---
title: "aaaCreate Python веб-приложения в Azure | Документы Microsoft"
description: "Разверните свое первое приложение Hello World на языке Python в веб-приложении службы приложений Azure за считаные минуты."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 928ee2e5-6143-4c0c-8546-366f5a3d80ce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 03/17/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 42178d490d8aa8eaf93710667aad598794c62c8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-python-web-app-in-azure"></a><span data-ttu-id="7602c-103">Создание веб-приложения Python в Azure</span><span class="sxs-lookup"><span data-stu-id="7602c-103">Create a Python web app in Azure</span></span>

<span data-ttu-id="7602c-104">[Веб-приложения Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="7602c-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="7602c-105">Это краткое руководство рассматривается toodevelop и развернуть tooAzure приложения Python веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="7602c-105">This quickstart walks through how toodevelop and deploy a Python app tooAzure Web Apps.</span></span> <span data-ttu-id="7602c-106">Создание веб-приложения hello, с помощью hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), и использовать Git toodeploy Python образец кода toohello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="7602c-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample Python code toohello web app.</span></span>

![Пример приложения, выполняющегося в Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="7602c-108">Выполните действия hello ниже, с помощью компьютером Mac, Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="7602c-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="7602c-109">После установки необходимых компонентов hello, требует toocomplete около пяти минут hello действия.</span><span class="sxs-lookup"><span data-stu-id="7602c-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>
## <a name="prerequisites"></a><span data-ttu-id="7602c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7602c-110">Prerequisites</span></span>

<span data-ttu-id="7602c-111">toocomplete этого учебника:</span><span class="sxs-lookup"><span data-stu-id="7602c-111">toocomplete this tutorial:</span></span>

1. <span data-ttu-id="7602c-112">[установите Git](https://git-scm.com/);</span><span class="sxs-lookup"><span data-stu-id="7602c-112">[Install Git](https://git-scm.com/)</span></span>
1. <span data-ttu-id="7602c-113">[установите Python](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="7602c-113">[Install Python](https://www.python.org/downloads/)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7602c-114">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="7602c-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="7602c-115">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="7602c-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7602c-116">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7602c-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="7602c-117">Загрузить образец hello</span><span class="sxs-lookup"><span data-stu-id="7602c-117">Download hello sample</span></span>

<span data-ttu-id="7602c-118">В окне терминала запустите hello, следующая команда tooclone hello образец приложения репозитория tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="7602c-118">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

<span data-ttu-id="7602c-119">В этом кратком руководстве все команды hello использовать этот toorun окно терминала.</span><span class="sxs-lookup"><span data-stu-id="7602c-119">You use this terminal window toorun all hello commands in this quickstart.</span></span>

<span data-ttu-id="7602c-120">Изменить toohello каталог, содержащий образец кода hello.</span><span class="sxs-lookup"><span data-stu-id="7602c-120">Change toohello directory that contains hello sample code.</span></span>

```bash
cd Python-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="7602c-121">Выполните приложение hello локально</span><span class="sxs-lookup"><span data-stu-id="7602c-121">Run hello app locally</span></span>

<span data-ttu-id="7602c-122">Установите необходимые hello пакетов с помощью `pip`.</span><span class="sxs-lookup"><span data-stu-id="7602c-122">Install hello required packages using `pip`.</span></span>

```bash
pip install -r requirements.txt
```

<span data-ttu-id="7602c-123">Запустите приложение hello локально, откройте окно терминала и с помощью hello `Python` команда toolaunch hello встроенного Python веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="7602c-123">Run hello application locally by opening a terminal window and using hello `Python` command toolaunch hello built-in Python web server.</span></span>

```bash
python main.py
```

<span data-ttu-id="7602c-124">Откройте веб-браузер и перейдите toohello пример приложения http://localhost: 5000.</span><span class="sxs-lookup"><span data-stu-id="7602c-124">Open a web browser, and navigate toohello sample app at http://localhost:5000.</span></span>

<span data-ttu-id="7602c-125">Вы увидите hello **Hello World** сообщения из примера приложения hello, отображаемое на странице приветствия.</span><span class="sxs-lookup"><span data-stu-id="7602c-125">You can see hello **Hello World** message from hello sample app displayed in hello page.</span></span>

![Пример приложения, выполняющегося локально](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

<span data-ttu-id="7602c-127">В окне терминала, нажмите клавишу **Ctrl + C** tooexit hello веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="7602c-127">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Пустая страница веб-приложения](media/app-service-web-get-started-python/app-service-web-service-created.png)

<span data-ttu-id="7602c-129">Вы создали пустое веб-приложение в Azure.</span><span class="sxs-lookup"><span data-stu-id="7602c-129">You’ve created an empty new web app in Azure.</span></span>

## <a name="configure-toouse-python"></a><span data-ttu-id="7602c-130">Настройка toouse Python</span><span class="sxs-lookup"><span data-stu-id="7602c-130">Configure toouse Python</span></span>

<span data-ttu-id="7602c-131">Используйте hello [набор параметров конфигурации для веб-приложения az](/cli/azure/webapp/config#set) команда tooconfigure hello веб-приложения toouse Python версию `3.4`.</span><span class="sxs-lookup"><span data-stu-id="7602c-131">Use hello [az webapp config set](/cli/azure/webapp/config#set) command tooconfigure hello web app toouse Python version `3.4`.</span></span>

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


<span data-ttu-id="7602c-132">Установка версии Python hello таким образом использует контейнер по умолчанию, предоставляемых платформой hello.</span><span class="sxs-lookup"><span data-stu-id="7602c-132">Setting hello Python version this way uses a default container provided by hello platform.</span></span> <span data-ttu-id="7602c-133">toouse контейнера, см. hello Справочник CLI для hello [набор контейнера конфигурации веб-приложения az](/cli/azure/webapp/config/container#set) команды.</span><span class="sxs-lookup"><span data-stu-id="7602c-133">toouse your own container, see hello CLI reference for hello [az webapp config container set](/cli/azure/webapp/config/container#set) command.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 18, done.
Delta compression using up too4 threads.
Compressing objects: 100% (16/16), done.
Writing objects: 100% (18/18), 4.31 KiB | 0 bytes/s, done.
Total 18 (delta 4), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '44e74fe7dd'.
remote: Generating deployment script.
remote: Generating deployment script for python Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling python deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'main.py'
remote: Copying file: 'README.md'
remote: Copying file: 'requirements.txt'
remote: Copying file: 'virtualenv_proxy.py'
remote: Copying file: 'web.2.7.config'
remote: Copying file: 'web.3.4.config'
remote: Detected requirements.txt.  You can skip Python specific steps with a .skipPythonDeployment file.
remote: Detecting Python runtime from site configuration
remote: Detected python-3.4
remote: Creating python-3.4 virtual environment.
remote: .................................
remote: Pip install requirements.
remote: Successfully installed Flask click itsdangerous Jinja2 Werkzeug MarkupSafe
remote: Cleaning up...
remote: .
remote: Overwriting web.config with web.3.4.config
remote:         1 file(s) copied.
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="7602c-134">Обзор toohello приложения</span><span class="sxs-lookup"><span data-stu-id="7602c-134">Browse toohello app</span></span>

<span data-ttu-id="7602c-135">Обзор toohello развернуть приложение с помощью веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="7602c-135">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="7602c-136">пример кода Python Hello работает в веб-приложение службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="7602c-136">hello Python sample code is running in an Azure App Service web app.</span></span>

![Пример приложения, выполняющегося в Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="7602c-138">**Поздравляем!**</span><span class="sxs-lookup"><span data-stu-id="7602c-138">**Congratulations!**</span></span> <span data-ttu-id="7602c-139">Ваш первый tooApp приложения Python службы после развертывания.</span><span class="sxs-lookup"><span data-stu-id="7602c-139">You've deployed your first Python app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-code"></a><span data-ttu-id="7602c-140">Обновление и повторное развертывание кода hello</span><span class="sxs-lookup"><span data-stu-id="7602c-140">Update and redeploy hello code</span></span>

<span data-ttu-id="7602c-141">С помощью локального текстовом редакторе откройте hello `main.py` файла в приложение hello Python и внести небольшое изменение toohello Далее toohello текст `return` инструкции:</span><span class="sxs-lookup"><span data-stu-id="7602c-141">Using a local text editor, open hello `main.py` file in hello Python app, and make a small change toohello text next toohello `return` statement:</span></span>

```python
return 'Hello, Azure!'
```

<span data-ttu-id="7602c-142">Фиксация изменений в Git и затем отправьте tooAzure изменения кода hello.</span><span class="sxs-lookup"><span data-stu-id="7602c-142">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="7602c-143">После завершения развертывания переключитесь задней toohello окно браузера, который открыт в hello [toohello приложения обзора](#browse-to-the-app) шаг и обновите страницу приветствия.</span><span class="sxs-lookup"><span data-stu-id="7602c-143">Once deployment has completed, switch back toohello browser window that opened in hello [Browse toohello app](#browse-to-the-app) step, and refresh hello page.</span></span>

![Обновленный пример приложения, выполняющегося в Azure](media/app-service-web-get-started-python/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="7602c-145">Управление новым веб-приложением Azure</span><span class="sxs-lookup"><span data-stu-id="7602c-145">Manage your new Azure web app</span></span>

<span data-ttu-id="7602c-146">Go toohello <a href="https://portal.azure.com" target="_blank">портал Azure</a> toomanage hello веб-приложения был создан.</span><span class="sxs-lookup"><span data-stu-id="7602c-146">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="7602c-147">Hello в левом меню, щелкните **службы приложений**, а затем щелкните имя hello Azure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="7602c-147">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Веб-приложения портала навигации tooAzure](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="7602c-149">Отобразится страница обзора вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="7602c-149">You see your web app's Overview page.</span></span> <span data-ttu-id="7602c-150">Вы можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление.</span><span class="sxs-lookup"><span data-stu-id="7602c-150">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Колонка службы приложений на портале Azure](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="7602c-152">меню слева Hello предоставляет различные страницы для настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="7602c-152">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="7602c-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7602c-153">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7602c-154">Использование Python и PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="7602c-154">Python with PostgreSQL</span></span>](app-service-web-tutorial-docker-python-postgresql-app.md)
