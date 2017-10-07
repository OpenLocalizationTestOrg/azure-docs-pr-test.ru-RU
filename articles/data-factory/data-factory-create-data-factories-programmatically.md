---
title: "конвейеры данных aaaCreate с помощью пакета SDK .NET Azure | Документы Microsoft"
description: "Узнайте, как tooprogrammatically создавать, отслеживать и управлять фабриками данных Azure с помощью пакета SDK фабрики данных."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b0a357be-3040-4789-831e-0d0a32a0bda5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 190b5f99edbb3c27e1e8efb8990b9e601b22458f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a>Создание, отслеживание фабрик данных Azure и управление ими с помощью пакета SDK фабрики данных Azure для .NET
## <a name="overview"></a>Обзор
Создание, отслеживание фабрик данных и управление ими программным способом с помощью пакета .NET SDK фабрики данных. Эта статья содержит пошаговое руководство, которое нужно выполнить toocreate консольного приложения .NET образца, создает и отслеживает фабрики данных. 

> [!NOTE]
> Данная статья не охватывает все hello API .NET для фабрики данных. Полную документацию по API .NET для фабрики данных см. в [справочнике по API .NET фабрики данных](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1). 

## <a name="prerequisites"></a>Предварительные требования
* Visual Studio 2012, 2013 или 2015
* Скачанный и установленный [пакет SDK для Azure .NET](http://azure.microsoft.com/downloads/).
* Azure PowerShell. Следуйте инструкциям в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) статью tooinstall Azure PowerShell на компьютере. Можно использовать Azure PowerShell toocreate приложение Azure Active Directory.

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
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
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
В пошаговом руководстве hello создать фабрику данных с конвейером, который содержит операции копирования. Hello действие копирования копирует данные из папки в папку tooanother хранилища BLOB-объектов Azure в hello же хранилище больших двоичных объектов. 

Действие копирования Hello выполняет перемещение данных hello в фабрике данных Azure. Действие Hello выключен глобально доступной можно копировать данные между различными хранилищами данных в виде безопасные, надежные и масштабируемые службы. В разделе [действия перемещения данных](data-factory-data-movement-activities.md) статьи приведены сведения о действии копирования hello.

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
4. Замените содержимое hello **App.config** файл в проекте hello с hello после содержимого: 
    
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
5. В файле App.Config hello, обновите значения для  **&lt;идентификатор приложения&gt;**,  **&lt;пароль&gt;**,  **&lt; Идентификатор подписки&gt;**, и  **&lt;идентификатор клиента&gt;**  своими собственными значениями.
6. Добавьте следующее hello **с помощью** toohello инструкций **Program.cs** файл в проекте hello.

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

    //IMPORTANT: specify hello name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: hello name of hello data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > Замените значение hello **resourceGroupName** с именем hello группы ресурсов Azure. Можно создать группу ресурсов с помощью hello [New AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) командлета.
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
9. Добавьте следующий код, создающий hello **наборы входных и выходных данных** toohello **Main** метод.

    Hello **FolderPath** для входного большого двоичного объекта hello установлено слишком**adftutorial /** где **adftutorial** является именем hello hello контейнера в хранилище BLOB-объектов. Если этот контейнер не существует в хранилище BLOB-объектов Azure, создать контейнер с таким именем: **adftutorial** и отправить файл toohello текстовый контейнер.

    Hello FolderPath для hello выходные данные большого двоичного объекта имеет значение: **adftutorial/apifactoryoutput / {Slice}** где **срез** является hello динамически вычисленная на основе значений **SliceStart**(запустите даты и времени каждого среза).

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "DatasetBlobSource";
    string Dataset_Destination = "DatasetBlobDestination";
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
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
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Destination,
            Properties = new DatasetProperties()
            {
    
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/apifactoryoutput/{Slice}",
                    PartitionedBy = new Collection<Partition>()
                    {
                        new Partition()
                        {
                            Name = "Slice",
                            Value = new DateTimePartitionValue()
                            {
                                Date = "SliceStart",
                                Format = "yyyyMMdd-HH"
                            }
                        }
                    }
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
10. Добавьте hello следующий код, чтобы **создает и активирует конвейера** toohello **Main** метод. В этом конвейере есть действие **CopyActivity**, принимающие **BlobSource** как источник и **BlobSink** как приемник.

    Действие копирования Hello выполняет перемещение данных hello в фабрике данных Azure. Действие Hello выключен глобально доступной можно копировать данные между различными хранилищами данных в виде безопасные, надежные и масштабируемые службы. В разделе [действия перемещения данных](data-factory-data-movement-activities.md) статьи приведены сведения о действии копирования hello.

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2014, 8, 9, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
    string PipelineName = "PipelineBlobSample";
    
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
                        Name = "BlobToBlob",
                        Inputs = new List<ActivityInput>()
                        {
                            new ActivityInput()
                {
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
    
                },
            }
        }
    });
    ```
12. Добавьте следующий код toohello hello **Main** метод tooget hello состояние срез данных hello выходной набор данных. В этом примере ожидается только один срез.

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
13. **(необязательно)**  Добавить hello следующий код запуска tooget подробные сведения об toohello срез данных **Main** метод.

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
        });
    
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
14. Добавьте следующий вспомогательный метод, используемый hello hello **Main** toohello метод **программы** класса. Этот метод выводит диалоговое окно, который позволяет предоставлять **имя пользователя** и **пароль** использовать toolog tooAzure портала.

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

15. В hello обозревателе решений разверните проект hello: **DataFactoryAPITestApp**, щелкните правой кнопкой мыши **ссылки**и нажмите кнопку **добавить ссылку**. Установите флажок для сборки `System.Configuration` и нажмите кнопку **ОК**.
15. Построение консольного приложения hello. Нажмите кнопку **построения** на hello меню и выберите пункт **построить решение**.
16. Убедитесь, что установлен хотя бы один файл в контейнере adftutorial hello в хранилище BLOB-объектов Azure. В противном случае создайте Emp.txt файл в Блокноте с hello после содержимого и выгрузить его toohello adftutorial контейнера.

    ```
    John, Doe
    Jane, Doe
    ```
17. Запуск образца hello, щелкнув **отладки** -> **начать отладку** в меню "hello". При появлении hello **начало выполнения сведения о срез данных**, подождите несколько минут и нажмите клавишу **ввод**.
18. Используйте hello Azure портала tooverify этой фабрики данных hello **APITutorialFactory** создается с hello следующие артефакты:
    * Связанная служба: **AzureStorageLinkedService**.
    * Набор данных: **DatasetBlobSource** и **DatasetBlobDestination**.
    * Конвейер: **PipelineBlobSample**
19. Убедитесь, что выходной файл создается в hello **apifactoryoutput** папки в hello **adftutorial** контейнера.

## <a name="get-a-list-of-failed-data-slices"></a>Получение списка невыполненных срезов данных 

```csharp
// Parse hello resource path
var ResourceGroupName = "ADFTutorialResourceGroup";
var DataFactoryName = "DataFactoryAPITestApp";

var parameters = new ActivityWindowsByDataFactoryListParameters(ResourceGroupName, DataFactoryName);
parameters.WindowState = "Failed";
var response = dataFactoryManagementClient.ActivityWindows.List(parameters);
do
{
    foreach (var activityWindow in response.ActivityWindowListResponseValue.ActivityWindows)
    {
        var row = string.Join(
            "\t",
            activityWindow.WindowStart.ToString(),
            activityWindow.WindowEnd.ToString(),
            activityWindow.RunStart.ToString(),
            activityWindow.RunEnd.ToString(),
            activityWindow.DataFactoryName,
            activityWindow.PipelineName,
            activityWindow.ActivityName,
            string.Join(",", activityWindow.OutputDatasets));
        Console.WriteLine(row);
    }

    if (response.NextLink != null)
    {
        response = dataFactoryManagementClient.ActivityWindows.ListNext(response.NextLink, parameters);
    }
    else
    {
        response = null;
    }
}
while (response != null);
```

## <a name="next-steps"></a>Дальнейшие действия
См. следующий пример для создания конвейера, с помощью пакета SDK .NET, копирующего данные из базы данных Azure SQL tooan хранилища BLOB-объектов Azure hello. 

- [Создание конвейера toocopy данных из хранилища больших двоичных объектов tooSQL базы данных](data-factory-copy-activity-tutorial-using-dotnet-api.md)
