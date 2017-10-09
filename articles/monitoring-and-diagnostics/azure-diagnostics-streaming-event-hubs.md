---
title: "данные диагностики Azure в hello Горячий путь с помощью концентраторов событий aaaStreaming | Документы Microsoft"
description: "Настройку диагностики Azure с концентраторами событий последний tooend, включая руководство для распространенных сценариев."
services: event-hubs
documentationcenter: na
author: rboucher
manager: carmonm
editor: 
ms.assetid: edeebaac-1c47-4b43-9687-f28e7e1e446a
ms.service: monitoring-and-diagnostics
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: robb
ms.openlocfilehash: a2528ddd0688d1c23a8631e769ca016dd79e4159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-azure-diagnostics-data-in-hello-hot-path-by-using-event-hubs"></a><span data-ttu-id="a387e-103">Потоковая передача данных диагностики Azure в hello Горячий путь с помощью концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="a387e-103">Streaming Azure Diagnostics data in hello hot path by using Event Hubs</span></span>
<span data-ttu-id="a387e-104">Диагностика Azure предоставляет гибкие возможности toocollect метрики и журналов из облачных служб виртуальных машин (ВМ) и передачи результатов tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="a387e-104">Azure Diagnostics provides flexible ways toocollect metrics and logs from cloud services virtual machines (VMs) and transfer results tooAzure Storage.</span></span> <span data-ttu-id="a387e-105">Начиная с версии hello марта 2016 г. (SDK 2.9) временные рамки, можно отправить toocustom диагностики источники данных и передачи данных Горячий путь в секундах с помощью [концентраторов событий Azure](https://azure.microsoft.com/services/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="a387e-105">Starting in hello March 2016 (SDK 2.9) time frame, you can send Diagnostics toocustom data sources and transfer hot path data in seconds by using [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span>

<span data-ttu-id="a387e-106">Поддерживаемые типы данных включают:</span><span class="sxs-lookup"><span data-stu-id="a387e-106">Supported data types include:</span></span>

* <span data-ttu-id="a387e-107">Трассировка событий Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="a387e-107">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="a387e-108">Счетчики производительности</span><span class="sxs-lookup"><span data-stu-id="a387e-108">Performance counters</span></span>
* <span data-ttu-id="a387e-109">Журналы событий Windows</span><span class="sxs-lookup"><span data-stu-id="a387e-109">Windows event logs</span></span>
* <span data-ttu-id="a387e-110">Журналы приложений</span><span class="sxs-lookup"><span data-stu-id="a387e-110">Application logs</span></span>
* <span data-ttu-id="a387e-111">Журналы инфраструктуры системы диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="a387e-111">Azure Diagnostics infrastructure logs</span></span>

<span data-ttu-id="a387e-112">В этой статье рассказывается о том, tooconfigure диагностики Azure с концентраторами событий из конечного tooend.</span><span class="sxs-lookup"><span data-stu-id="a387e-112">This article shows you how tooconfigure Azure Diagnostics with Event Hubs from end tooend.</span></span> <span data-ttu-id="a387e-113">Также описаны следующие распространенные сценарии hello:</span><span class="sxs-lookup"><span data-stu-id="a387e-113">Guidance is also provided for hello following common scenarios:</span></span>

* <span data-ttu-id="a387e-114">Каким образом ведет журнал toocustomize hello и метрики, которые отправляются tooEvent концентраторы</span><span class="sxs-lookup"><span data-stu-id="a387e-114">How toocustomize hello logs and metrics that get sent tooEvent Hubs</span></span>
* <span data-ttu-id="a387e-115">Как toochange конфигураций в каждой среде</span><span class="sxs-lookup"><span data-stu-id="a387e-115">How toochange configurations in each environment</span></span>
* <span data-ttu-id="a387e-116">Как концентраторы событий tooview поток данных</span><span class="sxs-lookup"><span data-stu-id="a387e-116">How tooview Event Hubs stream data</span></span>
* <span data-ttu-id="a387e-117">Как tootroubleshoot hello подключения</span><span class="sxs-lookup"><span data-stu-id="a387e-117">How tootroubleshoot hello connection</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="a387e-118">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a387e-118">Prerequisites</span></span>
<span data-ttu-id="a387e-119">Данные receieving концентраторов событий из системы диагностики Azure поддерживаются в облачных служб, виртуальных машин, наборы масштабирования виртуальных машин и Service Fabric, начиная с Azure SDK 2.9 hello и hello соответствующий средства Azure для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a387e-119">Event Hubs receieving data from Azure Diagnostics is supported in Cloud Services, VMs, Virtual Machine Scale Sets, and Service Fabric starting in hello Azure SDK 2.9 and hello corresponding Azure Tools for Visual Studio.</span></span>

* <span data-ttu-id="a387e-120">Расширение системы диагностики Azure версии 1.6 (в[пакете SDK для Azure для .NET 2.9 или более поздней версии](https://azure.microsoft.com/downloads/) оно используется по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="a387e-120">Azure Diagnostics extension 1.6 ([Azure SDK for .NET 2.9 or later](https://azure.microsoft.com/downloads/) targets this by default)</span></span>
* [<span data-ttu-id="a387e-121">Visual Studio 2013 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="a387e-121">Visual Studio 2013 or later</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="a387e-122">Существующие конфигурации диагностики Azure в приложении с помощью *.wadcfgx* файл и один из следующих методов hello:</span><span class="sxs-lookup"><span data-stu-id="a387e-122">Existing configurations of Azure Diagnostics in an application by using a *.wadcfgx* file and one of hello following methods:</span></span>
  * <span data-ttu-id="a387e-123">Visual Studio: [настройка системы диагностики для облачных служб и виртуальных машин Azure](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span><span class="sxs-lookup"><span data-stu-id="a387e-123">Visual Studio: [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span></span>
  * <span data-ttu-id="a387e-124">Windows PowerShell: [включение диагностики в облачных службах Azure с помощью PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="a387e-124">Windows PowerShell: [Enable diagnostics in Azure Cloud Services using PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span></span>
* <span data-ttu-id="a387e-125">Пространство имен концентраторов событий подготовлены для статьи hello [приступить к работе с концентраторами событий](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="a387e-125">Event Hubs namespace provisioned per hello article, [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span></span>

## <a name="connect-azure-diagnostics-tooevent-hubs-sink"></a><span data-ttu-id="a387e-126">Подключение приемника концентраторов tooEvent диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="a387e-126">Connect Azure Diagnostics tooEvent Hubs sink</span></span>
<span data-ttu-id="a387e-127">По умолчанию диагностики Azure всегда отправляет журналы и показатели tooan учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="a387e-127">By default, Azure Diagnostics always sends logs and metrics tooan Azure Storage account.</span></span> <span data-ttu-id="a387e-128">Приложения также могут отправлять данные tooEvent концентраторов путем добавления нового **приемники** "раздела" hello **PublicConfig** / **WadCfg** элемент hello *.wadcfgx* файла.</span><span class="sxs-lookup"><span data-stu-id="a387e-128">An application may also send data tooEvent Hubs by adding a new **Sinks** section under hello **PublicConfig** / **WadCfg** element of hello *.wadcfgx* file.</span></span> <span data-ttu-id="a387e-129">В Visual Studio hello *.wadcfgx* файл хранится в пути hello: **проекта облачной службы** > **ролей** > **() RoleName)** > **diagnostics.wadcfgx** файла.</span><span class="sxs-lookup"><span data-stu-id="a387e-129">In Visual Studio, hello *.wadcfgx* file is stored in hello following path: **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx** file.</span></span>

```xml
<SinksConfig>
  <Sink name="HotPath">
    <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" />
  </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "HotPath",
            "EventHub": {
                "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
                "SharedAccessKeyName": "SendRule"
            }
        }
    ]
}
```

<span data-ttu-id="a387e-130">В этом примере URL-адрес имеет значение toohello полностью концентратора событий hello полное пространство имен концентратора событий hello: пространство имен концентраторов событий + «/» + имя концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="a387e-130">In this example, hello event hub URL is set toohello fully qualified namespace of hello event hub: Event Hubs namespace  + "/" + event hub name.</span></span>  

<span data-ttu-id="a387e-131">URL-адрес отображается в hello концентратора событий Hello [портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885) на панели мониторинга hello концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="a387e-131">hello event hub URL is displayed in hello [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) on hello Event Hubs dashboard.</span></span>  

<span data-ttu-id="a387e-132">Hello **приемника** имя можно задать допустимую строку tooany при условии, что hello одинаковое значение согласованно используется в файле конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="a387e-132">hello **Sink** name can be set tooany valid string as long as hello same value is used consistently throughout hello config file.</span></span>

> [!NOTE]
> <span data-ttu-id="a387e-133">В этом разделе могут быть настроены дополнительные приемники, например *applicationInsights* .</span><span class="sxs-lookup"><span data-stu-id="a387e-133">There may be additional sinks, such as *applicationInsights* configured in this section.</span></span> <span data-ttu-id="a387e-134">Система диагностики Azure позволяет одному или более приемники определено, если каждый приемник также объявляется в hello toobe **PrivateConfig** раздела.</span><span class="sxs-lookup"><span data-stu-id="a387e-134">Azure Diagnostics allows one or more sinks toobe defined if each sink is also declared in hello **PrivateConfig** section.</span></span>  
>
>

<span data-ttu-id="a387e-135">Hello концентраторов событий приемник должен также быть объявляются и определяются в hello **PrivateConfig** раздел hello *.wadcfgx* файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a387e-135">hello Event Hubs sink must also be declared and defined in hello **PrivateConfig** section of hello *.wadcfgx* config file.</span></span>

```XML
<PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <StorageAccount name="{account name}" key="{account key}" endpoint="{optional storage endpoint}" />
  <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
</PrivateConfig>
```
```JSON
{
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{optional storage endpoint}",
    "EventHub": {
        "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    }
}
```

<span data-ttu-id="a387e-136">Hello `SharedAccessKeyName` значение должно соответствовать ключ подписи общего доступа (SAS) и политики, который был определен в hello **концентраторов событий** пространства имен.</span><span class="sxs-lookup"><span data-stu-id="a387e-136">hello `SharedAccessKeyName` value must match a Shared Access Signature (SAS) key and policy that has been defined in hello **Event Hubs** namespace.</span></span> <span data-ttu-id="a387e-137">Обзор панели мониторинга концентраторов событий toohello в hello [портал Azure](https://manage.windowsazure.com), щелкните hello **Настройка** вкладку и настроить именованной политики (например, «SendRule»), который имеет *отправки* разрешения.</span><span class="sxs-lookup"><span data-stu-id="a387e-137">Browse toohello Event Hubs dashboard in hello [Azure portal](https://manage.windowsazure.com), click hello **Configure** tab, and set up a named policy (for example, "SendRule") that has *Send* permissions.</span></span> <span data-ttu-id="a387e-138">Hello **StorageAccount** также объявляется в **PrivateConfig**.</span><span class="sxs-lookup"><span data-stu-id="a387e-138">hello **StorageAccount** is also declared in **PrivateConfig**.</span></span> <span data-ttu-id="a387e-139">Нет необходимости toochange значения, если они работают.</span><span class="sxs-lookup"><span data-stu-id="a387e-139">There is no need toochange values here if they are working.</span></span> <span data-ttu-id="a387e-140">В этом примере мы оставьте hello значения пустой, это знак, подчиненных активов будет устанавливать значения hello.</span><span class="sxs-lookup"><span data-stu-id="a387e-140">In this example, we leave hello values empty, which is a sign that a downstream asset will set hello values.</span></span> <span data-ttu-id="a387e-141">Например, hello *ServiceConfiguration.Cloud.cscfg* файла конфигурации среды задает имена неподходящей среде hello и ключи.</span><span class="sxs-lookup"><span data-stu-id="a387e-141">For example, hello *ServiceConfiguration.Cloud.cscfg* environment configuration file sets hello environment-appropriate names and keys.</span></span>  

> [!WARNING]
> <span data-ttu-id="a387e-142">ключ SAS концентраторов событий Hello хранится в виде обычного текста в hello *.wadcfgx* файла.</span><span class="sxs-lookup"><span data-stu-id="a387e-142">hello Event Hubs SAS key is stored in plain text in hello *.wadcfgx* file.</span></span> <span data-ttu-id="a387e-143">Часто этот ключ возврата системы управления версиями toosource или доступна как ресурс в ваш сервер сборки, поэтому его следует защитить соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="a387e-143">Often, this key is checked in toosource code control or is available as an asset in your build server, so you should protect it as appropriate.</span></span> <span data-ttu-id="a387e-144">Рекомендуется использовать ключ SAS с *только отправку* разрешения таким образом, пользователь-злоумышленник может записи toohello концентратора событий, но не прослушивания tooit или управлять им.</span><span class="sxs-lookup"><span data-stu-id="a387e-144">We recommend that you use a SAS key here with *Send only* permissions so that a malicious user can write toohello event hub, but not listen tooit or manage it.</span></span>
>
>

## <a name="configure-azure-diagnostics-toosend-logs-and-metrics-tooevent-hubs"></a><span data-ttu-id="a387e-145">Настройка системы диагностики Azure toosend журналы и показатели tooEvent концентраторы</span><span class="sxs-lookup"><span data-stu-id="a387e-145">Configure Azure Diagnostics toosend logs and metrics tooEvent Hubs</span></span>
<span data-ttu-id="a387e-146">Как отмечалось ранее, все по умолчанию и пользовательские диагностические данные, то есть метрики и журналов, автоматически отправляется tooAzure хранилища в интервалах hello настроен.</span><span class="sxs-lookup"><span data-stu-id="a387e-146">As discussed previously, all default and custom diagnostics data, that is, metrics and logs, is automatically sent tooAzure Storage in hello configured intervals.</span></span> <span data-ttu-id="a387e-147">С концентраторами событий и любой дополнительный приемник можно указать любой корневой или конечный узел в toobe иерархии hello отправлено toohello концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="a387e-147">With Event Hubs and any additional sink, you can specify any root or leaf node in hello hierarchy toobe sent toohello event hub.</span></span> <span data-ttu-id="a387e-148">К этим данным относятся события трассировки Windows, счетчики производительности, журналы событий Windows и журналы приложений.</span><span class="sxs-lookup"><span data-stu-id="a387e-148">This includes ETW events, performance counters, Windows event logs, and application logs.</span></span>   

<span data-ttu-id="a387e-149">Очень важно, передача концентраторов tooEvent tooconsider следует количества точек данных.</span><span class="sxs-lookup"><span data-stu-id="a387e-149">It is important tooconsider how many data points should actually be transferred tooEvent Hubs.</span></span> <span data-ttu-id="a387e-150">Обычно разработчики передают по критическому пути с низкой задержкой данные, которые должны быть быстро использованы и интерпретированы.</span><span class="sxs-lookup"><span data-stu-id="a387e-150">Typically, developers transfer low-latency hot-path data that must be consumed and interpreted quickly.</span></span> <span data-ttu-id="a387e-151">Примерами являются системы, отслеживающие предупреждения, или правила автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="a387e-151">Systems that monitor alerts or autoscale rules are examples.</span></span> <span data-ttu-id="a387e-152">Разработчик также может настроить альтернативное хранилище данных анализа или поиска, например, Stream Analytics, ElasticSearch, пользовательской системы мониторинга или сторонней системы мониторинга, которую вы предпочитаете.</span><span class="sxs-lookup"><span data-stu-id="a387e-152">A developer might also configure an alternate analysis store or search store -- for example, Azure Stream Analytics, Elasticsearch, a custom monitoring system, or a favorite monitoring system from others.</span></span>

<span data-ttu-id="a387e-153">Hello ниже приведены некоторые примеры конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a387e-153">hello following are some example configurations.</span></span>

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "sinks": "HotPath",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        }
    ]
}
```

<span data-ttu-id="a387e-154">В приведенном выше примере hello, hello приемник является родительским примененных toohello **PerformanceCounters** узла в иерархии hello, что означает все дочерние **PerformanceCounters** будут отправляться tooEvent концентраторов.</span><span class="sxs-lookup"><span data-stu-id="a387e-154">In hello above example, hello sink is applied toohello parent **PerformanceCounters** node in hello hierarchy, which means all child **PerformanceCounters** will be sent tooEvent Hubs.</span></span>  

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" sinks="HotPath" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" sinks="HotPath"/>
  <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" sinks="HotPath"/>
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Rejected",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Queued",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        }
    ]
}
```

<span data-ttu-id="a387e-155">В предыдущем примере hello hello приемник является три счетчика примененных tooonly: **запросов в очереди**, **отклонение запросов**, и **% загруженности процессора**.</span><span class="sxs-lookup"><span data-stu-id="a387e-155">In hello previous example, hello sink is applied tooonly three counters: **Requests Queued**, **Requests Rejected**, and **% Processor time**.</span></span>  

<span data-ttu-id="a387e-156">Hello следующем примере показано, как разработчик может ограничить hello объем отправляемых данных toobe hello важные метрики, используемые для этой службы работоспособности.</span><span class="sxs-lookup"><span data-stu-id="a387e-156">hello following example shows how a developer can limit hello amount of sent data toobe hello critical metrics that are used for this service’s health.</span></span>  

```XML
<Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
```
```JSON
"Logs": {
    "scheduledTransferPeriod": "PT1M",
    "scheduledTransferLogLevelFilter": "Error",
    "sinks": "HotPath"
}
```

<span data-ttu-id="a387e-157">В этом примере hello приемник примененных toologs который отфильтрованный только tooerror уровня трассировки.</span><span class="sxs-lookup"><span data-stu-id="a387e-157">In this example, hello sink is applied toologs and is filtered only tooerror level trace.</span></span>

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a><span data-ttu-id="a387e-158">Развертывание и обновление приложения облачной службы и конфигурации системы диагностики</span><span class="sxs-lookup"><span data-stu-id="a387e-158">Deploy and update a Cloud Services application and diagnostics config</span></span>
<span data-ttu-id="a387e-159">Visual Studio предоставляет hello самый простой путь toodeploy hello приложения и конфигурации приемника концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="a387e-159">Visual Studio provides hello easiest path toodeploy hello application and Event Hubs sink configuration.</span></span> <span data-ttu-id="a387e-160">hello tooview и измените файл, открыть hello *.wadcfgx* файла в Visual Studio, измените его и сохранить его.</span><span class="sxs-lookup"><span data-stu-id="a387e-160">tooview and edit hello file, open hello *.wadcfgx* file in Visual Studio, edit it, and save it.</span></span> <span data-ttu-id="a387e-161">путь Hello **проекта облачной службы** > **ролей** > **(RoleName)** > **diagnostics.wadcfgx**.</span><span class="sxs-lookup"><span data-stu-id="a387e-161">hello path is **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx**.</span></span>  

<span data-ttu-id="a387e-162">На этом этапе все и развертывания обновление действий в Visual Studio, Visual Studio Team System и всех команд или сценариев, которые основаны на MSBuild и использовать hello **/t: публикация** целевой включают hello *.wadcfgx*  в процессе обработки пакетов hello.</span><span class="sxs-lookup"><span data-stu-id="a387e-162">At this point, all deployment and deployment update actions in Visual Studio, Visual Studio Team System, and all commands or scripts that are based on MSBuild and use hello **/t:publish** target include hello *.wadcfgx* in hello packaging process.</span></span> <span data-ttu-id="a387e-163">Кроме того развертывания и обновления развертывание hello tooAzure файла с помощью hello соответствующее расширение агента диагностики Azure на виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="a387e-163">In addition, deployments and updates deploy hello file tooAzure by using hello appropriate Azure Diagnostics agent extension on your VMs.</span></span>

<span data-ttu-id="a387e-164">После развертывания приложения hello и конфигурации системы диагностики Azure будет сразу же видеть действия на панели мониторинга hello hello концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="a387e-164">After you deploy hello application and Azure Diagnostics configuration, you will immediately see activity in hello dashboard of hello event hub.</span></span> <span data-ttu-id="a387e-165">Это означает, что вы будете готовы toomove на tooviewing hello-path данных hello прослушивателя клиента или анализа средство по вашему выбору.</span><span class="sxs-lookup"><span data-stu-id="a387e-165">This indicates that you're ready toomove on tooviewing hello hot-path data in hello listener client or analysis tool of your choice.</span></span>  

<span data-ttu-id="a387e-166">Следующий рисунок hello hello концентраторов событий мониторинга представлен работоспособное отправку диагностики данных toohello события концентратора запуск через некоторое время после 23: 00.</span><span class="sxs-lookup"><span data-stu-id="a387e-166">In hello following figure, hello Event Hubs dashboard shows healthy sending of diagnostics data toohello event hub starting sometime after 11 PM.</span></span> <span data-ttu-id="a387e-167">Это время hello приложение было развернуто с обновленной *.wadcfgx* файла и hello приемника был настроен должным образом.</span><span class="sxs-lookup"><span data-stu-id="a387e-167">That's when hello application was deployed with an updated *.wadcfgx* file, and hello sink was configured properly.</span></span>

![][0]  

> [!NOTE]
> <span data-ttu-id="a387e-168">При внесении toohello обновлений для файла конфигурации диагностики Azure (.wadcfgx), рекомендуется push hello обновления toohello всего приложения, а также hello конфигурации с помощью публикации Visual Studio или сценарий Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a387e-168">When you make updates toohello Azure Diagnostics config file (.wadcfgx), it's recommended that you push hello updates toohello entire application as well as hello configuration by using either Visual Studio publishing, or a Windows PowerShell script.</span></span>  
>
>

## <a name="view-hot-path-data"></a><span data-ttu-id="a387e-169">Просмотр данных, передаваемых по критическому пути</span><span class="sxs-lookup"><span data-stu-id="a387e-169">View hot-path data</span></span>
<span data-ttu-id="a387e-170">Как отмечалось ранее, существует множество вариантов использования для прослушивания tooand обработки данных для концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="a387e-170">As discussed previously, there are many use cases for listening tooand processing Event Hubs data.</span></span>

<span data-ttu-id="a387e-171">Один простой подход — toocreate небольшую тестовую консольного приложения toolisten toohello концентратора событий и Здравствуй, мир выходной поток.</span><span class="sxs-lookup"><span data-stu-id="a387e-171">One simple approach is toocreate a small test console application toolisten toohello event hub and print hello output stream.</span></span> <span data-ttu-id="a387e-172">Можно поместить следующий код, который является более подробно в hello [приступить к работе с концентраторами событий](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), в консольном приложении.</span><span class="sxs-lookup"><span data-stu-id="a387e-172">You can place hello following code, which is explained in more detail in [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in a console application.</span></span>  

<span data-ttu-id="a387e-173">Обратите внимание, что консольное приложение hello должен включать hello [пакет NuGet узел обработчика событий](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="a387e-173">Note that hello console application must include hello [Event Processor Host NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>  

<span data-ttu-id="a387e-174">Запомнить tooreplace значения hello в угловые скобки в hello **Main** функция со значениями для ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a387e-174">Remember tooreplace hello values in angle brackets in hello **Main** function with values for your resources.</span></span>   

```csharp
//Console application code for EventHub test client
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.ServiceBus.Messaging;

namespace EventHubListener
{
    class SimpleEventProcessor : IEventProcessor
    {
        Stopwatch checkpointStopWatch;

        async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
            if (reason == CloseReason.Shutdown)
            {
                await context.CheckpointAsync();
            }
        }

        Task IEventProcessor.OpenAsync(PartitionContext context)
        {
            Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
            this.checkpointStopWatch = new Stopwatch();
            this.checkpointStopWatch.Start();
            return Task.FromResult<object>(null);
        }

        async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (EventData eventData in messages)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                    Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                        context.Lease.PartitionId, data));

                foreach (var x in eventData.Properties)
                {
                    Console.WriteLine(string.Format("    {0} = {1}", x.Key, x.Value));
                }
            }

            //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
            if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
            {
                await context.CheckpointAsync();
                this.checkpointStopWatch.Restart();
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string eventHubConnectionString = "Endpoint= <your connection string>”
            string eventHubName = "<Event hub name>";
            string storageAccountName = "<Storage account name>";
            string storageAccountKey = "<Storage account key>”;
            string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);

            string eventProcessorHostName = Guid.NewGuid().ToString();
            EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
            Console.WriteLine("Registering EventProcessor...");
            var options = new EventProcessorOptions();
            options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
            eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();

            Console.WriteLine("Receiving. Press enter key toostop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a><span data-ttu-id="a387e-175">Устранение неполадок приемников концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="a387e-175">Troubleshoot Event Hubs sinks</span></span>
* <span data-ttu-id="a387e-176">концентратор событий Hello не показывает активность входящих или исходящих событий должным образом.</span><span class="sxs-lookup"><span data-stu-id="a387e-176">hello event hub does not show incoming or outgoing event activity as expected.</span></span>

    <span data-ttu-id="a387e-177">Убедитесь в том, что концентратор событий успешно подготовлен.</span><span class="sxs-lookup"><span data-stu-id="a387e-177">Check that your event hub is successfully provisioned.</span></span> <span data-ttu-id="a387e-178">Все сведения о соединении в hello **PrivateConfig** раздел *.wadcfgx* должна соответствовать значениям hello ресурса, как показано на портале hello.</span><span class="sxs-lookup"><span data-stu-id="a387e-178">All connection info in hello **PrivateConfig** section of *.wadcfgx* must match hello values of your resource as seen in hello portal.</span></span> <span data-ttu-id="a387e-179">Убедитесь, что SAS политики определен («SendRule» в примере hello) в hello портала и что *отправки* разрешение.</span><span class="sxs-lookup"><span data-stu-id="a387e-179">Make sure that you have a SAS policy defined ("SendRule" in hello example) in hello portal and that *Send* permission is granted.</span></span>  
* <span data-ttu-id="a387e-180">После обновления концентратора событий hello перестал активности входящих или исходящих событий.</span><span class="sxs-lookup"><span data-stu-id="a387e-180">After an update, hello event hub no longer shows incoming or outgoing event activity.</span></span>

    <span data-ttu-id="a387e-181">Во-первых, убедитесь, что этот концентратор событий hello и сведения о конфигурации указано правильно, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="a387e-181">First, make sure that hello event hub and configuration info is correct as explained previously.</span></span> <span data-ttu-id="a387e-182">Здравствуйте, иногда **PrivateConfig** сбрасывается в обновлении развертывания.</span><span class="sxs-lookup"><span data-stu-id="a387e-182">Sometimes hello **PrivateConfig** is reset in a deployment update.</span></span> <span data-ttu-id="a387e-183">Hello рекомендуется исправить, все изменения слишком toomake*.wadcfgx* в hello проект и затем отправить обновления завершения приложения.</span><span class="sxs-lookup"><span data-stu-id="a387e-183">hello recommended fix is toomake all changes too*.wadcfgx* in hello project and then push a complete application update.</span></span> <span data-ttu-id="a387e-184">Если это невозможно, убедитесь, что это обновление диагностики hello помещает полный **PrivateConfig** , включающего hello ключ SAS.</span><span class="sxs-lookup"><span data-stu-id="a387e-184">If this is not possible, make sure that hello diagnostics update pushes a complete **PrivateConfig** that includes hello SAS key.</span></span>  
* <span data-ttu-id="a387e-185">Я попытался предложения hello и hello концентратора событий по-прежнему не работает.</span><span class="sxs-lookup"><span data-stu-id="a387e-185">I tried hello suggestions, and hello event hub is still not working.</span></span>

    <span data-ttu-id="a387e-186">Попробуйте найти в таблице хранилища Azure hello, содержащий и журналы ошибок для самой системе диагностики Azure: **WADDiagnosticInfrastructureLogsTable**.</span><span class="sxs-lookup"><span data-stu-id="a387e-186">Try looking in hello Azure Storage table that contains logs and errors for Azure Diagnostics itself: **WADDiagnosticInfrastructureLogsTable**.</span></span> <span data-ttu-id="a387e-187">Один из вариантов — toouse средства, как [обозреватель хранилищ Azure](http://www.storageexplorer.com) учетной записи хранилища toothis tooconnect просмотра этой таблицы и добавить запрос для меток времени в hello последние 24 часа.</span><span class="sxs-lookup"><span data-stu-id="a387e-187">One option is toouse a tool such as [Azure Storage Explorer](http://www.storageexplorer.com) tooconnect toothis storage account, view this table, and add a query for TimeStamp in hello last 24 hours.</span></span> <span data-ttu-id="a387e-188">Можно использовать средство hello tooexport в CSV-файл и откройте его в приложении, таком как Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="a387e-188">You can use hello tool tooexport a .csv file and open it in an application such as Microsoft Excel.</span></span> <span data-ttu-id="a387e-189">Excel позволяет легко toosearch карточки строк, таких как **EventHubs**, toosee, что возникла ошибка.</span><span class="sxs-lookup"><span data-stu-id="a387e-189">Excel makes it easy toosearch for calling-card strings, such as **EventHubs**, toosee what error is reported.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="a387e-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a387e-190">Next steps</span></span>
<span data-ttu-id="a387e-191">•    [Дополнительные сведения о концентраторах событий](https://azure.microsoft.com/services/event-hubs/)</span><span class="sxs-lookup"><span data-stu-id="a387e-191">•    [Learn more about Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span></span>

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a><span data-ttu-id="a387e-192">Приложение. Полный пример файла конфигурации системы диагностики Azure (WADCFGX-файл)</span><span class="sxs-lookup"><span data-stu-id="a387e-192">Appendix: Complete Azure Diagnostics configuration file (.wadcfgx) example</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticsConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <WadCfg>
      <DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="applicationInsights.errors">
        <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error" />
        <Directories scheduledTransferPeriod="PT1M">
          <IISLogs containerName="wad-iis-logfiles" />
          <FailedRequestLogs containerName="wad-failedrequestlogs" />
        </Directories>
        <PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
        </PerformanceCounters>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*" />
        </WindowsEventLog>
        <CrashDumps>
          <CrashDumpConfiguration processName="WaIISHost.exe" />
          <CrashDumpConfiguration processName="WaWorkerHost.exe" />
          <CrashDumpConfiguration processName="w3wp.exe" />
        </CrashDumps>
        <Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
      </DiagnosticMonitorConfiguration>
      <SinksConfig>
        <Sink name="HotPath">
          <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" />
        </Sink>
        <Sink name="applicationInsights">
          <ApplicationInsights />
          <Channels>
            <Channel logLevel="Error" name="errors" />
          </Channels>
        </Sink>
      </SinksConfig>
    </WadCfg>
    <StorageAccount>ACCOUNT_NAME</StorageAccount>
  </PublicConfig>
  <PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <StorageAccount name="{account name}" key="{account key}" endpoint="{storage endpoint}" />
    <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" SharedAccessKey="YOUR_KEY_HERE" />
  </PrivateConfig>
  <IsEnabled>true</IsEnabled>
</DiagnosticsConfiguration>
```

<span data-ttu-id="a387e-193">Hello взаимодополняющие *ServiceConfiguration.Cloud.cscfg* для выглядит в этом примере hello следующим образом.</span><span class="sxs-lookup"><span data-stu-id="a387e-193">hello complementary *ServiceConfiguration.Cloud.cscfg* for this example looks like hello following.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="MyFixItCloudService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2015-04.2.6">
  <Role name="MyFixIt.WorkerRole">
    <Instances count="1" />
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="YOUR_CONNECTION_STRING" />
    </ConfigurationSettings>
  </Role>
</ServiceConfiguration>
```

<span data-ttu-id="a387e-194">Эквивалентные параметры на основе JSON для виртуальных машин выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a387e-194">Equivalent Json based settings for virtual machines is as follows:</span></span>
```JSON
"settings": {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 4096,
            "sinks": "applicationInsights.errors",
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "Directories": {
                "scheduledTransferPeriod": "PT1M",
                "IISLogs": {
                    "containerName": "wad-iis-logfiles"
                },
                "FailedRequestLogs": {
                    "containerName": "wad-failedrequestlogs"
                }
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "sinks": "HotPath",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Memory\\Available MBytes",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\Bytes Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Requests/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Errors Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Queued",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Rejected",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT3M"
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT1M",
                "DataSource": [
                    {
                        "name": "Application!*"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Error",
                "sinks": "HotPath"
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "HotPath",
                    "EventHub": {
                        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
                        "SharedAccessKeyName": "SendRule"
                    }
                },
                {
                    "name": "applicationInsights",
                    "ApplicationInsights": "",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "errors"
                            }
                        ]
                    }
                }
            ]
        }
    },
    "StorageAccount": "{account name}"
}


"protectedSettings": {
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{storage endpoint}",
    "EventHub": {
        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "YOUR_KEY_HERE"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="a387e-195">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a387e-195">Next steps</span></span>
<span data-ttu-id="a387e-196">На сайте ссылкам hello, изучите более подробную концентраторов событий:</span><span class="sxs-lookup"><span data-stu-id="a387e-196">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="a387e-197">Обзор концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="a387e-197">Event Hubs overview</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="a387e-198">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="a387e-198">Create an event hub</span></span>](../event-hubs/event-hubs-create.md)
* [<span data-ttu-id="a387e-199">Часто задаваемые вопросы о концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="a387e-199">Event Hubs FAQ</span></span>](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
