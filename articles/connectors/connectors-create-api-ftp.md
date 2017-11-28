---
title: "aaaLearn как toouse hello соединителя FTP в приложениях для логики | Документы Microsoft"
description: "Создание приложений логики с помощью службы приложений Azure. Подключите toomanage сервера tooFTP файлов. Вы можете выполнять различные действия, такие как отправка, обновление, получение и удаление файлов на FTP-сервере."
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
tags: connectors
ms.assetid: d83c55fe-eb59-4b7b-a5ec-afac5c772616
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/22/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a7020df2005ebb34fc569627ae0516b8528cc7a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-ftp-connector"></a><span data-ttu-id="d9e37-105">Начало работы с соединителем hello FTP</span><span class="sxs-lookup"><span data-stu-id="d9e37-105">Get started with hello FTP connector</span></span>
<span data-ttu-id="d9e37-106">Использовать соединитель toomonitor hello FTP, управлять и создания файлов с FTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="d9e37-106">Use hello FTP connector toomonitor, manage and create files on an  FTP server.</span></span> 

<span data-ttu-id="d9e37-107">toouse [всех соединителей](apis-list.md), необходимо сначала toocreate приложения логики.</span><span class="sxs-lookup"><span data-stu-id="d9e37-107">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="d9e37-108">Вы можете начать с [создания приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="d9e37-108">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooftp"></a><span data-ttu-id="d9e37-109">Подключение tooFTP</span><span class="sxs-lookup"><span data-stu-id="d9e37-109">Connect tooFTP</span></span>
<span data-ttu-id="d9e37-110">Логика приложения можно получить доступ к любой службы, необходимо сначала toocreate *подключения* toohello службы.</span><span class="sxs-lookup"><span data-stu-id="d9e37-110">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="d9e37-111">Таким образом вы установите [соединение](connectors-overview.md) между приложением логики и другой службой.</span><span class="sxs-lookup"><span data-stu-id="d9e37-111">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-tooftp"></a><span data-ttu-id="d9e37-112">Создание tooFTP подключения</span><span class="sxs-lookup"><span data-stu-id="d9e37-112">Create a connection tooFTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooFTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a><span data-ttu-id="d9e37-113">Использование триггера FTP</span><span class="sxs-lookup"><span data-stu-id="d9e37-113">Use a FTP trigger</span></span>
<span data-ttu-id="d9e37-114">Триггер — это событие, которое может быть рабочий процесс используется toostart hello, определенной в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="d9e37-114">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="d9e37-115">[Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="d9e37-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="d9e37-116">Hello FTP соединителя требуется FTP-сервер, который доступен из Интернета hello и настроен toooperate ПАССИВНЫЙ режим.</span><span class="sxs-lookup"><span data-stu-id="d9e37-116">hello FTP connector requires an FTP server that  is accessible from hello Internet and is configured toooperate with PASSIVE mode.</span></span> <span data-ttu-id="d9e37-117">Кроме того, соединитель hello FTP — **не совместим с неявное FTPS (FTP через SSL)**.</span><span class="sxs-lookup"><span data-stu-id="d9e37-117">Also, hello FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span></span> <span data-ttu-id="d9e37-118">Hello FTP connector поддерживает только явные FTPS (FTP через SSL).</span><span class="sxs-lookup"><span data-stu-id="d9e37-118">hello FTP connector only supports explicit FTPS (FTP over SSL).</span></span>  
> 
> 

<span data-ttu-id="d9e37-119">В этом примере будет показано как toouse hello **FTP - при добавлении или изменении файла** триггера tooinitiate логику приложения рабочего процесса, при добавлении файла, или изменена на FTP-сервере.</span><span class="sxs-lookup"><span data-stu-id="d9e37-119">In this example, I will show you how toouse hello **FTP - When a file is added or modified** trigger tooinitiate a logic app workflow when a file is added to, or modified on, an FTP server.</span></span> <span data-ttu-id="d9e37-120">В примере enterprise можно использовать этот триггер toomonitor FTP-папка для новых файлов, которые представляют заказы от клиентов.</span><span class="sxs-lookup"><span data-stu-id="d9e37-120">In an enterprise example, you could use this trigger toomonitor an FTP folder for new files that represent orders from customers.</span></span>  <span data-ttu-id="d9e37-121">Затем можно использовать действие соединителя FTP например **получение содержимого файла** tooget hello содержимое заказа hello для дальнейшей обработки и хранения в базе данных заказов.</span><span class="sxs-lookup"><span data-stu-id="d9e37-121">You could then use an FTP connector action such as **Get file content** tooget hello contents of hello order for further processing and storage in your orders database.</span></span>

1. <span data-ttu-id="d9e37-122">Введите *ftp* в поле поиска hello в конструкторе приложений логики hello выберите hello **FTP - при добавлении или изменении файла** триггера</span><span class="sxs-lookup"><span data-stu-id="d9e37-122">Enter *ftp* in hello search box on hello logic apps designer then select hello **FTP - When a file is added or modified**  trigger</span></span>   
   <span data-ttu-id="d9e37-123">![Изображение 1. Триггер FTP](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="d9e37-123">![FTP trigger image 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span></span>  
   <span data-ttu-id="d9e37-124">Hello **при добавлении или изменении файла** открывает элемент управления</span><span class="sxs-lookup"><span data-stu-id="d9e37-124">hello **When a file is added or modified** control opens up</span></span>  
   <span data-ttu-id="d9e37-125">![Изображение 2. Триггер FTP](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="d9e37-125">![FTP trigger image 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span></span>  
2. <span data-ttu-id="d9e37-126">Выберите hello **...**  на hello правой части элемента управления hello.</span><span class="sxs-lookup"><span data-stu-id="d9e37-126">Select hello **...** located on hello right side of hello control.</span></span> <span data-ttu-id="d9e37-127">Это открывает элемент управления для выбора папки hello</span><span class="sxs-lookup"><span data-stu-id="d9e37-127">This opens hello folder picker control</span></span>  
   <span data-ttu-id="d9e37-128">![Изображение 3. Триггер FTP](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span><span class="sxs-lookup"><span data-stu-id="d9e37-128">![FTP trigger image 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span></span>  
3. <span data-ttu-id="d9e37-129">Выберите hello  **>**  (стрелка вправо) и найдите папку hello toofind, чтобы получить toomonitor новые или измененные файлы.</span><span class="sxs-lookup"><span data-stu-id="d9e37-129">Select hello **>** (right arrow) and browse toofind hello folder that you want toomonitor for new or modified files.</span></span> <span data-ttu-id="d9e37-130">Выберите папку hello и обратите внимание, папка hello теперь отображается в hello **папки** элемента управления.</span><span class="sxs-lookup"><span data-stu-id="d9e37-130">Select hello folder and notice hello folder is now displayed in hello **Folder** control.</span></span>  
   <span data-ttu-id="d9e37-131">![Изображение 4. Триггер FTP](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span><span class="sxs-lookup"><span data-stu-id="d9e37-131">![FTP trigger image 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span></span>   

<span data-ttu-id="d9e37-132">На этом этапе приложение логики, были настроены триггер начала запуска hello других триггеров и действий в рабочем процессе hello при изменении или созданы в определенной папке FTP hello файла.</span><span class="sxs-lookup"><span data-stu-id="d9e37-132">At this point, your logic app has been configured with a trigger that will begin a run of hello other triggers and actions in hello workflow when a file is either modified or created in hello specific FTP folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="d9e37-133">Логика приложения toobe функциональной должен содержать хотя бы один триггер и одно действие.</span><span class="sxs-lookup"><span data-stu-id="d9e37-133">For a logic app toobe functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="d9e37-134">Следуйте указаниям hello hello Далее раздел tooadd действие.</span><span class="sxs-lookup"><span data-stu-id="d9e37-134">Follow hello steps in hello next section tooadd an action.</span></span>  
> 
> 

## <a name="use-a-ftp-action"></a><span data-ttu-id="d9e37-135">Использование действия FTP</span><span class="sxs-lookup"><span data-stu-id="d9e37-135">Use a FTP action</span></span>
<span data-ttu-id="d9e37-136">Действие — операции, выполняемые hello рабочего процесса, определенного в приложении логику.</span><span class="sxs-lookup"><span data-stu-id="d9e37-136">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="d9e37-137">[Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="d9e37-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="d9e37-138">Теперь, когда вы добавили триггер, выполните эти шаги tooadd действие, которое получит содержимое hello hello нового или измененного файла, найден триггером hello.</span><span class="sxs-lookup"><span data-stu-id="d9e37-138">Now that you have added a trigger, follow these steps tooadd an action that will get hello contents of hello new or modified file found by hello trigger.</span></span>    

1. <span data-ttu-id="d9e37-139">Выберите **+ новый шаг** tooadd hello hello действие tooget hello содержимое hello файла на сервере hello FTP</span><span class="sxs-lookup"><span data-stu-id="d9e37-139">Select **+ New step** tooadd hello hello action tooget hello contents of hello file on hello FTP server</span></span>  
2. <span data-ttu-id="d9e37-140">Выберите hello **добавить действие** ссылку.</span><span class="sxs-lookup"><span data-stu-id="d9e37-140">Select hello **Add an action** link.</span></span>  
   <span data-ttu-id="d9e37-141">![Изображение 1. Действие FTP](./media/connectors-create-api-ftp/ftp-action-1.png)</span><span class="sxs-lookup"><span data-stu-id="d9e37-141">![FTP action image 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span></span>  
3. <span data-ttu-id="d9e37-142">Введите *FTP* toosearch для всех действий, связанных с tooFTP.</span><span class="sxs-lookup"><span data-stu-id="d9e37-142">Enter *FTP* toosearch for all actions related tooFTP.</span></span>
4. <span data-ttu-id="d9e37-143">Выберите **FTP - получение содержимого файла** как hello tootake действие, если новый или измененный файл находится в папке hello FTP.</span><span class="sxs-lookup"><span data-stu-id="d9e37-143">Select **FTP - Get file content**  as hello action tootake when a new or modified file is found in hello FTP folder.</span></span>      
   <span data-ttu-id="d9e37-144">![Изображение 2. Действие FTP](./media/connectors-create-api-ftp/ftp-action-2.png)</span><span class="sxs-lookup"><span data-stu-id="d9e37-144">![FTP action image 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span></span>  
   <span data-ttu-id="d9e37-145">Hello **получение содержимого файла** управления откроется.</span><span class="sxs-lookup"><span data-stu-id="d9e37-145">hello **Get file content** control opens.</span></span> <span data-ttu-id="d9e37-146">**Примечание**: вы будет запрашиваемые tooauthorize вашей tooaccess логику приложения, на FTP-сервер учетную запись, если вы еще не сделали это.</span><span class="sxs-lookup"><span data-stu-id="d9e37-146">**Note**: you will be prompted tooauthorize your logic app tooaccess your FTP server account if you have not done so previously.</span></span>  
   <span data-ttu-id="d9e37-147">![Изображение 3. Действие FTP](./media/connectors-create-api-ftp/ftp-action-3.png)</span><span class="sxs-lookup"><span data-stu-id="d9e37-147">![FTP action image 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span></span>   
5. <span data-ttu-id="d9e37-148">Выберите hello **файл** управления (hello пробелы. он располагается ниже **ФАЙЛ***).</span><span class="sxs-lookup"><span data-stu-id="d9e37-148">Select hello **File** control (hello white space located below **FILE***).</span></span> <span data-ttu-id="d9e37-149">Здесь можно использовать любой из hello различные свойства из hello нового или измененного файла, найден hello FTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="d9e37-149">Here, you can use any of hello various properties from hello new or modified file found on hello FTP server.</span></span>  
6. <span data-ttu-id="d9e37-150">Выберите hello **содержимое файла** параметр.</span><span class="sxs-lookup"><span data-stu-id="d9e37-150">Select hello **File content** option.</span></span>  
   <span data-ttu-id="d9e37-151">![Изображение 4. Действие FTP](./media/connectors-create-api-ftp/ftp-action-4.png)</span><span class="sxs-lookup"><span data-stu-id="d9e37-151">![FTP action image 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span></span>   
7. <span data-ttu-id="d9e37-152">обновлен элемент управления Hello, указывающее, что hello **FTP - получение содержимого файла** действие получит hello *содержимое файла* hello нового или измененного файла на сервере hello FTP.</span><span class="sxs-lookup"><span data-stu-id="d9e37-152">hello control is updated, indicating that hello **FTP - Get file content** action will get hello *file content* of hello new or modified file on hello FTP server.</span></span>      
   <span data-ttu-id="d9e37-153">![Изображение 5. Действие FTP](./media/connectors-create-api-ftp/ftp-action-5.png)</span><span class="sxs-lookup"><span data-stu-id="d9e37-153">![FTP action image 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span></span>     
8. <span data-ttu-id="d9e37-154">Сохранить результаты работы, а затем добавить tootest папки FTP toohello файл рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="d9e37-154">Save your work then add a file toohello FTP folder tootest your workflow.</span></span>    

<span data-ttu-id="d9e37-155">На этом этапе приложение hello логику было настроено toomonitor триггер папку на FTP-сервер и инициировать hello рабочего процесса при обнаружении нового файла или открытии файла на сервере hello FTP.</span><span class="sxs-lookup"><span data-stu-id="d9e37-155">At this point, hello logic app has been configured with a trigger toomonitor a folder on an FTP server and initiate hello workflow when it finds either a new file or a modified file on hello FTP server.</span></span> 

<span data-ttu-id="d9e37-156">приложение Hello логику также настроен hello содержимое tooget действие hello нового или измененного файла.</span><span class="sxs-lookup"><span data-stu-id="d9e37-156">hello logic app also has been configured with an action tooget hello contents of hello new or modified file.</span></span>

<span data-ttu-id="d9e37-157">Теперь можно добавить другое действие, например hello [SQL Server — вставить строку](connectors-create-api-sqlazure.md) содержимое hello tooinsert действие hello нового или измененного файла в таблицу базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="d9e37-157">You can now add another action such as hello [SQL Server - insert row](connectors-create-api-sqlazure.md) action tooinsert hello contents of hello new or modified file into a SQL database table.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="d9e37-158">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="d9e37-158">Connector-specific details</span></span>

<span data-ttu-id="d9e37-159">Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/ftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="d9e37-159">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/ftpconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d9e37-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d9e37-160">Next Steps</span></span>
[<span data-ttu-id="d9e37-161">Создайте приложение логики</span><span class="sxs-lookup"><span data-stu-id="d9e37-161">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

