---
title: "копирования пользовательских виртуальной Машины Linux с помощью Azure CLI 2.0 или aaaUpload | Документы Microsoft"
description: "Загрузки или копирования настраиваемую виртуальную машину с помощью модели развертывания диспетчера ресурсов hello и hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/06/2017
ms.author: cynthn
ms.openlocfilehash: 79af897120a6ba7f4a427ba6c7d0c31b7b870bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a>Создайте виртуальную Машину Linux из пользовательского диска с hello Azure CLI 2.0

<!-- rename toocreate-vm-specialized -->

В этой статье показано, как tooupload настроенного виртуального жесткого диска (VHD) или скопировать существующий VHD в Azure и создания новых виртуальных машин Linux (ВМ) с hello пользовательского диска. Можно установить и настроить требования tooyour дистрибутив Linux и затем использовать этот ДИСК tooquickly создания новой виртуальной машины Azure.

Следует toocreate несколько виртуальных машин с настроенные диска следует создать образ виртуальной Машины или виртуального жесткого диска. Дополнительные сведения см. в разделе [создать образ виртуальной машины Azure с помощью hello CLI](tutorial-custom-images.md).

Существует два варианта.
* [Передача VHD](#option-1-upload-a-specialized-vhd)
* [Копирование имеющейся виртуальной машины Azure](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a>Быстрые команды

При создании новой виртуальной Машины с помощью [создания виртуальной машины az](/cli/azure/vm#create) с специальную или специализированного диска вы **присоединения** hello диска (--присоединить os диск) вместо указания нестандартной проверки подлинности или marketplace изображения (--изображения). Hello следующий пример создает Виртуальную машину с именем *myVM* с помощью hello управляемого диска с именем *myManagedDisk* создан из вашего настроенного виртуального жесткого диска:

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a>Требования
toocomplete hello следующие действия, необходимо:

* Виртуальная машина Linux, которая была подготовлена для использования в Azure. Hello [hello подготовки виртуальной Машины](#prepare-the-vm) данной статьи рассматриваются как toofind дистрибутив определенные сведения об установке hello Azure Linux Agent (waagent) необходимый для toowork ВМ hello должным образом в Azure и вы toobe может tooconnect tooit с помощью SSH.
* Hello VHD-файл из существующего [дистрибутив Linux в одобренных Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (или в разделе [сведения для распределений, отличных от одобренных](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa виртуальный диск в формате VHD hello. Несколько средств существует toocreate виртуальной Машины и виртуального жесткого диска:
  * Установка и настройка [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) или [KVM](http://www.linux-kvm.org/page/RunningKVM), отвечающий за toouse виртуальный жесткий ДИСК в формате изображения. При необходимости вы можете [преобразовать образ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) с помощью команды **qemu-img convert**.
  * Кроме того, можно использовать Hyper-V [в Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) или [Windows Server 2012 и 2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Hello более новый формат VHDX не поддерживается в Azure. При создании виртуальной Машины, задайте hello формат виртуального жесткого диска. При необходимости можно преобразовать tooVHD диски VHDX с помощью [qemu img преобразовать](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) или hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) командлета PowerShell. Кроме того Azure не поддерживает передачи динамических виртуальных жестких дисков, поэтому требуется tooconvert toostatic такие диски VHD перед отправкой. Можно использовать средства, такие как [утилиты Azure виртуального жесткого диска для GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert динамических дисков во время процесса hello передачи tooAzure.
> 
> 


* Убедитесь, что hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).

В hello следующих примерах замените примеры имен параметров собственные значения. Примеры имен параметров: *myResourceGroup*, *mystorageaccount* и *mydisks*.

<a id="prepimage"> </a>

## <a name="prepare-hello-vm"></a>Подготовка виртуальной Машины hello

Azure поддерживает различные дистрибутивы Linux (см. раздел [Рекомендованные дистрибутивы](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). следующие статьи Hello проводит пользователя через как tooprepare hello различных дистрибутивов Linux, которые поддерживаются в Azure:

* [Подготовка виртуальной машины на основе CentOS для Azure](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Подготовка виртуального жесткого диска Debian для Azure](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Подготовка виртуальной машины на основе Red Hat для Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Подготовка виртуальной машины SLES или openSUSE для Azure](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Информация о нерекомендованных дистрибутивах](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

См. также hello [замечания по установке Linux](create-upload-generic.md#general-linux-installation-notes) Общие рекомендации по подготовке образов Linux для Azure.

> [!NOTE]
> Hello [платформы Azure соглашения об уровне ОБСЛУЖИВАНИЯ](https://azure.microsoft.com/support/legal/sla/virtual-machines/) применяется tooVMs под управлением Linux, если один из hello одобренных распределения используется с данными конфигурации hello, как указано в списке поддерживаемых версиях только в [Linux в одобренных Azure Распределения](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

## <a name="option-1-upload-a-vhd"></a>Вариант 1. Передача VHD

Вы можете передать настраиваемый VHD, выполняемый на локальном компьютере или который вы экспортировали из другого облака. виртуальный жесткий ДИСК toocreate hello toouse новой виртуальной Машины Azure, потребуется tooupload hello VHD tooa хранилище учетной записи и создания управляемой дисковой из hello виртуального жесткого диска. 

### <a name="create-a-resource-group"></a>Создание группы ресурсов

Перед загрузкой пользовательского диска и создании виртуальных машин, необходимо сначала toocreate группу ресурсов с [Создание группы az](/cli/azure/group#create).

Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение: [Общие сведения о дисках управляемых Azure](../windows/managed-disks-overview.md)
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a>Создать учетную запись хранения

Создайте учетную запись хранения для пользовательского диска и виртуальных машин с помощью команды [az storage account create](/cli/azure/storage/account#create). 

Hello следующий пример создает учетную запись хранения с именем *mystorageaccount* в ранее созданную группу ресурсов hello:

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a>Вывод списка ключей учетной записи хранения
Azure создает два 512-разрядных ключа доступа для каждой учетной записи хранения. Эти ключи доступа используются при проверке подлинности учетной записи хранилища toohello, как и выполнения операций записи. Дополнительные сведения о [управление доступ здесь toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). Просмотреть ключи доступа hello с [список ключей учетной записи хранилища az](/cli/azure/storage/account/keys#list).

Просмотр ключей доступа к hello для hello хранилища созданную учетную запись:

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

Hello выходные данные выглядят аналогично:

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
Запомните или запишите **key1** как он будет использоваться toointeract с вашей учетной записи хранения в hello дальнейшие действия.

### <a name="create-a-storage-container"></a>Создание контейнера хранилища
В hello так же, создания разных каталогах toologically организации локальной файловой системе, создайте контейнерам внутри tooorganize учетной записи хранения на дисках. Учетная запись хранения может содержать любое количество контейнеров. Создайте контейнер с помощью команды [az storage container create](/cli/azure/storage/container#create).

Hello следующий пример создает контейнер с именем *mydisks*:

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-hello-vhd"></a>Отправка hello виртуального жесткого диска
Теперь передайте пользовательский диск с помощью команды [az storage blob upload](/cli/azure/storage/blob#upload). Пользовательский диск передается и хранится как страничный BLOB-объект.

Укажите ваш ключ доступа, контейнер hello, созданный на предыдущем шаге hello и затем hello toohello пользовательского диска на локальном компьютере:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
Отправка hello виртуального жесткого диска может занять некоторое время.

### <a name="create-a-managed-disk"></a>Создание управляемого диска


Создание управляемого диска из hello виртуального жесткого диска с помощью [создать диск az](/cli/azure/disk#create). Hello следующий пример создает управляемого диска с именем *myManagedDisk* из hello виртуальный жесткий ДИСК отправлен tooyour с именем учетной записи хранилища и контейнера:

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a>Вариант 2. Копирование имеющейся виртуальной машины

Можно также создать hello настроенных ВМ в Azure, а затем Копировать диск ОС hello и присоединить ее новой виртуальной Машины toocreate tooa другую копию. Это хорошо работает для тестирования, но если требуется toouse существующей ВМ Azure как модель hello несколько новых виртуальных машин, действительно следует создать **изображения** вместо него. Дополнительные сведения о создании образа на основе существующей виртуальной Машине Azure см. в разделе [создать образ виртуальной машины Azure с помощью hello CLI](tutorial-custom-images.md)

### <a name="create-a-snapshot"></a>Создание моментального снимка

В этом примере создается моментальный снимок виртуальной машины с именем *myVM* в группе ресурсов *myResourceGroup*, а также моментальный снимок с именем *osDiskSnapshot*.

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-hello-managed-disk"></a>Создание управляемого диска hello

Создание нового управляемого диска из моментального снимка hello.

Получите идентификатор hello hello моментального снимка. В этом примере имя моментального снимка hello *osDiskSnapshot* и hello *myResourceGroup* группы ресурсов.

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

Создание управляемого диска hello. В этом примере мы создадим управляемый диск с именем *myManagedDisk* на основе моментального снимка размером в 128 ГБ, который хранится в хранилище уровня "Стандартный".

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-hello-vm"></a>Создание виртуальной Машины hello

Теперь создайте ВМ с [создания виртуальной машины az](/cli/azure/vm#create) и присоединения (--присоединить os диск) hello управляемых диск как диск ОС hello. Hello следующий пример создает Виртуальную машину с именем *myNewVM* с помощью hello управляемого диск, созданный из вашего загруженного VHD-файла:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

После этого можно будет tooSSH в hello виртуальной Машины с помощью учетных данных hello из hello исходной виртуальной Машины. 

## <a name="next-steps"></a>Дальнейшие действия
После подготовки и передачи пользовательского виртуального диска ознакомьтесь с дополнительными сведениями об [использовании Resource Manager и шаблонов](../../azure-resource-manager/resource-group-overview.md). Вы также можете слишком[добавьте диск данных](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour новые виртуальные машины. При наличии приложений, выполняющихся на виртуальные машины, необходимо tooaccess, нужно убедиться, что слишком[открыть порты и конечные точки](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

