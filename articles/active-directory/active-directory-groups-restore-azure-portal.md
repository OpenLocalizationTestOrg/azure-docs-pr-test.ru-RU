---
title: "Группа aaaRestore удаленные Office 365 в Azure Active Directory | Документы Microsoft"
description: "Как toorestore удаленные из группы, Просмотр групп могут быть восстановлены и permamnently удаление группы в Azure Active Directory"
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
ms.date: 05/18/2017
ms.author: curtand
ms.openlocfilehash: 4e6650d64aa19f0c909f1c511f48681de8032f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a><span data-ttu-id="9c059-103">Восстановление удаленной группы Office 365 в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9c059-103">Restore a deleted Office 365 group in Azure Active Directory</span></span>

<span data-ttu-id="9c059-104">При удалении группы Office 365 в Azure Active Directory (Azure AD) hello, hello удалена группа зависимых, но не отображается в течение 30 дней от даты удаления hello.</span><span class="sxs-lookup"><span data-stu-id="9c059-104">When you delete an Office 365 group in hello Azure Active Directory (Azure AD), hello deleted group is retained but not visible for 30 days from hello deletion date.</span></span> <span data-ttu-id="9c059-105">Это, чтобы группа hello и его содержимое можно восстановить при необходимости.</span><span class="sxs-lookup"><span data-stu-id="9c059-105">This is so that hello group and its contents can be restored if needed.</span></span> <span data-ttu-id="9c059-106">Эта функциональность ограничен исключительно tooOffice 365 группы в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9c059-106">This functionality is restricted exclusively tooOffice 365 groups in Azure AD.</span></span> <span data-ttu-id="9c059-107">Она недоступна для групп безопасности или групп рассылки.</span><span class="sxs-lookup"><span data-stu-id="9c059-107">It is not available for security groups and distribution groups.</span></span>

> [!NOTE] 
> <span data-ttu-id="9c059-108">Не используйте `Remove-MsolGroup` поскольку очищает hello группы без возможности восстановления.</span><span class="sxs-lookup"><span data-stu-id="9c059-108">Don't use `Remove-MsolGroup` because it purges hello group permanently.</span></span> <span data-ttu-id="9c059-109">Всегда используйте `Remove-AzureADMSGroup` группы toodelete Office 365.</span><span class="sxs-lookup"><span data-stu-id="9c059-109">Always use `Remove-AzureADMSGroup` toodelete an O365 group.</span></span> 

<span data-ttu-id="9c059-110">требуемые разрешения Hello toorestore группы может быть любым из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="9c059-110">hello permissions required toorestore a group can be any of hello following:</span></span>

<span data-ttu-id="9c059-111">Роль</span><span class="sxs-lookup"><span data-stu-id="9c059-111">Role</span></span>  | <span data-ttu-id="9c059-112">Разрешения</span><span class="sxs-lookup"><span data-stu-id="9c059-112">Permissions</span></span> 
--------- | ---------
<span data-ttu-id="9c059-113">Администратор компании, партнер с поддержкой 2 уровня; администратор службы InTune</span><span class="sxs-lookup"><span data-stu-id="9c059-113">Company Administrator, Partner Tier2 support, and InTune Service Admins</span></span> | <span data-ttu-id="9c059-114">Восстановление любой удаленной группы Office 365</span><span class="sxs-lookup"><span data-stu-id="9c059-114">Can restore any deleted Office 365 group</span></span> 
<span data-ttu-id="9c059-115">Администратор учетных записей, партнер с поддержкой 1 уровня</span><span class="sxs-lookup"><span data-stu-id="9c059-115">User Account Administrator and Partner Tier1 support</span></span> | <span data-ttu-id="9c059-116">Можно восстановить в любой удаленной группы Office 365, за исключением этих назначенного toohello роли администратора компании</span><span class="sxs-lookup"><span data-stu-id="9c059-116">Can restore any deleted Office 365 group except those assigned toohello Company Administrator role</span></span> 
<span data-ttu-id="9c059-117">Пользователь</span><span class="sxs-lookup"><span data-stu-id="9c059-117">User</span></span> | <span data-ttu-id="9c059-118">Восстановление любой удаленной группы Office 365, которая принадлежала им</span><span class="sxs-lookup"><span data-stu-id="9c059-118">Can restore any deleted Office 365 group that they owned</span></span> 


## <a name="view-hello-deleted-office-365-groups-that-are-available-toorestore"></a><span data-ttu-id="9c059-119">Представление hello удалить группы Office 365, которые будут доступны toorestore</span><span class="sxs-lookup"><span data-stu-id="9c059-119">View hello deleted Office 365 groups that are available toorestore</span></span>
<span data-ttu-id="9c059-120">следующие командлеты Hello может быть tooverify группы удалены hello используется tooview, один hello или те, которые вы хотите быть не еще удалены без возможности восстановления.</span><span class="sxs-lookup"><span data-stu-id="9c059-120">hello following cmdlets can be used tooview hello deleted groups tooverify that hello one or ones you're interested in have not yet been permanently purged.</span></span> <span data-ttu-id="9c059-121">Эти командлеты являются частью hello [модуля Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="9c059-121">These cmdlets are part of hello [Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span> <span data-ttu-id="9c059-122">Дополнительные сведения об этом модуле можно найти в hello [Azure Active Directory PowerShell версии 2](/powershell/azure/install-adv2?view=azureadps-2.0) статьи.</span><span class="sxs-lookup"><span data-stu-id="9c059-122">More information about this module can be found in hello [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0) article.</span></span>

1.  <span data-ttu-id="9c059-123">Запустите следующий командлет toodisplay удалить группы Office 365 в клиенте, по-прежнему доступны toorestore hello.</span><span class="sxs-lookup"><span data-stu-id="9c059-123">Run hello following cmdlet toodisplay all deleted Office 365 groups in your tenant that are still available toorestore.</span></span>
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  <span data-ttu-id="9c059-124">Кроме того Если вы знаете objectID hello определенной группы (и его можно получить из командлета hello в шаге 1) выполнения hello, выполнив командлет tooverify, Здравствуйте, удаленные из определенной группы не еще был удален без возможности восстановления.</span><span class="sxs-lookup"><span data-stu-id="9c059-124">Alternately, if you know hello objectID of a specific group (and you can get it from hello cmdlet in step 1), run hello following cmdlet tooverify that hello specific deleted group has not yet been permanently purged.</span></span>
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-toorestore-your-deleted-office-365-group"></a><span data-ttu-id="9c059-125">Как toorestore удаленные группы Office 365</span><span class="sxs-lookup"><span data-stu-id="9c059-125">How toorestore your deleted Office 365 group</span></span>
<span data-ttu-id="9c059-126">После проверки того, что группы hello toorestore по-прежнему доступны, группа удалена hello восстановления с одним hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="9c059-126">Once you have verified that hello group is still available toorestore, restore hello deleted group with one of hello following steps.</span></span> <span data-ttu-id="9c059-127">Если группа hello содержит документы, SP сайты или другие постоянные объекты, он может занять too24 часы toofully восстановления группы и ее содержимое.</span><span class="sxs-lookup"><span data-stu-id="9c059-127">If hello group contains documents, SP sites, or other persistent objects, it might take up too24 hours toofully restore a group and its contents.</span></span>

1.  <span data-ttu-id="9c059-128">Выполнения hello следующие группы hello toorestore командлет и его содержимое.</span><span class="sxs-lookup"><span data-stu-id="9c059-128">Run hello following cmdlet toorestore hello group and its contents.</span></span>
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

<span data-ttu-id="9c059-129">Кроме того hello следующий командлет может выполняться toopermanently удалить hello удалить группу.</span><span class="sxs-lookup"><span data-stu-id="9c059-129">Alternatively, hello following cmdlet can be run toopermanently remove hello deleted group.</span></span>
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a><span data-ttu-id="9c059-130">Как убедиться, что действие выполнено?</span><span class="sxs-lookup"><span data-stu-id="9c059-130">How do you know this worked?</span></span>
<span data-ttu-id="9c059-131">успешно восстановленных группы Office 365, запустите hello tooverify `Get-AzureADGroup –ObjectId <objectId>` командлет toodisplay сведения о группе hello.</span><span class="sxs-lookup"><span data-stu-id="9c059-131">tooverify that you’ve successfully restored an Office 365 group, run hello `Get-AzureADGroup –ObjectId <objectId>` cmdlet toodisplay information about hello group.</span></span> <span data-ttu-id="9c059-132">После восстановления hello завершения запроса:</span><span class="sxs-lookup"><span data-stu-id="9c059-132">After hello restore request is completed:</span></span>
- <span data-ttu-id="9c059-133">Hello группа отображается в левой навигационной панели hello на сервере Exchange</span><span class="sxs-lookup"><span data-stu-id="9c059-133">hello group will appear in hello Left nav bar on Exchange</span></span>
- <span data-ttu-id="9c059-134">Планирование Hello hello группы будут отображаться в планировщик</span><span class="sxs-lookup"><span data-stu-id="9c059-134">hello plan for hello group will appear in Planner</span></span>
- <span data-ttu-id="9c059-135">Станут доступны все сайты Sharepoint и их содержимое.</span><span class="sxs-lookup"><span data-stu-id="9c059-135">Any Sharepoint sites and all of their contents will be available</span></span>
- <span data-ttu-id="9c059-136">Группа Hello может осуществляться из любого из конечных точек обмена hello и других рабочих нагрузок Office 365, поддерживающие группы Office 365</span><span class="sxs-lookup"><span data-stu-id="9c059-136">hello group can be accessed from any of hello Exchange endpoints and other Office 365 workloads that support Office 365 groups</span></span>


## <a name="next-steps"></a><span data-ttu-id="9c059-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9c059-137">Next steps</span></span>
<span data-ttu-id="9c059-138">В следующих статьях содержатся дополнительные сведения о группах Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9c059-138">These articles provide additional information on Azure Active Directory groups.</span></span>

* [<span data-ttu-id="9c059-139">Просмотр существующих групп</span><span class="sxs-lookup"><span data-stu-id="9c059-139">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="9c059-140">Управление параметрами группы</span><span class="sxs-lookup"><span data-stu-id="9c059-140">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="9c059-141">Управление участниками группы</span><span class="sxs-lookup"><span data-stu-id="9c059-141">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="9c059-142">Управление членством в группе</span><span class="sxs-lookup"><span data-stu-id="9c059-142">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="9c059-143">Управление динамическими правилами для пользователей в группе</span><span class="sxs-lookup"><span data-stu-id="9c059-143">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
