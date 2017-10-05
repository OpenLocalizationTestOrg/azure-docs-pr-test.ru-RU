---
title: "Разработка Функций Azure с помощью служб мультимедиа"
description: "В этой статье описывается разработка Функций Azure с помощью служб мультимедиа на портале Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 51bdcb01-1846-4e1f-bd90-70020ab471b0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/21/2017
ms.author: juliako
ms.openlocfilehash: 35d539855572fef6c00de614a4e57738a8abd075
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
#<a name="develop-azure-functions-with-media-services"></a><span data-ttu-id="57092-103">Разработка Функций Azure с помощью служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="57092-103">Develop Azure Functions with Media Services</span></span>

<span data-ttu-id="57092-104">В этой статье описывается создание Функций Azure, использующих службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="57092-104">This topic shows you how to get started with creating Azure Functions that use Media Services.</span></span> <span data-ttu-id="57092-105">Функция Azure, определенная в этом разделе, отслеживает контейнер учетной записи хранения **input** на наличие новых MP4-файлов.</span><span class="sxs-lookup"><span data-stu-id="57092-105">The Azure Function defined in this topic monitors a storage account container named **input** for new MP4 files.</span></span> <span data-ttu-id="57092-106">После попадания файла в контейнер хранилища триггер большого двоичного объекта выполнит функцию.</span><span class="sxs-lookup"><span data-stu-id="57092-106">Once a file is dropped into the storage container, the blob trigger will execute the function.</span></span>

<span data-ttu-id="57092-107">Если вы хотите изучить и развернуть существующие службы "Функции Azure", использующие службы мультимедиа Azure, ознакомьтесь с [функциями Azure для служб мультимедиа](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="57092-107">If you want to explore and deploy existing Azure Functions that use Azure Media Services, check out [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span> <span data-ttu-id="57092-108">Этот репозиторий содержит примеры, которые используют службы мультимедиа, чтобы показать рабочие процессы, связанные с приемом содержимого напрямую от хранилища BLOB-объектов, шифрованием и записью содержимого обратно в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="57092-108">This repository contains examples that use Media Services to show workflows related to ingesting content directly from blob storage, encoding, and writing content back to blob storage.</span></span> <span data-ttu-id="57092-109">В нем также содержатся примеры отслеживания уведомлений заданий через объекты webhook и очереди Azure.</span><span class="sxs-lookup"><span data-stu-id="57092-109">It also includes examples of how to monitor job notifications via WebHooks and Azure Queues.</span></span> <span data-ttu-id="57092-110">Можно также разработать свои функции на основе примеров из репозитория [Функций Azure для служб мультимедиа](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="57092-110">You can also develop your Functions based on the examples in the [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repository.</span></span> <span data-ttu-id="57092-111">Для развертывания функций нажмите кнопку **Развертывание в Azure**.</span><span class="sxs-lookup"><span data-stu-id="57092-111">To deploy the functions, press the **Deploy to Azure** button.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57092-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="57092-112">Prerequisites</span></span>

- <span data-ttu-id="57092-113">Чтобы создавать функции, вам нужна активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="57092-113">Before you can create your first function, you need to have an active Azure account.</span></span> <span data-ttu-id="57092-114">Если у вас ее нет, воспользуйтесь [бесплатной учетной записью Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="57092-114">If you don't already have an Azure account, [free accounts are available](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="57092-115">Если вы хотите создать Функции Azure, которые выполняют определенные действия в учетной записи служб мультимедиа Azure (AMS) или прослушивают события, отправляемые службами мультимедиа, вам необходимо создать учетную запись AMS, следуя приведенным [здесь](media-services-portal-create-account.md) инструкциям.</span><span class="sxs-lookup"><span data-stu-id="57092-115">If you are going to create Azure Functions that perform actions on your Azure Media Services (AMS) account or listen to events sent by Media Services, you should create an AMS account, as described [here](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="57092-116">Общие сведения об [использовании Функций Azure](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="57092-116">Understanding of [how to use Azure functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="57092-117">Кроме того, ознакомьтесь со следующими разделами:</span><span class="sxs-lookup"><span data-stu-id="57092-117">Also, review:</span></span>
    - [<span data-ttu-id="57092-118">Привязки HTTP и webhook в функциях Azure</span><span class="sxs-lookup"><span data-stu-id="57092-118">Azure functions HTTP and webhook bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
    - [<span data-ttu-id="57092-119">Настройка параметров приложения-функции Azure</span><span class="sxs-lookup"><span data-stu-id="57092-119">How to configure Azure Function app settings</span></span>](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a><span data-ttu-id="57092-120">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="57092-120">Considerations</span></span>

-  <span data-ttu-id="57092-121">Функции Azure, стоимость которых рассчитывается, исходя из плана потребления, имеют ограничение времени ожидания 5 минут.</span><span class="sxs-lookup"><span data-stu-id="57092-121">Azure Functions running under the Consumption plan have 5 minutes timeout limit.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="57092-122">Создание приложения-функции</span><span class="sxs-lookup"><span data-stu-id="57092-122">Create a function app</span></span>

1. <span data-ttu-id="57092-123">Перейдите на [портал Azure](http://portal.azure.com) и войдите, используя свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="57092-123">Go to the [Azure portal](http://portal.azure.com) and sign-in with your Azure account.</span></span>
2. <span data-ttu-id="57092-124">Создайте приложение-функцию, как описано [здесь](../azure-functions/functions-create-function-app-portal.md).</span><span class="sxs-lookup"><span data-stu-id="57092-124">Create a function app as described [here](../azure-functions/functions-create-function-app-portal.md).</span></span>

>[!NOTE]
> <span data-ttu-id="57092-125">Учетная запись хранения, указанная в переменной среды **StorageConnection** (см. следующий шаг), должна находиться в том же регионе, что и ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="57092-125">A storage account that you specify in the **StorageConnection** environment variable (see the next step) should be in the same region as your app.</span></span>

## <a name="configure-function-app-settings"></a><span data-ttu-id="57092-126">Настройка параметров приложения-функции</span><span class="sxs-lookup"><span data-stu-id="57092-126">Configure function app settings</span></span>

<span data-ttu-id="57092-127">При разработке функций служб мультимедиа удобно добавить переменные среды, которые будут использоваться в функциях.</span><span class="sxs-lookup"><span data-stu-id="57092-127">When developing Media Services functions, it is handy to add environment variables that will be used throughout your functions.</span></span> <span data-ttu-id="57092-128">Чтобы настроить параметры приложения, щелкните ссылку "Настроить параметры приложения".</span><span class="sxs-lookup"><span data-stu-id="57092-128">To configure app settings, click the Configure App Settings link.</span></span> <span data-ttu-id="57092-129">Дополнительную информацию см. в разделе [Настройка параметров приложения-функции Azure](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span><span class="sxs-lookup"><span data-stu-id="57092-129">For more information, see  [How to configure Azure Function app settings](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span></span> 

<span data-ttu-id="57092-130">Например:</span><span class="sxs-lookup"><span data-stu-id="57092-130">For example:</span></span>

![Параметры](./media/media-services-azure-functions/media-services-azure-functions001.png)

<span data-ttu-id="57092-132">В функции, определенной в этой статье, предполагается, что в параметрах приложения настроены следующие переменные среды.</span><span class="sxs-lookup"><span data-stu-id="57092-132">The function, defined in this article, assumes you have the following environment variables in your app settings:</span></span>

<span data-ttu-id="57092-133">**AMSAccount**: *имя учетной записи AMS* (например, testams).</span><span class="sxs-lookup"><span data-stu-id="57092-133">**AMSAccount** : *AMS account name* (e.g. testams)</span></span>

<span data-ttu-id="57092-134">**AMSKey**: *ключ учетной записи AMS* (например, IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=).</span><span class="sxs-lookup"><span data-stu-id="57092-134">**AMSKey** : *AMS account key* (e.g. IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span></span>

<span data-ttu-id="57092-135">**MediaServicesStorageAccountName**: *имя учетной записи хранения* (например, testamsstorage).</span><span class="sxs-lookup"><span data-stu-id="57092-135">**MediaServicesStorageAccountName** : *storage account name* (e.g., testamsstorage)</span></span>

<span data-ttu-id="57092-136">**MediaServicesStorageAccountKey**: *ключ учетной записи хранения* (например, xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ или awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==).</span><span class="sxs-lookup"><span data-stu-id="57092-136">**MediaServicesStorageAccountKey** : *storage account key* (e.g., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span></span>

<span data-ttu-id="57092-137">**StorageConnection**: *подключения к хранилищу* (например, DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==).</span><span class="sxs-lookup"><span data-stu-id="57092-137">**StorageConnection** : *storage connection* (e.g., DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span></span>

## <a name="create-a-function"></a><span data-ttu-id="57092-138">Создание функции</span><span class="sxs-lookup"><span data-stu-id="57092-138">Create a function</span></span>

<span data-ttu-id="57092-139">После развертывания приложения-функции его можно найти в Функциях Azure **службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="57092-139">Once your function app is deployed, you can find it among **App Services** Azure Functions.</span></span>

1. <span data-ttu-id="57092-140">Выберите свое приложение-функцию и щелкните **Новая функция**.</span><span class="sxs-lookup"><span data-stu-id="57092-140">Select your function app and click **New Function**.</span></span>
2. <span data-ttu-id="57092-141">Выберите язык **C#** и сценарий **Обработка данных**.</span><span class="sxs-lookup"><span data-stu-id="57092-141">Choose the **C#** language and **Data Processing** scenario.</span></span>
3. <span data-ttu-id="57092-142">Выберите шаблон **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="57092-142">Choose **BlobTrigger** template.</span></span> <span data-ttu-id="57092-143">Эта функция активируется каждый раз, когда в контейнер **input** передается большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="57092-143">This function will be triggered whenever a blob is uploaded into the **input** container.</span></span> <span data-ttu-id="57092-144">На следующем шаге в **Path** указывается имя **input**.</span><span class="sxs-lookup"><span data-stu-id="57092-144">The **input** name is specified in the **Path**, in the next step.</span></span>

    ![файлов](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. <span data-ttu-id="57092-146">После выбора **BlobTrigger** на странице появится несколько дополнительных элементов управления.</span><span class="sxs-lookup"><span data-stu-id="57092-146">Once you select **BlobTrigger**, some more controls will appear on the page.</span></span>

    ![файлов](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. <span data-ttu-id="57092-148">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="57092-148">Click **Create**.</span></span> 


## <a name="files"></a><span data-ttu-id="57092-149">Файлы</span><span class="sxs-lookup"><span data-stu-id="57092-149">Files</span></span>

<span data-ttu-id="57092-150">Функция Azure связана с файлами кода и другими файлами, описание которых представлено в данной статье.</span><span class="sxs-lookup"><span data-stu-id="57092-150">Your Azure function is associated with code files and other files that are described in this section.</span></span> <span data-ttu-id="57092-151">По умолчанию она связана с файлами **function.json** и **run.csx** (C#).</span><span class="sxs-lookup"><span data-stu-id="57092-151">By default, a function is associated with **function.json** and **run.csx** (C#) files.</span></span> <span data-ttu-id="57092-152">Вам потребуется добавить файл **project.json**.</span><span class="sxs-lookup"><span data-stu-id="57092-152">You will need to add a **project.json** file.</span></span> <span data-ttu-id="57092-153">Ниже приведены определения этих файлов.</span><span class="sxs-lookup"><span data-stu-id="57092-153">The rest of this section shows the definitions for these files.</span></span>

![файлов](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a><span data-ttu-id="57092-155">function.json</span><span class="sxs-lookup"><span data-stu-id="57092-155">function.json</span></span>

<span data-ttu-id="57092-156">Файл function.json определяет привязки функций и другие параметры конфигурации.</span><span class="sxs-lookup"><span data-stu-id="57092-156">The function.json file defines the function bindings and other configuration settings.</span></span> <span data-ttu-id="57092-157">В среде выполнения этот файл используется для определения событий, которые необходимо отслеживать, и способа передачи данных в выполнение функции и возвращения данных из него.</span><span class="sxs-lookup"><span data-stu-id="57092-157">The runtime uses this file to determine the events to monitor and how to pass data into and return data from function execution.</span></span> <span data-ttu-id="57092-158">Дополнительные сведения см. в статье [Привязки HTTP и webhook в функциях Azure](../azure-functions/functions-reference.md#function-code).</span><span class="sxs-lookup"><span data-stu-id="57092-158">For more information, see [Azure functions HTTP and webhook bindings](../azure-functions/functions-reference.md#function-code).</span></span>

>[!NOTE]
><span data-ttu-id="57092-159">Чтобы функция не выполнялась, задайте для свойства **disabled** значение **true**.</span><span class="sxs-lookup"><span data-stu-id="57092-159">Set the **disabled** property to **true** to prevent the function from being executed.</span></span> 


<span data-ttu-id="57092-160">Ниже приведен пример файла **function.json**.</span><span class="sxs-lookup"><span data-stu-id="57092-160">Here is an example of **function.json** file.</span></span>

    {
    "bindings": [
      {
        "name": "myBlob",
        "type": "blobTrigger",
        "direction": "in",
        "path": "input/{fileName}.mp4",
        "connection": "StorageConnection"
      }
    ],
    "disabled": false
    }

### <a name="projectjson"></a><span data-ttu-id="57092-161">project.json</span><span class="sxs-lookup"><span data-stu-id="57092-161">project.json</span></span>

<span data-ttu-id="57092-162">Файл project.json содержит зависимости.</span><span class="sxs-lookup"><span data-stu-id="57092-162">The project.json file contains dependencies.</span></span> <span data-ttu-id="57092-163">Ниже приведен пример файла **project.json**, содержащего необходимые пакеты служб мультимедиа Azure для .NET из NuGet.</span><span class="sxs-lookup"><span data-stu-id="57092-163">Here is an example of **project.json** file that includes the required .NET Azure Media Services packages from Nuget.</span></span> <span data-ttu-id="57092-164">Обратите внимание, что номера версий изменятся после выпуска последних обновлений для пакетов, поэтому следует убедиться в наличии самых последних версий.</span><span class="sxs-lookup"><span data-stu-id="57092-164">Note that the version numbers will change with latest updates to the packages, so you should confirm the most recent versions.</span></span> 

    {
      "frameworks": {
        "net46":{
          "dependencies": {
        "windowsazure.mediaservices": "3.8.0.5",
        "windowsazure.mediaservices.extensions": "3.8.0.3"
          }
        }
       }
    }
    
### <a name="runcsx"></a><span data-ttu-id="57092-165">run.csx</span><span class="sxs-lookup"><span data-stu-id="57092-165">run.csx</span></span>

<span data-ttu-id="57092-166">Это код C# для функции.</span><span class="sxs-lookup"><span data-stu-id="57092-166">This is the C# code for your function.</span></span>  <span data-ttu-id="57092-167">Функция, определенная ниже, отслеживает контейнер учетной записи хранения **input** (который был указан в пути) на наличие новых MP4-файлов.</span><span class="sxs-lookup"><span data-stu-id="57092-167">The function defined below monitors a storage account container named **input** (that is what was specified in the path) for new MP4 files.</span></span> <span data-ttu-id="57092-168">После попадания файла в контейнер хранилища триггер большого двоичного объекта выполнит функцию.</span><span class="sxs-lookup"><span data-stu-id="57092-168">Once a file is dropped into the storage container, the blob trigger will execute the function.</span></span>
    
<span data-ttu-id="57092-169">В примере, определенном в этом разделе, демонстрируется,</span><span class="sxs-lookup"><span data-stu-id="57092-169">The example defined in this section demonstrates</span></span> 

1. <span data-ttu-id="57092-170">как принять ресурс в учетной записи служб мультимедиа (скопировать большой двоичный объект в ресурс AMS) и</span><span class="sxs-lookup"><span data-stu-id="57092-170">how to ingest an asset into a Media Services account (by coping a blob into an AMS asset) and</span></span> 
2. <span data-ttu-id="57092-171">как отправить задание кодирования, использующее предустановку Adaptive Streaming из Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="57092-171">how to submit an encoding job that uses Media Encoder Standard's "Adaptive Streaming" preset .</span></span>

<span data-ttu-id="57092-172">В реальном сценарии скорее всего потребуется отслеживать ход выполнения задания, а затем опубликовать закодированный ресурс.</span><span class="sxs-lookup"><span data-stu-id="57092-172">In the real life scenario, you most likely want to track job progress and then publish your encoded asset.</span></span> <span data-ttu-id="57092-173">Дополнительные сведения см. в статье [Использование объектов Webhook Azure для наблюдения за уведомлениями о заданиях служб мультимедиа с использованием .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="57092-173">For more information, see [Use Azure WebHooks to monitor Media Services job notifications](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> <span data-ttu-id="57092-174">Дополнительные примеры приведены в разделе [функций Azure для служб мультимедиа](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="57092-174">For more examples, see [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>  

<span data-ttu-id="57092-175">После определения функции щелкните **Сохранить и запустить**.</span><span class="sxs-lookup"><span data-stu-id="57092-175">Once you are done defining your function click **Save and Run**.</span></span>

    #r "Microsoft.WindowsAzure.Storage"
    #r "Newtonsoft.Json"
    #r "System.Web"

    using System;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Net;
    using System.Threading;
    using System.Threading.Tasks;
    using System.IO;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Auth;

    private static readonly string _mediaServicesAccountName = Environment.GetEnvironmentVariable("AMSAccount");
    private static readonly string _mediaServicesAccountKey = Environment.GetEnvironmentVariable("AMSKey");

    static string _storageAccountName = Environment.GetEnvironmentVariable("MediaServicesStorageAccountName");
    static string _storageAccountKey = Environment.GetEnvironmentVariable("MediaServicesStorageAccountKey");

    private static CloudStorageAccount _destinationStorageAccount = null;

    // Field for service context.
    private static CloudMediaContext _context = null;
    private static MediaServicesCredentials _cachedCredentials = null;

    public static void Run(CloudBlockBlob myBlob, string fileName, TraceWriter log)
    {
        // NOTE that the variables {fileName} here come from the path setting in function.json
        // and are passed into the  Run method signature above. We can use this to make decisions on what type of file
        // was dropped into the input container for the function. 

        // No need to do any Retry strategy in this function, By default, the SDK calls a function up to 5 times for a 
        // given blob. If the fifth try fails, the SDK adds a message to a queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache the Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used the chached credentials to create CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy the Blob into a new Input Asset for the Job
        // ***NOTE: Ideally we would have a method to ingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with the Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass to it the name of the 
        // processor to use for the specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with the encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify the input asset to be encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset to contain the results of the job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means the output asset is not encrypted. 
        task.OutputAssets.AddNew(fileName, AssetCreationOptions.None);

        job.Submit();
        log.Info("Job Submitted");

        }
        catch (Exception ex)
        {
        log.Error("ERROR: failed.");
        log.Info($"StackTrace : {ex.StackTrace}");
        throw ex;
        }
    }

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


    public static async Task<IAsset> CreateAssetFromBlob(CloudBlockBlob blob, string assetName, TraceWriter log){
        IAsset newAsset = null;

        try{
            Task<IAsset> copyAssetTask = CreateAssetFromBlobAsync(blob, assetName, log);
            newAsset = await copyAssetTask;
            log.Info($"Asset Copied : {newAsset.Id}");
        }
        catch(Exception ex){
            log.Info("Copy Failed");
            log.Info($"ERROR : {ex.Message}");
            throw ex;
        }

        return newAsset;
    }

    /// <summary>
    /// Creates a new asset and copies blobs from the specifed storage account.
    /// </summary>
    /// <param name="blob">The specified blob.</param>
    /// <returns>The new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference to the storage account that is associated with the Media Services account. 
        StorageCredentials mediaServicesStorageCredentials =
        new StorageCredentials(_storageAccountName, _storageAccountKey);
        _destinationStorageAccount = new CloudStorageAccount(mediaServicesStorageCredentials, false);

        // Create a new asset. 
        var asset = _context.Assets.Create(blob.Name, AssetCreationOptions.None);
        log.Info($"Created new asset {asset.Name}");

        IAccessPolicy writePolicy = _context.AccessPolicies.Create("writePolicy",
        TimeSpan.FromHours(4), AccessPermissions.Write);
        ILocator destinationLocator = _context.Locators.CreateLocator(LocatorType.Sas, asset, writePolicy);
        CloudBlobClient destBlobStorage = _destinationStorageAccount.CreateCloudBlobClient();

        // Get the destination asset container reference
        string destinationContainerName = (new Uri(destinationLocator.Path)).Segments[1];
        CloudBlobContainer assetContainer = destBlobStorage.GetContainerReference(destinationContainerName);

        try{
        assetContainer.CreateIfNotExists();
        }
        catch (Exception ex)
        {
        log.Error ("ERROR:" + ex.Message);
        }

        log.Info("Created asset.");

        // Get hold of the destination blob
        CloudBlockBlob destinationBlob = assetContainer.GetBlockBlobReference(blob.Name);

        // Copy Blob
        try
        {
        using (var stream = await blob.OpenReadAsync()) 
        {            
            await destinationBlob.UploadFromStreamAsync(stream);          
        }

        log.Info("Copy Complete.");

        var assetFile = asset.AssetFiles.Create(blob.Name);
        assetFile.ContentFileSize = blob.Properties.Length;
        assetFile.IsPrimary = true;
        assetFile.Update();
        asset.Update();
        }
        catch (Exception ex)
        {
        log.Error(ex.Message);
        log.Info (ex.StackTrace);
        log.Info ("Copy Failed.");
        throw;
        }

        destinationLocator.Delete();
        writePolicy.Delete();

        return asset;
    }
##<a name="test-your-function"></a><span data-ttu-id="57092-176">Тестирование функции</span><span class="sxs-lookup"><span data-stu-id="57092-176">Test your function</span></span>

<span data-ttu-id="57092-177">Чтобы протестировать функцию, необходимо передать MP4-файл в контейнер учетной записи хранения **input**, указанный в строке подключения.</span><span class="sxs-lookup"><span data-stu-id="57092-177">To test your function, you need to upload an MP4 file into the **input** container of the storage account that you specified in the connection string.</span></span>  

## <a name="next-step"></a><span data-ttu-id="57092-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="57092-178">Next step</span></span>

<span data-ttu-id="57092-179">На этом этапе вы готовы начать разработку приложения служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="57092-179">At this point, you are ready to start developing a Media Services application.</span></span> 
 
<span data-ttu-id="57092-180">Дополнительные сведения и полные примеры и решения на основе Функций Azure и Logic Apps с использованием служб мультимедиа Azure, предназначенные для создания рабочих процессов, создающих пользовательское содержимое, можно изучить на [примере интеграции Функций Azure и служб мультимедиа с помощью .NET, приведенном на сайте GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="57092-180">For more details and complete samples/solutions of using Azure Functions and Logic Apps with Azure Media Services to create custom content creation workflows, see the [Media Services .NET Functions Integraiton Sample on GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span></span>

<span data-ttu-id="57092-181">Кроме того, ознакомьтесь с разделом [Использование объектов Webhook Azure для наблюдения за уведомлениями о заданиях служб мультимедиа с использованием .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="57092-181">Also, see [Use Azure WebHooks to monitor Media Services job notifications with .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="57092-182">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="57092-182">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="57092-183">Отзывы</span><span class="sxs-lookup"><span data-stu-id="57092-183">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

