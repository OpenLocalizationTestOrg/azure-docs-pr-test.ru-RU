---
title: "истечение срока действия в Azure Active Directory группы aaaPreview Office 365 | Документы Microsoft"
description: "Сопоставление групп tooset копирование истечения срока действия для Office 365 в Azure Active Directory (Предварительная версия)"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro
ms.openlocfilehash: a8c99961cff3aad3f4d8b0cc1b2eb8e8a4c9ba95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a><span data-ttu-id="2cccc-103">Настройка срока действия групп Office 365 (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="2cccc-103">Configure Office 365 groups expiration (preview)</span></span>

<span data-ttu-id="2cccc-104">Теперь вы можете управлять жизненным циклом hello групп Office 365, задав истечение срока действия для выбранных групп Office 365.</span><span class="sxs-lookup"><span data-stu-id="2cccc-104">You can now manage hello lifecycle of Office 365 groups by setting expiration for any Office 365 groups that you select.</span></span> <span data-ttu-id="2cccc-105">После установки этот срок действия, владельцы этих групп — запрос toorenew их группы, если они по-прежнему требуются группы hello.</span><span class="sxs-lookup"><span data-stu-id="2cccc-105">Once this expiration is set, owners of those groups are asked toorenew their groups if they still need hello groups.</span></span> <span data-ttu-id="2cccc-106">Все группы Office 365, которые не будут обновлены, будут удалены.</span><span class="sxs-lookup"><span data-stu-id="2cccc-106">Any Office 365 group that is not renewed will be deleted.</span></span> <span data-ttu-id="2cccc-107">Любой группы Office 365, который был удален, можно восстановить в течение 30 дней владельцев группы hello или администратором hello.</span><span class="sxs-lookup"><span data-stu-id="2cccc-107">Any Office 365 group that was deleted can be restored within 30 days by hello group owners or hello administrator.</span></span>  


> [!NOTE]
> <span data-ttu-id="2cccc-108">Срок действия можно задать только для групп Office 365.</span><span class="sxs-lookup"><span data-stu-id="2cccc-108">You can set expiration for only Office 365 groups.</span></span>
>
> <span data-ttu-id="2cccc-109">Для этого требуется наличие лицензии Azure AD Premium:</span><span class="sxs-lookup"><span data-stu-id="2cccc-109">Setting expiration for O365 groups requires that an Azure AD Premium license is assigned to</span></span>
>   - <span data-ttu-id="2cccc-110">Здравствуйте, администратор, настраивающий параметры истечения срока действия hello для приветствия клиента</span><span class="sxs-lookup"><span data-stu-id="2cccc-110">hello administrator who configures hello expiration settings for hello tenant</span></span>
>   - <span data-ttu-id="2cccc-111">Все члены группы hello, выбранные для этого параметра</span><span class="sxs-lookup"><span data-stu-id="2cccc-111">All members of hello groups selected for this setting</span></span>

## <a name="set-office-365-groups-expiration"></a><span data-ttu-id="2cccc-112">Настройка срока действия групп Office 365</span><span class="sxs-lookup"><span data-stu-id="2cccc-112">Set Office 365 groups expiration</span></span>

1. <span data-ttu-id="2cccc-113">Откройте hello [Центр администрирования Azure AD](https://aad.portal.azure.com) с учетной записью, которая является глобальным администратором в клиенте Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2cccc-113">Open hello [Azure AD admin center](https://aad.portal.azure.com) with an account that is a global administrator in your Azure AD tenant.</span></span>

2. <span data-ttu-id="2cccc-114">Откройте страницу Azure AD и щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="2cccc-114">Open Azure AD, select **Users and groups**.</span></span>

3. <span data-ttu-id="2cccc-115">Выберите **параметры групповой** , а затем выберите **истечение срока действия** параметры истечения срока действия tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="2cccc-115">Select **Group settings** and then select **Expiration** tooopen hello expiration settings.</span></span>
  
  ![Колонка "Срок действия"](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. <span data-ttu-id="2cccc-117">На hello **истечение срока действия** колонку, вы можете:</span><span class="sxs-lookup"><span data-stu-id="2cccc-117">On hello **Expiration** blade, you can:</span></span>

  * <span data-ttu-id="2cccc-118">Задать время существования группы hello в днях.</span><span class="sxs-lookup"><span data-stu-id="2cccc-118">Set hello group lifetime in days.</span></span> <span data-ttu-id="2cccc-119">Можно выбрать один из hello предустановленный набор значений или пользовательское значение (должно быть 31 дня или больше).</span><span class="sxs-lookup"><span data-stu-id="2cccc-119">You could select one of hello preset values, or a custom value (should be 31 days or more).</span></span> 
  * <span data-ttu-id="2cccc-120">Укажите адрес электронной почты, где должны отправляться уведомления об окончания срока действия и обновления hello при группы не имеет владельца.</span><span class="sxs-lookup"><span data-stu-id="2cccc-120">Specify an email address where hello renewal and expiration notifications should be sent when a group has no owner.</span></span> 
  * <span data-ttu-id="2cccc-121">Выбрать, срок действия каких групп Office 365 может истечь.</span><span class="sxs-lookup"><span data-stu-id="2cccc-121">Select which Office 365 groups expire.</span></span> <span data-ttu-id="2cccc-122">Можно включить истечение срока действия для **все** группы Office 365, можно выбрать один из группы Office 365 hello, или выбрать **нет** отключение истечения срока действия для всех групп.</span><span class="sxs-lookup"><span data-stu-id="2cccc-122">You can enable expiration for **All** Office 365 groups, you can select from among hello Office 365 groups, or you select **None** to disable expiration for all groups.</span></span>
  * <span data-ttu-id="2cccc-123">По завершении сохраните параметры, нажав кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2cccc-123">Save your settings when you're done by selecting **Save**.</span></span>

<span data-ttu-id="2cccc-124">Инструкции hello как toodownload и установка срока действия tooconfigure модуль Microsoft PowerShell для группы Office 365 с помощью PowerShell см. в разделе [модуля Azure Active Directory V2 PowerShell - общедоступный выпуск предварительной версии 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span><span class="sxs-lookup"><span data-stu-id="2cccc-124">For instructions on how toodownload and install hello Microsoft PowerShell module tooconfigure expiration for Office 365 groups via PowerShell, see [Azure Active Directory V2 PowerShell Module - Public Preview Release 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span></span>

<span data-ttu-id="2cccc-125">Уведомления по электронной почте, подобные данному, отправляются владельцев группы Office 365 toohello 30 дней, 15 дней и 1 день предыдущего tooexpiration hello группы.</span><span class="sxs-lookup"><span data-stu-id="2cccc-125">Email notifications such as this one are sent toohello Office 365 group owners 30 days, 15 days, and 1 day prior tooexpiration of hello group.</span></span>

![Уведомление по электронной почте о истечении срока действия](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

<span data-ttu-id="2cccc-127">Владелец группы Hello можно выбрать **обновления группы** toorenew hello группы Office 365, или можно выбрать **Go toogroup** toosee hello элементы и другие сведения о hello группы.</span><span class="sxs-lookup"><span data-stu-id="2cccc-127">hello group owner can then select **Renew group** toorenew hello Office 365 group, or can select **Go toogroup** toosee hello members and other details about hello group.</span></span>

<span data-ttu-id="2cccc-128">По истечении срока действия группы hello группа удаляется один день после даты окончания срока действия hello.</span><span class="sxs-lookup"><span data-stu-id="2cccc-128">When a group expires, hello group is deleted one day after hello expiration date.</span></span> <span data-ttu-id="2cccc-129">Уведомление по электронной почте, подобные данному, отправляется владельцев группы toohello Office 365, уведомляющее их о hello истечение срока действия и последующего удаления группы Office 365.</span><span class="sxs-lookup"><span data-stu-id="2cccc-129">An email notification such as this one is sent toohello Office 365 group owners informing them about hello expiration and subsequent deletion of their Office 365 group.</span></span>

![Уведомление по электронной почте об удалении группы](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

<span data-ttu-id="2cccc-131">Hello группы можно восстановить, выбрав **восстановления группы** либо используя командлеты PowerShell, как описано в [Группа восстановление удаленных Office 365 в Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/ Active-Directory-Groups-RESTORE-Azure-Portal).</span><span class="sxs-lookup"><span data-stu-id="2cccc-131">hello group can be restored by selecting **Restore group** or by using PowerShell cmdlets, as described in [Restore a deleted Office 365 group in Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/active-directory-groups-restore-azure-portal).</span></span>
    
<span data-ttu-id="2cccc-132">Если hello группу, в которую производится восстановление содержит документы, сайтов SharePoint или другие постоянные объекты, он может занять too24 часы toofully восстановления hello группы и ее содержимое.</span><span class="sxs-lookup"><span data-stu-id="2cccc-132">If hello group you're restoring contains documents, SharePoint sites, or other persistent objects, it might take up too24 hours toofully restore hello group and its contents.</span></span>

> [!NOTE]
> * <span data-ttu-id="2cccc-133">При развертывании настройки срока окончания действия hello, возможно, некоторые группы, которые являются более старыми, чем период истечения срока действия hello.</span><span class="sxs-lookup"><span data-stu-id="2cccc-133">When deploying hello expiration settings, there might be some groups that are older than hello expiration window.</span></span> <span data-ttu-id="2cccc-134">Эти группы не будут удалены немедленно, но являются значение too30 дней до истечения срока действия.</span><span class="sxs-lookup"><span data-stu-id="2cccc-134">These groups are not be immediately deleted, but are set too30 days until expiration.</span></span> <span data-ttu-id="2cccc-135">Hello первого обновления уведомление по электронной почте отправляется в течение дня.</span><span class="sxs-lookup"><span data-stu-id="2cccc-135">hello first renewal notification email is sent out within a day.</span></span> <span data-ttu-id="2cccc-136">Например, группа A создан 400 дней назад, и задать срок действия hello too180 дней.</span><span class="sxs-lookup"><span data-stu-id="2cccc-136">For example, Group A was created 400 days ago, and hello expiration interval is set too180 days.</span></span> <span data-ttu-id="2cccc-137">При применении параметры истечения срока действия группы A имеет 30 дней, прежде чем он будет удален, если владельца hello обновляет его.</span><span class="sxs-lookup"><span data-stu-id="2cccc-137">When you apply expiration settings, Group A has 30 days before it is deleted, unless hello owner renews it.</span></span>
> * <span data-ttu-id="2cccc-138">Если это динамическая группа удаляется и восстановлены, он рассматривается как новую группу и повторно заполненная соответствующим toohello правило.</span><span class="sxs-lookup"><span data-stu-id="2cccc-138">When a dynamic group is deleted and restored, it is seen as a new group and re-populated according toohello rule.</span></span> <span data-ttu-id="2cccc-139">Этот процесс может занять too24 часов.</span><span class="sxs-lookup"><span data-stu-id="2cccc-139">This process might take up too24 hours.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2cccc-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2cccc-140">Next steps</span></span>
<span data-ttu-id="2cccc-141">В следующих статьях содержатся дополнительные сведения о группах Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2cccc-141">These articles provide additional information on Azure AD groups.</span></span>

* [<span data-ttu-id="2cccc-142">Просмотр существующих групп</span><span class="sxs-lookup"><span data-stu-id="2cccc-142">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="2cccc-143">Управление параметрами группы</span><span class="sxs-lookup"><span data-stu-id="2cccc-143">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="2cccc-144">Управление участниками группы</span><span class="sxs-lookup"><span data-stu-id="2cccc-144">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="2cccc-145">Управление членством в группе</span><span class="sxs-lookup"><span data-stu-id="2cccc-145">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="2cccc-146">Управление динамическими правилами для пользователей в группе</span><span class="sxs-lookup"><span data-stu-id="2cccc-146">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
