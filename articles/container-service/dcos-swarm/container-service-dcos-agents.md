---
title: "пулы агентов aaaDC/OS для контейнера службы Azure | Документы Microsoft"
description: "Как работают пулы агентов открытых и закрытых hello с кластер контейнера службы Azure DC/OS"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: c7d3889db07cb9908e8b68b668bd8a14ef3c2552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a><span data-ttu-id="29c1d-104">Пулы агентов DC/OS для службы контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="29c1d-104">DC/OS agent pools for Azure Container Service</span></span>
<span data-ttu-id="29c1d-105">Кластеры DC/OS службы контейнеров Azure содержат узлы агентов в двух пулах —общедоступном и частном.</span><span class="sxs-lookup"><span data-stu-id="29c1d-105">DC/OS clusters in Azure Container Service contain agent nodes in two pools, a public pool and a private pool.</span></span> <span data-ttu-id="29c1d-106">Приложения могут развертываться tooeither пула, влияя на доступность между машинами в контейнере службы.</span><span class="sxs-lookup"><span data-stu-id="29c1d-106">An application can be deployed tooeither pool, affecting accessibility between machines in your container service.</span></span> <span data-ttu-id="29c1d-107">Hello машины могут быть предоставляется toohello Интернета (public) или внутренний (частный) сохраняются.</span><span class="sxs-lookup"><span data-stu-id="29c1d-107">hello machines can be exposed toohello internet (public) or kept internal (private).</span></span> <span data-ttu-id="29c1d-108">В этой статье приводятся общие сведения о причинах использования общедоступных и частных пулов.</span><span class="sxs-lookup"><span data-stu-id="29c1d-108">This article gives a brief overview of why there are public and private pools.</span></span>


* <span data-ttu-id="29c1d-109">**Частные агенты**: частные узлы агентов работают в сети без глобальной маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="29c1d-109">**Private agents**: Private agent nodes run through a non-routable network.</span></span> <span data-ttu-id="29c1d-110">Эта сеть доступна только из зоны hello администрирования или с помощью hello открытый зоны пограничный маршрутизатор.</span><span class="sxs-lookup"><span data-stu-id="29c1d-110">This network is only accessible from hello admin zone or through hello public zone edge router.</span></span> <span data-ttu-id="29c1d-111">По умолчанию DC/OS запускает приложения на частных узлах агента.</span><span class="sxs-lookup"><span data-stu-id="29c1d-111">By default, DC/OS launches apps on private agent nodes.</span></span> 

* <span data-ttu-id="29c1d-112">**Общедоступные агенты**: общедоступные узлы агентов выполняют приложения и службы DC/OS в общедоступной сети.</span><span class="sxs-lookup"><span data-stu-id="29c1d-112">**Public agents**: Public agent nodes run DC/OS apps and services through a publicly accessible network.</span></span> 

<span data-ttu-id="29c1d-113">Дополнительные сведения о сетевой безопасности контроллера домена/OS см. в разделе hello [документации DC/OS](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span><span class="sxs-lookup"><span data-stu-id="29c1d-113">For more information about DC/OS network security, see hello [DC/OS documentation](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span></span>

## <a name="deploy-agent-pools"></a><span data-ttu-id="29c1d-114">Развертывание пулов агента</span><span class="sxs-lookup"><span data-stu-id="29c1d-114">Deploy agent pools</span></span>

<span data-ttu-id="29c1d-115">пулы агентов DC/OS Hello в контейнере службы Azure создаются следующим образом:</span><span class="sxs-lookup"><span data-stu-id="29c1d-115">hello DC/OS agent pools In Azure Container Service are created as follows:</span></span>

* <span data-ttu-id="29c1d-116">Hello **закрытый пула** содержит hello число узлов агента, укажите время вы [развертывание кластера DC/OS hello](container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="29c1d-116">hello **private pool** contains hello number of agent nodes that you specify when you [deploy hello DC/OS cluster](container-service-deployment.md).</span></span> 

* <span data-ttu-id="29c1d-117">Hello **открытый пул** изначально содержит заранее заданное количество узлов агента.</span><span class="sxs-lookup"><span data-stu-id="29c1d-117">hello **public pool** initially contains a predetermined number of agent nodes.</span></span> <span data-ttu-id="29c1d-118">Этот пул добавляется автоматически при подготовке кластера DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="29c1d-118">This pool is added automatically when hello DC/OS cluster is provisioned.</span></span>

<span data-ttu-id="29c1d-119">закрытый пула Hello и открытые пула hello являются наборы масштабирования виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="29c1d-119">hello private pool and hello public pool are Azure virtual machine scale sets.</span></span> <span data-ttu-id="29c1d-120">Размер этих пулов можно изменить после развертывания.</span><span class="sxs-lookup"><span data-stu-id="29c1d-120">You can resize these pools after deployment.</span></span>

## <a name="use-agent-pools"></a><span data-ttu-id="29c1d-121">Использование пулов агента</span><span class="sxs-lookup"><span data-stu-id="29c1d-121">Use agent pools</span></span>
<span data-ttu-id="29c1d-122">По умолчанию **Marathon** развертывает все новые приложения toohello *закрытый* узлы агентов.</span><span class="sxs-lookup"><span data-stu-id="29c1d-122">By default, **Marathon** deploys any new application toohello *private* agent nodes.</span></span> <span data-ttu-id="29c1d-123">У вас есть tooexplicitly развертывание toohello приложения hello *открытый* узлов во время создания приложения hello hello.</span><span class="sxs-lookup"><span data-stu-id="29c1d-123">You have tooexplicitly deploy hello application toohello *public* nodes during hello creation of hello application.</span></span> <span data-ttu-id="29c1d-124">Выберите hello **необязательно** вкладку и введите **slave_public** для hello **принят ролей ресурса** значение.</span><span class="sxs-lookup"><span data-stu-id="29c1d-124">Select hello **Optional** tab and enter **slave_public** for hello **Accepted Resource Roles** value.</span></span> <span data-ttu-id="29c1d-125">Этот процесс описан в [здесь](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) и в hello [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) документации.</span><span class="sxs-lookup"><span data-stu-id="29c1d-125">This process is documented [here](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) and in hello [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29c1d-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="29c1d-126">Next steps</span></span>
* <span data-ttu-id="29c1d-127">Узнайте больше об [управлении контейнерами DC/OS](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="29c1d-127">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

* <span data-ttu-id="29c1d-128">Узнайте, каким образом слишком[открыть брандмауэр hello](container-service-enable-public-access.md) , предоставляемые Azure tooallow общего доступа tooyour DC/OS контейнеров.</span><span class="sxs-lookup"><span data-stu-id="29c1d-128">Learn how too[open hello firewall](container-service-enable-public-access.md) provided by Azure tooallow public access tooyour DC/OS containers.</span></span>

