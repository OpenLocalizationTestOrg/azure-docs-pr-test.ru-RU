---
title: "aaaChange пути больших двоичных объектов относительно значения по умолчанию hello | Документы Microsoft"
description: "Узнайте, как tooset копирования Azure работать toorename путь к файлу большого двоичного объекта (личной предварительной версии)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 2c414603514223c701ab1a3bd0b81ee18f1af666
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="change-a-blob-path-from-hello-default-path-private-preview"></a><span data-ttu-id="50877-103">Изменение пути больших двоичных объектов из пути по умолчанию hello (личной предварительной версии)</span><span class="sxs-lookup"><span data-stu-id="50877-103">Change a blob path from hello default path (private preview)</span></span>

<span data-ttu-id="50877-104">В этой статье описывается, как tooset копирования Azure работать toorename путь к файлу большого двоичного объекта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="50877-104">This article describes how tooset up an Azure function toorename a default blob file path.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="50877-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="50877-105">Prerequisites</span></span>

<span data-ttu-id="50877-106">Убедитесь в наличии определения задания, которое правильно настроено в гибридном ресурсе данных в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="50877-106">Ensure that you have a job definition that has been correctly configured in a hybrid data resource within a resource group.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="50877-107">Создание функции Azure</span><span class="sxs-lookup"><span data-stu-id="50877-107">Create an Azure function</span></span>

<span data-ttu-id="50877-108">toocreate функцию Azure hello следующие:</span><span class="sxs-lookup"><span data-stu-id="50877-108">toocreate an Azure function, do hello following:</span></span>

1. <span data-ttu-id="50877-109">Go toohello [портал Azure](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="50877-109">Go toohello [Azure portal](http://portal.azure.com/).</span></span>

2. <span data-ttu-id="50877-110">Hello верхней части левой панели hello, нажмите кнопку **New**.</span><span class="sxs-lookup"><span data-stu-id="50877-110">At hello top of hello left pane, click **New**.</span></span> 

3. <span data-ttu-id="50877-111">В hello **поиска** введите **функции приложения**, и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="50877-111">In hello **Search** box, type **Function App**, and then press Enter.</span></span>

    ![Введите «Функция приложение» в поле поиска hello](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. <span data-ttu-id="50877-113">В hello **результатов** выберите **функции приложения**.</span><span class="sxs-lookup"><span data-stu-id="50877-113">In hello **Results** list, click **Function App**.</span></span>

    ![Выберите ресурс приложения hello функций в списке результатов hello](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    <span data-ttu-id="50877-115">Hello **функции приложения** открывается окно.</span><span class="sxs-lookup"><span data-stu-id="50877-115">hello **Function App** window opens.</span></span>

5. <span data-ttu-id="50877-116">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="50877-116">Click **Create**.</span></span>

    ![Кнопка «Создать» окна приложения функции Hello](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. <span data-ttu-id="50877-118">На hello **функции приложения** колонке конфигурации hello следующие:</span><span class="sxs-lookup"><span data-stu-id="50877-118">On hello **Function App** configuration blade, do hello following:</span></span>

    <span data-ttu-id="50877-119">а.</span><span class="sxs-lookup"><span data-stu-id="50877-119">a.</span></span> <span data-ttu-id="50877-120">В hello **имя приложения** введите имя приложения hello.</span><span class="sxs-lookup"><span data-stu-id="50877-120">In hello **App name** box, type hello app name.</span></span>
    
    <span data-ttu-id="50877-121">b.</span><span class="sxs-lookup"><span data-stu-id="50877-121">b.</span></span> <span data-ttu-id="50877-122">В hello **подписки** введите имя hello hello подписки.</span><span class="sxs-lookup"><span data-stu-id="50877-122">In hello **Subscription** box, type hello name of hello subscription.</span></span>

    <span data-ttu-id="50877-123">c.</span><span class="sxs-lookup"><span data-stu-id="50877-123">c.</span></span> <span data-ttu-id="50877-124">В разделе **группы ресурсов**, нажмите кнопку **создать новый**и затем имя типа hello hello группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="50877-124">Under **Resource Group**, click **Create new**, and then type hello name of hello resource group.</span></span>

    <span data-ttu-id="50877-125">d.</span><span class="sxs-lookup"><span data-stu-id="50877-125">d.</span></span> <span data-ttu-id="50877-126">В hello **плана размещения** введите **планирование потребления**.</span><span class="sxs-lookup"><span data-stu-id="50877-126">In hello **Hosting Plan** box, type **Consumption Plan**.</span></span>

    <span data-ttu-id="50877-127">д.</span><span class="sxs-lookup"><span data-stu-id="50877-127">e.</span></span> <span data-ttu-id="50877-128">В hello **расположение** поле расположение типа hello.</span><span class="sxs-lookup"><span data-stu-id="50877-128">In hello **Location** box, type hello location.</span></span>

    <span data-ttu-id="50877-129">f.</span><span class="sxs-lookup"><span data-stu-id="50877-129">f.</span></span> <span data-ttu-id="50877-130">В разделе **Учетная запись хранения** выберите существующую учетную запись хранения или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="50877-130">Under **Storage account**, select an existing storage account or create a new storage account.</span></span> <span data-ttu-id="50877-131">Учетная запись хранения используется внутренне для функции hello.</span><span class="sxs-lookup"><span data-stu-id="50877-131">A storage account is used internally for hello function.</span></span>

    ![Введение данных конфигурации нового приложения-функции](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. <span data-ttu-id="50877-133">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="50877-133">Click **Create**.</span></span>  
    <span data-ttu-id="50877-134">создается приложение функции Hello.</span><span class="sxs-lookup"><span data-stu-id="50877-134">hello function app is created.</span></span>

8. <span data-ttu-id="50877-135">Hello левой панели щелкните **больше услуг**и затем hello следующие:</span><span class="sxs-lookup"><span data-stu-id="50877-135">In hello left pane, click **More services**, and then do hello following:</span></span>
    
    <span data-ttu-id="50877-136">а.</span><span class="sxs-lookup"><span data-stu-id="50877-136">a.</span></span> <span data-ttu-id="50877-137">В hello **фильтра** введите **службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="50877-137">In hello **Filter** box, type **App services**.</span></span>
    
    <span data-ttu-id="50877-138">b.</span><span class="sxs-lookup"><span data-stu-id="50877-138">b.</span></span> <span data-ttu-id="50877-139">Щелкните **Службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="50877-139">Click **App Services**.</span></span> 

    ![Ссылка «Дополнительные службы» в левой области hello](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. <span data-ttu-id="50877-141">В списке служб приложения hello щелкните имя функции приложение hello hello.</span><span class="sxs-lookup"><span data-stu-id="50877-141">In hello list of app services, click hello name of hello function app.</span></span>  
    <span data-ttu-id="50877-142">Откроется страница приложения функции Hello.</span><span class="sxs-lookup"><span data-stu-id="50877-142">hello function app page opens.</span></span>

10. <span data-ttu-id="50877-143">Hello левой панели щелкните **новая функция**и затем hello следующие:</span><span class="sxs-lookup"><span data-stu-id="50877-143">In hello left pane, click **New Function**, and then do hello following:</span></span> 

    <span data-ttu-id="50877-144">а.</span><span class="sxs-lookup"><span data-stu-id="50877-144">a.</span></span> <span data-ttu-id="50877-145">В hello **язык** выберите **C#**.</span><span class="sxs-lookup"><span data-stu-id="50877-145">In hello **Language** list, select **C#**.</span></span>
    
    <span data-ttu-id="50877-146">b.</span><span class="sxs-lookup"><span data-stu-id="50877-146">b.</span></span> <span data-ttu-id="50877-147">В массиве hello плиток шаблона, выберите **QueueTrigger CSharp**.</span><span class="sxs-lookup"><span data-stu-id="50877-147">In hello array of template tiles, select **QueueTrigger-CSharp**.</span></span>

    <span data-ttu-id="50877-148">c.</span><span class="sxs-lookup"><span data-stu-id="50877-148">c.</span></span> <span data-ttu-id="50877-149">В hello **имя функции** введите имя функции.</span><span class="sxs-lookup"><span data-stu-id="50877-149">In hello **Name your function** box, type a name for your function.</span></span>

    <span data-ttu-id="50877-150">d.</span><span class="sxs-lookup"><span data-stu-id="50877-150">d.</span></span> <span data-ttu-id="50877-151">В hello **имя очереди** введите свое имя определения задания преобразования данных.</span><span class="sxs-lookup"><span data-stu-id="50877-151">In hello **Queue name** box, type your data-transformation job definition name.</span></span>

    <span data-ttu-id="50877-152">д.</span><span class="sxs-lookup"><span data-stu-id="50877-152">e.</span></span> <span data-ttu-id="50877-153">В разделе **подключения к учетной записи хранилища**, нажмите кнопку **новый**и затем выберите учетную запись hello, соответствующее задание toohello преобразования данных.</span><span class="sxs-lookup"><span data-stu-id="50877-153">Under **Storage account connection**, click **new**, and then select hello account that corresponds toohello data-transformation job.</span></span>  
        <span data-ttu-id="50877-154">Запишите имя подключения hello.</span><span class="sxs-lookup"><span data-stu-id="50877-154">Make a note of hello connection name.</span></span> <span data-ttu-id="50877-155">Далее в hello Azure функции требуется имя Hello.</span><span class="sxs-lookup"><span data-stu-id="50877-155">hello name is required later in hello Azure function.</span></span>

       ![Создание функции C#](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    <span data-ttu-id="50877-157">f.</span><span class="sxs-lookup"><span data-stu-id="50877-157">f.</span></span> <span data-ttu-id="50877-158">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="50877-158">Click **Create**.</span></span>  
    <span data-ttu-id="50877-159">Hello **функция** открывается окно.</span><span class="sxs-lookup"><span data-stu-id="50877-159">hello **Function** window opens.</span></span>

11. <span data-ttu-id="50877-160">В hello **функция** выполните _.csx_ файла, а затем hello следующие:</span><span class="sxs-lookup"><span data-stu-id="50877-160">In hello **Function** window, run _.csx_ file, and then do hello following:</span></span>

    <span data-ttu-id="50877-161">а.</span><span class="sxs-lookup"><span data-stu-id="50877-161">a.</span></span> <span data-ttu-id="50877-162">Вставьте следующий код hello:</span><span class="sxs-lookup"><span data-stu-id="50877-162">Paste hello following code:</span></span>

    ```
    using System;
    using System.Configuration;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Queue;
    using Microsoft.WindowsAzure.Storage;
    using System.Collections.Generic;
    using System.Linq;

    public static void Run(QueueItem myQueueItem, TraceWriter log)
    {
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["STORAGE_CONNECTIONNAME"]);

        string storageAccUriEndswith = "windows.net/";
        string uri = myQueueItem.TargetLocation.Replace("%20", " ");
        log.Info($"Blob Uri: {uri}");

        // Remove storage account uri string
        uri = uri.Substring(uri.IndexOf(storageAccUriEndswith) + storageAccUriEndswith.Length);

        string containerName = uri.Substring(0, uri.IndexOf("/")); 

        // Remove container name string
        uri = uri.Substring(containerName.Length + 1);

        // Current blob path
        string blobName = uri; 

        string volumeName = uri.Substring(containerName.Length + 1);
        volumeName = uri.Substring(0, uri.IndexOf("/"));

        // Remove volume name string
        uri = uri.Substring(volumeName.Length + 1);

        string newContainerName = uri.Substring(0, uri.IndexOf("/")).ToLower();
        string newBlobName = uri.Substring(newContainerName.Length + 1);

        log.Info($"Container name: {containerName}");
        log.Info($"Volume name: {volumeName}");
        log.Info($"New container name: {newContainerName}");

        log.Info($"Blob name: {blobName}");
        log.Info($"New blob name: {newBlobName}");

        // Create hello blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Container reference
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlobContainer newContainer = blobClient.GetContainerReference(newContainerName);
        newContainer.CreateIfNotExists();

        if(!container.Exists())
        {
            log.Info($"Container - {containerName} not exists");
            return;
        }

        if(!newContainer.Exists())
        {
            log.Info($"Container - {newContainerName} not exists");
            return;
        }

        CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
        if (!blob.Exists())
        {
            // Skip toocopy hello blob toonew container, if source blob doesn't exist
            log.Info($"hello specified blob does not exist.");
            log.Info($"Blob Uri: {blob.Uri}");
            return;
        }

        CloudBlockBlob blobCopy = newContainer.GetBlockBlobReference(newBlobName);
        if (!blobCopy.Exists())
        {
            blobCopy.StartCopy(blob);
            // Delete old blob, after copy toonew container
            blob.DeleteIfExists();
            log.Info($"Blob file path renamed completed successfully");
        }
        else
        {
            log.Info($"Blob file path renamed already done");
            // Delete old blob, if already exists.
            blob.DeleteIfExists();
        }
    }

    public class QueueItem
    {
        public string SourceLocation {get;set;}
        public long SizeInBytes {get;set;}
        public string Status {get;set;}
        public string JobID {get;set;}
        public string TargetLocation {get; set;}
    }

    ```

    <span data-ttu-id="50877-163">b.</span><span class="sxs-lookup"><span data-stu-id="50877-163">b.</span></span> <span data-ttu-id="50877-164">Замените имя **STORAGE_CONNECTIONNAME** в строке 11 именем подключения к учетной записи хранения (см. пункт 8c).</span><span class="sxs-lookup"><span data-stu-id="50877-164">Replace **STORAGE_CONNECTIONNAME** on line 11 with your storage account connection (refer point 8c).</span></span>

    <span data-ttu-id="50877-165">c.</span><span class="sxs-lookup"><span data-stu-id="50877-165">c.</span></span> <span data-ttu-id="50877-166">Вверху hello слева, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="50877-166">At hello top left, click **Save**.</span></span>

    ![Сохранение функции](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. <span data-ttu-id="50877-168">toocomplete Здравствуйте, функция, добавьте один дополнительные файл, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="50877-168">toocomplete hello function, add one more file by doing hello following:</span></span>

    <span data-ttu-id="50877-169">а.</span><span class="sxs-lookup"><span data-stu-id="50877-169">a.</span></span> <span data-ttu-id="50877-170">Щелкните **Просмотреть файлы**.</span><span class="sxs-lookup"><span data-stu-id="50877-170">Click **View files**.</span></span>

       ![Здравствуйте, ссылка «Просмотр файлов»](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    <span data-ttu-id="50877-172">b.</span><span class="sxs-lookup"><span data-stu-id="50877-172">b.</span></span> <span data-ttu-id="50877-173">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="50877-173">Click **Add**.</span></span>
    
    <span data-ttu-id="50877-174">c.</span><span class="sxs-lookup"><span data-stu-id="50877-174">c.</span></span> <span data-ttu-id="50877-175">Введите **project.json** и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="50877-175">Type **project.json**, and then press Enter.</span></span>
    
    <span data-ttu-id="50877-176">d.</span><span class="sxs-lookup"><span data-stu-id="50877-176">d.</span></span> <span data-ttu-id="50877-177">В hello **project.json** файла, вставьте hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="50877-177">In hello **project.json** file, paste hello following code:</span></span>

    ```
    {
    "frameworks": {
        "net46":{
        "dependencies": {
            "windowsazure.storage": "8.1.1"
        }
        }
    }
    }

    ```

    <span data-ttu-id="50877-178">д.</span><span class="sxs-lookup"><span data-stu-id="50877-178">e.</span></span> <span data-ttu-id="50877-179">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="50877-179">Click **Save**.</span></span>

<span data-ttu-id="50877-180">Вы создали функцию Azure.</span><span class="sxs-lookup"><span data-stu-id="50877-180">You have created an Azure function.</span></span> <span data-ttu-id="50877-181">Эта функция активируется каждый раз, когда новый большой двоичный объект создается заданием hello преобразования данных.</span><span class="sxs-lookup"><span data-stu-id="50877-181">This function is triggered each time a new blob is generated by hello data-transformation job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50877-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="50877-182">Next steps</span></span>

[<span data-ttu-id="50877-183">Использовать пользовательский Интерфейс диспетчера данных StorSimple tootransform данные</span><span class="sxs-lookup"><span data-stu-id="50877-183">Use StorSimple Data Manager UI tootransform your data</span></span>](storsimple-data-manager-ui.md)
