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
# <a name="how-tooencrypt-virtual-disks-on-a-windows-vm"></a><span data-ttu-id="1b11c-103">Как tooencrypt виртуальных дисков на виртуальной Машине Windows</span><span class="sxs-lookup"><span data-stu-id="1b11c-103">How tooencrypt virtual disks on a Windows VM</span></span>
<span data-ttu-id="1b11c-104">Для улучшения уровня безопасности и соответствия требованиям виртуальной машины содержание виртуальных дисков в Azure можно зашифровать.</span><span class="sxs-lookup"><span data-stu-id="1b11c-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="1b11c-105">Диски можно зашифровать с использованием криптографических ключей, защищенных в хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="1b11c-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="1b11c-106">Вы будете управлять этими криптографическими ключами и проводить аудит их использования.</span><span class="sxs-lookup"><span data-stu-id="1b11c-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="1b11c-107">Это статье сведения как tooencrypt виртуальных дисков на виртуальной Машине Windows, с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1b11c-107">This article details how tooencrypt virtual disks on a Windows VM using Azure PowerShell.</span></span> <span data-ttu-id="1b11c-108">Вы также можете [шифрования ВМ Linux с помощью Azure CLI 2.0 hello](../linux/encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="1b11c-108">You can also [encrypt a Linux VM using hello Azure CLI 2.0](../linux/encrypt-disks.md).</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="1b11c-109">Общие сведения о шифровании дисков</span><span class="sxs-lookup"><span data-stu-id="1b11c-109">Overview of disk encryption</span></span>
<span data-ttu-id="1b11c-110">Виртуальные диски на виртуальных машинах Windows шифруются в неактивном состоянии с помощью Bitlocker.</span><span class="sxs-lookup"><span data-stu-id="1b11c-110">Virtual disks on Windows VMs are encrypted at rest using Bitlocker.</span></span> <span data-ttu-id="1b11c-111">В Azure за шифрование виртуальных дисков плата не взимается.</span><span class="sxs-lookup"><span data-stu-id="1b11c-111">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="1b11c-112">Ключи шифрования хранятся в хранилище ключей Azure с помощью защиты программного обеспечения, или можно импортировать или создавать ключи в аппаратных модулях безопасности (HSM) сертифицированные tooFIPS стандартов 140-2 уровня 2.</span><span class="sxs-lookup"><span data-stu-id="1b11c-112">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="1b11c-113">Эти ключи шифрования, используемые tooencrypt и расшифровки tooyour подключенных виртуальных дисков виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="1b11c-113">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="1b11c-114">Вы сохраняете контроль над этими криптографическими ключами и можете проводить аудит их использования.</span><span class="sxs-lookup"><span data-stu-id="1b11c-114">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="1b11c-115">Субъект-служба Azure Active Directory предоставляет безопасный механизм для выдачи этих криптографических ключей при включении и отключении виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="1b11c-115">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="1b11c-116">Hello процесс шифрования виртуальной Машины выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1b11c-116">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="1b11c-117">Создайте криптографический ключ в хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="1b11c-117">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="1b11c-118">Настройте hello криптографических ключей toobe может использоваться для шифрования дисков.</span><span class="sxs-lookup"><span data-stu-id="1b11c-118">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="1b11c-119">tooread hello криптографический ключ из хранилища ключей Azure, hello создания участника службы Azure Active Directory с соответствующими разрешениями hello.</span><span class="sxs-lookup"><span data-stu-id="1b11c-119">tooread hello cryptographic key from hello Azure Key Vault, create an Azure Active Directory service principal with hello appropriate permissions.</span></span>
4. <span data-ttu-id="1b11c-120">Выдавать виртуальных дисков, указание hello участника-службы Azure Active Directory и использовать соответствующие криптографических ключей toobe tooencrypt команда hello.</span><span class="sxs-lookup"><span data-stu-id="1b11c-120">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory service principal and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="1b11c-121">запросы основной службы Azure Active Directory Hello hello требуется криптографический ключ из хранилища ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="1b11c-121">hello Azure Active Directory service principal requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="1b11c-122">виртуальные диски Hello шифруются с помощью предоставленных hello криптографический ключ.</span><span class="sxs-lookup"><span data-stu-id="1b11c-122">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="1b11c-123">Процесс шифрования</span><span class="sxs-lookup"><span data-stu-id="1b11c-123">Encryption process</span></span>
<span data-ttu-id="1b11c-124">Шифрование диска основывается на hello следующие дополнительные компоненты:</span><span class="sxs-lookup"><span data-stu-id="1b11c-124">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="1b11c-125">**Хранилище ключей Azure** -использовать toosafeguard криптографических ключей и используемая для шифрования и расшифровки диска hello.</span><span class="sxs-lookup"><span data-stu-id="1b11c-125">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span> 
  * <span data-ttu-id="1b11c-126">При наличии можно воспользоваться имеющимся хранилищем ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="1b11c-126">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="1b11c-127">У вас toodedicate дисков tooencrypting хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="1b11c-127">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="1b11c-128">tooseparate административные границы и видимость ключа, можно создать выделенный хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="1b11c-128">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="1b11c-129">**Azure Active Directory** - дескрипторы hello безопасный обмен необходимых ключей шифрования и проверки подлинности для запрошенного действия.</span><span class="sxs-lookup"><span data-stu-id="1b11c-129">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span> 
  * <span data-ttu-id="1b11c-130">Как правило, для размещения приложения можно использовать имеющийся экземпляр Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b11c-130">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="1b11c-131">Субъект-служба Hello предоставляет toorequest безопасный механизм и выдаваться hello соответствующих криптографических ключей.</span><span class="sxs-lookup"><span data-stu-id="1b11c-131">hello service principal provides a secure mechanism toorequest and be issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="1b11c-132">При этом вы не разрабатываете фактическое приложение, которое интегрируется с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b11c-132">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="1b11c-133">Требования и ограничения</span><span class="sxs-lookup"><span data-stu-id="1b11c-133">Requirements and limitations</span></span>
<span data-ttu-id="1b11c-134">Поддерживаемые сценарии и требования для шифрования дисков:</span><span class="sxs-lookup"><span data-stu-id="1b11c-134">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="1b11c-135">включение шифрования для новых виртуальных машин Windows из образов Azure Marketplace или пользовательского образа виртуального жесткого диска;</span><span class="sxs-lookup"><span data-stu-id="1b11c-135">Enabling encryption on new Windows VMs from Azure Marketplace images or custom VHD image.</span></span>
* <span data-ttu-id="1b11c-136">включение шифрования для имеющихся виртуальных машин в Azure;</span><span class="sxs-lookup"><span data-stu-id="1b11c-136">Enabling encryption on existing Windows VMs in Azure.</span></span>
* <span data-ttu-id="1b11c-137">включение шифрования для виртуальных машин Windows, использующих дисковые пространства;</span><span class="sxs-lookup"><span data-stu-id="1b11c-137">Enabling encryption on Windows VMs that are configured using Storage Spaces.</span></span>
* <span data-ttu-id="1b11c-138">отключение шифрования дисков данных и дисков операционной системы виртуальных машин Windows;</span><span class="sxs-lookup"><span data-stu-id="1b11c-138">Disabling encryption on OS and data drives for Windows VMs.</span></span>
* <span data-ttu-id="1b11c-139">Все ресурсы (например, хранилище ключей, учетной записи хранилища и виртуальных Машин), должны быть в hello и подписка одного региона Azure.</span><span class="sxs-lookup"><span data-stu-id="1b11c-139">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="1b11c-140">виртуальные машины уровня "Стандартный", такие как серии A, D, DS, G и GS.</span><span class="sxs-lookup"><span data-stu-id="1b11c-140">Standard tier VMs, such as A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="1b11c-141">Шифрование диска не поддерживается в настоящее время в hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="1b11c-141">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="1b11c-142">виртуальные машины уровня "Базовый";</span><span class="sxs-lookup"><span data-stu-id="1b11c-142">Basic tier VMs.</span></span>
* <span data-ttu-id="1b11c-143">Виртуальные машины, созданные с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="1b11c-143">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="1b11c-144">Обновление криптографических ключей hello на Виртуальной машине уже зашифрованный.</span><span class="sxs-lookup"><span data-stu-id="1b11c-144">Updating hello cryptographic keys on an already encrypted VM.</span></span>
* <span data-ttu-id="1b11c-145">интеграция с локальной службой управления ключами.</span><span class="sxs-lookup"><span data-stu-id="1b11c-145">Integration with on-prem Key Management Service.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="1b11c-146">Создание Azure Key Vault и ключей</span><span class="sxs-lookup"><span data-stu-id="1b11c-146">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="1b11c-147">Прежде чем начать, убедитесь, что последняя версия hello hello установлен модуль Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1b11c-147">Before you start, make sure that hello latest version of hello Azure PowerShell module has been installed.</span></span> <span data-ttu-id="1b11c-148">Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1b11c-148">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="1b11c-149">В примерах команд hello замените все параметры в примере с именами, расположение и значения ключа.</span><span class="sxs-lookup"><span data-stu-id="1b11c-149">Throughout hello command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="1b11c-150">Hello следующих примерах используется соглашение о *myResourceGroup*, *myKeyVault*, *myVM*и т. д.</span><span class="sxs-lookup"><span data-stu-id="1b11c-150">hello following examples use a convention of *myResourceGroup*, *myKeyVault*, *myVM*, etc.</span></span>

<span data-ttu-id="1b11c-151">Hello первым шагом является toocreate toostore хранилище ключей Azure криптографические ключи.</span><span class="sxs-lookup"><span data-stu-id="1b11c-151">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="1b11c-152">Хранилище ключей Azure можно хранить ключи секретные данные, или пароли, которые позволяют вам toosecurely их реализации в приложениях и службах.</span><span class="sxs-lookup"><span data-stu-id="1b11c-152">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="1b11c-153">Для шифрования диска создайте криптографический ключ, который будет использоваться tooencrypt toostore хранилище ключей или расшифровать виртуальных дисков.</span><span class="sxs-lookup"><span data-stu-id="1b11c-153">For virtual disk encryption, you create a Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span> 

<span data-ttu-id="1b11c-154">Включение hello поставщика хранилища ключей Azure в подписке Azure с [регистра AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), затем создайте группу ресурсов с [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="1b11c-154">Enable hello Azure Key Vault provider within your Azure subscription with [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), then create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="1b11c-155">Hello следующий пример создает имя группы ресурсов *myResourceGroup* в hello *Восток США* расположение:</span><span class="sxs-lookup"><span data-stu-id="1b11c-155">hello following example creates a resource group name *myResourceGroup* in hello *East US* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

<span data-ttu-id="1b11c-156">Hello хранилище ключей Azure содержащего hello криптографических ключей и связанные вычислений, ресурсы, такие как хранилища и hello самой ВМ должны находиться в hello в одном регионе.</span><span class="sxs-lookup"><span data-stu-id="1b11c-156">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="1b11c-157">Создание хранилища ключей Azure с [New AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) и включите hello хранилища ключей для шифрования диска.</span><span class="sxs-lookup"><span data-stu-id="1b11c-157">Create an Azure Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="1b11c-158">Укажите уникальное имя Key Vault для параметра *keyVaultName*, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1b11c-158">Specify a unique Key Vault name for *keyVaultName* as follows:</span></span>

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

<span data-ttu-id="1b11c-159">Хранить криптографические ключи можно с помощью программного обеспечения или защиты HSM.</span><span class="sxs-lookup"><span data-stu-id="1b11c-159">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="1b11c-160">Для использования HSM требуется хранилище ключей уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="1b11c-160">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="1b11c-161">Нет дополнительных затрат toocreating premium, хранилище ключей, а не стандартный хранилища ключей, которое хранит программно защищенных ключей.</span><span class="sxs-lookup"><span data-stu-id="1b11c-161">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="1b11c-162">добавить toocreate premium хранилище ключей в предшествующих шаг hello hello *- Sku «Premium»* параметров.</span><span class="sxs-lookup"><span data-stu-id="1b11c-162">toocreate a premium Key Vault, in hello preceding step add hello *-Sku "Premium"* parameters.</span></span> <span data-ttu-id="1b11c-163">Hello следующий пример использует программно защищенных ключей создания стандартных хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="1b11c-163">hello following example uses software-protected keys since we created a standard Key Vault.</span></span> 

<span data-ttu-id="1b11c-164">Для обеих моделей защиты hello платформы Azure должен toobe предоставленные криптографические ключи доступа toorequest hello hello виртуальной Машины загружается toodecrypt hello виртуальных дисков.</span><span class="sxs-lookup"><span data-stu-id="1b11c-164">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="1b11c-165">Создайте криптографический ключ в своем Key Vault, выполнив команду [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span><span class="sxs-lookup"><span data-stu-id="1b11c-165">Create a cryptographic key in your Key Vault with [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span></span> <span data-ttu-id="1b11c-166">Hello следующий пример создает раздел с именем *myKey*:</span><span class="sxs-lookup"><span data-stu-id="1b11c-166">hello following example creates a key named *myKey*:</span></span>

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-hello-azure-active-directory-service-principal"></a><span data-ttu-id="1b11c-167">Создать участника-службы Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="1b11c-167">Create hello Azure Active Directory service principal</span></span>
<span data-ttu-id="1b11c-168">При виртуальные диски зашифрованные или расшифрованные, необходимо указать hello toohandle проверки подлинности учетной записи и обмена ключей шифрования из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="1b11c-168">When virtual disks are encrypted or decrypted, you specify an account toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="1b11c-169">Эта учетная запись субъекта-службы Azure Active Directory, позволяет toorequest платформы Azure hello hello соответствующие криптографических ключей от имени hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="1b11c-169">This account, an Azure Active Directory service principal, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="1b11c-170">Экземпляр Azure Active Directory по умолчанию доступен в вашей подписке, хотя во многих организациях есть выделенные каталоги Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b11c-170">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="1b11c-171">Создайте субъект-службу в Azure Active Directory, выполнив команду [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span><span class="sxs-lookup"><span data-stu-id="1b11c-171">Create a service principal in Azure Active Directory with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span></span> <span data-ttu-id="1b11c-172">toospecify безопасного пароля, выполните hello [ограничения в Azure Active Directory и политики паролей](../../active-directory/active-directory-passwords-policy.md):</span><span class="sxs-lookup"><span data-stu-id="1b11c-172">toospecify a secure password, follow hello [Password policies and restrictions in Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span></span>

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

<span data-ttu-id="1b11c-173">toosuccessfully шифрования или расшифровки виртуальные диски, разрешения на hello криптографический ключ, хранящийся в хранилище ключей должно быть основной tooread ключей hello hello Azure Active Directory набора toopermit службы.</span><span class="sxs-lookup"><span data-stu-id="1b11c-173">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory service principal tooread hello keys.</span></span> <span data-ttu-id="1b11c-174">Задайте разрешение для Key Vault, выполнив команду [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span><span class="sxs-lookup"><span data-stu-id="1b11c-174">Set permissions on your Key Vault with [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a><span data-ttu-id="1b11c-175">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="1b11c-175">Create virtual machine</span></span>
<span data-ttu-id="1b11c-176">tootest Здравствуйте, процесс шифрования, давайте создадим виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="1b11c-176">tootest hello encryption process, let's create a VM.</span></span> <span data-ttu-id="1b11c-177">Hello следующий пример создает Виртуальную машину с именем *myVM* с помощью *Windows Server 2016 Datacenter* изображения:</span><span class="sxs-lookup"><span data-stu-id="1b11c-177">hello following example creates a VM named *myVM* using a *Windows Server 2016 Datacenter* image:</span></span>

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


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="1b11c-178">Шифрование виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="1b11c-178">Encrypt virtual machine</span></span>
<span data-ttu-id="1b11c-179">tooencrypt hello виртуальные диски, можно объединить все предыдущие компоненты hello:</span><span class="sxs-lookup"><span data-stu-id="1b11c-179">tooencrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="1b11c-180">Укажите hello субъекта-службы Azure Active Directory и пароль.</span><span class="sxs-lookup"><span data-stu-id="1b11c-180">Specify hello Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="1b11c-181">Укажите метаданные hello toostore hello хранилища ключей для зашифрованных дисков.</span><span class="sxs-lookup"><span data-stu-id="1b11c-181">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="1b11c-182">Укажите toouse hello ключи шифрования для hello фактического шифрования и расшифровки.</span><span class="sxs-lookup"><span data-stu-id="1b11c-182">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="1b11c-183">Укажите, следует ли tooencrypt hello ОС диска, диски с данными hello или все.</span><span class="sxs-lookup"><span data-stu-id="1b11c-183">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="1b11c-184">Шифрование ВМ с [AzureRmVMDiskEncryptionExtension набор](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) с помощью ключа хранилища ключей Azure hello и учетных данных участника службы Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b11c-184">Encrypt your VM with [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) using hello Azure Key Vault key and Azure Active Directory service principal credentials.</span></span> <span data-ttu-id="1b11c-185">Hello следующий пример извлекает все сведения о ключе, hello затем шифрует hello виртуальной Машины с именем *myVM*:</span><span class="sxs-lookup"><span data-stu-id="1b11c-185">hello following example retrieves all hello key information then encrypts hello VM named *myVM*:</span></span>

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

<span data-ttu-id="1b11c-186">Примите запрос toocontinue hello с шифрованием hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="1b11c-186">Accept hello prompt toocontinue with hello VM encryption.</span></span> <span data-ttu-id="1b11c-187">Hello ВМ перезапускается во время процесса hello.</span><span class="sxs-lookup"><span data-stu-id="1b11c-187">hello VM restarts during hello process.</span></span> <span data-ttu-id="1b11c-188">После завершения процесса шифрования hello hello ВМ был перезагружен, проверьте состояние шифрования hello с [Get AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span><span class="sxs-lookup"><span data-stu-id="1b11c-188">Once hello encryption process completes and hello VM has rebooted, review hello encryption status with [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span></span>

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

<span data-ttu-id="1b11c-189">Hello вывода будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="1b11c-189">hello output is similar toohello following example:</span></span>

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a><span data-ttu-id="1b11c-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1b11c-190">Next steps</span></span>
* <span data-ttu-id="1b11c-191">Дополнительные сведения об управлении Azure Key Vault см. в разделе [Настройка Key Vault для виртуальных машин](key-vault-setup.md).</span><span class="sxs-lookup"><span data-stu-id="1b11c-191">For more information about managing Azure Key Vault, see [Set up Key Vault for virtual machines](key-vault-setup.md).</span></span>
* <span data-ttu-id="1b11c-192">Дополнительные сведения о шифровании диска, такие как подготовка зашифрованный пользовательский ВМ tooupload tooAzure, в разделе [шифрование диска Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="1b11c-192">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
