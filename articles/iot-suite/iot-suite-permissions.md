---
title: "aaaAzure IoT Suite и Azure Active Directory | Документы Microsoft"
description: "Описывает, как Azure IoT Suite использует Azure Active Directory toomanage разрешения."
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
ms.openlocfilehash: 4768630f2de4bb431731fbd4e8929232bc80b9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-on-hello-azureiotsuitecom-site"></a><span data-ttu-id="4ac82-103">Разрешения на сайт azureiotsuite.com hello</span><span class="sxs-lookup"><span data-stu-id="4ac82-103">Permissions on hello azureiotsuite.com site</span></span>

## <a name="what-happens-when-you-sign-in"></a><span data-ttu-id="4ac82-104">Что происходит при входе</span><span class="sxs-lookup"><span data-stu-id="4ac82-104">What happens when you sign in</span></span>

<span data-ttu-id="4ac82-105">Здравствуйте, войдите в первый раз [azureiotsuite.com][lnk-azureiotsuite], hello сайту определяет, основано на hello в настоящее время уровни разрешений hello выбранного клиента Azure Active Directory (AAD) и Azure подписка.</span><span class="sxs-lookup"><span data-stu-id="4ac82-105">hello first time you sign in at [azureiotsuite.com][lnk-azureiotsuite], hello site determines hello permission levels you have based on hello currently selected Azure Active Directory (AAD) tenant and Azure subscription.</span></span>

1. <span data-ttu-id="4ac82-106">Во-первых toopopulate hello список клиентов показано далее tooyour username, hello сайта выясняется, из Azure какие клиенты AAD, вы принадлежите.</span><span class="sxs-lookup"><span data-stu-id="4ac82-106">First, toopopulate hello list of tenants seen next tooyour username, hello site finds out from Azure which AAD tenants you belong to.</span></span> <span data-ttu-id="4ac82-107">В настоящее время hello сайта только могут получить токены пользователя для одного клиента одновременно.</span><span class="sxs-lookup"><span data-stu-id="4ac82-107">Currently, hello site can only obtain user tokens for one tenant at a time.</span></span> <span data-ttu-id="4ac82-108">Таким образом при переключении клиентов с помощью раскрывающегося списка hello в правом верхнем углу hello сайта hello входе вы toothat клиента tooobtain hello токены для этого клиента.</span><span class="sxs-lookup"><span data-stu-id="4ac82-108">Therefore, when you switch tenants using hello dropdown in hello top right corner, hello site logs you in toothat tenant tooobtain hello tokens for that tenant.</span></span>

2. <span data-ttu-id="4ac82-109">После этого сайта hello выясняется, из подписки, которые связаны с hello выбранного клиента Azure.</span><span class="sxs-lookup"><span data-stu-id="4ac82-109">Next, hello site finds out from Azure which subscriptions you have associated with hello selected tenant.</span></span> <span data-ttu-id="4ac82-110">Вы видите hello доступные подписки, при создании новых предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="4ac82-110">You see hello available subscriptions when you create a new preconfigured solution.</span></span>

3. <span data-ttu-id="4ac82-111">Наконец hello сайта получает все ресурсы hello в подписках hello и группы ресурсов отмечен как предварительно настроенных решений и заполняет hello плитки на домашней странице приветствия.</span><span class="sxs-lookup"><span data-stu-id="4ac82-111">Finally, hello site retrieves all hello resources in hello subscriptions and resource groups tagged as preconfigured solutions and populates hello tiles on hello home page.</span></span>

<span data-ttu-id="4ac82-112">Hello в следующих разделах описаны hello ролей, управляющих доступа toohello предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="4ac82-112">hello following sections describe hello roles that control access toohello preconfigured solutions.</span></span>

## <a name="aad-roles"></a><span data-ttu-id="4ac82-113">Роли AAD</span><span class="sxs-lookup"><span data-stu-id="4ac82-113">AAD roles</span></span>

<span data-ttu-id="4ac82-114">роли AAD Hello hello возможность подготовки предварительно настроенных решений для управления пользователями в предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="4ac82-114">hello AAD roles control hello ability provision preconfigured solutions and manage users in a preconfigured solution.</span></span>

<span data-ttu-id="4ac82-115">Дополнительные сведения о ролях администратора в AAD см. в статье [Назначение ролей администратора в Azure AD][lnk-aad-admin].</span><span class="sxs-lookup"><span data-stu-id="4ac82-115">You can find more information about administrator roles in AAD in [Assigning administrator roles in Azure AD][lnk-aad-admin].</span></span> <span data-ttu-id="4ac82-116">Hello текущего статье основное внимание уделяется hello **глобального администратора** и hello **пользователя** ролей каталога, как используется hello предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="4ac82-116">hello current article focuses on hello **Global Administrator** and hello **User** directory roles as used by hello preconfigured solutions.</span></span>

### <a name="global-administrator"></a><span data-ttu-id="4ac82-117">Глобальный администратор</span><span class="sxs-lookup"><span data-stu-id="4ac82-117">Global administrator</span></span>

<span data-ttu-id="4ac82-118">В одном клиенте AAD может быть несколько глобальных администраторов.</span><span class="sxs-lookup"><span data-stu-id="4ac82-118">There can be many global administrators per AAD tenant:</span></span>

* <span data-ttu-id="4ac82-119">При создании клиент AAD, вы, по умолчанию hello глобального администратора из этого клиента.</span><span class="sxs-lookup"><span data-stu-id="4ac82-119">When you create an AAD tenant, you are by default hello global administrator of that tenant.</span></span>
* <span data-ttu-id="4ac82-120">глобальный администратор Hello можно подготовить предварительно настроенных решений и назначается **администратора** роли для приложения hello в свой клиент AAD.</span><span class="sxs-lookup"><span data-stu-id="4ac82-120">hello global administrator can provision a preconfigured solution and is assigned an **Admin** role for hello application inside their AAD tenant.</span></span>
* <span data-ttu-id="4ac82-121">Если другой пользователь в hello же клиента AAD создается приложение, роль по умолчанию hello предоставил — глобальный администратор toohello **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="4ac82-121">If another user in hello same AAD tenant creates an application, hello default role granted toohello global administrator is **ReadOnly**.</span></span>
* <span data-ttu-id="4ac82-122">Глобальный администратор может назначить tooroles пользователей для приложений, использующих hello [портал Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="4ac82-122">A global administrator can assign users tooroles for applications using hello [Azure portal][lnk-portal].</span></span>

### <a name="domain-user"></a><span data-ttu-id="4ac82-123">Пользователь домена</span><span class="sxs-lookup"><span data-stu-id="4ac82-123">Domain user</span></span>

<span data-ttu-id="4ac82-124">На каждый клиент AAD может приходиться много пользователей домена.</span><span class="sxs-lookup"><span data-stu-id="4ac82-124">There can be many domain users per AAD tenant:</span></span>

* <span data-ttu-id="4ac82-125">Пользователь домена можно подготовить предварительно настроенных решений по hello [azureiotsuite.com] [ lnk-azureiotsuite] сайта.</span><span class="sxs-lookup"><span data-stu-id="4ac82-125">A domain user can provision a preconfigured solution through hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="4ac82-126">По умолчанию, пользователь домена hello предоставляется hello **администратора** роли в hello подготовить приложение.</span><span class="sxs-lookup"><span data-stu-id="4ac82-126">By default, hello domain user is granted hello **Admin** role in hello provisioned application.</span></span>
* <span data-ttu-id="4ac82-127">Пользователь домена может создавать приложения с помощью скрипт build.cmd hello в hello [azure iot удаленного мониторинга][lnk-rm-github-repo], [azure-iot — диагностическое обслуживание] [ lnk-pm-github-repo], или [-iot подключен фабрики azure] [ lnk-cf-github-repo] репозитория.</span><span class="sxs-lookup"><span data-stu-id="4ac82-127">A domain user can create an application using hello build.cmd script in hello [azure-iot-remote-monitoring][lnk-rm-github-repo],  [azure-iot-predictive-maintenance][lnk-pm-github-repo], or [azure-iot-connected-factory][lnk-cf-github-repo] repository.</span></span> <span data-ttu-id="4ac82-128">Однако роль по умолчанию hello предоставлено является пользователем домена toohello **ReadOnly**, так как пользователь домена не имеет разрешений роли tooassign.</span><span class="sxs-lookup"><span data-stu-id="4ac82-128">However, hello default role granted toohello domain user is **ReadOnly**, because a domain user does not have permission tooassign roles.</span></span>
* <span data-ttu-id="4ac82-129">Если другой пользователь в клиенте AAD hello создается приложение, пользователь домена hello назначается hello **ReadOnly** роли по умолчанию для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="4ac82-129">If another user in hello AAD tenant creates an application, hello domain user is assigned hello **ReadOnly** role by default for that application.</span></span>
* <span data-ttu-id="4ac82-130">Пользователь домена не может назначать роли для приложений, поэтому он не может добавлять пользователей к ролям или присваивать пользователям роли для приложения, даже если он подготовил это приложение.</span><span class="sxs-lookup"><span data-stu-id="4ac82-130">A domain user cannot assign roles for applications; therefore a domain user cannot add users or roles for users for an application even if they provisioned it.</span></span>

### <a name="guest-user"></a><span data-ttu-id="4ac82-131">Гостевой пользователь</span><span class="sxs-lookup"><span data-stu-id="4ac82-131">Guest User</span></span>

<span data-ttu-id="4ac82-132">В одном клиенте AAD может быть много гостевых пользователей.</span><span class="sxs-lookup"><span data-stu-id="4ac82-132">There can be many guest users per AAD tenant.</span></span> <span data-ttu-id="4ac82-133">Гостевые пользователи обладают ограниченным набором прав в клиенте AAD hello.</span><span class="sxs-lookup"><span data-stu-id="4ac82-133">Guest users have a limited set of rights in hello AAD tenant.</span></span> <span data-ttu-id="4ac82-134">В результате гостевых пользователей не удается подготовить предварительно настроенных решений в клиенте AAD hello.</span><span class="sxs-lookup"><span data-stu-id="4ac82-134">As a result, guest users cannot provision a preconfigured solution in hello AAD tenant.</span></span>

<span data-ttu-id="4ac82-135">Дополнительные сведения о пользователях и ролях в Azure Active Directory см. в разделе hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="4ac82-135">For more information about users and roles in AAD, see hello following resources:</span></span>

* <span data-ttu-id="4ac82-136">[Добавление новых пользователей или пользователей с учетными записями Майкрософт в Azure Active Directory][lnk-create-edit-users]</span><span class="sxs-lookup"><span data-stu-id="4ac82-136">[Create users in Azure AD][lnk-create-edit-users]</span></span>
* <span data-ttu-id="4ac82-137">[Назначить пользователей tooapps][lnk-assign-app-roles]</span><span class="sxs-lookup"><span data-stu-id="4ac82-137">[Assign users tooapps][lnk-assign-app-roles]</span></span>

## <a name="azure-subscription-administrator-roles"></a><span data-ttu-id="4ac82-138">Роли администратора подписки Azure</span><span class="sxs-lookup"><span data-stu-id="4ac82-138">Azure subscription administrator roles</span></span>

<span data-ttu-id="4ac82-139">роли администратора Azure Hello управлять toomap возможность hello клиент tooan AD подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="4ac82-139">hello Azure admin roles control hello ability toomap an Azure subscription tooan AD tenant.</span></span>

<span data-ttu-id="4ac82-140">Дополнительные сведения о роли администратора Azure hello в статье hello [как tooadd или изменить Соадминистратор Azure, администратор службы и учетной записи администратора][lnk-admin-roles].</span><span class="sxs-lookup"><span data-stu-id="4ac82-140">Find out more about hello Azure admin roles in hello article [How tooadd or change Azure Co-Administrator, Service Administrator, and Account Administrator][lnk-admin-roles].</span></span>

## <a name="application-roles"></a><span data-ttu-id="4ac82-141">Роли приложений</span><span class="sxs-lookup"><span data-stu-id="4ac82-141">Application roles</span></span>

<span data-ttu-id="4ac82-142">роли приложения Hello управления доступа toodevices предварительно настроенного решения.</span><span class="sxs-lookup"><span data-stu-id="4ac82-142">hello application roles control access toodevices in your preconfigured solution.</span></span>

<span data-ttu-id="4ac82-143">В подготовленном приложении существует две определенные и одна неявная роль.</span><span class="sxs-lookup"><span data-stu-id="4ac82-143">There are two defined roles and one implicit role defined in a provisioned application:</span></span>

* <span data-ttu-id="4ac82-144">**Администрирование:** имеет полный доступ tooadd, управление, удаление устройств и изменить параметры.</span><span class="sxs-lookup"><span data-stu-id="4ac82-144">**Admin:** Has full control tooadd, manage, remove devices, and modify settings.</span></span>
* <span data-ttu-id="4ac82-145">**Только для чтения.** Просмотр устройств, правил, действий, заданий и телеметрии.</span><span class="sxs-lookup"><span data-stu-id="4ac82-145">**ReadOnly:** Can view devices, rules, actions, jobs, and telemetry.</span></span>

<span data-ttu-id="4ac82-146">Можно найти hello разрешения назначены роли tooeach в hello [RolePermissions.cs] [ lnk-resource-cs] исходный файл.</span><span class="sxs-lookup"><span data-stu-id="4ac82-146">You can find hello permissions assigned tooeach role in hello [RolePermissions.cs][lnk-resource-cs] source file.</span></span>

### <a name="changing-application-roles-for-a-user"></a><span data-ttu-id="4ac82-147">Изменение ролей приложений для пользователя</span><span class="sxs-lookup"><span data-stu-id="4ac82-147">Changing application roles for a user</span></span>

<span data-ttu-id="4ac82-148">Можно использовать следующие процедуры toomake пользователя в Active Directory администратор предварительно настроенного решения hello.</span><span class="sxs-lookup"><span data-stu-id="4ac82-148">You can use hello following procedure toomake a user in your Active Directory an administrator of your preconfigured solution.</span></span>

<span data-ttu-id="4ac82-149">Должен быть toochange роли глобального администратора AAD для пользователя:</span><span class="sxs-lookup"><span data-stu-id="4ac82-149">You must be an AAD global administrator toochange roles for a user:</span></span>

1. <span data-ttu-id="4ac82-150">Go toohello [портал Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="4ac82-150">Go toohello [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="4ac82-151">Выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4ac82-151">Select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="4ac82-152">Убедитесь, что вы используете directory hello, выбранное на azureiotsuite.com при подготовке решения.</span><span class="sxs-lookup"><span data-stu-id="4ac82-152">Make sure you are using hello directory you chose on azureiotsuite.com when you provisioned your solution.</span></span> <span data-ttu-id="4ac82-153">Если у вас несколько каталогов, связанных с подпиской, можно переключаться между их, если щелкнуть имя учетной записи в hello правой верхней части портала hello.</span><span class="sxs-lookup"><span data-stu-id="4ac82-153">If you have multiple directories associated with your subscription, you can switch between them if you click your account name at hello top-right of hello portal.</span></span>
4. <span data-ttu-id="4ac82-154">Щелкните **Корпоративные приложения**, а затем **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ac82-154">Click **Enterprise applications**, then **All applications**.</span></span>
4. <span data-ttu-id="4ac82-155">Отобразите **все приложения** с состоянием **Любой**.</span><span class="sxs-lookup"><span data-stu-id="4ac82-155">Show **All applications** with **Any** status.</span></span> <span data-ttu-id="4ac82-156">Затем найдите приложения с именем вашего предварительно настроенного решения.</span><span class="sxs-lookup"><span data-stu-id="4ac82-156">Then search for an application with name of your preconfigured solution.</span></span>
5. <span data-ttu-id="4ac82-157">Щелкните имя приложения hello, совпадающим с именем предварительно настроенных решений hello.</span><span class="sxs-lookup"><span data-stu-id="4ac82-157">Click hello name of hello application that matches your preconfigured solution name.</span></span>
6. <span data-ttu-id="4ac82-158">Щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="4ac82-158">Click **Users and groups**.</span></span>
7. <span data-ttu-id="4ac82-159">Выберите пользователя hello требуется tooswitch ролей.</span><span class="sxs-lookup"><span data-stu-id="4ac82-159">Select hello user you want tooswitch roles.</span></span>
8. <span data-ttu-id="4ac82-160">Нажмите кнопку **назначить** и роли выберите hello (такие как **администратора**) хотелось бы tooassign toohello пользователя, щелкните флажок hello.</span><span class="sxs-lookup"><span data-stu-id="4ac82-160">Click **Assign** and select hello role (such as **Admin**) you'd like tooassign toohello user, click hello check mark.</span></span>

## <a name="faq"></a><span data-ttu-id="4ac82-161">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="4ac82-161">FAQ</span></span>

### <a name="im-a-service-administrator-and-id-like-toochange-hello-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a><span data-ttu-id="4ac82-162">Я администратором службы и как toochange hello каталогов сопоставление между подпиской и конкретного клиента AAD.</span><span class="sxs-lookup"><span data-stu-id="4ac82-162">I'm a service administrator and I'd like toochange hello directory mapping between my subscription and a specific AAD tenant.</span></span> <span data-ttu-id="4ac82-163">Как выполнить эту задачу?</span><span class="sxs-lookup"><span data-stu-id="4ac82-163">How do I complete this task?</span></span>

1. <span data-ttu-id="4ac82-164">Go toohello [классический портал Azure][lnk-classic-portal], нажмите кнопку **параметры** в списке hello служб hello левой стороны.</span><span class="sxs-lookup"><span data-stu-id="4ac82-164">Go toohello [Azure classic portal][lnk-classic-portal], click **Settings** in hello list of services on hello left-hand side.</span></span>
2. <span data-ttu-id="4ac82-165">Выберите подписку hello, которой вы хотите сопоставление каталога toochange hello в.</span><span class="sxs-lookup"><span data-stu-id="4ac82-165">Select hello subscription you'd like toochange hello directory mapping to.</span></span>
3. <span data-ttu-id="4ac82-166">Щелкните **Изменить каталог**.</span><span class="sxs-lookup"><span data-stu-id="4ac82-166">Click **Edit Directory**.</span></span>
4. <span data-ttu-id="4ac82-167">Выберите hello **каталога** хотелось бы toouse в раскрывающемся списке hello.</span><span class="sxs-lookup"><span data-stu-id="4ac82-167">Select hello **Directory** you would like toouse in hello dropdown.</span></span> <span data-ttu-id="4ac82-168">Щелкните стрелку «вперед» hello.</span><span class="sxs-lookup"><span data-stu-id="4ac82-168">Click hello forward arrow.</span></span>
5. <span data-ttu-id="4ac82-169">Подтвердите сопоставление каталога hello и затронутых соадминистраторов.</span><span class="sxs-lookup"><span data-stu-id="4ac82-169">Confirm hello directory mapping and affected co-administrators.</span></span> <span data-ttu-id="4ac82-170">При перемещении из другого каталога, удаляются все соадминистраторы из исходного каталога hello hello.</span><span class="sxs-lookup"><span data-stu-id="4ac82-170">If you are moving from another directory, all hello co-administrators from hello original directory are removed.</span></span>

### <a name="im-a-domain-usermember-on-hello-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a><span data-ttu-id="4ac82-171">Я пользователя или члена домена на приветствия клиента AAD и создадим предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="4ac82-171">I'm a domain user/member on hello AAD tenant and I've created a preconfigured solution.</span></span> <span data-ttu-id="4ac82-172">Как мне получить роль для своего приложения?</span><span class="sxs-lookup"><span data-stu-id="4ac82-172">How do I get assigned a role for my application?</span></span>

<span data-ttu-id="4ac82-173">Попросите toomake глобального администратора вы глобального администратора на hello AAD клиента, а затем назначьте роли toousers самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="4ac82-173">Ask a global administrator toomake you a global administrator on hello AAD tenant and then assign roles toousers yourself.</span></span> <span data-ttu-id="4ac82-174">Кроме того, попросите tooassign глобального администратора вы непосредственно роли.</span><span class="sxs-lookup"><span data-stu-id="4ac82-174">Alternatively, ask a global administrator tooassign you a role directly.</span></span> <span data-ttu-id="4ac82-175">Если вы хотите toochange hello AAD клиента, который был развернут предварительно настроенного решения, см. следующий вопрос hello.</span><span class="sxs-lookup"><span data-stu-id="4ac82-175">If you'd like toochange hello AAD tenant your preconfigured solution has been deployed to, see hello next question.</span></span>

### <a name="how-do-i-switch-hello-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a><span data-ttu-id="4ac82-176">Как переключаться клиента AAD hello назначаются Мой удаленного мониторинга предварительно настроенных решений и приложений?</span><span class="sxs-lookup"><span data-stu-id="4ac82-176">How do I switch hello AAD tenant my remote monitoring preconfigured solution and application are assigned to?</span></span>

<span data-ttu-id="4ac82-177">Можно запустить развернутую облачную службу со страницы <https://github.com/Azure/azure-iot-remote-monitoring> и повторить развертывание в новом клиенте AAD.</span><span class="sxs-lookup"><span data-stu-id="4ac82-177">You can run a cloud deployment from <https://github.com/Azure/azure-iot-remote-monitoring> and redeploy with a newly created AAD tenant.</span></span> <span data-ttu-id="4ac82-178">Поскольку являются, по умолчанию является глобальным администратором при создании клиент AAD имеется tooadd разрешения пользователей и назначить роли пользователей toothose.</span><span class="sxs-lookup"><span data-stu-id="4ac82-178">Because you are, by default, a global administrator when you create an AAD tenant, you have permissions tooadd users and assign roles toothose users.</span></span>

1. <span data-ttu-id="4ac82-179">Создайте каталог AAD в hello [портал Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="4ac82-179">Create an AAD directory in hello [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="4ac82-180">Go слишком<https://github.com/Azure/azure-iot-remote-monitoring>.</span><span class="sxs-lookup"><span data-stu-id="4ac82-180">Go too<https://github.com/Azure/azure-iot-remote-monitoring>.</span></span>
3. <span data-ttu-id="4ac82-181">Выполните команду `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (например, `build.cmd cloud debug myRMSolution`).</span><span class="sxs-lookup"><span data-stu-id="4ac82-181">Run `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (For example, `build.cmd cloud debug myRMSolution`)</span></span>
4. <span data-ttu-id="4ac82-182">При появлении запроса установите hello **tenantid** toobe клиент только что созданный вместо предыдущего клиента.</span><span class="sxs-lookup"><span data-stu-id="4ac82-182">When prompted, set hello **tenantid** toobe your newly created tenant instead of your previous tenant.</span></span>

### <a name="i-want-toochange-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a><span data-ttu-id="4ac82-183">Я хочу toochange администратором служб или Соадминистратора, войдя в систему с учетной записью работы</span><span class="sxs-lookup"><span data-stu-id="4ac82-183">I want toochange a Service Administrator or Co-Administrator when logged in with an organisational account</span></span>

<span data-ttu-id="4ac82-184">См. в статье поддержка hello [изменение администратора службы и Соадминистратор, войдя в систему с учетной записью работы][lnk-service-admins].</span><span class="sxs-lookup"><span data-stu-id="4ac82-184">See hello support article [Changing Service Administrator and Co-Administrator when logged in with an organisational account][lnk-service-admins].</span></span>

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-hello-proper-permissions-toocreate-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a><span data-ttu-id="4ac82-185">Почему появляется ошибка</span><span class="sxs-lookup"><span data-stu-id="4ac82-185">Why am I seeing this error?</span></span> <span data-ttu-id="4ac82-186">«Ваша учетная запись не имеет toocreate hello соответствующие разрешения решения.</span><span class="sxs-lookup"><span data-stu-id="4ac82-186">"Your account does not have hello proper permissions toocreate a solution.</span></span> <span data-ttu-id="4ac82-187">Обратитесь к администратору учетной записи или попробуйте использовать другую учетную запись»</span><span class="sxs-lookup"><span data-stu-id="4ac82-187">Please check with your account administrator or try with a different account."</span></span>

<span data-ttu-id="4ac82-188">Рассмотрим следующие схемы рекомендации hello.</span><span class="sxs-lookup"><span data-stu-id="4ac82-188">Look at hello following diagram for guidance:</span></span>

![][img-flowchart]

> [!NOTE]
> <span data-ttu-id="4ac82-189">При продолжении toosee hello ошибка после проверки глобального администратора в клиенте AAD hello и соадминистратор для подписки hello, попросите администратора учетной записи удаления пользователя hello и переназначить необходимых разрешений в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="4ac82-189">If you continue toosee hello error after validating you are a global administrator on hello AAD tenant and a co-administrator on hello subscription, have your account administrator remove hello user and reassign necessary permissions in this order.</span></span> <span data-ttu-id="4ac82-190">Во-первых добавить пользователя hello как глобальный администратор, а затем добавьте пользователя в качестве соадминистратора на hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="4ac82-190">First, add hello user as a global administrator and then add user as a co-administrator on hello Azure subscription.</span></span> <span data-ttu-id="4ac82-191">Если проблемы не удается устранить, обратитесь в службу [справки и поддержки][lnk-help-support].</span><span class="sxs-lookup"><span data-stu-id="4ac82-191">If issues persist, contact [Help & Support][lnk-help-support].</span></span>

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-toocreate-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a><span data-ttu-id="4ac82-192">Почему эта ошибка появляется при наличии подписки Azure?</span><span class="sxs-lookup"><span data-stu-id="4ac82-192">Why am I seeing this error when I have an Azure subscription?</span></span> <span data-ttu-id="4ac82-193">«Подписка Azure является обязательным toocreate предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="4ac82-193">"An Azure subscription is required toocreate pre-configured solutions.</span></span> <span data-ttu-id="4ac82-194">Вы можете создать бесплатную пробную учетную запись всего за несколько минут".</span><span class="sxs-lookup"><span data-stu-id="4ac82-194">You can create a free trial account in just a couple of minutes."</span></span>

<span data-ttu-id="4ac82-195">Если точно известно, что у вас есть подписка Azure, проверить сопоставление для вашей подписки клиентов hello и убедитесь, что клиент правильно hello выбран в раскрывающемся списке hello.</span><span class="sxs-lookup"><span data-stu-id="4ac82-195">If you're certain you have an Azure subscription, validate hello tenant mapping for your subscription and ensure hello correct tenant is selected in hello dropdown.</span></span> <span data-ttu-id="4ac82-196">Если были проверены hello требуемого правильность клиента, выполните hello предшествующий схемы и проверить сопоставление hello о подписке и этого клиента AAD.</span><span class="sxs-lookup"><span data-stu-id="4ac82-196">If you’ve validated hello desired tenant is correct, follow hello preceding diagram and validate hello mapping of your subscription and this AAD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ac82-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4ac82-197">Next steps</span></span>
<span data-ttu-id="4ac82-198">toocontinue изучения IoT Suite см. способы [настроить предварительно настроенных решений][lnk-customize].</span><span class="sxs-lookup"><span data-stu-id="4ac82-198">toocontinue learning about IoT Suite, see how you can [customize a preconfigured solution][lnk-customize].</span></span>

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
