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
ms.topic: tutorial
ms.date: 06/13/2017
ms.author: rachelap
ms.custom: mvc, devcenter
ms.openlocfilehash: 81d08e047a3689d110195f2325b52c6c0457e644
ms.sourcegitcommit: 176c575aea7602682afd6214880aad0be6167c52
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/09/2018
---
# <a name="build-a-nodejs-restful-api-and-deploy-it-to-an-api-app-in-azure"></a>Создание API RESTful Node.js и его развертывание в приложении API в Azure

В этом кратком руководстве объясняется, как создать REST API, написанный с использованием Node.js [Express](http://expressjs.com/) с помощью определения [Swagger](http://swagger.io/), а затем развернуть его в Azure. Вы научитесь создавать приложения, используя программы командной строки, настраивать ресурсы в [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) и развертывать приложения с помощью Git.  Завершив работу, вы получите рабочий образец REST API в Azure.

## <a name="prerequisites"></a>Необходимые компоненты

* [Git.](https://git-scm.com/)
* [Node.js и NPM](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии. Чтобы узнать версию, выполните команду `az --version`. Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="prepare-your-environment"></a>Подготовка среды

1. В окне терминала выполните следующую команду для клонирования образца на локальный компьютер.

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. Перейдите в каталог, в котором содержится образец кода.

    ```bash
    cd app-service-api-node-contact-list
    ```

3. Установите [Swaggerize](https://www.npmjs.com/package/swaggerize-express) на локальном компьютере. Swaggerize — это средство, которое создает код Node.js для REST API из определения Swagger.

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a>Создание кода Node.js 

В этом разделе руководства моделируется рабочий процесс разработки API, в котором сначала создаются метаданные Swagger, а затем они используются при формировании (автоматическом создании) серверного кода для API. 

Перейдите в каталог *start* и затем запустите `yo swaggerize`. Swaggerize создаст для API проект Node.js из определения Swagger в *api.json*.

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

Когда Swaggerize запросит имя проекта, используйте имя *ContactList*.
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like to call this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-the-project-code"></a>Настройка кода проекта

1. Скопируйте папку *lib* в папку *ContactList*, созданную с помощью `yo swaggerize`, затем перейдите в каталог *ContactList*.

    ```bash
    cp -r lib ContactList/
    cd ContactList
    ```

2. Установите модули NPM: `jsonpath` и `swaggerize-ui`. 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. Замените код в файле *handlers/contacts.js* следующим кодом: 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    Этот код использует данные JSON, хранящиеся в файле *lib/contacts.json* (обрабатывается с помощью *lib/contactRepository.js*). Новый код *contacts.js* возвращает все контакты в репозитории как полезные данные JSON. 

4. Замените код в файле **handlers/contacts/{ИД}.js** следующим кодом:

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    Этот код позволяет использовать переменную пути исключительно для получения контакта с заданным идентификатором.

5. Замените код в файле **server.js** следующим кодом:

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

    Этот код вносит небольшие изменения, обеспечивая поддержку службы приложений Azure и предоставляя интерактивный веб-интерфейс для API.

### <a name="test-the-api-locally"></a>Локальное тестирование API

1. Настройка приложения Node.js
    ```bash
    npm start
    ```
    
2. Перейдите на страницу http://localhost:8000/contacts, чтобы просмотреть JSON-файл с полным списком контактов.
   
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

3. Перейдите на страницу http://localhost:8000/contacts/2 , чтобы просмотреть контакты с `id` 2.
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. Протестируйте API с помощью веб-интерфейса Swagger на странице http://localhost:8000/docs.
   
    ![Веб-интерфейс Swagger](media/app-service-web-tutorial-rest-api/swagger-ui.png)

## <a id="createapiapp"></a> Создание приложения API

В этом разделе с помощью Azure CLI 2.0 мы создадим ресурсы для размещения API в службе приложений Azure. 

1.  Войдите в подписку Azure с помощью команды [az login](/cli/azure/?view=azure-cli-latest#az_login) и следуйте инструкциям на экране.

    ```azurecli-interactive
    az login
    ```

2. Если у вас несколько подписок Azure, выберите нужную вместо подписки по умолчанию.

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-the-api-with-git"></a>Развертывание API с помощью Git

Разверните код в приложении API, отправив фиксации из локального репозитория Git в службу приложений Azure.

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. Инициализируйте новый репозиторий в каталоге *ContactList*. 

    ```bash
    git init .
    ```

3. Исключите каталог *node_modules*, созданный npm из Git ранее в руководстве. Создайте файл `.gitignore` в текущем каталоге и добавьте следующий текст в новую строку в файле (ее расположение не имеет значения).

    ```
    node_modules/
    ```
    Подтвердите, что папка `node_modules` должна игнорироваться `git status`.
    
4. Добавьте в `package.json` следующие строки. Код, написанный с помощью Swaggerize, не указывает версию модуля Node.js. Если версия не указана, Azure использует версию `0.10.18` по умолчанию, которая не совместима с созданным кодом.

    ```javascript
    "engines": {
        "node": "~0.10.22"
    },
    ```

5. Зафиксируйте изменения в репозитории.
    ```bash
    git add .
    git commit -m "initial version"
    ```

6. [!INCLUDE [Push to Azure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-the-api--in-azure"></a>Тестирование API в Azure

1. Откройте в браузере страницу http://app_name.azurewebsites.net/contacts. Как видите, мы получаем тот же JSON-файл, что и ранее при создании локального запроса в рамках этого руководства.

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

2. В браузере перейдите к конечной точке `http://app_name.azurewebsites.net/docs`, чтобы протестировать работу пользовательского интерфейса Swagger в Azure.

    ![Пользовательский интерфейс Swagger](media/app-service-web-tutorial-rest-api/swagger-azure-ui.png)

    Теперь можно развернуть обновления примера API в Azure. Для этого достаточно отправить фиксации в репозиторий Azure Git.

## <a name="clean-up"></a>Очистка

Чтобы удалить ресурсы, созданные в ходе работы с этим руководством, выполните следующую команду Azure CLI:

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a>Дальнейшие действия 
> [!div class="nextstepaction"]
> [Сопоставление существующего настраиваемого DNS-имени с веб-приложениями Azure](app-service-web-tutorial-custom-domain.md)

