---
title: "Как добавлять операции в API в управлении API Azure | Документация Майкрософт"
description: "Добавление операций в API в службе управления API Azure"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 1158a023-1913-4e9c-93de-9164b672f9b3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 105fc51c2d1152a40a5757985da47330e0b7b8cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-operations-to-an-api-in-azure-api-management"></a><span data-ttu-id="1a5f1-103">Добавление операций в API в Azure API Management</span><span class="sxs-lookup"><span data-stu-id="1a5f1-103">How to add operations to an API in Azure API Management</span></span>
<span data-ttu-id="1a5f1-104">Прежде чем API может быть использован в API Management, должны быть добавлены операции.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-104">Before an API in API Management can be used, operations must be added.</span></span> <span data-ttu-id="1a5f1-105">Это руководство описывает добавление и настройку операций различного типа в интерфейсе API в API Management.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-105">This guide shows how to add and configure different types of operations to an API in API Management.</span></span>

## <span data-ttu-id="1a5f1-106"><a name="add-operation"> </a>Добавление операции</span><span class="sxs-lookup"><span data-stu-id="1a5f1-106"><a name="add-operation"> </a>Add an operation</span></span>
<span data-ttu-id="1a5f1-107">Операции добавляются и настраиваются для API на портале издателя.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-107">Operations are added and configured to an API in the publisher portal.</span></span> <span data-ttu-id="1a5f1-108">Чтобы перейти на портал издателя, на портале Azure щелкните **Publisher portal** (Портал издателя) для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-108">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Портал издателя][api-management-management-console]

> <span data-ttu-id="1a5f1-110">Если экземпляр службы управления API еще не создан, см. раздел [Создание экземпляра управления API][Create an API Management service instance] в руководстве [Начало работы со службой управления Azure API][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="1a5f1-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="1a5f1-111">Выберите требуемый API на портале издателя, а затем перейдите на вкладку **Операции** .</span><span class="sxs-lookup"><span data-stu-id="1a5f1-111">Select the desired API in the publisher portal and then select the **Operations** tab.</span></span> 

![Операции][api-management-operations]

<span data-ttu-id="1a5f1-113">Щелкните **Добавить операцию** , чтобы добавить новую операцию.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-113">Click **Add Operation** to add a new operation.</span></span> <span data-ttu-id="1a5f1-114">Появится окно **Новая операция**, вкладка **Сигнатура** будет выбрана по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-114">The **New operation** will be displayed and the **Signature** tab will be selected by default.</span></span>

![Добавить операцию][api-management-add-operation]

<span data-ttu-id="1a5f1-116">Выберите **команду HTTP** в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-116">Specify the **HTTP verb** by choosing from the drop-down list.</span></span>

![Метод HTTP][api-management-http-method]

<a name="url-template"></a>

<span data-ttu-id="1a5f1-118">Определите шаблон URL-адреса путем ввода фрагмента URL-адреса, который содержит один или несколько сегментов пути URL, а также несколько параметров строки запроса (либо вообще без параметров).</span><span class="sxs-lookup"><span data-stu-id="1a5f1-118">Define the URL template by typing in a URL fragment consisting of one or more URL path segments and zero or more query string parameters.</span></span> <span data-ttu-id="1a5f1-119">Шаблон URL-адреса, добавляемый к основному URL-адресу API, идентифицирует одиночную HTTP-операцию.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-119">The URL template, appended to the base URL of the API, identifies a single HTTP operation.</span></span> <span data-ttu-id="1a5f1-120">Он может содержать один или несколько частей переменной с именем, которые идентифицируются изогнутыми фигурными скобками.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-120">It may contain one or more named variable parts that are identified by curly braces.</span></span> <span data-ttu-id="1a5f1-121">Эти части переменной называются параметрами шаблона и представляют собой динамически назначаемые значения, извлекаемые из URL-адреса запроса, когда запрос обрабатывается платформой API Management.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-121">These variable parts are called template parameters and are dynamically assigned values extracted from the request's URL when the request is being processed by the API Management platform.</span></span>

> <span data-ttu-id="1a5f1-122">Шаблон URL-адреса может включать шаблоны с подстановочными знаками.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-122">The URL template can include wildcard patterns.</span></span> <span data-ttu-id="1a5f1-123">Например, если указать `/*`, то все запросы этого метода HTTP будут перенаправляться на внутреннюю службу.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-123">For example, specifying `/*` will forward all requests for that HTTP method to the back end service.</span></span>

![Шаблон URL-адреса][api-management-url-template]

<a name="rewrite-url-template"></a>

<span data-ttu-id="1a5f1-125">При необходимости укажите **Шаблон URL-адреса перезаписи**.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-125">If desired, specify the **Rewrite URL template**.</span></span> <span data-ttu-id="1a5f1-126">Это позволяет использовать стандартный шаблон URL-адреса для обработки входящих запросов на интерфейсной части при вызове серверной части с помощью преобразованного URL-адреса в соответствии с шаблоном перезаписи.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-126">This allows you to use the standard URL template for processing incoming requests on the front-end, while calling the back-end via a converted URL according to the rewrite template.</span></span> <span data-ttu-id="1a5f1-127">В шаблоне перезаписи должны использоваться параметры шаблона из шаблона URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-127">Template parameters from the URL template should be used in the rewrite template.</span></span> <span data-ttu-id="1a5f1-128">В следующем пример показано, как тип контента, закодированный как сегмент пути в веб-службе из предыдущего примера, может быть введен в качестве параметра запроса в API, опубликованном на платформе API Management с помощью шаблонов URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-128">The following example shows how content type encoded as path segment in the web service from the previous example can be provided as a query parameter in the API published via the API Management platform using the URL templates.</span></span>

![Перезапись шаблона URL-адреса][api-management-url-template-rewrite]

<span data-ttu-id="1a5f1-130">Вызывающие объекты операции будут использовать формат `/customers?customerid=ALFKI`, который будет сопоставляться с форматом `/Customers('ALFKI')` при вызове серверной службы.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-130">Callers to the operation will use the format `/customers?customerid=ALFKI` and this will be mapped to `/Customers('ALFKI')` when the back-end service is invoked.</span></span>

<span data-ttu-id="1a5f1-131">Текстовые поля **Отображаемое имя** и **Описание** содержат описание операции и используются для предоставления документации разработчикам, которые используют этот API на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-131">**Display** name and **Description** provide a description of the operation and are used to provide documentation to the developers using this API in the developer portal.</span></span>

![Описание][api-management-description]

<span data-ttu-id="1a5f1-133">Описание операции может быть введено в виде обычного текста или в формате HTML в текстовом поле **Описание** .</span><span class="sxs-lookup"><span data-stu-id="1a5f1-133">The operation description can be specified as plain text or HTML in the **Description** text box.</span></span>

## <span data-ttu-id="1a5f1-134"><a name="operation-caching"> </a>Кэширование операций</span><span class="sxs-lookup"><span data-stu-id="1a5f1-134"><a name="operation-caching"> </a>Operation caching</span></span>
<span data-ttu-id="1a5f1-135">Кэширование ответов уменьшает задержку для потребителей API, снижает потребляемую пропускную способность и сокращает нагрузку на веб-службу HTTP, которая реализует интерфейс API.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-135">Response caching reduces latency perceived by the API consumers, lowers bandwidth consumption and decreases the load on the HTTP web service implementing the API.</span></span> 

<span data-ttu-id="1a5f1-136">Для легкого и быстрого включения кэширования для операции перейдите на вкладку **Кэширование** и установите флажок **Включить**.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-136">To easily and quickly enable caching for the operation, select the **Caching** tab and check the **Enable** checkbox.</span></span>

![Caching][api-management-caching-tab]

<span data-ttu-id="1a5f1-138">**Длительность** указывает период времени, в течение которого ответ операции остается в кэше.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-138">**Duration** specifies the time period during which the operation response remains in the cache.</span></span> <span data-ttu-id="1a5f1-139">Значение по умолчанию составляет 3600 секунд или 1 час.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-139">The default value is 3600 seconds or 1 hour.</span></span>

<span data-ttu-id="1a5f1-140">Ключи кэша используются, чтобы отличать ответы друг от друга таким образом, чтобы ответ, соответствующий каждому отличному ключу кэша, получал свое собственное отдельное кэшированное значение.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-140">Cache keys are used to differentiate between responses so that the response corresponding to each different cache key will get its own separate cached value.</span></span> <span data-ttu-id="1a5f1-141">Или же можно ввести специальные параметры строки запроса и/или HTTP-заголовки, которые должны будут использоваться при вычислении значений ключей кэша, соответственно в текстовые поля **В зависимости от параметров строки запроса** и **Vary by headers** (В зависимости от заголовков).</span><span class="sxs-lookup"><span data-stu-id="1a5f1-141">Optionally, enter specific query string parameters and/or HTTP headers to be used in computing cache key values in the **Vary by query string parameters** and **Vary by headers** text boxes respectively.</span></span> <span data-ttu-id="1a5f1-142">Если они не заданы, при создании ключей кэша используются полный URL-адрес запроса и следующие значения HTTP-заголовка: **Accept** и **Accept-Charset**.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-142">When none are specified, full request URL and the following HTTP header values are used in cache key generation: **Accept** and **Accept-Charset**.</span></span>

> <span data-ttu-id="1a5f1-143">Дополнительные сведения о кэшировании и политиках кэширования см. в статье [Добавление кэширования для повышения производительности в службе управления API Azure][How to cache operation results in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="1a5f1-143">For more information on caching and caching policies, see [How to cache operation results in Azure API Management][How to cache operation results in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="1a5f1-144"><a name="request-parameters"> </a>Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="1a5f1-144"><a name="request-parameters"> </a>Request parameters</span></span>
<span data-ttu-id="1a5f1-145">Параметрами операции можно управлять на вкладке «Параметры».</span><span class="sxs-lookup"><span data-stu-id="1a5f1-145">Operation parameters are managed on the Parameters tab.</span></span> <span data-ttu-id="1a5f1-146">Параметры, заданные в поле **Шаблон URL-адреса** на вкладке **Сигнатура**, добавляются автоматически и могут быть изменены только путем редактирования шаблона URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-146">Parameters specified in the **URL Template** on the **Signature** tab are added automatically and can be changed only by editing the URL template.</span></span> <span data-ttu-id="1a5f1-147">Дополнительные параметры можно вводить вручную.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-147">Additional parameters can be entered manually.</span></span>

<span data-ttu-id="1a5f1-148">Для добавления нового параметра запроса щелкните **Добавить параметр запроса** и введите следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-148">To add a new query parameter, click **Add Query Parameter** and enter the following information:</span></span>

* <span data-ttu-id="1a5f1-149">**Имя** - имя параметра.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-149">**Name** - parameter name.</span></span>
* <span data-ttu-id="1a5f1-150">**Описание** - краткое описание параметра (необязательно).</span><span class="sxs-lookup"><span data-stu-id="1a5f1-150">**Description** - a brief description of the parameter (optional).</span></span>
* <span data-ttu-id="1a5f1-151">**Тип** - тип параметра, выбранный в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-151">**Type** - parameter type, selected in the drop down.</span></span>
* <span data-ttu-id="1a5f1-152">**Значения** - значения, которые могут быть назначены этому параметру.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-152">**Values** - values that can be assigned to this parameter.</span></span> <span data-ttu-id="1a5f1-153">Одно из значений может быть отмечено как значение по умолчанию (необязательно).</span><span class="sxs-lookup"><span data-stu-id="1a5f1-153">One of the values can be marked as default (optional).</span></span>
* <span data-ttu-id="1a5f1-154">**Обязательный** - установите флажок, если этот параметр должен быть обязательным.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-154">**Required** - make the parameter mandatory by checking the checkbox.</span></span> 

![Параметры запроса][api-management-request-parameters]

## <span data-ttu-id="1a5f1-156"><a name="request-body"> </a>Текст запроса</span><span class="sxs-lookup"><span data-stu-id="1a5f1-156"><a name="request-body"> </a>Request body</span></span>
<span data-ttu-id="1a5f1-157">Если операция допускает (например, PUT, POST) и требует наличия тела, то можно ввести пример такого тела во всех поддерживаемых форматах представления (например, json, XML).</span><span class="sxs-lookup"><span data-stu-id="1a5f1-157">If the operation allows (e.g. PUT, POST) and requires a body you may provide an example of it in all of the supported representation formats (e.g. json, XML).</span></span> 

> <span data-ttu-id="1a5f1-158">Тело запроса используется только в документационных целях и не проверяется.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-158">The request body is used for documentation purposes only and is not validated.</span></span>
> 
> 

<span data-ttu-id="1a5f1-159">Для ввода тела запроса перейдите на вкладку **Тело** .</span><span class="sxs-lookup"><span data-stu-id="1a5f1-159">To enter a request body, switch to the **Body** tab.</span></span>

<span data-ttu-id="1a5f1-160">Щелкните **Добавить представление**, начните вводить требуемое название типа контента (например, приложение/json), выберите его в раскрывающемся списке и вставьте требуемый пример тела запроса в выбранном формате в текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-160">Click **Add Representation**, start typing desired content type name (e.g. application/json), select it in the drop-down, and paste the desired request body example in the selected format into the text box.</span></span> 

![Текст запроса][api-management-request-body]

<span data-ttu-id="1a5f1-162">В дополнение к представлениям необязательное текстовое описание также можно ввести в текстовом поле **Описание** .</span><span class="sxs-lookup"><span data-stu-id="1a5f1-162">In additional to representations, you can also specify an optional text description in the **Description** text box.</span></span>

## <span data-ttu-id="1a5f1-163"><a name="responses"> </a>Ответы</span><span class="sxs-lookup"><span data-stu-id="1a5f1-163"><a name="responses"> </a>Responses</span></span>
<span data-ttu-id="1a5f1-164">Рекомендуется создавать примеры ответов для всех кодов состояния, которые может выдать операция.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-164">It is a good practice to provide examples of responses for all status codes that the operation may produce.</span></span> <span data-ttu-id="1a5f1-165">Каждый код состояния может содержать более одного примера содержимого ответа, по одному для каждого поддерживаемого типа содержимого.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-165">Each status code may have more than one response body example, one for each of the supported content types.</span></span> 

<span data-ttu-id="1a5f1-166">Для добавления ответа щелкните **Добавить** и начните вводить требуемый код состояния.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-166">To add a response, click **Add** and start typing the desired status code.</span></span> <span data-ttu-id="1a5f1-167">В этом примере код состояния — **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-167">In this example the status code is **200 OK**.</span></span> <span data-ttu-id="1a5f1-168">Как только код появится в раскрывающемся списке, выберите его. Будет создан код ответа, который будет добавлен в вашу операцию.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-168">Once the code is displayed in the drop-down, select it, and the response code is created and added to your operation.</span></span>

![Код ответа][api-management-response-code]

<span data-ttu-id="1a5f1-170">Щелкните **Добавить представление**, начните вводить требуемое название типа контента (например, приложение/json), а затем выберите его в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-170">Click **Add Representation**, start typing the desired content type name (e.g. application/json) and then select it in the drop down.</span></span>

![Тип контента тела][api-management-response-body-content-type]

<span data-ttu-id="1a5f1-172">Вставьте пример тела ответа в выбранном формате в текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-172">Paste the response body example in the selected format into the text box.</span></span> 

![Тело ответа][api-management-response-body]

<span data-ttu-id="1a5f1-174">При необходимости добавьте необязательное описание в текстовое поле **Описание** .</span><span class="sxs-lookup"><span data-stu-id="1a5f1-174">If desired, add an optional description into the **Description** text box.</span></span>

<span data-ttu-id="1a5f1-175">После настройки операции щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-175">Once the operation is configured, click **Save**.</span></span>

## <span data-ttu-id="1a5f1-176"><a name="next-steps"> </a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1a5f1-176"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="1a5f1-177">Как только операции будут добавлены в API, следующим шагом будет сопоставление интерфейса API с продуктом и его публикация, чтобы разработчики могли вызывать его операции.</span><span class="sxs-lookup"><span data-stu-id="1a5f1-177">Once the operations are added to an API, the next step is to associate the API with a product and publish it so that developers can call its operations.</span></span>

* <span data-ttu-id="1a5f1-178">[Как создать и опубликовать продукт][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="1a5f1-178">[How to create and publish a product][How to create and publish a product]</span></span>

[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to cache operation results in Azure API Management]: api-management-howto-cache.md
