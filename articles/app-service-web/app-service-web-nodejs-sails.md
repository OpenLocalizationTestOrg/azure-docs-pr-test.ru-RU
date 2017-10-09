---
title: "aaaDeploy tooAzure приложения web Sails.js службы приложений | Документы Microsoft"
description: "Узнайте, как toodeploy Node.js приложения службы приложений Azure. Этот учебник показывает, как toodeploy Sails.js веб-приложения."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 8877ddc8-1476-45ae-9e7f-3c75917b4564
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: f5b2518b9c87c040845f7268763862be8c15e83e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-sailsjs-web-app-tooazure-app-service"></a>Развертывание tooAzure приложения web Sails.js службы приложений
В этом учебнике показано как toodeploy tooAzure приложения Sails.js службы приложений. В процессе hello, можно обнаружить некоторые сведения о том, как tooconfigure вашей toorun приложения Node.js в службе приложений.

Здесь вы овладеете такими полезными навыками:

* Настройка запуска приложения Sails.js в службе приложений.
* Развертывание приложения tooApp службы, из командной строки hello.
* Чтение stderr и stdout tootroubleshoot журналы проблем развертывания.
* Сохранение переменных среды вне системы управления версиями.
* Получение доступа к переменным среды Azure из приложения.
* Подключение базы данных tooa (MongoDB).

У вас должен быть опыт работы с Sails.js. Этот учебник не предполагаемого toohelp вы с проблемами связанные toorunning Sail.js в целом.

## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI

Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

- [Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) — нашей CLI для hello классический и ресурсов развертывания модели управления
- [Azure CLI 2.0](app-service-web-nodejs-sails.md) -нашей нового поколения CLI для модели развертывания hello ресурсов управления

## <a name="prerequisites"></a>Предварительные требования
* [Node.js](https://nodejs.org/)
* [Sails.js](http://sailsjs.org/get-started)
* [Git.](http://www.git-scm.com/downloads)
* [Azure CLI 2.0](/cli/azure/install-az-cli2)
* Учетная запись Microsoft Azure. Если у вас нет учетной записи, [подпишитесь на бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) или [активируйте преимущества для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/) возможно даже без учетной записи Azure. Создание начального приложения и воспроизведение к ней до часа tooan--без кредитной карты требуется, не обязательства.
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a>Шаг 1. Создание и настройка приложения Sails.js в локальной среде
Сначала быстро создайте приложение Sails.js по умолчанию в своей среде разработки, выполнив следующее.

1. Откройте hello командной строки терминалов по своему усмотрению и `CD` tooa рабочий каталог.
2. Создайте приложение Sails.js и запустите его.

        sails new <app_name>
        cd <app_name>
        sails lift

    Убедитесь, что можно перемещаться toohello домашнюю страницу по умолчанию в http://localhost:1377.

1. Затем включите ведение журнала для Azure. В корневом каталоге создайте файл с именем `iisnode.yml` и добавьте hello, следующие две строки:

        loggingEnabled: true
        logDirectory: iisnode

    Ведение журнала включено для hello [iisnode](https://github.com/tjanczuk/iisnode) сервера, что службе приложений Azure использует toorun приложений Node.js. 
    Дополнительные сведения о том, как это работает см. в разделе [как toodebug Node.js веб-приложения в службе приложений Azure](web-sites-nodejs-debug.md).

2. Настройте Sails.js приложения hello toouse-переменных среды Azure. Откройте config/env/production.js tooconfigure рабочей среды и настройте `port` и `hookTimeout`:

        module.exports = {

            // Use process.env.port toohandle web requests toohello default HTTP port
            port: process.env.port,
            // Increase hooks timout too30 seconds
            // This avoids hello Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    Сведения об этих параметрах конфигурации можно найти в [документации по Sails.js](http://sailsjs.org/documentation/reference/configuration/sails-config).

4. Далее следует жестко кодировать hello Node.js версии требуется toouse. В package.json, добавьте следующее hello `engines` свойство tooset hello Node.js версии tooone, нам нужно.

        "engines": {
            "node": "6.9.1"
        },

5. Теперь инициализируйте репозиторий Git и сохраните свои файлы. В hello корневой каталог приложения (где — package.json), запустите следующие команды Git hello:

        git init
        git add .
        git commit -m "<your commit message>"

Код является готов toobe развертывания. 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a>Шаг 2. Создание приложения Azure и развертывание Sails.js

Далее создайте hello ресурса приложения службы в Azure и развертывания вашего tooit Sails.js приложения.

1. вход tooAzure следующим образом:

        az login

    Выполните hello prompt toocontinue hello входа в браузере с учетной записью Майкрософт, с вашей подпиской Azure.

3. Настройка hello пользователя развертывания для приложения службы. Вы развернете код позже с помощью этих учетных данных.
   
        az appservice web deployment user set --user-name <username> --password <password>

3. Создайте [группу ресурсов](../azure-resource-manager/resource-group-overview.md) и присвойте ей имя. В этом учебнике Node.js не обязательно tooknow его.

        az group create --location "<location>" --name my-sailsjs-app-group

    toosee какие возможные значения следует использовать для `<location>`, использовать hello `az appservice list-locations` команду CLI.

3. Создайте [план службы приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) уровня "Бесплатный" и присвойте ему имя. В рамках этого руководства по Node.js вам достаточно знать, что этот план не предусматривает выставление счетов за веб-приложения.

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. Создайте веб-приложение с уникальным именем в `<app_name>`.

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a>Шаг 3. Настройка и развертывание приложения Sails.js

1. Настройте локальное развертывание Git для нового веб-приложения с hello следующую команду:

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    Вы получите выходных данных JSON наподобие этого, это означает, что настроен, удаленный репозиторий Git hello:

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. Добавить URL-адрес hello hello JSON в качестве удаленного для ваш локальный репозиторий Git (называется `azure` для простоты).

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. Развертывание в образце кода toohello `azure` Git remote. При появлении запроса используйте учетные данные развертывания hello, настроенных ранее.

        git push azure master

7. Наконец запуск динамической приложения Azure в обозревателе hello.

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    Теперь вы увидите hello же Sails.js домашней страницы.

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a>Устранение неполадок развертывания
Если какой-либо причине в службе приложений произошел сбой приложения Sails.js, найти журналы stderr hello toohelp устраните эту ошибку.
Дополнительные сведения см. в разделе [как toodebug Node.js веб-приложения в службе приложений Azure](web-sites-nodejs-debug.md).
Если приложение hello успешно запущен, hello stdout журнала следует показать знакомы сообщение hello:

                   .-..-.
    
       Sails              <|    .-..-.
       v0.12.11            |\
                          /|.\
                         / || \
                       ,'  |'  \
                    .-'.-==|/_--'
                    `--'-------' 
       __---___--___---___--___---___--___
     ____---___--___---___--___---___--___-__

    Server lifted in `D:\home\site\wwwroot`
    toosee your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    tooshut down Sails, press <CTRL> + C at any time.

Можно задать гранулярность журналы stdout hello в hello [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) файла.

## <a name="connect-tooa-database-in-azure"></a>Подключение базы данных tooa в Azure
База данных tooa tooconnect в Azure, создайте базу данных hello по своему усмотрению в Azure, таких как базы данных SQL Azure, MySQL, MongoDB, кэш Azure (redis —), т. д. и используйте соответствующий hello [адаптер хранилища данных](https://github.com/balderdashy/sails#compatibility) tooconnect tooit. Hello действия, описанные в этом разделе показывается, как tooMongoDB tooconnect с помощью [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) базы данных, которая может поддерживать подключения клиентов MongoDB.

1. [Создайте учетную запись Cosmos DB с поддержкой протокола MongoDB](../documentdb/documentdb-create-mongodb-account.md).
2. [Создайте коллекцию и базу данных Cosmos DB](../documentdb/documentdb-create-collection.md). Имя коллекции hello Hello не имеет значения, но требуется имя hello hello базы данных при подключении из Sails.js.
3. [Найти сведения для базы данных Cosmos DB hello](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).
2. Из командной строки терминала Установка адаптера MongoDB hello:

        npm install sails-mongo --save

3. Откройте config/connections.js и добавьте hello после списка toohello объект соединения.

        docDbMongo: {
            adapter: 'sails-mongo',
            user: process.env.dbuser,
            password: process.env.dbpassword,
            host: process.env.dbhost,
            port: process.env.dbport,
            database: process.env.dbname,
            ssl: true
        },

    > [!NOTE] 
    > Hello `ssl: true` возможность важна поскольку [Cosmos DB требует](../cosmos-db/connect-mongodb-account.md#connection-string-requirements). 
    >
    >

4. Для каждой переменной среды (`process.env.*`), необходимо tooset его в службе приложений. toodo, выполнения hello, следующие команды из терминала. Используйте сведения о подключении hello для Cosmos базы данных.

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    Чтобы предотвратить доступ системы управления версиями (Git) к конфиденциальным данным, в код приложения Azure необходимо добавить собственные параметры. Далее следует настроить разработки среды toouse hello же сведения о соединении.
5. Откройте config/local.js и добавьте следующий объект подключений hello.

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    Эта конфигурация переопределяет параметры hello в файле config/connections.js для hello локальной среде. Этот файл исключенными .gitignore по умолчанию hello в вашем проекте, поэтому он не будет храниться в Git. Теперь все возможности tooconnect tooyour DB Cosmos (MongoDB), базы данных и из Azure веб-приложения в локальной среде разработки.
6. Откройте config/env/production.js tooconfigure рабочей среды и добавьте следующие hello `models` объекта:

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. Откройте config/env/development.js tooconfigure среды разработки и добавьте следующее hello `models` объекта:

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    `migrate: 'alter'`позволяет использовать toocreate возможности миграции базы данных и легко обновлять коллекции базы данных или таблицы. Тем не менее `migrate: 'safe'` используется для вашей среды Azure (производство), поскольку Sails.js не позволит toouse `migrate: 'alter'` в рабочей среде (см. [Sails.js документации](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).
8. Из hello терминалов [создания](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) Sails.js [чертежом API](http://sailsjs.org/documentation/concepts/blueprints) , как вы затем выполнялся бы `sails lift` для создания базы данных hello Sails.js миграцию базы данных. Например:

         sails generate api mywidget
         sails lift

    Hello `mywidget` модель, созданная при помощи этой команды пуст, но мы используем tooshow, что у нас есть подключение к базе данных.
    При выполнении `sails lift`, он создает отсутствует коллекции hello и таблицы для hello моделирует использует вашего приложения.
9. План API hello доступ, только что созданный в браузере hello. Например:

        http://localhost:1337/mywidget/create

    Hello API должен возвращать tooyou обратной записи создан hello в окне браузера hello, это означает, что ваша коллекция успешно создана.

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. Теперь push вашей tooAzure изменения и обзор toomake приложения tooyour убедиться, что он по-прежнему работает.

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. Доступ API чертежом hello Azure веб-приложения. Например:

         http://<appname>.azurewebsites.net/mywidget/create

     Если hello API возвращает еще одну новую запись, Azure веб-приложения взаимодействуют базы данных tooyour DB Cosmos (MongoDB).

## <a name="more-resources"></a>Дополнительные ресурсы
* [Приступая к работе с веб-приложениями Node.js в службе приложений Azure](app-service-web-get-started-nodejs.md)
* [Использование модулей Node.js с приложениями Azure](../nodejs-use-node-modules-azure-apps.md)
