---
title: "форматы aaaFile и сжатия в фабрике данных Azure | Документы Microsoft"
description: "Дополнительные сведения о форматах файлов hello, поддерживаемых фабрикой данных Azure."
keywords: "данные BLOB-объектов, копирование BLOB-объекта Azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 9d40517b059fc533776bcc088db8c531ee5b003d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a><span data-ttu-id="93bde-104">Форматы файлов и сжатия данных, поддерживаемые фабрикой данных Azure</span><span class="sxs-lookup"><span data-stu-id="93bde-104">File and compression formats supported by Azure Data Factory</span></span>
<span data-ttu-id="93bde-105">*В этом разделе рассматриваются следующие соединители toohello: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [больших двоичных объектов Azure](data-factory-azure-blob-connector.md), [хранилища Озера данных Azure](data-factory-azure-datalake-connector.md), [файловой системы](data-factory-onprem-file-system-connector.md), [ FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), и [SFTP](data-factory-sftp-connector.md).*</span><span class="sxs-lookup"><span data-stu-id="93bde-105">*This topic applies toohello following connectors: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [File System](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), and [SFTP](data-factory-sftp-connector.md).*</span></span>

<span data-ttu-id="93bde-106">Фабрика данных Azure поддерживает следующие типы формата файла hello:</span><span class="sxs-lookup"><span data-stu-id="93bde-106">Azure Data Factory supports hello following file format types:</span></span>

* <span data-ttu-id="93bde-107">[текстовый формат](#text-format);</span><span class="sxs-lookup"><span data-stu-id="93bde-107">[Text format](#text-format)</span></span>
* <span data-ttu-id="93bde-108">[формат JSON](#json-format);</span><span class="sxs-lookup"><span data-stu-id="93bde-108">[JSON format](#json-format)</span></span>
* <span data-ttu-id="93bde-109">[формат Avro](#avro-format);</span><span class="sxs-lookup"><span data-stu-id="93bde-109">[Avro format](#avro-format)</span></span>
* <span data-ttu-id="93bde-110">[формат ORC](#orc-format);</span><span class="sxs-lookup"><span data-stu-id="93bde-110">[ORC format](#orc-format)</span></span>
* <span data-ttu-id="93bde-111">[формат Parquet](#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="93bde-111">[Parquet format](#parquet-format)</span></span>

## <a name="text-format"></a><span data-ttu-id="93bde-112">Текстовый формат</span><span class="sxs-lookup"><span data-stu-id="93bde-112">Text format</span></span>
<span data-ttu-id="93bde-113">Если требуется tooread из текстового файла или запись tooa текстовый файл, задайте hello `type` свойство в hello `format` части набора данных hello слишком**TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="93bde-113">If you want tooread from a text file or write tooa text file, set hello `type` property in hello `format` section of hello dataset too**TextFormat**.</span></span> <span data-ttu-id="93bde-114">Можно также указать следующие hello **необязательно** свойства в hello `format` раздела.</span><span class="sxs-lookup"><span data-stu-id="93bde-114">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="93bde-115">В разделе [примере TextFormat](#textformat-example) раздел, в tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="93bde-115">See [TextFormat example](#textformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="93bde-116">Свойство</span><span class="sxs-lookup"><span data-stu-id="93bde-116">Property</span></span> | <span data-ttu-id="93bde-117">Описание</span><span class="sxs-lookup"><span data-stu-id="93bde-117">Description</span></span> | <span data-ttu-id="93bde-118">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="93bde-118">Allowed values</span></span> | <span data-ttu-id="93bde-119">Обязательно</span><span class="sxs-lookup"><span data-stu-id="93bde-119">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="93bde-120">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="93bde-120">columnDelimiter</span></span> |<span data-ttu-id="93bde-121">символ Hello использовать tooseparate столбцов в файле.</span><span class="sxs-lookup"><span data-stu-id="93bde-121">hello character used tooseparate columns in a file.</span></span> <span data-ttu-id="93bde-122">Можно рассмотреть toouse редких непечатаемые char, может не скорее всего, существует в данных.</span><span class="sxs-lookup"><span data-stu-id="93bde-122">You can consider toouse a rare unprintable char that may not likely exists in your data.</span></span> <span data-ttu-id="93bde-123">Например, укажите "\u0001", что соответствует символу начала заголовка (SOH).</span><span class="sxs-lookup"><span data-stu-id="93bde-123">For example, specify "\u0001", which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="93bde-124">Допускается только один знак.</span><span class="sxs-lookup"><span data-stu-id="93bde-124">Only one character is allowed.</span></span> <span data-ttu-id="93bde-125">Hello **по умолчанию** значение **запятая (,)**.</span><span class="sxs-lookup"><span data-stu-id="93bde-125">hello **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="93bde-126">toouse символ Юникода ссылаться слишком[символов Юникода](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello соответствующий код для него.</span><span class="sxs-lookup"><span data-stu-id="93bde-126">toouse a Unicode character, refer too[Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello corresponding code for it.</span></span> |<span data-ttu-id="93bde-127">Нет</span><span class="sxs-lookup"><span data-stu-id="93bde-127">No</span></span> |
| <span data-ttu-id="93bde-128">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="93bde-128">rowDelimiter</span></span> |<span data-ttu-id="93bde-129">символ Hello использовать tooseparate строк в файле.</span><span class="sxs-lookup"><span data-stu-id="93bde-129">hello character used tooseparate rows in a file.</span></span> |<span data-ttu-id="93bde-130">Допускается только один знак.</span><span class="sxs-lookup"><span data-stu-id="93bde-130">Only one character is allowed.</span></span> <span data-ttu-id="93bde-131">Hello **по умолчанию** значение представляет собой любой hello последующих значений на чтение: **[«\r\n», «\r», «\n»]** и **«\r\n»** при записи.</span><span class="sxs-lookup"><span data-stu-id="93bde-131">hello **default** value is any of hello following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="93bde-132">Нет</span><span class="sxs-lookup"><span data-stu-id="93bde-132">No</span></span> |
| <span data-ttu-id="93bde-133">escapeChar</span><span class="sxs-lookup"><span data-stu-id="93bde-133">escapeChar</span></span> |<span data-ttu-id="93bde-134">специальный символ Hello использовать tooescape разделитель столбцов в hello содержимое входного файла.</span><span class="sxs-lookup"><span data-stu-id="93bde-134">hello special character used tooescape a column delimiter in hello content of input file.</span></span> <br/><br/><span data-ttu-id="93bde-135">Для таблицы нельзя указать и escapeChar, и quoteChar.</span><span class="sxs-lookup"><span data-stu-id="93bde-135">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="93bde-136">Допускается только один знак.</span><span class="sxs-lookup"><span data-stu-id="93bde-136">Only one character is allowed.</span></span> <span data-ttu-id="93bde-137">Значение по умолчанию отсутствует.</span><span class="sxs-lookup"><span data-stu-id="93bde-137">No default value.</span></span> <br/><br/><span data-ttu-id="93bde-138">Пример: при наличии запятая («,») как разделитель столбцов hello, но его необходимо toohave hello запятая в тексте hello (пример: «Hello, world»), можно определить как hello escape-символ «$» и использовать строку «Hello$, world» в источнике hello.</span><span class="sxs-lookup"><span data-stu-id="93bde-138">Example: if you have comma (',') as hello column delimiter but you want toohave hello comma character in hello text (example: "Hello, world"), you can define ‘$’ as hello escape character and use string "Hello$, world" in hello source.</span></span> |<span data-ttu-id="93bde-139">Нет</span><span class="sxs-lookup"><span data-stu-id="93bde-139">No</span></span> |
| <span data-ttu-id="93bde-140">quoteChar</span><span class="sxs-lookup"><span data-stu-id="93bde-140">quoteChar</span></span> |<span data-ttu-id="93bde-141">использовать знак Hello tooquote строковое значение.</span><span class="sxs-lookup"><span data-stu-id="93bde-141">hello character used tooquote a string value.</span></span> <span data-ttu-id="93bde-142">Hello разделители столбцов и строк внутри кавычек hello будет рассматриваться как часть hello строковое значение.</span><span class="sxs-lookup"><span data-stu-id="93bde-142">hello column and row delimiters inside hello quote characters would be treated as part of hello string value.</span></span> <span data-ttu-id="93bde-143">Это свойство является применимо tooboth ввода и вывода наборов данных.</span><span class="sxs-lookup"><span data-stu-id="93bde-143">This property is applicable tooboth input and output datasets.</span></span><br/><br/><span data-ttu-id="93bde-144">Для таблицы нельзя указать и escapeChar, и quoteChar.</span><span class="sxs-lookup"><span data-stu-id="93bde-144">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="93bde-145">Допускается только один знак.</span><span class="sxs-lookup"><span data-stu-id="93bde-145">Only one character is allowed.</span></span> <span data-ttu-id="93bde-146">Значение по умолчанию отсутствует.</span><span class="sxs-lookup"><span data-stu-id="93bde-146">No default value.</span></span> <br/><br/><span data-ttu-id="93bde-147">Например, если у вас есть запятая («,») как разделитель столбцов hello, но его необходимо toohave запятая в тексте hello (пример: < Hello, world >), можно определить» (двойная кавычка) как hello знак кавычек, чтобы использовать строку hello «Hello, world» в источнике hello.</span><span class="sxs-lookup"><span data-stu-id="93bde-147">For example, if you have comma (',') as hello column delimiter but you want toohave comma character in hello text (example: <Hello, world>), you can define " (double quote) as hello quote character and use hello string "Hello, world" in hello source.</span></span> |<span data-ttu-id="93bde-148">Нет</span><span class="sxs-lookup"><span data-stu-id="93bde-148">No</span></span> |
| <span data-ttu-id="93bde-149">nullValue</span><span class="sxs-lookup"><span data-stu-id="93bde-149">nullValue</span></span> |<span data-ttu-id="93bde-150">Один или несколько символов используется toorepresent значение null.</span><span class="sxs-lookup"><span data-stu-id="93bde-150">One or more characters used toorepresent a null value.</span></span> |<span data-ttu-id="93bde-151">Один или несколько знаков.</span><span class="sxs-lookup"><span data-stu-id="93bde-151">One or more characters.</span></span> <span data-ttu-id="93bde-152">Hello **по умолчанию** значения **«\N» и «NULL»** для чтения и **«\N»** при записи.</span><span class="sxs-lookup"><span data-stu-id="93bde-152">hello **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="93bde-153">Нет</span><span class="sxs-lookup"><span data-stu-id="93bde-153">No</span></span> |
| <span data-ttu-id="93bde-154">encodingName</span><span class="sxs-lookup"><span data-stu-id="93bde-154">encodingName</span></span> |<span data-ttu-id="93bde-155">Укажите название кодировки hello.</span><span class="sxs-lookup"><span data-stu-id="93bde-155">Specify hello encoding name.</span></span> |<span data-ttu-id="93bde-156">Допустимое имя кодировки.</span><span class="sxs-lookup"><span data-stu-id="93bde-156">A valid encoding name.</span></span> <span data-ttu-id="93bde-157">Ознакомьтесь с описанием свойства [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="93bde-157">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="93bde-158">Пример: windows-1250 или shift_jis.</span><span class="sxs-lookup"><span data-stu-id="93bde-158">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="93bde-159">Hello **по умолчанию** значение **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="93bde-159">hello **default** value is **UTF-8**.</span></span> |<span data-ttu-id="93bde-160">Нет</span><span class="sxs-lookup"><span data-stu-id="93bde-160">No</span></span> |
| <span data-ttu-id="93bde-161">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="93bde-161">firstRowAsHeader</span></span> |<span data-ttu-id="93bde-162">Указывает, является ли tooconsider hello первую строку как заголовок.</span><span class="sxs-lookup"><span data-stu-id="93bde-162">Specifies whether tooconsider hello first row as a header.</span></span> <span data-ttu-id="93bde-163">Фабрика данных считывает первую строку входного набора данных как заголовок.</span><span class="sxs-lookup"><span data-stu-id="93bde-163">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="93bde-164">Фабрика данных записывает первую строку как заголовок в выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="93bde-164">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="93bde-165">Примеры сценариев см. в разделе [Сценарии использования `firstRowAsHeader` и `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount).</span><span class="sxs-lookup"><span data-stu-id="93bde-165">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="93bde-166">Да</span><span class="sxs-lookup"><span data-stu-id="93bde-166">True</span></span><br/><span data-ttu-id="93bde-167"><b>False (по умолчанию)</b></span><span class="sxs-lookup"><span data-stu-id="93bde-167"><b>False (default)</b></span></span> |<span data-ttu-id="93bde-168">Нет</span><span class="sxs-lookup"><span data-stu-id="93bde-168">No</span></span> |
| <span data-ttu-id="93bde-169">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="93bde-169">skipLineCount</span></span> |<span data-ttu-id="93bde-170">Указывает номер hello tooskip строк, при считывании данных из входных файлов.</span><span class="sxs-lookup"><span data-stu-id="93bde-170">Indicates hello number of rows tooskip when reading data from input files.</span></span> <span data-ttu-id="93bde-171">Если указаны skipLineCount и firstRowAsHeader, hello строки пропускаются сначала и затем сведения о заголовке hello считывается из входного файла hello.</span><span class="sxs-lookup"><span data-stu-id="93bde-171">If both skipLineCount and firstRowAsHeader are specified, hello lines are skipped first and then hello header information is read from hello input file.</span></span> <br/><br/><span data-ttu-id="93bde-172">Примеры сценариев см. в разделе [Сценарии использования `firstRowAsHeader` и `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount).</span><span class="sxs-lookup"><span data-stu-id="93bde-172">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="93bde-173">Целое число </span><span class="sxs-lookup"><span data-stu-id="93bde-173">Integer</span></span> |<span data-ttu-id="93bde-174">Нет</span><span class="sxs-lookup"><span data-stu-id="93bde-174">No</span></span> |
| <span data-ttu-id="93bde-175">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="93bde-175">treatEmptyAsNull</span></span> |<span data-ttu-id="93bde-176">Указывает, является ли tootreat null или пустую строку как строку null значения при считывании данных из входного файла.</span><span class="sxs-lookup"><span data-stu-id="93bde-176">Specifies whether tootreat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="93bde-177">**True (по умолчанию)**</span><span class="sxs-lookup"><span data-stu-id="93bde-177">**True (default)**</span></span><br/><span data-ttu-id="93bde-178">Ложь</span><span class="sxs-lookup"><span data-stu-id="93bde-178">False</span></span> |<span data-ttu-id="93bde-179">Нет</span><span class="sxs-lookup"><span data-stu-id="93bde-179">No</span></span> |

### <a name="textformat-example"></a><span data-ttu-id="93bde-180">Пример TextFormat</span><span class="sxs-lookup"><span data-stu-id="93bde-180">TextFormat example</span></span>
<span data-ttu-id="93bde-181">В hello после определения JSON для набора данных задаются некоторые из дополнительных свойств hello.</span><span class="sxs-lookup"><span data-stu-id="93bde-181">In hello following JSON definition for a dataset, some of hello optional properties are specified.</span></span>

```json
"typeProperties":
{
    "folderPath": "mycontainer/myfolder",
    "fileName": "myblobname",
    "format":
    {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";",
        "quoteChar": "\"",
        "NullValue": "NaN",
        "firstRowAsHeader": true,
        "skipLineCount": 0,
        "treatEmptyAsNull": true
    }
},
```

<span data-ttu-id="93bde-182">toouse `escapeChar` вместо `quoteChar`, замените строку hello с `quoteChar` с hello использовать escapeChar следующие:</span><span class="sxs-lookup"><span data-stu-id="93bde-182">toouse an `escapeChar` instead of `quoteChar`, replace hello line with `quoteChar` with hello following escapeChar:</span></span>

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="93bde-183">Сценарии использования firstRowAsHeader и skipLineCount</span><span class="sxs-lookup"><span data-stu-id="93bde-183">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="93bde-184">Копирование из файла источника, не являющимся файлами tooa и хотите tooadd заголовка строки, содержащей hello схемы метаданных (например: SQL-схема).</span><span class="sxs-lookup"><span data-stu-id="93bde-184">You are copying from a non-file source tooa text file and would like tooadd a header line containing hello schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="93bde-185">Укажите `firstRowAsHeader` как true в hello выходной набор данных для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="93bde-185">Specify `firstRowAsHeader` as true in hello output dataset for this scenario.</span></span>
* <span data-ttu-id="93bde-186">Копирование из текстового файла, содержащего приемник не являющимся файлами tooa заголовка строки и хотите toodrop, строка.</span><span class="sxs-lookup"><span data-stu-id="93bde-186">You are copying from a text file containing a header line tooa non-file sink and would like toodrop that line.</span></span> <span data-ttu-id="93bde-187">Укажите `firstRowAsHeader` как true во входном наборе данных hello.</span><span class="sxs-lookup"><span data-stu-id="93bde-187">Specify `firstRowAsHeader` as true in hello input dataset.</span></span>
* <span data-ttu-id="93bde-188">Копирование из текстового файла и хотите tooskip несколько строк в начале hello, которые не содержат данных или заголовка информации.</span><span class="sxs-lookup"><span data-stu-id="93bde-188">You are copying from a text file and want tooskip a few lines at hello beginning that contain no data or header information.</span></span> <span data-ttu-id="93bde-189">Укажите `skipLineCount` tooindicate hello число строк toobe пропущено.</span><span class="sxs-lookup"><span data-stu-id="93bde-189">Specify `skipLineCount` tooindicate hello number of lines toobe skipped.</span></span> <span data-ttu-id="93bde-190">Если hello остальной части файла hello содержит строку заголовка, можно указать `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="93bde-190">If hello rest of hello file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="93bde-191">Если оба `skipLineCount` и `firstRowAsHeader` указаны, hello строки пропускаются сначала и затем сведения о заголовке hello считывается из входного файла hello</span><span class="sxs-lookup"><span data-stu-id="93bde-191">If both `skipLineCount` and `firstRowAsHeader` are specified, hello lines are skipped first and then hello header information is read from hello input file</span></span>

## <a name="json-format"></a><span data-ttu-id="93bde-192">Формат JSON</span><span class="sxs-lookup"><span data-stu-id="93bde-192">JSON format</span></span>
<span data-ttu-id="93bde-193">слишком**импорта и экспорта файла JSON как-в / из базы данных Azure Cosmos**, hello см. в разделе [документов JSON импорта и экспорта](data-factory-azure-documentdb-connector.md#importexport-json-documents) статьи [перемещения данных из базы данных Azure Cosmos](data-factory-azure-documentdb-connector.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="93bde-193">too**import/export a JSON file as-is into/from Azure Cosmos DB**, hello see [Import/export JSON documents](data-factory-azure-documentdb-connector.md#importexport-json-documents) section in [Move data to/from Azure Cosmos DB](data-factory-azure-documentdb-connector.md) article.</span></span>

<span data-ttu-id="93bde-194">Если требуется tooparse hello JSON-файлов или запись данных hello в формате JSON, задайте hello `type` свойство в hello `format` статьи слишком**JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="93bde-194">If you want tooparse hello JSON files or write hello data in JSON format, set hello `type` property in hello `format` section too**JsonFormat**.</span></span> <span data-ttu-id="93bde-195">Можно также указать следующие hello **необязательно** свойства в hello `format` раздела.</span><span class="sxs-lookup"><span data-stu-id="93bde-195">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="93bde-196">В разделе [JsonFormat пример](#jsonformat-example) раздел, в tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="93bde-196">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="93bde-197">Свойство</span><span class="sxs-lookup"><span data-stu-id="93bde-197">Property</span></span> | <span data-ttu-id="93bde-198">Описание</span><span class="sxs-lookup"><span data-stu-id="93bde-198">Description</span></span> | <span data-ttu-id="93bde-199">Обязательно</span><span class="sxs-lookup"><span data-stu-id="93bde-199">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="93bde-200">filePattern</span><span class="sxs-lookup"><span data-stu-id="93bde-200">filePattern</span></span> |<span data-ttu-id="93bde-201">Укажите шаблон hello данных, хранящихся в каждом файле JSON.</span><span class="sxs-lookup"><span data-stu-id="93bde-201">Indicate hello pattern of data stored in each JSON file.</span></span> <span data-ttu-id="93bde-202">Допустимые значения: **setOfObjects** и **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="93bde-202">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="93bde-203">Hello **по умолчанию** значение **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="93bde-203">hello **default** value is **setOfObjects**.</span></span> <span data-ttu-id="93bde-204">Подробные сведения об этих шаблонах см. в разделе [Шаблоны файлов JSON](#json-file-patterns).</span><span class="sxs-lookup"><span data-stu-id="93bde-204">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="93bde-205">Нет</span><span class="sxs-lookup"><span data-stu-id="93bde-205">No</span></span> |
| <span data-ttu-id="93bde-206">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="93bde-206">jsonNodeReference</span></span> | <span data-ttu-id="93bde-207">Tooiterate и извлечения данных из объектов hello в массив полей с hello же шаблон, укажите путь к JSON hello этого массива.</span><span class="sxs-lookup"><span data-stu-id="93bde-207">If you want tooiterate and extract data from hello objects inside an array field with hello same pattern, specify hello JSON path of that array.</span></span> <span data-ttu-id="93bde-208">Это свойство поддерживается только в том случае, если данные копируются из JSON-файлов.</span><span class="sxs-lookup"><span data-stu-id="93bde-208">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="93bde-209">Нет</span><span class="sxs-lookup"><span data-stu-id="93bde-209">No</span></span> |
| <span data-ttu-id="93bde-210">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="93bde-210">jsonPathDefinition</span></span> | <span data-ttu-id="93bde-211">Укажите hello выражения пути JSON для каждого сопоставления столбцов с именем пользовательские столбца (начало строчных).</span><span class="sxs-lookup"><span data-stu-id="93bde-211">Specify hello JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="93bde-212">Это свойство поддерживается только в том случае, если данные копируются из JSON-файлов и данные можно извлечь из объекта или массива.</span><span class="sxs-lookup"><span data-stu-id="93bde-212">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="93bde-213">Для поля в корневой объект, начинаться с $ корневой; для полей внутри массива hello выбирается программой `jsonNodeReference` свойство начинаются с Привет элемента массива.</span><span class="sxs-lookup"><span data-stu-id="93bde-213">For fields under root object, start with root $; for fields inside hello array chosen by `jsonNodeReference` property, start from hello array element.</span></span> <span data-ttu-id="93bde-214">В разделе [JsonFormat пример](#jsonformat-example) раздел, в tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="93bde-214">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span> | <span data-ttu-id="93bde-215">Нет</span><span class="sxs-lookup"><span data-stu-id="93bde-215">No</span></span> |
| <span data-ttu-id="93bde-216">encodingName</span><span class="sxs-lookup"><span data-stu-id="93bde-216">encodingName</span></span> |<span data-ttu-id="93bde-217">Укажите название кодировки hello.</span><span class="sxs-lookup"><span data-stu-id="93bde-217">Specify hello encoding name.</span></span> <span data-ttu-id="93bde-218">Hello список допустимых названий кодировок см. в разделе: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) свойство.</span><span class="sxs-lookup"><span data-stu-id="93bde-218">For hello list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="93bde-219">Например: windows-1250 или shift_jis.</span><span class="sxs-lookup"><span data-stu-id="93bde-219">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="93bde-220">Hello **по умолчанию** значение: **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="93bde-220">hello **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="93bde-221">Нет</span><span class="sxs-lookup"><span data-stu-id="93bde-221">No</span></span> |
| <span data-ttu-id="93bde-222">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="93bde-222">nestingSeparator</span></span> |<span data-ttu-id="93bde-223">Символ, используемые tooseparate уровней вложения.</span><span class="sxs-lookup"><span data-stu-id="93bde-223">Character that is used tooseparate nesting levels.</span></span> <span data-ttu-id="93bde-224">значение по умолчанию Hello "." (точка).</span><span class="sxs-lookup"><span data-stu-id="93bde-224">hello default value is '.' (dot).</span></span> |<span data-ttu-id="93bde-225">Нет</span><span class="sxs-lookup"><span data-stu-id="93bde-225">No</span></span> |

### <a name="json-file-patterns"></a><span data-ttu-id="93bde-226">Шаблоны файлов JSON</span><span class="sxs-lookup"><span data-stu-id="93bde-226">JSON file patterns</span></span>

<span data-ttu-id="93bde-227">Действие копирования можно обработать hello следующие шаблоны файлов JSON:</span><span class="sxs-lookup"><span data-stu-id="93bde-227">Copy activity can parse hello following patterns of JSON files:</span></span>

- <span data-ttu-id="93bde-228">**Тип 1: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="93bde-228">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="93bde-229">Каждый файл содержит один объект или несколько разделенных строками или объединенных объектов.</span><span class="sxs-lookup"><span data-stu-id="93bde-229">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="93bde-230">Если этот параметр выбран в выходном наборе данных, то в результате копирования будет создан JSON-файл, где каждый объект будет находиться в отдельной строке (файл с разделителем-строкой).</span><span class="sxs-lookup"><span data-stu-id="93bde-230">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="93bde-231">**Пример единого объекта JSON**</span><span class="sxs-lookup"><span data-stu-id="93bde-231">**single object JSON example**</span></span>

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        ```

    * <span data-ttu-id="93bde-232">**Пример JSON-файла с разделителем-строкой**</span><span class="sxs-lookup"><span data-stu-id="93bde-232">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="93bde-233">**Пример объединенного JSON-файла**</span><span class="sxs-lookup"><span data-stu-id="93bde-233">**concatenated JSON example**</span></span>

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        }
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
        ```

- <span data-ttu-id="93bde-234">**Тип 2: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="93bde-234">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="93bde-235">Каждый файл содержит массив объектов.</span><span class="sxs-lookup"><span data-stu-id="93bde-235">Each file contains an array of objects.</span></span>

    ```json
    [
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        },
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        },
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
    ]
    ```

### <a name="jsonformat-example"></a><span data-ttu-id="93bde-236">Пример JsonFormat</span><span class="sxs-lookup"><span data-stu-id="93bde-236">JsonFormat example</span></span>

<span data-ttu-id="93bde-237">**Вариант 1. Копирование данных из JSON-файлов**</span><span class="sxs-lookup"><span data-stu-id="93bde-237">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="93bde-238">В разделе hello, следующие два примера при копировании данных из JSON-файлов.</span><span class="sxs-lookup"><span data-stu-id="93bde-238">See hello following two samples when copying data from JSON files.</span></span> <span data-ttu-id="93bde-239">Универсальный Hello точки toonote:</span><span class="sxs-lookup"><span data-stu-id="93bde-239">hello generic points toonote:</span></span>

<span data-ttu-id="93bde-240">**Пример 1. Извлечение данных из объекта и массива**</span><span class="sxs-lookup"><span data-stu-id="93bde-240">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="93bde-241">В этом примере предполагается, что один корневой объект JSON, отображающий toosingle записи в табличный результат.</span><span class="sxs-lookup"><span data-stu-id="93bde-241">In this sample, you expect one root JSON object maps toosingle record in tabular result.</span></span> <span data-ttu-id="93bde-242">Если имеется файл JSON с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="93bde-242">If you have a JSON file with hello following content:</span></span>  

```json
{
    "id": "ed0e4960-d9c5-11e6-85dc-d7996816aad3",
    "context": {
        "device": {
            "type": "PC"
        },
        "custom": {
            "dimensions": [
                {
                    "TargetResourceType": "Microsoft.Compute/virtualMachines"
                },
                {
                    "ResourceManagmentProcessRunId": "827f8aaa-ab72-437c-ba48-d8917a7336a3"
                },
                {
                    "OccurrenceTime": "1/13/2017 11:24:37 AM"
                }
            ]
        }
    }
}
```
<span data-ttu-id="93bde-243">и необходимо отформатировать его в таблице Azure SQL в следующих hello, путем извлечения данных из объектов и массив toocopy:</span><span class="sxs-lookup"><span data-stu-id="93bde-243">and you want toocopy it into an Azure SQL table in hello following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="93bde-244">id</span><span class="sxs-lookup"><span data-stu-id="93bde-244">id</span></span> | <span data-ttu-id="93bde-245">deviceType</span><span class="sxs-lookup"><span data-stu-id="93bde-245">deviceType</span></span> | <span data-ttu-id="93bde-246">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="93bde-246">targetResourceType</span></span> | <span data-ttu-id="93bde-247">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="93bde-247">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="93bde-248">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="93bde-248">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="93bde-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="93bde-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="93bde-250">PC</span><span class="sxs-lookup"><span data-stu-id="93bde-250">PC</span></span> | <span data-ttu-id="93bde-251">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="93bde-251">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="93bde-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="93bde-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="93bde-253">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="93bde-253">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="93bde-254">Hello входного набора данных с **JsonFormat** тип определяется следующим образом: (частичное определение с частями hello применимо).</span><span class="sxs-lookup"><span data-stu-id="93bde-254">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="93bde-255">В частности:</span><span class="sxs-lookup"><span data-stu-id="93bde-255">More specifically:</span></span>

- <span data-ttu-id="93bde-256">`structure`раздел определяет имена столбцов настроенные hello и hello соответствующие типы данных во время преобразования данных tootabular.</span><span class="sxs-lookup"><span data-stu-id="93bde-256">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="93bde-257">Этот раздел представляет **необязательно** при отсутствии необходимости toodo сопоставления столбцов.</span><span class="sxs-lookup"><span data-stu-id="93bde-257">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="93bde-258">В разделе [сопоставление столбцов набора данных toodestination столбцов набора данных источника](data-factory-map-columns.md) более подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="93bde-258">See [Map source dataset columns toodestination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="93bde-259">`jsonPathDefinition`Указывает путь hello JSON для каждого столбца, указывающее, где tooextract hello данные из.</span><span class="sxs-lookup"><span data-stu-id="93bde-259">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="93bde-260">toocopy данные из массива, можно использовать **.property массива [x]** tooextract значение hello заданного свойства из объекта xth hello, или же можно использовать  **массива [*] .property** toofind значение Hello из любого объекта, содержащего такого свойства.</span><span class="sxs-lookup"><span data-stu-id="93bde-260">toocopy data from array, you can use **array[x].property** tooextract value of hello given property from hello xth object, or you can use **array[*].property** toofind hello value from any object containing such property.</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "deviceType",
            "type": "String"
        },
        {
            "name": "targetResourceType",
            "type": "String"
        },
        {
            "name": "resourceManagmentProcessRunId",
            "type": "String"
        },
        {
            "name": "occurrenceTime",
            "type": "DateTime"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonPathDefinition": {"id": "$.id", "deviceType": "$.context.device.type", "targetResourceType": "$.context.custom.dimensions[0].TargetResourceType", "resourceManagmentProcessRunId": "$.context.custom.dimensions[1].ResourceManagmentProcessRunId", "occurrenceTime": " $.context.custom.dimensions[2].OccurrenceTime"}      
        }
    }
}
```

<span data-ttu-id="93bde-261">**Пример 2: кросс-примените несколько объектов с hello же шаблон из массива**</span><span class="sxs-lookup"><span data-stu-id="93bde-261">**Sample 2: cross apply multiple objects with hello same pattern from array**</span></span>

<span data-ttu-id="93bde-262">В этом примере предполагается, что tootransform один корневой объект JSON в несколько записей в табличный результат.</span><span class="sxs-lookup"><span data-stu-id="93bde-262">In this sample, you expect tootransform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="93bde-263">Если имеется файл JSON с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="93bde-263">If you have a JSON file with hello following content:</span></span>  

```json
{
    "ordernumber": "01",
    "orderdate": "20170122",
    "orderlines": [
        {
            "prod": "p1",
            "price": 23
        },
        {
            "prod": "p2",
            "price": 13
        },
        {
            "prod": "p3",
            "price": 231
        }
    ],
    "city": [ { "sanmateo": "No 1" } ]
}
```
<span data-ttu-id="93bde-264">и отформатируйте его в таблице Azure SQL в следующих hello, выравнивание данных hello внутри массива hello toocopy перекрестное соединение с hello, общие сведения о корневой:</span><span class="sxs-lookup"><span data-stu-id="93bde-264">and you want toocopy it into an Azure SQL table in hello following format, by flattening hello data inside hello array and cross join with hello common root info:</span></span>

| <span data-ttu-id="93bde-265">ordernumber</span><span class="sxs-lookup"><span data-stu-id="93bde-265">ordernumber</span></span> | <span data-ttu-id="93bde-266">orderdate</span><span class="sxs-lookup"><span data-stu-id="93bde-266">orderdate</span></span> | <span data-ttu-id="93bde-267">order_pd</span><span class="sxs-lookup"><span data-stu-id="93bde-267">order_pd</span></span> | <span data-ttu-id="93bde-268">order_price</span><span class="sxs-lookup"><span data-stu-id="93bde-268">order_price</span></span> | <span data-ttu-id="93bde-269">city</span><span class="sxs-lookup"><span data-stu-id="93bde-269">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="93bde-270">01</span><span class="sxs-lookup"><span data-stu-id="93bde-270">01</span></span> | <span data-ttu-id="93bde-271">20170122</span><span class="sxs-lookup"><span data-stu-id="93bde-271">20170122</span></span> | <span data-ttu-id="93bde-272">P1</span><span class="sxs-lookup"><span data-stu-id="93bde-272">P1</span></span> | <span data-ttu-id="93bde-273">23</span><span class="sxs-lookup"><span data-stu-id="93bde-273">23</span></span> | <span data-ttu-id="93bde-274">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="93bde-274">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="93bde-275">01</span><span class="sxs-lookup"><span data-stu-id="93bde-275">01</span></span> | <span data-ttu-id="93bde-276">20170122</span><span class="sxs-lookup"><span data-stu-id="93bde-276">20170122</span></span> | <span data-ttu-id="93bde-277">P2</span><span class="sxs-lookup"><span data-stu-id="93bde-277">P2</span></span> | <span data-ttu-id="93bde-278">13.</span><span class="sxs-lookup"><span data-stu-id="93bde-278">13</span></span> | <span data-ttu-id="93bde-279">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="93bde-279">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="93bde-280">01</span><span class="sxs-lookup"><span data-stu-id="93bde-280">01</span></span> | <span data-ttu-id="93bde-281">20170122</span><span class="sxs-lookup"><span data-stu-id="93bde-281">20170122</span></span> | <span data-ttu-id="93bde-282">P3</span><span class="sxs-lookup"><span data-stu-id="93bde-282">P3</span></span> | <span data-ttu-id="93bde-283">231</span><span class="sxs-lookup"><span data-stu-id="93bde-283">231</span></span> | <span data-ttu-id="93bde-284">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="93bde-284">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="93bde-285">Hello входного набора данных с **JsonFormat** тип определяется следующим образом: (частичное определение с частями hello применимо).</span><span class="sxs-lookup"><span data-stu-id="93bde-285">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="93bde-286">В частности:</span><span class="sxs-lookup"><span data-stu-id="93bde-286">More specifically:</span></span>

- <span data-ttu-id="93bde-287">`structure`раздел определяет имена столбцов настроенные hello и hello соответствующие типы данных во время преобразования данных tootabular.</span><span class="sxs-lookup"><span data-stu-id="93bde-287">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="93bde-288">Этот раздел представляет **необязательно** при отсутствии необходимости toodo сопоставления столбцов.</span><span class="sxs-lookup"><span data-stu-id="93bde-288">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="93bde-289">В разделе [сопоставление столбцов набора данных toodestination столбцов набора данных источника](data-factory-map-columns.md) более подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="93bde-289">See [Map source dataset columns toodestination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="93bde-290">`jsonNodeReference`Указывает tooiterate и извлечения данных из объектов hello с hello же шаблон в списке **массива** orderlines.</span><span class="sxs-lookup"><span data-stu-id="93bde-290">`jsonNodeReference` indicates tooiterate and extract data from hello objects with hello same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="93bde-291">`jsonPathDefinition`Указывает путь hello JSON для каждого столбца, указывающее, где tooextract hello данные из.</span><span class="sxs-lookup"><span data-stu-id="93bde-291">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="93bde-292">В этом примере «ordernumber», «orderdate» и «Город» находятся в корневой объект пути JSON, начиная с «$»., хотя «order_pd» и «order_price» определяются с путем, производный от элемента массива hello без «$»..</span><span class="sxs-lookup"><span data-stu-id="93bde-292">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from hello array element without "$.".</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "ordernumber",
            "type": "String"
        },
        {
            "name": "orderdate",
            "type": "String"
        },
        {
            "name": "order_pd",
            "type": "String"
        },
        {
            "name": "order_price",
            "type": "Int64"
        },
        {
            "name": "city",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonNodeReference": "$.orderlines",
            "jsonPathDefinition": {"ordernumber": "$.ordernumber", "orderdate": "$.orderdate", "order_pd": "prod", "order_price": "price", "city": " $.city"}         
        }
    }
}
```

<span data-ttu-id="93bde-293">**Обратите внимание hello после точки.**</span><span class="sxs-lookup"><span data-stu-id="93bde-293">**Note hello following points:**</span></span>

* <span data-ttu-id="93bde-294">Если hello `structure` и `jsonPathDefinition` не определены в наборе данных фабрики данных hello hello действие копирования обнаруживает hello схемы из первого объекта hello и одноуровневые hello объекта целиком.</span><span class="sxs-lookup"><span data-stu-id="93bde-294">If hello `structure` and `jsonPathDefinition` are not defined in hello Data Factory dataset, hello Copy Activity detects hello schema from hello first object and flatten hello whole object.</span></span>
* <span data-ttu-id="93bde-295">По умолчанию Если входные данные JSON hello массив, hello действие копирования преобразует весь массив значение hello в строку.</span><span class="sxs-lookup"><span data-stu-id="93bde-295">If hello JSON input has an array, by default hello Copy Activity converts hello entire array value into a string.</span></span> <span data-ttu-id="93bde-296">Для выбора tooextract данных с помощью `jsonNodeReference` и/или `jsonPathDefinition`, или пропустить его, не указывайте его в `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="93bde-296">You can choose tooextract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="93bde-297">При наличии дубликатов имен в Здравствуйте того же уровня, hello действие копирования выбирает hello последним.</span><span class="sxs-lookup"><span data-stu-id="93bde-297">If there are duplicate names at hello same level, hello Copy Activity picks hello last one.</span></span>
* <span data-ttu-id="93bde-298">В именах свойств учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="93bde-298">Property names are case-sensitive.</span></span> <span data-ttu-id="93bde-299">Два свойства с одинаковым именем, но в разных регистрах, рассматриваются как два отдельных свойства.</span><span class="sxs-lookup"><span data-stu-id="93bde-299">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="93bde-300">**Вариант 2: Запись файла tooJSON данных**</span><span class="sxs-lookup"><span data-stu-id="93bde-300">**Case 2: Writing data tooJSON file**</span></span>

<span data-ttu-id="93bde-301">Если у вас есть hello в следующей таблице в базе данных SQL:</span><span class="sxs-lookup"><span data-stu-id="93bde-301">If you have hello following table in SQL Database:</span></span>

| <span data-ttu-id="93bde-302">id</span><span class="sxs-lookup"><span data-stu-id="93bde-302">id</span></span> | <span data-ttu-id="93bde-303">order_date</span><span class="sxs-lookup"><span data-stu-id="93bde-303">order_date</span></span> | <span data-ttu-id="93bde-304">order_price</span><span class="sxs-lookup"><span data-stu-id="93bde-304">order_price</span></span> | <span data-ttu-id="93bde-305">order_by</span><span class="sxs-lookup"><span data-stu-id="93bde-305">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="93bde-306">1</span><span class="sxs-lookup"><span data-stu-id="93bde-306">1</span></span> | <span data-ttu-id="93bde-307">20170119</span><span class="sxs-lookup"><span data-stu-id="93bde-307">20170119</span></span> | <span data-ttu-id="93bde-308">2000</span><span class="sxs-lookup"><span data-stu-id="93bde-308">2000</span></span> | <span data-ttu-id="93bde-309">David</span><span class="sxs-lookup"><span data-stu-id="93bde-309">David</span></span> |
| <span data-ttu-id="93bde-310">2</span><span class="sxs-lookup"><span data-stu-id="93bde-310">2</span></span> | <span data-ttu-id="93bde-311">20170120</span><span class="sxs-lookup"><span data-stu-id="93bde-311">20170120</span></span> | <span data-ttu-id="93bde-312">3500</span><span class="sxs-lookup"><span data-stu-id="93bde-312">3500</span></span> | <span data-ttu-id="93bde-313">Patrick</span><span class="sxs-lookup"><span data-stu-id="93bde-313">Patrick</span></span> |
| <span data-ttu-id="93bde-314">3</span><span class="sxs-lookup"><span data-stu-id="93bde-314">3</span></span> | <span data-ttu-id="93bde-315">20170121</span><span class="sxs-lookup"><span data-stu-id="93bde-315">20170121</span></span> | <span data-ttu-id="93bde-316">4000</span><span class="sxs-lookup"><span data-stu-id="93bde-316">4000</span></span> | <span data-ttu-id="93bde-317">Jason</span><span class="sxs-lookup"><span data-stu-id="93bde-317">Jason</span></span> |

<span data-ttu-id="93bde-318">и для каждой записи, ожидается, что объект JSON tooa toowrite hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="93bde-318">and for each record, you expect toowrite tooa JSON object in hello following format:</span></span>
```json
{
    "id": "1",
    "order": {
        "date": "20170119",
        "price": 2000,
        "customer": "David"
    }
}
```

<span data-ttu-id="93bde-319">Hello выходной набор данных с **JsonFormat** тип определяется следующим образом: (частичное определение с частями hello применимо).</span><span class="sxs-lookup"><span data-stu-id="93bde-319">hello output dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="93bde-320">В частности `structure` раздел определяет имена свойств настроенные hello в конечный файл `nestingSeparator` (по умолчанию — «.»), уровень вложенности hello используется tooidentify из имени hello.</span><span class="sxs-lookup"><span data-stu-id="93bde-320">More specifically, `structure` section defines hello customized property names in destination file, `nestingSeparator` (default is ".") are used tooidentify hello nest layer from hello name.</span></span> <span data-ttu-id="93bde-321">Этот раздел представляет **необязательно** , если не требуется имя свойства toochange hello, сравнение с именем столбца источника или вложить некоторые свойства hello.</span><span class="sxs-lookup"><span data-stu-id="93bde-321">This section is **optional** unless you want toochange hello property name comparing with source column name, or nest some of hello properties.</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "order.date",
            "type": "String"
        },
        {
            "name": "order.price",
            "type": "Int64"
        },
        {
            "name": "order.customer",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat"
        }
    }
}
```

## <a name="avro-format"></a><span data-ttu-id="93bde-322">Формат Avro</span><span class="sxs-lookup"><span data-stu-id="93bde-322">AVRO format</span></span>
<span data-ttu-id="93bde-323">Если требуется tooparse hello Avro файлы или записи данных hello в формате Avro, задайте hello `format` `type` свойство слишком**AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="93bde-323">If you want tooparse hello Avro files or write hello data in Avro format, set hello `format` `type` property too**AvroFormat**.</span></span> <span data-ttu-id="93bde-324">Необязательно toospecify любые свойства в раздел формата hello внутри раздела typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="93bde-324">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="93bde-325">Пример:</span><span class="sxs-lookup"><span data-stu-id="93bde-325">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="93bde-326">toouse в формате Avro в таблицу Hive можно ссылаться слишком[Apache Hive учебника](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="93bde-326">toouse Avro format in a Hive table, you can refer too[Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="93bde-327">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="93bde-327">Note hello following points:</span></span>  

* <span data-ttu-id="93bde-328">[Сложные типы данных](http://avro.apache.org/docs/current/spec.html#schema_complex) (записи, перечисления, массивы, сопоставления, объединения и фиксированные данные) не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="93bde-328">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions, and fixed).</span></span>

## <a name="orc-format"></a><span data-ttu-id="93bde-329">Формат ORC</span><span class="sxs-lookup"><span data-stu-id="93bde-329">ORC format</span></span>
<span data-ttu-id="93bde-330">Если требуется tooparse hello ORC файлы или записи данных hello в формат ORC, задайте hello `format` `type` свойство слишком**OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="93bde-330">If you want tooparse hello ORC files or write hello data in ORC format, set hello `format` `type` property too**OrcFormat**.</span></span> <span data-ttu-id="93bde-331">Необязательно toospecify любые свойства в раздел формата hello внутри раздела typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="93bde-331">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="93bde-332">Пример:</span><span class="sxs-lookup"><span data-stu-id="93bde-332">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="93bde-333">При копировании файлов ORC не **как-является** между локальными и облачными хранилищами данных, необходимо tooinstall hello JRE 8 (среда выполнения Java) на компьютере шлюза.</span><span class="sxs-lookup"><span data-stu-id="93bde-333">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="93bde-334">Для 64-разрядного шлюза требуется 64-разрядная версия JRE, а для 32-разрядного шлюза — 32-разрядная версия JRE.</span><span class="sxs-lookup"><span data-stu-id="93bde-334">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="93bde-335">Обе эти версии доступны [здесь](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="93bde-335">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="93bde-336">Выберите подходящее hello.</span><span class="sxs-lookup"><span data-stu-id="93bde-336">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="93bde-337">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="93bde-337">Note hello following points:</span></span>

* <span data-ttu-id="93bde-338">Данные сложных типов (STRUCT, MAP, LIST, UNION) не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="93bde-338">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="93bde-339">Для ORC-файлов используется три [параметра сжатия](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB и SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="93bde-339">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="93bde-340">Фабрика данных поддерживает чтение данных из ORC-файла в любом из этих форматов.</span><span class="sxs-lookup"><span data-stu-id="93bde-340">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="93bde-341">Она использует сжатие hello кодек находится в данных hello tooread hello метаданных.</span><span class="sxs-lookup"><span data-stu-id="93bde-341">It uses hello compression codec is in hello metadata tooread hello data.</span></span> <span data-ttu-id="93bde-342">Однако при записи файла ORC tooan, фабрики данных выбирает ZLIB, который является по умолчанию hello для ORC.</span><span class="sxs-lookup"><span data-stu-id="93bde-342">However, when writing tooan ORC file, Data Factory chooses ZLIB, which is hello default for ORC.</span></span> <span data-ttu-id="93bde-343">В настоящее время нет отсутствует параметр toooverride это поведение.</span><span class="sxs-lookup"><span data-stu-id="93bde-343">Currently, there is no option toooverride this behavior.</span></span>

## <a name="parquet-format"></a><span data-ttu-id="93bde-344">Формат Parquet</span><span class="sxs-lookup"><span data-stu-id="93bde-344">Parquet format</span></span>
<span data-ttu-id="93bde-345">Если требуется tooparse hello Parquet файлы или записи данных hello в формате Parquet, задайте hello `format` `type` свойство слишком**ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="93bde-345">If you want tooparse hello Parquet files or write hello data in Parquet format, set hello `format` `type` property too**ParquetFormat**.</span></span> <span data-ttu-id="93bde-346">Необязательно toospecify любые свойства в раздел формата hello внутри раздела typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="93bde-346">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="93bde-347">Пример:</span><span class="sxs-lookup"><span data-stu-id="93bde-347">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="93bde-348">При копировании файлов Parquet не **как-является** между локальными и облачными хранилищами данных, необходимо tooinstall hello JRE 8 (среда выполнения Java) на компьютере шлюза.</span><span class="sxs-lookup"><span data-stu-id="93bde-348">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="93bde-349">Для 64-разрядного шлюза требуется 64-разрядная версия JRE, а для 32-разрядного шлюза — 32-разрядная версия JRE.</span><span class="sxs-lookup"><span data-stu-id="93bde-349">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="93bde-350">Обе эти версии доступны [здесь](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="93bde-350">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="93bde-351">Выберите подходящее hello.</span><span class="sxs-lookup"><span data-stu-id="93bde-351">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="93bde-352">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="93bde-352">Note hello following points:</span></span>

* <span data-ttu-id="93bde-353">Данные сложных типов (MAP, LIST) не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="93bde-353">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="93bde-354">Файл parquet имеет следующие параметры, связанные с сжатия hello: NONE, SNAPPY, GZIP и LZO.</span><span class="sxs-lookup"><span data-stu-id="93bde-354">Parquet file has hello following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="93bde-355">Фабрика данных поддерживает чтение данных из ORC-файла в любом из этих форматов.</span><span class="sxs-lookup"><span data-stu-id="93bde-355">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="93bde-356">Он использует кодек сжатия hello в данных hello tooread hello метаданных.</span><span class="sxs-lookup"><span data-stu-id="93bde-356">It uses hello compression codec in hello metadata tooread hello data.</span></span> <span data-ttu-id="93bde-357">Однако при записи файла Parquet tooa, фабрики данных выбирает SNAPPY, что является по умолчанию hello для формата Parquet.</span><span class="sxs-lookup"><span data-stu-id="93bde-357">However, when writing tooa Parquet file, Data Factory chooses SNAPPY, which is hello default for Parquet format.</span></span> <span data-ttu-id="93bde-358">В настоящее время нет отсутствует параметр toooverride это поведение.</span><span class="sxs-lookup"><span data-stu-id="93bde-358">Currently, there is no option toooverride this behavior.</span></span>

## <a name="compression-support"></a><span data-ttu-id="93bde-359">Поддержка сжатия</span><span class="sxs-lookup"><span data-stu-id="93bde-359">Compression support</span></span>
<span data-ttu-id="93bde-360">Обработка больших наборов данных может привести к возникновению узких мест ввода-вывода и сети.</span><span class="sxs-lookup"><span data-stu-id="93bde-360">Processing large data sets can cause I/O and network bottlenecks.</span></span> <span data-ttu-id="93bde-361">Таким образом, сжатых данных в хранилищах можно не только ускорения передачи данных по сети hello и сэкономить место на диске, но также перевести значительное повышение производительности при обработке больших данных.</span><span class="sxs-lookup"><span data-stu-id="93bde-361">Therefore, compressed data in stores can not only speed up data transfer across hello network and save disk space, but also bring significant performance improvements in processing big data.</span></span> <span data-ttu-id="93bde-362">Сейчас сжатие поддерживается для файловых хранилищ данных, таких как хранилище BLOB-объектов Azure или локальная файловая система.</span><span class="sxs-lookup"><span data-stu-id="93bde-362">Currently, compression is supported for file-based data stores such as Azure Blob or On-premises File System.</span></span>  

<span data-ttu-id="93bde-363">Сжатие toospecify для набора данных, используйте hello **сжатия** свойство в наборе данных hello JSON и hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="93bde-363">toospecify compression for a dataset, use hello **compression** property in hello dataset JSON as in hello following example:</span></span>   

```json
{  
    "name": "AzureBlobDataSet",  
    "properties": {  
        "availability": {  
            "frequency": "Day",  
              "interval": 1  
        },  
        "type": "AzureBlob",  
        "linkedServiceName": "StorageLinkedService",  
        "typeProperties": {  
            "fileName": "pagecounts.csv.gz",  
            "folderPath": "compression/file/",  
            "compression": {  
                "type": "GZip",  
                "level": "Optimal"  
            }  
        }  
    }  
}  
```

<span data-ttu-id="93bde-364">Предположим, что образец hello набора данных используется как hello выходные данные операции копирования, hello сжимает действия копирования hello выходных данных с помощью оптимальное соотношение кодека GZIP, а затем написать hello сжатых данных в файл с именем pagecounts.csv.gz в hello хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="93bde-364">Suppose hello sample dataset is used as hello output of a copy activity, hello copy activity compresses hello output data with GZIP codec using optimal ratio and then write hello compressed data into a file named pagecounts.csv.gz in hello Azure Blob Storage.</span></span>

> [!NOTE]
> <span data-ttu-id="93bde-365">Параметры сжатия не поддерживаются для данных в hello **AvroFormat**, **OrcFormat**, или **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="93bde-365">Compression settings are not supported for data in hello **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span></span> <span data-ttu-id="93bde-366">При чтении файлов в этих форматах, фабрики данных определяет и использует кодек сжатия hello в метаданных hello.</span><span class="sxs-lookup"><span data-stu-id="93bde-366">When reading files in these formats, Data Factory detects and uses hello compression codec in hello metadata.</span></span> <span data-ttu-id="93bde-367">При написании toofiles в этих форматах, фабрики данных выбирает hello кодек сжатия по умолчанию для этого формата.</span><span class="sxs-lookup"><span data-stu-id="93bde-367">When writing toofiles in these formats, Data Factory chooses hello default compression codec for that format.</span></span> <span data-ttu-id="93bde-368">Например, ZLIB для OrcFormat и SNAPPY для ParquetFormat.</span><span class="sxs-lookup"><span data-stu-id="93bde-368">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span></span>   

<span data-ttu-id="93bde-369">Hello **сжатия** раздел имеет два свойства:</span><span class="sxs-lookup"><span data-stu-id="93bde-369">hello **compression** section has two properties:</span></span>  

* <span data-ttu-id="93bde-370">**Тип:** hello сжатия кодека, который может быть **GZIP**, **Deflate**, **BZIP2**, или **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="93bde-370">**Type:** hello compression codec, which can be **GZIP**, **Deflate**, **BZIP2**, or **ZipDeflate**.</span></span>  
* <span data-ttu-id="93bde-371">**Уровень:** hello степени сжатия, который может быть **оптимальный** или **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="93bde-371">**Level:** hello compression ratio, which can be **Optimal** or **Fastest**.</span></span>

  * <span data-ttu-id="93bde-372">**Самый быстрый:** операция сжатия hello следует выполнить как можно скорее, даже если hello получившийся файл оптимально не сжимаются.</span><span class="sxs-lookup"><span data-stu-id="93bde-372">**Fastest:** hello compression operation should complete as quickly as possible, even if hello resulting file is not optimally compressed.</span></span>
  * <span data-ttu-id="93bde-373">**Оптимальное**: операция сжатия hello оптимального сжатия, даже если hello занимает больше времени, toocomplete время.</span><span class="sxs-lookup"><span data-stu-id="93bde-373">**Optimal**: hello compression operation should be optimally compressed, even if hello operation takes a longer time toocomplete.</span></span>

    <span data-ttu-id="93bde-374">Дополнительные сведения см. в разделе [Уровень сжатия](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx).</span><span class="sxs-lookup"><span data-stu-id="93bde-374">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span></span>

<span data-ttu-id="93bde-375">При указании `compression` свойства во входном наборе данных JSON конвейера hello можно считывать сжатые данные из источника hello; и при указании свойства hello в выходной набор данных JSON действие hello копирования можно написать назначения toohello сжатых данных.</span><span class="sxs-lookup"><span data-stu-id="93bde-375">When you specify `compression` property in an input dataset JSON, hello pipeline can read compressed data from hello source; and when you specify hello property in an output dataset JSON, hello copy activity can write compressed data toohello destination.</span></span> <span data-ttu-id="93bde-376">Ниже приведено несколько примеров сценариев:</span><span class="sxs-lookup"><span data-stu-id="93bde-376">Here are a few sample scenarios:</span></span>

* <span data-ttu-id="93bde-377">Прочитать GZIP сжатые данные из большого двоичного объекта Azure, распакуйте его и записи базы данных Azure SQL tooan данных результатов.</span><span class="sxs-lookup"><span data-stu-id="93bde-377">Read GZIP compressed data from an Azure blob, decompress it, and write result data tooan Azure SQL database.</span></span> <span data-ttu-id="93bde-378">Определение hello входного набора данных больших двоичных объектов Azure с hello `compression` `type` свойство JSON как GZIP.</span><span class="sxs-lookup"><span data-stu-id="93bde-378">You define hello input Azure Blob dataset with hello `compression` `type` JSON property as GZIP.</span></span>
* <span data-ttu-id="93bde-379">Чтение данных из текстового файла в локальной файловой системе, сжать формате GZip и записи tooan hello сжатых данных BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="93bde-379">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write hello compressed data tooan Azure blob.</span></span> <span data-ttu-id="93bde-380">Определите выходной набор данных BLOB-объектов Azure с hello `compression` `type` свойство JSON как GZip.</span><span class="sxs-lookup"><span data-stu-id="93bde-380">You define an output Azure Blob dataset with hello `compression` `type` JSON property as GZip.</span></span>
* <span data-ttu-id="93bde-381">Чтение ZIP-файл с FTP-сервера, распаковать его файлы hello tooget внутри и перемещаться эти файлы в хранилище Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="93bde-381">Read .zip file from FTP server, decompress it tooget hello files inside, and land those files into Azure Data Lake Store.</span></span> <span data-ttu-id="93bde-382">Определение входного набора данных FTP с hello `compression` `type` свойства JSON в виде ZipDeflate.</span><span class="sxs-lookup"><span data-stu-id="93bde-382">You define an input FTP dataset with hello `compression` `type` JSON property as ZipDeflate.</span></span>
* <span data-ttu-id="93bde-383">Считывать данные, сжатые GZIP из большого двоичного объекта Azure, распакуйте его, сжатие с помощью BZIP2 и записи tooan результат данных BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="93bde-383">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data tooan Azure blob.</span></span> <span data-ttu-id="93bde-384">Определение hello входного набора данных больших двоичных объектов Azure с `compression` `type` задать tooGZIP и hello выходной набор данных с `compression` `type` в этом случае задайте tooBZIP2.</span><span class="sxs-lookup"><span data-stu-id="93bde-384">You define hello input Azure Blob dataset with `compression` `type` set tooGZIP and hello output dataset with `compression` `type` set tooBZIP2 in this case.</span></span>   


## <a name="next-steps"></a><span data-ttu-id="93bde-385">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="93bde-385">Next steps</span></span>
<span data-ttu-id="93bde-386">См. следующие статьи для хранилищ данных на основе файла, поддерживаемые фабрикой данных Azure hello.</span><span class="sxs-lookup"><span data-stu-id="93bde-386">See hello following articles for file-based data stores supported by Azure Data Factory:</span></span>

- [<span data-ttu-id="93bde-387">Хранилище BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="93bde-387">Azure Blob Storage</span></span>](data-factory-azure-blob-connector.md)
- [<span data-ttu-id="93bde-388">Хранилище озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="93bde-388">Azure Data Lake Store</span></span>](data-factory-azure-datalake-connector.md)
- [<span data-ttu-id="93bde-389">FTP</span><span class="sxs-lookup"><span data-stu-id="93bde-389">FTP</span></span>](data-factory-ftp-connector.md)
- [<span data-ttu-id="93bde-390">HDFS</span><span class="sxs-lookup"><span data-stu-id="93bde-390">HDFS</span></span>](data-factory-hdfs-connector.md)
- [<span data-ttu-id="93bde-391">Перемещение данных в локальную файловую систему или из нее с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="93bde-391">File System</span></span>](data-factory-onprem-file-system-connector.md)
- [<span data-ttu-id="93bde-392">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="93bde-392">Amazon S3</span></span>](data-factory-amazon-simple-storage-service-connector.md)
