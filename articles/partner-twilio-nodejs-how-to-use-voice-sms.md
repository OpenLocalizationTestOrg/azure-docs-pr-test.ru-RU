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
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a><span data-ttu-id="7546e-104">Использование Twilio для голосовой связи, VoIP и SMS сообщений в Azure</span><span class="sxs-lookup"><span data-stu-id="7546e-104">Using Twilio for Voice, VoIP, and SMS Messaging in Azure</span></span>
<span data-ttu-id="7546e-105">В этом руководстве показано, как приложения toobuild, взаимодействовать с Twilio и node.js в Azure.</span><span class="sxs-lookup"><span data-stu-id="7546e-105">This guide demonstrates how toobuild apps that communicate with Twilio and node.js on Azure.</span></span>

<a id="whatis"/>

## <a name="what-is-twilio"></a><span data-ttu-id="7546e-106">Что такое Twilio?</span><span class="sxs-lookup"><span data-stu-id="7546e-106">What is Twilio?</span></span>
<span data-ttu-id="7546e-107">Twilio — это платформа API, который облегчает разработчикам toomake и приема телефонных звонков, отправлять и получать текстовые сообщения и внедрение VoIP вызова на основе браузера и собственных мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="7546e-107">Twilio is an API platform that makes it easy for developers toomake and receive phone calls, send and receive text messages, and embed VoIP calling into browser-based and native mobile applications.</span></span> <span data-ttu-id="7546e-108">Сначала вкратце рассмотрим принцип работы.</span><span class="sxs-lookup"><span data-stu-id="7546e-108">Let's briefly go over how this works before diving in.</span></span>

### <a name="receiving-calls-and-text-messages"></a><span data-ttu-id="7546e-109">Прием вызовов и получение текстовых сообщений</span><span class="sxs-lookup"><span data-stu-id="7546e-109">Receiving Calls and Text Messages</span></span>
<span data-ttu-id="7546e-110">Twilio позволяет разработчикам слишком[приобрести программируемый телефонных номеров] [ purchase_phone] которого может быть используется tooboth отправлять и получать вызовы и текстовые сообщения.</span><span class="sxs-lookup"><span data-stu-id="7546e-110">Twilio allows developers too[purchase programmable phone numbers][purchase_phone] which can be used tooboth send and receive calls and text messages.</span></span> <span data-ttu-id="7546e-111">Получив Twilio число входящих звонков или текст, Twilio будет отправлять веб-приложения HTTP POST или GET запросом, запрашивающее инструкции на как toohandle hello звонок или текстовое.</span><span class="sxs-lookup"><span data-stu-id="7546e-111">When a Twilio number receives an inbound call or text, Twilio will send your web application an HTTP POST or GET request, asking you for instructions on how toohandle hello call or text.</span></span> <span data-ttu-id="7546e-112">Ваш сервер будет отвечать на HTTP-запроса tooTwilio с [TwiML][twiml], простой набор XML-теги, которые содержат инструкции toohandle звонок или текстовое.</span><span class="sxs-lookup"><span data-stu-id="7546e-112">Your server will respond tooTwilio's HTTP request with [TwiML][twiml], a simple set of XML tags that contain instructions on how toohandle a call or text.</span></span> <span data-ttu-id="7546e-113">Чуть позже мы увидим примеры TwiML.</span><span class="sxs-lookup"><span data-stu-id="7546e-113">We will see examples of TwiML in just a moment.</span></span>

### <a name="making-calls-and-sending-text-messages"></a><span data-ttu-id="7546e-114">Осуществление вызовов и отправка текстовых сообщений</span><span class="sxs-lookup"><span data-stu-id="7546e-114">Making Calls and Sending Text Messages</span></span>
<span data-ttu-id="7546e-115">Выполняя запросы HTTP toohello Twilio API веб-службы, разработчиков можно отправлять текстовые сообщения или инициировать исходящих телефонных звонков.</span><span class="sxs-lookup"><span data-stu-id="7546e-115">By making HTTP requests toohello Twilio web service API, developers can send text messages or initiate outbound phone calls.</span></span> <span data-ttu-id="7546e-116">Для исходящих вызовов developer Привет необходимо также указать URL-адрес, возвращающий TwiML инструкции по способ hello toohandle исходящего вызова после его подключения.</span><span class="sxs-lookup"><span data-stu-id="7546e-116">For outbound calls, hello developer must also specify a URL that returns TwiML instructions for how toohandle hello outbound call once it is connected.</span></span>

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a><span data-ttu-id="7546e-117">Внедрение возможностей VoIP в код пользовательского интерфейса (JavaScript, iOS и Android)</span><span class="sxs-lookup"><span data-stu-id="7546e-117">Embedding VoIP Capabilities in UI code (JavaScript, iOS, or Android)</span></span>
<span data-ttu-id="7546e-118">Twilio предоставляет клиентский пакет SDK, который может превратить в VoIP-телефон любой веб-браузер, приложение iOS или Android.</span><span class="sxs-lookup"><span data-stu-id="7546e-118">Twilio provides a client-side SDK which can turn any desktop web browser, iOS app, or Android app into a VoIP phone.</span></span> <span data-ttu-id="7546e-119">В этой статье рассматривается как toouse VoIP вызов в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="7546e-119">In this article, we will focus on how toouse VoIP calling in hello browser.</span></span> <span data-ttu-id="7546e-120">В дополнение toohello *Twilio JavaScript SDK* выполняется в браузере hello, серверного приложения (наше приложение node.js) должен быть используется tooissue «токен возможность» toohello клиента JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7546e-120">In addition toohello *Twilio JavaScript SDK* running in hello browser, a server-side application (our node.js application) must be used tooissue a "capability token" toohello JavaScript client.</span></span> <span data-ttu-id="7546e-121">Можно прочитать подробнее об использовании VoIP с node.js [в блоге разработчиков hello Twilio][voipnode].</span><span class="sxs-lookup"><span data-stu-id="7546e-121">You can read more about using VoIP with node.js [on hello Twilio dev blog][voipnode].</span></span>

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a><span data-ttu-id="7546e-122">Подпишитесь на Twilio (скидка Microsoft)</span><span class="sxs-lookup"><span data-stu-id="7546e-122">Sign Up For Twilio (Microsoft Discount)</span></span>
<span data-ttu-id="7546e-123">Перед использованием службы Twilio необходимо сначала [зарегистрироваться для получения учетной записи][signup].</span><span class="sxs-lookup"><span data-stu-id="7546e-123">Before using Twilio services, you must first [sign up for an account][signup].</span></span> <span data-ttu-id="7546e-124">Microsoft Azure клиенты получают особую скидку - [быть toosign убедиться, что здесь][signup]!</span><span class="sxs-lookup"><span data-stu-id="7546e-124">Microsoft Azure customers receive a special discount - [be sure toosign up here][signup]!</span></span>

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a><span data-ttu-id="7546e-125">Создание и развертывание веб-сайта node.js</span><span class="sxs-lookup"><span data-stu-id="7546e-125">Create and Deploy a node.js Azure Website</span></span>
<span data-ttu-id="7546e-126">Далее нужно будет toocreate node.js веб-сайта в Azure.</span><span class="sxs-lookup"><span data-stu-id="7546e-126">Next, you will need toocreate a node.js website running on Azure.</span></span> <span data-ttu-id="7546e-127">[Hello официальной документации для этого находится здесь][azure_new_site].</span><span class="sxs-lookup"><span data-stu-id="7546e-127">[hello official documentation for doing this is located here][azure_new_site].</span></span> <span data-ttu-id="7546e-128">На высоком уровне вы будете проводить hello следующее:</span><span class="sxs-lookup"><span data-stu-id="7546e-128">At a high level, you will be doing hello following:</span></span>

* <span data-ttu-id="7546e-129">Регистрация для получения учетной записи Azure в случае ее отсутствия</span><span class="sxs-lookup"><span data-stu-id="7546e-129">Signing up for an Azure account, if you don't have one already</span></span>
* <span data-ttu-id="7546e-130">С помощью toocreate консоли администрирования Azure hello нового веб-сайта</span><span class="sxs-lookup"><span data-stu-id="7546e-130">Using hello Azure admin console toocreate a new website</span></span>
* <span data-ttu-id="7546e-131">Добавление поддержки системы управления версиями (подразумевается, что используется git)</span><span class="sxs-lookup"><span data-stu-id="7546e-131">Adding source control support (we will assume you used git)</span></span>
* <span data-ttu-id="7546e-132">Создание файла `server.js` с простым веб-приложением node.js</span><span class="sxs-lookup"><span data-stu-id="7546e-132">Creating a file `server.js` with a simple node.js web application</span></span>
* <span data-ttu-id="7546e-133">Развертывание этого tooAzure простого приложения</span><span class="sxs-lookup"><span data-stu-id="7546e-133">Deploying this simple application tooAzure</span></span>

<a id="twiliomodule"/>

## <a name="configure-hello-twilio-module"></a><span data-ttu-id="7546e-134">Настройка модуля Twilio hello</span><span class="sxs-lookup"><span data-stu-id="7546e-134">Configure hello Twilio Module</span></span>
<span data-ttu-id="7546e-135">Далее мы начнем toowrite приложения простой node.js, что делает использование hello Twilio API.</span><span class="sxs-lookup"><span data-stu-id="7546e-135">Next, we will begin toowrite a simple node.js application which makes use of hello Twilio API.</span></span> <span data-ttu-id="7546e-136">Прежде чем начать, мы должны tooconfigure нашей учетные данные учетной записи Twilio.</span><span class="sxs-lookup"><span data-stu-id="7546e-136">Before we begin, we need tooconfigure our Twilio account credentials.</span></span>

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a><span data-ttu-id="7546e-137">Настройка учетных данных Twilio в системных переменных среды</span><span class="sxs-lookup"><span data-stu-id="7546e-137">Configuring Twilio Credentials in System Environment Variables</span></span>
<span data-ttu-id="7546e-138">В порядке toomake проверку подлинности запросов к серверной части Twilio hello нам нужна наши SID учетной записи и проверки подлинности маркера, какие функции в качестве hello имени пользователя и пароля, заданных для наших учетной записи Twilio.</span><span class="sxs-lookup"><span data-stu-id="7546e-138">In order toomake authenticated requests against hello Twilio back end, we need our account SID and auth token, which function as hello username and password set for our Twilio account.</span></span> <span data-ttu-id="7546e-139">Здравствуйте, наиболее безопасный способ tooconfigure, их для использования с модулем hello узла в Azure можно с помощью переменных среды, которые можно установить непосредственно в консоли администрирования Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7546e-139">hello most secure way tooconfigure these for use with hello node module in Azure is via system environment variables, which you can set directly in hello Azure admin console.</span></span>

<span data-ttu-id="7546e-140">Выберите веб-сайт node.js и щелкните ссылку «НАСТРОИТЬ» hello.</span><span class="sxs-lookup"><span data-stu-id="7546e-140">Select your node.js website, and click hello "CONFIGURE" link.</span></span>  <span data-ttu-id="7546e-141">Если немного прокрутить экран, появится область, где можно задать свойства конфигурации для приложения.</span><span class="sxs-lookup"><span data-stu-id="7546e-141">If you scroll down a bit, you will see an area where you can set configuration properties for your application.</span></span>  <span data-ttu-id="7546e-142">Введите учетные данные учетной записи Twilio ([найти на консоли Twilio][twilio_console]) как показано - убедитесь, что tooname их `TWILIO_ACCOUNT_SID` и `TWILIO_AUTH_TOKEN`соответственно:</span><span class="sxs-lookup"><span data-stu-id="7546e-142">Enter your Twilio account credentials ([found on your Twilio Console][twilio_console]) as shown - make sure tooname them `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN`, respectively:</span></span>

![Консоль администрирования Azure][azure-admin-console]

<span data-ttu-id="7546e-144">Настроив эти переменные, перезапустите приложение в консоли Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7546e-144">Once you have configured these variables, restart your application in hello Azure console.</span></span>

### <a name="declaring-hello-twilio-module-in-packagejson"></a><span data-ttu-id="7546e-145">Объявление модуля Twilio hello в package.json</span><span class="sxs-lookup"><span data-stu-id="7546e-145">Declaring hello Twilio module in package.json</span></span>
<span data-ttu-id="7546e-146">Теперь нам нужны toocreate package.json toomanage нашей зависимости модулей узла через [npm].</span><span class="sxs-lookup"><span data-stu-id="7546e-146">Next, we need toocreate a package.json toomanage our node module dependencies via [npm].</span></span> <span data-ttu-id="7546e-147">На hello же уровне как hello `server.js` файл, созданный в hello *Azure/node.js* учебник, создать файл с именем `package.json`.</span><span class="sxs-lookup"><span data-stu-id="7546e-147">At hello same level as hello `server.js` file you created in hello *Azure/node.js* tutorial, create a file named `package.json`.</span></span>  <span data-ttu-id="7546e-148">В этот файл поместите hello следующее:</span><span class="sxs-lookup"><span data-stu-id="7546e-148">Inside this file, place hello following:</span></span>

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

<span data-ttu-id="7546e-149">Этот код объявляет hello twilio модуль как зависимостей, а также hello популярных [Express веб-платформа] [ express] и шаблонизатор EJS hello.</span><span class="sxs-lookup"><span data-stu-id="7546e-149">This declares hello twilio module as a dependency, as well as hello popular [Express web framework][express] and hello EJS template engine.</span></span>  <span data-ttu-id="7546e-150">Итак, теперь все готово. Давайте напишем код!</span><span class="sxs-lookup"><span data-stu-id="7546e-150">Okay, now we're all set - let's write some code!</span></span>

<a id="makecall"/>

## <a name="make-an-outbound-call"></a><span data-ttu-id="7546e-151">Осуществление исходящего вызова</span><span class="sxs-lookup"><span data-stu-id="7546e-151">Make an Outbound Call</span></span>
<span data-ttu-id="7546e-152">Давайте создадим простая форма, которая будет поместить номер tooa вызова, которые мы выбираем.</span><span class="sxs-lookup"><span data-stu-id="7546e-152">Let's create a simple form that will place a call tooa number we choose.</span></span> <span data-ttu-id="7546e-153">Откройте `server.js`и введите следующий код hello.</span><span class="sxs-lookup"><span data-stu-id="7546e-153">Open up `server.js`, and enter hello following code.</span></span> <span data-ttu-id="7546e-154">Обратите внимание, где отображается надпись «CHANGE_ME» - помещены туда hello имя веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="7546e-154">Note where it says "CHANGE_ME" - put hello name of your azure website there:</span></span>

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

<span data-ttu-id="7546e-155">Создайте каталог с именем `views` — в этом каталоге создайте файл с именем `index.ejs` с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="7546e-155">Next, create a directory called `views` - inside this directory, create a file named `index.ejs` with hello following contents:</span></span>

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

<span data-ttu-id="7546e-156">Теперь развертывание tooAzure вашего веб-сайта и откройте дома.</span><span class="sxs-lookup"><span data-stu-id="7546e-156">Now, deploy your website tooAzure and open your home.</span></span> <span data-ttu-id="7546e-157">Необходимо будет tooenter ваш номер телефона в поле текста hello и получить вызов ваш номер Twilio!</span><span class="sxs-lookup"><span data-stu-id="7546e-157">You should be able tooenter your phone number in hello text field, and receive a call from your Twilio number!</span></span>

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a><span data-ttu-id="7546e-158">Отправка SMS-сообщения</span><span class="sxs-lookup"><span data-stu-id="7546e-158">Send an SMS Message</span></span>
<span data-ttu-id="7546e-159">Теперь можно перейти к настройке пользовательского интерфейса и форму toosend логику обработки текстового сообщения.</span><span class="sxs-lookup"><span data-stu-id="7546e-159">Now, let's set up a user interface and form handling logic toosend a text message.</span></span> <span data-ttu-id="7546e-160">Откройте `server.js`и добавьте следующий код после последнего вызова hello слишком hello`app.post`:</span><span class="sxs-lookup"><span data-stu-id="7546e-160">Open up `server.js`, and add hello following code after hello last call too`app.post`:</span></span>

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

<span data-ttu-id="7546e-161">В `views/index.ejs`, добавьте другую форму под hello toosubmit первый из них, номер и текст сообщения:</span><span class="sxs-lookup"><span data-stu-id="7546e-161">In `views/index.ejs`, add another form under hello first one toosubmit a number and a text message:</span></span>

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message toosend" name="message"/>
  <br/>
  <input type="submit" value="Send text toohello number above"/>
</form>
```

<span data-ttu-id="7546e-162">Повторное развертывание tooAzure вашего приложения, и можно будет toosubmit, форму и отправки текстового сообщения самостоятельно (или любого из друзей ближайший)!</span><span class="sxs-lookup"><span data-stu-id="7546e-162">Re-deploy your application tooAzure, and you should now be able toosubmit that form and send yourself (or any of your closest friends) a text message!</span></span>

<a id="nextsteps"/>

## <a name="next-steps"></a><span data-ttu-id="7546e-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7546e-163">Next Steps</span></span>
<span data-ttu-id="7546e-164">Вы изучили hello основные принципы использования node.js и Twilio toobuild приложений, которые обмениваются данными.</span><span class="sxs-lookup"><span data-stu-id="7546e-164">You have now learned hello basics of using node.js and Twilio toobuild apps that communicate.</span></span> <span data-ttu-id="7546e-165">Но эти примеры едва scratch поверхности hello возможности с помощью вызова Twilio и node.js.</span><span class="sxs-lookup"><span data-stu-id="7546e-165">But these examples barely scratch hello surface of what's possible with Twilio and node.js.</span></span> <span data-ttu-id="7546e-166">Дополнительные сведения об использовании Twilio с помощью node.js ознакомьтесь с hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="7546e-166">For more information using Twilio with node.js, check out hello following resources:</span></span>

* <span data-ttu-id="7546e-167">[Официальные документы по модулю][docs]</span><span class="sxs-lookup"><span data-stu-id="7546e-167">[Official module docs][docs]</span></span>
* <span data-ttu-id="7546e-168">[Учебник по использованию VoIP с приложениями node.js][voipnode]</span><span class="sxs-lookup"><span data-stu-id="7546e-168">[Tutorial on VoIP with node.js applications][voipnode]</span></span>
* <span data-ttu-id="7546e-169">[Votr — приложение SMS-голосования в режиме реального времени с node.js и CouchDB (три части)][votr]</span><span class="sxs-lookup"><span data-stu-id="7546e-169">[Votr - a real-time SMS voting application with node.js and CouchDB (three parts)][votr]</span></span>
* <span data-ttu-id="7546e-170">[Пара программирования в браузере hello с node.js][pair]</span><span class="sxs-lookup"><span data-stu-id="7546e-170">[Pair programming in hello browser with node.js][pair]</span></span>

<span data-ttu-id="7546e-171">Надеемся, вам понравится работать с node.js и Twilio в Azure!</span><span class="sxs-lookup"><span data-stu-id="7546e-171">We hope you love hacking node.js and Twilio on Azure!</span></span>

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
