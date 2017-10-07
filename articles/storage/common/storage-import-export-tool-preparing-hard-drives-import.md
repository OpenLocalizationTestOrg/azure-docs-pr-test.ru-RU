---
title: "Задание импорта aaaPreparing жестких дисков для импорта и экспорта Azure | Документы Microsoft"
description: "Узнайте, как tooprepare жесткие диски с помощью hello toocreate средство WAImportExport задания импорта для hello службы импорта и экспорта Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: muralikk
ms.openlocfilehash: dc4f4f580f70dbd504317f59df142b3e4c48cb66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-hard-drives-for-an-import-job"></a>Подготовка жестких дисков к заданию импорта

Hello средство WAImportExport является hello диск средство подготовки и восстановления, можно использовать с hello [службы импорта и экспорта Microsoft Azure](../storage-import-export-service.md). Можно использовать этот инструмент toocopy данных toohello жестких дисков будет tooship tooan центра обработки данных Azure. После завершения задания импорта, можно использовать этот инструмент toorepair все большие двоичные объекты, которые были повреждены, были потеряны или конфликтуют с другими большими двоичными объектами. После получения hello диски с выполненным заданием экспорта, можно использовать этот инструмент toorepair все файлы, которые были повреждены или отсутствуют на дисках hello. В этой статье будет рассмотрена hello использование этого средства.

## <a name="prerequisites"></a>Предварительные требования

### <a name="requirements-for-waimportexportexe"></a>Требования к WAImportExport.exe

- **Конфигурация компьютера**
  - Windows 7, Windows Server 2008 R2 или операционная система Windows более поздней версии.
  - На компьютере должна быть установлена платформа .NET Framework 4. В разделе [часто задаваемые вопросы о](#faq) о том, как toocheck, если .net Framework установлены на компьютере hello.
- **Ключ учетной записи хранения** -требуется по крайней мере одна hello ключей учетной записи для учетной записи хранения hello.

### <a name="preparing-disk-for-import-job"></a>Подготовка диска к заданию импорта

- **BitLocker —** BitLocker должен быть включен как средство WAImportExport выполнение hello hello компьютеров. В разделе hello [часто задаваемые вопросы о](#faq) как tooenable BitLocker.
- **Диски** должны быть доступными на компьютере, где запущено средство WAImportExport. Спецификацию дисков см. в [часто задаваемых вопросах](#faq).
- **Исходные файлы** -файлы hello планирование tooimport должен быть доступен из машина для копирования hello ли они находятся в общей сетевой папке или на локальный жесткий диск.

### <a name="repairing-a-partially-failed-import-job"></a>Восстановление задания импорта, частично завершившегося сбоем

- **Файл журнала копирования**, созданный во время копирования службой импорта и экспорта Azure данных между учетной записью хранения и диском. Он находится в целевой учетной записи хранения.

### <a name="repairing-a-partially-failed-export-job"></a>Восстановление задания экспорта, частично завершившегося сбоем

- **Файл журнала копирования**, созданный во время копирования службой импорта и экспорта Azure данных между учетной записью хранения и диском. Он находится в исходной учетной записи хранения.
- **Файл манифеста.** Он находится на экспортированном диске, возвращенном корпорацией Майкрософт (необязательно).

## <a name="download-and-install-waimportexport"></a>Скачивание и установка средства WAImportExport

Загрузите hello [последнюю версию WAImportExport.exe](https://www.microsoft.com/download/details.aspx?id=55280). Извлеките hello ZIP-папки содержимого tooa каталог на локальном компьютере.

Следующая задача — toocreate CSV-файлы.

## <a name="prepare-hello-dataset-csv-file"></a>Подготовка CSV-файл hello набора данных

### <a name="what-is-dataset-csv"></a>Что такое CSV-файл набора данных

Набор данных CSV-файл является hello значение флага/набор_данных CSV-файл, содержащий список каталогов или список дисков tootarget toobe копируются файлы. Hello toocreating первый шаг задания импорта является toodetermine какие каталоги и файлы будут tooimport. Это может быть список каталогов, список уникальных файлов или оба списка. Если каталог включен, все файлы в каталоге hello и его подкаталогах будет частью задания импорта hello.

Для каждого toobe каталог или файл, в импортирован необходимо определить целевой виртуальный каталог или большой двоичный объект в hello службы больших двоичных объектов. Эти целевые объекты будет использоваться в качестве средства WAImportExport toohello входных данных. Каталоги следует разделять символом косой черты hello «/».

Привет, в следующей таблице приведены некоторые примеры целевых больших двоичных объектов.

| Исходный файл или каталог | Целевой большой двоичный объект или виртуальный каталог |
| --- | --- |
| H:\Video | https://mystorageaccount.blob.core.windows.net/video |
| H:\Photo | https://mystorageaccount.blob.core.windows.net/photo |
| K:\Temp\FavoriteVideo.ISO | https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO |
| \\myshare\john\music | https://mystorageaccount.blob.core.windows.net/music |

### <a name="sample-datasetcsv"></a>Пример файла dataset.csv

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
"F:\50M_original\100M_1.csv.txt","containername/100M_1.csv.txt",BlockBlob,rename,"None",None
"F:\50M_original\","containername/",BlockBlob,rename,"None",None
```

### <a name="dataset-csv-file-fields"></a>Поля CSV-файла набора данных

| Поле | Описание |
| --- | --- |
| BasePath | **[Обязательный параметр]**<br/>значение этого параметра Hello представляет hello источник расположения toobe данных hello импортированы. Средство Hello будет рекурсивное копирование всех данных, расположенных в этом пути.<br><br/>**Допустимые значения**: это toobe допустимый путь на локальном компьютере или допустимым путем к папке и должна быть доступна пользователем hello. путь к каталогу Hello должен быть абсолютным (не относительный путь). Если путь hello заканчивается»\\«, он представляет каталог else путь заканчивается без»\\"представляет файл.<br/>В этом поле запрещается использовать регулярные выражения. Если hello путь содержит пробелы, поместите его «».<br><br/>**Пример:** c:\Directory\c\Directory\File.txt,<br>"\\\\FBaseFilesharePath.domain.net\sharename\directory\"  |
| DstBlobPathOrPrefix | **[Обязательный параметр]**<br/> Hello путь toohello целевой виртуальный каталог в учетной записи хранилища Windows Azure. виртуальный каталог Hello может или уже не существует. Если он отсутствует, служба импорта и экспорта создаст его.<br/><br/>Быть убедиться, что toouse допустимые имена контейнеров, при указании целевых виртуальных каталогов или больших двоичных объектов. Обратите внимание, что имена каталогов пишутся строчными буквами. Правила именования контейнеров см. в статье [Именование контейнеров, больших двоичных объектов и метаданных и ссылка на них](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata). Корневой указано, если только структуру каталогов hello источника hello реплицируется в контейнер больших двоичных объектов назначения hello. Желанию структуры другой каталог чем hello другой в источнике, несколько строк сопоставления в формате CSV<br/><br/>Контейнер или префикс большого двоичного объекта можно указать следующим образом: music/70s/. Hello целевой каталог должен начинаться с имени контейнера hello, следуют косой черты «/» и при необходимости может включаться каталога виртуального большого двоичного объекта, заканчивающееся на «/».<br/><br/>Если hello целевой контейнер — hello корневой контейнер, необходимо явно указать корневой контейнер hello, включая косую черту hello, как $root /. Так как не может включать большие двоичные объекты в корневом контейнере hello «/» в именах, все подкаталоги в исходном каталоге hello не будут скопированы, если каталог назначения hello — hello корневой контейнер.<br/><br/>**Пример**<br/>Если пути к BLOB-объект назначения hello https://mystorageaccount.blob.core.windows.net/video, hello значением этого поля может быть видео /  |
| BlobType | **[Необязательный параметр]** block &#124; page<br/>В настоящее время служба импорта и экспорта поддерживает 2 вида больших двоичных объектов: страничные BLOB-объекты и блочные BLOB-объекты. По умолчанию все файлы импортируются как блочные BLOB-объекты. И \*.vhd и \*.vhdx, импортируется как страница BlobsThere — ограничение на блочный BLOB-объект hello и страничным допустимый размер. Дополнительные сведения см. в статье [Целевые показатели масштабируемости и производительности службы хранилища Azure](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files).  |
| Disposition | **[Необязательный параметр]** rename &#124; no-overwrite &#124; overwrite <br/> Это поле указывает функции копирования hello во время импорта т. е. данных загружен toohello учетной записи хранилища с диска hello. Доступные параметры: переименование &#124; перезаписать &#124; нет перезаписать. Значения по умолчанию слишком «переименовать» Если ничего не указано. <br/><br/>**rename** — при наличии двух объектов с одинаковым именем создает копию в целевом расположении.<br/>Перезаписать: перезаписывает файл hello с новым файлом. файл Hello в wins, Дата последнего изменения.<br/>**Не перезаписывать**: пропускает записи hello файл, если он уже существует.|
| MetadataFile | **[Необязательный параметр]** <br/>поле toothis значение Hello является hello файла метаданных, который можно указать, если один hello должен toopreserve hello метаданных объектов hello или предоставлять пользовательские метаданные. Файл метаданных toohello путь для hello целевых больших двоичных объектов. Дополнительные сведения см. в статье [Формат файла свойств и метаданных службы импорта и экспорта](../storage-import-export-file-format-metadata-and-properties.md). |
| PropertiesFile | **[Необязательный параметр]** <br/>Путь к файлу свойств toohello для hello целевых больших двоичных объектов. Дополнительные сведения см. в статье [Формат файла свойств и метаданных службы импорта и экспорта](../storage-import-export-file-format-metadata-and-properties.md). |

## <a name="prepare-initialdriveset-or-additionaldriveset-csv-file"></a>Подготовка CSV-файла InitialDriveSet или AdditionalDriveSet

### <a name="what-is-driveset-csv"></a>Что такое CSV-файл набора дисков

Hello hello /InitialDriveSet или /AdditionalDriveSet флаг равен CSV-файл, содержащий список hello дисков буквы дисков hello toowhich сопоставления, чтобы hello средство может правильно hello список выбора toobe диски подготовлены. Если размер данных hello больше, чем размер одного диска, средство WAImportExport hello будет распространять данные hello на нескольких дисках, этот CSV-файл прикреплен оптимальным образом.

Нет ограничений на hello число дисков данных hello могут быть записаны tooin один сеанс. Средство Hello будет распространять данные, на основе места на диске и размера папки. Он выбирает диск hello, наиболее оптимизирован для размер объекта hello. Здравствуйте данных при отправке toohello учетной записи хранения будут структура каталогов схождением toohello назад, был указан в файле набора данных. В порядке toocreate driveset CSV выполните следующие шаги hello.

### <a name="create-basic-volume-and-assign-drive-letter"></a>Создание базового тома и назначение буквы диска

В порядок toocreate базового тома и назначить букву диска в соответствии с инструкциями hello для простой раздела» Создание «в [Обзор управления дисками](https://technet.microsoft.com/library/cc754936.aspx).

### <a name="sample-initialdriveset-and-additionaldriveset-csv-file"></a>Пример CSV-файла InitialDriveSet и AdditionalDriveSet

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631
H,Format,SilentMode,Encrypt,
```

### <a name="driveset-csv-file-fields"></a>Поля CSV-файла набора дисков

| Поля | Значение |
| --- | --- |
| DriveLetter | **[Обязательный параметр]**<br/> Каждого диска, который предоставляется средство toohello hello назначения должен иметь простой том NTFS на нем и буквой tooit.<br/> <br/>**Пример:** R или r. |
| FormatOption | **[Обязательный параметр]** Format &#124; AlreadyFormatted<br/><br/> **Формат**: задание этого отформатирует все hello данные на диске hello. <br/>**AlreadyFormatted**: hello средство будет пропускать форматирование, если это значение задано. |
| SilentOrPromptOnFormat | **[Обязательный параметр]** SilentMode &#124; PromptOnFormat<br/><br/>**SilentMode**: использование этого значения позволит средство hello toorun пользователя в автоматическом режиме. <br/>**PromptOnFormat**: hello, будет предложено hello пользователя tooconfirm ли действие hello предназначено действительно в любом формате.<br/><br/>Если не задать его, выполнение команды прервется и отобразится сообщение "Неправильное значение для свойства SilentOrPromptOnFormat: none". |
| Шифрование | **[Обязательный параметр]**  Encrypt &#124; AlreadyEncrypted<br/> Hello значением этого поля решает, какие tooencrypt диск, а какие не к. <br/><br/>**Шифрование**: средство отформатирует диск hello. Если значение поля «FormatOption» — «Format», это значение является обязательным toobe «Encrypt». Если в этом случае задать значение AlreadyEncrypted, отобразится следующее сообщение об ошибке: When Format is specified, Encrypt must also be specified (Если задано значение Format, то также необходимо задать значение Encrypt).<br/>**AlreadyEncrypted**: средство будет расшифровывать диск hello, с помощью hello BitLockerKey, указанный в поле «ExistingBitLockerKey». Если для поля FormatOption задано значение AlreadyFormatted, то в этом поле можно задать как значение Encrypt, так и AlreadyEncrypted. |
| ExistingBitLockerKey | **[Обязательный параметр]**, если в поле Encryption задано значение AlreadyEncrypted<br/> Hello значением этого поля является ключ BitLocker hello, связанный с конкретного диска hello. <br/><br/>В этом поле следует оставить пустым, если hello значение поля «Шифрование» — «Encrypt».  Если в этом случае указать ключ BitLocker, отобразится следующее сообщение об ошибке: Bitlocker Key should not be specified (Не следует указывать ключ BitLocker).<br/>  **Пример**: 060456-014509-132033-080300-252615-584177-672089-411631.|

##  <a name="preparing-disk-for-import-job"></a>Подготовка диска к заданию импорта

tooprepare дисков для задания импорта, вызовите средство WAImportExport hello с hello **PrepImport** команды. Используемые параметры зависит от того, является ли это является hello первого сеанса копирования или последующего сеанса.

### <a name="first-session"></a>Первый сеанс

Первый сеанс копирования tooCopy Single/Multiple каталог tooa один или несколько дисков (в зависимости от того, что указано в CSV-файл) средство WAImportExport PrepImport команду для hello сначала скопируйте сеанса toocopy каталоги и файлы в новом сеансе копирования:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>] DataSet:<dataset.csv>
```

**Пример**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:\*\*\*\*\*\*\*\*\*\*\*\*\* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

### <a name="add-data-in-subsequent-session"></a>Добавление данных в последующем сеансе

В последующих сеансах копирования не обязательно toospecify hello исходные параметры. Требуется toouse hello же файл журнала для hello средство tooremember того места в hello предыдущего сеанса. состояние сеанса копирования hello Hello записывается toohello файла журнала. Ниже приведен синтаксис hello последующие копии сеанса toocopy Дополнительные каталоги и файлы:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<DifferentSessionId>  [DataSet:<differentdataset.csv>]
```

**Пример**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

### <a name="add-drives-toolatest-session"></a>Добавление дисков toolatest сеанса

Если данные hello не уместилось в выбранные диски в InitialDriveset, можно использовать toosame hello средство tooadd дополнительные диски сеанс копирования. 

>[!NOTE] 
>Идентификатор сеанса Hello должен соответствовать hello идентификатор предыдущего сеанса. Файл журнала должен соответствовать hello, указанному в предыдущем сеансе.
>
```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AdditionalDriveSet:<newdriveset.csv>
```

**Пример**

```
WAImportExport.exe PrepImport /j:SameJournalTest.jrn /id:session#2  /AdditionalDriveSet:driveset-2.csv
```

### <a name="abort-hello-latest-session"></a>Прервать hello последний сеанс:

Если сеанс копирования прерывается и не является возможные tooresume (например, если исходный каталог недоступен), то необходимо прервать hello текущего сеанса, чтобы его можно откатить назад» и «новые сеансы копирования можно запустить:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AbortSession
```

**Пример**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /AbortSession
```

Только hello последний сеанс копирования был завершен аварийно, может быть прервана. Обратите внимание, что нельзя отменить hello первого сеанса копирования для диска. Вместо этого необходимо перезапустить сеанс копирования hello с новым файлом журнала.

### <a name="resume-a-latest-interrupted-session"></a>Возобновление последнего прерванного сеанса

Если сеанс копирования прерван по какой-либо причине, его можно возобновить, запустив программу hello только файл журнала hello указанных:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /ResumeSession
```

**Пример**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /ResumeSession
```

> [!IMPORTANT] 
> При возобновлении сеанса копирования не изменяйте hello источника файлы и папки данных путем добавления или удаления файлов.

## <a name="waimportexport-parameters"></a>Параметры WAImportExport

| Параметры | Описание |
| --- | --- |
|     /j:&lt;JournalFile&gt;  | **Обязательный**<br/> Путь к файлу журнала toohello. Файл журнала отслеживает наборе дисков и записей hello выполняется при подготовке таких дисков. всегда необходимо указать файл журнала Hello.  |
|     /logdir:&lt;LogDirectory&gt;  | **Необязательно**. каталог журнала Hello.<br/> Файлы подробных журналов, а также некоторые временные файлы будут записаны toothis каталога. Если не указан, текущий каталог будет использоваться как каталог журнала hello. Hello каталог журнала может быть указан только один раз для hello же файл журнала.  |
|     /id:&lt;SessionId&gt;  | **Обязательный**<br/> Hello сеанс, когда идентификатор используется tooidentify сеанс копирования. Это используется tooensure точного восстановления прерванного сеанса копирования.  |
|     /ResumeSession  | необязательный параметр. Если hello последний сеанс копирования было неожиданно прервано, этот параметр может иметь указанный tooresume hello сеанса.   |
|     /AbortSession  | необязательный параметр. Если hello последний сеанс копирования было неожиданно прервано, этот параметр может иметь указанный tooabort hello сеанса.  |
|     /sn:&lt;StorageAccountName&gt;  | **Обязательный**<br/> Применяется только для команд RepairImport и RepairExport. Имя учетной записи хранилища hello Hello.  |
|     /sk:&lt;StorageAccountKey&gt;  | **Обязательный**<br/> ключ учетной записи хранилища hello Hello. |
|     /InitialDriveSet:&lt;driveset.csv&gt;  | **Требуется** при выполнении hello первого сеанса копирования<br/> CSV-файл, содержащий список tooprepare дисков.  |
|     /AdditionalDriveSet:&lt;driveset.csv&gt; | **Обязательный**. При добавлении сеанса копирования toocurrent дисков. <br/> CSV-файл, содержащий список добавлен toobe дополнительные диски.  |
|      /r:&lt;RepairFile&gt; | **Обязательный параметр.** Применяется только для команд RepairImport и RepairExport.<br/> Путь к файлу toohello для отслеживания хода выполнения восстановления. Каждый диск должен быть связан с одним и только одним файлом восстановления.  |
|     /d:&lt;TargetDirectories&gt; | **Обязательный**. Применяется только для команд RepairImport и RepairExport. Для RepairImport один или несколько каталогов, разделенных точкой с запятой toorepair; Для RepairExport toorepair один каталог, например корневой каталог диска hello.  |
|     /CopyLogFile:&lt;DriveCopyLogFile&gt; | **Обязательный параметр.** Применяется только для команд RepairImport и RepairExport. Файл журнала копирования диска toohello путь (verbose или ошибка).  |
|     /ManifestFile:&lt;DriveManifestFile&gt; | **Обязательный параметр.** Применяется только для команды RepairExport.<br/> Путь toohello файл манифеста диска.  |
|     /PathMapFile:&lt;DrivePathMapFile&gt; | **Необязательно**. Применяется только для команды RepairImport.<br/> Путь к файлу toohello, содержащий сопоставления toolocations корневой диск относительный toohello пути файла фактических файлов (с разделителями табуляции). При первом указании он заполняется пустыми путями. Это означает, что эти файлы отсутствуют в целевых каталогах, доступ к ним запрещен, они имеют недопустимое имя или находятся в нескольких каталогах. файл сопоставления путей Hello может быть вручную отредактированные tooinclude hello правильного целевого пути, указанные снова для пути к файлам hello hello средство tooresolve правильно.  |
|     /ExportBlobListFile:&lt;ExportBlobListFile&gt; | **Обязательный**. Применяется только для команды PreviewExport.<br/> Путь toohello XML файлу, содержащему список путей больших двоичных объектов или префиксов для экспорта toobe большие двоичные объекты hello. формат файла Hello hello же hello большой двоичный объект списка больших двоичных объектов в формат hello операцией вставки задания из REST API службы импорта и экспорта hello.  |
|     /DriveSize:&lt;DriveSize&gt; | **Обязательный**. Применяется только для команды PreviewExport.<br/>  Размер toobe диски, используемые для экспорта. Пример: 500 ГБ, 1,5 ТБ. Примечание: 1 ГБ = 1 000 000 000 байтов, 1 ТБ = 1 000 000 000 000 байтов.  |
|     /DataSet:&lt;dataset.csv&gt; | **Обязательный**<br/> CSV-файл, содержащий список каталогов или список toobe файлы скопированы tootarget дисков.  |
|     /silentmode  | **Необязательно**.<br/> Не указан, будет напоминать о требование дисков hello и требуют toocontinue вашего подтверждения.  |

## <a name="tool-output"></a>Выходные данные инструмента

### <a name="sample-drive-manifest-file"></a>Пример файла манифеста диска

```xml
<?xml version="1.0" encoding="UTF-8"?>
<DriveManifest Version="2011-MM-DD">
   <Drive>
      <DriveId>drive-id</DriveId>
      <StorageAccountKey>storage-account-key</StorageAccountKey>
      <ClientCreator>client-creator</ClientCreator>
      <!-- First Blob List -->
      <BlobList Id="session#1-0">
         <!-- Global properties and metadata that applies tooall blobs -->
         <MetadataPath Hash="md5-hash">global-metadata-file-path</MetadataPath>
         <PropertiesPath Hash="md5-hash">global-properties-file-path</PropertiesPath>
         <!-- First Blob -->
         <Blob>
            <BlobPath>blob-path-relative-to-account</BlobPath>
            <FilePath>file-path-relative-to-transfer-disk</FilePath>
            <ClientData>client-data</ClientData>
            <Length>content-length</Length>
            <ImportDisposition>import-disposition</ImportDisposition>
            <!-- page-range-list-or-block-list -->
            <!-- page-range-list -->
            <PageRangeList>
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
            </PageRangeList>
            <!-- block-list -->
            <BlockList>
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
            </BlockList>
            <MetadataPath Hash="md5-hash">metadata-file-path</MetadataPath>
            <PropertiesPath Hash="md5-hash">properties-file-path</PropertiesPath>
         </Blob>
      </BlobList>
   </Drive>
</DriveManifest>
```

### <a name="sample-journal-file-xml-for-each-drive"></a>Пример файла журнала для каждого диска (XML-файл)

```xml
[BeginUpdateRecord][2016/11/01 21:22:25.379][Type:ActivityRecord]
ActivityId: DriveInfo
DriveState: [BeginValue]
<?xml version="1.0" encoding="UTF-8"?>
<Drive>
   <DriveId>drive-id</DriveId>
   <BitLockerKey>*******</BitLockerKey>
   <ManifestFile>\DriveManifest.xml</ManifestFile>
   <ManifestHash>D863FE44F861AE0DA4DCEAEEFFCCCE68</ManifestHash> </Drive>
[EndValue]
SaveCommandOutput: Completed
[EndUpdateRecord]
```

### <a name="sample-journal-file-jrn-for-session-that-records-hello-trail-of-sessions"></a>Пример файла журнала (JRN) для сеанса, который записывает журнал hello сеансов

```
[BeginUpdateRecord][2016/11/02 18:24:14.735][Type:NewJournalFile]
VocabularyVersion: 2013-02-01
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.749][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
LogDirectory: F:\logs
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.754][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
StorageAccountKey: *******
[EndUpdateRecord]
```

## <a name="faq"></a>Часто задаваемые вопросы

### <a name="general"></a>Общие сведения

#### <a name="what-is-waimportexport-tool"></a>Что такое средство WAImportExport?

Средство WAImportExport Hello — hello диск средство подготовки и восстановления, можно использовать с hello службы импорта и экспорта Microsoft Azure. Можно использовать этот инструмент toocopy данных toohello жестких дисков будет центр обработки данных Azure tooan tooship. После завершения задания импорта, можно использовать этот инструмент toorepair все большие двоичные объекты, которые были повреждены, были потеряны или конфликтуют с другими большими двоичными объектами. После получения hello диски с выполненным заданием экспорта, можно использовать этот инструмент toorepair все файлы, которые были повреждены или отсутствуют на дисках hello.

#### <a name="how-does-hello-waimportexport-tool-work-on-multiple-source-dir-and-disks"></a>Как hello выполняет средство WAImportExport работают на нескольких dir источника и диски?

Если размер данных hello больше, чем размер диска hello, средство WAImportExport hello распространять hello данных между дисками hello оптимальным образом. копирование toomultiple Hello данных дисков может выполняться параллельно или последовательно. Нет ограничений на hello число дисков данных hello могут быть записаны toosimultaneously. Средство Hello будет распространять данные, на основе места на диске и размера папки. Он выбирает диск hello, наиболее оптимизирован для размер объекта hello. Здравствуйте данных при отправке учетной записи хранилища toohello быть переведено обратно toohello указан структуру каталогов.

#### <a name="where-can-i-find-previous-version-of-waimportexport-tool"></a>Где можно найти предыдущую версию средства WAImportExport?

Средство WAImportExport поддерживает все те же функции, что и его первая версия. Средство WAImportExport позволяет пользователям toospecify несколькими источниками и записи toomultiple дисков. Кроме того один позволяет легко управлять различные расположения исходных файлов, из которых данные hello должны toobe копируются в одном CSV-файле. Однако в случае необходим SAS поддерживает либо использовать диск toosingle toocopy одного источника, вы можете [загрузить средство WAImportExport V1] (http://go.Microsoft.com/fwlink/?) LinkID = 301900&amp;clcid = 0x409) и ссылаться слишком[WAImportExport V1 ссылка](storage-import-export-tool-how-to-v1.md) для получения справки по использованию WAImportExport V1.

#### <a name="what-is-a-session-id"></a>Что такое идентификатор сеанса?

Средство Hello ожидает сеанса копирования hello (или идентификатор) параметр toobe hello таким же, если намерение hello toospread hello данные на нескольких дисках. Поддержание hello таким же именем сеанса копирования hello включит toocopy данные пользователя с одним или несколькими расположения исходных файлов в один или несколько дисков и папки назначения. Поддержание таким же идентификатором сеанса позволяет toopick средство hello hello копию файлов, из которой она была оставлена hello время последнего.

Тем не менее одного сеанса копирования не может быть учетных записей хранилища используется tooimport данных toodifferent.

Когда сеанс копирования оно же между несколькими запусками средства hello, hello файла журнала (/ logdir) и ключ учетной записи хранения (/ sk) является также ожидаемый toobe hello таким же.

Идентификатор сеанса может содержать буквы, цифры от 0 до 9, а также символ подчеркивания (\_), тире (-) или хэш (#). Его длина должна быть от 3 до 30 символов.

Например, session-1, session#1 или session\_1.

#### <a name="what-is-a-journal-file"></a>Что такое файл журнала?

Каждый раз при запуске hello WAImportExport средство toocopy toohello жесткий диск для файлов, hello средство создает сеанс копирования. состояние сеанса копирования hello Hello записывается toohello файла журнала. Если сеанс копирования прерывается (например, из-за потери питания системы tooa), его можно возобновить, запустив средство hello повторно и указывая файл журнала hello в командной строке hello.

Для каждого жесткого диска, который вы подготавливаете с hello средство импорта и экспорта Azure, hello средство создает один файл журнала с именем «&lt;ID_диска с помощью&gt;.xml «где идентификатор диска — hello серийный номер связан toohello диск, на котором hello средство считывает из диск Hello. Вам потребуется hello файлы журнала из всех задания импорта hello toocreate дисков. Hello файл журнала также может быть подготовки диска используется tooresume, если средство hello прерывается.

#### <a name="what-is-a-log-directory"></a>Что такое каталог журнала?

каталог журнала Hello указывает directory toobe toostore подробных журналов, а также временных файлов манифеста. Если не указан, текущий каталог hello будет использоваться как каталог журнала hello. журналы Hello являются подробных журналов.

### <a name="prerequisites"></a>Предварительные требования

#### <a name="what-are-hello-specifications-of-my-disk"></a>Что такое hello спецификации компьютере?

Пустой SATAII 2,5 дюйма или 3,5 дюймовых или III или SSD жестких дисков toohello подключенного машина для копирования.

#### <a name="how-can-i-enable-bitlocker-on-my-machine"></a>Как включить BitLocker на моем компьютере?

Простой способ toocheck — щелкните правой кнопкой мыши на системном диске. Он покажет параметры для Bitlocker, если включена возможность hello. а если нет, эти параметры отображаться не будут.

![Проверка BitLocker](./media/storage-import-export-tool-preparing-hard-drives-import/BitLocker.png)

Вот статьи на [как tooenable BitLocker](https://technet.microsoft.com/library/cc766295.aspx)

На вашем компьютере может отсутствовать микросхема доверенного платформенного модуля (TPM). Если вы не получите выходные данные с помощью tpm.msc, посмотрите hello ответе на следующий ВОПРОС.

#### <a name="how-toodisable-trusted-platform-module-tpm-in-bitlocker"></a>Как toodisable доверенный платформенный модуль (TPM) в BitLocker?
> [!NOTE]
> Только в том случае, если имеется без доверенного платформенного МОДУЛЯ в серверах, необходимо toodisable доверенного платформенного МОДУЛЯ политики. Это не необходимые toodisable доверенного платформенного МОДУЛЯ, если сервер пользователя доверенный платформенный модуль. 
> 

В порядке toodisable доверенного платформенного МОДУЛЯ в BitLocker необходимо пройти hello следующие шаги:<br/>
1. Запустите **редактор групповых политик**. Для этого в окне командной строки введите команду gpedit.msc. Если **групповыми политиками** отображается как недоступная для включения BitLocker, сначала, toobe. См. предыдущий часто задаваемый вопрос.
2. Выберите **Политика локального компьютера &gt; Конфигурация компьютера &gt; Административные шаблоны &gt; Компоненты Windows &gt; Шифрование диска BitLocker &gt; Диски операционной системы**.
3. Измените политику **Обязательная дополнительная проверка подлинности при запуске**.
4. Задать политику hello слишком**включено** и убедитесь, что **разрешить использование BitLocker без совместимого TPM** проверяется.

####  <a name="how-toocheck-if-net-4-or-higher-version-is-installed-on-my-machine"></a>Как toocheck .NET 4 или более поздней версии установлен на моем компьютере?

Все версии Microsoft .NET Framework устанавливаются в следующем каталоге: %windir%\Microsoft.NET\Framework\.

Перейдите toohello над упомянутых частью на целевом компьютере, где hello средство должно toorun. Найдите папку, имя которой начинается с v4. Если эта папка отсутствует, это означает, что на компьютере не установлена платформа .NET 4. Ее можно скачать с сайта [Microsoft .NET Framework 4 (веб-установщик)](https://www.microsoft.com/download/details.aspx?id=17851).

### <a name="limits"></a>Ограничения

#### <a name="how-many-drives-can-i-preparesend-at-hello-same-time"></a>Сколько дисков можно ли подготовить или отправке на hello одновременно?

Нет ограничения на hello количество дисков, которые hello средства можно подготовить. Однако средство hello ожидает, что буквы дисков в качестве входных данных. Это ограничивает too25 подготовки дисков одновременно. В рамках одного задания одновременно можно обрабатывать не более 10 дисков. При подготовке больше 10 дисков для различных версий Здравствуйте учетную запись хранения, hello диски можно распределить между несколькими заданиями.

#### <a name="can-i-target-more-than-one-storage-account"></a>Можно ли назначить более одной учетной записи хранения?

В рамках одного задания и одного сеанса копирования можно отправить только одну учетную запись хранения.

### <a name="capabilities"></a>Возможности

#### <a name="does-waimportexportexe-encrypt-my-data"></a>Шифрует ли средство WAImportExport.exe данные?

Да. Для этого процесса требуется шифрование, поэтому это средство выполняет шифрование на основе технологии BitLocker.

#### <a name="what-will-be-hello-hierarchy-of-my-data-when-it-appears-in-hello-storage-account"></a>Когда он появится в учетной записи хранения hello, каким будет hello иерархии данных?

Несмотря на то, что данные распределяются по дискам, hello данных при отправке toohello учетной записи хранилища, на которые будет схождение выполнено резервное toohello структуру каталогов, указанных в файле CSV hello набора данных.

#### <a name="how-many-of-hello-input-disks-will-have-active-io-in-parallel-when-copy-is-in-progress"></a>Сколько hello введенных диски имеют активные операции ввода-ВЫВОДА в параллельном режиме, когда идет копирование?

Средство Hello распределяет данные по hello входной диски на основе размера hello hello входных файлов. С другой стороны, полностью delends hello число активных дисков параллельно природе hello hello входных данных. В зависимости от размера hello отдельных файлов во входном наборе данных hello один или несколько дисков может отображать активные операции ввода-ВЫВОДА в параллельном режиме. Чтобы получить дополнительные сведения, ознакомьтесь со следующим вопросом.

#### <a name="how-does-hello-tool-distribute-hello-files-across-hello-disks"></a>Как средство hello распределить файлы hello на hello дисков?

Средство WAImportExport выполняет операции чтения и записи файлов пакет за пакетом. Каждый пакет содержит не более 100 000 файлов. Это означает, что одновременно средство может записать не более 100 000 файлов. Несколько дисков, записываемых toosimultaneously, если эти файлы 100000 распределенных toomulti дисков. Однако ли hello программа записывает toomultiple дисков одновременно или одного диска зависит от hello совокупный размер пакета hello. Например в случае меньшие файлы при одновременном 10,0000 файлов может toofit на одном диске, средство запишет tooonly один диск во время обработки hello этого пакета.

### <a name="waimportexport-output"></a>Выходные данные WAImportExport

#### <a name="there-are-two-journal-files-which-one-should-i-upload-tooazure-portal"></a>Существуют два файла журнала, какой из них следует отправить tooAzure портала?

**XML-файла** -для каждого жесткого диска, который вы подготавливаете с помощью средства WAImportExport hello, hello средство создает один файл журнала с именем `<DriveID>.xml` где ID_диска с помощью — hello серийный номер связан toohello диск, на котором hello средство считывает из hello диска. Вам потребуется hello файлы журнала из всех задания импорта hello toocreate дисков в hello портал Azure. Этот файл журнала также может быть подготовки диска используется tooresume, если средство hello прерывается.

**.jrn** -hello файла журнала с суффиксом `.jrn` содержит hello состояние для всех сеансов копирования для жесткого диска. Он также содержит сведения hello необходимости toocreate hello задания импорта. Всегда необходимо указать файл журнала после выполнения средства WAImportExport hello, а также сеанс копирования по идентификатору.

## <a name="next-steps"></a>Дальнейшие действия

* [Установка hello средство импорта и экспорта Azure](storage-import-export-tool-setup.md)
* [Настройка свойств и метаданных во время hello процессе импорта](storage-import-export-tool-setting-properties-metadata-import.md)
* [Образец рабочего процесса tooprepare жесткие диски для задания импорта](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
* [Краткий справочник по часто используемым командам](storage-import-export-tool-quick-reference.md) 
* [Просмотр состояния задания с помощью файлов журнала копирования](storage-import-export-tool-reviewing-job-status-v1.md)
* [Подготовка задания импорта](storage-import-export-tool-repairing-an-import-job-v1.md)
* [Подготовка задания экспорта](storage-import-export-tool-repairing-an-export-job-v1.md)
* [Устранение неполадок средства импорта и экспорта Azure hello](storage-import-export-tool-troubleshooting-v1.md)
