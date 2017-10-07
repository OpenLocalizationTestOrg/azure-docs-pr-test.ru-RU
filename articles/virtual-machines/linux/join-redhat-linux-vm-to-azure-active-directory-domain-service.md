---
title: "aaaJoin tooan RedHat Linux VM Azure Active Directory доменных служб Active Directory | Документы Microsoft"
description: "Как toojoin существующие tooan RedHat Enterprise Linux 7 ВМ доменные службы Active Directory Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/14/2016
ms.author: v-livech
ms.openlocfilehash: f3ba3c764e253191753f1cc5fc8c3b85c53818af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-redhat-linux-vm-tooan-azure-active-directory-domain-service"></a>Присоединение виртуальной Машины с Linux RedHat tooan доменные службы Active Directory Azure

В этой статье показано, как toojoin tooan виртуальной машины Red Hat Enterprise Linux (RHEL) 7 Azure Active Directory домена службы (AADDS) Управление домена.  Существуют следующие требования Hello.

- [учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/);

- [файлы открытого и закрытого ключа SSH](mac-create-ssh-keys.md).

- [доменные службы Azure Active Directory](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-commands"></a>Быстрые команды

_Замените все примеры параметров своими значениями_.

### <a name="switch-hello-azure-cli-tooclassic-deployment-mode"></a>Переключение режима развертывания tooclassic hello azure cli

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a>Поиск версии и образа RHEL

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a>Создание виртуальной машины Red Hat Linux

```azurecli
azure vm create myVM \
-o a879bbefc56a43abb0ce65052aac09f3__RHEL_7_2_Standard_Azure_RHUI-20161026220742 \
-g ahmet \
-p myPassword \
-e 22 \
-t "~/.ssh/id_rsa.pub" \
-z "Small" \
-l "West US"
```

### <a name="ssh-toohello-vm"></a>Toohello SSH виртуальной Машины

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a>Обновление пакетов YUM

```bash
sudo yum update
```

### <a name="install-packages-needed"></a>Установка требуемых пакетов

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

Теперь, когда требуется hello пакеты устанавливаются на виртуальной машине Linux hello, следующая задача hello-toojoin hello виртуальной машины toohello управляемый домен.

### <a name="discover-hello-aad-domain-services-managed-domain"></a>Обнаружение управляемого домена доменных служб AAD hello

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a>Инициализация Kerberos

Убедитесь, что пользователь, принадлежащий группы администраторов контроллера домена, toohello «AAD». Только эти пользователи могут присоединен к домену управляемых компьютеров toohello.

```bash
kinit ahmet@mydomain.com
```

### <a name="join-hello-machine-toohello-domain"></a>Домену toohello машины hello

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-hello-machine-is-joined-toohello-domain"></a>Убедитесь, что hello машины присоединены к домену toohello домена

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a>Дальнейшие действия

* [Red Hat Update Infrastructure для предоставляемых по запросу виртуальных машин Red Hat Enterprise Linux в Azure](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Настройка хранилища ключей для виртуальных машин в Azure Resource Manager](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Развертывание и управление виртуальными машинами с помощью шаблонов диспетчера ресурсов Azure и hello Azure CLI](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
