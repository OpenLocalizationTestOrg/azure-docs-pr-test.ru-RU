---
title: "aaaHow tooUse Twilio для SMS (.NET) и голосовой | Документы Microsoft"
description: "Узнайте, как toomake телефонного звонка и SMS отправки сообщений с hello Twilio API службы в Azure. Примеры программного кода написаны в .NET."
services: 
documentationcenter: .net
author: devinrader
manager: twilio
editor: 
ms.assetid: 74d4f3c9-f1cb-4968-b744-36b32cd0e834
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/24/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: f568da87ef15e9f540fee9674de31e983d4acb6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-from-azure"></a>Как toouse Twilio для голосовых возможностей и SMS из Azure
В этом руководстве показано, как tooperform часто встречающиеся задачи программирования с hello Twilio API службы в Azure. Hello сценарии включают телефонных звонков и отправке сообщения службы коротких сообщений (SMS). Дополнительные сведения о Twilio и использования голоса и SMS в приложениях см. в разделе hello [дальнейшие действия](#NextSteps) раздела.

## <a id="WhatIs"></a>Что такое Twilio?
Twilio включении hello будущее делового общения, включение разработчики tooembed голос, VoIP и обмен сообщениями в приложения. Они виртуализация всех инфраструктуру в среде облачных, глобальные, предоставляя его через hello Twilio communications API платформы. Приложения, простой toobuild и масштабируемость. Оцените гибкость работы с оплатой по мере использования и преимущества надежности облака.

**Голосовой Twilio** позволяет toomake вашего приложения и приема телефонных звонков. **Twilio SMS** включает toosend вашего приложения и получения сообщений SMS. **Клиента Twilio** позволяет toomake VoIP вызовы из любой телефон, планшет или браузера и поддерживает WebRTC.

## <a id="Pricing"></a>Цены и специальные предложения Twilio
Клиентам Azure доступно [специальное предложение](http://www.twilio.com/azure): кредит Twilio в размере 10 долл. США при обновлении учетной записи Twilio. Это кредит Twilio может быть применен tooany Twilio использования ($10 кредит эквивалентные toosending до 1 000 SMS-сообщений или получение копии too1000 входящих голосовых минут, в зависимости от расположения hello ваш телефонный номер и сообщений или вызовов назначения). Получите этот кредит Twilio и приступите к работе на [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).

Twilio представляет собой службу с повременной оплатой. Стартовые платежи отсутствуют, а учетную запись можно закрыть в любое время. Дополнительные сведения см. в статье [Цены на Twilio](http://www.twilio.com/voice/pricing).

## <a id="Concepts"></a>Основные понятия
Hello Twilio API является API RESTful, который предоставляет функциональные возможности SMS и голосовой для приложений. Полный список клиентских библиотек API Twilio, которые доступны на разных языках, см. на [этой странице][twilio_libraries].

Ключевые аспекты hello Twilio API, Twilio глаголов и язык разметки Twilio (TwiML).

### <a id="Verbs"></a>Команды Twilio
Hello API использует Twilio команд; Например, hello  **&lt;Say&gt;**  команда предписывает Twilio tooaudibly доставить сообщение во время вызова.

Hello ниже приведен список команд, Twilio.  Дополнительные сведения о hello других команд и возможностей через [документации язык разметки Twilio](http://www.twilio.com/docs/api/twiml).

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

## <a id="create_app"></a>Создание приложения Azure
Приложение Azure, на котором размещается приложение с поддержкой Twilio, ничем не отличается от любого другого приложения Azure. Добавление библиотеки Twilio .NET hello и настроить hello роли toouse hello Twilio .NET библиотеки.
Сведения о создании начального проекта Azure с помощью Visual Studio см. на [этой странице][vs_project].

## <a id="configure_app"></a>Настройка приложения toouse Twilio библиотек
Twilio предоставляет набор вспомогательных библиотек .NET, являющиеся оболочками для различных аспектов toointeract простой и легко tooprovide Twilio с Twilio REST API hello и клиента Twilio toogenerate TwiML ответов.

Twilio предоставляет пять библиотек для разработчиков .NET:
Библиотека|Описание
---|---
Twilio.API|Twilio библиотеки ядра Hello, которая создает оболочку для API-интерфейса REST Twilio hello понятное библиотеки .NET. Эта библиотека доступна для .NET, Silverlight и Windows Phone 7.
Twilio.TwiML|Предоставляет разметку TwiML toogenerate .NET понятным способом.
Twilio.MVC|Для разработчиков, использующих ASP.NET MVC, эта библиотека включает в себя TwilioController, TwiML ActionResult и атрибут проверки запроса.
Twilio.WebMatrix|Для разработчиков, использующих бесплатное средство разработки WebMatrix от Microsoft, эта библиотека содержит помощники синтаксиса Razor для выполнения различных действий Twilio.
Twilio.Client.Capability|Содержит маркера генератор hello возможностей для использования с hello Twilio клиента JavaScript SDK.

Обратите внимание, что для всех библиотек требуется .NET 3.5, Silverlight 4 и Windows Phone 7 или более поздней версии.

Hello образцы, описанные в настоящем руководстве используйте библиотеку Twilio.API hello.

Hello библиотеки могут быть [установить с помощью расширения диспетчера пакетов NuGet hello](http://www.twilio.com/docs/csharp/install) доступны для Visual Studio 2010 копии too2015.  Hello исходный код размещается на [GitHub][twilio_github_repo], который включает вики-сайт, который содержит полную документацию по использованию библиотеки hello.

По умолчанию Microsoft Visual Studio 2010 устанавливает NuGet версии 1.2. Установка библиотек Twilio hello требуется версия 1.6 NuGet или более поздней версии. Дополнительные сведения об установке или обновлении NuGet см. на веб-сайте [http://nuget.org/][nuget].

> [!NOTE]
> tooinstall hello версию NuGet, сначала необходимо удалить hello Загруженная версия с помощью hello Диспетчер расширений Visual Studio. toodo таким образом, необходимо запустить Visual Studio от имени администратора. В противном случае будет отключена кнопка удаления hello.
>
>

### <a id="use_nuget"></a>tooadd hello Twilio библиотеки tooyour проекта Visual Studio:
1. Откройте решение в Visual Studio.
2. Щелкните правой кнопкой мыши **References**(Ссылки).
3. Щелкните **Manage NuGet Packages...**
4. Щелкните **Online**(В сети).
5. В hello поиска online введите *twilio*.
6. Нажмите кнопку **установить** hello Twilio пакета.

## <a id="howto_make_call"></a>Практическое руководство. Осуществление исходящего вызова
Hello ниже показано, как исходящий toomake вызвать с помощью hello **CallResource** класса. Этот код также использует предоставляемые системой Twilio сайта tooreturn hello ответ языка разметки Twilio (TwiML). Подставьте собственные значения hello **для** и **из** номера телефонов и убедитесь в правильности hello **из** телефонный номер для учетной записи Twilio перед выполнением кода hello.

    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize hello TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    var url = "http://twimlets.com/message";
    url = $"{url}?Message%5B0%5D=Hello%20World";

    // Set hello call From, To, and URL values toouse for hello call.
    // This sample uses hello sandbox number provided by
    // Twilio toomake hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri(url));
        }

Дополнительные сведения о параметрах hello, передаваемых в toohello **CallResource.Create** метода, в разделе [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].

Как уже упоминалось, этот код использует hello tooreturn Twilio техники сайта TwiML ответа. Можно использовать собственный узел tooprovide hello TwiML ответа. Дополнительные сведения см. в разделе [Практическое руководство. Предоставление ответа TwiML с собственного веб-сайта](#howto_provide_twiml_responses).

## <a id="howto_send_sms"></a>Практическое руководство. Отправка SMS-сообщения
Hello следующем снимке экрана показано, как hello toosend сообщение SMS с помощью **MessageResource** класса. Hello **из** номер обеспечивается Twilio для пробной версии учетных записей toosend SMS-сообщений. Hello **для** необходимо проверить номер для учетной записи Twilio, перед выполнением кода hello.

    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize hello TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    try
    {
        // Send an SMS message.
        var message = MessageResource.Create(
            to: new PhoneNumber("+12069419717"),
            from: new PhoneNumber("+14155992671"),
            body: "This is my SMS message.");
    }
    catch (TwilioException ex)
    {
        // An exception occurred making hello REST call
        Console.WriteLine(ex.Message);
    }

## <a id="howto_provide_twiml_responses"></a>Практическое руководство. Предоставление откликов TwiML с вашего веб-сайта
Когда приложения так, инициирует вызов toohello Twilio API - через hello **CallResource.Create** метод - Twilio отправляет вашей tooan URL-адрес запроса, ожидаемый tooreturn TwiML ответ. пример Hello в [как: Убедитесь, исходящий вызов](#howto_make_call) использует Здравствуйте, предоставляемых системой Twilio URL-адрес [http://twimlets.com/message] [ twimlet_message_url] tooreturn hello ответа.

> [!NOTE]
> Хотя TwiML предназначен для использования веб-службами, hello TwiML можно просмотреть в браузере. Например, щелкните [http://twimlets.com/message] [ twimlet_message_url] toosee пустой &lt;ответ&gt; элемента; еще один пример, нажмите кнопку [http://twimlets.com/message ? Сообщение 5B0 %% 5 D = Hello % 20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee &lt;ответа&gt; элемент, содержащий &lt;Say&gt; элемент.
>
>

Вместо hello Twilio предоставленный URL-адрес, можно создать собственного URL-адрес веб-сайта, возвращающий HTTP-ответов. Можно создать сайт hello на любом языке, который возвращает HTTP-ответов. В этом разделе предполагается, что будет размещение hello URL-адрес из обработчика универсальных ASP.NET.

следующий обработчик ASP.NET Hello crafts TwiML ответ, который говорит **Hello World** при вызове функции hello.

    using System.Text;
    using System.Web;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {
            public void ProcessRequest(HttpContext context)
            {
                const string twiMLResponse =
                    "<Response><Say>Hello World.</Say></Response>";
                
                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.ContentEncoding = Encoding.UTF8;
                context.Response.Write(twiMLResponse);
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }
    
Как видно в приведенном выше примере hello hello TwiML ответа является просто XML-документа. Библиотека Twilio.TwiML Hello содержит классы, которые создают TwiML для вас. Hello приведенном ниже примере создает эквивалентный ответа hello, как показано выше, но использует hello **VoiceResponse** класса.

    using System.Web;
    using Twilio.TwiML;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {

            public void ProcessRequest(HttpContext context)
            {
                var twiml = new VoiceResponse();
                twiml.Say("Hello World.");

                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.Write(twiml.ToString());
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }

Дополнительные сведения о TwiML см. по следующему адресу: [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).

После настройки ответы TwiML tooprovide способом можно передать этот URL-адрес toohello **CallResource.Create** метод. Например, если у вас есть веб-приложения с именем tooan MyTwiML развертывания облачной службы Azure, а hello обработчиком ASP.NET называется mytwiml.ashx, hello URL-адрес можно передать слишком**CallResource.Create** как показано в следующим hello Пример:

    // This sample uses hello sandbox number provided by Twilio toomake hello call.
    // Place hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

Дополнительные сведения об использовании Twilio в Azure с помощью ASP.NET см. в разделе [как toomake вызвать с использованием Twilio в веб-роли в Azure Телефон][howto_phonecall_dotnet].

[!INCLUDE [twilio-additional-services-and-next-steps](../includes/twilio-additional-services-and-next-steps.md)]

[howto_phonecall_dotnet]: partner-twilio-cloud-services-dotnet-phone-call-web-role.md

[twimlet_message_url]: http://twimlets.com/message

[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls

[vs_project]:http://msdn.microsoft.com/library/windowsazure/ee405487.aspx
[nuget]:http://nuget.org/
[twilio_github_repo]:https://github.com/twilio/twilio-csharp

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified
