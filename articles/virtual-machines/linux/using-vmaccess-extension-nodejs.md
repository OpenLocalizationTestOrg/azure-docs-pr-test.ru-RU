---
title: "Здравствуйте, aaaReset доступа на виртуальных машинах Linux в Azure с помощью расширения VMAccess | Документы Microsoft"
description: "Сбросить настройки доступа на виртуальных машинах Azure Linux с помощью расширения VMAccess hello."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: 2636655f3f7d14ba30e1dc62c319e4e278521ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-10"></a><span data-ttu-id="9ff59-103">Управление пользователями, SSH и проверку или восстановление дисков на виртуальных машинах Linux в Azure с помощью расширения VMAccess hello с hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="9ff59-103">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension with hello Azure CLI 1.0</span></span>
<span data-ttu-id="9ff59-104">В этой статье показано, как toouse hello Azure VMAcesss расширения toocheck восстановления диска, доступ пользователей, управление учетными записями пользователей и перезагрузки конфигурации SSHD hello в Linux.</span><span class="sxs-lookup"><span data-stu-id="9ff59-104">This article shows you how toouse hello Azure VMAcesss Extension toocheck or repair a disk, reset user access, manage user accounts, or reset hello SSHD configuration on Linux.</span></span> <span data-ttu-id="9ff59-105">требуются Hello статьи:</span><span class="sxs-lookup"><span data-stu-id="9ff59-105">hello article requires:</span></span>

* <span data-ttu-id="9ff59-106">Учетная запись Azure ([получите бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/)).</span><span class="sxs-lookup"><span data-stu-id="9ff59-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="9ff59-107">Hello [Azure CLI](../../cli-install-nodejs.md) вход в систему `azure login`.</span><span class="sxs-lookup"><span data-stu-id="9ff59-107">hello [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="9ff59-108">Hello Azure CLI *должен находиться в* режим диспетчера ресурсов Azure `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="9ff59-108">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="9ff59-109">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="9ff59-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="9ff59-110">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="9ff59-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="9ff59-111">[Azure CLI 1.0](#quick-commands)— нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="9ff59-111">[Azure CLI 1.0](#quick-commands)– our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="9ff59-112">[Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="9ff59-112">[Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="9ff59-113">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="9ff59-113">Quick commands</span></span>
<span data-ttu-id="9ff59-114">Существует два способа toouse VMAccess на виртуальные машины Linux:</span><span class="sxs-lookup"><span data-stu-id="9ff59-114">There are two ways toouse VMAccess on your Linux VMs:</span></span>

* <span data-ttu-id="9ff59-115">С помощью Azure CLI 1.0 hello и hello необходимые параметры.</span><span class="sxs-lookup"><span data-stu-id="9ff59-115">Using hello Azure CLI 1.0 and hello required parameters.</span></span>
* <span data-ttu-id="9ff59-116">С помощью необработанных файлов JSON, которые расширение VMAccess обрабатывает для выполнения операций с ними.</span><span class="sxs-lookup"><span data-stu-id="9ff59-116">Using raw JSON files that VMAccess processes and then act on.</span></span>

<span data-ttu-id="9ff59-117">Для секции команду Быстрый hello, мы будем toouse hello Azure CLI 1.0 `azure vm reset-access` метод.</span><span class="sxs-lookup"><span data-stu-id="9ff59-117">For hello quick command section, we are going toouse hello Azure CLI 1.0 `azure vm reset-access` method.</span></span> <span data-ttu-id="9ff59-118">В hello в примерах команд замените hello значения, которые содержат «пример» со значениями hello из вашей среды.</span><span class="sxs-lookup"><span data-stu-id="9ff59-118">In hello following command examples, replace hello values that contain "example" with hello values from your own environment.</span></span>

## <a name="create-a-resource-group-and-linux-vm"></a><span data-ttu-id="9ff59-119">Создание группы ресурсов и виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="9ff59-119">Create a Resource Group and Linux VM</span></span>
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a><span data-ttu-id="9ff59-120">Создание виртуальной машины Debian</span><span class="sxs-lookup"><span data-stu-id="9ff59-120">Create a Debian VM</span></span>
```azurecli
azure vm quick-create \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -g myResourceGroup \
  -l westus \
  -y Linux \
  -n myVM \
  -Q Debian
```

## <a name="reset-root-password"></a><span data-ttu-id="9ff59-121">Сброс пароля пользователя root</span><span class="sxs-lookup"><span data-stu-id="9ff59-121">Reset root password</span></span>
<span data-ttu-id="9ff59-122">пароль пользователя root hello tooreset:</span><span class="sxs-lookup"><span data-stu-id="9ff59-122">tooreset hello root password:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a><span data-ttu-id="9ff59-123">Сброс ключа SSH</span><span class="sxs-lookup"><span data-stu-id="9ff59-123">SSH key reset</span></span>
<span data-ttu-id="9ff59-124">tooreset ключ SSH hello непривилегированного пользователя:</span><span class="sxs-lookup"><span data-stu-id="9ff59-124">tooreset hello SSH key of a non-root user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a><span data-ttu-id="9ff59-125">Создание пользователя</span><span class="sxs-lookup"><span data-stu-id="9ff59-125">Create a user</span></span>
<span data-ttu-id="9ff59-126">toocreate пользователь:</span><span class="sxs-lookup"><span data-stu-id="9ff59-126">toocreate a user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a><span data-ttu-id="9ff59-127">Удаление пользователя</span><span class="sxs-lookup"><span data-stu-id="9ff59-127">Remove a user</span></span>
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a><span data-ttu-id="9ff59-128">Сброс SSHD</span><span class="sxs-lookup"><span data-stu-id="9ff59-128">Reset SSHD</span></span>
<span data-ttu-id="9ff59-129">Конфигурация SSHD tooreset hello:</span><span class="sxs-lookup"><span data-stu-id="9ff59-129">tooreset hello SSHD configuration:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a><span data-ttu-id="9ff59-130">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="9ff59-130">Detailed walkthrough</span></span>
### <a name="vmaccess-defined"></a><span data-ttu-id="9ff59-131">Определение VMAccess</span><span class="sxs-lookup"><span data-stu-id="9ff59-131">VMAccess defined:</span></span>
<span data-ttu-id="9ff59-132">Hello диска на ВМ Linux отображаются ошибки.</span><span class="sxs-lookup"><span data-stu-id="9ff59-132">hello disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="9ff59-133">Каким-либо образом сбросить пароль учетной записи root hello для ВМ Linux или случайно удалены ваш закрытый ключ SSH.</span><span class="sxs-lookup"><span data-stu-id="9ff59-133">You somehow reset hello root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="9ff59-134">Если обратно в днях hello hello центра обработки данных, описанную бы требуется toodrive существует, а затем откройте tooget KVM hello в консоли сервера hello.</span><span class="sxs-lookup"><span data-stu-id="9ff59-134">If that happened back in hello days of hello datacenter, you would need toodrive there and then open hello KVM tooget at hello server console.</span></span> <span data-ttu-id="9ff59-135">Считаете hello расширения Azure VMAccess, KVM-коммутатор, который позволяет tooaccess hello tooLinux доступа tooreset консоли или уровня обслуживания диска.</span><span class="sxs-lookup"><span data-stu-id="9ff59-135">Think of hello Azure VMAccess extension as that KVM switch that allows you tooaccess hello console tooreset access tooLinux or perform disk level maintenance.</span></span>

<span data-ttu-id="9ff59-136">Подробную hello пошаговом руководстве мы будем toouse hello длинная форма VMAccess, который использует необработанные файлы JSON.</span><span class="sxs-lookup"><span data-stu-id="9ff59-136">For hello detailed walkthrough, we are going toouse hello long form of VMAccess, which uses raw JSON files.</span></span>  <span data-ttu-id="9ff59-137">Эти файлы JSON VMAccess также можно вызывать из шаблонов Azure.</span><span class="sxs-lookup"><span data-stu-id="9ff59-137">These VMAccess JSON files can also be called from Azure templates.</span></span>

### <a name="using-vmaccess-toocheck-or-repair-hello-disk-of-a-linux-vm"></a><span data-ttu-id="9ff59-138">С помощью VMAccess toocheck или восстановление диска hello ВМ Linux</span><span class="sxs-lookup"><span data-stu-id="9ff59-138">Using VMAccess toocheck or repair hello disk of a Linux VM</span></span>
<span data-ttu-id="9ff59-139">С помощью VMAccess можно сделать fsck на диске hello в ВМ Linux.</span><span class="sxs-lookup"><span data-stu-id="9ff59-139">Using VMAccess you can do a fsck run on hello disk under your Linux VM.</span></span>  <span data-ttu-id="9ff59-140">Также можно выполнить проверку и восстановление диска с помощью VMAccess.</span><span class="sxs-lookup"><span data-stu-id="9ff59-140">You can also do a disk check and a disk repair using a VMAccess.</span></span>

<span data-ttu-id="9ff59-141">Этот сценарий VMAccess использовать toocheck, а затем hello диск восстановления:</span><span class="sxs-lookup"><span data-stu-id="9ff59-141">toocheck, and then repair hello disk use this VMAccess script:</span></span>

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

<span data-ttu-id="9ff59-142">Выполните сценарий VMAccess hello с:</span><span class="sxs-lookup"><span data-stu-id="9ff59-142">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-tooreset-user-access-toolinux"></a><span data-ttu-id="9ff59-143">С помощью пользовательского доступа VMAccess tooreset tooLinux</span><span class="sxs-lookup"><span data-stu-id="9ff59-143">Using VMAccess tooreset user access tooLinux</span></span>
<span data-ttu-id="9ff59-144">В случае потери доступа tooroot на ВМ Linux, вы можете запустить VMAccess сценария tooreset hello корневой пароль.</span><span class="sxs-lookup"><span data-stu-id="9ff59-144">If you have lost access tooroot on your Linux VM, you can launch a VMAccess script tooreset hello root password.</span></span>

<span data-ttu-id="9ff59-145">tooreset hello пароль учетной записи root, с помощью этого сценария VMAccess:</span><span class="sxs-lookup"><span data-stu-id="9ff59-145">tooreset hello root password, use this VMAccess script:</span></span>

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

<span data-ttu-id="9ff59-146">Выполните сценарий VMAccess hello с:</span><span class="sxs-lookup"><span data-stu-id="9ff59-146">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

<span data-ttu-id="9ff59-147">ключ SSH hello tooreset непривилегированного пользователя, с помощью этого сценария VMAccess:</span><span class="sxs-lookup"><span data-stu-id="9ff59-147">tooreset hello SSH key of a non-root user, use this VMAccess script:</span></span>

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

<span data-ttu-id="9ff59-148">Выполните сценарий VMAccess hello с:</span><span class="sxs-lookup"><span data-stu-id="9ff59-148">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-toomanage-user-accounts-on-linux"></a><span data-ttu-id="9ff59-149">С помощью учетных записей пользователей toomanage VMAccess в Linux</span><span class="sxs-lookup"><span data-stu-id="9ff59-149">Using VMAccess toomanage user accounts on Linux</span></span>
<span data-ttu-id="9ff59-150">VMAccess — это сценарий Python, который может быть пользователей используется toomanage на ВМ Linux без регистрации и использования учетной записи root sudo или hello.</span><span class="sxs-lookup"><span data-stu-id="9ff59-150">VMAccess is a Python script that can be used toomanage users on your Linux VM without logging in and using sudo or hello root account.</span></span>

<span data-ttu-id="9ff59-151">toocreate пользователя, с помощью этого сценария VMAccess:</span><span class="sxs-lookup"><span data-stu-id="9ff59-151">toocreate a user, use this VMAccess script:</span></span>

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="9ff59-152">Выполните сценарий VMAccess hello с:</span><span class="sxs-lookup"><span data-stu-id="9ff59-152">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

<span data-ttu-id="9ff59-153">toodelete пользователя, с помощью этого сценария VMAccess:</span><span class="sxs-lookup"><span data-stu-id="9ff59-153">toodelete a user, use this VMAccess script:</span></span>

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

<span data-ttu-id="9ff59-154">Выполните сценарий VMAccess hello с:</span><span class="sxs-lookup"><span data-stu-id="9ff59-154">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-tooreset-hello-sshd-configuration"></a><span data-ttu-id="9ff59-155">С помощью VMAccess tooreset hello SSHD конфигурации</span><span class="sxs-lookup"><span data-stu-id="9ff59-155">Using VMAccess tooreset hello SSHD configuration</span></span>
<span data-ttu-id="9ff59-156">При внесении изменений toohello SSHD виртуальных машин Linux конфигурации и закрыть hello SSH-подключения перед проверкой hello изменения, не разрешается из SSH'ing назад.</span><span class="sxs-lookup"><span data-stu-id="9ff59-156">If you make changes toohello Linux VMs SSHD configuration and close hello SSH connection before verifying hello changes, you may be prevented from SSH'ing back in.</span></span>  <span data-ttu-id="9ff59-157">VMAccess можно использовать tooreset hello SSHD конфигурации задней tooa удачной конфигурации без вход через SSH.</span><span class="sxs-lookup"><span data-stu-id="9ff59-157">VMAccess can be used tooreset hello SSHD configuration back tooa known good configuration without being logged in over SSH.</span></span>

<span data-ttu-id="9ff59-158">Этот сценарий VMAccess использовать tooreset hello SSHD конфигурации:</span><span class="sxs-lookup"><span data-stu-id="9ff59-158">tooreset hello SSHD configuration use this VMAccess script:</span></span>

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="9ff59-159">Выполните сценарий VMAccess hello с:</span><span class="sxs-lookup"><span data-stu-id="9ff59-159">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a><span data-ttu-id="9ff59-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9ff59-160">Next steps</span></span>
<span data-ttu-id="9ff59-161">Обновление Linux с помощью расширения VMAccess Azure является одно изменение метода toomake на работающей ВМ Linux.</span><span class="sxs-lookup"><span data-stu-id="9ff59-161">Updating Linux using Azure VMAccess Extensions is one method toomake changes on a running Linux VM.</span></span>  <span data-ttu-id="9ff59-162">Также можно использовать такие средства, как облачные init и шаблоны Azure toomodify ВМ Linux во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="9ff59-162">You can also use tools like cloud-init and Azure Templates toomodify your Linux VM on boot.</span></span>

[<span data-ttu-id="9ff59-163">Обзор расширений и компонентов виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="9ff59-163">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="9ff59-164">Разработка шаблонов Azure Resource Manager с расширениями виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="9ff59-164">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="9ff59-165">С помощью toocustomize init облака виртуальной Машины Linux во время создания</span><span class="sxs-lookup"><span data-stu-id="9ff59-165">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

