---
title: "aaaEncrypt дисков на виртуальной Машине Windows в Azure | Документы Microsoft"
description: "Как tooencrypt виртуальным дискам на виртуальной Машине Windows для улучшенной безопасности, с помощью Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/10/2017
ms.author: iainfou
ms.openlocfilehash: 77c42a67cb57a9dc5fe3159fce0be75e3a965be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-windows-vm"></a>Как tooencrypt виртуальных дисков на виртуальной Машине Windows
Для улучшения уровня безопасности и соответствия требованиям виртуальной машины содержание виртуальных дисков в Azure можно зашифровать. Диски можно зашифровать с использованием криптографических ключей, защищенных в хранилище ключей Azure. Вы будете управлять этими криптографическими ключами и проводить аудит их использования. Это статье сведения как tooencrypt виртуальных дисков на виртуальной Машине Windows, с помощью Azure PowerShell. Вы также можете [шифрования ВМ Linux с помощью Azure CLI 2.0 hello](../linux/encrypt-disks.md).

## <a name="overview-of-disk-encryption"></a>Общие сведения о шифровании дисков
Виртуальные диски на виртуальных машинах Windows шифруются в неактивном состоянии с помощью Bitlocker. В Azure за шифрование виртуальных дисков плата не взимается. Ключи шифрования хранятся в хранилище ключей Azure с помощью защиты программного обеспечения, или можно импортировать или создавать ключи в аппаратных модулях безопасности (HSM) сертифицированные tooFIPS стандартов 140-2 уровня 2. Эти ключи шифрования, используемые tooencrypt и расшифровки tooyour подключенных виртуальных дисков виртуальной Машины. Вы сохраняете контроль над этими криптографическими ключами и можете проводить аудит их использования. Субъект-служба Azure Active Directory предоставляет безопасный механизм для выдачи этих криптографических ключей при включении и отключении виртуальных машин.

Hello процесс шифрования виртуальной Машины выглядит следующим образом:

1. Создайте криптографический ключ в хранилище ключей Azure.
2. Настройте hello криптографических ключей toobe может использоваться для шифрования дисков.
3. tooread hello криптографический ключ из хранилища ключей Azure, hello создания участника службы Azure Active Directory с соответствующими разрешениями hello.
4. Выдавать виртуальных дисков, указание hello участника-службы Azure Active Directory и использовать соответствующие криптографических ключей toobe tooencrypt команда hello.
5. запросы основной службы Azure Active Directory Hello hello требуется криптографический ключ из хранилища ключей Azure.
6. виртуальные диски Hello шифруются с помощью предоставленных hello криптографический ключ.

## <a name="encryption-process"></a>Процесс шифрования
Шифрование диска основывается на hello следующие дополнительные компоненты:

* **Хранилище ключей Azure** -использовать toosafeguard криптографических ключей и используемая для шифрования и расшифровки диска hello. 
  * При наличии можно воспользоваться имеющимся хранилищем ключей Azure. У вас toodedicate дисков tooencrypting хранилища ключей.
  * tooseparate административные границы и видимость ключа, можно создать выделенный хранилища ключей.
* **Azure Active Directory** - дескрипторы hello безопасный обмен необходимых ключей шифрования и проверки подлинности для запрошенного действия. 
  * Как правило, для размещения приложения можно использовать имеющийся экземпляр Azure Active Directory.
  * Субъект-служба Hello предоставляет toorequest безопасный механизм и выдаваться hello соответствующих криптографических ключей. При этом вы не разрабатываете фактическое приложение, которое интегрируется с Azure Active Directory.

## <a name="requirements-and-limitations"></a>Требования и ограничения
Поддерживаемые сценарии и требования для шифрования дисков:

* включение шифрования для новых виртуальных машин Windows из образов Azure Marketplace или пользовательского образа виртуального жесткого диска;
* включение шифрования для имеющихся виртуальных машин в Azure;
* включение шифрования для виртуальных машин Windows, использующих дисковые пространства;
* отключение шифрования дисков данных и дисков операционной системы виртуальных машин Windows;
* Все ресурсы (например, хранилище ключей, учетной записи хранилища и виртуальных Машин), должны быть в hello и подписка одного региона Azure.
* виртуальные машины уровня "Стандартный", такие как серии A, D, DS, G и GS.

Шифрование диска не поддерживается в настоящее время в hello следующие сценарии:

* виртуальные машины уровня "Базовый";
* Виртуальные машины, созданные с помощью hello классической модели развертывания.
* Обновление криптографических ключей hello на Виртуальной машине уже зашифрованный.
* интеграция с локальной службой управления ключами.

## <a name="create-azure-key-vault-and-keys"></a>Создание Azure Key Vault и ключей
Прежде чем начать, убедитесь, что последняя версия hello hello установлен модуль Azure PowerShell. Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview). В примерах команд hello замените все параметры в примере с именами, расположение и значения ключа. Hello следующих примерах используется соглашение о *myResourceGroup*, *myKeyVault*, *myVM*и т. д.

Hello первым шагом является toocreate toostore хранилище ключей Azure криптографические ключи. Хранилище ключей Azure можно хранить ключи секретные данные, или пароли, которые позволяют вам toosecurely их реализации в приложениях и службах. Для шифрования диска создайте криптографический ключ, который будет использоваться tooencrypt toostore хранилище ключей или расшифровать виртуальных дисков. 

Включение hello поставщика хранилища ключей Azure в подписке Azure с [регистра AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), затем создайте группу ресурсов с [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Hello следующий пример создает имя группы ресурсов *myResourceGroup* в hello *Восток США* расположение:

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

Hello хранилище ключей Azure содержащего hello криптографических ключей и связанные вычислений, ресурсы, такие как хранилища и hello самой ВМ должны находиться в hello в одном регионе. Создание хранилища ключей Azure с [New AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) и включите hello хранилища ключей для шифрования диска. Укажите уникальное имя Key Vault для параметра *keyVaultName*, выполнив следующую команду:

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

Хранить криптографические ключи можно с помощью программного обеспечения или защиты HSM. Для использования HSM требуется хранилище ключей уровня "Премиум". Нет дополнительных затрат toocreating premium, хранилище ключей, а не стандартный хранилища ключей, которое хранит программно защищенных ключей. добавить toocreate premium хранилище ключей в предшествующих шаг hello hello *- Sku «Premium»* параметров. Hello следующий пример использует программно защищенных ключей создания стандартных хранилища ключей. 

Для обеих моделей защиты hello платформы Azure должен toobe предоставленные криптографические ключи доступа toorequest hello hello виртуальной Машины загружается toodecrypt hello виртуальных дисков. Создайте криптографический ключ в своем Key Vault, выполнив команду [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey). Hello следующий пример создает раздел с именем *myKey*:

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-hello-azure-active-directory-service-principal"></a>Создать участника-службы Azure Active Directory hello
При виртуальные диски зашифрованные или расшифрованные, необходимо указать hello toohandle проверки подлинности учетной записи и обмена ключей шифрования из хранилища ключей. Эта учетная запись субъекта-службы Azure Active Directory, позволяет toorequest платформы Azure hello hello соответствующие криптографических ключей от имени hello виртуальной Машины. Экземпляр Azure Active Directory по умолчанию доступен в вашей подписке, хотя во многих организациях есть выделенные каталоги Azure Active Directory.

Создайте субъект-службу в Azure Active Directory, выполнив команду [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal). toospecify безопасного пароля, выполните hello [ограничения в Azure Active Directory и политики паролей](../../active-directory/active-directory-passwords-policy.md):

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

toosuccessfully шифрования или расшифровки виртуальные диски, разрешения на hello криптографический ключ, хранящийся в хранилище ключей должно быть основной tooread ключей hello hello Azure Active Directory набора toopermit службы. Задайте разрешение для Key Vault, выполнив команду [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a>Создание виртуальной машины
tootest Здравствуйте, процесс шифрования, давайте создадим виртуальной Машины. Hello следующий пример создает Виртуальную машину с именем *myVM* с помощью *Windows Server 2016 Datacenter* изображения:

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "mypublicdns$(Get-Random)"

$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$cred = Get-Credential

$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```


## <a name="encrypt-virtual-machine"></a>Шифрование виртуальной машины
tooencrypt hello виртуальные диски, можно объединить все предыдущие компоненты hello:

1. Укажите hello субъекта-службы Azure Active Directory и пароль.
2. Укажите метаданные hello toostore hello хранилища ключей для зашифрованных дисков.
3. Укажите toouse hello ключи шифрования для hello фактического шифрования и расшифровки.
4. Укажите, следует ли tooencrypt hello ОС диска, диски с данными hello или все.

Шифрование ВМ с [AzureRmVMDiskEncryptionExtension набор](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) с помощью ключа хранилища ключей Azure hello и учетных данных участника службы Azure Active Directory. Hello следующий пример извлекает все сведения о ключе, hello затем шифрует hello виртуальной Машины с именем *myVM*:

```powershell
$keyVault = Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $rgName;
$diskEncryptionKeyVaultUrl = $keyVault.VaultUri;
$keyVaultResourceId = $keyVault.ResourceId;
$keyEncryptionKeyUrl = (Get-AzureKeyVaultKey -VaultName $keyVaultName -Name myKey).Key.kid;

Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $rgName `
    -VMName $vmName `
    -AadClientID $app.ApplicationId `
    -AadClientSecret $securePassword `
    -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl `
    -DiskEncryptionKeyVaultId $keyVaultResourceId `
    -KeyEncryptionKeyUrl $keyEncryptionKeyUrl `
    -KeyEncryptionKeyVaultId $keyVaultResourceId
```

Примите запрос toocontinue hello с шифрованием hello виртуальной Машины. Hello ВМ перезапускается во время процесса hello. После завершения процесса шифрования hello hello ВМ был перезагружен, проверьте состояние шифрования hello с [Get AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

Hello вывода будет примерно toohello следующий пример:

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения об управлении Azure Key Vault см. в разделе [Настройка Key Vault для виртуальных машин](key-vault-setup.md).
* Дополнительные сведения о шифровании диска, такие как подготовка зашифрованный пользовательский ВМ tooupload tooAzure, в разделе [шифрование диска Azure](../../security/azure-security-disk-encryption.md).
