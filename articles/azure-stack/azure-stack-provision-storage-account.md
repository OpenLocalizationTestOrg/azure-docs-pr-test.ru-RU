---
title: "Учетные записи хранения в Azure стек | Документы Microsoft"
description: "Сведения о создании учетной записи хранилища Azure стека."
services: azure-stack
documentationcenter: 
author: vhorne
manager: byronr
editor: 
ms.assetid: e1152110-b756-4c1a-9fa2-73fe3ab0ad8e
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 3/1/2017
ms.author: victorh
ms.openlocfilehash: de32c0ce79e8357274cc19cd1ea4ec23b85b918f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="storage-accounts-in-azure-stack"></a>Учетные записи хранения в Azure Stack
Учетные записи хранения включают в себя службы BLOB-объектов и таблиц, а также уникальное пространство имен для объектов данных хранилища. По умолчанию данные в учетной записи доступны только владельцу учетной записи хранения.

1. На компьютере, подтверждения Концепции стек Azure, войдите на `https://adminportal.local.azurestack.external` как [администратора](azure-stack-connect-azure-stack.md)и нажмите кнопку **New** > **данные + хранилище**  >  **Учетной записи хранилища**.

   ![](media/azure-stack-provision-storage-account/image01.png)
2. В **создать учетную запись хранения** колонки, введите имя для вашей учетной записи. Создайте новый **группы ресурсов**, или выберите существующую, а затем нажмите кнопку **создать** для создания учетной записи хранилища.

   ![](media/azure-stack-provision-storage-account/image02.png)
3. Чтобы просмотреть новую учетную запись хранения, щелкните **все ресурсы**, выполните поиск учетной записи хранения и щелкните ее имя.

    ![](media/azure-stack-provision-storage-account/image03.png)

### <a name="next-steps"></a>Дальнейшие действия
[Использование шаблонов диспетчера ресурсов Azure](azure-stack-arm-templates.md)

[Дополнительные сведения об учетных записях хранилища Azure](../storage/common/storage-create-storage-account.md)

[Загрузить руководство проверки хранилища Azure согласованное стек Azure](http://aka.ms/azurestacktp1doc)
