---
title: "aaaNode.js API приложения в службе приложений Azure | Документы Microsoft"
description: "Узнайте, как toocreate Node.js RESTful API и разверните его tooan API приложения в службе приложений Azure."
services: app-service\api
documentationcenter: node
author: bradygaster
manager: erikre
editor: 
ms.assetid: a820e400-06af-4852-8627-12b3db4a8e70
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: get-started-article
ms.date: 06/13/2017
ms.author: rachelap
ms.openlocfilehash: 3b3229c1453b6ca4d06bef26f476e92afda4e244
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-restful-api-and-deploy-it-tooan-api-app-in-azure"></a><span data-ttu-id="8e254-103">Node.js RESTful API и развернет его tooan API приложение в Azure</span><span class="sxs-lookup"><span data-stu-id="8e254-103">Build a Node.js RESTful API and deploy it tooan API app in Azure</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="8e254-104">Краткого руководства показано, как toocreate REST API, написанные на Node.js [Express](http://expressjs.com/), с использованием [Swagger](http://swagger.io/) определение и развертывание его как [приложения API](app-service-api-apps-why-best-platform.md) в Azure.</span><span class="sxs-lookup"><span data-stu-id="8e254-104">This quickstart shows how toocreate a REST API, written with Node.js [Express](http://expressjs.com/), using a [Swagger](http://swagger.io/) definition and deploying it as an [API app](app-service-api-apps-why-best-platform.md) on Azure.</span></span> <span data-ttu-id="8e254-105">Создание приложения hello, с помощью средства командной строки, настройте ресурсы с hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)и развертывание приложения hello, с помощью Git.</span><span class="sxs-lookup"><span data-stu-id="8e254-105">You create hello app using command-line tools, configure resources with hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and deploy hello app using Git.</span></span>  <span data-ttu-id="8e254-106">Завершив работу, вы получите рабочий образец REST API в Azure.</span><span class="sxs-lookup"><span data-stu-id="8e254-106">When you've finished, you have a working sample REST API running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e254-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8e254-107">Prerequisites</span></span>

* [<span data-ttu-id="8e254-108">Git.</span><span class="sxs-lookup"><span data-stu-id="8e254-108">Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="8e254-109">Node.js и NPM</span><span class="sxs-lookup"><span data-stu-id="8e254-109">Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8e254-110">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="8e254-110">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="8e254-111">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="8e254-111">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="8e254-112">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8e254-112">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-your-environment"></a><span data-ttu-id="8e254-113">Подготовка среды</span><span class="sxs-lookup"><span data-stu-id="8e254-113">Prepare your environment</span></span>

1. <span data-ttu-id="8e254-114">В окне терминала запустите hello, следующая команда tooclone hello образец tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="8e254-114">In a terminal window, run hello following command tooclone hello sample tooyour local machine.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. <span data-ttu-id="8e254-115">Изменить toohello каталог, содержащий образец кода hello.</span><span class="sxs-lookup"><span data-stu-id="8e254-115">Change toohello directory that contains hello sample code.</span></span>

    ```bash
    cd app-service-api-node-contact-list
    ```

3. <span data-ttu-id="8e254-116">Установите [Swaggerize](https://www.npmjs.com/package/swaggerize-express) на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="8e254-116">Install [Swaggerize](https://www.npmjs.com/package/swaggerize-express) on your local machine.</span></span> <span data-ttu-id="8e254-117">Swaggerize — это средство, которое создает код Node.js для REST API из определения Swagger.</span><span class="sxs-lookup"><span data-stu-id="8e254-117">Swaggerize is a tool that generates Node.js code for your REST API from a Swagger definition.</span></span>

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a><span data-ttu-id="8e254-118">Создание кода Node.js</span><span class="sxs-lookup"><span data-stu-id="8e254-118">Generate Node.js code</span></span> 

<span data-ttu-id="8e254-119">В этом разделе учебника hello моделирует рабочего процесса разработки API сначала создать метаданные Swagger и использовать этот tooscaffold (автоматическое создание) код сервера hello API.</span><span class="sxs-lookup"><span data-stu-id="8e254-119">This section of hello tutorial models an API development workflow in which you create Swagger metadata first and use that tooscaffold (auto-generate) server code for hello API.</span></span> 

<span data-ttu-id="8e254-120">Изменить каталог toohello *запустить* папку, затем запустите `yo swaggerize`.</span><span class="sxs-lookup"><span data-stu-id="8e254-120">Change directory toohello *start* folder, then run `yo swaggerize`.</span></span> <span data-ttu-id="8e254-121">Swaggerize создает проект Node.js для API из определения Swagger hello в *api.json*.</span><span class="sxs-lookup"><span data-stu-id="8e254-121">Swaggerize creates a Node.js project for your API from hello Swagger definition in *api.json*.</span></span>

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

<span data-ttu-id="8e254-122">Когда Swaggerize запросит имя проекта, используйте имя *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="8e254-122">When Swaggerize asks for a project name, use *ContactList*.</span></span>
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like toocall this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-hello-project-code"></a><span data-ttu-id="8e254-123">Настройка проекта кода hello</span><span class="sxs-lookup"><span data-stu-id="8e254-123">Customize hello project code</span></span>

1. <span data-ttu-id="8e254-124">Hello копирования *lib* папки в hello *ContactList* папки, созданные `yo swaggerize`, затем перейдите в *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="8e254-124">Copy hello *lib* folder into hello *ContactList* folder created by `yo swaggerize`, then change directory into *ContactList*.</span></span>

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. <span data-ttu-id="8e254-125">Установка hello `jsonpath` и `swaggerize-ui` модули NPM.</span><span class="sxs-lookup"><span data-stu-id="8e254-125">Install hello `jsonpath` and `swaggerize-ui` NPM modules.</span></span> 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. <span data-ttu-id="8e254-126">Замените код hello в hello *handlers/contacts.js* с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="8e254-126">Replace hello code in hello *handlers/contacts.js* with hello following code:</span></span> 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    <span data-ttu-id="8e254-127">Этот код использует данные JSON hello, хранятся в *lib/contacts.json* обслуживаемых *lib/contactRepository.js*.</span><span class="sxs-lookup"><span data-stu-id="8e254-127">This code uses hello JSON data stored in *lib/contacts.json* served by *lib/contactRepository.js*.</span></span> <span data-ttu-id="8e254-128">новый Hello *contacts.js* код возвращает все контакты в репозитории hello в качестве полезных данных JSON.</span><span class="sxs-lookup"><span data-stu-id="8e254-128">hello new *contacts.js* code returns all contacts in hello repository as a JSON payload.</span></span> 

4. <span data-ttu-id="8e254-129">Замените код hello в hello **handlers/contacts/{id}.js** файл с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="8e254-129">Replace hello code in hello **handlers/contacts/{id}.js** file with hello following code:</span></span>

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    <span data-ttu-id="8e254-130">Этот код позволяет использовать путь переменной tooreturn только hello контакт с заданным идентификатором.</span><span class="sxs-lookup"><span data-stu-id="8e254-130">This code lets you use a path variable tooreturn only hello contact with a given ID.</span></span>

5. <span data-ttu-id="8e254-131">Замените код hello в **server.js** с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="8e254-131">Replace hello code in **server.js** with hello following code:</span></span>

    ```javascript
    'use strict';

    var port = process.env.PORT || 8000; 

    var http = require('http');
    var express = require('express');
    var bodyParser = require('body-parser');
    var swaggerize = require('swaggerize-express');
    var swaggerUi = require('swaggerize-ui'); 
    var path = require('path');
    var fs = require("fs");
    
    fs.existsSync = fs.existsSync || require('path').existsSync;

    var app = express();

    var server = http.createServer(app);

    app.use(bodyParser.json());

    app.use(swaggerize({
        api: path.resolve('./config/swagger.json'),
        handlers: path.resolve('./handlers'),
        docspath: '/swagger' 
    }));

    // change four
    app.use('/docs', swaggerUi({
        docs: '/swagger'  
    }));

    server.listen(port, function () { 
    });
    ```   

    <span data-ttu-id="8e254-132">Этот код делает toolet некоторые небольшие изменения, она будет работать службе приложений Azure и предоставляет интерактивные веб-интерфейса API.</span><span class="sxs-lookup"><span data-stu-id="8e254-132">This code makes some small changes toolet it work with Azure App Service and exposes an interactive web interface for your API.</span></span>

### <a name="test-hello-api-locally"></a><span data-ttu-id="8e254-133">Тест hello API локально</span><span class="sxs-lookup"><span data-stu-id="8e254-133">Test hello API locally</span></span>

1. <span data-ttu-id="8e254-134">Запустить приложение hello Node.js</span><span class="sxs-lookup"><span data-stu-id="8e254-134">Start up hello Node.js app</span></span>
    ```bash
    npm start
    ```
    
2. <span data-ttu-id="8e254-135">Обзор toohttp://localhost:8000 / обращается tooview hello JSON для hello весь список контактов.</span><span class="sxs-lookup"><span data-stu-id="8e254-135">Browse toohttp://localhost:8000/contacts tooview hello JSON for hello entire contact list.</span></span>
   
   ```json
    {
        "id": 1,
        "name": "Barney Poland",
        "email": "barney@contoso.com"
    },
    {
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    },
    {
        "id": 3,
        "name": "Lora Riggs",
        "email": "lora@contoso.com"
    }
   ```

3. <span data-ttu-id="8e254-136">Обзор toohttp://localhost:8000/contacts/2 tooview hello контакт с `id` двух.</span><span class="sxs-lookup"><span data-stu-id="8e254-136">Browse toohttp://localhost:8000/contacts/2 tooview hello contact with an `id` of two.</span></span>
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. <span data-ttu-id="8e254-137">С помощью веб-интерфейса Swagger hello в HTTP://localhost: 8000/docs API hello тестов.</span><span class="sxs-lookup"><span data-stu-id="8e254-137">Test hello API using hello Swagger web interface at http://localhost:8000/docs.</span></span>
   
    ![Веб-интерфейс Swagger](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <span data-ttu-id="8e254-139"><a id="createapiapp"></a> Создание приложения API</span><span class="sxs-lookup"><span data-stu-id="8e254-139"><a id="createapiapp"></a> Create an API App</span></span>

<span data-ttu-id="8e254-140">В этом разделе используется hello hello Azure CLI 2.0 toocreate hello ресурсы toohost API в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="8e254-140">In this section, you use hello Azure CLI 2.0 toocreate hello resources toohost hello API on Azure App Service.</span></span> 

1.  <span data-ttu-id="8e254-141">Войдите в подписку Azure совместно с hello tooyour [входа az](/cli/azure/#login) команды и выполните hello на экране инструкциям.</span><span class="sxs-lookup"><span data-stu-id="8e254-141">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

    ```azurecli-interactive
    az login
    ```

2. <span data-ttu-id="8e254-142">Если у вас несколько подписок Azure, toohello подписки по умолчанию hello изменения требуемого один.</span><span class="sxs-lookup"><span data-stu-id="8e254-142">If you have multiple Azure subscriptions, change hello default subscription toohello desired one.</span></span>

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-hello-api-with-git"></a><span data-ttu-id="8e254-143">Развертывание hello API с Git</span><span class="sxs-lookup"><span data-stu-id="8e254-143">Deploy hello API with Git</span></span>

<span data-ttu-id="8e254-144">Разверните приложение API toohello кода с помощью принудительной отправки фиксаций из вашей локальной tooAzure репозитория Git службы приложений.</span><span class="sxs-lookup"><span data-stu-id="8e254-144">Deploy your code toohello API app by pushing commits from your local Git repository tooAzure App Service.</span></span>

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. <span data-ttu-id="8e254-145">Инициализировать новый репозиторий в hello *ContactList* каталога.</span><span class="sxs-lookup"><span data-stu-id="8e254-145">Initialize a new repo in hello *ContactList* directory.</span></span> 

    ```bash
    git init .
    ```

3. <span data-ttu-id="8e254-146">Исключить hello *node_modules* каталога, созданных npm в предыдущем шаге, в учебнике hello из Git.</span><span class="sxs-lookup"><span data-stu-id="8e254-146">Exclude hello *node_modules* directory created by npm in an earlier step in hello tutorial from Git.</span></span> <span data-ttu-id="8e254-147">Создайте новый `.gitignore` в текущем каталоге hello и добавьте следующий текст на новой строке в любом месте файла hello hello.</span><span class="sxs-lookup"><span data-stu-id="8e254-147">Create a new `.gitignore` file in hello current directory and add hello following text on a new line anywhere in hello file.</span></span>

    ```
    node_modules/
    ```
    <span data-ttu-id="8e254-148">Подтвердите hello `node_modules` папку пропускается с `git status`.</span><span class="sxs-lookup"><span data-stu-id="8e254-148">Confirm hello `node_modules` folder is being ignored with  `git status`.</span></span>

4. <span data-ttu-id="8e254-149">Зафиксируйте hello изменения toohello репозитория.</span><span class="sxs-lookup"><span data-stu-id="8e254-149">Commit hello changes toohello repo.</span></span>
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push tooAzure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-hello-api--in-azure"></a><span data-ttu-id="8e254-150">Тест hello API в Azure</span><span class="sxs-lookup"><span data-stu-id="8e254-150">Test hello API  in Azure</span></span>

1. <span data-ttu-id="8e254-151">Откройте toohttp://app_name.azurewebsites.net/contacts браузера.</span><span class="sxs-lookup"><span data-stu-id="8e254-151">Open a browser toohttp://app_name.azurewebsites.net/contacts.</span></span> <span data-ttu-id="8e254-152">Вы увидите hello, возвращенная же JSON как ранее в учебнике hello внесения hello запрос локально.</span><span class="sxs-lookup"><span data-stu-id="8e254-152">You see hello same JSON returned as when you made hello request locally earlier in hello tutorial.</span></span>

   ```json
   {
       "id": 1,
       "name": "Barney Poland",
       "email": "barney@contoso.com"
   },
   {
       "id": 2,
       "name": "Lacy Barrera",
       "email": "lacy@contoso.com"
   },
   {
       "id": 3,
       "name": "Lora Riggs",
       "email": "lora@contoso.com"
   }
   ```

2. <span data-ttu-id="8e254-153">В браузере перейдите toohello `http://app_name.azurewebsites.net/docs` tootry конечной точки ожидания hello Swagger пользовательского интерфейса в Azure.</span><span class="sxs-lookup"><span data-stu-id="8e254-153">In a browser, go toohello `http://app_name.azurewebsites.net/docs` endpoint tootry out hello Swagger UI running on Azure.</span></span>

    ![Пользовательский интерфейс Swagger](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    <span data-ttu-id="8e254-155">Теперь можно развернуть обновления toohello пример API tooAzure просто нажатием toohello фиксации Azure репозитории.</span><span class="sxs-lookup"><span data-stu-id="8e254-155">You can now deploy updates toohello sample API tooAzure simply by pushing commits toohello Azure Git repository.</span></span>

## <a name="clean-up"></a><span data-ttu-id="8e254-156">Очистка</span><span class="sxs-lookup"><span data-stu-id="8e254-156">Clean up</span></span>

<span data-ttu-id="8e254-157">tooclean hello ресурсов, созданные в этом кратком руководстве, запустите следующую команду Azure CLI hello:</span><span class="sxs-lookup"><span data-stu-id="8e254-157">tooclean up hello resources created in this quickstart, run hello following Azure CLI command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a><span data-ttu-id="8e254-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8e254-158">Next step</span></span> 
> [!div class="nextstepaction"]
> [<span data-ttu-id="8e254-159">Использование приложения API из JavaScript с помощью CORS</span><span class="sxs-lookup"><span data-stu-id="8e254-159">Consume API apps from JavaScript clients with CORS</span></span>](app-service-api-cors-consume-javascript.md)

