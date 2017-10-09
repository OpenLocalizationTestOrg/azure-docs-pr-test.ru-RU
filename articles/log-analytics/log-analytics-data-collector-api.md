---
title: "API-Интерфейс сборщика данных HTTP Analytics aaaLog | Документы Microsoft"
description: "Можно использовать hello API сборщика данных HTTP аналитики журналов tooadd POST JSON данных toohello анализа журналов репозиторий из любого клиента, который можно вызвать hello REST API. В этой статье описывается toouse hello API и содержит примеры toopublish данных с использованием различных языков программирования."
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
ms.openlocfilehash: c2921082831c49da764d946ac9c4fab975a38185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="send-data-toolog-analytics-with-hello-http-data-collector-api"></a><span data-ttu-id="df32e-104">Отправка данных tooLog аналитика с hello HTTP API-Интерфейс сборщика данных</span><span class="sxs-lookup"><span data-stu-id="df32e-104">Send data tooLog Analytics with hello HTTP Data Collector API</span></span>
<span data-ttu-id="df32e-105">В этой статье показано, как toouse hello tooLog данных API-Интерфейс сборщика данных HTTP toosend Analytics из клиента REST API.</span><span class="sxs-lookup"><span data-stu-id="df32e-105">This article shows you how toouse hello HTTP Data Collector API toosend data tooLog Analytics from a REST API client.</span></span>  <span data-ttu-id="df32e-106">Он описывает, как tooformat данными, собранными сценарий или приложение, включить его в запросе и иметь этот запрос авторизован службой аналитики журналов.</span><span class="sxs-lookup"><span data-stu-id="df32e-106">It describes how tooformat data collected by your script or application, include it in a request, and have that request authorized by Log Analytics.</span></span>  <span data-ttu-id="df32e-107">В этой статье приведены примеры для PowerShell, C# и Python.</span><span class="sxs-lookup"><span data-stu-id="df32e-107">Examples are provided for PowerShell, C#, and Python.</span></span>

## <a name="concepts"></a><span data-ttu-id="df32e-108">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="df32e-108">Concepts</span></span>
<span data-ttu-id="df32e-109">Можно использовать toosend данных API-Интерфейс сборщика данных HTTP hello tooLog Analytics из любого клиента, который может вызывать API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="df32e-109">You can use hello HTTP Data Collector API toosend data tooLog Analytics from any client that can call a REST API.</span></span>  <span data-ttu-id="df32e-110">Это может быть runbook в автоматизации Azure, которая собирает управления данные из Azure или другой облака или он может быть системой альтернативного управления, которая использует tooconsolidate анализа журналов и анализа данных.</span><span class="sxs-lookup"><span data-stu-id="df32e-110">This might be a runbook in Azure Automation that collects management data from Azure or another cloud, or it might be an alternate management system that uses Log Analytics tooconsolidate and analyze data.</span></span>

<span data-ttu-id="df32e-111">Все данные в репозитории hello анализа журналов хранятся как запись с записей типа.</span><span class="sxs-lookup"><span data-stu-id="df32e-111">All data in hello Log Analytics repository is stored as a record with a particular record type.</span></span>  <span data-ttu-id="df32e-112">Формат вашего toohello toosend данных HTTP API-Интерфейс сборщика данных нескольких записей в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="df32e-112">You format your data toosend toohello HTTP Data Collector API as multiple records in JSON.</span></span>  <span data-ttu-id="df32e-113">При отправке данных hello отдельную запись создается в репозитории hello для каждой записи в полезных данных запроса hello.</span><span class="sxs-lookup"><span data-stu-id="df32e-113">When you submit hello data, an individual record is created in hello repository for each record in hello request payload.</span></span>


![Обзор сборщика данных HTTP](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a><span data-ttu-id="df32e-115">Создание запроса</span><span class="sxs-lookup"><span data-stu-id="df32e-115">Create a request</span></span>
<span data-ttu-id="df32e-116">API сборщик данных toouse hello HTTP, создайте запрос POST, включающий toosend данных hello в JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="df32e-116">toouse hello HTTP Data Collector API, you create a POST request that includes hello data toosend in JavaScript Object Notation (JSON).</span></span>  <span data-ttu-id="df32e-117">Здравствуйте, атрибуты hello списка следующих трех таблиц, необходимых для каждого запроса.</span><span class="sxs-lookup"><span data-stu-id="df32e-117">hello next three tables list hello attributes that are required for each request.</span></span> <span data-ttu-id="df32e-118">Описаны более подробно далее в статье hello каждого атрибута.</span><span class="sxs-lookup"><span data-stu-id="df32e-118">We describe each attribute in more detail later in hello article.</span></span>

### <a name="request-uri"></a><span data-ttu-id="df32e-119">URI запроса</span><span class="sxs-lookup"><span data-stu-id="df32e-119">Request URI</span></span>
| <span data-ttu-id="df32e-120">Атрибут</span><span class="sxs-lookup"><span data-stu-id="df32e-120">Attribute</span></span> | <span data-ttu-id="df32e-121">Свойство</span><span class="sxs-lookup"><span data-stu-id="df32e-121">Property</span></span> |
|:--- |:--- |
| <span data-ttu-id="df32e-122">Метод</span><span class="sxs-lookup"><span data-stu-id="df32e-122">Method</span></span> |<span data-ttu-id="df32e-123">ПУБЛИКАЦИЯ</span><span class="sxs-lookup"><span data-stu-id="df32e-123">POST</span></span> |
| <span data-ttu-id="df32e-124">URI</span><span class="sxs-lookup"><span data-stu-id="df32e-124">URI</span></span> |<span data-ttu-id="df32e-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span><span class="sxs-lookup"><span data-stu-id="df32e-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span></span> |
| <span data-ttu-id="df32e-126">Тип содержимого</span><span class="sxs-lookup"><span data-stu-id="df32e-126">Content type</span></span> |<span data-ttu-id="df32e-127">приложение/json</span><span class="sxs-lookup"><span data-stu-id="df32e-127">application/json</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="df32e-128">Параметры URI запроса</span><span class="sxs-lookup"><span data-stu-id="df32e-128">Request URI parameters</span></span>
| <span data-ttu-id="df32e-129">Параметр</span><span class="sxs-lookup"><span data-stu-id="df32e-129">Parameter</span></span> | <span data-ttu-id="df32e-130">Описание</span><span class="sxs-lookup"><span data-stu-id="df32e-130">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="df32e-131">CustomerID</span><span class="sxs-lookup"><span data-stu-id="df32e-131">CustomerID</span></span> |<span data-ttu-id="df32e-132">Уникальный идентификатор Hello для рабочей области Microsoft Operations Management Suite hello.</span><span class="sxs-lookup"><span data-stu-id="df32e-132">hello unique identifier for hello Microsoft Operations Management Suite workspace.</span></span> |
| <span data-ttu-id="df32e-133">Ресурс</span><span class="sxs-lookup"><span data-stu-id="df32e-133">Resource</span></span> |<span data-ttu-id="df32e-134">Имя ресурса Hello API: / api/logs.</span><span class="sxs-lookup"><span data-stu-id="df32e-134">hello API resource name: /api/logs.</span></span> |
| <span data-ttu-id="df32e-135">Версия API</span><span class="sxs-lookup"><span data-stu-id="df32e-135">API Version</span></span> |<span data-ttu-id="df32e-136">версия Hello toouse hello API с этим запросом.</span><span class="sxs-lookup"><span data-stu-id="df32e-136">hello version of hello API toouse with this request.</span></span> <span data-ttu-id="df32e-137">В настоящее время это версия 2016-04-01.</span><span class="sxs-lookup"><span data-stu-id="df32e-137">Currently, it's 2016-04-01.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="df32e-138">Заголовки запросов</span><span class="sxs-lookup"><span data-stu-id="df32e-138">Request headers</span></span>
| <span data-ttu-id="df32e-139">Заголовок</span><span class="sxs-lookup"><span data-stu-id="df32e-139">Header</span></span> | <span data-ttu-id="df32e-140">Описание</span><span class="sxs-lookup"><span data-stu-id="df32e-140">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="df32e-141">Авторизация</span><span class="sxs-lookup"><span data-stu-id="df32e-141">Authorization</span></span> |<span data-ttu-id="df32e-142">подпись авторизации Hello.</span><span class="sxs-lookup"><span data-stu-id="df32e-142">hello authorization signature.</span></span> <span data-ttu-id="df32e-143">Далее в статье hello вы найдете сведения о том, как заголовок toocreate HMAC-SHA256.</span><span class="sxs-lookup"><span data-stu-id="df32e-143">Later in hello article, you can read about how toocreate an HMAC-SHA256 header.</span></span> |
| <span data-ttu-id="df32e-144">Log-Type</span><span class="sxs-lookup"><span data-stu-id="df32e-144">Log-Type</span></span> |<span data-ttu-id="df32e-145">Укажите тип записи hello hello отправляемых данных.</span><span class="sxs-lookup"><span data-stu-id="df32e-145">Specify hello record type of hello data that is being submitted.</span></span> <span data-ttu-id="df32e-146">В настоящее время тип журнала hello поддерживает только текстовые символы.</span><span class="sxs-lookup"><span data-stu-id="df32e-146">Currently, hello log type supports only alpha characters.</span></span> <span data-ttu-id="df32e-147">Цифры и специальные символы не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="df32e-147">It does not support numerics or special characters.</span></span> |
| <span data-ttu-id="df32e-148">x-ms-date</span><span class="sxs-lookup"><span data-stu-id="df32e-148">x-ms-date</span></span> |<span data-ttu-id="df32e-149">Дата Hello обработки этого запроса hello, в формате RFC 1123.</span><span class="sxs-lookup"><span data-stu-id="df32e-149">hello date that hello request was processed, in RFC 1123 format.</span></span> |
| <span data-ttu-id="df32e-150">time-generated-field</span><span class="sxs-lookup"><span data-stu-id="df32e-150">time-generated-field</span></span> |<span data-ttu-id="df32e-151">Имя поля данных hello, содержащей timestamp hello элемента данных hello Hello.</span><span class="sxs-lookup"><span data-stu-id="df32e-151">hello name of a field in hello data that contains hello timestamp of hello data item.</span></span> <span data-ttu-id="df32e-152">Если вы укажете здесь поле, его содержимое будет использоваться как значение параметра **TimeGenerated**.</span><span class="sxs-lookup"><span data-stu-id="df32e-152">If you specify a field then its contents are used for **TimeGenerated**.</span></span> <span data-ttu-id="df32e-153">Если это поле не указано, по умолчанию для Здравствуйте, **TimeGenerated** — время hello, hello полученный является сообщение.</span><span class="sxs-lookup"><span data-stu-id="df32e-153">If this field isn’t specified, hello default for **TimeGenerated** is hello time that hello message is ingested.</span></span> <span data-ttu-id="df32e-154">содержимое поля сообщения hello Hello следовать hello ISO 8601 формат гггг-мм-: Ssz.</span><span class="sxs-lookup"><span data-stu-id="df32e-154">hello contents of hello message field should follow hello ISO 8601 format YYYY-MM-DDThh:mm:ssZ.</span></span> |

## <a name="authorization"></a><span data-ttu-id="df32e-155">Авторизация</span><span class="sxs-lookup"><span data-stu-id="df32e-155">Authorization</span></span>
<span data-ttu-id="df32e-156">Любой запрос toohello API сборщика данных HTTP аналитики журналов должен включать заголовок авторизации.</span><span class="sxs-lookup"><span data-stu-id="df32e-156">Any request toohello Log Analytics HTTP Data Collector API must include an authorization header.</span></span> <span data-ttu-id="df32e-157">tooauthenticate запроса, необходимо подписать запрос hello с hello первичный или вторичный ключ hello hello рабочей области, которая делает запрос hello.</span><span class="sxs-lookup"><span data-stu-id="df32e-157">tooauthenticate a request, you must sign hello request with either hello primary or hello secondary key for hello workspace that is making hello request.</span></span> <span data-ttu-id="df32e-158">Затем передайте подпись в составе запроса hello.</span><span class="sxs-lookup"><span data-stu-id="df32e-158">Then, pass that signature as part of hello request.</span></span>   

<span data-ttu-id="df32e-159">Вот hello формат для заголовка авторизации hello.</span><span class="sxs-lookup"><span data-stu-id="df32e-159">Here's hello format for hello authorization header:</span></span>

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

<span data-ttu-id="df32e-160">*ИД рабочей области* — уникальный идентификатор рабочей области Operations Management Suite hello hello.</span><span class="sxs-lookup"><span data-stu-id="df32e-160">*WorkspaceID* is hello unique identifier for hello Operations Management Suite workspace.</span></span> <span data-ttu-id="df32e-161">*Подпись* — [хэш-проверки подлинности сообщения код (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) , создается из запроса hello и затем вычисляется с помощью hello [алгоритм SHA256](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span><span class="sxs-lookup"><span data-stu-id="df32e-161">*Signature* is a [Hash-based Message Authentication Code (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) that is constructed from hello request and then computed by using hello [SHA256 algorithm](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span></span> <span data-ttu-id="df32e-162">Затем его можно закодировать с помощью кодировки Base64.</span><span class="sxs-lookup"><span data-stu-id="df32e-162">Then, you encode it by using Base64 encoding.</span></span>

<span data-ttu-id="df32e-163">Используйте этот формат tooencode hello **SharedKey** строки подписи:</span><span class="sxs-lookup"><span data-stu-id="df32e-163">Use this format tooencode hello **SharedKey** signature string:</span></span>

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

<span data-ttu-id="df32e-164">Вот пример строки подписи:</span><span class="sxs-lookup"><span data-stu-id="df32e-164">Here's an example of a signature string:</span></span>

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

<span data-ttu-id="df32e-165">При наличии строки подписи hello, кодировать их с помощью hello алгоритм HMAC-SHA256 на hello строку в кодировке UTF-8 и затем кодирует hello результат в Base64.</span><span class="sxs-lookup"><span data-stu-id="df32e-165">When you have hello signature string, encode it by using hello HMAC-SHA256 algorithm on hello UTF-8-encoded string, and then encode hello result as Base64.</span></span> <span data-ttu-id="df32e-166">Используйте следующий формат:</span><span class="sxs-lookup"><span data-stu-id="df32e-166">Use this format:</span></span>

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

<span data-ttu-id="df32e-167">Примеры Hello в следующих разделах hello имеют toohelp кода образца, создайте заголовок авторизации.</span><span class="sxs-lookup"><span data-stu-id="df32e-167">hello samples in hello next sections have sample code toohelp you create an authorization header.</span></span>

## <a name="request-body"></a><span data-ttu-id="df32e-168">Тело запроса</span><span class="sxs-lookup"><span data-stu-id="df32e-168">Request body</span></span>
<span data-ttu-id="df32e-169">тело Hello приветственное сообщение должно быть в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="df32e-169">hello body of hello message must be in JSON.</span></span> <span data-ttu-id="df32e-170">Она должна включать один или несколько записей с пар имен и значений свойств hello в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="df32e-170">It must include one or more records with hello property name and value pairs in this format:</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

<span data-ttu-id="df32e-171">Позволяет выполнять пакетные несколько записей вместе в одном запросе с помощью hello следующая формата.</span><span class="sxs-lookup"><span data-stu-id="df32e-171">You can batch multiple records together in a single request by using hello following format.</span></span> <span data-ttu-id="df32e-172">Все записи hello должно быть hello таким же типом записи.</span><span class="sxs-lookup"><span data-stu-id="df32e-172">All hello records must be hello same record type.</span></span>

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

## <a name="record-type-and-properties"></a><span data-ttu-id="df32e-173">Тип и свойства записи</span><span class="sxs-lookup"><span data-stu-id="df32e-173">Record type and properties</span></span>
<span data-ttu-id="df32e-174">Определить тип пользовательских записей, при передаче данных с помощью hello API сборщика данных HTTP аналитики журналов.</span><span class="sxs-lookup"><span data-stu-id="df32e-174">You define a custom record type when you submit data through hello Log Analytics HTTP Data Collector API.</span></span> <span data-ttu-id="df32e-175">В настоящее время не удается записать данные tooexisting типы записей, которые были созданы в другие типы данных и решениях.</span><span class="sxs-lookup"><span data-stu-id="df32e-175">Currently, you can't write data tooexisting record types that were created by other data types and solutions.</span></span> <span data-ttu-id="df32e-176">Служба аналитики журналов считывает hello входящих данных, а затем создает свойства, которые соответствуют типам данных hello значений Привет вводимых.</span><span class="sxs-lookup"><span data-stu-id="df32e-176">Log Analytics reads hello incoming data and then creates properties that match hello data types of hello values that you enter.</span></span>

<span data-ttu-id="df32e-177">Каждый запрос toohello, необходимо включить API аналитики журналов **тип журнала** заголовок с именем hello hello типа записи.</span><span class="sxs-lookup"><span data-stu-id="df32e-177">Each request toohello Log Analytics API must include a **Log-Type** header with hello name for hello record type.</span></span> <span data-ttu-id="df32e-178">суффикс Hello **_CL** — имя автоматически добавленных toohello введите toodistinguish его из других журналов типы как пользовательского журнала.</span><span class="sxs-lookup"><span data-stu-id="df32e-178">hello suffix **_CL** is automatically appended toohello name you enter toodistinguish it from other log types as a custom log.</span></span> <span data-ttu-id="df32e-179">Например, если ввести имя hello **MyNewRecordType**, аналитика журналов создается запись с типом hello **MyNewRecordType_CL**.</span><span class="sxs-lookup"><span data-stu-id="df32e-179">For example, if you enter hello name **MyNewRecordType**, Log Analytics creates a record with hello type **MyNewRecordType_CL**.</span></span> <span data-ttu-id="df32e-180">Это помогает избежать конфликтов между именами типов, создаваемыми пользователями, и готовыми именами существующих или будущих решений Microsoft.</span><span class="sxs-lookup"><span data-stu-id="df32e-180">This helps ensure that there are no conflicts between user-created type names and those shipped in current or future Microsoft solutions.</span></span>

<span data-ttu-id="df32e-181">Тип данных свойства tooidentify, аналитика журналов добавляет суффикс toohello имя свойства.</span><span class="sxs-lookup"><span data-stu-id="df32e-181">tooidentify a property's data type, Log Analytics adds a suffix toohello property name.</span></span> <span data-ttu-id="df32e-182">Если свойство содержит значение null, свойство hello не включено в этой записи.</span><span class="sxs-lookup"><span data-stu-id="df32e-182">If a property contains a null value, hello property is not included in that record.</span></span> <span data-ttu-id="df32e-183">В этой таблице перечислены тип данных свойства hello и соответствующего суффикса.</span><span class="sxs-lookup"><span data-stu-id="df32e-183">This table lists hello property data type and corresponding suffix:</span></span>

| <span data-ttu-id="df32e-184">Тип данных свойства</span><span class="sxs-lookup"><span data-stu-id="df32e-184">Property data type</span></span> | <span data-ttu-id="df32e-185">Суффикс</span><span class="sxs-lookup"><span data-stu-id="df32e-185">Suffix</span></span> |
|:--- |:--- |
| <span data-ttu-id="df32e-186">Строка</span><span class="sxs-lookup"><span data-stu-id="df32e-186">String</span></span> |<span data-ttu-id="df32e-187">_s</span><span class="sxs-lookup"><span data-stu-id="df32e-187">_s</span></span> |
| <span data-ttu-id="df32e-188">Логический</span><span class="sxs-lookup"><span data-stu-id="df32e-188">Boolean</span></span> |<span data-ttu-id="df32e-189">_b</span><span class="sxs-lookup"><span data-stu-id="df32e-189">_b</span></span> |
| <span data-ttu-id="df32e-190">Double</span><span class="sxs-lookup"><span data-stu-id="df32e-190">Double</span></span> |<span data-ttu-id="df32e-191">_d</span><span class="sxs-lookup"><span data-stu-id="df32e-191">_d</span></span> |
| <span data-ttu-id="df32e-192">Дата и время</span><span class="sxs-lookup"><span data-stu-id="df32e-192">Date/time</span></span> |<span data-ttu-id="df32e-193">_t</span><span class="sxs-lookup"><span data-stu-id="df32e-193">_t</span></span> |
| <span data-ttu-id="df32e-194">GUID</span><span class="sxs-lookup"><span data-stu-id="df32e-194">GUID</span></span> |<span data-ttu-id="df32e-195">_g</span><span class="sxs-lookup"><span data-stu-id="df32e-195">_g</span></span> |

<span data-ttu-id="df32e-196">Hello тип данных, который использует служба аналитики журналов для каждого свойства зависит от типа записи hello для новой записи hello, существуют ли уже.</span><span class="sxs-lookup"><span data-stu-id="df32e-196">hello data type that Log Analytics uses for each property depends on whether hello record type for hello new record already exists.</span></span>

* <span data-ttu-id="df32e-197">Если тип записи hello не существует, аналитика журналов создает новую.</span><span class="sxs-lookup"><span data-stu-id="df32e-197">If hello record type does not exist, Log Analytics creates a new one.</span></span> <span data-ttu-id="df32e-198">Служба аналитики журналов использует hello JSON вывод toodetermine hello тип данных для каждого свойства для новой записи hello.</span><span class="sxs-lookup"><span data-stu-id="df32e-198">Log Analytics uses hello JSON type inference toodetermine hello data type for each property for hello new record.</span></span>
* <span data-ttu-id="df32e-199">Если существует тип записи hello, аналитика журналов попыток toocreate новой записи на основе существующих свойств.</span><span class="sxs-lookup"><span data-stu-id="df32e-199">If hello record type does exist, Log Analytics attempts toocreate a new record based on existing properties.</span></span> <span data-ttu-id="df32e-200">Если hello тип данных для свойства в новой записи hello не соответствуют и не может быть преобразованный toohello существующий тип или если hello запись содержит свойство, которое не существует, аналитика журналов создает новое свойство с соответствующей суффикс hello.</span><span class="sxs-lookup"><span data-stu-id="df32e-200">If hello data type for a property in hello new record doesn’t match and can’t be converted toohello existing type, or if hello record includes a property that doesn’t exist, Log Analytics creates a new property that has hello relevant suffix.</span></span>

<span data-ttu-id="df32e-201">Например, при отправке следующих данных создается запись с тремя свойствами: **number_d**, **boolean_b** и **string_s**:</span><span class="sxs-lookup"><span data-stu-id="df32e-201">For example, this submission entry would create a record with three properties, **number_d**, **boolean_b**, and **string_s**:</span></span>

![Пример записи 1](media/log-analytics-data-collector-api/record-01.png)

<span data-ttu-id="df32e-203">Если введен этот следующей записи со всеми значениями в строковом формате hello свойства не будут изменяться.</span><span class="sxs-lookup"><span data-stu-id="df32e-203">If you then submitted this next entry, with all values formatted as strings, hello properties would not change.</span></span> <span data-ttu-id="df32e-204">Эти значения могут быть tooexisting преобразованные типы данных:</span><span class="sxs-lookup"><span data-stu-id="df32e-204">These values can be converted tooexisting data types:</span></span>

![Пример записи 2](media/log-analytics-data-collector-api/record-02.png)

<span data-ttu-id="df32e-206">Но при внесении следующего Отправка анализа журналов приведет hello новые свойства **boolean_d** и **string_d**.</span><span class="sxs-lookup"><span data-stu-id="df32e-206">But, if you then made this next submission, Log Analytics would create hello new properties **boolean_d** and **string_d**.</span></span> <span data-ttu-id="df32e-207">Преобразовать эти значения нельзя:</span><span class="sxs-lookup"><span data-stu-id="df32e-207">These values can't be converted:</span></span>

![Пример записи 3](media/log-analytics-data-collector-api/record-03.png)

<span data-ttu-id="df32e-209">Если введен hello следующие записи, перед созданием тип записи hello анализа журналов создать запись с тремя свойствами **указанного**, **boolean_s**, и **string_s**.</span><span class="sxs-lookup"><span data-stu-id="df32e-209">If you then submitted hello following entry, before hello record type was created, Log Analytics would create a record with three properties, **number_s**, **boolean_s**, and **string_s**.</span></span> <span data-ttu-id="df32e-210">В этой операции каждый начальные значения hello форматируется как строка:</span><span class="sxs-lookup"><span data-stu-id="df32e-210">In this entry, each of hello initial values is formatted as a string:</span></span>

![Пример записи 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a><span data-ttu-id="df32e-212">Ограничения данных</span><span class="sxs-lookup"><span data-stu-id="df32e-212">Data limits</span></span>
<span data-ttu-id="df32e-213">Существуют некоторые ограничения вокруг hello данные, отправленные toohello сбора данных аналитики журналов API.</span><span class="sxs-lookup"><span data-stu-id="df32e-213">There are some constraints around hello data posted toohello Log Analytics Data collection API.</span></span>

* <span data-ttu-id="df32e-214">Не более 30 МБ на tooLog post Analytics API-Интерфейс сборщика данных.</span><span class="sxs-lookup"><span data-stu-id="df32e-214">Maximum of 30 MB per post tooLog Analytics Data Collector API.</span></span> <span data-ttu-id="df32e-215">Это ограничение размера для одной публикации.</span><span class="sxs-lookup"><span data-stu-id="df32e-215">This is a size limit for a single post.</span></span> <span data-ttu-id="df32e-216">Если hello данных из одной записи, размер которой превышает 30 МБ, следует разбить hello фрагментами данных вверх toosmaller размера, а затем отправить их одновременно.</span><span class="sxs-lookup"><span data-stu-id="df32e-216">If hello data from a single post that exceeds 30 MB, you should split hello data up toosmaller sized chunks and send them concurrently.</span></span>
* <span data-ttu-id="df32e-217">Не более 32 КБ для значений полей.</span><span class="sxs-lookup"><span data-stu-id="df32e-217">Maximum of 32 KB limit for field values.</span></span> <span data-ttu-id="df32e-218">Если значение поля hello превышает 32 КБ, hello данные будут усечены.</span><span class="sxs-lookup"><span data-stu-id="df32e-218">If hello field value is greater than 32 KB, hello data will be truncated.</span></span>
* <span data-ttu-id="df32e-219">Рекомендуемое максимальное количество полей для данного типа — 50.</span><span class="sxs-lookup"><span data-stu-id="df32e-219">Recommended maximum number of fields for a given type is 50.</span></span> <span data-ttu-id="df32e-220">Это ограничение введено для удобства поиска и использования.</span><span class="sxs-lookup"><span data-stu-id="df32e-220">This is a practical limit from a usability and search experience perspective.</span></span>  

## <a name="return-codes"></a><span data-ttu-id="df32e-221">Коды возврата</span><span class="sxs-lookup"><span data-stu-id="df32e-221">Return codes</span></span>
<span data-ttu-id="df32e-222">Код состояния HTTP 200 Hello означает, что для обработки был получен этот запрос hello.</span><span class="sxs-lookup"><span data-stu-id="df32e-222">hello HTTP status code 200 means that hello request has been received for processing.</span></span> <span data-ttu-id="df32e-223">Это означает, что hello, операция выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="df32e-223">This indicates that hello operation completed successfully.</span></span>

<span data-ttu-id="df32e-224">В этой таблице перечислены hello полный набор кодов состояний, которые могут возвращать hello службы.</span><span class="sxs-lookup"><span data-stu-id="df32e-224">This table lists hello complete set of status codes that hello service might return:</span></span>

| <span data-ttu-id="df32e-225">Код</span><span class="sxs-lookup"><span data-stu-id="df32e-225">Code</span></span> | <span data-ttu-id="df32e-226">Состояние</span><span class="sxs-lookup"><span data-stu-id="df32e-226">Status</span></span> | <span data-ttu-id="df32e-227">Код ошибки</span><span class="sxs-lookup"><span data-stu-id="df32e-227">Error code</span></span> | <span data-ttu-id="df32e-228">Описание</span><span class="sxs-lookup"><span data-stu-id="df32e-228">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df32e-229">200</span><span class="sxs-lookup"><span data-stu-id="df32e-229">200</span></span> |<span data-ttu-id="df32e-230">ОК</span><span class="sxs-lookup"><span data-stu-id="df32e-230">OK</span></span> | |<span data-ttu-id="df32e-231">успешно принят запрос Hello.</span><span class="sxs-lookup"><span data-stu-id="df32e-231">hello request was successfully accepted.</span></span> |
| <span data-ttu-id="df32e-232">400</span><span class="sxs-lookup"><span data-stu-id="df32e-232">400</span></span> |<span data-ttu-id="df32e-233">Недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="df32e-233">Bad request</span></span> |<span data-ttu-id="df32e-234">InactiveCustomer</span><span class="sxs-lookup"><span data-stu-id="df32e-234">InactiveCustomer</span></span> |<span data-ttu-id="df32e-235">Рабочая область Hello был закрыт.</span><span class="sxs-lookup"><span data-stu-id="df32e-235">hello workspace has been closed.</span></span> |
| <span data-ttu-id="df32e-236">400</span><span class="sxs-lookup"><span data-stu-id="df32e-236">400</span></span> |<span data-ttu-id="df32e-237">Недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="df32e-237">Bad request</span></span> |<span data-ttu-id="df32e-238">InvalidApiVersion</span><span class="sxs-lookup"><span data-stu-id="df32e-238">InvalidApiVersion</span></span> |<span data-ttu-id="df32e-239">Hello API версии, указанной службой hello не распознана.</span><span class="sxs-lookup"><span data-stu-id="df32e-239">hello API version that you specified was not recognized by hello service.</span></span> |
| <span data-ttu-id="df32e-240">400</span><span class="sxs-lookup"><span data-stu-id="df32e-240">400</span></span> |<span data-ttu-id="df32e-241">Недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="df32e-241">Bad request</span></span> |<span data-ttu-id="df32e-242">InvalidCustomerId</span><span class="sxs-lookup"><span data-stu-id="df32e-242">InvalidCustomerId</span></span> |<span data-ttu-id="df32e-243">указан недопустимый ИД рабочей области Hello.</span><span class="sxs-lookup"><span data-stu-id="df32e-243">hello workspace ID specified is invalid.</span></span> |
| <span data-ttu-id="df32e-244">400</span><span class="sxs-lookup"><span data-stu-id="df32e-244">400</span></span> |<span data-ttu-id="df32e-245">Недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="df32e-245">Bad request</span></span> |<span data-ttu-id="df32e-246">InvalidDataFormat</span><span class="sxs-lookup"><span data-stu-id="df32e-246">InvalidDataFormat</span></span> |<span data-ttu-id="df32e-247">Отправлены недопустимые данные JSON.</span><span class="sxs-lookup"><span data-stu-id="df32e-247">Invalid JSON was submitted.</span></span> <span data-ttu-id="df32e-248">текст Hello ответа может содержать дополнительные сведения о как tooresolve hello ошибки.</span><span class="sxs-lookup"><span data-stu-id="df32e-248">hello response body might contain more information about how tooresolve hello error.</span></span> |
| <span data-ttu-id="df32e-249">400</span><span class="sxs-lookup"><span data-stu-id="df32e-249">400</span></span> |<span data-ttu-id="df32e-250">Недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="df32e-250">Bad request</span></span> |<span data-ttu-id="df32e-251">InvalidLogType</span><span class="sxs-lookup"><span data-stu-id="df32e-251">InvalidLogType</span></span> |<span data-ttu-id="df32e-252">Тип журнала Hello указан автономной специальные символы и цифры.</span><span class="sxs-lookup"><span data-stu-id="df32e-252">hello log type specified contained special characters or numerics.</span></span> |
| <span data-ttu-id="df32e-253">400</span><span class="sxs-lookup"><span data-stu-id="df32e-253">400</span></span> |<span data-ttu-id="df32e-254">Недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="df32e-254">Bad request</span></span> |<span data-ttu-id="df32e-255">MissingApiVersion</span><span class="sxs-lookup"><span data-stu-id="df32e-255">MissingApiVersion</span></span> |<span data-ttu-id="df32e-256">версия API Hello не был указан.</span><span class="sxs-lookup"><span data-stu-id="df32e-256">hello API version wasn’t specified.</span></span> |
| <span data-ttu-id="df32e-257">400</span><span class="sxs-lookup"><span data-stu-id="df32e-257">400</span></span> |<span data-ttu-id="df32e-258">Недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="df32e-258">Bad request</span></span> |<span data-ttu-id="df32e-259">MissingContentType</span><span class="sxs-lookup"><span data-stu-id="df32e-259">MissingContentType</span></span> |<span data-ttu-id="df32e-260">Тип содержимого Hello не был указан.</span><span class="sxs-lookup"><span data-stu-id="df32e-260">hello content type wasn’t specified.</span></span> |
| <span data-ttu-id="df32e-261">400</span><span class="sxs-lookup"><span data-stu-id="df32e-261">400</span></span> |<span data-ttu-id="df32e-262">Недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="df32e-262">Bad request</span></span> |<span data-ttu-id="df32e-263">MissingLogType</span><span class="sxs-lookup"><span data-stu-id="df32e-263">MissingLogType</span></span> |<span data-ttu-id="df32e-264">Hello требуется значение тип журнала не был указан.</span><span class="sxs-lookup"><span data-stu-id="df32e-264">hello required value log type wasn’t specified.</span></span> |
| <span data-ttu-id="df32e-265">400</span><span class="sxs-lookup"><span data-stu-id="df32e-265">400</span></span> |<span data-ttu-id="df32e-266">Недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="df32e-266">Bad request</span></span> |<span data-ttu-id="df32e-267">UnsupportedContentType</span><span class="sxs-lookup"><span data-stu-id="df32e-267">UnsupportedContentType</span></span> |<span data-ttu-id="df32e-268">Тип содержимого Hello не было задано слишком**приложение/json**.</span><span class="sxs-lookup"><span data-stu-id="df32e-268">hello content type was not set too**application/json**.</span></span> |
| <span data-ttu-id="df32e-269">403</span><span class="sxs-lookup"><span data-stu-id="df32e-269">403</span></span> |<span data-ttu-id="df32e-270">Запрещено</span><span class="sxs-lookup"><span data-stu-id="df32e-270">Forbidden</span></span> |<span data-ttu-id="df32e-271">InvalidAuthorization</span><span class="sxs-lookup"><span data-stu-id="df32e-271">InvalidAuthorization</span></span> |<span data-ttu-id="df32e-272">Hello службы не удалось выполнить запрос tooauthenticate hello.</span><span class="sxs-lookup"><span data-stu-id="df32e-272">hello service failed tooauthenticate hello request.</span></span> <span data-ttu-id="df32e-273">Проверьте ключ рабочей области, hello идентификатор и подключения являются допустимыми.</span><span class="sxs-lookup"><span data-stu-id="df32e-273">Verify that hello workspace ID and connection key are valid.</span></span> |
| <span data-ttu-id="df32e-274">404</span><span class="sxs-lookup"><span data-stu-id="df32e-274">404</span></span> |<span data-ttu-id="df32e-275">Не найдено</span><span class="sxs-lookup"><span data-stu-id="df32e-275">Not Found</span></span> | | <span data-ttu-id="df32e-276">Возможно, неверно указан URL-адрес hello или hello запроса слишком велик.</span><span class="sxs-lookup"><span data-stu-id="df32e-276">Either hello URL provided is incorrect, or hello request is too large.</span></span> |
| <span data-ttu-id="df32e-277">429</span><span class="sxs-lookup"><span data-stu-id="df32e-277">429</span></span> |<span data-ttu-id="df32e-278">Слишком много запросов</span><span class="sxs-lookup"><span data-stu-id="df32e-278">Too Many Requests</span></span> | | <span data-ttu-id="df32e-279">Hello служба столкнулась с большим объемом данных из вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="df32e-279">hello service is experiencing a high volume of data from your account.</span></span> <span data-ttu-id="df32e-280">Повторите попытку запроса hello позже.</span><span class="sxs-lookup"><span data-stu-id="df32e-280">Please retry hello request later.</span></span> |
| <span data-ttu-id="df32e-281">500</span><span class="sxs-lookup"><span data-stu-id="df32e-281">500</span></span> |<span data-ttu-id="df32e-282">Внутренняя ошибка сервера</span><span class="sxs-lookup"><span data-stu-id="df32e-282">Internal Server Error</span></span> |<span data-ttu-id="df32e-283">UnspecifiedError</span><span class="sxs-lookup"><span data-stu-id="df32e-283">UnspecifiedError</span></span> |<span data-ttu-id="df32e-284">Внутренняя ошибка службы Hello.</span><span class="sxs-lookup"><span data-stu-id="df32e-284">hello service encountered an internal error.</span></span> <span data-ttu-id="df32e-285">Запрос hello. Повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="df32e-285">Please retry hello request.</span></span> |
| <span data-ttu-id="df32e-286">503</span><span class="sxs-lookup"><span data-stu-id="df32e-286">503</span></span> |<span data-ttu-id="df32e-287">Служба недоступна</span><span class="sxs-lookup"><span data-stu-id="df32e-287">Service Unavailable</span></span> |<span data-ttu-id="df32e-288">ServiceUnavailable</span><span class="sxs-lookup"><span data-stu-id="df32e-288">ServiceUnavailable</span></span> |<span data-ttu-id="df32e-289">Служба Hello в настоящее время является недоступным tooreceive запросов.</span><span class="sxs-lookup"><span data-stu-id="df32e-289">hello service currently is unavailable tooreceive requests.</span></span> <span data-ttu-id="df32e-290">Повторите запрос.</span><span class="sxs-lookup"><span data-stu-id="df32e-290">Please retry your request.</span></span> |

## <a name="query-data"></a><span data-ttu-id="df32e-291">Запрос данных</span><span class="sxs-lookup"><span data-stu-id="df32e-291">Query data</span></span>
<span data-ttu-id="df32e-292">tooquery данные, зафиксированные hello API сборщика данных HTTP аналитики журналов, поиска записей в режиме **тип** , равно toohello **LogType** с добавлением указанным вами значением **_CL**.</span><span class="sxs-lookup"><span data-stu-id="df32e-292">tooquery data submitted by hello Log Analytics HTTP Data Collector API, search for records with **Type** that is equal toohello **LogType** value that you specified, appended with **_CL**.</span></span> <span data-ttu-id="df32e-293">Например, если вы использовали значение **MyCustomLog**, будут возвращены все записи, содержащие текст **Type=MyCustomLog_CL**.</span><span class="sxs-lookup"><span data-stu-id="df32e-293">For example, if you used **MyCustomLog**, then you'd return all records with **Type=MyCustomLog_CL**.</span></span>

>[!NOTE]
> <span data-ttu-id="df32e-294">Если обновленный toohello рабочей области [языка запросов новый журнал аналитики](log-analytics-log-search-upgrade.md), то hello выше запрос изменится toohello следующее.</span><span class="sxs-lookup"><span data-stu-id="df32e-294">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above query would change toohello following.</span></span>

> `MyCustomLog_CL`

## <a name="sample-requests"></a><span data-ttu-id="df32e-295">Примеры запросов</span><span class="sxs-lookup"><span data-stu-id="df32e-295">Sample requests</span></span>
<span data-ttu-id="df32e-296">В следующих разделах hello, вы найдете примеры данных toosubmit toohello API сборщика данных HTTP аналитики журналов с помощью различных языков программирования.</span><span class="sxs-lookup"><span data-stu-id="df32e-296">In hello next sections, you'll find samples of how toosubmit data toohello Log Analytics HTTP Data Collector API by using different programming languages.</span></span>

<span data-ttu-id="df32e-297">Для каждого образца выполните указанные ниже действия tooset hello переменных для заголовка авторизации hello:</span><span class="sxs-lookup"><span data-stu-id="df32e-297">For each sample, do these steps tooset hello variables for hello authorization header:</span></span>

1. <span data-ttu-id="df32e-298">На портале Operations Management Suite hello, выберите hello **параметры** плитку, а затем выберите hello **подключенные источники** вкладки.</span><span class="sxs-lookup"><span data-stu-id="df32e-298">In hello Operations Management Suite portal, select hello **Settings** tile, and then select hello **Connected Sources** tab.</span></span>
2. <span data-ttu-id="df32e-299">toohello справа от **идентификатор рабочей области**, выберите значок копирования hello, а затем вставьте идентификатор hello в качестве значения hello hello **Customer ID** переменной.</span><span class="sxs-lookup"><span data-stu-id="df32e-299">toohello right of **Workspace ID**, select hello copy icon, and then paste hello ID as hello value of hello **Customer ID** variable.</span></span>
3. <span data-ttu-id="df32e-300">toohello справа от **первичного ключа**, выберите значок копирования hello, а затем вставьте идентификатор hello в качестве значения hello hello **Shared Key** переменной.</span><span class="sxs-lookup"><span data-stu-id="df32e-300">toohello right of **Primary Key**, select hello copy icon, and then paste hello ID as hello value of hello **Shared Key** variable.</span></span>

<span data-ttu-id="df32e-301">Кроме того можно изменить hello переменных типа hello журнала и данных JSON.</span><span class="sxs-lookup"><span data-stu-id="df32e-301">Alternatively, you can change hello variables for hello log type and JSON data.</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="df32e-302">Пример для PowerShell</span><span class="sxs-lookup"><span data-stu-id="df32e-302">PowerShell sample</span></span>
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify hello name of hello record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with hello created time for hello records
$TimeStampField = "DateValue"


# Create two records with hello same set of properties toocreate
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

# Create hello function toocreate hello authorization signature
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


# Create hello function toocreate and post hello request
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

# Submit hello data toohello API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a><span data-ttu-id="df32e-303">Пример на языке C#</span><span class="sxs-lookup"><span data-stu-id="df32e-303">C# sample</span></span>
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

        // Update customerId tooyour Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either hello primary or hello secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of hello event type that is being submitted tooLog Analytics
        static string LogName = "DemoExample";

        // You can use an optional field toospecify hello timestamp from hello data. If hello time field is not specified, Log Analytics assumes hello time is hello message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for hello API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build hello API signature
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

        // Send a request toohello POST API endpoint
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

### <a name="python-sample"></a><span data-ttu-id="df32e-304">Пример на языке Python</span><span class="sxs-lookup"><span data-stu-id="df32e-304">Python sample</span></span>
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update hello customer ID tooyour Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For hello shared key, use either hello primary or hello secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# hello log type is hello name of hello event that is being submitted
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

# Build hello API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request toohello POST API
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

## <a name="next-steps"></a><span data-ttu-id="df32e-305">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="df32e-305">Next steps</span></span>
- <span data-ttu-id="df32e-306">Используйте hello [API поиска журналов](log-analytics-log-search-api.md) tooretrieve данными из репозитория анализа журналов hello.</span><span class="sxs-lookup"><span data-stu-id="df32e-306">Use hello [Log Search API](log-analytics-log-search-api.md) tooretrieve data from hello Log Analytics repository.</span></span>
