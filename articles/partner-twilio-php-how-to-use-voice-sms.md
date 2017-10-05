---
title: "Использование Twilio для поддержки голосовых вызовов и SMS (PHP) | Документация Майкрософт"
description: "Узнайте, как осуществлять телефонные вызовы и отправку SMS-сообщений с помощью службы Twilio API в Azure. Примеры кода написаны на PHP."
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
ms.openlocfilehash: bd50eac7390e8639f77894689388e6926cdb619c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-php"></a><span data-ttu-id="e2fe3-104">Использование Twilio для поддержки голосовых возможностей и SMS в PHP</span><span class="sxs-lookup"><span data-stu-id="e2fe3-104">How to Use Twilio for Voice and SMS Capabilities in PHP</span></span>
<span data-ttu-id="e2fe3-105">В этом руководстве показано, как выполнять типовые задачи программирования с помощью службы Twilio API в Azure.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="e2fe3-106">Здесь описываются такие сценарии, как телефонный звонок и отправка SMS-сообщения.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="e2fe3-107">Дополнительные сведения о Twilio и использовании голосовых функций и SMS в приложениях см. в разделе [Дальнейшие действия](#NextSteps).</span><span class="sxs-lookup"><span data-stu-id="e2fe3-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="e2fe3-108"><a id="WhatIs"></a>Что такое Twilio?</span><span class="sxs-lookup"><span data-stu-id="e2fe3-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="e2fe3-109">Twilio создает новые возможности для бизнес-коммуникаций, позволяя разработчикам встраивать в приложения функции голосовой связи, VoIP и обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="e2fe3-110">Они виртуализируют всю необходимую инфраструктуру в облачной глобальной среде с предоставлением доступа через коммуникационную API платформу Twilio.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span></span> <span data-ttu-id="e2fe3-111">Приложения отличаются простотой создания и масштабирования.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-111">Applications are simple to build and scalable.</span></span> <span data-ttu-id="e2fe3-112">Оцените гибкость повременной оплаты, а также преимущества, связанные с надежностью облачных решений.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="e2fe3-113">**Twilio Voice** позволяет приложениям осуществлять и принимать телефонные вызовы.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-113">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="e2fe3-114">**Twilio SMS** позволяет приложениям отправлять и принимать текстовые сообщения.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-114">**Twilio SMS** enables your application to send and receive text messages.</span></span> <span data-ttu-id="e2fe3-115">**Twilio Client** позволяет выполнять VoIP звонки с любого телефона, планшета или из браузера, а также поддерживает WebRTC.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="e2fe3-116"><a id="Pricing"></a>Цены и специальные предложения Twilio</span><span class="sxs-lookup"><span data-stu-id="e2fe3-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="e2fe3-117">Клиентам Azure доступно [специальное предложение](http://www.twilio.com/azure): кредит Twilio в размере 10 долл. США при обновлении учетной записи Twilio.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="e2fe3-118">Этот кредит Twilio применяется к любым сценариям использования Twilio (кредит в размере 10 $ позволяет отправить 1000 SMS-сообщений или получать входящие голосовые вызовы продолжительностью до 1000 минут в зависимости от расположения телефонного номера, а также от направления отправки сообщения или совершения звонка).</span><span class="sxs-lookup"><span data-stu-id="e2fe3-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span></span> <span data-ttu-id="e2fe3-119">Получите этот кредит Twilio и приступите к работе на странице [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="e2fe3-119">Redeem this Twilio credit and get started at: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="e2fe3-120">Twilio представляет собой службу с повременной оплатой.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="e2fe3-121">Стартовые платежи отсутствуют, а учетную запись можно закрыть в любое время.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="e2fe3-122">Дополнительные сведения см. в статье [Цены на Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="e2fe3-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="e2fe3-123"><a id="Concepts"></a>Основные понятия</span><span class="sxs-lookup"><span data-stu-id="e2fe3-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="e2fe3-124">Twilio API — это интерфейс API RESTful, который предоставляет приложениям функции для работы с голосовыми вызовами и SMS.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="e2fe3-125">Полный список клиентских библиотек API Twilio, которые доступны на разных языках, см. на [этой странице][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="e2fe3-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="e2fe3-126">Основные аспекты Twilio API: команды Twilio и язык разметки Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="e2fe3-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="e2fe3-127"><a id="Verbs"></a>Команды Twilio</span><span class="sxs-lookup"><span data-stu-id="e2fe3-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="e2fe3-128">В API используются команды Twilio: например, команда **&lt;Say&gt;** указывает Twilio, что необходимо воспроизвести сообщение в случае вызова.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="e2fe3-129">Ниже приведен список команд Twilio.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-129">The following is a list of Twilio verbs.</span></span> <span data-ttu-id="e2fe3-130">Дополнительные сведения о других командах и возможностях см. в [документации по языку разметки Twilio](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="e2fe3-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="e2fe3-131">**&lt;Dial&gt;**: подключение вызывающего абонента к другому телефону.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="e2fe3-132">**&lt;Gather&gt;**: сбор цифр, введенных на клавиатуре телефона.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="e2fe3-133">**&lt;Hangup&gt;**: окончание вызова.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="e2fe3-134">**&lt;Play&gt;**: воспроизведение звукового файла.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="e2fe3-135">**&lt;Pause&gt;**: бесшумное ожидание в течение указанного времени (в секундах).</span><span class="sxs-lookup"><span data-stu-id="e2fe3-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="e2fe3-136">**&lt;Record&gt;**: запись голоса вызывающего абонента и возврат URL-адреса файла, содержащего запись.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-136">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="e2fe3-137">**&lt;Redirect&gt;**: передача управления для вызова или SMS в TwiML по другому URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="e2fe3-138">**&lt;Reject&gt;**: отклонение входящего вызова на ваш номер Twilio без выставления счета.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-138">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="e2fe3-139">**&lt;Say&gt;**: преобразование текста в речь при вызове.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-139">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="e2fe3-140">**&lt;Sms&gt;**: отправка SMS-сообщения.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="e2fe3-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="e2fe3-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="e2fe3-142">TwiML — это набор инструкций на основе XML и с использованием команд Twilio, которые сообщают службе Twilio, как необходимо обработать вызов или SMS.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-142">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="e2fe3-143">Например, следующие инструкции TwiML преобразуют текст **Hello World** в речь.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-143">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="e2fe3-144">Когда приложение вызывает Twilio API, одним из параметров API является URL-адрес, который возвращает ответ TwiML.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-144">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="e2fe3-145">Для целей разработки можно использовать URL-адреса из Twilio для предоставления ответов TwiML, используемых приложениями.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-145">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="e2fe3-146">Также может разместить свои собственные URL-адреса для получения ответов TwiML; другой вариант — использовать объект **TwiMLResponse** .</span><span class="sxs-lookup"><span data-stu-id="e2fe3-146">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="e2fe3-147">Дополнительные сведения о командах Twilio, их атрибутах и TwiML см. на странице [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="e2fe3-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="e2fe3-148">Дополнительные сведения об API Twilio см. на [этой странице][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="e2fe3-148">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="e2fe3-149"><a id="CreateAccount"></a>Создание учетной записи Twilio</span><span class="sxs-lookup"><span data-stu-id="e2fe3-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="e2fe3-150">После подготовки к получению учетной записи Twilio зарегистрируйтесь на [странице получения пробной версии Twilio ][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="e2fe3-150">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="e2fe3-151">Вы можете начать с бесплатной учетной записи и обновить ее позднее.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="e2fe3-152">При регистрации учетной записи Twilio, вы получите идентификатор учетной записи и маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="e2fe3-153">Эти элементы необходимы для вызовов Twilio API.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-153">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="e2fe3-154">Чтобы предотвратить несанкционированный доступ к учетной записи, храните маркер проверки подлинности в безопасности.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-154">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="e2fe3-155">Идентификатор учетной записи и маркер аутентификации отображаются на [странице учетной записи Twilio][twilio_account] в полях **ACCOUNT SID** (Идентификатор безопасности учетной записи) и **AUTH TOKEN** (Маркер аутентификации) соответственно.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-155">Your account ID and authentication token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="e2fe3-156"><a id="create_app"></a>Создание приложения PHP</span><span class="sxs-lookup"><span data-stu-id="e2fe3-156"><a id="create_app"></a>Create a PHP Application</span></span>
<span data-ttu-id="e2fe3-157">Приложение PHP, которое использует службу Twilio и выполняется в Azure, не отличается от других приложений PHP, которые используют службу Twilio.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-157">A PHP application that uses the Twilio service and is running in Azure is no different than any other PHP application that uses the Twilio service.</span></span> <span data-ttu-id="e2fe3-158">Хотя Twilio служб на основе REST и может вызываться из PHP несколькими способами, в этой статье основное внимание уделяется использование Twilio служб с [Twilio библиотеки для PHP с сайта GitHub][twilio_php].</span><span class="sxs-lookup"><span data-stu-id="e2fe3-158">While Twilio services are REST-based and can be called from PHP in several ways, this article will focus on how to use Twilio services with [Twilio library for PHP from GitHub][twilio_php].</span></span> <span data-ttu-id="e2fe3-159">Дополнительные сведения об использовании библиотеки Twilio для PHP см. в разделе [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="e2fe3-159">For more information about using the Twilio library for PHP, see [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="e2fe3-160">Подробные инструкции для создания и развертывания приложения Twilio и PHP в Azure можно найти по адресу [как сделать приложения PHP в Azure с помощью вызова Twilio телефонный звонок][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="e2fe3-160">Detailed instructions for building and deploying a Twilio/PHP application to Azure are available at [How to Make a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="e2fe3-161"><a id="configure_app"></a>Настройка приложения для использования библиотек Twilio</span><span class="sxs-lookup"><span data-stu-id="e2fe3-161"><a id="configure_app"></a>Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="e2fe3-162">Настройку приложения для работы с библиотекой Twilio для PHP можно выполнить двумя способами:</span><span class="sxs-lookup"><span data-stu-id="e2fe3-162">You can configure your application to use the Twilio library for PHP in two ways:</span></span>

1. <span data-ttu-id="e2fe3-163">Загрузить библиотеку Twilio для PHP с сайта GitHub ([https://github.com/twilio/twilio-php][twilio_php]) и добавьте **служб** каталог для приложения.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-163">Download the Twilio library for PHP from GitHub ([https://github.com/twilio/twilio-php][twilio_php]) and add the **Services** directory to your application.</span></span>
   
    <span data-ttu-id="e2fe3-164">-ИЛИ-</span><span class="sxs-lookup"><span data-stu-id="e2fe3-164">-OR-</span></span>
2. <span data-ttu-id="e2fe3-165">Установите библиотеку Twilio для PHP в виде пакета PEAR.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-165">Install the Twilio library for PHP as a PEAR package.</span></span> <span data-ttu-id="e2fe3-166">Для установки можно использовать следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e2fe3-166">It can be installed with the following commands:</span></span>
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

<span data-ttu-id="e2fe3-167">После установки библиотеки Twilio для PHP вы можете добавлять в начало PHP-файлов инструкцию **require_once**, задающую ссылку на эту библиотеку:</span><span class="sxs-lookup"><span data-stu-id="e2fe3-167">Once you have installed the Twilio library for PHP, you can then add a **require_once** statement at the top of your PHP files to reference the library:</span></span>

        require_once 'Services/Twilio.php';

<span data-ttu-id="e2fe3-168">Дополнительные сведения см. в разделе [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="e2fe3-168">For more information, see [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="e2fe3-169"><a id="howto_make_call"></a>Практическое руководство. Осуществление исходящего вызова</span><span class="sxs-lookup"><span data-stu-id="e2fe3-169"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="e2fe3-170">Ниже показано, как осуществлять исходящий вызов с использованием класса **Services_Twilio**.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-170">The following shows how to make an outgoing call using the **Services_Twilio** class.</span></span> <span data-ttu-id="e2fe3-171">Этот код также использует сайт из Twilio для выдачи ответа на языке разметки Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="e2fe3-171">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="e2fe3-172">Замените значения телефонных номеров **From** (От) и **To** (Кому) и проверьте номер телефона **From** (От) для учетной записи Twilio до выполнения кода.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-172">Substitute your values for the **From** and **To** phone numbers, and ensure that you verify the **From** phone number for your Twilio account prior to running the code.</span></span>

    // Include the Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";

    // The number of the phone initiating the the call.
    $from_number = "NNNNNNNNNNN";

    // The number of the phone receiving call.
    $to_number = "NNNNNNNNNNN";

    // Use the Twilio-provided site for the TwiML response.
    $url = "http://twimlets.com/message";

    // The phone message text.
    $message = "Hello world.";

    // Create the call client.
    $client = new Services_Twilio($sid, $token, $version);

    //Make the call.
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

<span data-ttu-id="e2fe3-173">Как уже упоминалось, этот код также использует сайт из Twilio для выдачи ответа на языке TwiML.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-173">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="e2fe3-174">Можно использовать собственный веб-сайт для предоставления ответа TwiML; дополнительные сведения содержатся в разделе [Предоставление ответов TwiML с собственного веб-сайта](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="e2fe3-174">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

* <span data-ttu-id="e2fe3-175">**Примечание**: сведения об устранении ошибки проверки сертификатов SSL см [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span><span class="sxs-lookup"><span data-stu-id="e2fe3-175">**Note**: To troubleshoot SSL certificate validation errors, see [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span></span> 

## <span data-ttu-id="e2fe3-176"><a id="howto_send_sms"></a>Практическое руководство. Отправка SMS-сообщения</span><span class="sxs-lookup"><span data-stu-id="e2fe3-176"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="e2fe3-177">Ниже показано, как отправить SMS-сообщение с использованием класса **Services_Twilio**.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-177">The following shows how to send an SMS message using the **Services_Twilio** class.</span></span> <span data-ttu-id="e2fe3-178">С целью отправки SMS-сообщений для пробных учетных записей номер **From** (От) предоставляется Twilio.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-178">The **From** number is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="e2fe3-179">Номер **To** (Кому) для учетной записи Twilio необходимо проверить перед выполнением кода.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-179">The **To** number must be verified for your Twilio account prior to running the code.</span></span>

    // Include the Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";


    $from_number = "NNNNNNNNNNN"; // With trial account, texts can only be sent from your Twilio number.
    $to_number = "NNNNNNNNNNN";
    $message = "Hello world.";

    // Create the call client.
    $client = new Services_Twilio($sid, $token, $version);

    // Send the SMS message.
    try
    {
        $client->$client->account->messages->sendMessage($from_number, $to_number, $message);
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

## <span data-ttu-id="e2fe3-180"><a id="howto_provide_twiml_responses"></a>Практическое руководство. Предоставление ответов TwiML с собственного веб-сайта</span><span class="sxs-lookup"><span data-stu-id="e2fe3-180"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="e2fe3-181">Когда приложение инициирует вызов API Twilio, Twilio отправляет ваш запрос на URL-адрес, который должен возвратить ответ TwiML.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-181">When your application initiates a call to the Twilio API, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="e2fe3-182">В примере выше используется предоставляемый Twilio URL-адрес [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="e2fe3-182">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="e2fe3-183">(Хотя TwiML предназначается для использования службой Twilio, его можно также просмотреть в браузере.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-183">(While TwiML is designed for use by Twilio, you can view the it in your browser.</span></span> <span data-ttu-id="e2fe3-184">Например, щелкните [http://twimlets.com/message][twimlet_message_url] для просмотра пустого элемента `<Response>`; в качестве другого примера щелкните [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] для просмотра элемента `<Response>`, содержащего элемент `<Say>`.)</span><span class="sxs-lookup"><span data-stu-id="e2fe3-184">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] to see a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="e2fe3-185">Вместо того чтобы использовать URL-адрес, предоставленный Twilio, можно создать собственный сайт для возврата HTTP-ответов.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-185">Instead of relying on the Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="e2fe3-186">Веб-сайт можно создавать на любом языке, который возвращает XML-ответы; в этом разделе предполагается, что для создания TwiML будет использоваться язык PHP.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-186">You can create the site in any language that returns XML responses; this topic assumes you'll be using PHP to create the TwiML.</span></span>

<span data-ttu-id="e2fe3-187">Следующая страница PHP создает ответ TwiML **Hello World** на вызов.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-187">The following PHP page results in a TwiML response that says **Hello World** on the call.</span></span>

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

<span data-ttu-id="e2fe3-188">Как видно из приведенного выше примера, ответ TwiML будет представлять собой простой XML-документ.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-188">As you can see from the example above, the TwiML response is simply an XML document.</span></span> <span data-ttu-id="e2fe3-189">Библиотека Twilio для PHP содержит классы, которые создадут для вас TwiML.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-189">The Twilio library for PHP contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="e2fe3-190">В следующем примере возвращается аналогичный предыдущему ответ, однако используется класс **Services\_Twilio\_Twiml** из библиотеки Twilio для PHP:</span><span class="sxs-lookup"><span data-stu-id="e2fe3-190">The example below produces the equivalent response as shown above, but uses the **Services\_Twilio\_Twiml** class in the Twilio library for PHP:</span></span>

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

<span data-ttu-id="e2fe3-191">Дополнительные сведения о TwiML см. по следующему адресу: [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="e2fe3-191">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span> 

<span data-ttu-id="e2fe3-192">После настройки PHP-страницы для предоставления ответов TwiML используйте URL-адрес PHP-страницы как URL-адрес, передаваемый в метод `Services_Twilio->account->calls->create`.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-192">Once you have your PHP page set up to provide TwiML responses, use the URL of the PHP page as the URL passed into the  `Services_Twilio->account->calls->create`  method.</span></span> <span data-ttu-id="e2fe3-193">Например, если у вас есть веб-приложение с именем **MyTwiML**, развернутое в размещенной службе Azure, а PHP-страница использует имя **mytwiml.php**, URL-адрес можно передать в класс **Services_Twilio->account->calls->create**, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="e2fe3-193">For example, if you have a Web application named **MyTwiML** deployed to an Azure hosted service, and the name of the PHP page is **mytwiml.php**, the URL can be passed to  **Services_Twilio->account->calls->create**  as shown in the following example:</span></span>

    require_once 'Services/Twilio.php';

    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";
    $from_number = "NNNNNNNNNNN";
    $to_number = "NNNNNNNNNNN";
    $url = "http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.php";

    // The phone message text.
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

<span data-ttu-id="e2fe3-194">Дополнительные сведения об использовании Twilio в Azure с PHP см. в разделе [как сделать приложения PHP в Azure с помощью вызова Twilio телефонный звонок][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="e2fe3-194">For additional information about using Twilio in Azure with PHP, see [How to Make a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="e2fe3-195"><a id="AdditionalServices"></a>Руководство: использование дополнительных служб Twilio</span><span class="sxs-lookup"><span data-stu-id="e2fe3-195"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="e2fe3-196">В дополнение к приведенным примерам, Twilio предлагает веб-интерфейсы API для использования дополнительных функций Twilio в вашем приложении Azure.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-196">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="e2fe3-197">Дополнительные сведения см. в [документации по интерфейсу API Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="e2fe3-197">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="e2fe3-198"><a id="NextSteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e2fe3-198"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="e2fe3-199">Вы узнали основные сведения о службе Twilio. Для получения дополнительных сведений используйте следующие ссылки.</span><span class="sxs-lookup"><span data-stu-id="e2fe3-199">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="e2fe3-200">[Рекомендации по безопасности Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="e2fe3-200">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="e2fe3-201">[Практические руководства по Twilio и примеры кода][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="e2fe3-201">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="e2fe3-202">[Краткие учебники по Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="e2fe3-202">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="e2fe3-203">[Twilio на GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="e2fe3-203">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="e2fe3-204">[Обращение в службу поддержки Twilio][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="e2fe3-204">[Talk to Twilio Support][twilio_support]</span></span>

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
