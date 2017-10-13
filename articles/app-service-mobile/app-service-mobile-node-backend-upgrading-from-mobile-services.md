---
title: "Обновление приложения мобильных служб до службы приложений Azure — Node.js"
description: "Узнайте, как без труда обновить приложение мобильных служб до мобильного приложения службы приложений."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: c58f6df0-5aad-40a3-bddc-319c378218e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5fc61fed674f0d2fc64bc29c064e7e872b4f2e68
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="upgrade-your-existing-nodejs-azure-mobile-service-to-app-service"></a>Обновление существующего приложения мобильной службы Azure Node.js до службы приложений
Мобильное приложение службы приложений — это новый способ сборки мобильных приложений с помощью Microsoft Azure. Дополнительные сведения см. в статье [Общие сведения о мобильных приложениях].

В этой статье описывается процесс обновления существующего серверного приложения Node.js мобильных служб Azure до нового мобильного приложения службы приложений. Во время обновления существующее приложение мобильных служб может продолжать работать.  Если необходимо обновить приложение с серверной частью Node.js, см. статью [Обновление существующего приложения мобильной службы Azure .NET до службы приложений](app-service-mobile-net-upgrading-from-mobile-services.md).

Когда мобильное серверное приложение обновляется до службы приложений Azure, оно получает доступ ко всем возможностям службы приложений. Тарификация при этом будет осуществляться в соответствии с [ценами службы приложений], а не мобильных служб.

## <a name="migrate-vs-upgrade"></a>Миграция или обновление
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> Перед обновлением рекомендуется [выполнить миграцию](app-service-mobile-migrating-from-mobile-services.md) . Таким образом, к обеим версиям приложения будет применен один тарифный план службы, а дополнительные затраты будут исключены.
>
>

### <a name="improvements-in-mobile-apps-nodejs-server-sdk"></a>Улучшения в пакете SDK сервера Node.js мобильных приложений
Обновление до нового [пакета SDK для мобильных приложений](https://www.npmjs.com/package/azure-mobile-apps) содержит множество улучшений, в частности:

* Новый упрощенный пакет SDK для Node, созданный на [платформе Express](http://expressjs.com/en/index.html), разработан специально для новых версий Node, которые будут выпускаться. Поведение приложения можно настроить с помощью ПО промежуточного слоя Express.
* Значительное повышение производительности по сравнению с пакетом SDK для мобильных служб.
* Веб-сайт можно разместить вместе с мобильным сервером. Аналогичным образом можно легко добавить пакет SDK для мобильных приложений Azure в любое существующее приложение express.v4.
* Пакет SDK для мобильных приложений предназначен для кроссплатформенной и локальной разработки. Поэтому приложения с его использованием можно разрабатывать и запускать локально на платформах Windows, Linux и OSX. Теперь стало удобнее использовать распространенные методы разработки Node (например, выполнение тестов [Mocha](https://mochajs.org/) перед развертыванием).

## <a name="overview"></a>Общие сведения об обновлении
Чтобы упростить обновление серверной части Node.js, служба приложений Azure предоставила пакет обеспечения совместимости.  После обновления вы получите новый сайт, который можно развернуть в службе приложений.

Пакеты SDK для клиента мобильных служб **несовместимы** с новым пакетом SDK для сервера мобильных приложений. Чтобы обеспечить непрерывность обслуживания приложения, не следует публиковать изменения на сайте, который в настоящее время обслуживает опубликованные клиенты. Вместо этого нужно создать новое мобильное приложение, которое является дубликатом. Это приложение можно включить в тот же план службы приложений, чтобы избежать дополнительных финансовых затрат.

После этого у вас будет две версии приложения: одна, которая остается без изменений и обслуживает опубликованные приложения на практике, и другая, которую можно обновить и ориентировать на новый выпуск клиента. Переносить и тестировать код можно в любое удобное для вас время. Однако перед этим необходимо убедиться, что внесенные исправления применены к обеим версиям. Если вы считаете, что до последней версии уже обновлено требуемое количество клиентских приложений, при желании можно удалить исходное перенесенное приложение. При размещении в одном плане службы приложений с мобильным приложением дополнительная плата не взимается.

Полная схема процесса обновления выглядит следующим образом.

1. Скачайте имеющуюся (перенесенную) мобильную службу Azure.
2. Преобразуйте проект в мобильное приложение Azure с помощью пакета обеспечения совместимости.
3. Устраните все различия (например, параметры проверки подлинности).
4. Разверните преобразованный проект мобильного приложения Azure в новую службу приложений.
5. Выпустите новую версию клиентского приложения, которая использует новое мобильное приложение.
6. (Необязательно.) Удалите исходное перенесенное приложение мобильной службы.

Удаление может произойти при отсутствии трафика к исходному перенесенному приложению мобильной службы.

## <a name="install-npm-package"></a> Установка необходимых компонентов
На локальном компьютере необходимо установить [Node].  Кроме того, требуется установить пакет обеспечения совместимости.  После установки Node можно выполнить следующую команду в новой командной строке или строке PowerShell:

```npm i -g azure-mobile-apps-compatibility```

## <a name="obtain-ams-scripts"></a> Получение скриптов мобильных служб Azure
* Войдите на [портал Azure].
* Чтобы найти сайт мобильных служб, щелкните **Все ресурсы** или **Службы приложений**.
* Чтобы перейти на сайт Kudu, на сайте щелкните **Средства** -> **Kudu** -> **Перейти**.
* Чтобы открыть консоль отладки, щелкните **Консоль отладки** -> **PowerShell**.
* Перейдите в папку `site/wwwroot/App_Data/config` , щелкнув каждый каталог по очереди.
* Щелкните значок скачивания рядом с каталогом `scripts` .

После этого будут скачаны скрипты в формате ZIP.  Создайте каталог на локальном компьютере и распакуйте в нем файл `scripts.ZIP` .  В результате будет создан каталог `scripts` .

## <a name="scaffold-app"></a> Формирование шаблонов серверной части новых мобильных приложений Azure
Выполните следующую команду в каталоге, содержащем скрипты:

```scaffold-mobile-app scripts out```

Будут созданы сформированные шаблоны серверной части мобильных приложений Azure в каталоге `out`.  Рекомендуется зарегистрировать каталог `out` в желаемом репозитории исходного кода. Хотя это и не обязательно.

## <a name="deploy-ama-app"></a> Развертывание серверной части мобильных приложений Azure
Во время развертывания необходимо сделать следующее:

1. Создайте мобильное приложение на [портал Azure].
2. Выполните скрипт `createViews.sql` в подключенной базе данных.
3. Свяжите базу данных, привязанную к вашей мобильной службе, с новой службой приложений.
4. Свяжите все ресурсы (например, Центры уведомлений) с новой службой приложений.
5. Разверните созданный код на новом сайте.

### <a name="create-a-new-mobile-app"></a>Создание нового мобильного приложения.
1. Войдите на [портал Azure].
2. Щелкните **+Создать** > **Интернет+мобильные устройства** > **Мобильное приложение**, а затем введите имя серверной части мобильного приложения.
3. В поле **Группа ресурсов**выберите существующую группу ресурсов или создайте новую (с тем же именем, что и у приложения).

    Выберите другой план службы приложений или создайте новый. Дополнительные сведения о планах службы приложений, а также о создании плана другой ценовой категории и в другом расположении см. в статье [Подробный обзор планов службы приложений Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
4. В качестве **плана службы приложений**используется план по умолчанию (для [уровня "Стандартный"](https://azure.microsoft.com/pricing/details/app-service/)). Вы также можете [создать план](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan) или выбрать другой. Параметры плана службы приложений определяют [расположение, функции, стоимость и вычислительные ресурсы](https://azure.microsoft.com/pricing/details/app-service/) , связанные с вашим приложением.

    Выбрав план, нажмите кнопку **Создать**. Будет создана серверная часть мобильного приложения,

### <a name="run-createviewssql"></a>Выполнение CreateViews.SQL
Сформированный шаблон приложения содержит файл с именем `createViews.sql`.  Этот скрипт должен выполняться в целевой базе данных.  Строку подключения целевой базы данных можно получить из перенесенной мобильной службы в разделе **Строки подключения** в колонке **Параметры**.  Ее название — `MS_TableConnectionString`.

Этот скрипт можно выполнить в среде SQL Server Management Studio или Visual Studio.

### <a name="link-the-database-to-your-app-service"></a>Связывание базы данных со службой приложений
Чтобы связать имеющуюся базу данных со службой приложений, сделайте следующее:

* Откройте службу приложений на [портал Azure].
* Выберите **Все параметры** -> **Подключения к данным**.
* Щелкните **+ Add**(+ Добавить).
* В раскрывающемся списке выберите **База данных SQL**
* В разделе **База данных SQL** выберите имеющуюся базу данных, а затем щелкните **Выбрать**.
* В разделе **Строка подключения** введите имя пользователя и пароль для базы данных, а затем нажмите кнопку **ОК**.
* В колонке **Add data connections** (Добавление подключений к данным) нажмите кнопку **ОК**.

Имя пользователя и пароль можно найти, просмотрев строку подключения целевой базы данных в перенесенной мобильной службе.

### <a name="set-up-authentication"></a>Настройка проверки подлинности
Мобильные приложения Azure позволяют настроить проверку подлинности в Azure Active Directory, Facebook, Google, Microsoft и Twitter прямо в службе.  Пользовательскую проверку подлинности необходимо настроить отдельно.  Дополнительные сведения см. в документации, посвященной [методам] и [быстрому запуску проверки подлинности].  

## <a name="updating-clients"></a>Обновление мобильных клиентов
После получения рабочей серверной части мобильных приложений вы можете работать с новой версией клиентского приложения, которое использует эту серверную часть. Мобильные приложения также содержат новую версию клиентских пакетов SDK. Поэтому, как и при обновлении сервера, перед установкой версий мобильных приложений потребуется удалить все ссылки на пакеты SDK для мобильных служб.

Одно из основных различий между версиями заключается в том, что конструкторам больше не требуется ключ приложения.
Просто передайте URL-адрес мобильного приложения. Например, в клиентах .NET конструктор `MobileServiceClient` теперь выглядит так:

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net" // URL of the Mobile App
        );

Сведения об установке новых пакетов SDK и использовании новой структуры см. по ссылкам ниже:

* [Android 2.2 или более поздней версии](app-service-mobile-android-how-to-use-client-library.md)
* [iOS 3.0.0 или более поздней версии](app-service-mobile-ios-how-to-use-client-library.md)
* [.NET (Windows/Xamarin) 2.0.0 или более поздней версии](app-service-mobile-dotnet-how-to-use-client-library.md)
* [Apache Cordova 2.0 или более поздней версии](app-service-mobile-cordova-how-to-use-client-library.md)

Если приложение использует push-уведомления, обратите внимание на особые инструкции по регистрации для каждой платформы, так как они немного изменились.

Когда новая версия клиента будет готова, испробуйте ее в новом обновленном серверном проекте. После проверки ее работы вы можете предоставить новую версию приложения клиентам. Когда как клиенты смогут получить эти обновления, версию мобильных служб приложения можно удалить. Этот шаг завершает обновление до мобильного приложения службы приложений с помощью последнего пакета SDK сервера мобильных приложений.

<!-- URLs. -->

[Портал Azure]: https://portal.azure.com/
[Azure classic portal]: https://manage.windowsazure.com/
[Общие сведения о мобильных приложениях]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[Mobile App Server SDK]: https://www.npmjs.com/package/azure-mobile-apps
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications to your mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication to your mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure Scheduler]: /en-us/documentation/services/scheduler/
[Web Job]: https://github.com/Azure/azure-webjobs-sdk/wiki
[How to use the .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services to an App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service to App Service]: app-service-mobile-migrating-from-mobile-services.md
[ценами службы приложений]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[.NET server SDK overview]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[методам]: ../app-service/app-service-authentication-overview.md
[быстрому запуску проверки подлинности]: app-service-mobile-auth.md

[портал Azure]: https://portal.azure.com/
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js package]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
