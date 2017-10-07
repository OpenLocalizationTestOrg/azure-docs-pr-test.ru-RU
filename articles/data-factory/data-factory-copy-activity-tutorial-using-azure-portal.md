---
title: "Учебник: Создание данных toocopy конвейера фабрики данных Azure (портал Azure) | Документы Microsoft"
description: "В этом учебнике вы используете Azure портала toocreate конвейера фабрики данных Azure с toocopy действие копирования данных из базы данных Azure SQL tooan хранилища BLOB-объектов Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d9317652-0170-4fd3-b9b2-37711272162b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fadd840fe9a15cd8831cdb25dccbd10ac42fa161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-azure-portal-toocreate-a-data-factory-pipeline-toocopy-data"></a>Учебник: Использование Azure портала toocreate toocopy данных конвейера фабрики данных 
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

В этой статье вы узнаете, как toouse [портал Azure](https://portal.azure.com) toocreate фабрики данных с конвейером, который копирует данные из базы данных Azure SQL tooan хранилища BLOB-объектов Azure. Если новый tooAzure фабрики данных, прочтите hello [tooAzure введение фабрики данных](data-factory-introduction.md) статьи, прежде чем выполнять задания этого учебника.   

В этом руководстве описывается создание конвейера с одним действием — действием копирования. Действие копирования Hello копирует данные из поддерживаемых хранилища tooa поддерживаемых приемник данных хранилищ данных. Список хранилищ данных, которые поддерживаются в качестве источников и приемников, см. в разделе [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Действие Hello выключен глобально доступной можно копировать данные между различными хранилищами данных в виде безопасные, надежные и масштабируемые службы. Дополнительные сведения о действии копирования hello см. в разделе [действия перемещения данных](data-factory-data-movement-activities.md).

Конвейер может содержать сразу несколько действий. Кроме того, можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия. Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

> [!NOTE] 
> конвейер данных Hello в этом учебнике копирует данные из источника данных хранилища tooa целевое хранилище данных. Учебник о том, как tootransform данных, с помощью фабрики данных Azure, в разделе [учебника: построение конвейера анализа tootransform использование кластера Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Предварительные требования
Выполните предварительные требования, перечисленные в hello [предварительных требованиях для учебников](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) статьи перед выполнением этого учебника.

## <a name="steps"></a>Действия
Ниже приведены hello действий, выполняемых в рамках этого учебника.

1. Создайте **фабрику данных** Azure. На этом этапе вы создадите фабрику данных Azure с именем ADFTutorialDataFactory. 
2. Создание **связанные службы** в фабрике данных hello. На этом этапе вы создадите две связанные службы — службу хранилища Azure и базу данных SQL Azure. 
    
    Hello AzureStorageLinkedService связывает фабрику данных toohello учетной записи хранилища Azure. Создан контейнер и загруженные в рамках учетной записи хранения данных toothis [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    AzureSqlLinkedService связывает фабрику данных toohello базы данных Azure SQL. Hello данные, копируемые из хранилища больших двоичных объектов hello хранится в этой базе данных. Вы создали таблицу SQL в этой базе данных в ходе выполнения [предварительных требований](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   
3. Создать входной и выходной **наборы данных** в фабрике данных hello.  
    
    Hello связанной службой хранилища Azure задает строку подключения hello, который использует служба фабрики данных во время выполнения tooconnect tooyour учетной записи хранилища Azure. И входного BLOB-объекта dataset hello указывает контейнер hello и hello папку, содержащую hello входных данных.  

    Аналогичным образом hello связана база данных SQL Azure службы указывает hello строку подключения, использующее служба фабрики данных в базе данных Azure SQL tooyour tooconnect время выполнения. И SQL таблицы hello выходной набор данных указывает, что таблица hello в данных hello toowhich hello базы данных из хранилища больших двоичных объектов hello копируется.
4. Создание **конвейера** в фабрике данных hello. На этом этапе вы создадите конвейер с действием копирования.   
    
    Действие копирования Hello копирует данные из большого двоичного объекта в таблице tooa хранилища BLOB-объектов Azure hello в базе данных Azure SQL hello. Действие копирования можно использовать в конвейер toocopy данных из любого места назначения tooany поддерживается поддерживаемой исходной. Список поддерживаемых хранилищ данных см. в [этом разделе](data-factory-data-movement-activities.md#supported-data-stores-and-formats). 
5. Монитор hello конвейера. На этом шаге вы **монитор** hello фрагменты наборов входных и выходных данных с помощью портала Azure. 

## <a name="create-data-factory"></a>Создание фабрики данных
> [!IMPORTANT]
> Полный [необходимых компонентов для учебника hello](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) Если это еще не сделано.   

Фабрика данных может иметь один или несколько конвейеров. Конвейер может содержать одно или несколько действий. Например toocopy действие копирования данных из целевое хранилище данных источника tooa и toorun действие Hive в HDInsight tootransform скрипт Hive входных данных tooproduct выходных данных. Давайте начнем с создания фабрики данных hello на этом шаге.

1. После входа в toohello [портал Azure](https://portal.azure.com/), нажмите кнопку **New** hello левого меню **данные + аналитика**и нажмите кнопку **фабрики данных**. 
   
   ![Создать -> Фабрика данных](./media/data-factory-copy-activity-tutorial-using-azure-portal/NewDataFactoryMenu.png)    
2. В hello **новую фабрику данных** колонки:
   
   1. Введите **ADFTutorialDataFactory** для hello **имя**. 
      
         ![Создать колонку "Фабрика данных"](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-new-data-factory.png)
      
       Имя фабрики данных Azure hello Hello должно быть **глобальный уникальный**. Если появляется следующая ошибка hello, измените имя hello hello фабрики данных (например, yournameADFTutorialDataFactory) и повторите попытку создания. Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.
      
           Data factory name “ADFTutorialDataFactory” is not available  
      
       ![Имя фабрики данных недоступно](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-not-available.png)
   2. Выберите Azure **подписки** требуется фабрики данных toocreate hello. 
   3. Для hello **группы ресурсов**, выполните одно из hello следующие шаги:
      
      - Выберите **использовать существующие**и выберите существующую группу ресурсов из раскрывающегося списка hello. 
      - Выберите **создать новый**и введите имя группы ресурсов hello.   
         
          Некоторые шаги hello в этом учебнике предполагается использовать имя hello: **ADFTutorialResourceGroup** для группы ресурсов hello. toolearn о группах ресурсов. в разделе [с помощью ресурса группы toomanage ресурсам Azure](../azure-resource-manager/resource-group-overview.md).  
   4. Выберите hello **расположение** для фабрики данных hello. В раскрывающемся списке hello отображаются только регионов, поддерживаемых hello служба фабрики данных.
   5. Выберите **toodashboard ПИН-кода**.     
   6. Щелкните **Создать**.
      
      > [!IMPORTANT]
      > экземпляры toocreate фабрики данных, необходимо быть членом hello [участника фабрики данных](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) роли на уровне группы hello подписки или ресурса.
      > 
      > Имя фабрики данных hello Hello может зарегистрирован как DNS-имя в будущем hello и таким образом становятся общедоступен.                
      > 
      > 
3. На панели мониторинга hello см следующие hello плитку с состоянием: **развертывание фабрики данных**. 

    ![Элемент Deploying data factory (Развертывание фабрики данных)](media/data-factory-copy-activity-tutorial-using-azure-portal/deploying-data-factory.png)
4. После завершения создания hello, вы видите hello **фабрики данных** колонки, как показано на рисунке hello.
   
   ![Домашняя страница фабрики данных](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-home-page.png)

## <a name="create-linked-services"></a>Создание связанных служб
Создания связанных служб в toolink фабрики данных, хранит и вычислений фабрики данных toohello службы данных. В этом руководстве не используются службы вычислений, например Azure HDInsight или Azure Data Lake Analytics. Вы используете два хранилища данных — служба хранилища Azure (источник) и база данных SQL Azure (конечное хранилище). 

Поэтому нужно создать две связанные службы: служба хранилища Azure с именем AzureStorageLinkedService и база данных SQL Azure с именем AzureSqlLinkedService.  

Hello AzureStorageLinkedService связывает фабрику данных toohello учетной записи хранилища Azure. Эта учетная запись хранения является hello один в котором можно создать контейнер и загруженные данные hello в рамках [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

AzureSqlLinkedService связывает фабрику данных toohello базы данных Azure SQL. Hello данные, копируемые из хранилища больших двоичных объектов hello хранится в этой базе данных. Создана таблица emp hello в этой базе данных как часть [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).  

### <a name="create-azure-storage-linked-service"></a>Создание связанной службы хранения Azure
На этом шаге связать фабрики данных tooyour учетной записи хранилища Azure. Укажите имя hello и ключ учетной записи хранилища Azure в этом разделе.  

1. В hello **фабрики данных** колонка, щелкните **автор и развертывание** плитки.
   
   ![Плитка "Создание и развертывание"](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-author-deploy-tile.png) 
2. Вы видите hello **редактор фабрики данных** как показано в hello после изображения: 

    ![Редактор фабрики данных](./media/data-factory-copy-activity-tutorial-using-azure-portal/data-factory-editor.png)
3. В редакторе hello щелкните **новое хранилище данных** кнопку на hello и отметьте **хранилища Azure** hello раскрывающегося меню. Вы увидите hello шаблон JSON для создания связанной службой хранилища Azure в правой области hello. 
   
    ![Кнопка "Создать хранилище данных" в редакторе](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-newdatastore-button.png)    
3. Замените `<accountname>` и `<accountkey>` с hello учетной записи имя и учетную запись значения ключа для вашей учетной записи хранилища Azure. 
   
    ![Хранилище больших двоичных объектов JSON в редакторе](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-json.png)    
4. Нажмите кнопку **развернуть** на панели инструментов hello. Вы увидите hello развернут **AzureStorageLinkedService** теперь в дереве hello просматривать. 
   
    ![Развертывание хранилища больших двоичных объектов в редакторе](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-deploy.png)

    Дополнительные сведения о свойствах JSON в определении службы hello связаны см. в разделе [соединителя хранилища больших двоичных объектов](data-factory-azure-blob-connector.md#linked-service-properties) статьи.

### <a name="create-a-linked-service-for-hello-azure-sql-database"></a>Создание связанной службы для hello базы данных SQL Azure
На этом шаге связать фабрики данных tooyour базы данных Azure SQL. Укажите имя сервера Azure SQL hello, имя базы данных, имя пользователя и пароль пользователя в этом разделе. 

1. В hello **редактор фабрики данных**, нажмите кнопку **новое хранилище данных** кнопку на hello и отметьте **базы данных SQL Azure** hello раскрывающегося меню. Вы увидите hello шаблон JSON для создания hello связанной службой Azure SQL в правой области hello.
2. Замените `<servername>`, `<databasename>`, `<username>@<servername>` и `<password>` именем своего сервера SQL Azure, именем учетной записи пользователя и паролем. 
3. Нажмите кнопку **развернуть** hello toocreate инструментов и развернуть hello **AzureSqlLinkedService**.
4. Убедитесь, что это **AzureSqlLinkedService** в древовидном представлении hello под **связанные службы**.  

    Дополнительные сведения об этих свойствах JSON см. в статье о [соединителе базы данных SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties).

## <a name="create-datasets"></a>Создание наборов данных
В предыдущем шаге hello создать связанные службы toolink вашей учетной записи хранилища Azure и фабрику данных tooyour базы данных Azure SQL. На этом шаге можно определить два набора данных с именем InputDataset и OutputDataset, представляющие входные данные и выходные данные, которые хранятся в хранилищах данных hello, на которые ссылается AzureStorageLinkedService и AzureSqlLinkedService соответственно.

Hello связанной службой хранилища Azure задает строку подключения hello, который использует служба фабрики данных во время выполнения tooconnect tooyour учетной записи хранилища Azure. И hello входного BLOB-объекта dataset (InputDataset) указывает контейнер hello и hello папку, содержащую hello входных данных.  

Аналогичным образом hello связана база данных SQL Azure службы указывает hello строку подключения, использующее служба фабрики данных в базе данных Azure SQL tooyour tooconnect время выполнения. И hello выходной набор данных таблицы SQL (OututDataset) указывает таблицу hello в hello базы данных toowhich hello и копирования данных из хранилища больших двоичных объектов hello. 

### <a name="create-input-dataset"></a>Создание входного набора данных
На этом шаге создается набор данных с именем InputDataset, который указывает файл tooa больших двоичных объектов (emp.txt) в корневой папке hello контейнер больших двоичных объектов (adftutorial) в hello представленный hello AzureStorageLinkedService связанной службы хранилища Azure. Если не указать значение для имени файла hello (или пропустить его), данные из всех больших двоичных объектов в папке входной hello, скопированный toohello назначения. В этом учебнике укажите значение для имени файла hello. 

1. В hello **редактор** hello фабрики данных, щелкните **... Дополнительные**, нажмите кнопку **новый набор данных**и нажмите кнопку **хранилища больших двоичных объектов Azure** hello раскрывающегося меню. 
   
    ![Меню "Новый набор данных"](./media/data-factory-copy-activity-tutorial-using-azure-portal/new-dataset-menu.png)
2. Замените JSON в правой области hello hello, следующий фрагмент JSON: 
   
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
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
          "folderPath": "adftutorial/",
          "fileName": "emp.txt",
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
3. Нажмите кнопку **развернуть** hello toocreate инструментов и развернуть hello **InputDataset** набора данных. Подтвердите, что вы видите hello **InputDataset** в представлении дерева hello.

### <a name="create-output-dataset"></a>Создание выходного набора данных
Hello базы данных SQL Azure связанные службы задает hello строку подключения, использующее служба фабрики данных в базе данных Azure SQL tooyour tooconnect время выполнения. Hello выходного SQL таблицы набора данных (OututDataset) на этом шаге создается указывает, что таблица hello в данных hello toowhich hello базы данных из хранилища больших двоичных объектов hello копируется.

1. В hello **редактор** hello фабрики данных, щелкните **... Дополнительные**, нажмите кнопку **новый набор данных**и нажмите кнопку **Azure SQL** hello раскрывающегося меню. 
2. Замените JSON в правой области hello hello, следующий фрагмент JSON:

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
        "linkedServiceName": "AzureSqlLinkedService",
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
3. Нажмите кнопку **развернуть** hello toocreate инструментов и развернуть hello **OutputDataset** набора данных. Подтвердите, что вы видите hello **OutputDataset** в древовидном представлении hello под **наборы данных**. 

## <a name="create-pipeline"></a>Создание конвейера
На этом этапе вы создадите конвейер с **действием копирования**, которое использует **InputDataset** в качестве входных данных и **OutputDataset** в качестве выходных.

В настоящее время выходной набор данных — того, какие диски hello расписания. В этом учебнике выходной набор данных является настроенным tooproduce срез один раз в час. конвейер Hello содержит время начала и время окончания, которые однажды друг от друга, что составляет 24 часа. Таким образом 24 фрагменты выходной набор данных создают hello конвейера. 

1. В hello **редактор** hello фабрики данных, щелкните **... Дополнительно** и **Новый конвейер**. Кроме того, можно щелкнуть **конвейеры** в древовидном представлении hello и нажмите кнопку **новый конвейер**.
2. Замените JSON в правой области hello hello, следующий фрагмент JSON: 

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
              "retry": 0,
              "timeout": "01:00:00"
            }
          }
        ],
        "start": "2017-05-11T00:00:00Z",
        "end": "2017-05-12T00:00:00Z"
      }
    } 
    ```   
    
    Обратите внимание hello после точки.
   
    - В разделе "действия" hello, имеется только одно действие, **тип** задано слишком**копирования**. Дополнительные сведения о действии копирования hello см. в разделе [действия перемещения данных](data-factory-data-movement-activities.md). В решениях фабрики данных можно также использовать [действия преобразования данных](data-factory-data-transformation-activities.md).
    - Входных данных для действия hello установлено слишком**InputDataset** и вывода для hello действия установлено слишком**OutputDataset**. 
    - В hello **typeProperties** разделе **BlobSource** указан в качестве типа источника hello и **SqlSink** указан как тип приемника hello. Перечень хранилищ данных, поддерживаемые действием копирования hello как источники и приемники см. в разделе [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats). как сохранить toouse конкретных поддерживаемые данные в качестве источника и приемника, toolearn по ссылке hello в таблице hello.
    - Даты начала и окончания должны быть в [формате ISO](http://en.wikipedia.org/wiki/ISO_8601). Например, 2016-10-14T16:32:41Z. Hello **окончания** времени является необязательным, но мы используем в этом учебнике. Если не указать значение для hello **окончания** свойство, оно вычисляется как «**start + 48 часов**». конвейер hello toorun неопределенно долгое время, укажите **9999-09-09** как значение hello для hello **окончания** свойство.
     
    В предыдущих пример hello существует 24 срезы данных, как каждый срез данных создается каждый час.

    Описание свойств JSON в определении конвейера см. в статье [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md). Описание свойств JSON в определении действия копирования см. в статье [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md). Описание свойств JSON, поддерживаемых BlobSource, см. в статье о [соединителе больших двоичных объектов Azure](data-factory-azure-blob-connector.md). Описание свойств JSON, поддерживаемых SqlSink, см. в статье о [соединителе базы данных SQL Azure](data-factory-azure-sql-connector.md).
3. Нажмите кнопку **развернуть** hello toocreate инструментов и развернуть hello **ADFTutorialPipeline**. Подтвердите, что вы видите hello конвейера в представлении дерева hello. 
4. Теперь закройте hello **редактор** колонки, щелкнув **X**. Нажмите кнопку **X** снова hello toosee **фабрики данных** Домашняя страница hello **ADFTutorialDataFactory**.

**Поздравляем!** Успешно создана фабрикой данных Azure с toocopy конвейера данных из базы данных Azure SQL tooan хранилища BLOB-объектов Azure. 


## <a name="monitor-pipeline"></a>Отслеживание конвейера
На этом шаге используется hello Azure портала toomonitor, происходящем в фабрикой данных Azure.    

### <a name="monitor-pipeline-using-monitor--manage-app"></a>Мониторинг конвейера с использованием приложения по мониторингу и управлению
Hello следующие шаги показывают, как toomonitor конвейеров в вашей фабрике данных с помощью приложения hello отслеживать состо & Управление: 

1. Нажмите кнопку **отслеживать состо & Управление** плитки на домашней странице приветствия для фабрики данных.
   
    ![Плитка Monitor & Manage (Мониторинг и управление)](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-manage-tile.png) 
2. **Приложение "Мониторинг и управление"** должно появиться на отдельной вкладке. 

    > [!NOTE]
    > При появлении этого веб-браузер hello застряла в «Авторизации...», выполните одно из следующих hello: очистить hello **блокировать сторонние файлы cookie и данным сайта** флажок (или) создайте исключение для **login.microsoftonline.com**, а затем повторите попытку tooopen приложение hello.

    ![Приложение по мониторингу и управлению](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-and-manage-app.png)
3. Изменение hello **время начала** и **время окончания** tooinclude запуск (2017 г-05-11) и завершить конвейер время (2017 г-05-12) и нажмите кнопку **применить**.     
3. Вы видите hello **действия windows** связанные с каждый час между конвейера начала и окончания раз в списке hello в средней области hello. 
4. toosee сведения об окне действие, выберите hello окна действия в hello **действия Windows** списка. 
    ![Сведения об окне действия](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)

    В проводнике Windows действия на правой hello, вы видите, hello срезы вверх toohello текущее время в формате UTC (8:12 PM) обрабатываются (в зеленый цвет). 8-9 PM, PM, 9 10 10 11 PM, 23: 00 - 12: 00 фрагменты Hello еще не обрабатываются.

    Hello **попыток** раздел в правой области содержит сведения о выполнении для среза данных hello действия hello hello. Если произошла ошибка, он предоставляет сведения об ошибке hello. Например если hello входных данных, папке или контейнер не существует и происходит сбой обработки среза hello, появится сообщение о этот контейнер hello или папка не существует.

    ![Попытки выполнения действия](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-run-attempts.png) 
4. Запустите **SQL Server Management Studio**, подключение toohello базы данных SQL Azure и убедитесь, что hello строки вставляются в toohello **emp** таблицы в базе данных hello.
    
    ![результаты SQL-запроса](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)

Дополнительные сведения об использовании этого приложения см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью нового приложения по мониторингу и управлению](data-factory-monitor-manage-app.md).

### <a name="monitor-pipeline-using-diagram-view"></a>Мониторинг конвейера с использованием представления схемы
Вы также можете монитор конвейеры данных с помощью представления диаграммы hello.  

1. В hello **фабрики данных** колонка, щелкните **схема**.
   
    ![Колонка "Фабрика данных" — плитка схемы](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-datafactoryblade-diagramtile.png)
2. Вы увидите примерно toohello hello диаграммы после изображения: 
   
    ![Представление схемы](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-diagram-blade.png)  
5. В представлении диаграммы hello, дважды щелкните **InputDataset** toosee фрагменты для hello набора данных.  
   
    ![Наборы данных с выбранным элементом InputDataset](./media/data-factory-copy-activity-tutorial-using-azure-portal/DataSetsWithInputDatasetFromBlobSelected.png)   
5. Нажмите кнопку **увеличить** связать toosee все срезы данных hello. Вы увидите срезы, созданные в течение 24 часов в промежутке между временем начала и окончания конвейера. 
   
    ![Все срезы входных данных](./media/data-factory-copy-activity-tutorial-using-azure-portal/all-input-slices.png)  
   
    Обратите внимание, что все hello срезы данных вверх toohello текущее время в формате UTC, **готовности** поскольку hello **emp.txt** файл существует все время hello в контейнер больших двоичных объектов hello: **adftutorial\input**. срезы Hello для будущих раз hello еще не в состоянии готовности. Убедитесь, что нет срезов показываться в hello **недавно с неудачными срезами** раздела внизу hello.
6. Закрыть hello колонок, пока вы см hello схему представления (или) прокрутки влево toosee hello схему просмотра. Затем дважды щелкните **OutputDataset**. 
8. Нажмите кнопку **дополнительную информацию см** ссылку на hello **таблицы** колонке **OutputDataset** toosee все hello срезов.

    ![Колонка срезов данных](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslices-blade.png) 
9. Обратите внимание, что все hello фрагменты вверх toohello текущее время UTC переместить из **ожидающие выполнения** состояние = > **выполняется** ==> **готовности** состояния. Здравствуйте фрагменты из последних hello (до текущего времени) обрабатываются из последней toooldest по умолчанию. Например если hello текущее время — 20:12:00 UTC, до 18: 00 – 19: 00 срез hello обрабатывается hello срез для 19: 00 - 20: 00. Hello 20: 00 – 9 по срез обрабатывается в конце hello hello интервал времени по умолчанию, после 9 PM.  
10. Щелкните любой сегмент данных из списка hello и вы увидите hello **срез данных** колонку. Фрагмент данных, связанный с окном действия, называется срезом. Срез может быть одним файлом или несколькими файлами.  
    
     ![Колонка среза данных](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslice-blade.png)
    
     Если срез hello не hello **готовности** состояние, можно увидеть hello восходящие срезы, которые еще не готовы и блокируют hello текущего среза выполнения в hello **восходящие срезы, которые не готовы** списка.
11. В hello **СРЕЗ данных** колонку, вы увидите все действие выполняется в списке hello нижней hello. Нажмите кнопку **при выполнении действия** toosee hello **сведения о выполнении действия** колонку. 
    
    ![Сведения о выполнении действия](./media/data-factory-copy-activity-tutorial-using-azure-portal/ActivityRunDetails.png)

    В этой колонке отображается как потребовалось бы операции копирования long hello, какая пропускная способность, сколько байт данных были чтения и время начала записи, запустите, выполняется время окончания и т. д.  
12. Нажмите кнопку **X** tooclose все колонках hello, пока не будет вернуть toohello домашней колонке hello **ADFTutorialDataFactory**.
13. (необязательно) щелкните hello **наборы данных** плитки или **конвейеры** колонок hello tooget плитки, вы увидели hello описанные выше шаги. 
14. Запустите **SQL Server Management Studio**, подключение toohello базы данных SQL Azure и убедитесь, что hello строки вставляются в toohello **emp** таблицы в базе данных hello.
    
    ![результаты SQL-запроса](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)


## <a name="summary"></a>Сводка
В этом учебнике вы создали данных toocopy фабрики данных Azure из базы данных Azure SQL tooan BLOB-объектов Azure. Вы использовали фабрики данных hello Azure портала toocreate hello, связанные службы, наборы данных и конвейера. Ниже приведены hello высокоуровневые действия, выполняемые в этом учебнике.  

1. Создание **фабрики данных Azure**.
2. Создание **связанных служб**.
   1. **Хранилища Azure** связанные toolink службы учетной записи хранилища Azure, содержащий входные данные.     
   2. **Azure SQL** связанные toolink службы базы данных Azure SQL, которое содержит hello выходных данных. 
3. Создание **наборов данных** , которые описывают входные и выходные данные для конвейеров.
4. Создание **конвейера** с **BlobSource** в качестве источника и **SqlSink** в качестве приемника с помощью **действия копирования**.  

## <a name="next-steps"></a>Дальнейшие действия
В этом руководстве в ходе операции копирования вы использовали хранилище BLOB-объектов Azure как исходное хранилище данных, а базу данных SQL Azure — как целевое хранилище данных. Hello следующей таблице приведен список хранилищ данных, поддерживаемые действием копирования hello как источники и назначения: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn о том, как хранилище данных toocopy из данных, щелкните ссылку hello hello хранилища данных в таблице hello.
