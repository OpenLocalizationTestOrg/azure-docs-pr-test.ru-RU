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
# <a name="add-a-user-tooan-azure-vm"></a><span data-ttu-id="a4c70-103">Добавить пользователя tooan ВМ Azure</span><span class="sxs-lookup"><span data-stu-id="a4c70-103">Add a user tooan Azure VM</span></span>
<span data-ttu-id="a4c70-104">Одним из первых задач hello на все новые виртуальные Машины Linux является toocreate нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="a4c70-104">One of hello first tasks on any new Linux VM is toocreate a new user.</span></span>  <span data-ttu-id="a4c70-105">В этой статье мы рассматривается создание учетной записи пользователя прав sudo, установка пароля hello, добавление SSH открытых ключей и наконец используйте `visudo` tooallow sudo без пароля.</span><span class="sxs-lookup"><span data-stu-id="a4c70-105">In this article, we walk through creating a sudo user account, setting hello password, adding SSH Public Keys, and finally use `visudo` tooallow sudo without a password.</span></span>

<span data-ttu-id="a4c70-106">Необходимые условия: [учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/), [открытый и закрытый ключи SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), группы ресурсов Azure и Azure CLI hello установлен и переключается на использование режима диспетчера ресурсов tooAzure `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="a4c70-106">Prerequisites are: [an Azure account](https://azure.microsoft.com/pricing/free-trial/), [SSH public and private keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), an Azure resource group, and hello Azure CLI installed and switched tooAzure Resource Manager mode using `azure config mode arm`.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="a4c70-107">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="a4c70-107">Quick Commands</span></span>
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

## <a name="detailed-walkthrough"></a><span data-ttu-id="a4c70-108">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="a4c70-108">Detailed Walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="a4c70-109">Введение</span><span class="sxs-lookup"><span data-stu-id="a4c70-109">Introduction</span></span>
<span data-ttu-id="a4c70-110">Одним из hello первой и наиболее распространенные задачи с нового сервера является tooadd учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="a4c70-110">One of hello first and most common task with a new server is tooadd a user account.</span></span>  <span data-ttu-id="a4c70-111">Корневой имен входа должны быть отключены и учетной записи root hello сам не следует использовать с сервером Linux только sudo.</span><span class="sxs-lookup"><span data-stu-id="a4c70-111">Root logins should be disabled and hello root account itself should not be used with your Linux server, only sudo.</span></span>  <span data-ttu-id="a4c70-112">Предоставление полномочий с использованием sudo с ней hello tooadminister правильным способом, а Linux укрупнения корневого пользователя.</span><span class="sxs-lookup"><span data-stu-id="a4c70-112">Giving a user root escalation privileges using sudo it hello proper way tooadminister and use Linux.</span></span>

<span data-ttu-id="a4c70-113">С помощью команды hello `useradd` мы добавляем toohello учетных записей пользователя виртуальной Машины с Linux.</span><span class="sxs-lookup"><span data-stu-id="a4c70-113">Using hello command `useradd` we are adding user accounts toohello Linux VM.</span></span>  <span data-ttu-id="a4c70-114">Выполнение `useradd` изменяет `/etc/passwd`, `/etc/shadow`, `/etc/group` и `/etc/gshadow`.</span><span class="sxs-lookup"><span data-stu-id="a4c70-114">Running `useradd` modifies `/etc/passwd`, `/etc/shadow`, `/etc/group`, and `/etc/gshadow`.</span></span>  <span data-ttu-id="a4c70-115">Мы добавляем toohello командной строки флаг `useradd` команда tooalso добавить новую группу в правильную sudo пользователей toohello hello в Linux.</span><span class="sxs-lookup"><span data-stu-id="a4c70-115">We are adding a command-line flag toohello `useradd` command tooalso add hello new user toohello proper sudo group on Linux.</span></span>  <span data-ttu-id="a4c70-116">Даже можно `useradd` создает запись в `/etc/passwd` он не дает hello новой учетной записи пользователя пароль.</span><span class="sxs-lookup"><span data-stu-id="a4c70-116">Even thou `useradd` creates an entry into `/etc/passwd` it does not give hello new user account a password.</span></span>  <span data-ttu-id="a4c70-117">Мы создаем начального пароля для hello нового пользователя с помощью простого hello `passwd` команды.</span><span class="sxs-lookup"><span data-stu-id="a4c70-117">We are creating an initial password for hello new user using hello simple `passwd` command.</span></span>  <span data-ttu-id="a4c70-118">Последний шаг Hello — toomodify hello sudo правил tooallow команды tooexecute этого пользователя с правами sudo без необходимости tooenter пароль для каждой команды.</span><span class="sxs-lookup"><span data-stu-id="a4c70-118">hello last step is toomodify hello sudo rules tooallow that user tooexecute commands with sudo privileges without having tooenter a password for every command.</span></span>  <span data-ttu-id="a4c70-119">Вход с использованием закрытого ключа hello, предполагается, что учетная запись пользователя от недобросовестных сторон и будет доступ sudo tooallow без пароля.</span><span class="sxs-lookup"><span data-stu-id="a4c70-119">Logging in using hello Private key we are assuming that user account is safe from bad actors and are going tooallow sudo access without a password.</span></span>  

### <a name="adding-a-single-sudo-user-tooan-azure-vm"></a><span data-ttu-id="a4c70-120">Добавление tooan пользователя sudo одной виртуальной Машине Azure</span><span class="sxs-lookup"><span data-stu-id="a4c70-120">Adding a single sudo user tooan Azure VM</span></span>
<span data-ttu-id="a4c70-121">Войдите в систему toohello ВМ Azure с помощью ключей SSH.</span><span class="sxs-lookup"><span data-stu-id="a4c70-121">Log in toohello Azure VM using SSH keys.</span></span>  <span data-ttu-id="a4c70-122">Если доступ по открытому ключу SSH не настроен, сначала выполните инструкции в статье [Использование проверки подлинности по открытому ключу с помощью Azure](http://link.to/article).</span><span class="sxs-lookup"><span data-stu-id="a4c70-122">If you have not setup SSH public key access, complete this article first [Using Public Key Authentication with Azure](http://link.to/article).</span></span>  

<span data-ttu-id="a4c70-123">Hello `useradd` выполнения команды hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="a4c70-123">hello `useradd` command completes hello following tasks:</span></span>

* <span data-ttu-id="a4c70-124">создание учетной записи пользователя;</span><span class="sxs-lookup"><span data-stu-id="a4c70-124">create a new user account</span></span>
* <span data-ttu-id="a4c70-125">создать новую группу пользователей с hello таким же именем</span><span class="sxs-lookup"><span data-stu-id="a4c70-125">create a new user group with hello same name</span></span>
* <span data-ttu-id="a4c70-126">Добавьте пустую запись слишком`/etc/passwd`</span><span class="sxs-lookup"><span data-stu-id="a4c70-126">add a blank entry too`/etc/passwd`</span></span>
* <span data-ttu-id="a4c70-127">Добавьте пустую запись слишком`/etc/gpasswd`</span><span class="sxs-lookup"><span data-stu-id="a4c70-127">add a blank entry too`/etc/gpasswd`</span></span>

<span data-ttu-id="a4c70-128">Hello `-G` командной строки флаг добавляет hello новой учетной записи toohello правильную Linux группы пользователей предоставление прав укрупнения корневой hello новой учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="a4c70-128">hello `-G` command-line flag adds hello new user account toohello proper Linux group giving hello new user account root escalation privileges.</span></span>

#### <a name="add-hello-user"></a><span data-ttu-id="a4c70-129">Добавить пользователя hello</span><span class="sxs-lookup"><span data-stu-id="a4c70-129">Add hello user</span></span>
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a><span data-ttu-id="a4c70-130">Задание пароля</span><span class="sxs-lookup"><span data-stu-id="a4c70-130">Set a password</span></span>
<span data-ttu-id="a4c70-131">Hello `useradd` команда создает пользователя hello и добавляет запись tooboth `/etc/passwd` и `/etc/gpasswd` , но фактически не задан пароль hello.</span><span class="sxs-lookup"><span data-stu-id="a4c70-131">hello `useradd` command creates hello user and adds an entry tooboth `/etc/passwd` and `/etc/gpasswd` but does not actually set hello password.</span></span>  <span data-ttu-id="a4c70-132">Hello пароль добавляется toohello входа с помощью hello `passwd` команды.</span><span class="sxs-lookup"><span data-stu-id="a4c70-132">hello password is added toohello entry using hello `passwd` command.</span></span>

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

<span data-ttu-id="a4c70-133">Теперь у нас есть пользователь с правами sudo на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="a4c70-133">We now have a user with sudo privileges on hello server.</span></span>

### <a name="add-your-ssh-public-key-toohello-new-user-account"></a><span data-ttu-id="a4c70-134">Добавить открытый ключ SSH toohello новой учетной записи пользователя</span><span class="sxs-lookup"><span data-stu-id="a4c70-134">Add your SSH Public Key toohello new user account</span></span>
<span data-ttu-id="a4c70-135">С компьютера, используйте hello `ssh-copy-id` с hello новый пароль.</span><span class="sxs-lookup"><span data-stu-id="a4c70-135">From your machine, use hello `ssh-copy-id` command with hello new password.</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-tooallow-sudo-usage-without-a-password"></a><span data-ttu-id="a4c70-136">С помощью использования sudo tooallow visudo без пароля</span><span class="sxs-lookup"><span data-stu-id="a4c70-136">Using visudo tooallow sudo usage without a password</span></span>
<span data-ttu-id="a4c70-137">С помощью `visudo` tooedit hello `/etc/sudoers` файл добавляет несколько уровней защиты от неправильного изменения важный файл.</span><span class="sxs-lookup"><span data-stu-id="a4c70-137">Using `visudo` tooedit hello `/etc/sudoers` file adds a few layers of protection against incorrectly modifying this important file.</span></span>  <span data-ttu-id="a4c70-138">При выполнении `visudo`, hello `/etc/sudoers` файл является заблокированным tooensure другой пользователь не может внести изменения, пока активно редактируется.</span><span class="sxs-lookup"><span data-stu-id="a4c70-138">Upon executing `visudo`, hello `/etc/sudoers` file is locked tooensure no other user can make changes while it is actively being edited.</span></span>  <span data-ttu-id="a4c70-139">Hello `/etc/sudoers` файла также проверяется наличие ошибок, `visudo` при попытку toosave или завершить работу, поэтому не удается сохранить файл неработающие sudoers.</span><span class="sxs-lookup"><span data-stu-id="a4c70-139">hello `/etc/sudoers` file is also checked for mistakes by `visudo` when you attempt toosave or exit so you cannot save a broken sudoers file.</span></span>

<span data-ttu-id="a4c70-140">Пользователи уже имеется в группе по умолчанию hello для доступа к sudo.</span><span class="sxs-lookup"><span data-stu-id="a4c70-140">We already have users in hello correct default group for sudo access.</span></span>  <span data-ttu-id="a4c70-141">Теперь мы будем tooenable sudo toouse этих групп без пароля.</span><span class="sxs-lookup"><span data-stu-id="a4c70-141">Now we are going tooenable those groups toouse sudo with no password.</span></span>

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

### <a name="verify-hello-user-ssh-keys-and-sudo"></a><span data-ttu-id="a4c70-142">Проверка пользователя hello ssh ключей и sudo</span><span class="sxs-lookup"><span data-stu-id="a4c70-142">Verify hello user, ssh keys, and sudo</span></span>
```bash
# Verify hello SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
