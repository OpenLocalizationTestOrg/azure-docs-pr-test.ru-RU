---
title: "Создание приложения для разговоров на Node.js с использованием Socket.IO в службе приложений Azure"
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
ms.openlocfilehash: e1aa539e1134884261ea7464bfda6d14815618d4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a><span data-ttu-id="6d295-103">Создание приложения для разговоров на Node.js с использованием Socket.IO в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="6d295-103">Create a Node.js chat application with Socket.IO in Azure App Service</span></span>
<span data-ttu-id="6d295-104">Socket.IO обеспечивает связь в режиме реального времени между сервером Node.js и клиентами с помощью WebSockets.</span><span class="sxs-lookup"><span data-stu-id="6d295-104">Socket.IO provides real-time communication between your node.js server and clients using WebSockets.</span></span> <span data-ttu-id="6d295-105">Он также поддерживает переход к другим протоколам (например, длинному опросу), работающим со старыми браузерами.</span><span class="sxs-lookup"><span data-stu-id="6d295-105">It also supports fallback to other transports (such as long polling) that work with older browsers.</span></span> <span data-ttu-id="6d295-106">В этом руководстве детально описано размещение приложения чата на основе Socket.IO в качестве веб-приложения Azure и показано, как выполнять масштабирование с помощью [кэша Redis для Azure].</span><span class="sxs-lookup"><span data-stu-id="6d295-106">This tutorial will walk you through hosting a Socket.IO based chat application as an Azure web app, and show you how to scale the application using [Azure Redis Cache].</span></span> <span data-ttu-id="6d295-107">Дополнительные сведения о Socket.IO см. на веб-сайте <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="6d295-107">For more information on Socket.IO, see <http://socket.io/>.</span></span>

> [!NOTE]
> <span data-ttu-id="6d295-108">Процедуры в этой задаче применяются к [веб-приложениям службы приложений]. Информацию об облачных службах см. в статье [Создание приложения для разговора Node.js с Socket.IO в облачной службе Azure].</span><span class="sxs-lookup"><span data-stu-id="6d295-108">The procedures in this task apply to [App Service Web Apps]; for Cloud Services, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>
> 
> 

## <a name="download-the-chat-example"></a><span data-ttu-id="6d295-109">Скачивание примера разговора</span><span class="sxs-lookup"><span data-stu-id="6d295-109">Download the chat example</span></span>
<span data-ttu-id="6d295-110">Для этого проекта мы будем использовать пример разговора из [репозитория GitHub Socket.IO].</span><span class="sxs-lookup"><span data-stu-id="6d295-110">For this project, we will use the chat example from the [Socket.IO GitHub repository].</span></span> <span data-ttu-id="6d295-111">Выполните следующие действия, чтобы скачать пример и добавить его в ранее созданный проект.</span><span class="sxs-lookup"><span data-stu-id="6d295-111">Perform the following steps to download the example and add it to the project you previously created.</span></span>

1. <span data-ttu-id="6d295-112">Загрузите выпуск проекта Socket.IO [в архиве ZIP или GZ] (в данном документе использована версия 1.3.5).</span><span class="sxs-lookup"><span data-stu-id="6d295-112">Download a [ZIP or GZ archived release] of the Socket.IO project (version 1.3.5 was used for this document)</span></span>
2. <span data-ttu-id="6d295-113">Извлеките содержимое архива и скопируйте каталог **examples\\chat** в новое расположение.</span><span class="sxs-lookup"><span data-stu-id="6d295-113">Extract the archive and copy the **examples\\chat** directory to a new location.</span></span> <span data-ttu-id="6d295-114">Например, в **\\node\\chat**.</span><span class="sxs-lookup"><span data-stu-id="6d295-114">For example, **\\node\\chat**.</span></span>

## <a name="modify-appjs-and-install-modules"></a><span data-ttu-id="6d295-115">Изменение app.js и установка модулей</span><span class="sxs-lookup"><span data-stu-id="6d295-115">Modify app.js and install modules</span></span>
1. <span data-ttu-id="6d295-116">Переименуйте файл **index.js** в **app.js**.</span><span class="sxs-lookup"><span data-stu-id="6d295-116">Rename the **index.js** file to **app.js**.</span></span> <span data-ttu-id="6d295-117">Благодаря этому Azure сможет распознать, что это приложение Node.js.</span><span class="sxs-lookup"><span data-stu-id="6d295-117">This allows Azure to detect that this is a Node.js application.</span></span>
2. <span data-ttu-id="6d295-118">Откройте файл **app.js** в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="6d295-118">Open the **app.js** file in a text editor.</span></span> <span data-ttu-id="6d295-119">Измените строку, содержащую `var io = require('../..')(server);` , как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="6d295-119">Change the line containing `var io = require('../..')(server);` as shown below:</span></span>
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. <span data-ttu-id="6d295-120">Откройте файл **package.json** и добавьте ссылку на socket.io в `dependencies`, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="6d295-120">Open the **package.json** file and add a reference to socket.io under `dependencies`, as shown below:</span></span>
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. <span data-ttu-id="6d295-121">В командной строке перейдите в каталог **\\node\\chat**, а затем выполните команду npm, чтобы установить модули, необходимые для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="6d295-121">From the command-line, change to the **\\node\\chat** directory and use npm to install the modules required by this application:</span></span>
   
        npm install
   
    <span data-ttu-id="6d295-122">Будет выполнена установка модулей во вложенную папку **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="6d295-122">This will install the modules into a subfolder named **node_modules**.</span></span>

## <a name="create-an-azure-web-app"></a><span data-ttu-id="6d295-123">Создание веб-приложения Azure</span><span class="sxs-lookup"><span data-stu-id="6d295-123">Create an Azure Web App</span></span>
<span data-ttu-id="6d295-124">Выполните следующие действия, чтобы создать веб-приложение Azure, включить публикацию Git, а затем включить поддержку WebSocket для этого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6d295-124">Follow these steps to create an Azure web app, enable Git publishing, and then enable WebSocket support for the web app.</span></span>

> [!NOTE]
> <span data-ttu-id="6d295-125">Для работы с этим учебником требуется учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="6d295-125">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="6d295-126">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="6d295-126">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6d295-127">Дополнительные сведения см. в разделе <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Бесплатная пробная версия Azure</a>;</span><span class="sxs-lookup"><span data-stu-id="6d295-127">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

1. <span data-ttu-id="6d295-128">Установите интерфейс командной строки Azure (Azure CLI) и подключитесь к своей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="6d295-128">Install the Azure Command-Line Interface (Azure CLI) and connect to your Azure subscription.</span></span> <span data-ttu-id="6d295-129">Ознакомьтесь со статьей [Установка и настройка интерфейса командной строки Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="6d295-129">See [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="6d295-130">Если вы настраиваете репозиторий в Azure впервые, потребуется создать для него учетные данные для входа.</span><span class="sxs-lookup"><span data-stu-id="6d295-130">If this is your first time setting up a repository in Azure, you need to create login credentials.</span></span> <span data-ttu-id="6d295-131">В интерфейсе командной строки Azure введите команду:</span><span class="sxs-lookup"><span data-stu-id="6d295-131">From the Azure CLI, enter the following command:</span></span>
   
        azure site deployment user set [username] [password]
3. <span data-ttu-id="6d295-132">Перейдите в каталог **\\node\chat** и выполните следующую команду, чтобы создать новое веб-приложение Azure и локальный репозиторий Git.</span><span class="sxs-lookup"><span data-stu-id="6d295-132">Change to the **\\node\chat** directory and use the following command to create a new Azure web app and a local Git repository.</span></span> <span data-ttu-id="6d295-133">Эта команда также создает удаленный Git с именем azure.</span><span class="sxs-lookup"><span data-stu-id="6d295-133">This command also creates a Git remote named 'azure'.</span></span>
   
        azure site create mysitename --git
   
    <span data-ttu-id="6d295-134">Замените mysitename уникальным именем созданного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6d295-134">You must replace 'mysitename' with a unique name for your web app.</span></span>
4. <span data-ttu-id="6d295-135">Поместите существующие файлы в локальный репозиторий посредством следующих команд:</span><span class="sxs-lookup"><span data-stu-id="6d295-135">Commit the existing files to the local repository by using the following commands:</span></span>
   
        git add .
        git commit -m "Initial commit"
5. <span data-ttu-id="6d295-136">Передайте файлы в репозиторий службы веб-приложений Azure с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="6d295-136">Push the files to the Azure Web Apps repository with the following command:</span></span>
   
        git push azure master
   
    <span data-ttu-id="6d295-137">При появлении запроса введите свои учетные данные из шага 2.</span><span class="sxs-lookup"><span data-stu-id="6d295-137">When prompted, enter your credentials from step 2.</span></span> <span data-ttu-id="6d295-138">Вы будете получать сообщения о статусе по мере импорта модулей на сервере.</span><span class="sxs-lookup"><span data-stu-id="6d295-138">You will receive status messages as modules are imported on the server.</span></span> <span data-ttu-id="6d295-139">После завершения этого процесса приложение будет размещаться в вашем веб-приложении Azure.</span><span class="sxs-lookup"><span data-stu-id="6d295-139">Once this process has completed, the application will be hosted on your Azure web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6d295-140">Во время установки модуля могут возникнуть ошибки "Импортированный проект ... не найден".</span><span class="sxs-lookup"><span data-stu-id="6d295-140">During module installation, you may notice errors that 'The imported project ... was not found'.</span></span> <span data-ttu-id="6d295-141">Эти сообщения можно спокойно проигнорировать.</span><span class="sxs-lookup"><span data-stu-id="6d295-141">These can safely be ignored.</span></span>
   > 
   > 
6. <span data-ttu-id="6d295-142">В Socket.IO используются сокеты WebSockets, которые по умолчанию не включены в Azure.</span><span class="sxs-lookup"><span data-stu-id="6d295-142">Socket.IO uses WebSockets, which are not enabled by default on Azure.</span></span> <span data-ttu-id="6d295-143">Для включения веб-сокетов воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="6d295-143">To enable web sockets, use the following command:</span></span>
   
        azure site set -w
   
    <span data-ttu-id="6d295-144">При появлении запроса введите имя веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6d295-144">If prompted, enter the name of the web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6d295-145">Команда azure site set -w действует только в интерфейсе командной строки Azure версии 0.7.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="6d295-145">The 'azure site set -w' command will work only with version 0.7.4 or higher of the Azure Command-Line Interface.</span></span> <span data-ttu-id="6d295-146">Вы также можете включить поддержку WebSocket с помощью [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6d295-146">You can also enable WebSocket support using the [Azure Portal](https://portal.azure.com).</span></span>
   > 
   > <span data-ttu-id="6d295-147">Чтобы включить WebSockets с помощью портала Azure, щелкните веб-приложение в колонке "Веб-приложения" и откройте **Все параметры** > **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="6d295-147">To enable WebSockets using the Azure Portal, click the web app from the Web Apps blade, click **All settings** > **Application settings**.</span></span> <span data-ttu-id="6d295-148">В разделе **Веб-сокеты** щелкните **Включить**.</span><span class="sxs-lookup"><span data-stu-id="6d295-148">Under **Web Sockets**, click **On**.</span></span> <span data-ttu-id="6d295-149">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="6d295-149">Then click **Save**.</span></span>
   > 
   > 
7. <span data-ttu-id="6d295-150">Для просмотра веб-сайта на платформе Azure выполните следующую команду, чтобы запустить веб-браузер и перейти к размещенному веб-приложению:</span><span class="sxs-lookup"><span data-stu-id="6d295-150">To view the web app on Azure, use the following command to launch your web browser and navigate to the hosted web app:</span></span>
   
        azure site browse

<span data-ttu-id="6d295-151">Теперь ваше приложение работает на платформе Azure и может передавать сообщения разговора между различными клиентами с использованием Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="6d295-151">Your app is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

## <a name="scale-out"></a><span data-ttu-id="6d295-152">Масштабирование</span><span class="sxs-lookup"><span data-stu-id="6d295-152">Scale out</span></span>
<span data-ttu-id="6d295-153">Приложения Socket.IO можно масштабировать с помощью **адаптера**, чтобы распределить сообщения и события между несколькими экземплярами приложения.</span><span class="sxs-lookup"><span data-stu-id="6d295-153">Socket.IO applications can be scaled out by using an **adapter** to distribute messages and events between multiple application instances.</span></span> <span data-ttu-id="6d295-154">Хотя доступно несколько адаптеров, адаптер [socket.io-redis] можно легко использовать с функцией кэша Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="6d295-154">While there are several adapters available, the [socket.io-redis] adapter can be easily used with the Azure Redis Cache feature.</span></span>

> [!NOTE]
> <span data-ttu-id="6d295-155">Дополнительным требованием к масштабированию решений Socket.IO является поддержка прикрепленных сеансов.</span><span class="sxs-lookup"><span data-stu-id="6d295-155">An additional requirement for scaling out a Socket.IO solution is support for sticky sessions.</span></span> <span data-ttu-id="6d295-156">Прикрепленные сеансы включены для веб-приложений Azure по умолчанию через маршрутизацию запросов Azure.</span><span class="sxs-lookup"><span data-stu-id="6d295-156">Sticky sessions are enabled by default for Azure Web Apps through Azure Request Routing.</span></span> <span data-ttu-id="6d295-157">Дополнительные сведения см. в разделе [Сходство экземпляров на веб-сайтах Azure].</span><span class="sxs-lookup"><span data-stu-id="6d295-157">For more information, see [Instance Affinity in Azure Web Sites].</span></span>
> 
> 

### <a name="create-a-redis-cache"></a><span data-ttu-id="6d295-158">Создание кэша Redis</span><span class="sxs-lookup"><span data-stu-id="6d295-158">Create a Redis cache</span></span>
<span data-ttu-id="6d295-159">Выполните шаги, приведенные в разделе [Создание кэша Azure Redis] , чтобы создать новый кэш.</span><span class="sxs-lookup"><span data-stu-id="6d295-159">Perform the steps in [Create a cache in Azure Redis Cache] to create a new cache.</span></span>

> [!NOTE]
> <span data-ttu-id="6d295-160">Сохраните значения **Имя узла** и **Первичный ключ** кэша, так как они понадобятся позднее.</span><span class="sxs-lookup"><span data-stu-id="6d295-160">Save the **Host name** and **Primary key** for your cache, as these will be needed in the next steps.</span></span>
> 
> 

### <a name="add-the-redis-and-socketio-redis-modules"></a><span data-ttu-id="6d295-161">Добавление модулей redis и socket.io-redis</span><span class="sxs-lookup"><span data-stu-id="6d295-161">Add the redis and socket.io-redis modules</span></span>
1. <span data-ttu-id="6d295-162">В командной строке перейдите в каталог **\\\node\\chat** и выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="6d295-162">From a command-line, change to the **\\node\\chat** directory and use the following command.</span></span>
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > <span data-ttu-id="6d295-163">Версии, указанные в этой команде, использовались при тестировании данной процедуры.</span><span class="sxs-lookup"><span data-stu-id="6d295-163">The versions specified in this command are the versions used when testing this article.</span></span>
   > 
   > 
2. <span data-ttu-id="6d295-164">Измените файл **app.js**, добавив приведенные ниже строки сразу после `var io = require('socket.io')(server);`.</span><span class="sxs-lookup"><span data-stu-id="6d295-164">Modify the **app.js** file to add the following lines immediately after `var io = require('socket.io')(server);`</span></span>
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    <span data-ttu-id="6d295-165">Замените **redishostname** и **rediskey** именем узла и ключом кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="6d295-165">Replace **redishostname** and **rediskey** with the host name and key for your Redis cache.</span></span>
   
    <span data-ttu-id="6d295-166">Будет создан клиент публикации и подписки для ранее созданного кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="6d295-166">This will create a publish and subscribe client to the Redis cache created previously.</span></span> <span data-ttu-id="6d295-167">С помощью клиентов и адаптера будет настроен Socket.IO для использования кэша Redis, что обеспечит передачу сообщений и событий между экземплярами вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="6d295-167">The clients are then used with the adapter to configure Socket.IO to use the Redis cache for passing messages and events between instances of your application</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6d295-168">Хотя адаптер **socket.io-redis** может взаимодействовать непосредственно с Redis, текущая версия не поддерживает аутентификацию, требуемую кэшем Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="6d295-168">While the **socket.io-redis** adapter can communicate directly to Redis, the current version does not support the authentication required by Azure Redis cache.</span></span> <span data-ttu-id="6d295-169">Поэтому первоначальное подключение создается с помощью модуля **redis**, а затем клиент передается адаптеру **socket.io-redis**.</span><span class="sxs-lookup"><span data-stu-id="6d295-169">So the initial connection is created using the **redis** module, then the client is passed to the **socket.io-redis** adapter.</span></span>
   > 
   > <span data-ttu-id="6d295-170">Хотя кэш Azure Redis поддерживает безопасные подключения через порт 6380, модули, использованные в данном примере, по состоянию на 14.7.2014 не поддерживают безопасные подключения.</span><span class="sxs-lookup"><span data-stu-id="6d295-170">While Azure Redis Cache supports secure connections using port 6380, the modules used in this example do not support secure connections as of 7/14/2014.</span></span> <span data-ttu-id="6d295-171">В приведенном выше коде используется небезопасный порт по умолчанию — 6379.</span><span class="sxs-lookup"><span data-stu-id="6d295-171">The above code uses the default, unsecure port of 6379.</span></span>
   > 
   > 
3. <span data-ttu-id="6d295-172">Сохраните измененный файл **app.js**.</span><span class="sxs-lookup"><span data-stu-id="6d295-172">Save the modified **app.js**</span></span>

### <a name="commit-changes-and-redeploy"></a><span data-ttu-id="6d295-173">Подтверждение изменений и повторное развертывание</span><span class="sxs-lookup"><span data-stu-id="6d295-173">Commit changes and redeploy</span></span>
<span data-ttu-id="6d295-174">В командной строке в каталоге **\\node\\chat** выполните следующую команду для подтверждения изменений и повторного развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="6d295-174">From the command-line in the **\\node\\chat** directory, use the following commands to commit changes and redeploy the application.</span></span>

    git add .
    git commit -m "implementing scale out"
    git push azure master

<span data-ttu-id="6d295-175">Как только изменения будут отправлены на сервер, вы сможете масштабировать сайт между несколькими экземплярами следующей командой:</span><span class="sxs-lookup"><span data-stu-id="6d295-175">Once the changes have been pushed to the server, you can scale your site across multiple instances by using the following command.</span></span>

    azure site scale instances --instances #

<span data-ttu-id="6d295-176">где **#** — количество экземпляров, которое требуется создать.</span><span class="sxs-lookup"><span data-stu-id="6d295-176">Where **#** is the number of instances to create.</span></span>

<span data-ttu-id="6d295-177">Вы можете подключиться к своему веб-приложению из разных браузеров и с разных компьютеров, чтобы убедиться, что сообщения должным образом отправляются всем клиентам.</span><span class="sxs-lookup"><span data-stu-id="6d295-177">You can connect to your web app from multiple browsers or computers to verify that messages are correctly sent to all clients.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6d295-178">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="6d295-178">Troubleshooting</span></span>
### <a name="connection-limits"></a><span data-ttu-id="6d295-179">Ограничения на подключения</span><span class="sxs-lookup"><span data-stu-id="6d295-179">Connection limits</span></span>
<span data-ttu-id="6d295-180">Веб-приложения Azure доступны в нескольких номерах SKU, которые определяются ресурсами, доступными для вашего сайта.</span><span class="sxs-lookup"><span data-stu-id="6d295-180">Azure Web Apps is available in multiple SKUs, which determine the resources available to your site.</span></span> <span data-ttu-id="6d295-181">Сюда входит количество разрешенных соединений WebSocket.</span><span class="sxs-lookup"><span data-stu-id="6d295-181">This includes the number of allowed WebSocket connections.</span></span> <span data-ttu-id="6d295-182">Дополнительные сведения см. на странице [цен на веб-приложения].</span><span class="sxs-lookup"><span data-stu-id="6d295-182">For more information, see the [Web Apps Pricing page].</span></span>

### <a name="messages-arent-being-sent-using-websockets"></a><span data-ttu-id="6d295-183">Не отправляются сообщения через WebSockets</span><span class="sxs-lookup"><span data-stu-id="6d295-183">Messages aren't being sent using WebSockets</span></span>
<span data-ttu-id="6d295-184">Если браузеры клиентов по-прежнему переходят к длинному опросу и не используют WebSockets, возможны следующие причины.</span><span class="sxs-lookup"><span data-stu-id="6d295-184">If client browsers keep falling back to long polling instead of using WebSockets, it may be because of one of the following.</span></span>

* <span data-ttu-id="6d295-185">**Попробуйте ограничить протоколы, оставив только WebSockets**</span><span class="sxs-lookup"><span data-stu-id="6d295-185">**Try limiting the transport to just WebSockets**</span></span>
  
    <span data-ttu-id="6d295-186">Чтобы Socket.IO использовал в качестве протокола сообщений WebSockets, как сервер, так и клиент должны поддерживать WebSockets.</span><span class="sxs-lookup"><span data-stu-id="6d295-186">In order for Socket.IO to use WebSockets as the messaging transport, both the server and client must support WebSockets.</span></span> <span data-ttu-id="6d295-187">Если тот или другой его не поддерживает, Socket.IO согласует другой протокол, например длинный опрос.</span><span class="sxs-lookup"><span data-stu-id="6d295-187">If one or the other does not, Socket.IO will negotiate another transport, such as long polling.</span></span> <span data-ttu-id="6d295-188">Список протоколов по умолчанию, используемых Socket.IO: ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span><span class="sxs-lookup"><span data-stu-id="6d295-188">The default list of transports used by Socket.IO is ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span></span> <span data-ttu-id="6d295-189">Вы можете указать принудительное использование только протокола WebSockets, добавив следующий код в файл **app.js** после строки с `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="6d295-189">You can force it to only use WebSockets by adding the following code to the **app.js** file, after the line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > <span data-ttu-id="6d295-190">Обратите внимание, что старые браузеры, не поддерживающие WebSockets, не смогут подключиться к сайту, если вышеуказанный код будет активен, так как он ограничивает обмен данными протоколом WebSockets.</span><span class="sxs-lookup"><span data-stu-id="6d295-190">Note that older browsers that do not support WebSockets will not be able to connect to the site while the above code is active, as it restricts communication to WebSockets only.</span></span>
  > 
  > 
* <span data-ttu-id="6d295-191">**Использование SSL**</span><span class="sxs-lookup"><span data-stu-id="6d295-191">**Use SSL**</span></span>
  
    <span data-ttu-id="6d295-192">WebSockets использует некоторые малоиспользуемые заголовки HTTP, например **Upgrade** .</span><span class="sxs-lookup"><span data-stu-id="6d295-192">WebSockets relies on some lesser used HTTP headers, such as the **Upgrade** header.</span></span> <span data-ttu-id="6d295-193">Некоторые промежуточные сетевые устройства, например прокси-серверы, могут удалять эти заголовки.</span><span class="sxs-lookup"><span data-stu-id="6d295-193">Some intermediate network devices, such as web proxies, may remove these headers.</span></span> <span data-ttu-id="6d295-194">Чтобы избежать этого, можно установить подключение WebSocket через SSL.</span><span class="sxs-lookup"><span data-stu-id="6d295-194">To avoid this problem, you can establish the WebSocket connection over SSL.</span></span>
  
    <span data-ttu-id="6d295-195">Простой способ сделать это — настроить для Socket.IO протокол `match origin protocol`.</span><span class="sxs-lookup"><span data-stu-id="6d295-195">An easy way to accomplish this is to configure Socket.IO to `match origin protocol`.</span></span> <span data-ttu-id="6d295-196">При этом Socket.IO будет защищать соединения WebSockets тем же образом, что и исходные запросы HTTP/HTTPS к веб-странице.</span><span class="sxs-lookup"><span data-stu-id="6d295-196">This instructs Socket.IO to secure WebSockets communication the same as the originating HTTP/HTTPS request for the web page.</span></span> <span data-ttu-id="6d295-197">Если браузер использует для посещения сайта URL-адрес с протоколом HTTPS, последующий обмен данными WebSocket через Socket.IO будет защищен с помощью SSL.</span><span class="sxs-lookup"><span data-stu-id="6d295-197">If a browser uses an HTTPS URL to visit your website, subsequent WebSocket communications through Socket.IO will be secured over SSL.</span></span>
  
    <span data-ttu-id="6d295-198">Чтобы включить такую конфигурацию в данном примере, добавьте приведенный ниже код в файл **app.js** после строки с `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="6d295-198">To modify this example to enable this configuration, add the following code to the **app.js** file after the line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* <span data-ttu-id="6d295-199">**Проверка настроек web.config**</span><span class="sxs-lookup"><span data-stu-id="6d295-199">**Verify web.config settings**</span></span>
  
    <span data-ttu-id="6d295-200">Веб-приложения Azure с приложениями Node.js используют файл **web.config** для маршрутизации входящих запросов к приложению Node.js.</span><span class="sxs-lookup"><span data-stu-id="6d295-200">Azure web apps that host Node.js applications use the **web.config** file to route incoming requests to the Node.js application.</span></span> <span data-ttu-id="6d295-201">Чтобы WebSockets работал правильно с приложениями Node.js, в файле **web.config** должна быть следующая запись:</span><span class="sxs-lookup"><span data-stu-id="6d295-201">For WebSockets to function correctly with Node.js applications, the **web.config** must contain the following entry.</span></span>
  
        <webSocket enabled="false"/>
  
    <span data-ttu-id="6d295-202">Это позволяет отключить модуль WebSocket служб IIS, который содержит собственную реализацию модулей WebSocket и конфликтует с модулями WebSocket, используемыми специально для Node.js, например с Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="6d295-202">This disables the IIS WebSockets module, which includes its own implementation of WebSockets and conflicts with Node.js specific WebSocket modules such as Socket.IO.</span></span> <span data-ttu-id="6d295-203">Если эта строка отсутствует или для нее задано значение `true`, возможно, из-за этого в приложении не будет работать транспорт WebSocket.</span><span class="sxs-lookup"><span data-stu-id="6d295-203">If this line is not present, or is set to `true`, this may be the reason that the WebSocket transport is not working for your application.</span></span>
  
    <span data-ttu-id="6d295-204">Обычно приложения Node.js не включают файл **web.config** , поэтому веб-сайты Azure автоматически будут создавать его для приложений Node.js при их развертывании.</span><span class="sxs-lookup"><span data-stu-id="6d295-204">Normally, Node.js applications do not include a **web.config** file, so Azure Websites will automatically generate one for Node.js applications when they are deployed.</span></span> <span data-ttu-id="6d295-205">Поскольку этот файл автоматически создается на сервере, следует использовать для его просмотра URL-адрес с протоколами FTP и FTPS.</span><span class="sxs-lookup"><span data-stu-id="6d295-205">Since this file is automatically generated on the server, you must use the FTP or FTPS URL for your website to view this file.</span></span> <span data-ttu-id="6d295-206">URL-адреса с протоколами FTP и FTPS для вашего сайта можно найти на классическом портале Azure: выберите свое веб-приложение, а затем ссылку **Панель мониторинга** .</span><span class="sxs-lookup"><span data-stu-id="6d295-206">You can find the FTP and FTPS URLs for your site in the classic portal by selecting your web app, and then the **Dashboard** link.</span></span> <span data-ttu-id="6d295-207">URL-адреса будут выведены в разделе **Сводка** .</span><span class="sxs-lookup"><span data-stu-id="6d295-207">The URLs are displayed in the **quick glance** section.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="6d295-208">Файл **web.config** создается веб-сайтами Azure, только если его нет в самом приложении.</span><span class="sxs-lookup"><span data-stu-id="6d295-208">The **web.config** file is only generated by Azure Websites if your application does not provide one.</span></span> <span data-ttu-id="6d295-209">Если в корне проекта приложения есть файл **web.config** , веб-приложения Azure будут использовать его.</span><span class="sxs-lookup"><span data-stu-id="6d295-209">If you provide a **web.config** file in the root of your application project, it will be used by Azure Web Apps.</span></span>
  > 
  > 
  
    <span data-ttu-id="6d295-210">Если запись отсутствует или для нее установлено значение `true`, следует создать файл **web.config** в корне приложения Node.js и задать значение `false`.</span><span class="sxs-lookup"><span data-stu-id="6d295-210">If the entry is not present, or is set to a value of `true`, then you should create a **web.config** in the root of your Node.js application and specify a value of `false`.</span></span>  <span data-ttu-id="6d295-211">Для справки ниже представлен файл **web.config** по умолчанию для приложения, использующего **app.js** в качестве точки входа.</span><span class="sxs-lookup"><span data-stu-id="6d295-211">For reference, the below is a default **web.config** for an application that uses **app.js** as the entry point.</span></span>
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used to run node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that the server.js file is a node.js web app to be handled by the iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether the incoming URL matches a physical file in the /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped to the node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using the following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes to restart the server
                * node_env: will be propagated to node as NODE_ENV environment variable
                * debuggingEnabled - controls whether the built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    <span data-ttu-id="6d295-212">Если приложение использует точку входа, отличную от **app.js**, то следует заменить все вхождения **app.js** соответствующей точкой входа.</span><span class="sxs-lookup"><span data-stu-id="6d295-212">If your application uses an entry point other than **app.js**, you must replace all occurrences of **app.js** with the correct entry point.</span></span> <span data-ttu-id="6d295-213">Например, заменить **app.js** на **server.js**.</span><span class="sxs-lookup"><span data-stu-id="6d295-213">For example, replacing **app.js** with **server.js**.</span></span>

> [!NOTE]
> <span data-ttu-id="6d295-214">Чтобы приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений], где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="6d295-214">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="6d295-215">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="6d295-215">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="6d295-216">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6d295-216">Next steps</span></span>
<span data-ttu-id="6d295-217">В данном учебнике рассмотрено создание приложения для разговоров, размещенного в веб-приложении Azure.</span><span class="sxs-lookup"><span data-stu-id="6d295-217">In this tutorial you learned how to create a chat application hosted in an Azure web app.</span></span> <span data-ttu-id="6d295-218">Это приложение также можно разместить в качестве облачной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="6d295-218">You can also host this application as an Azure Cloud Service.</span></span> <span data-ttu-id="6d295-219">Инструкции о том, как это сделать, см. в разделе [Создание приложения для разговора Node.js с Socket.IO в облачной службе Azure].</span><span class="sxs-lookup"><span data-stu-id="6d295-219">For steps on how to accomplish this, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>

<span data-ttu-id="6d295-220">Дополнительные сведения см. также в [центре по разработке для Node.js].</span><span class="sxs-lookup"><span data-stu-id="6d295-220">For more information, see also the [Node.js Developer Center].</span></span>

## <a name="whats-changed"></a><span data-ttu-id="6d295-221">Изменения</span><span class="sxs-lookup"><span data-stu-id="6d295-221">What's changed</span></span>
* <span data-ttu-id="6d295-222">Руководство по переходу от веб-сайтов к службе приложений представлено в статье [Служба приложений Azure и существующие службы Azure].</span><span class="sxs-lookup"><span data-stu-id="6d295-222">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services].</span></span>

<!-- URL List -->

<span data-ttu-id="6d295-223">[кэша Redis для Azure]: /documentation/services/redis-cache/</span><span class="sxs-lookup"><span data-stu-id="6d295-223">[Azure Redis Cache]: /documentation/services/redis-cache/</span></span>
<span data-ttu-id="6d295-224">[веб-приложениям службы приложений]: http://go.microsoft.com/fwlink/?LinkId=529714</span><span class="sxs-lookup"><span data-stu-id="6d295-224">[App Service Web Apps]: http://go.microsoft.com/fwlink/?LinkId=529714</span></span>
<span data-ttu-id="6d295-225">[цен на веб-приложения]: http://go.microsoft.com/fwlink/?LinkId=511643</span><span class="sxs-lookup"><span data-stu-id="6d295-225">[Web Apps Pricing page]: http://go.microsoft.com/fwlink/?LinkId=511643</span></span>
<span data-ttu-id="6d295-226">[Создание приложения для разговора Node.js с Socket.IO в облачной службе Azure]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md</span><span class="sxs-lookup"><span data-stu-id="6d295-226">[Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md</span></span>
[Install and Configure the Azure CLI]: ../cli-install-nodejs.md
<span data-ttu-id="6d295-227">[Служба приложений Azure и существующие службы Azure]: http://go.microsoft.com/fwlink/?LinkId=529714</span><span class="sxs-lookup"><span data-stu-id="6d295-227">[Azure App Service and Its Impact on Existing Azure Services]: http://go.microsoft.com/fwlink/?LinkId=529714</span></span>
<span data-ttu-id="6d295-228">[центре по разработке для Node.js]: /develop/nodejs/</span><span class="sxs-lookup"><span data-stu-id="6d295-228">[Node.js Developer Center]: /develop/nodejs/</span></span>
<span data-ttu-id="6d295-229">[Пробное использование службы приложений]: https://azure.microsoft.com/try/app-service/</span><span class="sxs-lookup"><span data-stu-id="6d295-229">[Try App Service]: https://azure.microsoft.com/try/app-service/</span></span>
<span data-ttu-id="6d295-230">[Сходство экземпляров на веб-сайтах Azure]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/</span><span class="sxs-lookup"><span data-stu-id="6d295-230">[Instance Affinity in Azure Web Sites]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/</span></span>
<span data-ttu-id="6d295-231">[Создание кэша Azure Redis]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md</span><span class="sxs-lookup"><span data-stu-id="6d295-231">[Create a cache in Azure Redis Cache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md</span></span>

<span data-ttu-id="6d295-232">[socket.io-redis]: https://github.com/socketio/socket.io-redis</span><span class="sxs-lookup"><span data-stu-id="6d295-232">[socket.io-redis]: https://github.com/socketio/socket.io-redis</span></span>
<span data-ttu-id="6d295-233">[репозитория GitHub Socket.IO]: https://github.com/socketio/socket.io</span><span class="sxs-lookup"><span data-stu-id="6d295-233">[Socket.IO GitHub repository]: https://github.com/socketio/socket.io</span></span>
<span data-ttu-id="6d295-234">[в архиве ZIP или GZ]: https://github.com/socketio/socket.io/releases</span><span class="sxs-lookup"><span data-stu-id="6d295-234">[ZIP or GZ archived release]: https://github.com/socketio/socket.io/releases</span></span>

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
