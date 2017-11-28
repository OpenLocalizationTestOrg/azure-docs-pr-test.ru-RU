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
# <a name="use-stream-analytics-tooprocess-exported-data-from-application-insights"></a><span data-ttu-id="44666-103">Используйте Stream Analytics tooprocess экспортированных данных из Application Insights</span><span class="sxs-lookup"><span data-stu-id="44666-103">Use Stream Analytics tooprocess exported data from Application Insights</span></span>
<span data-ttu-id="44666-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) hello идеальным средством для обработки данных — [экспортированы из Application Insights](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="44666-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is hello ideal tool for processing data [exported from Application Insights](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="44666-105">Stream Analytics может извлекать данные из различных источников.</span><span class="sxs-lookup"><span data-stu-id="44666-105">Stream Analytics can pull data from a variety of sources.</span></span> <span data-ttu-id="44666-106">Его преобразования и фильтрации данных hello и затем направлять tooa различных приемников.</span><span class="sxs-lookup"><span data-stu-id="44666-106">It can transform and filter hello data, and then route it tooa variety of sinks.</span></span>

<span data-ttu-id="44666-107">В этом примере мы создадим адаптер, который импортирует данные из Application Insights, переименование и обрабатывает некоторые поля hello и направляет его в Power BI.</span><span class="sxs-lookup"><span data-stu-id="44666-107">In this example, we'll create an adaptor that takes data from Application Insights, renames and processes some of hello fields, and pipes it into Power BI.</span></span>

> [!WARNING]
> <span data-ttu-id="44666-108">Существуют значительно улучшают и упрощают [рекомендуемым методом toodisplay Application Insights данных в Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="44666-108">There are much better and easier [recommended ways toodisplay Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="44666-109">Hello пути, показанный здесь является просто tooillustrate примере как tooprocess экспортированных данных.</span><span class="sxs-lookup"><span data-stu-id="44666-109">hello path illustrated here is just an example tooillustrate how tooprocess exported data.</span></span>
> 
> 

![Блок-схема для экспорта посредством SA tooPBI](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a><span data-ttu-id="44666-111">Создание хранилища в Azure</span><span class="sxs-lookup"><span data-stu-id="44666-111">Create storage in Azure</span></span>
<span data-ttu-id="44666-112">Непрерывный Экспорт всегда выдает учетной записи хранилища Azure tooan данных, поэтому сначала требуется toocreate hello хранилища.</span><span class="sxs-lookup"><span data-stu-id="44666-112">Continuous export always outputs data tooan Azure Storage account, so you need toocreate hello storage first.</span></span>

1. <span data-ttu-id="44666-113">Создать учетную запись хранилища «классический» в подписке в hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="44666-113">Create a "classic" storage account in your subscription in hello [Azure portal](https://portal.azure.com).</span></span>
   
   ![На портале Azure выберите "Создать", "Данные", "Хранилище".](./media/app-insights-export-stream-analytics/030.png)
2. <span data-ttu-id="44666-115">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="44666-115">Create a container</span></span>
   
    ![В новое хранилище hello выберите контейнеры, щелкните плитку hello контейнеров, а затем добавить](./media/app-insights-export-stream-analytics/040.png)
3. <span data-ttu-id="44666-117">Скопируйте ключ доступа к хранилищу hello</span><span class="sxs-lookup"><span data-stu-id="44666-117">Copy hello storage access key</span></span>
   
    <span data-ttu-id="44666-118">Вам потребуется его скоро tooset hello ввода toohello stream analytics службы.</span><span class="sxs-lookup"><span data-stu-id="44666-118">You'll need it soon tooset up hello input toohello stream analytics service.</span></span>
   
    ![В хранилище hello откройте параметры, ключи и сделайте копию hello первичный ключ доступа](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-tooazure-storage"></a><span data-ttu-id="44666-120">Запуск хранилища tooAzure непрерывный Экспорт</span><span class="sxs-lookup"><span data-stu-id="44666-120">Start continuous export tooAzure storage</span></span>
<span data-ttu-id="44666-121">[Непрерывный экспорт](app-insights-export-telemetry.md) перемещает данные из Application Insights в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="44666-121">[Continuous export](app-insights-export-telemetry.md) moves data from Application Insights into Azure storage.</span></span>

1. <span data-ttu-id="44666-122">В hello портал Azure найдите ресурс Application Insights toohello, созданный для приложения.</span><span class="sxs-lookup"><span data-stu-id="44666-122">In hello Azure portal, browse toohello Application Insights resource you created for your application.</span></span>
   
    ![Выберите "Обзор", Application Insights, а затем выберите свое приложение.](./media/app-insights-export-stream-analytics/050.png)
2. <span data-ttu-id="44666-124">Создайте непрерывный экспорт.</span><span class="sxs-lookup"><span data-stu-id="44666-124">Create a continuous export.</span></span>
   
    ![Выберите "Параметры", "Непрерывный экспорт", "Добавить".](./media/app-insights-export-stream-analytics/060.png)

    <span data-ttu-id="44666-126">Выберите учетную запись хранения hello, созданную ранее:</span><span class="sxs-lookup"><span data-stu-id="44666-126">Select hello storage account you created earlier:</span></span>

    ![Задать назначение экспорта hello](./media/app-insights-export-stream-analytics/070.png)

    <span data-ttu-id="44666-128">Установите нужные типы событий hello toosee:</span><span class="sxs-lookup"><span data-stu-id="44666-128">Set hello event types you want toosee:</span></span>

    ![Выберите типы событий.](./media/app-insights-export-stream-analytics/080.png)

1. <span data-ttu-id="44666-130">Пусть данные накопятся.</span><span class="sxs-lookup"><span data-stu-id="44666-130">Let some data accumulate.</span></span> <span data-ttu-id="44666-131">Предоставьте пользователям возможность поработать с приложением на протяжении некоторого времени.</span><span class="sxs-lookup"><span data-stu-id="44666-131">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="44666-132">После получения данных телеметрии в [обозревателе метрик](app-insights-metrics-explorer.md) отобразятся статистические диаграммы, а в разделе [поиска по журналу диагностики](app-insights-diagnostic-search.md) — отдельные события.</span><span class="sxs-lookup"><span data-stu-id="44666-132">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="44666-133">И Кроме того, будет Экспорт tooyour хранилища данных hello.</span><span class="sxs-lookup"><span data-stu-id="44666-133">And also, hello data will export tooyour storage.</span></span> 
2. <span data-ttu-id="44666-134">Проверьте hello экспортированы данные.</span><span class="sxs-lookup"><span data-stu-id="44666-134">Inspect hello exported data.</span></span> <span data-ttu-id="44666-135">В Visual Studio откройте меню **"Вид" или "Обозреватель облака"**и выберите элемент "Azure" или "Хранилище".</span><span class="sxs-lookup"><span data-stu-id="44666-135">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="44666-136">(Если у вас нет этот пункт меню, необходимо tooinstall hello Azure SDK: Откройте диалоговое окно нового проекта hello и откройте Visual C# / облако / получить Microsoft Azure SDK для .NET.)</span><span class="sxs-lookup"><span data-stu-id="44666-136">(If you don't have this menu option, you need tooinstall hello Azure SDK: Open hello New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    <span data-ttu-id="44666-137">Запишите hello общую часть hello путь, который является производным от hello приложения имя и ключ инструментирования.</span><span class="sxs-lookup"><span data-stu-id="44666-137">Make a note of hello common part of hello path name, which is derived from hello application name and instrumentation key.</span></span> 

<span data-ttu-id="44666-138">Hello события записываются tooblob файлы в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="44666-138">hello events are written tooblob files in JSON format.</span></span> <span data-ttu-id="44666-139">Каждый файл может содержать одно или несколько событий.</span><span class="sxs-lookup"><span data-stu-id="44666-139">Each file may contain one or more events.</span></span> <span data-ttu-id="44666-140">Поэтому мы предлагаем данных события tooread hello и отфильтровать hello поля, которые должны.</span><span class="sxs-lookup"><span data-stu-id="44666-140">So we'd like tooread hello event data and filter out hello fields we want.</span></span> <span data-ttu-id="44666-141">Существуют все виды вещей, которые можно было бы сделать с данными hello, но мы планируем на сегодняшний день является tooPower toouse Stream Analytics toopipe hello данных бизнес-Аналитики.</span><span class="sxs-lookup"><span data-stu-id="44666-141">There are all kinds of things we could do with hello data, but our plan today is toouse Stream Analytics toopipe hello data tooPower BI.</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="44666-142">Создание экземпляра Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="44666-142">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="44666-143">Из hello [классический портал Azure](https://manage.windowsazure.com/), выберите службу hello Azure Stream Analytics и создайте новое задание Stream Analytics:</span><span class="sxs-lookup"><span data-stu-id="44666-143">From hello [Classic Azure Portal](https://manage.windowsazure.com/), select hello Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

<span data-ttu-id="44666-144">Когда создается новое задание hello, разверните его данные:</span><span class="sxs-lookup"><span data-stu-id="44666-144">When hello new job is created, expand its details:</span></span>

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a><span data-ttu-id="44666-145">Установка расположения большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="44666-145">Set blob location</span></span>
<span data-ttu-id="44666-146">Задайте tootake входные данные из вашей непрерывного экспорта больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="44666-146">Set it tootake input from your Continuous Export blob:</span></span>

![](./media/app-insights-export-stream-analytics/120.png)

<span data-ttu-id="44666-147">Теперь вам требуется hello первичный ключ доступа из вашей учетной записи хранилища, в котором записанные ранее.</span><span class="sxs-lookup"><span data-stu-id="44666-147">Now you'll need hello Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="44666-148">Настроить его как hello ключ учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="44666-148">Set this as hello Storage Account Key.</span></span>

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a><span data-ttu-id="44666-149">Установка шаблона префикса пути</span><span class="sxs-lookup"><span data-stu-id="44666-149">Set path prefix pattern</span></span>
![](./media/app-insights-export-stream-analytics/140.png)

<span data-ttu-id="44666-150">**Быть убедиться, что tooset hello формат даты tooYYYY мм-дд (с дефисы).**</span><span class="sxs-lookup"><span data-stu-id="44666-150">**Be sure tooset hello Date Format tooYYYY-MM-DD (with dashes).**</span></span>

<span data-ttu-id="44666-151">Шаблон префикс пути Hello указывает, где Stream Analytics обнаруживает hello входных файлов в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="44666-151">hello Path Prefix Pattern specifies where Stream Analytics finds hello input files in hello storage.</span></span> <span data-ttu-id="44666-152">Требуется tooset его toohow toocorrespond непрерывный Экспорт хранит данные hello.</span><span class="sxs-lookup"><span data-stu-id="44666-152">You need tooset it toocorrespond toohow Continuous Export stores hello data.</span></span> <span data-ttu-id="44666-153">Задайте следующее значение:</span><span class="sxs-lookup"><span data-stu-id="44666-153">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="44666-154">В данном примере:</span><span class="sxs-lookup"><span data-stu-id="44666-154">In this example:</span></span>

* <span data-ttu-id="44666-155">`webapplication27`— Имя hello hello ресурс Application Insights **все строчные**.</span><span class="sxs-lookup"><span data-stu-id="44666-155">`webapplication27` is hello name of hello Application Insights resource **all lower case**.</span></span>
* <span data-ttu-id="44666-156">`1234...`ключ инструментирования hello hello ресурс Application Insights **пропуск тире**.</span><span class="sxs-lookup"><span data-stu-id="44666-156">`1234...` is hello instrumentation key of hello Application Insights resource, **omitting dashes**.</span></span> 
* <span data-ttu-id="44666-157">`PageViews`— Тип hello данных требуется tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="44666-157">`PageViews` is hello type of data you want tooanalyze.</span></span> <span data-ttu-id="44666-158">Доступные типы Hello зависят от фильтра hello, заданные в непрерывный экспорт.</span><span class="sxs-lookup"><span data-stu-id="44666-158">hello available types depend on hello filter you set in Continuous Export.</span></span> <span data-ttu-id="44666-159">Просмотрите другие доступные типы hello экспортированных данных toosee hello и hello в разделе [Экспорт модели данных](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="44666-159">Examine hello exported data toosee hello other available types, and see hello [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="44666-160">`/{date}/{time}` – шаблон, записанный буквально.</span><span class="sxs-lookup"><span data-stu-id="44666-160">`/{date}/{time}` is a pattern written literally.</span></span>

> [!NOTE]
> <span data-ttu-id="44666-161">Проверьте убедиться, что путь hello получения правильных toomake хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="44666-161">Inspect hello storage toomake sure you get hello path right.</span></span>
> 
> 

### <a name="finish-initial-setup"></a><span data-ttu-id="44666-162">Завершение начальной настройки</span><span class="sxs-lookup"><span data-stu-id="44666-162">Finish initial setup</span></span>
<span data-ttu-id="44666-163">Подтверждение hello формат сериализации:</span><span class="sxs-lookup"><span data-stu-id="44666-163">Confirm hello serialization format:</span></span>

![Подтвердите выбор и закройте мастер.](./media/app-insights-export-stream-analytics/150.png)

<span data-ttu-id="44666-165">Закройте мастер hello и дождитесь toocomplete установки hello.</span><span class="sxs-lookup"><span data-stu-id="44666-165">Close hello wizard and wait for hello setup toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="44666-166">Используйте toodownload команда образец hello некоторые данные.</span><span class="sxs-lookup"><span data-stu-id="44666-166">Use hello Sample command toodownload some data.</span></span> <span data-ttu-id="44666-167">Сохранение в виде toodebug теста образца запроса.</span><span class="sxs-lookup"><span data-stu-id="44666-167">Keep it as a test sample toodebug your query.</span></span>
> 
> 

## <a name="set-hello-output"></a><span data-ttu-id="44666-168">Выходной набор hello</span><span class="sxs-lookup"><span data-stu-id="44666-168">Set hello output</span></span>
<span data-ttu-id="44666-169">Теперь выберите задание и установите hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="44666-169">Now select your job and set hello output.</span></span>

![Выберите новый канал hello, щелкните выходов, добавить, Power BI](./media/app-insights-export-stream-analytics/160.png)

<span data-ttu-id="44666-171">Укажите ваш **рабочая учетная запись** tooauthorize tooaccess Stream Analytics ресурса Power BI.</span><span class="sxs-lookup"><span data-stu-id="44666-171">Provide your **work or school account** tooauthorize Stream Analytics tooaccess your Power BI resource.</span></span> <span data-ttu-id="44666-172">Затем придумать имя для вывода hello, а для набора данных Power BI целевой hello и таблицы.</span><span class="sxs-lookup"><span data-stu-id="44666-172">Then invent a name for hello output, and for hello target Power BI dataset and table.</span></span>

![Создание трех имен.](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-hello-query"></a><span data-ttu-id="44666-174">Набор запросов hello</span><span class="sxs-lookup"><span data-stu-id="44666-174">Set hello query</span></span>
<span data-ttu-id="44666-175">запрос Hello регулирует hello перевод из входного toooutput.</span><span class="sxs-lookup"><span data-stu-id="44666-175">hello query governs hello translation from input toooutput.</span></span>

![Выберите задание hello и щелкните запрос.](./media/app-insights-export-stream-analytics/180.png)

<span data-ttu-id="44666-178">Используйте hello тестирования функции toocheck получение выходных данных справа hello.</span><span class="sxs-lookup"><span data-stu-id="44666-178">Use hello Test function toocheck that you get hello right output.</span></span> <span data-ttu-id="44666-179">Присвойте ему hello образец данных, в результате со страницы приветствия входных данных.</span><span class="sxs-lookup"><span data-stu-id="44666-179">Give it hello sample data that you took from hello inputs page.</span></span> 

### <a name="query-toodisplay-counts-of-events"></a><span data-ttu-id="44666-180">Счетчики событий toodisplay запроса</span><span class="sxs-lookup"><span data-stu-id="44666-180">Query toodisplay counts of events</span></span>
<span data-ttu-id="44666-181">Вставьте следующий запрос.</span><span class="sxs-lookup"><span data-stu-id="44666-181">Paste this query:</span></span>

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

* <span data-ttu-id="44666-182">входные данные экспорта — псевдоним hello, присвоенное входящий поток toohello</span><span class="sxs-lookup"><span data-stu-id="44666-182">export-input is hello alias we gave toohello stream input</span></span>
* <span data-ttu-id="44666-183">Вывод элемента невыполненной работы — hello Псевдоним выхода, который мы определили</span><span class="sxs-lookup"><span data-stu-id="44666-183">pbi-output is hello output alias we defined</span></span>
* <span data-ttu-id="44666-184">Мы используем [GetElements ВНЕШНЕГО применить](https://msdn.microsoft.com/library/azure/dn706229.aspx) так как имя события hello вложенных arrray JSON.</span><span class="sxs-lookup"><span data-stu-id="44666-184">We use [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) because hello event name is in a nested JSON arrray.</span></span> <span data-ttu-id="44666-185">Затем выберите подбор hello hello имя события, количество hello количество экземпляров с таким именем hello период времени.</span><span class="sxs-lookup"><span data-stu-id="44666-185">Then hello Select picks hello event name, together with a count of hello number of instances with that name in hello time period.</span></span> <span data-ttu-id="44666-186">Hello [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) предложение группирует элементы hello периодам времени 1 минута.</span><span class="sxs-lookup"><span data-stu-id="44666-186">hello [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clause groups hello elements into time periods of 1 minute.</span></span>

### <a name="query-toodisplay-metric-values"></a><span data-ttu-id="44666-187">Значения метрик toodisplay запроса</span><span class="sxs-lookup"><span data-stu-id="44666-187">Query toodisplay metric values</span></span>
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

* <span data-ttu-id="44666-188">Этот запрос детализация в hello hello метрики телеметрии tooget времени события и значение метрики hello.</span><span class="sxs-lookup"><span data-stu-id="44666-188">This query drills into hello metrics telemetry tooget hello event time and hello metric value.</span></span> <span data-ttu-id="44666-189">значения метрики Hello находятся в массив, поэтому мы используем hello ВНЕШНЕГО GetElements применить шаблон tooextract hello строк.</span><span class="sxs-lookup"><span data-stu-id="44666-189">hello metric values are inside an array, so we use hello OUTER APPLY GetElements pattern tooextract hello rows.</span></span> <span data-ttu-id="44666-190">«myMetric» в этом случае является hello имя метрики hello.</span><span class="sxs-lookup"><span data-stu-id="44666-190">"myMetric" is hello name of hello metric in this case.</span></span> 

### <a name="query-tooinclude-values-of-dimension-properties"></a><span data-ttu-id="44666-191">Запрашивать tooinclude значения свойств измерения</span><span class="sxs-lookup"><span data-stu-id="44666-191">Query tooinclude values of dimension properties</span></span>
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

* <span data-ttu-id="44666-192">Этот запрос не содержит значения свойств измерения hello без в зависимости от конкретного измерения, основных индекса в массиве измерения hello.</span><span class="sxs-lookup"><span data-stu-id="44666-192">This query includes values of hello dimension properties without depending on a particular dimension being at a fixed index in hello dimension array.</span></span>

## <a name="run-hello-job"></a><span data-ttu-id="44666-193">Запустить задание hello</span><span class="sxs-lookup"><span data-stu-id="44666-193">Run hello job</span></span>
<span data-ttu-id="44666-194">Можно выбрать дату в hello за toostart в задании hello.</span><span class="sxs-lookup"><span data-stu-id="44666-194">You can select a date in hello past toostart hello job from.</span></span> 

![Выберите задание hello и щелкните запрос.](./media/app-insights-export-stream-analytics/190.png)

<span data-ttu-id="44666-197">Подождите, пока выполняется задание hello.</span><span class="sxs-lookup"><span data-stu-id="44666-197">Wait until hello job is Running.</span></span>

## <a name="see-results-in-power-bi"></a><span data-ttu-id="44666-198">Просмотр результатов в Power BI</span><span class="sxs-lookup"><span data-stu-id="44666-198">See results in Power BI</span></span>
> [!WARNING]
> <span data-ttu-id="44666-199">Существуют значительно улучшают и упрощают [рекомендуемым методом toodisplay Application Insights данных в Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="44666-199">There are much better and easier [recommended ways toodisplay Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="44666-200">Hello пути, показанный здесь является просто tooillustrate примере как tooprocess экспортированных данных.</span><span class="sxs-lookup"><span data-stu-id="44666-200">hello path illustrated here is just an example tooillustrate how tooprocess exported data.</span></span>
> 
> 

<span data-ttu-id="44666-201">Откройте Power BI с рабочими или рабочую учетную запись и выберите hello набора данных и таблицы, которая определена как hello выходные данные задания Stream Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="44666-201">Open Power BI with your work or school account, and select hello dataset and table that you defined as hello output of hello Stream Analytics job.</span></span>

![Выбор набора данных и полей в Power BI.](./media/app-insights-export-stream-analytics/200.png)

<span data-ttu-id="44666-203">Теперь этот набор данных можно использовать в отчетах и панелях мониторинга в [Power BI](https://powerbi.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="44666-203">Now you can use this dataset in reports and dashboards in [Power BI](https://powerbi.microsoft.com).</span></span>

![Выбор набора данных и полей в Power BI.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a><span data-ttu-id="44666-205">Данные отсутствуют?</span><span class="sxs-lookup"><span data-stu-id="44666-205">No data?</span></span>
* <span data-ttu-id="44666-206">Проверьте, которую [формат даты hello набор](#set-path-prefix-pattern) правильно tooYYYY мм-дд (с дефисы).</span><span class="sxs-lookup"><span data-stu-id="44666-206">Check that you [set hello date format](#set-path-prefix-pattern) correctly tooYYYY-MM-DD (with dashes).</span></span>

## <a name="video"></a><span data-ttu-id="44666-207">Видео</span><span class="sxs-lookup"><span data-stu-id="44666-207">Video</span></span>
<span data-ttu-id="44666-208">Zeev Бен Noam показано, как tooprocess экспортированные данные, с помощью Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="44666-208">Noam Ben Zeev shows how tooprocess exported data using Stream Analytics.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="44666-209">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="44666-209">Next steps</span></span>
* [<span data-ttu-id="44666-210">непрерывный экспорт.</span><span class="sxs-lookup"><span data-stu-id="44666-210">Continuous export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="44666-211">Подробные данные модели ссылок для значений и типы свойств hello.</span><span class="sxs-lookup"><span data-stu-id="44666-211">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="44666-212">Application Insights</span><span class="sxs-lookup"><span data-stu-id="44666-212">Application Insights</span></span>](app-insights-overview.md)

