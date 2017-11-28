---
title: "aaaAzure Mobile Engagement Troubleshooting Guide - API-интерфейсы"
description: "Руководства по устранению неполадок для Служб мобильного взаимодействия Azure —API"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3efc8a52-2b74-4917-b887-815ae8277474
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/04/2016
ms.author: piyushjo
ms.openlocfilehash: 5656b6f0f1aaf3e496a168c7cf09b307b9ab2a4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-api-issues"></a><span data-ttu-id="fd8a8-103">Поиск и устранение неполадок API</span><span class="sxs-lookup"><span data-stu-id="fd8a8-103">Troubleshooting guide for API issues</span></span>
<span data-ttu-id="fd8a8-104">Hello ниже приведены возможные проблемы, которые могут возникнуть с как администраторы взаимодействовать с Azure Mobile Engagement через API-интерфейсы hello.</span><span class="sxs-lookup"><span data-stu-id="fd8a8-104">hello following are possible issues you may encounter with how administrators interact with Azure Mobile Engagement via hello APIs.</span></span>

## <a name="syntax-issues"></a><span data-ttu-id="fd8a8-105">Проблемы, связанные с синтаксисом</span><span class="sxs-lookup"><span data-stu-id="fd8a8-105">Syntax issues</span></span>
### <a name="issue"></a><span data-ttu-id="fd8a8-106">Проблема</span><span class="sxs-lookup"><span data-stu-id="fd8a8-106">Issue</span></span>
* <span data-ttu-id="fd8a8-107">Синтаксические ошибки с помощью hello API (или непредвиденное поведение).</span><span class="sxs-lookup"><span data-stu-id="fd8a8-107">Syntax Errors using hello API (or unexpected behavior).</span></span>

### <a name="causes"></a><span data-ttu-id="fd8a8-108">Причины</span><span class="sxs-lookup"><span data-stu-id="fd8a8-108">Causes</span></span>
* <span data-ttu-id="fd8a8-109">Проблемы, связанные с синтаксисом</span><span class="sxs-lookup"><span data-stu-id="fd8a8-109">Syntax issues:</span></span>
  * <span data-ttu-id="fd8a8-110">Сделать убедиться, что toocheck hello синтаксис конкретного API hello использовании tooconfirm, hello параметр доступен.</span><span class="sxs-lookup"><span data-stu-id="fd8a8-110">Make sure toocheck hello Syntax of hello specific API you are using tooconfirm that hello option is available.</span></span>
  * <span data-ttu-id="fd8a8-111">Распространенные проблемы с использованием API — tooconfuse hello Reach API и hello Push-API (большинство задач должно выполняться с помощью hello Reach API вместо hello Push-API).</span><span class="sxs-lookup"><span data-stu-id="fd8a8-111">A common issue with API usage is tooconfuse hello Reach API and hello Push API (most tasks should be performed with hello Reach API instead of hello Push API).</span></span> 
  * <span data-ttu-id="fd8a8-112">Другой распространенные проблемы с интеграцией пакета SDK и использование API — tooconfuse hello ключ SDK и hello ключ API.</span><span class="sxs-lookup"><span data-stu-id="fd8a8-112">Another common issue with SDK integration and API usage is tooconfuse hello SDK Key and hello API Key.</span></span>
  * <span data-ttu-id="fd8a8-113">Сценарии, которые подключения toohello API-интерфейсы должны toosend данных каждые 10 минут или подключения hello выдаст ошибку времени ожидания (особенно часто применяется в скриптах API-Интерфейс монитора прослушивает данные).</span><span class="sxs-lookup"><span data-stu-id="fd8a8-113">Scripts that connect toohello APIs need toosend data at least every 10 minutes or hello connection will time out (especially common in Monitor API scripts listening for data).</span></span> <span data-ttu-id="fd8a8-114">tooprevent истечение времени ожидания, у вашей отправки сценария XMPP ping каждый hello 10 минут tookeep, сеанс проверки активности с сервером hello.</span><span class="sxs-lookup"><span data-stu-id="fd8a8-114">tooprevent timeouts, have your script send an XMPP ping every 10 minutes tookeep hello session alive with hello server.</span></span>

### <a name="see-also"></a><span data-ttu-id="fd8a8-115">См. также</span><span class="sxs-lookup"><span data-stu-id="fd8a8-115">See also</span></span>
* <span data-ttu-id="fd8a8-116">[Документация по API-интерфейсам][Link 4]</span><span class="sxs-lookup"><span data-stu-id="fd8a8-116">[API Documentation][Link 4]</span></span>
* [<span data-ttu-id="fd8a8-117">Сведения о протоколе XMPP</span><span class="sxs-lookup"><span data-stu-id="fd8a8-117">XMPP Protocol Info</span></span>](http://xmpp.org/extensions/xep-0199.html)

## <a name="unable-toouse-hello-api-tooperform-hello-same-action-available-in-hello-azure-mobile-engagement-ui"></a><span data-ttu-id="fd8a8-118">Не удается toouse hello API tooperform hello же действии, доступном в hello пользовательского интерфейса Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="fd8a8-118">Unable toouse hello API tooperform hello same action available in hello Azure Mobile Engagement UI</span></span>
### <a name="issue"></a><span data-ttu-id="fd8a8-119">Проблема</span><span class="sxs-lookup"><span data-stu-id="fd8a8-119">Issue</span></span>
* <span data-ttu-id="fd8a8-120">Действие, которое работает из пользовательского интерфейса Azure Mobile Engagement не работает с hello приветствия, связанные с Azure Mobile Engagement API.</span><span class="sxs-lookup"><span data-stu-id="fd8a8-120">An action that works from hello Azure Mobile Engagement UI doesn't work from hello related Azure Mobile Engagement API.</span></span>

### <a name="causes"></a><span data-ttu-id="fd8a8-121">Причины</span><span class="sxs-lookup"><span data-stu-id="fd8a8-121">Causes</span></span>
* <span data-ttu-id="fd8a8-122">Здравствуйте, подтверждающее, что вы сможете выполнять hello показано действие из пользовательского интерфейса Azure Mobile Engagement hello правильно интегрированы этот компонент Azure Mobile Engagement с SDK.</span><span class="sxs-lookup"><span data-stu-id="fd8a8-122">Confirming that you can perform hello same action from hello Azure Mobile Engagement UI shows that you have correctly integrated this feature of Azure Mobile Engagement with hello SDK.</span></span>

### <a name="see-also"></a><span data-ttu-id="fd8a8-123">См. также</span><span class="sxs-lookup"><span data-stu-id="fd8a8-123">See also</span></span>
* <span data-ttu-id="fd8a8-124">[Управление существующими приложениями и проектами][Link 1]</span><span class="sxs-lookup"><span data-stu-id="fd8a8-124">[UI Documentation][Link 1]</span></span>

## <a name="error-messages"></a><span data-ttu-id="fd8a8-125">сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="fd8a8-125">Error Messages</span></span>
### <a name="issue"></a><span data-ttu-id="fd8a8-126">Проблема</span><span class="sxs-lookup"><span data-stu-id="fd8a8-126">Issue</span></span>
* <span data-ttu-id="fd8a8-127">Коды ошибок, с помощью API hello, отображаемых во время выполнения или в журналах.</span><span class="sxs-lookup"><span data-stu-id="fd8a8-127">Error codes using hello API displayed at runtime or in logs.</span></span>

### <a name="causes"></a><span data-ttu-id="fd8a8-128">Причины</span><span class="sxs-lookup"><span data-stu-id="fd8a8-128">Causes</span></span>
* <span data-ttu-id="fd8a8-129">Ниже приведен общий список распространенных кодов состояния API для справки и предварительного устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="fd8a8-129">Here is a composite list of common API status codes numbers for reference and preliminary troubleshooting:</span></span>
  
        200        Success.
        200        Account updated: device registered, associated, updated, or removed from hello current account.
        200        Returns a list of projects as a JSON object or an authentication token generated and returned in hello response’s body.
        201        Account created.
        400        Invalid parameter or validation exception (check payload for details). hello parameters provided toohello API or service are invalid. In this case, hello HTTP response will embed more details. Make sure tootest for hello MIME type of hello response as hello payload can either be plain text or a JSON object.
        401        Authentication error. No user is currently authenticated or connected (check hello AppID and SDK key).
        402        Billing lock. hello application is either off its quotas or is currently in a bad billing state.
        403        hello application is not enabled or hello specific API is disabled for this application.
        403        Unauthorized access toohello project or application, invalid access key (hello key must match hello one provided when created).
        403        Campaign specific errors: campaign must be finished (or has already been activated), hello suspend action can only be performed on an scheduled campaign, cannot finish a campaign that is not currently “in progress”, campaign must be “in progress” and hello campaign’s property named, manual Push must be set tootrue.
        403        hello email address is already associated tooanother account (a super user for instance). No authentication token will be generated.
        404        Application, device, campaign, or project identifier not found.
        404        Query parameter is invalid JSON or has a field with an unexpected value.
        404        hello email address is not associated with an account. Please create or update hello account first.
        405        Invalid HTTP method (GET, POST, etc.) or trying tooedit a read only segment (i.e. add or update or delete a criterion). A segment becomes read only after it has been computed for hello first time.
        409        Name already associated tooa different device ID or campaign.
        413        Too many device identifiers (current limit is 1,000), POST URL encoded entity is over 2MB, or hello period is too large toobe displayed (hello server didn’t retrieve hello analytics because hello user request is for a period that is too large).
        503        Analytics not available yet (hello requested information is not computed yet for an application).
        504        hello server was not able toohandle your request in a reasonable time (if you make multiple calls tooan API very quickly, try toomake one call at a time and spread hello calls out over time).

### <a name="see-also"></a><span data-ttu-id="fd8a8-130">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="fd8a8-130">See also</span></span>
* <span data-ttu-id="fd8a8-131">[Mobile Engagement][Link 4]</span><span class="sxs-lookup"><span data-stu-id="fd8a8-131">[API Documentation - for detailed errors on each specific API][Link 4]</span></span>

## <a name="silent-failures"></a><span data-ttu-id="fd8a8-132">Автоматические сбои</span><span class="sxs-lookup"><span data-stu-id="fd8a8-132">Silent failures</span></span>
### <a name="issue"></a><span data-ttu-id="fd8a8-133">Проблема</span><span class="sxs-lookup"><span data-stu-id="fd8a8-133">Issue</span></span>
* <span data-ttu-id="fd8a8-134">Действие с использованием API заканчивается сбоем, при этом во время выполнения или по завершении в журналах не отображается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="fd8a8-134">API action fails with no error message displayed at runtime or in logs.</span></span>

### <a name="causes"></a><span data-ttu-id="fd8a8-135">Причины</span><span class="sxs-lookup"><span data-stu-id="fd8a8-135">Causes</span></span>
* <span data-ttu-id="fd8a8-136">Многие элементы будут отключены hello пользовательского интерфейса Azure Mobile Engagement, если они не являются правильной интеграции, но будет выполнена из hello API, поэтому необходимо учитывать tootest hello же функциональные возможности пользовательского интерфейса toosee hello, если он работает.</span><span class="sxs-lookup"><span data-stu-id="fd8a8-136">Many items will be disabled in hello Azure Mobile Engagement UI if they aren't integrated correctly, but will fail silently from hello API, so remember tootest hello same functionality from hello UI toosee if it works.</span></span>
* <span data-ttu-id="fd8a8-137">Azure Mobile Engagement и несколько дополнительных функций из Azure Mobile Engagement, который вы пытаетесь toouse toobe необходимости по отдельности интегрируется в приложение с помощью пакета SDK для hello как отдельные шаги перед их использованием.</span><span class="sxs-lookup"><span data-stu-id="fd8a8-137">Azure Mobile Engagement, and many advanced features of Azure Mobile Engagement you are attempting toouse, need toobe individually integrated into your app with hello SDK as separate steps before you can use them.</span></span>

### <a name="see-also"></a><span data-ttu-id="fd8a8-138">См. также</span><span class="sxs-lookup"><span data-stu-id="fd8a8-138">See also</span></span>
* <span data-ttu-id="fd8a8-139">[Руководство по поиску и устранению проблем с интеграцией при использовании SDK][Link 25]</span><span class="sxs-lookup"><span data-stu-id="fd8a8-139">[Troubleshooting Guide - SDK][Link 25]</span></span>

<!--Link references-->
[Link 1]: mobile-engagement-user-interface-home.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

