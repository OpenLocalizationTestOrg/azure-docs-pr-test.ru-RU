---
title: "aaaSelecting имена пользователей для Linux | Документы Microsoft"
description: "Узнайте, как имена tooselect пользователя для виртуальной машины Linux в Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 33b50c97-92f1-46c9-a623-e37f67459c5c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: c65e2ac46f40bb8c9d74cccbaf248a070c0fa6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a>Выбор имен пользователей для Linux в Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

При подготовке виртуальной машины Linux в Azure необходимо указать имя hello непривилегированного пользователя, что toolog можно использовать позже в hello виртуальной Машины. Можно выбрать имя нового пользователя hello hello, или если Подготовка с помощью классического портала Azure "hello" может принимать по умолчанию hello имя «azureuser».

В большинстве случаев этот пользователь не должен существовать на базовый образ hello и создается во время процесса инициализации hello. Если hello пользователя существует на hello базового образа виртуальной Машины, а затем просто настраивает агент Azure Linux hello hello пароль или ключ SSH для этого пользователя, основанный на сведениях hello, указанный при создании виртуальной Машины hello.

**Тем не менее**Linux определяет набор имен пользователей, которые нельзя использовать. Hello подготовки процесса будет **ошибкой** при попытке tooprovision ВМ Linux с помощью существующего пользователя системы, которая определяется как пользователь с UID 0 до 99. Типичным примером является hello `root` пользователя, который имеет идентификатор 0.

* См. также: [База стандартов Linux. Диапазоны идентификаторов пользователей](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html).

Hello ниже приведен список общих встроенных системных пользователей для CentOS и Ubuntu, что не следует использовать при подготовке виртуальной машины Linux в Azure. Этот список является лишь пример, см. документацию toohello вашей tooensure распространения username hello выбранного не конфликтует с существующего пользователя системы.

## <a name="centos"></a>CentOS
* abrt
* adm
* audio
* bin
* cdrom
* cgred
* daemon
* dbus
* dialout
* dip
* disk
* floppy
* ftp
* ftp
* games
* gopher
* haldaemon
* halt
* kmem
* lock
* lp
* mail
* man
* mem
* nfsnobody
* nobody
* ntp
* operator
* oprofile
* postdrop
* postfix
* qpidd
* root
* rpc
* rpcuser
* saslauth
* shutdown
* slocate
* sshd
* stapdev
* stapusr
* sync
* sys
* tape
* test
* tcpdump
* tty
* users
* utempter
* utmp
* uucp
* vcsa
* video
* wheel

## <a name="ubuntu"></a>Ubuntu
* adm
* admin
* audio
* backup
* bin
* cdrom
* crontab
* daemon
* dialout
* dip
* disk
* fax
* floppy
* fuse
* games
* gnats
* irc
* kmem
* landscape
* libuuid
* list
* lp
* mail
* man
* messagebus
* mlocate
* netdev
* news
* nobody
* nogroup
* operator
* plugdev
* proxy
* root
* sasl
* shadow
* src
* ssh
* sshd
* staff
* sudo
* sync
* sys
* syslog
* tape
* tty
* users
* utmp
* uucp
* video
* voice
* whoopsie
* www-data

