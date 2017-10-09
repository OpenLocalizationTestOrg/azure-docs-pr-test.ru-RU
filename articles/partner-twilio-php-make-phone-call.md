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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-php-application-on-azure"></a>Как tooMake Twilio с помощью телефонного звонка в приложения PHP в Azure
Hello пример вы использование Twilio toomake вызов с PHP веб-страницы, размещенной в Azure. полученное приложение Hello пользователю будет предложено hello ввести значения телефонного вызова, как показано на следующий снимок экрана приветствия.

![Форма звонка Azure с использованием службы Twilio и PHP][twilio_php]

Вам потребуется следующее hello toodo toouse hello кода в этом разделе:

1. Получите учетную запись Twilio и маркер проверки подлинности из [консоли Twilio][twilio_console]. Оценка tooget к работе с Twilio, цены на [http://www.twilio.com/pricing][twilio_pricing]. Вы можете зарегистрироваться для пробной учетной записи на сайте [https://www.twilio.com/try-twilio][try_twilio].
2. Получить hello [Twilio библиотеки для PHP](https://github.com/twilio/twilio-php) или установить его как ГРУШИ пакета. Дополнительные сведения см. в разделе hello [файл readme](https://github.com/twilio/twilio-php/blob/master/README.md).
3. Установите hello Azure SDK для PHP. Обзор hello SDK и инструкции по его установке см. в разделе [Настройка hello Azure SDK для PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)

## <a name="create-a-web-form-for-making-a-call"></a>Создание веб-формы для выполнения звонка
Привет, следуя HTML-коде показано использование toobuild веб-страницы (**callform.html**), извлекает данные пользователя для вызова:

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

## <a name="create-hello-code-toomake-hello-call"></a>Создание вызова hello toomake кода hello
Здравствуйте, как следующий код показывает toobuild **makecall.php**, который вызывается при hello пользователь отправляет форму hello, отображаемого элементом **callform.html**. Приведенный ниже код Hello создает вызов приветственное сообщение и создает вызов hello. Кроме того, следует убедиться, что toouse вашей учетной записи Twilio и проверки подлинности токена из hello [консоли Twilio] [ twilio_console] вместо значения заполнителей hello, назначенный слишком**$sid** и **$token** в следующем примере кода hello.

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

В дополнение к этому toomaking hello вызовов, **makecall.php** отображает некоторые метаданные вызова, как показано в приведенном ниже рисунке hello. Дополнительные сведения о метаданных звонка см. в разделе [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].

![Ответ на звонок Azure с использованием службы Twilio и PHP][twilio_php_response]

## <a name="run-hello-application"></a>Запустите приложение hello
Hello следующим шагом является toodeploy tooAzure вашего приложения веб-сайтов. Hello следующие статьи содержат hello сведения для создания веб-сайта и развертывание кода с помощью Git, FTP и WebMatrix (хотя и не все данные в каждой статье применимо):

* [Создание веб-сайта PHP-MySQL в службе приложений Azure и развертывание с помощью Git](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [Создание веб-сайта PHP-MySQL Azure и развертывание с помощью FTP](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a>Дальнейшие действия
Этот код был предоставлен tooshow вы основные функциональные возможности с использованием Twilio в PHP в Azure. Перед развертыванием tooAzure в рабочей среде, вы можете tooadd дополнительные обработки ошибок или других компонентов. Например:

* Вместо использования веб-формы, может использовать хранилища Azure BLOB-объектов или базы данных SQL toostore телефонных номеров и вызовите текста. Дополнительные сведения об использовании BLOB-объектов Azure в PHP см. в разделе [Использование службы хранения BLOB-объектов Azure в PHP-приложениях][howto_blob_storage_php]. Дополнительные сведения об использовании базы данных SQL в PHP см. в разделе [Использование базы данных SQL в PHP-приложениях][howto_sql_azure_php].
* Hello **makecall.php** код использует предоставляемые системой Twilio URL-адрес ([http://twimlets.com/message][twimlet_message_url]) tooprovide Twilio о том, как ответ языка разметки Twilio (TwiML) tooproceed вызовом hello. Например, может содержать hello TwiML, который возвращается `<Say>` команду, которая приводит к текст будет произноситься toohello получателя вызова. Вместо hello Twilio предоставленный URL-адрес, можно строить собственные службы tooTwilio toorespond запроса; Дополнительные сведения см. в разделе [как tooUse Twilio для голосовых возможностей и SMS на PHP][howto_twilio_voice_sms_php]. Дополнительные сведения о TwiML можно найти на сайте [http://www.twilio.com/docs/api/twiml][twiml]. Дополнительные сведения о `<Say>` и других командах Twilio можно найти на сайте [http://www.twilio.com/docs/api/twiml/say][twilio_say].
* Прочитать рекомендации по безопасности Twilio hello в [https://www.twilio.com/docs/security][twilio_docs_security].

Дополнительные сведения о Twilio см. на сайте [https://www.twilio.com/docs][twilio_docs].

## <a name="see-also"></a>См. также
* [Как tooUse Twilio для голосовых возможностей и SMS на PHP](partner-twilio-php-how-to-use-voice-sms.md)

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
