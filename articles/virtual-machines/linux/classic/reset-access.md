---
title: "aaaReset пароль виртуальной Машины Linux и SSH ключа из hello CLI | Документы Microsoft"
description: "Как исправить конфигурацию SSH hello hello toouse расширения VMAccess из tooreset hello Azure интерфейс командной строки (CLI) виртуальной Машины с Linux пароль или ключ SSH и проверка согласованности диска"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d975eb70-5ff1-40d1-a634-8dd2646dcd17
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: cynthn
ms.openlocfilehash: 1650ad64fb982627ae9f90b1a8209bb56bac7004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-a-linux-vm-password-or-ssh-key-fix-hello-ssh-configuration-and-check-disk-consistency-using-hello-vmaccess-extension"></a><span data-ttu-id="fd903-103">Как tooreset ВМ Linux пароля или ключа SSH, исправьте конфигурацию SSH hello и проверка целостности дисков, использование расширения VMAccess hello</span><span class="sxs-lookup"><span data-stu-id="fd903-103">How tooreset a Linux VM password or SSH key, fix hello SSH configuration, and check disk consistency using hello VMAccess extension</span></span>
<span data-ttu-id="fd903-104">Если tooa Linux виртуальной машины в Azure не удается подключиться из-за забытый пароль неверный ключ Secure Shell (SSH) и проблемы с конфигурацией SSH hello, hello расширение VMAccessForLinux hello Azure CLI tooreset hello пароля или ключа SSH, исправьте Здравствуйте конфигурации SSH и проверять согласованность диска.</span><span class="sxs-lookup"><span data-stu-id="fd903-104">If you can't connect tooa Linux virtual machine on Azure because of a forgotten password, an incorrect Secure Shell (SSH) key, or a problem with hello SSH configuration, use hello VMAccessForLinux extension with hello Azure CLI tooreset hello password or SSH key, fix hello SSH configuration, and check disk consistency.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="fd903-105">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fd903-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fd903-106">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="fd903-106">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="fd903-107">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fd903-107">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="fd903-108">Узнайте, каким образом слишком[выполните следующие действия с помощью диспетчера ресурсов модели hello](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="fd903-108">Learn how too[perform these steps using hello Resource Manager model](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span>

<span data-ttu-id="fd903-109">С hello Azure CLI, используйте hello **набор расширений ВМ azure** из команды tooaccess интерфейс командной строки (Bash, терминалов, Командная строка).</span><span class="sxs-lookup"><span data-stu-id="fd903-109">With hello Azure CLI, you use hello **azure vm extension set** command from your command-line interface (Bash, Terminal, Command prompt) tooaccess commands.</span></span> <span data-ttu-id="fd903-110">Выполните команду **azure help vm extension set** для получения подробных сведений об использовании расширения.</span><span class="sxs-lookup"><span data-stu-id="fd903-110">Run **azure help vm extension set** for detailed extension usage.</span></span>

<span data-ttu-id="fd903-111">Hello Azure CLI, позволяет выполнять hello следующие задания:</span><span class="sxs-lookup"><span data-stu-id="fd903-111">With hello Azure CLI, you can do hello following tasks:</span></span>

* [<span data-ttu-id="fd903-112">Сброс пароля hello</span><span class="sxs-lookup"><span data-stu-id="fd903-112">Reset hello password</span></span>](#pwresetcli)
* [<span data-ttu-id="fd903-113">Сбросить SSH-ключ hello</span><span class="sxs-lookup"><span data-stu-id="fd903-113">Reset hello SSH key</span></span>](#sshkeyresetcli)
* [<span data-ttu-id="fd903-114">Сброс hello hello и пароль ключа SSH</span><span class="sxs-lookup"><span data-stu-id="fd903-114">Reset hello password and hello SSH key</span></span>](#resetbothcli)
* [<span data-ttu-id="fd903-115">Создание новой учетной записи пользователя sudo</span><span class="sxs-lookup"><span data-stu-id="fd903-115">Create a new sudo user account</span></span>](#createnewsudocli)
* [<span data-ttu-id="fd903-116">Сброс конфигурации SSH hello</span><span class="sxs-lookup"><span data-stu-id="fd903-116">Reset hello SSH configuration</span></span>](#sshconfigresetcli)
* [<span data-ttu-id="fd903-117">Удаление пользователя</span><span class="sxs-lookup"><span data-stu-id="fd903-117">Delete a user</span></span>](#deletecli)
* [<span data-ttu-id="fd903-118">Отображение состояния hello hello расширение VMAccess</span><span class="sxs-lookup"><span data-stu-id="fd903-118">Display hello status of hello VMAccess extension</span></span>](#statuscli)
* [<span data-ttu-id="fd903-119">проверка согласованности добавленных дисков</span><span class="sxs-lookup"><span data-stu-id="fd903-119">Check consistency of added disks</span></span>](#checkdisk)
* [<span data-ttu-id="fd903-120">восстановление дисков, добавленных на виртуальной машине Linux.</span><span class="sxs-lookup"><span data-stu-id="fd903-120">Repair added disks on your Linux VM</span></span>](#repairdisk)

## <a name="prerequisites"></a><span data-ttu-id="fd903-121">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fd903-121">Prerequisites</span></span>
<span data-ttu-id="fd903-122">Вам потребуется toodo hello следующее:</span><span class="sxs-lookup"><span data-stu-id="fd903-122">You will need toodo hello following:</span></span>

* <span data-ttu-id="fd903-123">Необходимо будет слишком[установить hello Azure CLI](../../../cli-install-nodejs.md) и [подключения подписки tooyour](../../../xplat-cli-connect.md) toouse Azure ресурсы, связанные с вашей учетной записью.</span><span class="sxs-lookup"><span data-stu-id="fd903-123">You will need too[install hello Azure CLI](../../../cli-install-nodejs.md) and [connect tooyour subscription](../../../xplat-cli-connect.md) toouse Azure resources associated with your account.</span></span>
* <span data-ttu-id="fd903-124">Настроить hello правильный режим для hello классической модели развертывания, введя следующее hello hello командной строки:</span><span class="sxs-lookup"><span data-stu-id="fd903-124">Set hello correct mode for hello classic deployment model by typing hello following at hello command prompt:</span></span>
    ``` 
        azure config mode asm
    ```
* <span data-ttu-id="fd903-125">Наличие новый пароль или набора ключей SSH tooreset любой из них.</span><span class="sxs-lookup"><span data-stu-id="fd903-125">Have a new password or set of SSH keys, if you want tooreset either one.</span></span> <span data-ttu-id="fd903-126">Если требуется, чтобы конфигурации SSH hello tooreset эти не требуется.</span><span class="sxs-lookup"><span data-stu-id="fd903-126">You don't need these if you want tooreset hello SSH configuration.</span></span>

## <span data-ttu-id="fd903-127"><a name="pwresetcli"></a>Сброс пароля hello</span><span class="sxs-lookup"><span data-stu-id="fd903-127"><a name="pwresetcli"></a>Reset hello password</span></span>
1. <span data-ttu-id="fd903-128">Создайте на локальном компьютере файл с именем PrivateConf.json с такими строками.</span><span class="sxs-lookup"><span data-stu-id="fd903-128">Create a file on your local computer named PrivateConf.json with these lines.</span></span> <span data-ttu-id="fd903-129">Замените строку **myUserName** и **myP@ssW0rd** своим именем пользователя и паролем и установите собственную дату окончания срока действия.</span><span class="sxs-lookup"><span data-stu-id="fd903-129">Replace **myUserName** and **myP@ssW0rd** with your own user name and password and set your own date for expiration.</span></span>

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. <span data-ttu-id="fd903-130">Запустите следующую команду, заменив имя виртуальной машины для hello **myVM**.</span><span class="sxs-lookup"><span data-stu-id="fd903-130">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <span data-ttu-id="fd903-131"><a name="sshkeyresetcli"></a>Сбросить SSH-ключ hello</span><span class="sxs-lookup"><span data-stu-id="fd903-131"><a name="sshkeyresetcli"></a>Reset hello SSH key</span></span>
1. <span data-ttu-id="fd903-132">Создайте файл с именем PrivateConf.json с таким содержимым.</span><span class="sxs-lookup"><span data-stu-id="fd903-132">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="fd903-133">Замените hello **myUserName** и **mySSHKey** значения с помощью своих собственных сведений.</span><span class="sxs-lookup"><span data-stu-id="fd903-133">Replace hello **myUserName** and **mySSHKey** values with your own information.</span></span>

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. <span data-ttu-id="fd903-134">Запустите следующую команду, заменив имя виртуальной машины для hello **myVM**.</span><span class="sxs-lookup"><span data-stu-id="fd903-134">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <span data-ttu-id="fd903-135"><a name="resetbothcli"></a>Сброс пароля hello и SSH-ключ hello</span><span class="sxs-lookup"><span data-stu-id="fd903-135"><a name="resetbothcli"></a>Reset both hello password and hello SSH key</span></span>
1. <span data-ttu-id="fd903-136">Создайте файл с именем PrivateConf.json с таким содержимым.</span><span class="sxs-lookup"><span data-stu-id="fd903-136">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="fd903-137">Замените hello **myUserName**, **mySSHKey** и  **myP@ssW0rd**  значения с помощью своих собственных сведений.</span><span class="sxs-lookup"><span data-stu-id="fd903-137">Replace hello **myUserName**, **mySSHKey** and **myP@ssW0rd** values with your own information.</span></span>

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. <span data-ttu-id="fd903-138">Запустите следующую команду, заменив имя виртуальной машины для hello **myVM**.</span><span class="sxs-lookup"><span data-stu-id="fd903-138">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="fd903-139"><a name="createnewsudocli"></a>Создание новой учетной записи пользователя sudo</span><span class="sxs-lookup"><span data-stu-id="fd903-139"><a name="createnewsudocli"></a>Create a new sudo user account</span></span>

<span data-ttu-id="fd903-140">Если вы забыли имя пользователя, VMAccess toocreate можно использовать новый с центром sudo hello.</span><span class="sxs-lookup"><span data-stu-id="fd903-140">If you forget your user name, you can use VMAccess toocreate a new one with hello sudo authority.</span></span> <span data-ttu-id="fd903-141">В этом случае hello существующее имя пользователя и пароль не будет изменен.</span><span class="sxs-lookup"><span data-stu-id="fd903-141">In this case, hello existing user name and password will not be modified.</span></span>

<span data-ttu-id="fd903-142">Новый пользователь sudo с пароль доступа, используйте сценарий hello в toocreate [hello сброс пароля](#pwresetcli) и укажите новое имя пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="fd903-142">toocreate a new sudo user with password access, use hello script in [Reset hello password](#pwresetcli) and specify hello new user name.</span></span>

<span data-ttu-id="fd903-143">toocreate нового пользователя sudo с доступ к ключу SSH, использовать сценарий hello в [сброса hello SSH-ключ](#sshkeyresetcli) и укажите новое имя пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="fd903-143">toocreate a new sudo user with SSH key access, use hello script in [Reset hello SSH key](#sshkeyresetcli) and specify hello new user name.</span></span>

<span data-ttu-id="fd903-144">Можно также использовать [сбросить пароль hello и SSH-ключ hello](#resetbothcli) toocreate нового пользователя, пароль и доступ к ключу SSH.</span><span class="sxs-lookup"><span data-stu-id="fd903-144">You can also use [Reset hello password and hello SSH key](#resetbothcli) toocreate a new user with both password and SSH key access.</span></span>

## <span data-ttu-id="fd903-145"><a name="sshconfigresetcli"></a>Сброс конфигурации SSH hello</span><span class="sxs-lookup"><span data-stu-id="fd903-145"><a name="sshconfigresetcli"></a>Reset hello SSH configuration</span></span>
<span data-ttu-id="fd903-146">Если нежелательных изменений конфигурации SSH hello, также может потерять доступ toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="fd903-146">If hello SSH configuration is in an undesired state, you might also lose access toohello VM.</span></span> <span data-ttu-id="fd903-147">Можно использовать hello VMAccess расширения tooreset hello конфигурации tooits состояние по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="fd903-147">You can use hello VMAccess extension tooreset hello configuration tooits default state.</span></span> <span data-ttu-id="fd903-148">toodo таким образом, необходимо просто ключ «reset_ssh» hello tooset слишком «True».</span><span class="sxs-lookup"><span data-stu-id="fd903-148">toodo so, you just need tooset hello “reset_ssh” key too“True”.</span></span> <span data-ttu-id="fd903-149">расширение Hello перезапуск сервера SSH hello, откройте порт SSH hello на ВМ и сбросить значения toodefault конфигурации SSH hello.</span><span class="sxs-lookup"><span data-stu-id="fd903-149">hello extension will restart hello SSH server, open hello SSH port on your VM, and reset hello SSH configuration toodefault values.</span></span> <span data-ttu-id="fd903-150">Hello учетной записи пользователя (имя, пароль или ключи SSH) не будут изменены.</span><span class="sxs-lookup"><span data-stu-id="fd903-150">hello user account (name, password or SSH keys) will not be changed.</span></span>

> [!NOTE]
> <span data-ttu-id="fd903-151">файл конфигурации SSH Hello, сбрасывается находится в /etc/ssh/sshd_config.</span><span class="sxs-lookup"><span data-stu-id="fd903-151">hello SSH configuration file that gets reset is located at /etc/ssh/sshd_config.</span></span>
> 
> 

1. <span data-ttu-id="fd903-152">Создайте файл с именем PrivateConf.json с таким содержимым.</span><span class="sxs-lookup"><span data-stu-id="fd903-152">Create a file named PrivateConf.json with this content.</span></span>

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. <span data-ttu-id="fd903-153">Запустите следующую команду, заменив имя виртуальной машины для hello **myVM**.</span><span class="sxs-lookup"><span data-stu-id="fd903-153">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="fd903-154"><a name="deletecli"></a>Удаление пользователя</span><span class="sxs-lookup"><span data-stu-id="fd903-154"><a name="deletecli"></a>Delete a user</span></span>
<span data-ttu-id="fd903-155">Следует toodelete учетной записи пользователя без непосредственного выхода toohello виртуальной Машины можно использовать этот сценарий.</span><span class="sxs-lookup"><span data-stu-id="fd903-155">If you want toodelete a user account without logging into toohello VM directly, you can use this script.</span></span>

1. <span data-ttu-id="fd903-156">Создайте файл с именем PrivateConf.json с этого содержимого, заменив hello tooremove имя пользователя для **removeUserName**.</span><span class="sxs-lookup"><span data-stu-id="fd903-156">Create a file named PrivateConf.json with this content, substituting hello user name tooremove for **removeUserName**.</span></span> 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. <span data-ttu-id="fd903-157">Запустите следующую команду, заменив имя виртуальной машины для hello **myVM**.</span><span class="sxs-lookup"><span data-stu-id="fd903-157">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="fd903-158"><a name="statuscli"></a>Отображение состояния hello hello расширение VMAccess</span><span class="sxs-lookup"><span data-stu-id="fd903-158"><a name="statuscli"></a>Display hello status of hello VMAccess extension</span></span>
<span data-ttu-id="fd903-159">состояние hello toodisplay hello расширения VMAccess, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="fd903-159">toodisplay hello status of hello VMAccess extension, run this command.</span></span>

```
        azure vm extension get
```

## <span data-ttu-id="fd903-160"><a name='checkdisk'></a>Проверка согласованности добавленных дисков</span><span class="sxs-lookup"><span data-stu-id="fd903-160"><a name='checkdisk'></a>Check consistency of added disks</span></span>
<span data-ttu-id="fd903-161">toorun fsck на всех дисках, на виртуальной машине Linux, нужно будет toodo hello следующее:</span><span class="sxs-lookup"><span data-stu-id="fd903-161">toorun fsck on all disks in your Linux virtual machine, you will need toodo hello following:</span></span>

1. <span data-ttu-id="fd903-162">Создайте файл с именем PublicConf.json с таким содержимым.</span><span class="sxs-lookup"><span data-stu-id="fd903-162">Create a file named PublicConf.json with this content.</span></span> <span data-ttu-id="fd903-163">Проверка диска прикреплено ли диски toocheck tooyour виртуальной машины или не принимает логическое значение.</span><span class="sxs-lookup"><span data-stu-id="fd903-163">Check Disk takes a boolean for whether toocheck disks attached tooyour virtual machine or not.</span></span> 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. <span data-ttu-id="fd903-164">Запустите этот tooexecute команду, подставив имя hello виртуальной машины для **myVM**.</span><span class="sxs-lookup"><span data-stu-id="fd903-164">Run this command tooexecute, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <span data-ttu-id="fd903-165"><a name='repairdisk'></a>Восстановление дисков</span><span class="sxs-lookup"><span data-stu-id="fd903-165"><a name='repairdisk'></a>Repair disks</span></span>
<span data-ttu-id="fd903-166">toorepair диски, которые не подключаются или с ошибками конфигурации подключения, использующие hello VMAccess расширения tooreset hello подключения на виртуальной машине Linux.</span><span class="sxs-lookup"><span data-stu-id="fd903-166">toorepair disks that are not mounting or have mount configuration errors, use hello VMAccess extension tooreset hello mount configuration on your Linux virtual machine.</span></span> <span data-ttu-id="fd903-167">Вставку hello имя диска для **myDisk**.</span><span class="sxs-lookup"><span data-stu-id="fd903-167">Substituting hello name of your disk for **myDisk**.</span></span>

1. <span data-ttu-id="fd903-168">Создайте файл с именем PublicConf.json с таким содержимым.</span><span class="sxs-lookup"><span data-stu-id="fd903-168">Create a file named PublicConf.json with this content.</span></span> 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. <span data-ttu-id="fd903-169">Запустите этот tooexecute команду, подставив имя hello виртуальной машины для **myVM**.</span><span class="sxs-lookup"><span data-stu-id="fd903-169">Run this command tooexecute, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a><span data-ttu-id="fd903-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fd903-170">Next steps</span></span>
* <span data-ttu-id="fd903-171">Если требуется toouse командлетов Azure PowerShell или диспетчера ресурсов Azure шаблоны tooreset hello пароля или ключа SSH, исправьте конфигурацию SSH hello и проверять согласованность диска см. в разделе hello [документации расширения VMAccess на GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="fd903-171">If you want toouse Azure PowerShell cmdlets or Azure Resource Manager templates tooreset hello password or SSH key, fix hello SSH configuration, and check disk consistency, see hello [VMAccess extension documentation on GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span> 
* <span data-ttu-id="fd903-172">Можно также использовать hello [портал Azure](https://portal.azure.com) tooreset hello пароля или ключа SSH для виртуальной Машины Linux развернутых в hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="fd903-172">You can also use hello [Azure portal](https://portal.azure.com) tooreset hello password or SSH key of a Linux VM deployed in hello classic deployment model.</span></span> <span data-ttu-id="fd903-173">Вы нельзя использовать в настоящее время toothis портала выполните hello для развертывания виртуальной Машины Linux в модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="fd903-173">You can't currently use hello portal do toothis for a Linux VM deployed in hello Resource Manager deployment model.</span></span>
* <span data-ttu-id="fd903-174">В статье [Обзор расширений и компонентов виртуальной машины](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) приводятся дополнительные сведения об использовании расширений для виртуальных машин Azure.</span><span class="sxs-lookup"><span data-stu-id="fd903-174">See [About virtual machine extensions and features](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more about using VM extensions for Azure virtual machines.</span></span>

