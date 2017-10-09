---
title: "данные приложения Azure Application Insights aaaView | Документы Microsoft"
description: "Можно использовать проблем с производительностью toodiagnose решения hello соединитель аналитики приложений и понять, какие пользователи должны иметь вместе с приложением при мониторинге с помощью Application Insights."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 49280cad-3526-43e1-a365-c6a3bf66db52
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: banders
ms.openlocfilehash: 38109337ebbc8970dccb65365ba8284d9cee19a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-connector-solution-preview-in-operations-management-suite-oms"></a>Решение "Соединитель Application Insights" (предварительная версия) в Operations Management Suite (OMS)

![Символ Application Insights](./media/log-analytics-app-insights-connector/app-insights-connector-symbol.png)

Hello решения соединитель аналитики приложений служит для диагностики проблем с производительностью и понять, какие пользователи иметь приложения при его отслеживается с [Application Insights](../application-insights/app-insights-overview.md). Представления из hello же телеметрии приложения, разработчики в Application Insights, доступны в OMS. Тем не менее при интеграции приложений Application Insights с OMS видимость приложений увеличивается, так как данные операций и приложения находятся в одном месте. Того же hello представлений помогает toocollaborate с разработчиками вашего приложения. Общие представления Hello может помочь сократить время toodetect hello и разрешения приложения и проблем с платформой.

При использовании решения hello, вы можете:

- просматривать все приложения Application Insights в одном месте, даже если они находятся в разных подписках Azure;
- сопоставлять данные инфраструктуры с данными приложений;
- визуализировать данные приложения с перспективами в поиске по журналам;
- Сведения из приложения Application Insights tooyour данных аналитики журналов в hello OMS и порталов Azure

## <a name="connected-sources"></a>Подключенные источники

В отличие от большинства других решений анализа журналов данные не собираются для hello соединитель аналитики приложений агентами. Все данные, используемые решением hello получаются непосредственно из Azure.

| Подключенный источник | Поддерживаются | Описание |
| --- | --- | --- |
| [Агенты Windows](log-analytics-windows-agents.md) | Нет | решение Hello не собирать данные из агентов Windows. |
| [Агенты Linux](log-analytics-linux-agents.md) | Нет | решение Hello не собирать данные из агентов Linux. |
| [Группы управления SCOM](log-analytics-om-agents.md) | Нет | решение Hello не собирать данные из агентов в подключенной группе управления SCOM. |
| [Учетная запись хранения Azure](log-analytics-azure-storage.md) | Нет | решение Hello не не сбора сведений из хранилища Azure. |

## <a name="prerequisites"></a>Предварительные требования

- tooaccess сведения соединитель аналитики приложений, необходимо иметь подписку Azure
- Необходимо иметь хотя бы один настроенный ресурс Application Insights.
- Должен быть hello владельца или участника hello ресурс Application Insights.

## <a name="configuration"></a>Конфигурация

1. Включить решение Azure Web Analytics приложения hello из hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ApplicationInsights?tab=Overview) или с помощью hello процесс, описанный в [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md).
2. На портале OMS hello щелкните **параметры** &gt; **данные** &gt; **Application Insights**.
3. В разделе **Выбор подписки** выберите подписку с ресурсами Application Insights, а затем в разделе **Имя приложения** выберите одно или несколько приложений.
4. Щелкните **Сохранить**.

Около 30 минут данные становятся доступны и Application Insights плитки приветствия обновляется с данными, как hello после изображения:

![Плитка Application Insights](./media/log-analytics-app-insights-connector/app-insights-tile.png)

Другие точки tookeep помнить:

- Можно связать только рабочая область OMS tooone приложений Application Insights.
- Можно связать только [ресурсы Standard или Premium Application Insights](https://azure.microsoft.com/pricing/details/application-insights) tooOMS анализа журналов. Тем не менее можно использовать уровень Free hello аналитики журналов.

## <a name="management-packs"></a>Пакеты управления

В этом решении не предусматривается установка пакетов управления в подключенных группах управления.

## <a name="use-hello-solution"></a>Используйте решение hello

Hello следующих разделах описано, как можно использовать hello колонки, отображается в панели мониторинга tooview hello Application Insights и взаимодействовать с данными от приложений.

### <a name="view-application-insights-connector-information"></a>Просмотр сведений о соединителе Application Insights

Щелкните hello **Application Insights** плитки приветствия tooopen **Application Insights** следующие колонках hello toosee панели мониторинга.

![Панель мониторинга Application Insights](./media/log-analytics-app-insights-connector/app-insights-dash01.png)

![Панель мониторинга Application Insights](./media/log-analytics-app-insights-connector/app-insights-dash02.png)

панель мониторинга Hello включает колонках hello, приведенных в таблице hello. Каждой колонки перечислены вверх too10 сузьте указан, в колонке критерий hello области и временной диапазон. Можно выполнить поиск журнала, который возвращает все записи при нажатии кнопки **все** внизу hello колонка hello, или если щелкнуть заголовок колонки hello.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

| **Столбец** | **Описание** |
| --- | --- |
| Applications — Number of applications | Показывает номер hello приложений в ресурсы приложения. Также приложение списки имен и для каждой из них, hello количество записей приложения. Щелкните номер toorun hello поиск журнала<code>Type=ApplicationInsights &#124; measure sum(SampledCount) by ApplicationName</code> <br><br>  Щелкните toorun имя приложения поиска журналов приложения hello, записей приложения на узле, записей по типу данных телеметрии и все данные по типу (на основе hello последний день). |
| Data Volume — Hosts sending data | Показывает номер hello узлов компьютера, которые отправляют данные. Здесь также приводятся узлы компьютера и количество записей для каждого узла. Щелкните номер toorun hello поиск журнала<code>Type=ApplicationInsights &#124; measure sum(SampledCount) by Host</code> <br><br> Щелкните имя компьютера toorun поиска журналов для узла hello показаны записи приложения для каждого узла, записей по типу данных телеметрии и все данные по типу (на основе hello последний день). |
| Availability — Webtest results | Показывает кольцевую диаграмму с результатами веб-тестов, в которой указано, положительные они или отрицательные. Щелкните диаграмму toorun hello поиска журналов для<code>Type=ApplicationInsights TelemetryType=Availability &#124; measure sum(SampledCount) by AvailabilityResult</code> <br><br> Результаты показывают hello количество этапов и сбоев для всех тестов. Отображаются все веб-приложений с трафиком hello последнюю минуту. Щелкните имя приложения tooview поиска журналов, подробными сведениями о неудачных веб-тестов. |
| Server Requests — Requests per hour | Просмотреть диаграмму строку hello server запросов в час для различных приложений. Наведите курсор на строку hello диаграммы toosee hello первые 3 приложений получения запросов для точки времени. Также отображается список приложения hello, получающие запросы и hello число запросов для hello выбранного периода. <br><br>Нажмите кнопку hello graph toorun поиска журналов для <code>Type=ApplicationInsights TelemetryType=Request &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> , можно просмотреть диаграмму подробных строку hello server запросов в час для различных приложений. <br><br> Выберите приложение из списка toorun hello поиска журналов для <code>Type=ApplicationInsights  ApplicationName=yourapplicationname  TelemetryType=Request</code> коды ответа, отображается список запросов, диаграммы для запросов на протяжении времени и запрос и список запроса.   |
| Failures — Failed requests per hour | Показывает график со сведениями о количестве невыполненных запросов приложения в час. Наведите указатель мыши hello диаграммы toosee hello top 3 приложений с помощью невыполненных запросов для точки времени. Также отображает список приложений с использованием hello число невыполненных запросов для каждого. Щелкните диаграмму toorun hello поиска журналов для <code>Type=ApplicationInsights TelemetryType=Request  RequestSuccess = false &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> , отображающий подробные график запросов отказавшего приложения. <br><br>Щелкните элемент в списке toorun hello поиска журналов для <code>Type=ApplicationInsights ApplicationName=yourapplicationname TelemetryType=Request  RequestSuccess=false</code> , показывает количество неудачных запросов, диаграммы для неудачных запросов через длительность времени и запрос и список кодов ответа невыполненных запросов. |
| Exceptions — Exceptions per hour | Показывает график со сведениями о количестве исключений в час. Наведите указатель мыши hello диаграммы toosee hello основных 3 приложений с исключениями для точки времени. Также отображает список приложений с hello число исключений для каждого. Щелкните диаграмму toorun hello поиска журналов для <code>Type=ApplicationInsights TelemetryType=Exception &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> , можно просмотреть диаграмму связи подробных исключений. <br><br>Щелкните элемент в списке toorun hello поиска журналов для <code>Type=ApplicationInsights  ApplicationName=yourapplicationname TelemetryType=Exception</code> , отображается список исключений, диаграммы для исключения по времени и неудачные запросы и список типов исключений.  |

### <a name="view-hello-application-insights-perspective-with-log-search"></a>Просмотреть перспективы hello Application Insights с поиска журналов

Если щелкнуть любой элемент в панель мониторинга hello, вы видите точки зрения Application Insights, показанные в поиске. Перспектива Hello предоставляет расширенные визуализации, в зависимости от выбранного типа телеметрии hello. Таким образом содержимое визуализации изменяется для различных типов телеметрии.

Если щелкнуть в любом месте в колонке приложения hello, отображается по умолчанию hello **приложений** перспективы.

![Перспектива "Приложения" Application Insights](./media/log-analytics-app-insights-connector/applications-blade-drill-search.png)

перспективы Hello приведен обзор приложение hello, выбранное.

Hello **доступности** колонке показано представление другую перспективу, где можно просмотреть результаты веб-теста и связанные невыполненных запросов.

![Перспектива "Доступность" Application Insights](./media/log-analytics-app-insights-connector/availability-blade-drill-search.png)

Если щелкнуть в любом месте в hello **запросов к серверу** или **сбоев** колонки, изменяются компоненты toogive перспективы hello вы визуализации, связанные с toorequests.

![Колонка "Сбои" Application Insights](./media/log-analytics-app-insights-connector/server-requests-failures-drill-search.png)

Если щелкнуть в любом месте в hello **исключения** колонки, отображается визуализации, которые соответствуют tooexceptions.

![Колонка "Исключения" Application Insights](./media/log-analytics-app-insights-connector/exceptions-blade-drill-search.png)

Независимо от выбранного параметра — что-то одно hello **соединитель аналитики приложений** панели мониторинга в среде hello **поиска** страницы, любой запрос, возвращающий данные Application Insights показывают hello Перспектива аналитики приложений. Например, если вы просматриваете данные Application Insights **&#42;** запроса также показана вкладка перспективы hello как hello после изображения:

![Application Insights ](./media/log-analytics-app-insights-connector/app-insights-search.png)

Перспективы компоненты будут обновлены в зависимости от hello поискового запроса. Это означает, что можно фильтровать результаты hello с помощью поля поиска, дает hello toosee возможность hello данные из:

- всех ваших приложений;
- одного выбранного приложения;
- группы приложений.

### <a name="pivot-tooan-app-in-hello-azure-portal"></a>Приложение tooan со сводными данными в hello портал Azure

Колонки соединитель аналитики приложений являются спроектированный tooenable toopivot toohello выбранные приложения Application Insights *при использовании портала OMS hello*. Можно использовать решение hello как высокоуровневые мониторинга платформу, которая позволяет устранять неполадки в приложении. При появлении возможную проблему в одном из подключенных приложений, вы можете либо Исследуйте в поиске OMS или toohello приложения Application Insights позволяет прикрепить напрямую.

toopivot, нажмите кнопку с многоточием hello (**...** ), в конце каждой строки в hello и выберите пункт **открыт в Application Insights**.

>[!NOTE]
>**Открыть в Application Insights** недоступно в hello портал Azure.

![Открыть в Application Insights](./media/log-analytics-app-insights-connector/open-in-app-insights.png)

### <a name="sample-corrected-data"></a>Данные исправления выборки

Предоставляет Application Insights  *[выборки исправления](../application-insights/app-insights-sampling.md)*  toohelp уменьшить трафик телеметрии. При включении выборки в приложении Application Insights уменьшается количество записей, хранимых в Application Insights и в службе OMS. Во время проверки согласованности данных сохраняется в hello **соединитель аналитики приложений** страницы и перспектив, необходимо вручную исправить данные выборки для пользовательских запросов.

Ниже приведен пример исправления выборки в запросе поиска по журналам:

```
Type=ApplicationInsights | measure sum(SampledCount) by TelemetryType
```

Hello **выборки счетчика** во всех записях присутствует поле и отображает hello число точек данных, которые представляет запись hello. Если включить функцию выборки для вашего приложения Application Insights, значение поля **Sampled Count** (Количество данных выборки) будет больше 1. Фактическое число записей, которые приложение создает, сумма hello hello toocount **выборки счетчика** поля.

Выборка затрагивает только hello общее количество записей, которые приложение создает. Не требуется toocorrect выборки для метрики полей, таких как **RequestDuration** или **AvailabilityDuration** из-за этих полях отображаются hello среднее значение для представленного записи.

## <a name="input-data"></a>Входные данные

решение Hello получает hello следующие типы данных телеметрии из подключенных приложений Application Insights:

- Доступность
- Исключения
- Запросы
- Страница представления — для вашей рабочей области tooreceive просмотры страниц, toocollect вашего приложения необходимо настроить эти сведения. Дополнительные сведения см. в разделе [Просмотры страниц](../application-insights/app-insights-api-custom-events-metrics.md#page-views).
- Пользовательские события — для пользовательских событий tooreceive вашей рабочей области, необходимо настроить эти сведения toocollect вашего приложения. Дополнительные сведения см. в разделе [TrackEvent (Отслеживание событий)](../application-insights/app-insights-api-custom-events-metrics.md#trackevent).

Как только данные станут доступными, они поступают из Application Insights в OMS.

## <a name="output-data"></a>Выходные данные

Для каждого типа входных данных создается запись с данными о *типе* *ApplicationInsights*. ApplicationInsights записи имеют свойства, показанные в следующих разделах hello:

### <a name="generic-fields"></a>Универсальные поля

| Свойство | Описание |
| --- | --- |
| Тип | ApplicationInsights |
| ClientIP |   |
| TimeGenerated | Время записи hello |
| ApplicationId | Ключ инструментирования Application Insights приложения hello |
| ApplicationName | Имя приложения hello Application Insights |
| RoleInstance | Идентификатор узла сервера |
| DeviceType | Устройство клиента |
| ScreenResolution |   |
| Continent | Континент, где был сформирован запрос hello |
| Страна | Страна, где был сформирован запрос hello |
| Province | Край, состояние или где hello источником запроса языкового стандарта |
| City | Города, где был сформирован запрос hello |
| isSynthetic | Указывает, была создана hello запроса пользователем или автоматически. Значение true означает, что запрос создан пользователем, а значение false — автоматически |
| SamplingRate | Процент создаваемых hello SDK, который отправляется tooportal телеметрии. Диапазон 0,0–100,0. |
| SampledCount | 100/(частота выборки). Например, 4 = &gt; 25 %. |
| IsAuthenticated | Значение true или false |
| OperationID | Элементы, имеющие hello таким же Идентификатором операции отображаются в виде связанных элементов портала hello. Идентификатор запроса обычно hello |
| ParentOperationID | Идентификатор родительской операции hello |
| OperationName |   |
| SessionId | GUID toouniquely идентификации сеанса hello, где был создан запрос hello |
| SourceSystem | ApplicationInsights |

### <a name="availability-specific-fields"></a>Поля со сведениями о доступности

| Свойство | Описание |
| --- | --- |
| TelemetryType | Доступность |
| AvailabilityTestName | Имя веб-теста hello |
| AvailabilityRunLocation | Географический источник HTTP-запроса |
| AvailabilityResult | Указывает hello успешный результат hello веб-теста |
| AvailabilityMessage | приветственное сообщение присоединенного toohello веб-теста |
| AvailabilityCount | 100/(частота выборки). Например, 4 = &gt; 25 %. |
| DataSizeMetricValue | 1,0 или 0,0. |
| DataSizeMetricCount | 100/(частота выборки). Например, 4 = &gt; 25 %. |
| AvailabilityDuration | Время (в миллисекундах) длительность теста hello web |
| AvailabilityDurationCount | 100/(частота выборки). Например, 4 = &gt; 25 %. |
| AvailabilityValue |   |
| AvailabilityMetricCount |   |
| AvailabilityTestId | Уникальный идентификатор GUID для hello веб-теста |
| AvailabilityTimestamp | Точные метки времени теста доступности hello |
| AvailabilityDurationMin | Для выборки записей в этом поле отображается продолжительность теста hello минимальное web (в миллисекундах) для точек данных представлены hello |
| AvailabilityDurationMax | Для выборки записей в этом поле отображается продолжительность теста hello максимальное web (в миллисекундах) для точек данных представлены hello |
| AvailabilityDurationStdDev | Для выборки записей в этом поле показан hello стандартное отклонение между длительность всех веб-теста (в миллисекундах) для точек данных представлены hello |
| AvailabilityMin |   |
| AvailabilityMax |   |
| AvailabilityStdDev | &nbsp;  |

### <a name="exception-specific-fields"></a>Поля со сведениями об исключениях

| Тип | ApplicationInsights |
| --- | --- |
| TelemetryType | Исключение |
| ExceptionType | Тип исключения hello |
| ExceptionMethod | метод Hello, который создает исключение hello |
| ExceptionAssembly | Сборка включает hello framework и версия а также токен открытого ключа hello |
| ExceptionGroup | Тип исключения hello |
| ExceptionHandledAt | Указывает уровень hello, обработавшего исключение hello |
| ExceptionCount | 100/(частота выборки). Например, 4 = &gt; 25 %. |
| ExceptionMessage | Сообщение hello исключения |
| ExceptionStack | Полный стек исключений hello |
| ExceptionHasStack | Значение true, если исключение содержит стек |



### <a name="request-specific-fields"></a>Поля со сведениями о запросах

| Свойство | Описание |
| --- | --- |
| Тип | ApplicationInsights |
| TelemetryType | Запрос |
| ResponseCode | Отправлено ответов tooclient HTTP |
| RequestSuccess | Указывает успешное или неудачное выполнение. Значение true или false. |
| RequestID | Идентификатор toouniquely идентификации hello запроса |
| RequestName | GET или POST + базовый URL-адрес |
| RequestDuration | Время в секундах для hello длительность запроса |
| URL-адрес | URL-адрес запроса hello, без учета узла |
| Узел | Узел веб-сервера |
| URLBase | Полный URL-адрес запроса hello |
| ApplicationProtocol | Тип протокола, используемого приложением hello |
| RequestCount | 100/(частота выборки). Например, 4 = &gt; 25 %. |
| RequestDurationCount | 100/(частота выборки). Например, 4 = &gt; 25 %. |
| RequestDurationMin | Для выборки записей в этом поле отображается длительность hello минимальное запроса (в миллисекундах) для точек данных представлены hello. |
| RequestDurationMax | Для выборки записей в этом поле показан hello Максимальная длительность запроса (в миллисекундах) для точек данных представлены hello |
| RequestDurationStdDev | Для выборки записей в этом поле показан hello стандартное отклонение от всех длительность запроса (в миллисекундах) для точек данных представлены hello |

## <a name="sample-log-searches"></a>Пример поисков журналов

Это решение не имеет набор образца запросов поиска журналов отображаются на панели мониторинга hello. Тем не менее, пример запросов поиска журналов с описаниями отображаются в hello [сведения соединитель аналитики приложений представление](#view-application-insights-connector-information) раздела.

## <a name="next-steps"></a>Дальнейшие действия

- Используйте [поиска журналов](log-analytics-log-searches.md) tooview подробные сведения о приложениях Application Insights.
