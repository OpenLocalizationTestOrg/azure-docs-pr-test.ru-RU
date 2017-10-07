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
# <a name="build-a-nodejs-restful-api-and-deploy-it-tooan-api-app-in-azure"></a>Node.js RESTful API и развернет его tooan API приложение в Azure
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

Краткого руководства показано, как toocreate REST API, написанные на Node.js [Express](http://expressjs.com/), с использованием [Swagger](http://swagger.io/) определение и развертывание его как [приложения API](app-service-api-apps-why-best-platform.md) в Azure. Создание приложения hello, с помощью средства командной строки, настройте ресурсы с hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)и развертывание приложения hello, с помощью Git.  Завершив работу, вы получите рабочий образец REST API в Azure.

## <a name="prerequisites"></a>Предварительные требования

* [Git.](https://git-scm.com/)
* [Node.js и NPM](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="prepare-your-environment"></a>Подготовка среды

1. В окне терминала запустите hello, следующая команда tooclone hello образец tooyour локального компьютера.

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. Изменить toohello каталог, содержащий образец кода hello.

    ```bash
    cd app-service-api-node-contact-list
    ```

3. Установите [Swaggerize](https://www.npmjs.com/package/swaggerize-express) на локальном компьютере. Swaggerize — это средство, которое создает код Node.js для REST API из определения Swagger.

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a>Создание кода Node.js 

В этом разделе учебника hello моделирует рабочего процесса разработки API сначала создать метаданные Swagger и использовать этот tooscaffold (автоматическое создание) код сервера hello API. 

Изменить каталог toohello *запустить* папку, затем запустите `yo swaggerize`. Swaggerize создает проект Node.js для API из определения Swagger hello в *api.json*.

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

Когда Swaggerize запросит имя проекта, используйте имя *ContactList*.
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like toocall this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-hello-project-code"></a>Настройка проекта кода hello

1. Hello копирования *lib* папки в hello *ContactList* папки, созданные `yo swaggerize`, затем перейдите в *ContactList*.

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. Установка hello `jsonpath` и `swaggerize-ui` модули NPM. 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. Замените код hello в hello *handlers/contacts.js* с hello, следующий код: 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    Этот код использует данные JSON hello, хранятся в *lib/contacts.json* обслуживаемых *lib/contactRepository.js*. новый Hello *contacts.js* код возвращает все контакты в репозитории hello в качестве полезных данных JSON. 

4. Замените код hello в hello **handlers/contacts/{id}.js** файл с hello, следующий код:

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    Этот код позволяет использовать путь переменной tooreturn только hello контакт с заданным идентификатором.

5. Замените код hello в **server.js** с hello, следующий код:

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

    Этот код делает toolet некоторые небольшие изменения, она будет работать службе приложений Azure и предоставляет интерактивные веб-интерфейса API.

### <a name="test-hello-api-locally"></a>Тест hello API локально

1. Запустить приложение hello Node.js
    ```bash
    npm start
    ```
    
2. Обзор toohttp://localhost:8000 / обращается tooview hello JSON для hello весь список контактов.
   
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

3. Обзор toohttp://localhost:8000/contacts/2 tooview hello контакт с `id` двух.
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. С помощью веб-интерфейса Swagger hello в HTTP://localhost: 8000/docs API hello тестов.
   
    ![Веб-интерфейс Swagger](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <a id="createapiapp"></a> Создание приложения API

В этом разделе используется hello hello Azure CLI 2.0 toocreate hello ресурсы toohost API в службе приложений Azure. 

1.  Войдите в подписку Azure совместно с hello tooyour [входа az](/cli/azure/#login) команды и выполните hello на экране инструкциям.

    ```azurecli-interactive
    az login
    ```

2. Если у вас несколько подписок Azure, toohello подписки по умолчанию hello изменения требуемого один.

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-hello-api-with-git"></a>Развертывание hello API с Git

Разверните приложение API toohello кода с помощью принудительной отправки фиксаций из вашей локальной tooAzure репозитория Git службы приложений.

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. Инициализировать новый репозиторий в hello *ContactList* каталога. 

    ```bash
    git init .
    ```

3. Исключить hello *node_modules* каталога, созданных npm в предыдущем шаге, в учебнике hello из Git. Создайте новый `.gitignore` в текущем каталоге hello и добавьте следующий текст на новой строке в любом месте файла hello hello.

    ```
    node_modules/
    ```
    Подтвердите hello `node_modules` папку пропускается с `git status`.

4. Зафиксируйте hello изменения toohello репозитория.
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push tooAzure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-hello-api--in-azure"></a>Тест hello API в Azure

1. Откройте toohttp://app_name.azurewebsites.net/contacts браузера. Вы увидите hello, возвращенная же JSON как ранее в учебнике hello внесения hello запрос локально.

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

2. В браузере перейдите toohello `http://app_name.azurewebsites.net/docs` tootry конечной точки ожидания hello Swagger пользовательского интерфейса в Azure.

    ![Пользовательский интерфейс Swagger](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    Теперь можно развернуть обновления toohello пример API tooAzure просто нажатием toohello фиксации Azure репозитории.

## <a name="clean-up"></a>Очистка

tooclean hello ресурсов, созданные в этом кратком руководстве, запустите следующую команду Azure CLI hello:

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a>Дальнейшие действия 
> [!div class="nextstepaction"]
> [Использование приложения API из JavaScript с помощью CORS](app-service-api-cors-consume-javascript.md)

