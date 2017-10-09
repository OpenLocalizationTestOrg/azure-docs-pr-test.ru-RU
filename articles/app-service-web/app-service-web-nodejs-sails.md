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
# <a name="deploy-a-sailsjs-web-app-tooazure-app-service"></a><span data-ttu-id="b14de-104">Развертывание tooAzure приложения web Sails.js службы приложений</span><span class="sxs-lookup"><span data-stu-id="b14de-104">Deploy a Sails.js web app tooAzure App Service</span></span>
<span data-ttu-id="b14de-105">В этом учебнике показано как toodeploy tooAzure приложения Sails.js службы приложений.</span><span class="sxs-lookup"><span data-stu-id="b14de-105">This tutorial shows you how toodeploy a Sails.js app tooAzure App Service.</span></span> <span data-ttu-id="b14de-106">В процессе hello, можно обнаружить некоторые сведения о том, как tooconfigure вашей toorun приложения Node.js в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="b14de-106">In hello process, you can glean some general knowledge on how tooconfigure your Node.js app toorun in App Service.</span></span>

<span data-ttu-id="b14de-107">Здесь вы овладеете такими полезными навыками:</span><span class="sxs-lookup"><span data-stu-id="b14de-107">Here, you will learn useful skills like:</span></span>

* <span data-ttu-id="b14de-108">Настройка запуска приложения Sails.js в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="b14de-108">Configure a Sails.js app run in App Service.</span></span>
* <span data-ttu-id="b14de-109">Развертывание приложения tooApp службы, из командной строки hello.</span><span class="sxs-lookup"><span data-stu-id="b14de-109">Deploy an app tooApp Service from hello command line.</span></span>
* <span data-ttu-id="b14de-110">Чтение stderr и stdout tootroubleshoot журналы проблем развертывания.</span><span class="sxs-lookup"><span data-stu-id="b14de-110">Read stderr and stdout logs tootroubleshoot any deployment issues.</span></span>
* <span data-ttu-id="b14de-111">Сохранение переменных среды вне системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="b14de-111">Store environment variables outside of source control.</span></span>
* <span data-ttu-id="b14de-112">Получение доступа к переменным среды Azure из приложения.</span><span class="sxs-lookup"><span data-stu-id="b14de-112">Access Azure environment variables from your app.</span></span>
* <span data-ttu-id="b14de-113">Подключение базы данных tooa (MongoDB).</span><span class="sxs-lookup"><span data-stu-id="b14de-113">Connect tooa database (MongoDB).</span></span>

<span data-ttu-id="b14de-114">У вас должен быть опыт работы с Sails.js.</span><span class="sxs-lookup"><span data-stu-id="b14de-114">You should have working knowledge of Sails.js.</span></span> <span data-ttu-id="b14de-115">Этот учебник не предполагаемого toohelp вы с проблемами связанные toorunning Sail.js в целом.</span><span class="sxs-lookup"><span data-stu-id="b14de-115">This tutorial is not intended toohelp you with issues related toorunning Sail.js in general.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="b14de-116">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="b14de-116">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="b14de-117">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="b14de-117">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="b14de-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) — нашей CLI для hello классический и ресурсов развертывания модели управления</span><span class="sxs-lookup"><span data-stu-id="b14de-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span>
- <span data-ttu-id="b14de-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) -нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="b14de-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b14de-120">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b14de-120">Prerequisites</span></span>
* [<span data-ttu-id="b14de-121">Node.js</span><span class="sxs-lookup"><span data-stu-id="b14de-121">Node.js</span></span>](https://nodejs.org/)
* [<span data-ttu-id="b14de-122">Sails.js</span><span class="sxs-lookup"><span data-stu-id="b14de-122">Sails.js</span></span>](http://sailsjs.org/get-started)
* [<span data-ttu-id="b14de-123">Git.</span><span class="sxs-lookup"><span data-stu-id="b14de-123">Git</span></span>](http://www.git-scm.com/downloads)
* [<span data-ttu-id="b14de-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b14de-124">Azure CLI 2.0</span></span>](/cli/azure/install-az-cli2)
* <span data-ttu-id="b14de-125">Учетная запись Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b14de-125">A Microsoft Azure account.</span></span> <span data-ttu-id="b14de-126">Если у вас нет учетной записи, [подпишитесь на бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) или [активируйте преимущества для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="b14de-126">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="b14de-127">[Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/) возможно даже без учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="b14de-127">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="b14de-128">Создание начального приложения и воспроизведение к ней до часа tooan--без кредитной карты требуется, не обязательства.</span><span class="sxs-lookup"><span data-stu-id="b14de-128">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a><span data-ttu-id="b14de-129">Шаг 1. Создание и настройка приложения Sails.js в локальной среде</span><span class="sxs-lookup"><span data-stu-id="b14de-129">Step 1: Create and configure a Sails.js app locally</span></span>
<span data-ttu-id="b14de-130">Сначала быстро создайте приложение Sails.js по умолчанию в своей среде разработки, выполнив следующее.</span><span class="sxs-lookup"><span data-stu-id="b14de-130">First, quickly create a default Sails.js app in your development environment by following these steps:</span></span>

1. <span data-ttu-id="b14de-131">Откройте hello командной строки терминалов по своему усмотрению и `CD` tooa рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="b14de-131">Open hello command-line terminal of your choice and `CD` tooa working directory.</span></span>
2. <span data-ttu-id="b14de-132">Создайте приложение Sails.js и запустите его.</span><span class="sxs-lookup"><span data-stu-id="b14de-132">Create a Sails.js app and run it:</span></span>

        sails new <app_name>
        cd <app_name>
        sails lift

    <span data-ttu-id="b14de-133">Убедитесь, что можно перемещаться toohello домашнюю страницу по умолчанию в http://localhost:1377.</span><span class="sxs-lookup"><span data-stu-id="b14de-133">Make sure you can navigate toohello default home page at http://localhost:1377.</span></span>

1. <span data-ttu-id="b14de-134">Затем включите ведение журнала для Azure.</span><span class="sxs-lookup"><span data-stu-id="b14de-134">Next, enable logging for Azure.</span></span> <span data-ttu-id="b14de-135">В корневом каталоге создайте файл с именем `iisnode.yml` и добавьте hello, следующие две строки:</span><span class="sxs-lookup"><span data-stu-id="b14de-135">In your root directory, create a file called `iisnode.yml` and add hello following two lines:</span></span>

        loggingEnabled: true
        logDirectory: iisnode

    <span data-ttu-id="b14de-136">Ведение журнала включено для hello [iisnode](https://github.com/tjanczuk/iisnode) сервера, что службе приложений Azure использует toorun приложений Node.js.</span><span class="sxs-lookup"><span data-stu-id="b14de-136">Logging is now enabled for hello [iisnode](https://github.com/tjanczuk/iisnode) server that Azure App Service uses toorun Node.js apps.</span></span> 
    <span data-ttu-id="b14de-137">Дополнительные сведения о том, как это работает см. в разделе [как toodebug Node.js веб-приложения в службе приложений Azure](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="b14de-137">For more information on how this works, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

2. <span data-ttu-id="b14de-138">Настройте Sails.js приложения hello toouse-переменных среды Azure.</span><span class="sxs-lookup"><span data-stu-id="b14de-138">Next, configure hello Sails.js app toouse Azure environment variables.</span></span> <span data-ttu-id="b14de-139">Откройте config/env/production.js tooconfigure рабочей среды и настройте `port` и `hookTimeout`:</span><span class="sxs-lookup"><span data-stu-id="b14de-139">Open config/env/production.js tooconfigure your production environment, and set `port` and `hookTimeout`:</span></span>

        module.exports = {

            // Use process.env.port toohandle web requests toohello default HTTP port
            port: process.env.port,
            // Increase hooks timout too30 seconds
            // This avoids hello Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    <span data-ttu-id="b14de-140">Сведения об этих параметрах конфигурации можно найти в [документации по Sails.js](http://sailsjs.org/documentation/reference/configuration/sails-config).</span><span class="sxs-lookup"><span data-stu-id="b14de-140">You can find documentation for these configuration settings in the  [Sails.js Documentation](http://sailsjs.org/documentation/reference/configuration/sails-config).</span></span>

4. <span data-ttu-id="b14de-141">Далее следует жестко кодировать hello Node.js версии требуется toouse.</span><span class="sxs-lookup"><span data-stu-id="b14de-141">Next, hardcode hello Node.js version you want toouse.</span></span> <span data-ttu-id="b14de-142">В package.json, добавьте следующее hello `engines` свойство tooset hello Node.js версии tooone, нам нужно.</span><span class="sxs-lookup"><span data-stu-id="b14de-142">In package.json, add hello following `engines` property tooset hello Node.js version tooone that we want.</span></span>

        "engines": {
            "node": "6.9.1"
        },

5. <span data-ttu-id="b14de-143">Теперь инициализируйте репозиторий Git и сохраните свои файлы.</span><span class="sxs-lookup"><span data-stu-id="b14de-143">Finally, initialize a Git repository and commit your files.</span></span> <span data-ttu-id="b14de-144">В hello корневой каталог приложения (где — package.json), запустите следующие команды Git hello:</span><span class="sxs-lookup"><span data-stu-id="b14de-144">In hello application root (where package.json is), run hello following Git commands:</span></span>

        git init
        git add .
        git commit -m "<your commit message>"

<span data-ttu-id="b14de-145">Код является готов toobe развертывания.</span><span class="sxs-lookup"><span data-stu-id="b14de-145">Your code is ready toobe deployed.</span></span> 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a><span data-ttu-id="b14de-146">Шаг 2. Создание приложения Azure и развертывание Sails.js</span><span class="sxs-lookup"><span data-stu-id="b14de-146">Step 2: Create an Azure app and deploy Sails.js</span></span>

<span data-ttu-id="b14de-147">Далее создайте hello ресурса приложения службы в Azure и развертывания вашего tooit Sails.js приложения.</span><span class="sxs-lookup"><span data-stu-id="b14de-147">Next, create hello App Service resource in Azure and deploy your Sails.js app tooit.</span></span>

1. <span data-ttu-id="b14de-148">вход tooAzure следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b14de-148">log in tooAzure like so:</span></span>

        az login

    <span data-ttu-id="b14de-149">Выполните hello prompt toocontinue hello входа в браузере с учетной записью Майкрософт, с вашей подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="b14de-149">Follow hello prompt toocontinue hello login in a browser with a Microsoft account that has your Azure subscription.</span></span>

3. <span data-ttu-id="b14de-150">Настройка hello пользователя развертывания для приложения службы.</span><span class="sxs-lookup"><span data-stu-id="b14de-150">Set hello deployment user for App Service.</span></span> <span data-ttu-id="b14de-151">Вы развернете код позже с помощью этих учетных данных.</span><span class="sxs-lookup"><span data-stu-id="b14de-151">You will deploy code using these credentials later.</span></span>
   
        az appservice web deployment user set --user-name <username> --password <password>

3. <span data-ttu-id="b14de-152">Создайте [группу ресурсов](../azure-resource-manager/resource-group-overview.md) и присвойте ей имя.</span><span class="sxs-lookup"><span data-stu-id="b14de-152">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with a name.</span></span> <span data-ttu-id="b14de-153">В этом учебнике Node.js не обязательно tooknow его.</span><span class="sxs-lookup"><span data-stu-id="b14de-153">For this Node.js tutorial, you don't really need tooknow what it is.</span></span>

        az group create --location "<location>" --name my-sailsjs-app-group

    <span data-ttu-id="b14de-154">toosee какие возможные значения следует использовать для `<location>`, использовать hello `az appservice list-locations` команду CLI.</span><span class="sxs-lookup"><span data-stu-id="b14de-154">toosee what possible values you can use for `<location>`, use hello `az appservice list-locations` CLI command.</span></span>

3. <span data-ttu-id="b14de-155">Создайте [план службы приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) уровня "Бесплатный" и присвойте ему имя.</span><span class="sxs-lookup"><span data-stu-id="b14de-155">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) with a name.</span></span> <span data-ttu-id="b14de-156">В рамках этого руководства по Node.js вам достаточно знать, что этот план не предусматривает выставление счетов за веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="b14de-156">For this Node.js tutorial, just know that you won't be charged for web apps in this plan.</span></span>

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. <span data-ttu-id="b14de-157">Создайте веб-приложение с уникальным именем в `<app_name>`.</span><span class="sxs-lookup"><span data-stu-id="b14de-157">Create a new web app with a unique name in `<app_name>`.</span></span>

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a><span data-ttu-id="b14de-158">Шаг 3. Настройка и развертывание приложения Sails.js</span><span class="sxs-lookup"><span data-stu-id="b14de-158">Step 3: Configure and deploy your Sails.js app</span></span>

1. <span data-ttu-id="b14de-159">Настройте локальное развертывание Git для нового веб-приложения с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b14de-159">Configure local Git deployment for your new web app with hello following command:</span></span>

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="b14de-160">Вы получите выходных данных JSON наподобие этого, это означает, что настроен, удаленный репозиторий Git hello:</span><span class="sxs-lookup"><span data-stu-id="b14de-160">You will get a JSON output like this, which means that hello remote Git repository is configured:</span></span>

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. <span data-ttu-id="b14de-161">Добавить URL-адрес hello hello JSON в качестве удаленного для ваш локальный репозиторий Git (называется `azure` для простоты).</span><span class="sxs-lookup"><span data-stu-id="b14de-161">Add hello URL in hello JSON as a Git remote for your local repository (called `azure` for simplicity).</span></span>

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. <span data-ttu-id="b14de-162">Развертывание в образце кода toohello `azure` Git remote.</span><span class="sxs-lookup"><span data-stu-id="b14de-162">Deploy your sample code toohello `azure` Git remote.</span></span> <span data-ttu-id="b14de-163">При появлении запроса используйте учетные данные развертывания hello, настроенных ранее.</span><span class="sxs-lookup"><span data-stu-id="b14de-163">When prompted, use hello deployment credentials you configured earlier.</span></span>

        git push azure master

7. <span data-ttu-id="b14de-164">Наконец запуск динамической приложения Azure в обозревателе hello.</span><span class="sxs-lookup"><span data-stu-id="b14de-164">Finally, just launch your live Azure app in hello browser:</span></span>

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="b14de-165">Теперь вы увидите hello же Sails.js домашней страницы.</span><span class="sxs-lookup"><span data-stu-id="b14de-165">You should now see hello same Sails.js home page.</span></span>

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a><span data-ttu-id="b14de-166">Устранение неполадок развертывания</span><span class="sxs-lookup"><span data-stu-id="b14de-166">Troubleshoot your deployment</span></span>
<span data-ttu-id="b14de-167">Если какой-либо причине в службе приложений произошел сбой приложения Sails.js, найти журналы stderr hello toohelp устраните эту ошибку.</span><span class="sxs-lookup"><span data-stu-id="b14de-167">If your Sails.js application fails for some reason in App Service, find hello stderr logs toohelp troubleshoot it.</span></span>
<span data-ttu-id="b14de-168">Дополнительные сведения см. в разделе [как toodebug Node.js веб-приложения в службе приложений Azure](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="b14de-168">For more information, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>
<span data-ttu-id="b14de-169">Если приложение hello успешно запущен, hello stdout журнала следует показать знакомы сообщение hello:</span><span class="sxs-lookup"><span data-stu-id="b14de-169">If hello app has started successfully, hello stdout log should show you hello familiar message:</span></span>

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

<span data-ttu-id="b14de-170">Можно задать гранулярность журналы stdout hello в hello [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) файла.</span><span class="sxs-lookup"><span data-stu-id="b14de-170">You can control granularity of hello stdout logs in hello [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.</span></span>

## <a name="connect-tooa-database-in-azure"></a><span data-ttu-id="b14de-171">Подключение базы данных tooa в Azure</span><span class="sxs-lookup"><span data-stu-id="b14de-171">Connect tooa database in Azure</span></span>
<span data-ttu-id="b14de-172">База данных tooa tooconnect в Azure, создайте базу данных hello по своему усмотрению в Azure, таких как базы данных SQL Azure, MySQL, MongoDB, кэш Azure (redis —), т. д. и используйте соответствующий hello [адаптер хранилища данных](https://github.com/balderdashy/sails#compatibility) tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="b14de-172">tooconnect tooa database in Azure, you create hello database of your choice in Azure, such as Azure SQL Database, MySQL, MongoDB, Azure (Redis) Cache, etc., and use hello corresponding [datastore adapter](https://github.com/balderdashy/sails#compatibility) tooconnect tooit.</span></span> <span data-ttu-id="b14de-173">Hello действия, описанные в этом разделе показывается, как tooMongoDB tooconnect с помощью [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) базы данных, которая может поддерживать подключения клиентов MongoDB.</span><span class="sxs-lookup"><span data-stu-id="b14de-173">hello steps in this section show you how tooconnect tooMongoDB by using an [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, which can support MongoDB client connections.</span></span>

1. <span data-ttu-id="b14de-174">[Создайте учетную запись Cosmos DB с поддержкой протокола MongoDB](../documentdb/documentdb-create-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="b14de-174">[Create a Cosmos DB account with MongoDB protocol support](../documentdb/documentdb-create-mongodb-account.md).</span></span>
2. <span data-ttu-id="b14de-175">[Создайте коллекцию и базу данных Cosmos DB](../documentdb/documentdb-create-collection.md).</span><span class="sxs-lookup"><span data-stu-id="b14de-175">[Create a Cosmos DB collection and database](../documentdb/documentdb-create-collection.md).</span></span> <span data-ttu-id="b14de-176">Имя коллекции hello Hello не имеет значения, но требуется имя hello hello базы данных при подключении из Sails.js.</span><span class="sxs-lookup"><span data-stu-id="b14de-176">hello name of hello collection doesn't matter, but you need hello name of hello database when you connect from Sails.js.</span></span>
3. <span data-ttu-id="b14de-177">[Найти сведения для базы данных Cosmos DB hello](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="b14de-177">[Find hello connection information for your Cosmos DB database](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span></span>
2. <span data-ttu-id="b14de-178">Из командной строки терминала Установка адаптера MongoDB hello:</span><span class="sxs-lookup"><span data-stu-id="b14de-178">From your command-line terminal, install hello MongoDB adapter:</span></span>

        npm install sails-mongo --save

3. <span data-ttu-id="b14de-179">Откройте config/connections.js и добавьте hello после списка toohello объект соединения.</span><span class="sxs-lookup"><span data-stu-id="b14de-179">Open config/connections.js and add hello following connection object toohello list:</span></span>

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
    > <span data-ttu-id="b14de-180">Hello `ssl: true` возможность важна поскольку [Cosmos DB требует](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="b14de-180">hello `ssl: true` option is important because [Cosmos DB requires it](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 
    >
    >

4. <span data-ttu-id="b14de-181">Для каждой переменной среды (`process.env.*`), необходимо tooset его в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="b14de-181">For each environment variable (`process.env.*`), you need tooset it in App Service.</span></span> <span data-ttu-id="b14de-182">toodo, выполнения hello, следующие команды из терминала.</span><span class="sxs-lookup"><span data-stu-id="b14de-182">toodo this, run hello following commands from your terminal.</span></span> <span data-ttu-id="b14de-183">Используйте сведения о подключении hello для Cosmos базы данных.</span><span class="sxs-lookup"><span data-stu-id="b14de-183">Use hello connection information for your Cosmos DB.</span></span>

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="b14de-184">Чтобы предотвратить доступ системы управления версиями (Git) к конфиденциальным данным, в код приложения Azure необходимо добавить собственные параметры.</span><span class="sxs-lookup"><span data-stu-id="b14de-184">Putting your settings in Azure app settings keeps sensitive data out of your source control (Git).</span></span> <span data-ttu-id="b14de-185">Далее следует настроить разработки среды toouse hello же сведения о соединении.</span><span class="sxs-lookup"><span data-stu-id="b14de-185">Next, you will configure your development environment toouse hello same connection information.</span></span>
5. <span data-ttu-id="b14de-186">Откройте config/local.js и добавьте следующий объект подключений hello.</span><span class="sxs-lookup"><span data-stu-id="b14de-186">Open config/local.js and add hello following connections object:</span></span>

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    <span data-ttu-id="b14de-187">Эта конфигурация переопределяет параметры hello в файле config/connections.js для hello локальной среде.</span><span class="sxs-lookup"><span data-stu-id="b14de-187">This configuration overrides hello settings in your config/connections.js file for hello local environment.</span></span> <span data-ttu-id="b14de-188">Этот файл исключенными .gitignore по умолчанию hello в вашем проекте, поэтому он не будет храниться в Git.</span><span class="sxs-lookup"><span data-stu-id="b14de-188">This file is excluded by hello default .gitignore in your project, so it will not be stored in Git.</span></span> <span data-ttu-id="b14de-189">Теперь все возможности tooconnect tooyour DB Cosmos (MongoDB), базы данных и из Azure веб-приложения в локальной среде разработки.</span><span class="sxs-lookup"><span data-stu-id="b14de-189">Now, you are able tooconnect tooyour Cosmos DB (MongoDB) database both from your Azure web app and from your local development environment.</span></span>
6. <span data-ttu-id="b14de-190">Откройте config/env/production.js tooconfigure рабочей среды и добавьте следующие hello `models` объекта:</span><span class="sxs-lookup"><span data-stu-id="b14de-190">Open config/env/production.js tooconfigure your production environment, and add hello following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. <span data-ttu-id="b14de-191">Откройте config/env/development.js tooconfigure среды разработки и добавьте следующее hello `models` объекта:</span><span class="sxs-lookup"><span data-stu-id="b14de-191">Open config/env/development.js tooconfigure your development environment, and add hello following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    <span data-ttu-id="b14de-192">`migrate: 'alter'`позволяет использовать toocreate возможности миграции базы данных и легко обновлять коллекции базы данных или таблицы.</span><span class="sxs-lookup"><span data-stu-id="b14de-192">`migrate: 'alter'` lets you use database migration features toocreate and update database collections or tables easily.</span></span> <span data-ttu-id="b14de-193">Тем не менее `migrate: 'safe'` используется для вашей среды Azure (производство), поскольку Sails.js не позволит toouse `migrate: 'alter'` в рабочей среде (см. [Sails.js документации](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span><span class="sxs-lookup"><span data-stu-id="b14de-193">However, `migrate: 'safe'` is used for your Azure (production) environment because Sails.js does not allow you toouse `migrate: 'alter'` in a production environment (see [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span></span>
8. <span data-ttu-id="b14de-194">Из hello терминалов [создания](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) Sails.js [чертежом API](http://sailsjs.org/documentation/concepts/blueprints) , как вы затем выполнялся бы `sails lift` для создания базы данных hello Sails.js миграцию базы данных.</span><span class="sxs-lookup"><span data-stu-id="b14de-194">From hello terminal, [generate](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) a Sails.js [blueprint API](http://sailsjs.org/documentation/concepts/blueprints) like you normally would, then run `sails lift` to create hello database with Sails.js database migration.</span></span> <span data-ttu-id="b14de-195">Например:</span><span class="sxs-lookup"><span data-stu-id="b14de-195">For example:</span></span>

         sails generate api mywidget
         sails lift

    <span data-ttu-id="b14de-196">Hello `mywidget` модель, созданная при помощи этой команды пуст, но мы используем tooshow, что у нас есть подключение к базе данных.</span><span class="sxs-lookup"><span data-stu-id="b14de-196">hello `mywidget` model generated by this command is empty, but we can use it tooshow that we have database connectivity.</span></span>
    <span data-ttu-id="b14de-197">При выполнении `sails lift`, он создает отсутствует коллекции hello и таблицы для hello моделирует использует вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="b14de-197">When you run `sails lift`, it creates hello missing collections and tables for hello models your app uses.</span></span>
9. <span data-ttu-id="b14de-198">План API hello доступ, только что созданный в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="b14de-198">Access hello blueprint API you just created in hello browser.</span></span> <span data-ttu-id="b14de-199">Например:</span><span class="sxs-lookup"><span data-stu-id="b14de-199">For example:</span></span>

        http://localhost:1337/mywidget/create

    <span data-ttu-id="b14de-200">Hello API должен возвращать tooyou обратной записи создан hello в окне браузера hello, это означает, что ваша коллекция успешно создана.</span><span class="sxs-lookup"><span data-stu-id="b14de-200">hello API should return hello created entry back tooyou in hello browser window, which means that your collection is created  successfully.</span></span>

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. <span data-ttu-id="b14de-201">Теперь push вашей tooAzure изменения и обзор toomake приложения tooyour убедиться, что он по-прежнему работает.</span><span class="sxs-lookup"><span data-stu-id="b14de-201">Now, push your changes tooAzure, and browse tooyour app toomake sure it still works.</span></span>

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. <span data-ttu-id="b14de-202">Доступ API чертежом hello Azure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="b14de-202">Access hello blueprint API of your Azure web app.</span></span> <span data-ttu-id="b14de-203">Например:</span><span class="sxs-lookup"><span data-stu-id="b14de-203">For example:</span></span>

         http://<appname>.azurewebsites.net/mywidget/create

     <span data-ttu-id="b14de-204">Если hello API возвращает еще одну новую запись, Azure веб-приложения взаимодействуют базы данных tooyour DB Cosmos (MongoDB).</span><span class="sxs-lookup"><span data-stu-id="b14de-204">If hello API returns another new entry, then your Azure web app is talking tooyour Cosmos DB (MongoDB) database.</span></span>

## <a name="more-resources"></a><span data-ttu-id="b14de-205">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b14de-205">More resources</span></span>
* [<span data-ttu-id="b14de-206">Приступая к работе с веб-приложениями Node.js в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="b14de-206">Get started with Node.js web apps in Azure App Service</span></span>](app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="b14de-207">Использование модулей Node.js с приложениями Azure</span><span class="sxs-lookup"><span data-stu-id="b14de-207">Using Node.js Modules with Azure applications</span></span>](../nodejs-use-node-modules-azure-apps.md)
