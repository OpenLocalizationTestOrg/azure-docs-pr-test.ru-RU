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
# <a name="how-tooreset-a-linux-vm-password-or-ssh-key-fix-hello-ssh-configuration-and-check-disk-consistency-using-hello-vmaccess-extension"></a>Как tooreset ВМ Linux пароля или ключа SSH, исправьте конфигурацию SSH hello и проверка целостности дисков, использование расширения VMAccess hello
Если tooa Linux виртуальной машины в Azure не удается подключиться из-за забытый пароль неверный ключ Secure Shell (SSH) и проблемы с конфигурацией SSH hello, hello расширение VMAccessForLinux hello Azure CLI tooreset hello пароля или ключа SSH, исправьте Здравствуйте конфигурации SSH и проверять согласованность диска. 

> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Узнайте, каким образом слишком[выполните следующие действия с помощью диспетчера ресурсов модели hello](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).

С hello Azure CLI, используйте hello **набор расширений ВМ azure** из команды tooaccess интерфейс командной строки (Bash, терминалов, Командная строка). Выполните команду **azure help vm extension set** для получения подробных сведений об использовании расширения.

Hello Azure CLI, позволяет выполнять hello следующие задания:

* [Сброс пароля hello](#pwresetcli)
* [Сбросить SSH-ключ hello](#sshkeyresetcli)
* [Сброс hello hello и пароль ключа SSH](#resetbothcli)
* [Создание новой учетной записи пользователя sudo](#createnewsudocli)
* [Сброс конфигурации SSH hello](#sshconfigresetcli)
* [Удаление пользователя](#deletecli)
* [Отображение состояния hello hello расширение VMAccess](#statuscli)
* [проверка согласованности добавленных дисков](#checkdisk)
* [восстановление дисков, добавленных на виртуальной машине Linux.](#repairdisk)

## <a name="prerequisites"></a>Предварительные требования
Вам потребуется toodo hello следующее:

* Необходимо будет слишком[установить hello Azure CLI](../../../cli-install-nodejs.md) и [подключения подписки tooyour](../../../xplat-cli-connect.md) toouse Azure ресурсы, связанные с вашей учетной записью.
* Настроить hello правильный режим для hello классической модели развертывания, введя следующее hello hello командной строки:
    ``` 
        azure config mode asm
    ```
* Наличие новый пароль или набора ключей SSH tooreset любой из них. Если требуется, чтобы конфигурации SSH hello tooreset эти не требуется.

## <a name="pwresetcli"></a>Сброс пароля hello
1. Создайте на локальном компьютере файл с именем PrivateConf.json с такими строками. Замените строку **myUserName** и **myP@ssW0rd** своим именем пользователя и паролем и установите собственную дату окончания срока действия.

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. Запустите следующую команду, заменив имя виртуальной машины для hello **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <a name="sshkeyresetcli"></a>Сбросить SSH-ключ hello
1. Создайте файл с именем PrivateConf.json с таким содержимым. Замените hello **myUserName** и **mySSHKey** значения с помощью своих собственных сведений.

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. Запустите следующую команду, заменив имя виртуальной машины для hello **myVM**.
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <a name="resetbothcli"></a>Сброс пароля hello и SSH-ключ hello
1. Создайте файл с именем PrivateConf.json с таким содержимым. Замените hello **myUserName**, **mySSHKey** и  **myP@ssW0rd**  значения с помощью своих собственных сведений.

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. Запустите следующую команду, заменив имя виртуальной машины для hello **myVM**.

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="createnewsudocli"></a>Создание новой учетной записи пользователя sudo

Если вы забыли имя пользователя, VMAccess toocreate можно использовать новый с центром sudo hello. В этом случае hello существующее имя пользователя и пароль не будет изменен.

Новый пользователь sudo с пароль доступа, используйте сценарий hello в toocreate [hello сброс пароля](#pwresetcli) и укажите новое имя пользователя hello.

toocreate нового пользователя sudo с доступ к ключу SSH, использовать сценарий hello в [сброса hello SSH-ключ](#sshkeyresetcli) и укажите новое имя пользователя hello.

Можно также использовать [сбросить пароль hello и SSH-ключ hello](#resetbothcli) toocreate нового пользователя, пароль и доступ к ключу SSH.

## <a name="sshconfigresetcli"></a>Сброс конфигурации SSH hello
Если нежелательных изменений конфигурации SSH hello, также может потерять доступ toohello виртуальной Машины. Можно использовать hello VMAccess расширения tooreset hello конфигурации tooits состояние по умолчанию. toodo таким образом, необходимо просто ключ «reset_ssh» hello tooset слишком «True». расширение Hello перезапуск сервера SSH hello, откройте порт SSH hello на ВМ и сбросить значения toodefault конфигурации SSH hello. Hello учетной записи пользователя (имя, пароль или ключи SSH) не будут изменены.

> [!NOTE]
> файл конфигурации SSH Hello, сбрасывается находится в /etc/ssh/sshd_config.
> 
> 

1. Создайте файл с именем PrivateConf.json с таким содержимым.

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. Запустите следующую команду, заменив имя виртуальной машины для hello **myVM**. 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="deletecli"></a>Удаление пользователя
Следует toodelete учетной записи пользователя без непосредственного выхода toohello виртуальной Машины можно использовать этот сценарий.

1. Создайте файл с именем PrivateConf.json с этого содержимого, заменив hello tooremove имя пользователя для **removeUserName**. 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. Запустите следующую команду, заменив имя виртуальной машины для hello **myVM**. 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="statuscli"></a>Отображение состояния hello hello расширение VMAccess
состояние hello toodisplay hello расширения VMAccess, выполните следующую команду.

```
        azure vm extension get
```

## <a name='checkdisk'></a>Проверка согласованности добавленных дисков
toorun fsck на всех дисках, на виртуальной машине Linux, нужно будет toodo hello следующее:

1. Создайте файл с именем PublicConf.json с таким содержимым. Проверка диска прикреплено ли диски toocheck tooyour виртуальной машины или не принимает логическое значение. 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. Запустите этот tooexecute команду, подставив имя hello виртуальной машины для **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <a name='repairdisk'></a>Восстановление дисков
toorepair диски, которые не подключаются или с ошибками конфигурации подключения, использующие hello VMAccess расширения tooreset hello подключения на виртуальной машине Linux. Вставку hello имя диска для **myDisk**.

1. Создайте файл с именем PublicConf.json с таким содержимым. 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. Запустите этот tooexecute команду, подставив имя hello виртуальной машины для **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a>Дальнейшие действия
* Если требуется toouse командлетов Azure PowerShell или диспетчера ресурсов Azure шаблоны tooreset hello пароля или ключа SSH, исправьте конфигурацию SSH hello и проверять согласованность диска см. в разделе hello [документации расширения VMAccess на GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess). 
* Можно также использовать hello [портал Azure](https://portal.azure.com) tooreset hello пароля или ключа SSH для виртуальной Машины Linux развернутых в hello классической модели развертывания. Вы нельзя использовать в настоящее время toothis портала выполните hello для развертывания виртуальной Машины Linux в модели развертывания диспетчера ресурсов hello.
* В статье [Обзор расширений и компонентов виртуальной машины](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) приводятся дополнительные сведения об использовании расширений для виртуальных машин Azure.

