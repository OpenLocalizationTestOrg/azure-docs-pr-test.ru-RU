---
title: "Создание веб-приложения PHP в Azure | Документация Майкрософт"
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
ms.openlocfilehash: 3a78e0b485046ad6228bf4819d3908042c298d1a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-php-web-app-in-azure"></a><span data-ttu-id="cb7d3-103">Создание веб-приложения PHP в Azure</span><span class="sxs-lookup"><span data-stu-id="cb7d3-103">Create a PHP web app in Azure</span></span>

<span data-ttu-id="cb7d3-104">[Веб-приложения Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="cb7d3-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="cb7d3-105">В этом кратком руководстве объясняется, как развернуть приложение PHP в веб-приложениях Azure.</span><span class="sxs-lookup"><span data-stu-id="cb7d3-105">This quickstart tutorial shows how to deploy a PHP app to Azure Web Apps.</span></span> <span data-ttu-id="cb7d3-106">Создайте веб-приложение с помощью [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) в Cloud Shell и разверните пример кода PHP в веб-приложении с помощью Git.</span><span class="sxs-lookup"><span data-stu-id="cb7d3-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) in Cloud Shell, and you use Git to deploy sample PHP code to the web app.</span></span>

<span data-ttu-id="cb7d3-107">![Пример приложения, выполняющегося в Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span><span class="sxs-lookup"><span data-stu-id="cb7d3-107">![Sample app running in Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span></span>

<span data-ttu-id="cb7d3-108">Выполните действия, приведенные ниже, с помощью компьютера Mac, Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="cb7d3-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="cb7d3-109">После установки необходимых компонентов для выполнения этих шагов потребуется около пяти минут.</span><span class="sxs-lookup"><span data-stu-id="cb7d3-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb7d3-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cb7d3-110">Prerequisites</span></span>

<span data-ttu-id="cb7d3-111">Для работы с этим кратким руководством сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="cb7d3-111">To complete this quickstart:</span></span>

* <span data-ttu-id="cb7d3-112">[установите Git](https://git-scm.com/);</span><span class="sxs-lookup"><span data-stu-id="cb7d3-112">[Install Git](https://git-scm.com/)</span></span>
* <span data-ttu-id="cb7d3-113">[установите PHP](https://php.net).</span><span class="sxs-lookup"><span data-stu-id="cb7d3-113">[Install PHP](https://php.net)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample-locally"></a><span data-ttu-id="cb7d3-114">Скачать пример на локальный компьютер</span><span class="sxs-lookup"><span data-stu-id="cb7d3-114">Download the sample locally</span></span>

<span data-ttu-id="cb7d3-115">Выполните следующие команды в окне терминала.</span><span class="sxs-lookup"><span data-stu-id="cb7d3-115">In a terminal window, run the following commands.</span></span> <span data-ttu-id="cb7d3-116">Так вы клонируете пример приложения на локальный компьютер и перейдете в каталог, содержащий пример кода.</span><span class="sxs-lookup"><span data-stu-id="cb7d3-116">This will clone the sample application to your local machine, and navigate to the directory containing the sample code.</span></span>

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="cb7d3-117">Локальный запуск приложения</span><span class="sxs-lookup"><span data-stu-id="cb7d3-117">Run the app locally</span></span>

<span data-ttu-id="cb7d3-118">Запустите приложение в локальной среде, открыв окно терминала и выполнив команду `php`, чтобы запустить встроенный веб-сервер PHP.</span><span class="sxs-lookup"><span data-stu-id="cb7d3-118">Run the application locally by opening a terminal window and using the `php` command to launch the built-in PHP web server.</span></span>

```bash
php -S localhost:8080
```

<span data-ttu-id="cb7d3-119">Откройте браузер и перейдите к примеру приложения по адресу http://localhost:8080.</span><span class="sxs-lookup"><span data-stu-id="cb7d3-119">Open a web browser, and navigate to the sample app at http://localhost:8080.</span></span>

<span data-ttu-id="cb7d3-120">На странице отобразится сообщение **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="cb7d3-120">You see the **Hello World!**</span></span> <span data-ttu-id="cb7d3-121">из примера приложения.</span><span class="sxs-lookup"><span data-stu-id="cb7d3-121">message from the sample app displayed in the page.</span></span>

![Пример приложения, выполняющегося локально](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

<span data-ttu-id="cb7d3-123">В окне терминала нажмите клавиши **CTRL+C**, чтобы выйти из веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="cb7d3-123">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![Пустая страница веб-приложения](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="cb7d3-125">Вы создали пустое веб-приложение в Azure.</span><span class="sxs-lookup"><span data-stu-id="cb7d3-125">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 2, done.
Delta compression using up to 4 threads.
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
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
   cc39b1e..25f1805  master -> master
```

## <a name="browse-to-the-app-locally"></a><span data-ttu-id="cb7d3-126">Переход к приложению на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="cb7d3-126">Browse to the app locally</span></span>

<span data-ttu-id="cb7d3-127">Перейдите в развертываемое приложение с помощью веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="cb7d3-127">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="cb7d3-128">Пример кода PHP выполняется в веб-приложении службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="cb7d3-128">The PHP sample code is running in an Azure App Service web app.</span></span>

![Пример приложения, выполняющегося в Azure](media/app-service-web-get-started-php/hello-world-in-browser.png)

<span data-ttu-id="cb7d3-130">**Поздравляем!**</span><span class="sxs-lookup"><span data-stu-id="cb7d3-130">**Congratulations!**</span></span> <span data-ttu-id="cb7d3-131">Вы развернули свое первое приложение PHP в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="cb7d3-131">You've deployed your first PHP app to App Service.</span></span>

## <a name="update-locally-and-redeploy-the-code"></a><span data-ttu-id="cb7d3-132">Обновление на локальном компьютере и повторное развертывание кода</span><span class="sxs-lookup"><span data-stu-id="cb7d3-132">Update locally and redeploy the code</span></span>

<span data-ttu-id="cb7d3-133">В локальном текстовом редакторе в приложении PHP откройте файл `index.php` и внесите небольшое изменение в текстовой строке рядом с `echo`:</span><span class="sxs-lookup"><span data-stu-id="cb7d3-133">Using a local text editor, open the `index.php` file within the PHP app, and make a small change to the text within the string next to `echo`:</span></span>

```php
echo "Hello Azure!";
```

<span data-ttu-id="cb7d3-134">Зафиксируйте изменения в Git, а затем отправьте изменения кода в Azure.</span><span class="sxs-lookup"><span data-stu-id="cb7d3-134">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="cb7d3-135">После завершения развертывания перейдите в окно браузера, открытое на шаге **перехода в приложение**, и обновите страницу.</span><span class="sxs-lookup"><span data-stu-id="cb7d3-135">Once deployment has completed, switch back to the browser window that opened in the **Browse to the app** step, and refresh the page.</span></span>

![Обновленный пример приложения, выполняющегося в Azure](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="cb7d3-137">Управление новым веб-приложением Azure</span><span class="sxs-lookup"><span data-stu-id="cb7d3-137">Manage your new Azure web app</span></span>

<span data-ttu-id="cb7d3-138">Перейдите на <a href="https://portal.azure.com" target="_blank">портал Azure</a> для управления созданным веб-приложением.</span><span class="sxs-lookup"><span data-stu-id="cb7d3-138">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="cb7d3-139">В меню слева выберите **Службы приложений**, а затем щелкните имя своего веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="cb7d3-139">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Переход к веб-приложению Azure на портале](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

<span data-ttu-id="cb7d3-141">Отобразится страница обзора вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="cb7d3-141">You see your web app's Overview page.</span></span> <span data-ttu-id="cb7d3-142">Вы можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление.</span><span class="sxs-lookup"><span data-stu-id="cb7d3-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span>

![Колонка службы приложений на портале Azure](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

<span data-ttu-id="cb7d3-144">В меню слева доступно несколько страниц для настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="cb7d3-144">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="cb7d3-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cb7d3-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cb7d3-146">Использование PHP и MySQL</span><span class="sxs-lookup"><span data-stu-id="cb7d3-146">PHP with MySQL</span></span>](app-service-web-tutorial-php-mysql.md)
