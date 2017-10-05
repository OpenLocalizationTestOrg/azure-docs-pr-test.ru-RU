---
title: "Сбор пользовательских данных JSON в OMS Log Analytics | Документы Майкрософт"
description: "С помощью агента OMS для Linux можно собрать данные из пользовательских источников данных JSON в Log Analytics.  В качестве такого пользовательского источника данных может использоваться простой сценарий, возвращающий результат в формате JSON, например curl, или один из более чем 300 подключаемых модулей FluentD. В этой статье описано, как настроить такой сбор данных."
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
ms.openlocfilehash: 800ee1269556e7c2d56fbbf2b497c10509b5c78c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="collecting-custom-json-data-sources-with-the-oms-agent-for-linux-in-log-analytics"></a><span data-ttu-id="29319-105">Сбор данных из пользовательских источников данных JSON с помощью агента OMS для Linux в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="29319-105">Collecting custom JSON data sources with the OMS Agent for Linux in Log Analytics</span></span>
<span data-ttu-id="29319-106">С помощью агента OMS для Linux можно собрать данные из пользовательских источников данных JSON в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="29319-106">Custom JSON data sources can be collected into Log Analytics using the OMS Agent for Linux.</span></span>  <span data-ttu-id="29319-107">В качестве такого пользовательского источника данных может использоваться простой сценарий, возвращающий результат в формате JSON, например [curl](https://curl.haxx.se/), или один из более чем [300 подключаемых модулей FluentD](http://www.fluentd.org/plugins/all).</span><span class="sxs-lookup"><span data-stu-id="29319-107">These custom data sources can be simple scripts returning JSON such as [curl](https://curl.haxx.se/) or one of [FluentD's 300+ plugins](http://www.fluentd.org/plugins/all).</span></span> <span data-ttu-id="29319-108">В этой статье описано, как настроить такой сбор данных.</span><span class="sxs-lookup"><span data-stu-id="29319-108">This article describes the configuration required for this data collection.</span></span>

> [!NOTE]
> <span data-ttu-id="29319-109">Для работы с пользовательскими источниками данных требуется агент OMS для Linux версии 1.1.0-217 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="29319-109">OMS Agent for Linux v1.1.0-217+ is required for Custom JSON Data</span></span>

## <a name="configuration"></a><span data-ttu-id="29319-110">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="29319-110">Configuration</span></span>

### <a name="configure-input-plugin"></a><span data-ttu-id="29319-111">Настройка входного подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="29319-111">Configure input plugin</span></span>

<span data-ttu-id="29319-112">Для сбора данных JSON в Log Analytics добавьте `oms.api.` в начало тега FluentD во входном подключаемом модуле.</span><span class="sxs-lookup"><span data-stu-id="29319-112">To collect JSON data in Log Analytics, add `oms.api.` to the start of a FluentD tag in an input plugin.</span></span>

<span data-ttu-id="29319-113">Например, ниже приведен отдельный файл конфигурации `exec-json.conf` в `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span><span class="sxs-lookup"><span data-stu-id="29319-113">For example, following is a separate configuration file `exec-json.conf` in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span></span>  <span data-ttu-id="29319-114">В нем используется подключаемый модуль FluentD `exec` для запуска команды curl каждые 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="29319-114">This uses the FluentD plugin `exec` to run a curl command every 30 seconds.</span></span>  <span data-ttu-id="29319-115">Выходные данные этой команды собираются с помощью выходного подключаемого модуля JSON.</span><span class="sxs-lookup"><span data-stu-id="29319-115">The output from this command is collected by the JSON output plugin.</span></span>

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
<span data-ttu-id="29319-116">Для файла конфигурации, добавленного в разделе `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`, необходимо изменить владельца, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="29319-116">The configuration file added under `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` will require to have its ownership changed with the following command.</span></span>

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a><span data-ttu-id="29319-117">Настройка выходного подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="29319-117">Configure output plugin</span></span> 
<span data-ttu-id="29319-118">Добавьте следующую конфигурацию выходного подключаемого модуля в раздел `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` основной конфигурации или в отдельный файл конфигурации в каталоге `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span><span class="sxs-lookup"><span data-stu-id="29319-118">Add the following output plugin configuration to the main configuration in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` or as a separate configuration file placed in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span></span>

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

### <a name="restart-oms-agent-for-linux"></a><span data-ttu-id="29319-119">Перезапустите агент OMS для Linux</span><span class="sxs-lookup"><span data-stu-id="29319-119">Restart OMS Agent for Linux</span></span>
<span data-ttu-id="29319-120">Перезапустите службу агента OMS для Linux, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="29319-120">Restart the OMS Agent for Linux service with the following command.</span></span>

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a><span data-ttu-id="29319-121">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="29319-121">Output</span></span>
<span data-ttu-id="29319-122">Данные, собираемые в Log Analytics, будут иметь тип записи `<FLUENTD_TAG>_CL`.</span><span class="sxs-lookup"><span data-stu-id="29319-122">The data will be collected in Log Analytics with a record type of `<FLUENTD_TAG>_CL`.</span></span>

<span data-ttu-id="29319-123">Например, пользовательский тег `tag oms.api.tomcat` в Log Analytics будет иметь тип записи `tomcat_CL`.</span><span class="sxs-lookup"><span data-stu-id="29319-123">For example, the custom tag `tag oms.api.tomcat` in Log Analytics with a record type of `tomcat_CL`.</span></span>  <span data-ttu-id="29319-124">Для получения всех записей этого типа выполните поиск по журналам следующим образом.</span><span class="sxs-lookup"><span data-stu-id="29319-124">You could retrieve all records of this type with the following log search.</span></span>

    Type=tomcat_CL

<span data-ttu-id="29319-125">Поддерживаются вложенные источники данных JSON, но они индексируются не на основе родительского поля.</span><span class="sxs-lookup"><span data-stu-id="29319-125">Nested JSON data sources are supported, but are indexed based off of parent field.</span></span> <span data-ttu-id="29319-126">Например, в результате выполнения поискового запроса `tag_s : "[{ "a":"1", "b":"2" }]` в Log Analytics будут возвращены следующие данные JSON.</span><span class="sxs-lookup"><span data-stu-id="29319-126">For example, the following JSON data is returned from a Log Analytics search as `tag_s : "[{ "a":"1", "b":"2" }]`.</span></span>

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a><span data-ttu-id="29319-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="29319-127">Next steps</span></span>
* <span data-ttu-id="29319-128">Узнайте больше об [операциях поиска по журналу](log-analytics-log-searches.md) , которые можно применять для анализа данных, собираемых из источников данных и решений.</span><span class="sxs-lookup"><span data-stu-id="29319-128">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
 