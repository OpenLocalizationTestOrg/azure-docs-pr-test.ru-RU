---
title: "aaaCollect журналы с помощью диагностики Azure | Документы Microsoft"
description: "В этой статье описывается, как tooset копирование toocollect диагностики Azure журналов из кластера Service Fabric, запущенных в Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 9f7e1fa5-6543-4efd-b53f-39510f18df56
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: afbcfbe972b1847ef33bf0539b4398794b1bd56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a><span data-ttu-id="01979-103">Сбор журналов с помощью системы диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="01979-103">Collect logs by using Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="01979-104">Windows</span><span class="sxs-lookup"><span data-stu-id="01979-104">Windows</span></span>](service-fabric-diagnostics-how-to-setup-wad.md)
> * [<span data-ttu-id="01979-105">Linux</span><span class="sxs-lookup"><span data-stu-id="01979-105">Linux</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

<span data-ttu-id="01979-106">При запуске кластера с Azure Service Fabric это журналы hello смысл toocollect со всех узлов hello в центральном расположении.</span><span class="sxs-lookup"><span data-stu-id="01979-106">When you're running an Azure Service Fabric cluster, it's a good idea toocollect hello logs from all hello nodes in a central location.</span></span> <span data-ttu-id="01979-107">Наличие журналы hello в центральном расположении, помогает выполнить анализ и устранение проблем в кластере, или в hello приложений и служб, работающих в этом кластере.</span><span class="sxs-lookup"><span data-stu-id="01979-107">Having hello logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in hello applications and services running in that cluster.</span></span>

<span data-ttu-id="01979-108">Собирать журналы и tooupload один из способов — расширение диагностики Azure toouse hello, какие передачи журналов tooAzure хранилища Azure Application Insights и концентраторов событий Azure.</span><span class="sxs-lookup"><span data-stu-id="01979-108">One way tooupload and collect logs is toouse hello Azure Diagnostics extension, which uploads logs tooAzure Storage, Azure Application Insights, or Azure Event Hubs.</span></span> <span data-ttu-id="01979-109">журналы Hello не окажется полезным непосредственно в хранилище или концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="01979-109">hello logs are not that useful directly in storage or in Event Hubs.</span></span> <span data-ttu-id="01979-110">Однако вы можете использовать внешний процесс tooread hello событий из хранилища и поместите их в продукте [анализа журналов](../log-analytics/log-analytics-service-fabric.md) или другим решением для синтаксического анализа журнала.</span><span class="sxs-lookup"><span data-stu-id="01979-110">But you can use an external process tooread hello events from storage and place them in a product such as [Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span> <span data-ttu-id="01979-111">В [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) предоставляется с возможностью полного поиска по журналам и встроенной службой аналитики.</span><span class="sxs-lookup"><span data-stu-id="01979-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) comes with a comprehensive log search and analytics service built-in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01979-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="01979-112">Prerequisites</span></span>
<span data-ttu-id="01979-113">Используйте эти средства tooperform некоторые операции hello в этом документе:</span><span class="sxs-lookup"><span data-stu-id="01979-113">You use these tools tooperform some of hello operations in this document:</span></span>

* <span data-ttu-id="01979-114">[Диагностика Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (о tooAzure облачные службы, но имеет хорошее сведения и примеры)</span><span class="sxs-lookup"><span data-stu-id="01979-114">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related tooAzure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="01979-115">Диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="01979-115">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="01979-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="01979-116">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="01979-117">Клиент Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="01979-117">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="01979-118">Шаблон Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="01979-118">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-toocollect"></a><span data-ttu-id="01979-119">Вы можете toocollect источников журнала</span><span class="sxs-lookup"><span data-stu-id="01979-119">Log sources that you might want toocollect</span></span>
* <span data-ttu-id="01979-120">**Журналы Service Fabric**: создается для hello платформы toostandard трассировки событий для Windows (ETW) и EventSource каналов.</span><span class="sxs-lookup"><span data-stu-id="01979-120">**Service Fabric logs**: Emitted from hello platform toostandard Event Tracing for Windows (ETW) and EventSource channels.</span></span> <span data-ttu-id="01979-121">Журналы могут принадлежать к одному из следующих типов.</span><span class="sxs-lookup"><span data-stu-id="01979-121">Logs can be one of several types:</span></span>
  * <span data-ttu-id="01979-122">События операционного канала: журналы для операций, которые выполняет платформы Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="01979-122">Operational events: Logs for operations that hello Service Fabric platform performs.</span></span> <span data-ttu-id="01979-123">Некоторые примеры: создание приложений и служб, изменение состояния узлов и сведения об обновлении.</span><span class="sxs-lookup"><span data-stu-id="01979-123">Examples include creation of applications and services, node state changes, and upgrade information.</span></span>
  * <span data-ttu-id="01979-124">[События модели программирования на основе Reliable Actors](service-fabric-reliable-actors-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="01979-124">[Reliable Actors programming model events](service-fabric-reliable-actors-diagnostics.md)</span></span>
  * <span data-ttu-id="01979-125">[События модели программирования на основе Reliable Services](service-fabric-reliable-services-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="01979-125">[Reliable Services programming model events](service-fabric-reliable-services-diagnostics.md)</span></span>
* <span data-ttu-id="01979-126">**События приложения**: события, переданные из кода приложения службы и записывается с помощью вспомогательного класса EventSource hello, в Visual Studio шаблоны hello.</span><span class="sxs-lookup"><span data-stu-id="01979-126">**Application events**: Events emitted from your service's code and written out by using hello EventSource helper class provided in hello Visual Studio templates.</span></span> <span data-ttu-id="01979-127">Дополнительные сведения о как toowrite журналы из приложения в разделе [монитора и диагностики служб в случае установки локального компьютера разработки](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="01979-127">For more information on how toowrite logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-hello-diagnostics-extension"></a><span data-ttu-id="01979-128">Развертывание расширения диагностики hello</span><span class="sxs-lookup"><span data-stu-id="01979-128">Deploy hello Diagnostics extension</span></span>
<span data-ttu-id="01979-129">Первым шагом Hello в сбор журналов является расширение диагностики toodeploy hello в каждой из виртуальных машин hello в кластер Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="01979-129">hello first step in collecting logs is toodeploy hello Diagnostics extension on each of hello VMs in hello Service Fabric cluster.</span></span> <span data-ttu-id="01979-130">Hello расширения диагностики собирает журналы на каждой виртуальной Машине и отправляет их toohello учетной записи хранения, указанной вами.</span><span class="sxs-lookup"><span data-stu-id="01979-130">hello Diagnostics extension collects logs on each VM and uploads them toohello storage account that you specify.</span></span> <span data-ttu-id="01979-131">шаги Hello немного отличаться в зависимости от hello портал Azure или диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="01979-131">hello steps vary a little based on whether you use hello Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="01979-132">Hello действия также различаются в зависимости от возможность развертывания hello является частью создания кластера или кластера, который уже существует.</span><span class="sxs-lookup"><span data-stu-id="01979-132">hello steps also vary based on whether hello deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="01979-133">Давайте рассмотрим hello действия для каждого сценария.</span><span class="sxs-lookup"><span data-stu-id="01979-133">Let's look at hello steps for each scenario.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-hello-portal"></a><span data-ttu-id="01979-134">Развертывание расширения диагностики hello в процессе создания кластера через портал hello</span><span class="sxs-lookup"><span data-stu-id="01979-134">Deploy hello Diagnostics extension as part of cluster creation through hello portal</span></span>
<span data-ttu-id="01979-135">toodeploy hello диагностики расширения toohello виртуальных машин в кластере hello в процессе создания кластера, используйте панель параметров диагностики hello, показано в hello после изображения.</span><span class="sxs-lookup"><span data-stu-id="01979-135">toodeploy hello Diagnostics extension toohello VMs in hello cluster as part of cluster creation, you use hello Diagnostics settings panel shown in hello following image.</span></span> <span data-ttu-id="01979-136">tooenable сбора событий службы Reliable Actor или надежные службы, убедитесь, что диагностики слишком**на** (по умолчанию hello).</span><span class="sxs-lookup"><span data-stu-id="01979-136">tooenable Reliable Actors or Reliable Services event collection, ensure that Diagnostics is set too**On** (hello default setting).</span></span> <span data-ttu-id="01979-137">После создания кластера hello, нельзя изменить эти параметры с помощью портала hello.</span><span class="sxs-lookup"><span data-stu-id="01979-137">After you create hello cluster, you can't change these settings by using hello portal.</span></span>

![Параметры диагностики Azure hello портала для создания кластера](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

<span data-ttu-id="01979-139">Здравствуйте, группа поддержки Azure *требует* поддержки журналы toohelp resolve запросы в службу поддержки, создаваемые.</span><span class="sxs-lookup"><span data-stu-id="01979-139">hello Azure support team *requires* support logs toohelp resolve any support requests that you create.</span></span> <span data-ttu-id="01979-140">Эти журналы собираются в режиме реального времени и хранятся в одной из учетных записей хранилища hello, создан в группе ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="01979-140">These logs are collected in real time and are stored in one of hello storage accounts created in hello resource group.</span></span> <span data-ttu-id="01979-141">параметры диагностики Hello настройте события уровня приложения.</span><span class="sxs-lookup"><span data-stu-id="01979-141">hello Diagnostics settings configure application-level events.</span></span> <span data-ttu-id="01979-142">К этим событиям относятся [службы Reliable Actor](service-fabric-reliable-actors-diagnostics.md) события, [надежного обмена](service-fabric-reliable-services-diagnostics.md) события, а некоторые события toobe Service Fabric системного уровня, в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="01979-142">These events include [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) events, [Reliable Services](service-fabric-reliable-services-diagnostics.md) events, and some system-level Service Fabric events toobe stored in Azure Storage.</span></span>

<span data-ttu-id="01979-143">Продукты, такие как [Elasticsearch](https://www.elastic.co/guide/index.html) собственного процесса, можно получить из учетной записи хранения hello hello события.</span><span class="sxs-lookup"><span data-stu-id="01979-143">Products such as [Elasticsearch](https://www.elastic.co/guide/index.html) or your own process can get hello events from hello storage account.</span></span> <span data-ttu-id="01979-144">В данный момент нет способа toofilter или очистки hello событий, отправляемых toohello таблицы.</span><span class="sxs-lookup"><span data-stu-id="01979-144">There is currently no way toofilter or groom hello events that are sent toohello table.</span></span> <span data-ttu-id="01979-145">Если не реализовать tooremove обработки событий, из таблицы hello, таблица hello останется toogrow.</span><span class="sxs-lookup"><span data-stu-id="01979-145">If you don't implement a process tooremove events from hello table, hello table will continue toogrow.</span></span>

<span data-ttu-id="01979-146">При создании кластера с помощью портала hello, настоятельно рекомендуется загрузить шаблон hello **до нажатия кнопки ОК** toocreate hello кластера.</span><span class="sxs-lookup"><span data-stu-id="01979-146">When you're creating a cluster by using hello portal, we highly recommend that you download hello template **before you click OK** toocreate hello cluster.</span></span> <span data-ttu-id="01979-147">Дополнительные сведения приведены слишком[настроить кластер Service Fabric с помощью шаблона Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="01979-147">For details, refer too[Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="01979-148">Потребуется hello шаблон toomake изменений более поздней версии, так как не удается внести некоторые изменения с помощью портала hello.</span><span class="sxs-lookup"><span data-stu-id="01979-148">You'll need hello template toomake changes later, because you can't make some changes by using hello portal.</span></span>

<span data-ttu-id="01979-149">Шаблоны можно экспортировать из hello портала с помощью hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="01979-149">You can export templates from hello portal by using hello following steps.</span></span> <span data-ttu-id="01979-150">Тем не менее эти шаблоны может быть сложнее toouse, так как они могут иметь значения null, в которых отсутствуют необходимые сведения.</span><span class="sxs-lookup"><span data-stu-id="01979-150">However, these templates can be more difficult toouse because they might have null values that are missing required information.</span></span>

1. <span data-ttu-id="01979-151">Откройте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="01979-151">Open your resource group.</span></span>
2. <span data-ttu-id="01979-152">Выберите **параметры** toodisplay hello параметры панели.</span><span class="sxs-lookup"><span data-stu-id="01979-152">Select **Settings** toodisplay hello settings panel.</span></span>
3. <span data-ttu-id="01979-153">Выберите **развертываний** «журнал» toodisplay hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="01979-153">Select **Deployments** toodisplay hello deployment history panel.</span></span>
4. <span data-ttu-id="01979-154">Выберите сведения о hello развертывания toodisplay hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="01979-154">Select a deployment toodisplay hello details of hello deployment.</span></span>
5. <span data-ttu-id="01979-155">Выберите **Экспорт шаблона** toodisplay hello шаблона панели.</span><span class="sxs-lookup"><span data-stu-id="01979-155">Select **Export Template** toodisplay hello template panel.</span></span>
6. <span data-ttu-id="01979-156">Выберите **сохранить toofile** tooexport ZIP-файл, содержащий шаблон hello, параметры и файлы PowerShell.</span><span class="sxs-lookup"><span data-stu-id="01979-156">Select **Save toofile** tooexport a .zip file that contains hello template, parameter, and PowerShell files.</span></span>

<span data-ttu-id="01979-157">После экспорта файлов hello необходимо toomake изменение.</span><span class="sxs-lookup"><span data-stu-id="01979-157">After you export hello files, you need toomake a modification.</span></span> <span data-ttu-id="01979-158">Измените файл parameters.json hello и удалите hello **adminPassword** элемента.</span><span class="sxs-lookup"><span data-stu-id="01979-158">Edit hello parameters.json file and remove hello **adminPassword** element.</span></span> <span data-ttu-id="01979-159">Запрашивать пароль hello произойдет при запуске скрипта развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="01979-159">This will cause a prompt for hello password when hello deployment script is run.</span></span> <span data-ttu-id="01979-160">При запуске скрипта развертывания hello, может потребоваться toofix значения null для параметров.</span><span class="sxs-lookup"><span data-stu-id="01979-160">When you're running hello deployment script, you might have toofix null parameter values.</span></span>

<span data-ttu-id="01979-161">toouse hello загрузить tooupdate шаблона конфигурации:</span><span class="sxs-lookup"><span data-stu-id="01979-161">toouse hello downloaded template tooupdate a configuration:</span></span>

1. <span data-ttu-id="01979-162">Извлеките hello содержимое tooa папку на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="01979-162">Extract hello contents tooa folder on your local computer.</span></span>
2. <span data-ttu-id="01979-163">Измените hello содержимое tooreflect hello новую конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="01979-163">Modify hello contents tooreflect hello new configuration.</span></span>
3. <span data-ttu-id="01979-164">Запустите PowerShell и изменить папку toohello, которую было извлечено содержимое hello.</span><span class="sxs-lookup"><span data-stu-id="01979-164">Start PowerShell and change toohello folder where you extracted hello content.</span></span>
4. <span data-ttu-id="01979-165">Запустите **deploy.ps1** и введите идентификатор подписки hello, имя группы ресурсов hello (используйте hello же конфигурации hello tooupdate имени) и имя развертывания.</span><span class="sxs-lookup"><span data-stu-id="01979-165">Run **deploy.ps1** and fill in hello subscription ID, hello resource group name (use hello same name tooupdate hello configuration), and a unique deployment name.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="01979-166">Развертывание расширения диагностики hello в процессе создания кластера с помощью диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="01979-166">Deploy hello Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="01979-167">toocreate кластера с помощью диспетчера ресурсов необходимо tooadd hello диагностики конфигурации JSON toohello полного кластера шаблона диспетчера ресурсов перед созданием кластера hello.</span><span class="sxs-lookup"><span data-stu-id="01979-167">toocreate a cluster by using Resource Manager, you need tooadd hello Diagnostics configuration JSON toohello full cluster Resource Manager template before you create hello cluster.</span></span> <span data-ttu-id="01979-168">Мы предоставляем образец шаблона диспетчера ресурсов кластера пяти ВМ с конфигурацией диагностики добавлены tooit как часть наши примеры шаблона диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="01979-168">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added tooit as part of our Resource Manager template samples.</span></span> <span data-ttu-id="01979-169">Его можно просматривать в этом месте в коллекции примеров Azure hello: [пяти узла кластера с образцом шаблона диспетчера ресурсов диагностики](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span><span class="sxs-lookup"><span data-stu-id="01979-169">You can see it at this location in hello Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span></span>

<span data-ttu-id="01979-170">параметры диагностики toosee hello в hello шаблона диспетчера ресурсов, откройте hello azuredeploy.json файл и выполните поиск **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="01979-170">toosee hello Diagnostics setting in hello Resource Manager template, open hello azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="01979-171">toocreate кластера с помощью этого шаблона, выберите hello **развертывание tooAzure** кнопка доступны по ссылке на предыдущую hello.</span><span class="sxs-lookup"><span data-stu-id="01979-171">toocreate a cluster by using this template, select hello **Deploy tooAzure** button available at hello previous link.</span></span>

<span data-ttu-id="01979-172">Можно также загрузить образец hello диспетчера ресурсов, внести изменения tooit и создайте кластер с hello измененный шаблон с помощью hello `New-AzureRmResourceGroupDeployment` команду в окне Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="01979-172">Alternatively, you can download hello Resource Manager sample, make changes tooit, and create a cluster with hello modified template by using hello `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="01979-173">См. следующий код для hello параметры, которые передаются в команде toohello hello.</span><span class="sxs-lookup"><span data-stu-id="01979-173">See hello following code for hello parameters that you pass in toohello command.</span></span> <span data-ttu-id="01979-174">Подробные сведения о том, как группировать toodeploy ресурса с помощью PowerShell. в статье hello [развертывания группы ресурсов с помощью шаблона Azure Resource Manager hello](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="01979-174">For detailed information on how toodeploy a resource group by using PowerShell, see hello article [Deploy a resource group with hello Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a><span data-ttu-id="01979-175">Развертывание существующего кластера расширения диагностики tooan hello</span><span class="sxs-lookup"><span data-stu-id="01979-175">Deploy hello Diagnostics extension tooan existing cluster</span></span>
<span data-ttu-id="01979-176">При наличии существующего кластера, у которого нет диагностики развертывания или вы хотите toomodify существующей конфигурации, можно добавить или обновить ее.</span><span class="sxs-lookup"><span data-stu-id="01979-176">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want toomodify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="01979-177">Изменение шаблона диспетчера ресурсов hello, используемые toocreate hello существующего кластера или загрузить шаблон hello из портала hello, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="01979-177">Modify hello Resource Manager template that's used toocreate hello existing cluster or download hello template from hello portal as described earlier.</span></span> <span data-ttu-id="01979-178">Измените файл template.json hello, выполнив следующие задачи hello.</span><span class="sxs-lookup"><span data-stu-id="01979-178">Modify hello template.json file by performing hello following tasks.</span></span>

<span data-ttu-id="01979-179">Добавьте новый шаблон toohello ресурсов хранения, добавив раздел ресурсов toohello.</span><span class="sxs-lookup"><span data-stu-id="01979-179">Add a new storage resource toohello template by adding toohello resources section.</span></span>

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[parameters('applicationDiagnosticsStorageAccountName')]",
  "location": "[parameters('computeLocation')]",
  "properties": {
    "accountType": "[parameters('applicationDiagnosticsStorageAccountType')]"
  },
  "tags": {
    "resourceType": "Service Fabric",
    "clusterName": "[parameters('clusterName')]"
  }
},
```

 <span data-ttu-id="01979-180">Добавьте параметры toohello статьи сразу после определения учетной записи хранилища hello, между `supportLogStorageAccountName` и `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="01979-180">Next, add toohello parameters section just after hello storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="01979-181">Замените текст заполнителя hello *здесь имя учетной записи хранения* с именем hello hello учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="01979-181">Replace hello placeholder text *storage account name goes here* with hello name of hello storage account.</span></span>

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for hello application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for hello storage account that contains application diagnostics data from hello cluster"
      }
    },
```
<span data-ttu-id="01979-182">Обновите hello `VirtualMachineProfile` раздел файла template.json hello, добавив следующий код в пределах массива расширения hello hello.</span><span class="sxs-lookup"><span data-stu-id="01979-182">Then, update hello `VirtualMachineProfile` section of hello template.json file by adding hello following code within hello extensions array.</span></span> <span data-ttu-id="01979-183">Быть убедиться, что tooadd запятая в начале hello или в конце hello, в зависимости от того, куда вставляется.</span><span class="sxs-lookup"><span data-stu-id="01979-183">Be sure tooadd a comma at hello beginning or hello end, depending on where it's inserted.</span></span>

```json
{
    "name": "[concat(parameters('vmNodeType0Name'),'_Microsoft.Insights.VMDiagnosticsSettings')]",
    "properties": {
        "type": "IaaSDiagnostics",
        "autoUpgradeMinorVersion": true,
        "protectedSettings": {
        "storageAccountName": "[parameters('applicationDiagnosticsStorageAccountName')]",
        "storageAccountKey": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName')),'2015-05-01-preview').key1]",
        "storageAccountEndPoint": "https://core.windows.net/"
        },
        "publisher": "Microsoft.Azure.Diagnostics",
        "settings": {
        "WadCfg": {
            "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": "50000",
            "EtwProviders": {
                "EtwEventSourceProviderConfiguration": [
                {
                    "provider": "Microsoft-ServiceFabric-Actors",
                    "scheduledTransferKeywordFilter": "1",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableActorEventTable"
                    }
                },
                {
                    "provider": "Microsoft-ServiceFabric-Services",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableServiceEventTable"
                    }
                }
                ],
                "EtwManifestProviderConfiguration": [
                {
                    "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
                    "scheduledTransferLogLevelFilter": "Information",
                    "scheduledTransferKeywordFilter": "4611686018427387904",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricSystemEventTable"
                    }
                }
                ]
            }
            }
        },
        "StorageAccount": "[parameters('applicationDiagnosticsStorageAccountName')]"
        },
        "typeHandlerVersion": "1.5"
    }
}
```

<span data-ttu-id="01979-184">После изменения файла template.json hello, как описано, повторная публикация шаблона диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="01979-184">After you modify hello template.json file as described, republish hello Resource Manager template.</span></span> <span data-ttu-id="01979-185">Если шаблон hello был экспортирован, выполняется файл deploy.ps1 hello опубликует hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="01979-185">If hello template was exported, running hello deploy.ps1 file republishes hello template.</span></span> <span data-ttu-id="01979-186">После развертывания убедитесь, что параметр **ProvisioningState** имеет значение **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="01979-186">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="update-diagnostics-toocollect-health-and-load-events"></a><span data-ttu-id="01979-187">События диагностики toocollect работоспособности и загрузка обновления</span><span class="sxs-lookup"><span data-stu-id="01979-187">Update diagnostics toocollect health and load events</span></span>

<span data-ttu-id="01979-188">Начиная с выпуска hello 5.4 Service Fabric, работоспособности и загрузка метрики события, доступные для коллекции.</span><span class="sxs-lookup"><span data-stu-id="01979-188">Starting with hello 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="01979-189">Эти события отражают события, создаваемые системой hello или код с помощью работоспособности hello или загрузить отчетов интерфейсы API, такие как [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) или [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="01979-189">These events reflect events generated by hello system or your code by using hello health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="01979-190">Это обеспечивает статистическую обработку и просмотр состояния работоспособности системы с течением временем, а также оповещение на основе событий работоспособности или нагрузки.</span><span class="sxs-lookup"><span data-stu-id="01979-190">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="01979-191">Эти события в окне просмотра событий диагностики в Visual Studio добавьте tooview «Microsoft-ServiceFabric:4:0x4000000000000008» toohello список поставщиков трассировки событий Windows.</span><span class="sxs-lookup"><span data-stu-id="01979-191">tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" toohello list of ETW providers.</span></span>

<span data-ttu-id="01979-192">события toocollect hello, изменить tooinclude шаблона диспетчера ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="01979-192">toocollect hello events, modify hello resource manager template tooinclude</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387912",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

## <a name="update-diagnostics-toocollect-and-upload-logs-from-new-eventsource-channels"></a><span data-ttu-id="01979-193">Обновление toocollect диагностики и отправлять журналы из новых каналов EventSource</span><span class="sxs-lookup"><span data-stu-id="01979-193">Update Diagnostics toocollect and upload logs from new EventSource channels</span></span>
<span data-ttu-id="01979-194">журналы toocollect tooupdate диагностики из новых каналов EventSource, представляющие новое приложение, которое скоро будет toodeploy, выполнять hello же шаги как hello [предыдущего раздела](#deploywadarm) для настройки диагностики для существующей кластер.</span><span class="sxs-lookup"><span data-stu-id="01979-194">tooupdate Diagnostics toocollect logs from new EventSource channels that represent a new application that you're about toodeploy, perform hello same steps as in hello [previous section](#deploywadarm) for setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="01979-195">Обновить hello `EtwEventSourceProviderConfiguration` раздела записи tooadd hello template.json файлов для обновления hello новых EventSource каналов перед применением hello конфигурации с помощью hello `New-AzureRmResourceGroupDeployment` команды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="01979-195">Update hello `EtwEventSourceProviderConfiguration` section in hello template.json file tooadd entries for hello new EventSource channels before you apply hello configuration update by using hello `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="01979-196">Имя источника события hello Hello определяется как часть кода в файле hello ServiceEventSource.cs, созданный средой Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="01979-196">hello name of hello event source is defined as part of your code in hello Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="01979-197">Например если источник события с именем My Eventsource, добавьте следующую hello tooplace коды событий из Мой Eventsource в таблицу с именем MyDestinationTableName hello.</span><span class="sxs-lookup"><span data-stu-id="01979-197">For example, if your event source is named My-Eventsource, add hello following code tooplace hello events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="01979-198">счетчики производительности toocollect или журналы событий изменения шаблона диспетчера ресурсов hello с помощью hello примеры, приведенные в [Создание виртуальной машины Windows с помощью мониторинга и диагностики с помощью шаблона Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="01979-198">toocollect performance counters or event logs, modify hello Resource Manager template by using hello examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="01979-199">Затем повторно опубликуйте hello шаблона диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="01979-199">Then, republish hello Resource Manager template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01979-200">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="01979-200">Next steps</span></span>
<span data-ttu-id="01979-201">какие события следует искать при диагностике проблем с toounderstand более подробно см. события диагностики hello для [службы Reliable Actor](service-fabric-reliable-actors-diagnostics.md) и [надежного обмена](service-fabric-reliable-services-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="01979-201">toounderstand in more detail what events you should look for while troubleshooting issues, see hello diagnostic events emitted for [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) and [Reliable Services](service-fabric-reliable-services-diagnostics.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="01979-202">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="01979-202">Related articles</span></span>
* [<span data-ttu-id="01979-203">Узнайте, как счетчики производительности toocollect или журналы с помощью hello расширения диагностики</span><span class="sxs-lookup"><span data-stu-id="01979-203">Learn how toocollect performance counters or logs by using hello Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* <span data-ttu-id="01979-204">[Service Fabric Solution in Log Analytics](../log-analytics/log-analytics-service-fabric.md) (Решение Service Fabric в Log Analytics)</span><span class="sxs-lookup"><span data-stu-id="01979-204">[Service Fabric solution in Log Analytics](../log-analytics/log-analytics-service-fabric.md)</span></span>

