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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-ruby"></a><span data-ttu-id="bca11-104">Как tooUse Twilio для голосовых возможностей и SMS в Ruby</span><span class="sxs-lookup"><span data-stu-id="bca11-104">How tooUse Twilio for Voice and SMS Capabilities in Ruby</span></span>
<span data-ttu-id="bca11-105">В этом руководстве показано, как tooperform часто встречающиеся задачи программирования с hello Twilio API службы в Azure.</span><span class="sxs-lookup"><span data-stu-id="bca11-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="bca11-106">Hello сценарии включают телефонных звонков и отправке сообщения службы коротких сообщений (SMS).</span><span class="sxs-lookup"><span data-stu-id="bca11-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="bca11-107">Дополнительные сведения о Twilio и использования голоса и SMS в приложениях см. в разделе hello [дальнейшие действия](#NextSteps) раздела.</span><span class="sxs-lookup"><span data-stu-id="bca11-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="bca11-108"><a id="WhatIs"></a>Что такое Twilio?</span><span class="sxs-lookup"><span data-stu-id="bca11-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="bca11-109">Twilio — это API веб службы телефонии, которая позволяет использовать существующие языки веб и навыки toobuild голос, а приложений SMS.</span><span class="sxs-lookup"><span data-stu-id="bca11-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills toobuild voice and SMS applications.</span></span> <span data-ttu-id="bca11-110">Twilio — это сторонняя служба (не компонент Azure и не продукт Майкрософт).</span><span class="sxs-lookup"><span data-stu-id="bca11-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="bca11-111">**Голосовой Twilio** позволяет toomake вашего приложения и приема телефонных звонков.</span><span class="sxs-lookup"><span data-stu-id="bca11-111">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="bca11-112">**Twilio SMS** позволяет toomake вашего приложения и получения сообщений SMS.</span><span class="sxs-lookup"><span data-stu-id="bca11-112">**Twilio SMS** allows your applications toomake and receive SMS messages.</span></span> <span data-ttu-id="bca11-113">**Клиента Twilio** позволяет tooenable голосовой связи с использованием существующих соединений Интернета, в том числе мобильными приложениями.</span><span class="sxs-lookup"><span data-stu-id="bca11-113">**Twilio Client** allows your applications tooenable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="bca11-114"><a id="Pricing"></a>Цены и специальные предложения Twilio</span><span class="sxs-lookup"><span data-stu-id="bca11-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="bca11-115">Сведения о ценах на Twilio доступны на веб-сайте [цен на Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="bca11-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="bca11-116">Клиентам Azure доступно [специальное предложение][special_offer]: бесплатный кредит на 1000 текстовых сообщений или 1000 минут входящих вызовов.</span><span class="sxs-lookup"><span data-stu-id="bca11-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="bca11-117">toosign для использования это предложение или получить дополнительные сведения, посетите [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="bca11-117">toosign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>  

## <span data-ttu-id="bca11-118"><a id="Concepts"></a>Основные понятия</span><span class="sxs-lookup"><span data-stu-id="bca11-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="bca11-119">Hello Twilio API является API RESTful, который предоставляет функциональные возможности SMS и голосовой для приложений.</span><span class="sxs-lookup"><span data-stu-id="bca11-119">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="bca11-120">Полный список клиентских библиотек API Twilio, которые доступны на разных языках, см. на [этой странице][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="bca11-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

### <span data-ttu-id="bca11-121"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="bca11-121"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="bca11-122">TwiML — это набор инструкций, основанный на XML, чтобы сообщить Twilio как tooprocess звонок или SMS.</span><span class="sxs-lookup"><span data-stu-id="bca11-122">TwiML is a set of XML-based instructions that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="bca11-123">Например, следующие TwiML hello бы преобразование текста hello **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="bca11-123">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="bca11-124">Во всех документах TwiML элемент `<Response>` является корневым.</span><span class="sxs-lookup"><span data-stu-id="bca11-124">All TwiML documents have `<Response>` as their root element.</span></span> <span data-ttu-id="bca11-125">После этого используйте команды Twilio toodefine hello поведение приложения.</span><span class="sxs-lookup"><span data-stu-id="bca11-125">From there, you use Twilio Verbs toodefine hello behavior of your application.</span></span>

### <span data-ttu-id="bca11-126"><a id="Verbs"></a>Команды TwiML</span><span class="sxs-lookup"><span data-stu-id="bca11-126"><a id="Verbs"></a>TwiML Verbs</span></span>
<span data-ttu-id="bca11-127">Twilio команды — это XML-теги, которые сообщают Twilio, что слишком**сделать**.</span><span class="sxs-lookup"><span data-stu-id="bca11-127">Twilio Verbs are XML tags that tell Twilio what too**do**.</span></span> <span data-ttu-id="bca11-128">Например, hello  **&lt;Say&gt;**  команда предписывает Twilio tooaudibly доставить сообщение во время вызова.</span><span class="sxs-lookup"><span data-stu-id="bca11-128">For example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span> 

<span data-ttu-id="bca11-129">Hello ниже приведен список команд, Twilio.</span><span class="sxs-lookup"><span data-stu-id="bca11-129">hello following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="bca11-130">**&lt;Удаленный&gt;**: подключается phone tooanother hello вызывающего объекта.</span><span class="sxs-lookup"><span data-stu-id="bca11-130">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="bca11-131">**&lt;Соберите&gt;**: собирает цифры, введенные на клавиатуре телефона hello.</span><span class="sxs-lookup"><span data-stu-id="bca11-131">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="bca11-132">**&lt;Hangup&gt;**: окончание вызова.</span><span class="sxs-lookup"><span data-stu-id="bca11-132">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="bca11-133">**&lt;Play&gt;**: воспроизведение звукового файла.</span><span class="sxs-lookup"><span data-stu-id="bca11-133">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="bca11-134">**&lt;Pause&gt;**: бесшумное ожидание в течение указанного времени (в секундах).</span><span class="sxs-lookup"><span data-stu-id="bca11-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="bca11-135">**&lt;Запись&gt;**: записи голоса hello вызывающего объекта и возвращает URL-адрес файла, содержащего запись hello.</span><span class="sxs-lookup"><span data-stu-id="bca11-135">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="bca11-136">**&lt;Перенаправить&gt;**: передает управление вызова или SMS toohello TwiML на другой URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="bca11-136">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="bca11-137">**&lt;Отклонить&gt;**: отклоняет во входящих вызова tooyour Twilio номер без выставления счетов, вы</span><span class="sxs-lookup"><span data-stu-id="bca11-137">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="bca11-138">**&lt;Предположим,&gt;**: toospeech преобразует текст, который выполняется при вызове функции.</span><span class="sxs-lookup"><span data-stu-id="bca11-138">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="bca11-139">**&lt;Sms&gt;**: отправка SMS-сообщения.</span><span class="sxs-lookup"><span data-stu-id="bca11-139">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

<span data-ttu-id="bca11-140">Дополнительные сведения о командах Twilio, их атрибутах и TwiML см. на странице [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="bca11-140">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="bca11-141">Дополнительные сведения о hello Twilio API см. в разделе [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="bca11-141">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="bca11-142"><a id="CreateAccount"></a>Создание учетной записи Twilio</span><span class="sxs-lookup"><span data-stu-id="bca11-142"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="bca11-143">Когда вы будете готовы tooget учетной записи Twilio, зарегистрируйтесь на [повторите Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="bca11-143">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="bca11-144">Вы можете начать с бесплатной учетной записи и обновить ее позднее.</span><span class="sxs-lookup"><span data-stu-id="bca11-144">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="bca11-145">После регистрации учетной записи Twilio вы получите бесплатный номер телефона для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="bca11-145">When you sign up for a Twilio account, you'll get a free phone number for your application.</span></span> <span data-ttu-id="bca11-146">Вы также получите идентификатор безопасности учетной записи и маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="bca11-146">You'll also receive an account SID and an auth token.</span></span> <span data-ttu-id="bca11-147">Как будет toomake необходимые вызовы Twilio API.</span><span class="sxs-lookup"><span data-stu-id="bca11-147">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="bca11-148">tooprevent несанкционированный доступ к учетной записи tooyour, безопасность срок действия токена проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="bca11-148">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="bca11-149">Ваш ИД безопасности учетной записи и маркер проверки подлинности можно просмотреть в hello [странице учетной записи Twilio][twilio_account]в hello поля с меткой **ИД безопасности учетной записи** и **ТОКЕНА проверки Подлинности** , соответственно.</span><span class="sxs-lookup"><span data-stu-id="bca11-149">Your account SID and auth token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

### <span data-ttu-id="bca11-150"><a id="VerifyPhoneNumbers"></a>Проверка телефонных номеров</span><span class="sxs-lookup"><span data-stu-id="bca11-150"><a id="VerifyPhoneNumbers"></a>Verify Phone Numbers</span></span>
<span data-ttu-id="bca11-151">В дополнение toohello номер выделил Twilio также можно проверить номера управления (т. е. Ваш мобильный телефон или домашней номер телефона) для использования в приложениях.</span><span class="sxs-lookup"><span data-stu-id="bca11-151">In addition toohello number you are given by Twilio, you can also verify numbers that you control (i.e. your cell phone or home phone number) for use in your applications.</span></span> 

<span data-ttu-id="bca11-152">Сведения о том, как tooverify номер телефона, в разделе [управление номера][verify_phone].</span><span class="sxs-lookup"><span data-stu-id="bca11-152">For information on how tooverify a phone number, see [Manage Numbers][verify_phone].</span></span>

## <span data-ttu-id="bca11-153"><a id="create_app"></a>Создание приложения Ruby</span><span class="sxs-lookup"><span data-stu-id="bca11-153"><a id="create_app"></a>Create a Ruby Application</span></span>
<span data-ttu-id="bca11-154">Ruby приложение, которое использует службу hello Twilio и работает в Azure не отличается от любого другого Ruby приложения, использующего службу hello Twilio.</span><span class="sxs-lookup"><span data-stu-id="bca11-154">A Ruby application that uses hello Twilio service and is running in Azure is no different than any other Ruby application that uses hello Twilio service.</span></span> <span data-ttu-id="bca11-155">Хотя Twilio службы являются категории RESTful и может вызываться из Ruby несколькими способами, в этой статье основное внимание уделяется как toouse Twilio служб с [Twilio вспомогательная библиотека для Ruby][twilio_ruby].</span><span class="sxs-lookup"><span data-stu-id="bca11-155">While Twilio services are RESTful and can be called from Ruby in several ways, this article will focus on how toouse Twilio services with [Twilio helper library for Ruby][twilio_ruby].</span></span>

<span data-ttu-id="bca11-156">Во-первых, [установки новой виртуальной Машины Linux Azure] [ azure_vm_setup] tooact как узел нового Ruby веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="bca11-156">First, [set-up a new Azure Linux VM][azure_vm_setup] tooact as a host for your new Ruby web application.</span></span> <span data-ttu-id="bca11-157">Игнорировать hello шагов, затрагивающих hello создания приложения направляющие, просто hello настройки виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="bca11-157">Ignore hello steps involving hello creation of a Rails app, just set-up hello VM.</span></span> <span data-ttu-id="bca11-158">Обязательно создайте конечную точку с внешним портом 80 и внутренним портом 5000.</span><span class="sxs-lookup"><span data-stu-id="bca11-158">Make sure you create an Endpoint with an external port of 80 and an internal port of 5000.</span></span>

<span data-ttu-id="bca11-159">В примерах hello ниже, мы будем использовать [Sinatra][sinatra], это очень простой веб-платформа для Ruby.</span><span class="sxs-lookup"><span data-stu-id="bca11-159">In hello examples below, we will be using [Sinatra][sinatra], a very simple web framework for Ruby.</span></span> <span data-ttu-id="bca11-160">Но определенно можно использовать вспомогательную библиотеку hello Twilio для Ruby с любой другой web платформой, включая Ruby на направляющие.</span><span class="sxs-lookup"><span data-stu-id="bca11-160">But you can certainly use hello Twilio helper library for Ruby with any other web framework, including Ruby on Rails.</span></span>

<span data-ttu-id="bca11-161">Войдите на новую виртуальную машину по протоколу SSH и создайте каталог для нового приложения.</span><span class="sxs-lookup"><span data-stu-id="bca11-161">SSH into your new VM and create a directory for your new app.</span></span> <span data-ttu-id="bca11-162">В этом каталоге создайте файл с именем hello Gemfile и скопируйте следующий код в него:</span><span class="sxs-lookup"><span data-stu-id="bca11-162">Inside that directory, create a file called Gemfile and copy hello following code into it:</span></span>

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

<span data-ttu-id="bca11-163">Hello в командной строке запустите `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="bca11-163">On hello command line run `bundle install`.</span></span> <span data-ttu-id="bca11-164">Будут установлены зависимости hello выше.</span><span class="sxs-lookup"><span data-stu-id="bca11-164">This will install hello dependencies above.</span></span> <span data-ttu-id="bca11-165">Затем создайте файл с именем `web.rb`.</span><span class="sxs-lookup"><span data-stu-id="bca11-165">Next create a file called `web.rb`.</span></span> <span data-ttu-id="bca11-166">Это будет, где находятся hello кода для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="bca11-166">This will be where hello code for your web app lives.</span></span> <span data-ttu-id="bca11-167">Вставьте следующий код в него hello:</span><span class="sxs-lookup"><span data-stu-id="bca11-167">Paste hello following code into it:</span></span>

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

<span data-ttu-id="bca11-168">На этом этапе следует может hello запустите команду hello `ruby web.rb -p 5000`.</span><span class="sxs-lookup"><span data-stu-id="bca11-168">At this point you should be able hello run hello command `ruby web.rb -p 5000`.</span></span> <span data-ttu-id="bca11-169">Она настроит небольшой веб-сервер с портом 5000.</span><span class="sxs-lookup"><span data-stu-id="bca11-169">This will spin-up a small web server on port 5000.</span></span> <span data-ttu-id="bca11-170">Приложение может toobrowse toothis должно быть в браузере, перейдя по адресу hello URL-адрес настройки для ВМ Azure.</span><span class="sxs-lookup"><span data-stu-id="bca11-170">You should be able toobrowse toothis app in your browser by visiting hello URL you set-up for your Azure VM.</span></span> <span data-ttu-id="bca11-171">После можно получить доступ к веб-приложения в браузере hello, теперь вы готовы toostart построение приложения Twilio.</span><span class="sxs-lookup"><span data-stu-id="bca11-171">Once you can reach your web app in hello browser, you're ready toostart building a Twilio app.</span></span>

## <span data-ttu-id="bca11-172"><a id="configure_app"></a>Настройка приложения tooUse Twilio</span><span class="sxs-lookup"><span data-stu-id="bca11-172"><a id="configure_app"></a>Configure Your Application tooUse Twilio</span></span>
<span data-ttu-id="bca11-173">Можно настроить библиотеку Twilio toouse hello web app, обновив вашей `Gemfile` tooinclude этой строки:</span><span class="sxs-lookup"><span data-stu-id="bca11-173">You can configure your web app toouse hello Twilio library by updating your `Gemfile` tooinclude this line:</span></span>

    gem 'twilio-ruby'

<span data-ttu-id="bca11-174">В командной строке hello запуска `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="bca11-174">On hello command line, run `bundle install`.</span></span> <span data-ttu-id="bca11-175">Теперь откройте `web.rb` и включая эту строку в верхней hello:</span><span class="sxs-lookup"><span data-stu-id="bca11-175">Now open `web.rb` and including this line at hello top:</span></span>

    require 'twilio-ruby'

<span data-ttu-id="bca11-176">Вы теперь все набор toouse hello Twilio вспомогательную библиотеку для Ruby в веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="bca11-176">You're now all set toouse hello Twilio helper library for Ruby in your web app.</span></span>

## <span data-ttu-id="bca11-177"><a id="howto_make_call"></a>Практическое руководство. Осуществление исходящего вызова</span><span class="sxs-lookup"><span data-stu-id="bca11-177"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="bca11-178">Следуя Hello показано, как вызвать toomake исходящего сообщения.</span><span class="sxs-lookup"><span data-stu-id="bca11-178">hello following shows how toomake an outgoing call.</span></span> <span data-ttu-id="bca11-179">Основные понятия относится использование hello Twilio вспомогательную библиотеку для toomake Ruby, которые вызывает API-Интерфейс REST и подготовке к просмотру TwiML.</span><span class="sxs-lookup"><span data-stu-id="bca11-179">Key concepts include using hello Twilio helper library for Ruby toomake REST API calls and rendering TwiML.</span></span> <span data-ttu-id="bca11-180">Подставьте собственные значения hello **из** и **для** номера телефонов и убедитесь в правильности hello **из** телефонный номер для кода hello предыдущих toorunning учетной записи Twilio.</span><span class="sxs-lookup"><span data-stu-id="bca11-180">Substitute your values for hello **From** and **To** phone numbers, and ensure that you verify hello **From** phone number for your Twilio account prior toorunning hello code.</span></span>

<span data-ttu-id="bca11-181">Добавьте эту функцию слишком`web.md`:</span><span class="sxs-lookup"><span data-stu-id="bca11-181">Add this function too`web.md`:</span></span>

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

<span data-ttu-id="bca11-182">Если вы открыть доступ к `http://yourdomain.cloudapp.net/make_call` в браузере, вызывающих hello вызовов Twilio API toohello toomake hello телефонный звонок.</span><span class="sxs-lookup"><span data-stu-id="bca11-182">If you open-up `http://yourdomain.cloudapp.net/make_call` in a browser, that will trigger hello call toohello Twilio API toomake hello phone call.</span></span> <span data-ttu-id="bca11-183">Здравствуйте, первые два параметра в `client.account.calls.create` говорят сами за себя: hello номеров hello вызов `from` и число вызовов hello hello `to`.</span><span class="sxs-lookup"><span data-stu-id="bca11-183">hello first two parameters in `client.account.calls.create` are fairly self-explanatory: hello number hello call is `from` and hello number hello call is `to`.</span></span> 

<span data-ttu-id="bca11-184">Здравствуйте, третий параметр (`url`) — hello URL-адрес, что Twilio запросы tooget инструкции какие toodo после подключения вызова hello.</span><span class="sxs-lookup"><span data-stu-id="bca11-184">hello third parameter (`url`) is hello URL that Twilio requests tooget instructions on what toodo once hello call is connected.</span></span> <span data-ttu-id="bca11-185">В данном случае мы настройки URL-адрес (`http://yourdomain.cloudapp.net`), возвращает простой документ TwiML и использует hello `<Say>` вызова команды toodo некоторые преобразования текста в речь и сказать «Hello Monkey» toohello лицо, получающее hello.</span><span class="sxs-lookup"><span data-stu-id="bca11-185">In this case we set-up a URL (`http://yourdomain.cloudapp.net`) that returns a simple TwiML document and uses hello `<Say>` verb toodo some text-to-speech and say "Hello Monkey" toohello person recieving hello call.</span></span>

## <span data-ttu-id="bca11-186"><a id="howto_recieve_sms"></a>Руководство: получение SMS-сообщения</span><span class="sxs-lookup"><span data-stu-id="bca11-186"><a id="howto_recieve_sms"></a>How to: Recieve an SMS message</span></span>
<span data-ttu-id="bca11-187">В предыдущем примере hello инициировал **исходящих** телефонный звонок.</span><span class="sxs-lookup"><span data-stu-id="bca11-187">In hello previous example we initiated an **outgoing** phone call.</span></span> <span data-ttu-id="bca11-188">Это время, воспользуемся hello номер телефона, который мы получили Twilio во время регистрации tooprocess **входящих** SMS-сообщения.</span><span class="sxs-lookup"><span data-stu-id="bca11-188">This time, let's use hello phone number that Twilio gave us during sign-up tooprocess an **incoming** SMS message.</span></span>

<span data-ttu-id="bca11-189">Во-первых, в журнал tooyour [панель мониторинга Twilio][twilio_account].</span><span class="sxs-lookup"><span data-stu-id="bca11-189">First, log-in tooyour [Twilio dashboard][twilio_account].</span></span> <span data-ttu-id="bca11-190">Щелкните «Чисел» в верхней панели навигации hello и выберите команду hello номер Twilio, которые были предоставлены.</span><span class="sxs-lookup"><span data-stu-id="bca11-190">Click on "Numbers" in hello top nav and then click on hello Twilio number you were provided.</span></span> <span data-ttu-id="bca11-191">Вы увидите два URL-адреса, которые можно настроить:</span><span class="sxs-lookup"><span data-stu-id="bca11-191">You'll see two URLs that you can configure.</span></span> <span data-ttu-id="bca11-192">URL-адрес запроса голосового вызова и URL-адрес запроса SMS.</span><span class="sxs-lookup"><span data-stu-id="bca11-192">A Voice Request URL and an SMS Request URL.</span></span> <span data-ttu-id="bca11-193">Это URL-адреса hello внесенных Twilio вызовы каждый раз, когда телефонный звонок или SMS-сообщения отправляется номер tooyour.</span><span class="sxs-lookup"><span data-stu-id="bca11-193">These are hello URLs that Twilio calls whenever a phone call is made or an SMS is sent tooyour number.</span></span> <span data-ttu-id="bca11-194">Hello URL-адреса также известны как «обработчики web».</span><span class="sxs-lookup"><span data-stu-id="bca11-194">hello URLs are also known as "web hooks".</span></span>

<span data-ttu-id="bca11-195">Мы хотели бы tooprocess SMS-сообщений, поэтому необходимо обновить URL-адрес hello слишком`http://yourdomain.cloudapp.net/sms_url`.</span><span class="sxs-lookup"><span data-stu-id="bca11-195">We would like tooprocess incoming SMS messages, so let's update hello URL too`http://yourdomain.cloudapp.net/sms_url`.</span></span> <span data-ttu-id="bca11-196">Продолжим и нажмите кнопку Сохранить изменения hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="bca11-196">Go ahead and click Save Changes at hello bottom of hello page.</span></span> <span data-ttu-id="bca11-197">Вернувшись `web.rb` давайте запрограммировать нашей toohandle приложения:</span><span class="sxs-lookup"><span data-stu-id="bca11-197">Now, back in `web.rb` let's program our application toohandle this:</span></span>

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for hello ping! Twilio and Azure rock!</Message>
       </Response>"
    end

<span data-ttu-id="bca11-198">После изменения "hello", убедитесь, что toore-start веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="bca11-198">After making hello change, make sure toore-start your web app.</span></span> <span data-ttu-id="bca11-199">Теперь Извлеките ваш телефон и отправки SMS tooyour номер Twilio.</span><span class="sxs-lookup"><span data-stu-id="bca11-199">Now, take out your phone and send an SMS tooyour Twilio number.</span></span> <span data-ttu-id="bca11-200">Следует своевременно получать ответ SMS, который говорит, что ему, Спасибо, что hello ping!</span><span class="sxs-lookup"><span data-stu-id="bca11-200">You should promptly get an SMS response that says "Hey, thanks for hello ping!</span></span> <span data-ttu-id="bca11-201">Twilio and Azure rock!" (Спасибо за сообщение. Twilio и Azure лучше всех!).</span><span class="sxs-lookup"><span data-stu-id="bca11-201">Twilio and Azure rock!".</span></span>

## <span data-ttu-id="bca11-202"><a id="additional_services"></a>Руководство: использование дополнительных служб Twilio</span><span class="sxs-lookup"><span data-stu-id="bca11-202"><a id="additional_services"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="bca11-203">В дополнение к этому toohello в этой статье примерах, Twilio предлагает веб-API, можно использовать дополнительные возможности Twilio tooleverage из приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="bca11-203">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="bca11-204">Дополнительные сведения см. в разделе hello [документации по Twilio API][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="bca11-204">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

### <span data-ttu-id="bca11-205"><a id="NextSteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bca11-205"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="bca11-206">Теперь, когда вы узнали основы hello hello Twilio службы, выполните следующие дополнительные toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="bca11-206">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="bca11-207">[Рекомендации по безопасности Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="bca11-207">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="bca11-208">[Практические руководства по Twilio и пример кода][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="bca11-208">[Twilio HowTos and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="bca11-209">[Краткие учебники по Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="bca11-209">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="bca11-210">[Twilio на GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="bca11-210">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="bca11-211">[Обращайтесь tooTwilio поддержки][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="bca11-211">[Talk tooTwilio Support][twilio_support]</span></span>

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
