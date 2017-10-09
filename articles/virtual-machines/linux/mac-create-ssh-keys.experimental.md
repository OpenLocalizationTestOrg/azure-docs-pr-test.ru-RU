---
title: "пары ключей aaaCreate SSH для виртуальных машин Linux в Azure | Документы Microsoft"
description: "Безопасное создание пары из открытого и закрытого ключей SSH для виртуальных машин Linux в Linux."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: rasquill
ms.openlocfilehash: c4c7cec77c9b48295f2a28c8179b30a4dc38a555
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a>Создание пары из открытого и закрытого ключей SSH для виртуальных машин Linux

В этой статье показано, как toogenerate SSH протокол версии 2 открытый и закрытый ключ RSA файл toouse пары с виртуальных машин Linux.  С пару ключей SSH можно создавать виртуальные машины в Azure, то по умолчанию toousing ключей SSH для проверки подлинности, устраняя необходимость hello toolog пароли в.  Пароли можно подобрать и открыть виртуальные машины вверх tooguess попыток toorelentless подбора пароля. Виртуальные машины, созданные с помощью шаблонов Azure или hello `azure-cli` можно включить свой открытый ключ SSH как часть развертывания hello, удаление шаг настройки развертывания post отключения имена входа пароль для SSH.

## <a name="quick-commands"></a>Быстрые команды

Следующие команды в оболочке Bash, заменив собственный выбор hello примеры выполнения hello.

По умолчанию файл открытого ключа SSH создается в каталоге `~/.ssh/id_rsa.pub`. При появлении запроса, используя следующую команду hello, следует создать toosecure «парольную фразу» ваш закрытый ключ. (парольная фраза hello есть использовать tooencrypt пароль закрытого ключа.)

```bash
ssh-keygen -t rsa -b 2048 
```

Добавьте hello только что созданный раздел слишком`ssh-agent`:

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> Здравствуйте выше команды на операционные системы Linux, почти все распределения, но не всегда работают в контейнерах, как hello среды радикально могут быть ограничены. 

## <a name="detailed-walkthrough"></a>Подробное пошаговое руководство

Использование открытый и закрытый ключи SSH — toolog простым способом hello в tooyour серверы Linux. [Шифрование с открытым ключом](https://en.wikipedia.org/wiki/Public-key_cryptography) предоставляет гораздо более безопасный способ toolog в tooyour Linux или BSD виртуальную Машину в Azure чем пароль, который может быть принудительно применен гораздо проще.

> [!IMPORTANT]
> Открытый ключ можно предоставить любому пользователю, тогда как закрытый ключ принадлежит только вам (или локальной инфраструктуре безопасности).  должен иметь закрытый ключ SSH Hello [высокий уровень безопасности пароля](https://www.xkcd.com/936/) (источник:[xkcd.com](https://xkcd.com)) toosafeguard его.  Этот пароль должен быть закрытый ключ SSH просто tooaccess hello и **не** hello пароль учетной записи пользователя.  При добавлении пароль tooyour SSH-ключ, шифрует hello закрытый ключ с помощью 128-разрядный AES, чтобы hello закрытый ключ не имеет смысла без пароля toodecrypt hello его.  Если злоумышленник украсть ваш закрытый ключ и пароль не был ключ, они будут иметь доступ toouse, закрытый ключ toolog в tooany серверов, которые имеют hello соответствующего открытого ключа.  Если закрытый ключ защищен паролем, злоумышленник не сможет использовать его. Такой подход обеспечивает дополнительный уровень безопасности инфраструктуры в Azure.

В этой статье создает протокол SSH версии 2 RSA открытого и закрытого ключей файлы, которые рекомендуются для развертывания на hello диспетчера ресурсов.  *SSH-rsa* в hello необходимы ключи [портала](https://portal.azure.com) классический и развертывания диспетчера ресурсов.

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a>Отключение паролей SSH за счет использования ключей SSH

В Azure необходимо использовать по крайней 2048-разрядные открытые и закрытые ключи в формате ssh-rsa. Используйте ключи toocreate hello `ssh-keygen`, который задает ряд вопросов, а затем записывает закрытого ключа и соответствующего открытого ключа. При создании виртуальной Машины Azure открытый ключ hello копируется слишком`~/.ssh/authorized_keys`.  Ключи SSH в `~/.ssh/authorized_keys` , используемые toochallenge hello клиента toomatch hello соответствующий закрытый ключ для имени входа SSH-подключения.  При создании ВМ Linux Azure с помощью ключей SSH для проверки подлинности, Azure настраивает hello SSHD toonot сервера разрешить имен входа, пароль, только ключи SSH.  Таким образом путем создания виртуальных машин Linux в Azure с ключи SSH, можно помочь hello безопасного развертывания виртуальной Машины и сохранить самостоятельно шаг стандартной конфигурации после развертывания hello отключения пароли в файле конфигурации sshd_config hello.

## <a name="using-ssh-keygen"></a>Использование команды ssh-keygen

Эта команда создает пароль, защищенным (зашифрованное) пару ключей SSH, с помощью RSA 2048 бит и его закомментирована tooeasily идентифицировать его.  

SSH ключи, по умолчанию хранится в hello `~/.ssh` каталога.  Если у вас `~/.ssh` каталог, hello `ssh-keygen` команда создает его с hello правильные разрешения.

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

*Описание команды*

`ssh-keygen`= hello программа, используемая toocreate hello ключи

`-t rsa`Тип ключа toocreate, который имеет формат RSA hello = [](https://en.wikipedia.org/wiki/RSA_(cryptosystem) Википедии

`-b 2048`= bits hello ключа


## <a name="classic-portal-and-x509-certs"></a>Классический портал и сертификаты X.509

Если вы используете hello Azure [классический портал](https://manage.windowsazure.com/), это требует сертификаты X.509 для hello ключей SSH.  Другие типы открытых ключей SSH не используются. *Требуются* только сертификаты X.509.

toocreate сертификат X.509 с существующие закрытый ключ SSH-RSA:

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a>Классическое развертывание с помощью `asm`

Если используется классический hello развертывания модели (управления службами Azure CLI `asm`), можно использовать открытый ключ SSH-RSA или RFC4716 в формате ключа в **.pem** контейнера.  открытый ключ SSH-RSA Hello является то, что был создан ранее в этой статье с помощью `ssh-keygen`.

toocreate RFC4716 формат ключа из существующих открытый ключ SSH:

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a>Пример с ssh-keygen

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
hello keys randomart image is:
+--[ RSA 2048]----+
|        o o. .   |
|      E. = .o    |
|      ..o...     |
|     . o....     |
|      o S =      |
|     . + O       |
|      + = =      |
|       o +       |
|        .        |
+-----------------+
```

Сохраненные файлы ключей:

`Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

Имя Hello пару ключей для данной статьи.  Наличие пару ключей с именем **id_rsa** значения по умолчанию hello и ожидать, некоторые средства hello **id_rsa** имени файла закрытого ключа, имеющая одно имеет смысл. каталог Hello `~/.ssh/` hello расположение по умолчанию для пар ключей SSH и файл конфигурации SSH hello.  Если не указано с указанием полного пути `ssh-keygen` будет создавать ключи hello в текущем рабочем каталоге hello, не hello по умолчанию `~/.ssh`.

Перечень hello `~/.ssh` каталога.

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

Пароль ключа:

`Enter passphrase (empty for no passphrase):`

`ssh-keygen`закрытый ключ hello tooencrypt tooa пароль, используемый диск называется «парольную фразу.»  Это *строго* рекомендуется tooadd пары ключей tooyour парольную фразу. Без парольную фразу защищающее hello закрытого ключа имеющему hello файла ключа можно использовать toolog в tooany сервер, имеющий hello соответствующего открытого ключа. Добавление парольную фразу предлагает дополнительные защиты в случае, если кто-то — может toogain доступа tooyour файла закрытого ключа, что дает время toochange hello ключи, используемые tooauthenticate вы.

## <a name="using-ssh-agent-toostore-your-private-key-password"></a>С помощью ssh агента toostore пароль закрытого ключа

Введите ваш закрытый ключ tooavoid файл парольную фразу все имена входа SSH, можно использовать `ssh-agent` toocache пароль файла закрытого ключа. При использовании Mac OSX цепочки ключей hello надежно сохраняет пароли закрытых ключей hello при вызове `ssh-agent`.

Проверить и использовать `ssh-agent` и `ssh-add` tooinform hello SSH системы о hello ключевых файлов, чтобы hello парольная фраза не нужно использовать в интерактивном режиме toobe.

```bash
eval "$(ssh-agent -s)"
```

Теперь добавьте закрытый ключ hello слишком`ssh-agent` с помощью команды hello `ssh-add`.

```bash
ssh-add ~/.ssh/id_rsa
```

Hello пароль закрытого ключа сохраняется в `ssh-agent`.

## <a name="using-ssh-copy-id-tooinstall-hello-new-key"></a>С помощью `ssh-copy-id` tooinstall hello новый ключ
При создании виртуальной Машины можно установить hello новый SSH открытого ключа tooyour виртуальной Машины Linux при hello следующую команду, заменив имя пользователя виртуальной Машины hello и адрес сервера hello собственные значения.

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a>Создание и настройка файла конфигурации SSH

Он является наиболее toocreate рекомендаций и настроить `~/.ssh/config` toospeed файл вверх имена входа и оптимизации поведение клиента SSH.

Следующий пример Hello показывает стандартной конфигурации.

### <a name="create-hello-file"></a>Создайте файл hello

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a>Изменение hello файл tooadd hello новой конфигурации SSH:

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a>Пример файла `~/.ssh/config`:

```bash
# Azure Keys
Host fedora22
  Hostname 102.160.203.241
  User ahmet
# ./Azure Keys
# Default Settings
Host *
  PubkeyAuthentication=yes
  IdentitiesOnly=yes
  ServerAliveInterval=60
  ServerAliveCountMax=30
  ControlMaster auto
  ControlPath ~/.ssh/SSHConnections/ssh-%r@%h:%p
  ControlPersist 4h
  IdentityFile ~/.ssh/id_rsa
```

Это дает конфигурации SSH, вы разделы для каждого сервера tooenable каждого toohave свой собственный выделенный пару ключей. Здравствуйте, параметры по умолчанию (`Host *`) предназначены для тех узлах, которые не соответствует ни одному из hello конкретных узлов, чем в файле конфигурации hello.

### <a name="config-file-explained"></a>Описание файла конфигурации

`Host`= hello имя узла hello, вызываемый на hello терминалов.  `ssh fedora22`сообщает `SSH` toouse значения hello в блоке settings hello с меткой `Host fedora22` Примечание: для узла можно указать любую метку, для использования логического и не представляют Привет фактическое имя узла любого сервера.

`Hostname 102.160.203.241`= hello IP-адрес или DNS-имя сервера hello к которому выполняется доступ.

`User ahmet`= toouse учетную запись удаленного пользователя hello при входе toohello сервера.

`PubKeyAuthentication yes`= сообщает SSH требуется toouse toolog ключа SSH.

`IdentityFile /home/ahmet/.ssh/id_id_rsa`= hello SSH закрытого ключа и соответствующего открытого ключа toouse для проверки подлинности.

## <a name="ssh-into-linux-without-a-password"></a>Вход в Linux с использованием SSH без пароля

Теперь, когда у вас есть пару ключей SSH и настроенный файл конфигурации SSH, быстро и надежно являются может toolog в tooyour виртуальной Машины с Linux. Здравствуйте, во время первого входа в tooa сервера, с помощью SSH ключа hello командные строки можно для hello парольную фразу для этого файла ключа.

```bash
ssh fedora22
```

### <a name="command-explained"></a>Описание команды

Когда `ssh fedora22` выполнении SSH сначала находит и загружает все параметры из hello `Host fedora22` блока, а затем загружает все hello оставшиеся параметры из hello последний блок `Host *`.

## <a name="next-steps"></a>Дальнейшие действия

Далее вверх toocreate виртуальных машин Linux Azure использует hello новый SSH открытый ключ.  Виртуальные машины Azure, созданных с помощью открытого ключа SSH от имени для входа hello, лучше защищенным, чем виртуальные машины, созданные с помощью метода входа по умолчанию hello, пароли.  В настройках виртуальных машин Azure, созданных с помощью ключей SSH, пароли отключены по умолчанию для защиты от атак методом подбора. Если необходима дополнительная помощь при создании вашего пару ключей SSH или требуются дополнительные сертификаты, например, для использования с классического портала hello, см. раздел [подробные пар ключей SSH toocreate действия и сертификаты](create-ssh-keys-detailed.md).

* [Создание защищенной виртуальной машины Linux с помощью шаблона Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Создание безопасного ВМ Linux с помощью hello портал Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Создание безопасного ВМ Linux с помощью hello Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
