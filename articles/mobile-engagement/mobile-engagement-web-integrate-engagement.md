---
title: "Интеграция веб-пакета SDK для Служб мобильного взаимодействия Azure | Документация Майкрософт"
description: "Последние обновления и процедуры для веб-пакета SDK для Служб мобильного взаимодействия Azure"
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
ms.openlocfilehash: 7d8eaa180e277741a583522ee62d68f5247b92bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a><span data-ttu-id="85a72-103">Интегрирование Служб мобильного взаимодействия Azure в веб-приложение</span><span class="sxs-lookup"><span data-stu-id="85a72-103">Integrate Azure Mobile Engagement in a web application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="85a72-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="85a72-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="85a72-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="85a72-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="85a72-106">iOS</span><span class="sxs-lookup"><span data-stu-id="85a72-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="85a72-107">Android</span><span class="sxs-lookup"><span data-stu-id="85a72-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="85a72-108">В этой статье описана самая простая процедура активации функций аналитики и мониторинга Служб мобильного взаимодействия Azure в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="85a72-108">The procedures in this article describe the simplest way to activate the analytics and monitoring functions in Azure Mobile Engagement in your web application.</span></span>

<span data-ttu-id="85a72-109">Выполните следующие шаги, чтобы активировать отчеты по журналам, которые необходимы для вычисления всех статистических данных, касающихся пользователей, сеансов, действий, сбоев и технической информации.</span><span class="sxs-lookup"><span data-stu-id="85a72-109">Follow the steps to activate the log reports that are needed to compute all statistics about users, sessions, activities, crashes, and technicals.</span></span> <span data-ttu-id="85a72-110">Для статистики, зависящей от приложения, такой как события, ошибки или задания, необходимо вручную активировать отчеты по журналам, используя API Служб мобильного взаимодействия Azure.</span><span class="sxs-lookup"><span data-stu-id="85a72-110">For application-dependent statistics, such as events, errors, and jobs, you must activate log reports manually by using the Azure Mobile Engagement API.</span></span> <span data-ttu-id="85a72-111">Дополнительно узнайте, [как использовать API для расширенного добавления тегов Служб мобильного взаимодействия в веб-приложении](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="85a72-111">For more information, learn [how to use the advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="85a72-112">Введение</span><span class="sxs-lookup"><span data-stu-id="85a72-112">Introduction</span></span>
<span data-ttu-id="85a72-113">[Скачайте веб-пакет SDK для Служб мобильного взаимодействия Azure](http://aka.ms/P7b453).</span><span class="sxs-lookup"><span data-stu-id="85a72-113">[Download the Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span></span>
<span data-ttu-id="85a72-114">Веб-пакет SDK для Служб мобильного взаимодействия поставляется как отдельный файл JavaScript с именем azure-engagement.js, который необходимо включить в каждую страницу сайта или веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="85a72-114">The Mobile Engagement Web SDK is shipped as a single JavaScript file, azure-engagement.js, which you have to include in each page of your site or web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="85a72-115">Этот сценарий необходимо выполнить после выполнения фрагмента сценария или кода, который вы создаете, чтобы настроить Службы мобильного взаимодействия для приложения.</span><span class="sxs-lookup"><span data-stu-id="85a72-115">Before you run this script, you must run a script or code snippet that you write to configure Mobile Engagement for your application.</span></span>
> 
> 

## <a name="browser-compatibility"></a><span data-ttu-id="85a72-116">Совместимость с браузерами</span><span class="sxs-lookup"><span data-stu-id="85a72-116">Browser compatibility</span></span>
<span data-ttu-id="85a72-117">Веб-пакет SDK для Служб мобильного взаимодействия использует собственное кодирование и декодирование JSON, помимо междоменных запросов AJAX (на основе спецификации W3C CORS).</span><span class="sxs-lookup"><span data-stu-id="85a72-117">The Mobile Engagement Web SDK uses native JSON encoding and decoding, in addition to cross-domain AJAX requests (relying on the W3C CORS specification).</span></span> <span data-ttu-id="85a72-118">Он совместим со следующими браузерами:</span><span class="sxs-lookup"><span data-stu-id="85a72-118">It's compatible with the following browsers:</span></span>

* <span data-ttu-id="85a72-119">Microsoft Edge 12 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="85a72-119">Microsoft Edge 12+</span></span>
* <span data-ttu-id="85a72-120">Internet Explorer 10 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="85a72-120">Internet Explorer 10+</span></span>
* <span data-ttu-id="85a72-121">Firefox 3.5 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="85a72-121">Firefox 3.5+</span></span>
* <span data-ttu-id="85a72-122">Chrome 4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="85a72-122">Chrome 4+</span></span>
* <span data-ttu-id="85a72-123">Safari 6 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="85a72-123">Safari 6+</span></span>
* <span data-ttu-id="85a72-124">Opera 12 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="85a72-124">Opera 12+</span></span>

## <a name="configure-mobile-engagement"></a><span data-ttu-id="85a72-125">Настройка Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="85a72-125">Configure Mobile Engagement</span></span>
<span data-ttu-id="85a72-126">Создайте сценарий, который создает глобальный объект JavaScript `azureEngagement` , как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="85a72-126">Write a script that creates a global `azureEngagement` JavaScript object, as in the following example.</span></span> <span data-ttu-id="85a72-127">Так как сайт может иметь несколько страниц, в примере предполагается, что этот сценарий включен в каждую страницу.</span><span class="sxs-lookup"><span data-stu-id="85a72-127">Because your site might have multiples pages, this example assumes that this script is included in every page.</span></span> <span data-ttu-id="85a72-128">В этом примере объект JavaScript имеет имя `azure-engagement-conf.js`.</span><span class="sxs-lookup"><span data-stu-id="85a72-128">In this example, the JavaScript object is named `azure-engagement-conf.js`.</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

<span data-ttu-id="85a72-129">Значение `connectionString` для приложения отображается на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="85a72-129">The `connectionString` value for your application is displayed in the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="85a72-130">Параметры `appVersionName` и `appVersionCode` являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="85a72-130">`appVersionName` and `appVersionCode` are optional.</span></span> <span data-ttu-id="85a72-131">Однако рекомендуется их также настроить, чтобы аналитика могла обрабатывать сведения о версии.</span><span class="sxs-lookup"><span data-stu-id="85a72-131">However, we recommend that you configure them so that analytics can process version information.</span></span>
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a><span data-ttu-id="85a72-132">Добавление сценариев Служб мобильного взаимодействия в страницы</span><span class="sxs-lookup"><span data-stu-id="85a72-132">Include Mobile Engagement scripts in your pages</span></span>
<span data-ttu-id="85a72-133">Добавьте сценарии Служб мобильного взаимодействия в свои страницы одним из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="85a72-133">Add Mobile Engagement scripts to your pages in one of the following ways:</span></span>

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

<span data-ttu-id="85a72-134">или</span><span class="sxs-lookup"><span data-stu-id="85a72-134">Or this:</span></span>

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a><span data-ttu-id="85a72-135">Alias</span><span class="sxs-lookup"><span data-stu-id="85a72-135">Alias</span></span>
<span data-ttu-id="85a72-136">После загрузки сценарий веб-пакета SDK для Служб мобильного взаимодействия создает псевдоним **engagement** для доступа к интерфейсам API пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="85a72-136">After the Mobile Engagement Web SDK script is loaded, it creates the **engagement** alias to access the SDK APIs.</span></span> <span data-ttu-id="85a72-137">Этот псевдоним нельзя использовать для определения конфигурации пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="85a72-137">You cannot use this alias to define the SDK configuration.</span></span> <span data-ttu-id="85a72-138">В данной документации он используется в справочных целях.</span><span class="sxs-lookup"><span data-stu-id="85a72-138">This alias is used as a reference in this documentation.</span></span>

<span data-ttu-id="85a72-139">Обратите внимание, что если псевдоним по умолчанию конфликтует с другой глобальной переменной страницы, то вы можете переопределить его в конфигурации перед загрузкой веб-пакета SDK для Служб мобильного взаимодействия. Это делается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="85a72-139">Note that if the default alias conflicts with another global variable from your page, you can redefine it in the configuration as follows before you load the Mobile Engagement Web SDK:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a><span data-ttu-id="85a72-140">Упрощенные отчеты</span><span class="sxs-lookup"><span data-stu-id="85a72-140">Basic reporting</span></span>
<span data-ttu-id="85a72-141">Базовые отчеты в Службах мобильного взаимодействия охватывают статистику на уровне сеанса, такую как данные о пользователях, сеансах, действиях и сбоях.</span><span class="sxs-lookup"><span data-stu-id="85a72-141">Basic reporting in Mobile Engagement covers session-level statistics, such as statistics about users, sessions, activities, and crashes.</span></span>

### <a name="session-tracking"></a><span data-ttu-id="85a72-142">Отслеживание сеансов</span><span class="sxs-lookup"><span data-stu-id="85a72-142">Session tracking</span></span>
<span data-ttu-id="85a72-143">Сеанс Служб мобильного взаимодействия состоит из последовательности действий, каждое из которых определяется по имени.</span><span class="sxs-lookup"><span data-stu-id="85a72-143">A Mobile Engagement session is divided into a sequence of activities, each identified by a name.</span></span>

<span data-ttu-id="85a72-144">На классическом веб-сайте рекомендуется объявлять разные действия на разных страницах сайта.</span><span class="sxs-lookup"><span data-stu-id="85a72-144">In a classic website, we recommend that you declare a different activity on each page of your site.</span></span> <span data-ttu-id="85a72-145">На веб-сайте или в веб-приложении, которое никогда не изменяет текущую страницу, может потребоваться отслеживать действия более точным способом, например в пределах страницы.</span><span class="sxs-lookup"><span data-stu-id="85a72-145">For a website or web application in which the current page never changes, you might want to track the activities on a smaller scale, such as within the page.</span></span>

<span data-ttu-id="85a72-146">В любом случае, чтобы запустить или изменить текущее действие пользователя, вызовите функцию `engagement.agent.startActivity` .</span><span class="sxs-lookup"><span data-stu-id="85a72-146">Either way, to start or change the current user activity, call the `engagement.agent.startActivity` function.</span></span> <span data-ttu-id="85a72-147">Например:</span><span class="sxs-lookup"><span data-stu-id="85a72-147">For example:</span></span>

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

<span data-ttu-id="85a72-148">Сервер Служб мобильного взаимодействия автоматически завершает открытый сеанс через три минуты после закрытия страницы приложения.</span><span class="sxs-lookup"><span data-stu-id="85a72-148">The Mobile Engagement server automatically ends an open session within three minutes after the application page is closed.</span></span>

<span data-ttu-id="85a72-149">Также можно завершить сеанс вручную, вызвав `engagement.agent.endActivity`.</span><span class="sxs-lookup"><span data-stu-id="85a72-149">Alternatively, you can end a session manually by calling `engagement.agent.endActivity`.</span></span> <span data-ttu-id="85a72-150">При этом текущее действие пользователя переводится в состояние "Неактивно".</span><span class="sxs-lookup"><span data-stu-id="85a72-150">This sets the current user activity to 'Idle.'</span></span>  <span data-ttu-id="85a72-151">Сеанс будет завершен через 10 секунд, если только в этот период его не возобновит новый вызов `engagement.agent.startActivity` .</span><span class="sxs-lookup"><span data-stu-id="85a72-151">The session will end 10 seconds later unless a new call to `engagement.agent.startActivity` resumes the session.</span></span>

<span data-ttu-id="85a72-152">Эту задержку в 10 секунд можно настроить в глобальном объекте engagement:</span><span class="sxs-lookup"><span data-stu-id="85a72-152">You can configure the 10-second delay in the global engagement object, as follows:</span></span>

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end the session as soon as endActivity is called

> [!NOTE]
> <span data-ttu-id="85a72-153">`engagement.agent.endActivity` нельзя использовать в обратном вызове `onunload`, так как на этом этапе вызовы AJAX невозможны.</span><span class="sxs-lookup"><span data-stu-id="85a72-153">You cannot use `engagement.agent.endActivity` in the `onunload` callback because you cannot make AJAX calls at this stage.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="85a72-154">Расширенные отчеты</span><span class="sxs-lookup"><span data-stu-id="85a72-154">Advanced reporting</span></span>
<span data-ttu-id="85a72-155">Если вы хотите получать отчеты о событиях, ошибках и заданиях, относящихся к конкретному приложению, следует использовать API Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="85a72-155">Optionally, if you want to report application-specific events, errors, and jobs, you need to use the Mobile Engagement API.</span></span> <span data-ttu-id="85a72-156">Доступ к API Служб мобильного взаимодействия можно получить посредством объекта `engagement.agent`.</span><span class="sxs-lookup"><span data-stu-id="85a72-156">You access the Mobile Engagement API through the `engagement.agent` object.</span></span>

<span data-ttu-id="85a72-157">API Служб мобильного взаимодействия позволяет использовать все расширенные возможности этой службы.</span><span class="sxs-lookup"><span data-stu-id="85a72-157">You can access all of the advanced capabilities in Mobile Engagement in the Mobile Engagement API.</span></span> <span data-ttu-id="85a72-158">Дополнительные сведения об API см. в статье [Использование API Служб мобильного взаимодействия Azure в веб-приложении](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="85a72-158">The API is detailed in the article [How to use the advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="customize-the-urls-used-for-ajax-calls"></a><span data-ttu-id="85a72-159">Настройка URL-адресов, используемых для вызовов AJAX</span><span class="sxs-lookup"><span data-stu-id="85a72-159">Customize the URLs used for AJAX calls</span></span>
<span data-ttu-id="85a72-160">Вы можете настроить URL-адреса, используемые веб-пакетом SDK для Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="85a72-160">You can customize URLs that the Mobile Engagement Web SDK uses.</span></span> <span data-ttu-id="85a72-161">Например, чтобы переопределить URL-адрес журнала (конечную точку пакета SDK для ведения журнала), можно переопределить конфигурацию следующим образом:</span><span class="sxs-lookup"><span data-stu-id="85a72-161">For example, to redefine the log URL (the SDK endpoint for logging), you can override the configuration like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

<span data-ttu-id="85a72-162">Если ваши функции URL-адреса возвращают строку, начинающуюся с `/`, `//`, `http://` или `https://`, то схема по умолчанию не используется.</span><span class="sxs-lookup"><span data-stu-id="85a72-162">If your URL functions return a string that begins with `/`, `//`, `http://`, or `https://`, the default scheme is not used.</span></span> <span data-ttu-id="85a72-163">По умолчанию для этих URL-адресов используется схема `https://` .</span><span class="sxs-lookup"><span data-stu-id="85a72-163">By default, the `https://` scheme is used for those URLs.</span></span> <span data-ttu-id="85a72-164">Если вы хотите настроить схему по умолчанию, то переопределите конфигурацию следующим образом:</span><span class="sxs-lookup"><span data-stu-id="85a72-164">If you want to customize the default scheme, override the configuration, like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
