---
title: "aaaHow tooUse Twilio для голоса и SMS (Python) | Документы Microsoft"
description: "Узнайте, как toomake телефонного звонка и SMS отправки сообщений с hello Twilio API службы в Azure. Примеры кода написаны на Python."
services: 
documentationcenter: python
author: devinrader
manager: twilio
editor: 
ms.assetid: 561bc75b-4ac4-40ba-bcba-48e901f27cc3
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: 1f16a107d95c94589b8d61a0971c5b62d639c571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-python"></a>Как tooUse Twilio для голосовых возможностей и SMS на Python
В этом руководстве показано, как tooperform часто встречающиеся задачи программирования с hello Twilio API службы в Azure. Hello сценарии включают телефонных звонков и отправке сообщения службы коротких сообщений (SMS). Дополнительные сведения о Twilio и использования голоса и SMS в приложениях см. в разделе hello [дальнейшие действия](#NextSteps) раздела.

## <a id="WhatIs"></a>Что такое Twilio?
Twilio включении hello будущее делового общения, включение разработчики tooembed голос, VoIP и обмен сообщениями в приложения. Они виртуализация всех инфраструктуру в среде облачных, глобальные, предоставляя его через hello Twilio communications API платформы. Приложения, простой toobuild и масштабируемость. Оцените гибкость повременной оплаты, а также преимущества, связанные с надежностью облачных решений.

**Голосовой Twilio** позволяет toomake вашего приложения и приема телефонных звонков.
**Twilio SMS** позволяет toosend вашего приложения и получать текстовые сообщения.
**Клиента Twilio** позволяет toomake VoIP вызовы из любой телефон, планшет или браузера и поддерживает WebRTC.

## <a id="Pricing"></a>Цены и специальные предложения Twilio
Клиентам Azure доступно [специальное предложение][special_offer]: кредит Twilio в размере 10 долл. США при обновлении учетной записи Twilio. Это кредит Twilio может быть применен tooany Twilio использования ($10 кредит эквивалентные toosending до 1 000 SMS-сообщений или получение копии too1000 входящих голосовых минут, в зависимости от расположения hello ваш телефонный номер и сообщений или вызовов назначения). Получите этот [кредит Twilio][special_offer] и приступите к работе.

Twilio представляет собой службу с повременной оплатой. Стартовые платежи отсутствуют, а учетную запись можно закрыть в любое время. Дополнительные сведения см. в статье [Цены на Twilio][twilio_pricing].

## <a id="Concepts"></a>Основные понятия
Hello Twilio API является API RESTful, который предоставляет функциональные возможности SMS и голосовой для приложений. Полный список клиентских библиотек API Twilio, которые доступны на разных языках, см. на [этой странице][twilio_libraries].

Ключевые аспекты hello Twilio API, Twilio глаголов и язык разметки Twilio (TwiML).

### <a id="Verbs"></a>Команды Twilio
Hello API использует Twilio команд; Например, hello  **&lt;Say&gt;**  команда предписывает Twilio tooaudibly доставить сообщение во время вызова.

Hello ниже приведен список команд, Twilio. Дополнительные сведения о hello других команд и возможностей через [документации язык разметки Twilio][twiml].

* **&lt;Удаленный&gt;**: подключается phone tooanother hello вызывающего объекта.
* **&lt;Соберите&gt;**: собирает цифры, введенные на клавиатуре телефона hello.
* **&lt;Hangup&gt;**: окончание вызова.
* **&lt;Pause&gt;**: бесшумное ожидание в течение указанного времени (в секундах).
* **&lt;Play&gt;**: воспроизведение звукового файла.
* **&lt;Очередь&gt;**: добавить очередь tooa hello вызывающих объектов.
* **&lt;Запись&gt;**: записи голоса hello hello вызывающего объекта и возвращает URL-адрес файла, содержащего запись hello.
* **&lt;Перенаправить&gt;**: передает управление вызова или SMS toohello TwiML на другой URL-адрес.
* **&lt;Отклонить&gt;**: отклоняет во входящих вызова tooyour Twilio номер без выставления счетов за вас.
* **&lt;Предположим,&gt;**: toospeech преобразует текст, который выполняется при вызове функции.
* **&lt;Sms&gt;**: отправка SMS-сообщения.

### <a id="TwiML"></a>TwiML
TwiML — это набор инструкций, основанный на XML основании hello Twilio команд, которые сообщают Twilio того, как tooprocess звонок или SMS.

Например, следующие TwiML hello бы преобразование текста hello **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

Когда приложение вызывает hello Twilio API, один из параметров API hello, hello URL-адрес, который возвращает ответ TwiML hello. В целях разработки можно использовать предоставляемые системой Twilio URL-адреса hello tooprovide TwiML ответов, используемых приложениями. Может также содержать собственные ответы TwiML hello tooproduce URL-адресов и другой вариант — toouse hello `TwiMLResponse` объекта.

Дополнительные сведения о командах Twilio, их атрибутах и TwiML см. на странице [TwiML][twiml]. Дополнительные сведения о hello Twilio API см. в разделе [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Создание учетной записи Twilio
Когда вы будете готовы tooget учетной записи Twilio, зарегистрируйтесь на [повторите Twilio][try_twilio]. Вы можете начать с бесплатной учетной записи и обновить ее позднее.

При регистрации учетной записи Twilio вы получите идентификатор безопасности учетной записи и маркер проверки подлинности. Как будет toomake необходимые вызовы Twilio API. tooprevent несанкционированный доступ к учетной записи tooyour, безопасность срок действия токена проверки подлинности. Ваш ИД безопасности учетной записи и токена проверки подлинности можно просмотреть в hello [консоли Twilio][twilio_console]в hello поля с меткой **ИД безопасности учетной записи** и **ТОКЕНА проверки Подлинности**соответственно.

## <a id="create_app"></a> Создание приложения Python
Приложения Python, которое использует службу hello Twilio и работает в Azure не отличается от любого другого приложения Python, использующего службу hello Twilio. Хотя Twilio служб на основе REST и может вызываться из Python несколькими способами, в этой статье основное внимание уделяется как toouse Twilio служб с [Twilio библиотеки для Python из GitHub][twilio_python]. Дополнительные сведения об использовании библиотеки hello Twilio для Python см. в разделе [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].

Во-первых, [установки новой виртуальной Машины Linux Azure] [azure_vm_setup] tooact в качестве узла для нового веб-приложения Python. После того, как hello виртуальная машина запущена, будет должны tooexpose приложения на открытый порт, как описано ниже.

### <a name="add-an-incoming-rule"></a>Добавление правила для входящего трафика
  1. Go [сетевую группу безопасности] [azure_nsg] toohello страницы.
  2. Выберите hello сетевая группа безопасности, соответствующий с вашей виртуальной машины.
  3. Добавьте **Правило для исходящего трафика** для **порта 80**. Убедиться, что tooallow быть входящих с любых адресов.

### <a name="set-hello-dns-name-label"></a>Набор hello метка DNS-имени
  1. Go toohello [hello открытый IP-адресов] [azure_ips] страницы.
  2. Выберите общедоступный IP-адрес, correspends с вашей виртуальной машиной hello.
  3. Набор hello **метка DNS-имени** в hello **конфигурации** раздела. В случае hello в этом примере это будет выглядеть примерно следующим образом *your метка доменного*. centralus.cloudapp.azure.com

Здравствуйте после можно tooconnect через SSH toohello виртуальной машины, можно установить веб-платформа, по вашему выбору (hello два наиболее хорошо известен в Python, [термосе](http://flask.pocoo.org/) и [Django](https://www.djangoproject.com)). Любое из них можно установить только выполнив hello `pip install` команды.

Имейте в виду, что настраивался hello виртуальной машины tooallow трафик только через порт 80. Поэтому следует убедиться, что toouse приложения hello tooconfigure этот порт.

## <a id="configure_app"></a>Настройка приложения tooUse Twilio библиотек
Библиотеки приложения hello toouse Twilio для Python можно настроить двумя способами:

* Установка библиотеки Twilio hello Python виде PIP-адрес пакета. Он может быть установлен с hello, следующие команды:
   
        $ pip install twilio

    -ИЛИ-

* Загрузка библиотеки hello Twilio для Python с сайта GitHub ([https://github.com/twilio/twilio-python][twilio_python]) и установите его следующим образом:

        $ python setup.py install

После установки библиотеки hello Twilio для Python, после этого можно `import` в Python файлов:

        import twilio

Дополнительные сведения см. в документе [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].

## <a id="howto_make_call"></a>Практическое руководство. Осуществление исходящего вызова
Следуя Hello показано, как вызвать toomake исходящего сообщения. Этот код также использует предоставляемые системой Twilio сайта tooreturn hello ответ языка разметки Twilio (TwiML). Подставьте собственные значения hello **from_number** и **to_number** номера телефонов и убедитесь, что вы убедились hello **from_number** телефонный номер для учетной записи Twilio Прежде чем выполнение кода hello.

    from urllib.parse import urlencode

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from_number = "NNNNNNNNNNN"

    # hello number of hello phone receiving call.
    to_number = "NNNNNNNNNNN"

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://twimlets.com/message?"

    # hello phone message text.
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url + urlencode({'Message': message}))
    print(call.sid)

Как уже упоминалось, этот код использует hello tooreturn Twilio техники сайта TwiML ответа. Можно использовать собственный узел tooprovide hello TwiML ответа; Дополнительные сведения см. в разделе [как tooProvide TwiML ответов от ваш собственный веб-сайт](#howto_provide_twiml_responses).

## <a id="howto_send_sms"></a>Практическое руководство. Отправка SMS-сообщения
Hello ниже показано, как сообщение SMS с помощью toosend hello `TwilioRestClient` класса. Hello **from_number** номер обеспечивается Twilio для пробной версии учетных записей toosend SMS-сообщений. Hello **to_number** номер для учетной записи Twilio должна проверяться перед запуском кода hello.

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    from_number = "NNNNNNNNNNN"  # With trial account, texts can only be sent from your Twilio number.
    to_number = "NNNNNNNNNNN"
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Send hello SMS message.
    message = client.messages.create(to=to_number,
                                     from_=from_number,
                                     body=message)

## <a id="howto_provide_twiml_responses"></a>Практическое руководство. Предоставление ответов TwiML с собственного веб-сайта
Когда приложение начинает toohello вызова Twilio API, Twilio будет отправлено на tooa URL-адрес запроса, ожидался tooreturn TwiML ответ. Hello выше примере hello Twilio предоставленный URL-адрес [http://twimlets.com/message][twimlet_message_url]. (Хотя TwiML предназначается для использования службой Twilio, его можно также просмотреть в браузере. Например, щелкните [http://twimlets.com/message] [ twimlet_message_url] toosee пустой `<Response>` элемент; в качестве другого примера, нажмите кнопку [http://twimlets.com/message? Сообщения % 5B0 %5 D = Hello % 20World] [ twimlet_message_url_hello_world] toosee `<Response>` элемент, содержащий `<Say>` элемента.)

Вместо hello Twilio предоставленный URL-адрес, можно создать собственного веб-сайта, который возвращает HTTP-ответов. Можно создать узел hello на любом языке, который возвращает XML-ответов; в этом разделе предполагается, что вы используете Python toocreate hello TwiML.

Hello следующие примеры будет выводить TwiML ответ, который говорит **Hello World** при вызове функции hello.

С помощью Flask:

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

С помощью Django:

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

Как видно в приведенном выше примере hello hello TwiML ответа является просто XML-документа. Библиотека Twilio Hello для Python содержит классы, которые создают TwiML для вас. Hello приведенном ниже примере создает эквивалентный ответа hello, как показано выше, но использует hello `twiml` модуль для Python hello Twilio библиотеки:

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

Дополнительные сведения о TwiML см. по следующему адресу: [https://www.twilio.com/docs/api/twiml][twiml_reference].

После настройки tooprovide TwiML ответов приложения Python, служит hello URL-адрес приложения hello hello URL-адреса, переданные в hello `client.calls.create` метод. Например, если у вас есть веб-приложения с именем **MyTwiML** развернутой tooan Azure размещенной службы, вы можете использовать его URL-адрес как веб-перехватчика, как показано в следующий пример hello:

    from twilio.rest import TwilioRestClient

    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"
    from_number = "NNNNNNNNNNN"
    to_number = "NNNNNNNNNNN"
    url = "http://your-domain-label.centralus.cloudapp.azure.com/MyTwiML/"

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url)
    print(call.sid)

## <a id="AdditionalServices"></a>Руководство: использование дополнительных служб Twilio
В дополнение к этому toohello в этой статье примерах, Twilio предлагает веб-API, можно использовать дополнительные возможности Twilio tooleverage из приложения Azure. Дополнительные сведения см. в разделе hello [документации по Twilio API][twilio_api].

## <a id="NextSteps"></a>Дальнейшие действия
Теперь, когда вы изучили основы hello hello Twilio службы, выполните следующие дополнительные toolearn ссылки.

* [Рекомендации по безопасности Twilio][twilio_security_guidelines]
* [Практические руководства по Twilio и примеры кода][twilio_howtos]
* [Краткие учебники по Twilio][twilio_quickstarts]
* [Twilio на GitHub][twilio_on_github]
* [Обращайтесь tooTwilio поддержки][twilio_support]

[special_offer]: http://ahoy.twilio.com/azure
[twilio_python]: https://github.com/twilio/twilio-python
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-python/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-python/blob/master/README.md

[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
[twilio_pricing]: http://www.twilio.com/pricing

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
