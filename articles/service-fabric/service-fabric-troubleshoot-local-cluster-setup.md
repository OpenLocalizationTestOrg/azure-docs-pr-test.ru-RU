---
title: "aaaTroubleshoot вашей локальной настройки кластера Service Fabric | Документы Microsoft"
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
ms.openlocfilehash: ce36f62a4bc69d2cd5b6c3df4abda6ca88fa84f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a><span data-ttu-id="3a497-103">Устранение неполадок в работе кластера локальной разработки</span><span class="sxs-lookup"><span data-stu-id="3a497-103">Troubleshoot your local development cluster setup</span></span>
<span data-ttu-id="3a497-104">Если возникли проблемы при взаимодействии с локального кластера разработки Azure Service Fabric просмотрите hello из следующих способов для возможных решений.</span><span class="sxs-lookup"><span data-stu-id="3a497-104">If you run into an issue while interacting with your local Azure Service Fabric development cluster, review hello following suggestions for potential solutions.</span></span>

## <a name="cluster-setup-failures"></a><span data-ttu-id="3a497-105">Ошибки настройки кластера</span><span class="sxs-lookup"><span data-stu-id="3a497-105">Cluster setup failures</span></span>
### <a name="cannot-clean-up-service-fabric-logs"></a><span data-ttu-id="3a497-106">Не удается очистить журналы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3a497-106">Cannot clean up Service Fabric logs</span></span>
#### <a name="problem"></a><span data-ttu-id="3a497-107">Проблема</span><span class="sxs-lookup"><span data-stu-id="3a497-107">Problem</span></span>
<span data-ttu-id="3a497-108">При выполнении скрипта DevClusterSetup hello, появится сообщение об ошибке, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3a497-108">While running hello DevClusterSetup script, you see an error like this:</span></span>

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held tooitems in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a><span data-ttu-id="3a497-109">Решение</span><span class="sxs-lookup"><span data-stu-id="3a497-109">Solution</span></span>
<span data-ttu-id="3a497-110">Закройте hello текущее окно PowerShell и откройте окно PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="3a497-110">Close hello current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="3a497-111">Теперь должен быть доступ toosuccessfully, запустите скрипт hello.</span><span class="sxs-lookup"><span data-stu-id="3a497-111">You should now be able toosuccessfully run hello script.</span></span>

## <a name="cluster-connection-failures"></a><span data-ttu-id="3a497-112">Ошибки подключения к кластеру</span><span class="sxs-lookup"><span data-stu-id="3a497-112">Cluster connection failures</span></span>
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a><span data-ttu-id="3a497-113">Командлеты Service Fabric PowerShell не распознаются в Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a497-113">Service Fabric PowerShell cmdlets are not recognized in Azure PowerShell</span></span>
#### <a name="problem"></a><span data-ttu-id="3a497-114">Проблема</span><span class="sxs-lookup"><span data-stu-id="3a497-114">Problem</span></span>
<span data-ttu-id="3a497-115">Если вы выполните toorun hello командлеты PowerShell для службы структуры, таких как `Connect-ServiceFabricCluster` в окне Azure PowerShell, происходит сбой, о том, командлет hello не распознан.</span><span class="sxs-lookup"><span data-stu-id="3a497-115">If you try toorun any of hello Service Fabric PowerShell cmdlets, such as `Connect-ServiceFabricCluster` in an Azure PowerShell window, it fails, saying that hello cmdlet is not recognized.</span></span> <span data-ttu-id="3a497-116">Hello причина в том, что Azure PowerShell используется hello 32-разрядной версии оболочки Windows PowerShell (даже на 64-разрядной версии ОС), в то время как hello Service Fabric командлеты работают только в 64-разрядных сред.</span><span class="sxs-lookup"><span data-stu-id="3a497-116">hello reason for this is that Azure PowerShell uses hello 32-bit version of Windows PowerShell (even on 64-bit OS versions), whereas hello Service Fabric cmdlets only work in 64-bit environments.</span></span>

#### <a name="solution"></a><span data-ttu-id="3a497-117">Решение</span><span class="sxs-lookup"><span data-stu-id="3a497-117">Solution</span></span>
<span data-ttu-id="3a497-118">Всегда запускайте командлеты Service Fabric непосредственно из Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3a497-118">Always run Service Fabric cmdlets directly from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="3a497-119">Hello последнюю версию Azure PowerShell не создает специальные ярлык, поэтому это больше не возникает.</span><span class="sxs-lookup"><span data-stu-id="3a497-119">hello latest version of Azure PowerShell does not create a special shortcut, so this should no longer occur.</span></span>
> 
> 

### <a name="type-initialization-exception"></a><span data-ttu-id="3a497-120">Исключение типа инициализации</span><span class="sxs-lookup"><span data-stu-id="3a497-120">Type Initialization exception</span></span>
#### <a name="problem"></a><span data-ttu-id="3a497-121">Проблема</span><span class="sxs-lookup"><span data-stu-id="3a497-121">Problem</span></span>
<span data-ttu-id="3a497-122">При подключении toohello кластера в PowerShell, вы увидите hello ошибка TypeInitializationException System.Fabric.Common.AppTrace.</span><span class="sxs-lookup"><span data-stu-id="3a497-122">When you are connecting toohello cluster in PowerShell, you see hello error TypeInitializationException for System.Fabric.Common.AppTrace.</span></span>

#### <a name="solution"></a><span data-ttu-id="3a497-123">Решение</span><span class="sxs-lookup"><span data-stu-id="3a497-123">Solution</span></span>
<span data-ttu-id="3a497-124">При установке была неправильно настроена переменная пути.</span><span class="sxs-lookup"><span data-stu-id="3a497-124">Your path variable was not correctly set during installation.</span></span> <span data-ttu-id="3a497-125">Выйдите из Windows и снова выполните вход.</span><span class="sxs-lookup"><span data-stu-id="3a497-125">Sign out of Windows and sign back in.</span></span> <span data-ttu-id="3a497-126">Путь обновится.</span><span class="sxs-lookup"><span data-stu-id="3a497-126">This refreshes your path.</span></span>

### <a name="cluster-connection-fails-with-object-is-closed"></a><span data-ttu-id="3a497-127">Сбой подключения к кластеру с сообщением об ошибке "Объект закрыт"</span><span class="sxs-lookup"><span data-stu-id="3a497-127">Cluster connection fails with "Object is closed"</span></span>
#### <a name="problem"></a><span data-ttu-id="3a497-128">Проблема</span><span class="sxs-lookup"><span data-stu-id="3a497-128">Problem</span></span>
<span data-ttu-id="3a497-129">Вызов tooConnect-ServiceFabricCluster завершается с ошибкой следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3a497-129">A call tooConnect-ServiceFabricCluster fails with an error like this:</span></span>

    Connect-ServiceFabricCluster : hello object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a><span data-ttu-id="3a497-130">Решение</span><span class="sxs-lookup"><span data-stu-id="3a497-130">Solution</span></span>
<span data-ttu-id="3a497-131">Закройте hello текущее окно PowerShell и откройте окно PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="3a497-131">Close hello current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="3a497-132">Теперь можно подключиться toosuccessfully.</span><span class="sxs-lookup"><span data-stu-id="3a497-132">You should now be able toosuccessfully connect.</span></span>

### <a name="fabric-connection-denied-exception"></a><span data-ttu-id="3a497-133">Исключение Fabric Connection Denied</span><span class="sxs-lookup"><span data-stu-id="3a497-133">Fabric Connection Denied exception</span></span>
#### <a name="problem"></a><span data-ttu-id="3a497-134">Проблема</span><span class="sxs-lookup"><span data-stu-id="3a497-134">Problem</span></span>
<span data-ttu-id="3a497-135">При отладке в Visual Studio отображается ошибка FabricConnectionDeniedException.</span><span class="sxs-lookup"><span data-stu-id="3a497-135">When debugging from Visual Studio, you get a FabricConnectionDeniedException error.</span></span>

#### <a name="solution"></a><span data-ttu-id="3a497-136">Решение</span><span class="sxs-lookup"><span data-stu-id="3a497-136">Solution</span></span>
<span data-ttu-id="3a497-137">Эта ошибка обычно возникает при попытке toostart хост-процесса службы вручную, а не указывайте toostart среда выполнения Service Fabric hello его автоматически.</span><span class="sxs-lookup"><span data-stu-id="3a497-137">This error usually occurs when you try toostart a service host process manually, rather than allowing hello Service Fabric runtime toostart it for you.</span></span>

<span data-ttu-id="3a497-138">Убедитесь, что в решении нет проектов служб, настроенных в качестве запускаемых проектов.</span><span class="sxs-lookup"><span data-stu-id="3a497-138">Ensure that you do not have any service projects set as startup projects in your solution.</span></span> <span data-ttu-id="3a497-139">В качестве запускаемых проектов можно настраивать только проекты приложений Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3a497-139">Only Service Fabric application projects should be set as startup projects.</span></span>

> [!TIP]
> <span data-ttu-id="3a497-140">Если после завершения программы установки, локального кластера начинает toobehave аварийно, его можно сбросить с помощью приложения для области hello локального кластера диспетчера уведомлений.</span><span class="sxs-lookup"><span data-stu-id="3a497-140">If, following setup, your local cluster begins toobehave abnormally, you can reset it using hello local cluster manager system tray application.</span></span> <span data-ttu-id="3a497-141">Это удаляет hello существующего кластера и настройте новый.</span><span class="sxs-lookup"><span data-stu-id="3a497-141">This removes hello existing cluster and set up a new one.</span></span> <span data-ttu-id="3a497-142">Учтите, что все развернутые приложения и связанные данные будут удалены.</span><span class="sxs-lookup"><span data-stu-id="3a497-142">Note that all deployed applications and associated data is removed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="3a497-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3a497-143">Next steps</span></span>
* [<span data-ttu-id="3a497-144">Обзор и диагностика кластера с помощью системных отчетов о работоспособности</span><span class="sxs-lookup"><span data-stu-id="3a497-144">Understand and troubleshoot your cluster with system health reports</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="3a497-145">Визуализация кластера с помощью обозревателя Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3a497-145">Visualize your cluster with Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

