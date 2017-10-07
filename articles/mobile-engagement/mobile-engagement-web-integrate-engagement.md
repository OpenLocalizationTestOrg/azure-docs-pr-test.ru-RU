---
title: "пакет SDK Mobile Engagement Web интеграции aaaAzure | Документы Microsoft"
description: "Здравствуйте, последние обновления и процедуры для hello Azure Mobile Engagement Web SDK"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: b5daa2a2-942b-489d-aa1d-568c3b25e56f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 02/29/2016
ms.author: piyushjo
ms.openlocfilehash: 99613b68b615bec4ddcfcc8e4e0133ce9d887bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a><span data-ttu-id="928b1-103">Интегрирование Служб мобильного взаимодействия Azure в веб-приложение</span><span class="sxs-lookup"><span data-stu-id="928b1-103">Integrate Azure Mobile Engagement in a web application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="928b1-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="928b1-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="928b1-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="928b1-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="928b1-106">iOS</span><span class="sxs-lookup"><span data-stu-id="928b1-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="928b1-107">Android</span><span class="sxs-lookup"><span data-stu-id="928b1-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="928b1-108">Hello в этой статье описывается hello простейший способ tooactivate hello аналитика и мониторинга в Azure Mobile Engagement в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="928b1-108">hello procedures in this article describe hello simplest way tooactivate hello analytics and monitoring functions in Azure Mobile Engagement in your web application.</span></span>

<span data-ttu-id="928b1-109">Выполните все статистические данные о пользователях, сеансах, действия, сбои и technicals hello действия tooactivate hello журнала отчетов, необходимые toocompute.</span><span class="sxs-lookup"><span data-stu-id="928b1-109">Follow hello steps tooactivate hello log reports that are needed toocompute all statistics about users, sessions, activities, crashes, and technicals.</span></span> <span data-ttu-id="928b1-110">Для статистики, связанные с приложением, например события, ошибок и задания необходимо активировать журнала отчетов вручную с помощью hello Azure Mobile Engagement API.</span><span class="sxs-lookup"><span data-stu-id="928b1-110">For application-dependent statistics, such as events, errors, and jobs, you must activate log reports manually by using hello Azure Mobile Engagement API.</span></span> <span data-ttu-id="928b1-111">Дополнительные сведения Узнайте [как toouse hello дополнительные теги API в веб-приложение Mobile Engagement](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="928b1-111">For more information, learn [how toouse hello advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="928b1-112">Введение</span><span class="sxs-lookup"><span data-stu-id="928b1-112">Introduction</span></span>
<span data-ttu-id="928b1-113">[Загрузите hello Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span><span class="sxs-lookup"><span data-stu-id="928b1-113">[Download hello Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span></span>
<span data-ttu-id="928b1-114">Привет, мобильных веб-Engagement пакет SDK поставляется как отдельный файл JavaScript, azure-engagement.js, у вас есть tooinclude на каждой странице сайта или веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="928b1-114">hello Mobile Engagement Web SDK is shipped as a single JavaScript file, azure-engagement.js, which you have tooinclude in each page of your site or web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="928b1-115">Перед запуском этого скрипта необходимо запустить скрипт или писать tooconfigure Mobile Engagement для вашего приложения фрагмент кода.</span><span class="sxs-lookup"><span data-stu-id="928b1-115">Before you run this script, you must run a script or code snippet that you write tooconfigure Mobile Engagement for your application.</span></span>
> 
> 

## <a name="browser-compatibility"></a><span data-ttu-id="928b1-116">Совместимость с браузерами</span><span class="sxs-lookup"><span data-stu-id="928b1-116">Browser compatibility</span></span>
<span data-ttu-id="928b1-117">Hello Mobile Engagement Web SDK использует собственный JSON кодирования и декодирования, кроме запросы AJAX toocross домена (полагаться на спецификации W3C CORS hello).</span><span class="sxs-lookup"><span data-stu-id="928b1-117">hello Mobile Engagement Web SDK uses native JSON encoding and decoding, in addition toocross-domain AJAX requests (relying on hello W3C CORS specification).</span></span> <span data-ttu-id="928b1-118">Она совместима с hello следующие браузеры:</span><span class="sxs-lookup"><span data-stu-id="928b1-118">It's compatible with hello following browsers:</span></span>

* <span data-ttu-id="928b1-119">Microsoft Edge 12 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="928b1-119">Microsoft Edge 12+</span></span>
* <span data-ttu-id="928b1-120">Internet Explorer 10 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="928b1-120">Internet Explorer 10+</span></span>
* <span data-ttu-id="928b1-121">Firefox 3.5 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="928b1-121">Firefox 3.5+</span></span>
* <span data-ttu-id="928b1-122">Chrome 4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="928b1-122">Chrome 4+</span></span>
* <span data-ttu-id="928b1-123">Safari 6 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="928b1-123">Safari 6+</span></span>
* <span data-ttu-id="928b1-124">Opera 12 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="928b1-124">Opera 12+</span></span>

## <a name="configure-mobile-engagement"></a><span data-ttu-id="928b1-125">Настройка Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="928b1-125">Configure Mobile Engagement</span></span>
<span data-ttu-id="928b1-126">Написать сценарий, который создает глобальный `azureEngagement` объекта JavaScript, такого как следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="928b1-126">Write a script that creates a global `azureEngagement` JavaScript object, as in hello following example.</span></span> <span data-ttu-id="928b1-127">Так как сайт может иметь несколько страниц, в примере предполагается, что этот сценарий включен в каждую страницу.</span><span class="sxs-lookup"><span data-stu-id="928b1-127">Because your site might have multiples pages, this example assumes that this script is included in every page.</span></span> <span data-ttu-id="928b1-128">В этом примере hello объекта JavaScript с именем `azure-engagement-conf.js`.</span><span class="sxs-lookup"><span data-stu-id="928b1-128">In this example, hello JavaScript object is named `azure-engagement-conf.js`.</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

<span data-ttu-id="928b1-129">Hello `connectionString` значение приложении отображается в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="928b1-129">hello `connectionString` value for your application is displayed in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="928b1-130">Параметры `appVersionName` и `appVersionCode` являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="928b1-130">`appVersionName` and `appVersionCode` are optional.</span></span> <span data-ttu-id="928b1-131">Однако рекомендуется их также настроить, чтобы аналитика могла обрабатывать сведения о версии.</span><span class="sxs-lookup"><span data-stu-id="928b1-131">However, we recommend that you configure them so that analytics can process version information.</span></span>
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a><span data-ttu-id="928b1-132">Добавление сценариев Служб мобильного взаимодействия в страницы</span><span class="sxs-lookup"><span data-stu-id="928b1-132">Include Mobile Engagement scripts in your pages</span></span>
<span data-ttu-id="928b1-133">Добавьте мобильного охвата сценарии tooyour страниц в одном из следующих способов hello:</span><span class="sxs-lookup"><span data-stu-id="928b1-133">Add Mobile Engagement scripts tooyour pages in one of hello following ways:</span></span>

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

<span data-ttu-id="928b1-134">или</span><span class="sxs-lookup"><span data-stu-id="928b1-134">Or this:</span></span>

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a><span data-ttu-id="928b1-135">Alias</span><span class="sxs-lookup"><span data-stu-id="928b1-135">Alias</span></span>
<span data-ttu-id="928b1-136">После загрузки hello Mobile Engagement Web SDK сценария, он создает hello **engagement** API пакета SDK для hello tooaccess псевдоним.</span><span class="sxs-lookup"><span data-stu-id="928b1-136">After hello Mobile Engagement Web SDK script is loaded, it creates hello **engagement** alias tooaccess hello SDK APIs.</span></span> <span data-ttu-id="928b1-137">Нельзя использовать эту конфигурацию пакета SDK для hello toodefine псевдоним.</span><span class="sxs-lookup"><span data-stu-id="928b1-137">You cannot use this alias toodefine hello SDK configuration.</span></span> <span data-ttu-id="928b1-138">В данной документации он используется в справочных целях.</span><span class="sxs-lookup"><span data-stu-id="928b1-138">This alias is used as a reference in this documentation.</span></span>

<span data-ttu-id="928b1-139">Обратите внимание, что при псевдоним по умолчанию hello конфликтует с другой глобальной переменной со страницы, можно переопределить его в конфигурации hello следующим перед их загрузкой hello Mobile Engagement Web SDK.</span><span class="sxs-lookup"><span data-stu-id="928b1-139">Note that if hello default alias conflicts with another global variable from your page, you can redefine it in hello configuration as follows before you load hello Mobile Engagement Web SDK:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a><span data-ttu-id="928b1-140">Упрощенные отчеты</span><span class="sxs-lookup"><span data-stu-id="928b1-140">Basic reporting</span></span>
<span data-ttu-id="928b1-141">Базовые отчеты в Службах мобильного взаимодействия охватывают статистику на уровне сеанса, такую как данные о пользователях, сеансах, действиях и сбоях.</span><span class="sxs-lookup"><span data-stu-id="928b1-141">Basic reporting in Mobile Engagement covers session-level statistics, such as statistics about users, sessions, activities, and crashes.</span></span>

### <a name="session-tracking"></a><span data-ttu-id="928b1-142">Отслеживание сеансов</span><span class="sxs-lookup"><span data-stu-id="928b1-142">Session tracking</span></span>
<span data-ttu-id="928b1-143">Сеанс Служб мобильного взаимодействия состоит из последовательности действий, каждое из которых определяется по имени.</span><span class="sxs-lookup"><span data-stu-id="928b1-143">A Mobile Engagement session is divided into a sequence of activities, each identified by a name.</span></span>

<span data-ttu-id="928b1-144">На классическом веб-сайте рекомендуется объявлять разные действия на разных страницах сайта.</span><span class="sxs-lookup"><span data-stu-id="928b1-144">In a classic website, we recommend that you declare a different activity on each page of your site.</span></span> <span data-ttu-id="928b1-145">Для веб-сайта или веб-приложения, в какие hello текущей страницы никогда не меняется может потребоваться tootrack hello действий в меньшем масштабе, такие как внутри страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="928b1-145">For a website or web application in which hello current page never changes, you might want tootrack hello activities on a smaller scale, such as within hello page.</span></span>

<span data-ttu-id="928b1-146">Либо способом, toostart или измените hello текущая активность пользователей hello вызовов `engagement.agent.startActivity` функции.</span><span class="sxs-lookup"><span data-stu-id="928b1-146">Either way, toostart or change hello current user activity, call hello `engagement.agent.startActivity` function.</span></span> <span data-ttu-id="928b1-147">Например:</span><span class="sxs-lookup"><span data-stu-id="928b1-147">For example:</span></span>

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

<span data-ttu-id="928b1-148">Hello сервера мобильного охвата автоматически завершает открытый сеанс в течение трех минут после закрытия страницы приложения hello.</span><span class="sxs-lookup"><span data-stu-id="928b1-148">hello Mobile Engagement server automatically ends an open session within three minutes after hello application page is closed.</span></span>

<span data-ttu-id="928b1-149">Также можно завершить сеанс вручную, вызвав `engagement.agent.endActivity`.</span><span class="sxs-lookup"><span data-stu-id="928b1-149">Alternatively, you can end a session manually by calling `engagement.agent.endActivity`.</span></span> <span data-ttu-id="928b1-150">Это задает hello текущего пользователя действия too'Idle. "</span><span class="sxs-lookup"><span data-stu-id="928b1-150">This sets hello current user activity too'Idle.'</span></span>  <span data-ttu-id="928b1-151">Hello сеанс будет завершен 10 секунд позже, если только новый вызов слишком`engagement.agent.startActivity` возобновляет hello сеанса.</span><span class="sxs-lookup"><span data-stu-id="928b1-151">hello session will end 10 seconds later unless a new call too`engagement.agent.startActivity` resumes hello session.</span></span>

<span data-ttu-id="928b1-152">10-секундная задержка hello hello объекта глобального обязательств, можно настроить следующим образом.</span><span class="sxs-lookup"><span data-stu-id="928b1-152">You can configure hello 10-second delay in hello global engagement object, as follows:</span></span>

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end hello session as soon as endActivity is called

> [!NOTE]
> <span data-ttu-id="928b1-153">Нельзя использовать `engagement.agent.endActivity` в hello `onunload` обратного вызова, так как нельзя выполнять вызовы AJAX на этом этапе.</span><span class="sxs-lookup"><span data-stu-id="928b1-153">You cannot use `engagement.agent.endActivity` in hello `onunload` callback because you cannot make AJAX calls at this stage.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="928b1-154">Расширенные отчеты</span><span class="sxs-lookup"><span data-stu-id="928b1-154">Advanced reporting</span></span>
<span data-ttu-id="928b1-155">При необходимости следует tooreport события конкретного приложения, ошибок и задания необходимо hello toouse Mobile Engagement API.</span><span class="sxs-lookup"><span data-stu-id="928b1-155">Optionally, if you want tooreport application-specific events, errors, and jobs, you need toouse hello Mobile Engagement API.</span></span> <span data-ttu-id="928b1-156">Доступ к hello Mobile Engagement API через hello `engagement.agent` объекта.</span><span class="sxs-lookup"><span data-stu-id="928b1-156">You access hello Mobile Engagement API through hello `engagement.agent` object.</span></span>

<span data-ttu-id="928b1-157">Вы может получить доступ ко всем hello расширенных возможностей мобильного охвата, в hello Mobile Engagement API.</span><span class="sxs-lookup"><span data-stu-id="928b1-157">You can access all of hello advanced capabilities in Mobile Engagement in hello Mobile Engagement API.</span></span> <span data-ttu-id="928b1-158">Hello API, описанные в статье hello [как toouse hello дополнительные теги API в веб-приложение Mobile Engagement](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="928b1-158">hello API is detailed in hello article [How toouse hello advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="customize-hello-urls-used-for-ajax-calls"></a><span data-ttu-id="928b1-159">Настраивать hello URL-адреса, используемый для вызовов AJAX</span><span class="sxs-lookup"><span data-stu-id="928b1-159">Customize hello URLs used for AJAX calls</span></span>
<span data-ttu-id="928b1-160">Вы можете настроить URL-адреса, которые использует пакет SDK Mobile Engagement Web hello.</span><span class="sxs-lookup"><span data-stu-id="928b1-160">You can customize URLs that hello Mobile Engagement Web SDK uses.</span></span> <span data-ttu-id="928b1-161">Например tooredefine hello URL-адрес (hello SDK конечную точку для ведения журнала), можно переопределить конфигурацию hello следующим образом.</span><span class="sxs-lookup"><span data-stu-id="928b1-161">For example, tooredefine hello log URL (hello SDK endpoint for logging), you can override hello configuration like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

<span data-ttu-id="928b1-162">Если ваш URL-адрес функции возвращают строку, начинающуюся с `/`, `//`, `http://`, или `https://`, не используется схема по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="928b1-162">If your URL functions return a string that begins with `/`, `//`, `http://`, or `https://`, hello default scheme is not used.</span></span> <span data-ttu-id="928b1-163">По умолчанию hello `https://` используется схема для этих URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="928b1-163">By default, hello `https://` scheme is used for those URLs.</span></span> <span data-ttu-id="928b1-164">Если схема по умолчанию hello toocustomize, переопределите hello конфигурации, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="928b1-164">If you want toocustomize hello default scheme, override hello configuration, like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
