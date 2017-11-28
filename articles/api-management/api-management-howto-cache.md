---
title: "кэширование tooimprove производительности в Azure API Management aaaAdd | Документы Microsoft"
description: "Узнайте, как загрузить tooimprove hello задержки, потребление пропускной способности и веб-службы для вызовов службы управления API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 740f6a27-8323-474d-ade2-828ae0c75e7a
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 056ab7cf788218327e30bd5c028b76e3b1977fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-caching-tooimprove-performance-in-azure-api-management"></a><span data-ttu-id="134ac-103">Добавить кэширование tooimprove производительность в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="134ac-103">Add caching tooimprove performance in Azure API Management</span></span>
<span data-ttu-id="134ac-104">Операции в управлении API можно настроить для кэширования ответов.</span><span class="sxs-lookup"><span data-stu-id="134ac-104">Operations in API Management can be configured for response caching.</span></span> <span data-ttu-id="134ac-105">Кэширование ответов может значительно уменьшить время задержки API, потребляемую пропускную способность, и нагрузку на веб-службу применительно к данным, которые изменяются редко.</span><span class="sxs-lookup"><span data-stu-id="134ac-105">Response caching can significantly reduce API latency, bandwidth consumption, and web service load for data that does not change frequently.</span></span>

<span data-ttu-id="134ac-106">В этом руководстве показано, как ответ tooadd кэширование для API и настроить политики для операций Echo API пример hello.</span><span class="sxs-lookup"><span data-stu-id="134ac-106">This guide shows you how tooadd response caching for your API and configure policies for hello sample Echo API operations.</span></span> <span data-ttu-id="134ac-107">Затем можно вызвать операцию hello от разработчика hello портала tooverify кэширования в действии.</span><span class="sxs-lookup"><span data-stu-id="134ac-107">You can then call hello operation from hello developer portal tooverify caching in action.</span></span>

> [!NOTE]
> <span data-ttu-id="134ac-108">Сведения о кэшировании элементов по ключу с помощью выражений политики см. в статье [Пользовательское кэширование в службе управления API Azure](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="134ac-108">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="134ac-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="134ac-109">Prerequisites</span></span>
<span data-ttu-id="134ac-110">Перед следующей hello шаги данного руководства, необходимо иметь экземпляра службы управления API с API и настройки продукта.</span><span class="sxs-lookup"><span data-stu-id="134ac-110">Before following hello steps in this guide, you must have an API Management service instance with an API and a product configured.</span></span> <span data-ttu-id="134ac-111">Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.</span><span class="sxs-lookup"><span data-stu-id="134ac-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

## <span data-ttu-id="134ac-112"><a name="configure-caching"> </a>Настройка операции для кэширования</span><span class="sxs-lookup"><span data-stu-id="134ac-112"><a name="configure-caching"> </a>Configure an operation for caching</span></span>
<span data-ttu-id="134ac-113">На этом шаге вы просмотрите hello кэширование параметры hello **получить ресурс (с кэшированием)** операции образца hello Echo API.</span><span class="sxs-lookup"><span data-stu-id="134ac-113">In this step, you will review hello caching settings of hello **GET Resource (cached)** operation of hello sample Echo API.</span></span>

> [!NOTE]
> <span data-ttu-id="134ac-114">Каждый экземпляр службы управления API поставляется предварительно настроенных Echo API-интерфейсы, можно использовать tooexperiment с и Дополнительные сведения о службе управления API.</span><span class="sxs-lookup"><span data-stu-id="134ac-114">Each API Management service instance comes preconfigured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="134ac-115">Дополнительные сведения см. в статье [Начало работы со службой управления Azure API][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="134ac-115">For more information, see [Get started with Azure API Management][Get started with Azure API Management].</span></span>
> 
> 

<span data-ttu-id="134ac-116">tooget работу, нажмите кнопку **портал издателя** в hello портала Azure для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="134ac-116">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="134ac-117">Откроется портал издателя управления API toohello.</span><span class="sxs-lookup"><span data-stu-id="134ac-117">This takes you toohello API Management publisher portal.</span></span>

![Портал издателя][api-management-management-console]

<span data-ttu-id="134ac-119">Нажмите кнопку **API-интерфейсы** из hello **API управления** меню hello слева, а затем нажмите **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="134ac-119">Click **APIs** from hello **API Management** menu on hello left, and then click **Echo API**.</span></span>

![Echo API][api-management-echo-api]

<span data-ttu-id="134ac-121">Щелкните hello **операции** , а затем щелкните hello **получить ресурс (с кэшированием)** операции hello **операции** списка.</span><span class="sxs-lookup"><span data-stu-id="134ac-121">Click hello **Operations** tab, and then click hello **GET Resource (cached)** operation from hello **Operations** list.</span></span>

![Операции интерфейса Echo API][api-management-echo-api-operations]

<span data-ttu-id="134ac-123">Нажмите кнопку hello **кэширование** hello tooview вкладку Параметры для этой операции кэширования.</span><span class="sxs-lookup"><span data-stu-id="134ac-123">Click hello **Caching** tab tooview hello caching settings for this operation.</span></span>

![Вкладка "Кэширование"][api-management-caching-tab]

<span data-ttu-id="134ac-125">кэширование tooenable для операции select hello **включить** флажок.</span><span class="sxs-lookup"><span data-stu-id="134ac-125">tooenable caching for an operation, select hello **Enable** check box.</span></span> <span data-ttu-id="134ac-126">В этом примере кэширование включено.</span><span class="sxs-lookup"><span data-stu-id="134ac-126">In this example, caching is enabled.</span></span>

<span data-ttu-id="134ac-127">Каждый ответ операции различаемых по значениям hello в hello **происходит изменение параметров строки запроса** и **Vary заголовками** поля.</span><span class="sxs-lookup"><span data-stu-id="134ac-127">Each operation response is keyed, based on hello values in hello **Vary by query string parameters** and **Vary by headers** fields.</span></span> <span data-ttu-id="134ac-128">Если требуется несколько ответов на основе параметров строки запроса или заголовки toocache, можно настроить их в следующих двух полей.</span><span class="sxs-lookup"><span data-stu-id="134ac-128">If you want toocache multiple responses based on query string parameters or headers, you can configure them in these two fields.</span></span>

<span data-ttu-id="134ac-129">**Длительность** указывает интервал срока действия hello hello кэширования ответов.</span><span class="sxs-lookup"><span data-stu-id="134ac-129">**Duration** specifies hello expiration interval of hello cached responses.</span></span> <span data-ttu-id="134ac-130">В этом примере — интервал приветствия **3600** секунд — эквивалент tooone час.</span><span class="sxs-lookup"><span data-stu-id="134ac-130">In this example, hello interval is **3600** seconds, which is equivalent tooone hour.</span></span>

<span data-ttu-id="134ac-131">С помощью конфигурации кэширования в этом примере hello, hello первый запрос toohello **получить ресурс (с кэшированием)** операция возвращает ответ от службы внутренних hello.</span><span class="sxs-lookup"><span data-stu-id="134ac-131">Using hello caching configuration in this example, hello first request toohello **GET Resource (cached)** operation returns a response from hello backend service.</span></span> <span data-ttu-id="134ac-132">Этот ответ кэшируются, ключом которых является указанный hello заголовки и запрос строковых параметров.</span><span class="sxs-lookup"><span data-stu-id="134ac-132">This response will be cached, keyed by hello specified headers and query string parameters.</span></span> <span data-ttu-id="134ac-133">Последующие вызовы операции toohello с соответствующими параметрами, будет иметь hello ответ возвращается, пока не истечет интервал длительности hello кэша в кэше.</span><span class="sxs-lookup"><span data-stu-id="134ac-133">Subsequent calls toohello operation, with matching parameters, will have hello cached response returned, until hello cache duration interval has expired.</span></span>

## <span data-ttu-id="134ac-134"><a name="caching-policies"></a>Hello проверки политики кэширования</span><span class="sxs-lookup"><span data-stu-id="134ac-134"><a name="caching-policies"> </a>Review hello caching policies</span></span>
<span data-ttu-id="134ac-135">На этом шаге, проверьте параметры для hello кэширования hello **получить ресурс (с кэшированием)** операции образца hello Echo API.</span><span class="sxs-lookup"><span data-stu-id="134ac-135">In this step, you review hello caching settings for hello **GET Resource (cached)** operation of hello sample Echo API.</span></span>

<span data-ttu-id="134ac-136">Если настроены параметры кэширования для операции на hello **кэширование** вкладке кэширования для операции hello добавляются политики.</span><span class="sxs-lookup"><span data-stu-id="134ac-136">When caching settings are configured for an operation on hello **Caching** tab, caching policies are added for hello operation.</span></span> <span data-ttu-id="134ac-137">Эти политики можно просматривать и редактировать в редакторе политики hello.</span><span class="sxs-lookup"><span data-stu-id="134ac-137">These policies can be viewed and edited in hello policy editor.</span></span>

<span data-ttu-id="134ac-138">Нажмите кнопку **политики** из hello **API управления** меню hello слева, а затем выберите **Echo API и получить ресурс (с кэшированием)** из hello **операции**раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="134ac-138">Click **Policies** from hello **API Management** menu on hello left, and then select **Echo API / GET Resource (cached)** from hello **Operation** drop-down list.</span></span>

![Операция с диапазоном политик][api-management-operation-dropdown]

<span data-ttu-id="134ac-140">При этом в редактор политики hello отображаются hello политик для этой операции.</span><span class="sxs-lookup"><span data-stu-id="134ac-140">This displays hello policies for this operation in hello policy editor.</span></span>

![Редактор политик API Management][api-management-policy-editor]

<span data-ttu-id="134ac-142">Определение политики Hello для этой операции включает политик hello, определяющих hello конфигурации кэша, были проверены с помощью hello **кэширование** вкладку в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="134ac-142">hello policy definition for this operation includes hello policies that define hello caching configuration that were reviewed using hello **Caching** tab in hello previous step.</span></span>

```xml
<policies>
    <inbound>
        <base />
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">
            <vary-by-header>Accept</vary-by-header>
            <vary-by-header>Accept-Charset</vary-by-header>
        </cache-lookup>
        <rewrite-uri template="/resource" />
    </inbound>
    <outbound>
        <base />
        <cache-store caching-mode="cache-on" duration="3600" />
    </outbound>
</policies>
```

> [!NOTE]
> <span data-ttu-id="134ac-143">Политики в редакторе hello политики кэширования toohello изменения будут отражены на hello **кэширование** вкладке операции и наоборот.</span><span class="sxs-lookup"><span data-stu-id="134ac-143">Changes made toohello caching policies in hello policy editor will be reflected on hello **Caching** tab of an operation, and vice-versa.</span></span>
> 
> 

## <span data-ttu-id="134ac-144"><a name="test-operation"></a>Вызов операции и тестирование кэширования hello</span><span class="sxs-lookup"><span data-stu-id="134ac-144"><a name="test-operation"> </a>Call an operation and test hello caching</span></span>
<span data-ttu-id="134ac-145">toosee hello кэширования в действии, можно вызвать операцию hello с портала разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="134ac-145">toosee hello caching in action, we can call hello operation from hello developer portal.</span></span> <span data-ttu-id="134ac-146">Нажмите кнопку **портал разработчиков** в правом верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="134ac-146">Click **Developer portal** in hello top right menu.</span></span>

![Портал разработчика][api-management-developer-portal-menu]

<span data-ttu-id="134ac-148">Нажмите кнопку **API-интерфейсы** в верхнем меню hello, а затем выберите **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="134ac-148">Click **APIs** in hello top menu, and then select **Echo API**.</span></span>

![Echo API][api-management-apis-echo-api]

> <span data-ttu-id="134ac-150">Если у вас есть только один API-Интерфейс настройки или видимым tooyour учетной записи, выбрав API-интерфейсы вы перейдете непосредственно toohello операции для этого API-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="134ac-150">If you have only one API configured or visible tooyour account, then clicking APIs takes you directly toohello operations for that API.</span></span>
> 
> 

<span data-ttu-id="134ac-151">Выберите hello **получить ресурс (с кэшированием)** операции, а затем щелкните **откройте консоль**.</span><span class="sxs-lookup"><span data-stu-id="134ac-151">Select hello **GET Resource (cached)** operation, and then click **Open Console**.</span></span>

![Открытие консоли][api-management-open-console]

<span data-ttu-id="134ac-153">Hello консоли позволяет выполнять операции tooinvoke непосредственно с портала разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="134ac-153">hello console allows you tooinvoke operations directly from hello developer portal.</span></span>

![Консоль][api-management-console]

<span data-ttu-id="134ac-155">Сохраните значения по умолчанию hello для **param1** и **param2**.</span><span class="sxs-lookup"><span data-stu-id="134ac-155">Keep hello default values for **param1** and **param2**.</span></span>

<span data-ttu-id="134ac-156">Здравствуйте, выберите нужный ключ из hello **ключ подписки** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="134ac-156">Select hello desired key from hello **subscription-key** drop-down list.</span></span> <span data-ttu-id="134ac-157">Если ваша учетная запись содержит только одну подписку, он уже будет выбран.</span><span class="sxs-lookup"><span data-stu-id="134ac-157">If your account has only one subscription, it will already be selected.</span></span>

<span data-ttu-id="134ac-158">Введите **sampleheader:value1** в hello **заголовки запроса** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="134ac-158">Enter **sampleheader:value1** in hello **Request headers** text box.</span></span>

<span data-ttu-id="134ac-159">Нажмите кнопку **HTTP Get** и запишите hello заголовки ответа.</span><span class="sxs-lookup"><span data-stu-id="134ac-159">Click **HTTP Get** and make a note of hello response headers.</span></span>

<span data-ttu-id="134ac-160">Введите **sampleheader:value2** в hello **заголовки запроса** текстовое поле и нажмите кнопку **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="134ac-160">Enter **sampleheader:value2** in hello **Request headers** text box, and then click **HTTP Get**.</span></span>

<span data-ttu-id="134ac-161">Обратите внимание, что значение hello **sampleheader** по-прежнему **значение1** в ответ hello.</span><span class="sxs-lookup"><span data-stu-id="134ac-161">Note that hello value of **sampleheader** is still **value1** in hello response.</span></span> <span data-ttu-id="134ac-162">Попробуйте несколько различных значений и обратите внимание, что hello кэшированного ответа от первого вызова hello возвращается.</span><span class="sxs-lookup"><span data-stu-id="134ac-162">Try some different values and note that hello cached response from hello first call is returned.</span></span>

<span data-ttu-id="134ac-163">Введите **25** в hello **param2** , а затем щелкните **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="134ac-163">Enter **25** into hello **param2** field, and then click **HTTP Get**.</span></span>

<span data-ttu-id="134ac-164">Обратите внимание, что значение hello **sampleheader** в hello ответа является **value2**.</span><span class="sxs-lookup"><span data-stu-id="134ac-164">Note that hello value of **sampleheader** in hello response is now **value2**.</span></span> <span data-ttu-id="134ac-165">Поскольку hello результаты операции с ключами, соответствующими строки запроса, не был возвращен hello предыдущего кэшированного ответа.</span><span class="sxs-lookup"><span data-stu-id="134ac-165">Because hello operation results are keyed by query string, hello previous cached response was not returned.</span></span>

## <span data-ttu-id="134ac-166"><a name="next-steps"> </a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="134ac-166"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="134ac-167">Дополнительные сведения о кэшировании политик см. в разделе [политики кэширования] [ Caching policies] в hello [Справочник по политикам управления API][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="134ac-167">For more information about caching policies, see [Caching policies][Caching policies] in hello [API Management policy reference][API Management policy reference].</span></span>
* <span data-ttu-id="134ac-168">Сведения о кэшировании элементов по ключу с помощью выражений политики см. в статье [Пользовательское кэширование в службе управления API Azure](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="134ac-168">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>

[api-management-management-console]: ./media/api-management-howto-cache/api-management-management-console.png
[api-management-echo-api]: ./media/api-management-howto-cache/api-management-echo-api.png
[api-management-echo-api-operations]: ./media/api-management-howto-cache/api-management-echo-api-operations.png
[api-management-caching-tab]: ./media/api-management-howto-cache/api-management-caching-tab.png
[api-management-operation-dropdown]: ./media/api-management-howto-cache/api-management-operation-dropdown.png
[api-management-policy-editor]: ./media/api-management-howto-cache/api-management-policy-editor.png
[api-management-developer-portal-menu]: ./media/api-management-howto-cache/api-management-developer-portal-menu.png
[api-management-apis-echo-api]: ./media/api-management-howto-cache/api-management-apis-echo-api.png
[api-management-open-console]: ./media/api-management-howto-cache/api-management-open-console.png
[api-management-console]: ./media/api-management-howto-cache/api-management-console.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review hello caching policies]: #caching-policies
[Call an operation and test hello caching]: #test-operation
[Next steps]: #next-steps
