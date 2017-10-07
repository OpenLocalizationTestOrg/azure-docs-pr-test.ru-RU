---
title: "с помощью Stream Analytics из Azure Application Insights aaaExport | Документы Microsoft"
description: "Stream Analytics можно постоянно преобразования, фильтр и hello данные маршрута, экспортированные из Application Insights."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 31594221-17bd-4e5e-9534-950f3b022209
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: fda9b64f588c520833b2669eafdf650efc3de6be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-stream-analytics-tooprocess-exported-data-from-application-insights"></a>Используйте Stream Analytics tooprocess экспортированных данных из Application Insights
[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) hello идеальным средством для обработки данных — [экспортированы из Application Insights](app-insights-export-telemetry.md). Stream Analytics может извлекать данные из различных источников. Его преобразования и фильтрации данных hello и затем направлять tooa различных приемников.

В этом примере мы создадим адаптер, который импортирует данные из Application Insights, переименование и обрабатывает некоторые поля hello и направляет его в Power BI.

> [!WARNING]
> Существуют значительно улучшают и упрощают [рекомендуемым методом toodisplay Application Insights данных в Power BI](app-insights-export-power-bi.md). Hello пути, показанный здесь является просто tooillustrate примере как tooprocess экспортированных данных.
> 
> 

![Блок-схема для экспорта посредством SA tooPBI](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a>Создание хранилища в Azure
Непрерывный Экспорт всегда выдает учетной записи хранилища Azure tooan данных, поэтому сначала требуется toocreate hello хранилища.

1. Создать учетную запись хранилища «классический» в подписке в hello [портал Azure](https://portal.azure.com).
   
   ![На портале Azure выберите "Создать", "Данные", "Хранилище".](./media/app-insights-export-stream-analytics/030.png)
2. Создание контейнера
   
    ![В новое хранилище hello выберите контейнеры, щелкните плитку hello контейнеров, а затем добавить](./media/app-insights-export-stream-analytics/040.png)
3. Скопируйте ключ доступа к хранилищу hello
   
    Вам потребуется его скоро tooset hello ввода toohello stream analytics службы.
   
    ![В хранилище hello откройте параметры, ключи и сделайте копию hello первичный ключ доступа](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-tooazure-storage"></a>Запуск хранилища tooAzure непрерывный Экспорт
[Непрерывный экспорт](app-insights-export-telemetry.md) перемещает данные из Application Insights в хранилище Azure.

1. В hello портал Azure найдите ресурс Application Insights toohello, созданный для приложения.
   
    ![Выберите "Обзор", Application Insights, а затем выберите свое приложение.](./media/app-insights-export-stream-analytics/050.png)
2. Создайте непрерывный экспорт.
   
    ![Выберите "Параметры", "Непрерывный экспорт", "Добавить".](./media/app-insights-export-stream-analytics/060.png)

    Выберите учетную запись хранения hello, созданную ранее:

    ![Задать назначение экспорта hello](./media/app-insights-export-stream-analytics/070.png)

    Установите нужные типы событий hello toosee:

    ![Выберите типы событий.](./media/app-insights-export-stream-analytics/080.png)

1. Пусть данные накопятся. Предоставьте пользователям возможность поработать с приложением на протяжении некоторого времени. После получения данных телеметрии в [обозревателе метрик](app-insights-metrics-explorer.md) отобразятся статистические диаграммы, а в разделе [поиска по журналу диагностики](app-insights-diagnostic-search.md) — отдельные события. 
   
    И Кроме того, будет Экспорт tooyour хранилища данных hello. 
2. Проверьте hello экспортированы данные. В Visual Studio откройте меню **"Вид" или "Обозреватель облака"**и выберите элемент "Azure" или "Хранилище". (Если у вас нет этот пункт меню, необходимо tooinstall hello Azure SDK: Откройте диалоговое окно нового проекта hello и откройте Visual C# / облако / получить Microsoft Azure SDK для .NET.)
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    Запишите hello общую часть hello путь, который является производным от hello приложения имя и ключ инструментирования. 

Hello события записываются tooblob файлы в формате JSON. Каждый файл может содержать одно или несколько событий. Поэтому мы предлагаем данных события tooread hello и отфильтровать hello поля, которые должны. Существуют все виды вещей, которые можно было бы сделать с данными hello, но мы планируем на сегодняшний день является tooPower toouse Stream Analytics toopipe hello данных бизнес-Аналитики.

## <a name="create-an-azure-stream-analytics-instance"></a>Создание экземпляра Azure Stream Analytics
Из hello [классический портал Azure](https://manage.windowsazure.com/), выберите службу hello Azure Stream Analytics и создайте новое задание Stream Analytics:

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

Когда создается новое задание hello, разверните его данные:

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a>Установка расположения большого двоичного объекта
Задайте tootake входные данные из вашей непрерывного экспорта больших двоичных объектов.

![](./media/app-insights-export-stream-analytics/120.png)

Теперь вам требуется hello первичный ключ доступа из вашей учетной записи хранилища, в котором записанные ранее. Настроить его как hello ключ учетной записи хранения.

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a>Установка шаблона префикса пути
![](./media/app-insights-export-stream-analytics/140.png)

**Быть убедиться, что tooset hello формат даты tooYYYY мм-дд (с дефисы).**

Шаблон префикс пути Hello указывает, где Stream Analytics обнаруживает hello входных файлов в хранилище hello. Требуется tooset его toohow toocorrespond непрерывный Экспорт хранит данные hello. Задайте следующее значение:

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

В данном примере:

* `webapplication27`— Имя hello hello ресурс Application Insights **все строчные**.
* `1234...`ключ инструментирования hello hello ресурс Application Insights **пропуск тире**. 
* `PageViews`— Тип hello данных требуется tooanalyze. Доступные типы Hello зависят от фильтра hello, заданные в непрерывный экспорт. Просмотрите другие доступные типы hello экспортированных данных toosee hello и hello в разделе [Экспорт модели данных](app-insights-export-data-model.md).
* `/{date}/{time}` – шаблон, записанный буквально.

> [!NOTE]
> Проверьте убедиться, что путь hello получения правильных toomake хранилища hello.
> 
> 

### <a name="finish-initial-setup"></a>Завершение начальной настройки
Подтверждение hello формат сериализации:

![Подтвердите выбор и закройте мастер.](./media/app-insights-export-stream-analytics/150.png)

Закройте мастер hello и дождитесь toocomplete установки hello.

> [!TIP]
> Используйте toodownload команда образец hello некоторые данные. Сохранение в виде toodebug теста образца запроса.
> 
> 

## <a name="set-hello-output"></a>Выходной набор hello
Теперь выберите задание и установите hello выходных данных.

![Выберите новый канал hello, щелкните выходов, добавить, Power BI](./media/app-insights-export-stream-analytics/160.png)

Укажите ваш **рабочая учетная запись** tooauthorize tooaccess Stream Analytics ресурса Power BI. Затем придумать имя для вывода hello, а для набора данных Power BI целевой hello и таблицы.

![Создание трех имен.](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-hello-query"></a>Набор запросов hello
запрос Hello регулирует hello перевод из входного toooutput.

![Выберите задание hello и щелкните запрос. Вставьте образец hello ниже.](./media/app-insights-export-stream-analytics/180.png)

Используйте hello тестирования функции toocheck получение выходных данных справа hello. Присвойте ему hello образец данных, в результате со страницы приветствия входных данных. 

### <a name="query-toodisplay-counts-of-events"></a>Счетчики событий toodisplay запроса
Вставьте следующий запрос.

```SQL

    SELECT
      flat.ArrayValue.name,
      count(*)
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.[event]) as flat
    GROUP BY TumblingWindow(minute, 1), flat.ArrayValue.name
```

* входные данные экспорта — псевдоним hello, присвоенное входящий поток toohello
* Вывод элемента невыполненной работы — hello Псевдоним выхода, который мы определили
* Мы используем [GetElements ВНЕШНЕГО применить](https://msdn.microsoft.com/library/azure/dn706229.aspx) так как имя события hello вложенных arrray JSON. Затем выберите подбор hello hello имя события, количество hello количество экземпляров с таким именем hello период времени. Hello [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) предложение группирует элементы hello периодам времени 1 минута.

### <a name="query-toodisplay-metric-values"></a>Значения метрик toodisplay запроса
```SQL

    SELECT
      A.context.data.eventtime,
      avg(CASE WHEN flat.arrayvalue.myMetric.value IS NULL THEN 0 ELSE  flat.arrayvalue.myMetric.value END) as myValue
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.context.custom.metrics) as flat
    GROUP BY TumblingWindow(minute, 1), A.context.data.eventtime

``` 

* Этот запрос детализация в hello hello метрики телеметрии tooget времени события и значение метрики hello. значения метрики Hello находятся в массив, поэтому мы используем hello ВНЕШНЕГО GetElements применить шаблон tooextract hello строк. «myMetric» в этом случае является hello имя метрики hello. 

### <a name="query-tooinclude-values-of-dimension-properties"></a>Запрашивать tooinclude значения свойств измерения
```SQL

    WITH flat AS (
    SELECT
      MySource.context.data.eventTime as eventTime,
      InstanceId = MyDimension.ArrayValue.InstanceId.value,
      BusinessUnitId = MyDimension.ArrayValue.BusinessUnitId.value
    FROM MySource
    OUTER APPLY GetArrayElements(MySource.context.custom.dimensions) MyDimension
    )
    SELECT
     eventTime,
     InstanceId,
     BusinessUnitId
    INTO AIOutput
    FROM flat

```

* Этот запрос не содержит значения свойств измерения hello без в зависимости от конкретного измерения, основных индекса в массиве измерения hello.

## <a name="run-hello-job"></a>Запустить задание hello
Можно выбрать дату в hello за toostart в задании hello. 

![Выберите задание hello и щелкните запрос. Вставьте образец hello ниже.](./media/app-insights-export-stream-analytics/190.png)

Подождите, пока выполняется задание hello.

## <a name="see-results-in-power-bi"></a>Просмотр результатов в Power BI
> [!WARNING]
> Существуют значительно улучшают и упрощают [рекомендуемым методом toodisplay Application Insights данных в Power BI](app-insights-export-power-bi.md). Hello пути, показанный здесь является просто tooillustrate примере как tooprocess экспортированных данных.
> 
> 

Откройте Power BI с рабочими или рабочую учетную запись и выберите hello набора данных и таблицы, которая определена как hello выходные данные задания Stream Analytics hello.

![Выбор набора данных и полей в Power BI.](./media/app-insights-export-stream-analytics/200.png)

Теперь этот набор данных можно использовать в отчетах и панелях мониторинга в [Power BI](https://powerbi.microsoft.com).

![Выбор набора данных и полей в Power BI.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a>Данные отсутствуют?
* Проверьте, которую [формат даты hello набор](#set-path-prefix-pattern) правильно tooYYYY мм-дд (с дефисы).

## <a name="video"></a>Видео
Zeev Бен Noam показано, как tooprocess экспортированные данные, с помощью Stream Analytics.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
* [непрерывный экспорт.](app-insights-export-telemetry.md)
* [Подробные данные модели ссылок для значений и типы свойств hello.](app-insights-export-data-model.md)
* [Application Insights](app-insights-overview.md)

