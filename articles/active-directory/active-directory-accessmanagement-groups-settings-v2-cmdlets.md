---
title: "Примеры PowerShell для управления группами в Azure Active Directory | Документация Майкрософт"
description: "На этой странице представлены примеры командлетов PowerShell, которые помогут вам управлять группами в Azure Active Directory."
keywords: "Azure AD, Azure Active Directory, PowerShell, группы, управление группами"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7a5023dc-2727-4c25-8254-b531fc3244ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: rodejo
ms.openlocfilehash: a81820bc778c26f6e8051e2817ebd2b9c24b697a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a><span data-ttu-id="3c9e0-104">Командлеты Azure Active Directory версии 2 для управления группами</span><span class="sxs-lookup"><span data-stu-id="3c9e0-104">Azure Active Directory version 2 cmdlets for group management</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3c9e0-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="3c9e0-105">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="3c9e0-106">Классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="3c9e0-106">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="3c9e0-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c9e0-107">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="3c9e0-108">В этой статье приведены примеры управления группами в Azure Active Directory (Azure AD) с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3c9e0-108">This article contains examples of how to use PowerShell to manage your groups in Azure Active Directory (Azure AD).</span></span>  <span data-ttu-id="3c9e0-109">Кроме того, в ней содержатся сведения о том, как выполнить настройки модуля Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3c9e0-109">It also tells you how to get set up with the Azure AD PowerShell module.</span></span> <span data-ttu-id="3c9e0-110">Во-первых, необходимо [скачать модуль Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="3c9e0-110">First, you must [download the Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="installing-the-azure-ad-powershell-module"></a><span data-ttu-id="3c9e0-111">Установка модуля Azure AD PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c9e0-111">Installing the Azure AD PowerShell module</span></span>
<span data-ttu-id="3c9e0-112">Чтобы установить модуль Azure AD PowerShell, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="3c9e0-112">To install the Azure AD PowerShell module, use the following commands:</span></span>

    PS C:\Windows\system32> install-module azuread

<span data-ttu-id="3c9e0-113">Чтобы проверить, установлен ли модуль, воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="3c9e0-113">To verify that the module was installed, use the following command:</span></span>

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

<span data-ttu-id="3c9e0-114">Теперь можно начать использование командлетов в модуле.</span><span class="sxs-lookup"><span data-stu-id="3c9e0-114">Now you can start using the cmdlets in the module.</span></span> <span data-ttu-id="3c9e0-115">Полное описание командлетов в модуле Azure AD см. в электронной справочной документации по [PowerShell версии 2 для Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="3c9e0-115">For a full description of the cmdlets in the Azure AD module, please refer to the online reference documentation for [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="connecting-to-the-directory"></a><span data-ttu-id="3c9e0-116">Подключение к каталогу</span><span class="sxs-lookup"><span data-stu-id="3c9e0-116">Connecting to the directory</span></span>
<span data-ttu-id="3c9e0-117">Прежде чем приступить к управлению группами с помощью командлетов Azure AD PowerShell, необходимо подключить сеанс PowerShell к каталогу, которым вы хотите управлять.</span><span class="sxs-lookup"><span data-stu-id="3c9e0-117">Before you can start managing groups using Azure AD PowerShell cmdlets, you must connect your PowerShell session to the directory you want to manage.</span></span> <span data-ttu-id="3c9e0-118">Используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3c9e0-118">Use the following command:</span></span>

    PS C:\Windows\system32> Connect-AzureAD

<span data-ttu-id="3c9e0-119">Командлет запросит ввести учетные данные, которые вы хотите использовать для доступа к каталогу.</span><span class="sxs-lookup"><span data-stu-id="3c9e0-119">The cmdlet prompts you for the credentials you want to use to access your directory.</span></span> <span data-ttu-id="3c9e0-120">В этом примере для доступа к демонстрационному каталогу используется karen@drumkit.onmicrosoft.com .</span><span class="sxs-lookup"><span data-stu-id="3c9e0-120">In this example, we are using karen@drumkit.onmicrosoft.com to access the demonstration directory.</span></span> <span data-ttu-id="3c9e0-121">Командлет возвращает подтверждение, показывающее, что сеанс был успешно подключен к каталогу:</span><span class="sxs-lookup"><span data-stu-id="3c9e0-121">The cmdlet returns a confirmation to show the session was connected successfully to your directory:</span></span>

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

<span data-ttu-id="3c9e0-122">Теперь можно начать использование командлетов Azure AD для управления группами в каталоге.</span><span class="sxs-lookup"><span data-stu-id="3c9e0-122">Now you can start using the AzureAD cmdlets to manage groups in your directory.</span></span>

## <a name="retrieving-groups"></a><span data-ttu-id="3c9e0-123">Получение сведений о группах</span><span class="sxs-lookup"><span data-stu-id="3c9e0-123">Retrieving groups</span></span>
<span data-ttu-id="3c9e0-124">Для получения сведений о существующих группах из каталога можно воспользоваться командлетом Get-AzureADGroups.</span><span class="sxs-lookup"><span data-stu-id="3c9e0-124">To retrieve existing groups from your directory you can use the Get-AzureADGroups cmdlet.</span></span> <span data-ttu-id="3c9e0-125">Чтобы получить сведения о всех группах в каталоге, используйте командлет без параметров:</span><span class="sxs-lookup"><span data-stu-id="3c9e0-125">To retrieve all groups in the directory, use the cmdlet without parameters:</span></span>

    PS C:\Windows\system32> get-azureadgroup

<span data-ttu-id="3c9e0-126">Командлет возвращает сведения о всех группах в подключенном каталоге.</span><span class="sxs-lookup"><span data-stu-id="3c9e0-126">The cmdlet returns all groups in the connected directory.</span></span>

<span data-ttu-id="3c9e0-127">Для получения сведений о конкретной группе, для которой указывается идентификатор объекта, можно использовать параметр -objectID:</span><span class="sxs-lookup"><span data-stu-id="3c9e0-127">You can use the -objectID parameter to retrieve a specific group for which you specify the group’s objectID:</span></span>

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

<span data-ttu-id="3c9e0-128">Командлет возвращает сведения о группе, идентификатор objectID которой совпадает со значением введенного параметра:</span><span class="sxs-lookup"><span data-stu-id="3c9e0-128">The cmdlet now returns the group whose objectID matches the value of the parameter you entered:</span></span>

    DeletionTimeStamp            :
    ObjectId                     : e29bae11-4ac0-450c-bc37-6dae8f3da61b
    ObjectType                   : Group
    Description                  :
    DirSyncEnabled               :
    DisplayName                  : Pacific NW Support
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 9bb4139b-60a1-434a-8c0d-7c1f8eee2df9
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

<span data-ttu-id="3c9e0-129">Для поиска конкретной группы можно использовать параметр -filter.</span><span class="sxs-lookup"><span data-stu-id="3c9e0-129">You can search for a specific group using the -filter parameter.</span></span> <span data-ttu-id="3c9e0-130">Этот параметр принимает предложение фильтра ODATA и возвращает сведения о всех группах, соответствующих фильтру, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="3c9e0-130">This parameter takes an ODATA filter clause and returns all groups that match the filter, as in the following example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

> [!NOTE] 
> <span data-ttu-id="3c9e0-131">Командлеты AzureAD PowerShell используют стандарт запросов OData.</span><span class="sxs-lookup"><span data-stu-id="3c9e0-131">The AzureAD PowerShell cmdlets implement the OData query standard.</span></span> <span data-ttu-id="3c9e0-132">Дополнительные сведения см. в разделе **$filter** статьи [OData system query options using the OData endpoint](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter) (Параметры системных запросов OData с использованием конечной точки OData).</span><span class="sxs-lookup"><span data-stu-id="3c9e0-132">For more information, see **$filter** in [OData system query options using the OData endpoint](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span></span>

## <a name="creating-groups"></a><span data-ttu-id="3c9e0-133">Создание групп</span><span class="sxs-lookup"><span data-stu-id="3c9e0-133">Creating groups</span></span>
<span data-ttu-id="3c9e0-134">Чтобы создать новую группу в каталоге, используйте командлет New-AzureADGroup.</span><span class="sxs-lookup"><span data-stu-id="3c9e0-134">To create a new group in your directory, use the New-AzureADGroup cmdlet.</span></span> <span data-ttu-id="3c9e0-135">Этот командлет создает новую группу безопасности с именем Marketing:</span><span class="sxs-lookup"><span data-stu-id="3c9e0-135">This cmdlet creates a new security group called “Marketing":</span></span>

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a><span data-ttu-id="3c9e0-136">Обновление групп</span><span class="sxs-lookup"><span data-stu-id="3c9e0-136">Updating groups</span></span>
<span data-ttu-id="3c9e0-137">Чтобы обновить существующую группу, используйте командлет Set-AzureADGroup.</span><span class="sxs-lookup"><span data-stu-id="3c9e0-137">To update an existing group, use the Set-AzureADGroup cmdlet.</span></span> <span data-ttu-id="3c9e0-138">В этом примере изменяется свойство DisplayName группы Intune Administrators.</span><span class="sxs-lookup"><span data-stu-id="3c9e0-138">In this example, we’re changing the DisplayName property of the group “Intune Administrators.”</span></span> <span data-ttu-id="3c9e0-139">Сначала с помощью командлета Get-AzureADGroup мы находим группу и фильтруем, используя атрибут DisplayName:</span><span class="sxs-lookup"><span data-stu-id="3c9e0-139">First, we’re finding the group using the Get-AzureADGroup cmdlet and filter using the DisplayName attribute:</span></span>

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

<span data-ttu-id="3c9e0-140">Затем мы меняем свойство Description на новое значение — Intune Device Administrators:</span><span class="sxs-lookup"><span data-stu-id="3c9e0-140">Next, we’re changing the Description property to the new value “Intune Device Administrators”:</span></span>

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

<span data-ttu-id="3c9e0-141">Если теперь снова выполнить поиск группы, то мы увидим, что свойство Description обновилось и отражает новое значение:</span><span class="sxs-lookup"><span data-stu-id="3c9e0-141">Now if we find the group again, we see the Description property is updated to reflect the new value:</span></span>

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Device Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

## <a name="deleting-groups"></a><span data-ttu-id="3c9e0-142">Удаление групп</span><span class="sxs-lookup"><span data-stu-id="3c9e0-142">Deleting groups</span></span>
<span data-ttu-id="3c9e0-143">Для удаления групп из каталога используйте командлет Remove-AzureADGroup, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="3c9e0-143">To delete groups from your directory, use the Remove-AzureADGroup cmdlet as follows:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a><span data-ttu-id="3c9e0-144">Управление членами групп</span><span class="sxs-lookup"><span data-stu-id="3c9e0-144">Managing members of groups</span></span>
<span data-ttu-id="3c9e0-145">Для добавления в группу новых членов используйте командлет Add-AzureADGroupMember.</span><span class="sxs-lookup"><span data-stu-id="3c9e0-145">If you need to add new members to a group, use the Add-AzureADGroupMember cmdlet.</span></span> <span data-ttu-id="3c9e0-146">Эта команда добавляет члена в группу Intune Administrators, которую мы использовали в предыдущем примере:</span><span class="sxs-lookup"><span data-stu-id="3c9e0-146">This command adds a member to the Intune Administrators group we used in the previous example:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="3c9e0-147">Параметр -ObjectId — это идентификатор объекта группы, в которую требуется добавить члена, а -RefObjectId — это идентификатор объекта пользователя, которого требуется добавить в качестве члена группы.</span><span class="sxs-lookup"><span data-stu-id="3c9e0-147">The -ObjectId parameter is the ObjectID of the group to which we want to add a member, and the -RefObjectId is the ObjectID of the user we want to add as a member to the group.</span></span>

<span data-ttu-id="3c9e0-148">Чтобы получить сведения о существующих членах группы, используйте командлет Get-AzureADGroupMember, как показано в этом примере:</span><span class="sxs-lookup"><span data-stu-id="3c9e0-148">To get the existing members of a group, use the Get-AzureADGroupMember cmdlet, as in this example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

<span data-ttu-id="3c9e0-149">Чтобы удалить члена, ранее добавленного в группу, используйте командлет Remove-AzureADGroupMember, как показано здесь:</span><span class="sxs-lookup"><span data-stu-id="3c9e0-149">To remove the member we previously added to the group, use the Remove-AzureADGroupMember cmdlet, as is shown here:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="3c9e0-150">Чтобы проверить, является ли пользователь членом какой-либо группы, используйте командлет Select-AzureADGroupIdsUserIsMemberOf.</span><span class="sxs-lookup"><span data-stu-id="3c9e0-150">To verify the group membership(s) of a user, use the Select-AzureADGroupIdsUserIsMemberOf cmdlet.</span></span> <span data-ttu-id="3c9e0-151">В качестве параметров этот командлет принимает идентификатор объекта пользователя, для которого выполняется проверка членства в группах, и список групп, в которых проверяется членство.</span><span class="sxs-lookup"><span data-stu-id="3c9e0-151">This cmdlet takes as its parameters the ObjectId of the user for which to check the group memberships, and a list of groups for which to check the memberships.</span></span> <span data-ttu-id="3c9e0-152">Список групп необходимо указать в форме сложной переменной типа Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck, поэтому сначала необходимо создать переменную с этим типом:</span><span class="sxs-lookup"><span data-stu-id="3c9e0-152">The list of groups must be provided in the form of a complex variable of type “Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck”, so we first must create a variable with that type:</span></span>

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

<span data-ttu-id="3c9e0-153">Затем необходимо указать значения идентификаторов группы для регистрации атрибута GroupIds этой сложной переменной:</span><span class="sxs-lookup"><span data-stu-id="3c9e0-153">Next, we provide values for the groupIds to check in the attribute “GroupIds” of this complex variable:</span></span>

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

<span data-ttu-id="3c9e0-154">Теперь, если требуется проверить членство пользователя с идентификатором объекта 72cd4bbd-2594-40a2-935c-016f3cfeeeea в группах в $g, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3c9e0-154">Now, if we want to check the group memberships of a user with ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea against the groups in $g, we should use:</span></span>

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


<span data-ttu-id="3c9e0-155">Возвращаемое значение — это список групп, членом которых является данный пользователь.</span><span class="sxs-lookup"><span data-stu-id="3c9e0-155">The value returned is a list of groups of which this user is a member.</span></span> <span data-ttu-id="3c9e0-156">Этот метод также можно применять для проверки членства в контактах, группах или субъектах-службах для определенного списка групп. Для этого используйте командлеты Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf и Select-AzureADGroupIdsServicePrincipalIsMemberOf.</span><span class="sxs-lookup"><span data-stu-id="3c9e0-156">You can also apply this method to check Contacts, Groups or Service Principals membership for a given list of groups, using Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf or Select-AzureADGroupIdsServicePrincipalIsMemberOf</span></span>

## <a name="managing-owners-of-groups"></a><span data-ttu-id="3c9e0-157">Управление владельцами групп</span><span class="sxs-lookup"><span data-stu-id="3c9e0-157">Managing owners of groups</span></span>
<span data-ttu-id="3c9e0-158">Чтобы добавить в группу новых владельцев, воспользуйтесь командлетом Add-AzureADGroupOwner:</span><span class="sxs-lookup"><span data-stu-id="3c9e0-158">To add owners to a group, use the Add-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="3c9e0-159">Параметр -ObjectId — это идентификатор объекта группы, в которую требуется добавить владельца, а -RefObjectId — это идентификатор объекта пользователя, которого требуется добавить в качестве владельца группы.</span><span class="sxs-lookup"><span data-stu-id="3c9e0-159">The -ObjectId parameter is the ObjectID of the group to which we want to add an owner, and the -RefObjectId is the ObjectID of the user we want to add as an owner of the group.</span></span>

<span data-ttu-id="3c9e0-160">Для получения сведений о владельцах группы используйте командлет Get-AzureADGroupOwner:</span><span class="sxs-lookup"><span data-stu-id="3c9e0-160">To retrieve the owners of a group, use the Get-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

<span data-ttu-id="3c9e0-161">Командлет возвращает список владельцев для указанной группы:</span><span class="sxs-lookup"><span data-stu-id="3c9e0-161">The cmdlet returns the list of owners for the specified group:</span></span>

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

<span data-ttu-id="3c9e0-162">Для удаления владельца из группы используйте командлет Remove-AzureADGroupOwner:</span><span class="sxs-lookup"><span data-stu-id="3c9e0-162">If you want to remove an owner from a group, use the Remove-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a><span data-ttu-id="3c9e0-163">Зарезервированные псевдонимы</span><span class="sxs-lookup"><span data-stu-id="3c9e0-163">Reserved aliases</span></span> 
<span data-ttu-id="3c9e0-164">После создания группы определенные конечные точки позволяют пользователю указать mailNickname или псевдоним, который можно использовать как часть адреса электронной почты группы.</span><span class="sxs-lookup"><span data-stu-id="3c9e0-164">When a group is created, certain endpoints allow the end user to specify a mailNickname or alias to be used as part of the email address of the group.</span></span> <span data-ttu-id="3c9e0-165">Группы с приведенными ниже привилегированными псевдонимами электронной почты может создавать только глобальный администратор Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c9e0-165">Groups with the following highly privileged email aliases can only be created by an Azure AD global administrator.</span></span> 
  
* <span data-ttu-id="3c9e0-166">abuse</span><span class="sxs-lookup"><span data-stu-id="3c9e0-166">abuse</span></span> 
* <span data-ttu-id="3c9e0-167">admin</span><span class="sxs-lookup"><span data-stu-id="3c9e0-167">admin</span></span> 
* <span data-ttu-id="3c9e0-168">administrator</span><span class="sxs-lookup"><span data-stu-id="3c9e0-168">administrator</span></span> 
* <span data-ttu-id="3c9e0-169">hostmaster</span><span class="sxs-lookup"><span data-stu-id="3c9e0-169">hostmaster</span></span> 
* <span data-ttu-id="3c9e0-170">majordomo</span><span class="sxs-lookup"><span data-stu-id="3c9e0-170">majordomo</span></span> 
* <span data-ttu-id="3c9e0-171">postmaster</span><span class="sxs-lookup"><span data-stu-id="3c9e0-171">postmaster</span></span> 
* <span data-ttu-id="3c9e0-172">root</span><span class="sxs-lookup"><span data-stu-id="3c9e0-172">root</span></span> 
* <span data-ttu-id="3c9e0-173">secure</span><span class="sxs-lookup"><span data-stu-id="3c9e0-173">secure</span></span> 
* <span data-ttu-id="3c9e0-174">security</span><span class="sxs-lookup"><span data-stu-id="3c9e0-174">security</span></span> 
* <span data-ttu-id="3c9e0-175">ssl-admin</span><span class="sxs-lookup"><span data-stu-id="3c9e0-175">ssl-admin</span></span> 
* <span data-ttu-id="3c9e0-176">webmaster</span><span class="sxs-lookup"><span data-stu-id="3c9e0-176">webmaster</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3c9e0-177">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3c9e0-177">Next steps</span></span>
<span data-ttu-id="3c9e0-178">Дополнительную документацию по PowerShell Azure Active Directory см. в разделе [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0) (Командлеты Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="3c9e0-178">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

* [<span data-ttu-id="3c9e0-179">Управление доступом к ресурсам с помощью групп Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3c9e0-179">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="3c9e0-180">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3c9e0-180">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
