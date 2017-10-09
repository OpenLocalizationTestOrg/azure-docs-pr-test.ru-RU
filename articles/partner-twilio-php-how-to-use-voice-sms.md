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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-php"></a><span data-ttu-id="2bcdf-104">Как tooUse Twilio для голосовых возможностей и SMS на PHP</span><span class="sxs-lookup"><span data-stu-id="2bcdf-104">How tooUse Twilio for Voice and SMS Capabilities in PHP</span></span>
<span data-ttu-id="2bcdf-105">В этом руководстве показано, как tooperform часто встречающиеся задачи программирования с hello Twilio API службы в Azure.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="2bcdf-106">Hello сценарии включают телефонных звонков и отправке сообщения службы коротких сообщений (SMS).</span><span class="sxs-lookup"><span data-stu-id="2bcdf-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="2bcdf-107">Дополнительные сведения о Twilio и использования голоса и SMS в приложениях см. в разделе hello [дальнейшие действия](#NextSteps) раздела.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="2bcdf-108"><a id="WhatIs"></a>Что такое Twilio?</span><span class="sxs-lookup"><span data-stu-id="2bcdf-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="2bcdf-109">Twilio включении hello будущее делового общения, включение разработчики tooembed голос, VoIP и обмен сообщениями в приложения.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="2bcdf-110">Они виртуализация всех инфраструктуру в среде облачных, глобальные, предоставляя его через hello Twilio communications API платформы.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="2bcdf-111">Приложения, простой toobuild и масштабируемость.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="2bcdf-112">Оцените гибкость повременной оплаты, а также преимущества, связанные с надежностью облачных решений.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="2bcdf-113">**Голосовой Twilio** позволяет toomake вашего приложения и приема телефонных звонков.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="2bcdf-114">**Twilio SMS** позволяет toosend вашего приложения и получать текстовые сообщения.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-114">**Twilio SMS** enables your application toosend and receive text messages.</span></span> <span data-ttu-id="2bcdf-115">**Клиента Twilio** позволяет toomake VoIP вызовы из любой телефон, планшет или браузера и поддерживает WebRTC.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="2bcdf-116"><a id="Pricing"></a>Цены и специальные предложения Twilio</span><span class="sxs-lookup"><span data-stu-id="2bcdf-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="2bcdf-117">Клиентам Azure доступно [специальное предложение](http://www.twilio.com/azure): кредит Twilio в размере 10 долл. США при обновлении учетной записи Twilio.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="2bcdf-118">Это кредит Twilio может быть применен tooany Twilio использования ($10 кредит эквивалентные toosending до 1 000 SMS-сообщений или получение копии too1000 входящих голосовых минут, в зависимости от расположения hello ваш телефонный номер и сообщений или вызовов назначения).</span><span class="sxs-lookup"><span data-stu-id="2bcdf-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="2bcdf-119">Получите этот кредит Twilio и приступите к работе на странице [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="2bcdf-119">Redeem this Twilio credit and get started at: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="2bcdf-120">Twilio представляет собой службу с повременной оплатой.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="2bcdf-121">Стартовые платежи отсутствуют, а учетную запись можно закрыть в любое время.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="2bcdf-122">Дополнительные сведения см. в статье [Цены на Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="2bcdf-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="2bcdf-123"><a id="Concepts"></a>Основные понятия</span><span class="sxs-lookup"><span data-stu-id="2bcdf-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="2bcdf-124">Hello Twilio API является API RESTful, который предоставляет функциональные возможности SMS и голосовой для приложений.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="2bcdf-125">Полный список клиентских библиотек API Twilio, которые доступны на разных языках, см. на [этой странице][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="2bcdf-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="2bcdf-126">Ключевые аспекты hello Twilio API, Twilio глаголов и язык разметки Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="2bcdf-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="2bcdf-127"><a id="Verbs"></a>Команды Twilio</span><span class="sxs-lookup"><span data-stu-id="2bcdf-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="2bcdf-128">Hello API использует Twilio команд; Например, hello  **&lt;Say&gt;**  команда предписывает Twilio tooaudibly доставить сообщение во время вызова.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="2bcdf-129">Hello ниже приведен список команд, Twilio.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-129">hello following is a list of Twilio verbs.</span></span> <span data-ttu-id="2bcdf-130">Дополнительные сведения о hello других команд и возможностей через [документации язык разметки Twilio](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="2bcdf-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="2bcdf-131">**&lt;Удаленный&gt;**: подключается phone tooanother hello вызывающего объекта.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="2bcdf-132">**&lt;Соберите&gt;**: собирает цифры, введенные на клавиатуре телефона hello.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="2bcdf-133">**&lt;Hangup&gt;**: окончание вызова.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="2bcdf-134">**&lt;Play&gt;**: воспроизведение звукового файла.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="2bcdf-135">**&lt;Pause&gt;**: бесшумное ожидание в течение указанного времени (в секундах).</span><span class="sxs-lookup"><span data-stu-id="2bcdf-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="2bcdf-136">**&lt;Запись&gt;**: записи голоса hello вызывающего объекта и возвращает URL-адрес файла, содержащего запись hello.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-136">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="2bcdf-137">**&lt;Перенаправить&gt;**: передает управление вызова или SMS toohello TwiML на другой URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="2bcdf-138">**&lt;Отклонить&gt;**: отклоняет во входящих вызова tooyour Twilio номер без выставления счетов, вы</span><span class="sxs-lookup"><span data-stu-id="2bcdf-138">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="2bcdf-139">**&lt;Предположим,&gt;**: toospeech преобразует текст, который выполняется при вызове функции.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-139">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="2bcdf-140">**&lt;Sms&gt;**: отправка SMS-сообщения.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="2bcdf-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="2bcdf-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="2bcdf-142">TwiML — это набор инструкций, основанный на XML основании hello Twilio команд, которые сообщают Twilio того, как tooprocess звонок или SMS.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-142">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="2bcdf-143">Например, следующие TwiML hello бы преобразование текста hello **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-143">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="2bcdf-144">Когда приложение вызывает hello Twilio API, один из параметров API hello, hello URL-адрес, который возвращает ответ TwiML hello.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-144">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="2bcdf-145">В целях разработки можно использовать предоставляемые системой Twilio URL-адреса hello tooprovide TwiML ответов, используемых приложениями.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-145">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="2bcdf-146">Может также содержать собственные ответы TwiML hello tooproduce URL-адресов и другой вариант — toouse hello **TwiMLResponse** объекта.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-146">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="2bcdf-147">Дополнительные сведения о командах Twilio, их атрибутах и TwiML см. на странице [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="2bcdf-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="2bcdf-148">Дополнительные сведения о hello Twilio API см. в разделе [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="2bcdf-148">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="2bcdf-149"><a id="CreateAccount"></a>Создание учетной записи Twilio</span><span class="sxs-lookup"><span data-stu-id="2bcdf-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="2bcdf-150">Когда вы будете готовы tooget учетной записи Twilio, зарегистрируйтесь на [повторите Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="2bcdf-150">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="2bcdf-151">Вы можете начать с бесплатной учетной записи и обновить ее позднее.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="2bcdf-152">При регистрации учетной записи Twilio, вы получите идентификатор учетной записи и маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="2bcdf-153">Как будет toomake необходимые вызовы Twilio API.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-153">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="2bcdf-154">tooprevent несанкционированный доступ к учетной записи tooyour, безопасность срок действия токена проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-154">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="2bcdf-155">Идентификатор учетной записи и проверки подлинности маркера могут быть просмотрены в hello [странице учетной записи Twilio][twilio_account]в hello поля с меткой **ИД безопасности учетной записи** и **ТОКЕНА проверки Подлинности**соответственно.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-155">Your account ID and authentication token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="2bcdf-156"><a id="create_app"></a>Создание приложения PHP</span><span class="sxs-lookup"><span data-stu-id="2bcdf-156"><a id="create_app"></a>Create a PHP Application</span></span>
<span data-ttu-id="2bcdf-157">Приложение PHP, которое использует службу hello Twilio и работает в Azure не отличается от любого другого приложения PHP, использующего службу hello Twilio.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-157">A PHP application that uses hello Twilio service and is running in Azure is no different than any other PHP application that uses hello Twilio service.</span></span> <span data-ttu-id="2bcdf-158">Хотя Twilio служб на основе REST и может вызываться из PHP несколькими способами, в этой статье основное внимание уделяется как toouse Twilio служб с [Twilio библиотеки для PHP с сайта GitHub][twilio_php].</span><span class="sxs-lookup"><span data-stu-id="2bcdf-158">While Twilio services are REST-based and can be called from PHP in several ways, this article will focus on how toouse Twilio services with [Twilio library for PHP from GitHub][twilio_php].</span></span> <span data-ttu-id="2bcdf-159">Дополнительные сведения об использовании библиотеки hello Twilio для PHP см. в разделе [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="2bcdf-159">For more information about using hello Twilio library for PHP, see [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="2bcdf-160">Подробные инструкции для создания и развертывания приложения Twilio и PHP tooAzure можно найти по адресу [как tooMake Twilio с помощью телефонного звонка в приложения PHP в Azure][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="2bcdf-160">Detailed instructions for building and deploying a Twilio/PHP application tooAzure are available at [How tooMake a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="2bcdf-161"><a id="configure_app"></a>Настройка приложения tooUse Twilio библиотек</span><span class="sxs-lookup"><span data-stu-id="2bcdf-161"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="2bcdf-162">Можно настроить библиотеку приложения hello toouse Twilio для PHP двумя способами:</span><span class="sxs-lookup"><span data-stu-id="2bcdf-162">You can configure your application toouse hello Twilio library for PHP in two ways:</span></span>

1. <span data-ttu-id="2bcdf-163">Загрузка библиотеки hello Twilio для PHP с сайта GitHub ([https://github.com/twilio/twilio-php][twilio_php]) и добавьте hello **служб** приложение tooyour каталога.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-163">Download hello Twilio library for PHP from GitHub ([https://github.com/twilio/twilio-php][twilio_php]) and add hello **Services** directory tooyour application.</span></span>
   
    <span data-ttu-id="2bcdf-164">-ИЛИ-</span><span class="sxs-lookup"><span data-stu-id="2bcdf-164">-OR-</span></span>
2. <span data-ttu-id="2bcdf-165">Установка библиотеки hello Twilio для PHP в качестве ГРУШИ пакета.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-165">Install hello Twilio library for PHP as a PEAR package.</span></span> <span data-ttu-id="2bcdf-166">Он может быть установлен с hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="2bcdf-166">It can be installed with hello following commands:</span></span>
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

<span data-ttu-id="2bcdf-167">После установки библиотеки hello Twilio для PHP можно добавить **require_once** инструкции вверху hello вашей PHP файлы библиотеки hello tooreference:</span><span class="sxs-lookup"><span data-stu-id="2bcdf-167">Once you have installed hello Twilio library for PHP, you can then add a **require_once** statement at hello top of your PHP files tooreference hello library:</span></span>

        require_once 'Services/Twilio.php';

<span data-ttu-id="2bcdf-168">Дополнительные сведения см. в разделе [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="2bcdf-168">For more information, see [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="2bcdf-169"><a id="howto_make_call"></a>Практическое руководство. Осуществление исходящего вызова</span><span class="sxs-lookup"><span data-stu-id="2bcdf-169"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="2bcdf-170">Hello ниже показано, как исходящий toomake вызвать с помощью hello **Services_Twilio** класса.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-170">hello following shows how toomake an outgoing call using hello **Services_Twilio** class.</span></span> <span data-ttu-id="2bcdf-171">Этот код также использует предоставляемые системой Twilio сайта tooreturn hello ответ языка разметки Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="2bcdf-171">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="2bcdf-172">Подставьте собственные значения hello **из** и **для** номера телефонов и убедитесь в правильности hello **из** телефонный номер для кода hello предыдущих toorunning учетной записи Twilio.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-172">Substitute your values for hello **From** and **To** phone numbers, and ensure that you verify hello **From** phone number for your Twilio account prior toorunning hello code.</span></span>

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

<span data-ttu-id="2bcdf-173">Как уже упоминалось, этот код использует hello tooreturn Twilio техники сайта TwiML ответа.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-173">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="2bcdf-174">Можно использовать собственный узел tooprovide hello TwiML ответа; Дополнительные сведения см. в разделе [как tooProvide TwiML ответов от ваш собственный веб-сайт](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="2bcdf-174">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

* <span data-ttu-id="2bcdf-175">**Примечание**: см. ошибки проверки сертификатов SSL tootroubleshoot [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span><span class="sxs-lookup"><span data-stu-id="2bcdf-175">**Note**: tootroubleshoot SSL certificate validation errors, see [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span></span> 

## <span data-ttu-id="2bcdf-176"><a id="howto_send_sms"></a>Практическое руководство. Отправка SMS-сообщения</span><span class="sxs-lookup"><span data-stu-id="2bcdf-176"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="2bcdf-177">Hello ниже показано, как сообщение SMS с помощью toosend hello **Services_Twilio** класса.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-177">hello following shows how toosend an SMS message using hello **Services_Twilio** class.</span></span> <span data-ttu-id="2bcdf-178">Hello **из** номер обеспечивается Twilio для пробной версии учетных записей toosend SMS-сообщений.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-178">hello **From** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="2bcdf-179">Hello **для** номер должен быть проверен кода hello предыдущих toorunning учетной записи Twilio.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-179">hello **To** number must be verified for your Twilio account prior toorunning hello code.</span></span>

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

## <span data-ttu-id="2bcdf-180"><a id="howto_provide_twiml_responses"></a>Практическое руководство. Предоставление ответов TwiML с собственного веб-сайта</span><span class="sxs-lookup"><span data-stu-id="2bcdf-180"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="2bcdf-181">Когда приложение начинает toohello вызова Twilio API, Twilio будет отправлено на tooa URL-адрес запроса, ожидался tooreturn TwiML ответ.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-181">When your application initiates a call toohello Twilio API, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="2bcdf-182">Hello выше примере hello Twilio предоставленный URL-адрес [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="2bcdf-182">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="2bcdf-183">(Хотя TwiML предназначен для использования с Twilio, можно просмотреть его hello в браузере.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-183">(While TwiML is designed for use by Twilio, you can view hello it in your browser.</span></span> <span data-ttu-id="2bcdf-184">Например, щелкните [http://twimlets.com/message] [ twimlet_message_url] toosee пустой `<Response>` элемент; в качестве другого примера, нажмите кнопку [http://twimlets.com/message? Сообщения % 5B0 %5 D = Hello % 20World] [ twimlet_message_url_hello_world] toosee `<Response>` элемент, содержащий `<Say>` элемента.)</span><span class="sxs-lookup"><span data-stu-id="2bcdf-184">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] toosee a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="2bcdf-185">Вместо hello Twilio предоставленный URL-адрес, можно создать собственного веб-сайта, который возвращает HTTP-ответов.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-185">Instead of relying on hello Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="2bcdf-186">Можно создать узел hello на любом языке, который возвращает XML-ответов; в этом разделе предполагается, что вы будете использовать PHP toocreate hello TwiML.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-186">You can create hello site in any language that returns XML responses; this topic assumes you'll be using PHP toocreate hello TwiML.</span></span>

<span data-ttu-id="2bcdf-187">Здравствуйте следующие результаты в виде страниц PHP в TwiML ответ, который говорит **Hello World** при вызове функции hello.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-187">hello following PHP page results in a TwiML response that says **Hello World** on hello call.</span></span>

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

<span data-ttu-id="2bcdf-188">Как видно в приведенном выше примере hello hello TwiML ответа является просто XML-документа.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-188">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="2bcdf-189">Библиотека Twilio Hello для PHP содержит классы, которые создают TwiML для вас.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-189">hello Twilio library for PHP contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="2bcdf-190">пример Hello ниже создает эквивалентный ответа hello, как показано выше, но использует hello **службы\_Twilio\_Twiml** класс библиотеки hello Twilio для PHP:</span><span class="sxs-lookup"><span data-stu-id="2bcdf-190">hello example below produces hello equivalent response as shown above, but uses hello **Services\_Twilio\_Twiml** class in hello Twilio library for PHP:</span></span>

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

<span data-ttu-id="2bcdf-191">Дополнительные сведения о TwiML см. по следующему адресу: [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="2bcdf-191">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span> 

<span data-ttu-id="2bcdf-192">При наличии на странице PHP, Настройка tooprovide TwiML ответов служит hello URL-адрес страницы PHP hello hello URL-адреса, переданные в hello `Services_Twilio->account->calls->create` метод.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-192">Once you have your PHP page set up tooprovide TwiML responses, use hello URL of hello PHP page as hello URL passed into hello  `Services_Twilio->account->calls->create`  method.</span></span> <span data-ttu-id="2bcdf-193">Например, если у вас есть веб-приложения с именем **MyTwiML** развернутой tooan Azure размещенной службы, а имя hello страницы приветствия PHP — **mytwiml.php**, URL-адрес может быть передан слишком hello **Services_ Twilio -> учетной записи вызовы "->" -> создать** как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="2bcdf-193">For example, if you have a Web application named **MyTwiML** deployed tooan Azure hosted service, and hello name of hello PHP page is **mytwiml.php**, hello URL can be passed too **Services_Twilio->account->calls->create**  as shown in hello following example:</span></span>

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

<span data-ttu-id="2bcdf-194">Дополнительные сведения об использовании Twilio в Azure с PHP см. в разделе [как tooMake Twilio с помощью телефонного звонка в приложения PHP в Azure][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="2bcdf-194">For additional information about using Twilio in Azure with PHP, see [How tooMake a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="2bcdf-195"><a id="AdditionalServices"></a>Руководство: использование дополнительных служб Twilio</span><span class="sxs-lookup"><span data-stu-id="2bcdf-195"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="2bcdf-196">В дополнение к этому toohello в этой статье примерах, Twilio предлагает веб-API, можно использовать дополнительные возможности Twilio tooleverage из приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-196">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="2bcdf-197">Дополнительные сведения см. в разделе hello [документации по Twilio API][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="2bcdf-197">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="2bcdf-198"><a id="NextSteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2bcdf-198"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="2bcdf-199">Теперь, когда вы узнали основы hello hello Twilio службы, выполните следующие дополнительные toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="2bcdf-199">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="2bcdf-200">[Рекомендации по безопасности Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="2bcdf-200">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="2bcdf-201">[Практические руководства по Twilio и примеры кода][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="2bcdf-201">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="2bcdf-202">[Краткие учебники по Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="2bcdf-202">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="2bcdf-203">[Twilio на GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="2bcdf-203">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="2bcdf-204">[Обращайтесь tooTwilio поддержки][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="2bcdf-204">[Talk tooTwilio Support][twilio_support]</span></span>

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
