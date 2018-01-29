---
title: "Журналы IIS в службе Azure Log Analytics | Документация Майкрософт"
description: "Службы IIS (Internet Information Services) хранят данные об активности пользователей в файлах журналов, собираемых службой Log Analytics.  Из этой статьи вы узнаете, как настроить коллекцию журналов IIS и сведения о записях, создаваемых журналами в рабочей области Log Analytics."
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
ms.date: 01/07/2018
ms.author: bwren
ms.openlocfilehash: b8ce4e6fe6e12aa3edb81abad1589924e3e121e4
ms.sourcegitcommit: 176c575aea7602682afd6214880aad0be6167c52
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/09/2018
---
# <a name="iis-logs-in-log-analytics"></a>Журналы IIS в службе Log Analytics
Службы IIS (Internet Information Services) хранят данные об активности пользователей в файлах журналов, собираемых службой Log Analytics.  

![Журналы IIS](media/log-analytics-data-sources-iis-logs/overview.png)

## <a name="configuring-iis-logs"></a>Настройка журналов IIS
Служба Log Analytics собирает записи из файлов журналов, созданных службами IIS, поэтому вам необходимо [настроить IIS для ведения журнала](https://technet.microsoft.com/library/hh831775.aspx).

Служба Log Analytics поддерживает только те файлы журналов IIS, которые хранятся в формате W3C, и не поддерживает настраиваемые поля или расширенное ведение журналов IIS.  
Она не собирает журналы в формате NCSA или в собственном формате IIS.

Журналы IIS настраиваются в меню ["Данные" в параметрах Log Analytics](log-analytics-data-sources.md#configuring-data-sources).  Никакие настройки, кроме выбора параметра **Сбор файлов журналов IIS в формате W3C**, не требуются.

Если вы включаете сбор данных журналов IIS, рекомендуем настроить на каждом сервере переход на журналы IIS.

## <a name="data-collection"></a>Сбор данных
Log Analytics собирает записи в журналах IIS из каждого подключенного источника примерно раз в 15 минут.  Агент фиксирует место сбора в каждом журнале событий, который используется для сбора данных.  Если агент перейдет в автономный режим, Log Analytics собирает события, начиная с места остановки, даже если эти события были созданы, пока агент находился вне сети.

## <a name="iis-log-record-properties"></a>Свойства записей в журналах IIS
Записи в журналах IIS относятся к типу **W3CIISLog** и обладают свойствами, описанными в таблице ниже.

| Свойство | ОПИСАНИЕ |
|:--- |:--- |
| Компьютер |Имя компьютера, с которого было получено событие. |
| cIP |IP-адрес клиента. |
| csMethod |Метод запроса, такой как GET или POST. |
| csReferer |Сайт, с которого пользователь перешел на текущий сайт. |
| csUserAgent |Тип браузера клиента. |
| csUserName |Имя прошедшего проверку пользователя, который подключился к серверу. Анонимные пользователи обозначаются дефисом. |
| csUriStem |Целевой объект запроса, такой как веб-страница. |
| csUriQuery |Запрос, который пытался выполнить клиент (если есть). |
| ManagementGroupName |Имя группы управления для агентов Operations Manager.  Для других агентов это AOI-\<идентификатор_рабочей_области\>. |
| RemoteIPCountry |Страна IP-адреса клиента. |
| RemoteIPLatitude |Широта IP-адреса клиента. |
| RemoteIPLongitude |Долгота IP-адреса клиента. |
| scStatus |Код состояния HTTP. |
| scSubStatus |Код ошибки подсостояния . |
| scWin32Status |Код состояния Windows. |
| sIP |IP-адрес веб-сервера. |
| SourceSystem |OpsMgr |
| sPort |Порт на сервере, к которому подключен клиент. |
| sSiteName |Имя сайта IIS. |
| TimeGenerated |Дата и время регистрации записи. |
| TimeTaken |Время обработки запроса в миллисекундах. |

## <a name="log-searches-with-iis-logs"></a>Поиск по журналами с помощью журналов IIS
В следующей таблице представлены различные примеры запросов к журналу, извлекающих записи из журналов IIS.

| Запрос | ОПИСАНИЕ |
|:--- |:--- |
| W3CIISLog |Все записи в журнале IIS. |
| W3CIISLog &#124; where scStatus==500 |Все записи журнала IIS с состоянием возврата 500. |
| W3CIISLog &#124; summarize count() by cIP |Число записей в журнале IIS по IP-адресу клиента. |
| W3CIISLog &#124; where csHost=="www.contoso.com" &#124; summarize count() by csUriStem |Число записей в журнале IIS по URL-адресу для узла www.contoso.com. |
| W3CIISLog &#124; summarize sum(csBytes) by Computer &#124; take 500000 |Общее количество байтов, полученных каждым компьютером IIS. |

## <a name="next-steps"></a>Дополнительная информация
* Настройте службу Log Analytics для сбора других [источников данных](log-analytics-data-sources.md) для анализа.
* Узнайте больше об [операциях поиска по журналу](log-analytics-log-searches.md) , которые можно применять для анализа данных, собираемых из источников данных и решений.
* Настройте оповещения в службе Log Analytics для получения заблаговременных уведомлений о важных условиях, обнаруженных в журналах IIS.
