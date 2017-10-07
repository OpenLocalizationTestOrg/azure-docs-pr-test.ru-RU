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
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a>Создание приложения Ruby с помощью веб-приложений на платформе Linux 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

[Веб-приложения Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости. Краткого руководства показывает, toocreate основные Ruby на направляющие приложение затем развертывания tooAzure как веб-приложения на платформе Linux.

![Приложение Hello World](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a>Предварительные требования

* [Ruby 2.4.1 или более поздней версии](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).
* [Git](https://git-scm.com/downloads).
* [Активная подписка Azure](https://azure.microsoft.com/pricing/free-trial/).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a>Загрузить образец hello

В окне терминала выполните hello, следующая команда tooclone hello образец приложения репозитория tooyour локального компьютера.

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-hello-application-locally"></a>Запустите приложение hello локально

Запустите сервер направляющие hello toowork приложения hello. Изменить toohello *hello world* каталога и hello `rails server` команда запускает hello server.

```bash
cd hello-world\bin
rails server
```
    
С помощью веб-браузере перейдите слишком`http://localhost:3000` tootest приложение hello локально.  

![Приложение Hello World](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-toodisplay-welcome-message"></a>Измените приложение toodisplay приветственное сообщение

Изменения приложения hello, поэтому он отображает приветственное сообщение. Измените контроллера приложения hello, таким образом, чтобы он возвращает сообщение hello как toohello HTML-браузером. 

Откройте файл *~/workspace/hello-world/app/controllers/application_controller.rb* для редактирования. Изменение hello `ApplicationController` toolook класс как hello следующий образец кода:

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

Теперь приложение настроено. С помощью веб-браузере перейдите слишком`http://localhost:3000` tooconfirm hello корневой целевая страница.

![Приложение Hello World настроено](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a>Создание веб-приложения Ruby в Azure

Используйте hello [создать план служб приложений az](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate команда план служб приложений для веб-приложения. 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

Затем аналогичный hello [создать веб-приложение az](https://docs.microsoft.com/cli/azure/webapp) команда hello toocreate веб-приложения, использующего hello только что созданный план обслуживания. Обратите внимание, среды выполнения hello установлен слишком`ruby|2.3`. Не забывайте tooreplace `<app name>` с именем уникальный приложения.

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

После создания веб-приложения hello **Обзор** страница является доступной tooview. Перейдите tooit. отображается следующая всплывающая страница приветствия.

![Страница заставки](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a>Развертывание приложения

Используйте tooAzure Ruby приложения hello toodeploy Git. Hello веб-приложения уже настроен развертывания Git. URL-адрес развертывания hello можно получить путем выполнения [развертывания веб-приложения az](https://docs.microsoft.com/cli/azure/webapp/deployment) команды.  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

Обратите внимание, что URL-адрес Git hello имеет следующие формы, основанной на имя вашего веб-приложения hello.

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

Выполните следующие команды toodeploy hello локальное приложение tooyour веб-сайте Azure hello.

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

Убедитесь, что операции удаленного развертывания hello сообщать об успехе. Hello команды создают выходной аналогичные toohello следующий текст:

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

После завершения развертывания hello, перезапустите веб-приложения для эффекта tootake hello развертывания с помощью hello [перезапуск веб-приложение az](https://docs.microsoft.com/cli/azure/webapp#restart) команды, как показано ниже:

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

Перейдите на сайт tooyour и проверки результатов hello.

```bash
http://<your web app name>.azurewebsites.net
```
![Обновленное веб-приложение](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> Во время перезапуска приложение hello попытка toobrowse hello сайта приводит код состояния HTTP `Error 503 Server unavailable`. Может потребоваться несколько минут toofully перезапуска.
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a>Дальнейшие действия

[Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)