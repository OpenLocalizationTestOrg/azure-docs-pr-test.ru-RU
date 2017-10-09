---
title: "aaaOptimize MySQL производительности в Linux | Документы Microsoft"
description: "Узнайте, как toooptimize MySQL на виртуальной машине Azure (ВМ) под управлением Linux."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0c1c7fc5-a528-4d84-b65d-2df225f2233f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: ningk
ms.openlocfilehash: 9e6458723233721e06f30b9de33635d403eefcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a><span data-ttu-id="7395a-103">Оптимизация производительности MySQL на виртуальных машинах Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="7395a-103">Optimize MySQL Performance on Azure Linux VMs</span></span>
<span data-ttu-id="7395a-104">Существует множество факторов, влияющих на производительность MySQL в Azure, которые зависят и от выбора виртуального оборудования, и от конфигурации программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="7395a-104">There are many factors that affect MySQL performance on Azure, both in virtual hardware selection and software configuration.</span></span> <span data-ttu-id="7395a-105">Эта статья посвящена оптимизации производительности с помощью конфигураций хранилища, системы и базы данных.</span><span class="sxs-lookup"><span data-stu-id="7395a-105">This article focuses on optimizing performance through storage, system, and database configurations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7395a-106">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager](../../../resource-manager-deployment-model.md) и классическая модель.</span><span class="sxs-lookup"><span data-stu-id="7395a-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="7395a-107">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="7395a-107">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="7395a-108">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7395a-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="7395a-109">Сведения об оптимизации виртуальных Машин Linux с моделью hello диспетчера ресурсов см. в разделе [оптимизировать ВМ Linux в Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7395a-109">For information about Linux VM optimizations with hello Resource Manager model, see [Optimize your Linux VM on Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="utilize-raid-on-an-azure-virtual-machine"></a><span data-ttu-id="7395a-110">Использование RAID на виртуальной машине Azure</span><span class="sxs-lookup"><span data-stu-id="7395a-110">Utilize RAID on an Azure virtual machine</span></span>
<span data-ttu-id="7395a-111">Хранилище — hello ключевым фактором, влияющим на производительность базы данных в облачных средах.</span><span class="sxs-lookup"><span data-stu-id="7395a-111">Storage is hello key factor that affects database performance in cloud environments.</span></span> <span data-ttu-id="7395a-112">Сравниваемые tooa одного диска, RAID обеспечивается более быстрый доступ посредством параллелизма.</span><span class="sxs-lookup"><span data-stu-id="7395a-112">Compared tooa single disk, RAID can provide faster access via concurrency.</span></span> <span data-ttu-id="7395a-113">Дополнительные сведения см. в описании [стандартных уровней RAID](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span><span class="sxs-lookup"><span data-stu-id="7395a-113">For more information, see [Standard RAID levels](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span></span>   

<span data-ttu-id="7395a-114">С помощью RAID в Azure можно существенно увеличить пропускную способность и время ответа для операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="7395a-114">Disk I/O throughput and I/O response time in Azure can be improved through RAID.</span></span> <span data-ttu-id="7395a-115">Наши тесты лаборатории Показать, что можно удвоить пропускной способности дискового ввода-вывода и времени ответа ввода-вывода уменьшается вдвое в среднем при hello количество дисков RAID в два раза (из двух toofour, четыре tooeight, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="7395a-115">Our lab tests show that disk I/O throughput can be doubled and I/O response time can be reduced by half on average when hello number of RAID disks is doubled (from two toofour, four tooeight, etc.).</span></span> <span data-ttu-id="7395a-116">Дополнительные сведения см. в [приложении А](#AppendixA).</span><span class="sxs-lookup"><span data-stu-id="7395a-116">See [Appendix A](#AppendixA) for details.</span></span>  

<span data-ttu-id="7395a-117">В дополнение к этому toodisk ввода-вывода, MySQL производительность повышается при увеличении hello уровень RAID.</span><span class="sxs-lookup"><span data-stu-id="7395a-117">In addition toodisk I/O, MySQL performance improves when you increase hello RAID level.</span></span>  <span data-ttu-id="7395a-118">Дополнительные сведения см. в [приложении Б](#AppendixB).</span><span class="sxs-lookup"><span data-stu-id="7395a-118">See [Appendix B](#AppendixB) for details.</span></span>  

<span data-ttu-id="7395a-119">Можно также настроить размер блока tooconsider hello.</span><span class="sxs-lookup"><span data-stu-id="7395a-119">You might also want tooconsider hello chunk size.</span></span> <span data-ttu-id="7395a-120">Обычно чем больше размер блока, тем ниже нагрузка, особенно для объемных операций записи.</span><span class="sxs-lookup"><span data-stu-id="7395a-120">In general, when you have a larger chunk size, you get lower overhead, especially for large writes.</span></span> <span data-ttu-id="7395a-121">Однако когда hello размер фрагмента данных слишком велик, может добавить дополнительную нагрузку, которая не позволяет воспользоваться преимуществом RAID.</span><span class="sxs-lookup"><span data-stu-id="7395a-121">However, when hello chunk size is too large, it might add additional overhead that prevents you from taking advantage of RAID.</span></span> <span data-ttu-id="7395a-122">Hello текущий размер по умолчанию — 512 КБ, что подтверждается toobe оптимальным для большинства рабочих сред.</span><span class="sxs-lookup"><span data-stu-id="7395a-122">hello current default size is 512 KB, which is proven toobe optimal for most general production environments.</span></span> <span data-ttu-id="7395a-123">Дополнительные сведения см. в [приложении В](#AppendixC).</span><span class="sxs-lookup"><span data-stu-id="7395a-123">See [Appendix C](#AppendixC) for details.</span></span>   

<span data-ttu-id="7395a-124">Для виртуальных машин разных типов существуют ограничения на количество дисков, которые можно добавить.</span><span class="sxs-lookup"><span data-stu-id="7395a-124">There are limits on how many disks you can add for different virtual machine types.</span></span> <span data-ttu-id="7395a-125">Эти ограничения описаны в статье [Размеры для облачных служб](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="7395a-125">These limits are detailed in [Virtual machine and cloud service sizes for Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span> <span data-ttu-id="7395a-126">Несмотря на то, что вы можете tooset копирование RAID с меньшим числом дисков, потребуется четыре присоединенные диски toofollow hello RAID пример данных в этой статье.</span><span class="sxs-lookup"><span data-stu-id="7395a-126">You will need four attached data disks toofollow hello RAID example in this article, although you can choose tooset up RAID with fewer disks.</span></span>  

<span data-ttu-id="7395a-127">В этой статье предполагается, что вы уже создали виртуальную машину Linux, а также установили и настроили MySQL.</span><span class="sxs-lookup"><span data-stu-id="7395a-127">This article assumes you have already created a Linux virtual machine and have MYSQL installed and configured.</span></span> <span data-ttu-id="7395a-128">Дополнительные сведения о начале работы см. в разделе как tooinstall MySQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="7395a-128">For more information on getting started, see How tooinstall MySQL on Azure.</span></span>  

### <a name="set-up-raid-on-azure"></a><span data-ttu-id="7395a-129">Настройка RAID в Azure</span><span class="sxs-lookup"><span data-stu-id="7395a-129">Set up RAID on Azure</span></span>
<span data-ttu-id="7395a-130">Hello следующие шаги показывают, как toocreate RAID-КОНТРОЛЛЕР на Azure с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7395a-130">hello following steps show how toocreate RAID on Azure by using hello Azure portal.</span></span> <span data-ttu-id="7395a-131">RAID также можно настроить с помощью сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7395a-131">You can also set up RAID by using Windows PowerShell scripts.</span></span>
<span data-ttu-id="7395a-132">В этом примере мы настроим RAID 0 с 4 дисками.</span><span class="sxs-lookup"><span data-stu-id="7395a-132">In this example, we will configure RAID 0 with four disks.</span></span>  

#### <a name="add-a-data-disk-tooyour-virtual-machine"></a><span data-ttu-id="7395a-133">Добавить виртуальную машину tooyour диска данных</span><span class="sxs-lookup"><span data-stu-id="7395a-133">Add a data disk tooyour virtual machine</span></span>
<span data-ttu-id="7395a-134">В hello портал Azure перейдите toohello панели мониторинга и выберите toowhich hello виртуальной машины, нужно tooadd диск данных.</span><span class="sxs-lookup"><span data-stu-id="7395a-134">In hello Azure portal, go toohello dashboard and select hello virtual machine toowhich you want tooadd a data disk.</span></span> <span data-ttu-id="7395a-135">В этом примере hello виртуальной машины — mysqlnode1.</span><span class="sxs-lookup"><span data-stu-id="7395a-135">In this example, hello virtual machine is mysqlnode1.</span></span>  

<!--![Virtual machines][1]-->

<span data-ttu-id="7395a-136">Щелкните **Диски** и выберите **Подключить новый**.</span><span class="sxs-lookup"><span data-stu-id="7395a-136">Click **Disks** and then click **Attach New**.</span></span>

![Добавление дисков в виртуальную машину](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

<span data-ttu-id="7395a-138">Создайте новый диск объемом 500 ГБ.</span><span class="sxs-lookup"><span data-stu-id="7395a-138">Create a new 500 GB disk.</span></span> <span data-ttu-id="7395a-139">Убедитесь, что **настройки кэша узла** задано слишком**нет**.</span><span class="sxs-lookup"><span data-stu-id="7395a-139">Make sure that **Host Cache Preference** is set too**None**.</span></span>  <span data-ttu-id="7395a-140">Закончив, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7395a-140">When you're finished, click **OK**.</span></span>

![Присоединить пустой диск](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


<span data-ttu-id="7395a-142">Теперь вы добавили один пустой диск в виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="7395a-142">This adds one empty disk into your virtual machine.</span></span> <span data-ttu-id="7395a-143">Повторите этот шаг еще три раза, чтобы настроить четыре диска данных для RAID.</span><span class="sxs-lookup"><span data-stu-id="7395a-143">Repeat this step three more times so that you have four data disks for RAID.</span></span>  

<span data-ttu-id="7395a-144">Вы увидите hello добавлены дисков на виртуальной машине hello, просмотрев журнал сообщений hello ядра.</span><span class="sxs-lookup"><span data-stu-id="7395a-144">You can see hello added drives in hello virtual machine by looking at hello kernel message log.</span></span> <span data-ttu-id="7395a-145">Например, toosee это на Ubuntu hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7395a-145">For example, toosee this on Ubuntu, use hello following command:</span></span>  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-hello-additional-disks"></a><span data-ttu-id="7395a-146">Создайте RAID с hello дополнительные диски.</span><span class="sxs-lookup"><span data-stu-id="7395a-146">Create RAID with hello additional disks</span></span>
<span data-ttu-id="7395a-147">Hello следующие шаги описывают как слишком[Настройка программного RAID на платформе Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7395a-147">hello following steps describe how too[configure software RAID on Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="7395a-148">При использовании hello XFS файловой системы, выполните следующие шаги после создания RAID hello.</span><span class="sxs-lookup"><span data-stu-id="7395a-148">If you are using hello XFS file system, execute hello following steps after you have created RAID.</span></span>
>
>

<span data-ttu-id="7395a-149">tooinstall XFS на Linux Mint, Debian и Ubuntu hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7395a-149">tooinstall XFS on Debian, Ubuntu, or Linux Mint, use hello following command:</span></span>  

    apt-get -y install xfsprogs  

<span data-ttu-id="7395a-150">tooinstall XFS на Fedora, CentOS или RHEL, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7395a-150">tooinstall XFS on Fedora, CentOS, or RHEL, use hello following command:</span></span>  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a><span data-ttu-id="7395a-151">Настройка нового пути к хранилищу</span><span class="sxs-lookup"><span data-stu-id="7395a-151">Set up a new storage path</span></span>
<span data-ttu-id="7395a-152">Используйте hello следующая команда tooset новый путь хранения:</span><span class="sxs-lookup"><span data-stu-id="7395a-152">Use hello following command tooset up a new storage path:</span></span>  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-hello-original-data-toohello-new-storage-path"></a><span data-ttu-id="7395a-153">Скопируйте hello исходные данные toohello новый путь к хранилищу</span><span class="sxs-lookup"><span data-stu-id="7395a-153">Copy hello original data toohello new storage path</span></span>
<span data-ttu-id="7395a-154">Используйте следующие команды toocopy данных toohello новый путь к хранилищу hello.</span><span class="sxs-lookup"><span data-stu-id="7395a-154">Use hello following command toocopy data toohello new storage path:</span></span>  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-hello-data-disk"></a><span data-ttu-id="7395a-155">Изменить разрешения, поэтому можно получить доступ к MySQL (чтение и запись) диска данных hello</span><span class="sxs-lookup"><span data-stu-id="7395a-155">Modify permissions so MySQL can access (read and write) hello data disk</span></span>
<span data-ttu-id="7395a-156">Используйте следующие команды toomodify разрешения hello.</span><span class="sxs-lookup"><span data-stu-id="7395a-156">Use hello following command toomodify permissions:</span></span>  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-hello-disk-io-scheduling-algorithm"></a><span data-ttu-id="7395a-157">Настройка hello дискового ввода-вывода, алгоритм планирования</span><span class="sxs-lookup"><span data-stu-id="7395a-157">Adjust hello disk I/O scheduling algorithm</span></span>
<span data-ttu-id="7395a-158">В Linux реализовано четыре типа алгоритмов планирования операций ввода-вывода:</span><span class="sxs-lookup"><span data-stu-id="7395a-158">Linux implements four types of I/O scheduling algorithms:</span></span>  

* <span data-ttu-id="7395a-159">алгоритм NOOP (без операции);</span><span class="sxs-lookup"><span data-stu-id="7395a-159">NOOP algorithm (No Operation)</span></span>
* <span data-ttu-id="7395a-160">алгоритм крайнего срока (крайний срок);</span><span class="sxs-lookup"><span data-stu-id="7395a-160">Deadline algorithm (Deadline)</span></span>
* <span data-ttu-id="7395a-161">алгоритм организации полностью равноправных очередей (CFQ);</span><span class="sxs-lookup"><span data-stu-id="7395a-161">Completely fair queuing algorithm (CFQ)</span></span>
* <span data-ttu-id="7395a-162">алгоритм бюджетного периода (прогнозирование).</span><span class="sxs-lookup"><span data-stu-id="7395a-162">Budget period algorithm (Anticipatory)</span></span>  

<span data-ttu-id="7395a-163">Можно выбрать различные планировщики ввода-вывода в различных сценариях toooptimize производительности.</span><span class="sxs-lookup"><span data-stu-id="7395a-163">You can select different I/O schedulers under different scenarios toooptimize performance.</span></span> <span data-ttu-id="7395a-164">В среде полностью произвольного доступа не значительные различия между hello CFQ и алгоритмы крайний срок для повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="7395a-164">In a completely random access environment, there is not a significant difference between hello CFQ and Deadline algorithms for performance.</span></span> <span data-ttu-id="7395a-165">Мы рекомендуем задавать tooDeadline среды базы данных MySQL hello для стабильности.</span><span class="sxs-lookup"><span data-stu-id="7395a-165">We recommend that you set hello MySQL database environment tooDeadline for stability.</span></span> <span data-ttu-id="7395a-166">Если выполняется много последовательных операций ввода-вывода, метод равноправных очередей может снизить производительность дисковых операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="7395a-166">If there is a lot of sequential I/O, CFQ might reduce disk I/O performance.</span></span>   

<span data-ttu-id="7395a-167">SSD и другом оборудовании NOOP или крайний срок можно улучшить производительность, чем планировщик по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="7395a-167">For SSD and other equipment, NOOP or Deadline can achieve better performance than hello default scheduler.</span></span>   

<span data-ttu-id="7395a-168">Предыдущий toohello ядра 2.5 hello ввода-вывода по умолчанию алгоритм планирования — крайнего срока.</span><span class="sxs-lookup"><span data-stu-id="7395a-168">Prior toohello kernel 2.5, hello default I/O scheduling algorithm is Deadline.</span></span> <span data-ttu-id="7395a-169">Начиная с hello ядра 2.6.18 CFQ стала Алгоритм планирования операций ввода-вывода по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="7395a-169">Starting with hello kernel 2.6.18, CFQ became hello default I/O scheduling algorithm.</span></span>  <span data-ttu-id="7395a-170">Можно указать этот параметр во время загрузки ядра или динамически изменять этот параметр, при запуске системы hello.</span><span class="sxs-lookup"><span data-stu-id="7395a-170">You can specify this setting at kernel boot time or dynamically modify this setting when hello system is running.</span></span>  

<span data-ttu-id="7395a-171">Hello в следующем примере показано, как toocheck и набор hello алгоритм NOOP toohello планировщик по умолчанию hello Debian распространения семейства.</span><span class="sxs-lookup"><span data-stu-id="7395a-171">hello following example demonstrates how toocheck and set hello default scheduler toohello NOOP algorithm in hello Debian distribution family.</span></span>  

### <a name="view-hello-current-io-scheduler"></a><span data-ttu-id="7395a-172">Представление hello текущего планировщика ввода-вывода</span><span class="sxs-lookup"><span data-stu-id="7395a-172">View hello current I/O scheduler</span></span>
<span data-ttu-id="7395a-173">Запустите планировщик hello tooview hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7395a-173">tooview hello scheduler run hello following command:</span></span>  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

<span data-ttu-id="7395a-174">Вы увидите следующие выходных данных, который указывает hello текущего планировщика.</span><span class="sxs-lookup"><span data-stu-id="7395a-174">You will see following output, which indicates hello current scheduler:</span></span>  

    noop [deadline] cfq


### <a name="change-hello-current-device-devsda-of-hello-io-scheduling-algorithm"></a><span data-ttu-id="7395a-175">Изменить текущее устройство hello (/ dev/sda) Алгоритм планирования hello ввода-вывода</span><span class="sxs-lookup"><span data-stu-id="7395a-175">Change hello current device (/dev/sda) of hello I/O scheduling algorithm</span></span>
<span data-ttu-id="7395a-176">Выполните следующие команды toochange hello текущего устройства hello.</span><span class="sxs-lookup"><span data-stu-id="7395a-176">Run hello following commands toochange hello current device:</span></span>  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> <span data-ttu-id="7395a-177">Настраивать алгоритм только для устройства /dev/sda бесполезно.</span><span class="sxs-lookup"><span data-stu-id="7395a-177">Setting this for /dev/sda alone is not useful.</span></span> <span data-ttu-id="7395a-178">Его необходимо задавать на все диски с данными, где находится база данных hello.</span><span class="sxs-lookup"><span data-stu-id="7395a-178">It must be set on all data disks where hello database resides.</span></span>  
>
>

<span data-ttu-id="7395a-179">Вы должны увидеть hello следующие выходные данные, об grub.cfg был перестроен успешно, и этот планировщик по умолчанию hello был обновленные tooNOOP.</span><span class="sxs-lookup"><span data-stu-id="7395a-179">You should see hello following output, indicating that grub.cfg has been rebuilt successfully and that hello default scheduler has been updated tooNOOP:</span></span>  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

<span data-ttu-id="7395a-180">Для hello семейства распространения Red Hat требуются только hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7395a-180">For hello Red Hat distribution family, you need only hello following command:</span></span>

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a><span data-ttu-id="7395a-181">Настройка параметров операций системного файла</span><span class="sxs-lookup"><span data-stu-id="7395a-181">Configure system file operations settings</span></span>
<span data-ttu-id="7395a-182">Один рекомендуется toodisable hello *atime* функции ведения журнала в файловой системе hello.</span><span class="sxs-lookup"><span data-stu-id="7395a-182">One best practice is toodisable hello *atime* logging feature on hello file system.</span></span> <span data-ttu-id="7395a-183">Atime — hello времени последнего открытия файла.</span><span class="sxs-lookup"><span data-stu-id="7395a-183">Atime is hello last file access time.</span></span> <span data-ttu-id="7395a-184">При каждом обращении к файлу, записей hello hello timestamp в журнале hello.</span><span class="sxs-lookup"><span data-stu-id="7395a-184">Whenever a file is accessed, hello file system records hello timestamp in hello log.</span></span> <span data-ttu-id="7395a-185">Однако эта информация используется редко.</span><span class="sxs-lookup"><span data-stu-id="7395a-185">However, this information is rarely used.</span></span> <span data-ttu-id="7395a-186">При необходимости эту функцию можно отключить, что позволит уменьшить общее время доступа к диску.</span><span class="sxs-lookup"><span data-stu-id="7395a-186">You can disable it if you don't need it, which will reduce overall disk access time.</span></span>  

<span data-ttu-id="7395a-187">toodisable atime ведения журнала, toomodify hello файла система конфигурации файл/etc / fstab и добавьте hello **noatime** параметр.</span><span class="sxs-lookup"><span data-stu-id="7395a-187">toodisable atime logging, you need toomodify hello file system configuration file /etc/ fstab and add hello **noatime** option.</span></span>  

<span data-ttu-id="7395a-188">Например измените файл/etc/fstab vim hello, добавления hello noatime, как показано в следующих образец hello.</span><span class="sxs-lookup"><span data-stu-id="7395a-188">For example, edit hello vim /etc/fstab file, adding hello noatime as shown in hello following sample:</span></span>  

    # CLOUD_IMG: This file was created/modified by hello Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add hello “noatime” option below toodisable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

<span data-ttu-id="7395a-189">Затем подключите hello файловой системы с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7395a-189">Then, remount hello file system with hello following command:</span></span>  

    mount -o remount /RAID0

<span data-ttu-id="7395a-190">Тест hello изменить результат.</span><span class="sxs-lookup"><span data-stu-id="7395a-190">Test hello modified result.</span></span> <span data-ttu-id="7395a-191">При изменении файла теста hello, время доступа hello не обновляется.</span><span class="sxs-lookup"><span data-stu-id="7395a-191">When you modify hello test file, hello access time is not updated.</span></span> <span data-ttu-id="7395a-192">Hello в следующих примерах показано, какая часть кода hello выглядит до и после изменения.</span><span class="sxs-lookup"><span data-stu-id="7395a-192">hello following examples show what hello code looks like before and after modification.</span></span>

<span data-ttu-id="7395a-193">До:</span><span class="sxs-lookup"><span data-stu-id="7395a-193">Before:</span></span>        

![Код до внесения изменений][5]

<span data-ttu-id="7395a-195">После:</span><span class="sxs-lookup"><span data-stu-id="7395a-195">After:</span></span>

![Код после внесения изменений][6]

## <a name="increase-hello-maximum-number-of-system-handles-for-high-concurrency"></a><span data-ttu-id="7395a-197">Увеличьте максимальное число системных дескрипторов для высокого уровня параллелизма hello</span><span class="sxs-lookup"><span data-stu-id="7395a-197">Increase hello maximum number of system handles for high concurrency</span></span>
<span data-ttu-id="7395a-198">MySQL — база данных с высокой степенью параллелизма.</span><span class="sxs-lookup"><span data-stu-id="7395a-198">MySQL is a high concurrency database.</span></span> <span data-ttu-id="7395a-199">количество параллельных дескрипторы по умолчанию Hello — 1024 для Linux, что не всегда достаточно.</span><span class="sxs-lookup"><span data-stu-id="7395a-199">hello default number of concurrent handles is 1024 for Linux, which is not always sufficient.</span></span> <span data-ttu-id="7395a-200">Используйте следующие шаги tooincrease hello Максимальная одновременных дескрипторы hello системы toosupport высокого уровня параллелизма MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="7395a-200">Use hello following steps tooincrease hello maximum concurrent handles of hello system toosupport high concurrency of MySQL.</span></span>

### <a name="modify-hello-limitsconf-file"></a><span data-ttu-id="7395a-201">Измените файл limits.conf hello</span><span class="sxs-lookup"><span data-stu-id="7395a-201">Modify hello limits.conf file</span></span>
<span data-ttu-id="7395a-202">hello tooincrease максимальное допустимое параллельных дескрипторов, добавьте следующие четыре строки в файле /etc/security/limits.conf hello hello.</span><span class="sxs-lookup"><span data-stu-id="7395a-202">tooincrease hello maximum allowed concurrent handles, add hello following four lines in hello /etc/security/limits.conf file.</span></span> <span data-ttu-id="7395a-203">Обратите внимание, что 65536 hello максимального количества, которое может поддерживаться системой hello.</span><span class="sxs-lookup"><span data-stu-id="7395a-203">Note that 65536 is hello maximum number that hello system can support.</span></span>   

    * <span data-ttu-id="7395a-204">soft nofile 65536</span><span class="sxs-lookup"><span data-stu-id="7395a-204">soft nofile 65536</span></span>
    * <span data-ttu-id="7395a-205">hard nofile 65536</span><span class="sxs-lookup"><span data-stu-id="7395a-205">hard nofile 65536</span></span>
    * <span data-ttu-id="7395a-206">soft nproc 65536</span><span class="sxs-lookup"><span data-stu-id="7395a-206">soft nproc 65536</span></span>
    * <span data-ttu-id="7395a-207">hard nproc 65536</span><span class="sxs-lookup"><span data-stu-id="7395a-207">hard nproc 65536</span></span>

### <a name="update-hello-system-for-hello-new-limits"></a><span data-ttu-id="7395a-208">Обновление системы hello hello новых ограничений</span><span class="sxs-lookup"><span data-stu-id="7395a-208">Update hello system for hello new limits</span></span>
<span data-ttu-id="7395a-209">tooupdate система hello, запустите hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="7395a-209">tooupdate hello system, run hello following commands:</span></span>  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-hello-limits-are-updated-at-boot-time"></a><span data-ttu-id="7395a-210">Убедитесь, что ограничения hello обновляются во время загрузки</span><span class="sxs-lookup"><span data-stu-id="7395a-210">Ensure that hello limits are updated at boot time</span></span>
<span data-ttu-id="7395a-211">Поместите hello, после запуска команды в файле /etc/rc.local hello, вступают в силу во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="7395a-211">Put hello following startup commands in hello /etc/rc.local file so it will take effect at boot time.</span></span>  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a><span data-ttu-id="7395a-212">Оптимизация базы данных MySQL</span><span class="sxs-lookup"><span data-stu-id="7395a-212">MySQL database optimization</span></span>
<span data-ttu-id="7395a-213">tooconfigure MySQL в Azure, можно использовать hello же стратегия настройки производительности, используйте на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="7395a-213">tooconfigure MySQL on Azure, you can use hello same performance-tuning strategy you use on an on-premises machine.</span></span>  

<span data-ttu-id="7395a-214">Hello основных операций ввода-вывода оптимизации правила таковы:</span><span class="sxs-lookup"><span data-stu-id="7395a-214">hello main I/O optimization rules are:</span></span>   

* <span data-ttu-id="7395a-215">Увеличивайте размер кэша hello.</span><span class="sxs-lookup"><span data-stu-id="7395a-215">Increase hello cache size.</span></span>
* <span data-ttu-id="7395a-216">уменьшите время ответа при выполнении операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="7395a-216">Reduce I/O response time.</span></span>  

<span data-ttu-id="7395a-217">Параметры сервера MySQL toooptimize, можно обновить файл my.cnf hello, хранящийся в файле конфигурации по умолчанию hello для сервера и клиентских компьютеров.</span><span class="sxs-lookup"><span data-stu-id="7395a-217">toooptimize MySQL server settings, you can update hello my.cnf file, which is hello default configuration file for both server and client computers.</span></span>  

<span data-ttu-id="7395a-218">Hello следующие элементы конфигурации являются hello основные факторы, влияющие на производительность MySQL.</span><span class="sxs-lookup"><span data-stu-id="7395a-218">hello following configuration items are hello main factors that affect MySQL performance:</span></span>  

* <span data-ttu-id="7395a-219">**innodb_buffer_pool_size**: hello буферный пул содержит буферизованные данные и индекс hello.</span><span class="sxs-lookup"><span data-stu-id="7395a-219">**innodb_buffer_pool_size**: hello buffer pool contains buffered data and hello index.</span></span> <span data-ttu-id="7395a-220">Этот параметр обычно задается too70% физической памяти.</span><span class="sxs-lookup"><span data-stu-id="7395a-220">This is usually set too70 percent of physical memory.</span></span>
* <span data-ttu-id="7395a-221">**innodb_log_file_size**: размер журнала hello повтора.</span><span class="sxs-lookup"><span data-stu-id="7395a-221">**innodb_log_file_size**: This is hello redo log size.</span></span> <span data-ttu-id="7395a-222">Используется tooensure журналы повтора операции записи, быстрый, надежный и возможностью восстановления после сбоя.</span><span class="sxs-lookup"><span data-stu-id="7395a-222">You use redo logs tooensure that write operations are fast, reliable, and recoverable after a crash.</span></span> <span data-ttu-id="7395a-223">Этот параметр задается too512 МБ, что обеспечит Вам достаточно места для ведения журнала операций записи.</span><span class="sxs-lookup"><span data-stu-id="7395a-223">This is set too512 MB, which will give you plenty of space for logging write operations.</span></span>
* <span data-ttu-id="7395a-224">**max_connections**. Иногда приложения не закрывают подключения должным образом.</span><span class="sxs-lookup"><span data-stu-id="7395a-224">**max_connections**: Sometimes applications do not close connections properly.</span></span> <span data-ttu-id="7395a-225">Увеличьте значение даст hello server toorecycle привело к бездействию подключений больше времени.</span><span class="sxs-lookup"><span data-stu-id="7395a-225">A larger value will give hello server more time toorecycle idled connections.</span></span> <span data-ttu-id="7395a-226">Максимальное число подключений Hello 10 000, но рекомендуется hello, максимальное — 5000.</span><span class="sxs-lookup"><span data-stu-id="7395a-226">hello maximum number of connections is 10,000, but hello recommended maximum is 5,000.</span></span>
* <span data-ttu-id="7395a-227">**Innodb_file_per_table**: этот параметр включает или отключает возможность hello InnoDB toostore таблиц в отдельных файлах.</span><span class="sxs-lookup"><span data-stu-id="7395a-227">**Innodb_file_per_table**: This setting enables or disables hello ability of InnoDB toostore tables in separate files.</span></span> <span data-ttu-id="7395a-228">Включите параметр tooensure hello, что несколько операций расширенного администрирования может применяться эффективно.</span><span class="sxs-lookup"><span data-stu-id="7395a-228">Turn on hello option tooensure that several advanced administration operations can be applied efficiently.</span></span> <span data-ttu-id="7395a-229">С точки зрения производительности его ускорения передачи пространство таблицы hello и оптимизировать производительность управления hello мусор.</span><span class="sxs-lookup"><span data-stu-id="7395a-229">From a performance point of view, it can speed up hello table space transmission and optimize hello debris management performance.</span></span> <span data-ttu-id="7395a-230">Hello рекомендуемые для этого параметра имеет значение ON.</span><span class="sxs-lookup"><span data-stu-id="7395a-230">hello recommended setting for this option is ON.</span></span></br></br>
<span data-ttu-id="7395a-231">Из MySQL 5.6 hello по умолчанию равно ON, поэтому никаких действий не требуется.</span><span class="sxs-lookup"><span data-stu-id="7395a-231">From MySQL 5.6, hello default setting is ON, so no action is required.</span></span> <span data-ttu-id="7395a-232">В более ранних версиях hello по умолчанию — OFF.</span><span class="sxs-lookup"><span data-stu-id="7395a-232">For earlier versions, hello default setting is OFF.</span></span> <span data-ttu-id="7395a-233">параметр Hello должны изменяться до загрузки данных, так как она затронет только вновь созданных таблицах.</span><span class="sxs-lookup"><span data-stu-id="7395a-233">hello setting should be changed before data is loaded, because only newly created tables are affected.</span></span>
* <span data-ttu-id="7395a-234">**innodb_flush_log_at_trx_commit**: hello значение по умолчанию равно 1, с hello область значение too0 ~ 2.</span><span class="sxs-lookup"><span data-stu-id="7395a-234">**innodb_flush_log_at_trx_commit**: hello default value is 1, with hello scope set too0~2.</span></span> <span data-ttu-id="7395a-235">значение по умолчанию Hello — hello наиболее подходящий вариант для автономной базы данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="7395a-235">hello default value is hello most suitable option for standalone MySQL DB.</span></span> <span data-ttu-id="7395a-236">Hello, равное 2 — разрешает hello большинство целостность данных и подходит для базы данных Master в кластере MySQL.</span><span class="sxs-lookup"><span data-stu-id="7395a-236">hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL Cluster.</span></span> <span data-ttu-id="7395a-237">параметр Hello 0 позволяет потерь данных, который может повлиять на надежность (в некоторых случаях с точки зрения производительности) и подходит для ведомый экземпляр в кластер MySQL.</span><span class="sxs-lookup"><span data-stu-id="7395a-237">hello setting of 0 allows data loss, which can affect reliability (in some cases with better performance), and is suitable for Slave in MySQL Cluster.</span></span>
* <span data-ttu-id="7395a-238">**Innodb_log_buffer_size**: hello буфера журнала позволяет toorun транзакций без необходимости toodisk журнала hello tooflush до фиксации транзакции hello.</span><span class="sxs-lookup"><span data-stu-id="7395a-238">**Innodb_log_buffer_size**: hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit.</span></span> <span data-ttu-id="7395a-239">Если большой двоичный объект или текстовое поле, hello кэша будет быстро израсходовано и часто дискового ввода-вывода будет запущено.</span><span class="sxs-lookup"><span data-stu-id="7395a-239">However, if there is large binary object or text field, hello cache will be consumed quickly and frequent disk I/O will be triggered.</span></span> <span data-ttu-id="7395a-240">Это лучше увеличить размер буфера hello, если переменной состояния Innodb_log_waits не 0.</span><span class="sxs-lookup"><span data-stu-id="7395a-240">It is better increase hello buffer size if Innodb_log_waits state variable is not 0.</span></span>
* <span data-ttu-id="7395a-241">**query_cache_size**: hello наилучшим вариантом является toodisable с самого начала hello.</span><span class="sxs-lookup"><span data-stu-id="7395a-241">**query_cache_size**: hello best option is toodisable it from hello outset.</span></span> <span data-ttu-id="7395a-242">Too0 query_cache_size (это параметр по умолчанию hello в MySQL 5.6) и выбрать другие методы toospeed запросов.</span><span class="sxs-lookup"><span data-stu-id="7395a-242">Set query_cache_size too0 (this is hello default setting in MySQL 5.6) and use other methods toospeed up queries.</span></span>  

<span data-ttu-id="7395a-243">В разделе [приложение D](#AppendixD) Сравнение производительности до и после оптимизации hello.</span><span class="sxs-lookup"><span data-stu-id="7395a-243">See [Appendix D](#AppendixD) for a comparison of performance before and after hello optimization.</span></span>

## <a name="turn-on-hello-mysql-slow-query-log-for-analyzing-hello-performance-bottleneck"></a><span data-ttu-id="7395a-244">Включите журнал медленных запросов hello MySQL для анализа узким местом производительности hello</span><span class="sxs-lookup"><span data-stu-id="7395a-244">Turn on hello MySQL slow query log for analyzing hello performance bottleneck</span></span>
<span data-ttu-id="7395a-245">Журнал медленных запросов в MySQL Hello может помочь в идентификации медленных запросов hello для MySQL.</span><span class="sxs-lookup"><span data-stu-id="7395a-245">hello MySQL slow query log can help you identify hello slow queries for MySQL.</span></span> <span data-ttu-id="7395a-246">После включения журнал медленных запросов в MySQL hello, вы можете использовать инструменты MySQL как **mysqldumpslow** tooidentify узким местом производительности hello.</span><span class="sxs-lookup"><span data-stu-id="7395a-246">After enabling hello MySQL slow query log, you can use MySQL tools like **mysqldumpslow** tooidentify hello performance bottleneck.</span></span>  

<span data-ttu-id="7395a-247">По умолчанию он отключен.</span><span class="sxs-lookup"><span data-stu-id="7395a-247">By default, this is not enabled.</span></span> <span data-ttu-id="7395a-248">Включение hello журнал медленных запросов может использовать некоторые ресурсы ЦП.</span><span class="sxs-lookup"><span data-stu-id="7395a-248">Turning on hello slow query log might consume some CPU resources.</span></span> <span data-ttu-id="7395a-249">Мы рекомендуем включать его ненадолго, только для устранения узких мест производительности.</span><span class="sxs-lookup"><span data-stu-id="7395a-249">We recommend that you enable this temporarily for troubleshooting performance bottlenecks.</span></span> <span data-ttu-id="7395a-250">tooturn на журнал медленных запросов hello:</span><span class="sxs-lookup"><span data-stu-id="7395a-250">tooturn on hello slow query log:</span></span>

1. <span data-ttu-id="7395a-251">Измените файл my.cnf hello, добавив после окончания строк toohello hello:</span><span class="sxs-lookup"><span data-stu-id="7395a-251">Modify hello my.cnf file by adding hello following lines toohello end:</span></span>

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. <span data-ttu-id="7395a-252">Перезапустите сервер MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="7395a-252">Restart hello MySQL server.</span></span>

        service  mysql  restart

3. <span data-ttu-id="7395a-253">Проверьте, занимает ли приветствия эффект с помощью hello **Показать** команды.</span><span class="sxs-lookup"><span data-stu-id="7395a-253">Check whether hello setting is taking effect by using hello **show** command.</span></span>

![Включение Slow-query-log][7]   

![Результаты Slow-query-log][8]

<span data-ttu-id="7395a-256">В этом примере вы увидите, включите эту функцию hello медленных запросов.</span><span class="sxs-lookup"><span data-stu-id="7395a-256">In this example, you can see that hello slow query feature has been turned on.</span></span> <span data-ttu-id="7395a-257">Затем можно использовать hello **mysqldumpslow** средства toodetermine узкие места по производительности и оптимизации производительности, например, добавлением индексов.</span><span class="sxs-lookup"><span data-stu-id="7395a-257">You can then use hello **mysqldumpslow** tool toodetermine performance bottlenecks and optimize performance, such as adding indexes.</span></span>

## <a name="appendices"></a><span data-ttu-id="7395a-258">Приложения</span><span class="sxs-lookup"><span data-stu-id="7395a-258">Appendices</span></span>
<span data-ttu-id="7395a-259">Здесь представлены Hello образец производительности тестовых данных, полученных в целевой среде.</span><span class="sxs-lookup"><span data-stu-id="7395a-259">hello following are sample performance test data produced in a targeted lab environment.</span></span> <span data-ttu-id="7395a-260">Они предоставляют общие для данных тренда hello производительности различных подходов быстродействия.</span><span class="sxs-lookup"><span data-stu-id="7395a-260">They provide general background on hello performance data trend with different performance tuning approaches.</span></span> <span data-ttu-id="7395a-261">Hello результаты могут отличаться в различных версиях среды или продукта.</span><span class="sxs-lookup"><span data-stu-id="7395a-261">hello results might vary under different environment or product versions.</span></span>

### <span data-ttu-id="7395a-262"><a name="AppendixA"></a>Приложение А</span><span class="sxs-lookup"><span data-stu-id="7395a-262"><a name="AppendixA"></a>Appendix A</span></span>  
<span data-ttu-id="7395a-263">**Производительность диска (количество операций ввода-вывода в секунду) с разными уровнями RAID**</span><span class="sxs-lookup"><span data-stu-id="7395a-263">**Disk performance (IOPS) with different RAID levels**</span></span>

![Количество операций ввода-вывода в секунду с разными уровнями RAID][9]

<span data-ttu-id="7395a-265">**Команды тестирования**</span><span class="sxs-lookup"><span data-stu-id="7395a-265">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> <span data-ttu-id="7395a-266">Рабочая нагрузка Hello этого теста использует 64 потока, попытки tooreach hello верхний предел RAID.</span><span class="sxs-lookup"><span data-stu-id="7395a-266">hello workload of this test uses 64 threads, trying tooreach hello upper limit of RAID.</span></span>
>
>

### <span data-ttu-id="7395a-267"><a name="AppendixB"></a>Приложение Б</span><span class="sxs-lookup"><span data-stu-id="7395a-267"><a name="AppendixB"></a>Appendix B</span></span>  
<span data-ttu-id="7395a-268">**Сравнение производительности (пропускной способности) MySQL с разными уровнями RAID** </span><span class="sxs-lookup"><span data-stu-id="7395a-268">**MySQL performance (throughput) comparison with different RAID levels** </span></span>  
<span data-ttu-id="7395a-269">(Файловая система XFS)</span><span class="sxs-lookup"><span data-stu-id="7395a-269">(XFS file system)</span></span>

![Сравнение производительности MySQL с разными уровнями RAID][10]  
![Сравнение производительности MySQL с разными уровнями RAID][11]

<span data-ttu-id="7395a-272">**Команды тестирования**</span><span class="sxs-lookup"><span data-stu-id="7395a-272">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

<span data-ttu-id="7395a-273">**Сравнение производительности (OLTP) MySQL с разными уровнями RAID**</span><span class="sxs-lookup"><span data-stu-id="7395a-273">**MySQL performance (OLTP) comparison with different RAID levels**</span></span>  
<span data-ttu-id="7395a-274">![Сравнение производительности (OLTP) MySQL с разными уровнями RAID][12]</span><span class="sxs-lookup"><span data-stu-id="7395a-274">![MySQL performance (OLTP) comparison with different RAID levels][12]</span></span>

<span data-ttu-id="7395a-275">**Команды тестирования**</span><span class="sxs-lookup"><span data-stu-id="7395a-275">**Test commands**</span></span>

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <span data-ttu-id="7395a-276"><a name="AppendixC"></a>Приложение В</span><span class="sxs-lookup"><span data-stu-id="7395a-276"><a name="AppendixC"></a>Appendix C</span></span>   
<span data-ttu-id="7395a-277">**Сравнение производительности диска (количества операций ввода-вывода в секунду) для разного размера блоков**</span><span class="sxs-lookup"><span data-stu-id="7395a-277">**Disk performance (IOPS) comparison for different chunk sizes**</span></span>  
<span data-ttu-id="7395a-278">(Файловая система XFS)</span><span class="sxs-lookup"><span data-stu-id="7395a-278">(XFS file system)</span></span>

![][13]

<span data-ttu-id="7395a-279">**Команды тестирования**</span><span class="sxs-lookup"><span data-stu-id="7395a-279">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

<span data-ttu-id="7395a-280">размеры файлов Hello, используемые для тестирования 30 ГБ и 1 ГБ, соответственно, с помощью RAID 0 (4 диска) XFS файловой системы.</span><span class="sxs-lookup"><span data-stu-id="7395a-280">hello file sizes used for this testing are 30 GB and 1 GB, respectively, with RAID 0 (4 disks) XFS file system.</span></span>

### <span data-ttu-id="7395a-281"><a name="AppendixD"></a>Приложение Г</span><span class="sxs-lookup"><span data-stu-id="7395a-281"><a name="AppendixD"></a>Appendix D</span></span>  
<span data-ttu-id="7395a-282">**Сравнение производительности (пропускной способности) MySQL до и после оптимизации**</span><span class="sxs-lookup"><span data-stu-id="7395a-282">**MySQL performance (throughput) comparison before and after optimization**</span></span>  
<span data-ttu-id="7395a-283">(Файловая система XFS)</span><span class="sxs-lookup"><span data-stu-id="7395a-283">(XFS File System)</span></span>

![Сравнение производительности (пропускной способности) MySQL до и после оптимизации][14]

<span data-ttu-id="7395a-285">**Команды тестирования**</span><span class="sxs-lookup"><span data-stu-id="7395a-285">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

<span data-ttu-id="7395a-286">**параметр конфигурации Hello для оптимизации и по умолчанию будет следующим:**</span><span class="sxs-lookup"><span data-stu-id="7395a-286">**hello configuration setting for default and optimization is as follows:**</span></span>

| <span data-ttu-id="7395a-287">Параметры</span><span class="sxs-lookup"><span data-stu-id="7395a-287">Parameters</span></span> | <span data-ttu-id="7395a-288">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="7395a-288">Default</span></span> | <span data-ttu-id="7395a-289">Оптимизация</span><span class="sxs-lookup"><span data-stu-id="7395a-289">Optimization</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7395a-290">**innodb_buffer_pool_size**</span><span class="sxs-lookup"><span data-stu-id="7395a-290">**innodb_buffer_pool_size**</span></span> |<span data-ttu-id="7395a-291">None</span><span class="sxs-lookup"><span data-stu-id="7395a-291">None</span></span> |<span data-ttu-id="7395a-292">7 ГБ</span><span class="sxs-lookup"><span data-stu-id="7395a-292">7 GB</span></span> |
| <span data-ttu-id="7395a-293">**innodb_log_file_size**</span><span class="sxs-lookup"><span data-stu-id="7395a-293">**innodb_log_file_size**</span></span> |<span data-ttu-id="7395a-294">5 МБ</span><span class="sxs-lookup"><span data-stu-id="7395a-294">5 MB</span></span> |<span data-ttu-id="7395a-295">512 МБ</span><span class="sxs-lookup"><span data-stu-id="7395a-295">512 MB</span></span> |
| <span data-ttu-id="7395a-296">**max_connections**</span><span class="sxs-lookup"><span data-stu-id="7395a-296">**max_connections**</span></span> |<span data-ttu-id="7395a-297">100</span><span class="sxs-lookup"><span data-stu-id="7395a-297">100</span></span> |<span data-ttu-id="7395a-298">5000</span><span class="sxs-lookup"><span data-stu-id="7395a-298">5000</span></span> |
| <span data-ttu-id="7395a-299">**innodb_file_per_table**</span><span class="sxs-lookup"><span data-stu-id="7395a-299">**innodb_file_per_table**</span></span> |<span data-ttu-id="7395a-300">0</span><span class="sxs-lookup"><span data-stu-id="7395a-300">0</span></span> |<span data-ttu-id="7395a-301">1</span><span class="sxs-lookup"><span data-stu-id="7395a-301">1</span></span> |
| <span data-ttu-id="7395a-302">**innodb_flush_log_at_trx_commit**</span><span class="sxs-lookup"><span data-stu-id="7395a-302">**innodb_flush_log_at_trx_commit**</span></span> |<span data-ttu-id="7395a-303">1</span><span class="sxs-lookup"><span data-stu-id="7395a-303">1</span></span> |<span data-ttu-id="7395a-304">2</span><span class="sxs-lookup"><span data-stu-id="7395a-304">2</span></span> |
| <span data-ttu-id="7395a-305">**innodb_log_buffer_size**</span><span class="sxs-lookup"><span data-stu-id="7395a-305">**innodb_log_buffer_size**</span></span> |<span data-ttu-id="7395a-306">8 МБ</span><span class="sxs-lookup"><span data-stu-id="7395a-306">8 MB</span></span> |<span data-ttu-id="7395a-307">128 МБ</span><span class="sxs-lookup"><span data-stu-id="7395a-307">128 MB</span></span> |
| <span data-ttu-id="7395a-308">**query_cache_size**</span><span class="sxs-lookup"><span data-stu-id="7395a-308">**query_cache_size**</span></span> |<span data-ttu-id="7395a-309">16 МБ</span><span class="sxs-lookup"><span data-stu-id="7395a-309">16 MB</span></span> |<span data-ttu-id="7395a-310">0</span><span class="sxs-lookup"><span data-stu-id="7395a-310">0</span></span> |

<span data-ttu-id="7395a-311">Более подробные [параметров конфигурации оптимизации](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), см. toohello [MySQL официальный инструкции](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span><span class="sxs-lookup"><span data-stu-id="7395a-311">For more detailed [optimization configuration parameters](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), refer toohello [MySQL official instructions](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span></span>  

  <span data-ttu-id="7395a-312">**Тестовая среда**</span><span class="sxs-lookup"><span data-stu-id="7395a-312">**Test environment**</span></span>  

| <span data-ttu-id="7395a-313">Оборудование</span><span class="sxs-lookup"><span data-stu-id="7395a-313">Hardware</span></span> | <span data-ttu-id="7395a-314">Сведения</span><span class="sxs-lookup"><span data-stu-id="7395a-314">Details</span></span> |
| --- | --- |
| <span data-ttu-id="7395a-315">ЦП</span><span class="sxs-lookup"><span data-stu-id="7395a-315">CPU</span></span> |<span data-ttu-id="7395a-316">AMD Opteron(tm), процессор 4171 HE, 4 ядра</span><span class="sxs-lookup"><span data-stu-id="7395a-316">AMD Opteron(tm) Processor 4171 HE/4 cores</span></span> |
| <span data-ttu-id="7395a-317">Память</span><span class="sxs-lookup"><span data-stu-id="7395a-317">Memory</span></span> |<span data-ttu-id="7395a-318">14 ГБ</span><span class="sxs-lookup"><span data-stu-id="7395a-318">14 GB</span></span> |
| <span data-ttu-id="7395a-319">Диск</span><span class="sxs-lookup"><span data-stu-id="7395a-319">Disk</span></span> |<span data-ttu-id="7395a-320">10 ГБ на диск</span><span class="sxs-lookup"><span data-stu-id="7395a-320">10 GB/disk</span></span> |
| <span data-ttu-id="7395a-321">ОС</span><span class="sxs-lookup"><span data-stu-id="7395a-321">OS</span></span> |<span data-ttu-id="7395a-322">Ubuntu 14.04.1 LTS</span><span class="sxs-lookup"><span data-stu-id="7395a-322">Ubuntu 14.04.1 LTS</span></span> |

[1]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-01.png
[2]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-02.png
[3]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-03.png
[4]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-04.png
[5]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-05.png
[6]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-06.png
[7]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-07.png
[8]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-08.png
[9]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-09.png
[10]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-10.png
[11]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-11.png
[12]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-12.png
[13]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-13.png
[14]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-14.png

