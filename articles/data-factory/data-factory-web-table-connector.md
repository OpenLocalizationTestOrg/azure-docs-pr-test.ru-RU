---
title: "aaaMove данные из веб-таблицы, с помощью фабрики данных Azure | Документы Microsoft"
description: "Дополнительные сведения о том, как toomove данные из таблицы на веб-страницу с использованием фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f54a26a4-baa4-4255-9791-5a8f935898e2
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e52216305583ebbe71ed896522f361bb22f01278
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a>Перемещение данных из источника веб-таблицы с помощью фабрики данных Azure
В этой статье рассматриваются как hello toouse действие копирования фабрики данных Azure toomove данных из таблицы в tooa веб-страницы поддерживается приемника хранилища данных. Эта статья основана на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, дан обзор перемещения данных на копии действия и hello список хранилищ данных, поддерживаемые в качестве источников и приемников.

Фабрика данных в настоящее время поддерживает только хранит перемещение данных из веб-tooother данных таблицы, но не перемещения данных из других данных хранит целевую таблицу tooa Web.

> [!IMPORTANT]
> Сейчас этот веб-соединитель поддерживает только извлечение содержимого таблицы из HTML-страницы. использовать tooretrieve данные из конечной точки HTTP/s [соединителя HTTP](data-factory-http-connector.md) вместо него.

## <a name="getting-started"></a>Приступая к работе
Вы можете создать конвейер с действием копирования, которое перемещает данные из локального хранилища данных Cassandra, с помощью разных инструментов и интерфейсов API. 

- toocreate простым способом Hello конвейера — toouse hello **мастер копирования**. В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера. 
- Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**. В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования. 

Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.

1. Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.
2. Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования. 
3. Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных. 

При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически. При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.  Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из веб-таблица, в разделе [пример JSON: копирование данных из таблицы Web tooAzure большого двоичного объекта](#json-example-copy-data-from-web-table-to-azure-blob) этой статьи. 

Привет, в следующих разделах содержат сведения о JSON свойства, которые являются таблицы используется toodefine фабрики данных сущностей определенного tooa Web:

## <a name="linked-service-properties"></a>Свойства связанной службы
Hello в следующей таблице приводится описание службы конкретных tooWeb связанные элементы JSON.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| type |свойство типа Hello должно быть присвоено: **Web** |Да |
| URL-адрес |URL-адрес toohello веб-источнику |Да |
| authenticationType |Анонимная. |Да |

### <a name="using-anonymous-authentication"></a>Использовать анонимную проверку подлинности

```json
{
    "name": "web",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

## <a name="dataset-properties"></a>Свойства набора данных
Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи. Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).

Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello. Hello typeProperties статьи для набора данных типа **таблицы WebTable** имеет следующие свойства hello

| Свойство | Описание | Обязательно |
|:--- |:--- |:--- |
| type |Тип набора данных hello. необходимо задать слишком**таблицы WebTable** |Да |
| path |Относительный URL-адрес ресурса toohello, содержащей таблицу hello. |Нет. Если путь не указан, используется только hello URL-адрес, указанный в определении службы hello связаны. |
| index |Индекс таблицы hello в ресурсе hello Hello. В разделе [Get индекс таблицы в HTML-страницу](#get-index-of-a-table-in-an-html-page) раздел для действия toogetting индекса таблицы в HTML-страницы. |Да |

**Пример**

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a>Свойства действия копирования
Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи. Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.

В то время как свойства в разделе typeProperties hello hello действия зависят от типа каждого действия. Для действия копирования они зависят от типов источников и приемников hello.

В настоящее время, если источник hello в действии копирования имеет тип **WebSource**, дополнительных свойств не поддерживаются.


## <a name="json-example-copy-data-from-web-table-tooazure-blob"></a>Пример JSON: копирование данных из таблицы Web tooAzure больших двоичных объектов
Hello следующем образце показано:

1. Связанная служба типа [Web](#linked-service-properties).
2. Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Входной [набор данных](data-factory-create-datasets.md) типа [WebTable](#dataset-properties).
4. Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. [Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [WebSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Образец Hello копирует данные из tooan таблицы Web BLOB-объектов Azure каждый час. свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.

Следующий образец Hello показано, как данные toocopy из tooan таблицы Web Azure BLOB-объектов. Тем не менее, данные можно скопировать непосредственно tooany из hello приемники уже говорилось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи с помощью hello действие копирования в фабрике данных Azure.

**Web связанная служба** в этом примере используется hello Web связанная служба с анонимной проверкой подлинности. Сведения об используемых типах аутентификации см. в разделе [Связанная веб-служба](#linked-service-properties).

```json
{
    "name": "WebLinkedService",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

**Связанная служба хранения Azure**

```json
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

**Входной набор данных таблицы WebTable** параметр **внешних** слишком**true** информирует hello служба фабрики данных, набор данных hello фабрики toohello внешних данных и не был создан из действия в hello фабрики данных.

> [!NOTE]
> В разделе [Get индекс таблицы в HTML-страницу](#get-index-of-a-table-in-an-html-page) раздел для действия toogetting индекса таблицы в HTML-страницы.  
>
>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
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

Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```



**Конвейер с действием копирования**

Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**WebSource** и **приемник** тип установлен слишком**BlobSink**.

В разделе [свойства типа WebSource](#copy-activity-type-properties) список свойств, поддерживаемых hello WebSource hello.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "WebTableToAzureBlob",
        "description": "Copy from a Web table tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "WebTableInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "WebSource"
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

## <a name="get-index-of-a-table-in-an-html-page"></a>Получение индекса таблицы на HTML-странице
1. Запустите **Excel 2016** и переключения toohello **данные** вкладки.  
2. Нажмите кнопку **новый запрос** на панели инструментов hello, точка слишком**из других источников** и нажмите кнопку **из Интернета**.

    ![Меню Power Query](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. В hello **из Интернета** диалогового окна введите **URL-адрес** , вы будете использовать в связанной службы JSON (например: https://en.wikipedia.org/wiki/) наряду с указанием пути, следует указать для hello набора данных (например: корпорация AFI % 27s_100_Years... 100_Movies) и нажмите кнопку **ОК**.

    ![Диалоговое окно "Из Интернета"](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    В этом примере используется URL-адрес https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies
4. Если вы видите **веб-доступа к содержимому** диалоговое окно, выберите hello справа **URL-адрес**, **проверки подлинности**и нажмите кнопку **Connect**.

   ![Диалоговое окно "Доступ к веб-содержимому"](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. Нажмите кнопку **таблицы** в содержимом toosee представление дерева hello из таблицы hello и выберите команду **изменить** кнопку в нижней части hello.  

   ![Диалоговое окно навигатора](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. В hello **редактора запросов** окно, нажмите кнопку **расширенный редактор** на инструментов «hello».

    ![Кнопка "Расширенный редактор"](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. В диалоговом окне Расширенный редактор hello, hello номер рядом слишком «Источник» является индекс hello.

    ![Расширенный редактор — индекс](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

Если вы используете Excel 2013, используйте [Microsoft Power Query для Excel](https://www.microsoft.com/download/details.aspx?id=39379) tooget hello индекса. В разделе [Connect tooa веб-страницы](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) Дополнительные сведения см. Hello шаги похожи, если вы используете [Microsoft Power BI для рабочего стола](https://powerbi.microsoft.com/desktop/).

> [!NOTE]
> toomap столбцы из источника toocolumns набора данных из набора данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Производительность и настройка
В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.
