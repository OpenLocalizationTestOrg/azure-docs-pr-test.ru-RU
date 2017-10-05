---
title: "Работа с пакетом SDK для внутреннего сервера Node.js для мобильных приложений | Документация Майкрософт"
description: "Узнайте, как работать с пакетом SDK для серверной части на Node.js для мобильных приложений службы приложений Azure."
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
ms.openlocfilehash: 1d3aa7a0089279a8eafeb0ded951a5238e189eaa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-azure-mobile-apps-nodejs-sdk"></a><span data-ttu-id="dd456-103">Использование пакета SDK Node.js для мобильных приложений Azure</span><span class="sxs-lookup"><span data-stu-id="dd456-103">How to use the Azure Mobile Apps Node.js SDK</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="dd456-104">Эта статья содержит подробную информацию о программировании серверной части на платформе Node.js в мобильных приложениях службы приложений Azure, а также соответствующие примеры.</span><span class="sxs-lookup"><span data-stu-id="dd456-104">This article provides detailed information and examples showing how to work with a Node.js backend in Azure App Service Mobile Apps.</span></span>

## <span data-ttu-id="dd456-105"><a name="Introduction"></a>Введение</span><span class="sxs-lookup"><span data-stu-id="dd456-105"><a name="Introduction"></a>Introduction</span></span>
<span data-ttu-id="dd456-106">Мобильное приложение службы приложений Azure позволяет добавлять веб-API в веб-приложения для доступа к данным, оптимизированным для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="dd456-106">Azure App Service Mobile Apps provides the capability to add a mobile-optimized data access Web API to a web application.</span></span>  <span data-ttu-id="dd456-107">Пакет SDK для мобильных приложений службы приложений Azure используется в веб-приложениях ASP.NET и Node.js.</span><span class="sxs-lookup"><span data-stu-id="dd456-107">The Azure App Service Mobile Apps SDK is provided for ASP.NET and Node.js web applications.</span></span>  <span data-ttu-id="dd456-108">С помощью этого пакета SDK выполняются следующие операции:</span><span class="sxs-lookup"><span data-stu-id="dd456-108">The SDK provides the following operations:</span></span>

* <span data-ttu-id="dd456-109">Табличные операции (чтение, вставка, обновление, удаление данных).</span><span class="sxs-lookup"><span data-stu-id="dd456-109">Table operations (Read, Insert, Update, Delete) for data access</span></span>
* <span data-ttu-id="dd456-110">Пользовательские операции API.</span><span class="sxs-lookup"><span data-stu-id="dd456-110">Custom API operations</span></span>

<span data-ttu-id="dd456-111">Операции обоих типов поддерживают проверку подлинности для всех поставщиков удостоверений, разрешенных службой приложений Azure, включая поставщиков удостоверений социальных сетей, таких как Facebook, Twitter, Google и Майкрософт, а также Azure Active Directory для корпоративной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="dd456-111">Both operations provide for authentication across all identity providers allowed by Azure App Service, including social identity providers such as Facebook, Twitter, Google and Microsoft as well as Azure Active Directory for enterprise identity.</span></span>

<span data-ttu-id="dd456-112">Примеры для каждого варианта использования можно найти в [каталоге примеров на сайте GitHub].</span><span class="sxs-lookup"><span data-stu-id="dd456-112">You can find samples for each use case in the [samples directory on GitHub].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="dd456-113">Поддерживаемые платформы</span><span class="sxs-lookup"><span data-stu-id="dd456-113">Supported Platforms</span></span>
<span data-ttu-id="dd456-114">Пакет SDK Node для мобильных приложений Azure поддерживает текущий выпуск LTS Node и более поздние версии.</span><span class="sxs-lookup"><span data-stu-id="dd456-114">The Azure Mobile Apps Node SDK supports the current LTS release of Node and later.</span></span>  <span data-ttu-id="dd456-115">На момент написания статьи последней версией LTS является Node 4.5.0.</span><span class="sxs-lookup"><span data-stu-id="dd456-115">As of writing, the latest LTS version is Node v4.5.0.</span></span>  <span data-ttu-id="dd456-116">Другие версии Node могут также работать, но они не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="dd456-116">Other versions of Node may work, but are not supported.</span></span>

<span data-ttu-id="dd456-117">Пакет SDK Node для мобильных приложений Azure поддерживает два драйвера базы данных. Драйвер node-mssql поддерживает SQL Azure и локальные экземпляры SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dd456-117">The Azure Mobile Apps Node SDK supports two database drivers - the node-mssql driver supports SQL Azure and local SQL Server instances.</span></span>  <span data-ttu-id="dd456-118">Драйвер sqlite3 поддерживает базы данных SQLite только в отдельном экземпляре.</span><span class="sxs-lookup"><span data-stu-id="dd456-118">The sqlite3 driver supports SQLite databases on a single instance only.</span></span>

### <span data-ttu-id="dd456-119"><a name="howto-cmdline-basicapp"></a>Создание базовой серверной части на основе Node.js с помощью командной строки</span><span class="sxs-lookup"><span data-stu-id="dd456-119"><a name="howto-cmdline-basicapp"></a>How to: Create a Basic Node.js backend using the Command Line</span></span>
<span data-ttu-id="dd456-120">Каждая серверная часть на Node.js для мобильного приложения службы приложений Azure запускается как приложение ExpressJS.</span><span class="sxs-lookup"><span data-stu-id="dd456-120">Every Azure App Service Mobile App Node.js backend starts as an ExpressJS application.</span></span>  <span data-ttu-id="dd456-121">ExpressJS является наиболее популярной платформой веб-служб для Node.js.</span><span class="sxs-lookup"><span data-stu-id="dd456-121">ExpressJS is the most popular web service framework available for Node.js.</span></span>  <span data-ttu-id="dd456-122">Вот как создать простое приложение [Express] :</span><span class="sxs-lookup"><span data-stu-id="dd456-122">You can create a basic [Express] application as follows:</span></span>

1. <span data-ttu-id="dd456-123">В командной строке или окне PowerShell создайте каталог для проекта.</span><span class="sxs-lookup"><span data-stu-id="dd456-123">In a command or PowerShell window, create a directory for your project.</span></span>

        mkdir basicapp
2. <span data-ttu-id="dd456-124">Запустите команду npm init, чтобы инициализировать структуру пакета.</span><span class="sxs-lookup"><span data-stu-id="dd456-124">Run npm init to initialize the package structure.</span></span>

        cd basicapp
        npm init

    <span data-ttu-id="dd456-125">Для инициализации проекта команда npm init выводит ряд вопросов.</span><span class="sxs-lookup"><span data-stu-id="dd456-125">The npm init command asks a set of questions to initialize the project.</span></span>  <span data-ttu-id="dd456-126">Пример выходных данных приведен ниже.</span><span class="sxs-lookup"><span data-stu-id="dd456-126">See the example output:</span></span>

    ![Выходные данные npm init][0]
3. <span data-ttu-id="dd456-128">Установите библиотеки express и azure-mobile-apps из репозитория npm.</span><span class="sxs-lookup"><span data-stu-id="dd456-128">Install the express and azure-mobile-apps libraries from the npm repository.</span></span>

        npm install --save express azure-mobile-apps
4. <span data-ttu-id="dd456-129">Создайте файл app.js для реализации базового мобильного сервера.</span><span class="sxs-lookup"><span data-stu-id="dd456-129">Create an app.js file to implement the basic mobile server.</span></span>

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add the mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

<span data-ttu-id="dd456-130">Это приложение создает веб-API, оптимизированный для мобильных устройств, с одной конечной точкой (`/tables/TodoItem`), которая с помощью динамической схемы предоставляет доступ к базовому хранилищу данных SQL без аутентификации.</span><span class="sxs-lookup"><span data-stu-id="dd456-130">This application creates a mobile-optimized WebAPI with a single endpoint (`/tables/TodoItem`) that provides unauthenticated access to an underlying SQL data store using a dynamic schema.</span></span>  <span data-ttu-id="dd456-131">Этот пример подходит к следующим примерам использования клиентских библиотек.</span><span class="sxs-lookup"><span data-stu-id="dd456-131">It is suitable for following the client library quick starts:</span></span>

* <span data-ttu-id="dd456-132">[Быстрый запуск клиента Android]</span><span class="sxs-lookup"><span data-stu-id="dd456-132">[Android Client QuickStart]</span></span>
* <span data-ttu-id="dd456-133">[Быстрый запуск клиента Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="dd456-133">[Apache Cordova Client QuickStart]</span></span>
* <span data-ttu-id="dd456-134">[Быстрый запуск клиента iOS.]</span><span class="sxs-lookup"><span data-stu-id="dd456-134">[iOS Client QuickStart]</span></span>
* <span data-ttu-id="dd456-135">[Быстрый запуск клиента Магазина Windows Phone.]</span><span class="sxs-lookup"><span data-stu-id="dd456-135">[Windows Store Client QuickStart]</span></span>
* <span data-ttu-id="dd456-136">[Быстрый запуск клиента Xamarin.iOS.]</span><span class="sxs-lookup"><span data-stu-id="dd456-136">[Xamarin.iOS Client QuickStart]</span></span>
* <span data-ttu-id="dd456-137">[Быстрый запуск клиента Xamarin.Android.]</span><span class="sxs-lookup"><span data-stu-id="dd456-137">[Xamarin.Android Client QuickStart]</span></span>
* <span data-ttu-id="dd456-138">[Быстрый запуск клиента Xamarin.Forms.]</span><span class="sxs-lookup"><span data-stu-id="dd456-138">[Xamarin.Forms Client QuickStart]</span></span>

<span data-ttu-id="dd456-139">Код этого базового приложения можно найти в [примере basicapp на сайте GitHub].</span><span class="sxs-lookup"><span data-stu-id="dd456-139">You can find the code for this basic application in the [basicapp sample on GitHub].</span></span>

### <span data-ttu-id="dd456-140"><a name="howto-vs2015-basicapp"></a>Создание серверной части на основе Node.js с помощью Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="dd456-140"><a name="howto-vs2015-basicapp"></a>How to: Create a Node backend with Visual Studio 2015</span></span>
<span data-ttu-id="dd456-141">Для разработки приложений на Node.js в рамках IDE с помощью Visual Studio 2015 требуется специальное расширение.</span><span class="sxs-lookup"><span data-stu-id="dd456-141">Visual Studio 2015 requires an extension to develop Node.js applications within the IDE.</span></span>  <span data-ttu-id="dd456-142">Для начала установите [Node.js Tools 1.1 для Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="dd456-142">To start, install the [Node.js Tools 1.1 for Visual Studio].</span></span>  <span data-ttu-id="dd456-143">После установки средств Node.js для Visual Studio создайте приложение Express 4.x.</span><span class="sxs-lookup"><span data-stu-id="dd456-143">Once the Node.js Tools for Visual Studio are installed, create an Express 4.x application:</span></span>

1. <span data-ttu-id="dd456-144">Откройте диалоговое окно **Новый проект** (последовательно выберите **Файл** > **Создать** > **Проект**).</span><span class="sxs-lookup"><span data-stu-id="dd456-144">Open the **New Project** dialog (from **File** > **New** > **Project...**).</span></span>
2. <span data-ttu-id="dd456-145">Разверните **Шаблоны** > **JavaScript** > **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="dd456-145">Expand **Templates** > **JavaScript** > **Node.js**.</span></span>
3. <span data-ttu-id="dd456-146">Выберите **Базовое приложение Node.js Express 4 для Azure**.</span><span class="sxs-lookup"><span data-stu-id="dd456-146">Select the **Basic Azure Node.js Express 4 Application**.</span></span>
4. <span data-ttu-id="dd456-147">Введите имя проекта.</span><span class="sxs-lookup"><span data-stu-id="dd456-147">Fill in the project name.</span></span>  <span data-ttu-id="dd456-148">Нажмите кнопку *ОК*.</span><span class="sxs-lookup"><span data-stu-id="dd456-148">Click *OK*.</span></span>

    ![Новый проект Visual Studio 2015][1]
5. <span data-ttu-id="dd456-150">Щелкните правой кнопкой мыши узел **npm** и выберите пункт **Install New npm packages…** (Установка новых пакетов npm).</span><span class="sxs-lookup"><span data-stu-id="dd456-150">Right-click the **npm** node and select **Install New npm packages...**.</span></span>
6. <span data-ttu-id="dd456-151">Вам может потребоваться обновить каталог npm перед созданием первого приложения на Node.js.</span><span class="sxs-lookup"><span data-stu-id="dd456-151">You may need to refresh the npm catalog on creating your first Node.js application.</span></span>  <span data-ttu-id="dd456-152">При необходимости щелкните **Обновить** .</span><span class="sxs-lookup"><span data-stu-id="dd456-152">Click **Refresh** if necessary.</span></span>
7. <span data-ttu-id="dd456-153">В поле поиска введите *azure-mobile-apps* .</span><span class="sxs-lookup"><span data-stu-id="dd456-153">Enter *azure-mobile-apps* in the search box.</span></span>  <span data-ttu-id="dd456-154">Щелкните пакет **azure-mobile-apps 2.0.0** и нажмите кнопку **Установить пакет**.</span><span class="sxs-lookup"><span data-stu-id="dd456-154">Click the **azure-mobile-apps 2.0.0** package, then click **Install Package**.</span></span>

    ![Установка новых пакетов npm][2]
8. <span data-ttu-id="dd456-156">Нажмите кнопку **Закрыть**</span><span class="sxs-lookup"><span data-stu-id="dd456-156">Click **Close**.</span></span>
9. <span data-ttu-id="dd456-157">Откройте файл *app.js* , чтобы добавить поддержку пакета SDK для мобильных приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="dd456-157">Open the *app.js* file to add support for the Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="dd456-158">В строке 6 в нижней части инструкций require библиотеки добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="dd456-158">At line 6 at the bottom of the library require statements, add the following code:</span></span>

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    <span data-ttu-id="dd456-159">Примерно в строке 27 после других инструкций app.use добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="dd456-159">At approximately line 27 after the other app.use statements, add the following code:</span></span>

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    <span data-ttu-id="dd456-160">Сохраните файл .</span><span class="sxs-lookup"><span data-stu-id="dd456-160">Save the file.</span></span>
10. <span data-ttu-id="dd456-161">Запустите приложение локально (API обслуживается по адресу http://localhost:3000) или опубликуйте его в Azure.</span><span class="sxs-lookup"><span data-stu-id="dd456-161">Either run the application locally (the API is served on http://localhost:3000) or publish to Azure.</span></span>

### <span data-ttu-id="dd456-162"><a name="create-node-backend-portal"></a>Практическое руководство. Создание серверной части Node.js с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="dd456-162"><a name="create-node-backend-portal"></a>How to: Create a Node.js backend using the Azure portal</span></span>
<span data-ttu-id="dd456-163">Серверную часть мобильного приложения можно создать прямо на [портале Azure].</span><span class="sxs-lookup"><span data-stu-id="dd456-163">You can create a Mobile App backend right in the [Azure portal].</span></span> <span data-ttu-id="dd456-164">Для этого выполните описанные ниже действия либо инструкции из учебника [Создание мобильного приложения](app-service-mobile-ios-get-started.md) , где описано одновременное создание клиента и сервера.</span><span class="sxs-lookup"><span data-stu-id="dd456-164">You can either follow the following steps or create a client and server together by following the [Create a mobile app](app-service-mobile-ios-get-started.md) tutorial.</span></span> <span data-ttu-id="dd456-165">В этом учебнике представлена упрощенная версия этих инструкций, что лучше всего подходит для проектов, предназначенных для подтверждения концепции.</span><span class="sxs-lookup"><span data-stu-id="dd456-165">The tutorial contains a simplified version of these instructions and is best for proof of concept projects.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="dd456-166">Вернитесь в колонку *Начало работы* и в разделе **Create a table API** (Создание API таблицы) выберите в поле **Backend language** (Язык серверной части) значение **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="dd456-166">Back in the *Get started* blade, under **Create a table API**, choose **Node.js** as your **Backend language**.</span></span>
<span data-ttu-id="dd456-167">Установите флажок **Я понимаю, что это перезапишет все содержимое сайта.** и щелкните **Создание таблицы TodoItem**.</span><span class="sxs-lookup"><span data-stu-id="dd456-167">Check the box for "**I acknowledge that this will overwrite all site contents.**", then click **Create TodoItem table**.</span></span>

### <span data-ttu-id="dd456-168"><a name="download-quickstart"></a>Загрузка серверной части на основе Node.js в виде готового кода для быстрого запуска с помощью Git</span><span class="sxs-lookup"><span data-stu-id="dd456-168"><a name="download-quickstart"></a>How to: Download the Node.js backend quickstart code project using Git</span></span>
<span data-ttu-id="dd456-169">Когда вы создаете серверную часть мобильного приложения Node.js с помощью колонки портала **Быстрый запуск**, для вас будет создан и развернут на сайте проект Node.js.</span><span class="sxs-lookup"><span data-stu-id="dd456-169">When you create a Node.js Mobile App backend by using the portal **Quick start** blade, a Node.js project is created for you and deployed to your site.</span></span> <span data-ttu-id="dd456-170">На портале вы сможете добавлять таблицы и API-интерфейсы, а также изменять файлы кода серверной части Node.js.</span><span class="sxs-lookup"><span data-stu-id="dd456-170">You can add tables and APIs and edit code files for the Node.js backend in the portal.</span></span> <span data-ttu-id="dd456-171">С помощью различных инструментов развертывания вы можете скачать проект серверной части, чтобы добавить или изменить таблицы и интерфейсы API, а затем повторно опубликовать этот проект.</span><span class="sxs-lookup"><span data-stu-id="dd456-171">You can also use various deployment tools to download the backend project so that you can add or modify tables and APIs, then republish the project.</span></span> <span data-ttu-id="dd456-172">Дополнительные сведения см. в [руководстве по развертыванию службы приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="dd456-172">For more information, see the [Azure App Service Deployment Guide].</span></span> <span data-ttu-id="dd456-173">В следующей процедуре используется репозиторий Git для скачивания кода проекта быстрого запуска.</span><span class="sxs-lookup"><span data-stu-id="dd456-173">the following procedure uses a Git repository to download the quickstart project code.</span></span>

1. <span data-ttu-id="dd456-174">Установите Git, если его у вас еще нет.</span><span class="sxs-lookup"><span data-stu-id="dd456-174">Install Git, if you haven't already done so.</span></span> <span data-ttu-id="dd456-175">Действия, необходимые для установки Git, отличаются в разных операционных системах.</span><span class="sxs-lookup"><span data-stu-id="dd456-175">The steps required to install Git vary between operating systems.</span></span> <span data-ttu-id="dd456-176">Сведения о дистрибутивах для разных операционных систем и руководство по установке см. в разделе [Установка Git](http://git-scm.com/book/en/Getting-Started-Installing-Git).</span><span class="sxs-lookup"><span data-stu-id="dd456-176">See [Installing Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) for operating system-specific distributions and installation guidance.</span></span>
2. <span data-ttu-id="dd456-177">Выполните инструкции из раздела [Включение репозитория для приложения службы приложений](../app-service-web/app-service-deploy-local-git.md#Step3), чтобы включить репозиторий Git для сайта серверной части. Запишите имя пользователя и пароль для развертывания.</span><span class="sxs-lookup"><span data-stu-id="dd456-177">Follow the steps in [Enable the App Service app repository](../app-service-web/app-service-deploy-local-git.md#Step3) to enable the Git repository for your backend site, making a note of the deployment username and password.</span></span>
3. <span data-ttu-id="dd456-178">В колонке для серверной части мобильного приложения найдите параметр **URL-адрес клона Git** и запишите его.</span><span class="sxs-lookup"><span data-stu-id="dd456-178">In the blade for your Mobile App backend, make a note of the **Git clone URL** setting.</span></span>
4. <span data-ttu-id="dd456-179">Выполните команду `git clone`, указав URL-адрес клона Git, и введите пароль в ответ на запрос, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="dd456-179">Execute the `git clone` command using the Git clone URL, entering your password when required, as in the following example:</span></span>

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. <span data-ttu-id="dd456-180">Перейдите в локальный каталог (в приведенном выше примере это /todolist) и убедитесь, что файлы проекта скачаны.</span><span class="sxs-lookup"><span data-stu-id="dd456-180">Browse to local directory, which in the preceding example is /todolist, and notice that project files have been downloaded.</span></span> <span data-ttu-id="dd456-181">Найдите файл `todoitem.json` в каталоге `/tables`.</span><span class="sxs-lookup"><span data-stu-id="dd456-181">Locate the `todoitem.json` file in the `/tables` directory.</span></span>  <span data-ttu-id="dd456-182">Этот файл определяет разрешения для таблицы.</span><span class="sxs-lookup"><span data-stu-id="dd456-182">This file defines permissions on the table.</span></span>  <span data-ttu-id="dd456-183">В том же каталоге найдите файл `todoitem.js`, который определяет сценарии операций CRUD для таблицы.</span><span class="sxs-lookup"><span data-stu-id="dd456-183">Also find the `todoitem.js` file in the same directory, which defines that CRUD operation scripts for the table.</span></span>
6. <span data-ttu-id="dd456-184">После внесения изменений в файлы проекта выполните следующие команды, чтобы добавить, зафиксировать и передать изменения на сайт:</span><span class="sxs-lookup"><span data-stu-id="dd456-184">After you have made changes to project files, execute the following commands to add, commit, then upload the changes to the site:</span></span>

        $ git commit -m "updated the table script"
        $ git push origin master

    <span data-ttu-id="dd456-185">При добавлении новых файлов в проект необходимо сначала выполнить команду `git add .`.</span><span class="sxs-lookup"><span data-stu-id="dd456-185">When you add new files to the project, you first need to execute the `git add .` command.</span></span>

<span data-ttu-id="dd456-186">Каждый раз, когда на сайт помещается новый набор фиксаций, сайт повторно публикуется.</span><span class="sxs-lookup"><span data-stu-id="dd456-186">The site is republished every time a new set of commits is pushed to the site.</span></span>

### <span data-ttu-id="dd456-187"><a name="howto-publish-to-azure"></a>Публикация серверной части на основе Node.js в Azure</span><span class="sxs-lookup"><span data-stu-id="dd456-187"><a name="howto-publish-to-azure"></a>How to: Publish your Node.js backend to Azure</span></span>
<span data-ttu-id="dd456-188">Microsoft Azure предоставляет множество механизмов публикации серверной части на платформе Node.js для мобильных приложений службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="dd456-188">Microsoft Azure provides many mechanisms for publishing your Azure App Service Mobile Apps Node.js backend to the Azure service.</span></span>  <span data-ttu-id="dd456-189">К ним относятся инструменты развертывания, интегрированные в Visual Studio, программы командной строки и средства непрерывного развертывания на основе системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="dd456-189">These include utilizing deployment tools integrated into Visual Studio, command-line tools, and continuous deployment options based on source control.</span></span>  <span data-ttu-id="dd456-190">Дополнительные сведения по этой теме см. в [руководстве по развертыванию службы приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="dd456-190">For more information on this topic, see the [Azure App Service Deployment Guide].</span></span>

<span data-ttu-id="dd456-191">В отношении приложений на Node.js в службе приложений Azure существуют четкие рекомендации, с которыми вам следует ознакомиться перед развертыванием:</span><span class="sxs-lookup"><span data-stu-id="dd456-191">Azure App Service has specific advice for Node.js application that you should review before deploying:</span></span>

* <span data-ttu-id="dd456-192">[Указание версии Node]</span><span class="sxs-lookup"><span data-stu-id="dd456-192">How to [specify the Node Version]</span></span>
* <span data-ttu-id="dd456-193">[Использование модулей Node]</span><span class="sxs-lookup"><span data-stu-id="dd456-193">How to [use Node modules]</span></span>

### <span data-ttu-id="dd456-194"><a name="howto-enable-homepage"></a>Практическое руководство. Включение домашней страницы для приложения</span><span class="sxs-lookup"><span data-stu-id="dd456-194"><a name="howto-enable-homepage"></a>How to: Enable a Home Page for your application</span></span>
<span data-ttu-id="dd456-195">Многие приложения доступны в виде комбинации веб-приложений и мобильных приложений; платформа ExpressJS позволяет комбинировать эти компоненты.</span><span class="sxs-lookup"><span data-stu-id="dd456-195">Many applications are a combination of web and mobile apps and the ExpressJS framework allows you to combine the two facets.</span></span>  <span data-ttu-id="dd456-196">Тем не менее иногда нужно реализовать только мобильный интерфейс.</span><span class="sxs-lookup"><span data-stu-id="dd456-196">Sometimes, however, you may wish to only implement a mobile interface.</span></span>  <span data-ttu-id="dd456-197">Это полезно, когда нужно создать целевую страницу, чтобы проверить работоспособность службы приложений.</span><span class="sxs-lookup"><span data-stu-id="dd456-197">It is useful to provide a landing page to ensure the app service is up and running.</span></span>  <span data-ttu-id="dd456-198">Можно указать свою домашнюю страницу или включить временную.</span><span class="sxs-lookup"><span data-stu-id="dd456-198">You can either provide your own home page or enable a temporary home page.</span></span>  <span data-ttu-id="dd456-199">Чтобы включить временную домашнюю страницу, выполните следующую команду для создания экземпляра мобильных приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="dd456-199">To enable a temporary home page, use the following to instantiate Azure Mobile Apps:</span></span>

    var mobile = azureMobileApps({ homePage: true });

<span data-ttu-id="dd456-200">Если вам нужно использовать данную возможность только при локальной разработке, то этот параметр можно добавить в файл `azureMobile.js` .</span><span class="sxs-lookup"><span data-stu-id="dd456-200">If you only want this option available when developing locally, you can add this setting to your `azureMobile.js` file.</span></span>

## <span data-ttu-id="dd456-201"><a name="TableOperations"></a>Операции с таблицами</span><span class="sxs-lookup"><span data-stu-id="dd456-201"><a name="TableOperations"></a>Table operations</span></span>
<span data-ttu-id="dd456-202">Серверный пакет SDK azure-mobile-apps для Node.js предоставляет механизмы доступа через веб-интерфейсы к таблицам, хранящимся в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="dd456-202">The azure-mobile-apps Node.js Server SDK provides mechanisms to expose data tables stored in Azure SQL Database as a WebAPI.</span></span>  <span data-ttu-id="dd456-203">Пакетом предоставляются пять операций.</span><span class="sxs-lookup"><span data-stu-id="dd456-203">Five operations are provided.</span></span>

| <span data-ttu-id="dd456-204">Операция</span><span class="sxs-lookup"><span data-stu-id="dd456-204">Operation</span></span> | <span data-ttu-id="dd456-205">Описание</span><span class="sxs-lookup"><span data-stu-id="dd456-205">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dd456-206">GET /tables/*имя_таблицы*</span><span class="sxs-lookup"><span data-stu-id="dd456-206">GET /tables/*tablename*</span></span> |<span data-ttu-id="dd456-207">Получает все записи в таблице</span><span class="sxs-lookup"><span data-stu-id="dd456-207">Get all records in the table</span></span> |
| <span data-ttu-id="dd456-208">GET /tables/*имя_таблицы*/:id</span><span class="sxs-lookup"><span data-stu-id="dd456-208">GET /tables/*tablename*/:id</span></span> |<span data-ttu-id="dd456-209">Получает определенную запись из таблицы</span><span class="sxs-lookup"><span data-stu-id="dd456-209">Get a specific record in the table</span></span> |
| <span data-ttu-id="dd456-210">POST /tables/*имя_таблицы*</span><span class="sxs-lookup"><span data-stu-id="dd456-210">POST /tables/*tablename*</span></span> |<span data-ttu-id="dd456-211">Создает запись в таблице.</span><span class="sxs-lookup"><span data-stu-id="dd456-211">Create a record in the table</span></span> |
| <span data-ttu-id="dd456-212">PATCH /tables/*имя_таблицы*/:id</span><span class="sxs-lookup"><span data-stu-id="dd456-212">PATCH /tables/*tablename*/:id</span></span> |<span data-ttu-id="dd456-213">Обновляет запись в таблице.</span><span class="sxs-lookup"><span data-stu-id="dd456-213">Update a record in the table</span></span> |
| <span data-ttu-id="dd456-214">DELETE /tables/*имя_таблицы*/:id</span><span class="sxs-lookup"><span data-stu-id="dd456-214">DELETE /tables/*tablename*/:id</span></span> |<span data-ttu-id="dd456-215">Удаляет запись из таблицы</span><span class="sxs-lookup"><span data-stu-id="dd456-215">Delete a record in the table</span></span> |

<span data-ttu-id="dd456-216">Этот веб-API поддерживает протокол [OData] и расширяет схему таблицы для поддержки [автономной синхронизации данных].</span><span class="sxs-lookup"><span data-stu-id="dd456-216">This WebAPI supports [OData] and extends the table schema to support [offline data sync].</span></span>

### <span data-ttu-id="dd456-217"><a name="howto-dynamicschema"></a>Определение таблиц с помощью динамической схемы</span><span class="sxs-lookup"><span data-stu-id="dd456-217"><a name="howto-dynamicschema"></a>How to: Define tables using a dynamic schema</span></span>
<span data-ttu-id="dd456-218">Перед использованием таблицы ее необходимо определить.</span><span class="sxs-lookup"><span data-stu-id="dd456-218">Before a table can be used, it must be defined.</span></span>  <span data-ttu-id="dd456-219">Таблицы можно определять с помощью статических схем (когда разработчик определяет столбцы в схеме) или динамических схем (когда схема определяется пакетом SDK в зависимости от поступающих запросов).</span><span class="sxs-lookup"><span data-stu-id="dd456-219">Tables can be defined with a static schema (where the developer defines the columns within the schema) or dynamically (where the SDK controls the schema based on incoming requests).</span></span> <span data-ttu-id="dd456-220">Кроме того, разработчик может управлять некоторыми деталями работы WebAPI путем добавления в определение кода на JavaScript.</span><span class="sxs-lookup"><span data-stu-id="dd456-220">In addition, the developer can control specific aspects of the WebAPI by adding Javascript code to the definition.</span></span>

<span data-ttu-id="dd456-221">Рекомендуется определять все таблицы в отдельных файлах JavaScript и размещать их в каталоге tables, а затем использовать метод tables.import(), чтобы импортировать таблицы.</span><span class="sxs-lookup"><span data-stu-id="dd456-221">As a best practice, you should define each table in a Javascript file in the tables directory, then use the tables.import() method to import the tables.</span></span>  <span data-ttu-id="dd456-222">Расширим базовое приложение, изменив файл app.js:</span><span class="sxs-lookup"><span data-stu-id="dd456-222">Extending the basic-app, the app.js file would be adjusted:</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define the database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add the mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

<span data-ttu-id="dd456-223">Определение таблицы в файле ./tables/TodoItem.js:</span><span class="sxs-lookup"><span data-stu-id="dd456-223">Define the table in ./tables/TodoItem.js:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for the table goes here

    module.exports = table;

<span data-ttu-id="dd456-224">По умолчанию в таблицах используется динамическая схема.</span><span class="sxs-lookup"><span data-stu-id="dd456-224">Tables use dynamic schema by default.</span></span>  <span data-ttu-id="dd456-225">Чтобы глобально отключить динамическую схему, на портале Azure установите значение false для параметра приложения **MS_DynamicSchema**.</span><span class="sxs-lookup"><span data-stu-id="dd456-225">To turn off dynamic schema globally, set the App Setting **MS_DynamicSchema** to false within the Azure portal.</span></span>

<span data-ttu-id="dd456-226">Полный пример можно найти в [примере todo на GitHub].</span><span class="sxs-lookup"><span data-stu-id="dd456-226">You can find a complete example in the [todo sample on GitHub].</span></span>

### <span data-ttu-id="dd456-227"><a name="howto-staticschema"></a>Определение таблиц с помощью статической схемы</span><span class="sxs-lookup"><span data-stu-id="dd456-227"><a name="howto-staticschema"></a>How to: Define tables using a static schema</span></span>
<span data-ttu-id="dd456-228">Вы можете явным образом определять столбцы, которые будут предоставляться через WebAPI.</span><span class="sxs-lookup"><span data-stu-id="dd456-228">You can explicitly define the columns to expose via the WebAPI.</span></span>  <span data-ttu-id="dd456-229">Пакет SDK для Node.js (azure-mobile-apps) автоматически добавляет к вашему списку дополнительные столбцы, необходимые для автономной синхронизации данных.</span><span class="sxs-lookup"><span data-stu-id="dd456-229">The azure-mobile-apps Node.js SDK automatically adds any additional columns required for offline data sync to the list that you provide.</span></span>  <span data-ttu-id="dd456-230">Например, в примерах клиентских приложений требуется таблица с двумя столбцами: text (строка) и завершения complete (логическое значение).</span><span class="sxs-lookup"><span data-stu-id="dd456-230">For example, the QuickStart client applications require a table with two columns: text (a string) and complete (a boolean).</span></span>  
<span data-ttu-id="dd456-231">Эту таблицу можно указать в определении таблицы в файле JavaScript (расположен в каталоге tables) следующим образом.</span><span class="sxs-lookup"><span data-stu-id="dd456-231">The table can be defined in the table definition JavaScript file (located in the tables directory) as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

<span data-ttu-id="dd456-232">Если таблица определяется статически, то вам потребуется вызвать метод tables.initialize(), чтобы создать схему базы данных при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="dd456-232">If you define tables statically, then you must also call the tables.initialize() method to create the database schema on startup.</span></span>  <span data-ttu-id="dd456-233">Метод tables.initialize() возвращает объект [Promise] , чтобы веб-служба не начинала обслуживать запросы до инициализации базы данных.</span><span class="sxs-lookup"><span data-stu-id="dd456-233">The tables.initialize() method returns a [Promise] so that the web service does not serve requests before the database being initialized.</span></span>

### <span data-ttu-id="dd456-234"><a name="howto-sqlexpress-setup"></a>Использование SQL Express в качестве хранилища данных при разработке на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="dd456-234"><a name="howto-sqlexpress-setup"></a>How to: Use SQL Express as a development data store on your local machine</span></span>
<span data-ttu-id="dd456-235">Пакет SDK для мобильных приложений Azure на Node предоставляет три стандартных варианта обслуживания данных:</span><span class="sxs-lookup"><span data-stu-id="dd456-235">The Azure Mobile Apps The AzureMobile Apps Node SDK provides three options for serving data out of the box: SDK provides three options for serving data out of the box:</span></span>

* <span data-ttu-id="dd456-236">драйвер **memory** удобен для создания временного хранилища примеров;</span><span class="sxs-lookup"><span data-stu-id="dd456-236">Use the **memory** driver to provide a non-persistent example store</span></span>
* <span data-ttu-id="dd456-237">драйвер **mssql** с доступом к хранилищу данных SQL Express рекомендуется на этапе разработки;</span><span class="sxs-lookup"><span data-stu-id="dd456-237">Use the **mssql** driver to provide a SQL Express data store for development</span></span>
* <span data-ttu-id="dd456-238">драйвер **mssql** с доступом к хранилищу данных SQL Azure рекомендуется для рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="dd456-238">Use the **mssql** driver to provide an Azure SQL Database data store for production</span></span>

<span data-ttu-id="dd456-239">Пакет SDK для мобильных приложений Azure на основе Node.js использует пакет [mssql Node.js] для создания и использования подключения к базам данных обоих типов: SQL Express и базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="dd456-239">The Azure Mobile Apps Node.js SDK uses the [mssql Node.js package] to establish and use a connection to both SQL Express and SQL Database.</span></span>  <span data-ttu-id="dd456-240">Для использования этого пакета необходимо включить TCP-подключения в вашем экземпляре SQL Express.</span><span class="sxs-lookup"><span data-stu-id="dd456-240">This package requires that you enable TCP connections on your SQL Express instance.</span></span>

> [!TIP]
> <span data-ttu-id="dd456-241">Драйвер memory не предоставляет полный набор средств для тестирования.</span><span class="sxs-lookup"><span data-stu-id="dd456-241">The memory driver does not provide a complete set of facilities for testing.</span></span>  <span data-ttu-id="dd456-242">Для тестирования серверной части в локальном режиме рекомендуется использовать базу данных SQL Express и драйвер mssql.</span><span class="sxs-lookup"><span data-stu-id="dd456-242">If you wish to test your backend locally, we recommend the use of a SQL Express data store and the mssql driver.</span></span>
>
>

1. <span data-ttu-id="dd456-243">Загрузите и установите [Microsoft SQL Server 2014 Express].</span><span class="sxs-lookup"><span data-stu-id="dd456-243">Download and install [Microsoft SQL Server 2014 Express].</span></span>  <span data-ttu-id="dd456-244">Убедитесь, что устанавливается выпуск SQL Server 2014 Express с инструментами.</span><span class="sxs-lookup"><span data-stu-id="dd456-244">Ensure you install the SQL Server 2014 Express with Tools edition.</span></span>  <span data-ttu-id="dd456-245">Если вам явно не требуется 64-разрядная версия, воспользуйтесь 32-разрядной версией, которая потребляет меньше памяти во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="dd456-245">Unless you explicitly require 64-bit support, the 32-bit version consumes less memory when running.</span></span>
2. <span data-ttu-id="dd456-246">Запустите диспетчер конфигурации SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="dd456-246">Run the SQL Server 2014 Configuration Manager.</span></span>

   1. <span data-ttu-id="dd456-247">Разверните узел **Сетевая конфигурация SQL Server** в дереве слева.</span><span class="sxs-lookup"><span data-stu-id="dd456-247">Expand the **SQL Server Network Configuration** node in the left-hand tree menu.</span></span>
   2. <span data-ttu-id="dd456-248">Выберите **Протоколы для SQLEXPRESS**.</span><span class="sxs-lookup"><span data-stu-id="dd456-248">Click **Protocols for SQLEXPRESS**.</span></span>
   3. <span data-ttu-id="dd456-249">Щелкните правой кнопкой мыши **TCP/IP** и выберите **Включить**.</span><span class="sxs-lookup"><span data-stu-id="dd456-249">Right-click **TCP/IP** and select **Enable**.</span></span>  <span data-ttu-id="dd456-250">Нажмите кнопку **ОК** во всплывающем диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="dd456-250">Click **OK** in the pop-up dialog.</span></span>
   4. <span data-ttu-id="dd456-251">Щелкните правой кнопкой мыши **TCP/IP** и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="dd456-251">Right-click **TCP/IP** and select **Properties**.</span></span>
   5. <span data-ttu-id="dd456-252">Откройте вкладку **IP-адреса** .</span><span class="sxs-lookup"><span data-stu-id="dd456-252">Click the **IP Addresses** tab.</span></span>
   6. <span data-ttu-id="dd456-253">Найдите узел **IPAll** .</span><span class="sxs-lookup"><span data-stu-id="dd456-253">Find the **IPAll** node.</span></span>  <span data-ttu-id="dd456-254">В поле **TCP-порт** введите **1433**.</span><span class="sxs-lookup"><span data-stu-id="dd456-254">In the **TCP Port** field, enter **1433**.</span></span>

          ![Configure SQL Express for TCP/IP][3]
   7. <span data-ttu-id="dd456-255">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dd456-255">Click **OK**.</span></span>  <span data-ttu-id="dd456-256">Нажмите кнопку **ОК** во всплывающем диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="dd456-256">Click **OK** in the pop-up dialog.</span></span>
   8. <span data-ttu-id="dd456-257">В дереве слева выберите **Службы SQL Server** .</span><span class="sxs-lookup"><span data-stu-id="dd456-257">Click **SQL Server Services** in the left-hand tree menu.</span></span>
   9. <span data-ttu-id="dd456-258">Щелкните правой кнопкой мыши **SQL Server (SQLEXPRESS)** и выберите **Перезапустить**.</span><span class="sxs-lookup"><span data-stu-id="dd456-258">Right-click **SQL Server (SQLEXPRESS)** and select **Restart**</span></span>
   10. <span data-ttu-id="dd456-259">Закройте диспетчер конфигурации SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="dd456-259">Close the SQL Server 2014 Configuration Manager.</span></span>
3. <span data-ttu-id="dd456-260">Запустите SQL Server 2014 Management Studio и подключитесь к локальному экземпляру SQL Express.</span><span class="sxs-lookup"><span data-stu-id="dd456-260">Run the SQL Server 2014 Management Studio and connect to your local SQL Express instance</span></span>

   1. <span data-ttu-id="dd456-261">Щелкните правой кнопкой мыши экземпляр SQL Express в обозревателе объектов и выберите **Свойства**</span><span class="sxs-lookup"><span data-stu-id="dd456-261">Right-click your instance in the Object Explorer and select **Properties**</span></span>
   2. <span data-ttu-id="dd456-262">Перейдите на страницу **Безопасность** .</span><span class="sxs-lookup"><span data-stu-id="dd456-262">Select the **Security** page.</span></span>
   3. <span data-ttu-id="dd456-263">Убедитесь, что выбран режим **Проверка подлинности SQL Server и Windows** .</span><span class="sxs-lookup"><span data-stu-id="dd456-263">Ensure the **SQL Server and Windows Authentication mode** is selected</span></span>
   4. <span data-ttu-id="dd456-264">Нажмите кнопку **ОК**</span><span class="sxs-lookup"><span data-stu-id="dd456-264">Click **OK**</span></span>

          ![Configure SQL Express Authentication][4]
   5. <span data-ttu-id="dd456-265">Разверните узел **Безопасность** > **Имена входа** .</span><span class="sxs-lookup"><span data-stu-id="dd456-265">Expand **Security** > **Logins** in the Object Explorer</span></span>
   6. <span data-ttu-id="dd456-266">Щелкните правой кнопкой мыши пункт **Имена входа** и выберите **Создать имя входа**.</span><span class="sxs-lookup"><span data-stu-id="dd456-266">Right-click **Logins** and select **New Login...**</span></span>
   7. <span data-ttu-id="dd456-267">Введите имя входа.</span><span class="sxs-lookup"><span data-stu-id="dd456-267">Enter a Login name.</span></span>  <span data-ttu-id="dd456-268">Выберите **Проверка подлинности SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="dd456-268">Select **SQL Server authentication**.</span></span>  <span data-ttu-id="dd456-269">Введите пароль, а затем в поле **Подтверждение пароля** введите пароль еще раз.</span><span class="sxs-lookup"><span data-stu-id="dd456-269">Enter a Password, then enter the same password in **Confirm password**.</span></span>  <span data-ttu-id="dd456-270">Пароль должен соответствовать требованиям к сложности паролей, установленным в Windows.</span><span class="sxs-lookup"><span data-stu-id="dd456-270">The password must meet Windows complexity requirements.</span></span>
   8. <span data-ttu-id="dd456-271">Нажмите кнопку **ОК**</span><span class="sxs-lookup"><span data-stu-id="dd456-271">Click **OK**</span></span>

          ![Add a new user to SQL Express][5]
   9. <span data-ttu-id="dd456-272">Щелкните правой кнопкой мыши новое имя для входа и выберите **Свойства**</span><span class="sxs-lookup"><span data-stu-id="dd456-272">Right-click your new login and select **Properties**</span></span>
   10. <span data-ttu-id="dd456-273">Перейдите на страницу **Роли сервера** .</span><span class="sxs-lookup"><span data-stu-id="dd456-273">Select the **Server Roles** page</span></span>
   11. <span data-ttu-id="dd456-274">Установите флажок рядом с ролью **dbcreator** .</span><span class="sxs-lookup"><span data-stu-id="dd456-274">Check the box next to the **dbcreator** server role</span></span>
   12. <span data-ttu-id="dd456-275">Нажмите кнопку **ОК**</span><span class="sxs-lookup"><span data-stu-id="dd456-275">Click **OK**</span></span>
   13. <span data-ttu-id="dd456-276">Закройте SQL Server 2015 Management Studio.</span><span class="sxs-lookup"><span data-stu-id="dd456-276">Close the SQL Server 2015 Management Studio</span></span>

<span data-ttu-id="dd456-277">Запишите имя созданного пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="dd456-277">Ensure you record the username and password you selected.</span></span>  <span data-ttu-id="dd456-278">В зависимости от требований конкретной базы данных, вам может потребоваться назначить дополнительные роли сервера или разрешения.</span><span class="sxs-lookup"><span data-stu-id="dd456-278">You may need to assign additional server roles or permissions depending on your specific database requirements.</span></span>

<span data-ttu-id="dd456-279">Для получения строки подключения к этой базе данных приложение Node.js обращается к переменной среды **SQLCONNSTR_MS_TableConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="dd456-279">The Node.js application reads the **SQLCONNSTR_MS_TableConnectionString** environment variable for the connection string for this database.</span></span>  <span data-ttu-id="dd456-280">Значение этой переменной можно задать непосредственно в своей среде.</span><span class="sxs-lookup"><span data-stu-id="dd456-280">You can set this variable within your environment.</span></span>  <span data-ttu-id="dd456-281">Например, чтобы присвоить этой переменной значение, вы можете воспользоваться следующей командой PowerShell:</span><span class="sxs-lookup"><span data-stu-id="dd456-281">For example, you can use PowerShell to set this environment variable:</span></span>

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

<span data-ttu-id="dd456-282">Доступ к базе данных осуществляется через подключение TCP/IP, и для этого подключения требуется указать имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="dd456-282">Access the database through a TCP/IP connection and provide a username and password for the connection.</span></span>

### <span data-ttu-id="dd456-283"><a name="howto-config-localdev"></a>Настройка проекта для локальной разработки</span><span class="sxs-lookup"><span data-stu-id="dd456-283"><a name="howto-config-localdev"></a>How to: Configure your project for local development</span></span>
<span data-ttu-id="dd456-284">Мобильные приложения Azure считывают файл JavaScript с именем *azureMobile.js* из локальной файловой системы.</span><span class="sxs-lookup"><span data-stu-id="dd456-284">Azure Mobile Apps reads a JavaScript file called *azureMobile.js* from the local filesystem.</span></span>  <span data-ttu-id="dd456-285">В рабочей среде не следует использовать этот файл для настройки пакета SDK для мобильных приложений Azure. Вместо этого используйте параметры приложения на [портале Azure].</span><span class="sxs-lookup"><span data-stu-id="dd456-285">Do not use this file to configure the Azure Mobile Apps SDK in production - use App Settings within the [Azure portal] instead.</span></span>  <span data-ttu-id="dd456-286">Файл *azureMobile.js* должен экспортировать объект конфигурации.</span><span class="sxs-lookup"><span data-stu-id="dd456-286">The *azureMobile.js* file should export a configuration object.</span></span>  <span data-ttu-id="dd456-287">Ниже перечислены основные параметры.</span><span class="sxs-lookup"><span data-stu-id="dd456-287">The most common settings are:</span></span>

* <span data-ttu-id="dd456-288">Параметры базы данных</span><span class="sxs-lookup"><span data-stu-id="dd456-288">Database Settings</span></span>
* <span data-ttu-id="dd456-289">Параметры ведения журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="dd456-289">Diagnostic Logging Settings</span></span>
* <span data-ttu-id="dd456-290">Дополнительные параметры CORS</span><span class="sxs-lookup"><span data-stu-id="dd456-290">Alternate CORS Settings</span></span>

<span data-ttu-id="dd456-291">Ниже приведен пример файла *azureMobile.js* , реализующего указанные выше параметры базы данных.</span><span class="sxs-lookup"><span data-stu-id="dd456-291">An example *azureMobile.js* file implementing the preceding database settings follows:</span></span>

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

<span data-ttu-id="dd456-292">Мы рекомендуем добавить *azureMobile.js* в *GITIGNORE*-файл (или в другой файл игнорирования для системы управления исходным кодом), чтобы не допустить сохранения паролей в облаке.</span><span class="sxs-lookup"><span data-stu-id="dd456-292">We recommend that you add *azureMobile.js* to your *.gitignore* file (or other source code control ignore file) to prevent passwords from being stored in the cloud.</span></span>  <span data-ttu-id="dd456-293">Параметры рабочей версии всегда следует настраивать в разделе "Параметры приложения" на [портале Azure].</span><span class="sxs-lookup"><span data-stu-id="dd456-293">Always configure production settings in App Settings within the [Azure portal].</span></span>

### <span data-ttu-id="dd456-294"><a name="howto-appsettings"></a>Практическое руководство. Настройка параметров для мобильного приложения</span><span class="sxs-lookup"><span data-stu-id="dd456-294"><a name="howto-appsettings"></a>How: Configure App Settings for your Mobile App</span></span>
<span data-ttu-id="dd456-295">Для большинства параметров в файле *azureMobile.js* имеется эквивалентный параметр приложения на [портале Azure].</span><span class="sxs-lookup"><span data-stu-id="dd456-295">Most settings in the *azureMobile.js* file have an equivalent App Setting in the [Azure portal].</span></span>  <span data-ttu-id="dd456-296">Используйте следующий список, чтобы настроить свое приложение в параметрах приложения:</span><span class="sxs-lookup"><span data-stu-id="dd456-296">Use the following list to configure your app in App Settings:</span></span>

| <span data-ttu-id="dd456-297">Параметр приложения</span><span class="sxs-lookup"><span data-stu-id="dd456-297">App Setting</span></span> | <span data-ttu-id="dd456-298">*azureMobile.js* </span><span class="sxs-lookup"><span data-stu-id="dd456-298">*azureMobile.js* Setting</span></span> | <span data-ttu-id="dd456-299">Описание</span><span class="sxs-lookup"><span data-stu-id="dd456-299">Description</span></span> | <span data-ttu-id="dd456-300">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="dd456-300">Valid Values</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="dd456-301">**MS_MobileAppName**</span><span class="sxs-lookup"><span data-stu-id="dd456-301">**MS_MobileAppName**</span></span> |<span data-ttu-id="dd456-302">name</span><span class="sxs-lookup"><span data-stu-id="dd456-302">name</span></span> |<span data-ttu-id="dd456-303">Имя приложения</span><span class="sxs-lookup"><span data-stu-id="dd456-303">The name of the app</span></span> |<span data-ttu-id="dd456-304">string</span><span class="sxs-lookup"><span data-stu-id="dd456-304">string</span></span> |
| <span data-ttu-id="dd456-305">**MS_MobileLoggingLevel**</span><span class="sxs-lookup"><span data-stu-id="dd456-305">**MS_MobileLoggingLevel**</span></span> |<span data-ttu-id="dd456-306">logging.level</span><span class="sxs-lookup"><span data-stu-id="dd456-306">logging.level</span></span> |<span data-ttu-id="dd456-307">Минимальный уровень ведения журнала для регистрируемых сообщений</span><span class="sxs-lookup"><span data-stu-id="dd456-307">Minimum log level of messages to log</span></span> |<span data-ttu-id="dd456-308">error, warning, info, verbose, debug, silly</span><span class="sxs-lookup"><span data-stu-id="dd456-308">error, warning, info, verbose, debug, silly</span></span> |
| <span data-ttu-id="dd456-309">**MS_DebugMode**</span><span class="sxs-lookup"><span data-stu-id="dd456-309">**MS_DebugMode**</span></span> |<span data-ttu-id="dd456-310">debug</span><span class="sxs-lookup"><span data-stu-id="dd456-310">debug</span></span> |<span data-ttu-id="dd456-311">Включение или отключение режима отладки</span><span class="sxs-lookup"><span data-stu-id="dd456-311">Enable or Disable debug mode</span></span> |<span data-ttu-id="dd456-312">true, false</span><span class="sxs-lookup"><span data-stu-id="dd456-312">true, false</span></span> |
| <span data-ttu-id="dd456-313">**MS_TableSchema**</span><span class="sxs-lookup"><span data-stu-id="dd456-313">**MS_TableSchema**</span></span> |<span data-ttu-id="dd456-314">data.schema</span><span class="sxs-lookup"><span data-stu-id="dd456-314">data.schema</span></span> |<span data-ttu-id="dd456-315">Имя схемы по умолчанию для таблиц SQL</span><span class="sxs-lookup"><span data-stu-id="dd456-315">Default schema name for SQL tables</span></span> |<span data-ttu-id="dd456-316">строка (значение по умолчанию: dbo)</span><span class="sxs-lookup"><span data-stu-id="dd456-316">string (default: dbo)</span></span> |
| <span data-ttu-id="dd456-317">**MS_DynamicSchema**</span><span class="sxs-lookup"><span data-stu-id="dd456-317">**MS_DynamicSchema**</span></span> |<span data-ttu-id="dd456-318">data.dynamicSchema</span><span class="sxs-lookup"><span data-stu-id="dd456-318">data.dynamicSchema</span></span> |<span data-ttu-id="dd456-319">Включение или отключение режима отладки</span><span class="sxs-lookup"><span data-stu-id="dd456-319">Enable or Disable debug mode</span></span> |<span data-ttu-id="dd456-320">true, false</span><span class="sxs-lookup"><span data-stu-id="dd456-320">true, false</span></span> |
| <span data-ttu-id="dd456-321">**MS_DisableVersionHeader**</span><span class="sxs-lookup"><span data-stu-id="dd456-321">**MS_DisableVersionHeader**</span></span> |<span data-ttu-id="dd456-322">version (задано значение undefined)</span><span class="sxs-lookup"><span data-stu-id="dd456-322">version (set to undefined)</span></span> |<span data-ttu-id="dd456-323">Отключение заголовка X-ZUMO-Server-Version</span><span class="sxs-lookup"><span data-stu-id="dd456-323">Disables the X-ZUMO-Server-Version header</span></span> |<span data-ttu-id="dd456-324">true, false</span><span class="sxs-lookup"><span data-stu-id="dd456-324">true, false</span></span> |
| <span data-ttu-id="dd456-325">**MS_SkipVersionCheck**</span><span class="sxs-lookup"><span data-stu-id="dd456-325">**MS_SkipVersionCheck**</span></span> |<span data-ttu-id="dd456-326">skipversioncheck</span><span class="sxs-lookup"><span data-stu-id="dd456-326">skipversioncheck</span></span> |<span data-ttu-id="dd456-327">Отключение проверки версии API клиента</span><span class="sxs-lookup"><span data-stu-id="dd456-327">Disables the client API version check</span></span> |<span data-ttu-id="dd456-328">true, false</span><span class="sxs-lookup"><span data-stu-id="dd456-328">true, false</span></span> |

<span data-ttu-id="dd456-329">Порядок задания параметра приложения:</span><span class="sxs-lookup"><span data-stu-id="dd456-329">To set an App Setting:</span></span>

1. <span data-ttu-id="dd456-330">Войдите на [портале Azure].</span><span class="sxs-lookup"><span data-stu-id="dd456-330">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="dd456-331">Выберите **Все ресурсы** или **Службы приложений**, а затем щелкните имя своего мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="dd456-331">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="dd456-332">По умолчанию откроется колонка "Параметры".</span><span class="sxs-lookup"><span data-stu-id="dd456-332">The Settings blade opens by default.</span></span> <span data-ttu-id="dd456-333">В противном случае щелкните **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="dd456-333">If it doesn't, click **Settings**.</span></span>
4. <span data-ttu-id="dd456-334">В меню "Общие" щелкните **Параметры приложения** .</span><span class="sxs-lookup"><span data-stu-id="dd456-334">Click **Application settings** in the GENERAL menu.</span></span>
5. <span data-ttu-id="dd456-335">Выполните прокрутку вниз до раздела "Параметры приложения".</span><span class="sxs-lookup"><span data-stu-id="dd456-335">Scroll to the App Settings section.</span></span>
6. <span data-ttu-id="dd456-336">Если параметр приложения уже существует, щелкните значение этого параметра, чтобы изменить его.</span><span class="sxs-lookup"><span data-stu-id="dd456-336">If your app setting already exists, click the value of the app setting to edit the value.</span></span>
7. <span data-ttu-id="dd456-337">Если параметр приложения не существует, введите параметр в поле "Ключ" и значение в поле "Значение".</span><span class="sxs-lookup"><span data-stu-id="dd456-337">If your app setting does not exist, enter the App Setting in the Key box and the value in the Value box.</span></span>
8. <span data-ttu-id="dd456-338">После завершения нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="dd456-338">Once you are complete, click **Save**.</span></span>

<span data-ttu-id="dd456-339">Для большинства параметров после внесения изменений потребуется перезапустить службу.</span><span class="sxs-lookup"><span data-stu-id="dd456-339">Changing most app settings requires a service restart.</span></span>

### <span data-ttu-id="dd456-340"><a name="howto-use-sqlazure"></a>Практическое руководство. Использование базы данных SQL для хранения данных в рабочей среде</span><span class="sxs-lookup"><span data-stu-id="dd456-340"><a name="howto-use-sqlazure"></a>How to: Use SQL Database as your production data store</span></span>
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

<span data-ttu-id="dd456-341">Порядок использования базы данных SQL в качестве хранилища данных идентичен для всех типов приложений службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="dd456-341">Using Azure SQL Database as a data store is identical across all Azure App Service application types.</span></span> <span data-ttu-id="dd456-342">Если вы этого еще не сделали, создайте серверную часть мобильного приложения, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="dd456-342">If you have not done so already, follow these steps to create a Mobile App backend.</span></span>

1. <span data-ttu-id="dd456-343">Войдите на [портале Azure].</span><span class="sxs-lookup"><span data-stu-id="dd456-343">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="dd456-344">В верхнем левом углу окна нажмите кнопку **+ создать** кнопку > **Интернет + мобильные устройства** > **мобильное приложение**, затем введите имя для мобильного приложения серверной части.</span><span class="sxs-lookup"><span data-stu-id="dd456-344">In the top left of the window, click the **+NEW** button > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="dd456-345">В окне **Группа ресурсов** введите имя своего приложения.</span><span class="sxs-lookup"><span data-stu-id="dd456-345">In the **Resource Group** box, enter the same name as your app.</span></span>
4. <span data-ttu-id="dd456-346">Будет выбран план службы приложений по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="dd456-346">The Default App Service plan is selected.</span></span>  <span data-ttu-id="dd456-347">Если вы хотите изменить план службы приложений, выберите "План службы приложений" > **+ Создать**.</span><span class="sxs-lookup"><span data-stu-id="dd456-347">If you wish to change your App Service plan, you can do so by clicking the App Service Plan > **+ Create New**.</span></span>  <span data-ttu-id="dd456-348">Введите имя нового плана службы приложений и выберите подходящее расположение.</span><span class="sxs-lookup"><span data-stu-id="dd456-348">Provide a name of the new App Service plan and select an appropriate location.</span></span>  <span data-ttu-id="dd456-349">Щелкните "Ценовая категория" и выберите соответствующую категорию для своей службы.</span><span class="sxs-lookup"><span data-stu-id="dd456-349">Click the Pricing tier and select an appropriate pricing tier for the service.</span></span> <span data-ttu-id="dd456-350">Щелкните **Просмотреть все**, чтобы просмотреть другие варианты тарификации, например **Бесплатный** и **Общий**.</span><span class="sxs-lookup"><span data-stu-id="dd456-350">Select **View all** to view more pricing options, such as **Free** and **Shared**.</span></span>  <span data-ttu-id="dd456-351">Выберите ценовую категорию и нажмите кнопку **Выбрать** .</span><span class="sxs-lookup"><span data-stu-id="dd456-351">Once you have selected the pricing tier, click the **Select** button.</span></span>  <span data-ttu-id="dd456-352">В колонке **План службы приложений** нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dd456-352">Back in the **App Service plan** blade, click **OK**.</span></span>
5. <span data-ttu-id="dd456-353">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dd456-353">Click **Create**.</span></span> <span data-ttu-id="dd456-354">Подготовка серверной части мобильного приложения может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="dd456-354">Provisioning a Mobile App backend can take a couple of minutes.</span></span>  <span data-ttu-id="dd456-355">Когда серверная часть мобильного приложения будет подготовлена, на портале для нее откроется колонка **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="dd456-355">Once the Mobile App backend is provisioned, the portal opens the **Settings** blade for the Mobile App backend.</span></span>

<span data-ttu-id="dd456-356">Создав серверную часть мобильного приложения, вы можете подключить ее к существующей базе данных SQL либо создать новую базу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="dd456-356">Once the Mobile App backend is created, you can choose to either connect an existing SQL database to your Mobile App backend or create a new SQL database.</span></span>  <span data-ttu-id="dd456-357">В этом разделе мы создадим базу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="dd456-357">In this section, we create a SQL database.</span></span>

> [!NOTE]
> <span data-ttu-id="dd456-358">Если у вас уже есть база данных в том же расположении, что и серверная часть мобильного приложения, то вы можете выбрать эту базу данных, щелкнув **Использовать существующую базу данных** .</span><span class="sxs-lookup"><span data-stu-id="dd456-358">If you already have a database in the same location as the mobile app backend, you can instead choose **Use an existing database** and then select that database.</span></span> <span data-ttu-id="dd456-359">Ввиду более длительных задержек не рекомендуется использовать базу данных в другом расположении.</span><span class="sxs-lookup"><span data-stu-id="dd456-359">The use of a database in a different location is not recommended because of higher latencies.</span></span>
>
>

1. <span data-ttu-id="dd456-360">В новой серверной части мобильного приложения щелкните **Параметры** > **Мобильное приложение** > **Данные** > **+Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dd456-360">In the new Mobile App backend, click **Settings** > **Mobile App** > **Data** > **+Add**.</span></span>
2. <span data-ttu-id="dd456-361">В колонке **Добавить подключение данных** щелкните **База данных SQL — Настройка обязательных параметров** > **Создать новую базу данных**.</span><span class="sxs-lookup"><span data-stu-id="dd456-361">In the **Add data connection** blade, click **SQL Database - Configure required settings** > **Create a new database**.</span></span>  <span data-ttu-id="dd456-362">Введите имя новой базы данных в поле **Имя** .</span><span class="sxs-lookup"><span data-stu-id="dd456-362">Enter the name of the new database in the **Name** field.</span></span>
3. <span data-ttu-id="dd456-363">Щелкните **Сервер**.</span><span class="sxs-lookup"><span data-stu-id="dd456-363">Click **Server**.</span></span>  <span data-ttu-id="dd456-364">В колонке **Новый сервер** введите уникальное имя сервера в поле **Имя сервера** и укажите подходящие **имя администратора сервера** и **пароль**.</span><span class="sxs-lookup"><span data-stu-id="dd456-364">In the **New server** blade, enter a unique server name in the **Server name** field, and provide a suitable **Server admin login** and **Password**.</span></span>  <span data-ttu-id="dd456-365">Убедитесь, что установлен флажок напротив пункта **Разрешить службам Azure доступ к серверу** .</span><span class="sxs-lookup"><span data-stu-id="dd456-365">Ensure **Allow azure services to access server** is checked.</span></span>  <span data-ttu-id="dd456-366">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dd456-366">Click **OK**.</span></span>

    ![Создание базы данных SQL Azure][6]
4. <span data-ttu-id="dd456-368">В колонке **Новая база данных** нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dd456-368">On the **New database** blade, click **OK**.</span></span>
5. <span data-ttu-id="dd456-369">В колонке **Add data connection** (Добавление подключения данных) выберите **Строка подключения** и введите имя и пароль, указанные при создании базы данных.</span><span class="sxs-lookup"><span data-stu-id="dd456-369">Back on the **Add data connection** blade, select **Connection string**, enter the login and password that you provided when creating the database.</span></span>  <span data-ttu-id="dd456-370">При использовании существующей базы данных укажите соответствующие учетные данные для входа.</span><span class="sxs-lookup"><span data-stu-id="dd456-370">If you use an existing database, provide the login credentials for that database.</span></span>  <span data-ttu-id="dd456-371">Выполнив вход, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dd456-371">Once entered, click **OK**.</span></span>
6. <span data-ttu-id="dd456-372">В колонке **Add data connection** (Добавление подключения данных) снова нажмите кнопку **ОК**, чтобы создать базу данных.</span><span class="sxs-lookup"><span data-stu-id="dd456-372">Back on the **Add data connection** blade again, click **OK** to create the database.</span></span>

<!--- END OF ALTERNATE INCLUDE -->

<span data-ttu-id="dd456-373">Создание базы данных может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="dd456-373">Creation of the database can take a few minutes.</span></span>  <span data-ttu-id="dd456-374">Используйте область **Уведомления** , чтобы отслеживать ход выполнения развертывания.</span><span class="sxs-lookup"><span data-stu-id="dd456-374">Use the **Notifications** area to monitor the progress of the deployment.</span></span>  <span data-ttu-id="dd456-375">Не выполняйте дальнейших действий, пока база данных не будет успешно развернута.</span><span class="sxs-lookup"><span data-stu-id="dd456-375">Do not progress until the database has been deployed successfully.</span></span>  <span data-ttu-id="dd456-376">После завершения развертывания в настройки серверной части мобильного приложения будет добавлена строка подключения к экземпляру базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="dd456-376">Once successfully deployed, a Connection String is created for the SQL Database instance in your Mobile backend App Settings.</span></span>  <span data-ttu-id="dd456-377">Эту настройку можно увидеть, выбрав **Параметры** > **Параметры приложения** > **Строки подключения**.</span><span class="sxs-lookup"><span data-stu-id="dd456-377">You can see this app setting in the **Settings** > **Application settings** > **Connection strings**.</span></span>

### <span data-ttu-id="dd456-378"><a name="howto-tables-auth"></a>Практическое руководство. Обязательная аутентификация для доступа к таблицам</span><span class="sxs-lookup"><span data-stu-id="dd456-378"><a name="howto-tables-auth"></a>How to: Require authentication for access to tables</span></span>
<span data-ttu-id="dd456-379">Если вы хотите использовать аутентификацию службы приложений для конечной точки таблиц, сначала нужно настроить аутентификацию службы приложений на [портале Azure] .</span><span class="sxs-lookup"><span data-stu-id="dd456-379">If you wish to use App Service Authentication with the tables endpoint, you must configure App Service Authentication in the [Azure portal] first.</span></span>  <span data-ttu-id="dd456-380">Дополнительные сведения о настройке проверки подлинности в службе приложений Azure приведены в руководстве по настройке соответствующего поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="dd456-380">For more details about configuring authentication in an Azure App Service, review the Configuration Guide for the identity provider you intend to use:</span></span>

* <span data-ttu-id="dd456-381">[Настройка проверки подлинности в Azure Active Directory.]</span><span class="sxs-lookup"><span data-stu-id="dd456-381">[How to configure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="dd456-382">[Настройка проверки подлинности в Facebook.]</span><span class="sxs-lookup"><span data-stu-id="dd456-382">[How to configure Facebook Authentication]</span></span>
* <span data-ttu-id="dd456-383">[Настройка проверки подлинности в Google.]</span><span class="sxs-lookup"><span data-stu-id="dd456-383">[How to configure Google Authentication]</span></span>
* <span data-ttu-id="dd456-384">[Настройка проверки подлинности в Microsoft.]</span><span class="sxs-lookup"><span data-stu-id="dd456-384">[How to configure Microsoft Authentication]</span></span>
* <span data-ttu-id="dd456-385">[Настройка проверки подлинности в Twitter.]</span><span class="sxs-lookup"><span data-stu-id="dd456-385">[How to configure Twitter Authentication]</span></span>

<span data-ttu-id="dd456-386">В каждой таблице имеется свойство доступа (access), которое можно использовать для контроля доступа к таблице.</span><span class="sxs-lookup"><span data-stu-id="dd456-386">Each table has an access property that can be used to control access to the table.</span></span>  <span data-ttu-id="dd456-387">В следующем примере показана статически определенная таблица с обязательной проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="dd456-387">The following sample shows a statically defined table with authentication required.</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="dd456-388">Свойство access может принимать одно из трех значений:</span><span class="sxs-lookup"><span data-stu-id="dd456-388">The access property can take one of three values</span></span>

* <span data-ttu-id="dd456-389">*anonymous* указывает, что клиентское приложение может считывать данные без проверки подлинности;</span><span class="sxs-lookup"><span data-stu-id="dd456-389">*anonymous* indicates that the client application is allowed to read data without authentication</span></span>
* <span data-ttu-id="dd456-390">*authenticated* указывает, что клиентское приложение вместе с запросом должно отправлять действительный токен проверки подлинности;</span><span class="sxs-lookup"><span data-stu-id="dd456-390">*authenticated* indicates that the client application must send a valid authentication token with the request</span></span>
* <span data-ttu-id="dd456-391">*disabled* указывает, что эта таблица сейчас отключена.</span><span class="sxs-lookup"><span data-stu-id="dd456-391">*disabled* indicates that this table is currently disabled</span></span>

<span data-ttu-id="dd456-392">Если свойство доступа нельзя определить, будет разрешен доступ без проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="dd456-392">If the access property is undefined, unauthenticated access is allowed.</span></span>

### <span data-ttu-id="dd456-393"><a name="howto-tables-getidentity"></a>Практическое руководство. Использование утверждений аутентификации для таблиц</span><span class="sxs-lookup"><span data-stu-id="dd456-393"><a name="howto-tables-getidentity"></a>How to: Use authentication claims with your tables</span></span>
<span data-ttu-id="dd456-394">Можно настроить различные утверждения, запрашиваемые при настройке аутентификации.</span><span class="sxs-lookup"><span data-stu-id="dd456-394">You can set up various claims that are requested when authentication is set up.</span></span>  <span data-ttu-id="dd456-395">Обычно эти утверждения недоступны через объект `context.user` .</span><span class="sxs-lookup"><span data-stu-id="dd456-395">These claims are not normally available through the `context.user` object.</span></span>  <span data-ttu-id="dd456-396">Тем не менее их можно извлечь с помощью метода `context.user.getIdentity()` .</span><span class="sxs-lookup"><span data-stu-id="dd456-396">However, they can be retrieved using the `context.user.getIdentity()` method.</span></span>  <span data-ttu-id="dd456-397">Метод `getIdentity()` возвращает обещание, которое разрешается в объект.</span><span class="sxs-lookup"><span data-stu-id="dd456-397">The `getIdentity()` method returns a Promise that resolves to an object.</span></span>  <span data-ttu-id="dd456-398">Объект помечается ключом метода аутентификации (facebook, google, twitter, microsoftaccount или aad).</span><span class="sxs-lookup"><span data-stu-id="dd456-398">The object is keyed by the authentication method (facebook, google, twitter, microsoftaccount, or aad).</span></span>

<span data-ttu-id="dd456-399">Например, если вы настраиваете аутентификацию учетных записей Майкрософт и запрашиваете утверждение электронного адреса, то можете добавить электронный адрес в запись с помощью следующего контроллера таблиц.</span><span class="sxs-lookup"><span data-stu-id="dd456-399">For example, if you set up Microsoft Account authentication and request the email addresses claim, you can add the email address to the record with the following table controller:</span></span>

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
    * Limit the context query to those records with the authenticated user email address
    * @param {Context} context the operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds the email address from the claims to the context item - used for
    * insert operations
    * @param {Context} context the operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when the client does a request
    // READ - only return records belonging to the authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite the userId based on the authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong to the authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong to the authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

<span data-ttu-id="dd456-400">Чтобы узнать, какие утверждения доступны, используйте веб-браузер для просмотра конечной точки `/.auth/me` своего сайта.</span><span class="sxs-lookup"><span data-stu-id="dd456-400">To see what claims are available, use a web browser to view the `/.auth/me` endpoint of your site.</span></span>

### <span data-ttu-id="dd456-401"><a name="howto-tables-disabled"></a>Практическое руководство. Запрет доступа к определенным операциям с таблицей</span><span class="sxs-lookup"><span data-stu-id="dd456-401"><a name="howto-tables-disabled"></a>How to: Disable access to specific table operations</span></span>
<span data-ttu-id="dd456-402">Свойство доступа может относиться не только к таблице в целом, но и к отдельным операциям.</span><span class="sxs-lookup"><span data-stu-id="dd456-402">In addition to appearing on the table, the access property can be used to control individual operations.</span></span>  <span data-ttu-id="dd456-403">Существует четыре операции:</span><span class="sxs-lookup"><span data-stu-id="dd456-403">There are four operations:</span></span>

* <span data-ttu-id="dd456-404">*read* — REST-запрос GET для таблицы;</span><span class="sxs-lookup"><span data-stu-id="dd456-404">*read* is the RESTful GET operation on the table</span></span>
* <span data-ttu-id="dd456-405">*insert* — REST-запрос POST для таблицы;</span><span class="sxs-lookup"><span data-stu-id="dd456-405">*insert* is the RESTful POST operation on the table</span></span>
* <span data-ttu-id="dd456-406">*update* — REST-запрос PATCH для таблицы;</span><span class="sxs-lookup"><span data-stu-id="dd456-406">*update* is the RESTful PATCH operation on the table</span></span>
* <span data-ttu-id="dd456-407">*delete* — REST-запрос DELETE для таблицы.</span><span class="sxs-lookup"><span data-stu-id="dd456-407">*delete* is the RESTful DELETE operation on the table</span></span>

<span data-ttu-id="dd456-408">Например, вы хотите создать таблицу с доступом только для чтения без аутентификации.</span><span class="sxs-lookup"><span data-stu-id="dd456-408">For example, you may wish to provide a read-only unauthenticated table:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <span data-ttu-id="dd456-409"><a name="howto-tables-query"></a>Практическое руководство. Изменение запроса, используемого в операциях с таблицей</span><span class="sxs-lookup"><span data-stu-id="dd456-409"><a name="howto-tables-query"></a>How to: Adjust the query that is used with table operations</span></span>
<span data-ttu-id="dd456-410">Частой задачей в операциях с таблицей является ограничение доступа к определенным данным.</span><span class="sxs-lookup"><span data-stu-id="dd456-410">A common requirement for table operations is to provide a restricted view of the data.</span></span>  <span data-ttu-id="dd456-411">Например, вам может потребоваться предоставить таблицу с указанием идентификатора аутентифицированного пользователя, чтобы вы могли считывать или обновлять только свои записи.</span><span class="sxs-lookup"><span data-stu-id="dd456-411">For example, you may provide a table that is tagged with the authenticated user ID such that you can only read or update your own records.</span></span>  <span data-ttu-id="dd456-412">Эту возможность обеспечивает следующее определение таблицы.</span><span class="sxs-lookup"><span data-stu-id="dd456-412">The following table definition provides this functionality:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for the table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for the authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite the userId with the authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

<span data-ttu-id="dd456-413">Операции, которые подразумевают выполнение запроса, содержат свойство query, в которое можно добавить предложение where.</span><span class="sxs-lookup"><span data-stu-id="dd456-413">Operations that normally execute a query have a query property that you can adjust with a where clause.</span></span> <span data-ttu-id="dd456-414">Свойство query представляет собой объект [QueryJS] , используемый для преобразования запроса OData в то, что может быть обработано серверной частью.</span><span class="sxs-lookup"><span data-stu-id="dd456-414">The query property is a [QueryJS] object that is used to convert an OData query to something that the data backend can process.</span></span>  <span data-ttu-id="dd456-415">В простых операциях сравнения (как в примере выше) можно использовать карту.</span><span class="sxs-lookup"><span data-stu-id="dd456-415">For simple equality cases (like the preceding one), a map can be used.</span></span> <span data-ttu-id="dd456-416">Можно также добавить определенные предложения SQL.</span><span class="sxs-lookup"><span data-stu-id="dd456-416">You can also add specific SQL clauses:</span></span>

    context.query.where('myfield eq ?', 'value');

### <span data-ttu-id="dd456-417"><a name="howto-tables-softdelete"></a>Практическое руководство. Настройка обратимого удаления для таблицы</span><span class="sxs-lookup"><span data-stu-id="dd456-417"><a name="howto-tables-softdelete"></a>How to: Configure soft delete on a table</span></span>
<span data-ttu-id="dd456-418">При обратимом удалении записи фактически не удаляются.</span><span class="sxs-lookup"><span data-stu-id="dd456-418">Soft Delete does not actually delete records.</span></span>  <span data-ttu-id="dd456-419">Вместо этого они помечаются как удаленные установкой значения true в столбце deleted.</span><span class="sxs-lookup"><span data-stu-id="dd456-419">Instead it marks them as deleted within the database by setting the deleted column to true.</span></span>  <span data-ttu-id="dd456-420">Пакет SDK для мобильных приложений Azure автоматически удаляет записи, помеченные как удаленные, из результатов запроса, если только в методе не используется конструкция IncludeDeleted().</span><span class="sxs-lookup"><span data-stu-id="dd456-420">The Azure Mobile Apps SDK automatically removes soft-deleted records from results unless the Mobile Client SDK uses IncludeDeleted().</span></span>  <span data-ttu-id="dd456-421">Чтобы настроить обратимое удаление из таблицы, настройте свойство `softDelete` в файле определения таблицы.</span><span class="sxs-lookup"><span data-stu-id="dd456-421">To configure a table for soft delete, set the `softDelete` property in the table definition file:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="dd456-422">Следует создать механизм удаления записей посредством клиентского приложения, веб-заданий, функции Azure или настраиваемого API.</span><span class="sxs-lookup"><span data-stu-id="dd456-422">You should establish a mechanism for purging records - either from a client application, via a WebJob, Azure Function or through a custom API.</span></span>

### <span data-ttu-id="dd456-423"><a name="howto-tables-seeding"></a>Практическое руководство. Заполнение базы данных данными</span><span class="sxs-lookup"><span data-stu-id="dd456-423"><a name="howto-tables-seeding"></a>How to: Seed your database with data</span></span>
<span data-ttu-id="dd456-424">При создании нового приложения вам может потребоваться заполнить таблицу данными.</span><span class="sxs-lookup"><span data-stu-id="dd456-424">When creating a new application, you may wish to seed a table with data.</span></span>  <span data-ttu-id="dd456-425">Это можно сделать в файле JavaScript определения таблицы:</span><span class="sxs-lookup"><span data-stu-id="dd456-425">This can be done within the table definition JavaScript file as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
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

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="dd456-426">Присвоение начальных значений данных выполняется только при создании таблицы с помощью пакета SDK для мобильных приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="dd456-426">Seeding of data is only done when the table is created by the Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="dd456-427">Если таблица уже существует в базе данных, данные не добавляются.</span><span class="sxs-lookup"><span data-stu-id="dd456-427">If the table already exists within the database, no data is injected into the table.</span></span>  <span data-ttu-id="dd456-428">Если включено использование динамической схемы, то схема будет определена на основании добавляемых данных.</span><span class="sxs-lookup"><span data-stu-id="dd456-428">If dynamic schema is turned on, then the schema is inferred from the seeded data.</span></span>

<span data-ttu-id="dd456-429">Чтобы создать таблицу при запуске службы, рекомендуется явно вызывать метод `tables.initialize()`.</span><span class="sxs-lookup"><span data-stu-id="dd456-429">We recommend that you explicitly call the `tables.initialize()` method to create the table when the service starts running.</span></span>

### <span data-ttu-id="dd456-430"><a name="Swagger"></a>Практическое руководство. Включение поддержки Swagger</span><span class="sxs-lookup"><span data-stu-id="dd456-430"><a name="Swagger"></a>How to: Enable Swagger support</span></span>
<span data-ttu-id="dd456-431">Мобильные приложения службы приложений Azure предоставляются со встроенной поддержкой [Swagger] .</span><span class="sxs-lookup"><span data-stu-id="dd456-431">Azure App Service Mobile Apps comes with built-in [Swagger] support.</span></span>  <span data-ttu-id="dd456-432">Чтобы включить поддержку Swagger, сначала необходимо установить пользовательский интерфейс Swagger в качестве зависимости:</span><span class="sxs-lookup"><span data-stu-id="dd456-432">To enable Swagger support, first install the swagger-ui as a dependency:</span></span>

    npm install --save swagger-ui

<span data-ttu-id="dd456-433">После установки можно включить поддержку Swagger в конструкторе мобильных приложений Azure:</span><span class="sxs-lookup"><span data-stu-id="dd456-433">Once installed, you can enable Swagger support in the Azure Mobile Apps constructor:</span></span>

    var mobile = azureMobileApps({ swagger: true });

<span data-ttu-id="dd456-434">Возможно, вам потребуется включить поддержку Swagger только в разрабатываемых выпусках.</span><span class="sxs-lookup"><span data-stu-id="dd456-434">You probably only want to enable Swagger support in development editions.</span></span>  <span data-ttu-id="dd456-435">Это можно сделать с помощью параметра `NODE_ENV` приложения.</span><span class="sxs-lookup"><span data-stu-id="dd456-435">You can do this by utilizing the `NODE_ENV` app setting:</span></span>

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

<span data-ttu-id="dd456-436">Конечная точка Swagger находится по адресу http://*ваш_сайт*.azurewebsites.net/swagger.</span><span class="sxs-lookup"><span data-stu-id="dd456-436">The swagger endpoint is located at http://*yoursite*.azurewebsites.net/swagger.</span></span>  <span data-ttu-id="dd456-437">Доступ к пользовательскому интерфейсу Swagger можно получить с помощью конечной точки `/swagger/ui` .</span><span class="sxs-lookup"><span data-stu-id="dd456-437">You can access the Swagger UI via the `/swagger/ui` endpoint.</span></span>  <span data-ttu-id="dd456-438">Swagger вернет ошибку для конечной точки, если настроить обязательную аутентификацию для всего приложения.</span><span class="sxs-lookup"><span data-stu-id="dd456-438">if you choose to require authentication across your entire application, Swagger produces an error.</span></span>  <span data-ttu-id="dd456-439">Чтобы достичь наилучших результатов, разрешите получать запросы без аутентификации в параметрах аутентификации и авторизации в службе приложений Azure, а затем управляйте аутентификацией через свойство `table.access` .</span><span class="sxs-lookup"><span data-stu-id="dd456-439">For best results, choose to allow unauthenticated requests through in the Azure App Service Authentication / Authorization settings, then control authentication using the `table.access` property.</span></span>

<span data-ttu-id="dd456-440">Кроме того, вы можете добавить параметр Swagger в файл `azureMobile.js` , если поддержка Swagger требуется только при локальной разработке.</span><span class="sxs-lookup"><span data-stu-id="dd456-440">You can also add the Swagger option to your `azureMobile.js` file if you only want Swagger support when developing locally.</span></span>

## <a name="a-namepushpush-notifications"></a><span data-ttu-id="dd456-441"><a name="push">Push-уведомления</span><span class="sxs-lookup"><span data-stu-id="dd456-441"><a name="push">Push notifications</span></span>
<span data-ttu-id="dd456-442">Мобильные приложения интегрируются с концентраторами уведомлений Azure, чтобы вы могли отправлять целевые push-уведомления на миллионы устройств в рамках всех основных платформ.</span><span class="sxs-lookup"><span data-stu-id="dd456-442">Mobile Apps integrates with Azure Notification Hubs to enable you to send targeted push notifications to millions of devices across all major platforms.</span></span> <span data-ttu-id="dd456-443">С помощью концентраторов уведомлений можно отправлять push-уведомления на устройства iOS, Android и Windows.</span><span class="sxs-lookup"><span data-stu-id="dd456-443">By using Notification Hubs, you can send push notifications to iOS, Android and Windows devices.</span></span> <span data-ttu-id="dd456-444">Дополнительные сведения обо всем, что можно сделать с помощью концентраторов уведомлений, см. в [обзоре концентраторов уведомлений](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dd456-444">To learn more about all that you can do with Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

### <span data-ttu-id="dd456-445"></a><a name="send-push"></a>Практическое руководство. Отправка push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="dd456-445"></a><a name="send-push"></a>How to: Send push notifications</span></span>
<span data-ttu-id="dd456-446">В коде ниже показано, как использовать push-объект для отправки широковещательных push-уведомлений на зарегистрированные устройства iOS.</span><span class="sxs-lookup"><span data-stu-id="dd456-446">The following code shows how to use the push object to send a broadcast push notification to registered iOS devices:</span></span>

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do the push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }

<span data-ttu-id="dd456-447">Создав шаблонную регистрацию push-уведомлений с клиента, можно отправлять шаблонные push-сообщения на устройства на всех поддерживаемых платформах.</span><span class="sxs-lookup"><span data-stu-id="dd456-447">By creating a template push registration from the client, you can instead send a template push message to devices on all supported platforms.</span></span> <span data-ttu-id="dd456-448">В коде ниже показано, как отправить шаблонное уведомление.</span><span class="sxs-lookup"><span data-stu-id="dd456-448">The following code shows how to send a template notification:</span></span>

    // Define the template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do the push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }


### <span data-ttu-id="dd456-449"><a name="push-user"></a>Практическое руководство. Отправка push-уведомлений аутентифицированному пользователю с помощью тегов</span><span class="sxs-lookup"><span data-stu-id="dd456-449"><a name="push-user"></a>How to: Send push notifications to an authenticated user using tags</span></span>
<span data-ttu-id="dd456-450">Когда прошедший проверку пользователь регистрируется для работы с push-уведомлениями, в регистрацию автоматически добавляется тег с идентификатором пользователя.</span><span class="sxs-lookup"><span data-stu-id="dd456-450">When an authenticated user registers for push notifications, a user ID tag is automatically added to the registration.</span></span> <span data-ttu-id="dd456-451">С помощью этого тега можно отправлять push-уведомления на все устройства, зарегистрированные конкретным пользователем.</span><span class="sxs-lookup"><span data-stu-id="dd456-451">By using this tag, you can send push notifications to all devices registered by a specific user.</span></span> <span data-ttu-id="dd456-452">Следующий код получает идентификатор SID пользователя, выполняющего запрос, и отправляет шаблонное push-уведомление в каждую регистрацию устройства для этого пользователя:</span><span class="sxs-lookup"><span data-stu-id="dd456-452">The following code gets the SID of user making the request and sends a template push notification to every device registration for that user:</span></span>

    // Only do the push if configured
    if (context.push) {
        // Send a notification to the current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }

<span data-ttu-id="dd456-453">При регистрации для работы с push-уведомлениями на клиенте, прошедшем проверку подлинности, убедитесь, что проверка подлинности завершена, и только после этого начинайте регистрацию.</span><span class="sxs-lookup"><span data-stu-id="dd456-453">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span>

## <span data-ttu-id="dd456-454"><a name="CustomAPI"></a>Настраиваемые API</span><span class="sxs-lookup"><span data-stu-id="dd456-454"><a name="CustomAPI"></a> Custom APIs</span></span>
### <span data-ttu-id="dd456-455"><a name="howto-customapi-basic"></a>Практическое руководство. Определение настраиваемого интерфейса API</span><span class="sxs-lookup"><span data-stu-id="dd456-455"><a name="howto-customapi-basic"></a>How to: Define a custom API</span></span>
<span data-ttu-id="dd456-456">Помимо API доступа к данным через конечную точку, мобильные приложения Azure могут предоставлять настраиваемые службы API.</span><span class="sxs-lookup"><span data-stu-id="dd456-456">In addition to the data access API via the /tables endpoint, Azure Mobile Apps can provide custom API coverage.</span></span>  <span data-ttu-id="dd456-457">Настраиваемые службы API определяются так же, как и таблицы, и могут использовать тот же набор возможностей, включая проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="dd456-457">Custom APIs are defined in a similar way to the table definitions and can access all the same facilities, including authentication.</span></span>

<span data-ttu-id="dd456-458">Если вы хотите использовать аутентификацию службы приложений для настраиваемого API, сначала нужно настроить аутентификацию службы приложений на [портале Azure] .</span><span class="sxs-lookup"><span data-stu-id="dd456-458">If you wish to use App Service Authentication with a Custom API, you must configure App Service Authentication in the [Azure portal] first.</span></span>  <span data-ttu-id="dd456-459">Дополнительные сведения о настройке проверки подлинности в службе приложений Azure приведены в руководстве по настройке соответствующего поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="dd456-459">For more details about configuring authentication in an Azure App Service, review the Configuration Guide for the identity provider you intend to use:</span></span>

* <span data-ttu-id="dd456-460">[Настройка проверки подлинности в Azure Active Directory.]</span><span class="sxs-lookup"><span data-stu-id="dd456-460">[How to configure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="dd456-461">[Настройка проверки подлинности в Facebook.]</span><span class="sxs-lookup"><span data-stu-id="dd456-461">[How to configure Facebook Authentication]</span></span>
* <span data-ttu-id="dd456-462">[Настройка проверки подлинности в Google.]</span><span class="sxs-lookup"><span data-stu-id="dd456-462">[How to configure Google Authentication]</span></span>
* <span data-ttu-id="dd456-463">[Настройка проверки подлинности в Microsoft.]</span><span class="sxs-lookup"><span data-stu-id="dd456-463">[How to configure Microsoft Authentication]</span></span>
* <span data-ttu-id="dd456-464">[Настройка проверки подлинности в Twitter.]</span><span class="sxs-lookup"><span data-stu-id="dd456-464">[How to configure Twitter Authentication]</span></span>

<span data-ttu-id="dd456-465">Определение настраиваемых API схоже с определением API таблиц.</span><span class="sxs-lookup"><span data-stu-id="dd456-465">Custom APIs are defined in much the same way as the Tables API.</span></span>

1. <span data-ttu-id="dd456-466">Создайте каталог **api** .</span><span class="sxs-lookup"><span data-stu-id="dd456-466">Create an **api** directory</span></span>
2. <span data-ttu-id="dd456-467">В каталоге **api** создайте файл JavaScript с определением API.</span><span class="sxs-lookup"><span data-stu-id="dd456-467">Create an API definition JavaScript file in the **api** directory.</span></span>
3. <span data-ttu-id="dd456-468">Вызовите метод import, чтобы импортировать каталог **api** .</span><span class="sxs-lookup"><span data-stu-id="dd456-468">Use the import method to import the **api** directory.</span></span>

<span data-ttu-id="dd456-469">Вот прототип определения API для использованного выше примера basic-app.</span><span class="sxs-lookup"><span data-stu-id="dd456-469">Here is the prototype api definition based on the basic-app sample we used earlier.</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import the Custom API
    mobile.api.import('./api');

    // Add the mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="dd456-470">Рассмотрим пример API, который возвращает дату сервера с помощью метода *Date.now()* .</span><span class="sxs-lookup"><span data-stu-id="dd456-470">Let's take an example API that returns the server date using the *Date.now()* method.</span></span>  <span data-ttu-id="dd456-471">Ниже приведено содержимое файла api/date.js:</span><span class="sxs-lookup"><span data-stu-id="dd456-471">Here is the api/date.js file:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

<span data-ttu-id="dd456-472">Каждый параметр соответствует стандартной команде RESTful: GET, POST, PATCH или DELETE.</span><span class="sxs-lookup"><span data-stu-id="dd456-472">Each parameter is one of the standard RESTful verbs - GET, POST, PATCH, or DELETE.</span></span>  <span data-ttu-id="dd456-473">Этот метод является стандартной функцией [промежуточного слоя ExpressJS] , которая отправляет требуемые выходные данные.</span><span class="sxs-lookup"><span data-stu-id="dd456-473">The method is a standard [ExpressJS Middleware] function that sends the required output.</span></span>

### <span data-ttu-id="dd456-474"><a name="howto-customapi-auth"></a>Практическое руководство. Обязательная проверка подлинности для доступа к настраиваемому API</span><span class="sxs-lookup"><span data-stu-id="dd456-474"><a name="howto-customapi-auth"></a>How to: Require authentication for access to a custom API</span></span>
<span data-ttu-id="dd456-475">Пакет SDK для мобильных приложений Azure реализует проверку подлинности точно так же, как конечные точки доступа к таблицам и настраиваемые службы API.</span><span class="sxs-lookup"><span data-stu-id="dd456-475">Azure Mobile Apps SDK implements authentication in the same way for both the tables endpoint and custom APIs.</span></span>  <span data-ttu-id="dd456-476">Чтобы добавить проверку подлинности к API-интерфейсу, который мы создали в предыдущем разделе, добавьте свойство **access** :</span><span class="sxs-lookup"><span data-stu-id="dd456-476">To add authentication to the API developed in the previous section, add an **access** property:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="dd456-477">Также можно определить проверку подлинности для конкретных операций:</span><span class="sxs-lookup"><span data-stu-id="dd456-477">You can also specify authentication on specific operations:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // The GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="dd456-478">Для настраиваемых служб API, требующих проверки подлинности, необходимо использовать тот же маркер, что и для конечных точек доступа к таблицам.</span><span class="sxs-lookup"><span data-stu-id="dd456-478">The same token that is used for the tables endpoint must be used for custom APIs requiring authentication.</span></span>

### <span data-ttu-id="dd456-479"><a name="howto-customapi-auth"></a>Практическое руководство. Обработка передачи больших файлов</span><span class="sxs-lookup"><span data-stu-id="dd456-479"><a name="howto-customapi-auth"></a>How to: Handle large file uploads</span></span>
<span data-ttu-id="dd456-480">Пакет SDK для мобильных приложений Azure использует [ПО промежуточного слоя средства синтаксического анализа текста](https://github.com/expressjs/body-parser) для приема и расшифровки содержимого текста в отправляемых данных.</span><span class="sxs-lookup"><span data-stu-id="dd456-480">Azure Mobile Apps SDK uses the [body-parser middleware](https://github.com/expressjs/body-parser) to accept and decode body content in your submission.</span></span>  <span data-ttu-id="dd456-481">Анализатор текста запроса можно предварительно настроить для приема отправки больших файлов:</span><span class="sxs-lookup"><span data-stu-id="dd456-481">You can pre-configure body-parser to accept larger file uploads:</span></span>

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import the Custom API
    mobile.api.import('./api');

    // Add the mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="dd456-482">Перед передачей файл кодируется в Base-64.</span><span class="sxs-lookup"><span data-stu-id="dd456-482">The file is base-64 encoded before transmission.</span></span>  <span data-ttu-id="dd456-483">Это увеличивает размер передаваемых данных, что нужно учесть.</span><span class="sxs-lookup"><span data-stu-id="dd456-483">This increases the size of the actual upload (and hence the size you must account for).</span></span>

### <span data-ttu-id="dd456-484"><a name="howto-customapi-sql"></a>Практическое руководство. Выполнение пользовательских инструкций SQL</span><span class="sxs-lookup"><span data-stu-id="dd456-484"><a name="howto-customapi-sql"></a>How to: Execute custom SQL statements</span></span>
<span data-ttu-id="dd456-485">Пакет SDK для мобильных приложений Azure предоставляет доступ ко всему контексту через объект запроса, позволяя легко выполнять параметризованные инструкции SQL для определенного поставщика данных:</span><span class="sxs-lookup"><span data-stu-id="dd456-485">The Azure Mobile Apps SDK allows access to the entire Context through the request object, allowing you to execute parameterized SQL statements to the defined data provider easily:</span></span>

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on to a later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define the query - anything that can be handled by the mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute the query.  The context for Azure Mobile Apps is available through
            // request.azureMobile - the data object contains the configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <span data-ttu-id="dd456-486"><a name="Debugging"></a>Отладка, простые таблицы и простые интерфейсы API</span><span class="sxs-lookup"><span data-stu-id="dd456-486"><a name="Debugging"></a>Debugging, Easy Tables, and Easy APIs</span></span>
### <span data-ttu-id="dd456-487"><a name="howto-diagnostic-logs"></a>Практическое руководство. Отладка, диагностика и устранение неполадок мобильных приложений Azure</span><span class="sxs-lookup"><span data-stu-id="dd456-487"><a name="howto-diagnostic-logs"></a>How to: Debug, diagnose, and troubleshoot Azure Mobile apps</span></span>
<span data-ttu-id="dd456-488">Служба приложений Azure предоставляет несколько методов отладки и устранения неполадок в приложениях на Node.js.</span><span class="sxs-lookup"><span data-stu-id="dd456-488">The Azure App Service provides several debugging and troubleshooting techniques for Node.js applications.</span></span>
<span data-ttu-id="dd456-489">Ознакомьтесь со следующими статьями, чтобы приступить к устранению неполадок серверной части мобильной службы Node.js:</span><span class="sxs-lookup"><span data-stu-id="dd456-489">Refer to the following articles to get started in troubleshooting your Node.js Mobile backend:</span></span>

* <span data-ttu-id="dd456-490">[Мониторинг службы приложений Azure]</span><span class="sxs-lookup"><span data-stu-id="dd456-490">[Monitoring an Azure App Service]</span></span>
* <span data-ttu-id="dd456-491">[Включение ведения журналов диагностики в службе приложений Azure]</span><span class="sxs-lookup"><span data-stu-id="dd456-491">[Enable Diagnostic Logging in Azure App Service]</span></span>
* <span data-ttu-id="dd456-492">[Диагностика службы приложений Azure в Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="dd456-492">[Troubleshoot an Azure App Service in Visual Studio]</span></span>

<span data-ttu-id="dd456-493">Приложениям на Node.js предоставляется доступ к различным средствам работы с журналами диагностики.</span><span class="sxs-lookup"><span data-stu-id="dd456-493">Node.js applications have access to a wide range of diagnostic log tools.</span></span>  <span data-ttu-id="dd456-494">Для ведения журнала диагностики пакет SDK для мобильных приложений Azure на Node.js использует [Winston] .</span><span class="sxs-lookup"><span data-stu-id="dd456-494">Internally, the Azure Mobile Apps Node.js SDK uses [Winston] for diagnostic logging.</span></span>  <span data-ttu-id="dd456-495">Ведение журналов включается автоматически при включении режима отладки или при установке значения true для параметра **MS_DebugMode** на [портале Azure].</span><span class="sxs-lookup"><span data-stu-id="dd456-495">Logging is automatically enabled by enabling debug mode or by setting the **MS_DebugMode** app setting to true in the [Azure portal].</span></span> <span data-ttu-id="dd456-496">Созданные журналы появляются на странице "Журналы диагностики" [портале Azure].</span><span class="sxs-lookup"><span data-stu-id="dd456-496">Generated logs appear in the Diagnostic Logs on the [Azure portal].</span></span>

### <span data-ttu-id="dd456-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>Практическое руководство. Работа с простыми таблицами на портале Azure</span><span class="sxs-lookup"><span data-stu-id="dd456-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>How to: Work with Easy Tables in the Azure portal</span></span>
<span data-ttu-id="dd456-498">Инструмент "Easy Tables" позволяет легко создавать и изменять таблицы непосредственно на портале.</span><span class="sxs-lookup"><span data-stu-id="dd456-498">Easy Tables in the portal let you create and work with tables right in the portal.</span></span> <span data-ttu-id="dd456-499">Вы даже можете редактировать операции с таблицами в редакторе службы приложений.</span><span class="sxs-lookup"><span data-stu-id="dd456-499">You can even edit table operations using the App Service Editor.</span></span>

<span data-ttu-id="dd456-500">Щелкнув **Простые таблицы** в параметрах сайта серверной части, вы сможете добавить, изменить или удалить таблицу.</span><span class="sxs-lookup"><span data-stu-id="dd456-500">When you click **Easy tables** in your backend site settings, you can add, modify, or delete a table.</span></span> <span data-ttu-id="dd456-501">Также можно просмотреть данные, которые хранятся в таблице.</span><span class="sxs-lookup"><span data-stu-id="dd456-501">You can also see data in the table.</span></span>

![Работа с Easy Tables](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

<span data-ttu-id="dd456-503">На панели команд для таблицы есть следующие команды.</span><span class="sxs-lookup"><span data-stu-id="dd456-503">The following commands are available on the command bar for a table:</span></span>

* <span data-ttu-id="dd456-504">**Изменить разрешения** — позволяет изменить права на операции чтения, вставки, обновления и удаления для таблицы.</span><span class="sxs-lookup"><span data-stu-id="dd456-504">**Change permissions** - modify the permission for read, insert, update and delete operations on the table.</span></span>
  <span data-ttu-id="dd456-505">Возможные варианты: разрешен анонимный доступ, требуется проверка подлинности, любой доступ к операции запрещен.</span><span class="sxs-lookup"><span data-stu-id="dd456-505">Options are to allow anonymous access, to require authentication, or to disable all access to the operation.</span></span>
* <span data-ttu-id="dd456-506">**Изменить сценарий** — позволяет открыть файл сценария для таблицы в редакторе службы приложений.</span><span class="sxs-lookup"><span data-stu-id="dd456-506">**Edit script** - the script file for the table is opened in the App Service Editor.</span></span>
* <span data-ttu-id="dd456-507">**Управление схемой** — позволяет удалять или добавлять столбцы, а также изменять индекс таблицы.</span><span class="sxs-lookup"><span data-stu-id="dd456-507">**Manage schema** - add or delete columns or change the table index.</span></span>
* <span data-ttu-id="dd456-508">**Очистить таблицу** — удаляет из существующей таблицы все строки данных, сохраняя неизменной ее схему.</span><span class="sxs-lookup"><span data-stu-id="dd456-508">**Clear table** - truncates an existing table be deleting all data rows but leaving the schema unchanged.</span></span>
* <span data-ttu-id="dd456-509">**Удалить строки** — удаляет отдельные строки данных.</span><span class="sxs-lookup"><span data-stu-id="dd456-509">**Delete rows** - delete individual rows of data.</span></span>
* <span data-ttu-id="dd456-510">**Просмотреть журналы потоковой передачи** — позволяет подключиться к службе потоковой передачи журналов для вашего сайта.</span><span class="sxs-lookup"><span data-stu-id="dd456-510">**View streaming logs** - connects you to the streaming log service for your site.</span></span>

### <span data-ttu-id="dd456-511"><a name="work-easy-apis"></a>Практическое руководство. Работа с инструментом "Easy APIs" на портале Azure</span><span class="sxs-lookup"><span data-stu-id="dd456-511"><a name="work-easy-apis"></a>How to: Work with Easy APIs in the Azure portal</span></span>
<span data-ttu-id="dd456-512">Инструмент "Easy APIs" позволяет легко создавать и изменять настраиваемые API-интерфейсы непосредственно на портале.</span><span class="sxs-lookup"><span data-stu-id="dd456-512">Easy APIs in the portal let you create and work with custom APIs right in the portal.</span></span> <span data-ttu-id="dd456-513">Вы даже можете редактировать сценарии API в редакторе службы приложений.</span><span class="sxs-lookup"><span data-stu-id="dd456-513">You can edit API scripts using the App Service Editor.</span></span>

<span data-ttu-id="dd456-514">Щелкнув **Простые API** в параметрах сайта серверной части, вы сможете добавить, изменить или удалить настраиваемую конечную точку API.</span><span class="sxs-lookup"><span data-stu-id="dd456-514">When you click **Easy APIs** in your backend site settings, you can add, modify, or delete a custom API endpoint.</span></span>

![Работа с Easy APIs](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

<span data-ttu-id="dd456-516">На портале можно изменять права доступа для выполнения определенного действия HTTP, редактировать файл сценария API в редакторе службы приложений или просматривать журналы потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="dd456-516">In the portal, you can change the access permissions for a given HTTP action, edit the API script file in the App Service Editor, or view the streaming logs.</span></span>

### <span data-ttu-id="dd456-517"><a name="online-editor"></a>Практическое руководство. Изменение кода в редакторе службы приложений</span><span class="sxs-lookup"><span data-stu-id="dd456-517"><a name="online-editor"></a>How to: Edit code in the App Service Editor</span></span>
<span data-ttu-id="dd456-518">Портал Azure позволяет редактировать файлы сценария серверной части Node.js в редакторе службы приложений без скачивания проекта на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="dd456-518">The Azure portal lets you edit your Node.js backend script files in the App Service Editor without having to download the project to your local computer.</span></span> <span data-ttu-id="dd456-519">Чтобы изменить файлы сценариев в онлайн-редакторе, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dd456-519">To edit script files in the online editor:</span></span>

1. <span data-ttu-id="dd456-520">В колонке серверной части мобильного приложения щелкните **Все параметры**, затем **Простые таблицы** или **Простые API**, выберите таблицу или API и щелкните **Изменить сценарий**.</span><span class="sxs-lookup"><span data-stu-id="dd456-520">In your Mobile App backend blade, click **All settings** > either **Easy tables** or **Easy APIs**, click a table or API, then click **Edit script**.</span></span> <span data-ttu-id="dd456-521">Файл сценария будет открыт в редакторе службы приложений.</span><span class="sxs-lookup"><span data-stu-id="dd456-521">The script file is opened in the App Service Editor.</span></span>

    ![Редактор службы приложений](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. <span data-ttu-id="dd456-523">Внесите необходимые изменения в файл кода с помощью онлайн-редактора.</span><span class="sxs-lookup"><span data-stu-id="dd456-523">Make your changes to the code file in the online editor.</span></span> <span data-ttu-id="dd456-524">Изменения сохраняются автоматически при вводе.</span><span class="sxs-lookup"><span data-stu-id="dd456-524">Changes are saved automatically as you type.</span></span>

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
<span data-ttu-id="dd456-525">[Быстрый запуск клиента Android]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="dd456-525">[Android Client QuickStart]: app-service-mobile-android-get-started.md</span></span>
<span data-ttu-id="dd456-526">[Быстрый запуск клиента Apache Cordova]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="dd456-526">[Apache Cordova Client QuickStart]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="dd456-527">[Быстрый запуск клиента iOS.]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="dd456-527">[iOS Client QuickStart]: app-service-mobile-ios-get-started.md</span></span>
<span data-ttu-id="dd456-528">[Быстрый запуск клиента Xamarin.iOS.]: app-service-mobile-xamarin-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="dd456-528">[Xamarin.iOS Client QuickStart]: app-service-mobile-xamarin-ios-get-started.md</span></span>
<span data-ttu-id="dd456-529">[Быстрый запуск клиента Xamarin.Android.]: app-service-mobile-xamarin-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="dd456-529">[Xamarin.Android Client QuickStart]: app-service-mobile-xamarin-android-get-started.md</span></span>
<span data-ttu-id="dd456-530">[Быстрый запуск клиента Xamarin.Forms.]: app-service-mobile-xamarin-forms-get-started.md</span><span class="sxs-lookup"><span data-stu-id="dd456-530">[Xamarin.Forms Client QuickStart]: app-service-mobile-xamarin-forms-get-started.md</span></span>
<span data-ttu-id="dd456-531">[Быстрый запуск клиента Магазина Windows Phone.]: app-service-mobile-windows-store-dotnet-get-started.md</span><span class="sxs-lookup"><span data-stu-id="dd456-531">[Windows Store Client QuickStart]: app-service-mobile-windows-store-dotnet-get-started.md</span></span>
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
<span data-ttu-id="dd456-532">[автономной синхронизации данных]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="dd456-532">[offline data sync]: app-service-mobile-offline-data-sync.md</span></span>
<span data-ttu-id="dd456-533">[Настройка проверки подлинности в Azure Active Directory.]: app-service-mobile-how-to-configure-active-directory-authentication.md</span><span class="sxs-lookup"><span data-stu-id="dd456-533">[How to configure Azure Active Directory Authentication]: app-service-mobile-how-to-configure-active-directory-authentication.md</span></span>
<span data-ttu-id="dd456-534">[Настройка проверки подлинности в Facebook.]: app-service-mobile-how-to-configure-facebook-authentication.md</span><span class="sxs-lookup"><span data-stu-id="dd456-534">[How to configure Facebook Authentication]: app-service-mobile-how-to-configure-facebook-authentication.md</span></span>
<span data-ttu-id="dd456-535">[Настройка проверки подлинности в Google.]: app-service-mobile-how-to-configure-google-authentication.md</span><span class="sxs-lookup"><span data-stu-id="dd456-535">[How to configure Google Authentication]: app-service-mobile-how-to-configure-google-authentication.md</span></span>
<span data-ttu-id="dd456-536">[Настройка проверки подлинности в Microsoft.]: app-service-mobile-how-to-configure-microsoft-authentication.md</span><span class="sxs-lookup"><span data-stu-id="dd456-536">[How to configure Microsoft Authentication]: app-service-mobile-how-to-configure-microsoft-authentication.md</span></span>
<span data-ttu-id="dd456-537">[Настройка проверки подлинности в Twitter.]: app-service-mobile-how-to-configure-twitter-authentication.md</span><span class="sxs-lookup"><span data-stu-id="dd456-537">[How to configure Twitter Authentication]: app-service-mobile-how-to-configure-twitter-authentication.md</span></span>
<span data-ttu-id="dd456-538">[руководстве по развертыванию службы приложений Azure]: ../app-service-web/web-sites-deploy.md</span><span class="sxs-lookup"><span data-stu-id="dd456-538">[Azure App Service Deployment Guide]: ../app-service-web/web-sites-deploy.md</span></span>
<span data-ttu-id="dd456-539">[Мониторинг службы приложений Azure]: ../app-service-web/web-sites-monitor.md</span><span class="sxs-lookup"><span data-stu-id="dd456-539">[Monitoring an Azure App Service]: ../app-service-web/web-sites-monitor.md</span></span>
<span data-ttu-id="dd456-540">[Включение ведения журналов диагностики в службе приложений Azure]: ../app-service-web/web-sites-enable-diagnostic-log.md</span><span class="sxs-lookup"><span data-stu-id="dd456-540">[Enable Diagnostic Logging in Azure App Service]: ../app-service-web/web-sites-enable-diagnostic-log.md</span></span>
<span data-ttu-id="dd456-541">[Диагностика службы приложений Azure в Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md</span><span class="sxs-lookup"><span data-stu-id="dd456-541">[Troubleshoot an Azure App Service in Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md</span></span>
<span data-ttu-id="dd456-542">[Указание версии Node]: ../nodejs-specify-node-version-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="dd456-542">[specify the Node Version]: ../nodejs-specify-node-version-azure-apps.md</span></span>
<span data-ttu-id="dd456-543">[Использование модулей Node]: ../nodejs-use-node-modules-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="dd456-543">[use Node modules]: ../nodejs-use-node-modules-azure-apps.md</span></span>
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
<span data-ttu-id="dd456-544">[Express]: http://expressjs.com/</span><span class="sxs-lookup"><span data-stu-id="dd456-544">[Express]: http://expressjs.com/</span></span>
<span data-ttu-id="dd456-545">[Swagger]: http://swagger.io/</span><span class="sxs-lookup"><span data-stu-id="dd456-545">[Swagger]: http://swagger.io/</span></span>

<span data-ttu-id="dd456-546">[портале Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="dd456-546">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="dd456-547">[OData]: http://www.odata.org</span><span class="sxs-lookup"><span data-stu-id="dd456-547">[OData]: http://www.odata.org</span></span>
<span data-ttu-id="dd456-548">[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise</span><span class="sxs-lookup"><span data-stu-id="dd456-548">[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise</span></span>
<span data-ttu-id="dd456-549">[примере basicapp на сайте GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app</span><span class="sxs-lookup"><span data-stu-id="dd456-549">[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app</span></span>
<span data-ttu-id="dd456-550">[примере todo на GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo</span><span class="sxs-lookup"><span data-stu-id="dd456-550">[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo</span></span>
<span data-ttu-id="dd456-551">[каталоге примеров на сайте GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples</span><span class="sxs-lookup"><span data-stu-id="dd456-551">[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples</span></span>
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
<span data-ttu-id="dd456-552">[QueryJS]: https://github.com/Azure/queryjs</span><span class="sxs-lookup"><span data-stu-id="dd456-552">[QueryJS]: https://github.com/Azure/queryjs</span></span>
<span data-ttu-id="dd456-553">[Node.js Tools 1.1 для Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1</span><span class="sxs-lookup"><span data-stu-id="dd456-553">[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1</span></span>
<span data-ttu-id="dd456-554">[mssql Node.js]: https://www.npmjs.com/package/mssql</span><span class="sxs-lookup"><span data-stu-id="dd456-554">[mssql Node.js package]: https://www.npmjs.com/package/mssql</span></span>
<span data-ttu-id="dd456-555">[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx</span><span class="sxs-lookup"><span data-stu-id="dd456-555">[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx</span></span>
<span data-ttu-id="dd456-556">[промежуточного слоя ExpressJS]: http://expressjs.com/guide/using-middleware.html</span><span class="sxs-lookup"><span data-stu-id="dd456-556">[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html</span></span>
<span data-ttu-id="dd456-557">[Winston]: https://github.com/winstonjs/winston</span><span class="sxs-lookup"><span data-stu-id="dd456-557">[Winston]: https://github.com/winstonjs/winston</span></span>
