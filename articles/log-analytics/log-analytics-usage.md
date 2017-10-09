---
title: "Использование данных aaaAnalyze в службе анализа журналов | Документы Microsoft"
description: "Используйте панель мониторинга использования hello в tooview аналитики журналов, какой объем данных, отправляемых toohello службы анализа журналов и определить причину отправки больших объемов данных."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 74d0adcb-4dc2-425e-8b62-c65537cef270
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: magoedte
ms.openlocfilehash: c30373dd6edbe3ff900fbebc865575fee61ce14c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-usage-in-log-analytics"></a>Анализ использования данных в службе Log Analytics
Служба аналитики журналов содержатся сведения о hello объем данных собираются, отправившему компьютеров hello данных и различные типы данных, отправляемых hello.  Используйте hello **журналами Analytics** toohello Служба аналитики журнала отправлено мониторинга toosee hello объем данных. Hello панели мониторинга отображается объем данных собираются по каждому решению и какой объем данных компьютеры отправляют.

## <a name="understand-hello-usage-dashboard"></a>Понимать мониторинга использования hello
Hello **анализа журналов использования** панель мониторинга отображает hello следующую информацию:

- Объем данных:
    - объем данных по времени (зависит от текущего периода времени);
    - объем данных для каждого решения;
    - данные, не связанные с компьютером.
- Компьютеры
    - компьютеры, отправляющие данные;
    - компьютеры без данных за последние 24 часа.
- Предложения:
    - узлы Insight and Analytics;
    - узлы автоматизации и управления;
    - узлы безопасности.
- Производительность
    - Время, затраченное toocollect и данные индекса
- список запросов.

![панель мониторинга "Использование"](./media/log-analytics-usage/usage-dashboard01.png)

### <a name="toowork-with-usage-data"></a>toowork с данными об использовании
1. Если это еще не сделано, войдите в toohello [портал Azure](https://portal.azure.com) с помощью вашей подписки Azure.
2. На hello **концентратора** меню, нажмите кнопку **дополнительные службы** и введите в список ресурсов hello, **анализа журналов**. Началом ввода hello список фильтров на основе ввода. Щелкните **Log Analytics**.  
    ![Концентратор Azure](./media/log-analytics-usage/hub.png)
3. Hello **анализа журналов** панели отображается список рабочих областей. Выберите рабочую область.
4. В hello *рабочей* панели мониторинга, щелкните **анализа журналов использования**.
5. На hello **журналами Analytics** панели мониторинга, щелкните **время: последние 24 часа** toochange hello временной интервал.  
    ![период времени](./media/log-analytics-usage/time.png)
6. Представление использования hello категории колонках которых отображаются интересующие вас интересует. Выберите панель и щелкните элемент в нем tooview, Дополнительные сведения см в [поиска журналов](log-analytics-log-searches.md).  
    ![пример колонки использования данных](./media/log-analytics-usage/blade.png)
7. На панели поиска журналов hello просмотрите hello результатов, возвращаемых из поиска hello.  
    ![пример поиска по журналу использования](./media/log-analytics-usage/usage-log-search.png)

## <a name="create-an-alert-when-data-collection-is-higher-than-expected"></a>Создание оповещения для превышенного объема сбора данных
В этом разделе описываются как toocreate оповещение, если:
- объем данных превышает заданный объем;
- Том данных имеет прогнозируемых tooexceed заданного значения.

[Оповещения](log-analytics-alerts-creating.md) Log Analytics используют поисковые запросы. Hello следующий запрос имеет результат при наличии более чем 100 ГБ данных, собранных в hello последние 24 часа:

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`

Hello следующий запрос использует простой формулы toopredict при более чем 100 ГБ данных, которые будут отправляться в день: 

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`

tooalert на томе данных, изменение hello 100 в hello запрашивает toohello число требуются tooalert ГБ.

Используйте hello действия, описанные в [создать правило оповещения](log-analytics-alerts-creating.md#create-an-alert-rule) toobe уведомление, когда сбор данных будет выше, чем ожидалось.

При создании hello предупреждение для hello первый запрос — при наличии более чем 100 ГБ данных в течение 24 часов задать:
- **Имя** слишком*объем данных превышает 100 ГБ в течение 24 часов*
- **Серьезность** слишком*предупреждение*
- **Запрос поиска** слишком`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`
- **Временное окно** слишком*24 часа*.
- **Предупреждения частоты** toobe один час, так как данные об использовании hello обновляется только один раз в час.
- **Создать предупреждение на основе** toobe *число результатов*
- **Количество результатов** toobe *больше 0*

Используйте hello действия, описанные в [добавить правила tooalert действия](log-analytics-alerts-actions.md) настройку действия электронной почты, веб-перехватчик или runbook для правила оповещения hello.

Если создание hello предупреждение для hello второй запрос — при прогнозируется, что будет более 100 ГБ данных в течение 24 часов значение:
- **Имя** слишком*toogreater более 100 ГБ и ожидается интенсивный данные за 24 часа*
- **Серьезность** слишком*предупреждение*
- **Запрос поиска** слишком`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`
- **Временное окно** слишком*3 часа*.
- **Предупреждения частоты** toobe один час, так как данные об использовании hello обновляется только один раз в час.
- **Создать предупреждение на основе** toobe *число результатов*
- **Количество результатов** toobe *больше 0*

Когда вы получаете предупреждение, выполните действия hello в hello следующий раздел tootroubleshoot, почему использования больше, чем ожидалось.

## <a name="troubleshooting-why-usage-is-higher-than-expected"></a>Превышенный объем данных: причины и устранение
панели мониторинга использования Hello помогает tooidentify почему использование (и поэтому затрат) больше, чем вы ожидали.

Превышенное использование вызывается одной (или двумя) причинами:
- Больше данных, чем ожидалось, отправляемых tooLog аналитика
- Больше узлов, чем ожидалось, отправка данных tooLog аналитика

### <a name="check-if-there-is-more-data-than-expected"></a>Проверьте, превышен ли объем данных 
Существует два ключа раздела страница использования hello, помогающие определить причину hello собранные toobe большинство данных.

Hello *тома данных со временем* диаграмма показывает общий объем данных, отправляемых hello и hello компьютеров, отправляющих hello большую часть данных. Hello диаграммы вверху hello позволяет toosee при использовании веб-данных в целом растет осталось неизменным или убывания. Hello компьютеров перечислены hello 10 компьютеров, отправляющих hello большую часть данных.

Hello *объем данных в зависимости от решения* диаграмма отображает hello объем данных, который отправляется службой каждого решения и решения hello, отправка hello большинство данных. Диаграмма Hello вверху hello показывает общий объем данных, отправляемых для каждого решения со временем hello. Эти сведения позволяют tooidentify ли решение отправляет дополнительные данные, о hello же сумму данных или меньше данных со временем. список решений Hello показаны hello 10 решения, отправка hello большинство данных. 

На этих двух диаграммах отображаются все данные. Одни данные оплачиваются, другие — нет. toofocus только с данными, оплачиваемых изменить запрос hello на tooinclude страницу поиска hello `IsBillable=true`.  

![диаграммы объема данных](./media/log-analytics-usage/log-analytics-usage-data-volume.png)

Рассмотрим hello *тома данных со временем* диаграммы. toosee hello решения и типы данных, которые отправляют hello большинство данных для конкретного компьютера, щелкните имя hello hello компьютера. Щелкните имя hello hello первого компьютера в список hello.

В следующий снимок экрана приветствия, hello *управления журналами и производительности* тип данных передает hello большинство данных для компьютера hello. 

![Объем данных для компьютера](./media/log-analytics-usage/log-analytics-usage-data-volume-computer.png)

Теперь перейдите toohello *использование* панели мониторинга и посмотрите на hello *объем данных в зависимости от решения* диаграммы. компьютеры hello toosee Отправка hello большинство данных для решения, щелкните имя hello hello решения в списке hello. Щелкните имя hello hello первое решение в списке hello. 

В следующий снимок экрана приветствия, это подтверждает, что hello *acmetomcat* компьютер отправляет hello большинство данных в решении по управлению журнала hello.

![объем данных для решения](./media/log-analytics-usage/log-analytics-usage-data-volume-solution.png)

При необходимости выполните дополнительный анализ tooidentify больших томов в типе данных или решения. Примеры запросов приведены ниже.

+ Решение по **безопасности**
  - `Type=SecurityEvent | measure count() by EventID`
+ Решение для **управления журналами**
  - `Type=Usage Solution=LogManagement IsBillable=true | measure count() by DataType`
+ Тип данных **Perf**
  - `Type=Perf | measure count() by CounterPath`
  - `Type=Perf | measure count() by CounterName`
+ Тип данных **Event**
  - `Type=Event | measure count() by EventID`
  - `Type=Event | measure count() by EventLog, EventLevelName`
+ Тип данных **Syslog**
  - `Type=Syslog | measure count() by Facility, SeverityLevel`
  - `Type=Syslog | measure count() by ProcessName`
+ Тип данных **AzureDiagnostics**
  - `Type=AzureDiagnostics | measure count() by ResourceProvider, ResourceId`

Используйте следующие шаги tooreduce hello объем сохраняемых журналов hello.

| Источник превышенного объема данных | Как tooreduce тома данных |
| -------------------------- | ------------------------- |
| События безопасности            | Выберите [события со стандартным или минимальным уровнем безопасности](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/). <br> Изменить hello политики требуется только toocollect себя события аудита безопасности. В частности просмотрите hello необходимость toocollect событий для <br> - [аудит платформы фильтрации](https://technet.microsoft.com/library/dd772749(WS.10).aspx); <br> - [аудит реестра](https://docs.microsoft.com/windows/device-security/auditing/audit-registry);<br> - [аудит файловой системы](https://docs.microsoft.com/windows/device-security/auditing/audit-file-system);<br> - [аудит объектов ядра](https://docs.microsoft.com/windows/device-security/auditing/audit-kernel-object);<br> - [аудит работы с дескрипторами](https://docs.microsoft.com/windows/device-security/auditing/audit-handle-manipulation);<br> - [аудит съемных носителей](https://docs.microsoft.com/windows/device-security/auditing/audit-removable-storage). |
| Счетчики производительности       | Измените [конфигурацию счетчика производительности](log-analytics-data-sources-performance-counters.md), чтобы <br> -Уменьшить частоту сбора hello <br> сократить число счетчиков производительности. |
| Журналы событий                 | Измените [конфигурацию журнала событий](log-analytics-data-sources-windows-events.md), чтобы <br> -Reduce hello число сохраняемых журналов событий <br> выполнять сбор только необходимых уровней событий. Например, не выполняйте сбор событий уровня *сведений*. |
| syslog                     | Измените [конфигурацию системного журнала](log-analytics-data-sources-syslog.md), чтобы <br> -Сократите число hello помещений собраны <br> выполнять сбор только необходимых уровней событий. Например, не выполняйте сбор событий уровня *сведений* и *отладки*. |
| AzureDiagnostics           | Измените коллекцию журнала ресурсов, чтобы: <br> -Reduce hello количество ресурсов отправки журналов tooLog аналитика <br> Выполнять сбор только необходимых журналов. |
| Решение данные с компьютеров, которым не требуется решение hello | Используйте [решений, предназначенных для](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect данные из только требуемые группы компьютеров. |

### <a name="check-if-there-are-more-nodes-than-expected"></a>Проверьте, превышено ли число узлов
Если вы работаете с hello *каждого узла (OMS)* в ценовой категории, а затем взимается плата на основе hello числа узлов и решений можно использовать. Можно увидеть, сколько узлов каждое предложение используются в hello *предложений* панели мониторинга использования hello.

![панель мониторинга "Использование"](./media/log-analytics-usage/log-analytics-usage-offerings.png)

Щелкните **просмотреть все...**  tooview hello полный список компьютеров, отправляющих данные для выбранного предложения hello.

Используйте [решений, предназначенных для](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect данные из только требуемые группы компьютеров.


## <a name="next-steps"></a>Дальнейшие действия
* В разделе [входа поиска аналитики журналов](log-analytics-log-searches.md) toolearn как toouse hello поиск языка. Поиск запросов tooperform дополнительного анализа можно использовать hello данных по использованию.
* Используйте hello действия, описанные в [создать правило оповещения](log-analytics-alerts-creating.md#create-an-alert-rule) выполнены toobe уведомления, когда условия поиска
* Используйте [решений, предназначенных для](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect данные из только требуемые группы компьютеров
* Выберите [события со стандартным или минимальным уровнем безопасности](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/).
* Измените [конфигурацию счетчика производительности](log-analytics-data-sources-performance-counters.md).
* Измените [конфигурацию журнала событий](log-analytics-data-sources-windows-events.md).
* Измените [конфигурацию системного журнала](log-analytics-data-sources-syslog.md).
