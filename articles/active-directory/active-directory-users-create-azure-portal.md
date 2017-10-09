---
title: "aaaAdd tooAzure новых пользователей Active Directory | Документы Microsoft"
description: "Объясняет, как tooadd новых пользователей или изменение сведений о пользователе в Azure Active Directory."
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
ms.openlocfilehash: c4a156ea31b81202bb0d0ac224afbfc3f1785532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-tooazure-active-directory"></a><span data-ttu-id="087f4-103">Добавить новый tooAzure пользователей Active Directory</span><span class="sxs-lookup"><span data-stu-id="087f4-103">Add new users tooAzure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="087f4-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="087f4-104">Azure portal</span></span>](active-directory-users-create-azure-portal.md)
> * [<span data-ttu-id="087f4-105">классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="087f4-105">Azure classic portal</span></span>](active-directory-create-users.md)
>
>

<span data-ttu-id="087f4-106">В этой статье объясняется, как tooadd новых пользователей в вашей организации в hello Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="087f4-106">This article explains how tooadd new users in your organization in hello Azure Active Directory (Azure AD).</span></span> 

1. <span data-ttu-id="087f4-107">Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.</span><span class="sxs-lookup"><span data-stu-id="087f4-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="087f4-108">Выберите **дополнительные службы**, введите **пользователей и групп** в hello текстовое поле, а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="087f4-108">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Открытие пользователей и групп](./media/active-directory-users-create-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="087f4-110">На hello **пользователей и групп** колонки, выберите **всех пользователей**, а затем выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="087f4-110">On hello **Users and groups** blade, select **All users**, and then select **Add**.</span></span>

   ![При выборе команды Добавить hello](./media/active-directory-users-create-azure-portal/create-users-add-command.png)
4. <span data-ttu-id="087f4-112">Введите сведения для пользователя hello, таких как **имя** и **имя пользователя**.</span><span class="sxs-lookup"><span data-stu-id="087f4-112">Enter details for hello user, such as **Name** and **User name**.</span></span> <span data-ttu-id="087f4-113">Hello часть имени домена hello имя пользователя должно быть имя домена «foo.onmicrosoft.com» имени домена по умолчанию hello или имя проверенного домена без поддержки федерации, например «contoso.com».</span><span class="sxs-lookup"><span data-stu-id="087f4-113">hello domain name portion of hello user name must either be hello initial default domain name "foo.onmicrosoft.com" domain name, or a verified, non-federated domain name such as "contoso.com."</span></span>
5. <span data-ttu-id="087f4-114">Копирование или в противном случае Примечание hello создать пароль пользователя, таким образом, чтобы можно предоставить его toohello пользователя после завершения этого процесса.</span><span class="sxs-lookup"><span data-stu-id="087f4-114">Copy or otherwise note hello generated user password so that you can provide it toohello user after this process is complete.</span></span>
6. <span data-ttu-id="087f4-115">При необходимости можно открыть и заполните сведения hello в hello **профиль** колонки, hello **группы** колонке или hello **роли каталога** колонку для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="087f4-115">Optionally, you can open and fill out hello information in hello **Profile** blade, hello **Groups** blade, or hello **Directory role** blade for hello user.</span></span> <span data-ttu-id="087f4-116">Дополнительные сведения о ролях пользователей и администраторов см. в статье [Назначение ролей администратора в Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="087f4-116">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="087f4-117">На hello **пользователя** колонке выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="087f4-117">On hello **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="087f4-118">Безопасно распространите hello созданный пароль toohello нового пользователя, чтобы hello пользователь сможет войти в.</span><span class="sxs-lookup"><span data-stu-id="087f4-118">Securely distribute hello generated password toohello new user so that hello user can sign in.</span></span>

### <a name="next-steps"></a><span data-ttu-id="087f4-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="087f4-119">Next steps</span></span>
* [<span data-ttu-id="087f4-120">Добавление внешнего пользователя</span><span class="sxs-lookup"><span data-stu-id="087f4-120">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)
* [<span data-ttu-id="087f4-121">Сброс пароля пользователя в новый портал Azure hello</span><span class="sxs-lookup"><span data-stu-id="087f4-121">Reset a user's password in hello new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="087f4-122">Изменение сведений о работе пользователя</span><span class="sxs-lookup"><span data-stu-id="087f4-122">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="087f4-123">Управление профилями пользователей</span><span class="sxs-lookup"><span data-stu-id="087f4-123">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="087f4-124">Удаление пользователя из Azure AD</span><span class="sxs-lookup"><span data-stu-id="087f4-124">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
* [<span data-ttu-id="087f4-125">Назначьте роль tooa пользователя в Azure AD</span><span class="sxs-lookup"><span data-stu-id="087f4-125">Assign a user tooa role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)
