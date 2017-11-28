---
title: "Импорт aaaRestrictions и известные проблемы в API управления Azure | Документы Microsoft"
description: "Сведения об известных проблемах и ограничения для импорта в службы управления API Azure, используя форматы прикладной программный Интерфейс, WSDL или WADL hello."
services: api-management
documentationcenter: 
author: mattfarm
manager: vlvinogr
editor: 
ms.assetid: 7a5a63f0-3e72-49d3-a28c-1bb23ab495e2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: apipm
ms.openlocfilehash: 0bed5ace47de6ccbfbecba25ea6b69c5329de089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="api-import-restrictions-and-known-issues"></a><span data-ttu-id="4d145-103">Ограничения и известные проблемы при импорте API</span><span class="sxs-lookup"><span data-stu-id="4d145-103">API import restrictions and known issues</span></span>
## <a name="about-this-list"></a><span data-ttu-id="4d145-104">Об этом списке</span><span class="sxs-lookup"><span data-stu-id="4d145-104">About this list</span></span>
<span data-ttu-id="4d145-105">Во время передачи tooensure все усилия, что при импорте API в службе управления API Azure как можно менее заметным и отсутствие ошибок, возможно, мы иногда накладывать ограничения или выявить проблемы, которые потребуется устранить, прежде чем импортировать успешно toobe.</span><span class="sxs-lookup"><span data-stu-id="4d145-105">While every effort is made tooensure that importing your API into Azure API Management is as seamless and problem-free as possible, we do occasionally impose restrictions or identify issues that will need toobe rectified before you can successfully import.</span></span> <span data-ttu-id="4d145-106">В этой статье приведены эти, сгруппированные по формат импорта hello hello API.</span><span class="sxs-lookup"><span data-stu-id="4d145-106">This article documents these, organised by hello import format of hello API.</span></span>

## <span data-ttu-id="4d145-107"><a name="open-api"> </a>Open API/Swagger</span><span class="sxs-lookup"><span data-stu-id="4d145-107"><a name="open-api"> </a>Open API/Swagger</span></span>
<span data-ttu-id="4d145-108">Как правило, появление ошибок при импорте документа прикладной программный Интерфейс, убедитесь, проверки его - либо с помощью конструктора hello в hello новый портал Azure (конструктора - Front End - открытых API спецификации редактор), либо со сходной стороннего средства, такие как <a href="http://www.swagger.io"> Swagger редактор</a>.</span><span class="sxs-lookup"><span data-stu-id="4d145-108">In general, if you are receiving errors importing your Open API document, please ensure you have validated it - either using hello designer in hello new Azure Portal (Design - Front End - Open API Specification Editor), or with a 3rd party tool such as <a href="http://www.swagger.io">Swagger Editor</a>.</span></span>

* <span data-ttu-id="4d145-109">**Host Name** (Имя узла): необходимо указать атрибут имени узла.</span><span class="sxs-lookup"><span data-stu-id="4d145-109">**Host Name** we require a host name attribute.</span></span>
* <span data-ttu-id="4d145-110">**Base Path** (Базовый путь): необходимо указать атрибут базового пути.</span><span class="sxs-lookup"><span data-stu-id="4d145-110">**Base Path** we require a base path attribute.</span></span>
* <span data-ttu-id="4d145-111">**Schemes** (Схемы): необходимо указать массив схем.</span><span class="sxs-lookup"><span data-stu-id="4d145-111">**Schemes** we require a scheme array.</span></span> 

## <span data-ttu-id="4d145-112"><a name="wsdl"> </a>WSDL</span><span class="sxs-lookup"><span data-stu-id="4d145-112"><a name="wsdl"> </a>WSDL</span></span>
<span data-ttu-id="4d145-113">Файлы WSDL toogenerate используется API-интерфейс SOAP к серверу, или служат hello внутренних API-интерфейса SOAP для REST.</span><span class="sxs-lookup"><span data-stu-id="4d145-113">WSDL files are used toogenerate SOAP Pass-through APIs, or serve as hello backend of a SOAP-to-REST API.</span></span>

* <span data-ttu-id="4d145-114">**WSDL:import**: в настоящее время интерфейсы API, использующие этот атрибут, не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="4d145-114">**WSDL:Import** we do not currently support APIs using this attribute.</span></span> <span data-ttu-id="4d145-115">Клиенты должен объединять hello импортировать элементы в одном документе.</span><span class="sxs-lookup"><span data-stu-id="4d145-115">Customers should merge hello imported elements into one document.</span></span>
* <span data-ttu-id="4d145-116">**Сообщения из нескольких частей**: в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="4d145-116">**Messages with multiple parts** are currently not supported.</span></span>
* <span data-ttu-id="4d145-117">**WCF wsHttpBinding**: в службах SOAP, созданных с помощью технологии Windows Communication Foundation, следует использовать значение basicHttpBinding. Значение wsHttpBinding не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="4d145-117">**WCF wsHttpBinding** SOAP services created with Windows Communication Foundation should use basicHttpBinding - wsHttpBinding is not supported.</span></span>
* <span data-ttu-id="4d145-118">**MTOM**: службы, использующие MTOM, <em>могут</em> работать.</span><span class="sxs-lookup"><span data-stu-id="4d145-118">**MTOM** Services using MTOM <em>may</em> work.</span></span> <span data-ttu-id="4d145-119">Но официальная поддержка в данный момент не предоставляется.</span><span class="sxs-lookup"><span data-stu-id="4d145-119">Official support is not offered at this time.</span></span>
* <span data-ttu-id="4d145-120">**Рекурсия** типов, которые определены рекурсивно (например ссылаться tooan массив сами) не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="4d145-120">**Recursion** types that are defined recursively (e.g. refer tooan array of themselves) are not supported.</span></span>

## <span data-ttu-id="4d145-121"><a name="wadl"> </a>WADL</span><span class="sxs-lookup"><span data-stu-id="4d145-121"><a name="wadl"> </a>WADL</span></span>
<span data-ttu-id="4d145-122">У нас нет сведений о проблемах импорта с помощью формата WADL.</span><span class="sxs-lookup"><span data-stu-id="4d145-122">There are no known WADL import issues currently.</span></span>


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
