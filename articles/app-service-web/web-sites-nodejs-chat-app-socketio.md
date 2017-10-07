---
title: "aaaCreate приложения Node.js разговора с Socket.IO в службе приложений Azure"
description: "В этом учебнике рассматривается использование Socket.io в веб-приложениях Node.js, размещенных в Azure."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c4c4af36-3ecf-4619-b586-ca90d53ce35b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 3bd7867ccc297dc0a21c7a00cc9db06358877f5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a><span data-ttu-id="7dca4-103">Создание приложения для разговоров на Node.js с использованием Socket.IO в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="7dca4-103">Create a Node.js chat application with Socket.IO in Azure App Service</span></span>
<span data-ttu-id="7dca4-104">Socket.IO обеспечивает связь в режиме реального времени между сервером Node.js и клиентами с помощью WebSockets.</span><span class="sxs-lookup"><span data-stu-id="7dca4-104">Socket.IO provides real-time communication between your node.js server and clients using WebSockets.</span></span> <span data-ttu-id="7dca4-105">Оно также поддерживает резервной tooother транспорты (например, длинные опроса), работающие с старых браузерах.</span><span class="sxs-lookup"><span data-stu-id="7dca4-105">It also supports fallback tooother transports (such as long polling) that work with older browsers.</span></span> <span data-ttu-id="7dca4-106">Этот учебник пошаговыми руководствами для размещения приложения на основе Socket.IO разговора как веб-приложение Azure и показать, как tooscale hello приложения с помощью [кэш Azure Redis].</span><span class="sxs-lookup"><span data-stu-id="7dca4-106">This tutorial will walk you through hosting a Socket.IO based chat application as an Azure web app, and show you how tooscale hello application using [Azure Redis Cache].</span></span> <span data-ttu-id="7dca4-107">Дополнительные сведения о Socket.IO см. на веб-сайте <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="7dca4-107">For more information on Socket.IO, see <http://socket.io/>.</span></span>

> [!NOTE]
> <span data-ttu-id="7dca4-108">Hello процедуры в этой задаче применяются слишком[веб-приложений служб приложения]; для облачных служб. в разделе [построения приложения чат Node.js с Socket.IO на облачную службу Azure].</span><span class="sxs-lookup"><span data-stu-id="7dca4-108">hello procedures in this task apply too[App Service Web Apps]; for Cloud Services, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>
> 
> 

## <a name="download-hello-chat-example"></a><span data-ttu-id="7dca4-109">Загрузить пример hello чата</span><span class="sxs-lookup"><span data-stu-id="7dca4-109">Download hello chat example</span></span>
<span data-ttu-id="7dca4-110">Для этого проекта, мы будем использовать пример hello разговора с hello [репозитории Socket.IO GitHub].</span><span class="sxs-lookup"><span data-stu-id="7dca4-110">For this project, we will use hello chat example from hello [Socket.IO GitHub repository].</span></span> <span data-ttu-id="7dca4-111">Выполните следующий пример hello toodownload действия hello и добавьте его toohello проекта, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="7dca4-111">Perform hello following steps toodownload hello example and add it toohello project you previously created.</span></span>

1. <span data-ttu-id="7dca4-112">Загрузить [ZIP-файл или GZ архивные версии] hello Socket.IO проекта (версия 1.3.5 использовалась для этого документа)</span><span class="sxs-lookup"><span data-stu-id="7dca4-112">Download a [ZIP or GZ archived release] of hello Socket.IO project (version 1.3.5 was used for this document)</span></span>
2. <span data-ttu-id="7dca4-113">Извлеките hello и архивные копии hello **примеры\\чата** tooa новый каталог.</span><span class="sxs-lookup"><span data-stu-id="7dca4-113">Extract hello archive and copy hello **examples\\chat** directory tooa new location.</span></span> <span data-ttu-id="7dca4-114">Например, в **\\node\\chat**.</span><span class="sxs-lookup"><span data-stu-id="7dca4-114">For example, **\\node\\chat**.</span></span>

## <a name="modify-appjs-and-install-modules"></a><span data-ttu-id="7dca4-115">Изменение app.js и установка модулей</span><span class="sxs-lookup"><span data-stu-id="7dca4-115">Modify app.js and install modules</span></span>
1. <span data-ttu-id="7dca4-116">Переименование hello **index.js** файла слишком**в файле app.js**.</span><span class="sxs-lookup"><span data-stu-id="7dca4-116">Rename hello **index.js** file too**app.js**.</span></span> <span data-ttu-id="7dca4-117">Это позволяет Azure toodetect, что это приложение Node.js.</span><span class="sxs-lookup"><span data-stu-id="7dca4-117">This allows Azure toodetect that this is a Node.js application.</span></span>
2. <span data-ttu-id="7dca4-118">Откройте hello **в файле app.js** файл в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="7dca4-118">Open hello **app.js** file in a text editor.</span></span> <span data-ttu-id="7dca4-119">Изменение hello строке, содержащей `var io = require('../..')(server);` как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="7dca4-119">Change hello line containing `var io = require('../..')(server);` as shown below:</span></span>
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. <span data-ttu-id="7dca4-120">Откройте hello **package.json** и добавьте toosocket.io ссылку в разделе файла `dependencies`, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="7dca4-120">Open hello **package.json** file and add a reference toosocket.io under `dependencies`, as shown below:</span></span>
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. <span data-ttu-id="7dca4-121">Из командной строки hello, изменить toohello  **\\узел\\чата** каталог и использовать npm tooinstall hello модулями, необходимыми этим приложением:</span><span class="sxs-lookup"><span data-stu-id="7dca4-121">From hello command-line, change toohello **\\node\\chat** directory and use npm tooinstall hello modules required by this application:</span></span>
   
        npm install
   
    <span data-ttu-id="7dca4-122">Hello модули будут установлены в подпапку **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="7dca4-122">This will install hello modules into a subfolder named **node_modules**.</span></span>

## <a name="create-an-azure-web-app"></a><span data-ttu-id="7dca4-123">Создание веб-приложения Azure</span><span class="sxs-lookup"><span data-stu-id="7dca4-123">Create an Azure Web App</span></span>
<span data-ttu-id="7dca4-124">Выполните эти шаги toocreate Azure веб-приложение, включить публикацию Git и затем включите поддержка WebSocket для веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7dca4-124">Follow these steps toocreate an Azure web app, enable Git publishing, and then enable WebSocket support for hello web app.</span></span>

> [!NOTE]
> <span data-ttu-id="7dca4-125">toocomplete этого учебника необходима учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="7dca4-125">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="7dca4-126">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="7dca4-126">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="7dca4-127">Дополнительные сведения см. в разделе <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Бесплатная пробная версия Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="7dca4-127">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

1. <span data-ttu-id="7dca4-128">Установка hello Azure командной строки (CLI Azure) и подключение tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="7dca4-128">Install hello Azure Command-Line Interface (Azure CLI) and connect tooyour Azure subscription.</span></span> <span data-ttu-id="7dca4-129">В разделе [Установка и настройка hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="7dca4-129">See [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="7dca4-130">Если это ваш первый подготовку в репозитории в Azure, необходимо toocreate учетные данные для входа.</span><span class="sxs-lookup"><span data-stu-id="7dca4-130">If this is your first time setting up a repository in Azure, you need toocreate login credentials.</span></span> <span data-ttu-id="7dca4-131">Введите следующую команду hello hello Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="7dca4-131">From hello Azure CLI, enter hello following command:</span></span>
   
        azure site deployment user set [username] [password]
3. <span data-ttu-id="7dca4-132">Изменить toohello  **\\node\chat** каталога и используйте следующие hello команд toocreate новый Azure веб-приложения и локального репозитория Git.</span><span class="sxs-lookup"><span data-stu-id="7dca4-132">Change toohello **\\node\chat** directory and use hello following command toocreate a new Azure web app and a local Git repository.</span></span> <span data-ttu-id="7dca4-133">Эта команда также создает удаленный Git с именем azure.</span><span class="sxs-lookup"><span data-stu-id="7dca4-133">This command also creates a Git remote named 'azure'.</span></span>
   
        azure site create mysitename --git
   
    <span data-ttu-id="7dca4-134">Замените mysitename уникальным именем созданного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="7dca4-134">You must replace 'mysitename' with a unique name for your web app.</span></span>
4. <span data-ttu-id="7dca4-135">Зафиксировать hello существующие файлы toohello локального репозитория с помощью hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="7dca4-135">Commit hello existing files toohello local repository by using hello following commands:</span></span>
   
        git add .
        git commit -m "Initial commit"
5. <span data-ttu-id="7dca4-136">Принудительная toohello веб-приложениях Azure hello файлы репозитория с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7dca4-136">Push hello files toohello Azure Web Apps repository with hello following command:</span></span>
   
        git push azure master
   
    <span data-ttu-id="7dca4-137">При появлении запроса введите свои учетные данные из шага 2.</span><span class="sxs-lookup"><span data-stu-id="7dca4-137">When prompted, enter your credentials from step 2.</span></span> <span data-ttu-id="7dca4-138">Вы получите сообщения о состоянии, как модули импортируются на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="7dca4-138">You will receive status messages as modules are imported on hello server.</span></span> <span data-ttu-id="7dca4-139">После завершения этого процесса будет размещаться приложение hello в Azure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="7dca4-139">Once this process has completed, hello application will be hosted on your Azure web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7dca4-140">Во время установки модуля могут появиться ошибки, "hello... импортированный проект не найден".</span><span class="sxs-lookup"><span data-stu-id="7dca4-140">During module installation, you may notice errors that 'hello imported project ... was not found'.</span></span> <span data-ttu-id="7dca4-141">Эти сообщения можно спокойно проигнорировать.</span><span class="sxs-lookup"><span data-stu-id="7dca4-141">These can safely be ignored.</span></span>
   > 
   > 
6. <span data-ttu-id="7dca4-142">В Socket.IO используются сокеты WebSockets, которые по умолчанию не включены в Azure.</span><span class="sxs-lookup"><span data-stu-id="7dca4-142">Socket.IO uses WebSockets, which are not enabled by default on Azure.</span></span> <span data-ttu-id="7dca4-143">tooenable веб-сокеты hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7dca4-143">tooenable web sockets, use hello following command:</span></span>
   
        azure site set -w
   
    <span data-ttu-id="7dca4-144">Если будет предложено, введите имя hello hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="7dca4-144">If prompted, enter hello name of hello web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7dca4-145">Здравствуйте, «azure site set -w» работают только с версии 0.7.4 или более поздней версии из hello интерфейса командной строки Azure будет команды.</span><span class="sxs-lookup"><span data-stu-id="7dca4-145">hello 'azure site set -w' command will work only with version 0.7.4 or higher of hello Azure Command-Line Interface.</span></span> <span data-ttu-id="7dca4-146">Также можно включить с помощью hello поддержка WebSocket [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7dca4-146">You can also enable WebSocket support using hello [Azure Portal](https://portal.azure.com).</span></span>
   > 
   > <span data-ttu-id="7dca4-147">с помощью WebSockets tooenable hello портал Azure, щелкните веб-приложение hello из колонки веб-приложения hello, **все параметры** > **параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="7dca4-147">tooenable WebSockets using hello Azure Portal, click hello web app from hello Web Apps blade, click **All settings** > **Application settings**.</span></span> <span data-ttu-id="7dca4-148">В разделе **Веб-сокеты** щелкните **Включить**.</span><span class="sxs-lookup"><span data-stu-id="7dca4-148">Under **Web Sockets**, click **On**.</span></span> <span data-ttu-id="7dca4-149">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7dca4-149">Then click **Save**.</span></span>
   > 
   > 
7. <span data-ttu-id="7dca4-150">tooview hello веб-приложения на следующий hello Azure, используйте команду toolaunch веб-браузере и перейдите toohello размещенного веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="7dca4-150">tooview hello web app on Azure, use hello following command toolaunch your web browser and navigate toohello hosted web app:</span></span>
   
        azure site browse

<span data-ttu-id="7dca4-151">Теперь ваше приложение работает на платформе Azure и может передавать сообщения разговора между различными клиентами с использованием Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="7dca4-151">Your app is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

## <a name="scale-out"></a><span data-ttu-id="7dca4-152">Масштабирование</span><span class="sxs-lookup"><span data-stu-id="7dca4-152">Scale out</span></span>
<span data-ttu-id="7dca4-153">Socket.IO приложения можно расширить с помощью **адаптер** toodistribute сообщений и событий между несколькими экземплярами приложения.</span><span class="sxs-lookup"><span data-stu-id="7dca4-153">Socket.IO applications can be scaled out by using an **adapter** toodistribute messages and events between multiple application instances.</span></span> <span data-ttu-id="7dca4-154">При наличии нескольких адаптеров, hello [socket.io redis] адаптер можно легко использовать с помощью функции hello кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="7dca4-154">While there are several adapters available, hello [socket.io-redis] adapter can be easily used with hello Azure Redis Cache feature.</span></span>

> [!NOTE]
> <span data-ttu-id="7dca4-155">Дополнительным требованием к масштабированию решений Socket.IO является поддержка прикрепленных сеансов.</span><span class="sxs-lookup"><span data-stu-id="7dca4-155">An additional requirement for scaling out a Socket.IO solution is support for sticky sessions.</span></span> <span data-ttu-id="7dca4-156">Прикрепленные сеансы включены для веб-приложений Azure по умолчанию через маршрутизацию запросов Azure.</span><span class="sxs-lookup"><span data-stu-id="7dca4-156">Sticky sessions are enabled by default for Azure Web Apps through Azure Request Routing.</span></span> <span data-ttu-id="7dca4-157">Дополнительные сведения см. в разделе [Сходство экземпляров на веб-сайтах Azure].</span><span class="sxs-lookup"><span data-stu-id="7dca4-157">For more information, see [Instance Affinity in Azure Web Sites].</span></span>
> 
> 

### <a name="create-a-redis-cache"></a><span data-ttu-id="7dca4-158">Создание кэша Redis</span><span class="sxs-lookup"><span data-stu-id="7dca4-158">Create a Redis cache</span></span>
<span data-ttu-id="7dca4-159">Выполните действия hello в [создание кэша в кэше Redis для Azure] toocreate нового кэша.</span><span class="sxs-lookup"><span data-stu-id="7dca4-159">Perform hello steps in [Create a cache in Azure Redis Cache] toocreate a new cache.</span></span>

> [!NOTE]
> <span data-ttu-id="7dca4-160">Сохранить hello **имя узла** и **первичный ключ** для кэша, как их потребуется в hello дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="7dca4-160">Save hello **Host name** and **Primary key** for your cache, as these will be needed in hello next steps.</span></span>
> 
> 

### <a name="add-hello-redis-and-socketio-redis-modules"></a><span data-ttu-id="7dca4-161">Добавление hello redis и модули socket.io redis</span><span class="sxs-lookup"><span data-stu-id="7dca4-161">Add hello redis and socket.io-redis modules</span></span>
1. <span data-ttu-id="7dca4-162">Из командной строки, измените toohello  **\\узел\\чата** hello каталог и использовать следующую команду.</span><span class="sxs-lookup"><span data-stu-id="7dca4-162">From a command-line, change toohello **\\node\\chat** directory and use hello following command.</span></span>
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > <span data-ttu-id="7dca4-163">Hello версии, указанные в этой команде являются версии hello, используемых при тестировании в этой статье.</span><span class="sxs-lookup"><span data-stu-id="7dca4-163">hello versions specified in this command are hello versions used when testing this article.</span></span>
   > 
   > 
2. <span data-ttu-id="7dca4-164">Изменение hello **в файле app.js** файл tooadd hello следующие строки в том, сразу после`var io = require('socket.io')(server);`</span><span class="sxs-lookup"><span data-stu-id="7dca4-164">Modify hello **app.js** file tooadd hello following lines immediately after `var io = require('socket.io')(server);`</span></span>
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    <span data-ttu-id="7dca4-165">Замените **redishostname** и **rediskey** с именем узла hello и ключ для кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="7dca4-165">Replace **redishostname** and **rediskey** with hello host name and key for your Redis cache.</span></span>
   
    <span data-ttu-id="7dca4-166">Будет создан публикации и подписки клиента toohello кэш Redis, созданный ранее.</span><span class="sxs-lookup"><span data-stu-id="7dca4-166">This will create a publish and subscribe client toohello Redis cache created previously.</span></span> <span data-ttu-id="7dca4-167">Клиенты Hello затем используются с tooconfigure адаптера hello кэш Redis hello toouse Socket.IO для передачи сообщений и событий между экземплярами приложения</span><span class="sxs-lookup"><span data-stu-id="7dca4-167">hello clients are then used with hello adapter tooconfigure Socket.IO toouse hello Redis cache for passing messages and events between instances of your application</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7dca4-168">При hello **socket.io redis** адаптер может напрямую взаимодействовать tooRedis, hello текущая версия не поддерживает hello проверки подлинности, необходимые для кэша Azure Redis.</span><span class="sxs-lookup"><span data-stu-id="7dca4-168">While hello **socket.io-redis** adapter can communicate directly tooRedis, hello current version does not support hello authentication required by Azure Redis cache.</span></span> <span data-ttu-id="7dca4-169">Поэтому hello начального подключения создается с помощью hello **redis** модуля, затем клиент hello передается toohello **socket.io redis** адаптера.</span><span class="sxs-lookup"><span data-stu-id="7dca4-169">So hello initial connection is created using hello **redis** module, then hello client is passed toohello **socket.io-redis** adapter.</span></span>
   > 
   > <span data-ttu-id="7dca4-170">Хотя кэш Azure Redis поддерживает безопасные соединения через порт 6380, hello модули, используемые в этом примере не поддерживают безопасные соединения по состоянию на 7/14/2014.</span><span class="sxs-lookup"><span data-stu-id="7dca4-170">While Azure Redis Cache supports secure connections using port 6380, hello modules used in this example do not support secure connections as of 7/14/2014.</span></span> <span data-ttu-id="7dca4-171">Hello выше код использует по умолчанию hello, незащищенного порта 6379.</span><span class="sxs-lookup"><span data-stu-id="7dca4-171">hello above code uses hello default, unsecure port of 6379.</span></span>
   > 
   > 
3. <span data-ttu-id="7dca4-172">Hello сохранить изменения **в файле app.js**</span><span class="sxs-lookup"><span data-stu-id="7dca4-172">Save hello modified **app.js**</span></span>

### <a name="commit-changes-and-redeploy"></a><span data-ttu-id="7dca4-173">Подтверждение изменений и повторное развертывание</span><span class="sxs-lookup"><span data-stu-id="7dca4-173">Commit changes and redeploy</span></span>
<span data-ttu-id="7dca4-174">Из командной строки в hello hello  **\\узел\\чата** каталогов, используйте следующие команды toocommit отличия hello и повторного развертывания приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7dca4-174">From hello command-line in hello **\\node\\chat** directory, use hello following commands toocommit changes and redeploy hello application.</span></span>

    git add .
    git commit -m "implementing scale out"
    git push azure master

<span data-ttu-id="7dca4-175">После изменения hello отправлены toohello сервера, можно масштабировать веб-узла по нескольким экземплярам, используя следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="7dca4-175">Once hello changes have been pushed toohello server, you can scale your site across multiple instances by using hello following command.</span></span>

    azure site scale instances --instances #

<span data-ttu-id="7dca4-176">Где  **#**  hello число экземпляров toocreate.</span><span class="sxs-lookup"><span data-stu-id="7dca4-176">Where **#** is hello number of instances toocreate.</span></span>

<span data-ttu-id="7dca4-177">Tooyour веб-приложения можно подключиться из нескольких браузеров или компьютеры tooverify сообщений, отправленных правильно tooall клиентов.</span><span class="sxs-lookup"><span data-stu-id="7dca4-177">You can connect tooyour web app from multiple browsers or computers tooverify that messages are correctly sent tooall clients.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7dca4-178">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="7dca4-178">Troubleshooting</span></span>
### <a name="connection-limits"></a><span data-ttu-id="7dca4-179">Ограничения на подключения</span><span class="sxs-lookup"><span data-stu-id="7dca4-179">Connection limits</span></span>
<span data-ttu-id="7dca4-180">Azure веб-приложений можно найти в несколько конфигураций, которые определяют веб-сайт доступен tooyour ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="7dca4-180">Azure Web Apps is available in multiple SKUs, which determine hello resources available tooyour site.</span></span> <span data-ttu-id="7dca4-181">Сюда входят hello число разрешенных подключений WebSocket.</span><span class="sxs-lookup"><span data-stu-id="7dca4-181">This includes hello number of allowed WebSocket connections.</span></span> <span data-ttu-id="7dca4-182">Дополнительные сведения см. в разделе hello [цены приложения Web].</span><span class="sxs-lookup"><span data-stu-id="7dca4-182">For more information, see hello [Web Apps Pricing page].</span></span>

### <a name="messages-arent-being-sent-using-websockets"></a><span data-ttu-id="7dca4-183">Не отправляются сообщения через WebSockets</span><span class="sxs-lookup"><span data-stu-id="7dca4-183">Messages aren't being sent using WebSockets</span></span>
<span data-ttu-id="7dca4-184">Если клиентскими браузерами сохранить возврата toolong опроса вместо WebSockets, возможно из-за одного из следующих hello.</span><span class="sxs-lookup"><span data-stu-id="7dca4-184">If client browsers keep falling back toolong polling instead of using WebSockets, it may be because of one of hello following.</span></span>

* <span data-ttu-id="7dca4-185">**Попробуйте ограничить hello транспорта toojust WebSockets**</span><span class="sxs-lookup"><span data-stu-id="7dca4-185">**Try limiting hello transport toojust WebSockets**</span></span>
  
    <span data-ttu-id="7dca4-186">Socket.IO toouse WebSockets как обмена сообщениями транспортного hello, клиента и сервера hello должен поддерживать в WebSockets.</span><span class="sxs-lookup"><span data-stu-id="7dca4-186">In order for Socket.IO toouse WebSockets as hello messaging transport, both hello server and client must support WebSockets.</span></span> <span data-ttu-id="7dca4-187">Если один или hello другие — нет, Socket.IO согласует другого транспорта, такого как долго опрашивающего.</span><span class="sxs-lookup"><span data-stu-id="7dca4-187">If one or hello other does not, Socket.IO will negotiate another transport, such as long polling.</span></span> <span data-ttu-id="7dca4-188">список по умолчанию Hello транспортов, используемые Socket.IO ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span><span class="sxs-lookup"><span data-stu-id="7dca4-188">hello default list of transports used by Socket.IO is ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span></span> <span data-ttu-id="7dca4-189">Для принудительного использования tooonly WebSockets, добавив следующий код toohello hello **в файле app.js** файла после hello строке, содержащей `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="7dca4-189">You can force it tooonly use WebSockets by adding hello following code toohello **app.js** file, after hello line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > <span data-ttu-id="7dca4-190">Следует Заметьте, что старых браузерах, которые не поддерживают WebSockets не может tooconnect toohello сайта во время hello над кодом активной, как она ограничивает только tooWebSockets связи.</span><span class="sxs-lookup"><span data-stu-id="7dca4-190">Note that older browsers that do not support WebSockets will not be able tooconnect toohello site while hello above code is active, as it restricts communication tooWebSockets only.</span></span>
  > 
  > 
* <span data-ttu-id="7dca4-191">**Использование SSL**</span><span class="sxs-lookup"><span data-stu-id="7dca4-191">**Use SSL**</span></span>
  
    <span data-ttu-id="7dca4-192">WebSockets зависит от некоторых меньшее используется заголовки HTTP, такие как hello **обновление** заголовок.</span><span class="sxs-lookup"><span data-stu-id="7dca4-192">WebSockets relies on some lesser used HTTP headers, such as hello **Upgrade** header.</span></span> <span data-ttu-id="7dca4-193">Некоторые промежуточные сетевые устройства, например прокси-серверы, могут удалять эти заголовки.</span><span class="sxs-lookup"><span data-stu-id="7dca4-193">Some intermediate network devices, such as web proxies, may remove these headers.</span></span> <span data-ttu-id="7dca4-194">tooavoid эту проблему, можно установить соединение WebSocket hello по протоколу SSL.</span><span class="sxs-lookup"><span data-stu-id="7dca4-194">tooavoid this problem, you can establish hello WebSocket connection over SSL.</span></span>
  
    <span data-ttu-id="7dca4-195">Простой способ tooaccomplish tooconfigure Socket.IO это слишком`match origin protocol`.</span><span class="sxs-lookup"><span data-stu-id="7dca4-195">An easy way tooaccomplish this is tooconfigure Socket.IO too`match origin protocol`.</span></span> <span data-ttu-id="7dca4-196">Это указывает, что запрос таким же, как hello, рассчитанные на HTTP или HTTPS для веб-страницы приветствия связи hello Socket.IO toosecure WebSockets.</span><span class="sxs-lookup"><span data-stu-id="7dca4-196">This instructs Socket.IO toosecure WebSockets communication hello same as hello originating HTTP/HTTPS request for hello web page.</span></span> <span data-ttu-id="7dca4-197">Если браузер использует toovisit HTTPS URL-адрес веб-сайта, последующие соединения WebSocket через Socket.IO будут защищаться по протоколу SSL.</span><span class="sxs-lookup"><span data-stu-id="7dca4-197">If a browser uses an HTTPS URL toovisit your website, subsequent WebSocket communications through Socket.IO will be secured over SSL.</span></span>
  
    <span data-ttu-id="7dca4-198">toomodify этот пример tooenable этой конфигурации, добавьте следующий код toohello hello **в файле app.js** файла после hello строке, содержащей `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="7dca4-198">toomodify this example tooenable this configuration, add hello following code toohello **app.js** file after hello line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* <span data-ttu-id="7dca4-199">**Проверка настроек web.config**</span><span class="sxs-lookup"><span data-stu-id="7dca4-199">**Verify web.config settings**</span></span>
  
    <span data-ttu-id="7dca4-200">Использовать веб-приложениях Azure, размещающие приложения Node.js hello **web.config** tooroute файл входящих запросов приложений Node.js toohello.</span><span class="sxs-lookup"><span data-stu-id="7dca4-200">Azure web apps that host Node.js applications use hello **web.config** file tooroute incoming requests toohello Node.js application.</span></span> <span data-ttu-id="7dca4-201">WebSockets toofunction правильно с приложениями, Node.js, hello **web.config** должен содержать следующие записи hello.</span><span class="sxs-lookup"><span data-stu-id="7dca4-201">For WebSockets toofunction correctly with Node.js applications, hello **web.config** must contain hello following entry.</span></span>
  
        <webSocket enabled="false"/>
  
    <span data-ttu-id="7dca4-202">Это приведет к отключению hello модуль WebSocket служб IIS, в котором включает собственную реализацию конфликты с Node.js определенных модулей WebSocket, такие как Socket.IO и WebSockets.</span><span class="sxs-lookup"><span data-stu-id="7dca4-202">This disables hello IIS WebSockets module, which includes its own implementation of WebSockets and conflicts with Node.js specific WebSocket modules such as Socket.IO.</span></span> <span data-ttu-id="7dca4-203">Если эта строка отсутствует или задано слишком`true`, возможно, причина hello, транспорт WebSocket hello не работает для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="7dca4-203">If this line is not present, or is set too`true`, this may be hello reason that hello WebSocket transport is not working for your application.</span></span>
  
    <span data-ttu-id="7dca4-204">Обычно приложения Node.js не включают файл **web.config** , поэтому веб-сайты Azure автоматически будут создавать его для приложений Node.js при их развертывании.</span><span class="sxs-lookup"><span data-stu-id="7dca4-204">Normally, Node.js applications do not include a **web.config** file, so Azure Websites will automatically generate one for Node.js applications when they are deployed.</span></span> <span data-ttu-id="7dca4-205">Так как этот файл автоматически создается на сервере hello, необходимо использовать hello FTP или FTPS URL-адрес для вашего веб-сайта tooview этот файл.</span><span class="sxs-lookup"><span data-stu-id="7dca4-205">Since this file is automatically generated on hello server, you must use hello FTP or FTPS URL for your website tooview this file.</span></span> <span data-ttu-id="7dca4-206">Найти hello FTP и FTPS URL-адреса для веб-узла в hello классический портал, выбрав веб-приложения и затем hello **мониторинга** ссылку.</span><span class="sxs-lookup"><span data-stu-id="7dca4-206">You can find hello FTP and FTPS URLs for your site in hello classic portal by selecting your web app, and then hello **Dashboard** link.</span></span> <span data-ttu-id="7dca4-207">Hello URL-адреса отображаются в hello **быстрый обзор** раздела.</span><span class="sxs-lookup"><span data-stu-id="7dca4-207">hello URLs are displayed in hello **quick glance** section.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="7dca4-208">Hello **web.config** файл только создается веб-сайтов Azure, если приложение не предоставляет.</span><span class="sxs-lookup"><span data-stu-id="7dca4-208">hello **web.config** file is only generated by Azure Websites if your application does not provide one.</span></span> <span data-ttu-id="7dca4-209">При указании **web.config** файл в корне проекта приложения hello, он будет использоваться веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="7dca4-209">If you provide a **web.config** file in hello root of your application project, it will be used by Azure Web Apps.</span></span>
  > 
  > 
  
    <span data-ttu-id="7dca4-210">Если запись hello не указан или задано значение tooa `true`, следует создать **web.config** в корневом каталоге приложения Node.js hello и укажите значение `false`.</span><span class="sxs-lookup"><span data-stu-id="7dca4-210">If hello entry is not present, or is set tooa value of `true`, then you should create a **web.config** in hello root of your Node.js application and specify a value of `false`.</span></span>  <span data-ttu-id="7dca4-211">Для справки ниже hello является значением по умолчанию **web.config** для приложения, использующего **в файле app.js** в качестве точки входа hello.</span><span class="sxs-lookup"><span data-stu-id="7dca4-211">For reference, hello below is a default **web.config** for an application that uses **app.js** as hello entry point.</span></span>
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used toorun node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that hello server.js file is a node.js web app toobe handled by hello iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether hello incoming URL matches a physical file in hello /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped toohello node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using hello following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes toorestart hello server
                * node_env: will be propagated toonode as NODE_ENV environment variable
                * debuggingEnabled - controls whether hello built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    <span data-ttu-id="7dca4-212">Если приложение использует точки входа, отличный от **в файле app.js**, необходимо заменить все вхождения **в файле app.js** с hello исправить точку входа.</span><span class="sxs-lookup"><span data-stu-id="7dca4-212">If your application uses an entry point other than **app.js**, you must replace all occurrences of **app.js** with hello correct entry point.</span></span> <span data-ttu-id="7dca4-213">Например, заменить **app.js** на **server.js**.</span><span class="sxs-lookup"><span data-stu-id="7dca4-213">For example, replacing **app.js** with **server.js**.</span></span>

> [!NOTE]
> <span data-ttu-id="7dca4-214">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений], в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="7dca4-214">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="7dca4-215">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="7dca4-215">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="7dca4-216">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7dca4-216">Next steps</span></span>
<span data-ttu-id="7dca4-217">В этом учебнике вы узнали, как toocreate это чат приложение, размещенное в веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="7dca4-217">In this tutorial you learned how toocreate a chat application hosted in an Azure web app.</span></span> <span data-ttu-id="7dca4-218">Это приложение также можно разместить в качестве облачной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="7dca4-218">You can also host this application as an Azure Cloud Service.</span></span> <span data-ttu-id="7dca4-219">Пошаговые инструкции о том, как tooaccomplish, см. в разделе [построения приложения чат Node.js с Socket.IO на облачную службу Azure].</span><span class="sxs-lookup"><span data-stu-id="7dca4-219">For steps on how tooaccomplish this, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>

<span data-ttu-id="7dca4-220">Дополнительные сведения см. также: hello [Центр разработчика Node.js].</span><span class="sxs-lookup"><span data-stu-id="7dca4-220">For more information, see also hello [Node.js Developer Center].</span></span>

## <a name="whats-changed"></a><span data-ttu-id="7dca4-221">Изменения</span><span class="sxs-lookup"><span data-stu-id="7dca4-221">What's changed</span></span>
* <span data-ttu-id="7dca4-222">Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure].</span><span class="sxs-lookup"><span data-stu-id="7dca4-222">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services].</span></span>

<!-- URL List -->

[кэш Azure Redis]: /documentation/services/redis-cache/
[веб-приложений служб приложения]: http://go.microsoft.com/fwlink/?LinkId=529714
[цены приложения Web]: http://go.microsoft.com/fwlink/?LinkId=511643
[построения приложения чат Node.js с Socket.IO на облачную службу Azure]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure hello Azure CLI]: ../cli-install-nodejs.md
[службе приложений Azure и ее влияние на существующие службы Azure]: http://go.microsoft.com/fwlink/?LinkId=529714
[Центр разработчика Node.js]: /develop/nodejs/
[повторите служб приложений]: https://azure.microsoft.com/try/app-service/
[Сходство экземпляров на веб-сайтах Azure]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[создание кэша в кэше Redis для Azure]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[socket.io redis]: https://github.com/socketio/socket.io-redis
[репозитории Socket.IO GitHub]: https://github.com/socketio/socket.io
[ZIP-файл или GZ архивные версии]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
