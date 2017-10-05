---
title: "Изменение пути к большому двоичному объекту по умолчанию | Документация Майкрософт"
description: "Узнайте, как настроить функцию Azure для переименования пути к файлу большого двоичного объекта (закрытая предварительная версия)"
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
ms.openlocfilehash: 057d4d7370207859617eb63238bf425bfa6d3e16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="change-a-blob-path-from-the-default-path-private-preview"></a><span data-ttu-id="ce143-103">Изменение пути к большому двоичному объекту по умолчанию (закрытая предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="ce143-103">Change a blob path from the default path (private preview)</span></span>

<span data-ttu-id="ce143-104">В этой статье описывается настройка функции Azure для переименования пути к файлу большого двоичного объекта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ce143-104">This article describes how to set up an Azure function to rename a default blob file path.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ce143-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ce143-105">Prerequisites</span></span>

<span data-ttu-id="ce143-106">Убедитесь в наличии определения задания, которое правильно настроено в гибридном ресурсе данных в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ce143-106">Ensure that you have a job definition that has been correctly configured in a hybrid data resource within a resource group.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="ce143-107">Создание функции Azure</span><span class="sxs-lookup"><span data-stu-id="ce143-107">Create an Azure function</span></span>

<span data-ttu-id="ce143-108">Чтобы создать функцию Azure, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ce143-108">To create an Azure function, do the following:</span></span>

1. <span data-ttu-id="ce143-109">Перейдите на [портал Azure](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ce143-109">Go to the [Azure portal](http://portal.azure.com/).</span></span>

2. <span data-ttu-id="ce143-110">В верхней части левой области щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ce143-110">At the top of the left pane, click **New**.</span></span> 

3. <span data-ttu-id="ce143-111">В поле **поиска** введите **Приложение-функция** и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="ce143-111">In the **Search** box, type **Function App**, and then press Enter.</span></span>

    ![Введение "Приложение-функция" поле поиска](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. <span data-ttu-id="ce143-113">В списке **Результаты** щелкните **Приложение-функция**.</span><span class="sxs-lookup"><span data-stu-id="ce143-113">In the **Results** list, click **Function App**.</span></span>

    ![Выбор ресурса приложения-функции в списке результатов](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    <span data-ttu-id="ce143-115">Откроется окно **Приложение-функция**.</span><span class="sxs-lookup"><span data-stu-id="ce143-115">The **Function App** window opens.</span></span>

5. <span data-ttu-id="ce143-116">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ce143-116">Click **Create**.</span></span>

    ![Кнопка "Создать" в окне "Приложение-функция"](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. <span data-ttu-id="ce143-118">В колонке настройки **Приложение-функция** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ce143-118">On the **Function App** configuration blade, do the following:</span></span>

    <span data-ttu-id="ce143-119">а.</span><span class="sxs-lookup"><span data-stu-id="ce143-119">a.</span></span> <span data-ttu-id="ce143-120">В поле **Имя приложения** введите имя приложения.</span><span class="sxs-lookup"><span data-stu-id="ce143-120">In the **App name** box, type the app name.</span></span>
    
    <span data-ttu-id="ce143-121">b.</span><span class="sxs-lookup"><span data-stu-id="ce143-121">b.</span></span> <span data-ttu-id="ce143-122">В поле **Подписка** введите имя подписки.</span><span class="sxs-lookup"><span data-stu-id="ce143-122">In the **Subscription** box, type the name of the subscription.</span></span>

    <span data-ttu-id="ce143-123">c.</span><span class="sxs-lookup"><span data-stu-id="ce143-123">c.</span></span> <span data-ttu-id="ce143-124">В разделе **Группа ресурсов** щелкните **Создать**, а затем введите имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ce143-124">Under **Resource Group**, click **Create new**, and then type the name of the resource group.</span></span>

    <span data-ttu-id="ce143-125">d.</span><span class="sxs-lookup"><span data-stu-id="ce143-125">d.</span></span> <span data-ttu-id="ce143-126">В поле **План размещения** укажите **План потребления**.</span><span class="sxs-lookup"><span data-stu-id="ce143-126">In the **Hosting Plan** box, type **Consumption Plan**.</span></span>

    <span data-ttu-id="ce143-127">д.</span><span class="sxs-lookup"><span data-stu-id="ce143-127">e.</span></span> <span data-ttu-id="ce143-128">В поле **Расположение** укажите расположение.</span><span class="sxs-lookup"><span data-stu-id="ce143-128">In the **Location** box, type the location.</span></span>

    <span data-ttu-id="ce143-129">f.</span><span class="sxs-lookup"><span data-stu-id="ce143-129">f.</span></span> <span data-ttu-id="ce143-130">В разделе **Учетная запись хранения** выберите существующую учетную запись хранения или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="ce143-130">Under **Storage account**, select an existing storage account or create a new storage account.</span></span> <span data-ttu-id="ce143-131">Учетная запись хранения используется внутренне для функции.</span><span class="sxs-lookup"><span data-stu-id="ce143-131">A storage account is used internally for the function.</span></span>

    ![Введение данных конфигурации нового приложения-функции](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. <span data-ttu-id="ce143-133">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ce143-133">Click **Create**.</span></span>  
    <span data-ttu-id="ce143-134">Приложение-функция создано.</span><span class="sxs-lookup"><span data-stu-id="ce143-134">The function app is created.</span></span>

8. <span data-ttu-id="ce143-135">В левой области щелкните **Больше служб**, а затем выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ce143-135">In the left pane, click **More services**, and then do the following:</span></span>
    
    <span data-ttu-id="ce143-136">а.</span><span class="sxs-lookup"><span data-stu-id="ce143-136">a.</span></span> <span data-ttu-id="ce143-137">В поле **Фильтр** введите **Службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="ce143-137">In the **Filter** box, type **App services**.</span></span>
    
    <span data-ttu-id="ce143-138">b.</span><span class="sxs-lookup"><span data-stu-id="ce143-138">b.</span></span> <span data-ttu-id="ce143-139">Щелкните **Службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="ce143-139">Click **App Services**.</span></span> 

    ![Ссылка "Больше служб" в левой области](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. <span data-ttu-id="ce143-141">В списке служб приложений щелкните имя приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="ce143-141">In the list of app services, click the name of the function app.</span></span>  
    <span data-ttu-id="ce143-142">Откроется страница этого приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="ce143-142">The function app page opens.</span></span>

10. <span data-ttu-id="ce143-143">В левой области щелкните **Новая функция**, а затем выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ce143-143">In the left pane, click **New Function**, and then do the following:</span></span> 

    <span data-ttu-id="ce143-144">а.</span><span class="sxs-lookup"><span data-stu-id="ce143-144">a.</span></span> <span data-ttu-id="ce143-145">В списке **Язык** выберите **C#**.</span><span class="sxs-lookup"><span data-stu-id="ce143-145">In the **Language** list, select **C#**.</span></span>
    
    <span data-ttu-id="ce143-146">b.</span><span class="sxs-lookup"><span data-stu-id="ce143-146">b.</span></span> <span data-ttu-id="ce143-147">В массиве элементов выберите шаблон **QueueTrigger-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="ce143-147">In the array of template tiles, select **QueueTrigger-CSharp**.</span></span>

    <span data-ttu-id="ce143-148">c.</span><span class="sxs-lookup"><span data-stu-id="ce143-148">c.</span></span> <span data-ttu-id="ce143-149">В поле **Присвойте функции имя** введите имя для своей функции.</span><span class="sxs-lookup"><span data-stu-id="ce143-149">In the **Name your function** box, type a name for your function.</span></span>

    <span data-ttu-id="ce143-150">d.</span><span class="sxs-lookup"><span data-stu-id="ce143-150">d.</span></span> <span data-ttu-id="ce143-151">В поле **Имя очереди** введите имя определения задания преобразования данных.</span><span class="sxs-lookup"><span data-stu-id="ce143-151">In the **Queue name** box, type your data-transformation job definition name.</span></span>

    <span data-ttu-id="ce143-152">д.</span><span class="sxs-lookup"><span data-stu-id="ce143-152">e.</span></span> <span data-ttu-id="ce143-153">В разделе **Подключение к учетной записи хранения** щелкните **создать**и выберите учетную запись, соответствующую заданию преобразования данных.</span><span class="sxs-lookup"><span data-stu-id="ce143-153">Under **Storage account connection**, click **new**, and then select the account that corresponds to the data-transformation job.</span></span>  
        <span data-ttu-id="ce143-154">Запишите это имя подключения.</span><span class="sxs-lookup"><span data-stu-id="ce143-154">Make a note of the connection name.</span></span> <span data-ttu-id="ce143-155">Оно понадобится позже в функции Azure.</span><span class="sxs-lookup"><span data-stu-id="ce143-155">The name is required later in the Azure function.</span></span>

       ![Создание функции C#](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    <span data-ttu-id="ce143-157">f.</span><span class="sxs-lookup"><span data-stu-id="ce143-157">f.</span></span> <span data-ttu-id="ce143-158">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ce143-158">Click **Create**.</span></span>  
    <span data-ttu-id="ce143-159">Откроется окно **Функция**.</span><span class="sxs-lookup"><span data-stu-id="ce143-159">The **Function** window opens.</span></span>

11. <span data-ttu-id="ce143-160">В окне **Функция** выполните _CSX_-файл, а затем выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ce143-160">In the **Function** window, run _.csx_ file, and then do the following:</span></span>

    <span data-ttu-id="ce143-161">а.</span><span class="sxs-lookup"><span data-stu-id="ce143-161">a.</span></span> <span data-ttu-id="ce143-162">Вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="ce143-162">Paste the following code:</span></span>

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

        // Create the blob client.
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
            // Skip to copy the blob to new container, if source blob doesn't exist
            log.Info($"The specified blob does not exist.");
            log.Info($"Blob Uri: {blob.Uri}");
            return;
        }

        CloudBlockBlob blobCopy = newContainer.GetBlockBlobReference(newBlobName);
        if (!blobCopy.Exists())
        {
            blobCopy.StartCopy(blob);
            // Delete old blob, after copy to new container
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

    <span data-ttu-id="ce143-163">b.</span><span class="sxs-lookup"><span data-stu-id="ce143-163">b.</span></span> <span data-ttu-id="ce143-164">Замените имя **STORAGE_CONNECTIONNAME** в строке 11 именем подключения к учетной записи хранения (см. пункт 8c).</span><span class="sxs-lookup"><span data-stu-id="ce143-164">Replace **STORAGE_CONNECTIONNAME** on line 11 with your storage account connection (refer point 8c).</span></span>

    <span data-ttu-id="ce143-165">c.</span><span class="sxs-lookup"><span data-stu-id="ce143-165">c.</span></span> <span data-ttu-id="ce143-166">В верхней левом углу нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ce143-166">At the top left, click **Save**.</span></span>

    ![Сохранение функции](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. <span data-ttu-id="ce143-168">Чтобы завершить создание функции, добавьте еще один файл, выполнив следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ce143-168">To complete the function, add one more file by doing the following:</span></span>

    <span data-ttu-id="ce143-169">а.</span><span class="sxs-lookup"><span data-stu-id="ce143-169">a.</span></span> <span data-ttu-id="ce143-170">Щелкните **Просмотреть файлы**.</span><span class="sxs-lookup"><span data-stu-id="ce143-170">Click **View files**.</span></span>

       ![Ссылка "Просмотреть файлы"](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    <span data-ttu-id="ce143-172">b.</span><span class="sxs-lookup"><span data-stu-id="ce143-172">b.</span></span> <span data-ttu-id="ce143-173">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ce143-173">Click **Add**.</span></span>
    
    <span data-ttu-id="ce143-174">c.</span><span class="sxs-lookup"><span data-stu-id="ce143-174">c.</span></span> <span data-ttu-id="ce143-175">Введите **project.json** и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="ce143-175">Type **project.json**, and then press Enter.</span></span>
    
    <span data-ttu-id="ce143-176">d.</span><span class="sxs-lookup"><span data-stu-id="ce143-176">d.</span></span> <span data-ttu-id="ce143-177">В файле **project.json** скопируйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="ce143-177">In the **project.json** file, paste the following code:</span></span>

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

    <span data-ttu-id="ce143-178">д.</span><span class="sxs-lookup"><span data-stu-id="ce143-178">e.</span></span> <span data-ttu-id="ce143-179">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ce143-179">Click **Save**.</span></span>

<span data-ttu-id="ce143-180">Вы создали функцию Azure.</span><span class="sxs-lookup"><span data-stu-id="ce143-180">You have created an Azure function.</span></span> <span data-ttu-id="ce143-181">Эта функция запускается каждый раз, когда задание преобразования данных создает большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="ce143-181">This function is triggered each time a new blob is generated by the data-transformation job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce143-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ce143-182">Next steps</span></span>

[<span data-ttu-id="ce143-183">Использование пользовательского интерфейса для службы диспетчера данных StorSimple (закрытая предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="ce143-183">Use StorSimple Data Manager UI to transform your data</span></span>](storsimple-data-manager-ui.md)
