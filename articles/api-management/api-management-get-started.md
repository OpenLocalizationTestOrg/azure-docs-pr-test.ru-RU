---
title: "Приступая к работе с API в службе управления API Azure | Документация Майкрософт"
description: "Узнайте, как создавать API, добавлять операции и начать работу со службой управления API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 51b7df8b-1c43-43c6-90c9-0aa24f48206b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 6e76d1ee08f804637999ef2ebf5d25becf6a0408
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a><span data-ttu-id="85a48-103">Начало работы со службой управления Azure API </span><span class="sxs-lookup"><span data-stu-id="85a48-103">Manage your first API in Azure API Management</span></span>
## <span data-ttu-id="85a48-104"><a name="overview"> </a>Содержание раздела</span><span class="sxs-lookup"><span data-stu-id="85a48-104"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="85a48-105">Это руководство поможет быстро начать работу со службой управления API Azure и создать первый вызов API.</span><span class="sxs-lookup"><span data-stu-id="85a48-105">This guide shows you how to quickly get started in using Azure API Management and make your first API call.</span></span>

## <span data-ttu-id="85a48-106"><a name="concepts"> </a>Что такое служба управления Azure API?</span><span class="sxs-lookup"><span data-stu-id="85a48-106"><a name="concepts"> </a>What is Azure API Management?</span></span>
<span data-ttu-id="85a48-107">Службу управления Azure API можно использовать для запуска полноценной программы API на основе любого внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="85a48-107">You can use Azure API Management to take any backend and launch a full-fledged API program based on it.</span></span>

<span data-ttu-id="85a48-108">Ниже приведены распространенные сценарии.</span><span class="sxs-lookup"><span data-stu-id="85a48-108">Common scenarios include:</span></span>

* <span data-ttu-id="85a48-109">**Защита мобильной инфраструктуры** путем ограничения доступа с помощью ключей API, а также предотвращения DOS-атак за счет регулирования или использования расширенных политик безопасности, например проверки маркера JWT.</span><span class="sxs-lookup"><span data-stu-id="85a48-109">**Securing mobile infrastructure** by gating access with API keys, preventing DOS attacks by using throttling, or using advanced security policies like JWT token validation.</span></span>
* <span data-ttu-id="85a48-110">**Включение партнерской экосистемы независимого поставщика программного обеспечения** путем предложения быстрой партнерской адаптации на портале разработчика и создания интерфейсной части API поможет отделиться от внутренних реализаций, не готовых для использования партнером.</span><span class="sxs-lookup"><span data-stu-id="85a48-110">**Enabling ISV partner ecosystems** by offering fast partner onboarding through the developer portal and building an API facade to decouple from internal implementations that are not ripe for partner consumption.</span></span>
* <span data-ttu-id="85a48-111">**Выполнение внутренней программы API** за счет предложения организации централизованного расположения для обмена данными о доступности и последних изменениях в интерфейсах API, а также ограничения доступа на основе учетных записей организации, которые основаны на защищенном канале между шлюзом API и сервером.</span><span class="sxs-lookup"><span data-stu-id="85a48-111">**Running an internal API program** by offering a centralized location for the organization to communicate about the availability and latest changes to APIs, gating access based on organizational accounts, all based on a secured channel between the API gateway and the backend.</span></span>

<span data-ttu-id="85a48-112">Система состоит из следующих компонентов.</span><span class="sxs-lookup"><span data-stu-id="85a48-112">The system is made up of the following components:</span></span>

* <span data-ttu-id="85a48-113">**Шлюз API** – конечная точка, которая:</span><span class="sxs-lookup"><span data-stu-id="85a48-113">The **API gateway** is the endpoint that:</span></span>
  
  * <span data-ttu-id="85a48-114">принимает вызовы API и направляет их на серверы;</span><span class="sxs-lookup"><span data-stu-id="85a48-114">Accepts API calls and routes them to your backends.</span></span>
  * <span data-ttu-id="85a48-115">проверяет ключи API, маркеры привязки JWT, сертификаты и другие учетные данные;</span><span class="sxs-lookup"><span data-stu-id="85a48-115">Verifies API keys, JWT tokens, certificates, and other credentials.</span></span>
  * <span data-ttu-id="85a48-116">принудительно применяет квоты использования и ограничения скорости;</span><span class="sxs-lookup"><span data-stu-id="85a48-116">Enforces usage quotas and rate limits.</span></span>
  * <span data-ttu-id="85a48-117">преобразует API в режиме реального времени без изменения кода;</span><span class="sxs-lookup"><span data-stu-id="85a48-117">Transforms your API on the fly without code modifications.</span></span>
  * <span data-ttu-id="85a48-118">кэширует ответы сервера, если они настроены;</span><span class="sxs-lookup"><span data-stu-id="85a48-118">Caches backend responses where set up.</span></span>
  * <span data-ttu-id="85a48-119">регистрирует метаданные вызова для аналитики.</span><span class="sxs-lookup"><span data-stu-id="85a48-119">Logs call metadata for analytics purposes.</span></span>
* <span data-ttu-id="85a48-120">**Портал издателя** — административный интерфейс, предназначенный для настройки программы API.</span><span class="sxs-lookup"><span data-stu-id="85a48-120">The **publisher portal** is the administrative interface where you set up your API program.</span></span> <span data-ttu-id="85a48-121">Он используется, чтобы:</span><span class="sxs-lookup"><span data-stu-id="85a48-121">Use it to:</span></span>
  
  * <span data-ttu-id="85a48-122">определять или импортировать схемы API;</span><span class="sxs-lookup"><span data-stu-id="85a48-122">Define or import API schema.</span></span>
  * <span data-ttu-id="85a48-123">упаковывать интерфейсы API в продукты;</span><span class="sxs-lookup"><span data-stu-id="85a48-123">Package APIs into products.</span></span>
  * <span data-ttu-id="85a48-124">настраивать политики,например квоты или преобразования, в интерфейсах API;</span><span class="sxs-lookup"><span data-stu-id="85a48-124">Set up policies like quotas or transformations on the APIs.</span></span>
  * <span data-ttu-id="85a48-125">получать дополнительную информацию на основе аналитики;</span><span class="sxs-lookup"><span data-stu-id="85a48-125">Get insights from analytics.</span></span>
  * <span data-ttu-id="85a48-126">управлять пользователями.</span><span class="sxs-lookup"><span data-stu-id="85a48-126">Manage users.</span></span>
* <span data-ttu-id="85a48-127">**Портал разработчика** выступает в качестве основной веб-платформы для разработчиков, которая позволяет:</span><span class="sxs-lookup"><span data-stu-id="85a48-127">The **developer portal** serves as the main web presence for developers, where they can:</span></span>
  
  * <span data-ttu-id="85a48-128">читать документацию по API;</span><span class="sxs-lookup"><span data-stu-id="85a48-128">Read API documentation.</span></span>
  * <span data-ttu-id="85a48-129">использовать API через интерактивную консоль;</span><span class="sxs-lookup"><span data-stu-id="85a48-129">Try out an API via the interactive console.</span></span>
  * <span data-ttu-id="85a48-130">создать учетную запись и оформить подписку, чтобы получить ключи API;</span><span class="sxs-lookup"><span data-stu-id="85a48-130">Create an account and subscribe to get API keys.</span></span>
  * <span data-ttu-id="85a48-131">получить доступ к аналитике по использованию.</span><span class="sxs-lookup"><span data-stu-id="85a48-131">Access analytics on their own usage.</span></span>

## <span data-ttu-id="85a48-132"><a name="create-service-instance"></a>Создание экземпляра управления API</span><span class="sxs-lookup"><span data-stu-id="85a48-132"><a name="create-service-instance"> </a>Create an API Management instance</span></span>
> [!NOTE]
> <span data-ttu-id="85a48-133">Для работы с этим учебником требуется учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="85a48-133">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="85a48-134">Если ее нет, можно создать бесплатную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="85a48-134">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="85a48-135">Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][Azure Free Trial].</span><span class="sxs-lookup"><span data-stu-id="85a48-135">For details, see [Azure Free Trial][Azure Free Trial].</span></span>
> 
> 

<span data-ttu-id="85a48-136">Создание экземпляра службы — это первый шаг в работе с API Management.</span><span class="sxs-lookup"><span data-stu-id="85a48-136">The first step in working with API Management is to create a service instance.</span></span> <span data-ttu-id="85a48-137">Войдите на [портал Azure][Azure Portal] и щелкните **Создать**, **Интернет+мобильные устройства**, **Управление API**.</span><span class="sxs-lookup"><span data-stu-id="85a48-137">Sign in to the [Azure Portal][Azure Portal] and click **New**, **Web + Mobile**, **API Management**.</span></span>

![Новый экземпляр службы управления API ][api-management-create-instance-menu]

<span data-ttu-id="85a48-139">В качестве **имени** укажите уникальное имя поддомена для использования в качестве URL-адреса службы.</span><span class="sxs-lookup"><span data-stu-id="85a48-139">For **Name**, specify a unique sub-domain name to use for the service URL.</span></span>

<span data-ttu-id="85a48-140">Выберите необходимые значения в поле **Подписка**, **Группа ресурсов** и **Расположение** для своего экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="85a48-140">Choose the desired **Subscription**, **Resource group** and **Location** for your service instance.</span></span>

<span data-ttu-id="85a48-141">Введите **Contoso Ltd.**</span><span class="sxs-lookup"><span data-stu-id="85a48-141">Enter **Contoso Ltd.**</span></span> <span data-ttu-id="85a48-142">в поле **Имя организации** и укажите свой электронный адрес в поле **Адрес электронной почты администратора**.</span><span class="sxs-lookup"><span data-stu-id="85a48-142">for the **Organization Name**, and enter your email address in the **Administrator E-Mail** field.</span></span>

> [!NOTE]
> <span data-ttu-id="85a48-143">Этот адрес электронный почты используется для получения уведомлений от системы API Management.</span><span class="sxs-lookup"><span data-stu-id="85a48-143">This email address is used for notifications from the API Management system.</span></span> <span data-ttu-id="85a48-144">Дополнительные сведения см. в статье о [настройке уведомлений и почтовых шаблонов в службе управления Azure API][How to configure notifications and email templates in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="85a48-144">For more information, see [How to configure notifications and email templates in Azure API Management][How to configure notifications and email templates in Azure API Management].</span></span>
> 
> 

![Новая служба управления API][api-management-create-instance-step1]

<span data-ttu-id="85a48-146">Экземпляры службы управления API доступны на трех уровнях: Developer, Standard и Premium.</span><span class="sxs-lookup"><span data-stu-id="85a48-146">API Management service instances are available in three tiers: Developer, Standard, and Premium.</span></span>

> [!NOTE]
> <span data-ttu-id="85a48-147">Уровень Developer предназначен для разработки, тестирования и пилотного запуска приложений API, для которых доступность — это некритичный параметр.</span><span class="sxs-lookup"><span data-stu-id="85a48-147">The Developer Tier is for development, testing, and pilot API programs where high availability is not a concern.</span></span> <span data-ttu-id="85a48-148">На уровнях Standard и Premium можно масштабировать зарезервированное число единиц для обслуживания большего объема трафика.</span><span class="sxs-lookup"><span data-stu-id="85a48-148">In the Standard and Premium tiers, you can scale your reserved unit count to handle more traffic.</span></span> <span data-ttu-id="85a48-149">На уровнях Standard и Premium служба управления API обеспечивает наибольший уровень мощности и производительности.</span><span class="sxs-lookup"><span data-stu-id="85a48-149">The Standard and Premium tiers provide your API Management service with the most processing power and performance.</span></span> <span data-ttu-id="85a48-150">Вы можете изучать этот учебник, используя любой уровень.</span><span class="sxs-lookup"><span data-stu-id="85a48-150">You can complete this tutorial by using any tier.</span></span> <span data-ttu-id="85a48-151">Дополнительные сведения об уровнях управления API см. на странице с [расценками на службу управления API][API Management pricing].</span><span class="sxs-lookup"><span data-stu-id="85a48-151">For more information about API Management tiers, see [API Management pricing][API Management pricing].</span></span>
> 
> 

<span data-ttu-id="85a48-152">Щелкните **Создать**, чтобы начать подготовку экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="85a48-152">Click **Create** to start provisioning your service instance.</span></span>

![Новая служба управления API][api-management-instance-created]

<span data-ttu-id="85a48-154">После создания экземпляра службы на следующем шаге создается или импортируется API.</span><span class="sxs-lookup"><span data-stu-id="85a48-154">Once the service instance is created, the next step is to create or import an API.</span></span>

## <span data-ttu-id="85a48-155"><a name="create-api"> </a>Импорт API</span><span class="sxs-lookup"><span data-stu-id="85a48-155"><a name="create-api"> </a>Import an API</span></span>
<span data-ttu-id="85a48-156">API представляет набор операций, которые могут быть вызваны клиентскими приложениями.</span><span class="sxs-lookup"><span data-stu-id="85a48-156">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="85a48-157">Операции API передаются существующей веб-службе.</span><span class="sxs-lookup"><span data-stu-id="85a48-157">API operations are proxied to existing web services.</span></span>

<span data-ttu-id="85a48-158">Вы можете создавать интерфейсы API (и добавлять операции) вручную, а также импортировать и то, и другое.</span><span class="sxs-lookup"><span data-stu-id="85a48-158">APIs can be created (and operations can be added) manually, or they can be imported.</span></span> <span data-ttu-id="85a48-159">В этом учебнике мы импортируем API для примера веб-службы калькулятора, предоставляемой корпорацией Майкрософт и размещенной в Azure.</span><span class="sxs-lookup"><span data-stu-id="85a48-159">In this tutorial, we will import the API for a sample calculator web service provided by Microsoft and hosted on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="85a48-160">Указания о создании API и добавлении операций вручную см. в статьях, посвященных [созданию интерфейсов API в службе управления Azure API](api-management-howto-create-apis.md) и [добавлению операций в службе управления Azure API](api-management-howto-add-operations.md).</span><span class="sxs-lookup"><span data-stu-id="85a48-160">For guidance on creating an API and manually adding operations, see [How to create APIs](api-management-howto-create-apis.md) and [How to add operations to an API](api-management-howto-add-operations.md).</span></span>
> 
> 

<span data-ttu-id="85a48-161">Интерфейсы API настраиваются на портале издателя.</span><span class="sxs-lookup"><span data-stu-id="85a48-161">APIs are configured from the publisher portal.</span></span> <span data-ttu-id="85a48-162">Чтобы открыть его, щелкните **Publisher portal** (Портал издателя) на панели инструментов службы.</span><span class="sxs-lookup"><span data-stu-id="85a48-162">To reach it, click **Publisher portal** from the service toolbar.</span></span>

![Портал издателя][api-management-management-console]

<span data-ttu-id="85a48-164">Чтобы импортировать API калькулятора, щелкните **API** в расположенном слева меню **Управление API**, а затем выберите **Импортировать API**.</span><span class="sxs-lookup"><span data-stu-id="85a48-164">To import the calculator API, click **APIs** from the **API Management** menu on the left, and then click **Import API**.</span></span>

![Кнопка импорта API][api-management-import-api]

<span data-ttu-id="85a48-166">Выполните следующие действия, чтобы настроить API калькулятора.</span><span class="sxs-lookup"><span data-stu-id="85a48-166">Perform the following steps to configure the calculator API:</span></span>

1. <span data-ttu-id="85a48-167">Щелкните **Из URL-адреса**, введите **http://calcapi.cloudapp.net/calcapi.json** в текстовое поле **URL-адрес документа спецификаций** и щелкните переключатель **Swagger**.</span><span class="sxs-lookup"><span data-stu-id="85a48-167">Click **From URL**, enter **http://calcapi.cloudapp.net/calcapi.json** into the **Specification document URL** text box, and click the **Swagger** radio button.</span></span>
2. <span data-ttu-id="85a48-168">В текстовое поле **Суффикс URL-адреса веб-API** введите **calc**.</span><span class="sxs-lookup"><span data-stu-id="85a48-168">Type **calc** into the **Web API URL suffix** text box.</span></span>
3. <span data-ttu-id="85a48-169">Щелкните в поле **Продукты (необязательно)** и выберите **Starter**.</span><span class="sxs-lookup"><span data-stu-id="85a48-169">Click in the **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="85a48-170">Щелкните **Сохранить** , чтобы импортировать API.</span><span class="sxs-lookup"><span data-stu-id="85a48-170">Click **Save** to import the API.</span></span>

![Добавление нового API][api-management-import-new-api]

> [!NOTE]
> <span data-ttu-id="85a48-172">**управления API** поддерживает импорт документа Swagger версий 1.2 и 2.0 .</span><span class="sxs-lookup"><span data-stu-id="85a48-172">**API Management** currently supports both 1.2 and 2.0 version of Swagger document for import.</span></span> <span data-ttu-id="85a48-173">Хотя в [спецификации по Swagger 2.0](http://swagger.io/specification) заявлено, что свойства `host`, `basePath` и `schemes` являются необязательными, ваш документ Swagger 2.0 **ДОЛЖЕН** содержать их — в противном случае он не импортируется.</span><span class="sxs-lookup"><span data-stu-id="85a48-173">Make sure that, even though [Swagger 2.0 specification](http://swagger.io/specification) declares that `host`, `basePath`, and `schemes` properties are optional, your Swagger 2.0 document **MUST** contain those properties; otherwise it won't get imported.</span></span> 
> 
> 

<span data-ttu-id="85a48-174">После импорта API на портале издателя выводится страница сводных данных для API.</span><span class="sxs-lookup"><span data-stu-id="85a48-174">Once the API is imported, the summary page for the API is displayed in the publisher portal.</span></span>

![Сводные данные API][api-management-imported-api-summary]

<span data-ttu-id="85a48-176">Раздел API содержит несколько вкладок.</span><span class="sxs-lookup"><span data-stu-id="85a48-176">The API section has several tabs.</span></span> <span data-ttu-id="85a48-177">Вкладка **Сводные данные** содержит базовые показатели и информацию об API.</span><span class="sxs-lookup"><span data-stu-id="85a48-177">The **Summary** tab displays basic metrics and information about the API.</span></span> <span data-ttu-id="85a48-178">Вкладка [Параметры](api-management-howto-create-apis.md#configure-api-settings) используется для проверки и изменения конфигурации для API.</span><span class="sxs-lookup"><span data-stu-id="85a48-178">The [Settings](api-management-howto-create-apis.md#configure-api-settings) tab is used to view and edit the configuration for an API.</span></span> <span data-ttu-id="85a48-179">Вкладка [Операции](api-management-howto-add-operations.md) используется для управления операциями API.</span><span class="sxs-lookup"><span data-stu-id="85a48-179">The [Operations](api-management-howto-add-operations.md) tab is used to manage the API's operations.</span></span> <span data-ttu-id="85a48-180">Вкладка **Безопасность** используется для настройки проверки подлинности шлюза для внутреннего сервера с помощью базовой проверки подлинности или [взаимной проверки подлинности с помощью сертификатов](api-management-howto-mutual-certificates.md) и настройки [авторизации пользователя с помощью OAuth 2.0](api-management-howto-oauth2.md).</span><span class="sxs-lookup"><span data-stu-id="85a48-180">The **Security** tab can be used to configure gateway authentication for the backend server by using Basic authentication or [mutual certificate authentication](api-management-howto-mutual-certificates.md), and to configure [user authorization by using OAuth 2.0](api-management-howto-oauth2.md).</span></span>  <span data-ttu-id="85a48-181">На вкладке **Проблемы** отображаются проблемы, о которых сообщают разработчики, использующие интерфейсы API.</span><span class="sxs-lookup"><span data-stu-id="85a48-181">The **Issues** tab is used to view issues reported by the developers who are using your APIs.</span></span> <span data-ttu-id="85a48-182">На вкладке **Продукты** можно настроить продукты, которые содержат этот API.</span><span class="sxs-lookup"><span data-stu-id="85a48-182">The **Products** tab is used to configure the products that contain this API.</span></span>

<span data-ttu-id="85a48-183">По умолчанию каждый экземпляр API управления поставляется с двумя демонстрационными продуктами:</span><span class="sxs-lookup"><span data-stu-id="85a48-183">By default, each API Management instance comes with two sample products:</span></span>

* <span data-ttu-id="85a48-184">**Starter**</span><span class="sxs-lookup"><span data-stu-id="85a48-184">**Starter**</span></span>
* <span data-ttu-id="85a48-185">**Unlimited**</span><span class="sxs-lookup"><span data-stu-id="85a48-185">**Unlimited**</span></span>

<span data-ttu-id="85a48-186">В этом учебнике базовый API калькулятора был добавлен в продукт Starter при импорте API.</span><span class="sxs-lookup"><span data-stu-id="85a48-186">In this tutorial, the Basic Calculator API was added to the Starter product when the API was imported.</span></span>

<span data-ttu-id="85a48-187">Чтобы делать вызовы к API, разработчикам сначала необходимо подписаться на продукт, что дает им возможность доступа к нему.</span><span class="sxs-lookup"><span data-stu-id="85a48-187">In order to make calls to an API, developers must first subscribe to a product that gives them access to it.</span></span> <span data-ttu-id="85a48-188">Разработчики могут подписываться на продукты в портале разработчика. За них это также могут сделать администраторы в издательском портале.</span><span class="sxs-lookup"><span data-stu-id="85a48-188">Developers can subscribe to products in the developer portal, or administrators can subscribe developers to products in the publisher portal.</span></span> <span data-ttu-id="85a48-189">Вы становитесь администратором по умолчанию, так как создали экземпляр API управления на предыдущих шагах руководства, и поэтому вы подписаны на каждый продукт по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="85a48-189">You are an administrator since you created the API Management instance in the previous steps in the tutorial, so you are already subscribed to every product by default.</span></span>

## <span data-ttu-id="85a48-190"><a name="call-operation"> </a>Вызов операции с портала разработчика</span><span class="sxs-lookup"><span data-stu-id="85a48-190"><a name="call-operation"> </a>Call an operation from the developer portal</span></span>
<span data-ttu-id="85a48-191">Операции могут быть вызваны из портала разработчика, в который встроен удобный способ просмотра и проверки операций API.</span><span class="sxs-lookup"><span data-stu-id="85a48-191">Operations can be called directly from the developer portal, which provides a convenient way to view and test the operations of an API.</span></span> <span data-ttu-id="85a48-192">На этом шаге учебника будет вызвана операция **Добавление двух целых** базового API калькулятора.</span><span class="sxs-lookup"><span data-stu-id="85a48-192">In this tutorial step, you will call the Basic Calculator API's **Add two integers** operation.</span></span> <span data-ttu-id="85a48-193">Выберите **Портал разработчика** в правом верхнем меню в портале издателя.</span><span class="sxs-lookup"><span data-stu-id="85a48-193">Click **Developer portal** from the menu at the top right of the publisher portal.</span></span>

![Портал разработчика][api-management-developer-portal-menu]

<span data-ttu-id="85a48-195">Выберите **API** в верхнем меню и щелкните **Базовый калькулятор**, чтобы увидеть доступные операции.</span><span class="sxs-lookup"><span data-stu-id="85a48-195">Click **APIs** from the top menu, and then click **Basic Calculator** to see the available operations.</span></span>

![Портал разработчика][api-management-developer-portal-calc-api]

<span data-ttu-id="85a48-197">Обратите внимание на описание и параметры примера, импортированные с API и с операциями, благодаря чему разработчики, которые будут использовать эту операцию, получают необходимую документацию.</span><span class="sxs-lookup"><span data-stu-id="85a48-197">Note the sample descriptions and parameters that were imported along with the API and operations, providing documentation for the developers that will use this operation.</span></span> <span data-ttu-id="85a48-198">Эти описания можно также добавить при добавлении операций вручную.</span><span class="sxs-lookup"><span data-stu-id="85a48-198">These descriptions can also be added when operations are added manually.</span></span>

<span data-ttu-id="85a48-199">Чтобы вызвать операцию **Добавление двух целых**, нажмите кнопку **Попробовать**.</span><span class="sxs-lookup"><span data-stu-id="85a48-199">To call the **Add two integers** operation, click **Try it**.</span></span>

![Попробовать][api-management-developer-portal-calc-api-console]

<span data-ttu-id="85a48-201">Вы можете ввести некоторые значения для параметров или оставить значения по умолчанию и щелкнуть **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="85a48-201">You can enter some values for the parameters or keep the defaults, and then click **Send**.</span></span>

![HTTP Get][api-management-invoke-get]

<span data-ttu-id="85a48-203">После вызова операции портал разработчика отображает **состояние ответа**, **заголовки ответа** и **содержимое ответа**.</span><span class="sxs-lookup"><span data-stu-id="85a48-203">After an operation is invoked, the developer portal displays the **Response status**, the **Response headers**, and any **Response content**.</span></span>

![Ответ][api-management-invoke-get-response]

## <span data-ttu-id="85a48-205"><a name="view-analytics"> </a>Просмотр аналитики</span><span class="sxs-lookup"><span data-stu-id="85a48-205"><a name="view-analytics"> </a>View analytics</span></span>
<span data-ttu-id="85a48-206">Чтобы просмотреть аналитику для базового калькулятора, снова перейдите к порталу разработчика, выбрав **Управление** в верхнем правом меню пользователя на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="85a48-206">To view analytics for Basic Calculator, switch back to the publisher portal by selecting **Manage** from the menu at the top right of the developer portal.</span></span>

![Управление][api-management-manage-menu]

<span data-ttu-id="85a48-208">Представление портала издателя по умолчанию представляет собой **панель мониторинга**, где присутствует информация об экземпляре управления API.</span><span class="sxs-lookup"><span data-stu-id="85a48-208">The default view for the publisher portal is the **Dashboard**, which provides an overview of your API Management instance.</span></span>

![панель мониторинга][api-management-dashboard]

<span data-ttu-id="85a48-210">Наведите указатель мыши на диаграмму **базового калькулятора** , чтобы просмотреть конкретные показатели использования API за данный период времени.</span><span class="sxs-lookup"><span data-stu-id="85a48-210">Hover the mouse over the chart for **Basic Calculator** to see the specific metrics for the usage of the API for a given time period.</span></span>

> [!NOTE]
> <span data-ttu-id="85a48-211">Если на диаграмме нет показателей, перейдите назад к порталу разработчика и сделайте несколько вызовов API, подождите немного, а затем вернитесь к панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="85a48-211">If you don't see any lines on your chart, switch back to the developer portal and make some calls into the API, wait a few moments, and then come back to the dashboard.</span></span>
> 
> 

<span data-ttu-id="85a48-212">Щелкните **Просмотр сведений** для просмотра страницы сводной информации по API, включая расширенную версию выводимых показателей.</span><span class="sxs-lookup"><span data-stu-id="85a48-212">Click **View Details** to view the summary page for the API, including a larger version of the displayed metrics.</span></span>

![Аналитика][api-management-mouse-over]

![Сводка][api-management-api-summary-metrics]

<span data-ttu-id="85a48-215">Для просмотра более подробных метрик и отчетов щелкните пункт **Аналитика** в меню **Управление API** слева.</span><span class="sxs-lookup"><span data-stu-id="85a48-215">For detailed metrics and reports, click **Analytics** from the **API Management** menu on the left.</span></span>

![Обзор][api-management-analytics-overview]

<span data-ttu-id="85a48-217">Раздел **Аналитика** имеет следующие четыре вкладки.</span><span class="sxs-lookup"><span data-stu-id="85a48-217">The **Analytics** section has the following four tabs:</span></span>

* <span data-ttu-id="85a48-218">**Вкратце** содержит общую информацию об использовании и показатели состояния, а также информацию о наиболее активных разработчиках, продуктах, API и операциях.</span><span class="sxs-lookup"><span data-stu-id="85a48-218">**At a glance** provides overall usage and health metrics, as well as the top developers, top products, top APIs, and top operations.</span></span>
* <span data-ttu-id="85a48-219">**Использование** содержит обзор деталей вызовов API и полосы пропускания, включая географическое представление.</span><span class="sxs-lookup"><span data-stu-id="85a48-219">**Usage** provides an in-depth look at API calls and bandwidth, including a geographical representation.</span></span>
* <span data-ttu-id="85a48-220">**Работоспособность** содержит коды состояний, показатели успешных попаданий в кэш и времена ответов API и служб.</span><span class="sxs-lookup"><span data-stu-id="85a48-220">**Health** focuses on status codes, cache success rates, response times, and API and service response times.</span></span>
* <span data-ttu-id="85a48-221">**Активность** содержит отчеты по конкретной активности для разработчиков, продуктов, API и операций.</span><span class="sxs-lookup"><span data-stu-id="85a48-221">**Activity** provides reports that drill down on the specific activity by developer, product, API, and operation.</span></span>

## <span data-ttu-id="85a48-222"><a name="next-steps"> </a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="85a48-222"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="85a48-223">Информация о [защите интерфейсов API с помощью ограничений скорости](api-management-howto-product-with-rules.md).</span><span class="sxs-lookup"><span data-stu-id="85a48-223">Learn how to [Protect your API with rate limits](api-management-howto-product-with-rules.md).</span></span>

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add the new API to a product]: #add-api-to-product
[Subscribe to the product that contains the API]: #subscribe
[Call an operation from the Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How to manage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How to configure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[API Management pricing]: http://azure.microsoft.com/pricing/details/api-management/

[Azure Portal]: https://portal.azure.com/

[api-management-management-console]: ./media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: ./media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: ./media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: ./media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: ./media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: ./media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: ./media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png
