---
title: "aaaUsing аналитика - hello мощное средство аналитики приложений Azure | Документы Microsoft"
description: "С помощью hello Analytics hello мощное средство диагностики поиска средство аналитики приложений. "
services: application-insights
documentationcenter: 
author: danhadari
manager: carmonm
ms.assetid: c3b34430-f592-4c32-b900-e9f50ca096b3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6e0246848457db368c57d08c47b5bf73f4e5e3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-analytics-in-application-insights"></a>Использование аналитики в Application Insights
[Аналитика](app-insights-analytics.md) — мощное средство поиска функция hello [Application Insights](app-insights-overview.md). На этих страницах описан язык запросов Log Analytics.

* **[Вводное видео hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Испытайте аналитика на нашем смоделированные данные](https://analytics.applicationinsights.io/demo)**  Если ваше приложение еще не отправляет данные tooApplication аналитики.

## <a name="open-analytics"></a>Открытие аналитики
В домашнем ресурсе вашего приложения в Application Insights щелкните "Аналитика".

![На сайте portal.azure.com откройте ресурс Application Insights и щелкните "Аналитика".](./media/app-insights-analytics-using/001.png)

Hello встроенного учебник дает некоторые сведения о возможностях.

Смотрите [исчерпывающий обзор здесь](app-insights-analytics-tour.md).

## <a name="query-your-telemetry"></a>Запрос данных телеметрии
### <a name="write-a-query"></a>Напишите запрос
![Отображение схемы](./media/app-insights-analytics-using/150.png)

Начать с именами hello какой-либо таблицы hello в списке слева hello (или hello [диапазон](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) или [объединение](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) операторы). Используйте `|` toocreate в конвейер [операторы](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html). 

IntelliSense предлагает операторы hello и элементы hello выражений, которые можно использовать. Щелкните значок сведений hello (или нажмите клавиши CTRL + ПРОБЕЛ) tooget подробное описание и примеры toouse каждого элемента.

В разделе hello [обзор языка Analytics](app-insights-analytics-tour.md) и [Справочник по языку](app-insights-analytics-reference.md).

### <a name="run-a-query"></a>Выполнение запроса
![Выполнение запроса](./media/app-insights-analytics-using/130.png)

1. В запросе можно использовать только однократные разрывы строк.
2. Поместите курсор hello внутри или в конце hello hello запроса, который должен toorun.
3. Проверьте hello диапазон времени запроса. (Его можно изменить или переопределить, добавив в запрос собственное предложение [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html).)
3. Нажмите кнопку Go toorun hello запрос.
4. Не помещайте в запрос пустые строки. На одной вкладке запроса можно хранить несколько отдельных запросов, разделив их пустыми строками. Выполняется только hello запроса с курсором hello.

### <a name="save-a-query"></a>Сохранение запроса
![Сохранение запроса](./media/app-insights-analytics-using/140.png)

1. Сохраните текущий файл запрос hello.
2. Откройте сохраненный файл запроса.
3. Создайте новый файл запроса.

## <a name="see-hello-details"></a>Просмотреть сведения о hello
Разверните любую строку в toosee результаты hello его полный список свойств. Далее можно развернуть любое свойство, например со структурированными значениями -, пользовательские измерения или стек hello в исключение.

![Развертывание строки](./media/app-insights-analytics-using/070.png)

## <a name="arrange-hello-results"></a>Упорядочить результаты hello
Можно сортировать, фильтровать, разбиение на страницы и группы hello результаты, возвращаемые из запроса.

> [!NOTE]
> Сортировка, Группировка и фильтрация в браузере hello не повторно выполнить запрос. Они только изменить hello результаты, возвращенные последнего запроса. 
> 
> tooperform этих задач в сервере hello, прежде чем hello результатов, написать собственный запрос с hello [сортировки](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [суммировать](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) и [где](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) операторы.
> 
> 

Выбрать столбцы hello и как toosee, перетащите toorearrange заголовки столбцов, а также изменить размер столбцов, перетаскивая их границы.

![Упорядочивание столбцов](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a>Сортировка и фильтрация элементов
Результаты сортировки, щелкнув hello заголовка столбца. Снова щелкните toosort hello другим способом, а нажмите кнопку в третий раз toorevert toohello исходный порядок возвращаемые запросом.

Используйте значок toonarrow hello фильтр поиска.

![Сортировка и фильтрация столбцов](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a>Группирование элементов
toosort по нескольким столбцам, используют группирование. Сначала ее включить, а затем перетащите заголовки столбцов в пространство hello над таблицей hello.

![Группа](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a>Если некоторые результаты отсутствуют

Если вы считаете, что вы не видите все ожидаемые результаты hello, существует несколько возможных причин.

* **Фильтр диапазона времени**. По умолчанию вы увидите только результаты из hello последние 24 часа. Нет автоматический фильтр, который ограничивает диапазон hello результатов, которые извлекаются из исходных таблиц hello. 

    Тем не менее, можно изменить диапазон времени hello фильтра с помощью раскрывающегося меню hello.

    Или можно переопределить hello автоматическое изменение диапазона, включая свою собственную [ `where  ... timestamp ...` предложение](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) в свой запрос. Например:

    `requests | where timestamp > ago('2d')`

* **Ограничение результатов**. Ограничено 10 тысяч строк на hello результаты, возвращаемые из портала hello. Предупреждение показывает, переходе превышении hello. В этом случае Сортировка результатов в таблице hello не всегда показывают все hello фактические первой или последней результаты. 

    Это ограничение hello попадание tooavoid рекомендаций. Использовать фильтр по диапазону времени hello, или использовать операторы, такие как:

  * [top 100 by timestamp;](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [take 100;](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [summarize ](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [where timestamp > ago(3d)](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

(Требуется более 10 тысяч строк? Рассмотрите возможность использования [непрерывного экспорта](app-insights-export-telemetry.md). Аналитика предназначена для анализа, а не получения необработанных данных.)

## <a name="diagrams"></a>Схемы
Выберите тип диаграммы, которую вы хотите hello:

![Выберите тип диаграммы](./media/app-insights-analytics-using/230.png)

Если имеется несколько столбцов типов правой hello, вы можете hello x и оси y и столбец измерения toosplit hello результаты по.

По умолчанию изначально результаты отображаются в виде таблицы и диаграммы hello выбрать вручную. Но вы можете использовать hello [визуализации директива](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) конце hello запроса tooselect диаграмму.

### <a name="analytics-diagnostics"></a>Диагностика аналитики


На timechart Если неожиданный всплеск или этапа в данных, может появиться точки выделенной строке hello. Это означает, что аналитика диагностики определил сочетания свойств, которые отфильтровать hello внезапные изменения. Дополнительные сведения о фильтрации hello и toosee hello отфильтрованной версии нажмите кнопку tooget точки hello. Это может помочь определить, какие изменения вызвало hello. 

[Диагностика внезапных изменений в телеметрии приложения](app-insights-analytics-diagnostics.md)


![Диагностика аналитики](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-toodashboard"></a>Toodashboard ПИН-кода
Вы можете закрепить tooone схему или таблицу из вашего [общих панелей мониторинга](app-insights-dashboards.md) -просто щелкните hello ПИН-код. (Может потребоваться слишком[обновления приложения тарифного пакета](app-insights-pricing.md) tooturn эту функцию.) 

![Нажмите кнопку hello ПИН-кода](./media/app-insights-analytics-using/pin-01.png)

Это означает, что при сборке toohelp панели мониторинга, мониторинг производительности hello или использования веб-служб, можно включить довольно сложными analysis рядом с hello другие показатели. 

Можно закрепить панель мониторинга toohello таблицы, если у него есть четыре или меньшее число столбцов. Отображаются только hello первые семь строк.

### <a name="dashboard-refresh"></a>Обновление панели мониторинга
мониторинга toohello Hello закрепить диаграммы автоматически обновляются примерно каждые часов повторным запуском запроса hello. Кроме того, можно нажать кнопку обновления hello.

### <a name="automatic-simplifications"></a>Автоматические упрощения

Определенные упрощения, примененные tooa диаграммы, когда вы Закрепить панель мониторинга tooa.

**Ограничение времени:** запросы, ограничивают выбор toohello за последние 14 дней. Hello эффект hello же, как если запрос включает `where timestamp > ago(14d)`.

**Ограничение на количество ячеек:** Если отобразить диаграмму, которая содержит много дискретных ячейки (обычно линейчатую диаграмму), меньше заполненных ячеек автоматически группируются в одном «другие» hello ячейки. Например, запрос

    requests | summarize count_search = count() by client_CountryOrRegion

в аналитике выглядит следующим образом:

![Диаграмма с длинным "хвостом"](./media/app-insights-analytics-using/pin-07.png)

Однако при закреплении его tooa панели мониторинга, он выглядит следующим образом:

![Диаграмма с ограниченным количеством ячеек](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-tooexcel"></a>Экспортировать tooExcel
После выполнения запроса можно скачать CSV-файл. Щелкните **"Экспорт", Excel**.

## <a name="export-toopower-bi"></a>Экспорт tooPower бизнес-Аналитики
Поместите курсор hello в запросе и выберите **экспорта Power BI**.

![Экспорт из Analytics tooPower бизнес-Аналитики](./media/app-insights-analytics-using/240.png)

При выполнении запроса hello в Power BI Может быть задана toorefresh по расписанию.

С помощью Power BI вы можете создавать панели мониторинга, объединяющие данные из разных источников.

[Дополнительные сведения об экспорте tooPower бизнес-Аналитики](app-insights-export-power-bi.md)

## <a name="deep-link"></a>Прямая ссылка

Получить ссылку в разделе **Экспорт общей ссылки** следует отправить tooanother пользователя. Предоставляемый пользователем hello [группы ресурсов tooyour доступ](app-insights-resources-roles-access-control.md), hello запрос будет открываться в hello Analytics пользовательского интерфейса.

(В ссылке hello hello текст запроса появляется после «? q =», сжимаются gzip и в кодировке base-64. Можно написать код toogenerate прямые ссылки необходимо указать toousers. Однако рекомендуется использовать hello toorun способом Analytics из кода можно с помощью hello [API-интерфейса REST](https://dev.applicationinsights.io/).)


## <a name="automation"></a>Служба автоматизации

Используйте hello [REST API-Интерфейс](https://dev.applicationinsights.io/) toorun аналитические запросы. [Пример](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (использование PowerShell):

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

В отличие от hello Analytics пользовательского интерфейса hello API-интерфейса REST автоматически не добавляются все запросы tooyour ограничение отметки времени. Помните tooadd собственные-предложения where, tooavoid получения огромный ответов.



## <a name="import-data"></a>Импорт данных

Можно импортировать данные из CSV-файла. Типичным использованием является tooimport статические данные, можно присоединить с таблицами, с помощью телеметрии. 

Например в случае прошедших проверку подлинности пользователей в телеметрии скрытый идентификатор или псевдоним, можно импортировать таблицу, которая сопоставляет имена tooreal псевдонимы. В результате соединения hello телеметрии запроса, можно определить пользователей, их реальные имена в отчетах аналитики hello.

### <a name="define-your-data-schema"></a>Определение схемы данных

1. Щелкните **Параметры** (в верхнем левом углу) и выберите **Источники данных**. 
2. Добавление источника данных, следуя инструкциям hello. Вы являетесь задаваемые toosupply образец hello данных, который должен содержать по крайней мере 10 строк. Исправьте схему hello.

Определяет источник данных, который затем можно будет использовать tooimport отдельных таблиц.

### <a name="import-a-table"></a>Импорт таблицы

1. Откройте определение источника данных из списка hello.
2. Нажмите кнопку «Отправить» и следуйте hello инструкции tooupload hello таблицы. Это включает в себя tooa вызова интерфейса API REST, и в этом случае легко tooautomate. 

Таблица теперь доступна для использования в запросах аналитики. Она будет отображаться в Аналитике. 

### <a name="use-hello-table"></a>Используйте таблицу hello

Предположим, что определение источника данных называется `usermap` и содержит два поля, `realName` и `user_AuthenticatedId`. Hello `requests` таблица также содержит поле с именем `user_AuthenticatedId`, поэтому его легко toojoin их:

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
Hello результирующая таблица запросов имеет дополнительный столбец, `realName`.

### <a name="import-from-logstash"></a>Импорт из LogStash

Если вы используете [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), можно использовать tooquery аналитика журналов. Используйте hello [подключаемого модуля, который передает данные в Analytics](https://github.com/Microsoft/logstash-output-application-insights). 

## <a name="video"></a>Видео

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

