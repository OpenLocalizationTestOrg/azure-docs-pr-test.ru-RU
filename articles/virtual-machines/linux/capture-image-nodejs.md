---
title: "Запись образа виртуальной машины Linux Azure для его использования в качестве шаблона | Документация Майкрософт"
description: "Узнайте, как записать и подготовить образ виртуальной машины Azure под управлением Linux, созданной посредством модели развертывания с помощью Azure Resource Manager."
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
ms.openlocfilehash: b1164fbd816eea5189786850f096438e32f8f802
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a><span data-ttu-id="268ab-103">Запись виртуальной машины Linux, работающей в Azure</span><span class="sxs-lookup"><span data-stu-id="268ab-103">Capture a Linux virtual machine running on Azure</span></span>
<span data-ttu-id="268ab-104">Выполните инструкции в этой статье, чтобы подготовить и записать образ виртуальной машины под управлением Linux для Azure в рамках модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="268ab-104">Follow the steps in this article to generalize and capture your Azure Linux virtual machine (VM) in the Resource Manager deployment model.</span></span> <span data-ttu-id="268ab-105">При подготовке к использованию виртуальной машины удаляются личные сведения учетных записей и виртуальная машина подготавливается к использованию в качестве образа.</span><span class="sxs-lookup"><span data-stu-id="268ab-105">When you generalize the VM, you remove personal account information and prepare the VM to be used as an image.</span></span> <span data-ttu-id="268ab-106">После этого можно записать универсальный образ виртуального жесткого диска (VHD) для операционной системы, виртуальные жесткие диски для подключенных дисков данных и [шаблон Resource Manager](../../azure-resource-manager/resource-group-overview.md) для развертывания новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="268ab-106">You then capture a generalized virtual hard disk (VHD) image for the OS, VHDs for attached data disks, and a [Resource Manager template](../../azure-resource-manager/resource-group-overview.md) for new VM deployments.</span></span> <span data-ttu-id="268ab-107">В этой статье подробно описано, как записать образ виртуальной машины, использующей неуправляемые диски, с помощью Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="268ab-107">This article details how to capture a VM image with the Azure CLI 1.0 for a VM using unmanaged disks.</span></span> <span data-ttu-id="268ab-108">Вы можете также [записать образ виртуальной машины, использующей Управляемые диски Azure, с помощью Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="268ab-108">You can also [capture a VM using Azure Managed Disks with the Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="268ab-109">Управляемые диски полностью контролируются платформой Azure и не требуют никакой подготовки или выделения места.</span><span class="sxs-lookup"><span data-stu-id="268ab-109">Managed disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="268ab-110">Дополнительные сведения об Управляемых дисках Azure см. в [этой статье](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="268ab-110">For more information, see [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="268ab-111">Для создания виртуальных машин с помощью образа следует настроить сетевые ресурсы для каждой новой виртуальной машины и развернуть ее посредством записанных образов VHD, воспользовавшись шаблоном (файлом нотаций объектов JavaScript, т. е. JSON-файлом).</span><span class="sxs-lookup"><span data-stu-id="268ab-111">To create VMs using the image, set up network resources for each new VM, and use the template (a JavaScript Object Notation, or JSON, file) to deploy it from the captured VHD images.</span></span> <span data-ttu-id="268ab-112">Таким образом можно реплицировать виртуальную машину и ее текущую конфигурацию программного обеспечения точно так же, как вы используете образы из Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="268ab-112">In this way, you can replicate a VM with its current software configuration, similar to the way you use images in the Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="268ab-113">Если вы хотите создать копию существующей виртуальной машины Linux в конкретном состоянии в целях архивации или отладки, ознакомьтесь с разделом [Создание копии виртуальной машины Linux, работающей в Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="268ab-113">If you want to create a copy of your existing Linux VM with its specialized state for backup or debugging, see [Create a copy of a Linux virtual machine running on Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="268ab-114">А если вам требуется передать виртуальный жесткий диск Linux локальной виртуальной машины, ознакомьтесь с разделом [Передача пользовательского образа диска и создание виртуальной машины Linux на его основе](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="268ab-114">And if you want to upload a Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>  

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="268ab-115">Версии интерфейса командной строки для выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="268ab-115">CLI versions to complete the task</span></span>
<span data-ttu-id="268ab-116">Вы можете выполнить задачу, используя одну из следующих версий интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="268ab-116">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="268ab-117">[Azure CLI 1.0](#before-you-begin) — интерфейс командной строки для классической модели развертывания и модели развертывания Resource Manager (в этой статье).</span><span class="sxs-lookup"><span data-stu-id="268ab-117">[Azure CLI 1.0](#before-you-begin) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="268ab-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) — интерфейс командной строки следующего поколения для модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="268ab-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="268ab-119">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="268ab-119">Before you begin</span></span>
<span data-ttu-id="268ab-120">Необходимо выполнить следующие условия.</span><span class="sxs-lookup"><span data-stu-id="268ab-120">Ensure that you meet the following prerequisites:</span></span>

* <span data-ttu-id="268ab-121">**Виртуальная машина Azure, созданная в рамках модели развертывания с помощью Resource Manager**. Если вы еще не создали виртуальную машину Linux, для этого можно использовать [портал](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [интерфейс командной строки Azure (Azure CLI)](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или [шаблоны Resource Manager](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="268ab-121">**Azure VM created in the Resource Manager deployment model** - If you haven't created a Linux VM, you can use the [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), the [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> 
  
    <span data-ttu-id="268ab-122">Настройте виртуальную машину согласно своим требованиям.</span><span class="sxs-lookup"><span data-stu-id="268ab-122">Configure the VM as needed.</span></span> <span data-ttu-id="268ab-123">Например, [добавьте диски данных](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), примените обновления и установите приложения.</span><span class="sxs-lookup"><span data-stu-id="268ab-123">For example, [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), apply updates, and install applications.</span></span> 
* <span data-ttu-id="268ab-124">**Azure CLI**. Установите [Azure CLI](../../cli-install-nodejs.md) на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="268ab-124">**Azure CLI** - Install the [Azure CLI](../../cli-install-nodejs.md) on a local computer.</span></span>

## <a name="step-1-remove-the-azure-linux-agent"></a><span data-ttu-id="268ab-125">Шаг 1. Удалите агент Linux для Azure</span><span class="sxs-lookup"><span data-stu-id="268ab-125">Step 1: Remove the Azure Linux agent</span></span>
<span data-ttu-id="268ab-126">Сначала на виртуальной машине Linux выполните команду **waagent** с параметром **deprovision**.</span><span class="sxs-lookup"><span data-stu-id="268ab-126">First, run the **waagent** command with the **deprovision** parameter on the Linux VM.</span></span> <span data-ttu-id="268ab-127">Эта команда удаляет файлы и данные перед подготовкой виртуальной машины к использованию.</span><span class="sxs-lookup"><span data-stu-id="268ab-127">This command deletes files and data to make the VM ready for generalizing.</span></span> <span data-ttu-id="268ab-128">Дополнительные сведения см. в [руководстве пользователя агента Linux для Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="268ab-128">For details, see the [Azure Linux Agent user guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

1. <span data-ttu-id="268ab-129">Подключитесь к виртуальной машине Linux c помощью клиента SSH.</span><span class="sxs-lookup"><span data-stu-id="268ab-129">Connect to your Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="268ab-130">В окне сеанса SSH введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="268ab-130">In the SSH window, type the following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > <span data-ttu-id="268ab-131">Эту команду следует выполнять только на той виртуальной машине, образ которой вы хотите записать.</span><span class="sxs-lookup"><span data-stu-id="268ab-131">Only run this command on a VM that you intend to capture as an image.</span></span> <span data-ttu-id="268ab-132">Она не гарантирует, что из образа будет удалена вся конфиденциальная информация и что он будет готов к повторному распространению.</span><span class="sxs-lookup"><span data-stu-id="268ab-132">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution.</span></span>
 
3. <span data-ttu-id="268ab-133">Чтобы продолжить, введите **y** .</span><span class="sxs-lookup"><span data-stu-id="268ab-133">Type **y** to continue.</span></span> <span data-ttu-id="268ab-134">Чтобы запрос на подтверждение не появлялся, добавьте параметр **-force** .</span><span class="sxs-lookup"><span data-stu-id="268ab-134">You can add the **-force** parameter to avoid this confirmation step.</span></span>
4. <span data-ttu-id="268ab-135">После выполнения команды введите **exit**.</span><span class="sxs-lookup"><span data-stu-id="268ab-135">After the command completes, type **exit**.</span></span> <span data-ttu-id="268ab-136">Клиент SSH будет закрыт.</span><span class="sxs-lookup"><span data-stu-id="268ab-136">This step closes the SSH client.</span></span>

## <a name="step-2-capture-the-vm"></a><span data-ttu-id="268ab-137">Шаг 2. Запись виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="268ab-137">Step 2: Capture the VM</span></span>
<span data-ttu-id="268ab-138">Используйте Azure CLI для подготовки и записи виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="268ab-138">Use the Azure CLI to generalize and capture the VM.</span></span> <span data-ttu-id="268ab-139">В следующих примерах замените имена параметров собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="268ab-139">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="268ab-140">Примеры имен параметров: **myResourceGroup**, **myVnet** и **myVM**.</span><span class="sxs-lookup"><span data-stu-id="268ab-140">Example parameter names include **myResourceGroup**, **myVnet**, and **myVM**.</span></span>

1. <span data-ttu-id="268ab-141">На локальном компьютере откройте Azure CLI и [войдите в свою подписку Azure](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="268ab-141">From your local computer, open the Azure CLI and [login to your Azure subscription](../../xplat-cli-connect.md).</span></span> 
2. <span data-ttu-id="268ab-142">Убедитесь, что режим Resource Manager включен.</span><span class="sxs-lookup"><span data-stu-id="268ab-142">Make sure you are in Resource Manager mode.</span></span>
   
    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="268ab-143">Завершите работу отозванной виртуальной машины с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="268ab-143">Shut down the VM that you already deprovisioned by using the following command:</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. <span data-ttu-id="268ab-144">Обобщите виртуальную машину:</span><span class="sxs-lookup"><span data-stu-id="268ab-144">Generalize the VM with the following command:</span></span>
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. <span data-ttu-id="268ab-145">Теперь выполните команду **azure vm capture**, которая записывает виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="268ab-145">Now run the **azure vm capture** command, which captures the VM.</span></span> <span data-ttu-id="268ab-146">В следующем примере виртуальные жесткие диски образа записываются с именами, которые начинаются с **MyVHDNamePrefix**, а параметр **-t** указывает путь к шаблону **MyTemplate.json**.</span><span class="sxs-lookup"><span data-stu-id="268ab-146">In the following example, the image VHDs are captured with names beginning with **MyVHDNamePrefix**, and the **-t** option specifies a path to the template **MyTemplate.json**.</span></span> 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > <span data-ttu-id="268ab-147">По умолчанию VHD-файлы образа создаются в учетной записи хранения, которую использует исходная виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="268ab-147">The image VHD files get created by default in the same storage account that the original VM used.</span></span> <span data-ttu-id="268ab-148">Для хранения виртуальных жестких дисков для любых новых виртуальных машин, создаваемых из образа, используйте ту же *учетную запись хранения*.</span><span class="sxs-lookup"><span data-stu-id="268ab-148">Use the *same storage account* to store the VHDs for any new VMs you create from the image.</span></span> 

6. <span data-ttu-id="268ab-149">Чтобы найти расположение записанного образа, откройте шаблон JSON в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="268ab-149">To find the location of a captured image, open the JSON template in a text editor.</span></span> <span data-ttu-id="268ab-150">В разделе **storageProfile** в контейнере **system** найдите **универсальный код ресурса (URI)** **образа**.</span><span class="sxs-lookup"><span data-stu-id="268ab-150">In the **storageProfile**, find the **uri** of the **image** located in the **system** container.</span></span> <span data-ttu-id="268ab-151">Например, универсальный код ресурса (URI) для образа диска ОС может выглядеть так: `https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span><span class="sxs-lookup"><span data-stu-id="268ab-151">For example, the URI of the OS disk image is similar to `https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>

## <a name="step-3-create-a-vm-from-the-captured-image"></a><span data-ttu-id="268ab-152">Шаг 3. Создание виртуальной машины из записанного образа</span><span class="sxs-lookup"><span data-stu-id="268ab-152">Step 3: Create a VM from the captured image</span></span>
<span data-ttu-id="268ab-153">Теперь с помощью образа и шаблона мы создадим виртуальную машину под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="268ab-153">Now use the image with a template to create a Linux VM.</span></span> <span data-ttu-id="268ab-154">Ниже описывается, как можно создать виртуальную машину в новой виртуальной сети, используя Azure CLI и записанный JSON-файл шаблона.</span><span class="sxs-lookup"><span data-stu-id="268ab-154">These steps show you how to use the Azure CLI and the JSON file template you captured to create the VM in a new virtual network.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="268ab-155">Создание сетевых ресурсов</span><span class="sxs-lookup"><span data-stu-id="268ab-155">Create network resources</span></span>
<span data-ttu-id="268ab-156">Чтобы использовать шаблон, для новой виртуальной машины сначала необходимо настроить виртуальную сеть и сетевую карту.</span><span class="sxs-lookup"><span data-stu-id="268ab-156">To use the template, you first need to set up a virtual network and NIC for your new VM.</span></span> <span data-ttu-id="268ab-157">Мы рекомендуем создать группу ресурсов для этих ресурсов в расположении, в котором хранится образ виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="268ab-157">We recommend you create a resource group for these resources in the location where your VM image is stored.</span></span> <span data-ttu-id="268ab-158">Выполните приведенные ниже команды, подставив нужные имена ресурсов и указав соответствующий регион Azure (вместе centralus).</span><span class="sxs-lookup"><span data-stu-id="268ab-158">Run commands similar to the following, substituting names for your resources and an appropriate Azure location ("centralus" in these commands):</span></span>

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-the-id-of-the-nic"></a><span data-ttu-id="268ab-159">Получение идентификатора сетевой карты</span><span class="sxs-lookup"><span data-stu-id="268ab-159">Get the Id of the NIC</span></span>
<span data-ttu-id="268ab-160">Чтобы развернуть виртуальную машину из образа, используя JSON-файл, который был сохранен во время записи образа, требуется идентификатор сетевой карты.</span><span class="sxs-lookup"><span data-stu-id="268ab-160">To deploy a VM from the image by using the JSON you saved during capture, you need the Id of the NIC.</span></span> <span data-ttu-id="268ab-161">Получить идентификатор можно с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="268ab-161">Obtain it by running the following command:</span></span>

```azurecli
azure network nic show myResourceGroup1 myNIC
```

<span data-ttu-id="268ab-162">Значение **Id** в выходных данных имеет следующий вид: `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`.</span><span class="sxs-lookup"><span data-stu-id="268ab-162">The **Id** in the output is similar to `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="268ab-163">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="268ab-163">Create a VM</span></span>
<span data-ttu-id="268ab-164">Теперь из записанного образа создайте виртуальную машину. Для этого выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="268ab-164">Now run the following command to create your VM from the captured VM image.</span></span> <span data-ttu-id="268ab-165">Используйте параметр **-f**, чтобы указать путь к сохраненному JSON-файлу шаблона.</span><span class="sxs-lookup"><span data-stu-id="268ab-165">Use the **-f** parameter to specify the path to the template JSON file you saved.</span></span>

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

<span data-ttu-id="268ab-166">После вывода результатов команды вам будет предложено указать имя виртуальной машины, имя и пароль администратора, а также идентификатор созданной ранее сетевой карты.</span><span class="sxs-lookup"><span data-stu-id="268ab-166">In the command output, you are prompted to supply a new VM name, the admin user name and password, and the Id of the NIC you created previously.</span></span>

```bash
info:    Executing command group deployment create
info:    Supply values for the following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

<span data-ttu-id="268ab-167">Ниже приведен пример вывода на экран при успешном развертывании.</span><span class="sxs-lookup"><span data-stu-id="268ab-167">The following sample shows what you see for a successful deployment:</span></span>

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment to complete
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

### <a name="verify-the-deployment"></a><span data-ttu-id="268ab-168">Проверка развертывания</span><span class="sxs-lookup"><span data-stu-id="268ab-168">Verify the deployment</span></span>
<span data-ttu-id="268ab-169">Чтобы проверить развертывание и начать использовать новую виртуальную машину, подключитесь к ней с помощью SSH-клиента.</span><span class="sxs-lookup"><span data-stu-id="268ab-169">Now SSH to the virtual machine you created to verify the deployment and start using the new VM.</span></span> <span data-ttu-id="268ab-170">Для этого сначала определите IP-адрес созданной виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="268ab-170">To connect via SSH, find the IP address of the VM you created by running the following command:</span></span>

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

<span data-ttu-id="268ab-171">Команда возвращает общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="268ab-171">The public IP address is listed in the command output.</span></span> <span data-ttu-id="268ab-172">По умолчанию подключение к виртуальной машине Linux по протоколу SSH выполняется через порт 22.</span><span class="sxs-lookup"><span data-stu-id="268ab-172">By default you connect to the Linux VM by SSH on port 22.</span></span>

## <a name="create-additional-vms"></a><span data-ttu-id="268ab-173">Создание дополнительных виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="268ab-173">Create additional VMs</span></span>
<span data-ttu-id="268ab-174">Развертывание дополнительных виртуальных машин с использованием записанного образа и шаблона выполняется так же, как описано в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="268ab-174">Use the captured image and template to deploy additional VMs using the steps in the preceding section.</span></span> <span data-ttu-id="268ab-175">Кроме того, для создания виртуальных машин из образа можно использовать шаблон быстрого запуска или команду **azure vm create**.</span><span class="sxs-lookup"><span data-stu-id="268ab-175">Other options to create VMs from the image include using a quickstart template or running the **azure vm create** command.</span></span>

### <a name="use-the-captured-template"></a><span data-ttu-id="268ab-176">Использование записанного шаблона</span><span class="sxs-lookup"><span data-stu-id="268ab-176">Use the captured template</span></span>
<span data-ttu-id="268ab-177">Чтобы использовать записанные образ и шаблон, выполните приведенные ниже действия (которые подробно описаны в предыдущем разделе).</span><span class="sxs-lookup"><span data-stu-id="268ab-177">To use the captured image and template, follow these steps (detailed in the preceding section):</span></span>

* <span data-ttu-id="268ab-178">Убедитесь, что образ виртуальной машины хранится в той же учетной записи хранения, в которой размещен виртуальный жесткий диск виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="268ab-178">Ensure that your VM image is in the same storage account that hosts your VM's VHD.</span></span>
* <span data-ttu-id="268ab-179">Скопируйте JSON-файл шаблона и укажите уникальное имя для виртуального жесткого диска (или дисков) ОС новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="268ab-179">Copy the template JSON file and specify a unique name for the OS disk of the new VM's VHD (or VHDs).</span></span> <span data-ttu-id="268ab-180">Например, в разделе **storageProfile** в подразделе **vhd** в элементе **uri** укажите уникальное имя виртуального жесткого диска **osDisk**. Пример: `https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span><span class="sxs-lookup"><span data-stu-id="268ab-180">For example, in the **storageProfile**, under **vhd**, in **uri**, specify a unique name for the **osDisk** VHD, similar to `https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>
* <span data-ttu-id="268ab-181">Создайте сетевую карту в той же или другой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="268ab-181">Create a NIC in either the same or a different virtual network.</span></span>
* <span data-ttu-id="268ab-182">С помощью измененного JSON-файла шаблона создайте развертывание в группе ресурсов, в которой вы настраиваете виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="268ab-182">Using the modified template JSON file, create a deployment in the resource group in which you set up the virtual network.</span></span>

### <a name="use-a-quickstart-template"></a><span data-ttu-id="268ab-183">Использование шаблона быстрого запуска</span><span class="sxs-lookup"><span data-stu-id="268ab-183">Use a quickstart template</span></span>
<span data-ttu-id="268ab-184">Если вы хотите, чтобы параметры сети настроились автоматически при создании виртуальной машины из образа, то можете указать ее ресурсы в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="268ab-184">If you want the network set up automatically when you create a VM from the image, you can specify those resources in a template.</span></span> <span data-ttu-id="268ab-185">Для примера можно ознакомиться с шаблоном [101-vm-from-user-image template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) с сайта GitHub.</span><span class="sxs-lookup"><span data-stu-id="268ab-185">For example, see the [101-vm-from-user-image template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) from GitHub.</span></span> <span data-ttu-id="268ab-186">Этот шаблон создает не только виртуальную машину из пользовательского образа, но и необходимую виртуальную сеть, общедоступный IP-адрес и сетевые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="268ab-186">This template creates a VM from your custom image and the necessary virtual network, public IP address, and NIC resources.</span></span> <span data-ttu-id="268ab-187">Пошаговые инструкции по использованию шаблона на портале Azure см. в статье [How to create a virtual machine from a custom image using a ARM template](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/) (Как создать виртуальную машину из пользовательского образа с помощью шаблона ARM).</span><span class="sxs-lookup"><span data-stu-id="268ab-187">For a walkthrough of using the template in the Azure portal, see [How to create a virtual machine from a custom image using a Resource Manager template](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span></span>

### <a name="use-the-azure-vm-create-command"></a><span data-ttu-id="268ab-188">Команда azure vm create</span><span class="sxs-lookup"><span data-stu-id="268ab-188">Use the azure vm create command</span></span>
<span data-ttu-id="268ab-189">Обычно для создания виртуальной машины из образа проще всего использовать шаблон Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="268ab-189">Usually it's easiest to use a Resource Manager template to create a VM from the image.</span></span> <span data-ttu-id="268ab-190">Однако виртуальную машину можно создать и *по запросу* — с помощью команды **azure vm create** с параметром **-Q** (**--image-urn**).</span><span class="sxs-lookup"><span data-stu-id="268ab-190">However, you can create the VM *imperatively* by using the **azure vm create** command with the **-Q** (**--image-urn**) parameter.</span></span> <span data-ttu-id="268ab-191">В случае использования данного метода также передается параметр **-d** (**--os-disk-vhd**), чтобы указать расположение VHD-файла операционной системы для новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="268ab-191">If you use this method, you also pass the **-d** (**--os-disk-vhd**) parameter to specify the location of the OS .vhd file for the new VM.</span></span> <span data-ttu-id="268ab-192">Этот файл должен находиться в контейнере виртуальных жестких дисков учетной записи хранения, где хранится VHD-файл образа.</span><span class="sxs-lookup"><span data-stu-id="268ab-192">This file must be in the vhds container of the storage account where the image VHD file is stored.</span></span> <span data-ttu-id="268ab-193">Эта команда автоматически копирует виртуальный жесткий диск для новой виртуальной машины в контейнер **vhds**.</span><span class="sxs-lookup"><span data-stu-id="268ab-193">The command copies the VHD for the new VM automatically to the **vhds** container.</span></span>

<span data-ttu-id="268ab-194">Прежде чем создать виртуальную машину из образа с помощью команды **azure vm create**, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="268ab-194">Before running **azure vm create** with the image, complete the following steps:</span></span>

1. <span data-ttu-id="268ab-195">Создайте для развертывания группу ресурсов или укажите существующую.</span><span class="sxs-lookup"><span data-stu-id="268ab-195">Create a resource group, or identify an existing resource group for the deployment.</span></span>
2. <span data-ttu-id="268ab-196">Создайте для новой виртуальной машины общедоступный IP-адрес и сетевой адаптер.</span><span class="sxs-lookup"><span data-stu-id="268ab-196">Create a public IP address resource and a NIC resource for the new VM.</span></span> <span data-ttu-id="268ab-197">Процедура создания виртуальной сети, общедоступного IP-адреса и сетевого адаптера с помощью интерфейса командной строки описана выше в этой статье.</span><span class="sxs-lookup"><span data-stu-id="268ab-197">For steps to create a virtual network, public IP address, and NIC by using the CLI, see earlier in this article.</span></span> <span data-ttu-id="268ab-198">(Команда**azure vm create** может также создать и сетевую карту, но для этого потребуется указать дополнительные параметры виртуальной сети и подсети.)</span><span class="sxs-lookup"><span data-stu-id="268ab-198">(**azure vm create** can also create a NIC, but you need to pass additional parameters for a virtual network and subnet.)</span></span>

<span data-ttu-id="268ab-199">Затем выполните команду, которая передает универсальный код ресурса (URI) в новый VHD-файл операционной системы и в существующий образ.</span><span class="sxs-lookup"><span data-stu-id="268ab-199">Then run a command that passes URIs to both the new OS VHD file and the existing image.</span></span> <span data-ttu-id="268ab-200">В этом примере создается виртуальная машина размера Standard_A1 в регионе "Восточная часть США".</span><span class="sxs-lookup"><span data-stu-id="268ab-200">In this example, a size Standard_A1 VM is created in the East US region.</span></span>

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

<span data-ttu-id="268ab-201">Чтобы получить информацию о дополнительных параметрах команды, выполните команду `azure help vm create`.</span><span class="sxs-lookup"><span data-stu-id="268ab-201">For additional command options, run `azure help vm create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="268ab-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="268ab-202">Next steps</span></span>
<span data-ttu-id="268ab-203">Для управления виртуальными машинами с помощью интерфейса командной строки ознакомьтесь с задачами, описанными в статье [Развертывание виртуальных машин и управление ими с помощью шаблонов диспетчера ресурсов Azure и интерфейса командной строки Azure](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="268ab-203">To manage your VMs with the CLI, see the tasks in [Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI](create-ssh-secured-vm-from-template.md).</span></span>

