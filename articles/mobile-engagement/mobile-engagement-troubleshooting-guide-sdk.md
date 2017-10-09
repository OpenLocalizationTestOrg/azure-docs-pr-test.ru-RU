---
title: aaaAzure Mobile Engagement Troubleshooting Guide - SDK
description: "Устранение неполадок интеграции пакета в Службы мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: de265cf1-2f88-43ef-8616-156ada5be7b6
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1c082b81d898f4bdb47b8efe6cfbacfd83fe9279
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a><span data-ttu-id="a1666-103">Руководство по поиску и устранению проблем с интеграцией при использовании SDK</span><span class="sxs-lookup"><span data-stu-id="a1666-103">Troubleshooting guide for SDK integration issues</span></span>
<span data-ttu-id="a1666-104">Hello ниже приведены возможные проблемы, которые могут возникнуть с как Azure Mobile Engagement интегрирован в приложение.</span><span class="sxs-lookup"><span data-stu-id="a1666-104">hello following are possible issues you may encounter with how Azure Mobile Engagement integrates into your application.</span></span>

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a><span data-ttu-id="a1666-105">Проблемы SDK обнаруживаются, когда в другой области приложения происходит сбой</span><span class="sxs-lookup"><span data-stu-id="a1666-105">SDK issues discovered by a failure in another area of your application</span></span>
### <a name="issue"></a><span data-ttu-id="a1666-106">Проблема</span><span class="sxs-lookup"><span data-stu-id="a1666-106">Issue</span></span>
* <span data-ttu-id="a1666-107">Сбой сбора данных в пользовательском интерфейсе (в разделах аналитики, мониторинга, сегментации или панели мониторинга).</span><span class="sxs-lookup"><span data-stu-id="a1666-107">UI data collection failure (in Analytics, Monitoring, Segmentation, or Dashboards).</span></span>
* <span data-ttu-id="a1666-108">Сбои push-уведомлений (в приложении, вне приложения или и там и там).</span><span class="sxs-lookup"><span data-stu-id="a1666-108">Push Failures (Pushes don't work in app, out of app, or both).</span></span>
* <span data-ttu-id="a1666-109">Сбои дополнительных функций (не работает отслеживание, определение географического расположения, или не передаются push-уведомления на определенной платформе).</span><span class="sxs-lookup"><span data-stu-id="a1666-109">Advanced Feature Failures (Tracking, Geolocation, or platform specific Pushes don’t work).</span></span>
* <span data-ttu-id="a1666-110">Сбои API (часто сбои API происходят незаметно и без сообщений об ошибке).</span><span class="sxs-lookup"><span data-stu-id="a1666-110">API Failures (APIs fail often silently without error messages).</span></span>
* <span data-ttu-id="a1666-111">Сбои службы (ни один раздел Служб мобильного взаимодействия Azure не работает в приложении).</span><span class="sxs-lookup"><span data-stu-id="a1666-111">Service Failures (none of Azure Mobile Engagement works for your application).</span></span>

### <a name="causes"></a><span data-ttu-id="a1666-112">Причины</span><span class="sxs-lookup"><span data-stu-id="a1666-112">Causes</span></span>
* <span data-ttu-id="a1666-113">Большинство проблем, требующих toobe разрешен с помощью hello Azure Mobile Engagement SDK будет обнаружен сбой в приложении (например, сбой сбора данных пользовательского интерфейса, сбой принудительной, дополнительная возможность сбоя, ошибка API, сбои приложения или явной службы Сбой).</span><span class="sxs-lookup"><span data-stu-id="a1666-113">Most issues that need toobe resolved with hello Azure Mobile Engagement SDK will be discovered by a failure in your application (such as a UI data collection failure, push failure, advanced feature failure, API failure, Application crashes, or apparent service outage).</span></span>  
* <span data-ttu-id="a1666-114">Если конкретная функция Azure Mobile Engagement приложения перед никогда не работал, необходимо будет toocomplete hello интеграции.</span><span class="sxs-lookup"><span data-stu-id="a1666-114">If a particular feature of Azure Mobile Engagement has never worked in your app before, you will need toocomplete hello integration.</span></span> 
* <span data-ttu-id="a1666-115">Если конкретная функция Azure Mobile Engagement работали и остановлена, может потребоваться tooupgrade toohello последней версии с пакетом SDK Azure Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="a1666-115">If a particular feature of Azure Mobile Engagement was working and stopped, you may need tooupgrade toohello last version with hello Azure Mobile Engagement SDK.</span></span> <span data-ttu-id="a1666-116">Помните, что имеется другая версия hello Azure Mobile Engagement SDK для каждой платформы, поддерживаемые Azure Mobile Engagement (Android, iOS, Windows и Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="a1666-116">Remember that there is a different version of hello Azure Mobile Engagement SDK for each platform supported by Azure Mobile Engagement (Android, iOS, Windows, and Windows Phone).</span></span>

#### <a name="sdk-integration"></a><span data-ttu-id="a1666-117">Интеграция пакета SDK</span><span class="sxs-lookup"><span data-stu-id="a1666-117">SDK Integration</span></span>
* <span data-ttu-id="a1666-118">Службы мобильного взаимодействия Azure неправильно интегрированы в пакет SDK (раздел аналитики).</span><span class="sxs-lookup"><span data-stu-id="a1666-118">Azure Mobile Engagement not correctly integrated in SDK (Analytics).</span></span>
* <span data-ttu-id="a1666-119">Функция рекламных кампаний неправильно интегрирована в пакет SDK (push-уведомления в приложениях и вне приложений).</span><span class="sxs-lookup"><span data-stu-id="a1666-119">Reach not correctly integrated in SDK (In App and Out of App Pushes).</span></span>
* <span data-ttu-id="a1666-120">Истек срок действия сертификата, или используется неверная версия PROD или DEV (только iOS).</span><span class="sxs-lookup"><span data-stu-id="a1666-120">Certificate expired or incorrect PROD vs. DEV (iOS only).</span></span>
* <span data-ttu-id="a1666-121">Служба GCM или ADM неправильно интегрирована в пакет SDK (только в Android в отношении push-уведомлений конкретных служб).</span><span class="sxs-lookup"><span data-stu-id="a1666-121">GCM or ADM not correctly integrated in SDK (Android only - Service Specific Pushes).</span></span>
* <span data-ttu-id="a1666-122">Функция отслеживания неправильно интегрирована в пакет SDK (отслеживания установки из магазина).</span><span class="sxs-lookup"><span data-stu-id="a1666-122">Tracking not correctly integrated in SDK (Install store tracking).</span></span>
* <span data-ttu-id="a1666-123">Адаптирующееся расположение или GPS-расположение неправильно интегрировано в пакет SDK (отслеживание по GPS-расположению).</span><span class="sxs-lookup"><span data-stu-id="a1666-123">Lazy Location or GPS Location not correctly integrated in SDK (Targeting by geo-location).</span></span>

<span data-ttu-id="a1666-124">**См. также:**</span><span class="sxs-lookup"><span data-stu-id="a1666-124">**See also:**</span></span>

* <span data-ttu-id="a1666-125">[Документация по службам мобильного взаимодействия][Link 5]</span><span class="sxs-lookup"><span data-stu-id="a1666-125">[SDK Documentation - Integration Guides][Link 5]</span></span> 
* <span data-ttu-id="a1666-126">[Руководство по устранению неисправностей функций push-уведомлений и рекламных кампаний][Link 23]</span><span class="sxs-lookup"><span data-stu-id="a1666-126">[Troubleshooting Guide - Push][Link 23]</span></span>

#### <a name="sdk-upgrade"></a><span data-ttu-id="a1666-127">Обновление пакета SDK</span><span class="sxs-lookup"><span data-stu-id="a1666-127">SDK Upgrade</span></span>
* <span data-ttu-id="a1666-128">Требуется tooupgrade SDK tooresolve проблемы с более ранними версиями hello SDK (часто связанных toonewer версии ОС устройства hello).</span><span class="sxs-lookup"><span data-stu-id="a1666-128">Need tooupgrade SDK tooresolve issues with older versions of hello SDK (often related toonewer versions of hello device OS).</span></span>
* <span data-ttu-id="a1666-129">Удалите все предыдущие версии приложения с устройства и повторно установить последнюю версию приложения hello, hello повторно зарегистрировать ИД устройства из пользовательского интерфейса Azure Mobile Engagement tooconfirm hello, что устройство использует последнюю версию приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a1666-129">Uninstall all previous versions of your app from your device and reinstall hello newest version of your app, hello re-register your Device ID from hello Azure Mobile Engagement UI tooconfirm that your device is using hello newest version of your app.</span></span>

<span data-ttu-id="a1666-130">**См. также:**</span><span class="sxs-lookup"><span data-stu-id="a1666-130">**See also:**</span></span>

* [<span data-ttu-id="a1666-131">Документация к пакету SDK – примечания к выпуску</span><span class="sxs-lookup"><span data-stu-id="a1666-131">SDK Documentation - Release Notes</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [<span data-ttu-id="a1666-132">Документация к пакету SDK – руководства по обновлению</span><span class="sxs-lookup"><span data-stu-id="a1666-132">SDK Documentation - Upgrade Guides</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a><span data-ttu-id="a1666-133">Другие SDK</span><span class="sxs-lookup"><span data-stu-id="a1666-133">SDK Other</span></span>
* <span data-ttu-id="a1666-134">Ошибки в манифесте приложения «AndroidManifest.xml» может привести к Azure Mobile Engagement toowork (Android).</span><span class="sxs-lookup"><span data-stu-id="a1666-134">Errors in Application Manifest "AndroidManifest.xml" can cause Azure Mobile Engagement not toowork (Android only).</span></span>
* <span data-ttu-id="a1666-135">Распространенные проблемы с интеграцией пакета SDK и использование API — tooconfuse hello ключ SDK и hello ключ API.</span><span class="sxs-lookup"><span data-stu-id="a1666-135">A common issue with SDK integration and API usage is tooconfuse hello SDK Key and hello API Key.</span></span>

<span data-ttu-id="a1666-136">**См. также:**</span><span class="sxs-lookup"><span data-stu-id="a1666-136">**See also:**</span></span>

* <span data-ttu-id="a1666-137">[Основные понятия Azure Mobile Engagement][Link 6]</span><span class="sxs-lookup"><span data-stu-id="a1666-137">[Concepts - Glossary][Link 6]</span></span>

## <a name="advanced-coding-issues"></a><span data-ttu-id="a1666-138">Более сложные проблемы кодирования</span><span class="sxs-lookup"><span data-stu-id="a1666-138">Advanced coding issues</span></span>
### <a name="issue"></a><span data-ttu-id="a1666-139">Проблема</span><span class="sxs-lookup"><span data-stu-id="a1666-139">Issue</span></span>
* <span data-ttu-id="a1666-140">Определенный код платформы не связаны tooAzure мобильного охвата может вызвать проблемы в iOS, Android и Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="a1666-140">Platform specific code not directly related tooAzure Mobile Engagement can cause issues on iOS, Android, and Windows Phone.</span></span>

### <a name="causes"></a><span data-ttu-id="a1666-141">Причины</span><span class="sxs-lookup"><span data-stu-id="a1666-141">Causes</span></span>
* <span data-ttu-id="a1666-142">Причиной многих дополнительных ошибок кодирования, связанных с Azure Mobile Engagement неправильно написанный платформы конкретного кода не напрямую, связанные с tooAzure мобильного охвата.</span><span class="sxs-lookup"><span data-stu-id="a1666-142">Many advanced coding issues with Azure Mobile Engagement are caused by improperly written platform specific code not directly related tooAzure Mobile Engagement.</span></span> <span data-ttu-id="a1666-143">Вам потребуется tooconsult документации toohello определенной платформы, разрабатываемом для Кроме документации мобильного охвата tooAzure (Android, iOS, Web, Windows и Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="a1666-143">You will need tooconsult documentation specific toohello platform you are developing for in addition tooAzure Mobile Engagement documentation (Android, iOS, Web, Windows, and Windows Phone).</span></span>
* <span data-ttu-id="a1666-144">Настройка неправильно «категории», предотвращает связывания из расположения tooanother уведомления внутри или за пределами приложение hello (Android).</span><span class="sxs-lookup"><span data-stu-id="a1666-144">Not correctly configuring "categories", prevents linking from a notification tooanother location either inside or outside of hello app (Android only).</span></span> 
* <span data-ttu-id="a1666-145">Не параметр «UIKit.framework» слишком «необязательные» в коде операций ввода-вывода, отображает «Ошибка не найдена "Symbol» и/или аварийно завершает работу на старые устройства iOS (только iOS).</span><span class="sxs-lookup"><span data-stu-id="a1666-145">Not setting "UIKit.framework" too"optional" in your iOS code, shows a "Symbol not found error" and/or crashes on older iOS devices (iOS only).</span></span>
* <span data-ttu-id="a1666-146">Просроченные сертификаты или используя неправильно hello разработки или версии Prod hello cert, принудительной причины проблемы (только iOS).</span><span class="sxs-lookup"><span data-stu-id="a1666-146">Expired certificates or not correctly using hello DEV or Prod version of hello cert, causes push issues (iOS only).</span></span>
* <span data-ttu-id="a1666-147">Существуют некоторые ограничения специфические tooa платформу, которая не может управлять Azure Mobile Engagement (например, как работает hello system center для вне приложения Push-уведомлений в iOS и Android).</span><span class="sxs-lookup"><span data-stu-id="a1666-147">There are some limitations inherent tooa platform that Azure Mobile Engagement can't control (like how hello system center works for out of app pushes in Android and iOS).</span></span>
* <span data-ttu-id="a1666-148">Azure Mobile Engagement публикует полный список пакетов внутренней hello, используемые Azure Mobile Engagement для iOS и Android для ссылки.</span><span class="sxs-lookup"><span data-stu-id="a1666-148">Azure Mobile Engagement publishes a full list of hello internal packages used by Azure Mobile Engagement for iOS and Android for reference.</span></span> <span data-ttu-id="a1666-149">Имейте в виду, что некоторые функции Azure Mobile Engagement являются toohello конкретных платформ (Android, iOS, Web, Windows и Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="a1666-149">Keep in mind that some features of Azure Mobile Engagement are specific toohello platform (Android, iOS, Web, Windows, and Windows Phone).</span></span>

### <a name="see-also"></a><span data-ttu-id="a1666-150">См. также</span><span class="sxs-lookup"><span data-stu-id="a1666-150">See also</span></span>
* <span data-ttu-id="a1666-151">[Руководство по устранению неисправностей функций push-уведомлений и рекламных кампаний][Link 23]</span><span class="sxs-lookup"><span data-stu-id="a1666-151">[Troubleshooting Guide - Push][Link 23]</span></span> 
* <span data-ttu-id="a1666-152">[Документация по службам мобильного взаимодействия][Link 5]</span><span class="sxs-lookup"><span data-stu-id="a1666-152">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="a1666-153">[Документация по службам мобильного взаимодействия][Link 5]</span><span class="sxs-lookup"><span data-stu-id="a1666-153">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="application-crashes"></a><span data-ttu-id="a1666-154">Сбои приложений</span><span class="sxs-lookup"><span data-stu-id="a1666-154">Application crashes</span></span>
### <a name="issue"></a><span data-ttu-id="a1666-155">Проблема</span><span class="sxs-lookup"><span data-stu-id="a1666-155">Issue</span></span>
* <span data-ttu-id="a1666-156">Приложение аварийно завершает работу на устройстве hello конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="a1666-156">Your application crashes on hello end users' device.</span></span>

### <a name="causes"></a><span data-ttu-id="a1666-157">Причины</span><span class="sxs-lookup"><span data-stu-id="a1666-157">Causes</span></span>
* <span data-ttu-id="a1666-158">Об аварийных завершениях можно просмотреть в hello *пользовательского интерфейса Analytics* или hello *API аналитики*</span><span class="sxs-lookup"><span data-stu-id="a1666-158">Crash information can be viewed in hello *Analytics UI* or hello *Analytics API*</span></span>
* <span data-ttu-id="a1666-159">Можно найти hello идентификатор устройства тестирования устройства и предпринять hello же действие, вызвавшее toocrash вашего приложения для конечных пользователей toohelp определить причину hello вашей аварийного завершения.</span><span class="sxs-lookup"><span data-stu-id="a1666-159">You can find hello Device ID of your test device and take hello same action that caused your application toocrash for an end user toohelp identify hello cause of your crash.</span></span>
* <span data-ttu-id="a1666-160">Известные проблемы с Azure Mobile Engagement SDK hello, вызывающие toocrash приложений иногда решена обновление toohello последнюю версию пакета SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="a1666-160">Known issues with hello Azure Mobile Engagement SDK that cause applications toocrash are sometimes resolved by upgrading toohello latest version of hello SDK.</span></span> <span data-ttu-id="a1666-161">Убедитесь, что toocheck hello заметках о выпуске на платформе при анализе сбоев.</span><span class="sxs-lookup"><span data-stu-id="a1666-161">Make sure toocheck hello release notes about your platform when investigating crashes.</span></span>

### <a name="see-also"></a><span data-ttu-id="a1666-162">См. также</span><span class="sxs-lookup"><span data-stu-id="a1666-162">See also</span></span>
* <span data-ttu-id="a1666-163">[Документация по службам мобильного взаимодействия][Link 5]</span><span class="sxs-lookup"><span data-stu-id="a1666-163">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="a1666-164">[Документация по службам мобильного взаимодействия][Link 5]</span><span class="sxs-lookup"><span data-stu-id="a1666-164">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="app-store-upload-failures"></a><span data-ttu-id="a1666-165">Сбои передачи в магазин приложений</span><span class="sxs-lookup"><span data-stu-id="a1666-165">App store upload failures</span></span>
### <a name="issue"></a><span data-ttu-id="a1666-166">Проблема</span><span class="sxs-lookup"><span data-stu-id="a1666-166">Issue</span></span>
* <span data-ttu-id="a1666-167">Ошибки, связанные с toouploading hello последнюю версию приложения tooApple, Google или магазина Windows hello.</span><span class="sxs-lookup"><span data-stu-id="a1666-167">Errors related toouploading hello latest version of your app tooApple, Google, or hello Windows App store.</span></span>

### <a name="causes"></a><span data-ttu-id="a1666-168">Причины</span><span class="sxs-lookup"><span data-stu-id="a1666-168">Causes</span></span>
* <span data-ttu-id="a1666-169">Приложение сохраняет иногда блокировать приложений с определенных включенными функциями (например hello Apple Store предотвращает использование hello IDFV приложений в магазине hello а хранилища GooglePlay hello hello совместное использование информации приложения между приложениями).</span><span class="sxs-lookup"><span data-stu-id="a1666-169">App stores sometimes block apps with certain features enabled (e.g. hello Apple Store prevents hello use of IDFV in apps in hello store and hello GooglePlay store prevents hello sharing of application information between apps).</span></span> 
* <span data-ttu-id="a1666-170">Убедитесь, что проверка hello замечания о платформе и текущая версия пакета SDK для hello при возникновении затруднений при отправке toohello магазина.</span><span class="sxs-lookup"><span data-stu-id="a1666-170">Make sure that you check hello release notes about your platform and current version of hello SDK if you have difficulty uploading an app toohello store.</span></span>

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
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

