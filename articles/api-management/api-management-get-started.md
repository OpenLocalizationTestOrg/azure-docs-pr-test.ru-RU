---
title: "aaaManage первый API в службе управления API Azure | Документы Microsoft"
description: "Узнайте, как toocreate API, добавьте операции и приступить к работе со службой управления API."
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
ms.openlocfilehash: 7d43f33aa359c4d1e605e9fb41e43d323ca6a777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a><span data-ttu-id="bdb40-103">Начало работы со службой управления Azure API </span><span class="sxs-lookup"><span data-stu-id="bdb40-103">Manage your first API in Azure API Management</span></span>
## <span data-ttu-id="bdb40-104"><a name="overview"> </a>Содержание раздела</span><span class="sxs-lookup"><span data-stu-id="bdb40-104"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="bdb40-105">В этом руководстве показано, как tooquickly Приступая к работе с использованием службы управления API Azure и сделать ваш первый вызов API.</span><span class="sxs-lookup"><span data-stu-id="bdb40-105">This guide shows you how tooquickly get started in using Azure API Management and make your first API call.</span></span>

## <span data-ttu-id="bdb40-106"><a name="concepts"> </a>Что такое служба управления Azure API?</span><span class="sxs-lookup"><span data-stu-id="bdb40-106"><a name="concepts"> </a>What is Azure API Management?</span></span>
<span data-ttu-id="bdb40-107">Можно использовать любой серверной tootake API управления Azure и запустить программу полноценные API, на его основе.</span><span class="sxs-lookup"><span data-stu-id="bdb40-107">You can use Azure API Management tootake any backend and launch a full-fledged API program based on it.</span></span>

<span data-ttu-id="bdb40-108">Ниже приведены распространенные сценарии.</span><span class="sxs-lookup"><span data-stu-id="bdb40-108">Common scenarios include:</span></span>

* <span data-ttu-id="bdb40-109">**Защита мобильной инфраструктуры** путем ограничения доступа с помощью ключей API, а также предотвращения DOS-атак за счет регулирования или использования расширенных политик безопасности, например проверки маркера JWT.</span><span class="sxs-lookup"><span data-stu-id="bdb40-109">**Securing mobile infrastructure** by gating access with API keys, preventing DOS attacks by using throttling, or using advanced security policies like JWT token validation.</span></span>
* <span data-ttu-id="bdb40-110">**Включение экосистемы партнера ISV** , предлагая адаптации быстрого партнера по hello разработки при помощи портала и построение toodecouple оболочкой API из внутренней реализации, не богатыми возможностями потребления партнера.</span><span class="sxs-lookup"><span data-stu-id="bdb40-110">**Enabling ISV partner ecosystems** by offering fast partner onboarding through hello developer portal and building an API facade toodecouple from internal implementations that are not ripe for partner consumption.</span></span>
* <span data-ttu-id="bdb40-111">**Запущено внутренних API** обеспечивая централизованное hello toocommunicate организации о доступности hello и последних изменений tooAPIs, стробирования доступ на основании учетных записей организации, на основе защищенного канала между шлюз Hello API и серверной hello.</span><span class="sxs-lookup"><span data-stu-id="bdb40-111">**Running an internal API program** by offering a centralized location for hello organization toocommunicate about hello availability and latest changes tooAPIs, gating access based on organizational accounts, all based on a secured channel between hello API gateway and hello backend.</span></span>

<span data-ttu-id="bdb40-112">система Hello состоит из hello следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="bdb40-112">hello system is made up of hello following components:</span></span>

* <span data-ttu-id="bdb40-113">Hello **шлюза API** является конечной точкой hello:</span><span class="sxs-lookup"><span data-stu-id="bdb40-113">hello **API gateway** is hello endpoint that:</span></span>
  
  * <span data-ttu-id="bdb40-114">Принимает вызывает API и направляет их tooyour серверных системах.</span><span class="sxs-lookup"><span data-stu-id="bdb40-114">Accepts API calls and routes them tooyour backends.</span></span>
  * <span data-ttu-id="bdb40-115">проверяет ключи API, маркеры привязки JWT, сертификаты и другие учетные данные;</span><span class="sxs-lookup"><span data-stu-id="bdb40-115">Verifies API keys, JWT tokens, certificates, and other credentials.</span></span>
  * <span data-ttu-id="bdb40-116">принудительно применяет квоты использования и ограничения скорости;</span><span class="sxs-lookup"><span data-stu-id="bdb40-116">Enforces usage quotas and rate limits.</span></span>
  * <span data-ttu-id="bdb40-117">Преобразует API на лету hello без изменения кода.</span><span class="sxs-lookup"><span data-stu-id="bdb40-117">Transforms your API on hello fly without code modifications.</span></span>
  * <span data-ttu-id="bdb40-118">кэширует ответы сервера, если они настроены;</span><span class="sxs-lookup"><span data-stu-id="bdb40-118">Caches backend responses where set up.</span></span>
  * <span data-ttu-id="bdb40-119">регистрирует метаданные вызова для аналитики.</span><span class="sxs-lookup"><span data-stu-id="bdb40-119">Logs call metadata for analytics purposes.</span></span>
* <span data-ttu-id="bdb40-120">Hello **портал издателя** — административный интерфейс hello, где можно настроить программу API.</span><span class="sxs-lookup"><span data-stu-id="bdb40-120">hello **publisher portal** is hello administrative interface where you set up your API program.</span></span> <span data-ttu-id="bdb40-121">Он используется, чтобы:</span><span class="sxs-lookup"><span data-stu-id="bdb40-121">Use it to:</span></span>
  
  * <span data-ttu-id="bdb40-122">определять или импортировать схемы API;</span><span class="sxs-lookup"><span data-stu-id="bdb40-122">Define or import API schema.</span></span>
  * <span data-ttu-id="bdb40-123">упаковывать интерфейсы API в продукты;</span><span class="sxs-lookup"><span data-stu-id="bdb40-123">Package APIs into products.</span></span>
  * <span data-ttu-id="bdb40-124">Настройка политики, такие как квоты или преобразований на hello API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="bdb40-124">Set up policies like quotas or transformations on hello APIs.</span></span>
  * <span data-ttu-id="bdb40-125">получать дополнительную информацию на основе аналитики;</span><span class="sxs-lookup"><span data-stu-id="bdb40-125">Get insights from analytics.</span></span>
  * <span data-ttu-id="bdb40-126">управлять пользователями.</span><span class="sxs-lookup"><span data-stu-id="bdb40-126">Manage users.</span></span>
* <span data-ttu-id="bdb40-127">Hello **портал разработчиков** служит в качестве основного веб-приложения hello для разработчиков, где они могут:</span><span class="sxs-lookup"><span data-stu-id="bdb40-127">hello **developer portal** serves as hello main web presence for developers, where they can:</span></span>
  
  * <span data-ttu-id="bdb40-128">читать документацию по API;</span><span class="sxs-lookup"><span data-stu-id="bdb40-128">Read API documentation.</span></span>
  * <span data-ttu-id="bdb40-129">Пробное использование API посредством hello интерактивной консоли.</span><span class="sxs-lookup"><span data-stu-id="bdb40-129">Try out an API via hello interactive console.</span></span>
  * <span data-ttu-id="bdb40-130">Создать учетную запись и подписаться ключи tooget API.</span><span class="sxs-lookup"><span data-stu-id="bdb40-130">Create an account and subscribe tooget API keys.</span></span>
  * <span data-ttu-id="bdb40-131">получить доступ к аналитике по использованию.</span><span class="sxs-lookup"><span data-stu-id="bdb40-131">Access analytics on their own usage.</span></span>

## <span data-ttu-id="bdb40-132"><a name="create-service-instance"></a>Создание экземпляра управления API</span><span class="sxs-lookup"><span data-stu-id="bdb40-132"><a name="create-service-instance"> </a>Create an API Management instance</span></span>
> [!NOTE]
> <span data-ttu-id="bdb40-133">toocomplete этого учебника необходима учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="bdb40-133">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="bdb40-134">Если ее нет, можно создать бесплатную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="bdb40-134">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="bdb40-135">Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][Azure Free Trial].</span><span class="sxs-lookup"><span data-stu-id="bdb40-135">For details, see [Azure Free Trial][Azure Free Trial].</span></span>
> 
> 

<span data-ttu-id="bdb40-136">Hello первый шаг при работе со службой управления API — toocreate экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="bdb40-136">hello first step in working with API Management is toocreate a service instance.</span></span> <span data-ttu-id="bdb40-137">Войдите в toohello [портала Azure] [ Azure Portal] и нажмите кнопку **New**, **Интернет + мобильные устройства**, **управления API**.</span><span class="sxs-lookup"><span data-stu-id="bdb40-137">Sign in toohello [Azure Portal][Azure Portal] and click **New**, **Web + Mobile**, **API Management**.</span></span>

![Новый экземпляр службы управления API ][api-management-create-instance-menu]

<span data-ttu-id="bdb40-139">Для **имя**, укажите toouse поддомене уникальное имя для URL-адрес службы hello.</span><span class="sxs-lookup"><span data-stu-id="bdb40-139">For **Name**, specify a unique sub-domain name toouse for hello service URL.</span></span>

<span data-ttu-id="bdb40-140">Выберите требуемого hello **подписки**, **группы ресурсов** и **расположение** для вашего экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="bdb40-140">Choose hello desired **Subscription**, **Resource group** and **Location** for your service instance.</span></span>

<span data-ttu-id="bdb40-141">Введите **Contoso Ltd.** для hello **название организации**и введите адрес электронной почты в hello **адрес электронной почты администратора** поля.</span><span class="sxs-lookup"><span data-stu-id="bdb40-141">Enter **Contoso Ltd.** for hello **Organization Name**, and enter your email address in hello **Administrator E-Mail** field.</span></span>

> [!NOTE]
> <span data-ttu-id="bdb40-142">Этот адрес электронной почты используется для получения уведомлений из системы управления API hello.</span><span class="sxs-lookup"><span data-stu-id="bdb40-142">This email address is used for notifications from hello API Management system.</span></span> <span data-ttu-id="bdb40-143">Дополнительные сведения см. в разделе [как tooconfigure уведомления и шаблонов в Azure API Management электронной почты][How tooconfigure notifications and email templates in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="bdb40-143">For more information, see [How tooconfigure notifications and email templates in Azure API Management][How tooconfigure notifications and email templates in Azure API Management].</span></span>
> 
> 

![Новая служба управления API][api-management-create-instance-step1]

<span data-ttu-id="bdb40-145">Экземпляры службы управления API доступны на трех уровнях: Developer, Standard и Premium.</span><span class="sxs-lookup"><span data-stu-id="bdb40-145">API Management service instances are available in three tiers: Developer, Standard, and Premium.</span></span>

> [!NOTE]
> <span data-ttu-id="bdb40-146">Hello уровень Developer предназначен для разработки, тестирования и пилотного развертывания программ API, где высокий уровень доступности не имеет значения.</span><span class="sxs-lookup"><span data-stu-id="bdb40-146">hello Developer Tier is for development, testing, and pilot API programs where high availability is not a concern.</span></span> <span data-ttu-id="bdb40-147">В hello Standard и Premium уровней можно масштабировать ваш toohandle число зарезервированных единиц большего объема трафика.</span><span class="sxs-lookup"><span data-stu-id="bdb40-147">In hello Standard and Premium tiers, you can scale your reserved unit count toohandle more traffic.</span></span> <span data-ttu-id="bdb40-148">Hello уровней Standard и Premium обеспечивают вашей службе управления API hello большинство вычислительной мощности и производительности.</span><span class="sxs-lookup"><span data-stu-id="bdb40-148">hello Standard and Premium tiers provide your API Management service with hello most processing power and performance.</span></span> <span data-ttu-id="bdb40-149">Вы можете изучать этот учебник, используя любой уровень.</span><span class="sxs-lookup"><span data-stu-id="bdb40-149">You can complete this tutorial by using any tier.</span></span> <span data-ttu-id="bdb40-150">Дополнительные сведения об уровнях управления API см. на странице с [расценками на службу управления API][API Management pricing].</span><span class="sxs-lookup"><span data-stu-id="bdb40-150">For more information about API Management tiers, see [API Management pricing][API Management pricing].</span></span>
> 
> 

<span data-ttu-id="bdb40-151">Нажмите кнопку **создать** toostart подготовки вашего экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="bdb40-151">Click **Create** toostart provisioning your service instance.</span></span>

![Новая служба управления API][api-management-instance-created]

<span data-ttu-id="bdb40-153">После создания экземпляра службы hello hello следующим шагом является toocreate или импортировать API.</span><span class="sxs-lookup"><span data-stu-id="bdb40-153">Once hello service instance is created, hello next step is toocreate or import an API.</span></span>

## <span data-ttu-id="bdb40-154"><a name="create-api"> </a>Импорт API</span><span class="sxs-lookup"><span data-stu-id="bdb40-154"><a name="create-api"> </a>Import an API</span></span>
<span data-ttu-id="bdb40-155">API представляет набор операций, которые могут быть вызваны клиентскими приложениями.</span><span class="sxs-lookup"><span data-stu-id="bdb40-155">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="bdb40-156">Операции API-интерфейса — tooexisting через прокси веб-службы.</span><span class="sxs-lookup"><span data-stu-id="bdb40-156">API operations are proxied tooexisting web services.</span></span>

<span data-ttu-id="bdb40-157">Вы можете создавать интерфейсы API (и добавлять операции) вручную, а также импортировать и то, и другое.</span><span class="sxs-lookup"><span data-stu-id="bdb40-157">APIs can be created (and operations can be added) manually, or they can be imported.</span></span> <span data-ttu-id="bdb40-158">В этом учебнике будет Импорт hello API образец калькулятора веб-служб, предоставляемых корпорацией Майкрософт и размещенных в Azure.</span><span class="sxs-lookup"><span data-stu-id="bdb40-158">In this tutorial, we will import hello API for a sample calculator web service provided by Microsoft and hosted on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="bdb40-159">Руководство по созданию API и вручную добавлять операций см. в разделе [как toocreate API-интерфейсы](api-management-howto-create-apis.md) и [как tooan tooadd операций API](api-management-howto-add-operations.md).</span><span class="sxs-lookup"><span data-stu-id="bdb40-159">For guidance on creating an API and manually adding operations, see [How toocreate APIs](api-management-howto-create-apis.md) and [How tooadd operations tooan API](api-management-howto-add-operations.md).</span></span>
> 
> 

<span data-ttu-id="bdb40-160">API-интерфейсы настроены с портала издателя hello.</span><span class="sxs-lookup"><span data-stu-id="bdb40-160">APIs are configured from hello publisher portal.</span></span> <span data-ttu-id="bdb40-161">tooreach его, нажмите кнопку **портал издателя** из инструментов службы hello.</span><span class="sxs-lookup"><span data-stu-id="bdb40-161">tooreach it, click **Publisher portal** from hello service toolbar.</span></span>

![Портал издателя][api-management-management-console]

<span data-ttu-id="bdb40-163">Калькулятор hello tooimport API, нажмите кнопку **API-интерфейсы** из hello **API управления** меню hello слева, а затем нажмите **импорта API**.</span><span class="sxs-lookup"><span data-stu-id="bdb40-163">tooimport hello calculator API, click **APIs** from hello **API Management** menu on hello left, and then click **Import API**.</span></span>

![Кнопка импорта API][api-management-import-api]

<span data-ttu-id="bdb40-165">Выполните следующие шаги tooconfigure hello калькулятора API hello.</span><span class="sxs-lookup"><span data-stu-id="bdb40-165">Perform hello following steps tooconfigure hello calculator API:</span></span>

1. <span data-ttu-id="bdb40-166">Нажмите кнопку **URL-адрес из**, введите **http://calcapi.cloudapp.net/calcapi.json** в hello **URL-адрес документа спецификации** текст и нажмите кнопку hello **Swagger**  переключатель.</span><span class="sxs-lookup"><span data-stu-id="bdb40-166">Click **From URL**, enter **http://calcapi.cloudapp.net/calcapi.json** into hello **Specification document URL** text box, and click hello **Swagger** radio button.</span></span>
2. <span data-ttu-id="bdb40-167">Тип **calc** в hello **суффикс URL-адрес API** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="bdb40-167">Type **calc** into hello **Web API URL suffix** text box.</span></span>
3. <span data-ttu-id="bdb40-168">Нажмите кнопку в hello **продуктов (необязательно)** и выберите **начальный**.</span><span class="sxs-lookup"><span data-stu-id="bdb40-168">Click in hello **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="bdb40-169">Нажмите кнопку **Сохранить** tooimport hello API.</span><span class="sxs-lookup"><span data-stu-id="bdb40-169">Click **Save** tooimport hello API.</span></span>

![Добавление нового API][api-management-import-new-api]

> [!NOTE]
> <span data-ttu-id="bdb40-171">**управления API** поддерживает импорт документа Swagger версий 1.2 и 2.0 .</span><span class="sxs-lookup"><span data-stu-id="bdb40-171">**API Management** currently supports both 1.2 and 2.0 version of Swagger document for import.</span></span> <span data-ttu-id="bdb40-172">Хотя в [спецификации по Swagger 2.0](http://swagger.io/specification) заявлено, что свойства `host`, `basePath` и `schemes` являются необязательными, ваш документ Swagger 2.0 **ДОЛЖЕН** содержать их — в противном случае он не импортируется.</span><span class="sxs-lookup"><span data-stu-id="bdb40-172">Make sure that, even though [Swagger 2.0 specification](http://swagger.io/specification) declares that `host`, `basePath`, and `schemes` properties are optional, your Swagger 2.0 document **MUST** contain those properties; otherwise it won't get imported.</span></span> 
> 
> 

<span data-ttu-id="bdb40-173">После импорта hello API hello сводной страницы для hello API отображается в портал издателя hello.</span><span class="sxs-lookup"><span data-stu-id="bdb40-173">Once hello API is imported, hello summary page for hello API is displayed in hello publisher portal.</span></span>

![Сводные данные API][api-management-imported-api-summary]

<span data-ttu-id="bdb40-175">Hello API разделе есть несколько вкладок.</span><span class="sxs-lookup"><span data-stu-id="bdb40-175">hello API section has several tabs.</span></span> <span data-ttu-id="bdb40-176">Hello **Сводка** вкладке отображаются основные показатели и сведения о hello API.</span><span class="sxs-lookup"><span data-stu-id="bdb40-176">hello **Summary** tab displays basic metrics and information about hello API.</span></span> <span data-ttu-id="bdb40-177">Hello [параметры](api-management-howto-create-apis.md#configure-api-settings) вкладка — tooview и измените hello конфигурации для API.</span><span class="sxs-lookup"><span data-stu-id="bdb40-177">hello [Settings](api-management-howto-create-apis.md#configure-api-settings) tab is used tooview and edit hello configuration for an API.</span></span> <span data-ttu-id="bdb40-178">Hello [операции](api-management-howto-add-operations.md) вкладка — операций hello toomanage используется API-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="bdb40-178">hello [Operations](api-management-howto-add-operations.md) tab is used toomanage hello API's operations.</span></span> <span data-ttu-id="bdb40-179">Hello **безопасности** вкладка может быть tooconfigure используется проверка подлинности шлюза для hello внутреннему серверу с помощью обычной проверки подлинности или [взаимной проверки подлинности сертификатов](api-management-howto-mutual-certificates.md)и tooconfigure [ Проверка подлинности пользователя с помощью OAuth 2.0](api-management-howto-oauth2.md).</span><span class="sxs-lookup"><span data-stu-id="bdb40-179">hello **Security** tab can be used tooconfigure gateway authentication for hello backend server by using Basic authentication or [mutual certificate authentication](api-management-howto-mutual-certificates.md), and tooconfigure [user authorization by using OAuth 2.0](api-management-howto-oauth2.md).</span></span>  <span data-ttu-id="bdb40-180">Hello **проблемы** вкладка — используется tooview неполадках, собранную hello разработчики, использующие собственные интерфейсы API.</span><span class="sxs-lookup"><span data-stu-id="bdb40-180">hello **Issues** tab is used tooview issues reported by hello developers who are using your APIs.</span></span> <span data-ttu-id="bdb40-181">Hello **продуктов** вкладка — используется tooconfigure hello продуктов, которые содержат этот API.</span><span class="sxs-lookup"><span data-stu-id="bdb40-181">hello **Products** tab is used tooconfigure hello products that contain this API.</span></span>

<span data-ttu-id="bdb40-182">По умолчанию каждый экземпляр API управления поставляется с двумя демонстрационными продуктами:</span><span class="sxs-lookup"><span data-stu-id="bdb40-182">By default, each API Management instance comes with two sample products:</span></span>

* <span data-ttu-id="bdb40-183">**Starter**</span><span class="sxs-lookup"><span data-stu-id="bdb40-183">**Starter**</span></span>
* <span data-ttu-id="bdb40-184">**Unlimited**</span><span class="sxs-lookup"><span data-stu-id="bdb40-184">**Unlimited**</span></span>

<span data-ttu-id="bdb40-185">В этом учебнике hello базовый API-Интерфейс калькулятора добавлена продукт начальный toohello при импорте hello API.</span><span class="sxs-lookup"><span data-stu-id="bdb40-185">In this tutorial, hello Basic Calculator API was added toohello Starter product when hello API was imported.</span></span>

<span data-ttu-id="bdb40-186">В порядке toomake вызовы tooan API разработчики сначала необходимо подписаться tooa продукт, который дает им доступ tooit.</span><span class="sxs-lookup"><span data-stu-id="bdb40-186">In order toomake calls tooan API, developers must first subscribe tooa product that gives them access tooit.</span></span> <span data-ttu-id="bdb40-187">Разработчики могут подписаться tooproducts на портале разработчиков hello или Администраторы могут подписаться tooproducts разработчики hello портала издателя.</span><span class="sxs-lookup"><span data-stu-id="bdb40-187">Developers can subscribe tooproducts in hello developer portal, or administrators can subscribe developers tooproducts in hello publisher portal.</span></span> <span data-ttu-id="bdb40-188">Вы являетесь администратором, с момента создания экземпляра API управления hello в hello предыдущие шаги в учебнике hello, вы уже подписанных tooevery продукта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="bdb40-188">You are an administrator since you created hello API Management instance in hello previous steps in hello tutorial, so you are already subscribed tooevery product by default.</span></span>

## <span data-ttu-id="bdb40-189"><a name="call-operation"></a>Вызова операции с портала разработчиков hello</span><span class="sxs-lookup"><span data-stu-id="bdb40-189"><a name="call-operation"> </a>Call an operation from hello developer portal</span></span>
<span data-ttu-id="bdb40-190">Операции могут вызываться непосредственно из портала разработчиков hello, который предоставляет удобный способ tooview и протестировать hello операции API-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="bdb40-190">Operations can be called directly from hello developer portal, which provides a convenient way tooview and test hello operations of an API.</span></span> <span data-ttu-id="bdb40-191">На этом шаге учебника будет вызывать hello основные калькулятора API-Интерфейсы **добавьте два целых числа** операции.</span><span class="sxs-lookup"><span data-stu-id="bdb40-191">In this tutorial step, you will call hello Basic Calculator API's **Add two integers** operation.</span></span> <span data-ttu-id="bdb40-192">Нажмите кнопку **портал разработчиков** меню hello hello верхнему правому углу портала издателя hello.</span><span class="sxs-lookup"><span data-stu-id="bdb40-192">Click **Developer portal** from hello menu at hello top right of hello publisher portal.</span></span>

![Портал разработчика][api-management-developer-portal-menu]

<span data-ttu-id="bdb40-194">Нажмите кнопку **API-интерфейсы** hello верхнем меню, и нажмите кнопку **калькулятору** toosee hello доступных операций.</span><span class="sxs-lookup"><span data-stu-id="bdb40-194">Click **APIs** from hello top menu, and then click **Basic Calculator** toosee hello available operations.</span></span>

![Портал разработчика][api-management-developer-portal-calc-api]

<span data-ttu-id="bdb40-196">Обратите внимание, описания образец hello и параметры, которые были импортированы вместе с hello API и операции, предоставляя документации для разработчиков hello, которые будут использовать эту операцию.</span><span class="sxs-lookup"><span data-stu-id="bdb40-196">Note hello sample descriptions and parameters that were imported along with hello API and operations, providing documentation for hello developers that will use this operation.</span></span> <span data-ttu-id="bdb40-197">Эти описания можно также добавить при добавлении операций вручную.</span><span class="sxs-lookup"><span data-stu-id="bdb40-197">These descriptions can also be added when operations are added manually.</span></span>

<span data-ttu-id="bdb40-198">toocall hello **добавьте два целых числа** операцию, нажмите кнопку **опробовать**.</span><span class="sxs-lookup"><span data-stu-id="bdb40-198">toocall hello **Add two integers** operation, click **Try it**.</span></span>

![Попробовать][api-management-developer-portal-calc-api-console]

<span data-ttu-id="bdb40-200">Можно ввести некоторые значения для параметров hello или оставьте значения по умолчанию hello и нажмите кнопку **отправки**.</span><span class="sxs-lookup"><span data-stu-id="bdb40-200">You can enter some values for hello parameters or keep hello defaults, and then click **Send**.</span></span>

![HTTP Get][api-management-invoke-get]

<span data-ttu-id="bdb40-202">После вызова операции портал разработчиков hello отображает hello **состояние ответа**, hello **заголовки ответа**и любые **содержимого отклика**.</span><span class="sxs-lookup"><span data-stu-id="bdb40-202">After an operation is invoked, hello developer portal displays hello **Response status**, hello **Response headers**, and any **Response content**.</span></span>

![Ответ][api-management-invoke-get-response]

## <span data-ttu-id="bdb40-204"><a name="view-analytics"> </a>Просмотр аналитики</span><span class="sxs-lookup"><span data-stu-id="bdb40-204"><a name="view-analytics"> </a>View analytics</span></span>
<span data-ttu-id="bdb40-205">Аналитика tooview для калькулятору портал издателя задней toohello коммутатора, выбрав **управление** меню hello hello верхнему правому углу портала разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="bdb40-205">tooview analytics for Basic Calculator, switch back toohello publisher portal by selecting **Manage** from hello menu at hello top right of hello developer portal.</span></span>

![Управление][api-management-manage-menu]

<span data-ttu-id="bdb40-207">Hello представление по умолчанию для портала издателя hello — hello **мониторинга**, предоставляющее обзор вашего экземпляра управления API.</span><span class="sxs-lookup"><span data-stu-id="bdb40-207">hello default view for hello publisher portal is hello **Dashboard**, which provides an overview of your API Management instance.</span></span>

![Панель мониторинга][api-management-dashboard]

<span data-ttu-id="bdb40-209">Наведите указатель мыши hello на диаграмме hello для **калькулятору** toosee hello определенных показателей использования hello hello API для определенного периода времени.</span><span class="sxs-lookup"><span data-stu-id="bdb40-209">Hover hello mouse over hello chart for **Basic Calculator** toosee hello specific metrics for hello usage of hello API for a given time period.</span></span>

> [!NOTE]
> <span data-ttu-id="bdb40-210">Если вы не видите все линии на диаграмме, переключиться назад toohello портал разработчиков и выполнять некоторые вызовы hello API, подождите несколько секунд и затем вернуться toohello панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="bdb40-210">If you don't see any lines on your chart, switch back toohello developer portal and make some calls into hello API, wait a few moments, and then come back toohello dashboard.</span></span>
> 
> 

<span data-ttu-id="bdb40-211">Нажмите кнопку **Просмотр сведений о** tooview hello Сводная страница hello API, включая увеличения hello отображаемых метрик.</span><span class="sxs-lookup"><span data-stu-id="bdb40-211">Click **View Details** tooview hello summary page for hello API, including a larger version of hello displayed metrics.</span></span>

![Аналитика][api-management-mouse-over]

![Сводка][api-management-api-summary-metrics]

<span data-ttu-id="bdb40-214">Подробные метрики и отчеты, щелкните **Analytics** из hello **управления API** меню слева hello.</span><span class="sxs-lookup"><span data-stu-id="bdb40-214">For detailed metrics and reports, click **Analytics** from hello **API Management** menu on hello left.</span></span>

![Обзор][api-management-analytics-overview]

<span data-ttu-id="bdb40-216">Hello **Analytics** раздел имеет hello следующие четыре вкладки:</span><span class="sxs-lookup"><span data-stu-id="bdb40-216">hello **Analytics** section has hello following four tabs:</span></span>

* <span data-ttu-id="bdb40-217">**Краткий обзор** предоставляет общее использование и метрики работоспособности также hello крупнейших разработчиков лучших продуктов, верхнем API-интерфейсы операции и top.</span><span class="sxs-lookup"><span data-stu-id="bdb40-217">**At a glance** provides overall usage and health metrics, as well as hello top developers, top products, top APIs, and top operations.</span></span>
* <span data-ttu-id="bdb40-218">**Использование** содержит обзор деталей вызовов API и полосы пропускания, включая географическое представление.</span><span class="sxs-lookup"><span data-stu-id="bdb40-218">**Usage** provides an in-depth look at API calls and bandwidth, including a geographical representation.</span></span>
* <span data-ttu-id="bdb40-219">**Работоспособность** содержит коды состояний, показатели успешных попаданий в кэш и времена ответов API и служб.</span><span class="sxs-lookup"><span data-stu-id="bdb40-219">**Health** focuses on status codes, cache success rates, response times, and API and service response times.</span></span>
* <span data-ttu-id="bdb40-220">**Действие** предоставляет отчеты, которые детализируют на конкретное действие hello, developer, продукт, API и операции.</span><span class="sxs-lookup"><span data-stu-id="bdb40-220">**Activity** provides reports that drill down on hello specific activity by developer, product, API, and operation.</span></span>

## <span data-ttu-id="bdb40-221"><a name="next-steps"> </a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bdb40-221"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="bdb40-222">Узнайте, каким образом слишком[защиты API с пределы скорости](api-management-howto-product-with-rules.md).</span><span class="sxs-lookup"><span data-stu-id="bdb40-222">Learn how too[Protect your API with rate limits](api-management-howto-product-with-rules.md).</span></span>

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add hello new API tooa product]: #add-api-to-product
[Subscribe toohello product that contains hello API]: #subscribe
[Call an operation from hello Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How toomanage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How tooconfigure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
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
