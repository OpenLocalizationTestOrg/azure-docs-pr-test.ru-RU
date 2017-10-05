---
title: "Импорт данных в инструмент аналитики в Azure Application Insights | Документация Майкрософт"
description: "Импорт статических данных для объединения с данными телеметрии приложения или импорт отдельного потока данных для выполнения запроса с помощью аналитики."
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
ms.openlocfilehash: aa855a9050ec4e5e7c5db88b7209b8bb48bdba51
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="import-data-into-analytics"></a><span data-ttu-id="e4735-104">Импорт данных в инструмент аналитики</span><span class="sxs-lookup"><span data-stu-id="e4735-104">Import data into Analytics</span></span>

<span data-ttu-id="e4735-105">Импортируйте табличные данные в инструмент [аналитики](app-insights-analytics.md), чтобы объединить их с данными телеметрии [Application Insights](app-insights-overview.md) из приложения или проанализировать в отдельном потоке.</span><span class="sxs-lookup"><span data-stu-id="e4735-105">Import any tabular data into [Analytics](app-insights-analytics.md), either to join it with [Application Insights](app-insights-overview.md) telemetry from your app, or so that you can analyze it as a separate stream.</span></span> <span data-ttu-id="e4735-106">Аналитика — это эффективный язык запросов, который удобно использовать для анализа больших потоков данных телеметрии с метками времени.</span><span class="sxs-lookup"><span data-stu-id="e4735-106">Analytics is a powerful query language well-suited to analyzing high-volume timestamped streams of telemetry.</span></span>

<span data-ttu-id="e4735-107">Вы можете импортировать данные в инструмент аналитики, используя собственную схему.</span><span class="sxs-lookup"><span data-stu-id="e4735-107">You can import data into Analytics using your own schema.</span></span> <span data-ttu-id="e4735-108">В этой схеме не обязательно использовать стандартные схемы Application Insights, например запрос или трассировку.</span><span class="sxs-lookup"><span data-stu-id="e4735-108">It doesn't have to use the standard Application Insights schemas such as request or trace.</span></span>

<span data-ttu-id="e4735-109">Можно импортировать файлы в формате JSON или DSV (значения с разделителями — запятыми, точками с запятой или знаками табуляции).</span><span class="sxs-lookup"><span data-stu-id="e4735-109">You can import JSON or DSV (delimiter-separated values - comma, semicolon or tab) files.</span></span>

<span data-ttu-id="e4735-110">Импорт в инструмент аналитики может понадобиться в трех ситуациях.</span><span class="sxs-lookup"><span data-stu-id="e4735-110">There are three situations where importing to Analytics is useful:</span></span>

* <span data-ttu-id="e4735-111">**Объединение с данными телеметрии приложения.**</span><span class="sxs-lookup"><span data-stu-id="e4735-111">**Join with app telemetry.**</span></span> <span data-ttu-id="e4735-112">Например, вы можете импортировать таблицу, которая сопоставляет URL-адреса веб-сайта с удобными для чтения заголовками страниц.</span><span class="sxs-lookup"><span data-stu-id="e4735-112">For example, you could import a table that maps URLs from your website to more readable page titles.</span></span> <span data-ttu-id="e4735-113">В инструменте аналитики можно создать отчет-диаграмму панели мониторинга, показывающий десять наиболее популярных страниц веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="e4735-113">In Analytics, you can create a dashboard chart report that shows the ten most popular pages in your website.</span></span> <span data-ttu-id="e4735-114">Теперь вместо URL-адресов он может отображать заголовки страниц.</span><span class="sxs-lookup"><span data-stu-id="e4735-114">Now it can show the page titles instead of the URLs.</span></span>
* <span data-ttu-id="e4735-115">**Сопоставление данных телеметрии приложения** с другими источниками, например с отчетом о сетевом трафике, данными сервера или файлами журнала CDN.</span><span class="sxs-lookup"><span data-stu-id="e4735-115">**Correlate your application telemetry** with other sources such as network traffic, server data, or CDN log files.</span></span>
* <span data-ttu-id="e4735-116">**Применение аналитики в отдельном потоке данных.**</span><span class="sxs-lookup"><span data-stu-id="e4735-116">**Apply Analytics to a separate data stream.**</span></span> <span data-ttu-id="e4735-117">Аналитика Application Insights — мощный инструмент, который хорошо работает с разреженным потоками с метками времени. Во многих случаях этот инструмент намного эффективнее, чем SQL.</span><span class="sxs-lookup"><span data-stu-id="e4735-117">Application Insights Analytics is a powerful tool, that works well with sparse, timestamped streams - much better than SQL in many cases.</span></span> <span data-ttu-id="e4735-118">С помощью аналитики вы можете проанализировать такой поток из другого источника.</span><span class="sxs-lookup"><span data-stu-id="e4735-118">If you have such a stream from some other source, you can analyze it with Analytics.</span></span>

<span data-ttu-id="e4735-119">Отправлять данные в источник данных очень легко.</span><span class="sxs-lookup"><span data-stu-id="e4735-119">Sending data to your data source is easy.</span></span> 

1. <span data-ttu-id="e4735-120">(Однократно.) Определите схему данных в источнике данных.</span><span class="sxs-lookup"><span data-stu-id="e4735-120">(One time) Define the schema of your data in a 'data source'.</span></span>
2. <span data-ttu-id="e4735-121">(Периодически.) Передайте данные в службу хранилища Azure и вызовите REST API, чтобы получать уведомления о новых данных, ожидающих приема.</span><span class="sxs-lookup"><span data-stu-id="e4735-121">(Periodically) Upload your data to Azure storage, and call the REST API to notify us that new data is waiting for ingestion.</span></span> <span data-ttu-id="e4735-122">Через несколько минут данные будут доступны для запросов в инструменте аналитики.</span><span class="sxs-lookup"><span data-stu-id="e4735-122">Within a few minutes, the data is available for query in Analytics.</span></span>

<span data-ttu-id="e4735-123">Вы сами определяете частоту передачи и решаете, как скоро данные должны быть доступны для запросов.</span><span class="sxs-lookup"><span data-stu-id="e4735-123">The frequency of the upload is defined by you and how fast would you like your data to be available for queries.</span></span> <span data-ttu-id="e4735-124">Данные лучше передавать блоками большого объема, но не более 1 ГБ.</span><span class="sxs-lookup"><span data-stu-id="e4735-124">It is more efficient to upload data in larger chunks, but not larger than 1GB.</span></span>

> [!NOTE]
> <span data-ttu-id="e4735-125">*Если у вас много источников данных для анализа*,</span><span class="sxs-lookup"><span data-stu-id="e4735-125">*Got lots of data sources to analyze?*</span></span> [<span data-ttu-id="e4735-126">*попробуйте использовать* конвейер logstash *для отправки данных в Application Insights.*</span><span class="sxs-lookup"><span data-stu-id="e4735-126">*Consider using* logstash *to ship your data into Application Insights.*</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a><span data-ttu-id="e4735-127">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="e4735-127">Before you start</span></span>

<span data-ttu-id="e4735-128">Вам необходимы:</span><span class="sxs-lookup"><span data-stu-id="e4735-128">You need:</span></span>

1. <span data-ttu-id="e4735-129">Ресурс Application Insights в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e4735-129">An Application Insights resource in Microsoft Azure.</span></span>

 * <span data-ttu-id="e4735-130">Если вы хотите анализировать данные отдельно от других данных телеметрии, [создайте новый ресурс Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="e4735-130">If you want to analyze your data separately from any other telemetry, [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span>
 * <span data-ttu-id="e4735-131">Если вы объединяете или сравниваете данные с данными телеметрии из приложения, для которого уже настроена надстройка Application Insights, вы можете использовать ресурс этого приложения.</span><span class="sxs-lookup"><span data-stu-id="e4735-131">If you're joining or comparing your data with telemetry from an app that is already set up with Application Insights, then you can use the resource for that app.</span></span>
 * <span data-ttu-id="e4735-132">Права владельца или участника на доступ к этому ресурсу.</span><span class="sxs-lookup"><span data-stu-id="e4735-132">Contributor or owner access to that resource.</span></span>
 
2. <span data-ttu-id="e4735-133">хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="e4735-133">Azure storage.</span></span> <span data-ttu-id="e4735-134">Вы передаете данные в службу хранилища Azure, а инструмент аналитики получает данные из него.</span><span class="sxs-lookup"><span data-stu-id="e4735-134">You upload to Azure storage, and Analytics gets your data from there.</span></span> 

 * <span data-ttu-id="e4735-135">Рекомендуем создать отдельную учетную запись хранения для больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="e4735-135">We recommend you create a dedicated storage account for your blobs.</span></span> <span data-ttu-id="e4735-136">Если большие двоичные объекты используются другими процессами, нашим процессам понадобится больше времени для чтения этих объектов.</span><span class="sxs-lookup"><span data-stu-id="e4735-136">If your blobs are shared with other processes, it takes longer for our processes to read your blobs.</span></span>


## <a name="define-your-schema"></a><span data-ttu-id="e4735-137">Определение схемы</span><span class="sxs-lookup"><span data-stu-id="e4735-137">Define your schema</span></span>

<span data-ttu-id="e4735-138">Прежде чем импортировать данные, необходимо определить *источник данных*, в котором указана схема данных.</span><span class="sxs-lookup"><span data-stu-id="e4735-138">Before you can import data, you must define a *data source,* which specifies the schema of your data.</span></span>
<span data-ttu-id="e4735-139">В отдельном ресурсе Application Insights может быть до 50 источников данных.</span><span class="sxs-lookup"><span data-stu-id="e4735-139">You can have up to 50 data sources in a single Application Insights resource</span></span>

1. <span data-ttu-id="e4735-140">Запустите мастер источников данных.</span><span class="sxs-lookup"><span data-stu-id="e4735-140">Start the data source wizard.</span></span> <span data-ttu-id="e4735-141">Воспользуйтесь кнопкой Add new data source (Добавить новый источник данных).</span><span class="sxs-lookup"><span data-stu-id="e4735-141">Use "Add new data source" button.</span></span> <span data-ttu-id="e4735-142">Кроме того, нажмите кнопку "Параметры" в правом верхнем углу и в раскрывающемся меню выберите "Источники данных".</span><span class="sxs-lookup"><span data-stu-id="e4735-142">Alternatively - click on settings button in right upper corner and choose "Data Sources" in dropdown menu.</span></span>

    ![Добавление источника данных](./media/app-insights-analytics-import/add-new-data-source.png)

    <span data-ttu-id="e4735-144">Введите имя для нового источника данных.</span><span class="sxs-lookup"><span data-stu-id="e4735-144">Provide a name for your new data source.</span></span>

2. <span data-ttu-id="e4735-145">Определите формат файлов, которые требуется передать.</span><span class="sxs-lookup"><span data-stu-id="e4735-145">Define format of the files that you will upload.</span></span>

    <span data-ttu-id="e4735-146">Можно задать формат вручную или передать пример файла.</span><span class="sxs-lookup"><span data-stu-id="e4735-146">You can either define the format manually, or upload a sample file.</span></span>

    <span data-ttu-id="e4735-147">Если используются данные в формате CSV, то первая строка примера может содержать заголовки столбцов.</span><span class="sxs-lookup"><span data-stu-id="e4735-147">If the data is in CSV format, the first row of the sample can be column headers.</span></span> <span data-ttu-id="e4735-148">Вы сможете изменить имена полей на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="e4735-148">You can change the field names in the next step.</span></span>

    <span data-ttu-id="e4735-149">Пример должен содержать по крайней мере 10 строк или записей данных.</span><span class="sxs-lookup"><span data-stu-id="e4735-149">The sample should include at least 10 rows or records of data.</span></span>

    <span data-ttu-id="e4735-150">Имена столбцов или полей должны состоять из букв и цифр (без пробелов и знаков препинания).</span><span class="sxs-lookup"><span data-stu-id="e4735-150">Column or field names should have alphanumeric names (without spaces or punctuation).</span></span>

    ![Передача примера файла](./media/app-insights-analytics-import/sample-data-file.png)


3. <span data-ttu-id="e4735-152">Проверьте схему, которую получил мастер.</span><span class="sxs-lookup"><span data-stu-id="e4735-152">Review the schema that the wizard has got.</span></span> <span data-ttu-id="e4735-153">Если он вывел типы из примера, то, возможно, потребуется настроить выводимые типы столбцов.</span><span class="sxs-lookup"><span data-stu-id="e4735-153">If it inferred the types from a sample, you might need to adjust the inferred types of the columns.</span></span>

    ![Просмотр выводимой схемы](./media/app-insights-analytics-import/data-source-review-schema.png)

 * <span data-ttu-id="e4735-155">(Необязательно.) Отправьте определение схемы.</span><span class="sxs-lookup"><span data-stu-id="e4735-155">(Optional.) Upload a schema definition.</span></span> <span data-ttu-id="e4735-156">Формат приведен ниже.</span><span class="sxs-lookup"><span data-stu-id="e4735-156">See the format below.</span></span>

 * <span data-ttu-id="e4735-157">Выберите метку времени.</span><span class="sxs-lookup"><span data-stu-id="e4735-157">Select a Timestamp.</span></span> <span data-ttu-id="e4735-158">Все данные в инструменте аналитики должны включать поле метки времени.</span><span class="sxs-lookup"><span data-stu-id="e4735-158">All data in Analytics must have a timestamp field.</span></span> <span data-ttu-id="e4735-159">Это должно быть поле даты и времени (`datetime`), но его не обязательно называть timestamp.</span><span class="sxs-lookup"><span data-stu-id="e4735-159">It must have type `datetime`, but it doesn't have to be named 'timestamp'.</span></span> <span data-ttu-id="e4735-160">Если данные содержат столбец, содержащий дату и время в формате ISO, выберите его в качестве столбца метки времени.</span><span class="sxs-lookup"><span data-stu-id="e4735-160">If your data has a column containing a date and time in ISO format, choose this as the timestamp column.</span></span> <span data-ttu-id="e4735-161">Или выберите "по мере поступления данных". В этом случае процесс импорта добавит полу метки времени.</span><span class="sxs-lookup"><span data-stu-id="e4735-161">Otherwise, choose "as data arrived", and the import process will add a timestamp field.</span></span>

5. <span data-ttu-id="e4735-162">Создайте источник данных.</span><span class="sxs-lookup"><span data-stu-id="e4735-162">Create the data source.</span></span>

### <a name="schema-definition-file-format"></a><span data-ttu-id="e4735-163">Формат файла определения схемы</span><span class="sxs-lookup"><span data-stu-id="e4735-163">Schema definition file format</span></span>

<span data-ttu-id="e4735-164">Вместо того, чтобы редактировать схему в пользовательском интерфейсе, загрузите определение схемы из файла.</span><span class="sxs-lookup"><span data-stu-id="e4735-164">Instead of editing the schema in UI, you can load the schema definition from a file.</span></span> <span data-ttu-id="e4735-165">Определение схемы имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="e4735-165">The schema definition format is as follows:</span></span> 

<span data-ttu-id="e4735-166">Формат с разделителями</span><span class="sxs-lookup"><span data-stu-id="e4735-166">Delimited format</span></span> 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

<span data-ttu-id="e4735-167">Формат JSON</span><span class="sxs-lookup"><span data-stu-id="e4735-167">JSON format</span></span> 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
<span data-ttu-id="e4735-168">Каждый столбец идентифицируется по расположению, имени и типу.</span><span class="sxs-lookup"><span data-stu-id="e4735-168">Each column is identified by the location, name and type.</span></span> 

* <span data-ttu-id="e4735-169">Расположение: для формата с разделителями это расположение сопоставленного значения.</span><span class="sxs-lookup"><span data-stu-id="e4735-169">Location – For delimited file format it is the position of the mapped value.</span></span> <span data-ttu-id="e4735-170">Для формата JSON это путь jpath сопоставленного ключа.</span><span class="sxs-lookup"><span data-stu-id="e4735-170">For JSON format, it is the jpath of the mapped key.</span></span>
* <span data-ttu-id="e4735-171">Имя: отображаемое имя столбца.</span><span class="sxs-lookup"><span data-stu-id="e4735-171">Name – the displayed name of the column.</span></span>
* <span data-ttu-id="e4735-172">Тип: тип данных столбца.</span><span class="sxs-lookup"><span data-stu-id="e4735-172">Type – the data type of that column.</span></span>
 
<span data-ttu-id="e4735-173">Если использовался пример данных и формат файла с разделителями, то определение схемы должно сопоставить все столбцы и добавить в конце новые столбцы.</span><span class="sxs-lookup"><span data-stu-id="e4735-173">In case a sample data was used and file format is delimited, the schema definition must map all columns and add new columns at the end.</span></span> 

<span data-ttu-id="e4735-174">Формат JSON позволяет выполнить частичное сопоставление данных, поэтому определение схемы в формате JSON не должно сопоставлять каждый ключ, найденный в примере данных.</span><span class="sxs-lookup"><span data-stu-id="e4735-174">JSON allows partial mapping of the data, therefore the schema definition of JSON format doesn’t have to map every key which is found in a sample data.</span></span> <span data-ttu-id="e4735-175">Оно также может сопоставить столбцы, которые не являются частью примера данных.</span><span class="sxs-lookup"><span data-stu-id="e4735-175">It can also map columns which are not part of the sample data.</span></span> 

## <a name="import-data"></a><span data-ttu-id="e4735-176">Импорт данных</span><span class="sxs-lookup"><span data-stu-id="e4735-176">Import data</span></span>

<span data-ttu-id="e4735-177">Чтобы импортировать данные, передайте их в службу хранилища Azure, создайте ключ доступа и вызовите REST API.</span><span class="sxs-lookup"><span data-stu-id="e4735-177">To import data, you upload it to Azure storage, create an access key for it, and then make a REST API call.</span></span>

![Добавление источника данных](./media/app-insights-analytics-import/analytics-upload-process.png)

<span data-ttu-id="e4735-179">Вы можете выполнить описанный ниже процесс вручную или настроить автоматизированную систему, которая будет делать это регулярно.</span><span class="sxs-lookup"><span data-stu-id="e4735-179">You can perform the following process manually, or set up an automated system to do it at regular intervals.</span></span> <span data-ttu-id="e4735-180">Выполните следующие шаги для каждого блока данных, которые нужно импортировать.</span><span class="sxs-lookup"><span data-stu-id="e4735-180">You need to follow these steps for each block of data you want to import.</span></span>

1. <span data-ttu-id="e4735-181">Отправьте данные в [хранилище BLOB-объектов Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="e4735-181">Upload the data to [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> 

 * <span data-ttu-id="e4735-182">Размер больших двоичных объектов в несжатом виде не должен превышать 1 ГБ.</span><span class="sxs-lookup"><span data-stu-id="e4735-182">Blobs can be any size up to 1GB uncompressed.</span></span> <span data-ttu-id="e4735-183">С точки зрения производительности идеально использовать большие двоичные объекты размером несколько сотен мегабайт.</span><span class="sxs-lookup"><span data-stu-id="e4735-183">Large blobs of hundreds of MB are ideal from a performance perspective.</span></span>
 * <span data-ttu-id="e4735-184">Чтобы сократить время передачи и минимизировать задержку доступности данных для запроса, сожмите данные с помощью Gzip.</span><span class="sxs-lookup"><span data-stu-id="e4735-184">You can compress it with Gzip to improve upload time and latency for the data to be available for query.</span></span> <span data-ttu-id="e4735-185">Используйте расширение файла `.gz`.</span><span class="sxs-lookup"><span data-stu-id="e4735-185">Use the `.gz` filename extension.</span></span>
 * <span data-ttu-id="e4735-186">Для этой цели рекомендуется использовать отдельную учетную запись хранения, чтобы избежать вызовов от разных служб, снижающих производительность.</span><span class="sxs-lookup"><span data-stu-id="e4735-186">It's best to use a separate storage account for this purpose, to avoid calls from different services slowing performance.</span></span>
 * <span data-ttu-id="e4735-187">При отправке данных с высокой частотой (каждые несколько секунд) рекомендуется использовать более одной учетной записи хранения, чтобы повысить производительность.</span><span class="sxs-lookup"><span data-stu-id="e4735-187">When sending data in high frequency, every few seconds, it is recommended to use more than one storage account, for performance reasons.</span></span>

 
2. <span data-ttu-id="e4735-188">[Создайте ключ подписанного URL-адреса для большого двоичного объекта](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="e4735-188">[Create a Shared Access Signature key for the blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span> <span data-ttu-id="e4735-189">Ключ должен иметь срок действия один день и предоставлять доступ для чтения.</span><span class="sxs-lookup"><span data-stu-id="e4735-189">The key should have an expiration period of one day and provide read access.</span></span>
3. <span data-ttu-id="e4735-190">Вызовите REST, чтобы уведомить Application Insights о данных, которые ожидают приема.</span><span class="sxs-lookup"><span data-stu-id="e4735-190">Make a REST call to notify Application Insights that data is waiting.</span></span>

 * <span data-ttu-id="e4735-191">Конечная точка: `https://dc.services.visualstudio.com/v2/track`</span><span class="sxs-lookup"><span data-stu-id="e4735-191">Endpoint: `https://dc.services.visualstudio.com/v2/track`</span></span>
 * <span data-ttu-id="e4735-192">Метод HTTP: POST</span><span class="sxs-lookup"><span data-stu-id="e4735-192">HTTP method: POST</span></span>
 * <span data-ttu-id="e4735-193">Полезные данные:</span><span class="sxs-lookup"><span data-stu-id="e4735-193">Payload:</span></span>

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

<span data-ttu-id="e4735-194">Заполнители:</span><span class="sxs-lookup"><span data-stu-id="e4735-194">The placeholders are:</span></span>

* <span data-ttu-id="e4735-195">`Blob URI with Shared Access Key` — вы получаете этот заполнитель во время создания ключа.</span><span class="sxs-lookup"><span data-stu-id="e4735-195">`Blob URI with Shared Access Key`: You get this from the procedure for creating a key.</span></span> <span data-ttu-id="e4735-196">Он относится к большому двоичному объекту.</span><span class="sxs-lookup"><span data-stu-id="e4735-196">It is specific to the blob.</span></span>
* <span data-ttu-id="e4735-197">`Schema ID` — идентификатор схемы, созданный для определенной схемы.</span><span class="sxs-lookup"><span data-stu-id="e4735-197">`Schema ID`: The schema ID generated for your defined schema.</span></span> <span data-ttu-id="e4735-198">Данные в большом двоичном объекте должны соответствовать схеме.</span><span class="sxs-lookup"><span data-stu-id="e4735-198">The data in this blob should conform to the schema.</span></span>
* <span data-ttu-id="e4735-199">`DateTime` — время отправки запроса в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="e4735-199">`DateTime`: The time at which the request is submitted, UTC.</span></span> <span data-ttu-id="e4735-200">Мы принимаем следующие форматы: ISO8601 (например, "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span><span class="sxs-lookup"><span data-stu-id="e4735-200">We accept these formats: ISO8601 (like "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span></span>
* <span data-ttu-id="e4735-201">`Instrumentation key` для ресурса Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e4735-201">`Instrumentation key` of your Application Insights resource.</span></span>

<span data-ttu-id="e4735-202">Данные будут доступны в аналитике через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="e4735-202">The data is available in Analytics after a few minutes.</span></span>

## <a name="error-responses"></a><span data-ttu-id="e4735-203">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="e4735-203">Error responses</span></span>

* <span data-ttu-id="e4735-204">**400. Недопустимый запрос** — означает, что запрос содержит недопустимые полезные данные.</span><span class="sxs-lookup"><span data-stu-id="e4735-204">**400 bad request**: indicates that the request payload is invalid.</span></span> <span data-ttu-id="e4735-205">Убедитесь, что:</span><span class="sxs-lookup"><span data-stu-id="e4735-205">Check:</span></span>
 * <span data-ttu-id="e4735-206">указан правильный ключ инструментирования;</span><span class="sxs-lookup"><span data-stu-id="e4735-206">Correct instrumentation key.</span></span>
 * <span data-ttu-id="e4735-207">указано допустимое значение времени</span><span class="sxs-lookup"><span data-stu-id="e4735-207">Valid time value.</span></span> <span data-ttu-id="e4735-208">(должно быть указано текущее время UTC);</span><span class="sxs-lookup"><span data-stu-id="e4735-208">It should be the time now in UTC.</span></span>
 * <span data-ttu-id="e4735-209">Данные JSON события соответствуют схеме.</span><span class="sxs-lookup"><span data-stu-id="e4735-209">JSON of the event conforms to the schema.</span></span>
* <span data-ttu-id="e4735-210">**403. Запрещено** — отправленный большой двоичный объект недоступен.</span><span class="sxs-lookup"><span data-stu-id="e4735-210">**403 Forbidden**: The blob you've sent is not accessible.</span></span> <span data-ttu-id="e4735-211">Убедитесь, что общий ключ доступа является допустимым и срок его действия не истек.</span><span class="sxs-lookup"><span data-stu-id="e4735-211">Make sure that the shared access key is valid and has not expired.</span></span>
* <span data-ttu-id="e4735-212">**404. Не найдено**:</span><span class="sxs-lookup"><span data-stu-id="e4735-212">**404 Not Found**:</span></span>
 * <span data-ttu-id="e4735-213">большой двоичный объект не существует;</span><span class="sxs-lookup"><span data-stu-id="e4735-213">The blob doesn't exist.</span></span>
 * <span data-ttu-id="e4735-214">Неправильный идентификатор sourceId.</span><span class="sxs-lookup"><span data-stu-id="e4735-214">The sourceId is wrong.</span></span>

<span data-ttu-id="e4735-215">Подробные сведения см. в сообщении об ошибке.</span><span class="sxs-lookup"><span data-stu-id="e4735-215">More detailed information is available in the response error message.</span></span>


## <a name="sample-code"></a><span data-ttu-id="e4735-216">Пример кода</span><span class="sxs-lookup"><span data-stu-id="e4735-216">Sample code</span></span>

<span data-ttu-id="e4735-217">Этот код использует пакет NuGet [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1).</span><span class="sxs-lookup"><span data-stu-id="e4735-217">This code uses the [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet package.</span></span>

### <a name="classes"></a><span data-ttu-id="e4735-218">Классы</span><span class="sxs-lookup"><span data-stu-id="e4735-218">Classes</span></span>

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

### <a name="ingest-data"></a><span data-ttu-id="e4735-219">Прием данных</span><span class="sxs-lookup"><span data-stu-id="e4735-219">Ingest data</span></span>

<span data-ttu-id="e4735-220">Используйте этот код для каждого большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="e4735-220">Use this code for each blob.</span></span> 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a><span data-ttu-id="e4735-221">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e4735-221">Next steps</span></span>

* [<span data-ttu-id="e4735-222">Знакомство с аналитикой в Application Insights</span><span class="sxs-lookup"><span data-stu-id="e4735-222">Tour of the Log Analytics query language</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="e4735-223">Использование *Logstash* для отправки данных в Application Insights</span><span class="sxs-lookup"><span data-stu-id="e4735-223">Use *Logstash* to send data to Application Insights</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
