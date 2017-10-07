---
title: "aaaAzure модели данных телеметрии приложения аналитики - контекст телеметрии | Документы Microsoft"
description: "Модель данных контекста телеметрии Application Insights"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/15/2017
ms.author: sergkanz
ms.openlocfilehash: 6cdd6240d1c448f883d104a871ee9d5f6b5af2ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-context-application-insights-data-model"></a><span data-ttu-id="53220-103">Контекст телеметрии: модель данных Application Insights</span><span class="sxs-lookup"><span data-stu-id="53220-103">Telemetry context: Application Insights data model</span></span>

<span data-ttu-id="53220-104">Каждый элемент данных телеметрии может иметь строго типизированные поля контекста.</span><span class="sxs-lookup"><span data-stu-id="53220-104">Every telemetry item may have a strongly typed context fields.</span></span> <span data-ttu-id="53220-105">Каждое поле обеспечивает определенный сценарий мониторинга.</span><span class="sxs-lookup"><span data-stu-id="53220-105">Every field enables a specific monitoring scenario.</span></span> <span data-ttu-id="53220-106">Используйте hello пользовательские свойства коллекции toostore пользовательских или конкретного приложения контекстную информацию.</span><span class="sxs-lookup"><span data-stu-id="53220-106">Use hello custom properties collection toostore custom or application-specific contextual information.</span></span>


##<a name="application-version"></a><span data-ttu-id="53220-107">Версия приложения</span><span class="sxs-lookup"><span data-stu-id="53220-107">Application version</span></span>

<span data-ttu-id="53220-108">Сведения в полях контекст приложения hello всегда связана с hello приложение, отправляющее телеметрии hello.</span><span class="sxs-lookup"><span data-stu-id="53220-108">Information in hello application context fields is always about hello application that is sending hello telemetry.</span></span> <span data-ttu-id="53220-109">Версия приложения, используется tooanalyze тренда изменений в поведение приложения hello и ее развертывания toohello корреляции.</span><span class="sxs-lookup"><span data-stu-id="53220-109">Application version is used tooanalyze trend changes in hello application behavior and its correlation toohello deployments.</span></span>

<span data-ttu-id="53220-110">Максимальная длина: 1024</span><span class="sxs-lookup"><span data-stu-id="53220-110">Max length: 1024</span></span>


##<a name="client-ip-address"></a><span data-ttu-id="53220-111">IP-адрес клиента</span><span class="sxs-lookup"><span data-stu-id="53220-111">Client IP address</span></span>

<span data-ttu-id="53220-112">IP-адрес клиентского устройства hello Hello.</span><span class="sxs-lookup"><span data-stu-id="53220-112">hello IP address of hello client device.</span></span> <span data-ttu-id="53220-113">Поддерживаются протоколы IPv4 и IPv6.</span><span class="sxs-lookup"><span data-stu-id="53220-113">IPv4 and IPv6 are supported.</span></span> <span data-ttu-id="53220-114">При отправке данных телеметрии из службы контексте местоположения hello посвящен hello пользователя, инициировавшего hello операции в службе hello.</span><span class="sxs-lookup"><span data-stu-id="53220-114">When telemetry is sent from a service, hello location context is about hello user that initiated hello operation in hello service.</span></span> <span data-ttu-id="53220-115">Извлечь сведения о географическом регионе hello из IP-адрес клиента hello Application Insights и он усекается.</span><span class="sxs-lookup"><span data-stu-id="53220-115">Application Insights extract hello geo-location information from hello client IP and then truncate it.</span></span> <span data-ttu-id="53220-116">Поэтому IP-адрес клиента сам по себе нельзя использовать как идентификационные данные конечного пользователя.</span><span class="sxs-lookup"><span data-stu-id="53220-116">So client IP by itself cannot be used as end-user identifiable information.</span></span> 

<span data-ttu-id="53220-117">Максимальная длина: 46</span><span class="sxs-lookup"><span data-stu-id="53220-117">Max length: 46</span></span>


##<a name="device-type"></a><span data-ttu-id="53220-118">Тип устройства</span><span class="sxs-lookup"><span data-stu-id="53220-118">Device type</span></span>

<span data-ttu-id="53220-119">Изначально использовался в этом поле используется тип hello tooindicate hello hello устройства конечного пользователя приложения hello.</span><span class="sxs-lookup"><span data-stu-id="53220-119">Originally this field was used tooindicate hello type of hello device hello end user of hello application is using.</span></span> <span data-ttu-id="53220-120">Сегодня используется главным образом toodistinguish JavaScript телеметрии с hello тип устройства «Браузер» телеметрии на стороне сервера с типом устройства hello «Компьютер».</span><span class="sxs-lookup"><span data-stu-id="53220-120">Today used primarily toodistinguish JavaScript telemetry with hello device type 'Browser' from server-side telemetry with hello device type 'PC'.</span></span>

<span data-ttu-id="53220-121">Максимальная длина: 64</span><span class="sxs-lookup"><span data-stu-id="53220-121">Max length: 64</span></span>


##<a name="operation-id"></a><span data-ttu-id="53220-122">Идентификатор операции</span><span class="sxs-lookup"><span data-stu-id="53220-122">Operation id</span></span>

<span data-ttu-id="53220-123">Уникальный идентификатор hello корневой операции.</span><span class="sxs-lookup"><span data-stu-id="53220-123">A unique identifier of hello root operation.</span></span> <span data-ttu-id="53220-124">Этот идентификатор позволяет toogroup телеметрии по нескольким компонентам.</span><span class="sxs-lookup"><span data-stu-id="53220-124">This identifier allows toogroup telemetry across multiple components.</span></span> <span data-ttu-id="53220-125">Подробные сведения см. в статье [Корреляция данных телеметрии](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="53220-125">See [telemetry correlation](application-insights-correlation.md) for details.</span></span> <span data-ttu-id="53220-126">Идентификатор операции Hello создается путем запроса или вид страницы.</span><span class="sxs-lookup"><span data-stu-id="53220-126">hello operation id is created by either a request or a page view.</span></span> <span data-ttu-id="53220-127">Все данные телеметрии задает toohello значение этого поля для hello, содержащей представление запроса или страницы.</span><span class="sxs-lookup"><span data-stu-id="53220-127">All other telemetry sets this field toohello value for hello containing request or page view.</span></span> 

<span data-ttu-id="53220-128">Максимальная длина: 128</span><span class="sxs-lookup"><span data-stu-id="53220-128">Max length: 128</span></span>


##<a name="parent-operation-id"></a><span data-ttu-id="53220-129">Идентификатор родительской операции</span><span class="sxs-lookup"><span data-stu-id="53220-129">Parent operation ID</span></span>

<span data-ttu-id="53220-130">Здравствуйте, уникальный идентификатор элемента телеметрии hello непосредственного родителя.</span><span class="sxs-lookup"><span data-stu-id="53220-130">hello unique identifier of hello telemetry item's immediate parent.</span></span> <span data-ttu-id="53220-131">Подробные сведения см. в статье [Корреляция данных телеметрии](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="53220-131">See [telemetry correlation](application-insights-correlation.md) for details.</span></span>

<span data-ttu-id="53220-132">Максимальная длина: 128</span><span class="sxs-lookup"><span data-stu-id="53220-132">Max length: 128</span></span>


##<a name="operation-name"></a><span data-ttu-id="53220-133">Имя операции</span><span class="sxs-lookup"><span data-stu-id="53220-133">Operation name</span></span>

<span data-ttu-id="53220-134">Имя Hello (группа) hello операции.</span><span class="sxs-lookup"><span data-stu-id="53220-134">hello name (group) of hello operation.</span></span> <span data-ttu-id="53220-135">Имя операции Hello создается путем запроса или вид страницы.</span><span class="sxs-lookup"><span data-stu-id="53220-135">hello operation name is created by either a request or a page view.</span></span> <span data-ttu-id="53220-136">Все прочие элементы телеметрии это значение поля toohello для hello, содержащей представление запроса или страницы.</span><span class="sxs-lookup"><span data-stu-id="53220-136">All other telemetry items set this field toohello value for hello containing request or page view.</span></span> <span data-ttu-id="53220-137">Имя операции, используемое для поиска всех элементов hello телеметрии для группы операций (например «GET Home/Index»).</span><span class="sxs-lookup"><span data-stu-id="53220-137">Operation name is used for finding all hello telemetry items for a group of operations (for example 'GET Home/Index').</span></span> <span data-ttu-id="53220-138">Это свойство контекста является используется tooanswer такие вопросы, как «Каковы hello типичные исключения на этой странице».</span><span class="sxs-lookup"><span data-stu-id="53220-138">This context property is used tooanswer questions like "what are hello typical exceptions thrown on this page."</span></span>

<span data-ttu-id="53220-139">Максимальная длина: 1024</span><span class="sxs-lookup"><span data-stu-id="53220-139">Max length: 1024</span></span>


##<a name="synthetic-source-of-hello-operation"></a><span data-ttu-id="53220-140">Синтетические источник операции hello</span><span class="sxs-lookup"><span data-stu-id="53220-140">Synthetic source of hello operation</span></span>

<span data-ttu-id="53220-141">Имя искусственного источника.</span><span class="sxs-lookup"><span data-stu-id="53220-141">Name of synthetic source.</span></span> <span data-ttu-id="53220-142">Некоторые данные телеметрии из приложения hello может представлять искуственного трафика.</span><span class="sxs-lookup"><span data-stu-id="53220-142">Some telemetry from hello application may represent synthetic traffic.</span></span> <span data-ttu-id="53220-143">Возможно, web программой-обходчиком индексирования hello веб-сайта, тестов доступности сайта или трассировки из диагностики библиотек, таких как пакет SDK для Application Insights сам.</span><span class="sxs-lookup"><span data-stu-id="53220-143">It may be web crawler indexing hello web site, site availability tests, or traces from diagnostic libraries like Application Insights SDK itself.</span></span>

<span data-ttu-id="53220-144">Максимальная длина: 1024</span><span class="sxs-lookup"><span data-stu-id="53220-144">Max length: 1024</span></span>


##<a name="session-id"></a><span data-ttu-id="53220-145">Идентификатор сеанса</span><span class="sxs-lookup"><span data-stu-id="53220-145">Session id</span></span>

<span data-ttu-id="53220-146">Идентификатор сеанса — экземпляр hello взаимодействия hello пользователя с приложение hello.</span><span class="sxs-lookup"><span data-stu-id="53220-146">Session ID - hello instance of hello user's interaction with hello app.</span></span> <span data-ttu-id="53220-147">Сведения в полях контекста сеанса hello всегда связана с hello конечного пользователя.</span><span class="sxs-lookup"><span data-stu-id="53220-147">Information in hello session context fields is always about hello end user.</span></span> <span data-ttu-id="53220-148">При отправке данных телеметрии из службы, контекст сеанса hello посвящен hello пользователя, инициировавшего hello операции в службе hello.</span><span class="sxs-lookup"><span data-stu-id="53220-148">When telemetry is sent from a service, hello session context is about hello user that initiated hello operation in hello service.</span></span>

<span data-ttu-id="53220-149">Максимальная длина: 64</span><span class="sxs-lookup"><span data-stu-id="53220-149">Max length: 64</span></span>


##<a name="anonymous-user-id"></a><span data-ttu-id="53220-150">Идентификатор анонимного пользователя</span><span class="sxs-lookup"><span data-stu-id="53220-150">Anonymous user id</span></span>

<span data-ttu-id="53220-151">Идентификатор анонимного пользователя. Представляет hello конечного пользователя приложения hello.</span><span class="sxs-lookup"><span data-stu-id="53220-151">Anonymous user id. Represents hello end user of hello application.</span></span> <span data-ttu-id="53220-152">При отправке данных телеметрии из службы hello пользовательский контекст — о hello пользователя, инициировавшего hello операции в службе hello.</span><span class="sxs-lookup"><span data-stu-id="53220-152">When telemetry is sent from a service, hello user context is about hello user that initiated hello operation in hello service.</span></span>

<span data-ttu-id="53220-153">[Выборка](app-insights-sampling.md) является одним из hello методы toominimize hello объем собранных данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="53220-153">[Sampling](app-insights-sampling.md) is one of hello techniques toominimize hello amount of collected telemetry.</span></span> <span data-ttu-id="53220-154">Выборка tooeither попыток алгоритм образец in или out все hello связаны телеметрии.</span><span class="sxs-lookup"><span data-stu-id="53220-154">Sampling algorithm attempts tooeither sample in or out all hello correlated telemetry.</span></span> <span data-ttu-id="53220-155">Идентификатор анонимного пользователя используется для создания оценки выборки.</span><span class="sxs-lookup"><span data-stu-id="53220-155">Anonymous user id is used for sampling score generation.</span></span> <span data-ttu-id="53220-156">Поэтому он должен представлять собой достаточно случайное значение.</span><span class="sxs-lookup"><span data-stu-id="53220-156">So anonymous user id should be a random enough value.</span></span> 

<span data-ttu-id="53220-157">С помощью имени пользователя toostore идентификатор анонимного пользователя является неправильное использование поля hello.</span><span class="sxs-lookup"><span data-stu-id="53220-157">Using anonymous user id toostore user name is a misuse of hello field.</span></span> <span data-ttu-id="53220-158">Используйте для этого идентификатор прошедшего проверку подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="53220-158">Use Authenticated user id.</span></span>

<span data-ttu-id="53220-159">Максимальная длина: 128</span><span class="sxs-lookup"><span data-stu-id="53220-159">Max length: 128</span></span>


##<a name="authenticated-user-id"></a><span data-ttu-id="53220-160">Идентификатор прошедшего проверку подлинности пользователя</span><span class="sxs-lookup"><span data-stu-id="53220-160">Authenticated user id</span></span>

<span data-ttu-id="53220-161">Идентификатор пользователя, прошедшего проверку подлинности. Hello противоположного идентификатор анонимного пользователя, это поле представляет пользователя hello с понятным именем.</span><span class="sxs-lookup"><span data-stu-id="53220-161">Authenticated user id. hello opposite of anonymous user id, this field represents hello user with a friendly name.</span></span> <span data-ttu-id="53220-162">Так как это персональные данные, они не собираются по умолчанию большинством пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="53220-162">Since its PII information it is not collected by default by most SDK.</span></span>

<span data-ttu-id="53220-163">Максимальная длина: 1024</span><span class="sxs-lookup"><span data-stu-id="53220-163">Max length: 1024</span></span>


##<a name="account-id"></a><span data-ttu-id="53220-164">Идентификатор учетной записи</span><span class="sxs-lookup"><span data-stu-id="53220-164">Account id</span></span>

<span data-ttu-id="53220-165">В мультитенантных приложений это hello идентификатор учетной записи или имени, какой пользователь hello действует с.</span><span class="sxs-lookup"><span data-stu-id="53220-165">In multi-tenant applications this is hello account ID or name, which hello user is acting with.</span></span> <span data-ttu-id="53220-166">Примерами могут служить идентификатор подписки на портал Azure или имя блога на платформе для ведения блогов.</span><span class="sxs-lookup"><span data-stu-id="53220-166">Examples may be subscription ID for Azure portal or blog name blogging platform.</span></span>

<span data-ttu-id="53220-167">Максимальная длина: 1024</span><span class="sxs-lookup"><span data-stu-id="53220-167">Max length: 1024</span></span>


##<a name="cloud-role"></a><span data-ttu-id="53220-168">Облачная роль</span><span class="sxs-lookup"><span data-stu-id="53220-168">Cloud role</span></span>

<span data-ttu-id="53220-169">Имя приложения hello hello роли является частью.</span><span class="sxs-lookup"><span data-stu-id="53220-169">Name of hello role hello application is a part of.</span></span> <span data-ttu-id="53220-170">Сопоставляет непосредственно toohello имя роли в azure.</span><span class="sxs-lookup"><span data-stu-id="53220-170">Maps directly toohello role name in azure.</span></span> <span data-ttu-id="53220-171">Также можно использовать toodistinguish micro службам, которые являются частью одного приложения.</span><span class="sxs-lookup"><span data-stu-id="53220-171">Can also be used toodistinguish micro services, which are part of a single application.</span></span>

<span data-ttu-id="53220-172">Максимальная длина: 256</span><span class="sxs-lookup"><span data-stu-id="53220-172">Max length: 256</span></span>


##<a name="cloud-role-instance"></a><span data-ttu-id="53220-173">Экземпляр облачной роли</span><span class="sxs-lookup"><span data-stu-id="53220-173">Cloud role instance</span></span>

<span data-ttu-id="53220-174">Имя экземпляра hello, в котором запущено приложение hello.</span><span class="sxs-lookup"><span data-stu-id="53220-174">Name of hello instance where hello application is running.</span></span> <span data-ttu-id="53220-175">Имя компьютера в локальной среде; имя экземпляра для Azure.</span><span class="sxs-lookup"><span data-stu-id="53220-175">Computer name for on-premises, instance name for Azure.</span></span>

<span data-ttu-id="53220-176">Максимальная длина: 256</span><span class="sxs-lookup"><span data-stu-id="53220-176">Max length: 256</span></span>


##<a name="internal-sdk-version"></a><span data-ttu-id="53220-177">Внутреннее: версия SDK</span><span class="sxs-lookup"><span data-stu-id="53220-177">Internal: SDK version</span></span>

<span data-ttu-id="53220-178">Версия пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="53220-178">SDK version.</span></span> <span data-ttu-id="53220-179">Дополнительные сведения см. на странице по адресу https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification.</span><span class="sxs-lookup"><span data-stu-id="53220-179">See https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification for information.</span></span>

<span data-ttu-id="53220-180">Максимальная длина: 64</span><span class="sxs-lookup"><span data-stu-id="53220-180">Max length: 64</span></span>


##<a name="internal-node-name"></a><span data-ttu-id="53220-181">Внутреннее: имя узла</span><span class="sxs-lookup"><span data-stu-id="53220-181">Internal: Node name</span></span>

<span data-ttu-id="53220-182">Это поле представляет hello имя узла, используемое для выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="53220-182">This field represents hello node name used for billing purposes.</span></span> <span data-ttu-id="53220-183">Используйте стандартные обнаружения toooverride hello узлов.</span><span class="sxs-lookup"><span data-stu-id="53220-183">Use it toooverride hello standard detection of nodes.</span></span>

<span data-ttu-id="53220-184">Максимальная длина: 256</span><span class="sxs-lookup"><span data-stu-id="53220-184">Max length: 256</span></span>


## <a name="next-steps"></a><span data-ttu-id="53220-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="53220-185">Next steps</span></span>

- <span data-ttu-id="53220-186">Узнайте, каким образом слишком[расширения и фильтровать данные телеметрии](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="53220-186">Learn how too[extend and filter telemetry](app-insights-api-filtering-sampling.md).</span></span>
- <span data-ttu-id="53220-187">В [этой статье](application-insights-data-model.md) представлены типы данных и модель данных для Application Insights.</span><span class="sxs-lookup"><span data-stu-id="53220-187">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="53220-188">Извлеките стандартную [конфигурацию](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) коллекции свойств контекста.</span><span class="sxs-lookup"><span data-stu-id="53220-188">Check out standard context properties collection [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span></span>
