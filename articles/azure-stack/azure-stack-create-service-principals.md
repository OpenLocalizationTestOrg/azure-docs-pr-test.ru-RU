---
title: "Создание субъекта-службы для Azure стека | Документы Microsoft"
description: "В этой статье описывается создание нового участника службы, который может использоваться для управления доступом к ресурсам с помощью элемента управления доступом на основе ролей в диспетчере ресурсов Azure."
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
ms.openlocfilehash: b3992b296d5a999601eb69b071559f9d37dacf8f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="provide-applications-access-to-azure-stack"></a><span data-ttu-id="e1db5-103">Предоставление доступа приложений к стек Azure</span><span class="sxs-lookup"><span data-stu-id="e1db5-103">Provide applications access to Azure Stack</span></span>
<span data-ttu-id="e1db5-104">При приложению доступ для развертывания или настройте ресурсами с помощью диспетчера ресурсов Azure в стек Azure, вы создаете субъект-служба, являющийся учетных данных для приложения.</span><span class="sxs-lookup"><span data-stu-id="e1db5-104">When an application needs access to deploy or configure resources through Azure Resource Manager in Azure Stack, you create a service principal, which is a credential for your application.</span></span>  <span data-ttu-id="e1db5-105">Затем можно делегировать только необходимые разрешения для этого участника службы.</span><span class="sxs-lookup"><span data-stu-id="e1db5-105">You can then delegate only the necessary permissions to that service principal.</span></span>  

<span data-ttu-id="e1db5-106">Например имеется средство управления конфигурации, которое использует диспетчера ресурсов Azure для инвентаризации ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="e1db5-106">As an example, you may have a configuration management tool that uses Azure Resource Manager to inventory Azure resources.</span></span>  <span data-ttu-id="e1db5-107">В этом случае можно создать участника службы, предоставления роли чтения данных этого участника службы и ограничить средство управления конфигурации для доступа только для чтения.</span><span class="sxs-lookup"><span data-stu-id="e1db5-107">In this scenario, you can create a service principal, grant the reader role to that service principal, and limit the configuration management tool to read-only access.</span></span> 

<span data-ttu-id="e1db5-108">Субъекты-службы предпочтительнее выполнение приложения в своих собственных учетных данных, так как:</span><span class="sxs-lookup"><span data-stu-id="e1db5-108">Service principals are preferable to running the app under your own credentials because:</span></span>

* <span data-ttu-id="e1db5-109">Можно назначить разрешения для участника, отличаются от разрешений учетной записи службы.</span><span class="sxs-lookup"><span data-stu-id="e1db5-109">You can assign permissions to the service principal that are different than your own account permissions.</span></span> <span data-ttu-id="e1db5-110">Как правило, приложение получает именно те разрешения, которые требуются для его работы.</span><span class="sxs-lookup"><span data-stu-id="e1db5-110">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="e1db5-111">Не требуется изменять учетные данные приложения в случае изменения ваших обязанностей.</span><span class="sxs-lookup"><span data-stu-id="e1db5-111">You do not have to change the app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="e1db5-112">Можно использовать сертификат, чтобы автоматизировать аутентификацию при выполнении автоматического сценария.</span><span class="sxs-lookup"><span data-stu-id="e1db5-112">You can use a certificate to automate authentication when executing an unattended script.</span></span>  

## <a name="getting-started"></a><span data-ttu-id="e1db5-113">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="e1db5-113">Getting started</span></span>

<span data-ttu-id="e1db5-114">В зависимости от способа развертывания Azure стека начните с создания участника службы.</span><span class="sxs-lookup"><span data-stu-id="e1db5-114">Depending on how you have deployed Azure Stack, you start by creating a service principal.</span></span>  <span data-ttu-id="e1db5-115">Этот документ поможет создать участника-службы для обоих [Azure Active Directory (Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad) и [Services(AD FS) федерации Active Directory](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="e1db5-115">This document guides you through creating a service principal for both [Azure Active Directory (Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad) and [Active Directory Federation Services(AD FS)](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs).</span></span>  <span data-ttu-id="e1db5-116">После создания участника службы, набор общих шагов в AD FS и Azure Active Directory используются для [делегировать разрешения](azure-stack-create-service-principals.md#assign-role-to-service-principal) к роли.</span><span class="sxs-lookup"><span data-stu-id="e1db5-116">Once you've created the service principal, a set of steps common to both AD FS and Azure Active Directory are used to [delegate permissions](azure-stack-create-service-principals.md#assign-role-to-service-principal) to the role.</span></span>     

## <a name="create-service-principal-for-azure-ad"></a><span data-ttu-id="e1db5-117">Создание участника службы для Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1db5-117">Create service principal for Azure AD</span></span>

<span data-ttu-id="e1db5-118">При развертывании с помощью Azure AD в качестве хранилища идентификаторов стек Azure можно создать участников службы, так же, как и для Azure.</span><span class="sxs-lookup"><span data-stu-id="e1db5-118">If you've deployed Azure Stack using Azure AD as the identity store, you can create service principals just like you do for Azure.</span></span>  <span data-ttu-id="e1db5-119">В этом разделе показано, как выполнять действия на портале.</span><span class="sxs-lookup"><span data-stu-id="e1db5-119">This section shows you how to perform the steps through the portal.</span></span>  <span data-ttu-id="e1db5-120">Убедитесь, что у вас есть [Azure AD разрешения, необходимые](../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions) перед началом.</span><span class="sxs-lookup"><span data-stu-id="e1db5-120">Check that you have the [required Azure AD permissions](../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions) before beginning.</span></span>

### <a name="create-service-principal"></a><span data-ttu-id="e1db5-121">Создание субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="e1db5-121">Create service principal</span></span>
<span data-ttu-id="e1db5-122">В этом разделе создается приложение (субъекта-службы) в Azure AD, который будет представлять приложение.</span><span class="sxs-lookup"><span data-stu-id="e1db5-122">In this section, you create an application (service principal) in Azure AD that will represent your application.</span></span>

1. <span data-ttu-id="e1db5-123">Войдите в учетную запись Azure на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e1db5-123">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e1db5-124">Выберите **Azure Active Directory** > **регистрации приложения** > **добавить**</span><span class="sxs-lookup"><span data-stu-id="e1db5-124">Select **Azure Active Directory** > **App registrations** > **Add**</span></span>   
3. <span data-ttu-id="e1db5-125">Укажите имя и URL-адрес для приложения.</span><span class="sxs-lookup"><span data-stu-id="e1db5-125">Provide a name and URL for the application.</span></span> <span data-ttu-id="e1db5-126">Выберите тип создаваемого приложения: **веб-приложение или API** или **собственное приложение**.</span><span class="sxs-lookup"><span data-stu-id="e1db5-126">Select either **Web app / API** or **Native** for the type of application you want to create.</span></span> <span data-ttu-id="e1db5-127">Выбрав нужные значения, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e1db5-127">After setting the values, select **Create**.</span></span>

<span data-ttu-id="e1db5-128">Вы создали субъекта-службы для приложения.</span><span class="sxs-lookup"><span data-stu-id="e1db5-128">You have created a service principal for your application.</span></span>

### <a name="get-credentials"></a><span data-ttu-id="e1db5-129">Получить учетные данные</span><span class="sxs-lookup"><span data-stu-id="e1db5-129">Get credentials</span></span>
<span data-ttu-id="e1db5-130">Программным способом входа в систему используется идентификатор для приложения и ключ проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="e1db5-130">When programmatically logging in, you use the ID for your application and an authentication key.</span></span> <span data-ttu-id="e1db5-131">Получить эти значения можно следующим образом.</span><span class="sxs-lookup"><span data-stu-id="e1db5-131">To get those values, use the following steps:</span></span>

1. <span data-ttu-id="e1db5-132">В Active Directory в разделе **регистрации приложений** выберите нужное приложение.</span><span class="sxs-lookup"><span data-stu-id="e1db5-132">From **App registrations** in Active Directory, select your application.</span></span>

2. <span data-ttu-id="e1db5-133">Скопируйте **идентификатор приложения** и сохраните его в коде приложения.</span><span class="sxs-lookup"><span data-stu-id="e1db5-133">Copy the **Application ID** and store it in your application code.</span></span> <span data-ttu-id="e1db5-134">Приложения в разделе [примеров приложений](#sample-applications) используют это значение как идентификатор клиента.</span><span class="sxs-lookup"><span data-stu-id="e1db5-134">The applications in the [sample applications](#sample-applications) section refer to this value as the client id.</span></span>

     ![Идентификатор клиента](./media/azure-stack-create-service-principal/image12.png)
3. <span data-ttu-id="e1db5-136">Чтобы создать ключ проверки подлинности, щелкните **Ключи**.</span><span class="sxs-lookup"><span data-stu-id="e1db5-136">To generate an authentication key, select **Keys**.</span></span>

4. <span data-ttu-id="e1db5-137">Введите описание и срок действия ключа.</span><span class="sxs-lookup"><span data-stu-id="e1db5-137">Provide a description of the key, and a duration for the key.</span></span> <span data-ttu-id="e1db5-138">Затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e1db5-138">When done, select **Save**.</span></span>

<span data-ttu-id="e1db5-139">После этого отобразится значение ключа.</span><span class="sxs-lookup"><span data-stu-id="e1db5-139">After saving the key, the value of the key is displayed.</span></span> <span data-ttu-id="e1db5-140">Это значение нельзя будет получить позже, поэтому скопируйте его сразу.</span><span class="sxs-lookup"><span data-stu-id="e1db5-140">Copy this value because you are not able to retrieve the key later.</span></span> <span data-ttu-id="e1db5-141">Укажите значение ключа с Идентификатором приложения для подписи приложения.</span><span class="sxs-lookup"><span data-stu-id="e1db5-141">You provide the key value with the application ID to sign as the application.</span></span> <span data-ttu-id="e1db5-142">Сохраните значение ключа, чтобы приложение могло получить к нему доступ.</span><span class="sxs-lookup"><span data-stu-id="e1db5-142">Store the key value where your application can retrieve it.</span></span>

![сохраненный ключ](./media/azure-stack-create-service-principal/image15.png)


<span data-ttu-id="e1db5-144">После завершения, перейдите к [назначение роли приложения](azure-stack-create-service-principals.md#assign-role-to-service-principal).</span><span class="sxs-lookup"><span data-stu-id="e1db5-144">Once complete, proceed to [assigning your application a role](azure-stack-create-service-principals.md#assign-role-to-service-principal).</span></span>

## <a name="create-service-principal-for-ad-fs"></a><span data-ttu-id="e1db5-145">Создание участника службы для AD FS</span><span class="sxs-lookup"><span data-stu-id="e1db5-145">Create service principal for AD FS</span></span>
<span data-ttu-id="e1db5-146">Если вы развернули Azure стека с AD FS, можно использовать PowerShell для создания участника службы, назначение роли для доступа и входа с PowerShell, с использованием указанного удостоверения.</span><span class="sxs-lookup"><span data-stu-id="e1db5-146">If you have deployed Azure Stack with AD FS, you can use PowerShell to create a service principal, assign a role for access, and sign in from PowerShell using that identity.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="e1db5-147">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="e1db5-147">Before you begin</span></span>

[<span data-ttu-id="e1db5-148">Загрузите средства, необходимые для работы со стеком Azure на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="e1db5-148">Download the tools required to work with Azure Stack to your local computer.</span></span>](azure-stack-powershell-download.md)

### <a name="import-the-identity-powershell-module"></a><span data-ttu-id="e1db5-149">Импортируйте модуль PowerShell идентификаторов</span><span class="sxs-lookup"><span data-stu-id="e1db5-149">Import the Identity PowerShell module</span></span>
<span data-ttu-id="e1db5-150">После загрузки средств, перейдите в папку загруженные и импортируйте модуль PowerShell идентификаторов с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="e1db5-150">After you download the tools, navigate to the downloaded folder and import the Identity PowerShell module by using the following command:</span></span>

```PowerShell
Import-Module .\Identity\AzureStack.Identity.psm1
```

<span data-ttu-id="e1db5-151">При импорте модуля может появиться сообщение об ошибке: «AzureStack.Connect.psm1 не имеет цифровой подписи.</span><span class="sxs-lookup"><span data-stu-id="e1db5-151">When you import the module, you may receive an error that says “AzureStack.Connect.psm1 is not digitally signed.</span></span> <span data-ttu-id="e1db5-152">Скрипт не будет выполняться в системе».</span><span class="sxs-lookup"><span data-stu-id="e1db5-152">The script will not execute on the system”.</span></span> <span data-ttu-id="e1db5-153">Чтобы устранить эту проблему, можно задать политику выполнения и разрешить запуск скрипта с помощью следующей команды в сеансе PowerShell с повышенными привилегиями:</span><span class="sxs-lookup"><span data-stu-id="e1db5-153">To resolve this issue, you can set execution policy to allow running the script with the following command in an elevated PowerShell session:</span></span>

```PowerShell
Set-ExecutionPolicy Unrestricted
```

### <a name="create-the-service-principal"></a><span data-ttu-id="e1db5-154">Создание субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="e1db5-154">Create the service principal</span></span>
<span data-ttu-id="e1db5-155">Можно создать субъект-службу, выполнив следующую команду, убедившись, что обновление *DisplayName* параметр:</span><span class="sxs-lookup"><span data-stu-id="e1db5-155">You can create a Service Principal by executing the following command, making sure to update the *DisplayName* parameter:</span></span>
```powershell
$servicePrincipal = New-AzSADGraphServicePrincipal `
 -DisplayName "<YourServicePrincipalName>" `
 -AdminCredential $(Get-Credential) `
 -AdfsMachineName "AZS-ADFS01" `
 -Verbose
```
### <a name="assign-a-role"></a><span data-ttu-id="e1db5-156">Назначение роли</span><span class="sxs-lookup"><span data-stu-id="e1db5-156">Assign a role</span></span>
<span data-ttu-id="e1db5-157">После создания участника службы необходимо [назначение роли](azure-stack-create-service-principals.md#assign-role-to-service-principal)</span><span class="sxs-lookup"><span data-stu-id="e1db5-157">Once the Service Principal is created, you must [assign it to a role](azure-stack-create-service-principals.md#assign-role-to-service-principal)</span></span>

### <a name="sign-in-through-powershell"></a><span data-ttu-id="e1db5-158">Войти с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1db5-158">Sign in through PowerShell</span></span>
<span data-ttu-id="e1db5-159">После был назначен роли, вы сможете войти в стек Azure, используя имя участника службы с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="e1db5-159">Once you've assigned a role, you can sign in to Azure Stack using the service principal with the following command:</span></span>

```powershell
Add-AzureRmAccount -EnvironmentName "<AzureStackEnvironmentName>" `
 -ServicePrincipal `
 -CertificateThumbprint $servicePrincipal.Thumbprint `
 -ApplicationId $servicePrincipal.ApplicationId ` 
 -TenantId $directoryTenantId
```

## <a name="assign-role-to-service-principal"></a><span data-ttu-id="e1db5-160">Назначение роли участника-службы</span><span class="sxs-lookup"><span data-stu-id="e1db5-160">Assign role to service principal</span></span>
<span data-ttu-id="e1db5-161">Чтобы обеспечить доступ к ресурсам в подписке, необходимо назначить приложению роль.</span><span class="sxs-lookup"><span data-stu-id="e1db5-161">To access resources in your subscription, you must assign the application to a role.</span></span> <span data-ttu-id="e1db5-162">Укажите, какая роль предоставит приложению необходимые разрешения.</span><span class="sxs-lookup"><span data-stu-id="e1db5-162">Decide which role represents the right permissions for the application.</span></span> <span data-ttu-id="e1db5-163">Дополнительные сведения о доступных ролях см. в статье [RBAC: встроенные роли](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="e1db5-163">To learn about the available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="e1db5-164">Вы можете задать область действия на уровне подписки, группы ресурсов или ресурса.</span><span class="sxs-lookup"><span data-stu-id="e1db5-164">You can set the scope at the level of the subscription, resource group, or resource.</span></span> <span data-ttu-id="e1db5-165">Разрешения наследуют более низкие уровни области действия.</span><span class="sxs-lookup"><span data-stu-id="e1db5-165">Permissions are inherited to lower levels of scope.</span></span> <span data-ttu-id="e1db5-166">Например, добавление приложения в роль читателя для группы ресурсов означает, что оно может считывать группу ресурсов и все содержащиеся в ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="e1db5-166">For example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains.</span></span>

1. <span data-ttu-id="e1db5-167">На портале Azure стека перейдите на уровень области действия, которые вы хотите назначить приложению.</span><span class="sxs-lookup"><span data-stu-id="e1db5-167">In the Azure Stack portal, navigate to the level of scope you wish to assign the application to.</span></span> <span data-ttu-id="e1db5-168">Например, чтобы назначить роль в области действия подписки выберите **Подписки**.</span><span class="sxs-lookup"><span data-stu-id="e1db5-168">For example, to assign a role at the subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="e1db5-169">Или же вы можете выбрать группу ресурсов либо отдельный ресурс.</span><span class="sxs-lookup"><span data-stu-id="e1db5-169">You could instead select a resource group or resource.</span></span>

2. <span data-ttu-id="e1db5-170">Выберите определенную подписку, группу ресурсов или ресурс, которым будет назначено приложение.</span><span class="sxs-lookup"><span data-stu-id="e1db5-170">Select the particular subscription (resource group or resource) to assign the application to.</span></span>

     ![выбрать подписку для назначения](./media/azure-stack-create-service-principal/image16.png)

3. <span data-ttu-id="e1db5-172">Выберите **Управление доступом (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="e1db5-172">Select **Access Control (IAM)**.</span></span>

     ![выбрать доступ](./media/azure-stack-create-service-principal/image17.png)

4. <span data-ttu-id="e1db5-174">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e1db5-174">Select **Add**.</span></span>

5. <span data-ttu-id="e1db5-175">Выберите роль, которая будет назначена приложению.</span><span class="sxs-lookup"><span data-stu-id="e1db5-175">Select the role you wish to assign to the application.</span></span>

6. <span data-ttu-id="e1db5-176">Найдите приложение и выберите его.</span><span class="sxs-lookup"><span data-stu-id="e1db5-176">Search for your application, and select it.</span></span>

7. <span data-ttu-id="e1db5-177">Нажмите кнопку **ОК**, чтобы завершить назначение роли.</span><span class="sxs-lookup"><span data-stu-id="e1db5-177">Select **OK** to finish assigning the role.</span></span> <span data-ttu-id="e1db5-178">Вы увидите свое приложение в списке пользователей, назначенных выбранной роли для выбранной области действия.</span><span class="sxs-lookup"><span data-stu-id="e1db5-178">You see your application in the list of users assigned to a role for that scope.</span></span>

<span data-ttu-id="e1db5-179">Теперь, создания участника службы и назначить роль, можно начать с помощью этого приложения для доступа к ресурсам Azure стека.</span><span class="sxs-lookup"><span data-stu-id="e1db5-179">Now that you've created a service principal and assigned a role, you can begin using this within your application to access Azure Stack resources.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="e1db5-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e1db5-180">Next steps</span></span>

<span data-ttu-id="e1db5-181">[Добавление пользователей для служб федерации Active Directory](azure-stack-add-users-adfs.md)
[управлять разрешениями пользователей](azure-stack-manage-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="e1db5-181">[Add users for ADFS](azure-stack-add-users-adfs.md)
[Manage user permissions](azure-stack-manage-permissions.md)</span></span>