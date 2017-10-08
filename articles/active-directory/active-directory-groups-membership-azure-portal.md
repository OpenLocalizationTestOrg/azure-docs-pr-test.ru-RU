---
title: "группы hello aaaManage группе принадлежит tooin Azure Active Directory | Документы Microsoft"
description: "В Azure Active Directory группы могут содержать другие группы. Вот как toomanage членство в этих группах."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e785c2d0-7724-47d4-a56e-c58280c08a14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0a0a1967084de0968e1e802559f9cdfd7ca6ae4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-toowhich-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a><span data-ttu-id="871ca-104">Управление группами toowhich, который принадлежит группа в клиенте Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="871ca-104">Manage toowhich groups a group belongs in your Azure Active Directory tenant</span></span>
<span data-ttu-id="871ca-105">В Azure Active Directory группы могут содержать другие группы.</span><span class="sxs-lookup"><span data-stu-id="871ca-105">Groups can contain other groups in Azure Active Directory.</span></span> <span data-ttu-id="871ca-106">Вот как toomanage членство в этих группах.</span><span class="sxs-lookup"><span data-stu-id="871ca-106">Here's how toomanage those memberships.</span></span>

## <a name="how-do-i-find-hello-groups-my-group-is-a-member-of"></a><span data-ttu-id="871ca-107">Как найти hello Моя группа является членом группы?</span><span class="sxs-lookup"><span data-stu-id="871ca-107">How do I find hello groups my group is a member of?</span></span>
1. <span data-ttu-id="871ca-108">Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.</span><span class="sxs-lookup"><span data-stu-id="871ca-108">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="871ca-109">Выберите **дополнительные службы**, введите **пользователей и групп** в hello текстовое поле, а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="871ca-109">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Открытие страницы "Управление пользователями"](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. <span data-ttu-id="871ca-111">На hello **пользователей и групп** колонке выберите **все группы**.</span><span class="sxs-lookup"><span data-stu-id="871ca-111">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Открытие hello групп колонку](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="871ca-113">На hello **пользователей и групп — все группы** колонки, выберите группу.</span><span class="sxs-lookup"><span data-stu-id="871ca-113">On hello **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="871ca-114">На hello **группа — *groupname***  колонке выберите **членство в группе**.</span><span class="sxs-lookup"><span data-stu-id="871ca-114">On hello **Group - *groupname*** blade, select **Group memberships**.</span></span>

   ![Открытие hello группы членства колонку](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. <span data-ttu-id="871ca-116">tooadd вашей группы в качестве члена другой группы, на hello **групповой - членство в группе** колонки, выберите hello **добавить** команды.</span><span class="sxs-lookup"><span data-stu-id="871ca-116">tooadd your group as a member of another group, on hello **Group - Group memberships** blade, select hello **Add** command.</span></span>
7. <span data-ttu-id="871ca-117">Выберите группу из hello **Выбор группы** и, при необходимости выберите hello **выберите** кнопку в нижней части hello колонка hello.</span><span class="sxs-lookup"><span data-stu-id="871ca-117">Select a group from hello **Select Group** blade, and then select hello **Select** button at hello bottom of hello blade.</span></span> <span data-ttu-id="871ca-118">Одновременно можно добавить одну группу tooonly группы.</span><span class="sxs-lookup"><span data-stu-id="871ca-118">You can add your group tooonly one group at a time.</span></span> <span data-ttu-id="871ca-119">Hello **пользователя** поле фильтры Здравствуйте, отображаемое на основе сопоставления вашей записи tooany часть имени пользователя или устройства.</span><span class="sxs-lookup"><span data-stu-id="871ca-119">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="871ca-120">Подстановочные знаки в поле не допускаются.</span><span class="sxs-lookup"><span data-stu-id="871ca-120">No wildcard characters are accepted in that box.</span></span>

   ![Добавление членства в группе](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. <span data-ttu-id="871ca-122">tooremove вашей группы в качестве члена другой группы, на hello **групповой - членство в группе** колонки, выберите группу.</span><span class="sxs-lookup"><span data-stu-id="871ca-122">tooremove your group as a member of another group, on hello **Group - Group memberships** blade, select a group.</span></span>
9. <span data-ttu-id="871ca-123">На hello ***groupname*** колонки, выберите hello **удалить** команду и подтвердите перемещение в строке приветствия.</span><span class="sxs-lookup"><span data-stu-id="871ca-123">On hello ***groupname*** blade, select hello **Remove** command, and confirm your choice at hello prompt.</span></span>

   ![Команда "Удаление членства"](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. <span data-ttu-id="871ca-125">Завершив изменение членства группы в других группах, щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="871ca-125">When you finish changing group memberships for your group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="871ca-126">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="871ca-126">Additional information</span></span>
<span data-ttu-id="871ca-127">В следующих статьях содержатся дополнительные сведения об Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="871ca-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="871ca-128">Просмотр существующих групп</span><span class="sxs-lookup"><span data-stu-id="871ca-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="871ca-129">Создание группы и добавление участников</span><span class="sxs-lookup"><span data-stu-id="871ca-129">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="871ca-130">Управление параметрами группы</span><span class="sxs-lookup"><span data-stu-id="871ca-130">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="871ca-131">Управление участниками группы</span><span class="sxs-lookup"><span data-stu-id="871ca-131">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="871ca-132">Управление динамическими правилами для пользователей в группе</span><span class="sxs-lookup"><span data-stu-id="871ca-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
