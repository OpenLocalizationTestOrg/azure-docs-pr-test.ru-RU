---
title: "aaaEncrypt дисков на виртуальной Машине Linux с hello Azure CLI 1.0 | Документы Microsoft"
description: "Как hello tooencrypt дисков на виртуальной Машине Linux с помощью Azure CLI 1.0 и модели развертывания диспетчера ресурсов hello"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/06/2017
ms.author: iainfou
ms.openlocfilehash: 68a0394d366c3c6941e2c6db0d4263123f951946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-hello-azure-cli-10"></a><span data-ttu-id="9eca9-103">Шифрование дисков на виртуальной Машине Linux с помощью hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="9eca9-103">Encrypt disks on a Linux VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="9eca9-104">Для улучшения уровня безопасности и соответствия требованиям виртуальной машины содержание виртуальных дисков в Azure можно зашифровать при хранении.</span><span class="sxs-lookup"><span data-stu-id="9eca9-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted at rest.</span></span> <span data-ttu-id="9eca9-105">Диски можно зашифровать с использованием криптографических ключей, защищенных в хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="9eca9-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="9eca9-106">Вы будете управлять этими криптографическими ключами и проводить аудит их использования.</span><span class="sxs-lookup"><span data-stu-id="9eca9-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="9eca9-107">В этой статье указаны как hello tooencrypt виртуальных дисков на виртуальной Машине Linux с помощью Azure CLI 1.0 и модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="9eca9-107">This article details how tooencrypt virtual disks on a Linux VM using hello Azure CLI 1.0 and hello Resource Manager deployment model.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="9eca9-108">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="9eca9-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="9eca9-109">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="9eca9-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="9eca9-110">[Azure CLI 1.0](#quick-commands) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="9eca9-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="9eca9-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="9eca9-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="9eca9-112">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="9eca9-112">Quick commands</span></span>
<span data-ttu-id="9eca9-113">Если вам требуется tooquickly выполнения задачи hello, hello следующий раздел сведения hello базовый команд tooencrypt виртуальным дискам на виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="9eca9-113">If you need tooquickly accomplish hello task, hello following section details hello base commands tooencrypt virtual disks on your VM.</span></span> <span data-ttu-id="9eca9-114">Более подробные сведения и контекста, для каждого шага можно найти hello остальной части документа hello [начиная здесь](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="9eca9-114">More detailed information and context for each step can be found hello rest of hello document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="9eca9-115">Требуется hello [последние Azure CLI 1.0](../../xplat-cli-install.md) установлен и вход с помощью режима диспетчера ресурсов hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9eca9-115">You need hello [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="9eca9-116">В hello следующих примерах замените примеры имен параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="9eca9-116">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="9eca9-117">Используемые имена параметров: `myResourceGroup`, `myKeyVault` и `myVM`.</span><span class="sxs-lookup"><span data-stu-id="9eca9-117">Example parameter names include `myResourceGroup`, `myKeyVault`, and `myVM`.</span></span>

<span data-ttu-id="9eca9-118">Во-первых включите hello поставщика хранилища ключей Azure в подписке Azure и создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9eca9-118">First, enable hello Azure Key Vault provider within your Azure subscription and create a resource group.</span></span> <span data-ttu-id="9eca9-119">Hello следующий пример создает имя группы ресурсов `myResourceGroup` в hello `WestUS` расположение:</span><span class="sxs-lookup"><span data-stu-id="9eca9-119">hello following example creates a resource group name `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="9eca9-120">Создайте хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="9eca9-120">Create an Azure Key Vault.</span></span> <span data-ttu-id="9eca9-121">Hello следующий пример создает хранилище ключей с именем `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="9eca9-121">hello following example creates a Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="9eca9-122">Создайте криптографический ключ в своем хранилище ключей и включите его для шифрования дисков.</span><span class="sxs-lookup"><span data-stu-id="9eca9-122">Create a cryptographic key in your Key Vault and enable it for disk encryption.</span></span> <span data-ttu-id="9eca9-123">Hello следующий пример создает раздел с именем `myKey`:</span><span class="sxs-lookup"><span data-stu-id="9eca9-123">hello following example creates a key named `myKey`:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

<span data-ttu-id="9eca9-124">Создайте конечную точку с помощью Azure Active Directory для управления проверкой подлинности hello и обмен ключей шифрования из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="9eca9-124">Create an endpoint using Azure Active Directory for handling hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="9eca9-125">Hello `--home-page` и `--identifier-uris` toobe фактическое маршрутизируемый адрес не обязательно.</span><span class="sxs-lookup"><span data-stu-id="9eca9-125">hello `--home-page` and `--identifier-uris` do not need toobe actual routable address.</span></span> <span data-ttu-id="9eca9-126">Для hello высокого уровня безопасности секреты клиента можно использовать вместо паролей.</span><span class="sxs-lookup"><span data-stu-id="9eca9-126">For hello highest level of security, client secrets should be used instead of passwords.</span></span> <span data-ttu-id="9eca9-127">Hello Azure CLI в настоящее время не удается создать секреты клиента.</span><span class="sxs-lookup"><span data-stu-id="9eca9-127">hello Azure CLI cannot currently generate client secrets.</span></span> <span data-ttu-id="9eca9-128">Секреты клиента может быть создана только в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9eca9-128">Client secrets can only be generated in hello Azure portal.</span></span> <span data-ttu-id="9eca9-129">Hello следующий пример создает конечную точку Azure Active Directory с именем `myAADApp` и использует пароль по `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="9eca9-129">hello following example creates an Azure Active Directory endpoint named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="9eca9-130">Укажите собственный пароль следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9eca9-130">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="9eca9-131">Примечание hello `applicationId` показано в выходных данных hello из предшествующих команда hello.</span><span class="sxs-lookup"><span data-stu-id="9eca9-131">Note hello `applicationId` shown in hello output from hello preceding command.</span></span> <span data-ttu-id="9eca9-132">Этот идентификатор приложения используется в hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="9eca9-132">This application ID is used in hello following steps:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

<span data-ttu-id="9eca9-133">Добавление существующей виртуальной Машины tooan диска данных.</span><span class="sxs-lookup"><span data-stu-id="9eca9-133">Add a data disk tooan existing VM.</span></span> <span data-ttu-id="9eca9-134">Hello следующий пример добавляет tooa диска данных виртуальной Машины с именем `myVM`:</span><span class="sxs-lookup"><span data-stu-id="9eca9-134">hello following example adds a data disk tooa VM named `myVM`:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="9eca9-135">Просмотрите сведения о hello созданный ключа хранилища ключей и hello.</span><span class="sxs-lookup"><span data-stu-id="9eca9-135">Review hello details for your Key Vault and hello key you created.</span></span> <span data-ttu-id="9eca9-136">Требуется hello идентификатор ключа хранилища, URI и ключ URL-адреса на заключительном этапе hello.</span><span class="sxs-lookup"><span data-stu-id="9eca9-136">You need hello Key Vault ID, URI, and key URL in hello final step.</span></span> <span data-ttu-id="9eca9-137">Hello следующий пример просматривает hello сведения для хранилища ключей с именем `myKeyVault` и ключ с именем `myKey`:</span><span class="sxs-lookup"><span data-stu-id="9eca9-137">hello following example reviews hello details for a Key Vault named `myKeyVault` and key named `myKey`:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="9eca9-138">Зашифруйте диски следующим образом, введя собственные имена параметров в следующих расположениях:</span><span class="sxs-lookup"><span data-stu-id="9eca9-138">Encrypt your disks as follows, entering your own parameter names throughout:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="9eca9-139">Hello Azure CLI не предоставляет подробные ошибки во время процесса шифрования hello.</span><span class="sxs-lookup"><span data-stu-id="9eca9-139">hello Azure CLI doesn't provide verbose errors during hello encryption process.</span></span> <span data-ttu-id="9eca9-140">Дополнительные сведения об устранении неполадок см. в файле `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span><span class="sxs-lookup"><span data-stu-id="9eca9-140">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span></span> <span data-ttu-id="9eca9-141">Как hello предшествующий команда имеет много переменных и не может получить много указание как toowhy hello завершилось неудачно, пример полностью команда будет выглядеть следующим:</span><span class="sxs-lookup"><span data-stu-id="9eca9-141">As hello preceding command has many variables and you may not get much indication as toowhy hello process fails, a complete command example would be as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

<span data-ttu-id="9eca9-142">Наконец, просмотрите состояние шифрования hello снова tooconfirm, что теперь были зашифрованы виртуальных дисков.</span><span class="sxs-lookup"><span data-stu-id="9eca9-142">Finally, review hello encryption status again tooconfirm that your virtual disks have now been encrypted.</span></span> <span data-ttu-id="9eca9-143">Hello следующий пример проверяет hello состояние виртуальной машины с именем `myVM` в hello `myResourceGroup` группа ресурсов:</span><span class="sxs-lookup"><span data-stu-id="9eca9-143">hello following example checks hello status of a VM named `myVM` in hello `myResourceGroup` resource group:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="9eca9-144">Общие сведения о шифровании дисков</span><span class="sxs-lookup"><span data-stu-id="9eca9-144">Overview of disk encryption</span></span>
<span data-ttu-id="9eca9-145">Виртуальные диски на виртуальных машинах Linux шифруются с помощью [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="9eca9-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="9eca9-146">В Azure за шифрование виртуальных дисков плата не взимается.</span><span class="sxs-lookup"><span data-stu-id="9eca9-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="9eca9-147">Ключи шифрования хранятся в хранилище ключей Azure с помощью защиты программного обеспечения, или можно импортировать или создавать ключи в аппаратных модулях безопасности (HSM) сертифицированные tooFIPS стандартов 140-2 уровня 2.</span><span class="sxs-lookup"><span data-stu-id="9eca9-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="9eca9-148">Вы сохраняете контроль над этими криптографическими ключами и можете проводить аудит их использования.</span><span class="sxs-lookup"><span data-stu-id="9eca9-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="9eca9-149">Эти ключи шифрования, используемые tooencrypt и расшифровки tooyour подключенных виртуальных дисков виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="9eca9-149">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="9eca9-150">Конечная точка Azure Active Directory предоставляет безопасный механизм для выдачи этих криптографических ключей при включении и отключении виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="9eca9-150">An Azure Active Directory endpoint provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="9eca9-151">Hello процесс шифрования виртуальной Машины выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9eca9-151">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="9eca9-152">Создайте криптографический ключ в хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="9eca9-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="9eca9-153">Настройте hello криптографических ключей toobe может использоваться для шифрования дисков.</span><span class="sxs-lookup"><span data-stu-id="9eca9-153">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="9eca9-154">tooread hello криптографический ключ из хранилища ключей Azure, hello создается конечная точка, с помощью Azure Active Directory с соответствующими разрешениями hello.</span><span class="sxs-lookup"><span data-stu-id="9eca9-154">tooread hello cryptographic key from hello Azure Key Vault, create an endpoint using Azure Active Directory with hello appropriate permissions.</span></span>
4. <span data-ttu-id="9eca9-155">Выдавать виртуальных дисков, указание конечной точки hello Azure Active Directory и использовать соответствующие криптографических ключей toobe tooencrypt команда hello.</span><span class="sxs-lookup"><span data-stu-id="9eca9-155">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory endpoint and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="9eca9-156">Конечная точка Azure Active Directory Hello запросы hello требуется криптографический ключ из хранилища ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="9eca9-156">hello Azure Active Directory endpoint requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="9eca9-157">виртуальные диски Hello шифруются с помощью предоставленных hello криптографический ключ.</span><span class="sxs-lookup"><span data-stu-id="9eca9-157">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="supporting-services-and-encryption-process"></a><span data-ttu-id="9eca9-158">Вспомогательные службы и процесс шифрования</span><span class="sxs-lookup"><span data-stu-id="9eca9-158">Supporting services and encryption process</span></span>
<span data-ttu-id="9eca9-159">Шифрование диска основывается на hello следующие дополнительные компоненты:</span><span class="sxs-lookup"><span data-stu-id="9eca9-159">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="9eca9-160">**Хранилище ключей Azure** -использовать toosafeguard криптографических ключей и используемая для шифрования и расшифровки диска hello.</span><span class="sxs-lookup"><span data-stu-id="9eca9-160">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span>
  * <span data-ttu-id="9eca9-161">При наличии можно воспользоваться имеющимся хранилищем ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="9eca9-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="9eca9-162">У вас toodedicate дисков tooencrypting хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="9eca9-162">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="9eca9-163">tooseparate административные границы и видимость ключа, можно создать выделенный хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="9eca9-163">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="9eca9-164">**Azure Active Directory** - дескрипторы hello безопасный обмен необходимых ключей шифрования и проверки подлинности для запрошенного действия.</span><span class="sxs-lookup"><span data-stu-id="9eca9-164">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="9eca9-165">Как правило, для размещения приложения можно использовать имеющийся экземпляр Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9eca9-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="9eca9-166">приложение Hello несколько конечную точку для hello хранилища ключей и toorequest службы виртуальной машины и получить выданный hello соответствующих криптографических ключей.</span><span class="sxs-lookup"><span data-stu-id="9eca9-166">hello application is more of an endpoint for hello Key Vault and Virtual Machine services toorequest and get issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="9eca9-167">При этом вы не разрабатываете фактическое приложение, которое интегрируется с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9eca9-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="9eca9-168">Требования и ограничения</span><span class="sxs-lookup"><span data-stu-id="9eca9-168">Requirements and limitations</span></span>
<span data-ttu-id="9eca9-169">Поддерживаемые сценарии и требования для шифрования дисков:</span><span class="sxs-lookup"><span data-stu-id="9eca9-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="9eca9-170">Здравствуйте, следуя Linux server SKU - Ubuntu, CentOS, SUSE и SUSE Linux Enterprise Server (SLES) и Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="9eca9-170">hello following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="9eca9-171">Все ресурсы (например, хранилище ключей, учетной записи хранилища и виртуальных Машин), должны быть в hello и подписка одного региона Azure.</span><span class="sxs-lookup"><span data-stu-id="9eca9-171">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="9eca9-172">стандартные серии A, D, DS, G и GS виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="9eca9-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="9eca9-173">Шифрование диска не поддерживается в настоящее время в hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="9eca9-173">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="9eca9-174">виртуальные машины уровня "Базовый";</span><span class="sxs-lookup"><span data-stu-id="9eca9-174">Basic tier VMs.</span></span>
* <span data-ttu-id="9eca9-175">Виртуальные машины, созданные с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="9eca9-175">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="9eca9-176">отключение шифрования дисков ОС на виртуальных машинах Linux;</span><span class="sxs-lookup"><span data-stu-id="9eca9-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="9eca9-177">Обновление криптографических ключей hello на Виртуальной машине уже зашифрованный Linux.</span><span class="sxs-lookup"><span data-stu-id="9eca9-177">Updating hello cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-hello-azure-key-vault-and-keys"></a><span data-ttu-id="9eca9-178">Создание hello хранилище ключей Azure и ключи</span><span class="sxs-lookup"><span data-stu-id="9eca9-178">Create hello Azure Key Vault and keys</span></span>
<span data-ttu-id="9eca9-179">toocomplete hello других разделах этого руководства, необходимо hello [последние Azure CLI 1.0](../../xplat-cli-install.md) установлен и вход с помощью режима диспетчера ресурсов hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9eca9-179">toocomplete hello remainder of this guide, you need hello [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="9eca9-180">В примерах команд hello замените все параметры в примере с именами, расположение и значения ключа.</span><span class="sxs-lookup"><span data-stu-id="9eca9-180">Throughout hello command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="9eca9-181">Hello следующих примерах используется соглашение о `myResourceGroup`, `myKeyVault`, `myAADApp`и т. д.</span><span class="sxs-lookup"><span data-stu-id="9eca9-181">hello following examples use a convention of `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.</span></span>

<span data-ttu-id="9eca9-182">Hello первым шагом является toocreate toostore хранилище ключей Azure криптографические ключи.</span><span class="sxs-lookup"><span data-stu-id="9eca9-182">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="9eca9-183">Хранилище ключей Azure можно хранить ключи секретные данные, или пароли, которые позволяют вам toosecurely их реализации в приложениях и службах.</span><span class="sxs-lookup"><span data-stu-id="9eca9-183">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="9eca9-184">Для шифрования диска используйте хранилище ключей toostore криптографический ключ, который будет использоваться tooencrypt или расшифровать виртуальных дисков.</span><span class="sxs-lookup"><span data-stu-id="9eca9-184">For virtual disk encryption, you use Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="9eca9-185">Включите hello поставщика хранилища ключей Azure в подписке Azure, а затем создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9eca9-185">Enable hello Azure Key Vault provider in your Azure subscription, then create a resource group.</span></span> <span data-ttu-id="9eca9-186">Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `WestUS` расположение:</span><span class="sxs-lookup"><span data-stu-id="9eca9-186">hello following example creates a resource group named `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="9eca9-187">Hello хранилище ключей Azure содержащего hello криптографических ключей и связанные вычислений, ресурсы, такие как хранилища и hello самой ВМ должны находиться в hello в одном регионе.</span><span class="sxs-lookup"><span data-stu-id="9eca9-187">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="9eca9-188">Hello следующий пример создает хранилище ключей Azure с именем `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="9eca9-188">hello following example creates an Azure Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="9eca9-189">Хранить криптографические ключи можно с помощью программного обеспечения или защиты HSM.</span><span class="sxs-lookup"><span data-stu-id="9eca9-189">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="9eca9-190">Для использования HSM требуется хранилище ключей уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="9eca9-190">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="9eca9-191">Нет дополнительных затрат toocreating premium, хранилище ключей, а не стандартный хранилища ключей, которое хранит программно защищенных ключей.</span><span class="sxs-lookup"><span data-stu-id="9eca9-191">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="9eca9-192">добавить premium хранилище ключей в предшествующих шаг hello toocreate `--sku Premium` toohello команды.</span><span class="sxs-lookup"><span data-stu-id="9eca9-192">toocreate a premium Key Vault, in hello preceding step add `--sku Premium` toohello command.</span></span> <span data-ttu-id="9eca9-193">Hello следующий пример использует программно защищенных ключей создания стандартных хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="9eca9-193">hello following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="9eca9-194">Для обеих моделей защиты hello платформы Azure должен toobe предоставленные криптографические ключи доступа toorequest hello hello виртуальной Машины загружается toodecrypt hello виртуальных дисков.</span><span class="sxs-lookup"><span data-stu-id="9eca9-194">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="9eca9-195">Создайте ключ шифрования в своем хранилище ключей, а затем включите его для шифрования виртуальных дисков.</span><span class="sxs-lookup"><span data-stu-id="9eca9-195">Create an encryption key within your Key Vault, then enable it for use with virtual disk encryption.</span></span> <span data-ttu-id="9eca9-196">Hello следующий пример создает раздел с именем `myKey` и затем активирует его для шифрования диска:</span><span class="sxs-lookup"><span data-stu-id="9eca9-196">hello following example creates a key named `myKey` and then enables it for disk encryption:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-hello-azure-active-directory-application"></a><span data-ttu-id="9eca9-197">Создание приложения hello Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9eca9-197">Create hello Azure Active Directory application</span></span>
<span data-ttu-id="9eca9-198">При виртуальные диски зашифрованные или расшифрованные, вы используете проверку подлинности конечной точки toohandle hello и обмена ключей шифрования из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="9eca9-198">When virtual disks are encrypted or decrypted, you use an endpoint toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="9eca9-199">Эта конечная точка приложения Azure Active Directory, позволяет toorequest платформы Azure hello hello соответствующие криптографических ключей от имени hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="9eca9-199">This endpoint, an Azure Active Directory application, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="9eca9-200">Экземпляр Azure Active Directory по умолчанию доступен в вашей подписке, хотя во многих организациях есть выделенные каталоги Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9eca9-200">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="9eca9-201">Здравствуйте, как завершенное приложение Azure Active Directory не создается, `--home-page` и `--identifier-uris` параметров в следующий пример hello не обязательно toobe фактическое маршрутизируемый адрес.</span><span class="sxs-lookup"><span data-stu-id="9eca9-201">As you are not creating a full Azure Active Directory application, hello `--home-page` and `--identifier-uris` parameters in hello following example do not need toobe actual routable address.</span></span> <span data-ttu-id="9eca9-202">Hello в примере также задает секрет, основанный на пароле, а не генерации ключей из внутри hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9eca9-202">hello following example also specifies a password-based secret rather than generating keys from within hello Azure portal.</span></span> <span data-ttu-id="9eca9-203">В настоящее время невозможно выполнить создание ключей из hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="9eca9-203">As this time, generating keys cannot be done from hello Azure CLI.</span></span>

<span data-ttu-id="9eca9-204">Создайте приложение Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9eca9-204">Create your Azure Active Directory application.</span></span> <span data-ttu-id="9eca9-205">Hello в примере создается приложение с именем `myAADApp` и использует пароль по `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="9eca9-205">hello following example creates an application named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="9eca9-206">Укажите собственный пароль следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9eca9-206">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="9eca9-207">Запишите hello `applicationId` возвращается в выходных данных hello из предшествующих команда hello.</span><span class="sxs-lookup"><span data-stu-id="9eca9-207">Make a note of hello `applicationId` that is returned in hello output from hello preceding command.</span></span> <span data-ttu-id="9eca9-208">Этот идентификатор приложения используется в некоторых hello, оставшиеся шаги.</span><span class="sxs-lookup"><span data-stu-id="9eca9-208">This application ID is used in some of hello remaining steps.</span></span> <span data-ttu-id="9eca9-209">Создайте имя участника-службы (SPN), чтобы приложение hello доступно в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="9eca9-209">Next, create a service principal name (SPN) so that hello application is accessible within your environment.</span></span> <span data-ttu-id="9eca9-210">toosuccessfully шифрования или расшифровки виртуальные диски, разрешения на hello криптографический ключ, хранящийся в хранилище ключей должно быть tooread ключей hello hello Azure Active Directory набора toopermit приложения.</span><span class="sxs-lookup"><span data-stu-id="9eca9-210">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory application tooread hello keys.</span></span>

<span data-ttu-id="9eca9-211">Создайте hello имени участника-службы и задайте соответствующие разрешения hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9eca9-211">Create hello SPN and set hello appropriate permissions as follows:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a><span data-ttu-id="9eca9-212">Добавление виртуального диска и просмотр состояния шифрования</span><span class="sxs-lookup"><span data-stu-id="9eca9-212">Add a virtual disk and review encryption status</span></span>
<span data-ttu-id="9eca9-213">tooactually шифрования некоторых виртуальных дисков, позволяет добавить tooan диск существующей виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="9eca9-213">tooactually encrypt some virtual disks, lets add a disk tooan existing VM.</span></span> <span data-ttu-id="9eca9-214">Добавьте tooan диск 5 ГБ данных, существующей виртуальной Машины следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9eca9-214">Add a 5Gb data disk tooan existing VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="9eca9-215">виртуальные диски Hello в настоящее время не шифруются.</span><span class="sxs-lookup"><span data-stu-id="9eca9-215">hello virtual disks are not currently encrypted.</span></span> <span data-ttu-id="9eca9-216">Просмотрите текущее состояние шифрования hello вашей виртуальной машины следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9eca9-216">Review hello current encryption status of your VM as follows:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a><span data-ttu-id="9eca9-217">Шифрование виртуальных дисков</span><span class="sxs-lookup"><span data-stu-id="9eca9-217">Encrypt virtual disks</span></span>
<span data-ttu-id="9eca9-218">toonow шифрования hello виртуальные диски, объедините все предыдущие компоненты hello:</span><span class="sxs-lookup"><span data-stu-id="9eca9-218">toonow encrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="9eca9-219">Укажите приложение hello Azure Active Directory и пароль.</span><span class="sxs-lookup"><span data-stu-id="9eca9-219">Specify hello Azure Active Directory application and password.</span></span>
2. <span data-ttu-id="9eca9-220">Укажите метаданные hello toostore hello хранилища ключей для зашифрованных дисков.</span><span class="sxs-lookup"><span data-stu-id="9eca9-220">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="9eca9-221">Укажите toouse hello ключи шифрования для hello фактического шифрования и расшифровки.</span><span class="sxs-lookup"><span data-stu-id="9eca9-221">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="9eca9-222">Укажите, следует ли tooencrypt hello ОС диска, диски с данными hello или все.</span><span class="sxs-lookup"><span data-stu-id="9eca9-222">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="9eca9-223">Позволяет просмотреть сведения о hello ключа хранилища ключей Azure и hello, созданный, hello идентификатор ключа хранилища, URI, а затем ключа URL-адрес на заключительном этапе hello:</span><span class="sxs-lookup"><span data-stu-id="9eca9-223">Lets review hello details for your Azure Key Vault and hello key you created, as you need hello Key Vault ID, URI, and then key URL in hello final step:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="9eca9-224">Шифрование виртуальных дисков с выходными данными hello hello `azure keyvault show` и `azure keyvault key show` команд следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9eca9-224">Encrypt your virtual disks using hello output from hello `azure keyvault show` and `azure keyvault key show` commands as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="9eca9-225">Как hello предыдущая команда имеет много переменных, hello следующий пример является полностью команда hello для ссылки:</span><span class="sxs-lookup"><span data-stu-id="9eca9-225">As hello preceding command has many variables, hello following example is hello complete command for reference:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

<span data-ttu-id="9eca9-226">Hello Azure CLI не предоставляет подробные ошибки во время процесса шифрования hello.</span><span class="sxs-lookup"><span data-stu-id="9eca9-226">hello Azure CLI doesn't provide verbose errors during hello encryption process.</span></span> <span data-ttu-id="9eca9-227">Дополнительные сведения об устранении неполадок, просмотрите `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` на hello виртуальной Машины, шифруются.</span><span class="sxs-lookup"><span data-stu-id="9eca9-227">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` on hello VM you are encrypting.</span></span>

<span data-ttu-id="9eca9-228">Наконец, позволяет просмотреть состояние шифрования hello снова tooconfirm, что теперь были зашифрованы виртуальных дисков:</span><span class="sxs-lookup"><span data-stu-id="9eca9-228">Finally, lets review hello encryption status again tooconfirm that your virtual disks have now been encrypted:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a><span data-ttu-id="9eca9-229">Добавление дополнительных дисков данных</span><span class="sxs-lookup"><span data-stu-id="9eca9-229">Add additional data disks</span></span>
<span data-ttu-id="9eca9-230">Зашифрованное диски с данными можно позднее добавить дополнительные виртуальные диски tooyour ВМ и шифровать также.</span><span class="sxs-lookup"><span data-stu-id="9eca9-230">Once you have encrypted your data disks, you can later add additional virtual disks tooyour VM and also encrypt them.</span></span> <span data-ttu-id="9eca9-231">При запуске hello `azure vm enable-disk-encryption` command, версия последовательности hello приращение, с помощью hello `--sequence-version` параметра.</span><span class="sxs-lookup"><span data-stu-id="9eca9-231">When you run hello `azure vm enable-disk-encryption` command, increment hello sequence version using hello `--sequence-version` parameter.</span></span> <span data-ttu-id="9eca9-232">Этот параметр версии последовательности позволяет tooperform последовательные операции с hello одной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="9eca9-232">This sequence version parameter allows you tooperform repeated operations on hello same VM.</span></span>

<span data-ttu-id="9eca9-233">Например позволяет добавить второй tooyour виртуальный диск виртуальной Машины следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9eca9-233">For example, lets add a second virtual disk tooyour VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="9eca9-234">Повторно запустите hello команда tooencrypt hello виртуальные диски, это время добавления hello `--sequence-version` параметр и hello значение приращения от наших первого запуска следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9eca9-234">Rerun hello command tooencrypt hello virtual disks, this time adding hello `--sequence-version` parameter, and incrementing hello value from our first run as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
  --sequence-version 2
```


## <a name="next-steps"></a><span data-ttu-id="9eca9-235">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9eca9-235">Next steps</span></span>
* <span data-ttu-id="9eca9-236">Дополнительные сведения об управлении хранилищем ключей Azure, а также об удалении криптографических ключей и хранилищ см. в статье [Управление хранилищем ключей с помощью интерфейса командной строки](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="9eca9-236">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="9eca9-237">Дополнительные сведения о шифровании диска, такие как подготовка зашифрованный пользовательский ВМ tooupload tooAzure, в разделе [шифрование диска Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="9eca9-237">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
