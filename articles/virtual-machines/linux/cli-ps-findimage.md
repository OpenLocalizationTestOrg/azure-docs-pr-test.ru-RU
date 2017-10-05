---
title: "Выбор образов виртуальных машин Linux с помощью Azure CLI | Документация Майкрософт"
description: "Узнайте, как использовать Azure CLI для определения издателя, предложения, номера SKU и версии для образов виртуальных машин из Marketplace."
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
ms.openlocfilehash: e0c27a7ee9e9a7ab1a3b004e070fa556b56a36a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-find-linux-vm-images-in-the-azure-marketplace-with-the-azure-cli"></a><span data-ttu-id="b9312-103">Поиск образов виртуальных машин Linux в Azure Marketplace с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b9312-103">How to find Linux VM images in the Azure Marketplace with the Azure CLI</span></span>
<span data-ttu-id="b9312-104">В этой статье описывается, как с помощью Azure CLI 2.0 находить образы виртуальных машин в Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b9312-104">This topic describes how to use the Azure CLI 2.0 to find VM images in the Azure Marketplace.</span></span> <span data-ttu-id="b9312-105">Воспользуйтесь этими сведениями, чтобы указать образ из Marketplace при создании виртуальной машины Linux.</span><span class="sxs-lookup"><span data-stu-id="b9312-105">Use this information to specify a Marketplace image when you create a Linux VM.</span></span>

<span data-ttu-id="b9312-106">Убедитесь, что у вас установлена последняя версия [Azure CLI 2.0](/cli/azure/install-az-cli2), и войдите в учетную запись Azure с помощью команды `az login`.</span><span class="sxs-lookup"><span data-stu-id="b9312-106">Make sure that you installed the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and are logged in to an Azure account (`az login`).</span></span>

## <a name="terminology"></a><span data-ttu-id="b9312-107">Терминология</span><span class="sxs-lookup"><span data-stu-id="b9312-107">Terminology</span></span>

<span data-ttu-id="b9312-108">Образы Marketplace определяются в интерфейсе командной строки и других инструментах Azure с учетом следующей иерархии:</span><span class="sxs-lookup"><span data-stu-id="b9312-108">Marketplace images are identified in the CLI and other Azure tools according to a hierarchy:</span></span>

* <span data-ttu-id="b9312-109">**Издатель.** Организация, создавшая образ.</span><span class="sxs-lookup"><span data-stu-id="b9312-109">**Publisher** - The organization that created the image.</span></span> <span data-ttu-id="b9312-110">Пример: Canonical.</span><span class="sxs-lookup"><span data-stu-id="b9312-110">Example: Canonical</span></span>
* <span data-ttu-id="b9312-111">**Предложение.** Группа связанных образов, созданных издателем.</span><span class="sxs-lookup"><span data-stu-id="b9312-111">**Offer** - A group of related images created by a publisher.</span></span> <span data-ttu-id="b9312-112">Пример: Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="b9312-112">Example: Ubuntu Server</span></span>
* <span data-ttu-id="b9312-113">**Номер SKU.** Экземпляр предложения, например основной выпуск дистрибутива.</span><span class="sxs-lookup"><span data-stu-id="b9312-113">**SKU** - An instance of an offer, such as a major release of a distribution.</span></span> <span data-ttu-id="b9312-114">Пример: 16.04-LTS.</span><span class="sxs-lookup"><span data-stu-id="b9312-114">Example: 16.04-LTS</span></span>
* <span data-ttu-id="b9312-115">**Версия.** Номер версии образа SKU.</span><span class="sxs-lookup"><span data-stu-id="b9312-115">**Version** - The version number of an image SKU.</span></span> <span data-ttu-id="b9312-116">При указании образа его номер версии можно заменить ключевым словом latest. В этом случае будет выбрана последняя версия дистрибутива.</span><span class="sxs-lookup"><span data-stu-id="b9312-116">When specifying the image, you can replace the version number with "latest", which selects the latest version of the distribution.</span></span>

<span data-ttu-id="b9312-117">Образ Marketplace обычно определяется на основе образа *URN*.</span><span class="sxs-lookup"><span data-stu-id="b9312-117">To specify a Marketplace image, you typically use the image *URN*.</span></span> <span data-ttu-id="b9312-118">В URN эти значения объединены (в качестве разделителя используется двоеточие): *Издатель*:*Предложение*:*Номер SKU*:*Версия*.</span><span class="sxs-lookup"><span data-stu-id="b9312-118">The URN combines these values, separated by the colon (:) character: *Publisher*:*Offer*:*Sku*:*Version*.</span></span> 


## <a name="list-popular-images"></a><span data-ttu-id="b9312-119">Просмотр списка популярных образов</span><span class="sxs-lookup"><span data-stu-id="b9312-119">List popular images</span></span>

<span data-ttu-id="b9312-120">Выполните команду [az vm image list](/cli/azure/vm/image#list) без параметра `--all`, чтобы просмотреть список популярных образов виртуальных машин в Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b9312-120">Run the [az vm image list](/cli/azure/vm/image#list) command, without the `--all` option, to see a list of popular VM images in the Azure Marketplace.</span></span> <span data-ttu-id="b9312-121">Например, чтобы увидеть кэшированный список популярных образов виртуальных машин в формате таблицы, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b9312-121">For example, run the following command to display a cached list of popular images in table format:</span></span>

```azurecli
az vm image list --output table
```

<span data-ttu-id="b9312-122">Выходные данные содержат URN (значение в столбце *URN*). На основе этого значения указывается образ.</span><span class="sxs-lookup"><span data-stu-id="b9312-122">The output includes the URN (the value in the *Urn* column), which you use to specify the image.</span></span> <span data-ttu-id="b9312-123">При создании виртуальной машины с помощью одного из популярных образов Marketplace в качестве альтернативы можно указать псевдоним URN, например *UbuntuLTS*.</span><span class="sxs-lookup"><span data-stu-id="b9312-123">When creating a VM with one of these popular Marketplace images, you can alternatively specify the URN alias, such as *UbuntuLTS*.</span></span>

```
You are viewing an offline list of images, use --all to retrieve an up-to-date list
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

## <a name="find-specific-images"></a><span data-ttu-id="b9312-124">Поиск определенных образов</span><span class="sxs-lookup"><span data-stu-id="b9312-124">Find specific images</span></span>

<span data-ttu-id="b9312-125">Чтобы найти конкретный образ виртуальной машины в Marketplace, выполните команду `az vm image list` с параметром `--all`.</span><span class="sxs-lookup"><span data-stu-id="b9312-125">To find a specific VM image in the Marketplace, use the `az vm image list` command with the `--all` option.</span></span> <span data-ttu-id="b9312-126">Этот процесс занимает некоторое время и может возвращать большие объемы выходных данных. Поэтому вы можете отфильтровать список по `--publisher` или другому параметру.</span><span class="sxs-lookup"><span data-stu-id="b9312-126">This version of the command takes some time to complete and can return lengthy output, so you usually filter the list by `--publisher` or another parameter.</span></span> 

<span data-ttu-id="b9312-127">Например, приведенная ниже команда отображает предложения для Debian (помните, что без параметра `--all` поиск выполняется только в локальном кэше общих образов).</span><span class="sxs-lookup"><span data-stu-id="b9312-127">For example, the following command displays all Debian offers (remember that without the `--all` switch, it only searches the local cache of common images):</span></span>

```azurecli
az vm image list --offer Debian --all --output table 

```

<span data-ttu-id="b9312-128">Частичные выходные данные приведены ниже.</span><span class="sxs-lookup"><span data-stu-id="b9312-128">Partial output:</span></span> 
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

<span data-ttu-id="b9312-129">Примените аналогичные фильтры, используя параметры `--location`, `--publisher` и `--sku`.</span><span class="sxs-lookup"><span data-stu-id="b9312-129">Apply similar filters with the `--location`, `--publisher`, and `--sku` options.</span></span> <span data-ttu-id="b9312-130">Можно даже искать частичные совпадения по фильтру. Так, с помощью параметра `--offer Deb` можно найти все образы Debian.</span><span class="sxs-lookup"><span data-stu-id="b9312-130">You can even perform partial matches on a filter, such as searching for `--offer Deb` to find all Debian images.</span></span>

<span data-ttu-id="b9312-131">Если с помощью параметра `--location` не указать определенное расположение, то по умолчанию возвращаются значения для региона `westus`.</span><span class="sxs-lookup"><span data-stu-id="b9312-131">If you don't specify a particular location with the `--location` option, the values for `westus` are returned by default.</span></span> <span data-ttu-id="b9312-132">(Задайте другое расположение по умолчанию с помощью команды `az configure --defaults location=<location>`.)</span><span class="sxs-lookup"><span data-stu-id="b9312-132">(Set a different default location by running `az configure --defaults location=<location>`.)</span></span>

<span data-ttu-id="b9312-133">Например, следующая команда возвращает список всех номеров SKU для Debian 8 в регионе `westeurope`:</span><span class="sxs-lookup"><span data-stu-id="b9312-133">For example, the following command lists all Debian 8 SKUs in `westeurope`:</span></span>

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

<span data-ttu-id="b9312-134">Частичные выходные данные приведены ниже.</span><span class="sxs-lookup"><span data-stu-id="b9312-134">Partial output:</span></span>

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

## <a name="navigate-the-images"></a><span data-ttu-id="b9312-135">Переход к образам</span><span class="sxs-lookup"><span data-stu-id="b9312-135">Navigate the images</span></span> 
<span data-ttu-id="b9312-136">Еще один способ поиска образа в определенном расположении — это выполнить по-очереди команды [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers) и [az vm image list-skus](/cli/azure/vm/image#list-skus).</span><span class="sxs-lookup"><span data-stu-id="b9312-136">Another way to find an image in a location is to run the [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers), and [az vm image list-skus](/cli/azure/vm/image#list-skus) commands in sequence.</span></span> <span data-ttu-id="b9312-137">С помощью этих команд определяются следующие значения:</span><span class="sxs-lookup"><span data-stu-id="b9312-137">With these commands, you determine these values:</span></span>

1. <span data-ttu-id="b9312-138">Получить список издателей образов.</span><span class="sxs-lookup"><span data-stu-id="b9312-138">List the image publishers.</span></span>
2. <span data-ttu-id="b9312-139">Получить список предложений нужного издателя.</span><span class="sxs-lookup"><span data-stu-id="b9312-139">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="b9312-140">Получить список номеров SKU для требуемого предложения.</span><span class="sxs-lookup"><span data-stu-id="b9312-140">For a given offer, list their SKUs.</span></span>


<span data-ttu-id="b9312-141">Например, следующая команда позволяет получить список издателей образов в расположении "Западная часть США":</span><span class="sxs-lookup"><span data-stu-id="b9312-141">For example, the following command lists the image publishers in the West US location:</span></span>

```azurecli
az vm image list-publishers --location westus --output table
```

<span data-ttu-id="b9312-142">Частичные выходные данные приведены ниже.</span><span class="sxs-lookup"><span data-stu-id="b9312-142">Partial output:</span></span>

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
<span data-ttu-id="b9312-143">Используйте эти сведения, чтобы найти предложения от определенного издателя.</span><span class="sxs-lookup"><span data-stu-id="b9312-143">Use this information to find offers from a specific publisher.</span></span> <span data-ttu-id="b9312-144">Например, если компания Canonical — издатель образов из западной части США, то найти ее предложения можно, выполнив команду `azure vm image list-offers`.</span><span class="sxs-lookup"><span data-stu-id="b9312-144">For example, if Canonical is an image publisher in the West US location, find their offers by running `azure vm image list-offers`.</span></span> <span data-ttu-id="b9312-145">Укажите расположение и издателя, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="b9312-145">Pass the location and the publisher as in the following example:</span></span>

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

<span data-ttu-id="b9312-146">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="b9312-146">Output:</span></span>

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
<span data-ttu-id="b9312-147">Вы видите, что издатель Canonical из западной части США предлагает **UbuntuServer** для Azure.</span><span class="sxs-lookup"><span data-stu-id="b9312-147">You see that in the West US region, Canonical publishes the **UbuntuServer** offer on Azure.</span></span> <span data-ttu-id="b9312-148">Однако нам также нужны номера SKU.</span><span class="sxs-lookup"><span data-stu-id="b9312-148">But what SKUs?</span></span> <span data-ttu-id="b9312-149">Чтобы получить их значения, выполните команду `azure vm image list-skus` и укажите обнаруженные расположение, издателя и предложение:</span><span class="sxs-lookup"><span data-stu-id="b9312-149">To get those values, run `azure vm image list-skus` and set the location, publisher, and offer that you have discovered:</span></span>

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

<span data-ttu-id="b9312-150">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="b9312-150">Output:</span></span>

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

<span data-ttu-id="b9312-151">Наконец, выполните команду `az vm image list`, чтобы найти определенную версию номера SKU, например **16.04-LTS**:</span><span class="sxs-lookup"><span data-stu-id="b9312-151">Finally, use the `az vm image list` command to find a specific version of the SKU you want, for example, **16.04-LTS**:</span></span>

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

<span data-ttu-id="b9312-152">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="b9312-152">Output:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="b9312-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b9312-153">Next steps</span></span>
<span data-ttu-id="b9312-154">Теперь по значению URN мы можем выбрать именно тот образ, который нам нужен.</span><span class="sxs-lookup"><span data-stu-id="b9312-154">Now you can choose precisely the image you want to use by taking note of the URN value.</span></span> <span data-ttu-id="b9312-155">Передайте это значение с параметром `--image` при создании виртуальной машины с помощью команды [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="b9312-155">Pass this value with the `--image` parameter when you create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="b9312-156">Помните, что при необходимости можно заменить номер версии в URN словом latest.</span><span class="sxs-lookup"><span data-stu-id="b9312-156">Remember that you can optionally replace the version number in the URN with "latest".</span></span> <span data-ttu-id="b9312-157">В этом случае всегда будет выбираться последняя версия дистрибутива.</span><span class="sxs-lookup"><span data-stu-id="b9312-157">This version is always the latest version of the distribution.</span></span> <span data-ttu-id="b9312-158">Инструкции по быстрому созданию виртуальной машины на основе данных URN см. в статье [Создание виртуальных машин Linux и управление ими с помощью Azure CLI](tutorial-manage-vm.md).</span><span class="sxs-lookup"><span data-stu-id="b9312-158">To create a virtual machine quickly by using the URN information, see [Create and Manage Linux VMs with the Azure CLI](tutorial-manage-vm.md).</span></span>
