---
title: "aaaCreate и подключите tooa базы данных MySQL в Azure"
description: "Узнайте, как toouse hello Azure портала toocreate базы данных MySQL, а затем подключите tooit из веб-приложения PHP в Azure."
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
ms.openlocfilehash: 3abc02f8887432625666afd847e9dc0c0a4db2e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-connect-tooa-mysql-database-in-azure"></a><span data-ttu-id="6099c-103">Создать и присоединить tooa базы данных MySQL в Azure</span><span class="sxs-lookup"><span data-stu-id="6099c-103">Create and connect tooa MySQL database in Azure</span></span>
<span data-ttu-id="6099c-104">В этом учебнике показано, как базы данных toocreate MySQL в hello [портал Azure](https://portal.azure.com) (поставщик [ClearDB](http://www.cleardb.com/)) и как tooit tooconnect из PHP веб-приложение, работающее в [службе приложений Azure](app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="6099c-104">This tutorial shows you how toocreate a MySQL database in hello [Azure portal](https://portal.azure.com) (provider is [ClearDB](http://www.cleardb.com/)) and how tooconnect tooit from a PHP web app running in [Azure App Service](app-service/app-service-value-prop-what-is.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6099c-105">Кроме того, вы можете создать базу данных MySQL как часть [шаблона приложения Marketplace](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="6099c-105">You can also create a MySQL database as part of a [Marketplace app template](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span></span>
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a><span data-ttu-id="6099c-106">Создание базы данных MySQL на портале Azure</span><span class="sxs-lookup"><span data-stu-id="6099c-106">Create a MySQL database in Azure portal</span></span>
<span data-ttu-id="6099c-107">toocreate базы данных MySQL в hello портал Azure hello следующие:</span><span class="sxs-lookup"><span data-stu-id="6099c-107">toocreate a MySQL database in hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="6099c-108">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6099c-108">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6099c-109">Hello в левом меню, щелкните **New** > **данные + хранилище** > **базы данных MySQL**.</span><span class="sxs-lookup"><span data-stu-id="6099c-109">From hello left menu, click **New** > **Data + Storage** > **MySQL Database**.</span></span>

    ![Создание базы данных MySQL на портале Azure — начало](./media/store-php-create-mysql-database/create-db-1-start.png)
3. <span data-ttu-id="6099c-111">В новую базу данных MySQL hello [колонке](azure-portal-overview.md), настройте новую базу данных MySQL следующим образом (*колонке*: на странице портала, открывается по горизонтали):</span><span class="sxs-lookup"><span data-stu-id="6099c-111">In hello New MySQL Database [blade](azure-portal-overview.md), configure your new MySQL database as follows (*blade*: a portal page that opens horizontally):</span></span>

   * <span data-ttu-id="6099c-112">**Имя базы данных**: введите уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="6099c-112">**Database Name**: Type a uniquely identifiable name</span></span>
   * <span data-ttu-id="6099c-113">**Подписки**: выберите toouse hello подписки</span><span class="sxs-lookup"><span data-stu-id="6099c-113">**Subscription**: Choose hello subscription toouse</span></span>
   * <span data-ttu-id="6099c-114">**Тип базы данных**: выберите **Shared** недорогих или бесплатную между уровнями или **Dedicated** tooget выделенные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="6099c-114">**Database Type**: Select **Shared** for low-cost or free tiers, or **Dedicated** tooget dedicated resources.</span></span>
   * <span data-ttu-id="6099c-115">**Группа ресурсов**: добавить существующий hello MySQL базы данных tooan [группы ресурсов](azure-resource-manager/resource-group-overview.md) или поместить его в новый.</span><span class="sxs-lookup"><span data-stu-id="6099c-115">**Resource group**: Add hello MySQL database tooan existing [resource group](azure-resource-manager/resource-group-overview.md) or put it in a new one.</span></span> <span data-ttu-id="6099c-116">Ресурсы в одной группе можно легко управлять вместе приветствия.</span><span class="sxs-lookup"><span data-stu-id="6099c-116">Resources in hello same group can be easily managed together.</span></span>
   * <span data-ttu-id="6099c-117">**Расположение**: выберите tooyou закрыть расположение.</span><span class="sxs-lookup"><span data-stu-id="6099c-117">**Location**: Select a location close tooyou.</span></span> <span data-ttu-id="6099c-118">При добавлении tooan существующие группы ресурсов, вы расположение группы ресурсов заблокированные toohello.</span><span class="sxs-lookup"><span data-stu-id="6099c-118">When adding tooan existing resource group, you're locked toohello resource group's location.</span></span>
   * <span data-ttu-id="6099c-119">**Ценовая категория**: щелкните **Ценовая категория**, затем выберите один из вариантов (категория **Меркурий** бесплатная) и щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="6099c-119">**Pricing Tier**: Click **Pricing Tier**, then select a pricing option (**Mercury** tier is free), and then click **Select**.</span></span>
   * <span data-ttu-id="6099c-120">**Условия использования**: щелкните **условия**, просмотрите сведения о покупке hello и нажмите кнопку **приобрести**.</span><span class="sxs-lookup"><span data-stu-id="6099c-120">**Legal Terms**: Click **Legal Terms**, review hello purchase details, and click **Purchase**.</span></span>
   * <span data-ttu-id="6099c-121">**ПИН-код toodashboard**: выберите, чтобы tooaccess непосредственно из панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="6099c-121">**Pin toodashboard**: Select if you want tooaccess it directly from hello dashboard.</span></span> <span data-ttu-id="6099c-122">Это особенно удобно, если вы еще не знакомы с навигацией по порталу.</span><span class="sxs-lookup"><span data-stu-id="6099c-122">This is especially helpful if you aren't familiar with portal navigation yet.</span></span>

     <span data-ttu-id="6099c-123">Следующий снимок экрана приветствия только примером может служить как можно настроить базу данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="6099c-123">hello following screenshot is just an example of how you can configure your MySQL database.</span></span>  
     ![Создание базы данных MySQL на портале Azure — настройка](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. <span data-ttu-id="6099c-125">Настроив все параметры, щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="6099c-125">When you're done configuring, click **Create**.</span></span>

    ![Создание базы данных MySQL на портале Azure — создание](./media/store-php-create-mysql-database/create-db-3-create.png)

    <span data-ttu-id="6099c-127">Отобразится всплывающее уведомление о запуске развертывания.</span><span class="sxs-lookup"><span data-stu-id="6099c-127">You will see a pop-up notification letting you know that deployment has started.</span></span>

    ![Создание базы данных MySQL на портале Azure — выполнение](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    <span data-ttu-id="6099c-129">По завершении развертывания отобразится еще одно всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="6099c-129">You will get another pop-up once deployment has succeeded.</span></span> <span data-ttu-id="6099c-130">в колонке базы данных MySQL будет автоматически открыт Hello портала.</span><span class="sxs-lookup"><span data-stu-id="6099c-130">hello portal will also open your MySQL database blade automatically.</span></span>

<a name="connect"></a>

## <a name="connect-tooyour-mysql-database"></a><span data-ttu-id="6099c-131">Подключение базы данных MySQL tooyour</span><span class="sxs-lookup"><span data-stu-id="6099c-131">Connect tooyour MySQL database</span></span>
<span data-ttu-id="6099c-132">сведения о соединении hello toosee для новой базы данных MySQL, просто щелкните **свойства** в колонке веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6099c-132">toosee hello connection information for your new MySQL database, just click **Properties** in your web app's blade.</span></span>

![Создание базы данных MySQL на портале Azure — колонка базы данных MySQL](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

<span data-ttu-id="6099c-134">Теперь эти сведения о подключении вы можете использовать в любом веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="6099c-134">You can now use that connection information in any web app.</span></span> <span data-ttu-id="6099c-135">Пример, в котором показано, как сведения о соединении hello toouse из простого приложения PHP доступен [здесь](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span><span class="sxs-lookup"><span data-stu-id="6099c-135">A sample that shows how toouse hello connection information from a simple PHP app is available [here](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span></span>

## <a name="connect-a-laravel-web-app-from-hello-php-get-started-tutorial"></a><span data-ttu-id="6099c-136">Подключение Laravel веб-приложения (из hello PHP get запущенную учебник)</span><span class="sxs-lookup"><span data-stu-id="6099c-136">Connect a Laravel web app (from hello PHP get started tutorial)</span></span>
<span data-ttu-id="6099c-137">Предположим, вы просто готовой hello учебника [создание, Настройка и развертывание приложения tooAzure PHP веб](app-service-web/app-service-web-php-get-started.md) и иметь [Laravel](https://www.laravel.com/) веб-приложения, работающие в Azure.</span><span class="sxs-lookup"><span data-stu-id="6099c-137">Suppose you just finished hello tutorial [Create, configure, and deploy a PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md) and have a [Laravel](https://www.laravel.com/) web app running in Azure.</span></span> <span data-ttu-id="6099c-138">Можно легко добавить приложения Laravel tooyour возможности базы данных.</span><span class="sxs-lookup"><span data-stu-id="6099c-138">You can easily add database capabilities tooyour Laravel app.</span></span> <span data-ttu-id="6099c-139">Выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="6099c-139">Just follow hello steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="6099c-140">Hello следующие шаги предполагают, что завершили hello учебника [создание, Настройка и развертывание приложения tooAzure PHP web](app-service-web/app-service-web-php-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6099c-140">hello following steps assume that you have finished hello tutorial [Create, configure, and deploy a PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md).</span></span>
>
>

1. <span data-ttu-id="6099c-141">Настройка приложения hello Laravel в вашей локальной разработки среды toopoint toohello базы данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="6099c-141">Configure hello Laravel app in your local development environment toopoint toohello MySQL database.</span></span> <span data-ttu-id="6099c-142">toodo, откройте `.env` из приложения Laravel корневого каталога и настроить параметры базы данных MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="6099c-142">toodo this, open `.env` from your Laravel app's root directory and configure hello MySQL database options.</span></span>

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > <span data-ttu-id="6099c-143">В hello **свойства** колонке может hello имя базы данных MySQL или могут не hello один в hello **имя базы данных** поля.</span><span class="sxs-lookup"><span data-stu-id="6099c-143">In hello **Properties** blade, hello name of your MySQL database may or may not be hello one shown in hello **DATABASE NAME** field.</span></span> <span data-ttu-id="6099c-144">Это параметр лучше toocheck hello базы данных в hello **строка подключения** поля.</span><span class="sxs-lookup"><span data-stu-id="6099c-144">It's better toocheck hello Database parameter in hello **CONNECTION STRING** field.</span></span>    
   >
   > ![Создание базы данных MySQL на портале Azure — выполнение](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. <span data-ttu-id="6099c-146">Hello быстрым способом tooverify, теперь имеется доступ MySQL — toouse [формирование шаблонов для проверки подлинности по умолчанию в Laravel](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span><span class="sxs-lookup"><span data-stu-id="6099c-146">hello quickest way tooverify that you have MySQL access now is toouse [Laravel's default authentication scaffolding](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span></span>
   <span data-ttu-id="6099c-147">Hello терминалов командной строки выполните следующие команды из корневого каталога приложения Laravel hello:</span><span class="sxs-lookup"><span data-stu-id="6099c-147">In hello command-line terminal, run hello following commands from your Laravel app's root directory:</span></span>

         php artisan migrate
         php artisan make:auth

    <span data-ttu-id="6099c-148">Первая команда Hello создает hello таблицы в зависимости от предопределенных миграции в hello Azure `database/migrations` каталога, а вторая команда hello закрепление hello основных представлений и маршруты для регистрации пользователя и проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="6099c-148">hello first command creates hello tables in Azure based on predefined migrations in hello `database/migrations` directory, and hello second  command scaffolds hello basic views and routes for user registration and authentication.</span></span>
3. <span data-ttu-id="6099c-149">Теперь запустите сервер разработки hello:</span><span class="sxs-lookup"><span data-stu-id="6099c-149">Run hello development server now:</span></span>

        php artisan serve
4. <span data-ttu-id="6099c-150">В браузере hello перейдите toohttp://localhost:8000 и регистрации нового пользователя, как показано:</span><span class="sxs-lookup"><span data-stu-id="6099c-150">In hello browser, navigate toohttp://localhost:8000 and register a new user as shown:</span></span>

    ![Подключение базы данных Azure tooMySQL - Регистрация пользователя](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    <span data-ttu-id="6099c-152">Выполните запрос завершения hello регистрации hello пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="6099c-152">Follow hello UI prompt complete hello registration.</span></span> <span data-ttu-id="6099c-153">После этого вы автоматически войдете.</span><span class="sxs-lookup"><span data-stu-id="6099c-153">Once registration completes, you will be logged in.</span></span>

    ![Подключение базы данных Azure tooMySQL - Регистрация пользователя](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    <span data-ttu-id="6099c-155">Теперь вы разрабатываете приложения для hello базы данных MySQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="6099c-155">You are now developing your app against hello MySQL database in Azure.</span></span>
5. <span data-ttu-id="6099c-156">Теперь необходимо просто tooreplicate вашей `.env` параметры tooyour веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="6099c-156">Now, you just need tooreplicate your `.env` settings tooyour Azure web app.</span></span> <span data-ttu-id="6099c-157">Выполните следующие команды Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="6099c-157">Run hello following Azure CLI commands:</span></span>

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. <span data-ttu-id="6099c-158">Далее, зафиксируйте и отправьте tooAzure hello локальные изменения, внесенные в ранее во время выполнения `php artisan make:auth`.</span><span class="sxs-lookup"><span data-stu-id="6099c-158">Next, commit and push tooAzure hello local changes made earlier while running `php artisan make:auth`.</span></span>

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. <span data-ttu-id="6099c-159">Обзор toohello веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="6099c-159">Browse toohello Azure web app.</span></span>

        azure site browse
8. <span data-ttu-id="6099c-160">Вход с помощью учетных данных пользователя hello, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="6099c-160">Log in using hello user credentials you created earlier.</span></span>

    ![Подключение базы данных tooMySQL в Azure — Обзор tooAzure веб-приложения](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    <span data-ttu-id="6099c-162">После входа, вы увидите понятное после входа в систему экран приветствия.</span><span class="sxs-lookup"><span data-stu-id="6099c-162">After you log in, you should see hello friendly post-login screen.</span></span>

    ![Подключение tooMySQL базы данных в Azure, вход](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    <span data-ttu-id="6099c-164">Теперь веб-приложение PHP в Azure имеет доступ к данным базы данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="6099c-164">Congratulations, your PHP web app in Azure is now accessing data from your MySQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6099c-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6099c-165">Next steps</span></span>
<span data-ttu-id="6099c-166">Дополнительные сведения см. в разделе hello [Центр разработчика PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="6099c-166">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>
