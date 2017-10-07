---
title: "aaaCreate приложении Ruby, с помощью веб-приложений на платформе Linux | Документы Microsoft"
description: "Дополнительные сведения toocreate Ruby приложений с Azure web wpp в Linux."
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
ms.openlocfilehash: 99ce3b5ee16703a147787387bb02973defce8190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a><span data-ttu-id="1f601-104">Создание приложения Ruby с помощью веб-приложений на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="1f601-104">Create a Ruby App with Web Apps on Linux</span></span> 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="1f601-105">[Веб-приложения Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="1f601-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="1f601-106">Краткого руководства показывает, toocreate основные Ruby на направляющие приложение затем развертывания tooAzure как веб-приложения на платформе Linux.</span><span class="sxs-lookup"><span data-stu-id="1f601-106">This quickstart shows you how toocreate a basic Ruby on Rails application you then deploy it tooAzure as a Web App on Linux.</span></span>

![Приложение Hello World](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a><span data-ttu-id="1f601-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1f601-108">Prerequisites</span></span>

* <span data-ttu-id="1f601-109">[Ruby 2.4.1 или более поздней версии](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span><span class="sxs-lookup"><span data-stu-id="1f601-109">[Ruby 2.4.1 or higher](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span></span>
* <span data-ttu-id="1f601-110">[Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="1f601-110">[Git](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="1f601-111">[Активная подписка Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1f601-111">An [active Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a><span data-ttu-id="1f601-112">Загрузить образец hello</span><span class="sxs-lookup"><span data-stu-id="1f601-112">Download hello sample</span></span>

<span data-ttu-id="1f601-113">В окне терминала выполните hello, следующая команда tooclone hello образец приложения репозитория tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="1f601-113">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine:</span></span>

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-hello-application-locally"></a><span data-ttu-id="1f601-114">Запустите приложение hello локально</span><span class="sxs-lookup"><span data-stu-id="1f601-114">Run hello application locally</span></span>

<span data-ttu-id="1f601-115">Запустите сервер направляющие hello toowork приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1f601-115">Run hello rails server in order for hello application toowork.</span></span> <span data-ttu-id="1f601-116">Изменить toohello *hello world* каталога и hello `rails server` команда запускает hello server.</span><span class="sxs-lookup"><span data-stu-id="1f601-116">Change toohello *hello-world* directory, and hello `rails server` command starts hello server.</span></span>

```bash
cd hello-world\bin
rails server
```
    
<span data-ttu-id="1f601-117">С помощью веб-браузере перейдите слишком`http://localhost:3000` tootest приложение hello локально.</span><span class="sxs-lookup"><span data-stu-id="1f601-117">Using your web browser, navigate too`http://localhost:3000` tootest hello app locally.</span></span>  

![Приложение Hello World](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-toodisplay-welcome-message"></a><span data-ttu-id="1f601-119">Измените приложение toodisplay приветственное сообщение</span><span class="sxs-lookup"><span data-stu-id="1f601-119">Modify app toodisplay welcome message</span></span>

<span data-ttu-id="1f601-120">Изменения приложения hello, поэтому он отображает приветственное сообщение.</span><span class="sxs-lookup"><span data-stu-id="1f601-120">Modify hello application so it displays a welcome message.</span></span> <span data-ttu-id="1f601-121">Измените контроллера приложения hello, таким образом, чтобы он возвращает сообщение hello как toohello HTML-браузером.</span><span class="sxs-lookup"><span data-stu-id="1f601-121">Change hello application's controller so it returns hello message as HTML toohello browser.</span></span> 

<span data-ttu-id="1f601-122">Откройте файл *~/workspace/hello-world/app/controllers/application_controller.rb* для редактирования.</span><span class="sxs-lookup"><span data-stu-id="1f601-122">Open *~/workspace/hello-world/app/controllers/application_controller.rb* for editing.</span></span> <span data-ttu-id="1f601-123">Изменение hello `ApplicationController` toolook класс как hello следующий образец кода:</span><span class="sxs-lookup"><span data-stu-id="1f601-123">Modify hello `ApplicationController` class toolook like hello following code sample:</span></span>

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

<span data-ttu-id="1f601-124">Теперь приложение настроено.</span><span class="sxs-lookup"><span data-stu-id="1f601-124">Your app is now configured.</span></span> <span data-ttu-id="1f601-125">С помощью веб-браузере перейдите слишком`http://localhost:3000` tooconfirm hello корневой целевая страница.</span><span class="sxs-lookup"><span data-stu-id="1f601-125">Using your web browser, navigate too`http://localhost:3000` tooconfirm hello root landing page.</span></span>

![Приложение Hello World настроено](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a><span data-ttu-id="1f601-127">Создание веб-приложения Ruby в Azure</span><span class="sxs-lookup"><span data-stu-id="1f601-127">Create a Ruby web app on Azure</span></span>

<span data-ttu-id="1f601-128">Используйте hello [создать план служб приложений az](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate команда план служб приложений для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="1f601-128">Use hello [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) command toocreate an app service plan for your web app.</span></span> 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

<span data-ttu-id="1f601-129">Затем аналогичный hello [создать веб-приложение az](https://docs.microsoft.com/cli/azure/webapp) команда hello toocreate веб-приложения, использующего hello только что созданный план обслуживания.</span><span class="sxs-lookup"><span data-stu-id="1f601-129">Next, issue hello [az webapp create](https://docs.microsoft.com/cli/azure/webapp) command toocreate hello web app that uses hello newly created service plan.</span></span> <span data-ttu-id="1f601-130">Обратите внимание, среды выполнения hello установлен слишком`ruby|2.3`.</span><span class="sxs-lookup"><span data-stu-id="1f601-130">Notice that hello runtime is set too`ruby|2.3`.</span></span> <span data-ttu-id="1f601-131">Не забывайте tooreplace `<app name>` с именем уникальный приложения.</span><span class="sxs-lookup"><span data-stu-id="1f601-131">Don't forget tooreplace `<app name>` with a unique app name.</span></span>

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

<span data-ttu-id="1f601-132">После создания веб-приложения hello **Обзор** страница является доступной tooview.</span><span class="sxs-lookup"><span data-stu-id="1f601-132">Once hello web app is created, an **Overview** page is available tooview.</span></span> <span data-ttu-id="1f601-133">Перейдите tooit.</span><span class="sxs-lookup"><span data-stu-id="1f601-133">Navigate tooit.</span></span> <span data-ttu-id="1f601-134">отображается следующая всплывающая страница приветствия.</span><span class="sxs-lookup"><span data-stu-id="1f601-134">hello following splash page is displayed:</span></span>

![Страница заставки](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a><span data-ttu-id="1f601-136">Развертывание приложения</span><span class="sxs-lookup"><span data-stu-id="1f601-136">Deploy your application</span></span>

<span data-ttu-id="1f601-137">Используйте tooAzure Ruby приложения hello toodeploy Git.</span><span class="sxs-lookup"><span data-stu-id="1f601-137">Use Git toodeploy hello Ruby application tooAzure.</span></span> <span data-ttu-id="1f601-138">Hello веб-приложения уже настроен развертывания Git.</span><span class="sxs-lookup"><span data-stu-id="1f601-138">hello web app already has a Git deployment configured.</span></span> <span data-ttu-id="1f601-139">URL-адрес развертывания hello можно получить путем выполнения [развертывания веб-приложения az](https://docs.microsoft.com/cli/azure/webapp/deployment) команды.</span><span class="sxs-lookup"><span data-stu-id="1f601-139">You can retrieve hello deployment URL by issuing an [az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment) command.</span></span>  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="1f601-140">Обратите внимание, что URL-адрес Git hello имеет следующие формы, основанной на имя вашего веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1f601-140">Notice that hello Git URL has hello following form based on your web app name:</span></span>

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

<span data-ttu-id="1f601-141">Выполните следующие команды toodeploy hello локальное приложение tooyour веб-сайте Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1f601-141">Run hello following commands toodeploy hello local application tooyour Azure website:</span></span>

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="1f601-142">Убедитесь, что операции удаленного развертывания hello сообщать об успехе.</span><span class="sxs-lookup"><span data-stu-id="1f601-142">Confirm that hello remote deployment operations report success.</span></span> <span data-ttu-id="1f601-143">Hello команды создают выходной аналогичные toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="1f601-143">hello commands produce output similar toohello following text:</span></span>

```bash
remote: Using sass-rails 5.0.6
remote: Updating files in vendor/cache
remote: Bundle gems are installed into ./vendor/bundle
remote: Updating files in vendor/cache
remote: ~site/repository
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<your web app name>.scm.azurewebsites.net/<your web app name>.git
  579ccb....2ca5f31  master -> master
myuser@ubuntu1234:~workspace/<app name>$
```

<span data-ttu-id="1f601-144">После завершения развертывания hello, перезапустите веб-приложения для эффекта tootake hello развертывания с помощью hello [перезапуск веб-приложение az](https://docs.microsoft.com/cli/azure/webapp#restart) команды, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="1f601-144">Once hello deployment has completed, restart your web app for hello deployment tootake effect by using hello [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart) command, as shown here:</span></span>

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="1f601-145">Перейдите на сайт tooyour и проверки результатов hello.</span><span class="sxs-lookup"><span data-stu-id="1f601-145">Navigate tooyour site and verify hello results.</span></span>

```bash
http://<your web app name>.azurewebsites.net
```
![Обновленное веб-приложение](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> <span data-ttu-id="1f601-147">Во время перезапуска приложение hello попытка toobrowse hello сайта приводит код состояния HTTP `Error 503 Server unavailable`.</span><span class="sxs-lookup"><span data-stu-id="1f601-147">While hello app is restarting, attempting toobrowse hello site results in an HTTP status code `Error 503 Server unavailable`.</span></span> <span data-ttu-id="1f601-148">Может потребоваться несколько минут toofully перезапуска.</span><span class="sxs-lookup"><span data-stu-id="1f601-148">It may take a few minutes toofully restart.</span></span>
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a><span data-ttu-id="1f601-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1f601-149">Next steps</span></span>

[<span data-ttu-id="1f601-150">Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="1f601-150">Azure App Service Web App on Linux FAQ</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)