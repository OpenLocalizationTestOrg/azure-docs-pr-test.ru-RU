---
title: "aaaSet кластера Azure Service Fabric | Документы Microsoft"
description: "Краткое руководство о создании кластера Service Fabric для Windows или Linux в Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 13c60e293d19d607bb41ee4859706508c219a833
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a><span data-ttu-id="e5743-103">Создание первого кластера Service Fabric в Azure</span><span class="sxs-lookup"><span data-stu-id="e5743-103">Create your first Service Fabric cluster on Azure</span></span>
<span data-ttu-id="e5743-104">[Кластер Service Fabric](service-fabric-deploy-anywhere.md) — это подключенный к сети набор виртуальных машин или физических компьютеров, в котором вы развертываете микрослужбы и управляете ими.</span><span class="sxs-lookup"><span data-stu-id="e5743-104">A [Service Fabric cluster](service-fabric-deploy-anywhere.md) is a network-connected set of virtual or physical machines into which your microservices are deployed and managed.</span></span> <span data-ttu-id="e5743-105">Это краткое руководство поможет вам toocreate пяти кластера из узла, ОС Windows или Linux, через hello [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) или [портал Azure](http://portal.azure.com) через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="e5743-105">This quickstart helps you toocreate a five-node cluster, running on either Windows or Linux, through hello [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) or [Azure portal](http://portal.azure.com) in just a few minutes.</span></span>  

<span data-ttu-id="e5743-106">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="e5743-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


## <a name="use-hello-azure-portal"></a><span data-ttu-id="e5743-107">Использовать hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="e5743-107">Use hello Azure portal</span></span>

<span data-ttu-id="e5743-108">Вход toohello портал Azure по адресу [http://portal.azure.com](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e5743-108">Log in toohello Azure portal at [http://portal.azure.com](http://portal.azure.com).</span></span>

### <a name="create-hello-cluster"></a><span data-ttu-id="e5743-109">Создание кластера hello</span><span class="sxs-lookup"><span data-stu-id="e5743-109">Create hello cluster</span></span>

1. <span data-ttu-id="e5743-110">Нажмите кнопку hello **New** кнопка найдена в верхнем левом углу hello hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e5743-110">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>
2. <span data-ttu-id="e5743-111">Выберите **вычислений** из hello **New** и затем выберите **кластера Service Fabric** из hello **вычислений** колонку.</span><span class="sxs-lookup"><span data-stu-id="e5743-111">Select **Compute** from hello **New** blade and then select **Service Fabric Cluster** from hello **Compute** blade.</span></span>
3. <span data-ttu-id="e5743-112">Заполните hello Service Fabric **основы** формы.</span><span class="sxs-lookup"><span data-stu-id="e5743-112">Fill out hello Service Fabric **Basics** form.</span></span> <span data-ttu-id="e5743-113">Для **операционной системы**выберите hello версией Windows или Linux, нужно hello toorun узлов кластера.</span><span class="sxs-lookup"><span data-stu-id="e5743-113">For **Operating system**, select hello version of Windows or Linux you want hello cluster nodes toorun.</span></span> <span data-ttu-id="e5743-114">Hello имя пользователя и пароль, введенный здесь — используется toolog toohello виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="e5743-114">hello user name and password entered here is used toolog in toohello virtual machine.</span></span> <span data-ttu-id="e5743-115">Создайте **группу ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="e5743-115">For **Resource group**, create a new one.</span></span> <span data-ttu-id="e5743-116">Группа ресурсов — это логический контейнер, в котором происходит создание ресурсов Azure и коллективное управление ими.</span><span class="sxs-lookup"><span data-stu-id="e5743-116">A resource group is a logical container into which Azure resources are created and collectively managed.</span></span> <span data-ttu-id="e5743-117">По завершении нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e5743-117">When complete, click **OK**.</span></span>

    ![Результат установки кластера][cluster-setup-basics]

4. <span data-ttu-id="e5743-119">Заполните hello **конфигурации кластера** формы.</span><span class="sxs-lookup"><span data-stu-id="e5743-119">Fill out hello **Cluster configuration** form.</span></span>  <span data-ttu-id="e5743-120">Для параметра **Число типа узлов** введите значение "1".</span><span class="sxs-lookup"><span data-stu-id="e5743-120">For **Node type count**, enter "1".</span></span>

5. <span data-ttu-id="e5743-121">Выберите **тип узла (первичный) 1** и заполнить hello **конфигурации узла типа** формы.</span><span class="sxs-lookup"><span data-stu-id="e5743-121">Select **Node type 1 (Primary)** and fill out hello **Node type configuration** form.</span></span>  <span data-ttu-id="e5743-122">Укажите имя типа узла и установите hello [уровень устойчивости](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) слишком «бронзового.»</span><span class="sxs-lookup"><span data-stu-id="e5743-122">Enter a node type name and set hello [Durability tier](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) too"Bronze."</span></span>  <span data-ttu-id="e5743-123">Выберите размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e5743-123">Select a VM size.</span></span>

    <span data-ttu-id="e5743-124">Размер виртуальной Машины hello, количество виртуальных машин, пользовательские конечные точки определяют типы узлов и других параметров для hello виртуальных машин данного типа.</span><span class="sxs-lookup"><span data-stu-id="e5743-124">Node types define hello VM size, number of VMs, custom endpoints, and other settings for hello VMs of that type.</span></span> <span data-ttu-id="e5743-125">Каждый определенный тип узел настроен как набор масштабирования отдельной виртуальной машине — как набор используемых toodeploy и управляемых виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e5743-125">Each node type defined is set up as a separate virtual machine scale set, which is used toodeploy and managed virtual machines as a set.</span></span> <span data-ttu-id="e5743-126">Каждый тип узла поддерживает возможность независимого масштабирования, имеет разные наборы открытых портов и собственные метрики емкости.</span><span class="sxs-lookup"><span data-stu-id="e5743-126">Each node type can be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>  <span data-ttu-id="e5743-127">Hello первой или основной, тип узла — где размещаются Service Fabric системных служб и должен иметь пять или более виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e5743-127">hello first, or primary, node type is where Service Fabric system services are hosted and must have five or more VMs.</span></span>

    <span data-ttu-id="e5743-128">Для любой рабочей развернутой службы важным шагом является [планирование загрузки](service-fabric-cluster-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="e5743-128">For any production deployment, [capacity planning](service-fabric-cluster-capacity.md) is an important step.</span></span>  <span data-ttu-id="e5743-129">Так как в этом кратком руководстве вы не будете выполнять приложения, вы можете выбрать размер виртуальной машины *DS1_v2 Standard*.</span><span class="sxs-lookup"><span data-stu-id="e5743-129">For this quick start, however, you aren't running applications so select a *DS1_v2 Standard* VM size.</span></span>  <span data-ttu-id="e5743-130">Выберите «Серебряный» для hello [уровень надежности](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) и начального набора масштабирования виртуальных машин емкость 5.</span><span class="sxs-lookup"><span data-stu-id="e5743-130">Select "Silver" for hello [reliability tier](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) and an initial virtual machine scale set capacity of 5.</span></span>  

    <span data-ttu-id="e5743-131">Пользовательские конечные точки открыть порты в подсистеме балансировки нагрузки Azure hello, что позволяет подключаться с приложениями, работающими на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="e5743-131">Custom endpoints open up ports in hello Azure load balancer so that you can connect with applications running on hello cluster.</span></span>  <span data-ttu-id="e5743-132">Введите «80, 8172» tooopen порты 80 и 8172.</span><span class="sxs-lookup"><span data-stu-id="e5743-132">Enter "80, 8172" tooopen up ports 80 and 8172.</span></span>

    <span data-ttu-id="e5743-133">Не устанавливайте hello **Настройка дополнительных параметров** поле, которое используется для настройки конечных точек управления TCP или HTTP, диапазонов портов приложения, [ограничения размещения](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), и [емкости свойства](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="e5743-133">Do not check hello **Configure advanced settings** box, which is used for customizing TCP/HTTP management endpoints, application port ranges, [placement constraints](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), and [capacity properties](service-fabric-cluster-resource-manager-metrics.md).</span></span>    

    <span data-ttu-id="e5743-134">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e5743-134">Select **OK**.</span></span>

6. <span data-ttu-id="e5743-135">В hello **конфигурации кластера** задайте **диагностики** слишком**на**.</span><span class="sxs-lookup"><span data-stu-id="e5743-135">In hello **Cluster configuration** form, set **Diagnostics** too**On**.</span></span>  <span data-ttu-id="e5743-136">Для краткого руководства, нет необходимости tooenter любое [структуры параметр](service-fabric-cluster-fabric-settings.md) свойства.</span><span class="sxs-lookup"><span data-stu-id="e5743-136">For this quickstart, you do not need tooenter any [fabric setting](service-fabric-cluster-fabric-settings.md) properties.</span></span>  <span data-ttu-id="e5743-137">В **версия Fabric**выберите **автоматического** режим обновления, чтобы корпорация Майкрософт автоматически обновляет версию hello hello структуры работающего кластера hello.</span><span class="sxs-lookup"><span data-stu-id="e5743-137">In **Fabric version**, select **Automatic** upgrade mode so that Microsoft automatically updates hello version of hello fabric code running hello cluster.</span></span>  <span data-ttu-id="e5743-138">Установить режим hello слишком**вручную** Если требуется слишком[выберите поддерживаемую версию](service-fabric-cluster-upgrade.md) tooupgrade для.</span><span class="sxs-lookup"><span data-stu-id="e5743-138">Set hello mode too**Manual** if you want too[choose a supported version](service-fabric-cluster-upgrade.md) tooupgrade to.</span></span> 

    ![Конфигурация типа узла][node-type-config]

    <span data-ttu-id="e5743-140">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e5743-140">Select **OK**.</span></span>

7. <span data-ttu-id="e5743-141">Заполните hello **безопасности** формы.</span><span class="sxs-lookup"><span data-stu-id="e5743-141">Fill out hello **Security** form.</span></span>  <span data-ttu-id="e5743-142">Для этого руководства выберите **незащищенный** режим.</span><span class="sxs-lookup"><span data-stu-id="e5743-142">For this quick start select **Unsecure**.</span></span>  <span data-ttu-id="e5743-143">Это настоятельно рекомендуется toocreate безопасного кластера для рабочих нагрузок, тем не менее, поскольку любой пользователь может анонимно подключения tooan небезопасные кластера и выполнять операции управления.</span><span class="sxs-lookup"><span data-stu-id="e5743-143">It is highly recommended toocreate a secure cluster for production workloads, however, since anyone can anonymously connect tooan unsecure cluster and perform management operations.</span></span>  

    <span data-ttu-id="e5743-144">Сертификаты используются в Service Fabric tooprovide проверки подлинности и шифрования toosecure различные аспекты кластера и его применения.</span><span class="sxs-lookup"><span data-stu-id="e5743-144">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="e5743-145">Дополнительные сведения о том, как сертификаты используются в Service Fabric, см. в статье [Сценарии защиты кластера Service Fabric](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="e5743-145">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md).</span></span>  <span data-ttu-id="e5743-146">Использование Azure Active Directory или tooset сертификаты для обеспечения безопасности приложения, проверка подлинности пользователя tooenable [создания кластера из шаблона диспетчера ресурсов](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="e5743-146">tooenable user authentication using Azure Active Directory or tooset up certificates for application security, [create a cluster from a Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span>

    <span data-ttu-id="e5743-147">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e5743-147">Select **OK**.</span></span>

8. <span data-ttu-id="e5743-148">Просмотрите hello сводки.</span><span class="sxs-lookup"><span data-stu-id="e5743-148">Review hello summary.</span></span>  <span data-ttu-id="e5743-149">Если вы хотите toodownload введено шаблона диспетчера ресурсов, построенная hello параметры, выберите **загрузки шаблона и параметров**.</span><span class="sxs-lookup"><span data-stu-id="e5743-149">If you'd like toodownload a Resource Manager template built from hello settings you entered, select **Download template and parameters**.</span></span>  <span data-ttu-id="e5743-150">Выберите **создать** toocreate hello кластера.</span><span class="sxs-lookup"><span data-stu-id="e5743-150">Select **Create** toocreate hello cluster.</span></span>

    <span data-ttu-id="e5743-151">Вы увидите ход создания hello в уведомлениях hello.</span><span class="sxs-lookup"><span data-stu-id="e5743-151">You can see hello creation progress in hello notifications.</span></span> <span data-ttu-id="e5743-152">(Щелкните значок колокольчика «hello» рядом с hello строку состояния в hello верхнем правом углу экрана.) Если вы нажали кнопку **tooStartboard ПИН-код** при создании кластера hello, см **развертывание кластера Service Fabric** закрепленные toohello **запустить** доски.</span><span class="sxs-lookup"><span data-stu-id="e5743-152">(Click hello "Bell" icon near hello status bar at hello upper right of your screen.) If you clicked **Pin tooStartboard** while creating hello cluster, you see **Deploying Service Fabric Cluster** pinned toohello **Start** board.</span></span>

### <a name="view-cluster-status"></a><span data-ttu-id="e5743-153">Просмотр сведений о состоянии кластера</span><span class="sxs-lookup"><span data-stu-id="e5743-153">View cluster status</span></span>
<span data-ttu-id="e5743-154">После создания кластера можно проверить кластер на hello **Обзор** колонке hello портала.</span><span class="sxs-lookup"><span data-stu-id="e5743-154">Once your cluster is created, you can inspect your cluster in hello **Overview** blade in hello portal.</span></span> <span data-ttu-id="e5743-155">Теперь можно просмотреть сведения hello кластера на панели мониторинга hello, включая общедоступную конечную точку кластера hello и ссылка tooService Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="e5743-155">You can now see hello details of your cluster in hello dashboard, including hello cluster's public endpoint and a link tooService Fabric Explorer.</span></span>

![Состояние кластера][cluster-status]

### <a name="visualize-hello-cluster-using-service-fabric-explorer"></a><span data-ttu-id="e5743-157">Визуализация hello кластера с помощью обозревателя Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e5743-157">Visualize hello cluster using Service Fabric explorer</span></span>
<span data-ttu-id="e5743-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) — хорошее средство для визуализации кластера и управления приложениями.</span><span class="sxs-lookup"><span data-stu-id="e5743-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="e5743-159">Обозреватель Service Fabric — это служба, запускаемую в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="e5743-159">Service Fabric Explorer is a service that runs in hello cluster.</span></span>  <span data-ttu-id="e5743-160">Доступ к ним через веб-браузер, нажав кнопку hello **Service Fabric Explorer** связь кластера hello **Обзор** портале hello.</span><span class="sxs-lookup"><span data-stu-id="e5743-160">Access it using a web browser by clicking hello **Service Fabric Explorer** link of hello cluster **Overview** page in hello portal.</span></span>  <span data-ttu-id="e5743-161">Можно также ввести адрес hello непосредственно в браузер hello: [http://quickstartcluster.westus.cloudapp.azure.com:19080/обозреватель](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span><span class="sxs-lookup"><span data-stu-id="e5743-161">You can also enter hello address directly into hello browser: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span></span>

<span data-ttu-id="e5743-162">панели мониторинга кластера Hello Обзор кластера, в том числе сводную приложения и состояние работоспособности узла.</span><span class="sxs-lookup"><span data-stu-id="e5743-162">hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="e5743-163">представление узла Hello отображает hello физическую структуру hello кластера.</span><span class="sxs-lookup"><span data-stu-id="e5743-163">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="e5743-164">Для каждого узла можно просмотреть, какие приложения были развернуты на этом узле</span><span class="sxs-lookup"><span data-stu-id="e5743-164">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-toohello-cluster-using-powershell"></a><span data-ttu-id="e5743-166">Подключите кластер toohello с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5743-166">Connect toohello cluster using PowerShell</span></span>
<span data-ttu-id="e5743-167">Убедитесь, что данный кластер hello выполняется путем подключения с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e5743-167">Verify that hello cluster is running by connecting using PowerShell.</span></span>  <span data-ttu-id="e5743-168">Hello модуля ServiceFabric PowerShell устанавливается вместе с hello [пакет Service Fabric SDK](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e5743-168">hello ServiceFabric PowerShell module is installed with hello [Service Fabric SDK](service-fabric-get-started.md).</span></span>  <span data-ttu-id="e5743-169">Hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) командлет устанавливает toohello подключения кластера.</span><span class="sxs-lookup"><span data-stu-id="e5743-169">hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection toohello cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
<span data-ttu-id="e5743-170">В разделе [кластера безопасное подключение tooa](service-fabric-connect-to-secure-cluster.md) другие примеры соединения tooa кластера.</span><span class="sxs-lookup"><span data-stu-id="e5743-170">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting tooa cluster.</span></span> <span data-ttu-id="e5743-171">После подключения кластера toohello, используйте hello [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) toodisplay командлет список узлов в hello сведения о кластере и состоянии для каждого узла.</span><span class="sxs-lookup"><span data-stu-id="e5743-171">After connecting toohello cluster, use hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay a list of nodes in hello cluster and status information for each node.</span></span> <span data-ttu-id="e5743-172">**Состояние работоспособности** каждого узла должно иметь значение *ОК*.</span><span class="sxs-lookup"><span data-stu-id="e5743-172">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\Users\sfuser> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName     IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- --------     --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     _nodetype1_2 10.0.0.6        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_1 10.0.0.5        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_0 10.0.0.4        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_4 10.0.0.8        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_3 10.0.0.7        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
```

### <a name="remove-hello-cluster"></a><span data-ttu-id="e5743-173">Удаление кластера hello</span><span class="sxs-lookup"><span data-stu-id="e5743-173">Remove hello cluster</span></span>
<span data-ttu-id="e5743-174">Кластер Service Fabric состоит из других ресурсов Azure в дополнение к этому toohello сам ресурс кластера.</span><span class="sxs-lookup"><span data-stu-id="e5743-174">A Service Fabric cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="e5743-175">Поэтому toocompletely Удаление кластера Service Fabric требуется также toodelete Здравствуйте, все ресурсы, которые оно состоит из.</span><span class="sxs-lookup"><span data-stu-id="e5743-175">So toocompletely delete a Service Fabric cluster you also need toodelete all hello resources it is made of.</span></span> <span data-ttu-id="e5743-176">Hello простейший способ toodelete hello кластера и все ресурсы hello, которые он использует является группой ресурсов toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="e5743-176">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span> <span data-ttu-id="e5743-177">Для других способов toodelete кластера или toodelete некоторых (но не всех) hello ресурсы в группе ресурсов см. [удалить кластер](service-fabric-cluster-delete.md)</span><span class="sxs-lookup"><span data-stu-id="e5743-177">For other ways toodelete a cluster or toodelete some (but not all) hello resources in a resource group, see [Delete a cluster](service-fabric-cluster-delete.md)</span></span>

<span data-ttu-id="e5743-178">Удаление группы ресурсов в hello портала Azure:</span><span class="sxs-lookup"><span data-stu-id="e5743-178">Delete a resource group in hello Azure portal:</span></span>
1. <span data-ttu-id="e5743-179">Переход кластера Service Fabric toohello требуется toodelete.</span><span class="sxs-lookup"><span data-stu-id="e5743-179">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
2. <span data-ttu-id="e5743-180">Нажмите кнопку hello **группы ресурсов** имя на странице essentials hello кластера.</span><span class="sxs-lookup"><span data-stu-id="e5743-180">Click hello **Resource Group** name on hello cluster essentials page.</span></span>
3. <span data-ttu-id="e5743-181">В hello **Essentials группы ресурсов** щелкните **удалить группу ресурсов** и следуйте появляющимся hello на этой странице toocomplete hello удаления группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="e5743-181">In hello **Resource Group Essentials** page, click **Delete resource group** and follow hello instructions on that page toocomplete hello deletion of hello resource group.</span></span>
    <span data-ttu-id="e5743-182">![Удаление группы ресурсов hello][cluster-delete]</span><span class="sxs-lookup"><span data-stu-id="e5743-182">![Delete hello resource group][cluster-delete]</span></span>


## <a name="use-azure-powershell-toodeploy-a-secure-cluster"></a><span data-ttu-id="e5743-183">Использование Azure Powershell toodeploy безопасности кластера</span><span class="sxs-lookup"><span data-stu-id="e5743-183">Use Azure Powershell toodeploy a secure cluster</span></span>
1. <span data-ttu-id="e5743-184">Загрузите hello [Azure Powershell 4.0 или более поздней версии модуля](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) на компьютере.</span><span class="sxs-lookup"><span data-stu-id="e5743-184">Download hello [Azure Powershell module version 4.0 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) on your machine.</span></span>

2. <span data-ttu-id="e5743-185">Откройте окно Windows PowerShell, hello выполнить следующую команду.</span><span class="sxs-lookup"><span data-stu-id="e5743-185">Open a Windows PowerShell window, Run hello following command.</span></span> 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    <span data-ttu-id="e5743-186">Должны появиться следующие выходные данные как toohello.</span><span class="sxs-lookup"><span data-stu-id="e5743-186">You should see an output similar toohello following.</span></span>

    ![Список PowerShell][ps-list]

3. <span data-ttu-id="e5743-188">TooAzure входа и toocreate hello кластеру toowhich подписки выберите hello</span><span class="sxs-lookup"><span data-stu-id="e5743-188">Login tooAzure and Select hello subscription toowhich you want toocreate hello cluster</span></span>

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. <span data-ttu-id="e5743-189">Выполнения hello, следующая команда toonow создания безопасного кластера.</span><span class="sxs-lookup"><span data-stu-id="e5743-189">Run hello following command toonow create a secure cluster.</span></span> <span data-ttu-id="e5743-190">Не забудьте toocustomize hello параметров.</span><span class="sxs-lookup"><span data-stu-id="e5743-190">Do not forget toocustomize hello parameters.</span></span> 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also hello name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    <span data-ttu-id="e5743-191">Команда Hello может занять от toocomplete минут too30 10 минут hello конец, вы должны получить следующие выходные данные как toohello.</span><span class="sxs-lookup"><span data-stu-id="e5743-191">hello command can take anywhere from 10 minutes too30 minutes toocomplete, at hello end of it, you should get an output similar toohello following.</span></span> <span data-ttu-id="e5743-192">сведения о сертификате hello, hello KeyVault, где был загружен, и hello локальную папку, куда копируется сертификат hello Hello вывода.</span><span class="sxs-lookup"><span data-stu-id="e5743-192">hello output has information about hello certificate, hello KeyVault where it was uploaded to, and hello local folder where hello certificate is copied.</span></span> 

    ![Результат PowerShell][ps-out]

5. <span data-ttu-id="e5743-194">Копировать все выходные данные hello и сохраните текстовый файл tooa образом toorefer tooit.</span><span class="sxs-lookup"><span data-stu-id="e5743-194">Copy hello entire output and save tooa text file as we need toorefer tooit.</span></span> <span data-ttu-id="e5743-195">Запишите следующие сведения из выходных данных hello hello.</span><span class="sxs-lookup"><span data-stu-id="e5743-195">Make a note of hello following information from hello output.</span></span> 

    - <span data-ttu-id="e5743-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span><span class="sxs-lookup"><span data-stu-id="e5743-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span></span>
    - <span data-ttu-id="e5743-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span><span class="sxs-lookup"><span data-stu-id="e5743-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span></span>
    - <span data-ttu-id="e5743-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span><span class="sxs-lookup"><span data-stu-id="e5743-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span></span>
    - <span data-ttu-id="e5743-199">**ClientConnectionEndpointPort** : 19000</span><span class="sxs-lookup"><span data-stu-id="e5743-199">**ClientConnectionEndpointPort** : 19000</span></span>

### <a name="install-hello-certificate-on-your-local-machine"></a><span data-ttu-id="e5743-200">Установите сертификат hello на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="e5743-200">Install hello certificate on your local machine</span></span>
  
<span data-ttu-id="e5743-201">кластер toohello tooconnect, потребуется tooinstall hello сертификат в хранилище персональных (Мои) hello hello текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="e5743-201">tooconnect toohello cluster, you need tooinstall hello certificate into hello Personal (My) store of hello current user.</span></span> 

<span data-ttu-id="e5743-202">Запустите следующие PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="e5743-202">Run hello following PowerShell</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\hello name of hello cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

<span data-ttu-id="e5743-203">Теперь вы находитесь кластера безопасных готовы tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="e5743-203">You are now ready tooconnect tooyour secure cluster.</span></span>

### <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="e5743-204">Подключите кластер безопасного tooa</span><span class="sxs-lookup"><span data-stu-id="e5743-204">Connect tooa secure cluster</span></span> 

<span data-ttu-id="e5743-205">Запустите следующие hello PowerShell команды tooconnect tooa безопасности кластера.</span><span class="sxs-lookup"><span data-stu-id="e5743-205">Run hello following PowerShell command tooconnect tooa secure cluster.</span></span> <span data-ttu-id="e5743-206">сведения о сертификате Hello должно соответствовать сертификат, который был используется tooset hello кластера.</span><span class="sxs-lookup"><span data-stu-id="e5743-206">hello certificate details must match a certificate that was used tooset up hello cluster.</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


<span data-ttu-id="e5743-207">Следующий пример показывает hello Hello завершено параметров:</span><span class="sxs-lookup"><span data-stu-id="e5743-207">hello following example shows hello completed parameters:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="e5743-208">Запустите hello, выполнив команду toocheck, что вы подключены и hello кластера находится в работоспособном состоянии.</span><span class="sxs-lookup"><span data-stu-id="e5743-208">Run hello following command toocheck that you are connected and hello cluster is healthy.</span></span>

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-tooyour-cluster-from-visual-studio"></a><span data-ttu-id="e5743-209">Публикация кластера tooyour приложения из Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e5743-209">Publish your apps tooyour cluster from Visual Studio</span></span>

<span data-ttu-id="e5743-210">Теперь, когда вы настроили кластер Azure, можно опубликовать tooit вашего приложения из Visual Studio по следующей hello [кластера tooan публикации](service-fabric-publish-app-remote-cluster.md) документа.</span><span class="sxs-lookup"><span data-stu-id="e5743-210">Now that you have set up an Azure cluster, you can publish your applications tooit from Visual Studio by following hello [Publish tooan cluster](service-fabric-publish-app-remote-cluster.md) document.</span></span> 

### <a name="remove-hello-cluster"></a><span data-ttu-id="e5743-211">Удаление кластера hello</span><span class="sxs-lookup"><span data-stu-id="e5743-211">Remove hello cluster</span></span>
<span data-ttu-id="e5743-212">Кластер состоит из других ресурсов Azure в дополнение к этому toohello сам ресурс кластера.</span><span class="sxs-lookup"><span data-stu-id="e5743-212">A cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="e5743-213">Hello простейший способ toodelete hello кластера и все ресурсы hello, которые он использует является группой ресурсов toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="e5743-213">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span> 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a><span data-ttu-id="e5743-214">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e5743-214">Next steps</span></span>
<span data-ttu-id="e5743-215">Теперь, когда вы настроили кластеру разработки, попробуйте hello следующее:</span><span class="sxs-lookup"><span data-stu-id="e5743-215">Now that you have set up a development cluster, try hello following:</span></span>
* [<span data-ttu-id="e5743-216">Создание безопасного кластера на портале hello</span><span class="sxs-lookup"><span data-stu-id="e5743-216">Create a secure cluster in hello portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* <span data-ttu-id="e5743-217">[Create a cluster from a template](service-fabric-cluster-creation-via-arm.md) (Создание кластера из шаблона)</span><span class="sxs-lookup"><span data-stu-id="e5743-217">[Create a cluster from a template](service-fabric-cluster-creation-via-arm.md)</span></span> 
* [<span data-ttu-id="e5743-218">Разверните приложения с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5743-218">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
