---
title: "API сборщика данных HTTP в Log Analytics | Документация Майкрософт"
description: "API сборщика данных HTTP в Log Analytics можно использовать для добавления данных POST JSON в репозиторий Log Analytics из любого клиента, который может вызывать REST API. В этой статье описывается, как использовать API, и приводятся примеры публикации данных с использованием разных языков программирования."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: b0c45ff8c1d4c9d35fbb3c8839b38a20df277055
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="send-data-to-log-analytics-with-the-http-data-collector-api"></a><span data-ttu-id="1e261-104">Отправка данных Log Analytics с помощью API сборщика данных HTTP</span><span class="sxs-lookup"><span data-stu-id="1e261-104">Send data to Log Analytics with the HTTP Data Collector API</span></span>
<span data-ttu-id="1e261-105">В этой статье показано, как с помощью API сборщика данных HTTP отправить данные в Log Analytics из клиента REST API.</span><span class="sxs-lookup"><span data-stu-id="1e261-105">This article shows you how to use the HTTP Data Collector API to send data to Log Analytics from a REST API client.</span></span>  <span data-ttu-id="1e261-106">Здесь также описано, как отформатировать данные, собранные сценарием или приложением, добавить их в запрос и авторизовать этот запрос в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1e261-106">It describes how to format data collected by your script or application, include it in a request, and have that request authorized by Log Analytics.</span></span>  <span data-ttu-id="1e261-107">В этой статье приведены примеры для PowerShell, C# и Python.</span><span class="sxs-lookup"><span data-stu-id="1e261-107">Examples are provided for PowerShell, C#, and Python.</span></span>

## <a name="concepts"></a><span data-ttu-id="1e261-108">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="1e261-108">Concepts</span></span>
<span data-ttu-id="1e261-109">API сборщика данных HTTP можно использовать, чтобы отправить данные в Log Analytics из любого клиента, который может вызвать REST API.</span><span class="sxs-lookup"><span data-stu-id="1e261-109">You can use the HTTP Data Collector API to send data to Log Analytics from any client that can call a REST API.</span></span>  <span data-ttu-id="1e261-110">Это может быть модуль runbook в службе автоматизации Azure, который собирает данные по управлению из Azure или другого облака, или любая другая система управления, использующая Log Analytics для консолидации и анализа данных.</span><span class="sxs-lookup"><span data-stu-id="1e261-110">This might be a runbook in Azure Automation that collects management data from Azure or another cloud, or it might be an alternate management system that uses Log Analytics to consolidate and analyze data.</span></span>

<span data-ttu-id="1e261-111">Все данные в репозитории Log Analytics хранятся как запись определенного типа.</span><span class="sxs-lookup"><span data-stu-id="1e261-111">All data in the Log Analytics repository is stored as a record with a particular record type.</span></span>  <span data-ttu-id="1e261-112">Чтобы отправить данные в API сборщика данных HTTP, их необходимо отформатировать как несколько записей в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="1e261-112">You format your data to send to the HTTP Data Collector API as multiple records in JSON.</span></span>  <span data-ttu-id="1e261-113">При отправке данных в репозитории для каждой записи в запрошенных полезных данных создается отдельная запись.</span><span class="sxs-lookup"><span data-stu-id="1e261-113">When you submit the data, an individual record is created in the repository for each record in the request payload.</span></span>


![Обзор сборщика данных HTTP](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a><span data-ttu-id="1e261-115">Создание запроса</span><span class="sxs-lookup"><span data-stu-id="1e261-115">Create a request</span></span>
<span data-ttu-id="1e261-116">Чтобы использовать API сборщика данных HTTP, необходимо создать запрос POST, содержащий данные для отправки в нотацию объектов JavaScript (JSON).</span><span class="sxs-lookup"><span data-stu-id="1e261-116">To use the HTTP Data Collector API, you create a POST request that includes the data to send in JavaScript Object Notation (JSON).</span></span>  <span data-ttu-id="1e261-117">В следующих трех таблицах перечислены обязательные атрибуты для каждого запроса.</span><span class="sxs-lookup"><span data-stu-id="1e261-117">The next three tables list the attributes that are required for each request.</span></span> <span data-ttu-id="1e261-118">Более подробное описание каждого из атрибутов приводится далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="1e261-118">We describe each attribute in more detail later in the article.</span></span>

### <a name="request-uri"></a><span data-ttu-id="1e261-119">URI запроса</span><span class="sxs-lookup"><span data-stu-id="1e261-119">Request URI</span></span>
| <span data-ttu-id="1e261-120">Атрибут</span><span class="sxs-lookup"><span data-stu-id="1e261-120">Attribute</span></span> | <span data-ttu-id="1e261-121">Свойство</span><span class="sxs-lookup"><span data-stu-id="1e261-121">Property</span></span> |
|:--- |:--- |
| <span data-ttu-id="1e261-122">Метод</span><span class="sxs-lookup"><span data-stu-id="1e261-122">Method</span></span> |<span data-ttu-id="1e261-123">ПУБЛИКАЦИЯ</span><span class="sxs-lookup"><span data-stu-id="1e261-123">POST</span></span> |
| <span data-ttu-id="1e261-124">URI</span><span class="sxs-lookup"><span data-stu-id="1e261-124">URI</span></span> |<span data-ttu-id="1e261-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span><span class="sxs-lookup"><span data-stu-id="1e261-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span></span> |
| <span data-ttu-id="1e261-126">Тип содержимого</span><span class="sxs-lookup"><span data-stu-id="1e261-126">Content type</span></span> |<span data-ttu-id="1e261-127">приложение/json</span><span class="sxs-lookup"><span data-stu-id="1e261-127">application/json</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="1e261-128">Параметры URI запроса</span><span class="sxs-lookup"><span data-stu-id="1e261-128">Request URI parameters</span></span>
| <span data-ttu-id="1e261-129">Параметр</span><span class="sxs-lookup"><span data-stu-id="1e261-129">Parameter</span></span> | <span data-ttu-id="1e261-130">Описание</span><span class="sxs-lookup"><span data-stu-id="1e261-130">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1e261-131">CustomerID</span><span class="sxs-lookup"><span data-stu-id="1e261-131">CustomerID</span></span> |<span data-ttu-id="1e261-132">Уникальный идентификатор для рабочей области Microsoft Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="1e261-132">The unique identifier for the Microsoft Operations Management Suite workspace.</span></span> |
| <span data-ttu-id="1e261-133">Ресурс</span><span class="sxs-lookup"><span data-stu-id="1e261-133">Resource</span></span> |<span data-ttu-id="1e261-134">Имя ресурса API: /api/logs.</span><span class="sxs-lookup"><span data-stu-id="1e261-134">The API resource name: /api/logs.</span></span> |
| <span data-ttu-id="1e261-135">Версия API</span><span class="sxs-lookup"><span data-stu-id="1e261-135">API Version</span></span> |<span data-ttu-id="1e261-136">Версия API для использования с этим запросом.</span><span class="sxs-lookup"><span data-stu-id="1e261-136">The version of the API to use with this request.</span></span> <span data-ttu-id="1e261-137">В настоящее время это версия 2016-04-01.</span><span class="sxs-lookup"><span data-stu-id="1e261-137">Currently, it's 2016-04-01.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1e261-138">Заголовки запросов</span><span class="sxs-lookup"><span data-stu-id="1e261-138">Request headers</span></span>
| <span data-ttu-id="1e261-139">Заголовок</span><span class="sxs-lookup"><span data-stu-id="1e261-139">Header</span></span> | <span data-ttu-id="1e261-140">Описание</span><span class="sxs-lookup"><span data-stu-id="1e261-140">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1e261-141">Авторизация</span><span class="sxs-lookup"><span data-stu-id="1e261-141">Authorization</span></span> |<span data-ttu-id="1e261-142">Подпись авторизации.</span><span class="sxs-lookup"><span data-stu-id="1e261-142">The authorization signature.</span></span> <span data-ttu-id="1e261-143">Далее в этой статье вы найдете сведения о том, как создать заголовок HMAC-SHA256.</span><span class="sxs-lookup"><span data-stu-id="1e261-143">Later in the article, you can read about how to create an HMAC-SHA256 header.</span></span> |
| <span data-ttu-id="1e261-144">Log-Type</span><span class="sxs-lookup"><span data-stu-id="1e261-144">Log-Type</span></span> |<span data-ttu-id="1e261-145">Укажите тип записи для отправляемых данных.</span><span class="sxs-lookup"><span data-stu-id="1e261-145">Specify the record type of the data that is being submitted.</span></span> <span data-ttu-id="1e261-146">Сейчас для указания типа журнала можно использовать только буквы.</span><span class="sxs-lookup"><span data-stu-id="1e261-146">Currently, the log type supports only alpha characters.</span></span> <span data-ttu-id="1e261-147">Цифры и специальные символы не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="1e261-147">It does not support numerics or special characters.</span></span> |
| <span data-ttu-id="1e261-148">x-ms-date</span><span class="sxs-lookup"><span data-stu-id="1e261-148">x-ms-date</span></span> |<span data-ttu-id="1e261-149">Дата обработки запроса в формате RFC 1123.</span><span class="sxs-lookup"><span data-stu-id="1e261-149">The date that the request was processed, in RFC 1123 format.</span></span> |
| <span data-ttu-id="1e261-150">time-generated-field</span><span class="sxs-lookup"><span data-stu-id="1e261-150">time-generated-field</span></span> |<span data-ttu-id="1e261-151">Имя поля данных, содержащее метку времени элемента данных.</span><span class="sxs-lookup"><span data-stu-id="1e261-151">The name of a field in the data that contains the timestamp of the data item.</span></span> <span data-ttu-id="1e261-152">Если вы укажете здесь поле, его содержимое будет использоваться как значение параметра **TimeGenerated**.</span><span class="sxs-lookup"><span data-stu-id="1e261-152">If you specify a field then its contents are used for **TimeGenerated**.</span></span> <span data-ttu-id="1e261-153">Если это поле не указано, по умолчанию для **TimeGenerated** будет использоваться время приема сообщения.</span><span class="sxs-lookup"><span data-stu-id="1e261-153">If this field isn’t specified, the default for **TimeGenerated** is the time that the message is ingested.</span></span> <span data-ttu-id="1e261-154">Содержимое поля сообщения должно соответствовать формату ISO 8601: YYYY-MM-DDThh:mm:ssZ.</span><span class="sxs-lookup"><span data-stu-id="1e261-154">The contents of the message field should follow the ISO 8601 format YYYY-MM-DDThh:mm:ssZ.</span></span> |

## <a name="authorization"></a><span data-ttu-id="1e261-155">Авторизация</span><span class="sxs-lookup"><span data-stu-id="1e261-155">Authorization</span></span>
<span data-ttu-id="1e261-156">Любой запрос к API сборщика данных HTTP в Log Analytics должен включать заголовок авторизации.</span><span class="sxs-lookup"><span data-stu-id="1e261-156">Any request to the Log Analytics HTTP Data Collector API must include an authorization header.</span></span> <span data-ttu-id="1e261-157">Чтобы проверить подлинность запроса, необходимо подписать запрос с помощью первичного или вторичного ключа для рабочей области, выполняющей запрос.</span><span class="sxs-lookup"><span data-stu-id="1e261-157">To authenticate a request, you must sign the request with either the primary or the secondary key for the workspace that is making the request.</span></span> <span data-ttu-id="1e261-158">Затем следует передать подпись как часть запроса.</span><span class="sxs-lookup"><span data-stu-id="1e261-158">Then, pass that signature as part of the request.</span></span>   

<span data-ttu-id="1e261-159">Вот формат заголовка авторизации:</span><span class="sxs-lookup"><span data-stu-id="1e261-159">Here's the format for the authorization header:</span></span>

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

<span data-ttu-id="1e261-160">*WorkspaceID* — это уникальный идентификатор для рабочей области Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="1e261-160">*WorkspaceID* is the unique identifier for the Operations Management Suite workspace.</span></span> <span data-ttu-id="1e261-161">*Signature* — это [код проверки подлинности сообщения на основе хэша (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx), созданный из запроса и вычисленный с помощью [алгоритма SHA256](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e261-161">*Signature* is a [Hash-based Message Authentication Code (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) that is constructed from the request and then computed by using the [SHA256 algorithm](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span></span> <span data-ttu-id="1e261-162">Затем его можно закодировать с помощью кодировки Base64.</span><span class="sxs-lookup"><span data-stu-id="1e261-162">Then, you encode it by using Base64 encoding.</span></span>

<span data-ttu-id="1e261-163">Используйте этот формат для кодирования строки подписи **SharedKey**:</span><span class="sxs-lookup"><span data-stu-id="1e261-163">Use this format to encode the **SharedKey** signature string:</span></span>

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

<span data-ttu-id="1e261-164">Вот пример строки подписи:</span><span class="sxs-lookup"><span data-stu-id="1e261-164">Here's an example of a signature string:</span></span>

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

<span data-ttu-id="1e261-165">При наличии строки подписи закодируйте ее с помощью алгоритма HMAC-SHA256 в строке в кодировке UTF-8, а затем закодируйте результат в Base64.</span><span class="sxs-lookup"><span data-stu-id="1e261-165">When you have the signature string, encode it by using the HMAC-SHA256 algorithm on the UTF-8-encoded string, and then encode the result as Base64.</span></span> <span data-ttu-id="1e261-166">Используйте следующий формат:</span><span class="sxs-lookup"><span data-stu-id="1e261-166">Use this format:</span></span>

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

<span data-ttu-id="1e261-167">Примеры в следующих разделах содержат образец кода, с помощью которого вы сможете создать заголовок авторизации.</span><span class="sxs-lookup"><span data-stu-id="1e261-167">The samples in the next sections have sample code to help you create an authorization header.</span></span>

## <a name="request-body"></a><span data-ttu-id="1e261-168">Тело запроса</span><span class="sxs-lookup"><span data-stu-id="1e261-168">Request body</span></span>
<span data-ttu-id="1e261-169">Текст сообщения должен иметь формат JSON.</span><span class="sxs-lookup"><span data-stu-id="1e261-169">The body of the message must be in JSON.</span></span> <span data-ttu-id="1e261-170">Он должен содержать одну или несколько записей с парами имени и значения свойств в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="1e261-170">It must include one or more records with the property name and value pairs in this format:</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

<span data-ttu-id="1e261-171">Вы можете сгруппировать в одном запросе несколько записей, используя следующий формат.</span><span class="sxs-lookup"><span data-stu-id="1e261-171">You can batch multiple records together in a single request by using the following format.</span></span> <span data-ttu-id="1e261-172">Все записи должны принадлежать к одному типу.</span><span class="sxs-lookup"><span data-stu-id="1e261-172">All the records must be the same record type.</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
},
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

## <a name="record-type-and-properties"></a><span data-ttu-id="1e261-173">Тип и свойства записи</span><span class="sxs-lookup"><span data-stu-id="1e261-173">Record type and properties</span></span>
<span data-ttu-id="1e261-174">При отправке данных через API сборщика данных HTTP в Log Analytics определяется тип пользовательской записи.</span><span class="sxs-lookup"><span data-stu-id="1e261-174">You define a custom record type when you submit data through the Log Analytics HTTP Data Collector API.</span></span> <span data-ttu-id="1e261-175">В настоящее время нельзя записывать данные в записи существующих типов, созданные с помощью других типов данных и решений.</span><span class="sxs-lookup"><span data-stu-id="1e261-175">Currently, you can't write data to existing record types that were created by other data types and solutions.</span></span> <span data-ttu-id="1e261-176">Log Analytics считывает входящие данные, а затем создает свойства, которые соответствуют типам данных вводимых значений.</span><span class="sxs-lookup"><span data-stu-id="1e261-176">Log Analytics reads the incoming data and then creates properties that match the data types of the values that you enter.</span></span>

<span data-ttu-id="1e261-177">Каждый запрос к API Log Analytics должен содержать заголовок **Log-Type** с именем типа записей.</span><span class="sxs-lookup"><span data-stu-id="1e261-177">Each request to the Log Analytics API must include a **Log-Type** header with the name for the record type.</span></span> <span data-ttu-id="1e261-178">Суффикс **_CL** автоматически добавляется к вводимому имени, чтобы пользовательский журнал отличался от журналов других типов.</span><span class="sxs-lookup"><span data-stu-id="1e261-178">The suffix **_CL** is automatically appended to the name you enter to distinguish it from other log types as a custom log.</span></span> <span data-ttu-id="1e261-179">Например, если ввести имя **MyNewRecordType**, Log Analytics создаст запись с типом **MyNewRecordType_CL**.</span><span class="sxs-lookup"><span data-stu-id="1e261-179">For example, if you enter the name **MyNewRecordType**, Log Analytics creates a record with the type **MyNewRecordType_CL**.</span></span> <span data-ttu-id="1e261-180">Это помогает избежать конфликтов между именами типов, создаваемыми пользователями, и готовыми именами существующих или будущих решений Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1e261-180">This helps ensure that there are no conflicts between user-created type names and those shipped in current or future Microsoft solutions.</span></span>

<span data-ttu-id="1e261-181">Чтобы определить тип данных свойства, Log Analytics добавляет суффикс к имени свойства.</span><span class="sxs-lookup"><span data-stu-id="1e261-181">To identify a property's data type, Log Analytics adds a suffix to the property name.</span></span> <span data-ttu-id="1e261-182">Если свойство содержит значение NULL, свойство не включается в эту запись.</span><span class="sxs-lookup"><span data-stu-id="1e261-182">If a property contains a null value, the property is not included in that record.</span></span> <span data-ttu-id="1e261-183">В таблице ниже перечислены типы данных свойства и соответствующие суффиксы.</span><span class="sxs-lookup"><span data-stu-id="1e261-183">This table lists the property data type and corresponding suffix:</span></span>

| <span data-ttu-id="1e261-184">Тип данных свойства</span><span class="sxs-lookup"><span data-stu-id="1e261-184">Property data type</span></span> | <span data-ttu-id="1e261-185">Суффикс</span><span class="sxs-lookup"><span data-stu-id="1e261-185">Suffix</span></span> |
|:--- |:--- |
| <span data-ttu-id="1e261-186">Строка</span><span class="sxs-lookup"><span data-stu-id="1e261-186">String</span></span> |<span data-ttu-id="1e261-187">_s</span><span class="sxs-lookup"><span data-stu-id="1e261-187">_s</span></span> |
| <span data-ttu-id="1e261-188">Логический</span><span class="sxs-lookup"><span data-stu-id="1e261-188">Boolean</span></span> |<span data-ttu-id="1e261-189">_b</span><span class="sxs-lookup"><span data-stu-id="1e261-189">_b</span></span> |
| <span data-ttu-id="1e261-190">Double</span><span class="sxs-lookup"><span data-stu-id="1e261-190">Double</span></span> |<span data-ttu-id="1e261-191">_d</span><span class="sxs-lookup"><span data-stu-id="1e261-191">_d</span></span> |
| <span data-ttu-id="1e261-192">Дата и время</span><span class="sxs-lookup"><span data-stu-id="1e261-192">Date/time</span></span> |<span data-ttu-id="1e261-193">_t</span><span class="sxs-lookup"><span data-stu-id="1e261-193">_t</span></span> |
| <span data-ttu-id="1e261-194">GUID</span><span class="sxs-lookup"><span data-stu-id="1e261-194">GUID</span></span> |<span data-ttu-id="1e261-195">_g</span><span class="sxs-lookup"><span data-stu-id="1e261-195">_g</span></span> |

<span data-ttu-id="1e261-196">Тип данных, который Log Analytics использует для каждого свойства, зависит от того, существует ли тип записи для новой записи.</span><span class="sxs-lookup"><span data-stu-id="1e261-196">The data type that Log Analytics uses for each property depends on whether the record type for the new record already exists.</span></span>

* <span data-ttu-id="1e261-197">Если тип записи не существует, Log Analytics создает новый тип.</span><span class="sxs-lookup"><span data-stu-id="1e261-197">If the record type does not exist, Log Analytics creates a new one.</span></span> <span data-ttu-id="1e261-198">Log Analytics использует определение типа JSON для указания типа данных для каждого свойства новой записи.</span><span class="sxs-lookup"><span data-stu-id="1e261-198">Log Analytics uses the JSON type inference to determine the data type for each property for the new record.</span></span>
* <span data-ttu-id="1e261-199">Если тип записи не существует, Log Analytics пытается создать новую запись на основе существующих свойств.</span><span class="sxs-lookup"><span data-stu-id="1e261-199">If the record type does exist, Log Analytics attempts to create a new record based on existing properties.</span></span> <span data-ttu-id="1e261-200">Если тип данных для свойства в новой записи не соответствует существующему типу и не может быть преобразован в него или если запись включает свойство, которое не существует, Log Analytics создает новое свойство с соответствующим суффиксом.</span><span class="sxs-lookup"><span data-stu-id="1e261-200">If the data type for a property in the new record doesn’t match and can’t be converted to the existing type, or if the record includes a property that doesn’t exist, Log Analytics creates a new property that has the relevant suffix.</span></span>

<span data-ttu-id="1e261-201">Например, при отправке следующих данных создается запись с тремя свойствами: **number_d**, **boolean_b** и **string_s**:</span><span class="sxs-lookup"><span data-stu-id="1e261-201">For example, this submission entry would create a record with three properties, **number_d**, **boolean_b**, and **string_s**:</span></span>

![Пример записи 1](media/log-analytics-data-collector-api/record-01.png)

<span data-ttu-id="1e261-203">Если отправить следующую запись со всеми значениями в строковом формате, свойства не изменятся.</span><span class="sxs-lookup"><span data-stu-id="1e261-203">If you then submitted this next entry, with all values formatted as strings, the properties would not change.</span></span> <span data-ttu-id="1e261-204">Эти значения можно преобразовать в существующие типы данных:</span><span class="sxs-lookup"><span data-stu-id="1e261-204">These values can be converted to existing data types:</span></span>

![Пример записи 2](media/log-analytics-data-collector-api/record-02.png)

<span data-ttu-id="1e261-206">Но если отправить следующую запись, Log Analytics создаст новые свойства **boolean_d** и **string_d**.</span><span class="sxs-lookup"><span data-stu-id="1e261-206">But, if you then made this next submission, Log Analytics would create the new properties **boolean_d** and **string_d**.</span></span> <span data-ttu-id="1e261-207">Преобразовать эти значения нельзя:</span><span class="sxs-lookup"><span data-stu-id="1e261-207">These values can't be converted:</span></span>

![Пример записи 3](media/log-analytics-data-collector-api/record-03.png)

<span data-ttu-id="1e261-209">Если затем будет отправлена следующая запись, прежде чем будет создан тип записи, Log Analytics создаст запись с тремя свойствами: **number_s**, **boolean_s** и **string_s**.</span><span class="sxs-lookup"><span data-stu-id="1e261-209">If you then submitted the following entry, before the record type was created, Log Analytics would create a record with three properties, **number_s**, **boolean_s**, and **string_s**.</span></span> <span data-ttu-id="1e261-210">В этой записи каждое начальное значение форматируется как строка:</span><span class="sxs-lookup"><span data-stu-id="1e261-210">In this entry, each of the initial values is formatted as a string:</span></span>

![Пример записи 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a><span data-ttu-id="1e261-212">Ограничения данных</span><span class="sxs-lookup"><span data-stu-id="1e261-212">Data limits</span></span>
<span data-ttu-id="1e261-213">Существуют ограничения на данные, публикуемые в API сбора данных Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1e261-213">There are some constraints around the data posted to the Log Analytics Data collection API.</span></span>

* <span data-ttu-id="1e261-214">Не более 30 МБ на публикацию для API сбора данных Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1e261-214">Maximum of 30 MB per post to Log Analytics Data Collector API.</span></span> <span data-ttu-id="1e261-215">Это ограничение размера для одной публикации.</span><span class="sxs-lookup"><span data-stu-id="1e261-215">This is a size limit for a single post.</span></span> <span data-ttu-id="1e261-216">Если данные одной публикации превышают 30 МБ, необходимо разделить данные на меньшие фрагменты и отправить их параллельно.</span><span class="sxs-lookup"><span data-stu-id="1e261-216">If the data from a single post that exceeds 30 MB, you should split the data up to smaller sized chunks and send them concurrently.</span></span>
* <span data-ttu-id="1e261-217">Не более 32 КБ для значений полей.</span><span class="sxs-lookup"><span data-stu-id="1e261-217">Maximum of 32 KB limit for field values.</span></span> <span data-ttu-id="1e261-218">Если значение поля превышает 32 КБ, данные будут усечены.</span><span class="sxs-lookup"><span data-stu-id="1e261-218">If the field value is greater than 32 KB, the data will be truncated.</span></span>
* <span data-ttu-id="1e261-219">Рекомендуемое максимальное количество полей для данного типа — 50.</span><span class="sxs-lookup"><span data-stu-id="1e261-219">Recommended maximum number of fields for a given type is 50.</span></span> <span data-ttu-id="1e261-220">Это ограничение введено для удобства поиска и использования.</span><span class="sxs-lookup"><span data-stu-id="1e261-220">This is a practical limit from a usability and search experience perspective.</span></span>  

## <a name="return-codes"></a><span data-ttu-id="1e261-221">Коды возврата</span><span class="sxs-lookup"><span data-stu-id="1e261-221">Return codes</span></span>
<span data-ttu-id="1e261-222">Код состояния HTTP 200 означает, что запрос получен для обработки.</span><span class="sxs-lookup"><span data-stu-id="1e261-222">The HTTP status code 200 means that the request has been received for processing.</span></span> <span data-ttu-id="1e261-223">Такой результат означает, что операция завершена успешно.</span><span class="sxs-lookup"><span data-stu-id="1e261-223">This indicates that the operation completed successfully.</span></span>

<span data-ttu-id="1e261-224">В этой таблице представлен полный набор кодов состояний, которые может возвращать служба:</span><span class="sxs-lookup"><span data-stu-id="1e261-224">This table lists the complete set of status codes that the service might return:</span></span>

| <span data-ttu-id="1e261-225">Код</span><span class="sxs-lookup"><span data-stu-id="1e261-225">Code</span></span> | <span data-ttu-id="1e261-226">Состояние</span><span class="sxs-lookup"><span data-stu-id="1e261-226">Status</span></span> | <span data-ttu-id="1e261-227">Код ошибки</span><span class="sxs-lookup"><span data-stu-id="1e261-227">Error code</span></span> | <span data-ttu-id="1e261-228">Описание</span><span class="sxs-lookup"><span data-stu-id="1e261-228">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1e261-229">200</span><span class="sxs-lookup"><span data-stu-id="1e261-229">200</span></span> |<span data-ttu-id="1e261-230">ОК</span><span class="sxs-lookup"><span data-stu-id="1e261-230">OK</span></span> | |<span data-ttu-id="1e261-231">Запрос был успешно принят.</span><span class="sxs-lookup"><span data-stu-id="1e261-231">The request was successfully accepted.</span></span> |
| <span data-ttu-id="1e261-232">400</span><span class="sxs-lookup"><span data-stu-id="1e261-232">400</span></span> |<span data-ttu-id="1e261-233">Недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="1e261-233">Bad request</span></span> |<span data-ttu-id="1e261-234">InactiveCustomer</span><span class="sxs-lookup"><span data-stu-id="1e261-234">InactiveCustomer</span></span> |<span data-ttu-id="1e261-235">Рабочая область закрыта.</span><span class="sxs-lookup"><span data-stu-id="1e261-235">The workspace has been closed.</span></span> |
| <span data-ttu-id="1e261-236">400</span><span class="sxs-lookup"><span data-stu-id="1e261-236">400</span></span> |<span data-ttu-id="1e261-237">Недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="1e261-237">Bad request</span></span> |<span data-ttu-id="1e261-238">InvalidApiVersion</span><span class="sxs-lookup"><span data-stu-id="1e261-238">InvalidApiVersion</span></span> |<span data-ttu-id="1e261-239">Указанная версия API не распознана службой.</span><span class="sxs-lookup"><span data-stu-id="1e261-239">The API version that you specified was not recognized by the service.</span></span> |
| <span data-ttu-id="1e261-240">400</span><span class="sxs-lookup"><span data-stu-id="1e261-240">400</span></span> |<span data-ttu-id="1e261-241">Недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="1e261-241">Bad request</span></span> |<span data-ttu-id="1e261-242">InvalidCustomerId</span><span class="sxs-lookup"><span data-stu-id="1e261-242">InvalidCustomerId</span></span> |<span data-ttu-id="1e261-243">Указан недопустимый идентификатор рабочей области.</span><span class="sxs-lookup"><span data-stu-id="1e261-243">The workspace ID specified is invalid.</span></span> |
| <span data-ttu-id="1e261-244">400</span><span class="sxs-lookup"><span data-stu-id="1e261-244">400</span></span> |<span data-ttu-id="1e261-245">Недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="1e261-245">Bad request</span></span> |<span data-ttu-id="1e261-246">InvalidDataFormat</span><span class="sxs-lookup"><span data-stu-id="1e261-246">InvalidDataFormat</span></span> |<span data-ttu-id="1e261-247">Отправлены недопустимые данные JSON.</span><span class="sxs-lookup"><span data-stu-id="1e261-247">Invalid JSON was submitted.</span></span> <span data-ttu-id="1e261-248">Текст ответа может содержать дополнительные сведения о том, как устранить ошибку.</span><span class="sxs-lookup"><span data-stu-id="1e261-248">The response body might contain more information about how to resolve the error.</span></span> |
| <span data-ttu-id="1e261-249">400</span><span class="sxs-lookup"><span data-stu-id="1e261-249">400</span></span> |<span data-ttu-id="1e261-250">Недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="1e261-250">Bad request</span></span> |<span data-ttu-id="1e261-251">InvalidLogType</span><span class="sxs-lookup"><span data-stu-id="1e261-251">InvalidLogType</span></span> |<span data-ttu-id="1e261-252">Указанный тип журнала содержит специальные символы или цифры.</span><span class="sxs-lookup"><span data-stu-id="1e261-252">The log type specified contained special characters or numerics.</span></span> |
| <span data-ttu-id="1e261-253">400</span><span class="sxs-lookup"><span data-stu-id="1e261-253">400</span></span> |<span data-ttu-id="1e261-254">Недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="1e261-254">Bad request</span></span> |<span data-ttu-id="1e261-255">MissingApiVersion</span><span class="sxs-lookup"><span data-stu-id="1e261-255">MissingApiVersion</span></span> |<span data-ttu-id="1e261-256">Версия API не указана.</span><span class="sxs-lookup"><span data-stu-id="1e261-256">The API version wasn’t specified.</span></span> |
| <span data-ttu-id="1e261-257">400</span><span class="sxs-lookup"><span data-stu-id="1e261-257">400</span></span> |<span data-ttu-id="1e261-258">Недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="1e261-258">Bad request</span></span> |<span data-ttu-id="1e261-259">MissingContentType</span><span class="sxs-lookup"><span data-stu-id="1e261-259">MissingContentType</span></span> |<span data-ttu-id="1e261-260">Тип содержимого не указан.</span><span class="sxs-lookup"><span data-stu-id="1e261-260">The content type wasn’t specified.</span></span> |
| <span data-ttu-id="1e261-261">400</span><span class="sxs-lookup"><span data-stu-id="1e261-261">400</span></span> |<span data-ttu-id="1e261-262">Недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="1e261-262">Bad request</span></span> |<span data-ttu-id="1e261-263">MissingLogType</span><span class="sxs-lookup"><span data-stu-id="1e261-263">MissingLogType</span></span> |<span data-ttu-id="1e261-264">Обязательное значение типа журнала не указано.</span><span class="sxs-lookup"><span data-stu-id="1e261-264">The required value log type wasn’t specified.</span></span> |
| <span data-ttu-id="1e261-265">400</span><span class="sxs-lookup"><span data-stu-id="1e261-265">400</span></span> |<span data-ttu-id="1e261-266">Недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="1e261-266">Bad request</span></span> |<span data-ttu-id="1e261-267">UnsupportedContentType</span><span class="sxs-lookup"><span data-stu-id="1e261-267">UnsupportedContentType</span></span> |<span data-ttu-id="1e261-268">Для типа содержимого не было задано значение **application/json**.</span><span class="sxs-lookup"><span data-stu-id="1e261-268">The content type was not set to **application/json**.</span></span> |
| <span data-ttu-id="1e261-269">403</span><span class="sxs-lookup"><span data-stu-id="1e261-269">403</span></span> |<span data-ttu-id="1e261-270">Запрещено</span><span class="sxs-lookup"><span data-stu-id="1e261-270">Forbidden</span></span> |<span data-ttu-id="1e261-271">InvalidAuthorization</span><span class="sxs-lookup"><span data-stu-id="1e261-271">InvalidAuthorization</span></span> |<span data-ttu-id="1e261-272">Службе не удалось проверить подлинность запроса.</span><span class="sxs-lookup"><span data-stu-id="1e261-272">The service failed to authenticate the request.</span></span> <span data-ttu-id="1e261-273">Проверьте правильность идентификатора и ключа подключения рабочей области.</span><span class="sxs-lookup"><span data-stu-id="1e261-273">Verify that the workspace ID and connection key are valid.</span></span> |
| <span data-ttu-id="1e261-274">404</span><span class="sxs-lookup"><span data-stu-id="1e261-274">404</span></span> |<span data-ttu-id="1e261-275">Не найдено</span><span class="sxs-lookup"><span data-stu-id="1e261-275">Not Found</span></span> | | <span data-ttu-id="1e261-276">Указан неправильный URL-адрес либо запрос слишком большой.</span><span class="sxs-lookup"><span data-stu-id="1e261-276">Either the URL provided is incorrect, or the request is too large.</span></span> |
| <span data-ttu-id="1e261-277">429</span><span class="sxs-lookup"><span data-stu-id="1e261-277">429</span></span> |<span data-ttu-id="1e261-278">Слишком много запросов</span><span class="sxs-lookup"><span data-stu-id="1e261-278">Too Many Requests</span></span> | | <span data-ttu-id="1e261-279">В службу поступает слишком большой объем данных из вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="1e261-279">The service is experiencing a high volume of data from your account.</span></span> <span data-ttu-id="1e261-280">Повторите запрос позже.</span><span class="sxs-lookup"><span data-stu-id="1e261-280">Please retry the request later.</span></span> |
| <span data-ttu-id="1e261-281">500</span><span class="sxs-lookup"><span data-stu-id="1e261-281">500</span></span> |<span data-ttu-id="1e261-282">Внутренняя ошибка сервера</span><span class="sxs-lookup"><span data-stu-id="1e261-282">Internal Server Error</span></span> |<span data-ttu-id="1e261-283">UnspecifiedError</span><span class="sxs-lookup"><span data-stu-id="1e261-283">UnspecifiedError</span></span> |<span data-ttu-id="1e261-284">Служба обнаружила внутреннюю ошибку.</span><span class="sxs-lookup"><span data-stu-id="1e261-284">The service encountered an internal error.</span></span> <span data-ttu-id="1e261-285">Повторите запрос.</span><span class="sxs-lookup"><span data-stu-id="1e261-285">Please retry the request.</span></span> |
| <span data-ttu-id="1e261-286">503</span><span class="sxs-lookup"><span data-stu-id="1e261-286">503</span></span> |<span data-ttu-id="1e261-287">Служба недоступна</span><span class="sxs-lookup"><span data-stu-id="1e261-287">Service Unavailable</span></span> |<span data-ttu-id="1e261-288">ServiceUnavailable</span><span class="sxs-lookup"><span data-stu-id="1e261-288">ServiceUnavailable</span></span> |<span data-ttu-id="1e261-289">Служба сейчас недоступна для получения запросов.</span><span class="sxs-lookup"><span data-stu-id="1e261-289">The service currently is unavailable to receive requests.</span></span> <span data-ttu-id="1e261-290">Повторите запрос.</span><span class="sxs-lookup"><span data-stu-id="1e261-290">Please retry your request.</span></span> |

## <a name="query-data"></a><span data-ttu-id="1e261-291">Запрос данных</span><span class="sxs-lookup"><span data-stu-id="1e261-291">Query data</span></span>
<span data-ttu-id="1e261-292">Для запроса данных, отправленных посредством API сборщика данных HTTP в Log Analytics, найдите записи с **типом**, равным указанному вами значению **LogType**, к которому добавлен суффикс**_CL**.</span><span class="sxs-lookup"><span data-stu-id="1e261-292">To query data submitted by the Log Analytics HTTP Data Collector API, search for records with **Type** that is equal to the **LogType** value that you specified, appended with **_CL**.</span></span> <span data-ttu-id="1e261-293">Например, если вы использовали значение **MyCustomLog**, будут возвращены все записи, содержащие текст **Type=MyCustomLog_CL**.</span><span class="sxs-lookup"><span data-stu-id="1e261-293">For example, if you used **MyCustomLog**, then you'd return all records with **Type=MyCustomLog_CL**.</span></span>

>[!NOTE]
> <span data-ttu-id="1e261-294">Если ваша рабочая область переведена на [язык запросов Log Analytics](log-analytics-log-search-upgrade.md), приведенный выше запрос будет изменен следующим образом.</span><span class="sxs-lookup"><span data-stu-id="1e261-294">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above query would change to the following.</span></span>

> `MyCustomLog_CL`

## <a name="sample-requests"></a><span data-ttu-id="1e261-295">Примеры запросов</span><span class="sxs-lookup"><span data-stu-id="1e261-295">Sample requests</span></span>
<span data-ttu-id="1e261-296">В следующих разделах вы найдете примеры отправки данных в API сборщика данных HTTP в Log Analytics с использованием разных языков программирования.</span><span class="sxs-lookup"><span data-stu-id="1e261-296">In the next sections, you'll find samples of how to submit data to the Log Analytics HTTP Data Collector API by using different programming languages.</span></span>

<span data-ttu-id="1e261-297">Для каждого примера выполните следующие действия, чтобы задать переменные в заголовке авторизации:</span><span class="sxs-lookup"><span data-stu-id="1e261-297">For each sample, do these steps to set the variables for the authorization header:</span></span>

1. <span data-ttu-id="1e261-298">На портале Operations Management Suite выберите плитку **Параметры**, а затем перейдите на вкладку **Подключенные источники**.</span><span class="sxs-lookup"><span data-stu-id="1e261-298">In the Operations Management Suite portal, select the **Settings** tile, and then select the **Connected Sources** tab.</span></span>
2. <span data-ttu-id="1e261-299">Справа от **идентификатора рабочей области** щелкните значок копирования и вставьте идентификатор как значение переменной **CustomerID**.</span><span class="sxs-lookup"><span data-stu-id="1e261-299">To the right of **Workspace ID**, select the copy icon, and then paste the ID as the value of the **Customer ID** variable.</span></span>
3. <span data-ttu-id="1e261-300">Справа от **первичного ключа** щелкните значок копирования и вставьте идентификатор как значение переменной **SharedKey**.</span><span class="sxs-lookup"><span data-stu-id="1e261-300">To the right of **Primary Key**, select the copy icon, and then paste the ID as the value of the **Shared Key** variable.</span></span>

<span data-ttu-id="1e261-301">Также можно изменить переменные для типа журнала и данных JSON.</span><span class="sxs-lookup"><span data-stu-id="1e261-301">Alternatively, you can change the variables for the log type and JSON data.</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="1e261-302">Пример для PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e261-302">PowerShell sample</span></span>
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify the name of the record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with the created time for the records
$TimeStampField = "DateValue"


# Create two records with the same set of properties to create
$json = @"
[{  "StringValue": "MyString1",
    "NumberValue": 42,
    "BooleanValue": true,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "9909ED01-A74C-4874-8ABF-D2678E3AE23D"
},
{   "StringValue": "MyString2",
    "NumberValue": 43,
    "BooleanValue": false,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "8809ED01-A74C-4874-8ABF-D2678E3AE23D"
}]
"@

# Create the function to create the authorization signature
Function Build-Signature ($customerId, $sharedKey, $date, $contentLength, $method, $contentType, $resource)
{
    $xHeaders = "x-ms-date:" + $date
    $stringToHash = $method + "`n" + $contentLength + "`n" + $contentType + "`n" + $xHeaders + "`n" + $resource

    $bytesToHash = [Text.Encoding]::UTF8.GetBytes($stringToHash)
    $keyBytes = [Convert]::FromBase64String($sharedKey)

    $sha256 = New-Object System.Security.Cryptography.HMACSHA256
    $sha256.Key = $keyBytes
    $calculatedHash = $sha256.ComputeHash($bytesToHash)
    $encodedHash = [Convert]::ToBase64String($calculatedHash)
    $authorization = 'SharedKey {0}:{1}' -f $customerId,$encodedHash
    return $authorization
}


# Create the function to create and post the request
Function Post-OMSData($customerId, $sharedKey, $body, $logType)
{
    $method = "POST"
    $contentType = "application/json"
    $resource = "/api/logs"
    $rfc1123date = [DateTime]::UtcNow.ToString("r")
    $contentLength = $body.Length
    $signature = Build-Signature `
        -customerId $customerId `
        -sharedKey $sharedKey `
        -date $rfc1123date `
        -contentLength $contentLength `
        -fileName $fileName `
        -method $method `
        -contentType $contentType `
        -resource $resource
    $uri = "https://" + $customerId + ".ods.opinsights.azure.com" + $resource + "?api-version=2016-04-01"

    $headers = @{
        "Authorization" = $signature;
        "Log-Type" = $logType;
        "x-ms-date" = $rfc1123date;
        "time-generated-field" = $TimeStampField;
    }

    $response = Invoke-WebRequest -Uri $uri -Method $method -ContentType $contentType -Headers $headers -Body $body -UseBasicParsing
    return $response.StatusCode

}

# Submit the data to the API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a><span data-ttu-id="1e261-303">Пример на языке C#</span><span class="sxs-lookup"><span data-stu-id="1e261-303">C# sample</span></span>
```
using System;
using System.Net;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Security.Cryptography;
using System.Text;
using System.Threading.Tasks;

namespace OIAPIExample
{
    class ApiExample
    {
        // An example JSON object, with key/value pairs
        static string json = @"[{""DemoField1"":""DemoValue1"",""DemoField2"":""DemoValue2""},{""DemoField3"":""DemoValue3"",""DemoField4"":""DemoValue4""}]";

        // Update customerId to your Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either the primary or the secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of the event type that is being submitted to Log Analytics
        static string LogName = "DemoExample";

        // You can use an optional field to specify the timestamp from the data. If the time field is not specified, Log Analytics assumes the time is the message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for the API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build the API signature
        public static string BuildSignature(string message, string secret)
        {
            var encoding = new System.Text.ASCIIEncoding();
            byte[] keyByte = Convert.FromBase64String(secret);
            byte[] messageBytes = encoding.GetBytes(message);
            using (var hmacsha256 = new HMACSHA256(keyByte))
            {
                byte[] hash = hmacsha256.ComputeHash(messageBytes);
                return Convert.ToBase64String(hash);
            }
        }

        // Send a request to the POST API endpoint
        public static void PostData(string signature, string date, string json)
        {
            try
            {
                string url = "https://" + customerId + ".ods.opinsights.azure.com/api/logs?api-version=2016-04-01";

                System.Net.Http.HttpClient client = new System.Net.Http.HttpClient();
                client.DefaultRequestHeaders.Add("Accept", "application/json");
                client.DefaultRequestHeaders.Add("Log-Type", LogName);
                client.DefaultRequestHeaders.Add("Authorization", signature);
                client.DefaultRequestHeaders.Add("x-ms-date", date);
                client.DefaultRequestHeaders.Add("time-generated-field", TimeStampField);

                System.Net.Http.HttpContent httpContent = new StringContent(json, Encoding.UTF8);
                httpContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");
                Task<System.Net.Http.HttpResponseMessage> response = client.PostAsync(new Uri(url), httpContent);

                System.Net.Http.HttpContent responseContent = response.Result.Content;
                string result = responseContent.ReadAsStringAsync().Result;
                Console.WriteLine("Return Result: " + result);
            }
            catch (Exception excep)
            {
                Console.WriteLine("API Post Exception: " + excep.Message);
            }
        }
    }
}

```

### <a name="python-sample"></a><span data-ttu-id="1e261-304">Пример на языке Python</span><span class="sxs-lookup"><span data-stu-id="1e261-304">Python sample</span></span>
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update the customer ID to your Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For the shared key, use either the primary or the secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# The log type is the name of the event that is being submitted
log_type = 'WebMonitorTest'

# An example JSON web monitor object
json_data = [{
   "slot_ID": 12345,
    "ID": "5cdad72f-c848-4df0-8aaa-ffe033e75d57",
    "availability_Value": 100,
    "performance_Value": 6.954,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "true"
},
{   
    "slot_ID": 67890,
    "ID": "b6bee458-fb65-492e-996d-61c4d7fbb942",
    "availability_Value": 100,
    "performance_Value": 3.379,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "false"
}]
body = json.dumps(json_data)

#####################
######Functions######  
#####################

# Build the API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request to the POST API
def post_data(customer_id, shared_key, body, log_type):
    method = 'POST'
    content_type = 'application/json'
    resource = '/api/logs'
    rfc1123date = datetime.datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
    content_length = len(body)
    signature = build_signature(customer_id, shared_key, rfc1123date, content_length, method, content_type, resource)
    uri = 'https://' + customer_id + '.ods.opinsights.azure.com' + resource + '?api-version=2016-04-01'

    headers = {
        'content-type': content_type,
        'Authorization': signature,
        'Log-Type': log_type,
        'x-ms-date': rfc1123date
    }

    response = requests.post(uri,data=body, headers=headers)
    if (response.status_code >= 200 and response.status_code <= 299):
        print 'Accepted'
    else:
        print "Response code: {}".format(response.status_code)

post_data(customer_id, shared_key, body, log_type)
```

## <a name="next-steps"></a><span data-ttu-id="1e261-305">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1e261-305">Next steps</span></span>
- <span data-ttu-id="1e261-306">Чтобы получить данные из репозитория Log Analytics, используйте [API поиска по журналам](log-analytics-log-search-api.md).</span><span class="sxs-lookup"><span data-stu-id="1e261-306">Use the [Log Search API](log-analytics-log-search-api.md) to retrieve data from the Log Analytics repository.</span></span>
