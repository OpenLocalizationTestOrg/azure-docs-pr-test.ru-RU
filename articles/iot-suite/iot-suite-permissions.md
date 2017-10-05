---
title: "Azure IoT Suite и Azure Active Directory | Документация Майкрософт"
description: "В этой статье описывается, как набор Azure IoT Suite использует Azure Active Directory для управления разрешениями."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 246228ba-954a-4d96-b6d6-e53e4590cb4f
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: dobett
ms.openlocfilehash: 518e6a481ab6385b03dd3ddc2e155fb724e677fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="permissions-on-the-azureiotsuitecom-site"></a><span data-ttu-id="351b8-103">Разрешения на сайте azureiotsuite.com</span><span class="sxs-lookup"><span data-stu-id="351b8-103">Permissions on the azureiotsuite.com site</span></span>

## <a name="what-happens-when-you-sign-in"></a><span data-ttu-id="351b8-104">Что происходит при входе</span><span class="sxs-lookup"><span data-stu-id="351b8-104">What happens when you sign in</span></span>

<span data-ttu-id="351b8-105">При первом входе сайт [azureiotsuite.com][lnk-azureiotsuite] определяет ваши уровни разрешений в зависимости от выбранного клиента Azure Active Directory (AAD) и подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="351b8-105">The first time you sign in at [azureiotsuite.com][lnk-azureiotsuite], the site determines the permission levels you have based on the currently selected Azure Active Directory (AAD) tenant and Azure subscription.</span></span>

1. <span data-ttu-id="351b8-106">Сначала сайт получает из Azure сведения о ваших клиентах AAD, чтобы заполнить список клиентов, который отображается рядом с вашим именем пользователя после входа.</span><span class="sxs-lookup"><span data-stu-id="351b8-106">First, to populate the list of tenants seen next to your username, the site finds out from Azure which AAD tenants you belong to.</span></span> <span data-ttu-id="351b8-107">В настоящее время сайт может одновременно получать маркеры пользователя только для одного клиента.</span><span class="sxs-lookup"><span data-stu-id="351b8-107">Currently, the site can only obtain user tokens for one tenant at a time.</span></span> <span data-ttu-id="351b8-108">Поэтому, если вы переключитесь между клиентами в раскрывающемся списке в правом верхнем углу сайта, вам придется выполнить вход с указанием этого клиента, чтобы получить для него маркеры.</span><span class="sxs-lookup"><span data-stu-id="351b8-108">Therefore, when you switch tenants using the dropdown in the top right corner, the site logs you in to that tenant to obtain the tokens for that tenant.</span></span>

2. <span data-ttu-id="351b8-109">После этого сайт получает из Azure сведения о подписках, связанных с выбранным клиентом.</span><span class="sxs-lookup"><span data-stu-id="351b8-109">Next, the site finds out from Azure which subscriptions you have associated with the selected tenant.</span></span> <span data-ttu-id="351b8-110">Доступные подписки можно просмотреть при создании нового предварительно настроенного решения.</span><span class="sxs-lookup"><span data-stu-id="351b8-110">You see the available subscriptions when you create a new preconfigured solution.</span></span>

3. <span data-ttu-id="351b8-111">Наконец, сайт получает сведения о всех ресурсах в подписках и группах ресурсов, помеченных как предварительно настроенные решения, и заполняет элементы на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="351b8-111">Finally, the site retrieves all the resources in the subscriptions and resource groups tagged as preconfigured solutions and populates the tiles on the home page.</span></span>

<span data-ttu-id="351b8-112">В следующих разделах описываются роли, которые позволяют управлять доступом к предварительно настроенным решениям.</span><span class="sxs-lookup"><span data-stu-id="351b8-112">The following sections describe the roles that control access to the preconfigured solutions.</span></span>

## <a name="aad-roles"></a><span data-ttu-id="351b8-113">Роли AAD</span><span class="sxs-lookup"><span data-stu-id="351b8-113">AAD roles</span></span>

<span data-ttu-id="351b8-114">Роли AAD определяют возможность подготавливать предварительно настроенные решения и управлять пользователями в предварительно настроенных решениях.</span><span class="sxs-lookup"><span data-stu-id="351b8-114">The AAD roles control the ability provision preconfigured solutions and manage users in a preconfigured solution.</span></span>

<span data-ttu-id="351b8-115">Дополнительные сведения о ролях администратора в AAD см. в статье [Назначение ролей администратора в Azure AD][lnk-aad-admin].</span><span class="sxs-lookup"><span data-stu-id="351b8-115">You can find more information about administrator roles in AAD in [Assigning administrator roles in Azure AD][lnk-aad-admin].</span></span> <span data-ttu-id="351b8-116">В этой статье основное внимание уделяется ролям **глобального администратора**, а также **пользовательским** ролям каталога, которые используются в предварительно настроенных решениях.</span><span class="sxs-lookup"><span data-stu-id="351b8-116">The current article focuses on the **Global Administrator** and the **User** directory roles as used by the preconfigured solutions.</span></span>

### <a name="global-administrator"></a><span data-ttu-id="351b8-117">Глобальный администратор.</span><span class="sxs-lookup"><span data-stu-id="351b8-117">Global administrator</span></span>

<span data-ttu-id="351b8-118">В одном клиенте AAD может быть несколько глобальных администраторов.</span><span class="sxs-lookup"><span data-stu-id="351b8-118">There can be many global administrators per AAD tenant:</span></span>

* <span data-ttu-id="351b8-119">Создавая клиент AAD, вы по умолчанию становитесь его глобальным администратором.</span><span class="sxs-lookup"><span data-stu-id="351b8-119">When you create an AAD tenant, you are by default the global administrator of that tenant.</span></span>
* <span data-ttu-id="351b8-120">Глобальный администратор может подготовить предварительно настроенное решение. В таком случае ему назначается роль **администратора** приложения в клиенте AAD.</span><span class="sxs-lookup"><span data-stu-id="351b8-120">The global administrator can provision a preconfigured solution and is assigned an **Admin** role for the application inside their AAD tenant.</span></span>
* <span data-ttu-id="351b8-121">Если другой пользователь в том же клиенте AAD создаст приложение, глобальному администратору будет по умолчанию присвоена роль **только для чтения**.</span><span class="sxs-lookup"><span data-stu-id="351b8-121">If another user in the same AAD tenant creates an application, the default role granted to the global administrator is **ReadOnly**.</span></span>
* <span data-ttu-id="351b8-122">Глобальный администратор может назначать пользователям роли для приложений, используя [портал Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="351b8-122">A global administrator can assign users to roles for applications using the [Azure portal][lnk-portal].</span></span>

### <a name="domain-user"></a><span data-ttu-id="351b8-123">Пользователь домена</span><span class="sxs-lookup"><span data-stu-id="351b8-123">Domain user</span></span>

<span data-ttu-id="351b8-124">На каждый клиент AAD может приходиться много пользователей домена.</span><span class="sxs-lookup"><span data-stu-id="351b8-124">There can be many domain users per AAD tenant:</span></span>

* <span data-ttu-id="351b8-125">Пользователь домена может подготовить предварительно настроенное решение на сайте [azureiotsuite.com][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="351b8-125">A domain user can provision a preconfigured solution through the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="351b8-126">По умолчанию пользователю домена предоставляется роль **Администратор** в подготавливаемом приложении.</span><span class="sxs-lookup"><span data-stu-id="351b8-126">By default, the domain user is granted the **Admin** role in the provisioned application.</span></span>
* <span data-ttu-id="351b8-127">Пользователь домена может создать приложение с помощью скрипта build.cmd в репозитории [azure-iot-remote-monitoring][lnk-rm-github-repo], [azure-iot-predictive-maintenance][lnk-pm-github-repo] или [azure-iot-connected-factory][lnk-cf-github-repo].</span><span class="sxs-lookup"><span data-stu-id="351b8-127">A domain user can create an application using the build.cmd script in the [azure-iot-remote-monitoring][lnk-rm-github-repo],  [azure-iot-predictive-maintenance][lnk-pm-github-repo], or [azure-iot-connected-factory][lnk-cf-github-repo] repository.</span></span> <span data-ttu-id="351b8-128">Однако ему по умолчанию присваивается роль **только для чтения**, так как он не имеет права назначать роли.</span><span class="sxs-lookup"><span data-stu-id="351b8-128">However, the default role granted to the domain user is **ReadOnly**, because a domain user does not have permission to assign roles.</span></span>
* <span data-ttu-id="351b8-129">Если другой пользователь в клиенте AAD создаст приложение, пользователю домена по умолчанию будет присвоена роль **только для чтения** для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="351b8-129">If another user in the AAD tenant creates an application, the domain user is assigned the **ReadOnly** role by default for that application.</span></span>
* <span data-ttu-id="351b8-130">Пользователь домена не может назначать роли для приложений, поэтому он не может добавлять пользователей к ролям или присваивать пользователям роли для приложения, даже если он подготовил это приложение.</span><span class="sxs-lookup"><span data-stu-id="351b8-130">A domain user cannot assign roles for applications; therefore a domain user cannot add users or roles for users for an application even if they provisioned it.</span></span>

### <a name="guest-user"></a><span data-ttu-id="351b8-131">Гостевой пользователь</span><span class="sxs-lookup"><span data-stu-id="351b8-131">Guest User</span></span>

<span data-ttu-id="351b8-132">В одном клиенте AAD может быть много гостевых пользователей.</span><span class="sxs-lookup"><span data-stu-id="351b8-132">There can be many guest users per AAD tenant.</span></span> <span data-ttu-id="351b8-133">Пользователи-гости обладают ограниченным набором прав в клиенте AAD.</span><span class="sxs-lookup"><span data-stu-id="351b8-133">Guest users have a limited set of rights in the AAD tenant.</span></span> <span data-ttu-id="351b8-134">Поэтому они не могут подготавливать предварительно настроенные решения в клиенте AAD.</span><span class="sxs-lookup"><span data-stu-id="351b8-134">As a result, guest users cannot provision a preconfigured solution in the AAD tenant.</span></span>

<span data-ttu-id="351b8-135">Дополнительные сведения о пользователях и ролях в AAD см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="351b8-135">For more information about users and roles in AAD, see the following resources:</span></span>

* <span data-ttu-id="351b8-136">[Добавление новых пользователей или пользователей с учетными записями Майкрософт в Azure Active Directory][lnk-create-edit-users]</span><span class="sxs-lookup"><span data-stu-id="351b8-136">[Create users in Azure AD][lnk-create-edit-users]</span></span>
* <span data-ttu-id="351b8-137">[Назначение пользователя или группы корпоративному приложению в предварительной версии Azure Active Directory][lnk-assign-app-roles]</span><span class="sxs-lookup"><span data-stu-id="351b8-137">[Assign users to apps][lnk-assign-app-roles]</span></span>

## <a name="azure-subscription-administrator-roles"></a><span data-ttu-id="351b8-138">Роли администратора подписки Azure</span><span class="sxs-lookup"><span data-stu-id="351b8-138">Azure subscription administrator roles</span></span>

<span data-ttu-id="351b8-139">Роли администратора Azure определяют возможность сопоставлять подписку Azure с клиентом AD.</span><span class="sxs-lookup"><span data-stu-id="351b8-139">The Azure admin roles control the ability to map an Azure subscription to an AD tenant.</span></span>

<span data-ttu-id="351b8-140">Дополнительные сведения о ролях администраторов Azure см. в статье [Добавление или изменение ролей администратора Azure, управляющих подписками и службами][lnk-admin-roles].</span><span class="sxs-lookup"><span data-stu-id="351b8-140">Find out more about the Azure admin roles in the article [How to add or change Azure Co-Administrator, Service Administrator, and Account Administrator][lnk-admin-roles].</span></span>

## <a name="application-roles"></a><span data-ttu-id="351b8-141">Роли приложений</span><span class="sxs-lookup"><span data-stu-id="351b8-141">Application roles</span></span>

<span data-ttu-id="351b8-142">Роли приложения позволяют контролировать доступ к устройствам в рамках предварительно настроенного решения.</span><span class="sxs-lookup"><span data-stu-id="351b8-142">The application roles control access to devices in your preconfigured solution.</span></span>

<span data-ttu-id="351b8-143">В подготовленном приложении существует две определенные и одна неявная роль.</span><span class="sxs-lookup"><span data-stu-id="351b8-143">There are two defined roles and one implicit role defined in a provisioned application:</span></span>

* <span data-ttu-id="351b8-144">**Администратор** может добавлять, удалять устройства и управлять ими, а также изменять параметры.</span><span class="sxs-lookup"><span data-stu-id="351b8-144">**Admin:** Has full control to add, manage, remove devices, and modify settings.</span></span>
* <span data-ttu-id="351b8-145">**Только для чтения.** Просмотр устройств, правил, действий, заданий и телеметрии.</span><span class="sxs-lookup"><span data-stu-id="351b8-145">**ReadOnly:** Can view devices, rules, actions, jobs, and telemetry.</span></span>

<span data-ttu-id="351b8-146">Вы можете найти разрешения, назначаемые каждой роли, в исходном файле [RolePermissions.cs][lnk-resource-cs].</span><span class="sxs-lookup"><span data-stu-id="351b8-146">You can find the permissions assigned to each role in the [RolePermissions.cs][lnk-resource-cs] source file.</span></span>

### <a name="changing-application-roles-for-a-user"></a><span data-ttu-id="351b8-147">Изменение ролей приложений для пользователя</span><span class="sxs-lookup"><span data-stu-id="351b8-147">Changing application roles for a user</span></span>

<span data-ttu-id="351b8-148">Чтобы сделать пользователя в Active Directory администратором предварительно настроенного решения, можно выполнить описанную ниже процедуру.</span><span class="sxs-lookup"><span data-stu-id="351b8-148">You can use the following procedure to make a user in your Active Directory an administrator of your preconfigured solution.</span></span>

<span data-ttu-id="351b8-149">Изменять роли пользователей может только глобальный администратор AAD.</span><span class="sxs-lookup"><span data-stu-id="351b8-149">You must be an AAD global administrator to change roles for a user:</span></span>

1. <span data-ttu-id="351b8-150">Перейдите на [портал Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="351b8-150">Go to the [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="351b8-151">Выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="351b8-151">Select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="351b8-152">Убедитесь, что вы используете каталог, который вы выбрали на сайте azureiotsuite.com при подготовке решения.</span><span class="sxs-lookup"><span data-stu-id="351b8-152">Make sure you are using the directory you chose on azureiotsuite.com when you provisioned your solution.</span></span> <span data-ttu-id="351b8-153">При наличии нескольких каталогов, связанных с подпиской, можно переключаться между ними, щелкнув имя учетной записи в правом верхнем углу страницы портала.</span><span class="sxs-lookup"><span data-stu-id="351b8-153">If you have multiple directories associated with your subscription, you can switch between them if you click your account name at the top-right of the portal.</span></span>
4. <span data-ttu-id="351b8-154">Щелкните **Корпоративные приложения**, а затем **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="351b8-154">Click **Enterprise applications**, then **All applications**.</span></span>
4. <span data-ttu-id="351b8-155">Отобразите **все приложения** с состоянием **Любой**.</span><span class="sxs-lookup"><span data-stu-id="351b8-155">Show **All applications** with **Any** status.</span></span> <span data-ttu-id="351b8-156">Затем найдите приложения с именем вашего предварительно настроенного решения.</span><span class="sxs-lookup"><span data-stu-id="351b8-156">Then search for an application with name of your preconfigured solution.</span></span>
5. <span data-ttu-id="351b8-157">Щелкните имя приложения, совпадающее с именем предварительно настроенного решения.</span><span class="sxs-lookup"><span data-stu-id="351b8-157">Click the name of the application that matches your preconfigured solution name.</span></span>
6. <span data-ttu-id="351b8-158">Щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="351b8-158">Click **Users and groups**.</span></span>
7. <span data-ttu-id="351b8-159">Выберите пользователя, для которого нужно изменить роли.</span><span class="sxs-lookup"><span data-stu-id="351b8-159">Select the user you want to switch roles.</span></span>
8. <span data-ttu-id="351b8-160">Щелкните **Назначить** и выберите роль (например, **Администратор**), которую нужно назначить пользователю, установив соответствующий флажок.</span><span class="sxs-lookup"><span data-stu-id="351b8-160">Click **Assign** and select the role (such as **Admin**) you'd like to assign to the user, click the check mark.</span></span>

## <a name="faq"></a><span data-ttu-id="351b8-161">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="351b8-161">FAQ</span></span>

### <a name="im-a-service-administrator-and-id-like-to-change-the-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a><span data-ttu-id="351b8-162">Я являюсь администратором службы и хочу изменить сопоставление каталогов подписки и конкретного клиента AAD.</span><span class="sxs-lookup"><span data-stu-id="351b8-162">I'm a service administrator and I'd like to change the directory mapping between my subscription and a specific AAD tenant.</span></span> <span data-ttu-id="351b8-163">Как выполнить эту задачу?</span><span class="sxs-lookup"><span data-stu-id="351b8-163">How do I complete this task?</span></span>

1. <span data-ttu-id="351b8-164">Войдите на [классический портал Azure][lnk-classic-portal] и выберите пункт **Параметры** в списке служб слева.</span><span class="sxs-lookup"><span data-stu-id="351b8-164">Go to the [Azure classic portal][lnk-classic-portal], click **Settings** in the list of services on the left-hand side.</span></span>
2. <span data-ttu-id="351b8-165">Выберите подписку, для которой вы хотите изменить сопоставление каталогов.</span><span class="sxs-lookup"><span data-stu-id="351b8-165">Select the subscription you'd like to change the directory mapping to.</span></span>
3. <span data-ttu-id="351b8-166">Щелкните **Изменить каталог**.</span><span class="sxs-lookup"><span data-stu-id="351b8-166">Click **Edit Directory**.</span></span>
4. <span data-ttu-id="351b8-167">Выберите в раскрывающемся списке **каталог** , который следует использовать.</span><span class="sxs-lookup"><span data-stu-id="351b8-167">Select the **Directory** you would like to use in the dropdown.</span></span> <span data-ttu-id="351b8-168">Щелкните стрелку «Далее».</span><span class="sxs-lookup"><span data-stu-id="351b8-168">Click the forward arrow.</span></span>
5. <span data-ttu-id="351b8-169">Проверьте сопоставление каталога и соответствующих соадминистраторов.</span><span class="sxs-lookup"><span data-stu-id="351b8-169">Confirm the directory mapping and affected co-administrators.</span></span> <span data-ttu-id="351b8-170">При перемещении из другого каталога удаляются все соадминистраторы из исходного каталога.</span><span class="sxs-lookup"><span data-stu-id="351b8-170">If you are moving from another directory, all the co-administrators from the original directory are removed.</span></span>

### <a name="im-a-domain-usermember-on-the-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a><span data-ttu-id="351b8-171">Я являюсь пользователем (членом) домена в клиенте AAD и создаю предварительно настроенное решение.</span><span class="sxs-lookup"><span data-stu-id="351b8-171">I'm a domain user/member on the AAD tenant and I've created a preconfigured solution.</span></span> <span data-ttu-id="351b8-172">Как мне получить роль для своего приложения?</span><span class="sxs-lookup"><span data-stu-id="351b8-172">How do I get assigned a role for my application?</span></span>

<span data-ttu-id="351b8-173">Попросите глобального администратора назначить вас глобальным администратором клиента AAD, а затем назначьте роли пользователям самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="351b8-173">Ask a global administrator to make you a global administrator on the AAD tenant and then assign roles to users yourself.</span></span> <span data-ttu-id="351b8-174">Кроме того, вы можете попросить глобального администратора назначить вам роль напрямую.</span><span class="sxs-lookup"><span data-stu-id="351b8-174">Alternatively, ask a global administrator to assign you a role directly.</span></span> <span data-ttu-id="351b8-175">Если вы хотите сменить клиент AAD, в котором развернуто ваше предварительно настроенное решение, см. следующий вопрос.</span><span class="sxs-lookup"><span data-stu-id="351b8-175">If you'd like to change the AAD tenant your preconfigured solution has been deployed to, see the next question.</span></span>

### <a name="how-do-i-switch-the-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a><span data-ttu-id="351b8-176">Как сменить клиент AAD, которому назначены мое предварительно настроенное решение удаленного мониторинга и приложение?</span><span class="sxs-lookup"><span data-stu-id="351b8-176">How do I switch the AAD tenant my remote monitoring preconfigured solution and application are assigned to?</span></span>

<span data-ttu-id="351b8-177">Можно запустить развернутую облачную службу со страницы <https://github.com/Azure/azure-iot-remote-monitoring> и повторить развертывание в новом клиенте AAD.</span><span class="sxs-lookup"><span data-stu-id="351b8-177">You can run a cloud deployment from <https://github.com/Azure/azure-iot-remote-monitoring> and redeploy with a newly created AAD tenant.</span></span> <span data-ttu-id="351b8-178">При создании клиента AAD вы по умолчанию назначаетесь глобальным администратором с разрешениями на добавление пользователей и назначение им ролей.</span><span class="sxs-lookup"><span data-stu-id="351b8-178">Because you are, by default, a global administrator when you create an AAD tenant, you have permissions to add users and assign roles to those users.</span></span>

1. <span data-ttu-id="351b8-179">Создайте каталог AAD на [портале Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="351b8-179">Create an AAD directory in the [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="351b8-180">Перейдите на страницу <https://github.com/Azure/azure-iot-remote-monitoring>.</span><span class="sxs-lookup"><span data-stu-id="351b8-180">Go to <https://github.com/Azure/azure-iot-remote-monitoring>.</span></span>
3. <span data-ttu-id="351b8-181">Выполните команду `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (например, `build.cmd cloud debug myRMSolution`).</span><span class="sxs-lookup"><span data-stu-id="351b8-181">Run `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (For example, `build.cmd cloud debug myRMSolution`)</span></span>
4. <span data-ttu-id="351b8-182">При появлении запроса задайте параметр **tenantid** для нового клиента вместо предыдущего клиента.</span><span class="sxs-lookup"><span data-stu-id="351b8-182">When prompted, set the **tenantid** to be your newly created tenant instead of your previous tenant.</span></span>

### <a name="i-want-to-change-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a><span data-ttu-id="351b8-183">Я хочу сменить администратора службы и соадминистратора при входе в систему с использованием учетной записи организации</span><span class="sxs-lookup"><span data-stu-id="351b8-183">I want to change a Service Administrator or Co-Administrator when logged in with an organisational account</span></span>

<span data-ttu-id="351b8-184">См. справочную статью [Смена администратора службы и соадминистратора при входе в систему с использованием учетной записи организации][lnk-service-admins].</span><span class="sxs-lookup"><span data-stu-id="351b8-184">See the support article [Changing Service Administrator and Co-Administrator when logged in with an organisational account][lnk-service-admins].</span></span>

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-the-proper-permissions-to-create-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a><span data-ttu-id="351b8-185">Почему появляется ошибка</span><span class="sxs-lookup"><span data-stu-id="351b8-185">Why am I seeing this error?</span></span> <span data-ttu-id="351b8-186">«У вашей учетной записи нет необходимых разрешений для создания решения.</span><span class="sxs-lookup"><span data-stu-id="351b8-186">"Your account does not have the proper permissions to create a solution.</span></span> <span data-ttu-id="351b8-187">Обратитесь к администратору учетной записи или попробуйте использовать другую учетную запись»</span><span class="sxs-lookup"><span data-stu-id="351b8-187">Please check with your account administrator or try with a different account."</span></span>

<span data-ttu-id="351b8-188">Руководствуйтесь следующей схемой:</span><span class="sxs-lookup"><span data-stu-id="351b8-188">Look at the following diagram for guidance:</span></span>

![][img-flowchart]

> [!NOTE]
> <span data-ttu-id="351b8-189">Вы выполнили проверку, которая подтверждает ваши права глобального администратора на клиенте AAD и соадминистратора подписки, но ошибка не устранена. В таком случае администратор учетной записи должен удалить этого пользователя и повторно назначить необходимые разрешения в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="351b8-189">If you continue to see the error after validating you are a global administrator on the AAD tenant and a co-administrator on the subscription, have your account administrator remove the user and reassign necessary permissions in this order.</span></span> <span data-ttu-id="351b8-190">Сначала добавить пользователя в качестве глобального администратора, а затем — пользователя в качестве соадминистратора подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="351b8-190">First, add the user as a global administrator and then add user as a co-administrator on the Azure subscription.</span></span> <span data-ttu-id="351b8-191">Если проблемы не удается устранить, обратитесь в службу [справки и поддержки][lnk-help-support].</span><span class="sxs-lookup"><span data-stu-id="351b8-191">If issues persist, contact [Help & Support][lnk-help-support].</span></span>

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-to-create-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a><span data-ttu-id="351b8-192">Почему эта ошибка появляется при наличии подписки Azure?</span><span class="sxs-lookup"><span data-stu-id="351b8-192">Why am I seeing this error when I have an Azure subscription?</span></span> <span data-ttu-id="351b8-193">"Для создания предварительно настроенных решений требуется подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="351b8-193">"An Azure subscription is required to create pre-configured solutions.</span></span> <span data-ttu-id="351b8-194">Вы можете создать бесплатную пробную учетную запись всего за несколько минут".</span><span class="sxs-lookup"><span data-stu-id="351b8-194">You can create a free trial account in just a couple of minutes."</span></span>

<span data-ttu-id="351b8-195">Если точно известно, что у вас есть подписка Azure, проверьте сопоставление клиентов для своей подписки и убедитесь, что в раскрывающемся списке выбран правильный клиент.</span><span class="sxs-lookup"><span data-stu-id="351b8-195">If you're certain you have an Azure subscription, validate the tenant mapping for your subscription and ensure the correct tenant is selected in the dropdown.</span></span> <span data-ttu-id="351b8-196">Если клиент выбран правильно, следуйте приведенной выше схеме и проверьте сопоставление подписки и этого клиента AAD.</span><span class="sxs-lookup"><span data-stu-id="351b8-196">If you’ve validated the desired tenant is correct, follow the preceding diagram and validate the mapping of your subscription and this AAD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="351b8-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="351b8-197">Next steps</span></span>
<span data-ttu-id="351b8-198">Чтобы продолжить изучение IoT Suite, см. статью [Настройка предварительно настроенного решения][lnk-customize].</span><span class="sxs-lookup"><span data-stu-id="351b8-198">To continue learning about IoT Suite, see how you can [customize a preconfigured solution][lnk-customize].</span></span>

[img-flowchart]: media/iot-suite-permissions/flowchart.png

[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-rm-github-repo]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-pm-github-repo]: https://github.com/Azure/azure-iot-predictive-maintenance
[lnk-cf-github-repo]: https://github.com/Azure/azure-iot-connected-factory
[lnk-aad-admin]: ../active-directory/active-directory-assign-admin-roles.md
[lnk-classic-portal]: https://manage.windowsazure.com/
[lnk-portal]: https://portal.azure.com/
[lnk-create-edit-users]: ../active-directory/active-directory-create-users.md
[lnk-assign-app-roles]: ../active-directory/active-directory-coreapps-assign-user-azure-portal.md
[lnk-service-admins]: https://azure.microsoft.com/support/changing-service-admin-and-co-admin/
[lnk-admin-roles]: ../billing/billing-add-change-azure-subscription-administrator.md
[lnk-resource-cs]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/DeviceAdministration/Web/Security/RolePermissions.cs
[lnk-help-support]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
