---
title: "aaaCreate и отправка tooAzure виртуального жесткого диска Linux | Документы Microsoft"
description: "Создание и отправка в Azure виртуального жесткого диска (VHD), содержащий hello Linux операционной системы с помощью hello классической модели развертывания"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8058ff98-db03-4309-9bf4-69842bd64dd4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: iainfou
ms.openlocfilehash: 77b01316386c4a6eb68c129fa68d42f0a8996edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-hello-linux-operating-system"></a>Создание и загрузка виртуального жесткого диска, который содержит hello операционной системы Linux
> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Вы можете также [передать пользовательский образ с помощью Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

В этой статье показано, как toocreate и передача виртуального жесткого диска (VHD), поэтому ее можно использовать в качестве собственного образа toocreate виртуальных машин в Azure. Узнайте, как tooprepare hello операционной системы, чтобы вы могли использовать toocreate нескольких виртуальных машин на основе этого образа. 


## <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается, что hello следующих элементов:

* **Операционной системы Linux в VHD-файла** -установки [дистрибутив Linux в одобренных Azure](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (или в разделе [сведения для распределений, отличных от одобренных](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa виртуального диска в формате VHD hello. Несколько средств существует toocreate виртуальной Машины и виртуального жесткого диска:
  * Установка и настройка [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) или [KVM](http://www.linux-kvm.org/page/RunningKVM), отвечающий за toouse виртуальный жесткий ДИСК в формате изображения. При необходимости вы можете [преобразовать образ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) с помощью `qemu-img convert`.
  * Кроме того, можно использовать Hyper-V [в Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) или [Windows Server 2012 и 2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Hello более новый формат VHDX не поддерживается в Azure. При создании виртуальной Машины, задайте hello формат виртуального жесткого диска. При необходимости можно преобразовать tooVHD диски VHDX с помощью [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) или hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) командлета PowerShell. Кроме того Azure не поддерживает передачи динамических виртуальных жестких дисков, поэтому требуется tooconvert toostatic такие диски VHD перед отправкой. Можно использовать средства, такие как [утилиты Azure виртуального жесткого диска для GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert динамических дисков во время процесса hello передачи tooAzure.

* **Интерфейс командной строки Azure** -последние hello установки [интерфейса командной строки Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooupload hello виртуального жесткого диска.

<a id="prepimage"> </a>

## <a name="step-1-prepare-hello-image-toobe-uploaded"></a>Шаг 1: Подготовка отправлен toobe изображения hello
Azure поддерживает различные дистрибутивы Linux (см. раздел [Рекомендованные дистрибутивы](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). следующие статьи Hello начнется как tooprepare hello различных дистрибутивов Linux, которые поддерживаются в Azure. После выполнения шагов hello в следующие руководства hello, могут быть вернитесь сюда, получив файл виртуального жесткого диска, готовы tooupload tooAzure:

* **[Дистрибутивы на основе CentOS](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES и OpenSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Прочее — нерекомендованные дистрибутивы](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

> [!NOTE]
> Hello соглашения об уровне ОБСЛУЖИВАНИЯ платформы Azure применяется toovirtual компьютеров под управлением ОС Linux только в том случае, если один из hello одобренных распределения используется с hello сведения о конфигурации, как указано в списке поддерживаемых версиях hello [Linux в распределениях Azure-Endorsed ](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Все дистрибутивы Linux в коллекции образов Azure hello являются индоссированный распределения с требуемой конфигурацией hello.
> 
> 

См. также hello  **[замечания по установке Linux](../create-upload-generic.md#general-linux-installation-notes)**  Общие рекомендации по подготовке образов Linux для Azure.

<a id="connect"> </a>

## <a name="step-2-prepare-hello-connection-tooazure"></a>Шаг 2: Подготовка tooAzure подключения hello
Убедитесь, что вы используете hello Azure CLI в hello классической модели развертывания (`azure config mode asm`), затем войдите в учетную запись tooyour:

```azurecli
azure login
```


<a id="upload"> </a>

## <a name="step-3-upload-hello-image-tooazure"></a>Шаг 3: Отправка tooAzure изображения hello
Необходимо tooupload учетной записи хранения файла виртуального жесткого диска. Можно выбрать существующую учетную запись хранения или [создать новую](../../../storage/common/storage-create-storage-account.md).

Используйте hello Azure CLI tooupload hello образ с помощью hello следующую команду:

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

В предыдущем примере hello:

* **BlobStorageURL** hello URL-адрес для учетной записи хранения hello планирование toouse
* **YourImagesFolder** — контейнер hello в хранилище больших двоичных объектов, место toostore изображений
* **VHDName** — hello метка, которая отображается в портале tooidentify hello виртуального жесткого диска.
* **PathToVHDFile** hello полный путь и имя hello VHD-файл на компьютере.

Следующая команда Hello приведен пример:

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-hello-image"></a>Шаг 4: Создайте виртуальную Машину из образа hello
Создание виртуальной Машины с помощью `azure vm create` в hello так же, как обычный виртуальной Машины. Укажите имя hello Вы дали образа на предыдущем шаге hello. В следующем примере hello, мы используем hello **myImage** имя изображения, указанного в предыдущем шаге hello:

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

toocreate собственные виртуальные машины предоставляют свои собственные пользователя + пароль, расположение, DNS-имя и имя образа.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения см. в разделе [ссылку Azure CLI для hello Azure классической модели развертывания](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

[Step 1: Prepare hello image toobe uploaded]:#prepimage
[Step 2: Prepare hello connection tooAzure]:#connect
[Step 3: Upload hello image tooAzure]:#upload
