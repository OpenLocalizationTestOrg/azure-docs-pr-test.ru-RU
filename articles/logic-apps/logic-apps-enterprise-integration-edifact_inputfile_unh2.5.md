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
# <a name="how-toohandle-edifact-documents-having-unh25-segment"></a>Как документы с UNH2.5 toohandle EDIFACT сегмент
При наличии в документ EDIFACT hello UNH2.5 он используется для просмотра схемы. 

Пример: hello UNH поле является **EAN008** в сообщения EDIFACT hello  
UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'  

Сообщение hello toohandle toofollow действия 
1. Обновление схемы hello
2. Проверьте параметры соглашения hello  

## <a name="update-hello-schema"></a>Обновление схемы hello
tooprocess приветственное сообщение, необходимо toodeploy схема с имя hello UNH2.5 корневого узла.  Для данного примера, будет корневым именем схемы hello **EFACT_D03B_ORDERS_EAN008**  

Для каждого D03B_ORDERS с другой сегмент UNH2.5 потребовалось бы toodeploy отдельных схем.  

## <a name="add-schema-toohello-edifact-agreement"></a>Добавить соглашения EDIFACT toohello схемы
### <a name="edifact-decode"></a>Декодирование EDIFACT
tooDecode Здравствуйте входящее сообщение, настроить схему hello в hello EDIFACT параметров получения соглашения
1. Добавление учетной записи интеграции toohello схемы hello    
2. Настройка схемы hello в hello EDIFACT параметров получения соглашения. 
3. Выберите соглашение EDIFACT и щелкните **Редактирование в качестве JSON**.  Добавить значение UNH2.5 в соглашении о получении hello **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)

### <a name="edifact-encode"></a>Кодирование EDIFACT
tooEncode Здравствуйте входящее сообщение, настроить схему hello в параметры отправки соглашения EDIFACT hello
1. Добавление учетной записи интеграции toohello схемы hello    
2. Настройка схемы hello в параметры отправки соглашения EDIFACT hello. 
3. Выберите соглашение EDIFACT и щелкните **Редактирование в качестве JSON**.  Добавить значение UNH2.5 в hello соглашение отправки **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)

## <a name="next-steps"></a>Дальнейшие действия
* [Дополнительные сведения о соглашениях учетных записей интеграции](../logic-apps/logic-apps-enterprise-integration-agreements.md "Дополнительные сведения о корпоративных соглашениях интеграции")  