---
title: "Добавление кэширования для повышения производительности в службе управления API Azure | Документация Майкрософт"
description: "Сведения об уменьшении задержки, использования пропускной способности и загрузки веб-службы для вызовов службы управления API."
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
ms.openlocfilehash: 59c595f0d5ce849f44c46fdb6cab0b44d35fffa0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="add-caching-to-improve-performance-in-azure-api-management"></a><span data-ttu-id="10fe1-103">Добавление кэширования для повышения производительности в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="10fe1-103">Add caching to improve performance in Azure API Management</span></span>
<span data-ttu-id="10fe1-104">Операции в управлении API можно настроить для кэширования ответов.</span><span class="sxs-lookup"><span data-stu-id="10fe1-104">Operations in API Management can be configured for response caching.</span></span> <span data-ttu-id="10fe1-105">Кэширование ответов может значительно уменьшить время задержки API, потребляемую пропускную способность, и нагрузку на веб-службу применительно к данным, которые изменяются редко.</span><span class="sxs-lookup"><span data-stu-id="10fe1-105">Response caching can significantly reduce API latency, bandwidth consumption, and web service load for data that does not change frequently.</span></span>

<span data-ttu-id="10fe1-106">В этом руководстве показано, как добавить кэширование ответов для API и настроить политики для примеров операций Echo API.</span><span class="sxs-lookup"><span data-stu-id="10fe1-106">This guide shows you how to add response caching for your API and configure policies for the sample Echo API operations.</span></span> <span data-ttu-id="10fe1-107">Затем можно вызвать операцию из портала разработчика, чтобы проверить кэширование в действии.</span><span class="sxs-lookup"><span data-stu-id="10fe1-107">You can then call the operation from the developer portal to verify caching in action.</span></span>

> [!NOTE]
> <span data-ttu-id="10fe1-108">Сведения о кэшировании элементов по ключу с помощью выражений политики см. в статье [Пользовательское кэширование в службе управления API Azure](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="10fe1-108">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="10fe1-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="10fe1-109">Prerequisites</span></span>
<span data-ttu-id="10fe1-110">Прежде чем выполнять действия из этого руководства, необходимо настроить экземпляр службы управления API с API и продуктом.</span><span class="sxs-lookup"><span data-stu-id="10fe1-110">Before following the steps in this guide, you must have an API Management service instance with an API and a product configured.</span></span> <span data-ttu-id="10fe1-111">Если экземпляр службы управления API еще не создан, см. раздел [Создание экземпляра управления API][Create an API Management service instance] в руководстве [Начало работы со службой управления Azure API][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="10fe1-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

## <span data-ttu-id="10fe1-112"><a name="configure-caching"> </a>Настройка операции для кэширования</span><span class="sxs-lookup"><span data-stu-id="10fe1-112"><a name="configure-caching"> </a>Configure an operation for caching</span></span>
<span data-ttu-id="10fe1-113">На этом этапе необходимо проверить параметры кэширования операции **GET Resource (cached)** примера Echo API.</span><span class="sxs-lookup"><span data-stu-id="10fe1-113">In this step, you will review the caching settings of the **GET Resource (cached)** operation of the sample Echo API.</span></span>

> [!NOTE]
> <span data-ttu-id="10fe1-114">В каждом экземпляре службы управления API предварительно настроен Echo API, с которым можно экспериментировать при изучении службы управления API.</span><span class="sxs-lookup"><span data-stu-id="10fe1-114">Each API Management service instance comes preconfigured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="10fe1-115">Дополнительные сведения см. в статье [Начало работы со службой управления Azure API][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="10fe1-115">For more information, see [Get started with Azure API Management][Get started with Azure API Management].</span></span>
> 
> 

<span data-ttu-id="10fe1-116">Чтобы начать работу, щелкните **Publisher portal** (Портал издателя) на портале Azure для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="10fe1-116">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="10fe1-117">Будет открыт портал издателя службы управления API.</span><span class="sxs-lookup"><span data-stu-id="10fe1-117">This takes you to the API Management publisher portal.</span></span>

![Портал издателя][api-management-management-console]

<span data-ttu-id="10fe1-119">Щелкните **API** в меню **Управление API** слева, а затем выберите **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="10fe1-119">Click **APIs** from the **API Management** menu on the left, and then click **Echo API**.</span></span>

![Echo API][api-management-echo-api]

<span data-ttu-id="10fe1-121">Перейдите на вкладку **Операции** и в списке **Операции** выберите операцию **GET Resource (cached)**.</span><span class="sxs-lookup"><span data-stu-id="10fe1-121">Click the **Operations** tab, and then click the **GET Resource (cached)** operation from the **Operations** list.</span></span>

![Операции интерфейса Echo API][api-management-echo-api-operations]

<span data-ttu-id="10fe1-123">Перейдите на вкладку **Кэширование** , чтобы просмотреть параметры кэширования для этой операции.</span><span class="sxs-lookup"><span data-stu-id="10fe1-123">Click the **Caching** tab to view the caching settings for this operation.</span></span>

![Вкладка "Кэширование"][api-management-caching-tab]

<span data-ttu-id="10fe1-125">Чтобы включить кэширование для операции, установите флажок **Включить** .</span><span class="sxs-lookup"><span data-stu-id="10fe1-125">To enable caching for an operation, select the **Enable** check box.</span></span> <span data-ttu-id="10fe1-126">В этом примере кэширование включено.</span><span class="sxs-lookup"><span data-stu-id="10fe1-126">In this example, caching is enabled.</span></span>

<span data-ttu-id="10fe1-127">Каждый ответ операции содержит ключ на основе значений в полях **В зависимости от параметров строки запроса** и **В зависимости от заголовков**.</span><span class="sxs-lookup"><span data-stu-id="10fe1-127">Each operation response is keyed, based on the values in the **Vary by query string parameters** and **Vary by headers** fields.</span></span> <span data-ttu-id="10fe1-128">Если вы хотите кэшировать несколько ответов на основании параметров строки запроса или заголовков, то такой режим можно настроить с помощью этих полей.</span><span class="sxs-lookup"><span data-stu-id="10fe1-128">If you want to cache multiple responses based on query string parameters or headers, you can configure them in these two fields.</span></span>

<span data-ttu-id="10fe1-129">**Длительность** указывает интервал срока действия кэшированных ответов.</span><span class="sxs-lookup"><span data-stu-id="10fe1-129">**Duration** specifies the expiration interval of the cached responses.</span></span> <span data-ttu-id="10fe1-130">В этом примере интервал составляет **3600** секунд, что эквивалентно одному часу.</span><span class="sxs-lookup"><span data-stu-id="10fe1-130">In this example, the interval is **3600** seconds, which is equivalent to one hour.</span></span>

<span data-ttu-id="10fe1-131">При использовании конфигурации кэширования в этом примере на первый запрос операции **GET Resource (cached)** возвращается ответ из серверной службы.</span><span class="sxs-lookup"><span data-stu-id="10fe1-131">Using the caching configuration in this example, the first request to the **GET Resource (cached)** operation returns a response from the backend service.</span></span> <span data-ttu-id="10fe1-132">Этот ответ будет кэшироваться, а также отмечаться (ключом) указанных заголовков и параметров строки запроса.</span><span class="sxs-lookup"><span data-stu-id="10fe1-132">This response will be cached, keyed by the specified headers and query string parameters.</span></span> <span data-ttu-id="10fe1-133">Для последующих вызовов операции с совпадающими параметрами будет возвращаться кэшированный ответ до тех пор, пока не истечет срок действия кэша.</span><span class="sxs-lookup"><span data-stu-id="10fe1-133">Subsequent calls to the operation, with matching parameters, will have the cached response returned, until the cache duration interval has expired.</span></span>

## <span data-ttu-id="10fe1-134"><a name="caching-policies"> </a>Анализ политик кэширования</span><span class="sxs-lookup"><span data-stu-id="10fe1-134"><a name="caching-policies"> </a>Review the caching policies</span></span>
<span data-ttu-id="10fe1-135">На этом шаге необходимо проверить параметры кэширования для операции **GET Resource (cached)** образца Echo API.</span><span class="sxs-lookup"><span data-stu-id="10fe1-135">In this step, you review the caching settings for the **GET Resource (cached)** operation of the sample Echo API.</span></span>

<span data-ttu-id="10fe1-136">После настройки параметров кэширования на вкладке **Кэширование** для операции добавляются политики кэширования.</span><span class="sxs-lookup"><span data-stu-id="10fe1-136">When caching settings are configured for an operation on the **Caching** tab, caching policies are added for the operation.</span></span> <span data-ttu-id="10fe1-137">Эти политики можно просматривать и изменять в редакторе политик.</span><span class="sxs-lookup"><span data-stu-id="10fe1-137">These policies can be viewed and edited in the policy editor.</span></span>

<span data-ttu-id="10fe1-138">Щелкните **Политики** в меню **Управление API** слева и выберите **Echo API / GET Resource (cached)** из раскрывающегося списка **Операция**.</span><span class="sxs-lookup"><span data-stu-id="10fe1-138">Click **Policies** from the **API Management** menu on the left, and then select **Echo API / GET Resource (cached)** from the **Operation** drop-down list.</span></span>

![Операция с диапазоном политик][api-management-operation-dropdown]

<span data-ttu-id="10fe1-140">При этом в редакторе политик отображаются политики для данной операции.</span><span class="sxs-lookup"><span data-stu-id="10fe1-140">This displays the policies for this operation in the policy editor.</span></span>

![Редактор политик API Management][api-management-policy-editor]

<span data-ttu-id="10fe1-142">Определение политики для этой операции содержит политики, определяющие конфигурацию кэширования, которые были проанализированы с помощью вкладки **Кэширование** на предыдущем этапе.</span><span class="sxs-lookup"><span data-stu-id="10fe1-142">The policy definition for this operation includes the policies that define the caching configuration that were reviewed using the **Caching** tab in the previous step.</span></span>

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
> <span data-ttu-id="10fe1-143">Изменения, внесенные в политики кэширования в редакторе политик, будут отражаться на вкладке **Кэширование** операции (и наоборот).</span><span class="sxs-lookup"><span data-stu-id="10fe1-143">Changes made to the caching policies in the policy editor will be reflected on the **Caching** tab of an operation, and vice-versa.</span></span>
> 
> 

## <span data-ttu-id="10fe1-144"><a name="test-operation"> </a>Вызов операции и проверка кэширования</span><span class="sxs-lookup"><span data-stu-id="10fe1-144"><a name="test-operation"> </a>Call an operation and test the caching</span></span>
<span data-ttu-id="10fe1-145">Чтобы увидеть процесс кэширования в действии, можно вызвать операцию из портала разработчика.</span><span class="sxs-lookup"><span data-stu-id="10fe1-145">To see the caching in action, we can call the operation from the developer portal.</span></span> <span data-ttu-id="10fe1-146">В правом верхнем меню выберите пункт **Developer portal** (Портал разработчика).</span><span class="sxs-lookup"><span data-stu-id="10fe1-146">Click **Developer portal** in the top right menu.</span></span>

![Портал разработчика][api-management-developer-portal-menu]

<span data-ttu-id="10fe1-148">Щелкните **API** в меню вверху и выберите **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="10fe1-148">Click **APIs** in the top menu, and then select **Echo API**.</span></span>

![Echo API][api-management-apis-echo-api]

> <span data-ttu-id="10fe1-150">Если есть только один настроенный или видимый API для данной учетной записи, тогда щелчок по API сразу приведет к операциям для этого API.</span><span class="sxs-lookup"><span data-stu-id="10fe1-150">If you have only one API configured or visible to your account, then clicking APIs takes you directly to the operations for that API.</span></span>
> 
> 

<span data-ttu-id="10fe1-151">Выберите операцию **GET Resource (cached)** и щелкните **Открыть консоль**.</span><span class="sxs-lookup"><span data-stu-id="10fe1-151">Select the **GET Resource (cached)** operation, and then click **Open Console**.</span></span>

![Открытие консоли][api-management-open-console]

<span data-ttu-id="10fe1-153">Консоль позволяет вызывать операции прямо на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="10fe1-153">The console allows you to invoke operations directly from the developer portal.</span></span>

![Консоль][api-management-console]

<span data-ttu-id="10fe1-155">Сохраните значения по умолчанию для **param1** и **param2**.</span><span class="sxs-lookup"><span data-stu-id="10fe1-155">Keep the default values for **param1** and **param2**.</span></span>

<span data-ttu-id="10fe1-156">Выберите в раскрывающемся списке **subscription-key** требуемый ключ.</span><span class="sxs-lookup"><span data-stu-id="10fe1-156">Select the desired key from the **subscription-key** drop-down list.</span></span> <span data-ttu-id="10fe1-157">Если ваша учетная запись содержит только одну подписку, он уже будет выбран.</span><span class="sxs-lookup"><span data-stu-id="10fe1-157">If your account has only one subscription, it will already be selected.</span></span>

<span data-ttu-id="10fe1-158">Введите **sampleheader:value1** в текстовом поле **Заголовки запроса**.</span><span class="sxs-lookup"><span data-stu-id="10fe1-158">Enter **sampleheader:value1** in the **Request headers** text box.</span></span>

<span data-ttu-id="10fe1-159">Щелкните **HTTP Get** и запишите значение заголовков ответа.</span><span class="sxs-lookup"><span data-stu-id="10fe1-159">Click **HTTP Get** and make a note of the response headers.</span></span>

<span data-ttu-id="10fe1-160">Введите в текстовое поле **Заголовки запроса** значение **sampleheader:value2** и нажмите **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="10fe1-160">Enter **sampleheader:value2** in the **Request headers** text box, and then click **HTTP Get**.</span></span>

<span data-ttu-id="10fe1-161">Следует отметить, что значение **sampleheader** по-прежнему совпадает со значение **value1** в ответе.</span><span class="sxs-lookup"><span data-stu-id="10fe1-161">Note that the value of **sampleheader** is still **value1** in the response.</span></span> <span data-ttu-id="10fe1-162">Попробуйте ввести другие значения и убедитесь, что возвращается кэшированный ответ из первого вызова.</span><span class="sxs-lookup"><span data-stu-id="10fe1-162">Try some different values and note that the cached response from the first call is returned.</span></span>

<span data-ttu-id="10fe1-163">Введите в поле **param2** значение **25** и нажмите **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="10fe1-163">Enter **25** into the **param2** field, and then click **HTTP Get**.</span></span>

<span data-ttu-id="10fe1-164">Следует отметить, что значением **sampleheader** в ответе теперь является **value2**.</span><span class="sxs-lookup"><span data-stu-id="10fe1-164">Note that the value of **sampleheader** in the response is now **value2**.</span></span> <span data-ttu-id="10fe1-165">Так как результаты операции определяются строкой запроса, то предыдущий кэшированный ответ не возвращается.</span><span class="sxs-lookup"><span data-stu-id="10fe1-165">Because the operation results are keyed by query string, the previous cached response was not returned.</span></span>

## <span data-ttu-id="10fe1-166"><a name="next-steps"> </a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="10fe1-166"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="10fe1-167">Дополнительные сведения о политиках кэширования см. в разделе [Политики кэширования][Caching policies] [справочника по политикам управления API][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="10fe1-167">For more information about caching policies, see [Caching policies][Caching policies] in the [API Management policy reference][API Management policy reference].</span></span>
* <span data-ttu-id="10fe1-168">Сведения о кэшировании элементов по ключу с помощью выражений политики см. в статье [Пользовательское кэширование в службе управления API Azure](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="10fe1-168">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>

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


[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review the caching policies]: #caching-policies
[Call an operation and test the caching]: #test-operation
[Next steps]: #next-steps
