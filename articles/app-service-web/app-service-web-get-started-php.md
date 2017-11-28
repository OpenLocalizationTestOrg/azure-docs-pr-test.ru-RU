---
title: "aaaCreate PHP, веб-приложения в Azure | Документы Microsoft"
description: "Разверните свое первое приложение Hello World на языке PHP в веб-приложении службы приложений Azure за считаные минуты."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 07/21/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 8e1022889ca162f8f15ce7435cc9393cc6efef06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-web-app-in-azure"></a><span data-ttu-id="b8f6c-103">Создание веб-приложения PHP в Azure</span><span class="sxs-lookup"><span data-stu-id="b8f6c-103">Create a PHP web app in Azure</span></span>

<span data-ttu-id="b8f6c-104">[Веб-приложения Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="b8f6c-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="b8f6c-105">Этот учебник показывает, как toodeploy tooAzure приложения PHP веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="b8f6c-105">This quickstart tutorial shows how toodeploy a PHP app tooAzure Web Apps.</span></span> <span data-ttu-id="b8f6c-106">Создание веб-приложения hello, с помощью hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) оболочки в облаке и вам использовать Git toodeploy PHP образец кода toohello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="b8f6c-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) in Cloud Shell, and you use Git toodeploy sample PHP code toohello web app.</span></span>

<span data-ttu-id="b8f6c-107">![Пример приложения, выполняющегося в Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span><span class="sxs-lookup"><span data-stu-id="b8f6c-107">![Sample app running in Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span></span>

<span data-ttu-id="b8f6c-108">Выполните действия hello ниже, с помощью компьютером Mac, Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="b8f6c-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="b8f6c-109">После установки необходимых компонентов hello, требует toocomplete около пяти минут hello действия.</span><span class="sxs-lookup"><span data-stu-id="b8f6c-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8f6c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b8f6c-110">Prerequisites</span></span>

<span data-ttu-id="b8f6c-111">toocomplete краткого руководства:</span><span class="sxs-lookup"><span data-stu-id="b8f6c-111">toocomplete this quickstart:</span></span>

* <span data-ttu-id="b8f6c-112">[установите Git](https://git-scm.com/);</span><span class="sxs-lookup"><span data-stu-id="b8f6c-112">[Install Git](https://git-scm.com/)</span></span>
* <span data-ttu-id="b8f6c-113">[установите PHP](https://php.net).</span><span class="sxs-lookup"><span data-stu-id="b8f6c-113">[Install PHP](https://php.net)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample-locally"></a><span data-ttu-id="b8f6c-114">Загрузить образец hello локально</span><span class="sxs-lookup"><span data-stu-id="b8f6c-114">Download hello sample locally</span></span>

<span data-ttu-id="b8f6c-115">В окне терминала выполните следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="b8f6c-115">In a terminal window, run hello following commands.</span></span> <span data-ttu-id="b8f6c-116">Будут клонировать hello образец приложения tooyour локального компьютера, после чего перейдите toohello каталога содержащий hello образец кода.</span><span class="sxs-lookup"><span data-stu-id="b8f6c-116">This will clone hello sample application tooyour local machine, and navigate toohello directory containing hello sample code.</span></span>

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="b8f6c-117">Выполните приложение hello локально</span><span class="sxs-lookup"><span data-stu-id="b8f6c-117">Run hello app locally</span></span>

<span data-ttu-id="b8f6c-118">Запустите приложение hello локально, откройте окно терминала и с помощью hello `php` команда toolaunch hello встроенного PHP веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="b8f6c-118">Run hello application locally by opening a terminal window and using hello `php` command toolaunch hello built-in PHP web server.</span></span>

```bash
php -S localhost:8080
```

<span data-ttu-id="b8f6c-119">Откройте веб-браузер и перейдите toohello пример приложения на http://localhost: 8080.</span><span class="sxs-lookup"><span data-stu-id="b8f6c-119">Open a web browser, and navigate toohello sample app at http://localhost:8080.</span></span>

<span data-ttu-id="b8f6c-120">Вы видите hello **Здравствуй, мир!**</span><span class="sxs-lookup"><span data-stu-id="b8f6c-120">You see hello **Hello World!**</span></span> <span data-ttu-id="b8f6c-121">сообщение из примера приложения hello, отображаемое на странице приветствия.</span><span class="sxs-lookup"><span data-stu-id="b8f6c-121">message from hello sample app displayed in hello page.</span></span>

![Пример приложения, выполняющегося локально](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

<span data-ttu-id="b8f6c-123">В окне терминала, нажмите клавишу **Ctrl + C** tooexit hello веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="b8f6c-123">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![Пустая страница веб-приложения](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="b8f6c-125">Вы создали пустое веб-приложение в Azure.</span><span class="sxs-lookup"><span data-stu-id="b8f6c-125">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 2, done.
Delta compression using up too4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 352 bytes | 0 bytes/s, done.
Total 2 (delta 1), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '25f18051e9'.
remote: Generating deployment script.
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.php'
remote: Ignoring: .git
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
   cc39b1e..25f1805  master -> master
```

## <a name="browse-toohello-app-locally"></a><span data-ttu-id="b8f6c-126">Обзор toohello приложения локально</span><span class="sxs-lookup"><span data-stu-id="b8f6c-126">Browse toohello app locally</span></span>

<span data-ttu-id="b8f6c-127">Обзор toohello развернуть приложение с помощью веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="b8f6c-127">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="b8f6c-128">Hello PHP образце кода выполняется в веб-приложение службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="b8f6c-128">hello PHP sample code is running in an Azure App Service web app.</span></span>

![Пример приложения, выполняющегося в Azure](media/app-service-web-get-started-php/hello-world-in-browser.png)

<span data-ttu-id="b8f6c-130">**Поздравляем!**</span><span class="sxs-lookup"><span data-stu-id="b8f6c-130">**Congratulations!**</span></span> <span data-ttu-id="b8f6c-131">Ваш первый tooApp приложения PHP службы после развертывания.</span><span class="sxs-lookup"><span data-stu-id="b8f6c-131">You've deployed your first PHP app tooApp Service.</span></span>

## <a name="update-locally-and-redeploy-hello-code"></a><span data-ttu-id="b8f6c-132">Обновлять локально и заново кода hello</span><span class="sxs-lookup"><span data-stu-id="b8f6c-132">Update locally and redeploy hello code</span></span>

<span data-ttu-id="b8f6c-133">С помощью локального текстовом редакторе откройте hello `index.php` файл включен в приложение PHP hello и сделать текст toohello небольшое изменение в строку hello рядом слишком`echo`:</span><span class="sxs-lookup"><span data-stu-id="b8f6c-133">Using a local text editor, open hello `index.php` file within hello PHP app, and make a small change toohello text within hello string next too`echo`:</span></span>

```php
echo "Hello Azure!";
```

<span data-ttu-id="b8f6c-134">Фиксация изменений в Git и затем отправьте tooAzure изменения кода hello.</span><span class="sxs-lookup"><span data-stu-id="b8f6c-134">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="b8f6c-135">После завершения развертывания переключитесь задней toohello окно браузера, который открыт в hello **toohello приложения обзора** шаг и обновите страницу приветствия.</span><span class="sxs-lookup"><span data-stu-id="b8f6c-135">Once deployment has completed, switch back toohello browser window that opened in hello **Browse toohello app** step, and refresh hello page.</span></span>

![Обновленный пример приложения, выполняющегося в Azure](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="b8f6c-137">Управление новым веб-приложением Azure</span><span class="sxs-lookup"><span data-stu-id="b8f6c-137">Manage your new Azure web app</span></span>

<span data-ttu-id="b8f6c-138">Go toohello <a href="https://portal.azure.com" target="_blank">портал Azure</a> toomanage hello веб-приложения был создан.</span><span class="sxs-lookup"><span data-stu-id="b8f6c-138">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="b8f6c-139">Hello в левом меню, щелкните **службы приложений**, а затем щелкните имя hello Azure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="b8f6c-139">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Веб-приложения портала навигации tooAzure](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

<span data-ttu-id="b8f6c-141">Отобразится страница обзора вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="b8f6c-141">You see your web app's Overview page.</span></span> <span data-ttu-id="b8f6c-142">Вы можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление.</span><span class="sxs-lookup"><span data-stu-id="b8f6c-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span>

![Колонка службы приложений на портале Azure](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

<span data-ttu-id="b8f6c-144">меню слева Hello предоставляет различные страницы для настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="b8f6c-144">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="b8f6c-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b8f6c-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b8f6c-146">Использование PHP и MySQL</span><span class="sxs-lookup"><span data-stu-id="b8f6c-146">PHP with MySQL</span></span>](app-service-web-tutorial-php-mysql.md)
