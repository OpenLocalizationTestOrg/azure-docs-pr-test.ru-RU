---
title: "Декодирование EDIFACT с разрешением UNH2.5 для Logic Apps B2B в Azure Logic Apps | Документация Майкрософт"
description: "Декодирование EDIFACT с разрешением UNH2.5 для Azure Logic Apps B2B"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 62ad8183cc6e9f56255b2729a04ee7710d00a21a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-handle-edifact-documents-having-unh25-segment"></a><span data-ttu-id="ac234-103">Как обрабатывать документы EDIFACT при наличии сегмента UNH2.5</span><span class="sxs-lookup"><span data-stu-id="ac234-103">How to handle EDIFACT documents having UNH2.5 segment</span></span>
<span data-ttu-id="ac234-104">При наличии сегмента UNH2.5 в документе EDIFACT он используется для поиска схемы.</span><span class="sxs-lookup"><span data-stu-id="ac234-104">When UNH2.5 is present in the EDIFACT document, it is being used for schema lookup.</span></span> 

<span data-ttu-id="ac234-105">Например, поле UNH представляет **EAN008** в сообщении EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="ac234-105">Example: The UNH field is **EAN008** in the EDIFACT message</span></span>  
<span data-ttu-id="ac234-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span><span class="sxs-lookup"><span data-stu-id="ac234-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span></span>  

<span data-ttu-id="ac234-107">Чтобы обработать сообщение, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="ac234-107">Steps to follow to handle the message</span></span> 
1. <span data-ttu-id="ac234-108">Обновите схему.</span><span class="sxs-lookup"><span data-stu-id="ac234-108">Update the schema</span></span>
2. <span data-ttu-id="ac234-109">Проверьте параметры соглашения.</span><span class="sxs-lookup"><span data-stu-id="ac234-109">Check the agreement settings</span></span>  

## <a name="update-the-schema"></a><span data-ttu-id="ac234-110">Обновление схемы</span><span class="sxs-lookup"><span data-stu-id="ac234-110">Update the schema</span></span>
<span data-ttu-id="ac234-111">Чтобы обработать сообщение, вам необходимо развернуть схему с именем корневого узла UNH2.5.</span><span class="sxs-lookup"><span data-stu-id="ac234-111">To process the message, you need to deploy a schema with the UNH2.5 root node name.</span></span>  <span data-ttu-id="ac234-112">В этом примере корневое имя схемы будет выглядеть так: **EFACT_D03B_ORDERS_EAN008**</span><span class="sxs-lookup"><span data-stu-id="ac234-112">For given an example, the schema root name would be **EFACT_D03B_ORDERS_EAN008**</span></span>  

<span data-ttu-id="ac234-113">Для каждого D03B_ORDERS с разными сегментами UNH2.5 вам понадобится развернуть отдельную схему.</span><span class="sxs-lookup"><span data-stu-id="ac234-113">For each D03B_ORDERS with a different UNH2.5 segment, you would have to deploy an individual schema.</span></span>  

## <a name="add-schema-to-the-edifact-agreement"></a><span data-ttu-id="ac234-114">Добавление схемы в соглашение EDIFACT</span><span class="sxs-lookup"><span data-stu-id="ac234-114">Add schema to the EDIFACT agreement</span></span>
### <a name="edifact-decode"></a><span data-ttu-id="ac234-115">Декодирование EDIFACT</span><span class="sxs-lookup"><span data-stu-id="ac234-115">EDIFACT Decode</span></span>
<span data-ttu-id="ac234-116">Чтобы декодировать входящее сообщение, настройте схему в параметрах получения для соглашения EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="ac234-116">To Decode the incoming message, configure the schema in the EDIFACT agreement receive settings</span></span>
1. <span data-ttu-id="ac234-117">Добавьте схему в учетную запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="ac234-117">Add the schema to the integration account</span></span>    
2. <span data-ttu-id="ac234-118">Настройте схему в параметрах получения для соглашения EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="ac234-118">Configure the schema in the EDIFACT agreement receive settings.</span></span> 
3. <span data-ttu-id="ac234-119">Выберите соглашение EDIFACT и щелкните **Редактирование в качестве JSON**.</span><span class="sxs-lookup"><span data-stu-id="ac234-119">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="ac234-120">Добавьте значение UNH2.5 в **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png) для соглашения получения.</span><span class="sxs-lookup"><span data-stu-id="ac234-120">Add UNH2.5 value in the Receive Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span></span>

### <a name="edifact-encode"></a><span data-ttu-id="ac234-121">Кодирование EDIFACT</span><span class="sxs-lookup"><span data-stu-id="ac234-121">EDIFACT Encode</span></span>
<span data-ttu-id="ac234-122">Чтобы выполнить кодирование входящего сообщения, настройте схему в параметрах отправки для соглашения EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="ac234-122">To Encode the incoming message, configure the schema in the EDIFACT agreement send settings</span></span>
1. <span data-ttu-id="ac234-123">Добавьте схему в учетную запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="ac234-123">Add the schema to the integration account</span></span>    
2. <span data-ttu-id="ac234-124">Настройте схему в параметрах отправки для соглашения EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="ac234-124">Configure the schema in the EDIFACT agreement send settings.</span></span> 
3. <span data-ttu-id="ac234-125">Выберите соглашение EDIFACT и щелкните **Редактирование в качестве JSON**.</span><span class="sxs-lookup"><span data-stu-id="ac234-125">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="ac234-126">Добавьте значение UNH2.5 в **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png) для соглашения отправки.</span><span class="sxs-lookup"><span data-stu-id="ac234-126">Add UNH2.5 value in the Send Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac234-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ac234-127">Next Steps</span></span>
* [<span data-ttu-id="ac234-128">Дополнительные сведения о соглашениях учетных записей интеграции</span><span class="sxs-lookup"><span data-stu-id="ac234-128">Learn more about integration account agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Дополнительные сведения о корпоративных соглашениях интеграции")  