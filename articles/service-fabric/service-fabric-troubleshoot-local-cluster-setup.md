---
title: "Устранение неполадок в настройке локального кластера Service Fabric | Документация Майкрософт"
description: "В этой статье описываются рекомендации по устранению неполадок с кластером локальной разработки."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 97f4feaa-bba0-47af-8fdd-07f811fe2202
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: aa393f884b564cee81fcf75cc2eff895efea9471
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a><span data-ttu-id="c51a9-103">Устранение неполадок в работе кластера локальной разработки</span><span class="sxs-lookup"><span data-stu-id="c51a9-103">Troubleshoot your local development cluster setup</span></span>
<span data-ttu-id="c51a9-104">Если у вас возникли проблемы при взаимодействии с кластером локальной разработки Azure Service Fabric, ознакомьтесь со следующими возможностями для решения.</span><span class="sxs-lookup"><span data-stu-id="c51a9-104">If you run into an issue while interacting with your local Azure Service Fabric development cluster, review the following suggestions for potential solutions.</span></span>

## <a name="cluster-setup-failures"></a><span data-ttu-id="c51a9-105">Ошибки настройки кластера</span><span class="sxs-lookup"><span data-stu-id="c51a9-105">Cluster setup failures</span></span>
### <a name="cannot-clean-up-service-fabric-logs"></a><span data-ttu-id="c51a9-106">Не удается очистить журналы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c51a9-106">Cannot clean up Service Fabric logs</span></span>
#### <a name="problem"></a><span data-ttu-id="c51a9-107">Проблема</span><span class="sxs-lookup"><span data-stu-id="c51a9-107">Problem</span></span>
<span data-ttu-id="c51a9-108">При выполнении сценария DevClusterSetup появляется следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="c51a9-108">While running the DevClusterSetup script, you see an error like this:</span></span>

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held to items in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a><span data-ttu-id="c51a9-109">Решение</span><span class="sxs-lookup"><span data-stu-id="c51a9-109">Solution</span></span>
<span data-ttu-id="c51a9-110">Закройте текущее и откройте новое окно PowerShell от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="c51a9-110">Close the current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="c51a9-111">Теперь можно успешно запустить сценарий.</span><span class="sxs-lookup"><span data-stu-id="c51a9-111">You should now be able to successfully run the script.</span></span>

## <a name="cluster-connection-failures"></a><span data-ttu-id="c51a9-112">Ошибки подключения к кластеру</span><span class="sxs-lookup"><span data-stu-id="c51a9-112">Cluster connection failures</span></span>
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a><span data-ttu-id="c51a9-113">Командлеты Service Fabric PowerShell не распознаются в Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c51a9-113">Service Fabric PowerShell cmdlets are not recognized in Azure PowerShell</span></span>
#### <a name="problem"></a><span data-ttu-id="c51a9-114">Проблема</span><span class="sxs-lookup"><span data-stu-id="c51a9-114">Problem</span></span>
<span data-ttu-id="c51a9-115">Попытка запустить командлеты Service Fabric PowerShell, например `Connect-ServiceFabricCluster` в окне Azure PowerShell, не удается, с сообщением о том, что командлет не распознан.</span><span class="sxs-lookup"><span data-stu-id="c51a9-115">If you try to run any of the Service Fabric PowerShell cmdlets, such as `Connect-ServiceFabricCluster` in an Azure PowerShell window, it fails, saying that the cmdlet is not recognized.</span></span> <span data-ttu-id="c51a9-116">Причина в том, что Azure PowerShell использует 32-разрядную версию Windows PowerShell (даже на 64-разрядной версии ОС), а командлеты Service Fabric работают только в 64-разрядной среде.</span><span class="sxs-lookup"><span data-stu-id="c51a9-116">The reason for this is that Azure PowerShell uses the 32-bit version of Windows PowerShell (even on 64-bit OS versions), whereas the Service Fabric cmdlets only work in 64-bit environments.</span></span>

#### <a name="solution"></a><span data-ttu-id="c51a9-117">Решение</span><span class="sxs-lookup"><span data-stu-id="c51a9-117">Solution</span></span>
<span data-ttu-id="c51a9-118">Всегда запускайте командлеты Service Fabric непосредственно из Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c51a9-118">Always run Service Fabric cmdlets directly from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="c51a9-119">Последняя версия Azure PowerShell не создает специальный ярлык, поэтому так больше не должно происходить.</span><span class="sxs-lookup"><span data-stu-id="c51a9-119">The latest version of Azure PowerShell does not create a special shortcut, so this should no longer occur.</span></span>
> 
> 

### <a name="type-initialization-exception"></a><span data-ttu-id="c51a9-120">Исключение типа инициализации</span><span class="sxs-lookup"><span data-stu-id="c51a9-120">Type Initialization exception</span></span>
#### <a name="problem"></a><span data-ttu-id="c51a9-121">Проблема</span><span class="sxs-lookup"><span data-stu-id="c51a9-121">Problem</span></span>
<span data-ttu-id="c51a9-122">При подключении к кластеру в PowerShell отображается ошибка TypeInitializationException для System.Fabric.Common.AppTrace.</span><span class="sxs-lookup"><span data-stu-id="c51a9-122">When you are connecting to the cluster in PowerShell, you see the error TypeInitializationException for System.Fabric.Common.AppTrace.</span></span>

#### <a name="solution"></a><span data-ttu-id="c51a9-123">Решение</span><span class="sxs-lookup"><span data-stu-id="c51a9-123">Solution</span></span>
<span data-ttu-id="c51a9-124">При установке была неправильно настроена переменная пути.</span><span class="sxs-lookup"><span data-stu-id="c51a9-124">Your path variable was not correctly set during installation.</span></span> <span data-ttu-id="c51a9-125">Выйдите из Windows и снова выполните вход.</span><span class="sxs-lookup"><span data-stu-id="c51a9-125">Sign out of Windows and sign back in.</span></span> <span data-ttu-id="c51a9-126">Путь обновится.</span><span class="sxs-lookup"><span data-stu-id="c51a9-126">This refreshes your path.</span></span>

### <a name="cluster-connection-fails-with-object-is-closed"></a><span data-ttu-id="c51a9-127">Сбой подключения к кластеру с сообщением об ошибке "Объект закрыт"</span><span class="sxs-lookup"><span data-stu-id="c51a9-127">Cluster connection fails with "Object is closed"</span></span>
#### <a name="problem"></a><span data-ttu-id="c51a9-128">Проблема</span><span class="sxs-lookup"><span data-stu-id="c51a9-128">Problem</span></span>
<span data-ttu-id="c51a9-129">Вызов Connect-ServiceFabricCluster завершается со следующей ошибкой:</span><span class="sxs-lookup"><span data-stu-id="c51a9-129">A call to Connect-ServiceFabricCluster fails with an error like this:</span></span>

    Connect-ServiceFabricCluster : The object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a><span data-ttu-id="c51a9-130">Решение</span><span class="sxs-lookup"><span data-stu-id="c51a9-130">Solution</span></span>
<span data-ttu-id="c51a9-131">Закройте текущее и откройте новое окно PowerShell от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="c51a9-131">Close the current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="c51a9-132">Теперь можно успешно подключиться.</span><span class="sxs-lookup"><span data-stu-id="c51a9-132">You should now be able to successfully connect.</span></span>

### <a name="fabric-connection-denied-exception"></a><span data-ttu-id="c51a9-133">Исключение Fabric Connection Denied</span><span class="sxs-lookup"><span data-stu-id="c51a9-133">Fabric Connection Denied exception</span></span>
#### <a name="problem"></a><span data-ttu-id="c51a9-134">Проблема</span><span class="sxs-lookup"><span data-stu-id="c51a9-134">Problem</span></span>
<span data-ttu-id="c51a9-135">При отладке в Visual Studio отображается ошибка FabricConnectionDeniedException.</span><span class="sxs-lookup"><span data-stu-id="c51a9-135">When debugging from Visual Studio, you get a FabricConnectionDeniedException error.</span></span>

#### <a name="solution"></a><span data-ttu-id="c51a9-136">Решение</span><span class="sxs-lookup"><span data-stu-id="c51a9-136">Solution</span></span>
<span data-ttu-id="c51a9-137">Эта ошибка обычно возникает, если вы пытаетесь запустить процесс узла службы вручную, а не указываете среде выполнения Service Fabric запустить его автоматически.</span><span class="sxs-lookup"><span data-stu-id="c51a9-137">This error usually occurs when you try to start a service host process manually, rather than allowing the Service Fabric runtime to start it for you.</span></span>

<span data-ttu-id="c51a9-138">Убедитесь, что в решении нет проектов служб, настроенных в качестве запускаемых проектов.</span><span class="sxs-lookup"><span data-stu-id="c51a9-138">Ensure that you do not have any service projects set as startup projects in your solution.</span></span> <span data-ttu-id="c51a9-139">В качестве запускаемых проектов можно настраивать только проекты приложений Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c51a9-139">Only Service Fabric application projects should be set as startup projects.</span></span>

> [!TIP]
> <span data-ttu-id="c51a9-140">Если после завершения программы установки у локального кластера наблюдается нетипичное поведение, такой кластер можно сбросить с помощью приложения панели задач диспетчера локального кластера.</span><span class="sxs-lookup"><span data-stu-id="c51a9-140">If, following setup, your local cluster begins to behave abnormally, you can reset it using the local cluster manager system tray application.</span></span> <span data-ttu-id="c51a9-141">Будет удален существующий кластер и настроен новый.</span><span class="sxs-lookup"><span data-stu-id="c51a9-141">This removes the existing cluster and set up a new one.</span></span> <span data-ttu-id="c51a9-142">Учтите, что все развернутые приложения и связанные данные будут удалены.</span><span class="sxs-lookup"><span data-stu-id="c51a9-142">Note that all deployed applications and associated data is removed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c51a9-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c51a9-143">Next steps</span></span>
* [<span data-ttu-id="c51a9-144">Обзор и диагностика кластера с помощью системных отчетов о работоспособности</span><span class="sxs-lookup"><span data-stu-id="c51a9-144">Understand and troubleshoot your cluster with system health reports</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="c51a9-145">Визуализация кластера с помощью обозревателя Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c51a9-145">Visualize your cluster with Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

