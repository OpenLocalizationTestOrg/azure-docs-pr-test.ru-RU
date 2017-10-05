---
title: "Создание базы данных MySQL и подключение к ней в Azure"
description: "Из этой статьи вы узнаете, как с помощью портала Azure создать базу данных MySQL и подключиться к ней из веб-приложения PHP в Azure."
documentationcenter: php
services: app-service\web
author: cephalin
manager: erikre
editor: 
tags: mysql
ms.assetid: 55465a9a-7e65-4fd9-8a65-dd83ee41f3e5
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;cephalin
ms.openlocfilehash: 66f4b7a5f8eb3f6f125c9420b40caffca3d43dd6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-connect-to-a-mysql-database-in-azure"></a><span data-ttu-id="09eae-103">Создание базы данных MySQL и подключение к ней в Azure</span><span class="sxs-lookup"><span data-stu-id="09eae-103">Create and connect to a MySQL database in Azure</span></span>
<span data-ttu-id="09eae-104">В этом учебнике объясняется, как создать базу данных MySQL на [портале Azure](https://portal.azure.com) (поставщик — [ClearDB](http://www.cleardb.com/)) и подключиться к ней из веб-приложения PHP, запущенного в [службе приложений Azure](app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="09eae-104">This tutorial shows you how to create a MySQL database in the [Azure portal](https://portal.azure.com) (provider is [ClearDB](http://www.cleardb.com/)) and how to connect to it from a PHP web app running in [Azure App Service](app-service/app-service-value-prop-what-is.md).</span></span>

> [!NOTE]
> <span data-ttu-id="09eae-105">Кроме того, вы можете создать базу данных MySQL как часть [шаблона приложения Marketplace](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="09eae-105">You can also create a MySQL database as part of a [Marketplace app template](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span></span>
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a><span data-ttu-id="09eae-106">Создание базы данных MySQL на портале Azure</span><span class="sxs-lookup"><span data-stu-id="09eae-106">Create a MySQL database in Azure portal</span></span>
<span data-ttu-id="09eae-107">Чтобы создать базу данных MySQL на портале Azure:</span><span class="sxs-lookup"><span data-stu-id="09eae-107">To create a MySQL database in the Azure portal, do the following:</span></span>

1. <span data-ttu-id="09eae-108">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="09eae-108">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="09eae-109">В меню слева выберите пункт **Создать** > **Данные + хранилище** > **База данных MySQL**.</span><span class="sxs-lookup"><span data-stu-id="09eae-109">From the left menu, click **New** > **Data + Storage** > **MySQL Database**.</span></span>

    ![Создание базы данных MySQL на портале Azure — начало](./media/store-php-create-mysql-database/create-db-1-start.png)
3. <span data-ttu-id="09eae-111">В [колонке](azure-portal-overview.md)(*колонка*— это страница портала, которая открывается горизонтально) новой базы данных MySQL настройте базу данных.</span><span class="sxs-lookup"><span data-stu-id="09eae-111">In the New MySQL Database [blade](azure-portal-overview.md), configure your new MySQL database as follows (*blade*: a portal page that opens horizontally):</span></span>

   * <span data-ttu-id="09eae-112">**Имя базы данных**: введите уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="09eae-112">**Database Name**: Type a uniquely identifiable name</span></span>
   * <span data-ttu-id="09eae-113">**Подписка**: выберите подписку, которую нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="09eae-113">**Subscription**: Choose the subscription to use</span></span>
   * <span data-ttu-id="09eae-114">**Тип базы данных**: выберите **Общий** для недорогих или бесплатных категорий или **Выделенный** для получения выделенных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="09eae-114">**Database Type**: Select **Shared** for low-cost or free tiers, or **Dedicated** to get dedicated resources.</span></span>
   * <span data-ttu-id="09eae-115">**Группа ресурсов**: добавьте базу данных MySQL в существующую или новую [группу ресурсов](azure-resource-manager/resource-group-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="09eae-115">**Resource group**: Add the MySQL database to an existing [resource group](azure-resource-manager/resource-group-overview.md) or put it in a new one.</span></span> <span data-ttu-id="09eae-116">Ресурсами, которые находятся в одной группе, легко управлять.</span><span class="sxs-lookup"><span data-stu-id="09eae-116">Resources in the same group can be easily managed together.</span></span>
   * <span data-ttu-id="09eae-117">**Расположение**: выберите близкое к вам расположение.</span><span class="sxs-lookup"><span data-stu-id="09eae-117">**Location**: Select a location close to you.</span></span> <span data-ttu-id="09eae-118">При добавлении элементов в существующую группу ресурсов вам автоматически назначается расположение этой группы.</span><span class="sxs-lookup"><span data-stu-id="09eae-118">When adding to an existing resource group, you're locked to the resource group's location.</span></span>
   * <span data-ttu-id="09eae-119">**Ценовая категория**: щелкните **Ценовая категория**, затем выберите один из вариантов (категория **Меркурий** бесплатная) и щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="09eae-119">**Pricing Tier**: Click **Pricing Tier**, then select a pricing option (**Mercury** tier is free), and then click **Select**.</span></span>
   * <span data-ttu-id="09eae-120">**Юридические условия**: щелкните **Юридические условия**, просмотрите сведения о покупке и нажмите кнопку **Приобрести**.</span><span class="sxs-lookup"><span data-stu-id="09eae-120">**Legal Terms**: Click **Legal Terms**, review the purchase details, and click **Purchase**.</span></span>
   * <span data-ttu-id="09eae-121">**Закрепление на панели мониторинга**: укажите, хотите ли вы получить к элементу доступ непосредственно на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="09eae-121">**Pin to dashboard**: Select if you want to access it directly from the dashboard.</span></span> <span data-ttu-id="09eae-122">Это особенно удобно, если вы еще не знакомы с навигацией по порталу.</span><span class="sxs-lookup"><span data-stu-id="09eae-122">This is especially helpful if you aren't familiar with portal navigation yet.</span></span>

     <span data-ttu-id="09eae-123">На следующем снимке экрана представлен пример того, как вы можете настроить базу данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="09eae-123">The following screenshot is just an example of how you can configure your MySQL database.</span></span>  
     ![Создание базы данных MySQL на портале Azure — настройка](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. <span data-ttu-id="09eae-125">Настроив все параметры, щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="09eae-125">When you're done configuring, click **Create**.</span></span>

    ![Создание базы данных MySQL на портале Azure — создание](./media/store-php-create-mysql-database/create-db-3-create.png)

    <span data-ttu-id="09eae-127">Отобразится всплывающее уведомление о запуске развертывания.</span><span class="sxs-lookup"><span data-stu-id="09eae-127">You will see a pop-up notification letting you know that deployment has started.</span></span>

    ![Создание базы данных MySQL на портале Azure — выполнение](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    <span data-ttu-id="09eae-129">По завершении развертывания отобразится еще одно всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="09eae-129">You will get another pop-up once deployment has succeeded.</span></span> <span data-ttu-id="09eae-130">Кроме того, на портале также автоматически откроется колонка базы данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="09eae-130">The portal will also open your MySQL database blade automatically.</span></span>

<a name="connect"></a>

## <a name="connect-to-your-mysql-database"></a><span data-ttu-id="09eae-131">Подключение к базе данных MySQL</span><span class="sxs-lookup"><span data-stu-id="09eae-131">Connect to your MySQL database</span></span>
<span data-ttu-id="09eae-132">Чтобы отобразить сведения о подключении для новой базы данных MySQL, просто щелкните **Свойства** в колонке своего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="09eae-132">To see the connection information for your new MySQL database, just click **Properties** in your web app's blade.</span></span>

![Создание базы данных MySQL на портале Azure — колонка базы данных MySQL](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

<span data-ttu-id="09eae-134">Теперь эти сведения о подключении вы можете использовать в любом веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="09eae-134">You can now use that connection information in any web app.</span></span> <span data-ttu-id="09eae-135">[Здесь](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql)доступен пример того, как использовать сведения о подключении в простом приложении PHP.</span><span class="sxs-lookup"><span data-stu-id="09eae-135">A sample that shows how to use the connection information from a simple PHP app is available [here](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span></span>

## <a name="connect-a-laravel-web-app-from-the-php-get-started-tutorial"></a><span data-ttu-id="09eae-136">Подключение веб-приложения Laravel (из руководства по началу работы с PHP)</span><span class="sxs-lookup"><span data-stu-id="09eae-136">Connect a Laravel web app (from the PHP get started tutorial)</span></span>
<span data-ttu-id="09eae-137">Предположим, что вы уже изучили учебник [Создание, настройка и развертывание веб-приложения PHP в Azure](app-service-web/app-service-web-php-get-started.md), а в Azure запущено веб-приложение [Laravel](https://www.laravel.com/).</span><span class="sxs-lookup"><span data-stu-id="09eae-137">Suppose you just finished the tutorial [Create, configure, and deploy a PHP web app to Azure](app-service-web/app-service-web-php-get-started.md) and have a [Laravel](https://www.laravel.com/) web app running in Azure.</span></span> <span data-ttu-id="09eae-138">Вы легко можете добавить возможности базы данных в это приложение.</span><span class="sxs-lookup"><span data-stu-id="09eae-138">You can easily add database capabilities to your Laravel app.</span></span> <span data-ttu-id="09eae-139">Просто сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="09eae-139">Just follow the steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="09eae-140">Чтобы выполнить приведенные ниже инструкции, следует предварительно изучить учебник [Создание, настройка и развертывание веб-приложения PHP в Azure](app-service-web/app-service-web-php-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="09eae-140">The following steps assume that you have finished the tutorial [Create, configure, and deploy a PHP web app to Azure](app-service-web/app-service-web-php-get-started.md).</span></span>
>
>

1. <span data-ttu-id="09eae-141">Настройте приложение Laravel в локальной среде разработки, чтобы указать на базу данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="09eae-141">Configure the Laravel app in your local development environment to point to the MySQL database.</span></span> <span data-ttu-id="09eae-142">Для этого откройте `.env` в корневом каталоге приложения Laravel и настройте параметры базы данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="09eae-142">To do this, open `.env` from your Laravel app's root directory and configure the MySQL database options.</span></span>

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > <span data-ttu-id="09eae-143">В колонке **Свойства** имя базы данных MySQL может совпадать с именем, отображаемым в поле **Имя базы данных** (а может и не совпадать).</span><span class="sxs-lookup"><span data-stu-id="09eae-143">In the **Properties** blade, the name of your MySQL database may or may not be the one shown in the **DATABASE NAME** field.</span></span> <span data-ttu-id="09eae-144">Лучше проверить параметр "База данных" в поле **Строка подключения** .</span><span class="sxs-lookup"><span data-stu-id="09eae-144">It's better to check the Database parameter in the **CONNECTION STRING** field.</span></span>    
   >
   > ![Создание базы данных MySQL на портале Azure — выполнение](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. <span data-ttu-id="09eae-146">Быстро проверить, есть ли у вас доступ к MySQL, можно с помощью [стандартного формирования шаблонов проверки подлинности Laravel](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span><span class="sxs-lookup"><span data-stu-id="09eae-146">The quickest way to verify that you have MySQL access now is to use [Laravel's default authentication scaffolding](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span></span>
   <span data-ttu-id="09eae-147">В терминале командной строки выполните из корневого каталога приложения Laravel такие команды:</span><span class="sxs-lookup"><span data-stu-id="09eae-147">In the command-line terminal, run the following commands from your Laravel app's root directory:</span></span>

         php artisan migrate
         php artisan make:auth

    <span data-ttu-id="09eae-148">Первая команда создает таблицы в Azure на основании предварительно заданных переносов в каталог `database/migrations`. Вторая команда формирует шаблоны основных представлений и маршрутов для регистрации и проверки подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="09eae-148">The first command creates the tables in Azure based on predefined migrations in the `database/migrations` directory, and the second  command scaffolds the basic views and routes for user registration and authentication.</span></span>
3. <span data-ttu-id="09eae-149">Теперь запустите сервер разработки.</span><span class="sxs-lookup"><span data-stu-id="09eae-149">Run the development server now:</span></span>

        php artisan serve
4. <span data-ttu-id="09eae-150">В браузере перейдите по адресу http://localhost:8000 и зарегистрируйте нового пользователя, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="09eae-150">In the browser, navigate to http://localhost:8000 and register a new user as shown:</span></span>

    ![Подключение к базе данных MySQL на портале Azure — регистрация пользователя](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    <span data-ttu-id="09eae-152">Следуя подсказкам интерфейса, завершите регистрацию.</span><span class="sxs-lookup"><span data-stu-id="09eae-152">Follow the UI prompt complete the registration.</span></span> <span data-ttu-id="09eae-153">После этого вы автоматически войдете.</span><span class="sxs-lookup"><span data-stu-id="09eae-153">Once registration completes, you will be logged in.</span></span>

    ![Подключение к базе данных MySQL на портале Azure — регистрация пользователя](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    <span data-ttu-id="09eae-155">Вы в процессе разработки приложения на основе базы данных MySQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="09eae-155">You are now developing your app against the MySQL database in Azure.</span></span>
5. <span data-ttu-id="09eae-156">Теперь вам осталось реплицировать параметры `.env` в веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="09eae-156">Now, you just need to replicate your `.env` settings to your Azure web app.</span></span> <span data-ttu-id="09eae-157">Запустите такие команды интерфейса командной строки Azure:</span><span class="sxs-lookup"><span data-stu-id="09eae-157">Run the following Azure CLI commands:</span></span>

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. <span data-ttu-id="09eae-158">Затем сохраните и примените в Azure изменения, сделанные раньше во время запуска `php artisan make:auth`.</span><span class="sxs-lookup"><span data-stu-id="09eae-158">Next, commit and push to Azure the local changes made earlier while running `php artisan make:auth`.</span></span>

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. <span data-ttu-id="09eae-159">Найдите веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="09eae-159">Browse to the Azure web app.</span></span>

        azure site browse
8. <span data-ttu-id="09eae-160">Войдите, используя созданные ранее учетные данные пользователя.</span><span class="sxs-lookup"><span data-stu-id="09eae-160">Log in using the user credentials you created earlier.</span></span>

    ![Подключение к базе данных MySQL на портале Azure — поиск веб-приложения Azure](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    <span data-ttu-id="09eae-162">После входа должен отобразиться понятный экран, предназначенный для работы после входа.</span><span class="sxs-lookup"><span data-stu-id="09eae-162">After you log in, you should see the friendly post-login screen.</span></span>

    ![Подключение к базе данных MySQL на портале Azure — выполнен вход](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    <span data-ttu-id="09eae-164">Теперь веб-приложение PHP в Azure имеет доступ к данным базы данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="09eae-164">Congratulations, your PHP web app in Azure is now accessing data from your MySQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09eae-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="09eae-165">Next steps</span></span>
<span data-ttu-id="09eae-166">Дополнительную информацию можно найти в [Центре разработчика PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="09eae-166">For more information, see the [PHP Developer Center](/develop/php/).</span></span>
