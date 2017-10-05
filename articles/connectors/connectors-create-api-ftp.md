---
title: "Использование соединителя FTP в приложениях логики | Документация Майкрософт"
description: "Создание приложений логики с помощью службы приложений Azure. Подключение к FTP-серверу для управления файлами. Вы можете выполнять различные действия, такие как отправка, обновление, получение и удаление файлов на FTP-сервере."
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
ms.openlocfilehash: 61bfbedfd4f1e84b6976099323a32f3a720634c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-ftp-connector"></a><span data-ttu-id="79ead-105">Начало работы с соединителем FTP</span><span class="sxs-lookup"><span data-stu-id="79ead-105">Get started with the FTP connector</span></span>
<span data-ttu-id="79ead-106">Соединитель FTP можно использовать для создания и мониторинга файлов на FTP-сервере, а также для управления ими.</span><span class="sxs-lookup"><span data-stu-id="79ead-106">Use the FTP connector to monitor, manage and create files on an  FTP server.</span></span> 

<span data-ttu-id="79ead-107">Чтобы использовать [соединитель](apis-list.md), сначала нужно создать приложение логики.</span><span class="sxs-lookup"><span data-stu-id="79ead-107">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="79ead-108">Вы можете начать с [создания приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="79ead-108">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-ftp"></a><span data-ttu-id="79ead-109">Подключение к FTP</span><span class="sxs-lookup"><span data-stu-id="79ead-109">Connect to FTP</span></span>
<span data-ttu-id="79ead-110">Чтобы обеспечить доступ приложения логики к какой-либо службе, сначала необходимо создать *подключение* к этой службе.</span><span class="sxs-lookup"><span data-stu-id="79ead-110">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="79ead-111">Таким образом вы установите [соединение](connectors-overview.md) между приложением логики и другой службой.</span><span class="sxs-lookup"><span data-stu-id="79ead-111">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-ftp"></a><span data-ttu-id="79ead-112">Создание подключения к FTP</span><span class="sxs-lookup"><span data-stu-id="79ead-112">Create a connection to FTP</span></span>
> [!INCLUDE [Steps to create a connection to FTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a><span data-ttu-id="79ead-113">Использование триггера FTP</span><span class="sxs-lookup"><span data-stu-id="79ead-113">Use a FTP trigger</span></span>
<span data-ttu-id="79ead-114">Триггер — это событие, которое можно использовать для запуска рабочего процесса, определенного в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="79ead-114">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="79ead-115">[Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="79ead-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="79ead-116">Для соединителя FTP требуется доступный через Интернет FTP-сервер, который настроен для работы с пассивным режимом.</span><span class="sxs-lookup"><span data-stu-id="79ead-116">The FTP connector requires an FTP server that  is accessible from the Internet and is configured to operate with PASSIVE mode.</span></span> <span data-ttu-id="79ead-117">Кроме того, соединитель FTP **не поддерживает неявную конфигурацию FTPS (FTP через SSL)**.</span><span class="sxs-lookup"><span data-stu-id="79ead-117">Also, the FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span></span> <span data-ttu-id="79ead-118">Он поддерживает только явную конфигурацию FTPS (FTP через SSL).</span><span class="sxs-lookup"><span data-stu-id="79ead-118">The FTP connector only supports explicit FTPS (FTP over SSL).</span></span>  
> 
> 

<span data-ttu-id="79ead-119">Из этого примера вы узнаете, как использовать триггер **FTP - When a file is added or modified** (FTP — при добавлении или изменении файла) для запуска рабочего процесса приложения логики при добавлении или изменении файла на FTP-сервере.</span><span class="sxs-lookup"><span data-stu-id="79ead-119">In this example, I will show you how to use the **FTP - When a file is added or modified** trigger to initiate a logic app workflow when a file is added to, or modified on, an FTP server.</span></span> <span data-ttu-id="79ead-120">В контексте предприятия можно использовать этот триггер, чтобы отслеживать в папке FTP новые файлы, представляющие заказы от клиентов.</span><span class="sxs-lookup"><span data-stu-id="79ead-120">In an enterprise example, you could use this trigger to monitor an FTP folder for new files that represent orders from customers.</span></span>  <span data-ttu-id="79ead-121">Вы также можете использовать действие соединителя FTP **Get file content** (Получение содержимого файла), чтобы получить содержимое заказа для дальнейшей обработки и сохранения в базе данных заказов.</span><span class="sxs-lookup"><span data-stu-id="79ead-121">You could then use an FTP connector action such as **Get file content** to get the contents of the order for further processing and storage in your orders database.</span></span>

1. <span data-ttu-id="79ead-122">В конструкторе приложений логики в поле поиска введите *sftp*, а затем выберите триггер **SFTP - When a file is added or modified** (SFTP — при добавлении или изменении файла).</span><span class="sxs-lookup"><span data-stu-id="79ead-122">Enter *ftp* in the search box on the logic apps designer then select the **FTP - When a file is added or modified**  trigger</span></span>   
   <span data-ttu-id="79ead-123">![Изображение 1. Триггер FTP](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="79ead-123">![FTP trigger image 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span></span>  
   <span data-ttu-id="79ead-124">Откроется элемент управления **When a file is added or modified** (При добавлении или изменении файла).</span><span class="sxs-lookup"><span data-stu-id="79ead-124">The **When a file is added or modified** control opens up</span></span>  
   <span data-ttu-id="79ead-125">![Изображение 2. Триггер FTP](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="79ead-125">![FTP trigger image 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span></span>  
2. <span data-ttu-id="79ead-126">В правой части элемента управления щелкните **…**.</span><span class="sxs-lookup"><span data-stu-id="79ead-126">Select the **...** located on the right side of the control.</span></span> <span data-ttu-id="79ead-127">Откроется элемент управления средства выбора папок.</span><span class="sxs-lookup"><span data-stu-id="79ead-127">This opens the folder picker control</span></span>  
   <span data-ttu-id="79ead-128">![Изображение 3. Триггер FTP](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span><span class="sxs-lookup"><span data-stu-id="79ead-128">![FTP trigger image 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span></span>  
3. <span data-ttu-id="79ead-129">Щелкните **>** (стрелку вправо) и перейдите к папке, в которой требуется отслеживать добавление или изменение файлов.</span><span class="sxs-lookup"><span data-stu-id="79ead-129">Select the **>** (right arrow) and browse to find the folder that you want to monitor for new or modified files.</span></span> <span data-ttu-id="79ead-130">Выберите папку и обратите внимание, что теперь она отображается в элементе управления **Папка**.</span><span class="sxs-lookup"><span data-stu-id="79ead-130">Select the folder and notice the folder is now displayed in the **Folder** control.</span></span>  
   <span data-ttu-id="79ead-131">![Изображение 4. Триггер FTP](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span><span class="sxs-lookup"><span data-stu-id="79ead-131">![FTP trigger image 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span></span>   

<span data-ttu-id="79ead-132">На этом этапе для приложения логики настроен триггер, который будет активировать другие триггеры и действия в рабочем процессе при изменении или создании файла в указанной папке FTP.</span><span class="sxs-lookup"><span data-stu-id="79ead-132">At this point, your logic app has been configured with a trigger that will begin a run of the other triggers and actions in the workflow when a file is either modified or created in the specific FTP folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="79ead-133">Чтобы приложение логики функционировало, оно должно содержать по крайней мере один триггер и одно действие.</span><span class="sxs-lookup"><span data-stu-id="79ead-133">For a logic app to be functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="79ead-134">Шаги по добавлению действия описаны в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="79ead-134">Follow the steps in the next section to add an action.</span></span>  
> 
> 

## <a name="use-a-ftp-action"></a><span data-ttu-id="79ead-135">Использование действия FTP</span><span class="sxs-lookup"><span data-stu-id="79ead-135">Use a FTP action</span></span>
<span data-ttu-id="79ead-136">Действие — это операция, выполняемая рабочим процессом, определенным в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="79ead-136">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="79ead-137">[Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="79ead-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="79ead-138">Добавив триггер, выполните следующие шаги, чтобы добавить действие для получения содержимого нового или измененного файла, найденного с помощью триггера.</span><span class="sxs-lookup"><span data-stu-id="79ead-138">Now that you have added a trigger, follow these steps to add an action that will get the contents of the new or modified file found by the trigger.</span></span>    

1. <span data-ttu-id="79ead-139">Щелкните **+ Новый шаг**, чтобы добавить действие для получения содержимого файла на FTP-сервере.</span><span class="sxs-lookup"><span data-stu-id="79ead-139">Select **+ New step** to add the the action to get the contents of the file on the FTP server</span></span>  
2. <span data-ttu-id="79ead-140">Щелкните ссылку **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="79ead-140">Select the **Add an action** link.</span></span>  
   <span data-ttu-id="79ead-141">![Изображение 1. Действие FTP](./media/connectors-create-api-ftp/ftp-action-1.png)</span><span class="sxs-lookup"><span data-stu-id="79ead-141">![FTP action image 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span></span>  
3. <span data-ttu-id="79ead-142">Введите *FTP* в поле поиска, чтобы найти все действия, связанные с FTP.</span><span class="sxs-lookup"><span data-stu-id="79ead-142">Enter *FTP* to search for all actions related to FTP.</span></span>
4. <span data-ttu-id="79ead-143">Выберите действие **FTP - Get file content** (FTP — получение содержимого файла), которое будет выполняться при обнаружении нового или измененного файла в папке FTP.</span><span class="sxs-lookup"><span data-stu-id="79ead-143">Select **FTP - Get file content**  as the action to take when a new or modified file is found in the FTP folder.</span></span>      
   <span data-ttu-id="79ead-144">![Изображение 2. Действие FTP](./media/connectors-create-api-ftp/ftp-action-2.png)</span><span class="sxs-lookup"><span data-stu-id="79ead-144">![FTP action image 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span></span>  
   <span data-ttu-id="79ead-145">Откроется элемент управления **Get file content** (Получение содержимого файла).</span><span class="sxs-lookup"><span data-stu-id="79ead-145">The **Get file content** control opens.</span></span> <span data-ttu-id="79ead-146">**Примечание**. Вам будет предложено авторизовать приложение логики для доступа к учетной записи FTP-сервера, если вы еще не сделали это.</span><span class="sxs-lookup"><span data-stu-id="79ead-146">**Note**: you will be prompted to authorize your logic app to access your FTP server account if you have not done so previously.</span></span>  
   <span data-ttu-id="79ead-147">![Изображение 3. Действие FTP](./media/connectors-create-api-ftp/ftp-action-3.png)</span><span class="sxs-lookup"><span data-stu-id="79ead-147">![FTP action image 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span></span>   
5. <span data-ttu-id="79ead-148">Выберите элемент управления **Файл** (пустое поле, расположенное под надписью **Файл***).</span><span class="sxs-lookup"><span data-stu-id="79ead-148">Select the **File** control (the white space located below **FILE***).</span></span> <span data-ttu-id="79ead-149">Здесь можно использовать одно из множества свойств нового или измененного файла, найденного на FTP-сервере.</span><span class="sxs-lookup"><span data-stu-id="79ead-149">Here, you can use any of the various properties from the new or modified file found on the FTP server.</span></span>  
6. <span data-ttu-id="79ead-150">Выберите параметр **Содержимое файла**.</span><span class="sxs-lookup"><span data-stu-id="79ead-150">Select the **File content** option.</span></span>  
   <span data-ttu-id="79ead-151">![Изображение 4. Действие FTP](./media/connectors-create-api-ftp/ftp-action-4.png)</span><span class="sxs-lookup"><span data-stu-id="79ead-151">![FTP action image 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span></span>   
7. <span data-ttu-id="79ead-152">Элемент управления будет обновлен. Значит, действие **FTP - Get file content** (FTP — получение содержимого файла) получит *содержимое* нового или измененного файла на FTP-сервере.</span><span class="sxs-lookup"><span data-stu-id="79ead-152">The control is updated, indicating that the **FTP - Get file content** action will get the *file content* of the new or modified file on the FTP server.</span></span>      
   <span data-ttu-id="79ead-153">![Изображение 5. Действие FTP](./media/connectors-create-api-ftp/ftp-action-5.png)</span><span class="sxs-lookup"><span data-stu-id="79ead-153">![FTP action image 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span></span>     
8. <span data-ttu-id="79ead-154">Сохраните внесенные изменения, а затем добавьте файл в папку FTP, чтобы протестировать рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="79ead-154">Save your work then add a file to the FTP folder to test your workflow.</span></span>    

<span data-ttu-id="79ead-155">На этом этапе для приложения логики настроен триггер, который отслеживает папку на FTP-сервере и запускает рабочий процесс при обнаружении в ней нового или измененного файла.</span><span class="sxs-lookup"><span data-stu-id="79ead-155">At this point, the logic app has been configured with a trigger to monitor a folder on an FTP server and initiate the workflow when it finds either a new file or a modified file on the FTP server.</span></span> 

<span data-ttu-id="79ead-156">Кроме того, для приложения логики настроено действие, которое получает содержимое нового или измененного файла.</span><span class="sxs-lookup"><span data-stu-id="79ead-156">The logic app also has been configured with an action to get the contents of the new or modified file.</span></span>

<span data-ttu-id="79ead-157">Теперь вы можете добавить другое действие, например [SQL Server - insert row](connectors-create-api-sqlazure.md) (SQL Server — вставка строки), которое будет вставлять содержимое нового или измененного файла в таблицу базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="79ead-157">You can now add another action such as the [SQL Server - insert row](connectors-create-api-sqlazure.md) action to insert the contents of the new or modified file into a SQL database table.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="79ead-158">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="79ead-158">Connector-specific details</span></span>

<span data-ttu-id="79ead-159">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/ftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="79ead-159">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/ftpconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="79ead-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="79ead-160">Next Steps</span></span>
[<span data-ttu-id="79ead-161">Создайте приложение логики</span><span class="sxs-lookup"><span data-stu-id="79ead-161">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

