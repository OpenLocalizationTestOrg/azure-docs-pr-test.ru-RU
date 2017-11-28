---
title: "aaaAzure веб-пакет SDK Mobile Engagement API | Документы Microsoft"
description: "Здравствуйте, последние обновления и процедуры для hello Web SDK для Azure Mobile Engagement"
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
ms.openlocfilehash: ec1261d6ad573b8c3ad6d5f616ab7bbe560d6fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-mobile-engagement-api-in-a-web-application"></a><span data-ttu-id="a20cd-103">Использовать hello Azure Mobile Engagement API веб-приложения</span><span class="sxs-lookup"><span data-stu-id="a20cd-103">Use hello Azure Mobile Engagement API in a web application</span></span>
<span data-ttu-id="a20cd-104">Этот документ является документом toohello сложения, информирующее о том, как слишком[интегрировать в веб-приложение Mobile Engagement](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="a20cd-104">This document is an addition toohello document that tells you how too[integrate Mobile Engagement in a web application](mobile-engagement-web-integrate-engagement.md).</span></span> <span data-ttu-id="a20cd-105">Он предоставляет подробные сведения о том, как toouse hello Azure Mobile Engagement API tooreport статистики вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="a20cd-105">It provides in-depth details about how toouse hello Azure Mobile Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="a20cd-106">Hello Mobile Engagement API обеспечивается hello `engagement.agent` объекта.</span><span class="sxs-lookup"><span data-stu-id="a20cd-106">hello Mobile Engagement API is provided by hello `engagement.agent` object.</span></span> <span data-ttu-id="a20cd-107">по умолчанию, Azure Mobile Engagement Web SDK псевдоним: Hello `engagement`.</span><span class="sxs-lookup"><span data-stu-id="a20cd-107">hello default Azure Mobile Engagement Web SDK alias is `engagement`.</span></span> <span data-ttu-id="a20cd-108">Можно переопределить этот псевдоним из конфигурации пакета SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="a20cd-108">You can redefine this alias from hello SDK configuration.</span></span>

## <a name="mobile-engagement-concepts"></a><span data-ttu-id="a20cd-109">Основные понятия Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="a20cd-109">Mobile Engagement concepts</span></span>
<span data-ttu-id="a20cd-110">Hello следующие части уточнения общих [мобильного охвата понятия](mobile-engagement-concepts.md) для hello веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="a20cd-110">hello following parts refine common [Mobile Engagement concepts](mobile-engagement-concepts.md) for hello web platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="a20cd-111">`Session` и `Activity`</span><span class="sxs-lookup"><span data-stu-id="a20cd-111">`Session` and `Activity`</span></span>
<span data-ttu-id="a20cd-112">Если более чем на несколько секунд между двумя действиями пользователя hello кластер простаивает, hello последовательность действий пользователя разбивается на двух различных сеансах.</span><span class="sxs-lookup"><span data-stu-id="a20cd-112">If hello user stays idle for more than a few seconds between two activities, hello user's sequence of activities is split into two distinct sessions.</span></span> <span data-ttu-id="a20cd-113">Эти несколько секунд, называются hello тайм-аут сеанса.</span><span class="sxs-lookup"><span data-stu-id="a20cd-113">These few seconds are called hello session timeout.</span></span>

<span data-ttu-id="a20cd-114">Если веб-приложение не объявляет hello конец действия пользователя само по себе (путем вызова hello `engagement.agent.endActivity` функции), сервера мобильного охвата hello автоматически истекает hello сеанс пользователя в течение трех минут после закрытия страницы приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a20cd-114">If your web application doesn't declare hello end of user activities by itself (by calling hello `engagement.agent.endActivity` function), hello Mobile Engagement server automatically expires hello user session within three minutes after hello application page is closed.</span></span> <span data-ttu-id="a20cd-115">Это называется hello время ожидания сеанса сервера.</span><span class="sxs-lookup"><span data-stu-id="a20cd-115">This is called hello server session timeout.</span></span>

### `Crash`
<span data-ttu-id="a20cd-116">Автоматические отчеты неперехваченных исключений JavaScript не создаются по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a20cd-116">Automated reports of uncaught JavaScript exceptions are not created by default.</span></span> <span data-ttu-id="a20cd-117">Тем не менее, можно сообщить сбоев вручную с помощью hello `sendCrash` функцию (см. раздел hello в reporting сбоев).</span><span class="sxs-lookup"><span data-stu-id="a20cd-117">However, you can report crashes manually by using hello `sendCrash` function (see hello section on reporting crashes).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="a20cd-118">Создание отчетов о действиях</span><span class="sxs-lookup"><span data-stu-id="a20cd-118">Reporting activities</span></span>
<span data-ttu-id="a20cd-119">Отчеты о активности пользователей включает в себя при запуске нового действия и hello пользователь завершает текущее действие hello.</span><span class="sxs-lookup"><span data-stu-id="a20cd-119">Reporting on user activity includes when a user starts a new activity, and when hello user ends hello current activity.</span></span>

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="a20cd-120">Пользователь запускает новое действие</span><span class="sxs-lookup"><span data-stu-id="a20cd-120">User starts a new activity</span></span>
    engagement.agent.startActivity("MyUserActivity");

<span data-ttu-id="a20cd-121">Требуется toocall `startActivity()` каждого действий пользователя во время изменения.</span><span class="sxs-lookup"><span data-stu-id="a20cd-121">You need toocall `startActivity()` each time user activity changes.</span></span> <span data-ttu-id="a20cd-122">функции Hello первый вызов toothis начинает новый сеанс пользователя.</span><span class="sxs-lookup"><span data-stu-id="a20cd-122">hello first call toothis function starts a new user session.</span></span>

### <a name="user-ends-hello-current-activity"></a><span data-ttu-id="a20cd-123">Пользователь завершает текущее действие hello</span><span class="sxs-lookup"><span data-stu-id="a20cd-123">User ends hello current activity</span></span>
    engagement.agent.endActivity();

<span data-ttu-id="a20cd-124">Требуется toocall `endActivity()` по крайней мере один раз в том случае, когда пользователь hello завершается их последнее действие.</span><span class="sxs-lookup"><span data-stu-id="a20cd-124">You need toocall `endActivity()` at least once when hello user finishes their last activity.</span></span> <span data-ttu-id="a20cd-125">Это позволяет сообщить hello Mobile Engagement Web SDK hello пользователя находится в режиме ожидания, которое, hello пользовательский сеанс должен toobe закрыто после истечения времени ожидания сеанса hello.</span><span class="sxs-lookup"><span data-stu-id="a20cd-125">This informs hello Mobile Engagement Web SDK that hello user is currently idle, and that hello user session needs toobe closed after hello session timeout expires.</span></span> <span data-ttu-id="a20cd-126">При вызове метода `startActivity()` до истечения времени ожидания сеанса hello, просто возобновить сеанс hello.</span><span class="sxs-lookup"><span data-stu-id="a20cd-126">If you call `startActivity()` before hello session timeout expires, hello session is simply resumed.</span></span>

<span data-ttu-id="a20cd-127">Так как отсутствует надежный вызов для закрытия окна навигатора hello, часто бывает сложно или невозможно toocatch hello конец действия пользователя внутри веб-среды.</span><span class="sxs-lookup"><span data-stu-id="a20cd-127">Because there's no reliable call for when hello navigator window is closed, it's often difficult or impossible toocatch hello end of user activities inside a web environment.</span></span> <span data-ttu-id="a20cd-128">Почему является hello мобильного охвата, сервер автоматически истекает hello сеанс пользователя в течение трех минут после закрытия страницы приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a20cd-128">That's why hello Mobile Engagement server automatically expires hello user session within three minutes after hello application page is closed.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="a20cd-129">Создание отчетов о событиях</span><span class="sxs-lookup"><span data-stu-id="a20cd-129">Reporting events</span></span>
<span data-ttu-id="a20cd-130">Отчеты создаются о событиях сеанса и изолированных событиях.</span><span class="sxs-lookup"><span data-stu-id="a20cd-130">Reporting on events covers session events and standalone events.</span></span>

### <a name="session-events"></a><span data-ttu-id="a20cd-131">События сеанса</span><span class="sxs-lookup"><span data-stu-id="a20cd-131">Session events</span></span>
<span data-ttu-id="a20cd-132">События сеанса обычно являются используется tooreport hello действия, выполняемые пользователем во время сеанса пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="a20cd-132">Session events usually are used tooreport hello actions performed by a user during hello user's session.</span></span>

<span data-ttu-id="a20cd-133">**Пример без дополнительных данных:**</span><span class="sxs-lookup"><span data-stu-id="a20cd-133">**Example without extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

<span data-ttu-id="a20cd-134">**Пример с дополнительными данными:**</span><span class="sxs-lookup"><span data-stu-id="a20cd-134">**Example with extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="a20cd-135">Изолированные события</span><span class="sxs-lookup"><span data-stu-id="a20cd-135">Standalone events</span></span>
<span data-ttu-id="a20cd-136">В отличие от событий сеанса автономный события могут возникать за пределами hello контекст сеанса.</span><span class="sxs-lookup"><span data-stu-id="a20cd-136">Unlike session events, standalone events can occur outside hello context of a session.</span></span>

<span data-ttu-id="a20cd-137">Для этого вместо метода ``engagement.agent.sendSessionEvent`` используется ``engagement.agent.sendEvent``.</span><span class="sxs-lookup"><span data-stu-id="a20cd-137">For that, use ``engagement.agent.sendEvent`` instead of ``engagement.agent.sendSessionEvent``.</span></span>

## <a name="reporting-errors"></a><span data-ttu-id="a20cd-138">Создание отчетов об ошибках</span><span class="sxs-lookup"><span data-stu-id="a20cd-138">Reporting errors</span></span>
<span data-ttu-id="a20cd-139">Отчеты создаются об ошибках сеанса и изолированных ошибках.</span><span class="sxs-lookup"><span data-stu-id="a20cd-139">Reporting on errors covers session errors and standalone errors.</span></span>

### <a name="session-errors"></a><span data-ttu-id="a20cd-140">Ошибки сеанса</span><span class="sxs-lookup"><span data-stu-id="a20cd-140">Session errors</span></span>
<span data-ttu-id="a20cd-141">Сеанс ошибок обычно являются используется tooreport hello ошибок, которые оказывают влияние на hello пользователя во время сеанса пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="a20cd-141">Session errors usually are used tooreport hello errors that have an impact on hello user during hello user's session.</span></span>

<span data-ttu-id="a20cd-142">**Пример без дополнительных данных:**</span><span class="sxs-lookup"><span data-stu-id="a20cd-142">**Example without extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

<span data-ttu-id="a20cd-143">**Пример с дополнительными данными:**</span><span class="sxs-lookup"><span data-stu-id="a20cd-143">**Example with extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="a20cd-144">Изолированные ошибки</span><span class="sxs-lookup"><span data-stu-id="a20cd-144">Standalone errors</span></span>
<span data-ttu-id="a20cd-145">В отличие от ошибок сеансов могут возникать ошибки автономный вне контекста hello сеанса.</span><span class="sxs-lookup"><span data-stu-id="a20cd-145">Unlike session errors, standalone errors can occur outside hello context of a session.</span></span>

<span data-ttu-id="a20cd-146">Для этого вместо метода `engagement.agent.sendSessionError` используется `engagement.agent.sendError`.</span><span class="sxs-lookup"><span data-stu-id="a20cd-146">For that, use `engagement.agent.sendError` instead of `engagement.agent.sendSessionError`.</span></span>

## <a name="reporting-jobs"></a><span data-ttu-id="a20cd-147">Создание отчетов о заданиях</span><span class="sxs-lookup"><span data-stu-id="a20cd-147">Reporting jobs</span></span>
<span data-ttu-id="a20cd-148">Для заданий создаются отчеты об ошибках отчетов и о событиях, происходящих во время выполнения задания, а также сбои отчетов.</span><span class="sxs-lookup"><span data-stu-id="a20cd-148">Reporting on jobs covers reporting errors and events that occur during a job, and reporting crashes.</span></span>

<span data-ttu-id="a20cd-149">**Пример**</span><span class="sxs-lookup"><span data-stu-id="a20cd-149">**Example:**</span></span>

<span data-ttu-id="a20cd-150">Если вы хотите toomonitor AJAX-запросом, следует использовать hello следующее:</span><span class="sxs-lookup"><span data-stu-id="a20cd-150">If you want toomonitor an AJAX request, you'd use hello following:</span></span>

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

### <a name="reporting-errors-during-a-job"></a><span data-ttu-id="a20cd-151">Создание отчетов об ошибках при выполнении задания</span><span class="sxs-lookup"><span data-stu-id="a20cd-151">Reporting errors during a job</span></span>
<span data-ttu-id="a20cd-152">Ошибки могут быть связанные tooa выполнения задания вместо toohello текущий сеанс пользователя.</span><span class="sxs-lookup"><span data-stu-id="a20cd-152">Errors can be related tooa running job instead of toohello current user session.</span></span>

<span data-ttu-id="a20cd-153">**Пример**</span><span class="sxs-lookup"><span data-stu-id="a20cd-153">**Example:**</span></span>

<span data-ttu-id="a20cd-154">Если требуется, чтобы tooreport ошибку, если запрос AJAX вызывает ошибку:</span><span class="sxs-lookup"><span data-stu-id="a20cd-154">If you want tooreport an error if an AJAX request fails:</span></span>

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

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="a20cd-155">Создание отчетов о событиях во время выполнения задания</span><span class="sxs-lookup"><span data-stu-id="a20cd-155">Reporting events during a job</span></span>
<span data-ttu-id="a20cd-156">События могут быть связанные tooa выполнения задания вместо toohello текущий сеанс пользователя благодаря использованию toohello `engagement.agent.sendJobEvent` функции.</span><span class="sxs-lookup"><span data-stu-id="a20cd-156">Events can be related tooa running job instead of toohello current user session, thanks toohello `engagement.agent.sendJobEvent` function.</span></span>

<span data-ttu-id="a20cd-157">Эта функция работает в точности как функция `engagement.agent.sendJobError`.</span><span class="sxs-lookup"><span data-stu-id="a20cd-157">This function works exactly like `engagement.agent.sendJobError`.</span></span>

### <a name="reporting-crashes"></a><span data-ttu-id="a20cd-158">Создание отчетов о сбоях</span><span class="sxs-lookup"><span data-stu-id="a20cd-158">Reporting crashes</span></span>
<span data-ttu-id="a20cd-159">Используйте hello `sendCrash` tooreport функция аварийно завершает работу вручную.</span><span class="sxs-lookup"><span data-stu-id="a20cd-159">Use hello `sendCrash` function tooreport crashes manually.</span></span>

<span data-ttu-id="a20cd-160">Hello `crashid` аргументом является строка, определяющая тип hello аварийного завершения.</span><span class="sxs-lookup"><span data-stu-id="a20cd-160">hello `crashid` argument is a string that identifies hello type of crash.</span></span>
<span data-ttu-id="a20cd-161">Hello `crash` аргумент обычно является hello трассировка стека сбоя hello в виде строки.</span><span class="sxs-lookup"><span data-stu-id="a20cd-161">hello `crash` argument usually is hello stack trace of hello crash as a string.</span></span>

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a><span data-ttu-id="a20cd-162">Дополнительные параметры</span><span class="sxs-lookup"><span data-stu-id="a20cd-162">Extra parameters</span></span>
<span data-ttu-id="a20cd-163">Можно присоединить событие tooan произвольные данные, ошибки, действия или задания.</span><span class="sxs-lookup"><span data-stu-id="a20cd-163">You can attach arbitrary data tooan event, error, activity, or job.</span></span>

<span data-ttu-id="a20cd-164">Hello данных может быть любой объект JSON (но не массив или примитивного типа).</span><span class="sxs-lookup"><span data-stu-id="a20cd-164">hello data can be any JSON object (but not an array or primitive type).</span></span>

<span data-ttu-id="a20cd-165">**Пример**</span><span class="sxs-lookup"><span data-stu-id="a20cd-165">**Example:**</span></span>

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="a20cd-166">Ограничения</span><span class="sxs-lookup"><span data-stu-id="a20cd-166">Limits</span></span>
<span data-ttu-id="a20cd-167">Ограничения, применяемые параметры tooextra находятся в областях hello регулярных выражений для ключей, типы значений и размер.</span><span class="sxs-lookup"><span data-stu-id="a20cd-167">Limits that apply tooextra parameters are in hello areas of regular expressions for keys, value types, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="a20cd-168">ключей</span><span class="sxs-lookup"><span data-stu-id="a20cd-168">Keys</span></span>
<span data-ttu-id="a20cd-169">Каждый ключ в hello объекта должно соответствовать hello следующее регулярное выражение:</span><span class="sxs-lookup"><span data-stu-id="a20cd-169">Each key in hello object must match hello following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="a20cd-170">Это означает, что ключ должен содержать не менее одной буквы, за которой следуют буквы, цифры или символы подчеркивания (\_).</span><span class="sxs-lookup"><span data-stu-id="a20cd-170">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="values"></a><span data-ttu-id="a20cd-171">Значения</span><span class="sxs-lookup"><span data-stu-id="a20cd-171">Values</span></span>
<span data-ttu-id="a20cd-172">Значения: ограниченный toostring, номер и логических типов.</span><span class="sxs-lookup"><span data-stu-id="a20cd-172">Values are limited toostring, number, and Boolean types.</span></span>

#### <a name="size"></a><span data-ttu-id="a20cd-173">Размер</span><span class="sxs-lookup"><span data-stu-id="a20cd-173">Size</span></span>
<span data-ttu-id="a20cd-174">Вспомогательные элементы, ограниченные too1, 024 символов на вызов (после hello Mobile Engagement Web SDK кодирует его в формате JSON).</span><span class="sxs-lookup"><span data-stu-id="a20cd-174">Extras are limited too1,024 characters per call (after hello Mobile Engagement Web SDK encodes it in JSON).</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="a20cd-175">Создание отчетов о данных приложения</span><span class="sxs-lookup"><span data-stu-id="a20cd-175">Reporting application information</span></span>
<span data-ttu-id="a20cd-176">Можно вручную сообщить отслеживания сведения (или другие сведения о приложении) с помощью hello `sendAppInfo()` функции.</span><span class="sxs-lookup"><span data-stu-id="a20cd-176">You can manually report tracking information (or any other application-specific information) by using hello `sendAppInfo()` function.</span></span>

<span data-ttu-id="a20cd-177">Обратите внимание, что эти данные можно отправлять поэтапно.</span><span class="sxs-lookup"><span data-stu-id="a20cd-177">Note that this information can be sent incrementally.</span></span> <span data-ttu-id="a20cd-178">Hello только последнее значение для определенного раздела будут храниться для конкретного устройства.</span><span class="sxs-lookup"><span data-stu-id="a20cd-178">Only hello latest value for a specific key will be kept for a specific device.</span></span>

<span data-ttu-id="a20cd-179">Как дополнения событий можно использовать любые сведения приложения tooabstract объекта JSON.</span><span class="sxs-lookup"><span data-stu-id="a20cd-179">Like event extras, you can use any JSON object tooabstract application information.</span></span> <span data-ttu-id="a20cd-180">Обратите внимание, что массивы или вложенные объекты рассматриваются как неструктурированные строки (с использованием сериализации JSON).</span><span class="sxs-lookup"><span data-stu-id="a20cd-180">Note that arrays or sub-objects are treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="a20cd-181">**Пример**</span><span class="sxs-lookup"><span data-stu-id="a20cd-181">**Example:**</span></span>

<span data-ttu-id="a20cd-182">Ниже приведен образец кода для отправки пользователя hello пол и дату рождения:</span><span class="sxs-lookup"><span data-stu-id="a20cd-182">Here is a code sample for sending hello user's gender and birth date:</span></span>

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a><span data-ttu-id="a20cd-183">Ограничения</span><span class="sxs-lookup"><span data-stu-id="a20cd-183">Limits</span></span>
<span data-ttu-id="a20cd-184">Ограничения, применяемые tooapplication сведения находятся в областях hello регулярных выражений для ключей и размер.</span><span class="sxs-lookup"><span data-stu-id="a20cd-184">Limits that apply tooapplication information are in hello areas of regular expressions for keys, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="a20cd-185">ключей</span><span class="sxs-lookup"><span data-stu-id="a20cd-185">Keys</span></span>
<span data-ttu-id="a20cd-186">Каждый ключ в hello объекта должно соответствовать hello следующее регулярное выражение:</span><span class="sxs-lookup"><span data-stu-id="a20cd-186">Each key in hello object must match hello following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="a20cd-187">Это означает, что ключ должен содержать не менее одной буквы, за которой следуют буквы, цифры или символы подчеркивания (\_).</span><span class="sxs-lookup"><span data-stu-id="a20cd-187">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="a20cd-188">Размер</span><span class="sxs-lookup"><span data-stu-id="a20cd-188">Size</span></span>
<span data-ttu-id="a20cd-189">Сведения о приложении — ограниченный too1, 024 символов на вызов (после hello Mobile Engagement Web SDK кодирует его в формате JSON).</span><span class="sxs-lookup"><span data-stu-id="a20cd-189">Application information is limited too1,024 characters per call (after hello Mobile Engagement Web SDK encodes it in JSON).</span></span>

<span data-ttu-id="a20cd-190">В предыдущих пример hello hello JSON отправлено toohello server 44 символов:</span><span class="sxs-lookup"><span data-stu-id="a20cd-190">In hello preceding example, hello JSON sent toohello server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
