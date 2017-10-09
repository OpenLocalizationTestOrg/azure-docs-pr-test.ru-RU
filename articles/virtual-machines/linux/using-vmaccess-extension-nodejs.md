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
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-10"></a>Управление пользователями, SSH и проверку или восстановление дисков на виртуальных машинах Linux в Azure с помощью расширения VMAccess hello с hello Azure CLI 1.0
В этой статье показано, как toouse hello Azure VMAcesss расширения toocheck восстановления диска, доступ пользователей, управление учетными записями пользователей и перезагрузки конфигурации SSHD hello в Linux. требуются Hello статьи:

* Учетная запись Azure ([получите бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/)).
* Hello [Azure CLI](../../cli-install-nodejs.md) вход в систему `azure login`.
* Hello Azure CLI *должен находиться в* режим диспетчера ресурсов Azure `azure config mode arm`.


## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI
Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

- [Azure CLI 1.0](#quick-commands)— нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)
- [Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -нашей нового поколения CLI для модели развертывания hello ресурсов управления


## <a name="quick-commands"></a>Быстрые команды
Существует два способа toouse VMAccess на виртуальные машины Linux:

* С помощью Azure CLI 1.0 hello и hello необходимые параметры.
* С помощью необработанных файлов JSON, которые расширение VMAccess обрабатывает для выполнения операций с ними.

Для секции команду Быстрый hello, мы будем toouse hello Azure CLI 1.0 `azure vm reset-access` метод. В hello в примерах команд замените hello значения, которые содержат «пример» со значениями hello из вашей среды.

## <a name="create-a-resource-group-and-linux-vm"></a>Создание группы ресурсов и виртуальной машины Linux
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a>Создание виртуальной машины Debian
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

## <a name="reset-root-password"></a>Сброс пароля пользователя root
пароль пользователя root hello tooreset:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a>Сброс ключа SSH
tooreset ключ SSH hello непривилегированного пользователя:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a>Создание пользователя
toocreate пользователь:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a>Удаление пользователя
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a>Сброс SSHD
Конфигурация SSHD tooreset hello:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a>Подробное пошаговое руководство
### <a name="vmaccess-defined"></a>Определение VMAccess
Hello диска на ВМ Linux отображаются ошибки. Каким-либо образом сбросить пароль учетной записи root hello для ВМ Linux или случайно удалены ваш закрытый ключ SSH. Если обратно в днях hello hello центра обработки данных, описанную бы требуется toodrive существует, а затем откройте tooget KVM hello в консоли сервера hello. Считаете hello расширения Azure VMAccess, KVM-коммутатор, который позволяет tooaccess hello tooLinux доступа tooreset консоли или уровня обслуживания диска.

Подробную hello пошаговом руководстве мы будем toouse hello длинная форма VMAccess, который использует необработанные файлы JSON.  Эти файлы JSON VMAccess также можно вызывать из шаблонов Azure.

### <a name="using-vmaccess-toocheck-or-repair-hello-disk-of-a-linux-vm"></a>С помощью VMAccess toocheck или восстановление диска hello ВМ Linux
С помощью VMAccess можно сделать fsck на диске hello в ВМ Linux.  Также можно выполнить проверку и восстановление диска с помощью VMAccess.

Этот сценарий VMAccess использовать toocheck, а затем hello диск восстановления:

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

Выполните сценарий VMAccess hello с:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-tooreset-user-access-toolinux"></a>С помощью пользовательского доступа VMAccess tooreset tooLinux
В случае потери доступа tooroot на ВМ Linux, вы можете запустить VMAccess сценария tooreset hello корневой пароль.

tooreset hello пароль учетной записи root, с помощью этого сценария VMAccess:

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

Выполните сценарий VMAccess hello с:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

ключ SSH hello tooreset непривилегированного пользователя, с помощью этого сценария VMAccess:

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

Выполните сценарий VMAccess hello с:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-toomanage-user-accounts-on-linux"></a>С помощью учетных записей пользователей toomanage VMAccess в Linux
VMAccess — это сценарий Python, который может быть пользователей используется toomanage на ВМ Linux без регистрации и использования учетной записи root sudo или hello.

toocreate пользователя, с помощью этого сценария VMAccess:

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

Выполните сценарий VMAccess hello с:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

toodelete пользователя, с помощью этого сценария VMAccess:

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

Выполните сценарий VMAccess hello с:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-tooreset-hello-sshd-configuration"></a>С помощью VMAccess tooreset hello SSHD конфигурации
При внесении изменений toohello SSHD виртуальных машин Linux конфигурации и закрыть hello SSH-подключения перед проверкой hello изменения, не разрешается из SSH'ing назад.  VMAccess можно использовать tooreset hello SSHD конфигурации задней tooa удачной конфигурации без вход через SSH.

Этот сценарий VMAccess использовать tooreset hello SSHD конфигурации:

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

Выполните сценарий VMAccess hello с:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a>Дальнейшие действия
Обновление Linux с помощью расширения VMAccess Azure является одно изменение метода toomake на работающей ВМ Linux.  Также можно использовать такие средства, как облачные init и шаблоны Azure toomodify ВМ Linux во время загрузки.

[Обзор расширений и компонентов виртуальной машины](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Разработка шаблонов Azure Resource Manager с расширениями виртуальной машины Linux](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[С помощью toocustomize init облака виртуальной Машины Linux во время создания](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

