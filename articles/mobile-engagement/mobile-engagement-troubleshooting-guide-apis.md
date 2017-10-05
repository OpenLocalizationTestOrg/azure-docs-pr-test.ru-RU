---
title: "Руководство по устранению неполадок Служб мобильного взаимодействия Azure — API"
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
ms.openlocfilehash: a7ae0a83046f2d67b790f672dcd3ae261987357a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-api-issues"></a><span data-ttu-id="d1913-103">Поиск и устранение неполадок API</span><span class="sxs-lookup"><span data-stu-id="d1913-103">Troubleshooting guide for API issues</span></span>
<span data-ttu-id="d1913-104">Ниже представлены проблемы, которые могут возникнуть в ходе взаимодействия администраторов со Службами мобильного взаимодействия Azure через интерфейсы API.</span><span class="sxs-lookup"><span data-stu-id="d1913-104">The following are possible issues you may encounter with how administrators interact with Azure Mobile Engagement via the APIs.</span></span>

## <a name="syntax-issues"></a><span data-ttu-id="d1913-105">Проблемы, связанные с синтаксисом</span><span class="sxs-lookup"><span data-stu-id="d1913-105">Syntax issues</span></span>
### <a name="issue"></a><span data-ttu-id="d1913-106">Проблема</span><span class="sxs-lookup"><span data-stu-id="d1913-106">Issue</span></span>
* <span data-ttu-id="d1913-107">Синтаксические ошибки при использовании API (или неожиданное поведение).</span><span class="sxs-lookup"><span data-stu-id="d1913-107">Syntax Errors using the API (or unexpected behavior).</span></span>

### <a name="causes"></a><span data-ttu-id="d1913-108">Причины</span><span class="sxs-lookup"><span data-stu-id="d1913-108">Causes</span></span>
* <span data-ttu-id="d1913-109">Проблемы, связанные с синтаксисом</span><span class="sxs-lookup"><span data-stu-id="d1913-109">Syntax issues:</span></span>
  * <span data-ttu-id="d1913-110">Проверьте синтаксис определенного API, который вы используете, чтобы подтвердить, что определенная возможность доступна.</span><span class="sxs-lookup"><span data-stu-id="d1913-110">Make sure to check the Syntax of the specific API you are using to confirm that the option is available.</span></span>
  * <span data-ttu-id="d1913-111">Распространенная проблема с использованием API — неправильное использование Reach API и API push-уведомлений (большинство задач необходимо выполнять с помощью Reach API, а не API push-уведомлений).</span><span class="sxs-lookup"><span data-stu-id="d1913-111">A common issue with API usage is to confuse the Reach API and the Push API (most tasks should be performed with the Reach API instead of the Push API).</span></span> 
  * <span data-ttu-id="d1913-112">Еще одна распространенная проблема с интеграцией пакета SDK и использованием API — неправильное использование ключа пакета SDK и ключа API.</span><span class="sxs-lookup"><span data-stu-id="d1913-112">Another common issue with SDK integration and API usage is to confuse the SDK Key and the API Key.</span></span>
  * <span data-ttu-id="d1913-113">Скрипты, подключающиеся к интерфейсам API, должны отправлять данные по крайней мере каждые 10 минут, в противном случае время ожидания подключения истечет (эта проблема особенно распространена в скриптах Monitor API, прослушивающих данные).</span><span class="sxs-lookup"><span data-stu-id="d1913-113">Scripts that connect to the APIs need to send data at least every 10 minutes or the connection will time out (especially common in Monitor API scripts listening for data).</span></span> <span data-ttu-id="d1913-114">Чтобы предотвратить возникновение задержки, ваш скрипт должен отправлять команду ping XMPP каждые 10 минут, чтобы сеанс работы с сервером не завершался.</span><span class="sxs-lookup"><span data-stu-id="d1913-114">To prevent timeouts, have your script send an XMPP ping every 10 minutes to keep the session alive with the server.</span></span>

### <a name="see-also"></a><span data-ttu-id="d1913-115">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="d1913-115">See also</span></span>
* <span data-ttu-id="d1913-116">[Документация по API-интерфейсам][Link 4]</span><span class="sxs-lookup"><span data-stu-id="d1913-116">[API Documentation][Link 4]</span></span>
* [<span data-ttu-id="d1913-117">Сведения о протоколе XMPP</span><span class="sxs-lookup"><span data-stu-id="d1913-117">XMPP Protocol Info</span></span>](http://xmpp.org/extensions/xep-0199.html)

## <a name="unable-to-use-the-api-to-perform-the-same-action-available-in-the-azure-mobile-engagement-ui"></a><span data-ttu-id="d1913-118">Не удается использовать API для выполнения действия, доступного в пользовательском интерфейсе Служб мобильного взаимодействия Azure.</span><span class="sxs-lookup"><span data-stu-id="d1913-118">Unable to use the API to perform the same action available in the Azure Mobile Engagement UI</span></span>
### <a name="issue"></a><span data-ttu-id="d1913-119">Проблема</span><span class="sxs-lookup"><span data-stu-id="d1913-119">Issue</span></span>
* <span data-ttu-id="d1913-120">Действие, которое выполняется в пользовательском интерфейсе Служб мобильного взаимодействия Azure, не выполняется в соответствующем API Служб мобильного взаимодействия Azure.</span><span class="sxs-lookup"><span data-stu-id="d1913-120">An action that works from the Azure Mobile Engagement UI doesn't work from the related Azure Mobile Engagement API.</span></span>

### <a name="causes"></a><span data-ttu-id="d1913-121">Причины</span><span class="sxs-lookup"><span data-stu-id="d1913-121">Causes</span></span>
* <span data-ttu-id="d1913-122">Подтверждение того, что вы можете выполнять это действие в пользовательском интерфейсе Служб мобильного взаимодействия Azure, свидетельствует о правильной интеграции этой функции Служб мобильного взаимодействия Azure в пакет SDK.</span><span class="sxs-lookup"><span data-stu-id="d1913-122">Confirming that you can perform the same action from the Azure Mobile Engagement UI shows that you have correctly integrated this feature of Azure Mobile Engagement with the SDK.</span></span>

### <a name="see-also"></a><span data-ttu-id="d1913-123">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="d1913-123">See also</span></span>
* <span data-ttu-id="d1913-124">[Управление существующими приложениями и проектами][Link 1]</span><span class="sxs-lookup"><span data-stu-id="d1913-124">[UI Documentation][Link 1]</span></span>

## <a name="error-messages"></a><span data-ttu-id="d1913-125">сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="d1913-125">Error Messages</span></span>
### <a name="issue"></a><span data-ttu-id="d1913-126">Проблема</span><span class="sxs-lookup"><span data-stu-id="d1913-126">Issue</span></span>
* <span data-ttu-id="d1913-127">Во время выполнения или по завершении в журналах отображаются коды ошибок, связанные с использованием API.</span><span class="sxs-lookup"><span data-stu-id="d1913-127">Error codes using the API displayed at runtime or in logs.</span></span>

### <a name="causes"></a><span data-ttu-id="d1913-128">Причины</span><span class="sxs-lookup"><span data-stu-id="d1913-128">Causes</span></span>
* <span data-ttu-id="d1913-129">Ниже приведен общий список распространенных кодов состояния API для справки и предварительного устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="d1913-129">Here is a composite list of common API status codes numbers for reference and preliminary troubleshooting:</span></span>
  
        200        Success.
        200        Account updated: device registered, associated, updated, or removed from the current account.
        200        Returns a list of projects as a JSON object or an authentication token generated and returned in the response’s body.
        201        Account created.
        400        Invalid parameter or validation exception (check payload for details). The parameters provided to the API or service are invalid. In this case, the HTTP response will embed more details. Make sure to test for the MIME type of the response as the payload can either be plain text or a JSON object.
        401        Authentication error. No user is currently authenticated or connected (check the AppID and SDK key).
        402        Billing lock. The application is either off its quotas or is currently in a bad billing state.
        403        The application is not enabled or the specific API is disabled for this application.
        403        Unauthorized access to the project or application, invalid access key (the key must match the one provided when created).
        403        Campaign specific errors: campaign must be finished (or has already been activated), the suspend action can only be performed on an scheduled campaign, cannot finish a campaign that is not currently “in progress”, campaign must be “in progress” and the campaign’s property named, manual Push must be set to true.
        403        The email address is already associated to another account (a super user for instance). No authentication token will be generated.
        404        Application, device, campaign, or project identifier not found.
        404        Query parameter is invalid JSON or has a field with an unexpected value.
        404        The email address is not associated with an account. Please create or update the account first.
        405        Invalid HTTP method (GET, POST, etc.) or trying to edit a read only segment (i.e. add or update or delete a criterion). A segment becomes read only after it has been computed for the first time.
        409        Name already associated to a different device ID or campaign.
        413        Too many device identifiers (current limit is 1,000), POST URL encoded entity is over 2MB, or the period is too large to be displayed (the server didn’t retrieve the analytics because the user request is for a period that is too large).
        503        Analytics not available yet (the requested information is not computed yet for an application).
        504        The server was not able to handle your request in a reasonable time (if you make multiple calls to an API very quickly, try to make one call at a time and spread the calls out over time).

### <a name="see-also"></a><span data-ttu-id="d1913-130">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="d1913-130">See also</span></span>
* <span data-ttu-id="d1913-131">[Mobile Engagement][Link 4]</span><span class="sxs-lookup"><span data-stu-id="d1913-131">[API Documentation - for detailed errors on each specific API][Link 4]</span></span>

## <a name="silent-failures"></a><span data-ttu-id="d1913-132">Автоматические сбои</span><span class="sxs-lookup"><span data-stu-id="d1913-132">Silent failures</span></span>
### <a name="issue"></a><span data-ttu-id="d1913-133">Проблема</span><span class="sxs-lookup"><span data-stu-id="d1913-133">Issue</span></span>
* <span data-ttu-id="d1913-134">Действие с использованием API заканчивается сбоем, при этом во время выполнения или по завершении в журналах не отображается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="d1913-134">API action fails with no error message displayed at runtime or in logs.</span></span>

### <a name="causes"></a><span data-ttu-id="d1913-135">Причины</span><span class="sxs-lookup"><span data-stu-id="d1913-135">Causes</span></span>
* <span data-ttu-id="d1913-136">При неправильной интеграции многие элементы будут отключены в пользовательском интерфейсе Служб мобильного взаимодействия Azure и незаметно завершатся ошибкой в API, поэтому не забудьте проверить определенную функцию в пользовательском интерфейсе, чтобы убедиться, что она работает.</span><span class="sxs-lookup"><span data-stu-id="d1913-136">Many items will be disabled in the Azure Mobile Engagement UI if they aren't integrated correctly, but will fail silently from the API, so remember to test the same functionality from the UI to see if it works.</span></span>
* <span data-ttu-id="d1913-137">Службы мобильного взаимодействия Azure и множество дополнительных функций этих служб, которые вы намереваетесь применять, перед использованием необходимо отдельно интегрировать в приложение с помощью пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="d1913-137">Azure Mobile Engagement, and many advanced features of Azure Mobile Engagement you are attempting to use, need to be individually integrated into your app with the SDK as separate steps before you can use them.</span></span>

### <a name="see-also"></a><span data-ttu-id="d1913-138">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="d1913-138">See also</span></span>
* <span data-ttu-id="d1913-139">[Руководство по поиску и устранению проблем с интеграцией при использовании SDK][Link 25]</span><span class="sxs-lookup"><span data-stu-id="d1913-139">[Troubleshooting Guide - SDK][Link 25]</span></span>

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

