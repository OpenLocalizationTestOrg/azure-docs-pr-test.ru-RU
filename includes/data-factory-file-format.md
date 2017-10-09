## <a name="specifying-formats"></a><span data-ttu-id="9d2dd-101">Указание форматов</span><span class="sxs-lookup"><span data-stu-id="9d2dd-101">Specifying formats</span></span>
<span data-ttu-id="9d2dd-102">Фабрика данных Azure поддерживает следующие типы формата hello:</span><span class="sxs-lookup"><span data-stu-id="9d2dd-102">Azure Data Factory supports hello following format types:</span></span>

* <span data-ttu-id="9d2dd-103">[текстовый формат](#specifying-textformat);</span><span class="sxs-lookup"><span data-stu-id="9d2dd-103">[Text Format](#specifying-textformat)</span></span>
* <span data-ttu-id="9d2dd-104">[формат JSON](#specifying-jsonformat);</span><span class="sxs-lookup"><span data-stu-id="9d2dd-104">[JSON Format](#specifying-jsonformat)</span></span>
* <span data-ttu-id="9d2dd-105">[формат Avro](#specifying-avroformat);</span><span class="sxs-lookup"><span data-stu-id="9d2dd-105">[Avro Format](#specifying-avroformat)</span></span>
* <span data-ttu-id="9d2dd-106">[формат ORC](#specifying-orcformat);</span><span class="sxs-lookup"><span data-stu-id="9d2dd-106">[ORC Format](#specifying-orcformat)</span></span>
* <span data-ttu-id="9d2dd-107">[формат PARQUET](#specifying-parquetformat).</span><span class="sxs-lookup"><span data-stu-id="9d2dd-107">[Parquet Format](#specifying-parquetformat)</span></span>

### <a name="specifying-textformat"></a><span data-ttu-id="9d2dd-108">Определение TextFormat</span><span class="sxs-lookup"><span data-stu-id="9d2dd-108">Specifying TextFormat</span></span>
<span data-ttu-id="9d2dd-109">Если требуется tooparse hello текстовые файлы или записи данных hello в текстовом формате, задайте hello `format` `type` свойство слишком**TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-109">If you want tooparse hello text files or write hello data in text format, set hello `format` `type` property too**TextFormat**.</span></span> <span data-ttu-id="9d2dd-110">Можно также указать следующие hello **необязательно** свойства в hello `format` раздела.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-110">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="9d2dd-111">В разделе [примере TextFormat](#textformat-example) раздел, в tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-111">See [TextFormat example](#textformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="9d2dd-112">Свойство</span><span class="sxs-lookup"><span data-stu-id="9d2dd-112">Property</span></span> | <span data-ttu-id="9d2dd-113">Описание</span><span class="sxs-lookup"><span data-stu-id="9d2dd-113">Description</span></span> | <span data-ttu-id="9d2dd-114">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="9d2dd-114">Allowed values</span></span> | <span data-ttu-id="9d2dd-115">Обязательно</span><span class="sxs-lookup"><span data-stu-id="9d2dd-115">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9d2dd-116">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="9d2dd-116">columnDelimiter</span></span> |<span data-ttu-id="9d2dd-117">символ Hello использовать tooseparate столбцов в файле.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-117">hello character used tooseparate columns in a file.</span></span> <span data-ttu-id="9d2dd-118">Можно рассмотреть возможность toouse редких непечатаемые char, вероятно, не существует в данных: например, укажите «\u0001» который представляет запуск из заголовка (SOH).</span><span class="sxs-lookup"><span data-stu-id="9d2dd-118">You can consider toouse a rare unprintable char which not likely exists in your data: e.g. specify "\u0001" which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="9d2dd-119">Допускается только один знак.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-119">Only one character is allowed.</span></span> <span data-ttu-id="9d2dd-120">Hello **по умолчанию** значение **запятая (,)**.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-120">hello **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="9d2dd-121">toouse символ Юникода ссылаться слишком[символов Юникода](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello соответствующий код для него.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-121">toouse an Unicode character, refer too[Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello corresponding code for it.</span></span> |<span data-ttu-id="9d2dd-122">Нет</span><span class="sxs-lookup"><span data-stu-id="9d2dd-122">No</span></span> |
| <span data-ttu-id="9d2dd-123">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="9d2dd-123">rowDelimiter</span></span> |<span data-ttu-id="9d2dd-124">символ Hello использовать tooseparate строк в файле.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-124">hello character used tooseparate rows in a file.</span></span> |<span data-ttu-id="9d2dd-125">Допускается только один знак.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-125">Only one character is allowed.</span></span> <span data-ttu-id="9d2dd-126">Hello **по умолчанию** значение представляет собой любой hello последующих значений на чтение: **[«\r\n», «\r», «\n»]** и **«\r\n»** при записи.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-126">hello **default** value is any of hello following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="9d2dd-127">Нет</span><span class="sxs-lookup"><span data-stu-id="9d2dd-127">No</span></span> |
| <span data-ttu-id="9d2dd-128">escapeChar</span><span class="sxs-lookup"><span data-stu-id="9d2dd-128">escapeChar</span></span> |<span data-ttu-id="9d2dd-129">специальный символ Hello использовать tooescape разделитель столбцов в hello содержимое входного файла.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-129">hello special character used tooescape a column delimiter in hello content of input file.</span></span> <br/><br/><span data-ttu-id="9d2dd-130">Для таблицы нельзя указать и escapeChar, и quoteChar.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-130">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="9d2dd-131">Допускается только один знак.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-131">Only one character is allowed.</span></span> <span data-ttu-id="9d2dd-132">Значение по умолчанию отсутствует.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-132">No default value.</span></span> <br/><br/><span data-ttu-id="9d2dd-133">Пример: при наличии запятая («,») как разделитель столбцов hello, но его необходимо toohave hello запятая в тексте hello (пример: «Hello, world»), можно определить как hello escape-символ «$» и использовать строку «Hello$, world» в источнике hello.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-133">Example: if you have comma (',') as hello column delimiter but you want toohave hello comma character in hello text (example: "Hello, world"), you can define ‘$’ as hello escape character and use string "Hello$, world" in hello source.</span></span> |<span data-ttu-id="9d2dd-134">Нет</span><span class="sxs-lookup"><span data-stu-id="9d2dd-134">No</span></span> |
| <span data-ttu-id="9d2dd-135">quoteChar</span><span class="sxs-lookup"><span data-stu-id="9d2dd-135">quoteChar</span></span> |<span data-ttu-id="9d2dd-136">использовать знак Hello tooquote строковое значение.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-136">hello character used tooquote a string value.</span></span> <span data-ttu-id="9d2dd-137">Hello разделители столбцов и строк внутри кавычек hello будет рассматриваться как часть hello строковое значение.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-137">hello column and row delimiters inside hello quote characters would be treated as part of hello string value.</span></span> <span data-ttu-id="9d2dd-138">Это свойство является применимо tooboth ввода и вывода наборов данных.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-138">This property is applicable tooboth input and output datasets.</span></span><br/><br/><span data-ttu-id="9d2dd-139">Для таблицы нельзя указать и escapeChar, и quoteChar.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-139">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="9d2dd-140">Допускается только один знак.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-140">Only one character is allowed.</span></span> <span data-ttu-id="9d2dd-141">Значение по умолчанию отсутствует.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-141">No default value.</span></span> <br/><br/><span data-ttu-id="9d2dd-142">Например, если у вас есть запятая («,») как разделитель столбцов hello, но его необходимо toohave запятая в тексте hello (пример: < Hello, world >), можно определить» (двойная кавычка) как hello знак кавычек, чтобы использовать строку hello «Hello, world» в источнике hello.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-142">For example, if you have comma (',') as hello column delimiter but you want toohave comma character in hello text (example: <Hello, world>), you can define " (double quote) as hello quote character and use hello string "Hello, world" in hello source.</span></span> |<span data-ttu-id="9d2dd-143">Нет</span><span class="sxs-lookup"><span data-stu-id="9d2dd-143">No</span></span> |
| <span data-ttu-id="9d2dd-144">nullValue</span><span class="sxs-lookup"><span data-stu-id="9d2dd-144">nullValue</span></span> |<span data-ttu-id="9d2dd-145">Один или несколько символов используется toorepresent значение null.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-145">One or more characters used toorepresent a null value.</span></span> |<span data-ttu-id="9d2dd-146">Один или несколько знаков.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-146">One or more characters.</span></span> <span data-ttu-id="9d2dd-147">Hello **по умолчанию** значения **«\N» и «NULL»** для чтения и **«\N»** при записи.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-147">hello **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="9d2dd-148">Нет</span><span class="sxs-lookup"><span data-stu-id="9d2dd-148">No</span></span> |
| <span data-ttu-id="9d2dd-149">encodingName</span><span class="sxs-lookup"><span data-stu-id="9d2dd-149">encodingName</span></span> |<span data-ttu-id="9d2dd-150">Укажите название кодировки hello.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-150">Specify hello encoding name.</span></span> |<span data-ttu-id="9d2dd-151">Допустимое имя кодировки.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-151">A valid encoding name.</span></span> <span data-ttu-id="9d2dd-152">Ознакомьтесь с описанием свойства [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d2dd-152">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="9d2dd-153">Пример: windows-1250 или shift_jis.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-153">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="9d2dd-154">Hello **по умолчанию** значение **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-154">hello **default** value is **UTF-8**.</span></span> |<span data-ttu-id="9d2dd-155">Нет</span><span class="sxs-lookup"><span data-stu-id="9d2dd-155">No</span></span> |
| <span data-ttu-id="9d2dd-156">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="9d2dd-156">firstRowAsHeader</span></span> |<span data-ttu-id="9d2dd-157">Указывает, является ли tooconsider hello первую строку как заголовок.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-157">Specifies whether tooconsider hello first row as a header.</span></span> <span data-ttu-id="9d2dd-158">Фабрика данных считывает первую строку входного набора данных как заголовок.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-158">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="9d2dd-159">Фабрика данных записывает первую строку как заголовок в выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-159">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="9d2dd-160">Примеры сценариев см. в разделе [Сценарии использования `firstRowAsHeader` и `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount).</span><span class="sxs-lookup"><span data-stu-id="9d2dd-160">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="9d2dd-161">Да</span><span class="sxs-lookup"><span data-stu-id="9d2dd-161">True</span></span><br/><span data-ttu-id="9d2dd-162">**False (по умолчанию)**</span><span class="sxs-lookup"><span data-stu-id="9d2dd-162">**False (default)**</span></span> |<span data-ttu-id="9d2dd-163">Нет</span><span class="sxs-lookup"><span data-stu-id="9d2dd-163">No</span></span> |
| <span data-ttu-id="9d2dd-164">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="9d2dd-164">skipLineCount</span></span> |<span data-ttu-id="9d2dd-165">Указывает номер hello tooskip строк, при считывании данных из входных файлов.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-165">Indicates hello number of rows tooskip when reading data from input files.</span></span> <span data-ttu-id="9d2dd-166">Если указаны skipLineCount и firstRowAsHeader, hello строки пропускаются сначала и затем сведения о заголовке hello считывается из входного файла hello.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-166">If both skipLineCount and firstRowAsHeader are specified, hello lines are skipped first and then hello header information is read from hello input file.</span></span> <br/><br/><span data-ttu-id="9d2dd-167">Примеры сценариев см. в разделе [Сценарии использования `firstRowAsHeader` и `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount).</span><span class="sxs-lookup"><span data-stu-id="9d2dd-167">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="9d2dd-168">Целое число </span><span class="sxs-lookup"><span data-stu-id="9d2dd-168">Integer</span></span> |<span data-ttu-id="9d2dd-169">Нет</span><span class="sxs-lookup"><span data-stu-id="9d2dd-169">No</span></span> |
| <span data-ttu-id="9d2dd-170">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="9d2dd-170">treatEmptyAsNull</span></span> |<span data-ttu-id="9d2dd-171">Указывает, является ли tootreat null или пустую строку как строку null значения при считывании данных из входного файла.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-171">Specifies whether tootreat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="9d2dd-172">**True (по умолчанию)**</span><span class="sxs-lookup"><span data-stu-id="9d2dd-172">**True (default)**</span></span><br/><span data-ttu-id="9d2dd-173">Ложь</span><span class="sxs-lookup"><span data-stu-id="9d2dd-173">False</span></span> |<span data-ttu-id="9d2dd-174">Нет</span><span class="sxs-lookup"><span data-stu-id="9d2dd-174">No</span></span> |

#### <a name="textformat-example"></a><span data-ttu-id="9d2dd-175">Пример TextFormat</span><span class="sxs-lookup"><span data-stu-id="9d2dd-175">TextFormat example</span></span>
<span data-ttu-id="9d2dd-176">Hello следующий пример показывает некоторые свойства формата hello для TextFormat.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-176">hello following sample shows some of hello format properties for TextFormat.</span></span>

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

<span data-ttu-id="9d2dd-177">toouse `escapeChar` вместо `quoteChar`, замените строку hello с `quoteChar` с hello использовать escapeChar следующие:</span><span class="sxs-lookup"><span data-stu-id="9d2dd-177">toouse an `escapeChar` instead of `quoteChar`, replace hello line with `quoteChar` with hello following escapeChar:</span></span>

```json
"escapeChar": "$",
```

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="9d2dd-178">Сценарии использования firstRowAsHeader и skipLineCount</span><span class="sxs-lookup"><span data-stu-id="9d2dd-178">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="9d2dd-179">Копирование из файла источника, не являющимся файлами tooa и хотите tooadd заголовка строки, содержащей hello схемы метаданных (например: SQL-схема).</span><span class="sxs-lookup"><span data-stu-id="9d2dd-179">You are copying from a non-file source tooa text file and would like tooadd a header line containing hello schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="9d2dd-180">Укажите `firstRowAsHeader` как true в hello выходной набор данных для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-180">Specify `firstRowAsHeader` as true in hello output dataset for this scenario.</span></span>
* <span data-ttu-id="9d2dd-181">Копирование из текстового файла, содержащего приемник не являющимся файлами tooa заголовка строки и хотите toodrop, строка.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-181">You are copying from a text file containing a header line tooa non-file sink and would like toodrop that line.</span></span> <span data-ttu-id="9d2dd-182">Укажите `firstRowAsHeader` как true во входном наборе данных hello.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-182">Specify `firstRowAsHeader` as true in hello input dataset.</span></span>
* <span data-ttu-id="9d2dd-183">Копирование из текстового файла и хотите tooskip несколько строк в начале hello, которые не содержат данных или заголовка информации.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-183">You are copying from a text file and want tooskip a few lines at hello beginning that contain no data or header information.</span></span> <span data-ttu-id="9d2dd-184">Укажите `skipLineCount` tooindicate hello число строк toobe пропущено.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-184">Specify `skipLineCount` tooindicate hello number of lines toobe skipped.</span></span> <span data-ttu-id="9d2dd-185">Если hello остальной части файла hello содержит строку заголовка, можно указать `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-185">If hello rest of hello file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="9d2dd-186">Если оба `skipLineCount` и `firstRowAsHeader` указаны, hello строки пропускаются сначала и затем сведения о заголовке hello считывается из входного файла hello</span><span class="sxs-lookup"><span data-stu-id="9d2dd-186">If both `skipLineCount` and `firstRowAsHeader` are specified, hello lines are skipped first and then hello header information is read from hello input file</span></span>

### <a name="specifying-jsonformat"></a><span data-ttu-id="9d2dd-187">Указание JsonFormat</span><span class="sxs-lookup"><span data-stu-id="9d2dd-187">Specifying JsonFormat</span></span>
<span data-ttu-id="9d2dd-188">слишком**импорта и экспорта файлов JSON в качестве-в / из базы данных Azure Cosmos**, в разделе [документов JSON импорта и экспорта](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) раздела hello Azure Cosmos DB соединителя с подробными сведениями.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-188">too**import/export JSON files as-is into/from Azure Cosmos DB**, see [Import/export JSON documents](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) section in hello Azure Cosmos DB connector with details.</span></span>

<span data-ttu-id="9d2dd-189">Если требуется tooparse hello JSON-файлов или запись данных hello в формате JSON, задайте hello `format` `type` свойство слишком**JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-189">If you want tooparse hello JSON files or write hello data in JSON format, set hello `format` `type` property too**JsonFormat**.</span></span> <span data-ttu-id="9d2dd-190">Можно также указать следующие hello **необязательно** свойства в hello `format` раздела.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-190">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="9d2dd-191">В разделе [JsonFormat пример](#jsonformat-example) раздел, в tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-191">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="9d2dd-192">Свойство</span><span class="sxs-lookup"><span data-stu-id="9d2dd-192">Property</span></span> | <span data-ttu-id="9d2dd-193">Описание</span><span class="sxs-lookup"><span data-stu-id="9d2dd-193">Description</span></span> | <span data-ttu-id="9d2dd-194">Обязательно</span><span class="sxs-lookup"><span data-stu-id="9d2dd-194">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9d2dd-195">filePattern</span><span class="sxs-lookup"><span data-stu-id="9d2dd-195">filePattern</span></span> |<span data-ttu-id="9d2dd-196">Укажите шаблон hello данных, хранящихся в каждом файле JSON.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-196">Indicate hello pattern of data stored in each JSON file.</span></span> <span data-ttu-id="9d2dd-197">Допустимые значения: **setOfObjects** и **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-197">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="9d2dd-198">Hello **по умолчанию** значение **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-198">hello **default** value is **setOfObjects**.</span></span> <span data-ttu-id="9d2dd-199">Подробные сведения об этих шаблонах см. в разделе [Шаблоны файлов JSON](#json-file-patterns).</span><span class="sxs-lookup"><span data-stu-id="9d2dd-199">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="9d2dd-200">Нет</span><span class="sxs-lookup"><span data-stu-id="9d2dd-200">No</span></span> |
| <span data-ttu-id="9d2dd-201">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="9d2dd-201">jsonNodeReference</span></span> | <span data-ttu-id="9d2dd-202">Tooiterate и извлечения данных из объектов hello в массив полей с hello же шаблон, укажите путь к JSON hello этого массива.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-202">If you want tooiterate and extract data from hello objects inside an array field with hello same pattern, specify hello JSON path of that array.</span></span> <span data-ttu-id="9d2dd-203">Это свойство поддерживается только в том случае, если данные копируются из JSON-файлов.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-203">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="9d2dd-204">Нет</span><span class="sxs-lookup"><span data-stu-id="9d2dd-204">No</span></span> |
| <span data-ttu-id="9d2dd-205">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="9d2dd-205">jsonPathDefinition</span></span> | <span data-ttu-id="9d2dd-206">Укажите hello выражения пути JSON для каждого сопоставления столбцов с именем пользовательские столбца (начало строчных).</span><span class="sxs-lookup"><span data-stu-id="9d2dd-206">Specify hello JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="9d2dd-207">Это свойство поддерживается только в том случае, если данные копируются из JSON-файлов и данные можно извлечь из объекта или массива.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-207">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="9d2dd-208">Для поля в корневой объект, начинаться с $ корневой; для полей внутри массива hello выбирается программой `jsonNodeReference` свойство начинаются с Привет элемента массива.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-208">For fields under root object, start with root $; for fields inside hello array chosen by `jsonNodeReference` property, start from hello array element.</span></span> <span data-ttu-id="9d2dd-209">В разделе [JsonFormat пример](#jsonformat-example) раздел, в tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-209">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span> | <span data-ttu-id="9d2dd-210">Нет</span><span class="sxs-lookup"><span data-stu-id="9d2dd-210">No</span></span> |
| <span data-ttu-id="9d2dd-211">encodingName</span><span class="sxs-lookup"><span data-stu-id="9d2dd-211">encodingName</span></span> |<span data-ttu-id="9d2dd-212">Укажите название кодировки hello.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-212">Specify hello encoding name.</span></span> <span data-ttu-id="9d2dd-213">Hello список допустимых названий кодировок см. в разделе: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) свойство.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-213">For hello list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="9d2dd-214">Например: windows-1250 или shift_jis.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-214">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="9d2dd-215">Hello **по умолчанию** значение: **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-215">hello **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="9d2dd-216">Нет</span><span class="sxs-lookup"><span data-stu-id="9d2dd-216">No</span></span> |
| <span data-ttu-id="9d2dd-217">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="9d2dd-217">nestingSeparator</span></span> |<span data-ttu-id="9d2dd-218">Символ, используемые tooseparate уровней вложения.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-218">Character that is used tooseparate nesting levels.</span></span> <span data-ttu-id="9d2dd-219">значение по умолчанию Hello "." (точка).</span><span class="sxs-lookup"><span data-stu-id="9d2dd-219">hello default value is '.' (dot).</span></span> |<span data-ttu-id="9d2dd-220">Нет</span><span class="sxs-lookup"><span data-stu-id="9d2dd-220">No</span></span> |

#### <a name="json-file-patterns"></a><span data-ttu-id="9d2dd-221">Шаблоны файлов JSON</span><span class="sxs-lookup"><span data-stu-id="9d2dd-221">JSON file patterns</span></span>

<span data-ttu-id="9d2dd-222">Действие копирования может проанализировать приведенные ниже шаблоны JSON-файлов.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-222">Copy activity can parse below patterns of JSON files:</span></span>

- <span data-ttu-id="9d2dd-223">**Тип 1: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="9d2dd-223">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="9d2dd-224">Каждый файл содержит один объект или несколько разделенных строками или объединенных объектов.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-224">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="9d2dd-225">Если этот параметр выбран в выходном наборе данных, то в результате копирования будет создан JSON-файл, где каждый объект будет находиться в отдельной строке (файл с разделителем-строкой).</span><span class="sxs-lookup"><span data-stu-id="9d2dd-225">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="9d2dd-226">**Пример единого объекта JSON**</span><span class="sxs-lookup"><span data-stu-id="9d2dd-226">**single object JSON example**</span></span>

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

    * <span data-ttu-id="9d2dd-227">**Пример JSON-файла с разделителем-строкой**</span><span class="sxs-lookup"><span data-stu-id="9d2dd-227">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="9d2dd-228">**Пример объединенного JSON-файла**</span><span class="sxs-lookup"><span data-stu-id="9d2dd-228">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="9d2dd-229">**Тип 2: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="9d2dd-229">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="9d2dd-230">Каждый файл содержит массив объектов.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-230">Each file contains an array of objects.</span></span>

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

#### <a name="jsonformat-example"></a><span data-ttu-id="9d2dd-231">Пример JsonFormat</span><span class="sxs-lookup"><span data-stu-id="9d2dd-231">JsonFormat example</span></span>

<span data-ttu-id="9d2dd-232">**Вариант 1. Копирование данных из JSON-файлов**</span><span class="sxs-lookup"><span data-stu-id="9d2dd-232">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="9d2dd-233">См. ниже два вида образцы при копировании данных из JSON-файлов и hello toonote универсальных точек:</span><span class="sxs-lookup"><span data-stu-id="9d2dd-233">See below two types of samples when copying data from JSON files, and hello generic points toonote:</span></span>

<span data-ttu-id="9d2dd-234">**Пример 1. Извлечение данных из объекта и массива**</span><span class="sxs-lookup"><span data-stu-id="9d2dd-234">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="9d2dd-235">В этом примере предполагается, что один корневой объект JSON, отображающий toosingle записи в табличный результат.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-235">In this sample, you expect one root JSON object maps toosingle record in tabular result.</span></span> <span data-ttu-id="9d2dd-236">Если имеется файл JSON с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="9d2dd-236">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="9d2dd-237">и необходимо отформатировать его в таблице Azure SQL в следующих hello, путем извлечения данных из объектов и массив toocopy:</span><span class="sxs-lookup"><span data-stu-id="9d2dd-237">and you want toocopy it into an Azure SQL table in hello following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="9d2dd-238">id</span><span class="sxs-lookup"><span data-stu-id="9d2dd-238">id</span></span> | <span data-ttu-id="9d2dd-239">deviceType</span><span class="sxs-lookup"><span data-stu-id="9d2dd-239">deviceType</span></span> | <span data-ttu-id="9d2dd-240">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="9d2dd-240">targetResourceType</span></span> | <span data-ttu-id="9d2dd-241">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="9d2dd-241">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="9d2dd-242">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="9d2dd-242">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="9d2dd-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="9d2dd-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="9d2dd-244">PC</span><span class="sxs-lookup"><span data-stu-id="9d2dd-244">PC</span></span> | <span data-ttu-id="9d2dd-245">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="9d2dd-245">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="9d2dd-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="9d2dd-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="9d2dd-247">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="9d2dd-247">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="9d2dd-248">Hello входного набора данных с **JsonFormat** тип определяется следующим образом: (частичное определение с частями hello применимо).</span><span class="sxs-lookup"><span data-stu-id="9d2dd-248">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="9d2dd-249">В частности:</span><span class="sxs-lookup"><span data-stu-id="9d2dd-249">More specifically:</span></span>

- <span data-ttu-id="9d2dd-250">`structure`раздел определяет имена столбцов настроенные hello и hello соответствующие типы данных во время преобразования данных tootabular.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-250">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="9d2dd-251">Этот раздел представляет **необязательно** при отсутствии необходимости toodo сопоставления столбцов.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-251">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="9d2dd-252">Дополнительные сведения см. в статье [Указание определения структуры для прямоугольных наборов данных](#specifying-structure-definition-for-rectangular-datasets).</span><span class="sxs-lookup"><span data-stu-id="9d2dd-252">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="9d2dd-253">`jsonPathDefinition`Указывает путь hello JSON для каждого столбца, указывающее, где tooextract hello данные из.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-253">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="9d2dd-254">toocopy данные из массива, можно использовать **.property массива [x]** tooextract значение hello заданного свойства из объекта xth hello, или же можно использовать  **массива [*] .property** toofind значение Hello из любого объекта, содержащего такого свойства.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-254">toocopy data from array, you can use **array[x].property** tooextract value of hello given property from hello xth object, or you can use **array[*].property** toofind hello value from any object containing such property.</span></span>

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

<span data-ttu-id="9d2dd-255">**Пример 2: кросс-примените несколько объектов с hello же шаблон из массива**</span><span class="sxs-lookup"><span data-stu-id="9d2dd-255">**Sample 2: cross apply multiple objects with hello same pattern from array**</span></span>

<span data-ttu-id="9d2dd-256">В этом примере предполагается, что tootransform один корневой объект JSON в несколько записей в табличный результат.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-256">In this sample, you expect tootransform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="9d2dd-257">Если имеется файл JSON с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="9d2dd-257">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="9d2dd-258">и отформатируйте его в таблице Azure SQL в следующих hello, выравнивание данных hello внутри массива hello toocopy перекрестное соединение с hello, общие сведения о корневой:</span><span class="sxs-lookup"><span data-stu-id="9d2dd-258">and you want toocopy it into an Azure SQL table in hello following format, by flattening hello data inside hello array and cross join with hello common root info:</span></span>

| <span data-ttu-id="9d2dd-259">ordernumber</span><span class="sxs-lookup"><span data-stu-id="9d2dd-259">ordernumber</span></span> | <span data-ttu-id="9d2dd-260">orderdate</span><span class="sxs-lookup"><span data-stu-id="9d2dd-260">orderdate</span></span> | <span data-ttu-id="9d2dd-261">order_pd</span><span class="sxs-lookup"><span data-stu-id="9d2dd-261">order_pd</span></span> | <span data-ttu-id="9d2dd-262">order_price</span><span class="sxs-lookup"><span data-stu-id="9d2dd-262">order_price</span></span> | <span data-ttu-id="9d2dd-263">city</span><span class="sxs-lookup"><span data-stu-id="9d2dd-263">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="9d2dd-264">01</span><span class="sxs-lookup"><span data-stu-id="9d2dd-264">01</span></span> | <span data-ttu-id="9d2dd-265">20170122</span><span class="sxs-lookup"><span data-stu-id="9d2dd-265">20170122</span></span> | <span data-ttu-id="9d2dd-266">P1</span><span class="sxs-lookup"><span data-stu-id="9d2dd-266">P1</span></span> | <span data-ttu-id="9d2dd-267">23</span><span class="sxs-lookup"><span data-stu-id="9d2dd-267">23</span></span> | <span data-ttu-id="9d2dd-268">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="9d2dd-268">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="9d2dd-269">01</span><span class="sxs-lookup"><span data-stu-id="9d2dd-269">01</span></span> | <span data-ttu-id="9d2dd-270">20170122</span><span class="sxs-lookup"><span data-stu-id="9d2dd-270">20170122</span></span> | <span data-ttu-id="9d2dd-271">P2</span><span class="sxs-lookup"><span data-stu-id="9d2dd-271">P2</span></span> | <span data-ttu-id="9d2dd-272">13.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-272">13</span></span> | <span data-ttu-id="9d2dd-273">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="9d2dd-273">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="9d2dd-274">01</span><span class="sxs-lookup"><span data-stu-id="9d2dd-274">01</span></span> | <span data-ttu-id="9d2dd-275">20170122</span><span class="sxs-lookup"><span data-stu-id="9d2dd-275">20170122</span></span> | <span data-ttu-id="9d2dd-276">P3</span><span class="sxs-lookup"><span data-stu-id="9d2dd-276">P3</span></span> | <span data-ttu-id="9d2dd-277">231</span><span class="sxs-lookup"><span data-stu-id="9d2dd-277">231</span></span> | <span data-ttu-id="9d2dd-278">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="9d2dd-278">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="9d2dd-279">Hello входного набора данных с **JsonFormat** тип определяется следующим образом: (частичное определение с частями hello применимо).</span><span class="sxs-lookup"><span data-stu-id="9d2dd-279">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="9d2dd-280">В частности:</span><span class="sxs-lookup"><span data-stu-id="9d2dd-280">More specifically:</span></span>

- <span data-ttu-id="9d2dd-281">`structure`раздел определяет имена столбцов настроенные hello и hello соответствующие типы данных во время преобразования данных tootabular.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-281">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="9d2dd-282">Этот раздел представляет **необязательно** при отсутствии необходимости toodo сопоставления столбцов.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-282">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="9d2dd-283">Дополнительные сведения см. в статье [Указание определения структуры для прямоугольных наборов данных](#specifying-structure-definition-for-rectangular-datasets).</span><span class="sxs-lookup"><span data-stu-id="9d2dd-283">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="9d2dd-284">`jsonNodeReference`Указывает tooiterate и извлечения данных из объектов hello с hello же шаблон в списке **массива** orderlines.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-284">`jsonNodeReference` indicates tooiterate and extract data from hello objects with hello same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="9d2dd-285">`jsonPathDefinition`Указывает путь hello JSON для каждого столбца, указывающее, где tooextract hello данные из.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-285">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="9d2dd-286">В этом примере «ordernumber», «orderdate» и «Город» находятся в корневой объект пути JSON, начиная с «$»., хотя «order_pd» и «order_price» определяются с путем, производный от элемента массива hello без «$»..</span><span class="sxs-lookup"><span data-stu-id="9d2dd-286">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from hello array element without "$.".</span></span>

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

<span data-ttu-id="9d2dd-287">**Обратите внимание hello после точки.**</span><span class="sxs-lookup"><span data-stu-id="9d2dd-287">**Note hello following points:**</span></span>

* <span data-ttu-id="9d2dd-288">Если hello `structure` и `jsonPathDefinition` не определены в наборе данных фабрики данных hello hello действие копирования обнаруживает hello схемы из первого объекта hello и одноуровневые hello объекта целиком.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-288">If hello `structure` and `jsonPathDefinition` are not defined in hello Data Factory dataset, hello Copy Activity detects hello schema from hello first object and flatten hello whole object.</span></span>
* <span data-ttu-id="9d2dd-289">По умолчанию Если входные данные JSON hello массив, hello действие копирования преобразует весь массив значение hello в строку.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-289">If hello JSON input has an array, by default hello Copy Activity converts hello entire array value into a string.</span></span> <span data-ttu-id="9d2dd-290">Для выбора tooextract данных с помощью `jsonNodeReference` и/или `jsonPathDefinition`, или пропустить его, не указывайте его в `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-290">You can choose tooextract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="9d2dd-291">При наличии дубликатов имен в Здравствуйте того же уровня, hello действие копирования выбирает hello последним.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-291">If there are duplicate names at hello same level, hello Copy Activity picks hello last one.</span></span>
* <span data-ttu-id="9d2dd-292">В именах свойств учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-292">Property names are case-sensitive.</span></span> <span data-ttu-id="9d2dd-293">Два свойства с одинаковым именем, но в разных регистрах, рассматриваются как два отдельных свойства.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-293">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="9d2dd-294">**Вариант 2: Запись файла tooJSON данных**</span><span class="sxs-lookup"><span data-stu-id="9d2dd-294">**Case 2: Writing data tooJSON file**</span></span>

<span data-ttu-id="9d2dd-295">Если в базе данных SQL есть такая таблица:</span><span class="sxs-lookup"><span data-stu-id="9d2dd-295">If you have below table in SQL Database:</span></span>

| <span data-ttu-id="9d2dd-296">id</span><span class="sxs-lookup"><span data-stu-id="9d2dd-296">id</span></span> | <span data-ttu-id="9d2dd-297">order_date</span><span class="sxs-lookup"><span data-stu-id="9d2dd-297">order_date</span></span> | <span data-ttu-id="9d2dd-298">order_price</span><span class="sxs-lookup"><span data-stu-id="9d2dd-298">order_price</span></span> | <span data-ttu-id="9d2dd-299">order_by</span><span class="sxs-lookup"><span data-stu-id="9d2dd-299">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9d2dd-300">1</span><span class="sxs-lookup"><span data-stu-id="9d2dd-300">1</span></span> | <span data-ttu-id="9d2dd-301">20170119</span><span class="sxs-lookup"><span data-stu-id="9d2dd-301">20170119</span></span> | <span data-ttu-id="9d2dd-302">2000</span><span class="sxs-lookup"><span data-stu-id="9d2dd-302">2000</span></span> | <span data-ttu-id="9d2dd-303">David</span><span class="sxs-lookup"><span data-stu-id="9d2dd-303">David</span></span> |
| <span data-ttu-id="9d2dd-304">2</span><span class="sxs-lookup"><span data-stu-id="9d2dd-304">2</span></span> | <span data-ttu-id="9d2dd-305">20170120</span><span class="sxs-lookup"><span data-stu-id="9d2dd-305">20170120</span></span> | <span data-ttu-id="9d2dd-306">3500</span><span class="sxs-lookup"><span data-stu-id="9d2dd-306">3500</span></span> | <span data-ttu-id="9d2dd-307">Patrick</span><span class="sxs-lookup"><span data-stu-id="9d2dd-307">Patrick</span></span> |
| <span data-ttu-id="9d2dd-308">3</span><span class="sxs-lookup"><span data-stu-id="9d2dd-308">3</span></span> | <span data-ttu-id="9d2dd-309">20170121</span><span class="sxs-lookup"><span data-stu-id="9d2dd-309">20170121</span></span> | <span data-ttu-id="9d2dd-310">4000</span><span class="sxs-lookup"><span data-stu-id="9d2dd-310">4000</span></span> | <span data-ttu-id="9d2dd-311">Jason</span><span class="sxs-lookup"><span data-stu-id="9d2dd-311">Jason</span></span> |

<span data-ttu-id="9d2dd-312">и для каждой записи, предполагается, что объект JSON tooa toowrite в ниже формат:</span><span class="sxs-lookup"><span data-stu-id="9d2dd-312">and for each record, you expect toowrite tooa JSON object in below format:</span></span>
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

<span data-ttu-id="9d2dd-313">Hello выходной набор данных с **JsonFormat** тип определяется следующим образом: (частичное определение с частями hello применимо).</span><span class="sxs-lookup"><span data-stu-id="9d2dd-313">hello output dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="9d2dd-314">В частности `structure` раздел определяет имена свойств настроенные hello в конечный файл `nestingSeparator` (по умолчанию — «.») будет иметь уровень вложенности hello используется tooidentify из имени hello.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-314">More specifically, `structure` section defines hello customized property names in destination file, `nestingSeparator` (default is ".") will be used tooidentify hello nest layer from hello name.</span></span> <span data-ttu-id="9d2dd-315">Этот раздел представляет **необязательно** , если не требуется имя свойства toochange hello, сравнение с именем столбца источника или вложить некоторые свойства hello.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-315">This section is **optional** unless you want toochange hello property name comparing with source column name, or nest some of hello properties.</span></span>

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

### <a name="specifying-avroformat"></a><span data-ttu-id="9d2dd-316">Определение AvroFormat</span><span class="sxs-lookup"><span data-stu-id="9d2dd-316">Specifying AvroFormat</span></span>
<span data-ttu-id="9d2dd-317">Если требуется tooparse hello Avro файлы или записи данных hello в формате Avro, задайте hello `format` `type` свойство слишком**AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-317">If you want tooparse hello Avro files or write hello data in Avro format, set hello `format` `type` property too**AvroFormat**.</span></span> <span data-ttu-id="9d2dd-318">Необязательно toospecify любые свойства в раздел формата hello внутри раздела typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-318">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="9d2dd-319">Пример:</span><span class="sxs-lookup"><span data-stu-id="9d2dd-319">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="9d2dd-320">toouse в формате Avro в таблицу Hive можно ссылаться слишком[Apache Hive учебника](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="9d2dd-320">toouse Avro format in a Hive table, you can refer too[Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="9d2dd-321">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-321">Note hello following points:</span></span>  

* <span data-ttu-id="9d2dd-322">[Сложные типы данных](http://avro.apache.org/docs/current/spec.html#schema_complex) (записи, перечисления, массивы, сопоставления, объединения и фиксированные данные) не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-322">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions and fixed).</span></span>

### <a name="specifying-orcformat"></a><span data-ttu-id="9d2dd-323">Указание OrcFormat</span><span class="sxs-lookup"><span data-stu-id="9d2dd-323">Specifying OrcFormat</span></span>
<span data-ttu-id="9d2dd-324">Если требуется tooparse hello ORC файлы или записи данных hello в формат ORC, задайте hello `format` `type` свойство слишком**OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-324">If you want tooparse hello ORC files or write hello data in ORC format, set hello `format` `type` property too**OrcFormat**.</span></span> <span data-ttu-id="9d2dd-325">Необязательно toospecify любые свойства в раздел формата hello внутри раздела typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-325">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="9d2dd-326">Пример:</span><span class="sxs-lookup"><span data-stu-id="9d2dd-326">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="9d2dd-327">При копировании файлов ORC не **как-является** между локальными и облачными хранилищами данных, необходимо tooinstall hello JRE 8 (среда выполнения Java) на компьютере шлюза.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-327">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="9d2dd-328">Для 64-разрядного шлюза требуется 64-разрядная версия JRE, а для 32-разрядного шлюза — 32-разрядная версия JRE.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-328">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="9d2dd-329">Обе эти версии доступны [здесь](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="9d2dd-329">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="9d2dd-330">Выберите подходящее hello.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-330">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="9d2dd-331">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-331">Note hello following points:</span></span>

* <span data-ttu-id="9d2dd-332">Данные сложных типов (STRUCT, MAP, LIST, UNION) не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-332">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="9d2dd-333">Для ORC-файлов используется три [параметра сжатия](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB и SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-333">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="9d2dd-334">Фабрика данных поддерживает чтение данных из ORC-файла в любом из этих форматов.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-334">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="9d2dd-335">Она использует сжатие hello кодек находится в данных hello tooread hello метаданных.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-335">It uses hello compression codec is in hello metadata tooread hello data.</span></span> <span data-ttu-id="9d2dd-336">Однако при записи файла ORC tooan, фабрики данных выбирает ZLIB, который является по умолчанию hello для ORC.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-336">However, when writing tooan ORC file, Data Factory chooses ZLIB, which is hello default for ORC.</span></span> <span data-ttu-id="9d2dd-337">В настоящее время нет отсутствует параметр toooverride это поведение.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-337">Currently, there is no option toooverride this behavior.</span></span>

### <a name="specifying-parquetformat"></a><span data-ttu-id="9d2dd-338">Указание ParquetFormat</span><span class="sxs-lookup"><span data-stu-id="9d2dd-338">Specifying ParquetFormat</span></span>
<span data-ttu-id="9d2dd-339">Если требуется tooparse hello Parquet файлы или записи данных hello в формате Parquet, задайте hello `format` `type` свойство слишком**ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-339">If you want tooparse hello Parquet files or write hello data in Parquet format, set hello `format` `type` property too**ParquetFormat**.</span></span> <span data-ttu-id="9d2dd-340">Необязательно toospecify любые свойства в раздел формата hello внутри раздела typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-340">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="9d2dd-341">Пример:</span><span class="sxs-lookup"><span data-stu-id="9d2dd-341">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="9d2dd-342">При копировании файлов Parquet не **как-является** между локальными и облачными хранилищами данных, необходимо tooinstall hello JRE 8 (среда выполнения Java) на компьютере шлюза.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-342">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="9d2dd-343">Для 64-разрядного шлюза требуется 64-разрядная версия JRE, а для 32-разрядного шлюза — 32-разрядная версия JRE.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-343">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="9d2dd-344">Обе эти версии доступны [здесь](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="9d2dd-344">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="9d2dd-345">Выберите подходящее hello.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-345">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="9d2dd-346">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-346">Note hello following points:</span></span>

* <span data-ttu-id="9d2dd-347">Данные сложных типов (MAP, LIST) не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-347">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="9d2dd-348">Файл parquet имеет следующие параметры, связанные с сжатия hello: NONE, SNAPPY, GZIP и LZO.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-348">Parquet file has hello following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="9d2dd-349">Фабрика данных поддерживает чтение данных из ORC-файла в любом из этих форматов.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-349">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="9d2dd-350">Он использует кодек сжатия hello в данных hello tooread hello метаданных.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-350">It uses hello compression codec in hello metadata tooread hello data.</span></span> <span data-ttu-id="9d2dd-351">Однако при записи файла Parquet tooa, фабрики данных выбирает SNAPPY, что является по умолчанию hello для формата Parquet.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-351">However, when writing tooa Parquet file, Data Factory chooses SNAPPY, which is hello default for Parquet format.</span></span> <span data-ttu-id="9d2dd-352">В настоящее время нет отсутствует параметр toooverride это поведение.</span><span class="sxs-lookup"><span data-stu-id="9d2dd-352">Currently, there is no option toooverride this behavior.</span></span>
