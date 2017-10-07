---
title: "пароль tooreset локального aaaHow Linux на виртуальных машинах Azure | Документы Microsoft"
description: "Вводит hello действия tooreset hello локальный Linux пароль на виртуальной Машине Azure"
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: delhan
ms.openlocfilehash: 3827e32186c5f034d9bb6fc502dc26708b52a00a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-linux-password-on-azure-vms"></a>Как tooreset локальный пароль Linux на виртуальных машинах Azure

В этой статье описывается несколько методов tooreset локальных Linux виртуальной машины (VM) паролей. Если истек срок действия учетной записи пользователя hello, или необходимо просто toocreate новую учетную запись, можно использовать следующие методы toocreate новой учетной записи локального администратора hello и повторно получить доступ toohello виртуальной Машины.

## <a name="symptoms"></a>Симптомы

Не удается войти в toohello ВМ и появляется сообщение о том, что это неправильный пароль, который использовался hello. Кроме того вы не может использовать VMAgent tooreset пароль на портале Azure hello. 

## <a name="manual-password-reset-procedure"></a>Процедура сброса пароля вручную

1.  Удаление hello виртуальной Машины с сохранением hello присоединенные диски.

2.  Присоединить диск операционной системы как диск данных tooanother hello временной виртуальной Машины в hello местоположения.

3.  Запустите hello после команды SSH на временной виртуальной Машины toobecome hello суперпользователя.


    ~~~~
    sudo su
    ~~~~

4.  Запустите **fdisk -l** или просмотрите hello toofind журналы системы вновь подключенного диска. Найдите имя toomount hello диска. Затем на hello файл журнала временной виртуальной Машины, можно найти в соответствующей hello.

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    Hello ниже приведен пример выходных данных команды grep hello.

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  Создайте точку подключения **tempmount**.

    ~~~~
    mkdir /tempmount
    ~~~~

6.  Подключите диск hello операционной системы в точке монтирования hello. Обычно требуется toomount sdc1 или sdc2. Это будет зависеть от размещения секции в каталоге/etc с диска неработающие машины hello hello.

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  Создайте резервную копию перед внесением каких-либо изменений.

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  Сброс пароля пользователя hello, необходимо:

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  Перемещение hello изменить правильное расположение файлов toohello на hello неработающие диск компьютера.

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back toohello root and unmount hello disk.

    ~~~~
    cd / umount /tempmount
    ~~~~

11. Detach hello disk from hello management portal.

12. Recreate hello VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk tooanother Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How toodelete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)
