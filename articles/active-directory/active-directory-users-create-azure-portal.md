---
title: "Добавление новых пользователей в Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как добавлять новых пользователей или изменять сведения о них в Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand;jeffsta
ms.reviewer: jeffsta
ms.openlocfilehash: bfe0c556d94d50207a23d2e3984371fb602e9406
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="add-new-users-to-azure-active-directory"></a><span data-ttu-id="6cef9-103">Добавление новых пользователей в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6cef9-103">Add new users to Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6cef9-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="6cef9-104">Azure portal</span></span>](active-directory-users-create-azure-portal.md)
> * [<span data-ttu-id="6cef9-105">классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="6cef9-105">Azure classic portal</span></span>](active-directory-create-users.md)
>
>

<span data-ttu-id="6cef9-106">В этой статье объясняется, как добавить новых пользователей организации в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6cef9-106">This article explains how to add new users in your organization in the Azure Active Directory (Azure AD).</span></span> 

1. <span data-ttu-id="6cef9-107">Войдите на [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога.</span><span class="sxs-lookup"><span data-stu-id="6cef9-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="6cef9-108">Выберите **Больше служб**, введите **Пользователи и группы** в текстовое поле, а затем нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="6cef9-108">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Открытие пользователей и групп](./media/active-directory-users-create-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="6cef9-110">В колонке **Пользователи и группы** выберите **Все пользователи** и щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6cef9-110">On the **Users and groups** blade, select **All users**, and then select **Add**.</span></span>

   ![Выбор команды "Добавить"](./media/active-directory-users-create-azure-portal/create-users-add-command.png)
4. <span data-ttu-id="6cef9-112">Введите сведения о пользователе в соответствующих полях, например **Имя** и **Имя пользователя**.</span><span class="sxs-lookup"><span data-stu-id="6cef9-112">Enter details for the user, such as **Name** and **User name**.</span></span> <span data-ttu-id="6cef9-113">Частью имени имя пользователя, представляющей собой доменное имя, должно быть доменное имя по умолчанию, foo.onmicrosoft.com, или проверенное доменное имя, не являющееся федеративным, например contoso.com.</span><span class="sxs-lookup"><span data-stu-id="6cef9-113">The domain name portion of the user name must either be the initial default domain name "foo.onmicrosoft.com" domain name, or a verified, non-federated domain name such as "contoso.com."</span></span>
5. <span data-ttu-id="6cef9-114">Скопируйте или иным способом запишите созданный пароль пользователя, чтобы после завершения этого процесса его можно было предоставить пользователю.</span><span class="sxs-lookup"><span data-stu-id="6cef9-114">Copy or otherwise note the generated user password so that you can provide it to the user after this process is complete.</span></span>
6. <span data-ttu-id="6cef9-115">При необходимости можно заполнить сведения, открыв колонку **Профиль**, **Группы** или **Роль каталога** для пользователя.</span><span class="sxs-lookup"><span data-stu-id="6cef9-115">Optionally, you can open and fill out the information in the **Profile** blade, the **Groups** blade, or the **Directory role** blade for the user.</span></span> <span data-ttu-id="6cef9-116">Дополнительные сведения о ролях пользователей и администраторов см. в статье [Назначение ролей администратора в Azure Active Directory](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="6cef9-116">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="6cef9-117">В колонке **Пользователь** щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="6cef9-117">On the **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="6cef9-118">Безопасным способом передайте созданный пароль новому пользователю, чтобы он мог войти в систему.</span><span class="sxs-lookup"><span data-stu-id="6cef9-118">Securely distribute the generated password to the new user so that the user can sign in.</span></span>

### <a name="next-steps"></a><span data-ttu-id="6cef9-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6cef9-119">Next steps</span></span>
* [<span data-ttu-id="6cef9-120">Добавление внешнего пользователя</span><span class="sxs-lookup"><span data-stu-id="6cef9-120">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)
* [<span data-ttu-id="6cef9-121">Сброс пароля пользователя на новом портале Azure</span><span class="sxs-lookup"><span data-stu-id="6cef9-121">Reset a user's password in the new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="6cef9-122">Изменение сведений о работе пользователя</span><span class="sxs-lookup"><span data-stu-id="6cef9-122">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="6cef9-123">Управление профилями пользователей</span><span class="sxs-lookup"><span data-stu-id="6cef9-123">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="6cef9-124">Удаление пользователя из Azure AD</span><span class="sxs-lookup"><span data-stu-id="6cef9-124">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
* [<span data-ttu-id="6cef9-125">Назначение пользователей в предварительной версии Azure AD</span><span class="sxs-lookup"><span data-stu-id="6cef9-125">Assign a user to a role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)
