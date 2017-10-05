---
title: "Как сбросить локальный пароль Linux на виртуальных машинах Azure | Документация Майкрософт"
description: "Описывается, как сбросить локальный пароль Linux на виртуальной машине Azure."
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
ms.openlocfilehash: 084cdb26c7dfd8f46fb6ec7f8c48f7b4a327e2ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-local-linux-password-on-azure-vms"></a><span data-ttu-id="86676-103">Как сбросить локальный пароль Linux на виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="86676-103">How to reset local Linux password on Azure VMs</span></span>

<span data-ttu-id="86676-104">В этой статье описано несколько способов сброса локальных паролей на виртуальных машинах Linux.</span><span class="sxs-lookup"><span data-stu-id="86676-104">This article introduces several methods to reset local Linux Virtual Machine (VM) passwords.</span></span> <span data-ttu-id="86676-105">Если истек срок действия учетной записи пользователя или требуется создать новую учетную запись, можно использовать приведенные ниже способы, чтобы создать новую учетную запись локального администратора и повторно получить доступ к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="86676-105">If the user account is expired or you just want to create a new account, you can use the following methods to create a new local admin account and re-gain access to the VM.</span></span>

## <a name="symptoms"></a><span data-ttu-id="86676-106">Симптомы</span><span class="sxs-lookup"><span data-stu-id="86676-106">Symptoms</span></span>

<span data-ttu-id="86676-107">Невозможно подключиться к виртуальной машине, и появляется сообщение о том, что указан неправильный пароль.</span><span class="sxs-lookup"><span data-stu-id="86676-107">You can't log in to the VM, and you receive a message that indicates that the password that you used is incorrect.</span></span> <span data-ttu-id="86676-108">Кроме того, невозможно использовать VMAgent для сброса пароля на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="86676-108">Additionally, you can't use VMAgent to reset your password on the Azure Portal.</span></span> 

## <a name="manual-password-reset-procedure"></a><span data-ttu-id="86676-109">Процедура сброса пароля вручную</span><span class="sxs-lookup"><span data-stu-id="86676-109">Manual Password Reset procedure</span></span>

1.  <span data-ttu-id="86676-110">Удалите виртуальную машину и сохраните ее подключенные диски.</span><span class="sxs-lookup"><span data-stu-id="86676-110">Delete the VM and keep the attached disks.</span></span>

2.  <span data-ttu-id="86676-111">Подключите диск ОС в качестве диска данных к другой временной виртуальной машине в том же расположении.</span><span class="sxs-lookup"><span data-stu-id="86676-111">Attach the OS Drive as a data disk to another temporal VM in the same location.</span></span>

3.  <span data-ttu-id="86676-112">Выполните приведенную ниже команду SSH на временной виртуальной машине, чтобы стать суперпользователем.</span><span class="sxs-lookup"><span data-stu-id="86676-112">Run the following SSH command on the temporal VM to become a super-user.</span></span>


    ~~~~
    sudo su
    ~~~~

4.  <span data-ttu-id="86676-113">Выполните **fdisk -l** или просмотрите системные журналы, чтобы найти только что подключенный диск.</span><span class="sxs-lookup"><span data-stu-id="86676-113">Run **fdisk -l** or look at system logs to find the newly attached disk.</span></span> <span data-ttu-id="86676-114">Найдите имя подключаемого диска.</span><span class="sxs-lookup"><span data-stu-id="86676-114">Locate the drive name to mount.</span></span> <span data-ttu-id="86676-115">Затем на временной виртуальной машине просмотрите соответствующий файл журнала.</span><span class="sxs-lookup"><span data-stu-id="86676-115">Then on the temporal VM, look in the relevant log file.</span></span>

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    <span data-ttu-id="86676-116">Ниже приведен пример выходных данных команды grep.</span><span class="sxs-lookup"><span data-stu-id="86676-116">The following is example output of the grep command:</span></span>

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  <span data-ttu-id="86676-117">Создайте точку подключения **tempmount**.</span><span class="sxs-lookup"><span data-stu-id="86676-117">Create a mount point called **tempmount**.</span></span>

    ~~~~
    mkdir /tempmount
    ~~~~

6.  <span data-ttu-id="86676-118">Подключите диск ОС к точке подключения.</span><span class="sxs-lookup"><span data-stu-id="86676-118">Mount the OS disk on the mount point.</span></span> <span data-ttu-id="86676-119">Обычно требуется подключить sdc1 или sdc2.</span><span class="sxs-lookup"><span data-stu-id="86676-119">You usually need to mount sdc1 or sdc2.</span></span> <span data-ttu-id="86676-120">Это будет зависеть от раздела размещения в каталоге /etc с диска неисправного компьютера.</span><span class="sxs-lookup"><span data-stu-id="86676-120">This will depend on the hosting partition in /etc directory from the broken machine disk.</span></span>

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  <span data-ttu-id="86676-121">Создайте резервную копию перед внесением каких-либо изменений.</span><span class="sxs-lookup"><span data-stu-id="86676-121">Perform a backup before making any changes:</span></span>

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  <span data-ttu-id="86676-122">Сбросьте соответствующий пароль пользователя.</span><span class="sxs-lookup"><span data-stu-id="86676-122">Reset the user’s password that you need:</span></span>

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  <span data-ttu-id="86676-123">Переместите измененные файлы на правильное расположение на диске неисправного компьютера.</span><span class="sxs-lookup"><span data-stu-id="86676-123">Move the modified files to the correct location on the broken machine's disk.</span></span>

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back to the root and unmount the disk.

    ~~~~
    <span data-ttu-id="86676-124">cd / umount /tempmount</span><span class="sxs-lookup"><span data-stu-id="86676-124">cd / umount /tempmount</span></span>
    ~~~~

11. Detach the disk from the management portal.

12. Recreate the VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk to another Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How to delete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)