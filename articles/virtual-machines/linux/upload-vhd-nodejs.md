---
title: "aaaUpload пользовательского образа Linux с помощью Azure CLI 1.0 | Документы Microsoft"
description: "Создание и отправка tooAzure виртуального жесткого диска (VHD) с помощью образа Linux с помощью модели развертывания диспетчера ресурсов hello и hello Azure CLI 1.0."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/10/2016
ms.author: iainfou
ms.openlocfilehash: 0bbd232debee1e632233d1c010e388dbc1548bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-hello-azure-cli-10"></a>Передача и создание виртуальной Машины Linux из пользовательского образа с помощью hello Azure CLI 1.0
В этой статье показано, как tooupload tooAzure виртуального жесткого диска (VHD) с помощью hello модели развертывания диспетчера ресурсов и создания виртуальных машин Linux из этого образа. Эта функция позволяет вам tooinstall и настройте требования tooyour дистрибутив Linux и затем использовать этот виртуальный жесткий ДИСК tooquickly создания виртуальных машин (ВМ) Azure.


## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI
Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

- [Azure CLI 1.0](#quick-commands) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)
- [Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -нашей нового поколения CLI для модели развертывания hello ресурсов управления


## <a name="quick-commands"></a>Быстрые команды
При необходимости tooquickly выполнения задачи hello, hello следующий раздел сведения hello базовые команды tooupload tooAzure виртуальной Машины. Более подробные сведения и контекста, для каждого шага можно найти hello остальной части документа hello [начиная здесь](#requirements).

Убедитесь, что [hello Azure CLI 1.0](../../cli-install-nodejs.md) входа в систему и использование режима диспетчера ресурсов:

```azurecli
azure config mode arm
```

В hello следующих примерах замените примеры имен параметров собственные значения. Используемые имена параметров — `myResourceGroup`, `mystorageaccount`, и `myimages`.

Сначала создайте группу ресурсов. Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `WestUs` расположение:

```azurecli
azure group create myResourceGroup --location "WestUS"
```

Создание учетной записи хранилища toohold виртуальных дисков. Hello следующий пример создает учетную запись хранения с именем `mystorageaccount`:

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

Список hello ключи доступа для учетной записи хранилища. Запишите `key1`:

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

Создание контейнера в учетной записи хранилища с помощью ключа хранилища hello, который был получен. Hello следующий пример создает контейнер с именем `myimages` с помощью hello значение ключа хранилища из `key1`:

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

И, наконец отправьте созданный контейнер toohello виртуального жесткого диска. Укажите локальный путь hello tooyour виртуальный жесткий ДИСК в разделе `/path/to/disk/mydisk.vhd`:

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

Теперь можно создать виртуальную машину из переданного виртуального диска [с помощью шаблона Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd). Можно также использовать hello CLI, указав hello URI tooyour диска (`--image-urn`). Hello следующий пример создает Виртуальную машину с именем `myVM` с помощью виртуального диска hello ранее отправленные:

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

Hello целевой учетной записью хранения имеет toobe Здравствуйте таким же, как где загруженный виртуальный диск. Также необходимо toospecify или ответить на запрос, все hello Дополнительные параметры, необходимые для hello `azure vm create` команды, такие как виртуальная сеть, общедоступный IP-адрес, имя пользователя и ключи SSH. Вы можете прочитать больше о hello [доступных параметров диспетчера ресурсов CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).

## <a name="requirements"></a>Требования
toocomplete hello следующие действия, необходимо:

* **Операционной системы Linux в VHD-файла** -установка [дистрибутив Linux в одобренных Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (или в разделе [сведения для распределений, отличных от одобренных](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa виртуальный диск в hello виртуального жесткого диска формат. Несколько средств существует toocreate виртуальной Машины и виртуального жесткого диска:
  * Установка и настройка [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) или [KVM](http://www.linux-kvm.org/page/RunningKVM), отвечающий за toouse виртуальный жесткий ДИСК в формате изображения. При необходимости вы можете [преобразовать образ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) с помощью `qemu-img convert`.
  * Кроме того, можно использовать Hyper-V [в Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) или [Windows Server 2012 и 2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Hello более новый формат VHDX не поддерживается в Azure. При создании виртуальной Машины, задайте hello формат виртуального жесткого диска. При необходимости можно преобразовать tooVHD диски VHDX с помощью [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) или hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) командлета PowerShell. Кроме того Azure не поддерживает передачи динамических виртуальных жестких дисков, поэтому требуется tooconvert toostatic такие диски VHD перед отправкой. Можно использовать средства, такие как [утилиты Azure виртуального жесткого диска для GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert динамических дисков во время процесса hello передачи tooAzure.
> 
> 

* Виртуальные машины, созданные из настраиваемого образа необходимо разместить в hello же учетной записи хранилища, само изображение hello
  * Создание хранилища учетной записи и контейнер toohold образ и созданные виртуальные машины
  * После создания всех виртуальных машин можно спокойно удалить образ.

Убедитесь, что [hello Azure CLI 1.0](../../cli-install-nodejs.md) входа в систему и использование режима диспетчера ресурсов:

```azurecli
azure config mode arm
```

В hello следующих примерах замените примеры имен параметров собственные значения. Используемые имена параметров — `myResourceGroup`, `mystorageaccount`, и `myimages`.

<a id="prepimage"> </a>

## <a name="prepare-hello-image-toobe-uploaded"></a>Подготовка toobe изображения hello отправлен
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


## <a name="create-a-resource-group"></a>Создание группы ресурсов
Группы ресурсов логически объединить все toosupport ресурсы Azure hello виртуальных машин, например hello виртуальных сетей и хранилища. Узнайте больше о группах ресурсов Azure [здесь](../../azure-resource-manager/resource-group-overview.md). Перед загрузкой вашего пользовательского образа и создании виртуальных машин, необходимо сначала toocreate группу ресурсов. 

Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `WestUS` расположение:

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a>Создайте учетную запись хранения.
Виртуальные машины хранятся в виде страничных BLOB-объектов в учетной записи хранения. Узнайте больше о хранилище BLOB-объектов Azure [здесь](../../storage/common/storage-introduction.md#blob-storage). Следует создать учетную запись хранения для пользовательского образа диска и виртуальных машин. Все виртуальные машины, создаваемые на основе toobe необходимость образ вашего пользовательского диска, в hello одной учетной записи хранилища, что это изображение.

Hello следующий пример создает учетную запись хранения с именем `mystorageaccount` в ранее созданную группу ресурсов hello:

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a>Вывод списка ключей учетной записи хранения
Azure создает два 512-разрядных ключа доступа для каждой учетной записи хранения. Эти ключи доступа используются при проверке подлинности учетной записи хранилища toohello, например toocarry операций записи. Дополнительные сведения о [управление доступ здесь toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). Можно просмотреть ключи доступа с hello `azure storage account keys list` команды.

Просмотр ключей доступа к hello для hello хранилища созданную учетную запись:

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
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
В hello так же, создания разных каталогах toologically организации локальной файловой системе, создание контейнеров в учетной записи хранилища tooorganize виртуальных дисков и образов. Учетная запись хранения может содержать любое количество контейнеров. 

Hello следующий пример создает контейнер с именем `myimages`, указав ключ доступа hello полученный в предыдущем шаге hello (`key1`):

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a>Передача VHD
Теперь можно передать ваш пользовательский образ диска. Как и любые виртуальные диски виртуальных машин, ваш пользовательский образ диска передается и сохраняется как страничный BLOB-объект.

Укажите ваш ключ доступа, контейнер hello, созданный на предыдущем шаге hello и затем hello путь toohello пользовательского образа на локальном компьютере:

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a>Создание виртуальной машины на основе пользовательского образа
При создании виртуальных машин из вашего пользовательского образа, укажите образ диска toohello URI hello. Убедитесь, что hello совпадений учетной записи хранилища назначения, где хранится образ жесткого диска для пользовательских. Можно создать с помощью hello Azure CLI или JSON диспетчера ресурсов шаблона виртуальной Машины.

### <a name="create-a-vm-using-hello-azure-cli"></a>Создайте виртуальную Машину с помощью hello Azure CLI
Укажите hello `--image-urn` параметр с hello `azure vm create` toopoint команда tooyour пользовательского образа. Убедитесь, что `--storage-account-name` совпадений hello учетной записи хранилища, где хранится образ жесткого диска пользовательских. У вас toouse hello одного контейнера как hello toostore изображение пользовательского диска виртуальных машин. Внесите любые дополнительные контейнеры toocreate убедиться, что в hello так же, как hello ранее перед отправкой диска пользовательских изображений.

Hello следующий пример создает Виртуальную машину с именем `myVM` из вашего пользовательского образа:

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

Вы по-прежнему требуется toospecify или ответить на запрос, все hello Дополнительные параметры, необходимые для hello `azure vm create` команды, такие как виртуальная сеть, общедоступный IP-адрес, имя пользователя и ключи SSH. Дополнительные сведения о hello [доступных параметров диспетчера ресурсов CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).

### <a name="create-a-vm-using-a-json-template"></a>Создание виртуальной машины с помощью шаблона JSON
Шаблоны Azure Resource Manager являются файлами JavaScript Object Notation (JSON), которые определяют среду hello нужно toobuild. шаблоны Hello разбиваются toodifferent поставщиков ресурсов, таких как вычислений или сети. Можно использовать существующие шаблоны или создать собственный. Узнайте больше об [использовании Resource Manager и шаблонов](../../azure-resource-manager/resource-group-overview.md).

В рамках hello `Microsoft.Compute/virtualMachines` у поставщика шаблона `storageProfile` узел, который содержит сведения о конфигурации hello для виртуальной Машины. tooedit Hello двумя основными параметрами, которые являются hello `image` и `vhd` URI, которые точки tooyour пользовательского образа и новой виртуальной Машины виртуальный диск. Hello ниже показан пример hello JSON с помощью пользовательского образа:

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

Можно использовать [toocreate этот существующий шаблон виртуальной Машины из образа](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) или для чтения о [Создание собственных шаблонов диспетчера ресурсов Azure](../../azure-resource-manager/resource-group-authoring-templates.md). 

После настройки шаблона, создания виртуальных машин с помощью hello `azure group deployment create` команды. Укажите hello URI шаблона JSON с hello `--template-uri` параметр:

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

Если имеется файл JSON, хранящиеся локально на компьютере, можно использовать hello `--template-file` параметра вместо:

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a>Дальнейшие действия
После подготовки и передачи пользовательского виртуального диска ознакомьтесь с дополнительными сведениями об [использовании Resource Manager и шаблонов](../../azure-resource-manager/resource-group-overview.md). Вы также можете слишком[добавьте диск данных](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour новые виртуальные машины. При наличии приложений, выполняющихся на виртуальные машины, необходимо tooaccess, нужно убедиться, что слишком[открыть порты и конечные точки](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

