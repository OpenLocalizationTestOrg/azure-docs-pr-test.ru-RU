---
title: "оповещения Nagios и Zabbix aaaCollect в аналитику журнала OMS | Документы Microsoft"
description: "Nagios и Zabbix — средства мониторинга с открытым исходным кодом. Можно собирать оповещения, с помощью этих средств в службе анализа журналов в порядке tooanalyze их вместе с предупреждениями из других источников.  В этой статье описывается, как tooconfigure hello агента OMS для Linux toocollect оповещений из этих систем."
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
ms.openlocfilehash: 23e2252e4fed8bc87baec063694a8472ca84220d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a>Сбор оповещений Nagios и Zabbix из агента OMS для Linux в Log Analytics 
[Nagios](https://www.nagios.org/) и [Zabbix](http://www.zabbix.com/) — средства мониторинга с открытым исходным кодом.  Можно собирать оповещения, с помощью этих средств в службе анализа журналов в порядке tooanalyze их вместе с [предупреждениями из других источников](log-analytics-alerts.md).  В этой статье описывается, как tooconfigure hello агента OMS для Linux toocollect оповещений из этих систем.
 
## <a name="configure-alert-collection"></a>Настройка сбора оповещений

### <a name="configuring-nagios-alert-collection"></a>Настройка сбора оповещений Nagios
Выполните следующие действия на предупреждения toocollect сервера Nagios hello hello.

1. Предоставление пользовательских hello **omsagent** файла журнала Nagios toohello доступ для чтения (т. е. `/var/log/nagios/nagios.log`). При условии, что файл nagios.log hello принадлежит группе hello `nagios`, можно добавить пользователя hello **omsagent** toohello **nagios** группы. 

    sudo usermod -a -G nagios omsagent

2.  Изменение файла конфигурации hello в (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`). Убедитесь, что присутствуют и не закомментированы следующие записи hello:  

        <source>  
          type tail  
          #Update path toopoint tooyour nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. Перезапустите управляющую программу omsagent hello

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a>Настройка сбора оповещений Zabbix
toocollect предупреждения с сервера Zabbix, требуются toospecify пользователя и пароль в *открытый текст*. Это не идеальное решение, но рекомендуется создать пользователя hello и предоставить onlu toomonitor разрешения.

Выполните следующие действия на предупреждения toocollect сервера Nagios hello hello.

1. Изменение файла конфигурации hello в (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`). Убедитесь, что присутствуют и не закомментированы следующие записи hello.  Изменить hello пользователя имя и пароль toovalues Zabbix среды.

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. Перезапустите управляющую программу omsagent hello

    sudo sh /opt/microsoft/omsagent/bin/service_control restart


## <a name="alert-records"></a>Записи оповещений
Записи оповещений из Nagios и Zabbix можно получить с помощью [поиска по журналам](log-analytics-log-searches.md) в Log Analytics.

### <a name="nagios-alert-records"></a>Записи оповещений Nagios

Для записей оповещений Nagios параметр **Type** (тип) имеет значение **Alert** (оповещение), а параметр **SourceSystem** (источник) — значение **Nagios**.  Они имеют свойства hello в hello в следующей таблице.

| Свойство | Описание |
|:--- |:--- |
| Тип |*Предупреждение* |
| SourceSystem |*Nagios* |
| AlertName |Имя предупреждения hello. |
| AlertDescription | Описание предупреждения hello. |
| AlertState | Состояние узла или службы hello.<br><br>ОК<br>ПРЕДУПРЕЖДЕНИЕ<br>РАБОТАЕТ<br>СБОЙ |
| HostName | Имя узла hello, создавшего предупреждение hello. |
| PriorityNumber | Уровень приоритета предупреждения hello. |
| StateType | Тип состояния предупреждения hello Hello.<br><br>SOFT — проблема, которая не проверялась повторно.<br>HARD — проблема, которая проверялась повторно заданное число раз.  |
| TimeGenerated |Создания предупреждения hello даты и времени. |


### <a name="zabbix-alert-records"></a>Записи оповещений Zabbix
Для записей оповещений Nagios параметр **Type** (тип) имеет значение **Alert** (оповещение), а параметр **SourceSystem** (источник) — значение **Zabbix**.  Они имеют свойства hello в hello в следующей таблице.

| Свойство | Описание |
|:--- |:--- |
| Тип |*Предупреждение* |
| SourceSystem |*Zabbix* |
| AlertName | Имя предупреждения hello. |
| AlertPriority | Серьезность предупреждения hello.<br><br>не определен<br>информационный.<br>Предупреждение<br>average<br>высокий<br>очень высокий  |
| AlertState | Состояние предупреждения hello.<br><br>0 — состояние — копирование toodate.<br>1 — состояние неизвестно.  |
| AlertTypeNumber | Указывает, может ли оповещение создавать несколько событий, связанных с проблемой.<br><br>0 — состояние — копирование toodate.<br>1 — состояние неизвестно.    |
| Комментарии | Дополнительные комментарии для оповещения. |
| HostName | Имя узла hello, создавшего предупреждение hello. |
| PriorityNumber | Значение, указывающее серьезность оповещения hello.<br><br>0 — не определен<br>1 — информация<br>2 — предупреждение<br>3 — средний<br>4 — высокий<br>5 — очень высокий |
| TimeGenerated |Создания предупреждения hello даты и времени. |
| TimeLastModified |Дата и время hello состояние оповещения hello последнего изменения. |


## <a name="next-steps"></a>Дальнейшие действия
* Ознакомьтесь с дополнительными сведениями об [оповещениях](log-analytics-alerts.md) в Log Analytics.
* Дополнительные сведения о [входа выполняет](log-analytics-log-searches.md) tooanalyze hello данные, собранные из источников данных и решений. 
