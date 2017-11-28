---
title: "tooon aaaConnect в локальной файловой системой приложения логики Azure | Документы Microsoft"
description: "Подключение локальной tooon файловых систем из рабочего процесса логику приложения через шлюз данных в локальной среде hello и connector файловой системы"
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
ms.openlocfilehash: beb5565293def4aba81f63f19e77d7498aac38c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-file-systems-from-logic-apps-with-hello-file-system-connector"></a><span data-ttu-id="128eb-104">Подключение локальной tooon файловых систем из логики приложений с помощью соединителя hello файловой системы</span><span class="sxs-lookup"><span data-stu-id="128eb-104">Connect tooon-premises file systems from logic apps with hello File System connector</span></span>

<span data-ttu-id="128eb-105">Подключение гибридного облака — центра toologic приложений, поэтому toomanage данных и безопасного доступа к локальным ресурсам, свои приложения логики можно использовать hello локальный шлюз данных.</span><span class="sxs-lookup"><span data-stu-id="128eb-105">Hybrid cloud connectivity is central toologic apps, so toomanage data and securely access on-premises resources, your logic apps can use hello on-premises data gateway.</span></span> <span data-ttu-id="128eb-106">В этой статье показано, как tooconnect tooan в локальной файловой системе с базового сценария: скопировать файл с tooa отправленного tooDropbox общая папка, а затем отправить сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="128eb-106">In this article, we show how tooconnect tooan on-premises file system with a basic scenario: copy a file that's uploaded tooDropbox tooa file share, then send an email.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="128eb-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="128eb-107">Prerequisites</span></span>

- <span data-ttu-id="128eb-108">Установка и настройка hello последней [локального шлюза данных](https://www.microsoft.com/download/details.aspx?id=53127).</span><span class="sxs-lookup"><span data-stu-id="128eb-108">Install and configure hello latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127).</span></span>
- <span data-ttu-id="128eb-109">Установка hello последнюю локального шлюза данных версии 1.15.6150.1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="128eb-109">Install hello latest on-premises data gateway, version 1.15.6150.1 or above.</span></span> <span data-ttu-id="128eb-110">[Шлюз данных toohello локального подключения](http://aka.ms/logicapps-gateway) списки hello действия.</span><span class="sxs-lookup"><span data-stu-id="128eb-110">[Connect toohello on-premises data gateway](http://aka.ms/logicapps-gateway) lists hello steps.</span></span> <span data-ttu-id="128eb-111">Hello шлюза должен устанавливаться на локальном компьютере, перед продолжением hello остальные шаги hello.</span><span class="sxs-lookup"><span data-stu-id="128eb-111">hello gateway must be installed on an on-premises machine before you can continue with hello rest of hello steps.</span></span>

## <a name="add-trigger-and-actions-for-connecting-tooyour-file-system"></a><span data-ttu-id="128eb-112">Добавление триггера и действия по подключению tooyour файловой системы</span><span class="sxs-lookup"><span data-stu-id="128eb-112">Add trigger and actions for connecting tooyour file system</span></span>

1. <span data-ttu-id="128eb-113">Создание приложения логики и добавление триггера Dropbox **При создании файла**</span><span class="sxs-lookup"><span data-stu-id="128eb-113">Create a logic app, and add this Dropbox trigger: **When a file is created**</span></span> 
2. <span data-ttu-id="128eb-114">В разделе hello триггер, выберите **следующий шаг** > **добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="128eb-114">Under hello trigger, choose **Next Step** > **Add an action**.</span></span> 
3. <span data-ttu-id="128eb-115">Введите в поле поиска hello, `file system` , чтобы просмотреть все поддерживаемые действия для соединителя hello файловой системы.</span><span class="sxs-lookup"><span data-stu-id="128eb-115">In hello search box, enter `file system` so you can view all supported actions for hello File System connector.</span></span>

   ![Поиск соединителя File](media/logic-apps-using-file-connector/search-file-connector.png)

2. <span data-ttu-id="128eb-117">Выберите hello **создать файл** действие и создать файловую систему tooyour соединения.</span><span class="sxs-lookup"><span data-stu-id="128eb-117">Choose hello **Create file** action, and create a connection tooyour file system.</span></span>

   <span data-ttu-id="128eb-118">Если у вас нет существующего подключения, не запрошенные toocreate один.</span><span class="sxs-lookup"><span data-stu-id="128eb-118">If you don't have an existing connection, you are prompted toocreate one.</span></span>

   1. <span data-ttu-id="128eb-119">Установите флажок **Connect via on-premises data gateway** (Подключение через локальный шлюз данных).</span><span class="sxs-lookup"><span data-stu-id="128eb-119">Choose **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="128eb-120">Отобразятся дополнительные свойства.</span><span class="sxs-lookup"><span data-stu-id="128eb-120">More properties appear.</span></span>
   2. <span data-ttu-id="128eb-121">Выберите корневую папку для файловой системы.</span><span class="sxs-lookup"><span data-stu-id="128eb-121">Select your root folder for your file system.</span></span>
      
       > [!NOTE]
       > <span data-ttu-id="128eb-122">Hello корневая папка является основной родительской папкой hello, который используется для относительных путей для всех действий, относящихся к файлам.</span><span class="sxs-lookup"><span data-stu-id="128eb-122">hello root folder is hello main parent folder, which is used for relative paths for all file-related actions.</span></span> <span data-ttu-id="128eb-123">Можно указать локальную папку на компьютере hello, где установлен hello локального шлюза данных, или может быть папка hello общую сетевую папку, hello машины могут иметь доступ к.</span><span class="sxs-lookup"><span data-stu-id="128eb-123">You can specify a local folder on hello machine where hello on-premises data gateway is installed, or hello folder can be a network share that hello machine can access.</span></span>

   3. <span data-ttu-id="128eb-124">Введите hello пользователя и пароль для шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="128eb-124">Enter hello username and password for hello gateway.</span></span>
   4. <span data-ttu-id="128eb-125">Выберите шлюз hello, установленного ранее.</span><span class="sxs-lookup"><span data-stu-id="128eb-125">Select hello gateway that you previously installed.</span></span>

       ![Настройка подключения](media/logic-apps-using-file-connector/create-file.png)

3. <span data-ttu-id="128eb-127">После ввода всех сведений о hello выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="128eb-127">After you provide all hello details, choose **Create**.</span></span> 

   <span data-ttu-id="128eb-128">Логика приложения настраивает и проверяет подключения, убедившись, что hello подключение работает правильно.</span><span class="sxs-lookup"><span data-stu-id="128eb-128">Logic Apps configures and tests your connection, making sure that hello connection works properly.</span></span> 
   <span data-ttu-id="128eb-129">Если подключение hello настроен правильно, можно увидеть параметры для действия hello, выбранного ранее.</span><span class="sxs-lookup"><span data-stu-id="128eb-129">If hello connection is set up correctly, you see options for hello action that you previously selected.</span></span> 
   <span data-ttu-id="128eb-130">Соединитель system Hello файл готов для использования.</span><span class="sxs-lookup"><span data-stu-id="128eb-130">hello file system connector is now ready for use.</span></span>

4. <span data-ttu-id="128eb-131">Укажите, требуется toocopy файлы из корневой папки общего банка данных toohello для файлового ресурса в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="128eb-131">Specify that you want toocopy files from Dropbox toohello root folder for your on-premises file share.</span></span>

   ![Действие для создания файла](media/logic-apps-using-file-connector/create-file-filled.png)

5. <span data-ttu-id="128eb-133">После файл hello копий логику приложения добавьте Outlook действие, которое отправляет сообщение электронной почты, поэтому соответствующие пользователи знают о hello новый файл.</span><span class="sxs-lookup"><span data-stu-id="128eb-133">After your logic app copies hello file, add an Outlook action that sends an email so relevant users know about hello new file.</span></span> <span data-ttu-id="128eb-134">Введите hello получателей, заголовок и текст hello электронной почты.</span><span class="sxs-lookup"><span data-stu-id="128eb-134">Enter hello recipients, title, and body of hello email.</span></span> 

   <span data-ttu-id="128eb-135">В hello динамического выделения содержимого вы можете выходных данных из файла соединителя hello, можно будет добавить дополнительные сведения о toohello по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="128eb-135">In hello dynamic content selector, you can choose data outputs from hello file connector so you can add more details toohello email.</span></span>

   ![Действие для отправки электронного сообщения](media/logic-apps-using-file-connector/send-email.png)

6. <span data-ttu-id="128eb-137">Сохраните приложение логики.</span><span class="sxs-lookup"><span data-stu-id="128eb-137">Save your logic app.</span></span> <span data-ttu-id="128eb-138">Протестируйте приложение, передав tooDropbox файла.</span><span class="sxs-lookup"><span data-stu-id="128eb-138">Test your app by uploading a file tooDropbox.</span></span> <span data-ttu-id="128eb-139">файл Hello должны получить скопированный toohello локальной общей папки и должно появиться сообщение электронной почты об операции hello.</span><span class="sxs-lookup"><span data-stu-id="128eb-139">hello file should get copied toohello on-premises file share, and you should receive an email about hello operation.</span></span>

   > [!TIP] 
   > <span data-ttu-id="128eb-140">Узнайте, каким образом слишком[Отслеживайте свои приложения логики](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="128eb-140">Learn how too[monitor your logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="128eb-141">Поздравляем, вы получите работающем приложении логики, можно подключиться tooyour в локальной файловой системе.</span><span class="sxs-lookup"><span data-stu-id="128eb-141">Congratulations, you now have a working logic app that can connect tooyour on-premises file system.</span></span> <span data-ttu-id="128eb-142">Попробуйте выполните изучение других функций, которые hello соединителя предложения, например:</span><span class="sxs-lookup"><span data-stu-id="128eb-142">Try exploring other functionalities that hello connector offers, for example:</span></span>

- <span data-ttu-id="128eb-143">Создание файла</span><span class="sxs-lookup"><span data-stu-id="128eb-143">Create file</span></span>
- <span data-ttu-id="128eb-144">List files in folder (Вывод списка файлов в папке)</span><span class="sxs-lookup"><span data-stu-id="128eb-144">List files in folder</span></span>
- <span data-ttu-id="128eb-145">Добавление файла</span><span class="sxs-lookup"><span data-stu-id="128eb-145">Append file</span></span>
- <span data-ttu-id="128eb-146">Удаление файла</span><span class="sxs-lookup"><span data-stu-id="128eb-146">Delete file</span></span>
- <span data-ttu-id="128eb-147">Получение содержимого файла</span><span class="sxs-lookup"><span data-stu-id="128eb-147">Get file content</span></span>
- <span data-ttu-id="128eb-148">Получение содержимого файла с помощью пути</span><span class="sxs-lookup"><span data-stu-id="128eb-148">Get file content using path</span></span>
- <span data-ttu-id="128eb-149">Получение метаданных файла</span><span class="sxs-lookup"><span data-stu-id="128eb-149">Get file metadata</span></span>
- <span data-ttu-id="128eb-150">Получение метаданных файла с помощью пути</span><span class="sxs-lookup"><span data-stu-id="128eb-150">Get file metadata using path</span></span>
- <span data-ttu-id="128eb-151">List files in root folder (Вывод списка файлов в корневой папке)</span><span class="sxs-lookup"><span data-stu-id="128eb-151">List files in root folder</span></span>
- <span data-ttu-id="128eb-152">Обновление файла</span><span class="sxs-lookup"><span data-stu-id="128eb-152">Update file</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="128eb-153">Представление hello swagger</span><span class="sxs-lookup"><span data-stu-id="128eb-153">View hello swagger</span></span>
<span data-ttu-id="128eb-154">В разделе hello [swagger сведения](/connectors/fileconnector/).</span><span class="sxs-lookup"><span data-stu-id="128eb-154">See hello [swagger details](/connectors/fileconnector/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="128eb-155">Получение справки</span><span class="sxs-lookup"><span data-stu-id="128eb-155">Get help</span></span>

<span data-ttu-id="128eb-156">вопросы tooask ответить на вопросы и узнайте, какие другие логику приложения Azure пользователи делают, посетите hello [форуме по Azure логику приложений](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="128eb-156">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="128eb-157">toohelp улучшить логику приложения Azure и соединителей, проголосовать или отправить идеями hello [веб-сайт отзывов пользователей приложения логики Azure](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="128eb-157">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="128eb-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="128eb-158">Next steps</span></span>

- <span data-ttu-id="128eb-159">[Подключение к данным локальной tooon](../logic-apps/logic-apps-gateway-connection.md) из приложений логики</span><span class="sxs-lookup"><span data-stu-id="128eb-159">[Connect tooon-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
- <span data-ttu-id="128eb-160">Дополнительные сведения о [корпоративной интеграции](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="128eb-160">Learn about [enterprise integration](../logic-apps/logic-apps-enterprise-integration-overview.md)</span></span>
