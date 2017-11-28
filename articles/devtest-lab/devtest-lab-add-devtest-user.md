---
title: "aaaAdd владельцы и пользователи в Azure DevTest Labs | Документы Microsoft"
description: "Добавьте в DevTest Labs Azure с помощью портала Azure hello или PowerShell владельцы и пользователи"
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
ms.openlocfilehash: 2a98f5fe1efbd7c23e0d97f58f47c37462aed3b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a><span data-ttu-id="2d3f8-103">Добавление владельцев и пользователей в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="2d3f8-103">Add owners and users in Azure DevTest Labs</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

<span data-ttu-id="2d3f8-104">Доступом к Azure DevTest Labs управляет [служба управления доступом на основе ролей Azure (RBAC)](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="2d3f8-104">Access in Azure DevTest Labs is controlled by [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span> <span data-ttu-id="2d3f8-105">С помощью RBAC, можно разделить обязанностей в рамках команды в *ролей* которой предоставлять только hello объем tooperform toousers необходимости доступа к своей работы.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-105">Using RBAC, you can segregate duties within your team into *roles* where you grant only hello amount of access necessary toousers tooperform their jobs.</span></span> <span data-ttu-id="2d3f8-106">RBAC предусматривает такие три основные роли: *Владелец*, *Пользователь DevTest Labs* и *Участник*.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-106">Three of these RBAC roles are *Owner*, *DevTest Labs User*, and *Contributor*.</span></span> <span data-ttu-id="2d3f8-107">В этой статье вы узнаете, какие действия могут выполняться в каждом из трех основных ролей RBAC hello.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-107">In this article, you learn what actions can be performed in each of hello three main RBAC roles.</span></span> <span data-ttu-id="2d3f8-108">После этого вы узнаете, как лаборатории tooa пользователей tooadd - оба через hello портала и через сценарий PowerShell и каким образом пользователи tooadd на hello уровня подписки.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-108">From there, you learn how tooadd users tooa lab - both via hello portal and via a PowerShell script, and how tooadd users at hello subscription level.</span></span>

## <a name="actions-that-can-be-performed-in-each-role"></a><span data-ttu-id="2d3f8-109">Действия, которые можно выполнять в каждой роли</span><span class="sxs-lookup"><span data-stu-id="2d3f8-109">Actions that can be performed in each role</span></span>
<span data-ttu-id="2d3f8-110">Пользователю можно назначить одну из трех основных ролей:</span><span class="sxs-lookup"><span data-stu-id="2d3f8-110">There are three main roles that you can assign a user:</span></span>

* <span data-ttu-id="2d3f8-111">Владелец</span><span class="sxs-lookup"><span data-stu-id="2d3f8-111">Owner</span></span>
* <span data-ttu-id="2d3f8-112">Пользователь DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="2d3f8-112">DevTest Labs User</span></span>
* <span data-ttu-id="2d3f8-113">Участник</span><span class="sxs-lookup"><span data-stu-id="2d3f8-113">Contributor</span></span>

<span data-ttu-id="2d3f8-114">Hello Следующая таблица показывает hello действия, выполненные пользователями в каждой из этих ролей.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-114">hello following table illustrates hello actions that can be performed by users in each of these roles:</span></span>

| <span data-ttu-id="2d3f8-115">**Действия, которые могут выполнять пользователи с этой ролью**</span><span class="sxs-lookup"><span data-stu-id="2d3f8-115">**Actions users in this role can perform**</span></span> | <span data-ttu-id="2d3f8-116">**Пользователь DevTest Labs**</span><span class="sxs-lookup"><span data-stu-id="2d3f8-116">**DevTest Labs User**</span></span> | <span data-ttu-id="2d3f8-117">**Владелец**</span><span class="sxs-lookup"><span data-stu-id="2d3f8-117">**Owner**</span></span> | <span data-ttu-id="2d3f8-118">**Участник**</span><span class="sxs-lookup"><span data-stu-id="2d3f8-118">**Contributor**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2d3f8-119">**Задачи лаборатории**</span><span class="sxs-lookup"><span data-stu-id="2d3f8-119">**Lab tasks**</span></span> | | | |
| <span data-ttu-id="2d3f8-120">Добавление пользователей tooa лаборатории</span><span class="sxs-lookup"><span data-stu-id="2d3f8-120">Add users tooa lab</span></span> |<span data-ttu-id="2d3f8-121">Нет</span><span class="sxs-lookup"><span data-stu-id="2d3f8-121">No</span></span> |<span data-ttu-id="2d3f8-122">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-122">Yes</span></span> |<span data-ttu-id="2d3f8-123">Нет</span><span class="sxs-lookup"><span data-stu-id="2d3f8-123">No</span></span> |
| <span data-ttu-id="2d3f8-124">Обновление параметров стоимости</span><span class="sxs-lookup"><span data-stu-id="2d3f8-124">Update cost settings</span></span> |<span data-ttu-id="2d3f8-125">Нет</span><span class="sxs-lookup"><span data-stu-id="2d3f8-125">No</span></span> |<span data-ttu-id="2d3f8-126">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-126">Yes</span></span> |<span data-ttu-id="2d3f8-127">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-127">Yes</span></span> |
| <span data-ttu-id="2d3f8-128">**Базовые задачи виртуальных машин**</span><span class="sxs-lookup"><span data-stu-id="2d3f8-128">**VM base tasks**</span></span> | | | |
| <span data-ttu-id="2d3f8-129">Добавление и удаление пользовательских образов</span><span class="sxs-lookup"><span data-stu-id="2d3f8-129">Add and remove custom images</span></span> |<span data-ttu-id="2d3f8-130">Нет</span><span class="sxs-lookup"><span data-stu-id="2d3f8-130">No</span></span> |<span data-ttu-id="2d3f8-131">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-131">Yes</span></span> |<span data-ttu-id="2d3f8-132">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-132">Yes</span></span> |
| <span data-ttu-id="2d3f8-133">Добавление, обновление и удаление формул</span><span class="sxs-lookup"><span data-stu-id="2d3f8-133">Add, update, and delete formulas</span></span> |<span data-ttu-id="2d3f8-134">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-134">Yes</span></span> |<span data-ttu-id="2d3f8-135">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-135">Yes</span></span> |<span data-ttu-id="2d3f8-136">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-136">Yes</span></span> |
| <span data-ttu-id="2d3f8-137">Разрешенные образы Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="2d3f8-137">Whitelist Azure Marketplace images</span></span> |<span data-ttu-id="2d3f8-138">Нет</span><span class="sxs-lookup"><span data-stu-id="2d3f8-138">No</span></span> |<span data-ttu-id="2d3f8-139">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-139">Yes</span></span> |<span data-ttu-id="2d3f8-140">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-140">Yes</span></span> |
| <span data-ttu-id="2d3f8-141">**Задачи виртуальных машин**</span><span class="sxs-lookup"><span data-stu-id="2d3f8-141">**VM tasks**</span></span> | | | |
| <span data-ttu-id="2d3f8-142">Создание виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="2d3f8-142">Create VMs</span></span> |<span data-ttu-id="2d3f8-143">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-143">Yes</span></span> |<span data-ttu-id="2d3f8-144">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-144">Yes</span></span> |<span data-ttu-id="2d3f8-145">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-145">Yes</span></span> |
| <span data-ttu-id="2d3f8-146">Запуск, остановка и удаление виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="2d3f8-146">Start, stop, and delete VMs</span></span> |<span data-ttu-id="2d3f8-147">Только виртуальные машины, созданные пользователем hello</span><span class="sxs-lookup"><span data-stu-id="2d3f8-147">Only VMs created by hello user</span></span> |<span data-ttu-id="2d3f8-148">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-148">Yes</span></span> |<span data-ttu-id="2d3f8-149">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-149">Yes</span></span> |
| <span data-ttu-id="2d3f8-150">Обновление политик виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="2d3f8-150">Update VM policies</span></span> |<span data-ttu-id="2d3f8-151">Нет</span><span class="sxs-lookup"><span data-stu-id="2d3f8-151">No</span></span> |<span data-ttu-id="2d3f8-152">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-152">Yes</span></span> |<span data-ttu-id="2d3f8-153">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-153">Yes</span></span> |
| <span data-ttu-id="2d3f8-154">Добавление и удаление дисков данных виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="2d3f8-154">Add/remove data disks to/from VMs</span></span> |<span data-ttu-id="2d3f8-155">Только виртуальные машины, созданные пользователем hello</span><span class="sxs-lookup"><span data-stu-id="2d3f8-155">Only VMs created by hello user</span></span> |<span data-ttu-id="2d3f8-156">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-156">Yes</span></span> |<span data-ttu-id="2d3f8-157">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-157">Yes</span></span> |
| <span data-ttu-id="2d3f8-158">**Задачи артефактов**</span><span class="sxs-lookup"><span data-stu-id="2d3f8-158">**Artifact tasks**</span></span> | | | |
| <span data-ttu-id="2d3f8-159">Добавление и удаление репозиториев артефактов</span><span class="sxs-lookup"><span data-stu-id="2d3f8-159">Add and remove artifact repositories</span></span> |<span data-ttu-id="2d3f8-160">Нет</span><span class="sxs-lookup"><span data-stu-id="2d3f8-160">No</span></span> |<span data-ttu-id="2d3f8-161">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-161">Yes</span></span> |<span data-ttu-id="2d3f8-162">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-162">Yes</span></span> |
| <span data-ttu-id="2d3f8-163">Применение артефактов</span><span class="sxs-lookup"><span data-stu-id="2d3f8-163">Apply artifacts</span></span> |<span data-ttu-id="2d3f8-164">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-164">Yes</span></span> |<span data-ttu-id="2d3f8-165">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-165">Yes</span></span> |<span data-ttu-id="2d3f8-166">Да</span><span class="sxs-lookup"><span data-stu-id="2d3f8-166">Yes</span></span> |

> [!NOTE]
> <span data-ttu-id="2d3f8-167">Если пользователь создает виртуальную Машину, этот пользователь будет автоматически назначено toohello **владельца** роль hello создания виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-167">When a user creates a VM, that user is automatically assigned toohello **Owner** role of hello created VM.</span></span>
> 
> 

## <a name="add-an-owner-or-user-at-hello-lab-level"></a><span data-ttu-id="2d3f8-168">Добавить владельца или пользователя на уровне hello лаборатории</span><span class="sxs-lookup"><span data-stu-id="2d3f8-168">Add an owner or user at hello lab level</span></span>
<span data-ttu-id="2d3f8-169">Владельцы и пользователи могут добавляться на уровне лаборатории hello через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-169">Owners and users can be added at hello lab level via hello Azure portal.</span></span> <span data-ttu-id="2d3f8-170">Можно также добавить внешних пользователей с допустимой [учетной записью Майкрософт (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="2d3f8-170">This includes external users with a valid [Microsoft account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span>
<span data-ttu-id="2d3f8-171">следующие шаги Hello проводит пользователя через процесс добавления лаборатории tooa владельцами или пользователями в Azure DevTest Labs hello:</span><span class="sxs-lookup"><span data-stu-id="2d3f8-171">hello following steps guide you through hello process of adding an owner or user tooa lab in Azure DevTest Labs:</span></span>

1. <span data-ttu-id="2d3f8-172">Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="2d3f8-172">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="2d3f8-173">Выберите **дополнительные службы**, а затем выберите **DevTest Labs** из списка hello.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-173">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="2d3f8-174">Выберите из списка hello лабораториям hello требуемой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-174">From hello list of labs, select hello desired lab.</span></span>
4. <span data-ttu-id="2d3f8-175">В колонке hello лаборатории выберите **конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-175">On hello lab's blade, select **Configuration**.</span></span> 
5. <span data-ttu-id="2d3f8-176">На hello **конфигурации** колонке выберите **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-176">On hello **Configuration** blade, select **Users**.</span></span>
6. <span data-ttu-id="2d3f8-177">На hello **пользователей** колонке выберите **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-177">On hello **Users** blade, select **+Add**.</span></span>
   
    ![Добавить пользователя](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. <span data-ttu-id="2d3f8-179">На hello **выберите роль** колонки, hello выберите нужную роль.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-179">On hello **Select a role** blade, select hello desired role.</span></span> <span data-ttu-id="2d3f8-180">Здравствуйте, раздел [действия, которые могут быть выполнены в каждой роли](#actions-that-can-be-performed-in-each-role) списки hello различные действия, выполненные пользователями в hello владельца, DevTest пользователя или участника роли.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-180">hello section [Actions that can be performed in each role](#actions-that-can-be-performed-in-each-role) lists hello various actions that can be performed by users in hello Owner, DevTest User, and Contributor roles.</span></span>
8. <span data-ttu-id="2d3f8-181">На hello **Добавление пользователей** колонки, введите адрес электронной почты hello или имя пользователя hello требуется tooadd в указанной роли hello.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-181">On hello **Add users** blade, enter hello email address or name of hello user you want tooadd in hello role you specified.</span></span> <span data-ttu-id="2d3f8-182">Если не удается найти пользователя hello, сообщение об ошибке описывается проблема hello.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-182">If hello user can't be found, an error message explains hello issue.</span></span> <span data-ttu-id="2d3f8-183">При обнаружении hello пользователя этот пользователь перечислены и выбраны.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-183">If hello user is found, that user is listed and selected.</span></span> 
9. <span data-ttu-id="2d3f8-184">Щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-184">Select **Select**.</span></span>
10. <span data-ttu-id="2d3f8-185">Выберите **ОК** tooclose hello **добавить доступ** колонку.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-185">Select **OK** tooclose hello **Add access** blade.</span></span>
11. <span data-ttu-id="2d3f8-186">При возвращении toohello **пользователей** колонке hello пользователь был добавлен.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-186">When you return toohello **Users** blade, hello user has been added.</span></span>  

## <a name="add-an-external-user-tooa-lab-using-powershell"></a><span data-ttu-id="2d3f8-187">Добавить лаборатории tooa внешнего пользователя, с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="2d3f8-187">Add an external user tooa lab using PowerShell</span></span>
<span data-ttu-id="2d3f8-188">Кроме того при tooadding пользователей в hello портал Azure, можно добавить лаборатории tooyour внешнего пользователя, с помощью сценария PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-188">In addition tooadding users in hello Azure portal, you can add an external user tooyour lab using a PowerShell script.</span></span> <span data-ttu-id="2d3f8-189">В hello просто следующий пример, измените значения параметров hello под hello **toochange значения** комментарий.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-189">In hello following example, simply modify hello parameter values under hello **Values toochange** comment.</span></span>
<span data-ttu-id="2d3f8-190">Вы можете получить hello `subscriptionId`, `labResourceGroup`, и `labName` значения из колонки лаборатории hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-190">You can retrieve hello `subscriptionId`, `labResourceGroup`, and `labName` values from hello lab blade in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="2d3f8-191">Образец Hello скрипта предполагается, что, hello указанный пользователь был добавлен в качестве гостя toohello Active Directory и завершится ошибкой, если это не так hello.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-191">hello sample script assumes that hello specified user has been added as a guest toohello Active Directory, and will fail if that is not hello case.</span></span> <span data-ttu-id="2d3f8-192">пользователь не зарегистрирован в hello лаборатории tooa Active Directory, tooadd использовать hello Azure портала tooassign hello tooa роль пользователя согласно инструкциям в разделе "hello" [добавьте владельца или пользователя на уровне лаборатории hello](#add-an-owner-or-user-at-the-lab-level).</span><span class="sxs-lookup"><span data-stu-id="2d3f8-192">tooadd a user not in hello Active Directory tooa lab, use hello Azure portal tooassign hello user tooa role as illustrated in hello section, [Add an owner or user at hello lab level](#add-an-owner-or-user-at-the-lab-level).</span></span>   
> 
> 

    # Add an external user in DevTest Labs user role tooa lab
    # Ensure that guest users can be added toohello Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve hello user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create hello role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-hello-subscription-level"></a><span data-ttu-id="2d3f8-193">Добавление владельца или пользователя на уровне подписки hello</span><span class="sxs-lookup"><span data-stu-id="2d3f8-193">Add an owner or user at hello subscription level</span></span>
<span data-ttu-id="2d3f8-194">Разрешения Azure переносятся из родительской области toochild область в Azure.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-194">Azure permissions are propagated from parent scope toochild scope in Azure.</span></span> <span data-ttu-id="2d3f8-195">Таким образом, владельцы подписки Azure, содержащей лаборатории, автоматически являются владельцами этих лабораторий.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-195">Therefore, owners of an Azure subscription that contains labs are automatically owners of those labs.</span></span> <span data-ttu-id="2d3f8-196">Они также являются hello виртуальные машины и другие ресурсы, созданные пользователями лаборатории hello и hello Azure DevTest Labs службы.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-196">They also own hello VMs and other resources created by hello lab's users, and hello Azure DevTest Labs service.</span></span> 

<span data-ttu-id="2d3f8-197">Можно добавить дополнительных владельцев лаборатории tooa через колонки hello лаборатории в hello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="2d3f8-197">You can add additional owners tooa lab via hello lab's blade in hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="2d3f8-198">Однако hello добавлена владельца области администрирования более узкий выше владельца подписки hello области.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-198">However, hello added owner's scope of administration is more narrow than hello subscription owner's scope.</span></span> <span data-ttu-id="2d3f8-199">Например hello добавлены владельцы имеют полный доступ toosome hello ресурсов, созданные в подписке hello hello DevTest Labs службы.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-199">For example, hello added owners do not have full access toosome of hello resources that are created in hello subscription by hello DevTest Labs service.</span></span> 

<span data-ttu-id="2d3f8-200">tooadd tooan владелец подписки Azure, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-200">tooadd an owner tooan Azure subscription, follow these steps:</span></span>

1. <span data-ttu-id="2d3f8-201">Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="2d3f8-201">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="2d3f8-202">Выберите **более служб**, а затем выберите **подписки** из списка hello.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-202">Select **More Services**, and then select **Subscriptions** from hello list.</span></span>
3. <span data-ttu-id="2d3f8-203">Выберите подписку требуемого hello.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-203">Select hello desired subscription.</span></span>
4. <span data-ttu-id="2d3f8-204">Щелкните значок **Доступ** .</span><span class="sxs-lookup"><span data-stu-id="2d3f8-204">Select **Access** icon.</span></span> 
   
    ![Доступ к пользователям](./media/devtest-lab-add-devtest-user/access-users.png)
5. <span data-ttu-id="2d3f8-206">На hello **пользователей** колонке выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-206">On hello **Users** blade, select **Add**.</span></span>
   
    ![Добавить пользователя](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. <span data-ttu-id="2d3f8-208">На hello **выберите роль** колонке выберите **владельца**.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-208">On hello **Select a role** blade, select **Owner**.</span></span>
7. <span data-ttu-id="2d3f8-209">На hello **Добавление пользователей** колонки, введите имя или адрес электронной почты hello hello пользователя требуется tooadd в качестве владельца.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-209">On hello **Add users** blade, enter hello email address or name of hello user you want tooadd as an owner.</span></span> <span data-ttu-id="2d3f8-210">Если не удается найти пользователя hello, появляется сообщение об ошибке, поясняющий hello.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-210">If hello user can't be found, you get an error message explaining hello issue.</span></span> <span data-ttu-id="2d3f8-211">Если hello пользователь найден, этот пользователь будет помещен в hello **пользователя** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-211">If hello user is found, that user is listed under hello **User** text box.</span></span>
8. <span data-ttu-id="2d3f8-212">Выберите имя hello найти пользователя.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-212">Select hello located user name.</span></span>
9. <span data-ttu-id="2d3f8-213">Щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-213">Select **Select**.</span></span>
10. <span data-ttu-id="2d3f8-214">Выберите **ОК** tooclose hello **добавить доступ** колонку.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-214">Select **OK** tooclose hello **Add access** blade.</span></span>
11. <span data-ttu-id="2d3f8-215">При возвращении toohello **пользователей** колонке hello пользователь добавлен в качестве владельца.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-215">When you return toohello **Users** blade, hello user has been added as an owner.</span></span> <span data-ttu-id="2d3f8-216">Этот пользователь будет владельца любого labs, созданных под этой подпиской и таким образом может tooperform владельца задачи.</span><span class="sxs-lookup"><span data-stu-id="2d3f8-216">This user is now an owner of any labs created under this subscription, and thus be able tooperform owner tasks.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

