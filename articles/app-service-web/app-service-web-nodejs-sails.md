---
title: "Развертывание веб-приложения Sails.js в службе приложений Azure | Документация Майкрософт"
description: "Сведения о развертывании приложения Node.js в службе приложений Azure. В этом учебнике показано, как развернуть веб-приложение Sails.js."
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
ms.openlocfilehash: e36fc5f5273f98c3cca91973db9910f32443ec7c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-a-sailsjs-web-app-to-azure-app-service"></a><span data-ttu-id="1bd01-104">Развертывание веб-приложения Sails.js в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="1bd01-104">Deploy a Sails.js web app to Azure App Service</span></span>
<span data-ttu-id="1bd01-105">В этом учебнике показано, как развернуть веб-приложение Sails.js в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="1bd01-105">This tutorial shows you how to deploy a Sails.js app to Azure App Service.</span></span> <span data-ttu-id="1bd01-106">При работе с учебником вы получите некоторые общие знания о настройке приложения Node.js для запуска в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="1bd01-106">In the process, you can glean some general knowledge on how to configure your Node.js app to run in App Service.</span></span>

<span data-ttu-id="1bd01-107">Здесь вы овладеете такими полезными навыками:</span><span class="sxs-lookup"><span data-stu-id="1bd01-107">Here, you will learn useful skills like:</span></span>

* <span data-ttu-id="1bd01-108">Настройка запуска приложения Sails.js в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="1bd01-108">Configure a Sails.js app run in App Service.</span></span>
* <span data-ttu-id="1bd01-109">Развертывание приложения в службе приложений из командной строки.</span><span class="sxs-lookup"><span data-stu-id="1bd01-109">Deploy an app to App Service from the command line.</span></span>
* <span data-ttu-id="1bd01-110">Устранение неполадок развертывания с помощью журналов stderr и stdout.</span><span class="sxs-lookup"><span data-stu-id="1bd01-110">Read stderr and stdout logs to troubleshoot any deployment issues.</span></span>
* <span data-ttu-id="1bd01-111">Сохранение переменных среды вне системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="1bd01-111">Store environment variables outside of source control.</span></span>
* <span data-ttu-id="1bd01-112">Получение доступа к переменным среды Azure из приложения.</span><span class="sxs-lookup"><span data-stu-id="1bd01-112">Access Azure environment variables from your app.</span></span>
* <span data-ttu-id="1bd01-113">Подключение к базе данных (MongoDB).</span><span class="sxs-lookup"><span data-stu-id="1bd01-113">Connect to a database (MongoDB).</span></span>

<span data-ttu-id="1bd01-114">У вас должен быть опыт работы с Sails.js.</span><span class="sxs-lookup"><span data-stu-id="1bd01-114">You should have working knowledge of Sails.js.</span></span> <span data-ttu-id="1bd01-115">Этот учебник не содержит рекомендаций по решению проблем, связанных с управлением Sails.js в целом.</span><span class="sxs-lookup"><span data-stu-id="1bd01-115">This tutorial is not intended to help you with issues related to running Sail.js in general.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="1bd01-116">Версии интерфейса командной строки для выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="1bd01-116">CLI versions to complete the task</span></span>

<span data-ttu-id="1bd01-117">Вы можете выполнить задачу, используя одну из следующих версий интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="1bd01-117">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="1bd01-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) — интерфейс командной строки для классической модели развертывания и модели развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1bd01-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span>
- <span data-ttu-id="1bd01-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) — интерфейс командной строки следующего поколения для модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1bd01-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1bd01-120">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1bd01-120">Prerequisites</span></span>
* [<span data-ttu-id="1bd01-121">Node.js</span><span class="sxs-lookup"><span data-stu-id="1bd01-121">Node.js</span></span>](https://nodejs.org/)
* [<span data-ttu-id="1bd01-122">Sails.js</span><span class="sxs-lookup"><span data-stu-id="1bd01-122">Sails.js</span></span>](http://sailsjs.org/get-started)
* [<span data-ttu-id="1bd01-123">Git.</span><span class="sxs-lookup"><span data-stu-id="1bd01-123">Git</span></span>](http://www.git-scm.com/downloads)
* [<span data-ttu-id="1bd01-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1bd01-124">Azure CLI 2.0</span></span>](/cli/azure/install-az-cli2)
* <span data-ttu-id="1bd01-125">Учетная запись Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1bd01-125">A Microsoft Azure account.</span></span> <span data-ttu-id="1bd01-126">Если у вас нет учетной записи, [подпишитесь на бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) или [активируйте преимущества для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="1bd01-126">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="1bd01-127">[Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/) возможно даже без учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="1bd01-127">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="1bd01-128">Вы можете создать приложение начального уровня и экспериментировать с ним в течение часа. Для этого вам не нужно указывать данные кредитной карты или брать на себя какие-либо обязательства.</span><span class="sxs-lookup"><span data-stu-id="1bd01-128">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a><span data-ttu-id="1bd01-129">Шаг 1. Создание и настройка приложения Sails.js в локальной среде</span><span class="sxs-lookup"><span data-stu-id="1bd01-129">Step 1: Create and configure a Sails.js app locally</span></span>
<span data-ttu-id="1bd01-130">Сначала быстро создайте приложение Sails.js по умолчанию в своей среде разработки, выполнив следующее.</span><span class="sxs-lookup"><span data-stu-id="1bd01-130">First, quickly create a default Sails.js app in your development environment by following these steps:</span></span>

1. <span data-ttu-id="1bd01-131">Откройте терминал и `CD` в рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="1bd01-131">Open the command-line terminal of your choice and `CD` to a working directory.</span></span>
2. <span data-ttu-id="1bd01-132">Создайте приложение Sails.js и запустите его.</span><span class="sxs-lookup"><span data-stu-id="1bd01-132">Create a Sails.js app and run it:</span></span>

        sails new <app_name>
        cd <app_name>
        sails lift

    <span data-ttu-id="1bd01-133">Убедитесь, что домашняя страница по умолчанию http://localhost:1377 открывается.</span><span class="sxs-lookup"><span data-stu-id="1bd01-133">Make sure you can navigate to the default home page at http://localhost:1377.</span></span>

1. <span data-ttu-id="1bd01-134">Затем включите ведение журнала для Azure.</span><span class="sxs-lookup"><span data-stu-id="1bd01-134">Next, enable logging for Azure.</span></span> <span data-ttu-id="1bd01-135">В корневом каталоге откройте файл `iisnode.yml` и добавьте в него следующие две строки:</span><span class="sxs-lookup"><span data-stu-id="1bd01-135">In your root directory, create a file called `iisnode.yml` and add the following two lines:</span></span>

        loggingEnabled: true
        logDirectory: iisnode

    <span data-ttu-id="1bd01-136">Теперь для сервера [iisnode](https://github.com/tjanczuk/iisnode), который служба приложений Azure использует для запуска приложений Node.js, включено ведение журнала.</span><span class="sxs-lookup"><span data-stu-id="1bd01-136">Logging is now enabled for the [iisnode](https://github.com/tjanczuk/iisnode) server that Azure App Service uses to run Node.js apps.</span></span> 
    <span data-ttu-id="1bd01-137">Дополнительные сведения об этом см. в статье [Отладка веб-приложения Node.js в службе приложений Azure](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="1bd01-137">For more information on how this works, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

2. <span data-ttu-id="1bd01-138">После этого настройте приложение Sails.js для использования переменных среды Azure.</span><span class="sxs-lookup"><span data-stu-id="1bd01-138">Next, configure the Sails.js app to use Azure environment variables.</span></span> <span data-ttu-id="1bd01-139">Откройте файл config/env/production.js для настройки рабочей среды и установите `port` и `hookTimeout`.</span><span class="sxs-lookup"><span data-stu-id="1bd01-139">Open config/env/production.js to configure your production environment, and set `port` and `hookTimeout`:</span></span>

        module.exports = {

            // Use process.env.port to handle web requests to the default HTTP port
            port: process.env.port,
            // Increase hooks timout to 30 seconds
            // This avoids the Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    <span data-ttu-id="1bd01-140">Сведения об этих параметрах конфигурации можно найти в [документации по Sails.js](http://sailsjs.org/documentation/reference/configuration/sails-config).</span><span class="sxs-lookup"><span data-stu-id="1bd01-140">You can find documentation for these configuration settings in the  [Sails.js Documentation](http://sailsjs.org/documentation/reference/configuration/sails-config).</span></span>

4. <span data-ttu-id="1bd01-141">Далее жестко задайте версию Node.js, которую следует использовать.</span><span class="sxs-lookup"><span data-stu-id="1bd01-141">Next, hardcode the Node.js version you want to use.</span></span> <span data-ttu-id="1bd01-142">Добавьте следующее свойство `engines` в файл package.json, чтобы задать нужную нам версию Node.js.</span><span class="sxs-lookup"><span data-stu-id="1bd01-142">In package.json, add the following `engines` property to set the Node.js version to one that we want.</span></span>

        "engines": {
            "node": "6.9.1"
        },

5. <span data-ttu-id="1bd01-143">Теперь инициализируйте репозиторий Git и сохраните свои файлы.</span><span class="sxs-lookup"><span data-stu-id="1bd01-143">Finally, initialize a Git repository and commit your files.</span></span> <span data-ttu-id="1bd01-144">В корневом каталоге приложения (где находится файл package.json) выполните следующие команды Git:</span><span class="sxs-lookup"><span data-stu-id="1bd01-144">In the application root (where package.json is), run the following Git commands:</span></span>

        git init
        git add .
        git commit -m "<your commit message>"

<span data-ttu-id="1bd01-145">Ваш код готов к развертыванию.</span><span class="sxs-lookup"><span data-stu-id="1bd01-145">Your code is ready to be deployed.</span></span> 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a><span data-ttu-id="1bd01-146">Шаг 2. Создание приложения Azure и развертывание Sails.js</span><span class="sxs-lookup"><span data-stu-id="1bd01-146">Step 2: Create an Azure app and deploy Sails.js</span></span>

<span data-ttu-id="1bd01-147">Теперь создайте ресурс службы приложений в Azure и разверните в него приложение Sails.js.</span><span class="sxs-lookup"><span data-stu-id="1bd01-147">Next, create the App Service resource in Azure and deploy your Sails.js app to it.</span></span>

1. <span data-ttu-id="1bd01-148">Войдите в Azure.</span><span class="sxs-lookup"><span data-stu-id="1bd01-148">log in to Azure like so:</span></span>

        az login

    <span data-ttu-id="1bd01-149">Следуйте указаниям, чтобы продолжить вход в браузере с помощью учетной записи Майкрософт в рамках своей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="1bd01-149">Follow the prompt to continue the login in a browser with a Microsoft account that has your Azure subscription.</span></span>

3. <span data-ttu-id="1bd01-150">Укажите пользователя развертывания для службы приложений.</span><span class="sxs-lookup"><span data-stu-id="1bd01-150">Set the deployment user for App Service.</span></span> <span data-ttu-id="1bd01-151">Вы развернете код позже с помощью этих учетных данных.</span><span class="sxs-lookup"><span data-stu-id="1bd01-151">You will deploy code using these credentials later.</span></span>
   
        az appservice web deployment user set --user-name <username> --password <password>

3. <span data-ttu-id="1bd01-152">Создайте [группу ресурсов](../azure-resource-manager/resource-group-overview.md) и присвойте ей имя.</span><span class="sxs-lookup"><span data-stu-id="1bd01-152">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with a name.</span></span> <span data-ttu-id="1bd01-153">В рамках этого руководства по Node.js вам не обязательно знать, что это такое.</span><span class="sxs-lookup"><span data-stu-id="1bd01-153">For this Node.js tutorial, you don't really need to know what it is.</span></span>

        az group create --location "<location>" --name my-sailsjs-app-group

    <span data-ttu-id="1bd01-154">Чтобы увидеть доступные значения для `<location>`, используйте команду `az appservice list-locations` интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="1bd01-154">To see what possible values you can use for `<location>`, use the `az appservice list-locations` CLI command.</span></span>

3. <span data-ttu-id="1bd01-155">Создайте [план службы приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) уровня "Бесплатный" и присвойте ему имя.</span><span class="sxs-lookup"><span data-stu-id="1bd01-155">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) with a name.</span></span> <span data-ttu-id="1bd01-156">В рамках этого руководства по Node.js вам достаточно знать, что этот план не предусматривает выставление счетов за веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="1bd01-156">For this Node.js tutorial, just know that you won't be charged for web apps in this plan.</span></span>

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. <span data-ttu-id="1bd01-157">Создайте веб-приложение с уникальным именем в `<app_name>`.</span><span class="sxs-lookup"><span data-stu-id="1bd01-157">Create a new web app with a unique name in `<app_name>`.</span></span>

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a><span data-ttu-id="1bd01-158">Шаг 3. Настройка и развертывание приложения Sails.js</span><span class="sxs-lookup"><span data-stu-id="1bd01-158">Step 3: Configure and deploy your Sails.js app</span></span>

1. <span data-ttu-id="1bd01-159">Настройте локальное развертывание Git для веб-приложения с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="1bd01-159">Configure local Git deployment for your new web app with the following command:</span></span>

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="1bd01-160">Если вы получите приблизительно следующие выходные данные JSON, это значит, что удаленный репозиторий Git настроен:</span><span class="sxs-lookup"><span data-stu-id="1bd01-160">You will get a JSON output like this, which means that the remote Git repository is configured:</span></span>

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. <span data-ttu-id="1bd01-161">Добавьте URL-адрес в JSON в качестве удаленного репозитория Git для локального репозитория (для простоты называется `azure`).</span><span class="sxs-lookup"><span data-stu-id="1bd01-161">Add the URL in the JSON as a Git remote for your local repository (called `azure` for simplicity).</span></span>

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. <span data-ttu-id="1bd01-162">Разверните образец кода в удаленном репозитории Git `azure`.</span><span class="sxs-lookup"><span data-stu-id="1bd01-162">Deploy your sample code to the `azure` Git remote.</span></span> <span data-ttu-id="1bd01-163">При появлении запроса используйте учетные данные для развертывания, настроенные ранее.</span><span class="sxs-lookup"><span data-stu-id="1bd01-163">When prompted, use the deployment credentials you configured earlier.</span></span>

        git push azure master

7. <span data-ttu-id="1bd01-164">Наконец, просто запустите приложение Azure в браузере:</span><span class="sxs-lookup"><span data-stu-id="1bd01-164">Finally, just launch your live Azure app in the browser:</span></span>

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="1bd01-165">Вы должны увидеть ту же домашнюю страницу Sails.js.</span><span class="sxs-lookup"><span data-stu-id="1bd01-165">You should now see the same Sails.js home page.</span></span>

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a><span data-ttu-id="1bd01-166">Устранение неполадок развертывания</span><span class="sxs-lookup"><span data-stu-id="1bd01-166">Troubleshoot your deployment</span></span>
<span data-ttu-id="1bd01-167">При сбое приложения Sails.js в службе приложений найдите журналы stderr, которые помогут в ее устранении.</span><span class="sxs-lookup"><span data-stu-id="1bd01-167">If your Sails.js application fails for some reason in App Service, find the stderr logs to help troubleshoot it.</span></span>
<span data-ttu-id="1bd01-168">Дополнительные сведения см. в статье [Отладка веб-приложения Node.js в службе приложений Azure](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="1bd01-168">For more information, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>
<span data-ttu-id="1bd01-169">Если приложение запущено успешно, в журнале stdout должно появиться знакомое сообщение:</span><span class="sxs-lookup"><span data-stu-id="1bd01-169">If the app has started successfully, the stdout log should show you the familiar message:</span></span>

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
    To see your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    To shut down Sails, press <CTRL> + C at any time.

<span data-ttu-id="1bd01-170">Степень детализации журналов stdout определяется в файле [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) .</span><span class="sxs-lookup"><span data-stu-id="1bd01-170">You can control granularity of the stdout logs in the [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.</span></span>

## <a name="connect-to-a-database-in-azure"></a><span data-ttu-id="1bd01-171">Подключение к базе данных в Azure</span><span class="sxs-lookup"><span data-stu-id="1bd01-171">Connect to a database in Azure</span></span>
<span data-ttu-id="1bd01-172">Чтобы подключиться к базе данных Azure, создайте в Azure базу данных выбранного типа (база данных SQL Azure, MySQL, MongoDB, кэш Redis для Azure и т. д.) и используйте соответствующий [адаптер хранилища данных](https://github.com/balderdashy/sails#compatibility) для подключения к ней.</span><span class="sxs-lookup"><span data-stu-id="1bd01-172">To connect to a database in Azure, you create the database of your choice in Azure, such as Azure SQL Database, MySQL, MongoDB, Azure (Redis) Cache, etc., and use the corresponding [datastore adapter](https://github.com/balderdashy/sails#compatibility) to connect to it.</span></span> <span data-ttu-id="1bd01-173">Действия, описанные в этом разделе, помогут вам подключиться к MongoDB с помощью базы данных [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md), которая поддерживает подключения клиентов MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1bd01-173">The steps in this section show you how to connect to MongoDB by using an [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, which can support MongoDB client connections.</span></span>

1. <span data-ttu-id="1bd01-174">[Создайте учетную запись Cosmos DB с поддержкой протокола MongoDB](../documentdb/documentdb-create-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="1bd01-174">[Create a Cosmos DB account with MongoDB protocol support](../documentdb/documentdb-create-mongodb-account.md).</span></span>
2. <span data-ttu-id="1bd01-175">[Создайте коллекцию и базу данных Cosmos DB](../documentdb/documentdb-create-collection.md).</span><span class="sxs-lookup"><span data-stu-id="1bd01-175">[Create a Cosmos DB collection and database](../documentdb/documentdb-create-collection.md).</span></span> <span data-ttu-id="1bd01-176">Имя коллекции не имеет значения, но при подключении из Sails.js необходимо знать имя базы данных.</span><span class="sxs-lookup"><span data-stu-id="1bd01-176">The name of the collection doesn't matter, but you need the name of the database when you connect from Sails.js.</span></span>
3. <span data-ttu-id="1bd01-177">[Найдите сведения о подключении к базе данных Cosmos DB](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="1bd01-177">[Find the connection information for your Cosmos DB database](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span></span>
2. <span data-ttu-id="1bd01-178">В терминале командной строки установите адаптер MongoDB:</span><span class="sxs-lookup"><span data-stu-id="1bd01-178">From your command-line terminal, install the MongoDB adapter:</span></span>

        npm install sails-mongo --save

3. <span data-ttu-id="1bd01-179">Откройте файл config/connections.js и добавьте в список следующий объект соединения:</span><span class="sxs-lookup"><span data-stu-id="1bd01-179">Open config/connections.js and add the following connection object to the list:</span></span>

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
    > <span data-ttu-id="1bd01-180">Параметр `ssl: true` важен, так как он [требуется для Cosmos DB](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="1bd01-180">The `ssl: true` option is important because [Cosmos DB requires it](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 
    >
    >

4. <span data-ttu-id="1bd01-181">Каждую переменную среды (`process.env.*`) необходимо задать в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="1bd01-181">For each environment variable (`process.env.*`), you need to set it in App Service.</span></span> <span data-ttu-id="1bd01-182">Для этого выполните следующие команды из терминала.</span><span class="sxs-lookup"><span data-stu-id="1bd01-182">To do this, run the following commands from your terminal.</span></span> <span data-ttu-id="1bd01-183">Используйте сведения о подключении Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1bd01-183">Use the connection information for your Cosmos DB.</span></span>

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="1bd01-184">Чтобы предотвратить доступ системы управления версиями (Git) к конфиденциальным данным, в код приложения Azure необходимо добавить собственные параметры.</span><span class="sxs-lookup"><span data-stu-id="1bd01-184">Putting your settings in Azure app settings keeps sensitive data out of your source control (Git).</span></span> <span data-ttu-id="1bd01-185">Далее необходимо настроить такие же данные о подключении для среды разработки.</span><span class="sxs-lookup"><span data-stu-id="1bd01-185">Next, you will configure your development environment to use the same connection information.</span></span>
5. <span data-ttu-id="1bd01-186">Откройте файл config/local.js и добавьте следующий объект соединения:</span><span class="sxs-lookup"><span data-stu-id="1bd01-186">Open config/local.js and add the following connections object:</span></span>

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    <span data-ttu-id="1bd01-187">Эта конфигурация позволяет переопределить параметры локальной среды в файле config/connections.js.</span><span class="sxs-lookup"><span data-stu-id="1bd01-187">This configuration overrides the settings in your config/connections.js file for the local environment.</span></span> <span data-ttu-id="1bd01-188">Этот файл входит в список исключений, определенный в GITIGNORE-файле по умолчанию для проекта, поэтому его нельзя сохранить в репозитории Git.</span><span class="sxs-lookup"><span data-stu-id="1bd01-188">This file is excluded by the default .gitignore in your project, so it will not be stored in Git.</span></span> <span data-ttu-id="1bd01-189">Теперь подключаться к базе данных Cosmos DB (MongoDB) можно как из веб-приложения Azure, так и из локальной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="1bd01-189">Now, you are able to connect to your Cosmos DB (MongoDB) database both from your Azure web app and from your local development environment.</span></span>
6. <span data-ttu-id="1bd01-190">Чтобы настроить рабочую среду, откройте файл config/env/production.js и добавьте в него следующий объект `models` .</span><span class="sxs-lookup"><span data-stu-id="1bd01-190">Open config/env/production.js to configure your production environment, and add the following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. <span data-ttu-id="1bd01-191">Чтобы настроить среду разработки, откройте файл config/env/development.js и добавьте в него следующий объект `models`.</span><span class="sxs-lookup"><span data-stu-id="1bd01-191">Open config/env/development.js to configure your development environment, and add the following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    <span data-ttu-id="1bd01-192">Объект `migrate: 'alter'` позволяет использовать функции миграции, чтобы легко создавать и обновлять коллекции и таблицы в базе данных.</span><span class="sxs-lookup"><span data-stu-id="1bd01-192">`migrate: 'alter'` lets you use database migration features to create and update database collections or tables easily.</span></span> <span data-ttu-id="1bd01-193">Так как приложение Sails.js не поддерживает параметр `migrate: 'alter'`, в (рабочей) среде Azure используется параметр `migrate: 'safe'` (дополнительные сведения см. в [документации по Sails.js](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span><span class="sxs-lookup"><span data-stu-id="1bd01-193">However, `migrate: 'safe'` is used for your Azure (production) environment because Sails.js does not allow you to use `migrate: 'alter'` in a production environment (see [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span></span>
8. <span data-ttu-id="1bd01-194">Чтобы создать базу данных с возможностями миграции Sails.js, в терминале [создайте](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) [проектный API](http://sailsjs.org/documentation/concepts/blueprints) для Sails.js, следуя обычной процедуре, а затем выполните команду `sails lift`.</span><span class="sxs-lookup"><span data-stu-id="1bd01-194">From the terminal, [generate](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) a Sails.js [blueprint API](http://sailsjs.org/documentation/concepts/blueprints) like you normally would, then run `sails lift` to create the database with Sails.js database migration.</span></span> <span data-ttu-id="1bd01-195">Например:</span><span class="sxs-lookup"><span data-stu-id="1bd01-195">For example:</span></span>

         sails generate api mywidget
         sails lift

    <span data-ttu-id="1bd01-196">После выполнения этой команды создается пустая модель `mywidget` , но с ее помощью можно подтвердить наличие связи с базой данных.</span><span class="sxs-lookup"><span data-stu-id="1bd01-196">The `mywidget` model generated by this command is empty, but we can use it to show that we have database connectivity.</span></span>
    <span data-ttu-id="1bd01-197">При выполнении команды `sails lift` для моделей, используемых приложением, создаются отсутствующие коллекции и таблицы.</span><span class="sxs-lookup"><span data-stu-id="1bd01-197">When you run `sails lift`, it creates the missing collections and tables for the models your app uses.</span></span>
9. <span data-ttu-id="1bd01-198">Обратитесь к проектному API, только что созданному в браузере.</span><span class="sxs-lookup"><span data-stu-id="1bd01-198">Access the blueprint API you just created in the browser.</span></span> <span data-ttu-id="1bd01-199">Например:</span><span class="sxs-lookup"><span data-stu-id="1bd01-199">For example:</span></span>

        http://localhost:1337/mywidget/create

    <span data-ttu-id="1bd01-200">API должен вернуть созданный объект в окно браузера, что будет означать, что коллекция успешно создана.</span><span class="sxs-lookup"><span data-stu-id="1bd01-200">The API should return the created entry back to you in the browser window, which means that your collection is created  successfully.</span></span>

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. <span data-ttu-id="1bd01-201">Теперь отправьте изменения в Azure и перейдите к своему приложению, чтобы убедиться, что оно работает.</span><span class="sxs-lookup"><span data-stu-id="1bd01-201">Now, push your changes to Azure, and browse to your app to make sure it still works.</span></span>

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. <span data-ttu-id="1bd01-202">Обратитесь к проектному API веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="1bd01-202">Access the blueprint API of your Azure web app.</span></span> <span data-ttu-id="1bd01-203">Например:</span><span class="sxs-lookup"><span data-stu-id="1bd01-203">For example:</span></span>

         http://<appname>.azurewebsites.net/mywidget/create

     <span data-ttu-id="1bd01-204">Если API возвращает другую новую запись, это значит, что между веб-приложением Azure и базой данных Cosmos DB (MongoDB) осуществляется взаимодействие.</span><span class="sxs-lookup"><span data-stu-id="1bd01-204">If the API returns another new entry, then your Azure web app is talking to your Cosmos DB (MongoDB) database.</span></span>

## <a name="more-resources"></a><span data-ttu-id="1bd01-205">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1bd01-205">More resources</span></span>
* [<span data-ttu-id="1bd01-206">Приступая к работе с веб-приложениями Node.js в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="1bd01-206">Get started with Node.js web apps in Azure App Service</span></span>](app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="1bd01-207">Использование модулей Node.js с приложениями Azure</span><span class="sxs-lookup"><span data-stu-id="1bd01-207">Using Node.js Modules with Azure applications</span></span>](../nodejs-use-node-modules-azure-apps.md)
