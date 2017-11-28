---
title: "aaaAssign пользователь tooadministrator роли в Azure Active Directory | Документы Microsoft"
description: "Объясняет, как toochange административных учетных данных пользователей в Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a1ca1a53-50d8-4bf0-ae8f-73fa1253e2d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.openlocfilehash: 8bb6711c2570843962fe075b6026542a4bca525f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-tooadministrator-roles-in-azure-active-directory"></a><span data-ttu-id="bc96c-103">Назначить пользователя роли tooadministrator в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bc96c-103">Assign a user tooadministrator roles in Azure Active Directory</span></span>
<span data-ttu-id="bc96c-104">В этой статье объясняется, как tooassign tooa пользователя с административной роли в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bc96c-104">This article explains how tooassign an administrative role tooa user in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="bc96c-105">Сведения о добавлении новых пользователей в организации см. в разделе [добавлять новых пользователей tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bc96c-105">For information about adding new users in your organization, see [Add new users tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="bc96c-106">Добавленные пользователи нет прав администратора по умолчанию, но можно назначить роли toothem в любое время.</span><span class="sxs-lookup"><span data-stu-id="bc96c-106">Added users don't have administrator permissions by default, but you can assign roles toothem at any time.</span></span>

## <a name="assign-a-role-tooa-user"></a><span data-ttu-id="bc96c-107">Назначить пользователя роли tooa</span><span class="sxs-lookup"><span data-stu-id="bc96c-107">Assign a role tooa user</span></span>
1. <span data-ttu-id="bc96c-108">Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.</span><span class="sxs-lookup"><span data-stu-id="bc96c-108">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="bc96c-109">Выберите **дополнительные службы**, введите **пользователей и групп** в hello текстовое поле, а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="bc96c-109">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Открытие страницы "Управление пользователями"](./media/active-directory-users-assign-role-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="bc96c-111">На hello **пользователей и групп** колонке выберите **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="bc96c-111">On hello **Users and groups** blade, select **All users**.</span></span>

   ![Открытие hello колонка "все пользователи"](./media/active-directory-users-assign-role-azure-portal/create-users-open-users-blade.png)
4. <span data-ttu-id="bc96c-113">На hello **пользователей и групп — все пользователи** колонке выберите пользователя из списка hello.</span><span class="sxs-lookup"><span data-stu-id="bc96c-113">On hello **Users and groups - All users** blade, select a user from hello list.</span></span>
5. <span data-ttu-id="bc96c-114">В колонке hello для выбранного пользователя hello, выберите **роли каталога**и затем назначить роль tooa hello пользователя из hello **роли каталога** списка.</span><span class="sxs-lookup"><span data-stu-id="bc96c-114">On hello blade for hello selected user, select **Directory role**, and then assign hello user tooa role from hello **Directory role** list.</span></span> <span data-ttu-id="bc96c-115">Дополнительные сведения о ролях пользователей и администраторов см. в статье [Назначение ролей администратора в Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="bc96c-115">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>

      ![Назначение роли пользователя tooa](./media/active-directory-users-assign-role-azure-portal/create-users-assign-role.png)
6. <span data-ttu-id="bc96c-117">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bc96c-117">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc96c-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bc96c-118">Next steps</span></span>
* [<span data-ttu-id="bc96c-119">Добавление пользователей</span><span class="sxs-lookup"><span data-stu-id="bc96c-119">Add a user</span></span>](active-directory-users-create-azure-portal.md)
* [<span data-ttu-id="bc96c-120">Сброс пароля пользователя в новый портал Azure hello</span><span class="sxs-lookup"><span data-stu-id="bc96c-120">Reset a user's password in hello new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="bc96c-121">Изменение сведений о работе пользователя</span><span class="sxs-lookup"><span data-stu-id="bc96c-121">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="bc96c-122">Управление профилями пользователей</span><span class="sxs-lookup"><span data-stu-id="bc96c-122">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="bc96c-123">Удаление пользователя из Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc96c-123">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
