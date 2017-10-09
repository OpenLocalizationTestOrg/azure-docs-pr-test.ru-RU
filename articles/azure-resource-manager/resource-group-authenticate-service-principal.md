---
title: "aaaCreate удостоверение для приложения Azure с помощью PowerShell | Документы Microsoft"
description: "Описание управления toocreate Azure PowerShell toouse приложение Azure Active Directory и участника-службы, а также предоставляет доступ к tooresources посредством доступа на основе ролей. Здесь показано, как tooauthenticate приложения с помощью пароля или сертификата."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: d2caf121-9fbe-4f00-bf9d-8f3d1f00a6ff
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: c534360799b590054a051e4426e5e27dccb559b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toocreate-a-service-principal-tooaccess-resources"></a><span data-ttu-id="5ed3b-104">Использование Azure PowerShell toocreate ресурсов tooaccess участника службы</span><span class="sxs-lookup"><span data-stu-id="5ed3b-104">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>

<span data-ttu-id="5ed3b-105">При наличии приложения или скрипт, который необходимо tooaccess ресурсов, можно установить удостоверение для приложения hello и проверки подлинности приложения hello в свои собственные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-105">When you have an app or script that needs tooaccess resources, you can set up an identity for hello app and authenticate hello app with its own credentials.</span></span> <span data-ttu-id="5ed3b-106">Этот идентификатор известен как субъект-служба.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-106">This identity is known as a service principal.</span></span> <span data-ttu-id="5ed3b-107">Такой подход позволяет выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="5ed3b-107">This approach enables you to:</span></span>

* <span data-ttu-id="5ed3b-108">Назначение разрешений удостоверение приложения toohello, отличаются от собственных разрешений.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-108">Assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="5ed3b-109">Как правило эти разрешения являются ограниченными tooexactly какие hello приложению toodo.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-109">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="5ed3b-110">Использовать сертификат для аутентификации при выполнении автоматического сценария.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="5ed3b-111">В этом разделе показано, как toouse [Azure PowerShell](/powershell/azure/overview) tooset все необходимое для toorun приложения под свои собственные учетные данные и удостоверений.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-111">This topic shows you how toouse [Azure PowerShell](/powershell/azure/overview) tooset up everything you need for an application toorun under its own credentials and identity.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="5ed3b-112">Необходимые разрешения</span><span class="sxs-lookup"><span data-stu-id="5ed3b-112">Required permissions</span></span>
<span data-ttu-id="5ed3b-113">toocomplete в этом разделе, необходимо иметь достаточные разрешения в Azure Active Directory и вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-113">toocomplete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="5ed3b-114">В частности необходимо быть может toocreate приложение в Azure Active Directory hello и назначить роль участника tooa hello службы.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-114">Specifically, you must be able toocreate an app in hello Azure Active Directory, and assign hello service principal tooa role.</span></span> 

<span data-ttu-id="5ed3b-115">Hello ли ваша учетная запись имеет достаточные разрешения — с помощью портала hello простой toocheck способом.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-115">hello easiest way toocheck whether your account has adequate permissions is through hello portal.</span></span> <span data-ttu-id="5ed3b-116">Ознакомьтесь с [проверкой наличия необходимых разрешений](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="5ed3b-116">See [Check required permission](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="5ed3b-117">Теперь выполните tooa раздела для проверки подлинности с помощью действия.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-117">Now, proceed tooa section for authenticating with:</span></span>

* [<span data-ttu-id="5ed3b-118">password</span><span class="sxs-lookup"><span data-stu-id="5ed3b-118">password</span></span>](#create-service-principal-with-password)
* [<span data-ttu-id="5ed3b-119">самозаверяющий сертификат</span><span class="sxs-lookup"><span data-stu-id="5ed3b-119">self-signed certificate</span></span>](#create-service-principal-with-self-signed-certificate)
* [<span data-ttu-id="5ed3b-120">сертификат из центра сертификации</span><span class="sxs-lookup"><span data-stu-id="5ed3b-120">certificate from Certificate Authority</span></span>](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a><span data-ttu-id="5ed3b-121">Команды PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ed3b-121">PowerShell commands</span></span>

<span data-ttu-id="5ed3b-122">tooset участника службы при использовании:</span><span class="sxs-lookup"><span data-stu-id="5ed3b-122">tooset up a service principal, you use:</span></span>

| <span data-ttu-id="5ed3b-123">Команда</span><span class="sxs-lookup"><span data-stu-id="5ed3b-123">Command</span></span> | <span data-ttu-id="5ed3b-124">Описание</span><span class="sxs-lookup"><span data-stu-id="5ed3b-124">Description</span></span> |
| ------- | ----------- | 
| [<span data-ttu-id="5ed3b-125">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="5ed3b-125">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="5ed3b-126">Создает субъект-службу Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-126">Creates an Azure Active Directory service principal</span></span> |
| [<span data-ttu-id="5ed3b-127">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="5ed3b-127">New-AzureRmRoleAssignment</span></span>](/powershell/module/azurerm.resources/new-azurermroleassignment) | <span data-ttu-id="5ed3b-128">Назначает hello указано RBAC роли toohello указанного участника, за hello указанные области.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-128">Assigns hello specified RBAC role toohello specified principal, at hello specified scope.</span></span> |


## <a name="create-service-principal-with-password"></a><span data-ttu-id="5ed3b-129">Создание субъекта-службы с использованием пароля</span><span class="sxs-lookup"><span data-stu-id="5ed3b-129">Create service principal with password</span></span>

<span data-ttu-id="5ed3b-130">toocreate используйте участника службы с hello роль участника для вашей подписки:</span><span class="sxs-lookup"><span data-stu-id="5ed3b-130">toocreate a service principal with hello Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="5ed3b-131">пример Hello бездействует в течение 20 секунд tooallow некоторое время для hello новой службы основной toopropagate во всей Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-131">hello example sleeps for 20 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="5ed3b-132">Если сценарий не ждет достаточно долго для того, вы увидите следующее сообщение об ошибке: «PrincipalNotFound: участник {id} не существует в каталоге hello.»</span><span class="sxs-lookup"><span data-stu-id="5ed3b-132">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>

<span data-ttu-id="5ed3b-133">Hello следующий сценарий позволяет toospecify область, отличную от подписки по умолчанию hello и повторные попытки hello назначение роли, при возникновении ошибки:</span><span class="sxs-lookup"><span data-stu-id="5ed3b-133">hello following script enables you toospecify a scope other than hello default subscription, and retries hello role assignment if an error occurs:</span></span>

```powershell
Param (

 # Use tooset scope tooresource group. If no value is provided, scope is set toosubscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use tooset subscription. If no value is provided, default subscription is used. 
 [Parameter(Mandatory=$false)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName,

 [Parameter(Mandatory=$true)]
 [String] $Password
)

 Login-AzureRmAccount
 Import-Module AzureRM.Resources

 if ($SubscriptionId -eq "") 
 {
    $SubscriptionId = (Get-AzureRmContext).Subscription.Id
 }
 else
 {
    Set-AzureRmContext -SubscriptionId $SubscriptionId
 }

 if ($ResourceGroup -eq "")
 {
    $Scope = "/subscriptions/" + $SubscriptionId
 }
 else
 {
    $Scope = (Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop).ResourceId
 }

 
 # Create Service Principal for hello AD app
 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

<span data-ttu-id="5ed3b-134">Несколько элементов toonote о hello сценария:</span><span class="sxs-lookup"><span data-stu-id="5ed3b-134">A few items toonote about hello script:</span></span>

* <span data-ttu-id="5ed3b-135">toogrant hello удостоверение доступа toohello подписки по умолчанию, нет необходимости tooprovide группа ресурсов или SubscriptionId параметров.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-135">toogrant hello identity access toohello default subscription, you do not need tooprovide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="5ed3b-136">Укажите параметр hello группа ресурсов только в том случае, если требуется область hello toolimit группы ресурсов tooa назначения роли hello.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-136">Specify hello ResourceGroup parameter only when you want toolimit hello scope of hello role assignment tooa resource group.</span></span>
*  <span data-ttu-id="5ed3b-137">В этом примере добавьте роль участника toohello основной службы hello.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-137">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="5ed3b-138">Сведения о других ролях см. в статье [RBAC: встроенные роли](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="5ed3b-138">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="5ed3b-139">сценарий Hello бездействует в течение 15 секунд tooallow некоторое время для hello новой службы основной toopropagate во всей Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-139">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="5ed3b-140">Если сценарий не ждет достаточно долго для того, вы увидите следующее сообщение об ошибке: «PrincipalNotFound: участник {id} не существует в каталоге hello.»</span><span class="sxs-lookup"><span data-stu-id="5ed3b-140">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="5ed3b-141">Если требуется toogrant hello службы доступа toomore подписки или групп ресурсов, запустите hello `New-AzureRMRoleAssignment` командлет еще раз с различными областями действия.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-141">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>


### <a name="provide-credentials-through-powershell"></a><span data-ttu-id="5ed3b-142">Предоставление учетных данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ed3b-142">Provide credentials through PowerShell</span></span>
<span data-ttu-id="5ed3b-143">Теперь требуется toolog в качестве операции tooperform приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-143">Now, you need toolog in as hello application tooperform operations.</span></span> <span data-ttu-id="5ed3b-144">Для имени пользователя hello, использовать hello `ApplicationId` , созданного для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-144">For hello user name, use hello `ApplicationId` that you created for hello application.</span></span> <span data-ttu-id="5ed3b-145">Для пароля hello используйте hello, указанный при создании учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-145">For hello password, use hello one you specified when creating hello account.</span></span> 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

<span data-ttu-id="5ed3b-146">ИД клиента Hello не учитывается, так можно внедрить его непосредственно в скрипте.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-146">hello tenant ID is not sensitive, so you can embed it directly in your script.</span></span> <span data-ttu-id="5ed3b-147">Если вам требуется идентификатор клиента tooretrieve hello, используйте:</span><span class="sxs-lookup"><span data-stu-id="5ed3b-147">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a><span data-ttu-id="5ed3b-148">Создание субъекта-службы с самозаверяющим сертификатом</span><span class="sxs-lookup"><span data-stu-id="5ed3b-148">Create service principal with self-signed certificate</span></span>

<span data-ttu-id="5ed3b-149">toocreate используйте участника службы с помощью самозаверяющего сертификата и роль участника hello для вашей подписки:</span><span class="sxs-lookup"><span data-stu-id="5ed3b-149">toocreate a service principal with a self-signed certificate and hello Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="5ed3b-150">пример Hello бездействует в течение 20 секунд tooallow некоторое время для hello новой службы основной toopropagate во всей Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-150">hello example sleeps for 20 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="5ed3b-151">Если сценарий не ждет достаточно долго для того, вы увидите следующее сообщение об ошибке: «PrincipalNotFound: участник {id} не существует в каталоге hello.»</span><span class="sxs-lookup"><span data-stu-id="5ed3b-151">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>

<span data-ttu-id="5ed3b-152">Hello следующий сценарий позволяет toospecify область, отличную от подписки по умолчанию hello и повторные попытки hello назначение ролей, если произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-152">hello following script enables you toospecify a scope other than hello default subscription, and retries hello role assignment if an error occurs.</span></span> <span data-ttu-id="5ed3b-153">Необходимо наличие Azure PowerShell 2.0 в Windows 10 или Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-153">You must have Azure PowerShell 2.0 on Windows 10 or Windows Server 2016.</span></span>

```powershell
Param (

 # Use tooset scope tooresource group. If no value is provided, scope is set toosubscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use tooset subscription. If no value is provided, default subscription is used. 
 [Parameter(Mandatory=$false)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName
 )

 Login-AzureRmAccount
 Import-Module AzureRM.Resources

 if ($SubscriptionId -eq "") 
 {
    $SubscriptionId = (Get-AzureRmContext).Subscription.Id
 }
 else
 {
    Set-AzureRmContext -SubscriptionId $SubscriptionId
 }

 if ($ResourceGroup -eq "")
 {
    $Scope = "/subscriptions/" + $SubscriptionId
 }
 else
 {
    $Scope = (Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop).ResourceId
 }

 $cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
 $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

<span data-ttu-id="5ed3b-154">Несколько элементов toonote о hello сценария:</span><span class="sxs-lookup"><span data-stu-id="5ed3b-154">A few items toonote about hello script:</span></span>

* <span data-ttu-id="5ed3b-155">toogrant hello удостоверение доступа toohello подписки по умолчанию, нет необходимости tooprovide группа ресурсов или SubscriptionId параметров.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-155">toogrant hello identity access toohello default subscription, you do not need tooprovide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="5ed3b-156">Укажите параметр hello группа ресурсов только в том случае, если требуется область hello toolimit группы ресурсов tooa назначения роли hello.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-156">Specify hello ResourceGroup parameter only when you want toolimit hello scope of hello role assignment tooa resource group.</span></span>
* <span data-ttu-id="5ed3b-157">В этом примере добавьте роль участника toohello основной службы hello.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-157">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="5ed3b-158">Сведения о других ролях см. в статье [RBAC: встроенные роли](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="5ed3b-158">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="5ed3b-159">сценарий Hello бездействует в течение 15 секунд tooallow некоторое время для hello новой службы основной toopropagate во всей Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-159">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="5ed3b-160">Если сценарий не ждет достаточно долго для того, вы увидите следующее сообщение об ошибке: «PrincipalNotFound: участник {id} не существует в каталоге hello.»</span><span class="sxs-lookup"><span data-stu-id="5ed3b-160">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="5ed3b-161">Если требуется toogrant hello службы доступа toomore подписки или групп ресурсов, запустите hello `New-AzureRMRoleAssignment` командлет еще раз с различными областями действия.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-161">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

<span data-ttu-id="5ed3b-162">Если вы **нет Windows 10 или Windows Server 2016 Technical Preview**, требуется toodownload hello [генератор самозаверяющий сертификат](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) из центра сценариев Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-162">If you **do not have Windows 10 or Windows Server 2016 Technical Preview**, you need toodownload hello [Self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from Microsoft Script Center.</span></span> <span data-ttu-id="5ed3b-163">Извлеките его содержимое и командлет hello, на который требуется импортировать.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-163">Extract its contents and import hello cmdlet you need.</span></span>

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
<span data-ttu-id="5ed3b-164">В сценарии hello замените hello, следующие две строки toogenerate hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-164">In hello script, substitute hello following two lines toogenerate hello certificate.</span></span>
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="5ed3b-165">Предоставление сертификата с помощью автоматизированного сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ed3b-165">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="5ed3b-166">При каждом входе в качестве участника-службы для приложения AD необходимо ИД клиента hello tooprovide hello каталога.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-166">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="5ed3b-167">Клиент — это экземпляр Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-167">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="5ed3b-168">Если у вас только одна подписка, используйте команду:</span><span class="sxs-lookup"><span data-stu-id="5ed3b-168">If you only have one subscription, you can use:</span></span>

```powershell
Param (
 
 [Parameter(Mandatory=$true)]
 [String] $CertSubject,
 
 [Parameter(Mandatory=$true)]
 [String] $ApplicationId,

 [Parameter(Mandatory=$true)]
 [String] $TenantId
 )

 $Thumbprint = (Get-ChildItem cert:\CurrentUser\My\ | Where-Object {$_.Subject -match $CertSubject }).Thumbprint
 Login-AzureRmAccount -ServicePrincipal -CertificateThumbprint $Thumbprint -ApplicationId $ApplicationId -TenantId $TenantId
```

<span data-ttu-id="5ed3b-169">приложение Hello код и код клиента не учитывает регистр, поэтому их можно внедрить непосредственно в скрипте.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-169">hello application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="5ed3b-170">Если вам требуется идентификатор клиента tooretrieve hello, используйте:</span><span class="sxs-lookup"><span data-stu-id="5ed3b-170">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="5ed3b-171">Если вам требуется идентификатор приложения hello tooretrieve, используйте:</span><span class="sxs-lookup"><span data-stu-id="5ed3b-171">If you need tooretrieve hello application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a><span data-ttu-id="5ed3b-172">Создание субъекта-службы с помощью сертификата из центра сертификации</span><span class="sxs-lookup"><span data-stu-id="5ed3b-172">Create service principal with certificate from Certificate Authority</span></span>
<span data-ttu-id="5ed3b-173">toouse сертификат, выданный центром сертификации toocreate субъекта-службы, hello используйте следующий сценарий:</span><span class="sxs-lookup"><span data-stu-id="5ed3b-173">toouse a certificate issued from a Certificate Authority toocreate service principal, use hello following script:</span></span>

```powershell
Param (
 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName,

 [Parameter(Mandatory=$true)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $CertPath,

 [Parameter(Mandatory=$true)]
 [String] $CertPlainPassword
 )

 Login-AzureRmAccount
 Import-Module AzureRM.Resources
 Set-AzureRmContext -SubscriptionId $SubscriptionId

 $KeyId = (New-Guid).Guid
 $CertPassword = ConvertTo-SecureString $CertPlainPassword -AsPlainText -Force

 $PFXCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($CertPath, $CertPassword)
 $KeyValue = [System.Convert]::ToBase64String($PFXCert.GetRawCertData())

 $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
 $KeyCredential.StartDate = $PFXCert.NotBefore
 $KeyCredential.EndDate= $PFXCert.NotAfter
 $KeyCredential.KeyId = $KeyId
 $KeyCredential.CertValue = $KeyValue

 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -KeyCredentials $keyCredential
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
 
 $NewRole
```

<span data-ttu-id="5ed3b-174">Несколько элементов toonote о hello сценария:</span><span class="sxs-lookup"><span data-stu-id="5ed3b-174">A few items toonote about hello script:</span></span>

* <span data-ttu-id="5ed3b-175">Доступ осуществляется с областью toohello подписки.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-175">Access is scoped toohello subscription.</span></span>
* <span data-ttu-id="5ed3b-176">В этом примере добавьте роль участника toohello основной службы hello.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-176">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="5ed3b-177">Сведения о других ролях см. в статье [RBAC: встроенные роли](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="5ed3b-177">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="5ed3b-178">сценарий Hello бездействует в течение 15 секунд tooallow некоторое время для hello новой службы основной toopropagate во всей Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-178">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="5ed3b-179">Если сценарий не ждет достаточно долго для того, вы увидите следующее сообщение об ошибке: «PrincipalNotFound: участник {id} не существует в каталоге hello.»</span><span class="sxs-lookup"><span data-stu-id="5ed3b-179">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="5ed3b-180">Если требуется toogrant hello службы доступа toomore подписки или групп ресурсов, запустите hello `New-AzureRMRoleAssignment` командлет еще раз с различными областями действия.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-180">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="5ed3b-181">Предоставление сертификата с помощью автоматизированного сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ed3b-181">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="5ed3b-182">При каждом входе в качестве участника-службы для приложения AD необходимо ИД клиента hello tooprovide hello каталога.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-182">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="5ed3b-183">Клиент — это экземпляр Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-183">A tenant is an instance of Azure Active Directory.</span></span>

```powershell
Param (
 
 [Parameter(Mandatory=$true)]
 [String] $CertPath,

 [Parameter(Mandatory=$true)]
 [String] $CertPlainPassword,
 
 [Parameter(Mandatory=$true)]
 [String] $ApplicationId,

 [Parameter(Mandatory=$true)]
 [String] $TenantId
 )

 $CertPassword = ConvertTo-SecureString $CertPlainPassword -AsPlainText -Force
 $PFXCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($CertPath, $CertPassword)
 $Thumbprint = $PFXCert.Thumbprint

 Login-AzureRmAccount -ServicePrincipal -CertificateThumbprint $Thumbprint -ApplicationId $ApplicationId -TenantId $TenantId
```

<span data-ttu-id="5ed3b-184">приложение Hello код и код клиента не учитывает регистр, поэтому их можно внедрить непосредственно в скрипте.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-184">hello application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="5ed3b-185">Если вам требуется идентификатор клиента tooretrieve hello, используйте:</span><span class="sxs-lookup"><span data-stu-id="5ed3b-185">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="5ed3b-186">Если вам требуется идентификатор приложения hello tooretrieve, используйте:</span><span class="sxs-lookup"><span data-stu-id="5ed3b-186">If you need tooretrieve hello application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a><span data-ttu-id="5ed3b-187">Изменение учетных данных</span><span class="sxs-lookup"><span data-stu-id="5ed3b-187">Change credentials</span></span>

<span data-ttu-id="5ed3b-188">учетные данные hello toochange для приложения AD, либо из-за нарушение безопасности или истечения срока действия учетных данных, используйте hello [удаление AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) и [New AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) командлетов.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-188">toochange hello credentials for an AD app, either because of a security compromise or a credential expiration, use hello [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) and [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlets.</span></span>

<span data-ttu-id="5ed3b-189">tooremove все hello учетные данные для приложения, используйте:</span><span class="sxs-lookup"><span data-stu-id="5ed3b-189">tooremove all hello credentials for an application, use:</span></span>

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

<span data-ttu-id="5ed3b-190">Используйте tooadd пароль:</span><span class="sxs-lookup"><span data-stu-id="5ed3b-190">tooadd a password, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

<span data-ttu-id="5ed3b-191">tooadd значение сертификата, создайте самозаверяющий сертификат, как показано в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-191">tooadd a certificate value, create a self-signed certificate as shown in this topic.</span></span> <span data-ttu-id="5ed3b-192">Затем используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-192">Then, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-toosimplify-log-in"></a><span data-ttu-id="5ed3b-193">Сохранить вход маркера toosimplify доступа</span><span class="sxs-lookup"><span data-stu-id="5ed3b-193">Save access token toosimplify log in</span></span>
<span data-ttu-id="5ed3b-194">tooavoid предоставление hello службы основной учетных данных каждый раз, он должен toolog в, можно сохранить hello маркер доступа.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-194">tooavoid providing hello service principal credentials every time it needs toolog in, you can save hello access token.</span></span>

<span data-ttu-id="5ed3b-195">toouse hello текущего маркера доступа в следующем сеансе сохранить профиль hello.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-195">toouse hello current access token in a later session, save hello profile.</span></span>
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
<span data-ttu-id="5ed3b-196">Откройте профиль hello и изучите его содержимое.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-196">Open hello profile and examine its contents.</span></span> <span data-ttu-id="5ed3b-197">Обратите внимание, что он содержит маркер доступа.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-197">Notice that it contains an access token.</span></span> <span data-ttu-id="5ed3b-198">Вместо вручную вход в систему, просто загрузить профиль hello.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-198">Instead of manually logging in again, simply load hello profile.</span></span>
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> <span data-ttu-id="5ed3b-199">Hello срока действия маркера доступа, поэтому с помощью сохраненного профиля работает только для при условии, что маркер hello является действительным.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-199">hello access token expires, so using a saved profile only works for as long as hello token is valid.</span></span>
>  

<span data-ttu-id="5ed3b-200">Кроме того могут вызывать операции REST из toolog PowerShell в.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-200">Alternatively, you can invoke REST operations from PowerShell toolog in.</span></span> <span data-ttu-id="5ed3b-201">Из hello ответ проверки подлинности можно получить маркер доступа hello для использования с другими операциями.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-201">From hello authentication response, you can retrieve hello access token for use with other operations.</span></span> <span data-ttu-id="5ed3b-202">Пример получения токена доступа hello путем вызова операции REST см. в разделе [создания токена доступа](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="5ed3b-202">For an example of retrieving hello access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="debug"></a><span data-ttu-id="5ed3b-203">Отладка</span><span class="sxs-lookup"><span data-stu-id="5ed3b-203">Debug</span></span>

<span data-ttu-id="5ed3b-204">Возможны следующие ошибки при создании участника службы hello.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-204">You may encounter hello following errors when creating a service principal:</span></span>

* <span data-ttu-id="5ed3b-205">**«Authentication_Unauthorized»** или **«подписка не найден в контексте hello».**</span><span class="sxs-lookup"><span data-stu-id="5ed3b-205">**"Authentication_Unauthorized"** or **"No subscription found in hello context."**</span></span> <span data-ttu-id="5ed3b-206">-Эта ошибка появляется, когда ваша учетная запись не имеет hello [разрешения, необходимые](#required-permissions) на hello Azure Active Directory tooregister приложения.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-206">- You see this error when your account does not have hello [required permissions](#required-permissions) on hello Azure Active Directory tooregister an app.</span></span> <span data-ttu-id="5ed3b-207">Как правило, эта ошибка возникает в тех случаях, когда регистрировать приложения в Azure Active Directory могут только администраторы, а ваша учетная запись не является административной. Попросите вашего администратора tooeither назначить вы tooan роль администратора или tooenable пользователей tooregister приложений.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-207">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin. Ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

* <span data-ttu-id="5ed3b-208">Ваша учетная запись **«не имеют авторизации tooperform действия «Microsoft.Authorization/roleAssignments/write» с областью «/ subscriptions / {guid}».»**  -Эта ошибка появляется, когда учетная запись имеет достаточные разрешения tooassign удостоверением tooan роли.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-208">Your account **"does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions tooassign a role tooan identity.</span></span> <span data-ttu-id="5ed3b-209">Попросите администратора вашей подписки tooadd вы tooUser доступа к роли администратора.</span><span class="sxs-lookup"><span data-stu-id="5ed3b-209">Ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="5ed3b-210">Примеры приложений</span><span class="sxs-lookup"><span data-stu-id="5ed3b-210">Sample applications</span></span>
<span data-ttu-id="5ed3b-211">Сведения о входе в систему как hello приложения с помощью различных платформ см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="5ed3b-211">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="5ed3b-212">.NET</span><span class="sxs-lookup"><span data-stu-id="5ed3b-212">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="5ed3b-213">Java</span><span class="sxs-lookup"><span data-stu-id="5ed3b-213">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="5ed3b-214">Node.js</span><span class="sxs-lookup"><span data-stu-id="5ed3b-214">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="5ed3b-215">Python</span><span class="sxs-lookup"><span data-stu-id="5ed3b-215">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="5ed3b-216">Ruby</span><span class="sxs-lookup"><span data-stu-id="5ed3b-216">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="5ed3b-217">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5ed3b-217">Next steps</span></span>
* <span data-ttu-id="5ed3b-218">Подробные инструкции по установке приложения в Azure для управления ресурсами см. в разделе [tooauthorization руководство разработчика с hello API диспетчера ресурсов Azure](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5ed3b-218">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="5ed3b-219">Более подробное описание приложений и субъектов-служб см. в статье [Объекты приложений и объекты участников-служб](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="5ed3b-219">For a more detailed explanation of applications and service principals, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span> 
* <span data-ttu-id="5ed3b-220">Дополнительные сведения о проверке подлинности Azure Active Directory см. в статье [Сценарии проверки подлинности в Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="5ed3b-220">For more information about Azure Active Directory authentication, see [Authentication Scenarios for Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span></span>
* <span data-ttu-id="5ed3b-221">Список доступных действий, которые могут быть предоставлены или запрещены toousers см. в разделе [операций поставщика ресурсов диспетчера ресурсов Azure](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="5ed3b-221">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>

