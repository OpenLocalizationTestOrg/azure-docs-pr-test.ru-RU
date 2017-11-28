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
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a><span data-ttu-id="4ddf0-103">Создание, отслеживание фабрик данных Azure и управление ими с помощью пакета SDK фабрики данных Azure для .NET</span><span class="sxs-lookup"><span data-stu-id="4ddf0-103">Create, monitor, and manage Azure data factories using Azure Data Factory .NET SDK</span></span>
## <a name="overview"></a><span data-ttu-id="4ddf0-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="4ddf0-104">Overview</span></span>
<span data-ttu-id="4ddf0-105">Создание, отслеживание фабрик данных и управление ими программным способом с помощью пакета .NET SDK фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-105">You can create, monitor, and manage Azure data factories programmatically using Data Factory .NET SDK.</span></span> <span data-ttu-id="4ddf0-106">Эта статья содержит пошаговое руководство, которое нужно выполнить toocreate консольного приложения .NET образца, создает и отслеживает фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-106">This article contains a walkthrough that you can follow toocreate a sample .NET console application that creates and monitors a data factory.</span></span> 

> [!NOTE]
> <span data-ttu-id="4ddf0-107">Данная статья не охватывает все hello API .NET для фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-107">This article does not cover all hello Data Factory .NET API.</span></span> <span data-ttu-id="4ddf0-108">Полную документацию по API .NET для фабрики данных см. в [справочнике по API .NET фабрики данных](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="4ddf0-108">See [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) for comprehensive documentation on .NET API for Data Factory.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4ddf0-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4ddf0-109">Prerequisites</span></span>
* <span data-ttu-id="4ddf0-110">Visual Studio 2012, 2013 или 2015</span><span class="sxs-lookup"><span data-stu-id="4ddf0-110">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="4ddf0-111">Скачанный и установленный [пакет SDK для Azure .NET](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="4ddf0-111">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="4ddf0-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-112">Azure PowerShell.</span></span> <span data-ttu-id="4ddf0-113">Следуйте инструкциям в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) статью tooinstall Azure PowerShell на компьютере.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-113">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall Azure PowerShell on your computer.</span></span> <span data-ttu-id="4ddf0-114">Можно использовать Azure PowerShell toocreate приложение Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-114">You use Azure PowerShell toocreate an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="4ddf0-115">Создание приложения в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4ddf0-115">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="4ddf0-116">Создать приложение Azure Active Directory, создать участника-службы для приложения hello и назначьте его toohello **участника фабрики данных** роли.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-116">Create an Azure Active Directory application, create a service principal for hello application, and assign it toohello **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="4ddf0-117">Запустите **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-117">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="4ddf0-118">Запустите следующую команду hello и введите hello имя пользователя и пароль, использовать toosign в toohello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-118">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="4ddf0-119">Запустите следующие команды tooview hello все hello подписки для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-119">Run hello following command tooview all hello subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="4ddf0-120">Следующая команда tooselect hello подписки на toowork с выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-120">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="4ddf0-121">Замените  **&lt;NameOfAzureSubscription** &gt; с именем hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-121">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="4ddf0-122">Запишите **SubscriptionId** и **TenantId** hello в выходных данных этой команды.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-122">Note down **SubscriptionId** and **TenantId** from hello output of this command.</span></span>

5. <span data-ttu-id="4ddf0-123">Создание группы ресурсов Azure с именем **ADFTutorialResourceGroup** , выполнив следующую команду в hello PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-123">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="4ddf0-124">Если группа ресурсов hello уже существует, укажите ли tooupdate его (Y) или сохранить его как (N).</span><span class="sxs-lookup"><span data-stu-id="4ddf0-124">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="4ddf0-125">Если вы используете другой группе ресурсов, в этом учебнике требуется имя hello toouse вместо ADFTutorialResourceGroup группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-125">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="4ddf0-126">Создайте приложение Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-126">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="4ddf0-127">Если появляется следующая ошибка hello, укажите другой URL-адрес и снова выполните команду hello.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-127">If you get hello following error, specify a different URL and run hello command again.</span></span>
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="4ddf0-128">Создайте участника-службы AD hello.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-128">Create hello AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="4ddf0-129">Добавление участника toohello службы **участника фабрики данных** роли.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-129">Add service principal toohello **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="4ddf0-130">Получить идентификатор приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-130">Get hello application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="4ddf0-131">Запишите идентификатор приложения hello (applicationID) hello в выходных данных.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-131">Note down hello application ID (applicationID) from hello output.</span></span>

<span data-ttu-id="4ddf0-132">Вы должны получить следующие четыре значения:</span><span class="sxs-lookup"><span data-stu-id="4ddf0-132">You should have following four values from these steps:</span></span>

* <span data-ttu-id="4ddf0-133">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="4ddf0-133">Tenant ID</span></span>
* <span data-ttu-id="4ddf0-134">Идентификатор подписки</span><span class="sxs-lookup"><span data-stu-id="4ddf0-134">Subscription ID</span></span>
* <span data-ttu-id="4ddf0-135">Идентификатор приложения</span><span class="sxs-lookup"><span data-stu-id="4ddf0-135">Application ID</span></span>
* <span data-ttu-id="4ddf0-136">Пароль (в первой команде hello)</span><span class="sxs-lookup"><span data-stu-id="4ddf0-136">Password (specified in hello first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="4ddf0-137">Пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="4ddf0-137">Walkthrough</span></span>
<span data-ttu-id="4ddf0-138">В пошаговом руководстве hello создать фабрику данных с конвейером, который содержит операции копирования.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-138">In hello walkthrough, you create a data factory with a pipeline that contains a copy activity.</span></span> <span data-ttu-id="4ddf0-139">Hello действие копирования копирует данные из папки в папку tooanother хранилища BLOB-объектов Azure в hello же хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-139">hello copy activity copies data from a folder in your Azure blob storage tooanother folder in hello same blob storage.</span></span> 

<span data-ttu-id="4ddf0-140">Действие копирования Hello выполняет перемещение данных hello в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-140">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="4ddf0-141">Действие Hello выключен глобально доступной можно копировать данные между различными хранилищами данных в виде безопасные, надежные и масштабируемые службы.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-141">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="4ddf0-142">В разделе [действия перемещения данных](data-factory-data-movement-activities.md) статьи приведены сведения о действии копирования hello.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-142">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>

1. <span data-ttu-id="4ddf0-143">С помощью Visual Studio 2012, 2013 или 2015 создайте консольное приложение C# .NET.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-143">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="4ddf0-144">Запустите **Visual Studio** 2012, 2013 или 2015.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-144">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="4ddf0-145">Нажмите кнопку **файл**, слишком точки**New**и нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-145">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="4ddf0-146">Разверните раздел **Шаблоны** и выберите **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-146">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="4ddf0-147">В этом пошаговом руководстве используется C#, но можно использовать любой язык .NET.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-147">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="4ddf0-148">Выберите **консольное приложение** hello списке типов проекта на hello вправо.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-148">Select **Console Application** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="4ddf0-149">Введите **DataFactoryAPITestApp** для hello имя.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-149">Enter **DataFactoryAPITestApp** for hello Name.</span></span>
   6. <span data-ttu-id="4ddf0-150">Выберите **C:\ADFGetStarted** для hello расположение.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-150">Select **C:\ADFGetStarted** for hello Location.</span></span>
   7. <span data-ttu-id="4ddf0-151">Нажмите кнопку **ОК** toocreate hello проекта.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-151">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="4ddf0-152">Нажмите кнопку **средства**, слишком точки**диспетчера пакетов NuGet**и нажмите кнопку **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-152">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="4ddf0-153">В hello **консоль диспетчера пакетов**, hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4ddf0-153">In hello **Package Manager Console**, do hello following steps:</span></span>
   1. <span data-ttu-id="4ddf0-154">Выполните hello, следующая команда tooinstall фабрики данных пакета.`Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="4ddf0-154">Run hello following command tooinstall Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="4ddf0-155">Выполните hello, следующая команда tooinstall Azure Active Directory пакет (использовать Active Directory API в коде hello).`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="4ddf0-155">Run hello following command tooinstall Azure Active Directory package (you use Active Directory API in hello code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="4ddf0-156">Замените содержимое hello **App.config** файл в проекте hello с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="4ddf0-156">Replace hello contents of **App.config** file in hello project with hello following content:</span></span> 
    
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
5. <span data-ttu-id="4ddf0-157">В файле App.Config hello, обновите значения для  **&lt;идентификатор приложения&gt;**,  **&lt;пароль&gt;**,  **&lt; Идентификатор подписки&gt;**, и  **&lt;идентификатор клиента&gt;**  своими собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-157">In hello App.Config file, update values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>
6. <span data-ttu-id="4ddf0-158">Добавьте следующее hello **с помощью** toohello инструкций **Program.cs** файл в проекте hello.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-158">Add hello following **using** statements toohello **Program.cs** file in hello project.</span></span>

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
6. <span data-ttu-id="4ddf0-159">Добавьте следующий код, который создает экземпляр hello **DataPipelineManagementClient** toohello класса **Main** метод.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-159">Add hello following code that creates an instance of **DataPipelineManagementClient** class toohello **Main** method.</span></span> <span data-ttu-id="4ddf0-160">Этот объект toocreate используется фабрики данных, связанной службы, входные и выходные наборы данных и конвейера.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-160">You use this object toocreate a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="4ddf0-161">Вы также использовать срезы toomonitor этот объект набора данных во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-161">You also use this object toomonitor slices of a dataset at runtime.</span></span>

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
   > <span data-ttu-id="4ddf0-162">Замените значение hello **resourceGroupName** с именем hello группы ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-162">Replace hello value of **resourceGroupName** with hello name of your Azure resource group.</span></span> <span data-ttu-id="4ddf0-163">Можно создать группу ресурсов с помощью hello [New AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) командлета.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-163">You can create a resource group using hello [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span>
   >
   > <span data-ttu-id="4ddf0-164">Обновите hello данных фабрики (с именем dataFactoryName) toobe уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-164">Update name of hello data factory (dataFactoryName) toobe unique.</span></span> <span data-ttu-id="4ddf0-165">Имя фабрики данных hello должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-165">Name of hello data factory must be globally unique.</span></span> <span data-ttu-id="4ddf0-166">Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-166">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
7. <span data-ttu-id="4ddf0-167">Добавьте следующий код, создающий hello **фабрики данных** toohello **Main** метод.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-167">Add hello following code that creates a **data factory** toohello **Main** method.</span></span>

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
8. <span data-ttu-id="4ddf0-168">Добавьте следующий код, создающий hello **связанная служба хранилища Azure** toohello **Main** метод.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-168">Add hello following code that creates an **Azure Storage linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4ddf0-169">Замените значения **storageaccountname** и **accountkey** именем и ключом вашей учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-169">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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
9. <span data-ttu-id="4ddf0-170">Добавьте следующий код, создающий hello **наборы входных и выходных данных** toohello **Main** метод.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-170">Add hello following code that creates **input and output datasets** toohello **Main** method.</span></span>

    <span data-ttu-id="4ddf0-171">Hello **FolderPath** для входного большого двоичного объекта hello установлено слишком**adftutorial /** где **adftutorial** является именем hello hello контейнера в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-171">hello **FolderPath** for hello input blob is set too**adftutorial/** where **adftutorial** is hello name of hello container in your blob storage.</span></span> <span data-ttu-id="4ddf0-172">Если этот контейнер не существует в хранилище BLOB-объектов Azure, создать контейнер с таким именем: **adftutorial** и отправить файл toohello текстовый контейнер.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-172">If this container does not exist in your Azure blob storage, create a container with this name: **adftutorial** and upload a text file toohello container.</span></span>

    <span data-ttu-id="4ddf0-173">Hello FolderPath для hello выходные данные большого двоичного объекта имеет значение: **adftutorial/apifactoryoutput / {Slice}** где **срез** является hello динамически вычисленная на основе значений **SliceStart**(запустите даты и времени каждого среза).</span><span class="sxs-lookup"><span data-stu-id="4ddf0-173">hello FolderPath for hello output blob is set to: **adftutorial/apifactoryoutput/{Slice}** where **Slice** is dynamically calculated based on hello value of **SliceStart** (start date-time of each slice.)</span></span>

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
10. <span data-ttu-id="4ddf0-174">Добавьте hello следующий код, чтобы **создает и активирует конвейера** toohello **Main** метод.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-174">Add hello following code that **creates and activates a pipeline** toohello **Main** method.</span></span> <span data-ttu-id="4ddf0-175">В этом конвейере есть действие **CopyActivity**, принимающие **BlobSource** как источник и **BlobSink** как приемник.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-175">This pipeline has a **CopyActivity** that takes **BlobSource** as a source and **BlobSink** as a sink.</span></span>

    <span data-ttu-id="4ddf0-176">Действие копирования Hello выполняет перемещение данных hello в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-176">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="4ddf0-177">Действие Hello выключен глобально доступной можно копировать данные между различными хранилищами данных в виде безопасные, надежные и масштабируемые службы.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-177">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="4ddf0-178">В разделе [действия перемещения данных](data-factory-data-movement-activities.md) статьи приведены сведения о действии копирования hello.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-178">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>

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
12. <span data-ttu-id="4ddf0-179">Добавьте следующий код toohello hello **Main** метод tooget hello состояние срез данных hello выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-179">Add hello following code toohello **Main** method tooget hello status of a data slice of hello output dataset.</span></span> <span data-ttu-id="4ddf0-180">В этом примере ожидается только один срез.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-180">There is only one slice expected in this sample.</span></span>

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
13. <span data-ttu-id="4ddf0-181">**(необязательно)**  Добавить hello следующий код запуска tooget подробные сведения об toohello срез данных **Main** метод.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-181">**(optional)** Add hello following code tooget run details for a data slice toohello **Main** method.</span></span>

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
14. <span data-ttu-id="4ddf0-182">Добавьте следующий вспомогательный метод, используемый hello hello **Main** toohello метод **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-182">Add hello following helper method used by hello **Main** method toohello **Program** class.</span></span> <span data-ttu-id="4ddf0-183">Этот метод выводит диалоговое окно, который позволяет предоставлять **имя пользователя** и **пароль** использовать toolog tooAzure портала.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-183">This method pops a dialog box that that lets you provide **user name** and **password** that you use toolog in tooAzure portal.</span></span>

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

15. <span data-ttu-id="4ddf0-184">В hello обозревателе решений разверните проект hello: **DataFactoryAPITestApp**, щелкните правой кнопкой мыши **ссылки**и нажмите кнопку **добавить ссылку**.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-184">In hello Solution Explorer, expand hello project: **DataFactoryAPITestApp**, right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="4ddf0-185">Установите флажок для сборки `System.Configuration` и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-185">Select check box for `System.Configuration` assembly and click **OK**.</span></span>
15. <span data-ttu-id="4ddf0-186">Построение консольного приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-186">Build hello console application.</span></span> <span data-ttu-id="4ddf0-187">Нажмите кнопку **построения** на hello меню и выберите пункт **построить решение**.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-187">Click **Build** on hello menu and click **Build Solution**.</span></span>
16. <span data-ttu-id="4ddf0-188">Убедитесь, что установлен хотя бы один файл в контейнере adftutorial hello в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-188">Confirm that there is at least one file in hello adftutorial container in your Azure blob storage.</span></span> <span data-ttu-id="4ddf0-189">В противном случае создайте Emp.txt файл в Блокноте с hello после содержимого и выгрузить его toohello adftutorial контейнера.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-189">If not, create Emp.txt file in Notepad with hello following content and upload it toohello adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
17. <span data-ttu-id="4ddf0-190">Запуск образца hello, щелкнув **отладки** -> **начать отладку** в меню "hello".</span><span class="sxs-lookup"><span data-stu-id="4ddf0-190">Run hello sample by clicking **Debug** -> **Start Debugging** on hello menu.</span></span> <span data-ttu-id="4ddf0-191">При появлении hello **начало выполнения сведения о срез данных**, подождите несколько минут и нажмите клавишу **ввод**.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-191">When you see hello **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
18. <span data-ttu-id="4ddf0-192">Используйте hello Azure портала tooverify этой фабрики данных hello **APITutorialFactory** создается с hello следующие артефакты:</span><span class="sxs-lookup"><span data-stu-id="4ddf0-192">Use hello Azure portal tooverify that hello data factory **APITutorialFactory** is created with hello following artifacts:</span></span>
    * <span data-ttu-id="4ddf0-193">Связанная служба: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-193">Linked service: **AzureStorageLinkedService**</span></span>
    * <span data-ttu-id="4ddf0-194">Набор данных: **DatasetBlobSource** и **DatasetBlobDestination**.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-194">Dataset: **DatasetBlobSource** and **DatasetBlobDestination**.</span></span>
    * <span data-ttu-id="4ddf0-195">Конвейер: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="4ddf0-195">Pipeline: **PipelineBlobSample**</span></span>
19. <span data-ttu-id="4ddf0-196">Убедитесь, что выходной файл создается в hello **apifactoryoutput** папки в hello **adftutorial** контейнера.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-196">Verify that an output file is created in hello **apifactoryoutput** folder in hello **adftutorial** container.</span></span>

## <a name="get-a-list-of-failed-data-slices"></a><span data-ttu-id="4ddf0-197">Получение списка невыполненных срезов данных</span><span class="sxs-lookup"><span data-stu-id="4ddf0-197">Get a list of failed data slices</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="4ddf0-198">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4ddf0-198">Next steps</span></span>
<span data-ttu-id="4ddf0-199">См. следующий пример для создания конвейера, с помощью пакета SDK .NET, копирующего данные из базы данных Azure SQL tooan хранилища BLOB-объектов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4ddf0-199">See hello following example for creating a pipeline using .NET SDK that copies data from an Azure blob storage tooan Azure SQL database:</span></span> 

- [<span data-ttu-id="4ddf0-200">Создание конвейера toocopy данных из хранилища больших двоичных объектов tooSQL базы данных</span><span class="sxs-lookup"><span data-stu-id="4ddf0-200">Create a pipeline toocopy data from Blob Storage tooSQL Database</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
