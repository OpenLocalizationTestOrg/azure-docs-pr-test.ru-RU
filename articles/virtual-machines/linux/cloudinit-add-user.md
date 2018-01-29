---
title: "Добавление пользователя на виртуальную машину Linux в Azure с помощью cloud-init | Документация Майкрософт"
description: "Как с помощью cloud-init и Azure CLI 2.0 добавить пользователя на создаваемую виртуальную машину Linux"
services: virtual-machines-linux
documentationcenter: 
author: rickstercdn
manager: jeconnoc
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 11/29/2017
ms.author: rclaus
ms.openlocfilehash: 728ffed27747cb298d5da312014a3c9e98b44f1e
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/04/2017
---
# <a name="use-cloud-init-to-add-a-user-to-a-linux-vm-in-azure"></a>Добавление пользователя на виртуальную машину Linux в Azure с помощью cloud-init
В этой статье показано, как с помощью [cloud-init](https://cloudinit.readthedocs.io) добавить пользователя на виртуальную машину или в масштабируемый набор виртуальных машин при подготовке в Azure. Этот скрипт cloud-init выполняется при первой загрузке, если в Azure подготовлены все нужные ресурсы. Дополнительные сведения о встроенной поддержке cloud-init в Azure и поддерживаемых дистрибутивах Linux см. в [обзоре cloud-init](using-cloud-init.md).

## <a name="add-a-user-to-a-vm-with-cloud-init"></a>Добавление пользователя в виртуальную машину с помощью cloud-init
Одна из первых задач, которую необходимо выполнить на любой из новых виртуальных машин Linux, — добавить дополнительного пользователя для себя, чтобы не использовать учетную запись *root*. Для безопасности и удобства мы рекомендуем применять ключи SSH. Их можно добавить в файл *~/.ssh/authorized_keys* с помощью следующего скрипта cloud-init.

Чтобы добавить пользователя на виртуальную машину Linux, создайте файл в текущей оболочке с именем *cloud_init_add_user.txt* и вставьте в него следующую конфигурацию. Для этого примера создайте файл в Cloud Shell, а не на локальном компьютере. Вы можете использовать любой редактор. Введите `sensible-editor cloud_init_add_user.txt`, чтобы создать файл и просмотреть список доступных редакторов. Выберите первый пункт, чтобы использовать редактор **nano**. Убедитесь, что весь файл cloud-init скопирован правильно, особенно первая строка.  Необходимо указать открытый ключ (например, содержимое файла *~/.ssh/id_rsa.pub*) в качестве значения `ssh-authorized-keys:` — здесь оно сокращено для упрощения примера.

```yaml
#cloud-config
users:
  - default
  - name: myadminuser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>
```
> [!NOTE] 
> Файл #cloud-config содержит параметр `- default`. Этот параметр позволяет добавить пользователя к существующему пользователю с правами администратора, созданному во время подготовки. Если создать пользователя без параметра `- default`, автоматически созданный платформой Azure администратор будет перезаписан. 

Прежде чем развернуть этот образ, необходимо создать группу ресурсов с помощью команды [az group create](/cli/azure/group#create). Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими. В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *eastus*.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

Теперь создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create) и укажите файл cloud-init с помощью `--custom-data cloud_init_add_user.txt`, как показано ниже.

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroup \
  --name centos74 \
  --image OpenLogic:CentOS:7-CI:latest \
  --custom-data cloud_init_add_user.txt \
  --generate-ssh-keys 
```

Подключитесь по протоколу SSH к общедоступному IP-адресу виртуальной машины, который указан в выходных данных предыдущей команды. Введите свой общедоступный IP-адрес в качестве значения для **publicIpAddress**, как показано здесь:

```bash
ssh <publicIpAddress>
```

Чтобы проверить, добавлен ли пользователь и правильное ли указаны группы на виртуальной машине, просмотрите содержимое файла */etc/groups*, как показано ниже.

```bash
cat /etc/group
```

В следующем примере выходных данных демонстрируется, что пользователь из файла *cloud_init_add_user.txt* был успешно создан на виртуальной машине и добавлен в соответствующую группу.

```bash
root:x:0:
<snip />
sudo:x:27:myadminuser
<snip />
myadminuser:x:1000:
```

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные примеры изменения конфигураций с помощью cloud-init см. по следующим ссылкам:
 
- [Добавление пользователя Linux к виртуальной машине](cloudinit-add-user.md)
- [Запуск диспетчера пакетов для обновления существующих пакетов при первой загрузке](cloudinit-update-vm.md)
- [Изменение имени локального узла виртуальной машины](cloudinit-update-vm-hostname.md) 
- [Установка пакета приложения, обновление файлов конфигурации и внедрение ключей](tutorial-automate-vm-deployment.md)