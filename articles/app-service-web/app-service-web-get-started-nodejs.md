---
title: "Создание веб-приложений Node.js в Azure | Документация Майкрософт"
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
ms.openlocfilehash: ce845da09a7c088b8a2ba29b818a46a3b41aa4e7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-nodejs-web-app-in-azure"></a><span data-ttu-id="48691-103">Создание веб-приложений Node.js в Azure</span><span class="sxs-lookup"><span data-stu-id="48691-103">Create a Node.js web app in Azure</span></span>

<span data-ttu-id="48691-104">[Веб-приложения Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="48691-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="48691-105">В этом кратком руководстве объясняется, как развертывать приложения Node.js в веб-приложениях Azure.</span><span class="sxs-lookup"><span data-stu-id="48691-105">This quickstart shows how to deploy a Node.js app to Azure Web Apps.</span></span> <span data-ttu-id="48691-106">С помощью [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) вы можете создавать веб-приложения, в которых можно развертывать примеры кода Node.js с использованием Git.</span><span class="sxs-lookup"><span data-stu-id="48691-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy sample Node.js code to the web app.</span></span>

![Пример приложения, выполняющегося в Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="48691-108">Выполните действия, приведенные ниже, с помощью компьютера Mac, Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="48691-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="48691-109">После установки необходимых компонентов для выполнения этих шагов потребуется около пяти минут.</span><span class="sxs-lookup"><span data-stu-id="48691-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a><span data-ttu-id="48691-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="48691-110">Prerequisites</span></span>

<span data-ttu-id="48691-111">Для работы с этим кратким руководством сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="48691-111">To complete this quickstart:</span></span>

* <span data-ttu-id="48691-112">[установите Git](https://git-scm.com/);</span><span class="sxs-lookup"><span data-stu-id="48691-112">[Install Git](https://git-scm.com/)</span></span>
* <span data-ttu-id="48691-113">[установите Node.j и NPM](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="48691-113">[Install Node.js and NPM](https://nodejs.org/)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="48691-114">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="48691-114">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="48691-115">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="48691-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="48691-116">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="48691-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-the-sample"></a><span data-ttu-id="48691-117">Скачивание примера приложения</span><span class="sxs-lookup"><span data-stu-id="48691-117">Download the sample</span></span>

<span data-ttu-id="48691-118">В окне терминала выполните следующую команду, чтобы клонировать репозиторий с примером приложения на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="48691-118">In a terminal window, run the following command to clone the sample app repository to your local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

<span data-ttu-id="48691-119">Используйте это окно терминала для выполнения всех команд в рамках этого руководства.</span><span class="sxs-lookup"><span data-stu-id="48691-119">You use this terminal window to run all the commands in this quickstart.</span></span>

<span data-ttu-id="48691-120">Перейдите в каталог, в котором содержится образец кода.</span><span class="sxs-lookup"><span data-stu-id="48691-120">Change to the directory that contains the sample code.</span></span>

```bash
cd nodejs-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="48691-121">Локальный запуск приложения</span><span class="sxs-lookup"><span data-stu-id="48691-121">Run the app locally</span></span>

<span data-ttu-id="48691-122">Запустите приложение в локальной среде, открыв окно терминала и выполнив скрипт `npm start`, чтобы запустить встроенный HTTP-сервер Node.js.</span><span class="sxs-lookup"><span data-stu-id="48691-122">Run the application locally by opening a terminal window and using the `npm start` script to launch the built in Node.js HTTP server.</span></span>

```bash
npm start
```

<span data-ttu-id="48691-123">Откройте браузер и перейдите к примеру приложения по адресу http://localhost:1337.</span><span class="sxs-lookup"><span data-stu-id="48691-123">Open a web browser, and navigate to the sample app at http://localhost:1337.</span></span>

<span data-ttu-id="48691-124">На странице отобразится сообщение **Hello World** из примера приложения.</span><span class="sxs-lookup"><span data-stu-id="48691-124">You see the **Hello World** message from the sample app displayed in the page.</span></span>

![Пример приложения, выполняющегося локально](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

<span data-ttu-id="48691-126">В окне терминала нажмите клавиши **CTRL+C**, чтобы выйти из веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="48691-126">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

[!INCLUDE [Log in to Azure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Пустая страница веб-приложения](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="48691-128">Вы создали пустое веб-приложение в Azure.</span><span class="sxs-lookup"><span data-stu-id="48691-128">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 23, done.
Delta compression using up to 4 threads.
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
remote: Node.js versions available on the platform are: 4.4.7, 4.5.0, 6.2.2, 6.6.0, 6.9.1.
remote: Selected node.js version 6.9.1. Use package.json file to choose a different version.
remote: Selected npm version 3.10.8
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net:443/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-to-the-app"></a><span data-ttu-id="48691-129">Переход в приложение</span><span class="sxs-lookup"><span data-stu-id="48691-129">Browse to the app</span></span>

<span data-ttu-id="48691-130">Перейдите в развертываемое приложение с помощью веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="48691-130">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="48691-131">Пример кода Node.js выполняется в веб-приложении службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="48691-131">The Node.js sample code is running in an Azure App Service web app.</span></span>

![Пример приложения, выполняющегося в Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="48691-133">**Поздравляем!**</span><span class="sxs-lookup"><span data-stu-id="48691-133">**Congratulations!**</span></span> <span data-ttu-id="48691-134">Вы развернули свое первое приложение Node.js в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="48691-134">You've deployed your first Node.js app to App Service.</span></span>

## <a name="update-and-redeploy-the-code"></a><span data-ttu-id="48691-135">Обновление и повторное развертывание кода</span><span class="sxs-lookup"><span data-stu-id="48691-135">Update and redeploy the code</span></span>

<span data-ttu-id="48691-136">В текстовом редакторе в приложении Node.js откройте файл `index.js` и измените текст в вызове `response.end`:</span><span class="sxs-lookup"><span data-stu-id="48691-136">Using a text editor, open the `index.js` file in the Node.js app, and make a small change to the text in the call to `response.end`:</span></span>

```nodejs
response.end("Hello Azure!");
```

<span data-ttu-id="48691-137">Зафиксируйте изменения в Git, а затем отправьте изменения кода в Azure.</span><span class="sxs-lookup"><span data-stu-id="48691-137">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="48691-138">После завершения развертывания переключитесь в окно браузера, открытое на этапе **перехода в приложение**, и щелкните "Обновить".</span><span class="sxs-lookup"><span data-stu-id="48691-138">Once deployment has completed, switch back to the browser window that opened in the **Browse to the app** step, and hit refresh.</span></span>

![Обновленный пример приложения, выполняющегося в Azure](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="48691-140">Управление новым веб-приложением Azure</span><span class="sxs-lookup"><span data-stu-id="48691-140">Manage your new Azure web app</span></span>

<span data-ttu-id="48691-141">Перейдите на <a href="https://portal.azure.com" target="_blank">портал Azure</a> для управления созданным веб-приложением.</span><span class="sxs-lookup"><span data-stu-id="48691-141">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="48691-142">В меню слева выберите **Службы приложений**, а затем щелкните имя своего веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="48691-142">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Переход к веб-приложению Azure на портале](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="48691-144">Отобразится страница обзора вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="48691-144">You see your web app's Overview page.</span></span> <span data-ttu-id="48691-145">Вы можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление.</span><span class="sxs-lookup"><span data-stu-id="48691-145">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Колонка службы приложений на портале Azure](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="48691-147">В меню слева доступно несколько страниц для настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="48691-147">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="48691-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="48691-148">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="48691-149">Node.js с MongoDB</span><span class="sxs-lookup"><span data-stu-id="48691-149">Node.js with MongoDB</span></span>](app-service-web-tutorial-nodejs-mongodb-app.md)
