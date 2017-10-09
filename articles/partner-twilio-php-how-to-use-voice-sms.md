---
title: "aaaHow tooUse Twilio для голоса и SMS (PHP) | Документы Microsoft"
description: "Узнайте, как toomake телефонного звонка и SMS отправки сообщений с hello Twilio API службы в Azure. Примеры кода написаны на PHP."
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 007f22e3-ac75-4868-8315-da000c2e0dd0
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 9354df8de694826a0ff7ea92620ec4d7e5c2fd70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-php"></a>Как tooUse Twilio для голосовых возможностей и SMS на PHP
В этом руководстве показано, как tooperform часто встречающиеся задачи программирования с hello Twilio API службы в Azure. Hello сценарии включают телефонных звонков и отправке сообщения службы коротких сообщений (SMS). Дополнительные сведения о Twilio и использования голоса и SMS в приложениях см. в разделе hello [дальнейшие действия](#NextSteps) раздела.

## <a id="WhatIs"></a>Что такое Twilio?
Twilio включении hello будущее делового общения, включение разработчики tooembed голос, VoIP и обмен сообщениями в приложения. Они виртуализация всех инфраструктуру в среде облачных, глобальные, предоставляя его через hello Twilio communications API платформы. Приложения, простой toobuild и масштабируемость. Оцените гибкость повременной оплаты, а также преимущества, связанные с надежностью облачных решений.

**Голосовой Twilio** позволяет toomake вашего приложения и приема телефонных звонков. **Twilio SMS** позволяет toosend вашего приложения и получать текстовые сообщения. **Клиента Twilio** позволяет toomake VoIP вызовы из любой телефон, планшет или браузера и поддерживает WebRTC.

## <a id="Pricing"></a>Цены и специальные предложения Twilio
Клиентам Azure доступно [специальное предложение](http://www.twilio.com/azure): кредит Twilio в размере 10 долл. США при обновлении учетной записи Twilio. Это кредит Twilio может быть применен tooany Twilio использования ($10 кредит эквивалентные toosending до 1 000 SMS-сообщений или получение копии too1000 входящих голосовых минут, в зависимости от расположения hello ваш телефонный номер и сообщений или вызовов назначения). Получите этот кредит Twilio и приступите к работе на странице [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).

Twilio представляет собой службу с повременной оплатой. Стартовые платежи отсутствуют, а учетную запись можно закрыть в любое время. Дополнительные сведения см. в статье [Цены на Twilio][twilio_pricing].

## <a id="Concepts"></a>Основные понятия
Hello Twilio API является API RESTful, который предоставляет функциональные возможности SMS и голосовой для приложений. Полный список клиентских библиотек API Twilio, которые доступны на разных языках, см. на [этой странице][twilio_libraries].

Ключевые аспекты hello Twilio API, Twilio глаголов и язык разметки Twilio (TwiML).

### <a id="Verbs"></a>Команды Twilio
Hello API использует Twilio команд; Например, hello  **&lt;Say&gt;**  команда предписывает Twilio tooaudibly доставить сообщение во время вызова.

Hello ниже приведен список команд, Twilio. Дополнительные сведения о hello других команд и возможностей через [документации язык разметки Twilio](http://www.twilio.com/docs/api/twiml).

* **&lt;Удаленный&gt;**: подключается phone tooanother hello вызывающего объекта.
* **&lt;Соберите&gt;**: собирает цифры, введенные на клавиатуре телефона hello.
* **&lt;Hangup&gt;**: окончание вызова.
* **&lt;Play&gt;**: воспроизведение звукового файла.
* **&lt;Pause&gt;**: бесшумное ожидание в течение указанного времени (в секундах).
* **&lt;Запись&gt;**: записи голоса hello вызывающего объекта и возвращает URL-адрес файла, содержащего запись hello.
* **&lt;Перенаправить&gt;**: передает управление вызова или SMS toohello TwiML на другой URL-адрес.
* **&lt;Отклонить&gt;**: отклоняет во входящих вызова tooyour Twilio номер без выставления счетов, вы
* **&lt;Предположим,&gt;**: toospeech преобразует текст, который выполняется при вызове функции.
* **&lt;Sms&gt;**: отправка SMS-сообщения.

### <a id="TwiML"></a>TwiML
TwiML — это набор инструкций, основанный на XML основании hello Twilio команд, которые сообщают Twilio того, как tooprocess звонок или SMS.

Например, следующие TwiML hello бы преобразование текста hello **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

Когда приложение вызывает hello Twilio API, один из параметров API hello, hello URL-адрес, который возвращает ответ TwiML hello. В целях разработки можно использовать предоставляемые системой Twilio URL-адреса hello tooprovide TwiML ответов, используемых приложениями. Может также содержать собственные ответы TwiML hello tooproduce URL-адресов и другой вариант — toouse hello **TwiMLResponse** объекта.

Дополнительные сведения о командах Twilio, их атрибутах и TwiML см. на странице [TwiML][twiml]. Дополнительные сведения о hello Twilio API см. в разделе [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Создание учетной записи Twilio
Когда вы будете готовы tooget учетной записи Twilio, зарегистрируйтесь на [повторите Twilio][try_twilio]. Вы можете начать с бесплатной учетной записи и обновить ее позднее.

При регистрации учетной записи Twilio, вы получите идентификатор учетной записи и маркер проверки подлинности. Как будет toomake необходимые вызовы Twilio API. tooprevent несанкционированный доступ к учетной записи tooyour, безопасность срок действия токена проверки подлинности. Идентификатор учетной записи и проверки подлинности маркера могут быть просмотрены в hello [странице учетной записи Twilio][twilio_account]в hello поля с меткой **ИД безопасности учетной записи** и **ТОКЕНА проверки Подлинности**соответственно.

## <a id="create_app"></a>Создание приложения PHP
Приложение PHP, которое использует службу hello Twilio и работает в Azure не отличается от любого другого приложения PHP, использующего службу hello Twilio. Хотя Twilio служб на основе REST и может вызываться из PHP несколькими способами, в этой статье основное внимание уделяется как toouse Twilio служб с [Twilio библиотеки для PHP с сайта GitHub][twilio_php]. Дополнительные сведения об использовании библиотеки hello Twilio для PHP см. в разделе [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].

Подробные инструкции для создания и развертывания приложения Twilio и PHP tooAzure можно найти по адресу [как tooMake Twilio с помощью телефонного звонка в приложения PHP в Azure][howto_phonecall_php].

## <a id="configure_app"></a>Настройка приложения tooUse Twilio библиотек
Можно настроить библиотеку приложения hello toouse Twilio для PHP двумя способами:

1. Загрузка библиотеки hello Twilio для PHP с сайта GitHub ([https://github.com/twilio/twilio-php][twilio_php]) и добавьте hello **служб** приложение tooyour каталога.
   
    -ИЛИ-
2. Установка библиотеки hello Twilio для PHP в качестве ГРУШИ пакета. Он может быть установлен с hello, следующие команды:
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

После установки библиотеки hello Twilio для PHP можно добавить **require_once** инструкции вверху hello вашей PHP файлы библиотеки hello tooreference:

        require_once 'Services/Twilio.php';

Дополнительные сведения см. в разделе [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].

## <a id="howto_make_call"></a>Практическое руководство. Осуществление исходящего вызова
Hello ниже показано, как исходящий toomake вызвать с помощью hello **Services_Twilio** класса. Этот код также использует предоставляемые системой Twilio сайта tooreturn hello ответ языка разметки Twilio (TwiML). Подставьте собственные значения hello **из** и **для** номера телефонов и убедитесь в правильности hello **из** телефонный номер для кода hello предыдущих toorunning учетной записи Twilio.

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";

    // hello number of hello phone initiating hello hello call.
    $from_number = "NNNNNNNNNNN";

    // hello number of hello phone receiving call.
    $to_number = "NNNNNNNNNNN";

    // Use hello Twilio-provided site for hello TwiML response.
    $url = "http://twimlets.com/message";

    // hello phone message text.
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    //Make hello call.
    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

Как уже упоминалось, этот код использует hello tooreturn Twilio техники сайта TwiML ответа. Можно использовать собственный узел tooprovide hello TwiML ответа; Дополнительные сведения см. в разделе [как tooProvide TwiML ответов от ваш собственный веб-сайт](#howto_provide_twiml_responses).

* **Примечание**: см. ошибки проверки сертификатов SSL tootroubleshoot [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation] 

## <a id="howto_send_sms"></a>Практическое руководство. Отправка SMS-сообщения
Hello ниже показано, как сообщение SMS с помощью toosend hello **Services_Twilio** класса. Hello **из** номер обеспечивается Twilio для пробной версии учетных записей toosend SMS-сообщений. Hello **для** номер должен быть проверен кода hello предыдущих toorunning учетной записи Twilio.

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";


    $from_number = "NNNNNNNNNNN"; // With trial account, texts can only be sent from your Twilio number.
    $to_number = "NNNNNNNNNNN";
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    // Send hello SMS message.
    try
    {
        $client->$client->account->messages->sendMessage($from_number, $to_number, $message);
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

## <a id="howto_provide_twiml_responses"></a>Практическое руководство. Предоставление ответов TwiML с собственного веб-сайта
Когда приложение начинает toohello вызова Twilio API, Twilio будет отправлено на tooa URL-адрес запроса, ожидался tooreturn TwiML ответ. Hello выше примере hello Twilio предоставленный URL-адрес [http://twimlets.com/message][twimlet_message_url]. (Хотя TwiML предназначен для использования с Twilio, можно просмотреть его hello в браузере. Например, щелкните [http://twimlets.com/message] [ twimlet_message_url] toosee пустой `<Response>` элемент; в качестве другого примера, нажмите кнопку [http://twimlets.com/message? Сообщения % 5B0 %5 D = Hello % 20World] [ twimlet_message_url_hello_world] toosee `<Response>` элемент, содержащий `<Say>` элемента.)

Вместо hello Twilio предоставленный URL-адрес, можно создать собственного веб-сайта, который возвращает HTTP-ответов. Можно создать узел hello на любом языке, который возвращает XML-ответов; в этом разделе предполагается, что вы будете использовать PHP toocreate hello TwiML.

Здравствуйте следующие результаты в виде страниц PHP в TwiML ответ, который говорит **Hello World** при вызове функции hello.

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

Как видно в приведенном выше примере hello hello TwiML ответа является просто XML-документа. Библиотека Twilio Hello для PHP содержит классы, которые создают TwiML для вас. пример Hello ниже создает эквивалентный ответа hello, как показано выше, но использует hello **службы\_Twilio\_Twiml** класс библиотеки hello Twilio для PHP:

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

Дополнительные сведения о TwiML см. по следующему адресу: [https://www.twilio.com/docs/api/twiml][twiml_reference]. 

При наличии на странице PHP, Настройка tooprovide TwiML ответов служит hello URL-адрес страницы PHP hello hello URL-адреса, переданные в hello `Services_Twilio->account->calls->create` метод. Например, если у вас есть веб-приложения с именем **MyTwiML** развернутой tooan Azure размещенной службы, а имя hello страницы приветствия PHP — **mytwiml.php**, URL-адрес может быть передан слишком hello **Services_ Twilio -> учетной записи вызовы "->" -> создать** как показано в следующий пример hello:

    require_once 'Services/Twilio.php';

    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";
    $from_number = "NNNNNNNNNNN";
    $to_number = "NNNNNNNNNNN";
    $url = "http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.php";

    // hello phone message text.
    $message = "Hello world.";

    $client = new Services_Twilio($sid, $token, "2010-04-01");

    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

Дополнительные сведения об использовании Twilio в Azure с PHP см. в разделе [как tooMake Twilio с помощью телефонного звонка в приложения PHP в Azure][howto_phonecall_php].

## <a id="AdditionalServices"></a>Руководство: использование дополнительных служб Twilio
В дополнение к этому toohello в этой статье примерах, Twilio предлагает веб-API, можно использовать дополнительные возможности Twilio tooleverage из приложения Azure. Дополнительные сведения см. в разделе hello [документации по Twilio API][twilio_api_documentation].

## <a id="NextSteps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello hello Twilio службы, выполните следующие дополнительные toolearn ссылки.

* [Рекомендации по безопасности Twilio][twilio_security_guidelines]
* [Практические руководства по Twilio и примеры кода][twilio_howtos]
* [Краткие учебники по Twilio][twilio_quickstarts] 
* [Twilio на GitHub][twilio_on_github]
* [Обращайтесь tooTwilio поддержки][twilio_support]

[twilio_php]: https://github.com/twilio/twilio-php
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-php/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-php/blob/master/README.md
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_api_service]: https://api.twilio.com
[howto_phonecall_php]: partner-twilio-php-make-phone-call.md
[twilio_voice_request]: https://www.twilio.com/docs/api/twiml/twilio_request
[twilio_sms_request]: https://www.twilio.com/docs/api/twiml/sms/twilio_request
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/user/account
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/api
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
