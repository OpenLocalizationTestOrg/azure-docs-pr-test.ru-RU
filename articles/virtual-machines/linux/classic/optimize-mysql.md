---
title: "Оптимизация производительности MySQL на ОС Linux | Документация Майкрософт"
description: "Узнайте, как оптимизировать MySQL в виртуальной машине Azure под управлением Linux."
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
ms.openlocfilehash: 8f2ec884fa98e989448ac11675e71f39aa21fa7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a><span data-ttu-id="c2230-103">Оптимизация производительности MySQL на виртуальных машинах Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="c2230-103">Optimize MySQL Performance on Azure Linux VMs</span></span>
<span data-ttu-id="c2230-104">Существует множество факторов, влияющих на производительность MySQL в Azure, которые зависят и от выбора виртуального оборудования, и от конфигурации программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="c2230-104">There are many factors that affect MySQL performance on Azure, both in virtual hardware selection and software configuration.</span></span> <span data-ttu-id="c2230-105">Эта статья посвящена оптимизации производительности с помощью конфигураций хранилища, системы и базы данных.</span><span class="sxs-lookup"><span data-stu-id="c2230-105">This article focuses on optimizing performance through storage, system, and database configurations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c2230-106">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager](../../../resource-manager-deployment-model.md) и классическая модель.</span><span class="sxs-lookup"><span data-stu-id="c2230-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="c2230-107">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="c2230-107">This article covers using the classic deployment model.</span></span> <span data-ttu-id="c2230-108">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c2230-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="c2230-109">Сведения об оптимизации виртуальных машин Linux с помощью модели Resource Manager см. в статье [Оптимизация виртуальной машины Linux в Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c2230-109">For information about Linux VM optimizations with the Resource Manager model, see [Optimize your Linux VM on Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="utilize-raid-on-an-azure-virtual-machine"></a><span data-ttu-id="c2230-110">Использование RAID на виртуальной машине Azure</span><span class="sxs-lookup"><span data-stu-id="c2230-110">Utilize RAID on an Azure virtual machine</span></span>
<span data-ttu-id="c2230-111">Хранилище — ключевой фактор, влияющий на производительность базы данных в облачных средах.</span><span class="sxs-lookup"><span data-stu-id="c2230-111">Storage is the key factor that affects database performance in cloud environments.</span></span> <span data-ttu-id="c2230-112">По сравнению с одним диском, RAID может обеспечить более быстрый доступ за счет параллелизма.</span><span class="sxs-lookup"><span data-stu-id="c2230-112">Compared to a single disk, RAID can provide faster access via concurrency.</span></span> <span data-ttu-id="c2230-113">Дополнительные сведения см. в описании [стандартных уровней RAID](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span><span class="sxs-lookup"><span data-stu-id="c2230-113">For more information, see [Standard RAID levels](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span></span>   

<span data-ttu-id="c2230-114">С помощью RAID в Azure можно существенно увеличить пропускную способность и время ответа для операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="c2230-114">Disk I/O throughput and I/O response time in Azure can be improved through RAID.</span></span> <span data-ttu-id="c2230-115">Наши лабораторные тесты показали, что при удвоении количества дисков RAID (с двух до четырех, с четырех до восьми и т. д.) удваивается пропускная способность ввода-вывода дисков, а время ответа операций ввода-вывода уменьшается в среднем в два раза.</span><span class="sxs-lookup"><span data-stu-id="c2230-115">Our lab tests show that disk I/O throughput can be doubled and I/O response time can be reduced by half on average when the number of RAID disks is doubled (from two to four, four to eight, etc.).</span></span> <span data-ttu-id="c2230-116">Дополнительные сведения см. в [приложении А](#AppendixA).</span><span class="sxs-lookup"><span data-stu-id="c2230-116">See [Appendix A](#AppendixA) for details.</span></span>  

<span data-ttu-id="c2230-117">Помимо дисковых операций ввода-вывода производительность MySQL увеличивается при увеличении уровня RAID.</span><span class="sxs-lookup"><span data-stu-id="c2230-117">In addition to disk I/O, MySQL performance improves when you increase the RAID level.</span></span>  <span data-ttu-id="c2230-118">Дополнительные сведения см. в [приложении Б](#AppendixB).</span><span class="sxs-lookup"><span data-stu-id="c2230-118">See [Appendix B](#AppendixB) for details.</span></span>  

<span data-ttu-id="c2230-119">Кроме того, вас может заинтересовать размер блоков.</span><span class="sxs-lookup"><span data-stu-id="c2230-119">You might also want to consider the chunk size.</span></span> <span data-ttu-id="c2230-120">Обычно чем больше размер блока, тем ниже нагрузка, особенно для объемных операций записи.</span><span class="sxs-lookup"><span data-stu-id="c2230-120">In general, when you have a larger chunk size, you get lower overhead, especially for large writes.</span></span> <span data-ttu-id="c2230-121">Но если размер блока слишком большой, это может привести к дополнительной нагрузке, которая нивелирует преимущества RAID.</span><span class="sxs-lookup"><span data-stu-id="c2230-121">However, when the chunk size is too large, it might add additional overhead that prevents you from taking advantage of RAID.</span></span> <span data-ttu-id="c2230-122">Текущий размер блоков по умолчанию — 512 КБ. Он является оптимальным для большинства рабочих сред.</span><span class="sxs-lookup"><span data-stu-id="c2230-122">The current default size is 512 KB, which is proven to be optimal for most general production environments.</span></span> <span data-ttu-id="c2230-123">Дополнительные сведения см. в [приложении В](#AppendixC).</span><span class="sxs-lookup"><span data-stu-id="c2230-123">See [Appendix C](#AppendixC) for details.</span></span>   

<span data-ttu-id="c2230-124">Для виртуальных машин разных типов существуют ограничения на количество дисков, которые можно добавить.</span><span class="sxs-lookup"><span data-stu-id="c2230-124">There are limits on how many disks you can add for different virtual machine types.</span></span> <span data-ttu-id="c2230-125">Эти ограничения описаны в статье [Размеры для облачных служб](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2230-125">These limits are detailed in [Virtual machine and cloud service sizes for Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span> <span data-ttu-id="c2230-126">Чтобы выполнить пример c RAID в этой статье, вам понадобится 4 подключенных диска данных, хотя вы можете настроить RAID и с меньшим количеством дисков.</span><span class="sxs-lookup"><span data-stu-id="c2230-126">You will need four attached data disks to follow the RAID example in this article, although you can choose to set up RAID with fewer disks.</span></span>  

<span data-ttu-id="c2230-127">В этой статье предполагается, что вы уже создали виртуальную машину Linux, а также установили и настроили MySQL.</span><span class="sxs-lookup"><span data-stu-id="c2230-127">This article assumes you have already created a Linux virtual machine and have MYSQL installed and configured.</span></span> <span data-ttu-id="c2230-128">Дополнительную информацию о начале работы см. в статье "Как установить MySQL в Azure".</span><span class="sxs-lookup"><span data-stu-id="c2230-128">For more information on getting started, see How to install MySQL on Azure.</span></span>  

### <a name="set-up-raid-on-azure"></a><span data-ttu-id="c2230-129">Настройка RAID в Azure</span><span class="sxs-lookup"><span data-stu-id="c2230-129">Set up RAID on Azure</span></span>
<span data-ttu-id="c2230-130">Ниже объясняется, как создать RAID в Azure с использованием портала Azure.</span><span class="sxs-lookup"><span data-stu-id="c2230-130">The following steps show how to create RAID on Azure by using the Azure portal.</span></span> <span data-ttu-id="c2230-131">RAID также можно настроить с помощью сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2230-131">You can also set up RAID by using Windows PowerShell scripts.</span></span>
<span data-ttu-id="c2230-132">В этом примере мы настроим RAID 0 с 4 дисками.</span><span class="sxs-lookup"><span data-stu-id="c2230-132">In this example, we will configure RAID 0 with four disks.</span></span>  

#### <a name="add-a-data-disk-to-your-virtual-machine"></a><span data-ttu-id="c2230-133">Добавление диска данных в виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="c2230-133">Add a data disk to your virtual machine</span></span>
<span data-ttu-id="c2230-134">На портале Azure перейдите к панели мониторинга и выберите виртуальную машину, к которой нужно добавить диск данных.</span><span class="sxs-lookup"><span data-stu-id="c2230-134">In the Azure portal, go to the dashboard and select the virtual machine to which you want to add a data disk.</span></span> <span data-ttu-id="c2230-135">В этом примере виртуальная машина — mysqlnode1.</span><span class="sxs-lookup"><span data-stu-id="c2230-135">In this example, the virtual machine is mysqlnode1.</span></span>  

<!--![Virtual machines][1]-->

<span data-ttu-id="c2230-136">Щелкните **Диски** и выберите **Подключить новый**.</span><span class="sxs-lookup"><span data-stu-id="c2230-136">Click **Disks** and then click **Attach New**.</span></span>

![Добавление дисков в виртуальную машину](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

<span data-ttu-id="c2230-138">Создайте новый диск объемом 500 ГБ.</span><span class="sxs-lookup"><span data-stu-id="c2230-138">Create a new 500 GB disk.</span></span> <span data-ttu-id="c2230-139">Для параметра **Настройки кэша узла** необходимо задать значение **Нет**.</span><span class="sxs-lookup"><span data-stu-id="c2230-139">Make sure that **Host Cache Preference** is set to **None**.</span></span>  <span data-ttu-id="c2230-140">Закончив, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c2230-140">When you're finished, click **OK**.</span></span>

![Присоединить пустой диск](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


<span data-ttu-id="c2230-142">Теперь вы добавили один пустой диск в виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="c2230-142">This adds one empty disk into your virtual machine.</span></span> <span data-ttu-id="c2230-143">Повторите этот шаг еще три раза, чтобы настроить четыре диска данных для RAID.</span><span class="sxs-lookup"><span data-stu-id="c2230-143">Repeat this step three more times so that you have four data disks for RAID.</span></span>  

<span data-ttu-id="c2230-144">Добавленные диски можно просмотреть в виртуальной машине, открыв журнал сообщений ядра.</span><span class="sxs-lookup"><span data-stu-id="c2230-144">You can see the added drives in the virtual machine by looking at the kernel message log.</span></span> <span data-ttu-id="c2230-145">Например, чтобы просмотреть этот журнал в Ubuntu, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c2230-145">For example, to see this on Ubuntu, use the following command:</span></span>  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-the-additional-disks"></a><span data-ttu-id="c2230-146">Создание RAID с дополнительными дисками</span><span class="sxs-lookup"><span data-stu-id="c2230-146">Create RAID with the additional disks</span></span>
<span data-ttu-id="c2230-147">Далее описано, как выполняется [Настройка программного RAID-массива в Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c2230-147">The following steps describe how to [configure software RAID on Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="c2230-148">Если вы используете файловую систему XFS, после создания RAID выполните следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="c2230-148">If you are using the XFS file system, execute the following steps after you have created RAID.</span></span>
>
>

<span data-ttu-id="c2230-149">Чтобы установить файловую систему XFS в ОС Debian, Ubuntu или Linux Mint, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c2230-149">To install XFS on Debian, Ubuntu, or Linux Mint, use the following command:</span></span>  

    apt-get -y install xfsprogs  

<span data-ttu-id="c2230-150">Чтобы установить файловую систему XFS для ОС Fedora, CentOS или RHEL, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c2230-150">To install XFS on Fedora, CentOS, or RHEL, use the following command:</span></span>  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a><span data-ttu-id="c2230-151">Настройка нового пути к хранилищу</span><span class="sxs-lookup"><span data-stu-id="c2230-151">Set up a new storage path</span></span>
<span data-ttu-id="c2230-152">Чтобы настроить новый путь к хранилищу, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c2230-152">Use the following command to set up a new storage path:</span></span>  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-the-original-data-to-the-new-storage-path"></a><span data-ttu-id="c2230-153">Копирование исходных данных в новый путь к хранилищу</span><span class="sxs-lookup"><span data-stu-id="c2230-153">Copy the original data to the new storage path</span></span>
<span data-ttu-id="c2230-154">Чтобы скопировать данные в новый путь к хранилищу, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c2230-154">Use the following command to copy data to the new storage path:</span></span>  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-the-data-disk"></a><span data-ttu-id="c2230-155">Изменение разрешений таким образом, чтобы MySQL могла получить доступ (на чтение и запись) к диску данных</span><span class="sxs-lookup"><span data-stu-id="c2230-155">Modify permissions so MySQL can access (read and write) the data disk</span></span>
<span data-ttu-id="c2230-156">Для изменения разрешений используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c2230-156">Use the following command to modify permissions:</span></span>  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-the-disk-io-scheduling-algorithm"></a><span data-ttu-id="c2230-157">Настройка алгоритма планирования дисковых операций ввода-вывода</span><span class="sxs-lookup"><span data-stu-id="c2230-157">Adjust the disk I/O scheduling algorithm</span></span>
<span data-ttu-id="c2230-158">В Linux реализовано четыре типа алгоритмов планирования операций ввода-вывода:</span><span class="sxs-lookup"><span data-stu-id="c2230-158">Linux implements four types of I/O scheduling algorithms:</span></span>  

* <span data-ttu-id="c2230-159">алгоритм NOOP (без операции);</span><span class="sxs-lookup"><span data-stu-id="c2230-159">NOOP algorithm (No Operation)</span></span>
* <span data-ttu-id="c2230-160">алгоритм крайнего срока (крайний срок);</span><span class="sxs-lookup"><span data-stu-id="c2230-160">Deadline algorithm (Deadline)</span></span>
* <span data-ttu-id="c2230-161">алгоритм организации полностью равноправных очередей (CFQ);</span><span class="sxs-lookup"><span data-stu-id="c2230-161">Completely fair queuing algorithm (CFQ)</span></span>
* <span data-ttu-id="c2230-162">алгоритм бюджетного периода (прогнозирование).</span><span class="sxs-lookup"><span data-stu-id="c2230-162">Budget period algorithm (Anticipatory)</span></span>  

<span data-ttu-id="c2230-163">Вы можете выбрать различные планировщики операций ввода-вывода с различными сценариями для оптимизации производительности.</span><span class="sxs-lookup"><span data-stu-id="c2230-163">You can select different I/O schedulers under different scenarios to optimize performance.</span></span> <span data-ttu-id="c2230-164">В среде с полностью произвольным порядком доступа производительность не зависит от используемого алгоритма: алгоритма равноправных очередей или алгоритма крайнего срока.</span><span class="sxs-lookup"><span data-stu-id="c2230-164">In a completely random access environment, there is not a significant difference between the CFQ and Deadline algorithms for performance.</span></span> <span data-ttu-id="c2230-165">Для среды базы данных MySQL мы рекомендуем алгоритм крайнего срока, поскольку он повышает стабильность.</span><span class="sxs-lookup"><span data-stu-id="c2230-165">We recommend that you set the MySQL database environment to Deadline for stability.</span></span> <span data-ttu-id="c2230-166">Если выполняется много последовательных операций ввода-вывода, метод равноправных очередей может снизить производительность дисковых операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="c2230-166">If there is a lot of sequential I/O, CFQ might reduce disk I/O performance.</span></span>   

<span data-ttu-id="c2230-167">Для твердотельных накопителей и некоторых других видов оборудования алгоритм NOOP или алгоритм крайнего срока обеспечивают более высокую производительность, чем планировщик по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c2230-167">For SSD and other equipment, NOOP or Deadline can achieve better performance than the default scheduler.</span></span>   

<span data-ttu-id="c2230-168">В ядре версий до 2.5 по умолчанию для операций ввода-вывода использовался алгоритм крайнего срока.</span><span class="sxs-lookup"><span data-stu-id="c2230-168">Prior to the kernel 2.5, the default I/O scheduling algorithm is Deadline.</span></span> <span data-ttu-id="c2230-169">Начиная с ядра 2.6.18 для планирования операций ввода-вывода по умолчанию используется алгоритм равноправных очередей.</span><span class="sxs-lookup"><span data-stu-id="c2230-169">Starting with the kernel 2.6.18, CFQ became the default I/O scheduling algorithm.</span></span>  <span data-ttu-id="c2230-170">Этот параметр можно указать при загрузке ядра или динамически изменять во время работы системы.</span><span class="sxs-lookup"><span data-stu-id="c2230-170">You can specify this setting at kernel boot time or dynamically modify this setting when the system is running.</span></span>  

<span data-ttu-id="c2230-171">Следующий пример для семейства дистрибутивов Debian демонстрирует, как узнать, какой используется планировщик, и установить в качестве планировщика по умолчанию алгоритм NOOP.</span><span class="sxs-lookup"><span data-stu-id="c2230-171">The following example demonstrates how to check and set the default scheduler to the NOOP algorithm in the Debian distribution family.</span></span>  

### <a name="view-the-current-io-scheduler"></a><span data-ttu-id="c2230-172">Просмотр текущего планировщика операций ввода-вывода</span><span class="sxs-lookup"><span data-stu-id="c2230-172">View the current I/O scheduler</span></span>
<span data-ttu-id="c2230-173">Чтобы узнать используемый планировщик, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c2230-173">To view the scheduler run the following command:</span></span>  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

<span data-ttu-id="c2230-174">Вы увидите следующий результат, который указывает тип текущего планировщика:</span><span class="sxs-lookup"><span data-stu-id="c2230-174">You will see following output, which indicates the current scheduler:</span></span>  

    noop [deadline] cfq


### <a name="change-the-current-device-devsda-of-the-io-scheduling-algorithm"></a><span data-ttu-id="c2230-175">Изменение текущего устройства (/dev/sda) для алгоритма планирования операций ввода-вывода</span><span class="sxs-lookup"><span data-stu-id="c2230-175">Change the current device (/dev/sda) of the I/O scheduling algorithm</span></span>
<span data-ttu-id="c2230-176">Выполните следующую команду, чтобы изменить текущее устройство:</span><span class="sxs-lookup"><span data-stu-id="c2230-176">Run the following commands to change the current device:</span></span>  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> <span data-ttu-id="c2230-177">Настраивать алгоритм только для устройства /dev/sda бесполезно.</span><span class="sxs-lookup"><span data-stu-id="c2230-177">Setting this for /dev/sda alone is not useful.</span></span> <span data-ttu-id="c2230-178">Его необходимо настроить для всех дисков данных, на которых расположена база данных.</span><span class="sxs-lookup"><span data-stu-id="c2230-178">It must be set on all data disks where the database resides.</span></span>  
>
>

<span data-ttu-id="c2230-179">Вы увидите следующий результат, означающий, что файл grub.cfg успешно перестроен и в качестве планировщика по умолчанию теперь используется алгоритм NOOP.</span><span class="sxs-lookup"><span data-stu-id="c2230-179">You should see the following output, indicating that grub.cfg has been rebuilt successfully and that the default scheduler has been updated to NOOP:</span></span>  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

<span data-ttu-id="c2230-180">Для семейства дистрибутивов Red Hat потребуется только одна команда:</span><span class="sxs-lookup"><span data-stu-id="c2230-180">For the Red Hat distribution family, you need only the following command:</span></span>

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a><span data-ttu-id="c2230-181">Настройка параметров операций системного файла</span><span class="sxs-lookup"><span data-stu-id="c2230-181">Configure system file operations settings</span></span>
<span data-ttu-id="c2230-182">Мы рекомендуем отключить функцию ведения журнала времени *atime* в файловой системе.</span><span class="sxs-lookup"><span data-stu-id="c2230-182">One best practice is to disable the *atime* logging feature on the file system.</span></span> <span data-ttu-id="c2230-183">Atime — время последнего доступа к файлу.</span><span class="sxs-lookup"><span data-stu-id="c2230-183">Atime is the last file access time.</span></span> <span data-ttu-id="c2230-184">При каждом обращении к файлу файловая система записывает метку времени в журнал.</span><span class="sxs-lookup"><span data-stu-id="c2230-184">Whenever a file is accessed, the file system records the timestamp in the log.</span></span> <span data-ttu-id="c2230-185">Однако эта информация используется редко.</span><span class="sxs-lookup"><span data-stu-id="c2230-185">However, this information is rarely used.</span></span> <span data-ttu-id="c2230-186">При необходимости эту функцию можно отключить, что позволит уменьшить общее время доступа к диску.</span><span class="sxs-lookup"><span data-stu-id="c2230-186">You can disable it if you don't need it, which will reduce overall disk access time.</span></span>  

<span data-ttu-id="c2230-187">Для этого следует изменить файл конфигурации файловой системы /etc/fstab и добавить параметр **noatime** .</span><span class="sxs-lookup"><span data-stu-id="c2230-187">To disable atime logging, you need to modify the file system configuration file /etc/ fstab and add the **noatime** option.</span></span>  

<span data-ttu-id="c2230-188">Например, добавьте в файл vim /etc/fstab параметр noatime, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="c2230-188">For example, edit the vim /etc/fstab file, adding the noatime as shown in the following sample:</span></span>  

    # CLOUD_IMG: This file was created/modified by the Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add the “noatime” option below to disable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

<span data-ttu-id="c2230-189">Затем подключите файловую систему заново с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="c2230-189">Then, remount the file system with the following command:</span></span>  

    mount -o remount /RAID0

<span data-ttu-id="c2230-190">Проверьте измененный результат.</span><span class="sxs-lookup"><span data-stu-id="c2230-190">Test the modified result.</span></span> <span data-ttu-id="c2230-191">Теперь при изменении файла время доступа не обновляется.</span><span class="sxs-lookup"><span data-stu-id="c2230-191">When you modify the test file, the access time is not updated.</span></span> <span data-ttu-id="c2230-192">В следующих примерах представлен код до и после изменения.</span><span class="sxs-lookup"><span data-stu-id="c2230-192">The following examples show what the code looks like before and after modification.</span></span>

<span data-ttu-id="c2230-193">До:</span><span class="sxs-lookup"><span data-stu-id="c2230-193">Before:</span></span>        

![Код до внесения изменений][5]

<span data-ttu-id="c2230-195">После:</span><span class="sxs-lookup"><span data-stu-id="c2230-195">After:</span></span>

![Код после внесения изменений][6]

## <a name="increase-the-maximum-number-of-system-handles-for-high-concurrency"></a><span data-ttu-id="c2230-197">Увеличение максимального количества системных дескрипторов для увеличения степени параллелизма</span><span class="sxs-lookup"><span data-stu-id="c2230-197">Increase the maximum number of system handles for high concurrency</span></span>
<span data-ttu-id="c2230-198">MySQL — база данных с высокой степенью параллелизма.</span><span class="sxs-lookup"><span data-stu-id="c2230-198">MySQL is a high concurrency database.</span></span> <span data-ttu-id="c2230-199">Количество параллельных дескрипторов по умолчанию для Linux — 1024. Однако их не всегда достаточно.</span><span class="sxs-lookup"><span data-stu-id="c2230-199">The default number of concurrent handles is 1024 for Linux, which is not always sufficient.</span></span> <span data-ttu-id="c2230-200">Выполните следующие шаги, чтобы увеличить максимальное количество параллельных дескрипторов системы для поддержки высокой степени параллелизма MySQL.</span><span class="sxs-lookup"><span data-stu-id="c2230-200">Use the following steps to increase the maximum concurrent handles of the system to support high concurrency of MySQL.</span></span>

### <a name="modify-the-limitsconf-file"></a><span data-ttu-id="c2230-201">Изменение файла limits.conf</span><span class="sxs-lookup"><span data-stu-id="c2230-201">Modify the limits.conf file</span></span>
<span data-ttu-id="c2230-202">Чтобы увеличить максимально допустимое количество параллельных дескрипторов, добавьте следующие четыре строки в файл /etc/security/limits.conf.</span><span class="sxs-lookup"><span data-stu-id="c2230-202">To increase the maximum allowed concurrent handles, add the following four lines in the /etc/security/limits.conf file.</span></span> <span data-ttu-id="c2230-203">Обратите внимание, что максимальное количество, поддерживаемое системой, — 65536.</span><span class="sxs-lookup"><span data-stu-id="c2230-203">Note that 65536 is the maximum number that the system can support.</span></span>   

    * <span data-ttu-id="c2230-204">soft nofile 65536</span><span class="sxs-lookup"><span data-stu-id="c2230-204">soft nofile 65536</span></span>
    * <span data-ttu-id="c2230-205">hard nofile 65536</span><span class="sxs-lookup"><span data-stu-id="c2230-205">hard nofile 65536</span></span>
    * <span data-ttu-id="c2230-206">soft nproc 65536</span><span class="sxs-lookup"><span data-stu-id="c2230-206">soft nproc 65536</span></span>
    * <span data-ttu-id="c2230-207">hard nproc 65536</span><span class="sxs-lookup"><span data-stu-id="c2230-207">hard nproc 65536</span></span>

### <a name="update-the-system-for-the-new-limits"></a><span data-ttu-id="c2230-208">Обновление операционной системы для новых ограничений</span><span class="sxs-lookup"><span data-stu-id="c2230-208">Update the system for the new limits</span></span>
<span data-ttu-id="c2230-209">Для обновления системы выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="c2230-209">To update the system, run the following commands:</span></span>  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-the-limits-are-updated-at-boot-time"></a><span data-ttu-id="c2230-210">Обеспечение обновления ограничений при загрузке</span><span class="sxs-lookup"><span data-stu-id="c2230-210">Ensure that the limits are updated at boot time</span></span>
<span data-ttu-id="c2230-211">Вставьте следующие команды в файл /etc/rc.local, чтобы они выполнялись при каждой загрузке.</span><span class="sxs-lookup"><span data-stu-id="c2230-211">Put the following startup commands in the /etc/rc.local file so it will take effect at boot time.</span></span>  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a><span data-ttu-id="c2230-212">Оптимизация базы данных MySQL</span><span class="sxs-lookup"><span data-stu-id="c2230-212">MySQL database optimization</span></span>
<span data-ttu-id="c2230-213">При настройке MySQL в Azure можно использовать те же методы повышения производительности, что и на локальной машине.</span><span class="sxs-lookup"><span data-stu-id="c2230-213">To configure MySQL on Azure, you can use the same performance-tuning strategy you use on an on-premises machine.</span></span>  

<span data-ttu-id="c2230-214">Основные правила оптимизации операций ввода-вывода:</span><span class="sxs-lookup"><span data-stu-id="c2230-214">The main I/O optimization rules are:</span></span>   

* <span data-ttu-id="c2230-215">увеличьте размер кэша;</span><span class="sxs-lookup"><span data-stu-id="c2230-215">Increase the cache size.</span></span>
* <span data-ttu-id="c2230-216">уменьшите время ответа при выполнении операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="c2230-216">Reduce I/O response time.</span></span>  

<span data-ttu-id="c2230-217">Чтобы оптимизировать параметры сервера MySQL, можно обновить файл my.cnf, который является файлом конфигурации по умолчанию для серверных и клиентских компьютеров.</span><span class="sxs-lookup"><span data-stu-id="c2230-217">To optimize MySQL server settings, you can update the my.cnf file, which is the default configuration file for both server and client computers.</span></span>  

<span data-ttu-id="c2230-218">Следующие элементы конфигурации являются основными факторами, влияющими на производительность MySQL.</span><span class="sxs-lookup"><span data-stu-id="c2230-218">The following configuration items are the main factors that affect MySQL performance:</span></span>  

* <span data-ttu-id="c2230-219">**innodb_buffer_pool_size**. Буферный пул содержит буферизованные данные и индекс.</span><span class="sxs-lookup"><span data-stu-id="c2230-219">**innodb_buffer_pool_size**: The buffer pool contains buffered data and the index.</span></span> <span data-ttu-id="c2230-220">Обычно для этого параметра задается значение, равное 70 % объема физической памяти.</span><span class="sxs-lookup"><span data-stu-id="c2230-220">This is usually set to 70 percent of physical memory.</span></span>
* <span data-ttu-id="c2230-221">**innodb_log_file_size**. Это размер журнала повторяемых операций.</span><span class="sxs-lookup"><span data-stu-id="c2230-221">**innodb_log_file_size**: This is the redo log size.</span></span> <span data-ttu-id="c2230-222">Журналы повторяемых операций используются, чтобы обеспечить высокую скорость, надежность и возможность восстановления операций записи после сбоя.</span><span class="sxs-lookup"><span data-stu-id="c2230-222">You use redo logs to ensure that write operations are fast, reliable, and recoverable after a crash.</span></span> <span data-ttu-id="c2230-223">Для этого параметра задается значение 512 МБ, что обеспечит достаточно места для ведения журнала операций записи.</span><span class="sxs-lookup"><span data-stu-id="c2230-223">This is set to 512 MB, which will give you plenty of space for logging write operations.</span></span>
* <span data-ttu-id="c2230-224">**max_connections**. Иногда приложения не закрывают подключения должным образом.</span><span class="sxs-lookup"><span data-stu-id="c2230-224">**max_connections**: Sometimes applications do not close connections properly.</span></span> <span data-ttu-id="c2230-225">Если установить большее значение, у сервера будет больше времени для очистки неактивных подключений.</span><span class="sxs-lookup"><span data-stu-id="c2230-225">A larger value will give the server more time to recycle idled connections.</span></span> <span data-ttu-id="c2230-226">Максимально возможное количество подключений — 10 000, но мы рекомендуем ограничить его до 5000.</span><span class="sxs-lookup"><span data-stu-id="c2230-226">The maximum number of connections is 10,000, but the recommended maximum is 5,000.</span></span>
* <span data-ttu-id="c2230-227">**Innodb_file_per_table**. Этот параметр позволяет включить или отключить возможность InnoDB сохранять таблицы в отдельных файлах.</span><span class="sxs-lookup"><span data-stu-id="c2230-227">**Innodb_file_per_table**: This setting enables or disables the ability of InnoDB to store tables in separate files.</span></span> <span data-ttu-id="c2230-228">Если включить этот параметр, вы сможете эффективно применять некоторые расширенные функции администрирования.</span><span class="sxs-lookup"><span data-stu-id="c2230-228">Turn on the option to ensure that several advanced administration operations can be applied efficiently.</span></span> <span data-ttu-id="c2230-229">С точки зрения производительности это позволит ускорить передачу табличного пространства и оптимизировать управление мусором.</span><span class="sxs-lookup"><span data-stu-id="c2230-229">From a performance point of view, it can speed up the table space transmission and optimize the debris management performance.</span></span> <span data-ttu-id="c2230-230">Рекомендуемое значение для этого параметра — ON.</span><span class="sxs-lookup"><span data-stu-id="c2230-230">The recommended setting for this option is ON.</span></span></br></br>
<span data-ttu-id="c2230-231">Начиная с версии MySQL 5.6 по умолчанию устанавливается значение ON, поэтому дополнительных действий не требуется.</span><span class="sxs-lookup"><span data-stu-id="c2230-231">From MySQL 5.6, the default setting is ON, so no action is required.</span></span> <span data-ttu-id="c2230-232">В более ранних версиях этот параметр по умолчанию отключен.</span><span class="sxs-lookup"><span data-stu-id="c2230-232">For earlier versions, the default setting is OFF.</span></span> <span data-ttu-id="c2230-233">Его необходимо изменить прежде, чем загружать данные, поскольку его значение влияет только на новые таблицы.</span><span class="sxs-lookup"><span data-stu-id="c2230-233">The setting should be changed before data is loaded, because only newly created tables are affected.</span></span>
* <span data-ttu-id="c2230-234">**innodb_flush_log_at_trx_commit**. По умолчанию установлено значение 1. Допустимый диапазон значений — от 0 до 2.</span><span class="sxs-lookup"><span data-stu-id="c2230-234">**innodb_flush_log_at_trx_commit**: The default value is 1, with the scope set to 0~2.</span></span> <span data-ttu-id="c2230-235">Значение по умолчанию — наиболее подходящий вариант для автономной базы данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="c2230-235">The default value is the most suitable option for standalone MySQL DB.</span></span> <span data-ttu-id="c2230-236">При установке значения 2 достигается наибольший уровень целостности данных. Это значение подходит для главного узла в кластере MySQL.</span><span class="sxs-lookup"><span data-stu-id="c2230-236">The setting of 2 enables the most data integrity and is suitable for Master in MySQL Cluster.</span></span> <span data-ttu-id="c2230-237">При установке значения 0 допускается потеря данных, которая может повлиять на надежность и в некоторых случаях увеличить производительность. Это значение подходит для подчиненного узла в кластере MySQL.</span><span class="sxs-lookup"><span data-stu-id="c2230-237">The setting of 0 allows data loss, which can affect reliability (in some cases with better performance), and is suitable for Slave in MySQL Cluster.</span></span>
* <span data-ttu-id="c2230-238">**Innodb_log_buffer_size**. Буфер журнала позволяет выполнять транзакции без необходимости записи журнала на диск до их фиксации.</span><span class="sxs-lookup"><span data-stu-id="c2230-238">**Innodb_log_buffer_size**: The log buffer allows transactions to run without having to flush the log to disk before the transactions commit.</span></span> <span data-ttu-id="c2230-239">Однако при работе с большим двоичным объектом или текстовым полем кэш будет быстро заполняться, что увеличит частоту дисковых операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="c2230-239">However, if there is large binary object or text field, the cache will be consumed quickly and frequent disk I/O will be triggered.</span></span> <span data-ttu-id="c2230-240">Лучше увеличить размер буфера, если для переменной состояния Innodb_log_waits установлено значение, отличное от 0.</span><span class="sxs-lookup"><span data-stu-id="c2230-240">It is better increase the buffer size if Innodb_log_waits state variable is not 0.</span></span>
* <span data-ttu-id="c2230-241">**query_cache_size**. Лучше всего сразу отключить его.</span><span class="sxs-lookup"><span data-stu-id="c2230-241">**query_cache_size**: The best option is to disable it from the outset.</span></span> <span data-ttu-id="c2230-242">Установите для параметра query_cache_size значение 0 (начиная с MySQL 5.6 это значение используется по умолчанию) и используйте другие методы для ускорения запросов.</span><span class="sxs-lookup"><span data-stu-id="c2230-242">Set query_cache_size to 0 (this is the default setting in MySQL 5.6) and use other methods to speed up queries.</span></span>  

<span data-ttu-id="c2230-243">В [приложении Г](#AppendixD) вы найдете сравнение производительности до и после оптимизации.</span><span class="sxs-lookup"><span data-stu-id="c2230-243">See [Appendix D](#AppendixD) for a comparison of performance before and after the optimization.</span></span>

## <a name="turn-on-the-mysql-slow-query-log-for-analyzing-the-performance-bottleneck"></a><span data-ttu-id="c2230-244">Включение журнала медленных запросов MySQL для анализа узкого места производительности</span><span class="sxs-lookup"><span data-stu-id="c2230-244">Turn on the MySQL slow query log for analyzing the performance bottleneck</span></span>
<span data-ttu-id="c2230-245">Журнал медленных запросов MySQL может помочь вам определить медленные запросы в MySQL.</span><span class="sxs-lookup"><span data-stu-id="c2230-245">The MySQL slow query log can help you identify the slow queries for MySQL.</span></span> <span data-ttu-id="c2230-246">После включения этого механизма вы можете использовать инструменты MySQL, такие как **mysqldumpslow** , для определения узкого места производительности.</span><span class="sxs-lookup"><span data-stu-id="c2230-246">After enabling the MySQL slow query log, you can use MySQL tools like **mysqldumpslow** to identify the performance bottleneck.</span></span>  

<span data-ttu-id="c2230-247">По умолчанию он отключен.</span><span class="sxs-lookup"><span data-stu-id="c2230-247">By default, this is not enabled.</span></span> <span data-ttu-id="c2230-248">Если включить ведение журнала медленных запросов, может немного увеличиться нагрузка на ЦП.</span><span class="sxs-lookup"><span data-stu-id="c2230-248">Turning on the slow query log might consume some CPU resources.</span></span> <span data-ttu-id="c2230-249">Мы рекомендуем включать его ненадолго, только для устранения узких мест производительности.</span><span class="sxs-lookup"><span data-stu-id="c2230-249">We recommend that you enable this temporarily for troubleshooting performance bottlenecks.</span></span> <span data-ttu-id="c2230-250">Включение журнала медленных запросов:</span><span class="sxs-lookup"><span data-stu-id="c2230-250">To turn on the slow query log:</span></span>

1. <span data-ttu-id="c2230-251">Измените файл my.cnf, добавив в его конец следующие строки:</span><span class="sxs-lookup"><span data-stu-id="c2230-251">Modify the my.cnf file by adding the following lines to the end:</span></span>

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. <span data-ttu-id="c2230-252">Перезапустите сервер MySQL.</span><span class="sxs-lookup"><span data-stu-id="c2230-252">Restart the MySQL server.</span></span>

        service  mysql  restart

3. <span data-ttu-id="c2230-253">С помощью команды **show** проверьте, действуют ли изменения настроек.</span><span class="sxs-lookup"><span data-stu-id="c2230-253">Check whether the setting is taking effect by using the **show** command.</span></span>

![Включение Slow-query-log][7]   

![Результаты Slow-query-log][8]

<span data-ttu-id="c2230-256">В этом примере видно, что функция медленных запросов включена.</span><span class="sxs-lookup"><span data-stu-id="c2230-256">In this example, you can see that the slow query feature has been turned on.</span></span> <span data-ttu-id="c2230-257">Затем можно использовать инструмент **mysqldumpslow** , чтобы определить узкие места производительности и оптимизировать ее (например, путем добавления индексов).</span><span class="sxs-lookup"><span data-stu-id="c2230-257">You can then use the **mysqldumpslow** tool to determine performance bottlenecks and optimize performance, such as adding indexes.</span></span>

## <a name="appendices"></a><span data-ttu-id="c2230-258">Приложения</span><span class="sxs-lookup"><span data-stu-id="c2230-258">Appendices</span></span>
<span data-ttu-id="c2230-259">Здесь приводятся результаты теста производительности, выполненного в целевой лабораторной среде.</span><span class="sxs-lookup"><span data-stu-id="c2230-259">The following are sample performance test data produced in a targeted lab environment.</span></span> <span data-ttu-id="c2230-260">Они предоставляют обобщенную информацию по эффективности разных стратегий повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="c2230-260">They provide general background on the performance data trend with different performance tuning approaches.</span></span> <span data-ttu-id="c2230-261">Результаты могут отличаться для разных сред и версий продукта.</span><span class="sxs-lookup"><span data-stu-id="c2230-261">The results might vary under different environment or product versions.</span></span>

### <span data-ttu-id="c2230-262"><a name="AppendixA"></a>Приложение А</span><span class="sxs-lookup"><span data-stu-id="c2230-262"><a name="AppendixA"></a>Appendix A</span></span>  
<span data-ttu-id="c2230-263">**Производительность диска (количество операций ввода-вывода в секунду) с разными уровнями RAID**</span><span class="sxs-lookup"><span data-stu-id="c2230-263">**Disk performance (IOPS) with different RAID levels**</span></span>

![Количество операций ввода-вывода в секунду с разными уровнями RAID][9]

<span data-ttu-id="c2230-265">**Команды тестирования**</span><span class="sxs-lookup"><span data-stu-id="c2230-265">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> <span data-ttu-id="c2230-266">В рабочей нагрузке этого теста используется 64 потока в попытке достичь верхнее предельное значение RAID.</span><span class="sxs-lookup"><span data-stu-id="c2230-266">The workload of this test uses 64 threads, trying to reach the upper limit of RAID.</span></span>
>
>

### <span data-ttu-id="c2230-267"><a name="AppendixB"></a>Приложение Б</span><span class="sxs-lookup"><span data-stu-id="c2230-267"><a name="AppendixB"></a>Appendix B</span></span>  
<span data-ttu-id="c2230-268">**Сравнение производительности (пропускной способности) MySQL с разными уровнями RAID** </span><span class="sxs-lookup"><span data-stu-id="c2230-268">**MySQL performance (throughput) comparison with different RAID levels** </span></span>  
<span data-ttu-id="c2230-269">(Файловая система XFS)</span><span class="sxs-lookup"><span data-stu-id="c2230-269">(XFS file system)</span></span>

![Сравнение производительности MySQL с разными уровнями RAID][10]  
![Сравнение производительности MySQL с разными уровнями RAID][11]

<span data-ttu-id="c2230-272">**Команды тестирования**</span><span class="sxs-lookup"><span data-stu-id="c2230-272">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

<span data-ttu-id="c2230-273">**Сравнение производительности (OLTP) MySQL с разными уровнями RAID**</span><span class="sxs-lookup"><span data-stu-id="c2230-273">**MySQL performance (OLTP) comparison with different RAID levels**</span></span>  
<span data-ttu-id="c2230-274">![Сравнение производительности (OLTP) MySQL с разными уровнями RAID][12]</span><span class="sxs-lookup"><span data-stu-id="c2230-274">![MySQL performance (OLTP) comparison with different RAID levels][12]</span></span>

<span data-ttu-id="c2230-275">**Команды тестирования**</span><span class="sxs-lookup"><span data-stu-id="c2230-275">**Test commands**</span></span>

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <span data-ttu-id="c2230-276"><a name="AppendixC"></a>Приложение В</span><span class="sxs-lookup"><span data-stu-id="c2230-276"><a name="AppendixC"></a>Appendix C</span></span>   
<span data-ttu-id="c2230-277">**Сравнение производительности диска (количества операций ввода-вывода в секунду) для разного размера блоков**</span><span class="sxs-lookup"><span data-stu-id="c2230-277">**Disk performance (IOPS) comparison for different chunk sizes**</span></span>  
<span data-ttu-id="c2230-278">(Файловая система XFS)</span><span class="sxs-lookup"><span data-stu-id="c2230-278">(XFS file system)</span></span>

![][13]

<span data-ttu-id="c2230-279">**Команды тестирования**</span><span class="sxs-lookup"><span data-stu-id="c2230-279">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

<span data-ttu-id="c2230-280">Для этого теста использовались файлы размером 30 ГБ и 1 ГБ и файловая система XFS с RAID 0 (4 диска).</span><span class="sxs-lookup"><span data-stu-id="c2230-280">The file sizes used for this testing are 30 GB and 1 GB, respectively, with RAID 0 (4 disks) XFS file system.</span></span>

### <span data-ttu-id="c2230-281"><a name="AppendixD"></a>Приложение Г</span><span class="sxs-lookup"><span data-stu-id="c2230-281"><a name="AppendixD"></a>Appendix D</span></span>  
<span data-ttu-id="c2230-282">**Сравнение производительности (пропускной способности) MySQL до и после оптимизации**</span><span class="sxs-lookup"><span data-stu-id="c2230-282">**MySQL performance (throughput) comparison before and after optimization**</span></span>  
<span data-ttu-id="c2230-283">(Файловая система XFS)</span><span class="sxs-lookup"><span data-stu-id="c2230-283">(XFS File System)</span></span>

![Сравнение производительности (пропускной способности) MySQL до и после оптимизации][14]

<span data-ttu-id="c2230-285">**Команды тестирования**</span><span class="sxs-lookup"><span data-stu-id="c2230-285">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

<span data-ttu-id="c2230-286">**Значения параметров конфигурации по умолчанию и для оптимизации выглядят следующим образом.**</span><span class="sxs-lookup"><span data-stu-id="c2230-286">**The configuration setting for default and optimization is as follows:**</span></span>

| <span data-ttu-id="c2230-287">Параметры</span><span class="sxs-lookup"><span data-stu-id="c2230-287">Parameters</span></span> | <span data-ttu-id="c2230-288">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="c2230-288">Default</span></span> | <span data-ttu-id="c2230-289">Оптимизация</span><span class="sxs-lookup"><span data-stu-id="c2230-289">Optimization</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c2230-290">**innodb_buffer_pool_size**</span><span class="sxs-lookup"><span data-stu-id="c2230-290">**innodb_buffer_pool_size**</span></span> |<span data-ttu-id="c2230-291">None</span><span class="sxs-lookup"><span data-stu-id="c2230-291">None</span></span> |<span data-ttu-id="c2230-292">7 ГБ</span><span class="sxs-lookup"><span data-stu-id="c2230-292">7 GB</span></span> |
| <span data-ttu-id="c2230-293">**innodb_log_file_size**</span><span class="sxs-lookup"><span data-stu-id="c2230-293">**innodb_log_file_size**</span></span> |<span data-ttu-id="c2230-294">5 МБ</span><span class="sxs-lookup"><span data-stu-id="c2230-294">5 MB</span></span> |<span data-ttu-id="c2230-295">512 МБ</span><span class="sxs-lookup"><span data-stu-id="c2230-295">512 MB</span></span> |
| <span data-ttu-id="c2230-296">**max_connections**</span><span class="sxs-lookup"><span data-stu-id="c2230-296">**max_connections**</span></span> |<span data-ttu-id="c2230-297">100</span><span class="sxs-lookup"><span data-stu-id="c2230-297">100</span></span> |<span data-ttu-id="c2230-298">5000</span><span class="sxs-lookup"><span data-stu-id="c2230-298">5000</span></span> |
| <span data-ttu-id="c2230-299">**innodb_file_per_table**</span><span class="sxs-lookup"><span data-stu-id="c2230-299">**innodb_file_per_table**</span></span> |<span data-ttu-id="c2230-300">0</span><span class="sxs-lookup"><span data-stu-id="c2230-300">0</span></span> |<span data-ttu-id="c2230-301">1</span><span class="sxs-lookup"><span data-stu-id="c2230-301">1</span></span> |
| <span data-ttu-id="c2230-302">**innodb_flush_log_at_trx_commit**</span><span class="sxs-lookup"><span data-stu-id="c2230-302">**innodb_flush_log_at_trx_commit**</span></span> |<span data-ttu-id="c2230-303">1</span><span class="sxs-lookup"><span data-stu-id="c2230-303">1</span></span> |<span data-ttu-id="c2230-304">2</span><span class="sxs-lookup"><span data-stu-id="c2230-304">2</span></span> |
| <span data-ttu-id="c2230-305">**innodb_log_buffer_size**</span><span class="sxs-lookup"><span data-stu-id="c2230-305">**innodb_log_buffer_size**</span></span> |<span data-ttu-id="c2230-306">8 МБ</span><span class="sxs-lookup"><span data-stu-id="c2230-306">8 MB</span></span> |<span data-ttu-id="c2230-307">128 МБ</span><span class="sxs-lookup"><span data-stu-id="c2230-307">128 MB</span></span> |
| <span data-ttu-id="c2230-308">**query_cache_size**</span><span class="sxs-lookup"><span data-stu-id="c2230-308">**query_cache_size**</span></span> |<span data-ttu-id="c2230-309">16 МБ</span><span class="sxs-lookup"><span data-stu-id="c2230-309">16 MB</span></span> |<span data-ttu-id="c2230-310">0</span><span class="sxs-lookup"><span data-stu-id="c2230-310">0</span></span> |

<span data-ttu-id="c2230-311">Дополнительную информацию о [параметрах конфигурации для оптимизации](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html) см. в [официальной документации MySQL](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span><span class="sxs-lookup"><span data-stu-id="c2230-311">For more detailed [optimization configuration parameters](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), refer to the [MySQL official instructions](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span></span>  

  <span data-ttu-id="c2230-312">**Тестовая среда**</span><span class="sxs-lookup"><span data-stu-id="c2230-312">**Test environment**</span></span>  

| <span data-ttu-id="c2230-313">Оборудование</span><span class="sxs-lookup"><span data-stu-id="c2230-313">Hardware</span></span> | <span data-ttu-id="c2230-314">Сведения</span><span class="sxs-lookup"><span data-stu-id="c2230-314">Details</span></span> |
| --- | --- |
| <span data-ttu-id="c2230-315">ЦП</span><span class="sxs-lookup"><span data-stu-id="c2230-315">CPU</span></span> |<span data-ttu-id="c2230-316">AMD Opteron(tm), процессор 4171 HE, 4 ядра</span><span class="sxs-lookup"><span data-stu-id="c2230-316">AMD Opteron(tm) Processor 4171 HE/4 cores</span></span> |
| <span data-ttu-id="c2230-317">Память</span><span class="sxs-lookup"><span data-stu-id="c2230-317">Memory</span></span> |<span data-ttu-id="c2230-318">14 ГБ</span><span class="sxs-lookup"><span data-stu-id="c2230-318">14 GB</span></span> |
| <span data-ttu-id="c2230-319">Диск</span><span class="sxs-lookup"><span data-stu-id="c2230-319">Disk</span></span> |<span data-ttu-id="c2230-320">10 ГБ на диск</span><span class="sxs-lookup"><span data-stu-id="c2230-320">10 GB/disk</span></span> |
| <span data-ttu-id="c2230-321">ОС</span><span class="sxs-lookup"><span data-stu-id="c2230-321">OS</span></span> |<span data-ttu-id="c2230-322">Ubuntu 14.04.1 LTS</span><span class="sxs-lookup"><span data-stu-id="c2230-322">Ubuntu 14.04.1 LTS</span></span> |

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

