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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-java"></a><span data-ttu-id="55eab-104">Как tooUse Twilio для голосовых возможностей и SMS в Java</span><span class="sxs-lookup"><span data-stu-id="55eab-104">How tooUse Twilio for Voice and SMS Capabilities in Java</span></span>
<span data-ttu-id="55eab-105">В этом руководстве показано, как tooperform часто встречающиеся задачи программирования с hello Twilio API службы в Azure.</span><span class="sxs-lookup"><span data-stu-id="55eab-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="55eab-106">Hello сценарии включают телефонных звонков и отправке сообщения службы коротких сообщений (SMS).</span><span class="sxs-lookup"><span data-stu-id="55eab-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="55eab-107">Дополнительные сведения о Twilio и использования голоса и SMS в приложениях см. в разделе hello [дальнейшие действия](#NextSteps) раздела.</span><span class="sxs-lookup"><span data-stu-id="55eab-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="55eab-108"><a id="WhatIs"></a>Что такое Twilio?</span><span class="sxs-lookup"><span data-stu-id="55eab-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="55eab-109">Twilio — это API веб службы телефонии, которая позволяет использовать существующие языки веб и навыки toobuild голос, а приложений SMS.</span><span class="sxs-lookup"><span data-stu-id="55eab-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills toobuild voice and SMS applications.</span></span> <span data-ttu-id="55eab-110">Twilio — это сторонняя служба (не компонент Azure и не продукт Майкрософт).</span><span class="sxs-lookup"><span data-stu-id="55eab-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="55eab-111">**Голосовой Twilio** позволяет toomake вашего приложения и приема телефонных звонков.</span><span class="sxs-lookup"><span data-stu-id="55eab-111">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="55eab-112">**Twilio SMS** позволяет toomake вашего приложения и получения сообщений SMS.</span><span class="sxs-lookup"><span data-stu-id="55eab-112">**Twilio SMS** allows your applications toomake and receive SMS messages.</span></span> <span data-ttu-id="55eab-113">**Клиента Twilio** позволяет tooenable голосовой связи с использованием существующих соединений Интернета, в том числе мобильными приложениями.</span><span class="sxs-lookup"><span data-stu-id="55eab-113">**Twilio Client** allows your applications tooenable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="55eab-114"><a id="Pricing"></a>Цены и специальные предложения Twilio</span><span class="sxs-lookup"><span data-stu-id="55eab-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="55eab-115">Сведения о ценах на Twilio доступны на веб-сайте [цен на Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="55eab-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="55eab-116">Клиентам Azure доступно [специальное предложение][special_offer]: бесплатный кредит на 1000 текстовых сообщений или 1000 минут входящих вызовов.</span><span class="sxs-lookup"><span data-stu-id="55eab-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="55eab-117">toosign для использования это предложение или получить дополнительные сведения, посетите [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="55eab-117">toosign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>

## <span data-ttu-id="55eab-118"><a id="Concepts"></a>Основные понятия</span><span class="sxs-lookup"><span data-stu-id="55eab-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="55eab-119">Hello Twilio API является API RESTful, который предоставляет функциональные возможности SMS и голосовой для приложений.</span><span class="sxs-lookup"><span data-stu-id="55eab-119">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="55eab-120">Полный список клиентских библиотек API Twilio, которые доступны на разных языках, см. на [этой странице][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="55eab-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="55eab-121">Ключевые аспекты hello Twilio API, Twilio глаголов и язык разметки Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="55eab-121">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="55eab-122"><a id="Verbs"></a>Команды Twilio</span><span class="sxs-lookup"><span data-stu-id="55eab-122"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="55eab-123">Hello API использует Twilio команд; Например, hello  **&lt;Say&gt;**  команда предписывает Twilio tooaudibly доставить сообщение во время вызова.</span><span class="sxs-lookup"><span data-stu-id="55eab-123">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="55eab-124">Hello ниже приведен список команд, Twilio.</span><span class="sxs-lookup"><span data-stu-id="55eab-124">hello following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="55eab-125">**&lt;Удаленный&gt;**: подключается phone tooanother hello вызывающего объекта.</span><span class="sxs-lookup"><span data-stu-id="55eab-125">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="55eab-126">**&lt;Соберите&gt;**: собирает цифры, введенные на клавиатуре телефона hello.</span><span class="sxs-lookup"><span data-stu-id="55eab-126">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="55eab-127">**&lt;Hangup&gt;**: окончание вызова.</span><span class="sxs-lookup"><span data-stu-id="55eab-127">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="55eab-128">**&lt;Play&gt;**: воспроизведение звукового файла.</span><span class="sxs-lookup"><span data-stu-id="55eab-128">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="55eab-129">**&lt;Очередь&gt;**: добавить очередь tooa hello вызывающих объектов.</span><span class="sxs-lookup"><span data-stu-id="55eab-129">**&lt;Queue&gt;**: Add hello tooa queue of callers.</span></span>
* <span data-ttu-id="55eab-130">**&lt;Pause&gt;**: бесшумное ожидание в течение указанного времени (в секундах).</span><span class="sxs-lookup"><span data-stu-id="55eab-130">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="55eab-131">**&lt;Запись&gt;**: записи голоса hello вызывающего объекта и возвращает URL-адрес файла, содержащего запись hello.</span><span class="sxs-lookup"><span data-stu-id="55eab-131">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="55eab-132">**&lt;Перенаправить&gt;**: передает управление вызова или SMS toohello TwiML на другой URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="55eab-132">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="55eab-133">**&lt;Отклонить&gt;**: отклоняет во входящих вызова tooyour Twilio номер без выставления счетов за вас.</span><span class="sxs-lookup"><span data-stu-id="55eab-133">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you.</span></span>
* <span data-ttu-id="55eab-134">**&lt;Предположим,&gt;**: toospeech преобразует текст, который выполняется при вызове функции.</span><span class="sxs-lookup"><span data-stu-id="55eab-134">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="55eab-135">**&lt;Sms&gt;**: отправка SMS-сообщения.</span><span class="sxs-lookup"><span data-stu-id="55eab-135">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="55eab-136"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="55eab-136"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="55eab-137">TwiML — это набор инструкций, основанный на XML основании hello Twilio команд, которые сообщают Twilio того, как tooprocess звонок или SMS.</span><span class="sxs-lookup"><span data-stu-id="55eab-137">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="55eab-138">Например, следующие TwiML hello бы преобразование текста hello **Здравствуй, мир!**</span><span class="sxs-lookup"><span data-stu-id="55eab-138">As an example, hello following TwiML would convert hello text **Hello World!**</span></span> <span data-ttu-id="55eab-139">toospeech.</span><span class="sxs-lookup"><span data-stu-id="55eab-139">toospeech.</span></span>

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="55eab-140">Когда приложение вызывает hello Twilio API, один из параметров API hello, hello URL-адрес, который возвращает ответ TwiML hello.</span><span class="sxs-lookup"><span data-stu-id="55eab-140">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="55eab-141">В целях разработки можно использовать предоставляемые системой Twilio URL-адреса hello tooprovide TwiML ответов, используемых приложениями.</span><span class="sxs-lookup"><span data-stu-id="55eab-141">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="55eab-142">Может также содержать собственные ответы TwiML hello tooproduce URL-адресов и другой вариант — toouse hello **TwiMLResponse** объекта.</span><span class="sxs-lookup"><span data-stu-id="55eab-142">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="55eab-143">Дополнительные сведения о командах Twilio, их атрибутах и TwiML см. на странице [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="55eab-143">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="55eab-144">Дополнительные сведения о hello Twilio API см. в разделе [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="55eab-144">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="55eab-145"><a id="CreateAccount"></a>Создание учетной записи Twilio</span><span class="sxs-lookup"><span data-stu-id="55eab-145"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="55eab-146">Когда вы будете готовы tooget учетной записи Twilio, зарегистрируйтесь на [повторите Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="55eab-146">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="55eab-147">Вы можете начать с бесплатной учетной записи и обновить ее позднее.</span><span class="sxs-lookup"><span data-stu-id="55eab-147">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="55eab-148">При регистрации учетной записи Twilio, вы получите идентификатор учетной записи и маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="55eab-148">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="55eab-149">Как будет toomake необходимые вызовы Twilio API.</span><span class="sxs-lookup"><span data-stu-id="55eab-149">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="55eab-150">tooprevent несанкционированный доступ к учетной записи tooyour, безопасность срок действия токена проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="55eab-150">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="55eab-151">Идентификатор учетной записи и проверки подлинности маркера могут быть просмотрены в hello [консоли Twilio][twilio_console]в hello поля с меткой **ИД безопасности учетной записи** и **ТОКЕНА проверки Подлинности**соответственно.</span><span class="sxs-lookup"><span data-stu-id="55eab-151">Your account ID and authentication token are viewable at hello [Twilio Console][twilio_console], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="55eab-152"><a id="create_app"></a>Создание приложения Java</span><span class="sxs-lookup"><span data-stu-id="55eab-152"><a id="create_app"></a>Create a Java Application</span></span>
1. <span data-ttu-id="55eab-153">Получить hello Twilio JAR и добавить его tooyour путь и сборку развертывания WAR сборок Java.</span><span class="sxs-lookup"><span data-stu-id="55eab-153">Obtain hello Twilio JAR and add it tooyour Java build path and your WAR deployment assembly.</span></span> <span data-ttu-id="55eab-154">В [https://github.com/twilio/twilio-java][twilio_java], можно загрузить исходных GitHub hello и создать собственные JAR или загрузить предварительно построенного JAR-ФАЙЛ (с или без зависимостей).</span><span class="sxs-lookup"><span data-stu-id="55eab-154">At [https://github.com/twilio/twilio-java][twilio_java], you can download hello GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
2. <span data-ttu-id="55eab-155">Убедитесь в JDK **cacerts** ключей содержит hello Equifax Secure сертификации сертификат с MD5 отпечатков пальцев 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello серийный номер имеет 35:DE:F4:CF и hello SHA1 отпечаток пальца является D2:32:09:AD:23:D3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="55eab-155">Ensure your JDK's **cacerts** keystore contains hello Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello serial number is 35:DE:F4:CF and hello SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="55eab-156">Это hello сертификат центра сертификации (ЦС) для hello [https://api.twilio.com] [ twilio_api_service] службы, которая вызывается при использовании API Twilio.</span><span class="sxs-lookup"><span data-stu-id="55eab-156">This is hello certificate authority (CA) certificate for hello [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="55eab-157">Сведения об обеспечении вашего JDK **cacerts** правильный сертификат ЦС hello содержит хранилище ключей см. в разделе [Добавление сертификата toohello хранилища сертификатов центра сертификации Java][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="55eab-157">For information about ensuring your JDK's **cacerts** keystore contains hello correct CA certificate, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="55eab-158">Подробные инструкции по использованию hello Twilio клиентская библиотека для Java можно найти по адресу [как tooMake Twilio с помощью телефонного звонка в приложении Java в Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="55eab-158">Detailed instructions for using hello Twilio client library for Java are available at [How tooMake a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="55eab-159"><a id="configure_app"></a>Настройка приложения tooUse Twilio библиотек</span><span class="sxs-lookup"><span data-stu-id="55eab-159"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="55eab-160">В коде, можно добавить **импорта** инструкции вверху hello исходные файлы для hello Twilio пакеты или классы, вы хотите toouse в приложении.</span><span class="sxs-lookup"><span data-stu-id="55eab-160">Within your code, you can add **import** statements at hello top of your source files for hello Twilio packages or classes you want toouse in your application.</span></span>

<span data-ttu-id="55eab-161">Для исходных файлов Java:</span><span class="sxs-lookup"><span data-stu-id="55eab-161">For Java source files:</span></span>

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

<span data-ttu-id="55eab-162">Для исходных файлов Java Server Page (JSP):</span><span class="sxs-lookup"><span data-stu-id="55eab-162">For Java Server Page (JSP) source files:</span></span>

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
<span data-ttu-id="55eab-163">В зависимости от того, какие пакеты Twilio или классы требуется toouse, ваш **импорта** инструкции может быть другим.</span><span class="sxs-lookup"><span data-stu-id="55eab-163">Depending on which Twilio packages or classes you want toouse, your **import** statements may be different.</span></span>

## <span data-ttu-id="55eab-164"><a id="howto_make_call"></a>Практическое руководство. Осуществление исходящего вызова</span><span class="sxs-lookup"><span data-stu-id="55eab-164"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="55eab-165">Hello ниже показано, как исходящий toomake вызвать с помощью hello **вызовите** класса.</span><span class="sxs-lookup"><span data-stu-id="55eab-165">hello following shows how toomake an outgoing call using hello **Call** class.</span></span> <span data-ttu-id="55eab-166">Этот код также использует предоставляемые системой Twilio сайта tooreturn hello ответ языка разметки Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="55eab-166">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="55eab-167">Подставьте собственные значения hello **из** и **для** номера телефонов и убедитесь в правильности hello **из** телефонный номер для кода hello предыдущих toorunning учетной записи Twilio.</span><span class="sxs-lookup"><span data-stu-id="55eab-167">Substitute your values for hello **from** and **to** phone numbers, and ensure that you verify hello **from** phone number for your Twilio account prior toorunning hello code.</span></span>

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

<span data-ttu-id="55eab-168">Дополнительные сведения о параметрах hello, передаваемых в toohello **Call.creator** метода, в разделе [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="55eab-168">For more information about hello parameters passed in toohello **Call.creator** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="55eab-169">Как уже упоминалось, этот код использует hello tooreturn Twilio техники сайта TwiML ответа.</span><span class="sxs-lookup"><span data-stu-id="55eab-169">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="55eab-170">Можно использовать собственный узел tooprovide hello TwiML ответа; Дополнительные сведения см. в разделе [как tooProvide TwiML ответов в приложении Java в Azure](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="55eab-170">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses in a Java Application on Azure](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="55eab-171"><a id="howto_send_sms"></a>Практическое руководство. Отправка SMS-сообщения</span><span class="sxs-lookup"><span data-stu-id="55eab-171"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="55eab-172">Hello ниже показано, как сообщение SMS с помощью toosend hello **сообщение** класса.</span><span class="sxs-lookup"><span data-stu-id="55eab-172">hello following shows how toosend an SMS message using hello **Message** class.</span></span> <span data-ttu-id="55eab-173">Hello **из** номер, **4155992671**, предоставляемые Twilio для пробной версии учетных записей toosend SMS-сообщений.</span><span class="sxs-lookup"><span data-stu-id="55eab-173">hello **from** number, **4155992671**, is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="55eab-174">Hello **для** номер должен быть проверен кода hello предыдущих toorunning учетной записи Twilio.</span><span class="sxs-lookup"><span data-stu-id="55eab-174">hello **to** number must be verified for your Twilio account prior toorunning hello code.</span></span>

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

<span data-ttu-id="55eab-175">Дополнительные сведения о параметрах hello, передаваемых в toohello **Message.creator** метода, в разделе [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span><span class="sxs-lookup"><span data-stu-id="55eab-175">For more information about hello parameters passed in toohello **Message.creator** method, see [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span></span>

## <span data-ttu-id="55eab-176"><a id="howto_provide_twiml_responses"></a>Практическое руководство. Предоставление ответов TwiML с собственного веб-сайта</span><span class="sxs-lookup"><span data-stu-id="55eab-176"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="55eab-177">Когда приложение инициирует toohello вызова Twilio API, например через hello **CallCreator.create** метода Twilio отправит ваш tooa URL-адрес запроса, ожидаемый tooreturn TwiML ответ.</span><span class="sxs-lookup"><span data-stu-id="55eab-177">When your application initiates a call toohello Twilio API, for example via hello **CallCreator.create** method, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="55eab-178">Hello выше примере hello Twilio предоставленный URL-адрес [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="55eab-178">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="55eab-179">(Хотя TwiML предназначен для использования веб-службами, можно просмотреть hello TwiML в браузере.</span><span class="sxs-lookup"><span data-stu-id="55eab-179">(While TwiML is designed for use by Web services, you can view hello TwiML in your browser.</span></span> <span data-ttu-id="55eab-180">Например, щелкните [http://twimlets.com/message] [ twimlet_message_url] toosee пустой  **&lt;ответ&gt;**  элемента; еще один пример, нажмите кнопку [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21] [ twimlet_message_url_hello_world] toosee  **&lt;ответ&gt;**  элемент, содержащий  **&lt;Say &gt;**  элемента.)</span><span class="sxs-lookup"><span data-stu-id="55eab-180">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty **&lt;Response&gt;** element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] toosee a **&lt;Response&gt;** element that contains a **&lt;Say&gt;** element.)</span></span>

<span data-ttu-id="55eab-181">Вместо hello Twilio предоставленный URL-адрес, можно создать собственного URL-адрес веб-сайта, возвращающий HTTP-ответов.</span><span class="sxs-lookup"><span data-stu-id="55eab-181">Instead of relying on hello Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="55eab-182">Можно создать узел hello на любом языке, который возвращает HTTP-ответов; в этом разделе предполагается, что будет размещение hello URL-адрес на странице JSP.</span><span class="sxs-lookup"><span data-stu-id="55eab-182">You can create hello site in any language that returns HTTP responses; this topic assumes you'll be hosting hello URL in a JSP page.</span></span>

<span data-ttu-id="55eab-183">Здравствуйте следующие результаты в виде страниц JSP в ответе TwiML потребовал **Здравствуй, мир!**</span><span class="sxs-lookup"><span data-stu-id="55eab-183">hello following JSP page results in a TwiML response that says **Hello World!**</span></span> <span data-ttu-id="55eab-184">При вызове функции hello.</span><span class="sxs-lookup"><span data-stu-id="55eab-184">on hello call.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="55eab-185">следующие результаты в виде страниц JSP в ответе TwiML потребовал некоторый текст Hello имеет несколько приостанавливает свою работу и сообщает сведения о версии Twilio API hello и имя роли Azure hello.</span><span class="sxs-lookup"><span data-stu-id="55eab-185">hello following JSP page results in a TwiML response that says some text, has several pauses, and says information about hello Twilio API version and hello Azure role name.</span></span>

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

<span data-ttu-id="55eab-186">Hello **ApiVersion** параметр доступен в Twilio голосовых запросов (не SMS запросов).</span><span class="sxs-lookup"><span data-stu-id="55eab-186">hello **ApiVersion** parameter is available in Twilio voice requests (not SMS requests).</span></span> <span data-ttu-id="55eab-187">toosee hello доступного запроса параметров для голосового вызова Twilio и SMS запросов, в подразделе <https://www.twilio.com/docs/api/twiml/twilio_request> и <https://www.twilio.com/docs/api/twiml/sms/twilio_request >соответственно.</span><span class="sxs-lookup"><span data-stu-id="55eab-187">toosee hello available request parameters for Twilio voice and SMS requests, see <https://www.twilio.com/docs/api/twiml/twilio_request> and <https://www.twilio.com/docs/api/twiml/sms/twilio_request>, respectively.</span></span> <span data-ttu-id="55eab-188">Hello **RoleName** переменная среды доступна как часть развертывания Azure.</span><span class="sxs-lookup"><span data-stu-id="55eab-188">hello **RoleName** environment variable is available as part of an Azure deployment.</span></span> <span data-ttu-id="55eab-189">(Если требуется tooadd пользовательские переменные, поэтому они могут быть выбраны из **System.getenv**, см. раздел переменные среды hello в [прочие параметры конфигурации роли] [misc_role_config_settings].)</span><span class="sxs-lookup"><span data-stu-id="55eab-189">(If you want tooadd custom environment variables so they could be picked up from **System.getenv**, see hello environment variables section at [Miscellaneous Role Configuration Settings][misc_role_config_settings].)</span></span>

<span data-ttu-id="55eab-190">После страницы JSP Настройка tooprovide TwiML ответов служит hello URL-адрес страницы JSP hello hello URL-адреса, переданные в hello **Call.creator** метод.</span><span class="sxs-lookup"><span data-stu-id="55eab-190">Once you have your JSP page set up tooprovide TwiML responses, use hello URL of hello JSP page as hello URL passed into hello **Call.creator** method.</span></span> <span data-ttu-id="55eab-191">Например, если у вас есть веб-приложение с именем tooan MyTwiML развертывания Azure размещенной службы и hello имя страницы JSP hello mytwiml.jsp, hello URL-адрес может быть передан слишком**Call.creator** как показано в следующих hello:</span><span class="sxs-lookup"><span data-stu-id="55eab-191">For example, if you have a Web application named MyTwiML deployed tooan Azure hosted service, and hello name of hello JSP page is mytwiml.jsp, hello URL can be passed too**Call.creator** as shown in hello following:</span></span>

```java
    // Declare tooand From numbers and hello URL of your JSP page
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="55eab-192">Отвечать на запросы с TwiML может через hello **VoiceResponse** класс, который доступен в hello **com.twilio.twiml** пакета.</span><span class="sxs-lookup"><span data-stu-id="55eab-192">Another option for responding with TwiML is via hello **VoiceResponse** class, which is available in hello **com.twilio.twiml** package.</span></span>

<span data-ttu-id="55eab-193">Дополнительные сведения об использовании Twilio в Azure с Java см. в разделе [как tooMake Twilio с помощью телефонного звонка в приложении Java в Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="55eab-193">For additional information about using Twilio in Azure with Java, see [How tooMake a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="55eab-194"><a id="AdditionalServices"></a>Руководство: использование дополнительных служб Twilio</span><span class="sxs-lookup"><span data-stu-id="55eab-194"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="55eab-195">В дополнение к этому toohello в этой статье примерах, Twilio предлагает веб-API, можно использовать дополнительные возможности Twilio tooleverage из приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="55eab-195">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="55eab-196">Дополнительные сведения см. в разделе hello [документации по Twilio API][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="55eab-196">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="55eab-197"><a id="NextSteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="55eab-197"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="55eab-198">Теперь, когда вы узнали основы hello hello Twilio службы, выполните следующие дополнительные toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="55eab-198">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="55eab-199">[Рекомендации по безопасности Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="55eab-199">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="55eab-200">[Практические руководства по Twilio и примеры кода][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="55eab-200">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="55eab-201">[Краткие учебники по Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="55eab-201">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="55eab-202">[Twilio на GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="55eab-202">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="55eab-203">[Обращайтесь tooTwilio поддержки][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="55eab-203">[Talk tooTwilio Support][twilio_support]</span></span>

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
