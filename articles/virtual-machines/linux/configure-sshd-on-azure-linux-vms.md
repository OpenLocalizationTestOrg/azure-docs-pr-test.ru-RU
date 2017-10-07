---
title: "aaaConfigure SSHD виртуальных машин Linux в Azure | Документы Microsoft"
description: "Настройте SSHD рекомендации по обеспечению безопасности и tooAzure SSH toolockdown виртуальных машин Linux."
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
ms.date: 11/21/2016
ms.author: v-livech
ms.openlocfilehash: c2361be7199a24b129c06acfc899dd32f6e1d6fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sshd-on-azure-linux-vms"></a>Настройка SSHD на виртуальных машинах Azure Linux

В этой статье показано, как toolockdown hello SSH сервера в Linux, tooprovide советы и рекомендации безопасности, а также toospeed процесс входа hello SSH с использованием ключей SSH вместо паролей.  блокировки toofurther SSHD, мы будем toodisable hello привилегированного пользователя не может toologin максимальное разрешенное toologin через список утвержденных групп пользователей hello отключение протокол SSH версии 1, немного минимального ключа и настройте auto выхода неактивных пользователей.  Hello требования для этой статьи: учетная запись Azure ([получить бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/)) и [файлы SSH открытого и закрытого ключей](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-commands"></a>Быстрые команды

Настройка `/etc/ssh/sshd_config` с hello следующие параметры:

### <a name="disable-password-logins"></a>Отключение входа с использованием пароля

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-hello-root-user"></a>Отключить вход с hello привилегированного пользователя

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a>Список разрешенных групп

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a>Список разрешенных пользователей

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a>Отключение протокола SSH версии 1

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a>Минимальное число битов в ключе

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a>Отключение неактивных пользователей

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a>Подробное пошаговое руководство

SSHD — hello SSH сервера, работающего на виртуальной Машине Linux hello.  SSH — это клиент, который запускается из оболочки на рабочей станции MacBook или Linux, а также из Bash в Windows.  Также является SSH hello протокол используется toosecure и шифрования hello обмена данными между рабочей станцией и hello виртуальных Машин Linux, делая SSH также виртуальной частной сети (виртуальной частной сети).

В этой статье это очень важно tookeep одно имя входа tooyour ВМ Linux открыть руководство всей hello.  После установления SSH-подключения, он остается открытым сеанс до тех пор, пока не закрывается окно приветствия.  Наличие одного терминала вход, позволяет toohello toobe внесенные изменения SSHD службы без попытки блокируются при внесении критических изменений.  Если вы блокируются ВМ Linux с конфигурацией SSHD нарушена, Azure предлагает возможность tooreset hello неработающие SSHD конфигурации с hello [расширения Access ВМ Azure](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

По этой причине мы откройте два терминальных и SSH toohello виртуальной Машине Linux из них.  Мы используем hello первый терминалов toomake hello изменения tooSSHDs файла конфигурации и перезапустите службу hello SSHD.  Мы используем терминалов tootest с второй hello эти изменения, после перезапуска службы hello.  Так как мы выполняется отключение SSH пароли и полагаться исключительно на ключи SSH, если ключи SSH неверны и закрыть toohello hello подключения виртуальной Машины, hello виртуальной Машины будут окончательно заблокирован и никто будут tooit toologin может запрашивать ее toobe удалена и создана заново.

## <a name="disable-password-logins"></a>Отключение входа с использованием пароля

Здравствуйте, быстрый способ toosecure вы виртуальных Машин Linux — toodisable пароль входа.  При включении пароль входа программы-роботы обходе hello web немедленно начать попытка toobrute принудительно предположение hello пароль для ВМ Linux с помощью SSH.  Отключает имена входа пароль полностью, позволяет tooignore сервера SSH hello всех попыток входа пароль.

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-hello-root-user"></a>Отключить вход с hello привилегированного пользователя

Следующие рекомендации Linux hello `root` пользователя никогда не будут занесены в через SSH или с помощью `sudo su`.  Все команды, которым требуются разрешения на уровне корневого всегда должен выполняться через hello `sudo` команду, которая регистрирует все действия выполнять дальнейший аудит.  Отключение hello `root` лучшие методики шаг для обеспечения безопасности, гарантирует только авторизованным пользователям разрешено tooSSH является пользователь войти в систему по протоколу SSH.

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a>Список разрешенных групп

SSH предусматривает способ ограничить для пользователей и групп возможность входа с помощью SSH.  Эта функция использует списки tooapprove или запретить вход определенных пользователей и групп.  Параметр toohello группы колесо hello `AllowGroups` список ограничивает утвержденные имена входа по SSH toojust учетных записей, которые находятся в одной группе hello колесико мыши.

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a>Список разрешенных пользователей

Ограничение toojust учетные данные SSH пользователи является более особым образом tooaccomplish hello же задача, которая `AllowGroups` —.  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a>Отключение протокола SSH версии 1

Протокол SSH версии 1 является небезопасным и должен быть отключен.  Протокол SSH версии 2 — hello текущей версии, которая предлагает серверу tooyour tooSSH безопасным способом.  Отключение SSH версии 1 запрещает любые SSH клиенты, пытающиеся tooestablish соединение с сервером SSH hello, с помощью SSH версии 1.  Только для соединений по протоколу SSH версии 2 разрешены toonegotiate подключение к серверу SSH hello.

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a>Минимальное число битов в ключе

Следующие рекомендации по обеспечению безопасности пароль входа по протоколу SSH отключены и разрешены только ключи SSH toobe использовать tooauthenticate с сервера SSH hello.  Эти SSH-ключи могут быть разной длины (измеряется в битах).  Советы и рекомендации, ключи длиной 2048 бит стойкость ключа минимального допустимого hello состояний.  Ключи меньше 2048 бит теоретически могут быть повреждены.  Параметр hello `ServerKeyBits` слишком`2048` разрешены все соединения, с использованием ключей 2048 бит или больше и запретить подключения меньше 2048 бит.

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a>Отключение неактивных пользователей

SSH имеет hello возможность toodisconnect пользователей, имеющих открытые соединения, остаются простоя в течение определенного периода секунд.  Сохранение открытых сеансов tooonly тем пользователям, которые являются раскрытия hello active ограничения hello виртуальной Машины с Linux.

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a>Перезапуск SSHD

Параметры tooenable hello в `/etc/ssh/sshd_config` перезапуска процесса SSHD hello, который перезапускает сервер SSH hello.  использовать сервер SSH hello toorestart окно терминала Hello остаются открытыми без потери Привет открыть сеанс SSH.  параметры нового сервера SSH tootest hello используйте второе окно терминала или на отдельной вкладке.  С помощью отдельных терминалов tootest hello SSH-подключения можно toogo назад и внести дополнительные изменения toohello `/etc/ssh/sshd_config` в первый терминалов hello, без блокировки SSHD критических изменений.  

### <a name="on-redhat-centos-and-fedora"></a>В Redhat, Centos и Fedora

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a>В Debian и Ubuntu

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a>Сброс SSHD с помощью команды Azure reset-access

Если заблокированы из toohello SSHD критические изменения конфигурации можно использовать расширение доступа виртуальной Машины Azure hello tooreset hello SSHD конфигурации задней toohello исходной конфигурации.

Замените все имена в примере собственными.

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a>Установка Fail2ban

Настоятельно рекомендуется tooinstall и установки открытой приложение hello Fail2ban, какие блоки повторных попыток toologin tooyour ВМ Linux через SSH с помощью подбора.  Повторяющиеся журналы Fail2ban Сбой попытки toologin через SSH, а затем создает правила брандмауэра tooblock hello IP-адрес, инициированный попыток hello.

* [Домашняя страница Fail2ban](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы настроили и блокировки сервера SSH hello на ВМ Linux существуют дополнительные рекомендации по безопасности, необходимо выполнить.  

* [Управлять пользователями, SSH и проверку или восстановление дисков на виртуальных машинах Linux в Azure с помощью hello расширения VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [Шифрование дисков на виртуальной Машине Linux с помощью hello Azure CLI](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [Доступ и безопасность в шаблонах Azure Resource Manager](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
