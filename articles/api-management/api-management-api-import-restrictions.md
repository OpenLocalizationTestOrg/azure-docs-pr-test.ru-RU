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
# <a name="api-import-restrictions-and-known-issues"></a>Ограничения и известные проблемы при импорте API
## <a name="about-this-list"></a>Об этом списке
Во время передачи tooensure все усилия, что при импорте API в службе управления API Azure как можно менее заметным и отсутствие ошибок, возможно, мы иногда накладывать ограничения или выявить проблемы, которые потребуется устранить, прежде чем импортировать успешно toobe. В этой статье приведены эти, сгруппированные по формат импорта hello hello API.

## <a name="open-api"> </a>Open API/Swagger
Как правило, появление ошибок при импорте документа прикладной программный Интерфейс, убедитесь, проверки его - либо с помощью конструктора hello в hello новый портал Azure (конструктора - Front End - открытых API спецификации редактор), либо со сходной стороннего средства, такие как <a href="http://www.swagger.io"> Swagger редактор</a>.

* **Host Name** (Имя узла): необходимо указать атрибут имени узла.
* **Base Path** (Базовый путь): необходимо указать атрибут базового пути.
* **Schemes** (Схемы): необходимо указать массив схем. 

## <a name="wsdl"> </a>WSDL
Файлы WSDL toogenerate используется API-интерфейс SOAP к серверу, или служат hello внутренних API-интерфейса SOAP для REST.

* **WSDL:import**: в настоящее время интерфейсы API, использующие этот атрибут, не поддерживаются. Клиенты должен объединять hello импортировать элементы в одном документе.
* **Сообщения из нескольких частей**: в настоящее время не поддерживаются.
* **WCF wsHttpBinding**: в службах SOAP, созданных с помощью технологии Windows Communication Foundation, следует использовать значение basicHttpBinding. Значение wsHttpBinding не поддерживается.
* **MTOM**: службы, использующие MTOM, <em>могут</em> работать. Но официальная поддержка в данный момент не предоставляется.
* **Рекурсия** типов, которые определены рекурсивно (например ссылаться tooan массив сами) не поддерживаются.

## <a name="wadl"> </a>WADL
У нас нет сведений о проблемах импорта с помощью формата WADL.


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
