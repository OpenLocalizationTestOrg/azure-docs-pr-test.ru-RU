---
title: "aaaUpload пользовательского диска Linux с помощью Azure CLI 2.0 | Документы Microsoft"
description: "Создание и отправка виртуального жесткого диска (VHD) tooAzure, с помощью модели развертывания диспетчера ресурсов hello и hello Azure CLI 2.0"
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
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: cf8556ab4dfe6c4e5eff4e99fe1ddc44393f774c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a>Передача и создание виртуальной Машины Linux с пользовательской диска с hello Azure CLI 2.0
В этой статье показано, как tooupload tooan виртуального жесткого диска (VHD) хранилища Azure учетной записи с hello Azure CLI 2.0 и создания виртуальных машин Linux с этого пользовательского диска. Можно также выполнить следующие действия с hello [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Эта функция позволяет вам tooinstall и настройте требования tooyour дистрибутив Linux и затем использовать этот виртуальный жесткий ДИСК tooquickly создания виртуальных машин (ВМ) Azure.

В этом разделе используются учетные записи хранения для hello окончательного виртуальные жесткие диски, но можно также сделать эти шаги с помощью [управляемых дисках](upload-vhd.md). 

## <a name="quick-commands"></a>Быстрые команды
При необходимости tooquickly выполнения задачи hello, hello следующий раздел сведения hello базовые команды tooupload tooAzure виртуального жесткого диска. Более подробные сведения и контекста, для каждого шага можно найти hello остальной части документа hello [начиная здесь](#requirements).

Убедитесь, что hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).

В hello следующих примерах замените примеры имен параметров собственные значения. Используемые имена параметров — `myResourceGroup`, `mystorageaccount`, и `mydisks`.

Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create). Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `WestUs` расположение:

```azurecli
az group create --name myResourceGroup --location westus
```

Создание учетной записи хранилища toohold виртуальных дисков с [создания учетной записи хранилища az](/cli/azure/storage/account#create). Hello следующий пример создает учетную запись хранения с именем `mystorageaccount`:

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

Список hello ключи доступа для учетной записи хранилища с [список ключей учетной записи хранилища az](/cli/azure/storage/account/keys#list). Запишите `key1`:

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

Создание контейнера в учетной записи хранилища с помощью ключа хранилища hello получен с [создать контейнер хранилища az](/cli/azure/storage/container#create). Hello следующий пример создает контейнер с именем `mydisks` с помощью hello значение ключа хранилища из `key1`:

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

Наконец, отправьте toohello контейнера VHD был создан с [передачи BLOB-объекта хранилища az](/cli/azure/storage/blob#upload). Укажите локальный путь hello tooyour виртуальный жесткий ДИСК в разделе `/path/to/disk/mydisk.vhd`:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

Укажите диск tooyour hello URI (`--image`) с [создания виртуальной машины az](/cli/azure/vm#create). Hello следующий пример создает Виртуальную машину с именем `myVM` с помощью виртуального диска hello ранее отправленные:

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

Hello целевой учетной записью хранения имеет toobe Здравствуйте таким же, как где загруженный виртуальный диск. Также необходимо toospecify или ответить на запрос, все hello Дополнительные параметры, необходимые для hello **создания виртуальной машины az** команды, такие как виртуальная сеть, общедоступный IP-адрес, имя пользователя и ключи SSH. Вы можете прочитать больше о hello [доступных параметров диспетчера ресурсов CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).

## <a name="requirements"></a>Требования
toocomplete hello следующие действия, необходимо:

* **Операционной системы Linux в VHD-файла** -установка [дистрибутив Linux в одобренных Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (или в разделе [сведения для распределений, отличных от одобренных](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa виртуальный диск в hello виртуального жесткого диска формат. Несколько средств существует toocreate виртуальной Машины и виртуального жесткого диска:
  * Установка и настройка [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) или [KVM](http://www.linux-kvm.org/page/RunningKVM), отвечающий за toouse виртуальный жесткий ДИСК в формате изображения. При необходимости вы можете [преобразовать образ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) с помощью `qemu-img convert`.
  * Кроме того, можно использовать Hyper-V [в Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) или [Windows Server 2012 и 2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Hello более новый формат VHDX не поддерживается в Azure. При создании виртуальной Машины, задайте hello формат виртуального жесткого диска. При необходимости можно преобразовать tooVHD диски VHDX с помощью [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) или hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) командлета PowerShell. Кроме того Azure не поддерживает передачи динамических виртуальных жестких дисков, поэтому требуется tooconvert toostatic такие диски VHD перед отправкой. Можно использовать средства, такие как [утилиты Azure виртуального жесткого диска для GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert динамических дисков во время процесса hello передачи tooAzure.
> 
> 

* Виртуальные машины, созданные с пользовательской диска необходимо разместить в hello же учетной записи хранилища, сам диск hello
  * Создание хранилища учетной записи и контейнер toohold созданных виртуальных машин и пользовательского диска
  * Когда вы закончите создание всех виртуальных машин, диск можно спокойно удалить.

Убедитесь, что hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).

В hello следующих примерах замените примеры имен параметров собственные значения. Используемые имена параметров — `myResourceGroup`, `mystorageaccount`, и `mydisks`.

<a id="prepimage"> </a>

## <a name="prepare-hello-disk-toobe-uploaded"></a>Подготовка toobe диска hello отправлен
Azure поддерживает различные дистрибутивы Linux (см. раздел [Рекомендованные дистрибутивы](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). следующие статьи Hello проводит пользователя через как tooprepare hello различных дистрибутивов Linux, которые поддерживаются в Azure:

* **[Дистрибутивы на основе CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES и OpenSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Прочее — нерекомендованные дистрибутивы](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

См. также hello  **[замечания по установке Linux](create-upload-generic.md#general-linux-installation-notes)**  Общие рекомендации по подготовке образов Linux для Azure.

> [!NOTE]
> Hello [платформы Azure соглашения об уровне ОБСЛУЖИВАНИЯ](https://azure.microsoft.com/support/legal/sla/virtual-machines/) применяется tooVMs под управлением Linux, если один из hello одобренных распределения используется с данными конфигурации hello, как указано в списке поддерживаемых версиях только в [Linux в одобренных Azure Распределения](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

## <a name="create-a-resource-group"></a>Создание группы ресурсов
Группы ресурсов логически объединить все toosupport ресурсы Azure hello виртуальных машин, например hello виртуальных сетей и хранилища. См. дополнительные сведения о [группах ресурсов](../../azure-resource-manager/resource-group-overview.md). Перед загрузкой пользовательского диска и создании виртуальных машин, необходимо сначала toocreate группу ресурсов с [Создание группы az](/cli/azure/group#create).

Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `westus` расположение:

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a>Создать учетную запись хранения

Создайте учетную запись хранения для пользовательского диска и виртуальных машин с помощью команды [az storage account create](/cli/azure/storage/account#create). Все виртуальные машины с неуправляемой диски, создаваемые на основе toobe потребности вашего пользовательского диска в hello же учетной записи хранилища этот диск. 

Hello следующий пример создает учетную запись хранения с именем `mystorageaccount` в ранее созданную группу ресурсов hello:

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a>Вывод списка ключей учетной записи хранения
Azure создает два 512-разрядных ключа доступа для каждой учетной записи хранения. Эти ключи доступа используются при проверке подлинности учетной записи хранилища toohello, например toocarry операций записи. Дополнительные сведения о [управление доступ здесь toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). Просмотреть ключи доступа hello с [список ключей учетной записи хранилища az](/cli/azure/storage/account/keys#list).

Просмотр ключей доступа к hello для hello хранилища созданную учетную запись:

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
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
Запомните или запишите `key1` как он будет использоваться toointeract с вашей учетной записи хранения в hello дальнейшие действия.

## <a name="create-a-storage-container"></a>Создание контейнера хранилища
В hello так же, создания разных каталогах toologically организации локальной файловой системе, создайте контейнерам внутри tooorganize учетной записи хранения на дисках. Учетная запись хранения может содержать любое количество контейнеров. Создайте контейнер с помощью команды [az storage container create](/cli/azure/storage/container#create).

Hello следующий пример создает контейнер с именем `mydisks`:

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a>Передача VHD
Теперь передайте пользовательский диск с помощью команды [az storage blob upload](/cli/azure/storage/blob#upload). Пользовательский диск передается и хранится как страничный BLOB-объект.

Укажите ваш ключ доступа, контейнер hello, созданный на предыдущем шаге hello и затем hello toohello пользовательского диска на локальном компьютере:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-hello-vm"></a>Создание виртуальной Машины hello
toocreate виртуальную Машину с неуправляемой дисков, укажите диск tooyour hello URI (`--image`) с [создания виртуальной машины az](/cli/azure/vm#create). Hello следующий пример создает Виртуальную машину с именем `myVM` с помощью виртуального диска hello ранее отправленные:

Укажите hello `--image` параметр с [создания виртуальной машины az](/cli/azure/vm#create) toopoint tooyour пользовательского диска. Убедитесь, что `--storage-account` совпадений hello учетной записи хранилища, где хранятся пользовательские диска. У вас toouse hello одного контейнера как hello toostore пользовательского диска виртуальных машин. Внесите любые дополнительные контейнеры toocreate убедиться, что в hello так же, как hello ранее перед отправкой пользовательского диска.

Hello следующий пример создает Виртуальную машину с именем `myVM` с пользовательской диска:

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

Вы по-прежнему требуется toospecify или ответить на запрос, все hello Дополнительные параметры, необходимые для hello **создания виртуальной машины az** команды, такие как имя пользователя и ключи SSH.


## <a name="resource-manager-template"></a>Шаблон Resource Manager
Шаблоны Azure Resource Manager являются файлами JavaScript Object Notation (JSON), которые определяют среду hello нужно toobuild. шаблоны Hello разбиваются toodifferent поставщиков ресурсов, таких как вычислений или сети. Можно использовать существующие шаблоны или создать собственный. Узнайте больше об [использовании Resource Manager и шаблонов](../../azure-resource-manager/resource-group-overview.md).

В рамках hello `Microsoft.Compute/virtualMachines` у поставщика шаблона `storageProfile` узел, который содержит сведения о конфигурации hello для виртуальной Машины. tooedit Hello двумя основными параметрами, которые являются hello `image` и `vhd` URI, которые точки tooyour пользовательского диска и виртуального диска новой виртуальной Машины. Hello ниже показан пример hello JSON для использования пользовательского диска:

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

Можно использовать [toocreate этот существующий шаблон виртуальной Машины из образа](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) или для чтения о [Создание собственных шаблонов диспетчера ресурсов Azure](../../azure-resource-manager/resource-group-authoring-templates.md). 

После настройки шаблона использовать [создания развертывания группы az](/cli/azure/group/deployment#create) toocreate виртуальных машин. Укажите hello URI шаблона JSON с hello `--template-uri` параметр:

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

Если имеется файл JSON, хранящиеся локально на компьютере, можно использовать hello `--template-file` параметра вместо:

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a>Дальнейшие действия
После подготовки и передачи пользовательского виртуального диска ознакомьтесь с дополнительными сведениями об [использовании Resource Manager и шаблонов](../../azure-resource-manager/resource-group-overview.md). Вы также можете слишком[добавьте диск данных](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour новые виртуальные машины. При наличии приложений, выполняющихся на виртуальные машины, необходимо tooaccess, нужно убедиться, что слишком[открыть порты и конечные точки](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

