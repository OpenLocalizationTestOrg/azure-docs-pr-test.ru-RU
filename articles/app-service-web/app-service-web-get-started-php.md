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
# <a name="create-a-php-web-app-in-azure"></a>Создание веб-приложения PHP в Azure

[Веб-приложения Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.  Этот учебник показывает, как toodeploy tooAzure приложения PHP веб-приложений. Создание веб-приложения hello, с помощью hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) оболочки в облаке и вам использовать Git toodeploy PHP образец кода toohello веб-приложения.

![Пример приложения, выполняющегося в Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)

Выполните действия hello ниже, с помощью компьютером Mac, Windows или Linux. После установки необходимых компонентов hello, требует toocomplete около пяти минут hello действия.

## <a name="prerequisites"></a>Предварительные требования

toocomplete краткого руководства:

* [установите Git](https://git-scm.com/);
* [установите PHP](https://php.net).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample-locally"></a>Загрузить образец hello локально

В окне терминала выполните следующие команды hello. Будут клонировать hello образец приложения tooyour локального компьютера, после чего перейдите toohello каталога содержащий hello образец кода.

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Выполните приложение hello локально

Запустите приложение hello локально, откройте окно терминала и с помощью hello `php` команда toolaunch hello встроенного PHP веб-сервера.

```bash
php -S localhost:8080
```

Откройте веб-браузер и перейдите toohello пример приложения на http://localhost: 8080.

Вы видите hello **Здравствуй, мир!** сообщение из примера приложения hello, отображаемое на странице приветствия.

![Пример приложения, выполняющегося локально](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

В окне терминала, нажмите клавишу **Ctrl + C** tooexit hello веб-сервера.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![Пустая страница веб-приложения](media/app-service-web-get-started-php/app-service-web-service-created.png)

Вы создали пустое веб-приложение в Azure.

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

## <a name="browse-toohello-app-locally"></a>Обзор toohello приложения локально

Обзор toohello развернуть приложение с помощью веб-браузере.

```bash
http://<app_name>.azurewebsites.net
```

Hello PHP образце кода выполняется в веб-приложение службы приложений Azure.

![Пример приложения, выполняющегося в Azure](media/app-service-web-get-started-php/hello-world-in-browser.png)

**Поздравляем!** Ваш первый tooApp приложения PHP службы после развертывания.

## <a name="update-locally-and-redeploy-hello-code"></a>Обновлять локально и заново кода hello

С помощью локального текстовом редакторе откройте hello `index.php` файл включен в приложение PHP hello и сделать текст toohello небольшое изменение в строку hello рядом слишком`echo`:

```php
echo "Hello Azure!";
```

Фиксация изменений в Git и затем отправьте tooAzure изменения кода hello.

```bash
git commit -am "updated output"
git push azure master
```

После завершения развертывания переключитесь задней toohello окно браузера, который открыт в hello **toohello приложения обзора** шаг и обновите страницу приветствия.

![Обновленный пример приложения, выполняющегося в Azure](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a>Управление новым веб-приложением Azure

Go toohello <a href="https://portal.azure.com" target="_blank">портал Azure</a> toomanage hello веб-приложения был создан.

Hello в левом меню, щелкните **службы приложений**, а затем щелкните имя hello Azure веб-приложения.

![Веб-приложения портала навигации tooAzure](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

Отобразится страница обзора вашего веб-приложения. Вы можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление.

![Колонка службы приложений на портале Azure](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

меню слева Hello предоставляет различные страницы для настройки приложения. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Использование PHP и MySQL](app-service-web-tutorial-php-mysql.md)
