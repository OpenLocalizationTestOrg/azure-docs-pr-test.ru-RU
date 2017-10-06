---
title: "aaaHow tooUse Twilio для голоса и SMS (Java) | Документы Microsoft"
description: "Узнайте, как toomake телефонного звонка и SMS отправки сообщений с hello Twilio API службы в Azure. Примеры кода написаны на Java."
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: f3508965-5527-4255-9d51-5d5f926f4d43
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: a186e2c8e73ced928bd0dec348971034f10ba82c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-java"></a>Как tooUse Twilio для голосовых возможностей и SMS в Java
В этом руководстве показано, как tooperform часто встречающиеся задачи программирования с hello Twilio API службы в Azure. Hello сценарии включают телефонных звонков и отправке сообщения службы коротких сообщений (SMS). Дополнительные сведения о Twilio и использования голоса и SMS в приложениях см. в разделе hello [дальнейшие действия](#NextSteps) раздела.

## <a id="WhatIs"></a>Что такое Twilio?
Twilio — это API веб службы телефонии, которая позволяет использовать существующие языки веб и навыки toobuild голос, а приложений SMS. Twilio — это сторонняя служба (не компонент Azure и не продукт Майкрософт).

**Голосовой Twilio** позволяет toomake вашего приложения и приема телефонных звонков. **Twilio SMS** позволяет toomake вашего приложения и получения сообщений SMS. **Клиента Twilio** позволяет tooenable голосовой связи с использованием существующих соединений Интернета, в том числе мобильными приложениями.

## <a id="Pricing"></a>Цены и специальные предложения Twilio
Сведения о ценах на Twilio доступны на веб-сайте [цен на Twilio][twilio_pricing]. Клиентам Azure доступно [специальное предложение][special_offer]: бесплатный кредит на 1000 текстовых сообщений или 1000 минут входящих вызовов. toosign для использования это предложение или получить дополнительные сведения, посетите [http://ahoy.twilio.com/azure][special_offer].

## <a id="Concepts"></a>Основные понятия
Hello Twilio API является API RESTful, который предоставляет функциональные возможности SMS и голосовой для приложений. Полный список клиентских библиотек API Twilio, которые доступны на разных языках, см. на [этой странице][twilio_libraries].

Ключевые аспекты hello Twilio API, Twilio глаголов и язык разметки Twilio (TwiML).

### <a id="Verbs"></a>Команды Twilio
Hello API использует Twilio команд; Например, hello  **&lt;Say&gt;**  команда предписывает Twilio tooaudibly доставить сообщение во время вызова.

Hello ниже приведен список команд, Twilio.

* **&lt;Удаленный&gt;**: подключается phone tooanother hello вызывающего объекта.
* **&lt;Соберите&gt;**: собирает цифры, введенные на клавиатуре телефона hello.
* **&lt;Hangup&gt;**: окончание вызова.
* **&lt;Play&gt;**: воспроизведение звукового файла.
* **&lt;Очередь&gt;**: добавить очередь tooa hello вызывающих объектов.
* **&lt;Pause&gt;**: бесшумное ожидание в течение указанного времени (в секундах).
* **&lt;Запись&gt;**: записи голоса hello вызывающего объекта и возвращает URL-адрес файла, содержащего запись hello.
* **&lt;Перенаправить&gt;**: передает управление вызова или SMS toohello TwiML на другой URL-адрес.
* **&lt;Отклонить&gt;**: отклоняет во входящих вызова tooyour Twilio номер без выставления счетов за вас.
* **&lt;Предположим,&gt;**: toospeech преобразует текст, который выполняется при вызове функции.
* **&lt;Sms&gt;**: отправка SMS-сообщения.

### <a id="TwiML"></a>TwiML
TwiML — это набор инструкций, основанный на XML основании hello Twilio команд, которые сообщают Twilio того, как tooprocess звонок или SMS.

Например, следующие TwiML hello бы преобразование текста hello **Здравствуй, мир!** toospeech.

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

Когда приложение вызывает hello Twilio API, один из параметров API hello, hello URL-адрес, который возвращает ответ TwiML hello. В целях разработки можно использовать предоставляемые системой Twilio URL-адреса hello tooprovide TwiML ответов, используемых приложениями. Может также содержать собственные ответы TwiML hello tooproduce URL-адресов и другой вариант — toouse hello **TwiMLResponse** объекта.

Дополнительные сведения о командах Twilio, их атрибутах и TwiML см. на странице [TwiML][twiml]. Дополнительные сведения о hello Twilio API см. в разделе [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Создание учетной записи Twilio
Когда вы будете готовы tooget учетной записи Twilio, зарегистрируйтесь на [повторите Twilio][try_twilio]. Вы можете начать с бесплатной учетной записи и обновить ее позднее.

При регистрации учетной записи Twilio, вы получите идентификатор учетной записи и маркер проверки подлинности. Как будет toomake необходимые вызовы Twilio API. tooprevent несанкционированный доступ к учетной записи tooyour, безопасность срок действия токена проверки подлинности. Идентификатор учетной записи и проверки подлинности маркера могут быть просмотрены в hello [консоли Twilio][twilio_console]в hello поля с меткой **ИД безопасности учетной записи** и **ТОКЕНА проверки Подлинности**соответственно.

## <a id="create_app"></a>Создание приложения Java
1. Получить hello Twilio JAR и добавить его tooyour путь и сборку развертывания WAR сборок Java. В [https://github.com/twilio/twilio-java][twilio_java], можно загрузить исходных GitHub hello и создать собственные JAR или загрузить предварительно построенного JAR-ФАЙЛ (с или без зависимостей).
2. Убедитесь в JDK **cacerts** ключей содержит hello Equifax Secure сертификации сертификат с MD5 отпечатков пальцев 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello серийный номер имеет 35:DE:F4:CF и hello SHA1 отпечаток пальца является D2:32:09:AD:23:D3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A). Это hello сертификат центра сертификации (ЦС) для hello [https://api.twilio.com] [ twilio_api_service] службы, которая вызывается при использовании API Twilio. Сведения об обеспечении вашего JDK **cacerts** правильный сертификат ЦС hello содержит хранилище ключей см. в разделе [Добавление сертификата toohello хранилища сертификатов центра сертификации Java][add_ca_cert].

Подробные инструкции по использованию hello Twilio клиентская библиотека для Java можно найти по адресу [как tooMake Twilio с помощью телефонного звонка в приложении Java в Azure][howto_phonecall_java].

## <a id="configure_app"></a>Настройка приложения tooUse Twilio библиотек
В коде, можно добавить **импорта** инструкции вверху hello исходные файлы для hello Twilio пакеты или классы, вы хотите toouse в приложении.

Для исходных файлов Java:

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

Для исходных файлов Java Server Page (JSP):

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
В зависимости от того, какие пакеты Twilio или классы требуется toouse, ваш **импорта** инструкции может быть другим.

## <a id="howto_make_call"></a>Практическое руководство. Осуществление исходящего вызова
Hello ниже показано, как исходящий toomake вызвать с помощью hello **вызовите** класса. Этот код также использует предоставляемые системой Twilio сайта tooreturn hello ответ языка разметки Twilio (TwiML). Подставьте собственные значения hello **из** и **для** номера телефонов и убедитесь в правильности hello **из** телефонный номер для кода hello предыдущих toorunning учетной записи Twilio.

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    URI uri = new URI("http://twimlets.com/message" +
            "?Message%5B0%5D=Hello%20World%21");

    // Declare tooand From numbers
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

Дополнительные сведения о параметрах hello, передаваемых в toohello **Call.creator** метода, в разделе [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].

Как уже упоминалось, этот код использует hello tooreturn Twilio техники сайта TwiML ответа. Можно использовать собственный узел tooprovide hello TwiML ответа; Дополнительные сведения см. в разделе [как tooProvide TwiML ответов в приложении Java в Azure](#howto_provide_twiml_responses).

## <a id="howto_send_sms"></a>Практическое руководство. Отправка SMS-сообщения
Hello ниже показано, как сообщение SMS с помощью toosend hello **сообщение** класса. Hello **из** номер, **4155992671**, предоставляемые Twilio для пробной версии учетных записей toosend SMS-сообщений. Hello **для** номер должен быть проверен кода hello предыдущих toorunning учетной записи Twilio.

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Declare tooand From numbers and hello Body of hello SMS message
    PhoneNumber too= new PhoneNumber("+14159352345"); // Replace with a valid phone number for your account.
    PhoneNumber from = new PhoneNumber("+14158141829"); // Replace with a valid phone number for your account.
    String body = "Where's Wallace?";

    // Create a Message creator passing From, tooand Body values
    // then send hello SMS message by calling hello create() method
    Message sms = Message.creator(to, from, body).create();
```

Дополнительные сведения о параметрах hello, передаваемых в toohello **Message.creator** метода, в разделе [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].

## <a id="howto_provide_twiml_responses"></a>Практическое руководство. Предоставление ответов TwiML с собственного веб-сайта
Когда приложение инициирует toohello вызова Twilio API, например через hello **CallCreator.create** метода Twilio отправит ваш tooa URL-адрес запроса, ожидаемый tooreturn TwiML ответ. Hello выше примере hello Twilio предоставленный URL-адрес [http://twimlets.com/message][twimlet_message_url]. (Хотя TwiML предназначен для использования веб-службами, можно просмотреть hello TwiML в браузере. Например, щелкните [http://twimlets.com/message] [ twimlet_message_url] toosee пустой  **&lt;ответ&gt;**  элемента; еще один пример, нажмите кнопку [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21] [ twimlet_message_url_hello_world] toosee  **&lt;ответ&gt;**  элемент, содержащий  **&lt;Say &gt;**  элемента.)

Вместо hello Twilio предоставленный URL-адрес, можно создать собственного URL-адрес веб-сайта, возвращающий HTTP-ответов. Можно создать узел hello на любом языке, который возвращает HTTP-ответов; в этом разделе предполагается, что будет размещение hello URL-адрес на странице JSP.

Здравствуйте следующие результаты в виде страниц JSP в ответе TwiML потребовал **Здравствуй, мир!** При вызове функции hello.

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

следующие результаты в виде страниц JSP в ответе TwiML потребовал некоторый текст Hello имеет несколько приостанавливает свою работу и сообщает сведения о версии Twilio API hello и имя роли Azure hello.

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello from Azure!</Say>
        <Pause></Pause>
        <Say>hello Twilio API version is <%= request.getParameter("ApiVersion") %>.</Say>
        <Say>hello Azure role name is <%= System.getenv("RoleName") %>.</Say>
        <Pause></Pause>
        <Say>Good bye.</Say>
    </Response>
```

Hello **ApiVersion** параметр доступен в Twilio голосовых запросов (не SMS запросов). toosee hello доступного запроса параметров для голосового вызова Twilio и SMS запросов, в подразделе <https://www.twilio.com/docs/api/twiml/twilio_request> и <https://www.twilio.com/docs/api/twiml/sms/twilio_request >соответственно. Hello **RoleName** переменная среды доступна как часть развертывания Azure. (Если требуется tooadd пользовательские переменные, поэтому они могут быть выбраны из **System.getenv**, см. раздел переменные среды hello в [прочие параметры конфигурации роли] [misc_role_config_settings].)

После страницы JSP Настройка tooprovide TwiML ответов служит hello URL-адрес страницы JSP hello hello URL-адреса, переданные в hello **Call.creator** метод. Например, если у вас есть веб-приложение с именем tooan MyTwiML развертывания Azure размещенной службы и hello имя страницы JSP hello mytwiml.jsp, hello URL-адрес может быть передан слишком**Call.creator** как показано в следующих hello:

```java
    // Declare tooand From numbers and hello URL of your JSP page
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

Отвечать на запросы с TwiML может через hello **VoiceResponse** класс, который доступен в hello **com.twilio.twiml** пакета.

Дополнительные сведения об использовании Twilio в Azure с Java см. в разделе [как tooMake Twilio с помощью телефонного звонка в приложении Java в Azure][howto_phonecall_java].

## <a id="AdditionalServices"></a>Руководство: использование дополнительных служб Twilio
В дополнение к этому toohello в этой статье примерах, Twilio предлагает веб-API, можно использовать дополнительные возможности Twilio tooleverage из приложения Azure. Дополнительные сведения см. в разделе hello [документации по Twilio API][twilio_api_documentation].

## <a id="NextSteps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello hello Twilio службы, выполните следующие дополнительные toolearn ссылки.

* [Рекомендации по безопасности Twilio][twilio_security_guidelines]
* [Практические руководства по Twilio и примеры кода][twilio_howtos]
* [Краткие учебники по Twilio][twilio_quickstarts]
* [Twilio на GitHub][twilio_on_github]
* [Обращайтесь tooTwilio поддержки][twilio_support]

[twilio_java]: https://github.com/twilio/twilio-java
[twilio_api_service]: https://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[howto_phonecall_java]: partner-twilio-java-phone-call-example.md
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World%21
[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls
[twilio_rest_sending_sms]: http://www.twilio.com/docs/api/rest/sending-sms
[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/docs
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
