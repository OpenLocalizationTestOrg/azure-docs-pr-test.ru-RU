---
title: "aaaCreate Node.js веб-приложения в Azure | Документы Microsoft"
description: "Быстрое развертывание первого приложения Hello World на Node.js в веб-приложении службы приложений Azure."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 582bb3c2-164b-42f5-b081-95bfcb7a502a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/05/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 163edf83b2353755fc9fa2d75aed489038cf7c81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-web-app-in-azure"></a>Создание веб-приложений Node.js в Azure

[Веб-приложения Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.  Краткого руководства показано, как toodeploy tooAzure приложение Node.js веб-приложений. Создание веб-приложения hello, с помощью hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), и использовать Git toodeploy образец кода toohello веб-приложение Node.js.

![Пример приложения, выполняющегося в Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

Выполните действия hello ниже, с помощью компьютером Mac, Windows или Linux. После установки необходимых компонентов hello, требует toocomplete около пяти минут hello действия.   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a>Предварительные требования

toocomplete краткого руководства:

* [установите Git](https://git-scm.com/);
* [установите Node.j и NPM](https://nodejs.org/).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="download-hello-sample"></a>Загрузить образец hello

В окне терминала запустите hello, следующая команда tooclone hello образец приложения репозитория tooyour локального компьютера.

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

В этом кратком руководстве все команды hello использовать этот toorun окно терминала.

Изменить toohello каталог, содержащий образец кода hello.

```bash
cd nodejs-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Выполните приложение hello локально

Запустите приложение hello локально, откройте окно терминала и с помощью hello `npm start` hello toolaunch сценария, встроенных в сервер Node.js HTTP.

```bash
npm start
```

Откройте веб-браузер и перейдите toohello пример приложения на http://localhost:1337.

Вы видите hello **Hello World** сообщения из примера приложения hello, отображаемое на странице приветствия.

![Пример приложения, выполняющегося локально](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

В окне терминала, нажмите клавишу **Ctrl + C** tooexit hello веб-сервера.

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Пустая страница веб-приложения](media/app-service-web-get-started-php/app-service-web-service-created.png)

Вы создали пустое веб-приложение в Azure.

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 23, done.
Delta compression using up too4 threads.
Compressing objects: 100% (21/21), done.
Writing objects: 100% (23/23), 3.71 KiB | 0 bytes/s, done.
Total 23 (delta 8), reused 7 (delta 1)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'bf114df591'.
remote: Generating deployment script.
remote: Generating deployment script for node.js Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling node.js deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.js'
remote: Copying file: 'package.json'
remote: Copying file: 'process.json'
remote: Deleting file: 'hostingstart.html'
remote: Ignoring: .git
remote: Using start-up script index.js from package.json.
remote: Node.js versions available on hello platform are: 4.4.7, 4.5.0, 6.2.2, 6.6.0, 6.9.1.
remote: Selected node.js version 6.9.1. Use package.json file toochoose a different version.
remote: Selected npm version 3.10.8
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net:443/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a>Обзор toohello приложения

Обзор toohello развернуть приложение с помощью веб-браузере.

```bash
http://<app_name>.azurewebsites.net
```

Hello Node.js образце кода выполняется в веб-приложение службы приложений Azure.

![Пример приложения, выполняющегося в Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

**Поздравляем!** Ваш первый tooApp приложение Node.js службы после развертывания.

## <a name="update-and-redeploy-hello-code"></a>Обновление и повторное развертывание кода hello

В текстовом редакторе, откройте hello `index.js` в Node.js приложение hello и создайте текстовый toohello небольшое изменение в вызове hello слишком`response.end`:

```nodejs
response.end("Hello Azure!");
```

Фиксация изменений в Git и затем отправьте tooAzure изменения кода hello.

```bash
git commit -am "updated output"
git push azure master
```

После завершения развертывания переключитесь задней toohello окно браузера, который открыт в hello **toohello приложения обзора** шаг и нажмите кнопку обновления.

![Обновленный пример приложения, выполняющегося в Azure](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a>Управление новым веб-приложением Azure

Go toohello <a href="https://portal.azure.com" target="_blank">портал Azure</a> toomanage hello веб-приложения был создан.

Hello в левом меню, щелкните **службы приложений**, а затем щелкните имя hello Azure веб-приложения.

![Веб-приложения портала навигации tooAzure](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

Отобразится страница обзора вашего веб-приложения. Вы можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление. 

![Колонка службы приложений на портале Azure](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

меню слева Hello предоставляет различные страницы для настройки приложения. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Node.js с MongoDB](app-service-web-tutorial-nodejs-mongodb-app.md)
