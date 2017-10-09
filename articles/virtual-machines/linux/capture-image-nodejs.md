---
title: "aaaCapture toouse виртуальной Машине Linux Azure как шаблон | Документы Microsoft"
description: "Узнайте, как toocapture и обобщить образ на основе Linux Azure созданная виртуальная машина (ВМ) с моделью развертывания диспетчера ресурсов Azure hello."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 877eee5c842bebe80e755c2240cdaaef4ade6ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a><span data-ttu-id="902fc-103">Запись виртуальной машины Linux, работающей в Azure</span><span class="sxs-lookup"><span data-stu-id="902fc-103">Capture a Linux virtual machine running on Azure</span></span>
<span data-ttu-id="902fc-104">Выполните действия hello в этой статье toogeneralize и сохранения виртуальной машине Azure Linux (ВМ) в модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="902fc-104">Follow hello steps in this article toogeneralize and capture your Azure Linux virtual machine (VM) in hello Resource Manager deployment model.</span></span> <span data-ttu-id="902fc-105">При создании hello виртуальной Машины вы удалите личных учетных записей и подготовка toobe hello виртуальной Машины, используемое в качестве изображения.</span><span class="sxs-lookup"><span data-stu-id="902fc-105">When you generalize hello VM, you remove personal account information and prepare hello VM toobe used as an image.</span></span> <span data-ttu-id="902fc-106">Вы затем обобщенный виртуальный жесткий диск (VHD) из образа для hello ОС, виртуальные жесткие диски для подключенные диски данных, отслеживания и [шаблона диспетчера ресурсов](../../azure-resource-manager/resource-group-overview.md) для нового развертывания виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="902fc-106">You then capture a generalized virtual hard disk (VHD) image for hello OS, VHDs for attached data disks, and a [Resource Manager template](../../azure-resource-manager/resource-group-overview.md) for new VM deployments.</span></span> <span data-ttu-id="902fc-107">В этой статье указаны как образ toocapture виртуальной Машины с hello Azure CLI 1.0 для виртуальной Машины с помощью неуправляемых дисков.</span><span class="sxs-lookup"><span data-stu-id="902fc-107">This article details how toocapture a VM image with hello Azure CLI 1.0 for a VM using unmanaged disks.</span></span> <span data-ttu-id="902fc-108">Вы также можете [захватить ВМ с помощью управляемых дисков Azure с hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="902fc-108">You can also [capture a VM using Azure Managed Disks with hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="902fc-109">Управляемый диски обрабатываются hello платформы Azure и не требуют toostore любые предварительные и расположение их.</span><span class="sxs-lookup"><span data-stu-id="902fc-109">Managed disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="902fc-110">Дополнительные сведения об Управляемых дисках Azure см. в [этой статье](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="902fc-110">For more information, see [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="902fc-111">toocreate виртуальные машины с помощью образа hello настроить сетевые ресурсы для каждой новой виртуальной Машины и использовать toodeploy hello шаблон (файл JavaScript, или JSON,), его из hello записанных образов виртуальных жестких ДИСКОВ.</span><span class="sxs-lookup"><span data-stu-id="902fc-111">toocreate VMs using hello image, set up network resources for each new VM, and use hello template (a JavaScript Object Notation, or JSON, file) toodeploy it from hello captured VHD images.</span></span> <span data-ttu-id="902fc-112">Таким образом можно реплицировать виртуальную Машину с текущей конфигурации программного обеспечения, так же как toohello использование изображений в hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="902fc-112">In this way, you can replicate a VM with its current software configuration, similar toohello way you use images in hello Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="902fc-113">Если toocreate копию существующей ВМ Linux с ее состоянием специализированные для резервного копирования или отладки, см. [создать копию виртуальной машины Linux в Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="902fc-113">If you want toocreate a copy of your existing Linux VM with its specialized state for backup or debugging, see [Create a copy of a Linux virtual machine running on Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="902fc-114">И если tooupload VHD из локальной виртуальной Машины Linux, см. [передача и создание виртуальной Машины Linux из пользовательского образа](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="902fc-114">And if you want tooupload a Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>  

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="902fc-115">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="902fc-115">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="902fc-116">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="902fc-116">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="902fc-117">[Azure CLI 1.0](#before-you-begin) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="902fc-117">[Azure CLI 1.0](#before-you-begin) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="902fc-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="902fc-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="902fc-119">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="902fc-119">Before you begin</span></span>
<span data-ttu-id="902fc-120">Убедитесь, что выполнены следующие предварительные требования hello:</span><span class="sxs-lookup"><span data-stu-id="902fc-120">Ensure that you meet hello following prerequisites:</span></span>

* <span data-ttu-id="902fc-121">**Виртуальная машина Azure создаются в модели развертывания диспетчера ресурсов hello** -Если вы еще не создали ВМ Linux, можно использовать hello [портала](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), или [диспетчера ресурсов шаблоны](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="902fc-121">**Azure VM created in hello Resource Manager deployment model** - If you haven't created a Linux VM, you can use hello [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> 
  
    <span data-ttu-id="902fc-122">Настройка виртуальной Машины, при необходимости hello.</span><span class="sxs-lookup"><span data-stu-id="902fc-122">Configure hello VM as needed.</span></span> <span data-ttu-id="902fc-123">Например, [добавьте диски данных](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), примените обновления и установите приложения.</span><span class="sxs-lookup"><span data-stu-id="902fc-123">For example, [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), apply updates, and install applications.</span></span> 
* <span data-ttu-id="902fc-124">**Azure CLI** -Install hello [Azure CLI](../../cli-install-nodejs.md) на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="902fc-124">**Azure CLI** - Install hello [Azure CLI](../../cli-install-nodejs.md) on a local computer.</span></span>

## <a name="step-1-remove-hello-azure-linux-agent"></a><span data-ttu-id="902fc-125">Шаг 1: Удаление агента Azure Linux hello</span><span class="sxs-lookup"><span data-stu-id="902fc-125">Step 1: Remove hello Azure Linux agent</span></span>
<span data-ttu-id="902fc-126">Сначала запустите hello **waagent** с hello **отзыва** параметров на виртуальной Машине Linux hello.</span><span class="sxs-lookup"><span data-stu-id="902fc-126">First, run hello **waagent** command with hello **deprovision** parameter on hello Linux VM.</span></span> <span data-ttu-id="902fc-127">Эта команда удаляет файлы и данные toomake hello виртуальная машина готова для обобщения.</span><span class="sxs-lookup"><span data-stu-id="902fc-127">This command deletes files and data toomake hello VM ready for generalizing.</span></span> <span data-ttu-id="902fc-128">Дополнительные сведения см. в разделе hello [руководство пользователя Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="902fc-128">For details, see hello [Azure Linux Agent user guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

1. <span data-ttu-id="902fc-129">Подключите tooyour виртуальных Машин Linux с помощью SSH-клиента.</span><span class="sxs-lookup"><span data-stu-id="902fc-129">Connect tooyour Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="902fc-130">В окне приветствия SSH введите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="902fc-130">In hello SSH window, type hello following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > <span data-ttu-id="902fc-131">Только выполните команду на виртуальной Машине, следует присвоить toocapture как изображение.</span><span class="sxs-lookup"><span data-stu-id="902fc-131">Only run this command on a VM that you intend toocapture as an image.</span></span> <span data-ttu-id="902fc-132">Он не гарантирует этот образ hello подходит для распространения или удаляется все конфиденциальные данные.</span><span class="sxs-lookup"><span data-stu-id="902fc-132">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution.</span></span>
 
3. <span data-ttu-id="902fc-133">Тип **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="902fc-133">Type **y** toocontinue.</span></span> <span data-ttu-id="902fc-134">Можно добавить hello **-принудительно** tooavoid параметр этого шага подтверждения.</span><span class="sxs-lookup"><span data-stu-id="902fc-134">You can add hello **-force** parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="902fc-135">После выполнения команды hello введите **выхода**.</span><span class="sxs-lookup"><span data-stu-id="902fc-135">After hello command completes, type **exit**.</span></span> <span data-ttu-id="902fc-136">Этот шаг закрывает клиент SSH hello.</span><span class="sxs-lookup"><span data-stu-id="902fc-136">This step closes hello SSH client.</span></span>

## <a name="step-2-capture-hello-vm"></a><span data-ttu-id="902fc-137">Шаг 2: Запись hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="902fc-137">Step 2: Capture hello VM</span></span>
<span data-ttu-id="902fc-138">Используйте toogeneralize hello Azure CLI и записать hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="902fc-138">Use hello Azure CLI toogeneralize and capture hello VM.</span></span> <span data-ttu-id="902fc-139">В hello следующих примерах замените примеры имен параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="902fc-139">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="902fc-140">Примеры имен параметров: **myResourceGroup**, **myVnet** и **myVM**.</span><span class="sxs-lookup"><span data-stu-id="902fc-140">Example parameter names include **myResourceGroup**, **myVnet**, and **myVM**.</span></span>

1. <span data-ttu-id="902fc-141">С локального компьютера, откройте hello Azure CLI и [tooyour входа подписки Azure](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="902fc-141">From your local computer, open hello Azure CLI and [login tooyour Azure subscription](../../xplat-cli-connect.md).</span></span> 
2. <span data-ttu-id="902fc-142">Убедитесь, что режим Resource Manager включен.</span><span class="sxs-lookup"><span data-stu-id="902fc-142">Make sure you are in Resource Manager mode.</span></span>
   
    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="902fc-143">Завершение работы hello виртуальной Машине, которая уже удалена с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="902fc-143">Shut down hello VM that you already deprovisioned by using hello following command:</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. <span data-ttu-id="902fc-144">Обобщить hello виртуальной Машины с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="902fc-144">Generalize hello VM with hello following command:</span></span>
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. <span data-ttu-id="902fc-145">Теперь запустите hello **записи виртуальной машины azure** команды, который получает hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="902fc-145">Now run hello **azure vm capture** command, which captures hello VM.</span></span> <span data-ttu-id="902fc-146">В следующем примере hello, hello образ VHD записанный с помощью имен, начиная с **MyVHDNamePrefix**и hello **-t** указывает путь шаблона toohello **MyTemplate.json**.</span><span class="sxs-lookup"><span data-stu-id="902fc-146">In hello following example, hello image VHDs are captured with names beginning with **MyVHDNamePrefix**, and hello **-t** option specifies a path toohello template **MyTemplate.json**.</span></span> 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > <span data-ttu-id="902fc-147">Hello образ VHD-файлов создаются по умолчанию в приветствия использовать одну учетную запись хранилища, hello исходной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="902fc-147">hello image VHD files get created by default in hello same storage account that hello original VM used.</span></span> <span data-ttu-id="902fc-148">Используйте hello *учетную запись хранения* toostore hello виртуальных жестких дисков для создания из образа hello новые виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="902fc-148">Use hello *same storage account* toostore hello VHDs for any new VMs you create from hello image.</span></span> 

6. <span data-ttu-id="902fc-149">расположение hello toofind записанный образ шаблона JSON Привет открыть в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="902fc-149">toofind hello location of a captured image, open hello JSON template in a text editor.</span></span> <span data-ttu-id="902fc-150">В hello **storageProfile**, найти hello **uri** из hello **изображения** в hello **системы** контейнера.</span><span class="sxs-lookup"><span data-stu-id="902fc-150">In hello **storageProfile**, find hello **uri** of hello **image** located in hello **system** container.</span></span> <span data-ttu-id="902fc-151">Например hello URI образа диска ОС hello аналогичен слишком`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="902fc-151">For example, hello URI of hello OS disk image is similar too`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>

## <a name="step-3-create-a-vm-from-hello-captured-image"></a><span data-ttu-id="902fc-152">Шаг 3: Создание виртуальной Машины из образа захвачен hello</span><span class="sxs-lookup"><span data-stu-id="902fc-152">Step 3: Create a VM from hello captured image</span></span>
<span data-ttu-id="902fc-153">Теперь можно используйте образ hello с toocreate шаблона виртуальной Машины Linux.</span><span class="sxs-lookup"><span data-stu-id="902fc-153">Now use hello image with a template toocreate a Linux VM.</span></span> <span data-ttu-id="902fc-154">Эти шаги показано, как toouse hello Azure CLI и hello шаблона файла JSON, вы записали hello toocreate виртуальной Машины в новой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="902fc-154">These steps show you how toouse hello Azure CLI and hello JSON file template you captured toocreate hello VM in a new virtual network.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="902fc-155">Создание сетевых ресурсов</span><span class="sxs-lookup"><span data-stu-id="902fc-155">Create network resources</span></span>
<span data-ttu-id="902fc-156">шаблон toouse hello, необходимо сначала tooset виртуальной сети и сетевой Адаптер для новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="902fc-156">toouse hello template, you first need tooset up a virtual network and NIC for your new VM.</span></span> <span data-ttu-id="902fc-157">Рекомендуется создать группу ресурсов для этих ресурсов hello там, где хранится образ виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="902fc-157">We recommend you create a resource group for these resources in hello location where your VM image is stored.</span></span> <span data-ttu-id="902fc-158">Выполните команды toohello примерно следующие, указав имена ресурсов и расположение соответствующих Azure («centralus» в этих командах):</span><span class="sxs-lookup"><span data-stu-id="902fc-158">Run commands similar toohello following, substituting names for your resources and an appropriate Azure location ("centralus" in these commands):</span></span>

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-hello-id-of-hello-nic"></a><span data-ttu-id="902fc-159">Получить идентификатор hello Сетевых hello</span><span class="sxs-lookup"><span data-stu-id="902fc-159">Get hello Id of hello NIC</span></span>
<span data-ttu-id="902fc-160">toodeploy виртуальной Машины из образа hello с помощью hello JSON, сохраненный во время записи, необходимо hello идентификатор hello сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="902fc-160">toodeploy a VM from hello image by using hello JSON you saved during capture, you need hello Id of hello NIC.</span></span> <span data-ttu-id="902fc-161">Получите его, запустив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="902fc-161">Obtain it by running hello following command:</span></span>

```azurecli
azure network nic show myResourceGroup1 myNIC
```

<span data-ttu-id="902fc-162">Hello **идентификатор** в hello вывод команды будет примерно слишком`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span><span class="sxs-lookup"><span data-stu-id="902fc-162">hello **Id** in hello output is similar too`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="902fc-163">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="902fc-163">Create a VM</span></span>
<span data-ttu-id="902fc-164">После выполнения hello следующая команда toocreate ВМ из hello запись образа виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="902fc-164">Now run hello following command toocreate your VM from hello captured VM image.</span></span> <span data-ttu-id="902fc-165">Используйте hello **-f** toohello путь шаблон JSON для параметра toospecify hello файл был сохранен.</span><span class="sxs-lookup"><span data-stu-id="902fc-165">Use hello **-f** parameter toospecify hello path toohello template JSON file you saved.</span></span>

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

<span data-ttu-id="902fc-166">В выходных данных команды hello вы запрашиваемые toosupply новое имя виртуальной Машины, имя пользователя администратора hello и пароль и hello идентификатор hello сетевого Адаптера, созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="902fc-166">In hello command output, you are prompted toosupply a new VM name, hello admin user name and password, and hello Id of hello NIC you created previously.</span></span>

```bash
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

<span data-ttu-id="902fc-167">Следующий образец Hello показывает, отображаемые для успешного развертывания:</span><span class="sxs-lookup"><span data-stu-id="902fc-167">hello following sample shows what you see for a successful deployment:</span></span>

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment toocomplete
data:    DeploymentName     : MyDeployment
data:    ResourceGroupName  : MyResourceGroup1
data:    ProvisioningState  : Succeeded
data:    Timestamp          : xxxxxxx
data:    Mode               : Incremental
data:    Name                Type          Value

data:    ------------------  ------------  -------------------------------------

data:    vmName              String        myNewVM

data:    vmSize              String        Standard_D1

data:    adminUserName       String        myAdminuser

data:    adminPassword       SecureString  undefined

data:    networkInterfaceId  String        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
info:    group deployment create command OK
```

### <a name="verify-hello-deployment"></a><span data-ttu-id="902fc-168">Проверка развертывания hello</span><span class="sxs-lookup"><span data-stu-id="902fc-168">Verify hello deployment</span></span>
<span data-ttu-id="902fc-169">Теперь SSH toohello виртуальной машины вы создали tooverify hello развертывания и запуска с помощью hello новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="902fc-169">Now SSH toohello virtual machine you created tooverify hello deployment and start using hello new VM.</span></span> <span data-ttu-id="902fc-170">tooconnect через SSH, поиска IP-адреса hello hello виртуальной Машины, созданные с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="902fc-170">tooconnect via SSH, find hello IP address of hello VM you created by running hello following command:</span></span>

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

<span data-ttu-id="902fc-171">Hello общедоступный IP-адрес отображается в выходных данных команды hello.</span><span class="sxs-lookup"><span data-stu-id="902fc-171">hello public IP address is listed in hello command output.</span></span> <span data-ttu-id="902fc-172">По умолчанию соединение toohello виртуальных Машин Linux по протоколу SSH на порт 22.</span><span class="sxs-lookup"><span data-stu-id="902fc-172">By default you connect toohello Linux VM by SSH on port 22.</span></span>

## <a name="create-additional-vms"></a><span data-ttu-id="902fc-173">Создание дополнительных виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="902fc-173">Create additional VMs</span></span>
<span data-ttu-id="902fc-174">Используйте hello захвата образа и шаблон toodeploy дополнительных ВМ с помощью действия hello в предшествующих раздел hello.</span><span class="sxs-lookup"><span data-stu-id="902fc-174">Use hello captured image and template toodeploy additional VMs using hello steps in hello preceding section.</span></span> <span data-ttu-id="902fc-175">Другие параметры toocreate виртуальные машины, из образа hello включать с помощью шаблона примеры использования или запуска hello **создания виртуальной машины azure** команды.</span><span class="sxs-lookup"><span data-stu-id="902fc-175">Other options toocreate VMs from hello image include using a quickstart template or running hello **azure vm create** command.</span></span>

### <a name="use-hello-captured-template"></a><span data-ttu-id="902fc-176">Используйте шаблон записанного hello</span><span class="sxs-lookup"><span data-stu-id="902fc-176">Use hello captured template</span></span>
<span data-ttu-id="902fc-177">toouse hello захвата образа и шаблона, выполните следующие действия, (подробные hello предшествующий раздел):</span><span class="sxs-lookup"><span data-stu-id="902fc-177">toouse hello captured image and template, follow these steps (detailed in hello preceding section):</span></span>

* <span data-ttu-id="902fc-178">Убедитесь, что образ виртуальной Машины в hello учетную запись хранения, на котором размещается виртуальный жесткий ДИСК Виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="902fc-178">Ensure that your VM image is in hello same storage account that hosts your VM's VHD.</span></span>
* <span data-ttu-id="902fc-179">Скопируйте файл JSON hello шаблон и укажите уникальное имя для диска ОС hello hello новой Виртуальной машины виртуальный жесткий ДИСК (или виртуальные жесткие диски).</span><span class="sxs-lookup"><span data-stu-id="902fc-179">Copy hello template JSON file and specify a unique name for hello OS disk of hello new VM's VHD (or VHDs).</span></span> <span data-ttu-id="902fc-180">Например, в hello **storageProfile**в разделе **виртуального жесткого диска**в **uri**, укажите уникальное имя для hello **osDisk** виртуального жесткого диска, аналогичные слишком`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="902fc-180">For example, in hello **storageProfile**, under **vhd**, in **uri**, specify a unique name for hello **osDisk** VHD, similar too`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>
* <span data-ttu-id="902fc-181">Создайте сетевую КАРТУ в любом hello того же или другой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="902fc-181">Create a NIC in either hello same or a different virtual network.</span></span>
* <span data-ttu-id="902fc-182">С помощью JSON-файл шаблона изменен hello, создайте развертывание в группе ресурсов hello, в котором можно настроить виртуальную сеть hello.</span><span class="sxs-lookup"><span data-stu-id="902fc-182">Using hello modified template JSON file, create a deployment in hello resource group in which you set up hello virtual network.</span></span>

### <a name="use-a-quickstart-template"></a><span data-ttu-id="902fc-183">Использование шаблона быстрого запуска</span><span class="sxs-lookup"><span data-stu-id="902fc-183">Use a quickstart template</span></span>
<span data-ttu-id="902fc-184">Если вы хотите настроить автоматически при создании виртуальной Машины из образа hello сети hello, можно указать эти ресурсы в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="902fc-184">If you want hello network set up automatically when you create a VM from hello image, you can specify those resources in a template.</span></span> <span data-ttu-id="902fc-185">Например, в разделе hello [101 виртуальных машин из пользовательского образа шаблона](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) из GitHub.</span><span class="sxs-lookup"><span data-stu-id="902fc-185">For example, see hello [101-vm-from-user-image template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) from GitHub.</span></span> <span data-ttu-id="902fc-186">Этот шаблон создает виртуальную Машину из пользовательского образа и hello необходимости виртуальной сети, общедоступный IP-адрес и Сетевых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="902fc-186">This template creates a VM from your custom image and hello necessary virtual network, public IP address, and NIC resources.</span></span> <span data-ttu-id="902fc-187">Пошаговое руководство по с помощью шаблона hello в hello портал Azure, в разделе [как toocreate виртуальной машины из образа с помощью шаблона диспетчера ресурсов](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span><span class="sxs-lookup"><span data-stu-id="902fc-187">For a walkthrough of using hello template in hello Azure portal, see [How toocreate a virtual machine from a custom image using a Resource Manager template](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span></span>

### <a name="use-hello-azure-vm-create-command"></a><span data-ttu-id="902fc-188">Создание виртуальной машины hello azure используйте команды</span><span class="sxs-lookup"><span data-stu-id="902fc-188">Use hello azure vm create command</span></span>
<span data-ttu-id="902fc-189">Обычно это самый простой toouse toocreate шаблона диспетчера ресурсов виртуальной Машины из образа hello.</span><span class="sxs-lookup"><span data-stu-id="902fc-189">Usually it's easiest toouse a Resource Manager template toocreate a VM from hello image.</span></span> <span data-ttu-id="902fc-190">Тем не менее, можно создать hello ВМ *принудительно* с помощью hello **создания виртуальной машины azure** с hello **-Q** (**--urn изображения**) параметра .</span><span class="sxs-lookup"><span data-stu-id="902fc-190">However, you can create hello VM *imperatively* by using hello **azure vm create** command with hello **-Q** (**--image-urn**) parameter.</span></span> <span data-ttu-id="902fc-191">При использовании этого метода можно также передать hello **-d** (**--ОС диска vhd-**) параметра toospecify hello расположение VHD-файл hello ОС для hello новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="902fc-191">If you use this method, you also pass hello **-d** (**--os-disk-vhd**) parameter toospecify hello location of hello OS .vhd file for hello new VM.</span></span> <span data-ttu-id="902fc-192">Этот файл должен быть в контейнере VHD-файлов hello учетной записи хранения hello, где хранится hello образ VHD-файл.</span><span class="sxs-lookup"><span data-stu-id="902fc-192">This file must be in hello vhds container of hello storage account where hello image VHD file is stored.</span></span> <span data-ttu-id="902fc-193">Здравствуйте, команда копирует hello виртуального жесткого диска для hello новой виртуальной Машины автоматически toohello **виртуальные жесткие диски** контейнера.</span><span class="sxs-lookup"><span data-stu-id="902fc-193">hello command copies hello VHD for hello new VM automatically toohello **vhds** container.</span></span>

<span data-ttu-id="902fc-194">Перед запуском **создания виртуальной машины azure** с образа hello, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="902fc-194">Before running **azure vm create** with hello image, complete hello following steps:</span></span>

1. <span data-ttu-id="902fc-195">Создайте группу ресурсов или укажите существующую группу ресурсов для развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="902fc-195">Create a resource group, or identify an existing resource group for hello deployment.</span></span>
2. <span data-ttu-id="902fc-196">Создайте открытый IP-адреса и ресурса сетевого Адаптера для hello новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="902fc-196">Create a public IP address resource and a NIC resource for hello new VM.</span></span> <span data-ttu-id="902fc-197">Действия toocreate виртуальной сети открытый IP-адреса и сетевого Адаптера с помощью hello CLI, см. выше в этой статье.</span><span class="sxs-lookup"><span data-stu-id="902fc-197">For steps toocreate a virtual network, public IP address, and NIC by using hello CLI, see earlier in this article.</span></span> <span data-ttu-id="902fc-198">(**создания виртуальной машины azure** можно также создать сетевой Адаптер, но требуется toopass Дополнительные параметры для виртуальной сети и подсети.)</span><span class="sxs-lookup"><span data-stu-id="902fc-198">(**azure vm create** can also create a NIC, but you need toopass additional parameters for a virtual network and subnet.)</span></span>

<span data-ttu-id="902fc-199">Выполните команду, которая передает идентификаторы URI tooboth hello новый файл виртуального жесткого диска операционной системы и hello существующий образ.</span><span class="sxs-lookup"><span data-stu-id="902fc-199">Then run a command that passes URIs tooboth hello new OS VHD file and hello existing image.</span></span> <span data-ttu-id="902fc-200">В этом примере размер виртуальной Машины Standard_A1 создается в регионе Восток США hello.</span><span class="sxs-lookup"><span data-stu-id="902fc-200">In this example, a size Standard_A1 VM is created in hello East US region.</span></span>

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

<span data-ttu-id="902fc-201">Чтобы получить информацию о дополнительных параметрах команды, выполните команду `azure help vm create`.</span><span class="sxs-lookup"><span data-stu-id="902fc-201">For additional command options, run `azure help vm create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="902fc-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="902fc-202">Next steps</span></span>
<span data-ttu-id="902fc-203">toomanage виртуальные машины с hello CLI, просмотреть задачи hello в [развертывание и управление виртуальными машинами с помощью шаблонов диспетчера ресурсов Azure и Azure CLI hello](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="902fc-203">toomanage your VMs with hello CLI, see hello tasks in [Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI](create-ssh-secured-vm-from-template.md).</span></span>

