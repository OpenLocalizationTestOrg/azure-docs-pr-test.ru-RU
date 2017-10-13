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
ms.openlocfilehash: 41c9ee37c43d4ad41c51ea2ed023d3b47d460dd1
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="storage-accounts-in-azure-stack"></a><span data-ttu-id="61af6-103">Учетные записи хранения в Azure Stack</span><span class="sxs-lookup"><span data-stu-id="61af6-103">Storage accounts in Azure Stack</span></span>
<span data-ttu-id="61af6-104">Учетные записи хранения включают в себя службы BLOB-объектов и таблиц, а также уникальное пространство имен для объектов данных хранилища.</span><span class="sxs-lookup"><span data-stu-id="61af6-104">Storage accounts include Blob and Table services, and the unique namespace for your storage data objects.</span></span> <span data-ttu-id="61af6-105">По умолчанию данные в учетной записи доступны только владельцу учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="61af6-105">By default, the data in your account is available only to you, the storage account owner.</span></span>

1. <span data-ttu-id="61af6-106">На компьютере, подтверждения Концепции стек Azure, войдите на `https://adminportal.local.azurestack.external` как [администратора](azure-stack-connect-azure-stack.md)и нажмите кнопку **New** > **данные + хранилище**  >  **Учетной записи хранилища**.</span><span class="sxs-lookup"><span data-stu-id="61af6-106">On the Azure Stack POC computer, log in to `https://adminportal.local.azurestack.external` as [an admin](azure-stack-connect-azure-stack.md), and then click **New** > **Data + Storage** > **Storage account**.</span></span>

   ![](media/azure-stack-provision-storage-account/image01.png)
2. <span data-ttu-id="61af6-107">В **создать учетную запись хранения** колонки, введите имя для вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="61af6-107">In the **Create storage account** blade, type a name for your storage account.</span></span> <span data-ttu-id="61af6-108">Создайте новый **группы ресурсов**, или выберите существующую, а затем нажмите кнопку **создать** для создания учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="61af6-108">Create a new **Resource Group**, or select an existing one, then click **Create** to create the storage account.</span></span>

   ![](media/azure-stack-provision-storage-account/image02.png)
3. <span data-ttu-id="61af6-109">Чтобы просмотреть новую учетную запись хранения, щелкните **все ресурсы**, выполните поиск учетной записи хранения и щелкните ее имя.</span><span class="sxs-lookup"><span data-stu-id="61af6-109">To see your new storage account, click **All resources**, then search for the storage account and click its name.</span></span>

    ![](media/azure-stack-provision-storage-account/image03.png)

### <a name="next-steps"></a><span data-ttu-id="61af6-110">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="61af6-110">Next steps</span></span>
[<span data-ttu-id="61af6-111">Использование шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="61af6-111">Use Azure Resource Manager templates</span></span>](user/azure-stack-arm-templates.md)

[<span data-ttu-id="61af6-112">Дополнительные сведения об учетных записях хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="61af6-112">Learn about Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)

[<span data-ttu-id="61af6-113">Загрузить руководство проверки хранилища Azure согласованное стек Azure</span><span class="sxs-lookup"><span data-stu-id="61af6-113">Download the Azure Stack Azure-consistent Storage Validation Guide</span></span>](http://aka.ms/azurestacktp1doc)
