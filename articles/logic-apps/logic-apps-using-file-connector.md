---
title: "Подключение к локальной файловой системе из Azure Logic Apps | Документация Майкрософт"
description: "Подключение к локальным файловым системам из рабочего процесса приложения логики через шлюз локальных данных и соединитель файловой системы"
keywords: "файловые системы"
services: logic-apps
author: derek1ee
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/27/2017
ms.author: LADocs; deli
ms.openlocfilehash: f33e7c58103c57e17e4e273caba1ab9b83f0cd2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-on-premises-file-systems-from-logic-apps-with-the-file-system-connector"></a><span data-ttu-id="45bec-104">Подключение к локальным файловым системам из приложений логики с помощью соединителя файловой системы</span><span class="sxs-lookup"><span data-stu-id="45bec-104">Connect to on-premises file systems from logic apps with the File System connector</span></span>

<span data-ttu-id="45bec-105">Подключение к гибридным облакам является ключевой функцией для приложений логики, поэтому для управления данными и безопасного доступа к локальным ресурсам приложения логики могут использовать шлюз локальных данных.</span><span class="sxs-lookup"><span data-stu-id="45bec-105">Hybrid cloud connectivity is central to logic apps, so to manage data and securely access on-premises resources, your logic apps can use the on-premises data gateway.</span></span> <span data-ttu-id="45bec-106">В этой статье мы покажем, как подключиться к локальной файловой системе в простом сценарии: копирование файла, переданного в Dropbox, в файловый ресурс, а затем отправка электронного сообщения.</span><span class="sxs-lookup"><span data-stu-id="45bec-106">In this article, we show how to connect to an on-premises file system with a basic scenario: copy a file that's uploaded to Dropbox to a file share, then send an email.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45bec-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="45bec-107">Prerequisites</span></span>

- <span data-ttu-id="45bec-108">Установите и настройте последнюю версию [локального шлюза данных](https://www.microsoft.com/download/details.aspx?id=53127).</span><span class="sxs-lookup"><span data-stu-id="45bec-108">Install and configure the latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127).</span></span>
- <span data-ttu-id="45bec-109">Установите последнюю версию локального шлюза данных (не ниже версии 1.15.6150.1).</span><span class="sxs-lookup"><span data-stu-id="45bec-109">Install the latest on-premises data gateway, version 1.15.6150.1 or above.</span></span> <span data-ttu-id="45bec-110">Эти действия приводятся в статье [Подключение к локальному шлюзу данных для приложений логики](http://aka.ms/logicapps-gateway).</span><span class="sxs-lookup"><span data-stu-id="45bec-110">[Connect to the on-premises data gateway](http://aka.ms/logicapps-gateway) lists the steps.</span></span> <span data-ttu-id="45bec-111">Шлюз нужно установить на локальном компьютере, прежде чем можно будет продолжить процедуру.</span><span class="sxs-lookup"><span data-stu-id="45bec-111">The gateway must be installed on an on-premises machine before you can continue with the rest of the steps.</span></span>

## <a name="add-trigger-and-actions-for-connecting-to-your-file-system"></a><span data-ttu-id="45bec-112">Добавление триггера и действий для подключения к файловой системе</span><span class="sxs-lookup"><span data-stu-id="45bec-112">Add trigger and actions for connecting to your file system</span></span>

1. <span data-ttu-id="45bec-113">Создание приложения логики и добавление триггера Dropbox **При создании файла**</span><span class="sxs-lookup"><span data-stu-id="45bec-113">Create a logic app, and add this Dropbox trigger: **When a file is created**</span></span> 
2. <span data-ttu-id="45bec-114">Для триггера выберите **Следующий шаг** > **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="45bec-114">Under the trigger, choose **Next Step** > **Add an action**.</span></span> 
3. <span data-ttu-id="45bec-115">В поле поиска введите `file system`, чтобы просмотреть все поддерживаемые действия для соединителя файловой системы.</span><span class="sxs-lookup"><span data-stu-id="45bec-115">In the search box, enter `file system` so you can view all supported actions for the File System connector.</span></span>

   ![Поиск соединителя File](media/logic-apps-using-file-connector/search-file-connector.png)

2. <span data-ttu-id="45bec-117">Выберите действие **Создать файл** и создайте подключение к файловой системе.</span><span class="sxs-lookup"><span data-stu-id="45bec-117">Choose the **Create file** action, and create a connection to your file system.</span></span>

   <span data-ttu-id="45bec-118">Если у вас нет существующего подключения, то вам будет предложено создать его.</span><span class="sxs-lookup"><span data-stu-id="45bec-118">If you don't have an existing connection, you are prompted to create one.</span></span>

   1. <span data-ttu-id="45bec-119">Установите флажок **Connect via on-premises data gateway** (Подключение через локальный шлюз данных).</span><span class="sxs-lookup"><span data-stu-id="45bec-119">Choose **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="45bec-120">Отобразятся дополнительные свойства.</span><span class="sxs-lookup"><span data-stu-id="45bec-120">More properties appear.</span></span>
   2. <span data-ttu-id="45bec-121">Выберите корневую папку для файловой системы.</span><span class="sxs-lookup"><span data-stu-id="45bec-121">Select your root folder for your file system.</span></span>
      
       > [!NOTE]
       > <span data-ttu-id="45bec-122">Корневая папка является основной родительской папкой, которая используется для относительных путей всех действий с файлами.</span><span class="sxs-lookup"><span data-stu-id="45bec-122">The root folder is the main parent folder, which is used for relative paths for all file-related actions.</span></span> <span data-ttu-id="45bec-123">Это может быть локальная папка на компьютере, где установлен локальный шлюз данных, или сетевая папка, к которой этот компьютер имеет доступ.</span><span class="sxs-lookup"><span data-stu-id="45bec-123">You can specify a local folder on the machine where the on-premises data gateway is installed, or the folder can be a network share that the machine can access.</span></span>

   3. <span data-ttu-id="45bec-124">Введите имя пользователя и пароль для шлюза.</span><span class="sxs-lookup"><span data-stu-id="45bec-124">Enter the username and password for the gateway.</span></span>
   4. <span data-ttu-id="45bec-125">Выберите шлюз, который был установлен ранее.</span><span class="sxs-lookup"><span data-stu-id="45bec-125">Select the gateway that you previously installed.</span></span>

       ![Настройка подключения](media/logic-apps-using-file-connector/create-file.png)

3. <span data-ttu-id="45bec-127">После предоставления всех сведений выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="45bec-127">After you provide all the details, choose **Create**.</span></span> 

   <span data-ttu-id="45bec-128">Logic Apps настраивает и проверяет подключение, гарантируя, что оно работает правильно.</span><span class="sxs-lookup"><span data-stu-id="45bec-128">Logic Apps configures and tests your connection, making sure that the connection works properly.</span></span> 
   <span data-ttu-id="45bec-129">Если подключение установлено правильно, можно увидеть параметры для действия, выбранного ранее.</span><span class="sxs-lookup"><span data-stu-id="45bec-129">If the connection is set up correctly, you see options for the action that you previously selected.</span></span> 
   <span data-ttu-id="45bec-130">Теперь соединитель файловой системы готов к использованию.</span><span class="sxs-lookup"><span data-stu-id="45bec-130">The file system connector is now ready for use.</span></span>

4. <span data-ttu-id="45bec-131">Укажите, что требуется скопировать файлы из Dropbox в корневую папку для локального общего ресурса.</span><span class="sxs-lookup"><span data-stu-id="45bec-131">Specify that you want to copy files from Dropbox to the root folder for your on-premises file share.</span></span>

   ![Действие для создания файла](media/logic-apps-using-file-connector/create-file-filled.png)

5. <span data-ttu-id="45bec-133">После того как приложение логики скопирует файл, добавьте действие Outlook, которое будет отправлять сообщение электронной почты соответствующим пользователям, которые должны знать о новом файле.</span><span class="sxs-lookup"><span data-stu-id="45bec-133">After your logic app copies the file, add an Outlook action that sends an email so relevant users know about the new file.</span></span> <span data-ttu-id="45bec-134">Укажите адреса получателей, тему и текст сообщения.</span><span class="sxs-lookup"><span data-stu-id="45bec-134">Enter the recipients, title, and body of the email.</span></span> 

   <span data-ttu-id="45bec-135">В селекторе динамического содержимого можно выбрать выходные данные из соединителя файлов, чтобы добавить дополнительные сведения в сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="45bec-135">In the dynamic content selector, you can choose data outputs from the file connector so you can add more details to the email.</span></span>

   ![Действие для отправки электронного сообщения](media/logic-apps-using-file-connector/send-email.png)

6. <span data-ttu-id="45bec-137">Сохраните приложение логики.</span><span class="sxs-lookup"><span data-stu-id="45bec-137">Save your logic app.</span></span> <span data-ttu-id="45bec-138">Тестирование приложения путем загрузки файла в Dropbox.</span><span class="sxs-lookup"><span data-stu-id="45bec-138">Test your app by uploading a file to Dropbox.</span></span> <span data-ttu-id="45bec-139">Файл будет скопирован в локальную общую папку, а вы получите сообщение электронной почты об этой операции.</span><span class="sxs-lookup"><span data-stu-id="45bec-139">The file should get copied to the on-premises file share, and you should receive an email about the operation.</span></span>

   > [!TIP] 
   > <span data-ttu-id="45bec-140">Узнайте о возможностях [мониторинга приложений логики](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="45bec-140">Learn how to [monitor your logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="45bec-141">Поздравляем, вы только что получили работающее приложение логики, которое может подключаться к локальной файловой системе.</span><span class="sxs-lookup"><span data-stu-id="45bec-141">Congratulations, you now have a working logic app that can connect to your on-premises file system.</span></span> <span data-ttu-id="45bec-142">Попробуйте изучить другие функции, которые предлагает соединитель, например:</span><span class="sxs-lookup"><span data-stu-id="45bec-142">Try exploring other functionalities that the connector offers, for example:</span></span>

- <span data-ttu-id="45bec-143">Создание файла</span><span class="sxs-lookup"><span data-stu-id="45bec-143">Create file</span></span>
- <span data-ttu-id="45bec-144">List files in folder (Вывод списка файлов в папке)</span><span class="sxs-lookup"><span data-stu-id="45bec-144">List files in folder</span></span>
- <span data-ttu-id="45bec-145">Добавление файла</span><span class="sxs-lookup"><span data-stu-id="45bec-145">Append file</span></span>
- <span data-ttu-id="45bec-146">Удаление файла</span><span class="sxs-lookup"><span data-stu-id="45bec-146">Delete file</span></span>
- <span data-ttu-id="45bec-147">Получение содержимого файла</span><span class="sxs-lookup"><span data-stu-id="45bec-147">Get file content</span></span>
- <span data-ttu-id="45bec-148">Получение содержимого файла с помощью пути</span><span class="sxs-lookup"><span data-stu-id="45bec-148">Get file content using path</span></span>
- <span data-ttu-id="45bec-149">Получение метаданных файла</span><span class="sxs-lookup"><span data-stu-id="45bec-149">Get file metadata</span></span>
- <span data-ttu-id="45bec-150">Получение метаданных файла с помощью пути</span><span class="sxs-lookup"><span data-stu-id="45bec-150">Get file metadata using path</span></span>
- <span data-ttu-id="45bec-151">List files in root folder (Вывод списка файлов в корневой папке)</span><span class="sxs-lookup"><span data-stu-id="45bec-151">List files in root folder</span></span>
- <span data-ttu-id="45bec-152">Обновление файла</span><span class="sxs-lookup"><span data-stu-id="45bec-152">Update file</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="45bec-153">Просмотр Swagger</span><span class="sxs-lookup"><span data-stu-id="45bec-153">View the swagger</span></span>
<span data-ttu-id="45bec-154">Ознакомьтесь с [дополнительными сведениями о Swagger](/connectors/fileconnector/).</span><span class="sxs-lookup"><span data-stu-id="45bec-154">See the [swagger details](/connectors/fileconnector/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="45bec-155">Получение справки</span><span class="sxs-lookup"><span data-stu-id="45bec-155">Get help</span></span>

<span data-ttu-id="45bec-156">Чтобы задать вопросы, помочь другим пользователям и узнать, что делают другие пользователи, посетите [форум по Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="45bec-156">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="45bec-157">Чтобы улучшить Azure Logic Apps и соединители, голосуйте за идеи или предлагайте собственные на [сайте обратной связи Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="45bec-157">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="45bec-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="45bec-158">Next steps</span></span>

- <span data-ttu-id="45bec-159">[Подключение к локальным данным](../logic-apps/logic-apps-gateway-connection.md) из приложений логики</span><span class="sxs-lookup"><span data-stu-id="45bec-159">[Connect to on-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
- <span data-ttu-id="45bec-160">Дополнительные сведения о [корпоративной интеграции](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="45bec-160">Learn about [enterprise integration](../logic-apps/logic-apps-enterprise-integration-overview.md)</span></span>
