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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-python"></a><span data-ttu-id="a52e8-104">Как tooUse Twilio для голосовых возможностей и SMS на Python</span><span class="sxs-lookup"><span data-stu-id="a52e8-104">How tooUse Twilio for Voice and SMS Capabilities in Python</span></span>
<span data-ttu-id="a52e8-105">В этом руководстве показано, как tooperform часто встречающиеся задачи программирования с hello Twilio API службы в Azure.</span><span class="sxs-lookup"><span data-stu-id="a52e8-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="a52e8-106">Hello сценарии включают телефонных звонков и отправке сообщения службы коротких сообщений (SMS).</span><span class="sxs-lookup"><span data-stu-id="a52e8-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="a52e8-107">Дополнительные сведения о Twilio и использования голоса и SMS в приложениях см. в разделе hello [дальнейшие действия](#NextSteps) раздела.</span><span class="sxs-lookup"><span data-stu-id="a52e8-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="a52e8-108"><a id="WhatIs"></a>Что такое Twilio?</span><span class="sxs-lookup"><span data-stu-id="a52e8-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="a52e8-109">Twilio включении hello будущее делового общения, включение разработчики tooembed голос, VoIP и обмен сообщениями в приложения.</span><span class="sxs-lookup"><span data-stu-id="a52e8-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="a52e8-110">Они виртуализация всех инфраструктуру в среде облачных, глобальные, предоставляя его через hello Twilio communications API платформы.</span><span class="sxs-lookup"><span data-stu-id="a52e8-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="a52e8-111">Приложения, простой toobuild и масштабируемость.</span><span class="sxs-lookup"><span data-stu-id="a52e8-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="a52e8-112">Оцените гибкость повременной оплаты, а также преимущества, связанные с надежностью облачных решений.</span><span class="sxs-lookup"><span data-stu-id="a52e8-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="a52e8-113">**Голосовой Twilio** позволяет toomake вашего приложения и приема телефонных звонков.</span><span class="sxs-lookup"><span data-stu-id="a52e8-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span>
<span data-ttu-id="a52e8-114">**Twilio SMS** позволяет toosend вашего приложения и получать текстовые сообщения.</span><span class="sxs-lookup"><span data-stu-id="a52e8-114">**Twilio SMS** enables your application toosend and receive text messages.</span></span>
<span data-ttu-id="a52e8-115">**Клиента Twilio** позволяет toomake VoIP вызовы из любой телефон, планшет или браузера и поддерживает WebRTC.</span><span class="sxs-lookup"><span data-stu-id="a52e8-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="a52e8-116"><a id="Pricing"></a>Цены и специальные предложения Twilio</span><span class="sxs-lookup"><span data-stu-id="a52e8-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="a52e8-117">Клиентам Azure доступно [специальное предложение][special_offer]: кредит Twilio в размере 10 долл. США при обновлении учетной записи Twilio.</span><span class="sxs-lookup"><span data-stu-id="a52e8-117">Azure customers receive a [special offer][special_offer] $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="a52e8-118">Это кредит Twilio может быть применен tooany Twilio использования ($10 кредит эквивалентные toosending до 1 000 SMS-сообщений или получение копии too1000 входящих голосовых минут, в зависимости от расположения hello ваш телефонный номер и сообщений или вызовов назначения).</span><span class="sxs-lookup"><span data-stu-id="a52e8-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="a52e8-119">Получите этот [кредит Twilio][special_offer] и приступите к работе.</span><span class="sxs-lookup"><span data-stu-id="a52e8-119">Redeem this [Twilio credit][special_offer] and get started.</span></span>

<span data-ttu-id="a52e8-120">Twilio представляет собой службу с повременной оплатой.</span><span class="sxs-lookup"><span data-stu-id="a52e8-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="a52e8-121">Стартовые платежи отсутствуют, а учетную запись можно закрыть в любое время.</span><span class="sxs-lookup"><span data-stu-id="a52e8-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="a52e8-122">Дополнительные сведения см. в статье [Цены на Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="a52e8-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="a52e8-123"><a id="Concepts"></a>Основные понятия</span><span class="sxs-lookup"><span data-stu-id="a52e8-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="a52e8-124">Hello Twilio API является API RESTful, который предоставляет функциональные возможности SMS и голосовой для приложений.</span><span class="sxs-lookup"><span data-stu-id="a52e8-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="a52e8-125">Полный список клиентских библиотек API Twilio, которые доступны на разных языках, см. на [этой странице][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="a52e8-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="a52e8-126">Ключевые аспекты hello Twilio API, Twilio глаголов и язык разметки Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="a52e8-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="a52e8-127"><a id="Verbs"></a>Команды Twilio</span><span class="sxs-lookup"><span data-stu-id="a52e8-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="a52e8-128">Hello API использует Twilio команд; Например, hello  **&lt;Say&gt;**  команда предписывает Twilio tooaudibly доставить сообщение во время вызова.</span><span class="sxs-lookup"><span data-stu-id="a52e8-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="a52e8-129">Hello ниже приведен список команд, Twilio.</span><span class="sxs-lookup"><span data-stu-id="a52e8-129">hello following is a list of Twilio verbs.</span></span> <span data-ttu-id="a52e8-130">Дополнительные сведения о hello других команд и возможностей через [документации язык разметки Twilio][twiml].</span><span class="sxs-lookup"><span data-stu-id="a52e8-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation][twiml].</span></span>

* <span data-ttu-id="a52e8-131">**&lt;Удаленный&gt;**: подключается phone tooanother hello вызывающего объекта.</span><span class="sxs-lookup"><span data-stu-id="a52e8-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="a52e8-132">**&lt;Соберите&gt;**: собирает цифры, введенные на клавиатуре телефона hello.</span><span class="sxs-lookup"><span data-stu-id="a52e8-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="a52e8-133">**&lt;Hangup&gt;**: окончание вызова.</span><span class="sxs-lookup"><span data-stu-id="a52e8-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="a52e8-134">**&lt;Pause&gt;**: бесшумное ожидание в течение указанного времени (в секундах).</span><span class="sxs-lookup"><span data-stu-id="a52e8-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="a52e8-135">**&lt;Play&gt;**: воспроизведение звукового файла.</span><span class="sxs-lookup"><span data-stu-id="a52e8-135">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="a52e8-136">**&lt;Очередь&gt;**: добавить очередь tooa hello вызывающих объектов.</span><span class="sxs-lookup"><span data-stu-id="a52e8-136">**&lt;Queue&gt;**: Add hello tooa queue of callers.</span></span>
* <span data-ttu-id="a52e8-137">**&lt;Запись&gt;**: записи голоса hello hello вызывающего объекта и возвращает URL-адрес файла, содержащего запись hello.</span><span class="sxs-lookup"><span data-stu-id="a52e8-137">**&lt;Record&gt;**: Records hello voice of hello caller and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="a52e8-138">**&lt;Перенаправить&gt;**: передает управление вызова или SMS toohello TwiML на другой URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="a52e8-138">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="a52e8-139">**&lt;Отклонить&gt;**: отклоняет во входящих вызова tooyour Twilio номер без выставления счетов за вас.</span><span class="sxs-lookup"><span data-stu-id="a52e8-139">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you.</span></span>
* <span data-ttu-id="a52e8-140">**&lt;Предположим,&gt;**: toospeech преобразует текст, который выполняется при вызове функции.</span><span class="sxs-lookup"><span data-stu-id="a52e8-140">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="a52e8-141">**&lt;Sms&gt;**: отправка SMS-сообщения.</span><span class="sxs-lookup"><span data-stu-id="a52e8-141">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="a52e8-142"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="a52e8-142"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="a52e8-143">TwiML — это набор инструкций, основанный на XML основании hello Twilio команд, которые сообщают Twilio того, как tooprocess звонок или SMS.</span><span class="sxs-lookup"><span data-stu-id="a52e8-143">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="a52e8-144">Например, следующие TwiML hello бы преобразование текста hello **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="a52e8-144">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="a52e8-145">Когда приложение вызывает hello Twilio API, один из параметров API hello, hello URL-адрес, который возвращает ответ TwiML hello.</span><span class="sxs-lookup"><span data-stu-id="a52e8-145">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="a52e8-146">В целях разработки можно использовать предоставляемые системой Twilio URL-адреса hello tooprovide TwiML ответов, используемых приложениями.</span><span class="sxs-lookup"><span data-stu-id="a52e8-146">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="a52e8-147">Может также содержать собственные ответы TwiML hello tooproduce URL-адресов и другой вариант — toouse hello `TwiMLResponse` объекта.</span><span class="sxs-lookup"><span data-stu-id="a52e8-147">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello `TwiMLResponse` object.</span></span>

<span data-ttu-id="a52e8-148">Дополнительные сведения о командах Twilio, их атрибутах и TwiML см. на странице [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="a52e8-148">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="a52e8-149">Дополнительные сведения о hello Twilio API см. в разделе [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="a52e8-149">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="a52e8-150"><a id="CreateAccount"></a>Создание учетной записи Twilio</span><span class="sxs-lookup"><span data-stu-id="a52e8-150"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="a52e8-151">Когда вы будете готовы tooget учетной записи Twilio, зарегистрируйтесь на [повторите Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="a52e8-151">When you are ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="a52e8-152">Вы можете начать с бесплатной учетной записи и обновить ее позднее.</span><span class="sxs-lookup"><span data-stu-id="a52e8-152">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="a52e8-153">При регистрации учетной записи Twilio вы получите идентификатор безопасности учетной записи и маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="a52e8-153">When you sign up for a Twilio account, you receive an account SID and an authentication token.</span></span> <span data-ttu-id="a52e8-154">Как будет toomake необходимые вызовы Twilio API.</span><span class="sxs-lookup"><span data-stu-id="a52e8-154">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="a52e8-155">tooprevent несанкционированный доступ к учетной записи tooyour, безопасность срок действия токена проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="a52e8-155">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="a52e8-156">Ваш ИД безопасности учетной записи и токена проверки подлинности можно просмотреть в hello [консоли Twilio][twilio_console]в hello поля с меткой **ИД безопасности учетной записи** и **ТОКЕНА проверки Подлинности**соответственно.</span><span class="sxs-lookup"><span data-stu-id="a52e8-156">Your account SID and authentication token are viewable in hello [Twilio Console][twilio_console], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="a52e8-157"><a id="create_app"></a> Создание приложения Python</span><span class="sxs-lookup"><span data-stu-id="a52e8-157"><a id="create_app"></a>Create a Python Application</span></span>
<span data-ttu-id="a52e8-158">Приложения Python, которое использует службу hello Twilio и работает в Azure не отличается от любого другого приложения Python, использующего службу hello Twilio.</span><span class="sxs-lookup"><span data-stu-id="a52e8-158">A Python application that uses hello Twilio service and is running in Azure is no different than any other Python application that uses hello Twilio service.</span></span> <span data-ttu-id="a52e8-159">Хотя Twilio служб на основе REST и может вызываться из Python несколькими способами, в этой статье основное внимание уделяется как toouse Twilio служб с [Twilio библиотеки для Python из GitHub][twilio_python].</span><span class="sxs-lookup"><span data-stu-id="a52e8-159">While Twilio services are REST-based and can be called from Python in several ways, this article will focus on how toouse Twilio services with [Twilio library for Python from GitHub][twilio_python].</span></span> <span data-ttu-id="a52e8-160">Дополнительные сведения об использовании библиотеки hello Twilio для Python см. в разделе [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="a52e8-160">For more information about using hello Twilio library for Python, see [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="a52e8-161">Во-первых, [установки новой виртуальной Машины Linux Azure] [azure_vm_setup] tooact в качестве узла для нового веб-приложения Python.</span><span class="sxs-lookup"><span data-stu-id="a52e8-161">First, [set-up a new Azure Linux VM][azure_vm_setup] tooact as a host for your new Python web application.</span></span> <span data-ttu-id="a52e8-162">После того, как hello виртуальная машина запущена, будет должны tooexpose приложения на открытый порт, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="a52e8-162">Once hello Virtual Machine is running, you will need tooexpose your application on a public port as described below.</span></span>

### <a name="add-an-incoming-rule"></a><span data-ttu-id="a52e8-163">Добавление правила для входящего трафика</span><span class="sxs-lookup"><span data-stu-id="a52e8-163">Add An Incoming Rule</span></span>
  1. <span data-ttu-id="a52e8-164">Go [сетевую группу безопасности] [azure_nsg] toohello страницы.</span><span class="sxs-lookup"><span data-stu-id="a52e8-164">Go toohello [Network Security Group][azure_nsg] page.</span></span>
  2. <span data-ttu-id="a52e8-165">Выберите hello сетевая группа безопасности, соответствующий с вашей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a52e8-165">Select hello Network Security Group that corresponds with your Virtual Machine.</span></span>
  3. <span data-ttu-id="a52e8-166">Добавьте **Правило для исходящего трафика** для **порта 80**.</span><span class="sxs-lookup"><span data-stu-id="a52e8-166">Add and **Outgoing Rule** for **port 80**.</span></span> <span data-ttu-id="a52e8-167">Убедиться, что tooallow быть входящих с любых адресов.</span><span class="sxs-lookup"><span data-stu-id="a52e8-167">Be sure tooallow incoming from any address.</span></span>

### <a name="set-hello-dns-name-label"></a><span data-ttu-id="a52e8-168">Набор hello метка DNS-имени</span><span class="sxs-lookup"><span data-stu-id="a52e8-168">Set hello DNS Name Label</span></span>
  1. <span data-ttu-id="a52e8-169">Go toohello [hello открытый IP-адресов] [azure_ips] страницы.</span><span class="sxs-lookup"><span data-stu-id="a52e8-169">Go toohello [hello Public IP Adresses][azure_ips] page.</span></span>
  2. <span data-ttu-id="a52e8-170">Выберите общедоступный IP-адрес, correspends с вашей виртуальной машиной hello.</span><span class="sxs-lookup"><span data-stu-id="a52e8-170">Select hello Public IP that correspends with your Virtual Machine.</span></span>
  3. <span data-ttu-id="a52e8-171">Набор hello **метка DNS-имени** в hello **конфигурации** раздела.</span><span class="sxs-lookup"><span data-stu-id="a52e8-171">Set hello **DNS Name Label** in hello **Configuration** section.</span></span> <span data-ttu-id="a52e8-172">В случае hello в этом примере это будет выглядеть примерно следующим образом *your метка доменного*. centralus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="a52e8-172">In hello case of this example it will look something like this *your-domain-label*.centralus.cloudapp.azure.com</span></span>

<span data-ttu-id="a52e8-173">Здравствуйте после можно tooconnect через SSH toohello виртуальной машины, можно установить веб-платформа, по вашему выбору (hello два наиболее хорошо известен в Python, [термосе](http://flask.pocoo.org/) и [Django](https://www.djangoproject.com)).</span><span class="sxs-lookup"><span data-stu-id="a52e8-173">Once you are able tooconnect through SSH toohello Virtual Machine you can install hello Web Framework of your choice (hello two most well known in Python being [Flask](http://flask.pocoo.org/) and [Django](https://www.djangoproject.com)).</span></span> <span data-ttu-id="a52e8-174">Любое из них можно установить только выполнив hello `pip install` команды.</span><span class="sxs-lookup"><span data-stu-id="a52e8-174">You can install either of them just by running hello `pip install` command.</span></span>

<span data-ttu-id="a52e8-175">Имейте в виду, что настраивался hello виртуальной машины tooallow трафик только через порт 80.</span><span class="sxs-lookup"><span data-stu-id="a52e8-175">Keep in mind that we configured hello Virtual Machine tooallow traffic only on port 80.</span></span> <span data-ttu-id="a52e8-176">Поэтому следует убедиться, что toouse приложения hello tooconfigure этот порт.</span><span class="sxs-lookup"><span data-stu-id="a52e8-176">So make sure tooconfigure hello application toouse this port.</span></span>

## <span data-ttu-id="a52e8-177"><a id="configure_app"></a>Настройка приложения tooUse Twilio библиотек</span><span class="sxs-lookup"><span data-stu-id="a52e8-177"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="a52e8-178">Библиотеки приложения hello toouse Twilio для Python можно настроить двумя способами:</span><span class="sxs-lookup"><span data-stu-id="a52e8-178">You can configure your application toouse hello Twilio library for Python in two ways:</span></span>

* <span data-ttu-id="a52e8-179">Установка библиотеки Twilio hello Python виде PIP-адрес пакета.</span><span class="sxs-lookup"><span data-stu-id="a52e8-179">Install hello Twilio library for Python as a Pip package.</span></span> <span data-ttu-id="a52e8-180">Он может быть установлен с hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="a52e8-180">It can be installed with hello following commands:</span></span>
   
        $ pip install twilio

    <span data-ttu-id="a52e8-181">-ИЛИ-</span><span class="sxs-lookup"><span data-stu-id="a52e8-181">-OR-</span></span>

* <span data-ttu-id="a52e8-182">Загрузка библиотеки hello Twilio для Python с сайта GitHub ([https://github.com/twilio/twilio-python][twilio_python]) и установите его следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a52e8-182">Download hello Twilio library for Python from GitHub ([https://github.com/twilio/twilio-python][twilio_python]) and install it like this:</span></span>

        $ python setup.py install

<span data-ttu-id="a52e8-183">После установки библиотеки hello Twilio для Python, после этого можно `import` в Python файлов:</span><span class="sxs-lookup"><span data-stu-id="a52e8-183">Once you have installed hello Twilio library for Python, you can then `import` it in your Python files:</span></span>

        import twilio

<span data-ttu-id="a52e8-184">Дополнительные сведения см. в документе [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="a52e8-184">For more information, see [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="a52e8-185"><a id="howto_make_call"></a>Практическое руководство. Осуществление исходящего вызова</span><span class="sxs-lookup"><span data-stu-id="a52e8-185"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="a52e8-186">Следуя Hello показано, как вызвать toomake исходящего сообщения.</span><span class="sxs-lookup"><span data-stu-id="a52e8-186">hello following shows how toomake an outgoing call.</span></span> <span data-ttu-id="a52e8-187">Этот код также использует предоставляемые системой Twilio сайта tooreturn hello ответ языка разметки Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="a52e8-187">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="a52e8-188">Подставьте собственные значения hello **from_number** и **to_number** номера телефонов и убедитесь, что вы убедились hello **from_number** телефонный номер для учетной записи Twilio Прежде чем выполнение кода hello.</span><span class="sxs-lookup"><span data-stu-id="a52e8-188">Substitute your values for hello **from_number** and **to_number** phone numbers, and ensure that you've verified hello **from_number** phone number for your Twilio account before running hello code.</span></span>

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

<span data-ttu-id="a52e8-189">Как уже упоминалось, этот код использует hello tooreturn Twilio техники сайта TwiML ответа.</span><span class="sxs-lookup"><span data-stu-id="a52e8-189">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="a52e8-190">Можно использовать собственный узел tooprovide hello TwiML ответа; Дополнительные сведения см. в разделе [как tooProvide TwiML ответов от ваш собственный веб-сайт](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="a52e8-190">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="a52e8-191"><a id="howto_send_sms"></a>Практическое руководство. Отправка SMS-сообщения</span><span class="sxs-lookup"><span data-stu-id="a52e8-191"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="a52e8-192">Hello ниже показано, как сообщение SMS с помощью toosend hello `TwilioRestClient` класса.</span><span class="sxs-lookup"><span data-stu-id="a52e8-192">hello following shows how toosend an SMS message using hello `TwilioRestClient` class.</span></span> <span data-ttu-id="a52e8-193">Hello **from_number** номер обеспечивается Twilio для пробной версии учетных записей toosend SMS-сообщений.</span><span class="sxs-lookup"><span data-stu-id="a52e8-193">hello **from_number** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="a52e8-194">Hello **to_number** номер для учетной записи Twilio должна проверяться перед запуском кода hello.</span><span class="sxs-lookup"><span data-stu-id="a52e8-194">hello **to_number** number must be verified for your Twilio account before running hello code.</span></span>

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

## <span data-ttu-id="a52e8-195"><a id="howto_provide_twiml_responses"></a>Практическое руководство. Предоставление ответов TwiML с собственного веб-сайта</span><span class="sxs-lookup"><span data-stu-id="a52e8-195"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="a52e8-196">Когда приложение начинает toohello вызова Twilio API, Twilio будет отправлено на tooa URL-адрес запроса, ожидался tooreturn TwiML ответ.</span><span class="sxs-lookup"><span data-stu-id="a52e8-196">When your application initiates a call toohello Twilio API, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="a52e8-197">Hello выше примере hello Twilio предоставленный URL-адрес [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="a52e8-197">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="a52e8-198">(Хотя TwiML предназначается для использования службой Twilio, его можно также просмотреть в браузере.</span><span class="sxs-lookup"><span data-stu-id="a52e8-198">(While TwiML is designed for use by Twilio, you can view it in your browser.</span></span> <span data-ttu-id="a52e8-199">Например, щелкните [http://twimlets.com/message] [ twimlet_message_url] toosee пустой `<Response>` элемент; в качестве другого примера, нажмите кнопку [http://twimlets.com/message? Сообщения % 5B0 %5 D = Hello % 20World] [ twimlet_message_url_hello_world] toosee `<Response>` элемент, содержащий `<Say>` элемента.)</span><span class="sxs-lookup"><span data-stu-id="a52e8-199">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] toosee a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="a52e8-200">Вместо hello Twilio предоставленный URL-адрес, можно создать собственного веб-сайта, который возвращает HTTP-ответов.</span><span class="sxs-lookup"><span data-stu-id="a52e8-200">Instead of relying on hello Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="a52e8-201">Можно создать узел hello на любом языке, который возвращает XML-ответов; в этом разделе предполагается, что вы используете Python toocreate hello TwiML.</span><span class="sxs-lookup"><span data-stu-id="a52e8-201">You can create hello site in any language that returns XML responses; this topic assumes you will be using Python toocreate hello TwiML.</span></span>

<span data-ttu-id="a52e8-202">Hello следующие примеры будет выводить TwiML ответ, который говорит **Hello World** при вызове функции hello.</span><span class="sxs-lookup"><span data-stu-id="a52e8-202">hello following examples will output a TwiML response that says **Hello World** on hello call.</span></span>

<span data-ttu-id="a52e8-203">С помощью Flask:</span><span class="sxs-lookup"><span data-stu-id="a52e8-203">With Flask:</span></span>

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

<span data-ttu-id="a52e8-204">С помощью Django:</span><span class="sxs-lookup"><span data-stu-id="a52e8-204">With Django:</span></span>

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

<span data-ttu-id="a52e8-205">Как видно в приведенном выше примере hello hello TwiML ответа является просто XML-документа.</span><span class="sxs-lookup"><span data-stu-id="a52e8-205">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="a52e8-206">Библиотека Twilio Hello для Python содержит классы, которые создают TwiML для вас.</span><span class="sxs-lookup"><span data-stu-id="a52e8-206">hello Twilio library for Python contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="a52e8-207">Hello приведенном ниже примере создает эквивалентный ответа hello, как показано выше, но использует hello `twiml` модуль для Python hello Twilio библиотеки:</span><span class="sxs-lookup"><span data-stu-id="a52e8-207">hello example below produces hello equivalent response as shown above, but uses hello `twiml` module in hello Twilio library for Python:</span></span>

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

<span data-ttu-id="a52e8-208">Дополнительные сведения о TwiML см. по следующему адресу: [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="a52e8-208">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span>

<span data-ttu-id="a52e8-209">После настройки tooprovide TwiML ответов приложения Python, служит hello URL-адрес приложения hello hello URL-адреса, переданные в hello `client.calls.create` метод.</span><span class="sxs-lookup"><span data-stu-id="a52e8-209">Once you have your Python application set up tooprovide TwiML responses, use hello URL of hello application as hello URL passed into hello `client.calls.create`  method.</span></span> <span data-ttu-id="a52e8-210">Например, если у вас есть веб-приложения с именем **MyTwiML** развернутой tooan Azure размещенной службы, вы можете использовать его URL-адрес как веб-перехватчика, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="a52e8-210">For example, if you have a Web application named **MyTwiML** deployed tooan Azure hosted service, you can use its url as webhook as shown in hello following example:</span></span>

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

## <span data-ttu-id="a52e8-211"><a id="AdditionalServices"></a>Руководство: использование дополнительных служб Twilio</span><span class="sxs-lookup"><span data-stu-id="a52e8-211"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="a52e8-212">В дополнение к этому toohello в этой статье примерах, Twilio предлагает веб-API, можно использовать дополнительные возможности Twilio tooleverage из приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="a52e8-212">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="a52e8-213">Дополнительные сведения см. в разделе hello [документации по Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="a52e8-213">For full details, see hello [Twilio API documentation][twilio_api].</span></span>

## <span data-ttu-id="a52e8-214"><a id="NextSteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a52e8-214"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="a52e8-215">Теперь, когда вы изучили основы hello hello Twilio службы, выполните следующие дополнительные toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="a52e8-215">Now that you have learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="a52e8-216">[Рекомендации по безопасности Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="a52e8-216">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="a52e8-217">[Практические руководства по Twilio и примеры кода][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="a52e8-217">[Twilio HowTo Guides and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="a52e8-218">[Краткие учебники по Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="a52e8-218">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="a52e8-219">[Twilio на GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="a52e8-219">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="a52e8-220">[Обращайтесь tooTwilio поддержки][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="a52e8-220">[Talk tooTwilio Support][twilio_support]</span></span>

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
