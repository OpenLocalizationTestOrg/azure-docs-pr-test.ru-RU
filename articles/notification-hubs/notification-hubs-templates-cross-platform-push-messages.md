---
title: "Шаблоны"
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
ms.openlocfilehash: 1ca24a4bf08ecdbe1c1e47a931613144309a04a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="templates"></a><span data-ttu-id="409c4-103">Шаблоны</span><span class="sxs-lookup"><span data-stu-id="409c4-103">Templates</span></span>
## <a name="overview"></a><span data-ttu-id="409c4-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="409c4-104">Overview</span></span>
<span data-ttu-id="409c4-105">Шаблоны позволяют клиентскому приложению определять точный формат уведомлений, которые оно будет получать.</span><span class="sxs-lookup"><span data-stu-id="409c4-105">Templates enable a client application to specify the exact format of the notifications it wants to receive.</span></span> <span data-ttu-id="409c4-106">С помощью шаблонов приложение получает несколько преимуществ, включая следующие:</span><span class="sxs-lookup"><span data-stu-id="409c4-106">Using templates, an app can realize several different benefits, including the following :</span></span>

* <span data-ttu-id="409c4-107">Серверная часть, не зависящая от платформы</span><span class="sxs-lookup"><span data-stu-id="409c4-107">A platform-agnostic backend</span></span>
* <span data-ttu-id="409c4-108">Персонализированные уведомления</span><span class="sxs-lookup"><span data-stu-id="409c4-108">Personalized notifications</span></span>
* <span data-ttu-id="409c4-109">Независимость от версии клиента</span><span class="sxs-lookup"><span data-stu-id="409c4-109">Client-version independence</span></span>
* <span data-ttu-id="409c4-110">Простая локализация</span><span class="sxs-lookup"><span data-stu-id="409c4-110">Easy localization</span></span>

<span data-ttu-id="409c4-111">В этом разделе приводится два подробных примера использования шаблонов для отправки платформонезависимых уведомлений, предназначенных для всех устройств на разных платформах, и для персонализации широковещательного уведомления для каждого устройства.</span><span class="sxs-lookup"><span data-stu-id="409c4-111">This section provides two in-depth examples of how to use templates to send platform-agnostic notifications targeting all your devices across platforms, and to personalize broadcast notification to each device.</span></span>

## <a name="using-templates-cross-platform"></a><span data-ttu-id="409c4-112">Использование шаблонов для разных платформ</span><span class="sxs-lookup"><span data-stu-id="409c4-112">Using templates cross-platform</span></span>
<span data-ttu-id="409c4-113">Стандартный способ отправки push-уведомлений заключается в отправке полезных данных в службу уведомлений платформы (WNS, APNS) для каждого уведомления.</span><span class="sxs-lookup"><span data-stu-id="409c4-113">The standard way to send push notifications is to send, for each notification that is to be sent, a specific payload to platform notification services (WNS, APNS).</span></span> <span data-ttu-id="409c4-114">Например, для отправки предупреждения службе APNS полезными данными будет объект JSON следующего вида:</span><span class="sxs-lookup"><span data-stu-id="409c4-114">For example, to send an alert to APNS, the payload is a Json object of the following form:</span></span>

    {"aps": {"alert" : "Hello!" }}

<span data-ttu-id="409c4-115">Для отправки аналогичного всплывающего сообщения в приложении Магазина Windows полезными данными XML будет:</span><span class="sxs-lookup"><span data-stu-id="409c4-115">To send a similar toast message on a Windows Store application, the XML payload is as follows:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

<span data-ttu-id="409c4-116">Аналогичные полезные данные можно создавать для платформ MPNS (Windows Phone) и GCM (Android).</span><span class="sxs-lookup"><span data-stu-id="409c4-116">You can create similar payloads for MPNS (Windows Phone) and GCM (Android) platforms.</span></span>

<span data-ttu-id="409c4-117">Это требование заставляет серверную часть приложения формировать разные полезные данные для каждой платформы, а также возлагает на нее ответственность за часть уровня представления данных в приложении.</span><span class="sxs-lookup"><span data-stu-id="409c4-117">This requirement forces the app backend to produce different payloads for each platform, and effectively makes the backend responsible for part of the presentation layer of the app.</span></span> <span data-ttu-id="409c4-118">К некоторым вопросам относятся локализация и графические макеты (особенно для приложений Магазина Windows, которые содержат уведомления для плиток различных типов).</span><span class="sxs-lookup"><span data-stu-id="409c4-118">Some concerns include localization and graphical layouts (especially for Windows Store apps that include notifications for various types of tiles).</span></span>

<span data-ttu-id="409c4-119">Шаблон центра уведомлений позволяет клиентскому приложению создавать специальные регистрации (называются шаблонными регистрациями), которые содержат не только набор тегов, но и шаблон.</span><span class="sxs-lookup"><span data-stu-id="409c4-119">The Notification Hubs template feature enables a client app to create special registrations, called template registrations, which include, in addition to the set of tags, a template.</span></span> <span data-ttu-id="409c4-120">Шаблон центра уведомлений позволяет клиентскому приложению связывать устройства с шаблонами, независимо от того, работаете ли вы с установкой (рекомендуется) или регистрацией.</span><span class="sxs-lookup"><span data-stu-id="409c4-120">The Notification Hubs template feature enables a client app to associate devices with templates whether you are working with Installations (preferred) or Registrations.</span></span> <span data-ttu-id="409c4-121">В предыдущих примерах полезных данных единственным фрагментом, не зависящим от платформы, является само сообщение "Hello!".</span><span class="sxs-lookup"><span data-stu-id="409c4-121">Given the preceding payload examples, the only platform-independent information is the actual alert message (Hello!).</span></span> <span data-ttu-id="409c4-122">Шаблон — это набор инструкций для центра уведомлений о форматировании платформонезависимых сообщений для регистрации конкретного клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="409c4-122">A template is a set of instructions for the Notification Hub on how to format a platform-independent message for the registration of that specific client app.</span></span> <span data-ttu-id="409c4-123">В предыдущем примере платформонезависимым сообщением является одно свойство: **message = Hello!**.</span><span class="sxs-lookup"><span data-stu-id="409c4-123">In the preceding example, the platform independent message is a single property: **message = Hello!**.</span></span>

<span data-ttu-id="409c4-124">На следующем рисунке показана схема работы.</span><span class="sxs-lookup"><span data-stu-id="409c4-124">The following picture illustrates the above process:</span></span>

![](./media/notification-hubs-templates/notification-hubs-hello.png)

<span data-ttu-id="409c4-125">Шаблон для регистрации клиентского приложения iOS выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="409c4-125">The template for the iOS client app registration is as follows:</span></span>

    {"aps": {"alert": "$(message)"}}

<span data-ttu-id="409c4-126">Соответствующий шаблон для клиентского приложения Магазина Windows:</span><span class="sxs-lookup"><span data-stu-id="409c4-126">The corresponding template for the Windows Store client app is:</span></span>

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

<span data-ttu-id="409c4-127">Обратите внимание, что фактическое сообщение меняется на выражение $(message).</span><span class="sxs-lookup"><span data-stu-id="409c4-127">Notice that the actual message is substituted for the expression $(message).</span></span> <span data-ttu-id="409c4-128">Это выражение предписывает центру уведомлений всякий раз, когда он отправляет сообщение для данной регистрации, создавать сообщение в соответствии с этим выражением и параметрами из общего значения.</span><span class="sxs-lookup"><span data-stu-id="409c4-128">This expression instructs the Notification Hub, whenever it sends a message to this particular registration, to build a message that follows it and switches in the common value.</span></span>

<span data-ttu-id="409c4-129">При работе с установками ключ "шаблона" установки содержит объект JSON для нескольких шаблонов.</span><span class="sxs-lookup"><span data-stu-id="409c4-129">If you are working with Installation model, the installation “templates” key holds a JSON of multiple templates.</span></span> <span data-ttu-id="409c4-130">При работе с регистрациями клиентское приложение может создавать несколько регистраций для использования нескольких шаблонов. Например, шаблон для предупреждений и шаблон для обновления плиток.</span><span class="sxs-lookup"><span data-stu-id="409c4-130">If you are working with Registration model, the client application can create multiple registrations in order to use multiple templates; for example, a template for alert messages and a template for tile updates.</span></span> <span data-ttu-id="409c4-131">Клиентские приложения также могут использовать комбинацию собственных регистраций (регистраций без шаблона) и регистраций с шаблонами.</span><span class="sxs-lookup"><span data-stu-id="409c4-131">Client applications can also mix native registrations (registrations with no template) and template registrations.</span></span>

<span data-ttu-id="409c4-132">Центр уведомлений отправляет одно уведомление для каждого шаблона, не учитывая, принадлежат ли они одному клиентскому приложению.</span><span class="sxs-lookup"><span data-stu-id="409c4-132">The Notification Hub sends one notification for each template without considering whether they belong to the same client app.</span></span> <span data-ttu-id="409c4-133">Это поведение может использоваться для преобразования платформонезависимых уведомлений в серию уведомлений.</span><span class="sxs-lookup"><span data-stu-id="409c4-133">This behavior can be used to translate platform-independent notifications into more notifications.</span></span> <span data-ttu-id="409c4-134">Например, одно платформонезависимое сообщение для центра уведомлений может быть автоматически преобразовано во всплывающее предупреждение и обновление плитки, не требуя участия серверной части.</span><span class="sxs-lookup"><span data-stu-id="409c4-134">For example, the same platform independent message to the Notification Hub can be seamlessly translated in a toast alert and a tile update, without requiring the backend to be aware of it.</span></span> <span data-ttu-id="409c4-135">Обратите внимание, что некоторые платформы (например iOS) могут сворачивать несколько уведомлений для одного устройства, если они отправляются в течение короткого периода времени.</span><span class="sxs-lookup"><span data-stu-id="409c4-135">Note that some platforms (for example, iOS) might collapse multiple notifications to the same device if they are sent in a short period of time.</span></span>

## <a name="using-templates-for-personalization"></a><span data-ttu-id="409c4-136">Использование шаблонов для персонализации</span><span class="sxs-lookup"><span data-stu-id="409c4-136">Using templates for personalization</span></span>
<span data-ttu-id="409c4-137">Еще одним преимуществом использования шаблонов является возможность использования центров уведомлений для персонализации уведомлений по отдельным регистрациям.</span><span class="sxs-lookup"><span data-stu-id="409c4-137">Another advantage to using templates is the ability to use Notification Hubs to perform per-registration personalization of notifications.</span></span> <span data-ttu-id="409c4-138">Например, рассмотрим погодное приложение, которое отображает плитку с погодными условиями в определенном месте.</span><span class="sxs-lookup"><span data-stu-id="409c4-138">For example, consider a weather app that displays a tile with the weather conditions at a specific location.</span></span> <span data-ttu-id="409c4-139">Пользователь может выбрать между отображением градусов Цельсия или Фаренгейта и прогноз на один или на пять дней.</span><span class="sxs-lookup"><span data-stu-id="409c4-139">A user can choose between Celsius or Fahrenheit degrees, and a single or five-day forecast.</span></span> <span data-ttu-id="409c4-140">С помощью шаблонов каждая установка клиентского приложения может зарегистрировать необходимый для себя формат (1 день и шкала Цельсия, 1 день и шкала Фаренгейта, 5 дней и шкала Цельсия, 5 дней и шкала Фаренгейта), а его серверная часть будет отправлять одно сообщение со всеми данными, необходимыми для заполнения шаблонов (например, пятидневный прогноз с градусами Цельсия и Фаренгейта).</span><span class="sxs-lookup"><span data-stu-id="409c4-140">Using templates, each client app installation can register for the format required (1-day Celsius, 1-day Fahrenheit, 5-days Celsius, 5-days Fahrenheit), and have the backend send a single message that contains all the information required to fill those templates (for example, a five-day forecast with Celsius and Fahrenheit degrees).</span></span>

<span data-ttu-id="409c4-141">Шаблон для прогноза погоды на один день и шкалой Цельсия выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="409c4-141">The template for the one-day forecast with Celsius temperatures is as follows:</span></span>

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

<span data-ttu-id="409c4-142">Сообщение, отправляемое в центр уведомлений, содержит следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="409c4-142">The message sent to the Notification Hub contains all the following properties:</span></span>

<table border="1">

<tr><td><span data-ttu-id="409c4-143">day1_image</span><span class="sxs-lookup"><span data-stu-id="409c4-143">day1_image</span></span></td><td><span data-ttu-id="409c4-144">day2_image</span><span class="sxs-lookup"><span data-stu-id="409c4-144">day2_image</span></span></td><td><span data-ttu-id="409c4-145">day3_image</span><span class="sxs-lookup"><span data-stu-id="409c4-145">day3_image</span></span></td><td><span data-ttu-id="409c4-146">day4_image</span><span class="sxs-lookup"><span data-stu-id="409c4-146">day4_image</span></span></td><td><span data-ttu-id="409c4-147">day5_image</span><span class="sxs-lookup"><span data-stu-id="409c4-147">day5_image</span></span></td></tr>

<tr><td><span data-ttu-id="409c4-148">day1_tempC</span><span class="sxs-lookup"><span data-stu-id="409c4-148">day1_tempC</span></span></td><td><span data-ttu-id="409c4-149">day2_tempC</span><span class="sxs-lookup"><span data-stu-id="409c4-149">day2_tempC</span></span></td><td><span data-ttu-id="409c4-150">day3_tempC</span><span class="sxs-lookup"><span data-stu-id="409c4-150">day3_tempC</span></span></td><td><span data-ttu-id="409c4-151">day4_tempC</span><span class="sxs-lookup"><span data-stu-id="409c4-151">day4_tempC</span></span></td><td><span data-ttu-id="409c4-152">day5_tempC</span><span class="sxs-lookup"><span data-stu-id="409c4-152">day5_tempC</span></span></td></tr>

<tr><td><span data-ttu-id="409c4-153">day1_tempF</span><span class="sxs-lookup"><span data-stu-id="409c4-153">day1_tempF</span></span></td><td><span data-ttu-id="409c4-154">day2_tempF</span><span class="sxs-lookup"><span data-stu-id="409c4-154">day2_tempF</span></span></td><td><span data-ttu-id="409c4-155">day3_tempF</span><span class="sxs-lookup"><span data-stu-id="409c4-155">day3_tempF</span></span></td><td><span data-ttu-id="409c4-156">day4_tempF</span><span class="sxs-lookup"><span data-stu-id="409c4-156">day4_tempF</span></span></td><td><span data-ttu-id="409c4-157">day5_tempF</span><span class="sxs-lookup"><span data-stu-id="409c4-157">day5_tempF</span></span></td></tr>
</table><br/>

<span data-ttu-id="409c4-158">С помощью этого шаблона серверная часть отправляет только одно сообщение без необходимости хранить персональные параметры для пользователей приложения.</span><span class="sxs-lookup"><span data-stu-id="409c4-158">By using this pattern, the backend only sends a single message without having to store specific personalization options for the app users.</span></span> <span data-ttu-id="409c4-159">На следующем рисунке показана схема работы.</span><span class="sxs-lookup"><span data-stu-id="409c4-159">The following picture illustrates this scenario:</span></span>

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-to-register-templates"></a><span data-ttu-id="409c4-160">Регистрация шаблонов</span><span class="sxs-lookup"><span data-stu-id="409c4-160">How to register templates</span></span>
<span data-ttu-id="409c4-161">Регистрация шаблонов с помощью механизма установок (рекомендуется) или регистраций описывается в статье [Управления регистрацией](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="409c4-161">To register with templates using the Installation model (preferred), or the Registration model, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

## <a name="template-expression-language"></a><span data-ttu-id="409c4-162">Язык выражений шаблонов</span><span class="sxs-lookup"><span data-stu-id="409c4-162">Template expression language</span></span>
<span data-ttu-id="409c4-163">В шаблоны можно использовать только форматы документов XML или JSON.</span><span class="sxs-lookup"><span data-stu-id="409c4-163">Templates are limited to XML or JSON document formats.</span></span> <span data-ttu-id="409c4-164">Кроме того, выражения можно размещать только в определенных местах. Например, атрибуты узла или значения для XML и значения строковых свойств для JSON.</span><span class="sxs-lookup"><span data-stu-id="409c4-164">Also, you can only place expressions in particular places; for example, node attributes or values for XML, string property values for JSON.</span></span>

<span data-ttu-id="409c4-165">В следующей таблице показан синтаксис, используемый в шаблонах:</span><span class="sxs-lookup"><span data-stu-id="409c4-165">The following table shows the language allowed in templates:</span></span>

| <span data-ttu-id="409c4-166">Выражение</span><span class="sxs-lookup"><span data-stu-id="409c4-166">Expression</span></span> | <span data-ttu-id="409c4-167">Описание</span><span class="sxs-lookup"><span data-stu-id="409c4-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="409c4-168">$(prop)</span><span class="sxs-lookup"><span data-stu-id="409c4-168">$(prop)</span></span> |<span data-ttu-id="409c4-169">Ссылка на свойство события с заданным именем.</span><span class="sxs-lookup"><span data-stu-id="409c4-169">Reference to an event property with the given name.</span></span> <span data-ttu-id="409c4-170">В именах свойств регистр не учитывается.</span><span class="sxs-lookup"><span data-stu-id="409c4-170">Property names are not case-sensitive.</span></span> <span data-ttu-id="409c4-171">Значением этого выражения является текстовое значение свойства или пустая строка, если свойство не существует.</span><span class="sxs-lookup"><span data-stu-id="409c4-171">This expression resolves into the property’s text value or into an empty string if the property is not present.</span></span> |
| <span data-ttu-id="409c4-172">$(prop, n)</span><span class="sxs-lookup"><span data-stu-id="409c4-172">$(prop, n)</span></span> |<span data-ttu-id="409c4-173">То же, что выше, но текст обрезается до n символов, например, выражение $(title, 20) сокращает содержимое свойства title до 20 символов.</span><span class="sxs-lookup"><span data-stu-id="409c4-173">As above, but the text is explicitly clipped at n characters, for example $(title, 20) clips the contents of the title property at 20 characters.</span></span> |
| <span data-ttu-id="409c4-174">.(prop, n)</span><span class="sxs-lookup"><span data-stu-id="409c4-174">.(prop, n)</span></span> |<span data-ttu-id="409c4-175">То же, что выше, но к тексту добавляются три точки, поскольку он является сокращенным.</span><span class="sxs-lookup"><span data-stu-id="409c4-175">As above, but the text is suffixed with three dots as it is clipped.</span></span> <span data-ttu-id="409c4-176">Общий размер сокращенной строки и суффикса не превышает n символов.</span><span class="sxs-lookup"><span data-stu-id="409c4-176">The total size of the clipped string and the suffix does not exceed n characters.</span></span> <span data-ttu-id="409c4-177">(title, 20) с исходным свойством "Это строка заголовка" превращается в **Это строка заголо...**</span><span class="sxs-lookup"><span data-stu-id="409c4-177">.(title, 20) with an input property of “This is the title line” results in **This is the title...**</span></span> |
| <span data-ttu-id="409c4-178">%(prop)</span><span class="sxs-lookup"><span data-stu-id="409c4-178">%(prop)</span></span> |<span data-ttu-id="409c4-179">Аналогично $(name), за исключением того, что выходные данные имеют формат URI.</span><span class="sxs-lookup"><span data-stu-id="409c4-179">Similar to $(name) except that the output is URI-encoded.</span></span> |
| <span data-ttu-id="409c4-180">#(prop)</span><span class="sxs-lookup"><span data-stu-id="409c4-180">#(prop)</span></span> |<span data-ttu-id="409c4-181">Используется в шаблонах JSON (например, для шаблонов iOS и Android).</span><span class="sxs-lookup"><span data-stu-id="409c4-181">Used in JSON templates (for example, for iOS and Android templates).</span></span><br><br><span data-ttu-id="409c4-182">Это выражение работает так же, как $(prop), указанное выше, за исключением случаев использования в шаблонах JSON (например, в шаблонах Apple).</span><span class="sxs-lookup"><span data-stu-id="409c4-182">This function works exactly the same as $(prop) previously specified, except when used in JSON templates (for example, Apple templates).</span></span> <span data-ttu-id="409c4-183">В этом случае, если функция не заключена в "{‘,’}" (например, ‘myJsonProperty’ : ‘#(name)’) и имеет значением число в формате Javascript, например регулярное выражение (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, то результат JSON является числом.</span><span class="sxs-lookup"><span data-stu-id="409c4-183">In this case, if this function is not surrounded by “{‘,’}” (for example, ‘myJsonProperty’ : ‘#(name)’), and it evaluates to a number in Javascript format, for example, regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, then the output JSON is a number.</span></span><br><br><span data-ttu-id="409c4-184">Например ‘badge : ‘#(name)’ становится ‘badge’ : 40 (а не ‘40‘).</span><span class="sxs-lookup"><span data-stu-id="409c4-184">For example, ‘badge : ‘#(name)’ becomes ‘badge’ : 40 (and not ‘40‘).</span></span> |
| <span data-ttu-id="409c4-185">‘text’ или “text”</span><span class="sxs-lookup"><span data-stu-id="409c4-185">‘text’ or “text”</span></span> |<span data-ttu-id="409c4-186">Литерал.</span><span class="sxs-lookup"><span data-stu-id="409c4-186">A literal.</span></span> <span data-ttu-id="409c4-187">Литералы содержат произвольный текст, заключенный в одинарные или двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="409c4-187">Literals contain arbitrary text enclosed in single or double quotes.</span></span> |
| <span data-ttu-id="409c4-188">expr1 + expr2</span><span class="sxs-lookup"><span data-stu-id="409c4-188">expr1 + expr2</span></span> |<span data-ttu-id="409c4-189">Оператор объединения, объединяющий два выражения в одну строку.</span><span class="sxs-lookup"><span data-stu-id="409c4-189">The concatenation operator joining two expressions into a single string.</span></span> |

<span data-ttu-id="409c4-190">Выражения могут быть любого из перечисленных выше видов.</span><span class="sxs-lookup"><span data-stu-id="409c4-190">The expressions can be any of the preceding forms.</span></span>

<span data-ttu-id="409c4-191">При использовании конкатенации все выражение должно быть заключено в фигурные кавычки {}.</span><span class="sxs-lookup"><span data-stu-id="409c4-191">When using concatenation, the entire expression must be surrounded with {}.</span></span> <span data-ttu-id="409c4-192">Например, {$(prop) + ‘ - ’ + $(prop2)}.</span><span class="sxs-lookup"><span data-stu-id="409c4-192">For example, {$(prop) + ‘ - ’ + $(prop2)}.</span></span> |

<span data-ttu-id="409c4-193">Например, ниже представлен недопустимый шаблон XML:</span><span class="sxs-lookup"><span data-stu-id="409c4-193">For example, the following is not a valid XML template:</span></span>

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


<span data-ttu-id="409c4-194">Как было сказано выше, при использовании конкатенации выражения должны быть заключены в фигурные скобки.</span><span class="sxs-lookup"><span data-stu-id="409c4-194">As explained above, when using concatenation, expressions must be wrapped in curly brackets.</span></span> <span data-ttu-id="409c4-195">Например:</span><span class="sxs-lookup"><span data-stu-id="409c4-195">For example:</span></span>

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

