---
title: "Создание статического веб-приложения HTML в Azure | Документация Майкрософт"
description: "Узнайте, как запускать веб-приложения в службе приложений Azure, развернув пример статического HTML-приложения."
services: app-service\web
documentationcenter: 
author: rick-anderson
manager: wpickett
editor: 
ms.assetid: 60495cc5-6963-4bf0-8174-52786d226c26
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/26/2017
ms.author: riande
ms.custom: mvc
ms.openlocfilehash: 42af5b08b8d2ff0c75fd73dcfa61c861647fd2c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-static-html-web-app-in-azure"></a><span data-ttu-id="bac1e-103">Создание статического веб-приложения HTML в Azure</span><span class="sxs-lookup"><span data-stu-id="bac1e-103">Create a static HTML web app in Azure</span></span>

<span data-ttu-id="bac1e-104">[Веб-приложения Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="bac1e-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="bac1e-105">В этом кратком руководстве объясняется, как развернуть базовый сайт HTML+CSS в веб-приложениях Azure.</span><span class="sxs-lookup"><span data-stu-id="bac1e-105">This quickstart shows how to deploy a basic HTML+CSS site to Azure Web Apps.</span></span> <span data-ttu-id="bac1e-106">Создайте веб-приложение с помощью [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) и разверните пример HTML-содержимого в веб-приложении с помощью Git.</span><span class="sxs-lookup"><span data-stu-id="bac1e-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy sample HTML content to the web app.</span></span>

![Домашняя страница в примере приложения](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="bac1e-108">Выполните действия, приведенные ниже, с помощью компьютера Mac, Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="bac1e-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="bac1e-109">После установки необходимых компонентов для выполнения этих шагов потребуется около пяти минут.</span><span class="sxs-lookup"><span data-stu-id="bac1e-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bac1e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bac1e-110">Prerequisites</span></span>

<span data-ttu-id="bac1e-111">Для работы с этим кратким руководством сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="bac1e-111">To complete this quickstart:</span></span>

- <span data-ttu-id="bac1e-112">[Установите Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)].</span><span class="sxs-lookup"><span data-stu-id="bac1e-112">[Install Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bac1e-113">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="bac1e-113">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="bac1e-114">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="bac1e-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="bac1e-115">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bac1e-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-the-sample"></a><span data-ttu-id="bac1e-116">Скачивание примера приложения</span><span class="sxs-lookup"><span data-stu-id="bac1e-116">Download the sample</span></span>

<span data-ttu-id="bac1e-117">В окне терминала выполните следующую команду, чтобы клонировать репозиторий с примером приложения на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="bac1e-117">In a terminal window, run the following command to clone the sample app repository to your local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

<span data-ttu-id="bac1e-118">Используйте это окно терминала для выполнения всех команд в рамках этого руководства.</span><span class="sxs-lookup"><span data-stu-id="bac1e-118">You use this terminal window to run all the commands in this quickstart.</span></span>

## <a name="view-the-html"></a><span data-ttu-id="bac1e-119">Просмотр HTML</span><span class="sxs-lookup"><span data-stu-id="bac1e-119">View the HTML</span></span>

<span data-ttu-id="bac1e-120">Перейдите в каталог, в котором содержится пример HTML.</span><span class="sxs-lookup"><span data-stu-id="bac1e-120">Navigate to the directory that contains the sample HTML.</span></span> <span data-ttu-id="bac1e-121">Откройте файл *index.html* в браузере.</span><span class="sxs-lookup"><span data-stu-id="bac1e-121">Open the *index.html* file in your browser.</span></span>

![Домашняя страница примера приложения](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in to Azure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Пустая страница веб-приложения](media/app-service-web-get-started-html/app-service-web-service-created.png)

<span data-ttu-id="bac1e-124">Вы создали пустое веб-приложение в Azure.</span><span class="sxs-lookup"><span data-stu-id="bac1e-124">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (13/13), 2.07 KiB | 0 bytes/s, done.
Total 13 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'cc39b1e4cb'.
remote: Generating deployment script.
remote: Generating deployment script for Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-to-the-app"></a><span data-ttu-id="bac1e-125">Переход в приложение</span><span class="sxs-lookup"><span data-stu-id="bac1e-125">Browse to the app</span></span>

<span data-ttu-id="bac1e-126">В браузере перейдите по URL-адресу веб-приложения Azure:</span><span class="sxs-lookup"><span data-stu-id="bac1e-126">In a browser, go to the Azure web app URL:</span></span>

```
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="bac1e-127">Страница выполняется как веб-приложение службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="bac1e-127">The page is running as an Azure App Service web app.</span></span>

![Домашняя страница примера приложения](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="bac1e-129">**Поздравляем!**</span><span class="sxs-lookup"><span data-stu-id="bac1e-129">**Congratulations!**</span></span> <span data-ttu-id="bac1e-130">Вы развернули свое первое HTML-приложение в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="bac1e-130">You've deployed your first HTML app to App Service.</span></span>

## <a name="update-and-redeploy-the-app"></a><span data-ttu-id="bac1e-131">Обновление и повторное развертывание приложения</span><span class="sxs-lookup"><span data-stu-id="bac1e-131">Update and redeploy the app</span></span>

<span data-ttu-id="bac1e-132">Откройте файл *index.html* в текстовом редакторе и измените разметку.</span><span class="sxs-lookup"><span data-stu-id="bac1e-132">Open the *index.html* file in a text editor, and make a change to the markup.</span></span> <span data-ttu-id="bac1e-133">Например, измените заголовок H1 "Служба приложений Azure — пример статического HTML-сайта" на "Служба приложений Azure".</span><span class="sxs-lookup"><span data-stu-id="bac1e-133">For example, change the H1 heading from "Azure App Service - Sample Static HTML Site" to just "Azure App Service\`.</span></span>

<span data-ttu-id="bac1e-134">Зафиксируйте изменения в Git, а затем отправьте изменения кода в Azure.</span><span class="sxs-lookup"><span data-stu-id="bac1e-134">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated HTML"
git push azure master
```

<span data-ttu-id="bac1e-135">Завершив развертывание, обновите страницу в браузере, чтобы увидеть изменения.</span><span class="sxs-lookup"><span data-stu-id="bac1e-135">Once deployment has completed, refresh your browser to see the changes.</span></span>

![Обновленная домашняя страница примера приложения](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="bac1e-137">Управление новым веб-приложением Azure</span><span class="sxs-lookup"><span data-stu-id="bac1e-137">Manage your new Azure web app</span></span>

<span data-ttu-id="bac1e-138">Перейдите на <a href="https://portal.azure.com" target="_blank">портал Azure</a> для управления созданным веб-приложением.</span><span class="sxs-lookup"><span data-stu-id="bac1e-138">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="bac1e-139">В меню слева выберите **Службы приложений**, а затем щелкните имя своего веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="bac1e-139">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Переход к веб-приложению Azure на портале](./media/app-service-web-get-started-html/portal1.png)

<span data-ttu-id="bac1e-141">Отобразится страница обзора вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="bac1e-141">You see your web app's Overview page.</span></span> <span data-ttu-id="bac1e-142">Вы можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление.</span><span class="sxs-lookup"><span data-stu-id="bac1e-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Колонка службы приложений на портале Azure](./media/app-service-web-get-started-html/portal2.png)

<span data-ttu-id="bac1e-144">В меню слева доступно несколько страниц для настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="bac1e-144">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="bac1e-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bac1e-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bac1e-146">Сопоставление пользовательского домена</span><span class="sxs-lookup"><span data-stu-id="bac1e-146">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
