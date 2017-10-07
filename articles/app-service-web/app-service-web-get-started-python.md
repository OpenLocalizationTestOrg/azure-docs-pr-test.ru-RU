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
# <a name="create-a-python-web-app-in-azure"></a>Создание веб-приложения Python в Azure

[Веб-приложения Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.  Это краткое руководство рассматривается toodevelop и развернуть tooAzure приложения Python веб-приложений. Создание веб-приложения hello, с помощью hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), и использовать Git toodeploy Python образец кода toohello веб-приложения.

![Пример приложения, выполняющегося в Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

Выполните действия hello ниже, с помощью компьютером Mac, Windows или Linux. После установки необходимых компонентов hello, требует toocomplete около пяти минут hello действия.
## <a name="prerequisites"></a>Предварительные требования

toocomplete этого учебника:

1. [установите Git](https://git-scm.com/);
1. [установите Python](https://www.python.org/downloads/).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="download-hello-sample"></a>Загрузить образец hello

В окне терминала запустите hello, следующая команда tooclone hello образец приложения репозитория tooyour локального компьютера.

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

В этом кратком руководстве все команды hello использовать этот toorun окно терминала.

Изменить toohello каталог, содержащий образец кода hello.

```bash
cd Python-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Выполните приложение hello локально

Установите необходимые hello пакетов с помощью `pip`.

```bash
pip install -r requirements.txt
```

Запустите приложение hello локально, откройте окно терминала и с помощью hello `Python` команда toolaunch hello встроенного Python веб-сервера.

```bash
python main.py
```

Откройте веб-браузер и перейдите toohello пример приложения http://localhost: 5000.

Вы увидите hello **Hello World** сообщения из примера приложения hello, отображаемое на странице приветствия.

![Пример приложения, выполняющегося локально](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

В окне терминала, нажмите клавишу **Ctrl + C** tooexit hello веб-сервера.

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Пустая страница веб-приложения](media/app-service-web-get-started-python/app-service-web-service-created.png)

Вы создали пустое веб-приложение в Azure.

## <a name="configure-toouse-python"></a>Настройка toouse Python

Используйте hello [набор параметров конфигурации для веб-приложения az](/cli/azure/webapp/config#set) команда tooconfigure hello веб-приложения toouse Python версию `3.4`.

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


Установка версии Python hello таким образом использует контейнер по умолчанию, предоставляемых платформой hello. toouse контейнера, см. hello Справочник CLI для hello [набор контейнера конфигурации веб-приложения az](/cli/azure/webapp/config/container#set) команды.

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

## <a name="browse-toohello-app"></a>Обзор toohello приложения

Обзор toohello развернуть приложение с помощью веб-браузере.

```bash
http://<app_name>.azurewebsites.net
```

пример кода Python Hello работает в веб-приложение службы приложений Azure.

![Пример приложения, выполняющегося в Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

**Поздравляем!** Ваш первый tooApp приложения Python службы после развертывания.

## <a name="update-and-redeploy-hello-code"></a>Обновление и повторное развертывание кода hello

С помощью локального текстовом редакторе откройте hello `main.py` файла в приложение hello Python и внести небольшое изменение toohello Далее toohello текст `return` инструкции:

```python
return 'Hello, Azure!'
```

Фиксация изменений в Git и затем отправьте tooAzure изменения кода hello.

```bash
git commit -am "updated output"
git push azure master
```

После завершения развертывания переключитесь задней toohello окно браузера, который открыт в hello [toohello приложения обзора](#browse-to-the-app) шаг и обновите страницу приветствия.

![Обновленный пример приложения, выполняющегося в Azure](media/app-service-web-get-started-python/hello-azure-in-browser.png)

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
> [Использование Python и PostgreSQL](app-service-web-tutorial-docker-python-postgresql-app.md)
