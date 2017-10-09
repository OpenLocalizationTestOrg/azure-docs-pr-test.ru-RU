---
title: "aaaCreate группу для пользователей в Azure Active Directory | Документы Microsoft"
description: "Как toocreate группы в Azure Active Directory и добавление членов группы toohello"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc583a7f02ce50e7f3b2c8f97a9c032a3e2dc33a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a><span data-ttu-id="9b2ce-103">Создание группы и добавление в нее пользователей в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9b2ce-103">Create a group and add members in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9b2ce-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="9b2ce-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="9b2ce-105">Классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="9b2ce-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="9b2ce-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b2ce-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="9b2ce-107">В этой статье объясняется, как toocreate и заполнить новую группу в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9b2ce-107">This article explains how toocreate and populate a new group in Azure Active Directory.</span></span> <span data-ttu-id="9b2ce-108">Используйте задачи управления tooperform группы, например назначение лицензии или разрешения tooa число пользователей или устройств одновременно.</span><span class="sxs-lookup"><span data-stu-id="9b2ce-108">Use a group tooperform management tasks such as assigning licenses or permissions tooa number of users or devices at once.</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="9b2ce-109">Как создать группу?</span><span class="sxs-lookup"><span data-stu-id="9b2ce-109">How do I create a group?</span></span>
1. <span data-ttu-id="9b2ce-110">Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.</span><span class="sxs-lookup"><span data-stu-id="9b2ce-110">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="9b2ce-111">Выберите **дополнительные службы**, введите **пользователей и групп** в hello текстовое поле, а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="9b2ce-111">Select **More services**, enter **User and groups** in hello text box, and then select **Enter**.</span></span>

   ![Открытие страницы "Управление пользователями"](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. <span data-ttu-id="9b2ce-113">На hello **пользователей и групп** колонке выберите **все группы**.</span><span class="sxs-lookup"><span data-stu-id="9b2ce-113">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Открытие hello групп колонку](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="9b2ce-115">На hello **пользователей и групп — все группы** колонки, выберите hello **добавить** команды.</span><span class="sxs-lookup"><span data-stu-id="9b2ce-115">On hello **Users and groups - All groups** blade, select hello **Add** command.</span></span>

   ![При выборе команды Добавить hello](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. <span data-ttu-id="9b2ce-117">На hello **группы** колонки, добавьте имя и описание группы hello.</span><span class="sxs-lookup"><span data-stu-id="9b2ce-117">On hello **Group** blade, add a name and description for hello group.</span></span>
6. <span data-ttu-id="9b2ce-118">tooselect элементы tooadd toohello группы выберите **назначено** в hello **тип регистрации членства** поле, а затем выберите **элементы**.</span><span class="sxs-lookup"><span data-stu-id="9b2ce-118">tooselect members tooadd toohello group, select **Assigned** in hello **Membership type** box, and then select **Members**.</span></span> <span data-ttu-id="9b2ce-119">Дополнительные сведения о как toomanage динамически hello членство в группе, в разделе [toocreate атрибуты с помощью расширенного правила для членства в группе](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9b2ce-119">For more information about how toomanage hello membership of a group dynamically, see [Using attributes toocreate advanced rules for group membership](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

   ![При выборе tooadd элементов](./media/active-directory-groups-create-azure-portal/select-members.png)
7. <span data-ttu-id="9b2ce-121">На hello **элементы** колонки, выберите один или несколько пользователей или устройств группы toohello tooadd и выберите hello **выберите** кнопку внизу hello hello колонке tooadd их toohello группы.</span><span class="sxs-lookup"><span data-stu-id="9b2ce-121">On hello **Members** blade, select one or more users or devices tooadd toohello group and select hello **Select** button at hello bottom of hello blade tooadd them toohello group.</span></span> <span data-ttu-id="9b2ce-122">Hello **пользователя** поле фильтры Здравствуйте, отображаемое на основе сопоставления вашей записи tooany часть имени пользователя или устройства.</span><span class="sxs-lookup"><span data-stu-id="9b2ce-122">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="9b2ce-123">Подстановочные знаки в поле не допускаются.</span><span class="sxs-lookup"><span data-stu-id="9b2ce-123">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="9b2ce-124">После добавления членов группы toohello выберите **создать** на hello **группы** колонку.</span><span class="sxs-lookup"><span data-stu-id="9b2ce-124">When you finish adding members toohello group, select **Create** on hello **Group** blade.</span></span>    

   ![Подтверждение создания группы](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a><span data-ttu-id="9b2ce-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9b2ce-126">Next steps</span></span>
<span data-ttu-id="9b2ce-127">В следующих статьях содержатся дополнительные сведения об Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9b2ce-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="9b2ce-128">Просмотр существующих групп</span><span class="sxs-lookup"><span data-stu-id="9b2ce-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="9b2ce-129">Управление параметрами группы</span><span class="sxs-lookup"><span data-stu-id="9b2ce-129">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="9b2ce-130">Управление участниками группы</span><span class="sxs-lookup"><span data-stu-id="9b2ce-130">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="9b2ce-131">Управление членством в группе</span><span class="sxs-lookup"><span data-stu-id="9b2ce-131">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="9b2ce-132">Управление динамическими правилами для пользователей в группе</span><span class="sxs-lookup"><span data-stu-id="9b2ce-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
