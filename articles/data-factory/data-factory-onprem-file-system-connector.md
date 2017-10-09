---
title: "aaaCopy данных из файловой системы, с помощью фабрики данных Azure | Документы Microsoft"
description: "Узнайте, как toocopy tooand данных из локальной файловой системы с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 201b8bc3ffa639df781443aa0c3f95c975d280be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-an-on-premises-file-system-by-using-azure-data-factory"></a>Копирование данных tooand из локальной файловой системы с помощью фабрики данных Azure
В этой статье объясняется, как toouse hello действие копирования в данных toocopy фабрики данных Azure из локальной файловой системы. Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.

## <a name="supported-scenarios"></a>Поддерживаемые сценарии использования.
Можно скопировать данные **из локальной файловой системы** toohello следующие хранилищ данных:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Можно скопировать данные из hello, следуя хранилищ данных **tooan в локальной файловой системе**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> Действие копирования не удаляет исходный файл hello после назначения успешно скопированного toohello. Если вам требуется toodelete hello исходного файла после успешным копированием, создайте файл hello toodelete пользовательское действие и действие hello используется в конвейере hello. 

## <a name="enabling-connectivity"></a>Включение соединения
Фабрика данных поддерживает подключения tooand из локальной файловой системы через **шлюз управления данными**. Необходимо установить hello шлюз управления данными в локальной среде hello фабрики данных службы tooconnect tooany поддерживаемые локальные данные хранилища в том числе файловой системы. toolearn о шлюз управления данными и получить пошаговые инструкции по настройке шлюза hello. в разделе [перемещения данных между локальным источникам и hello облако с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md). Помимо шлюз управления данными другие двоичные файлы должны установить toobe toocommunicate tooand из локальной файловой системы. Необходимо установить и использовать hello шлюз управления данными, даже когда hello файловой системы на виртуальной Машине Azure IaaS. Подробные сведения о шлюзе hello. в разделе [шлюз управления данными](data-factory-data-management-gateway.md).

Установка toouse общую папку Linux [Samba](https://www.samba.org/) на сервер Linux и установить шлюз управления данными на сервере Windows. Установка шлюза управления данными на сервер Linux не поддерживается.

## <a name="getting-started"></a>Приступая к работе
Можно создать конвейер с действием копирования, которое перемещает данные из файловой системы и обратно с помощью различных средств и API-интерфейсов.

toocreate простым способом Hello конвейера — toouse hello **мастер копирования**. В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.

Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**. В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.

Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.

1. Создание **фабрики данных**. Фабрика данных может содержать один или несколько конвейеров. 
2. Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных. Например при копировании данных из больших двоичных объектов Azure хранилища tooan в локальной файловой системы создается две связанные службы toolink в локальной файловой системы и фабрики данных tooyour учетной записи хранилища Azure. Свойства связанной службы, определенные tooan в локальной файловой системе, в разделе [связанные свойства службы](#linked-service-properties) раздела.
3. Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования. В примере hello, упомянутые в последнем шаге hello создать контейнер больших двоичных объектов dataset toospecify hello и папку, содержащую hello входных данных. И создать другой набор данных toospecify hello папку и имя файла (необязательно) в файловой системе. Свойства набора данных, определенных tooon в локальной файловой системе, см. в разделе [свойства набора данных](#dataset-properties) раздела.
4. Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных. В примере hello приведенные выше используются BlobSource в исходной и FileSystemSink в приемник для действия копирования hello. Аналогично при копировании из локального файла системы tooAzure хранилища BLOB-объектов используется FileSystemSource и BlobSink в действии копирования hello. Свойства действия копирования, определенные tooon в локальной файловой системе, см. в разделе [скопировать свойства действия](#copy-activity-properties) раздела. Дополнительные сведения о том, как toouse хранилища данных, как источник или приемник по ссылке hello в предыдущем разделе hello для источника данных.

При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически. При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.  Образцы с определениями JSON для сущностей фабрики данных, используемых toocopy данные из файловой системы см. в разделе [JSON примеры](#json-examples-for-copying-data-to-and-from-file-system) этой статьи.

Hello в следующих разделах содержатся сведения о свойствах JSON, которые являются системными toofile определенных сущностей фабрики данных используется toodefine:

## <a name="linked-service-properties"></a>Свойства связанной службы
Можно связать локального файла tooan данных Azure заводе hello **файловый сервер в локальной** связанной службы. Привет, в следующей таблице приводится описание JSON элементы, которые являются определенной toohello файловый сервер в локальной связанной службы.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| type |Убедитесь, что свойство типа hello слишком**OnPremisesFileServer**. |Да |
| host |Указывает путь к корневому каталогу hello hello папке, что toocopy. Использовать hello escape-символ "\" для специальных символов в строке приветствия. Примеры приведены в разделе [Примеры определений связанной службы и набора данных](#sample-linked-service-and-dataset-definitions). |Да |
| userid |Укажите идентификатор hello hello пользователя, имеющего доступ toohello сервера. |Нет (если выбрать encryptedcredential) |
| пароль |Задать пароль hello hello пользователя (userid). |Нет (если выбрать encryptedcredential) |
| encryptedCredential |Укажите hello зашифрованные учетные данные, которые можно получить, выполнив командлет New-AzureRmDataFactoryEncryptValue hello. |Нет (Если вы выберете toospecify идентификатор пользователя и пароль в виде обычного текста) |
| gatewayName |Указывает имя фабрики данных для использования локального файла tooconnect toohello сервера шлюза hello hello. |Да |


### <a name="sample-linked-service-and-dataset-definitions"></a>Примеры определений связанной службы и набора данных
| Сценарий | Размещение в определении связанной службы | Путь к файлу в определении набора данных |
| --- | --- | --- |
| Локальная папка на компьютере со шлюзом управления данными. <br/><br/>Примеры: "D:\\\\*" или "D:\папка\вложенная_папка\\\*" |"D:\\\\" (для шлюза управления данными 2.0 и более поздних версий) <br/><br/> localhost (для версий, предшествующих версии 2.0 шлюза управления данными) |.\\\\ или "папка\\\\вложенная_папка" (для шлюза управления данными 2.0 и более поздних версий) <br/><br/>"D:\\\\" или "D:\\\\папка\\\\вложенная_папка" (для шлюза версии ниже 2.0) |
| Удаленная общая папка: <br/><br/>Примеры: "\\\\сервер\\общая_папка\\\*" или "\\\\сервер\\общая_папка\\папка\\вложенная_папка\\*" |\\\\\\\\сервер\\\\общая_папка |.\\\\ или "папка\\\\вложенная_папка" |


### <a name="example-using-username-and-password-in-plain-text"></a>Пример указания имени пользователя и пароля в виде обычного текста

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

### <a name="example-using-encryptedcredential"></a>Пример использования encryptedcredential

```JSON
{
  "Name": " OnPremisesFileServerLinkedService ",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "D:\\",
      "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
      "gatewayName": "mygateway"
    }
  }
}
```

## <a name="dataset-properties"></a>Свойства набора данных
Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Наборы данных в фабрике данных Azure](data-factory-create-datasets.md). Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных.

раздел typeProperties Hello отличается для каждого типа набора данных. Он предоставляет сведения, такие как расположение hello и формат данных hello в хранилище данных hello. Hello typeProperties статьи для набора данных hello типа **FileShare** имеет следующие свойства hello:

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| folderPath |Указывает папку toohello вложенным hello. Использовать hello escape-символ "\" для специальных символов в строке приветствия. Примеры приведены в разделе [Примеры определений связанной службы и набора данных](#sample-linked-service-and-dataset-definitions).<br/><br/>Можно объединять с помощью этого свойства **partitionBy** toohave пути к папке зависимости среза дат начала и окончания. |Да |
| fileName |Укажите имя файла hello hello в hello **folderPath** Если hello таблицы toorefer tooa конкретный файл в папку hello. Если не указано значение для этого свойства, таблица hello указывает tooall файлы в папке hello.<br/><br/>При **fileName** не указано для выходной набор данных и **preserveHierarchy** не указан в приемник действия hello hello созданный файл имеет имя в hello следующий формат: <br/><br/>`Data.<Guid>.txt` (пример: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Нет |
| fileFilter |Укажите toobe фильтра используется tooselect подмножества файлов в hello folderPath, а не всех файлов. <br/><br/>Допустимые значения: `*` (несколько знаков) и `?` (один знак).<br/><br/>Пример 1: "fileFilter": "*.log"<br/>Пример 2: "fileFilter": 2014-1-?.txt"<br/><br/>Обратите внимание, что свойство fileFilter применяется к входному набору данных FileShare. |Нет |
| partitionedBy |PartitionedBy toospecify динамический folderPath и fileName можно использовать для временного ряда данных. Например, можно параметризовать значение folderPath для каждого часа получения данных. |Нет |
| свойства | поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Набор hello **тип** свойства в формате tooone из следующих значений. Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Если требуется слишком**скопируйте файлы как-является** между файловых хранилищ (двоичный копия), пропустите раздел формат hello в оба определения набора входных и выходных данных. |Нет |
| compression | Укажите тип hello и уровень сжатия данных hello. Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**. Поддерживаемые уровни: **Optimal** и **Fastest**. См. сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Нет |

> [!NOTE]
> Свойства filename и fileFilter невозможно использовать одновременно.

### <a name="using-partitionedby-property"></a>Использование свойства partitionedBy
Как упоминалось в предыдущем разделе hello, можно указать динамического folderPath и filename для временного ряда данных с hello **partitionedBy** свойства [функции фабрики данных, а системные переменные hello](data-factory-functions-variables.md).

см. Дополнительные сведения о наборах данных временных рядов, планирования и срезов, toounderstand [Создание наборов данных](data-factory-create-datasets.md), [планирования и выполнения](data-factory-scheduling-and-execution.md), и [Создание конвейеры](data-factory-create-pipelines.md).

#### <a name="sample-1"></a>Пример 1

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

В этом примере {Slice} заменяется значение hello hello системной переменной фабрики данных SliceStart в формате hello (ГГГГММДДЧЧ). SliceStart ссылается toostart время hello среза. Hello folderPath отличается для каждого среза. Например: wikidatagateway/wikisampledataout/2014100103 или wikidatagateway/wikisampledataout/2014100104.

#### <a name="sample-2"></a>Пример 2

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

В этом примере год, месяц, день и время SliceStart извлекаются в отдельные переменные, используемые свойства hello folderPath и fileName.

## <a name="copy-activity-properties"></a>Свойства действия копирования
Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи. Свойства, например имя, описание, входные и выходные таблицы, политики и т. д., доступны для всех типов действий. В то время как свойства, доступные в hello **typeProperties** раздел hello действия зависят от типа каждого действия.

Для действия копирования они зависят от типов источников и приемников hello. При перемещении данных из файловой системы в локальной установке hello исходного типа в действие копирования hello слишком**FileSystemSource**. Аналогичным образом, при перемещении данных tooan в локальной файловой системы, установите тип приемника hello в действии копирования hello слишком**FileSystemSink**. Этот раздел содержит список свойств, поддерживаемых типами FileSystemSource и FileSystemSink.

**FileSystemSource** поддерживает hello следующие свойства:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| recursive |Указывает, доступна ли для чтения рекурсивно hello данные из вложенных папок hello или только пользователей из указанной папки hello. |True, False (по умолчанию) |Нет |

**FileSystemSink** поддерживает hello следующие свойства:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| copyBehavior |Определяет поведение копирования hello, когда источник hello BlobSource или файловой системы. |**PreserveHierarchy:** сохраняет hello иерархию файлов в целевой папке hello. То есть относительный путь hello hello исходный файл toohello исходную папку hello такой же, как относительный путь hello hello целевой файл toohello целевую папку.<br/><br/>**FlattenHierarchy:** все файлы из исходной папки hello создаются в первый уровень hello целевую папку. Hello целевые файлы создаются с автоматически созданным именем.<br/><br/>**MergeFiles:** объединяет все файлы из папки tooone hello исходного файла. Если указано имя BLOB-объекта или имени файла hello hello объединенный файл называется hello указанным именем. В противном случае присваивается автоматически созданное имя файла. |Нет |

### <a name="recursive-and-copybehavior-examples"></a>Примеры recursive и copyBehavior
Этот раздел описывает поведение функции hello операции копирования для различных сочетаний значений для свойств рекурсивные и copyBehavior hello hello.

| Значение recursive | Значение copyBehavior | Результаты выполнения операции |
| --- | --- | --- |
| Да |preserveHierarchy |Источник папку Folder1 hello следующая структура,<br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5<br/><br/>Hello целевую папку Folder1 создается с таким же структуру как исходной hello hello.<br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5 |
| Да |flattenHierarchy |Источник папку Folder1 hello следующая структура,<br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5<br/><br/>целевой Hello папка1 создана следующая структура hello: <br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл1"<br/>&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл2"<br/>&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл3"<br/>&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл4"<br/>&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл5" |
| Да |mergeFiles |Источник папку Folder1 hello следующая структура,<br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5<br/><br/>целевой Hello папка1 создана следующая структура hello: <br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Содержимое файлов "Файл1", "Файл2", "Файл3", "Файл4" и "Файл5" объединяется в один файл с автоматически созданным именем. |
| нет |preserveHierarchy |Источник папку Folder1 hello следующая структура,<br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5<br/><br/>Hello целевую папку Folder1 создана следующая структура hello:<br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл2<br/><br/>Папка "Вложенная_папка1" с файлами "Файл3", "Файл4" и "Файл5" не будет включена в эту папку. |
| нет |flattenHierarchy |Источник папку Folder1 hello следующая структура,<br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5<br/><br/>Hello целевую папку Folder1 создана следующая структура hello:<br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл1"<br/>&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл2"<br/><br/>Папка "Вложенная_папка1" с файлами "Файл3", "Файл4" и "Файл5" не будет включена в эту папку. |
| нет |mergeFiles |Источник папку Folder1 hello следующая структура,<br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5<br/><br/>Hello целевую папку Folder1 создана следующая структура hello:<br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Содержимое файлов "Файл1" и "Файл2" объединяется в один файл с автоматически созданным именем.<br/>&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл1"<br/><br/>Папка "Вложенная_папка1" с файлами "Файл3", "Файл4" и "Файл5" не будет включена в эту папку. |

## <a name="supported-file-and-compression-formats"></a>Поддерживаемые форматы файлов и сжатия
Дополнительные сведения см. в статье [Форматы файлов и сжатия данных, поддерживаемые фабрикой данных Azure](data-factory-supported-file-and-compression-formats.md).

## <a name="json-examples-for-copying-data-tooand-from-file-system"></a>Примеры JSON для копирования данных tooand из файловой системы
Hello ниже приведены примеры определения образца JSON можно использовать toocreate конвейера с помощью hello [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Они показывают как toocopy tooand данных из хранилища больших двоичных объектов Azure и локальной файловой системе. Тем не менее, можно скопировать данные *непосредственно* из любого tooany источников hello hello приемников, перечисленных в [поддерживаемые источники и приемники](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью копирования действия в фабрике данных Azure.

### <a name="example-copy-data-from-an-on-premises-file-system-tooazure-blob-storage"></a>Пример: Копирование данных из tooAzure системы файл локального хранилища больших двоичных объектов
В этом примере показано, как данные toocopy из tooAzure системы файл локального хранилища больших двоичных объектов. Образец Hello имеет hello, следуя сущностей фабрики данных.

* Связанная служба типа [OnPremisesFileServer](#linked-service-properties).
* Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Входной [набор данных](data-factory-create-datasets.md) типа [FileShare](#dataset-properties).
* Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* [Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [FileSystemSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Следующий образец Hello копирует данные временных рядов с tooAzure системы файл локального хранилища больших двоичных объектов каждый час. свойства Hello JSON, используемые в этих примерах описаны в разделах hello после образцы hello.

В качестве первого шага, настроить шлюз управления данными согласно инструкциям hello [перемещения данных между локальным источникам и hello облако с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md).

**Связанная служба локального файлового сервера**

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

Мы рекомендуем использовать hello **encryptedCredential** свойство вместо hello **userid** и **пароль** свойства. Подробные сведения о связанной службе файлового сервера см. в [соответствующем разделе](#linked-service-properties).

**Связанная служба хранилища Azure**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

**Входной набор данных локальной файловой системы**

Данные берутся из нового файла каждый час. Здравствуйте, folderPath и fileName свойства определяются на основе времени начала hello hello среза.  

Параметр `"external": "true"` информирует фабрики данных, набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.

```JSON
{
  "name": "OnpremisesFileSystemInput",
  "properties": {
    "type": " FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ]
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

**Выходной набор данных хранилища BLOB-объектов Azure**

Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1). путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается. путь к папке Hello использует hello года, месяца, дня и часа части времени начала hello.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Действие копирования в конвейере с файловой системой в качестве источника и BLOB-объектом в качестве приемника**

Hello конвейера содержит операции копирования, настроенные toouse hello наборы входных и выходных данных, а — запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**FileSystemSource**, и **приемник** тип установлен слишком**BlobSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T19:00:00",
    "description":"Pipeline for copy activity",
    "activities":[  
      {
        "name": "OnpremisesFileSystemtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "OnpremisesFileSystemInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "FileSystemSource"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```

### <a name="example-copy-data-from-azure-sql-database-tooan-on-premises-file-system"></a>Пример: Копирование данных из базы данных SQL Azure tooan в локальной файловой системы
Hello следующем образце показано:

* Связанная служба типа [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).
* Связанная служба типа [OnPremisesFileServer](#linked-service-properties).
* Входной набор данных типа [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
* Выходной набор данных типа [FileShare](#dataset-properties).
* Конвейер с действием копирования, в котором используются [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) и [FileSystemSink](#copy-activity-properties).

Образец Hello копирует данные временных рядов с Azure SQL таблицы tooan в локальной файловой системе каждый час. После образцы hello Hello JSON свойства, которые используются в образцах описаны в разделах.

**Связанная служба базы данных SQL Azure:**

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```

**Связанная служба локального файлового сервера**

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

Мы рекомендуем использовать hello **encryptedCredential** свойство вместо использования hello **userid** и **пароль** свойства. Подробные сведения о связанной службе файловой системы см. в [соответствующем разделе](#linked-service-properties).

**Входной набор данных SQL Azure**

Образец Hello предполагается, что вы создали таблицу «MyTable» в Azure SQL и она содержит столбец с именем «timestampcolumn» для данных временных рядов.

Параметр ``“external”: ”true”`` информирует фабрики данных, набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

**Выходной набор данных локальной файловой системы**

Данные — новый файл скопированный tooa каждый час. Hello folderPath и fileName для большого двоичного объекта hello определяются на основе времени начала hello hello среза.

```JSON
{
  "name": "OnpremisesFileSystemOutput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ]
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

**Действие копирования в конвейере с базой данных SQL в качестве источника и файловой системой в качестве приемника**

Hello конвейера содержит операции копирования, настроенные toouse hello наборы входных и выходных данных, а — запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**SqlSource**и hello **приемник** тип установлен слишком**FileSystemSink**. Hello SQL-запрос, указанный для hello **SqlReaderQuery** свойство выбирает данные hello в hello за час toocopy.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T20:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoOnPremisesFile",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "OnpremisesFileSystemOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "FileSystemSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 3,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```


Также можно сопоставить столбцы из источника toocolumns набора данных из набора данных приемник в определении действия копирования hello. Дополнительные сведения см. в статье [Сопоставление столбцов исходного набора данных со столбцами целевого набора данных](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Производительность и настройка
 toolearn о ключе факторы, производительность hello влияние перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize, разделе hello [действие копирования производительности и руководство по настройке](data-factory-copy-activity-performance.md).
