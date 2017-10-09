---
title: "aaaHow toomake телефонный звонок от Twilio (PHP) | Документы Microsoft"
description: "Узнайте, как toomake телефонного звонка и SMS отправки сообщений с hello Twilio API службы в Azure. Примеры, для приложения PHP."
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 44e35adc-be06-4700-beee-8c9e2c20c540
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: e6fecc345bf9ae787d14d533bd8d96b175c2453b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-php-application-on-azure"></a><span data-ttu-id="c3a59-104">Как tooMake Twilio с помощью телефонного звонка в приложения PHP в Azure</span><span class="sxs-lookup"><span data-stu-id="c3a59-104">How tooMake a Phone Call Using Twilio in a PHP Application on Azure</span></span>
<span data-ttu-id="c3a59-105">Hello пример вы использование Twilio toomake вызов с PHP веб-страницы, размещенной в Azure.</span><span class="sxs-lookup"><span data-stu-id="c3a59-105">hello following example shows you how you can use Twilio toomake a call from a PHP web page hosted in Azure.</span></span> <span data-ttu-id="c3a59-106">полученное приложение Hello пользователю будет предложено hello ввести значения телефонного вызова, как показано на следующий снимок экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="c3a59-106">hello resulting application will prompt hello user for phone call values, as shown in hello following screen shot.</span></span>

![Форма звонка Azure с использованием службы Twilio и PHP][twilio_php]

<span data-ttu-id="c3a59-108">Вам потребуется следующее hello toodo toouse hello кода в этом разделе:</span><span class="sxs-lookup"><span data-stu-id="c3a59-108">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="c3a59-109">Получите учетную запись Twilio и маркер проверки подлинности из [консоли Twilio][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="c3a59-109">Acquire a Twilio account and authentication token from your [Twilio Console][twilio_console].</span></span> <span data-ttu-id="c3a59-110">Оценка tooget к работе с Twilio, цены на [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="c3a59-110">tooget started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="c3a59-111">Вы можете зарегистрироваться для пробной учетной записи на сайте [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="c3a59-111">You can sign up for a trial account at [https://www.twilio.com/try-twilio][try_twilio].</span></span>
2. <span data-ttu-id="c3a59-112">Получить hello [Twilio библиотеки для PHP](https://github.com/twilio/twilio-php) или установить его как ГРУШИ пакета.</span><span class="sxs-lookup"><span data-stu-id="c3a59-112">Obtain hello [Twilio library for PHP](https://github.com/twilio/twilio-php) or install it as a PEAR package.</span></span> <span data-ttu-id="c3a59-113">Дополнительные сведения см. в разделе hello [файл readme](https://github.com/twilio/twilio-php/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="c3a59-113">For more information, see hello [readme file](https://github.com/twilio/twilio-php/blob/master/README.md).</span></span>
3. <span data-ttu-id="c3a59-114">Установите hello Azure SDK для PHP.</span><span class="sxs-lookup"><span data-stu-id="c3a59-114">Install hello Azure SDK for PHP.</span></span> <span data-ttu-id="c3a59-115">Обзор hello SDK и инструкции по его установке см. в разделе [Настройка hello Azure SDK для PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span><span class="sxs-lookup"><span data-stu-id="c3a59-115">For an overview of hello SDK and instructions on installing it, see [Set up hello Azure SDK for PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="c3a59-116">Создание веб-формы для выполнения звонка</span><span class="sxs-lookup"><span data-stu-id="c3a59-116">Create a web form for making a call</span></span>
<span data-ttu-id="c3a59-117">Привет, следуя HTML-коде показано использование toobuild веб-страницы (**callform.html**), извлекает данные пользователя для вызова:</span><span class="sxs-lookup"><span data-stu-id="c3a59-117">hello following HTML code shows how toobuild a web page (**callform.html**) that retrieves user data for making a call:</span></span>

```html
<!DOCTYPE html>
<html>
<head>
  <title>Automated call form</title>
</head>
<body>
  <h1>Automated Call Form</h1>
  <p>Fill in all fields and click <b>Make this call</b>.</p>
  <form action="makecall.php" method="post">
    <table>
      <tr>
        <td>To:</td>
        <td><input name="callTo" size="50" type="text" value=""></td>
      </tr>
      <tr>
        <td>From:</td>
        <td><input name="callFrom" size="50" type="text" value=""></td>
      </tr>
      <tr>
        <td>Call message:</td>
        <td><input name="callText" size="100" type="text" value="Hello. This is hello call text. Good bye."></td>
      </tr>
      <tr>
        <td colspan="2"><input type="submit" value="Make this call"></td>
      </tr>
    </table>
  </form><br>
</body>
</html>
```

## <a name="create-hello-code-toomake-hello-call"></a><span data-ttu-id="c3a59-118">Создание вызова hello toomake кода hello</span><span class="sxs-lookup"><span data-stu-id="c3a59-118">Create hello code toomake hello call</span></span>
<span data-ttu-id="c3a59-119">Здравствуйте, как следующий код показывает toobuild **makecall.php**, который вызывается при hello пользователь отправляет форму hello, отображаемого элементом **callform.html**.</span><span class="sxs-lookup"><span data-stu-id="c3a59-119">hello following code shows how toobuild **makecall.php**, which is called when hello user submits hello form displayed by **callform.html**.</span></span> <span data-ttu-id="c3a59-120">Приведенный ниже код Hello создает вызов приветственное сообщение и создает вызов hello.</span><span class="sxs-lookup"><span data-stu-id="c3a59-120">hello code shown below creates hello call message and generates hello call.</span></span> <span data-ttu-id="c3a59-121">Кроме того, следует убедиться, что toouse вашей учетной записи Twilio и проверки подлинности токена из hello [консоли Twilio] [ twilio_console] вместо значения заполнителей hello, назначенный слишком**$sid** и **$token** в следующем примере кода hello.</span><span class="sxs-lookup"><span data-stu-id="c3a59-121">Also, be sure toouse your Twilio account and authentication token from hello [Twilio Console][twilio_console] instead of hello placeholder values assigned too**$sid** and **$token** in hello code below.</span></span>

```html
<html>
<head><title>Making call...</title></head>
<body>
<p>Your call is being made.</p>

<?php
require_once 'path/to/vendor/autoload.php';

$sid   = "your_account_sid";
$token = "your_authentication_token";

$from_number = $_POST['callFrom']; // Calls must be made from a registered Twilio number.
$to_number   = $_POST['callTo'];
$message     = $_POST['callText'];

$client = new Twilio\Rest\Client($sid, $token);

$call = $client->calls->create(
            $to_number,
            $from_number,
            array('url' => http://twimlets.com/message?Message=' . urlencode($message))
        );

echo "Call status: " . $call->status . "<br />";
echo "URI resource: " . $call->uri . "<br />";
?>
</body>
</html>
```

<span data-ttu-id="c3a59-122">В дополнение к этому toomaking hello вызовов, **makecall.php** отображает некоторые метаданные вызова, как показано в приведенном ниже рисунке hello.</span><span class="sxs-lookup"><span data-stu-id="c3a59-122">In addition toomaking hello call, **makecall.php** displays some call metadata, as is shown in hello image below.</span></span> <span data-ttu-id="c3a59-123">Дополнительные сведения о метаданных звонка см. в разделе [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span><span class="sxs-lookup"><span data-stu-id="c3a59-123">For more information about call metadata, see [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span></span>

![Ответ на звонок Azure с использованием службы Twilio и PHP][twilio_php_response]

## <a name="run-hello-application"></a><span data-ttu-id="c3a59-125">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="c3a59-125">Run hello application</span></span>
<span data-ttu-id="c3a59-126">Hello следующим шагом является toodeploy tooAzure вашего приложения веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="c3a59-126">hello next step is toodeploy your application tooAzure Websites.</span></span> <span data-ttu-id="c3a59-127">Hello следующие статьи содержат hello сведения для создания веб-сайта и развертывание кода с помощью Git, FTP и WebMatrix (хотя и не все данные в каждой статье применимо):</span><span class="sxs-lookup"><span data-stu-id="c3a59-127">hello following articles contain hello information for creating a website and deploying your code with Git, FTP, or WebMatrix (though not all information in each article is relevant):</span></span>

* [<span data-ttu-id="c3a59-128">Создание веб-сайта PHP-MySQL в службе приложений Azure и развертывание с помощью Git</span><span class="sxs-lookup"><span data-stu-id="c3a59-128">Create a PHP-MySQL Azure Web Site and deploy using Git</span></span>](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [<span data-ttu-id="c3a59-129">Создание веб-сайта PHP-MySQL Azure и развертывание с помощью FTP</span><span class="sxs-lookup"><span data-stu-id="c3a59-129">Create a PHP-MySQL Azure Web Site and Deploy Using FTP</span></span>](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a><span data-ttu-id="c3a59-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c3a59-130">Next steps</span></span>
<span data-ttu-id="c3a59-131">Этот код был предоставлен tooshow вы основные функциональные возможности с использованием Twilio в PHP в Azure.</span><span class="sxs-lookup"><span data-stu-id="c3a59-131">This code was provided tooshow you basic functionality using Twilio in PHP on Azure.</span></span> <span data-ttu-id="c3a59-132">Перед развертыванием tooAzure в рабочей среде, вы можете tooadd дополнительные обработки ошибок или других компонентов.</span><span class="sxs-lookup"><span data-stu-id="c3a59-132">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="c3a59-133">Например:</span><span class="sxs-lookup"><span data-stu-id="c3a59-133">For example:</span></span>

* <span data-ttu-id="c3a59-134">Вместо использования веб-формы, может использовать хранилища Azure BLOB-объектов или базы данных SQL toostore телефонных номеров и вызовите текста.</span><span class="sxs-lookup"><span data-stu-id="c3a59-134">Instead of using a web form, you could use Azure storage blobs or SQL Database toostore phone numbers and call text.</span></span> <span data-ttu-id="c3a59-135">Дополнительные сведения об использовании BLOB-объектов Azure в PHP см. в разделе [Использование службы хранения BLOB-объектов Azure в PHP-приложениях][howto_blob_storage_php].</span><span class="sxs-lookup"><span data-stu-id="c3a59-135">For information about using Azure storage blobs in PHP, see [Using Azure Storage with PHP Applications][howto_blob_storage_php].</span></span> <span data-ttu-id="c3a59-136">Дополнительные сведения об использовании базы данных SQL в PHP см. в разделе [Использование базы данных SQL в PHP-приложениях][howto_sql_azure_php].</span><span class="sxs-lookup"><span data-stu-id="c3a59-136">For information about using SQL Database in PHP, see [Using SQL Database with PHP Applications][howto_sql_azure_php].</span></span>
* <span data-ttu-id="c3a59-137">Hello **makecall.php** код использует предоставляемые системой Twilio URL-адрес ([http://twimlets.com/message][twimlet_message_url]) tooprovide Twilio о том, как ответ языка разметки Twilio (TwiML) tooproceed вызовом hello.</span><span class="sxs-lookup"><span data-stu-id="c3a59-137">hello **makecall.php** code uses Twilio-provided URL ([http://twimlets.com/message][twimlet_message_url]) tooprovide a Twilio Markup Language (TwiML) response that informs Twilio how tooproceed with hello call.</span></span> <span data-ttu-id="c3a59-138">Например, может содержать hello TwiML, который возвращается `<Say>` команду, которая приводит к текст будет произноситься toohello получателя вызова.</span><span class="sxs-lookup"><span data-stu-id="c3a59-138">For example, hello TwiML that is returned can contain a `<Say>` verb that results in text being spoken toohello call recipient.</span></span> <span data-ttu-id="c3a59-139">Вместо hello Twilio предоставленный URL-адрес, можно строить собственные службы tooTwilio toorespond запроса; Дополнительные сведения см. в разделе [как tooUse Twilio для голосовых возможностей и SMS на PHP][howto_twilio_voice_sms_php].</span><span class="sxs-lookup"><span data-stu-id="c3a59-139">Instead of using hello Twilio-provided URL, you could build your own service toorespond tooTwilio's request; for more information, see [How tooUse Twilio for Voice and SMS Capabilities in PHP][howto_twilio_voice_sms_php].</span></span> <span data-ttu-id="c3a59-140">Дополнительные сведения о TwiML можно найти на сайте [http://www.twilio.com/docs/api/twiml][twiml]. Дополнительные сведения о `<Say>` и других командах Twilio можно найти на сайте [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="c3a59-140">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about `<Say>` and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="c3a59-141">Прочитать рекомендации по безопасности Twilio hello в [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="c3a59-141">Read hello Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="c3a59-142">Дополнительные сведения о Twilio см. на сайте [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="c3a59-142">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="c3a59-143">См. также</span><span class="sxs-lookup"><span data-stu-id="c3a59-143">See Also</span></span>
* [<span data-ttu-id="c3a59-144">Как tooUse Twilio для голосовых возможностей и SMS на PHP</span><span class="sxs-lookup"><span data-stu-id="c3a59-144">How tooUse Twilio for Voice and SMS Capabilities in PHP</span></span>](partner-twilio-php-how-to-use-voice-sms.md)

[twilio_console]: https://www.twilio.com/console
[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/docs/api
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified
[twimlet_message_url]: http://twimlets.com/message
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api_service]: http://api.twilio.com
[build_php_azure_app]: http://azurephp.interoperabilitybridges.com/articles/build-and-deploy-a-windows-azure-php-application
[howto_twilio_voice_sms_php]: partner-twilio-php-how-to-use-voice-sms.md
[howto_blob_storage_php]: http://azure.microsoft.com/documentation/articles/storage-php-how-to-use-blobs/
[howto_sql_azure_php]: http://azure.microsoft.com/documentation/articles/sql-database-php-how-to-use/
[twilio_call_properties]: https://www.twilio.com/docs/api/rest/call#instance-properties
[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_php]: ./media/partner-twilio-php-make-phone-call/WA_TwilioPHPCallForm.jpg
[twilio_php_response]: ./media/partner-twilio-php-make-phone-call/WA_TwilioPHPMakeCall.jpg
[website-git]: ./web-sites/web-sites-php-mysql-deploy-use-git.md
[website-ftp]: ./web-sites/web-sites-php-mysql-deploy-use-ftp.md
[twilio_php_github]: https://github.com/twilio/twilio-php
