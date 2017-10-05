---
title: "Интерфейсы API веб-пакета SDK для Служб мобильного взаимодействия Azure | Документация Майкрософт"
description: "Последние обновления и процедуры для веб-пакета SDK для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8a87d5ac-d8b7-4a0d-bdee-414dbcc561b2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: 54c22ce6a03e382b1bbde102bccc97deec249b30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-mobile-engagement-api-in-a-web-application"></a><span data-ttu-id="8da44-103">Использование API Служб мобильного взаимодействия Azure в веб-приложении</span><span class="sxs-lookup"><span data-stu-id="8da44-103">Use the Azure Mobile Engagement API in a web application</span></span>
<span data-ttu-id="8da44-104">Этот документ представляет собой дополнение к документу, в котором описывается, [как интегрировать Службы мобильного взаимодействия в веб-приложение](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="8da44-104">This document is an addition to the document that tells you how to [integrate Mobile Engagement in a web application](mobile-engagement-web-integrate-engagement.md).</span></span> <span data-ttu-id="8da44-105">В нем подробно рассказывается о том, как с помощью API Служб мобильного взаимодействия Azure предоставлять статистику по приложению.</span><span class="sxs-lookup"><span data-stu-id="8da44-105">It provides in-depth details about how to use the Azure Mobile Engagement API to report your application statistics.</span></span>

<span data-ttu-id="8da44-106">API Служб мобильного взаимодействия предоставляется в объекте `engagement.agent`.</span><span class="sxs-lookup"><span data-stu-id="8da44-106">The Mobile Engagement API is provided by the `engagement.agent` object.</span></span> <span data-ttu-id="8da44-107">Псевдоним веб-пакета SDK для Служб мобильного взаимодействия Azure — `engagement`.</span><span class="sxs-lookup"><span data-stu-id="8da44-107">The default Azure Mobile Engagement Web SDK alias is `engagement`.</span></span> <span data-ttu-id="8da44-108">Этот псевдоним можно переопределить в конфигурации пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="8da44-108">You can redefine this alias from the SDK configuration.</span></span>

## <a name="mobile-engagement-concepts"></a><span data-ttu-id="8da44-109">Основные понятия Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="8da44-109">Mobile Engagement concepts</span></span>
<span data-ttu-id="8da44-110">В следующих подразделах дано более подробное объяснение [основных понятий Служб мобильного взаимодействия](mobile-engagement-concepts.md) для веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="8da44-110">The following parts refine common [Mobile Engagement concepts](mobile-engagement-concepts.md) for the web platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="8da44-111">`Session` и `Activity`</span><span class="sxs-lookup"><span data-stu-id="8da44-111">`Session` and `Activity`</span></span>
<span data-ttu-id="8da44-112">Если пользователь неактивен между двумя действиями больше чем несколько секунд, то последовательность его действий разбивается на два отдельных сеанса.</span><span class="sxs-lookup"><span data-stu-id="8da44-112">If the user stays idle for more than a few seconds between two activities, the user's sequence of activities is split into two distinct sessions.</span></span> <span data-ttu-id="8da44-113">Эти несколько секунд называются временем ожидания сеанса.</span><span class="sxs-lookup"><span data-stu-id="8da44-113">These few seconds are called the session timeout.</span></span>

<span data-ttu-id="8da44-114">Если веб-приложение не объявит завершение действия пользователя (путем вызова функции `engagement.agent.endActivity`), то сервер Служб мобильного взаимодействия автоматически завершит сеанс пользователя через три минуты после закрытия страницы приложения.</span><span class="sxs-lookup"><span data-stu-id="8da44-114">If your web application doesn't declare the end of user activities by itself (by calling the `engagement.agent.endActivity` function), the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span></span> <span data-ttu-id="8da44-115">Это называется временем ожидания сеанса сервера.</span><span class="sxs-lookup"><span data-stu-id="8da44-115">This is called the server session timeout.</span></span>

### `Crash`
<span data-ttu-id="8da44-116">Автоматические отчеты неперехваченных исключений JavaScript не создаются по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8da44-116">Automated reports of uncaught JavaScript exceptions are not created by default.</span></span> <span data-ttu-id="8da44-117">Тем не менее можно сообщать о сбоях вручную с помощью функции `sendCrash` (см. раздел об отчетах о сбоях).</span><span class="sxs-lookup"><span data-stu-id="8da44-117">However, you can report crashes manually by using the `sendCrash` function (see the section on reporting crashes).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="8da44-118">Создание отчетов о действиях</span><span class="sxs-lookup"><span data-stu-id="8da44-118">Reporting activities</span></span>
<span data-ttu-id="8da44-119">Создание отчетов о действиях пользователей начинается при запуске нового действия и заканчивается, когда пользователь завершает текущее действие.</span><span class="sxs-lookup"><span data-stu-id="8da44-119">Reporting on user activity includes when a user starts a new activity, and when the user ends the current activity.</span></span>

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="8da44-120">Пользователь запускает новое действие</span><span class="sxs-lookup"><span data-stu-id="8da44-120">User starts a new activity</span></span>
    engagement.agent.startActivity("MyUserActivity");

<span data-ttu-id="8da44-121">При каждом изменении пользовательского действия необходимо вызывать метод `startActivity()` .</span><span class="sxs-lookup"><span data-stu-id="8da44-121">You need to call `startActivity()` each time user activity changes.</span></span> <span data-ttu-id="8da44-122">При первом вызове этой функции начинается новый сеанс пользователя.</span><span class="sxs-lookup"><span data-stu-id="8da44-122">The first call to this function starts a new user session.</span></span>

### <a name="user-ends-the-current-activity"></a><span data-ttu-id="8da44-123">Пользователь завершает текущее действие</span><span class="sxs-lookup"><span data-stu-id="8da44-123">User ends the current activity</span></span>
    engagement.agent.endActivity();

<span data-ttu-id="8da44-124">Когда пользователь заканчивает свое последнее действие, необходимо как минимум один раз вызвать метод `endActivity()` .</span><span class="sxs-lookup"><span data-stu-id="8da44-124">You need to call `endActivity()` at least once when the user finishes their last activity.</span></span> <span data-ttu-id="8da44-125">В результате веб-пакет SDK для Служб мобильного взаимодействия получает сведения о том, что пользователь находится в режиме ожидания и по истечении этого времени сеанс необходимо закрыть.</span><span class="sxs-lookup"><span data-stu-id="8da44-125">This informs the Mobile Engagement Web SDK that the user is currently idle, and that the user session needs to be closed after the session timeout expires.</span></span> <span data-ttu-id="8da44-126">Если до окончания времени ожидания завершения сеанса вызвать метод `startActivity()` , сеанс будет возобновлен.</span><span class="sxs-lookup"><span data-stu-id="8da44-126">If you call `startActivity()` before the session timeout expires, the session is simply resumed.</span></span>

<span data-ttu-id="8da44-127">Часто бывает сложно или невозможно определить завершение действий пользователя внутри веб-среды, так как четкого сигнала о закрытии окна навигатора не поступает.</span><span class="sxs-lookup"><span data-stu-id="8da44-127">Because there's no reliable call for when the navigator window is closed, it's often difficult or impossible to catch the end of user activities inside a web environment.</span></span> <span data-ttu-id="8da44-128">Поэтому сервер Служб мобильного взаимодействия автоматически завершает сеанс пользователя через три минуты после закрытия страницы приложения.</span><span class="sxs-lookup"><span data-stu-id="8da44-128">That's why the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="8da44-129">Создание отчетов о событиях</span><span class="sxs-lookup"><span data-stu-id="8da44-129">Reporting events</span></span>
<span data-ttu-id="8da44-130">Отчеты создаются о событиях сеанса и изолированных событиях.</span><span class="sxs-lookup"><span data-stu-id="8da44-130">Reporting on events covers session events and standalone events.</span></span>

### <a name="session-events"></a><span data-ttu-id="8da44-131">События сеанса</span><span class="sxs-lookup"><span data-stu-id="8da44-131">Session events</span></span>
<span data-ttu-id="8da44-132">События сеанса обычно используются для создания отчетов о действиях, выполняемых пользователем во время сеанса.</span><span class="sxs-lookup"><span data-stu-id="8da44-132">Session events usually are used to report the actions performed by a user during the user's session.</span></span>

<span data-ttu-id="8da44-133">**Пример без дополнительных данных:**</span><span class="sxs-lookup"><span data-stu-id="8da44-133">**Example without extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

<span data-ttu-id="8da44-134">**Пример с дополнительными данными:**</span><span class="sxs-lookup"><span data-stu-id="8da44-134">**Example with extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="8da44-135">Изолированные события</span><span class="sxs-lookup"><span data-stu-id="8da44-135">Standalone events</span></span>
<span data-ttu-id="8da44-136">В отличие от событий сеанса изолированные события могут происходить вне контекста сеанса.</span><span class="sxs-lookup"><span data-stu-id="8da44-136">Unlike session events, standalone events can occur outside the context of a session.</span></span>

<span data-ttu-id="8da44-137">Для этого вместо метода ``engagement.agent.sendSessionEvent`` используется ``engagement.agent.sendEvent``.</span><span class="sxs-lookup"><span data-stu-id="8da44-137">For that, use ``engagement.agent.sendEvent`` instead of ``engagement.agent.sendSessionEvent``.</span></span>

## <a name="reporting-errors"></a><span data-ttu-id="8da44-138">Создание отчетов об ошибках</span><span class="sxs-lookup"><span data-stu-id="8da44-138">Reporting errors</span></span>
<span data-ttu-id="8da44-139">Отчеты создаются об ошибках сеанса и изолированных ошибках.</span><span class="sxs-lookup"><span data-stu-id="8da44-139">Reporting on errors covers session errors and standalone errors.</span></span>

### <a name="session-errors"></a><span data-ttu-id="8da44-140">Ошибки сеанса</span><span class="sxs-lookup"><span data-stu-id="8da44-140">Session errors</span></span>
<span data-ttu-id="8da44-141">Ошибки сеанса обычно используются для создания отчетов об ошибках, которые оказывают влияние на пользователя во время сеанса.</span><span class="sxs-lookup"><span data-stu-id="8da44-141">Session errors usually are used to report the errors that have an impact on the user during the user's session.</span></span>

<span data-ttu-id="8da44-142">**Пример без дополнительных данных:**</span><span class="sxs-lookup"><span data-stu-id="8da44-142">**Example without extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

<span data-ttu-id="8da44-143">**Пример с дополнительными данными:**</span><span class="sxs-lookup"><span data-stu-id="8da44-143">**Example with extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="8da44-144">Изолированные ошибки</span><span class="sxs-lookup"><span data-stu-id="8da44-144">Standalone errors</span></span>
<span data-ttu-id="8da44-145">В отличие от ошибок сеанса изолированные ошибки могут возникать вне контекста сеанса.</span><span class="sxs-lookup"><span data-stu-id="8da44-145">Unlike session errors, standalone errors can occur outside the context of a session.</span></span>

<span data-ttu-id="8da44-146">Для этого вместо метода `engagement.agent.sendSessionError` используется `engagement.agent.sendError`.</span><span class="sxs-lookup"><span data-stu-id="8da44-146">For that, use `engagement.agent.sendError` instead of `engagement.agent.sendSessionError`.</span></span>

## <a name="reporting-jobs"></a><span data-ttu-id="8da44-147">Создание отчетов о заданиях</span><span class="sxs-lookup"><span data-stu-id="8da44-147">Reporting jobs</span></span>
<span data-ttu-id="8da44-148">Для заданий создаются отчеты об ошибках отчетов и о событиях, происходящих во время выполнения задания, а также сбои отчетов.</span><span class="sxs-lookup"><span data-stu-id="8da44-148">Reporting on jobs covers reporting errors and events that occur during a job, and reporting crashes.</span></span>

<span data-ttu-id="8da44-149">**Пример**</span><span class="sxs-lookup"><span data-stu-id="8da44-149">**Example:**</span></span>

<span data-ttu-id="8da44-150">Если необходимо отслеживать запрос AJAX, используйте следующий код.</span><span class="sxs-lookup"><span data-stu-id="8da44-150">If you want to monitor an AJAX request, you'd use the following:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
      // [...]
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-errors-during-a-job"></a><span data-ttu-id="8da44-151">Создание отчетов об ошибках при выполнении задания</span><span class="sxs-lookup"><span data-stu-id="8da44-151">Reporting errors during a job</span></span>
<span data-ttu-id="8da44-152">Ошибки могут быть связаны с выполняемым заданием, а не с текущим сеансом пользователя.</span><span class="sxs-lookup"><span data-stu-id="8da44-152">Errors can be related to a running job instead of to the current user session.</span></span>

<span data-ttu-id="8da44-153">**Пример**</span><span class="sxs-lookup"><span data-stu-id="8da44-153">**Example:**</span></span>

<span data-ttu-id="8da44-154">Если нужно сообщить об ошибке в случае сбоя запроса AJAX, используйте следующий код.</span><span class="sxs-lookup"><span data-stu-id="8da44-154">If you want to report an error if an AJAX request fails:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
        // [...]
        if (xhr.status == 0 || xhr.status >= 400) {
          engagement.agent.sendJobError('publish_xhr', 'publish', {status: xhr.status, statusText: xhr.statusText});
        }
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="8da44-155">Создание отчетов о событиях во время выполнения задания</span><span class="sxs-lookup"><span data-stu-id="8da44-155">Reporting events during a job</span></span>
<span data-ttu-id="8da44-156">События могут быть связаны с выполняемым заданием, а не с текущим сеансом пользователя, благодаря функции `engagement.agent.sendJobEvent` .</span><span class="sxs-lookup"><span data-stu-id="8da44-156">Events can be related to a running job instead of to the current user session, thanks to the `engagement.agent.sendJobEvent` function.</span></span>

<span data-ttu-id="8da44-157">Эта функция работает в точности как функция `engagement.agent.sendJobError`.</span><span class="sxs-lookup"><span data-stu-id="8da44-157">This function works exactly like `engagement.agent.sendJobError`.</span></span>

### <a name="reporting-crashes"></a><span data-ttu-id="8da44-158">Создание отчетов о сбоях</span><span class="sxs-lookup"><span data-stu-id="8da44-158">Reporting crashes</span></span>
<span data-ttu-id="8da44-159">Используйте функцию `sendCrash` для создания отчетов о сбоях вручную.</span><span class="sxs-lookup"><span data-stu-id="8da44-159">Use the `sendCrash` function to report crashes manually.</span></span>

<span data-ttu-id="8da44-160">Аргумент `crashid` — это строка, определяющая тип сбоя.</span><span class="sxs-lookup"><span data-stu-id="8da44-160">The `crashid` argument is a string that identifies the type of crash.</span></span>
<span data-ttu-id="8da44-161">Аргумент `crash` — это, как правило, трассировка стека сбоя в виде строки.</span><span class="sxs-lookup"><span data-stu-id="8da44-161">The `crash` argument usually is the stack trace of the crash as a string.</span></span>

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a><span data-ttu-id="8da44-162">Дополнительные параметры</span><span class="sxs-lookup"><span data-stu-id="8da44-162">Extra parameters</span></span>
<span data-ttu-id="8da44-163">Вы можете присоединить произвольные данные к событию, ошибке, действию или заданию.</span><span class="sxs-lookup"><span data-stu-id="8da44-163">You can attach arbitrary data to an event, error, activity, or job.</span></span>

<span data-ttu-id="8da44-164">Данные могут быть любым объектом JSON (не массивом или простыми типами).</span><span class="sxs-lookup"><span data-stu-id="8da44-164">The data can be any JSON object (but not an array or primitive type).</span></span>

<span data-ttu-id="8da44-165">**Пример**</span><span class="sxs-lookup"><span data-stu-id="8da44-165">**Example:**</span></span>

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="8da44-166">Ограничения</span><span class="sxs-lookup"><span data-stu-id="8da44-166">Limits</span></span>
<span data-ttu-id="8da44-167">К дополнительным параметрам применяются ограничения в области регулярных выражений для ключей, типов значений и размера.</span><span class="sxs-lookup"><span data-stu-id="8da44-167">Limits that apply to extra parameters are in the areas of regular expressions for keys, value types, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="8da44-168">ключей</span><span class="sxs-lookup"><span data-stu-id="8da44-168">Keys</span></span>
<span data-ttu-id="8da44-169">Каждый ключ в объекте должен соответствовать следующему регулярному выражению:</span><span class="sxs-lookup"><span data-stu-id="8da44-169">Each key in the object must match the following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="8da44-170">Это означает, что ключ должен содержать не менее одной буквы, за которой следуют буквы, цифры или символы подчеркивания (\_).</span><span class="sxs-lookup"><span data-stu-id="8da44-170">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="values"></a><span data-ttu-id="8da44-171">Значения</span><span class="sxs-lookup"><span data-stu-id="8da44-171">Values</span></span>
<span data-ttu-id="8da44-172">Допустимые типы значений: строка, число и логическое значение.</span><span class="sxs-lookup"><span data-stu-id="8da44-172">Values are limited to string, number, and Boolean types.</span></span>

#### <a name="size"></a><span data-ttu-id="8da44-173">Размер</span><span class="sxs-lookup"><span data-stu-id="8da44-173">Size</span></span>
<span data-ttu-id="8da44-174">Вспомогательные элементы ограничены до 1024 знаков на вызов (после того, как веб-пакет SDK для Служб мобильного взаимодействия закодирует его в JSON).</span><span class="sxs-lookup"><span data-stu-id="8da44-174">Extras are limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="8da44-175">Создание отчетов о данных приложения</span><span class="sxs-lookup"><span data-stu-id="8da44-175">Reporting application information</span></span>
<span data-ttu-id="8da44-176">С помощью функции `sendAppInfo()` вы можете вручную сообщать о данных отслеживания (или любых других данных о приложении).</span><span class="sxs-lookup"><span data-stu-id="8da44-176">You can manually report tracking information (or any other application-specific information) by using the `sendAppInfo()` function.</span></span>

<span data-ttu-id="8da44-177">Обратите внимание, что эти данные можно отправлять поэтапно.</span><span class="sxs-lookup"><span data-stu-id="8da44-177">Note that this information can be sent incrementally.</span></span> <span data-ttu-id="8da44-178">Для конкретного устройства будет сохраняться только последнее значение определенного ключа.</span><span class="sxs-lookup"><span data-stu-id="8da44-178">Only the latest value for a specific key will be kept for a specific device.</span></span>

<span data-ttu-id="8da44-179">Как и в случае со вспомогательными данными событий, для извлечения сведений о приложении можно использовать любой объект JSON.</span><span class="sxs-lookup"><span data-stu-id="8da44-179">Like event extras, you can use any JSON object to abstract application information.</span></span> <span data-ttu-id="8da44-180">Обратите внимание, что массивы или вложенные объекты рассматриваются как неструктурированные строки (с использованием сериализации JSON).</span><span class="sxs-lookup"><span data-stu-id="8da44-180">Note that arrays or sub-objects are treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="8da44-181">**Пример**</span><span class="sxs-lookup"><span data-stu-id="8da44-181">**Example:**</span></span>

<span data-ttu-id="8da44-182">Ниже приведен пример кода для отправки данных о половой принадлежности пользователя и его дате рождения.</span><span class="sxs-lookup"><span data-stu-id="8da44-182">Here is a code sample for sending the user's gender and birth date:</span></span>

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a><span data-ttu-id="8da44-183">Ограничения</span><span class="sxs-lookup"><span data-stu-id="8da44-183">Limits</span></span>
<span data-ttu-id="8da44-184">К данным о приложении применяются ограничения в области регулярных выражений для ключей и размера.</span><span class="sxs-lookup"><span data-stu-id="8da44-184">Limits that apply to application information are in the areas of regular expressions for keys, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="8da44-185">ключей</span><span class="sxs-lookup"><span data-stu-id="8da44-185">Keys</span></span>
<span data-ttu-id="8da44-186">Каждый ключ в объекте должен соответствовать следующему регулярному выражению:</span><span class="sxs-lookup"><span data-stu-id="8da44-186">Each key in the object must match the following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="8da44-187">Это означает, что ключ должен содержать не менее одной буквы, за которой следуют буквы, цифры или символы подчеркивания (\_).</span><span class="sxs-lookup"><span data-stu-id="8da44-187">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="8da44-188">Размер</span><span class="sxs-lookup"><span data-stu-id="8da44-188">Size</span></span>
<span data-ttu-id="8da44-189">Данные о приложении ограничены до 1024 знаков на вызов (после того, как веб-пакет SDK для Служб мобильного взаимодействия закодирует его в JSON).</span><span class="sxs-lookup"><span data-stu-id="8da44-189">Application information is limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span></span>

<span data-ttu-id="8da44-190">В предыдущем примере длина JSON-файла, отправленного на сервер, составляет 44 знака.</span><span class="sxs-lookup"><span data-stu-id="8da44-190">In the preceding example, the JSON sent to the server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
