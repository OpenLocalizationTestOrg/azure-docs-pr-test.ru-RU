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
ms.openlocfilehash: 30c7cd1ba455d7b1bc93d76e7ee79455bb52aae9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a><span data-ttu-id="6735c-103">Руководство. Создание конвейера с действием копирования с помощью API .NET</span><span class="sxs-lookup"><span data-stu-id="6735c-103">Tutorial: Create a pipeline with Copy Activity using .NET API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6735c-104">Обзор и предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6735c-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="6735c-105">Мастер копирования</span><span class="sxs-lookup"><span data-stu-id="6735c-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="6735c-106">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="6735c-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="6735c-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6735c-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="6735c-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6735c-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="6735c-109">Шаблон Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6735c-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="6735c-110">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="6735c-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="6735c-111">API .NET</span><span class="sxs-lookup"><span data-stu-id="6735c-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="6735c-112">В этом руководстве показано, как создать фабрику данных c конвейером, который копирует данные из хранилища BLOB-объектов Azure в базу данных SQL Azure, с помощью [.NET API](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6735c-112">In this article, you learn how to use [.NET API](https://portal.azure.com) to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="6735c-113">Если вы еще не работали с фабрикой данных Azure, перед выполнением действий, описанных в этом руководстве, ознакомьтесь со статьей [Введение в фабрику данных Azure](data-factory-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6735c-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="6735c-114">В этом руководстве описывается создание конвейера с одним действием — действием копирования.</span><span class="sxs-lookup"><span data-stu-id="6735c-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="6735c-115">Действие копирования копирует данные из поддерживаемого хранилища данных в поддерживаемое хранилище данных-приемник.</span><span class="sxs-lookup"><span data-stu-id="6735c-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="6735c-116">Список хранилищ данных, которые поддерживаются в качестве источников и приемников, см. в разделе [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="6735c-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="6735c-117">Это действие выполняется с помощью глобально доступной службы, обеспечивающей безопасное, надежное и масштабируемое копирование данных между разными хранилищами.</span><span class="sxs-lookup"><span data-stu-id="6735c-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="6735c-118">Дополнительные сведения о действии копирования см. в статье [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="6735c-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="6735c-119">Конвейер может содержать сразу несколько действий.</span><span class="sxs-lookup"><span data-stu-id="6735c-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="6735c-120">Два действия можно объединить в цепочку (выполнить одно действие вслед за другим), настроив выходной набор данных одного действия как входной набор данных другого действия.</span><span class="sxs-lookup"><span data-stu-id="6735c-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="6735c-121">Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="6735c-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="6735c-122">Полную документацию по .NET API для Data Factory см. в [Справочник по .NET API фабрики данных](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="6735c-122">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>
> 
> <span data-ttu-id="6735c-123">В этом руководстве конвейер данных копирует данные из исходного хранилища данных в целевое.</span><span class="sxs-lookup"><span data-stu-id="6735c-123">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="6735c-124">Инструкции по преобразованию данных с помощью фабрики данных Azure см. в [руководстве по созданию конвейера для преобразования данных с помощью кластера Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="6735c-124">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6735c-125">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6735c-125">Prerequisites</span></span>
* <span data-ttu-id="6735c-126">Ознакомьтесь с [обзором руководства](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) и выполните **предварительные требования** .</span><span class="sxs-lookup"><span data-stu-id="6735c-126">Go through [Tutorial Overview and Pre-requisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) to get an overview of the tutorial and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="6735c-127">Visual Studio 2012, 2013 или 2015</span><span class="sxs-lookup"><span data-stu-id="6735c-127">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="6735c-128">Скачайте и установите пакет [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="6735c-128">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span></span>
* <span data-ttu-id="6735c-129">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6735c-129">Azure PowerShell.</span></span> <span data-ttu-id="6735c-130">Далее, чтобы установить Azure PowerShell на локальном компьютере, следуйте указаниям в разделе [Установка и настройка Azure PowerShell](../powershell-install-configure.md) .</span><span class="sxs-lookup"><span data-stu-id="6735c-130">Follow instructions in [How to install and configure Azure PowerShell](../powershell-install-configure.md) article to install Azure PowerShell on your computer.</span></span> <span data-ttu-id="6735c-131">С помощью Azure PowerShell вы создадите приложение Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6735c-131">You use Azure PowerShell to create an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="6735c-132">Создание приложения в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6735c-132">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="6735c-133">Вы создадите приложение Azure Active Directory и субъект-службу для приложения, а затем назначите роль **Участник Data Factory** .</span><span class="sxs-lookup"><span data-stu-id="6735c-133">Create an Azure Active Directory application, create a service principal for the application, and assign it to the **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="6735c-134">Запустите **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="6735c-134">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="6735c-135">Выполните следующую команду и введите имя пользователя и пароль, которые используются для входа на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6735c-135">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="6735c-136">Выполните следующую команду, чтобы просмотреть все подписки для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6735c-136">Run the following command to view all the subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="6735c-137">Выполните следующую команду, чтобы выбрать подписку, с которой вы собираетесь работать.</span><span class="sxs-lookup"><span data-stu-id="6735c-137">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="6735c-138">Замените **&lt;NameOfAzureSubscription**&gt; именем своей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="6735c-138">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="6735c-139">Запишите значения **SubscriptionId** и **TenantId**, указанные в выходных данных этой команды.</span><span class="sxs-lookup"><span data-stu-id="6735c-139">Note down **SubscriptionId** and **TenantId** from the output of this command.</span></span>

5. <span data-ttu-id="6735c-140">Создайте группу ресурсов Azure с именем **ADFTutorialResourceGroup** , выполнив следующую команду в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6735c-140">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="6735c-141">Если группа ресурсов уже есть, укажите, требуется или не требуется ее обновить (Y или N соответственно).</span><span class="sxs-lookup"><span data-stu-id="6735c-141">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="6735c-142">Если вы используете другую группу ресурсов, укажите ее имя вместо ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="6735c-142">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="6735c-143">Создайте приложение Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6735c-143">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="6735c-144">Если возникнет следующая ошибка, укажите другой URL-адрес и запустите команду еще раз.</span><span class="sxs-lookup"><span data-stu-id="6735c-144">If you get the following error, specify a different URL and run the command again.</span></span>
    
    ```PowerShell
    Another object with the same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="6735c-145">Создайте субъект-службу AD.</span><span class="sxs-lookup"><span data-stu-id="6735c-145">Create the AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="6735c-146">Назначьте субъекту-службе роль **Участник Data Factory** .</span><span class="sxs-lookup"><span data-stu-id="6735c-146">Add service principal to the **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="6735c-147">Получите идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="6735c-147">Get the application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="6735c-148">Запишите идентификатор приложения (applicationID) из выходных данных.</span><span class="sxs-lookup"><span data-stu-id="6735c-148">Note down the application ID (applicationID) from the output.</span></span>

<span data-ttu-id="6735c-149">Вы должны получить следующие четыре значения:</span><span class="sxs-lookup"><span data-stu-id="6735c-149">You should have following four values from these steps:</span></span>

* <span data-ttu-id="6735c-150">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="6735c-150">Tenant ID</span></span>
* <span data-ttu-id="6735c-151">Идентификатор подписки</span><span class="sxs-lookup"><span data-stu-id="6735c-151">Subscription ID</span></span>
* <span data-ttu-id="6735c-152">Идентификатор приложения</span><span class="sxs-lookup"><span data-stu-id="6735c-152">Application ID</span></span>
* <span data-ttu-id="6735c-153">пароль (указан в первой команде).</span><span class="sxs-lookup"><span data-stu-id="6735c-153">Password (specified in the first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="6735c-154">Пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="6735c-154">Walkthrough</span></span>
1. <span data-ttu-id="6735c-155">С помощью Visual Studio 2012, 2013 или 2015 создайте консольное приложение C# .NET.</span><span class="sxs-lookup"><span data-stu-id="6735c-155">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="6735c-156">Запустите **Visual Studio** 2012, 2013 или 2015.</span><span class="sxs-lookup"><span data-stu-id="6735c-156">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="6735c-157">Щелкните **Файл**, наведите указатель мыши на пункт **Создать** и щелкните **Проект**.</span><span class="sxs-lookup"><span data-stu-id="6735c-157">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="6735c-158">Разверните раздел **Шаблоны** и выберите **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="6735c-158">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="6735c-159">В этом пошаговом руководстве используется C#, но можно использовать любой язык .NET.</span><span class="sxs-lookup"><span data-stu-id="6735c-159">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="6735c-160">Выберите **Консольное приложение** в списке типов проектов справа.</span><span class="sxs-lookup"><span data-stu-id="6735c-160">Select **Console Application** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="6735c-161">В качестве имени введите **DataFactoryAPITestApp** .</span><span class="sxs-lookup"><span data-stu-id="6735c-161">Enter **DataFactoryAPITestApp** for the Name.</span></span>
   6. <span data-ttu-id="6735c-162">В качестве расположения укажите **C:\ADFGetStarted**.</span><span class="sxs-lookup"><span data-stu-id="6735c-162">Select **C:\ADFGetStarted** for the Location.</span></span>
   7. <span data-ttu-id="6735c-163">Нажмите кнопку **ОК** , чтобы создать проект.</span><span class="sxs-lookup"><span data-stu-id="6735c-163">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="6735c-164">Щелкните **Инструменты**, наведите указатель мыши на **Диспетчер пакетов NuGet** и щелкните **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="6735c-164">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="6735c-165">В **консоли диспетчера пакетов** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="6735c-165">In the **Package Manager Console**, do the following steps:</span></span>
   1. <span data-ttu-id="6735c-166">Выполните следующую команду, чтобы установить пакет фабрики данных: `Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="6735c-166">Run the following command to install Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="6735c-167">Выполните следующую команду, чтобы установить пакет Azure Active Directory (используйте Active Directory API в коде): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="6735c-167">Run the following command to install Azure Active Directory package (you use Active Directory API in the code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="6735c-168">Добавьте следующий раздел **appSetttings** в файл **App.config**.</span><span class="sxs-lookup"><span data-stu-id="6735c-168">Add the following **appSetttings** section to the **App.config** file.</span></span> <span data-ttu-id="6735c-169">Эти параметры используются вспомогательным методом **GetAuthorizationHeader**.</span><span class="sxs-lookup"><span data-stu-id="6735c-169">These settings are used by the helper method: **GetAuthorizationHeader**.</span></span>

    <span data-ttu-id="6735c-170">Замените значения **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;** и **&lt;tenant ID&gt;** собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="6735c-170">Replace values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>

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

5. <span data-ttu-id="6735c-171">Добавьте следующие операторы **using** в файл исходного кода (Program.cs) в проекте.</span><span class="sxs-lookup"><span data-stu-id="6735c-171">Add the following **using** statements to the source file (Program.cs) in the project.</span></span>

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

6. <span data-ttu-id="6735c-172">Добавьте в метод **Main** приведенный ниже код, который создает экземпляр класса **DataPipelineManagementClient**.</span><span class="sxs-lookup"><span data-stu-id="6735c-172">Add the following code that creates an instance of **DataPipelineManagementClient** class to the **Main** method.</span></span> <span data-ttu-id="6735c-173">Этот объект используется не только для создания фабрики данных, связанной службы, входных и выходных наборов данных, а также конвейера,</span><span class="sxs-lookup"><span data-stu-id="6735c-173">You use this object to create a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="6735c-174">но и для отслеживания срезов набора данных при выполнении.</span><span class="sxs-lookup"><span data-stu-id="6735c-174">You also use this object to monitor slices of a dataset at runtime.</span></span>

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
   > <span data-ttu-id="6735c-175">Замените значение **resourceGroupName** именем своей группы ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="6735c-175">Replace the value of **resourceGroupName** with the name of your Azure resource group.</span></span>
   >
   > <span data-ttu-id="6735c-176">Измените имя фабрики данных (dataFactoryName) на уникальное.</span><span class="sxs-lookup"><span data-stu-id="6735c-176">Update name of the data factory (dataFactoryName) to be unique.</span></span> <span data-ttu-id="6735c-177">чтобы оно было глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="6735c-177">Name of the data factory must be globally unique.</span></span> <span data-ttu-id="6735c-178">Ознакомьтесь с разделом [Фабрика данных — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="6735c-178">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>

7. <span data-ttu-id="6735c-179">Добавьте следующий код, создающий **фабрику данных**, в метод **Main**.</span><span class="sxs-lookup"><span data-stu-id="6735c-179">Add the following code that creates a **data factory** to the **Main** method.</span></span>

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

    <span data-ttu-id="6735c-180">Фабрика данных может иметь один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="6735c-180">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="6735c-181">Конвейер может содержать одно или несколько действий.</span><span class="sxs-lookup"><span data-stu-id="6735c-181">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="6735c-182">Это может быть, например, действие копирования данных из исходного хранилища в целевое или действие HDInsight Hive для выполнения скрипта Hive, преобразующего входные данные в выходные данные продукта.</span><span class="sxs-lookup"><span data-stu-id="6735c-182">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="6735c-183">Начнем с создания фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="6735c-183">Let's start with creating the data factory in this step.</span></span>
8. <span data-ttu-id="6735c-184">Добавьте следующий код, который создает **связанную службу хранилища Azure**, в метод **Main**.</span><span class="sxs-lookup"><span data-stu-id="6735c-184">Add the following code that creates an **Azure Storage linked service** to the **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="6735c-185">Замените значения **storageaccountname** и **accountkey** именем и ключом вашей учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="6735c-185">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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

    <span data-ttu-id="6735c-186">Связанная служба в фабрике данных связывает хранилища данных и службы вычислений с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="6735c-186">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="6735c-187">В этом руководстве не используются службы вычислений, например Azure HDInsight или Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6735c-187">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="6735c-188">Вы используете два хранилища данных — служба хранилища Azure (источник) и база данных SQL Azure (конечное хранилище).</span><span class="sxs-lookup"><span data-stu-id="6735c-188">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

    <span data-ttu-id="6735c-189">Поэтому нужно создать две связанные службы: служба хранилища Azure с именем AzureStorageLinkedService и база данных SQL Azure с именем AzureSqlLinkedService.</span><span class="sxs-lookup"><span data-stu-id="6735c-189">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

    <span data-ttu-id="6735c-190">Связанная служба хранилища Azure связывает учетную запись хранения Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="6735c-190">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="6735c-191">В этой учетной записи хранения вы создали контейнер и отправили в нее данные в ходе выполнения предварительных [требований](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="6735c-191">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
9. <span data-ttu-id="6735c-192">Добавьте следующий код, который создает **связанную службу SQL Azure**, в метод **Main**.</span><span class="sxs-lookup"><span data-stu-id="6735c-192">Add the following code that creates an **Azure SQL linked service** to the **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="6735c-193">Укажите вместо **servername**, **databasename**, **username** и **password** имя своего сервера Azure SQL Server, имя базы данных, имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="6735c-193">Replace **servername**, **databasename**, **username**, and **password** with names of your Azure SQL server, database, user, and password.</span></span>

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

    <span data-ttu-id="6735c-194">Связанная служба SQL Azure связывает базу данных SQL Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="6735c-194">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="6735c-195">В этой базе данных хранятся данные, скопированные из хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="6735c-195">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="6735c-196">Вы создали пустую таблицу в этой базе данных в ходе выполнения [предварительных требований](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="6735c-196">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
10. <span data-ttu-id="6735c-197">Добавьте следующий код, создающий **входные и выходные наборы данных**, в метод **Main**.</span><span class="sxs-lookup"><span data-stu-id="6735c-197">Add the following code that creates **input and output datasets** to the **Main** method.</span></span>

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
    
    <span data-ttu-id="6735c-198">На предыдущем шаге вы создали связанные службы, связывающие учетную запись хранения Azure и базу данных SQL Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="6735c-198">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="6735c-199">На этом этапе вы определите два набора данных (InputDataset и OutputDataset), представляющие входные и выходные данные в хранилищах данных, на которые ссылаются службы AzureStorageLinkedService и AzureSqlLinkedService соответственно.</span><span class="sxs-lookup"><span data-stu-id="6735c-199">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

    <span data-ttu-id="6735c-200">Связанная служба хранилища Azure указывает строку подключения, которую фабрика данных использует во время выполнения, чтобы подключиться к учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="6735c-200">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="6735c-201">А входной набор данных больших двоичных объектов (InputDataset) определяет контейнер и папку с входными данными.</span><span class="sxs-lookup"><span data-stu-id="6735c-201">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span></span>  

    <span data-ttu-id="6735c-202">Аналогичным образом связанная служба базы данных SQL Azure указывает строку подключения, которую служба фабрики данных использует во время выполнения, чтобы подключиться к базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6735c-202">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="6735c-203">А выходной набор данных таблицы SQL (OututDataset) определяет таблицу в базе данных, в которую копируются данные из хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="6735c-203">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span>

    <span data-ttu-id="6735c-204">На этом этапе вы создадите набор данных с именем InputDataset. Он указывает на файл большого двоичного объекта (emp.txt) в корневой папке контейнера больших двоичных объектов в службе хранилища Azure, которая представлена связанной службой AzureStorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="6735c-204">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="6735c-205">Если не указать значение fileName (или пропустить его), данные из всех больших двоичных объектов в папке входных данных копируются в целевое расположение.</span><span class="sxs-lookup"><span data-stu-id="6735c-205">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="6735c-206">В этом руководстве вы укажете значение параметра fileName.</span><span class="sxs-lookup"><span data-stu-id="6735c-206">In this tutorial, you specify a value for the fileName.</span></span>    

    <span data-ttu-id="6735c-207">На этом этапе мы создадим выходной набор данных с именем **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="6735c-207">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="6735c-208">Этот набор данных указывает на таблицу SQL в базе данных SQL Azure (представлена значением **AzureSqlLinkedService**).</span><span class="sxs-lookup"><span data-stu-id="6735c-208">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService**.</span></span>
11. <span data-ttu-id="6735c-209">Добавьте следующий код, который **создает и активирует конвейер**, в метод **Main**.</span><span class="sxs-lookup"><span data-stu-id="6735c-209">Add the following code that **creates and activates a pipeline** to the **Main** method.</span></span> <span data-ttu-id="6735c-210">На этом этапе вы создадите конвейер с **действием копирования**, которое использует **InputDataset** в качестве входных данных и **OutputDataset** в качестве выходных.</span><span class="sxs-lookup"><span data-stu-id="6735c-210">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

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

                    // Initial value for pipeline's active period. With this, you won't need to set slice status
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

    <span data-ttu-id="6735c-211">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="6735c-211">Note the following points:</span></span>
   
    - <span data-ttu-id="6735c-212">В разделе действий доступно только одно действие, параметр **type** которого имеет значение **Copy**.</span><span class="sxs-lookup"><span data-stu-id="6735c-212">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="6735c-213">Дополнительные сведения о действии копирования см. в статье [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="6735c-213">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="6735c-214">В решениях фабрики данных можно также использовать [действия преобразования данных](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="6735c-214">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="6735c-215">Для этого действия параметру input присвоено значение **InputDataset**, а параметру output — значение **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="6735c-215">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> 
    - <span data-ttu-id="6735c-216">В разделе **typeProperties** в качестве типа источника указано **BlobSource**, а в качестве типа приемника — **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="6735c-216">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="6735c-217">Список хранилищ данных, поддерживаемых действием копирования в качестве источников и приемников, см. в разделе [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="6735c-217">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="6735c-218">Чтобы узнать, как использовать конкретное хранилище данных в качестве источника или приемника, щелкните ссылку в таблице.</span><span class="sxs-lookup"><span data-stu-id="6735c-218">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
   
    <span data-ttu-id="6735c-219">Сейчас на основе этого набора настраивается расписание.</span><span class="sxs-lookup"><span data-stu-id="6735c-219">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="6735c-220">В этом руководстве выходной набор данных создает срез раз в час.</span><span class="sxs-lookup"><span data-stu-id="6735c-220">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="6735c-221">Для конвейера настроено время начала и время окончания с разницей в сутки.</span><span class="sxs-lookup"><span data-stu-id="6735c-221">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="6735c-222">Таким образом, конвейер создает 24 среза для выходного набора данных.</span><span class="sxs-lookup"><span data-stu-id="6735c-222">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span>
12. <span data-ttu-id="6735c-223">Добавьте следующий код в метод **Main** , чтобы получить состояние среза данных выходного набора данных.</span><span class="sxs-lookup"><span data-stu-id="6735c-223">Add the following code to the **Main** method to get the status of a data slice of the output dataset.</span></span> <span data-ttu-id="6735c-224">Существует только срез, ожидаемый в этом образце.</span><span class="sxs-lookup"><span data-stu-id="6735c-224">There is only slice expected in this sample.</span></span>

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

13. <span data-ttu-id="6735c-225">Добавьте в метод **Main** следующий код, чтобы получить сведения о выполнении для среза данных.</span><span class="sxs-lookup"><span data-stu-id="6735c-225">Add the following code to get run details for a data slice to the **Main** method.</span></span>

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

    Console.WriteLine("\nPress any key to exit.");
    Console.ReadKey();
    ```

14. <span data-ttu-id="6735c-226">Добавьте следующий вспомогательный метод, используемый методом **Main**, в класс **Program**.</span><span class="sxs-lookup"><span data-stu-id="6735c-226">Add the following helper method used by the **Main** method to the **Program** class.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6735c-227">При копировании и вставке следующего кода убедитесь, что скопированный код находится на том же уровне, что и метод Main.</span><span class="sxs-lookup"><span data-stu-id="6735c-227">When you copy and paste the following code, make sure that the copied code is at the same level as the Main method.</span></span>

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

15. <span data-ttu-id="6735c-228">В обозревателе решений разверните проект (DataFactoryAPITestApp), щелкните правой кнопкой мыши **Ссылки**, а затем выберите **Добавить ссылку**.</span><span class="sxs-lookup"><span data-stu-id="6735c-228">In the Solution Explorer, expand the project (DataFactoryAPITestApp), right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="6735c-229">Установите флажок для сборки **System.Configuration**.</span><span class="sxs-lookup"><span data-stu-id="6735c-229">Select check box for **System.Configuration** assembly.</span></span> <span data-ttu-id="6735c-230">Затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6735c-230">and click **OK**.</span></span>
16. <span data-ttu-id="6735c-231">Постройте консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="6735c-231">Build the console application.</span></span> <span data-ttu-id="6735c-232">В меню щелкните **Собрать** и выберите **Собрать решение**.</span><span class="sxs-lookup"><span data-stu-id="6735c-232">Click **Build** on the menu and click **Build Solution**.</span></span>
17. <span data-ttu-id="6735c-233">Убедитесь, что в контейнере **adftutorial** в хранилище BLOB-объектов Azure есть как минимум один файл.</span><span class="sxs-lookup"><span data-stu-id="6735c-233">Confirm that there is at least one file in the **adftutorial** container in your Azure blob storage.</span></span> <span data-ttu-id="6735c-234">В противном случае создайте в блокноте файл **Emp.txt** со следующим содержимым, а затем отправьте его в контейнер adftutorial.</span><span class="sxs-lookup"><span data-stu-id="6735c-234">If not, create **Emp.txt** file in Notepad with the following content and upload it to the adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
18. <span data-ttu-id="6735c-235">Запустите пример, щелкнув **Отладка** -> **Начать отладку** в меню.</span><span class="sxs-lookup"><span data-stu-id="6735c-235">Run the sample by clicking **Debug** -> **Start Debugging** on the menu.</span></span> <span data-ttu-id="6735c-236">При появлении сообщения **Getting run details of a data slice** (Получение сведений о выполнении для среза данных) подождите несколько минут и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="6735c-236">When you see the **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
19. <span data-ttu-id="6735c-237">Перейдите на портал Azure и убедитесь, что фабрика данных **APITutorialFactory** создана с использованием следующих артефактов:</span><span class="sxs-lookup"><span data-stu-id="6735c-237">Use the Azure portal to verify that the data factory **APITutorialFactory** is created with the following artifacts:</span></span>
   * <span data-ttu-id="6735c-238">Связанная служба: **LinkedService_AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="6735c-238">Linked service: **LinkedService_AzureStorage**</span></span>
   * <span data-ttu-id="6735c-239">Набор данных: **InputDataset** и **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="6735c-239">Dataset: **InputDataset** and **OutputDataset**.</span></span>
   * <span data-ttu-id="6735c-240">Конвейер: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="6735c-240">Pipeline: **PipelineBlobSample**</span></span>
20. <span data-ttu-id="6735c-241">Убедитесь, что в таблице **emp** в указанной базе данных Azure SQL созданы две записи сотрудников.</span><span class="sxs-lookup"><span data-stu-id="6735c-241">Verify that the two employee records are created in the **emp** table in the specified Azure SQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6735c-242">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6735c-242">Next steps</span></span>
<span data-ttu-id="6735c-243">Полную документацию по .NET API для Data Factory см. в [Справочник по .NET API фабрики данных](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="6735c-243">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>

<span data-ttu-id="6735c-244">В этом руководстве в ходе операции копирования вы использовали хранилище BLOB-объектов Azure как исходное хранилище данных, а базу данных SQL Azure — как целевое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="6735c-244">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="6735c-245">В следующей таблице приведен список хранилищ данных, которые поддерживаются в качестве источников и целевых расположений для действия копирования.</span><span class="sxs-lookup"><span data-stu-id="6735c-245">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="6735c-246">Чтобы получить дополнительные сведения о том, как скопировать данные в хранилище данных или из него, щелкните ссылку для хранилища данных в таблице.</span><span class="sxs-lookup"><span data-stu-id="6735c-246">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>

