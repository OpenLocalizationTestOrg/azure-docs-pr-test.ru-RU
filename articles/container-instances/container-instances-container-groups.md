---
title: "Группы контейнера экземпляры контейнером aaaAzure"
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
ms.openlocfilehash: 2b0e784609979045c8f77d7b6d0987ec3fee714c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="container-groups-in-azure-container-instances"></a><span data-ttu-id="d9d39-103">Группы контейнеров в службе "Экземпляры контейнеров Azure"</span><span class="sxs-lookup"><span data-stu-id="d9d39-103">Container Groups in Azure Container Instances</span></span>

<span data-ttu-id="d9d39-104">ресурс верхнего уровня Hello в экземплярах контейнера Azure — это группа контейнера.</span><span class="sxs-lookup"><span data-stu-id="d9d39-104">hello top-level resource in Azure Container Instances is a container group.</span></span> <span data-ttu-id="d9d39-105">В этой статье представлены сведения о группах контейнеров и о том, какие типы сценариев можно реализовать с их помощью.</span><span class="sxs-lookup"><span data-stu-id="d9d39-105">This article describes what container groups are and what types of scenarios they enable.</span></span>

## <a name="how-a-container-group-works"></a><span data-ttu-id="d9d39-106">Принцип работы группы контейнеров</span><span class="sxs-lookup"><span data-stu-id="d9d39-106">How a container group works</span></span>

<span data-ttu-id="d9d39-107">Группа контейнера — это коллекция контейнеров, которые могут планироваться на hello размещения машины и совместное использование жизненного цикла, локальной сети и тома хранилища.</span><span class="sxs-lookup"><span data-stu-id="d9d39-107">A container group is a collection of containers that get scheduled on hello same host machine and share a lifecycle, local network, and storage volumes.</span></span> <span data-ttu-id="d9d39-108">Это аналогично понятие toohello *pod* в [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) и [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span><span class="sxs-lookup"><span data-stu-id="d9d39-108">It is similar toohello concept of a *pod* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) and [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span></span>

<span data-ttu-id="d9d39-109">Hello следующей диаграмме показан пример контейнера группы, включающей несколько контейнеров.</span><span class="sxs-lookup"><span data-stu-id="d9d39-109">hello following diagram shows an example of a container group that includes multiple containers.</span></span>

![Пример групп контейнеров][container-groups-example]

<span data-ttu-id="d9d39-111">Обратите внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="d9d39-111">Note that:</span></span>

- <span data-ttu-id="d9d39-112">Группа Hello запланирован на одном хост-компьютере.</span><span class="sxs-lookup"><span data-stu-id="d9d39-112">hello group is scheduled on a single host machine.</span></span>
- <span data-ttu-id="d9d39-113">Группа Hello предоставляет один общий IP-адрес, с одной предоставленный порт.</span><span class="sxs-lookup"><span data-stu-id="d9d39-113">hello group exposes a single public IP address, with one exposed port.</span></span>
- <span data-ttu-id="d9d39-114">Hello группа состоит из двух контейнеров.</span><span class="sxs-lookup"><span data-stu-id="d9d39-114">hello group is made up of two containers.</span></span> <span data-ttu-id="d9d39-115">Один контейнер прослушивает порт 80, пока другие Здравствуй прослушивает порт 5000.</span><span class="sxs-lookup"><span data-stu-id="d9d39-115">One container listens on port 80, while hello other listens on port 5000.</span></span>
- <span data-ttu-id="d9d39-116">Группа Hello включает две общие папки файлов Azure как подключение тома, и каждый контейнер подключает одну из общих папок hello локально.</span><span class="sxs-lookup"><span data-stu-id="d9d39-116">hello group includes two Azure file shares as volume mounts, and each container mounts one of hello shares locally.</span></span>

### <a name="networking"></a><span data-ttu-id="d9d39-117">Сеть</span><span class="sxs-lookup"><span data-stu-id="d9d39-117">Networking</span></span>

<span data-ttu-id="d9d39-118">Группы контейнеров совместно используют IP-адрес и пространство имен порта для этого IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="d9d39-118">Container groups share an IP address and a port namespace on that IP address.</span></span> <span data-ttu-id="d9d39-119">tooreach внешних клиентов tooenable контейнер внутри группы hello, необходимо предоставить порт hello hello IP-адрес и из контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="d9d39-119">tooenable external clients tooreach a container within hello group, you must expose hello port on hello IP address and from hello container.</span></span> <span data-ttu-id="d9d39-120">Так как контейнеры в пределах группы hello используют порт пространства имен, сопоставление порта не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="d9d39-120">Because containers within hello group share a port namespace, port mapping is not supported.</span></span> <span data-ttu-id="d9d39-121">Контейнеры в пределах группы может получить доступ друг с другом через localhost на hello порты, которые предоставили, даже если эти порты не предоставляются в IP-адрес группы hello извне.</span><span class="sxs-lookup"><span data-stu-id="d9d39-121">Containers within a group can reach each other via localhost on hello ports that they have exposed, even if those ports are not exposed externally on hello group's IP address.</span></span>

### <a name="storage"></a><span data-ttu-id="d9d39-122">Хранилище</span><span class="sxs-lookup"><span data-stu-id="d9d39-122">Storage</span></span>

<span data-ttu-id="d9d39-123">Можно указать toomount внешних тома в пределах контейнера группы.</span><span class="sxs-lookup"><span data-stu-id="d9d39-123">You can specify external volumes toomount within a container group.</span></span> <span data-ttu-id="d9d39-124">Можно сопоставить эти тома в конкретных путей в пределах hello отдельных контейнеров в группе.</span><span class="sxs-lookup"><span data-stu-id="d9d39-124">You can map those volumes into specific paths within hello individual containers in a group.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="d9d39-125">Распространенные сценарии</span><span class="sxs-lookup"><span data-stu-id="d9d39-125">Common scenarios</span></span>

<span data-ttu-id="d9d39-126">Группы несколькими контейнера полезны в случаях, где нужно toodivide одной функциональной задачу в небольшое количество образов контейнера, которые могут доставляться различными группами и иметь отдельный ресурс требования.</span><span class="sxs-lookup"><span data-stu-id="d9d39-126">Multi-container groups are useful in cases where you want toodivide up a single functional task into a small number of container images, which can be delivered by different teams and have separate resource requirements.</span></span> <span data-ttu-id="d9d39-127">Пример использования может включать следующее:</span><span class="sxs-lookup"><span data-stu-id="d9d39-127">Example usage could include:</span></span>

- <span data-ttu-id="d9d39-128">Контейнер приложения и журнала.</span><span class="sxs-lookup"><span data-stu-id="d9d39-128">An application container and a logging container.</span></span> <span data-ttu-id="d9d39-129">Hello ведения журнала контейнера собирает журналы hello и выходные данные метрик, основное приложение hello и записывает их toolong длительного хранения.</span><span class="sxs-lookup"><span data-stu-id="d9d39-129">hello logging container collects hello logs and metrics output by hello main application and writes them toolong-term storage.</span></span>
- <span data-ttu-id="d9d39-130">Контейнер приложения и мониторинга.</span><span class="sxs-lookup"><span data-stu-id="d9d39-130">An application and a monitoring container.</span></span> <span data-ttu-id="d9d39-131">Hello периодически мониторинга контейнер делает tooensure запроса toohello приложения что он работает и правильно ли и выдает предупреждение, если это не так.</span><span class="sxs-lookup"><span data-stu-id="d9d39-131">hello monitoring container periodically makes a request toohello application tooensure that it's running and responding correctly and raises an alert if it's not.</span></span>
- <span data-ttu-id="d9d39-132">Контейнер, обслуживающий веб-приложения и контейнер извлекать последнее содержимое hello из системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="d9d39-132">A container serving a web application and a container pulling hello latest content from source control.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9d39-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d9d39-133">Next steps</span></span>

<span data-ttu-id="d9d39-134">Узнайте, каким образом слишком[развертывания нескольких контейнер группы](container-instances-multi-container-group.md) с использованием шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="d9d39-134">Learn how too[deploy a multi-container group](container-instances-multi-container-group.md) with an Azure Resource Manager template.</span></span>

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png