---
title: "Использование Twilio для поддержки голосовых вызовов и SMS (Ruby) | Документация Майкрософт"
description: "Узнайте, как осуществлять телефонные вызовы и отправку SMS-сообщений с помощью службы Twilio API в Azure. Примеры кода написаны на Ruby."
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
ms.openlocfilehash: 69e50e7fe0e1f302e96c309878b8dea6869dff4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-ruby"></a><span data-ttu-id="d6adc-104">Использование Twilio для поддержки голосовых возможностей и SMS в Ruby</span><span class="sxs-lookup"><span data-stu-id="d6adc-104">How to Use Twilio for Voice and SMS Capabilities in Ruby</span></span>
<span data-ttu-id="d6adc-105">В этом руководстве показано, как выполнять типовые задачи программирования с помощью службы Twilio API в Azure.</span><span class="sxs-lookup"><span data-stu-id="d6adc-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="d6adc-106">Здесь описываются такие сценарии, как телефонный звонок и отправка SMS-сообщения.</span><span class="sxs-lookup"><span data-stu-id="d6adc-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="d6adc-107">Дополнительные сведения о Twilio и использовании голосовых функций и SMS в приложениях см. в разделе [Дальнейшие действия](#NextSteps).</span><span class="sxs-lookup"><span data-stu-id="d6adc-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="d6adc-108"><a id="WhatIs"></a>Что такое Twilio?</span><span class="sxs-lookup"><span data-stu-id="d6adc-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="d6adc-109">Twilio — это API веб-службы телефонии, позволяющий использовать существующие языки веб-программирования и навыки для создания приложений для работы с голосовыми вызовами и SMS.</span><span class="sxs-lookup"><span data-stu-id="d6adc-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills to build voice and SMS applications.</span></span> <span data-ttu-id="d6adc-110">Twilio — это сторонняя служба (не компонент Azure и не продукт Майкрософт).</span><span class="sxs-lookup"><span data-stu-id="d6adc-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="d6adc-111">**Twilio Voice** позволяет приложениям осуществлять и принимать телефонные вызовы.</span><span class="sxs-lookup"><span data-stu-id="d6adc-111">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="d6adc-112">**Twilio SMS** позволяет приложениям отправлять и принимать SMS-сообщения.</span><span class="sxs-lookup"><span data-stu-id="d6adc-112">**Twilio SMS** allows your applications to make and receive SMS messages.</span></span> <span data-ttu-id="d6adc-113">**Twilio Client** позволяет приложениям реализовать речевую связь с помощью существующих интернет-подключений, в том числе на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="d6adc-113">**Twilio Client** allows your applications to enable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="d6adc-114"><a id="Pricing"></a>Цены и специальные предложения Twilio</span><span class="sxs-lookup"><span data-stu-id="d6adc-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="d6adc-115">Сведения о ценах на Twilio доступны на веб-сайте [цен на Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="d6adc-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="d6adc-116">Клиентам Azure доступно [специальное предложение][special_offer]: бесплатный кредит на 1000 текстовых сообщений или 1000 минут входящих вызовов.</span><span class="sxs-lookup"><span data-stu-id="d6adc-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="d6adc-117">Чтобы воспользоваться этим предложением или получить дополнительные сведения, посетите сайт [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="d6adc-117">To sign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>  

## <span data-ttu-id="d6adc-118"><a id="Concepts"></a>Основные понятия</span><span class="sxs-lookup"><span data-stu-id="d6adc-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="d6adc-119">Twilio API — это интерфейс API RESTful, который предоставляет приложениям функции для работы с голосовыми вызовами и SMS.</span><span class="sxs-lookup"><span data-stu-id="d6adc-119">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="d6adc-120">Полный список клиентских библиотек API Twilio, которые доступны на разных языках, см. на [этой странице][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="d6adc-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

### <span data-ttu-id="d6adc-121"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="d6adc-121"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="d6adc-122">TwiML — это набор инструкций на основе XML, которые сообщают службе Twilio, как необходимо обработать вызов или SMS.</span><span class="sxs-lookup"><span data-stu-id="d6adc-122">TwiML is a set of XML-based instructions that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="d6adc-123">Например, следующие инструкции TwiML преобразуют текст **Hello World** в речь.</span><span class="sxs-lookup"><span data-stu-id="d6adc-123">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="d6adc-124">Во всех документах TwiML элемент `<Response>` является корневым.</span><span class="sxs-lookup"><span data-stu-id="d6adc-124">All TwiML documents have `<Response>` as their root element.</span></span> <span data-ttu-id="d6adc-125">Вы будете использовать команды Twilio для определения поведения приложения.</span><span class="sxs-lookup"><span data-stu-id="d6adc-125">From there, you use Twilio Verbs to define the behavior of your application.</span></span>

### <span data-ttu-id="d6adc-126"><a id="Verbs"></a>Команды TwiML</span><span class="sxs-lookup"><span data-stu-id="d6adc-126"><a id="Verbs"></a>TwiML Verbs</span></span>
<span data-ttu-id="d6adc-127">Команды Twilio — это XML-теги, сообщающие Twilio, что **делать**.</span><span class="sxs-lookup"><span data-stu-id="d6adc-127">Twilio Verbs are XML tags that tell Twilio what to **do**.</span></span> <span data-ttu-id="d6adc-128">Например, команда **&lt;Say&gt;** указывает Twilio, что необходимо воспроизвести сообщение в случае вызова.</span><span class="sxs-lookup"><span data-stu-id="d6adc-128">For example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span> 

<span data-ttu-id="d6adc-129">Ниже приведен список команд Twilio.</span><span class="sxs-lookup"><span data-stu-id="d6adc-129">The following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="d6adc-130">**&lt;Dial&gt;**: подключение вызывающего абонента к другому телефону.</span><span class="sxs-lookup"><span data-stu-id="d6adc-130">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="d6adc-131">**&lt;Gather&gt;**: сбор цифр, введенных на клавиатуре телефона.</span><span class="sxs-lookup"><span data-stu-id="d6adc-131">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="d6adc-132">**&lt;Hangup&gt;**: окончание вызова.</span><span class="sxs-lookup"><span data-stu-id="d6adc-132">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="d6adc-133">**&lt;Play&gt;**: воспроизведение звукового файла.</span><span class="sxs-lookup"><span data-stu-id="d6adc-133">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="d6adc-134">**&lt;Pause&gt;**: бесшумное ожидание в течение указанного времени (в секундах).</span><span class="sxs-lookup"><span data-stu-id="d6adc-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="d6adc-135">**&lt;Record&gt;**: запись голоса вызывающего абонента и возврат URL-адреса файла, содержащего запись.</span><span class="sxs-lookup"><span data-stu-id="d6adc-135">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="d6adc-136">**&lt;Redirect&gt;**: передача управления для вызова или SMS в TwiML по другому URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="d6adc-136">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="d6adc-137">**&lt;Reject&gt;**: отклонение входящего вызова на ваш номер Twilio без выставления счета.</span><span class="sxs-lookup"><span data-stu-id="d6adc-137">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="d6adc-138">**&lt;Say&gt;**: преобразование текста в речь при вызове.</span><span class="sxs-lookup"><span data-stu-id="d6adc-138">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="d6adc-139">**&lt;Sms&gt;**: отправка SMS-сообщения.</span><span class="sxs-lookup"><span data-stu-id="d6adc-139">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

<span data-ttu-id="d6adc-140">Дополнительные сведения о командах Twilio, их атрибутах и TwiML см. на странице [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="d6adc-140">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="d6adc-141">Дополнительные сведения об API Twilio см. на [этой странице][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="d6adc-141">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="d6adc-142"><a id="CreateAccount"></a>Создание учетной записи Twilio</span><span class="sxs-lookup"><span data-stu-id="d6adc-142"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="d6adc-143">После подготовки к получению учетной записи Twilio зарегистрируйтесь на [странице получения пробной версии Twilio ][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="d6adc-143">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="d6adc-144">Вы можете начать с бесплатной учетной записи и обновить ее позднее.</span><span class="sxs-lookup"><span data-stu-id="d6adc-144">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="d6adc-145">После регистрации учетной записи Twilio вы получите бесплатный номер телефона для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="d6adc-145">When you sign up for a Twilio account, you'll get a free phone number for your application.</span></span> <span data-ttu-id="d6adc-146">Вы также получите идентификатор безопасности учетной записи и маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="d6adc-146">You'll also receive an account SID and an auth token.</span></span> <span data-ttu-id="d6adc-147">Эти элементы необходимы для вызовов Twilio API.</span><span class="sxs-lookup"><span data-stu-id="d6adc-147">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="d6adc-148">Чтобы предотвратить несанкционированный доступ к учетной записи, храните маркер проверки подлинности в безопасности.</span><span class="sxs-lookup"><span data-stu-id="d6adc-148">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="d6adc-149">Идентификатор безопасности учетной записи и маркер проверки подлинности отображаются на [странице учетной записи Twilio][twilio_account] в полях **ACCOUNT SID** (Идентификатор безопасности учетной записи) и **AUTH TOKEN** (Маркер проверки подлинности) соответственно.</span><span class="sxs-lookup"><span data-stu-id="d6adc-149">Your account SID and auth token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

### <span data-ttu-id="d6adc-150"><a id="VerifyPhoneNumbers"></a>Проверка телефонных номеров</span><span class="sxs-lookup"><span data-stu-id="d6adc-150"><a id="VerifyPhoneNumbers"></a>Verify Phone Numbers</span></span>
<span data-ttu-id="d6adc-151">В дополнение к номеру, предоставленному Twilio, вы также можете проверить номера, которыми вы управляете (например, номер сотового или домашнего телефона), для использования в приложениях.</span><span class="sxs-lookup"><span data-stu-id="d6adc-151">In addition to the number you are given by Twilio, you can also verify numbers that you control (i.e. your cell phone or home phone number) for use in your applications.</span></span> 

<span data-ttu-id="d6adc-152">Сведения о проверке номера телефона см. на [этой странице][verify_phone].</span><span class="sxs-lookup"><span data-stu-id="d6adc-152">For information on how to verify a phone number, see [Manage Numbers][verify_phone].</span></span>

## <span data-ttu-id="d6adc-153"><a id="create_app"></a>Создание приложения Ruby</span><span class="sxs-lookup"><span data-stu-id="d6adc-153"><a id="create_app"></a>Create a Ruby Application</span></span>
<span data-ttu-id="d6adc-154">Приложение Ruby, которое использует службу Twilio и выполняется в Azure, не отличается от других приложений Ruby, которые используют службу Twilio.</span><span class="sxs-lookup"><span data-stu-id="d6adc-154">A Ruby application that uses the Twilio service and is running in Azure is no different than any other Ruby application that uses the Twilio service.</span></span> <span data-ttu-id="d6adc-155">Хотя службы Twilio поддерживают REST и могут вызываться из Ruby несколькими способами, в этой статье основное внимание уделяется использованию служб Twilio со [вспомогательной библиотекой Twilio для Ruby][twilio_ruby].</span><span class="sxs-lookup"><span data-stu-id="d6adc-155">While Twilio services are RESTful and can be called from Ruby in several ways, this article will focus on how to use Twilio services with [Twilio helper library for Ruby][twilio_ruby].</span></span>

<span data-ttu-id="d6adc-156">Сначала [установите новую виртуальную машину Linux Azure][azure_vm_setup] в качестве узла для нового веб-приложения Ruby.</span><span class="sxs-lookup"><span data-stu-id="d6adc-156">First, [set-up a new Azure Linux VM][azure_vm_setup] to act as a host for your new Ruby web application.</span></span> <span data-ttu-id="d6adc-157">Игнорируйте инструкции, связанные с созданием приложения Rails, достаточно настроить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="d6adc-157">Ignore the steps involving the creation of a Rails app, just set-up the VM.</span></span> <span data-ttu-id="d6adc-158">Обязательно создайте конечную точку с внешним портом 80 и внутренним портом 5000.</span><span class="sxs-lookup"><span data-stu-id="d6adc-158">Make sure you create an Endpoint with an external port of 80 and an internal port of 5000.</span></span>

<span data-ttu-id="d6adc-159">В примерах ниже мы будем использовать [Sinatra][sinatra] — очень простую веб-платформу для Ruby.</span><span class="sxs-lookup"><span data-stu-id="d6adc-159">In the examples below, we will be using [Sinatra][sinatra], a very simple web framework for Ruby.</span></span> <span data-ttu-id="d6adc-160">Однако вы можете использовать вспомогательную библиотеку Twilio для Ruby с любой другой веб-платформой, в том числе Ruby on Rails.</span><span class="sxs-lookup"><span data-stu-id="d6adc-160">But you can certainly use the Twilio helper library for Ruby with any other web framework, including Ruby on Rails.</span></span>

<span data-ttu-id="d6adc-161">Войдите на новую виртуальную машину по протоколу SSH и создайте каталог для нового приложения.</span><span class="sxs-lookup"><span data-stu-id="d6adc-161">SSH into your new VM and create a directory for your new app.</span></span> <span data-ttu-id="d6adc-162">В этом каталоге создайте файл с именем Gemfile и скопируйте в него следующий код:</span><span class="sxs-lookup"><span data-stu-id="d6adc-162">Inside that directory, create a file called Gemfile and copy the following code into it:</span></span>

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

<span data-ttu-id="d6adc-163">В командной строке запустите `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="d6adc-163">On the command line run `bundle install`.</span></span> <span data-ttu-id="d6adc-164">Эта команда установит описанные выше зависимости.</span><span class="sxs-lookup"><span data-stu-id="d6adc-164">This will install the dependencies above.</span></span> <span data-ttu-id="d6adc-165">Затем создайте файл с именем `web.rb`.</span><span class="sxs-lookup"><span data-stu-id="d6adc-165">Next create a file called `web.rb`.</span></span> <span data-ttu-id="d6adc-166">В нем будет размещен код веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="d6adc-166">This will be where the code for your web app lives.</span></span> <span data-ttu-id="d6adc-167">Вставьте в него следующий код:</span><span class="sxs-lookup"><span data-stu-id="d6adc-167">Paste the following code into it:</span></span>

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

<span data-ttu-id="d6adc-168">На этом этапе можно будет выполнить команду `ruby web.rb -p 5000`.</span><span class="sxs-lookup"><span data-stu-id="d6adc-168">At this point you should be able the run the command `ruby web.rb -p 5000`.</span></span> <span data-ttu-id="d6adc-169">Она настроит небольшой веб-сервер с портом 5000.</span><span class="sxs-lookup"><span data-stu-id="d6adc-169">This will spin-up a small web server on port 5000.</span></span> <span data-ttu-id="d6adc-170">Вы сможете просмотреть приложение в браузере, перейдя по URL-адресу, настроенному для виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="d6adc-170">You should be able to browse to this app in your browser by visiting the URL you set-up for your Azure VM.</span></span> <span data-ttu-id="d6adc-171">После открытия веб-приложения в браузере вы готовы к созданию приложения Twilio.</span><span class="sxs-lookup"><span data-stu-id="d6adc-171">Once you can reach your web app in the browser, you're ready to start building a Twilio app.</span></span>

## <span data-ttu-id="d6adc-172"><a id="configure_app"></a>Настройка приложения для использования Twilio</span><span class="sxs-lookup"><span data-stu-id="d6adc-172"><a id="configure_app"></a>Configure Your Application to Use Twilio</span></span>
<span data-ttu-id="d6adc-173">Можно настроить веб-приложение для использования библиотеки Twilio, добавив к `Gemfile` следующую строку:</span><span class="sxs-lookup"><span data-stu-id="d6adc-173">You can configure your web app to use the Twilio library by updating your `Gemfile` to include this line:</span></span>

    gem 'twilio-ruby'

<span data-ttu-id="d6adc-174">В командной строке запустите `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="d6adc-174">On the command line, run `bundle install`.</span></span> <span data-ttu-id="d6adc-175">Теперь откройте `web.rb` и следующую строку в начале:</span><span class="sxs-lookup"><span data-stu-id="d6adc-175">Now open `web.rb` and including this line at the top:</span></span>

    require 'twilio-ruby'

<span data-ttu-id="d6adc-176">Теперь вы готовы к использованию вспомогательной библиотеки Twilio для Ruby в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="d6adc-176">You're now all set to use the Twilio helper library for Ruby in your web app.</span></span>

## <span data-ttu-id="d6adc-177"><a id="howto_make_call"></a>Практическое руководство. Осуществление исходящего вызова</span><span class="sxs-lookup"><span data-stu-id="d6adc-177"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="d6adc-178">Далее показано, как осуществлять исходящий вызов.</span><span class="sxs-lookup"><span data-stu-id="d6adc-178">The following shows how to make an outgoing call.</span></span> <span data-ttu-id="d6adc-179">К основным понятиям относятся использование вспомогательной библиотеки Twilio для Ruby для вызова API REST и отрисовки TwiML.</span><span class="sxs-lookup"><span data-stu-id="d6adc-179">Key concepts include using the Twilio helper library for Ruby to make REST API calls and rendering TwiML.</span></span> <span data-ttu-id="d6adc-180">Замените значения телефонных номеров **From** (От) и **To** (Кому) и проверьте номер телефона **From** (От) для учетной записи Twilio до выполнения кода.</span><span class="sxs-lookup"><span data-stu-id="d6adc-180">Substitute your values for the **From** and **To** phone numbers, and ensure that you verify the **From** phone number for your Twilio account prior to running the code.</span></span>

<span data-ttu-id="d6adc-181">Добавьте эту функцию в `web.md`:</span><span class="sxs-lookup"><span data-stu-id="d6adc-181">Add this function to `web.md`:</span></span>

    # Set your account ID and authentication token.
    sid = "your_twilio_account_sid";
    token = "your_twilio_authentication_token";

    # The number of the phone initiating the the call.
    # This should either be a Twilio number or a number that you've verified
    from = "NNNNNNNNNNN";

    # The number of the phone receiving call.
    to = "NNNNNNNNNNN";

    # Use the Twilio-provided site for the TwiML response.
    url = "http://yourdomain.cloudapp.net/voice_url";

    get '/make_call' do
      # Create the call client.
      client = Twilio::REST::Client.new(sid, token);

      # Make the call
      client.account.calls.create(to: to, from: from, url: url)
    end

    post '/voice_url' do
      "<Response>
         <Say>Hello Monkey!</Say>
       </Response>"
    end

<span data-ttu-id="d6adc-182">Если открыть `http://yourdomain.cloudapp.net/make_call` в браузере, вы активируете вызов API Twilio для осуществления звонка.</span><span class="sxs-lookup"><span data-stu-id="d6adc-182">If you open-up `http://yourdomain.cloudapp.net/make_call` in a browser, that will trigger the call to the Twilio API to make the phone call.</span></span> <span data-ttu-id="d6adc-183">Первые два параметра в `client.account.calls.create` говорят сами за себя: номер вызова `from` и номер вызова `to`.</span><span class="sxs-lookup"><span data-stu-id="d6adc-183">The first two parameters in `client.account.calls.create` are fairly self-explanatory: the number the call is `from` and the number the call is `to`.</span></span> 

<span data-ttu-id="d6adc-184">Третий параметр (`url`) — URL-адрес, который Twilio запрашивает для получения инструкций по действиям после подключения вызова.</span><span class="sxs-lookup"><span data-stu-id="d6adc-184">The third parameter (`url`) is the URL that Twilio requests to get instructions on what to do once the call is connected.</span></span> <span data-ttu-id="d6adc-185">В этом случае мы задаем URL-адрес (`http://yourdomain.cloudapp.net`), который возвращает простой документ TwiML и использует команду `<Say>`, чтобы преобразовать текст в речь и сказать "Hello Monkey" для принимающего вызов абонента.</span><span class="sxs-lookup"><span data-stu-id="d6adc-185">In this case we set-up a URL (`http://yourdomain.cloudapp.net`) that returns a simple TwiML document and uses the `<Say>` verb to do some text-to-speech and say "Hello Monkey" to the person recieving the call.</span></span>

## <span data-ttu-id="d6adc-186"><a id="howto_recieve_sms"></a>Руководство: получение SMS-сообщения</span><span class="sxs-lookup"><span data-stu-id="d6adc-186"><a id="howto_recieve_sms"></a>How to: Recieve an SMS message</span></span>
<span data-ttu-id="d6adc-187">В предыдущем примере мы инициировали **исходящий** звонок.</span><span class="sxs-lookup"><span data-stu-id="d6adc-187">In the previous example we initiated an **outgoing** phone call.</span></span> <span data-ttu-id="d6adc-188">На этот раз мы используем номер телефона, предоставленный Twilio во время регистрации, для обработки **входящего** SMS-сообщения.</span><span class="sxs-lookup"><span data-stu-id="d6adc-188">This time, let's use the phone number that Twilio gave us during sign-up to process an **incoming** SMS message.</span></span>

<span data-ttu-id="d6adc-189">Сначала войдите на [панель мониторинга Twilio][twilio_account].</span><span class="sxs-lookup"><span data-stu-id="d6adc-189">First, log-in to your [Twilio dashboard][twilio_account].</span></span> <span data-ttu-id="d6adc-190">Щелкните "Номера" на верхней панели навигации и выберите предоставленный вам номер Twilio.</span><span class="sxs-lookup"><span data-stu-id="d6adc-190">Click on "Numbers" in the top nav and then click on the Twilio number you were provided.</span></span> <span data-ttu-id="d6adc-191">Вы увидите два URL-адреса, которые можно настроить:</span><span class="sxs-lookup"><span data-stu-id="d6adc-191">You'll see two URLs that you can configure.</span></span> <span data-ttu-id="d6adc-192">URL-адрес запроса голосового вызова и URL-адрес запроса SMS.</span><span class="sxs-lookup"><span data-stu-id="d6adc-192">A Voice Request URL and an SMS Request URL.</span></span> <span data-ttu-id="d6adc-193">Эти URL-адреса используются Twilio при осуществлении голосового вызова или отправке SMS-сообщения на ваш номер.</span><span class="sxs-lookup"><span data-stu-id="d6adc-193">These are the URLs that Twilio calls whenever a phone call is made or an SMS is sent to your number.</span></span> <span data-ttu-id="d6adc-194">Эти адреса также называют "веб-привязками".</span><span class="sxs-lookup"><span data-stu-id="d6adc-194">The URLs are also known as "web hooks".</span></span>

<span data-ttu-id="d6adc-195">Мы хотели бы обработать входящие SMS-сообщения, поэтому изменим URL-адрес на `http://yourdomain.cloudapp.net/sms_url`.</span><span class="sxs-lookup"><span data-stu-id="d6adc-195">We would like to process incoming SMS messages, so let's update the URL to `http://yourdomain.cloudapp.net/sms_url`.</span></span> <span data-ttu-id="d6adc-196">Нажмите кнопку "Сохранить изменения" в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="d6adc-196">Go ahead and click Save Changes at the bottom of the page.</span></span> <span data-ttu-id="d6adc-197">Теперь вернемся к `web.rb` и напишем код, чтобы наше приложение могло обработать это:</span><span class="sxs-lookup"><span data-stu-id="d6adc-197">Now, back in `web.rb` let's program our application to handle this:</span></span>

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for the ping! Twilio and Azure rock!</Message>
       </Response>"
    end

<span data-ttu-id="d6adc-198">После внесения изменений перезапустите веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="d6adc-198">After making the change, make sure to re-start your web app.</span></span> <span data-ttu-id="d6adc-199">Теперь возьмите телефон и отправьте SMS на ваш номер Twilio.</span><span class="sxs-lookup"><span data-stu-id="d6adc-199">Now, take out your phone and send an SMS to your Twilio number.</span></span> <span data-ttu-id="d6adc-200">Вы должны быстро получить ответ: "Hey, thanks for the ping!</span><span class="sxs-lookup"><span data-stu-id="d6adc-200">You should promptly get an SMS response that says "Hey, thanks for the ping!</span></span> <span data-ttu-id="d6adc-201">Twilio and Azure rock!" (Спасибо за сообщение. Twilio и Azure лучше всех!).</span><span class="sxs-lookup"><span data-stu-id="d6adc-201">Twilio and Azure rock!".</span></span>

## <span data-ttu-id="d6adc-202"><a id="additional_services"></a>Руководство: использование дополнительных служб Twilio</span><span class="sxs-lookup"><span data-stu-id="d6adc-202"><a id="additional_services"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="d6adc-203">В дополнение к приведенным примерам, Twilio предлагает веб-интерфейсы API для использования дополнительных функций Twilio в вашем приложении Azure.</span><span class="sxs-lookup"><span data-stu-id="d6adc-203">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="d6adc-204">Дополнительные сведения см. в [документации по интерфейсу API Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="d6adc-204">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

### <span data-ttu-id="d6adc-205"><a id="NextSteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d6adc-205"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="d6adc-206">Вы узнали основные сведения о службе Twilio. Для получения дополнительных сведений используйте следующие ссылки.</span><span class="sxs-lookup"><span data-stu-id="d6adc-206">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="d6adc-207">[Рекомендации по безопасности Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="d6adc-207">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="d6adc-208">[Практические руководства по Twilio и пример кода][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="d6adc-208">[Twilio HowTos and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="d6adc-209">[Краткие учебники по Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="d6adc-209">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="d6adc-210">[Twilio на GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="d6adc-210">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="d6adc-211">[Обращение в службу поддержки Twilio][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="d6adc-211">[Talk to Twilio Support][twilio_support]</span></span>

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
