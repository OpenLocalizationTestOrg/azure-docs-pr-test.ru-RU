---
title: "aaaUsing Twilio голоса, VoIP и обмен сообщениями SMS в Azure"
description: "Узнайте, как toomake телефонного звонка и SMS отправки сообщений с hello Twilio API службы в Azure. Примеры кода написаны на Node.js."
services: 
documentationcenter: nodejs
author: devinrader
manager: wpickett
editor: 
ms.assetid: f558cbbd-13d2-416f-b9b1-33a99c426af9
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 11/25/2014
ms.author: wpickett
ms.openlocfilehash: 6c44d60e217fcdf51e69fd2a8197f979afbb507a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a>Использование Twilio для голосовой связи, VoIP и SMS сообщений в Azure
В этом руководстве показано, как приложения toobuild, взаимодействовать с Twilio и node.js в Azure.

<a id="whatis"/>

## <a name="what-is-twilio"></a>Что такое Twilio?
Twilio — это платформа API, который облегчает разработчикам toomake и приема телефонных звонков, отправлять и получать текстовые сообщения и внедрение VoIP вызова на основе браузера и собственных мобильных приложений. Сначала вкратце рассмотрим принцип работы.

### <a name="receiving-calls-and-text-messages"></a>Прием вызовов и получение текстовых сообщений
Twilio позволяет разработчикам слишком[приобрести программируемый телефонных номеров] [ purchase_phone] которого может быть используется tooboth отправлять и получать вызовы и текстовые сообщения. Получив Twilio число входящих звонков или текст, Twilio будет отправлять веб-приложения HTTP POST или GET запросом, запрашивающее инструкции на как toohandle hello звонок или текстовое. Ваш сервер будет отвечать на HTTP-запроса tooTwilio с [TwiML][twiml], простой набор XML-теги, которые содержат инструкции toohandle звонок или текстовое. Чуть позже мы увидим примеры TwiML.

### <a name="making-calls-and-sending-text-messages"></a>Осуществление вызовов и отправка текстовых сообщений
Выполняя запросы HTTP toohello Twilio API веб-службы, разработчиков можно отправлять текстовые сообщения или инициировать исходящих телефонных звонков. Для исходящих вызовов developer Привет необходимо также указать URL-адрес, возвращающий TwiML инструкции по способ hello toohandle исходящего вызова после его подключения.

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a>Внедрение возможностей VoIP в код пользовательского интерфейса (JavaScript, iOS и Android)
Twilio предоставляет клиентский пакет SDK, который может превратить в VoIP-телефон любой веб-браузер, приложение iOS или Android. В этой статье рассматривается как toouse VoIP вызов в браузере hello. В дополнение toohello *Twilio JavaScript SDK* выполняется в браузере hello, серверного приложения (наше приложение node.js) должен быть используется tooissue «токен возможность» toohello клиента JavaScript. Можно прочитать подробнее об использовании VoIP с node.js [в блоге разработчиков hello Twilio][voipnode].

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a>Подпишитесь на Twilio (скидка Microsoft)
Перед использованием службы Twilio необходимо сначала [зарегистрироваться для получения учетной записи][signup]. Microsoft Azure клиенты получают особую скидку - [быть toosign убедиться, что здесь][signup]!

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a>Создание и развертывание веб-сайта node.js
Далее нужно будет toocreate node.js веб-сайта в Azure. [Hello официальной документации для этого находится здесь][azure_new_site]. На высоком уровне вы будете проводить hello следующее:

* Регистрация для получения учетной записи Azure в случае ее отсутствия
* С помощью toocreate консоли администрирования Azure hello нового веб-сайта
* Добавление поддержки системы управления версиями (подразумевается, что используется git)
* Создание файла `server.js` с простым веб-приложением node.js
* Развертывание этого tooAzure простого приложения

<a id="twiliomodule"/>

## <a name="configure-hello-twilio-module"></a>Настройка модуля Twilio hello
Далее мы начнем toowrite приложения простой node.js, что делает использование hello Twilio API. Прежде чем начать, мы должны tooconfigure нашей учетные данные учетной записи Twilio.

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a>Настройка учетных данных Twilio в системных переменных среды
В порядке toomake проверку подлинности запросов к серверной части Twilio hello нам нужна наши SID учетной записи и проверки подлинности маркера, какие функции в качестве hello имени пользователя и пароля, заданных для наших учетной записи Twilio. Здравствуйте, наиболее безопасный способ tooconfigure, их для использования с модулем hello узла в Azure можно с помощью переменных среды, которые можно установить непосредственно в консоли администрирования Azure hello.

Выберите веб-сайт node.js и щелкните ссылку «НАСТРОИТЬ» hello.  Если немного прокрутить экран, появится область, где можно задать свойства конфигурации для приложения.  Введите учетные данные учетной записи Twilio ([найти на консоли Twilio][twilio_console]) как показано - убедитесь, что tooname их `TWILIO_ACCOUNT_SID` и `TWILIO_AUTH_TOKEN`соответственно:

![Консоль администрирования Azure][azure-admin-console]

Настроив эти переменные, перезапустите приложение в консоли Azure hello.

### <a name="declaring-hello-twilio-module-in-packagejson"></a>Объявление модуля Twilio hello в package.json
Теперь нам нужны toocreate package.json toomanage нашей зависимости модулей узла через [npm]. На hello же уровне как hello `server.js` файл, созданный в hello *Azure/node.js* учебник, создать файл с именем `package.json`.  В этот файл поместите hello следующее:

```json
{
  "name": "application-name",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node server"
  },
  "dependencies": {
    "body-parser": "^1.16.1",
    "ejs": "^2.5.5",
    "errorhandler": "^1.5.0",
    "express": "^4.14.1",
    "morgan": "^1.8.1",
    "twilio": "^2.11.1"
  }
}
```

Этот код объявляет hello twilio модуль как зависимостей, а также hello популярных [Express веб-платформа] [ express] и шаблонизатор EJS hello.  Итак, теперь все готово. Давайте напишем код!

<a id="makecall"/>

## <a name="make-an-outbound-call"></a>Осуществление исходящего вызова
Давайте создадим простая форма, которая будет поместить номер tooa вызова, которые мы выбираем. Откройте `server.js`и введите следующий код hello. Обратите внимание, где отображается надпись «CHANGE_ME» - помещены туда hello имя веб-сайте.

```javascript
// Module dependencies
const express = require('express');
const path = require('path');
const http = require('http');
const twilio = require('twilio');
const logger = require('morgan');
const bodyParser = require('body-parser');
const errorHandler = require('errorhandler');
const accountSid = process.env.TWILIO_ACCOUNT_SID;
const authToken = process.env.TWILIO_AUTH_TOKEN;
// Create Express web application
const app = express();

// Express configuration
app.set('port', process.env.PORT || 3000);
app.set('views', __dirname + '/views');
app.set('view engine', 'ejs');
app.use(logger('tiny'));
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())
app.use(express.static(path.join(__dirname, 'public')));

if (app.get('env') !== 'production') {
  app.use(errorHandler());
}

// Render an HTML user interface for hello application's home page
app.get('/', (request, response) => response.render('index'));

// Handle hello form POST tooplace a call
app.post('/call', (request, response) => {
  var client = twilio(accountSid, authToken);

  client.makeCall({
    // make a call toothis number
    to:request.body.number,

    // Change tooa Twilio number you bought - see:
    // https://www.twilio.com/console/phone-numbers/incoming
    from:'+15558675309',

    // A URL in our app which generates TwiML
    // Change "CHANGE_ME" tooyour app's name
    url:'https://CHANGE_ME.azurewebsites.net/outbound_call'
  }, () => {
      // Go back toohello home page
      response.redirect('/');
  });
});

// Generate TwiML toohandle an outbound call
app.post('/outbound_call', (request, response) => {
  var twiml = new twilio.TwimlResponse();

  // Say a message toohello call's receiver
  twiml.say('hello - thanks for checking out Twilio and Azure', {
      voice:'woman'
  });

  response.set('Content-Type', 'text/xml');
  response.send(twiml.toString());
});

// Start server
app.listen(app.get('port'), function(){
  console.log(`Express server listening on port ${app.get('port')}`);
});
```

Создайте каталог с именем `views` — в этом каталоге создайте файл с именем `index.ejs` с hello после содержимого:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Twilio Test</title>
  <style>
    input { height:20px; width:300px; font-size:18px; margin:5px; padding:5px; }
  </style>
</head>
<body>
  <h1>Twilio Test</h1>
  <form action="/call" method="POST">
      <input placeholder="Enter a phone number" name="number"/>
      <br/>
      <input type="submit" value="Call hello number above"/>
  </form>
</body>
</html>
```

Теперь развертывание tooAzure вашего веб-сайта и откройте дома. Необходимо будет tooenter ваш номер телефона в поле текста hello и получить вызов ваш номер Twilio!

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a>Отправка SMS-сообщения
Теперь можно перейти к настройке пользовательского интерфейса и форму toosend логику обработки текстового сообщения. Откройте `server.js`и добавьте следующий код после последнего вызова hello слишком hello`app.post`:

```javascript
app.post('/sms', (request, response) => {
  const client = twilio(accountSid, authToken);

  client.sendSms({
      // send a text toothis number
      to:request.body.number,

      // A Twilio number you bought - see:
      // https://www.twilio.com/console/phone-numbers/incoming
      from:'+15558675309',

      // hello body of hello text message
      body: request.body.message

  }, () => {
      // Go back toohello home page
      response.redirect('/');
  });
});
```

В `views/index.ejs`, добавьте другую форму под hello toosubmit первый из них, номер и текст сообщения:

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message toosend" name="message"/>
  <br/>
  <input type="submit" value="Send text toohello number above"/>
</form>
```

Повторное развертывание tooAzure вашего приложения, и можно будет toosubmit, форму и отправки текстового сообщения самостоятельно (или любого из друзей ближайший)!

<a id="nextsteps"/>

## <a name="next-steps"></a>Дальнейшие действия
Вы изучили hello основные принципы использования node.js и Twilio toobuild приложений, которые обмениваются данными. Но эти примеры едва scratch поверхности hello возможности с помощью вызова Twilio и node.js. Дополнительные сведения об использовании Twilio с помощью node.js ознакомьтесь с hello следующие ресурсы:

* [Официальные документы по модулю][docs]
* [Учебник по использованию VoIP с приложениями node.js][voipnode]
* [Votr — приложение SMS-голосования в режиме реального времени с node.js и CouchDB (три части)][votr]
* [Пара программирования в браузере hello с node.js][pair]

Надеемся, вам понравится работать с node.js и Twilio в Azure!

[purchase_phone]: https://www.twilio.com/console/phone-numbers/search
[twiml]: https://www.twilio.com/docs/api/twiml
[signup]: http://ahoy.twilio.com/azure
[azure_new_site]: app-service-web/app-service-web-get-started-nodejs.md
[twilio_console]: https://www.twilio.com/console
[npm]: http://npmjs.org
[express]: http://expressjs.com
[voipnode]: http://www.twilio.com/blog/2013/04/introduction-to-twilio-client-with-node-js.html
[docs]: http://twilio.github.io/twilio-node/
[votr]: http://www.twilio.com/blog/2012/09/building-a-real-time-sms-voting-app-part-1-node-js-couchdb.html
[pair]: http://www.twilio.com/blog/2013/06/pair-programming-in-the-browser-with-twilio.html
[azure-admin-console]: ./media/partner-twilio-nodejs-how-to-use-voice-sms/twilio_1.png
