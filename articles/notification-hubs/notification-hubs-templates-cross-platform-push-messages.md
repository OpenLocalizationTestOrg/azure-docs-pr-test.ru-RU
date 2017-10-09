---
title: aaaTemplates
description: "В этом разделе описываются шаблоны для центров уведомлений Azure."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: a41897bb-5b4b-48b2-bfd5-2e3c65edc37e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 0149f0c7473e5a4b952905bc8217582b58db2a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="templates"></a><span data-ttu-id="04589-103">Шаблоны</span><span class="sxs-lookup"><span data-stu-id="04589-103">Templates</span></span>
## <a name="overview"></a><span data-ttu-id="04589-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="04589-104">Overview</span></span>
<span data-ttu-id="04589-105">Шаблоны включают клиента toospecify hello точное формате приложения hello уведомлений, что ему нужны tooreceive.</span><span class="sxs-lookup"><span data-stu-id="04589-105">Templates enable a client application toospecify hello exact format of hello notifications it wants tooreceive.</span></span> <span data-ttu-id="04589-106">С помощью шаблонов, приложения могут использовать несколько разных преимуществ, включая hello следующее:</span><span class="sxs-lookup"><span data-stu-id="04589-106">Using templates, an app can realize several different benefits, including hello following :</span></span>

* <span data-ttu-id="04589-107">Серверная часть, не зависящая от платформы</span><span class="sxs-lookup"><span data-stu-id="04589-107">A platform-agnostic backend</span></span>
* <span data-ttu-id="04589-108">Персонализированные уведомления</span><span class="sxs-lookup"><span data-stu-id="04589-108">Personalized notifications</span></span>
* <span data-ttu-id="04589-109">Независимость от версии клиента</span><span class="sxs-lookup"><span data-stu-id="04589-109">Client-version independence</span></span>
* <span data-ttu-id="04589-110">Простая локализация</span><span class="sxs-lookup"><span data-stu-id="04589-110">Easy localization</span></span>

<span data-ttu-id="04589-111">В этом разделе примеры двух подробные как toouse toosend шаблоны платформенно независимые уведомления, предназначенных для всех устройств на платформах и toopersonalize широковещательных tooeach устройства создания уведомлений.</span><span class="sxs-lookup"><span data-stu-id="04589-111">This section provides two in-depth examples of how toouse templates toosend platform-agnostic notifications targeting all your devices across platforms, and toopersonalize broadcast notification tooeach device.</span></span>

## <a name="using-templates-cross-platform"></a><span data-ttu-id="04589-112">Использование шаблонов для разных платформ</span><span class="sxs-lookup"><span data-stu-id="04589-112">Using templates cross-platform</span></span>
<span data-ttu-id="04589-113">стандартный способ toosend Hello push-уведомления — toosend для каждого из уведомлений, отправленных toobe полезной нагрузки tooplatform служб notification services (WNS, APNS).</span><span class="sxs-lookup"><span data-stu-id="04589-113">hello standard way toosend push notifications is toosend, for each notification that is toobe sent, a specific payload tooplatform notification services (WNS, APNS).</span></span> <span data-ttu-id="04589-114">Для примера toosend предупреждения tooAPNS hello полезных данных является объект Json hello следующие формы:</span><span class="sxs-lookup"><span data-stu-id="04589-114">For example, toosend an alert tooAPNS, hello payload is a Json object of hello following form:</span></span>

    {"aps": {"alert" : "Hello!" }}

<span data-ttu-id="04589-115">toosend похожее сообщение извещения на приложения для магазина Windows hello полезные данные XML выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04589-115">toosend a similar toast message on a Windows Store application, hello XML payload is as follows:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

<span data-ttu-id="04589-116">Аналогичные полезные данные можно создавать для платформ MPNS (Windows Phone) и GCM (Android).</span><span class="sxs-lookup"><span data-stu-id="04589-116">You can create similar payloads for MPNS (Windows Phone) and GCM (Android) platforms.</span></span>

<span data-ttu-id="04589-117">Это требование заставляет hello приложения серверной tooproduce различных полезных данных для каждой платформы и фактически делает серверной hello ответственность за частью уровень представления hello приложение hello.</span><span class="sxs-lookup"><span data-stu-id="04589-117">This requirement forces hello app backend tooproduce different payloads for each platform, and effectively makes hello backend responsible for part of hello presentation layer of hello app.</span></span> <span data-ttu-id="04589-118">К некоторым вопросам относятся локализация и графические макеты (особенно для приложений Магазина Windows, которые содержат уведомления для плиток различных типов).</span><span class="sxs-lookup"><span data-stu-id="04589-118">Some concerns include localization and graphical layouts (especially for Windows Store apps that include notifications for various types of tiles).</span></span>

<span data-ttu-id="04589-119">функция шаблона Hello концентраторы уведомлений позволяет клиентского приложения toocreate специальные регистраций, вызывается регистрации шаблонов, которые включают, кроме toohello набор тегов, шаблон.</span><span class="sxs-lookup"><span data-stu-id="04589-119">hello Notification Hubs template feature enables a client app toocreate special registrations, called template registrations, which include, in addition toohello set of tags, a template.</span></span> <span data-ttu-id="04589-120">Hello концентраторы уведомлений шаблона позволяет клиентских устройств tooassociate приложения с шаблонами ли вы работаете с установок (предпочтительно) или регистраций.</span><span class="sxs-lookup"><span data-stu-id="04589-120">hello Notification Hubs template feature enables a client app tooassociate devices with templates whether you are working with Installations (preferred) or Registrations.</span></span> <span data-ttu-id="04589-121">Hello в предыдущих примерах полезных данных, hello только сведения, независимый от платформы является фактический предупреждающее сообщение hello (Привет!).</span><span class="sxs-lookup"><span data-stu-id="04589-121">Given hello preceding payload examples, hello only platform-independent information is hello actual alert message (Hello!).</span></span> <span data-ttu-id="04589-122">Шаблон — это набор инструкций для hello концентратора уведомлений на как tooformat зависящим от платформы сообщений для регистрации этого конкретного клиентского приложения hello.</span><span class="sxs-lookup"><span data-stu-id="04589-122">A template is a set of instructions for hello Notification Hub on how tooformat a platform-independent message for hello registration of that specific client app.</span></span> <span data-ttu-id="04589-123">В предыдущих пример hello, независимые сообщение hello платформы является одно свойство: **сообщения = Hello!**.</span><span class="sxs-lookup"><span data-stu-id="04589-123">In hello preceding example, hello platform independent message is a single property: **message = Hello!**.</span></span>

<span data-ttu-id="04589-124">Hello следующий рисунок иллюстрирует hello выше процесс:</span><span class="sxs-lookup"><span data-stu-id="04589-124">hello following picture illustrates hello above process:</span></span>

![](./media/notification-hubs-templates/notification-hubs-hello.png)

<span data-ttu-id="04589-125">Hello шаблон для регистрации клиентского приложения hello iOS выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04589-125">hello template for hello iOS client app registration is as follows:</span></span>

    {"aps": {"alert": "$(message)"}}

<span data-ttu-id="04589-126">— Hello соответствующего шаблона для клиентского приложения для магазина Windows hello:</span><span class="sxs-lookup"><span data-stu-id="04589-126">hello corresponding template for hello Windows Store client app is:</span></span>

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

<span data-ttu-id="04589-127">Обратите внимание, что фактическое сообщение hello будет подставляться выражение hello $(сообщение).</span><span class="sxs-lookup"><span data-stu-id="04589-127">Notice that hello actual message is substituted for hello expression $(message).</span></span> <span data-ttu-id="04589-128">Это выражение указывает, что hello концентратора уведомлений при каждой отправке toothis сообщения определенного регистрации, toobuild сообщение, которое соответствует ее и коммутаторов в общее значение hello.</span><span class="sxs-lookup"><span data-stu-id="04589-128">This expression instructs hello Notification Hub, whenever it sends a message toothis particular registration, toobuild a message that follows it and switches in hello common value.</span></span>

<span data-ttu-id="04589-129">При работе с моделью установки hello установочный ключ «шаблоны» содержит JSON несколько шаблонов.</span><span class="sxs-lookup"><span data-stu-id="04589-129">If you are working with Installation model, hello installation “templates” key holds a JSON of multiple templates.</span></span> <span data-ttu-id="04589-130">При работе с моделью регистрации клиентского приложения hello можно создать несколько регистраций в порядке toouse несколько шаблонов; Например шаблон для предупреждающих сообщений и шаблон для обновления плитки.</span><span class="sxs-lookup"><span data-stu-id="04589-130">If you are working with Registration model, hello client application can create multiple registrations in order toouse multiple templates; for example, a template for alert messages and a template for tile updates.</span></span> <span data-ttu-id="04589-131">Клиентские приложения также могут использовать комбинацию собственных регистраций (регистраций без шаблона) и регистраций с шаблонами.</span><span class="sxs-lookup"><span data-stu-id="04589-131">Client applications can also mix native registrations (registrations with no template) and template registrations.</span></span>

<span data-ttu-id="04589-132">Hello концентратора уведомлений отправляет одно уведомление для каждого шаблона без учета того, принадлежат ли они toohello того же клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="04589-132">hello Notification Hub sends one notification for each template without considering whether they belong toohello same client app.</span></span> <span data-ttu-id="04589-133">Это поведение может быть уведомлений используется tootranslate независимая от платформы в дополнительные уведомления.</span><span class="sxs-lookup"><span data-stu-id="04589-133">This behavior can be used tootranslate platform-independent notifications into more notifications.</span></span> <span data-ttu-id="04589-134">Например, hello же toohello независимыми сообщение платформы, которые концентратор уведомлений можно легко преобразовать в предупреждении всплывающих и обновление плитки, не требуя hello известна toobe серверной части.</span><span class="sxs-lookup"><span data-stu-id="04589-134">For example, hello same platform independent message toohello Notification Hub can be seamlessly translated in a toast alert and a tile update, without requiring hello backend toobe aware of it.</span></span> <span data-ttu-id="04589-135">Обратите внимание, что некоторые платформы (например, iOS) могут свернуть несколько уведомлений toohello одного устройства, если они отправляются за короткий период времени.</span><span class="sxs-lookup"><span data-stu-id="04589-135">Note that some platforms (for example, iOS) might collapse multiple notifications toohello same device if they are sent in a short period of time.</span></span>

## <a name="using-templates-for-personalization"></a><span data-ttu-id="04589-136">Использование шаблонов для персонализации</span><span class="sxs-lookup"><span data-stu-id="04589-136">Using templates for personalization</span></span>
<span data-ttu-id="04589-137">Другое преимущество toousing шаблонов — toouse hello возможности персонализации регистрации концентраторов уведомлений tooperform уведомлений.</span><span class="sxs-lookup"><span data-stu-id="04589-137">Another advantage toousing templates is hello ability toouse Notification Hubs tooperform per-registration personalization of notifications.</span></span> <span data-ttu-id="04589-138">Например рассмотрим приложение погоды, которое отображает плитки с hello погодных условий в указанное местоположение.</span><span class="sxs-lookup"><span data-stu-id="04589-138">For example, consider a weather app that displays a tile with hello weather conditions at a specific location.</span></span> <span data-ttu-id="04589-139">Пользователь может выбрать между отображением градусов Цельсия или Фаренгейта и прогноз на один или на пять дней.</span><span class="sxs-lookup"><span data-stu-id="04589-139">A user can choose between Celsius or Fahrenheit degrees, and a single or five-day forecast.</span></span> <span data-ttu-id="04589-140">С помощью шаблонов, каждая установка приложения клиента можно зарегистрировать для hello формат, требуемый (1 день Цельсия, 1 день Фаренгейта, 5 дней Цельсия 5 дней фаренгейт), и отправить одно сообщение, содержащий сведения обо всех hello необходимые toofill те серверной hello шаблоны (например, пять дней прогноз с градусы Цельсия или Фаренгейта).</span><span class="sxs-lookup"><span data-stu-id="04589-140">Using templates, each client app installation can register for hello format required (1-day Celsius, 1-day Fahrenheit, 5-days Celsius, 5-days Fahrenheit), and have hello backend send a single message that contains all hello information required toofill those templates (for example, a five-day forecast with Celsius and Fahrenheit degrees).</span></span>

<span data-ttu-id="04589-141">шаблон Hello для hello один день с Цельсию прогноза температуры выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04589-141">hello template for hello one-day forecast with Celsius temperatures is as follows:</span></span>

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

<span data-ttu-id="04589-142">сообщение, отправленное Hello toohello концентратора уведомлений содержит все hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="04589-142">hello message sent toohello Notification Hub contains all hello following properties:</span></span>

<table border="1">

<tr><td><span data-ttu-id="04589-143">day1_image</span><span class="sxs-lookup"><span data-stu-id="04589-143">day1_image</span></span></td><td><span data-ttu-id="04589-144">day2_image</span><span class="sxs-lookup"><span data-stu-id="04589-144">day2_image</span></span></td><td><span data-ttu-id="04589-145">day3_image</span><span class="sxs-lookup"><span data-stu-id="04589-145">day3_image</span></span></td><td><span data-ttu-id="04589-146">day4_image</span><span class="sxs-lookup"><span data-stu-id="04589-146">day4_image</span></span></td><td><span data-ttu-id="04589-147">day5_image</span><span class="sxs-lookup"><span data-stu-id="04589-147">day5_image</span></span></td></tr>

<tr><td><span data-ttu-id="04589-148">day1_tempC</span><span class="sxs-lookup"><span data-stu-id="04589-148">day1_tempC</span></span></td><td><span data-ttu-id="04589-149">day2_tempC</span><span class="sxs-lookup"><span data-stu-id="04589-149">day2_tempC</span></span></td><td><span data-ttu-id="04589-150">day3_tempC</span><span class="sxs-lookup"><span data-stu-id="04589-150">day3_tempC</span></span></td><td><span data-ttu-id="04589-151">day4_tempC</span><span class="sxs-lookup"><span data-stu-id="04589-151">day4_tempC</span></span></td><td><span data-ttu-id="04589-152">day5_tempC</span><span class="sxs-lookup"><span data-stu-id="04589-152">day5_tempC</span></span></td></tr>

<tr><td><span data-ttu-id="04589-153">day1_tempF</span><span class="sxs-lookup"><span data-stu-id="04589-153">day1_tempF</span></span></td><td><span data-ttu-id="04589-154">day2_tempF</span><span class="sxs-lookup"><span data-stu-id="04589-154">day2_tempF</span></span></td><td><span data-ttu-id="04589-155">day3_tempF</span><span class="sxs-lookup"><span data-stu-id="04589-155">day3_tempF</span></span></td><td><span data-ttu-id="04589-156">day4_tempF</span><span class="sxs-lookup"><span data-stu-id="04589-156">day4_tempF</span></span></td><td><span data-ttu-id="04589-157">day5_tempF</span><span class="sxs-lookup"><span data-stu-id="04589-157">day5_tempF</span></span></td></tr>
</table><br/>

<span data-ttu-id="04589-158">Используя этот шаблон, серверной hello только отправляет одно сообщение без необходимости toostore параметры конкретного персонализации для пользователей приложения hello.</span><span class="sxs-lookup"><span data-stu-id="04589-158">By using this pattern, hello backend only sends a single message without having toostore specific personalization options for hello app users.</span></span> <span data-ttu-id="04589-159">Hello следующий рисунок иллюстрирует этот сценарий:</span><span class="sxs-lookup"><span data-stu-id="04589-159">hello following picture illustrates this scenario:</span></span>

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-tooregister-templates"></a><span data-ttu-id="04589-160">Как tooregister шаблонов</span><span class="sxs-lookup"><span data-stu-id="04589-160">How tooregister templates</span></span>
<span data-ttu-id="04589-161">tooregister с шаблонами, с помощью модели установки hello (предпочтительно) или hello модель регистрации в разделе [управления регистрацией](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="04589-161">tooregister with templates using hello Installation model (preferred), or hello Registration model, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

## <a name="template-expression-language"></a><span data-ttu-id="04589-162">Язык выражений шаблонов</span><span class="sxs-lookup"><span data-stu-id="04589-162">Template expression language</span></span>
<span data-ttu-id="04589-163">Шаблоны — это ограниченная tooXML или форматы документов JSON.</span><span class="sxs-lookup"><span data-stu-id="04589-163">Templates are limited tooXML or JSON document formats.</span></span> <span data-ttu-id="04589-164">Кроме того, выражения можно размещать только в определенных местах. Например, атрибуты узла или значения для XML и значения строковых свойств для JSON.</span><span class="sxs-lookup"><span data-stu-id="04589-164">Also, you can only place expressions in particular places; for example, node attributes or values for XML, string property values for JSON.</span></span>

<span data-ttu-id="04589-165">Hello Следующая таблица показывает язык hello в шаблонах.</span><span class="sxs-lookup"><span data-stu-id="04589-165">hello following table shows hello language allowed in templates:</span></span>

| <span data-ttu-id="04589-166">Expression</span><span class="sxs-lookup"><span data-stu-id="04589-166">Expression</span></span> | <span data-ttu-id="04589-167">Описание</span><span class="sxs-lookup"><span data-stu-id="04589-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="04589-168">$(prop)</span><span class="sxs-lookup"><span data-stu-id="04589-168">$(prop)</span></span> |<span data-ttu-id="04589-169">Справочник по tooan свойство события с заданным именем hello.</span><span class="sxs-lookup"><span data-stu-id="04589-169">Reference tooan event property with hello given name.</span></span> <span data-ttu-id="04589-170">В именах свойств регистр не учитывается.</span><span class="sxs-lookup"><span data-stu-id="04589-170">Property names are not case-sensitive.</span></span> <span data-ttu-id="04589-171">Данное выражение равно в свойство hello текстовое значение или пустая строка, если свойство hello отсутствует.</span><span class="sxs-lookup"><span data-stu-id="04589-171">This expression resolves into hello property’s text value or into an empty string if hello property is not present.</span></span> |
| <span data-ttu-id="04589-172">$(prop, n)</span><span class="sxs-lookup"><span data-stu-id="04589-172">$(prop, n)</span></span> |<span data-ttu-id="04589-173">Как описано выше, но hello текст является явным образом обрезается до n символов, например $(название, 20) отсекает hello содержимое свойства title hello до 20 символов.</span><span class="sxs-lookup"><span data-stu-id="04589-173">As above, but hello text is explicitly clipped at n characters, for example $(title, 20) clips hello contents of hello title property at 20 characters.</span></span> |
| <span data-ttu-id="04589-174">.(prop, n)</span><span class="sxs-lookup"><span data-stu-id="04589-174">.(prop, n)</span></span> |<span data-ttu-id="04589-175">Как описано выше, но hello текст добавляется с тремя точками, как оно обрезается.</span><span class="sxs-lookup"><span data-stu-id="04589-175">As above, but hello text is suffixed with three dots as it is clipped.</span></span> <span data-ttu-id="04589-176">общий размер Hello hello усеченные строки и суффикс hello не превышает n символов.</span><span class="sxs-lookup"><span data-stu-id="04589-176">hello total size of hello clipped string and hello suffix does not exceed n characters.</span></span> <span data-ttu-id="04589-177">. (название, 20) с входного свойства «Это строка заголовка hello» при запуске **это заголовок hello...**</span><span class="sxs-lookup"><span data-stu-id="04589-177">.(title, 20) with an input property of “This is hello title line” results in **This is hello title...**</span></span> |
| <span data-ttu-id="04589-178">%(prop)</span><span class="sxs-lookup"><span data-stu-id="04589-178">%(prop)</span></span> |<span data-ttu-id="04589-179">Аналогичные too$(name), за исключением того, выходные данные hello закодированный URI.</span><span class="sxs-lookup"><span data-stu-id="04589-179">Similar too$(name) except that hello output is URI-encoded.</span></span> |
| <span data-ttu-id="04589-180">#(prop)</span><span class="sxs-lookup"><span data-stu-id="04589-180">#(prop)</span></span> |<span data-ttu-id="04589-181">Используется в шаблонах JSON (например, для шаблонов iOS и Android).</span><span class="sxs-lookup"><span data-stu-id="04589-181">Used in JSON templates (for example, for iOS and Android templates).</span></span><br><br><span data-ttu-id="04589-182">Эта функция работает точно hello же, как $(prop) ранее указано, за исключением случаев использования в шаблонах JSON (например, шаблоны Apple).</span><span class="sxs-lookup"><span data-stu-id="04589-182">This function works exactly hello same as $(prop) previously specified, except when used in JSON templates (for example, Apple templates).</span></span> <span data-ttu-id="04589-183">В этом случае, если эта функция не будет окружена «{«,»}» (например, «myJsonProperty»: «#(name)»), и он оценивает tooa число в формате Javascript, например, regexp: (0 &#124; (&#91; 1-9 &#93; &#91; 0-9 & #93 ;*))(\. &#91; 0-9 &#93; +)? ((e &#124; E) (+ &#124;-)? &#91; 0-9 &#93; +)?, то hello выходных данных JSON является числом.</span><span class="sxs-lookup"><span data-stu-id="04589-183">In this case, if this function is not surrounded by “{‘,’}” (for example, ‘myJsonProperty’ : ‘#(name)’), and it evaluates tooa number in Javascript format, for example, regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, then hello output JSON is a number.</span></span><br><br><span data-ttu-id="04589-184">Например ‘badge : ‘#(name)’ становится ‘badge’ : 40 (а не ‘40‘).</span><span class="sxs-lookup"><span data-stu-id="04589-184">For example, ‘badge : ‘#(name)’ becomes ‘badge’ : 40 (and not ‘40‘).</span></span> |
| <span data-ttu-id="04589-185">‘text’ или “text”</span><span class="sxs-lookup"><span data-stu-id="04589-185">‘text’ or “text”</span></span> |<span data-ttu-id="04589-186">Литерал.</span><span class="sxs-lookup"><span data-stu-id="04589-186">A literal.</span></span> <span data-ttu-id="04589-187">Литералы содержат произвольный текст, заключенный в одинарные или двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="04589-187">Literals contain arbitrary text enclosed in single or double quotes.</span></span> |
| <span data-ttu-id="04589-188">expr1 + expr2</span><span class="sxs-lookup"><span data-stu-id="04589-188">expr1 + expr2</span></span> |<span data-ttu-id="04589-189">Оператор объединения Hello объединение двух выражений в одну строку.</span><span class="sxs-lookup"><span data-stu-id="04589-189">hello concatenation operator joining two expressions into a single string.</span></span> |

<span data-ttu-id="04589-190">Hello выражения могут быть любые предшествующие forms hello.</span><span class="sxs-lookup"><span data-stu-id="04589-190">hello expressions can be any of hello preceding forms.</span></span>

<span data-ttu-id="04589-191">При использовании объединения, hello всего выражения должны заключаться в {}.</span><span class="sxs-lookup"><span data-stu-id="04589-191">When using concatenation, hello entire expression must be surrounded with {}.</span></span> <span data-ttu-id="04589-192">Например, {$(prop) + ‘ - ’ + $(prop2)}.</span><span class="sxs-lookup"><span data-stu-id="04589-192">For example, {$(prop) + ‘ - ’ + $(prop2)}.</span></span> |

<span data-ttu-id="04589-193">Например следующие hello не допустимый XML-шаблон:</span><span class="sxs-lookup"><span data-stu-id="04589-193">For example, hello following is not a valid XML template:</span></span>

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


<span data-ttu-id="04589-194">Как было сказано выше, при использовании конкатенации выражения должны быть заключены в фигурные скобки.</span><span class="sxs-lookup"><span data-stu-id="04589-194">As explained above, when using concatenation, expressions must be wrapped in curly brackets.</span></span> <span data-ttu-id="04589-195">Например:</span><span class="sxs-lookup"><span data-stu-id="04589-195">For example:</span></span>

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

