---
title: "aaaCollect данные из CollectD в аналитику журнала OMS | Документы Microsoft"
description: "CollectD — управляющая программа Linux с открытым исходным кодом, которая периодически собирает данные приложений и системные данные.  В этой статье приведены сведения о сборе данных CollectD в OMS Log Analytics."
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
ms.date: 05/02/2017
ms.author: magoedte
ms.openlocfilehash: 7ad82c9c67a664aabd44f08bef2253d84cd2dfba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a>Сбор данных CollectD с помощью агентов Linux в Log Analytics
[CollectD](https://collectd.org/) — управляющая программа Linux с открытым исходным кодом, которая периодически собирает метрики производительности приложений и системные данные. Пример приложения включают hello виртуальной машины Java (JVM), сервер MySQL и Nginx. В этой статье приводятся сведения о сборе данных производительности CollectD в Log Analytics.

Полный список доступных подключаемых модулей можно найти в [таблице подключаемых модулей](https://collectd.org/wiki/index.php/Table_of_Plugins).

![Обзор CollectD](media/log-analytics-data-sources-collectd/overview.png)

Hello следующая конфигурация CollectD включается в hello агента OMS для Linux tooroute CollectD данные toohello агента OMS для Linux.

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

Кроме того Если с помощью версии collectD, прежде чем 5.5 используется следующая конфигурация вместо hello.

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

Hello CollectD конфигурации используется по умолчанию hello`write_http` подключаемый модуль toosend метрики производительности через порт 26000 tooOMS агент для Linux. 

> [!NOTE]
> Это может быть настроенный tooa настраиваемого порт при необходимости.

Hello агента OMS для Linux также прослушивает порт 26000 для CollectD метрик и преобразует их tooOMS схемы метрики. Hello Вот hello агента OMS для Linux конфигурации `collectd.conf`.

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a>Поддерживаемые версии
- Log Analytics сейчас поддерживает CollectD версии 4.8 и более поздней версии.
- Для сбора метрик CollectD необходим агент OMS для Linux версии 1.1.0-217 или более поздней версии.


## <a name="configuration"></a>Конфигурация
Hello ниже приведены основные шаги коллекции tooconfigure CollectD данных в службе анализа журналов.

1. Настройка CollectD toosend данные toohello агента OMS для Linux с помощью подключаемого модуля write_http hello.  
2. Настройте hello агента OMS для Linux toolisten для hello CollectD данных на соответствующий порт hello.
3. Перезапустите CollectD и агент OMS для Linux.

### <a name="configure-collectd-tooforward-data"></a>Настройка данных tooforward CollectD 

1. tooroute CollectD данные toohello агента OMS для Linux, `oms.conf` toobe потребностей добавить каталог tooCollectD элемента конфигурации. Hello назначения этого файла зависит от дистрибутив Linux hello вашего компьютера.

    Если конфигурационные файлы CollectD находятся в папке /etc/collectd.d/:

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    Если конфигурационные файлы CollectD находятся в папке /etc/collectd/collectd.conf.d/:

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    >Для версий CollectD перед 5.5 имеется toomodify hello теги `oms.conf` как показано выше.
    >

2. Скопируйте каталог конфигурации рабочей области toohello требуемого collectd.conf omsagent.

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. Перезапустите CollectD и агента OMS для Linux с помощью следующих команд hello.

    sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart

## <a name="collectd-metrics-toolog-analytics-schema-conversion"></a>Метрики CollectD tooLog преобразование схемы аналитика
toomaintain знакомую модель между метрики инфраструктуры уже собранных агентом OMS для Linux и hello новых показателей собранные CollectD hello после сопоставления схемы используется:

| Поле метрики CollectD | Поле Log Analytics |
|:--|:--|
| host | Компьютер |
| plugin | None |
| plugin_instance | Имя экземпляра<br>Если **plugin_instance** имеет значение *null*, то InstanceName="*_Total*" |
| type | ObjectName |
| type_instance | CounterName<br>Если **type_instance** имеет значение *null*, то CounterName=**blank** |
| dsnames[] | CounterName |
| dstypes | None |
| values[] | CounterValue |

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о [входа выполняет](log-analytics-log-searches.md) tooanalyze hello данные, собранные из источников данных и решений. 
* Используйте [настраиваемые поля](log-analytics-custom-fields.md) tooparse данных из системного журнала записей в отдельные поля.

