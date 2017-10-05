---
title: "Создание приложения Ruby с помощью веб-приложений на платформе Linux | Документация Майкрософт"
description: "Узнайте, как создать приложения Ruby с помощью веб-приложений на платформе Linux."
keywords: "служба приложений azure, linux, oss, ruby"
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 6d00c73c-13cb-446f-8926-923db4101afa
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: wesmc;rachelap
ms.openlocfilehash: 17f3f1a2122c508501134a0c43ab6abce412fb44
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a><span data-ttu-id="119e6-104">Создание приложения Ruby с помощью веб-приложений на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="119e6-104">Create a Ruby App with Web Apps on Linux</span></span> 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="119e6-105">[Веб-приложения Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="119e6-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="119e6-106">В этом кратком руководстве показано, как создать базовое приложение Ruby on Rails и развернуть его в Azure в качестве веб-приложения на платформе Linux.</span><span class="sxs-lookup"><span data-stu-id="119e6-106">This quickstart shows you how to create a basic Ruby on Rails application you then deploy it to Azure as a Web App on Linux.</span></span>

![Приложение Hello World](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a><span data-ttu-id="119e6-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="119e6-108">Prerequisites</span></span>

* <span data-ttu-id="119e6-109">[Ruby 2.4.1 или более поздней версии](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span><span class="sxs-lookup"><span data-stu-id="119e6-109">[Ruby 2.4.1 or higher](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span></span>
* <span data-ttu-id="119e6-110">[Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="119e6-110">[Git](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="119e6-111">[Активная подписка Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="119e6-111">An [active Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample"></a><span data-ttu-id="119e6-112">Скачивание примера приложения</span><span class="sxs-lookup"><span data-stu-id="119e6-112">Download the sample</span></span>

<span data-ttu-id="119e6-113">В окне терминала выполните следующую команду, чтобы клонировать репозиторий с примером приложения на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="119e6-113">In a terminal window, run the following command to clone the sample app repository to your local machine:</span></span>

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-the-application-locally"></a><span data-ttu-id="119e6-114">Локальный запуск приложения</span><span class="sxs-lookup"><span data-stu-id="119e6-114">Run the application locally</span></span>

<span data-ttu-id="119e6-115">Запустите сервер Rails для работы приложения.</span><span class="sxs-lookup"><span data-stu-id="119e6-115">Run the rails server in order for the application to work.</span></span> <span data-ttu-id="119e6-116">Перейдите в каталог *hello-world* и запустите сервер, выполнив команду `rails server`.</span><span class="sxs-lookup"><span data-stu-id="119e6-116">Change to the *hello-world* directory, and the `rails server` command starts the server.</span></span>

```bash
cd hello-world\bin
rails server
```
    
<span data-ttu-id="119e6-117">С помощью веб-браузера перейдите к `http://localhost:3000`, чтобы протестировать приложение локально.</span><span class="sxs-lookup"><span data-stu-id="119e6-117">Using your web browser, navigate to `http://localhost:3000` to test the app locally.</span></span>    

![Приложение Hello World](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-to-display-welcome-message"></a><span data-ttu-id="119e6-119">Изменение приложения для отображения приветственного сообщения</span><span class="sxs-lookup"><span data-stu-id="119e6-119">Modify app to display welcome message</span></span>

<span data-ttu-id="119e6-120">Измените приложение, чтобы оно отображало приветственное сообщение.</span><span class="sxs-lookup"><span data-stu-id="119e6-120">Modify the application so it displays a welcome message.</span></span> <span data-ttu-id="119e6-121">Затем измените контроллер приложения, чтобы он возвращал сообщение в формате HTML браузеру.</span><span class="sxs-lookup"><span data-stu-id="119e6-121">Change the application's controller so it returns the message as HTML to the browser.</span></span> 

<span data-ttu-id="119e6-122">Откройте файл *~/workspace/hello-world/app/controllers/application_controller.rb* для редактирования.</span><span class="sxs-lookup"><span data-stu-id="119e6-122">Open *~/workspace/hello-world/app/controllers/application_controller.rb* for editing.</span></span> <span data-ttu-id="119e6-123">Измените класс `ApplicationController`, как показано в следующем примере кода:</span><span class="sxs-lookup"><span data-stu-id="119e6-123">Modify the `ApplicationController` class to look like the following code sample:</span></span>

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

<span data-ttu-id="119e6-124">Теперь приложение настроено.</span><span class="sxs-lookup"><span data-stu-id="119e6-124">Your app is now configured.</span></span> <span data-ttu-id="119e6-125">С помощью веб-браузера перейдите к `http://localhost:3000`, чтобы проверить корневую целевую страницу.</span><span class="sxs-lookup"><span data-stu-id="119e6-125">Using your web browser, navigate to `http://localhost:3000` to confirm the root landing page.</span></span>

![Приложение Hello World настроено](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a><span data-ttu-id="119e6-127">Создание веб-приложения Ruby в Azure</span><span class="sxs-lookup"><span data-stu-id="119e6-127">Create a Ruby web app on Azure</span></span>

<span data-ttu-id="119e6-128">Выполните команду [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create), чтобы создать план службы приложений для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="119e6-128">Use the [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) command to create an app service plan for your web app.</span></span> 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

<span data-ttu-id="119e6-129">Далее выполните команду [az webapp create](https://docs.microsoft.com/cli/azure/webapp), чтобы создать веб-приложение, использующее созданный план службы.</span><span class="sxs-lookup"><span data-stu-id="119e6-129">Next, issue the [az webapp create](https://docs.microsoft.com/cli/azure/webapp) command to create the web app that uses the newly created service plan.</span></span> <span data-ttu-id="119e6-130">Обратите внимание, что для среды выполнения установлено значение `ruby|2.3`.</span><span class="sxs-lookup"><span data-stu-id="119e6-130">Notice that the runtime is set to `ruby|2.3`.</span></span> <span data-ttu-id="119e6-131">Не забудьте указать уникальное имя приложения вместо `<app name>`.</span><span class="sxs-lookup"><span data-stu-id="119e6-131">Don't forget to replace `<app name>` with a unique app name.</span></span>

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

<span data-ttu-id="119e6-132">После создания веб-приложения страница **обзора** будет доступна для просмотра.</span><span class="sxs-lookup"><span data-stu-id="119e6-132">Once the web app is created, an **Overview** page is available to view.</span></span> <span data-ttu-id="119e6-133">Перейдите на эту страницу.</span><span class="sxs-lookup"><span data-stu-id="119e6-133">Navigate to it.</span></span> <span data-ttu-id="119e6-134">Отобразится следующая страница заставки:</span><span class="sxs-lookup"><span data-stu-id="119e6-134">The following splash page is displayed:</span></span>

![Страница заставки](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a><span data-ttu-id="119e6-136">Развертывание приложения</span><span class="sxs-lookup"><span data-stu-id="119e6-136">Deploy your application</span></span>

<span data-ttu-id="119e6-137">Используйте Git для развертывания приложения Ruby в Azure.</span><span class="sxs-lookup"><span data-stu-id="119e6-137">Use Git to deploy the Ruby application to Azure.</span></span> <span data-ttu-id="119e6-138">Для веб-приложения уже настроено развертывание Git.</span><span class="sxs-lookup"><span data-stu-id="119e6-138">The web app already has a Git deployment configured.</span></span> <span data-ttu-id="119e6-139">Выполните команду [az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment), чтобы извлечь URL-адрес развертывания.</span><span class="sxs-lookup"><span data-stu-id="119e6-139">You can retrieve the deployment URL by issuing an [az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment) command.</span></span>  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="119e6-140">Обратите внимание, что URL-адрес Git имеет следующий вид в соответствии с именем вашего веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="119e6-140">Notice that the Git URL has the following form based on your web app name:</span></span>

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

<span data-ttu-id="119e6-141">Выполните следующие команды, чтобы развернуть локальное приложение на веб-сайте Azure.</span><span class="sxs-lookup"><span data-stu-id="119e6-141">Run the following commands to deploy the local application to your Azure website:</span></span>

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="119e6-142">Убедитесь, что операции удаленного развертывания успешно выполнены.</span><span class="sxs-lookup"><span data-stu-id="119e6-142">Confirm that the remote deployment operations report success.</span></span> <span data-ttu-id="119e6-143">Выходные данные команд будут выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="119e6-143">The commands produce output similar to the following text:</span></span>

```bash
remote: Using sass-rails 5.0.6
remote: Updating files in vendor/cache
remote: Bundle gems are installed into ./vendor/bundle
remote: Updating files in vendor/cache
remote: ~site/repository
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
  579ccb....2ca5f31  master -> master
myuser@ubuntu1234:~workspace/<app name>$
```

<span data-ttu-id="119e6-144">После завершения развертывания перезапустите веб-приложение, чтобы изменения вступили в силу, выполнив команду [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart), как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="119e6-144">Once the deployment has completed, restart your web app for the deployment to take effect by using the [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart) command, as shown here:</span></span>

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="119e6-145">Перейдите на свой сайт и проверьте результаты.</span><span class="sxs-lookup"><span data-stu-id="119e6-145">Navigate to your site and verify the results.</span></span>

```bash
http://<your web app name>.azurewebsites.net
```
![Обновленное веб-приложение](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> <span data-ttu-id="119e6-147">Во время перезапуска приложения попытка просмотреть сайт приведет к ошибке с кодом состояния HTTP `Error 503 Server unavailable`.</span><span class="sxs-lookup"><span data-stu-id="119e6-147">While the app is restarting, attempting to browse the site results in an HTTP status code `Error 503 Server unavailable`.</span></span> <span data-ttu-id="119e6-148">На полный перезапуск может потребоваться несколько минут.</span><span class="sxs-lookup"><span data-stu-id="119e6-148">It may take a few minutes to fully restart.</span></span>
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a><span data-ttu-id="119e6-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="119e6-149">Next steps</span></span>

[<span data-ttu-id="119e6-150">Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="119e6-150">Azure App Service Web App on Linux FAQ</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)