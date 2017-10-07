---
title: "aaaAdd tooa пользователя виртуальной Машины с Linux в Azure | Документы Microsoft"
description: "Добавьте пользователя tooa виртуальных Машин Linux в Azure."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8aa633b-8b75-45d7-b61d-11ac112cedd5
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/18/2016
ms.author: v-livech
ms.openlocfilehash: eed050154adf0cbed2c168e7aa675bd3ded85fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-user-tooan-azure-vm"></a>Добавить пользователя tooan ВМ Azure
Одним из первых задач hello на все новые виртуальные Машины Linux является toocreate нового пользователя.  В этой статье мы рассматривается создание учетной записи пользователя прав sudo, установка пароля hello, добавление SSH открытых ключей и наконец используйте `visudo` tooallow sudo без пароля.

Необходимые условия: [учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/), [открытый и закрытый ключи SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), группы ресурсов Azure и Azure CLI hello установлен и переключается на использование режима диспетчера ресурсов tooAzure `azure config mode arm`.

## <a name="quick-commands"></a>Быстрые команды
```bash
# Add a new user on RedHat family distros
sudo useradd -G wheel exampleUser

# Add a new user on Debian family distros
sudo useradd -G sudo exampleUser

# Set a password
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully

# Copy hello SSH Public Key toohello new user
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver

# Change sudoers tooallow no password
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL

# Verify everything
# Verify hello SSH keys & User account
bill@slackware$ ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```

## <a name="detailed-walkthrough"></a>Подробное пошаговое руководство
### <a name="introduction"></a>Введение
Одним из hello первой и наиболее распространенные задачи с нового сервера является tooadd учетной записи пользователя.  Корневой имен входа должны быть отключены и учетной записи root hello сам не следует использовать с сервером Linux только sudo.  Предоставление полномочий с использованием sudo с ней hello tooadminister правильным способом, а Linux укрупнения корневого пользователя.

С помощью команды hello `useradd` мы добавляем toohello учетных записей пользователя виртуальной Машины с Linux.  Выполнение `useradd` изменяет `/etc/passwd`, `/etc/shadow`, `/etc/group` и `/etc/gshadow`.  Мы добавляем toohello командной строки флаг `useradd` команда tooalso добавить новую группу в правильную sudo пользователей toohello hello в Linux.  Даже можно `useradd` создает запись в `/etc/passwd` он не дает hello новой учетной записи пользователя пароль.  Мы создаем начального пароля для hello нового пользователя с помощью простого hello `passwd` команды.  Последний шаг Hello — toomodify hello sudo правил tooallow команды tooexecute этого пользователя с правами sudo без необходимости tooenter пароль для каждой команды.  Вход с использованием закрытого ключа hello, предполагается, что учетная запись пользователя от недобросовестных сторон и будет доступ sudo tooallow без пароля.  

### <a name="adding-a-single-sudo-user-tooan-azure-vm"></a>Добавление tooan пользователя sudo одной виртуальной Машине Azure
Войдите в систему toohello ВМ Azure с помощью ключей SSH.  Если доступ по открытому ключу SSH не настроен, сначала выполните инструкции в статье [Использование проверки подлинности по открытому ключу с помощью Azure](http://link.to/article).  

Hello `useradd` выполнения команды hello следующие задачи:

* создание учетной записи пользователя;
* создать новую группу пользователей с hello таким же именем
* Добавьте пустую запись слишком`/etc/passwd`
* Добавьте пустую запись слишком`/etc/gpasswd`

Hello `-G` командной строки флаг добавляет hello новой учетной записи toohello правильную Linux группы пользователей предоставление прав укрупнения корневой hello новой учетной записи пользователя.

#### <a name="add-hello-user"></a>Добавить пользователя hello
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a>Задание пароля
Hello `useradd` команда создает пользователя hello и добавляет запись tooboth `/etc/passwd` и `/etc/gpasswd` , но фактически не задан пароль hello.  Hello пароль добавляется toohello входа с помощью hello `passwd` команды.

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

Теперь у нас есть пользователь с правами sudo на сервере hello.

### <a name="add-your-ssh-public-key-toohello-new-user-account"></a>Добавить открытый ключ SSH toohello новой учетной записи пользователя
С компьютера, используйте hello `ssh-copy-id` с hello новый пароль.

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-tooallow-sudo-usage-without-a-password"></a>С помощью использования sudo tooallow visudo без пароля
С помощью `visudo` tooedit hello `/etc/sudoers` файл добавляет несколько уровней защиты от неправильного изменения важный файл.  При выполнении `visudo`, hello `/etc/sudoers` файл является заблокированным tooensure другой пользователь не может внести изменения, пока активно редактируется.  Hello `/etc/sudoers` файла также проверяется наличие ошибок, `visudo` при попытку toosave или завершить работу, поэтому не удается сохранить файл неработающие sudoers.

Пользователи уже имеется в группе по умолчанию hello для доступа к sudo.  Теперь мы будем tooenable sudo toouse этих групп без пароля.

```bash
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL
```

### <a name="verify-hello-user-ssh-keys-and-sudo"></a>Проверка пользователя hello ssh ключей и sudo
```bash
# Verify hello SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
