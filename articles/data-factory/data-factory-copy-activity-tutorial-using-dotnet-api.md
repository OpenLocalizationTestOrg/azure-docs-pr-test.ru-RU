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
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a><span data-ttu-id="55c69-103">Руководство. Создание конвейера с действием копирования с помощью API .NET</span><span class="sxs-lookup"><span data-stu-id="55c69-103">Tutorial: Create a pipeline with Copy Activity using .NET API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="55c69-104">Обзор и предварительные требования</span><span class="sxs-lookup"><span data-stu-id="55c69-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="55c69-105">Мастер копирования</span><span class="sxs-lookup"><span data-stu-id="55c69-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="55c69-106">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="55c69-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="55c69-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="55c69-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="55c69-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="55c69-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="55c69-109">Шаблон Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="55c69-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="55c69-110">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="55c69-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="55c69-111">API .NET</span><span class="sxs-lookup"><span data-stu-id="55c69-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="55c69-112">В этой статье вы узнаете, как toouse [.NET API](https://portal.azure.com) toocreate фабрики данных с конвейером, который копирует данные из базы данных Azure SQL tooan хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="55c69-112">In this article, you learn how toouse [.NET API](https://portal.azure.com) toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="55c69-113">Если новый tooAzure фабрики данных, прочтите hello [tooAzure введение фабрики данных](data-factory-introduction.md) статьи, прежде чем выполнять задания этого учебника.</span><span class="sxs-lookup"><span data-stu-id="55c69-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="55c69-114">В этом руководстве описывается создание конвейера с одним действием — действием копирования.</span><span class="sxs-lookup"><span data-stu-id="55c69-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="55c69-115">Действие копирования Hello копирует данные из поддерживаемых хранилища tooa поддерживаемых приемник данных хранилищ данных.</span><span class="sxs-lookup"><span data-stu-id="55c69-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="55c69-116">Список хранилищ данных, которые поддерживаются в качестве источников и приемников, см. в разделе [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="55c69-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="55c69-117">Действие Hello выключен глобально доступной можно копировать данные между различными хранилищами данных в виде безопасные, надежные и масштабируемые службы.</span><span class="sxs-lookup"><span data-stu-id="55c69-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="55c69-118">Дополнительные сведения о действии копирования hello см. в разделе [действия перемещения данных](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="55c69-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="55c69-119">Конвейер может содержать сразу несколько действий.</span><span class="sxs-lookup"><span data-stu-id="55c69-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="55c69-120">Кроме того, можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия.</span><span class="sxs-lookup"><span data-stu-id="55c69-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="55c69-121">Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="55c69-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="55c69-122">Полную документацию по .NET API для Data Factory см. в [Справочник по .NET API фабрики данных](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="55c69-122">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>
> 
> <span data-ttu-id="55c69-123">конвейер данных Hello в этом учебнике копирует данные из источника данных хранилища tooa целевое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="55c69-123">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="55c69-124">Учебник о том, как tootransform данных, с помощью фабрики данных Azure, в разделе [учебника: построение конвейера анализа tootransform использование кластера Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="55c69-124">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55c69-125">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="55c69-125">Prerequisites</span></span>
* <span data-ttu-id="55c69-126">Выполните [учебника Обзор и необходимые](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget Обзор учебника hello и завершения hello **необходимого компонента** действия.</span><span class="sxs-lookup"><span data-stu-id="55c69-126">Go through [Tutorial Overview and Pre-requisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget an overview of hello tutorial and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="55c69-127">Visual Studio 2012, 2013 или 2015</span><span class="sxs-lookup"><span data-stu-id="55c69-127">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="55c69-128">Скачайте и установите пакет [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="55c69-128">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span></span>
* <span data-ttu-id="55c69-129">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="55c69-129">Azure PowerShell.</span></span> <span data-ttu-id="55c69-130">Следуйте инструкциям в разделе [как tooinstall и настройка Azure PowerShell](../powershell-install-configure.md) статью tooinstall Azure PowerShell на компьютере.</span><span class="sxs-lookup"><span data-stu-id="55c69-130">Follow instructions in [How tooinstall and configure Azure PowerShell](../powershell-install-configure.md) article tooinstall Azure PowerShell on your computer.</span></span> <span data-ttu-id="55c69-131">Можно использовать Azure PowerShell toocreate приложение Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="55c69-131">You use Azure PowerShell toocreate an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="55c69-132">Создание приложения в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="55c69-132">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="55c69-133">Создать приложение Azure Active Directory, создать участника-службы для приложения hello и назначьте его toohello **участника фабрики данных** роли.</span><span class="sxs-lookup"><span data-stu-id="55c69-133">Create an Azure Active Directory application, create a service principal for hello application, and assign it toohello **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="55c69-134">Запустите **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="55c69-134">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="55c69-135">Запустите следующую команду hello и введите hello имя пользователя и пароль, использовать toosign в toohello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="55c69-135">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="55c69-136">Запустите следующие команды tooview hello все hello подписки для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="55c69-136">Run hello following command tooview all hello subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="55c69-137">Следующая команда tooselect hello подписки на toowork с выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="55c69-137">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="55c69-138">Замените  **&lt;NameOfAzureSubscription** &gt; с именем hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="55c69-138">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="55c69-139">Запишите **SubscriptionId** и **TenantId** hello в выходных данных этой команды.</span><span class="sxs-lookup"><span data-stu-id="55c69-139">Note down **SubscriptionId** and **TenantId** from hello output of this command.</span></span>

5. <span data-ttu-id="55c69-140">Создание группы ресурсов Azure с именем **ADFTutorialResourceGroup** , выполнив следующую команду в hello PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="55c69-140">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="55c69-141">Если группа ресурсов hello уже существует, укажите ли tooupdate его (Y) или сохранить его как (N).</span><span class="sxs-lookup"><span data-stu-id="55c69-141">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="55c69-142">Если вы используете другой группе ресурсов, в этом учебнике требуется имя hello toouse вместо ADFTutorialResourceGroup группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="55c69-142">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="55c69-143">Создайте приложение Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="55c69-143">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="55c69-144">Если появляется следующая ошибка hello, укажите другой URL-адрес и снова выполните команду hello.</span><span class="sxs-lookup"><span data-stu-id="55c69-144">If you get hello following error, specify a different URL and run hello command again.</span></span>
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="55c69-145">Создайте участника-службы AD hello.</span><span class="sxs-lookup"><span data-stu-id="55c69-145">Create hello AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="55c69-146">Добавление участника toohello службы **участника фабрики данных** роли.</span><span class="sxs-lookup"><span data-stu-id="55c69-146">Add service principal toohello **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="55c69-147">Получить идентификатор приложения hello.</span><span class="sxs-lookup"><span data-stu-id="55c69-147">Get hello application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="55c69-148">Запишите идентификатор приложения hello (applicationID) hello в выходных данных.</span><span class="sxs-lookup"><span data-stu-id="55c69-148">Note down hello application ID (applicationID) from hello output.</span></span>

<span data-ttu-id="55c69-149">Вы должны получить следующие четыре значения:</span><span class="sxs-lookup"><span data-stu-id="55c69-149">You should have following four values from these steps:</span></span>

* <span data-ttu-id="55c69-150">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="55c69-150">Tenant ID</span></span>
* <span data-ttu-id="55c69-151">Идентификатор подписки</span><span class="sxs-lookup"><span data-stu-id="55c69-151">Subscription ID</span></span>
* <span data-ttu-id="55c69-152">Идентификатор приложения</span><span class="sxs-lookup"><span data-stu-id="55c69-152">Application ID</span></span>
* <span data-ttu-id="55c69-153">Пароль (в первой команде hello)</span><span class="sxs-lookup"><span data-stu-id="55c69-153">Password (specified in hello first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="55c69-154">Пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="55c69-154">Walkthrough</span></span>
1. <span data-ttu-id="55c69-155">С помощью Visual Studio 2012, 2013 или 2015 создайте консольное приложение C# .NET.</span><span class="sxs-lookup"><span data-stu-id="55c69-155">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="55c69-156">Запустите **Visual Studio** 2012, 2013 или 2015.</span><span class="sxs-lookup"><span data-stu-id="55c69-156">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="55c69-157">Нажмите кнопку **файл**, слишком точки**New**и нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="55c69-157">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="55c69-158">Разверните раздел **Шаблоны** и выберите **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="55c69-158">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="55c69-159">В этом пошаговом руководстве используется C#, но можно использовать любой язык .NET.</span><span class="sxs-lookup"><span data-stu-id="55c69-159">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="55c69-160">Выберите **консольное приложение** hello списке типов проекта на hello вправо.</span><span class="sxs-lookup"><span data-stu-id="55c69-160">Select **Console Application** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="55c69-161">Введите **DataFactoryAPITestApp** для hello имя.</span><span class="sxs-lookup"><span data-stu-id="55c69-161">Enter **DataFactoryAPITestApp** for hello Name.</span></span>
   6. <span data-ttu-id="55c69-162">Выберите **C:\ADFGetStarted** для hello расположение.</span><span class="sxs-lookup"><span data-stu-id="55c69-162">Select **C:\ADFGetStarted** for hello Location.</span></span>
   7. <span data-ttu-id="55c69-163">Нажмите кнопку **ОК** toocreate hello проекта.</span><span class="sxs-lookup"><span data-stu-id="55c69-163">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="55c69-164">Нажмите кнопку **средства**, слишком точки**диспетчера пакетов NuGet**и нажмите кнопку **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="55c69-164">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="55c69-165">В hello **консоль диспетчера пакетов**, hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="55c69-165">In hello **Package Manager Console**, do hello following steps:</span></span>
   1. <span data-ttu-id="55c69-166">Выполните hello, следующая команда tooinstall фабрики данных пакета.`Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="55c69-166">Run hello following command tooinstall Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="55c69-167">Выполните hello, следующая команда tooinstall Azure Active Directory пакет (использовать Active Directory API в коде hello).`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="55c69-167">Run hello following command tooinstall Azure Active Directory package (you use Active Directory API in hello code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="55c69-168">Добавьте следующее hello **appSetttings** toohello раздел **App.config** файла.</span><span class="sxs-lookup"><span data-stu-id="55c69-168">Add hello following **appSetttings** section toohello **App.config** file.</span></span> <span data-ttu-id="55c69-169">Эти параметры используются hello вспомогательный метод: **GetAuthorizationHeader**.</span><span class="sxs-lookup"><span data-stu-id="55c69-169">These settings are used by hello helper method: **GetAuthorizationHeader**.</span></span>

    <span data-ttu-id="55c69-170">Замените значения **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;** и **&lt;tenant ID&gt;** собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="55c69-170">Replace values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>

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

5. <span data-ttu-id="55c69-171">Добавьте следующее hello **с помощью** toohello инструкций исходный файл (Program.cs) в проекте hello.</span><span class="sxs-lookup"><span data-stu-id="55c69-171">Add hello following **using** statements toohello source file (Program.cs) in hello project.</span></span>

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

6. <span data-ttu-id="55c69-172">Добавьте следующий код, который создает экземпляр hello **DataPipelineManagementClient** toohello класса **Main** метод.</span><span class="sxs-lookup"><span data-stu-id="55c69-172">Add hello following code that creates an instance of **DataPipelineManagementClient** class toohello **Main** method.</span></span> <span data-ttu-id="55c69-173">Этот объект toocreate используется фабрики данных, связанной службы, входные и выходные наборы данных и конвейера.</span><span class="sxs-lookup"><span data-stu-id="55c69-173">You use this object toocreate a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="55c69-174">Вы также использовать срезы toomonitor этот объект набора данных во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="55c69-174">You also use this object toomonitor slices of a dataset at runtime.</span></span>

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
   > <span data-ttu-id="55c69-175">Замените значение hello **resourceGroupName** с именем hello группы ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="55c69-175">Replace hello value of **resourceGroupName** with hello name of your Azure resource group.</span></span>
   >
   > <span data-ttu-id="55c69-176">Обновите hello данных фабрики (с именем dataFactoryName) toobe уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="55c69-176">Update name of hello data factory (dataFactoryName) toobe unique.</span></span> <span data-ttu-id="55c69-177">Имя фабрики данных hello должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="55c69-177">Name of hello data factory must be globally unique.</span></span> <span data-ttu-id="55c69-178">Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="55c69-178">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>

7. <span data-ttu-id="55c69-179">Добавьте следующий код, создающий hello **фабрики данных** toohello **Main** метод.</span><span class="sxs-lookup"><span data-stu-id="55c69-179">Add hello following code that creates a **data factory** toohello **Main** method.</span></span>

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

    <span data-ttu-id="55c69-180">Фабрика данных может иметь один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="55c69-180">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="55c69-181">Конвейер может содержать одно или несколько действий.</span><span class="sxs-lookup"><span data-stu-id="55c69-181">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="55c69-182">Например toocopy действие копирования данных из целевое хранилище данных источника tooa и toorun действие Hive в HDInsight tootransform скрипт Hive входных данных tooproduct выходных данных.</span><span class="sxs-lookup"><span data-stu-id="55c69-182">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="55c69-183">Давайте начнем с создания фабрики данных hello на этом шаге.</span><span class="sxs-lookup"><span data-stu-id="55c69-183">Let's start with creating hello data factory in this step.</span></span>
8. <span data-ttu-id="55c69-184">Добавьте следующий код, создающий hello **связанная служба хранилища Azure** toohello **Main** метод.</span><span class="sxs-lookup"><span data-stu-id="55c69-184">Add hello following code that creates an **Azure Storage linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="55c69-185">Замените значения **storageaccountname** и **accountkey** именем и ключом вашей учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="55c69-185">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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

    <span data-ttu-id="55c69-186">Создания связанных служб в toolink фабрики данных, хранит и вычислений фабрики данных toohello службы данных.</span><span class="sxs-lookup"><span data-stu-id="55c69-186">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="55c69-187">В этом руководстве не используются службы вычислений, например Azure HDInsight или Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="55c69-187">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="55c69-188">Вы используете два хранилища данных — служба хранилища Azure (источник) и база данных SQL Azure (конечное хранилище).</span><span class="sxs-lookup"><span data-stu-id="55c69-188">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

    <span data-ttu-id="55c69-189">Поэтому нужно создать две связанные службы: служба хранилища Azure с именем AzureStorageLinkedService и база данных SQL Azure с именем AzureSqlLinkedService.</span><span class="sxs-lookup"><span data-stu-id="55c69-189">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

    <span data-ttu-id="55c69-190">Hello AzureStorageLinkedService связывает фабрику данных toohello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="55c69-190">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="55c69-191">Эта учетная запись хранения является hello один в котором можно создать контейнер и загруженные данные hello в рамках [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="55c69-191">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
9. <span data-ttu-id="55c69-192">Добавьте следующий код, создающий hello **связанная служба Azure SQL** toohello **Main** метод.</span><span class="sxs-lookup"><span data-stu-id="55c69-192">Add hello following code that creates an **Azure SQL linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="55c69-193">Укажите вместо **servername**, **databasename**, **username** и **password** имя своего сервера Azure SQL Server, имя базы данных, имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="55c69-193">Replace **servername**, **databasename**, **username**, and **password** with names of your Azure SQL server, database, user, and password.</span></span>

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

    <span data-ttu-id="55c69-194">AzureSqlLinkedService связывает фабрику данных toohello базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="55c69-194">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="55c69-195">Hello данные, копируемые из хранилища больших двоичных объектов hello хранится в этой базе данных.</span><span class="sxs-lookup"><span data-stu-id="55c69-195">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="55c69-196">Создана таблица emp hello в этой базе данных как часть [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="55c69-196">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
10. <span data-ttu-id="55c69-197">Добавьте следующий код, создающий hello **наборы входных и выходных данных** toohello **Main** метод.</span><span class="sxs-lookup"><span data-stu-id="55c69-197">Add hello following code that creates **input and output datasets** toohello **Main** method.</span></span>

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
    
    <span data-ttu-id="55c69-198">В предыдущем шаге hello создать связанные службы toolink вашей учетной записи хранилища Azure и фабрику данных tooyour базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="55c69-198">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="55c69-199">На этом шаге можно определить два набора данных с именем InputDataset и OutputDataset, представляющие входные данные и выходные данные, которые хранятся в хранилищах данных hello, на которые ссылается AzureStorageLinkedService и AzureSqlLinkedService соответственно.</span><span class="sxs-lookup"><span data-stu-id="55c69-199">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

    <span data-ttu-id="55c69-200">Hello связанной службой хранилища Azure задает строку подключения hello, который использует служба фабрики данных во время выполнения tooconnect tooyour учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="55c69-200">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="55c69-201">И hello входного BLOB-объекта dataset (InputDataset) указывает контейнер hello и hello папку, содержащую hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="55c69-201">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="55c69-202">Аналогичным образом hello связана база данных SQL Azure службы указывает hello строку подключения, использующее служба фабрики данных в базе данных Azure SQL tooyour tooconnect время выполнения.</span><span class="sxs-lookup"><span data-stu-id="55c69-202">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="55c69-203">И hello выходной набор данных таблицы SQL (OututDataset) указывает таблицу hello в hello базы данных toowhich hello и копирования данных из хранилища больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="55c69-203">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>

    <span data-ttu-id="55c69-204">На этом шаге создается набор данных с именем InputDataset, который указывает файл tooa больших двоичных объектов (emp.txt) в корневой папке hello контейнер больших двоичных объектов (adftutorial) в hello представленный hello AzureStorageLinkedService связанной службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="55c69-204">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="55c69-205">Если не указать значение для имени файла hello (или пропустить его), данные из всех больших двоичных объектов в папке входной hello, скопированный toohello назначения.</span><span class="sxs-lookup"><span data-stu-id="55c69-205">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="55c69-206">В этом учебнике укажите значение для имени файла hello.</span><span class="sxs-lookup"><span data-stu-id="55c69-206">In this tutorial, you specify a value for hello fileName.</span></span>    

    <span data-ttu-id="55c69-207">На этом этапе мы создадим выходной набор данных с именем **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="55c69-207">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="55c69-208">Этот набор данных указывает tooa SQL таблицы в базе данных Azure SQL hello, представленного **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="55c69-208">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService**.</span></span>
11. <span data-ttu-id="55c69-209">Добавьте hello следующий код, чтобы **создает и активирует конвейера** toohello **Main** метод.</span><span class="sxs-lookup"><span data-stu-id="55c69-209">Add hello following code that **creates and activates a pipeline** toohello **Main** method.</span></span> <span data-ttu-id="55c69-210">На этом этапе вы создадите конвейер с **действием копирования**, которое использует **InputDataset** в качестве входных данных и **OutputDataset** в качестве выходных.</span><span class="sxs-lookup"><span data-stu-id="55c69-210">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

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

    <span data-ttu-id="55c69-211">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="55c69-211">Note hello following points:</span></span>
   
    - <span data-ttu-id="55c69-212">В разделе "действия" hello, имеется только одно действие, **тип** задано слишком**копирования**.</span><span class="sxs-lookup"><span data-stu-id="55c69-212">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="55c69-213">Дополнительные сведения о действии копирования hello см. в разделе [действия перемещения данных](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="55c69-213">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="55c69-214">В решениях фабрики данных можно также использовать [действия преобразования данных](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="55c69-214">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="55c69-215">Входных данных для действия hello установлено слишком**InputDataset** и вывода для hello действия установлено слишком**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="55c69-215">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="55c69-216">В hello **typeProperties** разделе **BlobSource** указан в качестве типа источника hello и **SqlSink** указан как тип приемника hello.</span><span class="sxs-lookup"><span data-stu-id="55c69-216">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="55c69-217">Перечень хранилищ данных, поддерживаемые действием копирования hello как источники и приемники см. в разделе [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="55c69-217">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="55c69-218">как сохранить toouse конкретных поддерживаемые данные в качестве источника и приемника, toolearn по ссылке hello в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="55c69-218">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
   
    <span data-ttu-id="55c69-219">В настоящее время выходной набор данных — того, какие диски hello расписания.</span><span class="sxs-lookup"><span data-stu-id="55c69-219">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="55c69-220">В этом учебнике выходной набор данных является настроенным tooproduce срез один раз в час.</span><span class="sxs-lookup"><span data-stu-id="55c69-220">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="55c69-221">конвейер Hello содержит время начала и время окончания, которые однажды друг от друга, что составляет 24 часа.</span><span class="sxs-lookup"><span data-stu-id="55c69-221">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="55c69-222">Таким образом 24 фрагменты выходной набор данных создают hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="55c69-222">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span>
12. <span data-ttu-id="55c69-223">Добавьте следующий код toohello hello **Main** метод tooget hello состояние срез данных hello выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="55c69-223">Add hello following code toohello **Main** method tooget hello status of a data slice of hello output dataset.</span></span> <span data-ttu-id="55c69-224">Существует только срез, ожидаемый в этом образце.</span><span class="sxs-lookup"><span data-stu-id="55c69-224">There is only slice expected in this sample.</span></span>

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

13. <span data-ttu-id="55c69-225">Добавьте приведенные ниже сведения tooget запустите код для фрагмента данных toohello hello **Main** метод.</span><span class="sxs-lookup"><span data-stu-id="55c69-225">Add hello following code tooget run details for a data slice toohello **Main** method.</span></span>

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

14. <span data-ttu-id="55c69-226">Добавьте следующий вспомогательный метод, используемый hello hello **Main** toohello метод **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="55c69-226">Add hello following helper method used by hello **Main** method toohello **Program** class.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="55c69-227">При копировании и вставке hello после кода, убедитесь в том, что hello скопированный код находится во hello же уровня как hello метода Main.</span><span class="sxs-lookup"><span data-stu-id="55c69-227">When you copy and paste hello following code, make sure that hello copied code is at hello same level as hello Main method.</span></span>

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

15. <span data-ttu-id="55c69-228">В hello в обозревателе решений разверните проект hello (DataFactoryAPITestApp), щелкните правой кнопкой мыши **ссылки**и нажмите кнопку **добавить ссылку**.</span><span class="sxs-lookup"><span data-stu-id="55c69-228">In hello Solution Explorer, expand hello project (DataFactoryAPITestApp), right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="55c69-229">Установите флажок для сборки **System.Configuration**.</span><span class="sxs-lookup"><span data-stu-id="55c69-229">Select check box for **System.Configuration** assembly.</span></span> <span data-ttu-id="55c69-230">Затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="55c69-230">and click **OK**.</span></span>
16. <span data-ttu-id="55c69-231">Построение консольного приложения hello.</span><span class="sxs-lookup"><span data-stu-id="55c69-231">Build hello console application.</span></span> <span data-ttu-id="55c69-232">Нажмите кнопку **построения** на hello меню и выберите пункт **построить решение**.</span><span class="sxs-lookup"><span data-stu-id="55c69-232">Click **Build** on hello menu and click **Build Solution**.</span></span>
17. <span data-ttu-id="55c69-233">Убедитесь, что установлен хотя бы один файл в hello **adftutorial** контейнера в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="55c69-233">Confirm that there is at least one file in hello **adftutorial** container in your Azure blob storage.</span></span> <span data-ttu-id="55c69-234">Если нет, создайте **Emp.txt** после содержимого hello-файл в Блокноте и отправьте его toohello adftutorial контейнера.</span><span class="sxs-lookup"><span data-stu-id="55c69-234">If not, create **Emp.txt** file in Notepad with hello following content and upload it toohello adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
18. <span data-ttu-id="55c69-235">Запуск образца hello, щелкнув **отладки** -> **начать отладку** в меню "hello".</span><span class="sxs-lookup"><span data-stu-id="55c69-235">Run hello sample by clicking **Debug** -> **Start Debugging** on hello menu.</span></span> <span data-ttu-id="55c69-236">При появлении hello **начало выполнения сведения о срез данных**, подождите несколько минут и нажмите клавишу **ввод**.</span><span class="sxs-lookup"><span data-stu-id="55c69-236">When you see hello **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
19. <span data-ttu-id="55c69-237">Используйте hello Azure портала tooverify этой фабрики данных hello **APITutorialFactory** создается с hello следующие артефакты:</span><span class="sxs-lookup"><span data-stu-id="55c69-237">Use hello Azure portal tooverify that hello data factory **APITutorialFactory** is created with hello following artifacts:</span></span>
   * <span data-ttu-id="55c69-238">Связанная служба: **LinkedService_AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="55c69-238">Linked service: **LinkedService_AzureStorage**</span></span>
   * <span data-ttu-id="55c69-239">Набор данных: **InputDataset** и **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="55c69-239">Dataset: **InputDataset** and **OutputDataset**.</span></span>
   * <span data-ttu-id="55c69-240">Конвейер: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="55c69-240">Pipeline: **PipelineBlobSample**</span></span>
20. <span data-ttu-id="55c69-241">Убедитесь, что записи сотрудников hello два создаются в hello **emp** указана таблица в hello базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="55c69-241">Verify that hello two employee records are created in hello **emp** table in hello specified Azure SQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55c69-242">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="55c69-242">Next steps</span></span>
<span data-ttu-id="55c69-243">Полную документацию по .NET API для Data Factory см. в [Справочник по .NET API фабрики данных](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="55c69-243">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>

<span data-ttu-id="55c69-244">В этом руководстве в ходе операции копирования вы использовали хранилище BLOB-объектов Azure как исходное хранилище данных, а базу данных SQL Azure — как целевое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="55c69-244">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="55c69-245">Hello следующей таблице приведен список хранилищ данных, поддерживаемые действием копирования hello как источники и назначения:</span><span class="sxs-lookup"><span data-stu-id="55c69-245">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="55c69-246">toolearn о том, как хранилище данных toocopy из данных, щелкните ссылку hello hello хранилища данных в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="55c69-246">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>

