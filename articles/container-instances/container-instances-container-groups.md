---
title: "Группы контейнеров в службе \"Экземпляры контейнеров Azure\""
description: "Основные сведения о работе групп контейнеров в службе \"Экземпляры контейнеров Azure\""
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 25eab41c3f0c986bcce33123f86f4c9638b77191
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="container-groups-in-azure-container-instances"></a><span data-ttu-id="dfbfd-103">Группы контейнеров в службе "Экземпляры контейнеров Azure"</span><span class="sxs-lookup"><span data-stu-id="dfbfd-103">Container Groups in Azure Container Instances</span></span>

<span data-ttu-id="dfbfd-104">Ресурс верхнего уровня в службе "Экземпляры контейнеров Azure" — это группа контейнеров.</span><span class="sxs-lookup"><span data-stu-id="dfbfd-104">The top-level resource in Azure Container Instances is a container group.</span></span> <span data-ttu-id="dfbfd-105">В этой статье представлены сведения о группах контейнеров и о том, какие типы сценариев можно реализовать с их помощью.</span><span class="sxs-lookup"><span data-stu-id="dfbfd-105">This article describes what container groups are and what types of scenarios they enable.</span></span>

## <a name="how-a-container-group-works"></a><span data-ttu-id="dfbfd-106">Принцип работы группы контейнеров</span><span class="sxs-lookup"><span data-stu-id="dfbfd-106">How a container group works</span></span>

<span data-ttu-id="dfbfd-107">Группа контейнеров — это набор контейнеров, которые можно планировать на одном хост-компьютере и которые могут разделять один жизненный цикл, локальную сеть и тома хранилища.</span><span class="sxs-lookup"><span data-stu-id="dfbfd-107">A container group is a collection of containers that get scheduled on the same host machine and share a lifecycle, local network, and storage volumes.</span></span> <span data-ttu-id="dfbfd-108">Они похожи на концепцию *pod* в [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) и [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span><span class="sxs-lookup"><span data-stu-id="dfbfd-108">It is similar to the concept of a *pod* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) and [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span></span>

<span data-ttu-id="dfbfd-109">На схеме ниже показан пример группы контейнеров, включающей несколько контейнеров.</span><span class="sxs-lookup"><span data-stu-id="dfbfd-109">The following diagram shows an example of a container group that includes multiple containers.</span></span>

![Пример групп контейнеров][container-groups-example]

<span data-ttu-id="dfbfd-111">Обратите внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="dfbfd-111">Note that:</span></span>

- <span data-ttu-id="dfbfd-112">Группа планируется на одном хост-компьютере.</span><span class="sxs-lookup"><span data-stu-id="dfbfd-112">The group is scheduled on a single host machine.</span></span>
- <span data-ttu-id="dfbfd-113">Она предоставляет один общедоступный IP-адрес с одним предоставленным портом.</span><span class="sxs-lookup"><span data-stu-id="dfbfd-113">The group exposes a single public IP address, with one exposed port.</span></span>
- <span data-ttu-id="dfbfd-114">Группа состоит из двух контейнеров.</span><span class="sxs-lookup"><span data-stu-id="dfbfd-114">The group is made up of two containers.</span></span> <span data-ttu-id="dfbfd-115">Один контейнер ожидает передачи данных на порте 80, а другой — на порте 5000.</span><span class="sxs-lookup"><span data-stu-id="dfbfd-115">One container listens on port 80, while the other listens on port 5000.</span></span>
- <span data-ttu-id="dfbfd-116">Группа включает два общих файловых ресурса Azure в качестве подключенных томов, а к каждому контейнеру локально подключен один из общих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="dfbfd-116">The group includes two Azure file shares as volume mounts, and each container mounts one of the shares locally.</span></span>

### <a name="networking"></a><span data-ttu-id="dfbfd-117">Сеть</span><span class="sxs-lookup"><span data-stu-id="dfbfd-117">Networking</span></span>

<span data-ttu-id="dfbfd-118">Группы контейнеров совместно используют IP-адрес и пространство имен порта для этого IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="dfbfd-118">Container groups share an IP address and a port namespace on that IP address.</span></span> <span data-ttu-id="dfbfd-119">Чтобы внешние клиенты могли получить доступ к контейнеру в группе, необходимо предоставить порт по IP-адресу и из контейнера.</span><span class="sxs-lookup"><span data-stu-id="dfbfd-119">To enable external clients to reach a container within the group, you must expose the port on the IP address and from the container.</span></span> <span data-ttu-id="dfbfd-120">Так как контейнеры в группе совместно используют пространство имен порта, сопоставление портов не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="dfbfd-120">Because containers within the group share a port namespace, port mapping is not supported.</span></span> <span data-ttu-id="dfbfd-121">Контейнеры в пределах группы могут взаимодействовать через локальный узел на предоставленных портах, даже если эти порты не предоставлены извне по IP-адресу группы.</span><span class="sxs-lookup"><span data-stu-id="dfbfd-121">Containers within a group can reach each other via localhost on the ports that they have exposed, even if those ports are not exposed externally on the group's IP address.</span></span>

### <a name="storage"></a><span data-ttu-id="dfbfd-122">Хранилище</span><span class="sxs-lookup"><span data-stu-id="dfbfd-122">Storage</span></span>

<span data-ttu-id="dfbfd-123">Вы можете указать внешние тома для подключения в пределах группы контейнеров.</span><span class="sxs-lookup"><span data-stu-id="dfbfd-123">You can specify external volumes to mount within a container group.</span></span> <span data-ttu-id="dfbfd-124">Эти тома можно сопоставить с конкретными путями в пределах отдельных контейнеров в группе.</span><span class="sxs-lookup"><span data-stu-id="dfbfd-124">You can map those volumes into specific paths within the individual containers in a group.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="dfbfd-125">Распространенные сценарии</span><span class="sxs-lookup"><span data-stu-id="dfbfd-125">Common scenarios</span></span>

<span data-ttu-id="dfbfd-126">Группы с несколькими контейнерами полезны, если требуется разделить одну функциональную задачу на небольшое количество образов контейнера, которые могут доставляться различными группами и иметь отдельные требования к ресурсам.</span><span class="sxs-lookup"><span data-stu-id="dfbfd-126">Multi-container groups are useful in cases where you want to divide up a single functional task into a small number of container images, which can be delivered by different teams and have separate resource requirements.</span></span> <span data-ttu-id="dfbfd-127">Пример использования может включать следующее:</span><span class="sxs-lookup"><span data-stu-id="dfbfd-127">Example usage could include:</span></span>

- <span data-ttu-id="dfbfd-128">Контейнер приложения и журнала.</span><span class="sxs-lookup"><span data-stu-id="dfbfd-128">An application container and a logging container.</span></span> <span data-ttu-id="dfbfd-129">Контейнер журнала собирает журналы и выходные данные метрик для основного приложения и записывает их в хранилище для долговременного хранения.</span><span class="sxs-lookup"><span data-stu-id="dfbfd-129">The logging container collects the logs and metrics output by the main application and writes them to long-term storage.</span></span>
- <span data-ttu-id="dfbfd-130">Контейнер приложения и мониторинга.</span><span class="sxs-lookup"><span data-stu-id="dfbfd-130">An application and a monitoring container.</span></span> <span data-ttu-id="dfbfd-131">Контейнер мониторинга периодически выполняет запрос к приложению, чтобы убедиться, что оно правильно работает и отвечает, и выдает предупреждение, если это не так.</span><span class="sxs-lookup"><span data-stu-id="dfbfd-131">The monitoring container periodically makes a request to the application to ensure that it's running and responding correctly and raises an alert if it's not.</span></span>
- <span data-ttu-id="dfbfd-132">Контейнер, обслуживающий веб-приложение, и контейнер, извлекающий последнее содержимое из системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="dfbfd-132">A container serving a web application and a container pulling the latest content from source control.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfbfd-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dfbfd-133">Next steps</span></span>

<span data-ttu-id="dfbfd-134">Узнайте, как [развертывать группу с несколькими контейнерами](container-instances-multi-container-group.md) с использованием шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dfbfd-134">Learn how to [deploy a multi-container group](container-instances-multi-container-group.md) with an Azure Resource Manager template.</span></span>

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png