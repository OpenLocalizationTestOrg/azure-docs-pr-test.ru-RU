---
title: "aaaCreate Azure автоматизации запуска от имени учетной записи с помощью PowerShell | Документы Microsoft"
description: "В этой статье описывается, как tooupgrade ваша учетная запись автоматизации с PowerShell hello toocreate запуска от имени учетных записей, если этот шаг не выполнялись во время первоначального создания из портала hello."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/14/2017
ms.author: magoedte
ms.openlocfilehash: 1049601321d2bc1e5f9d982f622788f8e4e4d797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="update-automation-run-as-account-using-powershell"></a><span data-ttu-id="10dac-103">Обновление учетной записи запуска от имени службы автоматизации с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="10dac-103">Update Automation Run As account using PowerShell</span></span>
<span data-ttu-id="10dac-104">Можно использовать существующую учетную запись автоматизации PowerShell tooupdate, если:</span><span class="sxs-lookup"><span data-stu-id="10dac-104">You can use PowerShell tooupdate your existing Automation account if:</span></span>

* <span data-ttu-id="10dac-105">Создание учетной записи автоматизации, но отклонить toocreate hello запуска от имени учетной записи.</span><span class="sxs-lookup"><span data-stu-id="10dac-105">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="10dac-106">Ресурсы диспетчера ресурсов автоматизации toomanage учетной записи уже используется, и требуется tooupdate hello tooinclude hello запуска от имени учетной записи для проверки подлинности runbook.</span><span class="sxs-lookup"><span data-stu-id="10dac-106">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="10dac-107">Учетная запись автоматизации toomanage классические ресурсы уже используется и нужно tooupdate его toouse hello классический запуска от имени учетной записи вместо создания новой учетной записи и переход к tooit Runbook и активов.</span><span class="sxs-lookup"><span data-stu-id="10dac-107">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="10dac-108">Требуется toocreate запуска от имени, а классические учетной записи запуска с помощью сертификата, выданного вашего центра сертификации предприятия (ЦС).</span><span class="sxs-lookup"><span data-stu-id="10dac-108">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10dac-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="10dac-109">Prerequisites</span></span>

* <span data-ttu-id="10dac-110">Hello сценарий может выполняться только в Windows 10 и Windows Server 2016 с модулями Azure Resource Manager 2.01 и более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="10dac-110">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="10dac-111">Более ранние версии Windows не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="10dac-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="10dac-112">Azure PowerShell 1.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="10dac-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="10dac-113">Сведения о выпуске hello PowerShell 1.0 см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="10dac-113">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="10dac-114">Учетная запись автоматизации, на которую ссылается как значение hello для hello *— AutomationAccountName* и *- ApplicationDisplayName* параметры в следующем скрипте PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="10dac-114">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="10dac-115">tooget hello значения для *SubscriptionID*, *ResourceGroup*, и *AutomationAccountName*, которой являются обязательными параметрами для скриптов hello, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="10dac-115">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello scripts, do hello following:</span></span>
1. <span data-ttu-id="10dac-116">В hello портал Azure, выберите учетную запись автоматизации на hello **учетной записи автоматизации** колонки, а затем выберите **все параметры**.</span><span class="sxs-lookup"><span data-stu-id="10dac-116">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="10dac-117">На hello **все параметры** колонки в разделе **параметры учетной записи**выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="10dac-117">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="10dac-118">Запишите значения hello на hello **свойства** колонку.</span><span class="sxs-lookup"><span data-stu-id="10dac-118">Note hello values on hello **Properties** blade.</span></span>

![колонку «Свойства» учетной записи автоматизации Hello](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

## <a name="create-run-as-account-powershell-script"></a><span data-ttu-id="10dac-120">Создание сценария PowerShell для учетной записи запуска от имени</span><span class="sxs-lookup"><span data-stu-id="10dac-120">Create Run As Account PowerShell script</span></span>
<span data-ttu-id="10dac-121">Этот сценарий PowerShell поддерживает hello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="10dac-121">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="10dac-122">создание учетной записи запуска от имени с использованием самозаверяющего сертификата;</span><span class="sxs-lookup"><span data-stu-id="10dac-122">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="10dac-123">создание учетной записи запуска от имени и классической учетной записи запуска от имени с использованием самозаверяющего сертификата;</span><span class="sxs-lookup"><span data-stu-id="10dac-123">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="10dac-124">создание учетной записи запуска от имени и классической учетной записи запуска от имени Azure с использованием корпоративного сертификата;</span><span class="sxs-lookup"><span data-stu-id="10dac-124">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="10dac-125">Создайте учетную запись запуска от имени и классический учетной записи запуска с помощью самозаверяющего сертификата в облако Azure для государственных hello.</span><span class="sxs-lookup"><span data-stu-id="10dac-125">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="10dac-126">В зависимости от hello параметров настройки при выборе hello скрипт создает hello следующих элементов.</span><span class="sxs-lookup"><span data-stu-id="10dac-126">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="10dac-127">**Для учетной записи запуска от имени:**</span><span class="sxs-lookup"><span data-stu-id="10dac-127">**For Run As accounts:**</span></span>

* <span data-ttu-id="10dac-128">Создает Azure AD приложения toobe экспортируются вместе с любой hello самозаверяющий или enterprise открытый ключ сертификата, создает основной учетной записи службы для приложения hello в Azure AD и назначает hello роль участника для учетной записи hello в существующую подписка.</span><span class="sxs-lookup"><span data-stu-id="10dac-128">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="10dac-129">Можно изменить этот параметр tooOwner или любая другая роль.</span><span class="sxs-lookup"><span data-stu-id="10dac-129">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="10dac-130">Дополнительные сведения см. в статье [Управление доступом на основе ролей в службе автоматизации Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="10dac-130">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="10dac-131">Создает ресурс-контейнер сертификата службы автоматизации с именем *AzureRunAsCertificate* в hello указана учетная запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="10dac-131">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="10dac-132">Hello активов сертификат содержит закрытый ключ сертификата hello, используемого приложением hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="10dac-132">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="10dac-133">Создает ресурс подключения автоматизации с именем *AzureRunAsConnection* в hello указана учетная запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="10dac-133">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="10dac-134">ресурс-контейнер подключений Hello содержит идентификатор приложения hello, идентификатора клиента, идентификатор подписки и отпечаток сертификата.</span><span class="sxs-lookup"><span data-stu-id="10dac-134">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="10dac-135">**Для классической учетной записи запуска от имени Azure:**</span><span class="sxs-lookup"><span data-stu-id="10dac-135">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="10dac-136">Создает ресурс-контейнер сертификата службы автоматизации с именем *AzureClassicRunAsCertificate* в hello указана учетная запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="10dac-136">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="10dac-137">Hello активов сертификат содержит закрытый ключ сертификата hello используемый сертификат управления hello.</span><span class="sxs-lookup"><span data-stu-id="10dac-137">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="10dac-138">Создает ресурс подключения автоматизации с именем *AzureClassicRunAsConnection* в hello указана учетная запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="10dac-138">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="10dac-139">ресурс-контейнер подключений Hello содержит имя подписки hello, идентификатор подписки и имя актива сертификатов.</span><span class="sxs-lookup"><span data-stu-id="10dac-139">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="10dac-140">При выборе любой из параметров для создания классических запуска от имени учетной записи, после выполнения сценария hello передачи hello открытый сертификат управления (CER-файл с расширением) toohello хранения для подписки hello этой учетной записи автоматизации hello был создан в.</span><span class="sxs-lookup"><span data-stu-id="10dac-140">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

1. <span data-ttu-id="10dac-141">Сохраните следующий сценарий на компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="10dac-141">Save hello following script on your computer.</span></span> <span data-ttu-id="10dac-142">В этом примере, сохраните его с именем файла hello *New RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="10dac-142">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

        #Requires -RunAsAdministrator
         Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                      [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
           -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
           -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
           Sleep -s 10
           New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
           $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
           $Retries++;
        }
           return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
          $CertificateName = $AutomationAccountName+$CertifcateAssetName
          $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
          $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
          $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
          CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                    "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload hello .cer format of #CERT#"

             if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
             $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
             $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
             $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
             $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
             $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
             $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
             $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
             $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
             CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="10dac-143">На компьютере, запустите **Windows PowerShell** из hello **запустить** экрана с повышенными правами пользователя.</span><span class="sxs-lookup"><span data-stu-id="10dac-143">On your computer, start **Windows PowerShell** from hello **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="10dac-144">Из hello повышенными оболочка командной строки, toohello откройте папку, содержащую hello скрипт, созданный на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="10dac-144">From hello elevated command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>  
4. <span data-ttu-id="10dac-145">Выполните сценарий hello, используя значения параметров hello hello конфигурации, требуемую.</span><span class="sxs-lookup"><span data-stu-id="10dac-145">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="10dac-146">**Создание учетной записи запуска от имени с использованием самозаверяющего сертификата**</span><span class="sxs-lookup"><span data-stu-id="10dac-146">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="10dac-147">**Создание учетной записи запуска от имени и классической учетной записи запуска от имени с использованием самозаверяющего сертификата**</span><span class="sxs-lookup"><span data-stu-id="10dac-147">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="10dac-148">**Создание учетной записи запуска от имени и классической учетной записи запуска от имени Azure с использованием корпоративного сертификата**</span><span class="sxs-lookup"><span data-stu-id="10dac-148">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="10dac-149">**Создание учетной записи запуска от имени и классический учетной записи запуска с помощью самозаверяющего сертификата в облако Azure для государственных hello**</span><span class="sxs-lookup"><span data-stu-id="10dac-149">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="10dac-150">После выполнения сценария hello, появится запрос tooauthenticate с Azure.</span><span class="sxs-lookup"><span data-stu-id="10dac-150">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="10dac-151">Войдите с учетной записью, которая является членом роли администраторов подписки hello и соадминистратором подписки hello.</span><span class="sxs-lookup"><span data-stu-id="10dac-151">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="10dac-152">После успешного выполнения сценария hello Обратите внимание hello следующее:</span><span class="sxs-lookup"><span data-stu-id="10dac-152">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="10dac-153">При создании классического учетной записи запуска с общей самозаверяющего сертификата (CER-файл), hello скрипт создает и сохраняет его toohello в папке временных файлов на компьютере в пользовательском профиле hello *%USERPROFILE%\AppData\Local\Temp*, мы использовали сеанс PowerShell tooexecute hello.</span><span class="sxs-lookup"><span data-stu-id="10dac-153">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="10dac-154">Если вы создали классическую учетную запись запуска от имени с использованием открытого корпоративного сертификата (CER-файл), используйте этот сертификат.</span><span class="sxs-lookup"><span data-stu-id="10dac-154">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="10dac-155">Следуйте инструкциям hello [передачи toohello сертификата API управления классический портал Azure](../azure-api-management-certs.md)и последующей проверки hello конфигурации учетных данных с ресурсами классическое развертывание с помощью hello [пример кода tooauthenticate с Azure классические ресурсы развертывания](automation-verify-runas-authentication.md#classic-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="10dac-155">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with classic deployment resources by using hello [sample code tooauthenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="10dac-156">Если вы уже сделали *не* создания классических учетной записи запуска, проверки подлинности в ресурсах диспетчера ресурсов и проверка конфигурации hello учетных данных с помощью hello [пример кода для проверки подлинности с помощью службы управления ресурсы](automation-verify-runas-authentication.md#automation-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="10dac-156">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="10dac-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="10dac-157">Next steps</span></span>
* <span data-ttu-id="10dac-158">Дополнительные сведения о субъектах ссылаться слишком[участника-службы и объекты приложений](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="10dac-158">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="10dac-159">Дополнительные сведения о сертификатах и служб Azure см. в разделе слишком[Общие сведения о сертификатах для облачных служб Azure](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="10dac-159">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
