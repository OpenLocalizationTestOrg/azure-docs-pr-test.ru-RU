---
title: "Пользовательский интерфейс Служб мобильного взаимодействия Azure — Рекламная кампания"
description: "Узнайте, как создавать кампании push-уведомлений с помощью Служб мобильного взаимодействия Azure, а также управлять ими"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2fe124a2-a86f-4136-81ba-a9d298ec798a
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: fc88db8db11d1ed12fa95c2087c9a32b21bf4de5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-manage-push-notification-campaigns"></a><span data-ttu-id="c77db-103">Создание кампаний по рассылке push-уведомлений и управление ими</span><span class="sxs-lookup"><span data-stu-id="c77db-103">How to create and manage push notification campaigns</span></span>
<span data-ttu-id="c77db-104">В разделе «Охват» можно создать новую кампанию push-уведомлений по сложной формуле, предоставив всю информацию, необходимую для отправки push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="c77db-104">You can use the Reach section of the UI to create a new Push campaign with a complex formula by providing all the information you need to send a push notification.</span></span> <span data-ttu-id="c77db-105">Параметры кампании по рассылке push-уведомлений немного отличаются в зависимости от типа кампании. Этих типов всего четыре: объявления, опросы, отправленные данные и плитки (только для Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="c77db-105">The options of a Push campaign vary slightly depending on the four campaign types: Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span>

### <a name="option-applies-to"></a><span data-ttu-id="c77db-106">Параметр применяется к таким разделам:</span><span class="sxs-lookup"><span data-stu-id="c77db-106">Option Applies to:</span></span>
* <span data-ttu-id="c77db-107">Языки: все типы кампаний (объявления, опросы, отправленные данные и плитки).</span><span class="sxs-lookup"><span data-stu-id="c77db-107">Languages:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="c77db-108">Кампания: все типы кампаний (объявления, опросы, отправленные данные и плитки).</span><span class="sxs-lookup"><span data-stu-id="c77db-108">Campaign:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="c77db-109">Уведомление: объявления, опросы.</span><span class="sxs-lookup"><span data-stu-id="c77db-109">Notification:     Announcements, Polls</span></span>
* <span data-ttu-id="c77db-110">Содержимое: уникально для каждого типа кампании.</span><span class="sxs-lookup"><span data-stu-id="c77db-110">Content:    Unique for each campaign type</span></span>
* <span data-ttu-id="c77db-111">Аудитория: все типы кампаний (объявления, опросы, отправленные данные и плитки).</span><span class="sxs-lookup"><span data-stu-id="c77db-111">Audience:     All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="c77db-112">Интервал времени: объявления, опросы и плитки.</span><span class="sxs-lookup"><span data-stu-id="c77db-112">Time frame:     Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="c77db-113">Тест: все типы кампаний (объявления, опросы, отправленные данные и плитки).</span><span class="sxs-lookup"><span data-stu-id="c77db-113">Test:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>

![Кампания — охват1][20]

## <a name="languages"></a><span data-ttu-id="c77db-115">Языки</span><span class="sxs-lookup"><span data-stu-id="c77db-115">Languages</span></span>
<span data-ttu-id="c77db-116">С помощью раскрывающегося меню «Языки» можно отправлять разные версии push-уведомления на устройства, в которых настроено использование разных языков.</span><span class="sxs-lookup"><span data-stu-id="c77db-116">You can use the Languages drop-down menu to send a different version of your Push to devices that are set to use different languages.</span></span> <span data-ttu-id="c77db-117">По умолчанию все устройства будут получать одинаковые push-уведомления независимо от настроенного в них языка.</span><span class="sxs-lookup"><span data-stu-id="c77db-117">By default, all devices will receive the same Push regardless of what language they are set to use.</span></span> <span data-ttu-id="c77db-118">Если в устройстве настроен другой язык, пользователь получит push-уведомление на языке по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c77db-118">Users with their device set to a different language will receive the Default Language version of the Push.</span></span> <span data-ttu-id="c77db-119">В кампании push-уведомлений есть множество параметров, позволяющих указать альтернативное содержимое для каждого из дополнительных выбираемых языков.</span><span class="sxs-lookup"><span data-stu-id="c77db-119">Many of the push campaign options allow you to specify alternate content for each of the additional languages you select.</span></span> 

![Кампания — охват2][21]

### <a name="language-differences-apply-to"></a><span data-ttu-id="c77db-121">Различия в языке применяются к таким разделам:</span><span class="sxs-lookup"><span data-stu-id="c77db-121">Language differences apply to:</span></span>
* <span data-ttu-id="c77db-122">Языки: возможность выбора других дополнительных языков.</span><span class="sxs-lookup"><span data-stu-id="c77db-122">Languages:    Unique languages may be selected in addition to the default language</span></span>
* <span data-ttu-id="c77db-123">Кампания: одинаково для всех языков.</span><span class="sxs-lookup"><span data-stu-id="c77db-123">Campaign:    Same for all languages</span></span>
* <span data-ttu-id="c77db-124">Уведомление: уникально для каждого дополнительно выбранного языка.</span><span class="sxs-lookup"><span data-stu-id="c77db-124">Notification:    Unique for each language in addition to the default language</span></span>
* <span data-ttu-id="c77db-125">Содержимое: уникально для каждого дополнительно выбранного языка.</span><span class="sxs-lookup"><span data-stu-id="c77db-125">Content:    Unique for each language in addition to the default language</span></span>
* <span data-ttu-id="c77db-126">Аудитория: возможность фильтрации отдельно по языковому критерию.</span><span class="sxs-lookup"><span data-stu-id="c77db-126">Audience:     May be filtered by a separate language criterion</span></span>
* <span data-ttu-id="c77db-127">Интервал времени: одинаково для всех языков.</span><span class="sxs-lookup"><span data-stu-id="c77db-127">Time frame:     Same for all languages</span></span>
* <span data-ttu-id="c77db-128">Тест: возможность одновременной отправки для каждого языка.</span><span class="sxs-lookup"><span data-stu-id="c77db-128">Test:    May be sent to each language at a time</span></span>

### <a name="supported-languages"></a><span data-ttu-id="c77db-129">Поддерживаемые языки:</span><span class="sxs-lookup"><span data-stu-id="c77db-129">Supported Languages:</span></span>
* <span data-ttu-id="c77db-130">Арабский (ar)</span><span class="sxs-lookup"><span data-stu-id="c77db-130">Arabic (ar)</span></span> 
* <span data-ttu-id="c77db-131">Болгарский (bg)</span><span class="sxs-lookup"><span data-stu-id="c77db-131">Bulgarian (bg)</span></span> 
* <span data-ttu-id="c77db-132">Каталонский (ca)</span><span class="sxs-lookup"><span data-stu-id="c77db-132">Catalan (ca)</span></span> 
* <span data-ttu-id="c77db-133">Китайский (zh)</span><span class="sxs-lookup"><span data-stu-id="c77db-133">Chinese (zh)</span></span> 
* <span data-ttu-id="c77db-134">Хорватский (hr)</span><span class="sxs-lookup"><span data-stu-id="c77db-134">Croatian (hr)</span></span> 
* <span data-ttu-id="c77db-135">Чешский (cs)</span><span class="sxs-lookup"><span data-stu-id="c77db-135">Czech (cs)</span></span> 
* <span data-ttu-id="c77db-136">Датский (da)</span><span class="sxs-lookup"><span data-stu-id="c77db-136">Danish (da)</span></span> 
* <span data-ttu-id="c77db-137">Нидерландский (nl)</span><span class="sxs-lookup"><span data-stu-id="c77db-137">Dutch (nl)</span></span> 
* <span data-ttu-id="c77db-138">Английский (en)</span><span class="sxs-lookup"><span data-stu-id="c77db-138">English (en)</span></span> 
* <span data-ttu-id="c77db-139">Финский (fi)</span><span class="sxs-lookup"><span data-stu-id="c77db-139">Finnish (fi)</span></span> 
* <span data-ttu-id="c77db-140">Французский (fr)</span><span class="sxs-lookup"><span data-stu-id="c77db-140">French (fr)</span></span> 
* <span data-ttu-id="c77db-141">Немецкий (de)</span><span class="sxs-lookup"><span data-stu-id="c77db-141">German (de)</span></span> 
* <span data-ttu-id="c77db-142">Греческий (el)</span><span class="sxs-lookup"><span data-stu-id="c77db-142">Greek (el)</span></span> 
* <span data-ttu-id="c77db-143">Иврит (he)</span><span class="sxs-lookup"><span data-stu-id="c77db-143">Hebrew (he)</span></span> 
* <span data-ttu-id="c77db-144">Хинди (hi)</span><span class="sxs-lookup"><span data-stu-id="c77db-144">Hindi (hi)</span></span> 
* <span data-ttu-id="c77db-145">Венгерский (hu)</span><span class="sxs-lookup"><span data-stu-id="c77db-145">Hungarian (hu)</span></span> 
* <span data-ttu-id="c77db-146">Индонезийский (id)</span><span class="sxs-lookup"><span data-stu-id="c77db-146">Indonesian (id)</span></span> 
* <span data-ttu-id="c77db-147">Итальянский (it)</span><span class="sxs-lookup"><span data-stu-id="c77db-147">Italian (it)</span></span> 
* <span data-ttu-id="c77db-148">Японский (ja)</span><span class="sxs-lookup"><span data-stu-id="c77db-148">Japanese (ja)</span></span> 
* <span data-ttu-id="c77db-149">Корейский (ko)</span><span class="sxs-lookup"><span data-stu-id="c77db-149">Korean (ko)</span></span> 
* <span data-ttu-id="c77db-150">Латышский (lv)</span><span class="sxs-lookup"><span data-stu-id="c77db-150">Latvian (lv)</span></span> 
* <span data-ttu-id="c77db-151">Литовский (lt)</span><span class="sxs-lookup"><span data-stu-id="c77db-151">Lithuanian (lt)</span></span> 
* <span data-ttu-id="c77db-152">Малайский (макроязык) (ms)</span><span class="sxs-lookup"><span data-stu-id="c77db-152">Malay (macrolanguage) (ms)</span></span> 
* <span data-ttu-id="c77db-153">Норвежский (букмол) (nb)</span><span class="sxs-lookup"><span data-stu-id="c77db-153">Norwegian Bokmål (nb)</span></span> 
* <span data-ttu-id="c77db-154">Польский (pl)</span><span class="sxs-lookup"><span data-stu-id="c77db-154">Polish (pl)</span></span> 
* <span data-ttu-id="c77db-155">Португальский (pt)</span><span class="sxs-lookup"><span data-stu-id="c77db-155">Portuguese (pt)</span></span> 
* <span data-ttu-id="c77db-156">Румынский (ro)</span><span class="sxs-lookup"><span data-stu-id="c77db-156">Romanian (ro)</span></span> 
* <span data-ttu-id="c77db-157">Русский (ru)</span><span class="sxs-lookup"><span data-stu-id="c77db-157">Russian (ru)</span></span> 
* <span data-ttu-id="c77db-158">Сербский (sr)</span><span class="sxs-lookup"><span data-stu-id="c77db-158">Serbian (sr)</span></span> 
* <span data-ttu-id="c77db-159">Словацкий (sk)</span><span class="sxs-lookup"><span data-stu-id="c77db-159">Slovak (sk)</span></span> 
* <span data-ttu-id="c77db-160">Словенский (sl)</span><span class="sxs-lookup"><span data-stu-id="c77db-160">Slovenian (sl)</span></span> 
* <span data-ttu-id="c77db-161">Испанский (es)</span><span class="sxs-lookup"><span data-stu-id="c77db-161">Spanish (es)</span></span> 
* <span data-ttu-id="c77db-162">Шведский (sv)</span><span class="sxs-lookup"><span data-stu-id="c77db-162">Swedish (sv)</span></span> 
* <span data-ttu-id="c77db-163">Тагальский (tl)</span><span class="sxs-lookup"><span data-stu-id="c77db-163">Tagalog (tl)</span></span> 
* <span data-ttu-id="c77db-164">Тайский (th)</span><span class="sxs-lookup"><span data-stu-id="c77db-164">Thai (th)</span></span> 
* <span data-ttu-id="c77db-165">Турецкий (tr)</span><span class="sxs-lookup"><span data-stu-id="c77db-165">Turkish (tr)</span></span> 
* <span data-ttu-id="c77db-166">Украинский (uk)</span><span class="sxs-lookup"><span data-stu-id="c77db-166">Ukrainian (uk)</span></span> 
* <span data-ttu-id="c77db-167">Вьетнамский (vi)</span><span class="sxs-lookup"><span data-stu-id="c77db-167">Vietnamese (vi)</span></span> 

## <a name="campaign"></a><span data-ttu-id="c77db-168">Кампания</span><span class="sxs-lookup"><span data-stu-id="c77db-168">Campaign</span></span>
<span data-ttu-id="c77db-169">Раздел «Охват» можно использовать, чтобы задать имя и категорию для кампании, а также, если вы не планируете использовать раздел «Аудитория» кампании push-уведомлений и хотите отправить ее через Reach API (и с помощью некоторых элементов API push-уведомлений низкого уровня).</span><span class="sxs-lookup"><span data-stu-id="c77db-169">You can use the Campaign section to set the name and category of your campaign as well as if you plan to ignore the audience section of a Push campaign and send this campaign via the Reach API (and some elements with the low level Push API) instead.</span></span> <span data-ttu-id="c77db-170">Категории можно использовать с пользовательским шаблоном уведомлений, чтобы управлять уведомлениями в приложении на основе предопределенных параметров.</span><span class="sxs-lookup"><span data-stu-id="c77db-170">Categories can be used with a custom notification template to control in-app notifications based on predefined settings.</span></span> <span data-ttu-id="c77db-171">Список существующих категорий можно получить через API охвата.</span><span class="sxs-lookup"><span data-stu-id="c77db-171">You can get a list of your existing “Categories” via the Reach API.</span></span>

> [!WARNING]
> <span data-ttu-id="c77db-172">При использовании параметра "Не учитывать аудиторию, push-уведомления будут отправляться пользователям через API" в разделе кампаний рекламной кампании кампания НЕ будет отправляться автоматически. Ее необходимо отправлять вручную через Reach API.</span><span class="sxs-lookup"><span data-stu-id="c77db-172">If you use the "Ignore Audience, push will be sent to users via the API" option in the "Campaign" section of a Reach campaign, the campaign will NOT automatically send, you will need to send it manually via the Reach API.</span></span>

![Кампания — охват3][22]

### <a name="option-applies-to"></a><span data-ttu-id="c77db-174">Параметр применяется к таким разделам:</span><span class="sxs-lookup"><span data-stu-id="c77db-174">Option Applies to:</span></span>
* <span data-ttu-id="c77db-175">Имя: все кампании.</span><span class="sxs-lookup"><span data-stu-id="c77db-175">Name:    All</span></span>
* <span data-ttu-id="c77db-176">Категория: объявления, опросы.</span><span class="sxs-lookup"><span data-stu-id="c77db-176">Category:    Announcements, Polls</span></span>
* <span data-ttu-id="c77db-177">Игнорировать аудиторию, push-уведомление будет отправлено пользователям через API: все кампании.</span><span class="sxs-lookup"><span data-stu-id="c77db-177">Ignore Audience, push will be sent to users via the API:    All</span></span>

## <a name="notification"></a><span data-ttu-id="c77db-178">Уведомление</span><span class="sxs-lookup"><span data-stu-id="c77db-178">Notification</span></span>
<span data-ttu-id="c77db-179">В разделе «Уведомление» можно задать основные параметры для push-уведомлений. Эти параметры включают название push-уведомления, сообщение, изображения в приложении, а также возможность закрыть это уведомление.</span><span class="sxs-lookup"><span data-stu-id="c77db-179">You can use the Notification section to set basic settings for your push including: The title of the Push, the message, an in-app image, or if it is dismissible.</span></span> <span data-ttu-id="c77db-180">Многие параметры уведомлений зависят от платформы устройства.</span><span class="sxs-lookup"><span data-stu-id="c77db-180">Many notification settings are specific to the platform of your device.</span></span> <span data-ttu-id="c77db-181">Вы можете выбрать способ отправки push-уведомлений: в приложении, за пределами приложения или оба варианта.</span><span class="sxs-lookup"><span data-stu-id="c77db-181">You can select whether your push will be sent "in app" or "out of app" or both.</span></span> <span data-ttu-id="c77db-182">(Помните, что пользователи могут согласиться или отказаться получать push-уведомления вне приложения на уровне операционной системы в устройствах. Службы мобильного взаимодействия Azure не смогут переопределить этот параметр.</span><span class="sxs-lookup"><span data-stu-id="c77db-182">(Remember that users can "opt-in" or "opt-out" of "out of app" Pushes at the Operating System level on their devices, and Azure Mobile Engagement will not be able to override this setting.</span></span> <span data-ttu-id="c77db-183">Также следует помнить, что API охвата обрабатывает push-уведомления в приложении и вне приложения.</span><span class="sxs-lookup"><span data-stu-id="c77db-183">Also remember that the Reach API handles "in app" and "out of app" Pushes.</span></span> <span data-ttu-id="c77db-184">Для обработки push-уведомлений вне приложения также используется API push-уведомлений). Для push-уведомлений можно настроить изображения или HTML-содержимое, включая прямые ссылки для перехода вне приложения или перехода в другое расположение в приложении (требуются категории намерений пакета SDK для Android версии 2.1.0 или более поздней).</span><span class="sxs-lookup"><span data-stu-id="c77db-184">The Push API can be used to handle "out of app" pushes too.) Pushes can be customized with pictures or HTML content, including deep links for linking outside of your App or to another location in your App (Android SDK 2.1.0 or later intent categories required).</span></span> <span data-ttu-id="c77db-185">Вы можете изменить значок или индикатор iOS и отправлять текст или веб-содержимое (всплывающее окно с HTML-содержимым, ссылка с URL-адресом на другое расположение в или вне приложения).</span><span class="sxs-lookup"><span data-stu-id="c77db-185">You can change the icon or iOS badge, and send either text or web content (a popup with html content, URL link to another location either inside or outside of the app).</span></span> <span data-ttu-id="c77db-186">Кроме того, можно настроить устройство с ОС Android таким образом, чтобы оно издавало сигнал или вибрировало при получении push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="c77db-186">You can also make Android devices ring or vibrate with the Push.</span></span> <span data-ttu-id="c77db-187">(Помните, чтобы устройство издавало сигнал или вибрировало, требуются правильные разрешения пакета SDK в файле манифеста в устройстве с ОС Android). Сейчас отраслевой стандарт для размера больших изображений устройств с ОС Android отсутствует, так как размеры экрана в каждом устройстве отличаются. Однако изображения размером 400x100 отображаются на экранах практически любого размера.</span><span class="sxs-lookup"><span data-stu-id="c77db-187">(Remember that you will need the correct SDK permissions in your Android manifest file to ring or vibrate a device.) There is currently no industry standard for Android "Big Picture" sizes, since screen sizes are different on every device, but 400x100 pictures work on almost any screen size.</span></span>

### <a name="delivery-types"></a><span data-ttu-id="c77db-188">Типы доставки</span><span class="sxs-lookup"><span data-stu-id="c77db-188">Delivery Types:</span></span>
* <span data-ttu-id="c77db-189">Только вне приложения: уведомление будет доставлено, когда пользователь не использует приложение.</span><span class="sxs-lookup"><span data-stu-id="c77db-189">Out of app only: the notification will be delivered when the user does not use the application.</span></span>
* <span data-ttu-id="c77db-190">Для доставки уведомления только вне приложения требуется сертификат Apple или Google (сертификат APNS или GCM).</span><span class="sxs-lookup"><span data-stu-id="c77db-190">The out of app only notification requires a certificate from Apple or Google (APNS or GCM certificate).</span></span>
* <span data-ttu-id="c77db-191">Только в приложении: уведомление отображается, только если запущено приложение.</span><span class="sxs-lookup"><span data-stu-id="c77db-191">In-app only: The notification appears only when the application is running.</span></span>
* <span data-ttu-id="c77db-192">Для доставки уведомления пользователю используется система доставки Capptain.</span><span class="sxs-lookup"><span data-stu-id="c77db-192">The notification uses the Capptain delivery system to reach the user.</span></span> <span data-ttu-id="c77db-193">Вы можете полностью настроить визуальный макет и отображение своего push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="c77db-193">You can fully customize the visual layout/display of your push.</span></span>
* <span data-ttu-id="c77db-194">В любое время: этот параметр отвечает за отправку уведомления независимо от того, работает приложение или нет.</span><span class="sxs-lookup"><span data-stu-id="c77db-194">Anytime: This option ensures that you send a notification either the application is running or not.</span></span>

![Кампания — охват4][23]

### <a name="option-applies-to"></a><span data-ttu-id="c77db-196">Параметр применяется к таким разделам:</span><span class="sxs-lookup"><span data-stu-id="c77db-196">Option Applies to:</span></span>
* <span data-ttu-id="c77db-197">Уведомление: объявления, опросы.</span><span class="sxs-lookup"><span data-stu-id="c77db-197">Notification:     Announcements, Polls</span></span>

## <a name="content"></a><span data-ttu-id="c77db-198">Содержимое</span><span class="sxs-lookup"><span data-stu-id="c77db-198">Content</span></span>
<span data-ttu-id="c77db-199">В разделе «Содержимое» можно изменить содержимое объявлений, опросов, отправленных данных и плиток (только для Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="c77db-199">You can use the Content section to modify the content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="c77db-200">Параметр, управляющий типом содержимого кампаний рush-уведомлений, зависит от типа кампании.</span><span class="sxs-lookup"><span data-stu-id="c77db-200">The Content setting of Push campaigns is specific to the type of campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="c77db-201">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="c77db-201">See also</span></span>
* <span data-ttu-id="c77db-202">[Управление уникальным контентом для различных типов кампаний push-уведомлений][Link 29]</span><span class="sxs-lookup"><span data-stu-id="c77db-202">[UI Documentation - Reach - Push Content][Link 29]</span></span>

![Кампания — охват5][24]

## <a name="audience"></a><span data-ttu-id="c77db-204">Аудитория</span><span class="sxs-lookup"><span data-stu-id="c77db-204">Audience</span></span>
<span data-ttu-id="c77db-205">С помощью раздела «Аудитория» можно определить стандартный список элементов, ограничивающих кампании, или ограничить кампании на основе настраиваемых критериев.</span><span class="sxs-lookup"><span data-stu-id="c77db-205">You can use the Audience section to define a standard list of items to limit your campaign or limits your campaign based on customized criteria.</span></span> <span data-ttu-id="c77db-206">Стандартный набор параметров для ограничения аудитории позволяет отправлять push-уведомления старым и новым пользователям, а также отправлять пользователям только системные push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="c77db-206">The standard set of options to Limit your Audience allows you to push to either new or old users or native push users only.</span></span> <span data-ttu-id="c77db-207">Кроме того, можно задать квоту, чтобы ограничить число пользователей, которые получают push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="c77db-207">You can also set a quota to limit the number of users who receive the push.</span></span> <span data-ttu-id="c77db-208">Вы можете вручную изменить выражение для фильтрации кампании, чтобы добавить один или несколько критериев для отслеживания пользователей.</span><span class="sxs-lookup"><span data-stu-id="c77db-208">You can manually Edit the expression for how your campaign is filtered to include one or more criterion to target users.</span></span> <span data-ttu-id="c77db-209">Выражение, определяющее связь между критериями, определяющими целевую аудиторию, можно вводить вручную.</span><span class="sxs-lookup"><span data-stu-id="c77db-209">You can manually type an audience expression.</span></span> <span data-ttu-id="c77db-210">Такое выражение должно явно определять связь между критериями.</span><span class="sxs-lookup"><span data-stu-id="c77db-210">Such an expression must explicitly define the relation between criteria.</span></span> <span data-ttu-id="c77db-211">Критерий описывается идентификатором, который должен начинаться с заглавной буквы и не должен содержать пробелы.</span><span class="sxs-lookup"><span data-stu-id="c77db-211">A criterion is described by an identifier that must start with a capital letter and cannot contain spaces.</span></span> <span data-ttu-id="c77db-212">Отношение между критериями можно описать с помощью операторов «and», «or», «not», а также символов «(",")».</span><span class="sxs-lookup"><span data-stu-id="c77db-212">The relation between the criteria can be described using 'and', 'or', 'not' operators as well as '(', ')'.</span></span> <span data-ttu-id="c77db-213">Пример: «критерий1 or (критерий1 and not критерий2)».</span><span class="sxs-lookup"><span data-stu-id="c77db-213">Example: "Criterion1 or (Criterion1 and not Criterion2)".</span></span>

> [!NOTE]
> <span data-ttu-id="c77db-214">Если кампания содержит большую аудиторию, серверное целевое сканирование может выполняться медленно, особенно при попытке запустить несколько кампаний одновременно.</span><span class="sxs-lookup"><span data-stu-id="c77db-214">With a large audience included in campaigns, the server side targeting scan can be slow, especially if you attempt to start multiple campaigns at the same time.</span></span>

* <span data-ttu-id="c77db-215">По возможности запускайте только одну кампанию за раз.</span><span class="sxs-lookup"><span data-stu-id="c77db-215">If possible, only start one campaign at a time.</span></span>
* <span data-ttu-id="c77db-216">Запускайте не больше четырех кампаний одновременно.</span><span class="sxs-lookup"><span data-stu-id="c77db-216">At the most, only start four campaigns at a time.</span></span>
* <span data-ttu-id="c77db-217">Отправляйте push-уведомления только активным пользователям (флажок «Использовать только пользователей, которым можно отправить системное push-уведомление» и «Использовать только активных пользователей»), чтобы сканировались только пользователи с установленным приложением, использующие его.</span><span class="sxs-lookup"><span data-stu-id="c77db-217">Push only to your active users (checkbox "Engage only users who can be reached using Native Push" and "Engage only active users") so that only your users who still have the app installed and use it will need to be scanned.</span></span>
  <span data-ttu-id="c77db-218">После определения аудитории можно нажать кнопку «Моделировать», чтобы узнать количество пользователей, которые получат это push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="c77db-218">Once your audience is defined, you can use the simulate button to find out how many users will receive this Push.</span></span> <span data-ttu-id="c77db-219">Таким образом будет рассчитано количество известных пользователей, потенциально включенных в эту аудиторию (оценка основана на случайной выборке пользователей).</span><span class="sxs-lookup"><span data-stu-id="c77db-219">This will compute the number of known users potentially targeted by this audience (this is an estimate based on a random sample of users).</span></span> <span data-ttu-id="c77db-220">Учтите, что пользователи, удалившие приложение, также являются частью этой аудитории, но им невозможно отправить уведомление.</span><span class="sxs-lookup"><span data-stu-id="c77db-220">Be aware that users who have uninstalled the application are also part of this audience, but cannot be reached.</span></span>

### <a name="see-also"></a><span data-ttu-id="c77db-221">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="c77db-221">See also</span></span>
* <span data-ttu-id="c77db-222">[Организация кампаний по рассылке push-уведомлений выбранному подмножеству пользователей с помощью условий таргетинга][Link 28]</span><span class="sxs-lookup"><span data-stu-id="c77db-222">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

![Кампания — охват6][25]

### <a name="edit-expression"></a><span data-ttu-id="c77db-224">Выражение для изменения</span><span class="sxs-lookup"><span data-stu-id="c77db-224">Edit expression</span></span>
![Кампания — охват7][26]

### <a name="limit-your-audience-option-applies-to"></a><span data-ttu-id="c77db-226">Параметр «Ограничить аудиторию» применяется к таким параметрам:</span><span class="sxs-lookup"><span data-stu-id="c77db-226">Limit your audience option applies to:</span></span>
* <span data-ttu-id="c77db-227">Включать только подмножество пользователей: все типы кампании (объявления, опросы, отправленные данные, плитки).</span><span class="sxs-lookup"><span data-stu-id="c77db-227">Engage only a subset of users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="c77db-228">Включать только старых пользователей: все типы кампании (объявления, опросы, отправленные данные, плитки).</span><span class="sxs-lookup"><span data-stu-id="c77db-228">Engage only old users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="c77db-229">Включать только новых пользователей: все типы кампании (объявления, опросы, отправленные данные, плитки).</span><span class="sxs-lookup"><span data-stu-id="c77db-229">Engage only new users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="c77db-230">Включать только неактивных пользователей: объявления, опросы, плитки.</span><span class="sxs-lookup"><span data-stu-id="c77db-230">Engage only idle users:    Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="c77db-231">Включать только активных пользователей: все типы кампании (объявления, опросы, отправленные данные, плитки).</span><span class="sxs-lookup"><span data-stu-id="c77db-231">Engage only active users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="c77db-232">Включать только пользователей, которым можно отправить системное push-уведомление: объявления, опросы.</span><span class="sxs-lookup"><span data-stu-id="c77db-232">Engage only users who can be reached using Native Push:     Announcements, Polls</span></span>

## <a name="time-frame"></a><span data-ttu-id="c77db-233">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="c77db-233">Time Frame</span></span>
<span data-ttu-id="c77db-234">В разделе «Интервал времени» можно задать время отправки push-уведомления. Если оставить этот раздел пустым, кампания будет запущена немедленно.</span><span class="sxs-lookup"><span data-stu-id="c77db-234">You can use the Time Frame section to set when the push will be sent or you can leave the time frame blank to start the campaign immediately.</span></span> <span data-ttu-id="c77db-235">Помните, что при использовании часового пояса конечных пользователей кампания может запуститься на день раньше от ожидаемого времени запуска для конечных пользователей в Азии. При этом push-уведомления будут отправляться небольшими пакетами за раз, пока интервал времени во всех часовых поясах в мире не будет соответствовать интервалу времени, заданному для кампании.</span><span class="sxs-lookup"><span data-stu-id="c77db-235">Remember that using the end-users' time zone may start the campaign a day earlier than you expect for your end-users in Asia and send small batches of pushes at a time until all time zones in the world match the time frame set for your campaign.</span></span> <span data-ttu-id="c77db-236">Кроме того, при использовании часового пояса конечных пользователей кампании также могут запускаться с задержкой, так как перед началом отправки push-уведомления кампании требуется запрашивать время с телефона.</span><span class="sxs-lookup"><span data-stu-id="c77db-236">Using the end users' time zone can also cause delays in campaigns since it has to request the time from the phone before starting the push.</span></span>

> [!NOTE]
> <span data-ttu-id="c77db-237">Кампании без даты завершения могут кэшировать push-уведомления локально и отображать их после завершения кампании вручную.</span><span class="sxs-lookup"><span data-stu-id="c77db-237">Campaigns without an end date can cache pushes locally and still display them after you manually complete campaigns.</span></span> <span data-ttu-id="c77db-238">Чтобы избежать этого, указывайте время окончания для кампаний.</span><span class="sxs-lookup"><span data-stu-id="c77db-238">To avoid this behavior, specific an end time for campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="c77db-239">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="c77db-239">See also</span></span>
* <span data-ttu-id="c77db-240">[Начало работы с push-уведомлениями и управление ими для взаимодействия с конечными пользователями][Link 3]</span><span class="sxs-lookup"><span data-stu-id="c77db-240">[Reach - How Tos – Scheduling][Link 3]</span></span> 

![Кампания — охват8][27]

### <a name="settings-apply-to"></a><span data-ttu-id="c77db-242">Возможности применения параметров</span><span class="sxs-lookup"><span data-stu-id="c77db-242">Settings Apply to:</span></span>
* <span data-ttu-id="c77db-243">Интервал времени: объявления, опросы и плитки.</span><span class="sxs-lookup"><span data-stu-id="c77db-243">Time frame:     Announcements, Polls, Tiles</span></span>

## <a name="test"></a><span data-ttu-id="c77db-244">Тест</span><span class="sxs-lookup"><span data-stu-id="c77db-244">Test</span></span>
<span data-ttu-id="c77db-245">С помощью раздела «Тест» перед сохранением кампании можно отправить push-уведомление на тестовое устройство.</span><span class="sxs-lookup"><span data-stu-id="c77db-245">You can use the Test section to send this push to your own test device before saving the campaign.</span></span> <span data-ttu-id="c77db-246">Если вы настроили какие-либо пользовательские языки для кампании, push-уведомление можно проверить для каждого из них.</span><span class="sxs-lookup"><span data-stu-id="c77db-246">If you have configured any custom languages for this campaign, you can test the push in each language.</span></span> <span data-ttu-id="c77db-247">Тестовое устройство можно настроить в разделе «Моя учетная запись».</span><span class="sxs-lookup"><span data-stu-id="c77db-247">You can setup a test device from “My Account”.</span></span>

> [!NOTE]
> <span data-ttu-id="c77db-248">Если вы используете кнопку для тестирования push-уведомлений, данные на стороне сервера не записываются. Они записываются только для реальных кампаний push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="c77db-248">No server side data is logged when you use the button to "test" pushes, data is only logged for real push campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="c77db-249">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="c77db-249">See also</span></span>
* <span data-ttu-id="c77db-250">[Управление профилем учетной записи и тестовыми устройствами][Link 14]</span><span class="sxs-lookup"><span data-stu-id="c77db-250">[UI Documentation - My Account][Link 14]</span></span>

![Кампания — охват9][28]

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
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

