---
title: "Здравствуйте, aaaAssess приложения Service Fabric с анализа журналов с помощью портала Azure | Документы Microsoft"
description: "Можно использовать решение Service Fabric hello в службе анализа журналов с помощью hello Azure портала tooassess hello риска и работоспособности приложения Service Fabric микро служб, узлов и кластеров."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 9c91aacb-c48e-466c-b792-261f25940c0c
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: nini
ms.openlocfilehash: 891c7f6e5ed511ac18599bdc280ab3dc09700fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-hello-azure-portal"></a><span data-ttu-id="d67ac-103">Оценка приложения Service Fabric и микро служб с помощью hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="d67ac-103">Assess Service Fabric applications and micro-services with hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d67ac-104">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="d67ac-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="d67ac-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d67ac-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>

![Символ Service Fabric](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="d67ac-107">В этой статье описывается как hello toouse Service Fabric решения в службе анализа журналов toohelp выявить и устранить проблемы к кластеру Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d67ac-107">This article describes how toouse hello Service Fabric solution in Log Analytics toohelp identify and troubleshoot issues across your Service Fabric cluster.</span></span>

<span data-ttu-id="d67ac-108">Hello Service Fabric решение использует данные диагностики Azure Service Fabric виртуальные машины, путем сбора данных из таблиц Azure WAD.</span><span class="sxs-lookup"><span data-stu-id="d67ac-108">hello Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="d67ac-109">Log Analytics затем считывает события платформы Service Fabric, включая **события надежной службы**, **события субъектов**, **операционные события** и **пользовательские события трассировки событий Windows**.</span><span class="sxs-lookup"><span data-stu-id="d67ac-109">Log Analytics then reads Service Fabric framework events, including **Reliable Service Events**, **Actor Events**, **Operational Events**, and **Custom ETW events**.</span></span> <span data-ttu-id="d67ac-110">С панели мониторинга решения hello являются важные моменты может tooview и соответствующие события в вашей среде Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d67ac-110">With hello solution dashboard, you are able tooview notable issues and relevant events in your Service Fabric environment.</span></span>

<span data-ttu-id="d67ac-111">tooget работы с решением hello, необходимо tooconnect рабочей области аналитики журналов tooa кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d67ac-111">tooget started with hello solution, you need tooconnect your Service Fabric cluster tooa Log Analytics workspace.</span></span> <span data-ttu-id="d67ac-112">Ниже приведены три tooconsider сценариев.</span><span class="sxs-lookup"><span data-stu-id="d67ac-112">Here are three scenarios tooconsider:</span></span>

1. <span data-ttu-id="d67ac-113">Если кластер Service Fabric не установлен, выполните действия hello в ***развертывание рабочей области аналитики журналов tooa подключения кластера Service Fabric*** toodeploy новый кластер и настроили tooreport tooLog Analytics.</span><span class="sxs-lookup"><span data-stu-id="d67ac-113">If you have not deployed your Service Fabric cluster, use hello steps in ***Deploy a Service Fabric Cluster connected tooa Log Analytics workspace*** toodeploy a new cluster and have it configured tooreport tooLog Analytics.</span></span>
2. <span data-ttu-id="d67ac-114">Счетчики производительности toocollect из вашего toouse узлов других решений OMS, такие как безопасность в кластере Service Fabric, выполните шаги hello в ***развертывание рабочей области аналитики журналов tooa подключения кластера Service Fabric с расширением ВМ установлен.***</span><span class="sxs-lookup"><span data-stu-id="d67ac-114">If you need toocollect performance counters from your hosts toouse other OMS solutions such as Security on your Service Fabric Cluster, follow hello steps in ***Deploy a Service Fabric Cluster connected tooa Log Analytics workspace with VM Extension installed.***</span></span>
3. <span data-ttu-id="d67ac-115">Если вы уже развернули кластера Service Fabric и tooconnect его tooLog Analytics, следуйте указаниям hello ***Добавление существующей учетной записи хранилища tooLog Analytics.***</span><span class="sxs-lookup"><span data-stu-id="d67ac-115">If you have already deployed your Service Fabric cluster and want tooconnect it tooLog Analytics, follow hello steps in ***Adding an existing storage account tooLog Analytics.***</span></span>

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace"></a><span data-ttu-id="d67ac-116">Развертывание рабочей области аналитики журналов tooa подключения кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d67ac-116">Deploy a Service Fabric Cluster connected tooa Log Analytics workspace.</span></span>
<span data-ttu-id="d67ac-117">Этот шаблон hello следующие:</span><span class="sxs-lookup"><span data-stu-id="d67ac-117">This template does hello following:</span></span>

1. <span data-ttu-id="d67ac-118">Развертывает рабочую область службы анализа журналов Azure Service Fabric tooa кластера уже подключен.</span><span class="sxs-lookup"><span data-stu-id="d67ac-118">Deploys an Azure Service Fabric cluster already connected tooa Log Analytics workspace.</span></span> <span data-ttu-id="d67ac-119">У вас есть параметр toocreate hello новую рабочую область при развертывании шаблона hello или имя входного hello уже существующей рабочей области аналитики журналов.</span><span class="sxs-lookup"><span data-stu-id="d67ac-119">You have hello option toocreate a new workspace while deploying hello template, or input hello name of an already existing Log Analytics workspace.</span></span>
2. <span data-ttu-id="d67ac-120">Добавление рабочей области аналитики журналов toohello hello хранилище диагностических данных учетной записи.</span><span class="sxs-lookup"><span data-stu-id="d67ac-120">Adds hello diagnostic storage account toohello Log Analytics workspace.</span></span>
3. <span data-ttu-id="d67ac-121">Позволяет hello Service Fabric решения в рабочей области аналитики журналов.</span><span class="sxs-lookup"><span data-stu-id="d67ac-121">Enables hello Service Fabric solution in your Log Analytics workspace.</span></span>

<span data-ttu-id="d67ac-122">[![Развертывание tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="d67ac-122">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="d67ac-123">После выбора hello развертывать кнопку выше, hello Azure откроется портал с параметрами для вас tooedit.</span><span class="sxs-lookup"><span data-stu-id="d67ac-123">Once you select hello deploy button above, hello Azure portal opens with parameters for you tooedit.</span></span> <span data-ttu-id="d67ac-124">Быть убедиться, что toocreate новую группу ресурсов при вводе имя новой рабочей области аналитики журналов:</span><span class="sxs-lookup"><span data-stu-id="d67ac-124">Be sure toocreate a new resource group if you input a new Log Analytics workspace name:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

<span data-ttu-id="d67ac-127">Примите условия использования hello и нажмите кнопку **создать** toostart hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="d67ac-127">Accept hello legal terms and click **Create** toostart hello deployment.</span></span> <span data-ttu-id="d67ac-128">После завершения развертывания hello должны видеть hello новую рабочую область и создания кластера и hello WADServiceFabric * событий, WADWindowsEventLogs и WADETWEvent добавляемых таблиц:</span><span class="sxs-lookup"><span data-stu-id="d67ac-128">Once hello deployment is completed, you should see hello new workspace and cluster created, and hello WADServiceFabric*Event, WADWindowsEventLogs and WADETWEvent tables added:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace-with-vm-extension-installed"></a><span data-ttu-id="d67ac-130">Развертывание рабочей области аналитики журналов tooa подключения кластера Service Fabric с установлены расширения виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="d67ac-130">Deploy a Service Fabric Cluster connected tooa Log Analytics workspace with VM Extension installed.</span></span>

<span data-ttu-id="d67ac-131">Этот шаблон hello следующие:</span><span class="sxs-lookup"><span data-stu-id="d67ac-131">This template does hello following:</span></span>

1. <span data-ttu-id="d67ac-132">Развертывает рабочую область службы анализа журналов Azure Service Fabric tooa кластера уже подключен.</span><span class="sxs-lookup"><span data-stu-id="d67ac-132">Deploys an Azure Service Fabric cluster already connected tooa Log Analytics workspace.</span></span> <span data-ttu-id="d67ac-133">Вы можете создать новую рабочую область или использовать существующую.</span><span class="sxs-lookup"><span data-stu-id="d67ac-133">You can create a new workspace or use an existing one.</span></span>
2. <span data-ttu-id="d67ac-134">Добавление рабочей области аналитики журналов toohello hello хранилище диагностических данных учетных записей.</span><span class="sxs-lookup"><span data-stu-id="d67ac-134">Adds hello diagnostic storage accounts toohello Log Analytics workspace.</span></span>
3. <span data-ttu-id="d67ac-135">Позволяет hello Service Fabric решения в рабочей области аналитики журналов hello.</span><span class="sxs-lookup"><span data-stu-id="d67ac-135">Enables hello Service Fabric solution in hello Log Analytics workspace.</span></span>
4. <span data-ttu-id="d67ac-136">Устанавливает расширение агента MMA hello в каждый набор кластера Service Fabric масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d67ac-136">Installs hello MMA agent extension in each virtual machine scale set in your Service Fabric cluster.</span></span> <span data-ttu-id="d67ac-137">С установленным агентом MMA hello являются метрики производительности может tooview об узлах.</span><span class="sxs-lookup"><span data-stu-id="d67ac-137">With hello MMA agent installed, you are able tooview performance metrics about your nodes.</span></span>

<span data-ttu-id="d67ac-138">[![Развертывание tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="d67ac-138">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="d67ac-139">Ниже hello же описанные выше шаги, необходимые параметры ввода hello и начнем развертывания.</span><span class="sxs-lookup"><span data-stu-id="d67ac-139">Following hello same steps above, input hello necessary parameters, and kick off a deployment.</span></span> <span data-ttu-id="d67ac-140">Еще раз должен появиться hello новую рабочую область, кластера и все созданные WAD-таблиц:</span><span class="sxs-lookup"><span data-stu-id="d67ac-140">Once again you should see hello new workspace, cluster and WAD tables all created:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a><span data-ttu-id="d67ac-142">Просмотр данных о производительности</span><span class="sxs-lookup"><span data-stu-id="d67ac-142">Viewing Performance Data</span></span>

<span data-ttu-id="d67ac-143">tooview данные о производительности из узлов:</span><span class="sxs-lookup"><span data-stu-id="d67ac-143">tooview Perf Data from your nodes:</span></span>


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- <span data-ttu-id="d67ac-144">Запустите рабочую область службы анализа журналов hello hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d67ac-144">Launch hello Log Analytics workspace from hello Azure portal.</span></span>
  <span data-ttu-id="d67ac-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span><span class="sxs-lookup"><span data-stu-id="d67ac-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span></span>
- <span data-ttu-id="d67ac-146">Перейдите на левой панели hello tooSettings и выбрать данные >> счетчиков производительности Windows >> «hello добавить выбранные счетчики производительности»: ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span><span class="sxs-lookup"><span data-stu-id="d67ac-146">Go tooSettings on hello left pane, and select Data >> Windows Performance Counters >> "Add hello selected performance counters": ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span></span>
- <span data-ttu-id="d67ac-147">В поиске по журналам используйте следующие запросы toodelve в основных метрик о узлы hello:</span><span class="sxs-lookup"><span data-stu-id="d67ac-147">In Log Search, use hello following queries toodelve into key metrics about your nodes:</span></span>

    <span data-ttu-id="d67ac-148">а.</span><span class="sxs-lookup"><span data-stu-id="d67ac-148">a.</span></span> <span data-ttu-id="d67ac-149">Сравнение hello среднее использование ЦП для всех узлов, в последний час toosee hello какие узлы в случае возникновения проблем и какие интервалом узла имели пик.</span><span class="sxs-lookup"><span data-stu-id="d67ac-149">Compare hello average CPU Utilization across all your nodes in hello last one hour toosee which nodes are having issues and at what time interval a node had a spike:</span></span>

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    <span data-ttu-id="d67ac-151">b.</span><span class="sxs-lookup"><span data-stu-id="d67ac-151">b.</span></span> <span data-ttu-id="d67ac-152">Просмотрите аналогичные графики для доступной памяти на каждом узле, используя этот запрос:</span><span class="sxs-lookup"><span data-stu-id="d67ac-152">View similar line charts for available memory on each node with this query:</span></span>

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    <span data-ttu-id="d67ac-153">tooview список всех узлов, показывающая hello точное среднее значение для доступно МБ для каждого узла, используется следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="d67ac-153">tooview a listing of all your nodes, showing hello exact average value for Available MBytes for each node, use this query:</span></span>

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    <span data-ttu-id="d67ac-155">c.</span><span class="sxs-lookup"><span data-stu-id="d67ac-155">c.</span></span> <span data-ttu-id="d67ac-156">В случае hello требуется toodrill работу в определенном узле изучив hello почасовой среднее минимальное, максимальное и 75 процентиля ЦП, вы могли toodo это по с помощью этого запроса (замените поле компьютера):</span><span class="sxs-lookup"><span data-stu-id="d67ac-156">In hello case that you want toodrill down into a specific node by examining hello hourly average, minimum, maximum and 75-percentile CPU usage, you're able toodo this by using this query (replace Computer field):</span></span>

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

<span data-ttu-id="d67ac-158">Дополнительные сведения о метриках производительности в службе анализа журналов на hello [Operations Management Suite блог](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span><span class="sxs-lookup"><span data-stu-id="d67ac-158">Read more information about performance metrics in Log Analytics at hello [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span></span>


## <a name="adding-an-existing-storage-account-toolog-analytics"></a><span data-ttu-id="d67ac-159">Добавление существующей учетной записи хранилища tooLog аналитика</span><span class="sxs-lookup"><span data-stu-id="d67ac-159">Adding an existing storage account tooLog Analytics</span></span>

<span data-ttu-id="d67ac-160">Этот шаблон просто добавляет существующего хранилища учетных записей tooa новый или существующий анализа журналов рабочей области.</span><span class="sxs-lookup"><span data-stu-id="d67ac-160">This template simply adds your existing storage accounts tooa new or existing Log Analytics workspace.</span></span>

<span data-ttu-id="d67ac-161">[![Развертывание tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="d67ac-161">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span></span>

> [!NOTE]
> <span data-ttu-id="d67ac-162">При работе с уже существующей рабочей области аналитики журналов выбора группы ресурсов, выберите «Использовать существующее» и выполните поиск hello группы ресурсов, содержащий рабочей областью аналитики журналов hello.</span><span class="sxs-lookup"><span data-stu-id="d67ac-162">In selecting a Resource Group, if you're working with an already existing Log Analytics workspace, select "Use Existing" and search for hello resource group containing hello Log Analytics workspace.</span></span> <span data-ttu-id="d67ac-163">В противном случае создайте новую.</span><span class="sxs-lookup"><span data-stu-id="d67ac-163">Create a new one if otherwise.</span></span>
> <span data-ttu-id="d67ac-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span><span class="sxs-lookup"><span data-stu-id="d67ac-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span></span>
>
>

<span data-ttu-id="d67ac-165">После развертывания этот шаблон можно будет toosee hello хранения подключена учетная запись tooyour анализа журналов рабочей области.</span><span class="sxs-lookup"><span data-stu-id="d67ac-165">After this template has been deployed, you will be able toosee hello storage account connected tooyour Log Analytics workspace.</span></span> <span data-ttu-id="d67ac-166">В этом случае добавлены один Дополнительные хранилища учетной записи toohello Exchange рабочей области, созданной выше.</span><span class="sxs-lookup"><span data-stu-id="d67ac-166">In this instance, I added one more storage account toohello Exchange workspace I created above.</span></span>
<span data-ttu-id="d67ac-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span><span class="sxs-lookup"><span data-stu-id="d67ac-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span></span>

## <a name="view-service-fabric-events"></a><span data-ttu-id="d67ac-168">Просмотр событий Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d67ac-168">View Service Fabric events</span></span>

<span data-ttu-id="d67ac-169">После завершения развертывания hello и включил hello Service Fabric решения в рабочей области, выберите hello **Service Fabric** плитки на панели мониторинга портала toolaunch hello hello анализа журналов Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d67ac-169">Once hello deployments are completed and hello Service Fabric solution has been enabled in your workspace, select hello **Service Fabric** tile in hello Log Analytics portal toolaunch hello Service Fabric dashboard.</span></span> <span data-ttu-id="d67ac-170">панель мониторинга Hello, включает столбцы hello hello в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="d67ac-170">hello dashboard includes hello columns in hello following table.</span></span> <span data-ttu-id="d67ac-171">Каждый столбец перечислены hello top 10 событий, сопоставляя count, критерии столбца для hello указанный диапазон времени.</span><span class="sxs-lookup"><span data-stu-id="d67ac-171">Each column lists hello top 10 events by count matching that column's criteria for hello specified time range.</span></span> <span data-ttu-id="d67ac-172">Можно выполнить поиск журнала, который предоставляет hello весь список, щелкнув **все** hello справа внизу каждого столбца или щелкните заголовок столбца hello.</span><span class="sxs-lookup"><span data-stu-id="d67ac-172">You can run a log search that provides hello entire list by clicking **See all** at hello right bottom of each column, or by clicking hello column header.</span></span>

| <span data-ttu-id="d67ac-173">**Событие Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="d67ac-173">**Service Fabric event**</span></span> | <span data-ttu-id="d67ac-174">**description**</span><span class="sxs-lookup"><span data-stu-id="d67ac-174">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="d67ac-175">Важные проблемы</span><span class="sxs-lookup"><span data-stu-id="d67ac-175">Notable Issues</span></span> |<span data-ttu-id="d67ac-176">Отображение таких проблем, как сбои и отмены RunAsync, а также отключение узлов.</span><span class="sxs-lookup"><span data-stu-id="d67ac-176">A Display of issues such as RunAsyncFailures RunAsynCancellations and Node Downs.</span></span> |
| <span data-ttu-id="d67ac-177">Операционные события</span><span class="sxs-lookup"><span data-stu-id="d67ac-177">Operational Events</span></span> |<span data-ttu-id="d67ac-178">Важные операционные события, такие как обновление и развертывание приложения.</span><span class="sxs-lookup"><span data-stu-id="d67ac-178">Notable operational events such as application upgrade and deployments.</span></span> |
| <span data-ttu-id="d67ac-179">События надежных служб</span><span class="sxs-lookup"><span data-stu-id="d67ac-179">Reliable Service Events</span></span> |<span data-ttu-id="d67ac-180">Важные события надежных служб, например вызовы RunAsync.</span><span class="sxs-lookup"><span data-stu-id="d67ac-180">Notable reliable service events such a Runasyncinvocations.</span></span> |
| <span data-ttu-id="d67ac-181">События субъектов</span><span class="sxs-lookup"><span data-stu-id="d67ac-181">Actor Events</span></span> |<span data-ttu-id="d67ac-182">Важные события субъектов, создаваемые микрослужбами, например исключения, вызываемые методом субъекта, включения и отключения субъекта и т. д.</span><span class="sxs-lookup"><span data-stu-id="d67ac-182">Notable actor events generated by your micro-services, such as exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="d67ac-183">События приложений</span><span class="sxs-lookup"><span data-stu-id="d67ac-183">Application Events</span></span> |<span data-ttu-id="d67ac-184">Все пользовательские события ETW, создаваемые приложениями.</span><span class="sxs-lookup"><span data-stu-id="d67ac-184">All custom ETW events generated by your applications.</span></span> |

![Панель мониторинга Service Fabric](./media/log-analytics-service-fabric/sf3.png)

![Панель мониторинга Service Fabric](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="d67ac-187">Hello ниже приведены методы сбора данных и другие сведения о сборе данных для Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d67ac-187">hello following table shows data collection methods and other details about how data is collected for Service Fabric.</span></span>

| <span data-ttu-id="d67ac-188">платформа</span><span class="sxs-lookup"><span data-stu-id="d67ac-188">platform</span></span> | <span data-ttu-id="d67ac-189">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="d67ac-189">Direct Agent</span></span> | <span data-ttu-id="d67ac-190">Агент Operations Manager</span><span class="sxs-lookup"><span data-stu-id="d67ac-190">Operations Manager agent</span></span> | <span data-ttu-id="d67ac-191">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="d67ac-191">Azure Storage</span></span> | <span data-ttu-id="d67ac-192">Нужен ли Operations Manager?</span><span class="sxs-lookup"><span data-stu-id="d67ac-192">Operations Manager required?</span></span> | <span data-ttu-id="d67ac-193">Отправка данных агента Operations Manager через группу управления</span><span class="sxs-lookup"><span data-stu-id="d67ac-193">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="d67ac-194">частота сбора</span><span class="sxs-lookup"><span data-stu-id="d67ac-194">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="d67ac-195">Windows</span><span class="sxs-lookup"><span data-stu-id="d67ac-195">Windows</span></span> |  |  | <span data-ttu-id="d67ac-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="d67ac-196">&#8226;</span></span> |  |  |<span data-ttu-id="d67ac-197">10 минут</span><span class="sxs-lookup"><span data-stu-id="d67ac-197">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="d67ac-198">Область hello этих событий в hello Service Fabric решения можно изменить, щелкнув **данные основаны на последних 7 дней** hello верхней части панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="d67ac-198">You can change hello scope of these events in hello Service Fabric solution by clicking **Data based on last 7 days** at hello top of hello dashboard.</span></span> <span data-ttu-id="d67ac-199">Также можно показать события, создаваемые в hello последние семь дней, один день или 6 часов.</span><span class="sxs-lookup"><span data-stu-id="d67ac-199">You can also show events generated within hello last seven days, one day, or six hours.</span></span> <span data-ttu-id="d67ac-200">Или можно выбрать **пользовательские** toospecify пользовательского диапазона дат.</span><span class="sxs-lookup"><span data-stu-id="d67ac-200">Or, you can select **Custom** toospecify a custom date range.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="d67ac-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d67ac-201">Next steps</span></span>

* <span data-ttu-id="d67ac-202">Используйте [поиска журналов в службе анализа журналов](log-analytics-log-searches.md) tooview подробные данные о событиях Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d67ac-202">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Service Fabric event data.</span></span>
