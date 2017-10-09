---
title: "toowork aaaHow с сервера базы данных hello Node.js SDK для мобильных приложений | Документы Microsoft"
description: "Узнайте, как toowork с hello внутренний сервер Node.js SDK для мобильных приложений службы приложения Azure."
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
ms.openlocfilehash: 2b1ea5fda6f6ca422b92fe29ff8d16bf035018d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-nodejs-sdk"></a>Как toouse hello SDK Azure Mobile приложений Node.js
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

В этой статье содержатся подробные сведения и примеры, показывающие, как toowork с серверной Node.js в мобильных приложениях службы приложений Azure.

## <a name="Introduction"></a>Введение
Приложение службы мобильные приложения Azure предоставляет hello возможность tooadd, оптимизированные для мобильных устройств доступ к данным веб-API tooa веб-приложения.  пакет SDK для Azure приложений службы мобильного приложения Hello предоставляется для веб-приложений ASP.NET и Node.js.  Hello SDK предоставляет hello следующие операции:

* Табличные операции (чтение, вставка, обновление, удаление данных).
* Пользовательские операции API.

Операции обоих типов поддерживают проверку подлинности для всех поставщиков удостоверений, разрешенных службой приложений Azure, включая поставщиков удостоверений социальных сетей, таких как Facebook, Twitter, Google и Майкрософт, а также Azure Active Directory для корпоративной проверки подлинности.

Можно найти примеры для каждого варианта использования в hello [каталог образцов на GitHub].

## <a name="supported-platforms"></a>Поддерживаемые платформы
Hello пакет SDK для приложений мобильных узла Azure поддерживает hello выпуске LTS текущего узла и более поздних версий.  На момент написания статьи, последняя версия LTS hello — v4.5.0 узла.  Другие версии Node могут также работать, но они не поддерживаются.

Hello пакет SDK для приложений мобильных узла Azure поддерживает два драйвера базы данных - hello узел mssql драйвер поддерживает SQL Azure и локальные экземпляры SQL Server.  Hello sqlite3 драйвер поддерживает SQLite баз данных в одном экземпляре.

### <a name="howto-cmdline-basicapp"></a>Как: Создание основных Node.js серверной части с помощью hello командной строки
Каждая серверная часть на Node.js для мобильного приложения службы приложений Azure запускается как приложение ExpressJS.  ExpressJS — hello наиболее популярных веб-службы платформа для Node.js.  Вот как создать простое приложение [Express] :

1. В командной строке или окне PowerShell создайте каталог для проекта.

        mkdir basicapp
2. Запустите структуры пакета hello tooinitialize init npm.

        cd basicapp
        npm init

    команда init npm Hello запрашивает набор вопросов tooinitialize hello проекта.  См. в выходных данных примера hello:

    ![выходные данные init npm Hello][0]
3. Установите экспресс-варианте и мобильных приложений azure библиотеки hello из репозитория npm hello.

        npm install --save express azure-mobile-apps
4. Создайте в файле app.js файл tooimplement hello основных мобильных сервер.

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

Это приложение создает WebAPI, оптимизированные для мобильных устройств с одной конечной точке (`/tables/TodoItem`), предоставляющий доступ без проверки подлинности tooan базового хранилища данных SQL с помощью динамической схемы.  Этот пример подходит к следующим примерам использования клиентских библиотек.

* [Быстрый запуск клиента Android]
* [Быстрый запуск клиента Apache Cordova]
* [Быстрый запуск клиента iOS.]
* [Быстрый запуск клиента Магазина Windows Phone.]
* [Быстрый запуск клиента Xamarin.iOS.]
* [Быстрый запуск клиента Xamarin.Android.]
* [Быстрый запуск клиента Xamarin.Forms.]

Это основное приложение hello находятся кода hello [пример basicapp на GitHub].

### <a name="howto-vs2015-basicapp"></a>Создание серверной части на основе Node.js с помощью Visual Studio 2015
Visual Studio 2015 требуется расширение приложений Node.js toodevelop внутри hello интегрированной среды разработки.  toostart установки hello [Node.js Tools 1.1 для Visual Studio].  После установки hello Node.js Tools для Visual Studio создайте приложение 4.x Express:

1. Откройте hello **новый проект** диалоговое окно (из **файл** > **New** > **проект...** ).
2. Разверните **Шаблоны** > **JavaScript** > **Node.js**.
3. Выберите hello **Basic Azure Express 4 приложения Node.js**.
4. Введите имя проекта hello.  Нажмите кнопку *ОК*.

    ![Новый проект Visual Studio 2015][1]
5. Щелкните правой кнопкой мыши hello **npm** , а затем выберите **установить новые пакеты npm...** .
6. Может потребоваться toorefresh hello npm каталога на создание первого приложения Node.js.  При необходимости щелкните **Обновить** .
7. Введите *мобильных приложений azure* в поле поиска hello.  Нажмите кнопку hello **приложения azure mobile 2.0.0** пакета, а затем нажмите кнопку **установить пакет**.

    ![Установка новых пакетов npm][2]
8. Нажмите кнопку **Закрыть**
9. Откройте hello *в файле app.js* файл tooadd поддержка hello пакет SDK Azure Mobile приложений.  В нижней границы hello 6 at hello библиотеки требуют инструкции, добавить hello, следующий код:

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    Около строки 27 после hello других инструкций app.use добавьте hello, следующий код:

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    Сохраните файл hello.
10. Запуск локально приложения hello (приветствия на http://localhost:3000 обслуживается API), либо опубликовать tooAzure.

### <a name="create-node-backend-portal"></a>Как: создание серверной части Node.js с помощью портала Azure hello
Создании право серверной мобильное приложение hello [портал Azure]. Можно либо выполнить hello следующих шагов или создать клиентом и сервером вместе с следующие hello [создать мобильное приложение](app-service-mobile-ios-get-started.md) учебника. Hello учебник содержит упрощенную версию эти инструкции и лучше всего подходит для проверки концепции проектов.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

В hello *приступить к работе* колонки в разделе **создать таблицу API**, выберите **Node.js** как вашей **языка серверной**.
Установите флажок "hello" для "**я подтверждаю, что это перезапишет все содержимое сайта.**«, нажмите кнопку **таблицы TodoItem создания**.

### <a name="download-quickstart"></a>Как: загрузки hello Node.js серверной быстрый запуск проекта кода с помощью Git
При создании серверной части Node.js мобильное приложение с помощью портала hello **краткого** колонке Node.js проект создается для вас и развернутых tooyour сайта. Можно добавлять таблицы и API-интерфейсы и изменять файлы кода для серверной части Node.js hello в портал hello. Также можно использовать различные развертывания средства toodownload hello серверного проекта, можно добавить или изменить таблицы и API-интерфейсы, а затем повторно опубликовать проект hello. Дополнительные сведения см. в [руководстве по развертыванию службы приложений Azure]. Hello следующая процедура использует код проекта Git репозитория toodownload hello краткое руководство.

1. Установите Git, если его у вас еще нет. tooinstall необходимые шаги Hello Git различаться для разных операционных систем. Сведения о дистрибутивах для разных операционных систем и руководство по установке см. в разделе [Установка Git](http://git-scm.com/book/en/Getting-Started-Installing-Git).
2. Следуйте указаниям hello [Enable hello репозитория приложения службы приложений](../app-service-web/app-service-deploy-local-git.md#Step3) tooenable hello репозитории для сайта серверной части, создания заметки из hello развертывания пользователя и пароль.
3. В колонке hello для серверной части мобильного приложения, запишите hello **URL-адрес клона Git** параметр.
4. Выполнение hello `git clone` hello Git URL-адрес клона, ввода пароля при необходимости, как показано в следующем примере с помощью команды:

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. Обзор toolocal каталога, в предыдущих пример hello /todolist и обратите внимание, что файлы проекта были загружены. Найдите hello `todoitem.json` файла в hello `/tables` каталога.  Этот файл определяет разрешения для таблицы.  Также найти hello `todoitem.js` файл hello же каталог, который определяет, что операции CRUD скрипты для таблицы hello.
6. После внесения изменений tooproject файлы, выполните следующие команды tooadd, commit, а затем отправить изменения сайта toohello hello:

        $ git commit -m "updated hello table script"
        $ git push origin master

    При добавлении нового проекта toohello файлы, необходимо сначала tooexecute hello `git add .` команды.

Каждый раз, новый набор фиксаций помещается toohello сайта повторно публикуется Hello сайта.

### <a name="howto-publish-to-azure"></a>Как: публикация вашего tooAzure серверной Node.js
Microsoft Azure предоставляет много механизмов публикации Azure приложение службы мобильных приложений Node.js серверной части для hello службы Azure.  К ним относятся инструменты развертывания, интегрированные в Visual Studio, программы командной строки и средства непрерывного развертывания на основе системы управления версиями.  Дополнительные сведения по этой теме см. в [руководстве по развертыванию службы приложений Azure].

В отношении приложений на Node.js в службе приложений Azure существуют четкие рекомендации, с которыми вам следует ознакомиться перед развертыванием:

* Как слишком[укажите hello версия узла]
* Как слишком[используйте модули узла]

### <a name="howto-enable-homepage"></a>Практическое руководство. Включение домашней страницы для приложения
Многие приложения представляют собой сочетание веб- и мобильных приложений и hello ExpressJS framework позволяет toocombine двух аспектов.  Иногда тем не менее, вы можете реализовать tooonly мобильных интерфейса.  Это полезно tooprovide службы стартовой страницы tooensure hello приложений является запущен и работает.  Можно указать свою домашнюю страницу или включить временную.  tooenable временные домашней страницы, используйте следующие мобильные приложения Azure tooinstantiate hello:

    var mobile = azureMobileApps({ homePage: true });

Если требуется только этот параметр доступен при разработке локально, можно добавить этот параметр tooyour `azureMobile.js` файл.

## <a name="TableOperations"></a>Операции с таблицами
Hello Server Node.js мобильных приложений azure SDK предоставляет механизмы tooexpose данные таблиц, сохраненных в базе данных SQL Azure с WebAPI.  Пакетом предоставляются пять операций.

| Операция | Описание |
| --- | --- |
| GET /tables/*имя_таблицы* |Получить все записи в таблице hello |
| GET /tables/*имя_таблицы*/:id |Получить конкретную запись в таблице hello |
| POST /tables/*имя_таблицы* |Создайте запись в таблице hello |
| PATCH /tables/*имя_таблицы*/:id |Обновить запись в таблице hello |
| DELETE /tables/*имя_таблицы*/:id |Удаление записи в таблице hello |

Поддерживает этот WebAPI [OData] и расширяет возможности hello таблицы схемы toosupport [автономные данные синхронизации].

### <a name="howto-dynamicschema"></a>Определение таблиц с помощью динамической схемы
Перед использованием таблицы ее необходимо определить.  Таблицы можно определить с помощью статического схемы (где hello разработчик определяет столбцы hello в схеме hello) или динамически (где hello SDK управляет hello схему, основанную на входящие запросы). Кроме того разработчик hello можно настроить определенные аспекты hello WebAPI, добавив определение toohello кода Javascript.

Рекомендуется следует определить каждой таблицы в файл Javascript в каталоге hello таблиц, то использовать tooimport hello tables.import() метод таблиц.  Расширение basic приложение hello, hello в файле app.js файл будет настраиваться:

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define hello database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

Определите таблицу hello в. / tables/TodoItem.js:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for hello table goes here

    module.exports = table;

По умолчанию в таблицах используется динамическая схема.  tooturn отключение динамической схемы глобально, задайте параметр приложения hello **MS_DynamicSchema** toofalse внутри hello портал Azure.

Полный пример можно найти в hello [пример todo на GitHub].

### <a name="howto-staticschema"></a>Определение таблиц с помощью статической схемы
Можно явно определять tooexpose столбцы hello через hello WebAPI.  пакет SDK для Node.js мобильных приложений azure автоматически добавляет все дополнительные столбцы, необходимые для toohello список автономные данные синхронизации, который предоставляется Hello.  Например, в примерах клиентских приложений требуется таблица с двумя столбцами: text (строка) и завершения complete (логическое значение).  
Hello таблицы могут быть определены в hello таблицы определение файл JavaScript (расположен в каталоге hello таблиц) следующим образом:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

Если статически определить таблицы, затем необходимо также вызвать hello hello tables.initialize() метод toocreate схемы базы данных во время запуска.  Возвращает метод Hello tables.initialize() [Promise] , чтобы не обрабатывать запросы до инициализации базы данных hello, hello веб-службы.

### <a name="howto-sqlexpress-setup"></a>Использование SQL Express в качестве хранилища данных при разработке на локальном компьютере
Hello hello мобильных приложений Azure SDK узел AzureMobile приложений предоставляют три параметра для обслуживания данных стандартной hello: пакет SDK предоставляет три варианта для обслуживания данных стандартной hello:

* Используйте hello **памяти** примере хранилище драйверов tooprovide не постоянно
* Используйте hello **mssql** tooprovide драйвер хранилища данных SQL Express для разработки
* Используйте hello **mssql** драйвер tooprovide хранилище данных базы данных SQL Azure для рабочей среды

Hello Azure мобильных приложений Node.js SDK использует hello [пакет Node.js mssql] tooestablish и использовать SQL Express tooboth подключения и базы данных SQL.  Для использования этого пакета необходимо включить TCP-подключения в вашем экземпляре SQL Express.

> [!TIP]
> Hello памяти драйвер не предоставляет полный набор средств для тестирования.  При желании tootest локально серверной части, рекомендуется использование hello в хранилище данных SQL Express и hello mssql драйвера.
>
>

1. Загрузите и установите [Microsoft SQL Server 2014 Express].  Убедитесь, что вы можете установить средства выпуска SQL Server 2014 Express hello.  Если не требуется поддержка 64-разрядных явно hello 32-разрядная версия потребляет меньше памяти при запуске.
2. Запустите диспетчер конфигурации SQL Server 2014 hello.

   1. Разверните hello **сетевая конфигурация SQL Server** узел в дереве слева меню hello.
   2. Выберите **Протоколы для SQLEXPRESS**.
   3. Щелкните правой кнопкой мыши **TCP/IP** и выберите **Включить**.  Нажмите кнопку **ОК** в всплывающем диалоговом окне приветствия.
   4. Щелкните правой кнопкой мыши **TCP/IP** и выберите **Свойства**.
   5. Нажмите кнопку hello **IP-адреса** вкладки.
   6. Найти hello **IPAll** узла.  В hello **TCP-порт** введите **1433**.

          ![Configure SQL Express for TCP/IP][3]
   7. Нажмите кнопку **ОК**.  Нажмите кнопку **ОК** в всплывающем диалоговом окне приветствия.
   8. Нажмите кнопку **служб SQL Server** в левом дереве меню hello.
   9. Щелкните правой кнопкой мыши **SQL Server (SQLEXPRESS)** и выберите **Перезапустить**.
   10. Закройте диспетчер конфигурации SQL Server 2014 hello.
3. Запустите hello SQL Server 2014 Management Studio и подключитесь tooyour локальный экземпляр SQL Express

   1. Щелкните правой кнопкой мыши в обозревателе объектов hello экземпляра и выберите **свойства**
   2. Выберите hello **безопасности** страницы.
   3. Убедитесь, hello **режим SQL Server и проверка подлинности Windows** выбран
   4. Щелкните **ОК**

          ![Configure SQL Express Authentication][4]
   5. Разверните **безопасности** > **входа** в обозревателе объектов hello
   6. Щелкните правой кнопкой мыши пункт **Имена входа** и выберите **Создать имя входа**.
   7. Введите имя входа.  Выберите **Проверка подлинности SQL Server**.  Введите пароль, а затем введите hello пароль еще раз в **подтверждение пароля**.  Hello пароль должен отвечать требованиям к сложности пароля Windows.
   8. Щелкните **ОК**

          ![Add a new user tooSQL Express][5]
   9. Щелкните правой кнопкой мыши новое имя для входа и выберите **Свойства**
   10. Выберите hello **ролей сервера** страницы
   11. Проверьте hello поле Далее toohello **dbcreator** роли сервера
   12. Щелкните **ОК**
   13. Закройте hello SQL Server 2015 Management Studio

Убедитесь, что записи hello пользователя и пароль, которые вы выбрали.  Tooassign дополнительных ролей сервера или разрешений может потребоваться в зависимости от требований к определенной базе данных.

Hello Node.js приложение считывает hello **SQLCONNSTR_MS_TableConnectionString** hello строку подключения для этой базы данных в переменной среды.  Значение этой переменной можно задать непосредственно в своей среде.  Например можно использовать PowerShell tooset этой переменной среды:

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

Доступ к базе данных hello через подключение TCP/IP и укажите имя пользователя и пароль для подключения hello.

### <a name="howto-config-localdev"></a>Настройка проекта для локальной разработки
Мобильные приложения Azure считывает файл JavaScript с именем *azureMobile.js* из локальной файловой системе hello.  Не использовать этот файл tooconfigure hello пакет SDK Azure Mobile приложения в рабочей среде — не использовать параметры приложения в hello [портал Azure] вместо него.  Hello *azureMobile.js* файла следует экспортировать объект конфигурации.  Hello наиболее распространенные следующие значения.

* Параметры базы данных
* Параметры ведения журналов диагностики
* Дополнительные параметры CORS

Пример *azureMobile.js* файла реализации hello перед следующим параметры базы данных:

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

Мы рекомендуем добавить *azureMobile.js* tooyour *.gitignore* файла (или другие системы управления исходным кодом Пропуск файла) tooprevent паролей, хранящихся в облаке hello.  Всегда настраивайте параметры производства в параметрах приложения внутри hello [портал Azure].

### <a name="howto-appsettings"></a>Практическое руководство. Настройка параметров для мобильного приложения
Большинство параметров в hello *azureMobile.js* файла у него эквивалентные настройки приложения в hello [портал Azure].  Используйте следующий список tooconfigure hello приложения в параметрах приложения:

| Параметр приложения | *azureMobile.js*  | Описание | Допустимые значения |
|:--- |:--- |:--- |:--- |
| **MS_MobileAppName** |name |Имя Hello приложение hello |string |
| **MS_MobileLoggingLevel** |logging.level |Минимальный уровень toolog сообщений |error, warning, info, verbose, debug, silly |
| **MS_DebugMode** |debug |Включение или отключение режима отладки |true, false |
| **MS_TableSchema** |data.schema |Имя схемы по умолчанию для таблиц SQL |строка (значение по умолчанию: dbo) |
| **MS_DynamicSchema** |data.dynamicSchema |Включение или отключение режима отладки |true, false |
| **MS_DisableVersionHeader** |версия (набор tooundefined) |Отключает заголовок X-ZUMO-Server-Version hello |true, false |
| **MS_SkipVersionCheck** |skipversioncheck |Отключает проверку версии hello API клиента |true, false |

tooset Настройка приложения:

1. Войдите в toohello [портал Azure].
2. Выберите **все ресурсы** или **службы приложений** щелкните имя мобильного приложения hello.
3. по умолчанию открывается колонку параметров Hello. В противном случае щелкните **Параметры**.
4. Нажмите кнопку **параметры приложения** в меню "Разное" hello.
5. Прокрутите toohello раздел параметров приложения.
6. Если приложение уже существует, щелкните значение hello значение hello tooedit параметра приложения hello.
7. При настройке приложения не существует, введите параметр приложения hello в hello ключ и значение hello в окне значение hello.
8. После завершения нажмите кнопку **Сохранить**.

Для большинства параметров после внесения изменений потребуется перезапустить службу.

### <a name="howto-use-sqlazure"></a>Практическое руководство. Использование базы данных SQL для хранения данных в рабочей среде
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

Порядок использования базы данных SQL в качестве хранилища данных идентичен для всех типов приложений службы приложений Azure. Если вы еще не сделали этого, выполните эти шаги toocreate серверной мобильного приложения.

1. Войдите в toohello [портал Azure].
2. В hello верхнего левого угла окна hello, щелкнув hello **+ создать** кнопку > **Интернет + мобильные устройства** > **мобильное приложение**, затем введите имя для мобильного приложения серверной части.
3. В hello **группы ресурсов** введите hello точно такое же имя в качестве приложения.
4. выбран план службы приложений по умолчанию Hello.  Если вы хотите toochange плана служб приложений, это можно сделать, щелкнув hello план обслуживания приложений > **+ создать**.  Введите имя нового плана служб приложений hello и выберите подходящее расположение.  Щелкните hello Ценовая категория и выберите соответствующий ценовую категорию для службы hello. Выберите **просмотреть все** tooview более цены параметры, такие как **Free** и **Shared**.  После выбора ценовой категории, нажмите кнопку hello **выберите** кнопки.  В hello **план служб приложений** колонка, щелкните **ОК**.
5. Щелкните **Создать**. Подготовка серверной части мобильного приложения может занять несколько минут.  После подготовки внутреннего сервера мобильного приложения hello hello портал открывает hello **параметры** колонку для внутреннего мобильное приложение hello.

После создания внутреннего сервера мобильного приложения hello, вы можете tooeither подключение существующей серверной части SQL базы данных tooyour мобильное приложение или создание новой базы данных SQL.  В этом разделе мы создадим базу данных SQL.

> [!NOTE]
> Если уже имеется база данных в hello местоположения внутреннего сервера мобильного приложения hello, вместо этого можно **базы данных** и выберите эту базу данных. Использование базы данных в другом месте Hello не рекомендуется из-за большей задержкой.
>
>

1. В hello новую серверную часть мобильное приложение, нажмите кнопку **параметры** > **мобильное приложение** > **данные** > **+ добавить**.
2. В hello **добавить подключение к данным** колонка, щелкните **базы данных SQL — необходимые настройки** > **создать новую базу данных**.  Введите имя новой базы данных hello hello в hello **имя** поля.
3. Щелкните **Сервер**.  В hello **новый сервер** колонки, введите имя сервера, уникальный в hello **имя сервера** , а укажите подходящего **имя входа администратора сервера** и **пароля**.  Убедитесь, **tooaccess сервера разрешить службам azure** проверяется.  Нажмите кнопку **ОК**.

    ![Создание базы данных SQL Azure][6]
4. На hello **новую базу данных** колонка, щелкните **ОК**.
5. Включите hello **добавить подключение к данным** колонке выберите **строка подключения**, введите hello входа и пароль, предоставленный при создании базы данных hello.  При использовании существующей базы данных, укажите учетные данные входа hello для этой базы данных.  Выполнив вход, нажмите кнопку **ОК**.
6. Включите hello **добавить подключение к данным** колонке снова нажмите **ОК** базы данных toocreate hello.

<!--- END OF ALTERNATE INCLUDE -->

Создание hello базы данных может занять несколько минут.  Используйте hello **уведомления** области toomonitor hello ход выполнения развертывания hello.  Невыполнение пока будет успешно развернут hello базы данных.  После успешного развертывания для hello экземпляр базы данных SQL в серверной части мобильных параметры приложения создается строка подключения.  Вы увидите следующий параметр приложения в hello **параметры** > **параметры приложения** > **строки подключения**.

### <a name="howto-tables-auth"></a>Как: требуется проверка подлинности для доступа к tootables
При желании toouse проверки подлинности приложения службы с конечной точкой hello таблиц необходимо настроить проверки подлинности службы приложения в hello [портал Azure] первой.  Для hello руководство по конфигурации для поставщика удостоверений hello просмотрите дополнительные сведения о настройке проверки подлинности в службе приложений Azure, предполагается toouse:

* [Как tooconfigure проверки подлинности Azure Active Directory]
* [Как tooconfigure проверки подлинности Facebook]
* [Как tooconfigure проверки подлинности Google]
* [Как tooconfigure проверки подлинности Майкрософт]
* [Как tooconfigure проверки подлинности Twitter]

Каждая таблица имеет свойства access, можно использовать toocontrol доступа toohello таблице.  Следующий образец Hello приводится статически определенный таблица с требуется проверка подлинности.

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

Hello доступа свойство может принимать одно из трех значений

* *анонимные* указывает, что клиентское приложение hello tooread данные без проверки подлинности
* *Проверка подлинности* указывает, что клиентское приложение hello необходимо отправить токен проверки подлинности с запросом hello
* *disabled* указывает, что эта таблица сейчас отключена.

Если свойство доступа hello не определен, разрешен доступ без проверки подлинности.

### <a name="howto-tables-getidentity"></a>Практическое руководство. Использование утверждений аутентификации для таблиц
Можно настроить различные утверждения, запрашиваемые при настройке аутентификации.  Эти утверждения не обычно доступны через hello `context.user` объекта.  Тем не менее, они могут быть получены с помощью hello `context.user.getIdentity()` метод.  Hello `getIdentity()` метод возвращает объект Promise, который разрешает tooan объект.  Hello объекта шифруется с помощью метода проверки подлинности (facebook, google, twitter, microsoftaccount или aad).

Например при настройке проверки подлинности учетной записи Майкрософт и утверждения адреса электронной почты hello запроса, можно добавить запись toohello адреса электронной почты hello с hello следующие таблицы контроллера:

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
    * Limit hello context query toothose records with hello authenticated user email address
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds hello email address from hello claims toohello context item - used for
    * insert operations
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when hello client does a request
    // READ - only return records belonging toohello authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite hello userId based on hello authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong toohello authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong toohello authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

toosee какие утверждения будут доступны, используйте hello веб браузера tooview `/.auth/me` конечной точки веб-узла.

### <a name="howto-tables-disabled"></a>Как: отключение доступа toospecific табличные операции
В tooappearing сложения для таблицы hello свойство hello доступ может быть используется toocontrol отдельных операций.  Существует четыре операции:

* *чтение* hello RESTful получить операция на таблице hello
* *Вставить* операция hello RESTful POST на таблице hello
* *Обновить* hello RESTful PATCH операция на таблице hello
* *Удалить* — hello RESTful удалить операцию в таблице hello

Например можно назвать tooprovide таблицу без проверки подлинности только для чтения:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <a name="howto-tables-query"></a>Как: Настройка hello запрос, который используется вместе с операциями таблицы
Общим требованием для операций с таблицами — tooprovide ограниченное представление данных hello.  Например может предоставлять таблицы, помеченного hello с проверкой подлинности пользователя таким образом, можно только считывать или обновлять собственные записи.  После определения таблицы Hello предоставляет следующие функциональные возможности:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for hello table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for hello authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite hello userId with hello authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

Операции, которые подразумевают выполнение запроса, содержат свойство query, в которое можно добавить предложение where. свойство запроса Hello [QueryJS] объект, можно обработать используется tooconvert toosomething запроса OData, hello внутренних данных.  Карты можно использовать для простого равенства случаях (например, предшествующие, hello). Можно также добавить определенные предложения SQL.

    context.query.where('myfield eq ?', 'value');

### <a name="howto-tables-softdelete"></a>Практическое руководство. Настройка обратимого удаления для таблицы
При обратимом удалении записи фактически не удаляются.  Вместо этого он отмечает их как удаленные в базе данных hello, задав tootrue hello удалить столбец.  пакет SDK Azure Mobile приложения Hello автоматически удаляет обратимо удаленных записей из результатов только если hello пакет SDK для мобильных клиентов используются IncludeDeleted().  удалить таблицу для программной, tooconfigure задать hello `softDelete` свойство в файле определения таблицы hello:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

Следует создать механизм удаления записей посредством клиентского приложения, веб-заданий, функции Azure или настраиваемого API.

### <a name="howto-tables-seeding"></a>Практическое руководство. Заполнение базы данных данными
При создании нового приложения, вы можете tooseed таблицу с данными.  Это можно сделать в файле JavaScript для определения таблицы hello следующим образом:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
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

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

Заполнение данных выполняется только при создании таблицы hello в пакет SDK Azure Mobile приложения hello.  Если hello таблица уже существует в базе данных hello, данные не вставляется в таблицу hello.  Если включена динамическая схема, схема выводится из данных hello заполнена.

Рекомендуется явным образом вызвать hello `tables.initialize()` метод toocreate hello таблицы при запуске службы hello.

### <a name="Swagger"></a>Практическое руководство. Включение поддержки Swagger
Мобильные приложения службы приложений Azure предоставляются со встроенной поддержкой [Swagger] .  Поддержка Swagger tooenable сначала установить swagger hello пользовательского интерфейса как зависимость:

    npm install --save swagger-ui

После установки можно включить поддержку Swagger в конструкторе мобильных приложений Azure hello:

    var mobile = azureMobileApps({ swagger: true });

Вы, возможно, только tooenable требуется поддержка Swagger в выпусках разработки.  Это можно сделать с помощью параметра `NODE_ENV` приложения.

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

Hello конечной точки swagger расположен в http://*данный сайт*.azurewebsites.net/swagger.  Можно получить доступ к hello Swagger пользовательского интерфейса через hello `/swagger/ui` конечной точки.  При выборе проверки подлинности toorequire через приложение Swagger приводит к ошибке.  Для получения наилучших результатов выберите tooallow не прошедшие проверку подлинности запросы через в hello проверки подлинности службы приложения Azure и авторизации, затем параметров проверки подлинности с использованием hello `table.access` свойство.

Можно также добавить параметр tooyour hello Swagger `azureMobile.js` файл, если требуется только Swagger поддержку при разработке локально.

## <a name="a-namepushpush-notifications"></a><a name="push">Push-уведомления
Мобильные приложения интегрируется с концентраторами уведомлений Azure tooenable вы toomillions уведомлений push toosend целевых устройств для всех основных платформ. С помощью концентраторов уведомлений, могут отправлять push tooiOS уведомления, Android и Windows. см. Дополнительные сведения о все, что вам можно делать с toolearn концентраторы уведомлений [Обзор концентраторов уведомлений](../notification-hubs/notification-hubs-push-notification-overview.md).

### </a><a name="send-push"></a>Практическое руководство. Отправка push-уведомлений
Hello, следующий код показывает, как toouse hello принудительной объекта toosend вещания push устройства iOS tooregistered уведомления:

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do hello push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

Создавая принудительную регистрацию шаблона из клиента hello, вместо этого можно отправить toodevices сообщение шаблона принудительной на всех поддерживаемых платформах. Здравствуйте, как следующий код показывает toosend шаблонное уведомление:

    // Define hello template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do hello push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }


### <a name="push-user"></a>Как: tooan уведомления принудительной отправки, проверку подлинности пользователя, с помощью тегов
Когда прошедший проверку пользователь регистрируется для push-уведомлений, тег ИД пользователя автоматически добавляется toohello регистрации. Используя этот тег, вы можете отправлять push уведомления tooall устройства, зарегистрированные определенным пользователем. Hello следующий код возвращает идентификатор SID пользователя, выполняющего запрос hello hello и отправляет шаблон регистрации push-уведомлений tooevery устройства для этого пользователя.

    // Only do hello push if configured
    if (context.push) {
        // Send a notification toohello current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

При регистрации для работы с push-уведомлениями на клиенте, прошедшем проверку подлинности, убедитесь, что проверка подлинности завершена, и только после этого начинайте регистрацию.

## <a name="CustomAPI"></a>Настраиваемые API
### <a name="howto-customapi-basic"></a>Практическое руководство. Определение настраиваемого интерфейса API
Кроме toohello доступа к данным API через конечную точку /tables hello, мобильные приложения Azure можно обслуживают пользовательские API.  Пользовательские API определяются в аналогичные определения таблиц toohello образом и можно получить доступ ко всем hello же средства, включая проверку подлинности.

При желании toouse службы проверки подлинности в приложении пользовательский интерфейс API, необходимо настроить приложение проверки подлинности службы в hello [портал Azure] первой.  Для hello руководство по конфигурации для поставщика удостоверений hello просмотрите дополнительные сведения о настройке проверки подлинности в службе приложений Azure, предполагается toouse:

* [Как tooconfigure проверки подлинности Azure Active Directory]
* [Как tooconfigure проверки подлинности Facebook]
* [Как tooconfigure проверки подлинности Google]
* [Как tooconfigure проверки подлинности Майкрософт]
* [Как tooconfigure проверки подлинности Twitter]

Пользовательские API определяются во многом так же, как hello API таблиц hello.

1. Создайте каталог **api** .
2. Создайте файл JavaScript определения API в hello **api** каталога.
3. Используйте hello импорта метод tooimport hello **api** каталога.

Вот определение api прототип hello, на основе выборки basic приложения hello, использовавшегося ранее.

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

Рассмотрим пример API, который возвращает дату hello server, с помощью hello *Date.now()* метод.  Ниже приведен файл api/date.js hello.

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

Каждый параметр представляет один hello стандартных RESTful команд - GET, POST, PATCH или DELETE.  метод Hello — это стандарт [ExpressJS по промежуточного слоя] функцию, которая отправляет выходные данные, необходимые hello.

### <a name="howto-customapi-auth"></a>Как: требуется проверка подлинности для доступа к tooa настраиваемого API
Пакет SDK для приложений мобильных Azure реализует проверку подлинности в hello одинаково для конечной точки hello таблицы и пользовательские API.  Чтобы добавить API toohello проверки подлинности, разработанные в предыдущем разделе hello, добавьте **доступа** свойство:

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

Также можно определить проверку подлинности для конкретных операций:

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // hello GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

Hello тот же токен, используемый для конечной точки hello таблиц необходимо использовать для пользовательских API, требующей проверки подлинности.

### <a name="howto-customapi-auth"></a>Практическое руководство. Обработка передачи больших файлов
Пакет SDK для приложений мобильных Azure использует hello [синтаксического анализа текста по промежуточного слоя](https://github.com/expressjs/body-parser) tooaccept и расшифровать содержимое тела в заявку на участие.  Можно предварительно настроить передачи больших файлов tooaccept синтаксического анализа текста:

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

файл Hello — перед передачей в кодировке base-64.  Это увеличивает размер hello непосредственную отправку hello (и следовательно hello размер, до которого необходимо учитывать).

### <a name="howto-customapi-sql"></a>Практическое руководство. Выполнение пользовательских инструкций SQL
пакет SDK Azure Mobile приложения Hello разрешает доступ toohello всего контекста с помощью hello объекта запроса, позволяя tooexecute легко параметризованные поставщик данных toohello инструкций SQL:

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on tooa later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define hello query - anything that can be handled by hello mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute hello query.  hello context for Azure Mobile Apps is available through
            // request.azureMobile - hello data object contains hello configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <a name="Debugging"></a>Отладка, простые таблицы и простые интерфейсы API
### <a name="howto-diagnostic-logs"></a>Практическое руководство. Отладка, диагностика и устранение неполадок мобильных приложений Azure
Hello службе приложений Azure предоставляет несколько отладки и рекомендации по устранению неполадок для приложений Node.js.
См. следующие статьи tooget работы при устранении неполадок серверной части мобильных Node.js toohello:

* [Мониторинг службы приложений Azure]
* [Включение ведения журналов диагностики в службе приложений Azure]
* [Диагностика службы приложений Azure в Visual Studio]

Node.js приложения имеют доступ tooa широкий спектр средств журнала диагностики.  На внутреннем уровне hello использует пакет SDK для Azure мобильных приложений Node.js [Winston] для ведения журнала диагностики.  Включение режима отладки или установка hello автоматически включено ведение журнала **MS_DebugMode** tootrue параметр приложения в hello [портал Azure]. Созданные журналы отображаются в hello журналов диагностики на hello [портал Azure].

### <a name="in-portal-editing"></a><a name="work-easy-tables"></a>Как: работать с простой таблицы в hello портал Azure
Простой таблицы в портале hello позволяют создавать и работать с правой таблицы в портале hello. Можно изменить даже hello редактор службы приложения с помощью операций с таблицами.

Щелкнув **Простые таблицы** в параметрах сайта серверной части, вы сможете добавить, изменить или удалить таблицу. Также вы увидите данные в таблице hello.

![Работа с Easy Tables](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

Hello доступны следующие команды на панели команд hello для таблицы:

* **Изменение разрешений** — изменять hello разрешений для чтения, вставки, операций обновления и удаления в таблице hello.
  Параметрами являются tooallow анонимный доступ, проверка подлинности toorequire или toodisable обращаться к toohello операции.
* **Измените скрипт** -hello скрипт для таблицы hello откроется в редакторе службы приложения hello.
* **Управление схемой** - Добавление или удаление столбцов или изменении индекса таблицы hello.
* **Очистить таблицу** -усекает существующей таблицы при удалении всех строк данных с сохранением hello схемы без изменений.
* **Удалить строки** — удаляет отдельные строки данных.
* **Журналы потоковой передачи представление** -подключит вас toohello потоковой передачи службы журналов для веб-узла.

### <a name="work-easy-apis"></a>Как: работать с простой API-интерфейсы в hello портал Azure
Простой API-интерфейсы в портале hello позволяют создавать и работать с пользовательского API-интерфейсы права на портале hello. Можно редактировать скрипты API, с помощью редактора службы приложения hello.

Щелкнув **Простые API** в параметрах сайта серверной части, вы сможете добавить, изменить или удалить настраиваемую конечную точку API.

![Работа с Easy APIs](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

На портале hello можно изменить hello разрешения на доступ для выполнения данного действия HTTP, измените файл скрипта API hello в редакторе приложения службы или Просмотр журналов потоковой передачи hello.

### <a name="online-editor"></a>Как: изменение кода в редакторе службы приложения hello
Hello Azure портал позволяет редактировать файлы скриптов серверной Node.js в редакторе службы приложения hello без необходимости загружать hello проекта tooyour локального компьютера. файлы скриптов tooedit в интерактивном редакторе hello:

1. В колонке серверной части мобильного приложения щелкните **Все параметры**, затем **Простые таблицы** или **Простые API**, выберите таблицу или API и щелкните **Изменить сценарий**. файл скрипта Hello открывается в редакторе службы приложения hello.

    ![Редактор службы приложений](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. Сделать файл кода toohello изменения в интерактивном редакторе hello. Изменения сохраняются автоматически при вводе.

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
[Быстрый запуск клиента Android]: app-service-mobile-android-get-started.md
[Быстрый запуск клиента Apache Cordova]: app-service-mobile-cordova-get-started.md
[Быстрый запуск клиента iOS.]: app-service-mobile-ios-get-started.md
[Быстрый запуск клиента Xamarin.iOS.]: app-service-mobile-xamarin-ios-get-started.md
[Быстрый запуск клиента Xamarin.Android.]: app-service-mobile-xamarin-android-get-started.md
[Быстрый запуск клиента Xamarin.Forms.]: app-service-mobile-xamarin-forms-get-started.md
[Быстрый запуск клиента Магазина Windows Phone.]: app-service-mobile-windows-store-dotnet-get-started.md
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
[автономные данные синхронизации]: app-service-mobile-offline-data-sync.md
[Как tooconfigure проверки подлинности Azure Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Как tooconfigure проверки подлинности Facebook]: app-service-mobile-how-to-configure-facebook-authentication.md
[Как tooconfigure проверки подлинности Google]: app-service-mobile-how-to-configure-google-authentication.md
[Как tooconfigure проверки подлинности Майкрософт]: app-service-mobile-how-to-configure-microsoft-authentication.md
[Как tooconfigure проверки подлинности Twitter]: app-service-mobile-how-to-configure-twitter-authentication.md
[руководстве по развертыванию службы приложений Azure]: ../app-service-web/web-sites-deploy.md
[Мониторинг службы приложений Azure]: ../app-service-web/web-sites-monitor.md
[Включение ведения журналов диагностики в службе приложений Azure]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Диагностика службы приложений Azure в Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md
[укажите hello версия узла]: ../nodejs-specify-node-version-azure-apps.md
[используйте модули узла]: ../nodejs-use-node-modules-azure-apps.md
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
[Express]: http://expressjs.com/
[Swagger]: http://swagger.io/

[портал Azure]: https://portal.azure.com/
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[пример basicapp на GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[пример todo на GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[каталог образцов на GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 для Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[пакет Node.js mssql]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS по промежуточного слоя]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
