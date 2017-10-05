---
title: "Форматы файлов и сжатия данных в фабрике данных Azure | Документация Майкрософт"
description: "Сведения о форматах файлов, поддерживаемых фабрикой данных Azure."
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
ms.openlocfilehash: f4746e0dd249e417b8077a9bc733d2886daafdf2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a><span data-ttu-id="bc7dc-104">Форматы файлов и сжатия данных, поддерживаемые фабрикой данных Azure</span><span class="sxs-lookup"><span data-stu-id="bc7dc-104">File and compression formats supported by Azure Data Factory</span></span>
<span data-ttu-id="bc7dc-105">*Этот раздел относится к соединителям для следующих компонентов: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [большой двоичный объект Azure](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [файловая система](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md) и [SFTP](data-factory-sftp-connector.md).*</span><span class="sxs-lookup"><span data-stu-id="bc7dc-105">*This topic applies to the following connectors: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [File System](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), and [SFTP](data-factory-sftp-connector.md).*</span></span>

<span data-ttu-id="bc7dc-106">Фабрика данных Azure поддерживает следующие форматы файлов:</span><span class="sxs-lookup"><span data-stu-id="bc7dc-106">Azure Data Factory supports the following file format types:</span></span>

* <span data-ttu-id="bc7dc-107">[текстовый формат](#text-format);</span><span class="sxs-lookup"><span data-stu-id="bc7dc-107">[Text format](#text-format)</span></span>
* <span data-ttu-id="bc7dc-108">[формат JSON](#json-format);</span><span class="sxs-lookup"><span data-stu-id="bc7dc-108">[JSON format](#json-format)</span></span>
* <span data-ttu-id="bc7dc-109">[формат Avro](#avro-format);</span><span class="sxs-lookup"><span data-stu-id="bc7dc-109">[Avro format](#avro-format)</span></span>
* <span data-ttu-id="bc7dc-110">[формат ORC](#orc-format);</span><span class="sxs-lookup"><span data-stu-id="bc7dc-110">[ORC format](#orc-format)</span></span>
* <span data-ttu-id="bc7dc-111">[формат Parquet](#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-111">[Parquet format](#parquet-format)</span></span>

## <a name="text-format"></a><span data-ttu-id="bc7dc-112">Текстовый формат</span><span class="sxs-lookup"><span data-stu-id="bc7dc-112">Text format</span></span>
<span data-ttu-id="bc7dc-113">Если вам нужно считать данные из текстового файла или записать в него данные, задайте для свойства `type` в разделе `format` набора данных значение **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-113">If you want to read from a text file or write to a text file, set the `type` property in the `format` section of the dataset to **TextFormat**.</span></span> <span data-ttu-id="bc7dc-114">В разделе `format` также можно указать следующие **необязательные** свойства.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-114">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="bc7dc-115">Инструкции по настройке см. в разделе [Пример TextFormat](#textformat-example).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-115">See [TextFormat example](#textformat-example) section on how to configure.</span></span>

| <span data-ttu-id="bc7dc-116">Свойство</span><span class="sxs-lookup"><span data-stu-id="bc7dc-116">Property</span></span> | <span data-ttu-id="bc7dc-117">Описание</span><span class="sxs-lookup"><span data-stu-id="bc7dc-117">Description</span></span> | <span data-ttu-id="bc7dc-118">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="bc7dc-118">Allowed values</span></span> | <span data-ttu-id="bc7dc-119">Обязательно</span><span class="sxs-lookup"><span data-stu-id="bc7dc-119">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bc7dc-120">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="bc7dc-120">columnDelimiter</span></span> |<span data-ttu-id="bc7dc-121">Знак, используемый для разделения столбцов в файле.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-121">The character used to separate columns in a file.</span></span> <span data-ttu-id="bc7dc-122">Вы можете использовать редкие непечатаемые символы, которые, скорее всего, не содержатся в ваших данных.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-122">You can consider to use a rare unprintable char that may not likely exists in your data.</span></span> <span data-ttu-id="bc7dc-123">Например, укажите "\u0001", что соответствует символу начала заголовка (SOH).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-123">For example, specify "\u0001", which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="bc7dc-124">Допускается только один знак.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-124">Only one character is allowed.</span></span> <span data-ttu-id="bc7dc-125">Значение **по умолчанию** — **запятая (,)**.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-125">The **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="bc7dc-126">Чтобы использовать символ Юникода, см. соответствующие коды в статье о [символах Юникода](https://en.wikipedia.org/wiki/List_of_Unicode_characters).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-126">To use a Unicode character, refer to [Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) to get the corresponding code for it.</span></span> |<span data-ttu-id="bc7dc-127">Нет</span><span class="sxs-lookup"><span data-stu-id="bc7dc-127">No</span></span> |
| <span data-ttu-id="bc7dc-128">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="bc7dc-128">rowDelimiter</span></span> |<span data-ttu-id="bc7dc-129">Знак, используемый для разделения строк в файле.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-129">The character used to separate rows in a file.</span></span> |<span data-ttu-id="bc7dc-130">Допускается только один знак.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-130">Only one character is allowed.</span></span> <span data-ttu-id="bc7dc-131">**По умолчанию** используется одно из следующих значений: **для чтения — [\r\n, \r, \n]**, для записи — **\r\n**.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-131">The **default** value is any of the following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="bc7dc-132">Нет</span><span class="sxs-lookup"><span data-stu-id="bc7dc-132">No</span></span> |
| <span data-ttu-id="bc7dc-133">escapeChar</span><span class="sxs-lookup"><span data-stu-id="bc7dc-133">escapeChar</span></span> |<span data-ttu-id="bc7dc-134">Специальный знак, используемый для экранирования разделителя столбцов в содержимом входного файла.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-134">The special character used to escape a column delimiter in the content of input file.</span></span> <br/><br/><span data-ttu-id="bc7dc-135">Для таблицы нельзя указать и escapeChar, и quoteChar.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-135">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="bc7dc-136">Допускается только один знак.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-136">Only one character is allowed.</span></span> <span data-ttu-id="bc7dc-137">Значение по умолчанию отсутствует.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-137">No default value.</span></span> <br/><br/><span data-ttu-id="bc7dc-138">Например, если в качестве разделителя столбцов используется запятая (,), но этот знак встречается и в тексте (пример: "Hello, world"), то в качестве знака экранирования можно определить знак доллара ($) и использовать в исходном тексте строку "Hello$, world".</span><span class="sxs-lookup"><span data-stu-id="bc7dc-138">Example: if you have comma (',') as the column delimiter but you want to have the comma character in the text (example: "Hello, world"), you can define ‘$’ as the escape character and use string "Hello$, world" in the source.</span></span> |<span data-ttu-id="bc7dc-139">Нет</span><span class="sxs-lookup"><span data-stu-id="bc7dc-139">No</span></span> |
| <span data-ttu-id="bc7dc-140">quoteChar</span><span class="sxs-lookup"><span data-stu-id="bc7dc-140">quoteChar</span></span> |<span data-ttu-id="bc7dc-141">Знак, используемый в качестве кавычки для заключения строкового значения.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-141">The character used to quote a string value.</span></span> <span data-ttu-id="bc7dc-142">Разделители столбцов и строк внутри знаков кавычек будут рассматриваться как часть строкового значения.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-142">The column and row delimiters inside the quote characters would be treated as part of the string value.</span></span> <span data-ttu-id="bc7dc-143">Это свойство применимо к входным и выходным наборам данных.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-143">This property is applicable to both input and output datasets.</span></span><br/><br/><span data-ttu-id="bc7dc-144">Для таблицы нельзя указать и escapeChar, и quoteChar.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-144">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="bc7dc-145">Допускается только один знак.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-145">Only one character is allowed.</span></span> <span data-ttu-id="bc7dc-146">Значение по умолчанию отсутствует.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-146">No default value.</span></span> <br/><br/><span data-ttu-id="bc7dc-147">Например, если в качестве разделителя столбцов используется запятая (,) и нужно, чтобы этот знак встречался в тексте (например, <Hello, world>), то можно в качестве знака кавычек определить двойную кавычку (") и использовать в исходном тексте строку "Hello, world".</span><span class="sxs-lookup"><span data-stu-id="bc7dc-147">For example, if you have comma (',') as the column delimiter but you want to have comma character in the text (example: <Hello, world>), you can define " (double quote) as the quote character and use the string "Hello, world" in the source.</span></span> |<span data-ttu-id="bc7dc-148">Нет</span><span class="sxs-lookup"><span data-stu-id="bc7dc-148">No</span></span> |
| <span data-ttu-id="bc7dc-149">nullValue</span><span class="sxs-lookup"><span data-stu-id="bc7dc-149">nullValue</span></span> |<span data-ttu-id="bc7dc-150">Один или несколько знаков, используемых для представления значения NULL.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-150">One or more characters used to represent a null value.</span></span> |<span data-ttu-id="bc7dc-151">Один или несколько знаков.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-151">One or more characters.</span></span> <span data-ttu-id="bc7dc-152">Значения **по умолчанию**: **\N и NULL** для чтения и **\N** для записи.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-152">The **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="bc7dc-153">Нет</span><span class="sxs-lookup"><span data-stu-id="bc7dc-153">No</span></span> |
| <span data-ttu-id="bc7dc-154">encodingName</span><span class="sxs-lookup"><span data-stu-id="bc7dc-154">encodingName</span></span> |<span data-ttu-id="bc7dc-155">Имя кодировки.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-155">Specify the encoding name.</span></span> |<span data-ttu-id="bc7dc-156">Допустимое имя кодировки.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-156">A valid encoding name.</span></span> <span data-ttu-id="bc7dc-157">Ознакомьтесь с описанием свойства [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-157">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="bc7dc-158">Пример: windows-1250 или shift_jis.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-158">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="bc7dc-159">**По умолчанию** используется **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-159">The **default** value is **UTF-8**.</span></span> |<span data-ttu-id="bc7dc-160">Нет</span><span class="sxs-lookup"><span data-stu-id="bc7dc-160">No</span></span> |
| <span data-ttu-id="bc7dc-161">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="bc7dc-161">firstRowAsHeader</span></span> |<span data-ttu-id="bc7dc-162">Указывает, следует ли рассматривать первую строки в качестве заголовка.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-162">Specifies whether to consider the first row as a header.</span></span> <span data-ttu-id="bc7dc-163">Фабрика данных считывает первую строку входного набора данных как заголовок.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-163">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="bc7dc-164">Фабрика данных записывает первую строку как заголовок в выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-164">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="bc7dc-165">Примеры сценариев см. в разделе [Сценарии использования `firstRowAsHeader` и `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-165">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="bc7dc-166">Да</span><span class="sxs-lookup"><span data-stu-id="bc7dc-166">True</span></span><br/><span data-ttu-id="bc7dc-167"><b>False (по умолчанию)</b></span><span class="sxs-lookup"><span data-stu-id="bc7dc-167"><b>False (default)</b></span></span> |<span data-ttu-id="bc7dc-168">Нет</span><span class="sxs-lookup"><span data-stu-id="bc7dc-168">No</span></span> |
| <span data-ttu-id="bc7dc-169">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="bc7dc-169">skipLineCount</span></span> |<span data-ttu-id="bc7dc-170">Указывает количество строк, которые нужно пропустить при чтении данных из входных файлов.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-170">Indicates the number of rows to skip when reading data from input files.</span></span> <span data-ttu-id="bc7dc-171">Если указаны skipLineCount и firstRowAsHeader, то сначала пропускаются строки, после чего из входного файла считываются данные заголовка.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-171">If both skipLineCount and firstRowAsHeader are specified, the lines are skipped first and then the header information is read from the input file.</span></span> <br/><br/><span data-ttu-id="bc7dc-172">Примеры сценариев см. в разделе [Сценарии использования `firstRowAsHeader` и `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-172">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="bc7dc-173">Целое число </span><span class="sxs-lookup"><span data-stu-id="bc7dc-173">Integer</span></span> |<span data-ttu-id="bc7dc-174">Нет</span><span class="sxs-lookup"><span data-stu-id="bc7dc-174">No</span></span> |
| <span data-ttu-id="bc7dc-175">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="bc7dc-175">treatEmptyAsNull</span></span> |<span data-ttu-id="bc7dc-176">Указывает, следует ли интерпретировать строки со значением NULL или пустые строки как значение NULL при чтении данных из входного файла.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-176">Specifies whether to treat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="bc7dc-177">**True (по умолчанию)**</span><span class="sxs-lookup"><span data-stu-id="bc7dc-177">**True (default)**</span></span><br/><span data-ttu-id="bc7dc-178">Ложь</span><span class="sxs-lookup"><span data-stu-id="bc7dc-178">False</span></span> |<span data-ttu-id="bc7dc-179">Нет</span><span class="sxs-lookup"><span data-stu-id="bc7dc-179">No</span></span> |

### <a name="textformat-example"></a><span data-ttu-id="bc7dc-180">Пример TextFormat</span><span class="sxs-lookup"><span data-stu-id="bc7dc-180">TextFormat example</span></span>
<span data-ttu-id="bc7dc-181">В следующем определении JSON для набора данных задаются некоторые необязательные свойства.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-181">In the following JSON definition for a dataset, some of the optional properties are specified.</span></span>

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

<span data-ttu-id="bc7dc-182">Чтобы использовать `escapeChar` вместо `quoteChar`, замените строку с `quoteChar` следующим escape-символом:</span><span class="sxs-lookup"><span data-stu-id="bc7dc-182">To use an `escapeChar` instead of `quoteChar`, replace the line with `quoteChar` with the following escapeChar:</span></span>

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="bc7dc-183">Сценарии использования firstRowAsHeader и skipLineCount</span><span class="sxs-lookup"><span data-stu-id="bc7dc-183">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="bc7dc-184">Вы выполняете копирование из нефайлового источника в текстовый файл и хотите добавить строку заголовка, содержащую метаданные схемы (например, схемы SQL).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-184">You are copying from a non-file source to a text file and would like to add a header line containing the schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="bc7dc-185">В этом случае укажите `firstRowAsHeader` со значением true в выходном наборе данных.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-185">Specify `firstRowAsHeader` as true in the output dataset for this scenario.</span></span>
* <span data-ttu-id="bc7dc-186">Вы копируете данные из текстового файла, содержащего строку заголовка, в нефайловый приемник и хотите удалить эту строку.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-186">You are copying from a text file containing a header line to a non-file sink and would like to drop that line.</span></span> <span data-ttu-id="bc7dc-187">Укажите `firstRowAsHeader` со значением true во входном наборе данных.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-187">Specify `firstRowAsHeader` as true in the input dataset.</span></span>
* <span data-ttu-id="bc7dc-188">Вы копируете данные из текстового файла и хотите пропустить несколько строк в начале, которые не содержат ни данных, ни заголовка.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-188">You are copying from a text file and want to skip a few lines at the beginning that contain no data or header information.</span></span> <span data-ttu-id="bc7dc-189">Укажите `skipLineCount`, чтобы задать число пропускаемых строк.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-189">Specify `skipLineCount` to indicate the number of lines to be skipped.</span></span> <span data-ttu-id="bc7dc-190">Если остальная часть файла содержит строку заголовка, можно также указать `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-190">If the rest of the file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="bc7dc-191">Если указаны `skipLineCount` и `firstRowAsHeader`, сначала пропускаются строки, а затем из входного файла считываются данные заголовка.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-191">If both `skipLineCount` and `firstRowAsHeader` are specified, the lines are skipped first and then the header information is read from the input file</span></span>

## <a name="json-format"></a><span data-ttu-id="bc7dc-192">Формат JSON</span><span class="sxs-lookup"><span data-stu-id="bc7dc-192">JSON format</span></span>
<span data-ttu-id="bc7dc-193">Чтобы **импортировать JSON-файл "как есть" в базу данных Azure Cosmos DB или экспортировать его из нее**, см. раздел [Документы JSON для импорта и экспорта](data-factory-azure-documentdb-connector.md#importexport-json-documents) статьи о [перемещении данных в базу данных Azure Cosmos DB и из нее](data-factory-azure-documentdb-connector.md).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-193">To **import/export a JSON file as-is into/from Azure Cosmos DB**, the see [Import/export JSON documents](data-factory-azure-documentdb-connector.md#importexport-json-documents) section in [Move data to/from Azure Cosmos DB](data-factory-azure-documentdb-connector.md) article.</span></span>

<span data-ttu-id="bc7dc-194">Если требуется проанализировать JSON-файлы или записать данные в формате JSON, задайте для свойства `type` в разделе `format` значение **JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-194">If you want to parse the JSON files or write the data in JSON format, set the `type` property in the `format` section to **JsonFormat**.</span></span> <span data-ttu-id="bc7dc-195">В разделе `format` также можно указать следующие **необязательные** свойства.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-195">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="bc7dc-196">Инструкции по настройке см. в разделе [Пример JsonFormat](#jsonformat-example).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-196">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span>

| <span data-ttu-id="bc7dc-197">Свойство</span><span class="sxs-lookup"><span data-stu-id="bc7dc-197">Property</span></span> | <span data-ttu-id="bc7dc-198">Описание</span><span class="sxs-lookup"><span data-stu-id="bc7dc-198">Description</span></span> | <span data-ttu-id="bc7dc-199">Обязательно</span><span class="sxs-lookup"><span data-stu-id="bc7dc-199">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc7dc-200">filePattern</span><span class="sxs-lookup"><span data-stu-id="bc7dc-200">filePattern</span></span> |<span data-ttu-id="bc7dc-201">Шаблон данных, хранящихся в каждом JSON-файле.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-201">Indicate the pattern of data stored in each JSON file.</span></span> <span data-ttu-id="bc7dc-202">Допустимые значения: **setOfObjects** и **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-202">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="bc7dc-203">Значение **по умолчанию** — **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-203">The **default** value is **setOfObjects**.</span></span> <span data-ttu-id="bc7dc-204">Подробные сведения об этих шаблонах см. в разделе [Шаблоны файлов JSON](#json-file-patterns).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-204">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="bc7dc-205">Нет</span><span class="sxs-lookup"><span data-stu-id="bc7dc-205">No</span></span> |
| <span data-ttu-id="bc7dc-206">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="bc7dc-206">jsonNodeReference</span></span> | <span data-ttu-id="bc7dc-207">Для итерации и извлечения данных из объектов в поле массива с таким же шаблоном укажите путь JSON этого массива.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-207">If you want to iterate and extract data from the objects inside an array field with the same pattern, specify the JSON path of that array.</span></span> <span data-ttu-id="bc7dc-208">Это свойство поддерживается только в том случае, если данные копируются из JSON-файлов.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-208">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="bc7dc-209">Нет</span><span class="sxs-lookup"><span data-stu-id="bc7dc-209">No</span></span> |
| <span data-ttu-id="bc7dc-210">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="bc7dc-210">jsonPathDefinition</span></span> | <span data-ttu-id="bc7dc-211">Выражение пути JSON для каждого столбца с его сопоставлением с настраиваемым именем столбца (начало в нижнем регистре).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-211">Specify the JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="bc7dc-212">Это свойство поддерживается только в том случае, если данные копируются из JSON-файлов и данные можно извлечь из объекта или массива.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-212">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="bc7dc-213">Для полей в области корневого объекта выражение пути должно начинаться с корня $. Для полей внутри массива, выбранных с помощью свойства `jsonNodeReference`, выражение должно начинаться с элемента массива.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-213">For fields under root object, start with root $; for fields inside the array chosen by `jsonNodeReference` property, start from the array element.</span></span> <span data-ttu-id="bc7dc-214">Инструкции по настройке см. в разделе [Пример JsonFormat](#jsonformat-example).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-214">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span> | <span data-ttu-id="bc7dc-215">Нет</span><span class="sxs-lookup"><span data-stu-id="bc7dc-215">No</span></span> |
| <span data-ttu-id="bc7dc-216">encodingName</span><span class="sxs-lookup"><span data-stu-id="bc7dc-216">encodingName</span></span> |<span data-ttu-id="bc7dc-217">Имя кодировки.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-217">Specify the encoding name.</span></span> <span data-ttu-id="bc7dc-218">Список допустимых имен кодировок приведен в описании свойства [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-218">For the list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="bc7dc-219">Например: windows-1250 или shift_jis.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-219">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="bc7dc-220">**По умолчанию** используется **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-220">The **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="bc7dc-221">Нет</span><span class="sxs-lookup"><span data-stu-id="bc7dc-221">No</span></span> |
| <span data-ttu-id="bc7dc-222">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="bc7dc-222">nestingSeparator</span></span> |<span data-ttu-id="bc7dc-223">Символ, используемый для разделения уровней вложенности.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-223">Character that is used to separate nesting levels.</span></span> <span data-ttu-id="bc7dc-224">Значение по умолчанию — точка (.).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-224">The default value is '.' (dot).</span></span> |<span data-ttu-id="bc7dc-225">Нет</span><span class="sxs-lookup"><span data-stu-id="bc7dc-225">No</span></span> |

### <a name="json-file-patterns"></a><span data-ttu-id="bc7dc-226">Шаблоны файлов JSON</span><span class="sxs-lookup"><span data-stu-id="bc7dc-226">JSON file patterns</span></span>

<span data-ttu-id="bc7dc-227">Действие копирования может проанализировать следующие шаблоны JSON-файлов.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-227">Copy activity can parse the following patterns of JSON files:</span></span>

- <span data-ttu-id="bc7dc-228">**Тип 1: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="bc7dc-228">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="bc7dc-229">Каждый файл содержит один объект или несколько разделенных строками или объединенных объектов.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-229">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="bc7dc-230">Если этот параметр выбран в выходном наборе данных, то в результате копирования будет создан JSON-файл, где каждый объект будет находиться в отдельной строке (файл с разделителем-строкой).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-230">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="bc7dc-231">**Пример единого объекта JSON**</span><span class="sxs-lookup"><span data-stu-id="bc7dc-231">**single object JSON example**</span></span>

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

    * <span data-ttu-id="bc7dc-232">**Пример JSON-файла с разделителем-строкой**</span><span class="sxs-lookup"><span data-stu-id="bc7dc-232">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="bc7dc-233">**Пример объединенного JSON-файла**</span><span class="sxs-lookup"><span data-stu-id="bc7dc-233">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="bc7dc-234">**Тип 2: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="bc7dc-234">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="bc7dc-235">Каждый файл содержит массив объектов.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-235">Each file contains an array of objects.</span></span>

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

### <a name="jsonformat-example"></a><span data-ttu-id="bc7dc-236">Пример JsonFormat</span><span class="sxs-lookup"><span data-stu-id="bc7dc-236">JsonFormat example</span></span>

<span data-ttu-id="bc7dc-237">**Вариант 1. Копирование данных из JSON-файлов**</span><span class="sxs-lookup"><span data-stu-id="bc7dc-237">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="bc7dc-238">Ниже приведены два примера копирования данных из JSON-файлов.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-238">See the following two samples when copying data from JSON files.</span></span> <span data-ttu-id="bc7dc-239">Учтите описанные далее общие моменты.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-239">The generic points to note:</span></span>

<span data-ttu-id="bc7dc-240">**Пример 1. Извлечение данных из объекта и массива**</span><span class="sxs-lookup"><span data-stu-id="bc7dc-240">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="bc7dc-241">В этом примере предполагается, что один корневой объект JSON соответствует одной записи в таблице результатов.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-241">In this sample, you expect one root JSON object maps to single record in tabular result.</span></span> <span data-ttu-id="bc7dc-242">Если у вас есть JSON-файл со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="bc7dc-242">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="bc7dc-243">и вы хотите скопировать это содержимое (посредством извлечения данных из объекта и массива) в таблицу SQL Azure в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="bc7dc-243">and you want to copy it into an Azure SQL table in the following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="bc7dc-244">id</span><span class="sxs-lookup"><span data-stu-id="bc7dc-244">id</span></span> | <span data-ttu-id="bc7dc-245">deviceType</span><span class="sxs-lookup"><span data-stu-id="bc7dc-245">deviceType</span></span> | <span data-ttu-id="bc7dc-246">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="bc7dc-246">targetResourceType</span></span> | <span data-ttu-id="bc7dc-247">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="bc7dc-247">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="bc7dc-248">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="bc7dc-248">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="bc7dc-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="bc7dc-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="bc7dc-250">PC</span><span class="sxs-lookup"><span data-stu-id="bc7dc-250">PC</span></span> | <span data-ttu-id="bc7dc-251">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="bc7dc-251">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="bc7dc-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="bc7dc-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="bc7dc-253">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="bc7dc-253">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="bc7dc-254">Входной набор данных с типом **JsonFormat** определяется следующим образом (частичное определение только соответствующих частей).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-254">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="bc7dc-255">В частности:</span><span class="sxs-lookup"><span data-stu-id="bc7dc-255">More specifically:</span></span>

- <span data-ttu-id="bc7dc-256">Раздел `structure` определяет настраиваемые имена столбцов и соответствующие типы данных при преобразовании в табличные данные.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-256">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="bc7dc-257">Этот раздел является **необязательным**, если вам не нужно сопоставлять столбцы.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-257">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="bc7dc-258">См. дополнительные сведения о [сопоставлении столбцов исходного набора данных со столбцами целевого набора данных](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-258">See [Map source dataset columns to destination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="bc7dc-259">`jsonPathDefinition` указывает путь к файлу JSON для каждого столбца, который определяет, откуда следует извлекать данные.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-259">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="bc7dc-260">Чтобы скопировать данные из массива, с помощью **array[X].property** можно извлечь значение нужного свойства из объекта X или с помощью **array[*].property** найти нужное значение в любом объекте с таким свойством.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-260">To copy data from array, you can use **array[x].property** to extract value of the given property from the xth object, or you can use **array[*].property** to find the value from any object containing such property.</span></span>

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

<span data-ttu-id="bc7dc-261">**Пример 2. Применение нескольких объектов с одинаковым шаблоном из массива**</span><span class="sxs-lookup"><span data-stu-id="bc7dc-261">**Sample 2: cross apply multiple objects with the same pattern from array**</span></span>

<span data-ttu-id="bc7dc-262">В этом примере предполагается, что один корневой объект JSON будет преобразован в несколько записей в таблице результатов.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-262">In this sample, you expect to transform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="bc7dc-263">Если у вас есть JSON-файл со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="bc7dc-263">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="bc7dc-264">И если вы хотите скопировать этот файл в таблицу Azure SQL в следующем формате путем сведения данных внутри массива и перекрестного соединения с общими сведениями о корневом объекте:</span><span class="sxs-lookup"><span data-stu-id="bc7dc-264">and you want to copy it into an Azure SQL table in the following format, by flattening the data inside the array and cross join with the common root info:</span></span>

| <span data-ttu-id="bc7dc-265">ordernumber</span><span class="sxs-lookup"><span data-stu-id="bc7dc-265">ordernumber</span></span> | <span data-ttu-id="bc7dc-266">orderdate</span><span class="sxs-lookup"><span data-stu-id="bc7dc-266">orderdate</span></span> | <span data-ttu-id="bc7dc-267">order_pd</span><span class="sxs-lookup"><span data-stu-id="bc7dc-267">order_pd</span></span> | <span data-ttu-id="bc7dc-268">order_price</span><span class="sxs-lookup"><span data-stu-id="bc7dc-268">order_price</span></span> | <span data-ttu-id="bc7dc-269">city</span><span class="sxs-lookup"><span data-stu-id="bc7dc-269">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="bc7dc-270">01</span><span class="sxs-lookup"><span data-stu-id="bc7dc-270">01</span></span> | <span data-ttu-id="bc7dc-271">20170122</span><span class="sxs-lookup"><span data-stu-id="bc7dc-271">20170122</span></span> | <span data-ttu-id="bc7dc-272">P1</span><span class="sxs-lookup"><span data-stu-id="bc7dc-272">P1</span></span> | <span data-ttu-id="bc7dc-273">23</span><span class="sxs-lookup"><span data-stu-id="bc7dc-273">23</span></span> | <span data-ttu-id="bc7dc-274">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="bc7dc-274">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="bc7dc-275">01</span><span class="sxs-lookup"><span data-stu-id="bc7dc-275">01</span></span> | <span data-ttu-id="bc7dc-276">20170122</span><span class="sxs-lookup"><span data-stu-id="bc7dc-276">20170122</span></span> | <span data-ttu-id="bc7dc-277">P2</span><span class="sxs-lookup"><span data-stu-id="bc7dc-277">P2</span></span> | <span data-ttu-id="bc7dc-278">13.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-278">13</span></span> | <span data-ttu-id="bc7dc-279">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="bc7dc-279">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="bc7dc-280">01</span><span class="sxs-lookup"><span data-stu-id="bc7dc-280">01</span></span> | <span data-ttu-id="bc7dc-281">20170122</span><span class="sxs-lookup"><span data-stu-id="bc7dc-281">20170122</span></span> | <span data-ttu-id="bc7dc-282">P3</span><span class="sxs-lookup"><span data-stu-id="bc7dc-282">P3</span></span> | <span data-ttu-id="bc7dc-283">231</span><span class="sxs-lookup"><span data-stu-id="bc7dc-283">231</span></span> | <span data-ttu-id="bc7dc-284">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="bc7dc-284">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="bc7dc-285">Входной набор данных с типом **JsonFormat** определяется следующим образом (частичное определение только соответствующих частей).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-285">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="bc7dc-286">В частности:</span><span class="sxs-lookup"><span data-stu-id="bc7dc-286">More specifically:</span></span>

- <span data-ttu-id="bc7dc-287">Раздел `structure` определяет настраиваемые имена столбцов и соответствующие типы данных при преобразовании в табличные данные.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-287">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="bc7dc-288">Этот раздел является **необязательным**, если вам не нужно сопоставлять столбцы.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-288">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="bc7dc-289">См. дополнительные сведения о [сопоставлении столбцов исходного набора данных со столбцами целевого набора данных](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-289">See [Map source dataset columns to destination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="bc7dc-290">Параметр `jsonNodeReference` обозначает итерацию и извлечение данных из объектов с одинаковым шаблоном в разделе orderlines **массива**.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-290">`jsonNodeReference` indicates to iterate and extract data from the objects with the same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="bc7dc-291">`jsonPathDefinition` указывает путь к файлу JSON для каждого столбца, который определяет, откуда следует извлекать данные.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-291">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="bc7dc-292">В этом примере значения ordernumber, orderdate и city находятся в корневом объекте. Путь JSON к этому объекту начинается с "$." а значения order_pd и order_price определяются с помощью пути, производного от элемента массива без "$.".</span><span class="sxs-lookup"><span data-stu-id="bc7dc-292">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from the array element without "$.".</span></span>

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

<span data-ttu-id="bc7dc-293">**Обратите внимание на следующие моменты.**</span><span class="sxs-lookup"><span data-stu-id="bc7dc-293">**Note the following points:**</span></span>

* <span data-ttu-id="bc7dc-294">Если параметры `structure` и `jsonPathDefinition` не определены в наборе данных фабрики данных, действие копирования обнаружит схему из первого объекта и выполнит сведение всего объекта.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-294">If the `structure` and `jsonPathDefinition` are not defined in the Data Factory dataset, the Copy Activity detects the schema from the first object and flatten the whole object.</span></span>
* <span data-ttu-id="bc7dc-295">Если входной JSON-файл содержит массив, по умолчанию действие копирования преобразует все значение массива в строку.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-295">If the JSON input has an array, by default the Copy Activity converts the entire array value into a string.</span></span> <span data-ttu-id="bc7dc-296">Вы можете извлечь данные из строки с помощью `jsonNodeReference` или `jsonPathDefinition`. Или можно пропустить строку, не указывая ее в `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-296">You can choose to extract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="bc7dc-297">Если на том же уровне существует повторяющиеся имена, то действие копирования выберет последнее из них.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-297">If there are duplicate names at the same level, the Copy Activity picks the last one.</span></span>
* <span data-ttu-id="bc7dc-298">В именах свойств учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-298">Property names are case-sensitive.</span></span> <span data-ttu-id="bc7dc-299">Два свойства с одинаковым именем, но в разных регистрах, рассматриваются как два отдельных свойства.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-299">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="bc7dc-300">**Вариант 2. Запись данных в JSON-файл**</span><span class="sxs-lookup"><span data-stu-id="bc7dc-300">**Case 2: Writing data to JSON file**</span></span>

<span data-ttu-id="bc7dc-301">Если в базе данных SQL есть следующая таблица:</span><span class="sxs-lookup"><span data-stu-id="bc7dc-301">If you have the following table in SQL Database:</span></span>

| <span data-ttu-id="bc7dc-302">id</span><span class="sxs-lookup"><span data-stu-id="bc7dc-302">id</span></span> | <span data-ttu-id="bc7dc-303">order_date</span><span class="sxs-lookup"><span data-stu-id="bc7dc-303">order_date</span></span> | <span data-ttu-id="bc7dc-304">order_price</span><span class="sxs-lookup"><span data-stu-id="bc7dc-304">order_price</span></span> | <span data-ttu-id="bc7dc-305">order_by</span><span class="sxs-lookup"><span data-stu-id="bc7dc-305">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bc7dc-306">1</span><span class="sxs-lookup"><span data-stu-id="bc7dc-306">1</span></span> | <span data-ttu-id="bc7dc-307">20170119</span><span class="sxs-lookup"><span data-stu-id="bc7dc-307">20170119</span></span> | <span data-ttu-id="bc7dc-308">2000</span><span class="sxs-lookup"><span data-stu-id="bc7dc-308">2000</span></span> | <span data-ttu-id="bc7dc-309">David</span><span class="sxs-lookup"><span data-stu-id="bc7dc-309">David</span></span> |
| <span data-ttu-id="bc7dc-310">2</span><span class="sxs-lookup"><span data-stu-id="bc7dc-310">2</span></span> | <span data-ttu-id="bc7dc-311">20170120</span><span class="sxs-lookup"><span data-stu-id="bc7dc-311">20170120</span></span> | <span data-ttu-id="bc7dc-312">3500</span><span class="sxs-lookup"><span data-stu-id="bc7dc-312">3500</span></span> | <span data-ttu-id="bc7dc-313">Patrick</span><span class="sxs-lookup"><span data-stu-id="bc7dc-313">Patrick</span></span> |
| <span data-ttu-id="bc7dc-314">3</span><span class="sxs-lookup"><span data-stu-id="bc7dc-314">3</span></span> | <span data-ttu-id="bc7dc-315">20170121</span><span class="sxs-lookup"><span data-stu-id="bc7dc-315">20170121</span></span> | <span data-ttu-id="bc7dc-316">4000</span><span class="sxs-lookup"><span data-stu-id="bc7dc-316">4000</span></span> | <span data-ttu-id="bc7dc-317">Jason</span><span class="sxs-lookup"><span data-stu-id="bc7dc-317">Jason</span></span> |

<span data-ttu-id="bc7dc-318">и для каждой записи вы предполагаете запись в объект JSON в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="bc7dc-318">and for each record, you expect to write to a JSON object in the following format:</span></span>
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

<span data-ttu-id="bc7dc-319">Выходной набор данных с типом **JsonFormat** определяется следующим образом (частичное определение только соответствующих частей).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-319">The output dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="bc7dc-320">В частности, раздел `structure` определяет настраиваемые имена свойств в конечном файле. Для определения уровня вложенности от имен будет использоваться разделитель вложенности `nestingSeparator` (по умолчанию — точка (.)).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-320">More specifically, `structure` section defines the customized property names in destination file, `nestingSeparator` (default is ".") are used to identify the nest layer from the name.</span></span> <span data-ttu-id="bc7dc-321">Этот раздел является **необязательным**, если вы не собираетесь изменять исходное имя свойства или вкладывать свойства.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-321">This section is **optional** unless you want to change the property name comparing with source column name, or nest some of the properties.</span></span>

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

## <a name="avro-format"></a><span data-ttu-id="bc7dc-322">Формат Avro</span><span class="sxs-lookup"><span data-stu-id="bc7dc-322">AVRO format</span></span>
<span data-ttu-id="bc7dc-323">Если требуется проанализировать файлы Avro или записать данные в формате Avro, установите для свойства `format` `type` значение **AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-323">If you want to parse the Avro files or write the data in Avro format, set the `format` `type` property to **AvroFormat**.</span></span> <span data-ttu-id="bc7dc-324">Вам не нужно указывать какие-либо свойства в подразделе Format раздела typeProperties.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-324">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="bc7dc-325">Пример:</span><span class="sxs-lookup"><span data-stu-id="bc7dc-325">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="bc7dc-326">Сведения об использовании формата Avro в таблице Hive см. в [руководстве по Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-326">To use Avro format in a Hive table, you can refer to [Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="bc7dc-327">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-327">Note the following points:</span></span>  

* <span data-ttu-id="bc7dc-328">[Сложные типы данных](http://avro.apache.org/docs/current/spec.html#schema_complex) (записи, перечисления, массивы, сопоставления, объединения и фиксированные данные) не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-328">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions, and fixed).</span></span>

## <a name="orc-format"></a><span data-ttu-id="bc7dc-329">Формат ORC</span><span class="sxs-lookup"><span data-stu-id="bc7dc-329">ORC format</span></span>
<span data-ttu-id="bc7dc-330">Если требуется проанализировать ORC-файлы или записать данные в формате ORC, установите для свойства `format` `type` значение **OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-330">If you want to parse the ORC files or write the data in ORC format, set the `format` `type` property to **OrcFormat**.</span></span> <span data-ttu-id="bc7dc-331">Вам не нужно указывать какие-либо свойства в подразделе Format раздела typeProperties.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-331">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="bc7dc-332">Пример:</span><span class="sxs-lookup"><span data-stu-id="bc7dc-332">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="bc7dc-333">Если вы не копируете ORC-файлов **как есть** между локальным и облачным хранилищами данных, то на компьютере шлюза необходимо установить 8 JRE (среду выполнения Java).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-333">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="bc7dc-334">Для 64-разрядного шлюза требуется 64-разрядная версия JRE, а для 32-разрядного шлюза — 32-разрядная версия JRE.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-334">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="bc7dc-335">Обе эти версии доступны [здесь](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-335">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="bc7dc-336">Выберите ту, что вам подходит.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-336">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="bc7dc-337">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-337">Note the following points:</span></span>

* <span data-ttu-id="bc7dc-338">Данные сложных типов (STRUCT, MAP, LIST, UNION) не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-338">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="bc7dc-339">Для ORC-файлов используется три [параметра сжатия](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB и SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-339">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="bc7dc-340">Фабрика данных поддерживает чтение данных из ORC-файла в любом из этих форматов.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-340">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="bc7dc-341">Для чтения данных используется кодек сжатия из метаданных.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-341">It uses the compression codec is in the metadata to read the data.</span></span> <span data-ttu-id="bc7dc-342">Однако при записи в ORC-файл фабрика данных по умолчанию выбирает ZLIB.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-342">However, when writing to an ORC file, Data Factory chooses ZLIB, which is the default for ORC.</span></span> <span data-ttu-id="bc7dc-343">В настоящее время изменить это поведение нельзя.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-343">Currently, there is no option to override this behavior.</span></span>

## <a name="parquet-format"></a><span data-ttu-id="bc7dc-344">Формат Parquet</span><span class="sxs-lookup"><span data-stu-id="bc7dc-344">Parquet format</span></span>
<span data-ttu-id="bc7dc-345">Если требуется проанализировать файлы Parquet или записать данные в формате Parquet, установите для свойства `format` `type` значение **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-345">If you want to parse the Parquet files or write the data in Parquet format, set the `format` `type` property to **ParquetFormat**.</span></span> <span data-ttu-id="bc7dc-346">Вам не нужно указывать какие-либо свойства в подразделе Format раздела typeProperties.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-346">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="bc7dc-347">Пример:</span><span class="sxs-lookup"><span data-stu-id="bc7dc-347">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="bc7dc-348">Если вы не копируете Parquet-файлы **как есть** между локальным и облачным хранилищами данных, то на компьютере шлюза необходимо установить JRE 8 (среду выполнения Java).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-348">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="bc7dc-349">Для 64-разрядного шлюза требуется 64-разрядная версия JRE, а для 32-разрядного шлюза — 32-разрядная версия JRE.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-349">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="bc7dc-350">Обе эти версии доступны [здесь](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-350">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="bc7dc-351">Выберите ту, что вам подходит.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-351">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="bc7dc-352">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-352">Note the following points:</span></span>

* <span data-ttu-id="bc7dc-353">Данные сложных типов (MAP, LIST) не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-353">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="bc7dc-354">Parquet-файл имеет следующие варианты сжатия: NONE, SNAPPY, GZIP и LZO.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-354">Parquet file has the following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="bc7dc-355">Фабрика данных поддерживает чтение данных из ORC-файла в любом из этих форматов.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-355">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="bc7dc-356">Для чтения данных используется кодек сжатия из метаданных.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-356">It uses the compression codec in the metadata to read the data.</span></span> <span data-ttu-id="bc7dc-357">Однако при записи в Parquet-файл фабрика данных по умолчанию выбирает SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-357">However, when writing to a Parquet file, Data Factory chooses SNAPPY, which is the default for Parquet format.</span></span> <span data-ttu-id="bc7dc-358">В настоящее время изменить это поведение нельзя.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-358">Currently, there is no option to override this behavior.</span></span>

## <a name="compression-support"></a><span data-ttu-id="bc7dc-359">Поддержка сжатия</span><span class="sxs-lookup"><span data-stu-id="bc7dc-359">Compression support</span></span>
<span data-ttu-id="bc7dc-360">Обработка больших наборов данных может привести к возникновению узких мест ввода-вывода и сети.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-360">Processing large data sets can cause I/O and network bottlenecks.</span></span> <span data-ttu-id="bc7dc-361">Поэтому использование сжатых данных в хранилищах может не только ускорить передачу данных по сети и освободить место на диске, но также обеспечить и значительное повышение производительности при обработке больших данных.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-361">Therefore, compressed data in stores can not only speed up data transfer across the network and save disk space, but also bring significant performance improvements in processing big data.</span></span> <span data-ttu-id="bc7dc-362">Сейчас сжатие поддерживается для файловых хранилищ данных, таких как хранилище BLOB-объектов Azure или локальная файловая система.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-362">Currently, compression is supported for file-based data stores such as Azure Blob or On-premises File System.</span></span>  

<span data-ttu-id="bc7dc-363">Чтобы указать сжатие для набора данных, используйте свойство **compression** в наборе данных JSON, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-363">To specify compression for a dataset, use the **compression** property in the dataset JSON as in the following example:</span></span>   

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

<span data-ttu-id="bc7dc-364">Предположим, что приведенный выше пример набора данных используется в качестве результата операции копирования. Эта операция сжимает выходные данные с использованием кодека GZIP и оптимального коэффициента сжатия, а затем записывает сжатые данные в файл с именем pagecounts.csv.gz в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-364">Suppose the sample dataset is used as the output of a copy activity, the copy activity compresses the output data with GZIP codec using optimal ratio and then write the compressed data into a file named pagecounts.csv.gz in the Azure Blob Storage.</span></span>

> [!NOTE]
> <span data-ttu-id="bc7dc-365">Параметры сжатия для данных в форматах **AvroFormat**, **OrcFormat** или **ParquetFormat** не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-365">Compression settings are not supported for data in the **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span></span> <span data-ttu-id="bc7dc-366">Для чтения данных в этих форматах фабрика данных выявляет и использует в метаданных кодек сжатия.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-366">When reading files in these formats, Data Factory detects and uses the compression codec in the metadata.</span></span> <span data-ttu-id="bc7dc-367">При записи в файл в одном из этих форматов фабрика данных выбирает кодек сжатия по умолчанию для этого формата.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-367">When writing to files in these formats, Data Factory chooses the default compression codec for that format.</span></span> <span data-ttu-id="bc7dc-368">Например, ZLIB для OrcFormat и SNAPPY для ParquetFormat.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-368">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span></span>   

<span data-ttu-id="bc7dc-369">Раздел **compression** содержит два свойства:</span><span class="sxs-lookup"><span data-stu-id="bc7dc-369">The **compression** section has two properties:</span></span>  

* <span data-ttu-id="bc7dc-370">**Type** — кодек сжатия. Возможные значения: **GZIP**, **Deflate**, **BZIP2** или **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-370">**Type:** the compression codec, which can be **GZIP**, **Deflate**, **BZIP2**, or **ZipDeflate**.</span></span>  
* <span data-ttu-id="bc7dc-371">**Level** — коэффициент сжатия; возможные значения: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-371">**Level:** the compression ratio, which can be **Optimal** or **Fastest**.</span></span>

  * <span data-ttu-id="bc7dc-372">**Fastest:** операция сжатия должна выполняться как можно быстрее, даже если итоговый файл сжимается не оптимально.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-372">**Fastest:** The compression operation should complete as quickly as possible, even if the resulting file is not optimally compressed.</span></span>
  * <span data-ttu-id="bc7dc-373">**Optimal**: операция сжатия должна выполняться оптимально, даже если для ее завершения требуется больше времени.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-373">**Optimal**: The compression operation should be optimally compressed, even if the operation takes a longer time to complete.</span></span>

    <span data-ttu-id="bc7dc-374">Дополнительные сведения см. в разделе [Уровень сжатия](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx).</span><span class="sxs-lookup"><span data-stu-id="bc7dc-374">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span></span>

<span data-ttu-id="bc7dc-375">Когда вы определяете свойство `compression` во входном наборе данных JSON, конвейер может считывать сжатые данные из источника. При определении же этого свойства в выходном наборе данных JSON операция копирования может записывать сжатые данные в целевое расположение.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-375">When you specify `compression` property in an input dataset JSON, the pipeline can read compressed data from the source; and when you specify the property in an output dataset JSON, the copy activity can write compressed data to the destination.</span></span> <span data-ttu-id="bc7dc-376">Ниже приведено несколько примеров сценариев:</span><span class="sxs-lookup"><span data-stu-id="bc7dc-376">Here are a few sample scenarios:</span></span>

* <span data-ttu-id="bc7dc-377">Считайте сжатые с помощью кодека GZIP данные из BLOB-объекта Azure, распакуйте их и запишите результирующие данные в Базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-377">Read GZIP compressed data from an Azure blob, decompress it, and write result data to an Azure SQL database.</span></span> <span data-ttu-id="bc7dc-378">Вы определяете входной набор данных BLOB-объекта Azure с помощью свойства JSON `compression` `type` как GZIP.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-378">You define the input Azure Blob dataset with the `compression` `type` JSON property as GZIP.</span></span>
* <span data-ttu-id="bc7dc-379">Считайте данные из обычного текстового файла в локальной файловой системе, сожмите их в формате GZip и запишите сжатые данные в BLOB-объект Azure.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-379">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write the compressed data to an Azure blob.</span></span> <span data-ttu-id="bc7dc-380">Вы определяете выходной набор данных BLOB-объекта Azure с помощью свойства JSON `compression` `type` как GZip.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-380">You define an output Azure Blob dataset with the `compression` `type` JSON property as GZip.</span></span>
* <span data-ttu-id="bc7dc-381">Считайте ZIP-файл с FTP-сервера, распакуйте его, чтобы получить содержащиеся в нем файлы, и отправьте их в хранилище Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-381">Read .zip file from FTP server, decompress it to get the files inside, and land those files into Azure Data Lake Store.</span></span> <span data-ttu-id="bc7dc-382">Вы определяете входной набор данных FTP с помощью свойства JSON `compression` `type` как ZipDeflate.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-382">You define an input FTP dataset with the `compression` `type` JSON property as ZipDeflate.</span></span>
* <span data-ttu-id="bc7dc-383">Считайте сжатые с помощью кодека GZIP данные из BLOB-объекта Azure, распакуйте их и сожмите с помощью BZIP2, а затем запишите результирующие данные в BLOB-объект Azure.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-383">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data to an Azure blob.</span></span> <span data-ttu-id="bc7dc-384">Вы определяете входной набор данных BLOB-объекта Azure, установив для `compression` `type` значение GZIP, и выходной набор данных, установив для `compression` `type` значение BZIP2.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-384">You define the input Azure Blob dataset with `compression` `type` set to GZIP and the output dataset with `compression` `type` set to BZIP2 in this case.</span></span>   


## <a name="next-steps"></a><span data-ttu-id="bc7dc-385">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bc7dc-385">Next steps</span></span>
<span data-ttu-id="bc7dc-386">Ниже приведены статьи для файловых хранилищ данных, поддерживаемых фабрикой данных Azure.</span><span class="sxs-lookup"><span data-stu-id="bc7dc-386">See the following articles for file-based data stores supported by Azure Data Factory:</span></span>

- [<span data-ttu-id="bc7dc-387">Хранилище BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="bc7dc-387">Azure Blob Storage</span></span>](data-factory-azure-blob-connector.md)
- [<span data-ttu-id="bc7dc-388">Хранилище озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="bc7dc-388">Azure Data Lake Store</span></span>](data-factory-azure-datalake-connector.md)
- [<span data-ttu-id="bc7dc-389">FTP</span><span class="sxs-lookup"><span data-stu-id="bc7dc-389">FTP</span></span>](data-factory-ftp-connector.md)
- [<span data-ttu-id="bc7dc-390">HDFS</span><span class="sxs-lookup"><span data-stu-id="bc7dc-390">HDFS</span></span>](data-factory-hdfs-connector.md)
- [<span data-ttu-id="bc7dc-391">Перемещение данных в локальную файловую систему или из нее с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="bc7dc-391">File System</span></span>](data-factory-onprem-file-system-connector.md)
- [<span data-ttu-id="bc7dc-392">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="bc7dc-392">Amazon S3</span></span>](data-factory-amazon-simple-storage-service-connector.md)
