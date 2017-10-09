---
title: "aaaAzure Service Fabric различия между Windows и Linux | Документы Microsoft"
description: "Различия между hello структуры предварительной версии службы Azure для Linux и Azure Service Fabric на Windows."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 7a16a440dfc8d9006e274f46951be1562e6f10d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="differences-between-service-fabric-on-linux-preview-and-windows-generally-available"></a><span data-ttu-id="c61c1-103">Различия между Service Fabric для Linux (предварительная версия) и Windows (общедоступная версия)</span><span class="sxs-lookup"><span data-stu-id="c61c1-103">Differences between Service Fabric on Linux (preview) and Windows (generally available)</span></span>

<span data-ttu-id="c61c1-104">Так как платформа Service Fabric для Linux доступна в предварительной версии, некоторые ее функции поддерживаются в Windows, но не в Linux.</span><span class="sxs-lookup"><span data-stu-id="c61c1-104">Since Service Fabric on Linux is a preview, there are some features that are supported on Windows, but not yet on Linux.</span></span> <span data-ttu-id="c61c1-105">Со временем наборы функций hello будут с контролем четности, когда Service Fabric в Linux станет общедоступной.</span><span class="sxs-lookup"><span data-stu-id="c61c1-105">Eventually, hello feature sets will be at parity when Service Fabric on Linux becomes generally available.</span></span> <span data-ttu-id="c61c1-106">В последующих выпусках это различие между наборами функций будет минимизировано.</span><span class="sxs-lookup"><span data-stu-id="c61c1-106">With upcoming releases, this feature gap will shrink.</span></span> <span data-ttu-id="c61c1-107">Hello следующие существуют различия между hello последние доступные выпуски (то есть, между версии 5.6 в Windows и версии 5.5 в Linux):</span><span class="sxs-lookup"><span data-stu-id="c61c1-107">hello following differences exist between hello latest available releases (that is, between version 5.6 on Windows and version 5.5 on Linux):</span></span> 

* <span data-ttu-id="c61c1-108">надежные коллекции (и надежные службы с отслеживанием состояния);</span><span class="sxs-lookup"><span data-stu-id="c61c1-108">Reliable Collections (and Reliable Stateful Services)</span></span> 
* <span data-ttu-id="c61c1-109">обратный прокси-сервер;</span><span class="sxs-lookup"><span data-stu-id="c61c1-109">ReverseProxy</span></span> 
* <span data-ttu-id="c61c1-110">автономный установщик;</span><span class="sxs-lookup"><span data-stu-id="c61c1-110">Standalone installer</span></span> 
* <span data-ttu-id="c61c1-111">проверка схемы XML для файлов манифеста;</span><span class="sxs-lookup"><span data-stu-id="c61c1-111">XML schema validation for manifest files</span></span> 
* <span data-ttu-id="c61c1-112">перенаправление консоли;</span><span class="sxs-lookup"><span data-stu-id="c61c1-112">Console redirection</span></span> 
* <span data-ttu-id="c61c1-113">Hello ошибки Analysis Service (FAS)</span><span class="sxs-lookup"><span data-stu-id="c61c1-113">hello Fault Analysis Service (FAS)</span></span>
* <span data-ttu-id="c61c1-114">драйверы Docker Compose, а также драйверы томов и ведения журнала для контейнеров;</span><span class="sxs-lookup"><span data-stu-id="c61c1-114">Docker compose and volume and logging drivers for containers</span></span> 
* <span data-ttu-id="c61c1-115">управление ресурсами для контейнеров и служб;</span><span class="sxs-lookup"><span data-stu-id="c61c1-115">Resource governance for containers and services</span></span> 
* <span data-ttu-id="c61c1-116">Служба DNS</span><span class="sxs-lookup"><span data-stu-id="c61c1-116">DNS service</span></span>
* <span data-ttu-id="c61c1-117">поддержка Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="c61c1-117">Azure Active Directory support</span></span>
* <span data-ttu-id="c61c1-118">команды интерфейса командной строки, эквивалентные некоторым командам PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c61c1-118">CLI command equivalents of certain Powershell commands</span></span> 
* <span data-ttu-id="c61c1-119">Для кластеров Linux (как в развернутом в следующем разделе hello) можно запустить только часть команды Powershell.</span><span class="sxs-lookup"><span data-stu-id="c61c1-119">Only a subset of Powershell commands can be run against a Linux cluster (as expanded in hello next section).</span></span>

>[!NOTE]
><span data-ttu-id="c61c1-120">Перенаправление консоли не поддерживается в рабочих кластерах, даже в Windows.</span><span class="sxs-lookup"><span data-stu-id="c61c1-120">Console redirection is not supported in production clusters, even on Windows.</span></span>

<span data-ttu-id="c61c1-121">Средства разработки в Windows и Linux также отличаются.</span><span class="sxs-lookup"><span data-stu-id="c61c1-121">Development tooling is also different between Windows and Linux.</span></span> <span data-ttu-id="c61c1-122">В Windows используются Visual Studio, PowerShell, VSTS и трассировка событий Windows, а в Linux — Yeoman, Eclipse, Jenkins и LTTng.</span><span class="sxs-lookup"><span data-stu-id="c61c1-122">VisualStudio, Powershell, VSTS, and ETW are used on Windows while Yeoman, Eclipse, Jenkins, and LTTng are used on Linux.</span></span>

## <a name="powershell-cmdlets-that-do-not-work-against-a-linux-service-fabric-cluster"></a><span data-ttu-id="c61c1-123">Командлеты PowerShell, которые не работают в кластере Service Fabric для Linux</span><span class="sxs-lookup"><span data-stu-id="c61c1-123">Powershell cmdlets that do not work against a Linux Service Fabric cluster</span></span>

* <span data-ttu-id="c61c1-124">Invoke-ServiceFabricChaosTestScenario</span><span class="sxs-lookup"><span data-stu-id="c61c1-124">Invoke-ServiceFabricChaosTestScenario</span></span>
* <span data-ttu-id="c61c1-125">Invoke-ServiceFabricFailoverTestScenario</span><span class="sxs-lookup"><span data-stu-id="c61c1-125">Invoke-ServiceFabricFailoverTestScenario</span></span>
* <span data-ttu-id="c61c1-126">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="c61c1-126">Invoke-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="c61c1-127">Invoke-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="c61c1-127">Invoke-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="c61c1-128">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="c61c1-128">Restart-ServiceFabricPartition</span></span>
* <span data-ttu-id="c61c1-129">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="c61c1-129">Start-ServiceFabricNode</span></span>
* <span data-ttu-id="c61c1-130">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="c61c1-130">Stop-ServiceFabricNode</span></span>
* <span data-ttu-id="c61c1-131">Get-ServiceFabricImageStoreContent</span><span class="sxs-lookup"><span data-stu-id="c61c1-131">Get-ServiceFabricImageStoreContent</span></span>
* <span data-ttu-id="c61c1-132">Get-ServiceFabricChaosReport</span><span class="sxs-lookup"><span data-stu-id="c61c1-132">Get-ServiceFabricChaosReport</span></span>
* <span data-ttu-id="c61c1-133">Get-ServiceFabricNodeTransitionProgress</span><span class="sxs-lookup"><span data-stu-id="c61c1-133">Get-ServiceFabricNodeTransitionProgress</span></span>
* <span data-ttu-id="c61c1-134">Get-ServiceFabricPartitionDataLossProgress</span><span class="sxs-lookup"><span data-stu-id="c61c1-134">Get-ServiceFabricPartitionDataLossProgress</span></span>
* <span data-ttu-id="c61c1-135">Get-ServiceFabricPartitionQuorumLossProgress</span><span class="sxs-lookup"><span data-stu-id="c61c1-135">Get-ServiceFabricPartitionQuorumLossProgress</span></span>
* <span data-ttu-id="c61c1-136">Get-ServiceFabricPartitionRestartProgress</span><span class="sxs-lookup"><span data-stu-id="c61c1-136">Get-ServiceFabricPartitionRestartProgress</span></span>
* <span data-ttu-id="c61c1-137">Get-ServiceFabricTestCommandStatusList</span><span class="sxs-lookup"><span data-stu-id="c61c1-137">Get-ServiceFabricTestCommandStatusList</span></span>
* <span data-ttu-id="c61c1-138">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="c61c1-138">Remove-ServiceFabricTestState</span></span>
* <span data-ttu-id="c61c1-139">Start-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="c61c1-139">Start-ServiceFabricChaos</span></span>
* <span data-ttu-id="c61c1-140">Start-ServiceFabricNodeTransition</span><span class="sxs-lookup"><span data-stu-id="c61c1-140">Start-ServiceFabricNodeTransition</span></span>
* <span data-ttu-id="c61c1-141">Start-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="c61c1-141">Start-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="c61c1-142">Start-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="c61c1-142">Start-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="c61c1-143">Start-ServiceFabricPartitionRestart</span><span class="sxs-lookup"><span data-stu-id="c61c1-143">Start-ServiceFabricPartitionRestart</span></span>
* <span data-ttu-id="c61c1-144">Stop-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="c61c1-144">Stop-ServiceFabricChaos</span></span>
* <span data-ttu-id="c61c1-145">Stop-ServiceFabricTestCommand</span><span class="sxs-lookup"><span data-stu-id="c61c1-145">Stop-ServiceFabricTestCommand</span></span>
* <span data-ttu-id="c61c1-146">Cmd</span><span class="sxs-lookup"><span data-stu-id="c61c1-146">Cmd</span></span>
* <span data-ttu-id="c61c1-147">Get-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="c61c1-147">Get-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="c61c1-148">Get-ServiceFabricClusterConfiguration</span><span class="sxs-lookup"><span data-stu-id="c61c1-148">Get-ServiceFabricClusterConfiguration</span></span>
* <span data-ttu-id="c61c1-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span><span class="sxs-lookup"><span data-stu-id="c61c1-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span></span>
* <span data-ttu-id="c61c1-150">Get-ServiceFabricPackageDebugParameters</span><span class="sxs-lookup"><span data-stu-id="c61c1-150">Get-ServiceFabricPackageDebugParameters</span></span>
* <span data-ttu-id="c61c1-151">New-ServiceFabricPackageDebugParameter</span><span class="sxs-lookup"><span data-stu-id="c61c1-151">New-ServiceFabricPackageDebugParameter</span></span>
* <span data-ttu-id="c61c1-152">New-ServiceFabricPackageSharingPolicy</span><span class="sxs-lookup"><span data-stu-id="c61c1-152">New-ServiceFabricPackageSharingPolicy</span></span>
* <span data-ttu-id="c61c1-153">Add-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="c61c1-153">Add-ServiceFabricNode</span></span>
* <span data-ttu-id="c61c1-154">Copy-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="c61c1-154">Copy-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="c61c1-155">Get-ServiceFabricRuntimeSupportedVersion</span><span class="sxs-lookup"><span data-stu-id="c61c1-155">Get-ServiceFabricRuntimeSupportedVersion</span></span>
* <span data-ttu-id="c61c1-156">Get-ServiceFabricRuntimeUpgradeVersion</span><span class="sxs-lookup"><span data-stu-id="c61c1-156">Get-ServiceFabricRuntimeUpgradeVersion</span></span>
* <span data-ttu-id="c61c1-157">New-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="c61c1-157">New-ServiceFabricCluster</span></span>
* <span data-ttu-id="c61c1-158">New-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="c61c1-158">New-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="c61c1-159">Remove-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="c61c1-159">Remove-ServiceFabricCluster</span></span>
* <span data-ttu-id="c61c1-160">Remove-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="c61c1-160">Remove-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="c61c1-161">Remove-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="c61c1-161">Remove-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="c61c1-162">Test-ServiceFabricClusterManifest</span><span class="sxs-lookup"><span data-stu-id="c61c1-162">Test-ServiceFabricClusterManifest</span></span>
* <span data-ttu-id="c61c1-163">Test-ServiceFabricConfiguration</span><span class="sxs-lookup"><span data-stu-id="c61c1-163">Test-ServiceFabricConfiguration</span></span>
* <span data-ttu-id="c61c1-164">Update-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="c61c1-164">Update-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="c61c1-165">Approve-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="c61c1-165">Approve-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="c61c1-166">Complete-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="c61c1-166">Complete-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="c61c1-167">Get-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="c61c1-167">Get-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="c61c1-168">Invoke-ServiceFabricDecryptText</span><span class="sxs-lookup"><span data-stu-id="c61c1-168">Invoke-ServiceFabricDecryptText</span></span>
* <span data-ttu-id="c61c1-169">Invoke-ServiceFabricEncryptSecret</span><span class="sxs-lookup"><span data-stu-id="c61c1-169">Invoke-ServiceFabricEncryptSecret</span></span>
* <span data-ttu-id="c61c1-170">Invoke-ServiceFabricEncryptText</span><span class="sxs-lookup"><span data-stu-id="c61c1-170">Invoke-ServiceFabricEncryptText</span></span>
* <span data-ttu-id="c61c1-171">Invoke-ServiceFabricInfrastructureCommand</span><span class="sxs-lookup"><span data-stu-id="c61c1-171">Invoke-ServiceFabricInfrastructureCommand</span></span>
* <span data-ttu-id="c61c1-172">Invoke-ServiceFabricInfrastructureQuery</span><span class="sxs-lookup"><span data-stu-id="c61c1-172">Invoke-ServiceFabricInfrastructureQuery</span></span>
* <span data-ttu-id="c61c1-173">Remove-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="c61c1-173">Remove-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="c61c1-174">Start-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="c61c1-174">Start-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="c61c1-175">Stop-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="c61c1-175">Stop-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="c61c1-176">Update-ServiceFabricRepairTaskHealthPolicy</span><span class="sxs-lookup"><span data-stu-id="c61c1-176">Update-ServiceFabricRepairTaskHealthPolicy</span></span>



## <a name="next-steps"></a><span data-ttu-id="c61c1-177">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c61c1-177">Next steps</span></span>
* [<span data-ttu-id="c61c1-178">Подготовка среды разработки в Linux</span><span class="sxs-lookup"><span data-stu-id="c61c1-178">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="c61c1-179">Настройка среды разработки для Mac OS X</span><span class="sxs-lookup"><span data-stu-id="c61c1-179">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="c61c1-180">Создание первого приложения Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c61c1-180">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* <span data-ttu-id="c61c1-181">[Getting started with Eclipse Plugin for Service Fabric Java application development](service-fabric-get-started-eclipse.md) (Начало работы с подключаемым модулем Eclipse для разработки приложения Service Fabric на Java)</span><span class="sxs-lookup"><span data-stu-id="c61c1-181">[Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse](service-fabric-get-started-eclipse.md)</span></span>
* [<span data-ttu-id="c61c1-182">Создание первого приложения Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c61c1-182">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="c61c1-183">Использовать toomanage hello CLI структуры службы приложения</span><span class="sxs-lookup"><span data-stu-id="c61c1-183">Use hello Service Fabric CLI toomanage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
