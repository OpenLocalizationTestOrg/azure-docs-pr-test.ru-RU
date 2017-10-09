---
title: "гостевые системы aaaLinux стек Azure | Документы Microsoft"
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
ms.openlocfilehash: 225bed7d630b676ca760add25731e347516b5bf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-linux-virtual-machines-on-azure-stack"></a>Развертывание виртуальных машин Linux в стек Azure
Можно развернуть виртуальные машины Linux в Azure стека Development Kit hello, добавив изображений на основе Linux в Azure Marketplace стека hello. Несколько поставщиков Linux предоставили образы, которые могут быть добавлены в пакет средств разработки Azure стека, или можно создать собственные.

## <a name="download-an-image"></a>Загрузить изображения
1. Загрузить и извлечь из ссылкам hello Azure стека совместимое изображение или Подготовка собственные:
   
   * [Bitnami](https://bitnami.com/azure-stack)
   * [CentOS](http://olstacks.cloudapp.net/latest/)
   * [CoreOS](https://stable.release.core-os.net/amd64-usr/current/coreos_production_azure_image.vhd.bz2)
   * [SuSE](https://download.suse.com/Download?buildid=VCFi7y7MsFQ~)
   * [Ubuntu 14.04 LTS](https://partner-images.canonical.com/azure/azure_stack/) / [Ubuntu 16.04 LTS](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)
2. Извлеките hello образа виртуального жесткого диска, при необходимости и [добавить toohello hello образа Marketplace](azure-stack-add-vm-image.md). Убедитесь в том, что hello `OSType` параметра установлено слишком`Linux`.
3. После добавления toohello hello образа Marketplace создается элемент Marketplace и развертывании виртуальной машины Linux.

## <a name="prepare-your-own-image"></a>Подготовьте свой собственный образ
1. Подготовьте свой собственный образ Linux с помощью одного из hello, следуйте инструкциям.
   
   * [Подготовка виртуальной машины на основе CentOS для Azure](../virtual-machines/linux/create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Подготовка виртуального жесткого диска Debian для Azure](../virtual-machines/linux/debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Oracle Linux](../virtual-machines/linux/oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Подготовка виртуальной машины на основе Red Hat для Azure](../virtual-machines/linux/redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Подготовка виртуальной машины SLES или openSUSE для Azure](../virtual-machines/linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Ubuntu](../virtual-machines/linux/create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. Загрузите и установите hello [агент Azure Linux](https://github.com/Azure/WALinuxAgent/)
   
    Hello Azure Linux Agent версии 2.1.3 или выше является обязательным tooprovision ВМ Linux Azure стек. Многие дистрибутивов hello, перечисленных выше, уже содержат эта версия агента hello или более поздней версии в виде пакета в их хранилищах (обычно называется `WALinuxAgent` или `walinuxagent`). Однако если hello версии пакета Azure агента hello, меньше, чем 2.1.3 (т. е. 2.0.18 или ниже), то необходимо вручную установить агент hello. Hello установлены версии можно определить имя пакета hello или запустив `/usr/sbin/waagent -version` на hello виртуальной Машины.
   
    Следуйте инструкциям hello ниже tooinstall hello Azure Linux agent вручную-
   
   * Во-первых, загрузите последнюю версию агента Azure Linux hello из [GitHub](https://github.com/Azure/WALinuxAgent/releases), пример:
     
            # wget https://github.com/Azure/WALinuxAgent/archive/v2.2.0.tar.gz
   * Распакуйте hello Azure агента:
     
            # tar -vzxf v2.2.0.tar.gz
   * Установка python дублирует
     
        **Debian и Ubuntu**
     
            # sudo apt-get update
            # sudo apt-get install python-setuptools
     
        **Ubuntu 16.04 +**
     
            # sudo apt-get install python3-setuptools
     
        **RHEL / CentOS и Oracle Linux**
     
            # sudo yum install python-setuptools
   * Установите агент Azure hello:
     
            # cd WALinuxAgent-2.2.0
            # sudo python setup.py install --register-service
     
     Системы с Python 2.x и Python 3.x установлен side-by-side возможно, потребуется hello toorun следующую команду:
     
         sudo python3 setup.py install --register-service
     Дополнительные сведения см. в разделе hello Azure Linux Agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md).
3. [Добавить toohello hello образа Marketplace](azure-stack-add-vm-image.md). Убедитесь в том, что hello `OSType` параметра установлено слишком`Linux`.
4. После добавления toohello hello образа Marketplace создается элемент Marketplace и развертывании виртуальной машины Linux.

## <a name="next-steps"></a>Дальнейшие действия
[Часто задаваемые вопросы про Azure стека](azure-stack-faq.md)

