---
title: "с помощью Socket.io приложения aaaNode.js | Документы Microsoft"
description: "Узнайте, как socket.io toouse в node.js приложении, размещенном в Azure."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 7f9435e0-7732-4aa1-a4df-ea0e894b847f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 47c6c4a748938959315b880340f41f31faab4ea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a><span data-ttu-id="f4b34-103">Создание приложения для разговора Node.js с Socket.IO в облачной службе Azure</span><span class="sxs-lookup"><span data-stu-id="f4b34-103">Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service</span></span>
<span data-ttu-id="f4b34-104">Socket.IO обеспечивает связь в режиме реального времени между сервером и клиентами node.js.</span><span class="sxs-lookup"><span data-stu-id="f4b34-104">Socket.IO provides realtime communication between between your node.js server and clients.</span></span> <span data-ttu-id="f4b34-105">В этом учебнике рассматривается размещение приложения для разговора на основе Socket.IO в Azure.</span><span class="sxs-lookup"><span data-stu-id="f4b34-105">This tutorial will walk you through hosting a socket.IO based chat application on Azure.</span></span> <span data-ttu-id="f4b34-106">Дополнительные сведения о Socket.IO см. на веб-сайте <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="f4b34-106">For more information on Socket.IO, see <http://socket.io/>.</span></span>

<span data-ttu-id="f4b34-107">Снимок экрана приложения hello завершения используется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f4b34-107">A screenshot of hello completed application is below:</span></span>

![Окно браузера, отображение hello службе, размещенной в Azure][completed-app]  

## <a name="prerequisites"></a><span data-ttu-id="f4b34-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f4b34-109">Prerequisites</span></span>
<span data-ttu-id="f4b34-110">Убедитесь, что hello следующих продуктов и версий, установленных toosuccessfully hello полный пример в этой статье:</span><span class="sxs-lookup"><span data-stu-id="f4b34-110">Ensure that hello following products and versions are installed toosuccessfully complete hello example in this article:</span></span>

* <span data-ttu-id="f4b34-111">установить [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx);</span><span class="sxs-lookup"><span data-stu-id="f4b34-111">Install [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span></span>
* <span data-ttu-id="f4b34-112">Установите [Node.js](https://nodejs.org/download/)</span><span class="sxs-lookup"><span data-stu-id="f4b34-112">Install [Node.js](https://nodejs.org/download/)</span></span>
* <span data-ttu-id="f4b34-113">Установите [Python версии 2.7.10](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="f4b34-113">Install [Python version 2.7.10](https://www.python.org/)</span></span>

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="f4b34-114">Создание проекта облачной службы</span><span class="sxs-lookup"><span data-stu-id="f4b34-114">Create a Cloud Service Project</span></span>
<span data-ttu-id="f4b34-115">Hello следующие действия создадут hello проекта облачной службы, где будет размещаться приложение Socket.IO hello.</span><span class="sxs-lookup"><span data-stu-id="f4b34-115">hello following steps create hello cloud service project that will host hello Socket.IO application.</span></span>

1. <span data-ttu-id="f4b34-116">Из hello **меню "Пуск"** или **рабочий стол**, поиск **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="f4b34-116">From hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="f4b34-117">Щелкните правой кнопкой мыши **Windows PowerShell** и выберите **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="f4b34-117">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Значок Azure PowerShell][powershell-menu]
2. <span data-ttu-id="f4b34-119">Сначала создайте каталог **c:\\node**.</span><span class="sxs-lookup"><span data-stu-id="f4b34-119">Create a directory called **c:\\node**.</span></span> 
   
        PS C:\> md node
3. <span data-ttu-id="f4b34-120">Измените каталоги toohello **c:\\узел** каталог</span><span class="sxs-lookup"><span data-stu-id="f4b34-120">Change directories toohello **c:\\node** directory</span></span>
   
        PS C:\> cd node
4. <span data-ttu-id="f4b34-121">Введите следующие команды toocreate новое решение с именем hello **chatapp** и рабочей роли с названием **WorkerRole1**:</span><span class="sxs-lookup"><span data-stu-id="f4b34-121">Enter hello following commands toocreate a new solution named **chatapp** and a worker role named **WorkerRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    <span data-ttu-id="f4b34-122">Вы увидите hello следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="f4b34-122">You will see hello following response:</span></span>
   
    ![Вывод Hello hello новый azureservice и добавить azurenodeworkerrolecmdlets](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-hello-chat-example"></a><span data-ttu-id="f4b34-124">Загрузите hello пример чата</span><span class="sxs-lookup"><span data-stu-id="f4b34-124">Download hello Chat Example</span></span>
<span data-ttu-id="f4b34-125">Для этого проекта, мы будем использовать пример hello разговора с hello [репозитории Socket.IO GitHub].</span><span class="sxs-lookup"><span data-stu-id="f4b34-125">For this project, we will use hello chat example from hello [Socket.IO GitHub repository].</span></span> <span data-ttu-id="f4b34-126">Выполните следующий пример hello toodownload действия hello и добавьте его toohello проекта, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="f4b34-126">Perform hello following steps toodownload hello example and add it toohello project you previously created.</span></span>

1. <span data-ttu-id="f4b34-127">Создать локальную копию репозитория hello с помощью hello **клон** кнопки.</span><span class="sxs-lookup"><span data-stu-id="f4b34-127">Create a local copy of hello repository by using hello **Clone** button.</span></span> <span data-ttu-id="f4b34-128">Можно также использовать hello **ZIP** кнопку toodownload hello проекта.</span><span class="sxs-lookup"><span data-stu-id="f4b34-128">You may also use hello **ZIP** button toodownload hello project.</span></span>
   
   ![Просмотр https://github.com/LearnBoost/socket.io/tree/master/examples/chat, значком загрузки ZIP "hello" выделяются окно браузера][chat-example-view]
2. <span data-ttu-id="f4b34-130">Перейдите структуры каталогов hello hello локальный репозиторий, пока не будет выполнен переход на hello **примеры\\чата** каталога.</span><span class="sxs-lookup"><span data-stu-id="f4b34-130">Navigate hello directory structure of hello local repository until you arrive at hello **examples\\chat** directory.</span></span> <span data-ttu-id="f4b34-131">Скопируйте содержимое hello этот каталог toothe **C:\\узел\\chatapp\\WorkerRole1** каталогом, созданным ранее.</span><span class="sxs-lookup"><span data-stu-id="f4b34-131">Copy hello contents of this directory toothe **C:\\node\\chatapp\\WorkerRole1** directory created earlier.</span></span>
   
   ![Обозреватель, отображающая содержимое hello hello примеры\\каталог чата, извлеченных из архива hello][chat-contents]
   
   <span data-ttu-id="f4b34-133">Hello выделенные элементы в снимке экрана приветствия выше, hello файлов, скопированных из hello **примеры\\чата** каталога</span><span class="sxs-lookup"><span data-stu-id="f4b34-133">hello highlighted items in hello screenshot above are hello files copied from hello **examples\\chat** directory</span></span>
3. <span data-ttu-id="f4b34-134">В hello **C:\\узел\\chatapp\\WorkerRole1** каталог, удаление hello **server.js** файла, а затем переименуйте hello **в файле app.js**файл слишком**server.js**.</span><span class="sxs-lookup"><span data-stu-id="f4b34-134">In hello **C:\\node\\chatapp\\WorkerRole1** directory, delete hello **server.js** file, and then rename hello **app.js** file too**server.js**.</span></span> <span data-ttu-id="f4b34-135">При этом удаляются по умолчанию hello **server.js** файл, созданный ранее hello **Add-AzureNodeWorkerRole** командлета и заменяет его с помощью приложения hello файл из hello пример разговора.</span><span class="sxs-lookup"><span data-stu-id="f4b34-135">This removes hello default **server.js** file created previously by hello **Add-AzureNodeWorkerRole** cmdlet and replaces it with hello application file from hello chat example.</span></span>

### <a name="modify-serverjs-and-install-modules"></a><span data-ttu-id="f4b34-136">Изменение Server.js и установка модулей</span><span class="sxs-lookup"><span data-stu-id="f4b34-136">Modify Server.js and Install Modules</span></span>
<span data-ttu-id="f4b34-137">Прежде чем приложение hello тестирования в hello эмулятор Azure необходимо некоторые незначительные изменения.</span><span class="sxs-lookup"><span data-stu-id="f4b34-137">Before testing hello application in hello Azure emulator, we must make some minor modifications.</span></span> <span data-ttu-id="f4b34-138">Выполните следующие шаги toothe server.js файл hello.</span><span class="sxs-lookup"><span data-stu-id="f4b34-138">Perform hello following steps toothe server.js file:</span></span>

1. <span data-ttu-id="f4b34-139">Откройте hello **server.js** файл в Visual Studio или в любом текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="f4b34-139">Open hello **server.js** file in Visual Studio or any text editor.</span></span>
2. <span data-ttu-id="f4b34-140">Найти hello **зависимости модулей** в начале hello server.js и измените hello строке, содержащей **sio = require('.. //.. LIB//Socket.IO ")** слишком**sio = require('socket.io')** как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="f4b34-140">Find hello **Module dependencies** section at hello beginning of server.js and change hello line containing **sio = require('..//..//lib//socket.io')** too**sio = require('socket.io')** as shown below:</span></span>
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. <span data-ttu-id="f4b34-141">приложение hello tooensure прослушивает hello правильный порт, откройте server.js в блокноте или любом редакторе и измените следующую строку, заменяя **3000** с **process.env.port** как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="f4b34-141">tooensure hello application listens on hello correct port, open server.js in Notepad or your favorite editor, and then change the following line by replacing **3000** with **process.env.port** as shown below:</span></span>
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

<span data-ttu-id="f4b34-142">После сохранения изменений hello слишком**server.js**, используйте hello следующие шаги для установки требуемых модулей и проверить приложение hello в эмуляторе Azure:</span><span class="sxs-lookup"><span data-stu-id="f4b34-142">After saving hello changes too**server.js**, use hello following steps to install required modules, and then test hello application in the Azure emulator:</span></span>

1. <span data-ttu-id="f4b34-143">С помощью **Azure PowerShell**, измените каталоги toohello **C:\\узел\\chatapp\\WorkerRole1** каталог и использовать hello, следующая команда tooinstall hello модули, необходимых для этого приложения:</span><span class="sxs-lookup"><span data-stu-id="f4b34-143">Using **Azure PowerShell**, change directories toohello **C:\\node\\chatapp\\WorkerRole1** directory and use hello following command tooinstall hello modules required by this application:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   <span data-ttu-id="f4b34-144">Будет выполнена установка hello модулей, перечисленных в файле package.json hello.</span><span class="sxs-lookup"><span data-stu-id="f4b34-144">This will install hello modules listed in hello package.json file.</span></span> <span data-ttu-id="f4b34-145">После завершения команды hello, вы увидите примерно toothe следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="f4b34-145">After hello command completes, you should see output similar toothe following:</span></span>
   
   ![Команда установки hello npm выходные данные Hello][The-output-of-the-npm-install-command]
2. <span data-ttu-id="f4b34-147">Поскольку в этом примере был изначально частью hello репозитории Socket.IO GitHub и прямая ссылка на библиотеку Socket.IO hello относительного пути, Socket.IO нет ссылок в файл package.json hello, поэтому его необходимо установить, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="f4b34-147">Since this example was originally a part of hello Socket.IO GitHub repository, and directly referenced hello Socket.IO library by relative path, Socket.IO was not referenced in hello package.json file, so we must install it by issuing hello following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a><span data-ttu-id="f4b34-148">Тестирование и развертывание</span><span class="sxs-lookup"><span data-stu-id="f4b34-148">Test and Deploy</span></span>
1. <span data-ttu-id="f4b34-149">Запустите эмулятор hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="f4b34-149">Launch hello emulator by issuing hello following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > <span data-ttu-id="f4b34-150">С запуском эмулятора может возникнуть проблема, например во время выполнения команды Start-AzureEmulator произошла непредвиденная ошибка.</span><span class="sxs-lookup"><span data-stu-id="f4b34-150">If you encounter issues with launching emulator, eg.: Start-AzureEmulator : An unexpected failure occurred.</span></span>  <span data-ttu-id="f4b34-151">Подробные сведения: Произошла непредвиденная ошибка hello объект связи System.ServiceModel.Channels.ServiceChannel, не может использоваться для связи, так как он находится в состоянии Faulted hello.</span><span class="sxs-lookup"><span data-stu-id="f4b34-151">Details: Encountered an unexpected error hello communication object,  System.ServiceModel.Channels.ServiceChannel, cannot be used for communication because it is in hello Faulted state.</span></span>
   
      <span data-ttu-id="f4b34-152">Переустановите AzureAuthoringTools версии 2.7.1 и AzureComputeEmulator версии 2.7 (убедитесь, что версии совпадают).</span><span class="sxs-lookup"><span data-stu-id="f4b34-152">reinstall AzureAuthoringTools v 2.7.1 and AzureComputeEmulator v 2.7 - make sure that version matches.</span></span>
   >
   >


2. <span data-ttu-id="f4b34-153">Откройте браузер и перейдите в слишком**http://127.0.0.1**.</span><span class="sxs-lookup"><span data-stu-id="f4b34-153">Open a browser and navigate too**http://127.0.0.1**.</span></span>
3. <span data-ttu-id="f4b34-154">В открывшемся окне браузера hello введите понятное имя и затем нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="f4b34-154">When hello browser window opens, enter a nickname and then hit enter.</span></span>
   <span data-ttu-id="f4b34-155">Это позволит вам toopost сообщений от определенного понятное имя.</span><span class="sxs-lookup"><span data-stu-id="f4b34-155">This will allow you toopost messages as a specific nickname.</span></span> <span data-ttu-id="f4b34-156">функциональные возможности tootest несколькими пользователями, открывать окна браузера, используя же URL-адрес и введите разные псевдонимы.</span><span class="sxs-lookup"><span data-stu-id="f4b34-156">tootest multi-user functionality, open additional browser windows using the same URL and enter different nicknames.</span></span>
   
   ![Два окна браузера с сообщениями разговора от пользователей User1 и User2](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. <span data-ttu-id="f4b34-158">После тестирования приложения hello остановите hello эмулятора, введя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f4b34-158">After testing hello application, stop hello emulator by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. <span data-ttu-id="f4b34-159">tooAzure приложения hello toodeploy, используйте **AzureServiceProject публикации** командлета.</span><span class="sxs-lookup"><span data-stu-id="f4b34-159">toodeploy hello application tooAzure, use the **Publish-AzureServiceProject** cmdlet.</span></span> <span data-ttu-id="f4b34-160">Например:</span><span class="sxs-lookup"><span data-stu-id="f4b34-160">For example:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > <span data-ttu-id="f4b34-161">Можно убедиться, что toouse уникальное имя, в противном случае hello публикации процесс завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="f4b34-161">Be sure toouse a unique name, otherwise hello publish process will fail.</span></span> <span data-ttu-id="f4b34-162">После завершения развертывания hello обозреватель hello и перехода toohello развертывания службы.</span><span class="sxs-lookup"><span data-stu-id="f4b34-162">After hello deployment has completed, hello browser will open and navigate toohello deployed service.</span></span>
   > 
   > <span data-ttu-id="f4b34-163">Если появляется следующее сообщение об ошибке, hello, если имя подписки не существует в hello импортировать профиль публикации, необходимо загрузить и импортировать профиль публикации hello для вашей подписки, перед развертыванием tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f4b34-163">If you receive an error stating that hello provided subscription name doesn't exist in hello imported publish profile, you must download and import hello publishing profile for your subscription before deploying tooAzure.</span></span> <span data-ttu-id="f4b34-164">. В разделе hello **развертывание tooAzure приложения hello** раздел [построения и развертывания tooan приложений Node.js облачной службы Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="f4b34-164">See hello **Deploying hello Application tooAzure** section of [Build and deploy a Node.js application tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 
   
   ![Окно браузера, отображение hello службе, размещенной в Azure][completed-app]
   
   > [!NOTE]
   > <span data-ttu-id="f4b34-166">Если появляется следующее сообщение об ошибке, hello, если имя подписки не существует в hello импортировать профиль публикации, необходимо загрузить и импортировать профиль публикации hello для вашей подписки, перед развертыванием tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f4b34-166">If you receive an error stating that hello provided subscription name doesn't exist in hello imported publish profile, you must download and import hello publishing profile for your subscription before deploying tooAzure.</span></span> <span data-ttu-id="f4b34-167">. В разделе hello **развертывание tooAzure приложения hello** раздел [построения и развертывания tooan приложений Node.js облачной службы Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="f4b34-167">See hello **Deploying hello Application tooAzure** section of [Build and deploy a Node.js application tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 

<span data-ttu-id="f4b34-168">Теперь ваше приложение выполняется на платформе Azure и может передавать сообщения чата между различными клиентами с использованием Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="f4b34-168">Your application is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

> [!NOTE]
> <span data-ttu-id="f4b34-169">Для простоты в этом примере используется ограниченный toochatting между toohello подключенных пользователей того же экземпляра.</span><span class="sxs-lookup"><span data-stu-id="f4b34-169">For simplicity, this sample is limited toochatting between users connected toohello same instance.</span></span> <span data-ttu-id="f4b34-170">Это означает, что если hello облачная служба создает двух экземпляров рабочей роли, пользователи только смогут toochat с другими разделами подключен toohello того же экземпляра роли рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="f4b34-170">This means that if hello cloud service creates two worker role instances, users will only be able toochat with others connected toohello same worker role instance.</span></span> <span data-ttu-id="f4b34-171">toowork приложения hello tooscale с несколькими экземплярами роли, можно использовать технологию как Service Bus tooshare hello Socket.IO сохранение состояния между экземплярами.</span><span class="sxs-lookup"><span data-stu-id="f4b34-171">tooscale hello application toowork with multiple role instances, you could use a technology like Service Bus tooshare hello Socket.IO store state across instances.</span></span> <span data-ttu-id="f4b34-172">Примеры см. в разделе hello очереди Service Bus и разделы примеры использования в hello [Azure SDK для репозитория Node.js GitHub](https://github.com/WindowsAzure/azure-sdk-for-node).</span><span class="sxs-lookup"><span data-stu-id="f4b34-172">For examples, see hello Service Bus Queues and Topics usage samples in hello [Azure SDK for Node.js GitHub repository](https://github.com/WindowsAzure/azure-sdk-for-node).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f4b34-173">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f4b34-173">Next steps</span></span>
<span data-ttu-id="f4b34-174">В этом учебнике вы узнали, как toocreate это основные чата приложение, размещенное в облачной службе Azure.</span><span class="sxs-lookup"><span data-stu-id="f4b34-174">In this tutorial you learned how toocreate a basic chat application hosted in an Azure Cloud Service.</span></span> <span data-ttu-id="f4b34-175">toolearn toohost этого приложения в веб-сайта Azure. в статье [построения приложения чат Node.js с Socket.IO на веб-сайте Azure][chatwebsite].</span><span class="sxs-lookup"><span data-stu-id="f4b34-175">toolearn how toohost this application in an Azure Website, see [Build a Node.js Chat Application with Socket.IO on an Azure Web Site][chatwebsite].</span></span>

<span data-ttu-id="f4b34-176">Дополнительные сведения см. также: hello [Центр разработчика Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="f4b34-176">For more information, see also hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[репозитории Socket.IO GitHub]: https://github.com/LearnBoost/socket.io/tree/0.9.14
[Azure Considerations]: #windowsazureconsiderations
[Hosting hello Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: ./media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png


