---
title: "aaaCreate участника-службы для Azure стека | Документы Microsoft"
description: "Описывает способ toocreate нового участника службы, который может использоваться с элементом управления доступом на основе hello в tooresources доступа toomanage диспетчера ресурсов Azure."
services: azure-resource-manager
documentationcenter: na
author: heathl17
manager: byronr
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: helaw
ms.openlocfilehash: f090ceed941abe9255bc35ec966bc43df3bb2955
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="provide-applications-access-tooazure-stack"></a><span data-ttu-id="1ead7-103">Предоставить доступ приложений tooAzure стека</span><span class="sxs-lookup"><span data-stu-id="1ead7-103">Provide applications access tooAzure Stack</span></span>
<span data-ttu-id="1ead7-104">При приложения должен toodeploy доступа или настроить ресурсами с помощью диспетчера ресурсов Azure в стек Azure, вы создаете субъект-служба, являющийся учетных данных для приложения.</span><span class="sxs-lookup"><span data-stu-id="1ead7-104">When an application needs access toodeploy or configure resources through Azure Resource Manager in Azure Stack, you create a service principal, which is a credential for your application.</span></span>  <span data-ttu-id="1ead7-105">Затем можно делегировать только hello необходимые разрешения toothat участника-службы.</span><span class="sxs-lookup"><span data-stu-id="1ead7-105">You can then delegate only hello necessary permissions toothat service principal.</span></span>  

<span data-ttu-id="1ead7-106">Например, возможно, средство управления конфигурации, которое использует Azure Resource Manager tooinventory ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="1ead7-106">As an example, you may have a configuration management tool that uses Azure Resource Manager tooinventory Azure resources.</span></span>  <span data-ttu-id="1ead7-107">В этом случае можно создать участника службы, предоставления роли участника службы toothat чтения hello и ограничить hello конфигурации управления средство tooread доступ только.</span><span class="sxs-lookup"><span data-stu-id="1ead7-107">In this scenario, you can create a service principal, grant hello reader role toothat service principal, and limit hello configuration management tool tooread-only access.</span></span> 

<span data-ttu-id="1ead7-108">Субъекты-службы, которые приложение hello предпочтительным toorunning в своих собственных учетных данных, так как:</span><span class="sxs-lookup"><span data-stu-id="1ead7-108">Service principals are preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="1ead7-109">Можно назначить участника службы toohello разрешения, отличаются от разрешений учетной записи.</span><span class="sxs-lookup"><span data-stu-id="1ead7-109">You can assign permissions toohello service principal that are different than your own account permissions.</span></span> <span data-ttu-id="1ead7-110">Как правило эти разрешения являются ограниченными tooexactly какие hello приложению toodo.</span><span class="sxs-lookup"><span data-stu-id="1ead7-110">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="1ead7-111">У вас приложение hello toochange учетные данные при изменении ваши обязанности.</span><span class="sxs-lookup"><span data-stu-id="1ead7-111">You do not have toochange hello app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="1ead7-112">При выполнении сценария автоматической можно использовать проверку подлинности сертификата tooautomate.</span><span class="sxs-lookup"><span data-stu-id="1ead7-112">You can use a certificate tooautomate authentication when executing an unattended script.</span></span>  

## <a name="getting-started"></a><span data-ttu-id="1ead7-113">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="1ead7-113">Getting started</span></span>

<span data-ttu-id="1ead7-114">В зависимости от способа развертывания Azure стека начните с создания участника службы.</span><span class="sxs-lookup"><span data-stu-id="1ead7-114">Depending on how you have deployed Azure Stack, you start by creating a service principal.</span></span>  <span data-ttu-id="1ead7-115">Этот документ поможет создать участника-службы для обоих [Azure Active Directory (Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad) и [Services(AD FS) федерации Active Directory](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="1ead7-115">This document guides you through creating a service principal for both [Azure Active Directory (Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad) and [Active Directory Federation Services(AD FS)](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs).</span></span>  <span data-ttu-id="1ead7-116">После создания hello участника-службы, набор tooboth общие шаги AD FS и Azure Active Directory используются слишком[делегировать разрешения](azure-stack-create-service-principals.md#assign-role-to-service-principal) toohello роли.</span><span class="sxs-lookup"><span data-stu-id="1ead7-116">Once you've created hello service principal, a set of steps common tooboth AD FS and Azure Active Directory are used too[delegate permissions](azure-stack-create-service-principals.md#assign-role-to-service-principal) toohello role.</span></span>     

## <a name="create-service-principal-for-azure-ad"></a><span data-ttu-id="1ead7-117">Создание участника службы для Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ead7-117">Create service principal for Azure AD</span></span>

<span data-ttu-id="1ead7-118">Если вы развернули стек Azure, с помощью Azure AD как хранилище удостоверений hello, можно создать участников службы, так же, как и для Azure.</span><span class="sxs-lookup"><span data-stu-id="1ead7-118">If you've deployed Azure Stack using Azure AD as hello identity store, you can create service principals just like you do for Azure.</span></span>  <span data-ttu-id="1ead7-119">В этом разделе показано, как tooperform hello проходит через портал hello.</span><span class="sxs-lookup"><span data-stu-id="1ead7-119">This section shows you how tooperform hello steps through hello portal.</span></span>  <span data-ttu-id="1ead7-120">Убедитесь, что hello [Azure AD разрешения, необходимые](../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions) перед началом.</span><span class="sxs-lookup"><span data-stu-id="1ead7-120">Check that you have hello [required Azure AD permissions](../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions) before beginning.</span></span>

### <a name="create-service-principal"></a><span data-ttu-id="1ead7-121">Создание субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="1ead7-121">Create service principal</span></span>
<span data-ttu-id="1ead7-122">В этом разделе создается приложение (субъекта-службы) в Azure AD, который будет представлять приложение.</span><span class="sxs-lookup"><span data-stu-id="1ead7-122">In this section, you create an application (service principal) in Azure AD that will represent your application.</span></span>

1. <span data-ttu-id="1ead7-123">Войдите в tooyour учетную запись Azure через hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1ead7-123">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1ead7-124">Выберите **Azure Active Directory** > **регистрации приложения** > **добавить**</span><span class="sxs-lookup"><span data-stu-id="1ead7-124">Select **Azure Active Directory** > **App registrations** > **Add**</span></span>   
3. <span data-ttu-id="1ead7-125">Укажите имя и URL-адрес для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1ead7-125">Provide a name and URL for hello application.</span></span> <span data-ttu-id="1ead7-126">Выберите либо **веб-приложения и API** или **собственного** для типа приложения hello требуется toocreate.</span><span class="sxs-lookup"><span data-stu-id="1ead7-126">Select either **Web app / API** or **Native** for hello type of application you want toocreate.</span></span> <span data-ttu-id="1ead7-127">После задания значения hello, выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="1ead7-127">After setting hello values, select **Create**.</span></span>

<span data-ttu-id="1ead7-128">Вы создали субъекта-службы для приложения.</span><span class="sxs-lookup"><span data-stu-id="1ead7-128">You have created a service principal for your application.</span></span>

### <a name="get-credentials"></a><span data-ttu-id="1ead7-129">Получить учетные данные</span><span class="sxs-lookup"><span data-stu-id="1ead7-129">Get credentials</span></span>
<span data-ttu-id="1ead7-130">Программным способом входа в систему используется идентификатор hello для приложения и ключ проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="1ead7-130">When programmatically logging in, you use hello ID for your application and an authentication key.</span></span> <span data-ttu-id="1ead7-131">те значения, tooget hello используйте следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="1ead7-131">tooget those values, use hello following steps:</span></span>

1. <span data-ttu-id="1ead7-132">В Active Directory в разделе **регистрации приложений** выберите нужное приложение.</span><span class="sxs-lookup"><span data-stu-id="1ead7-132">From **App registrations** in Active Directory, select your application.</span></span>

2. <span data-ttu-id="1ead7-133">Копировать hello **идентификатор приложения** и сохранить ее в коде приложения.</span><span class="sxs-lookup"><span data-stu-id="1ead7-133">Copy hello **Application ID** and store it in your application code.</span></span> <span data-ttu-id="1ead7-134">Здравствуйте, приложения hello [образцы приложений](#sample-applications) значение toothis, что идентификатор hello клиента см. раздел.</span><span class="sxs-lookup"><span data-stu-id="1ead7-134">hello applications in hello [sample applications](#sample-applications) section refer toothis value as hello client id.</span></span>

     ![Идентификатор клиента](./media/azure-stack-create-service-principal/image12.png)
3. <span data-ttu-id="1ead7-136">Выберите ключ проверки подлинности toogenerate **ключей**.</span><span class="sxs-lookup"><span data-stu-id="1ead7-136">toogenerate an authentication key, select **Keys**.</span></span>

4. <span data-ttu-id="1ead7-137">Введите описание ключа hello и длительность для ключа hello.</span><span class="sxs-lookup"><span data-stu-id="1ead7-137">Provide a description of hello key, and a duration for hello key.</span></span> <span data-ttu-id="1ead7-138">Затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1ead7-138">When done, select **Save**.</span></span>

<span data-ttu-id="1ead7-139">После сохранения ключа hello, отображается значение hello hello ключа.</span><span class="sxs-lookup"><span data-stu-id="1ead7-139">After saving hello key, hello value of hello key is displayed.</span></span> <span data-ttu-id="1ead7-140">Скопируйте это значение невозможно, поскольку ключ может tooretrieve hello позже.</span><span class="sxs-lookup"><span data-stu-id="1ead7-140">Copy this value because you are not able tooretrieve hello key later.</span></span> <span data-ttu-id="1ead7-141">Значение ключа hello предоставить toosign идентификатор приложения hello как приложение hello.</span><span class="sxs-lookup"><span data-stu-id="1ead7-141">You provide hello key value with hello application ID toosign as hello application.</span></span> <span data-ttu-id="1ead7-142">Сохраните значение ключа hello, где приложение может вернуть их.</span><span class="sxs-lookup"><span data-stu-id="1ead7-142">Store hello key value where your application can retrieve it.</span></span>

![сохраненный ключ](./media/azure-stack-create-service-principal/image15.png)


<span data-ttu-id="1ead7-144">После завершения продолжить слишком[назначение роли приложения](azure-stack-create-service-principals.md#assign-role-to-service-principal).</span><span class="sxs-lookup"><span data-stu-id="1ead7-144">Once complete, proceed too[assigning your application a role](azure-stack-create-service-principals.md#assign-role-to-service-principal).</span></span>

## <a name="create-service-principal-for-ad-fs"></a><span data-ttu-id="1ead7-145">Создание участника службы для AD FS</span><span class="sxs-lookup"><span data-stu-id="1ead7-145">Create service principal for AD FS</span></span>
<span data-ttu-id="1ead7-146">При развертывании Azure стека с AD FS можно использовать PowerShell toocreate участника службы, назначение роли для доступа и входа с PowerShell, с использованием указанного удостоверения.</span><span class="sxs-lookup"><span data-stu-id="1ead7-146">If you have deployed Azure Stack with AD FS, you can use PowerShell toocreate a service principal, assign a role for access, and sign in from PowerShell using that identity.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="1ead7-147">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="1ead7-147">Before you begin</span></span>

[<span data-ttu-id="1ead7-148">Загрузите необходимые toowork hello средства с Azure стека tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="1ead7-148">Download hello tools required toowork with Azure Stack tooyour local computer.</span></span>](azure-stack-powershell-download.md)

### <a name="import-hello-identity-powershell-module"></a><span data-ttu-id="1ead7-149">Модуль PowerShell идентификаторов hello импорта</span><span class="sxs-lookup"><span data-stu-id="1ead7-149">Import hello Identity PowerShell module</span></span>
<span data-ttu-id="1ead7-150">После загрузки средства hello, перейдите в папку toohello загрузки и импорт модуля PowerShell идентификаторов hello с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1ead7-150">After you download hello tools, navigate toohello downloaded folder and import hello Identity PowerShell module by using hello following command:</span></span>

```PowerShell
Import-Module .\Identity\AzureStack.Identity.psm1
```

<span data-ttu-id="1ead7-151">При импорте модуля hello, может появиться сообщение об ошибке: «AzureStack.Connect.psm1 не имеет цифровой подписи.</span><span class="sxs-lookup"><span data-stu-id="1ead7-151">When you import hello module, you may receive an error that says “AzureStack.Connect.psm1 is not digitally signed.</span></span> <span data-ttu-id="1ead7-152">Hello сценарий не будет выполняться в системе hello».</span><span class="sxs-lookup"><span data-stu-id="1ead7-152">hello script will not execute on hello system”.</span></span> <span data-ttu-id="1ead7-153">tooresolve эту проблему, задайте tooallow политики выполнения сценария hello, выполнив следующую команду в сеансе PowerShell с повышенными привилегиями hello:</span><span class="sxs-lookup"><span data-stu-id="1ead7-153">tooresolve this issue, you can set execution policy tooallow running hello script with hello following command in an elevated PowerShell session:</span></span>

```PowerShell
Set-ExecutionPolicy Unrestricted
```

### <a name="create-hello-service-principal"></a><span data-ttu-id="1ead7-154">Создать hello участника-службы</span><span class="sxs-lookup"><span data-stu-id="1ead7-154">Create hello service principal</span></span>
<span data-ttu-id="1ead7-155">Можно создать субъект-службу, выполнив следующие hello команды, выполняющего убедиться, что hello tooupdate *DisplayName* параметр:</span><span class="sxs-lookup"><span data-stu-id="1ead7-155">You can create a Service Principal by executing hello following command, making sure tooupdate hello *DisplayName* parameter:</span></span>
```powershell
$servicePrincipal = New-AzSADGraphServicePrincipal `
 -DisplayName "<YourServicePrincipalName>" `
 -AdminCredential $(Get-Credential) `
 -AdfsMachineName "AZS-ADFS01" `
 -Verbose
```
### <a name="assign-a-role"></a><span data-ttu-id="1ead7-156">Назначение роли</span><span class="sxs-lookup"><span data-stu-id="1ead7-156">Assign a role</span></span>
<span data-ttu-id="1ead7-157">Один раз hello при создании участника службы, необходимо [назначить его tooa роли](azure-stack-create-service-principals.md#assign-role-to-service-principal)</span><span class="sxs-lookup"><span data-stu-id="1ead7-157">Once hello Service Principal is created, you must [assign it tooa role](azure-stack-create-service-principals.md#assign-role-to-service-principal)</span></span>

### <a name="sign-in-through-powershell"></a><span data-ttu-id="1ead7-158">Войти с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ead7-158">Sign in through PowerShell</span></span>
<span data-ttu-id="1ead7-159">После был назначен роли, вы сможете войти в tooAzure стека с помощью субъекта-службы hello с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1ead7-159">Once you've assigned a role, you can sign in tooAzure Stack using hello service principal with hello following command:</span></span>

```powershell
Add-AzureRmAccount -EnvironmentName "<AzureStackEnvironmentName>" `
 -ServicePrincipal `
 -CertificateThumbprint $servicePrincipal.Thumbprint `
 -ApplicationId $servicePrincipal.ApplicationId ` 
 -TenantId $directoryTenantId
```

## <a name="assign-role-tooservice-principal"></a><span data-ttu-id="1ead7-160">Назначение роли участника tooservice</span><span class="sxs-lookup"><span data-stu-id="1ead7-160">Assign role tooservice principal</span></span>
<span data-ttu-id="1ead7-161">tooaccess ресурсам в подписке, необходимо назначить роль tooa приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1ead7-161">tooaccess resources in your subscription, you must assign hello application tooa role.</span></span> <span data-ttu-id="1ead7-162">Решите, какую роль представляет hello нужные разрешения для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1ead7-162">Decide which role represents hello right permissions for hello application.</span></span> <span data-ttu-id="1ead7-163">toolearn о hello доступным ролям, в разделе [RBAC: встроенные роли](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="1ead7-163">toolearn about hello available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="1ead7-164">Можно установить область hello на уровне hello hello подписки, группы ресурсов или ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1ead7-164">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="1ead7-165">Разрешения, наследуемые toolower уровни области действия.</span><span class="sxs-lookup"><span data-stu-id="1ead7-165">Permissions are inherited toolower levels of scope.</span></span> <span data-ttu-id="1ead7-166">Например для добавления роли модуля чтения toohello приложения для группы ресурсов есть может считать группы ресурсов hello и все ресурсы, которые он содержит.</span><span class="sxs-lookup"><span data-stu-id="1ead7-166">For example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains.</span></span>

1. <span data-ttu-id="1ead7-167">На портале Azure стека hello перейти на уровень toohello области, в которых надо tooassign hello приложению.</span><span class="sxs-lookup"><span data-stu-id="1ead7-167">In hello Azure Stack portal, navigate toohello level of scope you wish tooassign hello application to.</span></span> <span data-ttu-id="1ead7-168">Например, tooassign роль в области hello подписки, выберите **подписки**.</span><span class="sxs-lookup"><span data-stu-id="1ead7-168">For example, tooassign a role at hello subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="1ead7-169">Или же вы можете выбрать группу ресурсов либо отдельный ресурс.</span><span class="sxs-lookup"><span data-stu-id="1ead7-169">You could instead select a resource group or resource.</span></span>

2. <span data-ttu-id="1ead7-170">Выберите приложение hello tooassign hello определенной подписки (группа ресурсов или ресурсов) для.</span><span class="sxs-lookup"><span data-stu-id="1ead7-170">Select hello particular subscription (resource group or resource) tooassign hello application to.</span></span>

     ![выбрать подписку для назначения](./media/azure-stack-create-service-principal/image16.png)

3. <span data-ttu-id="1ead7-172">Выберите **Управление доступом (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="1ead7-172">Select **Access Control (IAM)**.</span></span>

     ![выбрать доступ](./media/azure-stack-create-service-principal/image17.png)

4. <span data-ttu-id="1ead7-174">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1ead7-174">Select **Add**.</span></span>

5. <span data-ttu-id="1ead7-175">Выберите роль hello нужно tooassign toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="1ead7-175">Select hello role you wish tooassign toohello application.</span></span>

6. <span data-ttu-id="1ead7-176">Найдите приложение и выберите его.</span><span class="sxs-lookup"><span data-stu-id="1ead7-176">Search for your application, and select it.</span></span>

7. <span data-ttu-id="1ead7-177">Выберите **ОК** toofinish назначение роли hello.</span><span class="sxs-lookup"><span data-stu-id="1ead7-177">Select **OK** toofinish assigning hello role.</span></span> <span data-ttu-id="1ead7-178">Вы видите приложение hello списка пользователей, назначенных роли tooa для данной области.</span><span class="sxs-lookup"><span data-stu-id="1ead7-178">You see your application in hello list of users assigned tooa role for that scope.</span></span>

<span data-ttu-id="1ead7-179">Теперь, создания участника службы и назначить роль, можно начать с помощью этого в рамках вашего приложения tooaccess ресурсы Azure стека.</span><span class="sxs-lookup"><span data-stu-id="1ead7-179">Now that you've created a service principal and assigned a role, you can begin using this within your application tooaccess Azure Stack resources.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="1ead7-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1ead7-180">Next steps</span></span>

<span data-ttu-id="1ead7-181">[Добавление пользователей для служб федерации Active Directory](azure-stack-add-users-adfs.md)
[управлять разрешениями пользователей](azure-stack-manage-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="1ead7-181">[Add users for ADFS](azure-stack-add-users-adfs.md)
[Manage user permissions](azure-stack-manage-permissions.md)</span></span>