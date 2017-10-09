---
title: "Руководство. Создание конвейера с действием копирования с помощью API .NET | Документация Майкрософт"
description: "В этом руководстве описано, как с помощью API .NET создать конвейер фабрики данных Azure с действием копирования."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 58fc4007-b46d-4c8e-a279-cb9e479b3e2b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 52f72da54cdd80691e09d7453bf6730454c4089e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a>Руководство. Создание конвейера с действием копирования с помощью API .NET
> [!div class="op_single_selector"]
> * [Обзор и предварительные требования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Мастер копирования](data-factory-copy-data-wizard-tutorial.md)
> * [Портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Шаблон Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [ИНТЕРФЕЙС REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)

В этой статье вы узнаете, как toouse [.NET API](https://portal.azure.com) toocreate фабрики данных с конвейером, который копирует данные из базы данных Azure SQL tooan хранилища BLOB-объектов Azure. Если новый tooAzure фабрики данных, прочтите hello [tooAzure введение фабрики данных](data-factory-introduction.md) статьи, прежде чем выполнять задания этого учебника.   

В этом руководстве описывается создание конвейера с одним действием — действием копирования. Действие копирования Hello копирует данные из поддерживаемых хранилища tooa поддерживаемых приемник данных хранилищ данных. Список хранилищ данных, которые поддерживаются в качестве источников и приемников, см. в разделе [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Действие Hello выключен глобально доступной можно копировать данные между различными хранилищами данных в виде безопасные, надежные и масштабируемые службы. Дополнительные сведения о действии копирования hello см. в разделе [действия перемещения данных](data-factory-data-movement-activities.md).

Конвейер может содержать сразу несколько действий. Кроме того, можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия. Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

> [!NOTE] 
> Полную документацию по .NET API для Data Factory см. в [Справочник по .NET API фабрики данных](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).
> 
> конвейер данных Hello в этом учебнике копирует данные из источника данных хранилища tooa целевое хранилище данных. Учебник о том, как tootransform данных, с помощью фабрики данных Azure, в разделе [учебника: построение конвейера анализа tootransform использование кластера Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Предварительные требования
* Выполните [учебника Обзор и необходимые](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget Обзор учебника hello и завершения hello **необходимого компонента** действия.
* Visual Studio 2012, 2013 или 2015
* Скачайте и установите пакет [Azure .NET SDK](http://azure.microsoft.com/downloads/)
* Azure PowerShell. Следуйте инструкциям в разделе [как tooinstall и настройка Azure PowerShell](../powershell-install-configure.md) статью tooinstall Azure PowerShell на компьютере. Можно использовать Azure PowerShell toocreate приложение Azure Active Directory.

### <a name="create-an-application-in-azure-active-directory"></a>Создание приложения в Azure Active Directory
Создать приложение Azure Active Directory, создать участника-службы для приложения hello и назначьте его toohello **участника фабрики данных** роли.

1. Запустите **PowerShell**.
2. Запустите следующую команду hello и введите hello имя пользователя и пароль, использовать toosign в toohello портал Azure.

    ```PowerShell
    Login-AzureRmAccount
    ```
3. Запустите следующие команды tooview hello все hello подписки для этой учетной записи.

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. Следующая команда tooselect hello подписки на toowork с выполнения hello. Замените  **&lt;NameOfAzureSubscription** &gt; с именем hello подписки Azure.

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > Запишите **SubscriptionId** и **TenantId** hello в выходных данных этой команды.

5. Создание группы ресурсов Azure с именем **ADFTutorialResourceGroup** , выполнив следующую команду в hello PowerShell hello.

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    Если группа ресурсов hello уже существует, укажите ли tooupdate его (Y) или сохранить его как (N).

    Если вы используете другой группе ресурсов, в этом учебнике требуется имя hello toouse вместо ADFTutorialResourceGroup группы ресурсов.
6. Создайте приложение Azure Active Directory.

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
    ```

    Если появляется следующая ошибка hello, укажите другой URL-адрес и снова выполните команду hello.
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. Создайте участника-службы AD hello.

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. Добавление участника toohello службы **участника фабрики данных** роли.

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. Получить идентификатор приложения hello.

    ```PowerShell
    $azureAdApplication 
    ```
    Запишите идентификатор приложения hello (applicationID) hello в выходных данных.

Вы должны получить следующие четыре значения:

* Tenant ID
* Идентификатор подписки
* Идентификатор приложения
* Пароль (в первой команде hello)

## <a name="walkthrough"></a>Пошаговое руководство
1. С помощью Visual Studio 2012, 2013 или 2015 создайте консольное приложение C# .NET.
   1. Запустите **Visual Studio** 2012, 2013 или 2015.
   2. Нажмите кнопку **файл**, слишком точки**New**и нажмите кнопку **проекта**.
   3. Разверните раздел **Шаблоны** и выберите **Visual C#**. В этом пошаговом руководстве используется C#, но можно использовать любой язык .NET.
   4. Выберите **консольное приложение** hello списке типов проекта на hello вправо.
   5. Введите **DataFactoryAPITestApp** для hello имя.
   6. Выберите **C:\ADFGetStarted** для hello расположение.
   7. Нажмите кнопку **ОК** toocreate hello проекта.
2. Нажмите кнопку **средства**, слишком точки**диспетчера пакетов NuGet**и нажмите кнопку **консоль диспетчера пакетов**.
3. В hello **консоль диспетчера пакетов**, hello следующие действия:
   1. Выполните hello, следующая команда tooinstall фабрики данных пакета.`Install-Package Microsoft.Azure.Management.DataFactories`
   2. Выполните hello, следующая команда tooinstall Azure Active Directory пакет (использовать Active Directory API в коде hello).`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`
4. Добавьте следующее hello **appSetttings** toohello раздел **App.config** файла. Эти параметры используются hello вспомогательный метод: **GetAuthorizationHeader**.

    Замените значения **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;** и **&lt;tenant ID&gt;** собственными значениями.

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating hello AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```

5. Добавьте следующее hello **с помощью** toohello инструкций исходный файл (Program.cs) в проекте hello.

    ```csharp
    using System.Configuration;
    using System.Collections.ObjectModel;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure;
    using Microsoft.Azure.Management.DataFactories;
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Common.Models;

    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    ```

6. Добавьте следующий код, который создает экземпляр hello **DataPipelineManagementClient** toohello класса **Main** метод. Этот объект toocreate используется фабрики данных, связанной службы, входные и выходные наборы данных и конвейера. Вы также использовать срезы toomonitor этот объект набора данных во время выполнения.

    ```csharp
    // create data factory management client
    string resourceGroupName = "ADFTutorialResourceGroup";
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > Замените значение hello **resourceGroupName** с именем hello группы ресурсов Azure.
   >
   > Обновите hello данных фабрики (с именем dataFactoryName) toobe уникальное имя. Имя фабрики данных hello должно быть глобально уникальным. Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.

7. Добавьте следующий код, создающий hello **фабрики данных** toohello **Main** метод.

    ```csharp
    // create a data factory
    Console.WriteLine("Creating a data factory");
    client.DataFactories.CreateOrUpdate(resourceGroupName,
        new DataFactoryCreateOrUpdateParameters()
        {
            DataFactory = new DataFactory()
            {
                Name = dataFactoryName,
                Location = "westus",
                Properties = new DataFactoryProperties()
            }
        }
    );
    ```

    Фабрика данных может иметь один или несколько конвейеров. Конвейер может содержать одно или несколько действий. Например toocopy действие копирования данных из целевое хранилище данных источника tooa и toorun действие Hive в HDInsight tootransform скрипт Hive входных данных tooproduct выходных данных. Давайте начнем с создания фабрики данных hello на этом шаге.
8. Добавьте следующий код, создающий hello **связанная служба хранилища Azure** toohello **Main** метод.

   > [!IMPORTANT]
   > Замените значения **storageaccountname** и **accountkey** именем и ключом вашей учетной записи хранения Azure.

    ```csharp
    // create a linked service for input data store: Azure Storage
    Console.WriteLine("Creating Azure Storage linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureStorageLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<accountkey>")
                )
            }
        }
    );
    ```

    Создания связанных служб в toolink фабрики данных, хранит и вычислений фабрики данных toohello службы данных. В этом руководстве не используются службы вычислений, например Azure HDInsight или Azure Data Lake Analytics. Вы используете два хранилища данных — служба хранилища Azure (источник) и база данных SQL Azure (конечное хранилище). 

    Поэтому нужно создать две связанные службы: служба хранилища Azure с именем AzureStorageLinkedService и база данных SQL Azure с именем AzureSqlLinkedService.  

    Hello AzureStorageLinkedService связывает фабрику данных toohello учетной записи хранилища Azure. Эта учетная запись хранения является hello один в котором можно создать контейнер и загруженные данные hello в рамках [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
9. Добавьте следующий код, создающий hello **связанная служба Azure SQL** toohello **Main** метод.

   > [!IMPORTANT]
   > Укажите вместо **servername**, **databasename**, **username** и **password** имя своего сервера Azure SQL Server, имя базы данных, имя пользователя и пароль.

    ```csharp
    // create a linked service for output data store: Azure SQL Database
    Console.WriteLine("Creating Azure SQL Database linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureSqlLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureSqlDatabaseLinkedService("Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30")
                )
            }
        }
    );
    ```

    AzureSqlLinkedService связывает фабрику данных toohello базы данных Azure SQL. Hello данные, копируемые из хранилища больших двоичных объектов hello хранится в этой базе данных. Создана таблица emp hello в этой базе данных как часть [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
10. Добавьте следующий код, создающий hello **наборы входных и выходных данных** toohello **Main** метод.

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "InputDataset";
    string Dataset_Destination = "OutputDataset";

    Console.WriteLine("Creating input dataset of type: Azure Blob");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                Structure = new List<DataElement>()
                {
                    new DataElement() { Name = "FirstName", Type = "String" },
                    new DataElement() { Name = "LastName", Type = "String" }
                },
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/",
                    FileName = "emp.txt"
                },
                External = true,
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },

                Policy = new Policy()
                {
                    Validation = new ValidationPolicy()
                    {
                        MinimumRows = 1
                    }
                }
            }
        }
    });

    Console.WriteLine("Creating output dataset of type: Azure SQL");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new DatasetCreateOrUpdateParameters()
        {
            Dataset = new Dataset()
            {
                Name = Dataset_Destination,
                Properties = new DatasetProperties()
                {
                    Structure = new List<DataElement>()
                    {
                        new DataElement() { Name = "FirstName", Type = "String" },
                        new DataElement() { Name = "LastName", Type = "String" }
                    },
                    LinkedServiceName = "AzureSqlLinkedService",
                    TypeProperties = new AzureSqlTableDataset()
                    {
                        TableName = "emp"
                    },
                    Availability = new Availability()
                    {
                        Frequency = SchedulePeriod.Hour,
                        Interval = 1,
                    },
                }
            }
        });
    ```
    
    В предыдущем шаге hello создать связанные службы toolink вашей учетной записи хранилища Azure и фабрику данных tooyour базы данных Azure SQL. На этом шаге можно определить два набора данных с именем InputDataset и OutputDataset, представляющие входные данные и выходные данные, которые хранятся в хранилищах данных hello, на которые ссылается AzureStorageLinkedService и AzureSqlLinkedService соответственно.

    Hello связанной службой хранилища Azure задает строку подключения hello, который использует служба фабрики данных во время выполнения tooconnect tooyour учетной записи хранилища Azure. И hello входного BLOB-объекта dataset (InputDataset) указывает контейнер hello и hello папку, содержащую hello входных данных.  

    Аналогичным образом hello связана база данных SQL Azure службы указывает hello строку подключения, использующее служба фабрики данных в базе данных Azure SQL tooyour tooconnect время выполнения. И hello выходной набор данных таблицы SQL (OututDataset) указывает таблицу hello в hello базы данных toowhich hello и копирования данных из хранилища больших двоичных объектов hello.

    На этом шаге создается набор данных с именем InputDataset, который указывает файл tooa больших двоичных объектов (emp.txt) в корневой папке hello контейнер больших двоичных объектов (adftutorial) в hello представленный hello AzureStorageLinkedService связанной службы хранилища Azure. Если не указать значение для имени файла hello (или пропустить его), данные из всех больших двоичных объектов в папке входной hello, скопированный toohello назначения. В этом учебнике укажите значение для имени файла hello.    

    На этом этапе мы создадим выходной набор данных с именем **OutputDataset**. Этот набор данных указывает tooa SQL таблицы в базе данных Azure SQL hello, представленного **AzureSqlLinkedService**.
11. Добавьте hello следующий код, чтобы **создает и активирует конвейера** toohello **Main** метод. На этом этапе вы создадите конвейер с **действием копирования**, которое использует **InputDataset** в качестве входных данных и **OutputDataset** в качестве выходных.

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2017, 5, 11, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = new DateTime(2017, 5, 12, 0, 0, 0, 0, DateTimeKind.Utc);
    string PipelineName = "ADFTutorialPipeline";

    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new PipelineCreateOrUpdateParameters()
        {
            Pipeline = new Pipeline()
            {
                Name = PipelineName,
                Properties = new PipelineProperties()
                {
                    Description = "Demo Pipeline for data transfer between blobs",

                    // Initial value for pipeline's active period. With this, you won't need tooset slice status
                    Start = PipelineActivePeriodStartTime,
                    End = PipelineActivePeriodEndTime,

                    Activities = new List<Activity>()
                    {
                        new Activity()
                        {
                            Name = "BlobToAzureSql",
                            Inputs = new List<ActivityInput>()
                            {
                                new ActivityInput() {
                                    Name = Dataset_Source
                                }
                            },
                            Outputs = new List<ActivityOutput>()
                            {
                                new ActivityOutput()
                                {
                                    Name = Dataset_Destination
                                }
                            },
                            TypeProperties = new CopyActivity()
                            {
                                Source = new BlobSource(),
                                Sink = new BlobSink()
                                {
                                    WriteBatchSize = 10000,
                                    WriteBatchTimeout = TimeSpan.FromMinutes(10)
                                }
                            }
                        }
                    }
                }
            }
        });
    ```

    Обратите внимание hello после точки.
   
    - В разделе "действия" hello, имеется только одно действие, **тип** задано слишком**копирования**. Дополнительные сведения о действии копирования hello см. в разделе [действия перемещения данных](data-factory-data-movement-activities.md). В решениях фабрики данных можно также использовать [действия преобразования данных](data-factory-data-transformation-activities.md).
    - Входных данных для действия hello установлено слишком**InputDataset** и вывода для hello действия установлено слишком**OutputDataset**. 
    - В hello **typeProperties** разделе **BlobSource** указан в качестве типа источника hello и **SqlSink** указан как тип приемника hello. Перечень хранилищ данных, поддерживаемые действием копирования hello как источники и приемники см. в разделе [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats). как сохранить toouse конкретных поддерживаемые данные в качестве источника и приемника, toolearn по ссылке hello в таблице hello.  
   
    В настоящее время выходной набор данных — того, какие диски hello расписания. В этом учебнике выходной набор данных является настроенным tooproduce срез один раз в час. конвейер Hello содержит время начала и время окончания, которые однажды друг от друга, что составляет 24 часа. Таким образом 24 фрагменты выходной набор данных создают hello конвейера.
12. Добавьте следующий код toohello hello **Main** метод tooget hello состояние срез данных hello выходной набор данных. Существует только срез, ожидаемый в этом образце.

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;

    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling hello slice status");        
        // wait before hello next status check
        Thread.Sleep(1000 * 12);

        var datalistResponse = client.DataSlices.List(resourceGroupName, dataFactoryName, Dataset_Destination,
            new DataSliceListParameters()
            {
                DataSliceRangeStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString(),
                DataSliceRangeEndTime = PipelineActivePeriodEndTime.ConvertToISO8601DateTimeString()
            });

        foreach (DataSlice slice in datalistResponse.DataSlices)
        {
            if (slice.State == DataSliceState.Failed || slice.State == DataSliceState.Ready)
            {
                Console.WriteLine("Slice execution is done with status: {0}", slice.State);
                done = true;
                break;
            }
            else
            {
                Console.WriteLine("Slice status is: {0}", slice.State);
            }
        }
    }
    ```

13. Добавьте приведенные ниже сведения tooget запустите код для фрагмента данных toohello hello **Main** метод.

    ```csharp
    Console.WriteLine("Getting run details of a data slice");

    // give it a few minutes for hello output slice toobe ready
    Console.WriteLine("\nGive it a few minutes for hello output slice toobe ready and press any key.");
    Console.ReadKey();

    var datasliceRunListResponse = client.DataSliceRuns.List(
            resourceGroupName,
            dataFactoryName,
            Dataset_Destination,
            new DataSliceRunListParameters()
            {
                DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
            }
        );

    foreach (DataSliceRun run in datasliceRunListResponse.DataSliceRuns)
    {
        Console.WriteLine("Status: \t\t{0}", run.Status);
        Console.WriteLine("DataSliceStart: \t{0}", run.DataSliceStart);
        Console.WriteLine("DataSliceEnd: \t\t{0}", run.DataSliceEnd);
        Console.WriteLine("ActivityId: \t\t{0}", run.ActivityName);
        Console.WriteLine("ProcessingStartTime: \t{0}", run.ProcessingStartTime);
        Console.WriteLine("ProcessingEndTime: \t{0}", run.ProcessingEndTime);
        Console.WriteLine("ErrorMessage: \t{0}", run.ErrorMessage);
    }

    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```

14. Добавьте следующий вспомогательный метод, используемый hello hello **Main** toohello метод **программы** класса.

    > [!NOTE] 
    > При копировании и вставке hello после кода, убедитесь в том, что hello скопированный код находится во hello же уровня как hello метода Main.

    ```csharp
    public static async Task<string> GetAuthorizationHeader()
    {
        AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
        ClientCredential credential = new ClientCredential(
            ConfigurationManager.AppSettings["ApplicationId"],
            ConfigurationManager.AppSettings["Password"]);
        AuthenticationResult result = await context.AcquireTokenAsync(
            resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
            clientCredential: credential);

        if (result != null)
            return result.AccessToken;

        throw new InvalidOperationException("Failed tooacquire token");
    }
    ```

15. В hello в обозревателе решений разверните проект hello (DataFactoryAPITestApp), щелкните правой кнопкой мыши **ссылки**и нажмите кнопку **добавить ссылку**. Установите флажок для сборки **System.Configuration**. Затем нажмите кнопку **ОК**.
16. Построение консольного приложения hello. Нажмите кнопку **построения** на hello меню и выберите пункт **построить решение**.
17. Убедитесь, что установлен хотя бы один файл в hello **adftutorial** контейнера в хранилище BLOB-объектов Azure. Если нет, создайте **Emp.txt** после содержимого hello-файл в Блокноте и отправьте его toohello adftutorial контейнера.

    ```
    John, Doe
    Jane, Doe
    ```
18. Запуск образца hello, щелкнув **отладки** -> **начать отладку** в меню "hello". При появлении hello **начало выполнения сведения о срез данных**, подождите несколько минут и нажмите клавишу **ввод**.
19. Используйте hello Azure портала tooverify этой фабрики данных hello **APITutorialFactory** создается с hello следующие артефакты:
   * Связанная служба: **LinkedService_AzureStorage**.
   * Набор данных: **InputDataset** и **OutputDataset**.
   * Конвейер: **PipelineBlobSample**
20. Убедитесь, что записи сотрудников hello два создаются в hello **emp** указана таблица в hello базы данных Azure SQL.

## <a name="next-steps"></a>Дальнейшие действия
Полную документацию по .NET API для Data Factory см. в [Справочник по .NET API фабрики данных](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).

В этом руководстве в ходе операции копирования вы использовали хранилище BLOB-объектов Azure как исходное хранилище данных, а базу данных SQL Azure — как целевое хранилище данных. Hello следующей таблице приведен список хранилищ данных, поддерживаемые действием копирования hello как источники и назначения: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn о том, как хранилище данных toocopy из данных, щелкните ссылку hello hello хранилища данных в таблице hello.

