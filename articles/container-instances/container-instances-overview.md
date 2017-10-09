---
title: "Обзор экземпляры контейнером aaaAzure | Azure документы"
description: "Общие сведения о службе \"Экземпляры контейнеров Azure\""
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
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: c0662ede1260b15d9841bfc2c3c4cec4c30338d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances"></a><span data-ttu-id="600a2-103">Экземпляры контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="600a2-103">Azure Container Instances</span></span>

<span data-ttu-id="600a2-104">Контейнеры быстро становятся hello предпочтительный способ toopackage, развертывания и управления облачных приложений.</span><span class="sxs-lookup"><span data-stu-id="600a2-104">Containers are quickly becoming hello preferred way toopackage, deploy, and manage cloud applications.</span></span> <span data-ttu-id="600a2-105">Экземпляры контейнером Azure предлагает hello самый быстрый и простой способ toorun контейнера в Azure, без необходимости tooprovision все виртуальные машины и без необходимости tooadopt более высокого уровня службы.</span><span class="sxs-lookup"><span data-stu-id="600a2-105">Azure Container Instances offers hello fastest and simplest way toorun a container in Azure, without having tooprovision any virtual machines and without having tooadopt a higher-level service.</span></span> 

<span data-ttu-id="600a2-106">Служба "Экземпляры контейнеров Azure" — идеальное решение для любых сценариев, которые могут выполняться в изолированных контейнерах, включая простые приложения, автоматизацию задач и задания сборки.</span><span class="sxs-lookup"><span data-stu-id="600a2-106">Azure Container Instances is a great solution for any scenario that can operate in isolated containers, including simple applications, task automation, and build jobs.</span></span> <span data-ttu-id="600a2-107">Для сценариев, где требуется для полного контейнера orchestration, включая службы обнаружения по нескольким контейнерам, автоматического масштабирования и обновлений скоординированного приложений, мы рекомендуем hello [контейнера службы Azure](https://docs.microsoft.com/azure/container-service/).</span><span class="sxs-lookup"><span data-stu-id="600a2-107">For scenarios where you need full container orchestration, including service discovery across multiple containers, automatic scaling, and coordinated application upgrades, we recommend hello [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

## <a name="fast-startup-times"></a><span data-ttu-id="600a2-108">Быстрый запуск</span><span class="sxs-lookup"><span data-stu-id="600a2-108">Fast startup times</span></span>

<span data-ttu-id="600a2-109">Контейнеры обеспечивают значительные преимущества для запуска по сравнению с виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="600a2-109">Containers offer significant startup benefits over virtual machines.</span></span> <span data-ttu-id="600a2-110">Экземпляры контейнером Azure можно начать использование контейнера в Azure, в секундах, без необходимости tooprovision hello и управление виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="600a2-110">With Azure Container Instances, you can start a container in Azure in seconds without hello need tooprovision and manage VMs.</span></span>

## <a name="hypervisor-level-security"></a><span data-ttu-id="600a2-111">Безопасность на уровне низкоуровневой оболочки</span><span class="sxs-lookup"><span data-stu-id="600a2-111">Hypervisor-level security</span></span>

<span data-ttu-id="600a2-112">Изначально контейнеры предоставляли изоляцию зависимостей приложения и возможность управления ресурсами, но не были достаточно защищены для использования в неблагоприятных мультитенантных средах.</span><span class="sxs-lookup"><span data-stu-id="600a2-112">Historically, containers have offered application dependency isolation and resource governance but have not been considered sufficiently hardened for hostile multi-tenant usage.</span></span> <span data-ttu-id="600a2-113">Служба "Экземпляры контейнеров Azure" изолирует приложение в контейнере, как на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="600a2-113">With Azure Container Instances, your application is as isolated in a container as it would be in a VM.</span></span>

## <a name="custom-sizes"></a><span data-ttu-id="600a2-114">Настраиваемые размеры</span><span class="sxs-lookup"><span data-stu-id="600a2-114">Custom sizes</span></span>

<span data-ttu-id="600a2-115">Контейнеры — обычно оптимизированного toorun только одно приложение, но hello конкретные нужды этих приложений может значительно отличаться.</span><span class="sxs-lookup"><span data-stu-id="600a2-115">Containers are typically optimized toorun just a single application, but hello exact needs of those applications can differ greatly.</span></span> <span data-ttu-id="600a2-116">Служба "Экземпляры контейнеров Azure" позволяет подать запрос с конкретными требованиями к ядрам ЦП и памяти.</span><span class="sxs-lookup"><span data-stu-id="600a2-116">With Azure Container Instances, you can request exactly what you need in terms of CPU cores and memory.</span></span> <span data-ttu-id="600a2-117">Вы платите зависимости можно запросить выставлен счет от hello во-вторых, чтобы мог точно оптимизировать расходы зависимости от потребностей.</span><span class="sxs-lookup"><span data-stu-id="600a2-117">You pay based on what you request, billed by hello second, so you can finely optimize your spending based on your needs.</span></span>

## <a name="public-ip-connectivity"></a><span data-ttu-id="600a2-118">Возможность подключения по общедоступному IP-адресу</span><span class="sxs-lookup"><span data-stu-id="600a2-118">Public IP connectivity</span></span>

<span data-ttu-id="600a2-119">Экземпляры контейнером Azure, можно предоставлять на контейнеры напрямую toohello Интернет, общий IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="600a2-119">With Azure Container Instances, you can expose your containers directly toohello internet with a public IP address.</span></span> <span data-ttu-id="600a2-120">В будущем hello мы разверните нашей сетевые возможности интеграции tooinclude с виртуальными сетями, загрузить балансировки нагрузки и других основных частей hello сетевой инфраструктуры Azure.</span><span class="sxs-lookup"><span data-stu-id="600a2-120">In hello future, we will expand our networking capabilities tooinclude integration with virtual networks, load balancers, and other core parts of hello Azure networking infrastructure.</span></span>

## <a name="persistent-storage"></a><span data-ttu-id="600a2-121">Постоянное хранилище</span><span class="sxs-lookup"><span data-stu-id="600a2-121">Persistent storage</span></span>

<span data-ttu-id="600a2-122">tooretrieve и сохранения состояния с экземплярами Azure контейнера, мы предлагаем прямое подключение Azure файлы общих папок.</span><span class="sxs-lookup"><span data-stu-id="600a2-122">tooretrieve and persist state with Azure Container Instances, we offer direct mounting of Azure files shares.</span></span>

## <a name="linux-and-windows-containers"></a><span data-ttu-id="600a2-123">Контейнеры Linux и Windows</span><span class="sxs-lookup"><span data-stu-id="600a2-123">Linux and Windows containers</span></span>

<span data-ttu-id="600a2-124">Экземпляры контейнером Azure можно запланировать в обоих окнах и контейнерами Linux с помощью hello же API-Интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="600a2-124">With Azure Container Instances, you can schedule both Windows and Linux containers with hello same API.</span></span> <span data-ttu-id="600a2-125">Просто указать hello базовый тип операционной системы и все остальные будут одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="600a2-125">Simply indicate hello base OS type and everything else is identical.</span></span>

## <a name="co-scheduled-groups"></a><span data-ttu-id="600a2-126">Общее расписание для групп</span><span class="sxs-lookup"><span data-stu-id="600a2-126">Co-scheduled groups</span></span>

<span data-ttu-id="600a2-127">Служба "Экземпляры контейнеров Azure" поддерживает установку расписания для многоконтейнерных групп, для которых задан один и тот же хост-компьютер, локальная сеть, хранилище и жизненный цикл.</span><span class="sxs-lookup"><span data-stu-id="600a2-127">Azure Container Instances supports scheduling of multi-container groups that share a host machine, local network, storage, and lifecycle.</span></span> <span data-ttu-id="600a2-128">Это позволяет вам toocombine основного приложения с другими разделами выступает в роли поддержки, например ведение журнала.</span><span class="sxs-lookup"><span data-stu-id="600a2-128">This enables you toocombine your main application with others acting in a supporting role, such as logging.</span></span>

## <a name="next-steps"></a><span data-ttu-id="600a2-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="600a2-129">Next steps</span></span>

<span data-ttu-id="600a2-130">Попробуйте выполнить развертывание tooAzure контейнера с помощью одной команды с помощью наших [краткого руководства](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="600a2-130">Try deploying a container tooAzure with a single command using our [quickstart guide](container-instances-quickstart.md).</span></span>
