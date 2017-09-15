## <a name="specifying-formats"></a><span data-ttu-id="df238-101">Указание форматов</span><span class="sxs-lookup"><span data-stu-id="df238-101">Specifying formats</span></span>
<span data-ttu-id="df238-102">Фабрика данных Azure поддерживает следующие типы форматов:</span><span class="sxs-lookup"><span data-stu-id="df238-102">Azure Data Factory supports the following format types:</span></span>

* <span data-ttu-id="df238-103">[текстовый формат](#specifying-textformat);</span><span class="sxs-lookup"><span data-stu-id="df238-103">[Text Format](#specifying-textformat)</span></span>
* <span data-ttu-id="df238-104">[формат JSON](#specifying-jsonformat);</span><span class="sxs-lookup"><span data-stu-id="df238-104">[JSON Format](#specifying-jsonformat)</span></span>
* <span data-ttu-id="df238-105">[формат Avro](#specifying-avroformat);</span><span class="sxs-lookup"><span data-stu-id="df238-105">[Avro Format](#specifying-avroformat)</span></span>
* <span data-ttu-id="df238-106">[формат ORC](#specifying-orcformat);</span><span class="sxs-lookup"><span data-stu-id="df238-106">[ORC Format](#specifying-orcformat)</span></span>
* <span data-ttu-id="df238-107">[формат PARQUET](#specifying-parquetformat).</span><span class="sxs-lookup"><span data-stu-id="df238-107">[Parquet Format](#specifying-parquetformat)</span></span>

### <a name="specifying-textformat"></a><span data-ttu-id="df238-108">Определение TextFormat</span><span class="sxs-lookup"><span data-stu-id="df238-108">Specifying TextFormat</span></span>
<span data-ttu-id="df238-109">Если требуется анализировать текстовые файлы или записать данные в текстовом формате, установите для свойства `format` `type` значение **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="df238-109">If you want to parse the text files or write the data in text format, set the `format` `type` property to **TextFormat**.</span></span> <span data-ttu-id="df238-110">В разделе `format` также можно указать следующие **необязательные** свойства.</span><span class="sxs-lookup"><span data-stu-id="df238-110">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="df238-111">Инструкции по настройке см. в разделе [Пример TextFormat](#textformat-example).</span><span class="sxs-lookup"><span data-stu-id="df238-111">See [TextFormat example](#textformat-example) section on how to configure.</span></span>

| <span data-ttu-id="df238-112">Свойство</span><span class="sxs-lookup"><span data-stu-id="df238-112">Property</span></span> | <span data-ttu-id="df238-113">Описание</span><span class="sxs-lookup"><span data-stu-id="df238-113">Description</span></span> | <span data-ttu-id="df238-114">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="df238-114">Allowed values</span></span> | <span data-ttu-id="df238-115">Обязательно</span><span class="sxs-lookup"><span data-stu-id="df238-115">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="df238-116">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="df238-116">columnDelimiter</span></span> |<span data-ttu-id="df238-117">Знак, используемый для разделения столбцов в файле.</span><span class="sxs-lookup"><span data-stu-id="df238-117">The character used to separate columns in a file.</span></span> <span data-ttu-id="df238-118">Вы можете использовать редкий непечатаемый символ, который обычно отсутствует в данных: например, укажите \u0001 (символ начала заголовка).</span><span class="sxs-lookup"><span data-stu-id="df238-118">You can consider to use a rare unprintable char which not likely exists in your data: e.g. specify "\u0001" which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="df238-119">Допускается только один знак.</span><span class="sxs-lookup"><span data-stu-id="df238-119">Only one character is allowed.</span></span> <span data-ttu-id="df238-120">Значение **по умолчанию** — **запятая (,)**.</span><span class="sxs-lookup"><span data-stu-id="df238-120">The **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="df238-121">Чтобы использовать [символы Юникода](https://en.wikipedia.org/wiki/List_of_Unicode_characters), необходимо получить соответствующий код.</span><span class="sxs-lookup"><span data-stu-id="df238-121">To use an Unicode character, refer to [Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) to get the corresponding code for it.</span></span> |<span data-ttu-id="df238-122">Нет</span><span class="sxs-lookup"><span data-stu-id="df238-122">No</span></span> |
| <span data-ttu-id="df238-123">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="df238-123">rowDelimiter</span></span> |<span data-ttu-id="df238-124">Знак, используемый для разделения строк в файле.</span><span class="sxs-lookup"><span data-stu-id="df238-124">The character used to separate rows in a file.</span></span> |<span data-ttu-id="df238-125">Допускается только один знак.</span><span class="sxs-lookup"><span data-stu-id="df238-125">Only one character is allowed.</span></span> <span data-ttu-id="df238-126">**По умолчанию** используется одно из следующих значений: **для чтения — [\r\n, \r, \n]**, для записи — **\r\n**.</span><span class="sxs-lookup"><span data-stu-id="df238-126">The **default** value is any of the following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="df238-127">Нет</span><span class="sxs-lookup"><span data-stu-id="df238-127">No</span></span> |
| <span data-ttu-id="df238-128">escapeChar</span><span class="sxs-lookup"><span data-stu-id="df238-128">escapeChar</span></span> |<span data-ttu-id="df238-129">Специальный знак, используемый для экранирования разделителя столбцов в содержимом входного файла.</span><span class="sxs-lookup"><span data-stu-id="df238-129">The special character used to escape a column delimiter in the content of input file.</span></span> <br/><br/><span data-ttu-id="df238-130">Для таблицы нельзя указать и escapeChar, и quoteChar.</span><span class="sxs-lookup"><span data-stu-id="df238-130">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="df238-131">Допускается только один знак.</span><span class="sxs-lookup"><span data-stu-id="df238-131">Only one character is allowed.</span></span> <span data-ttu-id="df238-132">Значение по умолчанию отсутствует.</span><span class="sxs-lookup"><span data-stu-id="df238-132">No default value.</span></span> <br/><br/><span data-ttu-id="df238-133">Например, если в качестве разделителя столбцов используется запятая (,), но этот знак встречается и в тексте (пример: "Hello, world"), то в качестве знака экранирования можно определить знак доллара ($) и использовать в исходном тексте строку "Hello$, world".</span><span class="sxs-lookup"><span data-stu-id="df238-133">Example: if you have comma (',') as the column delimiter but you want to have the comma character in the text (example: "Hello, world"), you can define ‘$’ as the escape character and use string "Hello$, world" in the source.</span></span> |<span data-ttu-id="df238-134">Нет</span><span class="sxs-lookup"><span data-stu-id="df238-134">No</span></span> |
| <span data-ttu-id="df238-135">quoteChar</span><span class="sxs-lookup"><span data-stu-id="df238-135">quoteChar</span></span> |<span data-ttu-id="df238-136">Знак, используемый в качестве кавычки для заключения строкового значения.</span><span class="sxs-lookup"><span data-stu-id="df238-136">The character used to quote a string value.</span></span> <span data-ttu-id="df238-137">Разделители столбцов и строк внутри знаков кавычек будут рассматриваться как часть строкового значения.</span><span class="sxs-lookup"><span data-stu-id="df238-137">The column and row delimiters inside the quote characters would be treated as part of the string value.</span></span> <span data-ttu-id="df238-138">Это свойство применимо к входным и выходным наборам данных.</span><span class="sxs-lookup"><span data-stu-id="df238-138">This property is applicable to both input and output datasets.</span></span><br/><br/><span data-ttu-id="df238-139">Для таблицы нельзя указать и escapeChar, и quoteChar.</span><span class="sxs-lookup"><span data-stu-id="df238-139">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="df238-140">Допускается только один знак.</span><span class="sxs-lookup"><span data-stu-id="df238-140">Only one character is allowed.</span></span> <span data-ttu-id="df238-141">Значение по умолчанию отсутствует.</span><span class="sxs-lookup"><span data-stu-id="df238-141">No default value.</span></span> <br/><br/><span data-ttu-id="df238-142">Например, если в качестве разделителя столбцов используется запятая (,) и нужно, чтобы этот знак встречался в тексте (например, <Hello, world>), то можно в качестве знака кавычек определить двойную кавычку (") и использовать в исходном тексте строку "Hello, world".</span><span class="sxs-lookup"><span data-stu-id="df238-142">For example, if you have comma (',') as the column delimiter but you want to have comma character in the text (example: <Hello, world>), you can define " (double quote) as the quote character and use the string "Hello, world" in the source.</span></span> |<span data-ttu-id="df238-143">Нет</span><span class="sxs-lookup"><span data-stu-id="df238-143">No</span></span> |
| <span data-ttu-id="df238-144">nullValue</span><span class="sxs-lookup"><span data-stu-id="df238-144">nullValue</span></span> |<span data-ttu-id="df238-145">Один или несколько знаков, используемых для представления значения NULL.</span><span class="sxs-lookup"><span data-stu-id="df238-145">One or more characters used to represent a null value.</span></span> |<span data-ttu-id="df238-146">Один или несколько знаков.</span><span class="sxs-lookup"><span data-stu-id="df238-146">One or more characters.</span></span> <span data-ttu-id="df238-147">Значения **по умолчанию**: **\N и NULL** для чтения и **\N** для записи.</span><span class="sxs-lookup"><span data-stu-id="df238-147">The **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="df238-148">Нет</span><span class="sxs-lookup"><span data-stu-id="df238-148">No</span></span> |
| <span data-ttu-id="df238-149">encodingName</span><span class="sxs-lookup"><span data-stu-id="df238-149">encodingName</span></span> |<span data-ttu-id="df238-150">Имя кодировки.</span><span class="sxs-lookup"><span data-stu-id="df238-150">Specify the encoding name.</span></span> |<span data-ttu-id="df238-151">Допустимое имя кодировки.</span><span class="sxs-lookup"><span data-stu-id="df238-151">A valid encoding name.</span></span> <span data-ttu-id="df238-152">Ознакомьтесь с описанием свойства [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="df238-152">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="df238-153">Пример: windows-1250 или shift_jis.</span><span class="sxs-lookup"><span data-stu-id="df238-153">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="df238-154">**По умолчанию** используется **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="df238-154">The **default** value is **UTF-8**.</span></span> |<span data-ttu-id="df238-155">Нет</span><span class="sxs-lookup"><span data-stu-id="df238-155">No</span></span> |
| <span data-ttu-id="df238-156">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="df238-156">firstRowAsHeader</span></span> |<span data-ttu-id="df238-157">Указывает, следует ли рассматривать первую строки в качестве заголовка.</span><span class="sxs-lookup"><span data-stu-id="df238-157">Specifies whether to consider the first row as a header.</span></span> <span data-ttu-id="df238-158">Фабрика данных считывает первую строку входного набора данных как заголовок.</span><span class="sxs-lookup"><span data-stu-id="df238-158">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="df238-159">Фабрика данных записывает первую строку как заголовок в выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="df238-159">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="df238-160">Примеры сценариев см. в разделе [Сценарии использования `firstRowAsHeader` и `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount).</span><span class="sxs-lookup"><span data-stu-id="df238-160">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="df238-161">Да</span><span class="sxs-lookup"><span data-stu-id="df238-161">True</span></span><br/><span data-ttu-id="df238-162">**False (по умолчанию)**</span><span class="sxs-lookup"><span data-stu-id="df238-162">**False (default)**</span></span> |<span data-ttu-id="df238-163">Нет</span><span class="sxs-lookup"><span data-stu-id="df238-163">No</span></span> |
| <span data-ttu-id="df238-164">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="df238-164">skipLineCount</span></span> |<span data-ttu-id="df238-165">Указывает количество строк, которые нужно пропустить при чтении данных из входных файлов.</span><span class="sxs-lookup"><span data-stu-id="df238-165">Indicates the number of rows to skip when reading data from input files.</span></span> <span data-ttu-id="df238-166">Если указаны skipLineCount и firstRowAsHeader, то сначала пропускаются строки, после чего из входного файла считываются данные заголовка.</span><span class="sxs-lookup"><span data-stu-id="df238-166">If both skipLineCount and firstRowAsHeader are specified, the lines are skipped first and then the header information is read from the input file.</span></span> <br/><br/><span data-ttu-id="df238-167">Примеры сценариев см. в разделе [Сценарии использования `firstRowAsHeader` и `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount).</span><span class="sxs-lookup"><span data-stu-id="df238-167">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="df238-168">Целое число </span><span class="sxs-lookup"><span data-stu-id="df238-168">Integer</span></span> |<span data-ttu-id="df238-169">Нет</span><span class="sxs-lookup"><span data-stu-id="df238-169">No</span></span> |
| <span data-ttu-id="df238-170">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="df238-170">treatEmptyAsNull</span></span> |<span data-ttu-id="df238-171">Указывает, следует ли интерпретировать строки со значением NULL или пустые строки как значение NULL при чтении данных из входного файла.</span><span class="sxs-lookup"><span data-stu-id="df238-171">Specifies whether to treat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="df238-172">**True (по умолчанию)**</span><span class="sxs-lookup"><span data-stu-id="df238-172">**True (default)**</span></span><br/><span data-ttu-id="df238-173">Ложь</span><span class="sxs-lookup"><span data-stu-id="df238-173">False</span></span> |<span data-ttu-id="df238-174">Нет</span><span class="sxs-lookup"><span data-stu-id="df238-174">No</span></span> |

#### <a name="textformat-example"></a><span data-ttu-id="df238-175">Пример TextFormat</span><span class="sxs-lookup"><span data-stu-id="df238-175">TextFormat example</span></span>
<span data-ttu-id="df238-176">В следующем примере показаны некоторые свойства формата для TextFormat.</span><span class="sxs-lookup"><span data-stu-id="df238-176">The following sample shows some of the format properties for TextFormat.</span></span>

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

<span data-ttu-id="df238-177">Чтобы использовать `escapeChar` вместо `quoteChar`, замените строку с `quoteChar` следующим escape-символом:</span><span class="sxs-lookup"><span data-stu-id="df238-177">To use an `escapeChar` instead of `quoteChar`, replace the line with `quoteChar` with the following escapeChar:</span></span>

```json
"escapeChar": "$",
```

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="df238-178">Сценарии использования firstRowAsHeader и skipLineCount</span><span class="sxs-lookup"><span data-stu-id="df238-178">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="df238-179">Вы выполняете копирование из нефайлового источника в текстовый файл и хотите добавить строку заголовка, содержащую метаданные схемы (например, схемы SQL).</span><span class="sxs-lookup"><span data-stu-id="df238-179">You are copying from a non-file source to a text file and would like to add a header line containing the schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="df238-180">В этом случае укажите `firstRowAsHeader` со значением true в выходном наборе данных.</span><span class="sxs-lookup"><span data-stu-id="df238-180">Specify `firstRowAsHeader` as true in the output dataset for this scenario.</span></span>
* <span data-ttu-id="df238-181">Вы копируете данные из текстового файла, содержащего строку заголовка, в нефайловый приемник и хотите удалить эту строку.</span><span class="sxs-lookup"><span data-stu-id="df238-181">You are copying from a text file containing a header line to a non-file sink and would like to drop that line.</span></span> <span data-ttu-id="df238-182">Укажите `firstRowAsHeader` со значением true во входном наборе данных.</span><span class="sxs-lookup"><span data-stu-id="df238-182">Specify `firstRowAsHeader` as true in the input dataset.</span></span>
* <span data-ttu-id="df238-183">Вы копируете данные из текстового файла и хотите пропустить несколько строк в начале, которые не содержат ни данных, ни заголовка.</span><span class="sxs-lookup"><span data-stu-id="df238-183">You are copying from a text file and want to skip a few lines at the beginning that contain no data or header information.</span></span> <span data-ttu-id="df238-184">Укажите `skipLineCount`, чтобы задать число пропускаемых строк.</span><span class="sxs-lookup"><span data-stu-id="df238-184">Specify `skipLineCount` to indicate the number of lines to be skipped.</span></span> <span data-ttu-id="df238-185">Если остальная часть файла содержит строку заголовка, можно также указать `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="df238-185">If the rest of the file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="df238-186">Если указаны `skipLineCount` и `firstRowAsHeader`, сначала пропускаются строки, а затем из входного файла считываются данные заголовка.</span><span class="sxs-lookup"><span data-stu-id="df238-186">If both `skipLineCount` and `firstRowAsHeader` are specified, the lines are skipped first and then the header information is read from the input file</span></span>

### <a name="specifying-jsonformat"></a><span data-ttu-id="df238-187">Указание JsonFormat</span><span class="sxs-lookup"><span data-stu-id="df238-187">Specifying JsonFormat</span></span>
<span data-ttu-id="df238-188">Сведения об **импорте и экспорте файлов в формате JSON "как есть" в Azure Cosmos DB и обратно** см. в [этом разделе](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents).</span><span class="sxs-lookup"><span data-stu-id="df238-188">To **import/export JSON files as-is into/from Azure Cosmos DB**, see [Import/export JSON documents](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) section in the Azure Cosmos DB connector with details.</span></span>

<span data-ttu-id="df238-189">Если требуется проанализировать JSON-файлы или записать данные в формате JSON, установите для свойства `format` `type` значение **JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="df238-189">If you want to parse the JSON files or write the data in JSON format, set the `format` `type` property to **JsonFormat**.</span></span> <span data-ttu-id="df238-190">В разделе `format` также можно указать следующие **необязательные** свойства.</span><span class="sxs-lookup"><span data-stu-id="df238-190">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="df238-191">Инструкции по настройке см. в разделе [Пример JsonFormat](#jsonformat-example).</span><span class="sxs-lookup"><span data-stu-id="df238-191">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span>

| <span data-ttu-id="df238-192">Свойство</span><span class="sxs-lookup"><span data-stu-id="df238-192">Property</span></span> | <span data-ttu-id="df238-193">Описание</span><span class="sxs-lookup"><span data-stu-id="df238-193">Description</span></span> | <span data-ttu-id="df238-194">Обязательно</span><span class="sxs-lookup"><span data-stu-id="df238-194">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="df238-195">filePattern</span><span class="sxs-lookup"><span data-stu-id="df238-195">filePattern</span></span> |<span data-ttu-id="df238-196">Шаблон данных, хранящихся в каждом JSON-файле.</span><span class="sxs-lookup"><span data-stu-id="df238-196">Indicate the pattern of data stored in each JSON file.</span></span> <span data-ttu-id="df238-197">Допустимые значения: **setOfObjects** и **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="df238-197">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="df238-198">Значение **по умолчанию** — **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="df238-198">The **default** value is **setOfObjects**.</span></span> <span data-ttu-id="df238-199">Подробные сведения об этих шаблонах см. в разделе [Шаблоны файлов JSON](#json-file-patterns).</span><span class="sxs-lookup"><span data-stu-id="df238-199">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="df238-200">Нет</span><span class="sxs-lookup"><span data-stu-id="df238-200">No</span></span> |
| <span data-ttu-id="df238-201">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="df238-201">jsonNodeReference</span></span> | <span data-ttu-id="df238-202">Для итерации и извлечения данных из объектов в поле массива с таким же шаблоном укажите путь JSON этого массива.</span><span class="sxs-lookup"><span data-stu-id="df238-202">If you want to iterate and extract data from the objects inside an array field with the same pattern, specify the JSON path of that array.</span></span> <span data-ttu-id="df238-203">Это свойство поддерживается только в том случае, если данные копируются из JSON-файлов.</span><span class="sxs-lookup"><span data-stu-id="df238-203">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="df238-204">Нет</span><span class="sxs-lookup"><span data-stu-id="df238-204">No</span></span> |
| <span data-ttu-id="df238-205">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="df238-205">jsonPathDefinition</span></span> | <span data-ttu-id="df238-206">Выражение пути JSON для каждого столбца с его сопоставлением с настраиваемым именем столбца (начало в нижнем регистре).</span><span class="sxs-lookup"><span data-stu-id="df238-206">Specify the JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="df238-207">Это свойство поддерживается только в том случае, если данные копируются из JSON-файлов и данные можно извлечь из объекта или массива.</span><span class="sxs-lookup"><span data-stu-id="df238-207">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="df238-208">Для полей в области корневого объекта выражение пути должно начинаться с корня $. Для полей внутри массива, выбранных с помощью свойства `jsonNodeReference`, выражение должно начинаться с элемента массива.</span><span class="sxs-lookup"><span data-stu-id="df238-208">For fields under root object, start with root $; for fields inside the array chosen by `jsonNodeReference` property, start from the array element.</span></span> <span data-ttu-id="df238-209">Инструкции по настройке см. в разделе [Пример JsonFormat](#jsonformat-example).</span><span class="sxs-lookup"><span data-stu-id="df238-209">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span> | <span data-ttu-id="df238-210">Нет</span><span class="sxs-lookup"><span data-stu-id="df238-210">No</span></span> |
| <span data-ttu-id="df238-211">encodingName</span><span class="sxs-lookup"><span data-stu-id="df238-211">encodingName</span></span> |<span data-ttu-id="df238-212">Имя кодировки.</span><span class="sxs-lookup"><span data-stu-id="df238-212">Specify the encoding name.</span></span> <span data-ttu-id="df238-213">Список допустимых имен кодировок приведен в описании свойства [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) .</span><span class="sxs-lookup"><span data-stu-id="df238-213">For the list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="df238-214">Например: windows-1250 или shift_jis.</span><span class="sxs-lookup"><span data-stu-id="df238-214">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="df238-215">**По умолчанию** используется **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="df238-215">The **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="df238-216">Нет</span><span class="sxs-lookup"><span data-stu-id="df238-216">No</span></span> |
| <span data-ttu-id="df238-217">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="df238-217">nestingSeparator</span></span> |<span data-ttu-id="df238-218">Символ, используемый для разделения уровней вложенности.</span><span class="sxs-lookup"><span data-stu-id="df238-218">Character that is used to separate nesting levels.</span></span> <span data-ttu-id="df238-219">Значение по умолчанию — точка (.).</span><span class="sxs-lookup"><span data-stu-id="df238-219">The default value is '.' (dot).</span></span> |<span data-ttu-id="df238-220">Нет</span><span class="sxs-lookup"><span data-stu-id="df238-220">No</span></span> |

#### <a name="json-file-patterns"></a><span data-ttu-id="df238-221">Шаблоны файлов JSON</span><span class="sxs-lookup"><span data-stu-id="df238-221">JSON file patterns</span></span>

<span data-ttu-id="df238-222">Действие копирования может проанализировать приведенные ниже шаблоны JSON-файлов.</span><span class="sxs-lookup"><span data-stu-id="df238-222">Copy activity can parse below patterns of JSON files:</span></span>

- <span data-ttu-id="df238-223">**Тип 1: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="df238-223">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="df238-224">Каждый файл содержит один объект или несколько разделенных строками или объединенных объектов.</span><span class="sxs-lookup"><span data-stu-id="df238-224">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="df238-225">Если этот параметр выбран в выходном наборе данных, то в результате копирования будет создан JSON-файл, где каждый объект будет находиться в отдельной строке (файл с разделителем-строкой).</span><span class="sxs-lookup"><span data-stu-id="df238-225">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="df238-226">**Пример единого объекта JSON**</span><span class="sxs-lookup"><span data-stu-id="df238-226">**single object JSON example**</span></span>

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

    * <span data-ttu-id="df238-227">**Пример JSON-файла с разделителем-строкой**</span><span class="sxs-lookup"><span data-stu-id="df238-227">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="df238-228">**Пример объединенного JSON-файла**</span><span class="sxs-lookup"><span data-stu-id="df238-228">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="df238-229">**Тип 2: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="df238-229">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="df238-230">Каждый файл содержит массив объектов.</span><span class="sxs-lookup"><span data-stu-id="df238-230">Each file contains an array of objects.</span></span>

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

#### <a name="jsonformat-example"></a><span data-ttu-id="df238-231">Пример JsonFormat</span><span class="sxs-lookup"><span data-stu-id="df238-231">JsonFormat example</span></span>

<span data-ttu-id="df238-232">**Вариант 1. Копирование данных из JSON-файлов**</span><span class="sxs-lookup"><span data-stu-id="df238-232">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="df238-233">Ниже приведены два типа примеров копирования данных из JSON-файлов и общие примечания.</span><span class="sxs-lookup"><span data-stu-id="df238-233">See below two types of samples when copying data from JSON files, and the generic points to note:</span></span>

<span data-ttu-id="df238-234">**Пример 1. Извлечение данных из объекта и массива**</span><span class="sxs-lookup"><span data-stu-id="df238-234">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="df238-235">В этом примере предполагается, что один корневой объект JSON соответствует одной записи в таблице результатов.</span><span class="sxs-lookup"><span data-stu-id="df238-235">In this sample, you expect one root JSON object maps to single record in tabular result.</span></span> <span data-ttu-id="df238-236">Если у вас есть JSON-файл со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="df238-236">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="df238-237">и вы хотите скопировать это содержимое (посредством извлечения данных из объекта и массива) в таблицу SQL Azure в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="df238-237">and you want to copy it into an Azure SQL table in the following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="df238-238">id</span><span class="sxs-lookup"><span data-stu-id="df238-238">id</span></span> | <span data-ttu-id="df238-239">deviceType</span><span class="sxs-lookup"><span data-stu-id="df238-239">deviceType</span></span> | <span data-ttu-id="df238-240">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="df238-240">targetResourceType</span></span> | <span data-ttu-id="df238-241">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="df238-241">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="df238-242">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="df238-242">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="df238-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="df238-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="df238-244">PC</span><span class="sxs-lookup"><span data-stu-id="df238-244">PC</span></span> | <span data-ttu-id="df238-245">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="df238-245">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="df238-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="df238-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="df238-247">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="df238-247">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="df238-248">Входной набор данных с типом **JsonFormat** определяется следующим образом (частичное определение только соответствующих частей).</span><span class="sxs-lookup"><span data-stu-id="df238-248">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="df238-249">В частности:</span><span class="sxs-lookup"><span data-stu-id="df238-249">More specifically:</span></span>

- <span data-ttu-id="df238-250">Раздел `structure` определяет настраиваемые имена столбцов и соответствующие типы данных при преобразовании в табличные данные.</span><span class="sxs-lookup"><span data-stu-id="df238-250">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="df238-251">Этот раздел является **необязательным**, если вам не нужно сопоставлять столбцы.</span><span class="sxs-lookup"><span data-stu-id="df238-251">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="df238-252">Дополнительные сведения см. в статье [Указание определения структуры для прямоугольных наборов данных](#specifying-structure-definition-for-rectangular-datasets).</span><span class="sxs-lookup"><span data-stu-id="df238-252">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="df238-253">`jsonPathDefinition` указывает путь к файлу JSON для каждого столбца, который определяет, откуда следует извлекать данные.</span><span class="sxs-lookup"><span data-stu-id="df238-253">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="df238-254">Чтобы скопировать данные из массива, с помощью **array[X].property** можно извлечь значение нужного свойства из объекта X или с помощью **array[*].property** найти нужное значение в любом объекте с таким свойством.</span><span class="sxs-lookup"><span data-stu-id="df238-254">To copy data from array, you can use **array[x].property** to extract value of the given property from the xth object, or you can use **array[*].property** to find the value from any object containing such property.</span></span>

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

<span data-ttu-id="df238-255">**Пример 2. Применение нескольких объектов с одинаковым шаблоном из массива**</span><span class="sxs-lookup"><span data-stu-id="df238-255">**Sample 2: cross apply multiple objects with the same pattern from array**</span></span>

<span data-ttu-id="df238-256">В этом примере предполагается, что один корневой объект JSON будет преобразован в несколько записей в таблице результатов.</span><span class="sxs-lookup"><span data-stu-id="df238-256">In this sample, you expect to transform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="df238-257">Если у вас есть JSON-файл со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="df238-257">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="df238-258">И если вы хотите скопировать этот файл в таблицу Azure SQL в следующем формате путем сведения данных внутри массива и перекрестного соединения с общими сведениями о корневом объекте:</span><span class="sxs-lookup"><span data-stu-id="df238-258">and you want to copy it into an Azure SQL table in the following format, by flattening the data inside the array and cross join with the common root info:</span></span>

| <span data-ttu-id="df238-259">ordernumber</span><span class="sxs-lookup"><span data-stu-id="df238-259">ordernumber</span></span> | <span data-ttu-id="df238-260">orderdate</span><span class="sxs-lookup"><span data-stu-id="df238-260">orderdate</span></span> | <span data-ttu-id="df238-261">order_pd</span><span class="sxs-lookup"><span data-stu-id="df238-261">order_pd</span></span> | <span data-ttu-id="df238-262">order_price</span><span class="sxs-lookup"><span data-stu-id="df238-262">order_price</span></span> | <span data-ttu-id="df238-263">city</span><span class="sxs-lookup"><span data-stu-id="df238-263">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="df238-264">01</span><span class="sxs-lookup"><span data-stu-id="df238-264">01</span></span> | <span data-ttu-id="df238-265">20170122</span><span class="sxs-lookup"><span data-stu-id="df238-265">20170122</span></span> | <span data-ttu-id="df238-266">P1</span><span class="sxs-lookup"><span data-stu-id="df238-266">P1</span></span> | <span data-ttu-id="df238-267">23</span><span class="sxs-lookup"><span data-stu-id="df238-267">23</span></span> | <span data-ttu-id="df238-268">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="df238-268">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="df238-269">01</span><span class="sxs-lookup"><span data-stu-id="df238-269">01</span></span> | <span data-ttu-id="df238-270">20170122</span><span class="sxs-lookup"><span data-stu-id="df238-270">20170122</span></span> | <span data-ttu-id="df238-271">P2</span><span class="sxs-lookup"><span data-stu-id="df238-271">P2</span></span> | <span data-ttu-id="df238-272">13.</span><span class="sxs-lookup"><span data-stu-id="df238-272">13</span></span> | <span data-ttu-id="df238-273">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="df238-273">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="df238-274">01</span><span class="sxs-lookup"><span data-stu-id="df238-274">01</span></span> | <span data-ttu-id="df238-275">20170122</span><span class="sxs-lookup"><span data-stu-id="df238-275">20170122</span></span> | <span data-ttu-id="df238-276">P3</span><span class="sxs-lookup"><span data-stu-id="df238-276">P3</span></span> | <span data-ttu-id="df238-277">231</span><span class="sxs-lookup"><span data-stu-id="df238-277">231</span></span> | <span data-ttu-id="df238-278">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="df238-278">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="df238-279">Входной набор данных с типом **JsonFormat** определяется следующим образом (частичное определение только соответствующих частей).</span><span class="sxs-lookup"><span data-stu-id="df238-279">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="df238-280">В частности:</span><span class="sxs-lookup"><span data-stu-id="df238-280">More specifically:</span></span>

- <span data-ttu-id="df238-281">Раздел `structure` определяет настраиваемые имена столбцов и соответствующие типы данных при преобразовании в табличные данные.</span><span class="sxs-lookup"><span data-stu-id="df238-281">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="df238-282">Этот раздел является **необязательным**, если вам не нужно сопоставлять столбцы.</span><span class="sxs-lookup"><span data-stu-id="df238-282">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="df238-283">Дополнительные сведения см. в статье [Указание определения структуры для прямоугольных наборов данных](#specifying-structure-definition-for-rectangular-datasets).</span><span class="sxs-lookup"><span data-stu-id="df238-283">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="df238-284">Параметр `jsonNodeReference` обозначает итерацию и извлечение данных из объектов с одинаковым шаблоном в разделе orderlines **массива**.</span><span class="sxs-lookup"><span data-stu-id="df238-284">`jsonNodeReference` indicates to iterate and extract data from the objects with the same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="df238-285">`jsonPathDefinition` указывает путь к файлу JSON для каждого столбца, который определяет, откуда следует извлекать данные.</span><span class="sxs-lookup"><span data-stu-id="df238-285">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="df238-286">В этом примере значения ordernumber, orderdate и city находятся в корневом объекте. Путь JSON к этому объекту начинается с "$." а значения order_pd и order_price определяются с помощью пути, производного от элемента массива без "$.".</span><span class="sxs-lookup"><span data-stu-id="df238-286">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from the array element without "$.".</span></span>

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

<span data-ttu-id="df238-287">**Обратите внимание на следующие моменты.**</span><span class="sxs-lookup"><span data-stu-id="df238-287">**Note the following points:**</span></span>

* <span data-ttu-id="df238-288">Если параметры `structure` и `jsonPathDefinition` не определены в наборе данных фабрики данных, действие копирования обнаружит схему из первого объекта и выполнит сведение всего объекта.</span><span class="sxs-lookup"><span data-stu-id="df238-288">If the `structure` and `jsonPathDefinition` are not defined in the Data Factory dataset, the Copy Activity detects the schema from the first object and flatten the whole object.</span></span>
* <span data-ttu-id="df238-289">Если входной JSON-файл содержит массив, по умолчанию действие копирования преобразует все значение массива в строку.</span><span class="sxs-lookup"><span data-stu-id="df238-289">If the JSON input has an array, by default the Copy Activity converts the entire array value into a string.</span></span> <span data-ttu-id="df238-290">Вы можете извлечь данные из строки с помощью `jsonNodeReference` или `jsonPathDefinition`. Или можно пропустить строку, не указывая ее в `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="df238-290">You can choose to extract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="df238-291">Если на том же уровне существует повторяющиеся имена, то действие копирования выберет последнее из них.</span><span class="sxs-lookup"><span data-stu-id="df238-291">If there are duplicate names at the same level, the Copy Activity picks the last one.</span></span>
* <span data-ttu-id="df238-292">В именах свойств учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="df238-292">Property names are case-sensitive.</span></span> <span data-ttu-id="df238-293">Два свойства с одинаковым именем, но в разных регистрах, рассматриваются как два отдельных свойства.</span><span class="sxs-lookup"><span data-stu-id="df238-293">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="df238-294">**Вариант 2. Запись данных в JSON-файл**</span><span class="sxs-lookup"><span data-stu-id="df238-294">**Case 2: Writing data to JSON file**</span></span>

<span data-ttu-id="df238-295">Если в базе данных SQL есть такая таблица:</span><span class="sxs-lookup"><span data-stu-id="df238-295">If you have below table in SQL Database:</span></span>

| <span data-ttu-id="df238-296">id</span><span class="sxs-lookup"><span data-stu-id="df238-296">id</span></span> | <span data-ttu-id="df238-297">order_date</span><span class="sxs-lookup"><span data-stu-id="df238-297">order_date</span></span> | <span data-ttu-id="df238-298">order_price</span><span class="sxs-lookup"><span data-stu-id="df238-298">order_price</span></span> | <span data-ttu-id="df238-299">order_by</span><span class="sxs-lookup"><span data-stu-id="df238-299">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="df238-300">1</span><span class="sxs-lookup"><span data-stu-id="df238-300">1</span></span> | <span data-ttu-id="df238-301">20170119</span><span class="sxs-lookup"><span data-stu-id="df238-301">20170119</span></span> | <span data-ttu-id="df238-302">2000</span><span class="sxs-lookup"><span data-stu-id="df238-302">2000</span></span> | <span data-ttu-id="df238-303">David</span><span class="sxs-lookup"><span data-stu-id="df238-303">David</span></span> |
| <span data-ttu-id="df238-304">2</span><span class="sxs-lookup"><span data-stu-id="df238-304">2</span></span> | <span data-ttu-id="df238-305">20170120</span><span class="sxs-lookup"><span data-stu-id="df238-305">20170120</span></span> | <span data-ttu-id="df238-306">3500</span><span class="sxs-lookup"><span data-stu-id="df238-306">3500</span></span> | <span data-ttu-id="df238-307">Patrick</span><span class="sxs-lookup"><span data-stu-id="df238-307">Patrick</span></span> |
| <span data-ttu-id="df238-308">3</span><span class="sxs-lookup"><span data-stu-id="df238-308">3</span></span> | <span data-ttu-id="df238-309">20170121</span><span class="sxs-lookup"><span data-stu-id="df238-309">20170121</span></span> | <span data-ttu-id="df238-310">4000</span><span class="sxs-lookup"><span data-stu-id="df238-310">4000</span></span> | <span data-ttu-id="df238-311">Jason</span><span class="sxs-lookup"><span data-stu-id="df238-311">Jason</span></span> |

<span data-ttu-id="df238-312">и для каждой записи вы предполагаете запись в объект JSON в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="df238-312">and for each record, you expect to write to a JSON object in below format:</span></span>
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

<span data-ttu-id="df238-313">Выходной набор данных с типом **JsonFormat** определяется следующим образом (частичное определение только соответствующих частей).</span><span class="sxs-lookup"><span data-stu-id="df238-313">The output dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="df238-314">В частности, раздел `structure` определяет настраиваемые имена свойств в конечном файле. Для определения уровня вложенности от имен будет использоваться разделитель вложенности `nestingSeparator` (по умолчанию — точка (.)).</span><span class="sxs-lookup"><span data-stu-id="df238-314">More specifically, `structure` section defines the customized property names in destination file, `nestingSeparator` (default is ".") will be used to identify the nest layer from the name.</span></span> <span data-ttu-id="df238-315">Этот раздел является **необязательным**, если вы не собираетесь изменять исходное имя свойства или вкладывать свойства.</span><span class="sxs-lookup"><span data-stu-id="df238-315">This section is **optional** unless you want to change the property name comparing with source column name, or nest some of the properties.</span></span>

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

### <a name="specifying-avroformat"></a><span data-ttu-id="df238-316">Определение AvroFormat</span><span class="sxs-lookup"><span data-stu-id="df238-316">Specifying AvroFormat</span></span>
<span data-ttu-id="df238-317">Если требуется проанализировать файлы Avro или записать данные в формате Avro, установите для свойства `format` `type` значение **AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="df238-317">If you want to parse the Avro files or write the data in Avro format, set the `format` `type` property to **AvroFormat**.</span></span> <span data-ttu-id="df238-318">Вам не нужно указывать какие-либо свойства в подразделе Format раздела typeProperties.</span><span class="sxs-lookup"><span data-stu-id="df238-318">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="df238-319">Пример:</span><span class="sxs-lookup"><span data-stu-id="df238-319">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="df238-320">Сведения об использовании формата Avro в таблице Hive см. в [руководстве по Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="df238-320">To use Avro format in a Hive table, you can refer to [Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="df238-321">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="df238-321">Note the following points:</span></span>  

* <span data-ttu-id="df238-322">[Сложные типы данных](http://avro.apache.org/docs/current/spec.html#schema_complex) (записи, перечисления, массивы, сопоставления, объединения и фиксированные данные) не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="df238-322">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions and fixed).</span></span>

### <a name="specifying-orcformat"></a><span data-ttu-id="df238-323">Указание OrcFormat</span><span class="sxs-lookup"><span data-stu-id="df238-323">Specifying OrcFormat</span></span>
<span data-ttu-id="df238-324">Если требуется проанализировать ORC-файлы или записать данные в формате ORC, установите для свойства `format` `type` значение **OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="df238-324">If you want to parse the ORC files or write the data in ORC format, set the `format` `type` property to **OrcFormat**.</span></span> <span data-ttu-id="df238-325">Вам не нужно указывать какие-либо свойства в подразделе Format раздела typeProperties.</span><span class="sxs-lookup"><span data-stu-id="df238-325">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="df238-326">Пример:</span><span class="sxs-lookup"><span data-stu-id="df238-326">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="df238-327">Если вы не копируете ORC-файлов **как есть** между локальным и облачным хранилищами данных, то на компьютере шлюза необходимо установить 8 JRE (среду выполнения Java).</span><span class="sxs-lookup"><span data-stu-id="df238-327">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="df238-328">Для 64-разрядного шлюза требуется 64-разрядная версия JRE, а для 32-разрядного шлюза — 32-разрядная версия JRE.</span><span class="sxs-lookup"><span data-stu-id="df238-328">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="df238-329">Обе эти версии доступны [здесь](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="df238-329">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="df238-330">Выберите ту, что вам подходит.</span><span class="sxs-lookup"><span data-stu-id="df238-330">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="df238-331">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="df238-331">Note the following points:</span></span>

* <span data-ttu-id="df238-332">Данные сложных типов (STRUCT, MAP, LIST, UNION) не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="df238-332">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="df238-333">Для ORC-файлов используется три [параметра сжатия](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB и SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="df238-333">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="df238-334">Фабрика данных поддерживает чтение данных из ORC-файла в любом из этих форматов.</span><span class="sxs-lookup"><span data-stu-id="df238-334">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="df238-335">Для чтения данных используется кодек сжатия из метаданных.</span><span class="sxs-lookup"><span data-stu-id="df238-335">It uses the compression codec is in the metadata to read the data.</span></span> <span data-ttu-id="df238-336">Однако при записи в ORC-файл фабрика данных по умолчанию выбирает ZLIB.</span><span class="sxs-lookup"><span data-stu-id="df238-336">However, when writing to an ORC file, Data Factory chooses ZLIB, which is the default for ORC.</span></span> <span data-ttu-id="df238-337">В настоящее время изменить это поведение нельзя.</span><span class="sxs-lookup"><span data-stu-id="df238-337">Currently, there is no option to override this behavior.</span></span>

### <a name="specifying-parquetformat"></a><span data-ttu-id="df238-338">Указание ParquetFormat</span><span class="sxs-lookup"><span data-stu-id="df238-338">Specifying ParquetFormat</span></span>
<span data-ttu-id="df238-339">Если требуется проанализировать файлы Parquet или записать данные в формате Parquet, установите для свойства `format` `type` значение **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="df238-339">If you want to parse the Parquet files or write the data in Parquet format, set the `format` `type` property to **ParquetFormat**.</span></span> <span data-ttu-id="df238-340">Вам не нужно указывать какие-либо свойства в подразделе Format раздела typeProperties.</span><span class="sxs-lookup"><span data-stu-id="df238-340">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="df238-341">Пример:</span><span class="sxs-lookup"><span data-stu-id="df238-341">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="df238-342">Если вы не копируете Parquet-файлы **как есть** между локальным и облачным хранилищами данных, то на компьютере шлюза необходимо установить JRE 8 (среду выполнения Java).</span><span class="sxs-lookup"><span data-stu-id="df238-342">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="df238-343">Для 64-разрядного шлюза требуется 64-разрядная версия JRE, а для 32-разрядного шлюза — 32-разрядная версия JRE.</span><span class="sxs-lookup"><span data-stu-id="df238-343">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="df238-344">Обе эти версии доступны [здесь](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="df238-344">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="df238-345">Выберите ту, что вам подходит.</span><span class="sxs-lookup"><span data-stu-id="df238-345">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="df238-346">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="df238-346">Note the following points:</span></span>

* <span data-ttu-id="df238-347">Данные сложных типов (MAP, LIST) не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="df238-347">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="df238-348">Parquet-файл имеет следующие варианты сжатия: NONE, SNAPPY, GZIP и LZO.</span><span class="sxs-lookup"><span data-stu-id="df238-348">Parquet file has the following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="df238-349">Фабрика данных поддерживает чтение данных из ORC-файла в любом из этих форматов.</span><span class="sxs-lookup"><span data-stu-id="df238-349">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="df238-350">Для чтения данных используется кодек сжатия из метаданных.</span><span class="sxs-lookup"><span data-stu-id="df238-350">It uses the compression codec in the metadata to read the data.</span></span> <span data-ttu-id="df238-351">Однако при записи в Parquet-файл фабрика данных по умолчанию выбирает SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="df238-351">However, when writing to a Parquet file, Data Factory chooses SNAPPY, which is the default for Parquet format.</span></span> <span data-ttu-id="df238-352">В настоящее время изменить это поведение нельзя.</span><span class="sxs-lookup"><span data-stu-id="df238-352">Currently, there is no option to override this behavior.</span></span>
