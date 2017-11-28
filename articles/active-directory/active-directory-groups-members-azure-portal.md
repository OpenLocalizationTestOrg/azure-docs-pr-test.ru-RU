---
title: "aaaManage hello членов группы в Azure Active Directory | Документы Microsoft"
description: "Как tooadd или удаление пользователей и устройств из группы в Azure Active Directory"
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
ms.openlocfilehash: 4cb16ee63828003da251423a04736f7174dd4896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a><span data-ttu-id="87d02-103">Управление участниками групп в клиенте Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="87d02-103">Manage group membership for users in your Azure Active Directory tenant</span></span>
<span data-ttu-id="87d02-104">В этой статье объясняется, как toomanage hello членов группы в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="87d02-104">This article explains how toomanage hello members for a group in Azure Active Directory (Azure AD).</span></span>

## <a name="how-do-i-find-hello-members-and-manage-them"></a><span data-ttu-id="87d02-105">Как найти члены hello и управлять ими?</span><span class="sxs-lookup"><span data-stu-id="87d02-105">How do I find hello members and manage them?</span></span>
1. <span data-ttu-id="87d02-106">Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.</span><span class="sxs-lookup"><span data-stu-id="87d02-106">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="87d02-107">Выберите **дополнительные службы**, введите **пользователей и групп** в hello текстовое поле, а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="87d02-107">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Открытие страницы "Управление пользователями"](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. <span data-ttu-id="87d02-109">На hello **пользователей и групп** колонке выберите **все группы**.</span><span class="sxs-lookup"><span data-stu-id="87d02-109">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Открытие hello групп колонку](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="87d02-111">На hello **пользователей и групп — все группы** колонки, выберите группу.</span><span class="sxs-lookup"><span data-stu-id="87d02-111">On hello **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="87d02-112">На hello **группа — *groupname***  колонке выберите **элементы**.</span><span class="sxs-lookup"><span data-stu-id="87d02-112">On hello **Group - *groupname*** blade, select **Members**.</span></span>

   ![Открытие hello члены колонку](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. <span data-ttu-id="87d02-114">группы toohello элементы tooadd на hello **группы - члены** колонке выберите **добавить членов**.</span><span class="sxs-lookup"><span data-stu-id="87d02-114">tooadd members toohello group, on hello **Group - Members** blade, select **Add Members**.</span></span>

   ![Команда "Добавить участников"](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. <span data-ttu-id="87d02-116">На hello **элементы** колонки, выберите один или несколько пользователей или устройств группы toohello tooadd и выберите hello **выберите** кнопку внизу hello hello колонке tooadd их toohello группы.</span><span class="sxs-lookup"><span data-stu-id="87d02-116">On hello **Members** blade, select one or more users or devices tooadd toohello group and select hello **Select** button at hello bottom of hello blade tooadd them toohello group.</span></span> <span data-ttu-id="87d02-117">Hello **пользователя** поле фильтры Здравствуйте, отображаемое на основе сопоставления вашей записи tooany часть имени пользователя или устройства.</span><span class="sxs-lookup"><span data-stu-id="87d02-117">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="87d02-118">Подстановочные знаки в поле не допускаются.</span><span class="sxs-lookup"><span data-stu-id="87d02-118">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="87d02-119">tooremove членов из группы hello на hello **группы - члены** колонке выберите член.</span><span class="sxs-lookup"><span data-stu-id="87d02-119">tooremove members from hello group, on hello **Group - Members** blade, select a member.</span></span>
9. <span data-ttu-id="87d02-120">На hello ***membername*** колонки, выберите hello **удалить** команду и подтвердите перемещение в строке приветствия.</span><span class="sxs-lookup"><span data-stu-id="87d02-120">On hello ***membername*** blade, select hello **Remove** command, and confirm your choice at hello prompt.</span></span>

   ![Команда "Удалить участников"](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. <span data-ttu-id="87d02-122">Завершив изменение состава группы hello, выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="87d02-122">When you finish changing members for hello group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="87d02-123">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="87d02-123">Additional information</span></span>
<span data-ttu-id="87d02-124">В следующих статьях содержатся дополнительные сведения об Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="87d02-124">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="87d02-125">Просмотр существующих групп</span><span class="sxs-lookup"><span data-stu-id="87d02-125">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="87d02-126">Создание группы и добавление участников</span><span class="sxs-lookup"><span data-stu-id="87d02-126">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="87d02-127">Управление параметрами группы</span><span class="sxs-lookup"><span data-stu-id="87d02-127">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="87d02-128">Управление членством в группе</span><span class="sxs-lookup"><span data-stu-id="87d02-128">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="87d02-129">Управление динамическими правилами для пользователей в группе</span><span class="sxs-lookup"><span data-stu-id="87d02-129">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
