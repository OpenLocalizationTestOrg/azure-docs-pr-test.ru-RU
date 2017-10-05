---
title: "Назначение пользователю ролей администратора в Azure Active Directory | Документы Майкрософт"
description: "В данном разделе поясняется, как изменить административную информацию о пользователе в Azure Active Directory."
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
ms.openlocfilehash: bfadf133154488f9827cfbeaa98ddb0eb84b52f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="assign-a-user-to-administrator-roles-in-azure-active-directory"></a><span data-ttu-id="18060-103">Назначение пользователю ролей администратора в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="18060-103">Assign a user to administrator roles in Azure Active Directory</span></span>
<span data-ttu-id="18060-104">В этой статье описывается назначение роли администратора пользователю в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="18060-104">This article explains how to assign an administrative role to a user in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="18060-105">Сведения о добавлении новых пользователей в организации см. в статье [Добавление пользователей из других каталогов или организаций-партнеров в предварительной версии Azure Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="18060-105">For information about adding new users in your organization, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="18060-106">По умолчанию добавленные пользователи не имеют прав администратора, но вы можете назначать им роли в любое время.</span><span class="sxs-lookup"><span data-stu-id="18060-106">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span></span>

## <a name="assign-a-role-to-a-user"></a><span data-ttu-id="18060-107">Назначение роли пользователю</span><span class="sxs-lookup"><span data-stu-id="18060-107">Assign a role to a user</span></span>
1. <span data-ttu-id="18060-108">Войдите на [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога.</span><span class="sxs-lookup"><span data-stu-id="18060-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="18060-109">Выберите **Больше служб**, введите **Пользователи и группы** в текстовое поле, а затем нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="18060-109">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Открытие страницы "Управление пользователями"](./media/active-directory-users-assign-role-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="18060-111">В колонке **Пользователи и группы** выберите **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="18060-111">On the **Users and groups** blade, select **All users**.</span></span>

   ![Открытие колонки "Все пользователи"](./media/active-directory-users-assign-role-azure-portal/create-users-open-users-blade.png)
4. <span data-ttu-id="18060-113">В колонке **Пользователи и группы — Все пользователи** выберите пользователя из списка.</span><span class="sxs-lookup"><span data-stu-id="18060-113">On the **Users and groups - All users** blade, select a user from the list.</span></span>
5. <span data-ttu-id="18060-114">В колонке для выбранного пользователя щелкните **Роль каталога**, после чего назначьте пользователя для роли из списка **Роль каталога**.</span><span class="sxs-lookup"><span data-stu-id="18060-114">On the blade for the selected user, select **Directory role**, and then assign the user to a role from the **Directory role** list.</span></span> <span data-ttu-id="18060-115">Дополнительные сведения о ролях пользователей и администраторов см. в статье [Назначение ролей администратора в Azure Active Directory](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="18060-115">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>

      ![Назначение пользователя для роли](./media/active-directory-users-assign-role-azure-portal/create-users-assign-role.png)
6. <span data-ttu-id="18060-117">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="18060-117">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18060-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="18060-118">Next steps</span></span>
* [<span data-ttu-id="18060-119">Добавление пользователей</span><span class="sxs-lookup"><span data-stu-id="18060-119">Add a user</span></span>](active-directory-users-create-azure-portal.md)
* [<span data-ttu-id="18060-120">Сброс пароля пользователя на новом портале Azure</span><span class="sxs-lookup"><span data-stu-id="18060-120">Reset a user's password in the new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="18060-121">Изменение сведений о работе пользователя</span><span class="sxs-lookup"><span data-stu-id="18060-121">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="18060-122">Управление профилями пользователей</span><span class="sxs-lookup"><span data-stu-id="18060-122">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="18060-123">Удаление пользователя из Azure AD</span><span class="sxs-lookup"><span data-stu-id="18060-123">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
