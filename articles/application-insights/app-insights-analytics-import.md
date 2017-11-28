---
title: "aaaImport вашей tooAnalytics данные в Azure Application Insights | Документы Microsoft"
description: "При импорте toojoin статические данные с телеметрии приложения или импорт tooquery потока данных с помощью аналитики."
services: application-insights
keywords: "открытие схемы, импорт данных"
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bwren
ms.openlocfilehash: 7a3a3c9155adc1885dd366ddb13dda80bb894adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-analytics"></a><span data-ttu-id="da472-104">Импорт данных в инструмент аналитики</span><span class="sxs-lookup"><span data-stu-id="da472-104">Import data into Analytics</span></span>

<span data-ttu-id="da472-105">Импорт табличных данных в [Analytics](app-insights-analytics.md), либо toojoin его с [Application Insights](app-insights-overview.md) телеметрии из приложения, или можно проанализировать в отдельном потоке.</span><span class="sxs-lookup"><span data-stu-id="da472-105">Import any tabular data into [Analytics](app-insights-analytics.md), either toojoin it with [Application Insights](app-insights-overview.md) telemetry from your app, or so that you can analyze it as a separate stream.</span></span> <span data-ttu-id="da472-106">Аналитика является потоки запросами языка хорошо подходит tooanalyzing отметку времени крупномасштабных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="da472-106">Analytics is a powerful query language well-suited tooanalyzing high-volume timestamped streams of telemetry.</span></span>

<span data-ttu-id="da472-107">Вы можете импортировать данные в инструмент аналитики, используя собственную схему.</span><span class="sxs-lookup"><span data-stu-id="da472-107">You can import data into Analytics using your own schema.</span></span> <span data-ttu-id="da472-108">Это не обязательно toouse hello Стандартная Application Insights схем, таких как запрос или трассировки.</span><span class="sxs-lookup"><span data-stu-id="da472-108">It doesn't have toouse hello standard Application Insights schemas such as request or trace.</span></span>

<span data-ttu-id="da472-109">Можно импортировать файлы в формате JSON или DSV (значения с разделителями — запятыми, точками с запятой или знаками табуляции).</span><span class="sxs-lookup"><span data-stu-id="da472-109">You can import JSON or DSV (delimiter-separated values - comma, semicolon or tab) files.</span></span>

<span data-ttu-id="da472-110">Существует три ситуации, когда полезно Импорт tooAnalytics:</span><span class="sxs-lookup"><span data-stu-id="da472-110">There are three situations where importing tooAnalytics is useful:</span></span>

* <span data-ttu-id="da472-111">**Объединение с данными телеметрии приложения.**</span><span class="sxs-lookup"><span data-stu-id="da472-111">**Join with app telemetry.**</span></span> <span data-ttu-id="da472-112">Например можно импортировать таблицу, которая сопоставляет URL-адреса из заголовков для чтения страниц toomore вашего веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="da472-112">For example, you could import a table that maps URLs from your website toomore readable page titles.</span></span> <span data-ttu-id="da472-113">В аналитике можно создать панель мониторинга отчета с диаграммой, показывающий hello десяти наиболее популярных страниц веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="da472-113">In Analytics, you can create a dashboard chart report that shows hello ten most popular pages in your website.</span></span> <span data-ttu-id="da472-114">Он может отображать hello названия страниц вместо hello URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="da472-114">Now it can show hello page titles instead of hello URLs.</span></span>
* <span data-ttu-id="da472-115">**Сопоставление данных телеметрии приложения** с другими источниками, например с отчетом о сетевом трафике, данными сервера или файлами журнала CDN.</span><span class="sxs-lookup"><span data-stu-id="da472-115">**Correlate your application telemetry** with other sources such as network traffic, server data, or CDN log files.</span></span>
* <span data-ttu-id="da472-116">**Примените Analytics tooa отдельный поток данных.**</span><span class="sxs-lookup"><span data-stu-id="da472-116">**Apply Analytics tooa separate data stream.**</span></span> <span data-ttu-id="da472-117">Аналитика Application Insights — мощный инструмент, который хорошо работает с разреженным потоками с метками времени. Во многих случаях этот инструмент намного эффективнее, чем SQL.</span><span class="sxs-lookup"><span data-stu-id="da472-117">Application Insights Analytics is a powerful tool, that works well with sparse, timestamped streams - much better than SQL in many cases.</span></span> <span data-ttu-id="da472-118">С помощью аналитики вы можете проанализировать такой поток из другого источника.</span><span class="sxs-lookup"><span data-stu-id="da472-118">If you have such a stream from some other source, you can analyze it with Analytics.</span></span>

<span data-ttu-id="da472-119">Отправка данных tooyour источник данных можно легко.</span><span class="sxs-lookup"><span data-stu-id="da472-119">Sending data tooyour data source is easy.</span></span> 

1. <span data-ttu-id="da472-120">(Один раз) Определите схему hello данных в «источник данных».</span><span class="sxs-lookup"><span data-stu-id="da472-120">(One time) Define hello schema of your data in a 'data source'.</span></span>
2. <span data-ttu-id="da472-121">(Периодически) Отправка tooAzure хранилище данных и вызывать API-интерфейса REST toonotify hello нас, новые данные ожидает приема.</span><span class="sxs-lookup"><span data-stu-id="da472-121">(Periodically) Upload your data tooAzure storage, and call hello REST API toonotify us that new data is waiting for ingestion.</span></span> <span data-ttu-id="da472-122">В течение нескольких минут hello данных доступна для запросов в аналитике.</span><span class="sxs-lookup"><span data-stu-id="da472-122">Within a few minutes, hello data is available for query in Analytics.</span></span>

<span data-ttu-id="da472-123">Hello частоту передачи hello определяется пользователем и как быстро хотите, чтобы ваш toobe данных, доступных для запросов.</span><span class="sxs-lookup"><span data-stu-id="da472-123">hello frequency of hello upload is defined by you and how fast would you like your data toobe available for queries.</span></span> <span data-ttu-id="da472-124">Это более эффективно tooupload данные большими частями, но не более 1 ГБ.</span><span class="sxs-lookup"><span data-stu-id="da472-124">It is more efficient tooupload data in larger chunks, but not larger than 1GB.</span></span>

> [!NOTE]
> <span data-ttu-id="da472-125">*У вас есть большое количество tooanalyze источники данных?*</span><span class="sxs-lookup"><span data-stu-id="da472-125">*Got lots of data sources tooanalyze?*</span></span> [<span data-ttu-id="da472-126">*Рассмотрите возможность использования* logstash *tooship данные в Application Insights.*</span><span class="sxs-lookup"><span data-stu-id="da472-126">*Consider using* logstash *tooship your data into Application Insights.*</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a><span data-ttu-id="da472-127">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="da472-127">Before you start</span></span>

<span data-ttu-id="da472-128">Вам необходимы:</span><span class="sxs-lookup"><span data-stu-id="da472-128">You need:</span></span>

1. <span data-ttu-id="da472-129">Ресурс Application Insights в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="da472-129">An Application Insights resource in Microsoft Azure.</span></span>

 * <span data-ttu-id="da472-130">Если требуется tooanalyze данных отдельно от других телеметрии [создать новый ресурс Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="da472-130">If you want tooanalyze your data separately from any other telemetry, [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span>
 * <span data-ttu-id="da472-131">Если вы будете объединения или сравнения данных с помощью телеметрии из приложения, которое уже настроен с помощью Application Insights, hello ресурсов можно использовать для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="da472-131">If you're joining or comparing your data with telemetry from an app that is already set up with Application Insights, then you can use hello resource for that app.</span></span>
 * <span data-ttu-id="da472-132">Сотрудник или владелец ресурса toothat доступа.</span><span class="sxs-lookup"><span data-stu-id="da472-132">Contributor or owner access toothat resource.</span></span>
 
2. <span data-ttu-id="da472-133">хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="da472-133">Azure storage.</span></span> <span data-ttu-id="da472-134">Отправка tooAzure хранилища и аналитики получает данные из него.</span><span class="sxs-lookup"><span data-stu-id="da472-134">You upload tooAzure storage, and Analytics gets your data from there.</span></span> 

 * <span data-ttu-id="da472-135">Рекомендуем создать отдельную учетную запись хранения для больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="da472-135">We recommend you create a dedicated storage account for your blobs.</span></span> <span data-ttu-id="da472-136">Если BLOB-объектов являются общими с другими процессами, он занимает больше времени для наших tooread процессы BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="da472-136">If your blobs are shared with other processes, it takes longer for our processes tooread your blobs.</span></span>


## <a name="define-your-schema"></a><span data-ttu-id="da472-137">Определение схемы</span><span class="sxs-lookup"><span data-stu-id="da472-137">Define your schema</span></span>

<span data-ttu-id="da472-138">Прежде чем импортировать данные, необходимо определить *источника данных* указывает, hello схемы данных.</span><span class="sxs-lookup"><span data-stu-id="da472-138">Before you can import data, you must define a *data source,* which specifies hello schema of your data.</span></span>
<span data-ttu-id="da472-139">Можно создать до too50 источники данных в один ресурс Application Insights</span><span class="sxs-lookup"><span data-stu-id="da472-139">You can have up too50 data sources in a single Application Insights resource</span></span>

1. <span data-ttu-id="da472-140">Запустите мастер источников данных hello.</span><span class="sxs-lookup"><span data-stu-id="da472-140">Start hello data source wizard.</span></span> <span data-ttu-id="da472-141">Воспользуйтесь кнопкой Add new data source (Добавить новый источник данных).</span><span class="sxs-lookup"><span data-stu-id="da472-141">Use "Add new data source" button.</span></span> <span data-ttu-id="da472-142">Кроме того, нажмите кнопку "Параметры" в правом верхнем углу и в раскрывающемся меню выберите "Источники данных".</span><span class="sxs-lookup"><span data-stu-id="da472-142">Alternatively - click on settings button in right upper corner and choose "Data Sources" in dropdown menu.</span></span>

    ![Добавление источника данных](./media/app-insights-analytics-import/add-new-data-source.png)

    <span data-ttu-id="da472-144">Введите имя для нового источника данных.</span><span class="sxs-lookup"><span data-stu-id="da472-144">Provide a name for your new data source.</span></span>

2. <span data-ttu-id="da472-145">Определение формата hello файлов, которые нужно будет загрузить.</span><span class="sxs-lookup"><span data-stu-id="da472-145">Define format of hello files that you will upload.</span></span>

    <span data-ttu-id="da472-146">Можно вручную задать формат hello или загрузить образец файла.</span><span class="sxs-lookup"><span data-stu-id="da472-146">You can either define hello format manually, or upload a sample file.</span></span>

    <span data-ttu-id="da472-147">Если hello данные в формате CSV, первая строка hello образец hello может быть заголовки столбцов.</span><span class="sxs-lookup"><span data-stu-id="da472-147">If hello data is in CSV format, hello first row of hello sample can be column headers.</span></span> <span data-ttu-id="da472-148">Можно изменить имена полей hello в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="da472-148">You can change hello field names in hello next step.</span></span>

    <span data-ttu-id="da472-149">Образец Hello должен включать по крайней мере 10 строк или записей данных.</span><span class="sxs-lookup"><span data-stu-id="da472-149">hello sample should include at least 10 rows or records of data.</span></span>

    <span data-ttu-id="da472-150">Имена столбцов или полей должны состоять из букв и цифр (без пробелов и знаков препинания).</span><span class="sxs-lookup"><span data-stu-id="da472-150">Column or field names should have alphanumeric names (without spaces or punctuation).</span></span>

    ![Передача примера файла](./media/app-insights-analytics-import/sample-data-file.png)


3. <span data-ttu-id="da472-152">Есть схемы проверки hello, hello мастера.</span><span class="sxs-lookup"><span data-stu-id="da472-152">Review hello schema that hello wizard has got.</span></span> <span data-ttu-id="da472-153">Если он выводимые типы hello из выборки, может потребоваться tooadjust hello вывести типы столбцов hello.</span><span class="sxs-lookup"><span data-stu-id="da472-153">If it inferred hello types from a sample, you might need tooadjust hello inferred types of hello columns.</span></span>

    ![Просмотр схемы вывести hello](./media/app-insights-analytics-import/data-source-review-schema.png)

 * <span data-ttu-id="da472-155">(Необязательно.) Отправьте определение схемы.</span><span class="sxs-lookup"><span data-stu-id="da472-155">(Optional.) Upload a schema definition.</span></span> <span data-ttu-id="da472-156">В разделе hello в указанном ниже формате.</span><span class="sxs-lookup"><span data-stu-id="da472-156">See hello format below.</span></span>

 * <span data-ttu-id="da472-157">Выберите метку времени.</span><span class="sxs-lookup"><span data-stu-id="da472-157">Select a Timestamp.</span></span> <span data-ttu-id="da472-158">Все данные в инструменте аналитики должны включать поле метки времени.</span><span class="sxs-lookup"><span data-stu-id="da472-158">All data in Analytics must have a timestamp field.</span></span> <span data-ttu-id="da472-159">Он должен иметь тип `datetime`, но он не имеет toobe с именем «timestamp».</span><span class="sxs-lookup"><span data-stu-id="da472-159">It must have type `datetime`, but it doesn't have toobe named 'timestamp'.</span></span> <span data-ttu-id="da472-160">Если в данных есть столбец, содержащий дату и время в формате ISO, выберите этот как hello столбец отметки времени.</span><span class="sxs-lookup"><span data-stu-id="da472-160">If your data has a column containing a date and time in ISO format, choose this as hello timestamp column.</span></span> <span data-ttu-id="da472-161">В противном случае выберите «как данные поступили», и процесс импорта hello добавит поле метки времени.</span><span class="sxs-lookup"><span data-stu-id="da472-161">Otherwise, choose "as data arrived", and hello import process will add a timestamp field.</span></span>

5. <span data-ttu-id="da472-162">Создайте источник данных hello.</span><span class="sxs-lookup"><span data-stu-id="da472-162">Create hello data source.</span></span>

### <a name="schema-definition-file-format"></a><span data-ttu-id="da472-163">Формат файла определения схемы</span><span class="sxs-lookup"><span data-stu-id="da472-163">Schema definition file format</span></span>

<span data-ttu-id="da472-164">Вместо редактирования схемы hello в пользовательском Интерфейсе, можно загрузить из файла определения схемы hello.</span><span class="sxs-lookup"><span data-stu-id="da472-164">Instead of editing hello schema in UI, you can load hello schema definition from a file.</span></span> <span data-ttu-id="da472-165">Hello схемы определения имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="da472-165">hello schema definition format is as follows:</span></span> 

<span data-ttu-id="da472-166">Формат с разделителями</span><span class="sxs-lookup"><span data-stu-id="da472-166">Delimited format</span></span> 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

<span data-ttu-id="da472-167">Формат JSON</span><span class="sxs-lookup"><span data-stu-id="da472-167">JSON format</span></span> 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
<span data-ttu-id="da472-168">Каждый столбец идентифицируется hello расположение, имя и тип.</span><span class="sxs-lookup"><span data-stu-id="da472-168">Each column is identified by hello location, name and type.</span></span> 

* <span data-ttu-id="da472-169">Расположение — формата файла с разделителями, он располагается hello hello сопоставить значения.</span><span class="sxs-lookup"><span data-stu-id="da472-169">Location – For delimited file format it is hello position of hello mapped value.</span></span> <span data-ttu-id="da472-170">Формат JSON это jpath hello hello сопоставлен ключа.</span><span class="sxs-lookup"><span data-stu-id="da472-170">For JSON format, it is hello jpath of hello mapped key.</span></span>
* <span data-ttu-id="da472-171">Имя — hello отображается имя столбца hello.</span><span class="sxs-lookup"><span data-stu-id="da472-171">Name – hello displayed name of hello column.</span></span>
* <span data-ttu-id="da472-172">Тип — hello тип данных этого столбца.</span><span class="sxs-lookup"><span data-stu-id="da472-172">Type – hello data type of that column.</span></span>
 
<span data-ttu-id="da472-173">В случае использовался в образце данных, а в качестве разделителя формат файла, определение схемы hello необходимо сопоставить все столбцы и добавить новые столбцы в конце hello.</span><span class="sxs-lookup"><span data-stu-id="da472-173">In case a sample data was used and file format is delimited, hello schema definition must map all columns and add new columns at hello end.</span></span> 

<span data-ttu-id="da472-174">JSON допускает частичное сопоставление данных hello, поэтому hello определение схемы формат JSON не имеют toomap каждый ключ, который находится в образце данных.</span><span class="sxs-lookup"><span data-stu-id="da472-174">JSON allows partial mapping of hello data, therefore hello schema definition of JSON format doesn’t have toomap every key which is found in a sample data.</span></span> <span data-ttu-id="da472-175">Также можно сопоставить столбцы, которые не являются частью hello образцов данных.</span><span class="sxs-lookup"><span data-stu-id="da472-175">It can also map columns which are not part of hello sample data.</span></span> 

## <a name="import-data"></a><span data-ttu-id="da472-176">Импорт данных</span><span class="sxs-lookup"><span data-stu-id="da472-176">Import data</span></span>

<span data-ttu-id="da472-177">tooimport данных, передать его tooAzure хранилища, создать ключ доступа для него и затем вызвать API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="da472-177">tooimport data, you upload it tooAzure storage, create an access key for it, and then make a REST API call.</span></span>

![Добавление источника данных](./media/app-insights-analytics-import/analytics-upload-process.png)

<span data-ttu-id="da472-179">Можно выполнить вручную после процесса hello или настройка автоматизированной системы toodo его через регулярные интервалы.</span><span class="sxs-lookup"><span data-stu-id="da472-179">You can perform hello following process manually, or set up an automated system toodo it at regular intervals.</span></span> <span data-ttu-id="da472-180">Вам требуется toofollow эти шаги для каждого блока данных требуется tooimport.</span><span class="sxs-lookup"><span data-stu-id="da472-180">You need toofollow these steps for each block of data you want tooimport.</span></span>

1. <span data-ttu-id="da472-181">Передача данных hello слишком[хранилище больших двоичных объектов](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="da472-181">Upload hello data too[Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> 

 * <span data-ttu-id="da472-182">Большие двоичные объекты могут быть любого размера вверх too1GB несжатых данных.</span><span class="sxs-lookup"><span data-stu-id="da472-182">Blobs can be any size up too1GB uncompressed.</span></span> <span data-ttu-id="da472-183">С точки зрения производительности идеально использовать большие двоичные объекты размером несколько сотен мегабайт.</span><span class="sxs-lookup"><span data-stu-id="da472-183">Large blobs of hundreds of MB are ideal from a performance perspective.</span></span>
 * <span data-ttu-id="da472-184">Он позволяет уменьшить время передачи tooimprove Gzip и задержки для toobe hello данных, доступных для запроса.</span><span class="sxs-lookup"><span data-stu-id="da472-184">You can compress it with Gzip tooimprove upload time and latency for hello data toobe available for query.</span></span> <span data-ttu-id="da472-185">Используйте hello `.gz` расширение имени файла.</span><span class="sxs-lookup"><span data-stu-id="da472-185">Use hello `.gz` filename extension.</span></span>
 * <span data-ttu-id="da472-186">Это наиболее toouse отдельную учетную запись хранилища для этой цели tooavoid вызовы от различных служб снижения производительности.</span><span class="sxs-lookup"><span data-stu-id="da472-186">It's best toouse a separate storage account for this purpose, tooavoid calls from different services slowing performance.</span></span>
 * <span data-ttu-id="da472-187">При отправке данных в высокой частотой, каждые несколько секунд, рекомендуется toouse больше, чем одну учетную запись хранения, для повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="da472-187">When sending data in high frequency, every few seconds, it is recommended toouse more than one storage account, for performance reasons.</span></span>

 
2. <span data-ttu-id="da472-188">[Создайте ключ подписи общего доступа для большого двоичного объекта hello](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="da472-188">[Create a Shared Access Signature key for hello blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span> <span data-ttu-id="da472-189">ключ Hello должны иметь срок действия одного дня и предоставить доступ для чтения.</span><span class="sxs-lookup"><span data-stu-id="da472-189">hello key should have an expiration period of one day and provide read access.</span></span>
3. <span data-ttu-id="da472-190">Сделайте toonotify вызов REST Application Insights, данных находится в состоянии ожидания.</span><span class="sxs-lookup"><span data-stu-id="da472-190">Make a REST call toonotify Application Insights that data is waiting.</span></span>

 * <span data-ttu-id="da472-191">Конечная точка: `https://dc.services.visualstudio.com/v2/track`</span><span class="sxs-lookup"><span data-stu-id="da472-191">Endpoint: `https://dc.services.visualstudio.com/v2/track`</span></span>
 * <span data-ttu-id="da472-192">Метод HTTP: POST</span><span class="sxs-lookup"><span data-stu-id="da472-192">HTTP method: POST</span></span>
 * <span data-ttu-id="da472-193">Полезные данные:</span><span class="sxs-lookup"><span data-stu-id="da472-193">Payload:</span></span>

```JSON

    {
       "data": {
            "baseType":"OpenSchemaData",
            "baseData":{
               "ver":"2",
               "blobSasUri":"<Blob URI with Shared Access Key>",
               "sourceName":"<Schema ID>",
               "sourceVersion":"1.0"
             }
       },
       "ver":1,
       "name":"Microsoft.ApplicationInsights.OpenSchema",
       "time":"<DateTime>",
       "iKey":"<instrumentation key>"
    }
```

<span data-ttu-id="da472-194">Hello местозаполнителей являются:</span><span class="sxs-lookup"><span data-stu-id="da472-194">hello placeholders are:</span></span>

* <span data-ttu-id="da472-195">`Blob URI with Shared Access Key`: Вы получаете это из hello процедуры для создания ключа.</span><span class="sxs-lookup"><span data-stu-id="da472-195">`Blob URI with Shared Access Key`: You get this from hello procedure for creating a key.</span></span> <span data-ttu-id="da472-196">Это конкретных toohello больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="da472-196">It is specific toohello blob.</span></span>
* <span data-ttu-id="da472-197">`Schema ID`: hello идентификатор схемы, созданные для определенной схемы.</span><span class="sxs-lookup"><span data-stu-id="da472-197">`Schema ID`: hello schema ID generated for your defined schema.</span></span> <span data-ttu-id="da472-198">Hello данные этого большого двоичного объекта должны соответствовать схеме toohello.</span><span class="sxs-lookup"><span data-stu-id="da472-198">hello data in this blob should conform toohello schema.</span></span>
* <span data-ttu-id="da472-199">`DateTime`: hello времени, на какие hello отправляется запрос, UTC.</span><span class="sxs-lookup"><span data-stu-id="da472-199">`DateTime`: hello time at which hello request is submitted, UTC.</span></span> <span data-ttu-id="da472-200">Мы принимаем следующие форматы: ISO8601 (например, "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span><span class="sxs-lookup"><span data-stu-id="da472-200">We accept these formats: ISO8601 (like "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span></span>
* <span data-ttu-id="da472-201">`Instrumentation key` для ресурса Application Insights.</span><span class="sxs-lookup"><span data-stu-id="da472-201">`Instrumentation key` of your Application Insights resource.</span></span>

<span data-ttu-id="da472-202">Hello становятся доступными в аналитике через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="da472-202">hello data is available in Analytics after a few minutes.</span></span>

## <a name="error-responses"></a><span data-ttu-id="da472-203">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="da472-203">Error responses</span></span>

* <span data-ttu-id="da472-204">**400 Ошибочный запрос**: указывает hello полезных данных запроса является недопустимым.</span><span class="sxs-lookup"><span data-stu-id="da472-204">**400 bad request**: indicates that hello request payload is invalid.</span></span> <span data-ttu-id="da472-205">Убедитесь, что:</span><span class="sxs-lookup"><span data-stu-id="da472-205">Check:</span></span>
 * <span data-ttu-id="da472-206">указан правильный ключ инструментирования;</span><span class="sxs-lookup"><span data-stu-id="da472-206">Correct instrumentation key.</span></span>
 * <span data-ttu-id="da472-207">указано допустимое значение времени</span><span class="sxs-lookup"><span data-stu-id="da472-207">Valid time value.</span></span> <span data-ttu-id="da472-208">Оно должно быть время hello, теперь в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="da472-208">It should be hello time now in UTC.</span></span>
 * <span data-ttu-id="da472-209">JSON hello события соответствует toohello схемы.</span><span class="sxs-lookup"><span data-stu-id="da472-209">JSON of hello event conforms toohello schema.</span></span>
* <span data-ttu-id="da472-210">**403 Запрещено**: hello больших двоичных объектов, отправленные вами недоступен.</span><span class="sxs-lookup"><span data-stu-id="da472-210">**403 Forbidden**: hello blob you've sent is not accessible.</span></span> <span data-ttu-id="da472-211">Убедитесь, что hello общий ключ доступа является допустимым и не истек.</span><span class="sxs-lookup"><span data-stu-id="da472-211">Make sure that hello shared access key is valid and has not expired.</span></span>
* <span data-ttu-id="da472-212">**404. Не найдено**:</span><span class="sxs-lookup"><span data-stu-id="da472-212">**404 Not Found**:</span></span>
 * <span data-ttu-id="da472-213">Hello большого двоичного объекта не существует.</span><span class="sxs-lookup"><span data-stu-id="da472-213">hello blob doesn't exist.</span></span>
 * <span data-ttu-id="da472-214">Неверный идентификатор sourceId Hello.</span><span class="sxs-lookup"><span data-stu-id="da472-214">hello sourceId is wrong.</span></span>

<span data-ttu-id="da472-215">Более подробные сведения содержатся в hello ответа, сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="da472-215">More detailed information is available in hello response error message.</span></span>


## <a name="sample-code"></a><span data-ttu-id="da472-216">Пример кода</span><span class="sxs-lookup"><span data-stu-id="da472-216">Sample code</span></span>

<span data-ttu-id="da472-217">Этот код использует hello [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="da472-217">This code uses hello [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet package.</span></span>

### <a name="classes"></a><span data-ttu-id="da472-218">Классы</span><span class="sxs-lookup"><span data-stu-id="da472-218">Classes</span></span>

```C#
namespace IngestionClient 
{ 
    using System; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceIngestionRequest 
    { 
        #region Members 
        private const string BaseDataRequiredVersion = "2"; 
        private const string RequestName = "Microsoft.ApplicationInsights.OpenSchema"; 
        #endregion Members 

        public AnalyticsDataSourceIngestionRequest(string ikey, string schemaId, string blobSasUri, int version = 1) 
        { 
            Ver = version; 
            IKey = ikey; 
            Data = new Data 
            { 
                BaseData = new BaseData 
                { 
                    Ver = BaseDataRequiredVersion, 
                    BlobSasUri = blobSasUri, 
                    SourceName = schemaId, 
                    SourceVersion = version.ToString() 
                } 
            }; 
        } 


        [JsonProperty("data")] 
        public Data Data { get; set; } 

        [JsonProperty("ver")] 
        public int Ver { get; set; } 

        [JsonProperty("name")] 
        public string Name { get { return RequestName; } } 

        [JsonProperty("time")] 
        public DateTime Time { get { return DateTime.UtcNow; } } 

        [JsonProperty("iKey")] 
        public string IKey { get; set; } 
    } 

    #region Internal Classes 

    public class Data 
    { 
        private const string DataBaseType = "OpenSchemaData"; 

        [JsonProperty("baseType")] 
        public string BaseType 
        { 
            get { return DataBaseType; } 
        } 

        [JsonProperty("baseData")] 
        public BaseData BaseData { get; set; } 
    } 


    public class BaseData 
    { 
        [JsonProperty("ver")] 
        public string Ver { get; set; } 

        [JsonProperty("blobSasUri")] 
        public string BlobSasUri { get; set; } 

        [JsonProperty("sourceName")] 
        public string SourceName { get; set; } 

        [JsonProperty("sourceVersion")] 
        public string SourceVersion { get; set; } 
    } 

    #endregion Internal Classes 
} 


namespace IngestionClient 
{ 
    using System; 
    using System.IO; 
    using System.Net; 
    using System.Text; 
    using System.Threading.Tasks; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceClient 
    { 
        #region Members 
        private readonly Uri endpoint = new Uri("https://dc.services.visualstudio.com/v2/track"); 
        private const string RequestContentType = "application/json; charset=UTF-8"; 
        private const string RequestAccess = "application/json"; 
        #endregion Members 

        #region Public 

        public async Task<bool> RequestBlobIngestion(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            HttpWebRequest request = WebRequest.CreateHttp(endpoint); 
            request.Method = WebRequestMethods.Http.Post; 
            request.ContentType = RequestContentType; 
            request.Accept = RequestAccess; 

            string notificationJson = Serialize(ingestionRequest); 
            byte[] notificationBytes = GetContentBytes(notificationJson); 
            request.ContentLength = notificationBytes.Length; 

            Stream requestStream = request.GetRequestStream(); 
            requestStream.Write(notificationBytes, 0, notificationBytes.Length); 
            requestStream.Close(); 

            try 
            { 
                using (var response = (HttpWebResponse)await request.GetResponseAsync())
                {
                    return response.StatusCode == HttpStatusCode.OK;
                }
            } 
            catch (WebException e) 
            { 
                HttpWebResponse httpResponse = e.Response as HttpWebResponse; 
                if (httpResponse != null) 
                { 
                    Console.WriteLine( 
                        "Ingestion request failed with status code: {0}. Error: {1}", 
                        httpResponse.StatusCode, 
                        httpResponse.StatusDescription); 
                    return false; 
                }
                throw; 
            } 
        } 
        #endregion Public 

        #region Private 
        private byte[] GetContentBytes(string content) 
        { 
            return Encoding.UTF8.GetBytes(content);
        } 


        private string Serialize(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            return JsonConvert.SerializeObject(ingestionRequest); 
        } 
        #endregion Private 
    } 
} 
```

### <a name="ingest-data"></a><span data-ttu-id="da472-219">Прием данных</span><span class="sxs-lookup"><span data-stu-id="da472-219">Ingest data</span></span>

<span data-ttu-id="da472-220">Используйте этот код для каждого большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="da472-220">Use this code for each blob.</span></span> 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a><span data-ttu-id="da472-221">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="da472-221">Next steps</span></span>

* [<span data-ttu-id="da472-222">Обзор hello язык запросов для анализа журналов</span><span class="sxs-lookup"><span data-stu-id="da472-222">Tour of hello Log Analytics query language</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="da472-223">Используйте *Logstash* tooApplication toosend данных аналитики</span><span class="sxs-lookup"><span data-stu-id="da472-223">Use *Logstash* toosend data tooApplication Insights</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
