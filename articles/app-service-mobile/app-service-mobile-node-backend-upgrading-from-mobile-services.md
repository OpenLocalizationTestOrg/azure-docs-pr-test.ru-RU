---
title: "aaaUpgrade из мобильных служб tooAzure службы приложений — Node.js"
description: "Узнайте, как tooeasily обновление вашего tooan приложения мобильных служб приложение службы мобильных приложений"
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
ms.openlocfilehash: 722cda244d4f633247827f58ea6f1397137ea600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-nodejs-azure-mobile-service-tooapp-service"></a>Обновление вашей существующей мобильной службы Azure Node.js tooApp службы
Мобильные приложения службы-это новый способ toobuild мобильных приложений с помощью Microsoft Azure. toolearn более, в разделе [Каковы мобильные приложения?].

В этом разделе описывается способ tooupgrade существующее приложение Node.js серверной части из мобильных служб Azure tooa новые мобильные приложения службы приложений. При выполнении этого обновления существующего приложения мобильных служб можно продолжить toooperate.  Если вам требуется tooupgrade Node.js внутреннее приложение, см. слишком[обновление мобильных служб .NET](app-service-mobile-net-upgrading-from-mobile-services.md).

Когда мобильной серверной части tooAzure обновленной службы приложений, он имеет доступ tooall функции службы приложений и являются выставлен счет на слишком в соответствии с[служб приложений Ценовая], цены не мобильных служб.

## <a name="migrate-vs-upgrade"></a>Миграция или обновление
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> Перед обновлением рекомендуется [выполнить миграцию](app-service-mobile-migrating-from-mobile-services.md) . Таким образом, можно поместить обе версии приложения hello же план службы приложений и создают без дополнительных затрат.
>
>

### <a name="improvements-in-mobile-apps-nodejs-server-sdk"></a>Улучшения в пакете SDK сервера Node.js мобильных приложений
Обновление нового toohello [пакет SDK для мобильных приложений](https://www.npmjs.com/package/azure-mobile-apps) предоставляет множество улучшений, включая:

* В зависимости от hello [Express framework](http://expressjs.com/en/index.html), hello SDK новый узел простых и предназначен tookeep вверх в новых версиях узла, как они продвижением. Можно настроить поведение приложения hello с по промежуточного слоя, экспресс-выпуск.
* Значительное повышение производительности по сравнению toohello пакет SDK мобильных служб.
* Теперь можно размещать веб-сайте вместе с мобильного внутреннего сервера; Аналогичным образом это легко tooadd hello пакет SDK Azure Mobile tooany существующие express.v4 приложение.
* Построен для разработки кросс платформенных и локальные hello пакет SDK для мобильных приложений разработки и запускать локально на платформах Windows, Linux и OSX. Теперь является просто toouse общий узел разработки такие методы, как работает [Mocha](https://mochajs.org/) toodeployment предыдущих тестов.

## <a name="overview"></a>Общие сведения об обновлении
tooaid при обновлении Node.js серверное приложение службы приложений Azure обеспечивает совместимость пакета.  После обновления необходимо будет сайту niew, который может быть развернутой tooa нового узла служб приложений.

Hello клиента мобильных служб, пакеты SDK **не** совместимой с сервером новые мобильные приложения hello SDK. Непрерывность tooprovide порядок службу для своего приложения не следует публиковать изменения tooa сайта в настоящее время обслуживая клиентов, опубликованной. Вместо этого нужно создать новое мобильное приложение, которое является дубликатом. Можно поместить это приложение hello же приложение службы плана tooavoid дополнительных финансовых затрат.

Затем имеется две версии приложения hello:, остается таким же hello и служит опубликованных приложений практике hello и другой, которую затем можно обновить и целевой объект с новым клиентом выпуска. Можно перемещать и тестирования кода в темпе, но следует убедиться в том, все исправления, внесенные get примененных tooboth. Если вы считаете, что требуемое число клиентских приложений на практике обновили toohello последней версии, при желании можно удалить исходный перенесенные приложение hello. Она не создает дополнительных денежных затрат, если в же службы приложений планировать в мобильные приложения hello.

Hello полной структуры для hello процесс обновления выглядит следующим образом:

1. Скачайте имеющуюся (перенесенную) мобильную службу Azure.
2. Преобразование проекта hello tooan мобильного приложения Azure с помощью пакета совместимости hello.
3. Устраните все различия (например, параметры проверки подлинности).
4. Развертывание вашей преобразованный проект tooa мобильного приложения Azure нового приложения службы.
5. Выпускает новую версию клиентского приложения hello, используйте новый мобильного приложения.
6. (Необязательно.) Удалите исходное перенесенное приложение мобильной службы.

Удаление может произойти при отсутствии трафика к исходному перенесенному приложению мобильной службы.

## <a name="install-npm-package"></a>Установите необходимые компоненты hello
На локальном компьютере необходимо установить [Node].  Также следует установить пакет совместимости hello.  После установки узла можно запустить следующую команду из командной строки PowerShell или cmd новый hello:

```npm i -g azure-mobile-apps-compatibility```

## <a name="obtain-ams-scripts"></a> Получение скриптов мобильных служб Azure
* Войдите в toohello [портала Azure].
* Чтобы найти сайт мобильных служб, щелкните **Все ресурсы** или **Службы приложений**.
* В пределах сайта hello, нажмите кнопку **средства** -> **Kudu** -> **Go** tooopen hello Kudu сайта.
* Щелкните **консоли отладки** -> **PowerShell** консоли отладки tooopen hello.
* Перейдите в слишком`site/wwwroot/App_Data/config` , щелкнув на каждый каталог, в свою очередь
* Нажмите кнопку Далее toohello hello загрузки значок `scripts` каталога.

Будет загружен в формате ZIP скрипты hello.  Создать новый каталог на локальном компьютере и распакуйте hello `scripts.ZIP` файл в каталоге hello.  В результате будет создан каталог `scripts` .

## <a name="scaffold-app"></a>Формировать hello новую серверную часть мобильных приложений Azure
Выполните следующую команду из hello каталог, содержащий каталог scripts hello hello.

```scaffold-mobile-app scripts out```

Это создаст формирования шаблонов серверной части мобильных приложений Azure в hello `out` каталога.  Хотя это необязательно, это разумно toocheck hello `out` каталога в репозиторий исходного кода по своему усмотрению.

## <a name="deploy-ama-app"></a> Развертывание серверной части мобильных приложений Azure
Во время развертывания необходимо будет toodo hello следующее:

1. Создавать приложения для мобильных устройств в hello [портала Azure].
2. Запустите hello `createViews.sql` сценария подключенной базы данных.
3. База данных hello ссылки, связанные tooyour tooyour мобильной службы нового приложения службы.
4. Связать все другие ресурсы (такие как концентраторы уведомлений) toohello нового приложения службы.
5. Развертывание hello созданный код tooyour новый сайт.

### <a name="create-a-new-mobile-app"></a>Создание нового мобильного приложения.
1. Войдите на hello [портала Azure].
2. Щелкните **+Создать** > **Интернет+мобильные устройства** > **Мобильное приложение**, а затем введите имя серверной части мобильного приложения.
3. Для hello **группы ресурсов**, выберите существующую группу ресурсов или создайте новую (с помощью hello совпадает с именем приложения).

    Выберите другой план службы приложений или создайте новый. Для получения дополнительных сведений о планах службы приложений и как уровня toocreate новый план, различные цен и в нужное расположение, в разделе [исчерпывающий обзор планы службы приложений Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
4. Для hello **план служб приложений**, план по умолчанию hello (в hello [стандартного уровня](https://azure.microsoft.com/pricing/details/app-service/)) установлен. Вы также можете [создать план](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan) или выбрать другой. Hello параметры плана служб приложений определяют hello [расположение, функции, стоимость и вычислительные ресурсы](https://azure.microsoft.com/pricing/details/app-service/) связанные с вашим приложением.

    После выбора плана hello, нажмите кнопку **создать**. При этом создается внутренний мобильное приложение hello.

### <a name="run-createviewssql"></a>Выполнение CreateViews.SQL
формирования шаблонов приложение Hello содержит файл с именем `createViews.sql`.  Этот скрипт должен выполняться в целевой базе данных.  Hello строку подключения для целевой базы данных hello можно получить из перенесенных мобильной службы из hello **параметры** колонке под **строки подключения**.  Ее название — `MS_TableConnectionString`.

Этот скрипт можно выполнить в среде SQL Server Management Studio или Visual Studio.

### <a name="link-hello-database-tooyour-app-service"></a>Ссылка hello tooyour базы данных служб приложений
Свяжите существующий hello tooyour базы данных приложения службы.

* В hello [портала Azure], откройте приложение службы.
* Выберите **Все параметры** -> **Подключения к данным**.
* Щелкните **+ Add**(+ Добавить).
* В hello раскрывающийся список, выберите **базы данных SQL**
* В разделе **База данных SQL** выберите имеющуюся базу данных, а затем щелкните **Выбрать**.
* В разделе **строка подключения**, введите hello имя пользователя и пароль для базы данных hello, а затем щелкните **ОК**.
* В hello **Добавление подключения к данным** колонка, щелкните здесь **ОК**.

Hello имя пользователя и пароль можно найти, просмотрев hello строку подключения для целевой базы данных hello в перенесенных мобильной службе.

### <a name="set-up-authentication"></a>Настройка проверки подлинности
Мобильные приложения Azure разрешает проверку подлинности Azure Active Directory, Facebook, Google, Microsoft и Twitter tooconfigure в службе hello.  Нестандартная проверка подлинности потребуется toobe разработан отдельно.  Ссылаться на приветствия [понятия проверки подлинности] документации и [примеры использования проверки подлинности] Дополнительные сведения см.  

## <a name="updating-clients"></a>Обновление мобильных клиентов
После получения рабочей серверной части мобильных приложений вы можете работать с новой версией клиентского приложения, которое использует эту серверную часть. Мобильные приложения также включает в себя новую версию клиента hello пакеты SDK и аналогичные обновления сервера toohello выше, необходимо будет tooremove все ссылки toohello Mobile Services SDK перед установкой версий мобильные приложения.

Одним из hello основные различия между версиями hello является то, что конструкторы hello больше не требуется ключ приложения.
Теперь просто передать URL-адрес hello мобильного приложения. Например, для клиентов .NET hello, hello `MobileServiceClient` конструктор больше не:

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net" // URL of hello Mobile App
        );

Вы можете прочесть об установке hello новых пакетов SDK и с помощью новой структуры hello через hello ссылки ниже:

* [Android 2.2 или более поздней версии](app-service-mobile-android-how-to-use-client-library.md)
* [iOS 3.0.0 или более поздней версии](app-service-mobile-ios-how-to-use-client-library.md)
* [.NET (Windows/Xamarin) 2.0.0 или более поздней версии](app-service-mobile-dotnet-how-to-use-client-library.md)
* [Apache Cordova 2.0 или более поздней версии](app-service-mobile-cordova-how-to-use-client-library.md)

Если приложение принимает использовать push-уведомлений, запишите hello инструкции конкретной регистрации для каждой платформы, как будут внесены некоторые изменения также.

При наличии hello новую версию клиента готов, попробуйте для проекта на обновленном сервере. После проверки того, что он работает, можно освободить новую версию toocustomers вашего приложения. Со временем Если ваши клиенты уже есть tooreceive вероятность эти обновления, можно удалить версии приложения для мобильных служб hello. В этот момент по окончании обновления tooan приложение службы мобильных приложений с помощью сервера последнюю мобильные приложения hello SDK.

<!-- URLs. -->

[Портал Azure]: https://portal.azure.com/
[Azure classic portal]: https://manage.windowsazure.com/
[Каковы мобильные приложения?]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[Mobile App Server SDK]: https://www.npmjs.com/package/azure-mobile-apps
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure Scheduler]: /en-us/documentation/services/scheduler/
[Web Job]: ../app-service-web/websites-webjobs-resources.md
[How toouse hello .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[служб приложений Ценовая]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[.NET server SDK overview]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[понятия проверки подлинности]: ../app-service/app-service-authentication-overview.md
[примеры использования проверки подлинности]: app-service-mobile-auth.md

[портала Azure]: https://portal.azure.com/
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
