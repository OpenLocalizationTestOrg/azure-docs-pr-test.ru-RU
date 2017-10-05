---
title: "Шифрование дисков виртуальной машины Linux с помощью Azure CLI 1.0 | Документация Майкрософт"
description: "Сведения о шифровании дисков в виртуальной машине Linux с использованием Azure CLI 1.0 и модели развертывания Resource Manager."
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
ms.openlocfilehash: b436f2d43c41000f4385889edb3fa3983d4a8c66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="c0abe-103">Шифрование дисков на виртуальной машине Linux с помощью Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c0abe-103">Encrypt disks on a Linux VM using the Azure CLI 1.0</span></span>
<span data-ttu-id="c0abe-104">Для улучшения уровня безопасности и соответствия требованиям виртуальной машины содержание виртуальных дисков в Azure можно зашифровать при хранении.</span><span class="sxs-lookup"><span data-stu-id="c0abe-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted at rest.</span></span> <span data-ttu-id="c0abe-105">Диски можно зашифровать с использованием криптографических ключей, защищенных в хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="c0abe-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="c0abe-106">Вы будете управлять этими криптографическими ключами и проводить аудит их использования.</span><span class="sxs-lookup"><span data-stu-id="c0abe-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="c0abe-107">В этой статье подробно описывается шифрование дисков на виртуальной машине Linux с использованием Azure CLI 1.0 и модели развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c0abe-107">This article details how to encrypt virtual disks on a Linux VM using the Azure CLI 1.0 and the Resource Manager deployment model.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="c0abe-108">Версии интерфейса командной строки для выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="c0abe-108">CLI versions to complete the task</span></span>
<span data-ttu-id="c0abe-109">Вы можете выполнить задачу, используя одну из следующих версий интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="c0abe-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="c0abe-110">[Azure CLI 1.0](#quick-commands) — интерфейс командной строки для классической модели развертывания и модели развертывания Resource Manager (в этой статье).</span><span class="sxs-lookup"><span data-stu-id="c0abe-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="c0abe-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) — интерфейс командной строки следующего поколения для модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c0abe-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="c0abe-112">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="c0abe-112">Quick commands</span></span>
<span data-ttu-id="c0abe-113">Если вам необходимо быстро выполнить задачу, в следующем разделе описаны основные команды для шифрования виртуальных дисков на вашей виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c0abe-113">If you need to quickly accomplish the task, the following section details the base commands to encrypt virtual disks on your VM.</span></span> <span data-ttu-id="c0abe-114">Более подробные сведения и контекст для каждого этапа можно найти в остальной части документа [начиная отсюда](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="c0abe-114">More detailed information and context for each step can be found the rest of the document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="c0abe-115">Кроме того, потребуется установить [последнюю версию Azure CLI 1.0](../../xplat-cli-install.md) и выполнить вход в систему в режиме Resource Manager, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="c0abe-115">You need the [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="c0abe-116">В следующих примерах замените имена параметров собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="c0abe-116">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="c0abe-117">Используемые имена параметров: `myResourceGroup`, `myKeyVault` и `myVM`.</span><span class="sxs-lookup"><span data-stu-id="c0abe-117">Example parameter names include `myResourceGroup`, `myKeyVault`, and `myVM`.</span></span>

<span data-ttu-id="c0abe-118">Сначала включите поставщик хранилища ключей Azure в подписке Azure и создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c0abe-118">First, enable the Azure Key Vault provider within your Azure subscription and create a resource group.</span></span> <span data-ttu-id="c0abe-119">В следующем примере создается имя группы ресурсов `myResourceGroup` в расположении `WestUS`.</span><span class="sxs-lookup"><span data-stu-id="c0abe-119">The following example creates a resource group name `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="c0abe-120">Создайте хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="c0abe-120">Create an Azure Key Vault.</span></span> <span data-ttu-id="c0abe-121">В следующем примере создается хранилище ключей с именем `myKeyVault`.</span><span class="sxs-lookup"><span data-stu-id="c0abe-121">The following example creates a Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="c0abe-122">Создайте криптографический ключ в своем хранилище ключей и включите его для шифрования дисков.</span><span class="sxs-lookup"><span data-stu-id="c0abe-122">Create a cryptographic key in your Key Vault and enable it for disk encryption.</span></span> <span data-ttu-id="c0abe-123">В следующем примере создается ключ с именем `myKey`.</span><span class="sxs-lookup"><span data-stu-id="c0abe-123">The following example creates a key named `myKey`:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

<span data-ttu-id="c0abe-124">Создайте конечную точку с помощью Azure Active Directory для выполнения проверки подлинности и обмена криптографическими ключами из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="c0abe-124">Create an endpoint using Azure Active Directory for handling the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="c0abe-125">`--home-page` и `--identifier-uris` не обязательно должны быть фактическими маршрутизируемыми адресами.</span><span class="sxs-lookup"><span data-stu-id="c0abe-125">The `--home-page` and `--identifier-uris` do not need to be actual routable address.</span></span> <span data-ttu-id="c0abe-126">Для обеспечения высшего уровня безопасности вместо паролей следует использовать секреты клиента.</span><span class="sxs-lookup"><span data-stu-id="c0abe-126">For the highest level of security, client secrets should be used instead of passwords.</span></span> <span data-ttu-id="c0abe-127">Сейчас интерфейс командной строки Azure не создает секреты клиента.</span><span class="sxs-lookup"><span data-stu-id="c0abe-127">The Azure CLI cannot currently generate client secrets.</span></span> <span data-ttu-id="c0abe-128">Секреты клиента могут создаваться только на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c0abe-128">Client secrets can only be generated in the Azure portal.</span></span> <span data-ttu-id="c0abe-129">В следующем примере создается конечная точка Azure Active Directory с именем `myAADApp` и используется пароль `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="c0abe-129">The following example creates an Azure Active Directory endpoint named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="c0abe-130">Укажите собственный пароль следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c0abe-130">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="c0abe-131">Запишите `applicationId`, который содержится в выходных данных предыдущей команды.</span><span class="sxs-lookup"><span data-stu-id="c0abe-131">Note the `applicationId` shown in the output from the preceding command.</span></span> <span data-ttu-id="c0abe-132">Этот идентификатор приложения используется при выполнении следующих действий:</span><span class="sxs-lookup"><span data-stu-id="c0abe-132">This application ID is used in the following steps:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

<span data-ttu-id="c0abe-133">Добавьте диск данных в имеющуюся виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="c0abe-133">Add a data disk to an existing VM.</span></span> <span data-ttu-id="c0abe-134">В следующем примере показано, как добавить диск данных в виртуальную машину с именем `myVM`.</span><span class="sxs-lookup"><span data-stu-id="c0abe-134">The following example adds a data disk to a VM named `myVM`:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="c0abe-135">Просмотрите сведения о своем хранилище ключей и созданном ключе.</span><span class="sxs-lookup"><span data-stu-id="c0abe-135">Review the details for your Key Vault and the key you created.</span></span> <span data-ttu-id="c0abe-136">На последнем шаге вам понадобится идентификатор хранилища ключей, универсальный код ресурса (URI) и URL-адрес ключа.</span><span class="sxs-lookup"><span data-stu-id="c0abe-136">You need the Key Vault ID, URI, and key URL in the final step.</span></span> <span data-ttu-id="c0abe-137">В следующем примере просматриваются данные о хранилище ключей с именем `myKeyVault` и ключе с именем `myKey`:</span><span class="sxs-lookup"><span data-stu-id="c0abe-137">The following example reviews the details for a Key Vault named `myKeyVault` and key named `myKey`:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="c0abe-138">Зашифруйте диски следующим образом, введя собственные имена параметров в следующих расположениях:</span><span class="sxs-lookup"><span data-stu-id="c0abe-138">Encrypt your disks as follows, entering your own parameter names throughout:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="c0abe-139">Интерфейс командной строки Azure не предоставляет подробные сообщения об ошибках в процессе шифрования.</span><span class="sxs-lookup"><span data-stu-id="c0abe-139">The Azure CLI doesn't provide verbose errors during the encryption process.</span></span> <span data-ttu-id="c0abe-140">Дополнительные сведения об устранении неполадок см. в файле `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span><span class="sxs-lookup"><span data-stu-id="c0abe-140">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span></span> <span data-ttu-id="c0abe-141">Так как в приведенной выше команде много переменных и могут отсутствовать сведения о том, почему процесс завершается ошибкой, пример всей команды будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c0abe-141">As the preceding command has many variables and you may not get much indication as to why the process fails, a complete command example would be as follows:</span></span>

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

<span data-ttu-id="c0abe-142">Наконец, просмотрите состояние шифрования, чтобы убедиться, что виртуальные диски зашифрованы.</span><span class="sxs-lookup"><span data-stu-id="c0abe-142">Finally, review the encryption status again to confirm that your virtual disks have now been encrypted.</span></span> <span data-ttu-id="c0abe-143">В следующем примере проверяется состояние виртуальной машины с именем `myVM` в группе ресурсов `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="c0abe-143">The following example checks the status of a VM named `myVM` in the `myResourceGroup` resource group:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="c0abe-144">Общие сведения о шифровании дисков</span><span class="sxs-lookup"><span data-stu-id="c0abe-144">Overview of disk encryption</span></span>
<span data-ttu-id="c0abe-145">Виртуальные диски на виртуальных машинах Linux шифруются с помощью [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="c0abe-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="c0abe-146">В Azure за шифрование виртуальных дисков плата не взимается.</span><span class="sxs-lookup"><span data-stu-id="c0abe-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="c0abe-147">Криптографические ключи хранятся в хранилище ключей Azure с применением защиты программного обеспечения. В качестве альтернативы можно импортировать или создать ключи аппаратных модулей безопасности (HSM), сертифицированных по стандартам уровня 2 FIPS 140-2.</span><span class="sxs-lookup"><span data-stu-id="c0abe-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="c0abe-148">Вы сохраняете контроль над этими криптографическими ключами и можете проводить аудит их использования.</span><span class="sxs-lookup"><span data-stu-id="c0abe-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="c0abe-149">Эти криптографические ключи используются для шифрования и расшифровки виртуальных дисков, подключенных к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c0abe-149">These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM.</span></span> <span data-ttu-id="c0abe-150">Конечная точка Azure Active Directory предоставляет безопасный механизм для выдачи этих криптографических ключей при включении и отключении виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="c0abe-150">An Azure Active Directory endpoint provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="c0abe-151">Процесс шифрования виртуальной машины выполняется следующим образом.</span><span class="sxs-lookup"><span data-stu-id="c0abe-151">The process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="c0abe-152">Создайте криптографический ключ в хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="c0abe-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="c0abe-153">Настройте криптографический ключ таким образом, чтобы его можно было использовать для шифрования дисков.</span><span class="sxs-lookup"><span data-stu-id="c0abe-153">Configure the cryptographic key to be usable for encrypting disks.</span></span>
3. <span data-ttu-id="c0abe-154">Чтобы прочитать криптографический ключ из хранилища ключей Azure, создайте конечную точку, используя Azure Active Directory с соответствующими разрешениями.</span><span class="sxs-lookup"><span data-stu-id="c0abe-154">To read the cryptographic key from the Azure Key Vault, create an endpoint using Azure Active Directory with the appropriate permissions.</span></span>
4. <span data-ttu-id="c0abe-155">Выполните команду для шифрования виртуальных дисков, указав конечную точку Azure Active Directory и соответствующий ключ шифрования, который необходимо использовать.</span><span class="sxs-lookup"><span data-stu-id="c0abe-155">Issue the command to encrypt your virtual disks, specifying the Azure Active Directory endpoint and appropriate cryptographic key to be used.</span></span>
5. <span data-ttu-id="c0abe-156">Конечная точка Azure Active Directory запрашивает требуемый криптографический ключ из хранилища ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="c0abe-156">The Azure Active Directory endpoint requests the required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="c0abe-157">Виртуальные диски зашифровываются с использованием предоставленного криптографического ключа.</span><span class="sxs-lookup"><span data-stu-id="c0abe-157">The virtual disks are encrypted using the provided cryptographic key.</span></span>

## <a name="supporting-services-and-encryption-process"></a><span data-ttu-id="c0abe-158">Вспомогательные службы и процесс шифрования</span><span class="sxs-lookup"><span data-stu-id="c0abe-158">Supporting services and encryption process</span></span>
<span data-ttu-id="c0abe-159">Шифрование дисков зависит от следующих дополнительных компонентов.</span><span class="sxs-lookup"><span data-stu-id="c0abe-159">Disk encryption relies on the following additional components:</span></span>

* <span data-ttu-id="c0abe-160">**Хранилище ключей Azure.** Используется для защиты криптографических ключей и секретов, используемых для шифрования или расшифровки дисков.</span><span class="sxs-lookup"><span data-stu-id="c0abe-160">**Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process.</span></span>
  * <span data-ttu-id="c0abe-161">При наличии можно воспользоваться имеющимся хранилищем ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="c0abe-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="c0abe-162">Для шифрования дисков не нужно выделять хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="c0abe-162">You do not have to dedicate a Key Vault to encrypting disks.</span></span>
  * <span data-ttu-id="c0abe-163">Чтобы разделить административные границы и обеспечить видимость ключа, можно создать выделенное хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="c0abe-163">To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="c0abe-164">**Azure Active Directory.** Осуществляет безопасный обмен необходимыми криптографическими ключами и проверку подлинности для запрошенных действий.</span><span class="sxs-lookup"><span data-stu-id="c0abe-164">**Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="c0abe-165">Как правило, для размещения приложения можно использовать имеющийся экземпляр Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c0abe-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="c0abe-166">Службы хранилища ключей и виртуальных машин запрашивают и получают соответствующие криптографические ключи с помощью приложения, выступающего в качестве конечной точки.</span><span class="sxs-lookup"><span data-stu-id="c0abe-166">The application is more of an endpoint for the Key Vault and Virtual Machine services to request and get issued the appropriate cryptographic keys.</span></span> <span data-ttu-id="c0abe-167">При этом вы не разрабатываете фактическое приложение, которое интегрируется с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c0abe-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="c0abe-168">Требования и ограничения</span><span class="sxs-lookup"><span data-stu-id="c0abe-168">Requirements and limitations</span></span>
<span data-ttu-id="c0abe-169">Поддерживаемые сценарии и требования для шифрования дисков:</span><span class="sxs-lookup"><span data-stu-id="c0abe-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="c0abe-170">SKU серверов Linux — Ubuntu, CentOS, SUSE, SUSE Linux Enterprise Server (SLES) и Red Hat Enterprise Linux;</span><span class="sxs-lookup"><span data-stu-id="c0abe-170">The following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="c0abe-171">все ресурсы (такие как хранилище ключей, учетная запись хранения и виртуальная машина) должны относиться к одному региону и одной подписке Azure;</span><span class="sxs-lookup"><span data-stu-id="c0abe-171">All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.</span></span>
* <span data-ttu-id="c0abe-172">стандартные серии A, D, DS, G и GS виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="c0abe-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="c0abe-173">Шифрование дисков сейчас не поддерживается в следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="c0abe-173">Disk encryption is not currently supported in the following scenarios:</span></span>

* <span data-ttu-id="c0abe-174">виртуальные машины уровня "Базовый";</span><span class="sxs-lookup"><span data-stu-id="c0abe-174">Basic tier VMs.</span></span>
* <span data-ttu-id="c0abe-175">виртуальные машины, созданные с использованием классической модели развертывания;</span><span class="sxs-lookup"><span data-stu-id="c0abe-175">VMs created using the Classic deployment model.</span></span>
* <span data-ttu-id="c0abe-176">отключение шифрования дисков ОС на виртуальных машинах Linux;</span><span class="sxs-lookup"><span data-stu-id="c0abe-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="c0abe-177">обновление криптографических ключей на уже зашифрованных виртуальных машинах Linux.</span><span class="sxs-lookup"><span data-stu-id="c0abe-177">Updating the cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-the-azure-key-vault-and-keys"></a><span data-ttu-id="c0abe-178">Создание хранилища ключей Azure и ключей</span><span class="sxs-lookup"><span data-stu-id="c0abe-178">Create the Azure Key Vault and keys</span></span>
<span data-ttu-id="c0abe-179">Для выполнения указаний из оставшейся части этого руководства потребуется установить [последнюю версию Azure CLI 1.0](../../xplat-cli-install.md) и выполнить вход в систему в режиме Resource Manager, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="c0abe-179">To complete the remainder of this guide, you need the [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="c0abe-180">В примерах команд замените все примеры параметров собственными именами, расположением и значениями ключей.</span><span class="sxs-lookup"><span data-stu-id="c0abe-180">Throughout the command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="c0abe-181">В следующих примерах используется соглашение `myResourceGroup`, `myKeyVault`, `myAADApp` и т. д.</span><span class="sxs-lookup"><span data-stu-id="c0abe-181">The following examples use a convention of `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.</span></span>

<span data-ttu-id="c0abe-182">Первым делом создайте хранилище ключей Azure для хранения криптографических ключей.</span><span class="sxs-lookup"><span data-stu-id="c0abe-182">The first step is to create an Azure Key Vault to store your cryptographic keys.</span></span> <span data-ttu-id="c0abe-183">В хранилище ключей Azure можно хранить ключи, секреты или пароли, что позволяет безопасно реализовать их в приложениях и службах.</span><span class="sxs-lookup"><span data-stu-id="c0abe-183">Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services.</span></span> <span data-ttu-id="c0abe-184">Для шифрования виртуальных дисков используйте хранилище ключей, чтобы хранить криптографический ключ, используемый для шифрования или расшифровки виртуальных дисков.</span><span class="sxs-lookup"><span data-stu-id="c0abe-184">For virtual disk encryption, you use Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="c0abe-185">Включите поставщик хранилища ключей Azure в подписке Azure и создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c0abe-185">Enable the Azure Key Vault provider in your Azure subscription, then create a resource group.</span></span> <span data-ttu-id="c0abe-186">В следующем примере создается группа ресурсов с именем `myResourceGroup` в расположении `WestUS`:</span><span class="sxs-lookup"><span data-stu-id="c0abe-186">The following example creates a resource group named `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="c0abe-187">Хранилище ключей Azure, содержащее криптографические ключи и связанные вычислительные ресурсы, такие как хранилище и виртуальная машина, должны находиться в одном и том же регионе.</span><span class="sxs-lookup"><span data-stu-id="c0abe-187">The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region.</span></span> <span data-ttu-id="c0abe-188">В следующем примере создается хранилище ключей Azure с именем `myKeyVault`.</span><span class="sxs-lookup"><span data-stu-id="c0abe-188">The following example creates an Azure Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="c0abe-189">Хранить криптографические ключи можно с помощью программного обеспечения или защиты HSM.</span><span class="sxs-lookup"><span data-stu-id="c0abe-189">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="c0abe-190">Для использования HSM требуется хранилище ключей уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="c0abe-190">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="c0abe-191">Создание хранилища ключей уровня "Премиум" осуществляется за дополнительную плату в отличие от хранилища ключей уровня "Стандартный", в котором хранятся ключи, защищенные программным обеспечением.</span><span class="sxs-lookup"><span data-stu-id="c0abe-191">There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="c0abe-192">Чтобы создать хранилище ключей уровня "Премиум", на предыдущем шаге добавьте `--sku Premium` к команде.</span><span class="sxs-lookup"><span data-stu-id="c0abe-192">To create a premium Key Vault, in the preceding step add `--sku Premium` to the command.</span></span> <span data-ttu-id="c0abe-193">В следующем примере используются ключи, защищенные программным обеспечением, так как мы создали хранилище ключей уровня "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="c0abe-193">The following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="c0abe-194">Для обеих моделей защиты платформе Azure необходимо предоставить доступ на запрос криптографических ключей при загрузке виртуальной машины для расшифровки виртуальных дисков.</span><span class="sxs-lookup"><span data-stu-id="c0abe-194">For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks.</span></span> <span data-ttu-id="c0abe-195">Создайте ключ шифрования в своем хранилище ключей, а затем включите его для шифрования виртуальных дисков.</span><span class="sxs-lookup"><span data-stu-id="c0abe-195">Create an encryption key within your Key Vault, then enable it for use with virtual disk encryption.</span></span> <span data-ttu-id="c0abe-196">В следующем примере создается ключ с именем `myKey`, а затем он включается для шифрования дисков.</span><span class="sxs-lookup"><span data-stu-id="c0abe-196">The following example creates a key named `myKey` and then enables it for disk encryption:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-the-azure-active-directory-application"></a><span data-ttu-id="c0abe-197">Создание приложения Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0abe-197">Create the Azure Active Directory application</span></span>
<span data-ttu-id="c0abe-198">При шифровании или расшифровке виртуальных дисков проверка подлинности и обмен криптографическими ключами из хранилища ключей осуществляется с помощью конечной точки.</span><span class="sxs-lookup"><span data-stu-id="c0abe-198">When virtual disks are encrypted or decrypted, you use an endpoint to handle the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="c0abe-199">Эта конечная точка, приложение Azure Active Directory, позволяет платформе Azure запрашивать соответствующие криптографические ключи от имени виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c0abe-199">This endpoint, an Azure Active Directory application, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM.</span></span> <span data-ttu-id="c0abe-200">Экземпляр Azure Active Directory по умолчанию доступен в вашей подписке, хотя во многих организациях есть выделенные каталоги Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c0abe-200">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="c0abe-201">Так как вы не создаете полноценное приложение Azure Active Directory, параметры `--home-page` и `--identifier-uris` в следующем примере не обязательно должны быть фактическими маршрутизируемыми адресами.</span><span class="sxs-lookup"><span data-stu-id="c0abe-201">As you are not creating a full Azure Active Directory application, the `--home-page` and `--identifier-uris` parameters in the following example do not need to be actual routable address.</span></span> <span data-ttu-id="c0abe-202">Кроме того, в следующем примере также вместо создания ключей на портале Azure указывается секрет на основе пароля.</span><span class="sxs-lookup"><span data-stu-id="c0abe-202">The following example also specifies a password-based secret rather than generating keys from within the Azure portal.</span></span> <span data-ttu-id="c0abe-203">Сейчас создавать ключи из командной строки Azure невозможно.</span><span class="sxs-lookup"><span data-stu-id="c0abe-203">As this time, generating keys cannot be done from the Azure CLI.</span></span>

<span data-ttu-id="c0abe-204">Создайте приложение Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c0abe-204">Create your Azure Active Directory application.</span></span> <span data-ttu-id="c0abe-205">В следующем примере создается приложение с именем `myAADApp` и используется пароль `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="c0abe-205">The following example creates an application named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="c0abe-206">Укажите собственный пароль следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c0abe-206">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="c0abe-207">Запишите `applicationId`, который возвращается в выходных данных из предыдущей команды.</span><span class="sxs-lookup"><span data-stu-id="c0abe-207">Make a note of the `applicationId` that is returned in the output from the preceding command.</span></span> <span data-ttu-id="c0abe-208">Этот идентификатор приложения используется в некоторых из оставшихся шагов.</span><span class="sxs-lookup"><span data-stu-id="c0abe-208">This application ID is used in some of the remaining steps.</span></span> <span data-ttu-id="c0abe-209">Далее создайте имя субъекта-службы, чтобы приложение было доступным в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="c0abe-209">Next, create a service principal name (SPN) so that the application is accessible within your environment.</span></span> <span data-ttu-id="c0abe-210">Для успешного шифрования или расшифровки виртуальных дисков необходимо настроить разрешения на криптографические ключи, которые хранятся в хранилище ключей, так, чтобы приложение Azure Active Directory могло читать их.</span><span class="sxs-lookup"><span data-stu-id="c0abe-210">To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory application to read the keys.</span></span>

<span data-ttu-id="c0abe-211">Создайте имя субъекта-службы и настройте соответствующие разрешения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c0abe-211">Create the SPN and set the appropriate permissions as follows:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a><span data-ttu-id="c0abe-212">Добавление виртуального диска и просмотр состояния шифрования</span><span class="sxs-lookup"><span data-stu-id="c0abe-212">Add a virtual disk and review encryption status</span></span>
<span data-ttu-id="c0abe-213">Чтобы зашифровать некоторые виртуальные диски, добавьте диск в имеющуюся виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="c0abe-213">To actually encrypt some virtual disks, lets add a disk to an existing VM.</span></span> <span data-ttu-id="c0abe-214">Добавьте диск данных емкостью 5 ГБ в имеющуюся виртуальную машину следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c0abe-214">Add a 5Gb data disk to an existing VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="c0abe-215">Виртуальные диски сейчас не зашифрованы.</span><span class="sxs-lookup"><span data-stu-id="c0abe-215">The virtual disks are not currently encrypted.</span></span> <span data-ttu-id="c0abe-216">Просмотрите текущее состояние шифрования виртуальной машины следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c0abe-216">Review the current encryption status of your VM as follows:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a><span data-ttu-id="c0abe-217">Шифрование виртуальных дисков</span><span class="sxs-lookup"><span data-stu-id="c0abe-217">Encrypt virtual disks</span></span>
<span data-ttu-id="c0abe-218">Чтобы шифровать виртуальные диски, объедините предыдущие компоненты.</span><span class="sxs-lookup"><span data-stu-id="c0abe-218">To now encrypt the virtual disks, you bring together all the previous components:</span></span>

1. <span data-ttu-id="c0abe-219">Укажите приложение и пароль Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c0abe-219">Specify the Azure Active Directory application and password.</span></span>
2. <span data-ttu-id="c0abe-220">Укажите хранилище ключей для хранения метаданных зашифрованных дисков.</span><span class="sxs-lookup"><span data-stu-id="c0abe-220">Specify the Key Vault to store the metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="c0abe-221">Укажите криптографические ключи для фактического шифрования и расшифровки.</span><span class="sxs-lookup"><span data-stu-id="c0abe-221">Specify the cryptographic keys to use for the actual encryption and decryption.</span></span>
4. <span data-ttu-id="c0abe-222">Укажите, что следует шифровать: диск ОС, диски данных или и то, и другое.</span><span class="sxs-lookup"><span data-stu-id="c0abe-222">Specify whether you want to encrypt the OS disk, the data disks, or all.</span></span>

<span data-ttu-id="c0abe-223">Просмотрите сведения о хранилище ключей Azure и созданном ключе, так как вам понадобится идентификатор ключа хранилища, универсальный код ресурса (URI) и URL-адрес ключа на последнем шаге.</span><span class="sxs-lookup"><span data-stu-id="c0abe-223">Lets review the details for your Azure Key Vault and the key you created, as you need the Key Vault ID, URI, and then key URL in the final step:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="c0abe-224">Зашифруйте виртуальные диски с использованием выходных данных из команд `azure keyvault show` и `azure keyvault key show` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c0abe-224">Encrypt your virtual disks using the output from the `azure keyvault show` and `azure keyvault key show` commands as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="c0abe-225">Так как в приведенной выше команде много переменных, в следующем примере приведена вся команда для справки:</span><span class="sxs-lookup"><span data-stu-id="c0abe-225">As the preceding command has many variables, the following example is the complete command for reference:</span></span>

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

<span data-ttu-id="c0abe-226">Интерфейс командной строки Azure не предоставляет подробные сообщения об ошибках в процессе шифрования.</span><span class="sxs-lookup"><span data-stu-id="c0abe-226">The Azure CLI doesn't provide verbose errors during the encryption process.</span></span> <span data-ttu-id="c0abe-227">Дополнительные сведения об устранении неполадок см. в файле `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` на виртуальной машине, на которой вы включаете шифрование.</span><span class="sxs-lookup"><span data-stu-id="c0abe-227">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` on the VM you are encrypting.</span></span>

<span data-ttu-id="c0abe-228">Наконец, просмотрите состояние шифрования снова, чтобы убедиться, что виртуальные диски зашифрованы.</span><span class="sxs-lookup"><span data-stu-id="c0abe-228">Finally, lets review the encryption status again to confirm that your virtual disks have now been encrypted:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a><span data-ttu-id="c0abe-229">Добавление дополнительных дисков данных</span><span class="sxs-lookup"><span data-stu-id="c0abe-229">Add additional data disks</span></span>
<span data-ttu-id="c0abe-230">После того как вы зашифруете диски данных, позже вы сможете добавить дополнительные виртуальные диски в виртуальную машину, а также зашифровать их.</span><span class="sxs-lookup"><span data-stu-id="c0abe-230">Once you have encrypted your data disks, you can later add additional virtual disks to your VM and also encrypt them.</span></span> <span data-ttu-id="c0abe-231">При выполнении команды `azure vm enable-disk-encryption` увеличьте версию последовательности с помощью параметра `--sequence-version`.</span><span class="sxs-lookup"><span data-stu-id="c0abe-231">When you run the `azure vm enable-disk-encryption` command, increment the sequence version using the `--sequence-version` parameter.</span></span> <span data-ttu-id="c0abe-232">Этот параметр версии последовательности позволяет выполнять последовательные операции на одной и той же виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c0abe-232">This sequence version parameter allows you to perform repeated operations on the same VM.</span></span>

<span data-ttu-id="c0abe-233">Например, добавим второй виртуальный диск к виртуальной машине следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c0abe-233">For example, lets add a second virtual disk to your VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="c0abe-234">Повторно выполните команду для шифрования виртуальных дисков, в этот раз добавив параметр `--sequence-version` и увеличив значение, применяемое при первом выполнении, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c0abe-234">Rerun the command to encrypt the virtual disks, this time adding the `--sequence-version` parameter, and incrementing the value from our first run as follows:</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="c0abe-235">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c0abe-235">Next steps</span></span>
* <span data-ttu-id="c0abe-236">Дополнительные сведения об управлении хранилищем ключей Azure, а также об удалении криптографических ключей и хранилищ см. в статье [Управление хранилищем ключей с помощью интерфейса командной строки](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="c0abe-236">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="c0abe-237">Дополнительные сведения о шифровании дисков, а именно о подготовке зашифрованной настраиваемой виртуальной машины к передаче в Azure, см. в статье [Дисковое шифрование Azure для виртуальных машин IaaS под управлением Windows и Linux](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="c0abe-237">For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
