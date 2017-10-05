---
title: "Гости Linux на стек Azure | Документы Microsoft"
description: "Узнайте, как создать виртуальные машины под управлением Linux стек Azure."
services: azure-stack
documentationcenter: 
author: anjayajodha
manager: byronr
editor: 
ms.assetid: d2155c59-902e-4f63-ac58-d19e6a765380
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: anajod
ms.openlocfilehash: 935cd31c4b38262b7e42271574a8a221377a3cec
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-linux-virtual-machines-on-azure-stack"></a>Развертывание виртуальных машин Linux в стек Azure
Можно развернуть виртуальные машины Linux в пакет средств разработки Azure стека, добавив изображений на основе Linux в Azure Marketplace стека. Несколько поставщиков Linux предоставили образы, которые могут быть добавлены в пакет средств разработки Azure стека, или можно создать собственные.

## <a name="download-an-image"></a>Загрузить изображения
1. Загрузить и извлечь изображение Azure стека совместимой по следующим ссылкам или подготовить собственные:
   
   * [Bitnami](https://bitnami.com/azure-stack)
   * [CentOS](http://olstacks.cloudapp.net/latest/)
   * [CoreOS](https://stable.release.core-os.net/amd64-usr/current/coreos_production_azure_image.vhd.bz2)
   * [SuSE](https://download.suse.com/Download?buildid=VCFi7y7MsFQ~)
   * [Ubuntu 14.04 LTS](https://partner-images.canonical.com/azure/azure_stack/) / [Ubuntu 16.04 LTS](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)
2. Извлеките образ виртуального жесткого диска, при необходимости и [добавить изображение в Marketplace](azure-stack-add-vm-image.md). Убедитесь, что `OSType` параметра равным `Linux`.
3. После добавления изображения в Marketplace создается элемент Marketplace и развертывании виртуальной машины Linux.

## <a name="prepare-your-own-image"></a>Подготовьте свой собственный образ
1. Подготовьте свой собственный образ Linux с помощью одного из следующих инструкций:
   
   * [Подготовка виртуальной машины на основе CentOS для Azure](../virtual-machines/linux/create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Подготовка виртуального жесткого диска Debian для Azure](../virtual-machines/linux/debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Oracle Linux](../virtual-machines/linux/oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Подготовка виртуальной машины на основе Red Hat для Azure](../virtual-machines/linux/redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Подготовка виртуальной машины SLES или openSUSE для Azure](../virtual-machines/linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Ubuntu](../virtual-machines/linux/create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. Загрузите и установите [агент Azure Linux](https://github.com/Azure/WALinuxAgent/)
   
    Azure Linux Agent версии 2.1.3 или более поздняя версия требуется для подготовки виртуальной Машины Linux в стеке Azure. Многие распределений, перечисленных выше, уже содержат эта версия агента или более поздней версии в виде пакета в их хранилищах (обычно называется `WALinuxAgent` или `walinuxagent`). Тем не менее если версия пакет Azure агента, меньше, чем 2.1.3 (т. е. 2.0.18 или ниже), то необходимо установить агент вручную. Установленная версия можно определить имя пакета или запустив `/usr/sbin/waagent -version` на виртуальной Машине.
   
    Следуйте инструкциям для установки агента Azure Linux вручную-
   
   * Во-первых, загрузите последнюю версию агента Azure Linux из [GitHub](https://github.com/Azure/WALinuxAgent/releases), пример:
     
            # wget https://github.com/Azure/WALinuxAgent/archive/v2.2.0.tar.gz
   * Распакуйте агент Azure:
     
            # tar -vzxf v2.2.0.tar.gz
   * Установка python дублирует
     
        **Debian и Ubuntu**
     
            # sudo apt-get update
            # sudo apt-get install python-setuptools
     
        **Ubuntu 16.04 +**
     
            # sudo apt-get install python3-setuptools
     
        **RHEL / CentOS и Oracle Linux**
     
            # sudo yum install python-setuptools
   * Установите агент Azure:
     
            # cd WALinuxAgent-2.2.0
            # sudo python setup.py install --register-service
     
     Системы с Python 2.x и Python 3.x установлен side-by-side может потребоваться выполнить следующую команду:
     
         sudo python3 setup.py install --register-service
     Дополнительные сведения см. в разделе агент Azure Linux [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md).
3. [Добавить изображение в Marketplace](azure-stack-add-vm-image.md). Убедитесь, что `OSType` параметра равным `Linux`.
4. После добавления изображения в Marketplace создается элемент Marketplace и развертывании виртуальной машины Linux.

## <a name="next-steps"></a>Дальнейшие действия
[Часто задаваемые вопросы про Azure стека](azure-stack-faq.md)

