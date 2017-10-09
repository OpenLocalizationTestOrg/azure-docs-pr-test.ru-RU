---
title: "Экспорт из Azure Application Insights tooSQL | Документы Microsoft"
description: "Постоянно Экспорт данных tooSQL Application Insights, с помощью Stream Analytics."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 48903032-2c99-4987-9948-d6e4559b4a63
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/06/2015
ms.author: bwren
ms.openlocfilehash: 58b579499113751a088dc7e66cbec71529773322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-export-toosql-from-application-insights-using-stream-analytics"></a>Пошаговое руководство: Экспорт tooSQL из Application Insights с помощью Stream Analytics
В этой статье показано, как toomove данные телеметрии из [Azure Application Insights] [ start] в базе данных Azure SQL с помощью [непрерывный Экспорт] [ export] и [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/). 

Непрерывный экспорт позволяет переместить данные телеметрии в службу хранилища Azure в формате JSON. Мы анализ hello объектов JSON, использование Azure Stream Analytics и создайте строки в таблицу базы данных.

(Как правило, непрерывного экспорта — toodo hello способом анализа телеметрии hello ваши приложения отправлять tooApplication аналитики. Можно адаптировать этот toodo образец кода прочего с hello экспортировать данные телеметрии, такие как статистическая обработка данных.)

Мы начнем с уже есть приложение hello требуется toomonitor допущения hello.

В этом примере мы используем данные представления страницы приветствия, но hello же шаблон можно легко расширить tooother типов данных, таких как пользовательские события и исключения. 

## <a name="add-application-insights-tooyour-application"></a>Добавить приложение tooyour Application Insights
tooget работы.

1. [Настройте Application Insights для веб-страниц](app-insights-javascript.md). 
   
    (В этом примере мы сосредоточимся на обработку данных представления страницы из hello клиентскими браузерами, но можно также настроить Application Insights для hello серверную часть вашей [Java](app-insights-java-get-started.md) или [ASP.NET](app-insights-asp-net.md) приложения и процесса запроса. зависимости и другие телеметрии server.)
2. Опубликуйте свое приложение и просмотрите данные телеметрии, появившиеся в ресурсе Application Insights.

## <a name="create-storage-in-azure"></a>Создание хранилища в Azure
Непрерывный Экспорт всегда выдает учетной записи хранилища Azure tooan данных, поэтому сначала требуется toocreate hello хранилища.

1. Создать учетную запись хранилища в подписке в hello [портал Azure][portal].
   
    ![На портале Azure выберите «Создать», «Данные», «Хранилище». Выберите «Классический» и щелкните «Создать». Введите имя хранилища.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. Создание контейнера
   
    ![В новое хранилище hello выберите контейнеры, щелкните плитку hello контейнеров, а затем добавить](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. Скопируйте ключ доступа к хранилищу hello
   
    Вам потребуется его скоро tooset hello ввода toohello stream analytics службы.
   
    ![В хранилище hello откройте параметры, ключи и сделайте копию hello первичный ключ доступа](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-tooazure-storage"></a>Запуск хранилища tooAzure непрерывный Экспорт
1. В hello портал Azure найдите ресурс Application Insights toohello, созданный для приложения.
   
    ![Выберите "Обзор", Application Insights, а затем выберите свое приложение.](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. Создайте непрерывный экспорт.
   
    ![Выберите "Параметры", "Непрерывный экспорт", "Добавить".](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    Выберите учетную запись хранения hello, созданную ранее:

    ![Задать назначение экспорта hello](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    Установите нужные типы событий hello toosee:

    ![Выберите типы событий.](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. Пусть данные накопятся. Предоставьте пользователям возможность поработать с приложением на протяжении некоторого времени. После получения данных телеметрии в [обозревателе метрик](app-insights-metrics-explorer.md) отобразятся статистические диаграммы, а в разделе [поиска по журналу диагностики](app-insights-diagnostic-search.md) — отдельные события. 
   
    И Кроме того, будет Экспорт tooyour хранилища данных hello. 
2. Проверки hello экспорта данных, либо на портале hello: Выбор **Обзор**, выберите учетную запись хранения, а затем **контейнеры** - или в Visual Studio. В Visual Studio откройте меню **"Вид" или "Обозреватель облака"**и выберите элемент "Azure" или "Хранилище". (Если у вас нет этот пункт меню, необходимо tooinstall hello Azure SDK: Откройте диалоговое окно нового проекта hello и откройте Visual C# / облако / получить Microsoft Azure SDK для .NET.)
   
    ![В Visual Studio откройте "Обозреватель сервера", "Azure", "Хранилище".](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    Запишите hello общую часть hello путь, который является производным от hello приложения имя и ключ инструментирования. 

Hello события записываются tooblob файлы в формате JSON. Каждый файл может содержать одно или несколько событий. Поэтому мы предлагаем данных события tooread hello и отфильтровать hello поля, которые должны. Существуют все виды вещей, которые можно было бы сделать с данными hello, но мы планируем на сегодняшний день является toouse Stream Analytics toomove hello данных tooa базы данных SQL. Чтобы легко toorun множество интересных запросов.

## <a name="create-an-azure-sql-database"></a>Создание базы данных SQL Azure
Еще раз, начиная с подпиской в [портал Azure][portal], создание hello базы данных (и новый сервер, пока у нас уже есть) toowhich вы напишете hello данных.

!["Создать", "Данные", SQL.](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

Убедитесь, что этот сервер базы данных hello разрешает доступ tooAzure служб:

![Обзор, серверы, server, параметры, брандмауэра tooAzure разрешить доступ](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a>Создание таблицы в базе данных SQL Azure
Подключите toohello базу данных, созданную в предыдущем разделе hello со средством управления предпочтительным. В этом пошаговом руководстве мы используем [инструменты управления SQL Server](https://msdn.microsoft.com/ms174173.aspx) (SSMS).

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

Создайте новый запрос и выполните следующий T-SQL hello:

```SQL

CREATE TABLE [dbo].[PageViewsTable](
    [pageName] [nvarchar](max) NOT NULL,
    [viewCount] [int] NOT NULL,
    [url] [nvarchar](max) NULL,
    [urlDataPort] [int] NULL,
    [urlDataprotocol] [nvarchar](50) NULL,
    [urlDataHost] [nvarchar](50) NULL,
    [urlDataBase] [nvarchar](50) NULL,
    [urlDataHashTag] [nvarchar](max) NULL,
    [eventTime] [datetime] NOT NULL,
    [isSynthetic] [nvarchar](50) NULL,
    [deviceId] [nvarchar](50) NULL,
    [deviceType] [nvarchar](50) NULL,
    [os] [nvarchar](50) NULL,
    [osVersion] [nvarchar](50) NULL,
    [locale] [nvarchar](50) NULL,
    [userAgent] [nvarchar](max) NULL,
    [browser] [nvarchar](50) NULL,
    [browserVersion] [nvarchar](50) NULL,
    [screenResolution] [nvarchar](50) NULL,
    [sessionId] [nvarchar](max) NULL,
    [sessionIsFirst] [nvarchar](50) NULL,
    [clientIp] [nvarchar](50) NULL,
    [continent] [nvarchar](50) NULL,
    [country] [nvarchar](50) NULL,
    [province] [nvarchar](50) NULL,
    [city] [nvarchar](50) NULL
)

CREATE CLUSTERED INDEX [pvTblIdx] ON [dbo].[PageViewsTable]
(
    [eventTime] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, SORT_IN_TEMPDB = OFF, DROP_EXISTING = OFF, ONLINE = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON)

```

![](./media/app-insights-code-sample-export-sql-stream-analytics/34-create-table.png)

В этом примере мы используем данные из представлений страниц. toosee hello другие данные, доступные, проверьте выходные данные JSON и разделе hello [Экспорт модели данных](app-insights-export-data-model.md).

## <a name="create-an-azure-stream-analytics-instance"></a>Создание экземпляра Azure Stream Analytics
Из hello [классический портал Azure](https://manage.windowsazure.com/), выберите службу hello Azure Stream Analytics и создайте новое задание Stream Analytics:

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

Когда создается новое задание hello, разверните его данные:

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a>Установка расположения большого двоичного объекта
Задайте tootake входные данные из вашей непрерывного экспорта больших двоичных объектов.

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

Теперь вам требуется hello первичный ключ доступа из вашей учетной записи хранилища, в котором записанные ранее. Настроить его как hello ключ учетной записи хранения.

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a>Установка шаблона префикса пути
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

Быть hello убедиться, что tooset формат даты слишком**гггг-мм-дд** (с **тире**).

Шаблон префикс пути Hello указывает, как Stream Analytics находит hello входных файлов в хранилище hello. Требуется tooset его toohow toocorrespond непрерывный Экспорт хранит данные hello. Задайте следующее значение:

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

В данном примере:

* `webapplication27`— Имя hello hello ресурс Application Insights **в нижнем регистре**. 
* `1234...`ключ инструментирования hello hello ресурс Application Insights **удалены два дефиса**. 
* `PageViews`hello тип данных, мы хотим tooanalyze. Доступные типы Hello зависят от фильтра hello, заданные в непрерывный экспорт. Просмотрите другие доступные типы hello экспортированных данных toosee hello и hello в разделе [Экспорт модели данных](app-insights-export-data-model.md).
* `/{date}/{time}` – шаблон, записанный буквально.

Имя tooget hello и iKey ресурса Application Insights, откройте Essentials на его «Обзор», или параметры.

#### <a name="finish-initial-setup"></a>Завершение начальной настройки
Подтверждение hello формат сериализации:

![Подтвердите выбор и закройте мастер.](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

Закройте мастер hello и дождитесь toocomplete установки hello.

> [!TIP]
> Используйте toocheck функция образец hello, правильно задать hello входного пути. В случае неудачи: Убедитесь, что в хранилище hello для выбранного диапазона времени образец hello данных. Изменить определение ввода hello и проверить набора hello учетной записи хранилища, префикс пути и Дата формат правильно.
> 
> 

## <a name="set-query"></a>Настройка запроса
Откройте раздел hello запроса:

![В Stream Analytics выберите "Запрос".](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

Замените запросов по умолчанию hello с:

```SQL

    SELECT flat.ArrayValue.name as pageName
    , flat.ArrayValue.count as viewCount
    , flat.ArrayValue.url as url
    , flat.ArrayValue.urlData.port as urlDataPort
    , flat.ArrayValue.urlData.protocol as urlDataprotocol
    , flat.ArrayValue.urlData.host as urlDataHost
    , flat.ArrayValue.urlData.base as urlDataBase
    , flat.ArrayValue.urlData.hashTag as urlDataHashTag
      ,A.context.data.eventTime as eventTime
      ,A.context.data.isSynthetic as isSynthetic
      ,A.context.device.id as deviceId
      ,A.context.device.type as deviceType
      ,A.context.device.os as os
      ,A.context.device.osVersion as osVersion
      ,A.context.device.locale as locale
      ,A.context.device.userAgent as userAgent
      ,A.context.device.browser as browser
      ,A.context.device.browserVersion as browserVersion
      ,A.context.device.screenResolution.value as screenResolution
      ,A.context.session.id as sessionId
      ,A.context.session.isFirst as sessionIsFirst
      ,A.context.location.clientip as clientIp
      ,A.context.location.continent as continent
      ,A.context.location.country as country
      ,A.context.location.province as province
      ,A.context.location.city as city
    INTO
      AIOutput
    FROM AIinput A
    CROSS APPLY GetElements(A.[view]) as flat


```

Обратите внимание, что сначала hello несколько свойств, определенных toopage представление данных. При экспорте телеметрии других типов будут получены другие свойства. В разделе hello [подробные справочные материалы по модели данных для значений и типы свойств hello.](app-insights-export-data-model.md)

## <a name="set-up-output-toodatabase"></a>Настройка вывода toodatabase
Выберите SQL в качестве выходных данных hello.

![В Stream Analytics выберите "Выходные данные".](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

Укажите базу данных SQL hello.

![Введите сведения о hello базы данных](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

Закройте мастер hello и ожидание уведомления, которые были настроены hello выходных данных.

## <a name="start-processing"></a>Начало обработки
Запустите задание hello hello панели действий:

![В Stream Analytics щелкните "Запуск".](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

Вы можете hello ли toostart обработки данных, начиная с сейчас или toostart с более ранние данные. последний Hello полезно в том случае, если у вас уже есть непрерывный экспорт, уже запущена в течение некоторого времени.

![В Stream Analytics щелкните "Запуск".](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

Через несколько минут средства управления сервером tooSQL вернуться назад и посмотрите, hello обмен данными в. Например, используйте запрос наподобие этого:

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a>Связанные статьи
* [С помощью Stream Analytics tooPowerBI экспорта](app-insights-export-power-bi.md)
* [Подробные данные модели ссылок для значений и типы свойств hello.](app-insights-export-data-model.md)
* [Непрерывный экспорт в Application Insights](app-insights-export-telemetry.md)
* [Application Insights](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

