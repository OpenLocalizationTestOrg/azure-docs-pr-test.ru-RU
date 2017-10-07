---
title: "aaaCreate приложения Node.js разговора с Socket.IO в службе приложений Azure"
description: "В этом учебнике рассматривается использование Socket.io в веб-приложениях Node.js, размещенных в Azure."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c4c4af36-3ecf-4619-b586-ca90d53ce35b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 3bd7867ccc297dc0a21c7a00cc9db06358877f5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a>Создание приложения для разговоров на Node.js с использованием Socket.IO в службе приложений Azure
Socket.IO обеспечивает связь в режиме реального времени между сервером Node.js и клиентами с помощью WebSockets. Оно также поддерживает резервной tooother транспорты (например, длинные опроса), работающие с старых браузерах. Этот учебник пошаговыми руководствами для размещения приложения на основе Socket.IO разговора как веб-приложение Azure и показать, как tooscale hello приложения с помощью [кэш Azure Redis]. Дополнительные сведения о Socket.IO см. на веб-сайте <http://socket.io/>.

> [!NOTE]
> Hello процедуры в этой задаче применяются слишком[веб-приложений служб приложения]; для облачных служб. в разделе [построения приложения чат Node.js с Socket.IO на облачную службу Azure].
> 
> 

## <a name="download-hello-chat-example"></a>Загрузить пример hello чата
Для этого проекта, мы будем использовать пример hello разговора с hello [репозитории Socket.IO GitHub]. Выполните следующий пример hello toodownload действия hello и добавьте его toohello проекта, созданного ранее.

1. Загрузить [ZIP-файл или GZ архивные версии] hello Socket.IO проекта (версия 1.3.5 использовалась для этого документа)
2. Извлеките hello и архивные копии hello **примеры\\чата** tooa новый каталог. Например, в **\\node\\chat**.

## <a name="modify-appjs-and-install-modules"></a>Изменение app.js и установка модулей
1. Переименование hello **index.js** файла слишком**в файле app.js**. Это позволяет Azure toodetect, что это приложение Node.js.
2. Откройте hello **в файле app.js** файл в текстовом редакторе. Изменение hello строке, содержащей `var io = require('../..')(server);` как показано ниже:
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. Откройте hello **package.json** и добавьте toosocket.io ссылку в разделе файла `dependencies`, как показано ниже:
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. Из командной строки hello, изменить toohello  **\\узел\\чата** каталог и использовать npm tooinstall hello модулями, необходимыми этим приложением:
   
        npm install
   
    Hello модули будут установлены в подпапку **node_modules**.

## <a name="create-an-azure-web-app"></a>Создание веб-приложения Azure
Выполните эти шаги toocreate Azure веб-приложение, включить публикацию Git и затем включите поддержка WebSocket для веб-приложения hello.

> [!NOTE]
> toocomplete этого учебника необходима учетная запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Бесплатная пробная версия Azure</a>.
> 
> 

1. Установка hello Azure командной строки (CLI Azure) и подключение tooyour подписки Azure. В разделе [Установка и настройка hello Azure CLI](../cli-install-nodejs.md).
2. Если это ваш первый подготовку в репозитории в Azure, необходимо toocreate учетные данные для входа. Введите следующую команду hello hello Azure CLI:
   
        azure site deployment user set [username] [password]
3. Изменить toohello  **\\node\chat** каталога и используйте следующие hello команд toocreate новый Azure веб-приложения и локального репозитория Git. Эта команда также создает удаленный Git с именем azure.
   
        azure site create mysitename --git
   
    Замените mysitename уникальным именем созданного веб-приложения.
4. Зафиксировать hello существующие файлы toohello локального репозитория с помощью hello, следующие команды:
   
        git add .
        git commit -m "Initial commit"
5. Принудительная toohello веб-приложениях Azure hello файлы репозитория с hello следующую команду:
   
        git push azure master
   
    При появлении запроса введите свои учетные данные из шага 2. Вы получите сообщения о состоянии, как модули импортируются на сервере hello. После завершения этого процесса будет размещаться приложение hello в Azure веб-приложения.
   
   > [!NOTE]
   > Во время установки модуля могут появиться ошибки, "hello... импортированный проект не найден". Эти сообщения можно спокойно проигнорировать.
   > 
   > 
6. В Socket.IO используются сокеты WebSockets, которые по умолчанию не включены в Azure. tooenable веб-сокеты hello используйте следующую команду:
   
        azure site set -w
   
    Если будет предложено, введите имя hello hello веб-приложения.
   
   > [!NOTE]
   > Здравствуйте, «azure site set -w» работают только с версии 0.7.4 или более поздней версии из hello интерфейса командной строки Azure будет команды. Также можно включить с помощью hello поддержка WebSocket [портала Azure](https://portal.azure.com).
   > 
   > с помощью WebSockets tooenable hello портал Azure, щелкните веб-приложение hello из колонки веб-приложения hello, **все параметры** > **параметры приложения**. В разделе **Веб-сокеты** щелкните **Включить**. Нажмите кнопку **Сохранить**.
   > 
   > 
7. tooview hello веб-приложения на следующий hello Azure, используйте команду toolaunch веб-браузере и перейдите toohello размещенного веб-приложения:
   
        azure site browse

Теперь ваше приложение работает на платформе Azure и может передавать сообщения разговора между различными клиентами с использованием Socket.IO.

## <a name="scale-out"></a>Масштабирование
Socket.IO приложения можно расширить с помощью **адаптер** toodistribute сообщений и событий между несколькими экземплярами приложения. При наличии нескольких адаптеров, hello [socket.io redis] адаптер можно легко использовать с помощью функции hello кэша Redis для Azure.

> [!NOTE]
> Дополнительным требованием к масштабированию решений Socket.IO является поддержка прикрепленных сеансов. Прикрепленные сеансы включены для веб-приложений Azure по умолчанию через маршрутизацию запросов Azure. Дополнительные сведения см. в разделе [Сходство экземпляров на веб-сайтах Azure].
> 
> 

### <a name="create-a-redis-cache"></a>Создание кэша Redis
Выполните действия hello в [создание кэша в кэше Redis для Azure] toocreate нового кэша.

> [!NOTE]
> Сохранить hello **имя узла** и **первичный ключ** для кэша, как их потребуется в hello дальнейшие действия.
> 
> 

### <a name="add-hello-redis-and-socketio-redis-modules"></a>Добавление hello redis и модули socket.io redis
1. Из командной строки, измените toohello  **\\узел\\чата** hello каталог и использовать следующую команду.
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > Hello версии, указанные в этой команде являются версии hello, используемых при тестировании в этой статье.
   > 
   > 
2. Изменение hello **в файле app.js** файл tooadd hello следующие строки в том, сразу после`var io = require('socket.io')(server);`
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    Замените **redishostname** и **rediskey** с именем узла hello и ключ для кэша Redis.
   
    Будет создан публикации и подписки клиента toohello кэш Redis, созданный ранее. Клиенты Hello затем используются с tooconfigure адаптера hello кэш Redis hello toouse Socket.IO для передачи сообщений и событий между экземплярами приложения
   
   > [!NOTE]
   > При hello **socket.io redis** адаптер может напрямую взаимодействовать tooRedis, hello текущая версия не поддерживает hello проверки подлинности, необходимые для кэша Azure Redis. Поэтому hello начального подключения создается с помощью hello **redis** модуля, затем клиент hello передается toohello **socket.io redis** адаптера.
   > 
   > Хотя кэш Azure Redis поддерживает безопасные соединения через порт 6380, hello модули, используемые в этом примере не поддерживают безопасные соединения по состоянию на 7/14/2014. Hello выше код использует по умолчанию hello, незащищенного порта 6379.
   > 
   > 
3. Hello сохранить изменения **в файле app.js**

### <a name="commit-changes-and-redeploy"></a>Подтверждение изменений и повторное развертывание
Из командной строки в hello hello  **\\узел\\чата** каталогов, используйте следующие команды toocommit отличия hello и повторного развертывания приложения hello.

    git add .
    git commit -m "implementing scale out"
    git push azure master

После изменения hello отправлены toohello сервера, можно масштабировать веб-узла по нескольким экземплярам, используя следующую команду hello.

    azure site scale instances --instances #

Где  **#**  hello число экземпляров toocreate.

Tooyour веб-приложения можно подключиться из нескольких браузеров или компьютеры tooverify сообщений, отправленных правильно tooall клиентов.

## <a name="troubleshooting"></a>Устранение неполадок
### <a name="connection-limits"></a>Ограничения на подключения
Azure веб-приложений можно найти в несколько конфигураций, которые определяют веб-сайт доступен tooyour ресурсов hello. Сюда входят hello число разрешенных подключений WebSocket. Дополнительные сведения см. в разделе hello [цены приложения Web].

### <a name="messages-arent-being-sent-using-websockets"></a>Не отправляются сообщения через WebSockets
Если клиентскими браузерами сохранить возврата toolong опроса вместо WebSockets, возможно из-за одного из следующих hello.

* **Попробуйте ограничить hello транспорта toojust WebSockets**
  
    Socket.IO toouse WebSockets как обмена сообщениями транспортного hello, клиента и сервера hello должен поддерживать в WebSockets. Если один или hello другие — нет, Socket.IO согласует другого транспорта, такого как долго опрашивающего. список по умолчанию Hello транспортов, используемые Socket.IO ` websocket, htmlfile, xhr-polling, jsonp-polling`. Для принудительного использования tooonly WebSockets, добавив следующий код toohello hello **в файле app.js** файла после hello строке, содержащей `, nicknames = {};`.
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > Следует Заметьте, что старых браузерах, которые не поддерживают WebSockets не может tooconnect toohello сайта во время hello над кодом активной, как она ограничивает только tooWebSockets связи.
  > 
  > 
* **Использование SSL**
  
    WebSockets зависит от некоторых меньшее используется заголовки HTTP, такие как hello **обновление** заголовок. Некоторые промежуточные сетевые устройства, например прокси-серверы, могут удалять эти заголовки. tooavoid эту проблему, можно установить соединение WebSocket hello по протоколу SSL.
  
    Простой способ tooaccomplish tooconfigure Socket.IO это слишком`match origin protocol`. Это указывает, что запрос таким же, как hello, рассчитанные на HTTP или HTTPS для веб-страницы приветствия связи hello Socket.IO toosecure WebSockets. Если браузер использует toovisit HTTPS URL-адрес веб-сайта, последующие соединения WebSocket через Socket.IO будут защищаться по протоколу SSL.
  
    toomodify этот пример tooenable этой конфигурации, добавьте следующий код toohello hello **в файле app.js** файла после hello строке, содержащей `, nicknames = {};`.
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* **Проверка настроек web.config**
  
    Использовать веб-приложениях Azure, размещающие приложения Node.js hello **web.config** tooroute файл входящих запросов приложений Node.js toohello. WebSockets toofunction правильно с приложениями, Node.js, hello **web.config** должен содержать следующие записи hello.
  
        <webSocket enabled="false"/>
  
    Это приведет к отключению hello модуль WebSocket служб IIS, в котором включает собственную реализацию конфликты с Node.js определенных модулей WebSocket, такие как Socket.IO и WebSockets. Если эта строка отсутствует или задано слишком`true`, возможно, причина hello, транспорт WebSocket hello не работает для вашего приложения.
  
    Обычно приложения Node.js не включают файл **web.config** , поэтому веб-сайты Azure автоматически будут создавать его для приложений Node.js при их развертывании. Так как этот файл автоматически создается на сервере hello, необходимо использовать hello FTP или FTPS URL-адрес для вашего веб-сайта tooview этот файл. Найти hello FTP и FTPS URL-адреса для веб-узла в hello классический портал, выбрав веб-приложения и затем hello **мониторинга** ссылку. Hello URL-адреса отображаются в hello **быстрый обзор** раздела.
  
  > [!NOTE]
  > Hello **web.config** файл только создается веб-сайтов Azure, если приложение не предоставляет. При указании **web.config** файл в корне проекта приложения hello, он будет использоваться веб-приложения Azure.
  > 
  > 
  
    Если запись hello не указан или задано значение tooa `true`, следует создать **web.config** в корневом каталоге приложения Node.js hello и укажите значение `false`.  Для справки ниже hello является значением по умолчанию **web.config** для приложения, использующего **в файле app.js** в качестве точки входа hello.
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used toorun node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that hello server.js file is a node.js web app toobe handled by hello iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether hello incoming URL matches a physical file in hello /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped toohello node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using hello following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes toorestart hello server
                * node_env: will be propagated toonode as NODE_ENV environment variable
                * debuggingEnabled - controls whether hello built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    Если приложение использует точки входа, отличный от **в файле app.js**, необходимо заменить все вхождения **в файле app.js** с hello исправить точку входа. Например, заменить **app.js** на **server.js**.

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений], в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике вы узнали, как toocreate это чат приложение, размещенное в веб-приложение Azure. Это приложение также можно разместить в качестве облачной службы Azure. Пошаговые инструкции о том, как tooaccomplish, см. в разделе [построения приложения чат Node.js с Socket.IO на облачную службу Azure].

Дополнительные сведения см. также: hello [Центр разработчика Node.js].

## <a name="whats-changed"></a>Изменения
* Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure].

<!-- URL List -->

[кэш Azure Redis]: /documentation/services/redis-cache/
[веб-приложений служб приложения]: http://go.microsoft.com/fwlink/?LinkId=529714
[цены приложения Web]: http://go.microsoft.com/fwlink/?LinkId=511643
[построения приложения чат Node.js с Socket.IO на облачную службу Azure]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure hello Azure CLI]: ../cli-install-nodejs.md
[службе приложений Azure и ее влияние на существующие службы Azure]: http://go.microsoft.com/fwlink/?LinkId=529714
[Центр разработчика Node.js]: /develop/nodejs/
[повторите служб приложений]: https://azure.microsoft.com/try/app-service/
[Сходство экземпляров на веб-сайтах Azure]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[создание кэша в кэше Redis для Azure]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[socket.io redis]: https://github.com/socketio/socket.io-redis
[репозитории Socket.IO GitHub]: https://github.com/socketio/socket.io
[ZIP-файл или GZ архивные версии]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
