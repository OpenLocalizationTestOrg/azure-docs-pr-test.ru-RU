---
title: "aaaCollecting пользовательских данных JSON в аналитику журнала OMS | Документы Microsoft"
description: "Пользовательские источники данных JSON можно собирать в службе анализа журналов с помощью hello агента OMS для Linux.  В качестве такого пользовательского источника данных может использоваться простой сценарий, возвращающий результат в формате JSON, например curl, или один из более чем 300 подключаемых модулей FluentD. В этой статье описывается hello конфигурация, необходимая для этой коллекции данных."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 97d401408a8c206d4a9ef2ec9b13ba1ca6b5e92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="collecting-custom-json-data-sources-with-hello-oms-agent-for-linux-in-log-analytics"></a><span data-ttu-id="19f2b-105">Сбор пользовательских источников данных JSON с hello агента OMS для Linux в службе анализа журналов</span><span class="sxs-lookup"><span data-stu-id="19f2b-105">Collecting custom JSON data sources with hello OMS Agent for Linux in Log Analytics</span></span>
<span data-ttu-id="19f2b-106">Пользовательские источники данных JSON можно собирать в службе анализа журналов с помощью hello агента OMS для Linux.</span><span class="sxs-lookup"><span data-stu-id="19f2b-106">Custom JSON data sources can be collected into Log Analytics using hello OMS Agent for Linux.</span></span>  <span data-ttu-id="19f2b-107">В качестве такого пользовательского источника данных может использоваться простой сценарий, возвращающий результат в формате JSON, например [curl](https://curl.haxx.se/), или один из более чем [300 подключаемых модулей FluentD](http://www.fluentd.org/plugins/all).</span><span class="sxs-lookup"><span data-stu-id="19f2b-107">These custom data sources can be simple scripts returning JSON such as [curl](https://curl.haxx.se/) or one of [FluentD's 300+ plugins](http://www.fluentd.org/plugins/all).</span></span> <span data-ttu-id="19f2b-108">В этой статье описывается hello конфигурация, необходимая для этой коллекции данных.</span><span class="sxs-lookup"><span data-stu-id="19f2b-108">This article describes hello configuration required for this data collection.</span></span>

> [!NOTE]
> <span data-ttu-id="19f2b-109">Для работы с пользовательскими источниками данных требуется агент OMS для Linux версии 1.1.0-217 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="19f2b-109">OMS Agent for Linux v1.1.0-217+ is required for Custom JSON Data</span></span>

## <a name="configuration"></a><span data-ttu-id="19f2b-110">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="19f2b-110">Configuration</span></span>

### <a name="configure-input-plugin"></a><span data-ttu-id="19f2b-111">Настройка входного подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="19f2b-111">Configure input plugin</span></span>

<span data-ttu-id="19f2b-112">добавить toocollect данных JSON в службы анализа журналов, `oms.api.` начало toohello тега FluentD возможности ввода подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="19f2b-112">toocollect JSON data in Log Analytics, add `oms.api.` toohello start of a FluentD tag in an input plugin.</span></span>

<span data-ttu-id="19f2b-113">Например, ниже приведен отдельный файл конфигурации `exec-json.conf` в `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span><span class="sxs-lookup"><span data-stu-id="19f2b-113">For example, following is a separate configuration file `exec-json.conf` in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span></span>  <span data-ttu-id="19f2b-114">В этом случае используется подключаемый модуль FluentD hello `exec` toorun команду curl каждые 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="19f2b-114">This uses hello FluentD plugin `exec` toorun a curl command every 30 seconds.</span></span>  <span data-ttu-id="19f2b-115">Подключаемый модуль выходных данных JSON hello собираются Hello выходные данные этой команды.</span><span class="sxs-lookup"><span data-stu-id="19f2b-115">hello output from this command is collected by hello JSON output plugin.</span></span>

```
<source>
  type exec
  command 'curl localhost/json.output'
  format json
  tag oms.api.httpresponse
  run_interval 30s
</source>

<match oms.api.httpresponse>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api_httpresponse*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```
<span data-ttu-id="19f2b-116">добавлено в файл конфигурации Hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` потребуется toohave сменить его владельца с hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="19f2b-116">hello configuration file added under `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` will require toohave its ownership changed with hello following command.</span></span>

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a><span data-ttu-id="19f2b-117">Настройка выходного подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="19f2b-117">Configure output plugin</span></span> 
<span data-ttu-id="19f2b-118">Добавьте следующие выходные данные подключаемого модуля конфигурации toohello основной конфигурации в hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` или как отдельный файл конфигурации будет помещен в`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span><span class="sxs-lookup"><span data-stu-id="19f2b-118">Add hello following output plugin configuration toohello main configuration in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` or as a separate configuration file placed in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span></span>

```
<match oms.api.**>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```

### <a name="restart-oms-agent-for-linux"></a><span data-ttu-id="19f2b-119">Перезапустите агент OMS для Linux</span><span class="sxs-lookup"><span data-stu-id="19f2b-119">Restart OMS Agent for Linux</span></span>
<span data-ttu-id="19f2b-120">Перезапустите hello агента OMS для Linux службы с hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="19f2b-120">Restart hello OMS Agent for Linux service with hello following command.</span></span>

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a><span data-ttu-id="19f2b-121">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="19f2b-121">Output</span></span>
<span data-ttu-id="19f2b-122">Hello данные будут собраны в ходе анализа журналов с типом записи `<FLUENTD_TAG>_CL`.</span><span class="sxs-lookup"><span data-stu-id="19f2b-122">hello data will be collected in Log Analytics with a record type of `<FLUENTD_TAG>_CL`.</span></span>

<span data-ttu-id="19f2b-123">Например, hello настраиваемый тег `tag oms.api.tomcat` в службе анализа журналов с типом записи `tomcat_CL`.</span><span class="sxs-lookup"><span data-stu-id="19f2b-123">For example, hello custom tag `tag oms.api.tomcat` in Log Analytics with a record type of `tomcat_CL`.</span></span>  <span data-ttu-id="19f2b-124">Можно извлечь все записи этого типа с hello после поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="19f2b-124">You could retrieve all records of this type with hello following log search.</span></span>

    Type=tomcat_CL

<span data-ttu-id="19f2b-125">Поддерживаются вложенные источники данных JSON, но они индексируются не на основе родительского поля.</span><span class="sxs-lookup"><span data-stu-id="19f2b-125">Nested JSON data sources are supported, but are indexed based off of parent field.</span></span> <span data-ttu-id="19f2b-126">Например, следующие данные JSON hello возвращается из поиска аналитики журналов как `tag_s : "[{ "a":"1", "b":"2" }]`.</span><span class="sxs-lookup"><span data-stu-id="19f2b-126">For example, hello following JSON data is returned from a Log Analytics search as `tag_s : "[{ "a":"1", "b":"2" }]`.</span></span>

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a><span data-ttu-id="19f2b-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="19f2b-127">Next steps</span></span>
* <span data-ttu-id="19f2b-128">Дополнительные сведения о [входа выполняет](log-analytics-log-searches.md) tooanalyze hello данные, собранные из источников данных и решений.</span><span class="sxs-lookup"><span data-stu-id="19f2b-128">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
 