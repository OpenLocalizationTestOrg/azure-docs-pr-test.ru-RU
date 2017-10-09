---
title: "aaaCreate статическим HTML веб-приложения в Azure | Документы Microsoft"
description: "Узнайте, как toorun веб-приложений в службе приложений Azure, развернув статическим HTML пример приложения."
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
ms.openlocfilehash: efd8c8189a3aa1ac35602b688eeb31bff6f5a373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-static-html-web-app-in-azure"></a><span data-ttu-id="7fd07-103">Создание статического веб-приложения HTML в Azure</span><span class="sxs-lookup"><span data-stu-id="7fd07-103">Create a static HTML web app in Azure</span></span>

<span data-ttu-id="7fd07-104">[Веб-приложения Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="7fd07-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="7fd07-105">Краткого руководства показано, как toodeploy основные HTML + CSS сайта tooAzure веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="7fd07-105">This quickstart shows how toodeploy a basic HTML+CSS site tooAzure Web Apps.</span></span> <span data-ttu-id="7fd07-106">Создание веб-приложения hello, с помощью hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), и использовать Git toodeploy образец HTML toohello содержимого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="7fd07-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample HTML content toohello web app.</span></span>

![Домашняя страница в примере приложения](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="7fd07-108">Выполните действия hello ниже, с помощью компьютером Mac, Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="7fd07-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="7fd07-109">После установки необходимых компонентов hello, требует toocomplete около пяти минут hello действия.</span><span class="sxs-lookup"><span data-stu-id="7fd07-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fd07-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7fd07-110">Prerequisites</span></span>

<span data-ttu-id="7fd07-111">toocomplete краткого руководства:</span><span class="sxs-lookup"><span data-stu-id="7fd07-111">toocomplete this quickstart:</span></span>

- <span data-ttu-id="7fd07-112">[Установите Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)].</span><span class="sxs-lookup"><span data-stu-id="7fd07-112">[Install Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7fd07-113">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="7fd07-113">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="7fd07-114">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="7fd07-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7fd07-115">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7fd07-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="7fd07-116">Загрузить образец hello</span><span class="sxs-lookup"><span data-stu-id="7fd07-116">Download hello sample</span></span>

<span data-ttu-id="7fd07-117">В окне терминала запустите hello, следующая команда tooclone hello образец приложения репозитория tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="7fd07-117">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

<span data-ttu-id="7fd07-118">В этом кратком руководстве все команды hello использовать этот toorun окно терминала.</span><span class="sxs-lookup"><span data-stu-id="7fd07-118">You use this terminal window toorun all hello commands in this quickstart.</span></span>

## <a name="view-hello-html"></a><span data-ttu-id="7fd07-119">Hello представление HTML</span><span class="sxs-lookup"><span data-stu-id="7fd07-119">View hello HTML</span></span>

<span data-ttu-id="7fd07-120">Перейдите в каталог toohello, который содержит образец hello HTML.</span><span class="sxs-lookup"><span data-stu-id="7fd07-120">Navigate toohello directory that contains hello sample HTML.</span></span> <span data-ttu-id="7fd07-121">Откройте hello *index.html* файла в браузере.</span><span class="sxs-lookup"><span data-stu-id="7fd07-121">Open hello *index.html* file in your browser.</span></span>

![Домашняя страница примера приложения](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Пустая страница веб-приложения](media/app-service-web-get-started-html/app-service-web-service-created.png)

<span data-ttu-id="7fd07-124">Вы создали пустое веб-приложение в Azure.</span><span class="sxs-lookup"><span data-stu-id="7fd07-124">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up too4 threads.
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
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="7fd07-125">Обзор toohello приложения</span><span class="sxs-lookup"><span data-stu-id="7fd07-125">Browse toohello app</span></span>

<span data-ttu-id="7fd07-126">В браузере перейдите на URL-адрес приложения Azure web toohello:</span><span class="sxs-lookup"><span data-stu-id="7fd07-126">In a browser, go toohello Azure web app URL:</span></span>

```
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="7fd07-127">Страница приветствия работает как веб-приложение службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="7fd07-127">hello page is running as an Azure App Service web app.</span></span>

![Домашняя страница примера приложения](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="7fd07-129">**Поздравляем!**</span><span class="sxs-lookup"><span data-stu-id="7fd07-129">**Congratulations!**</span></span> <span data-ttu-id="7fd07-130">Ваш первый tooApp приложения HTML службы после развертывания.</span><span class="sxs-lookup"><span data-stu-id="7fd07-130">You've deployed your first HTML app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-app"></a><span data-ttu-id="7fd07-131">Обновить и повторно развернуть приложение hello</span><span class="sxs-lookup"><span data-stu-id="7fd07-131">Update and redeploy hello app</span></span>

<span data-ttu-id="7fd07-132">Откройте hello *index.html* файл в текстовом редакторе и внести изменение toohello разметки.</span><span class="sxs-lookup"><span data-stu-id="7fd07-132">Open hello *index.html* file in a text editor, and make a change toohello markup.</span></span> <span data-ttu-id="7fd07-133">Изменить заголовок hello H1 из toojust Azure приложения — образец статических HTML «сайт службами», например, «служба приложений Azure ".</span><span class="sxs-lookup"><span data-stu-id="7fd07-133">For example, change hello H1 heading from "Azure App Service - Sample Static HTML Site" toojust "Azure App Service\`.</span></span>

<span data-ttu-id="7fd07-134">Фиксация изменений в Git и затем отправьте tooAzure изменения кода hello.</span><span class="sxs-lookup"><span data-stu-id="7fd07-134">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated HTML"
git push azure master
```

<span data-ttu-id="7fd07-135">После завершения развертывания обновления изменения hello toosee браузера.</span><span class="sxs-lookup"><span data-stu-id="7fd07-135">Once deployment has completed, refresh your browser toosee hello changes.</span></span>

![Обновленная домашняя страница примера приложения](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="7fd07-137">Управление новым веб-приложением Azure</span><span class="sxs-lookup"><span data-stu-id="7fd07-137">Manage your new Azure web app</span></span>

<span data-ttu-id="7fd07-138">Go toohello <a href="https://portal.azure.com" target="_blank">портал Azure</a> toomanage hello веб-приложения был создан.</span><span class="sxs-lookup"><span data-stu-id="7fd07-138">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="7fd07-139">Hello в левом меню, щелкните **службы приложений**, а затем щелкните имя hello Azure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="7fd07-139">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Веб-приложения портала навигации tooAzure](./media/app-service-web-get-started-html/portal1.png)

<span data-ttu-id="7fd07-141">Отобразится страница обзора вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="7fd07-141">You see your web app's Overview page.</span></span> <span data-ttu-id="7fd07-142">Вы можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление.</span><span class="sxs-lookup"><span data-stu-id="7fd07-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Колонка службы приложений на портале Azure](./media/app-service-web-get-started-html/portal2.png)

<span data-ttu-id="7fd07-144">меню слева Hello предоставляет различные страницы для настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="7fd07-144">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="7fd07-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7fd07-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7fd07-146">Сопоставление пользовательского домена</span><span class="sxs-lookup"><span data-stu-id="7fd07-146">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
