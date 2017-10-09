---
title: "aaaDeploy — приложение WordPress на портал Azure в течение пяти минут hello | Документы Microsoft"
description: "Узнайте, как просто можно toorun веб-приложений в службе приложений, развернув приложение WordPress. Кроме того, вы сможете быстро просмотреть результаты."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: cephalin
ms.openlocfilehash: 4cd26bbacf89657997847ded1284e472288ddebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-wordpress-app-in-hello-azure-portal-in-five-minutes"></a>Развертывание приложения WordPress в hello портал Azure в течение пяти минут

В этом учебнике показано как toodeploy первого [WordPress](https://wordpress.org/) веб-приложения слишком[службе приложений Azure](../app-service/app-service-value-prop-what-is.md) в минутах.

![Сайт WordPress](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a>Предварительные требования
Вам потребуется учетная запись Microsoft Azure. Если у вас нет учетной записи, [подпишитесь на бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) или [активируйте преимущества для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/) возможно даже без учетной записи Azure. Создание начального приложения и воспроизведение к ней до часа tooan--без кредитной карты требуется, не обязательства.
> 
> 

## <a name="deploy-hello-wordpress-app"></a>Развернуть приложение hello WordPress
1. Войдите в toohello [портал Azure](https://portal.azure.com).

2. Откройте страницу [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).

    Указывает tooimmediately ярлык настроить новое приложение WordPress в hello портал Azure.

3. В поле **Имя приложения** введите имя веб-приложения. Если вы увидите зеленый флажок в поле hello hello имя является уникальным в hello `azurewebsites.net` домена.
   
5. В **группы ресурсов**, нажмите кнопку **создать новый** toocreate новый [группы ресурсов](../azure-resource-manager/resource-group-overview.md), присвойте ему имя.

6. Из списка **Поставщик базы данных** выберите **CleaDB**.

7. Щелкните **Расположение или план службы приложений** > **Создать**. Настройка hello [план служб приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) следующим:

    - В **план служб приложений**, требуемое имя типа hello.
    - В **расположение**, выбрать план toohost расположение.
    - Щелкните **Ценовая категория**, а затем выберите **F1 Free** или другую категорию, которая вам подходит. Щелкните **Выбрать**.
    - Нажмите кнопку **ОК**.

8. Щелкните **База данных** > **Создать**. Настройте hello базы данных SQL, как показано.

    - В поле **Имя базы данных** введите имя базы данных. 
    - В **расположение**, выберите hello местоположения hello план служб приложений.
    - Щелкните **Ценовая категория**, а затем выберите **Mercury** или другую категорию, которая вам подходит. Щелкните **Выбрать**.
    - Выберите **Условия** и щелкните **Приобрести**.
    - Нажмите кнопку **ОК**.

9. Щелкните **Создать**.

    Теперь Azure создаст приложение WordPress на основе выбранной конфигурации. Должно появиться уведомление с текстом **Развертывание начато**.

    ![Начато развертывание: первое приложение WordPress в службе приложений Azure](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a>Запуск веб-приложения WordPress и управление им

Когда Azure завершит развертывание приложения, появится еще одно уведомление.

![Успешное развертывание: первое приложение WordPress в службе приложений Azure](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. Щелкните уведомление hello. Если вы пропустили всегда доступен, щелкнув hello уведомления колокольчика (![ниже уведомления - первый WordPress в службе приложений Azure](./media/app-service-web-get-started-dotnet-portal/notification.png)).

    Теперь должна отображаться [колонка](../azure-resource-manager/resource-group-portal.md#manage-resources) управления веб-приложением. (*Колонка*: горизонтальная страница портала.)

3. В hello вверху страницы обзора hello щелкните **Обзор**.
   
    ![Обзор: первое приложение WordPress в службе приложений Azure](./media/app-service-web-get-started-php-portal/browse.png)

    Теперь вы видите hello WordPress **приветствия** страницы. Настройка установки WordPress hello и начать воспроизведение с ним!

    ![Конфигурация WordPress: первое приложение WordPress в службе приложений Azure](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a>Дальнейшие действия
* [Создавать, настраивать и развертывать приложения tooAzure Laravel web](app-service-web-php-get-started.md) -овладеть основными навыками работы hello необходимо toorun любой PHP веб-приложения в Azure, такие как:

    * создание и настройка приложений в Azure с помощью PowerShell и Bash;
    * выбор версии PHP;
    * Используйте начальный файл, который не находится в корневом каталоге приложения hello.
    * Включение автоматизации Composer.
    * доступ к переменным конкретной среды;
    * устранение распространенных ошибок.

* [Развертывание tooAzure ваш код приложения службы](web-sites-deploy.md)-Узнайте, как toodeploy из FTP или источника контролировать репозиториев.
* [Добавление функциональности tooyour первого веб-приложения](app-service-web-get-started-2.md) -занять вашего приложения Azure toohello Далее уровня. Проверяйте подлинность пользователей. Масштабируйте приложение в зависимости от потребностей. Настраивайте оповещения производительности. И все это — с помощью нескольких действий.
