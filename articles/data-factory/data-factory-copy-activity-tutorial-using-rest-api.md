---
title: "Учебник: Использование API-интерфейса REST toocreate конвейера фабрики данных Azure | Документы Microsoft"
description: "В этом учебнике используется API-интерфейса REST toocreate конвейера фабрики данных Azure с toocopy действие копирования данных из хранилища Azure BLOB-объектов из базы данных Azure SQL."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1704cdf8-30ad-49bc-a71c-4057e26e7350
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: aa6c9b035101c4ff9acff90117ca6e3e7067f418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-rest-api-toocreate-an-azure-data-factory-pipeline-toocopy-data"></a>Учебник: Использование API-интерфейса REST toocreate данных toocopy конвейера фабрики данных Azure 
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

В этой статье вы узнаете, как toouse REST API toocreate фабрики данных с конвейером, который копирует данные из базы данных Azure SQL tooan хранилища BLOB-объектов Azure. Если новый tooAzure фабрики данных, прочтите hello [tooAzure введение фабрики данных](data-factory-introduction.md) статьи, прежде чем выполнять задания этого учебника.   

В этом руководстве описывается создание конвейера с одним действием — действием копирования. Действие копирования Hello копирует данные из поддерживаемых хранилища tooa поддерживаемых приемник данных хранилищ данных. Список хранилищ данных, которые поддерживаются в качестве источников и приемников, см. в разделе [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Действие Hello выключен глобально доступной можно копировать данные между различными хранилищами данных в виде безопасные, надежные и масштабируемые службы. Дополнительные сведения о действии копирования hello см. в разделе [действия перемещения данных](data-factory-data-movement-activities.md).

Конвейер может содержать сразу несколько действий. Кроме того, можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия. Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

> [!NOTE]
> Данная статья не охватывает все hello REST API фабрики данных. Полную документацию по командлетам фабрики данных см. в [справочнике по REST API фабрики данных](/rest/api/datafactory/).
>  
> конвейер данных Hello в этом учебнике копирует данные из источника данных хранилища tooa целевое хранилище данных. Учебник о том, как tootransform данных, с помощью фабрики данных Azure, в разделе [учебника: построение конвейера анализа tootransform использование кластера Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Предварительные требования
* Выполните [Обзор учебника](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) и завершения hello **необходимого компонента** действия.
* Установите на компьютер программу [curl](https://curl.haxx.se/dlwiz/) . Используйте средство перелистывание hello с toocreate команды REST фабрики данных. 
* Следуя инструкциям в [этой статье](../azure-resource-manager/resource-group-create-service-principal-portal.md) , выполните следующее: 
  1. Создайте веб-приложение с именем **ADFCopyTutorialApp** в Azure Active Directory.
  2. Получите **идентификатор клиента** и **секретный ключ**. 
  3. Получите значение для **tenant_id**. 
  4. Назначить hello **ADFCopyTutorialApp** toohello приложения **участника фабрики данных** роли.  
* Установите [Azure PowerShell](/powershell/azure/overview).  
* Запустите **PowerShell** и hello следующие действия. Не закрывайте Azure PowerShell до завершения этого учебника hello. Если закрыть и снова открыть понадобятся toorun hello команд.
  
  1. Запустите следующую команду hello и введите hello имя пользователя и пароль, использовать toosign в toohello портала Azure:
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. Выполните следующие команды tooview hello все hello подписки для этой учетной записи:

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. Следующая команда tooselect hello подписки на toowork с выполнения hello. Замените  **&lt;NameOfAzureSubscription** &gt; с именем hello подписки Azure. 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. Создание группы ресурсов Azure с именем **ADFTutorialResourceGroup** , выполнив следующую команду в hello PowerShell hello:  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      Если группа ресурсов hello уже существует, укажите ли tooupdate его (Y) или сохранить его как (N). 
     
      Некоторые шаги hello в этом учебнике предполагается использовать ADFTutorialResourceGroup с именем группы ресурсов hello. Если вы используете другой группе ресурсов, в этом учебнике требуется имя hello toouse вместо ADFTutorialResourceGroup группы ресурсов.

## <a name="create-json-definitions"></a>Создание определений JSON
Создайте следующие файлы JSON в папке hello, где находится curl.exe. 

### <a name="datafactoryjson"></a>datafactory.json
> [!IMPORTANT]
> Имя должно быть глобально уникальным, поэтому можно toomake ADFCopyTutorialDF tooprefix или суффикса его уникальное имя. 
> 
> 

```JSON
{  
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a>azurestoragelinkedservice.json
> [!IMPORTANT]
> Замените значения **accountname** и **accountkey** на имя вашей учетной записи хранения Azure и ее ключ. toolearn tooget хранилищем доступом ключа, см. в разделе [ключи доступа Просмотр, копирование и повторное создание хранилища](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).

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

Дополнительные сведения о свойствах JSON см. в разделе [Связанная служба хранилища Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service).

### <a name="azuersqllinkedservicejson"></a>azuersqllinkedservice.json
> [!IMPORTANT]
> Замените **servername**, **databasename**, **username**, и **пароль** с именем сервера Azure SQL, имя базы данных SQL, пользователь Учетная запись и пароль для учетной записи hello.  
> 
>

```JSON
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

Дополнительные сведения о свойствах JSON см. в разделе [Свойства связанной службы](data-factory-azure-sql-connector.md#linked-service-properties).

### <a name="inputdatasetjson"></a>inputdataset.json

```JSON
{
  "name": "AzureBlobInput",
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

### <a name="outputdatasetjson"></a>outputdataset.json

```JSON
{
  "name": "AzureSqlOutput",
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

### <a name="pipelinejson"></a>pipeline.json

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data tooAzure SQL database",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
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
- Входных данных для действия hello установлено слишком**AzureBlobInput** и вывода для hello действия установлено слишком**AzureSqlOutput**. 
- В hello **typeProperties** разделе **BlobSource** указан в качестве типа источника hello и **SqlSink** указан как тип приемника hello. Перечень хранилищ данных, поддерживаемые действием копирования hello как источники и приемники см. в разделе [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats). как сохранить toouse конкретных поддерживаемые данные в качестве источника и приемника, toolearn по ссылке hello в таблице hello.  
 
Замените значение hello hello **запустить** свойство с hello текущего дня и **окончания** значение с hello следующего дня. Можно указать только часть даты hello и пропустить hello время hello Дата и время. Например, «2017 г. 02-03-», который является эквивалентом "2017 г-02-03T00:00:00Z»
 
Даты начала и окончания должны быть в [формате ISO](http://en.wikipedia.org/wiki/ISO_8601). Например, 2016-10-14T16:32:41Z. Hello **окончания** времени является необязательным, но мы используем в этом учебнике. 
 
Если не указать значение для hello **окончания** свойство, оно вычисляется как «**start + 48 часов**». конвейер hello toorun неопределенно долгое время, укажите **9999-09-09** как значение hello для hello **окончания** свойство.
 
В предыдущих пример hello существует 24 срезы данных, как каждый срез данных создается каждый час.

Описание свойств JSON в определении конвейера см. в статье [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md). Описание свойств JSON в определении действия копирования см. в статье [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md). Описание свойств JSON, поддерживаемых BlobSource, см. в статье о [соединителе больших двоичных объектов Azure](data-factory-azure-blob-connector.md). Описание свойств JSON, поддерживаемых SqlSink, см. в статье о [соединителе базы данных SQL Azure](data-factory-azure-sql-connector.md).

## <a name="set-global-variables"></a>Настройка глобальных переменных
Выполните следующие команды после замены значения hello собственные hello в Azure PowerShell.

> [!IMPORTANT]
> Инструкции по получению значений для параметров client_id, client_secret, tenant и subscription_id см. в разделе [Предварительные требования](#prerequisites).   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

Выполните следующую команду, после обновления hello имя фабрики данных hello, которую вы используете hello. 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a>Проверка подлинности с помощью AAD
Выполнения hello следующая команда tooauthenticate с Azure Active Directory (AAD): 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a>Создание фабрики данных
На этом шаге создается фабрика данных Azure с именем **ADFCopyTutorialDF**. Фабрика данных может иметь один или несколько конвейеров. Конвейер может содержать одно или несколько действий. Например хранилища данных toocopy действие копирования данных из источников tooa назначения. Toorun действие Hive в HDInsight tootransform скрипт Hive входных данных tooproduct выходных данных. Выполните следующие hello данных команды toocreate фабрики hello. 

1. Назначить hello команды toovariable с именем **cmd**. 
   
    > [!IMPORTANT]
    > Убедитесь, что hello имя фабрики данных hello, указанные здесь имя, указанное в hello hello совпадений (ADFCopyTutorialDF) **datafactory.json**. 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. Команда hello с помощью **Invoke-Command**.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Просмотр результатов hello. Если hello фабрика данных успешно создана, вы видите hello JSON для фабрики данных hello в hello **результатов**; в противном случае отображается сообщение об ошибке.  
   
    ```
    Write-Host $results
    ```

Обратите внимание hello после точки.

* Имя Hello hello фабрики данных Azure должно быть глобально уникальным. При возникновении ошибки hello в результатах: **имя фабрики данных «ADFCopyTutorialDF» недоступен**, hello следующие действия:  
  
  1. Изменение имени hello (например, yournameADFCopyTutorialDF) в hello **datafactory.json** файла.
  2. В первой команде hello Здравствуйте, где **$cmd** переменной присваивается значение, замените ADFCopyTutorialDF hello новое имя и выполните команду hello. 
  3. Запуск hello следующие две команды tooinvoke hello API-интерфейса REST toocreate hello данных фабрики и печати hello результатов операции hello. 
     
     Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.
* экземпляры toocreate фабрики данных, необходимо toobe участника или администратор hello подписки Azure
* Имя фабрики данных hello Hello может зарегистрирован как DNS-имя в будущем hello и поэтому становятся публично видимых.
* Если ошибка hello: «**этой подписки не является пространством имен зарегистрированных toouse Microsoft.DataFactory**», выполните одно из следующих hello и повторите попытку публикации: 
  
  * В Azure PowerShell выполните hello, следующая команда tooregister hello фабрики данных поставщика. 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    Следующая команда tooconfirm hello можно запустить, hello зарегистрирован поставщик фабрики данных. 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Имя входа с помощью hello подписки Azure в hello [портал Azure](https://portal.azure.com) и перейдите в колонку tooa фабрики данных (или) создать фабрику данных в hello портал Azure. Это действие автоматически регистрирует поставщик hello.

Перед созданием конвейера, необходимо toocreate несколько сущностей фабрики данных сначала. Сначала создать связанные службы toolink источника и назначения данных сохраняет данные tooyour хранения. Затем определите данных toorepresent наборы входных и выходных данных в хранилищах связанных данных. Наконец создайте hello конвейера с действие, которое использует эти наборы данных.

## <a name="create-linked-services"></a>Создание связанных служб
Создания связанных служб в toolink фабрики данных, хранит и вычислений фабрики данных toohello службы данных. В этом руководстве не используются службы вычислений, например Azure HDInsight или Azure Data Lake Analytics. Вы используете два хранилища данных — служба хранилища Azure (источник) и база данных SQL Azure (конечное хранилище). Поэтому нужно создать две связанные службы: служба хранилища Azure с именем AzureStorageLinkedService и база данных SQL Azure с именем AzureSqlLinkedService.  

Hello AzureStorageLinkedService связывает фабрику данных toohello учетной записи хранилища Azure. Эта учетная запись хранения является hello один в котором можно создать контейнер и загруженные данные hello в рамках [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

AzureSqlLinkedService связывает фабрику данных toohello базы данных Azure SQL. Hello данные, копируемые из хранилища больших двоичных объектов hello хранится в этой базе данных. Создана таблица emp hello в этой базе данных как часть [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).  

### <a name="create-azure-storage-linked-service"></a>Создание связанной службы хранения Azure
На этом шаге связать фабрики данных tooyour учетной записи хранилища Azure. Укажите имя hello и ключ учетной записи хранилища Azure в этом разделе. В разделе [связанная служба хранилища Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) подробные сведения о JSON свойства, используемые toodefine связанная служба хранилища Azure.  

1. Назначить hello команды toovariable с именем **cmd**. 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. Команда hello с помощью **Invoke-Command**.

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Просмотр результатов hello. Если hello связаны была успешно создана служба см. в разделе hello JSON для службы hello связаны в hello **результатов**; в противном случае отображается сообщение об ошибке.

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a>Создание связанной службы SQL Azure
На этом шаге связать фабрики данных tooyour базы данных Azure SQL. Укажите имя сервера Azure SQL hello, имя базы данных, имя пользователя и пароль пользователя в этом разделе. В разделе [связанная служба Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties) подробные сведения о JSON свойства, используемые toodefine связанная служба SQL Azure.

1. Назначить hello команды toovariable с именем **cmd**. 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. Команда hello с помощью **Invoke-Command**.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Просмотр результатов hello. Если hello связаны была успешно создана служба см. в разделе hello JSON для службы hello связаны в hello **результатов**; в противном случае отображается сообщение об ошибке.
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a>Создание наборов данных
В предыдущем шаге hello создать связанные службы toolink вашей учетной записи хранилища Azure и фабрику данных tooyour базы данных Azure SQL. На этом шаге можно определить два набора данных с именем AzureBlobInput и AzureSqlOutput, представляющие входные данные и выходные данные, которые хранятся в хранилищах данных hello, на которые ссылается AzureStorageLinkedService и AzureSqlLinkedService соответственно.

Hello связанной службой хранилища Azure задает строку подключения hello, который использует служба фабрики данных во время выполнения tooconnect tooyour учетной записи хранилища Azure. И hello входного BLOB-объекта dataset (AzureBlobInput) указывает контейнер hello и hello папку, содержащую hello входных данных.  

Аналогичным образом hello связана база данных SQL Azure службы указывает hello строку подключения, использующее служба фабрики данных в базе данных Azure SQL tooyour tooconnect время выполнения. И hello выходной набор данных таблицы SQL (OututDataset) указывает таблицу hello в hello базы данных toowhich hello и копирования данных из хранилища больших двоичных объектов hello. 

### <a name="create-input-dataset"></a>Создание входного набора данных
На этом шаге создается набор данных с именем AzureBlobInput, который указывает файл tooa больших двоичных объектов (emp.txt) в корневой папке hello контейнер больших двоичных объектов (adftutorial) в hello представленный hello AzureStorageLinkedService связанной службы хранилища Azure. Если не указать значение для имени файла hello (или пропустить его), данные из всех больших двоичных объектов в папке входной hello, скопированный toohello назначения. В этом учебнике укажите значение для имени файла hello. 

1. Назначить hello команды toovariable с именем **cmd**. 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. Команда hello с помощью **Invoke-Command**.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Просмотр результатов hello. Если набор данных hello успешно создана, вы видите hello JSON для набора данных hello в hello **результатов**; в противном случае отображается сообщение об ошибке.
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a>Создание выходного набора данных
Hello базы данных SQL Azure связанные службы задает hello строку подключения, использующее служба фабрики данных в базе данных Azure SQL tooyour tooconnect время выполнения. Hello выходного SQL таблицы набора данных (OututDataset) на этом шаге создается указывает, что таблица hello в данных hello toowhich hello базы данных из хранилища больших двоичных объектов hello копируется.

1. Назначить hello команды toovariable с именем **cmd**.

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. Команда hello с помощью **Invoke-Command**.
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Просмотр результатов hello. Если набор данных hello успешно создана, вы видите hello JSON для набора данных hello в hello **результатов**; в противном случае отображается сообщение об ошибке.
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a>Создание конвейера
На этом шаге создается конвейер с **действием копирования**, которое использует **AzureBlobInput** в качестве входных данных и **AzureSqlOutput** в качестве выходных.

В настоящее время выходной набор данных — того, какие диски hello расписания. В этом учебнике выходной набор данных является настроенным tooproduce срез один раз в час. конвейер Hello содержит время начала и время окончания, которые однажды друг от друга, что составляет 24 часа. Таким образом 24 фрагменты выходной набор данных создают hello конвейера. 

1. Назначить hello команды toovariable с именем **cmd**.

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. Команда hello с помощью **Invoke-Command**.

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Просмотр результатов hello. Если набор данных hello успешно создана, вы видите hello JSON для набора данных hello в hello **результатов**; в противном случае отображается сообщение об ошибке.  

    ```PowerShell   
    Write-Host $results
    ```

**Поздравляем!** Успешно создана фабрикой данных Azure с конвейером, который копирует данные из базы данных SQL tooAzure хранилища больших двоичных объектов.

## <a name="monitor-pipeline"></a>Отслеживание конвейера
На этом шаге используется фрагменты toomonitor REST API фабрики данных, получаемых hello конвейера.

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> Убедитесь, что hello начального и конечного времени указано в hello следующая команда hello начало сопоставления времени и завершения hello конвейера. 

```PowerShell
$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=2017-05-11T00%3a00%3a00.0000000Z"&"end=2017-05-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};
```

```PowerShell
$results2 = Invoke-Command -scriptblock $cmd;
```

```PowerShell
IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

Запустить hello Invoke-Command и hello следующему пока не увидите срез в **готов** состояние или **сбой** состояния. Когда hello среза находится в состоянии готовности, проверьте hello **emp** таблицы в базе данных Azure SQL для hello выходных данных. 

Для каждого среза двух строк данных из исходного файла hello, скопированный toohello emp таблицы в базе данных Azure SQL hello. Таким образом 24 новых записей в таблице emp hello появляется, если все срезы hello успешно обрабатываются (в состоянии готовности). 

## <a name="summary"></a>Сводка
В этом учебнике используется API-интерфейса REST toocreate данных toocopy фабрики данных Azure, из базы данных Azure SQL tooan BLOB-объектов Azure. Ниже приведены hello высокоуровневые действия, выполняемые в этом учебнике.  

1. Создание **фабрики данных Azure**.
2. Создание **связанных служб**.
   1. Хранилище Azure связан toolink службы учетной записи хранилища Azure, содержащий входные данные.     
   2. Azure SQL связанные службы toolink базы данных Azure SQL, которое содержит hello выходных данных. 
3. Создание **наборов данных**, описывающих входные и выходные данные для конвейеров.
4. Создание **конвейера** с BlobSource в качестве источника и SqlSink в качестве приемника с помощью действия копирования. 

## <a name="next-steps"></a>Дальнейшие действия
В этом руководстве в ходе операции копирования вы использовали хранилище BLOB-объектов Azure как исходное хранилище данных, а базу данных SQL Azure — как целевое хранилище данных. Hello следующей таблице приведен список хранилищ данных, поддерживаемые действием копирования hello как источники и назначения: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn о том, как хранилище данных toocopy из данных, щелкните ссылку hello hello хранилища данных в таблице hello.
