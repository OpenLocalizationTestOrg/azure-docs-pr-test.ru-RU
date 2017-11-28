---
title: "aaaCreate пользовательских образов виртуальной Машины с hello Azure CLI | Документы Microsoft"
description: "Учебник - создать образ виртуальной Машины с помощью hello Azure CLI."
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
ms.openlocfilehash: 217a993c0c1d48939b74108ac6c5f7a1a619416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-hello-cli"></a><span data-ttu-id="64aea-103">Создать образ виртуальной машины Azure с помощью hello CLI</span><span class="sxs-lookup"><span data-stu-id="64aea-103">Create a custom image of an Azure VM using hello CLI</span></span>

<span data-ttu-id="64aea-104">Пользовательские образы похожи на образы магазина, однако их можно создавать самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="64aea-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="64aea-105">Пользовательские изображения может быть конфигурации используется toobootstrap, такие как предварительной загрузки приложений, конфигурации приложений и других настроек операционной системы.</span><span class="sxs-lookup"><span data-stu-id="64aea-105">Custom images can be used toobootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="64aea-106">В рамках этого руководства вы создадите собственный пользовательский образ виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="64aea-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="64aea-107">Вы узнаете, как выполнять такие задачи.</span><span class="sxs-lookup"><span data-stu-id="64aea-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="64aea-108">отменить подготовку виртуальных машин и подготовить их к использованию;</span><span class="sxs-lookup"><span data-stu-id="64aea-108">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="64aea-109">создавать пользовательский образ;</span><span class="sxs-lookup"><span data-stu-id="64aea-109">Create a custom image</span></span>
> * <span data-ttu-id="64aea-110">Создание виртуальной машины из пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="64aea-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="64aea-111">Отображение списка всех образов hello в подписке</span><span class="sxs-lookup"><span data-stu-id="64aea-111">List all hello images in your subscription</span></span>
> * <span data-ttu-id="64aea-112">удалять образ.</span><span class="sxs-lookup"><span data-stu-id="64aea-112">Delete an image</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="64aea-113">Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="64aea-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="64aea-114">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="64aea-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="64aea-115">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="64aea-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="64aea-116">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="64aea-116">Before you begin</span></span>

<span data-ttu-id="64aea-117">в следующих шагах Hello подробно, как tootake существующей виртуальной Машины и включите его в доступных для использования пользовательского образа, который можно использовать toocreate новые экземпляры виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="64aea-117">hello steps below detail how tootake an existing VM and turn it into a re-usable custom image that you can use toocreate new VM instances.</span></span>

<span data-ttu-id="64aea-118">Пример hello toocomplete в этом учебнике, необходимо иметь существующую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="64aea-118">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="64aea-119">Этот [пример сценария](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) позволяет создать ее при необходимости.</span><span class="sxs-lookup"><span data-stu-id="64aea-119">If needed, this [script sample](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) can create one for you.</span></span> <span data-ttu-id="64aea-120">Если заменить прохождение учебника hello группы ресурсов hello и ВМ имен при необходимости.</span><span class="sxs-lookup"><span data-stu-id="64aea-120">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

## <a name="create-a-custom-image"></a><span data-ttu-id="64aea-121">создавать пользовательский образ;</span><span class="sxs-lookup"><span data-stu-id="64aea-121">Create a custom image</span></span>

<span data-ttu-id="64aea-122">toocreate образ виртуальной машины, необходимо tooprepare hello виртуальной Машины путем отмены подготовки, освобождение и пометки hello исходной виртуальной Машины, как обобщенный.</span><span class="sxs-lookup"><span data-stu-id="64aea-122">toocreate an image of a virtual machine, you need tooprepare hello VM by deprovisioning, deallocating, and then marking hello source VM as generalized.</span></span> <span data-ttu-id="64aea-123">Один раз при hello, который был подготовлен виртуальной Машины, можно создать образ.</span><span class="sxs-lookup"><span data-stu-id="64aea-123">Once hello VM has been prepared, you can create an image.</span></span>

### <a name="deprovision-hello-vm"></a><span data-ttu-id="64aea-124">Hello отзыв виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="64aea-124">Deprovision hello VM</span></span> 

<span data-ttu-id="64aea-125">Отзыв обобщает hello виртуальных Машин, удалив сведения о компьютере.</span><span class="sxs-lookup"><span data-stu-id="64aea-125">Deprovisioning generalizes hello VM by removing machine-specific information.</span></span> <span data-ttu-id="64aea-126">Из этого общего правила делает возможных toodeploy много виртуальных машин из одного образа.</span><span class="sxs-lookup"><span data-stu-id="64aea-126">This generalization makes it possible toodeploy many VMs from a single image.</span></span> <span data-ttu-id="64aea-127">Во время отмены подготовки, имя узла hello сбрасывается слишком*localhost.localdomain*.</span><span class="sxs-lookup"><span data-stu-id="64aea-127">During deprovisioning, hello host name is reset too*localhost.localdomain*.</span></span> <span data-ttu-id="64aea-128">Ключи узла SSH, конфигурации сервера доменных имен, пароль учетной записи root и кэшированные аренды DHCP также удаляются.</span><span class="sxs-lookup"><span data-stu-id="64aea-128">SSH host keys, nameserver configurations, root password, and cached DHCP leases are also deleted.</span></span>

<span data-ttu-id="64aea-129">hello toodeprovision виртуальной Машины, с помощью агента ВМ Azure hello (waagent).</span><span class="sxs-lookup"><span data-stu-id="64aea-129">toodeprovision hello VM, use hello Azure VM agent (waagent).</span></span> <span data-ttu-id="64aea-130">агент ВМ Azure Hello устанавливается на hello виртуальной Машины и управляет подготовки и работать с ними hello Azure Fabric Controller.</span><span class="sxs-lookup"><span data-stu-id="64aea-130">hello Azure VM agent is installed on hello VM and manages provisioning and interacting with hello Azure Fabric Controller.</span></span> <span data-ttu-id="64aea-131">Дополнительные сведения см. в разделе hello [руководство пользователя Azure Linux Agent](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="64aea-131">For more information, see hello [Azure Linux Agent user guide](agent-user-guide.md).</span></span>

<span data-ttu-id="64aea-132">Подключение tooyour виртуальной Машины с помощью SSH и выполнения hello команда toodeprovision hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="64aea-132">Connect tooyour VM using SSH and run hello command toodeprovision hello VM.</span></span> <span data-ttu-id="64aea-133">С hello `+user` аргумента, hello последнюю подготовленный пользователь учетную запись и все связанные с ними данные удаляются.</span><span class="sxs-lookup"><span data-stu-id="64aea-133">With hello `+user` argument, hello last provisioned user account and any associated data are also deleted.</span></span> <span data-ttu-id="64aea-134">Замените IP-адрес hello пример hello общедоступный IP-адрес виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="64aea-134">Replace hello example IP address with hello public IP address of your VM.</span></span>

<span data-ttu-id="64aea-135">Toohello SSH виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="64aea-135">SSH toohello VM.</span></span>
```bash
ssh azureuser@52.174.34.95
```
<span data-ttu-id="64aea-136">Здравствуйте, отзыв виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="64aea-136">Deprovision hello VM.</span></span>

```bash
sudo waagent -deprovision+user -force
```
<span data-ttu-id="64aea-137">Закрыть сеанс SSH hello.</span><span class="sxs-lookup"><span data-stu-id="64aea-137">Close hello SSH session.</span></span>

```bash
exit
```

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a><span data-ttu-id="64aea-138">Выделение и пометить hello виртуальной Машины как обобщенный</span><span class="sxs-lookup"><span data-stu-id="64aea-138">Deallocate and mark hello VM as generalized</span></span>

<span data-ttu-id="64aea-139">toocreate изображения hello виртуальной Машины должен toobe освобождена.</span><span class="sxs-lookup"><span data-stu-id="64aea-139">toocreate an image, hello VM needs toobe deallocated.</span></span> <span data-ttu-id="64aea-140">DEALLOCATE hello виртуальной Машины с помощью [ВМ az deallocate](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="64aea-140">Deallocate hello VM using [az vm deallocate](/cli//azure/vm#deallocate).</span></span> 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="64aea-141">Задайте состояние hello hello виртуальной Машины как универсализации с [ВМ az generalize](/cli//azure/vm#generalize) чтобы hello ВМ обобщенный знал hello платформы Azure.</span><span class="sxs-lookup"><span data-stu-id="64aea-141">Finally, set hello state of hello VM as generalized with [az vm generalize](/cli//azure/vm#generalize) so hello Azure platform knows hello VM has been generalized.</span></span> <span data-ttu-id="64aea-142">Создать образ можно только из подготовленной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="64aea-142">You can only create an image from a generalized VM.</span></span>
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-hello-image"></a><span data-ttu-id="64aea-143">Создание образа hello</span><span class="sxs-lookup"><span data-stu-id="64aea-143">Create hello image</span></span>

<span data-ttu-id="64aea-144">Теперь можно создавать с помощью образа виртуальной Машины hello [создать образ az](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="64aea-144">Now you can create an image of hello VM by using [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="64aea-145">Hello следующий пример создает образ с именем *myImage* из виртуальной Машины с именем *myVM*.</span><span class="sxs-lookup"><span data-stu-id="64aea-145">hello following example creates an image named *myImage* from a VM named *myVM*.</span></span>
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-hello-image"></a><span data-ttu-id="64aea-146">Создать виртуальные машины из образа hello</span><span class="sxs-lookup"><span data-stu-id="64aea-146">Create VMs from hello image</span></span>

<span data-ttu-id="64aea-147">Теперь, когда у вас есть образ, можно создать один или несколько новых виртуальных машин из hello изображения с помощью [создания виртуальной машины az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="64aea-147">Now that you have an image, you can create one or more new VMs from hello image using [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="64aea-148">Hello следующий пример создает Виртуальную машину с именем *myVMfromImage* из образа hello с именем *myImage*.</span><span class="sxs-lookup"><span data-stu-id="64aea-148">hello following example creates a VM named *myVMfromImage* from hello image named *myImage*.</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a><span data-ttu-id="64aea-149">Управление образами</span><span class="sxs-lookup"><span data-stu-id="64aea-149">Image management</span></span> 

<span data-ttu-id="64aea-150">Ниже приведены некоторые примеры типичных задач управления изображения и как toocomplete их с помощью hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="64aea-150">Here are some examples of common image management tasks and how toocomplete them using hello Azure CLI.</span></span>

<span data-ttu-id="64aea-151">Получение списка всех образов по имени в формате таблицы.</span><span class="sxs-lookup"><span data-stu-id="64aea-151">List all images by name in a table format.</span></span>

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

<span data-ttu-id="64aea-152">Удаление образа.</span><span class="sxs-lookup"><span data-stu-id="64aea-152">Delete an image.</span></span> <span data-ttu-id="64aea-153">Этот пример удаляет hello изображение с именем *myOldImage* из hello *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="64aea-153">This example deletes hello image named *myOldImage* from hello *myResourceGroup*.</span></span>

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="64aea-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="64aea-154">Next steps</span></span>

<span data-ttu-id="64aea-155">В рамках этого руководства вы создали пользовательский образ виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="64aea-155">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="64aea-156">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="64aea-156">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="64aea-157">отменять подготовку виртуальных машин и подготавливать их к использованию;</span><span class="sxs-lookup"><span data-stu-id="64aea-157">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="64aea-158">создавать пользовательский образ;</span><span class="sxs-lookup"><span data-stu-id="64aea-158">Create a custom image</span></span>
> * <span data-ttu-id="64aea-159">Создание виртуальной машины из пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="64aea-159">Create a VM from a custom image</span></span>
> * <span data-ttu-id="64aea-160">Отображение списка всех образов hello в подписке</span><span class="sxs-lookup"><span data-stu-id="64aea-160">List all hello images in your subscription</span></span>
> * <span data-ttu-id="64aea-161">удалять образ.</span><span class="sxs-lookup"><span data-stu-id="64aea-161">Delete an image</span></span>

<span data-ttu-id="64aea-162">Переместить следующий учебник toolearn toohello о виртуальных машин высокой надежности.</span><span class="sxs-lookup"><span data-stu-id="64aea-162">Advance toohello next tutorial toolearn about highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="64aea-163">[Создание высокодоступных виртуальных машин](tutorial-availability-sets.md)</span><span class="sxs-lookup"><span data-stu-id="64aea-163">[Create highly available VMs](tutorial-availability-sets.md).</span></span>

