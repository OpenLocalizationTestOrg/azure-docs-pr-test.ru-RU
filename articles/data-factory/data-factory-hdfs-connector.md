---
title: "aaaMove данных из HDFS в локальной среде | Документы Microsoft"
description: "Дополнительные сведения о том, как toomove данные из локальной HDFS, с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3215b82d-291a-46db-8478-eac1a3219614
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 96387e5dd089099fc2e983ab26d67c2044b973b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a>Перемещение данных из локальной системы HDFS с помощью фабрики данных Azure
В этой статье объясняется, как toouse hello действие копирования в фабрике данных Azure toomove данных из HDFS в локальной среде. Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.

Можно скопировать данные из хранилища данных приемник tooany поддерживается HDFS. Список данных поддерживается хранилищ, приемники действием копирования hello см hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы. Фабрики данных в настоящее время поддерживает только перемещения данных из хранилищ данных tooother HDFS в локальной среде, но не для перемещения данных из других данных tooan хранилищ локальной HDFS.

> [!NOTE]
> Действие копирования не удаляет исходный файл hello после назначения успешно скопированного toohello. Если вам требуется toodelete hello исходного файла после успешным копированием, создайте файл hello toodelete пользовательское действие и действие hello используется в конвейере hello. 

## <a name="enabling-connectivity"></a>Включение соединения
Служба фабрики данных поддерживает подключения локальной tooon HDFS, с помощью hello шлюз управления данными. В разделе [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) toolearn статьи о шлюз управления данными и пошаговые инструкции по настройке шлюза hello. Используйте tooHDFS tooconnect шлюза hello, даже если она размещается на виртуальной Машине Azure IaaS.

> [!NOTE]
> Убедитесь, что hello шлюз управления данными можно получить доступ к слишком**все** hello [имя узла сервера]: [порт узла name] и [серверов узла данных]: [порт данных узла] hello кластера Hadoop. По умолчанию используются [порт_узла_имен] 50070 и [порт_узла_данных] 50075.

Хотя можно установить шлюз на hello же локального компьютера или виртуальной Машине Azure hello как hello HDFS, рекомендуется устанавливать шлюз hello на отдельных машин/Azure IaaS виртуальной Машины. Если для шлюза будет выделен отдельный компьютер, это минимизирует вероятность конфликта ресурсов и повысит производительность. При установке шлюза hello на отдельном компьютере hello машина должна была машину hello может tooaccess с hello HDFS.

## <a name="getting-started"></a>Приступая к работе
Вы можете создать конвейер с действием копирования, которое перемещает данные из HDFS, с помощью разных средств и API-интерфейсов.

toocreate простым способом Hello конвейера — toouse hello **мастер копирования**. В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.

Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**. В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.

Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.

1. Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.
2. Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.
3. Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.

При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически. При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.  Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из хранилища данных HDFS см [пример JSON: копирование данных из HDFS в локальной среде tooAzure большого двоичного объекта](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) данной статьи.

Hello в следующих разделах подробно JSON свойства, которые являются определенной tooHDFS используется toodefine фабрики данных сущности:

## <a name="linked-service-properties"></a>Свойства связанной службы
Связанная служба связывает фабрику данных tooa хранилища данных. Создание связанной службы типа **Hdfs** toolink фабрикой данных tooyour HDFS в локальной среде. Hello в следующей таблице приводится описание службы конкретных tooHDFS связанные элементы JSON.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| type |свойство типа Hello должно быть присвоено: **Hdfs** |Да |
| URL-адрес |URL-адрес toohello HDFS |Да |
| authenticationType |Anonymous или Windows. <br><br> toouse **проверки подлинности Kerberos** HDFS соединителя, см. в разделе слишком[в этом разделе](#use-kerberos-authentication-for-hdfs-connector) tooset вверх в локальной среде соответствующим образом. |Да |
| userName |Имя пользователя для проверки подлинности Windows. |Да (для проверки подлинности Windows) |
| пароль |Пароль для проверки подлинности Windows. |Да (для проверки подлинности Windows) |
| gatewayName |Имя шлюза hello, hello служба фабрики данных следует использовать tooconnect toohello HDFS. |Да |
| encryptedCredential |[Новый AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) выходных данных учетные данные доступа hello. |Нет |

### <a name="using-anonymous-authentication"></a>Использовать анонимную проверку подлинности

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-windows-authentication"></a>Использовать проверку подлинности Windows

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```
## <a name="dataset-properties"></a>Свойства набора данных
Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи. Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).

Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello. Hello typeProperties статьи для набора данных типа **FileShare** (включает набор данных HDFS) имеет следующие свойства hello

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| folderPath |Путь к папке toohello. Пример: `myfolder`<br/><br/>Использовать escape-символ "\" для специальных символов в строке приветствия. Например, для "папка\вложенная_папка" укажите "папка\\\\вложенная_папка", а для "d:\пример_папки" укажите "d:\\\\пример_папки".<br/><br/>Можно объединять с помощью этого свойства **partitionBy** toohave пути к папке зависимости среза дат начала и окончания. |Да |
| fileName |Укажите имя файла hello hello в hello **folderPath** Если hello таблицы toorefer tooa конкретный файл в папку hello. Если не указано значение для этого свойства, таблица hello указывает tooall файлы в папке hello.<br/><br/>Если имя файла не указано для выходной набор данных, имя hello hello созданный файл может быть в hello в следующем формате: <br/><br/>Data<Guid>.txt (например, Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.). |Нет |
| partitionedBy |partitionedBy можно использовать toospecify динамического folderPath, имя файла для временного ряда данных. Например, путь к папке (folderPath) каждый час будет другим. |Нет |
| свойства | поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Набор hello **тип** свойства в формате tooone из следующих значений. Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Если требуется слишком**скопируйте файлы как-является** между файловых хранилищ (двоичный копия), пропустите раздел формат hello в оба определения набора входных и выходных данных. |Нет |
| compression | Укажите тип hello и уровень сжатия данных hello. Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**. Поддерживаемые уровни: **Optimal** и **Fastest**. См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Нет |

> [!NOTE]
> Свойства filename и fileFilter нельзя использовать одновременно.

### <a name="using-partionedby-property"></a>Использование свойства partionedBy
Как упоминалось в предыдущем разделе hello, можно указать динамического folderPath и filename для временного ряда данных с hello **partitionedBy** свойства [функции фабрики данных, а системные переменные hello](data-factory-functions-variables.md).

toolearn Дополнительные сведения о наборах данных ряда времени, планирования и срезов, в разделе [Создание наборов данных](data-factory-create-datasets.md), [планирования и исполнение](data-factory-scheduling-and-execution.md), и [Создание конвейеры](data-factory-create-pipelines.md) статей.

#### <a name="sample-1"></a>Пример 1

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
В этом примере {Slice} заменяется hello значение системной переменной фабрики данных SliceStart в формате hello (ГГГГММДДЧЧ) указан. Hello SliceStart ссылается toostart время hello среза. Hello folderPath отличается для каждого среза. Например: wikidatagateway/wikisampledataout/2014100103 или wikidatagateway/wikisampledataout/2014100104.

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
В этом примере год, месяц, день и время SliceStart извлекаются в отдельные переменные, используемые в свойствах folderPath и fileName.

## <a name="copy-activity-properties"></a>Свойства действия копирования
Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи. Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.

В то время как свойства в разделе typeProperties hello hello действия зависят от типа каждого действия. Для действия копирования они зависят от типов источников и приемников hello.

Для действия копирования, когда источник типа **FileSystemSource** hello следующие свойства доступны в разделе "typeProperties":

**FileSystemSource** поддерживает hello следующие свойства:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| recursive |Указывает, доступна ли для чтения рекурсивно hello данных из подпапок hello или только из указанной папки hello. |True, False (по умолчанию) |Нет |

## <a name="supported-file-and-compression-formats"></a>Поддерживаемые форматы файлов и сжатия
Дополнительные сведения см. в статье [Форматы файлов и сжатия данных, поддерживаемые фабрикой данных Azure](data-factory-supported-file-and-compression-formats.md).

## <a name="json-example-copy-data-from-on-premises-hdfs-tooazure-blob"></a>Пример JSON: копирование данных из HDFS в локальной среде tooAzure больших двоичных объектов
В этом примере показано, как данные toocopy из tooAzure HDFS локального хранилища больших двоичных объектов. Тем не менее, данные можно скопировать **непосредственно** tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.  

Образец Hello предоставляет определения JSON для hello, следуя сущностей фабрики данных. Можно использовать эти определения toocreate toocopy конвейера данных из HDFS tooAzure хранилища больших двоичных объектов с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).

1. Связанная служба типа [OnPremisesHdfs](#linked-service-properties).
2. Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Входной [набор данных](data-factory-create-datasets.md) типа [FileShare](#dataset-properties).
4. Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. [Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [FileSystemSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Образец Hello копирует данные из локальной HDFS tooan BLOB-объектов Azure каждый час. свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.

В качестве первого шага можно Настройте шлюз управления данными hello. Здравствуйте, инструкциям hello [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) статьи.

**HDFS связанной службы:** в этом примере используется hello проверку подлинности Windows. Сведения о различных типах аутентификации, которые можно использовать, см. в разделе [Свойства связанной службы HDFS](#linked-service-properties).

```JSON
{
    "name": "HDFSLinkedService",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

**Связанная служба хранилища Azure**

```JSON
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

**HDFS входной набор данных:** toohello HDFS папку DataTransfer/UnitTest ссылается этот набор данных или. конвейер Hello копирует все файлы hello в это место назначения toohello папки.

Параметр «external»: «true» уведомляет службу hello фабрики данных, что набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.

```JSON
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

**Выходной набор данных BLOB-объекта Azure**

Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1). путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается. путь к папке Hello использует года, месяца, дня и часа части времени начала hello.

```JSON
{
    "name": "OutputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/hdfs/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Действие копирования в конвейере с файловой системой в качестве источника и BLOB-объектом в качестве приемника**

конвейер Hello содержит операции копирования, настроенные toouse эти наборы входных и выходных данных. она запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**FileSystemSource** и **приемник** тип установлен слишком**BlobSink**. запрос SQL Hello, указанный для hello **запроса** свойство выбирает данные hello в hello за час toocopy.

```JSON
{
    "name": "pipeline",
    "properties":
    {
        "activities":
        [
            {
                "name": "HdfsToBlobCopy",
                "inputs": [ {"name": "InputDataset"} ],
                "outputs": [ {"name": "OutputDataset"} ],
                "type": "Copy",
                "typeProperties":
                {
                    "source":
                    {
                        "type": "FileSystemSource"
                    },
                    "sink":
                    {
                        "type": "BlobSink"
                    }
                },
                "policy":
                {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "00:05:00"
                }
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="use-kerberos-authentication-for-hdfs-connector"></a>Использование аутентификации Kerberos для соединителя HDFS
Существует два tooset параметры копирования hello в локальную среду так, чтобы toouse проверки подлинности Kerberos в соединитель HDFS. Можно выбрать один hello лучше подходит в случае.
* Способ 1. [Присоединение компьютера шлюза к области Kerberos](#kerberos-join-realm)
* Вариант 2. [Активация взаимного доверия между доменом Windows и областью Kerberos](#kerberos-mutual-trust).

### <a name="kerberos-join-realm"></a>Способ 1. Присоединение компьютера шлюза к области Kerberos

#### <a name="requirement"></a>Условие

* компьютер шлюза Hello должен сферы Kerberos toojoin hello и не удается подключиться к любому домену Windows.

#### <a name="how-tooconfigure"></a>Как tooconfigure:

**Настройка на компьютере шлюза**

1.  Запустите hello **Ksetup** tooconfigure программа hello сервером центра распространения КЛЮЧЕЙ Kerberos и область.

    машины Hello должен быть настроен как член рабочей группы, поскольку областью Kerberos отличается от домена Windows. Это достигается путем установки сферы Kerberos hello и добавления сервера KDC следующим образом. Вместо *REALM.COM* укажите соответствующее имя области.

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    **Перезапустите** машину hello после выполнения этих команд 2.

2.  Проверка конфигурации hello с **Ksetup** команды. выходные данные Hello должен иметь следующий вид:

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

**Настройка фабрики данных Azure**

* Настройка с помощью соединителя hello HDFS **проверки подлинности Windows** вместе с Kerberos основного имени и пароля tooconnect toohello HDFS источника данных. Проверьте сведения о конфигурации — [свойства связанной службы HDFS](#linked-service-properties).

### <a name="kerberos-mutual-trust"></a>Вариант 2. Активация взаимного доверия между доменом Windows и областью Kerberos

#### <a name="requirement"></a>Условие
*   компьютер шлюза Hello необходимо присоединить к домену Windows.
*   Требуется задать параметры разрешений tooupdate hello контроллера домена.

#### <a name="how-tooconfigure"></a>Как tooconfigure:

> [!NOTE]
> Замените REALM.COM и AD.COM в hello, следующий учебник с собственного соответствующей области и контроллер домена, при необходимости.

**Настройка на сервере центра распространения ключей**

1.  Изменение конфигурации KDC hello в **krb5.conf** toolet файл KDC доверия домена Windows, ссылающиеся toohello следующий шаблон конфигурации. По умолчанию hello конфигурации находится в **/etc/krb5.conf**.

            [logging]
             default = FILE:/var/log/krb5libs.log
             kdc = FILE:/var/log/krb5kdc.log
             admin_server = FILE:/var/log/kadmind.log

            [libdefaults]
             default_realm = REALM.COM
             dns_lookup_realm = false
             dns_lookup_kdc = false
             ticket_lifetime = 24h
             renew_lifetime = 7d
             forwardable = true

            [realms]
             REALM.COM = {
              kdc = node.REALM.COM
              admin_server = node.REALM.COM
             }
            AD.COM = {
             kdc = windc.ad.com
             admin_server = windc.ad.com
            }

            [domain_realm]
             .REALM.COM = REALM.COM
             REALM.COM = REALM.COM
             .ad.com = AD.COM
             ad.com = AD.COM

            [capaths]
             AD.COM = {
              REALM.COM = .
             }

  **Перезапустите** hello после настройки службы KDC.

2.  Подготовка участника с именем  **krbtgt/REALM.COM@AD.COM**  Server KDC с hello следующую команду:

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  В файле **hadoop.security.auth_to_local** добавьте к конфигурации HDFS правило `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.

**Настройка на контроллере домена**

1.  Запустите следующие hello **Ksetup** tooadd запись в области команд:

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  Установление доверия из домена Windows tooKerberos области. [пароль] — пароль hello участника hello  **krbtgt/REALM.COM@AD.COM** .

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  Выберите алгоритм шифрования, используемый в Kerberos.

    1. Go tooServer Manager > Управление групповой политикой > домена > объекты групповой политики > по умолчанию или активная политика домена и редактирования.

    2. В hello **редактор управления групповыми политиками** всплывающего окна, откройте tooComputer конфигурации > политики > Параметры Windows > Параметры безопасности > Локальные политики > Параметры безопасности и настройте **сети безопасность: Настройка разрешены для протокола Kerberos типов шифрования**.

    3. Алгоритм шифрования выберите hello требуется toouse при подключении tooKDC. Как правило можно выбрать все параметры hello.

        ![Типы шифрования конфигурации для Kerberos](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. Используйте **Ksetup** команда toospecify hello шифрования алгоритм toobe на hello СФЕРЫ.

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  Создайте участника в порядке toouse участника Kerberos в домене Windows hello сопоставление учетной записи домена hello и Kerberos.

    1. Запустите средства администрирования hello > **Active Directory — пользователи и компьютеры**.

    2. Настройте расширенные функции, щелкнув **Просмотр** > **Расширенные функции**.

    3. Найдите hello toowhich учетной записи необходимые toocreate сопоставления затем щелкните правой кнопкой мыши tooview **сопоставления имен** > щелкните **имена Kerberos** вкладки.

    4. Добавление участника из сферы hello.

        ![Сопоставление удостоверения безопасности](media/data-factory-hdfs-connector/map-security-identity.png)

**Настройка на компьютере шлюза**

* Запустите следующие hello **Ksetup** tooadd запись в области команд.

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

**Настройка фабрики данных Azure**

* Настройка с помощью соединителя hello HDFS **проверки подлинности Windows** вместе с вашей учетной записи домена или источник данных участника Kerberos tooconnect toohello HDFS. Проверьте сведения о конфигурации — [свойства связанной службы HDFS](#linked-service-properties).

> [!NOTE]
> toomap столбцы из источника toocolumns набора данных из набора данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).


## <a name="performance-and-tuning"></a>Производительность и настройка
В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.
