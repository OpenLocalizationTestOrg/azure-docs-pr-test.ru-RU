---
title: "aaaManaging сущностей служб мультимедиа с REST | Документы Microsoft"
description: "Узнайте, как службы мультимедиа toomanage сущности с REST API."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 95262a32-0f2a-4286-b9e2-1a1ca6399b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: bcdc5288e422ebc4e6f682a97da4e925ce237a79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-media-services-entities-with-rest"></a><span data-ttu-id="b6a33-103">Управление сущностями служб мультимедиа с помощью REST</span><span class="sxs-lookup"><span data-stu-id="b6a33-103">Managing Media Services entities with REST</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b6a33-104">REST</span><span class="sxs-lookup"><span data-stu-id="b6a33-104">REST</span></span>](media-services-rest-manage-entities.md)
> * [<span data-ttu-id="b6a33-105">.NET</span><span class="sxs-lookup"><span data-stu-id="b6a33-105">.NET</span></span>](media-services-dotnet-manage-entities.md)
> 
> 

<span data-ttu-id="b6a33-106">Службы мультимедиа Microsoft Azure — это служба на основе REST, построенная на базе OData 3.</span><span class="sxs-lookup"><span data-stu-id="b6a33-106">Microsoft Azure Media Services is a REST-based service built on OData v3.</span></span> <span data-ttu-id="b6a33-107">Можно добавить запрос, обновления и удаления сущностей во многом hello же способом, что и на любой другой службе OData.</span><span class="sxs-lookup"><span data-stu-id="b6a33-107">You can add, query, update, and delete entities in much hello same way as you can on any other OData service.</span></span> <span data-ttu-id="b6a33-108">Исключения будут выделены, когда это понадобится.</span><span class="sxs-lookup"><span data-stu-id="b6a33-108">Exceptions will be called out when applicable.</span></span> <span data-ttu-id="b6a33-109">Дополнительные сведения об OData см. в [документации по протоколу Open Data Protocol](http://www.odata.org/documentation/).</span><span class="sxs-lookup"><span data-stu-id="b6a33-109">For more information on OData, see [Open Data Protocol documentation](http://www.odata.org/documentation/).</span></span>

<span data-ttu-id="b6a33-110">В этом разделе показано, как toomanage сущностей служб мультимедиа Azure с REST.</span><span class="sxs-lookup"><span data-stu-id="b6a33-110">This topic shows you how toomanage Azure Media Services entities with REST.</span></span>

>[!NOTE]
> <span data-ttu-id="b6a33-111">Начиная с 1 апреля 2017 г., записи любого задания в вашей учетной записи старше 90 дней автоматически удаляется, а также связанные с ней записи задачи, даже если hello общее количество записей ниже максимальная квота hello.</span><span class="sxs-lookup"><span data-stu-id="b6a33-111">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if hello total number of records is below hello maximum quota.</span></span> <span data-ttu-id="b6a33-112">Например, 1 апреля 2017 г. будет автоматически удалена любая запись задания в вашей учетной записи, созданная ранее 31 декабря 2016 г.</span><span class="sxs-lookup"><span data-stu-id="b6a33-112">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="b6a33-113">Если вам нужна информация задания или задачи tooarchive hello, можно использовать код hello, описанные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="b6a33-113">If you need tooarchive hello job/task information, you can use hello code described in this topic.</span></span>

## <a name="considerations"></a><span data-ttu-id="b6a33-114">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="b6a33-114">Considerations</span></span>  

<span data-ttu-id="b6a33-115">При доступе к сущностям в службах мультимедиа необходимо задать определенные поля и значения заголовков в HTTP-запросах.</span><span class="sxs-lookup"><span data-stu-id="b6a33-115">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="b6a33-116">Дополнительную информацию см. в статье [Обзор интерфейса REST API служб мультимедиа](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="b6a33-116">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="b6a33-117">Подключение служб tooMedia</span><span class="sxs-lookup"><span data-stu-id="b6a33-117">Connect tooMedia Services</span></span>

<span data-ttu-id="b6a33-118">Сведения о tooconnect toohello AMS API, в статье [hello доступа к API служб мультимедиа Azure с проверкой подлинности Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="b6a33-118">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="b6a33-119">После успешного подключения toohttps://media.windows.net, будет получено перенаправление 301 указывающее другой URI служб Media Services.</span><span class="sxs-lookup"><span data-stu-id="b6a33-119">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="b6a33-120">Необходимо внести toohello последующих вызовов новый URI.</span><span class="sxs-lookup"><span data-stu-id="b6a33-120">You must make subsequent calls toohello new URI.</span></span>

## <a name="adding-entities"></a><span data-ttu-id="b6a33-121">Добавление сущностей</span><span class="sxs-lookup"><span data-stu-id="b6a33-121">Adding entities</span></span>
<span data-ttu-id="b6a33-122">Каждая сущность в службах мультимедиа добавляется tooan набора сущностей, таких как активы, через запрос POST HTTP.</span><span class="sxs-lookup"><span data-stu-id="b6a33-122">Every entity in Media Services is added tooan entity set, such as Assets, through a POST HTTP request.</span></span>

<span data-ttu-id="b6a33-123">Следующий пример показывает как Hello toocreate AccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="b6a33-123">hello following example shows how toocreate an AccessPolicy.</span></span>

    POST https://media.windows.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

## <a name="querying-entities"></a><span data-ttu-id="b6a33-124">Запрашивание сущностей</span><span class="sxs-lookup"><span data-stu-id="b6a33-124">Querying entities</span></span>
<span data-ttu-id="b6a33-125">Запрашивание и перечисление сущностей выполняется просто. Для этого используется только запрос HTTP GET и необязательные операции OData.</span><span class="sxs-lookup"><span data-stu-id="b6a33-125">Querying and listing entities is straightforward and only involves a GET HTTP request and optional OData operations.</span></span>
<span data-ttu-id="b6a33-126">Hello следующий пример извлекает список всех объектов mediaprocessor.</span><span class="sxs-lookup"><span data-stu-id="b6a33-126">hello following example retrieves a list of all MediaProcessor entities.</span></span>

    GET https://media.windows.net/API/MediaProcessors HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="b6a33-127">Можно также получить определенный объект или все наборы сущностей, связанные с определенной сущности, такие как в следующих примерах hello:</span><span class="sxs-lookup"><span data-stu-id="b6a33-127">You can also retrieve a specific entity or all entity sets associated with a specific entity, such as in hello following examples:</span></span>

    GET https://media.windows.net/API/JobTemplates('nb:jtid:UUID:e81192f5-576f-b247-b781-70a790c20e7c') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336907474&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=OpuY0CeTylqFFcFaP4pKUVGesT4PGx4CP55zDf2zXnc%3d
    Host: media.windows.net

    GET https://media.windows.net/API/JobTemplates('nb:jtid:UUID:e81192f5-576f-b247-b781-70a790c20e7c')/TaskTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336907474&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=OpuY0CeTylqFFcFaP4pKUVGesT4PGx4CP55zDf2zXnc%3d
    Host: media.windows.net

<span data-ttu-id="b6a33-128">Hello следующий пример возвращает hello свойству состояния всех заданий.</span><span class="sxs-lookup"><span data-stu-id="b6a33-128">hello following example returns only hello State property of all Jobs.</span></span>

    GET https://media.windows.net/API/Jobs?$select=State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="b6a33-129">Hello следующий пример возвращает все объекты Jobtemplate с именем hello «SampleTemplate».</span><span class="sxs-lookup"><span data-stu-id="b6a33-129">hello following example returns all JobTemplates with hello name "SampleTemplate."</span></span>

    GET https://media.windows.net/API/JobTemplates?$filter=startswith(Name,%20'SampleTemplate') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

> [!NOTE]
> <span data-ttu-id="b6a33-130">Hello $expand операция не поддерживается в службах мультимедиа также hello неподдерживаемые методы LINQ, описанных в рекомендации по LINQ (службы данных WCF).</span><span class="sxs-lookup"><span data-stu-id="b6a33-130">hello $expand operation is not supported in Media Services as well as hello unsupported LINQ methods described in LINQ Considerations (WCF Data Services).</span></span>
> 
> 

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="b6a33-131">Перечисление больших коллекций сущностей</span><span class="sxs-lookup"><span data-stu-id="b6a33-131">Enumerating through large collections of entities</span></span>
<span data-ttu-id="b6a33-132">При запросе сущности, имеется ограничение в 1000 сущностей, возвращаемых одновременно, так как открытые v2 REST ограничивает результаты too1000 результаты запроса.</span><span class="sxs-lookup"><span data-stu-id="b6a33-132">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results too1000 results.</span></span> <span data-ttu-id="b6a33-133">Используйте **пропустить** и **верхней** tooenumerate через hello большое количество сущностей.</span><span class="sxs-lookup"><span data-stu-id="b6a33-133">Use **skip** and **top** tooenumerate through hello large collection of entities.</span></span> 

<span data-ttu-id="b6a33-134">Следующий пример показывает как Hello toouse **пропустить** и **верхней** tooskip hello сначала 2000 заданий и get hello рядом 1000 заданий.</span><span class="sxs-lookup"><span data-stu-id="b6a33-134">hello following example shows how toouse **skip** and **top** tooskip hello first 2000 jobs and get hello next 1000 jobs.</span></span>  

    GET https://media.windows.net/api/Jobs()?$skip=2000&$top=1000 HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

## <a name="updating-entities"></a><span data-ttu-id="b6a33-135">Обновление сущностей</span><span class="sxs-lookup"><span data-stu-id="b6a33-135">Updating entities</span></span>
<span data-ttu-id="b6a33-136">В зависимости от типа сущности hello и состояние hello, что он находится в можно обновить свойства с помощью обновления, PUT или MERGE HTTP.</span><span class="sxs-lookup"><span data-stu-id="b6a33-136">Depending on hello entity type and hello state that it is in, you can update properties on that entity through a PATCH, PUT, or MERGE HTTP requests.</span></span> <span data-ttu-id="b6a33-137">Дополнительные сведения об этих операциях см. [здесь](https://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="b6a33-137">For more information about these operations, see [PATCH/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="b6a33-138">Привет, в следующем примере кода показано, как tooupdate hello свойство Name объекта Asset.</span><span class="sxs-lookup"><span data-stu-id="b6a33-138">hello following code example shows how tooupdate hello Name property on an Asset entity.</span></span>

    MERGE https://media.windows.net/API/Assets('nb:cid:UUID:80782407-3f87-4e60-a43e-5e4454232f60') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337083279&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=DMLQXWah4jO0icpfwyws5k%2b1aCDfz9KDGIGao20xk6g%3d
    Host: media.windows.net
    Content-Length: 21
    Expect: 100-continue

    {"Name" : "NewName" }

## <a name="deleting-entities"></a><span data-ttu-id="b6a33-139">Удаление сущностей</span><span class="sxs-lookup"><span data-stu-id="b6a33-139">Deleting entities</span></span>
<span data-ttu-id="b6a33-140">Сущности в службах мультимедиа можно удалить с помощью запроса HTTP DELETE.</span><span class="sxs-lookup"><span data-stu-id="b6a33-140">Entities can be deleted in Media Services by using a DELETE HTTP request.</span></span> <span data-ttu-id="b6a33-141">В зависимости от сущности hello hello порядок, в котором можно удалить сущности могут быть важны.</span><span class="sxs-lookup"><span data-stu-id="b6a33-141">Depending on hello entity, hello order in which you delete entities may be important.</span></span> <span data-ttu-id="b6a33-142">Например, сущности, такие как средства требуется отозвать (или удалить) все Локаторы, которые ссылаются на данный объект Asset перед удалением hello активов.</span><span class="sxs-lookup"><span data-stu-id="b6a33-142">For example, entities such as Assets require that you revoke (or delete) all Locators that reference that particular Asset before deleting hello Asset.</span></span>

<span data-ttu-id="b6a33-143">Следующий пример показывает как Hello toodelete указателя, который был используется tooupload файла в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="b6a33-143">hello following example shows how toodelete a Locator that was used tooupload a file into blob storage.</span></span>

    DELETE https://media.windows.net/API/Locators('nb:lid:UUID:76dcc8e8-4230-463d-97b0-ce25c41b5c8d') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 0

## <a name="media-services-learning-paths"></a><span data-ttu-id="b6a33-144">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="b6a33-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b6a33-145">Отзывы</span><span class="sxs-lookup"><span data-stu-id="b6a33-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

