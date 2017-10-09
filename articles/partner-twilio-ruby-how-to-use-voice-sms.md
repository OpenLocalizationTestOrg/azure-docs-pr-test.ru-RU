---
title: "aaaHow tooUse Twilio для голоса и SMS (Ruby) | Документы Microsoft"
description: "Узнайте, как toomake телефонного звонка и SMS отправки сообщений с hello Twilio API службы в Azure. Примеры кода написаны на Ruby."
services: 
documentationcenter: ruby
author: devinrader
manager: twilio
editor: 
ms.assetid: 60e512f6-fa47-47c0-aedc-f19bb72a1158
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 11/25/2014
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: aca5ccb4663ff03c9c1f39c848469415f06dfb45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-ruby"></a>Как tooUse Twilio для голосовых возможностей и SMS в Ruby
В этом руководстве показано, как tooperform часто встречающиеся задачи программирования с hello Twilio API службы в Azure. Hello сценарии включают телефонных звонков и отправке сообщения службы коротких сообщений (SMS). Дополнительные сведения о Twilio и использования голоса и SMS в приложениях см. в разделе hello [дальнейшие действия](#NextSteps) раздела.

## <a id="WhatIs"></a>Что такое Twilio?
Twilio — это API веб службы телефонии, которая позволяет использовать существующие языки веб и навыки toobuild голос, а приложений SMS. Twilio — это сторонняя служба (не компонент Azure и не продукт Майкрософт).

**Голосовой Twilio** позволяет toomake вашего приложения и приема телефонных звонков. **Twilio SMS** позволяет toomake вашего приложения и получения сообщений SMS. **Клиента Twilio** позволяет tooenable голосовой связи с использованием существующих соединений Интернета, в том числе мобильными приложениями.

## <a id="Pricing"></a>Цены и специальные предложения Twilio
Сведения о ценах на Twilio доступны на веб-сайте [цен на Twilio][twilio_pricing]. Клиентам Azure доступно [специальное предложение][special_offer]: бесплатный кредит на 1000 текстовых сообщений или 1000 минут входящих вызовов. toosign для использования это предложение или получить дополнительные сведения, посетите [http://ahoy.twilio.com/azure][special_offer].  

## <a id="Concepts"></a>Основные понятия
Hello Twilio API является API RESTful, который предоставляет функциональные возможности SMS и голосовой для приложений. Полный список клиентских библиотек API Twilio, которые доступны на разных языках, см. на [этой странице][twilio_libraries].

### <a id="TwiML"></a>TwiML
TwiML — это набор инструкций, основанный на XML, чтобы сообщить Twilio как tooprocess звонок или SMS.

Например, следующие TwiML hello бы преобразование текста hello **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

Во всех документах TwiML элемент `<Response>` является корневым. После этого используйте команды Twilio toodefine hello поведение приложения.

### <a id="Verbs"></a>Команды TwiML
Twilio команды — это XML-теги, которые сообщают Twilio, что слишком**сделать**. Например, hello  **&lt;Say&gt;**  команда предписывает Twilio tooaudibly доставить сообщение во время вызова. 

Hello ниже приведен список команд, Twilio.

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

Дополнительные сведения о командах Twilio, их атрибутах и TwiML см. на странице [TwiML][twiml]. Дополнительные сведения о hello Twilio API см. в разделе [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Создание учетной записи Twilio
Когда вы будете готовы tooget учетной записи Twilio, зарегистрируйтесь на [повторите Twilio][try_twilio]. Вы можете начать с бесплатной учетной записи и обновить ее позднее.

После регистрации учетной записи Twilio вы получите бесплатный номер телефона для вашего приложения. Вы также получите идентификатор безопасности учетной записи и маркер проверки подлинности. Как будет toomake необходимые вызовы Twilio API. tooprevent несанкционированный доступ к учетной записи tooyour, безопасность срок действия токена проверки подлинности. Ваш ИД безопасности учетной записи и маркер проверки подлинности можно просмотреть в hello [странице учетной записи Twilio][twilio_account]в hello поля с меткой **ИД безопасности учетной записи** и **ТОКЕНА проверки Подлинности** , соответственно.

### <a id="VerifyPhoneNumbers"></a>Проверка телефонных номеров
В дополнение toohello номер выделил Twilio также можно проверить номера управления (т. е. Ваш мобильный телефон или домашней номер телефона) для использования в приложениях. 

Сведения о том, как tooverify номер телефона, в разделе [управление номера][verify_phone].

## <a id="create_app"></a>Создание приложения Ruby
Ruby приложение, которое использует службу hello Twilio и работает в Azure не отличается от любого другого Ruby приложения, использующего службу hello Twilio. Хотя Twilio службы являются категории RESTful и может вызываться из Ruby несколькими способами, в этой статье основное внимание уделяется как toouse Twilio служб с [Twilio вспомогательная библиотека для Ruby][twilio_ruby].

Во-первых, [установки новой виртуальной Машины Linux Azure] [ azure_vm_setup] tooact как узел нового Ruby веб-приложения. Игнорировать hello шагов, затрагивающих hello создания приложения направляющие, просто hello настройки виртуальной Машины. Обязательно создайте конечную точку с внешним портом 80 и внутренним портом 5000.

В примерах hello ниже, мы будем использовать [Sinatra][sinatra], это очень простой веб-платформа для Ruby. Но определенно можно использовать вспомогательную библиотеку hello Twilio для Ruby с любой другой web платформой, включая Ruby на направляющие.

Войдите на новую виртуальную машину по протоколу SSH и создайте каталог для нового приложения. В этом каталоге создайте файл с именем hello Gemfile и скопируйте следующий код в него:

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

Hello в командной строке запустите `bundle install`. Будут установлены зависимости hello выше. Затем создайте файл с именем `web.rb`. Это будет, где находятся hello кода для веб-приложения. Вставьте следующий код в него hello:

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

На этом этапе следует может hello запустите команду hello `ruby web.rb -p 5000`. Она настроит небольшой веб-сервер с портом 5000. Приложение может toobrowse toothis должно быть в браузере, перейдя по адресу hello URL-адрес настройки для ВМ Azure. После можно получить доступ к веб-приложения в браузере hello, теперь вы готовы toostart построение приложения Twilio.

## <a id="configure_app"></a>Настройка приложения tooUse Twilio
Можно настроить библиотеку Twilio toouse hello web app, обновив вашей `Gemfile` tooinclude этой строки:

    gem 'twilio-ruby'

В командной строке hello запуска `bundle install`. Теперь откройте `web.rb` и включая эту строку в верхней hello:

    require 'twilio-ruby'

Вы теперь все набор toouse hello Twilio вспомогательную библиотеку для Ruby в веб-приложения.

## <a id="howto_make_call"></a>Практическое руководство. Осуществление исходящего вызова
Следуя Hello показано, как вызвать toomake исходящего сообщения. Основные понятия относится использование hello Twilio вспомогательную библиотеку для toomake Ruby, которые вызывает API-Интерфейс REST и подготовке к просмотру TwiML. Подставьте собственные значения hello **из** и **для** номера телефонов и убедитесь в правильности hello **из** телефонный номер для кода hello предыдущих toorunning учетной записи Twilio.

Добавьте эту функцию слишком`web.md`:

    # Set your account ID and authentication token.
    sid = "your_twilio_account_sid";
    token = "your_twilio_authentication_token";

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from = "NNNNNNNNNNN";

    # hello number of hello phone receiving call.
    too= "NNNNNNNNNNN";

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://yourdomain.cloudapp.net/voice_url";

    get '/make_call' do
      # Create hello call client.
      client = Twilio::REST::Client.new(sid, token);

      # Make hello call
      client.account.calls.create(to: to, from: from, url: url)
    end

    post '/voice_url' do
      "<Response>
         <Say>Hello Monkey!</Say>
       </Response>"
    end

Если вы открыть доступ к `http://yourdomain.cloudapp.net/make_call` в браузере, вызывающих hello вызовов Twilio API toohello toomake hello телефонный звонок. Здравствуйте, первые два параметра в `client.account.calls.create` говорят сами за себя: hello номеров hello вызов `from` и число вызовов hello hello `to`. 

Здравствуйте, третий параметр (`url`) — hello URL-адрес, что Twilio запросы tooget инструкции какие toodo после подключения вызова hello. В данном случае мы настройки URL-адрес (`http://yourdomain.cloudapp.net`), возвращает простой документ TwiML и использует hello `<Say>` вызова команды toodo некоторые преобразования текста в речь и сказать «Hello Monkey» toohello лицо, получающее hello.

## <a id="howto_recieve_sms"></a>Руководство: получение SMS-сообщения
В предыдущем примере hello инициировал **исходящих** телефонный звонок. Это время, воспользуемся hello номер телефона, который мы получили Twilio во время регистрации tooprocess **входящих** SMS-сообщения.

Во-первых, в журнал tooyour [панель мониторинга Twilio][twilio_account]. Щелкните «Чисел» в верхней панели навигации hello и выберите команду hello номер Twilio, которые были предоставлены. Вы увидите два URL-адреса, которые можно настроить: URL-адрес запроса голосового вызова и URL-адрес запроса SMS. Это URL-адреса hello внесенных Twilio вызовы каждый раз, когда телефонный звонок или SMS-сообщения отправляется номер tooyour. Hello URL-адреса также известны как «обработчики web».

Мы хотели бы tooprocess SMS-сообщений, поэтому необходимо обновить URL-адрес hello слишком`http://yourdomain.cloudapp.net/sms_url`. Продолжим и нажмите кнопку Сохранить изменения hello нижней части страницы приветствия. Вернувшись `web.rb` давайте запрограммировать нашей toohandle приложения:

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for hello ping! Twilio and Azure rock!</Message>
       </Response>"
    end

После изменения "hello", убедитесь, что toore-start веб-приложения. Теперь Извлеките ваш телефон и отправки SMS tooyour номер Twilio. Следует своевременно получать ответ SMS, который говорит, что ему, Спасибо, что hello ping! Twilio and Azure rock!" (Спасибо за сообщение. Twilio и Azure лучше всех!).

## <a id="additional_services"></a>Руководство: использование дополнительных служб Twilio
В дополнение к этому toohello в этой статье примерах, Twilio предлагает веб-API, можно использовать дополнительные возможности Twilio tooleverage из приложения Azure. Дополнительные сведения см. в разделе hello [документации по Twilio API][twilio_api_documentation].

### <a id="NextSteps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello hello Twilio службы, выполните следующие дополнительные toolearn ссылки.

* [Рекомендации по безопасности Twilio][twilio_security_guidelines]
* [Практические руководства по Twilio и пример кода][twilio_howtos]
* [Краткие учебники по Twilio][twilio_quickstarts] 
* [Twilio на GitHub][twilio_on_github]
* [Обращайтесь tooTwilio поддержки][twilio_support]

[twilio_ruby]: https://www.twilio.com/docs/ruby/install





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
[sinatra]: http://www.sinatrarb.com/
[azure_vm_setup]: http://www.windowsazure.com/develop/ruby/tutorials/web-app-with-linux-vm/
