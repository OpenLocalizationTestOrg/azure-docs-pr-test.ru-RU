---
title: "обновление приложения Service Fabric hello aaaConfigure | Документы Microsoft"
description: "Узнайте, как tooconfigure hello параметров обновления приложения Service Fabric с помощью Microsoft Visual Studio."
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
ms.openlocfilehash: 8ca50aa9d911f3c98f017490c8fe29011e8d80cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-upgrade-of-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="a0bc7-103">Настройка обновления hello приложения Service Fabric в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a0bc7-103">Configure hello upgrade of a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="a0bc7-104">Visual Studio tools для Azure Service Fabric поддерживает обновления публикации toolocal или удаленных кластеров.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-104">Visual Studio tools for Azure Service Fabric provide upgrade support for publishing toolocal or remote clusters.</span></span> <span data-ttu-id="a0bc7-105">Существует три сценария, в которых требуется tooupgrade более новой версии приложения tooa вместо замены приложения hello во время тестирования и отладки.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-105">There are three scenarios in which you want tooupgrade your application tooa newer version instead of replacing hello application during testing and debugging:</span></span>

* <span data-ttu-id="a0bc7-106">Данные приложения не были потеряны во время обновления hello.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-106">Application data won't be lost during hello upgrade.</span></span>
* <span data-ttu-id="a0bc7-107">Доступность остается высокого уровня, не будет нарушения работы службы во время обновления hello при наличии достаточного числа экземпляров службы распределены по нескольким доменам обновления.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-107">Availability remains high so there won't be any service interruption during hello upgrade, if there are enough service instances spread across upgrade domains.</span></span>
* <span data-ttu-id="a0bc7-108">Тесты для приложения могут запускаться во время его обновления.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-108">Tests can be run against an application while it's being upgraded.</span></span>

## <a name="parameters-needed-tooupgrade"></a><span data-ttu-id="a0bc7-109">Параметры требуются tooupgrade</span><span class="sxs-lookup"><span data-stu-id="a0bc7-109">Parameters needed tooupgrade</span></span>
<span data-ttu-id="a0bc7-110">Существует два типа развертывания: обычное или обновление.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-110">You can choose from two types of deployment: regular or upgrade.</span></span> <span data-ttu-id="a0bc7-111">Регулярные развертывания будут удалены все предыдущие сведения о развертывании и данные на кластере hello во время развертывания обновления сохраняет его.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-111">A regular deployment erases any previous deployment information and data on hello cluster, while an upgrade deployment preserves it.</span></span> <span data-ttu-id="a0bc7-112">При обновлении приложения Service Fabric в Visual Studio требуется параметров обновления приложения tooprovide и проверку политики работоспособности.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-112">When you upgrade a Service Fabric application in Visual Studio, you need tooprovide application upgrade parameters and health check policies.</span></span> <span data-ttu-id="a0bc7-113">Обновление приложения, параметры помогают управлять обновления hello при проверку политики работоспособности определить, успешно ли прошло обновление hello.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-113">Application upgrade parameters help control hello upgrade, while health check policies determine whether hello upgrade was successful.</span></span> <span data-ttu-id="a0bc7-114">Дополнительные сведения см. в статье [Параметры обновления приложений](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="a0bc7-114">See [Service Fabric application upgrade: upgrade parameters](service-fabric-application-upgrade-parameters.md) for more details.</span></span>

<span data-ttu-id="a0bc7-115">Существует три режима обновления: *отслеживаемое*, *неотслеживаемое автоматическое* и *неотслеживаемое ручное*.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-115">There are three upgrade modes: *Monitored*, *UnmonitoredAuto*, and *UnmonitoredManual*.</span></span>

* <span data-ttu-id="a0bc7-116">Обновление отслеживаемое автоматизирует обновление hello и приложение проверки работоспособности.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-116">A Monitored upgrade automates hello upgrade and application health check.</span></span>
* <span data-ttu-id="a0bc7-117">Обновление UnmonitoredAuto автоматизирует обновление hello, но пропускает hello проверки работоспособности приложения.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-117">An UnmonitoredAuto upgrade automates hello upgrade, but skips hello application health check.</span></span>
* <span data-ttu-id="a0bc7-118">При этом обновление UnmonitoredManual необходимо toomanually обновить каждый домен обновления.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-118">When you do an UnmonitoredManual upgrade, you need toomanually upgrade each upgrade domain.</span></span>

<span data-ttu-id="a0bc7-119">Для каждого режима обновления необходим различный набор параметров.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-119">Each upgrade mode requires different sets of parameters.</span></span> <span data-ttu-id="a0bc7-120">В разделе [параметров обновления приложения](service-fabric-application-upgrade-parameters.md) toolearn больше о доступных параметрах обновления hello.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-120">See [Application upgrade parameters](service-fabric-application-upgrade-parameters.md) toolearn more about hello available upgrade options.</span></span>

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="a0bc7-121">Обновление приложения Service Fabric в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a0bc7-121">Upgrade a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="a0bc7-122">Если вы используете tooupgrade средств Visual Studio Service Fabric hello приложения Service Fabric, можно указать toobe процесс публикации обновления, а не регулярное развертывания путем проверки hello **обновление приложения hello** проверки поле.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-122">If you’re using hello Visual Studio Service Fabric tools tooupgrade a Service Fabric application, you can specify a publish process toobe an upgrade rather than a regular deployment by checking hello **Upgrade hello application** check box.</span></span>

### <a name="tooconfigure-hello-upgrade-parameters"></a><span data-ttu-id="a0bc7-123">Параметры обновления tooconfigure hello</span><span class="sxs-lookup"><span data-stu-id="a0bc7-123">tooconfigure hello upgrade parameters</span></span>
1. <span data-ttu-id="a0bc7-124">Нажмите кнопку hello **параметры** кнопки следующий toohello флажок.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-124">Click hello **Settings** button next toohello check box.</span></span> <span data-ttu-id="a0bc7-125">Hello **изменение параметров обновления** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-125">hello **Edit Upgrade Parameters** dialog box appears.</span></span> <span data-ttu-id="a0bc7-126">Hello **изменение параметров обновления** диалоговое окно поддерживает режимы hello отслеживаемое, UnmonitoredAuto и UnmonitoredManual обновления.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-126">hello **Edit Upgrade Parameters** dialog box supports hello Monitored, UnmonitoredAuto, and UnmonitoredManual upgrade modes.</span></span>
2. <span data-ttu-id="a0bc7-127">Выберите режим обновления hello toouse а затем заполнить hello сеткой параметров.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-127">Select hello upgrade mode that you want toouse and then fill out hello parameter grid.</span></span>

    <span data-ttu-id="a0bc7-128">Каждый параметр имеет значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-128">Each parameter has default values.</span></span> <span data-ttu-id="a0bc7-129">Необязательный параметр Hello *DefaultServiceTypeHealthPolicy* входные таблицы хэша.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-129">hello optional parameter *DefaultServiceTypeHealthPolicy* takes a hash table input.</span></span> <span data-ttu-id="a0bc7-130">Ниже приведен пример входной формат hello хэш-таблицы для *DefaultServiceTypeHealthPolicy*:</span><span class="sxs-lookup"><span data-stu-id="a0bc7-130">Here’s an example of hello hash table input format for *DefaultServiceTypeHealthPolicy*:</span></span>

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    <span data-ttu-id="a0bc7-131">*ServiceTypeHealthPolicyMap* еще один необязательный параметр, входные таблицы хэша в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="a0bc7-131">*ServiceTypeHealthPolicyMap* is another optional parameter that takes a hash table input in hello following format:</span></span>

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    <span data-ttu-id="a0bc7-132">Ниже приведен пример из реальной жизни:</span><span class="sxs-lookup"><span data-stu-id="a0bc7-132">Here's a real-life example:</span></span>

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. <span data-ttu-id="a0bc7-133">Если выбран режим обновления UnmonitoredManual, необходимо вручную запустите toocontinue консоль PowerShell и завершения процесса обновления hello.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-133">If you select UnmonitoredManual upgrade mode, you must manually start a PowerShell console toocontinue and finish hello upgrade process.</span></span> <span data-ttu-id="a0bc7-134">См. слишком[обновление приложения Service Fabric: Дополнительные разделы](service-fabric-application-upgrade-advanced.md) toolearn вручную обновить works.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-134">Refer too[Service Fabric application upgrade: advanced topics](service-fabric-application-upgrade-advanced.md) toolearn how manual upgrade works.</span></span>

## <a name="upgrade-an-application-by-using-powershell"></a><span data-ttu-id="a0bc7-135">Обновление приложения с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0bc7-135">Upgrade an application by using PowerShell</span></span>
<span data-ttu-id="a0bc7-136">Можно использовать командлеты PowerShell tooupgrade приложения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-136">You can use PowerShell cmdlets tooupgrade a Service Fabric application.</span></span> <span data-ttu-id="a0bc7-137">Подробные сведения см. в [руководстве по обновлению приложений Service Fabric](service-fabric-application-upgrade-tutorial.md) и статье, посвященной командлету [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx).</span><span class="sxs-lookup"><span data-stu-id="a0bc7-137">See [Service Fabric application upgrade tutorial](service-fabric-application-upgrade-tutorial.md) and [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) for detailed information.</span></span>

## <a name="specify-a-health-check-policy-in-hello-application-manifest-file"></a><span data-ttu-id="a0bc7-138">Укажите в файле манифеста приложения hello проверку политики работоспособности</span><span class="sxs-lookup"><span data-stu-id="a0bc7-138">Specify a health check policy in hello application manifest file</span></span>
<span data-ttu-id="a0bc7-139">Каждая служба в приложении Service Fabric может иметь собственные параметры политики работоспособности, которые переопределяют значения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-139">Every service in a Service Fabric application can have its own health policy parameters that override hello default values.</span></span> <span data-ttu-id="a0bc7-140">Можно предоставить значения этих параметров в файле манифеста приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-140">You can provide these parameter values in hello application manifest file.</span></span>

<span data-ttu-id="a0bc7-141">Hello следующем примере показано, как tooapply уникальный работоспособности проверьте политику для каждой службы в манифесте приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a0bc7-141">hello following example shows how tooapply a unique health check policy for each service in hello application manifest.</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="a0bc7-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a0bc7-142">Next steps</span></span>
<span data-ttu-id="a0bc7-143">Дополнительные сведения о развертывании приложений см. в статье [Развертывание гостевого исполняемого файла в Service Fabric](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="a0bc7-143">For more information about deploying an application, see [Deploy an existing application in Azure Service Fabric](service-fabric-deploy-existing-app.md).</span></span>