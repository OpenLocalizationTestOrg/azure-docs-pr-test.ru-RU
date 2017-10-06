---
title: "веб-приложение Umbraco в hello портал Azure в течение пяти минут aaaDeploy | Документы Microsoft"
description: "Узнайте, как просто можно toorun веб-приложений в службе приложений путем развертывания пример приложения ASP.NET. Кроме того, вы сможете быстро просмотреть результаты."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: cephalin
ms.openlocfilehash: 6da45f99b3043a3684e3d99c14e6443d597b5212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-umbraco-web-app-in-hello-azure-portal-in-five-minutes"></a>Развертывание веб-приложение Umbraco в hello портал Azure в течение пяти минут

Этот учебник поможет вам развернуть n [Umbraco](https://our.umbraco.org/) веб-приложения слишком[службе приложений Azure](../app-service/app-service-value-prop-what-is.md) в минутах.

![Приложение Umbraco](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a>Предварительные требования
Вам потребуется учетная запись Microsoft Azure. Если у вас нет учетной записи, [подпишитесь на бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) или [активируйте преимущества для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/) возможно даже без учетной записи Azure. Создание начального приложения и воспроизведение к ней до часа tooan--без кредитной карты требуется, не обязательства.
> 
> 

## <a name="deploy-hello-aspnet-app"></a>Развертывание приложения ASP.NET hello
1. Войдите в toohello [портал Azure](https://portal.azure.com).

2. Откройте страницу [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).

    Указывает tooimmediately ярлык настроить новое приложение Umbraco в hello портал Azure.

3. В поле **Имя приложения** введите имя веб-приложения. Если вы увидите зеленый флажок в поле hello hello имя является уникальным в hello `azurewebsites.net` домена.
   
5. В **группы ресурсов**, нажмите кнопку **создать новый** toocreate новый [группы ресурсов](../azure-resource-manager/resource-group-overview.md), присвойте ему имя.

7. Щелкните **Расположение или план службы приложений** > **Создать**. Настройка hello [план служб приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) следующим:

    - В **план служб приложений**, требуемое имя типа hello.
    - В **расположение**, выбрать план toohost расположение.
    - Щелкните **Ценовая категория**, а затем выберите **F1 Free** или другую категорию, которая вам подходит. Щелкните **Выбрать**.
    - Нажмите кнопку **ОК**.

    Конфигурация Umbraco CMS теперь должен выглядеть, как следующий снимок экрана приветствия:

    ![Настройка конфигурации: первое приложение Umbraco в службе приложений Azure](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. Щелкните **База данных SQL** > **Создать новую базу данных**. Настройте hello базы данных SQL, как показано.

    - В поле **Имя** введите имя, например **myDB**.
    - Щелкните **Ценовая категория**, а затем выберите **F1 Free** или другую категорию, которая вам подходит. Щелкните **Выбрать**.
    - Щелкните **Целевой сервер** > **Создать сервер**. Настройка сервера базы данных hello, как показано:

        - В поле **Имя сервера** введите имя сервера. Если вы увидите зеленый флажок в поле hello hello имя является уникальным в hello `.database.windows.net` домена.
        - В **имя входа администратора сервера**, имя пользователя администратора требуемого типа hello.
        - В **пароль** и **подтверждение пароля**, введите нужный пароль hello.
        - В расположении выберите hello того же расположения, используемого для веб-приложения hello.
        - Убедитесь, что **tooaccess сервера разрешить службам azure** выбран.
        - Нажмите кнопку **Выбрать**.
    
    - Нажмите кнопку **Выбрать**.

13. Нажмите кнопку **веб-параметров приложения**, укажите имя пользователя базы данных hello и пароль и нажмите кнопку **ОК**.

    Конфигурация Umbraco CMS теперь должен выглядеть, как следующий снимок экрана приветствия:

    ![Настройка конфигурации завершена: первое приложение Umbraco в службе приложений Azure](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. Щелкните **Создать**.
    
    Теперь Azure создаст приложение Umbraco на основе выбранной конфигурации. Должно появиться уведомление с текстом **Развертывание начато**.

    ![Успешное развертывание: первое приложение Umbraco в службе приложений Azure](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a>Запуск веб-приложения Umrbaco и управление им

Когда Azure завершит развертывание приложения, появится еще одно уведомление.

![Успешное развертывание: первое приложение Umbraco в службе приложений Azure](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. Щелкните уведомление hello. Если вы пропустили всегда доступен, щелкнув hello уведомления колокольчика (![ниже уведомления - первый Umbraco в службе приложений Azure](./media/app-service-web-get-started-dotnet-portal/notification.png)).

    Теперь должна отображаться [колонка](../azure-resource-manager/resource-group-portal.md#manage-resources) управления веб-приложением. (*Колонка*: горизонтальная страница портала.)

3. В hello вверху страницы обзора hello щелкните **Обзор**.
   
    ![Обзор: первое приложение Umbraco в службе приложений Azure](./media/app-service-web-get-started-dotnet-portal/browse.png)

    Теперь вы видите hello Umbraco **приветствия** страницы. Настройте установку Umbraco hello и начать воспроизведение с ним!

    ![Конфигурация Umbraco: первое приложение Umbraco в службе приложений Azure](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a>Дальнейшие действия
* [Развертывание ASP.NET tooAzure приложения web службу приложений, с помощью Visual Studio](app-service-web-get-started-dotnet.md) -Узнайте, как toocreate новый веб-приложение Azure из Visual Studio, используя любой из hello включены шаблоны приложений.
* [Развертывание tooAzure ваш код приложения службы](web-sites-deploy.md)-Узнайте, как toodeploy из FTP или источника контролировать репозиториев.
* [Добавление функциональности tooyour первого веб-приложения](app-service-web-get-started-2.md) -занять вашего приложения Azure toohello Далее уровня. Проверяйте подлинность пользователей. Масштабируйте приложение в зависимости от потребностей. Настраивайте оповещения производительности. И все это — с помощью нескольких действий.
