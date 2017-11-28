---
title: "aaaEncrypt дисков на виртуальной Машине Linux в Azure | Документы Microsoft"
description: "Как tooencrypt виртуальных дисков на виртуальной Машине Linux для усиления безопасности с помощью hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2a23b6fa-6941-4998-9804-8efe93b647b3
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: d6197742bc8562630e8395588c072093fc01d614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-linux-vm"></a><span data-ttu-id="43189-103">Как tooencrypt виртуальных дисков на виртуальной Машине Linux</span><span class="sxs-lookup"><span data-stu-id="43189-103">How tooencrypt virtual disks on a Linux VM</span></span>
<span data-ttu-id="43189-104">Для улучшения уровня безопасности и соответствия требованиям виртуальной машины содержание виртуальных дисков в Azure можно зашифровать.</span><span class="sxs-lookup"><span data-stu-id="43189-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="43189-105">Диски можно зашифровать с использованием криптографических ключей, защищенных в хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="43189-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="43189-106">Вы будете управлять этими криптографическими ключами и проводить аудит их использования.</span><span class="sxs-lookup"><span data-stu-id="43189-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="43189-107">В этой статье указаны как tooencrypt виртуальных дисков на виртуальной Машине Linux с помощью hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="43189-107">This article details how tooencrypt virtual disks on a Linux VM using hello Azure CLI 2.0.</span></span> <span data-ttu-id="43189-108">Можно также выполнить следующие действия с hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="43189-108">You can also perform these steps with hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="43189-109">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="43189-109">Quick commands</span></span>
<span data-ttu-id="43189-110">Если вам требуется tooquickly выполнения задачи hello, hello следующий раздел сведения hello базовый команд tooencrypt виртуальным дискам на виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="43189-110">If you need tooquickly accomplish hello task, hello following section details hello base commands tooencrypt virtual disks on your VM.</span></span> <span data-ttu-id="43189-111">Более подробные сведения и контекста, для каждого шага можно найти hello остальной части документа hello [начиная здесь](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="43189-111">More detailed information and context for each step can be found hello rest of hello document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="43189-112">Hello требуется последняя версия [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="43189-112">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="43189-113">В hello следующих примерах замените примеры имен параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="43189-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="43189-114">Примеры имен параметров: *myResourceGroup*, *myKey* и *myVM*.</span><span class="sxs-lookup"><span data-stu-id="43189-114">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="43189-115">Во-первых, включение hello поставщика хранилища ключей Azure в подписке Azure с [Регистрация поставщика az](/cli/azure/provider#register) и создайте группу ресурсов с [Создание группы az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="43189-115">First, enable hello Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="43189-116">Hello следующий пример создает имя группы ресурсов *myResourceGroup* в hello *eastus* расположение:</span><span class="sxs-lookup"><span data-stu-id="43189-116">hello following example creates a resource group name *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="43189-117">Создание хранилища ключей Azure с [az keyvault создать](/cli/azure/keyvault#create) и включите hello хранилища ключей для шифрования диска.</span><span class="sxs-lookup"><span data-stu-id="43189-117">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="43189-118">Укажите уникальное имя Key Vault для параметра *keyvault_name*, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="43189-118">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="43189-119">Создайте криптографический ключ в своем Key Vault, выполнив команду [az keyvault key create](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="43189-119">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="43189-120">Hello следующий пример создает раздел с именем *myKey*:</span><span class="sxs-lookup"><span data-stu-id="43189-120">hello following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

<span data-ttu-id="43189-121">Создайте субъект-службу с помощью Azure Active Directory, выполнив команду [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="43189-121">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="43189-122">дескрипторы основной службы Hello hello проверки подлинности и обмена ключей шифрования из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="43189-122">hello service principal handles hello authentication and exchange of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="43189-123">Следующий пример Hello считывает hello значениями hello участника-службы, идентификатор и пароль для использования в командах более поздней версии:</span><span class="sxs-lookup"><span data-stu-id="43189-123">hello following example reads in hello values for hello service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="43189-124">пароль Hello выводится только при создании hello участника-службы.</span><span class="sxs-lookup"><span data-stu-id="43189-124">hello password is only output when you create hello service principal.</span></span> <span data-ttu-id="43189-125">При необходимости, просмотр и запись hello пароль (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="43189-125">If desired, view and record hello password (`echo $sp_password`).</span></span> <span data-ttu-id="43189-126">Вы можете вывести список субъектов-служб, выполнив команду [az ad sp list](/cli/azure/ad/sp#list), и просмотреть дополнительные сведения о конкретном субъекте-службе, выполнив [az ad sp show](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="43189-126">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="43189-127">Задайте разрешение для Key Vault, выполнив команду [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="43189-127">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="43189-128">В следующем примере hello hello идентификатор участника службы предоставляются из hello предшествующий команды:</span><span class="sxs-lookup"><span data-stu-id="43189-128">In hello following example, hello service principal ID is supplied from hello preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

<span data-ttu-id="43189-129">Создайте виртуальною машину, выполнив команду [az vm create](/cli/azure/vm#create), и подключите диск данных емкостью 5 ГБ.</span><span class="sxs-lookup"><span data-stu-id="43189-129">Create a VM with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="43189-130">Только некоторые образы Marketplace поддерживают шифрование диска.</span><span class="sxs-lookup"><span data-stu-id="43189-130">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="43189-131">Hello следующий пример создает Виртуальную машину с именем `myVM` с помощью **CentOS 7.2n** изображения:</span><span class="sxs-lookup"><span data-stu-id="43189-131">hello following example creates a VM named `myVM` using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="43189-132">SSH tooyour виртуальной Машины с помощью hello `publicIpAddress` показано в выходные данные hello hello предшествующий команды.</span><span class="sxs-lookup"><span data-stu-id="43189-132">SSH tooyour VM using hello `publicIpAddress` shown in hello output of hello preceding command.</span></span> <span data-ttu-id="43189-133">Создать раздел и файловой системы, а затем подключить диск данных hello.</span><span class="sxs-lookup"><span data-stu-id="43189-133">Create a partition and filesystem, then mount hello data disk.</span></span> <span data-ttu-id="43189-134">Дополнительные сведения см. в разделе [подключение нового диска ВМ Linux toomount hello tooa](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="43189-134">For more information, see [Connect tooa Linux VM toomount hello new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="43189-135">Закройте сеанс SSH.</span><span class="sxs-lookup"><span data-stu-id="43189-135">Close your SSH session.</span></span>

<span data-ttu-id="43189-136">Зашифруйте виртуальную машину, выполнив команду [az vm encryption enable](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="43189-136">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="43189-137">Hello следующий пример использует hello `$sp_id` и `$sp_password` переменные из предыдущего hello `ad sp create-for-rbac` команды:</span><span class="sxs-lookup"><span data-stu-id="43189-137">hello following example uses hello `$sp_id` and `$sp_password` variables from hello preceding `ad sp create-for-rbac` command:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

<span data-ttu-id="43189-138">Потребуется некоторое время для toocomplete процесс шифрования диска hello.</span><span class="sxs-lookup"><span data-stu-id="43189-138">It takes some time for hello disk encryption process toocomplete.</span></span> <span data-ttu-id="43189-139">Мониторинг состояния hello hello процесса с [Показать шифрования ВМ az](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="43189-139">Monitor hello status of hello process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="43189-140">Здравствуйте, показано состояние **EncryptionInProgress**.</span><span class="sxs-lookup"><span data-stu-id="43189-140">hello status shows **EncryptionInProgress**.</span></span> <span data-ttu-id="43189-141">Подождать, пока состояние hello hello ОС диска отчетов **VMRestartPending**, затем перезапустите ВМ с [перезапуска ВМ az](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="43189-141">Wait until hello status for hello OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="43189-142">Hello процесс шифрования диска финализируется во время процесса загрузки hello, поэтому Подождите несколько минут перед проверкой hello состояние шифрования с **Показать шифрования ВМ az**:</span><span class="sxs-lookup"><span data-stu-id="43189-142">hello disk encryption process is finalized during hello boot process, so wait a few minutes before checking hello status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="43189-143">состояние Hello теперь следует сообщать диска hello операционной системы и диска данных как **шифрование**.</span><span class="sxs-lookup"><span data-stu-id="43189-143">hello status should now report both hello OS disk and data disk as **Encrypted**.</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="43189-144">Общие сведения о шифровании дисков</span><span class="sxs-lookup"><span data-stu-id="43189-144">Overview of disk encryption</span></span>
<span data-ttu-id="43189-145">Виртуальные диски на виртуальных машинах Linux шифруются с помощью [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="43189-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="43189-146">В Azure за шифрование виртуальных дисков плата не взимается.</span><span class="sxs-lookup"><span data-stu-id="43189-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="43189-147">Ключи шифрования хранятся в хранилище ключей Azure с помощью защиты программного обеспечения, или можно импортировать или создавать ключи в аппаратных модулях безопасности (HSM) сертифицированные tooFIPS стандартов 140-2 уровня 2.</span><span class="sxs-lookup"><span data-stu-id="43189-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="43189-148">Вы сохраняете контроль над этими криптографическими ключами и можете проводить аудит их использования.</span><span class="sxs-lookup"><span data-stu-id="43189-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="43189-149">Эти ключи шифрования, используемые tooencrypt и расшифровки tooyour подключенных виртуальных дисков виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="43189-149">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="43189-150">Субъект-служба Azure Active Directory предоставляет безопасный механизм для выдачи этих криптографических ключей при включении и отключении виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="43189-150">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="43189-151">Hello процесс шифрования виртуальной Машины выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="43189-151">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="43189-152">Создайте криптографический ключ в хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="43189-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="43189-153">Настройте hello криптографических ключей toobe может использоваться для шифрования дисков.</span><span class="sxs-lookup"><span data-stu-id="43189-153">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="43189-154">tooread hello криптографический ключ из хранилища ключей Azure, hello создания участника службы Azure Active Directory с соответствующими разрешениями hello.</span><span class="sxs-lookup"><span data-stu-id="43189-154">tooread hello cryptographic key from hello Azure Key Vault, create an Azure Active Directory service principal with hello appropriate permissions.</span></span>
4. <span data-ttu-id="43189-155">Выдавать виртуальных дисков, указание hello участника-службы Azure Active Directory и использовать соответствующие криптографических ключей toobe tooencrypt команда hello.</span><span class="sxs-lookup"><span data-stu-id="43189-155">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory service principal and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="43189-156">запросы основной службы Azure Active Directory Hello hello требуется криптографический ключ из хранилища ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="43189-156">hello Azure Active Directory service principal requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="43189-157">виртуальные диски Hello шифруются с помощью предоставленных hello криптографический ключ.</span><span class="sxs-lookup"><span data-stu-id="43189-157">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="43189-158">Процесс шифрования</span><span class="sxs-lookup"><span data-stu-id="43189-158">Encryption process</span></span>
<span data-ttu-id="43189-159">Шифрование диска основывается на hello следующие дополнительные компоненты:</span><span class="sxs-lookup"><span data-stu-id="43189-159">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="43189-160">**Хранилище ключей Azure** -использовать toosafeguard криптографических ключей и используемая для шифрования и расшифровки диска hello.</span><span class="sxs-lookup"><span data-stu-id="43189-160">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span>
  * <span data-ttu-id="43189-161">При наличии можно воспользоваться имеющимся хранилищем ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="43189-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="43189-162">У вас toodedicate дисков tooencrypting хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="43189-162">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="43189-163">tooseparate административные границы и видимость ключа, можно создать выделенный хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="43189-163">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="43189-164">**Azure Active Directory** - дескрипторы hello безопасный обмен необходимых ключей шифрования и проверки подлинности для запрошенного действия.</span><span class="sxs-lookup"><span data-stu-id="43189-164">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="43189-165">Как правило, для размещения приложения можно использовать имеющийся экземпляр Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="43189-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="43189-166">Субъект-служба Hello предоставляет toorequest безопасный механизм и выдаваться hello соответствующих криптографических ключей.</span><span class="sxs-lookup"><span data-stu-id="43189-166">hello service principal provides a secure mechanism toorequest and be issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="43189-167">При этом вы не разрабатываете фактическое приложение, которое интегрируется с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="43189-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="43189-168">Требования и ограничения</span><span class="sxs-lookup"><span data-stu-id="43189-168">Requirements and limitations</span></span>
<span data-ttu-id="43189-169">Поддерживаемые сценарии и требования для шифрования дисков:</span><span class="sxs-lookup"><span data-stu-id="43189-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="43189-170">Здравствуйте, следуя Linux server SKU - Ubuntu, CentOS, SUSE и SUSE Linux Enterprise Server (SLES) и Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="43189-170">hello following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="43189-171">Все ресурсы (например, хранилище ключей, учетной записи хранилища и виртуальных Машин), должны быть в hello и подписка одного региона Azure.</span><span class="sxs-lookup"><span data-stu-id="43189-171">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="43189-172">стандартные серии A, D, DS, G и GS виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="43189-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="43189-173">Шифрование диска не поддерживается в настоящее время в hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="43189-173">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="43189-174">виртуальные машины уровня "Базовый";</span><span class="sxs-lookup"><span data-stu-id="43189-174">Basic tier VMs.</span></span>
* <span data-ttu-id="43189-175">Виртуальные машины, созданные с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="43189-175">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="43189-176">отключение шифрования дисков ОС на виртуальных машинах Linux;</span><span class="sxs-lookup"><span data-stu-id="43189-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="43189-177">Обновление криптографических ключей hello на Виртуальной машине уже зашифрованный Linux.</span><span class="sxs-lookup"><span data-stu-id="43189-177">Updating hello cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="43189-178">Создание Azure Key Vault и ключей</span><span class="sxs-lookup"><span data-stu-id="43189-178">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="43189-179">Hello требуется последняя версия [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="43189-179">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="43189-180">В hello следующих примерах замените примеры имен параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="43189-180">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="43189-181">Примеры имен параметров: *myResourceGroup*, *myKey* и *myVM*.</span><span class="sxs-lookup"><span data-stu-id="43189-181">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="43189-182">Hello первым шагом является toocreate toostore хранилище ключей Azure криптографические ключи.</span><span class="sxs-lookup"><span data-stu-id="43189-182">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="43189-183">Хранилище ключей Azure можно хранить ключи секретные данные, или пароли, которые позволяют вам toosecurely их реализации в приложениях и службах.</span><span class="sxs-lookup"><span data-stu-id="43189-183">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="43189-184">Для шифрования диска используйте хранилище ключей toostore криптографический ключ, который будет использоваться tooencrypt или расшифровать виртуальных дисков.</span><span class="sxs-lookup"><span data-stu-id="43189-184">For virtual disk encryption, you use Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="43189-185">Включение hello поставщика хранилища ключей Azure в подписке Azure с [Регистрация поставщика az](/cli/azure/provider#register) и создайте группу ресурсов с [Создание группы az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="43189-185">Enable hello Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="43189-186">Hello следующий пример создает имя группы ресурсов *myResourceGroup* в hello `eastus` расположение:</span><span class="sxs-lookup"><span data-stu-id="43189-186">hello following example creates a resource group name *myResourceGroup* in hello `eastus` location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="43189-187">Hello хранилище ключей Azure содержащего hello криптографических ключей и связанные вычислений, ресурсы, такие как хранилища и hello самой ВМ должны находиться в hello в одном регионе.</span><span class="sxs-lookup"><span data-stu-id="43189-187">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="43189-188">Создание хранилища ключей Azure с [az keyvault создать](/cli/azure/keyvault#create) и включите hello хранилища ключей для шифрования диска.</span><span class="sxs-lookup"><span data-stu-id="43189-188">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="43189-189">Укажите уникальное имя Key Vault для параметра *keyvault_name*, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="43189-189">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="43189-190">Хранить криптографические ключи можно с помощью программного обеспечения или защиты HSM.</span><span class="sxs-lookup"><span data-stu-id="43189-190">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="43189-191">Для использования HSM требуется хранилище ключей уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="43189-191">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="43189-192">Нет дополнительных затрат toocreating premium, хранилище ключей, а не стандартный хранилища ключей, которое хранит программно защищенных ключей.</span><span class="sxs-lookup"><span data-stu-id="43189-192">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="43189-193">добавить premium хранилище ключей в предшествующих шаг hello toocreate `--sku Premium` toohello команды.</span><span class="sxs-lookup"><span data-stu-id="43189-193">toocreate a premium Key Vault, in hello preceding step add `--sku Premium` toohello command.</span></span> <span data-ttu-id="43189-194">Hello следующий пример использует программно защищенных ключей создания стандартных хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="43189-194">hello following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="43189-195">Для обеих моделей защиты hello платформы Azure должен toobe предоставленные криптографические ключи доступа toorequest hello hello виртуальной Машины загружается toodecrypt hello виртуальных дисков.</span><span class="sxs-lookup"><span data-stu-id="43189-195">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="43189-196">Создайте криптографический ключ в своем Key Vault, выполнив команду [az keyvault key create](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="43189-196">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="43189-197">Hello следующий пример создает раздел с именем *myKey*:</span><span class="sxs-lookup"><span data-stu-id="43189-197">hello following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-hello-azure-active-directory-service-principal"></a><span data-ttu-id="43189-198">Создать участника-службы Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="43189-198">Create hello Azure Active Directory service principal</span></span>
<span data-ttu-id="43189-199">При виртуальные диски зашифрованные или расшифрованные, необходимо указать hello toohandle проверки подлинности учетной записи и обмена ключей шифрования из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="43189-199">When virtual disks are encrypted or decrypted, you specify an account toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="43189-200">Эта учетная запись субъекта-службы Azure Active Directory, позволяет toorequest платформы Azure hello hello соответствующие криптографических ключей от имени hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="43189-200">This account, an Azure Active Directory service principal, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="43189-201">Экземпляр Azure Active Directory по умолчанию доступен в вашей подписке, хотя во многих организациях есть выделенные каталоги Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="43189-201">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="43189-202">Создайте субъект-службу с помощью Azure Active Directory, выполнив команду [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="43189-202">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="43189-203">Следующий пример Hello считывает hello значениями hello участника-службы, идентификатор и пароль для использования в командах более поздней версии:</span><span class="sxs-lookup"><span data-stu-id="43189-203">hello following example reads in hello values for hello service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="43189-204">пароль Hello отображается только при создании участника службы hello.</span><span class="sxs-lookup"><span data-stu-id="43189-204">hello password is only displayed when you create hello service principal.</span></span> <span data-ttu-id="43189-205">При необходимости, просмотр и запись hello пароль (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="43189-205">If desired, view and record hello password (`echo $sp_password`).</span></span> <span data-ttu-id="43189-206">Вы можете вывести список субъектов-служб, выполнив команду [az ad sp list](/cli/azure/ad/sp#list), и просмотреть дополнительные сведения о конкретном субъекте-службе, выполнив [az ad sp show](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="43189-206">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="43189-207">toosuccessfully шифрования или расшифровки виртуальные диски, разрешения на hello криптографический ключ, хранящийся в хранилище ключей должно быть основной tooread ключей hello hello Azure Active Directory набора toopermit службы.</span><span class="sxs-lookup"><span data-stu-id="43189-207">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory service principal tooread hello keys.</span></span> <span data-ttu-id="43189-208">Задайте разрешение для Key Vault, выполнив команду [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="43189-208">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="43189-209">В следующем примере hello hello идентификатор участника службы предоставляются из hello предшествующий команды:</span><span class="sxs-lookup"><span data-stu-id="43189-209">In hello following example, hello service principal ID is supplied from hello preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a><span data-ttu-id="43189-210">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="43189-210">Create virtual machine</span></span>
<span data-ttu-id="43189-211">tooactually шифрования некоторых виртуальных дисков, позволяет создать виртуальную Машину и добавьте диск данных.</span><span class="sxs-lookup"><span data-stu-id="43189-211">tooactually encrypt some virtual disks, lets create a VM and add a data disk.</span></span> <span data-ttu-id="43189-212">Создание виртуальной Машины tooencrypt с [создания виртуальной машины az](/cli/azure/vm#create) и присоединить диск данных 5 ГБ.</span><span class="sxs-lookup"><span data-stu-id="43189-212">Create a VM tooencrypt with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="43189-213">Только некоторые образы Marketplace поддерживают шифрование диска.</span><span class="sxs-lookup"><span data-stu-id="43189-213">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="43189-214">Hello следующий пример создает Виртуальную машину с именем *myVM* с помощью **CentOS 7.2n** изображения:</span><span class="sxs-lookup"><span data-stu-id="43189-214">hello following example creates a VM named *myVM* using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="43189-215">SSH tooyour виртуальной Машины с помощью hello `publicIpAddress` показано в выходные данные hello hello предшествующий команды.</span><span class="sxs-lookup"><span data-stu-id="43189-215">SSH tooyour VM using hello `publicIpAddress` shown in hello output of hello preceding command.</span></span> <span data-ttu-id="43189-216">Создать раздел и файловой системы, а затем подключить диск данных hello.</span><span class="sxs-lookup"><span data-stu-id="43189-216">Create a partition and filesystem, then mount hello data disk.</span></span> <span data-ttu-id="43189-217">Дополнительные сведения см. в разделе [подключение нового диска ВМ Linux toomount hello tooa](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="43189-217">For more information, see [Connect tooa Linux VM toomount hello new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="43189-218">Закройте сеанс SSH.</span><span class="sxs-lookup"><span data-stu-id="43189-218">Close your SSH session.</span></span>


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="43189-219">Шифрование виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="43189-219">Encrypt virtual machine</span></span>
<span data-ttu-id="43189-220">tooencrypt hello виртуальные диски, можно объединить все предыдущие компоненты hello:</span><span class="sxs-lookup"><span data-stu-id="43189-220">tooencrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="43189-221">Укажите hello субъекта-службы Azure Active Directory и пароль.</span><span class="sxs-lookup"><span data-stu-id="43189-221">Specify hello Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="43189-222">Укажите метаданные hello toostore hello хранилища ключей для зашифрованных дисков.</span><span class="sxs-lookup"><span data-stu-id="43189-222">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="43189-223">Укажите toouse hello ключи шифрования для hello фактического шифрования и расшифровки.</span><span class="sxs-lookup"><span data-stu-id="43189-223">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="43189-224">Укажите, следует ли tooencrypt hello ОС диска, диски с данными hello или все.</span><span class="sxs-lookup"><span data-stu-id="43189-224">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="43189-225">Зашифруйте виртуальную машину, выполнив команду [az vm encryption enable](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="43189-225">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="43189-226">Hello следующий пример использует hello `$sp_id` и `$sp_password` переменные из предыдущего hello `ad sp create-for-rbac` команды:</span><span class="sxs-lookup"><span data-stu-id="43189-226">hello following example uses hello `$sp_id` and `$sp_password` variables from hello preceding `ad sp create-for-rbac` command:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

<span data-ttu-id="43189-227">Потребуется некоторое время для toocomplete процесс шифрования диска hello.</span><span class="sxs-lookup"><span data-stu-id="43189-227">It takes some time for hello disk encryption process toocomplete.</span></span> <span data-ttu-id="43189-228">Мониторинг состояния hello hello процесса с [Показать шифрования ВМ az](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="43189-228">Monitor hello status of hello process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="43189-229">Hello выходные данные, аналогичные toohello следовать примере усеченные:</span><span class="sxs-lookup"><span data-stu-id="43189-229">hello output is similar toohello following truncated example:</span></span>

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

<span data-ttu-id="43189-230">Подождать, пока состояние hello hello ОС диска отчетов **VMRestartPending**, затем перезапустите ВМ с [перезапуска ВМ az](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="43189-230">Wait until hello status for hello OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="43189-231">Hello процесс шифрования диска финализируется во время процесса загрузки hello, поэтому Подождите несколько минут перед проверкой hello состояние шифрования с **Показать шифрования ВМ az**:</span><span class="sxs-lookup"><span data-stu-id="43189-231">hello disk encryption process is finalized during hello boot process, so wait a few minutes before checking hello status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="43189-232">состояние Hello теперь следует сообщать диска hello операционной системы и диска данных как **шифрование**.</span><span class="sxs-lookup"><span data-stu-id="43189-232">hello status should now report both hello OS disk and data disk as **Encrypted**.</span></span>


## <a name="add-additional-data-disks"></a><span data-ttu-id="43189-233">Добавление дополнительных дисков данных</span><span class="sxs-lookup"><span data-stu-id="43189-233">Add additional data disks</span></span>
<span data-ttu-id="43189-234">Зашифрованное диски с данными можно позднее добавить дополнительные виртуальные диски tooyour ВМ и шифровать также.</span><span class="sxs-lookup"><span data-stu-id="43189-234">Once you have encrypted your data disks, you can later add additional virtual disks tooyour VM and also encrypt them.</span></span> <span data-ttu-id="43189-235">Например позволяет добавить второй tooyour виртуальный диск виртуальной Машины следующим образом:</span><span class="sxs-lookup"><span data-stu-id="43189-235">For example, lets add a second virtual disk tooyour VM as follows:</span></span>

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

<span data-ttu-id="43189-236">Повторно запустите виртуальные диски tooencrypt команда hello hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="43189-236">Re-run hello command tooencrypt hello virtual disks as follows:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```


## <a name="next-steps"></a><span data-ttu-id="43189-237">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="43189-237">Next steps</span></span>
* <span data-ttu-id="43189-238">Дополнительные сведения об управлении хранилищем ключей Azure, а также об удалении криптографических ключей и хранилищ см. в статье [Управление хранилищем ключей с помощью интерфейса командной строки](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="43189-238">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="43189-239">Дополнительные сведения о шифровании диска, такие как подготовка зашифрованный пользовательский ВМ tooupload tooAzure, в разделе [шифрование диска Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="43189-239">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
