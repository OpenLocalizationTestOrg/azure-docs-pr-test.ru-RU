---
title: "aaaSQL действия хранимой процедуры сервера"
description: "Дополнительные сведения об использовании tooinvoke действия хранимой процедуры SQL Server hello хранимой процедуры в базе данных SQL Azure или хранилище данных SQL Azure из конвейера фабрики данных."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1c46ed69-4049-44ec-9b46-e90e964a4a8e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: spelluru
ms.openlocfilehash: 9116f80eefc59d95e866b2ba1de2feb1bdc4b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-stored-procedure-activity"></a>Действие "Хранимая процедура SQL Server"
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Действие Hive](data-factory-hive-activity.md) 
> * [Действие Pig](data-factory-pig-activity.md)
> * [Действие MapReduce](data-factory-map-reduce.md)
> * [Потоковая активность Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Действие Spark](data-factory-spark.md)
> * [Действие выполнения пакета машинного обучения](data-factory-azure-ml-batch-execution-activity.md)
> * [Действие "Обновить ресурс" в службе машинного обучения](data-factory-azure-ml-update-resource-activity.md)
> * [Действие хранимой процедуры](data-factory-stored-proc-activity.md)
> * [Действие U-SQL в Data Lake Analytics](data-factory-usql-activity.md)
> * [Настраиваемое действие .NET](data-factory-use-custom-activities.md)

## <a name="overview"></a>Обзор
Используйте действия преобразования данных в фабрике данных [конвейера](data-factory-create-pipelines.md) tootransform и процесс необработанные данные в прогнозы и аналитики. Hello действия хранимой процедуры — одно из действий hello преобразования, которые поддерживает фабрики данных. Эта статья основана на hello [действия преобразования данных](data-factory-data-transformation-activities.md) статьи, в котором предоставляются общие сведения о преобразования данных и hello поддерживается преобразование действия в фабрике данных.

Можно использовать tooinvoke действия хранимой процедуры hello хранимой процедуры в одном hello следующие данные хранятся в вашей организации или на виртуальной машине Azure (ВМ): 

- База данных SQL Azure
- Хранилище данных SQL Azure
- База данных SQL Server.  Если вы используете SQL Server, установите шлюз управления данными на приветствия же компьютер, что узлы hello базы данных или на отдельном компьютере, который имеет доступ к базе данных toohello. Шлюз управления данными — это компонент, который обеспечивает безопасное и управляемое подключение локальных источников данных или данных виртуальной машины Azure к облачным службам. Дополнительные сведения см. в статье [Шлюз управления данными](data-factory-data-management-gateway.md).

> [!IMPORTANT]
> При копировании данных в базе данных SQL Azure или SQL Server, можно настроить hello **SqlSink** в tooinvoke действия копирования хранимой процедуры с помощью hello **sqlWriterStoredProcedureName** свойство. Дополнительные сведения см. в статье [Вызов хранимой процедуры из действия копирования в фабрике данных Azure](data-factory-invoke-stored-procedure-from-copy-activity.md). Дополнительные сведения о свойстве hello см. следующие статьи соединителя: [базы данных SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties). Вызов хранимой процедуры во время копирования данных в хранилище данных SQL Azure с помощью операции копирования не поддерживается. Однако можно использовать tooinvoke действие hello хранимой процедуры хранимой процедуры в хранилище данных SQL. 
>  
> При копировании данных из базы данных SQL Azure или SQL Server или хранилище данных SQL Azure, можно настроить **SqlSource** в tooinvoke действия копирования данных tooread хранимой процедуры из базы данных-источника hello с помощью hello  **sqlReaderStoredProcedureName** свойство. Дополнительные сведения см. следующие статьи соединителя hello: [базы данных SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [хранилище данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)          


Пошаговое руководство использует следующие Hello hello действия хранимой процедуры в конвейер tooinvoke хранимую процедуру в базе данных Azure SQL. 

## <a name="walkthrough"></a>Пошаговое руководство
### <a name="sample-table-and-stored-procedure"></a>Образец таблицы и хранимая процедура
1. Создайте ниже hello **таблицы** в базе данных SQL Azure с помощью SQL Server Management Studio или любой другой инструмент, вы знакомы с. столбец datetimestamp Hello является hello даты и времени, когда создается соответствующий идентификатор hello.

    ```SQL
    CREATE TABLE dbo.sampletable
    (
        Id uniqueidentifier,
        datetimestamp nvarchar(127)
    )
    GO

    CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable(Id);
    GO
    ```
    Идентификатор hello уникальный идентифицировать а hello datetimestamp очередь hello даты и времени, когда создается соответствующий идентификатор hello.
    
    ![Пример данных](./media/data-factory-stored-proc-activity/sample-data.png)

    В этом образце hello хранимой процедуры находится в базе данных SQL Azure. Если hello хранимая процедура находится в хранилище данных SQL Azure и базы данных SQL Server, hello подход аналогичен. В случае с базой данных SQL Server необходимо установить [шлюз управления данными](data-factory-data-management-gateway.md).
2. Создайте ниже hello **хранимой процедуры** , вставляет данные в toohello **образец таблицы**.

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > **Имя** и **регистр** hello параметра (Дата и время в этом примере) должно совпадать, параметр, указанный в JSON конвейера hello и действия. В hello определение хранимой процедуры, убедитесь, что  **@**  используется в качестве префикса для параметра hello.

### <a name="create-a-data-factory"></a>Создать фабрику данных
1. Войдите в слишком[портал Azure](https://portal.azure.com/).
2. Нажмите кнопку **NEW** hello левого меню **аналитики + аналитика**и нажмите кнопку **фабрики данных**.

    ![Новая фабрика данных](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. В hello **новую фабрику данных** колонке введите **SProcDF** для hello имя. Имена фабрики данных Azure являются **глобально уникальными**. Требуется имя hello tooprefix hello фабрики данных с вашим именем tooenable hello успешного создания фабрики hello.

   ![Новая фабрика данных](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. Выберите свою **подписку Azure**.
5. Для **группы ресурсов**, выполните одно из hello следующие шаги:
   1. Нажмите кнопку **создать новый** и введите имя для группы ресурсов hello.
   2. Щелкните **Использовать существующий** и укажите имеющуюся группу ресурсов.  
6. Выберите hello **расположение** для фабрики данных hello.
7. Выберите **toodashboard ПИН-код** , чтобы увидеть hello фабрики данных на панели мониторинга hello следующем входе в систему.
8. Нажмите кнопку **создать** на hello **новую фабрику данных** колонку.
9. Вы видите hello фабрики данных, создаваемого в hello **мониторинга** из hello портал Azure. После успешного создания фабрики данных hello, отображается страница фабрики данных hello, в котором отображается содержимое фабрики данных hello hello.

   ![Домашняя страница фабрики данных](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a>Создание связанной службы SQL Azure
После создания фабрики данных hello, создайте связанной службой SQL Azure, связывающий базы данных Azure SQL, содержащий таблицу hello образец таблицы и sp_sample хранимые процедуры, tooyour фабрики данных.

1. Нажмите кнопку **автор и развернуть** на hello **фабрики данных** колонке **SProcDF** toolaunch hello редактор фабрики данных.
2. Нажмите кнопку **новое хранилище данных** hello панели команд и выберите **базы данных SQL Azure**. Вы увидите hello скрипта JSON для создания Azure SQL связанные службы в редакторе hello.

   ![Новое хранилище данных](media/data-factory-stored-proc-activity/new-data-store.png)
3. Убедитесь в hello скрипта JSON, hello следующие отличия.

   1. Замените `<servername>` с именем hello сервера базы данных SQL Azure.
   2. Замените `<databasename>` с hello базы данных, в которой создана таблица hello и hello хранимой процедуры.
   3. Замените `<username@servername>` с hello учетной записи пользователя, который имеет доступ к базе данных toohello.
   4. Замените `<password>` hello пароль для учетной записи пользователя hello.

      ![Новое хранилище данных](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. toodeploy Здравствуйте связанной службы, нажмите кнопку **развернуть** на панели команд hello. Подтвердите, что вы видите hello AzureSqlLinkedService hello дерева просмотра слева hello.

    ![иерархическое представление со связанными службами](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a>Создание выходного набора данных
Необходимо указать выходной набор данных для действия "хранимая процедура" даже если hello хранимой процедуры не создаются все данные. Это, так как его hello выходной набор данных, который управляет расписанием hello hello действия (частоту hello действие выполняется - ежечасно, ежедневно, и т. д.). Hello выходной набор данных необходимо использовать **связанная служба** , обозначающий tooan базы данных SQL Azure или хранилище данных SQL Azure или базе SQL Server, в котором нужно hello toorun хранимой процедуры. Hello выходной набор данных может служить результат hello toopass способом hello хранимые процедуры для последующей обработки другим действием ([цепочки действий](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) hello конвейера. Однако фабрики данных вывода автоматически hello объекта dataset toothis хранимой процедуры. Это hello хранимая процедура записи таблицы tooa SQL, который hello указывает выходного набора данных. В некоторых случаях может быть выходной набор данных hello **пустой набор данных** (набор данных, указывающий tooa таблицу, которая не удерживает действительно hello выходные данные хранимой процедуры). Этот пустой набор данных используется только для hello расписание hello toospecify действие хранимой процедуры. 

1. Нажмите **... Дополнительные** на hello инструментов щелкните **новый набор данных**и нажмите кнопку **Azure SQL**. **Новый набор данных** панели и выберите команду hello **Azure SQL**.

    ![иерархическое представление со связанными службами](media/data-factory-stored-proc-activity/new-dataset.png)
2. Скопируйте и вставьте следующий скрипт JSON в редакторе JSON toohello hello.

    ```JSON
    {                
        "name": "sprocsampleout",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "sampletable"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```
3. toodeploy Здравствуйте набора данных, нажмите кнопку **развернуть** на панели команд hello. Подтвердите, что вы видите hello набора данных в древовидном представлении hello.

    ![иерархическое представление со связанными службами](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a>Создание конвейера с помощью действия SqlServerStoredProcedure
Теперь создадим конвейер с помощью действия хранимой процедуры. 

Обратите внимание, hello следующие свойства: 

- Hello **тип** задано слишком**SqlServerStoredProcedure**. 
- Hello **storedProcedureName** в тип свойства заданы слишком**sp_sample** (имя hello хранимой процедуры).
- Hello **storedProcedureParameters** раздел содержит один параметр с именем **DataTime**. Имя и регистра параметра hello в JSON должны совпадать с именем hello и регистр hello параметра в определении hello хранимой процедуры. Если требуется передать значение null для параметра, используйте синтаксис hello: `"param1": null` (прописными буквами).
 
1. Нажмите **... Дополнительные** hello панели команд и нажмите кнопку **новый конвейер**.
2. Скопируйте и вставьте следующий фрагмент JSON hello:   

    ```JSON
    {
        "name": "SprocActivitySamplePipeline",
        "properties": {
            "activities": [
                {
                    "type": "SqlServerStoredProcedure",
                    "typeProperties": {
                        "storedProcedureName": "sp_sample",
                        "storedProcedureParameters": {
                            "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                        }
                    },
                    "outputs": [
                        {
                            "name": "sprocsampleout"
                        }
                    ],
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "SprocActivitySample"
                }
            ],
             "start": "2017-04-02T00:00:00Z",
             "end": "2017-04-02T05:00:00Z",
            "isPaused": false
        }
    }
    ```
3. toodeploy hello конвейера, нажмите кнопку **развернуть** на панели инструментов hello.  

### <a name="monitor-hello-pipeline"></a>Монитор hello конвейера
1. Нажмите кнопку **X** tooclose редактор фабрики данных колонках toonavigate резервное колонке toohello фабрики данных и нажмите кнопку **схема**.

    ![плитка "Схема"](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. В hello **представление диаграммы**, просмотреть обзор конвейеров hello и использовать наборы данных в этом учебнике.

    ![плитка "Схема"](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. В hello представление диаграммы, дважды щелкните набор данных hello `sprocsampleout`. Вы увидите hello срезов в состоянии готовности. Поскольку срезов каждый час между hello время начала и время окончания из hello JSON должно быть пять срезов.

    ![плитка "Схема"](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. Если срез находится в **готовности** состояние, запустите `select * from sampletable` запрос к tooverify базы данных Azure SQL hello, hello данных была вставлена в таблицу toohello hello хранимой процедурой.

   ![Выходные данные](./media/data-factory-stored-proc-activity/output.png)

   В разделе [конвейера hello монитор](data-factory-monitor-manage-pipelines.md) подробные сведения о мониторинге конвейеров фабрики данных Azure.  


## <a name="specify-an-input-dataset"></a>Указание набора входных данных
В пошаговом руководстве hello действия хранимой процедуры нет любой входных наборов данных. При указании входного набора данных, hello действие хранимой процедуры не запускается до hello фрагмент из набора входных данных доступен (в состоянии готовности). Hello набором данных может быть внешнего набора данных (не был создан другим действием hello же конвейера) или внутренний набор данных, данным, созданным вышестоящего действие (действие hello, который выполняется перед этим действием). Можно указать несколько входных наборов данных для действия hello хранимой процедуры. Если сделать это, hello действие хранимой процедуры выполняется только в том случае, если доступны все срезы hello входного набора данных (в состоянии готовности). Hello входного набора данных не может использоваться в hello хранимой процедуре как параметр. Это только используемые toocheck hello зависимостей, до начала hello действие хранимой процедуры.

## <a name="chaining-with-other-activities"></a>Объединение с другими действиями
Toochain восходящего действия с этим действием, укажите выходные данные hello восходящего действия hello, входным этого действия. При этом hello действие хранимой процедуры не выполняется до завершения действия вышестоящего hello и hello выходного набора данных hello восходящего действия доступен (в состоянии готовности). Выходные наборы данных из нескольких действий вышестоящего можно указать в качестве входных наборов данных действия hello хранимой процедуры. После этого hello действие хранимой процедуры выполняется только в том случае, когда доступны все срезы hello входного набора данных.  

В следующем примере hello, является hello выходным результатом действия копирования hello: OutputDataset, который является входным hello действие хранимой процедуры. Таким образом hello действие хранимой процедуры не выполняется до завершения действия копирования hello и hello OutputDataset фрагмент доступен (в состоянии готовности). При указании нескольких входных наборов данных hello действие хранимой процедуры не запускается до доступны все срезы hello входного набора данных (в состоянии готовности). Hello входных наборов данных не может использоваться непосредственно в виде параметров toohello хранимой процедуры действия. 

Дополнительные сведения о цепочках действий см. в разделе [Несколько действий в конвейере](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline).

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob tooblob",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [ { "name": "InputDataset" } ],
                "outputs": [ { "name": "OutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst"
                },
                "name": "CopyFromBlobToSQL"
            },
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "SPSproc"
                },
                "inputs": [ { "name": "OutputDataset" } ],
                "outputs": [ { "name": "SQLOutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunStoredProcedure"
            }

        ],
        "start": "2017-04-12T00:00:00Z",
        "end": "2017-04-13T00:00:00Z",
        "isPaused": false,
    }
}
```

Аналогичным образом toolink hello магазина действия процедуры с **нисходящие действия** (hello действия, выполняющие после hello хранимая процедура завершения действия), укажите hello выходного набора данных действие hello хранимой процедуры как входные данные hello нисходящие действия в конвейере hello.

> [!IMPORTANT]
> При копировании данных в базе данных SQL Azure или SQL Server, можно настроить hello **SqlSink** в tooinvoke действия копирования хранимой процедуры с помощью hello **sqlWriterStoredProcedureName** свойство. Дополнительные сведения см. в статье [Вызов хранимой процедуры из действия копирования в фабрике данных Azure](data-factory-invoke-stored-procedure-from-copy-activity.md). Дополнительные сведения о свойстве hello см. следующие статьи соединителя hello: [базы данных SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).
>  
> При копировании данных из базы данных SQL Azure или SQL Server или хранилище данных SQL Azure, можно настроить **SqlSource** в tooinvoke действия копирования данных tooread хранимой процедуры из базы данных-источника hello с помощью hello  **sqlReaderStoredProcedureName** свойство. Дополнительные сведения см. следующие статьи соединителя hello: [базы данных SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [хранилище данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)          

## <a name="json-format"></a>Формат JSON
Вот hello формат JSON для определения действия хранимой процедуры.

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of hello stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

Привет, в следующей таблице описываются эти свойства JSON:

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| name | Имя действия hello |Да |
| Описание |Текст, описывающий, какое действие hello используется для |Нет |
| type | Нужно задать значение **SqlServerStoredProcedure** | Да |
| inputs | необязательный параметр. При указании входного набора данных, он должен быть доступен (в состояние «Готово») для hello хранимой процедуры toorun действия. Hello входного набора данных не может использоваться в hello хранимой процедуре как параметр. Это только используемые toocheck hello зависимостей, до начала hello действие хранимой процедуры. |Нет |
| outputs | Для действия хранимой процедуры необходимо указать выходной набор данных. Выходной набор данных указывает hello **расписание** для hello действие хранимой процедуры (каждый час, еженедельно, ежемесячно, и т. д.). <br/><br/>Hello выходной набор данных необходимо использовать **связанная служба** , обозначающий tooan базы данных SQL Azure или хранилище данных SQL Azure или базе SQL Server, в котором нужно hello toorun хранимой процедуры. <br/><br/>Hello выходной набор данных может служить результат hello toopass способом hello хранимые процедуры для последующей обработки другим действием ([цепочки действий](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) hello конвейера. Однако фабрики данных вывода автоматически hello объекта dataset toothis хранимой процедуры. Это hello хранимая процедура записи таблицы tooa SQL, который hello указывает выходного набора данных. <br/><br/>В некоторых случаях может быть выходной набор данных hello **пустой набор данных**, который используется только для hello расписание hello toospecify действие хранимой процедуры. |Да |
| storedProcedureName |Укажите имя hello hello хранимой процедуры в базе данных Azure SQL hello или хранилище данных SQL Azure или SQL Server базы данных, представленного hello связаны службы, которая hello использования выходной таблицы. |Да |
| storedProcedureParameters |Указываемые значения для параметров хранимой процедуры. Если вам требуется toopass значение null для параметра, используйте синтаксис hello: «param1»: null (все строчные). См. следующий пример toolearn об использовании этого свойства hello. |Нет |

## <a name="passing-a-static-value"></a>Передача статического значения
Теперь давайте рассмотрим добавление другой столбец с именем «Сценарий» в таблице hello, содержащий статический значение с именем «Документа-пример».

![Пример данных 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

**Таблица:**

```SQL
CREATE TABLE dbo.sampletable2
(
    Id uniqueidentifier,
    datetimestamp nvarchar(127),
    scenario nvarchar(127)
)
GO

CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable2(Id);
```

**Хранимая процедура:**

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

Теперь, передавать hello **сценарий** значение параметра и hello из hello действие хранимой процедуры. Hello **typeProperties** раздела hello предшествующий выглядит пример hello, следующий фрагмент кода:

```JSON
"typeProperties":
{
    "storedProcedureName": "sp_sample",
    "storedProcedureParameters":
    {
        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
        "Scenario": "Document sample"
    }
}
```

**Набор данных фабрики данных:**

```JSON
{
    "name": "sprocsampleout2",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable2"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Конвейер фабрики данных**

```JSON
{
    "name": "SprocActivitySamplePipeline2",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample2",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
                        "Scenario": "Document sample"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout2"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2016-10-02T00:00:00Z",
        "end": "2016-10-02T05:00:00Z"
    }
}
```