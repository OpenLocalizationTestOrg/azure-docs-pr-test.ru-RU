---
title: "Создание конвейеров данных с помощью пакета SDK Azure для .NET | Документация Майкрософт"
description: "Узнайте, как программным способом создавать, отслеживать и контролировать фабрики данных Azure с помощью пакета SDK фабрики данных."
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
ms.openlocfilehash: 9d9dac75321c5d4e079f49320d9b7c6f56e48754
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a><span data-ttu-id="a76c8-103">Создание, отслеживание фабрик данных Azure и управление ими с помощью пакета SDK фабрики данных Azure для .NET</span><span class="sxs-lookup"><span data-stu-id="a76c8-103">Create, monitor, and manage Azure data factories using Azure Data Factory .NET SDK</span></span>
## <a name="overview"></a><span data-ttu-id="a76c8-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="a76c8-104">Overview</span></span>
<span data-ttu-id="a76c8-105">Создание, отслеживание фабрик данных и управление ими программным способом с помощью пакета .NET SDK фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="a76c8-105">You can create, monitor, and manage Azure data factories programmatically using Data Factory .NET SDK.</span></span> <span data-ttu-id="a76c8-106">Эта статья содержит пошаговое руководство по созданию образца консольного приложения .NET, которое будет создавать и отслеживать фабрику данных.</span><span class="sxs-lookup"><span data-stu-id="a76c8-106">This article contains a walkthrough that you can follow to create a sample .NET console application that creates and monitors a data factory.</span></span> 

> [!NOTE]
> <span data-ttu-id="a76c8-107">В этой статье рассматриваются не все API-интерфейсы .NET фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="a76c8-107">This article does not cover all the Data Factory .NET API.</span></span> <span data-ttu-id="a76c8-108">Полную документацию по API .NET для фабрики данных см. в [справочнике по API .NET фабрики данных](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="a76c8-108">See [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) for comprehensive documentation on .NET API for Data Factory.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a76c8-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a76c8-109">Prerequisites</span></span>
* <span data-ttu-id="a76c8-110">Visual Studio 2012, 2013 или 2015</span><span class="sxs-lookup"><span data-stu-id="a76c8-110">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="a76c8-111">Скачанный и установленный [пакет SDK для Azure .NET](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a76c8-111">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="a76c8-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a76c8-112">Azure PowerShell.</span></span> <span data-ttu-id="a76c8-113">Далее, чтобы установить Azure PowerShell на локальном компьютере, следуйте указаниям в разделе [Установка и настройка Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="a76c8-113">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install Azure PowerShell on your computer.</span></span> <span data-ttu-id="a76c8-114">С помощью Azure PowerShell вы создадите приложение Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a76c8-114">You use Azure PowerShell to create an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="a76c8-115">Создание приложения в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a76c8-115">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="a76c8-116">Вы создадите приложение Azure Active Directory и субъект-службу для приложения, а затем назначите роль **Участник Data Factory** .</span><span class="sxs-lookup"><span data-stu-id="a76c8-116">Create an Azure Active Directory application, create a service principal for the application, and assign it to the **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="a76c8-117">Запустите **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="a76c8-117">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="a76c8-118">Выполните следующую команду и введите имя пользователя и пароль, которые используются для входа на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a76c8-118">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="a76c8-119">Выполните следующую команду, чтобы просмотреть все подписки для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="a76c8-119">Run the following command to view all the subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="a76c8-120">Выполните следующую команду, чтобы выбрать подписку, с которой вы собираетесь работать.</span><span class="sxs-lookup"><span data-stu-id="a76c8-120">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="a76c8-121">Замените **&lt;NameOfAzureSubscription**&gt; именем своей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="a76c8-121">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="a76c8-122">Запишите значения **SubscriptionId** и **TenantId**, указанные в выходных данных этой команды.</span><span class="sxs-lookup"><span data-stu-id="a76c8-122">Note down **SubscriptionId** and **TenantId** from the output of this command.</span></span>

5. <span data-ttu-id="a76c8-123">Создайте группу ресурсов Azure с именем **ADFTutorialResourceGroup** , выполнив следующую команду в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a76c8-123">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="a76c8-124">Если группа ресурсов уже есть, укажите, требуется или не требуется ее обновить (Y или N соответственно).</span><span class="sxs-lookup"><span data-stu-id="a76c8-124">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="a76c8-125">Если вы используете другую группу ресурсов, укажите ее имя вместо ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="a76c8-125">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="a76c8-126">Создайте приложение Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a76c8-126">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="a76c8-127">Если возникнет следующая ошибка, укажите другой URL-адрес и запустите команду еще раз.</span><span class="sxs-lookup"><span data-stu-id="a76c8-127">If you get the following error, specify a different URL and run the command again.</span></span>
    
    ```PowerShell
    Another object with the same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="a76c8-128">Создайте субъект-службу AD.</span><span class="sxs-lookup"><span data-stu-id="a76c8-128">Create the AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="a76c8-129">Назначьте субъекту-службе роль **Участник Data Factory** .</span><span class="sxs-lookup"><span data-stu-id="a76c8-129">Add service principal to the **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="a76c8-130">Получите идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="a76c8-130">Get the application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="a76c8-131">Запишите идентификатор приложения (applicationID) из выходных данных.</span><span class="sxs-lookup"><span data-stu-id="a76c8-131">Note down the application ID (applicationID) from the output.</span></span>

<span data-ttu-id="a76c8-132">Вы должны получить следующие четыре значения:</span><span class="sxs-lookup"><span data-stu-id="a76c8-132">You should have following four values from these steps:</span></span>

* <span data-ttu-id="a76c8-133">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="a76c8-133">Tenant ID</span></span>
* <span data-ttu-id="a76c8-134">Идентификатор подписки</span><span class="sxs-lookup"><span data-stu-id="a76c8-134">Subscription ID</span></span>
* <span data-ttu-id="a76c8-135">Идентификатор приложения</span><span class="sxs-lookup"><span data-stu-id="a76c8-135">Application ID</span></span>
* <span data-ttu-id="a76c8-136">пароль (указан в первой команде).</span><span class="sxs-lookup"><span data-stu-id="a76c8-136">Password (specified in the first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="a76c8-137">Пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="a76c8-137">Walkthrough</span></span>
<span data-ttu-id="a76c8-138">В этом пошаговом руководстве вы создадите фабрику данных с конвейером, который содержит действие копирования.</span><span class="sxs-lookup"><span data-stu-id="a76c8-138">In the walkthrough, you create a data factory with a pipeline that contains a copy activity.</span></span> <span data-ttu-id="a76c8-139">Действие копирования копирует данные из папки в хранилище BLOB-объектов Azure в другую папку в том же хранилище.</span><span class="sxs-lookup"><span data-stu-id="a76c8-139">The copy activity copies data from a folder in your Azure blob storage to another folder in the same blob storage.</span></span> 

<span data-ttu-id="a76c8-140">Действие копирования перемещает данные в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="a76c8-140">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="a76c8-141">Это действие выполняется с помощью глобально доступной службы, обеспечивающей безопасное, надежное и масштабируемое копирование данных между разными хранилищами.</span><span class="sxs-lookup"><span data-stu-id="a76c8-141">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="a76c8-142">Дополнительные сведения о действии копирования см. в статье [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="a76c8-142">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>

1. <span data-ttu-id="a76c8-143">С помощью Visual Studio 2012, 2013 или 2015 создайте консольное приложение C# .NET.</span><span class="sxs-lookup"><span data-stu-id="a76c8-143">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="a76c8-144">Запустите **Visual Studio** 2012, 2013 или 2015.</span><span class="sxs-lookup"><span data-stu-id="a76c8-144">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="a76c8-145">Щелкните **Файл**, наведите указатель мыши на пункт **Создать** и щелкните **Проект**.</span><span class="sxs-lookup"><span data-stu-id="a76c8-145">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="a76c8-146">Разверните раздел **Шаблоны** и выберите **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="a76c8-146">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="a76c8-147">В этом пошаговом руководстве используется C#, но можно использовать любой язык .NET.</span><span class="sxs-lookup"><span data-stu-id="a76c8-147">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="a76c8-148">Выберите **Консольное приложение** в списке типов проектов справа.</span><span class="sxs-lookup"><span data-stu-id="a76c8-148">Select **Console Application** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="a76c8-149">В качестве имени введите **DataFactoryAPITestApp** .</span><span class="sxs-lookup"><span data-stu-id="a76c8-149">Enter **DataFactoryAPITestApp** for the Name.</span></span>
   6. <span data-ttu-id="a76c8-150">В качестве расположения укажите **C:\ADFGetStarted**.</span><span class="sxs-lookup"><span data-stu-id="a76c8-150">Select **C:\ADFGetStarted** for the Location.</span></span>
   7. <span data-ttu-id="a76c8-151">Нажмите кнопку **ОК** , чтобы создать проект.</span><span class="sxs-lookup"><span data-stu-id="a76c8-151">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="a76c8-152">Щелкните **Инструменты**, наведите указатель мыши на **Диспетчер пакетов NuGet** и щелкните **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="a76c8-152">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="a76c8-153">В **консоли диспетчера пакетов** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a76c8-153">In the **Package Manager Console**, do the following steps:</span></span>
   1. <span data-ttu-id="a76c8-154">Выполните следующую команду, чтобы установить пакет фабрики данных: `Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="a76c8-154">Run the following command to install Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="a76c8-155">Выполните следующую команду, чтобы установить пакет Azure Active Directory (используйте Active Directory API в коде): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="a76c8-155">Run the following command to install Azure Active Directory package (you use Active Directory API in the code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="a76c8-156">Замените содержимое файла **App.config** в проекте следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="a76c8-156">Replace the contents of **App.config** file in the project with the following content:</span></span> 
    
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating the AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```
5. <span data-ttu-id="a76c8-157">В файле App.Config замените значения **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;** и **&lt;tenant ID&gt;** собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="a76c8-157">In the App.Config file, update values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>
6. <span data-ttu-id="a76c8-158">Добавьте следующие инструкции **using** в файл **Program.cs** в проекте.</span><span class="sxs-lookup"><span data-stu-id="a76c8-158">Add the following **using** statements to the **Program.cs** file in the project.</span></span>

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
6. <span data-ttu-id="a76c8-159">Добавьте в метод **Main** приведенный ниже код, который создает экземпляр класса **DataPipelineManagementClient**.</span><span class="sxs-lookup"><span data-stu-id="a76c8-159">Add the following code that creates an instance of **DataPipelineManagementClient** class to the **Main** method.</span></span> <span data-ttu-id="a76c8-160">Этот объект используется не только для создания фабрики данных, связанной службы, входных и выходных наборов данных, а также конвейера,</span><span class="sxs-lookup"><span data-stu-id="a76c8-160">You use this object to create a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="a76c8-161">но и для отслеживания срезов набора данных при выполнении.</span><span class="sxs-lookup"><span data-stu-id="a76c8-161">You also use this object to monitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client

    //IMPORTANT: specify the name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: the name of the data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="a76c8-162">Замените значение **resourceGroupName** именем своей группы ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="a76c8-162">Replace the value of **resourceGroupName** with the name of your Azure resource group.</span></span> <span data-ttu-id="a76c8-163">Для создания группы ресурсов можно использовать командлет [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) .</span><span class="sxs-lookup"><span data-stu-id="a76c8-163">You can create a resource group using the [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span>
   >
   > <span data-ttu-id="a76c8-164">Измените имя фабрики данных (dataFactoryName) на уникальное.</span><span class="sxs-lookup"><span data-stu-id="a76c8-164">Update name of the data factory (dataFactoryName) to be unique.</span></span> <span data-ttu-id="a76c8-165">чтобы оно было глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="a76c8-165">Name of the data factory must be globally unique.</span></span> <span data-ttu-id="a76c8-166">Ознакомьтесь с разделом [Фабрика данных — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="a76c8-166">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
7. <span data-ttu-id="a76c8-167">Добавьте следующий код, создающий **фабрику данных**, в метод **Main**.</span><span class="sxs-lookup"><span data-stu-id="a76c8-167">Add the following code that creates a **data factory** to the **Main** method.</span></span>

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
8. <span data-ttu-id="a76c8-168">Добавьте следующий код, который создает **связанную службу хранилища Azure**, в метод **Main**.</span><span class="sxs-lookup"><span data-stu-id="a76c8-168">Add the following code that creates an **Azure Storage linked service** to the **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="a76c8-169">Замените значения **storageaccountname** и **accountkey** именем и ключом вашей учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="a76c8-169">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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
9. <span data-ttu-id="a76c8-170">Добавьте следующий код, создающий **входные и выходные наборы данных**, в метод **Main**.</span><span class="sxs-lookup"><span data-stu-id="a76c8-170">Add the following code that creates **input and output datasets** to the **Main** method.</span></span>

    <span data-ttu-id="a76c8-171">**FolderPath** для входного большого двоичного объекта задан как **adftutorial/**, где **adftutorial** — это имя контейнера в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="a76c8-171">The **FolderPath** for the input blob is set to **adftutorial/** where **adftutorial** is the name of the container in your blob storage.</span></span> <span data-ttu-id="a76c8-172">Если этот контейнер не существует в хранилище больших двоичных объектов Azure, создайте контейнер с именем **adftutorial** и отправьте в него текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="a76c8-172">If this container does not exist in your Azure blob storage, create a container with this name: **adftutorial** and upload a text file to the container.</span></span>

    <span data-ttu-id="a76c8-173">FolderPath для выходного большого двоичного объекта задан как **adftutorial/apifactoryoutput/{срез}**, где **срез** динамически рассчитывается на основе значения **SliceStart** (начальные дата и время каждого среза).</span><span class="sxs-lookup"><span data-stu-id="a76c8-173">The FolderPath for the output blob is set to: **adftutorial/apifactoryoutput/{Slice}** where **Slice** is dynamically calculated based on the value of **SliceStart** (start date-time of each slice.)</span></span>

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
10. <span data-ttu-id="a76c8-174">Добавьте следующий код, который **создает и активирует конвейер**, в метод **Main**.</span><span class="sxs-lookup"><span data-stu-id="a76c8-174">Add the following code that **creates and activates a pipeline** to the **Main** method.</span></span> <span data-ttu-id="a76c8-175">В этом конвейере есть действие **CopyActivity**, принимающие **BlobSource** как источник и **BlobSink** как приемник.</span><span class="sxs-lookup"><span data-stu-id="a76c8-175">This pipeline has a **CopyActivity** that takes **BlobSource** as a source and **BlobSink** as a sink.</span></span>

    <span data-ttu-id="a76c8-176">Действие копирования перемещает данные в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="a76c8-176">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="a76c8-177">Это действие выполняется с помощью глобально доступной службы, обеспечивающей безопасное, надежное и масштабируемое копирование данных между разными хранилищами.</span><span class="sxs-lookup"><span data-stu-id="a76c8-177">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="a76c8-178">Дополнительные сведения о действии копирования см. в статье [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="a76c8-178">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>

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
    
                // Initial value for pipeline's active period. With this, you won't need to set slice status
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
12. <span data-ttu-id="a76c8-179">Добавьте следующий код в метод **Main** , чтобы получить состояние среза данных выходного набора данных.</span><span class="sxs-lookup"><span data-stu-id="a76c8-179">Add the following code to the **Main** method to get the status of a data slice of the output dataset.</span></span> <span data-ttu-id="a76c8-180">В этом примере ожидается только один срез.</span><span class="sxs-lookup"><span data-stu-id="a76c8-180">There is only one slice expected in this sample.</span></span>

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling the slice status");
        // wait before the next status check
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
13. <span data-ttu-id="a76c8-181">**(Необязательно.)** Добавьте в метод **Main** следующий код для получения сведений о выполнении для среза данных.</span><span class="sxs-lookup"><span data-stu-id="a76c8-181">**(optional)** Add the following code to get run details for a data slice to the **Main** method.</span></span>

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for the output slice to be ready
    Console.WriteLine("\nGive it a few minutes for the output slice to be ready and press any key.");
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
    
    Console.WriteLine("\nPress any key to exit.");
    Console.ReadKey();
    ```
14. <span data-ttu-id="a76c8-182">Добавьте следующий вспомогательный метод, используемый методом **Main**, в класс **Program**.</span><span class="sxs-lookup"><span data-stu-id="a76c8-182">Add the following helper method used by the **Main** method to the **Program** class.</span></span> <span data-ttu-id="a76c8-183">Этот метод выводит диалоговое окно, которое позволяет ввести **имя пользователя** и **пароль**, используемые для входа на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a76c8-183">This method pops a dialog box that that lets you provide **user name** and **password** that you use to log in to Azure portal.</span></span>

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

        throw new InvalidOperationException("Failed to acquire token");
    }
    ```

15. <span data-ttu-id="a76c8-184">В обозревателе решений разверните проект **DataFactoryAPITestApp**, щелкните правой кнопкой мыши **Ссылки**, а затем выберите **Добавить ссылку**.</span><span class="sxs-lookup"><span data-stu-id="a76c8-184">In the Solution Explorer, expand the project: **DataFactoryAPITestApp**, right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="a76c8-185">Установите флажок для сборки `System.Configuration` и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a76c8-185">Select check box for `System.Configuration` assembly and click **OK**.</span></span>
15. <span data-ttu-id="a76c8-186">Постройте консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="a76c8-186">Build the console application.</span></span> <span data-ttu-id="a76c8-187">В меню щелкните **Собрать** и выберите **Собрать решение**.</span><span class="sxs-lookup"><span data-stu-id="a76c8-187">Click **Build** on the menu and click **Build Solution**.</span></span>
16. <span data-ttu-id="a76c8-188">Убедитесь, что как минимум один файл существует в контейнере adftutorial в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="a76c8-188">Confirm that there is at least one file in the adftutorial container in your Azure blob storage.</span></span> <span data-ttu-id="a76c8-189">В противном случае создайте файл Emp.txt в блокноте со следующим содержимым и передайте его в контейнер adftutorial.</span><span class="sxs-lookup"><span data-stu-id="a76c8-189">If not, create Emp.txt file in Notepad with the following content and upload it to the adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
17. <span data-ttu-id="a76c8-190">Запустите пример, щелкнув **Отладка** -> **Начать отладку** в меню.</span><span class="sxs-lookup"><span data-stu-id="a76c8-190">Run the sample by clicking **Debug** -> **Start Debugging** on the menu.</span></span> <span data-ttu-id="a76c8-191">При появлении сообщения **Getting run details of a data slice** (Получение сведений о выполнении для среза данных) подождите несколько минут и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="a76c8-191">When you see the **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
18. <span data-ttu-id="a76c8-192">Перейдите на портал Azure и убедитесь, что фабрика данных **APITutorialFactory** создана с использованием следующих артефактов:</span><span class="sxs-lookup"><span data-stu-id="a76c8-192">Use the Azure portal to verify that the data factory **APITutorialFactory** is created with the following artifacts:</span></span>
    * <span data-ttu-id="a76c8-193">Связанная служба: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="a76c8-193">Linked service: **AzureStorageLinkedService**</span></span>
    * <span data-ttu-id="a76c8-194">Набор данных: **DatasetBlobSource** и **DatasetBlobDestination**.</span><span class="sxs-lookup"><span data-stu-id="a76c8-194">Dataset: **DatasetBlobSource** and **DatasetBlobDestination**.</span></span>
    * <span data-ttu-id="a76c8-195">Конвейер: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="a76c8-195">Pipeline: **PipelineBlobSample**</span></span>
19. <span data-ttu-id="a76c8-196">Убедитесь, что выходной файл создан в папке **apifactoryoutput** в контейнере **adftutorial**.</span><span class="sxs-lookup"><span data-stu-id="a76c8-196">Verify that an output file is created in the **apifactoryoutput** folder in the **adftutorial** container.</span></span>

## <a name="get-a-list-of-failed-data-slices"></a><span data-ttu-id="a76c8-197">Получение списка невыполненных срезов данных</span><span class="sxs-lookup"><span data-stu-id="a76c8-197">Get a list of failed data slices</span></span> 

```csharp
// Parse the resource path
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

## <a name="next-steps"></a><span data-ttu-id="a76c8-198">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a76c8-198">Next steps</span></span>
<span data-ttu-id="a76c8-199">Ниже приведен пример создания конвейера с использованием пакета SDK для .NET, который копирует данные из хранилища BLOB-объектов Azure в базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a76c8-199">See the following example for creating a pipeline using .NET SDK that copies data from an Azure blob storage to an Azure SQL database:</span></span> 

- [<span data-ttu-id="a76c8-200">Руководство. Создание конвейера с действием копирования с помощью API .NET</span><span class="sxs-lookup"><span data-stu-id="a76c8-200">Create a pipeline to copy data from Blob Storage to SQL Database</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
