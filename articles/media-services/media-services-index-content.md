---
title: "aaaIndexing файлов мультимедиа с помощью индексатора мультимедиа Azure"
description: "Индексатор мультимедиа Azure позволяет toomake содержимого для поиска файлов мультимедиа и toogenerate полнотекстового сообщения для закрыто субтитров и ключевых слов. В этом разделе показано, как toouse индексатора мультимедиа."
services: media-services
documentationcenter: 
author: Asolanki
manager: cfowler
editor: 
ms.assetid: 827a56b2-58a5-4044-8d5c-3e5356488271
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: adsolank;juliako;johndeu
ms.openlocfilehash: c1bed774e302e61ca3510668645dc2015b434a0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-media-files-with-azure-media-indexer"></a>Индексирование файлов мультимедиа с помощью индексатора мультимедийных данных Azure
Индексатор мультимедиа Azure позволяет toomake содержимого для поиска файлов мультимедиа и toogenerate полнотекстового сообщения для закрыто субтитров и ключевых слов. Вы можете обработать один файл мультимедиа или несколько файлов мультимедиа в пакете.  

> [!IMPORTANT]
> Во время индексирования содержимого, убедитесь, что toouse файлы мультимедиа, которые максимально разборчивой речью (без фоновой музыки, шума, эффектов или шипения микрофона). Примерами подходящего содержимого могут служить записи собраний, лекций или презентаций. Hello следующее содержимое может не подходить для индексирования: фильмы, ТВ-передачи, что-либо со смешанными аудио- и звуковыми эффектами, некачественная запись содержимого с фоновым шумом (шипением).
> 
> 

Задание индексирования можно сформировать hello следующие выходные данные:

* Файлы со скрытыми титрами в hello следующие форматы: **SAMI**, **TTML**, и **WebVTT**.
  
    Файлы титров содержат тег Recognizability, — какие показатели, задание индексирования в зависимости от распознаваемости речи hello в hello источника видео.  Значение hello Recognizability tooscreen выходные файлы можно использовать для более удобной работы. Низкий показатель означает плохие результаты индексирования из-за tooaudio качества.
* Файл с ключевыми словами (XML).
* Файл большого двоичного объекта аудиоиндексации (AIB) для использования с SQL Server.
  
    Подробнее этот вопрос раскрыт в [Использование файлов AIB с индексатором мультимедийных данных Azure и SQL Server](https://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/).

В этом разделе показано, как индексирование toocreate задания слишком**индексация актива** и **индексация нескольких файлов**.

Последние обновления hello индексатора мультимедиа Azure, см. [блоги служб мультимедиа](#preset).

## <a name="using-configuration-and-manifest-files-for-indexing-tasks"></a>Использование файлов конфигурации и манифеста для задач индексирования
С помощью конфигурации задачи можно задать дополнительные параметры задач индексирования. Например можно указать какие toouse метаданные для файла мультимедиа. Эти метаданные используются tooexpand подсистемы языка hello словаря и значительного улучшения точности распознавания речи hello.  Вы, также может toospecify нужные выходные файлы.

С помощью файла манифеста можно также обработать несколько файлов мультимедиа одновременно.

Подробнее этот вопрос раскрыт в [Предустановка задачи для индексатора мультимедийных данных Azure](https://msdn.microsoft.com/library/dn783454.aspx).

## <a name="index-an-asset"></a>Индексирование ресурса
Hello следующий метод отправляет файл мультимедиа в виде актива и создает ресурс hello tooindex задания.

Обратите внимание, что если файл конфигурации не указан, файл мультимедиа hello будут индексироваться со всеми параметрами по умолчанию.

    static bool RunIndexingJob(string inputMediaFilePath, string outputFolder, string configurationFile = "")
    {
        // Create an asset and upload hello input media file toostorage.
        IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Indexing Input Asset",
            AssetCreationOptions.None);

        // Declare a new job.
        IJob job = _context.Jobs.Create("My Indexing Job");

        // Get a reference toohello Azure Media Indexer.
        string MediaProcessorName = "Azure Media Indexer";
        IMediaProcessor processor = GetLatestMediaProcessorByName(MediaProcessorName);

        // Read configuration from file if specified.
        string configuration = string.IsNullOrEmpty(configurationFile) ? "" : File.ReadAllText(configurationFile);

        // Create a task with hello encoding details, using a string preset.
        ITask task = job.Tasks.AddNew("My Indexing Task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input asset toobe indexed.
        task.InputAssets.Add(asset);

        // Add an output asset toocontain hello results of hello job.
        task.OutputAssets.AddNew("My Indexing Output Asset", AssetCreationOptions.None);

        // Use hello following event handler toocheck job progress.  
        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

        // Launch hello job.
        job.Submit();

        // Check job execution and wait for job toofinish.
        Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
        progressJobTask.Wait();

        // If job state is Error, hello event handling
        // method for job progress should log errors.  Here we check
        // for error state and exit if needed.
        if (job.State == JobState.Error)
        {
            Console.WriteLine("Exiting method due toojob error.");
            return false;
        }

        // Download hello job outputs.
        DownloadAsset(task.OutputAssets.First(), outputFolder);

        return true;
    }

    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = _context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }  
<!-- __ -->
### <a id="output_files"></a>Выходные файлы
По умолчанию задание индексирования создает следующие выходные файлы hello. в первый выходной актив hello будут храниться файлы Hello.

Если имеется более одного входного файла мультимедиа, индексатор создаст файл манифеста для выходных данных задания hello, с именем «JobResult.txt». Для каждого входного файла мультимедиа hello полученные AIB, SAMI, TTML, WebVTT и файлы ключевых слов последовательно пронумерованы и с именем с помощью «Alias» hello.

| Имя файла | Описание |
| --- | --- |
| **InputFileName.aib** |Файл большого двоичного объекта для индексирования аудиозаписей. <br/><br/> Файл большого двоичного объекта для индексирования аудиозаписей (AIB) — это двоичный файл, по которому можно выполнять полнотекстовый поиск на сервере Microsoft SQL Server.  файл AIB Hello эффективнее, чем hello простые файлы титров, так как она содержит альтернативные слова, позволяя основательный поиск. <br/> <br/>Она требует установки hello hello надстройку индексатора SQL на компьютере с Microsoft SQL server 2008 или более поздней версии. Поиск hello AIB с помощью Microsoft SQL server полнотекстовый поиск обеспечивает более точные результаты, чем поиск hello файлы со скрытыми титрами созданных WAMI. Это происходит потому hello AIB содержит другие слова, которые звучат схожим, тогда как hello файлы со скрытыми титрами содержат наиболее подходящее слово hello для каждого сегмента hello аудио. Если поиск произносимых слов крайне важен, то рекомендуется toouse hello AIB вместе с Microsoft SQL Server.<br/><br/> toodownload Здравствуйте надстройку, щелкните <a href="http://aka.ms/indexersql">надстройка индексатора SQL Azure Media служб</a>. <br/><br/>Он также возможно tooutilize другие поисковые системы, такие как Apache Lucene/Solr toosimply индекс hello видео на основе заголовка hello закрыт и ключевое слово XML-файлов, но это приведет к менее точным результатам поиска. |
| **InputFileName.smi**<br/>**InputFileName.ttml**<br/>**InputFileName.vtt** |Файлы скрытых субтитров (CC) в форматах SAMI, TTML и WebVTT.<br/><br/>Их можно использовать toomake аудио и видео файлы доступны toopeople возможностями слуха.<br/><br/>Файлы закрытых субтитров содержат тег <b>Recognizability</b> — который оценивает задание индексирования, в зависимости от распознаваемости речи hello в hello источника видео.  Можно использовать значение hello <b>Recognizability</b> tooscreen выходные файлы для более удобной работы. Низкий показатель означает плохие результаты индексирования из-за tooaudio качества. |
| **InputFileName.kw.xml<br/>InputFileName.info** |Файлы ключевых слов и сведений. <br/><br/>Файл ключевых слов является XML-файл, который содержит ключевые слова, извлеченные из голосового содержимого hello, с частотой и сведения о смещении. <br/><br/>Файл сведений — это обычный текстовый файл, который содержит подробные сведения о каждом распознанном термине. Первая строка Hello специальные и содержит показатель Recognizability hello. Каждая следующая строка является списком разделенных табуляцией hello следующие данные: запуск время, время окончания, слово или фраза, достоверности. Hello указывается в секундах и достоверности hello предоставляется как число от 0-1. <br/><br/>Пример строки: "1.20 1.45 word 0.67". <br/><br/>Эти файлы можно использовать для различных целей, например tooperform анализа голосовых функций, или предоставленный toosearch ядра например Bing, Google или Microsoft SharePoint toomake hello файлов мультимедиа более доступными или даже используется toodeliver более актуальной рекламы. |
| **JobResult.txt** |Выходной манифест, присутствует только в том случае, если индексирование нескольких файлов, содержащая hello следующую информацию:<br/><br/><table border="1"><tr><th>InputFile</th><th>Alias</th><th>MediaLength</th><th>Ошибка</th></tr><tr><td>a.mp4</td><td>Media_1</td><td>300</td><td>0</td></tr><tr><td>b.mp4</td><td>Media_2</td><td>0</td><td>3000</td></tr><tr><td>c.mp4</td><td>Media_3</td><td>600</td><td>0</td></tr></table><br/> |

Если не все файлы успешно индексированы, hello задание индексирования завершится ошибкой с кодом ошибки 4000. Подробнее этот вопрос раскрыт в [Коды ошибок](#error_codes).

## <a name="index-multiple-files"></a>индексирования нескольких файлов
Hello следующий метод отправляет несколько файлов мультимедиа в виде актива и создает tooindex задания эти файлы в пакете.

Файл манифеста с расширением .lst hello и отправляется в актив hello. файл манифеста Hello содержит hello список всех файлов активов hello. Подробнее этот вопрос раскрыт в [Предустановка задачи для индексатора мультимедийных данных Azure](https://msdn.microsoft.com/library/dn783454.aspx).

    static bool RunBatchIndexingJob(string[] inputMediaFiles, string outputFolder)
    {
        // Create an asset and upload toostorage.
        IAsset asset = CreateAssetAndUploadMultipleFiles(inputMediaFiles,
            "My Indexing Input Asset - Batch Mode",
            AssetCreationOptions.None);

        // Create a manifest file that contains all hello asset file names and upload toostorage.
        string manifestFile = "input.lst";            
        File.WriteAllLines(manifestFile, asset.AssetFiles.Select(f => f.Name).ToArray());
        var assetFile = asset.AssetFiles.Create(Path.GetFileName(manifestFile));
        assetFile.Upload(manifestFile);

        // Declare a new job.
        IJob job = _context.Jobs.Create("My Indexing Job - Batch Mode");

        // Get a reference toohello Azure Media Indexer.
        string MediaProcessorName = "Azure Media Indexer";
        IMediaProcessor processor = GetLatestMediaProcessorByName(MediaProcessorName);

        // Read configuration.
        string configuration = File.ReadAllText("batch.config");

        // Create a task with hello encoding details, using a string preset.
        ITask task = job.Tasks.AddNew("My Indexing Task - Batch Mode",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input asset toobe indexed.
        task.InputAssets.Add(asset);

        // Add an output asset toocontain hello results of hello job.
        task.OutputAssets.AddNew("My Indexing Output Asset - Batch Mode", AssetCreationOptions.None);

        // Use hello following event handler toocheck job progress.  
        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

        // Launch hello job.
        job.Submit();

        // Check job execution and wait for job toofinish.
        Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
        progressJobTask.Wait();

        // If job state is Error, hello event handling
        // method for job progress should log errors.  Here we check
        // for error state and exit if needed.
        if (job.State == JobState.Error)
        {
            Console.WriteLine("Exiting method due toojob error.");
            return false;
        }

        // Download hello job outputs.
        DownloadAsset(task.OutputAssets.First(), outputFolder);

        return true;
    }

    private static IAsset CreateAssetAndUploadMultipleFiles(string[] filePaths, string assetName, AssetCreationOptions options)
    {
        IAsset asset = _context.Assets.Create(assetName, options);

        foreach (string filePath in filePaths)
        {
            var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
            assetFile.Upload(filePath);
        }

        return asset;
    }

### <a name="partially-succeeded-job"></a>Частично успешно выполненное задание
Если не все файлы успешно индексированы, hello задание индексирования завершится ошибкой с кодом ошибки 4000. Подробнее этот вопрос раскрыт в [Коды ошибок](#error_codes).

Здравствуйте, те же выходные данные (в качестве выполненных заданий) создаются. Можно ссылаться toohello выходной файл манифеста toofind какие сбой входных файлов, в соответствии с toohello значения столбца ошибок. Для входных файлов, которые не удалось hello полученные AIB, SAMI, TTML, WebVTT и файлы ключевых слов не будут созданы.

### <a id="preset"></a> Предустановка задачи для индексатора мультимедийных данных Azure
Hello обработку индексатора мультимедиа Azure можно настроить, указав необязательные задачи, предустановленные вместе с задачу hello.  Hello ниже приводится формат hello этот XML-файл конфигурации.

| Имя | Обязательный параметр | Описание |
| --- | --- | --- |
| **input** |нет |Файлы активов, которые должны tooindex.</p><p>Индексатор мультимедиа Azure поддерживает следующие форматы файлов мультимедиа hello: MP4, WMV, MP3, M4A, WMA, AAC, WAV-файла.</p><p>Можно указать имя файла hello (s) в hello **имя** или **списка** атрибут hello **ввода** (как показано ниже). Если не указать какие tooindex файла актива, выбирается первичный файл hello. Если первичный файл актива, индексируется первый файл hello hello входного актива.</p><p>tooexplicitly укажите имя файла актива hello, выполните действия.<br/>`<input name="TestFile.wmv">`<br/><br/>Также можно индексировать несколько файлов актива одновременно (копии файлов too10). toodo это:<br/><br/><ol class="ordered"><li><p>Создайте текстовый файл (файл манифеста) с расширением LST. </p></li><li><p>Добавьте список всех имен файлов активов hello в файле манифеста toothis входного актива. </p></li><li><p>Добавьте файл toohello (отправить) thanifest активов.  </p></li><li><p>Укажите имя файла манифеста hello hello в атрибут списка входного актива hello.<br/>`<input list="input.lst">`</li></ol><br/><br/>Примечание: При добавлении файла манифеста более 10 файлов toohello hello, задание индексирования завершится ошибкой с кодом ошибки 2006 hello. |
| **metadata** |нет |Метаданные для hello указаны файлы активов, используемые для адаптации словаря.  Полезные tooprepare индексатора toorecognize стандартным словарь слова, такие как имена собственные.<br/>`<metadata key="..." value="..."/>` <br/><br/>Вы можете указать значения **value** для поддерживаемых ключей **key**. В настоящее время поддерживаются следующие ключи hello:<br/><br/>«title» и «description» — используются для словаря адаптации tootweak hello языка модели для вашей работы и повышения точности распознавания речи.  Hello значения в качестве начального Интернет поиск toofind зависимости от контекста соответствующий текст документов, с помощью hello содержимое tooaugment hello внутренний словарь для hello длительности задачи индексирования.<br/>`<metadata key="title" value="[Title of hello media file]" />`<br/>`<metadata key="description" value="[Description of hello media file] />"` |
| **features** <br/><br/> Добавлено в версии 1.2. В настоящее время функция hello поддерживается только — распознавания речи «(ASR)». |нет |функция распознавания речи Hello имеет следующие ключи параметров hello:<table><tr><th><p>Ключ</p></th>        <th><p>Описание</p></th><th><p>Пример значения</p></th></tr><tr><td><p>Язык</p></td><td><p>Здравствуйте, распознаваемые в файл мультимедиа hello toobe естественного языка.</p></td><td><p>English, Spanish</p></td></tr><tr><td><p>CaptionFormats</p></td><td><p>Список разделенных точкой с запятой hello требуемого форматах заголовок (если есть)</p></td><td><p>ttml;sami;webvtt</p></td></tr><tr><td><p>GenerateAIB</p></td><td><p>Логический флаг, указав, требуется ли AIB-файл (для использования с SQL Server и hello клиентом индексатора IFilter).  Подробнее этот вопрос раскрыт в <a href="http://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/">Использование файлов AIB с индексатором мультимедийных данных Azure и SQL Server</a>.</p></td><td><p>True; False</p></td></tr><tr><td><p>GenerateKeywords</p></td><td><p>Логический флаг. Если он установлен, создается XML-файл ключевых слов.</p></td><td><p>True; False </p></td></tr><tr><td><p>ForceFullCaption</p></td><td><p>Логический флаг, указав ли tooforce полной подписи (независимо от уровня достоверности).  </p><p>По умолчанию равно false, в этом случае слова и фразы, которые имеют меньше, чем уровень достоверности 50% включаются в выходные данные заголовка окончательного hello и заменяется многоточия («...»).  многоточие Hello полезны для контроля качества заголовка и аудита.</p></td><td><p>True; False </p></td></tr></table> |

### <a id="error_codes"></a>Коды ошибок
В случае ошибки hello индексатора мультимедиа Azure следует сообщать один hello следующие коды ошибок назад:

| Код | Имя | Возможные причины |
| --- | --- | --- |
| 2000 |Недопустимая конфигурация |Недопустимая конфигурация |
| 2001 |Недопустимые входные ресурсы |Отсутствие входных ресурсов или пустой ресурс. |
| 2002 |Недопустимый манифест |Манифест пуст или содержит недопустимые элементы. |
| 2003 |Не удалось toodownload файл мультимедиа |Недопустимый URL-адрес в файле манифеста. |
| 2004 |Неподдерживаемый протокол |Протокол URL-адреса мультимедиа не поддерживается. |
| 2005 |Неподдерживаемый тип файла |Тип файла входного мультимедиа не поддерживается. |
| 2006 |Слишком много входных файлов |Существует более чем 10 файлов в hello входной манифест. |
| 3000 |Не удалось toodecode файл мультимедиа |Кодек мультимедиа не поддерживается  <br/>или<br/> файл мультимедиа поврежден <br/>или<br/> Входной файл мультимедиа не содержит аудиопотока. |
| 4000 |Индексирование пакета выполнено частично |Hello носитель входные файлы, не удалось выполнить некоторые toobe проиндексированы. Дополнительные сведения см. в статье <a href="#output_files">Выходные файлы</a>. |
| Прочие |Внутренние ошибки |Обратитесь в службу поддержки. indexer@microsoft.com |

## <a id="supported_languages"></a>Поддерживаемые языки
В настоящее время поддерживаются hello английском и испанском языках. Дополнительные сведения см. в разделе [hello v1.2 выпуске блога](https://azure.microsoft.com/blog/2015/04/13/azure-media-indexer-spanish-v1-2/).

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Связанные ссылки
[Общие сведения об аналитике служб мультимедиа Azure](media-services-analytics-overview.md)

[Использование файлов AIB с индексатором мультимедийных данных Azure и SQL Server](https://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/)

[Индексирование файлов мультимедиа с помощью индексатора мультимедийных данных Azure 2 (предварительная версия)](media-services-process-content-with-indexer2.md)

