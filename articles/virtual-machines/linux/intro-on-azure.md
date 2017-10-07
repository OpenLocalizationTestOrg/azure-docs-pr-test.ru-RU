---
title: "tooLinux aaaIntroduction в Azure | Документы Microsoft"
description: "Узнайте о том, как использовать виртуальные машины Linux в Azure."
services: virtual-machines-linux
documentationcenter: python
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: b13bf305-87bf-4df3-815e-e8f6337aa6ea
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: szark
ms.openlocfilehash: 3a931447ee23ce7000174ca314c3e10abc6b8e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toolinux-on-azure"></a>TooLinux введение в Azure
Здесь представлен обзор некоторые аспекты использования виртуальных машин Linux в hello облако Azure. Развертывание виртуальной машины Linux — простой процесс, с помощью образа из коллекции hello.

## <a name="authentication-usernames-passwords-and-ssh-keys"></a>Проверка подлинности: имена пользователей, пароли и ключи SSH
При создании виртуальной машины Linux при помощи hello портал Azure, будет предложено tooprovide либо имя пользователя и пароль, или открытый ключ SSH. Hello Выбор имени пользователя для развертывания виртуальной машины Linux в Azure является toohello субъекта следующие ограничения: имена системных учетных записей (UID < 100) уже присутствует в hello виртуальной машины не разрешены, «root». пример.

* Ознакомьтесь со статьей [Создание виртуальной машины с ОС Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* В разделе [как tooUse SSH с Linux в Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="obtaining-superuser-privileges-using-sudo"></a>Получение привилегий суперпользователя с помощью `sudo`
Hello учетная запись пользователя, который указывается в процессе развертывания экземпляр виртуальной машины в Azure является привилегированной учетной записи. Эта учетная запись настраивается с hello Azure Linux Agent toobe может tooelevate права tooroot (учетной записи суперпользователя) с помощью hello `sudo` программы. После входа с помощью этой учетной записи пользователя, как корень, используя синтаксис команды hello будет может toorun команды:

    # sudo <COMMAND>

При необходимости можно получить доступ к оболочке root с помощью команды **sudo -s**.

* Ознакомьтесь со статьей [Использование прав корневой учетной записи на виртуальных машинах Linux в Azure](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="firewall-configuration"></a>Настройка брандмауэра
Azure предоставляет фильтр входящего пакета, который ограничивает tooports подключения, указанные в hello портал Azure. По умолчанию, hello только разрешенные используется порт SSH. Можно открыть порты доступа tooadditional на виртуальной машине Linux путем настройки конечных точек в hello портала Azure:

* См.: [как tooa tooSet Настройка конечных точек виртуальной машины](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

образы Linux Hello в коллекции Azure hello не включайте hello *утилита iptables* брандмауэра по умолчанию. При желании можно настроить брандмауэр hello tooprovide дополнительная фильтрация.

## <a name="hostname-changes"></a>Изменения имени узла
При начальном развертывании экземпляра образа Linux, все необходимые tooprovide имя узла для виртуальной машины hello. Hello виртуальная машина запущена, это имя узла после опубликованных toohello платформы DNS-серверы, чтобы несколькими виртуальными машинами, подключенными tooeach другие могли выполнять поиск IP адрес, с использованием имен узлов.

При необходимости изменения имени узла после развертывания виртуальной машины, используйте команду hello

    # sudo hostname <newname>

Hello Azure Linux Agent включает функциональные возможности tooautomatically обнаружить изменение имени и соответствующим образом настроить виртуальную машину toopersist hello это изменение и повторно опубликовать это изменение toohello платформы DNS-серверы.

* [Руководство пользователя агента Linux для Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="cloud-init"></a>Cloud-Init
Образы **Ubuntu** и **CoreOS** используют пакет cloud-init в Azure, предоставляющий дополнительные возможности для начальной загрузки виртуальной машины.

* [Как tooInject пользовательские данные](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Пользовательские данные и cloud-init в Microsoft Azure](https://azure.microsoft.com/blog/2014/04/21/custom-data-and-cloud-init-on-windows-azure/)
* [Создание разделов подкачки Azure с помощью cloud-init](https://wiki.ubuntu.com/AzureSwapPartitions)
* [Как tooUse CoreOS в Azure](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="virtual-machine-image-capture"></a>Запись образа виртуальной машины
Azure предоставляет возможность hello toocapture состоянии hello существующей виртуальной машины в образ, который впоследствии можно использовать toodeploy дополнительные экземпляры виртуальной машины. Hello Azure Linux Agent может быть используется toorollback некоторые hello настройку, выполненную во время процесса инициализации hello. Как изображение может следовать за hello описанные ниже toocapture виртуальной машины:

1. Запустите **waagent-deprovision** tooundo подготовки настройки. Или **waagent-deprovision + пользователь** toooptionally удалить hello учетные записи пользователей во время подготовки и все связанные данные.
2. Завершение списка и отключить виртуальную машину hello.
3. Нажмите кнопку **записи** в hello Azure hello портала или используйте PowerShell или интерфейс командной строки средств toocapture hello виртуальной машины как изображение.
   
   * См.: [как tooCapture tooUse виртуальной машины Linux как шаблон](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="attaching-disks"></a>Присоединение дисков
Каждая виртуальная машина также имеет подключенный временный локальный *диск ресурсов* . Поскольку данные на диске ресурсов может быть устойчивыми перезагрузках, часто используется приложениями и процессы, запущенные на виртуальной машине hello для временной и **временные** хранения данных. Это также используется toostore hello страница или файлы подкачки для hello операционной системы.

В Linux, обычно управляется hello Azure Linux Agent и автоматическое подключение слишком диска ресурсов hello**/mnt/resource** (или **/mnt** Ubuntu изображений).

> [!NOTE]
> Обратите внимание, этот диск ресурсов hello **временные** на диске и может быть удаляются и переформатированы при hello перезагрузке ВМ.
> 
> 

Диск данных hello в Linux может называться ядре hello как `/dev/sdc`, и пользователи должны будут toopartition, форматирования и подключить этот ресурс. Это рассматривается в учебнике hello пошаговые: [как tooAttach tooa диска данных виртуальной машины](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

* **См. также**: [Настройка программного RAID-массива в Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) & [Настройка диспетчера логических томов на виртуальной машине Linux в Azure](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

