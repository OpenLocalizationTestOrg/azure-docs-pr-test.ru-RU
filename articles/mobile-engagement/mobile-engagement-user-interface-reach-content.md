---
title: "Достичь содержимого aaaAzure Mobile Engagement пользовательского интерфейса:"
description: "Узнайте, как уникальный содержимое toomanage hello hello различных типов push-уведомление кампании в Azure Mobile Engagement"
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
ms.openlocfilehash: de389eb4368d986ef00135036c26e26a2464663e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-hello-unique-content-of-hello-different-types-of-push-notification-campaigns"></a><span data-ttu-id="a5530-103">Как toomanage hello уникальные материалы hello различные типы уведомлений push-кампаний</span><span class="sxs-lookup"><span data-stu-id="a5530-103">How toomanage hello unique content of hello different types of push notification campaigns</span></span>
<span data-ttu-id="a5530-104">Можно использовать раздел содержимого hello содержимого hello объявлений, опросы, помещает данные, и плитки (только для Windows Phone) в новой кампании reach toomodify.</span><span class="sxs-lookup"><span data-stu-id="a5530-104">You can use hello Content section of a new reach campaign toomodify hello content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="a5530-105">приветствия содержимого Push-кампаний равен toohello определенного типа кампании.</span><span class="sxs-lookup"><span data-stu-id="a5530-105">hello content setting of Push campaigns is specific toohello type of campaign.</span></span> 

### <a name="content-types"></a><span data-ttu-id="a5530-106">Типы содержимого</span><span class="sxs-lookup"><span data-stu-id="a5530-106">Content types:</span></span>
* <span data-ttu-id="a5530-107">Объявления</span><span class="sxs-lookup"><span data-stu-id="a5530-107">Announcements</span></span>
* <span data-ttu-id="a5530-108">Опросы</span><span class="sxs-lookup"><span data-stu-id="a5530-108">Polls</span></span>
* <span data-ttu-id="a5530-109">Отправки данных</span><span class="sxs-lookup"><span data-stu-id="a5530-109">Data pushes</span></span>
* <span data-ttu-id="a5530-110">Плитки (только для Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="a5530-110">Tiles (Windows Phone Only)</span></span>

## <a name="content-of-announcements"></a><span data-ttu-id="a5530-111">Содержимое объявлений</span><span class="sxs-lookup"><span data-stu-id="a5530-111">Content of Announcements</span></span>
 ![Рекламная кампания — Содержимое 1][30] 

### <a name="choose-hello-type-of-your-announcement"></a><span data-ttu-id="a5530-113">Выберите тип объявления hello.</span><span class="sxs-lookup"><span data-stu-id="a5530-113">Choose hello type of your announcement:</span></span>
* <span data-ttu-id="a5530-114">Только уведомление. Это простое стандартное уведомление.</span><span class="sxs-lookup"><span data-stu-id="a5530-114">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="a5530-115">Это означает, что если пользователь щелкает, без дополнительного представления будут отображаться, но только действие hello связанные tooit будут происходить.</span><span class="sxs-lookup"><span data-stu-id="a5530-115">Meaning that if a user clicks on it, no additional view will appear, but only hello action associated tooit will occur.</span></span>
* <span data-ttu-id="a5530-116">Текст объявления: это уведомление, которое использует toohave пользователя hello взглянуть на вид текста.</span><span class="sxs-lookup"><span data-stu-id="a5530-116">Text announcement: It is a notification that engages hello user toohave a look at a text view.</span></span>
* <span data-ttu-id="a5530-117">Объявление Web: это уведомление, которое использует toohave пользователя hello взглянуть на веб-представление.</span><span class="sxs-lookup"><span data-stu-id="a5530-117">Web announcement: It is a notification that engages hello user toohave a look at a web view.</span></span>

### <a name="see-also"></a><span data-ttu-id="a5530-118">См. также</span><span class="sxs-lookup"><span data-stu-id="a5530-118">See also</span></span>
* <span data-ttu-id="a5530-119">[Начало работы с push-уведомлениями и управление ими для взаимодействия с конечными пользователями][Link 3]</span><span class="sxs-lookup"><span data-stu-id="a5530-119">[Reach - How Tos - Announcements][Link 3]</span></span> 

### <a name="about-web-view-announcements"></a><span data-ttu-id="a5530-120">Об объявлениях с веб-представлением</span><span class="sxs-lookup"><span data-stu-id="a5530-120">About Web View Announcements:</span></span>
<span data-ttu-id="a5530-121">Вхождения образца hello «{deviceid}» в hello HTML-код или код JavaScript, здесь будет автоматически заменен идентификатором hello hello устройства отображения объявления «hello».</span><span class="sxs-lookup"><span data-stu-id="a5530-121">Occurrences of hello pattern "{deviceid}" in hello HTML code or JavaScript code you provide here will be automatically replaced by hello identifier of hello device displaying hello announcement.</span></span> <span data-ttu-id="a5530-122">Это простой способ tooretrieve Azure идентификаторы устройства Mobile Engagement во внешнем веб-службы, размещенной в операционном отделе.</span><span class="sxs-lookup"><span data-stu-id="a5530-122">This is an easy way tooretrieve Azure Mobile Engagement device identifiers in an external web service hosted on your back office.</span></span>
<span data-ttu-id="a5530-123">Если требуется, чтобы toocreate полного экрана веб-представление (без hello по умолчанию действие выхода кнопок и мы предоставляем) можно использовать hello следующие функции из кода JavaScript в объявлении веб-представление:</span><span class="sxs-lookup"><span data-stu-id="a5530-123">If you want toocreate a full screen web view (without hello default Action and Exit buttons we provide) you can use hello following functions from your web view announcement's JavaScript code:</span></span> 

* <span data-ttu-id="a5530-124">выполнить действие объявления hello: ReachContent.actionContent()</span><span class="sxs-lookup"><span data-stu-id="a5530-124">perform hello announcement action: ReachContent.actionContent()</span></span>
* <span data-ttu-id="a5530-125">выйти из объявления «hello»: ReachContent.exitContent()</span><span class="sxs-lookup"><span data-stu-id="a5530-125">exit from hello announcement: ReachContent.exitContent()</span></span>

### <a name="choose-your-action"></a><span data-ttu-id="a5530-126">Выбор действия</span><span class="sxs-lookup"><span data-stu-id="a5530-126">Choose your Action:</span></span>
### <a name="about-action-urls"></a><span data-ttu-id="a5530-127">Об URL-адресах действия</span><span class="sxs-lookup"><span data-stu-id="a5530-127">About Action URLs:</span></span>
<span data-ttu-id="a5530-128">Любой URL-адрес, который может интерпретироваться операционной системой целевого устройства, может использоваться как URL-адрес действия.</span><span class="sxs-lookup"><span data-stu-id="a5530-128">Any URL that can be interpreted by a targeted device's operating system can be used as an action URL.</span></span>
<span data-ttu-id="a5530-129">Любой выделенный URL-адрес, приложение может поддержки (например toomake пользователям переходить tooa экран) можно также использовать как URL-адрес действия.</span><span class="sxs-lookup"><span data-stu-id="a5530-129">Any dedicated URL that your application might support (e.g. toomake users jump tooa particular screen) can also be used as an action URL.</span></span>
<span data-ttu-id="a5530-130">Идентификатор hello hello устройства, выполняющего действие hello автоматически заменяется найденной hello {deviceid}.</span><span class="sxs-lookup"><span data-stu-id="a5530-130">Each occurrence of hello {deviceid} pattern is automatically replaced by hello identifier of hello device performing hello action.</span></span> <span data-ttu-id="a5530-131">Это может быть используется tooeasily получить идентификаторы устройства Azure Mobile Engagement через внешнюю веб-службу, размещенной в операционном отделе.</span><span class="sxs-lookup"><span data-stu-id="a5530-131">This can be used tooeasily retrieve Azure Mobile Engagement device identifiers via an external web service hosted on your back office.</span></span>

* <span data-ttu-id="a5530-132">**Действия для Android и iOS**</span><span class="sxs-lookup"><span data-stu-id="a5530-132">**Android + iOS actions**</span></span>
  * <span data-ttu-id="a5530-133">Открытие веб-страницы</span><span class="sxs-lookup"><span data-stu-id="a5530-133">Open a web page</span></span>
  * <span data-ttu-id="a5530-134">http://\[домен_веб_сайта\];</span><span class="sxs-lookup"><span data-stu-id="a5530-134">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="a5530-135">например, http://www.azure.com;</span><span class="sxs-lookup"><span data-stu-id="a5530-135">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="a5530-136">Отправка сообщения электронной почты</span><span class="sxs-lookup"><span data-stu-id="a5530-136">Send an e-mail</span></span>
  * <span data-ttu-id="a5530-137">mailto:\[получатель\]?subject=\[тема\]&body=\[сообщение\];</span><span class="sxs-lookup"><span data-stu-id="a5530-137">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="a5530-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="a5530-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="a5530-139">Отправка SMS-сообщения</span><span class="sxs-lookup"><span data-stu-id="a5530-139">Send a SMS</span></span>
  * <span data-ttu-id="a5530-140">sms:\[номер_телефона\];</span><span class="sxs-lookup"><span data-stu-id="a5530-140">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="a5530-141">Пример: sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="a5530-141">Example:sms:2125551212</span></span>
  * <span data-ttu-id="a5530-142">Набор номера телефона</span><span class="sxs-lookup"><span data-stu-id="a5530-142">Dial a phone number</span></span>
  * <span data-ttu-id="a5530-143">tel:\[номер_телефона\];</span><span class="sxs-lookup"><span data-stu-id="a5530-143">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="a5530-144">Пример: tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="a5530-144">Example:tel:2125551212</span></span>
* <span data-ttu-id="a5530-145">**Действия только для Android**</span><span class="sxs-lookup"><span data-stu-id="a5530-145">**Android only actions**</span></span>
  * <span data-ttu-id="a5530-146">Скачать приложение в магазине Google Play hello</span><span class="sxs-lookup"><span data-stu-id="a5530-146">Download an application on hello Play Store</span></span>
  * <span data-ttu-id="a5530-147">market://details?id=\[пакет_приложения\];</span><span class="sxs-lookup"><span data-stu-id="a5530-147">market://details?id=\[app package\]</span></span> 
  * <span data-ttu-id="a5530-148">Пример: market://details?id=com.microsoft.office.word</span><span class="sxs-lookup"><span data-stu-id="a5530-148">Example:market://details?id=com.microsoft.office.word</span></span>
  * <span data-ttu-id="a5530-149">Запуск поиска по географическому расположению</span><span class="sxs-lookup"><span data-stu-id="a5530-149">Start a geo-localized search</span></span>
  * <span data-ttu-id="a5530-150">geo:0,0?q=\[запрос_поиска\];</span><span class="sxs-lookup"><span data-stu-id="a5530-150">geo:0,0?q=\[search query\]</span></span> 
  * <span data-ttu-id="a5530-151">Пример:geo:0,0?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="a5530-151">Example:geo:0,0?q=starbucks,paris</span></span>
* <span data-ttu-id="a5530-152">**Действия только для iOS**</span><span class="sxs-lookup"><span data-stu-id="a5530-152">**iOS only actions**</span></span>
  * <span data-ttu-id="a5530-153">Скачать приложение hello App Store</span><span class="sxs-lookup"><span data-stu-id="a5530-153">Download an application on hello App Store</span></span>
  * <span data-ttu-id="a5530-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span><span class="sxs-lookup"><span data-stu-id="a5530-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span></span> 
  * <span data-ttu-id="a5530-155">например, http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8;</span><span class="sxs-lookup"><span data-stu-id="a5530-155">Example:http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span></span>
  * <span data-ttu-id="a5530-156">Действия для Windows</span><span class="sxs-lookup"><span data-stu-id="a5530-156">Windows Actions</span></span>
  * <span data-ttu-id="a5530-157">Открытие веб-страницы</span><span class="sxs-lookup"><span data-stu-id="a5530-157">Open a web page</span></span>
  * <span data-ttu-id="a5530-158">http://\[домен_веб_сайта\];</span><span class="sxs-lookup"><span data-stu-id="a5530-158">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="a5530-159">например, http://www.azure.com;</span><span class="sxs-lookup"><span data-stu-id="a5530-159">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="a5530-160">Отправка сообщения электронной почты</span><span class="sxs-lookup"><span data-stu-id="a5530-160">Send an e-mail</span></span>
  * <span data-ttu-id="a5530-161">mailto:\[получатель\]?subject=\[тема\]&body=\[сообщение\];</span><span class="sxs-lookup"><span data-stu-id="a5530-161">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="a5530-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="a5530-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="a5530-163">Отправка SMS-сообщения (требуется приложение Skype из Магазина)</span><span class="sxs-lookup"><span data-stu-id="a5530-163">Send a SMS (Skype Store App required)</span></span>
  * <span data-ttu-id="a5530-164">sms:\[номер_телефона\];</span><span class="sxs-lookup"><span data-stu-id="a5530-164">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="a5530-165">Пример: sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="a5530-165">Example:sms:2125551212</span></span>
  * <span data-ttu-id="a5530-166">Набор номера телефона (требуется приложение Skype из Магазина)</span><span class="sxs-lookup"><span data-stu-id="a5530-166">Dial a phone number (Skype Store App required)</span></span>
  * <span data-ttu-id="a5530-167">tel:\[номер_телефона\];</span><span class="sxs-lookup"><span data-stu-id="a5530-167">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="a5530-168">Пример: tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="a5530-168">Example:tel:2125551212</span></span>
  * <span data-ttu-id="a5530-169">Скачать приложение в магазине Google Play hello</span><span class="sxs-lookup"><span data-stu-id="a5530-169">Download an application on hello Play Store</span></span>
  * <span data-ttu-id="a5530-170">ms-windows-store:PDP?PFN=\[идентификатор_пакета_приложения\];</span><span class="sxs-lookup"><span data-stu-id="a5530-170">ms-windows-store:PDP?PFN=\[app package ID\]</span></span> 
  * <span data-ttu-id="a5530-171">Пример: ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span><span class="sxs-lookup"><span data-stu-id="a5530-171">Example:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span></span>
  * <span data-ttu-id="a5530-172">Запуск поиска по картам Bing</span><span class="sxs-lookup"><span data-stu-id="a5530-172">Start a bingmaps search</span></span>
  * <span data-ttu-id="a5530-173">bingmaps:?q=\[запрос_поиска\];</span><span class="sxs-lookup"><span data-stu-id="a5530-173">bingmaps:?q=\[search query\]</span></span> 
  * <span data-ttu-id="a5530-174">Пример:bingmaps:?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="a5530-174">Example:bingmaps:?q=starbucks,paris</span></span>
  * <span data-ttu-id="a5530-175">Использование пользовательской схемы</span><span class="sxs-lookup"><span data-stu-id="a5530-175">Use a custom scheme</span></span>
  * <span data-ttu-id="a5530-176">\[пользовательская_схема\]://\[параметры_пользовательской_схемы\];</span><span class="sxs-lookup"><span data-stu-id="a5530-176">\[custom scheme\]://\[custom scheme params\]</span></span> 
  * <span data-ttu-id="a5530-177">Пример: myCustomProtocol://myCustomParams</span><span class="sxs-lookup"><span data-stu-id="a5530-177">Example:myCustomProtocol://myCustomParams</span></span>
  * <span data-ttu-id="a5530-178">Использование данных пакета (требуется приложение из Магазина для расширения для чтения)</span><span class="sxs-lookup"><span data-stu-id="a5530-178">Use a package data (Store App for extension read required)</span></span>
  * <span data-ttu-id="a5530-179">\[папка\]\[данные\].\[расширение\];</span><span class="sxs-lookup"><span data-stu-id="a5530-179">\[folder\]\[data\].\[extension\]</span></span> 
  * <span data-ttu-id="a5530-180">Пример: myfolderdata.txt</span><span class="sxs-lookup"><span data-stu-id="a5530-180">Example:myfolderdata.txt</span></span>

### <a name="build-a-tracking-url"></a><span data-ttu-id="a5530-181">Создание URL-адреса отслеживания</span><span class="sxs-lookup"><span data-stu-id="a5530-181">Build a Tracking URL:</span></span>
* <span data-ttu-id="a5530-182">В разделе hello раздел «Параметры» hello <UI Documentation> для инструкций по созданию URL-адрес отслеживания, позволит пользователям toodownload одного из других приложений.</span><span class="sxs-lookup"><span data-stu-id="a5530-182">See hello “Settings” section of hello <UI Documentation> for instruction on building a tracking URL that will allow users toodownload one of your other applications.</span></span>

### <a name="define-hello-texts-of-your-announcement"></a><span data-ttu-id="a5530-183">Определить текст hello объявления</span><span class="sxs-lookup"><span data-stu-id="a5530-183">Define hello texts of your announcement</span></span>
<span data-ttu-id="a5530-184">Заполните hello заголовок, содержимое и текст кнопки объявления.</span><span class="sxs-lookup"><span data-stu-id="a5530-184">Fill in hello title, content, and button texts of your announcement.</span></span> <span data-ttu-id="a5530-185">Можно выбрать целевую аудиторию будущих кампании на основе отзывов reach hello объекта ответы пользователей toothis кампании.</span><span class="sxs-lookup"><span data-stu-id="a5530-185">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="a5530-186">Целевой аудитории может основываться на отзывах hello объекта ли эта Кампания был только что отправлен, был дан ответ, обработаны или закрыты.</span><span class="sxs-lookup"><span data-stu-id="a5530-186">Audience targeting can be based on hello feedback of whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="a5530-187">См. также</span><span class="sxs-lookup"><span data-stu-id="a5530-187">See also</span></span>
* <span data-ttu-id="a5530-188">[Организация кампаний по рассылке push-уведомлений выбранному подмножеству пользователей с помощью условий таргетинга][Link 28]</span><span class="sxs-lookup"><span data-stu-id="a5530-188">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-polls"></a><span data-ttu-id="a5530-189">Содержимое опросов</span><span class="sxs-lookup"><span data-stu-id="a5530-189">Content of Polls</span></span>
![Рекламная кампания — Содержимое 2][31] 

<span data-ttu-id="a5530-191">Заполните hello название, описание и текст кнопки объявления.</span><span class="sxs-lookup"><span data-stu-id="a5530-191">Fill in hello title, description, and button texts of your announcement.</span></span> <span data-ttu-id="a5530-192">Затем добавьте вопросов и вариантов для hello ответы tooyour вопросов.</span><span class="sxs-lookup"><span data-stu-id="a5530-192">Then, add questions and choices for hello answers tooyour questions.</span></span>
<span data-ttu-id="a5530-193">Можно выбрать целевую аудиторию будущих кампании на основе отзывов reach hello объекта ответы пользователей toothis кампании.</span><span class="sxs-lookup"><span data-stu-id="a5530-193">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="a5530-194">Кроме того, целевую аудиторию можно отслеживать на основе действий, совершенных с кампанией (отправка push-уведомления, ответ, выполнение действия или выход).</span><span class="sxs-lookup"><span data-stu-id="a5530-194">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span> <span data-ttu-id="a5530-195">Целевой аудитории может также основываться на ответам на опросы, где hello Выбор вопрос и ответ, используются в качестве критериев.</span><span class="sxs-lookup"><span data-stu-id="a5530-195">Audience targeting can also be based on Poll answer feedback, where hello question and answer choice are used as criteria.</span></span>

### <a name="see-also"></a><span data-ttu-id="a5530-196">См. также</span><span class="sxs-lookup"><span data-stu-id="a5530-196">See also</span></span>
* <span data-ttu-id="a5530-197">[Организация кампаний по рассылке push-уведомлений выбранному подмножеству пользователей с помощью условий таргетинга][Link 28]</span><span class="sxs-lookup"><span data-stu-id="a5530-197">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-data-pushes"></a><span data-ttu-id="a5530-198">Содержимое отправки данных</span><span class="sxs-lookup"><span data-stu-id="a5530-198">Content of Data Pushes</span></span>
![Рекламная кампания — Содержимое 3][32] 

### <a name="choose-hello-type-of-your-data"></a><span data-ttu-id="a5530-200">Выберите тип hello данных:</span><span class="sxs-lookup"><span data-stu-id="a5530-200">Choose hello type of your data:</span></span>
* <span data-ttu-id="a5530-201">текст</span><span class="sxs-lookup"><span data-stu-id="a5530-201">Text</span></span>
* <span data-ttu-id="a5530-202">Двоичные данные</span><span class="sxs-lookup"><span data-stu-id="a5530-202">Binary data</span></span>
* <span data-ttu-id="a5530-203">Данные Base64</span><span class="sxs-lookup"><span data-stu-id="a5530-203">Base64 data</span></span>

### <a name="define-hello-content-of-your-data"></a><span data-ttu-id="a5530-204">Определите содержимое данных hello</span><span class="sxs-lookup"><span data-stu-id="a5530-204">Define hello content of your data</span></span>
* <span data-ttu-id="a5530-205">Если вы выбрали toopush текстовые данные, скопируйте и вставьте текст hello в поле «содержимое» hello.</span><span class="sxs-lookup"><span data-stu-id="a5530-205">If you selected toopush text data, copy and paste hello text into hello "content" box.</span></span>
* <span data-ttu-id="a5530-206">Если вы выбрали toopush данных binary или base64, использовать tooupload кнопки «Отправить файл» hello файл.</span><span class="sxs-lookup"><span data-stu-id="a5530-206">If you selected toopush either binary or base64 data, use hello "upload your file" button tooupload your file.</span></span>
* <span data-ttu-id="a5530-207">Можно выбрать целевую аудиторию будущих кампании на основе отзывов reach hello объекта ответы пользователей toothis кампании.</span><span class="sxs-lookup"><span data-stu-id="a5530-207">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="a5530-208">Кроме того, целевую аудиторию можно отслеживать на основе действий, совершенных с кампанией (отправка push-уведомления, ответ, выполнение действия или выход).</span><span class="sxs-lookup"><span data-stu-id="a5530-208">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="a5530-209">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="a5530-209">See also</span></span>
* <span data-ttu-id="a5530-210">[Организация кампаний по рассылке push-уведомлений выбранному подмножеству пользователей с помощью условий таргетинга][Link 28]</span><span class="sxs-lookup"><span data-stu-id="a5530-210">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-tiles-windows-phone-only"></a><span data-ttu-id="a5530-211">Содержимое плиток (только для Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="a5530-211">Content of Tiles (Windows Phone only)</span></span>
![Рекламная кампания — Содержимое 4][33]

### <a name="define-hello-content-of-your-tile"></a><span data-ttu-id="a5530-213">Определение контента плитки приветствия</span><span class="sxs-lookup"><span data-stu-id="a5530-213">Define hello content of your tile</span></span>
<span data-ttu-id="a5530-214">полезные данные плитки Hello представляют Привет toobe текст, отображаются на плитке приветствия приложения на устройствах Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="a5530-214">hello tile payload is hello text toobe displayed in hello tile of your app on Windows Phone devices.</span></span>
<span data-ttu-id="a5530-215">Принудительная плитки — версия службы Microsoft Push Notification Service (MPNS) hello собственные Push-уведомления для Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="a5530-215">A tile push is hello Microsoft Push Notification Service (MPNS) version of a native push for Windows Phone.</span></span> <span data-ttu-id="a5530-216">Hello плитки push-hello только принудительной типом, нет ответа и таким образом hello аудитория будущих кампаний не может быть построен на hello результаты кампании push плитки.</span><span class="sxs-lookup"><span data-stu-id="a5530-216">hello tile push type is hello only push type that does not have a response and so hello audience of future campaigns can't be built on hello results of a tile push campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="a5530-217">См. также</span><span class="sxs-lookup"><span data-stu-id="a5530-217">See also</span></span>
* <span data-ttu-id="a5530-218">[Mobile Engagement][Link 4]</span><span class="sxs-lookup"><span data-stu-id="a5530-218">[API Documentation - Reach API - Native Push][Link 4]</span></span>

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

