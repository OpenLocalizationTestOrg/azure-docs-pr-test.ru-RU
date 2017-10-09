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
# <a name="use-azure-powershell-toocreate-a-service-principal-tooaccess-resources"></a>Использование Azure PowerShell toocreate ресурсов tooaccess участника службы

При наличии приложения или скрипт, который необходимо tooaccess ресурсов, можно установить удостоверение для приложения hello и проверки подлинности приложения hello в свои собственные учетные данные. Этот идентификатор известен как субъект-служба. Такой подход позволяет выполнить следующие действия:

* Назначение разрешений удостоверение приложения toohello, отличаются от собственных разрешений. Как правило эти разрешения являются ограниченными tooexactly какие hello приложению toodo.
* Использовать сертификат для аутентификации при выполнении автоматического сценария.

В этом разделе показано, как toouse [Azure PowerShell](/powershell/azure/overview) tooset все необходимое для toorun приложения под свои собственные учетные данные и удостоверений.

## <a name="required-permissions"></a>Необходимые разрешения
toocomplete в этом разделе, необходимо иметь достаточные разрешения в Azure Active Directory и вашей подписке Azure. В частности необходимо быть может toocreate приложение в Azure Active Directory hello и назначить роль участника tooa hello службы. 

Hello ли ваша учетная запись имеет достаточные разрешения — с помощью портала hello простой toocheck способом. Ознакомьтесь с [проверкой наличия необходимых разрешений](resource-group-create-service-principal-portal.md#required-permissions).

Теперь выполните tooa раздела для проверки подлинности с помощью действия.

* [password](#create-service-principal-with-password)
* [самозаверяющий сертификат](#create-service-principal-with-self-signed-certificate)
* [сертификат из центра сертификации](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a>Команды PowerShell

tooset участника службы при использовании:

| Команда | Описание |
| ------- | ----------- | 
| [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | Создает субъект-службу Azure Active Directory. |
| [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment) | Назначает hello указано RBAC роли toohello указанного участника, за hello указанные области. |


## <a name="create-service-principal-with-password"></a>Создание субъекта-службы с использованием пароля

toocreate используйте участника службы с hello роль участника для вашей подписки: 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

пример Hello бездействует в течение 20 секунд tooallow некоторое время для hello новой службы основной toopropagate во всей Azure Active Directory. Если сценарий не ждет достаточно долго для того, вы увидите следующее сообщение об ошибке: «PrincipalNotFound: участник {id} не существует в каталоге hello.»

Hello следующий сценарий позволяет toospecify область, отличную от подписки по умолчанию hello и повторные попытки hello назначение роли, при возникновении ошибки:

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

Несколько элементов toonote о hello сценария:

* toogrant hello удостоверение доступа toohello подписки по умолчанию, нет необходимости tooprovide группа ресурсов или SubscriptionId параметров.
* Укажите параметр hello группа ресурсов только в том случае, если требуется область hello toolimit группы ресурсов tooa назначения роли hello.
*  В этом примере добавьте роль участника toohello основной службы hello. Сведения о других ролях см. в статье [RBAC: встроенные роли](../active-directory/role-based-access-built-in-roles.md).
* сценарий Hello бездействует в течение 15 секунд tooallow некоторое время для hello новой службы основной toopropagate во всей Azure Active Directory. Если сценарий не ждет достаточно долго для того, вы увидите следующее сообщение об ошибке: «PrincipalNotFound: участник {id} не существует в каталоге hello.»
* Если требуется toogrant hello службы доступа toomore подписки или групп ресурсов, запустите hello `New-AzureRMRoleAssignment` командлет еще раз с различными областями действия.


### <a name="provide-credentials-through-powershell"></a>Предоставление учетных данных с помощью PowerShell
Теперь требуется toolog в качестве операции tooperform приложения hello. Для имени пользователя hello, использовать hello `ApplicationId` , созданного для приложения hello. Для пароля hello используйте hello, указанный при создании учетной записи hello. 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

ИД клиента Hello не учитывается, так можно внедрить его непосредственно в скрипте. Если вам требуется идентификатор клиента tooretrieve hello, используйте:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a>Создание субъекта-службы с самозаверяющим сертификатом

toocreate используйте участника службы с помощью самозаверяющего сертификата и роль участника hello для вашей подписки: 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

пример Hello бездействует в течение 20 секунд tooallow некоторое время для hello новой службы основной toopropagate во всей Azure Active Directory. Если сценарий не ждет достаточно долго для того, вы увидите следующее сообщение об ошибке: «PrincipalNotFound: участник {id} не существует в каталоге hello.»

Hello следующий сценарий позволяет toospecify область, отличную от подписки по умолчанию hello и повторные попытки hello назначение ролей, если произошла ошибка. Необходимо наличие Azure PowerShell 2.0 в Windows 10 или Windows Server 2016.

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

Несколько элементов toonote о hello сценария:

* toogrant hello удостоверение доступа toohello подписки по умолчанию, нет необходимости tooprovide группа ресурсов или SubscriptionId параметров.
* Укажите параметр hello группа ресурсов только в том случае, если требуется область hello toolimit группы ресурсов tooa назначения роли hello.
* В этом примере добавьте роль участника toohello основной службы hello. Сведения о других ролях см. в статье [RBAC: встроенные роли](../active-directory/role-based-access-built-in-roles.md).
* сценарий Hello бездействует в течение 15 секунд tooallow некоторое время для hello новой службы основной toopropagate во всей Azure Active Directory. Если сценарий не ждет достаточно долго для того, вы увидите следующее сообщение об ошибке: «PrincipalNotFound: участник {id} не существует в каталоге hello.»
* Если требуется toogrant hello службы доступа toomore подписки или групп ресурсов, запустите hello `New-AzureRMRoleAssignment` командлет еще раз с различными областями действия.

Если вы **нет Windows 10 или Windows Server 2016 Technical Preview**, требуется toodownload hello [генератор самозаверяющий сертификат](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) из центра сценариев Майкрософт. Извлеките его содержимое и командлет hello, на который требуется импортировать.

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
В сценарии hello замените hello, следующие две строки toogenerate hello сертификата.
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a>Предоставление сертификата с помощью автоматизированного сценария PowerShell
При каждом входе в качестве участника-службы для приложения AD необходимо ИД клиента hello tooprovide hello каталога. Клиент — это экземпляр Azure Active Directory. Если у вас только одна подписка, используйте команду:

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

приложение Hello код и код клиента не учитывает регистр, поэтому их можно внедрить непосредственно в скрипте. Если вам требуется идентификатор клиента tooretrieve hello, используйте:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

Если вам требуется идентификатор приложения hello tooretrieve, используйте:

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a>Создание субъекта-службы с помощью сертификата из центра сертификации
toouse сертификат, выданный центром сертификации toocreate субъекта-службы, hello используйте следующий сценарий:

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

Несколько элементов toonote о hello сценария:

* Доступ осуществляется с областью toohello подписки.
* В этом примере добавьте роль участника toohello основной службы hello. Сведения о других ролях см. в статье [RBAC: встроенные роли](../active-directory/role-based-access-built-in-roles.md).
* сценарий Hello бездействует в течение 15 секунд tooallow некоторое время для hello новой службы основной toopropagate во всей Azure Active Directory. Если сценарий не ждет достаточно долго для того, вы увидите следующее сообщение об ошибке: «PrincipalNotFound: участник {id} не существует в каталоге hello.»
* Если требуется toogrant hello службы доступа toomore подписки или групп ресурсов, запустите hello `New-AzureRMRoleAssignment` командлет еще раз с различными областями действия.

### <a name="provide-certificate-through-automated-powershell-script"></a>Предоставление сертификата с помощью автоматизированного сценария PowerShell
При каждом входе в качестве участника-службы для приложения AD необходимо ИД клиента hello tooprovide hello каталога. Клиент — это экземпляр Azure Active Directory.

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

приложение Hello код и код клиента не учитывает регистр, поэтому их можно внедрить непосредственно в скрипте. Если вам требуется идентификатор клиента tooretrieve hello, используйте:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

Если вам требуется идентификатор приложения hello tooretrieve, используйте:

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a>Изменение учетных данных

учетные данные hello toochange для приложения AD, либо из-за нарушение безопасности или истечения срока действия учетных данных, используйте hello [удаление AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) и [New AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) командлетов.

tooremove все hello учетные данные для приложения, используйте:

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

Используйте tooadd пароль:

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

tooadd значение сертификата, создайте самозаверяющий сертификат, как показано в этом разделе. Затем используйте следующую команду.

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-toosimplify-log-in"></a>Сохранить вход маркера toosimplify доступа
tooavoid предоставление hello службы основной учетных данных каждый раз, он должен toolog в, можно сохранить hello маркер доступа.

toouse hello текущего маркера доступа в следующем сеансе сохранить профиль hello.
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
Откройте профиль hello и изучите его содержимое. Обратите внимание, что он содержит маркер доступа. Вместо вручную вход в систему, просто загрузить профиль hello.
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> Hello срока действия маркера доступа, поэтому с помощью сохраненного профиля работает только для при условии, что маркер hello является действительным.
>  

Кроме того могут вызывать операции REST из toolog PowerShell в. Из hello ответ проверки подлинности можно получить маркер доступа hello для использования с другими операциями. Пример получения токена доступа hello путем вызова операции REST см. в разделе [создания токена доступа](resource-manager-rest-api.md#generating-an-access-token).

## <a name="debug"></a>Отладка

Возможны следующие ошибки при создании участника службы hello.

* **«Authentication_Unauthorized»** или **«подписка не найден в контексте hello».** -Эта ошибка появляется, когда ваша учетная запись не имеет hello [разрешения, необходимые](#required-permissions) на hello Azure Active Directory tooregister приложения. Как правило, эта ошибка возникает в тех случаях, когда регистрировать приложения в Azure Active Directory могут только администраторы, а ваша учетная запись не является административной. Попросите вашего администратора tooeither назначить вы tooan роль администратора или tooenable пользователей tooregister приложений.

* Ваша учетная запись **«не имеют авторизации tooperform действия «Microsoft.Authorization/roleAssignments/write» с областью «/ subscriptions / {guid}».»**  -Эта ошибка появляется, когда учетная запись имеет достаточные разрешения tooassign удостоверением tooan роли. Попросите администратора вашей подписки tooadd вы tooUser доступа к роли администратора.

## <a name="sample-applications"></a>Примеры приложений
Сведения о входе в систему как hello приложения с помощью различных платформ см. в разделе:

* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a>Дальнейшие действия
* Подробные инструкции по установке приложения в Azure для управления ресурсами см. в разделе [tooauthorization руководство разработчика с hello API диспетчера ресурсов Azure](resource-manager-api-authentication.md).
* Более подробное описание приложений и субъектов-служб см. в статье [Объекты приложений и объекты участников-служб](../active-directory/active-directory-application-objects.md). 
* Дополнительные сведения о проверке подлинности Azure Active Directory см. в статье [Сценарии проверки подлинности в Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).
* Список доступных действий, которые могут быть предоставлены или запрещены toousers см. в разделе [операций поставщика ресурсов диспетчера ресурсов Azure](../active-directory/role-based-access-control-resource-provider-operations.md).

