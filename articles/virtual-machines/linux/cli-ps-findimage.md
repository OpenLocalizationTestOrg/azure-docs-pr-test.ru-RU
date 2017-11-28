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
# <a name="how-toofind-linux-vm-images-in-hello-azure-marketplace-with-hello-azure-cli"></a><span data-ttu-id="444d4-103">Как образы виртуальных Машин Linux toofind в hello Azure Marketplace с hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="444d4-103">How toofind Linux VM images in hello Azure Marketplace with hello Azure CLI</span></span>
<span data-ttu-id="444d4-104">В этом разделе описывается, как toouse hello образов виртуальных Машин Azure CLI 2.0 toofind в hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="444d4-104">This topic describes how toouse hello Azure CLI 2.0 toofind VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="444d4-105">При создании виртуальной Машины Linux, используйте этот сведения toospecify образа Marketplace.</span><span class="sxs-lookup"><span data-stu-id="444d4-105">Use this information toospecify a Marketplace image when you create a Linux VM.</span></span>

<span data-ttu-id="444d4-106">Убедитесь, что последняя версия установлена hello [Azure CLI 2.0](/cli/azure/install-az-cli2) и регистрируются в tooan учетная запись Azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="444d4-106">Make sure that you installed hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and are logged in tooan Azure account (`az login`).</span></span>

## <a name="terminology"></a><span data-ttu-id="444d4-107">Терминология</span><span class="sxs-lookup"><span data-stu-id="444d4-107">Terminology</span></span>

<span data-ttu-id="444d4-108">Marketplace образов идентифицируются в hello CLI и другие средства Azure в соответствии с tooa иерархии:</span><span class="sxs-lookup"><span data-stu-id="444d4-108">Marketplace images are identified in hello CLI and other Azure tools according tooa hierarchy:</span></span>

* <span data-ttu-id="444d4-109">**Издатель** -hello организация, создавшие hello изображения.</span><span class="sxs-lookup"><span data-stu-id="444d4-109">**Publisher** - hello organization that created hello image.</span></span> <span data-ttu-id="444d4-110">Пример: Canonical.</span><span class="sxs-lookup"><span data-stu-id="444d4-110">Example: Canonical</span></span>
* <span data-ttu-id="444d4-111">**Предложение.** Группа связанных образов, созданных издателем.</span><span class="sxs-lookup"><span data-stu-id="444d4-111">**Offer** - A group of related images created by a publisher.</span></span> <span data-ttu-id="444d4-112">Пример: Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="444d4-112">Example: Ubuntu Server</span></span>
* <span data-ttu-id="444d4-113">**Номер SKU.** Экземпляр предложения, например основной выпуск дистрибутива.</span><span class="sxs-lookup"><span data-stu-id="444d4-113">**SKU** - An instance of an offer, such as a major release of a distribution.</span></span> <span data-ttu-id="444d4-114">Пример: 16.04-LTS.</span><span class="sxs-lookup"><span data-stu-id="444d4-114">Example: 16.04-LTS</span></span>
* <span data-ttu-id="444d4-115">**Версия** -hello номер версии образа SKU.</span><span class="sxs-lookup"><span data-stu-id="444d4-115">**Version** - hello version number of an image SKU.</span></span> <span data-ttu-id="444d4-116">При указании изображения hello, можно заменить hello номер версии с «последние», который выбирает последнюю версию hello hello распространения.</span><span class="sxs-lookup"><span data-stu-id="444d4-116">When specifying hello image, you can replace hello version number with "latest", which selects hello latest version of hello distribution.</span></span>

<span data-ttu-id="444d4-117">toospecify образа Marketplace, обычно используется изображение hello *URN*.</span><span class="sxs-lookup"><span data-stu-id="444d4-117">toospecify a Marketplace image, you typically use hello image *URN*.</span></span> <span data-ttu-id="444d4-118">Hello URN объединяет этих значений, разделенных символом двоеточия (:) hello: *издатель*:*предлагают*:*Sku*:*версии*.</span><span class="sxs-lookup"><span data-stu-id="444d4-118">hello URN combines these values, separated by hello colon (:) character: *Publisher*:*Offer*:*Sku*:*Version*.</span></span> 


## <a name="list-popular-images"></a><span data-ttu-id="444d4-119">Просмотр списка популярных образов</span><span class="sxs-lookup"><span data-stu-id="444d4-119">List popular images</span></span>

<span data-ttu-id="444d4-120">Запустите hello [списка изображений ВМ az](/cli/azure/vm/image#list) команду без hello `--all` параметр, toosee образы список популярных ВМ в Azure Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="444d4-120">Run hello [az vm image list](/cli/azure/vm/image#list) command, without hello `--all` option, toosee a list of popular VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="444d4-121">Например выполните следующие команды toodisplay hello кэшированный список популярных образов в табличном формате:</span><span class="sxs-lookup"><span data-stu-id="444d4-121">For example, run hello following command toodisplay a cached list of popular images in table format:</span></span>

```azurecli
az vm image list --output table
```

<span data-ttu-id="444d4-122">Вывод Hello включает hello URN (hello значение в hello *Urn* столбца), который вы используете образ toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="444d4-122">hello output includes hello URN (hello value in hello *Urn* column), which you use toospecify hello image.</span></span> <span data-ttu-id="444d4-123">При создании виртуальной Машины с одним из этих популярных Marketplace образов, в качестве альтернативы такие как указать псевдоним URN hello, *UbuntuLTS*.</span><span class="sxs-lookup"><span data-stu-id="444d4-123">When creating a VM with one of these popular Marketplace images, you can alternatively specify hello URN alias, such as *UbuntuLTS*.</span></span>

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

## <a name="find-specific-images"></a><span data-ttu-id="444d4-124">Поиск определенных образов</span><span class="sxs-lookup"><span data-stu-id="444d4-124">Find specific images</span></span>

<span data-ttu-id="444d4-125">toofind конкретных образа виртуальной Машины в hello Marketplace, использовать hello `az vm image list` с hello `--all` параметр.</span><span class="sxs-lookup"><span data-stu-id="444d4-125">toofind a specific VM image in hello Marketplace, use hello `az vm image list` command with hello `--all` option.</span></span> <span data-ttu-id="444d4-126">Этот вариант команды hello занимает некоторое время toocomplete и может возвращать длинных выходных данных, поэтому вы обычно фильтровать список hello по `--publisher` или другого параметра.</span><span class="sxs-lookup"><span data-stu-id="444d4-126">This version of hello command takes some time toocomplete and can return lengthy output, so you usually filter hello list by `--publisher` or another parameter.</span></span> 

<span data-ttu-id="444d4-127">Например, hello, следующая команда отображает все предложения Debian (следует помнить, что без hello `--all` переключиться, поиск выполняется только локальный кэш hello общих образов):</span><span class="sxs-lookup"><span data-stu-id="444d4-127">For example, hello following command displays all Debian offers (remember that without hello `--all` switch, it only searches hello local cache of common images):</span></span>

```azurecli
az vm image list --offer Debian --all --output table 

```

<span data-ttu-id="444d4-128">Частичные выходные данные приведены ниже.</span><span class="sxs-lookup"><span data-stu-id="444d4-128">Partial output:</span></span> 
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

<span data-ttu-id="444d4-129">Применяются аналогичные фильтров с hello `--location`, `--publisher`, и `--sku` параметры.</span><span class="sxs-lookup"><span data-stu-id="444d4-129">Apply similar filters with hello `--location`, `--publisher`, and `--sku` options.</span></span> <span data-ttu-id="444d4-130">Можно даже выполнять частичные совпадения в фильтре; например, поиск `--offer Deb` toofind все Debian изображения.</span><span class="sxs-lookup"><span data-stu-id="444d4-130">You can even perform partial matches on a filter, such as searching for `--offer Deb` toofind all Debian images.</span></span>

<span data-ttu-id="444d4-131">Если не указать определенное место с hello `--location` , hello значения параметров для `westus` возвращаются по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="444d4-131">If you don't specify a particular location with hello `--location` option, hello values for `westus` are returned by default.</span></span> <span data-ttu-id="444d4-132">(Задайте другое расположение по умолчанию с помощью команды `az configure --defaults location=<location>`.)</span><span class="sxs-lookup"><span data-stu-id="444d4-132">(Set a different default location by running `az configure --defaults location=<location>`.)</span></span>

<span data-ttu-id="444d4-133">Например, следующую команду hello перечислены все Debian номера SKU 8 в `westeurope`:</span><span class="sxs-lookup"><span data-stu-id="444d4-133">For example, hello following command lists all Debian 8 SKUs in `westeurope`:</span></span>

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

<span data-ttu-id="444d4-134">Частичные выходные данные приведены ниже.</span><span class="sxs-lookup"><span data-stu-id="444d4-134">Partial output:</span></span>

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

## <a name="navigate-hello-images"></a><span data-ttu-id="444d4-135">Перейдите hello изображений</span><span class="sxs-lookup"><span data-stu-id="444d4-135">Navigate hello images</span></span> 
<span data-ttu-id="444d4-136">Другой способ toofind изображения в расположении — toorun hello [образ виртуальной машины az список от издателей](/cli/azure/vm/image#list-publishers), [образ виртуальной машины az список предложений](/cli/azure/vm/image#list-offers), и [az ВМ образа списка SKU по](/cli/azure/vm/image#list-skus) команд в последовательности.</span><span class="sxs-lookup"><span data-stu-id="444d4-136">Another way toofind an image in a location is toorun hello [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers), and [az vm image list-skus](/cli/azure/vm/image#list-skus) commands in sequence.</span></span> <span data-ttu-id="444d4-137">С помощью этих команд определяются следующие значения:</span><span class="sxs-lookup"><span data-stu-id="444d4-137">With these commands, you determine these values:</span></span>

1. <span data-ttu-id="444d4-138">Список hello изображения издателей.</span><span class="sxs-lookup"><span data-stu-id="444d4-138">List hello image publishers.</span></span>
2. <span data-ttu-id="444d4-139">Получить список предложений нужного издателя.</span><span class="sxs-lookup"><span data-stu-id="444d4-139">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="444d4-140">Получить список номеров SKU для требуемого предложения.</span><span class="sxs-lookup"><span data-stu-id="444d4-140">For a given offer, list their SKUs.</span></span>


<span data-ttu-id="444d4-141">Например, hello следующая команда выводит список издателей изображения hello в hello расположение Западная часть США:</span><span class="sxs-lookup"><span data-stu-id="444d4-141">For example, hello following command lists hello image publishers in hello West US location:</span></span>

```azurecli
az vm image list-publishers --location westus --output table
```

<span data-ttu-id="444d4-142">Частичные выходные данные приведены ниже.</span><span class="sxs-lookup"><span data-stu-id="444d4-142">Partial output:</span></span>

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
<span data-ttu-id="444d4-143">Используйте этот toofind сведения предлагает с определенным издателем.</span><span class="sxs-lookup"><span data-stu-id="444d4-143">Use this information toofind offers from a specific publisher.</span></span> <span data-ttu-id="444d4-144">Например, если канонические издателя образа в hello расположение Запад США, найти их предложений, запустив `azure vm image list-offers`.</span><span class="sxs-lookup"><span data-stu-id="444d4-144">For example, if Canonical is an image publisher in hello West US location, find their offers by running `azure vm image list-offers`.</span></span> <span data-ttu-id="444d4-145">Передайте расположение hello и издатель hello как hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="444d4-145">Pass hello location and hello publisher as in hello following example:</span></span>

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

<span data-ttu-id="444d4-146">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="444d4-146">Output:</span></span>

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
<span data-ttu-id="444d4-147">Вы видите, что в области Запад США hello канонические публикует hello **UbuntuServer** предлагают в Azure.</span><span class="sxs-lookup"><span data-stu-id="444d4-147">You see that in hello West US region, Canonical publishes hello **UbuntuServer** offer on Azure.</span></span> <span data-ttu-id="444d4-148">Но какие? Запустите эти значения tooget `azure vm image list-skus` и задайте расположение hello, издателя и предложения, выполнить обнаружение:</span><span class="sxs-lookup"><span data-stu-id="444d4-148">But what SKUs? tooget those values, run `azure vm image list-skus` and set hello location, publisher, and offer that you have discovered:</span></span>

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

<span data-ttu-id="444d4-149">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="444d4-149">Output:</span></span>

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

<span data-ttu-id="444d4-150">Наконец, используйте hello `az vm image list` toofind команда конкретной версии hello SKU, требуется, например, **16.04 LTS**:</span><span class="sxs-lookup"><span data-stu-id="444d4-150">Finally, use hello `az vm image list` command toofind a specific version of hello SKU you want, for example, **16.04-LTS**:</span></span>

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

<span data-ttu-id="444d4-151">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="444d4-151">Output:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="444d4-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="444d4-152">Next steps</span></span>
<span data-ttu-id="444d4-153">Теперь вы можете точно hello образа необходимо toouse путем перевода заметку hello значение универсального имени РЕСУРСА.</span><span class="sxs-lookup"><span data-stu-id="444d4-153">Now you can choose precisely hello image you want toouse by taking note of hello URN value.</span></span> <span data-ttu-id="444d4-154">Передает это значение с hello `--image` параметр при создании виртуальной Машины с hello [создания виртуальной машины az](/cli/azure/vm#create) команды.</span><span class="sxs-lookup"><span data-stu-id="444d4-154">Pass this value with hello `--image` parameter when you create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="444d4-155">Помните, что можно при необходимости заменить hello номер версии в hello URN «последней».</span><span class="sxs-lookup"><span data-stu-id="444d4-155">Remember that you can optionally replace hello version number in hello URN with "latest".</span></span> <span data-ttu-id="444d4-156">Эта версия всегда является последней версии hello hello распределения.</span><span class="sxs-lookup"><span data-stu-id="444d4-156">This version is always hello latest version of hello distribution.</span></span> <span data-ttu-id="444d4-157">toocreate виртуальной машины быстро с помощью hello URN сведения см. в разделе [Создание и управление виртуальными машинами Linux с hello Azure CLI](tutorial-manage-vm.md).</span><span class="sxs-lookup"><span data-stu-id="444d4-157">toocreate a virtual machine quickly by using hello URN information, see [Create and Manage Linux VMs with hello Azure CLI](tutorial-manage-vm.md).</span></span>
