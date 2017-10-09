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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-from-azure"></a><span data-ttu-id="87bac-104">Как toouse Twilio для голосовых возможностей и SMS из Azure</span><span class="sxs-lookup"><span data-stu-id="87bac-104">How toouse Twilio for voice and SMS capabilities from Azure</span></span>
<span data-ttu-id="87bac-105">В этом руководстве показано, как tooperform часто встречающиеся задачи программирования с hello Twilio API службы в Azure.</span><span class="sxs-lookup"><span data-stu-id="87bac-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="87bac-106">Hello сценарии включают телефонных звонков и отправке сообщения службы коротких сообщений (SMS).</span><span class="sxs-lookup"><span data-stu-id="87bac-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="87bac-107">Дополнительные сведения о Twilio и использования голоса и SMS в приложениях см. в разделе hello [дальнейшие действия](#NextSteps) раздела.</span><span class="sxs-lookup"><span data-stu-id="87bac-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next steps](#NextSteps) section.</span></span>

## <span data-ttu-id="87bac-108"><a id="WhatIs"></a>Что такое Twilio?</span><span class="sxs-lookup"><span data-stu-id="87bac-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="87bac-109">Twilio включении hello будущее делового общения, включение разработчики tooembed голос, VoIP и обмен сообщениями в приложения.</span><span class="sxs-lookup"><span data-stu-id="87bac-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="87bac-110">Они виртуализация всех инфраструктуру в среде облачных, глобальные, предоставляя его через hello Twilio communications API платформы.</span><span class="sxs-lookup"><span data-stu-id="87bac-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="87bac-111">Приложения, простой toobuild и масштабируемость.</span><span class="sxs-lookup"><span data-stu-id="87bac-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="87bac-112">Оцените гибкость работы с оплатой по мере использования и преимущества надежности облака.</span><span class="sxs-lookup"><span data-stu-id="87bac-112">Enjoy flexibility with pay-as-you-go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="87bac-113">**Голосовой Twilio** позволяет toomake вашего приложения и приема телефонных звонков.</span><span class="sxs-lookup"><span data-stu-id="87bac-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="87bac-114">**Twilio SMS** включает toosend вашего приложения и получения сообщений SMS.</span><span class="sxs-lookup"><span data-stu-id="87bac-114">**Twilio SMS** enables your applications toosend and receive SMS messages.</span></span> <span data-ttu-id="87bac-115">**Клиента Twilio** позволяет toomake VoIP вызовы из любой телефон, планшет или браузера и поддерживает WebRTC.</span><span class="sxs-lookup"><span data-stu-id="87bac-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="87bac-116"><a id="Pricing"></a>Цены и специальные предложения Twilio</span><span class="sxs-lookup"><span data-stu-id="87bac-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="87bac-117">Клиентам Azure доступно [специальное предложение](http://www.twilio.com/azure): кредит Twilio в размере 10 долл. США при обновлении учетной записи Twilio.</span><span class="sxs-lookup"><span data-stu-id="87bac-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="87bac-118">Это кредит Twilio может быть применен tooany Twilio использования ($10 кредит эквивалентные toosending до 1 000 SMS-сообщений или получение копии too1000 входящих голосовых минут, в зависимости от расположения hello ваш телефонный номер и сообщений или вызовов назначения).</span><span class="sxs-lookup"><span data-stu-id="87bac-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="87bac-119">Получите этот кредит Twilio и приступите к работе на [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="87bac-119">Redeem this Twilio credit and get started at [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="87bac-120">Twilio представляет собой службу с повременной оплатой.</span><span class="sxs-lookup"><span data-stu-id="87bac-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="87bac-121">Стартовые платежи отсутствуют, а учетную запись можно закрыть в любое время.</span><span class="sxs-lookup"><span data-stu-id="87bac-121">There are no set-up fees, and you can close your account at any time.</span></span> <span data-ttu-id="87bac-122">Дополнительные сведения см. в статье [Цены на Twilio](http://www.twilio.com/voice/pricing).</span><span class="sxs-lookup"><span data-stu-id="87bac-122">You can find more details at [Twilio Pricing](http://www.twilio.com/voice/pricing).</span></span>

## <span data-ttu-id="87bac-123"><a id="Concepts"></a>Основные понятия</span><span class="sxs-lookup"><span data-stu-id="87bac-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="87bac-124">Hello Twilio API является API RESTful, который предоставляет функциональные возможности SMS и голосовой для приложений.</span><span class="sxs-lookup"><span data-stu-id="87bac-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="87bac-125">Полный список клиентских библиотек API Twilio, которые доступны на разных языках, см. на [этой странице][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="87bac-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="87bac-126">Ключевые аспекты hello Twilio API, Twilio глаголов и язык разметки Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="87bac-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="87bac-127"><a id="Verbs"></a>Команды Twilio</span><span class="sxs-lookup"><span data-stu-id="87bac-127"><a id="Verbs"></a>Twilio verbs</span></span>
<span data-ttu-id="87bac-128">Hello API использует Twilio команд; Например, hello  **&lt;Say&gt;**  команда предписывает Twilio tooaudibly доставить сообщение во время вызова.</span><span class="sxs-lookup"><span data-stu-id="87bac-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="87bac-129">Hello ниже приведен список команд, Twilio.</span><span class="sxs-lookup"><span data-stu-id="87bac-129">hello following is a list of Twilio verbs.</span></span>  <span data-ttu-id="87bac-130">Дополнительные сведения о hello других команд и возможностей через [документации язык разметки Twilio](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="87bac-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="87bac-131">**&lt;Удаленный&gt;**: подключается phone tooanother hello вызывающего объекта.</span><span class="sxs-lookup"><span data-stu-id="87bac-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="87bac-132">**&lt;Соберите&gt;**: собирает цифры, введенные на клавиатуре телефона hello.</span><span class="sxs-lookup"><span data-stu-id="87bac-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="87bac-133">**&lt;Hangup&gt;**: окончание вызова.</span><span class="sxs-lookup"><span data-stu-id="87bac-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="87bac-134">**&lt;Play&gt;**: воспроизведение звукового файла.</span><span class="sxs-lookup"><span data-stu-id="87bac-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="87bac-135">**&lt;Pause&gt;**: бесшумное ожидание в течение указанного времени (в секундах).</span><span class="sxs-lookup"><span data-stu-id="87bac-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="87bac-136">**&lt;Запись&gt;**: записи голоса hello вызывающего объекта и возвращает URL-адрес файла, содержащего запись hello.</span><span class="sxs-lookup"><span data-stu-id="87bac-136">**&lt;Record&gt;**: Records hello caller's voice and returns an URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="87bac-137">**&lt;Перенаправить&gt;**: передает управление вызова или SMS toohello TwiML на другой URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="87bac-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="87bac-138">**&lt;Отклонить&gt;**: отклоняет во входящих вызова tooyour Twilio номер без выставления счетов, вы</span><span class="sxs-lookup"><span data-stu-id="87bac-138">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="87bac-139">**&lt;Предположим,&gt;**: toospeech преобразует текст, который выполняется при вызове функции.</span><span class="sxs-lookup"><span data-stu-id="87bac-139">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="87bac-140">**&lt;Sms&gt;**: отправка SMS-сообщения.</span><span class="sxs-lookup"><span data-stu-id="87bac-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="87bac-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="87bac-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="87bac-142">TwiML — это набор инструкций, основанный на XML основании hello Twilio команд, которые сообщают Twilio того, как tooprocess звонок или SMS.</span><span class="sxs-lookup"><span data-stu-id="87bac-142">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="87bac-143">Например, следующие TwiML hello бы преобразование текста hello **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="87bac-143">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="87bac-144">Когда приложение вызывает hello Twilio API, один из параметров API hello, hello URL-адрес, который возвращает ответ TwiML hello.</span><span class="sxs-lookup"><span data-stu-id="87bac-144">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="87bac-145">В целях разработки можно использовать предоставляемые системой Twilio URL-адреса hello tooprovide TwiML ответов, используемых приложениями.</span><span class="sxs-lookup"><span data-stu-id="87bac-145">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="87bac-146">Может также содержать собственные ответы TwiML hello tooproduce URL-адресов и другой вариант — toouse hello **TwiMLResponse** объекта.</span><span class="sxs-lookup"><span data-stu-id="87bac-146">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="87bac-147">Дополнительные сведения о командах Twilio, их атрибутах и TwiML см. на странице [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="87bac-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="87bac-148">Дополнительные сведения о hello Twilio API см. в разделе [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="87bac-148">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="87bac-149"><a id="CreateAccount"></a>Создание учетной записи Twilio</span><span class="sxs-lookup"><span data-stu-id="87bac-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="87bac-150">Когда вы будете готовы tooget учетной записи Twilio, зарегистрируйтесь на [повторите Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="87bac-150">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="87bac-151">Вы можете начать с бесплатной учетной записи и обновить ее позднее.</span><span class="sxs-lookup"><span data-stu-id="87bac-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="87bac-152">При регистрации учетной записи Twilio, вы получите идентификатор учетной записи и маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="87bac-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="87bac-153">Как будет toomake необходимые вызовы Twilio API.</span><span class="sxs-lookup"><span data-stu-id="87bac-153">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="87bac-154">tooprevent несанкционированный доступ к учетной записи tooyour, безопасность срок действия токена проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="87bac-154">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="87bac-155">Идентификатор учетной записи и проверки подлинности маркера могут быть просмотрены в hello [странице учетной записи Twilio][twilio_account]в hello поля с меткой **ИД безопасности учетной записи** и **ТОКЕНА проверки Подлинности**соответственно.</span><span class="sxs-lookup"><span data-stu-id="87bac-155">Your account ID and authentication token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="87bac-156"><a id="create_app"></a>Создание приложения Azure</span><span class="sxs-lookup"><span data-stu-id="87bac-156"><a id="create_app"></a>Create an Azure Application</span></span>
<span data-ttu-id="87bac-157">Приложение Azure, на котором размещается приложение с поддержкой Twilio, ничем не отличается от любого другого приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="87bac-157">An Azure application that hosts a Twilio enabled application is no different from any other Azure application.</span></span> <span data-ttu-id="87bac-158">Добавление библиотеки Twilio .NET hello и настроить hello роли toouse hello Twilio .NET библиотеки.</span><span class="sxs-lookup"><span data-stu-id="87bac-158">You add hello Twilio .NET library and configure hello role toouse hello Twilio .NET libraries.</span></span>
<span data-ttu-id="87bac-159">Сведения о создании начального проекта Azure с помощью Visual Studio см. на [этой странице][vs_project].</span><span class="sxs-lookup"><span data-stu-id="87bac-159">For information on creating an initial Azure project, see [Creating an Azure project with Visual Studio][vs_project].</span></span>

## <span data-ttu-id="87bac-160"><a id="configure_app"></a>Настройка приложения toouse Twilio библиотек</span><span class="sxs-lookup"><span data-stu-id="87bac-160"><a id="configure_app"></a>Configure Your Application toouse Twilio Libraries</span></span>
<span data-ttu-id="87bac-161">Twilio предоставляет набор вспомогательных библиотек .NET, являющиеся оболочками для различных аспектов toointeract простой и легко tooprovide Twilio с Twilio REST API hello и клиента Twilio toogenerate TwiML ответов.</span><span class="sxs-lookup"><span data-stu-id="87bac-161">Twilio provides a set of .NET helper libraries that wrap various aspects of Twilio tooprovide simple and easy ways toointeract with hello Twilio REST API and Twilio Client toogenerate TwiML responses.</span></span>

<span data-ttu-id="87bac-162">Twilio предоставляет пять библиотек для разработчиков .NET:</span><span class="sxs-lookup"><span data-stu-id="87bac-162">Twilio provides five libraries for .NET developers:</span></span>
<span data-ttu-id="87bac-163">Библиотека</span><span class="sxs-lookup"><span data-stu-id="87bac-163">Library</span></span>|<span data-ttu-id="87bac-164">Описание</span><span class="sxs-lookup"><span data-stu-id="87bac-164">Description</span></span>
---|---
<span data-ttu-id="87bac-165">Twilio.API</span><span class="sxs-lookup"><span data-stu-id="87bac-165">Twilio.API</span></span>|<span data-ttu-id="87bac-166">Twilio библиотеки ядра Hello, которая создает оболочку для API-интерфейса REST Twilio hello понятное библиотеки .NET.</span><span class="sxs-lookup"><span data-stu-id="87bac-166">hello core Twilio library that wraps hello Twilio REST API in a friendly .NET library.</span></span> <span data-ttu-id="87bac-167">Эта библиотека доступна для .NET, Silverlight и Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="87bac-167">This library is available for .NET, Silverlight, and Windows Phone 7.</span></span>
<span data-ttu-id="87bac-168">Twilio.TwiML</span><span class="sxs-lookup"><span data-stu-id="87bac-168">Twilio.TwiML</span></span>|<span data-ttu-id="87bac-169">Предоставляет разметку TwiML toogenerate .NET понятным способом.</span><span class="sxs-lookup"><span data-stu-id="87bac-169">Provides a .NET friendly way toogenerate TwiML markup.</span></span>
<span data-ttu-id="87bac-170">Twilio.MVC</span><span class="sxs-lookup"><span data-stu-id="87bac-170">Twilio.MVC</span></span>|<span data-ttu-id="87bac-171">Для разработчиков, использующих ASP.NET MVC, эта библиотека включает в себя TwilioController, TwiML ActionResult и атрибут проверки запроса.</span><span class="sxs-lookup"><span data-stu-id="87bac-171">For developers using ASP.NET MVC, this library includes a TwilioController, TwiML ActionResult, and request validation attribute.</span></span>
<span data-ttu-id="87bac-172">Twilio.WebMatrix</span><span class="sxs-lookup"><span data-stu-id="87bac-172">Twilio.WebMatrix</span></span>|<span data-ttu-id="87bac-173">Для разработчиков, использующих бесплатное средство разработки WebMatrix от Microsoft, эта библиотека содержит помощники синтаксиса Razor для выполнения различных действий Twilio.</span><span class="sxs-lookup"><span data-stu-id="87bac-173">For developers using Microsoft's free WebMatrix development tool, this library contains Razor syntax helpers for various Twilio actions.</span></span>
<span data-ttu-id="87bac-174">Twilio.Client.Capability</span><span class="sxs-lookup"><span data-stu-id="87bac-174">Twilio.Client.Capability</span></span>|<span data-ttu-id="87bac-175">Содержит маркера генератор hello возможностей для использования с hello Twilio клиента JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="87bac-175">Contains hello Capability token generator for use with hello Twilio Client JavaScript SDK.</span></span>

<span data-ttu-id="87bac-176">Обратите внимание, что для всех библиотек требуется .NET 3.5, Silverlight 4 и Windows Phone 7 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="87bac-176">Note that all libraries require .NET 3.5, Silverlight 4, or Windows Phone 7 or later.</span></span>

<span data-ttu-id="87bac-177">Hello образцы, описанные в настоящем руководстве используйте библиотеку Twilio.API hello.</span><span class="sxs-lookup"><span data-stu-id="87bac-177">hello samples provided in this guide use hello Twilio.API library.</span></span>

<span data-ttu-id="87bac-178">Hello библиотеки могут быть [установить с помощью расширения диспетчера пакетов NuGet hello](http://www.twilio.com/docs/csharp/install) доступны для Visual Studio 2010 копии too2015.</span><span class="sxs-lookup"><span data-stu-id="87bac-178">hello libraries can be [installed using hello NuGet package manager extension](http://www.twilio.com/docs/csharp/install) available for Visual Studio 2010 up too2015.</span></span>  <span data-ttu-id="87bac-179">Hello исходный код размещается на [GitHub][twilio_github_repo], который включает вики-сайт, который содержит полную документацию по использованию библиотеки hello.</span><span class="sxs-lookup"><span data-stu-id="87bac-179">hello source code is hosted on [GitHub][twilio_github_repo], which includes a Wiki that contains complete documentation for using hello libraries.</span></span>

<span data-ttu-id="87bac-180">По умолчанию Microsoft Visual Studio 2010 устанавливает NuGet версии 1.2.</span><span class="sxs-lookup"><span data-stu-id="87bac-180">By default, Microsoft Visual Studio 2010 installs version 1.2 of NuGet.</span></span> <span data-ttu-id="87bac-181">Установка библиотек Twilio hello требуется версия 1.6 NuGet или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="87bac-181">Installing hello Twilio libraries requires version 1.6 of NuGet or higher.</span></span> <span data-ttu-id="87bac-182">Дополнительные сведения об установке или обновлении NuGet см. на веб-сайте [http://nuget.org/][nuget].</span><span class="sxs-lookup"><span data-stu-id="87bac-182">For information on installing or updating NuGet, see [http://nuget.org/][nuget].</span></span>

> [!NOTE]
> <span data-ttu-id="87bac-183">tooinstall hello версию NuGet, сначала необходимо удалить hello Загруженная версия с помощью hello Диспетчер расширений Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="87bac-183">tooinstall hello latest version of NuGet, you must first uninstall hello loaded version using hello Visual Studio Extension Manager.</span></span> <span data-ttu-id="87bac-184">toodo таким образом, необходимо запустить Visual Studio от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="87bac-184">toodo so, you must run Visual Studio as administrator.</span></span> <span data-ttu-id="87bac-185">В противном случае будет отключена кнопка удаления hello.</span><span class="sxs-lookup"><span data-stu-id="87bac-185">Otherwise, hello Uninstall button is disabled.</span></span>
>
>

### <span data-ttu-id="87bac-186"><a id="use_nuget"></a>tooadd hello Twilio библиотеки tooyour проекта Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="87bac-186"><a id="use_nuget"></a>tooadd hello Twilio libraries tooyour Visual Studio project:</span></span>
1. <span data-ttu-id="87bac-187">Откройте решение в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="87bac-187">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="87bac-188">Щелкните правой кнопкой мыши **References**(Ссылки).</span><span class="sxs-lookup"><span data-stu-id="87bac-188">Right-click **References**.</span></span>
3. <span data-ttu-id="87bac-189">Щелкните **Manage NuGet Packages...**</span><span class="sxs-lookup"><span data-stu-id="87bac-189">Click **Manage NuGet Packages...**</span></span>
4. <span data-ttu-id="87bac-190">Щелкните **Online**(В сети).</span><span class="sxs-lookup"><span data-stu-id="87bac-190">Click **Online**.</span></span>
5. <span data-ttu-id="87bac-191">В hello поиска online введите *twilio*.</span><span class="sxs-lookup"><span data-stu-id="87bac-191">In hello search online box, type *twilio*.</span></span>
6. <span data-ttu-id="87bac-192">Нажмите кнопку **установить** hello Twilio пакета.</span><span class="sxs-lookup"><span data-stu-id="87bac-192">Click **Install** on hello Twilio package.</span></span>

## <span data-ttu-id="87bac-193"><a id="howto_make_call"></a>Практическое руководство. Осуществление исходящего вызова</span><span class="sxs-lookup"><span data-stu-id="87bac-193"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="87bac-194">Hello ниже показано, как исходящий toomake вызвать с помощью hello **CallResource** класса.</span><span class="sxs-lookup"><span data-stu-id="87bac-194">hello following shows how toomake an outgoing call using hello **CallResource** class.</span></span> <span data-ttu-id="87bac-195">Этот код также использует предоставляемые системой Twilio сайта tooreturn hello ответ языка разметки Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="87bac-195">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="87bac-196">Подставьте собственные значения hello **для** и **из** номера телефонов и убедитесь в правильности hello **из** телефонный номер для учетной записи Twilio перед выполнением кода hello.</span><span class="sxs-lookup"><span data-stu-id="87bac-196">Substitute your values for hello **to** and **from** phone numbers, and ensure that you verify hello **from** phone number for your Twilio account before running hello code.</span></span>

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

<span data-ttu-id="87bac-197">Дополнительные сведения о параметрах hello, передаваемых в toohello **CallResource.Create** метода, в разделе [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="87bac-197">For more information about hello parameters passed in toohello **CallResource.Create** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="87bac-198">Как уже упоминалось, этот код использует hello tooreturn Twilio техники сайта TwiML ответа.</span><span class="sxs-lookup"><span data-stu-id="87bac-198">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="87bac-199">Можно использовать собственный узел tooprovide hello TwiML ответа.</span><span class="sxs-lookup"><span data-stu-id="87bac-199">You could instead use your own site tooprovide hello TwiML response.</span></span> <span data-ttu-id="87bac-200">Дополнительные сведения см. в разделе [Практическое руководство. Предоставление ответа TwiML с собственного веб-сайта](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="87bac-200">For more information, see [How to: Provide TwiML responses from your own website](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="87bac-201"><a id="howto_send_sms"></a>Практическое руководство. Отправка SMS-сообщения</span><span class="sxs-lookup"><span data-stu-id="87bac-201"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="87bac-202">Hello следующем снимке экрана показано, как hello toosend сообщение SMS с помощью **MessageResource** класса.</span><span class="sxs-lookup"><span data-stu-id="87bac-202">hello following screenshot shows how toosend an SMS message using hello **MessageResource**  class.</span></span> <span data-ttu-id="87bac-203">Hello **из** номер обеспечивается Twilio для пробной версии учетных записей toosend SMS-сообщений.</span><span class="sxs-lookup"><span data-stu-id="87bac-203">hello **from** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="87bac-204">Hello **для** необходимо проверить номер для учетной записи Twilio, перед выполнением кода hello.</span><span class="sxs-lookup"><span data-stu-id="87bac-204">hello **to** number must be verified for your Twilio account before you run hello code.</span></span>

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

## <span data-ttu-id="87bac-205"><a id="howto_provide_twiml_responses"></a>Практическое руководство. Предоставление откликов TwiML с вашего веб-сайта</span><span class="sxs-lookup"><span data-stu-id="87bac-205"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own website</span></span>
<span data-ttu-id="87bac-206">Когда приложения так, инициирует вызов toohello Twilio API - через hello **CallResource.Create** метод - Twilio отправляет вашей tooan URL-адрес запроса, ожидаемый tooreturn TwiML ответ.</span><span class="sxs-lookup"><span data-stu-id="87bac-206">When your application initiates a call toohello Twilio API - for example, via hello **CallResource.Create** method - Twilio sends your request tooan URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="87bac-207">пример Hello в [как: Убедитесь, исходящий вызов](#howto_make_call) использует Здравствуйте, предоставляемых системой Twilio URL-адрес [http://twimlets.com/message] [ twimlet_message_url] tooreturn hello ответа.</span><span class="sxs-lookup"><span data-stu-id="87bac-207">hello example in [How to: Make an outgoing call](#howto_make_call) uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url] tooreturn hello response.</span></span>

> [!NOTE]
> <span data-ttu-id="87bac-208">Хотя TwiML предназначен для использования веб-службами, hello TwiML можно просмотреть в браузере.</span><span class="sxs-lookup"><span data-stu-id="87bac-208">While TwiML is designed for use by web services, you can view hello TwiML in your browser.</span></span> <span data-ttu-id="87bac-209">Например, щелкните [http://twimlets.com/message] [ twimlet_message_url] toosee пустой &lt;ответ&gt; элемента; еще один пример, нажмите кнопку [http://twimlets.com/message ? Сообщение 5B0 %% 5 D = Hello % 20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee &lt;ответа&gt; элемент, содержащий &lt;Say&gt; элемент.</span><span class="sxs-lookup"><span data-stu-id="87bac-209">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty &lt;Response&gt; element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee a &lt;Response&gt; element that contains a &lt;Say&gt; element.</span></span>
>
>

<span data-ttu-id="87bac-210">Вместо hello Twilio предоставленный URL-адрес, можно создать собственного URL-адрес веб-сайта, возвращающий HTTP-ответов.</span><span class="sxs-lookup"><span data-stu-id="87bac-210">Instead of relying on hello Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="87bac-211">Можно создать сайт hello на любом языке, который возвращает HTTP-ответов.</span><span class="sxs-lookup"><span data-stu-id="87bac-211">You can create hello site in any language that returns HTTP responses.</span></span> <span data-ttu-id="87bac-212">В этом разделе предполагается, что будет размещение hello URL-адрес из обработчика универсальных ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="87bac-212">This topic assumes you'll be hosting hello URL from an ASP.NET generic handler.</span></span>

<span data-ttu-id="87bac-213">следующий обработчик ASP.NET Hello crafts TwiML ответ, который говорит **Hello World** при вызове функции hello.</span><span class="sxs-lookup"><span data-stu-id="87bac-213">hello following ASP.NET Handler crafts a TwiML response that says **Hello World** on hello call.</span></span>

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
    
<span data-ttu-id="87bac-214">Как видно в приведенном выше примере hello hello TwiML ответа является просто XML-документа.</span><span class="sxs-lookup"><span data-stu-id="87bac-214">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="87bac-215">Библиотека Twilio.TwiML Hello содержит классы, которые создают TwiML для вас.</span><span class="sxs-lookup"><span data-stu-id="87bac-215">hello Twilio.TwiML library contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="87bac-216">Hello приведенном ниже примере создает эквивалентный ответа hello, как показано выше, но использует hello **VoiceResponse** класса.</span><span class="sxs-lookup"><span data-stu-id="87bac-216">hello example below produces hello equivalent response as shown above, but uses hello **VoiceResponse** class.</span></span>

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

<span data-ttu-id="87bac-217">Дополнительные сведения о TwiML см. по следующему адресу: [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="87bac-217">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span></span>

<span data-ttu-id="87bac-218">После настройки ответы TwiML tooprovide способом можно передать этот URL-адрес toohello **CallResource.Create** метод.</span><span class="sxs-lookup"><span data-stu-id="87bac-218">Once you have set up a way tooprovide TwiML responses, you can pass that URL toohello **CallResource.Create** method.</span></span> <span data-ttu-id="87bac-219">Например, если у вас есть веб-приложения с именем tooan MyTwiML развертывания облачной службы Azure, а hello обработчиком ASP.NET называется mytwiml.ashx, hello URL-адрес можно передать слишком**CallResource.Create** как показано в следующим hello Пример:</span><span class="sxs-lookup"><span data-stu-id="87bac-219">For example, if you have a web application named MyTwiML deployed tooan Azure cloud service, and hello name of your ASP.NET Handler is mytwiml.ashx, hello URL can be passed too**CallResource.Create** as shown in hello following code sample:</span></span>

    // This sample uses hello sandbox number provided by Twilio toomake hello call.
    // Place hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

<span data-ttu-id="87bac-220">Дополнительные сведения об использовании Twilio в Azure с помощью ASP.NET см. в разделе [как toomake вызвать с использованием Twilio в веб-роли в Azure Телефон][howto_phonecall_dotnet].</span><span class="sxs-lookup"><span data-stu-id="87bac-220">For additional information about using Twilio on Azure with ASP.NET, see [How toomake a phone call using Twilio in a web role on Azure][howto_phonecall_dotnet].</span></span>

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
