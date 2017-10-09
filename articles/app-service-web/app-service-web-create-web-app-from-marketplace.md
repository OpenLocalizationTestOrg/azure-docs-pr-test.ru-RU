---
title: "aaaCreate веб-приложения из hello Azure Marketplace | Документы Microsoft"
description: "Узнайте, как toocreate новое веб-приложение WordPress из hello Azure Marketplace с помощью hello портала Azure."
services: app-service\web
documentationcenter: 
author: sunbuild
manager: erikre
editor: 
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: sunbuild
ms.custom: mvc
ms.openlocfilehash: 5ad1ca2f3f7831d857c3e9b02738b6b34acf3649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-from-hello-azure-marketplace"></a>Создание веб-приложения из hello Azure Marketplace
<!-- Note: This article replaces web-sites-php-web-site-gallery.md -->

[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

Hello Azure Marketplace предоставляет широкий набор популярных веб-приложений, разработанных с открытым исходным кодом сообщества программного обеспечения, например WordPress и Umbraco CMS. В этом учебнике вы узнаете, как приложение WordPress toocreate из Azure marketplace.
При котором создается веб-приложение Azure и база данных MySQL. 

![Пример панели мониторинга веб-приложения WordPress](./media/app-service-web-create-web-app-from-marketplace/wpdashboard2.png)

## <a name="before-you-begin"></a>Перед началом работы 

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) , прежде чем начинать работу.

## <a name="deploy-from-azure-marketplace"></a>Развертывание из Azure Marketplace
Выполните действия hello ниже toodeploy WordPress из Azure Marketplace.

### <a name="sign-in-tooazure"></a>Войдите в tooAzure
Войдите в toohello [портал Azure](https://portal.azure.com).

### <a name="deploy-wordpress-template"></a>Развертывание шаблона WordPress
Hello Azure Marketplace предоставляет шаблоны для настройки ресурсов, программа установки hello [WordPress](https://portal.azure.com/#create/WordPress.WordPress) tooget шаблона к работе.
   
Введите ниже hello сведения toodeploy hello WordPress приложения и его ресурсов.

  ![Последовательность создания приложения WordPress](./media/app-service-web-create-web-app-from-marketplace/wordpress-portal-create.png)


| Поле         | Рекомендуемое значение           | Описание  |
| ------------- |-------------------------|-------------|
| Имя приложения      | mywordpressapp          | Введите уникальное **имя веб-приложения**. Это имя используется как часть имени DNS по умолчанию hello в приложении `<app_name>.azurewebsites.net`, поэтому он должен toobe уникальным для всех приложений в Azure. Позже можно сопоставить приложении tooyour имя пользовательского домена, перед тем, как он tooyour пользователей |
| Подписки  | Оплата по мере использования             | Выберите **подписку**. Если у вас несколько подписок, выберите нужную подписку hello. |
| Группа ресурсов| mywordpressappgroup                 |    Укажите **группу ресурсов**. Группа ресурсов — это логический контейнер, в котором происходит развертывание ресурсов Azure (веб-приложений, баз данных и т. д.) и управление ими. Можно создать новую группу ресурсов или использовать существующую. |
| План обслуживания приложения | myappplan          | Планы служб приложений представляют коллекцию hello toohost физические ресурсы, используемые приложения. Выберите hello **расположение** и hello **Ценовая категория**. Дополнительные сведения о ценах см. в разделе [Ценовая категория службы приложений](https://azure.microsoft.com/pricing/details/app-service/). |
| База данных      | mywordpressapp          | Выберите поставщика hello соответствующей базы данных для MySQL. Веб-приложения поддерживают **ClearDB**, **базу данных Azure для MySQL** и **MySQL в приложении**. Дополнительные сведения см. в разделе [Конфигурация базы данных](#database-config) ниже. |
| Application Insights | "Вкл." или "Выкл."          | Это необязательно. Если щелкнуть **Вкл.**, [Application Insights](https://azure.microsoft.com/en-us/services/application-insights/) будет предоставлять службы мониторинга для веб-приложения.|

<a name="database-config"></a>

### <a name="database-configuration"></a>Конфигурация базы данных
Выполните hello ниже действия в зависимости от выбранного поставщика базы данных MySQL.  Рекомендуется использовать базы данных, веб-приложения и MySQL в hello местоположения.

#### <a name="cleardb"></a>ClearDB 
[ClearDB](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview) — это стороннее решение для полностью интегрированной службы MySQL в Azure. В базах данных ClearDB toouse заказ, вам потребуется tooassociate tooyour кредитной карты [учетная запись Azure](http://account.windowsazure.com/subscriptions). Если был выбран поставщик базы данных ClearDB, вы можете просмотреть список существующих баз данных toochoose из или щелкнуть **создать новый** кнопку toocreate базы данных.

![Создание базы данных ClearDB](./media/app-service-web-create-web-app-from-marketplace/mysqldbcreate.png)

#### <a name="azure-database-for-mysql-preview"></a>База данных Azure для MySQL (предварительная версия)
[База данных Azure для MySQL](https://azure.microsoft.com/en-us/services/mysql) предоставляет управляемая служба баз данных, для разработки приложений и развертывания, который позволяет toostand базу данных MySQL в минутах и шкалы в hello полет вы доверяете наиболее облаке hello. С помощью включительно модели ценообразования, можно получить все возможности hello, требуется как высокого уровня доступности, безопасности и восстановления – встроенным, бесплатной стоимость. Нажмите кнопку **Ценовая категория** toochoose другой [ценовой категории](https://azure.microsoft.com/pricing/details/mysql). toouse существующей базы данных или существующий сервер MySQL, используйте существующую группу ресурсов, в которых hello находится сервер. 

![Настройка параметров hello базы данных для веб-приложения hello](./media/app-service-web-create-web-app-from-marketplace/wordpress-azure-database.PNG)

> [!NOTE]
>  База данных Azure для MySQL (предварительная версия) и веб-приложение на платформе Linux (предварительная версия) доступны не во всех регионах. Дополнительные сведения о toolearn [базы данных Azure для MySQL (Предварительная версия)](https://docs.microsoft.com/en-us/azure/mysql) и [веб-приложения на платформе Linux](./app-service-linux-intro.md) ограничения. 

#### <a name="mysql-in-app"></a>MySQL в приложении
[MySQL в приложении](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app) — это функция службы приложений, который разрешает запуск MySql в собственном коде на платформе hello. Основные функции Hello поддерживается в выпуске hello hello компонента:

- Сервер MySQL, работающих на hello же экземпляра параллельно с веб-сервера размещения hello узла. Это повышает производительность вашего приложения
- Хранилище совместно используется для MySQL и файлов веб-приложения. Примечание с бесплатных и общих планов, которые вы можете достигнуть нашей квоту при помощью hello сайта на основе hello действий можно выполнить. Ознакомьтесь с [лимитами квоты](https://azure.microsoft.com/en-us/pricing/details/app-service/plans/) для планов "Бесплатный" и "Общий".
- Можно включить медленное ведение журнала и общее ведение журнала для MySQL. Обратите внимание, что это может повлиять на производительность сайта hello и следует не всегда включено. Функция ведения журнала Hello помогает анализе проблем с приложениями. 

Дополнительные сведения см. в [этой статье](https://blogs.msdn.microsoft.com/appserviceteam/2016/08/18/announcing-mysql-in-app-preview-for-web-apps/ ).

![Управление MySQL в приложении](./media/app-service-web-create-web-app-from-marketplace/mysqlinappmanage.PNG)

Можно отслеживать ход выполнения hello, щелкнув значок колокольчика hello hello верхней части страницы портала hello при приветствия WordPress приложение развертывается.    
![Индикатор хода выполнения](./media/app-service-web-create-web-app-from-marketplace/deploy-success.png)

## <a name="manage-your-new-azure-web-app"></a>Управление новым веб-приложением Azure

Go toohello Azure портала tootake рассмотрим hello веб-приложения, который вы только что создали.

toodo, вход слишком[https://portal.azure.com](https://portal.azure.com).

Hello в левом меню, щелкните **службы приложений**, затем щелкните имя hello Azure веб-приложения.

![Веб-приложения портала навигации tooAzure](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-list.png)


Вы попадете в _колонку_ веб-приложения (страница портала, открывшаяся горизонтально).

По умолчанию колонки веб-приложение отображает hello **Обзор** страницы. Здесь вы можете наблюдать за работой приложения. Вы также можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление. вкладки Hello hello левой части колонки hello показывает страницы hello другой конфигурации, которые можно открыть.

![Колонка службы приложений на портале Azure](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-detail.png)

Эти закладки в колонке hello показывают hello множеством замечательных функций, можно добавить tooyour веб-приложения. После списка Hello предоставляет несколько возможностей hello:

* сопоставление настраиваемого DNS-имени;
* привязка настраиваемого SSL-сертификата;
* настройка непрерывного развертывания;
* вертикальное и горизонтальное масштабирование;
* добавление аутентификации пользователей.

Завершите 5-минутного WordPress установки мастер toohave WordPress приложение hello запуска. Извлечение [документации Wordpress](https://codex.WordPress.org/) toodevelop веб-приложения.

![Мастер установки WordPress](./media/app-service-web-create-web-app-from-marketplace/wplanguage.png)

## <a name="configuring-your-app"></a>Настройка приложения 
Необходимо выполнить несколько действий по управлению приложением WordPress, прежде чем оно будет готово к использованию в рабочей среде. Выполните эти шаги tooconfigure и управления WordPress приложения:

| toodo это... | Используйте это... |
| --- | --- |
| **Отправка или хранение больших файлов** |[Подключаемый модуль WordPress для использования хранилища BLOB-объектов](https://wordpress.org/plugins/windows-azure-storage/)|
| **Отправка электронной почты** |Покупки [SendGrid](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SendGrid.SendGrid?tab=Overview) службы электронной почты и использовать hello [подключаемого модуля WordPress с помощью SendGrid](https://wordpress.org/plugins/sendgrid-email-delivery-simplified/) tooconfigure его|
| **Личные доменные имена** |[Настройка личного доменного имени в службе приложений Azure](app-service-web-tutorial-custom-domain.md) |
| **HTTPS** |[Включите протокол HTTPS для веб-приложения в службе приложений Azure](app-service-web-tutorial-custom-ssl.md). |
| **Предварительная проверка** |[Настройте промежуточную среду и среду разработки для веб-приложений в службе приложений Azure](web-sites-staged-publishing.md).|
| **Мониторинг и устранение неполадок** |[Включите ведение журнала диагностики для веб-приложений в службе приложений Azure](web-sites-enable-diagnostic-log.md) и [осуществляйте мониторинг веб-приложений в службе приложений Azure](app-service-web-tutorial-monitoring.md). |
| **Развертывание сайта** |[Разверните веб-приложение в службе приложений Azure](app-service-deploy-local-git.md). |


## <a name="secure-your-app"></a>Защита приложения 
Необходимо выполнить несколько действий по управлению приложением WordPress, прежде чем оно будет готово к использованию в рабочей среде. Выполните эти шаги tooconfigure и управления WordPress приложения:

| toodo это... | Используйте это... |
| --- | --- |
| **Надежное имя пользователя и пароль**|  Часто изменяйте пароль. Не применяйте часто используемые имена пользователей, например *admin* или *wordpress* и т. д. Принудительно все пользователи WordPress toouse уникальное имя пользователя и надежный пароль. |
| **Установка обновлений** | Сохраните ваш основной WordPress, темы, подключаемые модули копирование toodate. Используйте hello последней среды выполнения PHP доступны в службе приложений Azure |
| **Обновление ключей безопасности WordPress** | Обновление [ключ безопасности WordPress](https://codex.wordpress.org/Editing_wp-config.php#Security_Keys) tooimprove шифрования, хранимые в файлах cookie|

## <a name="improve-performance"></a>Повышение производительности
Производительность в облаке hello достигается в основном через кэширование и масштабирования. Тем не менее следует рассматривать hello памяти, пропускной способности и другие атрибуты размещения веб-приложений.

| toodo это... | Используйте это... |
| --- | --- |
| **Общая информация о возможностях экземпляра службы приложений** |[Информация о ценах, в том числе о возможностях уровней службы приложений](https://azure.microsoft.com/en-us/pricing/details/app-service/).|
| **Ресурсы кэша** |Используйте [кэш Azure Redis](https://azure.microsoft.com/en-us/services/cache/), или один из hello другими предложениями кэширования в hello [хранилища Azure](https://azuremarketplace.microsoft.com) |
| **Масштабирование приложения** |Требуется tooscale [hello веб-приложения в службе приложений Azure](web-sites-scale.md) или база данных MySQL. Функция "MySQL в приложении" не поддерживает развертывание, поэтому выберите ClearDB или базу данных Azure для MySQL (предварительная версия). [Масштабирование базы данных SQL Azure для MySQL (Предварительная версия)](https://azure.microsoft.com/en-us/pricing/details/mysql/) или при использовании [ClearDB высокий уровень доступности маршрутизации](http://w2.cleardb.net/faqs/) tooscale копирование базы данных |

## <a name="availability-and-disaster-recovery"></a>Доступность и аварийное восстановление
Высокий уровень доступности включает в себя hello аспектом непрерывности бизнеса toomaintain аварийного восстановления. Для планирования устранения сбоев и аварий в облаке hello необходимо сбоев hello toorecognize быстро. Эти решения помогают реализовать стратегию для обеспечения высокого уровня доступности.

| toodo это... | Используйте это... |
| --- | --- |
| **Сайты балансировки нагрузки** или **геораспределенные сайты** |[Используйте маршрутизацию трафика с помощью диспетчера трафика Azure](https://azure.microsoft.com/en-us/services/traffic-manager/). |
| **Архивация и восстановление** |[Архивируйте веб-приложение в Azure](web-sites-backup.md) и [восстанавливайте веб-приложение в Azure](web-sites-restore.md). |

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о различных компонентов [toodevelop службы приложений и масштаб](/app-service-web/).
