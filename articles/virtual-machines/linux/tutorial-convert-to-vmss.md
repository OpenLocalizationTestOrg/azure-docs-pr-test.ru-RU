---
title: "набор масштабирования виртуальной Машины Azure tooa aaaConvert | Документы Microsoft"
description: "Создание и развертывание с hello Azure CLI масштабирования виртуальных машин Linux Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/05/2017
ms.author: adegeo
ms.openlocfilehash: e228282ac4855cef589b8500e74e9d461f9aed84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="convert-an-existing-azure-virtual-machine-tooa-scale-set"></a><span data-ttu-id="175db-103">Преобразовать существующий набор масштабирования виртуальной машины Azure tooa</span><span class="sxs-lookup"><span data-stu-id="175db-103">Convert an existing Azure virtual machine tooa scale set</span></span>

<span data-ttu-id="175db-104">Этот учебник показывает, как tooconvert toouse Azure CLI 2.0 tooa виртуальной машины набора масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="175db-104">This tutorial shows you how toouse Azure CLI 2.0 tooconvert a virtual machine tooa virtual machine scale set.</span></span> <span data-ttu-id="175db-105">Вы также узнаете, как задать конфигурации hello tooautomate hello виртуальных машин на шкале hello.</span><span class="sxs-lookup"><span data-stu-id="175db-105">You also learn how tooautomate hello configuration of hello virtual machines in hello scale set.</span></span> <span data-ttu-id="175db-106">Дополнительные сведения о том, как tooinstall Azure CLI версии 2.0, см. [Приступая к работе с Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="175db-106">For more information on how tooinstall Azure CLI 2.0, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span> <span data-ttu-id="175db-107">Дополнительные сведения о наборах масштабирования см. в разделе [Наборы масштабирования виртуальных машин](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="175db-107">For more information about scale sets, see [Virtual Machine Scale Sets](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span></span>

## <a name="step-1---deprovision-hello-vm"></a><span data-ttu-id="175db-108">Шаг 1 hello отзыв виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="175db-108">Step 1 - Deprovision hello VM</span></span>

<span data-ttu-id="175db-109">С помощью SSH tooconnect toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="175db-109">Use SSH tooconnect toohello VM.</span></span>

<span data-ttu-id="175db-110">Hello отзыв виртуальной Машины с помощью файлов toodelete агента ВМ Azure hello и данных.</span><span class="sxs-lookup"><span data-stu-id="175db-110">Deprovision hello VM using hello Azure VM agent toodelete files and data.</span></span> <span data-ttu-id="175db-111">Подробный обзор отзыва представлен в разделе [Запись образа виртуальной машины Linux](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="175db-111">For a detailed overview of deprovisioning, see [Capture a Linux virtual machine](capture-image.md).</span></span>

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-hello-vm"></a><span data-ttu-id="175db-112">Шаг 2 - запись образа виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="175db-112">Step 2 - Capture an image of hello VM</span></span>

<span data-ttu-id="175db-113">Подробный обзор записи представлен в разделе [Запись образа виртуальной машины Linux](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="175db-113">For a detailed overview of capturing, see [Capture a Linux virtual machine](capture-image.md).</span></span>

<span data-ttu-id="175db-114">DEALLOCATE hello виртуальной Машины с [ВМ az deallocate](/cli/azure/vm#deallocate):</span><span class="sxs-lookup"><span data-stu-id="175db-114">Deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate):</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="175db-115">Обобщить hello виртуальной Машины с [ВМ az generalize](/cli/azure/vm#generalize):</span><span class="sxs-lookup"><span data-stu-id="175db-115">Generalize hello VM with [az vm generalize](/cli/azure/vm#generalize):</span></span>

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="175db-116">Создать образ на hello ресурса виртуальной Машины с [создать образ az](/cli/azure/image#create):</span><span class="sxs-lookup"><span data-stu-id="175db-116">Create an image from hello VM resource with [az image create](/cli/azure/image#create):</span></span>

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-hello-scale-set"></a><span data-ttu-id="175db-117">Шаг 3 — Создание набора масштабирования hello</span><span class="sxs-lookup"><span data-stu-id="175db-117">Step 3 - Create hello scale set</span></span>

<span data-ttu-id="175db-118">Получить hello **идентификатор** hello изображения.</span><span class="sxs-lookup"><span data-stu-id="175db-118">Get hello **id** of hello image.</span></span>

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

<span data-ttu-id="175db-119">Создайте виртуальную машину из ресурса образа с помощью команды [az vmss create](/cli/azure/vmss#create).</span><span class="sxs-lookup"><span data-stu-id="175db-119">Create a VM from your image resource with [az vmss create](/cli/azure/vmss#create):</span></span>

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

<span data-ttu-id="175db-120">Эта команда также подключает диск данных емкостью в 10 ГБ.</span><span class="sxs-lookup"><span data-stu-id="175db-120">This command also attached a 10gb data disk.</span></span> <span data-ttu-id="175db-121">Имейте в виду, что в зависимости от hello виртуальной Машины выбранного размера (мы использовали **Standard_DS1_v2**), количество дисков данных, допустимых в hello отличается.</span><span class="sxs-lookup"><span data-stu-id="175db-121">Keep in mind that depending on hello VM size chosen (we used **Standard_DS1_v2**), hello number of data disks allowed is different.</span></span> <span data-ttu-id="175db-122">Дополнительные сведения см. в статье hello [размеры виртуальных машин](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="175db-122">For more information, review hello [virtual machine sizes](sizes.md).</span></span>

<span data-ttu-id="175db-123">После завершения набора масштабирования hello, connect tooit.</span><span class="sxs-lookup"><span data-stu-id="175db-123">Once hello scale set finishes, connect tooit.</span></span> <span data-ttu-id="175db-124">Получить список IP-адресов для hello экземпляров для SSH с [списка vmss az-экземпляр соединения info](/cli/azure/vmss#list-instance-connection-info):</span><span class="sxs-lookup"><span data-stu-id="175db-124">Get a list of IP addresses for hello instances for SSH with [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info):</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

<span data-ttu-id="175db-125">Теперь можно подключить диск данных hello tooinitialize экземпляр toohello виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="175db-125">Now you can connect toohello virtual machine instance tooinitialize hello data disk</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-hello-data-disk"></a><span data-ttu-id="175db-126">Шаг 4. инициализация диска данных hello</span><span class="sxs-lookup"><span data-stu-id="175db-126">Step 4 - Initialize hello data disk</span></span>

<span data-ttu-id="175db-127">При подключенном toohello виртуальной машины, создать разделы на диске hello с `fdisk`:</span><span class="sxs-lookup"><span data-stu-id="175db-127">While connected toohello virtual machine, partition hello disk with `fdisk`:</span></span>

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="175db-128">Запись toohello разделе с файловой системой hello `mkfs` команды:</span><span class="sxs-lookup"><span data-stu-id="175db-128">Write a file system toohello partition with hello `mkfs` command:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="175db-129">Подключите новый диск hello, чтобы она доступна в операционной системе hello:</span><span class="sxs-lookup"><span data-stu-id="175db-129">Mount hello new disk so that it is accessible in hello operating system:</span></span>

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="175db-130">Hello диск теперь может быть доступ через монтирования datadrive hello, который может быть проверена с помощью `ls /datadrive/`.</span><span class="sxs-lookup"><span data-stu-id="175db-130">hello disk can now be accesses through hello datadrive mountpoint, which can be verified with `ls /datadrive/`.</span></span>

<span data-ttu-id="175db-131">Завершение сеанса SSH hello.</span><span class="sxs-lookup"><span data-stu-id="175db-131">End hello SSH session.</span></span>


## <a name="step-5---configure-firewall"></a><span data-ttu-id="175db-132">Шаг 5. Настройка брандмауэра</span><span class="sxs-lookup"><span data-stu-id="175db-132">Step 5 - Configure firewall</span></span>

<span data-ttu-id="175db-133">Дырокол бреши hello брандмауэра toohello webserver размещенных набором масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="175db-133">Punch a hole through hello firewall toohello webserver hosted by hello scale set.</span></span> <span data-ttu-id="175db-134">Когда был создан набор масштабирования hello, также было создано подсистемы балансировки нагрузки и он был использован **SSH** toohello отдельных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="175db-134">When hello scale set was created, a load balancer was also created, and you used it **SSH** toohello individual virtual machines.</span></span> <span data-ttu-id="175db-135">tooopen порт требуется два блока данных, который можно получить с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="175db-135">tooopen a port, you need two pieces of information, which you can get using Azure CLI.</span></span>

* <span data-ttu-id="175db-136">**Интерфейсный пул IP-адресов**</span><span class="sxs-lookup"><span data-stu-id="175db-136">**Frontend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* <span data-ttu-id="175db-137">**Внутренний пул IP-адресов**</span><span class="sxs-lookup"><span data-stu-id="175db-137">**Backend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

<span data-ttu-id="175db-138">С помощью этих двух имен можно открыть порт **80**.</span><span class="sxs-lookup"><span data-stu-id="175db-138">With those two names, you can open port **80**.</span></span>

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a><span data-ttu-id="175db-139">Шаг 6. Автоматизация настройки</span><span class="sxs-lookup"><span data-stu-id="175db-139">Step 6 - Automate configuration</span></span>

<span data-ttu-id="175db-140">диск данных Hello должен toobe, настроенный на каждый экземпляр виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="175db-140">hello data disk needs toobe configured on each virtual machine instance.</span></span> <span data-ttu-id="175db-141">Мы можете автоматизировать настройку hello hello виртуальную машину с hello **CustomScript** расширения.</span><span class="sxs-lookup"><span data-stu-id="175db-141">We can automate hello configuration of hello virtual machine with hello **CustomScript** extension.</span></span>

<span data-ttu-id="175db-142">Сначала создайте *.sh* скрипт, который содержит команды форматирования диска hello.</span><span class="sxs-lookup"><span data-stu-id="175db-142">First, create a *.sh* script that includes hello disk format commands.</span></span>

```sh
#!/bin/bash

# Setup hello data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

<span data-ttu-id="175db-143">Затем отправка, hello toowhere файла сценария **CustomScript** доступ к нему расширение.</span><span class="sxs-lookup"><span data-stu-id="175db-143">Next, upload that script file toowhere hello **CustomScript** extension can access it.</span></span> <span data-ttu-id="175db-144">Копия доступна [здесь](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span><span class="sxs-lookup"><span data-stu-id="175db-144">A copy is available [here](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span></span>

<span data-ttu-id="175db-145">Создание локального файла с именем **settings.json** и put hello после блока JSON в нем.</span><span class="sxs-lookup"><span data-stu-id="175db-145">Create a local file named **settings.json** and put hello following JSON block in it.</span></span> <span data-ttu-id="175db-146">Hello `flieUris` toowhere, отправленный в файле сценария необходимо задать для свойства.</span><span class="sxs-lookup"><span data-stu-id="175db-146">hello `flieUris` property should be set toowhere your script file was uploaded to.</span></span>

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

<span data-ttu-id="175db-147">Развертывание этой команды tooyour набор масштабирования с hello **CustomScript** расширения, ссылающиеся на hello **settings.json** только что созданный файл.</span><span class="sxs-lookup"><span data-stu-id="175db-147">Deploy this command tooyour scale set with hello **CustomScript** extension, referencing hello **settings.json** file we just created.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

<span data-ttu-id="175db-148">Это расширение автоматически запускается на всех текущих экземплярах и экземплярах, который будут созданы позже при масштабировании.</span><span class="sxs-lookup"><span data-stu-id="175db-148">This extension automatically runs on all current instances, and any instances later created by scaling.</span></span>

## <a name="step-7---configure-autoscale-rules"></a><span data-ttu-id="175db-149">Шаг 7. Настройка правил автомасштабирования</span><span class="sxs-lookup"><span data-stu-id="175db-149">Step 7 - Configure autoscale rules</span></span>

<span data-ttu-id="175db-150">В настоящее время с помощью Azure CLI нельзя задать правила автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="175db-150">Currently, autoscale rules cannot be set in Azure CLI.</span></span> <span data-ttu-id="175db-151">Используйте hello [портал Azure](https://portal.azure.com) tooconfigure автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="175db-151">Use hello [Azure portal](https://portal.azure.com) tooconfigure autoscale.</span></span>

## <a name="step-8---management-tasks"></a><span data-ttu-id="175db-152">Шаг 8. Задачи управления</span><span class="sxs-lookup"><span data-stu-id="175db-152">Step 8 - Management tasks</span></span>

<span data-ttu-id="175db-153">На протяжении жизненного цикла hello набора масштабирования hello, может потребоваться toorun одну или несколько задач управления.</span><span class="sxs-lookup"><span data-stu-id="175db-153">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="175db-154">Кроме того вы можете toocreate скрипты, автоматизирующие различные жизненного цикла задачи и hello Azure CLI предоставляет toodo быстро этих задач.</span><span class="sxs-lookup"><span data-stu-id="175db-154">Additionally, you may want toocreate scripts that automate various lifecycle-tasks, and hello Azure CLI provides a quick way toodo those tasks.</span></span> <span data-ttu-id="175db-155">Ниже приведено несколько распространенных задач.</span><span class="sxs-lookup"><span data-stu-id="175db-155">Here are a few common tasks.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="175db-156">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="175db-156">Get connection info</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a><span data-ttu-id="175db-157">Задание числа экземпляров (ручное масштабирование)</span><span class="sxs-lookup"><span data-stu-id="175db-157">Set instance count (manual scale)</span></span>

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a><span data-ttu-id="175db-158">Удалить группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="175db-158">Delete resource group</span></span>

<span data-ttu-id="175db-159">При удалении группы ресурсов будут также удалены все ресурсы, содержащиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="175db-159">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="175db-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="175db-160">Next steps</span></span>
<span data-ttu-id="175db-161">см. Дополнительные сведения о некоторых масштабирования виртуальных машин hello набор возможностей, представленных в этом учебнике toolearn hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="175db-161">toolearn more about some of hello virtual machine scale set features introduced in this tutorial, see hello following information:</span></span>

- [<span data-ttu-id="175db-162">Общие сведения о масштабируемых наборах виртуальных машин в Azure</span><span class="sxs-lookup"><span data-stu-id="175db-162">Azure Virtual Machine Scale Sets overview</span></span>](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [<span data-ttu-id="175db-163">Обзор Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="175db-163">Azure Load Balancer overview</span></span>](../../load-balancer/load-balancer-overview.md)
- [<span data-ttu-id="175db-164">Управление потоком сетевого трафика с помощью групп безопасности сети</span><span class="sxs-lookup"><span data-stu-id="175db-164">Control network traffic flow with network security groups</span></span>](../../virtual-network/virtual-networks-nsg.md)