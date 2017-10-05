---
title: "Управление разрешениями к ресурсам на пользователя в Azure стека (администратор службы и клиента) | Документы Microsoft"
description: "Администратор службы или клиента Узнайте, как для управления разрешениями RBAC."
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
ms.openlocfilehash: 95bdc83351acdec352620feaea3b1e50c0dabad4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="manage-role-based-access-control"></a><span data-ttu-id="d1002-103">Управление доступом на основе ролей</span><span class="sxs-lookup"><span data-stu-id="d1002-103">Manage Role-Based Access Control</span></span>
<span data-ttu-id="d1002-104">Пользователь в Azure Stack может быть читателем, владельцем или участником каждого экземпляра подписки, группы ресурсов или службы.</span><span class="sxs-lookup"><span data-stu-id="d1002-104">A user in Azure Stack can be a reader, owner, or contributor for each instance of a subscription, resource group, or service.</span></span> <span data-ttu-id="d1002-105">Например, пользователь A может иметь разрешения на чтение подписки 1, но иметь права владельца виртуальной машины 7.</span><span class="sxs-lookup"><span data-stu-id="d1002-105">For example, User A might have reader permissions to Subscription 1, but have owner permissions to Virtual Machine 7.</span></span>

* <span data-ttu-id="d1002-106">Читатель: пользователь может все просматривать, но не может вносить изменения.</span><span class="sxs-lookup"><span data-stu-id="d1002-106">Reader: User can view everything, but can’t make any changes.</span></span>
* <span data-ttu-id="d1002-107">Участник: пользователь может управлять всем, кроме доступа к ресурсам.</span><span class="sxs-lookup"><span data-stu-id="d1002-107">Contributor: User can manage everything except access to resources.</span></span>
* <span data-ttu-id="d1002-108">Владелец: пользователь может управлять всем, включая доступ к ресурсам.</span><span class="sxs-lookup"><span data-stu-id="d1002-108">Owner: User can manage everything, including access to resources.</span></span>

## <a name="set-access-permissions-for-a-user"></a><span data-ttu-id="d1002-109">Настройка прав доступа для пользователя</span><span class="sxs-lookup"><span data-stu-id="d1002-109">Set access permissions for a user</span></span>
1. <span data-ttu-id="d1002-110">Выполните вход с помощью с учетной записью с разрешениями владельца ресурса, которым вы хотите управлять.</span><span class="sxs-lookup"><span data-stu-id="d1002-110">Sign in with an account that has owner permissions to the resource you want to manage.</span></span>
2. <span data-ttu-id="d1002-111">В колонке для ресурса, нажмите кнопку **доступа** значок ![](media/azure-stack-manage-permissions/image1.png).</span><span class="sxs-lookup"><span data-stu-id="d1002-111">In the blade for the resource, click the **Access** icon ![](media/azure-stack-manage-permissions/image1.png).</span></span>
3. <span data-ttu-id="d1002-112">В **пользователей** колонка, щелкните **ролей**.</span><span class="sxs-lookup"><span data-stu-id="d1002-112">In the **Users** blade, click **Roles**.</span></span>
4. <span data-ttu-id="d1002-113">В **ролей** колонка, щелкните **добавить** для добавления разрешений для пользователя.</span><span class="sxs-lookup"><span data-stu-id="d1002-113">In the **Roles** blade, click **Add** to add permissions for the user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1002-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d1002-114">Next steps</span></span>
[<span data-ttu-id="d1002-115">Добавление клиента Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d1002-115">Add an Azure Stack tenant</span></span>](azure-stack-add-new-user-aad.md)

