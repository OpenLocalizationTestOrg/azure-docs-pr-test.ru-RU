---
title: "Настройка кластера Azure Service Fabric | Документация Майкрософт"
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
ms.openlocfilehash: ec59450052b377412a28f7eaf55d1f1512b55195
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a><span data-ttu-id="ee4f6-103">Создание первого кластера Service Fabric в Azure</span><span class="sxs-lookup"><span data-stu-id="ee4f6-103">Create your first Service Fabric cluster on Azure</span></span>
<span data-ttu-id="ee4f6-104">[Кластер Service Fabric](service-fabric-deploy-anywhere.md) — это подключенный к сети набор виртуальных машин или физических компьютеров, в котором вы развертываете микрослужбы и управляете ими.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-104">A [Service Fabric cluster](service-fabric-deploy-anywhere.md) is a network-connected set of virtual or physical machines into which your microservices are deployed and managed.</span></span> <span data-ttu-id="ee4f6-105">Используя это краткое руководство, вы сможете за несколько минут создать кластер с пятью узлами под управлением Windows или Linux на [портале Azure](http://portal.azure.com) или с помощью [Azure PowerShell](https://msdn.microsoft.com/library/dn135248).</span><span class="sxs-lookup"><span data-stu-id="ee4f6-105">This quickstart helps you to create a five-node cluster, running on either Windows or Linux, through the [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) or [Azure portal](http://portal.azure.com) in just a few minutes.</span></span>  

<span data-ttu-id="ee4f6-106">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) , прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


## <a name="use-the-azure-portal"></a><span data-ttu-id="ee4f6-107">Использование портала Azure</span><span class="sxs-lookup"><span data-stu-id="ee4f6-107">Use the Azure portal</span></span>

<span data-ttu-id="ee4f6-108">Войдите на портал Azure. Для этого перейдите по ссылке [http://portal.azure.com](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ee4f6-108">Log in to the Azure portal at [http://portal.azure.com](http://portal.azure.com).</span></span>

### <a name="create-the-cluster"></a><span data-ttu-id="ee4f6-109">Создание кластера</span><span class="sxs-lookup"><span data-stu-id="ee4f6-109">Create the cluster</span></span>

1. <span data-ttu-id="ee4f6-110">Щелкните **Создать** в верхнем левом углу портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-110">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>
2. <span data-ttu-id="ee4f6-111">Выберите **Среда выполнения приложений** в колонке **Создать**, а затем в колонке **Среда выполнения приложений** выберите **Кластер Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-111">Select **Compute** from the **New** blade and then select **Service Fabric Cluster** from the **Compute** blade.</span></span>
3. <span data-ttu-id="ee4f6-112">Заполните форму Service Fabric **Основы**.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-112">Fill out the Service Fabric **Basics** form.</span></span> <span data-ttu-id="ee4f6-113">Выберите версию **операционной системы** Windows или Linux для запуска узлов кластера.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-113">For **Operating system**, select the version of Windows or Linux you want the cluster nodes to run.</span></span> <span data-ttu-id="ee4f6-114">Имя пользователя и пароль понадобятся для входа на виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-114">The user name and password entered here is used to log in to the virtual machine.</span></span> <span data-ttu-id="ee4f6-115">Создайте **группу ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-115">For **Resource group**, create a new one.</span></span> <span data-ttu-id="ee4f6-116">Группа ресурсов — это логический контейнер, в котором происходит создание ресурсов Azure и коллективное управление ими.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-116">A resource group is a logical container into which Azure resources are created and collectively managed.</span></span> <span data-ttu-id="ee4f6-117">По завершении нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-117">When complete, click **OK**.</span></span>

    ![Результат установки кластера][cluster-setup-basics]

4. <span data-ttu-id="ee4f6-119">Заполните форму **Конфигурация кластера**.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-119">Fill out the **Cluster configuration** form.</span></span>  <span data-ttu-id="ee4f6-120">Для параметра **Число типа узлов** введите значение "1".</span><span class="sxs-lookup"><span data-stu-id="ee4f6-120">For **Node type count**, enter "1".</span></span>

5. <span data-ttu-id="ee4f6-121">Выберите **Node type 1 (Primary)** (Тип узла 1 (первичный)) и заполните форму **Конфигурация типа узла**.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-121">Select **Node type 1 (Primary)** and fill out the **Node type configuration** form.</span></span>  <span data-ttu-id="ee4f6-122">Укажите имя типа узла и задайте для параметра [Уровень устойчивости](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) значение "Бронзовый".</span><span class="sxs-lookup"><span data-stu-id="ee4f6-122">Enter a node type name and set the [Durability tier](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) to "Bronze."</span></span>  <span data-ttu-id="ee4f6-123">Выберите размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-123">Select a VM size.</span></span>

    <span data-ttu-id="ee4f6-124">Типы узлов определяют размер виртуальной машины, их число, пользовательские конечные точки и другие параметры для виртуальных машин этого типа.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-124">Node types define the VM size, number of VMs, custom endpoints, and other settings for the VMs of that type.</span></span> <span data-ttu-id="ee4f6-125">Каждый определенный тип узла настроен как отдельный масштабируемый набор виртуальных машин, используемый для развертывания виртуальных машин и управления ими в наборе.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-125">Each node type defined is set up as a separate virtual machine scale set, which is used to deploy and managed virtual machines as a set.</span></span> <span data-ttu-id="ee4f6-126">Каждый тип узла поддерживает возможность независимого масштабирования, имеет разные наборы открытых портов и собственные метрики емкости.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-126">Each node type can be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>  <span data-ttu-id="ee4f6-127">Первый или первичный тип узла определяет размещение системных служб Service Fabric и должен включать от пяти виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-127">The first, or primary, node type is where Service Fabric system services are hosted and must have five or more VMs.</span></span>

    <span data-ttu-id="ee4f6-128">Для любой рабочей развернутой службы важным шагом является [планирование загрузки](service-fabric-cluster-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="ee4f6-128">For any production deployment, [capacity planning](service-fabric-cluster-capacity.md) is an important step.</span></span>  <span data-ttu-id="ee4f6-129">Так как в этом кратком руководстве вы не будете выполнять приложения, вы можете выбрать размер виртуальной машины *DS1_v2 Standard*.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-129">For this quick start, however, you aren't running applications so select a *DS1_v2 Standard* VM size.</span></span>  <span data-ttu-id="ee4f6-130">Для [уровня надежности](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) задайте значение Silver, а для масштабируемого набора виртуальных машин задайте начальную мощность 5.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-130">Select "Silver" for the [reliability tier](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) and an initial virtual machine scale set capacity of 5.</span></span>  

    <span data-ttu-id="ee4f6-131">Пользовательские конечные точки открывают порты в подсистеме балансировщика нагрузки Azure, поэтому вы сможете подключиться к приложениям, выполняющимся в кластере.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-131">Custom endpoints open up ports in the Azure load balancer so that you can connect with applications running on the cluster.</span></span>  <span data-ttu-id="ee4f6-132">Введите "80, 8172", чтобы открыть порты 80 и 8172.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-132">Enter "80, 8172" to open up ports 80 and 8172.</span></span>

    <span data-ttu-id="ee4f6-133">Не устанавливайте флажок в поле **Настройка дополнительных параметров**, используемом для настройки конечных точек управления протоколами TCP и HTTP, диапазонов порта приложения, [ограничений на размещение](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints) и [свойств емкости](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="ee4f6-133">Do not check the **Configure advanced settings** box, which is used for customizing TCP/HTTP management endpoints, application port ranges, [placement constraints](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), and [capacity properties](service-fabric-cluster-resource-manager-metrics.md).</span></span>    

    <span data-ttu-id="ee4f6-134">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-134">Select **OK**.</span></span>

6. <span data-ttu-id="ee4f6-135">В форме **Конфигурация кластера** задайте значение **Вкл.** для **диагностики**.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-135">In the **Cluster configuration** form, set **Diagnostics** to **On**.</span></span>  <span data-ttu-id="ee4f6-136">При работе с этим руководством не нужно вводить свойства [настроек структуры](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="ee4f6-136">For this quickstart, you do not need to enter any [fabric setting](service-fabric-cluster-fabric-settings.md) properties.</span></span>  <span data-ttu-id="ee4f6-137">В разделе **Версия Fabric** выберите режим **автоматического** обновления, чтобы корпорация Майкрософт автоматически обновляла версию кода Fabric, выполняющегося в кластере.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-137">In **Fabric version**, select **Automatic** upgrade mode so that Microsoft automatically updates the version of the fabric code running the cluster.</span></span>  <span data-ttu-id="ee4f6-138">Если вы хотите [выбирать поддерживаемую версию](service-fabric-cluster-upgrade.md), задайте режим **Вручную**.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-138">Set the mode to **Manual** if you want to [choose a supported version](service-fabric-cluster-upgrade.md) to upgrade to.</span></span> 

    ![Конфигурация типа узла][node-type-config]

    <span data-ttu-id="ee4f6-140">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-140">Select **OK**.</span></span>

7. <span data-ttu-id="ee4f6-141">Заполните форму **Безопасность**.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-141">Fill out the **Security** form.</span></span>  <span data-ttu-id="ee4f6-142">Для этого руководства выберите **незащищенный** режим.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-142">For this quick start select **Unsecure**.</span></span>  <span data-ttu-id="ee4f6-143">Учитывая, что любой пользователь может анонимно подключиться к незащищенному кластеру и выполнять различные операции управления, для производственных рабочих нагрузок мы настоятельно рекомендуем создать безопасное подключение к кластеру.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-143">It is highly recommended to create a secure cluster for production workloads, however, since anyone can anonymously connect to an unsecure cluster and perform management operations.</span></span>  

    <span data-ttu-id="ee4f6-144">Сертификаты используются в Service Fabric, чтобы обеспечить функции аутентификации и шифрования для защиты различных аспектов кластера и его приложений.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-144">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="ee4f6-145">Дополнительные сведения о том, как сертификаты используются в Service Fabric, см. в статье [Сценарии защиты кластера Service Fabric](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="ee4f6-145">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md).</span></span>  <span data-ttu-id="ee4f6-146">Чтобы включить проверку подлинности пользователя с помощью Azure Active Directory или настроить сертификаты для безопасности приложения, [создайте кластер из шаблона Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="ee4f6-146">To enable user authentication using Azure Active Directory or to set up certificates for application security, [create a cluster from a Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span>

    <span data-ttu-id="ee4f6-147">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-147">Select **OK**.</span></span>

8. <span data-ttu-id="ee4f6-148">Проверьте сводные данные.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-148">Review the summary.</span></span>  <span data-ttu-id="ee4f6-149">Если вы хотите скачать шаблон Resource Manager, построенный из введенных вами параметров, выберите **Скачать шаблон и параметры**.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-149">If you'd like to download a Resource Manager template built from the settings you entered, select **Download template and parameters**.</span></span>  <span data-ttu-id="ee4f6-150">Выберите **Создать**, чтобы создать кластер.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-150">Select **Create** to create the cluster.</span></span>

    <span data-ttu-id="ee4f6-151">Ход создания кластера будет отображаться в области уведомлений.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-151">You can see the creation progress in the notifications.</span></span> <span data-ttu-id="ee4f6-152">(Щелкните значок колокольчика рядом со строкой состояния в правом верхнем углу экрана). Если при создании кластера вы установили флажок **Закрепить на начальной панели**, то на **начальной доске** вы увидите закрепленный элемент **Deploying Service Fabric Cluster** (Развертывание кластера Service Fabric).</span><span class="sxs-lookup"><span data-stu-id="ee4f6-152">(Click the "Bell" icon near the status bar at the upper right of your screen.) If you clicked **Pin to Startboard** while creating the cluster, you see **Deploying Service Fabric Cluster** pinned to the **Start** board.</span></span>

### <a name="view-cluster-status"></a><span data-ttu-id="ee4f6-153">Просмотр сведений о состоянии кластера</span><span class="sxs-lookup"><span data-stu-id="ee4f6-153">View cluster status</span></span>
<span data-ttu-id="ee4f6-154">После создания кластера его можно просмотреть на портале в колонке **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-154">Once your cluster is created, you can inspect your cluster in the **Overview** blade in the portal.</span></span> <span data-ttu-id="ee4f6-155">На панели мониторинга отобразятся подробные сведения о кластере, включая общедоступную конечную точку кластера и ссылку на Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-155">You can now see the details of your cluster in the dashboard, including the cluster's public endpoint and a link to Service Fabric Explorer.</span></span>

![Состояние кластера][cluster-status]

### <a name="visualize-the-cluster-using-service-fabric-explorer"></a><span data-ttu-id="ee4f6-157">Визуализация кластера с помощью Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="ee4f6-157">Visualize the cluster using Service Fabric explorer</span></span>
<span data-ttu-id="ee4f6-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) — хорошее средство для визуализации кластера и управления приложениями.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="ee4f6-159">Service Fabric Explorer — это служба, выполняющаяся в кластере.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-159">Service Fabric Explorer is a service that runs in the cluster.</span></span>  <span data-ttu-id="ee4f6-160">Чтобы получить доступ к этой службе, используйте веб-браузер. Для этого щелкните ссылку **Service Fabric Explorer** на странице **обзора** кластера.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-160">Access it using a web browser by clicking the **Service Fabric Explorer** link of the cluster **Overview** page in the portal.</span></span>  <span data-ttu-id="ee4f6-161">Вы также можете ввести адрес прямо в браузер [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span><span class="sxs-lookup"><span data-stu-id="ee4f6-161">You can also enter the address directly into the browser: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span></span>

<span data-ttu-id="ee4f6-162">На панели мониторинга кластера представлены общие сведения о кластере, включая общие сведения о приложении и работоспособности узла кластера.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-162">The cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="ee4f6-163">В представлении "Узлы" отображается физическая структура кластера.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-163">The node view shows the physical layout of the cluster.</span></span> <span data-ttu-id="ee4f6-164">Для каждого узла можно просмотреть, какие приложения были развернуты на этом узле</span><span class="sxs-lookup"><span data-stu-id="ee4f6-164">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-to-the-cluster-using-powershell"></a><span data-ttu-id="ee4f6-166">Подключение к кластеру с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee4f6-166">Connect to the cluster using PowerShell</span></span>
<span data-ttu-id="ee4f6-167">Убедитесь, что кластер работает, подключившись к нему с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-167">Verify that the cluster is running by connecting using PowerShell.</span></span>  <span data-ttu-id="ee4f6-168">Модуль PowerShell ServiceFabric установлен вместе с [пакетом SDK для Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ee4f6-168">The ServiceFabric PowerShell module is installed with the [Service Fabric SDK](service-fabric-get-started.md).</span></span>  <span data-ttu-id="ee4f6-169">Подключитесь к кластеру, используя командлет [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="ee4f6-169">The [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection to the cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
<span data-ttu-id="ee4f6-170">Примеры других способов подключения к кластеру см. в статье о [безопасном подключении к кластеру](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="ee4f6-170">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting to a cluster.</span></span> <span data-ttu-id="ee4f6-171">После подключения к кластеру используйте командлет [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps), чтобы отобразить список узлов в кластере и сведения о состоянии каждого узла.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-171">After connecting to the cluster, use the [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet to display a list of nodes in the cluster and status information for each node.</span></span> <span data-ttu-id="ee4f6-172">**Состояние работоспособности** каждого узла должно иметь значение *ОК*.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-172">**HealthState** should be *OK* for each node.</span></span>

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

### <a name="remove-the-cluster"></a><span data-ttu-id="ee4f6-173">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="ee4f6-173">Remove the cluster</span></span>
<span data-ttu-id="ee4f6-174">Кластер Service Fabric состоит из многих других ресурсов Azure помимо собственно ресурса кластера.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-174">A Service Fabric cluster is made up of other Azure resources in addition to the cluster resource itself.</span></span> <span data-ttu-id="ee4f6-175">Чтобы полностью удалить кластер Service Fabric, необходимо также удалить все ресурсы, из которых он состоит.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-175">So to completely delete a Service Fabric cluster you also need to delete all the resources it is made of.</span></span> <span data-ttu-id="ee4f6-176">Чтобы удалить кластер и все ресурсы, который он использует, проще всего удалить группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-176">The simplest way to delete the cluster and all the resources it consumes is to delete the resource group.</span></span> <span data-ttu-id="ee4f6-177">Чтобы узнать о других способах удаления кластера и некоторых (не всех) ресурсов в группе ресурсов, см. сведения об [удалении кластера](service-fabric-cluster-delete.md).</span><span class="sxs-lookup"><span data-stu-id="ee4f6-177">For other ways to delete a cluster or to delete some (but not all) the resources in a resource group, see [Delete a cluster](service-fabric-cluster-delete.md)</span></span>

<span data-ttu-id="ee4f6-178">Удаление группы ресурсов на портале Azure</span><span class="sxs-lookup"><span data-stu-id="ee4f6-178">Delete a resource group in the Azure portal:</span></span>
1. <span data-ttu-id="ee4f6-179">Перейдите к нужному кластеру Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-179">Navigate to the Service Fabric cluster you want to delete.</span></span>
2. <span data-ttu-id="ee4f6-180">Щелкните имя **группы ресурсов** на странице основных компонентов кластера.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-180">Click the **Resource Group** name on the cluster essentials page.</span></span>
3. <span data-ttu-id="ee4f6-181">На странице **основных компонентов группы ресурсов** щелкните **Удалить группу ресурсов** и выполните приведенные далее инструкции, чтобы завершить удаление группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-181">In the **Resource Group Essentials** page, click **Delete resource group** and follow the instructions on that page to complete the deletion of the resource group.</span></span>
    <span data-ttu-id="ee4f6-182">![Удаление группы ресурсов][cluster-delete]</span><span class="sxs-lookup"><span data-stu-id="ee4f6-182">![Delete the resource group][cluster-delete]</span></span>


## <a name="use-azure-powershell-to-deploy-a-secure-cluster"></a><span data-ttu-id="ee4f6-183">Развертывание защищенного кластера с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee4f6-183">Use Azure Powershell to deploy a secure cluster</span></span>
1. <span data-ttu-id="ee4f6-184">Скачайте [модуль Azure PowerShell 4.0 или более поздней версии](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) на компьютер.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-184">Download the [Azure Powershell module version 4.0 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) on your machine.</span></span>

2. <span data-ttu-id="ee4f6-185">Откройте окно Windows PowerShell и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ee4f6-185">Open a Windows PowerShell window, Run the following command.</span></span> 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    <span data-ttu-id="ee4f6-186">Должен отобразиться похожий результат:</span><span class="sxs-lookup"><span data-stu-id="ee4f6-186">You should see an output similar to the following.</span></span>

    ![Список PowerShell][ps-list]

3. <span data-ttu-id="ee4f6-188">Войдите в Azure и выберите подписку, в которой вы хотите создать кластер.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-188">Login to Azure and Select the subscription to which you want to create the cluster</span></span>

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. <span data-ttu-id="ee4f6-189">Чтобы создать защищенный кластер, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-189">Run the following command to now create a secure cluster.</span></span> <span data-ttu-id="ee4f6-190">Не забудьте настроить параметры.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-190">Do not forget to customize the parameters.</span></span> 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also the name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    <span data-ttu-id="ee4f6-191">Команда может выполняться 10–30 минут. Когда она выполнится, отобразятся похожие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ee4f6-191">The command can take anywhere from 10 minutes to 30 minutes to complete, at the end of it, you should get an output similar to the following.</span></span> <span data-ttu-id="ee4f6-192">Они содержат сведения о сертификате, хранилище ключей, в которое он передан, и локальной папке, в которую он скопирован.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-192">The output has information about the certificate, the KeyVault where it was uploaded to, and the local folder where the certificate is copied.</span></span> 

    ![Результат PowerShell][ps-out]

5. <span data-ttu-id="ee4f6-194">Скопируйте все выходные данные и сохраните их в текстовый файл, так как позднее вам понадобится сослаться на него.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-194">Copy the entire output and save to a text file as we need to refer to it.</span></span> <span data-ttu-id="ee4f6-195">Запишите следующие сведения из выходных данных.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-195">Make a note of the following information from the output.</span></span> 

    - <span data-ttu-id="ee4f6-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span><span class="sxs-lookup"><span data-stu-id="ee4f6-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span></span>
    - <span data-ttu-id="ee4f6-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span><span class="sxs-lookup"><span data-stu-id="ee4f6-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span></span>
    - <span data-ttu-id="ee4f6-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span><span class="sxs-lookup"><span data-stu-id="ee4f6-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span></span>
    - <span data-ttu-id="ee4f6-199">**ClientConnectionEndpointPort** : 19000</span><span class="sxs-lookup"><span data-stu-id="ee4f6-199">**ClientConnectionEndpointPort** : 19000</span></span>

### <a name="install-the-certificate-on-your-local-machine"></a><span data-ttu-id="ee4f6-200">Установка сертификата на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="ee4f6-200">Install the certificate on your local machine</span></span>
  
<span data-ttu-id="ee4f6-201">Чтобы подключиться к кластеру, необходимо установить сертификат в личное хранилище (Мое хранилище) текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-201">To connect to the cluster, you need to install the certificate into the Personal (My) store of the current user.</span></span> 

<span data-ttu-id="ee4f6-202">Выполните эту команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ee4f6-202">Run the following PowerShell</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\the name of the cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

<span data-ttu-id="ee4f6-203">Теперь все готово для подключения к защищенному кластеру.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-203">You are now ready to connect to your secure cluster.</span></span>

### <a name="connect-to-a-secure-cluster"></a><span data-ttu-id="ee4f6-204">Безопасное подключение к кластеру</span><span class="sxs-lookup"><span data-stu-id="ee4f6-204">Connect to a secure cluster</span></span> 

<span data-ttu-id="ee4f6-205">Для подключения к защищенному кластеру выполните следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ee4f6-205">Run the following PowerShell command to connect to a secure cluster.</span></span> <span data-ttu-id="ee4f6-206">Сведения о сертификате должны совпадать со сведениями сертификата, с помощью которого настраивался кластер.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-206">The certificate details must match a certificate that was used to set up the cluster.</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


<span data-ttu-id="ee4f6-207">В следующем примере показано, как настроить параметры:</span><span class="sxs-lookup"><span data-stu-id="ee4f6-207">The following example shows the completed parameters:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="ee4f6-208">Выполните следующую команду, чтобы проверить подключение к кластеру и убедиться, что кластер работает:</span><span class="sxs-lookup"><span data-stu-id="ee4f6-208">Run the following command to check that you are connected and the cluster is healthy.</span></span>

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-to-your-cluster-from-visual-studio"></a><span data-ttu-id="ee4f6-209">Публикация приложений из Visual Studio в кластер</span><span class="sxs-lookup"><span data-stu-id="ee4f6-209">Publish your apps to your cluster from Visual Studio</span></span>

<span data-ttu-id="ee4f6-210">После настройки кластера Azure можно опубликовать приложение из Visual Studio в Azure, следуя инструкциям из статьи о [публикации в кластер Azure](service-fabric-publish-app-remote-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="ee4f6-210">Now that you have set up an Azure cluster, you can publish your applications to it from Visual Studio by following the [Publish to an cluster](service-fabric-publish-app-remote-cluster.md) document.</span></span> 

### <a name="remove-the-cluster"></a><span data-ttu-id="ee4f6-211">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="ee4f6-211">Remove the cluster</span></span>
<span data-ttu-id="ee4f6-212">Помимо собственных ресурсов кластер содержит другие ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-212">A cluster is made up of other Azure resources in addition to the cluster resource itself.</span></span> <span data-ttu-id="ee4f6-213">Чтобы удалить кластер и все ресурсы, который он использует, проще всего удалить группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-213">The simplest way to delete the cluster and all the resources it consumes is to delete the resource group.</span></span> 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a><span data-ttu-id="ee4f6-214">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ee4f6-214">Next steps</span></span>
<span data-ttu-id="ee4f6-215">Теперь, когда вы настроили кластер разработки, перейдите к следующим шагам.</span><span class="sxs-lookup"><span data-stu-id="ee4f6-215">Now that you have set up a development cluster, try the following:</span></span>
* <span data-ttu-id="ee4f6-216">[Create a secure cluster in the portal](service-fabric-cluster-creation-via-portal.md) (Создание безопасного кластера на портале)</span><span class="sxs-lookup"><span data-stu-id="ee4f6-216">[Create a secure cluster in the portal](service-fabric-cluster-creation-via-portal.md)</span></span>
* <span data-ttu-id="ee4f6-217">[Create a cluster from a template](service-fabric-cluster-creation-via-arm.md) (Создание кластера из шаблона)</span><span class="sxs-lookup"><span data-stu-id="ee4f6-217">[Create a cluster from a template](service-fabric-cluster-creation-via-arm.md)</span></span> 
* [<span data-ttu-id="ee4f6-218">Разверните приложения с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee4f6-218">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
