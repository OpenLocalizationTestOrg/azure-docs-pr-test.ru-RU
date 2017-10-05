---
title: "Изменение имен устройств виртуальных машин Linux в Azure | Документация Майкрософт"
description: "В этом руководстве объясняется, почему изменяются имена устройств и предоставляются решения этой проблемы."
services: virtual-machines-linux
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: 
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 789f4580901a22dc3aaae9599c7205c76f268403
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a><span data-ttu-id="88735-103">Устранение неполадок. Изменение имен устройств виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="88735-103">Troubleshooting: Linux VM device names are changed</span></span>

<span data-ttu-id="88735-104">В этом руководстве описывается, почему изменяются имена устройств после перезапуска виртуальной машины Linux или после повторного подключения дисков.</span><span class="sxs-lookup"><span data-stu-id="88735-104">The article explains why device names are changed after you restart a Linux virtual machine (VM), or reattach the disks.</span></span> <span data-ttu-id="88735-105">В нем также предоставлены решения этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="88735-105">It also provides the solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="88735-106">Симптом</span><span class="sxs-lookup"><span data-stu-id="88735-106">Symptom</span></span>

<span data-ttu-id="88735-107">При выполнении виртуальных машин Linux в Microsoft Azure могут возникнуть следующие проблемы.</span><span class="sxs-lookup"><span data-stu-id="88735-107">You may experience the following problems when running Linux VMs in Microsoft Azure.</span></span>

- <span data-ttu-id="88735-108">После перезапуска виртуальная машина не загружается.</span><span class="sxs-lookup"><span data-stu-id="88735-108">The VM fails to boot after a restart.</span></span>

- <span data-ttu-id="88735-109">Если диски с данными отсоединить и присоединить повторно, имена дисков изменяются.</span><span class="sxs-lookup"><span data-stu-id="88735-109">If data disks are detached and reattached, the devices names for disks are changed.</span></span>

- <span data-ttu-id="88735-110">Приложение или скрипт, который ссылается на диск с использованием имени устройства, не работает.</span><span class="sxs-lookup"><span data-stu-id="88735-110">An application or script that references a disk by using device name fails.</span></span> <span data-ttu-id="88735-111">Вы обнаружите, что имя диска изменилось.</span><span class="sxs-lookup"><span data-stu-id="88735-111">You find that the device name of the disk is changed.</span></span>

## <a name="cause"></a><span data-ttu-id="88735-112">Причина:</span><span class="sxs-lookup"><span data-stu-id="88735-112">Cause</span></span>

<span data-ttu-id="88735-113">Пути устройств в Linux не обязательно будут согласованы после перезагрузок.</span><span class="sxs-lookup"><span data-stu-id="88735-113">Device paths in Linux are not guaranteed to be consistent across restarts.</span></span> <span data-ttu-id="88735-114">Имена устройств состоят из основного (буква) и дополнительного номеров.</span><span class="sxs-lookup"><span data-stu-id="88735-114">Device names consist of major (letter) and minor numbers.</span></span>  <span data-ttu-id="88735-115">Если драйвер устройства хранения Linux обнаруживает новое устройство, назначается основной и дополнительный номера из доступного диапазона.</span><span class="sxs-lookup"><span data-stu-id="88735-115">When the Linux storage device driver detects a new device, it assigns major and minor device numbers to it from the available range.</span></span> <span data-ttu-id="88735-116">При удалении устройства номера устройства освобождаются для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="88735-116">When a device is removed, the device numbers are freed to be reused later.</span></span>

<span data-ttu-id="88735-117">Проблема возникает, так как сканирование устройств в Linux, назначаемое подсистемой SCSI, происходит асинхронно.</span><span class="sxs-lookup"><span data-stu-id="88735-117">The problem occurs because the device scanning in Linux scheduled by the SCSI subsystem happens asynchronously.</span></span> <span data-ttu-id="88735-118">Окончательное именование пути устройства может различаться после перезагрузок.</span><span class="sxs-lookup"><span data-stu-id="88735-118">The final device path naming may vary across restarts.</span></span> 

## <a name="solution"></a><span data-ttu-id="88735-119">Решение</span><span class="sxs-lookup"><span data-stu-id="88735-119">Solution</span></span>

<span data-ttu-id="88735-120">Чтобы устранить эту проблему, используйте постоянное именование.</span><span class="sxs-lookup"><span data-stu-id="88735-120">To resolve this problem, use persistent naming.</span></span> <span data-ttu-id="88735-121">Существует четыре метода постоянного именования — метки файловой системы, UUID, идентификатор и путь.</span><span class="sxs-lookup"><span data-stu-id="88735-121">There are four methods to persistent naming - by filesystem label, by uuid, by id and by path.</span></span> <span data-ttu-id="88735-122">Для виртуальных машин Linux в Azure рекомендуется использовать методы меток файловой системы и UUID.</span><span class="sxs-lookup"><span data-stu-id="88735-122">We recommend the filesystem label and UUID methods for Azure Linux VMs.</span></span> 

<span data-ttu-id="88735-123">Большинство дистрибутивов также поддерживает параметры fstab **nofail** или **nobootwait**.</span><span class="sxs-lookup"><span data-stu-id="88735-123">Most distributions also provide either the **nofail** or **nobootwait** fstab options.</span></span> <span data-ttu-id="88735-124">Эти параметры позволяют системе загружаться, даже если диск не подключится во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="88735-124">These options enable a system to boot even if the disk fails to mount at startup.</span></span> <span data-ttu-id="88735-125">Дополнительные сведения об этих параметрах см. в документации дистрибутива.</span><span class="sxs-lookup"><span data-stu-id="88735-125">Check the distribution's documentation for more information about these parameters.</span></span> <span data-ttu-id="88735-126">Дополнительные сведения о настройке виртуальных машин Linux для использования UUID см. в разделе [Подключение к виртуальной машине Linux для подключения нового диска](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="88735-126">For more information about how to configure a Linux VM to use a UUID when you add a data disk, see [Connect to the Linux VM to mount the new disk](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> 

<span data-ttu-id="88735-127">После установки агента Azure Linux на виртуальной машине он использует правила Udev для формирования набора символических ссылок в каталоге **/dev/disk/azure**.</span><span class="sxs-lookup"><span data-stu-id="88735-127">When the Azure Linux agent is installed on a VM, it uses Udev rules to construct a set of symbolic links under **/dev/disk/azure**.</span></span> <span data-ttu-id="88735-128">Эти правила Udev могут использоваться приложениями и скриптами для идентификации дисков, подключенных к виртуальной машине, а также их типа и логического номера устройства (LUN).</span><span class="sxs-lookup"><span data-stu-id="88735-128">These Udev rules can be used by applications and scripts to identify disks are attached to the VM, their type, and the LUN.</span></span>

## <a name="more-information"></a><span data-ttu-id="88735-129">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="88735-129">More information</span></span>

### <a name="identify-disk-luns"></a><span data-ttu-id="88735-130">Определение LUN диска</span><span class="sxs-lookup"><span data-stu-id="88735-130">Identify disk LUNs</span></span>

<span data-ttu-id="88735-131">Приложение может использовать LUN, чтобы найти все присоединенные диски и создать символические ссылки.</span><span class="sxs-lookup"><span data-stu-id="88735-131">An application can use LUNs to find all the attached disks and constructing symbolic links.</span></span> <span data-ttu-id="88735-132">Агент Azure Linux содержит правила udev, с помощью которых настраиваются символические ссылки из LUN на устройства.</span><span class="sxs-lookup"><span data-stu-id="88735-132">The Azure Linux agent now includes udev rules that set up symbolic links from a LUN to the devices, as follows:</span></span>

    $ tree /dev/disk/azure

    /dev/disk/azure
    ├── resource -> ../../sdb
    ├── resource-part1 -> ../../sdb1
    ├── root -> ../../sda
    ├── root-part1 -> ../../sda1
    └── scsi1
        ├── lun0 -> ../../../sdc
        ├── lun0-part1 -> ../../../sdc1
        ├── lun1 -> ../../../sdd
        ├── lun1-part1 -> ../../../sdd1
        ├── lun1-part2 -> ../../../sdd2
        └── lun1-part3 -> ../../../sdd3                                    
                                 

<span data-ttu-id="88735-133">Также сведения о LUN можно получить с помощью гостевой виртуальной машины Linux, используя lsscsi или аналогичное средство следующим образом.</span><span class="sxs-lookup"><span data-stu-id="88735-133">LUN information can also be retrieved from the Linux guest using lsscsi or similar tool as follows.</span></span>

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

<span data-ttu-id="88735-134">Эти сведения о LUN гостевой машины можно использовать с метаданными подписки Azure, чтобы определить расположение виртуального жесткого диска, на котором хранятся данные раздела, в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="88735-134">This guest LUN information can be used with Azure subscription metadata to identify the location in Azure storage of the VHD which stores the partition data.</span></span> <span data-ttu-id="88735-135">Например, используйте командную строку Azure:</span><span class="sxs-lookup"><span data-stu-id="88735-135">For example, use the az cli:</span></span>

    $ az vm show --resource-group testVM --name testVM | jq -r .storageProfile.dataDisks                                        
    [                                                                                                                                                                  
    {                                                                                                                                                                  
    "caching": "None",                                                                                                                                              
      "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 1023,                                                                                                                                             
      "image": null,                                                                                                                                                   
    "lun": 0,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-114353",                                                                                                                    
    "vhd": {                                                                                                                                                          
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-114353.vhd"                                                       
    }                                                                                                                                                              
    },                                                                                                                                                                
    {                                                                                                                                                                   
    "caching": "None",                                                                                                                                               
    "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 512,                                                                                                                                              
    "image": null,                                                                                                                                                   
    "lun": 1,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-121516",                                                                                                                    
    "vhd": {                                                                                                                                                           
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-121516.vhd"                                                       
      }                                                                                                                                                             
      }                                                                                                                                                             
    ]

### <a name="discover-filesystem-uuids-by-using-blkid"></a><span data-ttu-id="88735-136">Обнаружение UUID файловой системы с помощью служебной программы blkid</span><span class="sxs-lookup"><span data-stu-id="88735-136">Discover filesystem UUIDs by using blkid</span></span>

<span data-ttu-id="88735-137">Выходные данные blkid или аналогичные источники данных можно прочитать с помощью скрипта либо приложения, чтобы сформировать символические ссылки в каталоге **/dev**.</span><span class="sxs-lookup"><span data-stu-id="88735-137">A script or application can read the output of blkid, or similar sources of information, and construct symbolic links in **/dev** for use.</span></span> <span data-ttu-id="88735-138">Выходные данные будут показывать UUID всех дисков, подключенных к виртуальной машине, и файл устройства, с которым они связаны:</span><span class="sxs-lookup"><span data-stu-id="88735-138">The output will show the UUIDs of all disks attached to the VM and the device file to which they are associated:</span></span>

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

<span data-ttu-id="88735-139">Правила udev waagent формируют набор символических ссылок в каталоге **/dev/disk/azure**:</span><span class="sxs-lookup"><span data-stu-id="88735-139">The waagent udev rules construct a set of symbolic links under **/dev/disk/azure**:</span></span>


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


<span data-ttu-id="88735-140">Приложение может использовать эти данные для идентификации загрузочного диска устройства и диска ресурсов (временного).</span><span class="sxs-lookup"><span data-stu-id="88735-140">The application can use this information identify the boot disk device and the resource (ephemeral) disk.</span></span> <span data-ttu-id="88735-141">В Azure для обнаружения этих разделов приложения должны ссылаться на **/dev/disk/azure/root-part1** или **/dev/disk/azure-resource-part1**.</span><span class="sxs-lookup"><span data-stu-id="88735-141">In Azure, applications should refer to **/dev/disk/azure/root-part1** or **/dev/disk/azure-resource-part1** to discover these partitions.</span></span>

<span data-ttu-id="88735-142">Если в списке blkid имеются дополнительные разделы, они находятся на диске данных.</span><span class="sxs-lookup"><span data-stu-id="88735-142">If there are additional partitions from the blkid list, they reside on a data disk.</span></span> <span data-ttu-id="88735-143">Приложения могут обрабатывать UUID для этих разделов и использовать путь, как например ниже, чтобы получить имя устройства в среде выполнения:</span><span class="sxs-lookup"><span data-stu-id="88735-143">Applications can maintain the UUID for these partitions and use a path like the below to discover the device name at runtime:</span></span>

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-the-latest-azure-storage-rules"></a><span data-ttu-id="88735-144">Получение последних правил хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="88735-144">Get the latest Azure storage rules</span></span>

<span data-ttu-id="88735-145">Чтобы получить последние правила хранилища Azure, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="88735-145">To the latest Azure storage rules, run th following commands:</span></span>

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


<span data-ttu-id="88735-146">Дополнительные сведения см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="88735-146">For more information, see the following articles:</span></span>

- <span data-ttu-id="88735-147">[Для Ubuntu: UsingUUID](https://help.ubuntu.com/community/UsingUUID) (Использование UUID)</span><span class="sxs-lookup"><span data-stu-id="88735-147">[Ubuntu: Using UUID](https://help.ubuntu.com/community/UsingUUID)</span></span>

- <span data-ttu-id="88735-148">[Для Red Hat: Persistent Naming](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html) (Постоянные именования)</span><span class="sxs-lookup"><span data-stu-id="88735-148">[Red Hat: Persistent Naming](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)</span></span>

- <span data-ttu-id="88735-149">[Для Linux: What UUIDs can do for you](https://www.linux.com/news/what-uuids-can-do-you) (Чем полезны идентификаторы UUID)</span><span class="sxs-lookup"><span data-stu-id="88735-149">[Linux: What UUIDs can do for you](https://www.linux.com/news/what-uuids-can-do-you)</span></span>

- <span data-ttu-id="88735-150">[Udev: Introduction to Device Management In Modern Linux System](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system) (Udev. Руководство по управлению устройствами в современной системе Linux)</span><span class="sxs-lookup"><span data-stu-id="88735-150">[Udev: Introduction to Device Management In Modern Linux System](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)</span></span>

