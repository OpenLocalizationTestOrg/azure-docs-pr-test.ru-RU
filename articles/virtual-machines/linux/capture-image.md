---
title: "образ виртуальной Машины Linux в Azure с помощью CLI 2.0 aaaCapture | Документы Microsoft"
description: "Запись образа виртуальной Машины Azure toouse массы развертываний с помощью Azure CLI 2.0 hello."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: 9558332a86186b282775097428df462709373012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-image-of-a-virtual-machine-or-vhd"></a><span data-ttu-id="be07a-103">Как toocreate образ виртуальной машины или виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="be07a-103">How toocreate an image of a virtual machine or VHD</span></span>

<!-- generalize, image - extended version of hello tutorial-->

<span data-ttu-id="be07a-104">toocreate несколько копий виртуальной машины (VM) toouse в Azure, запись образа виртуальной Машины hello или hello виртуального жесткого диска операционной системы.</span><span class="sxs-lookup"><span data-stu-id="be07a-104">toocreate multiple copies of a virtual machine (VM) toouse in Azure, capture an image of hello VM or hello OS VHD.</span></span> <span data-ttu-id="be07a-105">toocreate изображения, необходимо удалить сведения личную учетную запись, что делает более безопасным toodeploy несколько раз.</span><span class="sxs-lookup"><span data-stu-id="be07a-105">toocreate an image, you need remove personal account information which makes it safer toodeploy multiple times.</span></span> <span data-ttu-id="be07a-106">В следующие шаги hello отзыв существующей виртуальной Машины, deallocate и создания образа.</span><span class="sxs-lookup"><span data-stu-id="be07a-106">In hello following steps you deprovision an existing VM, deallocate and create an image.</span></span> <span data-ttu-id="be07a-107">Можно использовать этот образ toocreate виртуальных машин, в любую группу ресурсов в подписке.</span><span class="sxs-lookup"><span data-stu-id="be07a-107">You can use this image toocreate VMs across any resource group within your subscription.</span></span>

<span data-ttu-id="be07a-108">Если требуется toocreate копию существующей ВМ Linux для резервного копирования или отладки, или отправить специализированные Linux VHD из локальной виртуальной Машины, см. раздел [отправить и создавать из пользовательского образа виртуальной Машины Linux](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="be07a-108">If you want toocreate a copy of your existing Linux VM for backup or debugging, or upload a specialized Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md).</span></span>  

<span data-ttu-id="be07a-109">Можно также использовать **Packer** toocreate вашей пользовательской конфигурации.</span><span class="sxs-lookup"><span data-stu-id="be07a-109">You can also use **Packer** toocreate your custom configuration.</span></span> <span data-ttu-id="be07a-110">Дополнительные сведения об использовании Packer см. в разделе [как виртуальная машина Linux toocreate toouse Packer образы в Azure](build-image-with-packer.md).</span><span class="sxs-lookup"><span data-stu-id="be07a-110">For more information on using Packer, see [How toouse Packer toocreate Linux virtual machine images in Azure](build-image-with-packer.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="be07a-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="be07a-111">Before you begin</span></span>
<span data-ttu-id="be07a-112">Убедитесь, что выполнены следующие предварительные требования hello:</span><span class="sxs-lookup"><span data-stu-id="be07a-112">Ensure that you meet hello following prerequisites:</span></span>

* <span data-ttu-id="be07a-113">Необходимо создать в модели развертывания диспетчера ресурсов hello, с помощью управляемых дисков виртуальной Машины Azure.</span><span class="sxs-lookup"><span data-stu-id="be07a-113">You need an Azure VM created in hello Resource Manager deployment model using managed disks.</span></span> <span data-ttu-id="be07a-114">Если вы еще не создали ВМ Linux, можно использовать hello [портала](quick-create-portal.md), hello [Azure CLI](quick-create-cli.md), или [шаблоны диспетчера ресурсов](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="be07a-114">If you haven't created a Linux VM, you can use hello [portal](quick-create-portal.md), hello [Azure CLI](quick-create-cli.md), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> <span data-ttu-id="be07a-115">Настройка виртуальной Машины, при необходимости hello.</span><span class="sxs-lookup"><span data-stu-id="be07a-115">Configure hello VM as needed.</span></span> <span data-ttu-id="be07a-116">Например, [добавьте диски данных](add-disk.md), примените обновления и установите приложения.</span><span class="sxs-lookup"><span data-stu-id="be07a-116">For example, [add data disks](add-disk.md), apply updates, and install applications.</span></span> 

* <span data-ttu-id="be07a-117">Необходимо также toohave hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) установки и входят в систему по учетной записи Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="be07a-117">You also need toohave hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and be logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="be07a-118">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="be07a-118">Quick commands</span></span>

<span data-ttu-id="be07a-119">Упрощенную версию этого раздела, для тестирования, оценки или сведения о виртуальных машинах в Azure, см. [создать образ виртуальной машины Azure с помощью hello CLI](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="be07a-119">For a simplified version of this topic, for testing, evaluating or learning about VMs in Azure, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md).</span></span>


## <a name="step-1-deprovision-hello-vm"></a><span data-ttu-id="be07a-120">Шаг 1: Отзыв виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="be07a-120">Step 1: Deprovision hello VM</span></span>
<span data-ttu-id="be07a-121">В случае отмены провизионирования hello виртуальной Машины, используя агент ВМ Azure hello, toodelete машины определенные файлы и данные.</span><span class="sxs-lookup"><span data-stu-id="be07a-121">You deprovision hello VM, using hello Azure VM agent, toodelete machine specific files and data.</span></span> <span data-ttu-id="be07a-122">Используйте hello `waagent` с hello *-deprovision + пользователь* параметра в вашей исходной виртуальной Машины Linux.</span><span class="sxs-lookup"><span data-stu-id="be07a-122">Use hello `waagent` command with hello *-deprovision+user* parameter on your source Linux VM.</span></span> <span data-ttu-id="be07a-123">Дополнительные сведения см. в разделе hello [руководство пользователя Azure Linux Agent](../windows/agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="be07a-123">For more information, see hello [Azure Linux Agent user guide](../windows/agent-user-guide.md).</span></span>

1. <span data-ttu-id="be07a-124">Подключите tooyour виртуальных Машин Linux с помощью SSH-клиента.</span><span class="sxs-lookup"><span data-stu-id="be07a-124">Connect tooyour Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="be07a-125">В окне приветствия SSH введите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="be07a-125">In hello SSH window, type hello following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > <span data-ttu-id="be07a-126">Только выполните команду на виртуальной Машине, следует присвоить toocapture как изображение.</span><span class="sxs-lookup"><span data-stu-id="be07a-126">Only run this command on a VM that you intend toocapture as an image.</span></span> <span data-ttu-id="be07a-127">Он не гарантирует этот образ hello подходит для распространения или удаляется все конфиденциальные данные.</span><span class="sxs-lookup"><span data-stu-id="be07a-127">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution.</span></span> <span data-ttu-id="be07a-128">Hello *+ пользователь* параметра также приведет к удалению hello последняя подготовленного пользователя учетной записи.</span><span class="sxs-lookup"><span data-stu-id="be07a-128">hello *+user* parameter also removes hello last provisioned user account.</span></span> <span data-ttu-id="be07a-129">Учетные данные учетной записи tookeep в hello виртуальных Машин, просто используйте *-deprovision* tooleave hello учетной записи пользователя на месте.</span><span class="sxs-lookup"><span data-stu-id="be07a-129">If you want tookeep account credentials in hello VM, just use *-deprovision* tooleave hello user account in place.</span></span>
 
3. <span data-ttu-id="be07a-130">Тип **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="be07a-130">Type **y** toocontinue.</span></span> <span data-ttu-id="be07a-131">Можно добавить hello **-принудительно** tooavoid параметр этого шага подтверждения.</span><span class="sxs-lookup"><span data-stu-id="be07a-131">You can add hello **-force** parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="be07a-132">После выполнения команды hello введите **выхода**.</span><span class="sxs-lookup"><span data-stu-id="be07a-132">After hello command completes, type **exit**.</span></span> <span data-ttu-id="be07a-133">Этот шаг закрывает клиент SSH hello.</span><span class="sxs-lookup"><span data-stu-id="be07a-133">This step closes hello SSH client.</span></span>

## <a name="step-2-create-vm-image"></a><span data-ttu-id="be07a-134">Шаг 2. Создайте образ виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="be07a-134">Step 2: Create VM image</span></span>
<span data-ttu-id="be07a-135">Служит обобщенный hello toomark hello Azure CLI 2.0 ВМ и образа hello.</span><span class="sxs-lookup"><span data-stu-id="be07a-135">Use hello Azure CLI 2.0 toomark hello VM as generalized and capture hello image.</span></span> <span data-ttu-id="be07a-136">В hello следующих примерах замените примеры имен параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="be07a-136">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="be07a-137">Примеры имен параметров: *myResourceGroup*, *myVnet* и *myVM*.</span><span class="sxs-lookup"><span data-stu-id="be07a-137">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

1. <span data-ttu-id="be07a-138">DEALLOCATE hello виртуальной Машине, которая удалена с [ВМ az deallocate](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="be07a-138">Deallocate hello VM that you deprovisioned with [az vm deallocate](/cli//azure/vm#deallocate).</span></span> <span data-ttu-id="be07a-139">Hello следующий пример отменяет выделение hello виртуальной Машины с именем *myVM* в группе ресурсов hello с именем *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="be07a-139">hello following example deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. <span data-ttu-id="be07a-140">Пометить hello виртуальной Машины как универсализации с [ВМ az generalize](/cli//azure/vm#generalize).</span><span class="sxs-lookup"><span data-stu-id="be07a-140">Mark hello VM as generalized with [az vm generalize](/cli//azure/vm#generalize).</span></span> <span data-ttu-id="be07a-141">Следующий пример метки hello hello виртуальной Машины с именем Hello *myVM* в группе ресурсов hello с именем *myResourceGroup* как обобщенный:</span><span class="sxs-lookup"><span data-stu-id="be07a-141">hello following example marks hello hello VM named *myVM* in hello resource group named *myResourceGroup* as generalized:</span></span>
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. <span data-ttu-id="be07a-142">Теперь создайте образ hello ресурса виртуальной Машины с [создать образ az](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="be07a-142">Now create an image of hello VM resource with [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="be07a-143">Hello следующий пример создает образ с именем *myImage* в группе ресурсов hello с именем *myResourceGroup* с помощью hello ВМ ресурс с именем *myVM*:</span><span class="sxs-lookup"><span data-stu-id="be07a-143">hello following example creates an image named *myImage* in hello resource group named *myResourceGroup* using hello VM resource named *myVM*:</span></span>
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > <span data-ttu-id="be07a-144">Hello образу в hello же группе ресурсов, что к исходной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="be07a-144">hello image is created in hello same resource group as your source VM.</span></span> <span data-ttu-id="be07a-145">Виртуальную машину из этого образа можно создать в любой группе ресурсов в рамках вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="be07a-145">You can create VMs in any resource group within your subscription from this image.</span></span> <span data-ttu-id="be07a-146">С точки зрения управления вы можете toocreate определенной группы ресурсов для виртуальной Машины ресурсов и изображений.</span><span class="sxs-lookup"><span data-stu-id="be07a-146">From a management perspective, you may wish toocreate a specific resource group for your VM resources and images.</span></span>

## <a name="step-3-create-a-vm-from-hello-captured-image"></a><span data-ttu-id="be07a-147">Шаг 3: Создание виртуальной Машины из образа захвачен hello</span><span class="sxs-lookup"><span data-stu-id="be07a-147">Step 3: Create a VM from hello captured image</span></span>
<span data-ttu-id="be07a-148">Создайте виртуальную Машину с помощью образа hello, созданные с помощью [создания виртуальной машины az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="be07a-148">Create a VM using hello image you created with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="be07a-149">Hello следующий пример создает Виртуальную машину с именем *myVMDeployed* из образа hello с именем *myImage*:</span><span class="sxs-lookup"><span data-stu-id="be07a-149">hello following example creates a VM named *myVMDeployed* from hello image named *myImage*:</span></span>

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-hello-vm-in-another-resource-group"></a><span data-ttu-id="be07a-150">Создание виртуальной Машины hello в другой группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="be07a-150">Creating hello VM in another resource group</span></span> 

<span data-ttu-id="be07a-151">Вы можете создавать виртуальные машины из образа в любой группе ресурсов в рамках своей подписки.</span><span class="sxs-lookup"><span data-stu-id="be07a-151">You can create VMs from an image in any resource group within your subscription.</span></span> <span data-ttu-id="be07a-152">toocreate виртуальной Машины в другой группе ресурсов чем изображение hello укажите hello полный идентификатор tooyour изображение ресурса.</span><span class="sxs-lookup"><span data-stu-id="be07a-152">toocreate a VM in a different resource group than hello image, specify hello full resource ID tooyour image.</span></span> <span data-ttu-id="be07a-153">Используйте [списка изображений az](/cli/azure/image#list) tooview список образов.</span><span class="sxs-lookup"><span data-stu-id="be07a-153">Use [az image list](/cli/azure/image#list) tooview a list of images.</span></span> <span data-ttu-id="be07a-154">Hello вывода будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="be07a-154">hello output is similar toohello following example:</span></span>

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

<span data-ttu-id="be07a-155">Hello следующий пример использует [создания виртуальной машины az](/cli/azure/vm#create) toocreate виртуальной Машины в группе ресурсов, отличной от исходного образа hello, указав идентификатор ресурса изображения hello:</span><span class="sxs-lookup"><span data-stu-id="be07a-155">hello following example uses [az vm create](/cli/azure/vm#create) toocreate a VM in a different resource group than hello source image by specifying hello image resource ID:</span></span>

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-hello-deployment"></a><span data-ttu-id="be07a-156">Шаг 4: Проверка развертывания hello</span><span class="sxs-lookup"><span data-stu-id="be07a-156">Step 4: Verify hello deployment</span></span>

<span data-ttu-id="be07a-157">Теперь SSH toohello виртуальной машины вы создали tooverify hello развертывания и запуска с помощью hello новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="be07a-157">Now SSH toohello virtual machine you created tooverify hello deployment and start using hello new VM.</span></span> <span data-ttu-id="be07a-158">tooconnect через SSH, найти hello IP-адрес или полное доменное имя вашей виртуальной машины с [Показать ВМ az](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="be07a-158">tooconnect via SSH, find hello IP address or FQDN of your VM with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a><span data-ttu-id="be07a-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="be07a-159">Next steps</span></span>
<span data-ttu-id="be07a-160">Вы можете создать несколько виртуальных машин из исходного образа виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="be07a-160">You can create multiple VMs from your source VM image.</span></span> <span data-ttu-id="be07a-161">Если требуется, чтобы изображение tooyour toomake изменения:</span><span class="sxs-lookup"><span data-stu-id="be07a-161">If you need toomake changes tooyour image:</span></span> 

- <span data-ttu-id="be07a-162">Создайте виртуальную машину из образа.</span><span class="sxs-lookup"><span data-stu-id="be07a-162">Create a VM from your image.</span></span>
- <span data-ttu-id="be07a-163">Выполните желаемые обновления или изменения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="be07a-163">Make any updates or configuration changes.</span></span>
- <span data-ttu-id="be07a-164">Выполните hello снова toodeprovision, deallocate, обобщения, а также создания образа.</span><span class="sxs-lookup"><span data-stu-id="be07a-164">Follow hello steps again toodeprovision, deallocate, generalize, and create an image.</span></span>
- <span data-ttu-id="be07a-165">Используйте этот новый образ для будущих развертываний.</span><span class="sxs-lookup"><span data-stu-id="be07a-165">Use this new image for future deployments.</span></span> <span data-ttu-id="be07a-166">При необходимости удалите hello исходного изображения.</span><span class="sxs-lookup"><span data-stu-id="be07a-166">If desired, delete hello original image.</span></span>

<span data-ttu-id="be07a-167">Дополнительные сведения об управлении виртуальных машин с hello CLI см. в разделе [Azure CLI 2.0](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="be07a-167">For more information on managing your VMs with hello CLI, see [Azure CLI 2.0](/cli/azure/overview).</span></span>
