---
title: "Мониторинг кластера DC/OS Azure с помощью Operations Management | Документация Майкрософт"
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
ms.openlocfilehash: 9b8f96b34b53982c469273a3df9751ceb7930d60
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a><span data-ttu-id="78263-103">Мониторинг кластера DC/OS в Службе контейнеров Azure с помощью Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="78263-103">Monitor an Azure Container Service DC/OS cluster with Operations Management Suite</span></span>

<span data-ttu-id="78263-104">Microsoft Operations Management Suite (OMS) — это облачное решение Майкрософт для управления ИТ-средой, которое помогает управлять локальной и облачной инфраструктурой и защищать ее.</span><span class="sxs-lookup"><span data-stu-id="78263-104">Microsoft Operations Management Suite (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="78263-105">Контейнер OMS — это решение в OMS Log Analytics, которое помогает просматривать сведения, касающиеся инвентаризации и производительности контейнеров, а также соответствующие журналы в одном расположении.</span><span class="sxs-lookup"><span data-stu-id="78263-105">Container Solution is a solution in OMS Log Analytics, which helps you view the container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="78263-106">Оно позволяет выполнять аудит и устранять неполадки контейнеров, просматривая журналы в централизованном расположении, а также находить контейнеры с высоким уровнем потребления ресурсов на узле.</span><span class="sxs-lookup"><span data-stu-id="78263-106">You can audit, troubleshoot containers by viewing the logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="78263-107">Дополнительные сведения об этом решении см. в статье [Решение "Контейнеры" (предварительная версия) в Log Analytics](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="78263-107">For more information about Container Solution, please refer to the [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="setting-up-oms-from-the-dcos-universe"></a><span data-ttu-id="78263-108">Настройка OMS в среде DC/ОS</span><span class="sxs-lookup"><span data-stu-id="78263-108">Setting up OMS from the DC/OS universe</span></span>


<span data-ttu-id="78263-109">В этой статье предполагается, что вы настроили DC/OS и развернули простые приложения веб-контейнера в кластере.</span><span class="sxs-lookup"><span data-stu-id="78263-109">This article assumes that you have set up an DC/OS and have deployed simple web container applications on the cluster.</span></span>

### <a name="pre-requisite"></a><span data-ttu-id="78263-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="78263-110">Pre-requisite</span></span>
- <span data-ttu-id="78263-111">[Подписка Microsoft Azure](https://azure.microsoft.com/free/) — ее можно получить бесплатно.</span><span class="sxs-lookup"><span data-stu-id="78263-111">[Microsoft Azure Subscription](https://azure.microsoft.com/free/) - You can get this for free.</span></span>  
- <span data-ttu-id="78263-112">Настройка рабочей области Microsoft OMS — см. раздел "Шаг 3" ниже.</span><span class="sxs-lookup"><span data-stu-id="78263-112">Microsoft OMS Workspace Setup - see "Step 3" below</span></span>
- <span data-ttu-id="78263-113">Установленный [интерфейс командной строки DC/OS](https://dcos.io/docs/1.8/usage/cli/install/).</span><span class="sxs-lookup"><span data-stu-id="78263-113">[DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) installed.</span></span>

1. <span data-ttu-id="78263-114">На панели мониторинга DC/OS щелкните "Вселенная" и выполните поиск по запросу "OMS", как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="78263-114">In the DC/OS dashboard, click on Universe and search for ‘OMS’ as shown below.</span></span>

![](media/container-service-monitoring-oms/image2.png)

2. <span data-ttu-id="78263-115">Щелкните **Install**(Установить).</span><span class="sxs-lookup"><span data-stu-id="78263-115">Click **Install**.</span></span> <span data-ttu-id="78263-116">Отобразится всплывающее окно со сведениями о версии OMS и кнопкой **Установить пакет** или **Advanced Installation** (Расширенная установка).</span><span class="sxs-lookup"><span data-stu-id="78263-116">You will see a pop up with the OMS version information and an **Install Package** or **Advanced Installation** button.</span></span> <span data-ttu-id="78263-117">Нажав кнопку **Advanced Installation** (Расширенная установка), вы перейдете на страницу **OMS specific configuration properties** (Свойства конфигурации OMS).</span><span class="sxs-lookup"><span data-stu-id="78263-117">When you click **Advanced Installation**, which leads you to the **OMS specific configuration properties** page.</span></span>

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. <span data-ttu-id="78263-118">Здесь вам будет предложено ввести `wsid` (идентификатор рабочей области OMS) и `wskey` (первичный ключ OMS для идентификатора рабочей области).</span><span class="sxs-lookup"><span data-stu-id="78263-118">Here, you will be asked to enter the `wsid` (the OMS workspace ID) and `wskey` (the OMS primary key for the workspace id).</span></span> <span data-ttu-id="78263-119">Чтобы получить `wsid` и `wskey`, необходимо создать учетную запись OMS, перейдя по адресу <https://mms.microsoft.com>. Следуйте инструкциям, чтобы создать учетную запись.</span><span class="sxs-lookup"><span data-stu-id="78263-119">To get both `wsid` and `wskey` you need to create an OMS account at <https://mms.microsoft.com>. Please follow the steps to create an account.</span></span> <span data-ttu-id="78263-120">После создания учетной записи необходимо получить `wsid` и `wskey`, щелкнув **Параметры**, **Подключенные источники**, а затем — **Серверы с Linux**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="78263-120">Once you are done creating the account, you need to obtain your `wsid` and `wskey` by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

4. <span data-ttu-id="78263-121">Выберите необходимое количество экземпляров OMS и нажмите кнопку "Просмотреть и установить".</span><span class="sxs-lookup"><span data-stu-id="78263-121">Select the number you OMS instances that you want and click the ‘Review and Install’ button.</span></span> <span data-ttu-id="78263-122">Как правило, требуется количество экземпляров OMS, равное количеству виртуальных машин в кластере агента.</span><span class="sxs-lookup"><span data-stu-id="78263-122">Typically, you will want to have the number of OMS instances equal to the number of VM’s you have in your agent cluster.</span></span> <span data-ttu-id="78263-123">Агент OMS для Linux устанавливается в качестве отдельных контейнеров на каждой виртуальной машине, о которой необходимо собирать сведения для мониторинга и ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="78263-123">OMS Agent for Linux is installs as individual containers on each VM that it wants to collect information for monitoring and logging information.</span></span>

## <a name="setting-up-a-simple-oms-dashboard"></a><span data-ttu-id="78263-124">Настройка простой панели мониторинга OMS</span><span class="sxs-lookup"><span data-stu-id="78263-124">Setting up a simple OMS dashboard</span></span>

<span data-ttu-id="78263-125">Сразу после установки агента OMS для Linux на виртуальных машинах необходимо настроить панель мониторинга OMS.</span><span class="sxs-lookup"><span data-stu-id="78263-125">Once you have installed the OMS Agent for Linux on the VMs, next step is to set up the OMS dashboard.</span></span> <span data-ttu-id="78263-126">Это можно сделать двумя способами: на портале OMS или портале Azure.</span><span class="sxs-lookup"><span data-stu-id="78263-126">There are two ways to do this: OMS Portal or Azure Portal.</span></span>

### <a name="oms-portal"></a><span data-ttu-id="78263-127">Портал OMS</span><span class="sxs-lookup"><span data-stu-id="78263-127">OMS Portal</span></span> 

<span data-ttu-id="78263-128">Войдите на портал OMS (<https://mms.microsoft.com>) и выберите **Коллекция решений**.</span><span class="sxs-lookup"><span data-stu-id="78263-128">Log in to the OMS portal (<https://mms.microsoft.com>) and go to the **Solution Gallery**.</span></span>

![](media/container-service-monitoring-oms/image6.png)

<span data-ttu-id="78263-129">Войдя в **коллекцию решений**, выберите **Контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="78263-129">Once you are in the **Solution Gallery**, select **Containers**.</span></span>

![](media/container-service-monitoring-oms/image7.png)

<span data-ttu-id="78263-130">После выбора решения контейнера на странице обзорной панели мониторинга OMS отобразится плитка.</span><span class="sxs-lookup"><span data-stu-id="78263-130">Once you’ve selected the Container Solution, you will see the tile on the OMS Overview Dashboard page.</span></span> <span data-ttu-id="78263-131">Как только принятые данные контейнера будут проиндексированы, вы увидите плитку, заполненную сведениями на плитках представления решения.</span><span class="sxs-lookup"><span data-stu-id="78263-131">Once the ingested container data is indexed, you will see the tile populated with information on the solution view tiles.</span></span>

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a><span data-ttu-id="78263-132">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="78263-132">Azure Portal</span></span> 

<span data-ttu-id="78263-133">Войдите на портал Azure по адресу <https://portal.microsoft.com/>.</span><span class="sxs-lookup"><span data-stu-id="78263-133">Login to Azure portal at <https://portal.microsoft.com/>.</span></span> <span data-ttu-id="78263-134">Выберите **Marketplace**, **Мониторинг и управление** и **Показать все**.</span><span class="sxs-lookup"><span data-stu-id="78263-134">Go to **Marketplace**, select **Monitoring + management** and click **See All**.</span></span> <span data-ttu-id="78263-135">Затем в поле поиска введите `containers`.</span><span class="sxs-lookup"><span data-stu-id="78263-135">Then Type `containers` in search.</span></span> <span data-ttu-id="78263-136">В результатах отобразится "контейнеры".</span><span class="sxs-lookup"><span data-stu-id="78263-136">You will see "containers" in the search results.</span></span> <span data-ttu-id="78263-137">Выберите **Контейнеры** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="78263-137">Select **Containers** and click **Create**.</span></span>

![](media/container-service-monitoring-oms/image9.png)

<span data-ttu-id="78263-138">После нажатия кнопки **Создать** вам будет предложено выбрать рабочую область.</span><span class="sxs-lookup"><span data-stu-id="78263-138">Once you click **Create**, it will ask you for your workspace.</span></span> <span data-ttu-id="78263-139">Выберите свою рабочую область, а если у вас ее нет, создайте ее.</span><span class="sxs-lookup"><span data-stu-id="78263-139">Select your workspace or if you do not have one, create a new workspace.</span></span>

![](media/container-service-monitoring-oms/image10.PNG)

<span data-ttu-id="78263-140">Выбрав рабочую область, щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="78263-140">Once you’ve selected your workspace, click **Create**.</span></span>

![](media/container-service-monitoring-oms/image11.png)

<span data-ttu-id="78263-141">Дополнительные сведения о решении контейнера OMS см. в статье [Решение "Контейнеры" (предварительная версия) в Log Analytics](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="78263-141">For more information about the OMS Container Solution, please refer to the [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

### <a name="how-to-scale-oms-agent-with-acs-dcos"></a><span data-ttu-id="78263-142">Масштабирование агента OMS с помощью среды DC/OS службы ACS</span><span class="sxs-lookup"><span data-stu-id="78263-142">How to scale OMS Agent with ACS DC/OS</span></span> 

<span data-ttu-id="78263-143">Если установлен агент OMS с недостаточным количеством фактических узлов или требуется выполнить масштабирование VMSS путем добавления дополнительных виртуальных машин, можно масштабировать службу `msoms`.</span><span class="sxs-lookup"><span data-stu-id="78263-143">In case you need to have installed OMS agent short of the actual node count or you are scaling up VMSS by adding more VM, you can do so by scaling the `msoms` service.</span></span>

<span data-ttu-id="78263-144">Вы можете перейти в Marathon или на вкладку пользовательских служб DC/OS и масштабировать количество узлов.</span><span class="sxs-lookup"><span data-stu-id="78263-144">You can either go to Marathon or the DC/OS UI Services tab and scale up your node count.</span></span>

![](media/container-service-monitoring-oms/image12.PNG)

<span data-ttu-id="78263-145">Другие узлы, на которых еще не установлен агент OMS, также будут развернуты.</span><span class="sxs-lookup"><span data-stu-id="78263-145">This will deploy to other nodes which have not yet deployed the OMS agent.</span></span>

## <a name="uninstall-ms-oms"></a><span data-ttu-id="78263-146">Удаление MS OMS</span><span class="sxs-lookup"><span data-stu-id="78263-146">Uninstall MS OMS</span></span>

<span data-ttu-id="78263-147">Чтобы удалить MS OMS, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="78263-147">To uninstall MS OMS enter the following command:</span></span>

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a><span data-ttu-id="78263-148">Сообщите нам!</span><span class="sxs-lookup"><span data-stu-id="78263-148">Let us know!!!</span></span>
<span data-ttu-id="78263-149">Что работает?</span><span class="sxs-lookup"><span data-stu-id="78263-149">What works?</span></span> <span data-ttu-id="78263-150">Чего не хватает?</span><span class="sxs-lookup"><span data-stu-id="78263-150">What is missing?</span></span> <span data-ttu-id="78263-151">Что еще необходимо улучшить, чтобы этот инструмент был полезным для вас?</span><span class="sxs-lookup"><span data-stu-id="78263-151">What else do you need for this to be useful for you?</span></span> <span data-ttu-id="78263-152">Сообщите нам по адресу <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span><span class="sxs-lookup"><span data-stu-id="78263-152">Let us know at <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="78263-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="78263-153">Next steps</span></span>

 <span data-ttu-id="78263-154">Теперь, когда вы настроили OMS для мониторинга контейнеров, [просмотрите свою панель мониторинга контейнера](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="78263-154">Now that you have set up OMS to monitor your containers,[see your container dashboard](../../log-analytics/log-analytics-containers.md).</span></span>
