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
# <a name="collecting-custom-json-data-sources-with-hello-oms-agent-for-linux-in-log-analytics"></a>Сбор пользовательских источников данных JSON с hello агента OMS для Linux в службе анализа журналов
Пользовательские источники данных JSON можно собирать в службе анализа журналов с помощью hello агента OMS для Linux.  В качестве такого пользовательского источника данных может использоваться простой сценарий, возвращающий результат в формате JSON, например [curl](https://curl.haxx.se/), или один из более чем [300 подключаемых модулей FluentD](http://www.fluentd.org/plugins/all). В этой статье описывается hello конфигурация, необходимая для этой коллекции данных.

> [!NOTE]
> Для работы с пользовательскими источниками данных требуется агент OMS для Linux версии 1.1.0-217 или более поздней версии

## <a name="configuration"></a>Конфигурация

### <a name="configure-input-plugin"></a>Настройка входного подключаемого модуля

добавить toocollect данных JSON в службы анализа журналов, `oms.api.` начало toohello тега FluentD возможности ввода подключаемого модуля.

Например, ниже приведен отдельный файл конфигурации `exec-json.conf` в `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.  В этом случае используется подключаемый модуль FluentD hello `exec` toorun команду curl каждые 30 секунд.  Подключаемый модуль выходных данных JSON hello собираются Hello выходные данные этой команды.

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
добавлено в файл конфигурации Hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` потребуется toohave сменить его владельца с hello следующую команду.

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a>Настройка выходного подключаемого модуля 
Добавьте следующие выходные данные подключаемого модуля конфигурации toohello основной конфигурации в hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` или как отдельный файл конфигурации будет помещен в`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`

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

### <a name="restart-oms-agent-for-linux"></a>Перезапустите агент OMS для Linux
Перезапустите hello агента OMS для Linux службы с hello следующую команду.

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a>Выходные данные
Hello данные будут собраны в ходе анализа журналов с типом записи `<FLUENTD_TAG>_CL`.

Например, hello настраиваемый тег `tag oms.api.tomcat` в службе анализа журналов с типом записи `tomcat_CL`.  Можно извлечь все записи этого типа с hello после поиска журналов.

    Type=tomcat_CL

Поддерживаются вложенные источники данных JSON, но они индексируются не на основе родительского поля. Например, следующие данные JSON hello возвращается из поиска аналитики журналов как `tag_s : "[{ "a":"1", "b":"2" }]`.

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о [входа выполняет](log-analytics-log-searches.md) tooanalyze hello данные, собранные из источников данных и решений. 
 