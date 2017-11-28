---
title: "aaaAvailability задает учебника для виртуальных машин Linux в Azure | Документы Microsoft"
description: "Дополнительные сведения о hello группы доступности для виртуальных машин Linux в Azure."
documentationcenter: 
services: virtual-machines-linux
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 2a91e4a6057180035ec51410d9fffccaca343758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a><span data-ttu-id="a8e06-103">Каким образом задает toouse доступности</span><span class="sxs-lookup"><span data-stu-id="a8e06-103">How toouse availability sets</span></span>


<span data-ttu-id="a8e06-104">В этом учебнике вы узнаете, как tooincrease hello доступность и надежность решений для виртуальной машины в Azure, используя возможность вызывать группы доступности.</span><span class="sxs-lookup"><span data-stu-id="a8e06-104">In this tutorial, you will learn how tooincrease hello availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="a8e06-105">Группы доступности убедитесь, что hello, развертываемым в Azure виртуальные машины распределены по нескольким кластерам изолированное оборудовании.</span><span class="sxs-lookup"><span data-stu-id="a8e06-105">Availability sets ensure that hello VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="a8e06-106">Это гарантирует, что если происходит сбой оборудования или программного обеспечения в Azure, будут затронуты только подмножество виртуальных машин и что всего решения будет оставаться доступными и функциональными с точки зрения hello ваших клиентов, используя его.</span><span class="sxs-lookup"><span data-stu-id="a8e06-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from hello perspective of your customers using it.</span></span>

<span data-ttu-id="a8e06-107">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="a8e06-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a8e06-108">"Создать группу доступности"</span><span class="sxs-lookup"><span data-stu-id="a8e06-108">Create an availability set</span></span>
> * <span data-ttu-id="a8e06-109">Создание виртуальной машины в группе доступности</span><span class="sxs-lookup"><span data-stu-id="a8e06-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="a8e06-110">Проверка доступных размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="a8e06-110">Check available VM sizes</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a8e06-111">Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="a8e06-111">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a8e06-112">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="a8e06-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a8e06-113">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a8e06-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="availability-set-overview"></a><span data-ttu-id="a8e06-114">Обзор групп доступности</span><span class="sxs-lookup"><span data-stu-id="a8e06-114">Availability set overview</span></span>

<span data-ttu-id="a8e06-115">Группа доступности — возможность логическое группирование, который можно использовать в Azure tooensure, изолированы друг от друга ресурсы hello виртуальных Машин, размещаемых в ней при развертывании в центре обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e06-115">An Availability Set is a logical grouping capability that you can use in Azure tooensure that hello VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="a8e06-116">Azure гарантирует, что hello поместить в группу доступности, запустите несколько физических серверов, виртуальных машин, вычислений стойки, устройства хранения и сетевых коммутаторов.</span><span class="sxs-lookup"><span data-stu-id="a8e06-116">Azure ensures that hello VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="a8e06-117">Это гарантирует, что в событии hello оборудования или программного обеспечения Azure сбоя, будут затронуты только подмножество виртуальных машин и общую приложения будет работать и продолжить toobe tooyour доступны клиентам.</span><span class="sxs-lookup"><span data-stu-id="a8e06-117">This ensures that in hello event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue toobe available tooyour customers.</span></span> <span data-ttu-id="a8e06-118">С помощью групп доступности, tooleverage основных возможностей можно создать toobuild надежного облачных решений.</span><span class="sxs-lookup"><span data-stu-id="a8e06-118">Using Availability Sets is an essential capability tooleverage when you want toobuild reliable cloud solutions.</span></span>

<span data-ttu-id="a8e06-119">Рассмотрим стандартное решение на основе виртуальной машины, в котором может находиться 4 внешних веб-сервера и использоваться 2 внутренние виртуальные машины, содержащие базу данных.</span><span class="sxs-lookup"><span data-stu-id="a8e06-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="a8e06-120">С помощью Azure необходимо два набора доступности toodefine перед развертыванием виртуальных машин: группа доступности одного уровня «web» hello и один набор доступности для уровня «database» hello.</span><span class="sxs-lookup"><span data-stu-id="a8e06-120">With Azure, you’d want toodefine two availability sets before you deploy your VMs: one availability set for hello “web” tier and one availability set for hello “database” tier.</span></span> <span data-ttu-id="a8e06-121">При создании новой виртуальной Машины, можно указать hello доступности виртуальной машины az toohello параметр «Создать», а Azure автоматически гарантирует, что hello виртуальных машин, создаваемых внутри hello доступных набор изолированы по нескольким ресурсам физического оборудования.</span><span class="sxs-lookup"><span data-stu-id="a8e06-121">When you create a new VM you can then specify hello availability set as a parameter toohello az vm create command, and Azure will automatically ensure that hello VMs you create within hello available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="a8e06-122">Это означает, что если hello физическое оборудование, на котором один из веб-сервер или ВМ сервера базы данных выполняется на проблемы, вы знаете, hello другие экземпляры веб-сервера и базы данных виртуальных машин сможет продолжить работу нормально, так как они находятся на другое оборудование.</span><span class="sxs-lookup"><span data-stu-id="a8e06-122">This means that if hello physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that hello other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="a8e06-123">При необходимости toodeploy решений надежного Виртуальных машинах в Azure, следует всегда использовать группы доступности.</span><span class="sxs-lookup"><span data-stu-id="a8e06-123">You should always use Availability Sets when you want toodeploy reliable VM-based solutions within Azure.</span></span>


## <a name="create-an-availability-set"></a><span data-ttu-id="a8e06-124">"Создать группу доступности"</span><span class="sxs-lookup"><span data-stu-id="a8e06-124">Create an availability set</span></span>

<span data-ttu-id="a8e06-125">Вы можете создать группу доступности с помощью команды [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="a8e06-125">You can create an availability set using [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="a8e06-126">В этом примере задается количество доменах обновления и отказоустойчивости на обоих hello *2* для обеспечения доступности hello набор *myAvailabilitySet* в hello *myResourceGroupAvailability*группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a8e06-126">In this example, we set both hello number of update and fault domains at *2* for hello availability set named *myAvailabilitySet* in hello *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="a8e06-127">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a8e06-127">Create a resource group.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAvailability --location eastus
```


```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupAvailability \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

<span data-ttu-id="a8e06-128">Наборы доступности возможность tooisolate ресурсы в «домены сбоя» и «update доменов».</span><span class="sxs-lookup"><span data-stu-id="a8e06-128">Availability Sets allow you tooisolate resources across "fault domains" and "update domains".</span></span> <span data-ttu-id="a8e06-129">**Домен сбоя** представляет собой изолированную коллекцию ресурсов сервера, службы хранилища и сетевых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a8e06-129">A **fault domain** represents an isolated collection of server + network + storage resources.</span></span> <span data-ttu-id="a8e06-130">Предшествующий пример hello мы указываем, что мы хотим нашей доступности набора toobe распределяется по крайней мере в двух доменах отказоустойчивости при развертывании нашей виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="a8e06-130">In hello preceding example, we indicate that we want our availability set toobe distributed across at least two fault domains when our VMs are deployed.</span></span> <span data-ttu-id="a8e06-131">Кроме того, группу доступности необходимо распределить между двумя **доменами обновления**.</span><span class="sxs-lookup"><span data-stu-id="a8e06-131">We also indicate that we want our availability set distributed across two **update domains**.</span></span>  <span data-ttu-id="a8e06-132">Двумя доменами обновления убедитесь, что при Azure выполняет обновление программного обеспечения ресурсов виртуальной Машины изолированы, препятствует выполнению под нашей виртуальной Машины выполняется обновление на hello программное обеспечение hello то же время.</span><span class="sxs-lookup"><span data-stu-id="a8e06-132">Two update domains ensure that when Azure performs software updates our VM resources are isolated, preventing all hello software running underneath our VM from being updated at hello same time.</span></span>

## <a name="configure-virtual-network"></a><span data-ttu-id="a8e06-133">Настройка виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="a8e06-133">Configure virtual network</span></span>
<span data-ttu-id="a8e06-134">Перед развертыванием некоторые виртуальные машины и можно проверить балансировки, создайте hello, поддерживающие ресурсы виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="a8e06-134">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="a8e06-135">Дополнительные сведения о виртуальных сетях см. в разделе hello [управление виртуальными сетями Azure](tutorial-virtual-network.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="a8e06-135">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="a8e06-136">Создание сетевых ресурсов</span><span class="sxs-lookup"><span data-stu-id="a8e06-136">Create network resources</span></span>
<span data-ttu-id="a8e06-137">Создайте виртуальную сеть с помощью команды [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="a8e06-137">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="a8e06-138">Hello следующий пример создает виртуальную сеть с именем *myVnet* с подсеть с именем *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="a8e06-138">hello following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
<span data-ttu-id="a8e06-139">Для создания виртуальных сетевых карт используется команда [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="a8e06-139">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="a8e06-140">Hello следующий пример создает три виртуальных сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="a8e06-140">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="a8e06-141">(Один виртуальный сетевой Адаптер для каждой виртуальной Машины, создать приложение hello следующих шагов).</span><span class="sxs-lookup"><span data-stu-id="a8e06-141">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="a8e06-142">Можно создать в любое время дополнительных виртуальных сетевых адаптеров и виртуальные машины и добавить их toohello балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="a8e06-142">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupAvailability \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="a8e06-143">Создание виртуальных машин в группе доступности</span><span class="sxs-lookup"><span data-stu-id="a8e06-143">Create VMs inside an availability set</span></span>

<span data-ttu-id="a8e06-144">Виртуальные машины должны создаваться в том, что правильно распределены по оборудованию hello toomake набор доступности hello.</span><span class="sxs-lookup"><span data-stu-id="a8e06-144">VMs must be created within hello availability set toomake sure they are correctly distributed across hello hardware.</span></span> <span data-ttu-id="a8e06-145">Не удается добавить группу существующей виртуальной Машины tooan доступности после его создания.</span><span class="sxs-lookup"><span data-stu-id="a8e06-145">You can't add an existing VM tooan availability set after it is created.</span></span> 

<span data-ttu-id="a8e06-146">При создании виртуальной Машины с помощью [создания виртуальной машины az](/cli/azure/vm#create) укажите hello доступности с помощью hello `--availability-set` параметр toospecify hello имя набора доступности hello.</span><span class="sxs-lookup"><span data-stu-id="a8e06-146">When you create a VM using [az vm create](/cli/azure/vm#create) you specify hello availability set using hello `--availability-set` parameter toospecify hello name of hello availability set.</span></span>

```azurecli-interactive 
for i in `seq 1 2`; do
   az vm create \
     --resource-group myResourceGroupAvailability \
     --name myVM$i \
     --availability-set myAvailabilitySet \
     --nics myNic$i \
     --size Standard_DS1_v2  \
     --image Canonical:UbuntuServer:14.04.4-LTS:latest \
     --admin-username azureuser \
     --generate-ssh-keys \
     --no-wait
done 
```

<span data-ttu-id="a8e06-147">Теперь в созданной группе доступности у нас есть две виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="a8e06-147">We now have two virtual machines within our newly created availability set.</span></span> <span data-ttu-id="a8e06-148">Так как они находятся в hello же наборе доступности Azure гарантирует виртуальных машин, hello и все свои ресурсы (включая диски с данными) распределяются между изолированной физического оборудования.</span><span class="sxs-lookup"><span data-stu-id="a8e06-148">Because they are in hello same availability set, Azure will ensure that hello VMs and all their resources (including data disks) are distributed across isolated physical hardware.</span></span> <span data-ttu-id="a8e06-149">за счет чего обеспечивается более высокий уровень доступности общего решения виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a8e06-149">This distribution helps ensure much higher availability of our overall VM solution.</span></span>

<span data-ttu-id="a8e06-150">Единственное, что могут возникнуть при добавлении виртуальных машин — что определенного размера виртуальной Машины больше не доступны toouse в наборе доступности.</span><span class="sxs-lookup"><span data-stu-id="a8e06-150">One thing you may encounter as you add VMs is that a particular VM size is no longer available toouse within your availability set.</span></span> <span data-ttu-id="a8e06-151">Эта проблема может произойти, если больше не хватает tooadd емкости, сохраняя набор доступности hello правила изоляции hello контроллер обеспечивает соблюдение.</span><span class="sxs-lookup"><span data-stu-id="a8e06-151">This issue can happen if there is no longer enough capacity tooadd it while preserving hello isolation rules hello availability set enforces.</span></span> <span data-ttu-id="a8e06-152">Вы можете проверить toosee какие размеры виртуальных Машин, доступных toouse в существующий набор с помощью hello доступности `--availability-set list-sizes` параметра.</span><span class="sxs-lookup"><span data-stu-id="a8e06-152">You can check toosee what VM sizes are available toouse within an existing availability set using hello `--availability-set list-sizes` parameter.</span></span>

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="a8e06-153">Знакомство с доступными размерами виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="a8e06-153">Check for available VM sizes</span></span> 

<span data-ttu-id="a8e06-154">Можно добавить дополнительные виртуальные машины toohello доступности более поздней версии, но необходимо tooknow какие размеры виртуальных Машин доступны на оборудовании hello.</span><span class="sxs-lookup"><span data-stu-id="a8e06-154">You can add more VMs toohello availability set later, but you need tooknow what VM sizes are available on hello hardware.</span></span> <span data-ttu-id="a8e06-155">Используйте [список размеров az набора доступности виртуальных машин](/cli/azure/availability-set#list-sizes) toolist все доступные размеры hello на оборудовании hello кластера для группы доступности hello.</span><span class="sxs-lookup"><span data-stu-id="a8e06-155">Use [az vm availability-set list-sizes](/cli/azure/availability-set#list-sizes) toolist all hello available sizes on hello hardware cluster for hello availability set.</span></span>

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a><span data-ttu-id="a8e06-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a8e06-156">Next steps</span></span>

<span data-ttu-id="a8e06-157">Из этого руководства вы узнали, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="a8e06-157">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a8e06-158">"Создать группу доступности"</span><span class="sxs-lookup"><span data-stu-id="a8e06-158">Create an availability set</span></span>
> * <span data-ttu-id="a8e06-159">Создание виртуальной машины в группе доступности</span><span class="sxs-lookup"><span data-stu-id="a8e06-159">Create a VM in an availability set</span></span>
> * <span data-ttu-id="a8e06-160">Проверка доступных размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="a8e06-160">Check available VM sizes</span></span>

<span data-ttu-id="a8e06-161">Переместить следующий учебник toolearn toohello о наборы масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="a8e06-161">Advance toohello next tutorial toolearn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a8e06-162">Создание масштабируемого набора виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="a8e06-162">Create a VM scale set</span></span>](tutorial-create-vmss.md)

