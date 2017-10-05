---
title: "Создание пользовательских образов виртуальных машин с помощью Azure CLI | Документы Майкрософт"
description: "Руководство по созданию настраиваемого образа виртуальной машины с помощью Azure CLI."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/21/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: d32980f05ad17a76793021d0a5355d597974a4e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-the-cli"></a><span data-ttu-id="06462-103">Создание пользовательского образа виртуальной машины Azure с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="06462-103">Create a custom image of an Azure VM using the CLI</span></span>

<span data-ttu-id="06462-104">Пользовательские образы похожи на образы магазина, однако их можно создавать самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="06462-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="06462-105">Пользовательские образы можно использовать для начальной загрузки конфигураций, например при предварительной загрузке приложений, конфигураций приложений и других конфигураций операционной системы.</span><span class="sxs-lookup"><span data-stu-id="06462-105">Custom images can be used to bootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="06462-106">В рамках этого руководства вы создадите собственный пользовательский образ виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="06462-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="06462-107">Вы узнаете, как выполнять такие задачи.</span><span class="sxs-lookup"><span data-stu-id="06462-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="06462-108">отменить подготовку виртуальных машин и подготовить их к использованию;</span><span class="sxs-lookup"><span data-stu-id="06462-108">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="06462-109">создавать пользовательский образ;</span><span class="sxs-lookup"><span data-stu-id="06462-109">Create a custom image</span></span>
> * <span data-ttu-id="06462-110">Создание виртуальной машины из пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="06462-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="06462-111">Получение списка всех образов в подписке</span><span class="sxs-lookup"><span data-stu-id="06462-111">List all the images in your subscription</span></span>
> * <span data-ttu-id="06462-112">Удаление образа</span><span class="sxs-lookup"><span data-stu-id="06462-112">Delete an image</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="06462-113">Если вы решили установить и использовать интерфейс командной строки локально, то для работы с этим руководством вам понадобится Azure CLI 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="06462-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="06462-114">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="06462-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="06462-115">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="06462-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="06462-116">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="06462-116">Before you begin</span></span>

<span data-ttu-id="06462-117">Ниже подробно описано, как преобразовать существующую виртуальную машину в многократно используемый пользовательский образ, на основе которого можно создавать экземпляры виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="06462-117">The steps below detail how to take an existing VM and turn it into a re-usable custom image that you can use to create new VM instances.</span></span>

<span data-ttu-id="06462-118">Для выполнения примера в этом руководстве требуется виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="06462-118">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="06462-119">Этот [пример сценария](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) позволяет создать ее при необходимости.</span><span class="sxs-lookup"><span data-stu-id="06462-119">If needed, this [script sample](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) can create one for you.</span></span> <span data-ttu-id="06462-120">При работе с примером по мере необходимости заменяйте имена групп ресурсов и виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="06462-120">When working through the tutorial, replace the resource group and VM names where needed.</span></span>

## <a name="create-a-custom-image"></a><span data-ttu-id="06462-121">Создание пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="06462-121">Create a custom image</span></span>

<span data-ttu-id="06462-122">Чтобы создать образ виртуальной машины, нужно подготовить виртуальную машину, выполнив отзыв, отменив выделение и пометив исходную виртуальную машину как обобщенную.</span><span class="sxs-lookup"><span data-stu-id="06462-122">To create an image of a virtual machine, you need to prepare the VM by deprovisioning, deallocating, and then marking the source VM as generalized.</span></span> <span data-ttu-id="06462-123">После подготовки виртуальной машины вы можете создать образ.</span><span class="sxs-lookup"><span data-stu-id="06462-123">Once the VM has been prepared, you can create an image.</span></span>

### <a name="deprovision-the-vm"></a><span data-ttu-id="06462-124">Отзыв виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="06462-124">Deprovision the VM</span></span> 

<span data-ttu-id="06462-125">Отзыв обобщает виртуальную машину, удаляя относящиеся к ней сведения.</span><span class="sxs-lookup"><span data-stu-id="06462-125">Deprovisioning generalizes the VM by removing machine-specific information.</span></span> <span data-ttu-id="06462-126">Такое обобщение позволяет развернуть множество виртуальных машин из одного образа.</span><span class="sxs-lookup"><span data-stu-id="06462-126">This generalization makes it possible to deploy many VMs from a single image.</span></span> <span data-ttu-id="06462-127">Во время отзыва имя узла сбрасывается и принимает значение *localhost.localdomain*.</span><span class="sxs-lookup"><span data-stu-id="06462-127">During deprovisioning, the host name is reset to *localhost.localdomain*.</span></span> <span data-ttu-id="06462-128">Ключи узла SSH, конфигурации сервера доменных имен, пароль учетной записи root и кэшированные аренды DHCP также удаляются.</span><span class="sxs-lookup"><span data-stu-id="06462-128">SSH host keys, nameserver configurations, root password, and cached DHCP leases are also deleted.</span></span>

<span data-ttu-id="06462-129">Чтобы отозвать виртуальную машину, используйте агент виртуальной машины Azure (waagent).</span><span class="sxs-lookup"><span data-stu-id="06462-129">To deprovision the VM, use the Azure VM agent (waagent).</span></span> <span data-ttu-id="06462-130">Агент виртуальной машины Azure устанавливается на виртуальной машине и управляет подготовкой и взаимодействием с контроллером структуры Azure.</span><span class="sxs-lookup"><span data-stu-id="06462-130">The Azure VM agent is installed on the VM and manages provisioning and interacting with the Azure Fabric Controller.</span></span> <span data-ttu-id="06462-131">Дополнительные сведения см. в [руководстве пользователя агента Linux Azure](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="06462-131">For more information, see the [Azure Linux Agent user guide](agent-user-guide.md).</span></span>

<span data-ttu-id="06462-132">Подключитесь к виртуальной машине с помощью SSH и выполните команду для ее отзыва.</span><span class="sxs-lookup"><span data-stu-id="06462-132">Connect to your VM using SSH and run the command to deprovision the VM.</span></span> <span data-ttu-id="06462-133">При указании аргумента `+user` также удаляется последняя подготовленная учетная запись пользователя вместе со связанными данными.</span><span class="sxs-lookup"><span data-stu-id="06462-133">With the `+user` argument, the last provisioned user account and any associated data are also deleted.</span></span> <span data-ttu-id="06462-134">Замените IP-адрес в примере общедоступным IP-адресом виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="06462-134">Replace the example IP address with the public IP address of your VM.</span></span>

<span data-ttu-id="06462-135">Подключитесь к виртуальной машине по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="06462-135">SSH to the VM.</span></span>
```bash
ssh azureuser@52.174.34.95
```
<span data-ttu-id="06462-136">Отзовите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="06462-136">Deprovision the VM.</span></span>

```bash
sudo waagent -deprovision+user -force
```
<span data-ttu-id="06462-137">Закройте сеанс SSH.</span><span class="sxs-lookup"><span data-stu-id="06462-137">Close the SSH session.</span></span>

```bash
exit
```

### <a name="deallocate-and-mark-the-vm-as-generalized"></a><span data-ttu-id="06462-138">Отмена выделения и пометка виртуальной машины как обобщенной</span><span class="sxs-lookup"><span data-stu-id="06462-138">Deallocate and mark the VM as generalized</span></span>

<span data-ttu-id="06462-139">Чтобы создать образ, нужно отменить выделение виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="06462-139">To create an image, the VM needs to be deallocated.</span></span> <span data-ttu-id="06462-140">Отмените выделение виртуальной машины с помощью команды [az vm deallocate](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="06462-140">Deallocate the VM using [az vm deallocate](/cli//azure/vm#deallocate).</span></span> 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="06462-141">Наконец, сообщите платформе Azure, что виртуальная машина подготовлена к использованию, выполнив команду [az vm generalize](/cli//azure/vm#generalize).</span><span class="sxs-lookup"><span data-stu-id="06462-141">Finally, set the state of the VM as generalized with [az vm generalize](/cli//azure/vm#generalize) so the Azure platform knows the VM has been generalized.</span></span> <span data-ttu-id="06462-142">Создать образ можно только из подготовленной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="06462-142">You can only create an image from a generalized VM.</span></span>
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-the-image"></a><span data-ttu-id="06462-143">Создание образа</span><span class="sxs-lookup"><span data-stu-id="06462-143">Create the image</span></span>

<span data-ttu-id="06462-144">Теперь можно создать образ виртуальной машины с помощью команды [az image create](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="06462-144">Now you can create an image of the VM by using [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="06462-145">В следующем примере создается образ *myImage* из виртуальной машины *myVM*.</span><span class="sxs-lookup"><span data-stu-id="06462-145">The following example creates an image named *myImage* from a VM named *myVM*.</span></span>
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-the-image"></a><span data-ttu-id="06462-146">Создание виртуальных машин из образа</span><span class="sxs-lookup"><span data-stu-id="06462-146">Create VMs from the image</span></span>

<span data-ttu-id="06462-147">Теперь, когда образ готов, из него можно создать одну или несколько виртуальных машин с помощью команды [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="06462-147">Now that you have an image, you can create one or more new VMs from the image using [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="06462-148">В следующем примере создается виртуальная машина *myVMfromImage* из образа *myImage*.</span><span class="sxs-lookup"><span data-stu-id="06462-148">The following example creates a VM named *myVMfromImage* from the image named *myImage*.</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a><span data-ttu-id="06462-149">Управление образами</span><span class="sxs-lookup"><span data-stu-id="06462-149">Image management</span></span> 

<span data-ttu-id="06462-150">Ниже приведены некоторые примеры распространенных задач управления образами, а также способы их настройки с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="06462-150">Here are some examples of common image management tasks and how to complete them using the Azure CLI.</span></span>

<span data-ttu-id="06462-151">Получение списка всех образов по имени в формате таблицы.</span><span class="sxs-lookup"><span data-stu-id="06462-151">List all images by name in a table format.</span></span>

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

<span data-ttu-id="06462-152">Удаление образа.</span><span class="sxs-lookup"><span data-stu-id="06462-152">Delete an image.</span></span> <span data-ttu-id="06462-153">В этом примере из *myResourceGroup* удаляется образ с именем *myOldImage*.</span><span class="sxs-lookup"><span data-stu-id="06462-153">This example deletes the image named *myOldImage* from the *myResourceGroup*.</span></span>

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="06462-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="06462-154">Next steps</span></span>

<span data-ttu-id="06462-155">В рамках этого руководства вы создали пользовательский образ виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="06462-155">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="06462-156">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="06462-156">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="06462-157">отменять подготовку виртуальных машин и подготавливать их к использованию;</span><span class="sxs-lookup"><span data-stu-id="06462-157">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="06462-158">создавать пользовательский образ;</span><span class="sxs-lookup"><span data-stu-id="06462-158">Create a custom image</span></span>
> * <span data-ttu-id="06462-159">Создание виртуальной машины из пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="06462-159">Create a VM from a custom image</span></span>
> * <span data-ttu-id="06462-160">Получение списка всех образов в подписке</span><span class="sxs-lookup"><span data-stu-id="06462-160">List all the images in your subscription</span></span>
> * <span data-ttu-id="06462-161">удалять образ.</span><span class="sxs-lookup"><span data-stu-id="06462-161">Delete an image</span></span>

<span data-ttu-id="06462-162">Перейдите к следующему руководству, чтобы узнать о высокодоступных виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="06462-162">Advance to the next tutorial to learn about highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="06462-163">[Создание высокодоступных виртуальных машин](tutorial-availability-sets.md)</span><span class="sxs-lookup"><span data-stu-id="06462-163">[Create highly available VMs](tutorial-availability-sets.md).</span></span>

