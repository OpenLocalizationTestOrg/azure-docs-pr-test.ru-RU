---
title: "Управление группами, к которым относится ваша группа, в Azure Active Directory | Документы Майкрософт"
description: "В Azure Active Directory группы могут содержать другие группы. Вот как можно управлять членством такого типа."
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
ms.openlocfilehash: 08e04a6590176c4084ca47b4bd6cbb22500eca2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-to-which-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a><span data-ttu-id="c846d-104">Управление тем, к каким группам относится группа в клиенте Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c846d-104">Manage to which groups a group belongs in your Azure Active Directory tenant</span></span>
<span data-ttu-id="c846d-105">В Azure Active Directory группы могут содержать другие группы.</span><span class="sxs-lookup"><span data-stu-id="c846d-105">Groups can contain other groups in Azure Active Directory.</span></span> <span data-ttu-id="c846d-106">Вот как можно управлять членством такого типа.</span><span class="sxs-lookup"><span data-stu-id="c846d-106">Here's how to manage those memberships.</span></span>

## <a name="how-do-i-find-the-groups-my-group-is-a-member-of"></a><span data-ttu-id="c846d-107">Как можно узнать, участником каких групп является моя группа?</span><span class="sxs-lookup"><span data-stu-id="c846d-107">How do I find the groups my group is a member of?</span></span>
1. <span data-ttu-id="c846d-108">Войдите на [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога.</span><span class="sxs-lookup"><span data-stu-id="c846d-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="c846d-109">Выберите **Больше служб**, введите **Пользователи и группы** в текстовое поле, а затем нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="c846d-109">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Открытие страницы "Управление пользователями"](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. <span data-ttu-id="c846d-111">В колонке **Пользователи и группы** выберите **Все группы**.</span><span class="sxs-lookup"><span data-stu-id="c846d-111">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Открытие колонки группы](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="c846d-113">Выберите группу в колонке **Пользователи и группы — Все группы** .</span><span class="sxs-lookup"><span data-stu-id="c846d-113">On the **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="c846d-114">В колонке ***Группа —* имя_группы** выберите **Членства в группах**.</span><span class="sxs-lookup"><span data-stu-id="c846d-114">On the **Group - *groupname*** blade, select **Group memberships**.</span></span>

   ![Открытие колонки "Участие в группах"](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. <span data-ttu-id="c846d-116">Чтобы добавить группу в качестве участника в другую группу, в колонке **Группа — Членства в группах** выберите команду **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c846d-116">To add your group as a member of another group, on the **Group - Group memberships** blade, select the **Add** command.</span></span>
7. <span data-ttu-id="c846d-117">Выберите группу в колонке **Выбор группы** и нажмите кнопку **Выбрать**, расположенную в нижней части колонки.</span><span class="sxs-lookup"><span data-stu-id="c846d-117">Select a group from the **Select Group** blade, and then select the **Select** button at the bottom of the blade.</span></span> <span data-ttu-id="c846d-118">Одним действием группу можно добавить только в одну другую группу.</span><span class="sxs-lookup"><span data-stu-id="c846d-118">You can add your group to only one group at a time.</span></span> <span data-ttu-id="c846d-119">В поле **Пользователь** можно ввести часть имени пользователя или устройства, чтобы отфильтровать по нему список отображенных элементов.</span><span class="sxs-lookup"><span data-stu-id="c846d-119">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="c846d-120">Подстановочные знаки в поле не допускаются.</span><span class="sxs-lookup"><span data-stu-id="c846d-120">No wildcard characters are accepted in that box.</span></span>

   ![Добавление членства в группе](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. <span data-ttu-id="c846d-122">Чтобы удалить группу из другой группы, участником которой она является, в колонке **Группа — Принадлежность к группам** выберите удаляемую группу.</span><span class="sxs-lookup"><span data-stu-id="c846d-122">To remove your group as a member of another group, on the **Group - Group memberships** blade, select a group.</span></span>
9. <span data-ttu-id="c846d-123">В колонке ***имя_группы*** выберите команду **Удалить** и подтвердите свой выбор при появлении соответствующего запроса.</span><span class="sxs-lookup"><span data-stu-id="c846d-123">On the ***groupname*** blade, select the **Remove** command, and confirm your choice at the prompt.</span></span>

   ![Команда "Удаление членства"](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. <span data-ttu-id="c846d-125">Завершив изменение членства группы в других группах, щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c846d-125">When you finish changing group memberships for your group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="c846d-126">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="c846d-126">Additional information</span></span>
<span data-ttu-id="c846d-127">В следующих статьях содержатся дополнительные сведения об Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c846d-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="c846d-128">Просмотр существующих групп</span><span class="sxs-lookup"><span data-stu-id="c846d-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="c846d-129">Создание группы и добавление участников</span><span class="sxs-lookup"><span data-stu-id="c846d-129">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="c846d-130">Управление параметрами группы</span><span class="sxs-lookup"><span data-stu-id="c846d-130">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="c846d-131">Управление участниками группы</span><span class="sxs-lookup"><span data-stu-id="c846d-131">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="c846d-132">Управление динамическими правилами для пользователей в группе</span><span class="sxs-lookup"><span data-stu-id="c846d-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
