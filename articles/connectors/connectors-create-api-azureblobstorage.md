---
title: "hello aaaAdd хранилище больших двоичных объектов соединителя в приложениях для логики | Документы Microsoft"
description: "Начало работы и настройка соединителя хранилища BLOB-объектов Azure hello в приложение логики"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5dc3f75-6bea-420b-b250-183668d2848d
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/02/2017
ms.author: mandia; ladocs
ms.openlocfilehash: add61287ef1b2228ef9d3f54ce082807bad6858b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-blob-storage-connector-in-a-logic-app"></a><span data-ttu-id="ae86c-103">Использование соединителя хранилища BLOB-объектов Azure hello в приложение логики</span><span class="sxs-lookup"><span data-stu-id="ae86c-103">Use hello Azure blob storage connector in a logic app</span></span>
<span data-ttu-id="ae86c-104">Используйте hello Azure BLOB-объекта хранилища соединитель tooupload обновления, получение и удаление больших двоичных объектов в вашей учетной записи хранения, все в пределах приложения логики.</span><span class="sxs-lookup"><span data-stu-id="ae86c-104">Use hello Azure Blob storage connector tooupload, update, get, and delete blobs in your storage account, all within a logic app.</span></span>  

<span data-ttu-id="ae86c-105">Хранилище BLOB-объектов Azure позволяет выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ae86c-105">With Azure blob storage, you:</span></span>

* <span data-ttu-id="ae86c-106">создавать рабочие процессы, отправляя новые проекты или получая недавно обновленные файлы;</span><span class="sxs-lookup"><span data-stu-id="ae86c-106">Build your workflow by uploading new projects, or getting files that have been recently updated.</span></span>
* <span data-ttu-id="ae86c-107">Используйте метаданные файла tooget действия, удалите файл, копирование файлов и многое другое.</span><span class="sxs-lookup"><span data-stu-id="ae86c-107">Use actions tooget file metadata, delete a file, copy files, and more.</span></span> <span data-ttu-id="ae86c-108">Например, при обновлении средства на веб-сайте Azure (триггер) будет обновляться файл в хранилище BLOB-объектов (действие).</span><span class="sxs-lookup"><span data-stu-id="ae86c-108">For example, when a tool is updated in an Azure web site (a trigger), then update a file in blob storage (an action).</span></span> 

<span data-ttu-id="ae86c-109">В этом разделе показано, как toouse hello больших двоичных объектов хранилища соединителя в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="ae86c-109">This topic shows you how toouse hello blob storage connector in a logic app.</span></span>

<span data-ttu-id="ae86c-110">toolearn Дополнительные сведения о приложении логики в разделе [Каковы приложения логики](../logic-apps/logic-apps-what-are-logic-apps.md) и [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ae86c-110">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<span data-ttu-id="ae86c-111">toolearn Дополнительные сведения о приложении логики в разделе [Каковы приложения логики](../logic-apps/logic-apps-what-are-logic-apps.md) и [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ae86c-111">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooazure-blob-storage"></a><span data-ttu-id="ae86c-112">Подключение tooAzure хранилища больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="ae86c-112">Connect tooAzure blob storage</span></span>
<span data-ttu-id="ae86c-113">Логика приложения можно получить доступ к любой службы, сначала создайте *подключения* toohello службы.</span><span class="sxs-lookup"><span data-stu-id="ae86c-113">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="ae86c-114">Таким образом вы установите соединение между приложением логики и другой службой.</span><span class="sxs-lookup"><span data-stu-id="ae86c-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="ae86c-115">Например, учетная запись хранения tooa tooconnect сначала создать хранилище BLOB-объектов *соединения*.</span><span class="sxs-lookup"><span data-stu-id="ae86c-115">For example, tooconnect tooa storage account, you first create a blob storage *connection*.</span></span> <span data-ttu-id="ae86c-116">toocreate соединения, введите учетные данные hello, обычно используется tooaccess hello службы, которому вы подключаетесь.</span><span class="sxs-lookup"><span data-stu-id="ae86c-116">toocreate a connection, enter hello credentials you normally use tooaccess hello service you are connecting to.</span></span> <span data-ttu-id="ae86c-117">Поэтому с хранилищем Azure, введите toocreate соединение hello tooyour хранилища hello учетные данные учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ae86c-117">So with Azure storage, enter hello credentials tooyour storage account toocreate hello connection.</span></span> 

#### <a name="create-hello-connection"></a><span data-ttu-id="ae86c-118">Создайте соединение hello</span><span class="sxs-lookup"><span data-stu-id="ae86c-118">Create hello connection</span></span>
> [!INCLUDE [Create a connection tooAzure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a><span data-ttu-id="ae86c-119">Использование триггера</span><span class="sxs-lookup"><span data-stu-id="ae86c-119">Use a trigger</span></span>
<span data-ttu-id="ae86c-120">Этот соединитель не содержит триггеров.</span><span class="sxs-lookup"><span data-stu-id="ae86c-120">This connector does not have any triggers.</span></span> <span data-ttu-id="ae86c-121">Использование других триггеров toostart hello логики приложения, например повторения триггера, триггер HTTP веб-перехватчика, триггеры, доступных с другими соединители и многое другое.</span><span class="sxs-lookup"><span data-stu-id="ae86c-121">Use other triggers toostart hello logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="ae86c-122">Пример см. в статье о [создании приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ae86c-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="ae86c-123">Использование действий</span><span class="sxs-lookup"><span data-stu-id="ae86c-123">Use an action</span></span>
<span data-ttu-id="ae86c-124">Действие — операции, выполняемые hello рабочего процесса, определенного в приложении логику.</span><span class="sxs-lookup"><span data-stu-id="ae86c-124">An action is an operation carried out by hello workflow defined in a logic app.</span></span>

1. <span data-ttu-id="ae86c-125">Выберите hello "плюс".</span><span class="sxs-lookup"><span data-stu-id="ae86c-125">Select hello plus sign.</span></span> <span data-ttu-id="ae86c-126">Вы видите несколько вариантов: **добавить действие**, **добавить условие**, или один из hello **дополнительные** параметры.</span><span class="sxs-lookup"><span data-stu-id="ae86c-126">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. <span data-ttu-id="ae86c-127">Выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="ae86c-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="ae86c-128">В текстовом поле hello введите «большой двоичный объект» tooget список всех доступных действий hello.</span><span class="sxs-lookup"><span data-stu-id="ae86c-128">In hello text box, type “blob” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. <span data-ttu-id="ae86c-129">В этом примере для хранилища BLOB-объектов Azure мы выберем действие **Get file metadata using path** (Получить метаданные файла с помощью пути).</span><span class="sxs-lookup"><span data-stu-id="ae86c-129">In our example, choose **AzureBlob - Get file metadata using path**.</span></span> <span data-ttu-id="ae86c-130">Если подключение уже существует, то выберите hello **...** Tooselect кнопку (Показать выбор) файла.</span><span class="sxs-lookup"><span data-stu-id="ae86c-130">If a connection already exists, then select hello **...** (Show Picker) button tooselect a file.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    <span data-ttu-id="ae86c-131">При появлении соответствующего запроса сведений о соединении hello введите toocreate hello hello сведения соединения.</span><span class="sxs-lookup"><span data-stu-id="ae86c-131">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="ae86c-132">[Создайте соединение hello](connectors-create-api-azureblobstorage.md#create-the-connection) в этом разделе описываются эти свойства.</span><span class="sxs-lookup"><span data-stu-id="ae86c-132">[Create hello connection](connectors-create-api-azureblobstorage.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="ae86c-133">В этом примере мы получаем hello метаданные файла.</span><span class="sxs-lookup"><span data-stu-id="ae86c-133">In this example, we get hello metadata of a file.</span></span> <span data-ttu-id="ae86c-134">toosee hello метаданные, добавьте другое действие, которое создает новый файл с помощью другого соединителя.</span><span class="sxs-lookup"><span data-stu-id="ae86c-134">toosee hello metadata, add another action that creates a new file using another connector.</span></span> <span data-ttu-id="ae86c-135">Например добавьте OneDrive действие, которое создает новый файл «test» на основе метаданных hello.</span><span class="sxs-lookup"><span data-stu-id="ae86c-135">For example, add a OneDrive action that creates a new "test" file based on hello metadata.</span></span> 


5. <span data-ttu-id="ae86c-136">**Сохранить** изменения (левом верхнем углу панели инструментов hello).</span><span class="sxs-lookup"><span data-stu-id="ae86c-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="ae86c-137">Приложение логики сохранено и теперь может быть включено автоматически.</span><span class="sxs-lookup"><span data-stu-id="ae86c-137">Your logic app is saved and may be automatically enabled.</span></span>

> [!TIP]
> <span data-ttu-id="ae86c-138">[Обозреватель хранилищ](http://storageexplorer.com/) мощный инструмент слишком управление несколькими учетными записями хранения.</span><span class="sxs-lookup"><span data-stu-id="ae86c-138">[Storage Explorer](http://storageexplorer.com/) is a great tool too manage multiple storage accounts.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="ae86c-139">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="ae86c-139">Connector-specific details</span></span>

<span data-ttu-id="ae86c-140">Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/azureblobconnector/).</span><span class="sxs-lookup"><span data-stu-id="ae86c-140">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/azureblobconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ae86c-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ae86c-141">Next steps</span></span>
<span data-ttu-id="ae86c-142">[Создание приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ae86c-142">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="ae86c-143">Просмотр hello другие доступные соединители в приложениях для логики в наших [список API-интерфейсы](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="ae86c-143">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

