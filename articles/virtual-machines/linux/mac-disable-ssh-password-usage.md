---
title: "пароли aaaDisable SSH для ВМ Linux, настроив SSHD | Документы Microsoft"
description: "Защита виртуальной машины Linux в Azure посредством отключения входа с использованием пароля для SSH."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 46137640-a7d2-40e5-a1e9-9effef7eb190
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/26/2016
ms.author: v-livech
ms.openlocfilehash: fb67b2f5b8b3bf2ba214858940b04f2ea9013fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a>Отключение паролей SSH в виртуальной машине Linux в настройках SSHD
В этой статье основное внимание уделено toolock вниз hello безопасности входа в систему виртуальной машины Linux.  По мере открытия hello SSH-порт 22 программы-роботы world toohello запустите попытки toologin путем подбора паролей.  В этой статье мы отключим вход в систему с паролем по протоколу SSH.  Удалив hello возможность полностью toouse пароли защищен hello виртуальной Машине Linux из этого типа атаки методом принудительно атаки.  Hello добавлены премия — Linux SSHD tooonly позволяют настроить имена входа через открытый и закрытый ключи SSH, пока hello tooLinux toologin наиболее безопасным способом.  Hello возможных сочетаний, его потребуется закрытый ключ hello tooguess весьма велик и таким образом не рекомендует программы-роботы из даже беспокоить ключи SSH tootry toobrute force.

## <a name="goals"></a>Цели
* Настройте SSHD toodisallow.
  * Вход с использованием пароля
  * Вход привилегированного пользователя
  * Проверку подлинности через запрос и ответ
* Настройте SSHD tooallow.
  * Вход только с использованием SSH-ключей
* Перезапустите SSHD, не выходя из системы
* Новая конфигурация SSHD теста hello

## <a name="introduction"></a>Введение
[Определение SSH](https://en.wikipedia.org/wiki/Secure_Shell)

SSHD — hello SSH сервера, работающего на виртуальной Машине Linux hello.  SSH — это клиент, который запускается из оболочки на рабочей станции MacBook или Linux.  SSH также является протокол hello используется toosecure и шифрования hello обмена данными между рабочей станцией и hello виртуальной Машины с Linux.

В этой статье это очень важно tookeep перемещайтесь открыт для hello всей виртуальной Машины Linux один tooyour входа.  По этой причине их откроется два терминалы и SSH toohello виртуальной Машины с Linux.  Мы будет использовать hello первый терминалов toomake hello изменения tooSSHDs файл конфигурации и перезапустите службу SSHD hello.  Мы будем использовать терминалов tootest с второй hello эти изменения, после перезапуска службы hello.  Так как мы выполняется отключение SSH пароли и полагаться исключительно на ключи SSH, если ключи SSH неверны и закрыть toohello hello подключения виртуальной Машины, hello виртуальной Машины будут окончательно заблокирован и никто будут tooit toologin может запрашивать ее toobe удалена и создана заново.

## <a name="prerequisites"></a>Предварительные требования
* [Создание ключей SSH для виртуальных машин Linux в ОС Linux и Mac в Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Учетная запись Azure
  * [Бесплатная пробная версия подписки](https://azure.microsoft.com/pricing/free-trial/)
  * [Портал Azure](http://portal.azure.com)
* Виртуальная машина Linux в Azure
* Открытый и закрытый SSH-ключ в `~/.ssh/`
* Открытый ключ SSH в `~/.ssh/authorized_keys` на виртуальной Машине Linux hello
* Прав sudo на hello виртуальной Машины
* Открытый порт 22

## <a name="quick-commands"></a>Быстрые команды
*Начните здесь наемных Linux администраторов, желающих только версии TLDR hello.  Для всех остальных случаях, если оно hello подробное описание и пошагового пропустите этот раздел.*

```bash
sudo vim /etc/ssh/sshd_config
```

Измените файл конфигурации hello следующим образом:

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no

# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes

# Change PermitRootLogin toothis:
PermitRootLogin no

# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

Перезапустите службу SSHD hello. На основе дистрибутивов Debian:

```bash
sudo service ssh restart
```

На основе дистрибутивов Red Hat:

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a>Подробные пошаговые инструкции
Toohello входа в систему виртуальной Машины с Linux на сервере терминалов 1 (T1).  Toohello входа в систему виртуальной Машины с Linux для терминалов 2 (T2).

Файл конфигурации SSHD hello tooedit мы будем в таблицу T2.  

```bash
sudo vim /etc/ssh/sshd_config
```

Здесь мы изменить только пароли toodisable параметры hello и включить учетные записи ключа SSH.  Существует множество параметров в этот файл следует изучить и Смена toomake Linux SSH, как безопасные, сколько требуется.

#### <a name="disable-password-logins"></a>Отключение входа с использованием пароля

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a>Включение проверки подлинности с использованием открытого ключа

```sh
# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a>Отключение корневого входа

```sh
# Change PermitRootLogin toothis:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a>Отключение проверки подлинности через запрос и ответ
```sh
# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a>Перезапуск SSHD
Убедитесь, что по-прежнему вы вошли из оболочки hello T1.  Это важно, чтобы не потерять доступ к виртуальной машине, если SSH-ключи окажутся неправильными, поскольку пароли будут отключены.  Если ни один параметр неверны на вашей виртуальной Машине Linux, можно использовать T1 toofix sshd_config, а вы по-прежнему заносятся SSH будет активности hello подключения во время hello SSHD service перезапустите.

С терминала T2 выполните:

##### <a name="on-hello-debian-family"></a>В Debian семейства hello
```bash
sudo service ssh restart
```

##### <a name="on-hello-redhat-family"></a>На семейство RedHat hello
```bash
sudo service sshd restart
```

Теперь пароли на виртуальной машине отключены, что защищает ее от попыток входа методом подбора пароля.  Только SSH ключи допускается будет toologin может быстрее и безопаснее.

