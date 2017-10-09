---
title: "aaaAzure orchestration приложения Service Fabric исправление | Документы Microsoft"
description: "Приложение tooautomate операционной системы установку исправлений на кластер Service Fabric."
services: service-fabric
documentationcenter: .net
author: novino
manager: timlt
editor: 
ms.assetid: de7dacf5-4038-434a-a265-5d0de80a9b1d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/9/2017
ms.author: nachandr
ms.openlocfilehash: fbb89aa2ea418181ee908a01850178c113c462fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="patch-hello-windows-operating-system-in-your-service-fabric-cluster"></a><span data-ttu-id="32b6c-103">Исправление для операционной системы Windows hello кластера Service Fabric</span><span class="sxs-lookup"><span data-stu-id="32b6c-103">Patch hello Windows operating system in your Service Fabric cluster</span></span>

<span data-ttu-id="32b6c-104">Hello исправление orchestration приложение является приложением Azure Service Fabric, который автоматизирует установку исправлений на кластер Service Fabric в Azure без простоев операционной системы.</span><span class="sxs-lookup"><span data-stu-id="32b6c-104">hello patch orchestration application is an Azure Service Fabric application that automates operating system patching on a Service Fabric cluster on Azure without downtime.</span></span>

<span data-ttu-id="32b6c-105">orchestration приложение Hello исправление предоставляет hello ниже:</span><span class="sxs-lookup"><span data-stu-id="32b6c-105">hello patch orchestration app provides hello following:</span></span>

- <span data-ttu-id="32b6c-106">**Автоматическая установка обновлений операционной системы**.</span><span class="sxs-lookup"><span data-stu-id="32b6c-106">**Automatic operating system update installation**.</span></span> <span data-ttu-id="32b6c-107">Обновления операционной системы автоматически загружаются и устанавливаются.</span><span class="sxs-lookup"><span data-stu-id="32b6c-107">Operating system updates are automatically downloaded and installed.</span></span> <span data-ttu-id="32b6c-108">При необходимости узлы кластера перезагружаются без остановки его работы.</span><span class="sxs-lookup"><span data-stu-id="32b6c-108">Cluster nodes are rebooted as needed without cluster downtime.</span></span>

- <span data-ttu-id="32b6c-109">**Исправление с учетом состояния кластера и интеграция функций работоспособности**.</span><span class="sxs-lookup"><span data-stu-id="32b6c-109">**Cluster-aware patching and health integration**.</span></span> <span data-ttu-id="32b6c-110">Во время применения обновлений, приложение orchestration исправление hello отслеживает работоспособность hello hello узлов кластера.</span><span class="sxs-lookup"><span data-stu-id="32b6c-110">While applying updates, hello patch orchestration app monitors hello health of hello cluster nodes.</span></span> <span data-ttu-id="32b6c-111">Узлы кластера обновляются поочередно или по одному домену обновления за раз.</span><span class="sxs-lookup"><span data-stu-id="32b6c-111">Cluster nodes are upgraded one node at a time or one upgrade domain at a time.</span></span> <span data-ttu-id="32b6c-112">Если hello работоспособности кластера hello выходит из строя из-за выполнения процесса toohello исправления будет остановлена tooprevent aggravating проблема hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-112">If hello health of hello cluster goes down due toohello patching process, patching is stopped tooprevent aggravating hello problem.</span></span>

## <a name="internal-details-of-hello-app"></a><span data-ttu-id="32b6c-113">Внутренние сведения о приложение hello</span><span class="sxs-lookup"><span data-stu-id="32b6c-113">Internal details of hello app</span></span>

<span data-ttu-id="32b6c-114">orchestration приложение Hello patch состоит из hello следующие подкомпоненты:</span><span class="sxs-lookup"><span data-stu-id="32b6c-114">hello patch orchestration app is composed of hello following subcomponents:</span></span>

- <span data-ttu-id="32b6c-115">**Служба координатора** — эта служба с отслеживанием состояния отвечает за следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="32b6c-115">**Coordinator Service**: This stateful service is responsible for:</span></span>
    - <span data-ttu-id="32b6c-116">Согласование задания обновления Windows hello на весь кластер hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-116">Coordinating hello Windows Update job on hello entire cluster.</span></span>
    - <span data-ttu-id="32b6c-117">Хранение результатов hello завершенных операций обновления Windows.</span><span class="sxs-lookup"><span data-stu-id="32b6c-117">Storing hello result of completed Windows Update operations.</span></span>
- <span data-ttu-id="32b6c-118">**Служба агента узла** — это служба без отслеживания состояния, которая выполняется на всех узлах кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="32b6c-118">**Node Agent Service**: This stateless service runs on all Service Fabric cluster nodes.</span></span> <span data-ttu-id="32b6c-119">Hello служба отвечает за:</span><span class="sxs-lookup"><span data-stu-id="32b6c-119">hello service is responsible for:</span></span>
    - <span data-ttu-id="32b6c-120">Начальная загрузка hello NTService агента узла.</span><span class="sxs-lookup"><span data-stu-id="32b6c-120">Bootstrapping hello Node Agent NTService.</span></span>
    - <span data-ttu-id="32b6c-121">Мониторинг hello NTService агента узла.</span><span class="sxs-lookup"><span data-stu-id="32b6c-121">Monitoring hello Node Agent NTService.</span></span>
- <span data-ttu-id="32b6c-122">**Служба NTService агента узла** — служба Windows NT, которая выполняется с разрешением высокого уровня (СИСТЕМА).</span><span class="sxs-lookup"><span data-stu-id="32b6c-122">**Node Agent NTService**: This Windows NT service runs at a higher-level privilege (SYSTEM).</span></span> <span data-ttu-id="32b6c-123">Напротив hello служба агента узла и hello службы координатора запускать с привилегиями более низкого уровня (NETWORK SERVICE).</span><span class="sxs-lookup"><span data-stu-id="32b6c-123">In contrast, hello Node Agent Service and hello Coordinator Service run at a lower-level privilege (NETWORK SERVICE).</span></span> <span data-ttu-id="32b6c-124">Служба Hello несет ответственность за выполнение после задания центра обновления Windows на всех узлах кластера hello hello:</span><span class="sxs-lookup"><span data-stu-id="32b6c-124">hello service is responsible for performing hello following Windows Update jobs on all hello cluster nodes:</span></span>
    - <span data-ttu-id="32b6c-125">Отключение автоматического обновления Windows на узле hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-125">Disabling automatic Windows Update on hello node.</span></span>
    - <span data-ttu-id="32b6c-126">Загрузка и установка обновления Windows предоставил пользователь hello toohello политики в соответствии с.</span><span class="sxs-lookup"><span data-stu-id="32b6c-126">Downloading and installing Windows Update according toohello policy hello user has provided.</span></span>
    - <span data-ttu-id="32b6c-127">Перезапуск post машины hello установки обновления Windows.</span><span class="sxs-lookup"><span data-stu-id="32b6c-127">Restarting hello machine post Windows Update installation.</span></span>
    - <span data-ttu-id="32b6c-128">Отправка результатов hello toohello обновлений Windows служба координатора.</span><span class="sxs-lookup"><span data-stu-id="32b6c-128">Uploading hello results of Windows updates toohello Coordinator Service.</span></span>
    - <span data-ttu-id="32b6c-129">сообщение сведений о работоспособности, если операцию не удалось выполнить, исчерпав все повторные попытки.</span><span class="sxs-lookup"><span data-stu-id="32b6c-129">Reporting health reports in case an operation has failed after exhausting all retries.</span></span>

> [!NOTE]
> <span data-ttu-id="32b6c-130">использует приложение hello Service Fabric Hello исправление orchestration восстановить toodisable службы диспетчера system или включить hello узел и выполняет проверку работоспособности.</span><span class="sxs-lookup"><span data-stu-id="32b6c-130">hello patch orchestration app uses hello Service Fabric repair manager system service toodisable or enable hello node and perform health checks.</span></span> <span data-ttu-id="32b6c-131">Hello задачи восстановления, созданные hello hello исправление orchestration приложение отслеживает ход выполнения обновления Windows для каждого узла.</span><span class="sxs-lookup"><span data-stu-id="32b6c-131">hello repair task created by hello patch orchestration app tracks hello Windows Update progress for each node.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32b6c-132">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="32b6c-132">Prerequisites</span></span>

### <a name="minimum-supported-service-fabric-runtime-version"></a><span data-ttu-id="32b6c-133">Минимальная поддерживаемая версия среды выполнения Service Fabric</span><span class="sxs-lookup"><span data-stu-id="32b6c-133">Minimum supported Service Fabric runtime version</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="32b6c-134">Кластеры Azure</span><span class="sxs-lookup"><span data-stu-id="32b6c-134">Azure clusters</span></span>
<span data-ttu-id="32b6c-135">orchestration приложение Hello исправления должна выполняться на Azure кластеры версий Service Fabric среды выполнения версии 5.5 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="32b6c-135">hello patch orchestration app must be run on Azure clusters that have Service Fabric runtime version v5.5 or later.</span></span>

#### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="32b6c-136">Автономные локальные кластеры</span><span class="sxs-lookup"><span data-stu-id="32b6c-136">Standalone on-premises Clusters</span></span>
<span data-ttu-id="32b6c-137">orchestration приложение Hello исправления должна выполняться на изолированные кластеры, имеющие v5.6 версии среды выполнения Service Fabric или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="32b6c-137">hello patch orchestration app must be run on Standalone clusters that have Service Fabric runtime version v5.6 or later.</span></span>

### <a name="enable-hello-repair-manager-service-if-its-not-running-already"></a><span data-ttu-id="32b6c-138">Включение службы диспетчера восстановления hello (если она не была запущена ранее)</span><span class="sxs-lookup"><span data-stu-id="32b6c-138">Enable hello repair manager service (if it's not running already)</span></span>

<span data-ttu-id="32b6c-139">orchestration приложение Hello исправление требуется hello восстановления диспетчера системы службы toobe включена в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-139">hello patch orchestration app requires hello repair manager system service toobe enabled on hello cluster.</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="32b6c-140">Кластеры Azure</span><span class="sxs-lookup"><span data-stu-id="32b6c-140">Azure clusters</span></span>

<span data-ttu-id="32b6c-141">Кластеры Azure hello серебристом устойчивость уровня имеют hello исправления service manager включен по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="32b6c-141">Azure clusters in hello silver durability tier have hello repair manager service enabled by default.</span></span> <span data-ttu-id="32b6c-142">Кластеры Azure уровня gold устойчивость hello может иметь или не иметь включен, в зависимости от того, когда были созданы эти кластеры службы диспетчера восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-142">Azure clusters in hello gold durability tier might or might not have hello repair manager service enabled, depending on when those clusters were created.</span></span> <span data-ttu-id="32b6c-143">Кластеры Azure уровня бронзового устойчивость hello, по умолчанию имеют hello исправления service manager включен.</span><span class="sxs-lookup"><span data-stu-id="32b6c-143">Azure clusters in hello bronze durability tier, by default, do not have hello repair manager service enabled.</span></span> <span data-ttu-id="32b6c-144">Если hello служба уже включена, вы увидите его выполнение в разделе служб системы hello в обозреватель Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-144">If hello service is already enabled, you can see it running in hello system services section in hello Service Fabric Explorer.</span></span>

##### <a name="azure-portal"></a><span data-ttu-id="32b6c-145">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="32b6c-145">Azure portal</span></span>
<span data-ttu-id="32b6c-146">Диспетчер восстановления на портале Azure можно включить во время настройки кластера hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-146">You can enable repair manager from Azure portal at hello time of setting up of cluster.</span></span> <span data-ttu-id="32b6c-147">Выберите `Include Repair Manager` под флажком `Add on features` во время hello конфигурации кластера.</span><span class="sxs-lookup"><span data-stu-id="32b6c-147">Select `Include Repair Manager` option under `Add on features` at hello time of Cluster configuration.</span></span>
<span data-ttu-id="32b6c-148">![Снимок экрана с подключением диспетчера восстановления на портале Azure](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span><span class="sxs-lookup"><span data-stu-id="32b6c-148">![Image of Enabling Repair Manager from Azure portal](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span></span>

##### <a name="azure-resource-manager-template"></a><span data-ttu-id="32b6c-149">Шаблон диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="32b6c-149">Azure Resource Manager template</span></span>
<span data-ttu-id="32b6c-150">Можно также использовать hello [шаблона Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable hello службы диспетчера восстановления на новых и существующих кластеров Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="32b6c-150">Alternatively you can use hello [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable hello repair manager service on new and existing Service Fabric clusters.</span></span> <span data-ttu-id="32b6c-151">Получите шаблон hello hello кластера, которые должны toodeploy.</span><span class="sxs-lookup"><span data-stu-id="32b6c-151">Get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="32b6c-152">Можно использовать шаблоны образец hello или создать настраиваемый шаблон диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="32b6c-152">You can either use hello sample templates or create a custom Resource Manager template.</span></span> 

<span data-ttu-id="32b6c-153">tooenable hello восстановления диспетчера службы с помощью [шаблона Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span><span class="sxs-lookup"><span data-stu-id="32b6c-153">tooenable hello repair manager service using [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span></span>

1. <span data-ttu-id="32b6c-154">Сначала проверьте, что hello `apiversion` задано слишком`2017-07-01-preview` для hello `Microsoft.ServiceFabric/clusters` ресурсов, как показано в следующий фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-154">First check that hello `apiversion` is set too`2017-07-01-preview` for hello `Microsoft.ServiceFabric/clusters` resource, as shown in hello following snippet.</span></span> <span data-ttu-id="32b6c-155">Если он не совпадает, то вы должны tooupdate hello `apiVersion` toohello значение `2017-07-01-preview`:</span><span class="sxs-lookup"><span data-stu-id="32b6c-155">If it is different, then you need tooupdate hello `apiVersion` toohello value `2017-07-01-preview`:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="32b6c-156">Теперь включите службы диспетчера восстановления hello, добавив следующие hello `addonFeatures` разделе после hello `fabricSettings` раздела:</span><span class="sxs-lookup"><span data-stu-id="32b6c-156">Now enable hello repair manager service by adding hello following `addonFeatures` section after hello `fabricSettings` section:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="32b6c-157">После обновления шаблон кластера с этими изменениями, их применения и позволить завершить обновление hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-157">After you have updated your cluster template with these changes, apply them and let hello upgrade finish.</span></span> <span data-ttu-id="32b6c-158">Теперь можно увидеть hello диспетчер восстановления системной службы, работающих в кластере.</span><span class="sxs-lookup"><span data-stu-id="32b6c-158">You can now see hello repair manager system service running in your cluster.</span></span> <span data-ttu-id="32b6c-159">Он вызывается `fabric:/System/RepairManagerService` в разделе служб системы hello в обозреватель Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-159">It is called `fabric:/System/RepairManagerService` in hello system services section in hello Service Fabric Explorer.</span></span> 

### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="32b6c-160">Автономные локальные кластеры</span><span class="sxs-lookup"><span data-stu-id="32b6c-160">Standalone on-premises clusters</span></span>

<span data-ttu-id="32b6c-161">Можно использовать hello [параметры конфигурации для кластера Windows автономный](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable hello службы диспетчера восстановления на новых и существующих кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="32b6c-161">You can use hello [Configuration settings for standalone Windows cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable hello repair manager service on new and existing Service Fabric cluster.</span></span>

<span data-ttu-id="32b6c-162">Служба диспетчера восстановления hello tooenable:</span><span class="sxs-lookup"><span data-stu-id="32b6c-162">tooenable hello repair manager service:</span></span>

1. <span data-ttu-id="32b6c-163">Сначала проверьте, что hello `apiversion` в [конфигурации кластера Общие](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) задано слишком`04-2017` или более поздней версии:</span><span class="sxs-lookup"><span data-stu-id="32b6c-163">First check that hello `apiversion` in [General cluster configurations](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) is set too`04-2017` or higher:</span></span>

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. <span data-ttu-id="32b6c-164">Теперь включите службы диспетчера восстановления, добавив следующие hello `addonFeaturres` разделе после hello `fabricSettings` статьи, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="32b6c-164">Now enable repair manager service by adding hello following `addonFeaturres` section after hello `fabricSettings` section as shown below:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="32b6c-165">Обновить манифест кластера с этими изменениями, hello обновления манифеста кластера с помощью [Создание нового кластера](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) или [конфигурации кластера обновления hello](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span><span class="sxs-lookup"><span data-stu-id="32b6c-165">Update your cluster manifest with these changes, using hello updated cluster manifest [create a new cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) or [upgrade hello cluster configuration](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span></span> <span data-ttu-id="32b6c-166">После запуска кластера hello с манифестом обновленные кластера теперь можно увидеть hello диспетчер восстановления системной службы, работающих в кластере, который называется `fabric:/System/RepairManagerService`в разделе системных служб раздела Service Fabric explorer hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-166">Once hello cluster is running with updated cluster manifest, you can now see hello repair manager system service running in your cluster, which is called `fabric:/System/RepairManagerService`, under system services section in hello Service Fabric explorer.</span></span>

### <a name="disable-automatic-windows-update-on-all-nodes"></a><span data-ttu-id="32b6c-167">Отключение автоматического обновления Windows на всех узлах</span><span class="sxs-lookup"><span data-stu-id="32b6c-167">Disable automatic Windows Update on all nodes</span></span>

<span data-ttu-id="32b6c-168">Автоматическое обновление Windows может привести tooavailability потери, поскольку нескольким узлам кластера можно перезагрузить hello же время.</span><span class="sxs-lookup"><span data-stu-id="32b6c-168">Automatic Windows updates might lead tooavailability loss because multiple cluster nodes can restart at hello same time.</span></span> <span data-ttu-id="32b6c-169">приложение orchestration исправление Hello, по умолчанию, пытается toodisable hello автоматического обновления Windows на каждом узле кластера.</span><span class="sxs-lookup"><span data-stu-id="32b6c-169">hello patch orchestration app, by default, tries toodisable hello automatic Windows Update on each cluster node.</span></span> <span data-ttu-id="32b6c-170">Тем не менее если параметры hello управляются администратором или групповой политики, рекомендуется hello параметр политики слишком «уведомление перед загрузкой» явно центра обновления Windows.</span><span class="sxs-lookup"><span data-stu-id="32b6c-170">However, if hello settings are managed by an administrator or group policy, we recommend setting hello Windows Update policy too“Notify before Download” explicitly.</span></span>

### <a name="optional-enable-azure-diagnostics"></a><span data-ttu-id="32b6c-171">Включение системы диагностики Azure (необязательно)</span><span class="sxs-lookup"><span data-stu-id="32b6c-171">Optional: Enable Azure Diagnostics</span></span>

<span data-ttu-id="32b6c-172">Для кластеров со средой выполнения Service Fabric версии `5.6.220.9494` и выше журналы приложения для оркестрации исправлений будут собираться как часть журналов Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="32b6c-172">Clusters running Service Fabric runtime version `5.6.220.9494` and above collect patch orchestration app logs as part of Service Fabric logs.</span></span>
<span data-ttu-id="32b6c-173">Этот шаг можно пропустить, если кластер работает под управлением среды выполнения Service Fabric версии `5.6.220.9494` и выше.</span><span class="sxs-lookup"><span data-stu-id="32b6c-173">You can skip this step if your cluster is running on Service Fabric runtime version `5.6.220.9494` and above.</span></span>

<span data-ttu-id="32b6c-174">Для кластеров под управлением версии среды выполнения Service Fabric меньше, чем `5.6.220.9494`, журналы для orchestration приложение hello исправление собираются локально на каждом узле кластера hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-174">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs for hello patch orchestration app are collected locally on each of hello cluster nodes.</span></span>
<span data-ttu-id="32b6c-175">Мы рекомендуем настроить журналы диагностики Azure tooupload из центрального расположения tooa все узлы.</span><span class="sxs-lookup"><span data-stu-id="32b6c-175">We recommend that you configure Azure Diagnostics tooupload logs from all nodes tooa central location.</span></span>

<span data-ttu-id="32b6c-176">Сведения о включении системы диагностики Azure см. в статье [Сбор журналов с помощью системы диагностики Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span><span class="sxs-lookup"><span data-stu-id="32b6c-176">For information on enabling Azure Diagnostics, see [Collect logs by using Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span></span>

<span data-ttu-id="32b6c-177">Журналы для hello исправление orchestration приложения создаются на следующих основных поставщика идентификаторов hello:</span><span class="sxs-lookup"><span data-stu-id="32b6c-177">Logs for hello patch orchestration app are generated on hello following fixed provider IDs:</span></span>

- <span data-ttu-id="32b6c-178">e39b723c-590c-4090-abb0-11e3e6616346</span><span class="sxs-lookup"><span data-stu-id="32b6c-178">e39b723c-590c-4090-abb0-11e3e6616346</span></span>
- <span data-ttu-id="32b6c-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span><span class="sxs-lookup"><span data-stu-id="32b6c-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span></span>
- <span data-ttu-id="32b6c-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span><span class="sxs-lookup"><span data-stu-id="32b6c-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span></span>
- <span data-ttu-id="32b6c-181">05dc046c-60e9-4ef7-965e-91660adffa68</span><span class="sxs-lookup"><span data-stu-id="32b6c-181">05dc046c-60e9-4ef7-965e-91660adffa68</span></span>

<span data-ttu-id="32b6c-182">В диспетчер ресурсов шаблона goto `EtwEventSourceProviderConfiguration` раздела `WadCfg` и добавить hello следующие записи:</span><span class="sxs-lookup"><span data-stu-id="32b6c-182">In Resource Manager template goto `EtwEventSourceProviderConfiguration` section under `WadCfg` and add hello following entries:</span></span>

```json
  {
    "provider": "e39b723c-590c-4090-abb0-11e3e6616346",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
      "eventDestination": "PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "fc0028ff-bfdc-499f-80dc-ed922c52c5e9",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "24afa313-0d3b-4c7c-b485-1047fd964b60",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "05dc046c-60e9-4ef7-965e-91660adffa68",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  }
```

> [!NOTE]
> <span data-ttu-id="32b6c-183">Если кластер Service Fabric имеет несколько типов узлов, то необходимо добавить все hello hello предыдущего раздела `WadCfg` разделы.</span><span class="sxs-lookup"><span data-stu-id="32b6c-183">If your Service Fabric cluster has multiple node types, then hello previous section must be added for all hello `WadCfg` sections.</span></span>

## <a name="download-hello-app-package"></a><span data-ttu-id="32b6c-184">Загрузите пакет приложения hello</span><span class="sxs-lookup"><span data-stu-id="32b6c-184">Download hello app package</span></span>

<span data-ttu-id="32b6c-185">Загрузить приложение hello hello [ссылка для загрузки](https://go.microsoft.com/fwlink/P/?linkid=849590).</span><span class="sxs-lookup"><span data-stu-id="32b6c-185">Download hello application from hello [download link](https://go.microsoft.com/fwlink/P/?linkid=849590).</span></span>

## <a name="configure-hello-app"></a><span data-ttu-id="32b6c-186">Настройте приложение hello</span><span class="sxs-lookup"><span data-stu-id="32b6c-186">Configure hello app</span></span>

<span data-ttu-id="32b6c-187">Здравствуйте поведение orchestration приложение hello исправление может быть настроенный toomeet вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="32b6c-187">hello behavior of hello patch orchestration app can be configured toomeet your needs.</span></span> <span data-ttu-id="32b6c-188">Переопределите значения по умолчанию hello, передавая параметр приложения hello во время создания приложения или обновления.</span><span class="sxs-lookup"><span data-stu-id="32b6c-188">Override hello default values by passing in hello application parameter during application creation or update.</span></span> <span data-ttu-id="32b6c-189">Параметры приложения могут быть предоставлены, указав `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` или `New-ServiceFabricApplication` командлетов.</span><span class="sxs-lookup"><span data-stu-id="32b6c-189">Application parameters can be provided by specifying `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` or `New-ServiceFabricApplication` cmdlets.</span></span>

|<span data-ttu-id="32b6c-190">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="32b6c-190">**Parameter**</span></span>        |<span data-ttu-id="32b6c-191">**Тип**</span><span class="sxs-lookup"><span data-stu-id="32b6c-191">**Type**</span></span>                          | <span data-ttu-id="32b6c-192">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="32b6c-192">**Details**</span></span>|
|:-|-|-|
|<span data-ttu-id="32b6c-193">MaxResultsToCache</span><span class="sxs-lookup"><span data-stu-id="32b6c-193">MaxResultsToCache</span></span>    |<span data-ttu-id="32b6c-194">длинное целое</span><span class="sxs-lookup"><span data-stu-id="32b6c-194">Long</span></span>                              | <span data-ttu-id="32b6c-195">Максимальное количество результатов обновления Windows, которые необходимо кэшировать.</span><span class="sxs-lookup"><span data-stu-id="32b6c-195">Maximum number of Windows Update results, which should be cached.</span></span> <br><span data-ttu-id="32b6c-196">Значение по умолчанию — 3000 при условии, что:</span><span class="sxs-lookup"><span data-stu-id="32b6c-196">Default value is 3000 assuming the:</span></span> <br> <span data-ttu-id="32b6c-197">- количество узлов —20;</span><span class="sxs-lookup"><span data-stu-id="32b6c-197">- Number of nodes is 20.</span></span> <br> <span data-ttu-id="32b6c-198">- количество обновлений на узле в месяц — 5;</span><span class="sxs-lookup"><span data-stu-id="32b6c-198">- Number of updates happening on a node per month is five.</span></span> <br> <span data-ttu-id="32b6c-199">- количество результатов на операцию может быть 10;</span><span class="sxs-lookup"><span data-stu-id="32b6c-199">- Number of results per operation can be 10.</span></span> <br> <span data-ttu-id="32b6c-200">-Должны ли сохраняться результатов для hello за последние три месяца.</span><span class="sxs-lookup"><span data-stu-id="32b6c-200">- Results for hello past three months should be stored.</span></span> |
|<span data-ttu-id="32b6c-201">TaskApprovalPolicy</span><span class="sxs-lookup"><span data-stu-id="32b6c-201">TaskApprovalPolicy</span></span>   |<span data-ttu-id="32b6c-202">Перечисление.</span><span class="sxs-lookup"><span data-stu-id="32b6c-202">Enum</span></span> <br> <span data-ttu-id="32b6c-203">{ NodeWise, UpgradeDomainWise }</span><span class="sxs-lookup"><span data-stu-id="32b6c-203">{ NodeWise, UpgradeDomainWise }</span></span>                          |<span data-ttu-id="32b6c-204">TaskApprovalPolicy указывает политику hello, toobe, используемые tooinstall Windows hello службы координатора обновлений на узлах кластера Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-204">TaskApprovalPolicy indicates hello policy that is toobe used by hello Coordinator Service tooinstall Windows updates across hello Service Fabric cluster nodes.</span></span><br>                         <span data-ttu-id="32b6c-205">Допустимые значения:</span><span class="sxs-lookup"><span data-stu-id="32b6c-205">Allowed values are:</span></span> <br>                                                           <span data-ttu-id="32b6c-206"><b>NodeWise</b>.</span><span class="sxs-lookup"><span data-stu-id="32b6c-206"><b>NodeWise</b>.</span></span> <span data-ttu-id="32b6c-207">Обновление Windows устанавливается на один узел за раз.</span><span class="sxs-lookup"><span data-stu-id="32b6c-207">Windows Update is installed one node at a time.</span></span> <br>                                                           <span data-ttu-id="32b6c-208"><b>UpgradeDomainWise</b>.</span><span class="sxs-lookup"><span data-stu-id="32b6c-208"><b>UpgradeDomainWise</b>.</span></span> <span data-ttu-id="32b6c-209">Обновление Windows устанавливается на один домен обновления за раз</span><span class="sxs-lookup"><span data-stu-id="32b6c-209">Windows Update is installed one upgrade domain at a time.</span></span> <span data-ttu-id="32b6c-210">(На максимальный hello, все узлы hello, принадлежащий домену обновления tooan можно перейти для центра обновления Windows).</span><span class="sxs-lookup"><span data-stu-id="32b6c-210">(At hello maximum, all hello nodes belonging tooan upgrade domain can go for Windows Update.)</span></span>
|<span data-ttu-id="32b6c-211">LogsDiskQuotaInMB</span><span class="sxs-lookup"><span data-stu-id="32b6c-211">LogsDiskQuotaInMB</span></span>   |<span data-ttu-id="32b6c-212">длинное целое</span><span class="sxs-lookup"><span data-stu-id="32b6c-212">Long</span></span>  <br> <span data-ttu-id="32b6c-213">(значение по умолчанию: 1024)</span><span class="sxs-lookup"><span data-stu-id="32b6c-213">(Default: 1024)</span></span>               |<span data-ttu-id="32b6c-214">Максимальный размер журналов приложения для управления исправлениями, которые могут быть сохранены локально на узле (в мегабайтах).</span><span class="sxs-lookup"><span data-stu-id="32b6c-214">Maximum size of patch orchestration app logs in MB, which can be persisted locally on nodes.</span></span>
| <span data-ttu-id="32b6c-215">WUQuery</span><span class="sxs-lookup"><span data-stu-id="32b6c-215">WUQuery</span></span>               | <span data-ttu-id="32b6c-216">string</span><span class="sxs-lookup"><span data-stu-id="32b6c-216">string</span></span><br><span data-ttu-id="32b6c-217">(значение по умолчанию: IsInstalled=0)</span><span class="sxs-lookup"><span data-stu-id="32b6c-217">(Default: "IsInstalled=0")</span></span>                | <span data-ttu-id="32b6c-218">Запрос tooget обновления Windows.</span><span class="sxs-lookup"><span data-stu-id="32b6c-218">Query tooget Windows updates.</span></span> <span data-ttu-id="32b6c-219">Дополнительные сведения см. в разделе [WuQuery](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="32b6c-219">For more information, see [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span></span>
| <span data-ttu-id="32b6c-220">InstallWindowsOSOnlyUpdates</span><span class="sxs-lookup"><span data-stu-id="32b6c-220">InstallWindowsOSOnlyUpdates</span></span> | <span data-ttu-id="32b6c-221">Bool</span><span class="sxs-lookup"><span data-stu-id="32b6c-221">Bool</span></span> <br> <span data-ttu-id="32b6c-222">(значение по умолчанию: True)</span><span class="sxs-lookup"><span data-stu-id="32b6c-222">(default: True)</span></span>                 | <span data-ttu-id="32b6c-223">Этот флаг позволяет toobe обновления системы установлена операционная система Windows.</span><span class="sxs-lookup"><span data-stu-id="32b6c-223">This flag allows Windows operating system updates toobe installed.</span></span>            |
| <span data-ttu-id="32b6c-224">WUOperationTimeOutInMinutes</span><span class="sxs-lookup"><span data-stu-id="32b6c-224">WUOperationTimeOutInMinutes</span></span> | <span data-ttu-id="32b6c-225">int</span><span class="sxs-lookup"><span data-stu-id="32b6c-225">Int</span></span> <br><span data-ttu-id="32b6c-226">(значение по умолчанию: 90)</span><span class="sxs-lookup"><span data-stu-id="32b6c-226">(Default: 90)</span></span>                   | <span data-ttu-id="32b6c-227">Указывает время ожидания hello для любой операции обновления Windows (поиска или загружать или устанавливать).</span><span class="sxs-lookup"><span data-stu-id="32b6c-227">Specifies hello timeout for any Windows Update operation (search or download or install).</span></span> <span data-ttu-id="32b6c-228">Если операция hello не была завершена в течение Здравствуйте заданное время ожидания, он будет прерван.</span><span class="sxs-lookup"><span data-stu-id="32b6c-228">If hello operation is not completed within hello specified timeout, it is aborted.</span></span>       |
| <span data-ttu-id="32b6c-229">WURescheduleCount</span><span class="sxs-lookup"><span data-stu-id="32b6c-229">WURescheduleCount</span></span>     | <span data-ttu-id="32b6c-230">int</span><span class="sxs-lookup"><span data-stu-id="32b6c-230">Int</span></span> <br> <span data-ttu-id="32b6c-231">(значение по умолчанию: 5)</span><span class="sxs-lookup"><span data-stu-id="32b6c-231">(Default: 5)</span></span>                  | <span data-ttu-id="32b6c-232">Hello максимальное число hello службы, а затем — hello центра обновления Windows в случае постоянного сбоя операции.</span><span class="sxs-lookup"><span data-stu-id="32b6c-232">hello maximum number of times hello service reschedules hello Windows update in case an operation fails persistently.</span></span>          |
| <span data-ttu-id="32b6c-233">WURescheduleTimeInMinutes</span><span class="sxs-lookup"><span data-stu-id="32b6c-233">WURescheduleTimeInMinutes</span></span> | <span data-ttu-id="32b6c-234">int</span><span class="sxs-lookup"><span data-stu-id="32b6c-234">Int</span></span> <br><span data-ttu-id="32b6c-235">(значение по умолчанию: 30)</span><span class="sxs-lookup"><span data-stu-id="32b6c-235">(Default: 30)</span></span> | <span data-ttu-id="32b6c-236">Интервал приветствия, на какие hello службы, а затем — обновления Windows hello в случае, если ошибка продолжает появляться.</span><span class="sxs-lookup"><span data-stu-id="32b6c-236">hello interval at which hello service reschedules hello Windows update in case failure persists.</span></span> |
| <span data-ttu-id="32b6c-237">WUFrequency</span><span class="sxs-lookup"><span data-stu-id="32b6c-237">WUFrequency</span></span>           | <span data-ttu-id="32b6c-238">Строка с разделителями-запятыми (по умолчанию: Weekly, Wednesday, 7:00:00)</span><span class="sxs-lookup"><span data-stu-id="32b6c-238">Comma-separated string (Default: "Weekly, Wednesday, 7:00:00")</span></span>     | <span data-ttu-id="32b6c-239">частота Hello для установки обновления Windows.</span><span class="sxs-lookup"><span data-stu-id="32b6c-239">hello frequency for installing Windows Update.</span></span> <span data-ttu-id="32b6c-240">доступны следующие Hello формат и возможные значения:</span><span class="sxs-lookup"><span data-stu-id="32b6c-240">hello format and possible values are:</span></span> <br><span data-ttu-id="32b6c-241">- Ежемесячно, ДД,ЧЧ:ММ:СС (например: Monthly, 5,12:22:32);</span><span class="sxs-lookup"><span data-stu-id="32b6c-241">-   Monthly, DD,HH:MM:SS, for example, Monthly, 5,12:22:32.</span></span> <br> <span data-ttu-id="32b6c-242">- Еженедельно, ДЕНЬ, ЧЧ:ММ:СС (например: Weekly, Tuesday, 12:22:32);</span><span class="sxs-lookup"><span data-stu-id="32b6c-242">-   Weekly, DAY,HH:MM:SS, for example, Weekly, Tuesday, 12:22:32.</span></span>  <br> <span data-ttu-id="32b6c-243">- Ежедневно, ЧЧ:ММ:СС (например: Daily, 12:22:32);</span><span class="sxs-lookup"><span data-stu-id="32b6c-243">-   Daily, HH:MM:SS, for example, Daily, 12:22:32.</span></span>  <br> <span data-ttu-id="32b6c-244">- Никогда — указывает, что обновление Windows не должно выполняться.</span><span class="sxs-lookup"><span data-stu-id="32b6c-244">-  None indicates that Windows Update shouldn't be done.</span></span>  <br><br> <span data-ttu-id="32b6c-245">Обратите внимание, что все hello значения времени в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="32b6c-245">Note that all hello times are in UTC.</span></span>|
| <span data-ttu-id="32b6c-246">AcceptWindowsUpdateEula</span><span class="sxs-lookup"><span data-stu-id="32b6c-246">AcceptWindowsUpdateEula</span></span> | <span data-ttu-id="32b6c-247">Bool</span><span class="sxs-lookup"><span data-stu-id="32b6c-247">Bool</span></span> <br><span data-ttu-id="32b6c-248">(значение по умолчанию: True)</span><span class="sxs-lookup"><span data-stu-id="32b6c-248">(Default: true)</span></span> | <span data-ttu-id="32b6c-249">Установив этот флажок, приложение hello принимает hello конечным пользователем лицензионного соглашения для обновления Windows, от имени владельца hello машины hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-249">By setting this flag, hello application accepts hello End-User License Agreement for Windows Update on behalf of hello owner of hello machine.</span></span>              |

> [!TIP]
> <span data-ttu-id="32b6c-250">Если toohappen центра обновления Windows требуется немедленно, установите `WUFrequency` toohello относительного времени развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="32b6c-250">If you want Windows Update toohappen immediately, set `WUFrequency` relative toohello application deployment time.</span></span> <span data-ttu-id="32b6c-251">Например, предположим, имеется пять узел кластера и план toodeploy hello приложение теста в около 5:00 UTC.</span><span class="sxs-lookup"><span data-stu-id="32b6c-251">For example, suppose that you have a five-node test cluster and plan toodeploy hello app at around 5:00 PM UTC.</span></span> <span data-ttu-id="32b6c-252">Если предполагается, что обновление приложения hello или развертывания занимает 30 минут на hello максимальное, задайте hello WUFrequency как «Ежедневно, 17:30:00.»</span><span class="sxs-lookup"><span data-stu-id="32b6c-252">If you assume that hello application upgrade or deployment takes 30 minutes at hello maximum, set hello WUFrequency as "Daily, 17:30:00."</span></span>

## <a name="deploy-hello-app"></a><span data-ttu-id="32b6c-253">Развернуть приложение hello</span><span class="sxs-lookup"><span data-stu-id="32b6c-253">Deploy hello app</span></span>

1. <span data-ttu-id="32b6c-254">Завершите все hello кластера tooprepare hello обязательные шаги.</span><span class="sxs-lookup"><span data-stu-id="32b6c-254">Finish all hello prerequisite steps tooprepare hello cluster.</span></span>
2. <span data-ttu-id="32b6c-255">Разверните приложение hello исправление orchestration, как и любое другое приложение Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="32b6c-255">Deploy hello patch orchestration app like any other Service Fabric app.</span></span> <span data-ttu-id="32b6c-256">С помощью PowerShell, можно развернуть приложение hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-256">You can deploy hello app by using PowerShell.</span></span> <span data-ttu-id="32b6c-257">Следуйте указаниям hello [развертывание и удаление приложений с помощью PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="32b6c-257">Follow hello steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>
3. <span data-ttu-id="32b6c-258">приложение hello tooconfigure во время развертывания, передайте hello hello `ApplicationParamater` toohello `New-ServiceFabricApplication` командлета.</span><span class="sxs-lookup"><span data-stu-id="32b6c-258">tooconfigure hello application at hello time of deployment, pass hello `ApplicationParamater` toohello `New-ServiceFabricApplication` cmdlet.</span></span> <span data-ttu-id="32b6c-259">Для вашего удобства мы предоставили hello сценария Deploy.ps1 вместе с приложением hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-259">For your convenience, we’ve provided hello script Deploy.ps1 along with hello application.</span></span> <span data-ttu-id="32b6c-260">скрипт hello toouse:</span><span class="sxs-lookup"><span data-stu-id="32b6c-260">toouse hello script:</span></span>

    - <span data-ttu-id="32b6c-261">Подключиться с помощью кластера Service Fabric tooa `Connect-ServiceFabricCluster`.</span><span class="sxs-lookup"><span data-stu-id="32b6c-261">Connect tooa Service Fabric cluster by using `Connect-ServiceFabricCluster`.</span></span>
    - <span data-ttu-id="32b6c-262">Выполнить сценарий PowerShell hello Deploy.ps1 с hello соответствующие `ApplicationParameter` значение.</span><span class="sxs-lookup"><span data-stu-id="32b6c-262">Execute hello PowerShell script Deploy.ps1 with hello appropriate `ApplicationParameter` value.</span></span>

> [!NOTE]
> <span data-ttu-id="32b6c-263">Сохранить скрипт hello и папка приложения hello PatchOrchestrationApplication в hello один каталог.</span><span class="sxs-lookup"><span data-stu-id="32b6c-263">Keep hello script and hello application folder PatchOrchestrationApplication in hello same directory.</span></span>

## <a name="upgrade-hello-app"></a><span data-ttu-id="32b6c-264">Обновление приложения hello</span><span class="sxs-lookup"><span data-stu-id="32b6c-264">Upgrade hello app</span></span>

<span data-ttu-id="32b6c-265">tooupgrade существующего приложения orchestration исправлений с помощью PowerShell, выполните действия hello в [обновление приложения Service Fabric, с помощью PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span><span class="sxs-lookup"><span data-stu-id="32b6c-265">tooupgrade an existing patch orchestration app by using PowerShell, follow hello steps in [Service Fabric application upgrade using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span></span>

## <a name="remove-hello-app"></a><span data-ttu-id="32b6c-266">Удалите приложение hello</span><span class="sxs-lookup"><span data-stu-id="32b6c-266">Remove hello app</span></span>

<span data-ttu-id="32b6c-267">приложение hello tooremove, повторите шаги hello в [развертывание и удаление приложений с помощью PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="32b6c-267">tooremove hello application, follow hello steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>

<span data-ttu-id="32b6c-268">Для вашего удобства мы предоставили hello сценария Undeploy.ps1 вместе с приложением hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-268">For your convenience, we've provided hello script Undeploy.ps1 along with hello application.</span></span> <span data-ttu-id="32b6c-269">скрипт hello toouse:</span><span class="sxs-lookup"><span data-stu-id="32b6c-269">toouse hello script:</span></span>

  - <span data-ttu-id="32b6c-270">Подключиться с помощью кластера Service Fabric tooa ```Connect-ServiceFabricCluster```.</span><span class="sxs-lookup"><span data-stu-id="32b6c-270">Connect tooa Service Fabric cluster by using ```Connect-ServiceFabricCluster```.</span></span>

  - <span data-ttu-id="32b6c-271">Выполните сценарий PowerShell hello Undeploy.ps1.</span><span class="sxs-lookup"><span data-stu-id="32b6c-271">Execute hello PowerShell script Undeploy.ps1.</span></span>

> [!NOTE]
> <span data-ttu-id="32b6c-272">Сохранить скрипт hello и папка приложения hello PatchOrchestrationApplication в hello один каталог.</span><span class="sxs-lookup"><span data-stu-id="32b6c-272">Keep hello script and hello application folder PatchOrchestrationApplication in hello same directory.</span></span>

## <a name="view-hello-windows-update-results"></a><span data-ttu-id="32b6c-273">Просмотр результатов обновления Windows hello</span><span class="sxs-lookup"><span data-stu-id="32b6c-273">View hello Windows Update results</span></span>

<span data-ttu-id="32b6c-274">Hello исправление orchestration приложение предоставляет API-интерфейс REST toodisplay hello исторических результаты toohello пользователя.</span><span class="sxs-lookup"><span data-stu-id="32b6c-274">hello patch orchestration app exposes REST APIs toodisplay hello historical results toohello user.</span></span> <span data-ttu-id="32b6c-275">Пример результата hello JSON:</span><span class="sxs-lookup"><span data-stu-id="32b6c-275">An example of hello result JSON:</span></span>
```json
[
  {
    "NodeName": "_stg1vm_1",
    "WindowsUpdateOperationResults": [
      {
        "OperationResult": 0,
        "NodeName": "_stg1vm_1",
        "OperationTime": "2017-05-21T11:46:52.1953713Z",
        "UpdateDetails": [
          {
            "UpdateId": "7392acaf-6a85-427c-8a8d-058c25beb0d6",
            "Title": "Cumulative Security Update for Internet Explorer 11 for Windows Server 2012 R2 (KB3185319)",
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of hello issues that are included in this update, see hello associated Microsoft Knowledge Base article. After you install this update, you may have toorestart your system.",
            "ResultCode": 0
          }
        ],
        "OperationType": 1,
        "WindowsUpdateQuery": "IsInstalled=0",
        "WindowsUpdateFrequency": "Daily,10:00:00",
        "RebootRequired": false
      }
    ]
  },
  ...
]
```
<span data-ttu-id="32b6c-276">Если обновление не запланировано еще, результат hello JSON является пустым.</span><span class="sxs-lookup"><span data-stu-id="32b6c-276">If no update is scheduled yet, hello result JSON is empty.</span></span>

<span data-ttu-id="32b6c-277">Войдите в систему tooquery toohello кластера Windows Update результаты.</span><span class="sxs-lookup"><span data-stu-id="32b6c-277">Log in toohello cluster tooquery Windows Update results.</span></span> <span data-ttu-id="32b6c-278">Узнать адрес hello реплики для первичной hello hello службы координатора затем попаданий hello URL-адрес из браузера hello: http://&lt;РЕПЛИКИ IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1 / GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="32b6c-278">Then find out hello replica address for hello primary of hello Coordinator Service, and hit hello URL from hello browser: http://&lt;REPLICA-IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="32b6c-279">Hello конечную точку REST для службы координатора hello имеет динамический порт.</span><span class="sxs-lookup"><span data-stu-id="32b6c-279">hello REST endpoint for hello Coordinator Service has a dynamic port.</span></span> <span data-ttu-id="32b6c-280">toocheck hello точный URL-адрес, относятся toohello Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="32b6c-280">toocheck hello exact URL, refer toohello Service Fabric Explorer.</span></span> <span data-ttu-id="32b6c-281">Например, результаты hello доступны на `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span><span class="sxs-lookup"><span data-stu-id="32b6c-281">For example, hello results are available at `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span></span>

![Представление конечной точки REST](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


<span data-ttu-id="32b6c-283">Hello обратный прокси-сервер будет включен в кластер hello, можно получить доступ к hello URL-адрес за пределами кластера hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-283">If hello reverse proxy is enabled on hello cluster, you can access hello URL from outside of hello cluster as well.</span></span>
<span data-ttu-id="32b6c-284">Здравствуйте, конечная точка, которая должна toobe попадание — http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="32b6c-284">hello endpoint that needs toobe hit is http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="32b6c-285">tooenable hello обратного прокси-сервера на кластере hello, следуйте указаниям hello [обратный прокси-сервер в Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span><span class="sxs-lookup"><span data-stu-id="32b6c-285">tooenable hello reverse proxy on hello cluster, follow hello steps in [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span></span> 

> 
> [!WARNING]
> <span data-ttu-id="32b6c-286">После настройки hello обратного прокси-сервера, все micro службы в кластере hello, которые предоставляют конечную точку HTTP, адресуемых за пределами кластера hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-286">After hello reverse proxy is configured, all micro services in hello cluster that expose an HTTP endpoint are addressable from outside hello cluster.</span></span>

## <a name="diagnosticshealth-events"></a><span data-ttu-id="32b6c-287">События диагностики и работоспособности</span><span class="sxs-lookup"><span data-stu-id="32b6c-287">Diagnostics/health events</span></span>

### <a name="collect-patch-orchestration-app-logs"></a><span data-ttu-id="32b6c-288">Сбора журналов приложения для управления исправлениями</span><span class="sxs-lookup"><span data-stu-id="32b6c-288">Collect patch orchestration app logs</span></span>

<span data-ttu-id="32b6c-289">В среде выполнения версии `5.6.220.9494` и выше журналы приложения для управления исправлениями собираются как часть журналов Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="32b6c-289">Patch orchestration app logs are collected as part of Service Fabric logs from runtime version `5.6.220.9494` and above.</span></span>
<span data-ttu-id="32b6c-290">Для кластеров под управлением версии среды выполнения Service Fabric меньше, чем `5.6.220.9494`, можно собирать журналы с помощью одного из следующих методов hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-290">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs can be collected by using one of hello following methods.</span></span>

#### <a name="locally-on-each-node"></a><span data-ttu-id="32b6c-291">Локально на каждом узле</span><span class="sxs-lookup"><span data-stu-id="32b6c-291">Locally on each node</span></span>

<span data-ttu-id="32b6c-292">Если версия среды выполнения Service Fabric ниже, чем `5.6.220.9494`, журналы собираются локально на каждом узле кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="32b6c-292">Logs are collected locally on each Service Fabric cluster node if Service Fabric runtime version is less than `5.6.220.9494`.</span></span> <span data-ttu-id="32b6c-293">Hello журналы hello tooaccess расположение — \[Service Fabric\_установки\_диска\]:\\PatchOrchestrationApplication\\журналы.</span><span class="sxs-lookup"><span data-stu-id="32b6c-293">hello location tooaccess hello logs is \[Service Fabric\_Installation\_Drive\]:\\PatchOrchestrationApplication\\logs.</span></span>

<span data-ttu-id="32b6c-294">Например, Service Fabric установлен на диске D, hello путь — D:\\PatchOrchestrationApplication\\журналы.</span><span class="sxs-lookup"><span data-stu-id="32b6c-294">For example, if Service Fabric is installed on drive D, hello path is D:\\PatchOrchestrationApplication\\logs.</span></span>

#### <a name="central-location"></a><span data-ttu-id="32b6c-295">Центральное расположение</span><span class="sxs-lookup"><span data-stu-id="32b6c-295">Central location</span></span>

<span data-ttu-id="32b6c-296">Если диагностики Azure настроен как часть обязательные шаги, журналы для orchestration приложение hello исправления доступны в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="32b6c-296">If Azure Diagnostics is configured as part of prerequisite steps, logs for hello patch orchestration app are available in Azure Storage.</span></span>

### <a name="health-reports"></a><span data-ttu-id="32b6c-297">Отчеты о работоспособности</span><span class="sxs-lookup"><span data-stu-id="32b6c-297">Health reports</span></span>

<span data-ttu-id="32b6c-298">orchestration приложение Hello исправления также публикует отчеты о работоспособности от hello Координатор службы или hello служба агента узла в hello в следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="32b6c-298">hello patch orchestration app also publishes health reports against hello Coordinator Service or hello Node Agent Service in hello following cases:</span></span>

#### <a name="a-windows-update-operation-failed"></a><span data-ttu-id="32b6c-299">Сбой операции обновления Windows</span><span class="sxs-lookup"><span data-stu-id="32b6c-299">A Windows Update operation failed</span></span>

<span data-ttu-id="32b6c-300">Если операция обновления Windows не на узле, для hello службы узла агента создается отчет о работоспособности.</span><span class="sxs-lookup"><span data-stu-id="32b6c-300">If a Windows Update operation fails on a node, a health report is generated against hello Node Agent Service.</span></span> <span data-ttu-id="32b6c-301">Сведения об отчете о работоспособности hello содержат имя проблемный узел hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-301">Details of hello health report contain hello problematic node name.</span></span>

<span data-ttu-id="32b6c-302">После исправления успешно завершено на проблемный узел hello, hello отчета автоматически очищается.</span><span class="sxs-lookup"><span data-stu-id="32b6c-302">After patching is successfully completed on hello problematic node, hello report is automatically cleared.</span></span>

#### <a name="hello-node-agent-ntservice-is-down"></a><span data-ttu-id="32b6c-303">Hello NTService узел агента не работает</span><span class="sxs-lookup"><span data-stu-id="32b6c-303">hello Node Agent NTService is down</span></span>

<span data-ttu-id="32b6c-304">Если hello NTService узел агента не работает на узле, для hello служба агента узла создается отчет о работоспособности уровня предупреждения.</span><span class="sxs-lookup"><span data-stu-id="32b6c-304">If hello Node Agent NTService is down on a node, a warning-level health report is generated against hello Node Agent Service.</span></span>

#### <a name="hello-repair-manager-service-is-not-enabled"></a><span data-ttu-id="32b6c-305">Служба диспетчера восстановления Hello не включена</span><span class="sxs-lookup"><span data-stu-id="32b6c-305">hello repair manager service is not enabled</span></span>

<span data-ttu-id="32b6c-306">Если служба диспетчера восстановления hello не найден в кластере hello, для hello службы координатора создается отчет о работоспособности уровня предупреждения.</span><span class="sxs-lookup"><span data-stu-id="32b6c-306">If hello repair manager service is not found on hello cluster, a warning-level health report is generated for hello Coordinator Service.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="32b6c-307">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="32b6c-307">Frequently asked questions</span></span>

<span data-ttu-id="32b6c-308">В.</span><span class="sxs-lookup"><span data-stu-id="32b6c-308">Q.</span></span> <span data-ttu-id="32b6c-309">**Почему я вижу кластер в состоянии ошибки при запуске приложение orchestration hello исправление?**</span><span class="sxs-lookup"><span data-stu-id="32b6c-309">**Why do I see my cluster in an error state when hello patch orchestration app is running?**</span></span>

<span data-ttu-id="32b6c-310">О.</span><span class="sxs-lookup"><span data-stu-id="32b6c-310">A.</span></span> <span data-ttu-id="32b6c-311">Во время процесса установки hello orchestration приложение hello исправление отключает или перезагрузки узлов, которые временно может привести к hello работоспособности кластера hello выхода из строя.</span><span class="sxs-lookup"><span data-stu-id="32b6c-311">During hello installation process, hello patch orchestration app disables or restarts nodes, which can temporarily result in hello health of hello cluster going down.</span></span>

<span data-ttu-id="32b6c-312">На основе hello политики для приложения hello, либо один узел можно перейти во время операции исправления *или* всего домена обновления могут выключаться одновременно.</span><span class="sxs-lookup"><span data-stu-id="32b6c-312">Based on hello policy for hello application, either one node can go down during a patching operation *or* an entire upgrade domain can go down simultaneously.</span></span>

<span data-ttu-id="32b6c-313">Hello конце hello установки обновления Windows приветствия повторно включать узлы после перезапуска.</span><span class="sxs-lookup"><span data-stu-id="32b6c-313">By hello end of hello Windows Update installation, hello nodes are reenabled post restart.</span></span>

<span data-ttu-id="32b6c-314">В следующем примере hello кластер hello перехода, состояние ошибки tooan временно поскольку два узла были вниз и hello MaxPercentageUnhealthNodes политики было нарушено.</span><span class="sxs-lookup"><span data-stu-id="32b6c-314">In hello following example, hello cluster went tooan error state temporarily because two nodes were down and hello MaxPercentageUnhealthNodes policy was violated.</span></span> <span data-ttu-id="32b6c-315">Ошибка Hello является временной до текущей операции обновления hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-315">hello error is temporary until hello patching operation is ongoing.</span></span>

![Представление неработоспособного кластера](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

<span data-ttu-id="32b6c-317">Если hello проблема повторяется, см. раздел toohello Устранение неполадок.</span><span class="sxs-lookup"><span data-stu-id="32b6c-317">If hello issue persists, refer toohello Troubleshooting section.</span></span>

<span data-ttu-id="32b6c-318">В.</span><span class="sxs-lookup"><span data-stu-id="32b6c-318">Q.</span></span> <span data-ttu-id="32b6c-319">**Приложение для управления исправлениями находится в состоянии предупреждения**</span><span class="sxs-lookup"><span data-stu-id="32b6c-319">**Patch orchestration app is in warning state**</span></span>

<span data-ttu-id="32b6c-320">О.</span><span class="sxs-lookup"><span data-stu-id="32b6c-320">A.</span></span> <span data-ttu-id="32b6c-321">Проверьте toosee, если отчет о работоспособности учтена для приложения hello hello основную причину.</span><span class="sxs-lookup"><span data-stu-id="32b6c-321">Check toosee if a health report posted against hello application is hello root cause.</span></span> <span data-ttu-id="32b6c-322">Как правило предупреждение hello содержит подробности проблемы hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-322">Usually, hello warning contains details of hello problem.</span></span> <span data-ttu-id="32b6c-323">Если hello проблема временная, приложение hello является ожидаемым tooauto восстановление из этого состояния.</span><span class="sxs-lookup"><span data-stu-id="32b6c-323">If hello issue is transient, hello application is expected tooauto-recover from this state.</span></span>

<span data-ttu-id="32b6c-324">В.</span><span class="sxs-lookup"><span data-stu-id="32b6c-324">Q.</span></span> <span data-ttu-id="32b6c-325">**Что делать, если кластер работает неправильно, и требуется toodo обновление для срочных операционной системы?**</span><span class="sxs-lookup"><span data-stu-id="32b6c-325">**What can I do if my cluster is unhealthy and I need toodo an urgent operating system update?**</span></span>

<span data-ttu-id="32b6c-326">О.</span><span class="sxs-lookup"><span data-stu-id="32b6c-326">A.</span></span> <span data-ttu-id="32b6c-327">orchestration приложение Hello исправление не устанавливает обновления при hello кластер неработоспособен.</span><span class="sxs-lookup"><span data-stu-id="32b6c-327">hello patch orchestration app does not install updates while hello cluster is unhealthy.</span></span> <span data-ttu-id="32b6c-328">Попробуйте toobring кластера tooa работоспособное состояние toounblock hello исправление orchestration приложения рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="32b6c-328">Try toobring your cluster tooa healthy state toounblock hello patch orchestration app workflow.</span></span>

<span data-ttu-id="32b6c-329">В.</span><span class="sxs-lookup"><span data-stu-id="32b6c-329">Q.</span></span> <span data-ttu-id="32b6c-330">**Почему применения исправлений ко всем кластерам слишком долго toorun?**</span><span class="sxs-lookup"><span data-stu-id="32b6c-330">**Why does patching across clusters take so long toorun?**</span></span>

<span data-ttu-id="32b6c-331">О.</span><span class="sxs-lookup"><span data-stu-id="32b6c-331">A.</span></span> <span data-ttu-id="32b6c-332">Hello время, необходимое исправление orchestration приложением hello главным образом зависит hello следующие факторы:</span><span class="sxs-lookup"><span data-stu-id="32b6c-332">hello time needed by hello patch orchestration app is mostly dependent on hello following factors:</span></span>

- <span data-ttu-id="32b6c-333">политика Hello hello службы координатора.</span><span class="sxs-lookup"><span data-stu-id="32b6c-333">hello policy of hello Coordinator Service.</span></span> 
  - <span data-ttu-id="32b6c-334">Здравствуйте, политика по умолчанию `NodeWise`, приводит к исправления одновременно только один узел.</span><span class="sxs-lookup"><span data-stu-id="32b6c-334">hello default policy, `NodeWise`, results in patching only one node at a time.</span></span> <span data-ttu-id="32b6c-335">Особенно в случае hello больше кластеров, мы рекомендуем использовать hello `UpgradeDomainWise` tooachieve политики применения исправлений ко всем кластерам быстрее.</span><span class="sxs-lookup"><span data-stu-id="32b6c-335">Especially in hello case of bigger clusters, we recommend that you use hello `UpgradeDomainWise` policy tooachieve faster patching across clusters.</span></span>
- <span data-ttu-id="32b6c-336">число обновлений, доступных для загрузки и установки Hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-336">hello number of updates available for download and installation.</span></span> 
- <span data-ttu-id="32b6c-337">Здравствуйте, среднее время, необходимое toodownload и установите обновление, которое не должно превышать нескольких часов.</span><span class="sxs-lookup"><span data-stu-id="32b6c-337">hello average time needed toodownload and install an update, which should not exceed a couple of hours.</span></span>
- <span data-ttu-id="32b6c-338">производительность Hello hello виртуальной Машины и пропускную способность сети.</span><span class="sxs-lookup"><span data-stu-id="32b6c-338">hello performance of hello VM and network bandwidth.</span></span>

<span data-ttu-id="32b6c-339">В.</span><span class="sxs-lookup"><span data-stu-id="32b6c-339">Q.</span></span> <span data-ttu-id="32b6c-340">**Почему я вижу некоторые обновления в центре обновления Windows результатов, полученных через REST api, но не в журнале Центра обновления Windows на компьютере hello**</span><span class="sxs-lookup"><span data-stu-id="32b6c-340">**Why do I see some updates in Windows Update results obtained via REST api's, but not under hello Windows Update history on machine?**</span></span>

<span data-ttu-id="32b6c-341">О.</span><span class="sxs-lookup"><span data-stu-id="32b6c-341">A.</span></span> <span data-ttu-id="32b6c-342">Некоторые обновления продуктов должны toobe возврата истории соответствующие обновления, исправления.</span><span class="sxs-lookup"><span data-stu-id="32b6c-342">Some product updates need toobe checked in their respective update/patch history.</span></span> <span data-ttu-id="32b6c-343">Например, сведения об обновлении Защитника Windows не отображаются в журнале Центра обновлений Windows в Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="32b6c-343">Eg: Windows Defender updates do not show up in Windows Update history on Windows Server 2016.</span></span>

## <a name="disclaimers"></a><span data-ttu-id="32b6c-344">Заявления об отказе от ответственности</span><span class="sxs-lookup"><span data-stu-id="32b6c-344">Disclaimers</span></span>

- <span data-ttu-id="32b6c-345">приложение orchestration исправление Hello принимает hello конечным пользователем лицензионного соглашения из центра обновления Windows, от имени пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-345">hello patch orchestration app accepts hello End-User License Agreement of Windows Update on behalf of hello user.</span></span> <span data-ttu-id="32b6c-346">При необходимости приветствия можно отключить в конфигурации hello приложения hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-346">Optionally, hello setting can be turned off in hello configuration of hello application.</span></span>

- <span data-ttu-id="32b6c-347">orchestration приложение Hello исправление собирает использования tootrack телеметрии и производительности.</span><span class="sxs-lookup"><span data-stu-id="32b6c-347">hello patch orchestration app collects telemetry tootrack usage and performance.</span></span> <span data-ttu-id="32b6c-348">Данные телеметрии приложения Hello следует приветствия настройки телеметрии среды выполнения Service Fabric hello (который по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="32b6c-348">hello application’s telemetry follows hello setting of hello Service Fabric runtime’s telemetry setting (which is on by default).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="32b6c-349">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="32b6c-349">Troubleshooting</span></span>

### <a name="a-node-is-not-coming-back-tooup-state"></a><span data-ttu-id="32b6c-350">Узел не возвращается состояние tooup</span><span class="sxs-lookup"><span data-stu-id="32b6c-350">A node is not coming back tooup state</span></span>

<span data-ttu-id="32b6c-351">**узел Hello могло остаться в состоянии отключение из-за**:</span><span class="sxs-lookup"><span data-stu-id="32b6c-351">**hello node might be stuck in a disabling state because**:</span></span>

<span data-ttu-id="32b6c-352">Проверка безопасности находится в состоянии ожидания.</span><span class="sxs-lookup"><span data-stu-id="32b6c-352">A safety check is pending.</span></span> <span data-ttu-id="32b6c-353">tooremedy этой ситуации, чтобы обеспечить достаточное количество узлов в работоспособное состояние.</span><span class="sxs-lookup"><span data-stu-id="32b6c-353">tooremedy this situation, ensure that enough nodes are available in a healthy state.</span></span>

<span data-ttu-id="32b6c-354">**узел Hello могло остаться в отключенном состоянии, так как**:</span><span class="sxs-lookup"><span data-stu-id="32b6c-354">**hello node might be stuck in a disabled state because**:</span></span>

- <span data-ttu-id="32b6c-355">Hello узел был отключен вручную.</span><span class="sxs-lookup"><span data-stu-id="32b6c-355">hello node was disabled manually.</span></span>
- <span data-ttu-id="32b6c-356">Hello узел был отключен из-за tooan задания текущей инфраструктуры Azure.</span><span class="sxs-lookup"><span data-stu-id="32b6c-356">hello node was disabled due tooan ongoing Azure infrastructure job.</span></span>
- <span data-ttu-id="32b6c-357">узел Hello была временно отключена hello узел toopatch приложения hello исправление orchestration.</span><span class="sxs-lookup"><span data-stu-id="32b6c-357">hello node was disabled temporarily by hello patch orchestration app toopatch hello node.</span></span>

<span data-ttu-id="32b6c-358">**Hello узла могло остаться в отключенном состоянии из-за**:</span><span class="sxs-lookup"><span data-stu-id="32b6c-358">**hello node might be stuck in a down state because**:</span></span>

- <span data-ttu-id="32b6c-359">узел Hello вручную поместить в отключенном состоянии.</span><span class="sxs-lookup"><span data-stu-id="32b6c-359">hello node was put in a down state manually.</span></span>
- <span data-ttu-id="32b6c-360">Hello узел находится в режиме перезапуска (который может быть вызвано orchestration приложение hello исправления).</span><span class="sxs-lookup"><span data-stu-id="32b6c-360">hello node is undergoing a restart (which might be triggered by hello patch orchestration app).</span></span>
- <span data-ttu-id="32b6c-361">Hello узел не работает из-за tooa неисправный виртуальная машина или машины проблем или сетевым соединением.</span><span class="sxs-lookup"><span data-stu-id="32b6c-361">hello node is down due tooa faulty VM or machine or network connectivity issues.</span></span>

### <a name="updates-were-skipped-on-some-nodes"></a><span data-ttu-id="32b6c-362">Обновления на некоторых узлах пропущены</span><span class="sxs-lookup"><span data-stu-id="32b6c-362">Updates were skipped on some nodes</span></span>

<span data-ttu-id="32b6c-363">orchestration приложение Hello исправления пытается tooinstall обновления соответствующим toohello перенесения политики Windows.</span><span class="sxs-lookup"><span data-stu-id="32b6c-363">hello patch orchestration app tries tooinstall a Windows update according toohello rescheduling policy.</span></span> <span data-ttu-id="32b6c-364">Служба Hello пытается toorecover hello узел и пропустить политики приложения соответствующим toohello hello обновления.</span><span class="sxs-lookup"><span data-stu-id="32b6c-364">hello service tries toorecover hello node and skip hello update according toohello application policy.</span></span>

<span data-ttu-id="32b6c-365">В этом случае для hello службы узла агента создается отчет о работоспособности уровня предупреждения.</span><span class="sxs-lookup"><span data-stu-id="32b6c-365">In such a case, a warning-level health report is generated against hello Node Agent Service.</span></span> <span data-ttu-id="32b6c-366">результат Hello центра обновления Windows, также содержит hello возможных причин сбоя hello.</span><span class="sxs-lookup"><span data-stu-id="32b6c-366">hello result for Windows Update also contains hello possible reason for hello failure.</span></span>

### <a name="hello-health-of-hello-cluster-goes-tooerror-while-hello-update-installs"></a><span data-ttu-id="32b6c-367">Hello работоспособности кластера hello переходит tooerror во время установки обновления hello</span><span class="sxs-lookup"><span data-stu-id="32b6c-367">hello health of hello cluster goes tooerror while hello update installs</span></span>

<span data-ttu-id="32b6c-368">Ошибочный обновления Windows может привести к остановке hello работоспособности приложения или кластера на конкретный узел или домен обновления.</span><span class="sxs-lookup"><span data-stu-id="32b6c-368">A faulty Windows update can bring down hello health of an application or cluster on a particular node or upgrade domain.</span></span> <span data-ttu-id="32b6c-369">приложение orchestration исправление Hello прекращается любой последующей операции обновления Windows, пока hello кластер является работоспособным.</span><span class="sxs-lookup"><span data-stu-id="32b6c-369">hello patch orchestration app discontinues any subsequent Windows Update operation until hello cluster is healthy again.</span></span>

<span data-ttu-id="32b6c-370">Администратору необходимо вмешательство и определить, почему приложение hello или кластера стал неработоспособным из-за tooWindows обновления.</span><span class="sxs-lookup"><span data-stu-id="32b6c-370">An administrator must intervene and determine why hello application or cluster became unhealthy due tooWindows Update.</span></span>

## <a name="release-notes-"></a><span data-ttu-id="32b6c-371">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="32b6c-371">Release Notes :</span></span>

### <a name="version-110"></a><span data-ttu-id="32b6c-372">Версия 1.1.0</span><span class="sxs-lookup"><span data-stu-id="32b6c-372">Version 1.1.0</span></span>
- <span data-ttu-id="32b6c-373">Общедоступный выпуск</span><span class="sxs-lookup"><span data-stu-id="32b6c-373">Public release</span></span>

### <a name="version-111"></a><span data-ttu-id="32b6c-374">Версии 1.1.1</span><span class="sxs-lookup"><span data-stu-id="32b6c-374">Version 1.1.1</span></span>
- <span data-ttu-id="32b6c-375">Исправлена ошибка в SetupEntryPoint службы агента узла, которая препятствовала установке службы NTService агента узла.</span><span class="sxs-lookup"><span data-stu-id="32b6c-375">Fixed a bug in SetupEntryPoint of NodeAgentService that prevented installation of NodeAgentNTService.</span></span>

### <a name="version-120-latest"></a><span data-ttu-id="32b6c-376">Версия 1.2.0 (последняя версия)</span><span class="sxs-lookup"><span data-stu-id="32b6c-376">Version 1.2.0 (Latest)</span></span>

- <span data-ttu-id="32b6c-377">Исправлены ошибки, связанные с рабочим процессом перезапуска системы.</span><span class="sxs-lookup"><span data-stu-id="32b6c-377">Bug fixes around system restart workflow.</span></span>
- <span data-ttu-id="32b6c-378">Исправление ошибки при создании задач надежного обмена Сообщениями из-за проверки работоспособности toowhich при подготовке задач восстановления не происходит должным образом.</span><span class="sxs-lookup"><span data-stu-id="32b6c-378">Bug fix in creation of RM tasks due toowhich health check during preparing repair tasks wasn't happening as expected.</span></span>
- <span data-ttu-id="32b6c-379">Измененные hello режим запуска для службы windows POANodeSvc из toodelayed автоматически автоматический режим.</span><span class="sxs-lookup"><span data-stu-id="32b6c-379">Changed hello startup mode for windows service POANodeSvc from auto toodelayed-auto.</span></span>
