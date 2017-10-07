---
title: "aaaAzure Mobile Engagement пользовательского интерфейса: достижения кампании"
description: "Laern как toocreate и управлять ими с помощью Azure Mobile Engagement push-уведомлений кампаний"
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
ms.openlocfilehash: 825e550ace63a34d1a90b10fa976a61eb15a6d04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-push-notification-campaigns"></a><span data-ttu-id="10c81-103">Как toocreate и управлять push-кампаний, уведомления</span><span class="sxs-lookup"><span data-stu-id="10c81-103">How toocreate and manage push notification campaigns</span></span>
<span data-ttu-id="10c81-104">Можно использовать hello Reach раздел пользовательского интерфейса hello toocreate новой кампании Push сложные формулы, указав все сведения hello необходимы toosend push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="10c81-104">You can use hello Reach section of hello UI toocreate a new Push campaign with a complex formula by providing all hello information you need toosend a push notification.</span></span> <span data-ttu-id="10c81-105">Hello параметры кампании Push будут немного отличаться в зависимости от типов кампании hello четырех: извещения, опросы, помещает данные и плитки (только для Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="10c81-105">hello options of a Push campaign vary slightly depending on hello four campaign types: Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span>

### <a name="option-applies-to"></a><span data-ttu-id="10c81-106">Параметр применяется к таким разделам:</span><span class="sxs-lookup"><span data-stu-id="10c81-106">Option Applies to:</span></span>
* <span data-ttu-id="10c81-107">Языки: все типы кампаний (объявления, опросы, отправленные данные и плитки).</span><span class="sxs-lookup"><span data-stu-id="10c81-107">Languages:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="10c81-108">Кампания: все типы кампаний (объявления, опросы, отправленные данные и плитки).</span><span class="sxs-lookup"><span data-stu-id="10c81-108">Campaign:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="10c81-109">Уведомление: объявления, опросы.</span><span class="sxs-lookup"><span data-stu-id="10c81-109">Notification:     Announcements, Polls</span></span>
* <span data-ttu-id="10c81-110">Содержимое: уникально для каждого типа кампании.</span><span class="sxs-lookup"><span data-stu-id="10c81-110">Content:    Unique for each campaign type</span></span>
* <span data-ttu-id="10c81-111">Аудитория: все типы кампаний (объявления, опросы, отправленные данные и плитки).</span><span class="sxs-lookup"><span data-stu-id="10c81-111">Audience:     All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="10c81-112">Интервал времени: объявления, опросы и плитки.</span><span class="sxs-lookup"><span data-stu-id="10c81-112">Time frame:     Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="10c81-113">Тест: все типы кампаний (объявления, опросы, отправленные данные и плитки).</span><span class="sxs-lookup"><span data-stu-id="10c81-113">Test:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>

![Кампания — охват1][20]

## <a name="languages"></a><span data-ttu-id="10c81-115">Языки</span><span class="sxs-lookup"><span data-stu-id="10c81-115">Languages</span></span>
<span data-ttu-id="10c81-116">Можно использовать toosend меню hello раскрывающийся список языков с другой версией вашей toodevices Push, установленных для разных языков toouse.</span><span class="sxs-lookup"><span data-stu-id="10c81-116">You can use hello Languages drop-down menu toosend a different version of your Push toodevices that are set toouse different languages.</span></span> <span data-ttu-id="10c81-117">По умолчанию все устройства получат же Push независимо от того, на каком языке они заданы toouse hello.</span><span class="sxs-lookup"><span data-stu-id="10c81-117">By default, all devices will receive hello same Push regardless of what language they are set toouse.</span></span> <span data-ttu-id="10c81-118">Пользователи с их набор устройств tooa другой язык получат версии языка по умолчанию hello hello Push.</span><span class="sxs-lookup"><span data-stu-id="10c81-118">Users with their device set tooa different language will receive hello Default Language version of hello Push.</span></span> <span data-ttu-id="10c81-119">Многие из параметров кампании push hello разрешить toospecify альтернативное содержимое для каждого из дополнительных языков hello, при выборе.</span><span class="sxs-lookup"><span data-stu-id="10c81-119">Many of hello push campaign options allow you toospecify alternate content for each of hello additional languages you select.</span></span> 

![Кампания — охват2][21]

### <a name="language-differences-apply-to"></a><span data-ttu-id="10c81-121">Различия в языке применяются к таким разделам:</span><span class="sxs-lookup"><span data-stu-id="10c81-121">Language differences apply to:</span></span>
* <span data-ttu-id="10c81-122">Языки: Уникальный языков можно выбрать добавление toohello языка по умолчанию</span><span class="sxs-lookup"><span data-stu-id="10c81-122">Languages:    Unique languages may be selected in addition toohello default language</span></span>
* <span data-ttu-id="10c81-123">Кампания: одинаково для всех языков.</span><span class="sxs-lookup"><span data-stu-id="10c81-123">Campaign:    Same for all languages</span></span>
* <span data-ttu-id="10c81-124">Уведомление: Уникальный для каждого языка, кроме toohello язык по умолчанию</span><span class="sxs-lookup"><span data-stu-id="10c81-124">Notification:    Unique for each language in addition toohello default language</span></span>
* <span data-ttu-id="10c81-125">Содержимое: Уникальный для каждого языка, кроме toohello язык по умолчанию</span><span class="sxs-lookup"><span data-stu-id="10c81-125">Content:    Unique for each language in addition toohello default language</span></span>
* <span data-ttu-id="10c81-126">Аудитория: возможность фильтрации отдельно по языковому критерию.</span><span class="sxs-lookup"><span data-stu-id="10c81-126">Audience:     May be filtered by a separate language criterion</span></span>
* <span data-ttu-id="10c81-127">Интервал времени: одинаково для всех языков.</span><span class="sxs-lookup"><span data-stu-id="10c81-127">Time frame:     Same for all languages</span></span>
* <span data-ttu-id="10c81-128">Теста: Могут быть отправлены языка tooeach одновременно</span><span class="sxs-lookup"><span data-stu-id="10c81-128">Test:    May be sent tooeach language at a time</span></span>

### <a name="supported-languages"></a><span data-ttu-id="10c81-129">Поддерживаемые языки:</span><span class="sxs-lookup"><span data-stu-id="10c81-129">Supported Languages:</span></span>
* <span data-ttu-id="10c81-130">Арабский (ar)</span><span class="sxs-lookup"><span data-stu-id="10c81-130">Arabic (ar)</span></span> 
* <span data-ttu-id="10c81-131">Болгарский (bg)</span><span class="sxs-lookup"><span data-stu-id="10c81-131">Bulgarian (bg)</span></span> 
* <span data-ttu-id="10c81-132">Каталонский (ca)</span><span class="sxs-lookup"><span data-stu-id="10c81-132">Catalan (ca)</span></span> 
* <span data-ttu-id="10c81-133">Китайский (zh)</span><span class="sxs-lookup"><span data-stu-id="10c81-133">Chinese (zh)</span></span> 
* <span data-ttu-id="10c81-134">Хорватский (hr)</span><span class="sxs-lookup"><span data-stu-id="10c81-134">Croatian (hr)</span></span> 
* <span data-ttu-id="10c81-135">Чешский (cs)</span><span class="sxs-lookup"><span data-stu-id="10c81-135">Czech (cs)</span></span> 
* <span data-ttu-id="10c81-136">Датский (da)</span><span class="sxs-lookup"><span data-stu-id="10c81-136">Danish (da)</span></span> 
* <span data-ttu-id="10c81-137">Нидерландский (nl)</span><span class="sxs-lookup"><span data-stu-id="10c81-137">Dutch (nl)</span></span> 
* <span data-ttu-id="10c81-138">Английский (en)</span><span class="sxs-lookup"><span data-stu-id="10c81-138">English (en)</span></span> 
* <span data-ttu-id="10c81-139">Финский (fi)</span><span class="sxs-lookup"><span data-stu-id="10c81-139">Finnish (fi)</span></span> 
* <span data-ttu-id="10c81-140">Французский (fr)</span><span class="sxs-lookup"><span data-stu-id="10c81-140">French (fr)</span></span> 
* <span data-ttu-id="10c81-141">Немецкий (de)</span><span class="sxs-lookup"><span data-stu-id="10c81-141">German (de)</span></span> 
* <span data-ttu-id="10c81-142">Греческий (el)</span><span class="sxs-lookup"><span data-stu-id="10c81-142">Greek (el)</span></span> 
* <span data-ttu-id="10c81-143">Иврит (he)</span><span class="sxs-lookup"><span data-stu-id="10c81-143">Hebrew (he)</span></span> 
* <span data-ttu-id="10c81-144">Хинди (hi)</span><span class="sxs-lookup"><span data-stu-id="10c81-144">Hindi (hi)</span></span> 
* <span data-ttu-id="10c81-145">Венгерский (hu)</span><span class="sxs-lookup"><span data-stu-id="10c81-145">Hungarian (hu)</span></span> 
* <span data-ttu-id="10c81-146">Индонезийский (id)</span><span class="sxs-lookup"><span data-stu-id="10c81-146">Indonesian (id)</span></span> 
* <span data-ttu-id="10c81-147">Итальянский (it)</span><span class="sxs-lookup"><span data-stu-id="10c81-147">Italian (it)</span></span> 
* <span data-ttu-id="10c81-148">Японский (ja)</span><span class="sxs-lookup"><span data-stu-id="10c81-148">Japanese (ja)</span></span> 
* <span data-ttu-id="10c81-149">Корейский (ko)</span><span class="sxs-lookup"><span data-stu-id="10c81-149">Korean (ko)</span></span> 
* <span data-ttu-id="10c81-150">Латышский (lv)</span><span class="sxs-lookup"><span data-stu-id="10c81-150">Latvian (lv)</span></span> 
* <span data-ttu-id="10c81-151">Литовский (lt)</span><span class="sxs-lookup"><span data-stu-id="10c81-151">Lithuanian (lt)</span></span> 
* <span data-ttu-id="10c81-152">Малайский (макроязык) (ms)</span><span class="sxs-lookup"><span data-stu-id="10c81-152">Malay (macrolanguage) (ms)</span></span> 
* <span data-ttu-id="10c81-153">Норвежский (букмол) (nb)</span><span class="sxs-lookup"><span data-stu-id="10c81-153">Norwegian Bokmål (nb)</span></span> 
* <span data-ttu-id="10c81-154">Польский (pl)</span><span class="sxs-lookup"><span data-stu-id="10c81-154">Polish (pl)</span></span> 
* <span data-ttu-id="10c81-155">Португальский (pt)</span><span class="sxs-lookup"><span data-stu-id="10c81-155">Portuguese (pt)</span></span> 
* <span data-ttu-id="10c81-156">Румынский (ro)</span><span class="sxs-lookup"><span data-stu-id="10c81-156">Romanian (ro)</span></span> 
* <span data-ttu-id="10c81-157">Русский (ru)</span><span class="sxs-lookup"><span data-stu-id="10c81-157">Russian (ru)</span></span> 
* <span data-ttu-id="10c81-158">Сербский (sr)</span><span class="sxs-lookup"><span data-stu-id="10c81-158">Serbian (sr)</span></span> 
* <span data-ttu-id="10c81-159">Словацкий (sk)</span><span class="sxs-lookup"><span data-stu-id="10c81-159">Slovak (sk)</span></span> 
* <span data-ttu-id="10c81-160">Словенский (sl)</span><span class="sxs-lookup"><span data-stu-id="10c81-160">Slovenian (sl)</span></span> 
* <span data-ttu-id="10c81-161">Испанский (es)</span><span class="sxs-lookup"><span data-stu-id="10c81-161">Spanish (es)</span></span> 
* <span data-ttu-id="10c81-162">Шведский (sv)</span><span class="sxs-lookup"><span data-stu-id="10c81-162">Swedish (sv)</span></span> 
* <span data-ttu-id="10c81-163">Тагальский (tl)</span><span class="sxs-lookup"><span data-stu-id="10c81-163">Tagalog (tl)</span></span> 
* <span data-ttu-id="10c81-164">Тайский (th)</span><span class="sxs-lookup"><span data-stu-id="10c81-164">Thai (th)</span></span> 
* <span data-ttu-id="10c81-165">Турецкий (tr)</span><span class="sxs-lookup"><span data-stu-id="10c81-165">Turkish (tr)</span></span> 
* <span data-ttu-id="10c81-166">Украинский (uk)</span><span class="sxs-lookup"><span data-stu-id="10c81-166">Ukrainian (uk)</span></span> 
* <span data-ttu-id="10c81-167">Вьетнамский (vi)</span><span class="sxs-lookup"><span data-stu-id="10c81-167">Vietnamese (vi)</span></span> 

## <a name="campaign"></a><span data-ttu-id="10c81-168">Кампания</span><span class="sxs-lookup"><span data-stu-id="10c81-168">Campaign</span></span>
<span data-ttu-id="10c81-169">Можно использовать hello кампании tooset hello имя раздела и категория кампании также так, будто планирование tooignore hello аудитории раздел кампании Push-уведомлений и вместо отправки уведомления через hello Reach API (и некоторые элементы с низким уровнем hello Push-API).</span><span class="sxs-lookup"><span data-stu-id="10c81-169">You can use hello Campaign section tooset hello name and category of your campaign as well as if you plan tooignore hello audience section of a Push campaign and send this campaign via hello Reach API (and some elements with hello low level Push API) instead.</span></span> <span data-ttu-id="10c81-170">Категории можно использовать с настраиваемое уведомление шаблон toocontrol в приложении уведомления на основе предварительно определенных параметров.</span><span class="sxs-lookup"><span data-stu-id="10c81-170">Categories can be used with a custom notification template toocontrol in-app notifications based on predefined settings.</span></span> <span data-ttu-id="10c81-171">Можно получить список существующих «категорий» через hello Reach API.</span><span class="sxs-lookup"><span data-stu-id="10c81-171">You can get a list of your existing “Categories” via hello Reach API.</span></span>

> [!WARNING]
> <span data-ttu-id="10c81-172">Если указывается параметр hello «Игнорировать аудиторию push будут отправляться toousers через hello API» в разделе «Кампании» hello кампании Reach, не будет автоматически отправлять кампании hello, вам потребуется toosend его вручную через hello Reach API.</span><span class="sxs-lookup"><span data-stu-id="10c81-172">If you use hello "Ignore Audience, push will be sent toousers via hello API" option in hello "Campaign" section of a Reach campaign, hello campaign will NOT automatically send, you will need toosend it manually via hello Reach API.</span></span>

![Кампания — охват3][22]

### <a name="option-applies-to"></a><span data-ttu-id="10c81-174">Параметр применяется к таким разделам:</span><span class="sxs-lookup"><span data-stu-id="10c81-174">Option Applies to:</span></span>
* <span data-ttu-id="10c81-175">Имя: все кампании.</span><span class="sxs-lookup"><span data-stu-id="10c81-175">Name:    All</span></span>
* <span data-ttu-id="10c81-176">Категория: объявления, опросы.</span><span class="sxs-lookup"><span data-stu-id="10c81-176">Category:    Announcements, Polls</span></span>
* <span data-ttu-id="10c81-177">Игнорировать аудиторию Push-уведомления будут отправляться toousers через hello API: все</span><span class="sxs-lookup"><span data-stu-id="10c81-177">Ignore Audience, push will be sent toousers via hello API:    All</span></span>

## <a name="notification"></a><span data-ttu-id="10c81-178">Уведомление</span><span class="sxs-lookup"><span data-stu-id="10c81-178">Notification</span></span>
<span data-ttu-id="10c81-179">Можно использовать основные параметры раздела уведомления tooset hello о принудительной: hello заголовок hello принудительной приветственное сообщение, изображение в приложении, или если это маловажные.</span><span class="sxs-lookup"><span data-stu-id="10c81-179">You can use hello Notification section tooset basic settings for your push including: hello title of hello Push, hello message, an in-app image, or if it is dismissible.</span></span> <span data-ttu-id="10c81-180">Многие параметры уведомления, определенных toohello платформы устройства.</span><span class="sxs-lookup"><span data-stu-id="10c81-180">Many notification settings are specific toohello platform of your device.</span></span> <span data-ttu-id="10c81-181">Вы можете выбрать способ отправки push-уведомлений: в приложении, за пределами приложения или оба варианта.</span><span class="sxs-lookup"><span data-stu-id="10c81-181">You can select whether your push will be sent "in app" or "out of app" or both.</span></span> <span data-ttu-id="10c81-182">(Помните, что пользователи могут «включить» или «отказаться» «за пределы приложение» помещает hello операционной системы уровня на устройствах и Azure Mobile Engagement не будет иметь возможности toooverride этот параметр.</span><span class="sxs-lookup"><span data-stu-id="10c81-182">(Remember that users can "opt-in" or "opt-out" of "out of app" Pushes at hello Operating System level on their devices, and Azure Mobile Engagement will not be able toooverride this setting.</span></span> <span data-ttu-id="10c81-183">Также следует помните, что hello Reach API обрабатывает «приложение» и помещает «out приложения».</span><span class="sxs-lookup"><span data-stu-id="10c81-183">Also remember that hello Reach API handles "in app" and "out of app" Pushes.</span></span> <span data-ttu-id="10c81-184">Hello Push-API может быть используется toohandle «out приложения» помещает слишком.) Push-уведомлений может быть настроен с изображения или HTML-содержимое, включая прямые ссылки для связывания вне приложения или tooanother местоположения в приложение (Android SDK 2.1.0 или более поздней версии намерения категории требуется).</span><span class="sxs-lookup"><span data-stu-id="10c81-184">hello Push API can be used toohandle "out of app" pushes too.) Pushes can be customized with pictures or HTML content, including deep links for linking outside of your App or tooanother location in your App (Android SDK 2.1.0 or later intent categories required).</span></span> <span data-ttu-id="10c81-185">Можно изменить значок или операций ввода-вывода эмблемы hello и отправки текста или веб-содержимого (всплывающее окно с html, URL-адрес ссылки tooanother расположение содержимого внутри или за пределами приложение hello).</span><span class="sxs-lookup"><span data-stu-id="10c81-185">You can change hello icon or iOS badge, and send either text or web content (a popup with html content, URL link tooanother location either inside or outside of hello app).</span></span> <span data-ttu-id="10c81-186">Можно также включить подачу сигнала устройств Android или компакт-дисков с hello Push.</span><span class="sxs-lookup"><span data-stu-id="10c81-186">You can also make Android devices ring or vibrate with hello Push.</span></span> <span data-ttu-id="10c81-187">(Помните, что вам будет необходимо hello правильные разрешения SDK в Android tooring файл манифеста или управлять вибрацией устройства). Сейчас отраслевой стандарт для размера больших изображений устройств с ОС Android отсутствует, так как размеры экрана в каждом устройстве отличаются. Однако изображения размером 400x100 отображаются на экранах практически любого размера.</span><span class="sxs-lookup"><span data-stu-id="10c81-187">(Remember that you will need hello correct SDK permissions in your Android manifest file tooring or vibrate a device.) There is currently no industry standard for Android "Big Picture" sizes, since screen sizes are different on every device, but 400x100 pictures work on almost any screen size.</span></span>

### <a name="delivery-types"></a><span data-ttu-id="10c81-188">Типы доставки</span><span class="sxs-lookup"><span data-stu-id="10c81-188">Delivery Types:</span></span>
* <span data-ttu-id="10c81-189">Только вне приложения: hello уведомление будет выполнена после hello не используются приложения hello.</span><span class="sxs-lookup"><span data-stu-id="10c81-189">Out of app only: hello notification will be delivered when hello user does not use hello application.</span></span>
* <span data-ttu-id="10c81-190">Hello вне только уведомление приложения требуется сертификат из Apple или Google (сертификатов APNS или GCM).</span><span class="sxs-lookup"><span data-stu-id="10c81-190">hello out of app only notification requires a certificate from Apple or Google (APNS or GCM certificate).</span></span>
* <span data-ttu-id="10c81-191">В приложении только: hello уведомление отображается, только когда работает приложение hello.</span><span class="sxs-lookup"><span data-stu-id="10c81-191">In-app only: hello notification appears only when hello application is running.</span></span>
* <span data-ttu-id="10c81-192">hello Capptain доставки tooreach hello пользователь системы использует уведомление о Hello.</span><span class="sxs-lookup"><span data-stu-id="10c81-192">hello notification uses hello Capptain delivery system tooreach hello user.</span></span> <span data-ttu-id="10c81-193">Можно полностью настроить hello макета или отображаемым передачу.</span><span class="sxs-lookup"><span data-stu-id="10c81-193">You can fully customize hello visual layout/display of your push.</span></span>
* <span data-ttu-id="10c81-194">В любое время: Этот параметр обеспечивает отправки оповещения, которые либо hello приложение или нет.</span><span class="sxs-lookup"><span data-stu-id="10c81-194">Anytime: This option ensures that you send a notification either hello application is running or not.</span></span>

![Кампания — охват4][23]

### <a name="option-applies-to"></a><span data-ttu-id="10c81-196">Параметр применяется к таким разделам:</span><span class="sxs-lookup"><span data-stu-id="10c81-196">Option Applies to:</span></span>
* <span data-ttu-id="10c81-197">Уведомление: объявления, опросы.</span><span class="sxs-lookup"><span data-stu-id="10c81-197">Notification:     Announcements, Polls</span></span>

## <a name="content"></a><span data-ttu-id="10c81-198">Содержимое</span><span class="sxs-lookup"><span data-stu-id="10c81-198">Content</span></span>
<span data-ttu-id="10c81-199">Можно использовать hello раздела содержимого toomodify hello содержимое вашего объявления, опросы, помещает данные и плитки (только для Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="10c81-199">You can use hello Content section toomodify hello content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="10c81-200">приветствия содержимого Push-кампаний равен toohello определенного типа кампании.</span><span class="sxs-lookup"><span data-stu-id="10c81-200">hello Content setting of Push campaigns is specific toohello type of campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="10c81-201">См. также</span><span class="sxs-lookup"><span data-stu-id="10c81-201">See also</span></span>
* <span data-ttu-id="10c81-202">[Управление уникальным контентом для различных типов кампаний push-уведомлений][Link 29]</span><span class="sxs-lookup"><span data-stu-id="10c81-202">[UI Documentation - Reach - Push Content][Link 29]</span></span>

![Кампания — охват5][24]

## <a name="audience"></a><span data-ttu-id="10c81-204">Аудитория</span><span class="sxs-lookup"><span data-stu-id="10c81-204">Audience</span></span>
<span data-ttu-id="10c81-205">Можно использовать toodefine раздел аудитории hello стандартный список элементов toolimit кампании или ограничения кампании на основе настроенных условий.</span><span class="sxs-lookup"><span data-stu-id="10c81-205">You can use hello Audience section toodefine a standard list of items toolimit your campaign or limits your campaign based on customized criteria.</span></span> <span data-ttu-id="10c81-206">стандартный набор параметров tooLimit Hello аудитории можно toopush tooeither нового или старого или системное Push-уведомление пользователей только.</span><span class="sxs-lookup"><span data-stu-id="10c81-206">hello standard set of options tooLimit your Audience allows you toopush tooeither new or old users or native push users only.</span></span> <span data-ttu-id="10c81-207">Можно также задать квоты toolimit hello ряд пользователи, получающие принудительной hello.</span><span class="sxs-lookup"><span data-stu-id="10c81-207">You can also set a quota toolimit hello number of users who receive hello push.</span></span> <span data-ttu-id="10c81-208">Можно вручную изменить выражение hello обеспечения кампанию отфильтрованные tooinclude одного или нескольких пользователей tootarget критерий.</span><span class="sxs-lookup"><span data-stu-id="10c81-208">You can manually Edit hello expression for how your campaign is filtered tooinclude one or more criterion tootarget users.</span></span> <span data-ttu-id="10c81-209">Выражение, определяющее связь между критериями, определяющими целевую аудиторию, можно вводить вручную.</span><span class="sxs-lookup"><span data-stu-id="10c81-209">You can manually type an audience expression.</span></span> <span data-ttu-id="10c81-210">Такое выражение, необходимо явно определить hello отношения между условиями.</span><span class="sxs-lookup"><span data-stu-id="10c81-210">Such an expression must explicitly define hello relation between criteria.</span></span> <span data-ttu-id="10c81-211">Критерий описывается идентификатором, который должен начинаться с заглавной буквы и не должен содержать пробелы.</span><span class="sxs-lookup"><span data-stu-id="10c81-211">A criterion is described by an identifier that must start with a capital letter and cannot contain spaces.</span></span> <span data-ttu-id="10c81-212">Hello отношения между условиями hello можно описать с помощью «и», «или» операторы «not» а "(",")».</span><span class="sxs-lookup"><span data-stu-id="10c81-212">hello relation between hello criteria can be described using 'and', 'or', 'not' operators as well as '(', ')'.</span></span> <span data-ttu-id="10c81-213">Пример: «критерий1 or (критерий1 and not критерий2)».</span><span class="sxs-lookup"><span data-stu-id="10c81-213">Example: "Criterion1 or (Criterion1 and not Criterion2)".</span></span>

> [!NOTE]
> <span data-ttu-id="10c81-214">С большой аудитории, включенных в кампаниях, стороны сервера hello сканирование может выполняться медленно, особенно в том случае, если вы попробуете toostart несколько кампаний на hello же время.</span><span class="sxs-lookup"><span data-stu-id="10c81-214">With a large audience included in campaigns, hello server side targeting scan can be slow, especially if you attempt toostart multiple campaigns at hello same time.</span></span>

* <span data-ttu-id="10c81-215">По возможности запускайте только одну кампанию за раз.</span><span class="sxs-lookup"><span data-stu-id="10c81-215">If possible, only start one campaign at a time.</span></span>
* <span data-ttu-id="10c81-216">В более hello начала только четыре кампании за раз.</span><span class="sxs-lookup"><span data-stu-id="10c81-216">At hello most, only start four campaigns at a time.</span></span>
* <span data-ttu-id="10c81-217">Только активных пользователей tooyour Push (флажок «задействовать только тех пользователей, которые можно получить с помощью системных Push-уведомлений» и «Задействовать только активных пользователей»), чтобы только пользователей, которые по-прежнему установлено приложение hello и использовать его потребуется toobe сканирования.</span><span class="sxs-lookup"><span data-stu-id="10c81-217">Push only tooyour active users (checkbox "Engage only users who can be reached using Native Push" and "Engage only active users") so that only your users who still have hello app installed and use it will need toobe scanned.</span></span>
  <span data-ttu-id="10c81-218">После определения аудитории можно использовать hello имитации toofind кнопки, сколько пользователи получат это Push.</span><span class="sxs-lookup"><span data-stu-id="10c81-218">Once your audience is defined, you can use hello simulate button toofind out how many users will receive this Push.</span></span> <span data-ttu-id="10c81-219">Вычисляет hello числа известных пользователей, потенциально целевая аудитория (является приблизительным, в зависимости от случайной выборки пользователей).</span><span class="sxs-lookup"><span data-stu-id="10c81-219">This will compute hello number of known users potentially targeted by this audience (this is an estimate based on a random sample of users).</span></span> <span data-ttu-id="10c81-220">Имейте в виду, что пользователи, удалившие приложение hello также являются частью этой аудитории, но не может быть достигнута.</span><span class="sxs-lookup"><span data-stu-id="10c81-220">Be aware that users who have uninstalled hello application are also part of this audience, but cannot be reached.</span></span>

### <a name="see-also"></a><span data-ttu-id="10c81-221">См. также</span><span class="sxs-lookup"><span data-stu-id="10c81-221">See also</span></span>
* <span data-ttu-id="10c81-222">[Организация кампаний по рассылке push-уведомлений выбранному подмножеству пользователей с помощью условий таргетинга][Link 28]</span><span class="sxs-lookup"><span data-stu-id="10c81-222">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

![Кампания — охват6][25]

### <a name="edit-expression"></a><span data-ttu-id="10c81-224">Выражение для изменения</span><span class="sxs-lookup"><span data-stu-id="10c81-224">Edit expression</span></span>
![Кампания — охват7][26]

### <a name="limit-your-audience-option-applies-to"></a><span data-ttu-id="10c81-226">Параметр «Ограничить аудиторию» применяется к таким параметрам:</span><span class="sxs-lookup"><span data-stu-id="10c81-226">Limit your audience option applies to:</span></span>
* <span data-ttu-id="10c81-227">Включать только подмножество пользователей: все типы кампании (объявления, опросы, отправленные данные, плитки).</span><span class="sxs-lookup"><span data-stu-id="10c81-227">Engage only a subset of users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="10c81-228">Включать только старых пользователей: все типы кампании (объявления, опросы, отправленные данные, плитки).</span><span class="sxs-lookup"><span data-stu-id="10c81-228">Engage only old users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="10c81-229">Включать только новых пользователей: все типы кампании (объявления, опросы, отправленные данные, плитки).</span><span class="sxs-lookup"><span data-stu-id="10c81-229">Engage only new users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="10c81-230">Включать только неактивных пользователей: объявления, опросы, плитки.</span><span class="sxs-lookup"><span data-stu-id="10c81-230">Engage only idle users:    Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="10c81-231">Включать только активных пользователей: все типы кампании (объявления, опросы, отправленные данные, плитки).</span><span class="sxs-lookup"><span data-stu-id="10c81-231">Engage only active users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="10c81-232">Включать только пользователей, которым можно отправить системное push-уведомление: объявления, опросы.</span><span class="sxs-lookup"><span data-stu-id="10c81-232">Engage only users who can be reached using Native Push:     Announcements, Polls</span></span>

## <a name="time-frame"></a><span data-ttu-id="10c81-233">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="10c81-233">Time Frame</span></span>
<span data-ttu-id="10c81-234">Можно использовать раздел tooset hello промежуток времени, при hello Push-уведомление будет отправлено или можно оставить пустым toostart hello hello промежуток времени кампании немедленно.</span><span class="sxs-lookup"><span data-stu-id="10c81-234">You can use hello Time Frame section tooset when hello push will be sent or you can leave hello time frame blank toostart hello campaign immediately.</span></span> <span data-ttu-id="10c81-235">Помните, что часовой пояс hello конечных пользователей с помощью может запускать кампании hello дня раньше, чем ожидается, что для конечных пользователей в Азии и отправлять небольших пакетов во время, пока не задан всех часовых поясов в hello world соответствия hello временные рамки для кампании Push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="10c81-235">Remember that using hello end-users' time zone may start hello campaign a day earlier than you expect for your end-users in Asia and send small batches of pushes at a time until all time zones in hello world match hello time frame set for your campaign.</span></span> <span data-ttu-id="10c81-236">Часовой пояс hello конечных пользователей с помощью также может вызывать задержки в кампаниях, так как он содержит время hello toorequest с телефона hello перед запуском принудительной hello.</span><span class="sxs-lookup"><span data-stu-id="10c81-236">Using hello end users' time zone can also cause delays in campaigns since it has toorequest hello time from hello phone before starting hello push.</span></span>

> [!NOTE]
> <span data-ttu-id="10c81-237">Кампании без даты завершения могут кэшировать push-уведомления локально и отображать их после завершения кампании вручную.</span><span class="sxs-lookup"><span data-stu-id="10c81-237">Campaigns without an end date can cache pushes locally and still display them after you manually complete campaigns.</span></span> <span data-ttu-id="10c81-238">tooavoid этого поведения, определенного времени окончания кампании.</span><span class="sxs-lookup"><span data-stu-id="10c81-238">tooavoid this behavior, specific an end time for campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="10c81-239">См. также</span><span class="sxs-lookup"><span data-stu-id="10c81-239">See also</span></span>
* <span data-ttu-id="10c81-240">[Начало работы с push-уведомлениями и управление ими для взаимодействия с конечными пользователями][Link 3]</span><span class="sxs-lookup"><span data-stu-id="10c81-240">[Reach - How Tos – Scheduling][Link 3]</span></span> 

![Кампания — охват8][27]

### <a name="settings-apply-to"></a><span data-ttu-id="10c81-242">Возможности применения параметров</span><span class="sxs-lookup"><span data-stu-id="10c81-242">Settings Apply to:</span></span>
* <span data-ttu-id="10c81-243">Интервал времени: объявления, опросы и плитки.</span><span class="sxs-lookup"><span data-stu-id="10c81-243">Time frame:     Announcements, Polls, Tiles</span></span>

## <a name="test"></a><span data-ttu-id="10c81-244">Тест</span><span class="sxs-lookup"><span data-stu-id="10c81-244">Test</span></span>
<span data-ttu-id="10c81-245">Можно использовать раздел toosend hello теста это устройство собственных тестов tooyour push, перед сохранением hello кампании.</span><span class="sxs-lookup"><span data-stu-id="10c81-245">You can use hello Test section toosend this push tooyour own test device before saving hello campaign.</span></span> <span data-ttu-id="10c81-246">После настройки все пользовательские языки для кампании можно проверить hello push на этих языках.</span><span class="sxs-lookup"><span data-stu-id="10c81-246">If you have configured any custom languages for this campaign, you can test hello push in each language.</span></span> <span data-ttu-id="10c81-247">Тестовое устройство можно настроить в разделе «Моя учетная запись».</span><span class="sxs-lookup"><span data-stu-id="10c81-247">You can setup a test device from “My Account”.</span></span>

> [!NOTE]
> <span data-ttu-id="10c81-248">Ни одна сторона сервера данных регистрируется при использовании кнопки hello слишком «test» помещает, регистрируются только данные для реальных push-кампаний.</span><span class="sxs-lookup"><span data-stu-id="10c81-248">No server side data is logged when you use hello button too"test" pushes, data is only logged for real push campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="10c81-249">См. также</span><span class="sxs-lookup"><span data-stu-id="10c81-249">See also</span></span>
* <span data-ttu-id="10c81-250">[Управление профилем учетной записи и тестовыми устройствами][Link 14]</span><span class="sxs-lookup"><span data-stu-id="10c81-250">[UI Documentation - My Account][Link 14]</span></span>

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

