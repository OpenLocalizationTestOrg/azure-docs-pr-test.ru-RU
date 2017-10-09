---
title: "toowork aaaHow с сервера базы данных hello Node.js SDK для мобильных приложений | Документы Microsoft"
description: "Узнайте, как toowork с hello внутренний сервер Node.js SDK для мобильных приложений службы приложения Azure."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: e7d97d3b-356e-4fb3-ba88-38ecbda5ea50
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b1ea5fda6f6ca422b92fe29ff8d16bf035018d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-nodejs-sdk"></a><span data-ttu-id="df8a6-103">Как toouse hello SDK Azure Mobile приложений Node.js</span><span class="sxs-lookup"><span data-stu-id="df8a6-103">How toouse hello Azure Mobile Apps Node.js SDK</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="df8a6-104">В этой статье содержатся подробные сведения и примеры, показывающие, как toowork с серверной Node.js в мобильных приложениях службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="df8a6-104">This article provides detailed information and examples showing how toowork with a Node.js backend in Azure App Service Mobile Apps.</span></span>

## <span data-ttu-id="df8a6-105"><a name="Introduction"></a>Введение</span><span class="sxs-lookup"><span data-stu-id="df8a6-105"><a name="Introduction"></a>Introduction</span></span>
<span data-ttu-id="df8a6-106">Приложение службы мобильные приложения Azure предоставляет hello возможность tooadd, оптимизированные для мобильных устройств доступ к данным веб-API tooa веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="df8a6-106">Azure App Service Mobile Apps provides hello capability tooadd a mobile-optimized data access Web API tooa web application.</span></span>  <span data-ttu-id="df8a6-107">пакет SDK для Azure приложений службы мобильного приложения Hello предоставляется для веб-приложений ASP.NET и Node.js.</span><span class="sxs-lookup"><span data-stu-id="df8a6-107">hello Azure App Service Mobile Apps SDK is provided for ASP.NET and Node.js web applications.</span></span>  <span data-ttu-id="df8a6-108">Hello SDK предоставляет hello следующие операции:</span><span class="sxs-lookup"><span data-stu-id="df8a6-108">hello SDK provides hello following operations:</span></span>

* <span data-ttu-id="df8a6-109">Табличные операции (чтение, вставка, обновление, удаление данных).</span><span class="sxs-lookup"><span data-stu-id="df8a6-109">Table operations (Read, Insert, Update, Delete) for data access</span></span>
* <span data-ttu-id="df8a6-110">Пользовательские операции API.</span><span class="sxs-lookup"><span data-stu-id="df8a6-110">Custom API operations</span></span>

<span data-ttu-id="df8a6-111">Операции обоих типов поддерживают проверку подлинности для всех поставщиков удостоверений, разрешенных службой приложений Azure, включая поставщиков удостоверений социальных сетей, таких как Facebook, Twitter, Google и Майкрософт, а также Azure Active Directory для корпоративной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="df8a6-111">Both operations provide for authentication across all identity providers allowed by Azure App Service, including social identity providers such as Facebook, Twitter, Google and Microsoft as well as Azure Active Directory for enterprise identity.</span></span>

<span data-ttu-id="df8a6-112">Можно найти примеры для каждого варианта использования в hello [каталог образцов на GitHub].</span><span class="sxs-lookup"><span data-stu-id="df8a6-112">You can find samples for each use case in hello [samples directory on GitHub].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="df8a6-113">Поддерживаемые платформы</span><span class="sxs-lookup"><span data-stu-id="df8a6-113">Supported Platforms</span></span>
<span data-ttu-id="df8a6-114">Hello пакет SDK для приложений мобильных узла Azure поддерживает hello выпуске LTS текущего узла и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="df8a6-114">hello Azure Mobile Apps Node SDK supports hello current LTS release of Node and later.</span></span>  <span data-ttu-id="df8a6-115">На момент написания статьи, последняя версия LTS hello — v4.5.0 узла.</span><span class="sxs-lookup"><span data-stu-id="df8a6-115">As of writing, hello latest LTS version is Node v4.5.0.</span></span>  <span data-ttu-id="df8a6-116">Другие версии Node могут также работать, но они не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="df8a6-116">Other versions of Node may work, but are not supported.</span></span>

<span data-ttu-id="df8a6-117">Hello пакет SDK для приложений мобильных узла Azure поддерживает два драйвера базы данных - hello узел mssql драйвер поддерживает SQL Azure и локальные экземпляры SQL Server.</span><span class="sxs-lookup"><span data-stu-id="df8a6-117">hello Azure Mobile Apps Node SDK supports two database drivers - hello node-mssql driver supports SQL Azure and local SQL Server instances.</span></span>  <span data-ttu-id="df8a6-118">Hello sqlite3 драйвер поддерживает SQLite баз данных в одном экземпляре.</span><span class="sxs-lookup"><span data-stu-id="df8a6-118">hello sqlite3 driver supports SQLite databases on a single instance only.</span></span>

### <span data-ttu-id="df8a6-119"><a name="howto-cmdline-basicapp"></a>Как: Создание основных Node.js серверной части с помощью hello командной строки</span><span class="sxs-lookup"><span data-stu-id="df8a6-119"><a name="howto-cmdline-basicapp"></a>How to: Create a Basic Node.js backend using hello Command Line</span></span>
<span data-ttu-id="df8a6-120">Каждая серверная часть на Node.js для мобильного приложения службы приложений Azure запускается как приложение ExpressJS.</span><span class="sxs-lookup"><span data-stu-id="df8a6-120">Every Azure App Service Mobile App Node.js backend starts as an ExpressJS application.</span></span>  <span data-ttu-id="df8a6-121">ExpressJS — hello наиболее популярных веб-службы платформа для Node.js.</span><span class="sxs-lookup"><span data-stu-id="df8a6-121">ExpressJS is hello most popular web service framework available for Node.js.</span></span>  <span data-ttu-id="df8a6-122">Вот как создать простое приложение [Express] :</span><span class="sxs-lookup"><span data-stu-id="df8a6-122">You can create a basic [Express] application as follows:</span></span>

1. <span data-ttu-id="df8a6-123">В командной строке или окне PowerShell создайте каталог для проекта.</span><span class="sxs-lookup"><span data-stu-id="df8a6-123">In a command or PowerShell window, create a directory for your project.</span></span>

        mkdir basicapp
2. <span data-ttu-id="df8a6-124">Запустите структуры пакета hello tooinitialize init npm.</span><span class="sxs-lookup"><span data-stu-id="df8a6-124">Run npm init tooinitialize hello package structure.</span></span>

        cd basicapp
        npm init

    <span data-ttu-id="df8a6-125">команда init npm Hello запрашивает набор вопросов tooinitialize hello проекта.</span><span class="sxs-lookup"><span data-stu-id="df8a6-125">hello npm init command asks a set of questions tooinitialize hello project.</span></span>  <span data-ttu-id="df8a6-126">См. в выходных данных примера hello:</span><span class="sxs-lookup"><span data-stu-id="df8a6-126">See hello example output:</span></span>

    ![выходные данные init npm Hello][0]
3. <span data-ttu-id="df8a6-128">Установите экспресс-варианте и мобильных приложений azure библиотеки hello из репозитория npm hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-128">Install hello express and azure-mobile-apps libraries from hello npm repository.</span></span>

        npm install --save express azure-mobile-apps
4. <span data-ttu-id="df8a6-129">Создайте в файле app.js файл tooimplement hello основных мобильных сервер.</span><span class="sxs-lookup"><span data-stu-id="df8a6-129">Create an app.js file tooimplement hello basic mobile server.</span></span>

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

<span data-ttu-id="df8a6-130">Это приложение создает WebAPI, оптимизированные для мобильных устройств с одной конечной точке (`/tables/TodoItem`), предоставляющий доступ без проверки подлинности tooan базового хранилища данных SQL с помощью динамической схемы.</span><span class="sxs-lookup"><span data-stu-id="df8a6-130">This application creates a mobile-optimized WebAPI with a single endpoint (`/tables/TodoItem`) that provides unauthenticated access tooan underlying SQL data store using a dynamic schema.</span></span>  <span data-ttu-id="df8a6-131">Этот пример подходит к следующим примерам использования клиентских библиотек.</span><span class="sxs-lookup"><span data-stu-id="df8a6-131">It is suitable for following the client library quick starts:</span></span>

* <span data-ttu-id="df8a6-132">[Быстрый запуск клиента Android]</span><span class="sxs-lookup"><span data-stu-id="df8a6-132">[Android Client QuickStart]</span></span>
* <span data-ttu-id="df8a6-133">[Быстрый запуск клиента Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="df8a6-133">[Apache Cordova Client QuickStart]</span></span>
* <span data-ttu-id="df8a6-134">[Быстрый запуск клиента iOS.]</span><span class="sxs-lookup"><span data-stu-id="df8a6-134">[iOS Client QuickStart]</span></span>
* <span data-ttu-id="df8a6-135">[Быстрый запуск клиента Магазина Windows Phone.]</span><span class="sxs-lookup"><span data-stu-id="df8a6-135">[Windows Store Client QuickStart]</span></span>
* <span data-ttu-id="df8a6-136">[Быстрый запуск клиента Xamarin.iOS.]</span><span class="sxs-lookup"><span data-stu-id="df8a6-136">[Xamarin.iOS Client QuickStart]</span></span>
* <span data-ttu-id="df8a6-137">[Быстрый запуск клиента Xamarin.Android.]</span><span class="sxs-lookup"><span data-stu-id="df8a6-137">[Xamarin.Android Client QuickStart]</span></span>
* <span data-ttu-id="df8a6-138">[Быстрый запуск клиента Xamarin.Forms.]</span><span class="sxs-lookup"><span data-stu-id="df8a6-138">[Xamarin.Forms Client QuickStart]</span></span>

<span data-ttu-id="df8a6-139">Это основное приложение hello находятся кода hello [пример basicapp на GitHub].</span><span class="sxs-lookup"><span data-stu-id="df8a6-139">You can find hello code for this basic application in hello [basicapp sample on GitHub].</span></span>

### <span data-ttu-id="df8a6-140"><a name="howto-vs2015-basicapp"></a>Создание серверной части на основе Node.js с помощью Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="df8a6-140"><a name="howto-vs2015-basicapp"></a>How to: Create a Node backend with Visual Studio 2015</span></span>
<span data-ttu-id="df8a6-141">Visual Studio 2015 требуется расширение приложений Node.js toodevelop внутри hello интегрированной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="df8a6-141">Visual Studio 2015 requires an extension toodevelop Node.js applications within hello IDE.</span></span>  <span data-ttu-id="df8a6-142">toostart установки hello [Node.js Tools 1.1 для Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="df8a6-142">toostart, install hello [Node.js Tools 1.1 for Visual Studio].</span></span>  <span data-ttu-id="df8a6-143">После установки hello Node.js Tools для Visual Studio создайте приложение 4.x Express:</span><span class="sxs-lookup"><span data-stu-id="df8a6-143">Once hello Node.js Tools for Visual Studio are installed, create an Express 4.x application:</span></span>

1. <span data-ttu-id="df8a6-144">Откройте hello **новый проект** диалоговое окно (из **файл** > **New** > **проект...** ).</span><span class="sxs-lookup"><span data-stu-id="df8a6-144">Open hello **New Project** dialog (from **File** > **New** > **Project...**).</span></span>
2. <span data-ttu-id="df8a6-145">Разверните **Шаблоны** > **JavaScript** > **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-145">Expand **Templates** > **JavaScript** > **Node.js**.</span></span>
3. <span data-ttu-id="df8a6-146">Выберите hello **Basic Azure Express 4 приложения Node.js**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-146">Select hello **Basic Azure Node.js Express 4 Application**.</span></span>
4. <span data-ttu-id="df8a6-147">Введите имя проекта hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-147">Fill in hello project name.</span></span>  <span data-ttu-id="df8a6-148">Нажмите кнопку *ОК*.</span><span class="sxs-lookup"><span data-stu-id="df8a6-148">Click *OK*.</span></span>

    ![Новый проект Visual Studio 2015][1]
5. <span data-ttu-id="df8a6-150">Щелкните правой кнопкой мыши hello **npm** , а затем выберите **установить новые пакеты npm...** .</span><span class="sxs-lookup"><span data-stu-id="df8a6-150">Right-click hello **npm** node and select **Install New npm packages...**.</span></span>
6. <span data-ttu-id="df8a6-151">Может потребоваться toorefresh hello npm каталога на создание первого приложения Node.js.</span><span class="sxs-lookup"><span data-stu-id="df8a6-151">You may need toorefresh hello npm catalog on creating your first Node.js application.</span></span>  <span data-ttu-id="df8a6-152">При необходимости щелкните **Обновить** .</span><span class="sxs-lookup"><span data-stu-id="df8a6-152">Click **Refresh** if necessary.</span></span>
7. <span data-ttu-id="df8a6-153">Введите *мобильных приложений azure* в поле поиска hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-153">Enter *azure-mobile-apps* in hello search box.</span></span>  <span data-ttu-id="df8a6-154">Нажмите кнопку hello **приложения azure mobile 2.0.0** пакета, а затем нажмите кнопку **установить пакет**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-154">Click hello **azure-mobile-apps 2.0.0** package, then click **Install Package**.</span></span>

    ![Установка новых пакетов npm][2]
8. <span data-ttu-id="df8a6-156">Нажмите кнопку **Закрыть**</span><span class="sxs-lookup"><span data-stu-id="df8a6-156">Click **Close**.</span></span>
9. <span data-ttu-id="df8a6-157">Откройте hello *в файле app.js* файл tooadd поддержка hello пакет SDK Azure Mobile приложений.</span><span class="sxs-lookup"><span data-stu-id="df8a6-157">Open hello *app.js* file tooadd support for hello Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="df8a6-158">В нижней границы hello 6 at hello библиотеки требуют инструкции, добавить hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="df8a6-158">At line 6 at hello bottom of hello library require statements, add hello following code:</span></span>

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    <span data-ttu-id="df8a6-159">Около строки 27 после hello других инструкций app.use добавьте hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="df8a6-159">At approximately line 27 after hello other app.use statements, add hello following code:</span></span>

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    <span data-ttu-id="df8a6-160">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-160">Save hello file.</span></span>
10. <span data-ttu-id="df8a6-161">Запуск локально приложения hello (приветствия на http://localhost:3000 обслуживается API), либо опубликовать tooAzure.</span><span class="sxs-lookup"><span data-stu-id="df8a6-161">Either run hello application locally (hello API is served on http://localhost:3000) or publish tooAzure.</span></span>

### <span data-ttu-id="df8a6-162"><a name="create-node-backend-portal"></a>Как: создание серверной части Node.js с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="df8a6-162"><a name="create-node-backend-portal"></a>How to: Create a Node.js backend using hello Azure portal</span></span>
<span data-ttu-id="df8a6-163">Создании право серверной мобильное приложение hello [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="df8a6-163">You can create a Mobile App backend right in hello [Azure portal].</span></span> <span data-ttu-id="df8a6-164">Можно либо выполнить hello следующих шагов или создать клиентом и сервером вместе с следующие hello [создать мобильное приложение](app-service-mobile-ios-get-started.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="df8a6-164">You can either follow hello following steps or create a client and server together by following hello [Create a mobile app](app-service-mobile-ios-get-started.md) tutorial.</span></span> <span data-ttu-id="df8a6-165">Hello учебник содержит упрощенную версию эти инструкции и лучше всего подходит для проверки концепции проектов.</span><span class="sxs-lookup"><span data-stu-id="df8a6-165">hello tutorial contains a simplified version of these instructions and is best for proof of concept projects.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="df8a6-166">В hello *приступить к работе* колонки в разделе **создать таблицу API**, выберите **Node.js** как вашей **языка серверной**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-166">Back in hello *Get started* blade, under **Create a table API**, choose **Node.js** as your **Backend language**.</span></span>
<span data-ttu-id="df8a6-167">Установите флажок "hello" для "**я подтверждаю, что это перезапишет все содержимое сайта.**«, нажмите кнопку **таблицы TodoItem создания**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-167">Check hello box for "**I acknowledge that this will overwrite all site contents.**", then click **Create TodoItem table**.</span></span>

### <span data-ttu-id="df8a6-168"><a name="download-quickstart"></a>Как: загрузки hello Node.js серверной быстрый запуск проекта кода с помощью Git</span><span class="sxs-lookup"><span data-stu-id="df8a6-168"><a name="download-quickstart"></a>How to: Download hello Node.js backend quickstart code project using Git</span></span>
<span data-ttu-id="df8a6-169">При создании серверной части Node.js мобильное приложение с помощью портала hello **краткого** колонке Node.js проект создается для вас и развернутых tooyour сайта.</span><span class="sxs-lookup"><span data-stu-id="df8a6-169">When you create a Node.js Mobile App backend by using hello portal **Quick start** blade, a Node.js project is created for you and deployed tooyour site.</span></span> <span data-ttu-id="df8a6-170">Можно добавлять таблицы и API-интерфейсы и изменять файлы кода для серверной части Node.js hello в портал hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-170">You can add tables and APIs and edit code files for hello Node.js backend in hello portal.</span></span> <span data-ttu-id="df8a6-171">Также можно использовать различные развертывания средства toodownload hello серверного проекта, можно добавить или изменить таблицы и API-интерфейсы, а затем повторно опубликовать проект hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-171">You can also use various deployment tools toodownload hello backend project so that you can add or modify tables and APIs, then republish hello project.</span></span> <span data-ttu-id="df8a6-172">Дополнительные сведения см. в [руководстве по развертыванию службы приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="df8a6-172">For more information, see the [Azure App Service Deployment Guide].</span></span> <span data-ttu-id="df8a6-173">Hello следующая процедура использует код проекта Git репозитория toodownload hello краткое руководство.</span><span class="sxs-lookup"><span data-stu-id="df8a6-173">hello following procedure uses a Git repository toodownload hello quickstart project code.</span></span>

1. <span data-ttu-id="df8a6-174">Установите Git, если его у вас еще нет.</span><span class="sxs-lookup"><span data-stu-id="df8a6-174">Install Git, if you haven't already done so.</span></span> <span data-ttu-id="df8a6-175">tooinstall необходимые шаги Hello Git различаться для разных операционных систем.</span><span class="sxs-lookup"><span data-stu-id="df8a6-175">hello steps required tooinstall Git vary between operating systems.</span></span> <span data-ttu-id="df8a6-176">Сведения о дистрибутивах для разных операционных систем и руководство по установке см. в разделе [Установка Git](http://git-scm.com/book/en/Getting-Started-Installing-Git).</span><span class="sxs-lookup"><span data-stu-id="df8a6-176">See [Installing Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) for operating system-specific distributions and installation guidance.</span></span>
2. <span data-ttu-id="df8a6-177">Следуйте указаниям hello [Enable hello репозитория приложения службы приложений](../app-service-web/app-service-deploy-local-git.md#Step3) tooenable hello репозитории для сайта серверной части, создания заметки из hello развертывания пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="df8a6-177">Follow hello steps in [Enable hello App Service app repository](../app-service-web/app-service-deploy-local-git.md#Step3) tooenable hello Git repository for your backend site, making a note of hello deployment username and password.</span></span>
3. <span data-ttu-id="df8a6-178">В колонке hello для серверной части мобильного приложения, запишите hello **URL-адрес клона Git** параметр.</span><span class="sxs-lookup"><span data-stu-id="df8a6-178">In hello blade for your Mobile App backend, make a note of hello **Git clone URL** setting.</span></span>
4. <span data-ttu-id="df8a6-179">Выполнение hello `git clone` hello Git URL-адрес клона, ввода пароля при необходимости, как показано в следующем примере с помощью команды:</span><span class="sxs-lookup"><span data-stu-id="df8a6-179">Execute hello `git clone` command using hello Git clone URL, entering your password when required, as in the following example:</span></span>

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. <span data-ttu-id="df8a6-180">Обзор toolocal каталога, в предыдущих пример hello /todolist и обратите внимание, что файлы проекта были загружены.</span><span class="sxs-lookup"><span data-stu-id="df8a6-180">Browse toolocal directory, which in hello preceding example is /todolist, and notice that project files have been downloaded.</span></span> <span data-ttu-id="df8a6-181">Найдите hello `todoitem.json` файла в hello `/tables` каталога.</span><span class="sxs-lookup"><span data-stu-id="df8a6-181">Locate hello `todoitem.json` file in hello `/tables` directory.</span></span>  <span data-ttu-id="df8a6-182">Этот файл определяет разрешения для таблицы.</span><span class="sxs-lookup"><span data-stu-id="df8a6-182">This file defines permissions on the table.</span></span>  <span data-ttu-id="df8a6-183">Также найти hello `todoitem.js` файл hello же каталог, который определяет, что операции CRUD скрипты для таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-183">Also find hello `todoitem.js` file in hello same directory, which defines that CRUD operation scripts for hello table.</span></span>
6. <span data-ttu-id="df8a6-184">После внесения изменений tooproject файлы, выполните следующие команды tooadd, commit, а затем отправить изменения сайта toohello hello:</span><span class="sxs-lookup"><span data-stu-id="df8a6-184">After you have made changes tooproject files, execute hello following commands tooadd, commit, then upload the changes toohello site:</span></span>

        $ git commit -m "updated hello table script"
        $ git push origin master

    <span data-ttu-id="df8a6-185">При добавлении нового проекта toohello файлы, необходимо сначала tooexecute hello `git add .` команды.</span><span class="sxs-lookup"><span data-stu-id="df8a6-185">When you add new files toohello project, you first need tooexecute hello `git add .` command.</span></span>

<span data-ttu-id="df8a6-186">Каждый раз, новый набор фиксаций помещается toohello сайта повторно публикуется Hello сайта.</span><span class="sxs-lookup"><span data-stu-id="df8a6-186">hello site is republished every time a new set of commits is pushed toohello site.</span></span>

### <span data-ttu-id="df8a6-187"><a name="howto-publish-to-azure"></a>Как: публикация вашего tooAzure серверной Node.js</span><span class="sxs-lookup"><span data-stu-id="df8a6-187"><a name="howto-publish-to-azure"></a>How to: Publish your Node.js backend tooAzure</span></span>
<span data-ttu-id="df8a6-188">Microsoft Azure предоставляет много механизмов публикации Azure приложение службы мобильных приложений Node.js серверной части для hello службы Azure.</span><span class="sxs-lookup"><span data-stu-id="df8a6-188">Microsoft Azure provides many mechanisms for publishing your Azure App Service Mobile Apps Node.js backend to hello Azure service.</span></span>  <span data-ttu-id="df8a6-189">К ним относятся инструменты развертывания, интегрированные в Visual Studio, программы командной строки и средства непрерывного развертывания на основе системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="df8a6-189">These include utilizing deployment tools integrated into Visual Studio, command-line tools, and continuous deployment options based on source control.</span></span>  <span data-ttu-id="df8a6-190">Дополнительные сведения по этой теме см. в [руководстве по развертыванию службы приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="df8a6-190">For more information on this topic, see the [Azure App Service Deployment Guide].</span></span>

<span data-ttu-id="df8a6-191">В отношении приложений на Node.js в службе приложений Azure существуют четкие рекомендации, с которыми вам следует ознакомиться перед развертыванием:</span><span class="sxs-lookup"><span data-stu-id="df8a6-191">Azure App Service has specific advice for Node.js application that you should review before deploying:</span></span>

* <span data-ttu-id="df8a6-192">Как слишком[укажите hello версия узла]</span><span class="sxs-lookup"><span data-stu-id="df8a6-192">How too[specify hello Node Version]</span></span>
* <span data-ttu-id="df8a6-193">Как слишком[используйте модули узла]</span><span class="sxs-lookup"><span data-stu-id="df8a6-193">How too[use Node modules]</span></span>

### <span data-ttu-id="df8a6-194"><a name="howto-enable-homepage"></a>Практическое руководство. Включение домашней страницы для приложения</span><span class="sxs-lookup"><span data-stu-id="df8a6-194"><a name="howto-enable-homepage"></a>How to: Enable a Home Page for your application</span></span>
<span data-ttu-id="df8a6-195">Многие приложения представляют собой сочетание веб- и мобильных приложений и hello ExpressJS framework позволяет toocombine двух аспектов.</span><span class="sxs-lookup"><span data-stu-id="df8a6-195">Many applications are a combination of web and mobile apps and hello ExpressJS framework allows you toocombine the two facets.</span></span>  <span data-ttu-id="df8a6-196">Иногда тем не менее, вы можете реализовать tooonly мобильных интерфейса.</span><span class="sxs-lookup"><span data-stu-id="df8a6-196">Sometimes, however, you may wish tooonly implement a mobile interface.</span></span>  <span data-ttu-id="df8a6-197">Это полезно tooprovide службы стартовой страницы tooensure hello приложений является запущен и работает.</span><span class="sxs-lookup"><span data-stu-id="df8a6-197">It is useful tooprovide a landing page tooensure hello app service is up and running.</span></span>  <span data-ttu-id="df8a6-198">Можно указать свою домашнюю страницу или включить временную.</span><span class="sxs-lookup"><span data-stu-id="df8a6-198">You can either provide your own home page or enable a temporary home page.</span></span>  <span data-ttu-id="df8a6-199">tooenable временные домашней страницы, используйте следующие мобильные приложения Azure tooinstantiate hello:</span><span class="sxs-lookup"><span data-stu-id="df8a6-199">tooenable a temporary home page, use hello following tooinstantiate Azure Mobile Apps:</span></span>

    var mobile = azureMobileApps({ homePage: true });

<span data-ttu-id="df8a6-200">Если требуется только этот параметр доступен при разработке локально, можно добавить этот параметр tooyour `azureMobile.js` файл.</span><span class="sxs-lookup"><span data-stu-id="df8a6-200">If you only want this option available when developing locally, you can add this setting tooyour `azureMobile.js` file.</span></span>

## <span data-ttu-id="df8a6-201"><a name="TableOperations"></a>Операции с таблицами</span><span class="sxs-lookup"><span data-stu-id="df8a6-201"><a name="TableOperations"></a>Table operations</span></span>
<span data-ttu-id="df8a6-202">Hello Server Node.js мобильных приложений azure SDK предоставляет механизмы tooexpose данные таблиц, сохраненных в базе данных SQL Azure с WebAPI.</span><span class="sxs-lookup"><span data-stu-id="df8a6-202">hello azure-mobile-apps Node.js Server SDK provides mechanisms tooexpose data tables stored in Azure SQL Database as a WebAPI.</span></span>  <span data-ttu-id="df8a6-203">Пакетом предоставляются пять операций.</span><span class="sxs-lookup"><span data-stu-id="df8a6-203">Five operations are provided.</span></span>

| <span data-ttu-id="df8a6-204">Операция</span><span class="sxs-lookup"><span data-stu-id="df8a6-204">Operation</span></span> | <span data-ttu-id="df8a6-205">Описание</span><span class="sxs-lookup"><span data-stu-id="df8a6-205">Description</span></span> |
| --- | --- |
| <span data-ttu-id="df8a6-206">GET /tables/*имя_таблицы*</span><span class="sxs-lookup"><span data-stu-id="df8a6-206">GET /tables/*tablename*</span></span> |<span data-ttu-id="df8a6-207">Получить все записи в таблице hello</span><span class="sxs-lookup"><span data-stu-id="df8a6-207">Get all records in hello table</span></span> |
| <span data-ttu-id="df8a6-208">GET /tables/*имя_таблицы*/:id</span><span class="sxs-lookup"><span data-stu-id="df8a6-208">GET /tables/*tablename*/:id</span></span> |<span data-ttu-id="df8a6-209">Получить конкретную запись в таблице hello</span><span class="sxs-lookup"><span data-stu-id="df8a6-209">Get a specific record in hello table</span></span> |
| <span data-ttu-id="df8a6-210">POST /tables/*имя_таблицы*</span><span class="sxs-lookup"><span data-stu-id="df8a6-210">POST /tables/*tablename*</span></span> |<span data-ttu-id="df8a6-211">Создайте запись в таблице hello</span><span class="sxs-lookup"><span data-stu-id="df8a6-211">Create a record in hello table</span></span> |
| <span data-ttu-id="df8a6-212">PATCH /tables/*имя_таблицы*/:id</span><span class="sxs-lookup"><span data-stu-id="df8a6-212">PATCH /tables/*tablename*/:id</span></span> |<span data-ttu-id="df8a6-213">Обновить запись в таблице hello</span><span class="sxs-lookup"><span data-stu-id="df8a6-213">Update a record in hello table</span></span> |
| <span data-ttu-id="df8a6-214">DELETE /tables/*имя_таблицы*/:id</span><span class="sxs-lookup"><span data-stu-id="df8a6-214">DELETE /tables/*tablename*/:id</span></span> |<span data-ttu-id="df8a6-215">Удаление записи в таблице hello</span><span class="sxs-lookup"><span data-stu-id="df8a6-215">Delete a record in hello table</span></span> |

<span data-ttu-id="df8a6-216">Поддерживает этот WebAPI [OData] и расширяет возможности hello таблицы схемы toosupport [автономные данные синхронизации].</span><span class="sxs-lookup"><span data-stu-id="df8a6-216">This WebAPI supports [OData] and extends hello table schema toosupport [offline data sync].</span></span>

### <span data-ttu-id="df8a6-217"><a name="howto-dynamicschema"></a>Определение таблиц с помощью динамической схемы</span><span class="sxs-lookup"><span data-stu-id="df8a6-217"><a name="howto-dynamicschema"></a>How to: Define tables using a dynamic schema</span></span>
<span data-ttu-id="df8a6-218">Перед использованием таблицы ее необходимо определить.</span><span class="sxs-lookup"><span data-stu-id="df8a6-218">Before a table can be used, it must be defined.</span></span>  <span data-ttu-id="df8a6-219">Таблицы можно определить с помощью статического схемы (где hello разработчик определяет столбцы hello в схеме hello) или динамически (где hello SDK управляет hello схему, основанную на входящие запросы).</span><span class="sxs-lookup"><span data-stu-id="df8a6-219">Tables can be defined with a static schema (where hello developer defines hello columns within hello schema) or dynamically (where hello SDK controls hello schema based on incoming requests).</span></span> <span data-ttu-id="df8a6-220">Кроме того разработчик hello можно настроить определенные аспекты hello WebAPI, добавив определение toohello кода Javascript.</span><span class="sxs-lookup"><span data-stu-id="df8a6-220">In addition, hello developer can control specific aspects of hello WebAPI by adding Javascript code toohello definition.</span></span>

<span data-ttu-id="df8a6-221">Рекомендуется следует определить каждой таблицы в файл Javascript в каталоге hello таблиц, то использовать tooimport hello tables.import() метод таблиц.</span><span class="sxs-lookup"><span data-stu-id="df8a6-221">As a best practice, you should define each table in a Javascript file in hello tables directory, then use the tables.import() method tooimport hello tables.</span></span>  <span data-ttu-id="df8a6-222">Расширение basic приложение hello, hello в файле app.js файл будет настраиваться:</span><span class="sxs-lookup"><span data-stu-id="df8a6-222">Extending hello basic-app, hello app.js file would be adjusted:</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define hello database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

<span data-ttu-id="df8a6-223">Определите таблицу hello в. / tables/TodoItem.js:</span><span class="sxs-lookup"><span data-stu-id="df8a6-223">Define hello table in ./tables/TodoItem.js:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for hello table goes here

    module.exports = table;

<span data-ttu-id="df8a6-224">По умолчанию в таблицах используется динамическая схема.</span><span class="sxs-lookup"><span data-stu-id="df8a6-224">Tables use dynamic schema by default.</span></span>  <span data-ttu-id="df8a6-225">tooturn отключение динамической схемы глобально, задайте параметр приложения hello **MS_DynamicSchema** toofalse внутри hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="df8a6-225">tooturn off dynamic schema globally, set hello App Setting **MS_DynamicSchema** toofalse within hello Azure portal.</span></span>

<span data-ttu-id="df8a6-226">Полный пример можно найти в hello [пример todo на GitHub].</span><span class="sxs-lookup"><span data-stu-id="df8a6-226">You can find a complete example in hello [todo sample on GitHub].</span></span>

### <span data-ttu-id="df8a6-227"><a name="howto-staticschema"></a>Определение таблиц с помощью статической схемы</span><span class="sxs-lookup"><span data-stu-id="df8a6-227"><a name="howto-staticschema"></a>How to: Define tables using a static schema</span></span>
<span data-ttu-id="df8a6-228">Можно явно определять tooexpose столбцы hello через hello WebAPI.</span><span class="sxs-lookup"><span data-stu-id="df8a6-228">You can explicitly define hello columns tooexpose via hello WebAPI.</span></span>  <span data-ttu-id="df8a6-229">пакет SDK для Node.js мобильных приложений azure автоматически добавляет все дополнительные столбцы, необходимые для toohello список автономные данные синхронизации, который предоставляется Hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-229">hello azure-mobile-apps Node.js SDK automatically adds any additional columns required for offline data sync toohello list that you provide.</span></span>  <span data-ttu-id="df8a6-230">Например, в примерах клиентских приложений требуется таблица с двумя столбцами: text (строка) и завершения complete (логическое значение).</span><span class="sxs-lookup"><span data-stu-id="df8a6-230">For example, the QuickStart client applications require a table with two columns: text (a string) and complete (a boolean).</span></span>  
<span data-ttu-id="df8a6-231">Hello таблицы могут быть определены в hello таблицы определение файл JavaScript (расположен в каталоге hello таблиц) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="df8a6-231">hello table can be defined in hello table definition JavaScript file (located in hello tables directory) as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

<span data-ttu-id="df8a6-232">Если статически определить таблицы, затем необходимо также вызвать hello hello tables.initialize() метод toocreate схемы базы данных во время запуска.</span><span class="sxs-lookup"><span data-stu-id="df8a6-232">If you define tables statically, then you must also call hello tables.initialize() method toocreate hello database schema on startup.</span></span>  <span data-ttu-id="df8a6-233">Возвращает метод Hello tables.initialize() [Promise] , чтобы не обрабатывать запросы до инициализации базы данных hello, hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="df8a6-233">hello tables.initialize() method returns a [Promise] so that hello web service does not serve requests before hello database being initialized.</span></span>

### <span data-ttu-id="df8a6-234"><a name="howto-sqlexpress-setup"></a>Использование SQL Express в качестве хранилища данных при разработке на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="df8a6-234"><a name="howto-sqlexpress-setup"></a>How to: Use SQL Express as a development data store on your local machine</span></span>
<span data-ttu-id="df8a6-235">Hello hello мобильных приложений Azure SDK узел AzureMobile приложений предоставляют три параметра для обслуживания данных стандартной hello: пакет SDK предоставляет три варианта для обслуживания данных стандартной hello:</span><span class="sxs-lookup"><span data-stu-id="df8a6-235">hello Azure Mobile Apps hello AzureMobile Apps Node SDK provides three options for serving data out of hello box: SDK provides three options for serving data out of hello box:</span></span>

* <span data-ttu-id="df8a6-236">Используйте hello **памяти** примере хранилище драйверов tooprovide не постоянно</span><span class="sxs-lookup"><span data-stu-id="df8a6-236">Use hello **memory** driver tooprovide a non-persistent example store</span></span>
* <span data-ttu-id="df8a6-237">Используйте hello **mssql** tooprovide драйвер хранилища данных SQL Express для разработки</span><span class="sxs-lookup"><span data-stu-id="df8a6-237">Use hello **mssql** driver tooprovide a SQL Express data store for development</span></span>
* <span data-ttu-id="df8a6-238">Используйте hello **mssql** драйвер tooprovide хранилище данных базы данных SQL Azure для рабочей среды</span><span class="sxs-lookup"><span data-stu-id="df8a6-238">Use hello **mssql** driver tooprovide an Azure SQL Database data store for production</span></span>

<span data-ttu-id="df8a6-239">Hello Azure мобильных приложений Node.js SDK использует hello [пакет Node.js mssql] tooestablish и использовать SQL Express tooboth подключения и базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="df8a6-239">hello Azure Mobile Apps Node.js SDK uses hello [mssql Node.js package] tooestablish and use a connection tooboth SQL Express and SQL Database.</span></span>  <span data-ttu-id="df8a6-240">Для использования этого пакета необходимо включить TCP-подключения в вашем экземпляре SQL Express.</span><span class="sxs-lookup"><span data-stu-id="df8a6-240">This package requires that you enable TCP connections on your SQL Express instance.</span></span>

> [!TIP]
> <span data-ttu-id="df8a6-241">Hello памяти драйвер не предоставляет полный набор средств для тестирования.</span><span class="sxs-lookup"><span data-stu-id="df8a6-241">hello memory driver does not provide a complete set of facilities for testing.</span></span>  <span data-ttu-id="df8a6-242">При желании tootest локально серверной части, рекомендуется использование hello в хранилище данных SQL Express и hello mssql драйвера.</span><span class="sxs-lookup"><span data-stu-id="df8a6-242">If you wish tootest your backend locally, we recommend hello use of a SQL Express data store and hello mssql driver.</span></span>
>
>

1. <span data-ttu-id="df8a6-243">Загрузите и установите [Microsoft SQL Server 2014 Express].</span><span class="sxs-lookup"><span data-stu-id="df8a6-243">Download and install [Microsoft SQL Server 2014 Express].</span></span>  <span data-ttu-id="df8a6-244">Убедитесь, что вы можете установить средства выпуска SQL Server 2014 Express hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-244">Ensure you install hello SQL Server 2014 Express with Tools edition.</span></span>  <span data-ttu-id="df8a6-245">Если не требуется поддержка 64-разрядных явно hello 32-разрядная версия потребляет меньше памяти при запуске.</span><span class="sxs-lookup"><span data-stu-id="df8a6-245">Unless you explicitly require 64-bit support, hello 32-bit version consumes less memory when running.</span></span>
2. <span data-ttu-id="df8a6-246">Запустите диспетчер конфигурации SQL Server 2014 hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-246">Run hello SQL Server 2014 Configuration Manager.</span></span>

   1. <span data-ttu-id="df8a6-247">Разверните hello **сетевая конфигурация SQL Server** узел в дереве слева меню hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-247">Expand hello **SQL Server Network Configuration** node in hello left-hand tree menu.</span></span>
   2. <span data-ttu-id="df8a6-248">Выберите **Протоколы для SQLEXPRESS**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-248">Click **Protocols for SQLEXPRESS**.</span></span>
   3. <span data-ttu-id="df8a6-249">Щелкните правой кнопкой мыши **TCP/IP** и выберите **Включить**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-249">Right-click **TCP/IP** and select **Enable**.</span></span>  <span data-ttu-id="df8a6-250">Нажмите кнопку **ОК** в всплывающем диалоговом окне приветствия.</span><span class="sxs-lookup"><span data-stu-id="df8a6-250">Click **OK** in hello pop-up dialog.</span></span>
   4. <span data-ttu-id="df8a6-251">Щелкните правой кнопкой мыши **TCP/IP** и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-251">Right-click **TCP/IP** and select **Properties**.</span></span>
   5. <span data-ttu-id="df8a6-252">Нажмите кнопку hello **IP-адреса** вкладки.</span><span class="sxs-lookup"><span data-stu-id="df8a6-252">Click hello **IP Addresses** tab.</span></span>
   6. <span data-ttu-id="df8a6-253">Найти hello **IPAll** узла.</span><span class="sxs-lookup"><span data-stu-id="df8a6-253">Find hello **IPAll** node.</span></span>  <span data-ttu-id="df8a6-254">В hello **TCP-порт** введите **1433**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-254">In hello **TCP Port** field, enter **1433**.</span></span>

          ![Configure SQL Express for TCP/IP][3]
   7. <span data-ttu-id="df8a6-255">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-255">Click **OK**.</span></span>  <span data-ttu-id="df8a6-256">Нажмите кнопку **ОК** в всплывающем диалоговом окне приветствия.</span><span class="sxs-lookup"><span data-stu-id="df8a6-256">Click **OK** in hello pop-up dialog.</span></span>
   8. <span data-ttu-id="df8a6-257">Нажмите кнопку **служб SQL Server** в левом дереве меню hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-257">Click **SQL Server Services** in hello left-hand tree menu.</span></span>
   9. <span data-ttu-id="df8a6-258">Щелкните правой кнопкой мыши **SQL Server (SQLEXPRESS)** и выберите **Перезапустить**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-258">Right-click **SQL Server (SQLEXPRESS)** and select **Restart**</span></span>
   10. <span data-ttu-id="df8a6-259">Закройте диспетчер конфигурации SQL Server 2014 hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-259">Close hello SQL Server 2014 Configuration Manager.</span></span>
3. <span data-ttu-id="df8a6-260">Запустите hello SQL Server 2014 Management Studio и подключитесь tooyour локальный экземпляр SQL Express</span><span class="sxs-lookup"><span data-stu-id="df8a6-260">Run hello SQL Server 2014 Management Studio and connect tooyour local SQL Express instance</span></span>

   1. <span data-ttu-id="df8a6-261">Щелкните правой кнопкой мыши в обозревателе объектов hello экземпляра и выберите **свойства**</span><span class="sxs-lookup"><span data-stu-id="df8a6-261">Right-click your instance in hello Object Explorer and select **Properties**</span></span>
   2. <span data-ttu-id="df8a6-262">Выберите hello **безопасности** страницы.</span><span class="sxs-lookup"><span data-stu-id="df8a6-262">Select hello **Security** page.</span></span>
   3. <span data-ttu-id="df8a6-263">Убедитесь, hello **режим SQL Server и проверка подлинности Windows** выбран</span><span class="sxs-lookup"><span data-stu-id="df8a6-263">Ensure hello **SQL Server and Windows Authentication mode** is selected</span></span>
   4. <span data-ttu-id="df8a6-264">Щелкните **ОК**</span><span class="sxs-lookup"><span data-stu-id="df8a6-264">Click **OK**</span></span>

          ![Configure SQL Express Authentication][4]
   5. <span data-ttu-id="df8a6-265">Разверните **безопасности** > **входа** в обозревателе объектов hello</span><span class="sxs-lookup"><span data-stu-id="df8a6-265">Expand **Security** > **Logins** in hello Object Explorer</span></span>
   6. <span data-ttu-id="df8a6-266">Щелкните правой кнопкой мыши пункт **Имена входа** и выберите **Создать имя входа**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-266">Right-click **Logins** and select **New Login...**</span></span>
   7. <span data-ttu-id="df8a6-267">Введите имя входа.</span><span class="sxs-lookup"><span data-stu-id="df8a6-267">Enter a Login name.</span></span>  <span data-ttu-id="df8a6-268">Выберите **Проверка подлинности SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-268">Select **SQL Server authentication**.</span></span>  <span data-ttu-id="df8a6-269">Введите пароль, а затем введите hello пароль еще раз в **подтверждение пароля**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-269">Enter a Password, then enter hello same password in **Confirm password**.</span></span>  <span data-ttu-id="df8a6-270">Hello пароль должен отвечать требованиям к сложности пароля Windows.</span><span class="sxs-lookup"><span data-stu-id="df8a6-270">hello password must meet Windows complexity requirements.</span></span>
   8. <span data-ttu-id="df8a6-271">Щелкните **ОК**</span><span class="sxs-lookup"><span data-stu-id="df8a6-271">Click **OK**</span></span>

          ![Add a new user tooSQL Express][5]
   9. <span data-ttu-id="df8a6-272">Щелкните правой кнопкой мыши новое имя для входа и выберите **Свойства**</span><span class="sxs-lookup"><span data-stu-id="df8a6-272">Right-click your new login and select **Properties**</span></span>
   10. <span data-ttu-id="df8a6-273">Выберите hello **ролей сервера** страницы</span><span class="sxs-lookup"><span data-stu-id="df8a6-273">Select hello **Server Roles** page</span></span>
   11. <span data-ttu-id="df8a6-274">Проверьте hello поле Далее toohello **dbcreator** роли сервера</span><span class="sxs-lookup"><span data-stu-id="df8a6-274">Check hello box next toohello **dbcreator** server role</span></span>
   12. <span data-ttu-id="df8a6-275">Щелкните **ОК**</span><span class="sxs-lookup"><span data-stu-id="df8a6-275">Click **OK**</span></span>
   13. <span data-ttu-id="df8a6-276">Закройте hello SQL Server 2015 Management Studio</span><span class="sxs-lookup"><span data-stu-id="df8a6-276">Close hello SQL Server 2015 Management Studio</span></span>

<span data-ttu-id="df8a6-277">Убедитесь, что записи hello пользователя и пароль, которые вы выбрали.</span><span class="sxs-lookup"><span data-stu-id="df8a6-277">Ensure you record hello username and password you selected.</span></span>  <span data-ttu-id="df8a6-278">Tooassign дополнительных ролей сервера или разрешений может потребоваться в зависимости от требований к определенной базе данных.</span><span class="sxs-lookup"><span data-stu-id="df8a6-278">You may need tooassign additional server roles or permissions depending on your specific database requirements.</span></span>

<span data-ttu-id="df8a6-279">Hello Node.js приложение считывает hello **SQLCONNSTR_MS_TableConnectionString** hello строку подключения для этой базы данных в переменной среды.</span><span class="sxs-lookup"><span data-stu-id="df8a6-279">hello Node.js application reads hello **SQLCONNSTR_MS_TableConnectionString** environment variable for hello connection string for this database.</span></span>  <span data-ttu-id="df8a6-280">Значение этой переменной можно задать непосредственно в своей среде.</span><span class="sxs-lookup"><span data-stu-id="df8a6-280">You can set this variable within your environment.</span></span>  <span data-ttu-id="df8a6-281">Например можно использовать PowerShell tooset этой переменной среды:</span><span class="sxs-lookup"><span data-stu-id="df8a6-281">For example, you can use PowerShell tooset this environment variable:</span></span>

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

<span data-ttu-id="df8a6-282">Доступ к базе данных hello через подключение TCP/IP и укажите имя пользователя и пароль для подключения hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-282">Access hello database through a TCP/IP connection and provide a username and password for hello connection.</span></span>

### <span data-ttu-id="df8a6-283"><a name="howto-config-localdev"></a>Настройка проекта для локальной разработки</span><span class="sxs-lookup"><span data-stu-id="df8a6-283"><a name="howto-config-localdev"></a>How to: Configure your project for local development</span></span>
<span data-ttu-id="df8a6-284">Мобильные приложения Azure считывает файл JavaScript с именем *azureMobile.js* из локальной файловой системе hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-284">Azure Mobile Apps reads a JavaScript file called *azureMobile.js* from hello local filesystem.</span></span>  <span data-ttu-id="df8a6-285">Не использовать этот файл tooconfigure hello пакет SDK Azure Mobile приложения в рабочей среде — не использовать параметры приложения в hello [портал Azure] вместо него.</span><span class="sxs-lookup"><span data-stu-id="df8a6-285">Do not use this file tooconfigure hello Azure Mobile Apps SDK in production - use App Settings within hello [Azure portal] instead.</span></span>  <span data-ttu-id="df8a6-286">Hello *azureMobile.js* файла следует экспортировать объект конфигурации.</span><span class="sxs-lookup"><span data-stu-id="df8a6-286">hello *azureMobile.js* file should export a configuration object.</span></span>  <span data-ttu-id="df8a6-287">Hello наиболее распространенные следующие значения.</span><span class="sxs-lookup"><span data-stu-id="df8a6-287">hello most common settings are:</span></span>

* <span data-ttu-id="df8a6-288">Параметры базы данных</span><span class="sxs-lookup"><span data-stu-id="df8a6-288">Database Settings</span></span>
* <span data-ttu-id="df8a6-289">Параметры ведения журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="df8a6-289">Diagnostic Logging Settings</span></span>
* <span data-ttu-id="df8a6-290">Дополнительные параметры CORS</span><span class="sxs-lookup"><span data-stu-id="df8a6-290">Alternate CORS Settings</span></span>

<span data-ttu-id="df8a6-291">Пример *azureMobile.js* файла реализации hello перед следующим параметры базы данных:</span><span class="sxs-lookup"><span data-stu-id="df8a6-291">An example *azureMobile.js* file implementing hello preceding database settings follows:</span></span>

    module.exports = {
        cors: {
            origins: [ 'localhost' ]
        },
        data: {
            provider: 'mssql',
            server: '127.0.0.1',
            database: 'mytestdatabase',
            user: 'azuremobile',
            password: 'T3stPa55word'
        },
        logging: {
            level: 'verbose'
        }
    };

<span data-ttu-id="df8a6-292">Мы рекомендуем добавить *azureMobile.js* tooyour *.gitignore* файла (или другие системы управления исходным кодом Пропуск файла) tooprevent паролей, хранящихся в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-292">We recommend that you add *azureMobile.js* tooyour *.gitignore* file (or other source code control ignore file) tooprevent passwords from being stored in hello cloud.</span></span>  <span data-ttu-id="df8a6-293">Всегда настраивайте параметры производства в параметрах приложения внутри hello [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="df8a6-293">Always configure production settings in App Settings within hello [Azure portal].</span></span>

### <span data-ttu-id="df8a6-294"><a name="howto-appsettings"></a>Практическое руководство. Настройка параметров для мобильного приложения</span><span class="sxs-lookup"><span data-stu-id="df8a6-294"><a name="howto-appsettings"></a>How: Configure App Settings for your Mobile App</span></span>
<span data-ttu-id="df8a6-295">Большинство параметров в hello *azureMobile.js* файла у него эквивалентные настройки приложения в hello [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="df8a6-295">Most settings in hello *azureMobile.js* file have an equivalent App Setting in hello [Azure portal].</span></span>  <span data-ttu-id="df8a6-296">Используйте следующий список tooconfigure hello приложения в параметрах приложения:</span><span class="sxs-lookup"><span data-stu-id="df8a6-296">Use hello following list tooconfigure your app in App Settings:</span></span>

| <span data-ttu-id="df8a6-297">Параметр приложения</span><span class="sxs-lookup"><span data-stu-id="df8a6-297">App Setting</span></span> | <span data-ttu-id="df8a6-298">*azureMobile.js* </span><span class="sxs-lookup"><span data-stu-id="df8a6-298">*azureMobile.js* Setting</span></span> | <span data-ttu-id="df8a6-299">Описание</span><span class="sxs-lookup"><span data-stu-id="df8a6-299">Description</span></span> | <span data-ttu-id="df8a6-300">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="df8a6-300">Valid Values</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df8a6-301">**MS_MobileAppName**</span><span class="sxs-lookup"><span data-stu-id="df8a6-301">**MS_MobileAppName**</span></span> |<span data-ttu-id="df8a6-302">name</span><span class="sxs-lookup"><span data-stu-id="df8a6-302">name</span></span> |<span data-ttu-id="df8a6-303">Имя Hello приложение hello</span><span class="sxs-lookup"><span data-stu-id="df8a6-303">hello name of hello app</span></span> |<span data-ttu-id="df8a6-304">string</span><span class="sxs-lookup"><span data-stu-id="df8a6-304">string</span></span> |
| <span data-ttu-id="df8a6-305">**MS_MobileLoggingLevel**</span><span class="sxs-lookup"><span data-stu-id="df8a6-305">**MS_MobileLoggingLevel**</span></span> |<span data-ttu-id="df8a6-306">logging.level</span><span class="sxs-lookup"><span data-stu-id="df8a6-306">logging.level</span></span> |<span data-ttu-id="df8a6-307">Минимальный уровень toolog сообщений</span><span class="sxs-lookup"><span data-stu-id="df8a6-307">Minimum log level of messages toolog</span></span> |<span data-ttu-id="df8a6-308">error, warning, info, verbose, debug, silly</span><span class="sxs-lookup"><span data-stu-id="df8a6-308">error, warning, info, verbose, debug, silly</span></span> |
| <span data-ttu-id="df8a6-309">**MS_DebugMode**</span><span class="sxs-lookup"><span data-stu-id="df8a6-309">**MS_DebugMode**</span></span> |<span data-ttu-id="df8a6-310">debug</span><span class="sxs-lookup"><span data-stu-id="df8a6-310">debug</span></span> |<span data-ttu-id="df8a6-311">Включение или отключение режима отладки</span><span class="sxs-lookup"><span data-stu-id="df8a6-311">Enable or Disable debug mode</span></span> |<span data-ttu-id="df8a6-312">true, false</span><span class="sxs-lookup"><span data-stu-id="df8a6-312">true, false</span></span> |
| <span data-ttu-id="df8a6-313">**MS_TableSchema**</span><span class="sxs-lookup"><span data-stu-id="df8a6-313">**MS_TableSchema**</span></span> |<span data-ttu-id="df8a6-314">data.schema</span><span class="sxs-lookup"><span data-stu-id="df8a6-314">data.schema</span></span> |<span data-ttu-id="df8a6-315">Имя схемы по умолчанию для таблиц SQL</span><span class="sxs-lookup"><span data-stu-id="df8a6-315">Default schema name for SQL tables</span></span> |<span data-ttu-id="df8a6-316">строка (значение по умолчанию: dbo)</span><span class="sxs-lookup"><span data-stu-id="df8a6-316">string (default: dbo)</span></span> |
| <span data-ttu-id="df8a6-317">**MS_DynamicSchema**</span><span class="sxs-lookup"><span data-stu-id="df8a6-317">**MS_DynamicSchema**</span></span> |<span data-ttu-id="df8a6-318">data.dynamicSchema</span><span class="sxs-lookup"><span data-stu-id="df8a6-318">data.dynamicSchema</span></span> |<span data-ttu-id="df8a6-319">Включение или отключение режима отладки</span><span class="sxs-lookup"><span data-stu-id="df8a6-319">Enable or Disable debug mode</span></span> |<span data-ttu-id="df8a6-320">true, false</span><span class="sxs-lookup"><span data-stu-id="df8a6-320">true, false</span></span> |
| <span data-ttu-id="df8a6-321">**MS_DisableVersionHeader**</span><span class="sxs-lookup"><span data-stu-id="df8a6-321">**MS_DisableVersionHeader**</span></span> |<span data-ttu-id="df8a6-322">версия (набор tooundefined)</span><span class="sxs-lookup"><span data-stu-id="df8a6-322">version (set tooundefined)</span></span> |<span data-ttu-id="df8a6-323">Отключает заголовок X-ZUMO-Server-Version hello</span><span class="sxs-lookup"><span data-stu-id="df8a6-323">Disables hello X-ZUMO-Server-Version header</span></span> |<span data-ttu-id="df8a6-324">true, false</span><span class="sxs-lookup"><span data-stu-id="df8a6-324">true, false</span></span> |
| <span data-ttu-id="df8a6-325">**MS_SkipVersionCheck**</span><span class="sxs-lookup"><span data-stu-id="df8a6-325">**MS_SkipVersionCheck**</span></span> |<span data-ttu-id="df8a6-326">skipversioncheck</span><span class="sxs-lookup"><span data-stu-id="df8a6-326">skipversioncheck</span></span> |<span data-ttu-id="df8a6-327">Отключает проверку версии hello API клиента</span><span class="sxs-lookup"><span data-stu-id="df8a6-327">Disables hello client API version check</span></span> |<span data-ttu-id="df8a6-328">true, false</span><span class="sxs-lookup"><span data-stu-id="df8a6-328">true, false</span></span> |

<span data-ttu-id="df8a6-329">tooset Настройка приложения:</span><span class="sxs-lookup"><span data-stu-id="df8a6-329">tooset an App Setting:</span></span>

1. <span data-ttu-id="df8a6-330">Войдите в toohello [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="df8a6-330">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="df8a6-331">Выберите **все ресурсы** или **службы приложений** щелкните имя мобильного приложения hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-331">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="df8a6-332">по умолчанию открывается колонку параметров Hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-332">hello Settings blade opens by default.</span></span> <span data-ttu-id="df8a6-333">В противном случае щелкните **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-333">If it doesn't, click **Settings**.</span></span>
4. <span data-ttu-id="df8a6-334">Нажмите кнопку **параметры приложения** в меню "Разное" hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-334">Click **Application settings** in hello GENERAL menu.</span></span>
5. <span data-ttu-id="df8a6-335">Прокрутите toohello раздел параметров приложения.</span><span class="sxs-lookup"><span data-stu-id="df8a6-335">Scroll toohello App Settings section.</span></span>
6. <span data-ttu-id="df8a6-336">Если приложение уже существует, щелкните значение hello значение hello tooedit параметра приложения hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-336">If your app setting already exists, click hello value of hello app setting tooedit hello value.</span></span>
7. <span data-ttu-id="df8a6-337">При настройке приложения не существует, введите параметр приложения hello в hello ключ и значение hello в окне значение hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-337">If your app setting does not exist, enter hello App Setting in hello Key box and hello value in hello Value box.</span></span>
8. <span data-ttu-id="df8a6-338">После завершения нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-338">Once you are complete, click **Save**.</span></span>

<span data-ttu-id="df8a6-339">Для большинства параметров после внесения изменений потребуется перезапустить службу.</span><span class="sxs-lookup"><span data-stu-id="df8a6-339">Changing most app settings requires a service restart.</span></span>

### <span data-ttu-id="df8a6-340"><a name="howto-use-sqlazure"></a>Практическое руководство. Использование базы данных SQL для хранения данных в рабочей среде</span><span class="sxs-lookup"><span data-stu-id="df8a6-340"><a name="howto-use-sqlazure"></a>How to: Use SQL Database as your production data store</span></span>
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

<span data-ttu-id="df8a6-341">Порядок использования базы данных SQL в качестве хранилища данных идентичен для всех типов приложений службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="df8a6-341">Using Azure SQL Database as a data store is identical across all Azure App Service application types.</span></span> <span data-ttu-id="df8a6-342">Если вы еще не сделали этого, выполните эти шаги toocreate серверной мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="df8a6-342">If you have not done so already, follow these steps toocreate a Mobile App backend.</span></span>

1. <span data-ttu-id="df8a6-343">Войдите в toohello [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="df8a6-343">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="df8a6-344">В hello верхнего левого угла окна hello, щелкнув hello **+ создать** кнопку > **Интернет + мобильные устройства** > **мобильное приложение**, затем введите имя для мобильного приложения серверной части.</span><span class="sxs-lookup"><span data-stu-id="df8a6-344">In hello top left of hello window, click hello **+NEW** button > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="df8a6-345">В hello **группы ресурсов** введите hello точно такое же имя в качестве приложения.</span><span class="sxs-lookup"><span data-stu-id="df8a6-345">In hello **Resource Group** box, enter hello same name as your app.</span></span>
4. <span data-ttu-id="df8a6-346">выбран план службы приложений по умолчанию Hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-346">hello Default App Service plan is selected.</span></span>  <span data-ttu-id="df8a6-347">Если вы хотите toochange плана служб приложений, это можно сделать, щелкнув hello план обслуживания приложений > **+ создать**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-347">If you wish toochange your App Service plan, you can do so by clicking hello App Service Plan > **+ Create New**.</span></span>  <span data-ttu-id="df8a6-348">Введите имя нового плана служб приложений hello и выберите подходящее расположение.</span><span class="sxs-lookup"><span data-stu-id="df8a6-348">Provide a name of hello new App Service plan and select an appropriate location.</span></span>  <span data-ttu-id="df8a6-349">Щелкните hello Ценовая категория и выберите соответствующий ценовую категорию для службы hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-349">Click hello Pricing tier and select an appropriate pricing tier for hello service.</span></span> <span data-ttu-id="df8a6-350">Выберите **просмотреть все** tooview более цены параметры, такие как **Free** и **Shared**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-350">Select **View all** tooview more pricing options, such as **Free** and **Shared**.</span></span>  <span data-ttu-id="df8a6-351">После выбора ценовой категории, нажмите кнопку hello **выберите** кнопки.</span><span class="sxs-lookup"><span data-stu-id="df8a6-351">Once you have selected the pricing tier, click hello **Select** button.</span></span>  <span data-ttu-id="df8a6-352">В hello **план служб приложений** колонка, щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-352">Back in hello **App Service plan** blade, click **OK**.</span></span>
5. <span data-ttu-id="df8a6-353">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-353">Click **Create**.</span></span> <span data-ttu-id="df8a6-354">Подготовка серверной части мобильного приложения может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="df8a6-354">Provisioning a Mobile App backend can take a couple of minutes.</span></span>  <span data-ttu-id="df8a6-355">После подготовки внутреннего сервера мобильного приложения hello hello портал открывает hello **параметры** колонку для внутреннего мобильное приложение hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-355">Once hello Mobile App backend is provisioned, hello portal opens hello **Settings** blade for hello Mobile App backend.</span></span>

<span data-ttu-id="df8a6-356">После создания внутреннего сервера мобильного приложения hello, вы можете tooeither подключение существующей серверной части SQL базы данных tooyour мобильное приложение или создание новой базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="df8a6-356">Once hello Mobile App backend is created, you can choose tooeither connect an existing SQL database tooyour Mobile App backend or create a new SQL database.</span></span>  <span data-ttu-id="df8a6-357">В этом разделе мы создадим базу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="df8a6-357">In this section, we create a SQL database.</span></span>

> [!NOTE]
> <span data-ttu-id="df8a6-358">Если уже имеется база данных в hello местоположения внутреннего сервера мобильного приложения hello, вместо этого можно **базы данных** и выберите эту базу данных.</span><span class="sxs-lookup"><span data-stu-id="df8a6-358">If you already have a database in hello same location as hello mobile app backend, you can instead choose **Use an existing database** and then select that database.</span></span> <span data-ttu-id="df8a6-359">Использование базы данных в другом месте Hello не рекомендуется из-за большей задержкой.</span><span class="sxs-lookup"><span data-stu-id="df8a6-359">hello use of a database in a different location is not recommended because of higher latencies.</span></span>
>
>

1. <span data-ttu-id="df8a6-360">В hello новую серверную часть мобильное приложение, нажмите кнопку **параметры** > **мобильное приложение** > **данные** > **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-360">In hello new Mobile App backend, click **Settings** > **Mobile App** > **Data** > **+Add**.</span></span>
2. <span data-ttu-id="df8a6-361">В hello **добавить подключение к данным** колонка, щелкните **базы данных SQL — необходимые настройки** > **создать новую базу данных**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-361">In hello **Add data connection** blade, click **SQL Database - Configure required settings** > **Create a new database**.</span></span>  <span data-ttu-id="df8a6-362">Введите имя новой базы данных hello hello в hello **имя** поля.</span><span class="sxs-lookup"><span data-stu-id="df8a6-362">Enter hello name of hello new database in hello **Name** field.</span></span>
3. <span data-ttu-id="df8a6-363">Щелкните **Сервер**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-363">Click **Server**.</span></span>  <span data-ttu-id="df8a6-364">В hello **новый сервер** колонки, введите имя сервера, уникальный в hello **имя сервера** , а укажите подходящего **имя входа администратора сервера** и **пароля**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-364">In hello **New server** blade, enter a unique server name in hello **Server name** field, and provide a suitable **Server admin login** and **Password**.</span></span>  <span data-ttu-id="df8a6-365">Убедитесь, **tooaccess сервера разрешить службам azure** проверяется.</span><span class="sxs-lookup"><span data-stu-id="df8a6-365">Ensure **Allow azure services tooaccess server** is checked.</span></span>  <span data-ttu-id="df8a6-366">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-366">Click **OK**.</span></span>

    ![Создание базы данных SQL Azure][6]
4. <span data-ttu-id="df8a6-368">На hello **новую базу данных** колонка, щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-368">On hello **New database** blade, click **OK**.</span></span>
5. <span data-ttu-id="df8a6-369">Включите hello **добавить подключение к данным** колонке выберите **строка подключения**, введите hello входа и пароль, предоставленный при создании базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-369">Back on hello **Add data connection** blade, select **Connection string**, enter hello login and password that you provided when creating hello database.</span></span>  <span data-ttu-id="df8a6-370">При использовании существующей базы данных, укажите учетные данные входа hello для этой базы данных.</span><span class="sxs-lookup"><span data-stu-id="df8a6-370">If you use an existing database, provide hello login credentials for that database.</span></span>  <span data-ttu-id="df8a6-371">Выполнив вход, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-371">Once entered, click **OK**.</span></span>
6. <span data-ttu-id="df8a6-372">Включите hello **добавить подключение к данным** колонке снова нажмите **ОК** базы данных toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-372">Back on hello **Add data connection** blade again, click **OK** toocreate hello database.</span></span>

<!--- END OF ALTERNATE INCLUDE -->

<span data-ttu-id="df8a6-373">Создание hello базы данных может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="df8a6-373">Creation of hello database can take a few minutes.</span></span>  <span data-ttu-id="df8a6-374">Используйте hello **уведомления** области toomonitor hello ход выполнения развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-374">Use hello **Notifications** area toomonitor hello progress of hello deployment.</span></span>  <span data-ttu-id="df8a6-375">Невыполнение пока будет успешно развернут hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="df8a6-375">Do not progress until hello database has been deployed successfully.</span></span>  <span data-ttu-id="df8a6-376">После успешного развертывания для hello экземпляр базы данных SQL в серверной части мобильных параметры приложения создается строка подключения.</span><span class="sxs-lookup"><span data-stu-id="df8a6-376">Once successfully deployed, a Connection String is created for hello SQL Database instance in your Mobile backend App Settings.</span></span>  <span data-ttu-id="df8a6-377">Вы увидите следующий параметр приложения в hello **параметры** > **параметры приложения** > **строки подключения**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-377">You can see this app setting in hello **Settings** > **Application settings** > **Connection strings**.</span></span>

### <span data-ttu-id="df8a6-378"><a name="howto-tables-auth"></a>Как: требуется проверка подлинности для доступа к tootables</span><span class="sxs-lookup"><span data-stu-id="df8a6-378"><a name="howto-tables-auth"></a>How to: Require authentication for access tootables</span></span>
<span data-ttu-id="df8a6-379">При желании toouse проверки подлинности приложения службы с конечной точкой hello таблиц необходимо настроить проверки подлинности службы приложения в hello [портал Azure] первой.</span><span class="sxs-lookup"><span data-stu-id="df8a6-379">If you wish toouse App Service Authentication with hello tables endpoint, you must configure App Service Authentication in hello [Azure portal] first.</span></span>  <span data-ttu-id="df8a6-380">Для hello руководство по конфигурации для поставщика удостоверений hello просмотрите дополнительные сведения о настройке проверки подлинности в службе приложений Azure, предполагается toouse:</span><span class="sxs-lookup"><span data-stu-id="df8a6-380">For more details about configuring authentication in an Azure App Service, review hello Configuration Guide for hello identity provider you intend toouse:</span></span>

* <span data-ttu-id="df8a6-381">[Как tooconfigure проверки подлинности Azure Active Directory]</span><span class="sxs-lookup"><span data-stu-id="df8a6-381">[How tooconfigure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="df8a6-382">[Как tooconfigure проверки подлинности Facebook]</span><span class="sxs-lookup"><span data-stu-id="df8a6-382">[How tooconfigure Facebook Authentication]</span></span>
* <span data-ttu-id="df8a6-383">[Как tooconfigure проверки подлинности Google]</span><span class="sxs-lookup"><span data-stu-id="df8a6-383">[How tooconfigure Google Authentication]</span></span>
* <span data-ttu-id="df8a6-384">[Как tooconfigure проверки подлинности Майкрософт]</span><span class="sxs-lookup"><span data-stu-id="df8a6-384">[How tooconfigure Microsoft Authentication]</span></span>
* <span data-ttu-id="df8a6-385">[Как tooconfigure проверки подлинности Twitter]</span><span class="sxs-lookup"><span data-stu-id="df8a6-385">[How tooconfigure Twitter Authentication]</span></span>

<span data-ttu-id="df8a6-386">Каждая таблица имеет свойства access, можно использовать toocontrol доступа toohello таблице.</span><span class="sxs-lookup"><span data-stu-id="df8a6-386">Each table has an access property that can be used toocontrol access toohello table.</span></span>  <span data-ttu-id="df8a6-387">Следующий образец Hello приводится статически определенный таблица с требуется проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="df8a6-387">hello following sample shows a statically defined table with authentication required.</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="df8a6-388">Hello доступа свойство может принимать одно из трех значений</span><span class="sxs-lookup"><span data-stu-id="df8a6-388">hello access property can take one of three values</span></span>

* <span data-ttu-id="df8a6-389">*анонимные* указывает, что клиентское приложение hello tooread данные без проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="df8a6-389">*anonymous* indicates that hello client application is allowed tooread data without authentication</span></span>
* <span data-ttu-id="df8a6-390">*Проверка подлинности* указывает, что клиентское приложение hello необходимо отправить токен проверки подлинности с запросом hello</span><span class="sxs-lookup"><span data-stu-id="df8a6-390">*authenticated* indicates that hello client application must send a valid authentication token with hello request</span></span>
* <span data-ttu-id="df8a6-391">*disabled* указывает, что эта таблица сейчас отключена.</span><span class="sxs-lookup"><span data-stu-id="df8a6-391">*disabled* indicates that this table is currently disabled</span></span>

<span data-ttu-id="df8a6-392">Если свойство доступа hello не определен, разрешен доступ без проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="df8a6-392">If hello access property is undefined, unauthenticated access is allowed.</span></span>

### <span data-ttu-id="df8a6-393"><a name="howto-tables-getidentity"></a>Практическое руководство. Использование утверждений аутентификации для таблиц</span><span class="sxs-lookup"><span data-stu-id="df8a6-393"><a name="howto-tables-getidentity"></a>How to: Use authentication claims with your tables</span></span>
<span data-ttu-id="df8a6-394">Можно настроить различные утверждения, запрашиваемые при настройке аутентификации.</span><span class="sxs-lookup"><span data-stu-id="df8a6-394">You can set up various claims that are requested when authentication is set up.</span></span>  <span data-ttu-id="df8a6-395">Эти утверждения не обычно доступны через hello `context.user` объекта.</span><span class="sxs-lookup"><span data-stu-id="df8a6-395">These claims are not normally available through hello `context.user` object.</span></span>  <span data-ttu-id="df8a6-396">Тем не менее, они могут быть получены с помощью hello `context.user.getIdentity()` метод.</span><span class="sxs-lookup"><span data-stu-id="df8a6-396">However, they can be retrieved using hello `context.user.getIdentity()` method.</span></span>  <span data-ttu-id="df8a6-397">Hello `getIdentity()` метод возвращает объект Promise, который разрешает tooan объект.</span><span class="sxs-lookup"><span data-stu-id="df8a6-397">hello `getIdentity()` method returns a Promise that resolves tooan object.</span></span>  <span data-ttu-id="df8a6-398">Hello объекта шифруется с помощью метода проверки подлинности (facebook, google, twitter, microsoftaccount или aad).</span><span class="sxs-lookup"><span data-stu-id="df8a6-398">hello object is keyed by the authentication method (facebook, google, twitter, microsoftaccount, or aad).</span></span>

<span data-ttu-id="df8a6-399">Например при настройке проверки подлинности учетной записи Майкрософт и утверждения адреса электронной почты hello запроса, можно добавить запись toohello адреса электронной почты hello с hello следующие таблицы контроллера:</span><span class="sxs-lookup"><span data-stu-id="df8a6-399">For example, if you set up Microsoft Account authentication and request hello email addresses claim, you can add hello email address toohello record with hello following table controller:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    // Create a new table definition
    var table = azureMobileApps.table();

    table.columns = {
        "emailAddress": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;
    table.access = 'authenticated';

    /**
    * Limit hello context query toothose records with hello authenticated user email address
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds hello email address from hello claims toohello context item - used for
    * insert operations
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when hello client does a request
    // READ - only return records belonging toohello authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite hello userId based on hello authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong toohello authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong toohello authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

<span data-ttu-id="df8a6-400">toosee какие утверждения будут доступны, используйте hello веб браузера tooview `/.auth/me` конечной точки веб-узла.</span><span class="sxs-lookup"><span data-stu-id="df8a6-400">toosee what claims are available, use a web browser tooview hello `/.auth/me` endpoint of your site.</span></span>

### <span data-ttu-id="df8a6-401"><a name="howto-tables-disabled"></a>Как: отключение доступа toospecific табличные операции</span><span class="sxs-lookup"><span data-stu-id="df8a6-401"><a name="howto-tables-disabled"></a>How to: Disable access toospecific table operations</span></span>
<span data-ttu-id="df8a6-402">В tooappearing сложения для таблицы hello свойство hello доступ может быть используется toocontrol отдельных операций.</span><span class="sxs-lookup"><span data-stu-id="df8a6-402">In addition tooappearing on hello table, hello access property can be used toocontrol individual operations.</span></span>  <span data-ttu-id="df8a6-403">Существует четыре операции:</span><span class="sxs-lookup"><span data-stu-id="df8a6-403">There are four operations:</span></span>

* <span data-ttu-id="df8a6-404">*чтение* hello RESTful получить операция на таблице hello</span><span class="sxs-lookup"><span data-stu-id="df8a6-404">*read* is hello RESTful GET operation on hello table</span></span>
* <span data-ttu-id="df8a6-405">*Вставить* операция hello RESTful POST на таблице hello</span><span class="sxs-lookup"><span data-stu-id="df8a6-405">*insert* is hello RESTful POST operation on hello table</span></span>
* <span data-ttu-id="df8a6-406">*Обновить* hello RESTful PATCH операция на таблице hello</span><span class="sxs-lookup"><span data-stu-id="df8a6-406">*update* is hello RESTful PATCH operation on hello table</span></span>
* <span data-ttu-id="df8a6-407">*Удалить* — hello RESTful удалить операцию в таблице hello</span><span class="sxs-lookup"><span data-stu-id="df8a6-407">*delete* is hello RESTful DELETE operation on hello table</span></span>

<span data-ttu-id="df8a6-408">Например можно назвать tooprovide таблицу без проверки подлинности только для чтения:</span><span class="sxs-lookup"><span data-stu-id="df8a6-408">For example, you may wish tooprovide a read-only unauthenticated table:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <span data-ttu-id="df8a6-409"><a name="howto-tables-query"></a>Как: Настройка hello запрос, который используется вместе с операциями таблицы</span><span class="sxs-lookup"><span data-stu-id="df8a6-409"><a name="howto-tables-query"></a>How to: Adjust hello query that is used with table operations</span></span>
<span data-ttu-id="df8a6-410">Общим требованием для операций с таблицами — tooprovide ограниченное представление данных hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-410">A common requirement for table operations is tooprovide a restricted view of hello data.</span></span>  <span data-ttu-id="df8a6-411">Например может предоставлять таблицы, помеченного hello с проверкой подлинности пользователя таким образом, можно только считывать или обновлять собственные записи.</span><span class="sxs-lookup"><span data-stu-id="df8a6-411">For example, you may provide a table that is tagged with hello authenticated user ID such that you can only read or update your own records.</span></span>  <span data-ttu-id="df8a6-412">После определения таблицы Hello предоставляет следующие функциональные возможности:</span><span class="sxs-lookup"><span data-stu-id="df8a6-412">hello following table definition provides this functionality:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for hello table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for hello authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite hello userId with hello authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

<span data-ttu-id="df8a6-413">Операции, которые подразумевают выполнение запроса, содержат свойство query, в которое можно добавить предложение where.</span><span class="sxs-lookup"><span data-stu-id="df8a6-413">Operations that normally execute a query have a query property that you can adjust with a where clause.</span></span> <span data-ttu-id="df8a6-414">свойство запроса Hello [QueryJS] объект, можно обработать используется tooconvert toosomething запроса OData, hello внутренних данных.</span><span class="sxs-lookup"><span data-stu-id="df8a6-414">hello query property is a [QueryJS] object that is used tooconvert an OData query toosomething that hello data backend can process.</span></span>  <span data-ttu-id="df8a6-415">Карты можно использовать для простого равенства случаях (например, предшествующие, hello).</span><span class="sxs-lookup"><span data-stu-id="df8a6-415">For simple equality cases (like hello preceding one), a map can be used.</span></span> <span data-ttu-id="df8a6-416">Можно также добавить определенные предложения SQL.</span><span class="sxs-lookup"><span data-stu-id="df8a6-416">You can also add specific SQL clauses:</span></span>

    context.query.where('myfield eq ?', 'value');

### <span data-ttu-id="df8a6-417"><a name="howto-tables-softdelete"></a>Практическое руководство. Настройка обратимого удаления для таблицы</span><span class="sxs-lookup"><span data-stu-id="df8a6-417"><a name="howto-tables-softdelete"></a>How to: Configure soft delete on a table</span></span>
<span data-ttu-id="df8a6-418">При обратимом удалении записи фактически не удаляются.</span><span class="sxs-lookup"><span data-stu-id="df8a6-418">Soft Delete does not actually delete records.</span></span>  <span data-ttu-id="df8a6-419">Вместо этого он отмечает их как удаленные в базе данных hello, задав tootrue hello удалить столбец.</span><span class="sxs-lookup"><span data-stu-id="df8a6-419">Instead it marks them as deleted within hello database by setting hello deleted column tootrue.</span></span>  <span data-ttu-id="df8a6-420">пакет SDK Azure Mobile приложения Hello автоматически удаляет обратимо удаленных записей из результатов только если hello пакет SDK для мобильных клиентов используются IncludeDeleted().</span><span class="sxs-lookup"><span data-stu-id="df8a6-420">hello Azure Mobile Apps SDK automatically removes soft-deleted records from results unless hello Mobile Client SDK uses IncludeDeleted().</span></span>  <span data-ttu-id="df8a6-421">удалить таблицу для программной, tooconfigure задать hello `softDelete` свойство в файле определения таблицы hello:</span><span class="sxs-lookup"><span data-stu-id="df8a6-421">tooconfigure a table for soft delete, set hello `softDelete` property in hello table definition file:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="df8a6-422">Следует создать механизм удаления записей посредством клиентского приложения, веб-заданий, функции Azure или настраиваемого API.</span><span class="sxs-lookup"><span data-stu-id="df8a6-422">You should establish a mechanism for purging records - either from a client application, via a WebJob, Azure Function or through a custom API.</span></span>

### <span data-ttu-id="df8a6-423"><a name="howto-tables-seeding"></a>Практическое руководство. Заполнение базы данных данными</span><span class="sxs-lookup"><span data-stu-id="df8a6-423"><a name="howto-tables-seeding"></a>How to: Seed your database with data</span></span>
<span data-ttu-id="df8a6-424">При создании нового приложения, вы можете tooseed таблицу с данными.</span><span class="sxs-lookup"><span data-stu-id="df8a6-424">When creating a new application, you may wish tooseed a table with data.</span></span>  <span data-ttu-id="df8a6-425">Это можно сделать в файле JavaScript для определения таблицы hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="df8a6-425">This can be done within hello table definition JavaScript file as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };
    table.seed = [
        { text: 'Example 1', complete: false },
        { text: 'Example 2', complete: true }
    ];

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="df8a6-426">Заполнение данных выполняется только при создании таблицы hello в пакет SDK Azure Mobile приложения hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-426">Seeding of data is only done when hello table is created by hello Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="df8a6-427">Если hello таблица уже существует в базе данных hello, данные не вставляется в таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-427">If hello table already exists within hello database, no data is injected into hello table.</span></span>  <span data-ttu-id="df8a6-428">Если включена динамическая схема, схема выводится из данных hello заполнена.</span><span class="sxs-lookup"><span data-stu-id="df8a6-428">If dynamic schema is turned on, then the schema is inferred from hello seeded data.</span></span>

<span data-ttu-id="df8a6-429">Рекомендуется явным образом вызвать hello `tables.initialize()` метод toocreate hello таблицы при запуске службы hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-429">We recommend that you explicitly call hello `tables.initialize()` method toocreate hello table when hello service starts running.</span></span>

### <span data-ttu-id="df8a6-430"><a name="Swagger"></a>Практическое руководство. Включение поддержки Swagger</span><span class="sxs-lookup"><span data-stu-id="df8a6-430"><a name="Swagger"></a>How to: Enable Swagger support</span></span>
<span data-ttu-id="df8a6-431">Мобильные приложения службы приложений Azure предоставляются со встроенной поддержкой [Swagger] .</span><span class="sxs-lookup"><span data-stu-id="df8a6-431">Azure App Service Mobile Apps comes with built-in [Swagger] support.</span></span>  <span data-ttu-id="df8a6-432">Поддержка Swagger tooenable сначала установить swagger hello пользовательского интерфейса как зависимость:</span><span class="sxs-lookup"><span data-stu-id="df8a6-432">tooenable Swagger support, first install hello swagger-ui as a dependency:</span></span>

    npm install --save swagger-ui

<span data-ttu-id="df8a6-433">После установки можно включить поддержку Swagger в конструкторе мобильных приложений Azure hello:</span><span class="sxs-lookup"><span data-stu-id="df8a6-433">Once installed, you can enable Swagger support in hello Azure Mobile Apps constructor:</span></span>

    var mobile = azureMobileApps({ swagger: true });

<span data-ttu-id="df8a6-434">Вы, возможно, только tooenable требуется поддержка Swagger в выпусках разработки.</span><span class="sxs-lookup"><span data-stu-id="df8a6-434">You probably only want tooenable Swagger support in development editions.</span></span>  <span data-ttu-id="df8a6-435">Это можно сделать с помощью параметра `NODE_ENV` приложения.</span><span class="sxs-lookup"><span data-stu-id="df8a6-435">You can do this by utilizing the `NODE_ENV` app setting:</span></span>

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

<span data-ttu-id="df8a6-436">Hello конечной точки swagger расположен в http://*данный сайт*.azurewebsites.net/swagger.</span><span class="sxs-lookup"><span data-stu-id="df8a6-436">hello swagger endpoint is located at http://*yoursite*.azurewebsites.net/swagger.</span></span>  <span data-ttu-id="df8a6-437">Можно получить доступ к hello Swagger пользовательского интерфейса через hello `/swagger/ui` конечной точки.</span><span class="sxs-lookup"><span data-stu-id="df8a6-437">You can access hello Swagger UI via hello `/swagger/ui` endpoint.</span></span>  <span data-ttu-id="df8a6-438">При выборе проверки подлинности toorequire через приложение Swagger приводит к ошибке.</span><span class="sxs-lookup"><span data-stu-id="df8a6-438">if you choose toorequire authentication across your entire application, Swagger produces an error.</span></span>  <span data-ttu-id="df8a6-439">Для получения наилучших результатов выберите tooallow не прошедшие проверку подлинности запросы через в hello проверки подлинности службы приложения Azure и авторизации, затем параметров проверки подлинности с использованием hello `table.access` свойство.</span><span class="sxs-lookup"><span data-stu-id="df8a6-439">For best results, choose tooallow unauthenticated requests through in hello Azure App Service Authentication / Authorization settings, then control authentication using hello `table.access` property.</span></span>

<span data-ttu-id="df8a6-440">Можно также добавить параметр tooyour hello Swagger `azureMobile.js` файл, если требуется только Swagger поддержку при разработке локально.</span><span class="sxs-lookup"><span data-stu-id="df8a6-440">You can also add hello Swagger option tooyour `azureMobile.js` file if you only want Swagger support when developing locally.</span></span>

## <a name="a-namepushpush-notifications"></a><span data-ttu-id="df8a6-441"><a name="push">Push-уведомления</span><span class="sxs-lookup"><span data-stu-id="df8a6-441"><a name="push">Push notifications</span></span>
<span data-ttu-id="df8a6-442">Мобильные приложения интегрируется с концентраторами уведомлений Azure tooenable вы toomillions уведомлений push toosend целевых устройств для всех основных платформ.</span><span class="sxs-lookup"><span data-stu-id="df8a6-442">Mobile Apps integrates with Azure Notification Hubs tooenable you toosend targeted push notifications toomillions of devices across all major platforms.</span></span> <span data-ttu-id="df8a6-443">С помощью концентраторов уведомлений, могут отправлять push tooiOS уведомления, Android и Windows.</span><span class="sxs-lookup"><span data-stu-id="df8a6-443">By using Notification Hubs, you can send push notifications tooiOS, Android and Windows devices.</span></span> <span data-ttu-id="df8a6-444">см. Дополнительные сведения о все, что вам можно делать с toolearn концентраторы уведомлений [Обзор концентраторов уведомлений](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="df8a6-444">toolearn more about all that you can do with Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

### <span data-ttu-id="df8a6-445"></a><a name="send-push"></a>Практическое руководство. Отправка push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="df8a6-445"></a><a name="send-push"></a>How to: Send push notifications</span></span>
<span data-ttu-id="df8a6-446">Hello, следующий код показывает, как toouse hello принудительной объекта toosend вещания push устройства iOS tooregistered уведомления:</span><span class="sxs-lookup"><span data-stu-id="df8a6-446">hello following code shows how toouse hello push object toosend a broadcast push notification tooregistered iOS devices:</span></span>

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do hello push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

<span data-ttu-id="df8a6-447">Создавая принудительную регистрацию шаблона из клиента hello, вместо этого можно отправить toodevices сообщение шаблона принудительной на всех поддерживаемых платформах.</span><span class="sxs-lookup"><span data-stu-id="df8a6-447">By creating a template push registration from hello client, you can instead send a template push message toodevices on all supported platforms.</span></span> <span data-ttu-id="df8a6-448">Здравствуйте, как следующий код показывает toosend шаблонное уведомление:</span><span class="sxs-lookup"><span data-stu-id="df8a6-448">hello following code shows how toosend a template notification:</span></span>

    // Define hello template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do hello push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }


### <span data-ttu-id="df8a6-449"><a name="push-user"></a>Как: tooan уведомления принудительной отправки, проверку подлинности пользователя, с помощью тегов</span><span class="sxs-lookup"><span data-stu-id="df8a6-449"><a name="push-user"></a>How to: Send push notifications tooan authenticated user using tags</span></span>
<span data-ttu-id="df8a6-450">Когда прошедший проверку пользователь регистрируется для push-уведомлений, тег ИД пользователя автоматически добавляется toohello регистрации.</span><span class="sxs-lookup"><span data-stu-id="df8a6-450">When an authenticated user registers for push notifications, a user ID tag is automatically added toohello registration.</span></span> <span data-ttu-id="df8a6-451">Используя этот тег, вы можете отправлять push уведомления tooall устройства, зарегистрированные определенным пользователем.</span><span class="sxs-lookup"><span data-stu-id="df8a6-451">By using this tag, you can send push notifications tooall devices registered by a specific user.</span></span> <span data-ttu-id="df8a6-452">Hello следующий код возвращает идентификатор SID пользователя, выполняющего запрос hello hello и отправляет шаблон регистрации push-уведомлений tooevery устройства для этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="df8a6-452">hello following code gets hello SID of user making hello request and sends a template push notification tooevery device registration for that user:</span></span>

    // Only do hello push if configured
    if (context.push) {
        // Send a notification toohello current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

<span data-ttu-id="df8a6-453">При регистрации для работы с push-уведомлениями на клиенте, прошедшем проверку подлинности, убедитесь, что проверка подлинности завершена, и только после этого начинайте регистрацию.</span><span class="sxs-lookup"><span data-stu-id="df8a6-453">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span>

## <span data-ttu-id="df8a6-454"><a name="CustomAPI"></a>Настраиваемые API</span><span class="sxs-lookup"><span data-stu-id="df8a6-454"><a name="CustomAPI"></a> Custom APIs</span></span>
### <span data-ttu-id="df8a6-455"><a name="howto-customapi-basic"></a>Практическое руководство. Определение настраиваемого интерфейса API</span><span class="sxs-lookup"><span data-stu-id="df8a6-455"><a name="howto-customapi-basic"></a>How to: Define a custom API</span></span>
<span data-ttu-id="df8a6-456">Кроме toohello доступа к данным API через конечную точку /tables hello, мобильные приложения Azure можно обслуживают пользовательские API.</span><span class="sxs-lookup"><span data-stu-id="df8a6-456">In addition toohello data access API via hello /tables endpoint, Azure Mobile Apps can provide custom API coverage.</span></span>  <span data-ttu-id="df8a6-457">Пользовательские API определяются в аналогичные определения таблиц toohello образом и можно получить доступ ко всем hello же средства, включая проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="df8a6-457">Custom APIs are defined in a similar way toohello table definitions and can access all hello same facilities, including authentication.</span></span>

<span data-ttu-id="df8a6-458">При желании toouse службы проверки подлинности в приложении пользовательский интерфейс API, необходимо настроить приложение проверки подлинности службы в hello [портал Azure] первой.</span><span class="sxs-lookup"><span data-stu-id="df8a6-458">If you wish toouse App Service Authentication with a Custom API, you must configure App Service Authentication in hello [Azure portal] first.</span></span>  <span data-ttu-id="df8a6-459">Для hello руководство по конфигурации для поставщика удостоверений hello просмотрите дополнительные сведения о настройке проверки подлинности в службе приложений Azure, предполагается toouse:</span><span class="sxs-lookup"><span data-stu-id="df8a6-459">For more details about configuring authentication in an Azure App Service, review hello Configuration Guide for hello identity provider you intend toouse:</span></span>

* <span data-ttu-id="df8a6-460">[Как tooconfigure проверки подлинности Azure Active Directory]</span><span class="sxs-lookup"><span data-stu-id="df8a6-460">[How tooconfigure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="df8a6-461">[Как tooconfigure проверки подлинности Facebook]</span><span class="sxs-lookup"><span data-stu-id="df8a6-461">[How tooconfigure Facebook Authentication]</span></span>
* <span data-ttu-id="df8a6-462">[Как tooconfigure проверки подлинности Google]</span><span class="sxs-lookup"><span data-stu-id="df8a6-462">[How tooconfigure Google Authentication]</span></span>
* <span data-ttu-id="df8a6-463">[Как tooconfigure проверки подлинности Майкрософт]</span><span class="sxs-lookup"><span data-stu-id="df8a6-463">[How tooconfigure Microsoft Authentication]</span></span>
* <span data-ttu-id="df8a6-464">[Как tooconfigure проверки подлинности Twitter]</span><span class="sxs-lookup"><span data-stu-id="df8a6-464">[How tooconfigure Twitter Authentication]</span></span>

<span data-ttu-id="df8a6-465">Пользовательские API определяются во многом так же, как hello API таблиц hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-465">Custom APIs are defined in much hello same way as hello Tables API.</span></span>

1. <span data-ttu-id="df8a6-466">Создайте каталог **api** .</span><span class="sxs-lookup"><span data-stu-id="df8a6-466">Create an **api** directory</span></span>
2. <span data-ttu-id="df8a6-467">Создайте файл JavaScript определения API в hello **api** каталога.</span><span class="sxs-lookup"><span data-stu-id="df8a6-467">Create an API definition JavaScript file in hello **api** directory.</span></span>
3. <span data-ttu-id="df8a6-468">Используйте hello импорта метод tooimport hello **api** каталога.</span><span class="sxs-lookup"><span data-stu-id="df8a6-468">Use hello import method tooimport hello **api** directory.</span></span>

<span data-ttu-id="df8a6-469">Вот определение api прототип hello, на основе выборки basic приложения hello, использовавшегося ранее.</span><span class="sxs-lookup"><span data-stu-id="df8a6-469">Here is hello prototype api definition based on hello basic-app sample we used earlier.</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="df8a6-470">Рассмотрим пример API, который возвращает дату hello server, с помощью hello *Date.now()* метод.</span><span class="sxs-lookup"><span data-stu-id="df8a6-470">Let's take an example API that returns hello server date using hello *Date.now()* method.</span></span>  <span data-ttu-id="df8a6-471">Ниже приведен файл api/date.js hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-471">Here is hello api/date.js file:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

<span data-ttu-id="df8a6-472">Каждый параметр представляет один hello стандартных RESTful команд - GET, POST, PATCH или DELETE.</span><span class="sxs-lookup"><span data-stu-id="df8a6-472">Each parameter is one of hello standard RESTful verbs - GET, POST, PATCH, or DELETE.</span></span>  <span data-ttu-id="df8a6-473">метод Hello — это стандарт [ExpressJS по промежуточного слоя] функцию, которая отправляет выходные данные, необходимые hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-473">hello method is a standard [ExpressJS Middleware] function that sends hello required output.</span></span>

### <span data-ttu-id="df8a6-474"><a name="howto-customapi-auth"></a>Как: требуется проверка подлинности для доступа к tooa настраиваемого API</span><span class="sxs-lookup"><span data-stu-id="df8a6-474"><a name="howto-customapi-auth"></a>How to: Require authentication for access tooa custom API</span></span>
<span data-ttu-id="df8a6-475">Пакет SDK для приложений мобильных Azure реализует проверку подлинности в hello одинаково для конечной точки hello таблицы и пользовательские API.</span><span class="sxs-lookup"><span data-stu-id="df8a6-475">Azure Mobile Apps SDK implements authentication in hello same way for both hello tables endpoint and custom APIs.</span></span>  <span data-ttu-id="df8a6-476">Чтобы добавить API toohello проверки подлинности, разработанные в предыдущем разделе hello, добавьте **доступа** свойство:</span><span class="sxs-lookup"><span data-stu-id="df8a6-476">To add authentication toohello API developed in hello previous section, add an **access** property:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="df8a6-477">Также можно определить проверку подлинности для конкретных операций:</span><span class="sxs-lookup"><span data-stu-id="df8a6-477">You can also specify authentication on specific operations:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // hello GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="df8a6-478">Hello тот же токен, используемый для конечной точки hello таблиц необходимо использовать для пользовательских API, требующей проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="df8a6-478">hello same token that is used for hello tables endpoint must be used for custom APIs requiring authentication.</span></span>

### <span data-ttu-id="df8a6-479"><a name="howto-customapi-auth"></a>Практическое руководство. Обработка передачи больших файлов</span><span class="sxs-lookup"><span data-stu-id="df8a6-479"><a name="howto-customapi-auth"></a>How to: Handle large file uploads</span></span>
<span data-ttu-id="df8a6-480">Пакет SDK для приложений мобильных Azure использует hello [синтаксического анализа текста по промежуточного слоя](https://github.com/expressjs/body-parser) tooaccept и расшифровать содержимое тела в заявку на участие.</span><span class="sxs-lookup"><span data-stu-id="df8a6-480">Azure Mobile Apps SDK uses hello [body-parser middleware](https://github.com/expressjs/body-parser) tooaccept and decode body content in your submission.</span></span>  <span data-ttu-id="df8a6-481">Можно предварительно настроить передачи больших файлов tooaccept синтаксического анализа текста:</span><span class="sxs-lookup"><span data-stu-id="df8a6-481">You can pre-configure body-parser tooaccept larger file uploads:</span></span>

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="df8a6-482">файл Hello — перед передачей в кодировке base-64.</span><span class="sxs-lookup"><span data-stu-id="df8a6-482">hello file is base-64 encoded before transmission.</span></span>  <span data-ttu-id="df8a6-483">Это увеличивает размер hello непосредственную отправку hello (и следовательно hello размер, до которого необходимо учитывать).</span><span class="sxs-lookup"><span data-stu-id="df8a6-483">This increases hello size of hello actual upload (and hence hello size you must account for).</span></span>

### <span data-ttu-id="df8a6-484"><a name="howto-customapi-sql"></a>Практическое руководство. Выполнение пользовательских инструкций SQL</span><span class="sxs-lookup"><span data-stu-id="df8a6-484"><a name="howto-customapi-sql"></a>How to: Execute custom SQL statements</span></span>
<span data-ttu-id="df8a6-485">пакет SDK Azure Mobile приложения Hello разрешает доступ toohello всего контекста с помощью hello объекта запроса, позволяя tooexecute легко параметризованные поставщик данных toohello инструкций SQL:</span><span class="sxs-lookup"><span data-stu-id="df8a6-485">hello Azure Mobile Apps SDK allows access toohello entire Context through hello request object, allowing you tooexecute parameterized SQL statements toohello defined data provider easily:</span></span>

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on tooa later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define hello query - anything that can be handled by hello mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute hello query.  hello context for Azure Mobile Apps is available through
            // request.azureMobile - hello data object contains hello configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <span data-ttu-id="df8a6-486"><a name="Debugging"></a>Отладка, простые таблицы и простые интерфейсы API</span><span class="sxs-lookup"><span data-stu-id="df8a6-486"><a name="Debugging"></a>Debugging, Easy Tables, and Easy APIs</span></span>
### <span data-ttu-id="df8a6-487"><a name="howto-diagnostic-logs"></a>Практическое руководство. Отладка, диагностика и устранение неполадок мобильных приложений Azure</span><span class="sxs-lookup"><span data-stu-id="df8a6-487"><a name="howto-diagnostic-logs"></a>How to: Debug, diagnose, and troubleshoot Azure Mobile apps</span></span>
<span data-ttu-id="df8a6-488">Hello службе приложений Azure предоставляет несколько отладки и рекомендации по устранению неполадок для приложений Node.js.</span><span class="sxs-lookup"><span data-stu-id="df8a6-488">hello Azure App Service provides several debugging and troubleshooting techniques for Node.js applications.</span></span>
<span data-ttu-id="df8a6-489">См. следующие статьи tooget работы при устранении неполадок серверной части мобильных Node.js toohello:</span><span class="sxs-lookup"><span data-stu-id="df8a6-489">Refer toohello following articles tooget started in troubleshooting your Node.js Mobile backend:</span></span>

* <span data-ttu-id="df8a6-490">[Мониторинг службы приложений Azure]</span><span class="sxs-lookup"><span data-stu-id="df8a6-490">[Monitoring an Azure App Service]</span></span>
* <span data-ttu-id="df8a6-491">[Включение ведения журналов диагностики в службе приложений Azure]</span><span class="sxs-lookup"><span data-stu-id="df8a6-491">[Enable Diagnostic Logging in Azure App Service]</span></span>
* <span data-ttu-id="df8a6-492">[Диагностика службы приложений Azure в Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="df8a6-492">[Troubleshoot an Azure App Service in Visual Studio]</span></span>

<span data-ttu-id="df8a6-493">Node.js приложения имеют доступ tooa широкий спектр средств журнала диагностики.</span><span class="sxs-lookup"><span data-stu-id="df8a6-493">Node.js applications have access tooa wide range of diagnostic log tools.</span></span>  <span data-ttu-id="df8a6-494">На внутреннем уровне hello использует пакет SDK для Azure мобильных приложений Node.js [Winston] для ведения журнала диагностики.</span><span class="sxs-lookup"><span data-stu-id="df8a6-494">Internally, hello Azure Mobile Apps Node.js SDK uses [Winston] for diagnostic logging.</span></span>  <span data-ttu-id="df8a6-495">Включение режима отладки или установка hello автоматически включено ведение журнала **MS_DebugMode** tootrue параметр приложения в hello [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="df8a6-495">Logging is automatically enabled by enabling debug mode or by setting hello **MS_DebugMode** app setting tootrue in hello [Azure portal].</span></span> <span data-ttu-id="df8a6-496">Созданные журналы отображаются в hello журналов диагностики на hello [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="df8a6-496">Generated logs appear in hello Diagnostic Logs on hello [Azure portal].</span></span>

### <span data-ttu-id="df8a6-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>Как: работать с простой таблицы в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="df8a6-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>How to: Work with Easy Tables in hello Azure portal</span></span>
<span data-ttu-id="df8a6-498">Простой таблицы в портале hello позволяют создавать и работать с правой таблицы в портале hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-498">Easy Tables in hello portal let you create and work with tables right in hello portal.</span></span> <span data-ttu-id="df8a6-499">Можно изменить даже hello редактор службы приложения с помощью операций с таблицами.</span><span class="sxs-lookup"><span data-stu-id="df8a6-499">You can even edit table operations using hello App Service Editor.</span></span>

<span data-ttu-id="df8a6-500">Щелкнув **Простые таблицы** в параметрах сайта серверной части, вы сможете добавить, изменить или удалить таблицу.</span><span class="sxs-lookup"><span data-stu-id="df8a6-500">When you click **Easy tables** in your backend site settings, you can add, modify, or delete a table.</span></span> <span data-ttu-id="df8a6-501">Также вы увидите данные в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-501">You can also see data in hello table.</span></span>

![Работа с Easy Tables](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

<span data-ttu-id="df8a6-503">Hello доступны следующие команды на панели команд hello для таблицы:</span><span class="sxs-lookup"><span data-stu-id="df8a6-503">hello following commands are available on hello command bar for a table:</span></span>

* <span data-ttu-id="df8a6-504">**Изменение разрешений** — изменять hello разрешений для чтения, вставки, операций обновления и удаления в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-504">**Change permissions** - modify hello permission for read, insert, update and delete operations on hello table.</span></span>
  <span data-ttu-id="df8a6-505">Параметрами являются tooallow анонимный доступ, проверка подлинности toorequire или toodisable обращаться к toohello операции.</span><span class="sxs-lookup"><span data-stu-id="df8a6-505">Options are tooallow anonymous access, toorequire authentication, or toodisable all access toohello operation.</span></span>
* <span data-ttu-id="df8a6-506">**Измените скрипт** -hello скрипт для таблицы hello откроется в редакторе службы приложения hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-506">**Edit script** - hello script file for hello table is opened in hello App Service Editor.</span></span>
* <span data-ttu-id="df8a6-507">**Управление схемой** - Добавление или удаление столбцов или изменении индекса таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-507">**Manage schema** - add or delete columns or change hello table index.</span></span>
* <span data-ttu-id="df8a6-508">**Очистить таблицу** -усекает существующей таблицы при удалении всех строк данных с сохранением hello схемы без изменений.</span><span class="sxs-lookup"><span data-stu-id="df8a6-508">**Clear table** - truncates an existing table be deleting all data rows but leaving hello schema unchanged.</span></span>
* <span data-ttu-id="df8a6-509">**Удалить строки** — удаляет отдельные строки данных.</span><span class="sxs-lookup"><span data-stu-id="df8a6-509">**Delete rows** - delete individual rows of data.</span></span>
* <span data-ttu-id="df8a6-510">**Журналы потоковой передачи представление** -подключит вас toohello потоковой передачи службы журналов для веб-узла.</span><span class="sxs-lookup"><span data-stu-id="df8a6-510">**View streaming logs** - connects you toohello streaming log service for your site.</span></span>

### <span data-ttu-id="df8a6-511"><a name="work-easy-apis"></a>Как: работать с простой API-интерфейсы в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="df8a6-511"><a name="work-easy-apis"></a>How to: Work with Easy APIs in hello Azure portal</span></span>
<span data-ttu-id="df8a6-512">Простой API-интерфейсы в портале hello позволяют создавать и работать с пользовательского API-интерфейсы права на портале hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-512">Easy APIs in hello portal let you create and work with custom APIs right in hello portal.</span></span> <span data-ttu-id="df8a6-513">Можно редактировать скрипты API, с помощью редактора службы приложения hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-513">You can edit API scripts using hello App Service Editor.</span></span>

<span data-ttu-id="df8a6-514">Щелкнув **Простые API** в параметрах сайта серверной части, вы сможете добавить, изменить или удалить настраиваемую конечную точку API.</span><span class="sxs-lookup"><span data-stu-id="df8a6-514">When you click **Easy APIs** in your backend site settings, you can add, modify, or delete a custom API endpoint.</span></span>

![Работа с Easy APIs](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

<span data-ttu-id="df8a6-516">На портале hello можно изменить hello разрешения на доступ для выполнения данного действия HTTP, измените файл скрипта API hello в редакторе приложения службы или Просмотр журналов потоковой передачи hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-516">In hello portal, you can change hello access permissions for a given HTTP action, edit hello API script file in the App Service Editor, or view hello streaming logs.</span></span>

### <span data-ttu-id="df8a6-517"><a name="online-editor"></a>Как: изменение кода в редакторе службы приложения hello</span><span class="sxs-lookup"><span data-stu-id="df8a6-517"><a name="online-editor"></a>How to: Edit code in hello App Service Editor</span></span>
<span data-ttu-id="df8a6-518">Hello Azure портал позволяет редактировать файлы скриптов серверной Node.js в редакторе службы приложения hello без необходимости загружать hello проекта tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="df8a6-518">hello Azure portal lets you edit your Node.js backend script files in hello App Service Editor without having to download hello project tooyour local computer.</span></span> <span data-ttu-id="df8a6-519">файлы скриптов tooedit в интерактивном редакторе hello:</span><span class="sxs-lookup"><span data-stu-id="df8a6-519">tooedit script files in hello online editor:</span></span>

1. <span data-ttu-id="df8a6-520">В колонке серверной части мобильного приложения щелкните **Все параметры**, затем **Простые таблицы** или **Простые API**, выберите таблицу или API и щелкните **Изменить сценарий**.</span><span class="sxs-lookup"><span data-stu-id="df8a6-520">In your Mobile App backend blade, click **All settings** > either **Easy tables** or **Easy APIs**, click a table or API, then click **Edit script**.</span></span> <span data-ttu-id="df8a6-521">файл скрипта Hello открывается в редакторе службы приложения hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-521">hello script file is opened in hello App Service Editor.</span></span>

    ![Редактор службы приложений](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. <span data-ttu-id="df8a6-523">Сделать файл кода toohello изменения в интерактивном редакторе hello.</span><span class="sxs-lookup"><span data-stu-id="df8a6-523">Make your changes toohello code file in hello online editor.</span></span> <span data-ttu-id="df8a6-524">Изменения сохраняются автоматически при вводе.</span><span class="sxs-lookup"><span data-stu-id="df8a6-524">Changes are saved automatically as you type.</span></span>

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
[Быстрый запуск клиента Android]: app-service-mobile-android-get-started.md
[Быстрый запуск клиента Apache Cordova]: app-service-mobile-cordova-get-started.md
[Быстрый запуск клиента iOS.]: app-service-mobile-ios-get-started.md
[Быстрый запуск клиента Xamarin.iOS.]: app-service-mobile-xamarin-ios-get-started.md
[Быстрый запуск клиента Xamarin.Android.]: app-service-mobile-xamarin-android-get-started.md
[Быстрый запуск клиента Xamarin.Forms.]: app-service-mobile-xamarin-forms-get-started.md
[Быстрый запуск клиента Магазина Windows Phone.]: app-service-mobile-windows-store-dotnet-get-started.md
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
[автономные данные синхронизации]: app-service-mobile-offline-data-sync.md
[Как tooconfigure проверки подлинности Azure Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Как tooconfigure проверки подлинности Facebook]: app-service-mobile-how-to-configure-facebook-authentication.md
[Как tooconfigure проверки подлинности Google]: app-service-mobile-how-to-configure-google-authentication.md
[Как tooconfigure проверки подлинности Майкрософт]: app-service-mobile-how-to-configure-microsoft-authentication.md
[Как tooconfigure проверки подлинности Twitter]: app-service-mobile-how-to-configure-twitter-authentication.md
[руководстве по развертыванию службы приложений Azure]: ../app-service-web/web-sites-deploy.md
[Мониторинг службы приложений Azure]: ../app-service-web/web-sites-monitor.md
[Включение ведения журналов диагностики в службе приложений Azure]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Диагностика службы приложений Azure в Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md
[укажите hello версия узла]: ../nodejs-specify-node-version-azure-apps.md
[используйте модули узла]: ../nodejs-use-node-modules-azure-apps.md
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
[Express]: http://expressjs.com/
[Swagger]: http://swagger.io/

[портал Azure]: https://portal.azure.com/
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[пример basicapp на GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[пример todo на GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[каталог образцов на GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 для Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[пакет Node.js mssql]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS по промежуточного слоя]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
