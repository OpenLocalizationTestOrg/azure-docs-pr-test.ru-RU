---
title: "Настройка обновления приложения Service Fabric | Документация Майкрософт"
description: "Узнайте, как настроить параметры обновления приложения Service Fabric с помощью Microsoft Visual Studio."
services: service-fabric
documentationcenter: na
author: mikkelhegn
manager: mfussell
editor: tglee
ms.assetid: 1757ba85-0b7b-4f16-8a23-2ddaa61c86c6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/29/2017
ms.author: mikkelhegn
ms.openlocfilehash: 314b29a56e4651222822f40a116af97a7372ff2c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-upgrade-of-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="9aa22-103">Настройка обновления приложения Service Fabric в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9aa22-103">Configure the upgrade of a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="9aa22-104">Средства Visual Studio для Azure Service Fabric обеспечивают поддержку обновления для публикации на локальных и удаленных кластерах.</span><span class="sxs-lookup"><span data-stu-id="9aa22-104">Visual Studio tools for Azure Service Fabric provide upgrade support for publishing to local or remote clusters.</span></span> <span data-ttu-id="9aa22-105">Существуют три сценария, в которых следует обновить приложение до более новой версии, а не заменить его, во время тестирования и отладки:</span><span class="sxs-lookup"><span data-stu-id="9aa22-105">There are three scenarios in which you want to upgrade your application to a newer version instead of replacing the application during testing and debugging:</span></span>

* <span data-ttu-id="9aa22-106">данные приложения не будут потеряны во время обновления;</span><span class="sxs-lookup"><span data-stu-id="9aa22-106">Application data won't be lost during the upgrade.</span></span>
* <span data-ttu-id="9aa22-107">достигается высокий уровень доступности, так как не будет перерывов в доступности службы по время обновления, если по доменам обновления распределено достаточное количество экземпляров службы.</span><span class="sxs-lookup"><span data-stu-id="9aa22-107">Availability remains high so there won't be any service interruption during the upgrade, if there are enough service instances spread across upgrade domains.</span></span>
* <span data-ttu-id="9aa22-108">Тесты для приложения могут запускаться во время его обновления.</span><span class="sxs-lookup"><span data-stu-id="9aa22-108">Tests can be run against an application while it's being upgraded.</span></span>

## <a name="parameters-needed-to-upgrade"></a><span data-ttu-id="9aa22-109">Параметры, необходимые для обновления</span><span class="sxs-lookup"><span data-stu-id="9aa22-109">Parameters needed to upgrade</span></span>
<span data-ttu-id="9aa22-110">Существует два типа развертывания: обычное или обновление.</span><span class="sxs-lookup"><span data-stu-id="9aa22-110">You can choose from two types of deployment: regular or upgrade.</span></span> <span data-ttu-id="9aa22-111">При обычном развертывании стираются все предыдущие сведения о развертывании и данные в кластере, а при обновлении они сохраняются.</span><span class="sxs-lookup"><span data-stu-id="9aa22-111">A regular deployment erases any previous deployment information and data on the cluster, while an upgrade deployment preserves it.</span></span> <span data-ttu-id="9aa22-112">При обновлении приложения Service Fabric в Visual Studio необходимо указать параметры обновления приложения и политики проверки работоспособности.</span><span class="sxs-lookup"><span data-stu-id="9aa22-112">When you upgrade a Service Fabric application in Visual Studio, you need to provide application upgrade parameters and health check policies.</span></span> <span data-ttu-id="9aa22-113">Параметры обновления приложения помогают управлять обновлением, а политики проверки работоспособности определяют, было обновление успешным или нет.</span><span class="sxs-lookup"><span data-stu-id="9aa22-113">Application upgrade parameters help control the upgrade, while health check policies determine whether the upgrade was successful.</span></span> <span data-ttu-id="9aa22-114">Дополнительные сведения см. в статье [Параметры обновления приложений](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="9aa22-114">See [Service Fabric application upgrade: upgrade parameters](service-fabric-application-upgrade-parameters.md) for more details.</span></span>

<span data-ttu-id="9aa22-115">Существует три режима обновления: *отслеживаемое*, *неотслеживаемое автоматическое* и *неотслеживаемое ручное*.</span><span class="sxs-lookup"><span data-stu-id="9aa22-115">There are three upgrade modes: *Monitored*, *UnmonitoredAuto*, and *UnmonitoredManual*.</span></span>

* <span data-ttu-id="9aa22-116">При отслеживаемом обновлении процесс обновления и проверка работоспособности приложения автоматизируются.</span><span class="sxs-lookup"><span data-stu-id="9aa22-116">A Monitored upgrade automates the upgrade and application health check.</span></span>
* <span data-ttu-id="9aa22-117">При неотслеживаемом автоматическом обновлении процесс обновления автоматизируется, но проверка работоспособности приложения пропускается.</span><span class="sxs-lookup"><span data-stu-id="9aa22-117">An UnmonitoredAuto upgrade automates the upgrade, but skips the application health check.</span></span>
* <span data-ttu-id="9aa22-118">При выполнении неотслеживаемого ручного обновления необходимо вручную обновить каждый домен обновления.</span><span class="sxs-lookup"><span data-stu-id="9aa22-118">When you do an UnmonitoredManual upgrade, you need to manually upgrade each upgrade domain.</span></span>

<span data-ttu-id="9aa22-119">Для каждого режима обновления необходим различный набор параметров.</span><span class="sxs-lookup"><span data-stu-id="9aa22-119">Each upgrade mode requires different sets of parameters.</span></span> <span data-ttu-id="9aa22-120">Дополнительные сведения о доступных параметрах обновления см. в статье [Параметры обновления приложений](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="9aa22-120">See [Application upgrade parameters](service-fabric-application-upgrade-parameters.md) to learn more about the available upgrade options.</span></span>

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="9aa22-121">Обновление приложения Service Fabric в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9aa22-121">Upgrade a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="9aa22-122">При использовании средств Service Fabric Visual Studio для обновления приложения Service Fabric можно указать, что процесс публикации будет подразумевать обновление, а не обычное развертывание, установив флажок **Обновить приложение** .</span><span class="sxs-lookup"><span data-stu-id="9aa22-122">If you’re using the Visual Studio Service Fabric tools to upgrade a Service Fabric application, you can specify a publish process to be an upgrade rather than a regular deployment by checking the **Upgrade the application** check box.</span></span>

### <a name="to-configure-the-upgrade-parameters"></a><span data-ttu-id="9aa22-123">Настройка параметров обновления</span><span class="sxs-lookup"><span data-stu-id="9aa22-123">To configure the upgrade parameters</span></span>
1. <span data-ttu-id="9aa22-124">Нажмите кнопку **Параметры** рядом с флажком.</span><span class="sxs-lookup"><span data-stu-id="9aa22-124">Click the **Settings** button next to the check box.</span></span> <span data-ttu-id="9aa22-125">Откроется диалоговое окно **Изменение параметров обновления** .</span><span class="sxs-lookup"><span data-stu-id="9aa22-125">The **Edit Upgrade Parameters** dialog box appears.</span></span> <span data-ttu-id="9aa22-126">Диалоговое окно **Изменение параметров обновления** поддерживает отслеживаемое, неотслеживаемое автоматическое и ручное обновления.</span><span class="sxs-lookup"><span data-stu-id="9aa22-126">The **Edit Upgrade Parameters** dialog box supports the Monitored, UnmonitoredAuto, and UnmonitoredManual upgrade modes.</span></span>
2. <span data-ttu-id="9aa22-127">Выберите режим обновления, который хотите использовать, и заполните сетку параметров.</span><span class="sxs-lookup"><span data-stu-id="9aa22-127">Select the upgrade mode that you want to use and then fill out the parameter grid.</span></span>

    <span data-ttu-id="9aa22-128">Каждый параметр имеет значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9aa22-128">Each parameter has default values.</span></span> <span data-ttu-id="9aa22-129">Необязательный параметр *DefaultServiceTypeHealthPolicy* принимает входную хэш-таблицу.</span><span class="sxs-lookup"><span data-stu-id="9aa22-129">The optional parameter *DefaultServiceTypeHealthPolicy* takes a hash table input.</span></span> <span data-ttu-id="9aa22-130">Ниже приведен пример формата входной хэш-таблицы для *DefaultServiceTypeHealthPolicy*:</span><span class="sxs-lookup"><span data-stu-id="9aa22-130">Here’s an example of the hash table input format for *DefaultServiceTypeHealthPolicy*:</span></span>

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    <span data-ttu-id="9aa22-131">*ServiceTypeHealthPolicyMap* — еще один необязательный параметр, который принимает входную хэш-таблицу в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="9aa22-131">*ServiceTypeHealthPolicyMap* is another optional parameter that takes a hash table input in the following format:</span></span>

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    <span data-ttu-id="9aa22-132">Ниже приведен пример из реальной жизни:</span><span class="sxs-lookup"><span data-stu-id="9aa22-132">Here's a real-life example:</span></span>

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. <span data-ttu-id="9aa22-133">При выборе неотслеживаемого автоматического обновления необходимо будет вручную запустить консоль PowerShell для продолжения и завершения процесса обновления.</span><span class="sxs-lookup"><span data-stu-id="9aa22-133">If you select UnmonitoredManual upgrade mode, you must manually start a PowerShell console to continue and finish the upgrade process.</span></span> <span data-ttu-id="9aa22-134">Чтобы узнать, как работает ручное обновление, обратитесь к разделу [Обновление приложения Service Fabric: дополнительные разделы](service-fabric-application-upgrade-advanced.md) .</span><span class="sxs-lookup"><span data-stu-id="9aa22-134">Refer to [Service Fabric application upgrade: advanced topics](service-fabric-application-upgrade-advanced.md) to learn how manual upgrade works.</span></span>

## <a name="upgrade-an-application-by-using-powershell"></a><span data-ttu-id="9aa22-135">Обновление приложения с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="9aa22-135">Upgrade an application by using PowerShell</span></span>
<span data-ttu-id="9aa22-136">Обновить приложение Service Fabric можно с помощью командлетов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9aa22-136">You can use PowerShell cmdlets to upgrade a Service Fabric application.</span></span> <span data-ttu-id="9aa22-137">Подробные сведения см. в [руководстве по обновлению приложений Service Fabric](service-fabric-application-upgrade-tutorial.md) и статье, посвященной командлету [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx).</span><span class="sxs-lookup"><span data-stu-id="9aa22-137">See [Service Fabric application upgrade tutorial](service-fabric-application-upgrade-tutorial.md) and [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) for detailed information.</span></span>

## <a name="specify-a-health-check-policy-in-the-application-manifest-file"></a><span data-ttu-id="9aa22-138">Задание политики проверки работоспособности в файле манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="9aa22-138">Specify a health check policy in the application manifest file</span></span>
<span data-ttu-id="9aa22-139">Каждая служба в приложении Service Fabric может иметь собственные параметры политики работоспособности, которые переопределяют значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9aa22-139">Every service in a Service Fabric application can have its own health policy parameters that override the default values.</span></span> <span data-ttu-id="9aa22-140">Эти значения параметров можно указать в файле манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="9aa22-140">You can provide these parameter values in the application manifest file.</span></span>

<span data-ttu-id="9aa22-141">В следующем примере показано, как применить уникальную политику проверки работоспособности для каждой службы в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="9aa22-141">The following example shows how to apply a unique health check policy for each service in the application manifest.</span></span>

```xml
<Policies>
    <HealthPolicy ConsiderWarningAsError="false" MaxPercentUnhealthyDeployedApplications="20">
        <DefaultServiceTypeHealthPolicy MaxPercentUnhealthyServices="20"               
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />
        <ServiceTypeHealthPolicy ServiceTypeName="ServiceTypeName1"
                MaxPercentUnhealthyServices="20"
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />      
    </HealthPolicy>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="9aa22-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9aa22-142">Next steps</span></span>
<span data-ttu-id="9aa22-143">Дополнительные сведения о развертывании приложений см. в статье [Развертывание гостевого исполняемого файла в Service Fabric](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="9aa22-143">For more information about deploying an application, see [Deploy an existing application in Azure Service Fabric](service-fabric-deploy-existing-app.md).</span></span>