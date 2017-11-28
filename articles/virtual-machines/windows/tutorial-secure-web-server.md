---
title: "aaaSecure IIS с помощью SSL-сертификаты в Azure | Документы Microsoft"
description: "Узнайте, как toosecure hello IIS веб-сервер с SSL-сертификаты на виртуальной Машине Windows в Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/14/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 7a9e0ce07be2f55095fdb5347b64faf5caa4f7e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="b4c40-103">Защита веб-сервера IIS с помощью SSL-сертификатов на виртуальной машине Windows в Azure</span><span class="sxs-lookup"><span data-stu-id="b4c40-103">Secure IIS web server with SSL certificates on a Windows virtual machine in Azure</span></span>
<span data-ttu-id="b4c40-104">toosecure веб-серверов, сертификат позже SSL (Secure Sockets) можно использовать tooencrypt веб-трафика.</span><span class="sxs-lookup"><span data-stu-id="b4c40-104">toosecure web servers, a Secure Sockets Later (SSL) certificate can be used tooencrypt web traffic.</span></span> <span data-ttu-id="b4c40-105">SSL-сертификаты могут храниться в хранилище ключей Azure и разрешать безопасного развертывания сертификатов tooWindows виртуальных машин (ВМ) в Azure.</span><span class="sxs-lookup"><span data-stu-id="b4c40-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates tooWindows virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="b4c40-106">Из этого руководства вы узнаете, как выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="b4c40-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b4c40-107">Создание Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="b4c40-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="b4c40-108">Создать или отправить сертификат toohello хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="b4c40-108">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="b4c40-109">Создайте виртуальную Машину и установите веб-сервера IIS hello</span><span class="sxs-lookup"><span data-stu-id="b4c40-109">Create a VM and install hello IIS web server</span></span>
> * <span data-ttu-id="b4c40-110">Вставить сертификат hello в hello виртуальной Машины и настроить службы IIS с помощью SSL-привязки</span><span class="sxs-lookup"><span data-stu-id="b4c40-110">Inject hello certificate into hello VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="b4c40-111">Этот учебник требует hello Azure PowerShell модуль версии 3.6 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="b4c40-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="b4c40-112">Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="b4c40-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="b4c40-113">Получить tooupgrade [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="b4c40-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="overview"></a><span data-ttu-id="b4c40-114">Обзор</span><span class="sxs-lookup"><span data-stu-id="b4c40-114">Overview</span></span>
<span data-ttu-id="b4c40-115">Azure Key Vault защищает криптографические ключи и секреты, в том числе сертификаты или пароли.</span><span class="sxs-lookup"><span data-stu-id="b4c40-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="b4c40-116">Хранилище ключей помогает ускорить процесс управления сертификата hello и позволяет toomaintain управление ключами, которые обращаются к этих сертификатов.</span><span class="sxs-lookup"><span data-stu-id="b4c40-116">Key Vault helps streamline hello certificate management process and enables you toomaintain control of keys that access those certificates.</span></span> <span data-ttu-id="b4c40-117">Можно создать самозаверяющий сертификат в Key Vault или передать существующий доверенный сертификат.</span><span class="sxs-lookup"><span data-stu-id="b4c40-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="b4c40-118">Вместо того чтобы использовать образ виртуальной машины, включающий встроенные сертификаты, можно внедрить сертификаты в работающую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="b4c40-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="b4c40-119">Этот процесс гарантирует, что hello наиболее актуальные сертификаты установлены на веб-сервере во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="b4c40-119">This process ensures that hello most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="b4c40-120">Если обновления или замены сертификата, также нет toocreate нового пользовательского образа виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="b4c40-120">If you renew or replace a certificate, you don't also have toocreate a new custom VM image.</span></span> <span data-ttu-id="b4c40-121">Hello последние сертификаты добавляются автоматически при создании дополнительных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b4c40-121">hello latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="b4c40-122">В процессе hello всей hello сертификаты никогда не оставить hello платформы Azure или, представлены в скрипт, командной строки журнала или шаблона.</span><span class="sxs-lookup"><span data-stu-id="b4c40-122">During hello whole process, hello certificates never leave hello Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="b4c40-123">Создание Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="b4c40-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="b4c40-124">Прежде чем создать Key Vault и сертификаты, выполните командлет [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup), чтобы создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b4c40-124">Before you can create a Key Vault and certificates, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="b4c40-125">Hello следующий пример создает группу ресурсов с именем *myResourceGroupSecureWeb* в hello *Восток США* расположение:</span><span class="sxs-lookup"><span data-stu-id="b4c40-125">hello following example creates a resource group named *myResourceGroupSecureWeb* in hello *East US* location:</span></span>

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

<span data-ttu-id="b4c40-126">Чтобы создать Key Vault, используйте командлет [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span><span class="sxs-lookup"><span data-stu-id="b4c40-126">Next, create a Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span></span> <span data-ttu-id="b4c40-127">У каждого Key Vault должно быть уникальное имя в нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="b4c40-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="b4c40-128">Замените `<mykeyvault>` в hello следующий пример с собственное уникальное имя хранилища ключей:</span><span class="sxs-lookup"><span data-stu-id="b4c40-128">Replace `<mykeyvault>` in hello following example with your own unique Key Vault name:</span></span>

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="b4c40-129">Создание сертификата и его сохранение в Key Vault</span><span class="sxs-lookup"><span data-stu-id="b4c40-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="b4c40-130">Для использования в рабочей среде импортируйте действительный сертификат, подписанный доверенным поставщиком, выполнив командлет [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span><span class="sxs-lookup"><span data-stu-id="b4c40-130">For production use, you should import a valid certificate signed by trusted provider with [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span></span> <span data-ttu-id="b4c40-131">В этом учебнике hello следующем примере показано, как можно создать самозаверяющий сертификат с [добавить AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) hello, используется политика по умолчанию из [ Новый AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span><span class="sxs-lookup"><span data-stu-id="b4c40-131">For this tutorial, hello following example shows how you can generate a self-signed certificate with [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) that uses hello default certificate policy from [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span></span> 

```powershell
$policy = New-AzureKeyVaultCertificatePolicy `
    -SubjectName "CN=www.contoso.com" `
    -SecretContentType "application/x-pkcs12" `
    -IssuerName Self `
    -ValidityInMonths 12

Add-AzureKeyVaultCertificate `
    -VaultName $keyvaultName `
    -Name "mycert" `
    -CertificatePolicy $policy 
```


## <a name="create-a-virtual-machine"></a><span data-ttu-id="b4c40-132">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="b4c40-132">Create a virtual machine</span></span>
<span data-ttu-id="b4c40-133">Имя пользователя администратора и пароль для hello ВМ с набора [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="b4c40-133">Set an administrator username and password for hello VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="b4c40-134">Теперь можно создавать hello виртуальной Машины с [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="b4c40-134">Now you can create hello VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="b4c40-135">Hello следующий пример создает компоненты hello необходимые виртуальной сети, конфигурации hello ОС и затем создает Виртуальную машину с именем *myVM*:</span><span class="sxs-lookup"><span data-stu-id="b4c40-135">hello following example creates hello required virtual network components, hello OS configuration, and then creates a VM named *myVM*:</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myVnet" `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleRDP"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 443
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleWWW"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name "myNic" `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS2" | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName "myVM" -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName "MicrosoftWindowsServer" `
    -Offer "WindowsServer" -Skus "2016-Datacenter" -Version "latest" | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Create virtual machine
New-AzureRmVM -ResourceGroupName $resourceGroup -Location $location -VM $vmConfig

# Use hello Custom Script Extension tooinstall IIS
Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server -IncludeManagementTools"}'
```

<span data-ttu-id="b4c40-136">Он занимает несколько минут для создания toobe ВМ hello.</span><span class="sxs-lookup"><span data-stu-id="b4c40-136">It takes a few minutes for hello VM toobe created.</span></span> <span data-ttu-id="b4c40-137">Hello последний шаг использует hello Azure настраиваемое расширение скриптов tooinstall hello веб-сервера IIS с [AzureRmVmExtension набор](/powershell/module/azurerm.compute/set-azurermvmextension).</span><span class="sxs-lookup"><span data-stu-id="b4c40-137">hello last step uses hello Azure Custom Script Extension tooinstall hello IIS web server with [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span></span>


## <a name="add-a-certificate-toovm-from-key-vault"></a><span data-ttu-id="b4c40-138">Добавить tooVM сертификат из хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="b4c40-138">Add a certificate tooVM from Key Vault</span></span>
<span data-ttu-id="b4c40-139">tooadd hello сертификат из хранилища ключей tooa виртуальной Машины, получить hello Удостоверение сертификата с [Get AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="b4c40-139">tooadd hello certificate from Key Vault tooa VM, obtain hello ID of your certificate with [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span></span> <span data-ttu-id="b4c40-140">Добавление сертификата hello toohello виртуальной Машины с [AzureRmVMSecret добавить](/powershell/module/azurerm.compute/add-azurermvmsecret):</span><span class="sxs-lookup"><span data-stu-id="b4c40-140">Add hello certificate toohello VM with [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span></span>

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-toouse-hello-certificate"></a><span data-ttu-id="b4c40-141">Настройка сертификата hello toouse IIS</span><span class="sxs-lookup"><span data-stu-id="b4c40-141">Configure IIS toouse hello certificate</span></span>
<span data-ttu-id="b4c40-142">Используйте hello настраиваемое расширение скриптов с [AzureRmVMExtension набор](/powershell/module/azurerm.compute/set-azurermvmextension) конфигурации IIS tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="b4c40-142">Use hello Custom Script Extension again with [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooupdate hello IIS configuration.</span></span> <span data-ttu-id="b4c40-143">Это обновление применяется hello сертификат из хранилища ключей tooIIS вставлен и настраивает hello-привязку веб:</span><span class="sxs-lookup"><span data-stu-id="b4c40-143">This update applies hello certificate injected from Key Vault tooIIS and configures hello web binding:</span></span>

```powershell
$PublicSettings = '{
    "fileUris":["https://raw.githubusercontent.com/iainfoulds/azure-samples/master/secure-iis.ps1"],
    "commandToExecute":"powershell -ExecutionPolicy Unrestricted -File secure-iis.ps1"
}'

Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString $publicSettings
```


### <a name="test-hello-secure-web-app"></a><span data-ttu-id="b4c40-144">Тест hello безопасного веб-приложения</span><span class="sxs-lookup"><span data-stu-id="b4c40-144">Test hello secure web app</span></span>
<span data-ttu-id="b4c40-145">Получить hello общедоступный IP-адрес виртуальной Машины с [Get AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="b4c40-145">Obtain hello public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="b4c40-146">Hello следующий пример извлекает hello IP-адрес для `myPublicIP` созданную ранее:</span><span class="sxs-lookup"><span data-stu-id="b4c40-146">hello following example obtains hello IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="b4c40-147">Теперь можно открыть веб-браузер и введите `https://<myPublicIP>` в адресную строку hello.</span><span class="sxs-lookup"><span data-stu-id="b4c40-147">Now you can open a web browser and enter `https://<myPublicIP>` in hello address bar.</span></span> <span data-ttu-id="b4c40-148">предупреждения безопасности hello tooaccept, если используется самозаверяющий сертификат, выберите **сведения** и затем **перейдите на веб-странице toohello**:</span><span class="sxs-lookup"><span data-stu-id="b4c40-148">tooaccept hello security warning if you used a self-signed certificate, select **Details** and then **Go on toohello webpage**:</span></span>

![Принятие предупреждения о безопасности веб-браузера](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="b4c40-150">Защищенные веб-сайт IIS отображается как hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="b4c40-150">Your secured IIS website is then displayed as in hello following example:</span></span>

![Просмотр работающего защищенного сайта IIS](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a><span data-ttu-id="b4c40-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b4c40-152">Next steps</span></span>

<span data-ttu-id="b4c40-153">С помощью этого руководства вы защитили веб-сервер IIS SSL-сертификатом, который хранится в Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="b4c40-153">In this tutorial, you secured an IIS web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="b4c40-154">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="b4c40-154">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b4c40-155">Создание Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="b4c40-155">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="b4c40-156">Создать или отправить сертификат toohello хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="b4c40-156">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="b4c40-157">Создайте виртуальную Машину и установите веб-сервера IIS hello</span><span class="sxs-lookup"><span data-stu-id="b4c40-157">Create a VM and install hello IIS web server</span></span>
> * <span data-ttu-id="b4c40-158">Вставить сертификат hello в hello виртуальной Машины и настроить службы IIS с помощью SSL-привязки</span><span class="sxs-lookup"><span data-stu-id="b4c40-158">Inject hello certificate into hello VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="b4c40-159">Выполните этот toosee ссылку готовые примеры скриптов для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b4c40-159">Follow this link toosee pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b4c40-160">Примеры скриптов для виртуальной машины Windows</span><span class="sxs-lookup"><span data-stu-id="b4c40-160">Windows virtual machine script samples</span></span>](./powershell-samples.md)