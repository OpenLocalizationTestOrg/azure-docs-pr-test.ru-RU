---
title: "кластер aaaMonitor контейнера службы Azure с Sysdig | Документы Microsoft"
description: "Мониторинг кластера службы контейнеров Azure с помощью Sysdig."
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Контейнеры, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 72f2d3d6f6885f9876fa158b88aae58b84a4610f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a><span data-ttu-id="6a872-104">Мониторинг кластера службы контейнеров Azure с помощью Sysdig</span><span class="sxs-lookup"><span data-stu-id="6a872-104">Monitor an Azure Container Service cluster with Sysdig</span></span>
<span data-ttu-id="6a872-105">В этой статье описывается развертывание узлов Sysdig агенты tooall hello агента в кластере службы контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="6a872-105">In this article, we will deploy Sysdig agents tooall hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="6a872-106">Для работы с этой конфигурацией вам понадобится учетная запись с Sysdig.</span><span class="sxs-lookup"><span data-stu-id="6a872-106">You need an account with Sysdig for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6a872-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6a872-107">Prerequisites</span></span>
<span data-ttu-id="6a872-108">[Разверните](container-service-deployment.md) и [подключите](../container-service-connect.md) кластер, настроенный службой контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="6a872-108">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="6a872-109">Просмотр hello [Marathon пользовательского интерфейса](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="6a872-109">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="6a872-110">Go слишком[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset Sysdig облачной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6a872-110">Go too[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset up a Sysdig cloud account.</span></span> 

## <a name="sysdig"></a><span data-ttu-id="6a872-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="6a872-111">Sysdig</span></span>
<span data-ttu-id="6a872-112">Sysdig является службой мониторинга, которая позволяет вам toomonitor к контейнерам внутри кластера.</span><span class="sxs-lookup"><span data-stu-id="6a872-112">Sysdig is a monitoring service that allows you toomonitor your containers within your cluster.</span></span> <span data-ttu-id="6a872-113">Sysdig известен toohelp способы устранения неполадок, но также имеет базовые показатели мониторинга для ЦП, сети, памяти и ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="6a872-113">Sysdig is known toohelp with troubleshooting but it also has your basic monitoring metrics for CPU, Networking, Memory, and I/O.</span></span> <span data-ttu-id="6a872-114">Sysdig позволяет легко toosee работе какие контейнеры hello hardest или по существу, используя hello большинство памяти и ЦП.</span><span class="sxs-lookup"><span data-stu-id="6a872-114">Sysdig makes it easy toosee which containers are working hello hardest or essentially using hello most memory and CPU.</span></span> <span data-ttu-id="6a872-115">Это представление расположено hello раздела «Обзор», в котором в настоящее время находится в бета-версии.</span><span class="sxs-lookup"><span data-stu-id="6a872-115">This view is in hello “Overview” section, which is currently in beta.</span></span> 

![Sysdig: пользовательский интерфейс](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a><span data-ttu-id="6a872-117">Настройка развертывания Sysdig с помощью Marathon</span><span class="sxs-lookup"><span data-stu-id="6a872-117">Configure a Sysdig deployment with Marathon</span></span>
<span data-ttu-id="6a872-118">Эти действия демонстрируют, как tooconfigure и развернуть кластер tooyour Sysdig приложений с Marathon.</span><span class="sxs-lookup"><span data-stu-id="6a872-118">These steps will show you how tooconfigure and deploy Sysdig applications tooyour cluster with Marathon.</span></span> 

<span data-ttu-id="6a872-119">Доступ к Интерфейсу DC/OS через [http://localhost: 80 /](http://localhost:80/) один раз в hello DC/OS пользовательского интерфейса выберите toohello «Среда», на hello вниз, влево и выполните поиск «Sysdig».</span><span class="sxs-lookup"><span data-stu-id="6a872-119">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in hello DC/OS UI navigate toohello "Universe", which is on hello bottom left and then search for "Sysdig."</span></span>

![Sysdig: раздел "Universe" (Вселенная) DC/OS](./media/container-service-monitoring-sysdig/sysdig1.png)

<span data-ttu-id="6a872-121">Теперь конфигурация hello toocomplete необходимо Sysdig облачной учетной записи или бесплатную пробную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="6a872-121">Now toocomplete hello configuration you need a Sysdig cloud account or a free trial account.</span></span> <span data-ttu-id="6a872-122">После входа в toohello Sysdig облачные и веб-сайт, щелкните имя пользователя, и на странице приветствия вы увидите «Ключа доступа.»</span><span class="sxs-lookup"><span data-stu-id="6a872-122">Once you're logged in toohello Sysdig cloud website, click on your user name, and on hello page you should see your "Access Key."</span></span> 

![Sysdig: ключ API](./media/container-service-monitoring-sysdig/sysdig2.png) 

<span data-ttu-id="6a872-124">Далее введите ключ доступа в конфигурации Sysdig hello в hello вселенной DC/OS.</span><span class="sxs-lookup"><span data-stu-id="6a872-124">Next enter your Access Key into hello Sysdig configuration within hello DC/OS Universe.</span></span> 

![Конфигурация Sysdig в hello вселенной DC/OS](./media/container-service-monitoring-sysdig/sysdig3.png)

<span data-ttu-id="6a872-126">Теперь установите too10000000 экземпляров hello так, чтобы каждый раз при добавлении нового узла кластера toohello Sysdig будет автоматически развернуть агент toothat нового узла.</span><span class="sxs-lookup"><span data-stu-id="6a872-126">Now set hello instances too10000000 so whenever a new node is added toohello cluster Sysdig will automatically deploy an agent toothat new node.</span></span> <span data-ttu-id="6a872-127">Это промежуточное решение toomake том, что Sysdig развернет tooall новых агентов в пределах кластера hello.</span><span class="sxs-lookup"><span data-stu-id="6a872-127">This is an interim solution toomake sure Sysdig will deploy tooall new agents within hello cluster.</span></span> 

![Конфигурация Sysdig в hello контроллера домена, среда операционной системы-экземпляров](./media/container-service-monitoring-sysdig/sysdig4.png)

<span data-ttu-id="6a872-129">После установки пакета hello Перейдите назад toohello Sysdig пользовательского интерфейса, и вы будете может tooexplore hello различных показателями для контейнеров hello в пределах кластера.</span><span class="sxs-lookup"><span data-stu-id="6a872-129">Once you've installed hello package navigate back toohello Sysdig UI and you'll be able tooexplore hello different usage metrics for hello containers within your cluster.</span></span> 

<span data-ttu-id="6a872-130">Вы также можете установить панели мониторинга Mesos и Marathon с помощью [мастера создания панелей мониторинга](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="6a872-130">You can also install Mesos and Marathon specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
