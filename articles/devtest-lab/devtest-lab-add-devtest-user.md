---
title: "Добавление владельцев и пользователей в Azure DevTest Labs | Документация Майкрософт"
description: "Сведения о добавлении владельцев и пользователей в Azure DevTest Labs с помощью портала Azure или PowerShell"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: d67fa257574d6cb4ad4b18521900374fb51da290
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a><span data-ttu-id="4c9e5-103">Добавление владельцев и пользователей в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4c9e5-103">Add owners and users in Azure DevTest Labs</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

<span data-ttu-id="4c9e5-104">Доступом к Azure DevTest Labs управляет [служба управления доступом на основе ролей Azure (RBAC)](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="4c9e5-104">Access in Azure DevTest Labs is controlled by [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span> <span data-ttu-id="4c9e5-105">RBAC позволяет распределить обязанности внутри команды c помощью *ролей* и предоставить пользователям доступ на уровне, который им необходим для выполнения поставленных задач.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-105">Using RBAC, you can segregate duties within your team into *roles* where you grant only the amount of access necessary to users to perform their jobs.</span></span> <span data-ttu-id="4c9e5-106">RBAC предусматривает такие три основные роли: *Владелец*, *Пользователь DevTest Labs* и *Участник*.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-106">Three of these RBAC roles are *Owner*, *DevTest Labs User*, and *Contributor*.</span></span> <span data-ttu-id="4c9e5-107">В этой статье вы узнаете, какие действия могут выполнять пользователи с каждой из трех основных ролей RBAC.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-107">In this article, you learn what actions can be performed in each of the three main RBAC roles.</span></span> <span data-ttu-id="4c9e5-108">Здесь также приведены сведения о том, как добавлять пользователей в лабораторию (с использованием портала или сценария PowerShell) и как добавлять пользователей на уровне подписки.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-108">From there, you learn how to add users to a lab - both via the portal and via a PowerShell script, and how to add users at the subscription level.</span></span>

## <a name="actions-that-can-be-performed-in-each-role"></a><span data-ttu-id="4c9e5-109">Действия, которые можно выполнять в каждой роли</span><span class="sxs-lookup"><span data-stu-id="4c9e5-109">Actions that can be performed in each role</span></span>
<span data-ttu-id="4c9e5-110">Пользователю можно назначить одну из трех основных ролей:</span><span class="sxs-lookup"><span data-stu-id="4c9e5-110">There are three main roles that you can assign a user:</span></span>

* <span data-ttu-id="4c9e5-111">Владелец</span><span class="sxs-lookup"><span data-stu-id="4c9e5-111">Owner</span></span>
* <span data-ttu-id="4c9e5-112">Пользователь DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4c9e5-112">DevTest Labs User</span></span>
* <span data-ttu-id="4c9e5-113">Участник</span><span class="sxs-lookup"><span data-stu-id="4c9e5-113">Contributor</span></span>

<span data-ttu-id="4c9e5-114">В следующей таблице представлены действия, которые могут выполнять пользователи с каждой из этих ролей.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-114">The following table illustrates the actions that can be performed by users in each of these roles:</span></span>

| <span data-ttu-id="4c9e5-115">**Действия, которые могут выполнять пользователи с этой ролью**</span><span class="sxs-lookup"><span data-stu-id="4c9e5-115">**Actions users in this role can perform**</span></span> | <span data-ttu-id="4c9e5-116">**Пользователь DevTest Labs**</span><span class="sxs-lookup"><span data-stu-id="4c9e5-116">**DevTest Labs User**</span></span> | <span data-ttu-id="4c9e5-117">**Владелец**</span><span class="sxs-lookup"><span data-stu-id="4c9e5-117">**Owner**</span></span> | <span data-ttu-id="4c9e5-118">**Участник**</span><span class="sxs-lookup"><span data-stu-id="4c9e5-118">**Contributor**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4c9e5-119">**Задачи лаборатории**</span><span class="sxs-lookup"><span data-stu-id="4c9e5-119">**Lab tasks**</span></span> | | | |
| <span data-ttu-id="4c9e5-120">Добавление пользователей в лабораторию</span><span class="sxs-lookup"><span data-stu-id="4c9e5-120">Add users to a lab</span></span> |<span data-ttu-id="4c9e5-121">Нет</span><span class="sxs-lookup"><span data-stu-id="4c9e5-121">No</span></span> |<span data-ttu-id="4c9e5-122">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-122">Yes</span></span> |<span data-ttu-id="4c9e5-123">Нет</span><span class="sxs-lookup"><span data-stu-id="4c9e5-123">No</span></span> |
| <span data-ttu-id="4c9e5-124">Обновление параметров стоимости</span><span class="sxs-lookup"><span data-stu-id="4c9e5-124">Update cost settings</span></span> |<span data-ttu-id="4c9e5-125">Нет</span><span class="sxs-lookup"><span data-stu-id="4c9e5-125">No</span></span> |<span data-ttu-id="4c9e5-126">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-126">Yes</span></span> |<span data-ttu-id="4c9e5-127">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-127">Yes</span></span> |
| <span data-ttu-id="4c9e5-128">**Базовые задачи виртуальных машин**</span><span class="sxs-lookup"><span data-stu-id="4c9e5-128">**VM base tasks**</span></span> | | | |
| <span data-ttu-id="4c9e5-129">Добавление и удаление пользовательских образов</span><span class="sxs-lookup"><span data-stu-id="4c9e5-129">Add and remove custom images</span></span> |<span data-ttu-id="4c9e5-130">Нет</span><span class="sxs-lookup"><span data-stu-id="4c9e5-130">No</span></span> |<span data-ttu-id="4c9e5-131">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-131">Yes</span></span> |<span data-ttu-id="4c9e5-132">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-132">Yes</span></span> |
| <span data-ttu-id="4c9e5-133">Добавление, обновление и удаление формул</span><span class="sxs-lookup"><span data-stu-id="4c9e5-133">Add, update, and delete formulas</span></span> |<span data-ttu-id="4c9e5-134">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-134">Yes</span></span> |<span data-ttu-id="4c9e5-135">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-135">Yes</span></span> |<span data-ttu-id="4c9e5-136">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-136">Yes</span></span> |
| <span data-ttu-id="4c9e5-137">Разрешенные образы Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="4c9e5-137">Whitelist Azure Marketplace images</span></span> |<span data-ttu-id="4c9e5-138">Нет</span><span class="sxs-lookup"><span data-stu-id="4c9e5-138">No</span></span> |<span data-ttu-id="4c9e5-139">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-139">Yes</span></span> |<span data-ttu-id="4c9e5-140">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-140">Yes</span></span> |
| <span data-ttu-id="4c9e5-141">**Задачи виртуальных машин**</span><span class="sxs-lookup"><span data-stu-id="4c9e5-141">**VM tasks**</span></span> | | | |
| <span data-ttu-id="4c9e5-142">Создание виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="4c9e5-142">Create VMs</span></span> |<span data-ttu-id="4c9e5-143">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-143">Yes</span></span> |<span data-ttu-id="4c9e5-144">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-144">Yes</span></span> |<span data-ttu-id="4c9e5-145">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-145">Yes</span></span> |
| <span data-ttu-id="4c9e5-146">Запуск, остановка и удаление виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="4c9e5-146">Start, stop, and delete VMs</span></span> |<span data-ttu-id="4c9e5-147">Только виртуальные машины, созданные пользователем</span><span class="sxs-lookup"><span data-stu-id="4c9e5-147">Only VMs created by the user</span></span> |<span data-ttu-id="4c9e5-148">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-148">Yes</span></span> |<span data-ttu-id="4c9e5-149">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-149">Yes</span></span> |
| <span data-ttu-id="4c9e5-150">Обновление политик виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="4c9e5-150">Update VM policies</span></span> |<span data-ttu-id="4c9e5-151">Нет</span><span class="sxs-lookup"><span data-stu-id="4c9e5-151">No</span></span> |<span data-ttu-id="4c9e5-152">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-152">Yes</span></span> |<span data-ttu-id="4c9e5-153">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-153">Yes</span></span> |
| <span data-ttu-id="4c9e5-154">Добавление и удаление дисков данных виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="4c9e5-154">Add/remove data disks to/from VMs</span></span> |<span data-ttu-id="4c9e5-155">Только виртуальные машины, созданные пользователем</span><span class="sxs-lookup"><span data-stu-id="4c9e5-155">Only VMs created by the user</span></span> |<span data-ttu-id="4c9e5-156">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-156">Yes</span></span> |<span data-ttu-id="4c9e5-157">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-157">Yes</span></span> |
| <span data-ttu-id="4c9e5-158">**Задачи артефактов**</span><span class="sxs-lookup"><span data-stu-id="4c9e5-158">**Artifact tasks**</span></span> | | | |
| <span data-ttu-id="4c9e5-159">Добавление и удаление репозиториев артефактов</span><span class="sxs-lookup"><span data-stu-id="4c9e5-159">Add and remove artifact repositories</span></span> |<span data-ttu-id="4c9e5-160">Нет</span><span class="sxs-lookup"><span data-stu-id="4c9e5-160">No</span></span> |<span data-ttu-id="4c9e5-161">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-161">Yes</span></span> |<span data-ttu-id="4c9e5-162">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-162">Yes</span></span> |
| <span data-ttu-id="4c9e5-163">Применение артефактов</span><span class="sxs-lookup"><span data-stu-id="4c9e5-163">Apply artifacts</span></span> |<span data-ttu-id="4c9e5-164">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-164">Yes</span></span> |<span data-ttu-id="4c9e5-165">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-165">Yes</span></span> |<span data-ttu-id="4c9e5-166">Да</span><span class="sxs-lookup"><span data-stu-id="4c9e5-166">Yes</span></span> |

> [!NOTE]
> <span data-ttu-id="4c9e5-167">Когда пользователь создает виртуальную машину, ему автоматически назначается роль **Владелец** для этой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-167">When a user creates a VM, that user is automatically assigned to the **Owner** role of the created VM.</span></span>
> 
> 

## <a name="add-an-owner-or-user-at-the-lab-level"></a><span data-ttu-id="4c9e5-168">Добавление владельца или пользователя на уровне лаборатории</span><span class="sxs-lookup"><span data-stu-id="4c9e5-168">Add an owner or user at the lab level</span></span>
<span data-ttu-id="4c9e5-169">Владельцев и пользователей можно добавлять на уровне лаборатории с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-169">Owners and users can be added at the lab level via the Azure portal.</span></span> <span data-ttu-id="4c9e5-170">Можно также добавить внешних пользователей с допустимой [учетной записью Майкрософт (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="4c9e5-170">This includes external users with a valid [Microsoft account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span>
<span data-ttu-id="4c9e5-171">Ниже описана процедура добавления владельца или пользователя в лабораторию в Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-171">The following steps guide you through the process of adding an owner or user to a lab in Azure DevTest Labs:</span></span>

1. <span data-ttu-id="4c9e5-172">Войдите на [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="4c9e5-172">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="4c9e5-173">Щелкните **Другие службы**, а затем выберите в списке **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-173">Select **More services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="4c9e5-174">Из списка лабораторий выберите нужную лабораторию.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-174">From the list of labs, select the desired lab.</span></span>
4. <span data-ttu-id="4c9e5-175">В колонке лаборатории выберите **Конфигурация**.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-175">On the lab's blade, select **Configuration**.</span></span> 
5. <span data-ttu-id="4c9e5-176">В колонке **Конфигурация** выберите **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-176">On the **Configuration** blade, select **Users**.</span></span>
6. <span data-ttu-id="4c9e5-177">Выберите **Добавить** в колонке **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-177">On the **Users** blade, select **+Add**.</span></span>
   
    ![Добавить пользователя](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. <span data-ttu-id="4c9e5-179">В колонке **Выбор роли** выберите необходимую роль.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-179">On the **Select a role** blade, select the desired role.</span></span> <span data-ttu-id="4c9e5-180">В разделе [Действия, которые можно выполнять в каждой роли](#actions-that-can-be-performed-in-each-role) перечислены различные действия, которые могут выполнять пользователи с ролью владельца, пользователя DevTest или участника.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-180">The section [Actions that can be performed in each role](#actions-that-can-be-performed-in-each-role) lists the various actions that can be performed by users in the Owner, DevTest User, and Contributor roles.</span></span>
8. <span data-ttu-id="4c9e5-181">В колонке **Добавление пользователей** введите адрес электронной почты или имя пользователя, которому нужно назначить роль.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-181">On the **Add users** blade, enter the email address or name of the user you want to add in the role you specified.</span></span> <span data-ttu-id="4c9e5-182">Если пользователь не найден, система выдаст соответствующее сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-182">If the user can't be found, an error message explains the issue.</span></span> <span data-ttu-id="4c9e5-183">Если пользователь найден, он появится в списке и будет выбран.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-183">If the user is found, that user is listed and selected.</span></span> 
9. <span data-ttu-id="4c9e5-184">Щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-184">Select **Select**.</span></span>
10. <span data-ttu-id="4c9e5-185">Нажмите кнопку **ОК**, чтобы закрыть колонку **Добавить доступ**.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-185">Select **OK** to close the **Add access** blade.</span></span>
11. <span data-ttu-id="4c9e5-186">Вернувшись в колонку **Пользователи** , вы увидите, что пользователь добавлен.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-186">When you return to the **Users** blade, the user has been added.</span></span>  

## <a name="add-an-external-user-to-a-lab-using-powershell"></a><span data-ttu-id="4c9e5-187">Добавление внешнего пользователя в лабораторию с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c9e5-187">Add an external user to a lab using PowerShell</span></span>
<span data-ttu-id="4c9e5-188">Помимо добавления пользователей на портале Azure, вы можете добавить внешнего пользователя в лабораторию с помощью сценария PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-188">In addition to adding users in the Azure portal, you can add an external user to your lab using a PowerShell script.</span></span> <span data-ttu-id="4c9e5-189">В следующем примере просто измените значения параметров под комментарием **Values to change** (Изменяемые значения).</span><span class="sxs-lookup"><span data-stu-id="4c9e5-189">In the following example, simply modify the parameter values under the **Values to change** comment.</span></span>
<span data-ttu-id="4c9e5-190">Вы можете узнать значения `subscriptionId`, `labResourceGroup` и `labName` в колонке лаборатории на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-190">You can retrieve the `subscriptionId`, `labResourceGroup`, and `labName` values from the lab blade in the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="4c9e5-191">В примере сценария предполагается, что указанный пользователь добавлен в Active Directory в качестве гостя. Если это не так, сценарий завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-191">The sample script assumes that the specified user has been added as a guest to the Active Directory, and will fail if that is not the case.</span></span> <span data-ttu-id="4c9e5-192">Чтобы добавить в лабораторию пользователя, которого нет в Active Directory, используйте для назначения роли пользователю портал Azure, как показано в разделе [Добавление владельца или пользователя на уровне лаборатории](#add-an-owner-or-user-at-the-lab-level).</span><span class="sxs-lookup"><span data-stu-id="4c9e5-192">To add a user not in the Active Directory to a lab, use the Azure portal to assign the user to a role as illustrated in the section, [Add an owner or user at the lab level](#add-an-owner-or-user-at-the-lab-level).</span></span>   
> 
> 

    # Add an external user in DevTest Labs user role to a lab
    # Ensure that guest users can be added to the Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values to change
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select the Azure subscription that contains the lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve the user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create the role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-the-subscription-level"></a><span data-ttu-id="4c9e5-193">Добавление владельца или пользователя на уровне подписки</span><span class="sxs-lookup"><span data-stu-id="4c9e5-193">Add an owner or user at the subscription level</span></span>
<span data-ttu-id="4c9e5-194">Разрешения Azure распространяются от родительской области к дочерней.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-194">Azure permissions are propagated from parent scope to child scope in Azure.</span></span> <span data-ttu-id="4c9e5-195">Таким образом, владельцы подписки Azure, содержащей лаборатории, автоматически являются владельцами этих лабораторий.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-195">Therefore, owners of an Azure subscription that contains labs are automatically owners of those labs.</span></span> <span data-ttu-id="4c9e5-196">Они также являются владельцами виртуальных машин и других ресурсов, созданных пользователями лаборатории и службой Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-196">They also own the VMs and other resources created by the lab's users, and the Azure DevTest Labs service.</span></span> 

<span data-ttu-id="4c9e5-197">Дополнительных владельцев можно добавлять через колонку лаборатории на [портале Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="4c9e5-197">You can add additional owners to a lab via the lab's blade in the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="4c9e5-198">Тем не менее область их администрирования будет более узкой, чем у владельцев подписки.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-198">However, the added owner's scope of administration is more narrow than the subscription owner's scope.</span></span> <span data-ttu-id="4c9e5-199">У них, к примеру, не будет полного доступа к некоторым ресурсам, которые создаются в подписке службой DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-199">For example, the added owners do not have full access to some of the resources that are created in the subscription by the DevTest Labs service.</span></span> 

<span data-ttu-id="4c9e5-200">Чтобы добавить владельца подписки Azure, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="4c9e5-200">To add an owner to an Azure subscription, follow these steps:</span></span>

1. <span data-ttu-id="4c9e5-201">Войдите на [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="4c9e5-201">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="4c9e5-202">Щелкните **Больше служб**, а затем в списке выберите **Подписки**.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-202">Select **More Services**, and then select **Subscriptions** from the list.</span></span>
3. <span data-ttu-id="4c9e5-203">Выберите нужную подписку.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-203">Select the desired subscription.</span></span>
4. <span data-ttu-id="4c9e5-204">Щелкните значок **Доступ** .</span><span class="sxs-lookup"><span data-stu-id="4c9e5-204">Select **Access** icon.</span></span> 
   
    ![Доступ к пользователям](./media/devtest-lab-add-devtest-user/access-users.png)
5. <span data-ttu-id="4c9e5-206">Выберите **Добавить** в колонке **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-206">On the **Users** blade, select **Add**.</span></span>
   
    ![Добавить пользователя](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. <span data-ttu-id="4c9e5-208">В колонке **Выберите роль** щелкните **Владелец**.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-208">On the **Select a role** blade, select **Owner**.</span></span>
7. <span data-ttu-id="4c9e5-209">В колонке **Добавление пользователей** введите адрес электронной почты или имя пользователя, которому нужно назначить роль владельца.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-209">On the **Add users** blade, enter the email address or name of the user you want to add as an owner.</span></span> <span data-ttu-id="4c9e5-210">Если пользователь не найден, система выдаст соответствующее сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-210">If the user can't be found, you get an error message explaining the issue.</span></span> <span data-ttu-id="4c9e5-211">Если пользователь найден, он появится в текстовом поле **Пользователи** .</span><span class="sxs-lookup"><span data-stu-id="4c9e5-211">If the user is found, that user is listed under the **User** text box.</span></span>
8. <span data-ttu-id="4c9e5-212">Выберите имя найденного пользователя.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-212">Select the located user name.</span></span>
9. <span data-ttu-id="4c9e5-213">Щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-213">Select **Select**.</span></span>
10. <span data-ttu-id="4c9e5-214">Нажмите кнопку **ОК**, чтобы закрыть колонку **Добавить доступ**.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-214">Select **OK** to close the **Add access** blade.</span></span>
11. <span data-ttu-id="4c9e5-215">Вернувшись в колонку **Пользователи** , вы увидите, что пользователь добавлен как владелец.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-215">When you return to the **Users** blade, the user has been added as an owner.</span></span> <span data-ttu-id="4c9e5-216">Теперь он является владельцем любых лабораторий, созданных в этой подписке, а значит может выполнять задачи пользователя.</span><span class="sxs-lookup"><span data-stu-id="4c9e5-216">This user is now an owner of any labs created under this subscription, and thus be able to perform owner tasks.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

