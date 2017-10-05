---
title: "Управление участниками группы в Azure Active Directory | Документы Майкрософт"
description: "Сведения о том, как добавлять или удалять пользователей и устройства, которые входят в группу в Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d399a97d-fd2a-4b2d-b73d-0975db83f41b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 044e88f95712e1cc5b5532f5492c78d711a8d858
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a><span data-ttu-id="0a45d-103">Управление участниками групп в клиенте Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a45d-103">Manage group membership for users in your Azure Active Directory tenant</span></span>
<span data-ttu-id="0a45d-104">В этой статье объясняется, как управлять участниками группы в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0a45d-104">This article explains how to manage the members for a group in Azure Active Directory (Azure AD).</span></span>

## <a name="how-do-i-find-the-members-and-manage-them"></a><span data-ttu-id="0a45d-105">Как можно найти участников и управлять ими?</span><span class="sxs-lookup"><span data-stu-id="0a45d-105">How do I find the members and manage them?</span></span>
1. <span data-ttu-id="0a45d-106">Войдите на [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога.</span><span class="sxs-lookup"><span data-stu-id="0a45d-106">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="0a45d-107">Выберите **Больше служб**, введите **Пользователи и группы** в текстовое поле, а затем нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="0a45d-107">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Открытие страницы "Управление пользователями"](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. <span data-ttu-id="0a45d-109">В колонке **Пользователи и группы** выберите **Все группы**.</span><span class="sxs-lookup"><span data-stu-id="0a45d-109">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Открытие колонки группы](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="0a45d-111">Выберите группу в колонке **Пользователи и группы — Все группы** .</span><span class="sxs-lookup"><span data-stu-id="0a45d-111">On the **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="0a45d-112">В колонке **Группа — *имя_группы*** выберите **Участники**.</span><span class="sxs-lookup"><span data-stu-id="0a45d-112">On the **Group - *groupname*** blade, select **Members**.</span></span>

   ![Открытие колонки "Участники"](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. <span data-ttu-id="0a45d-114">Чтобы добавить участников в группу, в колонке **Группа — Участники** щелкните **Добавить участников**.</span><span class="sxs-lookup"><span data-stu-id="0a45d-114">To add members to the group, on the **Group - Members** blade, select **Add Members**.</span></span>

   ![Команда "Добавить участников"](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. <span data-ttu-id="0a45d-116">В колонке **Участники** выберите одного или несколько пользователей или устройств для добавления в группу, а затем нажмите кнопку **Выбрать**, расположенную в нижней части колонки, чтобы добавить их в группу.</span><span class="sxs-lookup"><span data-stu-id="0a45d-116">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span></span> <span data-ttu-id="0a45d-117">В поле **Пользователь** можно ввести часть имени пользователя или устройства, чтобы отфильтровать по нему список отображенных элементов.</span><span class="sxs-lookup"><span data-stu-id="0a45d-117">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="0a45d-118">Подстановочные знаки в поле не допускаются.</span><span class="sxs-lookup"><span data-stu-id="0a45d-118">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="0a45d-119">Чтобы удалить участника из группы, выберите его в колонке **Группы — Участники** .</span><span class="sxs-lookup"><span data-stu-id="0a45d-119">To remove members from the group, on the **Group - Members** blade, select a member.</span></span>
9. <span data-ttu-id="0a45d-120">В колонке ***имя_участника*** выберите команду **Удалить** и подтвердите свой выбор при появлении соответствующего запроса.</span><span class="sxs-lookup"><span data-stu-id="0a45d-120">On the ***membername*** blade, select the **Remove** command, and confirm your choice at the prompt.</span></span>

   ![Команда "Удалить участников"](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. <span data-ttu-id="0a45d-122">Завершив изменение состава группы, щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0a45d-122">When you finish changing members for the group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="0a45d-123">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="0a45d-123">Additional information</span></span>
<span data-ttu-id="0a45d-124">В следующих статьях содержатся дополнительные сведения об Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0a45d-124">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="0a45d-125">Просмотр существующих групп</span><span class="sxs-lookup"><span data-stu-id="0a45d-125">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="0a45d-126">Создание группы и добавление участников</span><span class="sxs-lookup"><span data-stu-id="0a45d-126">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="0a45d-127">Управление параметрами группы</span><span class="sxs-lookup"><span data-stu-id="0a45d-127">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="0a45d-128">Управление членством в группе</span><span class="sxs-lookup"><span data-stu-id="0a45d-128">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="0a45d-129">Управление динамическими правилами для пользователей в группе</span><span class="sxs-lookup"><span data-stu-id="0a45d-129">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
