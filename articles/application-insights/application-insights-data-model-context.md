---
title: "Модель данных телеметрии Azure Application Insights — контекст телеметрии | Документы Майкрософт"
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
ms.openlocfilehash: d6a0cad8bda6ca68aa691867e84f540c5ac9f6f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="telemetry-context-application-insights-data-model"></a><span data-ttu-id="70e35-103">Контекст телеметрии: модель данных Application Insights</span><span class="sxs-lookup"><span data-stu-id="70e35-103">Telemetry context: Application Insights data model</span></span>

<span data-ttu-id="70e35-104">Каждый элемент данных телеметрии может иметь строго типизированные поля контекста.</span><span class="sxs-lookup"><span data-stu-id="70e35-104">Every telemetry item may have a strongly typed context fields.</span></span> <span data-ttu-id="70e35-105">Каждое поле обеспечивает определенный сценарий мониторинга.</span><span class="sxs-lookup"><span data-stu-id="70e35-105">Every field enables a specific monitoring scenario.</span></span> <span data-ttu-id="70e35-106">Используйте пользовательскую коллекцию свойств для хранения пользовательских или связанных с приложением контекстных данных.</span><span class="sxs-lookup"><span data-stu-id="70e35-106">Use the custom properties collection to store custom or application-specific contextual information.</span></span>


##<a name="application-version"></a><span data-ttu-id="70e35-107">Версия приложения</span><span class="sxs-lookup"><span data-stu-id="70e35-107">Application version</span></span>

<span data-ttu-id="70e35-108">Сведения в полях контекста приложения всегда связаны с приложением, отправляющим данные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="70e35-108">Information in the application context fields is always about the application that is sending the telemetry.</span></span> <span data-ttu-id="70e35-109">Версия приложения используется для анализа изменений тенденций в работе приложения и его сопоставления с развертываниями.</span><span class="sxs-lookup"><span data-stu-id="70e35-109">Application version is used to analyze trend changes in the application behavior and its correlation to the deployments.</span></span>

<span data-ttu-id="70e35-110">Максимальная длина: 1024</span><span class="sxs-lookup"><span data-stu-id="70e35-110">Max length: 1024</span></span>


##<a name="client-ip-address"></a><span data-ttu-id="70e35-111">IP-адрес клиента</span><span class="sxs-lookup"><span data-stu-id="70e35-111">Client IP address</span></span>

<span data-ttu-id="70e35-112">IP-адрес клиентского устройства.</span><span class="sxs-lookup"><span data-stu-id="70e35-112">The IP address of the client device.</span></span> <span data-ttu-id="70e35-113">Поддерживаются протоколы IPv4 и IPv6.</span><span class="sxs-lookup"><span data-stu-id="70e35-113">IPv4 and IPv6 are supported.</span></span> <span data-ttu-id="70e35-114">Когда данные телеметрии отправляются из службы, контекст расположения указывает на пользователя, который инициировал операцию в службе.</span><span class="sxs-lookup"><span data-stu-id="70e35-114">When telemetry is sent from a service, the location context is about the user that initiated the operation in the service.</span></span> <span data-ttu-id="70e35-115">Application Insights извлекает сведения о географическом положении из IP-адреса клиента, а затем усекает его.</span><span class="sxs-lookup"><span data-stu-id="70e35-115">Application Insights extract the geo-location information from the client IP and then truncate it.</span></span> <span data-ttu-id="70e35-116">Поэтому IP-адрес клиента сам по себе нельзя использовать как идентификационные данные конечного пользователя.</span><span class="sxs-lookup"><span data-stu-id="70e35-116">So client IP by itself cannot be used as end-user identifiable information.</span></span> 

<span data-ttu-id="70e35-117">Максимальная длина: 46</span><span class="sxs-lookup"><span data-stu-id="70e35-117">Max length: 46</span></span>


##<a name="device-type"></a><span data-ttu-id="70e35-118">Тип устройства</span><span class="sxs-lookup"><span data-stu-id="70e35-118">Device type</span></span>

<span data-ttu-id="70e35-119">Изначально это поле использовалось для указания типа устройства, применяемого конечным пользователем приложения.</span><span class="sxs-lookup"><span data-stu-id="70e35-119">Originally this field was used to indicate the type of the device the end user of the application is using.</span></span> <span data-ttu-id="70e35-120">В настоящее время используется в первую очередь для различения данных телеметрии JavaScript с типом устройства "Браузер" от данных телеметрии на стороне сервера с типом устройства "ПК".</span><span class="sxs-lookup"><span data-stu-id="70e35-120">Today used primarily to distinguish JavaScript telemetry with the device type 'Browser' from server-side telemetry with the device type 'PC'.</span></span>

<span data-ttu-id="70e35-121">Максимальная длина: 64</span><span class="sxs-lookup"><span data-stu-id="70e35-121">Max length: 64</span></span>


##<a name="operation-id"></a><span data-ttu-id="70e35-122">Идентификатор операции</span><span class="sxs-lookup"><span data-stu-id="70e35-122">Operation id</span></span>

<span data-ttu-id="70e35-123">Уникальный идентификатор корневой операции.</span><span class="sxs-lookup"><span data-stu-id="70e35-123">A unique identifier of the root operation.</span></span> <span data-ttu-id="70e35-124">Этот идентификатор позволяет группировать данные телеметрии по нескольким компонентам.</span><span class="sxs-lookup"><span data-stu-id="70e35-124">This identifier allows to group telemetry across multiple components.</span></span> <span data-ttu-id="70e35-125">Подробные сведения см. в статье [Корреляция данных телеметрии](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="70e35-125">See [telemetry correlation](application-insights-correlation.md) for details.</span></span> <span data-ttu-id="70e35-126">Идентификатор операции создается в результате запроса или просмотра страницы.</span><span class="sxs-lookup"><span data-stu-id="70e35-126">The operation id is created by either a request or a page view.</span></span> <span data-ttu-id="70e35-127">Все другие данные телеметрии присваивают этому полю значение содержащего запроса или просмотра страницы.</span><span class="sxs-lookup"><span data-stu-id="70e35-127">All other telemetry sets this field to the value for the containing request or page view.</span></span> 

<span data-ttu-id="70e35-128">Максимальная длина: 128</span><span class="sxs-lookup"><span data-stu-id="70e35-128">Max length: 128</span></span>


##<a name="parent-operation-id"></a><span data-ttu-id="70e35-129">Идентификатор родительской операции</span><span class="sxs-lookup"><span data-stu-id="70e35-129">Parent operation ID</span></span>

<span data-ttu-id="70e35-130">Уникальный идентификатор непосредственного родительского объекта элемента данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="70e35-130">The unique identifier of the telemetry item's immediate parent.</span></span> <span data-ttu-id="70e35-131">Подробные сведения см. в статье [Корреляция данных телеметрии](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="70e35-131">See [telemetry correlation](application-insights-correlation.md) for details.</span></span>

<span data-ttu-id="70e35-132">Максимальная длина: 128</span><span class="sxs-lookup"><span data-stu-id="70e35-132">Max length: 128</span></span>


##<a name="operation-name"></a><span data-ttu-id="70e35-133">Имя операции</span><span class="sxs-lookup"><span data-stu-id="70e35-133">Operation name</span></span>

<span data-ttu-id="70e35-134">Имя (группа) операции</span><span class="sxs-lookup"><span data-stu-id="70e35-134">The name (group) of the operation.</span></span> <span data-ttu-id="70e35-135">Имя операции создается в результате запроса или просмотра страницы.</span><span class="sxs-lookup"><span data-stu-id="70e35-135">The operation name is created by either a request or a page view.</span></span> <span data-ttu-id="70e35-136">Все другие элементы данных телеметрии присваивают этому полю значение содержащего запроса или просмотра страницы.</span><span class="sxs-lookup"><span data-stu-id="70e35-136">All other telemetry items set this field to the value for the containing request or page view.</span></span> <span data-ttu-id="70e35-137">Имя операции используется для нахождения всех элементов данных телеметрии для группы операций (например, "GET Home/Index").</span><span class="sxs-lookup"><span data-stu-id="70e35-137">Operation name is used for finding all the telemetry items for a group of operations (for example 'GET Home/Index').</span></span> <span data-ttu-id="70e35-138">Это свойство контекста служит для ответа на вопросы типа "какие исключения, как правило, создаются на этой странице".</span><span class="sxs-lookup"><span data-stu-id="70e35-138">This context property is used to answer questions like "what are the typical exceptions thrown on this page."</span></span>

<span data-ttu-id="70e35-139">Максимальная длина: 1024</span><span class="sxs-lookup"><span data-stu-id="70e35-139">Max length: 1024</span></span>


##<a name="synthetic-source-of-the-operation"></a><span data-ttu-id="70e35-140">Искусственный источник операции</span><span class="sxs-lookup"><span data-stu-id="70e35-140">Synthetic source of the operation</span></span>

<span data-ttu-id="70e35-141">Имя искусственного источника.</span><span class="sxs-lookup"><span data-stu-id="70e35-141">Name of synthetic source.</span></span> <span data-ttu-id="70e35-142">Некоторые данные телеметрии из приложения могут представлять искусственный трафик.</span><span class="sxs-lookup"><span data-stu-id="70e35-142">Some telemetry from the application may represent synthetic traffic.</span></span> <span data-ttu-id="70e35-143">Он может возникать в результате индексации веб-сайта поисковым модулем, тестов доступности сайта или трассировок из библиотек диагностики, например самого пакета SDK для Application Insights.</span><span class="sxs-lookup"><span data-stu-id="70e35-143">It may be web crawler indexing the web site, site availability tests, or traces from diagnostic libraries like Application Insights SDK itself.</span></span>

<span data-ttu-id="70e35-144">Максимальная длина: 1024</span><span class="sxs-lookup"><span data-stu-id="70e35-144">Max length: 1024</span></span>


##<a name="session-id"></a><span data-ttu-id="70e35-145">Идентификатор сеанса</span><span class="sxs-lookup"><span data-stu-id="70e35-145">Session id</span></span>

<span data-ttu-id="70e35-146">Идентификатор сеанса — экземпляр взаимодействия пользователя с приложением.</span><span class="sxs-lookup"><span data-stu-id="70e35-146">Session ID - the instance of the user's interaction with the app.</span></span> <span data-ttu-id="70e35-147">Сведения в полях контекста сеанса всегда связаны с конечным пользователем.</span><span class="sxs-lookup"><span data-stu-id="70e35-147">Information in the session context fields is always about the end user.</span></span> <span data-ttu-id="70e35-148">Когда данные телеметрии отправляются из службы, контекст сеанса указывает на пользователя, который инициировал операцию в службе.</span><span class="sxs-lookup"><span data-stu-id="70e35-148">When telemetry is sent from a service, the session context is about the user that initiated the operation in the service.</span></span>

<span data-ttu-id="70e35-149">Максимальная длина: 64</span><span class="sxs-lookup"><span data-stu-id="70e35-149">Max length: 64</span></span>


##<a name="anonymous-user-id"></a><span data-ttu-id="70e35-150">Идентификатор анонимного пользователя</span><span class="sxs-lookup"><span data-stu-id="70e35-150">Anonymous user id</span></span>

<span data-ttu-id="70e35-151">Идентификатор анонимного пользователя.</span><span class="sxs-lookup"><span data-stu-id="70e35-151">Anonymous user id.</span></span> <span data-ttu-id="70e35-152">Представляет конечного пользователя приложения.</span><span class="sxs-lookup"><span data-stu-id="70e35-152">Represents the end user of the application.</span></span> <span data-ttu-id="70e35-153">Когда данные телеметрии отправляются из службы, контекст пользователя указывает на пользователя, который инициировал операцию в службе.</span><span class="sxs-lookup"><span data-stu-id="70e35-153">When telemetry is sent from a service, the user context is about the user that initiated the operation in the service.</span></span>

<span data-ttu-id="70e35-154">[Выборка](app-insights-sampling.md) — один из приемов, позволяющих свести к минимуму объем собираемых данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="70e35-154">[Sampling](app-insights-sampling.md) is one of the techniques to minimize the amount of collected telemetry.</span></span> <span data-ttu-id="70e35-155">Алгоритм выборки пытается произвести внутреннюю или внешнюю выборку всех сопоставленных данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="70e35-155">Sampling algorithm attempts to either sample in or out all the correlated telemetry.</span></span> <span data-ttu-id="70e35-156">Идентификатор анонимного пользователя используется для создания оценки выборки.</span><span class="sxs-lookup"><span data-stu-id="70e35-156">Anonymous user id is used for sampling score generation.</span></span> <span data-ttu-id="70e35-157">Поэтому он должен представлять собой достаточно случайное значение.</span><span class="sxs-lookup"><span data-stu-id="70e35-157">So anonymous user id should be a random enough value.</span></span> 

<span data-ttu-id="70e35-158">Использовать поле идентификатора анонимного пользователя для хранения имени пользователя неправильно.</span><span class="sxs-lookup"><span data-stu-id="70e35-158">Using anonymous user id to store user name is a misuse of the field.</span></span> <span data-ttu-id="70e35-159">Используйте для этого идентификатор прошедшего проверку подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="70e35-159">Use Authenticated user id.</span></span>

<span data-ttu-id="70e35-160">Максимальная длина: 128</span><span class="sxs-lookup"><span data-stu-id="70e35-160">Max length: 128</span></span>


##<a name="authenticated-user-id"></a><span data-ttu-id="70e35-161">Идентификатор прошедшего проверку подлинности пользователя</span><span class="sxs-lookup"><span data-stu-id="70e35-161">Authenticated user id</span></span>

<span data-ttu-id="70e35-162">Идентификатор прошедшего проверку подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="70e35-162">Authenticated user id.</span></span> <span data-ttu-id="70e35-163">В отличие от идентификатора анонимного пользователя, это поле содержит понятное имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="70e35-163">The opposite of anonymous user id, this field represents the user with a friendly name.</span></span> <span data-ttu-id="70e35-164">Так как это персональные данные, они не собираются по умолчанию большинством пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="70e35-164">Since its PII information it is not collected by default by most SDK.</span></span>

<span data-ttu-id="70e35-165">Максимальная длина: 1024</span><span class="sxs-lookup"><span data-stu-id="70e35-165">Max length: 1024</span></span>


##<a name="account-id"></a><span data-ttu-id="70e35-166">Идентификатор учетной записи</span><span class="sxs-lookup"><span data-stu-id="70e35-166">Account id</span></span>

<span data-ttu-id="70e35-167">В мультитенантных приложениях это идентификатор или имя учетной записи, в которой работает пользователь.</span><span class="sxs-lookup"><span data-stu-id="70e35-167">In multi-tenant applications this is the account ID or name, which the user is acting with.</span></span> <span data-ttu-id="70e35-168">Примерами могут служить идентификатор подписки на портал Azure или имя блога на платформе для ведения блогов.</span><span class="sxs-lookup"><span data-stu-id="70e35-168">Examples may be subscription ID for Azure portal or blog name blogging platform.</span></span>

<span data-ttu-id="70e35-169">Максимальная длина: 1024</span><span class="sxs-lookup"><span data-stu-id="70e35-169">Max length: 1024</span></span>


##<a name="cloud-role"></a><span data-ttu-id="70e35-170">Облачная роль</span><span class="sxs-lookup"><span data-stu-id="70e35-170">Cloud role</span></span>

<span data-ttu-id="70e35-171">Имя роли, к которой относится приложение.</span><span class="sxs-lookup"><span data-stu-id="70e35-171">Name of the role the application is a part of.</span></span> <span data-ttu-id="70e35-172">Сопоставляется непосредственно с именем роли в Azure.</span><span class="sxs-lookup"><span data-stu-id="70e35-172">Maps directly to the role name in azure.</span></span> <span data-ttu-id="70e35-173">Также может использоваться для различения микрослужб, которые входят в состав одного приложения.</span><span class="sxs-lookup"><span data-stu-id="70e35-173">Can also be used to distinguish micro services, which are part of a single application.</span></span>

<span data-ttu-id="70e35-174">Максимальная длина: 256</span><span class="sxs-lookup"><span data-stu-id="70e35-174">Max length: 256</span></span>


##<a name="cloud-role-instance"></a><span data-ttu-id="70e35-175">Экземпляр облачной роли</span><span class="sxs-lookup"><span data-stu-id="70e35-175">Cloud role instance</span></span>

<span data-ttu-id="70e35-176">Имя экземпляра, в котором работает приложение.</span><span class="sxs-lookup"><span data-stu-id="70e35-176">Name of the instance where the application is running.</span></span> <span data-ttu-id="70e35-177">Имя компьютера в локальной среде; имя экземпляра для Azure.</span><span class="sxs-lookup"><span data-stu-id="70e35-177">Computer name for on-premises, instance name for Azure.</span></span>

<span data-ttu-id="70e35-178">Максимальная длина: 256</span><span class="sxs-lookup"><span data-stu-id="70e35-178">Max length: 256</span></span>


##<a name="internal-sdk-version"></a><span data-ttu-id="70e35-179">Внутреннее: версия SDK</span><span class="sxs-lookup"><span data-stu-id="70e35-179">Internal: SDK version</span></span>

<span data-ttu-id="70e35-180">Версия пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="70e35-180">SDK version.</span></span> <span data-ttu-id="70e35-181">Дополнительные сведения см. на странице по адресу https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification.</span><span class="sxs-lookup"><span data-stu-id="70e35-181">See https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification for information.</span></span>

<span data-ttu-id="70e35-182">Максимальная длина: 64</span><span class="sxs-lookup"><span data-stu-id="70e35-182">Max length: 64</span></span>


##<a name="internal-node-name"></a><span data-ttu-id="70e35-183">Внутреннее: имя узла</span><span class="sxs-lookup"><span data-stu-id="70e35-183">Internal: Node name</span></span>

<span data-ttu-id="70e35-184">Это поле представляет имя узла, используемое для выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="70e35-184">This field represents the node name used for billing purposes.</span></span> <span data-ttu-id="70e35-185">Используйте его для переопределения стандартного механизма обнаружения узлов.</span><span class="sxs-lookup"><span data-stu-id="70e35-185">Use it to override the standard detection of nodes.</span></span>

<span data-ttu-id="70e35-186">Максимальная длина: 256</span><span class="sxs-lookup"><span data-stu-id="70e35-186">Max length: 256</span></span>


## <a name="next-steps"></a><span data-ttu-id="70e35-187">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="70e35-187">Next steps</span></span>

- <span data-ttu-id="70e35-188">Вы можете узнать, как [расширять и фильтровать данные телеметрии](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="70e35-188">Learn how to [extend and filter telemetry](app-insights-api-filtering-sampling.md).</span></span>
- <span data-ttu-id="70e35-189">В [этой статье](application-insights-data-model.md) представлены типы данных и модель данных для Application Insights.</span><span class="sxs-lookup"><span data-stu-id="70e35-189">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="70e35-190">Извлеките стандартную [конфигурацию](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) коллекции свойств контекста.</span><span class="sxs-lookup"><span data-stu-id="70e35-190">Check out standard context properties collection [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span></span>
