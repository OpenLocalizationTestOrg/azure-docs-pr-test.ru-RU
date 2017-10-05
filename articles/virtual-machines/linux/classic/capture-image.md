---
title: "Запись образа виртуальной машины Linux | Документация Майкрософт"
description: "Узнайте, как записать образ виртуальной машины Azure под управлением Linux, созданной с помощью классической модели развертывания."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17d7ffee-a58e-4290-9de1-64c3cf1ddc05
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: ecde5dd3211bfbb290e6910d7d55136d079c6cf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-capture-a-classic-linux-virtual-machine-as-an-image"></a><span data-ttu-id="bb87b-103">Запись классической виртуальной машины Linux в виде образа</span><span class="sxs-lookup"><span data-stu-id="bb87b-103">How to capture a classic Linux virtual machine as an image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bb87b-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bb87b-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bb87b-105">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="bb87b-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="bb87b-106">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="bb87b-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="bb87b-107">Узнайте, как [выполнить эти действия с помощью модели Resource Manager](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bb87b-107">Learn how to [perform these steps using the Resource Manager model](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="bb87b-108">В этой статье показано, как записать классическую виртуальную машину Azure под управлением Linux, чтобы использовать ее в качестве образа при создании других виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="bb87b-108">This article shows you how to capture a classic Azure virtual machine (VM) running Linux as an image to create other virtual machines.</span></span> <span data-ttu-id="bb87b-109">Данный образ виртуальной машины включает в себя диск операционной системы и прочие диски данных, присоединенные к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="bb87b-109">This image includes the OS disk and data disks attached to the VM.</span></span> <span data-ttu-id="bb87b-110">Он не включает в себя сетевую конфигурацию, поэтому ее необходимо настроить при создании другой виртуальной машины из образа.</span><span class="sxs-lookup"><span data-stu-id="bb87b-110">It doesn't include networking configuration, so you need to configure that when you create the other VM from the image.</span></span>

<span data-ttu-id="bb87b-111">Azure хранит образ в папке **Images** (Образы) вместе со всеми передаваемыми пользователем образами.</span><span class="sxs-lookup"><span data-stu-id="bb87b-111">Azure stores the image under **Images**, along with any images you've uploaded.</span></span> <span data-ttu-id="bb87b-112">Дополнительные сведения об образах см. в статье [Об образах виртуальных машин Linux][About Virtual Machine Images in Azure].</span><span class="sxs-lookup"><span data-stu-id="bb87b-112">For more information about images, see [About Virtual Machine Images in Azure][About Virtual Machine Images in Azure].</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bb87b-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="bb87b-113">Before you begin</span></span>
<span data-ttu-id="bb87b-114">В шагах этой статьи предполагается, что вы уже создали виртуальную машину Azure, используя классическую модель развертывания, и настроили операционную систему, а также присоединили диски данных.</span><span class="sxs-lookup"><span data-stu-id="bb87b-114">These steps assume that you've already created an Azure VM using the Classic deployment model and configured the operating system, including attaching any data disks.</span></span> <span data-ttu-id="bb87b-115">Если необходимо создать виртуальную машину, то прочтите статью [Создание виртуальной машины Linux с помощью интерфейса командной строки Azure][How to Create a Linux Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="bb87b-115">If you need to create a VM, read [How to Create a Linux Virtual Machine][How to Create a Linux Virtual Machine].</span></span>

## <a name="capture-the-virtual-machine"></a><span data-ttu-id="bb87b-116">Запись виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="bb87b-116">Capture the virtual machine</span></span>
1. <span data-ttu-id="bb87b-117">[Подключитесь к виртуальной машине](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) с помощью выбранного клиента SSH.</span><span class="sxs-lookup"><span data-stu-id="bb87b-117">[Connect to the VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) using an SSH client of your choice.</span></span>
2. <span data-ttu-id="bb87b-118">В окне SSH введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="bb87b-118">In the SSH window, type the following command.</span></span> <span data-ttu-id="bb87b-119">Выходные данные `waagent` могут незначительно отличаться в зависимости от версии этой служебной программы.</span><span class="sxs-lookup"><span data-stu-id="bb87b-119">The output from `waagent` may vary slightly depending on the version of this utility:</span></span>

    ```bash
    sudo waagent -deprovision+user
    ```

    <span data-ttu-id="bb87b-120">Эта команда пытается очистить систему и сделать ее пригодной для повторной подготовки.</span><span class="sxs-lookup"><span data-stu-id="bb87b-120">The preceding command attempts to clean the system and make it suitable for reprovisioning.</span></span> <span data-ttu-id="bb87b-121">В ходе операции выполняются такие задачи:</span><span class="sxs-lookup"><span data-stu-id="bb87b-121">This operation performs the following tasks:</span></span>

   * <span data-ttu-id="bb87b-122">удаляются ключи узла SSH (если в файле конфигурации для Provisioning.RegenerateSshHostKeyPair указано значение «y»);</span><span class="sxs-lookup"><span data-stu-id="bb87b-122">Removes SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in the configuration file)</span></span>
   * <span data-ttu-id="bb87b-123">очищается конфигурация имени сервера в /etc/resolv.conf;</span><span class="sxs-lookup"><span data-stu-id="bb87b-123">Clears nameserver configuration in /etc/resolv.conf</span></span>
   * <span data-ttu-id="bb87b-124">удаляется пароль пользователя `root` из /etc/shadow (если в файле конфигурации для Provisioning.DeleteRootPassword указано значение "y");</span><span class="sxs-lookup"><span data-stu-id="bb87b-124">Removes the `root` user password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in the configuration file)</span></span>
   * <span data-ttu-id="bb87b-125">удаляются кэшированные аренды DHCP-клиентов.</span><span class="sxs-lookup"><span data-stu-id="bb87b-125">Removes cached DHCP client leases</span></span>
   * <span data-ttu-id="bb87b-126">возвращается имя узла localhost.localdomain;</span><span class="sxs-lookup"><span data-stu-id="bb87b-126">Resets host name to localhost.localdomain</span></span>
   * <span data-ttu-id="bb87b-127">удаляется последняя подготовленная учетная запись пользователя (полученная из /var/lib/waagent) и **связанные с ней данные**.</span><span class="sxs-lookup"><span data-stu-id="bb87b-127">Deletes the last provisioned user account (obtained from /var/lib/waagent) **and associated data**.</span></span>

     > [!NOTE]
     > <span data-ttu-id="bb87b-128">Процедура отзыва приводит к удалению файлов и данных, так как образ подготавливается к использованию.</span><span class="sxs-lookup"><span data-stu-id="bb87b-128">Deprovisioning deletes files and data to "generalize" the image.</span></span> <span data-ttu-id="bb87b-129">Эту команду следует выполнять только на виртуальных машинах, которые требуется записать как шаблон нового образа.</span><span class="sxs-lookup"><span data-stu-id="bb87b-129">Only run this command on a VM that you intend to capture as a new image template.</span></span> <span data-ttu-id="bb87b-130">Отзыв не гарантирует, что из образа будет удалена вся конфиденциальная информация и что он будет готов к повторному распространению третьим сторонам.</span><span class="sxs-lookup"><span data-stu-id="bb87b-130">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution to third parties.</span></span>

3. <span data-ttu-id="bb87b-131">Чтобы продолжить, введите **y** .</span><span class="sxs-lookup"><span data-stu-id="bb87b-131">Type **y** to continue.</span></span> <span data-ttu-id="bb87b-132">Чтобы предотвратить появление запроса на подтверждение, добавьте параметр `-force` .</span><span class="sxs-lookup"><span data-stu-id="bb87b-132">You can add the `-force` parameter to avoid this confirmation step.</span></span>
4. <span data-ttu-id="bb87b-133">Введите **Exit** , чтобы закрыть SSH-клиент.</span><span class="sxs-lookup"><span data-stu-id="bb87b-133">Type **Exit** to close the SSH client.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bb87b-134">Далее предполагается, что вы уже [установили интерфейс командной строки Azure CLI](../../../cli-install-nodejs.md) (Azure CLI) на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="bb87b-134">The remaining steps assume you have already [installed the Azure CLI](../../../cli-install-nodejs.md) on your client computer.</span></span> <span data-ttu-id="bb87b-135">Все следующие действия также можно выполнить на [портале Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bb87b-135">All the following steps can also be done in the [Azure portal](http://portal.azure.com).</span></span>

5. <span data-ttu-id="bb87b-136">На клиентском компьютере откройте интерфейс командной строки Azure и войдите в подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="bb87b-136">From your client computer, open Azure CLI and login to your Azure subscription.</span></span> <span data-ttu-id="bb87b-137">Дополнительные сведения см. в статье [Войдите в Azure из командной строки Azure](../../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="bb87b-137">For details, read [Connect to an Azure subscription from the Azure CLI](../../../xplat-cli-connect.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="bb87b-138">Зайдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="bb87b-138">In the Azure portal, log in to the portal.</span></span>

6. <span data-ttu-id="bb87b-139">Убедитесь, что вы находитесь в режиме управления службами:</span><span class="sxs-lookup"><span data-stu-id="bb87b-139">Make sure you are in Service Management mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

7. <span data-ttu-id="bb87b-140">Завершите работу виртуальной машины, которая была отозвана.</span><span class="sxs-lookup"><span data-stu-id="bb87b-140">Shut down the VM that is already deprovisioned.</span></span> <span data-ttu-id="bb87b-141">В следующем примере завершается работа виртуальной машины с именем `myVM`:</span><span class="sxs-lookup"><span data-stu-id="bb87b-141">The following example shuts down the VM named `myVM`:</span></span>

    ```azurecli
    azure vm shutdown myVM
    ```
   <span data-ttu-id="bb87b-142">При необходимости вы можете просмотреть список всех виртуальных машин, созданных в своей подписке, с помощью команды `azure vm list`</span><span class="sxs-lookup"><span data-stu-id="bb87b-142">If needed, you can view a list all the VMs created in your subscription by using `azure vm list`</span></span>

   > [!NOTE]
   > <span data-ttu-id="bb87b-143">Если вы используете портал Azure, выберите виртуальную машину и щелкните **Остановить** для завершения ее работы.</span><span class="sxs-lookup"><span data-stu-id="bb87b-143">If you're using the Azure portal, select the VM and click **Stop** to shut down the VM.</span></span>

8. <span data-ttu-id="bb87b-144">Когда виртуальная машина остановлена, запишите образ.</span><span class="sxs-lookup"><span data-stu-id="bb87b-144">When the VM is stopped, capture the image.</span></span> <span data-ttu-id="bb87b-145">В следующем примере выполняется запись виртуальной машины `myVM` и создается обобщенный образ `myNewVM`:</span><span class="sxs-lookup"><span data-stu-id="bb87b-145">The following example captures the VM named `myVM` and creates a generalized image named `myNewVM`:</span></span>

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    <span data-ttu-id="bb87b-146">Подкоманда `-t` удаляет исходную виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="bb87b-146">The `-t` subcommand deletes the original virtual machine.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bb87b-147">На портале Azure вы можете создать образ, выбрав **Образ** в главном меню.</span><span class="sxs-lookup"><span data-stu-id="bb87b-147">In the Azure portal, you can capture an image by selecting **Image** from the hub menu.</span></span> <span data-ttu-id="bb87b-148">Для образа необходимо указать следующие сведения: имя, группу ресурсов, расположение, тип операционной системы и путь к большому двоичному объекту хранилища.</span><span class="sxs-lookup"><span data-stu-id="bb87b-148">You need to supply the following information for the image: name, resource group, location, operating system type, and storage blob path.</span></span>

9. <span data-ttu-id="bb87b-149">Новый образ станет доступным в списке образов, которые можно использовать для настройки любой новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="bb87b-149">The new image is now available in the list of images that can be used to configure any new VM.</span></span> <span data-ttu-id="bb87b-150">Его можно просмотреть с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="bb87b-150">You can view it with the command:</span></span>

   ```azurecli
   azure vm image list
   ```

   <span data-ttu-id="bb87b-151">На [портале Azure](http://portal.azure.com) в окне **Образы VM (классика)**, которое относится к службам **Вычисления**, отобразится новый образ.</span><span class="sxs-lookup"><span data-stu-id="bb87b-151">On the [Azure portal](http://portal.azure.com), the new image appears in the **VM images (classic)** that belongs to the **Compute** services.</span></span> <span data-ttu-id="bb87b-152">Чтобы открыть окно **Образы VM (классика)**, в нижней части списка служб Azure выберите _Больше служб_ и найдите службы **Вычисления**.</span><span class="sxs-lookup"><span data-stu-id="bb87b-152">You can access **VM images (classic)** by clicking _More services_ at the bottom of the Azure service list, and then looking in the **Compute** services.</span></span>   

   ![Успешная запись образа](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="bb87b-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bb87b-154">Next steps</span></span>
<span data-ttu-id="bb87b-155">Образ готов к использованию для создания виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="bb87b-155">The image is ready to be used to create VMs.</span></span> <span data-ttu-id="bb87b-156">Вы можете использовать команду Azure CLI `azure vm create` и указать имя образа, который создали.</span><span class="sxs-lookup"><span data-stu-id="bb87b-156">You can use the Azure CLI command `azure vm create` and supply the image name you created.</span></span> <span data-ttu-id="bb87b-157">Дополнительные сведения см. в статье [Команды Azure CLI в режиме управления службами Azure (ASM)](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="bb87b-157">For more information, see [Using the Azure CLI with Classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

<span data-ttu-id="bb87b-158">Кроме того, с помощью [портала Azure](http://portal.azure.com) можно создать настраиваемую виртуальную машину, выбрав метод **Образ** и указав созданный образ.</span><span class="sxs-lookup"><span data-stu-id="bb87b-158">Alternatively, use the [Azure portal](http://portal.azure.com) to create a custom VM by using the **Image** method and selecting the image you created.</span></span> <span data-ttu-id="bb87b-159">Дополнительные сведения см. в статье [Создание виртуальной машины Linux с помощью интерфейса командной строки Azure][How to Create a Custom Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="bb87b-159">For more information, see [How to Create a Custom VM][How to Create a Custom Virtual Machine].</span></span>

<span data-ttu-id="bb87b-160">**См. также:** [Руководство пользователя агента Linux для Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bb87b-160">**See also:** [Azure Linux Agent User Guide](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How to Create a Custom Virtual Machine]:create-custom.md
[How to Attach a Data Disk to a Virtual Machine]:attach-disk.md
[How to Create a Linux Virtual Machine]:create-custom.md
