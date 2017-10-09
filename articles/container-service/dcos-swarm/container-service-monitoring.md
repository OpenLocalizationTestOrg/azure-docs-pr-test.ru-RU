---
title: "кластер Azure DC/OS aaaMonitor - Datadog | Документы Microsoft"
description: "Мониторинг кластера службы контейнеров Azure с помощью Datadog. Использование hello DC/OS web пользовательского интерфейса toodeploy hello Datadog агенты tooyour кластера."
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Контейнеры, DC/OS, Docker Swarm, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 07/28/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 10268c04b5c2ef393429e706ed4a467fff80f718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a><span data-ttu-id="45cfe-105">Мониторинг кластера DC/OS в Службе контейнеров Azure с помощью Datadog</span><span class="sxs-lookup"><span data-stu-id="45cfe-105">Monitor an Azure Container Service DC/OS cluster with Datadog</span></span>
<span data-ttu-id="45cfe-106">В этой статье описывается развертывание узлов Datadog агенты tooall hello агента в кластере службы контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="45cfe-106">In this article we will deploy Datadog agents tooall hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="45cfe-107">Для работы с этой конфигурацией вам понадобится учетная запись с Datadog.</span><span class="sxs-lookup"><span data-stu-id="45cfe-107">You will need an account with Datadog for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="45cfe-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="45cfe-108">Prerequisites</span></span>
<span data-ttu-id="45cfe-109">[Разверните](container-service-deployment.md) и [подключите](../container-service-connect.md) кластер, настроенный службой контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="45cfe-109">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="45cfe-110">Просмотр hello [Marathon пользовательского интерфейса](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="45cfe-110">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="45cfe-111">Go слишком[http://datadoghq.com](http://datadoghq.com) tooset Datadog учетной записи.</span><span class="sxs-lookup"><span data-stu-id="45cfe-111">Go too[http://datadoghq.com](http://datadoghq.com) tooset up a Datadog account.</span></span> 

## <a name="datadog"></a><span data-ttu-id="45cfe-112">Datadog</span><span class="sxs-lookup"><span data-stu-id="45cfe-112">Datadog</span></span>
<span data-ttu-id="45cfe-113">Datadog представляет собой службу мониторинга, которая собирает данные мониторинга из контейнеров в кластере службы контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="45cfe-113">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="45cfe-114">Datadog имеет панель мониторинга интеграции с Docker, в которой вы можете увидеть некоторые метрики своих контейнеров.</span><span class="sxs-lookup"><span data-stu-id="45cfe-114">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="45cfe-115">Метрики контейнеров собраны в несколько групп: ЦП, память, сеть и ввод-вывод.</span><span class="sxs-lookup"><span data-stu-id="45cfe-115">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="45cfe-116">Datadog разделяет метрики по контейнерам и образам.</span><span class="sxs-lookup"><span data-stu-id="45cfe-116">Datadog splits metrics into containers and images.</span></span> <span data-ttu-id="45cfe-117">Примером какие hello пользовательского интерфейса похоже для ЦП использования ниже.</span><span class="sxs-lookup"><span data-stu-id="45cfe-117">An example of what hello UI looks like for CPU usage is below.</span></span>

![Пользовательский интерфейс Datadog](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a><span data-ttu-id="45cfe-119">Настройка развертывания Datadog с помощью Marathon</span><span class="sxs-lookup"><span data-stu-id="45cfe-119">Configure a Datadog deployment with Marathon</span></span>
<span data-ttu-id="45cfe-120">Эти действия демонстрируют, как tooconfigure и развернуть кластер tooyour Datadog приложений с Marathon.</span><span class="sxs-lookup"><span data-stu-id="45cfe-120">These steps will show you how tooconfigure and deploy Datadog applications tooyour cluster with Marathon.</span></span> 

<span data-ttu-id="45cfe-121">Откройте пользовательский интерфейс DC/OS по адресу [http://localhost:80/](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="45cfe-121">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="45cfe-122">Один раз в hello перейдите пользовательского интерфейса DC/OS toohello «Среда», находящийся на hello вниз, влево и выполните поиск «Datadog» и нажмите кнопку «Установить».</span><span class="sxs-lookup"><span data-stu-id="45cfe-122">Once in hello DC/OS UI navigate toohello "Universe" which is on hello bottom left and then search for "Datadog" and click "Install."</span></span>

![Пакет Datadog в hello вселенной DC/OS](./media/container-service-monitoring/datadog1.png)

<span data-ttu-id="45cfe-124">Теперь конфигурация hello toocomplete, вам потребуется учетной записи Datadog или бесплатную пробную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="45cfe-124">Now toocomplete hello configuration you will need a Datadog account or a free trial account.</span></span> <span data-ttu-id="45cfe-125">После входа в веб-сайт Datadog toohello найдите toohello влево и перейти tooIntegrations ->, затем [API-интерфейсы](https://app.datadoghq.com/account/settings#api).</span><span class="sxs-lookup"><span data-stu-id="45cfe-125">Once you're logged in toohello Datadog website look toohello left and go tooIntegrations -> then [APIs](https://app.datadoghq.com/account/settings#api).</span></span> 

![Ключ API Datadog](./media/container-service-monitoring/datadog2.png)

<span data-ttu-id="45cfe-127">Затем введите ваш ключ API в конфигурацию Datadog hello внутри hello вселенной DC/OS.</span><span class="sxs-lookup"><span data-stu-id="45cfe-127">Next enter your API key into hello Datadog configuration within hello DC/OS Universe.</span></span> 

![Конфигурация Datadog в hello вселенной DC/OS](./media/container-service-monitoring/datadog3.png) 

<span data-ttu-id="45cfe-129">В hello выше конфигурации экземпляров устанавливаются too10000000, поэтому каждый раз при добавлении нового узла кластера toohello Datadog автоматически развертывать узел toothat агента.</span><span class="sxs-lookup"><span data-stu-id="45cfe-129">In hello above configuration instances are set too10000000 so whenever a new node is added toohello cluster Datadog will automatically deploy an agent toothat node.</span></span> <span data-ttu-id="45cfe-130">Это промежуточное решение.</span><span class="sxs-lookup"><span data-stu-id="45cfe-130">This is an interim solution.</span></span> <span data-ttu-id="45cfe-131">После установки пакета hello следует перейти назад toohello Datadog веб-сайта и найти «[панелей мониторинга](https://app.datadoghq.com/dash/list).»</span><span class="sxs-lookup"><span data-stu-id="45cfe-131">Once you've installed hello package you should navigate back toohello Datadog website and find "[Dashboards](https://app.datadoghq.com/dash/list)."</span></span> <span data-ttu-id="45cfe-132">Здесь вы увидите пользовательские панели мониторинга и панели интеграции.</span><span class="sxs-lookup"><span data-stu-id="45cfe-132">From there you will see Custom and Integration Dashboards.</span></span> <span data-ttu-id="45cfe-133">Hello [Docker мониторинга](https://app.datadoghq.com/screen/integration/docker) будет иметь все метрики контейнера hello, необходимые для мониторинга кластера.</span><span class="sxs-lookup"><span data-stu-id="45cfe-133">hello [Docker dashboard](https://app.datadoghq.com/screen/integration/docker) will have all hello container metrics you need for monitoring your cluster.</span></span> 

