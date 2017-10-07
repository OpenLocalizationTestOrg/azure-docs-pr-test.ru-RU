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
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a>Устранение неполадок. Изменение имен устройств виртуальных машин Linux

Hello статье объясняется, почему были изменены имена устройств после перезапуска виртуальной машины (VM) Linux или заново присоединить диски hello. Он также предоставляет hello решения этой проблемы.

## <a name="symptom"></a>Симптом

Могут возникнуть следующие проблемы, при работающих виртуальных машин Linux в Microsoft Azure hello.

- Hello виртуальной Машины завершается сбоем tooboot после перезагрузки.

- Если диски с данными отсоединяются и повторно присоединить, имена устройств hello дисков, заменяются.

- Приложение или скрипт, который ссылается на диск с использованием имени устройства, не работает. Найти, hello имя устройства hello диска можно изменить.

## <a name="cause"></a>Причина:

Пути устройства в Linux не гарантируется toobe согласованных между перезагрузками. Имена устройств состоят из основного (буква) и дополнительного номеров.  Драйвер устройства хранения данных Linux hello обнаруживает новое устройство, присваивает tooit номера основной и дополнительный номер устройства из диапазона доступных hello. При удалении устройства номера устройств hello, освобожденные toobe использован позднее.

Hello происходит потому, что hello устройств сканирования в Linux, назначенные подсистемой SCSI hello происходит асинхронно. именование путь Hello конечного устройства могут различаться между перезагрузками. 

## <a name="solution"></a>Решение

tooresolve эту проблему, используйте постоянные именования. Существует четыре toopersistent методы именования - по метке файловой системы, uuid, по идентификатору и путь. Корпорация Майкрософт рекомендует hello метки файловой системы и методы UUID для виртуальных машин Linux в Azure. 

Большинством дистрибутивов также предоставляют либо hello **nofail** или **nobootwait** fstab параметры. Эти параметры обеспечивают tooboot системы даже в случае сбоя диска hello toomount во время запуска. Проверьте документацию hello распространения Дополнительные сведения об этих параметрах. Дополнительные сведения о том, как tooconfigure toouse ВМ Linux UUID, при добавлении диска данных, отображается [подключение нового диска ВМ Linux toomount hello toohello](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk). 

При установке агента Azure Linux hello на виртуальной Машине, он использует правила tooconstruct Udev набор символические ссылки в разделе **/dev/disk/azure**. Эти правила Udev могут использоваться приложениями и диски tooidentify сценариев toohello подключенных виртуальных Машин, их тип и hello LUN.

## <a name="more-information"></a>Дополнительные сведения

### <a name="identify-disk-luns"></a>Определение LUN диска

Приложение может использовать toofind LUN все hello присоединенные диски и Создание символических ссылок. Hello Azure Linux agent теперь включает udev правила, настроить символические ссылки с LUN toohello устройств, как показано ниже:

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
                                 

Также можно получить сведения LUN из hello виртуальной машине Linux с помощью lsscsi или аналогичное средство следующим образом.

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

Эти сведения гостевой LUN может использоваться с подпиской Azure метаданных tooidentify hello расположением в хранилище Azure hello виртуального жесткого диска, где хранятся данные секции hello. Например используйте hello az cli:

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

### <a name="discover-filesystem-uuids-by-using-blkid"></a>Обнаружение UUID файловой системы с помощью служебной программы blkid

Сценарий или приложение можно прочитать выходные данные hello блок идентификатором blkid или аналогичные источники данных и Создание символических ссылок в **/dev** для использования. Hello выходных данных будет показано, как hello UUID всех дисков присоединенного toohello виртуальной Машины и hello устройства файл toowhich они связаны.

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

Hello waagent udev правила формирования набора символических ссылок в группе **/dev/disk/azure**:


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


Эти сведения можно использовать приложение Hello идентификации hello загрузочного диска устройства и hello (эфемерных) ресурса диска. В Azure, приложения должны ссылаться слишком**/dev/disk/azure/root-part1** или **/dev/disk/azure-resource-part1** toodiscover этих секций.

Если имеются дополнительные разделы из списка блок идентификатором blkid hello, они находятся на диске данных. Приложения могут поддерживать hello UUID для этих секций и использовать пути, например hello под именем устройства hello toodiscover во время выполнения:

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-hello-latest-azure-storage-rules"></a>Получить последние хранилища Azure правила hello

toohello последнюю правила хранилища Azure, выполните рассматриваются следующие команды:

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


Дополнительные сведения см. в разделе hello в следующих статьях:

- [Для Ubuntu: UsingUUID](https://help.ubuntu.com/community/UsingUUID) (Использование UUID)

- [Для Red Hat: Persistent Naming](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html) (Постоянные именования)

- [Для Linux: What UUIDs can do for you](https://www.linux.com/news/what-uuids-can-do-you) (Чем полезны идентификаторы UUID)

- [Udev: TooDevice введение в современных Linux системы управления](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

