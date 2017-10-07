---
title: "aaaManage tooresources разрешения для пользователя в Azure стека (администратор службы и клиента) | Документы Microsoft"
description: "Как администратор службы или клиента, узнайте, как toomanage RBAC разрешения."
services: azure-stack
documentationcenter: 
author: Heathl17
manager: byronr
editor: 
ms.assetid: cccac19a-e1bf-4e36-8ac8-2228e8487646
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 461feab12a4cb8b9402c6c61b721371c50f60559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control"></a><span data-ttu-id="419b3-103">Управление доступом на основе ролей</span><span class="sxs-lookup"><span data-stu-id="419b3-103">Manage Role-Based Access Control</span></span>
<span data-ttu-id="419b3-104">Пользователь в Azure Stack может быть читателем, владельцем или участником каждого экземпляра подписки, группы ресурсов или службы.</span><span class="sxs-lookup"><span data-stu-id="419b3-104">A user in Azure Stack can be a reader, owner, or contributor for each instance of a subscription, resource group, or service.</span></span> <span data-ttu-id="419b3-105">Например пользователь A может иметь разрешения чтения tooSubscription 1, но имеют разрешения владельца tooVirtual машины 7.</span><span class="sxs-lookup"><span data-stu-id="419b3-105">For example, User A might have reader permissions tooSubscription 1, but have owner permissions tooVirtual Machine 7.</span></span>

* <span data-ttu-id="419b3-106">Читатель: пользователь может все просматривать, но не может вносить изменения.</span><span class="sxs-lookup"><span data-stu-id="419b3-106">Reader: User can view everything, but can’t make any changes.</span></span>
* <span data-ttu-id="419b3-107">Участник: Пользователь может управлять все, кроме tooresources доступа.</span><span class="sxs-lookup"><span data-stu-id="419b3-107">Contributor: User can manage everything except access tooresources.</span></span>
* <span data-ttu-id="419b3-108">Владелец: Пользователь может управлять всем, включая tooresources доступа.</span><span class="sxs-lookup"><span data-stu-id="419b3-108">Owner: User can manage everything, including access tooresources.</span></span>

## <a name="set-access-permissions-for-a-user"></a><span data-ttu-id="419b3-109">Настройка прав доступа для пользователя</span><span class="sxs-lookup"><span data-stu-id="419b3-109">Set access permissions for a user</span></span>
1. <span data-ttu-id="419b3-110">Вход с учетной записью, для которого требуется toomanage toohello ресурс с разрешения владельца.</span><span class="sxs-lookup"><span data-stu-id="419b3-110">Sign in with an account that has owner permissions toohello resource you want toomanage.</span></span>
2. <span data-ttu-id="419b3-111">В колонке hello для ресурса hello щелкните hello **доступа** значок ![](media/azure-stack-manage-permissions/image1.png).</span><span class="sxs-lookup"><span data-stu-id="419b3-111">In hello blade for hello resource, click hello **Access** icon ![](media/azure-stack-manage-permissions/image1.png).</span></span>
3. <span data-ttu-id="419b3-112">В hello **пользователей** колонка, щелкните **ролей**.</span><span class="sxs-lookup"><span data-stu-id="419b3-112">In hello **Users** blade, click **Roles**.</span></span>
4. <span data-ttu-id="419b3-113">В hello **ролей** колонка, щелкните **добавить** tooadd разрешения для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="419b3-113">In hello **Roles** blade, click **Add** tooadd permissions for hello user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="419b3-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="419b3-114">Next steps</span></span>
[<span data-ttu-id="419b3-115">Добавление клиента Azure Stack</span><span class="sxs-lookup"><span data-stu-id="419b3-115">Add an Azure Stack tenant</span></span>](azure-stack-add-new-user-aad.md)

