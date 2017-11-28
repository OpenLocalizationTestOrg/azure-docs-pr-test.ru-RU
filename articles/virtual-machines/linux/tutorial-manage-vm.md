---
title: "aaaCreate и управление виртуальными машинами Linux с hello Azure CLI | Документы Microsoft"
description: "Учебник — Создание и управление виртуальными машинами Linux с hello Azure CLI"
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
ms.openlocfilehash: 05f7c1cf860f809bc13f110778d3bddd619ac6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-linux-vms-with-hello-azure-cli"></a><span data-ttu-id="e7658-103">Создание и управление виртуальными машинами Linux с hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e7658-103">Create and Manage Linux VMs with hello Azure CLI</span></span>

<span data-ttu-id="e7658-104">Виртуальные машины Azure предоставляют полностью настраиваемую и гибкую вычислительную среду.</span><span class="sxs-lookup"><span data-stu-id="e7658-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="e7658-105">В этом руководстве рассматриваются основные элементы развертывания виртуальной машины Azure, например выбор ее размера, образа и ее развертывание.</span><span class="sxs-lookup"><span data-stu-id="e7658-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="e7658-106">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="e7658-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e7658-107">Создать и присоединить tooa виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="e7658-107">Create and connect tooa VM</span></span>
> * <span data-ttu-id="e7658-108">Выбор и использование образов виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="e7658-108">Select and use VM images</span></span>
> * <span data-ttu-id="e7658-109">Просмотр и использование определенных размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="e7658-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="e7658-110">Изменение размера виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e7658-110">Resize a VM</span></span>
> * <span data-ttu-id="e7658-111">Просмотр виртуальной машины и оценка ее состояния</span><span class="sxs-lookup"><span data-stu-id="e7658-111">View and understand VM state</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e7658-112">Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e7658-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="e7658-113">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="e7658-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e7658-114">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e7658-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-resource-group"></a><span data-ttu-id="e7658-115">Создать группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="e7658-115">Create resource group</span></span>

<span data-ttu-id="e7658-116">Создание группы ресурсов с hello [Создание группы az](https://docs.microsoft.com/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="e7658-116">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="e7658-117">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="e7658-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="e7658-118">Группу ресурсов следует создавать до виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e7658-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="e7658-119">В этом примере имя группы ресурсов *myResourceGroupVM* создается в hello *eastus* области.</span><span class="sxs-lookup"><span data-stu-id="e7658-119">In this example, a resource group named *myResourceGroupVM* is created in hello *eastus* region.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

<span data-ttu-id="e7658-120">Группа ресурсов Hello указывается при создании или изменении виртуальных Машин, который можно увидеть на протяжении этого учебника.</span><span class="sxs-lookup"><span data-stu-id="e7658-120">hello resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="e7658-121">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e7658-121">Create virtual machine</span></span>

<span data-ttu-id="e7658-122">Создание виртуальной машины с hello [создания виртуальной машины az](https://docs.microsoft.com/cli/azure/vm#create) команды.</span><span class="sxs-lookup"><span data-stu-id="e7658-122">Create a virtual machine with hello [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="e7658-123">При создании виртуальной машины доступно несколько вариантов, таких как образ операционной системы, определение размера диска и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="e7658-123">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="e7658-124">В этом примере создается виртуальная машина *myVM* под управлением Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="e7658-124">In this example, a virtual machine is created with a name of *myVM* running Ubuntu Server.</span></span> 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="e7658-125">Один раз hello создания виртуальной Машины, hello Azure CLI выводит сведения о hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="e7658-125">Once hello VM has been created, hello Azure CLI outputs information about hello VM.</span></span> <span data-ttu-id="e7658-126">Запишите hello `publicIpAddress`, этот адрес может быть используется tooaccess hello виртуальной машины...</span><span class="sxs-lookup"><span data-stu-id="e7658-126">Take note of hello `publicIpAddress`, this address can be used tooaccess hello virtual machine..</span></span> 

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

## <a name="connect-toovm"></a><span data-ttu-id="e7658-127">Подключение tooVM</span><span class="sxs-lookup"><span data-stu-id="e7658-127">Connect tooVM</span></span>

<span data-ttu-id="e7658-128">Теперь можно подключиться toohello виртуальной Машины с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="e7658-128">You can now connect toohello VM using SSH.</span></span> <span data-ttu-id="e7658-129">Замените IP-адрес hello пример hello `publicIpAddress` отмечалось в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="e7658-129">Replace hello example IP address with hello `publicIpAddress` noted in hello previous step.</span></span>

```bash
ssh 52.174.34.95
```

<span data-ttu-id="e7658-130">После завершения работы с hello виртуальной Машины, закройте сеанс SSH hello.</span><span class="sxs-lookup"><span data-stu-id="e7658-130">Once finished with hello VM, close hello SSH session.</span></span> 

```bash
exit
```

## <a name="understand-vm-images"></a><span data-ttu-id="e7658-131">Описание образов виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="e7658-131">Understand VM images</span></span>

<span data-ttu-id="e7658-132">Hello Azure marketplace включает большое количество изображений, которые могут быть toocreate используемых виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e7658-132">hello Azure marketplace includes many images that can be used toocreate VMs.</span></span> <span data-ttu-id="e7658-133">В предыдущих шагах hello на виртуальной машине был создан с помощью Ubuntu изображения.</span><span class="sxs-lookup"><span data-stu-id="e7658-133">In hello previous steps, a virtual machine was created using an Ubuntu image.</span></span> <span data-ttu-id="e7658-134">На этом шаге hello Azure CLI — marketplace hello toosearch используется для создания образа CentOS, которое затем используется toodeploy второй виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e7658-134">In this step, hello Azure CLI is used toosearch hello marketplace for a CentOS image, which is then used toodeploy a second virtual machine.</span></span>  

<span data-ttu-id="e7658-135">toosee список hello чаще всего используются изображения, используйте hello [списка изображений ВМ az](/cli/azure/vm/image#list) команды.</span><span class="sxs-lookup"><span data-stu-id="e7658-135">toosee a list of hello most commonly used images, use hello [az vm image list](/cli/azure/vm/image#list) command.</span></span>

```azurecli-interactive 
az vm image list --output table
```

<span data-ttu-id="e7658-136">выходные данные команды Hello возвращает hello наиболее популярных образов виртуальных Машин в Azure.</span><span class="sxs-lookup"><span data-stu-id="e7658-136">hello command output returns hello most popular VM images on Azure.</span></span>

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

<span data-ttu-id="e7658-137">Полный список можно увидеть, добавив hello `--all` аргумент.</span><span class="sxs-lookup"><span data-stu-id="e7658-137">A full list can be seen by adding hello `--all` argument.</span></span> <span data-ttu-id="e7658-138">список изображений Hello, также можно фильтровать по `--publisher` или `–-offer`.</span><span class="sxs-lookup"><span data-stu-id="e7658-138">hello image list can also be filtered by `--publisher` or `–-offer`.</span></span> <span data-ttu-id="e7658-139">В этом примере hello список отфильтрован и все образы, соответствующий предложением *CentOS*.</span><span class="sxs-lookup"><span data-stu-id="e7658-139">In this example, hello list is filtered for all images with an offer that matches *CentOS*.</span></span> 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

<span data-ttu-id="e7658-140">Частичные выходные данные приведены ниже.</span><span class="sxs-lookup"><span data-stu-id="e7658-140">Partial output:</span></span>

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

<span data-ttu-id="e7658-141">toodeploy ВМ с помощью специального образа, запишите значение hello hello *Urn* столбца.</span><span class="sxs-lookup"><span data-stu-id="e7658-141">toodeploy a VM using a specific image, take note of hello value in hello *Urn* column.</span></span> <span data-ttu-id="e7658-142">При указании изображения hello, номер версии образа hello можно заменить «последние», который выбирает последнюю версию hello hello распространения.</span><span class="sxs-lookup"><span data-stu-id="e7658-142">When specifying hello image, hello image version number can be replaced with “latest”, which selects hello latest version of hello distribution.</span></span> <span data-ttu-id="e7658-143">В этом примере hello `--image` аргумент является последней версии используется toospecify hello образа CentOS версии 6.5.</span><span class="sxs-lookup"><span data-stu-id="e7658-143">In this example, hello `--image` argument is used toospecify hello latest version of a CentOS 6.5 image.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="e7658-144">Описание размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="e7658-144">Understand VM sizes</span></span>

<span data-ttu-id="e7658-145">Размер виртуальной машины определяет hello объем вычислительных ресурсов, таких как ЦП, графического Процессора и памяти, сделанные доступными toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e7658-145">A virtual machine size determines hello amount of compute resources such as CPU, GPU, and memory that are made available toohello virtual machine.</span></span> <span data-ttu-id="e7658-146">Виртуальные машины должны toobe масштабы hello ожидается рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e7658-146">Virtual machines need toobe sized appropriately for hello expected work load.</span></span> <span data-ttu-id="e7658-147">При увеличении рабочей нагрузки размер существующей виртуальной машины может быть изменен.</span><span class="sxs-lookup"><span data-stu-id="e7658-147">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="e7658-148">Размеры виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="e7658-148">VM Sizes</span></span>

<span data-ttu-id="e7658-149">в следующей таблице Hello относит размеры вариантов использования.</span><span class="sxs-lookup"><span data-stu-id="e7658-149">hello following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="e7658-150">Тип</span><span class="sxs-lookup"><span data-stu-id="e7658-150">Type</span></span>                     | <span data-ttu-id="e7658-151">Размеры</span><span class="sxs-lookup"><span data-stu-id="e7658-151">Sizes</span></span>           |    <span data-ttu-id="e7658-152">Описание</span><span class="sxs-lookup"><span data-stu-id="e7658-152">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="e7658-153">Универсальные</span><span class="sxs-lookup"><span data-stu-id="e7658-153">General purpose</span></span>](sizes-general.md)         |<span data-ttu-id="e7658-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0–7</span><span class="sxs-lookup"><span data-stu-id="e7658-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="e7658-155">Сбалансированное соотношение ресурсов ЦП и памяти.</span><span class="sxs-lookup"><span data-stu-id="e7658-155">Balanced CPU-to-memory.</span></span> <span data-ttu-id="e7658-156">Идеально подходит для разработки и тестирования и малого toomedium приложениям и данным решения.</span><span class="sxs-lookup"><span data-stu-id="e7658-156">Ideal for dev / test and small toomedium applications and data solutions.</span></span>  |
| [<span data-ttu-id="e7658-157">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="e7658-157">Compute optimized</span></span>](sizes-compute.md)   | <span data-ttu-id="e7658-158">Fs, F</span><span class="sxs-lookup"><span data-stu-id="e7658-158">Fs, F</span></span>             | <span data-ttu-id="e7658-159">Высокое соотношение ресурсов ЦП и памяти.</span><span class="sxs-lookup"><span data-stu-id="e7658-159">High CPU-to-memory.</span></span> <span data-ttu-id="e7658-160">Подходят для приложений со средним объемом трафика, сетевых устройств и пакетных процессов.</span><span class="sxs-lookup"><span data-stu-id="e7658-160">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| [<span data-ttu-id="e7658-161">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="e7658-161">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)    | <span data-ttu-id="e7658-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="e7658-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="e7658-163">Высокое соотношение ресурсов памяти и числа ядер.</span><span class="sxs-lookup"><span data-stu-id="e7658-163">High memory-to-core.</span></span> <span data-ttu-id="e7658-164">Идеально подходит для реляционных баз данных, кэши средний toolarge и аналитики в памяти.</span><span class="sxs-lookup"><span data-stu-id="e7658-164">Great for relational databases, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="e7658-165">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="e7658-165">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)      | <span data-ttu-id="e7658-166">Ls</span><span class="sxs-lookup"><span data-stu-id="e7658-166">Ls</span></span>                | <span data-ttu-id="e7658-167">Высокая пропускная способность дисков и количество операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="e7658-167">High disk throughput and IO.</span></span> <span data-ttu-id="e7658-168">Идеальный вариант для работы с большими данными, а также с базами данных SQL и NoSQL.</span><span class="sxs-lookup"><span data-stu-id="e7658-168">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="e7658-169">GPU</span><span class="sxs-lookup"><span data-stu-id="e7658-169">GPU</span></span>](sizes-gpu.md)          | <span data-ttu-id="e7658-170">NV, NC</span><span class="sxs-lookup"><span data-stu-id="e7658-170">NV, NC</span></span>            | <span data-ttu-id="e7658-171">Специализированные виртуальные машины, предназначенные для ресурсоемкой отрисовки изображений и редактирования видео.</span><span class="sxs-lookup"><span data-stu-id="e7658-171">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| [<span data-ttu-id="e7658-172">Высокопроизводительные</span><span class="sxs-lookup"><span data-stu-id="e7658-172">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="e7658-173">H, A8–A11</span><span class="sxs-lookup"><span data-stu-id="e7658-173">H, A8-11</span></span>          | <span data-ttu-id="e7658-174">Виртуальные машины с самыми мощными ЦП, для которых можно настроить сетевые интерфейсы с высокой пропускной способностью (RDMA).</span><span class="sxs-lookup"><span data-stu-id="e7658-174">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="e7658-175">Поиск всех доступных размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="e7658-175">Find available VM sizes</span></span>

<span data-ttu-id="e7658-176">toosee список виртуальных Машин размеров, доступных в определенном регионе, используйте hello [списка размеров виртуальных машин az](/cli/azure/vm#list-sizes) команды.</span><span class="sxs-lookup"><span data-stu-id="e7658-176">toosee a list of VM sizes available in a particular region, use hello [az vm list-sizes](/cli/azure/vm#list-sizes) command.</span></span> 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

<span data-ttu-id="e7658-177">Частичные выходные данные приведены ниже.</span><span class="sxs-lookup"><span data-stu-id="e7658-177">Partial output:</span></span>

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

### <a name="create-vm-with-specific-size"></a><span data-ttu-id="e7658-178">Создание виртуальной машины с определенным размером</span><span class="sxs-lookup"><span data-stu-id="e7658-178">Create VM with specific size</span></span>

<span data-ttu-id="e7658-179">Hello предыдущего примера создания виртуальной Машины размер не указано, какие результаты размером по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e7658-179">In hello previous VM creation example, a size was not provided, which results in a default size.</span></span> <span data-ttu-id="e7658-180">Размер виртуальной Машины можно выбрать во время создания с помощью [создания виртуальной машины az](/cli/azure/vm#create) и hello `--size` аргумент.</span><span class="sxs-lookup"><span data-stu-id="e7658-180">A VM size can be selected at creation time using [az vm create](/cli/azure/vm#create) and hello `--size` argument.</span></span> 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a><span data-ttu-id="e7658-181">Изменение размера виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e7658-181">Resize a VM</span></span>

<span data-ttu-id="e7658-182">После развертывания виртуальной Машины, ее можно изменять размер tooincrease или уменьшить выделения ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e7658-182">After a VM has been deployed, it can be resized tooincrease or decrease resource allocation.</span></span>

<span data-ttu-id="e7658-183">Перед изменением размера виртуальной Машины, проверьте, если hello желаемый размер текущего кластера Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e7658-183">Before resizing a VM, check if hello desired size is available on hello current Azure cluster.</span></span> <span data-ttu-id="e7658-184">Hello [az виртуальной машины-vm-resize параметры списка](/cli/azure/vm#list-vm-resize-options) команда возвращает hello список размеров.</span><span class="sxs-lookup"><span data-stu-id="e7658-184">hello [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options) command returns hello list of sizes.</span></span> 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
<span data-ttu-id="e7658-185">При желании hello, что он доступен hello виртуальной Машины могут быть изменены из состояния включении, однако он не будет перезагружен во время операции hello.</span><span class="sxs-lookup"><span data-stu-id="e7658-185">If hello desired size is available, hello VM can be resized from a powered-on state, however it is rebooted during hello operation.</span></span> <span data-ttu-id="e7658-186">Используйте hello [изменить размер виртуальной машины az]( /cli/azure/vm#resize) команда tooperform hello, изменения размера.</span><span class="sxs-lookup"><span data-stu-id="e7658-186">Use hello [az vm resize]( /cli/azure/vm#resize) command tooperform hello resize.</span></span>

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

<span data-ttu-id="e7658-187">Если hello желаемый размер находится не на hello текущего кластера, hello ВМ потребностей, может произойти toobe освобождена до hello операцию изменения размера.</span><span class="sxs-lookup"><span data-stu-id="e7658-187">If hello desired size is not on hello current cluster, hello VM needs toobe deallocated before hello resize operation can occur.</span></span> <span data-ttu-id="e7658-188">Используйте hello [ВМ az deallocate]( /cli/azure/vm#deallocate) команды toostop и освобождать hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="e7658-188">Use hello [az vm deallocate]( /cli/azure/vm#deallocate) command toostop and deallocate hello VM.</span></span> <span data-ttu-id="e7658-189">Обратите внимание, что при hello виртуальная машина не будет включено обратно, могут быть удалены все данные на диске временный hello.</span><span class="sxs-lookup"><span data-stu-id="e7658-189">Note, when hello VM is powered back on, any data on hello temp disk may be removed.</span></span> <span data-ttu-id="e7658-190">Hello общедоступный IP-адрес также изменяется, если только не используется статический IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="e7658-190">hello public IP address also changes unless a static IP address is being used.</span></span> 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

<span data-ttu-id="e7658-191">После освобождена, может произойти изменения размера hello.</span><span class="sxs-lookup"><span data-stu-id="e7658-191">Once deallocated, hello resize can occur.</span></span> 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

<span data-ttu-id="e7658-192">После изменения размера hello, можно запустить hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="e7658-192">After hello resize, hello VM can be started.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a><span data-ttu-id="e7658-193">Состояния включенной виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e7658-193">VM power states</span></span>

<span data-ttu-id="e7658-194">Включенная виртуальная машина Azure может находиться в одном из многих состояний.</span><span class="sxs-lookup"><span data-stu-id="e7658-194">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="e7658-195">Это состояние представляет текущее состояние hello hello виртуальной Машины с точки зрения hello hello низкоуровневой оболочки.</span><span class="sxs-lookup"><span data-stu-id="e7658-195">This state represents hello current state of hello VM from hello standpoint of hello hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="e7658-196">Состояния включения</span><span class="sxs-lookup"><span data-stu-id="e7658-196">Power states</span></span>

| <span data-ttu-id="e7658-197">Состояние включения</span><span class="sxs-lookup"><span data-stu-id="e7658-197">Power State</span></span> | <span data-ttu-id="e7658-198">Описание</span><span class="sxs-lookup"><span data-stu-id="e7658-198">Description</span></span>
|----|----|
| <span data-ttu-id="e7658-199">Starting</span><span class="sxs-lookup"><span data-stu-id="e7658-199">Starting</span></span> | <span data-ttu-id="e7658-200">Указывает, что hello виртуальная машина запускается.</span><span class="sxs-lookup"><span data-stu-id="e7658-200">Indicates hello virtual machine is being started.</span></span> |
| <span data-ttu-id="e7658-201">Выполнение</span><span class="sxs-lookup"><span data-stu-id="e7658-201">Running</span></span> | <span data-ttu-id="e7658-202">Указывает, что выполняется hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e7658-202">Indicates that hello virtual machine is running.</span></span> |
| <span data-ttu-id="e7658-203">Остановка</span><span class="sxs-lookup"><span data-stu-id="e7658-203">Stopping</span></span> | <span data-ttu-id="e7658-204">Указывает, что выполняется остановка виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="e7658-204">Indicates that hello virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="e7658-205">Остановлено</span><span class="sxs-lookup"><span data-stu-id="e7658-205">Stopped</span></span> | <span data-ttu-id="e7658-206">Указывает, что этот hello виртуальная машина остановлена.</span><span class="sxs-lookup"><span data-stu-id="e7658-206">Indicates that hello virtual machine is stopped.</span></span> <span data-ttu-id="e7658-207">Виртуальные машины в состоянии остановки hello взиматься плата за вычислительные операции.</span><span class="sxs-lookup"><span data-stu-id="e7658-207">Virtual machines in hello stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="e7658-208">Отмена выделения</span><span class="sxs-lookup"><span data-stu-id="e7658-208">Deallocating</span></span> | <span data-ttu-id="e7658-209">Указывает, что выполняется освобождение hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e7658-209">Indicates that hello virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="e7658-210">Освобождено</span><span class="sxs-lookup"><span data-stu-id="e7658-210">Deallocated</span></span> | <span data-ttu-id="e7658-211">Указывает, что для этой виртуальной машине hello удален из hello низкоуровневой оболочки, но по-прежнему доступны в плоскости управления hello.</span><span class="sxs-lookup"><span data-stu-id="e7658-211">Indicates that hello virtual machine is removed from hello hypervisor but still available in hello control plane.</span></span> <span data-ttu-id="e7658-212">Виртуальные машины в состоянии освобождена hello не взимается вычислений.</span><span class="sxs-lookup"><span data-stu-id="e7658-212">Virtual machines in hello Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="e7658-213">Указывает на неизвестное состояние электропитания hello hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e7658-213">Indicates that hello power state of hello virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="e7658-214">Поиск состояние включения</span><span class="sxs-lookup"><span data-stu-id="e7658-214">Find power state</span></span>

<span data-ttu-id="e7658-215">состояние конкретной виртуальной Машины, используйте hello hello tooretrieve [ВМ az получить представление экземпляров](/cli/azure/vm#get-instance-view) команды.</span><span class="sxs-lookup"><span data-stu-id="e7658-215">tooretrieve hello state of a particular VM, use hello [az vm get instance-view](/cli/azure/vm#get-instance-view) command.</span></span> <span data-ttu-id="e7658-216">Быть toospecify убедиться, что допустимое имя для виртуальной машины и группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e7658-216">Be sure toospecify a valid name for a virtual machine and resource group.</span></span> 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

<span data-ttu-id="e7658-217">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e7658-217">Output:</span></span>

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a><span data-ttu-id="e7658-218">Задачи управления</span><span class="sxs-lookup"><span data-stu-id="e7658-218">Management tasks</span></span>

<span data-ttu-id="e7658-219">Во время hello жизненного цикла виртуальной машины может понадобиться toorun задачи управления, такие как запуск, остановка или удаление виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e7658-219">During hello life-cycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="e7658-220">Кроме того вы можете toocreate сценариев tooautomate повторяющихся или сложных задач.</span><span class="sxs-lookup"><span data-stu-id="e7658-220">Additionally, you may want toocreate scripts tooautomate repetitive or complex tasks.</span></span> <span data-ttu-id="e7658-221">С помощью hello Azure CLI, стандартных задач управления можно запускать из командной строки hello или в скриптах.</span><span class="sxs-lookup"><span data-stu-id="e7658-221">Using hello Azure CLI, many common management tasks can be run from hello command line or in scripts.</span></span> 

### <a name="get-ip-address"></a><span data-ttu-id="e7658-222">Получение IP-адреса</span><span class="sxs-lookup"><span data-stu-id="e7658-222">Get IP address</span></span>

<span data-ttu-id="e7658-223">Эта команда возвращает hello частных и общедоступных IP-адреса виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e7658-223">This command returns hello private and public IP addresses of a virtual machine.</span></span>  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a><span data-ttu-id="e7658-224">Прекращение работы виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e7658-224">Stop virtual machine</span></span>

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a><span data-ttu-id="e7658-225">Запуск виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e7658-225">Start virtual machine</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="e7658-226">Удалить группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="e7658-226">Delete resource group</span></span>

<span data-ttu-id="e7658-227">При удалении группы ресурсов будут также удалены все ресурсы, содержащиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="e7658-227">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a><span data-ttu-id="e7658-228">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e7658-228">Next steps</span></span>

<span data-ttu-id="e7658-229">В рамках этого руководства вы изучили основы создания виртуальной машины и управления ею. Вы узнали, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="e7658-229">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e7658-230">Создать и присоединить tooa виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="e7658-230">Create and connect tooa VM</span></span>
> * <span data-ttu-id="e7658-231">Выбор и использование образов виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="e7658-231">Select and use VM images</span></span>
> * <span data-ttu-id="e7658-232">Просмотр и использование определенных размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="e7658-232">View and use specific VM sizes</span></span>
> * <span data-ttu-id="e7658-233">Изменение размера виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e7658-233">Resize a VM</span></span>
> * <span data-ttu-id="e7658-234">Просмотр виртуальной машины и оценка ее состояния</span><span class="sxs-lookup"><span data-stu-id="e7658-234">View and understand VM state</span></span>

<span data-ttu-id="e7658-235">Переместить следующий учебник toolearn toohello о дисках виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="e7658-235">Advance toohello next tutorial toolearn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="e7658-236">Управление дисками Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e7658-236">Create and Manage VM disks</span></span>](./tutorial-manage-disks.md)
