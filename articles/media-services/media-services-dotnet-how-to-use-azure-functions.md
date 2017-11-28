---
title: "aaaDevelop функции Azure с помощью служб мультимедиа"
description: "В этом разделе показано, как toostart разработки Azure работают с помощью служб мультимедиа hello портал Azure."
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
ms.openlocfilehash: 3b2c2fb498fea399c862dfbdb63033d06cabf6d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
#<a name="develop-azure-functions-with-media-services"></a><span data-ttu-id="d4d5e-103">Разработка Функций Azure с помощью служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="d4d5e-103">Develop Azure Functions with Media Services</span></span>

<span data-ttu-id="d4d5e-104">В этом разделе показано, как tooget работу с создания функций Azure, использование служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-104">This topic shows you how tooget started with creating Azure Functions that use Media Services.</span></span> <span data-ttu-id="d4d5e-105">Hello Azure функцию, определенную в этом разделе отслеживает контейнер учетной записи хранилища с именем **ввода** для новых файлов MP4.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-105">hello Azure Function defined in this topic monitors a storage account container named **input** for new MP4 files.</span></span> <span data-ttu-id="d4d5e-106">После удаления файла в контейнер хранилища hello hello больших двоичных объектов будет выполняться триггер функции hello.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-106">Once a file is dropped into hello storage container, hello blob trigger will execute hello function.</span></span>

<span data-ttu-id="d4d5e-107">Извлечение tooexplore и развернуть существующих функций Azure, использование служб мультимедиа Azure, [функции Azure Media Services](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="d4d5e-107">If you want tooexplore and deploy existing Azure Functions that use Azure Media Services, check out [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span> <span data-ttu-id="d4d5e-108">Этот репозиторий содержит примеры использования служб мультимедиа tooshow рабочие процессы связанных tooingesting содержимого непосредственно из хранилища больших двоичных объектов, кодирования и записи содержимого резервное хранилище tooblob.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-108">This repository contains examples that use Media Services tooshow workflows related tooingesting content directly from blob storage, encoding, and writing content back tooblob storage.</span></span> <span data-ttu-id="d4d5e-109">Он также включает примеры как toomonitor задания уведомления через веб-перехватчиков и очереди Azure.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-109">It also includes examples of how toomonitor job notifications via WebHooks and Azure Queues.</span></span> <span data-ttu-id="d4d5e-110">Предусмотрена также возможность разрабатывать в виде примеров hello в hello функций [функции Azure Media Services](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) репозитория.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-110">You can also develop your Functions based on hello examples in hello [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repository.</span></span> <span data-ttu-id="d4d5e-111">функции hello toodeploy, нажмите клавишу hello **развертывание tooAzure** кнопки.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-111">toodeploy hello functions, press hello **Deploy tooAzure** button.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4d5e-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d4d5e-112">Prerequisites</span></span>

- <span data-ttu-id="d4d5e-113">Перед созданием первой функции, необходимо toohave активную учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-113">Before you can create your first function, you need toohave an active Azure account.</span></span> <span data-ttu-id="d4d5e-114">Если у вас ее нет, воспользуйтесь [бесплатной учетной записью Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="d4d5e-114">If you don't already have an Azure account, [free accounts are available](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="d4d5e-115">Если вы собираетесь функции toocreate Azure, выполнять действия в вашей учетной записи служб мультимедиа Azure (AMS) или прослушивания tooevents, отправленные службами мультимедиа, следует создать учетную запись AMS, как описано [здесь](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="d4d5e-115">If you are going toocreate Azure Functions that perform actions on your Azure Media Services (AMS) account or listen tooevents sent by Media Services, you should create an AMS account, as described [here](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="d4d5e-116">Понимание [как toouse Azure функции](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d4d5e-116">Understanding of [how toouse Azure functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="d4d5e-117">Кроме того, ознакомьтесь со следующими разделами:</span><span class="sxs-lookup"><span data-stu-id="d4d5e-117">Also, review:</span></span>
    - [<span data-ttu-id="d4d5e-118">Привязки HTTP и webhook в функциях Azure</span><span class="sxs-lookup"><span data-stu-id="d4d5e-118">Azure functions HTTP and webhook bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
    - [<span data-ttu-id="d4d5e-119">Как параметры приложения Azure функция tooconfigure</span><span class="sxs-lookup"><span data-stu-id="d4d5e-119">How tooconfigure Azure Function app settings</span></span>](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a><span data-ttu-id="d4d5e-120">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="d4d5e-120">Considerations</span></span>

-  <span data-ttu-id="d4d5e-121">Функции Azure, выполняемых в рамках плана потребления hello имеют ограничения времени ожидания 5 минут.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-121">Azure Functions running under hello Consumption plan have 5 minutes timeout limit.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="d4d5e-122">Создание приложения-функции</span><span class="sxs-lookup"><span data-stu-id="d4d5e-122">Create a function app</span></span>

1. <span data-ttu-id="d4d5e-123">Go toohello [портал Azure](http://portal.azure.com) и войдите с учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-123">Go toohello [Azure portal](http://portal.azure.com) and sign-in with your Azure account.</span></span>
2. <span data-ttu-id="d4d5e-124">Создайте приложение-функцию, как описано [здесь](../azure-functions/functions-create-function-app-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d4d5e-124">Create a function app as described [here](../azure-functions/functions-create-function-app-portal.md).</span></span>

>[!NOTE]
> <span data-ttu-id="d4d5e-125">Учетная запись хранения, указанной в hello **StorageConnection** переменной среды (см. следующий шаг hello) должны находиться в hello же регионе, что ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-125">A storage account that you specify in hello **StorageConnection** environment variable (see hello next step) should be in hello same region as your app.</span></span>

## <a name="configure-function-app-settings"></a><span data-ttu-id="d4d5e-126">Настройка параметров приложения-функции</span><span class="sxs-lookup"><span data-stu-id="d4d5e-126">Configure function app settings</span></span>

<span data-ttu-id="d4d5e-127">При разработке функций служб мультимедиа, бывает удобно tooadd переменные среды, которые будут использоваться во всей функции.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-127">When developing Media Services functions, it is handy tooadd environment variables that will be used throughout your functions.</span></span> <span data-ttu-id="d4d5e-128">Параметры приложения tooconfigure, щелкните ссылку настроить параметры приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-128">tooconfigure app settings, click hello Configure App Settings link.</span></span> <span data-ttu-id="d4d5e-129">Дополнительные сведения см. в разделе [как параметры приложения Azure функция tooconfigure](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span><span class="sxs-lookup"><span data-stu-id="d4d5e-129">For more information, see  [How tooconfigure Azure Function app settings](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span></span> 

<span data-ttu-id="d4d5e-130">Например:</span><span class="sxs-lookup"><span data-stu-id="d4d5e-130">For example:</span></span>

![данных](./media/media-services-azure-functions/media-services-azure-functions001.png)

<span data-ttu-id="d4d5e-132">функции Hello, определенные в этой статье предполагается, что у вас есть следующие переменные среды в параметрах приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-132">hello function, defined in this article, assumes you have hello following environment variables in your app settings:</span></span>

<span data-ttu-id="d4d5e-133">**AMSAccount**: *имя учетной записи AMS* (например, testams).</span><span class="sxs-lookup"><span data-stu-id="d4d5e-133">**AMSAccount** : *AMS account name* (e.g. testams)</span></span>

<span data-ttu-id="d4d5e-134">**AMSKey**: *ключ учетной записи AMS* (например, IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=).</span><span class="sxs-lookup"><span data-stu-id="d4d5e-134">**AMSKey** : *AMS account key* (e.g. IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span></span>

<span data-ttu-id="d4d5e-135">**MediaServicesStorageAccountName**: *имя учетной записи хранения* (например, testamsstorage).</span><span class="sxs-lookup"><span data-stu-id="d4d5e-135">**MediaServicesStorageAccountName** : *storage account name* (e.g., testamsstorage)</span></span>

<span data-ttu-id="d4d5e-136">**MediaServicesStorageAccountKey**: *ключ учетной записи хранения* (например, xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ или awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==).</span><span class="sxs-lookup"><span data-stu-id="d4d5e-136">**MediaServicesStorageAccountKey** : *storage account key* (e.g., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span></span>

<span data-ttu-id="d4d5e-137">**StorageConnection**: *подключения к хранилищу* (например, DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==).</span><span class="sxs-lookup"><span data-stu-id="d4d5e-137">**StorageConnection** : *storage connection* (e.g., DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span></span>

## <a name="create-a-function"></a><span data-ttu-id="d4d5e-138">Создание функции</span><span class="sxs-lookup"><span data-stu-id="d4d5e-138">Create a function</span></span>

<span data-ttu-id="d4d5e-139">После развертывания приложения-функции его можно найти в Функциях Azure **службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-139">Once your function app is deployed, you can find it among **App Services** Azure Functions.</span></span>

1. <span data-ttu-id="d4d5e-140">Выберите свое приложение-функцию и щелкните **Новая функция**.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-140">Select your function app and click **New Function**.</span></span>
2. <span data-ttu-id="d4d5e-141">Выберите hello **C#** языка и **обработки данных** сценария.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-141">Choose hello **C#** language and **Data Processing** scenario.</span></span>
3. <span data-ttu-id="d4d5e-142">Выберите шаблон **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-142">Choose **BlobTrigger** template.</span></span> <span data-ttu-id="d4d5e-143">Эта функция будет применяться всякий раз, когда большой двоичный объект загружается в hello **ввода** контейнера.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-143">This function will be triggered whenever a blob is uploaded into hello **input** container.</span></span> <span data-ttu-id="d4d5e-144">Hello **ввода** имя задается в hello **путь**, в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-144">hello **input** name is specified in hello **Path**, in hello next step.</span></span>

    ![файлов](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. <span data-ttu-id="d4d5e-146">После выбора **BlobTrigger**, некоторые дополнительные элементы управления будут отображаться на странице приветствия.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-146">Once you select **BlobTrigger**, some more controls will appear on hello page.</span></span>

    ![файлов](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. <span data-ttu-id="d4d5e-148">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-148">Click **Create**.</span></span> 


## <a name="files"></a><span data-ttu-id="d4d5e-149">Файлы</span><span class="sxs-lookup"><span data-stu-id="d4d5e-149">Files</span></span>

<span data-ttu-id="d4d5e-150">Функция Azure связана с файлами кода и другими файлами, описание которых представлено в данной статье.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-150">Your Azure function is associated with code files and other files that are described in this section.</span></span> <span data-ttu-id="d4d5e-151">По умолчанию она связана с файлами **function.json** и **run.csx** (C#).</span><span class="sxs-lookup"><span data-stu-id="d4d5e-151">By default, a function is associated with **function.json** and **run.csx** (C#) files.</span></span> <span data-ttu-id="d4d5e-152">Вам потребуется tooadd **project.json** файла.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-152">You will need tooadd a **project.json** file.</span></span> <span data-ttu-id="d4d5e-153">Hello оставшейся части этого раздела показаны hello определения для этих файлов.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-153">hello rest of this section shows hello definitions for these files.</span></span>

![файлов](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a><span data-ttu-id="d4d5e-155">function.json</span><span class="sxs-lookup"><span data-stu-id="d4d5e-155">function.json</span></span>

<span data-ttu-id="d4d5e-156">файл function.json Hello определяет привязки функций hello и других параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-156">hello function.json file defines hello function bindings and other configuration settings.</span></span> <span data-ttu-id="d4d5e-157">Hello среды выполнения использует этот файл toodetermine hello события toomonitor и функционировать как toopass и возврат данных из выполнения.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-157">hello runtime uses this file toodetermine hello events toomonitor and how toopass data into and return data from function execution.</span></span> <span data-ttu-id="d4d5e-158">Дополнительные сведения см. в статье [Привязки HTTP и webhook в функциях Azure](../azure-functions/functions-reference.md#function-code).</span><span class="sxs-lookup"><span data-stu-id="d4d5e-158">For more information, see [Azure functions HTTP and webhook bindings](../azure-functions/functions-reference.md#function-code).</span></span>

>[!NOTE]
><span data-ttu-id="d4d5e-159">Набор hello **отключено** свойство слишком**true** функции hello tooprevent выполнение.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-159">Set hello **disabled** property too**true** tooprevent hello function from being executed.</span></span> 


<span data-ttu-id="d4d5e-160">Ниже приведен пример файла **function.json**.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-160">Here is an example of **function.json** file.</span></span>

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

### <a name="projectjson"></a><span data-ttu-id="d4d5e-161">project.json</span><span class="sxs-lookup"><span data-stu-id="d4d5e-161">project.json</span></span>

<span data-ttu-id="d4d5e-162">файл project.json Hello содержит зависимости.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-162">hello project.json file contains dependencies.</span></span> <span data-ttu-id="d4d5e-163">Ниже приведен пример **project.json** файл, который включает службы мультимедиа Azure .NET hello необходимые пакеты из Nuget.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-163">Here is an example of **project.json** file that includes hello required .NET Azure Media Services packages from Nuget.</span></span> <span data-ttu-id="d4d5e-164">Обратите внимание, что номера версий hello изменится с последними обновлениями toohello пакетов, таким образом следует проверить hello самых последних версий.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-164">Note that hello version numbers will change with latest updates toohello packages, so you should confirm hello most recent versions.</span></span> 

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
    
### <a name="runcsx"></a><span data-ttu-id="d4d5e-165">run.csx</span><span class="sxs-lookup"><span data-stu-id="d4d5e-165">run.csx</span></span>

<span data-ttu-id="d4d5e-166">Это hello C# кода для функции.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-166">This is hello C# code for your function.</span></span>  <span data-ttu-id="d4d5e-167">функции Hello указанных ниже мониторы контейнер учетной записи хранилища с именем **ввода** (это то, что был указан в пути hello) для новых файлов MP4.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-167">hello function defined below monitors a storage account container named **input** (that is what was specified in hello path) for new MP4 files.</span></span> <span data-ttu-id="d4d5e-168">После удаления файла в контейнер хранилища hello hello больших двоичных объектов будет выполняться триггер функции hello.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-168">Once a file is dropped into hello storage container, hello blob trigger will execute hello function.</span></span>
    
<span data-ttu-id="d4d5e-169">демонстрирует пример Hello, заданные в этом разделе</span><span class="sxs-lookup"><span data-stu-id="d4d5e-169">hello example defined in this section demonstrates</span></span> 

1. <span data-ttu-id="d4d5e-170">учетной записи tooingest актива в службы мультимедиа (например, копирование большого двоичного объекта в актив AMS) и</span><span class="sxs-lookup"><span data-stu-id="d4d5e-170">how tooingest an asset into a Media Services account (by coping a blob into an AMS asset) and</span></span> 
2. <span data-ttu-id="d4d5e-171">как toosubmit предварительно задание кодирования, использующего носителя кодировщика Standard «адаптивной потоковой передачи».</span><span class="sxs-lookup"><span data-stu-id="d4d5e-171">how toosubmit an encoding job that uses Media Encoder Standard's "Adaptive Streaming" preset .</span></span>

<span data-ttu-id="d4d5e-172">В сценарии реальной жизни hello скорее всего, вы хотите tootrack ход выполнения задания, а затем опубликовать кодировке актива.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-172">In hello real life scenario, you most likely want tootrack job progress and then publish your encoded asset.</span></span> <span data-ttu-id="d4d5e-173">Дополнительные сведения см. в разделе [служб мультимедиа Azure использование веб-перехватчиков toomonitor задания уведомления](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="d4d5e-173">For more information, see [Use Azure WebHooks toomonitor Media Services job notifications](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> <span data-ttu-id="d4d5e-174">Дополнительные примеры приведены в разделе [функций Azure для служб мультимедиа](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="d4d5e-174">For more examples, see [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>  

<span data-ttu-id="d4d5e-175">После определения функции щелкните **Сохранить и запустить**.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-175">Once you are done defining your function click **Save and Run**.</span></span>

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
        // NOTE that hello variables {fileName} here come from hello path setting in function.json
        // and are passed into hello  Run method signature above. We can use this toomake decisions on what type of file
        // was dropped into hello input container for hello function. 

        // No need toodo any Retry strategy in this function, By default, hello SDK calls a function up too5 times for a 
        // given blob. If hello fifth try fails, hello SDK adds a message tooa queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used hello chached credentials toocreate CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy hello Blob into a new Input Asset for hello Job
        // ***NOTE: Ideally we would have a method tooingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with hello Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with hello encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify hello input asset toobe encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset toocontain hello results of hello job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means hello output asset is not encrypted. 
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
    /// Creates a new asset and copies blobs from hello specifed storage account.
    /// </summary>
    /// <param name="blob">hello specified blob.</param>
    /// <returns>hello new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference toohello storage account that is associated with hello Media Services account. 
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

        // Get hello destination asset container reference
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

        // Get hold of hello destination blob
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
##<a name="test-your-function"></a><span data-ttu-id="d4d5e-176">Тестирование функции</span><span class="sxs-lookup"><span data-stu-id="d4d5e-176">Test your function</span></span>

<span data-ttu-id="d4d5e-177">tootest функции, необходимые MP4-файл в hello tooupload **ввода** контейнера hello учетной записи хранения, указанной в строке подключения hello.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-177">tootest your function, you need tooupload an MP4 file into hello **input** container of hello storage account that you specified in hello connection string.</span></span>  

## <a name="next-step"></a><span data-ttu-id="d4d5e-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d4d5e-178">Next step</span></span>

<span data-ttu-id="d4d5e-179">На этом этапе вы являются готов toostart разработки приложений служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="d4d5e-179">At this point, you are ready toostart developing a Media Services application.</span></span> 
 
<span data-ttu-id="d4d5e-180">Дополнительные сведения и полный образцы и решений с помощью функции Azure и логика приложений с рабочими процессами создания пользовательского содержимого toocreate служб мультимедиа Azure см. в разделе hello [пример интеграции функций .NET служб мультимедиа на GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span><span class="sxs-lookup"><span data-stu-id="d4d5e-180">For more details and complete samples/solutions of using Azure Functions and Logic Apps with Azure Media Services toocreate custom content creation workflows, see hello [Media Services .NET Functions Integraiton Sample on GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span></span>

<span data-ttu-id="d4d5e-181">Кроме того, в разделе [служб мультимедиа Azure использование веб-перехватчиков toomonitor задания уведомления с помощью .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="d4d5e-181">Also, see [Use Azure WebHooks toomonitor Media Services job notifications with .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="d4d5e-182">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="d4d5e-182">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d4d5e-183">Отзывы</span><span class="sxs-lookup"><span data-stu-id="d4d5e-183">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

