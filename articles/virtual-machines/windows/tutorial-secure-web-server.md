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
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a>Защита веб-сервера IIS с помощью SSL-сертификатов на виртуальной машине Windows в Azure
toosecure веб-серверов, сертификат позже SSL (Secure Sockets) можно использовать tooencrypt веб-трафика. SSL-сертификаты могут храниться в хранилище ключей Azure и разрешать безопасного развертывания сертификатов tooWindows виртуальных машин (ВМ) в Azure. Из этого руководства вы узнаете, как выполнить следующие задачи:

> [!div class="checklist"]
> * Создание Azure Key Vault
> * Создать или отправить сертификат toohello хранилища ключей
> * Создайте виртуальную Машину и установите веб-сервера IIS hello
> * Вставить сертификат hello в hello виртуальной Машины и настроить службы IIS с помощью SSL-привязки

Этот учебник требует hello Azure PowerShell модуль версии 3.6 или более поздней версии. Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello. Получить tooupgrade [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).


## <a name="overview"></a>Обзор
Azure Key Vault защищает криптографические ключи и секреты, в том числе сертификаты или пароли. Хранилище ключей помогает ускорить процесс управления сертификата hello и позволяет toomaintain управление ключами, которые обращаются к этих сертификатов. Можно создать самозаверяющий сертификат в Key Vault или передать существующий доверенный сертификат.

Вместо того чтобы использовать образ виртуальной машины, включающий встроенные сертификаты, можно внедрить сертификаты в работающую виртуальную машину. Этот процесс гарантирует, что hello наиболее актуальные сертификаты установлены на веб-сервере во время развертывания. Если обновления или замены сертификата, также нет toocreate нового пользовательского образа виртуальной Машины. Hello последние сертификаты добавляются автоматически при создании дополнительных виртуальных машин. В процессе hello всей hello сертификаты никогда не оставить hello платформы Azure или, представлены в скрипт, командной строки журнала или шаблона.


## <a name="create-an-azure-key-vault"></a>Создание Azure Key Vault
Прежде чем создать Key Vault и сертификаты, выполните командлет [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup), чтобы создать группу ресурсов. Hello следующий пример создает группу ресурсов с именем *myResourceGroupSecureWeb* в hello *Восток США* расположение:

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

Чтобы создать Key Vault, используйте командлет [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault). У каждого Key Vault должно быть уникальное имя в нижнем регистре. Замените `<mykeyvault>` в hello следующий пример с собственное уникальное имя хранилища ключей:

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a>Создание сертификата и его сохранение в Key Vault
Для использования в рабочей среде импортируйте действительный сертификат, подписанный доверенным поставщиком, выполнив командлет [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate). В этом учебнике hello следующем примере показано, как можно создать самозаверяющий сертификат с [добавить AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) hello, используется политика по умолчанию из [ Новый AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy). 

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


## <a name="create-a-virtual-machine"></a>Создание виртуальной машины
Имя пользователя администратора и пароль для hello ВМ с набора [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Теперь можно создавать hello виртуальной Машины с [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). Hello следующий пример создает компоненты hello необходимые виртуальной сети, конфигурации hello ОС и затем создает Виртуальную машину с именем *myVM*:

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

Он занимает несколько минут для создания toobe ВМ hello. Hello последний шаг использует hello Azure настраиваемое расширение скриптов tooinstall hello веб-сервера IIS с [AzureRmVmExtension набор](/powershell/module/azurerm.compute/set-azurermvmextension).


## <a name="add-a-certificate-toovm-from-key-vault"></a>Добавить tooVM сертификат из хранилища ключей
tooadd hello сертификат из хранилища ключей tooa виртуальной Машины, получить hello Удостоверение сертификата с [Get AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret). Добавление сертификата hello toohello виртуальной Машины с [AzureRmVMSecret добавить](/powershell/module/azurerm.compute/add-azurermvmsecret):

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-toouse-hello-certificate"></a>Настройка сертификата hello toouse IIS
Используйте hello настраиваемое расширение скриптов с [AzureRmVMExtension набор](/powershell/module/azurerm.compute/set-azurermvmextension) конфигурации IIS tooupdate hello. Это обновление применяется hello сертификат из хранилища ключей tooIIS вставлен и настраивает hello-привязку веб:

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


### <a name="test-hello-secure-web-app"></a>Тест hello безопасного веб-приложения
Получить hello общедоступный IP-адрес виртуальной Машины с [Get AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress). Hello следующий пример извлекает hello IP-адрес для `myPublicIP` созданную ранее:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

Теперь можно открыть веб-браузер и введите `https://<myPublicIP>` в адресную строку hello. предупреждения безопасности hello tooaccept, если используется самозаверяющий сертификат, выберите **сведения** и затем **перейдите на веб-странице toohello**:

![Принятие предупреждения о безопасности веб-браузера](./media/tutorial-secure-web-server/browser-warning.png)

Защищенные веб-сайт IIS отображается как hello в следующем примере:

![Просмотр работающего защищенного сайта IIS](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a>Дальнейшие действия

С помощью этого руководства вы защитили веб-сервер IIS SSL-сертификатом, который хранится в Azure Key Vault. Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * Создание Azure Key Vault
> * Создать или отправить сертификат toohello хранилища ключей
> * Создайте виртуальную Машину и установите веб-сервера IIS hello
> * Вставить сертификат hello в hello виртуальной Машины и настроить службы IIS с помощью SSL-привязки

Выполните этот toosee ссылку готовые примеры скриптов для виртуальной машины.

> [!div class="nextstepaction"]
> [Примеры скриптов для виртуальной машины Windows](./powershell-samples.md)