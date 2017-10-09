---
title: "aaaCreate Node.js веб-приложения в Azure | Документы Microsoft"
description: "Быстрое развертывание первого приложения Hello World на Node.js в веб-приложении службы приложений Azure."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 582bb3c2-164b-42f5-b081-95bfcb7a502a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/05/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 163edf83b2353755fc9fa2d75aed489038cf7c81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-web-app-in-azure"></a><span data-ttu-id="431d5-103">Создание веб-приложений Node.js в Azure</span><span class="sxs-lookup"><span data-stu-id="431d5-103">Create a Node.js web app in Azure</span></span>

<span data-ttu-id="431d5-104">[Веб-приложения Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="431d5-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="431d5-105">Краткого руководства показано, как toodeploy tooAzure приложение Node.js веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="431d5-105">This quickstart shows how toodeploy a Node.js app tooAzure Web Apps.</span></span> <span data-ttu-id="431d5-106">Создание веб-приложения hello, с помощью hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), и использовать Git toodeploy образец кода toohello веб-приложение Node.js.</span><span class="sxs-lookup"><span data-stu-id="431d5-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample Node.js code toohello web app.</span></span>

![Пример приложения, выполняющегося в Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="431d5-108">Выполните действия hello ниже, с помощью компьютером Mac, Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="431d5-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="431d5-109">После установки необходимых компонентов hello, требует toocomplete около пяти минут hello действия.</span><span class="sxs-lookup"><span data-stu-id="431d5-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a><span data-ttu-id="431d5-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="431d5-110">Prerequisites</span></span>

<span data-ttu-id="431d5-111">toocomplete краткого руководства:</span><span class="sxs-lookup"><span data-stu-id="431d5-111">toocomplete this quickstart:</span></span>

* <span data-ttu-id="431d5-112">[установите Git](https://git-scm.com/);</span><span class="sxs-lookup"><span data-stu-id="431d5-112">[Install Git](https://git-scm.com/)</span></span>
* <span data-ttu-id="431d5-113">[установите Node.j и NPM](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="431d5-113">[Install Node.js and NPM](https://nodejs.org/)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="431d5-114">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="431d5-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="431d5-115">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="431d5-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="431d5-116">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="431d5-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="431d5-117">Загрузить образец hello</span><span class="sxs-lookup"><span data-stu-id="431d5-117">Download hello sample</span></span>

<span data-ttu-id="431d5-118">В окне терминала запустите hello, следующая команда tooclone hello образец приложения репозитория tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="431d5-118">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

<span data-ttu-id="431d5-119">В этом кратком руководстве все команды hello использовать этот toorun окно терминала.</span><span class="sxs-lookup"><span data-stu-id="431d5-119">You use this terminal window toorun all hello commands in this quickstart.</span></span>

<span data-ttu-id="431d5-120">Изменить toohello каталог, содержащий образец кода hello.</span><span class="sxs-lookup"><span data-stu-id="431d5-120">Change toohello directory that contains hello sample code.</span></span>

```bash
cd nodejs-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="431d5-121">Выполните приложение hello локально</span><span class="sxs-lookup"><span data-stu-id="431d5-121">Run hello app locally</span></span>

<span data-ttu-id="431d5-122">Запустите приложение hello локально, откройте окно терминала и с помощью hello `npm start` hello toolaunch сценария, встроенных в сервер Node.js HTTP.</span><span class="sxs-lookup"><span data-stu-id="431d5-122">Run hello application locally by opening a terminal window and using hello `npm start` script toolaunch hello built in Node.js HTTP server.</span></span>

```bash
npm start
```

<span data-ttu-id="431d5-123">Откройте веб-браузер и перейдите toohello пример приложения на http://localhost:1337.</span><span class="sxs-lookup"><span data-stu-id="431d5-123">Open a web browser, and navigate toohello sample app at http://localhost:1337.</span></span>

<span data-ttu-id="431d5-124">Вы видите hello **Hello World** сообщения из примера приложения hello, отображаемое на странице приветствия.</span><span class="sxs-lookup"><span data-stu-id="431d5-124">You see hello **Hello World** message from hello sample app displayed in hello page.</span></span>

![Пример приложения, выполняющегося локально](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

<span data-ttu-id="431d5-126">В окне терминала, нажмите клавишу **Ctrl + C** tooexit hello веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="431d5-126">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Пустая страница веб-приложения](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="431d5-128">Вы создали пустое веб-приложение в Azure.</span><span class="sxs-lookup"><span data-stu-id="431d5-128">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 23, done.
Delta compression using up too4 threads.
Compressing objects: 100% (21/21), done.
Writing objects: 100% (23/23), 3.71 KiB | 0 bytes/s, done.
Total 23 (delta 8), reused 7 (delta 1)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'bf114df591'.
remote: Generating deployment script.
remote: Generating deployment script for node.js Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling node.js deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.js'
remote: Copying file: 'package.json'
remote: Copying file: 'process.json'
remote: Deleting file: 'hostingstart.html'
remote: Ignoring: .git
remote: Using start-up script index.js from package.json.
remote: Node.js versions available on hello platform are: 4.4.7, 4.5.0, 6.2.2, 6.6.0, 6.9.1.
remote: Selected node.js version 6.9.1. Use package.json file toochoose a different version.
remote: Selected npm version 3.10.8
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net:443/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="431d5-129">Обзор toohello приложения</span><span class="sxs-lookup"><span data-stu-id="431d5-129">Browse toohello app</span></span>

<span data-ttu-id="431d5-130">Обзор toohello развернуть приложение с помощью веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="431d5-130">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="431d5-131">Hello Node.js образце кода выполняется в веб-приложение службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="431d5-131">hello Node.js sample code is running in an Azure App Service web app.</span></span>

![Пример приложения, выполняющегося в Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="431d5-133">**Поздравляем!**</span><span class="sxs-lookup"><span data-stu-id="431d5-133">**Congratulations!**</span></span> <span data-ttu-id="431d5-134">Ваш первый tooApp приложение Node.js службы после развертывания.</span><span class="sxs-lookup"><span data-stu-id="431d5-134">You've deployed your first Node.js app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-code"></a><span data-ttu-id="431d5-135">Обновление и повторное развертывание кода hello</span><span class="sxs-lookup"><span data-stu-id="431d5-135">Update and redeploy hello code</span></span>

<span data-ttu-id="431d5-136">В текстовом редакторе, откройте hello `index.js` в Node.js приложение hello и создайте текстовый toohello небольшое изменение в вызове hello слишком`response.end`:</span><span class="sxs-lookup"><span data-stu-id="431d5-136">Using a text editor, open hello `index.js` file in hello Node.js app, and make a small change toohello text in hello call too`response.end`:</span></span>

```nodejs
response.end("Hello Azure!");
```

<span data-ttu-id="431d5-137">Фиксация изменений в Git и затем отправьте tooAzure изменения кода hello.</span><span class="sxs-lookup"><span data-stu-id="431d5-137">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="431d5-138">После завершения развертывания переключитесь задней toohello окно браузера, который открыт в hello **toohello приложения обзора** шаг и нажмите кнопку обновления.</span><span class="sxs-lookup"><span data-stu-id="431d5-138">Once deployment has completed, switch back toohello browser window that opened in hello **Browse toohello app** step, and hit refresh.</span></span>

![Обновленный пример приложения, выполняющегося в Azure](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="431d5-140">Управление новым веб-приложением Azure</span><span class="sxs-lookup"><span data-stu-id="431d5-140">Manage your new Azure web app</span></span>

<span data-ttu-id="431d5-141">Go toohello <a href="https://portal.azure.com" target="_blank">портал Azure</a> toomanage hello веб-приложения был создан.</span><span class="sxs-lookup"><span data-stu-id="431d5-141">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="431d5-142">Hello в левом меню, щелкните **службы приложений**, а затем щелкните имя hello Azure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="431d5-142">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Веб-приложения портала навигации tooAzure](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="431d5-144">Отобразится страница обзора вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="431d5-144">You see your web app's Overview page.</span></span> <span data-ttu-id="431d5-145">Вы можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление.</span><span class="sxs-lookup"><span data-stu-id="431d5-145">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Колонка службы приложений на портале Azure](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="431d5-147">меню слева Hello предоставляет различные страницы для настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="431d5-147">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="431d5-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="431d5-148">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="431d5-149">Node.js с MongoDB</span><span class="sxs-lookup"><span data-stu-id="431d5-149">Node.js with MongoDB</span></span>](app-service-web-tutorial-nodejs-mongodb-app.md)
