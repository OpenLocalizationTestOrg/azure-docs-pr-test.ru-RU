---
title: "tooan aaaReset доступа к виртуальной Машине Linux Azure | Документы Microsoft"
description: "Как toomanage пользователей и сброс доступа на виртуальных машинах Linux с помощью расширения VMAccess hello и hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/04/2017
ms.author: danlep
ms.openlocfilehash: 2f8db01b9fac20bf547d8b1926e5c0b3c5d18280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-20"></a><span data-ttu-id="93dbb-103">Управление пользователями, SSH и проверку или восстановление дисков виртуальных машин Linux с помощью расширения VMAccess hello с hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="93dbb-103">Manage users, SSH, and check or repair disks on Linux VMs using hello VMAccess Extension with hello Azure CLI 2.0</span></span>
<span data-ttu-id="93dbb-104">Hello диска на ВМ Linux отображаются ошибки.</span><span class="sxs-lookup"><span data-stu-id="93dbb-104">hello disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="93dbb-105">Каким-либо образом сбросить пароль учетной записи root hello для ВМ Linux или случайно удалены ваш закрытый ключ SSH.</span><span class="sxs-lookup"><span data-stu-id="93dbb-105">You somehow reset hello root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="93dbb-106">Если обратно в днях hello hello центра обработки данных, описанную бы требуется toodrive существует, а затем откройте tooget KVM hello в консоли сервера hello.</span><span class="sxs-lookup"><span data-stu-id="93dbb-106">If that happened back in hello days of hello datacenter, you would need toodrive there and then open hello KVM tooget at hello server console.</span></span> <span data-ttu-id="93dbb-107">Считаете hello расширения Azure VMAccess, KVM-коммутатор, который позволяет tooaccess hello tooLinux доступа tooreset консоли или уровня обслуживания диска.</span><span class="sxs-lookup"><span data-stu-id="93dbb-107">Think of hello Azure VMAccess extension as that KVM switch that allows you tooaccess hello console tooreset access tooLinux or perform disk level maintenance.</span></span>

<span data-ttu-id="93dbb-108">В этой статье показано, как toouse hello Azure расширения VMAccess toocheck восстановления диска, доступ пользователей, управление учетными записями пользователей и перезагрузки конфигурации hello SSH в Linux.</span><span class="sxs-lookup"><span data-stu-id="93dbb-108">This article shows you how toouse hello Azure VMAccess Extension toocheck or repair a disk, reset user access, manage user accounts, or reset hello SSH configuration on Linux.</span></span> <span data-ttu-id="93dbb-109">Можно также выполнить следующие действия с hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="93dbb-109">You can also perform these steps with hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="ways-toouse-hello-vmaccess-extension"></a><span data-ttu-id="93dbb-110">Hello toouse способов расширения VMAccess</span><span class="sxs-lookup"><span data-stu-id="93dbb-110">Ways toouse hello VMAccess Extension</span></span>
<span data-ttu-id="93dbb-111">Существует два способа, которые можно использовать расширение VMAccess hello на виртуальные машины Linux:</span><span class="sxs-lookup"><span data-stu-id="93dbb-111">There are two ways that you can use hello VMAccess Extension on your Linux VMs:</span></span>

* <span data-ttu-id="93dbb-112">Используйте hello Azure CLI 2.0 и hello необходимые параметры.</span><span class="sxs-lookup"><span data-stu-id="93dbb-112">Use hello Azure CLI 2.0 and hello required parameters.</span></span>
* <span data-ttu-id="93dbb-113">[Необработанный JSON используйте файлы, процесс расширения VMAccess hello](#use-json-files-and-the-vmaccess-extension) , а затем.</span><span class="sxs-lookup"><span data-stu-id="93dbb-113">[Use raw JSON files that hello VMAccess Extension process](#use-json-files-and-the-vmaccess-extension) and then act on.</span></span>

<span data-ttu-id="93dbb-114">Здравствуйте, следующие примеры использования [пользователя ВМ az](/cli/azure/vm/user) команд.</span><span class="sxs-lookup"><span data-stu-id="93dbb-114">hello following examples use [az vm user](/cli/azure/vm/user) commands.</span></span> <span data-ttu-id="93dbb-115">tooperform эти шаги, необходимые hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="93dbb-115">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="reset-ssh-key"></a><span data-ttu-id="93dbb-116">Сброс ключа SSH</span><span class="sxs-lookup"><span data-stu-id="93dbb-116">Reset SSH key</span></span>
<span data-ttu-id="93dbb-117">Hello следующий пример сбрасывает hello SSH-ключ для пользователя hello `azureuser` на hello виртуальной Машины с именем `myVM`:</span><span class="sxs-lookup"><span data-stu-id="93dbb-117">hello following example resets hello SSH key for hello user `azureuser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a><span data-ttu-id="93dbb-118">Сброс пароля</span><span class="sxs-lookup"><span data-stu-id="93dbb-118">Reset password</span></span>
<span data-ttu-id="93dbb-119">Hello следующий пример сбрасывает hello пароль для пользователя hello `azureuser` на hello виртуальной Машины с именем `myVM`:</span><span class="sxs-lookup"><span data-stu-id="93dbb-119">hello following example resets hello password for hello user `azureuser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a><span data-ttu-id="93dbb-120">Перезапуск SSH</span><span class="sxs-lookup"><span data-stu-id="93dbb-120">Restart SSH</span></span>
<span data-ttu-id="93dbb-121">Hello следующий программный код перезапускает управляющая программа SSH hello и сбрасывает hello значения toodefault конфигурации SSH на виртуальной Машине с именем `myVM`:</span><span class="sxs-lookup"><span data-stu-id="93dbb-121">hello following example restarts hello SSH daemon and resets hello SSH configuration toodefault values on a VM named `myVM`:</span></span>

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a><span data-ttu-id="93dbb-122">Создание пользователя</span><span class="sxs-lookup"><span data-stu-id="93dbb-122">Create a user</span></span>
<span data-ttu-id="93dbb-123">Hello следующий пример создает пользователя с именем `myNewUser` с помощью ключа SSH для проверки подлинности на hello виртуальной Машины с именем `myVM`:</span><span class="sxs-lookup"><span data-stu-id="93dbb-123">hello following example creates a user named `myNewUser` using an SSH key for authentication on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a><span data-ttu-id="93dbb-124">Удаление пользователя</span><span class="sxs-lookup"><span data-stu-id="93dbb-124">Delete a user</span></span>
<span data-ttu-id="93dbb-125">Hello следующий пример удаляет пользователя с именем `myNewUser` на hello виртуальной Машины с именем `myVM`:</span><span class="sxs-lookup"><span data-stu-id="93dbb-125">hello following example deletes a user named `myNewUser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-hello-vmaccess-extension"></a><span data-ttu-id="93dbb-126">Используйте файлы JSON и hello расширение VMAccess</span><span class="sxs-lookup"><span data-stu-id="93dbb-126">Use JSON files and hello VMAccess Extension</span></span>
<span data-ttu-id="93dbb-127">Следующие примеры Hello использовать необработанные файлы JSON.</span><span class="sxs-lookup"><span data-stu-id="93dbb-127">hello following examples use raw JSON files.</span></span> <span data-ttu-id="93dbb-128">Используйте [набор расширения ВМ az](/cli/azure/vm/extension#set) toothen вызова JSON-файлов.</span><span class="sxs-lookup"><span data-stu-id="93dbb-128">Use [az vm extension set](/cli/azure/vm/extension#set) toothen call your JSON files.</span></span> <span data-ttu-id="93dbb-129">Эти JSON-файлы также можно вызывать из шаблонов Azure.</span><span class="sxs-lookup"><span data-stu-id="93dbb-129">These JSON files can also be called from Azure templates.</span></span> 

### <a name="reset-user-access"></a><span data-ttu-id="93dbb-130">Сброс доступа пользователей</span><span class="sxs-lookup"><span data-stu-id="93dbb-130">Reset user access</span></span>
<span data-ttu-id="93dbb-131">В случае потери доступа tooroot на ВМ Linux, можно запустить скрипт VMAccess tooreset ключ SSH или пароль пользователя.</span><span class="sxs-lookup"><span data-stu-id="93dbb-131">If you have lost access tooroot on your Linux VM, you can launch a VMAccess script tooreset a user's SSH key or password.</span></span>

<span data-ttu-id="93dbb-132">открытый ключ SSH hello-tooreset пользователя, создайте файл с именем `reset_ssh_key.json` и добавьте параметры в кодировке hello.</span><span class="sxs-lookup"><span data-stu-id="93dbb-132">tooreset hello SSH public key of a user, create a file named `reset_ssh_key.json` and add settings in hello following format.</span></span> <span data-ttu-id="93dbb-133">Подставьте собственные значения для hello `username` и `ssh_key` параметры:</span><span class="sxs-lookup"><span data-stu-id="93dbb-133">Substitute your own values for hello `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

<span data-ttu-id="93dbb-134">Выполните сценарий VMAccess hello с:</span><span class="sxs-lookup"><span data-stu-id="93dbb-134">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

<span data-ttu-id="93dbb-135">tooreset пароль пользователя, создайте файл с именем `reset_user_password.json` и добавьте параметры в кодировке hello.</span><span class="sxs-lookup"><span data-stu-id="93dbb-135">tooreset a user password, create a file named `reset_user_password.json` and add settings in hello following format.</span></span> <span data-ttu-id="93dbb-136">Подставьте собственные значения для hello `username` и `password` параметры:</span><span class="sxs-lookup"><span data-stu-id="93dbb-136">Substitute your own values for hello `username` and `password` parameters:</span></span>

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

<span data-ttu-id="93dbb-137">Выполните сценарий VMAccess hello с:</span><span class="sxs-lookup"><span data-stu-id="93dbb-137">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a><span data-ttu-id="93dbb-138">Перезапуск SSH</span><span class="sxs-lookup"><span data-stu-id="93dbb-138">Restart SSH</span></span>
<span data-ttu-id="93dbb-139">Здравствуйте, управляющая программа SSH и сбросить значения toodefault конфигурации SSH hello, создайте файл с именем toorestart `reset_sshd.json`.</span><span class="sxs-lookup"><span data-stu-id="93dbb-139">toorestart hello SSH daemon and reset hello SSH configuration toodefault values, create a file named `reset_sshd.json`.</span></span> <span data-ttu-id="93dbb-140">Добавьте следующие содержимое hello:</span><span class="sxs-lookup"><span data-stu-id="93dbb-140">Add hello following content:</span></span>

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="93dbb-141">Выполните сценарий VMAccess hello с:</span><span class="sxs-lookup"><span data-stu-id="93dbb-141">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a><span data-ttu-id="93dbb-142">Управление пользователями</span><span class="sxs-lookup"><span data-stu-id="93dbb-142">Manage users</span></span>

<span data-ttu-id="93dbb-143">toocreate пользователя, который использует ключ SSH для проверки подлинности, создайте файл с именем `create_new_user.json` и добавьте параметры в кодировке hello.</span><span class="sxs-lookup"><span data-stu-id="93dbb-143">toocreate a user that uses an SSH key for authentication, create a file named `create_new_user.json` and add settings in hello following format.</span></span> <span data-ttu-id="93dbb-144">Подставьте собственные значения для hello `username` и `ssh_key` параметры:</span><span class="sxs-lookup"><span data-stu-id="93dbb-144">Substitute your own values for hello `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="93dbb-145">Выполните сценарий VMAccess hello с:</span><span class="sxs-lookup"><span data-stu-id="93dbb-145">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

<span data-ttu-id="93dbb-146">toodelete пользователя, создайте файл с именем `delete_user.json` и добавьте следующие содержимое hello.</span><span class="sxs-lookup"><span data-stu-id="93dbb-146">toodelete a user, create a file named `delete_user.json` and add hello following content.</span></span> <span data-ttu-id="93dbb-147">Подставьте собственные значения для hello `remove_user` параметр:</span><span class="sxs-lookup"><span data-stu-id="93dbb-147">Substitute your own value for hello `remove_user` parameter:</span></span>

```json
{
  "remove_user":"myNewUser"
}
```

<span data-ttu-id="93dbb-148">Выполните сценарий VMAccess hello с:</span><span class="sxs-lookup"><span data-stu-id="93dbb-148">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-hello-disk"></a><span data-ttu-id="93dbb-149">Проверьте или восстановить диск hello</span><span class="sxs-lookup"><span data-stu-id="93dbb-149">Check or repair hello disk</span></span>
<span data-ttu-id="93dbb-150">С помощью VMAccess можно также проверить и восстановить диск, что вы добавили toohello ВМ Linux.</span><span class="sxs-lookup"><span data-stu-id="93dbb-150">Using VMAccess you can also check and repair a disk that you added toohello Linux VM.</span></span>

<span data-ttu-id="93dbb-151">toocheck, а затем может восстанавливать hello, создайте файл с именем `disk_check_repair.json` и добавьте параметры в кодировке hello.</span><span class="sxs-lookup"><span data-stu-id="93dbb-151">toocheck and then repair hello disk, create a file named `disk_check_repair.json` and add settings in hello following format.</span></span> <span data-ttu-id="93dbb-152">Замените значение hello имя `repair_disk`:</span><span class="sxs-lookup"><span data-stu-id="93dbb-152">Substitute your own value for hello name of `repair_disk`:</span></span>

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

<span data-ttu-id="93dbb-153">Выполните сценарий VMAccess hello с:</span><span class="sxs-lookup"><span data-stu-id="93dbb-153">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a><span data-ttu-id="93dbb-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="93dbb-154">Next steps</span></span>
<span data-ttu-id="93dbb-155">Обновление Linux с помощью hello расширения VMAccess Azure является одно изменение метода toomake на работающей ВМ Linux.</span><span class="sxs-lookup"><span data-stu-id="93dbb-155">Updating Linux using hello Azure VMAccess Extension is one method toomake changes on a running Linux VM.</span></span> <span data-ttu-id="93dbb-156">Также можно использовать такие средства, как облачные init и toomodify шаблонов диспетчера ресурсов Azure ВМ Linux во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="93dbb-156">You can also use tools like cloud-init and Azure Resource Manager templates toomodify your Linux VM on boot.</span></span>

[<span data-ttu-id="93dbb-157">Обзор расширений и компонентов виртуальных машин под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="93dbb-157">Virtual machine extensions and features for Linux</span></span>](extensions-features.md)

[<span data-ttu-id="93dbb-158">Разработка шаблонов Azure Resource Manager с расширениями виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="93dbb-158">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="93dbb-159">С помощью toocustomize init облака виртуальной Машины Linux во время создания</span><span class="sxs-lookup"><span data-stu-id="93dbb-159">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md)

