---
title: "aaaSet доступа для удаленного управления Windows для ВМ Azure | Документы Microsoft"
description: "Настройка WinRM доступ для использования с виртуальной машины Azure создаются в модели развертывания диспетчера ресурсов hello."
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
ms.openlocfilehash: 23d1d3a3065cbd8e4036be085c6d835cae36caae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="08d37-103">Настройка доступа WinRM для виртуальных машин в Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="08d37-103">Setting up WinRM access for Virtual Machines in Azure Resource Manager</span></span>
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a><span data-ttu-id="08d37-104">WinRM в управлении службами Azure или Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="08d37-104">WinRM in Azure Service Management vs Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* <span data-ttu-id="08d37-105">Общие сведения о hello диспетчера ресурсов Azure, см. в разделе это [статьи](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="08d37-105">For an overview of hello Azure Resource Manager, please see this [article](../../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="08d37-106">Сведения о различиях между управлением службами Azure и Azure Resource Manager см. в этой [статье](../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="08d37-106">For differences between Azure Service Management and Azure Resource Manager, please see this [article](../../resource-manager-deployment-model.md)</span></span>

<span data-ttu-id="08d37-107">Hello ключевое различие в настройке конфигурации WinRM между двумя стеками hello происходит сертификат hello возвращает Установка hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="08d37-107">hello key difference in setting up WinRM configuration between hello two stacks is how hello certificate gets installed on hello VM.</span></span> <span data-ttu-id="08d37-108">В стеке диспетчера ресурсов Azure hello сертификаты hello моделируются как ресурсы, управляемые hello поставщика ресурсов хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="08d37-108">In hello Azure Resource Manager stack, hello certificates are modeled as resources managed by hello Key Vault Resource Provider.</span></span> <span data-ttu-id="08d37-109">Таким образом пользователь hello должен tooprovide свой собственный сертификат и отправить tooa хранилище ключей перед их использованием в виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="08d37-109">Therefore, hello user needs tooprovide their own certificate and upload it tooa Key Vault before using it in a VM.</span></span>

<span data-ttu-id="08d37-110">Ниже приведены шаги hello необходимо tooset tootake ВМ с подключением удаленного управления Windows</span><span class="sxs-lookup"><span data-stu-id="08d37-110">Here are hello steps you need tootake tooset up a VM with WinRM connectivity</span></span>

1. <span data-ttu-id="08d37-111">создать хранилище ключей;</span><span class="sxs-lookup"><span data-stu-id="08d37-111">Create a Key Vault</span></span>
2. <span data-ttu-id="08d37-112">Создание самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="08d37-112">Create a self-signed certificate</span></span>
3. <span data-ttu-id="08d37-113">Отправьте ваш tooKey самозаверяющий сертификат хранилища</span><span class="sxs-lookup"><span data-stu-id="08d37-113">Upload your self-signed certificate tooKey Vault</span></span>
4. <span data-ttu-id="08d37-114">Получение URL-адреса hello самозаверяющего сертификата в хранилище ключей hello</span><span class="sxs-lookup"><span data-stu-id="08d37-114">Get hello URL for your self-signed certificate in hello Key Vault</span></span>
5. <span data-ttu-id="08d37-115">сослаться на URL-адрес самозаверяющего сертификата при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="08d37-115">Reference your self-signed certificates URL while creating a VM</span></span>

## <a name="step-1-create-a-key-vault"></a><span data-ttu-id="08d37-116">Шаг 1. Создание хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="08d37-116">Step 1: Create a Key Vault</span></span>
<span data-ttu-id="08d37-117">Можно использовать hello ниже команда toocreate hello хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="08d37-117">You can use hello below command toocreate hello Key Vault</span></span>

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a><span data-ttu-id="08d37-118">Шаг 2. Создание самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="08d37-118">Step 2: Create a self-signed certificate</span></span>
<span data-ttu-id="08d37-119">Можно создать самозаверяющий сертификат с помощью этого сценария PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08d37-119">You can create a self-signed certificate using this PowerShell script</span></span>

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter hello certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-toohello-key-vault"></a><span data-ttu-id="08d37-120">Шаг 3: Отправка вашей toohello самозаверяющий сертификат хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="08d37-120">Step 3: Upload your self-signed certificate toohello Key Vault</span></span>
<span data-ttu-id="08d37-121">Перед созданием отправка сертификата hello toohello хранилища ключей на шаге 1, в формате hello, понимали, поставщик ресурсов Microsoft.Compute ему tooconverted.</span><span class="sxs-lookup"><span data-stu-id="08d37-121">Before uploading hello certificate toohello Key Vault created in step 1, it needs tooconverted into a format hello Microsoft.Compute resource provider will understand.</span></span> <span data-ttu-id="08d37-122">Разрешает Hello ниже сценарий PowerShell, необходимо</span><span class="sxs-lookup"><span data-stu-id="08d37-122">hello below PowerShell script will allow you do that</span></span>

```
$fileName = "<Path toohello .pfx file>"
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

## <a name="step-4-get-hello-url-for-your-self-signed-certificate-in-hello-key-vault"></a><span data-ttu-id="08d37-123">Шаг 4: Получение hello URL-адреса для самозаверяющего сертификата в хранилище ключей hello</span><span class="sxs-lookup"><span data-stu-id="08d37-123">Step 4: Get hello URL for your self-signed certificate in hello Key Vault</span></span>
<span data-ttu-id="08d37-124">Hello поставщике ресурсов Microsoft.Compute должен секрета toohello URL-адрес внутри hello хранилища ключей во время подготовки hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="08d37-124">hello Microsoft.Compute resource provider needs a URL toohello secret inside hello Key Vault while provisioning hello VM.</span></span> <span data-ttu-id="08d37-125">Это позволяет hello Microsoft.Compute ресурсов поставщика toodownload hello секрета и создайте сертификат эквивалентные hello hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="08d37-125">This enables hello Microsoft.Compute resource provider toodownload hello secret and create hello equivalent certificate on hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="08d37-126">URL-адрес Hello hello секрет должен также версия hello tooinclude.</span><span class="sxs-lookup"><span data-stu-id="08d37-126">hello URL of hello secret needs tooinclude hello version as well.</span></span> <span data-ttu-id="08d37-127">Пример URL-адреса выглядит так: https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span><span class="sxs-lookup"><span data-stu-id="08d37-127">An example URL looks like below https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span></span>
> 
> 

#### <a name="templates"></a><span data-ttu-id="08d37-128">Шаблоны</span><span class="sxs-lookup"><span data-stu-id="08d37-128">Templates</span></span>
<span data-ttu-id="08d37-129">URL-адрес toohello hello ссылки можно получить в шаблон hello, используя hello ниже код</span><span class="sxs-lookup"><span data-stu-id="08d37-129">You can get hello link toohello URL in hello template using hello below code</span></span>

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a><span data-ttu-id="08d37-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="08d37-130">PowerShell</span></span>
<span data-ttu-id="08d37-131">Вы можете получить этот URL-адрес, используя hello ниже команды PowerShell</span><span class="sxs-lookup"><span data-stu-id="08d37-131">You can get this URL using hello below PowerShell command</span></span>

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a><span data-ttu-id="08d37-132">Шаг 5. Создание ссылки на URL-адрес самозаверяющего сертификата при создании виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="08d37-132">Step 5: Reference your self-signed certificates URL while creating a VM</span></span>
#### <a name="azure-resource-manager-templates"></a><span data-ttu-id="08d37-133">Шаблоны Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="08d37-133">Azure Resource Manager Templates</span></span>
<span data-ttu-id="08d37-134">При создании ВМ с помощью шаблонов, сертификат hello возвращает ссылаться секреты hello и разделов winRM hello, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="08d37-134">While creating a VM through templates, hello certificate gets referenced in hello secrets section and hello winRM section as below:</span></span>

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of hello Key Vault containing hello secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for hello certificate you got in Step 4>",
                  "certificateStore": "<Name of hello certificate store on hello VM>"
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
                  "certificateUrl": "<URL for hello certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

<span data-ttu-id="08d37-135">Образец шаблона для hello выше приведены ниже в [201-vm-winrm-keyvault — windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="08d37-135">A sample template for hello above can be found here at [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span></span>

<span data-ttu-id="08d37-136">Исходный код для этого шаблона можно найти на портале [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="08d37-136">Source code for this template can be found on [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span></span>

#### <a name="powershell"></a><span data-ttu-id="08d37-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="08d37-137">PowerShell</span></span>
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-toohello-vm"></a><span data-ttu-id="08d37-138">Шаг 6: Подключение toohello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="08d37-138">Step 6: Connecting toohello VM</span></span>
<span data-ttu-id="08d37-139">Перед подключением toohello виртуальной Машины необходимо убедиться, что компьютер настроен для удаленного управления WinRM toomake.</span><span class="sxs-lookup"><span data-stu-id="08d37-139">Before you can connect toohello VM you'll need toomake sure your machine is configured for WinRM remote management.</span></span> <span data-ttu-id="08d37-140">Запустите PowerShell с правами администратора и выполните hello ниже команда toomake том, что настройки нужных параметров.</span><span class="sxs-lookup"><span data-stu-id="08d37-140">Start PowerShell as an administrator and execute hello below command toomake sure you're set up.</span></span>

    Enable-PSRemoting -Force

> [!NOTE]
> <span data-ttu-id="08d37-141">Может потребоваться toomake том, что hello служба WinRM работает в том случае, если выше hello не работает.</span><span class="sxs-lookup"><span data-stu-id="08d37-141">You might need toomake sure hello WinRM service is running if hello above does not work.</span></span> <span data-ttu-id="08d37-142">Это можно сделать с помощью команды `Get-Service WinRM`</span><span class="sxs-lookup"><span data-stu-id="08d37-142">You can do that using `Get-Service WinRM`</span></span>
> 
> 

<span data-ttu-id="08d37-143">После завершения установки hello toohello ВМ можно подключиться с помощью hello ниже команды</span><span class="sxs-lookup"><span data-stu-id="08d37-143">Once hello setup is done, you can connect toohello VM using hello below command</span></span>

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
