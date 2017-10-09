---
title: "toocustomize aaaUsing init облака виртуальной Машины Linux во время создания в Azure | Документы Microsoft"
description: "Как облачные init toocustomize toouse в виртуальной Машине Linux во время создания с hello Azure CLI 1.0"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: v-livech
ms.openlocfilehash: b9f480bd04029956d0593bbef931795733cbc2f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation-with-hello-azure-cli-10"></a>Использовать toocustomize init облака виртуальной Машины Linux во время создания с hello Azure CLI 1.0
В этой статье показано, как toomake tooset сценарий облака init hello имя узла, установленных пакетов обновления и управление учетными записями пользователей.  во время создания виртуальной Машины из Azure CLI hello вызываются Hello init облачных сценариев.  требуются Hello статьи:

* Учетная запись Azure ([получите бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/)).
* Hello [Azure CLI](../../cli-install-nodejs.md) вход в систему `azure login`.
* Hello Azure CLI *должен находиться в* режим диспетчера ресурсов Azure `azure config mode arm`.

## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI
Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

- [Azure CLI 1.0](#quick-commands) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)
- [Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -нашей нового поколения CLI для модели развертывания hello ресурсов управления

## <a name="quick-commands"></a>Быстрые команды
Создание облака init.txt скрипт, который задает имя узла hello, все пакеты обновления и добавляет tooLinux sudo пользователя.

```sh
#cloud-config
hostname: myVMhostname
apt_upgrade: true
users:
  - name: myNewAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myVM
```
Создание виртуальных машин в toolaunch группы ресурсов.

```azurecli
azure group create myResourceGroup westus
```

Создайте виртуальную Машину Linux с помощью облака init tooconfigure его во время загрузки.

```azurecli
azure vm create \
  -g myResourceGroup \
  -n myVM \
  -l westus \
  -y Linux \
  -f myVMnic \
  -F myVNet \
  -P 10.0.0.0/22 \
  -j mySubnet \
  -k 10.0.0.0/24 \
  -Q canonical:ubuntuserver:14.04.2-LTS:latest \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -C cloud-init.txt
```

## <a name="detailed-walkthrough"></a>Подробное пошаговое руководство
### <a name="introduction"></a>Введение
При запуске новой виртуальной машины Linux вы получаете стандартную виртуальную машину, не настроенную под ваши потребности. [Облако init](https://cloudinit.readthedocs.org) является tooinject стандартный способ скрипт или конфигурации параметры в этой виртуальной Машины Linux при загрузке для hello первый раз.

В Azure, существует три различных способа изменения toomake на виртуальной Машине Linux время развернут или загружен.

* Внедрить сценарии с помощью cloud-init.
* Внедрить скриптов с использованием hello Azure [расширения VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Шаблон Azure с использованием cloud-init.
* Шаблон Azure с использованием расширения [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

сценарии tooinject в любое время после загрузки.

* Непосредственно команды toorun SSH
* Внедрить скриптов с использованием hello Azure [расширения VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), принудительно или в шаблоне Azure
* Воспользоваться средствами управления, такими как Ansible, Salt, Chef или Puppet.

> [!NOTE]
> : Расширение VMAccess выполняет скрипт как корневой hello же можно с помощью SSH.  Тем не менее использование расширения ВМ hello позволяет несколько функций, Azure предлагает, которые могут быть полезны в зависимости от ситуации.
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a>Доступность cloud-init для псевдонимов быстрого создания образов виртуальных машин Azure:
| Alias | Издатель | ПРЕДЛОЖЕНИЕ | SKU | Version (версия) | cloud-init |
|:--- |:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |CentOS |7,2 |последних |Нет |
| CoreOS |CoreOS |CoreOS |Stable |последних |Да |
| Debian |credativ |Debian |8 |последних |Нет |
| openSUSE |SUSE |openSUSE |13.2 |последних |Нет |
| RHEL |Redhat |RHEL |7,2 |последних |Нет |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |последних |Да |

Microsoft является работа с наших партнеров tooget облака init включены и работу в том, что они предоставляют tooAzure образы hello.

## <a name="adding-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a>Добавление создания облака init скрипта toohello ВМ с hello Azure CLI
toolaunch сценарий init облака при создании виртуальной Машины в Azure, укажите файл init облака hello, с помощью hello Azure CLI `--custom-data` переключения.

Создание виртуальных машин в toolaunch группы ресурсов.

```azurecli
azure group create myResourceGroup westus
```

Создайте виртуальную Машину Linux с помощью облака init tooconfigure его во время загрузки.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubnet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud-init.txt
```

## <a name="creating-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a>Создание облака init сценария tooset hello имени узла виртуальной машины Linux
Одним из hello простейшим и наиболее важные параметры для виртуальной Машины с Linux будет hello имя узла. Его можно легко задать с помощью приведенного ниже сценария cloud-init.  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a>Пример сценария cloud-init с именем `cloud_config_hostname.txt`
```sh
#cloud-config
hostname: myservername
```

Во время запуска начальной hello hello виртуальной Машины, этот сценарий облака init задает hello hostname, слишком`myservername`.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_hostname.txt
```

Имя входа и проверьте имя узла hello hello новой виртуальной Машины.

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-tooupdate-linux"></a>Создание облака init сценария tooupdate Linux
В целях безопасности необходимо tooupdate вашей виртуальной Машине Ubuntu при первой загрузке hello.  С помощью init облака можно сделать с hello выполните скрипт, в зависимости от hello дистрибутив Linux, которые вы используете.

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a>Пример сценария в облаке init `cloud_config_apt_upgrade.txt` для hello Debian семейства
```sh
#cloud-config
apt_upgrade: true
```

После загрузки операционной системы Linux, все пакеты установки hello обновляются через `apt-get`.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_apt_upgrade.txt
```

Выполните вход и проверьте, обновились ли все пакеты.

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
hello following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 tooremove and 0 not upgraded.
```

## <a name="creating-a-cloud-init-script-tooadd-a-user-toolinux"></a>Создание tooadd сценария облака init tooLinux пользователя
Один из первых задач hello на все новые виртуальные Машины Linux — tooadd пользователя для себя, или с помощью tooavoid `root`. SSH ключи — это рекомендуется для безопасности и удобство использования и они добавляются toohello `~/.ssh/authorized_keys` файл с помощью этого сценария init облака.

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a>Пример сценария cloud-init `cloud_config_add_users.txt` для семейства Debian
```sh
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

После загрузки операционной системы Linux, все пользователи в списке hello являются группа создана и добавлена toohello sudo.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_add_users.txt
```

Имя входа и проверки hello только что созданный пользователь.

```bash
ssh myVM
cat /etc/group
```

Выходные данные

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a>Дальнейшие действия
Облако init становится один стандартный способ toomodify ВМ Linux во время загрузки. Azure также имеет расширения ВМ, позволяющих toomodify вашей LinuxVM во время загрузки или пока она запущена. Например можно использовать hello Azure VMAccessExtension tooreset SSH или сведения о пользователе во время выполнения hello виртуальной Машины. С инициализацией облака потребуется перезагрузка tooreset hello пароль.

[Обзор расширений и компонентов виртуальной машины](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Управлять пользователями, SSH и проверку или восстановление дисков на виртуальных машинах Linux в Azure с помощью hello расширения VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

