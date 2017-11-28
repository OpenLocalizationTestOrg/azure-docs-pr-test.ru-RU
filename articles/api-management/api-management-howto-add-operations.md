---
title: "tooan операции aaaHow tooadd API в службе управления API Azure | Документы Microsoft"
description: "Узнайте, как tooan tooadd операций API в Azure API Management."
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
ms.openlocfilehash: d57fa59a2b0ceb392cde23150a0cbb326e52d27d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-operations-tooan-api-in-azure-api-management"></a><span data-ttu-id="10d47-103">Как tooan tooadd операций API в Azure API Management</span><span class="sxs-lookup"><span data-stu-id="10d47-103">How tooadd operations tooan API in Azure API Management</span></span>
<span data-ttu-id="10d47-104">Прежде чем API может быть использован в API Management, должны быть добавлены операции.</span><span class="sxs-lookup"><span data-stu-id="10d47-104">Before an API in API Management can be used, operations must be added.</span></span> <span data-ttu-id="10d47-105">Это руководство показывает, как tooadd и настройки различных типов tooan операций API в службе управления API.</span><span class="sxs-lookup"><span data-stu-id="10d47-105">This guide shows how tooadd and configure different types of operations tooan API in API Management.</span></span>

## <span data-ttu-id="10d47-106"><a name="add-operation"> </a>Добавление операции</span><span class="sxs-lookup"><span data-stu-id="10d47-106"><a name="add-operation"> </a>Add an operation</span></span>
<span data-ttu-id="10d47-107">Операции являются добавляется и настраивается tooan API hello портала издателя.</span><span class="sxs-lookup"><span data-stu-id="10d47-107">Operations are added and configured tooan API in hello publisher portal.</span></span> <span data-ttu-id="10d47-108">tooaccess hello издателя, щелкните **портал издателя** в hello портала Azure для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="10d47-108">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Портал издателя][api-management-management-console]

> <span data-ttu-id="10d47-110">Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.</span><span class="sxs-lookup"><span data-stu-id="10d47-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="10d47-111">Выберите hello необходимое API в портал издателя hello и выберите hello **операции** вкладки.</span><span class="sxs-lookup"><span data-stu-id="10d47-111">Select hello desired API in hello publisher portal and then select hello **Operations** tab.</span></span> 

![Операции][api-management-operations]

<span data-ttu-id="10d47-113">Нажмите кнопку **добавить операцию** tooadd новую операцию.</span><span class="sxs-lookup"><span data-stu-id="10d47-113">Click **Add Operation** tooadd a new operation.</span></span> <span data-ttu-id="10d47-114">Hello **новую операцию** будут отображены и hello **подписи** вкладка будет выбран по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="10d47-114">hello **New operation** will be displayed and hello **Signature** tab will be selected by default.</span></span>

![Добавить операцию][api-management-add-operation]

<span data-ttu-id="10d47-116">Укажите hello **HTTP-команду** , выбрав из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="10d47-116">Specify hello **HTTP verb** by choosing from hello drop-down list.</span></span>

![Метод HTTP][api-management-http-method]

<a name="url-template"></a>

<span data-ttu-id="10d47-118">Определение шаблона hello URL-адрес, введя в фрагмент URL-адреса, состоящий из одного или нескольких сегментов пути URL-адреса и ноль или более параметров строки запроса.</span><span class="sxs-lookup"><span data-stu-id="10d47-118">Define hello URL template by typing in a URL fragment consisting of one or more URL path segments and zero or more query string parameters.</span></span> <span data-ttu-id="10d47-119">шаблон URL-адреса Hello, добавленных toohello базовый URL-адрес hello API, определяет одну операцию HTTP.</span><span class="sxs-lookup"><span data-stu-id="10d47-119">hello URL template, appended toohello base URL of hello API, identifies a single HTTP operation.</span></span> <span data-ttu-id="10d47-120">Он может содержать один или несколько частей переменной с именем, которые идентифицируются изогнутыми фигурными скобками.</span><span class="sxs-lookup"><span data-stu-id="10d47-120">It may contain one or more named variable parts that are identified by curly braces.</span></span> <span data-ttu-id="10d47-121">Эти переменные части называются параметрами шаблона и динамически присваиваются значения, извлеченные из URL-адрес запроса hello при обработке запроса hello платформой управления API hello.</span><span class="sxs-lookup"><span data-stu-id="10d47-121">These variable parts are called template parameters and are dynamically assigned values extracted from hello request's URL when hello request is being processed by hello API Management platform.</span></span>

> <span data-ttu-id="10d47-122">шаблон URL-адреса Hello могут включать шаблоны из подстановочных знаков.</span><span class="sxs-lookup"><span data-stu-id="10d47-122">hello URL template can include wildcard patterns.</span></span> <span data-ttu-id="10d47-123">Например, при указании `/*` будет пересылать все запросы для этого HTTP метод toohello обратно остановить службы.</span><span class="sxs-lookup"><span data-stu-id="10d47-123">For example, specifying `/*` will forward all requests for that HTTP method toohello back end service.</span></span>

![Шаблон URL-адреса][api-management-url-template]

<a name="rewrite-url-template"></a>

<span data-ttu-id="10d47-125">При необходимости укажите hello **перепишите URL-адрес шаблона**.</span><span class="sxs-lookup"><span data-stu-id="10d47-125">If desired, specify hello **Rewrite URL template**.</span></span> <span data-ttu-id="10d47-126">Это позволяет вам toouse hello стандартный шаблон URL-адреса для обработки входящих запросов на hello переднего плана, в ходе вызова hello внутренней через преобразованный URL-адрес в соответствии с toohello перепишите шаблона.</span><span class="sxs-lookup"><span data-stu-id="10d47-126">This allows you toouse hello standard URL template for processing incoming requests on hello front-end, while calling hello back-end via a converted URL according toohello rewrite template.</span></span> <span data-ttu-id="10d47-127">В шаблоне перезаписи hello следует использовать параметры шаблона на основе шаблона hello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="10d47-127">Template parameters from hello URL template should be used in hello rewrite template.</span></span> <span data-ttu-id="10d47-128">Hello пример типа как содержимого, закодированные как сегмент пути в веб-службу hello из предыдущего примера hello могут быть предоставлены как параметр запроса в hello API опубликованные через hello платформы управления API, с помощью шаблонов hello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="10d47-128">hello following example shows how content type encoded as path segment in hello web service from hello previous example can be provided as a query parameter in hello API published via hello API Management platform using hello URL templates.</span></span>

![Перезапись шаблона URL-адреса][api-management-url-template-rewrite]

<span data-ttu-id="10d47-130">Операция toohello вызывающим объектам будет использовать формат hello `/customers?customerid=ALFKI` , и это будет сопоставляться слишком`/Customers('ALFKI')` при вызове hello внутренней службы.</span><span class="sxs-lookup"><span data-stu-id="10d47-130">Callers toohello operation will use hello format `/customers?customerid=ALFKI` and this will be mapped too`/Customers('ALFKI')` when hello back-end service is invoked.</span></span>

<span data-ttu-id="10d47-131">**Отображение** имя и **описание** обеспечивает описание операции hello и документации используется tooprovide toohello разработчики, использующие этот API на портале разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="10d47-131">**Display** name and **Description** provide a description of hello operation and are used tooprovide documentation toohello developers using this API in hello developer portal.</span></span>

![Описание][api-management-description]

<span data-ttu-id="10d47-133">Описание операции Hello в можно указать как обычный текст или HTML hello **описание** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="10d47-133">hello operation description can be specified as plain text or HTML in hello **Description** text box.</span></span>

## <span data-ttu-id="10d47-134"><a name="operation-caching"> </a>Кэширование операций</span><span class="sxs-lookup"><span data-stu-id="10d47-134"><a name="operation-caching"> </a>Operation caching</span></span>
<span data-ttu-id="10d47-135">Кэширование ответов снижает задержку для потребителей hello API, снижает потребление пропускной способности и уменьшается hello нагрузку на реализации службы web hello HTTP hello API.</span><span class="sxs-lookup"><span data-stu-id="10d47-135">Response caching reduces latency perceived by hello API consumers, lowers bandwidth consumption and decreases hello load on hello HTTP web service implementing hello API.</span></span> 

<span data-ttu-id="10d47-136">tooeasily и быстро включить кэширование для hello операции select hello **кэширование** вкладку и проверьте hello **включить** флажок.</span><span class="sxs-lookup"><span data-stu-id="10d47-136">tooeasily and quickly enable caching for hello operation, select hello **Caching** tab and check hello **Enable** checkbox.</span></span>

![Caching][api-management-caching-tab]

<span data-ttu-id="10d47-138">**Длительность** определяет период времени, во время которого hello ответ операции остается в кэше hello hello.</span><span class="sxs-lookup"><span data-stu-id="10d47-138">**Duration** specifies hello time period during which hello operation response remains in hello cache.</span></span> <span data-ttu-id="10d47-139">значение по умолчанию Hello — 3600 секунд или 1 час.</span><span class="sxs-lookup"><span data-stu-id="10d47-139">hello default value is 3600 seconds or 1 hour.</span></span>

<span data-ttu-id="10d47-140">Кэширование ключей, используемых toodifferentiate между ответами, чтобы ответ hello соответствующий ключ другой кэша tooeach получите свой собственный отдельный кэшированное значение.</span><span class="sxs-lookup"><span data-stu-id="10d47-140">Cache keys are used toodifferentiate between responses so that hello response corresponding tooeach different cache key will get its own separate cached value.</span></span> <span data-ttu-id="10d47-141">При необходимости введите параметры строки запроса и/или toobe заголовки HTTP, используемый при вычислении значения ключа кэша в hello **происходит изменение параметров строки запроса** и **Vary заголовками** текстовые поля, соответственно.</span><span class="sxs-lookup"><span data-stu-id="10d47-141">Optionally, enter specific query string parameters and/or HTTP headers toobe used in computing cache key values in hello **Vary by query string parameters** and **Vary by headers** text boxes respectively.</span></span> <span data-ttu-id="10d47-142">Когда ни одна не запроса задан, то полный URL-адрес и hello следующие значения заголовка HTTP используются при создании ключа кэша: **Accept** и **Accept-Charset**.</span><span class="sxs-lookup"><span data-stu-id="10d47-142">When none are specified, full request URL and hello following HTTP header values are used in cache key generation: **Accept** and **Accept-Charset**.</span></span>

> <span data-ttu-id="10d47-143">Дополнительные сведения о кэшировании и политики кэширования см. в разделе [отображением результатов операции toocache в Azure API Management][How toocache operation results in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="10d47-143">For more information on caching and caching policies, see [How toocache operation results in Azure API Management][How toocache operation results in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="10d47-144"><a name="request-parameters"> </a>Параметры запроса</span><span class="sxs-lookup"><span data-stu-id="10d47-144"><a name="request-parameters"> </a>Request parameters</span></span>
<span data-ttu-id="10d47-145">Параметры операции осуществляется на вкладке Параметры hello. Параметры, заданные в hello **URL-адрес шаблона** на hello **подписи** вкладка добавляются автоматически и можно изменить только путем изменения шаблона hello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="10d47-145">Operation parameters are managed on hello Parameters tab. Parameters specified in hello **URL Template** on hello **Signature** tab are added automatically and can be changed only by editing hello URL template.</span></span> <span data-ttu-id="10d47-146">Дополнительные параметры можно вводить вручную.</span><span class="sxs-lookup"><span data-stu-id="10d47-146">Additional parameters can be entered manually.</span></span>

<span data-ttu-id="10d47-147">tooadd новый параметр запроса, нажмите кнопку **добавить параметр запроса** и введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="10d47-147">tooadd a new query parameter, click **Add Query Parameter** and enter hello following information:</span></span>

* <span data-ttu-id="10d47-148">**Имя** - имя параметра.</span><span class="sxs-lookup"><span data-stu-id="10d47-148">**Name** - parameter name.</span></span>
* <span data-ttu-id="10d47-149">**Описание** -краткое описание параметра hello (необязательно).</span><span class="sxs-lookup"><span data-stu-id="10d47-149">**Description** - a brief description of hello parameter (optional).</span></span>
* <span data-ttu-id="10d47-150">**Тип** -типа параметра, выбранного в раскрывающемся hello.</span><span class="sxs-lookup"><span data-stu-id="10d47-150">**Type** - parameter type, selected in hello drop down.</span></span>
* <span data-ttu-id="10d47-151">**Значения** -значения, которые могут быть назначены toothis параметра.</span><span class="sxs-lookup"><span data-stu-id="10d47-151">**Values** - values that can be assigned toothis parameter.</span></span> <span data-ttu-id="10d47-152">Одно из значений hello может быть помечен как по умолчанию (необязательно).</span><span class="sxs-lookup"><span data-stu-id="10d47-152">One of hello values can be marked as default (optional).</span></span>
* <span data-ttu-id="10d47-153">**Требуется** -сделать обязательным параметром hello, установив флажок hello.</span><span class="sxs-lookup"><span data-stu-id="10d47-153">**Required** - make hello parameter mandatory by checking hello checkbox.</span></span> 

![Параметры запроса][api-management-request-parameters]

## <span data-ttu-id="10d47-155"><a name="request-body"> </a>Текст запроса</span><span class="sxs-lookup"><span data-stu-id="10d47-155"><a name="request-body"> </a>Request body</span></span>
<span data-ttu-id="10d47-156">Если операция hello позволяет (например, PUT, POST) и требует тело может предоставлять его во всех hello примером поддерживаемые форматы представления (например json, XML).</span><span class="sxs-lookup"><span data-stu-id="10d47-156">If hello operation allows (e.g. PUT, POST) and requires a body you may provide an example of it in all of hello supported representation formats (e.g. json, XML).</span></span> 

> <span data-ttu-id="10d47-157">текст запроса Hello используется только для документирования и не проверяется.</span><span class="sxs-lookup"><span data-stu-id="10d47-157">hello request body is used for documentation purposes only and is not validated.</span></span>
> 
> 

<span data-ttu-id="10d47-158">текст запроса, tooenter переключения toohello **текст** вкладки.</span><span class="sxs-lookup"><span data-stu-id="10d47-158">tooenter a request body, switch toohello **Body** tab.</span></span>

<span data-ttu-id="10d47-159">Нажмите кнопку **добавить представление**начать ввод имени требуемого типа содержимого (например приложение/json), выберите его в раскрывающемся hello и вставить hello требуемого пример текста запроса в выбранном формате hello в текстовое поле hello.</span><span class="sxs-lookup"><span data-stu-id="10d47-159">Click **Add Representation**, start typing desired content type name (e.g. application/json), select it in hello drop-down, and paste hello desired request body example in hello selected format into hello text box.</span></span> 

![Тело запроса][api-management-request-body]

<span data-ttu-id="10d47-161">В дополнительных toorepresentations также можно указать необязательное текстовое описание в hello **описание** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="10d47-161">In additional toorepresentations, you can also specify an optional text description in hello **Description** text box.</span></span>

## <span data-ttu-id="10d47-162"><a name="responses"> </a>Ответы</span><span class="sxs-lookup"><span data-stu-id="10d47-162"><a name="responses"> </a>Responses</span></span>
<span data-ttu-id="10d47-163">Это примеры tooprovide хорошей практикой ответов для всех коды состояния, которые может привести к операции hello.</span><span class="sxs-lookup"><span data-stu-id="10d47-163">It is a good practice tooprovide examples of responses for all status codes that hello operation may produce.</span></span> <span data-ttu-id="10d47-164">Каждый код состояния может иметь более одного пример текста ответа, один для каждого из hello поддерживаемые типы содержимого.</span><span class="sxs-lookup"><span data-stu-id="10d47-164">Each status code may have more than one response body example, one for each of hello supported content types.</span></span> 

<span data-ttu-id="10d47-165">Щелкните tooadd ответ, **добавить** и начните вводить код hello требуемого состояния.</span><span class="sxs-lookup"><span data-stu-id="10d47-165">tooadd a response, click **Add** and start typing hello desired status code.</span></span> <span data-ttu-id="10d47-166">В этом пример hello состояние код- **200 ОК**.</span><span class="sxs-lookup"><span data-stu-id="10d47-166">In this example hello status code is **200 OK**.</span></span> <span data-ttu-id="10d47-167">Если hello код отображается в раскрывающемся списке hello, выберите его и hello код ответа — операция создана и добавлена tooyour.</span><span class="sxs-lookup"><span data-stu-id="10d47-167">Once hello code is displayed in hello drop-down, select it, and hello response code is created and added tooyour operation.</span></span>

![Код ответа][api-management-response-code]

<span data-ttu-id="10d47-169">Нажмите кнопку **добавить представление**, начните вводить имя требуемого типа содержимого hello (например приложение/json) и выберите его в hello раскрывающийся список.</span><span class="sxs-lookup"><span data-stu-id="10d47-169">Click **Add Representation**, start typing hello desired content type name (e.g. application/json) and then select it in hello drop down.</span></span>

![Тип контента тела][api-management-response-body-content-type]

<span data-ttu-id="10d47-171">Вставьте hello пример текста ответа в выбранном формате hello в текстовое поле hello.</span><span class="sxs-lookup"><span data-stu-id="10d47-171">Paste hello response body example in hello selected format into hello text box.</span></span> 

![Тело ответа][api-management-response-body]

<span data-ttu-id="10d47-173">При желании добавьте описание (необязательно) в hello **описание** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="10d47-173">If desired, add an optional description into hello **Description** text box.</span></span>

<span data-ttu-id="10d47-174">Настроив hello операцию, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="10d47-174">Once hello operation is configured, click **Save**.</span></span>

## <span data-ttu-id="10d47-175"><a name="next-steps"> </a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="10d47-175"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="10d47-176">После добавления hello операций tooan API hello следующий шаг hello tooassociate API с продуктом и опубликовать разработчики могут вызывать его операций.</span><span class="sxs-lookup"><span data-stu-id="10d47-176">Once hello operations are added tooan API, hello next step is tooassociate hello API with a product and publish it so that developers can call its operations.</span></span>

* <span data-ttu-id="10d47-177">[Как toocreate и публикация продукта][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="10d47-177">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
