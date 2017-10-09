---
title: "aaaTesting SAP NetWeaver на виртуальных машинах Linux SUSE Azure Майкрософт | Документы Microsoft"
description: "Тестирование SAP NetWeaver на виртуальных машинах SUSE Linux Microsoft Azure"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 645e358b-3ca1-4d3d-bf70-b0f287498d7a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: hermannd
ms.openlocfilehash: 0e3faab05417a1a15541e2b79aa7eddacda44611
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="running-sap-netweaver-on-microsoft-azure-suse-linux-vms"></a>Запуск SAP NetWeaver на виртуальных машинах SUSE Linux в Microsoft Azure
Этой статье описываются различные tooconsider действия при работе с SAP NetWeaver на виртуальных машинах Microsoft Azure SUSE Linux (ВМ). По состоянию на 19 мая 2016 года SAP NetWeaver официально поддерживается на виртуальных машинах SUSE Linux в Azure. Все сведения о версиях Linux, версиях ядра SAP и т. д. можно найти в примечании SAP 1928533 "SAP Applications on Azure: Supported Products and Azure VM types" (Приложения SAP в Azure: поддерживаемые продукты и типы виртуальных машин Azure).
Дополнительную документацию по SAP на виртуальных машинах Linux можно найти здесь: [Использование SAP на виртуальных машинах Linux](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Hello следующие сведения помогут вам избежать некоторых потенциальных проблем.

## <a name="suse-images-on-azure-for-running-sap"></a>Образы SUSE в Azure для запуска SAP
Для запуска SAP NetWeaver в Azure используйте только SUSE Linux Enterprise Server SLES 12 (SPx). Также ознакомьтесь с примечанием SAP 1928533. Специальные изображению SUSE в hello Azure Marketplace («SLES 11 с пакетом обновления 3 для SAP CAL»), но он не предназначен для общего использования. Не используйте этот образ, поскольку он зарезервирован для hello [устройство библиотеки SAP облака](https://cal.sap.com/) решения.  

Все новые тесты и установки в Azure должны выполняться с помощью Azure Resource Manager. toolook для SUSE SLES изображений и версий с помощью Azure PowerShell или hello Azure командной строки (CLI), hello используйте следующие команды. Затем можно использовать hello выходных данных, например, toodefine hello образа ОС в шаблон JSON для развертывания новой виртуальной Машины Linux SUSE.
Для Azure Powershell версии 1.0.1 и более поздних действительны следующие команды PowerShell.

Хотя это все еще возможно toouse hello стандартных SLES изображений для установок SAP рекомендуется использование toomake hello новый SLES SAP образов, которые доступны теперь на hello Azure изображений коллекции. Дополнительные сведения об этих изображениях можно найти на соответствующий hello [страницы Azure Marketplace]( https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SUSE.SLES-SAP ) или hello [веб-страницы SUSE часто задаваемые вопросы о SLES для SAP]( https://www.suse.com/products/sles-for-sap/frequently-asked-questions/ ).


* Поиск существующих издателей, включая SUSE:
  
   ```
   PS  : Get-AzureRmVMImagePublisher -Location "West Europe"  | where-object { $_.publishername -like "*US*"  }
   CLI : azure vm image list-publishers westeurope | grep "US"
   ```
* Поиск существующих предложений от SUSE:
  
   ```
   PS  : Get-AzureRmVMImageOffer -Location "West Europe" -Publisher "SUSE"
   CLI : azure vm image list-offers westeurope SUSE
   ```
* Поиск предложений SLES от SUSE:
  
   ```
   PS  : Get-AzureRmVMImageSku -Location "West Europe" -Publisher "SUSE" -Offer "SLES"
   PS  : Get-AzureRmVMImageSku -Location "West Europe" -Publisher "SUSE" -Offer "SLES-SAP"
   CLI : azure vm image list-skus westeurope SUSE SLES
   CLI : azure vm image list-skus westeurope SUSE SLES-SAP
   ```
* Поиск определенной версии SKU для SLES:
  
   ```
   PS  : Get-AzureRmVMImage -Location "West Europe" -Publisher "SUSE" -Offer "SLES" -skus "12-SP2"
   PS  : Get-AzureRmVMImage -Location "West Europe" -Publisher "SUSE" -Offer "SLES-SAP" -skus "12-SP2"
   CLI : azure vm image list westeurope SUSE SLES 12-SP2
   CLI : azure vm image list westeurope SUSE SLES-SAP 12-SP2
   ```

## <a name="installing-walinuxagent-in-a-suse-vm"></a>Установка WALinuxAgent в виртуальной машине SUSE
Hello агентом, называемым WALinuxAgent является частью hello SLES изображений в hello Azure Marketplace. Сведения о его установке вручную (например, при отправке виртуального жесткого диска с ОС SLES из локальной среды) см. в статьях:

* [OpenSUSE](http://software.opensuse.org/package/WALinuxAgent)
* [Таблицы Azure](../../linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [SUSE](https://www.suse.com/communities/blog/suse-linux-enterprise-server-configuration-for-windows-azure/)

## <a name="sap-enhanced-monitoring"></a>"Расширенный мониторинг" SAP
SAP «улучшенный мониторинг» является обязательным к установке toorun SAP в Azure. Ознакомьтесь с информацией в примечании SAP 2191498 "SAP on Linux with Azure: Enhanced Monitoring" (SAP на платформе Linux в Azure: расширенный мониторинг).

## <a name="attaching-azure-data-disks-tooan-azure-linux-vm"></a>Присоединение дисков данных Azure tooan виртуальной Машине Linux Azure
Никогда не следует подключать диски данных Azure tooan виртуальной Машине Linux Azure с помощью кода hello устройства. Вместо этого используйте hello универсальный уникальный идентификатор (UUID). Будьте внимательны при использовании дисков данных Azure toomount графических средств, например. Следует внимательно hello записей в/etc/fstab.

Hello проблема с ИД устройства hello — он может измениться, которое затем hello виртуальной Машины Azure может зависнуть в процессе загрузки hello. toomitigate hello проблему, можно добавить параметр nofail hello в/etc/fstab. Но будьте осторожны с nofail, так как приложения могут использовать точки подключения hello как перед и может записать в hello корневой файловой системы, в случае, если во время загрузки hello не был подключен диск внешних данных Azure.

Hello toomounting единственное исключение через UUID присоединения диска ОС при устранении неполадок, как описано в следующем разделе hello.

## <a name="troubleshooting-a-suse-vm-that-isnt-accessible-anymore"></a>Устранение неполадок с виртуальной машиной SUSE, которая стала недоступной
Может возникнуть ситуация, где SUSE виртуальной Машины в Azure зависает в процессе загрузки hello (например, с помощью ошибка, связанная с подключением дисков). Эту проблему можно проверить с помощью функции диагностики hello загрузки для виртуальных машин Azure v2 в hello портал Azure. Дополнительные сведения см. в статье [Диагностика загрузки](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).

Одним из способов toosolve hello проблема заключается в том диска ОС tooattach hello из hello повреждена tooanother ВМ SUSE ВМ в Azure. Внесите соответствующие изменения как/etc/fstab редактирование или удаление правила udev сети, как описано в следующем разделе hello.

Имеется один tooconsider важно. Развертывание нескольких ВМ SUSE из hello, приводит к тому же Azure Marketplace изображение (например, 11 SP4 SLES) hello ОС подключить диск tooalways hello одинаковый UUID. Таким образом использование tooattach hello UUID диска ОС из другой виртуальной Машины, которое было развернуто с помощью того же образа Azure Marketplace приведет к два идентичных UUID hello. Это вызывает проблемы и может означать, что hello виртуальная машина, предназначен для устранения неполадок в действительности будет загружаться с присоединенного hello поврежденного диска операционной системы вместо hello оригинального.

Существует два способа tooavoid это:

* Используйте другое изображение Azure Marketplace для hello, устранение неполадок виртуальной Машины (например, SLES 11 SPx вместо SLES 12).
* Не присоединять hello повреждения диска ОС из другой виртуальной Машины с помощью идентификатора UUID--используйте другое.

## <a name="uploading-a-suse-vm-from-on-premises-tooazure"></a>Отправка SUSE виртуальную Машину из локальной tooAzure
Описание действия hello tooupload SUSE виртуальную Машину из локальной tooAzure см. в разделе [Подготовка виртуальной машины SLES или openSUSE для Azure](../../linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Tooupload виртуальной Машины без отзыва hello шаг в конце hello (например, tookeep существующей установки SAP, а также имя узла hello), установите флажок hello следующих элементов:

* Убедитесь, что подключен этот диск hello операционной системы с помощью идентификатора UUID и не hello идентификатор устройства. Изменение tooUUID только в/etc/fstab недостаточно для диска ОС hello. Кроме того не забывайте tooadapt hello загрузчик через YaST или изменив /boot/grub/menu.lst.
* При использовании формата VHDX hello для диска операционной системы SUSE hello и преобразовать его tooVHD для передачи tooAzure, скорее всего, сетевое устройство hello изменится с eth0 tooeth1. tooavoid проблем при загрузке в Azure, более поздней версии, изменить задней tooeth0, как описано в [исправления eth0 в клонировать SLES 11 VMware](https://dartron.wordpress.com/2013/09/27/fixing-eth1-in-cloned-sles-11-vmware/).

В дополнение к этому toowhat описанные в статье hello, рекомендуется удалить это:

   /lib/udev/rules.d/75-persistent-net-generator.rules.

Можно также установить hello Azure Linux Agent (waagent) toohelp избежать потенциальных проблем, при условии, что не существует несколько сетевых адаптеров.

## <a name="deploying-a-suse-vm-on-azure"></a>Развертывание виртуальной машины SUSE в Azure
Необходимо создать новые виртуальные машины SUSE с помощью файлов шаблона JSON в новую модель диспетчера ресурсов Azure hello. После создания файла шаблона JSON hello hello виртуальной Машины можно развернуть, используя следующую команду CLI как альтернативный tooPowerShell hello:

   ```
   azure group deployment create "<deployment name>" -g "<resource group name>" --template-file "<../../filename.json>"

   ```
Дополнительные сведения о JSON-файлах шаблонов см. в статьях [Создание шаблонов Azure Resource Manager](../../../resource-group-authoring-templates.md) и [Шаблоны быстрого запуска Azure](https://azure.microsoft.com/documentation/templates/).

Дополнительные сведения о CLI и диспетчера ресурсов Azure см. в разделе [используйте hello Azure CLI для Mac, Linux и Windows с помощью диспетчера ресурсов Azure](../../../xplat-cli-azure-resource-manager.md).

## <a name="sap-license-and-hardware-key"></a>Ключ оборудования и лицензия SAP
Для hello официальный сертификации SAP Azure новый механизм было введено toocalculate SAP hello аппаратный ключ, используемый для hello SAP лицензии. ядра SAP Hello было адаптировать toobe toomake использования данного объекта. В предыдущих версиях ядра SAP для Linux такое изменение кода отсутствует. Таким образом, в некоторых случаях (например, виртуальная машина Azure изменения размера), изменить ключ оборудования SAP hello и hello SAP лицензия была больше не действительна. Это решена в последней ядрах SAP Linux hello. Подробные сведения представлены в примечании SAP 1928533.

## <a name="suse-sapconf-package--tuned-adm"></a>Пакет SUSE sapconf / tuned-adm
В SUSE есть пакет под названием sapconf, который содержит набор параметров SAP. Дополнительные сведения об этом пакете какие не и как tooinstall и использовать его см. в разделе [систем SAP toorun SUSE Linux Enterprise Server с помощью sapconf tooprepare](https://www.suse.com/communities/blog/using-sapconf-to-prepare-suse-linux-enterprise-server-to-run-sap-systems/) и [возможности sapconf или как tooprepare SUSE Linux Enterprise Сервер для систем SAP? ](http://scn.sap.com/community/linux/blog/2014/03/31/what-is-sapconf-or-how-to-prepare-a-suse-linux-enterprise-server-for-running-sap-systems).

В hello пока имеется новое средство, который заменяет sapconf - настраиваемых adm. Один можно найти дополнительные сведения об этом инструменте hello два ссылкам ниже.

Документацию SLES по профилю sap-hana в tuned-adm см. [здесь](https://www.suse.com/documentation/sles-for-sap-12/book_s4s/data/sec_s4s_configure_sapconf.html). 

Сведения о настройке систем для рабочих нагрузок SAP с помощью tuned-adm см. в разделе 6.2 [этой статьи](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/book_s4s/book_s4s.pdf).

## <a name="nfs-share-in-distributed-sap-installations"></a>Общая папка NFS в распределенных установках SAP
При наличии распределенной установки — например, который нужно базы данных tooinstall hello и hello серверов приложений SAP в отдельных виртуальных машин — можно предоставить каталог /sapmnt hello через сетевой файловой системы (NFS). При наличии проблем с действия по установке hello после создания общей папки NFS для /sapmnt приветствия, проверьте toosee, если имеет значение «no_root_squash» для общего ресурса hello.

## <a name="logical-volumes"></a>Логические тома
В прошлом hello один необходимости большой логический том на нескольких дисках данных Azure (например, для базы данных SAP hello), рекомендовалось toouse mdadm как lvm не была проверена полностью еще в Azure. в статье tooset копирование RAID Linux в Azure с помощью mdadm, toolearn [Настройка программного RAID на платформе Linux](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). В hello это время на момент начала мая 2016 г. также lvm полностью поддерживается в Azure и можно использовать в качестве альтернативного toomdadm. Дополнительные сведения об использовании LVM в Azure см. в статье [Настройка диспетчера логических томов на виртуальной машине Linux в Azure](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="azure-suse-repository"></a>Репозиторий SUSE Azure
При наличии проблемы с репозиторием Azure SUSE стандартный доступ toohello tooreset простой команды можно использовать его. Это может произойти, если создать собственный образ операционной системы в регионе Azure, а затем копировать hello изображения tooa другой регион место toodeploy новые виртуальные машины, основанные на этот закрытый образ ОС. Просто выполните следующую команду в hello ВМ hello.

   ```
   service guestregister restart
   ```

## <a name="gnome-desktop"></a>Gnome Desktop
Toouse hello Gnome рабочего стола tooinstall завершения демонстрационная система SAP в одной виртуальной Машине — включая SAP GUI, браузера и консоль управления SAP — используйте этот tooinstall указание его на изображениях hello Azure SLES:

   Для SLES 11:

   ```
   zypper in -t pattern gnome
   ```

   Для SLES 12:

   ```
   zypper in -t pattern gnome-basic
   ```

## <a name="sap-support-for-oracle-on-linux-in-hello-cloud"></a>Поддержка Oracle в Linux в облаке hello в SAP
Существует ограничение поддержки, накладываемое Oracle на Linux в виртуализованных средах. Несмотря на то, что это не посвященных конкретным Azure, является важным toounderstand. SAP не поддерживает Oracle на SUSE или RedHat в общедоступном облаке, таком как Azure. toodiscuss в этом разделе, обратитесь непосредственно к Oracle.

