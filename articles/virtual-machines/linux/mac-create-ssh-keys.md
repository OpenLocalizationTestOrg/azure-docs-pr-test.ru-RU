---
title: "aaaCreate и использование SSH пары ключей для виртуальных машин Linux в Azure | Документы Microsoft"
description: "Как toocreate и использования открытого и закрытого пару ключей SSH для виртуальных машин Linux в Azure tooimprove hello безопасности hello процесса проверки подлинности."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: iainfou
ms.openlocfilehash: 7fb94841d34d5bc006f3134adf91102ddce5f174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a>Как связать toocreate и использования открытого и закрытого ключа SSH для виртуальных машин Linux в Azure
С помощью пары ключей безопасного shell (SSH) можно создать в Azure, использовать ключи SSH для проверки подлинности, устраняя необходимость hello toolog пароли в виртуальные машины (VM). В этой статье показано, как создать и использовать пару открытого и закрытого ключа файл RSA версии 2 протокола SSH для виртуальных машин Linux tooquickly. Более подробные инструкции и Дополнительные примеры см. в разделе [подробные пар ключей SSH toocreate действия и сертификаты](create-ssh-keys-detailed.md).

## <a name="create-an-ssh-key-pair"></a>Создание пары ключей SSH
Используйте hello `ssh-keygen` команды toocreate SSH файлы открытого и закрытого ключа, по умолчанию, созданные в hello `~/.ssh` каталога, но можно указать другое расположение и дополнительных парольную фразу (пароль tooaccess hello файл закрытого ключа) при запрос. Запустите следующую команду в оболочке Bash hello, ответы на hello приглашения с своих собственных сведений.

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-hello-ssh-key-pair"></a>Используйте пару ключей SSH hello
Hello открытый ключ, который поместить на ВМ Linux в Azure, по умолчанию сохраняется в `~/.ssh/id_rsa.pub`, если не изменено расположение hello при их создании. При использовании hello [Azure CLI 2.0](/cli/azure) toocreate ВМ, укажите расположение hello этот открытый ключ, при использовании hello [создания виртуальной машины az](/cli/azure/vm#create) с hello `--ssh-key-path` параметр. Если скопируйте и вставьте содержимое файла открытого ключа toouse hello hello в hello портал Azure или шаблона диспетчера ресурсов, убедитесь, что не копировать все дополнительные пробелы. Например, если вы используете OS X, можно передать hello файла открытого ключа (по умолчанию **~/.ssh/id_rsa.pub**) слишком**pbcopy** toocopy hello содержимого (используется в других программ Linux, которые hello одинаково, например `xclip`).

Если вы не работали с открытым ключом SSH, чтобы просмотреть его, выполните команду `cat`, заменив параметр `~/.ssh/id_rsa.pub` расположением файла собственного открытого ключа.

```bash
cat ~/.ssh/id_rsa.pub
```

Hello открытым ключом на ВМ Azure, SSH tooyour виртуальной Машины с помощью hello IP-адрес или DNS-имя виртуальной Машины (Помните tooreplace `azureuser` и `myvm.westus.cloudapp.azure.com` ниже используя hello пользователя с правами администратора и hello полное имя домена — или IP-адрес):

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

При указании парольную фразу при создании вашего пары ключей, введите парольную фразу hello при появлении запроса во время процесса входа в систему hello. (сервер hello добавляется tooyour `~/.ssh/known_hosts` папки и не будет запрашиваться tooconnect пока hello открытого ключа на виртуальной Машине Azure изменения или имя сервера hello удаляется из `~/.ssh/known_hosts`.)

## <a name="next-steps"></a>Дальнейшие действия

Виртуальные машины, созданные с помощью ключей SSH, по умолчанию настраивается с помощью паролей отключено, принудительно атаки методом подбора toomake пытается значительно дороже, а следовательно и сложной. В этой статье описано создание простой пары ключей SSH для быстрого использования. Если необходима дополнительная помощь при создании вашего пару ключей SSH или требуются дополнительные сертификаты, см. раздел [подробные пар ключей SSH toocreate действия и сертификаты](create-ssh-keys-detailed.md).

Можно создать виртуальные машины, использующие вашей пару ключей SSH с помощью портала Azure hello, CLI и шаблонов.

* [Создание безопасного ВМ Linux с помощью hello портал Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Создание безопасного ВМ Linux с помощью hello Azure CLI 2.0)](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Создание защищенной виртуальной машины Linux с помощью шаблона Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
