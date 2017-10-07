---
title: "aaaSelect образы виртуальных Машин Linux, с hello Azure CLI | Документы Microsoft"
description: "Узнайте, как toouse hello Azure CLI toodetermine hello издателя, предложение, SKU и версия для образов виртуальных Машин Marketplace."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7a858e38-4f17-4e8e-a28a-c7f801101721
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/24/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0b115b8654bc156b5bfadba53a6b002a105acb68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-linux-vm-images-in-hello-azure-marketplace-with-hello-azure-cli"></a>Как образы виртуальных Машин Linux toofind в hello Azure Marketplace с hello Azure CLI
В этом разделе описывается, как toouse hello образов виртуальных Машин Azure CLI 2.0 toofind в hello Azure Marketplace. При создании виртуальной Машины Linux, используйте этот сведения toospecify образа Marketplace.

Убедитесь, что последняя версия установлена hello [Azure CLI 2.0](/cli/azure/install-az-cli2) и регистрируются в tooan учетная запись Azure (`az login`).

## <a name="terminology"></a>Терминология

Marketplace образов идентифицируются в hello CLI и другие средства Azure в соответствии с tooa иерархии:

* **Издатель** -hello организация, создавшие hello изображения. Пример: Canonical.
* **Предложение.** Группа связанных образов, созданных издателем. Пример: Ubuntu Server.
* **Номер SKU.** Экземпляр предложения, например основной выпуск дистрибутива. Пример: 16.04-LTS.
* **Версия** -hello номер версии образа SKU. При указании изображения hello, можно заменить hello номер версии с «последние», который выбирает последнюю версию hello hello распространения.

toospecify образа Marketplace, обычно используется изображение hello *URN*. Hello URN объединяет этих значений, разделенных символом двоеточия (:) hello: *издатель*:*предлагают*:*Sku*:*версии*. 


## <a name="list-popular-images"></a>Просмотр списка популярных образов

Запустите hello [списка изображений ВМ az](/cli/azure/vm/image#list) команду без hello `--all` параметр, toosee образы список популярных ВМ в Azure Marketplace hello. Например выполните следующие команды toodisplay hello кэшированный список популярных образов в табличном формате:

```azurecli
az vm image list --output table
```

Вывод Hello включает hello URN (hello значение в hello *Urn* столбца), который вы используете образ toospecify hello. При создании виртуальной Машины с одним из этих популярных Marketplace образов, в качестве альтернативы такие как указать псевдоним URN hello, *UbuntuLTS*.

```
You are viewing an offline list of images, use --all tooretrieve an up-to-date list
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
...
```

## <a name="find-specific-images"></a>Поиск определенных образов

toofind конкретных образа виртуальной Машины в hello Marketplace, использовать hello `az vm image list` с hello `--all` параметр. Этот вариант команды hello занимает некоторое время toocomplete и может возвращать длинных выходных данных, поэтому вы обычно фильтровать список hello по `--publisher` или другого параметра. 

Например, hello, следующая команда отображает все предложения Debian (следует помнить, что без hello `--all` переключиться, поиск выполняется только локальный кэш hello общих образов):

```azurecli
az vm image list --offer Debian --all --output table 

```

Частичные выходные данные приведены ниже. 
```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  --------------
Debian   credativ     7                  credativ:Debian:7:7.0.201602010                  7.0.201602010
Debian   credativ     7                  credativ:Debian:7:7.0.201603020                  7.0.201603020
Debian   credativ     7                  credativ:Debian:7:7.0.201604050                  7.0.201604050
Debian   credativ     7                  credativ:Debian:7:7.0.201604200                  7.0.201604200
Debian   credativ     7                  credativ:Debian:7:7.0.201606280                  7.0.201606280
Debian   credativ     7                  credativ:Debian:7:7.0.201609120                  7.0.201609120
Debian   credativ     7                  credativ:Debian:7:7.0.201611020                  7.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
Debian   credativ     8                  credativ:Debian:8:8.0.201708040                  8.0.201708040
...
```

Применяются аналогичные фильтров с hello `--location`, `--publisher`, и `--sku` параметры. Можно даже выполнять частичные совпадения в фильтре; например, поиск `--offer Deb` toofind все Debian изображения.

Если не указать определенное место с hello `--location` , hello значения параметров для `westus` возвращаются по умолчанию. (Задайте другое расположение по умолчанию с помощью команды `az configure --defaults location=<location>`.)

Например, следующую команду hello перечислены все Debian номера SKU 8 в `westeurope`:

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

Частичные выходные данные приведены ниже.

```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  -------------
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
...
```

## <a name="navigate-hello-images"></a>Перейдите hello изображений 
Другой способ toofind изображения в расположении — toorun hello [образ виртуальной машины az список от издателей](/cli/azure/vm/image#list-publishers), [образ виртуальной машины az список предложений](/cli/azure/vm/image#list-offers), и [az ВМ образа списка SKU по](/cli/azure/vm/image#list-skus) команд в последовательности. С помощью этих команд определяются следующие значения:

1. Список hello изображения издателей.
2. Получить список предложений нужного издателя.
3. Получить список номеров SKU для требуемого предложения.


Например, hello следующая команда выводит список издателей изображения hello в hello расположение Западная часть США:

```azurecli
az vm image list-publishers --location westus --output table
```

Частичные выходные данные приведены ниже.

```
Location    Name
----------  ----------------------------------------------------
westus      1e
westus      4psa
westus      7isolutions
westus      a10networks
westus      abiquo
westus      accellion
westus      Acronis
westus      Acronis.Backup
westus      actian_matrix
westus      actifio
westus      activeeon
westus      adatao
...
```
Используйте этот toofind сведения предлагает с определенным издателем. Например, если канонические издателя образа в hello расположение Запад США, найти их предложений, запустив `azure vm image list-offers`. Передайте расположение hello и издатель hello как hello в следующем примере:

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

Выходные данные:

```
Location    Name
----------  -------------------------
westus      Ubuntu15.04Snappy
westus      Ubuntu15.04SnappyDocker
westus      UbunturollingSnappy
westus      UbuntuServer
westus      Ubuntu_Core
westus      Ubuntu_Snappy_Core
westus      Ubuntu_Snappy_Core_Docker
```
Вы видите, что в области Запад США hello канонические публикует hello **UbuntuServer** предлагают в Azure. Но какие? Запустите эти значения tooget `azure vm image list-skus` и задайте расположение hello, издателя и предложения, выполнить обнаружение:

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

Выходные данные:

```
Location    Name
----------  -----------------
westus      12.04.3-LTS
westus      12.04.4-LTS
westus      12.04.5-DAILY-LTS
westus      12.04.5-LTS
westus      12.10
westus      14.04.0-LTS
westus      14.04.1-LTS
westus      14.04.2-LTS
westus      14.04.3-LTS
westus      14.04.4-LTS
westus      14.04.5-DAILY-LTS
westus      14.04.5-LTS
westus      16.04-beta
westus      16.04-DAILY-LTS
westus      16.04-LTS
westus      16.04.0-LTS
westus      16.10
westus      16.10-DAILY
westus      17.04
westus      17.04-DAILY
westus      17.10-DAILY
```

Наконец, используйте hello `az vm image list` toofind команда конкретной версии hello SKU, требуется, например, **16.04 LTS**:

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

Выходные данные:

```
Offer         Publisher    Sku        Urn                                               Version
------------  -----------  ---------  ------------------------------------------------  ---------------
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611220  16.04.201611220
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611300  16.04.201611300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612050  16.04.201612050
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612140  16.04.201612140
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612210  16.04.201612210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201701130  16.04.201701130
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702020  16.04.201702020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702200  16.04.201702200
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702210  16.04.201702210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702240  16.04.201702240
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703020  16.04.201703020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703030  16.04.201703030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703070  16.04.201703070
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703270  16.04.201703270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703280  16.04.201703280
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703300  16.04.201703300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705080  16.04.201705080
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705160  16.04.201705160
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706100  16.04.201706100
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706191  16.04.201706191
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707210  16.04.201707210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707270  16.04.201707270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708030  16.04.201708030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708110  16.04.201708110
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708151  16.04.201708151
```
## <a name="next-steps"></a>Дальнейшие действия
Теперь вы можете точно hello образа необходимо toouse путем перевода заметку hello значение универсального имени РЕСУРСА. Передает это значение с hello `--image` параметр при создании виртуальной Машины с hello [создания виртуальной машины az](/cli/azure/vm#create) команды. Помните, что можно при необходимости заменить hello номер версии в hello URN «последней». Эта версия всегда является последней версии hello hello распределения. toocreate виртуальной машины быстро с помощью hello URN сведения см. в разделе [Создание и управление виртуальными машинами Linux с hello Azure CLI](tutorial-manage-vm.md).
