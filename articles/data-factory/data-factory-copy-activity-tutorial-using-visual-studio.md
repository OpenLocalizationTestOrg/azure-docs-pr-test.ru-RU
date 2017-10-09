---
title: "Руководство. Создание конвейера с действием копирования с помощью Visual Studio | Документация Майкрософт"
description: "С помощью этого руководства вы, используя Visual Studio, создадите конвейер фабрики данных Azure с действием копирования."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1751185b-ce0a-4ab2-a9c3-e37b4d149ca3
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: d99d8875807bab41f5122ab95a09f83f82923529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a>Руководство. Создание конвейера с действием копирования с помощью Visual Studio
> [!div class="op_single_selector"]
> * [Обзор и предварительные требования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Мастер копирования](data-factory-copy-data-wizard-tutorial.md)
> * [Портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Шаблон Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [ИНТЕРФЕЙС REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

В этой статье вы узнаете, как toouse hello toocreate Microsoft Visual Studio фабрики данных с конвейером, который копирует данные из базы данных Azure SQL tooan хранилища BLOB-объектов Azure. Если новый tooAzure фабрики данных, прочтите hello [tooAzure введение фабрики данных](data-factory-introduction.md) статьи, прежде чем выполнять задания этого учебника.   

В этом руководстве описывается создание конвейера с одним действием — действием копирования. Действие копирования Hello копирует данные из поддерживаемых хранилища tooa поддерживаемых приемник данных хранилищ данных. Список хранилищ данных, которые поддерживаются в качестве источников и приемников, см. в разделе [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Действие Hello выключен глобально доступной можно копировать данные между различными хранилищами данных в виде безопасные, надежные и масштабируемые службы. Дополнительные сведения о действии копирования hello см. в разделе [действия перемещения данных](data-factory-data-movement-activities.md).

Конвейер может содержать сразу несколько действий. Кроме того, можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия. Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

> [!NOTE] 
> конвейер данных Hello в этом учебнике копирует данные из источника данных хранилища tooa целевое хранилище данных. Учебник о том, как tootransform данных, с помощью фабрики данных Azure, в разделе [учебника: построение конвейера анализа tootransform использование кластера Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Предварительные требования
1. Прочтите [Обзор учебника](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) статьи и завершения hello **необходимого компонента** действия.       
2. экземпляры toocreate фабрики данных, необходимо быть членом hello [участника фабрики данных](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) роли на уровне группы hello подписки или ресурса.
3. Необходимо иметь следующие hello, установленной на компьютере. 
   * Visual Studio 2013 или Visual Studio 2015.
   * Загрузите пакет SDK Azure для Visual Studio 2013 или Visual Studio 2015. Перейдите в слишком[странице загрузки Azure](https://azure.microsoft.com/downloads/) и нажмите кнопку **VS 2013** или **VS 2015** в hello **.NET** раздела.
   * Загрузите hello последнюю фабрики данных Azure, подключаемый модуль для Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) или [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). Можно также обновить hello подключаемого модуля, выполнив следующие шаги hello: hello меню **средства** -> **расширения и обновления** -> **Online**  ->  **Коллекции visual Studio** -> **средства фабрики данных Microsoft Azure для Visual Studio** -> **обновление**.

## <a name="steps"></a>Действия
Ниже приведены hello действий, выполняемых в рамках этого учебника.

1. Создание **связанные службы** в фабрике данных hello. На этом этапе вы создадите две связанные службы — службу хранилища Azure и базу данных SQL Azure. 
    
    Hello AzureStorageLinkedService связывает фабрику данных toohello учетной записи хранилища Azure. Создан контейнер и загруженные в рамках учетной записи хранения данных toothis [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    AzureSqlLinkedService связывает фабрику данных toohello базы данных Azure SQL. Hello данные, копируемые из хранилища больших двоичных объектов hello хранится в этой базе данных. Вы создали таблицу SQL в этой базе данных в ходе выполнения [предварительных требований](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).     
2. Создать входной и выходной **наборы данных** в фабрике данных hello.  
    
    Hello связанной службой хранилища Azure задает строку подключения hello, который использует служба фабрики данных во время выполнения tooconnect tooyour учетной записи хранилища Azure. И входного BLOB-объекта dataset hello указывает контейнер hello и hello папку, содержащую hello входных данных.  

    Аналогичным образом hello связана база данных SQL Azure службы указывает hello строку подключения, использующее служба фабрики данных в базе данных Azure SQL tooyour tooconnect время выполнения. И SQL таблицы hello выходной набор данных указывает, что таблица hello в данных hello toowhich hello базы данных из хранилища больших двоичных объектов hello копируется.
3. Создание **конвейера** в фабрике данных hello. На этом этапе вы создадите конвейер с действием копирования.   
    
    Действие копирования Hello копирует данные из большого двоичного объекта в таблице tooa хранилища BLOB-объектов Azure hello в базе данных Azure SQL hello. Действие копирования можно использовать в конвейер toocopy данных из любого места назначения tooany поддерживается поддерживаемой исходной. Список поддерживаемых хранилищ данных см. в [этом разделе](data-factory-data-movement-activities.md#supported-data-stores-and-formats). 
4. Создайте **фабрику данных** Azure при развертывании сущностей фабрики данных (связанные службы, наборы данных, таблицы и конвейеры). 

## <a name="create-visual-studio-project"></a>Создание проекта Visual Studio
1. Запустите **Visual Studio 2015**. Нажмите кнопку **файл**, слишком точки**New**и нажмите кнопку **проекта**. Вы увидите hello **новый проект** диалоговое окно.  
2. В hello **новый проект** диалоговое окно, выберите hello **DataFactory** шаблона и нажмите кнопку **пустой проект фабрики данных**.  
   
    ![Диалоговое окно "Новый проект"](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. Укажите имя проекта hello, местоположение для решения hello hello и имя решения hello и нажмите кнопку **ОК**.
   
    ![Обозреватель решений](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a>Создание связанных служб
Создания связанных служб в toolink фабрики данных, хранит и вычислений фабрики данных toohello службы данных. В этом руководстве не используются службы вычислений, например Azure HDInsight или Azure Data Lake Analytics. Вы используете два хранилища данных — служба хранилища Azure (источник) и база данных SQL Azure (конечное хранилище). 

Вы создадите две связанные службы — AzureStorage и AzureSqlDatabase.  

Hello хранилища Azure связанные ссылки на службу фабрики данных toohello учетной записи хранилища Azure. Эта учетная запись хранения является hello один в котором можно создать контейнер и загруженные данные hello в рамках [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

Azure SQL связанные ссылки на службу фабрики данных toohello базы данных Azure SQL. Hello данные, копируемые из хранилища больших двоичных объектов hello хранится в этой базе данных. Создана таблица emp hello в этой базе данных как часть [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Связанные службы связывание хранилищ данных или фабрики данных Azure tooan службы вычислений. В разделе [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) для всех hello источники и приемники, поддерживаемые действием копирования hello. В разделе [связанные службы вычислений](data-factory-compute-linked-services.md) список hello вычислительных служб, поддерживаемые фабрикой данных. В этом руководстве не рассматривается использование служб вычислений. 

### <a name="create-hello-azure-storage-linked-service"></a>Создание hello связанной службой хранилища Azure
1. В **обозревателе решений**, щелкните правой кнопкой мыши **связанные службы**, слишком точки**добавить**и нажмите кнопку **новый элемент**.      
2. В hello **Добавление нового элемента** выберите **связанной службы хранилища Azure** hello списка и нажмите кнопку **добавить**. 
   
    ![Новая связанная служба](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. Замените `<accountname>` и `<accountkey>`* hello имя вашей учетной записи хранилища Azure и ее ключа. 
   
    ![Связанная служба хранилища Azure](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. Сохранить hello **AzureStorageLinkedService1.json** файла.

    Дополнительные сведения о свойствах JSON в определении службы hello связаны см. в разделе [соединителя хранилища больших двоичных объектов](data-factory-azure-blob-connector.md#linked-service-properties) статьи.

### <a name="create-hello-azure-sql-linked-service"></a>Создание hello связанной службой Azure SQL
1. Щелкните правой кнопкой мыши **связанные службы** узел в hello **обозревателе решений** снова точки слишком**добавить**и нажмите кнопку **новый элемент**. 
2. На этот раз выберите **Azure SQL Linked Service** (Связанная служба SQL Azure) и нажмите кнопку **Добавить**. 
3. В hello **файл AzureSqlLinkedService1.json**, замените `<servername>`, `<databasename>`, `<username@servername>`, и `<password>` с именами Azure SQL server, базы данных, учетная запись пользователя, и пароль.    
4. Сохранить hello **AzureSqlLinkedService1.json** файла. 
    
    Дополнительные сведения об этих свойствах JSON см. в статье о [соединителе базы данных SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties).


## <a name="create-datasets"></a>Создание наборов данных
В предыдущем шаге hello создать связанные службы toolink вашей учетной записи хранилища Azure и фабрику данных tooyour базы данных Azure SQL. На этом шаге можно определить два набора данных с именем InputDataset и OutputDataset, представляющие входные данные и выходные данные, которые хранятся в хранилищах данных hello, на которые ссылается AzureStorageLinkedService1 и AzureSqlLinkedService1 соответственно.

Hello связанной службой хранилища Azure задает строку подключения hello, который использует служба фабрики данных во время выполнения tooconnect tooyour учетной записи хранилища Azure. И hello входного BLOB-объекта dataset (InputDataset) указывает контейнер hello и hello папку, содержащую hello входных данных.  

Аналогичным образом hello связана база данных SQL Azure службы указывает hello строку подключения, использующее служба фабрики данных в базе данных Azure SQL tooyour tooconnect время выполнения. И hello выходной набор данных таблицы SQL (OututDataset) указывает таблицу hello в hello базы данных toowhich hello и копирования данных из хранилища больших двоичных объектов hello. 

### <a name="create-input-dataset"></a>Создание входного набора данных
На этом шаге создается набор данных с именем InputDataset, который указывает файл tooa больших двоичных объектов (emp.txt) в корневой папке hello контейнер больших двоичных объектов (adftutorial) в hello представленный hello AzureStorageLinkedService1 связанной службы хранилища Azure. Если не указать значение для имени файла hello (или пропустить его), данные из всех больших двоичных объектов в папке входной hello, скопированный toohello назначения. В этом учебнике укажите значение для имени файла hello. 

Здесь используется hello термин «таблицы» вместо «наборы данных». Таблица представляет собой прямоугольный набор данных и представляет единственный тип hello набора данных, поддерживаемые в данный момент. 

1. Щелкните правой кнопкой мыши **таблиц** в hello **обозревателе решений**, слишком точки**добавить**и нажмите кнопку **новый элемент**.
2. В hello **Добавление нового элемента** выберите **больших двоичных объектов Azure**и нажмите кнопку **добавить**.   
3. Заменить текст JSON hello после текста hello и сохранить hello **AzureBlobLocation1.json** файла. 

  ```json   
  {
    "name": "InputDataset",
    "properties": {
      "structure": [
        {
          "name": "FirstName",
          "type": "String"
        },
        {
          "name": "LastName",
          "type": "String"
        }
      ],
      "type": "AzureBlob",
      "linkedServiceName": "AzureStorageLinkedService1",
      "typeProperties": {
        "folderPath": "adftutorial/",
        "format": {
          "type": "TextFormat",
          "columnDelimiter": ","
        }
      },
      "external": true,
      "availability": {
        "frequency": "Hour",
        "interval": 1
      }
    }
  }
  ``` 
    Hello следующей таблице содержатся описания свойств JSON hello, используемых в фрагмент кода hello.

    | Свойство | Описание |
    |:--- |:--- |
    | type | Hello свойство type установлено слишком**AzureBlob** , так как данные находятся в хранилище больших двоичных объектов. |
    | linkedServiceName (имя связанной службы) | Указывает toohello **AzureStorageLinkedService** , созданного ранее. |
    | folderPath | Указывает hello blob **контейнера** и hello **папки** , содержащий входного BLOB-объектов. В этом учебнике adftutorial — контейнер больших двоичных объектов hello и папка является корневой папкой hello. | 
    | fileName | Это необязательное свойство. Если это свойство не указан, извлекаются все файлы из hello folderPath. В этом учебнике **emp.txt** задается для hello имя файла, поэтому только этот файл будет выбрано для обработки. |
    | format -> type |Hello входной файл имеет текстовый формат hello, поэтому мы используем **TextFormat**. |
    | columnDelimiter | Hello столбцов во входном файле hello разделяются **запятая (`,`)**. |
    | frequency и interval | частота Hello задано слишком**час** и интервала задано слишком**1**, это означает, что hello ввода доступны срезы **каждый час**. Другими словами, hello служба фабрики данных ищет входных данных каждый час в корневой папке hello контейнер больших двоичных объектов (**adftutorial**) было задано. Выполняет поиск данных hello в hello конвейера начального и конечного времени, не до или после этих значений времени.  |
    | external | Это свойство задано слишком**true** Если hello данных в этом конвейере не создается. в файле emp.txt hello, который создается в этом конвейере не, поэтому мы задали это свойство tootrue — Hello входных данных в этом учебнике. |

    Дополнительные сведения об этих свойствах JSON см. в [этом разделе](data-factory-azure-blob-connector.md#dataset-properties).   

### <a name="create-output-dataset"></a>Создание выходного набора данных
На этом этапе мы создадим выходной набор данных с именем **OutputDataset**. Этот набор данных указывает tooa SQL таблицы в базе данных Azure SQL hello, представленного **AzureSqlLinkedService1**. 

1. Щелкните правой кнопкой мыши **таблиц** в hello **обозревателе решений** снова точки слишком**добавить**и нажмите кнопку **новый элемент**.
2. В hello **Добавление нового элемента** выберите **Azure SQL**и нажмите кнопку **добавить**. 
3. Заменить текст JSON hello hello, следуя JSON и сохранить hello **AzureSqlTableLocation1.json** файла.

  ```json
    {
     "name": "OutputDataset",
     "properties": {
       "structure": [
         {
           "name": "FirstName",
           "type": "String"
         },
         {
           "name": "LastName",
           "type": "String"
         }
       ],
       "type": "AzureSqlTable",
       "linkedServiceName": "AzureSqlLinkedService1",
       "typeProperties": {
         "tableName": "emp"
       },
       "availability": {
         "frequency": "Hour",
         "interval": 1
       }
     }
    }
    ```
    Hello следующей таблице содержатся описания свойств JSON hello, используемых в фрагмент кода hello.

    | Свойство | Описание |
    |:--- |:--- |
    | type | Hello свойство type установлено слишком**AzureSqlTable** из-за данных скопированный tooa таблицы в базе данных Azure SQL. |
    | linkedServiceName (имя связанной службы) | Указывает toohello **AzureSqlLinkedService** , созданного ранее. |
    | tableName | Указанный hello **таблицы** toowhich hello данные копируются. | 
    | frequency и interval | Hello задана слишком**час** и интервал — **1**, это означает, что hello срезы выходных данных создаются **каждый час** между hello конвейера начала и время окончания, не до или После этих значений времени.  |

    Имеются три столбца — **идентификатор**, **FirstName**, и **LastName** — в таблице emp hello в базе данных hello. Идентификатор является столбцом идентификаторов, поэтому вам необходимо только toospecify **FirstName** и **LastName** здесь.

    Дополнительные сведения об этих свойствах JSON см. в [этом разделе](data-factory-azure-sql-connector.md#dataset-properties).

## <a name="create-pipeline"></a>Создание конвейера
На этом этапе вы создадите конвейер с **действием копирования**, которое использует **InputDataset** в качестве входных данных и **OutputDataset** в качестве выходных.

В настоящее время выходной набор данных — того, какие диски hello расписания. В этом учебнике выходной набор данных является настроенным tooproduce срез один раз в час. конвейер Hello содержит время начала и время окончания, которые однажды друг от друга, что составляет 24 часа. Таким образом 24 фрагменты выходной набор данных создают hello конвейера. 

1. Щелкните правой кнопкой мыши **конвейеры** в hello **обозревателе решений**, слишком точки**добавить**и нажмите кнопку **новый элемент**.  
2. Выберите **конвейера данных копирования** в hello **Добавление нового элемента** диалоговое окно и нажмите кнопку **добавить**. 
3. Замените следующие JSON hello hello JSON и сохраните hello **CopyActivity1.json** файла.

  ```json   
    {
     "name": "ADFTutorialPipeline",
     "properties": {
       "description": "Copy data from a blob tooAzure SQL table",
       "activities": [
         {
           "name": "CopyFromBlobToSQL",
           "type": "Copy",
           "inputs": [
             {
               "name": "InputDataset"
             }
           ],
           "outputs": [
             {
               "name": "OutputDataset"
             }
           ],
           "typeProperties": {
             "source": {
               "type": "BlobSource"
             },
             "sink": {
               "type": "SqlSink",
               "writeBatchSize": 10000,
               "writeBatchTimeout": "60:00:00"
             }
           },
           "Policy": {
             "concurrency": 1,
             "executionPriorityOrder": "NewestFirst",
             "style": "StartOfInterval",
             "retry": 0,
             "timeout": "01:00:00"
           }
         }
       ],
       "start": "2017-05-11T00:00:00Z",
       "end": "2017-05-12T00:00:00Z",
       "isPaused": false
     }
    }
    ```   
    - В разделе "действия" hello, имеется только одно действие, **тип** задано слишком**копирования**. Дополнительные сведения о действии копирования hello см. в разделе [действия перемещения данных](data-factory-data-movement-activities.md). В решениях фабрики данных можно также использовать [действия преобразования данных](data-factory-data-transformation-activities.md).
    - Входных данных для действия hello установлено слишком**InputDataset** и вывода для hello действия установлено слишком**OutputDataset**. 
    - В hello **typeProperties** разделе **BlobSource** указан в качестве типа источника hello и **SqlSink** указан как тип приемника hello. Перечень хранилищ данных, поддерживаемые действием копирования hello как источники и приемники см. в разделе [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats). как сохранить toouse конкретных поддерживаемые данные в качестве источника и приемника, toolearn по ссылке hello в таблице hello.  
     
    Замените значение hello hello **запустить** свойство с hello текущего дня и **окончания** значение с hello следующего дня. Можно указать только часть даты hello и пропустить hello время hello Дата и время. Например, «2016-02-03», который является эквивалентом "2016-02-03T00:00:00Z»
     
    Даты начала и окончания должны быть в [формате ISO](http://en.wikipedia.org/wiki/ISO_8601). Например, 2016-10-14T16:32:41Z. Hello **окончания** времени является необязательным, но мы используем в этом учебнике. 
     
    Если не указать значение для hello **окончания** свойство, оно вычисляется как «**start + 48 часов**». конвейер hello toorun неопределенно долгое время, укажите **9999-09-09** как значение hello для hello **окончания** свойство.
     
    В предыдущих пример hello существует 24 срезы данных, как каждый срез данных создается каждый час.

    Описание свойств JSON в определении конвейера см. в статье [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md). Описание свойств JSON в определении действия копирования см. в статье [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md). Описание свойств JSON, поддерживаемых BlobSource, см. в статье о [соединителе больших двоичных объектов Azure](data-factory-azure-blob-connector.md). Описание свойств JSON, поддерживаемых SqlSink, см. в статье о [соединителе базы данных SQL Azure](data-factory-azure-sql-connector.md).

## <a name="publishdeploy-data-factory-entities"></a>Публикация и развертывание сущностей фабрики данных
На этом этапе вы опубликуете созданные ранее сущности фабрики данных (связанные службы, наборы данных и конвейеры). Также следует определять имя hello hello новых данных фабрики toobe созданного toohold этих сущностей.  

1. Щелкните правой кнопкой мыши проект в обозревателе решений hello и нажмите кнопку **публикации**. 
2. Если вы видите **входа в учетную запись Майкрософт tooyour** диалоговое окно, введите свои учетные данные для hello учетной записи, имеющей подписку Azure и нажмите кнопку **входа**.
3. Вы должны увидеть следующие диалоговое окно приветствия.
   
   ![Диалоговое окно "Опубликовать"](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. На странице фабрики данных Настройка hello hello следующие действия: 
   
   1. Выберите **Создать новую фабрику данных** .
   2. Введите **VSTutorialFactory** в качестве **имени** фабрики данных.  
      
      > [!IMPORTANT]
      > Имя фабрики данных Azure hello Hello должно быть глобально уникальным. Если появляется ошибка об hello имя фабрики данных при публикации, измените имя hello hello фабрики данных (например, yournameVSTutorialFactory) и повторите попытку публикации. Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.        
      > 
      > 
   3. Выберите подписку Azure для hello **подписки** поля.
      
      > [!IMPORTANT]
      > Если вы не видите любую подписку, убедитесь, что вы вошли в учетную запись, которая является администратором или соадминистратором подписки hello.  
      > 
      > 
   4. Выберите hello **группы ресурсов** для hello данных фабрики toobe создан. 
   5. Выберите hello **область** для фабрики данных hello. В раскрывающемся списке hello отображаются только регионов, поддерживаемых hello служба фабрики данных.
   6. Нажмите кнопку **Далее** tooswitch toohello **публиковать элементы** страницы.
      
       ![Страница Configure data factory (Настройка фабрики данных)](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. В hello **публиковать элементы** убедитесь, что все hello фабрик данных сущностей установлены и нажмите кнопку **Далее** tooswitch toohello **Сводка** страницы.
   
   ![Страница Publish items (Публикация элементов)](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. Просмотрите hello сводки и нажмите кнопку **Далее** toostart hello развертывания процесса и представление hello **состояние развертывания**.
   
   ![Страница "Сводка публикации"](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. В hello **состояние развертывания** страницы, вы увидите hello состояние процесса развертывания hello. После завершения развертывания hello, нажмите кнопку "Готово".
 
   ![Страница "Состояние развертывания"](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

Обратите внимание hello после точки. 

* Если ошибка hello: «этой подписки не зарегистрированного toouse имен Microsoft.DataFactory», выполните одно из следующих hello и повторите попытку публикации: 
  
  * В Azure PowerShell запустите hello, следующая команда tooregister hello фабрики данных поставщика. 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    Следующая команда tooconfirm hello можно запустить, hello зарегистрирован поставщик фабрики данных. 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Имя входа с помощью hello подписки Azure в hello [портал Azure](https://portal.azure.com) и перейдите в колонку tooa фабрики данных (или) создать фабрику данных в hello портал Azure. Это действие автоматически регистрирует поставщик hello.
* Имя фабрики данных hello Hello может зарегистрирован как DNS-имя в будущем hello и таким образом становятся общедоступен.

> [!IMPORTANT]
> экземпляры toocreate фабрики данных, необходимо toobe администратором или соадминистратором hello подписки Azure

## <a name="monitor-pipeline"></a>Отслеживание конвейера
Перемещаться toohello домашней страницы для фабрики данных.

1. Войдите в слишком[портал Azure](https://portal.azure.com).
2. Нажмите кнопку **дополнительные службы** hello в левом меню и нажмите кнопку **фабрик данных**.

    ![Обзор фабрик данных](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. Начните вводить имя hello фабрики данных.

    ![Имя фабрики данных](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. Щелкните фабрики данных в hello результаты toosee hello домашней страницы списка для фабрики данных.

    ![Домашняя страница фабрики данных](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. Следуйте инструкциям из [отслеживать наборы данных и конвейера](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello конвейера и наборы данных создан в этом учебнике. Сейчас Visual Studio не поддерживает мониторинг конвейеров фабрики данных. 

## <a name="summary"></a>Сводка
В этом учебнике вы создали данных toocopy фабрики данных Azure из базы данных Azure SQL tooan BLOB-объектов Azure. Вы использовали фабрики данных hello toocreate Visual Studio, связанные службы, наборы данных и конвейера. Ниже приведены hello высокоуровневые действия, выполняемые в этом учебнике.  

1. Создание **фабрики данных Azure**.
2. Создание **связанных служб**.
   1. **Хранилища Azure** связанные toolink службы учетной записи хранилища Azure, содержащий входные данные.     
   2. **Azure SQL** связанные toolink службы базы данных Azure SQL, которое содержит hello выходных данных. 
3. Создание **наборов данных**, описывающих входные и выходные данные для конвейеров.
4. Создание **конвейера** с **BlobSource** в качестве источника и **SqlSink** в качестве приемника с помощью **действия копирования**. 

toosee toouse tootransform данных Hive действие HDInsight с помощью кластера Azure HDInsight. в статье [ учебника: построение первые данные конвейера tootransform использование кластера Hadoop](data-factory-build-your-first-pipeline.md).

Вы можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия. Подробные сведения см. в статье [Планирование и исполнение с использованием фабрики данных](data-factory-scheduling-and-execution.md). 

## <a name="view-all-data-factories-in-server-explorer"></a>Просмотр фабрик данных в обозревателе серверов
В этом разделе описывается toouse hello обозреватель серверов в Visual Studio tooview всех фабрик данных hello в вашей подписке Azure и Создание проекта Visual Studio, в зависимости от существующей фабрики данных. 

1. В **Visual Studio**, нажмите кнопку **представление** hello меню и нажмите кнопку **обозревателя серверов**.
2. Разверните в окне обозревателя серверов hello **Azure** и разверните **фабрики данных**. Если вы видите **входа tooVisual Studio**, введите hello **учетной записи** связанный с подпиской Azure и нажмите кнопку **Продолжить**. Введите **пароль** и нажмите кнопку **Войти**. Visual Studio предпринимает tooget сведения о всех фабрик данных Azure в вашей подписке. Состояние данной операции в hello hello **список задач фабрики данных** окна.

    ![Обозреватель серверов](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a>Создание проекта Visual Studio для имеющейся фабрики данных

- Щелкните правой кнопкой мыши фабрики данных в обозревателе серверов и выберите **tooNew экспорта фабрики данных проекта** toocreate проект Visual Studio основан на существующей фабрики данных.

    ![Экспорт проекта Visual STUDIO tooa фабрики данных](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

## <a name="update-data-factory-tools-for-visual-studio"></a>Обновление средств фабрик данных для Visual Studio
средства tooupdate фабрики данных Azure для Visual Studio hello следующие шаги:

1. Нажмите кнопку **средства** hello меню и выберите пункт **расширения и обновления**. 
2. Выберите **обновления** в hello левой панели, а затем выберите **коллекции Visual Studio**.
3. Выберите **Azure Data Factory tools for Visual Studio** (Средства фабрики данных Azure для Visual Studio) и нажмите кнопку **Обновить**. Если эта запись отсутствует, уже hello последнюю версию средств hello. 

## <a name="use-configuration-files"></a>Использование файлов конфигурации
Файлы конфигурации в свойствах tooconfigure Visual Studio можно использовать для связанной службы, таблицы и конвейеры по-разному для каждой среды.

Рассмотрим следующие определения JSON для связанной службой хранилища Azure hello. toospecify **connectionString** с различными значениями для accountname и accountkey в зависимости от среды (разработки или тестирования и рабочего) toowhich hello развертывании сущностей фабрики данных. Это можно сделать с помощью отдельного файла конфигурации для каждой среды.

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="add-a-configuration-file"></a>Добавление файла конфигурации
Добавьте файл конфигурации для каждой среды, выполнив следующие шаги hello.   

1. Щелкните правой кнопкой мыши hello фабрики данных проекта в решении Visual Studio, выберите пункт слишком**добавить**и нажмите кнопку **новый элемент**.
2. Выберите **Config** выберите из списка установленных шаблонов слева hello hello **файла конфигурации**, введите **имя** для hello конфигурации файла и нажмите кнопку **Добавить**.

    ![Добавление файла конфигурации](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. Добавление параметров конфигурации и их значений в кодировке hello:

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    В этом примере настраивается свойство connectionString связанной службы хранилища Azure и связанной службы Azure SQL. Обратите внимание, что hello синтаксис для указания имени [JsonPath](http://goessner.net/articles/JsonPath/).   

    Если JSON имеет свойство, которое содержит массив значений, как показано на hello, следующий код:  

    ```json
    "structure": [
          {
              "name": "FirstName",
            "type": "String"
          },
          {
            "name": "LastName",
            "type": "String"
        }
    ],
    ```

    Настройте свойства, как показано в hello следующий файл конфигурации (Используйте индексацию с нуля).

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a>Имена свойств c пробелами
Если имя свойства содержит пробелы, используйте квадратные скобки, как показано в hello в следующем примере (имя сервера базы данных):

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a>Развертывание решения с помощью конфигурации
При публикации сущностей фабрики данных Azure в Visual STUDIO, можно указать hello конфигурации требуется toouse для этой операции публикации.

toopublish сущности в проекте фабрики данных Azure, с помощью файла конфигурации:   

1. Щелкните правой кнопкой мыши проект в фабрике данных и нажмите кнопку **публикации** toosee hello **публиковать элементы** диалоговое окно.
2. Выберите существующую фабрику данных или указать значения для создания фабрики данных hello **фабрики данных Настройка** и нажмите кнопку **Далее**.   
3. На hello **публиковать элементы** страницы: отображается список раскрывающегося списка с конфигурации для hello **выбора конфигурации развертывания** поля.

    ![Выбор файла конфигурации](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. Выберите hello **файла конфигурации** , необходимо будет toouse и нажмите кнопку **Далее**.
5. Убедитесь, что это имя hello файла JSON в hello **Сводка** и нажмите кнопку **Далее**.
6. Нажмите кнопку **Готово** после завершения операции развертывания hello.

При развертывании, hello значения из файла конфигурации hello: используется tooset значения свойств в файлах JSON hello, прежде чем сущностей hello развернутой tooAzure служба фабрики данных.   

## <a name="use-azure-key-vault"></a>Использование хранилища ключей Azure
Это не рекомендуется и часто безопасности политики toocommit конфиденциальных данных, таких как репозиторий кода toohello строки подключения. В разделе [ADF Secure публикации](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) на GitHub toolearn о хранение конфиденциальных сведений в хранилище ключей Azure и его использования при публикации сущностей фабрики данных. Hello Secure публикации расширения для Visual Studio позволяет toobe hello секретные данные, хранящиеся в хранилище ключей и только ссылки на toothem указываются в связанных служб или конфигураций развертывания. Эти ссылки разрешаются во время публикации tooAzure сущностей фабрики данных. Эти файлы затем могут быть зафиксированы toosource репозитория без предоставления никакую конфиденциальную информацию.


## <a name="next-steps"></a>Дальнейшие действия
В этом руководстве в ходе операции копирования вы использовали хранилище BLOB-объектов Azure как исходное хранилище данных, а базу данных SQL Azure — как целевое хранилище данных. Hello следующей таблице приведен список хранилищ данных, поддерживаемые действием копирования hello как источники и назначения: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn о том, как хранилище данных toocopy из данных, щелкните ссылку hello hello хранилища данных в таблице hello.
