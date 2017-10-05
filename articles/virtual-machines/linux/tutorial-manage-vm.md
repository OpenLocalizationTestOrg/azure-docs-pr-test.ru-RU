---
title: "Создание виртуальных машин Linux и управление ими с помощью Azure CLI | Документация Майкрософт"
description: "Руководство по созданию виртуальных машин Linux и управлению ими с помощью Azure CLI."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c163c715eb1438a0d6b0ab53cbb43816ca8dbbb4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-manage-linux-vms-with-the-azure-cli"></a><span data-ttu-id="c409f-103">Создание виртуальных машин Linux и управление ими с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c409f-103">Create and Manage Linux VMs with the Azure CLI</span></span>

<span data-ttu-id="c409f-104">Виртуальные машины Azure предоставляют полностью настраиваемую и гибкую вычислительную среду.</span><span class="sxs-lookup"><span data-stu-id="c409f-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="c409f-105">В этом руководстве рассматриваются основные элементы развертывания виртуальной машины Azure, например выбор ее размера, образа и ее развертывание.</span><span class="sxs-lookup"><span data-stu-id="c409f-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="c409f-106">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="c409f-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c409f-107">Создание виртуальной машины и подключение к ней</span><span class="sxs-lookup"><span data-stu-id="c409f-107">Create and connect to a VM</span></span>
> * <span data-ttu-id="c409f-108">Выбор и использование образов виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="c409f-108">Select and use VM images</span></span>
> * <span data-ttu-id="c409f-109">Просмотр и использование определенных размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="c409f-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="c409f-110">Изменение размера виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c409f-110">Resize a VM</span></span>
> * <span data-ttu-id="c409f-111">Просмотр виртуальной машины и оценка ее состояния</span><span class="sxs-lookup"><span data-stu-id="c409f-111">View and understand VM state</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c409f-112">Если вы решили установить и использовать интерфейс командной строки локально, то для работы с этим руководством вам понадобится Azure CLI 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="c409f-112">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="c409f-113">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="c409f-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="c409f-114">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c409f-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-resource-group"></a><span data-ttu-id="c409f-115">Создать группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="c409f-115">Create resource group</span></span>

<span data-ttu-id="c409f-116">Создайте группу ресурсов с помощью команды [az group create](https://docs.microsoft.com/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c409f-116">Create a resource group with the [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="c409f-117">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="c409f-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="c409f-118">Группу ресурсов следует создавать до виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c409f-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="c409f-119">В этом примере создается группа ресурсов с именем *myResourceGroupVM* в регионе *eastus*.</span><span class="sxs-lookup"><span data-stu-id="c409f-119">In this example, a resource group named *myResourceGroupVM* is created in the *eastus* region.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

<span data-ttu-id="c409f-120">Группа ресурсов указывается при создании или изменении виртуальной машины, что показывается в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="c409f-120">The resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="c409f-121">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c409f-121">Create virtual machine</span></span>

<span data-ttu-id="c409f-122">Создайте виртуальную машину, выполнив команду [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="c409f-122">Create a virtual machine with the [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="c409f-123">При создании виртуальной машины доступно несколько вариантов, таких как образ операционной системы, определение размера диска и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="c409f-123">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="c409f-124">В этом примере создается виртуальная машина *myVM* под управлением Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="c409f-124">In this example, a virtual machine is created with a name of *myVM* running Ubuntu Server.</span></span> 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="c409f-125">После создания виртуальной машины Azure CLI выводит информацию о ней.</span><span class="sxs-lookup"><span data-stu-id="c409f-125">Once the VM has been created, the Azure CLI outputs information about the VM.</span></span> <span data-ttu-id="c409f-126">Запишите `publicIpAddress`. Этот адрес может использоваться для доступа к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c409f-126">Take note of the `publicIpAddress`, this address can be used to access the virtual machine..</span></span> 

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroupVM"
}
```

## <a name="connect-to-vm"></a><span data-ttu-id="c409f-127">Подключение к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="c409f-127">Connect to VM</span></span>

<span data-ttu-id="c409f-128">Теперь к виртуальной машине можно подключиться по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="c409f-128">You can now connect to the VM using SSH.</span></span> <span data-ttu-id="c409f-129">Замените IP-адрес в примере адресом `publicIpAddress`, записанным на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="c409f-129">Replace the example IP address with the `publicIpAddress` noted in the previous step.</span></span>

```bash
ssh 52.174.34.95
```

<span data-ttu-id="c409f-130">Завершив работу с виртуальной машиной, закройте сеанс SSH.</span><span class="sxs-lookup"><span data-stu-id="c409f-130">Once finished with the VM, close the SSH session.</span></span> 

```bash
exit
```

## <a name="understand-vm-images"></a><span data-ttu-id="c409f-131">Описание образов виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="c409f-131">Understand VM images</span></span>

<span data-ttu-id="c409f-132">Azure Marketplace содержит множество образов, которые можно использовать для создания виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="c409f-132">The Azure marketplace includes many images that can be used to create VMs.</span></span> <span data-ttu-id="c409f-133">На предыдущих шагах виртуальная машина создавалась с помощью образа Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c409f-133">In the previous steps, a virtual machine was created using an Ubuntu image.</span></span> <span data-ttu-id="c409f-134">На этом шаге Azure CLI используется для поиска на сайте Marketplace образа CentOS, который затем используется для развертывания второй виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c409f-134">In this step, the Azure CLI is used to search the marketplace for a CentOS image, which is then used to deploy a second virtual machine.</span></span>  

<span data-ttu-id="c409f-135">Чтобы просмотреть список наиболее часто используемых образов, используйте команду [az vm image list](/cli/azure/vm/image#list).</span><span class="sxs-lookup"><span data-stu-id="c409f-135">To see a list of the most commonly used images, use the [az vm image list](/cli/azure/vm/image#list) command.</span></span>

```azurecli-interactive 
az vm image list --output table
```

<span data-ttu-id="c409f-136">Она отобразит наиболее популярные образы виртуальных машин в Azure.</span><span class="sxs-lookup"><span data-stu-id="c409f-136">The command output returns the most popular VM images on Azure.</span></span>

```bash
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2016-Datacenter     MicrosoftWindowsServer:WindowsServer:2016-Datacenter:latest     Win2016Datacenter    latest
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
```

<span data-ttu-id="c409f-137">Получить полный список можно, добавив аргумент `--all`.</span><span class="sxs-lookup"><span data-stu-id="c409f-137">A full list can be seen by adding the `--all` argument.</span></span> <span data-ttu-id="c409f-138">Кроме того, список образов можно отфильтровать по издателю или предложению с помощью аргумента `--publisher` или `–-offer` соответственно.</span><span class="sxs-lookup"><span data-stu-id="c409f-138">The image list can also be filtered by `--publisher` or `–-offer`.</span></span> <span data-ttu-id="c409f-139">В этом примере список образов отфильтрован по предложению *CentOS*.</span><span class="sxs-lookup"><span data-stu-id="c409f-139">In this example, the list is filtered for all images with an offer that matches *CentOS*.</span></span> 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

<span data-ttu-id="c409f-140">Частичные выходные данные приведены ниже.</span><span class="sxs-lookup"><span data-stu-id="c409f-140">Partial output:</span></span>

```azurecli-interactive 
Offer             Publisher         Sku   Urn                                     Version
----------------  ----------------  ----  --------------------------------------  -----------
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201501         6.5.201501
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201503         6.5.201503
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201506         6.5.201506
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20150904       6.5.20150904
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20160309       6.5.20160309
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20170207       6.5.20170207
```

<span data-ttu-id="c409f-141">Чтобы развернуть виртуальную машину с помощью определенного образа, запишите значение в столбце *Urn*.</span><span class="sxs-lookup"><span data-stu-id="c409f-141">To deploy a VM using a specific image, take note of the value in the *Urn* column.</span></span> <span data-ttu-id="c409f-142">При указании образа его номер версии можно заменить ключевым словом latest. В этом случае будет выбрана последняя версия дистрибутива.</span><span class="sxs-lookup"><span data-stu-id="c409f-142">When specifying the image, the image version number can be replaced with “latest”, which selects the latest version of the distribution.</span></span> <span data-ttu-id="c409f-143">В данном примере добавлен аргумент `--image`, чтобы указать последнюю версию образа CentOS 6.5.</span><span class="sxs-lookup"><span data-stu-id="c409f-143">In this example, the `--image` argument is used to specify the latest version of a CentOS 6.5 image.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="c409f-144">Описание размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="c409f-144">Understand VM sizes</span></span>

<span data-ttu-id="c409f-145">Размер виртуальной машины определяет количество выделяемых ей вычислительных ресурсов, таких как ЦП, GPU и память.</span><span class="sxs-lookup"><span data-stu-id="c409f-145">A virtual machine size determines the amount of compute resources such as CPU, GPU, and memory that are made available to the virtual machine.</span></span> <span data-ttu-id="c409f-146">Размеры виртуальных машин должны соответствовать ожидаемой рабочей нагрузке.</span><span class="sxs-lookup"><span data-stu-id="c409f-146">Virtual machines need to be sized appropriately for the expected work load.</span></span> <span data-ttu-id="c409f-147">При увеличении рабочей нагрузки размер существующей виртуальной машины может быть изменен.</span><span class="sxs-lookup"><span data-stu-id="c409f-147">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="c409f-148">Размеры виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="c409f-148">VM Sizes</span></span>

<span data-ttu-id="c409f-149">В приведенной ниже таблицы указаны категории размеров и примеры использования.</span><span class="sxs-lookup"><span data-stu-id="c409f-149">The following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="c409f-150">Тип</span><span class="sxs-lookup"><span data-stu-id="c409f-150">Type</span></span>                     | <span data-ttu-id="c409f-151">Размеры</span><span class="sxs-lookup"><span data-stu-id="c409f-151">Sizes</span></span>           |    <span data-ttu-id="c409f-152">Описание</span><span class="sxs-lookup"><span data-stu-id="c409f-152">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="c409f-153">Универсальные</span><span class="sxs-lookup"><span data-stu-id="c409f-153">General purpose</span></span>](sizes-general.md)         |<span data-ttu-id="c409f-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0–7</span><span class="sxs-lookup"><span data-stu-id="c409f-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="c409f-155">Сбалансированное соотношение ресурсов ЦП и памяти.</span><span class="sxs-lookup"><span data-stu-id="c409f-155">Balanced CPU-to-memory.</span></span> <span data-ttu-id="c409f-156">Идеально подходят для разработки и тестирования малых и средних приложений и решений для обработки данных.</span><span class="sxs-lookup"><span data-stu-id="c409f-156">Ideal for dev / test and small to medium applications and data solutions.</span></span>  |
| [<span data-ttu-id="c409f-157">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="c409f-157">Compute optimized</span></span>](sizes-compute.md)   | <span data-ttu-id="c409f-158">Fs, F</span><span class="sxs-lookup"><span data-stu-id="c409f-158">Fs, F</span></span>             | <span data-ttu-id="c409f-159">Высокое соотношение ресурсов ЦП и памяти.</span><span class="sxs-lookup"><span data-stu-id="c409f-159">High CPU-to-memory.</span></span> <span data-ttu-id="c409f-160">Подходят для приложений со средним объемом трафика, сетевых устройств и пакетных процессов.</span><span class="sxs-lookup"><span data-stu-id="c409f-160">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| [<span data-ttu-id="c409f-161">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="c409f-161">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)    | <span data-ttu-id="c409f-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="c409f-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="c409f-163">Высокое соотношение ресурсов памяти и числа ядер.</span><span class="sxs-lookup"><span data-stu-id="c409f-163">High memory-to-core.</span></span> <span data-ttu-id="c409f-164">Отлично подходят для реляционных баз данных, кэша среднего и большого объема, а также выполняющейся в памяти аналитики.</span><span class="sxs-lookup"><span data-stu-id="c409f-164">Great for relational databases, medium to large caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="c409f-165">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="c409f-165">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)      | <span data-ttu-id="c409f-166">Ls</span><span class="sxs-lookup"><span data-stu-id="c409f-166">Ls</span></span>                | <span data-ttu-id="c409f-167">Высокая пропускная способность дисков и количество операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="c409f-167">High disk throughput and IO.</span></span> <span data-ttu-id="c409f-168">Идеальный вариант для работы с большими данными, а также с базами данных SQL и NoSQL.</span><span class="sxs-lookup"><span data-stu-id="c409f-168">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="c409f-169">GPU</span><span class="sxs-lookup"><span data-stu-id="c409f-169">GPU</span></span>](sizes-gpu.md)          | <span data-ttu-id="c409f-170">NV, NC</span><span class="sxs-lookup"><span data-stu-id="c409f-170">NV, NC</span></span>            | <span data-ttu-id="c409f-171">Специализированные виртуальные машины, предназначенные для ресурсоемкой отрисовки изображений и редактирования видео.</span><span class="sxs-lookup"><span data-stu-id="c409f-171">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| [<span data-ttu-id="c409f-172">Высокопроизводительные</span><span class="sxs-lookup"><span data-stu-id="c409f-172">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="c409f-173">H, A8–A11</span><span class="sxs-lookup"><span data-stu-id="c409f-173">H, A8-11</span></span>          | <span data-ttu-id="c409f-174">Виртуальные машины с самыми мощными ЦП, для которых можно настроить сетевые интерфейсы с высокой пропускной способностью (RDMA).</span><span class="sxs-lookup"><span data-stu-id="c409f-174">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="c409f-175">Поиск всех доступных размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="c409f-175">Find available VM sizes</span></span>

<span data-ttu-id="c409f-176">Чтобы просмотреть список доступных размеров виртуальных машин в определенном регионе, используйте команду [az vm list-sizes](/cli/azure/vm#list-sizes).</span><span class="sxs-lookup"><span data-stu-id="c409f-176">To see a list of VM sizes available in a particular region, use the [az vm list-sizes](/cli/azure/vm#list-sizes) command.</span></span> 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

<span data-ttu-id="c409f-177">Частичные выходные данные приведены ниже.</span><span class="sxs-lookup"><span data-stu-id="c409f-177">Partial output:</span></span>

```azurecli-interactive 
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          3584  Standard_DS1                          1           1047552                    7168
                 4          7168  Standard_DS2                          2           1047552                   14336
                 8         14336  Standard_DS3                          4           1047552                   28672
                16         28672  Standard_DS4                          8           1047552                   57344
                 4         14336  Standard_DS11                         2           1047552                   28672
                 8         28672  Standard_DS12                         4           1047552                   57344
                16         57344  Standard_DS13                         8           1047552                  114688
                32        114688  Standard_DS14                        16           1047552                  229376
                 1           768  Standard_A0                           1           1047552                   20480
                 2          1792  Standard_A1                           1           1047552                   71680
                 4          3584  Standard_A2                           2           1047552                  138240
                 8          7168  Standard_A3                           4           1047552                  291840
                 4         14336  Standard_A5                           2           1047552                  138240
                16         14336  Standard_A4                           8           1047552                  619520
                 8         28672  Standard_A6                           4           1047552                  291840
                16         57344  Standard_A7                           8           1047552                  619520
```

### <a name="create-vm-with-specific-size"></a><span data-ttu-id="c409f-178">Создание виртуальной машины с определенным размером</span><span class="sxs-lookup"><span data-stu-id="c409f-178">Create VM with specific size</span></span>

<span data-ttu-id="c409f-179">В предыдущем примере создания виртуальной машины размер не был указан, что привело к использованию размера по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c409f-179">In the previous VM creation example, a size was not provided, which results in a default size.</span></span> <span data-ttu-id="c409f-180">Размер виртуальной машины можно выбрать во время ее создания с помощью команды [az vm create](/cli/azure/vm#create) и аргумента `--size`.</span><span class="sxs-lookup"><span data-stu-id="c409f-180">A VM size can be selected at creation time using [az vm create](/cli/azure/vm#create) and the `--size` argument.</span></span> 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a><span data-ttu-id="c409f-181">Изменение размера виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c409f-181">Resize a VM</span></span>

<span data-ttu-id="c409f-182">После развертывания виртуальной машины ее размер можно изменить, чтобы увеличить или уменьшить выделенные ей ресурсы.</span><span class="sxs-lookup"><span data-stu-id="c409f-182">After a VM has been deployed, it can be resized to increase or decrease resource allocation.</span></span>

<span data-ttu-id="c409f-183">Перед изменением размера виртуальной машины проверьте, доступен ли желаемый размер в текущем кластере Azure.</span><span class="sxs-lookup"><span data-stu-id="c409f-183">Before resizing a VM, check if the desired size is available on the current Azure cluster.</span></span> <span data-ttu-id="c409f-184">Команда [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options) отображает список всех размеров.</span><span class="sxs-lookup"><span data-stu-id="c409f-184">The [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options) command returns the list of sizes.</span></span> 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
<span data-ttu-id="c409f-185">Если желаемый размер доступен, то размер виртуальной машины можно изменить во включенном состоянии, однако виртуальную машину нужно будет перезагрузить.</span><span class="sxs-lookup"><span data-stu-id="c409f-185">If the desired size is available, the VM can be resized from a powered-on state, however it is rebooted during the operation.</span></span> <span data-ttu-id="c409f-186">Используйте команду [az vm resize]( /cli/azure/vm#resize) для изменения размера.</span><span class="sxs-lookup"><span data-stu-id="c409f-186">Use the [az vm resize]( /cli/azure/vm#resize) command to perform the resize.</span></span>

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

<span data-ttu-id="c409f-187">Если желаемый размер в текущем кластере недоступен, то перед изменением размера виртуальную машину нужно освободить.</span><span class="sxs-lookup"><span data-stu-id="c409f-187">If the desired size is not on the current cluster, the VM needs to be deallocated before the resize operation can occur.</span></span> <span data-ttu-id="c409f-188">Используйте команду [az vm deallocate]( /cli/azure/vm#deallocate), чтобы остановить и освободить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="c409f-188">Use the [az vm deallocate]( /cli/azure/vm#deallocate) command to stop and deallocate the VM.</span></span> <span data-ttu-id="c409f-189">Обратите внимание на то, что после повторного включения виртуальной машины все данные на временном диске могут быть удалены.</span><span class="sxs-lookup"><span data-stu-id="c409f-189">Note, when the VM is powered back on, any data on the temp disk may be removed.</span></span> <span data-ttu-id="c409f-190">Кроме того, изменится общедоступный IP-адрес, если только не используется статический IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c409f-190">The public IP address also changes unless a static IP address is being used.</span></span> 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

<span data-ttu-id="c409f-191">После освобождения виртуальной машины ее размер можно изменить.</span><span class="sxs-lookup"><span data-stu-id="c409f-191">Once deallocated, the resize can occur.</span></span> 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

<span data-ttu-id="c409f-192">После изменения размера можно запустить будет виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="c409f-192">After the resize, the VM can be started.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a><span data-ttu-id="c409f-193">Состояния включенной виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c409f-193">VM power states</span></span>

<span data-ttu-id="c409f-194">Включенная виртуальная машина Azure может находиться в одном из многих состояний.</span><span class="sxs-lookup"><span data-stu-id="c409f-194">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="c409f-195">Это состояние отражает текущее состояние виртуальной машины с точки зрения гипервизора.</span><span class="sxs-lookup"><span data-stu-id="c409f-195">This state represents the current state of the VM from the standpoint of the hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="c409f-196">Состояния включения</span><span class="sxs-lookup"><span data-stu-id="c409f-196">Power states</span></span>

| <span data-ttu-id="c409f-197">Состояние включения</span><span class="sxs-lookup"><span data-stu-id="c409f-197">Power State</span></span> | <span data-ttu-id="c409f-198">Описание</span><span class="sxs-lookup"><span data-stu-id="c409f-198">Description</span></span>
|----|----|
| <span data-ttu-id="c409f-199">Starting</span><span class="sxs-lookup"><span data-stu-id="c409f-199">Starting</span></span> | <span data-ttu-id="c409f-200">Указывает, что виртуальная машина запущена.</span><span class="sxs-lookup"><span data-stu-id="c409f-200">Indicates the virtual machine is being started.</span></span> |
| <span data-ttu-id="c409f-201">Выполнение</span><span class="sxs-lookup"><span data-stu-id="c409f-201">Running</span></span> | <span data-ttu-id="c409f-202">Указывает, что виртуальная машина работает.</span><span class="sxs-lookup"><span data-stu-id="c409f-202">Indicates that the virtual machine is running.</span></span> |
| <span data-ttu-id="c409f-203">Остановка</span><span class="sxs-lookup"><span data-stu-id="c409f-203">Stopping</span></span> | <span data-ttu-id="c409f-204">Указывает, что виртуальная машина останавливается.</span><span class="sxs-lookup"><span data-stu-id="c409f-204">Indicates that the virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="c409f-205">Остановлено</span><span class="sxs-lookup"><span data-stu-id="c409f-205">Stopped</span></span> | <span data-ttu-id="c409f-206">Указывает, что виртуальная машина остановлена.</span><span class="sxs-lookup"><span data-stu-id="c409f-206">Indicates that the virtual machine is stopped.</span></span> <span data-ttu-id="c409f-207">За виртуальные машины в остановленном состоянии по-прежнему взимается плата за вычислительные операции.</span><span class="sxs-lookup"><span data-stu-id="c409f-207">Virtual machines in the stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="c409f-208">Отмена выделения</span><span class="sxs-lookup"><span data-stu-id="c409f-208">Deallocating</span></span> | <span data-ttu-id="c409f-209">Указывает, что виртуальная машина освобождается.</span><span class="sxs-lookup"><span data-stu-id="c409f-209">Indicates that the virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="c409f-210">Освобождено</span><span class="sxs-lookup"><span data-stu-id="c409f-210">Deallocated</span></span> | <span data-ttu-id="c409f-211">Указывает, что виртуальная машина удалена из гипервизора, но по-прежнему доступна в плоскости управления.</span><span class="sxs-lookup"><span data-stu-id="c409f-211">Indicates that the virtual machine is removed from the hypervisor but still available in the control plane.</span></span> <span data-ttu-id="c409f-212">За виртуальные машины в освобожденном состоянии не взимается плата за вычислительные операции.</span><span class="sxs-lookup"><span data-stu-id="c409f-212">Virtual machines in the Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="c409f-213">Указывает, что состояние включенной виртуальной машины неизвестно.</span><span class="sxs-lookup"><span data-stu-id="c409f-213">Indicates that the power state of the virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="c409f-214">Поиск состояние включения</span><span class="sxs-lookup"><span data-stu-id="c409f-214">Find power state</span></span>

<span data-ttu-id="c409f-215">Чтобы получить состояние конкретной виртуальной машины, используйте команду [az vm get instance-view](/cli/azure/vm#get-instance-view).</span><span class="sxs-lookup"><span data-stu-id="c409f-215">To retrieve the state of a particular VM, use the [az vm get instance-view](/cli/azure/vm#get-instance-view) command.</span></span> <span data-ttu-id="c409f-216">Необходимо указать допустимое имя виртуальной машины и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c409f-216">Be sure to specify a valid name for a virtual machine and resource group.</span></span> 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

<span data-ttu-id="c409f-217">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="c409f-217">Output:</span></span>

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a><span data-ttu-id="c409f-218">Задачи управления</span><span class="sxs-lookup"><span data-stu-id="c409f-218">Management tasks</span></span>

<span data-ttu-id="c409f-219">В течение жизненного цикла виртуальной машины можно выполнять задачи управления, такие как запуск, остановка или удаление виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c409f-219">During the life-cycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="c409f-220">Кроме того, можно создавать скрипты для автоматизации повторяющихся или сложных задач.</span><span class="sxs-lookup"><span data-stu-id="c409f-220">Additionally, you may want to create scripts to automate repetitive or complex tasks.</span></span> <span data-ttu-id="c409f-221">С помощью Azure CLI в командной строке или в скриптах можно выполнять множество распространенных задач управления.</span><span class="sxs-lookup"><span data-stu-id="c409f-221">Using the Azure CLI, many common management tasks can be run from the command line or in scripts.</span></span> 

### <a name="get-ip-address"></a><span data-ttu-id="c409f-222">Получение IP-адреса</span><span class="sxs-lookup"><span data-stu-id="c409f-222">Get IP address</span></span>

<span data-ttu-id="c409f-223">Эта команда возвращает частный и общедоступный IP-адрес виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c409f-223">This command returns the private and public IP addresses of a virtual machine.</span></span>  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a><span data-ttu-id="c409f-224">Прекращение работы виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c409f-224">Stop virtual machine</span></span>

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a><span data-ttu-id="c409f-225">Запуск виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c409f-225">Start virtual machine</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="c409f-226">Удалить группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="c409f-226">Delete resource group</span></span>

<span data-ttu-id="c409f-227">При удалении группы ресурсов будут также удалены все ресурсы, содержащиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="c409f-227">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a><span data-ttu-id="c409f-228">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c409f-228">Next steps</span></span>

<span data-ttu-id="c409f-229">В рамках этого руководства вы изучили основы создания виртуальной машины и управления ею. Вы узнали, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="c409f-229">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c409f-230">Создание виртуальной машины и подключение к ней</span><span class="sxs-lookup"><span data-stu-id="c409f-230">Create and connect to a VM</span></span>
> * <span data-ttu-id="c409f-231">Выбор и использование образов виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="c409f-231">Select and use VM images</span></span>
> * <span data-ttu-id="c409f-232">Просмотр и использование определенных размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="c409f-232">View and use specific VM sizes</span></span>
> * <span data-ttu-id="c409f-233">Изменение размера виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c409f-233">Resize a VM</span></span>
> * <span data-ttu-id="c409f-234">Просмотр виртуальной машины и оценка ее состояния</span><span class="sxs-lookup"><span data-stu-id="c409f-234">View and understand VM state</span></span>

<span data-ttu-id="c409f-235">Перейдите к следующему руководству, чтобы узнать о дисках виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="c409f-235">Advance to the next tutorial to learn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="c409f-236">Управление дисками Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c409f-236">Create and Manage VM disks</span></span>](./tutorial-manage-disks.md)
