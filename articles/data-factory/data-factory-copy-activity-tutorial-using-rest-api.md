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
# <a name="tutorial-use-rest-api-toocreate-an-azure-data-factory-pipeline-toocopy-data"></a><span data-ttu-id="32eab-103">Учебник: Использование API-интерфейса REST toocreate данных toocopy конвейера фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="32eab-103">Tutorial: Use REST API toocreate an Azure Data Factory pipeline toocopy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="32eab-104">Обзор и предварительные требования</span><span class="sxs-lookup"><span data-stu-id="32eab-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="32eab-105">Мастер копирования</span><span class="sxs-lookup"><span data-stu-id="32eab-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="32eab-106">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="32eab-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="32eab-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="32eab-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="32eab-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="32eab-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="32eab-109">Шаблон Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="32eab-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="32eab-110">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="32eab-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="32eab-111">API .NET</span><span class="sxs-lookup"><span data-stu-id="32eab-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="32eab-112">В этой статье вы узнаете, как toouse REST API toocreate фабрики данных с конвейером, который копирует данные из базы данных Azure SQL tooan хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="32eab-112">In this article, you learn how toouse REST API toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="32eab-113">Если новый tooAzure фабрики данных, прочтите hello [tooAzure введение фабрики данных](data-factory-introduction.md) статьи, прежде чем выполнять задания этого учебника.</span><span class="sxs-lookup"><span data-stu-id="32eab-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="32eab-114">В этом руководстве описывается создание конвейера с одним действием — действием копирования.</span><span class="sxs-lookup"><span data-stu-id="32eab-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="32eab-115">Действие копирования Hello копирует данные из поддерживаемых хранилища tooa поддерживаемых приемник данных хранилищ данных.</span><span class="sxs-lookup"><span data-stu-id="32eab-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="32eab-116">Список хранилищ данных, которые поддерживаются в качестве источников и приемников, см. в разделе [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="32eab-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="32eab-117">Действие Hello выключен глобально доступной можно копировать данные между различными хранилищами данных в виде безопасные, надежные и масштабируемые службы.</span><span class="sxs-lookup"><span data-stu-id="32eab-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="32eab-118">Дополнительные сведения о действии копирования hello см. в разделе [действия перемещения данных](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="32eab-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="32eab-119">Конвейер может содержать сразу несколько действий.</span><span class="sxs-lookup"><span data-stu-id="32eab-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="32eab-120">Кроме того, можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия.</span><span class="sxs-lookup"><span data-stu-id="32eab-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="32eab-121">Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="32eab-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="32eab-122">Данная статья не охватывает все hello REST API фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="32eab-122">This article does not cover all hello Data Factory REST API.</span></span> <span data-ttu-id="32eab-123">Полную документацию по командлетам фабрики данных см. в [справочнике по REST API фабрики данных](/rest/api/datafactory/).</span><span class="sxs-lookup"><span data-stu-id="32eab-123">See [Data Factory REST API Reference](/rest/api/datafactory/) for comprehensive documentation on Data Factory cmdlets.</span></span>
>  
> <span data-ttu-id="32eab-124">конвейер данных Hello в этом учебнике копирует данные из источника данных хранилища tooa целевое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="32eab-124">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="32eab-125">Учебник о том, как tootransform данных, с помощью фабрики данных Azure, в разделе [учебника: построение конвейера анализа tootransform использование кластера Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="32eab-125">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32eab-126">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="32eab-126">Prerequisites</span></span>
* <span data-ttu-id="32eab-127">Выполните [Обзор учебника](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) и завершения hello **необходимого компонента** действия.</span><span class="sxs-lookup"><span data-stu-id="32eab-127">Go through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="32eab-128">Установите на компьютер программу [curl](https://curl.haxx.se/dlwiz/) .</span><span class="sxs-lookup"><span data-stu-id="32eab-128">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="32eab-129">Используйте средство перелистывание hello с toocreate команды REST фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="32eab-129">You use hello Curl tool with REST commands toocreate a data factory.</span></span> 
* <span data-ttu-id="32eab-130">Следуя инструкциям в [этой статье](../azure-resource-manager/resource-group-create-service-principal-portal.md) , выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="32eab-130">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span> 
  1. <span data-ttu-id="32eab-131">Создайте веб-приложение с именем **ADFCopyTutorialApp** в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="32eab-131">Create a Web application named **ADFCopyTutorialApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="32eab-132">Получите **идентификатор клиента** и **секретный ключ**.</span><span class="sxs-lookup"><span data-stu-id="32eab-132">Get **client ID** and **secret key**.</span></span> 
  3. <span data-ttu-id="32eab-133">Получите значение для **tenant_id**.</span><span class="sxs-lookup"><span data-stu-id="32eab-133">Get **tenant ID**.</span></span> 
  4. <span data-ttu-id="32eab-134">Назначить hello **ADFCopyTutorialApp** toohello приложения **участника фабрики данных** роли.</span><span class="sxs-lookup"><span data-stu-id="32eab-134">Assign hello **ADFCopyTutorialApp** application toohello **Data Factory Contributor** role.</span></span>  
* <span data-ttu-id="32eab-135">Установите [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="32eab-135">Install [Azure PowerShell](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="32eab-136">Запустите **PowerShell** и hello следующие действия.</span><span class="sxs-lookup"><span data-stu-id="32eab-136">Launch **PowerShell** and do hello following steps.</span></span> <span data-ttu-id="32eab-137">Не закрывайте Azure PowerShell до завершения этого учебника hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-137">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="32eab-138">Если закрыть и снова открыть понадобятся toorun hello команд.</span><span class="sxs-lookup"><span data-stu-id="32eab-138">If you close and reopen, you need toorun hello commands again.</span></span>
  
  1. <span data-ttu-id="32eab-139">Запустите следующую команду hello и введите hello имя пользователя и пароль, использовать toosign в toohello портала Azure:</span><span class="sxs-lookup"><span data-stu-id="32eab-139">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal:</span></span>
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. <span data-ttu-id="32eab-140">Выполните следующие команды tooview hello все hello подписки для этой учетной записи:</span><span class="sxs-lookup"><span data-stu-id="32eab-140">Run hello following command tooview all hello subscriptions for this account:</span></span>

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. <span data-ttu-id="32eab-141">Следующая команда tooselect hello подписки на toowork с выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-141">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="32eab-142">Замените  **&lt;NameOfAzureSubscription** &gt; с именем hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="32eab-142">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span> 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. <span data-ttu-id="32eab-143">Создание группы ресурсов Azure с именем **ADFTutorialResourceGroup** , выполнив следующую команду в hello PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="32eab-143">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell:</span></span>  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      <span data-ttu-id="32eab-144">Если группа ресурсов hello уже существует, укажите ли tooupdate его (Y) или сохранить его как (N).</span><span class="sxs-lookup"><span data-stu-id="32eab-144">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span> 
     
      <span data-ttu-id="32eab-145">Некоторые шаги hello в этом учебнике предполагается использовать ADFTutorialResourceGroup с именем группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-145">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="32eab-146">Если вы используете другой группе ресурсов, в этом учебнике требуется имя hello toouse вместо ADFTutorialResourceGroup группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="32eab-146">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="32eab-147">Создание определений JSON</span><span class="sxs-lookup"><span data-stu-id="32eab-147">Create JSON definitions</span></span>
<span data-ttu-id="32eab-148">Создайте следующие файлы JSON в папке hello, где находится curl.exe.</span><span class="sxs-lookup"><span data-stu-id="32eab-148">Create following JSON files in hello folder where curl.exe is located.</span></span> 

### <a name="datafactoryjson"></a><span data-ttu-id="32eab-149">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="32eab-149">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="32eab-150">Имя должно быть глобально уникальным, поэтому можно toomake ADFCopyTutorialDF tooprefix или суффикса его уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="32eab-150">Name must be globally unique, so you may want tooprefix/suffix ADFCopyTutorialDF toomake it a unique name.</span></span> 
> 
> 

```JSON
{  
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="32eab-151">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="32eab-151">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="32eab-152">Замените значения **accountname** и **accountkey** на имя вашей учетной записи хранения Azure и ее ключ.</span><span class="sxs-lookup"><span data-stu-id="32eab-152">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="32eab-153">toolearn tooget хранилищем доступом ключа, см. в разделе [ключи доступа Просмотр, копирование и повторное создание хранилища](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="32eab-153">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>

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

<span data-ttu-id="32eab-154">Дополнительные сведения о свойствах JSON см. в разделе [Связанная служба хранилища Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="32eab-154">For details about JSON properties, see [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span></span>

### <a name="azuersqllinkedservicejson"></a><span data-ttu-id="32eab-155">azuersqllinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="32eab-155">azuersqllinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="32eab-156">Замените **servername**, **databasename**, **username**, и **пароль** с именем сервера Azure SQL, имя базы данных SQL, пользователь Учетная запись и пароль для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-156">Replace **servername**, **databasename**, **username**, and **password** with name of your Azure SQL server, name of SQL database, user account, and password for hello account.</span></span>  
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

<span data-ttu-id="32eab-157">Дополнительные сведения о свойствах JSON см. в разделе [Свойства связанной службы](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="32eab-157">For details about JSON properties, see [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="32eab-158">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="32eab-158">inputdataset.json</span></span>

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

<span data-ttu-id="32eab-159">Hello следующей таблице содержатся описания свойств JSON hello, используемых в фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-159">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="32eab-160">Свойство</span><span class="sxs-lookup"><span data-stu-id="32eab-160">Property</span></span> | <span data-ttu-id="32eab-161">Описание</span><span class="sxs-lookup"><span data-stu-id="32eab-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="32eab-162">type</span><span class="sxs-lookup"><span data-stu-id="32eab-162">type</span></span> | <span data-ttu-id="32eab-163">Hello свойство type установлено слишком**AzureBlob** , так как данные находятся в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="32eab-163">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
| <span data-ttu-id="32eab-164">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="32eab-164">linkedServiceName</span></span> | <span data-ttu-id="32eab-165">Указывает toohello **AzureStorageLinkedService** , созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="32eab-165">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="32eab-166">folderPath</span><span class="sxs-lookup"><span data-stu-id="32eab-166">folderPath</span></span> | <span data-ttu-id="32eab-167">Указывает hello blob **контейнера** и hello **папки** , содержащий входного BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="32eab-167">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="32eab-168">В этом учебнике adftutorial — контейнер больших двоичных объектов hello и папка является корневой папкой hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-168">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
| <span data-ttu-id="32eab-169">fileName</span><span class="sxs-lookup"><span data-stu-id="32eab-169">fileName</span></span> | <span data-ttu-id="32eab-170">Это необязательное свойство.</span><span class="sxs-lookup"><span data-stu-id="32eab-170">This property is optional.</span></span> <span data-ttu-id="32eab-171">Если это свойство не указан, извлекаются все файлы из hello folderPath.</span><span class="sxs-lookup"><span data-stu-id="32eab-171">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="32eab-172">В этом учебнике **emp.txt** задается для hello имя файла, поэтому только этот файл будет выбрано для обработки.</span><span class="sxs-lookup"><span data-stu-id="32eab-172">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
| <span data-ttu-id="32eab-173">format -> type</span><span class="sxs-lookup"><span data-stu-id="32eab-173">format -> type</span></span> |<span data-ttu-id="32eab-174">Hello входной файл имеет текстовый формат hello, поэтому мы используем **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="32eab-174">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
| <span data-ttu-id="32eab-175">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="32eab-175">columnDelimiter</span></span> | <span data-ttu-id="32eab-176">Hello столбцов во входном файле hello разделяются **запятая (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="32eab-176">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
| <span data-ttu-id="32eab-177">frequency и interval</span><span class="sxs-lookup"><span data-stu-id="32eab-177">frequency/interval</span></span> | <span data-ttu-id="32eab-178">частота Hello задано слишком**час** и интервала задано слишком**1**, это означает, что hello ввода доступны срезы **каждый час**.</span><span class="sxs-lookup"><span data-stu-id="32eab-178">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="32eab-179">Другими словами, hello служба фабрики данных ищет входных данных каждый час в корневой папке hello контейнер больших двоичных объектов (**adftutorial**) было задано.</span><span class="sxs-lookup"><span data-stu-id="32eab-179">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="32eab-180">Выполняет поиск данных hello в hello конвейера начального и конечного времени, не до или после этих значений времени.</span><span class="sxs-lookup"><span data-stu-id="32eab-180">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
| <span data-ttu-id="32eab-181">external</span><span class="sxs-lookup"><span data-stu-id="32eab-181">external</span></span> | <span data-ttu-id="32eab-182">Это свойство задано слишком**true** Если hello данных в этом конвейере не создается.</span><span class="sxs-lookup"><span data-stu-id="32eab-182">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="32eab-183">в файле emp.txt hello, который создается в этом конвейере не, поэтому мы задали это свойство tootrue — Hello входных данных в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="32eab-183">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

<span data-ttu-id="32eab-184">Дополнительные сведения об этих свойствах JSON см. в [этом разделе](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="32eab-184">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>

### <a name="outputdatasetjson"></a><span data-ttu-id="32eab-185">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="32eab-185">outputdataset.json</span></span>

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
<span data-ttu-id="32eab-186">Hello следующей таблице содержатся описания свойств JSON hello, используемых в фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-186">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="32eab-187">Свойство</span><span class="sxs-lookup"><span data-stu-id="32eab-187">Property</span></span> | <span data-ttu-id="32eab-188">Описание</span><span class="sxs-lookup"><span data-stu-id="32eab-188">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="32eab-189">type</span><span class="sxs-lookup"><span data-stu-id="32eab-189">type</span></span> | <span data-ttu-id="32eab-190">Hello свойство type установлено слишком**AzureSqlTable** из-за данных скопированный tooa таблицы в базе данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="32eab-190">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
| <span data-ttu-id="32eab-191">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="32eab-191">linkedServiceName</span></span> | <span data-ttu-id="32eab-192">Указывает toohello **AzureSqlLinkedService** , созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="32eab-192">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="32eab-193">tableName</span><span class="sxs-lookup"><span data-stu-id="32eab-193">tableName</span></span> | <span data-ttu-id="32eab-194">Указанный hello **таблицы** toowhich hello данные копируются.</span><span class="sxs-lookup"><span data-stu-id="32eab-194">Specified hello **table** toowhich hello data is copied.</span></span> | 
| <span data-ttu-id="32eab-195">frequency и interval</span><span class="sxs-lookup"><span data-stu-id="32eab-195">frequency/interval</span></span> | <span data-ttu-id="32eab-196">Hello задана слишком**час** и интервал — **1**, это означает, что hello срезы выходных данных создаются **каждый час** между hello конвейера начала и время окончания, не до или После этих значений времени.</span><span class="sxs-lookup"><span data-stu-id="32eab-196">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

<span data-ttu-id="32eab-197">Имеются три столбца — **идентификатор**, **FirstName**, и **LastName** — в таблице emp hello в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-197">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="32eab-198">Идентификатор является столбцом идентификаторов, поэтому вам необходимо только toospecify **FirstName** и **LastName** здесь.</span><span class="sxs-lookup"><span data-stu-id="32eab-198">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

<span data-ttu-id="32eab-199">Дополнительные сведения об этих свойствах JSON см. в [этом разделе](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="32eab-199">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="32eab-200">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="32eab-200">pipeline.json</span></span>

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

<span data-ttu-id="32eab-201">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="32eab-201">Note hello following points:</span></span>

- <span data-ttu-id="32eab-202">В разделе "действия" hello, имеется только одно действие, **тип** задано слишком**копирования**.</span><span class="sxs-lookup"><span data-stu-id="32eab-202">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="32eab-203">Дополнительные сведения о действии копирования hello см. в разделе [действия перемещения данных](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="32eab-203">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="32eab-204">В решениях фабрики данных можно также использовать [действия преобразования данных](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="32eab-204">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
- <span data-ttu-id="32eab-205">Входных данных для действия hello установлено слишком**AzureBlobInput** и вывода для hello действия установлено слишком**AzureSqlOutput**.</span><span class="sxs-lookup"><span data-stu-id="32eab-205">Input for hello activity is set too**AzureBlobInput** and output for hello activity is set too**AzureSqlOutput**.</span></span> 
- <span data-ttu-id="32eab-206">В hello **typeProperties** разделе **BlobSource** указан в качестве типа источника hello и **SqlSink** указан как тип приемника hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-206">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="32eab-207">Перечень хранилищ данных, поддерживаемые действием копирования hello как источники и приемники см. в разделе [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="32eab-207">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="32eab-208">как сохранить toouse конкретных поддерживаемые данные в качестве источника и приемника, toolearn по ссылке hello в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-208">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
 
<span data-ttu-id="32eab-209">Замените значение hello hello **запустить** свойство с hello текущего дня и **окончания** значение с hello следующего дня.</span><span class="sxs-lookup"><span data-stu-id="32eab-209">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="32eab-210">Можно указать только часть даты hello и пропустить hello время hello Дата и время.</span><span class="sxs-lookup"><span data-stu-id="32eab-210">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="32eab-211">Например, «2017 г. 02-03-», который является эквивалентом "2017 г-02-03T00:00:00Z»</span><span class="sxs-lookup"><span data-stu-id="32eab-211">For example, "2017-02-03", which is equivalent too"2017-02-03T00:00:00Z"</span></span>
 
<span data-ttu-id="32eab-212">Даты начала и окончания должны быть в [формате ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="32eab-212">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="32eab-213">Например, 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="32eab-213">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="32eab-214">Hello **окончания** времени является необязательным, но мы используем в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="32eab-214">hello **end** time is optional, but we use it in this tutorial.</span></span> 
 
<span data-ttu-id="32eab-215">Если не указать значение для hello **окончания** свойство, оно вычисляется как «**start + 48 часов**».</span><span class="sxs-lookup"><span data-stu-id="32eab-215">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="32eab-216">конвейер hello toorun неопределенно долгое время, укажите **9999-09-09** как значение hello для hello **окончания** свойство.</span><span class="sxs-lookup"><span data-stu-id="32eab-216">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
 
<span data-ttu-id="32eab-217">В предыдущих пример hello существует 24 срезы данных, как каждый срез данных создается каждый час.</span><span class="sxs-lookup"><span data-stu-id="32eab-217">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

<span data-ttu-id="32eab-218">Описание свойств JSON в определении конвейера см. в статье [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="32eab-218">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="32eab-219">Описание свойств JSON в определении действия копирования см. в статье [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="32eab-219">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="32eab-220">Описание свойств JSON, поддерживаемых BlobSource, см. в статье о [соединителе больших двоичных объектов Azure](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="32eab-220">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="32eab-221">Описание свойств JSON, поддерживаемых SqlSink, см. в статье о [соединителе базы данных SQL Azure](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="32eab-221">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="set-global-variables"></a><span data-ttu-id="32eab-222">Настройка глобальных переменных</span><span class="sxs-lookup"><span data-stu-id="32eab-222">Set global variables</span></span>
<span data-ttu-id="32eab-223">Выполните следующие команды после замены значения hello собственные hello в Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="32eab-223">In Azure PowerShell, execute hello following commands after replacing hello values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="32eab-224">Инструкции по получению значений для параметров client_id, client_secret, tenant и subscription_id см. в разделе [Предварительные требования](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="32eab-224">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

<span data-ttu-id="32eab-225">Выполните следующую команду, после обновления hello имя фабрики данных hello, которую вы используете hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-225">Run hello following command after updating hello name of hello data factory you are using:</span></span> 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a><span data-ttu-id="32eab-226">Проверка подлинности с помощью AAD</span><span class="sxs-lookup"><span data-stu-id="32eab-226">Authenticate with AAD</span></span>
<span data-ttu-id="32eab-227">Выполнения hello следующая команда tooauthenticate с Azure Active Directory (AAD):</span><span class="sxs-lookup"><span data-stu-id="32eab-227">Run hello following command tooauthenticate with Azure Active Directory (AAD):</span></span> 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a><span data-ttu-id="32eab-228">Создание фабрики данных</span><span class="sxs-lookup"><span data-stu-id="32eab-228">Create data factory</span></span>
<span data-ttu-id="32eab-229">На этом шаге создается фабрика данных Azure с именем **ADFCopyTutorialDF**.</span><span class="sxs-lookup"><span data-stu-id="32eab-229">In this step, you create an Azure Data Factory named **ADFCopyTutorialDF**.</span></span> <span data-ttu-id="32eab-230">Фабрика данных может иметь один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="32eab-230">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="32eab-231">Конвейер может содержать одно или несколько действий.</span><span class="sxs-lookup"><span data-stu-id="32eab-231">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="32eab-232">Например хранилища данных toocopy действие копирования данных из источников tooa назначения.</span><span class="sxs-lookup"><span data-stu-id="32eab-232">For example, a Copy Activity toocopy data from a source tooa destination data store.</span></span> <span data-ttu-id="32eab-233">Toorun действие Hive в HDInsight tootransform скрипт Hive входных данных tooproduct выходных данных.</span><span class="sxs-lookup"><span data-stu-id="32eab-233">A HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="32eab-234">Выполните следующие hello данных команды toocreate фабрики hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-234">Run hello following commands toocreate hello data factory:</span></span> 

1. <span data-ttu-id="32eab-235">Назначить hello команды toovariable с именем **cmd**.</span><span class="sxs-lookup"><span data-stu-id="32eab-235">Assign hello command toovariable named **cmd**.</span></span> 
   
    > [!IMPORTANT]
    > <span data-ttu-id="32eab-236">Убедитесь, что hello имя фабрики данных hello, указанные здесь имя, указанное в hello hello совпадений (ADFCopyTutorialDF) **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="32eab-236">Confirm that hello name of hello data factory you specify here (ADFCopyTutorialDF) matches hello name specified in hello **datafactory.json**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. <span data-ttu-id="32eab-237">Команда hello с помощью **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="32eab-237">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="32eab-238">Просмотр результатов hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-238">View hello results.</span></span> <span data-ttu-id="32eab-239">Если hello фабрика данных успешно создана, вы видите hello JSON для фабрики данных hello в hello **результатов**; в противном случае отображается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="32eab-239">If hello data factory has been successfully created, you see hello JSON for hello data factory in hello **results**; otherwise, you see an error message.</span></span>  
   
    ```
    Write-Host $results
    ```

<span data-ttu-id="32eab-240">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="32eab-240">Note hello following points:</span></span>

* <span data-ttu-id="32eab-241">Имя Hello hello фабрики данных Azure должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="32eab-241">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="32eab-242">При возникновении ошибки hello в результатах: **имя фабрики данных «ADFCopyTutorialDF» недоступен**, hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="32eab-242">If you see hello error in results: **Data factory name “ADFCopyTutorialDF” is not available**, do hello following steps:</span></span>  
  
  1. <span data-ttu-id="32eab-243">Изменение имени hello (например, yournameADFCopyTutorialDF) в hello **datafactory.json** файла.</span><span class="sxs-lookup"><span data-stu-id="32eab-243">Change hello name (for example, yournameADFCopyTutorialDF) in hello **datafactory.json** file.</span></span>
  2. <span data-ttu-id="32eab-244">В первой команде hello Здравствуйте, где **$cmd** переменной присваивается значение, замените ADFCopyTutorialDF hello новое имя и выполните команду hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-244">In hello first command where hello **$cmd** variable is assigned a value, replace ADFCopyTutorialDF with hello new name and run hello command.</span></span> 
  3. <span data-ttu-id="32eab-245">Запуск hello следующие две команды tooinvoke hello API-интерфейса REST toocreate hello данных фабрики и печати hello результатов операции hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-245">Run hello next two commands tooinvoke hello REST API toocreate hello data factory and print hello results of hello operation.</span></span> 
     
     <span data-ttu-id="32eab-246">Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="32eab-246">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="32eab-247">экземпляры toocreate фабрики данных, необходимо toobe участника или администратор hello подписки Azure</span><span class="sxs-lookup"><span data-stu-id="32eab-247">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="32eab-248">Имя фабрики данных hello Hello может зарегистрирован как DNS-имя в будущем hello и поэтому становятся публично видимых.</span><span class="sxs-lookup"><span data-stu-id="32eab-248">hello name of hello data factory may be registered as a DNS name in hello future and hence become publicly visible.</span></span>
* <span data-ttu-id="32eab-249">Если ошибка hello: «**этой подписки не является пространством имен зарегистрированных toouse Microsoft.DataFactory**», выполните одно из следующих hello и повторите попытку публикации:</span><span class="sxs-lookup"><span data-stu-id="32eab-249">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span> 
  
  * <span data-ttu-id="32eab-250">В Azure PowerShell выполните hello, следующая команда tooregister hello фабрики данных поставщика.</span><span class="sxs-lookup"><span data-stu-id="32eab-250">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="32eab-251">Следующая команда tooconfirm hello можно запустить, hello зарегистрирован поставщик фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="32eab-251">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="32eab-252">Имя входа с помощью hello подписки Azure в hello [портал Azure](https://portal.azure.com) и перейдите в колонку tooa фабрики данных (или) создать фабрику данных в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="32eab-252">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="32eab-253">Это действие автоматически регистрирует поставщик hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-253">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="32eab-254">Перед созданием конвейера, необходимо toocreate несколько сущностей фабрики данных сначала.</span><span class="sxs-lookup"><span data-stu-id="32eab-254">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="32eab-255">Сначала создать связанные службы toolink источника и назначения данных сохраняет данные tooyour хранения.</span><span class="sxs-lookup"><span data-stu-id="32eab-255">You first create linked services toolink source and destination data stores tooyour data store.</span></span> <span data-ttu-id="32eab-256">Затем определите данных toorepresent наборы входных и выходных данных в хранилищах связанных данных.</span><span class="sxs-lookup"><span data-stu-id="32eab-256">Then, define input and output datasets toorepresent data in linked data stores.</span></span> <span data-ttu-id="32eab-257">Наконец создайте hello конвейера с действие, которое использует эти наборы данных.</span><span class="sxs-lookup"><span data-stu-id="32eab-257">Finally, create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="32eab-258">Создание связанных служб</span><span class="sxs-lookup"><span data-stu-id="32eab-258">Create linked services</span></span>
<span data-ttu-id="32eab-259">Создания связанных служб в toolink фабрики данных, хранит и вычислений фабрики данных toohello службы данных.</span><span class="sxs-lookup"><span data-stu-id="32eab-259">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="32eab-260">В этом руководстве не используются службы вычислений, например Azure HDInsight или Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="32eab-260">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="32eab-261">Вы используете два хранилища данных — служба хранилища Azure (источник) и база данных SQL Azure (конечное хранилище).</span><span class="sxs-lookup"><span data-stu-id="32eab-261">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> <span data-ttu-id="32eab-262">Поэтому нужно создать две связанные службы: служба хранилища Azure с именем AzureStorageLinkedService и база данных SQL Azure с именем AzureSqlLinkedService.</span><span class="sxs-lookup"><span data-stu-id="32eab-262">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="32eab-263">Hello AzureStorageLinkedService связывает фабрику данных toohello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="32eab-263">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="32eab-264">Эта учетная запись хранения является hello один в котором можно создать контейнер и загруженные данные hello в рамках [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="32eab-264">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="32eab-265">AzureSqlLinkedService связывает фабрику данных toohello базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="32eab-265">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="32eab-266">Hello данные, копируемые из хранилища больших двоичных объектов hello хранится в этой базе данных.</span><span class="sxs-lookup"><span data-stu-id="32eab-266">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="32eab-267">Создана таблица emp hello в этой базе данных как часть [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="32eab-267">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="32eab-268">Создание связанной службы хранения Azure</span><span class="sxs-lookup"><span data-stu-id="32eab-268">Create Azure Storage linked service</span></span>
<span data-ttu-id="32eab-269">На этом шаге связать фабрики данных tooyour учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="32eab-269">In this step, you link your Azure storage account tooyour data factory.</span></span> <span data-ttu-id="32eab-270">Укажите имя hello и ключ учетной записи хранилища Azure в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="32eab-270">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="32eab-271">В разделе [связанная служба хранилища Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) подробные сведения о JSON свойства, используемые toodefine связанная служба хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="32eab-271">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span>  

1. <span data-ttu-id="32eab-272">Назначить hello команды toovariable с именем **cmd**.</span><span class="sxs-lookup"><span data-stu-id="32eab-272">Assign hello command toovariable named **cmd**.</span></span> 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="32eab-273">Команда hello с помощью **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="32eab-273">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="32eab-274">Просмотр результатов hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-274">View hello results.</span></span> <span data-ttu-id="32eab-275">Если hello связаны была успешно создана служба см. в разделе hello JSON для службы hello связаны в hello **результатов**; в противном случае отображается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="32eab-275">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a><span data-ttu-id="32eab-276">Создание связанной службы SQL Azure</span><span class="sxs-lookup"><span data-stu-id="32eab-276">Create Azure SQL linked service</span></span>
<span data-ttu-id="32eab-277">На этом шаге связать фабрики данных tooyour базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="32eab-277">In this step, you link your Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="32eab-278">Укажите имя сервера Azure SQL hello, имя базы данных, имя пользователя и пароль пользователя в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="32eab-278">You specify hello Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="32eab-279">В разделе [связанная служба Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties) подробные сведения о JSON свойства, используемые toodefine связанная служба SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="32eab-279">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used toodefine an Azure SQL linked service.</span></span>

1. <span data-ttu-id="32eab-280">Назначить hello команды toovariable с именем **cmd**.</span><span class="sxs-lookup"><span data-stu-id="32eab-280">Assign hello command toovariable named **cmd**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="32eab-281">Команда hello с помощью **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="32eab-281">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="32eab-282">Просмотр результатов hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-282">View hello results.</span></span> <span data-ttu-id="32eab-283">Если hello связаны была успешно создана служба см. в разделе hello JSON для службы hello связаны в hello **результатов**; в противном случае отображается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="32eab-283">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="32eab-284">Создание наборов данных</span><span class="sxs-lookup"><span data-stu-id="32eab-284">Create datasets</span></span>
<span data-ttu-id="32eab-285">В предыдущем шаге hello создать связанные службы toolink вашей учетной записи хранилища Azure и фабрику данных tooyour базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="32eab-285">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="32eab-286">На этом шаге можно определить два набора данных с именем AzureBlobInput и AzureSqlOutput, представляющие входные данные и выходные данные, которые хранятся в хранилищах данных hello, на которые ссылается AzureStorageLinkedService и AzureSqlLinkedService соответственно.</span><span class="sxs-lookup"><span data-stu-id="32eab-286">In this step, you define two datasets named AzureBlobInput and AzureSqlOutput that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="32eab-287">Hello связанной службой хранилища Azure задает строку подключения hello, который использует служба фабрики данных во время выполнения tooconnect tooyour учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="32eab-287">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="32eab-288">И hello входного BLOB-объекта dataset (AzureBlobInput) указывает контейнер hello и hello папку, содержащую hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="32eab-288">And, hello input blob dataset (AzureBlobInput) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="32eab-289">Аналогичным образом hello связана база данных SQL Azure службы указывает hello строку подключения, использующее служба фабрики данных в базе данных Azure SQL tooyour tooconnect время выполнения.</span><span class="sxs-lookup"><span data-stu-id="32eab-289">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="32eab-290">И hello выходной набор данных таблицы SQL (OututDataset) указывает таблицу hello в hello базы данных toowhich hello и копирования данных из хранилища больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-290">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="32eab-291">Создание входного набора данных</span><span class="sxs-lookup"><span data-stu-id="32eab-291">Create input dataset</span></span>
<span data-ttu-id="32eab-292">На этом шаге создается набор данных с именем AzureBlobInput, который указывает файл tooa больших двоичных объектов (emp.txt) в корневой папке hello контейнер больших двоичных объектов (adftutorial) в hello представленный hello AzureStorageLinkedService связанной службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="32eab-292">In this step, you create a dataset named AzureBlobInput that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="32eab-293">Если не указать значение для имени файла hello (или пропустить его), данные из всех больших двоичных объектов в папке входной hello, скопированный toohello назначения.</span><span class="sxs-lookup"><span data-stu-id="32eab-293">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="32eab-294">В этом учебнике укажите значение для имени файла hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-294">In this tutorial, you specify a value for hello fileName.</span></span> 

1. <span data-ttu-id="32eab-295">Назначить hello команды toovariable с именем **cmd**.</span><span class="sxs-lookup"><span data-stu-id="32eab-295">Assign hello command toovariable named **cmd**.</span></span> 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="32eab-296">Команда hello с помощью **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="32eab-296">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="32eab-297">Просмотр результатов hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-297">View hello results.</span></span> <span data-ttu-id="32eab-298">Если набор данных hello успешно создана, вы видите hello JSON для набора данных hello в hello **результатов**; в противном случае отображается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="32eab-298">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="32eab-299">Создание выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="32eab-299">Create output dataset</span></span>
<span data-ttu-id="32eab-300">Hello базы данных SQL Azure связанные службы задает hello строку подключения, использующее служба фабрики данных в базе данных Azure SQL tooyour tooconnect время выполнения.</span><span class="sxs-lookup"><span data-stu-id="32eab-300">hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="32eab-301">Hello выходного SQL таблицы набора данных (OututDataset) на этом шаге создается указывает, что таблица hello в данных hello toowhich hello базы данных из хранилища больших двоичных объектов hello копируется.</span><span class="sxs-lookup"><span data-stu-id="32eab-301">hello output SQL table dataset (OututDataset) you create in this step specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>

1. <span data-ttu-id="32eab-302">Назначить hello команды toovariable с именем **cmd**.</span><span class="sxs-lookup"><span data-stu-id="32eab-302">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="32eab-303">Команда hello с помощью **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="32eab-303">Run hello command by using **Invoke-Command**.</span></span>
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="32eab-304">Просмотр результатов hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-304">View hello results.</span></span> <span data-ttu-id="32eab-305">Если набор данных hello успешно создана, вы видите hello JSON для набора данных hello в hello **результатов**; в противном случае отображается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="32eab-305">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a><span data-ttu-id="32eab-306">Создание конвейера</span><span class="sxs-lookup"><span data-stu-id="32eab-306">Create pipeline</span></span>
<span data-ttu-id="32eab-307">На этом шаге создается конвейер с **действием копирования**, которое использует **AzureBlobInput** в качестве входных данных и **AzureSqlOutput** в качестве выходных.</span><span class="sxs-lookup"><span data-stu-id="32eab-307">In this step, you create a pipeline with a **copy activity** that uses **AzureBlobInput** as an input and **AzureSqlOutput** as an output.</span></span>

<span data-ttu-id="32eab-308">В настоящее время выходной набор данных — того, какие диски hello расписания.</span><span class="sxs-lookup"><span data-stu-id="32eab-308">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="32eab-309">В этом учебнике выходной набор данных является настроенным tooproduce срез один раз в час.</span><span class="sxs-lookup"><span data-stu-id="32eab-309">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="32eab-310">конвейер Hello содержит время начала и время окончания, которые однажды друг от друга, что составляет 24 часа.</span><span class="sxs-lookup"><span data-stu-id="32eab-310">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="32eab-311">Таким образом 24 фрагменты выходной набор данных создают hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="32eab-311">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 

1. <span data-ttu-id="32eab-312">Назначить hello команды toovariable с именем **cmd**.</span><span class="sxs-lookup"><span data-stu-id="32eab-312">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="32eab-313">Команда hello с помощью **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="32eab-313">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="32eab-314">Просмотр результатов hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-314">View hello results.</span></span> <span data-ttu-id="32eab-315">Если набор данных hello успешно создана, вы видите hello JSON для набора данных hello в hello **результатов**; в противном случае отображается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="32eab-315">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>  

    ```PowerShell   
    Write-Host $results
    ```

<span data-ttu-id="32eab-316">**Поздравляем!**</span><span class="sxs-lookup"><span data-stu-id="32eab-316">**Congratulations!**</span></span> <span data-ttu-id="32eab-317">Успешно создана фабрикой данных Azure с конвейером, который копирует данные из базы данных SQL tooAzure хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="32eab-317">You have successfully created an Azure data factory, with a pipeline that copies data from Azure Blob Storage tooAzure SQL database.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="32eab-318">Отслеживание конвейера</span><span class="sxs-lookup"><span data-stu-id="32eab-318">Monitor pipeline</span></span>
<span data-ttu-id="32eab-319">На этом шаге используется фрагменты toomonitor REST API фабрики данных, получаемых hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="32eab-319">In this step, you use Data Factory REST API toomonitor slices being produced by hello pipeline.</span></span>

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> <span data-ttu-id="32eab-320">Убедитесь, что hello начального и конечного времени указано в hello следующая команда hello начало сопоставления времени и завершения hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="32eab-320">Make sure that hello start and end times specified in hello following command match hello start and end times of hello pipeline.</span></span> 

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

<span data-ttu-id="32eab-321">Запустить hello Invoke-Command и hello следующему пока не увидите срез в **готов** состояние или **сбой** состояния.</span><span class="sxs-lookup"><span data-stu-id="32eab-321">Run hello Invoke-Command and hello next one until you see a slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="32eab-322">Когда hello среза находится в состоянии готовности, проверьте hello **emp** таблицы в базе данных Azure SQL для hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="32eab-322">When hello slice is in Ready state, check hello **emp** table in your Azure SQL database for hello output data.</span></span> 

<span data-ttu-id="32eab-323">Для каждого среза двух строк данных из исходного файла hello, скопированный toohello emp таблицы в базе данных Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-323">For each slice, two rows of data from hello source file are copied toohello emp table in hello Azure SQL database.</span></span> <span data-ttu-id="32eab-324">Таким образом 24 новых записей в таблице emp hello появляется, если все срезы hello успешно обрабатываются (в состоянии готовности).</span><span class="sxs-lookup"><span data-stu-id="32eab-324">Therefore, you see 24 new records in hello emp table when all hello slices are successfully processed (in Ready state).</span></span> 

## <a name="summary"></a><span data-ttu-id="32eab-325">Сводка</span><span class="sxs-lookup"><span data-stu-id="32eab-325">Summary</span></span>
<span data-ttu-id="32eab-326">В этом учебнике используется API-интерфейса REST toocreate данных toocopy фабрики данных Azure, из базы данных Azure SQL tooan BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="32eab-326">In this tutorial, you used REST API toocreate an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="32eab-327">Ниже приведены hello высокоуровневые действия, выполняемые в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="32eab-327">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="32eab-328">Создание **фабрики данных Azure**.</span><span class="sxs-lookup"><span data-stu-id="32eab-328">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="32eab-329">Создание **связанных служб**.</span><span class="sxs-lookup"><span data-stu-id="32eab-329">Created **linked services**:</span></span>
   1. <span data-ttu-id="32eab-330">Хранилище Azure связан toolink службы учетной записи хранилища Azure, содержащий входные данные.</span><span class="sxs-lookup"><span data-stu-id="32eab-330">An Azure Storage linked service toolink your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="32eab-331">Azure SQL связанные службы toolink базы данных Azure SQL, которое содержит hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="32eab-331">An Azure SQL linked service toolink your Azure SQL database that holds hello output data.</span></span> 
3. <span data-ttu-id="32eab-332">Создание **наборов данных**, описывающих входные и выходные данные для конвейеров.</span><span class="sxs-lookup"><span data-stu-id="32eab-332">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="32eab-333">Создание **конвейера** с BlobSource в качестве источника и SqlSink в качестве приемника с помощью действия копирования.</span><span class="sxs-lookup"><span data-stu-id="32eab-333">Created a **pipeline** with a Copy Activity with BlobSource as source and SqlSink as sink.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="32eab-334">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="32eab-334">Next steps</span></span>
<span data-ttu-id="32eab-335">В этом руководстве в ходе операции копирования вы использовали хранилище BLOB-объектов Azure как исходное хранилище данных, а базу данных SQL Azure — как целевое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="32eab-335">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="32eab-336">Hello следующей таблице приведен список хранилищ данных, поддерживаемые действием копирования hello как источники и назначения:</span><span class="sxs-lookup"><span data-stu-id="32eab-336">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="32eab-337">toolearn о том, как хранилище данных toocopy из данных, щелкните ссылку hello hello хранилища данных в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="32eab-337">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
