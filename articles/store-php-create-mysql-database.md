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
# <a name="create-and-connect-tooa-mysql-database-in-azure"></a>Создать и присоединить tooa базы данных MySQL в Azure
В этом учебнике показано, как базы данных toocreate MySQL в hello [портал Azure](https://portal.azure.com) (поставщик [ClearDB](http://www.cleardb.com/)) и как tooit tooconnect из PHP веб-приложение, работающее в [службе приложений Azure](app-service/app-service-value-prop-what-is.md).

> [!NOTE]
> Кроме того, вы можете создать базу данных MySQL как часть [шаблона приложения Marketplace](app-service-web/app-service-web-create-web-app-from-marketplace.md).
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a>Создание базы данных MySQL на портале Azure
toocreate базы данных MySQL в hello портал Azure hello следующие:

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Hello в левом меню, щелкните **New** > **данные + хранилище** > **базы данных MySQL**.

    ![Создание базы данных MySQL на портале Azure — начало](./media/store-php-create-mysql-database/create-db-1-start.png)
3. В новую базу данных MySQL hello [колонке](azure-portal-overview.md), настройте новую базу данных MySQL следующим образом (*колонке*: на странице портала, открывается по горизонтали):

   * **Имя базы данных**: введите уникальное имя.
   * **Подписки**: выберите toouse hello подписки
   * **Тип базы данных**: выберите **Shared** недорогих или бесплатную между уровнями или **Dedicated** tooget выделенные ресурсы.
   * **Группа ресурсов**: добавить существующий hello MySQL базы данных tooan [группы ресурсов](azure-resource-manager/resource-group-overview.md) или поместить его в новый. Ресурсы в одной группе можно легко управлять вместе приветствия.
   * **Расположение**: выберите tooyou закрыть расположение. При добавлении tooan существующие группы ресурсов, вы расположение группы ресурсов заблокированные toohello.
   * **Ценовая категория**: щелкните **Ценовая категория**, затем выберите один из вариантов (категория **Меркурий** бесплатная) и щелкните **Выбрать**.
   * **Условия использования**: щелкните **условия**, просмотрите сведения о покупке hello и нажмите кнопку **приобрести**.
   * **ПИН-код toodashboard**: выберите, чтобы tooaccess непосредственно из панели мониторинга hello. Это особенно удобно, если вы еще не знакомы с навигацией по порталу.

     Следующий снимок экрана приветствия только примером может служить как можно настроить базу данных MySQL.  
     ![Создание базы данных MySQL на портале Azure — настройка](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. Настроив все параметры, щелкните **Создать**.

    ![Создание базы данных MySQL на портале Azure — создание](./media/store-php-create-mysql-database/create-db-3-create.png)

    Отобразится всплывающее уведомление о запуске развертывания.

    ![Создание базы данных MySQL на портале Azure — выполнение](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    По завершении развертывания отобразится еще одно всплывающее окно. в колонке базы данных MySQL будет автоматически открыт Hello портала.

<a name="connect"></a>

## <a name="connect-tooyour-mysql-database"></a>Подключение базы данных MySQL tooyour
сведения о соединении hello toosee для новой базы данных MySQL, просто щелкните **свойства** в колонке веб-приложения.

![Создание базы данных MySQL на портале Azure — колонка базы данных MySQL](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

Теперь эти сведения о подключении вы можете использовать в любом веб-приложении. Пример, в котором показано, как сведения о соединении hello toouse из простого приложения PHP доступен [здесь](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).

## <a name="connect-a-laravel-web-app-from-hello-php-get-started-tutorial"></a>Подключение Laravel веб-приложения (из hello PHP get запущенную учебник)
Предположим, вы просто готовой hello учебника [создание, Настройка и развертывание приложения tooAzure PHP веб](app-service-web/app-service-web-php-get-started.md) и иметь [Laravel](https://www.laravel.com/) веб-приложения, работающие в Azure. Можно легко добавить приложения Laravel tooyour возможности базы данных. Выполните следующие действия hello:

> [!NOTE]
> Hello следующие шаги предполагают, что завершили hello учебника [создание, Настройка и развертывание приложения tooAzure PHP web](app-service-web/app-service-web-php-get-started.md).
>
>

1. Настройка приложения hello Laravel в вашей локальной разработки среды toopoint toohello базы данных MySQL. toodo, откройте `.env` из приложения Laravel корневого каталога и настроить параметры базы данных MySQL hello.

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > В hello **свойства** колонке может hello имя базы данных MySQL или могут не hello один в hello **имя базы данных** поля. Это параметр лучше toocheck hello базы данных в hello **строка подключения** поля.    
   >
   > ![Создание базы данных MySQL на портале Azure — выполнение](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. Hello быстрым способом tooverify, теперь имеется доступ MySQL — toouse [формирование шаблонов для проверки подлинности по умолчанию в Laravel](https://laravel.com/docs/5.2/authentication#authentication-quickstart).
   Hello терминалов командной строки выполните следующие команды из корневого каталога приложения Laravel hello:

         php artisan migrate
         php artisan make:auth

    Первая команда Hello создает hello таблицы в зависимости от предопределенных миграции в hello Azure `database/migrations` каталога, а вторая команда hello закрепление hello основных представлений и маршруты для регистрации пользователя и проверки подлинности.
3. Теперь запустите сервер разработки hello:

        php artisan serve
4. В браузере hello перейдите toohttp://localhost:8000 и регистрации нового пользователя, как показано:

    ![Подключение базы данных Azure tooMySQL - Регистрация пользователя](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    Выполните запрос завершения hello регистрации hello пользовательского интерфейса. После этого вы автоматически войдете.

    ![Подключение базы данных Azure tooMySQL - Регистрация пользователя](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    Теперь вы разрабатываете приложения для hello базы данных MySQL в Azure.
5. Теперь необходимо просто tooreplicate вашей `.env` параметры tooyour веб-приложение Azure. Выполните следующие команды Azure CLI hello.

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. Далее, зафиксируйте и отправьте tooAzure hello локальные изменения, внесенные в ранее во время выполнения `php artisan make:auth`.

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. Обзор toohello веб-приложение Azure.

        azure site browse
8. Вход с помощью учетных данных пользователя hello, созданную ранее.

    ![Подключение базы данных tooMySQL в Azure — Обзор tooAzure веб-приложения](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    После входа, вы увидите понятное после входа в систему экран приветствия.

    ![Подключение tooMySQL базы данных в Azure, вход](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    Теперь веб-приложение PHP в Azure имеет доступ к данным базы данных MySQL.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения см. в разделе hello [Центр разработчика PHP](/develop/php/).
