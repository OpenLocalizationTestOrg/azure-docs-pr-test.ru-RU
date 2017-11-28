---
title: "имена устройств виртуальной Машины aaaLinux изменяются в Azure | Документы Microsoft"
description: "Описание hello, почему имена устройств были изменены и предоставления решения для этой проблемы."
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
ms.openlocfilehash: 4d3a5853d61edd2c8e8b85ab69e5ed3b3bc00bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a><span data-ttu-id="c8e2a-103">Устранение неполадок. Изменение имен устройств виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="c8e2a-103">Troubleshooting: Linux VM device names are changed</span></span>

<span data-ttu-id="c8e2a-104">Hello статье объясняется, почему были изменены имена устройств после перезапуска виртуальной машины (VM) Linux или заново присоединить диски hello.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-104">hello article explains why device names are changed after you restart a Linux virtual machine (VM), or reattach hello disks.</span></span> <span data-ttu-id="c8e2a-105">Он также предоставляет hello решения этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-105">It also provides hello solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="c8e2a-106">Симптом</span><span class="sxs-lookup"><span data-stu-id="c8e2a-106">Symptom</span></span>

<span data-ttu-id="c8e2a-107">Могут возникнуть следующие проблемы, при работающих виртуальных машин Linux в Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-107">You may experience hello following problems when running Linux VMs in Microsoft Azure.</span></span>

- <span data-ttu-id="c8e2a-108">Hello виртуальной Машины завершается сбоем tooboot после перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-108">hello VM fails tooboot after a restart.</span></span>

- <span data-ttu-id="c8e2a-109">Если диски с данными отсоединяются и повторно присоединить, имена устройств hello дисков, заменяются.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-109">If data disks are detached and reattached, hello devices names for disks are changed.</span></span>

- <span data-ttu-id="c8e2a-110">Приложение или скрипт, который ссылается на диск с использованием имени устройства, не работает.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-110">An application or script that references a disk by using device name fails.</span></span> <span data-ttu-id="c8e2a-111">Найти, hello имя устройства hello диска можно изменить.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-111">You find that hello device name of hello disk is changed.</span></span>

## <a name="cause"></a><span data-ttu-id="c8e2a-112">Причина:</span><span class="sxs-lookup"><span data-stu-id="c8e2a-112">Cause</span></span>

<span data-ttu-id="c8e2a-113">Пути устройства в Linux не гарантируется toobe согласованных между перезагрузками.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-113">Device paths in Linux are not guaranteed toobe consistent across restarts.</span></span> <span data-ttu-id="c8e2a-114">Имена устройств состоят из основного (буква) и дополнительного номеров.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-114">Device names consist of major (letter) and minor numbers.</span></span>  <span data-ttu-id="c8e2a-115">Драйвер устройства хранения данных Linux hello обнаруживает новое устройство, присваивает tooit номера основной и дополнительный номер устройства из диапазона доступных hello.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-115">When hello Linux storage device driver detects a new device, it assigns major and minor device numbers tooit from hello available range.</span></span> <span data-ttu-id="c8e2a-116">При удалении устройства номера устройств hello, освобожденные toobe использован позднее.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-116">When a device is removed, hello device numbers are freed toobe reused later.</span></span>

<span data-ttu-id="c8e2a-117">Hello происходит потому, что hello устройств сканирования в Linux, назначенные подсистемой SCSI hello происходит асинхронно.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-117">hello problem occurs because hello device scanning in Linux scheduled by hello SCSI subsystem happens asynchronously.</span></span> <span data-ttu-id="c8e2a-118">именование путь Hello конечного устройства могут различаться между перезагрузками.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-118">hello final device path naming may vary across restarts.</span></span> 

## <a name="solution"></a><span data-ttu-id="c8e2a-119">Решение</span><span class="sxs-lookup"><span data-stu-id="c8e2a-119">Solution</span></span>

<span data-ttu-id="c8e2a-120">tooresolve эту проблему, используйте постоянные именования.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-120">tooresolve this problem, use persistent naming.</span></span> <span data-ttu-id="c8e2a-121">Существует четыре toopersistent методы именования - по метке файловой системы, uuid, по идентификатору и путь.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-121">There are four methods toopersistent naming - by filesystem label, by uuid, by id and by path.</span></span> <span data-ttu-id="c8e2a-122">Корпорация Майкрософт рекомендует hello метки файловой системы и методы UUID для виртуальных машин Linux в Azure.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-122">We recommend hello filesystem label and UUID methods for Azure Linux VMs.</span></span> 

<span data-ttu-id="c8e2a-123">Большинством дистрибутивов также предоставляют либо hello **nofail** или **nobootwait** fstab параметры.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-123">Most distributions also provide either hello **nofail** or **nobootwait** fstab options.</span></span> <span data-ttu-id="c8e2a-124">Эти параметры обеспечивают tooboot системы даже в случае сбоя диска hello toomount во время запуска.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-124">These options enable a system tooboot even if hello disk fails toomount at startup.</span></span> <span data-ttu-id="c8e2a-125">Проверьте документацию hello распространения Дополнительные сведения об этих параметрах.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-125">Check hello distribution's documentation for more information about these parameters.</span></span> <span data-ttu-id="c8e2a-126">Дополнительные сведения о том, как tooconfigure toouse ВМ Linux UUID, при добавлении диска данных, отображается [подключение нового диска ВМ Linux toomount hello toohello](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="c8e2a-126">For more information about how tooconfigure a Linux VM toouse a UUID when you add a data disk, see [Connect toohello Linux VM toomount hello new disk](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> 

<span data-ttu-id="c8e2a-127">При установке агента Azure Linux hello на виртуальной Машине, он использует правила tooconstruct Udev набор символические ссылки в разделе **/dev/disk/azure**.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-127">When hello Azure Linux agent is installed on a VM, it uses Udev rules tooconstruct a set of symbolic links under **/dev/disk/azure**.</span></span> <span data-ttu-id="c8e2a-128">Эти правила Udev могут использоваться приложениями и диски tooidentify сценариев toohello подключенных виртуальных Машин, их тип и hello LUN.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-128">These Udev rules can be used by applications and scripts tooidentify disks are attached toohello VM, their type, and hello LUN.</span></span>

## <a name="more-information"></a><span data-ttu-id="c8e2a-129">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="c8e2a-129">More information</span></span>

### <a name="identify-disk-luns"></a><span data-ttu-id="c8e2a-130">Определение LUN диска</span><span class="sxs-lookup"><span data-stu-id="c8e2a-130">Identify disk LUNs</span></span>

<span data-ttu-id="c8e2a-131">Приложение может использовать toofind LUN все hello присоединенные диски и Создание символических ссылок.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-131">An application can use LUNs toofind all hello attached disks and constructing symbolic links.</span></span> <span data-ttu-id="c8e2a-132">Hello Azure Linux agent теперь включает udev правила, настроить символические ссылки с LUN toohello устройств, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="c8e2a-132">hello Azure Linux agent now includes udev rules that set up symbolic links from a LUN toohello devices, as follows:</span></span>

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
                                 

<span data-ttu-id="c8e2a-133">Также можно получить сведения LUN из hello виртуальной машине Linux с помощью lsscsi или аналогичное средство следующим образом.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-133">LUN information can also be retrieved from hello Linux guest using lsscsi or similar tool as follows.</span></span>

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

<span data-ttu-id="c8e2a-134">Эти сведения гостевой LUN может использоваться с подпиской Azure метаданных tooidentify hello расположением в хранилище Azure hello виртуального жесткого диска, где хранятся данные секции hello.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-134">This guest LUN information can be used with Azure subscription metadata tooidentify hello location in Azure storage of hello VHD which stores hello partition data.</span></span> <span data-ttu-id="c8e2a-135">Например используйте hello az cli:</span><span class="sxs-lookup"><span data-stu-id="c8e2a-135">For example, use hello az cli:</span></span>

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

### <a name="discover-filesystem-uuids-by-using-blkid"></a><span data-ttu-id="c8e2a-136">Обнаружение UUID файловой системы с помощью служебной программы blkid</span><span class="sxs-lookup"><span data-stu-id="c8e2a-136">Discover filesystem UUIDs by using blkid</span></span>

<span data-ttu-id="c8e2a-137">Сценарий или приложение можно прочитать выходные данные hello блок идентификатором blkid или аналогичные источники данных и Создание символических ссылок в **/dev** для использования.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-137">A script or application can read hello output of blkid, or similar sources of information, and construct symbolic links in **/dev** for use.</span></span> <span data-ttu-id="c8e2a-138">Hello выходных данных будет показано, как hello UUID всех дисков присоединенного toohello виртуальной Машины и hello устройства файл toowhich они связаны.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-138">hello output will show hello UUIDs of all disks attached toohello VM and hello device file toowhich they are associated:</span></span>

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

<span data-ttu-id="c8e2a-139">Hello waagent udev правила формирования набора символических ссылок в группе **/dev/disk/azure**:</span><span class="sxs-lookup"><span data-stu-id="c8e2a-139">hello waagent udev rules construct a set of symbolic links under **/dev/disk/azure**:</span></span>


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


<span data-ttu-id="c8e2a-140">Эти сведения можно использовать приложение Hello идентификации hello загрузочного диска устройства и hello (эфемерных) ресурса диска.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-140">hello application can use this information identify hello boot disk device and hello resource (ephemeral) disk.</span></span> <span data-ttu-id="c8e2a-141">В Azure, приложения должны ссылаться слишком**/dev/disk/azure/root-part1** или **/dev/disk/azure-resource-part1** toodiscover этих секций.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-141">In Azure, applications should refer too**/dev/disk/azure/root-part1** or **/dev/disk/azure-resource-part1** toodiscover these partitions.</span></span>

<span data-ttu-id="c8e2a-142">Если имеются дополнительные разделы из списка блок идентификатором blkid hello, они находятся на диске данных.</span><span class="sxs-lookup"><span data-stu-id="c8e2a-142">If there are additional partitions from hello blkid list, they reside on a data disk.</span></span> <span data-ttu-id="c8e2a-143">Приложения могут поддерживать hello UUID для этих секций и использовать пути, например hello под именем устройства hello toodiscover во время выполнения:</span><span class="sxs-lookup"><span data-stu-id="c8e2a-143">Applications can maintain hello UUID for these partitions and use a path like hello below toodiscover hello device name at runtime:</span></span>

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-hello-latest-azure-storage-rules"></a><span data-ttu-id="c8e2a-144">Получить последние хранилища Azure правила hello</span><span class="sxs-lookup"><span data-stu-id="c8e2a-144">Get hello latest Azure storage rules</span></span>

<span data-ttu-id="c8e2a-145">toohello последнюю правила хранилища Azure, выполните рассматриваются следующие команды:</span><span class="sxs-lookup"><span data-stu-id="c8e2a-145">toohello latest Azure storage rules, run th following commands:</span></span>

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


<span data-ttu-id="c8e2a-146">Дополнительные сведения см. в разделе hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="c8e2a-146">For more information, see hello following articles:</span></span>

- <span data-ttu-id="c8e2a-147">[Для Ubuntu: UsingUUID](https://help.ubuntu.com/community/UsingUUID) (Использование UUID)</span><span class="sxs-lookup"><span data-stu-id="c8e2a-147">[Ubuntu: Using UUID](https://help.ubuntu.com/community/UsingUUID)</span></span>

- <span data-ttu-id="c8e2a-148">[Для Red Hat: Persistent Naming](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html) (Постоянные именования)</span><span class="sxs-lookup"><span data-stu-id="c8e2a-148">[Red Hat: Persistent Naming](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)</span></span>

- <span data-ttu-id="c8e2a-149">[Для Linux: What UUIDs can do for you](https://www.linux.com/news/what-uuids-can-do-you) (Чем полезны идентификаторы UUID)</span><span class="sxs-lookup"><span data-stu-id="c8e2a-149">[Linux: What UUIDs can do for you](https://www.linux.com/news/what-uuids-can-do-you)</span></span>

- [<span data-ttu-id="c8e2a-150">Udev: TooDevice введение в современных Linux системы управления</span><span class="sxs-lookup"><span data-stu-id="c8e2a-150">Udev: Introduction tooDevice Management In Modern Linux System</span></span>](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

