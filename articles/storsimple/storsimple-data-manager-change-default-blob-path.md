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
# <a name="change-a-blob-path-from-hello-default-path-private-preview"></a>Изменение пути больших двоичных объектов из пути по умолчанию hello (личной предварительной версии)

В этой статье описывается, как tooset копирования Azure работать toorename путь к файлу большого двоичного объекта по умолчанию. 

## <a name="prerequisites"></a>Предварительные требования

Убедитесь в наличии определения задания, которое правильно настроено в гибридном ресурсе данных в группе ресурсов.

## <a name="create-an-azure-function"></a>Создание функции Azure

toocreate функцию Azure hello следующие:

1. Go toohello [портал Azure](http://portal.azure.com/).

2. Hello верхней части левой панели hello, нажмите кнопку **New**. 

3. В hello **поиска** введите **функции приложения**, и нажмите клавишу ВВОД.

    ![Введите «Функция приложение» в поле поиска hello](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. В hello **результатов** выберите **функции приложения**.

    ![Выберите ресурс приложения hello функций в списке результатов hello](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    Hello **функции приложения** открывается окно.

5. Щелкните **Создать**.

    ![Кнопка «Создать» окна приложения функции Hello](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. На hello **функции приложения** колонке конфигурации hello следующие:

    а. В hello **имя приложения** введите имя приложения hello.
    
    b. В hello **подписки** введите имя hello hello подписки.

    c. В разделе **группы ресурсов**, нажмите кнопку **создать новый**и затем имя типа hello hello группы ресурсов.

    d. В hello **плана размещения** введите **планирование потребления**.

    д. В hello **расположение** поле расположение типа hello.

    f. В разделе **Учетная запись хранения** выберите существующую учетную запись хранения или создайте новую. Учетная запись хранения используется внутренне для функции hello.

    ![Введение данных конфигурации нового приложения-функции](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. Щелкните **Создать**.  
    создается приложение функции Hello.

8. Hello левой панели щелкните **больше услуг**и затем hello следующие:
    
    а. В hello **фильтра** введите **службы приложений**.
    
    b. Щелкните **Службы приложений**. 

    ![Ссылка «Дополнительные службы» в левой области hello](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. В списке служб приложения hello щелкните имя функции приложение hello hello.  
    Откроется страница приложения функции Hello.

10. Hello левой панели щелкните **новая функция**и затем hello следующие: 

    а. В hello **язык** выберите **C#**.
    
    b. В массиве hello плиток шаблона, выберите **QueueTrigger CSharp**.

    c. В hello **имя функции** введите имя функции.

    d. В hello **имя очереди** введите свое имя определения задания преобразования данных.

    д. В разделе **подключения к учетной записи хранилища**, нажмите кнопку **новый**и затем выберите учетную запись hello, соответствующее задание toohello преобразования данных.  
        Запишите имя подключения hello. Далее в hello Azure функции требуется имя Hello.

       ![Создание функции C#](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    f. Щелкните **Создать**.  
    Hello **функция** открывается окно.

11. В hello **функция** выполните _.csx_ файла, а затем hello следующие:

    а. Вставьте следующий код hello:

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

    b. Замените имя **STORAGE_CONNECTIONNAME** в строке 11 именем подключения к учетной записи хранения (см. пункт 8c).

    c. Вверху hello слева, нажмите кнопку **Сохранить**.

    ![Сохранение функции](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. toocomplete Здравствуйте, функция, добавьте один дополнительные файл, выполнив hello ниже:

    а. Щелкните **Просмотреть файлы**.

       ![Здравствуйте, ссылка «Просмотр файлов»](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    b. Щелкните **Добавить**.
    
    c. Введите **project.json** и нажмите клавишу ВВОД.
    
    d. В hello **project.json** файла, вставьте hello, следующий код:

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

    д. Щелкните **Сохранить**.

Вы создали функцию Azure. Эта функция активируется каждый раз, когда новый большой двоичный объект создается заданием hello преобразования данных.

## <a name="next-steps"></a>Дальнейшие действия

[Использовать пользовательский Интерфейс диспетчера данных StorSimple tootransform данные](storsimple-data-manager-ui.md)
