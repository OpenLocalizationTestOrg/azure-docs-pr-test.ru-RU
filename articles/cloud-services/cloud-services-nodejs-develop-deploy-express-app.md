---
title: "aaaWeb приложение с экспресс-выпуск (Node.js) | Документы Microsoft"
description: "Учебник, в котором основана на hello облачной службы учебника и показано, как toouse hello модуль экспресс-выпуск."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 24f8e7ef-e90d-4554-9b1e-a9b31d5824e5
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 91921bfbe137eeca9a110d4cb18eb57b46b0060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a><span data-ttu-id="57c8e-103">Создание веб-приложения Node.js с использованием модуля Express в облачной службе Azure</span><span class="sxs-lookup"><span data-stu-id="57c8e-103">Build a Node.js web application using Express on an Azure Cloud Service</span></span>
<span data-ttu-id="57c8e-104">Node.js включает минимальный набор функциональных возможностей в среде выполнения ядра hello.</span><span class="sxs-lookup"><span data-stu-id="57c8e-104">Node.js includes a minimal set of functionality in hello core runtime.</span></span>
<span data-ttu-id="57c8e-105">Разработчики часто используют сторонних производителей модулей tooprovide дополнительные функциональные возможности при разработке приложений Node.js.</span><span class="sxs-lookup"><span data-stu-id="57c8e-105">Developers often use 3rd party modules tooprovide additional functionality when developing a Node.js application.</span></span> <span data-ttu-id="57c8e-106">В этом учебнике создается новое приложение с помощью hello [Express] [ Express] модуль, который предоставляет платформу MVC для создания веб-приложений Node.js.</span><span class="sxs-lookup"><span data-stu-id="57c8e-106">In this tutorial you will create a new application using hello [Express][Express] module, which provides an MVC framework for creating Node.js web applications.</span></span>

<span data-ttu-id="57c8e-107">Снимок экрана приложения hello завершения используется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="57c8e-107">A screenshot of hello completed application is below:</span></span>

![Веб-браузер, отображение tooExpress Добро пожаловать в Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="57c8e-109">Создание проекта облачной службы</span><span class="sxs-lookup"><span data-stu-id="57c8e-109">Create a Cloud Service Project</span></span>
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

<span data-ttu-id="57c8e-110">Hello следующих шагов toocreate Создание проекта облачной службы с именем «expressapp»:</span><span class="sxs-lookup"><span data-stu-id="57c8e-110">Perform hello following steps toocreate a new cloud service project named 'expressapp':</span></span>

1. <span data-ttu-id="57c8e-111">Из hello **меню "Пуск"** или **рабочий стол**, поиск **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="57c8e-111">From hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="57c8e-112">Щелкните правой кнопкой мыши **Windows PowerShell** и выберите **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="57c8e-112">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Значок Azure PowerShell](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. <span data-ttu-id="57c8e-114">Измените каталоги toohello **c:\\узел** каталога, а затем введите следующие команды toocreate новое решение с именем hello **expressapp** и веб-роль с именем **WebRole1** :</span><span class="sxs-lookup"><span data-stu-id="57c8e-114">Change directories toohello **c:\\node** directory and then enter hello following commands toocreate a new solution named **expressapp** and a web role named **WebRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > <span data-ttu-id="57c8e-115">По умолчанию **Add-AzureNodeWebRole** использует предыдущую версию Node.js.</span><span class="sxs-lookup"><span data-stu-id="57c8e-115">By default, **Add-AzureNodeWebRole** uses an older version of Node.js.</span></span> <span data-ttu-id="57c8e-116">Hello **AzureServiceProjectRole набор** выше инструкция предписывает v0.10.21 Azure toouse узла.</span><span class="sxs-lookup"><span data-stu-id="57c8e-116">hello **Set-AzureServiceProjectRole** statement above instructs Azure toouse v0.10.21 of Node.</span></span>  <span data-ttu-id="57c8e-117">Обратите внимание, что параметры hello зависят от регистра.</span><span class="sxs-lookup"><span data-stu-id="57c8e-117">Note hello parameters are case-sensitive.</span></span>  <span data-ttu-id="57c8e-118">Можно проверить, проверив hello был выбран hello правильную версию Node.js **ядер** свойство в **WebRole1\package.json**.</span><span class="sxs-lookup"><span data-stu-id="57c8e-118">You can verify hello correct version of Node.js has been selected by checking hello **engines** property in **WebRole1\package.json**.</span></span>
    > 
    > 

## <a name="install-express"></a><span data-ttu-id="57c8e-119">Установка модуля Express</span><span class="sxs-lookup"><span data-stu-id="57c8e-119">Install Express</span></span>
1. <span data-ttu-id="57c8e-120">Установите генератор Express hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="57c8e-120">Install hello Express generator by issuing hello following command:</span></span>
   
        PS C:\node\expressapp> npm install express-generator -g
   
    <span data-ttu-id="57c8e-121">Hello выходные данные команды npm hello должен выглядеть примерно ниже toohello результата.</span><span class="sxs-lookup"><span data-stu-id="57c8e-121">hello output of hello npm command should look similar toohello result below.</span></span> 
   
    ![Express команда установки Windows PowerShell отображение hello выходные данные hello npm.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. <span data-ttu-id="57c8e-123">Измените каталоги toohello **WebRole1** каталог и использовать hello toogenerate express команда нового приложения:</span><span class="sxs-lookup"><span data-stu-id="57c8e-123">Change directories toohello **WebRole1** directory and use hello express command toogenerate a new application:</span></span>
   
        PS C:\node\expressapp\WebRole1> express
   
    <span data-ttu-id="57c8e-124">Вам будет запрашиваемые toooverwrite предыдущих приложения.</span><span class="sxs-lookup"><span data-stu-id="57c8e-124">You will be prompted toooverwrite your earlier application.</span></span> <span data-ttu-id="57c8e-125">Введите **y** или **Да** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="57c8e-125">Enter **y** or **yes** toocontinue.</span></span> <span data-ttu-id="57c8e-126">Express приведет к созданию файла в файле app.js hello и структуру папок для построения приложения.</span><span class="sxs-lookup"><span data-stu-id="57c8e-126">Express will generate hello app.js file and a folder structure for building your application.</span></span>
   
    ![Hello выходные данные команды express hello](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. <span data-ttu-id="57c8e-128">tooinstall Дополнительные зависимости, определенные в файле package.json hello, введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="57c8e-128">tooinstall additional dependencies defined in hello package.json file, enter hello following command:</span></span>
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![Команда установки hello npm выходные данные Hello](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. <span data-ttu-id="57c8e-130">Используйте hello следующая команда toocopy hello **bin/www** файла слишком**server.js**.</span><span class="sxs-lookup"><span data-stu-id="57c8e-130">Use hello following command toocopy hello **bin/www** file too**server.js**.</span></span> <span data-ttu-id="57c8e-131">Это так, чтобы hello облачной службы можно найти hello точку входа для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="57c8e-131">This is so hello cloud service can find hello entry point for this application.</span></span>
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   <span data-ttu-id="57c8e-132">После выполнения этой команды должно быть **server.js** файл в каталоге hello WebRole1.</span><span class="sxs-lookup"><span data-stu-id="57c8e-132">After this command completes, you should have a **server.js** file in hello WebRole1 directory.</span></span>
5. <span data-ttu-id="57c8e-133">Изменение hello **server.js** tooremove один hello "." символов из следующей строкой hello.</span><span class="sxs-lookup"><span data-stu-id="57c8e-133">Modify hello **server.js** tooremove one of hello '.' characters from hello following line.</span></span>
   
       var app = require('../app');
   
   <span data-ttu-id="57c8e-134">После внесения этого изменения, строка hello должен выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="57c8e-134">After making this modification, hello line should appear as follows.</span></span>
   
       var app = require('./app');
   
   <span data-ttu-id="57c8e-135">Это изменение не требуется, так как мы перешли файл hello (прежнее название — **bin/www**,) toohello же каталоге, что файл приложения hello является обязательным.</span><span class="sxs-lookup"><span data-stu-id="57c8e-135">This change is required since we moved hello file (formerly **bin/www**,) toohello same directory as hello app file being required.</span></span> <span data-ttu-id="57c8e-136">После этого изменения сохранить hello **server.js** файла.</span><span class="sxs-lookup"><span data-stu-id="57c8e-136">After making this change, save hello **server.js** file.</span></span>
6. <span data-ttu-id="57c8e-137">Используйте hello следующая команда toorun приложения hello в hello эмулятор Azure:</span><span class="sxs-lookup"><span data-stu-id="57c8e-137">Use hello following command toorun hello application in hello Azure emulator:</span></span>
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Веб-страница, содержащая tooexpress приветствия.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-hello-view"></a><span data-ttu-id="57c8e-139">Изменение представления hello</span><span class="sxs-lookup"><span data-stu-id="57c8e-139">Modifying hello View</span></span>
<span data-ttu-id="57c8e-140">Теперь измените hello представление toodisplay приветственное сообщение «Вас приветствует tooExpress в Azure».</span><span class="sxs-lookup"><span data-stu-id="57c8e-140">Now modify hello view toodisplay hello message "Welcome tooExpress in Azure".</span></span>

1. <span data-ttu-id="57c8e-141">Введите следующие команды tooopen hello index.jade файл hello:</span><span class="sxs-lookup"><span data-stu-id="57c8e-141">Enter hello following command tooopen hello index.jade file:</span></span>
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![Hello содержимое файла index.jade hello.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   <span data-ttu-id="57c8e-143">Jade — обработчик представлений по умолчанию hello, используемых приложениями, экспресс-выпуск.</span><span class="sxs-lookup"><span data-stu-id="57c8e-143">Jade is hello default view engine used by Express applications.</span></span> <span data-ttu-id="57c8e-144">Дополнительные сведения о обработчик Jade представлений hello. в разделе [http://jade-lang.com][http://jade-lang.com].</span><span class="sxs-lookup"><span data-stu-id="57c8e-144">For more information on hello Jade view engine, see [http://jade-lang.com][http://jade-lang.com].</span></span>
2. <span data-ttu-id="57c8e-145">Измените hello последней строки текста, добавив **в Azure**.</span><span class="sxs-lookup"><span data-stu-id="57c8e-145">Modify hello last line of text by appending **in Azure**.</span></span>
   
   ![считывает файл index.jade Hello, последняя строка hello: p Добро пожаловать слишком\#{title} в Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. <span data-ttu-id="57c8e-147">Сохраните файл hello и закройте Блокнот.</span><span class="sxs-lookup"><span data-stu-id="57c8e-147">Save hello file and exit Notepad.</span></span>
4. <span data-ttu-id="57c8e-148">Обновите браузер и увидите изменения.</span><span class="sxs-lookup"><span data-stu-id="57c8e-148">Refresh your browser and you will see your changes.</span></span>
   
   ![Окно браузера, страница приветствия содержит tooExpress Добро пожаловать в Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

<span data-ttu-id="57c8e-150">После тестирования приложения hello, используйте hello **Stop AzureEmulator** командлет toostop hello эмулятора.</span><span class="sxs-lookup"><span data-stu-id="57c8e-150">After testing hello application, use hello **Stop-AzureEmulator** cmdlet toostop hello emulator.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="57c8e-151">Публикация tooAzure приложения hello</span><span class="sxs-lookup"><span data-stu-id="57c8e-151">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="57c8e-152">В окне Azure PowerShell hello использовать hello **AzureServiceProject публикации** командлет toodeploy приложения hello tooa облачной службы</span><span class="sxs-lookup"><span data-stu-id="57c8e-152">In hello Azure PowerShell window, use hello **Publish-AzureServiceProject** cmdlet toodeploy hello application tooa cloud service</span></span>

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

<span data-ttu-id="57c8e-153">После завершения операции развертывания hello браузера открыть и отобразить веб-страницу приветствия.</span><span class="sxs-lookup"><span data-stu-id="57c8e-153">Once hello deployment operation completes, your browser will open and display hello web page.</span></span>

![Веб-браузер, отображения страницы приветствия, экспресс-выпуск.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a><span data-ttu-id="57c8e-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="57c8e-156">Next steps</span></span>
<span data-ttu-id="57c8e-157">Дополнительные сведения см. в разделе hello [Центр разработчика Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="57c8e-157">For more information, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


