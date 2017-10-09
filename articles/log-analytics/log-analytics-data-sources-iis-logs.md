---
title: "Регистрирует aaaIIS в службе анализа журналов | Документы Microsoft"
description: "Службы IIS (Internet Information Services) хранят данные об активности пользователей в файлах журналов, собираемых службой Log Analytics.  В этой статье описывается tooconfigure сбора журналов IIS и сведения о записи hello их создания в репозитории OMS hello."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: cec5ff0a-01f5-4262-b2e8-e3db7b7467d2
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: bwren
ms.openlocfilehash: c5575351090cdabaf651bcb49867794ee3a4b6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="iis-logs-in-log-analytics"></a>Журналы IIS в службе Log Analytics
Службы IIS (Internet Information Services) хранят данные об активности пользователей в файлах журналов, собираемых службой Log Analytics.  

![Журналы IIS](media/log-analytics-data-sources-iis-logs/overview.png)

## <a name="configuring-iis-logs"></a>Настройка журналов IIS
Служба Log Analytics собирает записи из файлов журналов, созданных службами IIS, поэтому вам необходимо [настроить IIS для ведения журнала](https://technet.microsoft.com/library/hh831775.aspx).

Служба Log Analytics поддерживает только те файлы журналов IIS, которые хранятся в формате W3C, и не поддерживает настраиваемые поля или расширенное ведение журналов IIS.  
Она не собирает журналы в формате NCSA или в собственном формате IIS.

Настройка журналов служб IIS в службе анализа журналов из hello [меню данные в параметры журнала аналитика](log-analytics-data-sources.md#configuring-data-sources).  Никакие настройки, кроме выбора параметра **Сбор файлов журналов IIS в формате W3C**, не требуются.

Рекомендуется при включении сбора журналов IIS, следует настроить приветствия смену журнала IIS на каждом сервере.

## <a name="data-collection"></a>Сбор данных
Log Analytics собирает записи в журналах IIS из каждого подключенного источника примерно раз в 15 минут.  Hello агент записывает его место в каждого, выполняющее сбор данных из журнала событий.  Если агент hello переходит в автономный режим, затем анализа журналов собирает события от последнего места остановки, даже если эти события создаются, когда агент hello находился в автономном режиме.

## <a name="iis-log-record-properties"></a>Свойства записей в журналах IIS
Записи журнала IIS имеют тип **W3CIISLog** и имеющих свойства hello в hello в следующей таблице:

| Свойство | Описание |
|:--- |:--- |
| Компьютер |Имя компьютера hello, hello события, собранные из. |
| cIP |IP-адрес клиента hello. |
| csMethod |Метод запроса hello, например GET или POST. |
| csReferer |Сайт, hello пользователя по ссылке с toohello текущего узла. |
| csUserAgent |Тип браузера клиента hello. |
| csUserName |Имя hello проверку подлинности пользователя, который получил доступ к серверу hello. Анонимные пользователи обозначаются дефисом. |
| csUriStem |Целевой объект запроса hello, например веб-страницы. |
| csUriQuery |Запрос, если таковые имеются, этот клиент hello пытается tooperform. |
| ManagementGroupName |Имя группы управления hello агенты Operations Manager.  Для других агентов это AOI-\<идентификатор_рабочей_области\>. |
| RemoteIPCountry |Страна hello IP-адрес клиента hello. |
| RemoteIPLatitude |Широта hello клиентского IP-адреса. |
| RemoteIPLongitude |Долгота hello клиентского IP-адреса. |
| scStatus |Код состояния HTTP. |
| scSubStatus |Код ошибки подсостояния . |
| scWin32Status |Код состояния Windows. |
| sIP |IP-адрес веб-сервера hello. |
| SourceSystem |OpsMgr |
| sPort |Hello server hello клиенту, подключившемуся к порту. |
| sSiteName |Имя сайта IIS hello. |
| TimeGenerated |Дата и время записи hello журнал. |
| TimeTaken |Длина hello tooprocess время запроса в миллисекундах. |

## <a name="log-searches-with-iis-logs"></a>Поиск по журналами с помощью журналов IIS
Hello следующей таблице приведены примеры различных журнала запросов, получающих записи журнала IIS.

| Запрос | Описание |
|:--- |:--- |
| Type=W3CIISLog |Все записи в журнале IIS. |
| Type=W3CIISLog scStatus=500 |Все записи журнала IIS с состоянием возврата 500. |
| Type=W3CIISLog &#124; Measure count() by cIP |Число записей в журнале IIS по IP-адресу клиента. |
| Type=W3CIISLog csHost="www.contoso.com" &#124; Measure count() by csUriStem |Число IIS элементы журнала по URL-адрес для узла www.contoso.com hello. |
| Type=W3CIISLog &#124; Measure Sum(csBytes) by Computer &#124; top 500000 |Общее количество байтов, полученных каждым компьютером IIS. |

>[!NOTE]
> Если рабочую область был обновленного toohello [языка запросов новый журнал аналитики](log-analytics-log-search-upgrade.md), то hello выше запросы будут изменены следующие toohello.

> | Запрос | Описание |
|:--- |:--- |
| W3CIISLog |Все записи в журнале IIS. |
| W3CIISLog &#124; where scStatus==500 |Все записи журнала IIS с состоянием возврата 500. |
| W3CIISLog &#124; summarize count() by cIP |Число записей в журнале IIS по IP-адресу клиента. |
| W3CIISLog &#124; where csHost=="www.contoso.com" &#124; summarize count() by csUriStem |Число IIS элементы журнала по URL-адрес для узла www.contoso.com hello. |
| W3CIISLog &#124; summarize sum(csBytes) by Computer &#124; take 500000 |Общее количество байтов, полученных каждым компьютером IIS. |

## <a name="next-steps"></a>Дальнейшие действия
* Настройка других анализа журналов toocollect [источники данных](log-analytics-data-sources.md) для анализа.
* Дополнительные сведения о [входа выполняет](log-analytics-log-searches.md) tooanalyze hello данные, собранные из источников данных и решений.
* Настройка оповещений в анализа журналов tooproactively уведомления о важных условий, которые обнаружены в журналах IIS.
