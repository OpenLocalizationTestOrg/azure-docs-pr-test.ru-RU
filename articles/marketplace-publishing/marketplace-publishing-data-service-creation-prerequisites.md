---
title: "Необходимые условия для создания службы данных для hello Marketplace aaaTechnical | Документы Microsoft"
description: "Сведения о требованиях hello для создания toodeploy службы данных и продавать hello Azure Marketplace"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: aaff609a-1cd1-4146-98f4-d04166b0fce0
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 2bba4282473fed63c3fcab43043a97e179705844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="technical-pre-requisites-for-creating-a-data-service-offer-for-hello-azure-marketplace"></a>Предложение технические необходимые компоненты для создания службы данных для hello Azure Marketplace
> [!IMPORTANT]
> **В настоящее время мы больше не подключаем новые издатели служб данных. Новые службы данных не будут утверждены для добавления в список.** Если у вас есть бизнес-приложений SaaS хотелось бы toopublish Дополнительные сведения можно найти на AppSource [здесь](https://appsource.microsoft.com/partners). Если у вас есть приложениях IaaS или разработчик службы вы бы как toopublish в Azure Marketplace можно найти дополнительные сведения о [здесь](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Чтение hello процесса тщательно перед началом и понять, где и почему каждого шага выполняются. Настолько, насколько возможно, вы должны подготовить сведения о компании и другие данные, загрузить необходимые средства и перед началом процесса создания предложения hello создать технические компоненты.

Должно быть hello следующих элементов готов до начала процесса hello:

## <a name="make-a-decision-on-what-technology-will-be-used-toopublish-your-data-service-offer"></a>Примите решение, какие технологии будут использоваться toopublish ваше предложение службы данных
Издатель может выбрать одну из нескольких технологий для публикации службы данных в Azure Marketplace. Hello основных технологий, поддерживаемых описано ниже. Независимо от того какая технология — hello используется toopublish службы данных, для конечных пользователей hello использует данные hello через hello **веб-канала OData** предоставляемых службой Azure Marketplace. Все сведения о службе OData можно найти на веб-сайте [http://www.odata.org/](http://www.odata.org/)

## <a name="sql-azure-database"></a>База данных SQL Azure
Издатель отвечает за размещение набора данных в SQL Azure. Вам потребуется toosubscribe tooAzure подготовить соответствующий размер базы данных и передача данных в базу данных SQL Azure. Издатель является также отвечает tookeep своевременных своих данных. Дополнительные сведения о подписке tooAzure служб можно найти на [https://azure.microsoft.com/services/sql-database/](https://azure.microsoft.com/services/sql-database/)

При перемещении данных hello в SQL Azure, можно предоставлять hello Azure Marketplace, таблиц и представлений. Hello Publisher можно указать, какие таблицы и представления и столбцы предоставляется toohello для конечных пользователей. Дальнейшие поставщика содержимого hello можно также указать столбцы, которые могут запрашиваться для конечных пользователей hello и какие из них возвращаются только в полезных данных hello. Это обеспечивает высокую гибкость, о которых следует предоставить данные в базе данных hello. Столбцы, которые могут запрашиваться должны toobe, основанным на один или несколько индексов базы данных.

## <a name="rest-based-web-service"></a>Веб-служба REST
Поддерживается протокол: **только HTTPS**

Существующие службы на основе REST может предоставляться через hello Azure Marketplace. Поскольку hello набор данных всегда конечного пользователя предоставляется toohello каналов OData, hello Azure Marketplace службы должен будет toomap toobe hello tooa службы OData на основе службы. toodo, поэтому конечные точки на основе REST hello tooexpose все параметры в качестве параметров HTTP.

полезные данные Hello должен toobe в форме, которая может быть отображен в отклик ATOM. Поэтому hello ответа от службы hello должен toobe в формате XML и может содержать только один повторяющийся элемент, содержащий значения hello полезных данных (например, набор записей). Hello службы Azure Marketplace сопоставит hello Повторяющаяся запись toohello каждого узла в значениях полезных данных ATOM и hello в свойство узлы внутри узла запись hello.

Сведения об авторизации (например, API ключа, проверки подлинности маркера, т. д.) должен toobe, предоставляемых в виде параметра HTTP или в заголовок HTTP hello (пара значений ключа) — Обычная проверка подлинности также поддерживается. Допустимый ключ должен toobe указано, и все запросы через Azure Marketplace выполняются через этот ключ. Пользователь, мониторинга и выставления счетов происходит на уровне hello Azure Marketplace.

Ошибки, возвращенный службой hello должны toobe сопоставляется коды состояния HTTP. В случае, если служба hello возвращает XML, который содержит ошибку hello они будут сопоставлены кодами hello Azure Marketplace службы tooHTTP состояния toobe.

## <a name="soap-based-web-services"></a>Веб-службы SOAP
Поддерживается протокол: **только HTTPS**

Hello требования являются hello же, как показано в разделе службы на основе REST hello. Hello единственное отличие заключается в том, что параметры также могут быть предоставлены в текст XML, передаются службе toohello издателя с каждым запросом, осуществленные через Azure Marketplace. Это означает, что пользователь hello параметры HTTP предоставляет во внешнем hello преобразуются в XML-элементы XML-документа, который отправляется hello запроса toohello поставщика содержимого веб-службе.

## <a name="odata-based-web-services"></a>Веб-службы OData
Поддерживается протокол: **только HTTPS**

Данные могут быть предоставлены как tooAzure службы OData Marketplace. система Hello toopass постоянной hello службы с помощью и заменяет hello корень службы hello корень службы Azure Marketplace hello — tooensure, все последующие вызовы проходить через Azure Marketplace.

Службы OData только нет необходимости toogo в базе данных в серверном hello. OData поддерживает любого типа хранилища или бизнес-логики toodrive hello службы.

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда проверки предварительных требований hello и выполнить необходимые задачи hello, можно переместить вперед с hello Создание ваше предложение службы данных, как описано в hello [руководство по публикации службы данных](marketplace-publishing-data-service-creation.md).

Или, если вы хотите tooreview hello в целом процесс и соответствующие статьи hello для каждого из этапов публикации hello, посетите hello статьи [Приступая к работе: как toopublish toohello предложение Azure Marketplace](marketplace-publishing-getting-started.md).

[link-acct]:marketplace-publishing-accounts-creation-registration.md
