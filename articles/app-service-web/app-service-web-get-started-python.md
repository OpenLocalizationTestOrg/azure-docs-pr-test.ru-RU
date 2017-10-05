---
title: "Создание веб-приложения Python в Azure | Документация Майкрософт"
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
ms.openlocfilehash: 119f9770097c010cc360e0e204d06a307a268814
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-python-web-app-in-azure"></a><span data-ttu-id="9fb3f-103">Создание веб-приложения Python в Azure</span><span class="sxs-lookup"><span data-stu-id="9fb3f-103">Create a Python web app in Azure</span></span>

<span data-ttu-id="9fb3f-104">[Веб-приложения Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="9fb3f-105">В этом кратком руководстве объясняется, как разработать и развернуть приложение Python в веб-приложениях Azure.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-105">This quickstart walks through how to develop and deploy a Python app to Azure Web Apps.</span></span> <span data-ttu-id="9fb3f-106">Создайте веб-приложение с помощью [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) и разверните пример кода Python в веб-приложении с помощью Git.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy sample Python code to the web app.</span></span>

![Пример приложения, выполняющегося в Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="9fb3f-108">Выполните действия, приведенные ниже, с помощью компьютера Mac, Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="9fb3f-109">После установки необходимых компонентов для выполнения этих шагов потребуется около пяти минут.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>
## <a name="prerequisites"></a><span data-ttu-id="9fb3f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9fb3f-110">Prerequisites</span></span>

<span data-ttu-id="9fb3f-111">Для работы с этим руководством:</span><span class="sxs-lookup"><span data-stu-id="9fb3f-111">To complete this tutorial:</span></span>

1. <span data-ttu-id="9fb3f-112">[установите Git](https://git-scm.com/);</span><span class="sxs-lookup"><span data-stu-id="9fb3f-112">[Install Git](https://git-scm.com/)</span></span>
1. <span data-ttu-id="9fb3f-113">[установите Python](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="9fb3f-113">[Install Python](https://www.python.org/downloads/)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9fb3f-114">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-114">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="9fb3f-115">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="9fb3f-116">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9fb3f-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-the-sample"></a><span data-ttu-id="9fb3f-117">Скачивание примера приложения</span><span class="sxs-lookup"><span data-stu-id="9fb3f-117">Download the sample</span></span>

<span data-ttu-id="9fb3f-118">В окне терминала выполните следующую команду, чтобы клонировать репозиторий с примером приложения на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-118">In a terminal window, run the following command to clone the sample app repository to your local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

<span data-ttu-id="9fb3f-119">Используйте это окно терминала для выполнения всех команд в рамках этого руководства.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-119">You use this terminal window to run all the commands in this quickstart.</span></span>

<span data-ttu-id="9fb3f-120">Перейдите в каталог, в котором содержится образец кода.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-120">Change to the directory that contains the sample code.</span></span>

```bash
cd Python-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="9fb3f-121">Локальный запуск приложения</span><span class="sxs-lookup"><span data-stu-id="9fb3f-121">Run the app locally</span></span>

<span data-ttu-id="9fb3f-122">Установите необходимые пакеты с помощью `pip`.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-122">Install the required packages using `pip`.</span></span>

```bash
pip install -r requirements.txt
```

<span data-ttu-id="9fb3f-123">Запустите приложение в локальной среде, открыв окно терминала и выполнив команду `Python`, чтобы запустить встроенный веб-сервер Python.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-123">Run the application locally by opening a terminal window and using the `Python` command to launch the built-in Python web server.</span></span>

```bash
python main.py
```

<span data-ttu-id="9fb3f-124">Откройте браузер и перейдите к примеру приложения по адресу http://localhost:5000.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-124">Open a web browser, and navigate to the sample app at http://localhost:5000.</span></span>

<span data-ttu-id="9fb3f-125">На странице отобразится сообщение **Hello World** из примера приложения.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-125">You can see the **Hello World** message from the sample app displayed in the page.</span></span>

![Пример приложения, выполняющегося локально](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

<span data-ttu-id="9fb3f-127">В окне терминала нажмите клавиши **CTRL+C**, чтобы выйти из веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-127">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

[!INCLUDE [Log in to Azure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Пустая страница веб-приложения](media/app-service-web-get-started-python/app-service-web-service-created.png)

<span data-ttu-id="9fb3f-129">Вы создали пустое веб-приложение в Azure.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-129">You’ve created an empty new web app in Azure.</span></span>

## <a name="configure-to-use-python"></a><span data-ttu-id="9fb3f-130">Настройка использования Python</span><span class="sxs-lookup"><span data-stu-id="9fb3f-130">Configure to use Python</span></span>

<span data-ttu-id="9fb3f-131">Используйте команду [az webapp config set](/cli/azure/webapp/config#set), чтобы настроить в веб-приложении использование языка Python версии `3.4`.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-131">Use the [az webapp config set](/cli/azure/webapp/config#set) command to configure the web app to use Python version `3.4`.</span></span>

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


<span data-ttu-id="9fb3f-132">При такой настройке версии Python будет использоваться контейнер по умолчанию, предоставляемый платформой.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-132">Setting the Python version this way uses a default container provided by the platform.</span></span> <span data-ttu-id="9fb3f-133">Чтобы использовать собственный контейнер, см. сведения о команде [az webapp config container set](/cli/azure/webapp/config/container#set) в справочнике по интерфейсу командной строки.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-133">To use your own container, see the CLI reference for the [az webapp config container set](/cli/azure/webapp/config/container#set) command.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 18, done.
Delta compression using up to 4 threads.
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
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-to-the-app"></a><span data-ttu-id="9fb3f-134">Переход в приложение</span><span class="sxs-lookup"><span data-stu-id="9fb3f-134">Browse to the app</span></span>

<span data-ttu-id="9fb3f-135">Перейдите в развертываемое приложение с помощью веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-135">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="9fb3f-136">Пример кода Python выполняется в веб-приложении службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-136">The Python sample code is running in an Azure App Service web app.</span></span>

![Пример приложения, выполняющегося в Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="9fb3f-138">**Поздравляем!**</span><span class="sxs-lookup"><span data-stu-id="9fb3f-138">**Congratulations!**</span></span> <span data-ttu-id="9fb3f-139">Вы развернули свое первое приложение Python в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-139">You've deployed your first Python app to App Service.</span></span>

## <a name="update-and-redeploy-the-code"></a><span data-ttu-id="9fb3f-140">Обновление и повторное развертывание кода</span><span class="sxs-lookup"><span data-stu-id="9fb3f-140">Update and redeploy the code</span></span>

<span data-ttu-id="9fb3f-141">В локальном текстовом редакторе в приложении Python откройте файл `main.py` и внесите небольшое изменение в текст рядом с оператором `return`:</span><span class="sxs-lookup"><span data-stu-id="9fb3f-141">Using a local text editor, open the `main.py` file in the Python app, and make a small change to the text next to the `return` statement:</span></span>

```python
return 'Hello, Azure!'
```

<span data-ttu-id="9fb3f-142">Зафиксируйте изменения в Git, а затем отправьте изменения кода в Azure.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-142">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="9fb3f-143">После завершения развертывания перейдите в окно браузера, открытое на шаге [перехода в приложение](#browse-to-the-app), и обновите страницу.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-143">Once deployment has completed, switch back to the browser window that opened in the [Browse to the app](#browse-to-the-app) step, and refresh the page.</span></span>

![Обновленный пример приложения, выполняющегося в Azure](media/app-service-web-get-started-python/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="9fb3f-145">Управление новым веб-приложением Azure</span><span class="sxs-lookup"><span data-stu-id="9fb3f-145">Manage your new Azure web app</span></span>

<span data-ttu-id="9fb3f-146">Перейдите на <a href="https://portal.azure.com" target="_blank">портал Azure</a> для управления созданным веб-приложением.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-146">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="9fb3f-147">В меню слева выберите **Службы приложений**, а затем щелкните имя своего веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-147">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Переход к веб-приложению Azure на портале](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="9fb3f-149">Отобразится страница обзора вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-149">You see your web app's Overview page.</span></span> <span data-ttu-id="9fb3f-150">Вы можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-150">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Колонка службы приложений на портале Azure](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="9fb3f-152">В меню слева доступно несколько страниц для настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="9fb3f-152">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="9fb3f-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9fb3f-153">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9fb3f-154">Использование Python и PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="9fb3f-154">Python with PostgreSQL</span></span>](app-service-web-tutorial-docker-python-postgresql-app.md)
