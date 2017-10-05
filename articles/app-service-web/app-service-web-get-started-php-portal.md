---
title: "Развертывание приложения WordPress на портале Azure за пять минут | Документация Майкрософт"
description: "Узнайте, как можно быстро запускать веб-приложения в службе приложений, развернув приложение WordPress. Кроме того, вы сможете быстро просмотреть результаты."
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
ms.openlocfilehash: ef3be9823384bd8dc978c86f5cfde00d1117c4a2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-wordpress-app-in-the-azure-portal-in-five-minutes"></a>Развертывание приложения WordPress на портале Azure за пять минут

В этом руководстве показано, как за считанные минуты развернуть свое первое веб-приложение [WordPress](https://wordpress.org/) в [службе приложений Azure](../app-service/app-service-value-prop-what-is.md).

![Сайт WordPress](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a>Предварительные требования
Вам потребуется учетная запись Microsoft Azure. Если у вас нет учетной записи, [подпишитесь на бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) или [активируйте преимущества для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/) возможно даже без учетной записи Azure. Вы можете создать приложение начального уровня и экспериментировать с ним в течение часа. Для этого вам не нужно указывать данные кредитной карты или брать на себя какие-либо обязательства.
> 
> 

## <a name="deploy-the-wordpress-app"></a>Развертывание приложения WordPress
1. Войдите на [портал Azure](https://portal.azure.com).

2. Откройте страницу [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).

    Эта ссылка позволит сразу перейти на страницу настройки нового приложения WordPress на портале Azure.

3. В поле **Имя приложения** введите имя веб-приложения. Если имя является уникальным в домене `azurewebsites.net`, то в поле появится зеленая галочка.
   
5. В разделе **Группа ресурсов** щелкните **Создать**, чтобы создать [группу ресурсов](../azure-resource-manager/resource-group-overview.md), и введите ее имя.

6. Из списка **Поставщик базы данных** выберите **CleaDB**.

7. Щелкните **Расположение или план службы приложений** > **Создать**. Настройте [план службы приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), как показано ниже.

    - В поле **План службы приложений** введите требуемое имя.
    - Из списка **Расположение** выберите расположение для размещения плана.
    - Щелкните **Ценовая категория**, а затем выберите **F1 Free** или другую категорию, которая вам подходит. Щелкните **Выбрать**.
    - Нажмите кнопку **ОК**.

8. Щелкните **База данных** > **Создать**. Настройте базу данных SQL, как показано ниже.

    - В поле **Имя базы данных** введите имя базы данных. 
    - Из списка **Расположение** выберите то же расположение, что и для плана службы приложений.
    - Щелкните **Ценовая категория**, а затем выберите **Mercury** или другую категорию, которая вам подходит. Щелкните **Выбрать**.
    - Выберите **Условия** и щелкните **Приобрести**.
    - Нажмите кнопку **ОК**.

9. Щелкните **Создать**.

    Теперь Azure создаст приложение WordPress на основе выбранной конфигурации. Должно появиться уведомление с текстом **Развертывание начато**.

    ![Начато развертывание: первое приложение WordPress в службе приложений Azure](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a>Запуск веб-приложения WordPress и управление им

Когда Azure завершит развертывание приложения, появится еще одно уведомление.

![Успешное развертывание: первое приложение WordPress в службе приложений Azure](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. Щелкните это уведомление. Если вы пропустили его, то всегда сможете открыть это уведомление, щелкнув значок уведомления (звонок). (![Уведомление внизу: первое приложение WordPress в службе приложений Azure](./media/app-service-web-get-started-dotnet-portal/notification.png).)

    Теперь должна отображаться [колонка](../azure-resource-manager/resource-group-portal.md#manage-resources) управления веб-приложением. (*Колонка*: горизонтальная страница портала.)

3. В верхней части страницы обзора щелкните **Обзор**.
   
    ![Обзор: первое приложение WordPress в службе приложений Azure](./media/app-service-web-get-started-php-portal/browse.png)

    Теперь вы видите страницу **приветствия** WordPress. Настройте установленное приложение WordPress и поэкспериментируйте с ним.

    ![Конфигурация WordPress: первое приложение WordPress в службе приложений Azure](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a>Дальнейшие действия
* [Создание, настройка и развертывание веб-приложения PHP в Azure](app-service-web-php-get-started.md). Изучите базовые навыки, необходимые для запуска любого веб-приложения PHP в Azure, в том числе:

    * создание и настройка приложений в Azure с помощью PowerShell и Bash;
    * выбор версии PHP;
    * использование файла запуска, который находится не в корневом каталоге приложения;
    * Включение автоматизации Composer.
    * доступ к переменным конкретной среды;
    * устранение распространенных ошибок.

* [Развертывание приложения в службе приложений Azure](web-sites-deploy.md). Узнайте, как развернуть свой код из FTP или репозиториев системы управления версиями.
* [Добавление функциональных возможностей в первое веб-приложение](app-service-web-get-started-2.md). Выведите приложение Azure на следующий уровень. Проверяйте подлинность пользователей. Масштабируйте приложение в зависимости от потребностей. Настраивайте оповещения производительности. И все это — с помощью нескольких действий.
