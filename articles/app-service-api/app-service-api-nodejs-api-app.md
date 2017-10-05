---
title: "Приложение API Node.js в службе приложений Azure | Документация Майкрософт"
description: "Узнайте, как создать API RESTful Node.js и развернуть его в приложении API с помощью службы приложений Azure."
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
ms.openlocfilehash: 806585edd43b9d2d678bfa41523e4d9d40af8cba
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-nodejs-restful-api-and-deploy-it-to-an-api-app-in-azure"></a><span data-ttu-id="ec92d-103">Создание API RESTful Node.js и его развертывание в приложении API в Azure</span><span class="sxs-lookup"><span data-stu-id="ec92d-103">Build a Node.js RESTful API and deploy it to an API app in Azure</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="ec92d-104">В этом кратком руководстве объясняется, как создать REST API, написанный с использованием Node.js, на платформе [Экспресс](http://expressjs.com/) с помощью определения [Swagger](http://swagger.io/), а затем развернуть его в Azure как [приложение API](app-service-api-apps-why-best-platform.md).</span><span class="sxs-lookup"><span data-stu-id="ec92d-104">This quickstart shows how to create a REST API, written with Node.js [Express](http://expressjs.com/), using a [Swagger](http://swagger.io/) definition and deploying it as an [API app](app-service-api-apps-why-best-platform.md) on Azure.</span></span> <span data-ttu-id="ec92d-105">Вы научитесь создавать приложения, используя программы командной строки, настраивать ресурсы в [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) и развертывать приложения с помощью Git.</span><span class="sxs-lookup"><span data-stu-id="ec92d-105">You create the app using command-line tools, configure resources with the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and deploy the app using Git.</span></span>  <span data-ttu-id="ec92d-106">Завершив работу, вы получите рабочий образец REST API в Azure.</span><span class="sxs-lookup"><span data-stu-id="ec92d-106">When you've finished, you have a working sample REST API running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec92d-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ec92d-107">Prerequisites</span></span>

* [<span data-ttu-id="ec92d-108">Git.</span><span class="sxs-lookup"><span data-stu-id="ec92d-108">Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="ec92d-109">Node.js и NPM</span><span class="sxs-lookup"><span data-stu-id="ec92d-109">Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ec92d-110">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="ec92d-110">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ec92d-111">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="ec92d-111">Run `az --version` to find the version.</span></span> <span data-ttu-id="ec92d-112">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ec92d-112">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-your-environment"></a><span data-ttu-id="ec92d-113">Подготовка среды</span><span class="sxs-lookup"><span data-stu-id="ec92d-113">Prepare your environment</span></span>

1. <span data-ttu-id="ec92d-114">В окне терминала выполните следующую команду для клонирования образца на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="ec92d-114">In a terminal window, run the following command to clone the sample to your local machine.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. <span data-ttu-id="ec92d-115">Перейдите в каталог, в котором содержится образец кода.</span><span class="sxs-lookup"><span data-stu-id="ec92d-115">Change to the directory that contains the sample code.</span></span>

    ```bash
    cd app-service-api-node-contact-list
    ```

3. <span data-ttu-id="ec92d-116">Установите [Swaggerize](https://www.npmjs.com/package/swaggerize-express) на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="ec92d-116">Install [Swaggerize](https://www.npmjs.com/package/swaggerize-express) on your local machine.</span></span> <span data-ttu-id="ec92d-117">Swaggerize — это средство, которое создает код Node.js для REST API из определения Swagger.</span><span class="sxs-lookup"><span data-stu-id="ec92d-117">Swaggerize is a tool that generates Node.js code for your REST API from a Swagger definition.</span></span>

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a><span data-ttu-id="ec92d-118">Создание кода Node.js</span><span class="sxs-lookup"><span data-stu-id="ec92d-118">Generate Node.js code</span></span> 

<span data-ttu-id="ec92d-119">В этом разделе руководства моделируется рабочий процесс разработки API, в котором сначала создаются метаданные Swagger, а затем они используются при формировании (автоматическом создании) серверного кода для API.</span><span class="sxs-lookup"><span data-stu-id="ec92d-119">This section of the tutorial models an API development workflow in which you create Swagger metadata first and use that to scaffold (auto-generate) server code for the API.</span></span> 

<span data-ttu-id="ec92d-120">Перейдите в каталог *start* и затем запустите `yo swaggerize`.</span><span class="sxs-lookup"><span data-stu-id="ec92d-120">Change directory to the *start* folder, then run `yo swaggerize`.</span></span> <span data-ttu-id="ec92d-121">Swaggerize создаст для API проект Node.js из определения Swagger в *api.json*.</span><span class="sxs-lookup"><span data-stu-id="ec92d-121">Swaggerize creates a Node.js project for your API from the Swagger definition in *api.json*.</span></span>

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

<span data-ttu-id="ec92d-122">Когда Swaggerize запросит имя проекта, используйте имя *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="ec92d-122">When Swaggerize asks for a project name, use *ContactList*.</span></span>
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like to call this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-the-project-code"></a><span data-ttu-id="ec92d-123">Настройка кода проекта</span><span class="sxs-lookup"><span data-stu-id="ec92d-123">Customize the project code</span></span>

1. <span data-ttu-id="ec92d-124">Скопируйте папку *lib* в папку *ContactList*, созданную с помощью `yo swaggerize`, затем перейдите в каталог *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="ec92d-124">Copy the *lib* folder into the *ContactList* folder created by `yo swaggerize`, then change directory into *ContactList*.</span></span>

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. <span data-ttu-id="ec92d-125">Установите модули NPM: `jsonpath` и `swaggerize-ui`.</span><span class="sxs-lookup"><span data-stu-id="ec92d-125">Install the `jsonpath` and `swaggerize-ui` NPM modules.</span></span> 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. <span data-ttu-id="ec92d-126">Замените код в файле *handlers/contacts.js* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="ec92d-126">Replace the code in the *handlers/contacts.js* with the following code:</span></span> 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    <span data-ttu-id="ec92d-127">Этот код использует данные JSON, хранящиеся в файле *lib/contacts.json* (обрабатывается с помощью *lib/contactRepository.js*).</span><span class="sxs-lookup"><span data-stu-id="ec92d-127">This code uses the JSON data stored in *lib/contacts.json* served by *lib/contactRepository.js*.</span></span> <span data-ttu-id="ec92d-128">Новый код *contacts.js* возвращает все контакты в репозитории как полезные данные JSON.</span><span class="sxs-lookup"><span data-stu-id="ec92d-128">The new *contacts.js* code returns all contacts in the repository as a JSON payload.</span></span> 

4. <span data-ttu-id="ec92d-129">Замените код в файле **handlers/contacts/{ИД}.js** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="ec92d-129">Replace the code in the **handlers/contacts/{id}.js** file with the following code:</span></span>

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    <span data-ttu-id="ec92d-130">Этот код позволяет использовать переменную пути исключительно для получения контакта с заданным идентификатором.</span><span class="sxs-lookup"><span data-stu-id="ec92d-130">This code lets you use a path variable to return only the contact with a given ID.</span></span>

5. <span data-ttu-id="ec92d-131">Замените код в файле **server.js** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="ec92d-131">Replace the code in **server.js** with the following code:</span></span>

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

    <span data-ttu-id="ec92d-132">Этот код вносит небольшие изменения, обеспечивая поддержку службы приложений Azure и предоставляя интерактивный веб-интерфейс для API.</span><span class="sxs-lookup"><span data-stu-id="ec92d-132">This code makes some small changes to let it work with Azure App Service and exposes an interactive web interface for your API.</span></span>

### <a name="test-the-api-locally"></a><span data-ttu-id="ec92d-133">Локальное тестирование API</span><span class="sxs-lookup"><span data-stu-id="ec92d-133">Test the API locally</span></span>

1. <span data-ttu-id="ec92d-134">Настройка приложения Node.js</span><span class="sxs-lookup"><span data-stu-id="ec92d-134">Start up the Node.js app</span></span>
    ```bash
    npm start
    ```
    
2. <span data-ttu-id="ec92d-135">Перейдите на страницу http://localhost:8000/contacts, чтобы просмотреть JSON-файл с полным списком контактов.</span><span class="sxs-lookup"><span data-stu-id="ec92d-135">Browse to http://localhost:8000/contacts to view the JSON for the entire contact list.</span></span>
   
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

3. <span data-ttu-id="ec92d-136">Перейдите на страницу http://localhost:8000/contacts/2 , чтобы просмотреть контакты с `id` 2.</span><span class="sxs-lookup"><span data-stu-id="ec92d-136">Browse to http://localhost:8000/contacts/2 to view the contact with an `id` of two.</span></span>
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. <span data-ttu-id="ec92d-137">Протестируйте API с помощью веб-интерфейса Swagger на странице http://localhost:8000/docs.</span><span class="sxs-lookup"><span data-stu-id="ec92d-137">Test the API using the Swagger web interface at http://localhost:8000/docs.</span></span>
   
    ![Веб-интерфейс Swagger](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <span data-ttu-id="ec92d-139"><a id="createapiapp"></a> Создание приложения API</span><span class="sxs-lookup"><span data-stu-id="ec92d-139"><a id="createapiapp"></a> Create an API App</span></span>

<span data-ttu-id="ec92d-140">В этом разделе с помощью Azure CLI 2.0 мы создадим ресурсы для размещения API в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="ec92d-140">In this section, you use the Azure CLI 2.0 to create the resources to host the API on Azure App Service.</span></span> 

1.  <span data-ttu-id="ec92d-141">Войдите в подписку Azure с помощью команды [az login](/cli/azure/#login) и следуйте инструкциям на экране.</span><span class="sxs-lookup"><span data-stu-id="ec92d-141">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

    ```azurecli-interactive
    az login
    ```

2. <span data-ttu-id="ec92d-142">Если у вас несколько подписок Azure, выберите нужную вместо подписки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ec92d-142">If you have multiple Azure subscriptions, change the default subscription to the desired one.</span></span>

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-the-api-with-git"></a><span data-ttu-id="ec92d-143">Развертывание API с помощью Git</span><span class="sxs-lookup"><span data-stu-id="ec92d-143">Deploy the API with Git</span></span>

<span data-ttu-id="ec92d-144">Разверните код в приложении API, отправив фиксации из локального репозитория Git в службу приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="ec92d-144">Deploy your code to the API app by pushing commits from your local Git repository to Azure App Service.</span></span>

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. <span data-ttu-id="ec92d-145">Инициализируйте новый репозиторий в каталоге *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="ec92d-145">Initialize a new repo in the *ContactList* directory.</span></span> 

    ```bash
    git init .
    ```

3. <span data-ttu-id="ec92d-146">Исключите каталог *node_modules*, созданный npm из Git ранее в руководстве.</span><span class="sxs-lookup"><span data-stu-id="ec92d-146">Exclude the *node_modules* directory created by npm in an earlier step in the tutorial from Git.</span></span> <span data-ttu-id="ec92d-147">Создайте файл `.gitignore` в текущем каталоге и добавьте следующий текст в новую строку в файле (ее расположение не имеет значения).</span><span class="sxs-lookup"><span data-stu-id="ec92d-147">Create a new `.gitignore` file in the current directory and add the following text on a new line anywhere in the file.</span></span>

    ```
    node_modules/
    ```
    <span data-ttu-id="ec92d-148">Подтвердите, что папка `node_modules` должна игнорироваться `git status`.</span><span class="sxs-lookup"><span data-stu-id="ec92d-148">Confirm the `node_modules` folder is being ignored with  `git status`.</span></span>

4. <span data-ttu-id="ec92d-149">Зафиксируйте изменения в репозитории.</span><span class="sxs-lookup"><span data-stu-id="ec92d-149">Commit the changes to the repo.</span></span>
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push to Azure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-the-api--in-azure"></a><span data-ttu-id="ec92d-150">Тестирование API в Azure</span><span class="sxs-lookup"><span data-stu-id="ec92d-150">Test the API  in Azure</span></span>

1. <span data-ttu-id="ec92d-151">Откройте в браузере страницу http://app_name.azurewebsites.net/contacts.</span><span class="sxs-lookup"><span data-stu-id="ec92d-151">Open a browser to http://app_name.azurewebsites.net/contacts.</span></span> <span data-ttu-id="ec92d-152">Как видите, мы получаем тот же JSON-файл, что и ранее при создании локального запроса в рамках этого руководства.</span><span class="sxs-lookup"><span data-stu-id="ec92d-152">You see the same JSON returned as when you made the request locally earlier in the tutorial.</span></span>

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

2. <span data-ttu-id="ec92d-153">В браузере перейдите к конечной точке `http://app_name.azurewebsites.net/docs`, чтобы протестировать работу пользовательского интерфейса Swagger в Azure.</span><span class="sxs-lookup"><span data-stu-id="ec92d-153">In a browser, go to the `http://app_name.azurewebsites.net/docs` endpoint to try out the Swagger UI running on Azure.</span></span>

    ![Пользовательский интерфейс Swagger](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    <span data-ttu-id="ec92d-155">Теперь можно развернуть обновления примера API в Azure. Для этого достаточно отправить фиксации в репозиторий Azure Git.</span><span class="sxs-lookup"><span data-stu-id="ec92d-155">You can now deploy updates to the sample API to Azure simply by pushing commits to the Azure Git repository.</span></span>

## <a name="clean-up"></a><span data-ttu-id="ec92d-156">Очистка</span><span class="sxs-lookup"><span data-stu-id="ec92d-156">Clean up</span></span>

<span data-ttu-id="ec92d-157">Чтобы удалить ресурсы, созданные в ходе работы с этим руководством, выполните следующую команду Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="ec92d-157">To clean up the resources created in this quickstart, run the following Azure CLI command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a><span data-ttu-id="ec92d-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ec92d-158">Next step</span></span> 
> [!div class="nextstepaction"]
> [<span data-ttu-id="ec92d-159">Использование приложения API из JavaScript с помощью CORS</span><span class="sxs-lookup"><span data-stu-id="ec92d-159">Consume API apps from JavaScript clients with CORS</span></span>](app-service-api-cors-consume-javascript.md)

