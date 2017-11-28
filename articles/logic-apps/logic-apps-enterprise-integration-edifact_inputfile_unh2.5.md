---
title: "aaaLogic приложения B2B декодировать edifact разрешить UNH2.5 - приложения логики Azure | Документы Microsoft"
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
ms.openlocfilehash: 6d85242d0f828fa52cdc9689938f3ba1e51b1183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toohandle-edifact-documents-having-unh25-segment"></a><span data-ttu-id="5a389-103">Как документы с UNH2.5 toohandle EDIFACT сегмент</span><span class="sxs-lookup"><span data-stu-id="5a389-103">How toohandle EDIFACT documents having UNH2.5 segment</span></span>
<span data-ttu-id="5a389-104">При наличии в документ EDIFACT hello UNH2.5 он используется для просмотра схемы.</span><span class="sxs-lookup"><span data-stu-id="5a389-104">When UNH2.5 is present in hello EDIFACT document, it is being used for schema lookup.</span></span> 

<span data-ttu-id="5a389-105">Пример: hello UNH поле является **EAN008** в сообщения EDIFACT hello</span><span class="sxs-lookup"><span data-stu-id="5a389-105">Example: hello UNH field is **EAN008** in hello EDIFACT message</span></span>  
<span data-ttu-id="5a389-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span><span class="sxs-lookup"><span data-stu-id="5a389-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span></span>  

<span data-ttu-id="5a389-107">Сообщение hello toohandle toofollow действия</span><span class="sxs-lookup"><span data-stu-id="5a389-107">Steps toofollow toohandle hello message</span></span> 
1. <span data-ttu-id="5a389-108">Обновление схемы hello</span><span class="sxs-lookup"><span data-stu-id="5a389-108">Update hello schema</span></span>
2. <span data-ttu-id="5a389-109">Проверьте параметры соглашения hello</span><span class="sxs-lookup"><span data-stu-id="5a389-109">Check hello agreement settings</span></span>  

## <a name="update-hello-schema"></a><span data-ttu-id="5a389-110">Обновление схемы hello</span><span class="sxs-lookup"><span data-stu-id="5a389-110">Update hello schema</span></span>
<span data-ttu-id="5a389-111">tooprocess приветственное сообщение, необходимо toodeploy схема с имя hello UNH2.5 корневого узла.</span><span class="sxs-lookup"><span data-stu-id="5a389-111">tooprocess hello message, you need toodeploy a schema with hello UNH2.5 root node name.</span></span>  <span data-ttu-id="5a389-112">Для данного примера, будет корневым именем схемы hello **EFACT_D03B_ORDERS_EAN008**</span><span class="sxs-lookup"><span data-stu-id="5a389-112">For given an example, hello schema root name would be **EFACT_D03B_ORDERS_EAN008**</span></span>  

<span data-ttu-id="5a389-113">Для каждого D03B_ORDERS с другой сегмент UNH2.5 потребовалось бы toodeploy отдельных схем.</span><span class="sxs-lookup"><span data-stu-id="5a389-113">For each D03B_ORDERS with a different UNH2.5 segment, you would have toodeploy an individual schema.</span></span>  

## <a name="add-schema-toohello-edifact-agreement"></a><span data-ttu-id="5a389-114">Добавить соглашения EDIFACT toohello схемы</span><span class="sxs-lookup"><span data-stu-id="5a389-114">Add schema toohello EDIFACT agreement</span></span>
### <a name="edifact-decode"></a><span data-ttu-id="5a389-115">Декодирование EDIFACT</span><span class="sxs-lookup"><span data-stu-id="5a389-115">EDIFACT Decode</span></span>
<span data-ttu-id="5a389-116">tooDecode Здравствуйте входящее сообщение, настроить схему hello в hello EDIFACT параметров получения соглашения</span><span class="sxs-lookup"><span data-stu-id="5a389-116">tooDecode hello incoming message, configure hello schema in hello EDIFACT agreement receive settings</span></span>
1. <span data-ttu-id="5a389-117">Добавление учетной записи интеграции toohello схемы hello</span><span class="sxs-lookup"><span data-stu-id="5a389-117">Add hello schema toohello integration account</span></span>    
2. <span data-ttu-id="5a389-118">Настройка схемы hello в hello EDIFACT параметров получения соглашения.</span><span class="sxs-lookup"><span data-stu-id="5a389-118">Configure hello schema in hello EDIFACT agreement receive settings.</span></span> 
3. <span data-ttu-id="5a389-119">Выберите соглашение EDIFACT и щелкните **Редактирование в качестве JSON**.</span><span class="sxs-lookup"><span data-stu-id="5a389-119">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="5a389-120">Добавить значение UNH2.5 в соглашении о получении hello **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5a389-120">Add UNH2.5 value in hello Receive Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span></span>

### <a name="edifact-encode"></a><span data-ttu-id="5a389-121">Кодирование EDIFACT</span><span class="sxs-lookup"><span data-stu-id="5a389-121">EDIFACT Encode</span></span>
<span data-ttu-id="5a389-122">tooEncode Здравствуйте входящее сообщение, настроить схему hello в параметры отправки соглашения EDIFACT hello</span><span class="sxs-lookup"><span data-stu-id="5a389-122">tooEncode hello incoming message, configure hello schema in hello EDIFACT agreement send settings</span></span>
1. <span data-ttu-id="5a389-123">Добавление учетной записи интеграции toohello схемы hello</span><span class="sxs-lookup"><span data-stu-id="5a389-123">Add hello schema toohello integration account</span></span>    
2. <span data-ttu-id="5a389-124">Настройка схемы hello в параметры отправки соглашения EDIFACT hello.</span><span class="sxs-lookup"><span data-stu-id="5a389-124">Configure hello schema in hello EDIFACT agreement send settings.</span></span> 
3. <span data-ttu-id="5a389-125">Выберите соглашение EDIFACT и щелкните **Редактирование в качестве JSON**.</span><span class="sxs-lookup"><span data-stu-id="5a389-125">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="5a389-126">Добавить значение UNH2.5 в hello соглашение отправки **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span><span class="sxs-lookup"><span data-stu-id="5a389-126">Add UNH2.5 value in hello Send Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a389-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5a389-127">Next Steps</span></span>
* [<span data-ttu-id="5a389-128">Дополнительные сведения о соглашениях учетных записей интеграции</span><span class="sxs-lookup"><span data-stu-id="5a389-128">Learn more about integration account agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Дополнительные сведения о корпоративных соглашениях интеграции")  