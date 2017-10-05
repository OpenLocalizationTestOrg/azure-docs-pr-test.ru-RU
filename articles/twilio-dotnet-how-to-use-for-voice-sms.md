---
title: "Как использовать Twilio для поддержки голосовых вызовов и SMS (.NET) | Документация Майкрософт"
description: "Узнайте, как осуществлять телефонные вызовы и отправку SMS-сообщений с помощью службы Twilio API в Azure. Примеры программного кода написаны в .NET."
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
ms.openlocfilehash: 1442e3af26ae87e645cf207228ed1197b2afdd4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-from-azure"></a><span data-ttu-id="18027-104">Использование Twilio для поддержки голосовых вызовов и SMS в Azure</span><span class="sxs-lookup"><span data-stu-id="18027-104">How to use Twilio for voice and SMS capabilities from Azure</span></span>
<span data-ttu-id="18027-105">В этом руководстве показано, как выполнять типовые задачи программирования с помощью службы Twilio API в Azure.</span><span class="sxs-lookup"><span data-stu-id="18027-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="18027-106">Здесь описываются такие сценарии, как телефонный звонок и отправка SMS-сообщения.</span><span class="sxs-lookup"><span data-stu-id="18027-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="18027-107">Дополнительные сведения о Twilio и использовании голосовых функций и SMS в приложениях см. в разделе [Дальнейшие действия](#NextSteps).</span><span class="sxs-lookup"><span data-stu-id="18027-107">For more information on Twilio and using voice and SMS in your applications, see the [Next steps](#NextSteps) section.</span></span>

## <span data-ttu-id="18027-108"><a id="WhatIs"></a>Что такое Twilio?</span><span class="sxs-lookup"><span data-stu-id="18027-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="18027-109">Twilio создает новые возможности для бизнес-коммуникаций, позволяя разработчикам встраивать в приложения функции голосовой связи, VoIP и обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="18027-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="18027-110">Они виртуализируют всю необходимую инфраструктуру в облачной глобальной среде с предоставлением доступа через коммуникационную API платформу Twilio.</span><span class="sxs-lookup"><span data-stu-id="18027-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span></span> <span data-ttu-id="18027-111">Приложения отличаются простотой создания и масштабирования.</span><span class="sxs-lookup"><span data-stu-id="18027-111">Applications are simple to build and scalable.</span></span> <span data-ttu-id="18027-112">Оцените гибкость работы с оплатой по мере использования и преимущества надежности облака.</span><span class="sxs-lookup"><span data-stu-id="18027-112">Enjoy flexibility with pay-as-you-go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="18027-113">**Twilio Voice** позволяет приложениям осуществлять и принимать телефонные вызовы.</span><span class="sxs-lookup"><span data-stu-id="18027-113">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="18027-114">**Twilio SMS** позволяет приложениям отправлять и принимать SMS-сообщения.</span><span class="sxs-lookup"><span data-stu-id="18027-114">**Twilio SMS** enables your applications to send and receive SMS messages.</span></span> <span data-ttu-id="18027-115">**Twilio Client** позволяет выполнять VoIP звонки с любого телефона, планшета или из браузера, а также поддерживает WebRTC.</span><span class="sxs-lookup"><span data-stu-id="18027-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="18027-116"><a id="Pricing"></a>Цены и специальные предложения Twilio</span><span class="sxs-lookup"><span data-stu-id="18027-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="18027-117">Клиентам Azure доступно [специальное предложение](http://www.twilio.com/azure): кредит Twilio в размере 10 долл. США при обновлении учетной записи Twilio.</span><span class="sxs-lookup"><span data-stu-id="18027-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="18027-118">Этот кредит Twilio применяется к любым сценариям использования Twilio (кредит в размере 10 $ позволяет отправить 1000 SMS-сообщений или получать входящие голосовые вызовы продолжительностью до 1000 минут в зависимости от расположения телефонного номера, а также от направления отправки сообщения или совершения звонка).</span><span class="sxs-lookup"><span data-stu-id="18027-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span></span> <span data-ttu-id="18027-119">Получите этот кредит Twilio и приступите к работе на [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="18027-119">Redeem this Twilio credit and get started at [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="18027-120">Twilio представляет собой службу с повременной оплатой.</span><span class="sxs-lookup"><span data-stu-id="18027-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="18027-121">Стартовые платежи отсутствуют, а учетную запись можно закрыть в любое время.</span><span class="sxs-lookup"><span data-stu-id="18027-121">There are no set-up fees, and you can close your account at any time.</span></span> <span data-ttu-id="18027-122">Дополнительные сведения см. в статье [Цены на Twilio](http://www.twilio.com/voice/pricing).</span><span class="sxs-lookup"><span data-stu-id="18027-122">You can find more details at [Twilio Pricing](http://www.twilio.com/voice/pricing).</span></span>

## <span data-ttu-id="18027-123"><a id="Concepts"></a>Основные понятия</span><span class="sxs-lookup"><span data-stu-id="18027-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="18027-124">Twilio API — это интерфейс API RESTful, который предоставляет приложениям функции для работы с голосовыми вызовами и SMS.</span><span class="sxs-lookup"><span data-stu-id="18027-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="18027-125">Полный список клиентских библиотек API Twilio, которые доступны на разных языках, см. на [этой странице][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="18027-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="18027-126">Основные аспекты Twilio API: команды Twilio и язык разметки Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="18027-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="18027-127"><a id="Verbs"></a>Команды Twilio</span><span class="sxs-lookup"><span data-stu-id="18027-127"><a id="Verbs"></a>Twilio verbs</span></span>
<span data-ttu-id="18027-128">В API используются команды Twilio: например, команда **&lt;Say&gt;** указывает Twilio, что необходимо воспроизвести сообщение в случае вызова.</span><span class="sxs-lookup"><span data-stu-id="18027-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="18027-129">Ниже приведен список команд Twilio.</span><span class="sxs-lookup"><span data-stu-id="18027-129">The following is a list of Twilio verbs.</span></span>  <span data-ttu-id="18027-130">Дополнительные сведения о других командах и возможностях см. в [документации по языку разметки Twilio](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="18027-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="18027-131">**&lt;Dial&gt;**: подключение вызывающего абонента к другому телефону.</span><span class="sxs-lookup"><span data-stu-id="18027-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="18027-132">**&lt;Gather&gt;**: сбор цифр, введенных на клавиатуре телефона.</span><span class="sxs-lookup"><span data-stu-id="18027-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="18027-133">**&lt;Hangup&gt;**: окончание вызова.</span><span class="sxs-lookup"><span data-stu-id="18027-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="18027-134">**&lt;Play&gt;**: воспроизведение звукового файла.</span><span class="sxs-lookup"><span data-stu-id="18027-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="18027-135">**&lt;Pause&gt;**: бесшумное ожидание в течение указанного времени (в секундах).</span><span class="sxs-lookup"><span data-stu-id="18027-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="18027-136">**&lt;Record&gt;**: запись голоса вызывающего абонента и возвращение URL-адреса файла, содержащего запись.</span><span class="sxs-lookup"><span data-stu-id="18027-136">**&lt;Record&gt;**: Records the caller's voice and returns an URL of a file that contains the recording.</span></span>
* <span data-ttu-id="18027-137">**&lt;Redirect&gt;**: передача управления для вызова или SMS в TwiML по другому URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="18027-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="18027-138">**&lt;Reject&gt;**: отклонение входящего вызова на ваш номер Twilio без выставления счета.</span><span class="sxs-lookup"><span data-stu-id="18027-138">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="18027-139">**&lt;Say&gt;**: преобразование текста в речь при вызове.</span><span class="sxs-lookup"><span data-stu-id="18027-139">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="18027-140">**&lt;Sms&gt;**: отправка SMS-сообщения.</span><span class="sxs-lookup"><span data-stu-id="18027-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="18027-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="18027-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="18027-142">TwiML — это набор инструкций на основе XML и с использованием команд Twilio, которые сообщают службе Twilio, как необходимо обработать вызов или SMS.</span><span class="sxs-lookup"><span data-stu-id="18027-142">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="18027-143">Например, следующие инструкции TwiML преобразуют текст **Hello World** в речь.</span><span class="sxs-lookup"><span data-stu-id="18027-143">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="18027-144">Когда приложение вызывает Twilio API, одним из параметров API является URL-адрес, который возвращает ответ TwiML.</span><span class="sxs-lookup"><span data-stu-id="18027-144">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="18027-145">Для целей разработки можно использовать URL-адреса из Twilio для предоставления ответов TwiML, используемых приложениями.</span><span class="sxs-lookup"><span data-stu-id="18027-145">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="18027-146">Также может разместить свои собственные URL-адреса для получения ответов TwiML; другой вариант — использовать объект **TwiMLResponse** .</span><span class="sxs-lookup"><span data-stu-id="18027-146">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="18027-147">Дополнительные сведения о командах Twilio, их атрибутах и TwiML см. на странице [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="18027-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="18027-148">Дополнительные сведения об API Twilio см. на [этой странице][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="18027-148">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="18027-149"><a id="CreateAccount"></a>Создание учетной записи Twilio</span><span class="sxs-lookup"><span data-stu-id="18027-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="18027-150">После подготовки к получению учетной записи Twilio зарегистрируйтесь на [странице получения пробной версии Twilio ][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="18027-150">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="18027-151">Вы можете начать с бесплатной учетной записи и обновить ее позднее.</span><span class="sxs-lookup"><span data-stu-id="18027-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="18027-152">При регистрации учетной записи Twilio, вы получите идентификатор учетной записи и маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="18027-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="18027-153">Эти элементы необходимы для вызовов Twilio API.</span><span class="sxs-lookup"><span data-stu-id="18027-153">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="18027-154">Чтобы предотвратить несанкционированный доступ к учетной записи, храните маркер проверки подлинности в безопасности.</span><span class="sxs-lookup"><span data-stu-id="18027-154">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="18027-155">Идентификатор учетной записи и маркер аутентификации отображаются на [странице учетной записи Twilio][twilio_account] в полях **ACCOUNT SID** (Идентификатор безопасности учетной записи) и **AUTH TOKEN** (Маркер аутентификации) соответственно.</span><span class="sxs-lookup"><span data-stu-id="18027-155">Your account ID and authentication token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="18027-156"><a id="create_app"></a>Создание приложения Azure</span><span class="sxs-lookup"><span data-stu-id="18027-156"><a id="create_app"></a>Create an Azure Application</span></span>
<span data-ttu-id="18027-157">Приложение Azure, на котором размещается приложение с поддержкой Twilio, ничем не отличается от любого другого приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="18027-157">An Azure application that hosts a Twilio enabled application is no different from any other Azure application.</span></span> <span data-ttu-id="18027-158">Добавьте библиотеку Twilio для .NET и настройте роль так, чтобы она могла использовать такие библиотеки.</span><span class="sxs-lookup"><span data-stu-id="18027-158">You add the Twilio .NET library and configure the role to use the Twilio .NET libraries.</span></span>
<span data-ttu-id="18027-159">Сведения о создании начального проекта Azure с помощью Visual Studio см. на [этой странице][vs_project].</span><span class="sxs-lookup"><span data-stu-id="18027-159">For information on creating an initial Azure project, see [Creating an Azure project with Visual Studio][vs_project].</span></span>

## <span data-ttu-id="18027-160"><a id="configure_app"></a>Настройка приложения для использования библиотек Twilio</span><span class="sxs-lookup"><span data-stu-id="18027-160"><a id="configure_app"></a>Configure Your Application to use Twilio Libraries</span></span>
<span data-ttu-id="18027-161">Twilio предоставляет набор вспомогательных библиотек .NET, содержащих различные аспекты Twilio для предоставления простых и легких способов взаимодействия с Twilio REST API и Twilio Client для создания ответов TwiML.</span><span class="sxs-lookup"><span data-stu-id="18027-161">Twilio provides a set of .NET helper libraries that wrap various aspects of Twilio to provide simple and easy ways to interact with the Twilio REST API and Twilio Client to generate TwiML responses.</span></span>

<span data-ttu-id="18027-162">Twilio предоставляет пять библиотек для разработчиков .NET:</span><span class="sxs-lookup"><span data-stu-id="18027-162">Twilio provides five libraries for .NET developers:</span></span>
<span data-ttu-id="18027-163">Библиотека</span><span class="sxs-lookup"><span data-stu-id="18027-163">Library</span></span>|<span data-ttu-id="18027-164">Описание</span><span class="sxs-lookup"><span data-stu-id="18027-164">Description</span></span>
---|---
<span data-ttu-id="18027-165">Twilio.API</span><span class="sxs-lookup"><span data-stu-id="18027-165">Twilio.API</span></span>|<span data-ttu-id="18027-166">Основная библиотека Twilio, реализующая интерфейс API REST Twilio в виде понятной библиотеки .NET.</span><span class="sxs-lookup"><span data-stu-id="18027-166">The core Twilio library that wraps the Twilio REST API in a friendly .NET library.</span></span> <span data-ttu-id="18027-167">Эта библиотека доступна для .NET, Silverlight и Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="18027-167">This library is available for .NET, Silverlight, and Windows Phone 7.</span></span>
<span data-ttu-id="18027-168">Twilio.TwiML</span><span class="sxs-lookup"><span data-stu-id="18027-168">Twilio.TwiML</span></span>|<span data-ttu-id="18027-169">Позволяет создавать разметку TwiML удобным для .NET способом.</span><span class="sxs-lookup"><span data-stu-id="18027-169">Provides a .NET friendly way to generate TwiML markup.</span></span>
<span data-ttu-id="18027-170">Twilio.MVC</span><span class="sxs-lookup"><span data-stu-id="18027-170">Twilio.MVC</span></span>|<span data-ttu-id="18027-171">Для разработчиков, использующих ASP.NET MVC, эта библиотека включает в себя TwilioController, TwiML ActionResult и атрибут проверки запроса.</span><span class="sxs-lookup"><span data-stu-id="18027-171">For developers using ASP.NET MVC, this library includes a TwilioController, TwiML ActionResult, and request validation attribute.</span></span>
<span data-ttu-id="18027-172">Twilio.WebMatrix</span><span class="sxs-lookup"><span data-stu-id="18027-172">Twilio.WebMatrix</span></span>|<span data-ttu-id="18027-173">Для разработчиков, использующих бесплатное средство разработки WebMatrix от Microsoft, эта библиотека содержит помощники синтаксиса Razor для выполнения различных действий Twilio.</span><span class="sxs-lookup"><span data-stu-id="18027-173">For developers using Microsoft's free WebMatrix development tool, this library contains Razor syntax helpers for various Twilio actions.</span></span>
<span data-ttu-id="18027-174">Twilio.Client.Capability</span><span class="sxs-lookup"><span data-stu-id="18027-174">Twilio.Client.Capability</span></span>|<span data-ttu-id="18027-175">Содержит генератор маркера "Возможность" для использования с Twilio Client JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="18027-175">Contains the Capability token generator for use with the Twilio Client JavaScript SDK.</span></span>

<span data-ttu-id="18027-176">Обратите внимание, что для всех библиотек требуется .NET 3.5, Silverlight 4 и Windows Phone 7 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="18027-176">Note that all libraries require .NET 3.5, Silverlight 4, or Windows Phone 7 or later.</span></span>

<span data-ttu-id="18027-177">В примерах, приведенных в этом руководстве, используется библиотека Twilio.API.</span><span class="sxs-lookup"><span data-stu-id="18027-177">The samples provided in this guide use the Twilio.API library.</span></span>

<span data-ttu-id="18027-178">Библиотеки можно [установить с помощью расширения диспетчера пакетов NuGet](http://www.twilio.com/docs/csharp/install), доступного для всех версий, начиная с Visual Studio 2010 и заканчивая Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="18027-178">The libraries can be [installed using the NuGet package manager extension](http://www.twilio.com/docs/csharp/install) available for Visual Studio 2010 up to 2015.</span></span>  <span data-ttu-id="18027-179">Исходный код размещен на веб-сайте [GitHub][twilio_github_repo]. Там же есть ссылка на вики-сайт с полной документацией по использованию этих библиотек.</span><span class="sxs-lookup"><span data-stu-id="18027-179">The source code is hosted on [GitHub][twilio_github_repo], which includes a Wiki that contains complete documentation for using the libraries.</span></span>

<span data-ttu-id="18027-180">По умолчанию Microsoft Visual Studio 2010 устанавливает NuGet версии 1.2.</span><span class="sxs-lookup"><span data-stu-id="18027-180">By default, Microsoft Visual Studio 2010 installs version 1.2 of NuGet.</span></span> <span data-ttu-id="18027-181">Для установки библиотек Twilio требуется версия NuGet 1.6 или выше.</span><span class="sxs-lookup"><span data-stu-id="18027-181">Installing the Twilio libraries requires version 1.6 of NuGet or higher.</span></span> <span data-ttu-id="18027-182">Дополнительные сведения об установке или обновлении NuGet см. на веб-сайте [http://nuget.org/][nuget].</span><span class="sxs-lookup"><span data-stu-id="18027-182">For information on installing or updating NuGet, see [http://nuget.org/][nuget].</span></span>

> [!NOTE]
> <span data-ttu-id="18027-183">Чтобы установить последнюю версию NuGet, сначала необходимо удалить загруженную версию, используя диспетчер расширений Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="18027-183">To install the latest version of NuGet, you must first uninstall the loaded version using the Visual Studio Extension Manager.</span></span> <span data-ttu-id="18027-184">Для этого необходимо запустить Visual Studio от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="18027-184">To do so, you must run Visual Studio as administrator.</span></span> <span data-ttu-id="18027-185">В противном случае кнопка «Удалить» будет неактивна.</span><span class="sxs-lookup"><span data-stu-id="18027-185">Otherwise, the Uninstall button is disabled.</span></span>
>
>

### <span data-ttu-id="18027-186"><a id="use_nuget"></a>Чтобы добавить библиотеки Twilio в проект Visual Studio, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="18027-186"><a id="use_nuget"></a>To add the Twilio libraries to your Visual Studio project:</span></span>
1. <span data-ttu-id="18027-187">Откройте решение в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="18027-187">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="18027-188">Щелкните правой кнопкой мыши **References**(Ссылки).</span><span class="sxs-lookup"><span data-stu-id="18027-188">Right-click **References**.</span></span>
3. <span data-ttu-id="18027-189">Щелкните **Manage NuGet Packages...**</span><span class="sxs-lookup"><span data-stu-id="18027-189">Click **Manage NuGet Packages...**</span></span>
4. <span data-ttu-id="18027-190">Щелкните **Online**(В сети).</span><span class="sxs-lookup"><span data-stu-id="18027-190">Click **Online**.</span></span>
5. <span data-ttu-id="18027-191">В поле поиска online введите *twilio*.</span><span class="sxs-lookup"><span data-stu-id="18027-191">In the search online box, type *twilio*.</span></span>
6. <span data-ttu-id="18027-192">Щелкните **Install** (Установить) на пакете Twilio.</span><span class="sxs-lookup"><span data-stu-id="18027-192">Click **Install** on the Twilio package.</span></span>

## <span data-ttu-id="18027-193"><a id="howto_make_call"></a>Практическое руководство. Осуществление исходящего вызова</span><span class="sxs-lookup"><span data-stu-id="18027-193"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="18027-194">Далее показано, как осуществлять исходящий вызов с использованием класса **CallResource**.</span><span class="sxs-lookup"><span data-stu-id="18027-194">The following shows how to make an outgoing call using the **CallResource** class.</span></span> <span data-ttu-id="18027-195">Этот код также использует сайт из Twilio для выдачи ответа на языке разметки Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="18027-195">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="18027-196">Замените значения телефонных номеров **To** (Кому) и **From** (От) и проверьте номер телефона **From** (От) для учетной записи Twilio перед выполнением кода.</span><span class="sxs-lookup"><span data-stu-id="18027-196">Substitute your values for the **to** and **from** phone numbers, and ensure that you verify the **from** phone number for your Twilio account before running the code.</span></span>

    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize the TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    // Use the Twilio-provided site for the TwiML response.
    var url = "http://twimlets.com/message";
    url = $"{url}?Message%5B0%5D=Hello%20World";

    // Set the call From, To, and URL values to use for the call.
    // This sample uses the sandbox number provided by
    // Twilio to make the call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri(url));
        }

<span data-ttu-id="18027-197">Дополнительные сведения о параметрах, передаваемых в метод **CallResource.Create**, см. в разделе [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="18027-197">For more information about the parameters passed in to the **CallResource.Create** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="18027-198">Как уже упоминалось, этот код также использует сайт из Twilio для выдачи ответа на языке TwiML.</span><span class="sxs-lookup"><span data-stu-id="18027-198">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="18027-199">Вместо этого можно использовать собственный веб-сайт для предоставления ответа TwiML.</span><span class="sxs-lookup"><span data-stu-id="18027-199">You could instead use your own site to provide the TwiML response.</span></span> <span data-ttu-id="18027-200">Дополнительные сведения см. в разделе [Практическое руководство. Предоставление ответа TwiML с собственного веб-сайта](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="18027-200">For more information, see [How to: Provide TwiML responses from your own website](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="18027-201"><a id="howto_send_sms"></a>Практическое руководство. Отправка SMS-сообщения</span><span class="sxs-lookup"><span data-stu-id="18027-201"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="18027-202">На следующем снимке экрана показано, как отправить SMS-сообщение с использованием класса **MessageResource**.</span><span class="sxs-lookup"><span data-stu-id="18027-202">The following screenshot shows how to send an SMS message using the **MessageResource**  class.</span></span> <span data-ttu-id="18027-203">С целью отправки SMS-сообщений для пробных учетных записей номер **From** (От) предоставляется Twilio.</span><span class="sxs-lookup"><span data-stu-id="18027-203">The **from** number is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="18027-204">Номер **To** (Кому) для учетной записи Twilio необходимо проверить перед выполнением кода.</span><span class="sxs-lookup"><span data-stu-id="18027-204">The **to** number must be verified for your Twilio account before you run the code.</span></span>

    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize the TwilioClient.
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
        // An exception occurred making the REST call
        Console.WriteLine(ex.Message);
    }

## <span data-ttu-id="18027-205"><a id="howto_provide_twiml_responses"></a>Практическое руководство. Предоставление откликов TwiML с вашего веб-сайта</span><span class="sxs-lookup"><span data-stu-id="18027-205"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own website</span></span>
<span data-ttu-id="18027-206">Когда приложение инициирует вызов API Twilio (например, с использованием метода **CallResource.Create**), Twilio отправляет ваш запрос на URL-адрес, который должен вернуть ответ TwiML.</span><span class="sxs-lookup"><span data-stu-id="18027-206">When your application initiates a call to the Twilio API - for example, via the **CallResource.Create** method - Twilio sends your request to an URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="18027-207">В примере, показанном в разделе [Практическое руководство. Осуществление исходящего звонка](#howto_make_call), для возврата отклика используется URL-адрес [http://twimlets.com/message][twimlet_message_url], предоставляемый Twilio.</span><span class="sxs-lookup"><span data-stu-id="18027-207">The example in [How to: Make an outgoing call](#howto_make_call) uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url] to return the response.</span></span>

> [!NOTE]
> <span data-ttu-id="18027-208">Хотя TwiML предназначается для использования веб-службами, TwiML можно также просмотреть в браузере.</span><span class="sxs-lookup"><span data-stu-id="18027-208">While TwiML is designed for use by web services, you can view the TwiML in your browser.</span></span> <span data-ttu-id="18027-209">Например, выберите [http://twimlets.com/message][twimlet_message_url] для просмотра пустого элемента &lt;Response&gt;. В качестве другого примера щелкните [http://twimlets.com/message?Message%5B0%5D=Hello%20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) для просмотра элемента &lt;Response&gt;, содержащего элемент &lt;Say&gt;.</span><span class="sxs-lookup"><span data-stu-id="18027-209">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty &lt;Response&gt; element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) to see a &lt;Response&gt; element that contains a &lt;Say&gt; element.</span></span>
>
>

<span data-ttu-id="18027-210">Вместо того чтобы использовать URL-адрес, предоставленный Twilio, можно создать собственный URL-адрес для возврата HTTP-ответов.</span><span class="sxs-lookup"><span data-stu-id="18027-210">Instead of relying on the Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="18027-211">Веб-сайт можно создавать на любом языке, который возвращает HTTP-ответы.</span><span class="sxs-lookup"><span data-stu-id="18027-211">You can create the site in any language that returns HTTP responses.</span></span> <span data-ttu-id="18027-212">В этом разделе предполагается, что URL-адрес будет размещаться из универсального обработчика ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="18027-212">This topic assumes you'll be hosting the URL from an ASP.NET generic handler.</span></span>

<span data-ttu-id="18027-213">Следующий обработчик ASP.NET создает ответ TwiML **Hello World** на вызов.</span><span class="sxs-lookup"><span data-stu-id="18027-213">The following ASP.NET Handler crafts a TwiML response that says **Hello World** on the call.</span></span>

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
    
<span data-ttu-id="18027-214">Как видно из приведенного выше примера, ответ TwiML будет представлять собой простой XML-документ.</span><span class="sxs-lookup"><span data-stu-id="18027-214">As you can see from the example above, the TwiML response is simply an XML document.</span></span> <span data-ttu-id="18027-215">Библиотека Twilio.TwiML содержит классы, которые создадут для вас TwiML.</span><span class="sxs-lookup"><span data-stu-id="18027-215">The Twilio.TwiML library contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="18027-216">В приведенном ниже примере выдается такой же ответ, как и в предыдущем примере, однако с использованием класса **VoiceResponse**.</span><span class="sxs-lookup"><span data-stu-id="18027-216">The example below produces the equivalent response as shown above, but uses the **VoiceResponse** class.</span></span>

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

<span data-ttu-id="18027-217">Дополнительные сведения о TwiML см. по следующему адресу: [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="18027-217">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span></span>

<span data-ttu-id="18027-218">После настройки способа предоставления ответов TwiML можно передать этот URL-адрес в метод **CallResource.Create**.</span><span class="sxs-lookup"><span data-stu-id="18027-218">Once you have set up a way to provide TwiML responses, you can pass that URL to the **CallResource.Create** method.</span></span> <span data-ttu-id="18027-219">Например, если у вас есть веб-приложение MyTwiML, развернутое в облачной службе Azure, а имя обработчика ASP.NET — mytwiml.ashx, то URL-адрес может быть передан в **CallResource.Create**, как показано в следующем примере кода.</span><span class="sxs-lookup"><span data-stu-id="18027-219">For example, if you have a web application named MyTwiML deployed to an Azure cloud service, and the name of your ASP.NET Handler is mytwiml.ashx, the URL can be passed to **CallResource.Create** as shown in the following code sample:</span></span>

    // This sample uses the sandbox number provided by Twilio to make the call.
    // Place the call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

<span data-ttu-id="18027-220">Дополнительные сведения об использовании Twilio в Azure с ASP.NET см. в статье [Осуществление телефонных звонков с использованием Twilio в веб-роли Azure][howto_phonecall_dotnet].</span><span class="sxs-lookup"><span data-stu-id="18027-220">For additional information about using Twilio on Azure with ASP.NET, see [How to make a phone call using Twilio in a web role on Azure][howto_phonecall_dotnet].</span></span>

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
