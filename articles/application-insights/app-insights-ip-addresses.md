---
title: "aaaIP адреса, используемые Application Insights | Документы Microsoft"
description: "Исключения брандмауэра сервера, требуемые для Application Insights"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 44d989f8-bae9-40ff-bfd5-8343d3e59358
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 8/11/2017
ms.author: bwren
ms.openlocfilehash: 2c101b8da2ba9594fbff607f4f7551cda80c3c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="ip-addresses-used-by-application-insights"></a>IP-адреса, используемые службой Application Insights
Hello [Azure Application Insights](app-insights-overview.md) служба использует несколько IP-адресов. Может потребоваться эти адреса tooknow, если приложение hello, которое вы наблюдаете находится за брандмауэром.

> [!NOTE]
> Несмотря на то, что эти адреса являются статическими, это возможно, что нам нужно будет toochange их tootime времени.
> 
> 

## <a name="outgoing-ports"></a>Порты для исходящего трафика
Требуется tooopen некоторые исходящие порты в hello tooallow брандмауэра сервера пакет SDK Application Insights и/или данные toohello монитор состояния toosend портала:

| Назначение | URL-адрес | IP-адрес | порты; |
| --- | --- | --- | --- |
| Телеметрия |dc.services.visualstudio.com<br/>dc.applicationinsights.microsoft.com |40.114.241.141<br/>104.45.136.42<br/>40.84.189.107<br/>168.63.242.221<br/>52.167.221.184<br/>52.169.64.244 |443 |
| Динамический поток метрик |rt.services.visualstudio.com<br/>rt.applicationinsights.microsoft.com |23.96.28.38<br/>13.92.40.198 |443 |
| Внутренняя телеметрия |breeze.aimon.applicationinsights.io |52.161.11.71 |443 |

## <a name="status-monitor"></a>Монитор состояния
Настройка монитора состояния (требуется только для внесения изменений).

| Назначение | URL-адрес | IP-адрес | порты; |
| --- | --- | --- | --- |
| Конфигурация |`management.core.windows.net` | |`443` |
| Конфигурация |`management.azure.com` | |`443` |
| Конфигурация |`login.windows.net` | |`443` |
| Конфигурация |`login.microsoftonline.com` | |`443` |
| Конфигурация |`secure.aadcdn.microsoftonline-p.com` | |`443` |
| Конфигурация |`auth.gfx.ms` | |`443` |
| Конфигурация |`login.live.com` | |`443` |
| Установка |`packages.nuget.org` | |`443` |

## <a name="hockeyapp"></a>HockeyApp
| Назначение | URL-адрес | IP-адрес | порты; |
| --- | --- | --- | --- |
| Данные о сбоях |gate.hockeyapp.net |104.45.136.42 |80, 443 |

## <a name="availability-tests"></a>Тесты доступности
Это список адресов, из которого hello [доступности веб-тесты](app-insights-monitor-web-app-availability.md) выполняются. Если вы хотите toorun веб-тестов в приложении, но веб-сервера имеет ограниченные tooserving конкретных клиентов, будет иметь toopermit входящий трафик от наших доступности тестовые серверы.

Откройте порты 80 (HTTP) и 443 (HTTPS) для входящего трафика с этих адресов (IP-адреса сгруппированы по расположению):

```
AU : Sydney
13.70.83.252
13.75.150.96
13.75.153.9
13.75.158.185
BR : Sao Paulo
191.232.32.122
191.232.172.45
191.232.176.218
191.232.191.225
CH : Zurich
94.245.66.43
94.245.66.44
94.245.66.45
94.245.66.48
FR : Paris
94.245.72.44
94.245.72.45
94.245.72.46
94.245.72.49
94.245.72.52
94.245.72.53
HK : Hong Kong
13.75.121.122
23.99.115.153
23.99.123.38
23.102.232.186
52.175.38.49
52.175.39.103
IE : Dublin
13.74.184.101
13.74.185.160
40.69.200.198
52.164.224.46
52.169.12.203
52.169.14.11
52.169.237.149
52.178.183.105
JP : Kawaguchi
52.243.33.33
52.243.33.141
52.243.35.253
52.243.41.117
NL : Amsterdam
52.174.166.113
52.174.178.96
52.174.31.140
52.174.35.14
52.178.104.23
52.178.109.190
52.178.111.139
52.233.166.221
RU : Moscow
94.245.82.32
94.245.82.33
94.245.82.37
94.245.82.38
SE : Stockholm
94.245.78.40
94.245.78.41
94.245.78.42
94.245.78.45
SG : Singapore
52.187.29.7
52.187.179.17
52.187.76.248
52.187.43.24
52.163.57.91
52.187.30.120
US : CA-San Jose
104.45.228.236
104.45.237.251
13.64.152.110
13.64.156.54
13.64.232.251
13.64.236.105
13.91.94.59
40.118.131.182
40.83.189.192
40.83.215.122
US : FL-Miami
65.54.78.49
65.54.78.50
65.54.78.51
65.54.78.54
65.54.78.57
65.54.78.58
65.54.78.59
65.54.78.60
US : IL-Chicago
23.96.247.139
23.96.249.113
52.162.124.242
52.162.126.139
52.162.241.147
52.162.246.222
52.162.247.136
52.237.153.231
52.237.154.216
52.237.156.14
52.237.157.218
52.237.157.37
US : TX-San Antonio
104.210.145.106
13.84.176.24
13.84.49.16
13.85.11.137
13.85.26.248
13.85.69.145
52.171.136.162
52.171.141.253
52.171.57.172
52.171.58.140
US : VA-Ashburn
13.82.218.95
13.90.96.71
13.90.98.52
13.92.137.70
40.85.187.235
40.87.61.61
52.168.8.247
52.170.38.79
52.170.80.61
52.179.9.26

```  

## <a name="data-access-api"></a>API доступа к данным
| Назначение | URI | IP-адрес | порты; |
| --- | --- | --- | --- |
| API |api.applicationinsights.io<br/>api1.applicationinsights.io<br/>api2.applicationinsights.io<br/>api3.applicationinsights.io<br/>api4.applicationinsights.io<br/>api5.applicationinsights.io |13.82.26.252<br/>40.76.213.73 |80, 443 |
| Документация по API |dev.applicationinsights.io<br/>dev.applicationinsights.microsoft.com<br/>dev.aisvc.visualstudio.com<br/>www.applicationinsights.io<br/>www.applicationinsights.microsoft.com<br/>www.aisvc.visualstudio.com |13.82.24.149<br/>40.114.82.10 |80, 443 |
| Внутренний API |aigs.aisvc.visualstudio.com<br/>aigs1.aisvc.visualstudio.com<br/>aigs2.aisvc.visualstudio.com<br/>aigs3.aisvc.visualstudio.com<br/>aigs4.aisvc.visualstudio.com<br/>aigs5.aisvc.visualstudio.com<br/>aigs6.aisvc.visualstudio.com |Динамический|443 |

## <a name="application-insights-analytics"></a>Аналитика Application Insights

| Назначение | URI | IP-адрес | порты; |
| --- | --- | --- | --- |
| Портал аналитики | analytics.applicationinsights.io | Динамический | 80, 443 |
| CDN | applicationanalytics.azureedge.net | Динамический | 80, 443 |
| Мультимедиа CDN | applicationanalyticsmedia.azureedge.net | Динамический | 80, 443 |

Примечание. Домен applicationinsights.io принадлежит команде Application Insights.

## <a name="application-insights-azure-portal-extension"></a>Расширение портала Azure для Application Insights

| Назначение | URI | IP-адрес | порты; |
| --- | --- | --- | --- |
| Расширение для Application Insights | stamp2.app.insightsportal.visualstudio.com | Динамический | 80, 443 |
| Расширение CDN для Application Insights | insightsportal-prod2-cdn.aisvc.visualstudio.com<br/>insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com<br/>insightsportal-cdn-aimon.applicationinsights.io | Динамический | 80, 443 |

## <a name="application-insights-sdks"></a>Пакеты средств разработки Application Insights

| Назначение | URI | IP-адрес | порты; |
| --- | --- | --- | --- |
| Пакеты средств разработки CDN JS Application Insights | az416426.vo.msecnd.net | Динамический | 80, 443 |
| Пакеты средств разработки Java Application Insights | aijavasdk.blob.core.windows.net | Динамический | 80, 443 |

## <a name="profiler"></a>Профилировщик

| Назначение | URI | IP-адрес | порты; |
| --- | --- | --- | --- |
| Агент | agent.azureserviceprofiler.net<br/>*.agent.azureserviceprofiler.net | Динамический | 443
| Microsoft Azure | gateway.azureserviceprofiler.net | Динамический | 443
| Хранилище | *.core.windows.net | Динамический | 443

## <a name="snapshot-debugger"></a>Отладчик моментальных снимков

| Назначение | URI | IP-адрес | порты; |
| --- | --- | --- | --- |
| Агент | ppe.azureserviceprofiler.net<br/>*.ppe.azureserviceprofiler.net | Динамический | 443
| Microsoft Azure | ppe.gateway.azureserviceprofiler.net | Динамический | 443
| Хранилище | *.core.windows.net | Динамический | 443
