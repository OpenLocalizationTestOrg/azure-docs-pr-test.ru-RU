---
title: "кластер Azure DC/OS aaaMonitor - операций управления | Документы Microsoft"
description: "Мониторинг кластера DC/OS в Службе контейнеров Azure с помощью Microsoft Operations Management Suite."
services: container-service
documentationcenter: 
author: keikhara
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 11/17/2016
ms.author: keikhara
ms.custom: mvc
ms.openlocfilehash: 0ebfa3ba3cef8f0205b15731b0e91f5b304bc8fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a><span data-ttu-id="824c1-103">Мониторинг кластера DC/OS в Службе контейнеров Azure с помощью Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="824c1-103">Monitor an Azure Container Service DC/OS cluster with Operations Management Suite</span></span>

<span data-ttu-id="824c1-104">Microsoft Operations Management Suite (OMS) — это облачное решение Майкрософт для управления ИТ-средой, которое помогает управлять локальной и облачной инфраструктурой и защищать ее.</span><span class="sxs-lookup"><span data-stu-id="824c1-104">Microsoft Operations Management Suite (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="824c1-105">Решение контейнер — это решение в аналитику журнала OMS, служащей для просмотра данных инвентаризации контейнера hello, производительности и журналов в одном месте.</span><span class="sxs-lookup"><span data-stu-id="824c1-105">Container Solution is a solution in OMS Log Analytics, which helps you view hello container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="824c1-106">Аудит, устранение неполадок контейнеры путем просмотра журналов hello в центральном расположении и найти шумный использование лишние контейнер на узле.</span><span class="sxs-lookup"><span data-stu-id="824c1-106">You can audit, troubleshoot containers by viewing hello logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="824c1-107">Дополнительные сведения о решении контейнера можно найти toothe [анализа журналов контейнера решение](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="824c1-107">For more information about Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="setting-up-oms-from-hello-dcos-universe"></a><span data-ttu-id="824c1-108">Установка OMS с контроллера домена/OS вселенной hello</span><span class="sxs-lookup"><span data-stu-id="824c1-108">Setting up OMS from hello DC/OS universe</span></span>


<span data-ttu-id="824c1-109">В этой статье предполагается, что настройки контроллера домена/OS и развертывания простого веб-приложения контейнера в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="824c1-109">This article assumes that you have set up an DC/OS and have deployed simple web container applications on hello cluster.</span></span>

### <a name="pre-requisite"></a><span data-ttu-id="824c1-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="824c1-110">Pre-requisite</span></span>
- <span data-ttu-id="824c1-111">[Подписка Microsoft Azure](https://azure.microsoft.com/free/) — ее можно получить бесплатно.</span><span class="sxs-lookup"><span data-stu-id="824c1-111">[Microsoft Azure Subscription](https://azure.microsoft.com/free/) - You can get this for free.</span></span>  
- <span data-ttu-id="824c1-112">Настройка рабочей области Microsoft OMS — см. раздел "Шаг 3" ниже.</span><span class="sxs-lookup"><span data-stu-id="824c1-112">Microsoft OMS Workspace Setup - see "Step 3" below</span></span>
- <span data-ttu-id="824c1-113">Установленный [интерфейс командной строки DC/OS](https://dcos.io/docs/1.8/usage/cli/install/).</span><span class="sxs-lookup"><span data-stu-id="824c1-113">[DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) installed.</span></span>

1. <span data-ttu-id="824c1-114">В панели мониторинга hello DC/OS щелкните вселенной и выполните поиск «OMS», как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="824c1-114">In hello DC/OS dashboard, click on Universe and search for ‘OMS’ as shown below.</span></span>

![](media/container-service-monitoring-oms/image2.png)

2. <span data-ttu-id="824c1-115">Щелкните **Install**(Установить).</span><span class="sxs-lookup"><span data-stu-id="824c1-115">Click **Install**.</span></span> <span data-ttu-id="824c1-116">Вы увидите pop вверх на сведения о версии OMS hello и **установить пакет** или **расширенный установки** кнопки.</span><span class="sxs-lookup"><span data-stu-id="824c1-116">You will see a pop up with hello OMS version information and an **Install Package** or **Advanced Installation** button.</span></span> <span data-ttu-id="824c1-117">При нажатии кнопки **расширенный установки**, который проводит toohello **OMS конкретной конфигурации свойства** страницы.</span><span class="sxs-lookup"><span data-stu-id="824c1-117">When you click **Advanced Installation**, which leads you toohello **OMS specific configuration properties** page.</span></span>

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. <span data-ttu-id="824c1-118">Здесь, будет выведено tooenter hello `wsid` (hello идентификатор рабочей области OMS) и `wskey` (hello OMS первичный ключ для hello идентификатор рабочей области).</span><span class="sxs-lookup"><span data-stu-id="824c1-118">Here, you will be asked tooenter hello `wsid` (hello OMS workspace ID) and `wskey` (hello OMS primary key for hello workspace id).</span></span> <span data-ttu-id="824c1-119">Оба tooget `wsid` и `wskey` требуется учетная запись OMS в toocreate <https://mms.microsoft.com>. Выполните шаги hello toocreate учетную запись.</span><span class="sxs-lookup"><span data-stu-id="824c1-119">tooget both `wsid` and `wskey` you need toocreate an OMS account at <https://mms.microsoft.com>. Please follow hello steps toocreate an account.</span></span> <span data-ttu-id="824c1-120">После завершения создания учетной записи hello, вам потребуется tooobtain вашей `wsid` и `wskey` , щелкнув **параметры**, затем **подключенные источники**, а затем **серверы Linux** , как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="824c1-120">Once you are done creating hello account, you need tooobtain your `wsid` and `wskey` by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

4. <span data-ttu-id="824c1-121">Выберите hello числа вы OMS экземпляров, необходимо и нажмите кнопку «Просмотреть и установить» hello.</span><span class="sxs-lookup"><span data-stu-id="824c1-121">Select hello number you OMS instances that you want and click hello ‘Review and Install’ button.</span></span> <span data-ttu-id="824c1-122">Как правило следует toohave hello число OMS экземпляры равны toohello количество Виртуальных машин в кластере агент.</span><span class="sxs-lookup"><span data-stu-id="824c1-122">Typically, you will want toohave hello number of OMS instances equal toohello number of VM’s you have in your agent cluster.</span></span> <span data-ttu-id="824c1-123">Агент OMS для Linux — устанавливает как отдельные контейнеры на каждой виртуальной Машине, что ему toocollect сведения для мониторинга и ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="824c1-123">OMS Agent for Linux is installs as individual containers on each VM that it wants toocollect information for monitoring and logging information.</span></span>

## <a name="setting-up-a-simple-oms-dashboard"></a><span data-ttu-id="824c1-124">Настройка простой панели мониторинга OMS</span><span class="sxs-lookup"><span data-stu-id="824c1-124">Setting up a simple OMS dashboard</span></span>

<span data-ttu-id="824c1-125">После установки hello агента OMS для Linux на виртуальных машинах hello, следующим шагом является tooset копирование hello мониторинга OMS.</span><span class="sxs-lookup"><span data-stu-id="824c1-125">Once you have installed hello OMS Agent for Linux on hello VMs, next step is tooset up hello OMS dashboard.</span></span> <span data-ttu-id="824c1-126">Существует два способа toodo это: портала OMS или портала Azure.</span><span class="sxs-lookup"><span data-stu-id="824c1-126">There are two ways toodo this: OMS Portal or Azure Portal.</span></span>

### <a name="oms-portal"></a><span data-ttu-id="824c1-127">Портал OMS</span><span class="sxs-lookup"><span data-stu-id="824c1-127">OMS Portal</span></span> 

<span data-ttu-id="824c1-128">Войдите в портал OMS toohello (<https://mms.microsoft.com>), а toohello **коллекции решений**.</span><span class="sxs-lookup"><span data-stu-id="824c1-128">Log in toohello OMS portal (<https://mms.microsoft.com>) and go toohello **Solution Gallery**.</span></span>

![](media/container-service-monitoring-oms/image6.png)

<span data-ttu-id="824c1-129">После входа в hello **коллекции решений**выберите **контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="824c1-129">Once you are in hello **Solution Gallery**, select **Containers**.</span></span>

![](media/container-service-monitoring-oms/image7.png)

<span data-ttu-id="824c1-130">После выбора hello контейнера решений, вы увидите плитку на странице панели мониторинга OMS Обзор hello hello.</span><span class="sxs-lookup"><span data-stu-id="824c1-130">Once you’ve selected hello Container Solution, you will see hello tile on hello OMS Overview Dashboard page.</span></span> <span data-ttu-id="824c1-131">После индексируется hello полученный контейнер данных, вы увидите плитку hello, заполненный данными на плитках решений представление.</span><span class="sxs-lookup"><span data-stu-id="824c1-131">Once hello ingested container data is indexed, you will see hello tile populated with information on the solution view tiles.</span></span>

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a><span data-ttu-id="824c1-132">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="824c1-132">Azure Portal</span></span> 

<span data-ttu-id="824c1-133">Портал tooAzure входа на <https://portal.microsoft.com/>.</span><span class="sxs-lookup"><span data-stu-id="824c1-133">Login tooAzure portal at <https://portal.microsoft.com/>.</span></span> <span data-ttu-id="824c1-134">Выберите **Marketplace**, **Мониторинг и управление** и **Показать все**.</span><span class="sxs-lookup"><span data-stu-id="824c1-134">Go to **Marketplace**, select **Monitoring + management** and click **See All**.</span></span> <span data-ttu-id="824c1-135">Затем в поле поиска введите `containers`.</span><span class="sxs-lookup"><span data-stu-id="824c1-135">Then Type `containers` in search.</span></span> <span data-ttu-id="824c1-136">Вы увидите «контейнеры» в результатах поиска hello.</span><span class="sxs-lookup"><span data-stu-id="824c1-136">You will see "containers" in hello search results.</span></span> <span data-ttu-id="824c1-137">Выберите **Контейнеры** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="824c1-137">Select **Containers** and click **Create**.</span></span>

![](media/container-service-monitoring-oms/image9.png)

<span data-ttu-id="824c1-138">После нажатия кнопки **Создать** вам будет предложено выбрать рабочую область.</span><span class="sxs-lookup"><span data-stu-id="824c1-138">Once you click **Create**, it will ask you for your workspace.</span></span> <span data-ttu-id="824c1-139">Выберите свою рабочую область, а если у вас ее нет, создайте ее.</span><span class="sxs-lookup"><span data-stu-id="824c1-139">Select your workspace or if you do not have one, create a new workspace.</span></span>

![](media/container-service-monitoring-oms/image10.PNG)

<span data-ttu-id="824c1-140">Выбрав рабочую область, щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="824c1-140">Once you’ve selected your workspace, click **Create**.</span></span>

![](media/container-service-monitoring-oms/image11.png)

<span data-ttu-id="824c1-141">Дополнительные сведения о hello контейнера решение OMS, можно найти toothe [анализа журналов контейнера решение](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="824c1-141">For more information about hello OMS Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

### <a name="how-tooscale-oms-agent-with-acs-dcos"></a><span data-ttu-id="824c1-142">Как tooscale агента OMS с ACS DC/OS</span><span class="sxs-lookup"><span data-stu-id="824c1-142">How tooscale OMS Agent with ACS DC/OS</span></span> 

<span data-ttu-id="824c1-143">В случае необходимости toohave установлен агент OMS во всех остальных случаях hello фактического числа или масштабирование VMSS путем добавления дополнительных виртуальных Машин, это можно сделать путем масштабирования hello `msoms` службы.</span><span class="sxs-lookup"><span data-stu-id="824c1-143">In case you need toohave installed OMS agent short of hello actual node count or you are scaling up VMSS by adding more VM, you can do so by scaling hello `msoms` service.</span></span>

<span data-ttu-id="824c1-144">Можно перейти tooMarathon или hello вкладку пользовательского интерфейса службы контроллера домена/OS и вертикальное масштабирование на число узлов.</span><span class="sxs-lookup"><span data-stu-id="824c1-144">You can either go tooMarathon or hello DC/OS UI Services tab and scale up your node count.</span></span>

![](media/container-service-monitoring-oms/image12.PNG)

<span data-ttu-id="824c1-145">Будет выполнено развертывание tooother узлов, которые еще не установлен агент OMS hello.</span><span class="sxs-lookup"><span data-stu-id="824c1-145">This will deploy tooother nodes which have not yet deployed hello OMS agent.</span></span>

## <a name="uninstall-ms-oms"></a><span data-ttu-id="824c1-146">Удаление MS OMS</span><span class="sxs-lookup"><span data-stu-id="824c1-146">Uninstall MS OMS</span></span>

<span data-ttu-id="824c1-147">toouninstall MS OMS введите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="824c1-147">toouninstall MS OMS enter hello following command:</span></span>

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a><span data-ttu-id="824c1-148">Сообщите нам!</span><span class="sxs-lookup"><span data-stu-id="824c1-148">Let us know!!!</span></span>
<span data-ttu-id="824c1-149">Что работает?</span><span class="sxs-lookup"><span data-stu-id="824c1-149">What works?</span></span> <span data-ttu-id="824c1-150">Чего не хватает?</span><span class="sxs-lookup"><span data-stu-id="824c1-150">What is missing?</span></span> <span data-ttu-id="824c1-151">Что еще необходимо для этого toobe полезным для вас?</span><span class="sxs-lookup"><span data-stu-id="824c1-151">What else do you need for this toobe useful for you?</span></span> <span data-ttu-id="824c1-152">Сообщите нам по адресу <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span><span class="sxs-lookup"><span data-stu-id="824c1-152">Let us know at <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="824c1-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="824c1-153">Next steps</span></span>

 <span data-ttu-id="824c1-154">Теперь, когда настройки OMS toomonitor вашей контейнеры[просмотра вашей информационной панели контейнера](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="824c1-154">Now that you have set up OMS toomonitor your containers,[see your container dashboard](../../log-analytics/log-analytics-containers.md).</span></span>
