---
title: "Настройка доступа WinRM для виртуальной машины Azure | Документация Майкрософт"
description: "Настройте доступ WinRM для использования с виртуальной машиной Azure, созданной в модели развертывания Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9718e85b-d360-4621-90b8-0b0b84a21208
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/16/2016
ms.author: kasing
ms.openlocfilehash: 2d6533462400bc1d93d0d3b0227769784e2658a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="14161-103">Настройка доступа WinRM для виртуальных машин в Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="14161-103">Setting up WinRM access for Virtual Machines in Azure Resource Manager</span></span>
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a><span data-ttu-id="14161-104">WinRM в управлении службами Azure или Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="14161-104">WinRM in Azure Service Management vs Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* <span data-ttu-id="14161-105">Общие сведения об Azure Resource Manager см. в этой [статье](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="14161-105">For an overview of the Azure Resource Manager, please see this [article](../../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="14161-106">Сведения о различиях между управлением службами Azure и Azure Resource Manager см. в этой [статье](../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="14161-106">For differences between Azure Service Management and Azure Resource Manager, please see this [article](../../resource-manager-deployment-model.md)</span></span>

<span data-ttu-id="14161-107">Основное различие в настройке конфигурации WinRM между двумя стеками — это как на виртуальной машине устанавливается сертификат.</span><span class="sxs-lookup"><span data-stu-id="14161-107">The key difference in setting up WinRM configuration between the two stacks is how the certificate gets installed on the VM.</span></span> <span data-ttu-id="14161-108">В стеке Azure Resource Manager сертификаты моделируются как ресурсы, управляемые поставщиком ресурсов хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="14161-108">In the Azure Resource Manager stack, the certificates are modeled as resources managed by the Key Vault Resource Provider.</span></span> <span data-ttu-id="14161-109">Поэтому пользователь должен предоставить свой собственный сертификат и передать его в хранилище ключей, прежде чем использовать на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="14161-109">Therefore, the user needs to provide their own certificate and upload it to a Key Vault before using it in a VM.</span></span>

<span data-ttu-id="14161-110">Ниже приведены шаги, которые необходимо выполнить для настройки виртуальной машины с возможностью подключения WinRM:</span><span class="sxs-lookup"><span data-stu-id="14161-110">Here are the steps you need to take to set up a VM with WinRM connectivity</span></span>

1. <span data-ttu-id="14161-111">создать хранилище ключей;</span><span class="sxs-lookup"><span data-stu-id="14161-111">Create a Key Vault</span></span>
2. <span data-ttu-id="14161-112">создать самозаверяющий сертификат;</span><span class="sxs-lookup"><span data-stu-id="14161-112">Create a self-signed certificate</span></span>
3. <span data-ttu-id="14161-113">передать самозаверяющий сертификат в хранилище ключей;</span><span class="sxs-lookup"><span data-stu-id="14161-113">Upload your self-signed certificate to Key Vault</span></span>
4. <span data-ttu-id="14161-114">получить URL-адрес для самозаверяющего сертификата в хранилище ключей;</span><span class="sxs-lookup"><span data-stu-id="14161-114">Get the URL for your self-signed certificate in the Key Vault</span></span>
5. <span data-ttu-id="14161-115">сослаться на URL-адрес самозаверяющего сертификата при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="14161-115">Reference your self-signed certificates URL while creating a VM</span></span>

## <a name="step-1-create-a-key-vault"></a><span data-ttu-id="14161-116">Шаг 1. Создание хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="14161-116">Step 1: Create a Key Vault</span></span>
<span data-ttu-id="14161-117">Для создания хранилища ключей можно воспользоваться следующей командой:</span><span class="sxs-lookup"><span data-stu-id="14161-117">You can use the below command to create the Key Vault</span></span>

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a><span data-ttu-id="14161-118">Шаг 2. Создание самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="14161-118">Step 2: Create a self-signed certificate</span></span>
<span data-ttu-id="14161-119">Можно создать самозаверяющий сертификат с помощью этого сценария PowerShell.</span><span class="sxs-lookup"><span data-stu-id="14161-119">You can create a self-signed certificate using this PowerShell script</span></span>

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter the certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-to-the-key-vault"></a><span data-ttu-id="14161-120">Шаг 3. Передача самозаверяющего сертификата в хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="14161-120">Step 3: Upload your self-signed certificate to the Key Vault</span></span>
<span data-ttu-id="14161-121">Перед передачей сертификата в хранилище ключей, созданное на шаге 1, необходимо преобразовать его в формат, который будет понятен для поставщика ресурсов Microsoft.Compute.</span><span class="sxs-lookup"><span data-stu-id="14161-121">Before uploading the certificate to the Key Vault created in step 1, it needs to converted into a format the Microsoft.Compute resource provider will understand.</span></span> <span data-ttu-id="14161-122">Следующий сценарий PowerShell позволит это сделать:</span><span class="sxs-lookup"><span data-stu-id="14161-122">The below PowerShell script will allow you do that</span></span>

```
$fileName = "<Path to the .pfx file>"
$fileContentBytes = Get-Content $fileName -Encoding Byte
$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

$jsonObject = @"
{
  "data": "$filecontentencoded",
  "dataType" :"pfx",
  "password": "<password>"
}
"@

$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText –Force
Set-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>" -SecretValue $secret
```

## <a name="step-4-get-the-url-for-your-self-signed-certificate-in-the-key-vault"></a><span data-ttu-id="14161-123">Шаг 4. Получение URL-адреса для самозаверяющего сертификата в хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="14161-123">Step 4: Get the URL for your self-signed certificate in the Key Vault</span></span>
<span data-ttu-id="14161-124">При подготовке виртуальной машины поставщику ресурсов Microsoft.Compute требуется URL-адрес для секрета в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="14161-124">The Microsoft.Compute resource provider needs a URL to the secret inside the Key Vault while provisioning the VM.</span></span> <span data-ttu-id="14161-125">Это позволяет поставщику ресурсов Microsoft.Compute скачать секрет и создать эквивалент сертификата на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="14161-125">This enables the Microsoft.Compute resource provider to download the secret and create the equivalent certificate on the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="14161-126">URL-адрес секрета также должен включать в себя версию.</span><span class="sxs-lookup"><span data-stu-id="14161-126">The URL of the secret needs to include the version as well.</span></span> <span data-ttu-id="14161-127">Пример URL-адреса выглядит так: https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span><span class="sxs-lookup"><span data-stu-id="14161-127">An example URL looks like below https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span></span>
> 
> 

#### <a name="templates"></a><span data-ttu-id="14161-128">Шаблоны</span><span class="sxs-lookup"><span data-stu-id="14161-128">Templates</span></span>
<span data-ttu-id="14161-129">Получить ссылку на URL-адрес в шаблоне можно с помощью следующего кода:</span><span class="sxs-lookup"><span data-stu-id="14161-129">You can get the link to the URL in the template using the below code</span></span>

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a><span data-ttu-id="14161-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="14161-130">PowerShell</span></span>
<span data-ttu-id="14161-131">Также для получения этого URL-адреса можно воспользоваться следующей командой PowerShell:</span><span class="sxs-lookup"><span data-stu-id="14161-131">You can get this URL using the below PowerShell command</span></span>

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a><span data-ttu-id="14161-132">Шаг 5. Создание ссылки на URL-адрес самозаверяющего сертификата при создании виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="14161-132">Step 5: Reference your self-signed certificates URL while creating a VM</span></span>
#### <a name="azure-resource-manager-templates"></a><span data-ttu-id="14161-133">Шаблоны Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="14161-133">Azure Resource Manager Templates</span></span>
<span data-ttu-id="14161-134">При создании виртуальной машины с помощью шаблонов ссылки на сертификат задаются в разделе секретов и разделе winRM, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="14161-134">While creating a VM through templates, the certificate gets referenced in the secrets section and the winRM section as below:</span></span>

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of the Key Vault containing the secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for the certificate you got in Step 4>",
                  "certificateStore": "<Name of the certificate store on the VM>"
                }
              ]
            }
          ],
          "windowsConfiguration": {
            ...
            "winRM": {
              "listeners": [
                {
                  "protocol": "http"
                },
                {
                  "protocol": "https",
                  "certificateUrl": "<URL for the certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

<span data-ttu-id="14161-135">Пример шаблона для описанного выше сценария можно найти здесь: [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="14161-135">A sample template for the above can be found here at [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span></span>

<span data-ttu-id="14161-136">Исходный код для этого шаблона можно найти на портале [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="14161-136">Source code for this template can be found on [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span></span>

#### <a name="powershell"></a><span data-ttu-id="14161-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="14161-137">PowerShell</span></span>
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-to-the-vm"></a><span data-ttu-id="14161-138">Шаг 6. Подключение к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="14161-138">Step 6: Connecting to the VM</span></span>
<span data-ttu-id="14161-139">Перед подключением к виртуальной машине убедитесь, что машина настроена для удаленного управления WinRM.</span><span class="sxs-lookup"><span data-stu-id="14161-139">Before you can connect to the VM you'll need to make sure your machine is configured for WinRM remote management.</span></span> <span data-ttu-id="14161-140">Запустите PowerShell от имени администратора и выполните следующую команду, чтобы убедиться в правильности настроек:</span><span class="sxs-lookup"><span data-stu-id="14161-140">Start PowerShell as an administrator and execute the below command to make sure you're set up.</span></span>

    Enable-PSRemoting -Force

> [!NOTE]
> <span data-ttu-id="14161-141">Если вышеописанные действия не дали результата, убедитесь, что служба WinRM запущена.</span><span class="sxs-lookup"><span data-stu-id="14161-141">You might need to make sure the WinRM service is running if the above does not work.</span></span> <span data-ttu-id="14161-142">Это можно сделать с помощью команды `Get-Service WinRM`</span><span class="sxs-lookup"><span data-stu-id="14161-142">You can do that using `Get-Service WinRM`</span></span>
> 
> 

<span data-ttu-id="14161-143">Когда настройки выполнены, можно подключиться к виртуальной машине с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="14161-143">Once the setup is done, you can connect to the VM using the below command</span></span>

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
