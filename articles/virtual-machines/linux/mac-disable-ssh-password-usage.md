---
title: "Отключение паролей SSH в виртуальной машине Linux в настройках SSHD | Документация Майкрософт"
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
ms.openlocfilehash: dc45a1cdce29cef061acc5c7e5b15d9d89265cd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a>Отключение паролей SSH в виртуальной машине Linux в настройках SSHD
В этой статье рассматривается отключение защиты входа в систему в виртуальной машине Linux.  Если открыть SSH-порт номер 22, программы-роботы сразу же будут пытаться войти в систему путем подбора паролей.  В этой статье мы отключим вход в систему с паролем по протоколу SSH.  За счет полного отключения возможности использовать пароли мы защитим виртуальную машину Linux от атак методом подбора.  Дополнительное преимущество состоит в том, что в настройках SSHD Linux вход в систему будет разрешен только с использованием открытых и закрытых ключей SSH, что является наиболее безопасным способом входа в ОС Linux.  Число возможных комбинаций при поиске закрытого ключа методом подбора настолько велико, что программы-роботы даже не пытаются использовать этот метод для взлома SSH-ключей.

## <a name="goals"></a>Цели
* Настройте SSHD, чтобы запретить:
  * Вход с использованием пароля
  * Вход привилегированного пользователя
  * Проверку подлинности через запрос и ответ
* Настройте SSHD, чтобы разрешить:
  * Вход только с использованием SSH-ключей
* Перезапустите SSHD, не выходя из системы
* Протестируйте новую конфигурацию SSHD

## <a name="introduction"></a>Введение
[Определение SSH](https://en.wikipedia.org/wiki/Secure_Shell)

SSHD — это SSH-сервер, работающий на виртуальной машине Linux.  SSH — это клиент, который запускается из оболочки на рабочей станции MacBook или Linux.  SSH — это также протокол, используемый для защиты и шифрования обмена данными между рабочей станцией и виртуальной машиной Linux.

Для этой статьи очень важно держать открытым один сеанс работы с виртуальной машиной Linux в течение прохождения всего пошагового руководства.  По этой причине мы откроем два терминала и установим подключение SSH к виртуальной машине Linux из каждого из них.  Первый терминал будет использоваться для изменений файла конфигурации SSHD и перезапуска службы SSHD.  Второй терминал будет использоваться для тестирования этих изменений после перезапуска службы.  Поскольку мы отключаем SSH-пароли и полагаемся исключительно на SSH-ключи, если ваши SSH-ключи неверны и вы закроете подключение к виртуальной машине, эта виртуальная машины окажется безвозвратно заблокированной. Никто не сможет войти в нее, поэтому ее придется удалить и создать заново.

## <a name="prerequisites"></a>Предварительные требования
* [Создание ключей SSH для виртуальных машин Linux в ОС Linux и Mac в Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Учетная запись Azure
  * [Бесплатная пробная версия подписки](https://azure.microsoft.com/pricing/free-trial/)
  * [Портал Azure](http://portal.azure.com)
* Виртуальная машина Linux в Azure
* Открытый и закрытый SSH-ключ в `~/.ssh/`
* Открытый SSH-ключ в `~/.ssh/authorized_keys` на виртуальной машине Linux
* Права sudo в виртуальной машине
* Открытый порт 22

## <a name="quick-commands"></a>Быстрые команды
*Опытные администраторы Linux, которым требуется только версия TLDR, начинают здесь.  Всем остальным, кому нужно подробное описание и пошаговое руководство, следует пропустить этот раздел.*

```bash
sudo vim /etc/ssh/sshd_config
```

Измените файл конфигурации следующим образом:

```sh
# Change PasswordAuthentication to this:
PasswordAuthentication no

# Change PubkeyAuthentication to this:
PubkeyAuthentication yes

# Change PermitRootLogin to this:
PermitRootLogin no

# Change ChallengeResponseAuthentication to this:
ChallengeResponseAuthentication no
```

Перезапустите службу SSHD. На основе дистрибутивов Debian:

```bash
sudo service ssh restart
```

На основе дистрибутивов Red Hat:

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a>Подробные пошаговые инструкции
Выполните вход в виртуальную машину Linux с терминала 1 (T1).  Выполните вход в виртуальную машину Linux с терминала 2 (T2).

На T2 мы собираемся изменить файл конфигурации SSHD.  

```bash
sudo vim /etc/ssh/sshd_config
```

Здесь мы изменим только те параметры, которые отключат пароли и включат вход в систему с использованием SSH-ключей.  В этом файле множество параметров, которые необходимо изучить и изменить, чтобы организовать безопасность Linux и SSH на необходимом вам уровне.

#### <a name="disable-password-logins"></a>Отключение входа с использованием пароля

```sh
# Change PasswordAuthentication to this:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a>Включение проверки подлинности с использованием открытого ключа

```sh
# Change PubkeyAuthentication to this:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a>Отключение корневого входа

```sh
# Change PermitRootLogin to this:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a>Отключение проверки подлинности через запрос и ответ
```sh
# Change ChallengeResponseAuthentication to this:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a>Перезапуск SSHD
С терминала T1 убедитесь, что вы все еще находитесь в системе.  Это важно, чтобы не потерять доступ к виртуальной машине, если SSH-ключи окажутся неправильными, поскольку пароли будут отключены.  Если какие-либо параметры виртуальной машины Linux окажутся неправильными, можно будет воспользоваться терминалом T1, чтобы исправить sshd_config, поскольку у вас сохраняется вход в систему и SSH будет поддерживать соединение во время перезапуска службы SSHD.

С терминала T2 выполните:

##### <a name="on-the-debian-family"></a>В семействе Debian
```bash
sudo service ssh restart
```

##### <a name="on-the-redhat-family"></a>В семействе RedHat
```bash
sudo service sshd restart
```

Теперь пароли на виртуальной машине отключены, что защищает ее от попыток входа методом подбора пароля.  Благодаря тому, что разрешены только SSH-ключи, вы сможете выполнять вход быстрее и гораздо безопаснее.

