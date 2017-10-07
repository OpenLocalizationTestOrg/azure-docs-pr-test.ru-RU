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
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-20"></a>Управление пользователями, SSH и проверку или восстановление дисков виртуальных машин Linux с помощью расширения VMAccess hello с hello Azure CLI 2.0
Hello диска на ВМ Linux отображаются ошибки. Каким-либо образом сбросить пароль учетной записи root hello для ВМ Linux или случайно удалены ваш закрытый ключ SSH. Если обратно в днях hello hello центра обработки данных, описанную бы требуется toodrive существует, а затем откройте tooget KVM hello в консоли сервера hello. Считаете hello расширения Azure VMAccess, KVM-коммутатор, который позволяет tooaccess hello tooLinux доступа tooreset консоли или уровня обслуживания диска.

В этой статье показано, как toouse hello Azure расширения VMAccess toocheck восстановления диска, доступ пользователей, управление учетными записями пользователей и перезагрузки конфигурации hello SSH в Linux. Можно также выполнить следующие действия с hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="ways-toouse-hello-vmaccess-extension"></a>Hello toouse способов расширения VMAccess
Существует два способа, которые можно использовать расширение VMAccess hello на виртуальные машины Linux:

* Используйте hello Azure CLI 2.0 и hello необходимые параметры.
* [Необработанный JSON используйте файлы, процесс расширения VMAccess hello](#use-json-files-and-the-vmaccess-extension) , а затем.

Здравствуйте, следующие примеры использования [пользователя ВМ az](/cli/azure/vm/user) команд. tooperform эти шаги, необходимые hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).

## <a name="reset-ssh-key"></a>Сброс ключа SSH
Hello следующий пример сбрасывает hello SSH-ключ для пользователя hello `azureuser` на hello виртуальной Машины с именем `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a>Сброс пароля
Hello следующий пример сбрасывает hello пароль для пользователя hello `azureuser` на hello виртуальной Машины с именем `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a>Перезапуск SSH
Hello следующий программный код перезапускает управляющая программа SSH hello и сбрасывает hello значения toodefault конфигурации SSH на виртуальной Машине с именем `myVM`:

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a>Создание пользователя
Hello следующий пример создает пользователя с именем `myNewUser` с помощью ключа SSH для проверки подлинности на hello виртуальной Машины с именем `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a>Удаление пользователя
Hello следующий пример удаляет пользователя с именем `myNewUser` на hello виртуальной Машины с именем `myVM`:

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-hello-vmaccess-extension"></a>Используйте файлы JSON и hello расширение VMAccess
Следующие примеры Hello использовать необработанные файлы JSON. Используйте [набор расширения ВМ az](/cli/azure/vm/extension#set) toothen вызова JSON-файлов. Эти JSON-файлы также можно вызывать из шаблонов Azure. 

### <a name="reset-user-access"></a>Сброс доступа пользователей
В случае потери доступа tooroot на ВМ Linux, можно запустить скрипт VMAccess tooreset ключ SSH или пароль пользователя.

открытый ключ SSH hello-tooreset пользователя, создайте файл с именем `reset_ssh_key.json` и добавьте параметры в кодировке hello. Подставьте собственные значения для hello `username` и `ssh_key` параметры:

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

Выполните сценарий VMAccess hello с:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

tooreset пароль пользователя, создайте файл с именем `reset_user_password.json` и добавьте параметры в кодировке hello. Подставьте собственные значения для hello `username` и `password` параметры:

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

Выполните сценарий VMAccess hello с:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a>Перезапуск SSH
Здравствуйте, управляющая программа SSH и сбросить значения toodefault конфигурации SSH hello, создайте файл с именем toorestart `reset_sshd.json`. Добавьте следующие содержимое hello:

```json
{
  "reset_ssh": true
}
```

Выполните сценарий VMAccess hello с:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a>Управление пользователями

toocreate пользователя, который использует ключ SSH для проверки подлинности, создайте файл с именем `create_new_user.json` и добавьте параметры в кодировке hello. Подставьте собственные значения для hello `username` и `ssh_key` параметры:

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

Выполните сценарий VMAccess hello с:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

toodelete пользователя, создайте файл с именем `delete_user.json` и добавьте следующие содержимое hello. Подставьте собственные значения для hello `remove_user` параметр:

```json
{
  "remove_user":"myNewUser"
}
```

Выполните сценарий VMAccess hello с:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-hello-disk"></a>Проверьте или восстановить диск hello
С помощью VMAccess можно также проверить и восстановить диск, что вы добавили toohello ВМ Linux.

toocheck, а затем может восстанавливать hello, создайте файл с именем `disk_check_repair.json` и добавьте параметры в кодировке hello. Замените значение hello имя `repair_disk`:

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

Выполните сценарий VMAccess hello с:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a>Дальнейшие действия
Обновление Linux с помощью hello расширения VMAccess Azure является одно изменение метода toomake на работающей ВМ Linux. Также можно использовать такие средства, как облачные init и toomodify шаблонов диспетчера ресурсов Azure ВМ Linux во время загрузки.

[Обзор расширений и компонентов виртуальных машин под управлением Linux](extensions-features.md)

[Разработка шаблонов Azure Resource Manager с расширениями виртуальной машины Linux](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[С помощью toocustomize init облака виртуальной Машины Linux во время создания](using-cloud-init.md)

