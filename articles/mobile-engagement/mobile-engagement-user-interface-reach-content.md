---
title: "Пользовательский интерфейс Служб мобильного взаимодействия Azure — Содержимое рекламных кампаний"
description: "Информация об управлении уникальным контентом для различных типов кампаний push-уведомлений в Службах мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: add64f06-43c9-475c-8722-51cd00bb844b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3741a43b74af5846e95e42d8a7b533621e780f2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-the-unique-content-of-the-different-types-of-push-notification-campaigns"></a><span data-ttu-id="99ec1-103">Управление уникальным контентом для различных типов кампаний push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="99ec1-103">How to manage the unique content of the different types of push notification campaigns</span></span>
<span data-ttu-id="99ec1-104">С помощью раздела «Содержимое» новой рекламной кампании можно изменять содержимое объявлений, опросов, отправок данных и плиток (только для Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="99ec1-104">You can use the Content section of a new reach campaign to modify the content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="99ec1-105">Параметр «Содержимое» кампаний push-уведомлений зависит от типа кампании.</span><span class="sxs-lookup"><span data-stu-id="99ec1-105">The content setting of Push campaigns is specific to the type of campaign.</span></span> 

### <a name="content-types"></a><span data-ttu-id="99ec1-106">Типы содержимого</span><span class="sxs-lookup"><span data-stu-id="99ec1-106">Content types:</span></span>
* <span data-ttu-id="99ec1-107">Объявления</span><span class="sxs-lookup"><span data-stu-id="99ec1-107">Announcements</span></span>
* <span data-ttu-id="99ec1-108">Опросы</span><span class="sxs-lookup"><span data-stu-id="99ec1-108">Polls</span></span>
* <span data-ttu-id="99ec1-109">Отправки данных</span><span class="sxs-lookup"><span data-stu-id="99ec1-109">Data pushes</span></span>
* <span data-ttu-id="99ec1-110">Плитки (только для Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="99ec1-110">Tiles (Windows Phone Only)</span></span>

## <a name="content-of-announcements"></a><span data-ttu-id="99ec1-111">Содержимое объявлений</span><span class="sxs-lookup"><span data-stu-id="99ec1-111">Content of Announcements</span></span>
 ![Рекламная кампания — Содержимое 1][30] 

### <a name="choose-the-type-of-your-announcement"></a><span data-ttu-id="99ec1-113">Выберите тип объявления:</span><span class="sxs-lookup"><span data-stu-id="99ec1-113">Choose the type of your announcement:</span></span>
* <span data-ttu-id="99ec1-114">Только уведомление. Это простое стандартное уведомление.</span><span class="sxs-lookup"><span data-stu-id="99ec1-114">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="99ec1-115">Это значит, что если пользователь щелкнет его, не отобразится никакое дополнительное представление, а будет только выполнено действие, связанное с ним.</span><span class="sxs-lookup"><span data-stu-id="99ec1-115">Meaning that if a user clicks on it, no additional view will appear, but only the action associated to it will occur.</span></span>
* <span data-ttu-id="99ec1-116">Текстовое объявление. Это уведомление, при появлении которого пользователь может посмотреть текстовое представление.</span><span class="sxs-lookup"><span data-stu-id="99ec1-116">Text announcement: It is a notification that engages the user to have a look at a text view.</span></span>
* <span data-ttu-id="99ec1-117">Веб-объявление. Это уведомление, при появлении которого пользователь может посмотреть веб-представление.</span><span class="sxs-lookup"><span data-stu-id="99ec1-117">Web announcement: It is a notification that engages the user to have a look at a web view.</span></span>

### <a name="see-also"></a><span data-ttu-id="99ec1-118">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="99ec1-118">See also</span></span>
* <span data-ttu-id="99ec1-119">[Начало работы с push-уведомлениями и управление ими для взаимодействия с конечными пользователями][Link 3]</span><span class="sxs-lookup"><span data-stu-id="99ec1-119">[Reach - How Tos - Announcements][Link 3]</span></span> 

### <a name="about-web-view-announcements"></a><span data-ttu-id="99ec1-120">Об объявлениях с веб-представлением</span><span class="sxs-lookup"><span data-stu-id="99ec1-120">About Web View Announcements:</span></span>
<span data-ttu-id="99ec1-121">Шаблон {deviceid} в предоставляемом здесь HTML-коде или коде JavaScript будет автоматически заменен идентификатором устройства, в котором отображается объявление.</span><span class="sxs-lookup"><span data-stu-id="99ec1-121">Occurrences of the pattern "{deviceid}" in the HTML code or JavaScript code you provide here will be automatically replaced by the identifier of the device displaying the announcement.</span></span> <span data-ttu-id="99ec1-122">Это простой способ получить идентификаторы устройств Служб мобильного взаимодействия Azure из внешней веб-службы, размещенной в операционном отделе организации.</span><span class="sxs-lookup"><span data-stu-id="99ec1-122">This is an easy way to retrieve Azure Mobile Engagement device identifiers in an external web service hosted on your back office.</span></span>
<span data-ttu-id="99ec1-123">Если вы хотите создать полноэкранное веб-представление (без предоставляемых кнопок по умолчанию «Действие» и «Выход»), вы можете использовать следующие функции в коде JavaScript объявления веб-представления:</span><span class="sxs-lookup"><span data-stu-id="99ec1-123">If you want to create a full screen web view (without the default Action and Exit buttons we provide) you can use the following functions from your web view announcement's JavaScript code:</span></span> 

* <span data-ttu-id="99ec1-124">выполнение действия объявления: ReachContent.actionContent()</span><span class="sxs-lookup"><span data-stu-id="99ec1-124">perform the announcement action: ReachContent.actionContent()</span></span>
* <span data-ttu-id="99ec1-125">выход из объявления: ReachContent.exitContent()</span><span class="sxs-lookup"><span data-stu-id="99ec1-125">exit from the announcement: ReachContent.exitContent()</span></span>

### <a name="choose-your-action"></a><span data-ttu-id="99ec1-126">Выбор действия</span><span class="sxs-lookup"><span data-stu-id="99ec1-126">Choose your Action:</span></span>
### <a name="about-action-urls"></a><span data-ttu-id="99ec1-127">Об URL-адресах действия</span><span class="sxs-lookup"><span data-stu-id="99ec1-127">About Action URLs:</span></span>
<span data-ttu-id="99ec1-128">Любой URL-адрес, который может интерпретироваться операционной системой целевого устройства, может использоваться как URL-адрес действия.</span><span class="sxs-lookup"><span data-stu-id="99ec1-128">Any URL that can be interpreted by a targeted device's operating system can be used as an action URL.</span></span>
<span data-ttu-id="99ec1-129">В качестве URL-адреса действия также может использоваться любой выделенный URL-адрес, поддерживаемый приложением (например, для перехода пользователя к определенному экрану).</span><span class="sxs-lookup"><span data-stu-id="99ec1-129">Any dedicated URL that your application might support (e.g. to make users jump to a particular screen) can also be used as an action URL.</span></span>
<span data-ttu-id="99ec1-130">Каждый шаблон {deviceid} автоматически заменяется идентификатором устройства, выполняющего действие.</span><span class="sxs-lookup"><span data-stu-id="99ec1-130">Each occurrence of the {deviceid} pattern is automatically replaced by the identifier of the device performing the action.</span></span> <span data-ttu-id="99ec1-131">Таким способом можно легко получить идентификаторы устройств Служб мобильного взаимодействия Azure из внешней веб-службы, размещенной в операционном отделе организации.</span><span class="sxs-lookup"><span data-stu-id="99ec1-131">This can be used to easily retrieve Azure Mobile Engagement device identifiers via an external web service hosted on your back office.</span></span>

* <span data-ttu-id="99ec1-132">**Действия для Android и iOS**</span><span class="sxs-lookup"><span data-stu-id="99ec1-132">**Android + iOS actions**</span></span>
  * <span data-ttu-id="99ec1-133">Открытие веб-страницы</span><span class="sxs-lookup"><span data-stu-id="99ec1-133">Open a web page</span></span>
  * <span data-ttu-id="99ec1-134">http://\[домен_веб_сайта\];</span><span class="sxs-lookup"><span data-stu-id="99ec1-134">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="99ec1-135">например, http://www.azure.com;</span><span class="sxs-lookup"><span data-stu-id="99ec1-135">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="99ec1-136">Отправка сообщения электронной почты</span><span class="sxs-lookup"><span data-stu-id="99ec1-136">Send an e-mail</span></span>
  * <span data-ttu-id="99ec1-137">mailto:\[получатель\]?subject=\[тема\]&body=\[сообщение\];</span><span class="sxs-lookup"><span data-stu-id="99ec1-137">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="99ec1-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="99ec1-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="99ec1-139">Отправка SMS-сообщения</span><span class="sxs-lookup"><span data-stu-id="99ec1-139">Send a SMS</span></span>
  * <span data-ttu-id="99ec1-140">sms:\[номер_телефона\];</span><span class="sxs-lookup"><span data-stu-id="99ec1-140">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="99ec1-141">Пример: sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="99ec1-141">Example:sms:2125551212</span></span>
  * <span data-ttu-id="99ec1-142">Набор номера телефона</span><span class="sxs-lookup"><span data-stu-id="99ec1-142">Dial a phone number</span></span>
  * <span data-ttu-id="99ec1-143">tel:\[номер_телефона\];</span><span class="sxs-lookup"><span data-stu-id="99ec1-143">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="99ec1-144">Пример: tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="99ec1-144">Example:tel:2125551212</span></span>
* <span data-ttu-id="99ec1-145">**Действия только для Android**</span><span class="sxs-lookup"><span data-stu-id="99ec1-145">**Android only actions**</span></span>
  * <span data-ttu-id="99ec1-146">Скачивание приложения из Магазина Google Play</span><span class="sxs-lookup"><span data-stu-id="99ec1-146">Download an application on the Play Store</span></span>
  * <span data-ttu-id="99ec1-147">market://details?id=\[пакет_приложения\];</span><span class="sxs-lookup"><span data-stu-id="99ec1-147">market://details?id=\[app package\]</span></span> 
  * <span data-ttu-id="99ec1-148">Пример: market://details?id=com.microsoft.office.word</span><span class="sxs-lookup"><span data-stu-id="99ec1-148">Example:market://details?id=com.microsoft.office.word</span></span>
  * <span data-ttu-id="99ec1-149">Запуск поиска по географическому расположению</span><span class="sxs-lookup"><span data-stu-id="99ec1-149">Start a geo-localized search</span></span>
  * <span data-ttu-id="99ec1-150">geo:0,0?q=\[запрос_поиска\];</span><span class="sxs-lookup"><span data-stu-id="99ec1-150">geo:0,0?q=\[search query\]</span></span> 
  * <span data-ttu-id="99ec1-151">Пример:geo:0,0?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="99ec1-151">Example:geo:0,0?q=starbucks,paris</span></span>
* <span data-ttu-id="99ec1-152">**Действия только для iOS**</span><span class="sxs-lookup"><span data-stu-id="99ec1-152">**iOS only actions**</span></span>
  * <span data-ttu-id="99ec1-153">Скачивание приложения из магазина App Store</span><span class="sxs-lookup"><span data-stu-id="99ec1-153">Download an application on the App Store</span></span>
  * <span data-ttu-id="99ec1-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span><span class="sxs-lookup"><span data-stu-id="99ec1-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span></span> 
  * <span data-ttu-id="99ec1-155">например, http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8;</span><span class="sxs-lookup"><span data-stu-id="99ec1-155">Example:http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span></span>
  * <span data-ttu-id="99ec1-156">Действия для Windows</span><span class="sxs-lookup"><span data-stu-id="99ec1-156">Windows Actions</span></span>
  * <span data-ttu-id="99ec1-157">Открытие веб-страницы</span><span class="sxs-lookup"><span data-stu-id="99ec1-157">Open a web page</span></span>
  * <span data-ttu-id="99ec1-158">http://\[домен_веб_сайта\];</span><span class="sxs-lookup"><span data-stu-id="99ec1-158">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="99ec1-159">например, http://www.azure.com;</span><span class="sxs-lookup"><span data-stu-id="99ec1-159">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="99ec1-160">Отправка сообщения электронной почты</span><span class="sxs-lookup"><span data-stu-id="99ec1-160">Send an e-mail</span></span>
  * <span data-ttu-id="99ec1-161">mailto:\[получатель\]?subject=\[тема\]&body=\[сообщение\];</span><span class="sxs-lookup"><span data-stu-id="99ec1-161">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="99ec1-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="99ec1-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="99ec1-163">Отправка SMS-сообщения (требуется приложение Skype из Магазина)</span><span class="sxs-lookup"><span data-stu-id="99ec1-163">Send a SMS (Skype Store App required)</span></span>
  * <span data-ttu-id="99ec1-164">sms:\[номер_телефона\];</span><span class="sxs-lookup"><span data-stu-id="99ec1-164">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="99ec1-165">Пример: sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="99ec1-165">Example:sms:2125551212</span></span>
  * <span data-ttu-id="99ec1-166">Набор номера телефона (требуется приложение Skype из Магазина)</span><span class="sxs-lookup"><span data-stu-id="99ec1-166">Dial a phone number (Skype Store App required)</span></span>
  * <span data-ttu-id="99ec1-167">tel:\[номер_телефона\];</span><span class="sxs-lookup"><span data-stu-id="99ec1-167">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="99ec1-168">Пример: tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="99ec1-168">Example:tel:2125551212</span></span>
  * <span data-ttu-id="99ec1-169">Скачивание приложения из Магазина Google Play</span><span class="sxs-lookup"><span data-stu-id="99ec1-169">Download an application on the Play Store</span></span>
  * <span data-ttu-id="99ec1-170">ms-windows-store:PDP?PFN=\[идентификатор_пакета_приложения\];</span><span class="sxs-lookup"><span data-stu-id="99ec1-170">ms-windows-store:PDP?PFN=\[app package ID\]</span></span> 
  * <span data-ttu-id="99ec1-171">Пример: ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span><span class="sxs-lookup"><span data-stu-id="99ec1-171">Example:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span></span>
  * <span data-ttu-id="99ec1-172">Запуск поиска по картам Bing</span><span class="sxs-lookup"><span data-stu-id="99ec1-172">Start a bingmaps search</span></span>
  * <span data-ttu-id="99ec1-173">bingmaps:?q=\[запрос_поиска\];</span><span class="sxs-lookup"><span data-stu-id="99ec1-173">bingmaps:?q=\[search query\]</span></span> 
  * <span data-ttu-id="99ec1-174">Пример:bingmaps:?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="99ec1-174">Example:bingmaps:?q=starbucks,paris</span></span>
  * <span data-ttu-id="99ec1-175">Использование пользовательской схемы</span><span class="sxs-lookup"><span data-stu-id="99ec1-175">Use a custom scheme</span></span>
  * <span data-ttu-id="99ec1-176">\[пользовательская_схема\]://\[параметры_пользовательской_схемы\];</span><span class="sxs-lookup"><span data-stu-id="99ec1-176">\[custom scheme\]://\[custom scheme params\]</span></span> 
  * <span data-ttu-id="99ec1-177">Пример: myCustomProtocol://myCustomParams</span><span class="sxs-lookup"><span data-stu-id="99ec1-177">Example:myCustomProtocol://myCustomParams</span></span>
  * <span data-ttu-id="99ec1-178">Использование данных пакета (требуется приложение из Магазина для расширения для чтения)</span><span class="sxs-lookup"><span data-stu-id="99ec1-178">Use a package data (Store App for extension read required)</span></span>
  * <span data-ttu-id="99ec1-179">\[папка\]\[данные\].\[расширение\];</span><span class="sxs-lookup"><span data-stu-id="99ec1-179">\[folder\]\[data\].\[extension\]</span></span> 
  * <span data-ttu-id="99ec1-180">Пример: myfolderdata.txt</span><span class="sxs-lookup"><span data-stu-id="99ec1-180">Example:myfolderdata.txt</span></span>

### <a name="build-a-tracking-url"></a><span data-ttu-id="99ec1-181">Создание URL-адреса отслеживания</span><span class="sxs-lookup"><span data-stu-id="99ec1-181">Build a Tracking URL:</span></span>
* <span data-ttu-id="99ec1-182">См. указания по созданию URL-адреса отслеживания, который позволит пользователям скачивать одно из ваших приложений, в разделе «Параметры» в <UI Documentation>.</span><span class="sxs-lookup"><span data-stu-id="99ec1-182">See the “Settings” section of the <UI Documentation> for instruction on building a tracking URL that will allow users to download one of your other applications.</span></span>

### <a name="define-the-texts-of-your-announcement"></a><span data-ttu-id="99ec1-183">Определение текста объявления</span><span class="sxs-lookup"><span data-stu-id="99ec1-183">Define the texts of your announcement</span></span>
<span data-ttu-id="99ec1-184">Введите заголовок, содержимое и названия для кнопок вашего объявления.</span><span class="sxs-lookup"><span data-stu-id="99ec1-184">Fill in the title, content, and button texts of your announcement.</span></span> <span data-ttu-id="99ec1-185">Целевую аудиторию будущей кампании можно отслеживать на основе отзывов и предложений по рекламным кампаниям из ответов пользователей на эту кампанию.</span><span class="sxs-lookup"><span data-stu-id="99ec1-185">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="99ec1-186">Кроме того, целевую аудиторию можно отслеживать на основе отзывов и предложений по действию, совершенному с кампанией (отправка push-уведомления, ответ, выполнение действия или выход).</span><span class="sxs-lookup"><span data-stu-id="99ec1-186">Audience targeting can be based on the feedback of whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="99ec1-187">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="99ec1-187">See also</span></span>
* <span data-ttu-id="99ec1-188">[Организация кампаний по рассылке push-уведомлений выбранному подмножеству пользователей с помощью условий таргетинга][Link 28]</span><span class="sxs-lookup"><span data-stu-id="99ec1-188">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-polls"></a><span data-ttu-id="99ec1-189">Содержимое опросов</span><span class="sxs-lookup"><span data-stu-id="99ec1-189">Content of Polls</span></span>
![Рекламная кампания — Содержимое 2][31] 

<span data-ttu-id="99ec1-191">Введите заголовок, описание и названия для кнопок вашего объявления.</span><span class="sxs-lookup"><span data-stu-id="99ec1-191">Fill in the title, description, and button texts of your announcement.</span></span> <span data-ttu-id="99ec1-192">Затем добавьте вопросы и варианты ответов.</span><span class="sxs-lookup"><span data-stu-id="99ec1-192">Then, add questions and choices for the answers to your questions.</span></span>
<span data-ttu-id="99ec1-193">Целевую аудиторию будущей кампании можно отслеживать на основе отзывов и предложений по рекламным кампаниям из ответов пользователей на эту кампанию.</span><span class="sxs-lookup"><span data-stu-id="99ec1-193">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="99ec1-194">Кроме того, целевую аудиторию можно отслеживать на основе действий, совершенных с кампанией (отправка push-уведомления, ответ, выполнение действия или выход).</span><span class="sxs-lookup"><span data-stu-id="99ec1-194">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span> <span data-ttu-id="99ec1-195">Кроме того, целевую аудиторию можно отслеживать на основе отзывов и предложений по ответам на опрос, в которых в качестве критериев используются вопрос и вариант ответа.</span><span class="sxs-lookup"><span data-stu-id="99ec1-195">Audience targeting can also be based on Poll answer feedback, where the question and answer choice are used as criteria.</span></span>

### <a name="see-also"></a><span data-ttu-id="99ec1-196">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="99ec1-196">See also</span></span>
* <span data-ttu-id="99ec1-197">[Организация кампаний по рассылке push-уведомлений выбранному подмножеству пользователей с помощью условий таргетинга][Link 28]</span><span class="sxs-lookup"><span data-stu-id="99ec1-197">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-data-pushes"></a><span data-ttu-id="99ec1-198">Содержимое отправки данных</span><span class="sxs-lookup"><span data-stu-id="99ec1-198">Content of Data Pushes</span></span>
![Рекламная кампания — Содержимое 3][32] 

### <a name="choose-the-type-of-your-data"></a><span data-ttu-id="99ec1-200">Выберите тип данных</span><span class="sxs-lookup"><span data-stu-id="99ec1-200">Choose the type of your data:</span></span>
* <span data-ttu-id="99ec1-201">текст</span><span class="sxs-lookup"><span data-stu-id="99ec1-201">Text</span></span>
* <span data-ttu-id="99ec1-202">Двоичные данные</span><span class="sxs-lookup"><span data-stu-id="99ec1-202">Binary data</span></span>
* <span data-ttu-id="99ec1-203">Данные Base64</span><span class="sxs-lookup"><span data-stu-id="99ec1-203">Base64 data</span></span>

### <a name="define-the-content-of-your-data"></a><span data-ttu-id="99ec1-204">Определение содержимого данных</span><span class="sxs-lookup"><span data-stu-id="99ec1-204">Define the content of your data</span></span>
* <span data-ttu-id="99ec1-205">Если вы выбрали отправку текстовых данных, скопируйте и вставьте текст в поле «Содержимое».</span><span class="sxs-lookup"><span data-stu-id="99ec1-205">If you selected to push text data, copy and paste the text into the "content" box.</span></span>
* <span data-ttu-id="99ec1-206">Если вы выбрали отправку двоичных данных или данных base64, нажмите кнопку «Отправить файл» для отправки файла.</span><span class="sxs-lookup"><span data-stu-id="99ec1-206">If you selected to push either binary or base64 data, use the "upload your file" button to upload your file.</span></span>
* <span data-ttu-id="99ec1-207">Целевую аудиторию будущей кампании можно отслеживать на основе отзывов и предложений по рекламным кампаниям из ответов пользователей на эту кампанию.</span><span class="sxs-lookup"><span data-stu-id="99ec1-207">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="99ec1-208">Кроме того, целевую аудиторию можно отслеживать на основе действий, совершенных с кампанией (отправка push-уведомления, ответ, выполнение действия или выход).</span><span class="sxs-lookup"><span data-stu-id="99ec1-208">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="99ec1-209">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="99ec1-209">See also</span></span>
* <span data-ttu-id="99ec1-210">[Организация кампаний по рассылке push-уведомлений выбранному подмножеству пользователей с помощью условий таргетинга][Link 28]</span><span class="sxs-lookup"><span data-stu-id="99ec1-210">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-tiles-windows-phone-only"></a><span data-ttu-id="99ec1-211">Содержимое плиток (только для Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="99ec1-211">Content of Tiles (Windows Phone only)</span></span>
![Рекламная кампания — Содержимое 4][33]

### <a name="define-the-content-of-your-tile"></a><span data-ttu-id="99ec1-213">Определение содержимого плитки</span><span class="sxs-lookup"><span data-stu-id="99ec1-213">Define the content of your tile</span></span>
<span data-ttu-id="99ec1-214">Полезные данные плитки — это текст, который отображается на плитке приложения в устройствах Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="99ec1-214">The tile payload is the text to be displayed in the tile of your app on Windows Phone devices.</span></span>
<span data-ttu-id="99ec1-215">Push-уведомление плитки представляет собой версию службы push-уведомлений Майкрософт (MPNS) для Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="99ec1-215">A tile push is the Microsoft Push Notification Service (MPNS) version of a native push for Windows Phone.</span></span> <span data-ttu-id="99ec1-216">Push-уведомление плитки — это единственный тип push-уведомлений без ответа, и поэтому аудиторию будущих кампаний нельзя создать на основе результатов кампании push-уведомлений плитки.</span><span class="sxs-lookup"><span data-stu-id="99ec1-216">The tile push type is the only push type that does not have a response and so the audience of future campaigns can't be built on the results of a tile push campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="99ec1-217">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="99ec1-217">See also</span></span>
* <span data-ttu-id="99ec1-218">[Mobile Engagement][Link 4]</span><span class="sxs-lookup"><span data-stu-id="99ec1-218">[API Documentation - Reach API - Native Push][Link 4]</span></span>

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

