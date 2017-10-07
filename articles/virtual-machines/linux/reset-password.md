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
ms.openlocfilehash: b28a679a36bf93c6881633eefa03aef3cd33e804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-linux-password-on-azure-vms"></a><span data-ttu-id="640fc-103">Как tooreset локальный пароль Linux на виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="640fc-103">How tooreset local Linux password on Azure VMs</span></span>

<span data-ttu-id="640fc-104">В этой статье описывается несколько методов tooreset локальных Linux виртуальной машины (VM) паролей.</span><span class="sxs-lookup"><span data-stu-id="640fc-104">This article introduces several methods tooreset local Linux Virtual Machine (VM) passwords.</span></span> <span data-ttu-id="640fc-105">Если истек срок действия учетной записи пользователя hello, или необходимо просто toocreate новую учетную запись, можно использовать следующие методы toocreate новой учетной записи локального администратора hello и повторно получить доступ toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="640fc-105">If hello user account is expired or you just want toocreate a new account, you can use hello following methods toocreate a new local admin account and re-gain access toohello VM.</span></span>

## <a name="symptoms"></a><span data-ttu-id="640fc-106">Симптомы</span><span class="sxs-lookup"><span data-stu-id="640fc-106">Symptoms</span></span>

<span data-ttu-id="640fc-107">Не удается войти в toohello ВМ и появляется сообщение о том, что это неправильный пароль, который использовался hello.</span><span class="sxs-lookup"><span data-stu-id="640fc-107">You can't log in toohello VM, and you receive a message that indicates that hello password that you used is incorrect.</span></span> <span data-ttu-id="640fc-108">Кроме того вы не может использовать VMAgent tooreset пароль на портале Azure hello.</span><span class="sxs-lookup"><span data-stu-id="640fc-108">Additionally, you can't use VMAgent tooreset your password on hello Azure Portal.</span></span> 

## <a name="manual-password-reset-procedure"></a><span data-ttu-id="640fc-109">Процедура сброса пароля вручную</span><span class="sxs-lookup"><span data-stu-id="640fc-109">Manual Password Reset procedure</span></span>

1.  <span data-ttu-id="640fc-110">Удаление hello виртуальной Машины с сохранением hello присоединенные диски.</span><span class="sxs-lookup"><span data-stu-id="640fc-110">Delete hello VM and keep hello attached disks.</span></span>

2.  <span data-ttu-id="640fc-111">Присоединить диск операционной системы как диск данных tooanother hello временной виртуальной Машины в hello местоположения.</span><span class="sxs-lookup"><span data-stu-id="640fc-111">Attach hello OS Drive as a data disk tooanother temporal VM in hello same location.</span></span>

3.  <span data-ttu-id="640fc-112">Запустите hello после команды SSH на временной виртуальной Машины toobecome hello суперпользователя.</span><span class="sxs-lookup"><span data-stu-id="640fc-112">Run hello following SSH command on hello temporal VM toobecome a super-user.</span></span>


    ~~~~
    sudo su
    ~~~~

4.  <span data-ttu-id="640fc-113">Запустите **fdisk -l** или просмотрите hello toofind журналы системы вновь подключенного диска.</span><span class="sxs-lookup"><span data-stu-id="640fc-113">Run **fdisk -l** or look at system logs toofind hello newly attached disk.</span></span> <span data-ttu-id="640fc-114">Найдите имя toomount hello диска.</span><span class="sxs-lookup"><span data-stu-id="640fc-114">Locate hello drive name toomount.</span></span> <span data-ttu-id="640fc-115">Затем на hello файл журнала временной виртуальной Машины, можно найти в соответствующей hello.</span><span class="sxs-lookup"><span data-stu-id="640fc-115">Then on hello temporal VM, look in hello relevant log file.</span></span>

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    <span data-ttu-id="640fc-116">Hello ниже приведен пример выходных данных команды grep hello.</span><span class="sxs-lookup"><span data-stu-id="640fc-116">hello following is example output of hello grep command:</span></span>

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  <span data-ttu-id="640fc-117">Создайте точку подключения **tempmount**.</span><span class="sxs-lookup"><span data-stu-id="640fc-117">Create a mount point called **tempmount**.</span></span>

    ~~~~
    mkdir /tempmount
    ~~~~

6.  <span data-ttu-id="640fc-118">Подключите диск hello операционной системы в точке монтирования hello.</span><span class="sxs-lookup"><span data-stu-id="640fc-118">Mount hello OS disk on hello mount point.</span></span> <span data-ttu-id="640fc-119">Обычно требуется toomount sdc1 или sdc2.</span><span class="sxs-lookup"><span data-stu-id="640fc-119">You usually need toomount sdc1 or sdc2.</span></span> <span data-ttu-id="640fc-120">Это будет зависеть от размещения секции в каталоге/etc с диска неработающие машины hello hello.</span><span class="sxs-lookup"><span data-stu-id="640fc-120">This will depend on hello hosting partition in /etc directory from hello broken machine disk.</span></span>

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  <span data-ttu-id="640fc-121">Создайте резервную копию перед внесением каких-либо изменений.</span><span class="sxs-lookup"><span data-stu-id="640fc-121">Perform a backup before making any changes:</span></span>

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  <span data-ttu-id="640fc-122">Сброс пароля пользователя hello, необходимо:</span><span class="sxs-lookup"><span data-stu-id="640fc-122">Reset hello user’s password that you need:</span></span>

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  <span data-ttu-id="640fc-123">Перемещение hello изменить правильное расположение файлов toohello на hello неработающие диск компьютера.</span><span class="sxs-lookup"><span data-stu-id="640fc-123">Move hello modified files toohello correct location on hello broken machine's disk.</span></span>

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back toohello root and unmount hello disk.

    ~~~~
    <span data-ttu-id="640fc-124">cd / umount /tempmount</span><span class="sxs-lookup"><span data-stu-id="640fc-124">cd / umount /tempmount</span></span>
    ~~~~

11. Detach hello disk from hello management portal.

12. Recreate hello VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk tooanother Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How toodelete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)
