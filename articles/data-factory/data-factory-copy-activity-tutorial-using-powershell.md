---
title: "Учебник: Создание конвейера toomove данных с помощью Azure PowerShell | Документы Microsoft"
description: "В этом руководстве вы создадите конвейер фабрики данных Azure с действием копирования с помощью Azure PowerShell."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 71087349-9365-4e95-9847-170658216ed8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 21406d7dfaa0c555b2538fbb52839d761c140fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a>Руководство по созданию конвейера фабрики данных для переноса данных с помощью Azure PowerShell
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

В этой статье вы узнаете, как toocreate toouse PowerShell фабрики данных с конвейером, который копирует данные из базы данных Azure SQL tooan хранилища BLOB-объектов Azure. Если новый tooAzure фабрики данных, прочтите hello [tooAzure введение фабрики данных](data-factory-introduction.md) статьи, прежде чем выполнять задания этого учебника.   

В этом руководстве описывается создание конвейера с одним действием — действием копирования. Действие копирования Hello копирует данные из поддерживаемых хранилища tooa поддерживаемых приемник данных хранилищ данных. Список хранилищ данных, которые поддерживаются в качестве источников и приемников, см. в разделе [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Действие Hello выключен глобально доступной можно копировать данные между различными хранилищами данных в виде безопасные, надежные и масштабируемые службы. Дополнительные сведения о действии копирования hello см. в разделе [действия перемещения данных](data-factory-data-movement-activities.md).

Конвейер может содержать сразу несколько действий. Кроме того, можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия. Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

> [!NOTE]
> Данная статья не охватывает все командлеты фабрики данных hello. Полную документацию по этим командлетам см. в [справочнике](/powershell/module/azurerm.datafactories).
> 
> конвейер данных Hello в этом учебнике копирует данные из источника данных хранилища tooa целевое хранилище данных. Учебник о том, как tootransform данных, с помощью фабрики данных Azure, в разделе [учебника: построение конвейера анализа tootransform использование кластера Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Предварительные требования
- Выполните предварительные требования, перечисленные в hello [предварительных требованиях для учебников](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) статьи.
- Установите **Azure PowerShell**. Следуйте инструкциям в разделе hello [как tooinstall и настройка Azure PowerShell](../powershell-install-configure.md).

## <a name="steps"></a>Действия
Ниже приведены hello действий, выполняемых в рамках этого учебника.

1. Создайте **фабрику данных** Azure. На этом этапе вы создадите фабрику данных Azure с именем ADFTutorialDataFactoryPSH. 
2. Создание **связанные службы** в фабрике данных hello. На этом этапе вы создадите две связанные службы — службу хранилища Azure и базу данных SQL Azure. 
    
    Hello AzureStorageLinkedService связывает фабрику данных toohello учетной записи хранилища Azure. Создан контейнер и загруженные в рамках учетной записи хранения данных toothis [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    AzureSqlLinkedService связывает фабрику данных toohello базы данных Azure SQL. Hello данные, копируемые из хранилища больших двоичных объектов hello хранится в этой базе данных. Вы создали таблицу SQL в этой базе данных в ходе выполнения [предварительных требований](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   
3. Создать входной и выходной **наборы данных** в фабрике данных hello.  
    
    Hello связанной службой хранилища Azure задает строку подключения hello, который использует служба фабрики данных во время выполнения tooconnect tooyour учетной записи хранилища Azure. И входного BLOB-объекта dataset hello указывает контейнер hello и hello папку, содержащую hello входных данных.  

    Аналогичным образом hello связана база данных SQL Azure службы указывает hello строку подключения, использующее служба фабрики данных в базе данных Azure SQL tooyour tooconnect время выполнения. И SQL таблицы hello выходной набор данных указывает, что таблица hello в данных hello toowhich hello базы данных из хранилища больших двоичных объектов hello копируется.
4. Создание **конвейера** в фабрике данных hello. На этом этапе вы создадите конвейер с действием копирования.   
    
    Действие копирования Hello копирует данные из большого двоичного объекта в таблице tooa хранилища BLOB-объектов Azure hello в базе данных Azure SQL hello. Действие копирования можно использовать в конвейер toocopy данных из любого места назначения tooany поддерживается поддерживаемой исходной. Список поддерживаемых хранилищ данных см. в [этом разделе](data-factory-data-movement-activities.md#supported-data-stores-and-formats). 
5. Монитор hello конвейера. На этом шаге вы **монитор** hello фрагменты наборов входных и выходных данных с помощью PowerShell.

## <a name="create-a-data-factory"></a>Создать фабрику данных
> [!IMPORTANT]
> Полный [необходимых компонентов для учебника hello](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) Если это еще не сделано.   

Фабрика данных может иметь один или несколько конвейеров. Конвейер может содержать одно или несколько действий. Например toocopy действие копирования данных из целевое хранилище данных источника tooa и toorun действие Hive в HDInsight tootransform скрипт Hive входных данных tooproduct выходных данных. Давайте начнем с создания фабрики данных hello на этом шаге.

1. Запустите **PowerShell**. Не закрывайте Azure PowerShell до завершения этого учебника hello. Если закрыть и снова открыть понадобятся toorun hello команд.

    Запустите следующую команду hello и введите hello имя пользователя и пароль, использовать toosign в toohello портал Azure.

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    Выполните следующие команды tooview hello все hello подписки для этой учетной записи:

    ```PowerShell
    Get-AzureRmSubscription
    ```

    Следующая команда tooselect hello подписки на toowork с выполнения hello. Замените  **&lt;NameOfAzureSubscription** &gt; с именем hello подписки Azure:

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. Создание группы ресурсов Azure с именем **ADFTutorialResourceGroup** , выполнив следующую команду hello:

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    Некоторые шаги hello в этом учебнике предполагается использовать с именем группы ресурсов hello **ADFTutorialResourceGroup**. Если вы используете другой группе ресурсов, необходимо toouse его вместо ADFTutorialResourceGroup в этом учебнике.
3. Запустите hello **New AzureRmDataFactory** toocreate командлет фабрики данных с именем **ADFTutorialDataFactoryPSH**:  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    Это имя уже может использоваться. Таким образом, чтобы hello имя фабрики данных hello уникальными путем добавления префикса или суффикса (например: ADFTutorialDataFactoryPSH05152017) и снова выполните команду hello.  

Обратите внимание hello после точки.

* Имя фабрики данных Azure hello Hello должно быть глобально уникальным. Если появляется следующая ошибка hello, измените имя hello (например, yournameADFTutorialDataFactoryPSH). Используйте это имя вместо ADFTutorialFactoryPSH при выполнении шагов в этом руководстве. Ознакомьтесь с [правилами именования](data-factory-naming-rules.md) артефактов фабрики данных.

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* экземпляры toocreate фабрики данных, вы должны быть участника или администратор hello подписки Azure.
* Hello имя фабрики данных hello быть зарегистрировано как DNS-имя в будущем hello и поэтому становятся публично видимых.
* Может появиться следующая ошибка hello: «**этой подписки не является пространством имен зарегистрированных toouse Microsoft.DataFactory.**» Выполните одно из следующих hello и повторите попытку публикации:

  * В Azure PowerShell выполните hello, следующая команда tooregister hello фабрики данных поставщика.

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    Выполните следующие команды tooconfirm hello, hello зарегистрирован поставщик фабрики данных:

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Вход с помощью hello подписки Azure toohello [портал Azure](https://portal.azure.com). Перейдите в колонку tooa фабрики данных или создать фабрику данных в hello портал Azure. Это действие автоматически регистрирует поставщик hello.

## <a name="create-linked-services"></a>Создание связанных служб
Создания связанных служб в toolink фабрики данных, хранит и вычислений фабрики данных toohello службы данных. В этом руководстве не используются службы вычислений, например Azure HDInsight или Azure Data Lake Analytics. Вы используете два хранилища данных — служба хранилища Azure (источник) и база данных SQL Azure (конечное хранилище). 

Поэтому нужно создать две связанные службы: служба хранилища Azure с именем AzureStorageLinkedService и база данных SQL Azure с именем AzureSqlLinkedService.  

Hello AzureStorageLinkedService связывает фабрику данных toohello учетной записи хранилища Azure. Эта учетная запись хранения является hello один в котором можно создать контейнер и загруженные данные hello в рамках [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

AzureSqlLinkedService связывает фабрику данных toohello базы данных Azure SQL. Hello данные, копируемые из хранилища больших двоичных объектов hello хранится в этой базе данных. Создана таблица emp hello в этой базе данных как часть [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a>Создание связанной службы для учетной записи хранения Azure
На этом шаге связать фабрики данных tooyour учетной записи хранилища Azure.

1. Создайте JSON-файл с именем **AzureStorageLinkedService.json** в **C:\ADFGetStartedPSH** папка с hello после содержимого: (Создание hello папки ADFGetStartedPSH, если он еще не существует.)

    > [!IMPORTANT]
    > Замените &lt;accountname&gt; и &lt;accountkey&gt; с именем и ключом вашей учетной записи хранилища Azure, прежде чем сохранять файл hello. 

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
2. В **Azure PowerShell**, переключение toohello **ADFGetStartedPSH** папки.
4. Запустите hello **New AzureRmDataFactoryLinkedService** toocreate hello командлет связанной службы: **AzureStorageLinkedService**. Этот командлет и другие командлеты фабрики данных, используемый в этом учебнике требуется toopass значения для hello **ResourceGroupName** и **с именем DataFactoryName** параметров. Кроме того можно передать объект DataFactory hello, возвращаемых командлетом New-AzureRmDataFactory hello без ввода ResourceGroupName и с именем DataFactoryName каждый раз при запуске командлета. 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    Вот пример выходных данных hello.

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    Второй способ создания эта связанная служба — имя группы ресурсов toospecify и имя фабрики данных вместо указания hello объекта DataFactory.  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a>Создание связанной службы для Базы данных SQL Azure
На этом шаге связать фабрики данных tooyour базы данных Azure SQL.

1. Создайте JSON-файл с именем AzureSqlLinkedService.json в папке C:\ADFGetStartedPSH и hello после содержимого:

    > [!IMPORTANT]
    > Вместо &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt; и &lt;password&gt; укажите имя своего сервера Azure SQL Server, имя базы данных, имя учетной записи пользователя и пароль.
    
    ```json
    {
        "name": "AzureSqlLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": "Server=tcp:<server>.database.windows.net,1433;Database=<databasename>;User ID=<user>@<server>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        }
     }
    ```
2. Выполните следующие команды toocreate hello связанной службы:

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    Вот пример выходных данных hello.

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   Убедитесь, что **разрешить доступ службы tooAzure** будет включена для базы данных SQL server. tooverify и включите его, hello следующие действия:

    1. Войдите в toohello [портал Azure](https://portal.azure.com)
    2. Нажмите кнопку **дополнительные службы >** hello слева, а затем нажмите **серверов SQL Server** в hello **баз данных** категории.
    3. Выберите сервер в список серверов SQL Server hello.
    4. В колонке hello SQL server выберите **Показать параметры брандмауэра** ссылку.
    5. В hello **параметры брандмауэра** колонка, щелкните **ON** для **разрешить доступ службы tooAzure**.
    6. Нажмите кнопку **Сохранить** на панели инструментов hello. 

## <a name="create-datasets"></a>Создание наборов данных
В предыдущем шаге hello создать связанные службы toolink вашей учетной записи хранилища Azure и фабрику данных tooyour базы данных Azure SQL. На этом шаге можно определить два набора данных с именем InputDataset и OutputDataset, представляющие входные данные и выходные данные, которые хранятся в хранилищах данных hello, на которые ссылается AzureStorageLinkedService и AzureSqlLinkedService соответственно.

Hello связанной службой хранилища Azure задает строку подключения hello, который использует служба фабрики данных во время выполнения tooconnect tooyour учетной записи хранилища Azure. И hello входного BLOB-объекта dataset (InputDataset) указывает контейнер hello и hello папку, содержащую hello входных данных.  

Аналогичным образом hello связана база данных SQL Azure службы указывает hello строку подключения, использующее служба фабрики данных в базе данных Azure SQL tooyour tooconnect время выполнения. И hello выходной набор данных таблицы SQL (OututDataset) указывает таблицу hello в hello базы данных toowhich hello и копирования данных из хранилища больших двоичных объектов hello. 

### <a name="create-an-input-dataset"></a>Создание входного набора данных
На этом шаге создается набор данных с именем InputDataset, который указывает файл tooa больших двоичных объектов (emp.txt) в корневой папке hello контейнер больших двоичных объектов (adftutorial) в hello представленный hello AzureStorageLinkedService связанной службы хранилища Azure. Если не указать значение для имени файла hello (или пропустить его), данные из всех больших двоичных объектов в папке входной hello, скопированный toohello назначения. В этом учебнике укажите значение для имени файла hello.  

1. Создайте JSON-файл с именем **InputDataset.json** в hello **C:\ADFGetStartedPSH** папке с hello после содержимого:

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
                "fileName": "emp.txt",
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
2. Запустите hello, следующая команда toocreate hello фабрики данных dataset.

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    Вот пример выходных данных hello.

    ```
    DatasetName       : InputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureBlobDataset
    Policy            : Microsoft.Azure.Management.DataFactories.Common.Models.Policy
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

### <a name="create-an-output-dataset"></a>Создание выходного набора данных
В этой части hello шаг создания выходной набор данных с именем **OutputDataset**. Этот набор данных указывает tooa SQL таблицы в базе данных Azure SQL hello, представленного **AzureSqlLinkedService**. 

1. Создайте JSON-файл с именем **OutputDataset.json** в hello **C:\ADFGetStartedPSH** папка с hello после содержимого:

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
2. Запустите следующий набор данных hello данных команды toocreate фабрики hello.

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    Вот пример выходных данных hello.

    ```
    DatasetName       : OutputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureSqlTableDataset
    Policy            :
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

## <a name="create-a-pipeline"></a>Создание конвейера
На этом этапе вы создадите конвейер с **действием копирования**, которое использует **InputDataset** в качестве входных данных и **OutputDataset** в качестве выходных.

В настоящее время выходной набор данных — того, какие диски hello расписания. В этом учебнике выходной набор данных является настроенным tooproduce срез один раз в час. конвейер Hello содержит время начала и время окончания, которые однажды друг от друга, что составляет 24 часа. Таким образом 24 фрагменты выходной набор данных создают hello конвейера. 


1. Создайте JSON-файл с именем **ADFTutorialPipeline.json** в hello **C:\ADFGetStartedPSH** папке с hello после содержимого:

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
     
    Замените значение hello hello **запустить** свойство с hello текущего дня и **окончания** значение с hello следующего дня. Можно указать только часть даты hello и пропустить hello время hello Дата и время. Например, «2016-02-03», который является эквивалентом "2016-02-03T00:00:00Z»
     
    Даты начала и окончания должны быть в [формате ISO](http://en.wikipedia.org/wiki/ISO_8601). Например, 2016-10-14T16:32:41Z. Hello **окончания** времени является необязательным, но мы используем в этом учебнике. 
     
    Если не указать значение для hello **окончания** свойство, оно вычисляется как «**start + 48 часов**». конвейер hello toorun неопределенно долгое время, укажите **9999-09-09** как значение hello для hello **окончания** свойство.
     
    В предыдущих пример hello существует 24 срезы данных, как каждый срез данных создается каждый час.

    Описание свойств JSON в определении конвейера см. в статье [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md). Описание свойств JSON в определении действия копирования см. в статье [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md). Описание свойств JSON, поддерживаемых BlobSource, см. в статье о [соединителе больших двоичных объектов Azure](data-factory-azure-blob-connector.md). Описание свойств JSON, поддерживаемых SqlSink, см. в статье о [соединителе базы данных SQL Azure](data-factory-azure-sql-connector.md).
2. Выполнения hello следующая команда таблицу фабрики данных toocreate hello.

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    Вот пример выходных данных hello. 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

**Поздравляем!** Успешно создана фабрикой данных Azure с toocopy конвейера данных из базы данных Azure SQL tooan хранилища BLOB-объектов Azure. 

## <a name="monitor-hello-pipeline"></a>Монитор hello конвейера
На этом шаге используется Azure PowerShell toomonitor происходящем в фабрикой данных Azure.

1. Замените &lt;с именем DataFactoryName&gt; с именем hello фабрику данных и выполнения **Get AzureRmDataFactory**и назначить переменной $df tooa hello выходных данных.

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    Например:
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    Затем выполните содержимое Здравствуй, мир hello toosee $df следующие выходные данные: 
    
    ```
    PS C:\ADFGetStartedPSH> $df
    
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DataFactoryId     : 6f194b34-03b3-49ab-8f03-9f8a7b9d3e30
    ResourceGroupName : ADFTutorialResourceGroup
    Location          : West US
    Tags              : {}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DataFactoryProperties
    ProvisioningState : Succeeded
    ```
2. Запустите **Get AzureRmDataFactorySlice** tooget сведения о всех фрагментов hello **OutputDataset**, являющееся hello выходной набор данных конвейера hello.  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   Это значение должно соответствовать hello **запустить** значение hello конвейера JSON. Вы увидите 24 срезов, один для каждого часа с 00: 00 для too12 текущий день hello AM из hello следующего дня.

   Ниже приведены три фрагмента образец hello в выходных данных. 

    ``` 
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 11:00:00 PM
    End               : 5/12/2017 12:00:00 AM
    RetryCount        : 0
    State             : Ready
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 9:00:00 PM
    End               : 5/11/2017 10:00:00 PM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0   

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 8:00:00 PM
    End               : 5/11/2017 9:00:00 PM
    RetryCount        : 0
    State             : Waiting
    SubState          : ConcurrencyLimit
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. Запустите **Get AzureRmDataFactoryRun** tooget сведения hello действия выполняется для **конкретных** среза. Скопируйте значение даты времени hello из выходных данных hello hello предыдущей команды toospecify hello значения для параметра StartDateTime hello. 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   Вот пример выходных данных hello. 

    ```
    Id                  : c0ddbd75-d0c7-4816-a775-704bbd7c7eab_636301332000000000_636301368000000000_OutputDataset
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : ADFTutorialDataFactoryPSH0516
    DatasetName         : OutputDataset
    ProcessingStartTime : 5/16/2017 8:00:33 PM
    ProcessingEndTime   : 5/16/2017 8:01:36 PM
    PercentComplete     : 100
    DataSliceStart      : 5/11/2017 9:00:00 PM
    DataSliceEnd        : 5/11/2017 10:00:00 PM
    Status              : Succeeded
    Timestamp           : 5/16/2017 8:00:33 PM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : CopyFromBlobToSQL
    PipelineName        : ADFTutorialPipeline
    Type                : Copy  
    ```

Полную документацию по командлетам фабрики данных см. в [этом справочнике](/powershell/module/azurerm.datafactories).

## <a name="summary"></a>Сводка
В этом учебнике вы создали данных toocopy фабрики данных Azure из базы данных Azure SQL tooan BLOB-объектов Azure. Вы использовали фабрики данных hello toocreate PowerShell, связанные службы, наборы данных и конвейера. Ниже приведены hello высокоуровневые действия, выполняемые в этом учебнике.  

1. Создание **фабрики данных Azure**.
2. Создание **связанных служб**.

   а. **Хранилища Azure** связанные службы toolink вашей учетной записи хранилища Azure, который содержит входные данные.     
   b. **Azure SQL** связанные toolink службы базы данных SQL, содержащий hello выходных данных.
3. Создание **наборов данных** , которые описывают входные и выходные данные для конвейеров.
4. Создан **конвейера** с **действие копирования**, с **BlobSource** как источник hello и **SqlSink** как приемник hello.

## <a name="next-steps"></a>Дальнейшие действия
В этом руководстве в ходе операции копирования вы использовали хранилище BLOB-объектов Azure как исходное хранилище данных, а базу данных SQL Azure — как целевое хранилище данных. Hello следующей таблице приведен список хранилищ данных, поддерживаемые действием копирования hello как источники и назначения: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn о том, как хранилище данных toocopy из данных, щелкните ссылку hello hello хранилища данных в таблице hello. 

