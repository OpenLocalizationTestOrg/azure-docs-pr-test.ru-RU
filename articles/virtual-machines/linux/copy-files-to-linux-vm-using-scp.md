---
title: "aaaMove файлы tooand из виртуальных машин Linux Azure с SCP | Документы Microsoft"
description: "Безопасно перемещать файлы tooand из виртуальной Машины Linux в Azure с использованием точки подключения службы и пару ключей SSH."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 9e4dce667aa581df74aec3d45a6ba5e52f777d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-files-tooand-from-a-linux-vm-using-scp"></a>Перемещение файлов tooand с ВМ Linux с помощью точки подключения службы

В этой статье показано, как toomove файлы из рабочей станции вверх tooan виртуальной Машине Linux Azure или виртуальной Машине Linux Azure работы tooyour рабочей станции, с использованием безопасного копирования (SCP). Быстрое и безопасное перемещение файлов между рабочей станцией и виртуальной машиной с Linux является важной частью управления инфраструктурой Azure. 

Для этой статьи необходима виртуальная машина Linux, развернутая в Azure с помощью [файлов открытого и закрытого ключей SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Кроме того, нужен клиент SCP для локального компьютера. При разработке на основе SSH и включены в оболочке Bash по умолчанию hello большинство компьютеров Linux и Mac и некоторые оболочки Windows.

## <a name="quick-commands"></a>Быстрые команды

Скопируйте файл вверх toohello ВМ Linux

```bash
scp file azureuser@azurehost:directory/targetfile
```

Скопируйте файл вниз с hello ВМ Linux

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a>Подробное пошаговое руководство

В качестве примеров, мы переместить в файл конфигурации Azure вверх tooa виртуальной Машины Linux и открыть его в каталог файла журнала, как с помощью клавиш SCP и SSH.   

## <a name="ssh-key-pair-authentication"></a>Аутентификация с помощью пары ключей SSH

Точка подключения службы использует SSH для hello транспортного уровня. SSH дескрипторы hello проверки подлинности на конечном узле hello и он перемещает файл hello в зашифрованный канал SSH в состав по умолчанию. Для аутентификации SSH можно использовать имена пользователей и пароли. Тем не менее по соображениям безопасности рекомендуется использовать аутентификацию с открытым и закрытым ключами SSH. После SSH прошел проверку соединения hello, SCP затем начинает копирование файла hello. С помощью правильно настроенного `~/.ssh/config` и открытые и закрытые ключи SSH, hello SCP соединение может быть установлено с использованием только имя сервера (или IP-адрес). Если имеется только один ключ SSH, SCP ищет его в hello `~/.ssh/` каталога и использует его по умолчанию toolog в toohello виртуальной Машины.

Дополнительные сведения о настройке файла `~/.ssh/config`, а также открытом и закрытом ключах SSH см. в статье [Как создать и использовать пару из открытого и закрытого ключей SSH для виртуальных машин Linux в Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="scp-a-file-tooa-linux-vm"></a>Точка подключения службы tooa файл виртуальной Машины с Linux

Первый пример hello мы скопировать файл конфигурации Azure вверх tooa виртуальной Машины Linux, которое используется toodeploy автоматизации. Так как этот файл содержит учетные данные API Azure, в том числе секреты, важно обеспечить его безопасность. Hello зашифрованные туннель SSH, предоставляемые защищает hello содержимое файла hello.

Здравствуйте, следующие команды копий hello локальной *.azure/config* файл tooan ВМ Azure с полным доменным ИМЕНЕМ *myserver.eastus.cloudapp.azure.com*. — имя пользователя администратора hello на виртуальной Машине Azure hello *azureuser* . Hello файл является целевой toohello */home/azureuser/* каталога. Подставьте собственные значения в эту команду.

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a>Копирование каталога с виртуальной машины Linux с помощью SCP

В этом примере мы копируем каталог файлов журнала из hello ВМ Linux работы tooyour рабочей станции. Файл журнала может содержать или не содержать секретные данные. Тем не менее с помощью SCP гарантирует, что зашифрованные hello содержимое файлов журналов hello. С помощью файлов hello tootransfer SCP является наиболее простым способом tooget hello Здравствуйте, при этом безопасный каталог журнала и файлы работы tooyour рабочей станции.

Hello следующая команда копирует файлы в hello */home/azureuser/журналы/* каталог в каталоге/tmp локального toohello виртуальной Машины Azure hello:

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

Hello `-r` cli флаг указывает, что точка подключения службы toorecursively копирования hello файлы и каталоги из точки hello hello каталог, который указан в команде hello.  Также Обратите внимание, что hello синтаксис командной строки — примерно tooa `cp` скопируйте команду.

## <a name="next-steps"></a>Дальнейшие действия

* [Управлять пользователями, SSH и проверку или восстановление дисков на виртуальных машинах Linux в Azure с помощью hello расширения VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
