---
title: "образ виртуальной Машины Linux aaaCapture | Документы Microsoft"
description: "Узнайте, как toocapture под управлением Linux Azure виртуальной машины (VM) создан образ с hello классической модели развертывания."
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
ms.openlocfilehash: 33c4059d5bb919a86bdc3492abca540750f365ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocapture-a-classic-linux-virtual-machine-as-an-image"></a><span data-ttu-id="8be39-103">Как toocapture классической виртуальной машины Linux как изображение</span><span class="sxs-lookup"><span data-stu-id="8be39-103">How toocapture a classic Linux virtual machine as an image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8be39-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8be39-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8be39-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="8be39-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="8be39-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8be39-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="8be39-107">Узнайте, каким образом слишком[выполните следующие действия с помощью диспетчера ресурсов модели hello](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8be39-107">Learn how too[perform these steps using hello Resource Manager model](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="8be39-108">В этой статье показано, как toocapture классической виртуальной машине Azure (ВМ) других виртуальных машин под управлением Linux как toocreate изображения.</span><span class="sxs-lookup"><span data-stu-id="8be39-108">This article shows you how toocapture a classic Azure virtual machine (VM) running Linux as an image toocreate other virtual machines.</span></span> <span data-ttu-id="8be39-109">Этот образ содержит hello диска ОС и дисков данных присоединяется toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8be39-109">This image includes hello OS disk and data disks attached toohello VM.</span></span> <span data-ttu-id="8be39-110">Она не включает сетевую конфигурацию, поэтому требуется tooconfigure, при создании hello другой виртуальной Машины из образа hello.</span><span class="sxs-lookup"><span data-stu-id="8be39-110">It doesn't include networking configuration, so you need tooconfigure that when you create hello other VM from hello image.</span></span>

<span data-ttu-id="8be39-111">Хранилища Azure hello образа в разделе **изображения**, вместе с отправленное изображений.</span><span class="sxs-lookup"><span data-stu-id="8be39-111">Azure stores hello image under **Images**, along with any images you've uploaded.</span></span> <span data-ttu-id="8be39-112">Дополнительные сведения об образах см. в статье [Об образах виртуальных машин Linux][About Virtual Machine Images in Azure].</span><span class="sxs-lookup"><span data-stu-id="8be39-112">For more information about images, see [About Virtual Machine Images in Azure][About Virtual Machine Images in Azure].</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8be39-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="8be39-113">Before you begin</span></span>
<span data-ttu-id="8be39-114">Предполагается, что ВМ Azure с помощью hello классической модели развертывания и настроенный hello операционной системы, включая присоединение диски с данными, уже создана.</span><span class="sxs-lookup"><span data-stu-id="8be39-114">These steps assume that you've already created an Azure VM using hello Classic deployment model and configured hello operating system, including attaching any data disks.</span></span> <span data-ttu-id="8be39-115">Если вам требуется toocreate виртуальной Машины, чтение [как tooCreate виртуальной машины Linux][How tooCreate a Linux Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="8be39-115">If you need toocreate a VM, read [How tooCreate a Linux Virtual Machine][How tooCreate a Linux Virtual Machine].</span></span>

## <a name="capture-hello-virtual-machine"></a><span data-ttu-id="8be39-116">Запись hello виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="8be39-116">Capture hello virtual machine</span></span>
1. <span data-ttu-id="8be39-117">[Подключение виртуальной Машины toohello](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) с помощью такой клиент SSH, по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="8be39-117">[Connect toohello VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) using an SSH client of your choice.</span></span>
2. <span data-ttu-id="8be39-118">В окне приветствия SSH введите следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="8be39-118">In hello SSH window, type hello following command.</span></span> <span data-ttu-id="8be39-119">Вывод Hello `waagent` может несколько отличаться в зависимости от версии hello этой служебной программы:</span><span class="sxs-lookup"><span data-stu-id="8be39-119">hello output from `waagent` may vary slightly depending on hello version of this utility:</span></span>

    ```bash
    sudo waagent -deprovision+user
    ```

    <span data-ttu-id="8be39-120">Hello предыдущая команда пытается tooclean hello системы и соответствующих инициализацию.</span><span class="sxs-lookup"><span data-stu-id="8be39-120">hello preceding command attempts tooclean hello system and make it suitable for reprovisioning.</span></span> <span data-ttu-id="8be39-121">Эта операция не выполняет hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="8be39-121">This operation performs hello following tasks:</span></span>

   * <span data-ttu-id="8be39-122">Удаляет ключи SSH узла (если Provisioning.RegenerateSshHostKeyPair «y» в файле конфигурации hello)</span><span class="sxs-lookup"><span data-stu-id="8be39-122">Removes SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in hello configuration file)</span></span>
   * <span data-ttu-id="8be39-123">очищается конфигурация имени сервера в /etc/resolv.conf;</span><span class="sxs-lookup"><span data-stu-id="8be39-123">Clears nameserver configuration in /etc/resolv.conf</span></span>
   * <span data-ttu-id="8be39-124">Удаляет hello `root` пароль пользователя с/etc/тени (если Provisioning.DeleteRootPassword «y» в файле конфигурации hello)</span><span class="sxs-lookup"><span data-stu-id="8be39-124">Removes hello `root` user password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in hello configuration file)</span></span>
   * <span data-ttu-id="8be39-125">удаляются кэшированные аренды DHCP-клиентов.</span><span class="sxs-lookup"><span data-stu-id="8be39-125">Removes cached DHCP client leases</span></span>
   * <span data-ttu-id="8be39-126">Сброс размещения toolocalhost.localdomain имя</span><span class="sxs-lookup"><span data-stu-id="8be39-126">Resets host name toolocalhost.localdomain</span></span>
   * <span data-ttu-id="8be39-127">Удаляет hello последнего подготовленных учетную запись пользователя (полученные от /var/lib/waagent) **и связанные данные**.</span><span class="sxs-lookup"><span data-stu-id="8be39-127">Deletes hello last provisioned user account (obtained from /var/lib/waagent) **and associated data**.</span></span>

     > [!NOTE]
     > <span data-ttu-id="8be39-128">Отзыв удаляет файлы и данные слишком «generalize» hello изображения.</span><span class="sxs-lookup"><span data-stu-id="8be39-128">Deprovisioning deletes files and data too"generalize" hello image.</span></span> <span data-ttu-id="8be39-129">Только выполните команду на виртуальной Машине, следует присвоить toocapture как шаблон для нового образа.</span><span class="sxs-lookup"><span data-stu-id="8be39-129">Only run this command on a VM that you intend toocapture as a new image template.</span></span> <span data-ttu-id="8be39-130">Он не гарантирует этот образ hello подходит для распространения toothird сторон или удаляется все конфиденциальные данные.</span><span class="sxs-lookup"><span data-stu-id="8be39-130">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution toothird parties.</span></span>

3. <span data-ttu-id="8be39-131">Тип **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="8be39-131">Type **y** toocontinue.</span></span> <span data-ttu-id="8be39-132">Можно добавить hello `-force` tooavoid параметр этого шага подтверждения.</span><span class="sxs-lookup"><span data-stu-id="8be39-132">You can add hello `-force` parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="8be39-133">Тип **выхода** tooclose hello SSH-клиента.</span><span class="sxs-lookup"><span data-stu-id="8be39-133">Type **Exit** tooclose hello SSH client.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8be39-134">Hello оставшихся шагах предполагается уже имеется [установлен hello Azure CLI](../../../cli-install-nodejs.md) на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="8be39-134">hello remaining steps assume you have already [installed hello Azure CLI](../../../cli-install-nodejs.md) on your client computer.</span></span> <span data-ttu-id="8be39-135">Все hello действий может быть также выполнена в hello [портал Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8be39-135">All hello following steps can also be done in hello [Azure portal](http://portal.azure.com).</span></span>

5. <span data-ttu-id="8be39-136">С клиентского компьютера откройте Azure CLI и tooyour входа подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="8be39-136">From your client computer, open Azure CLI and login tooyour Azure subscription.</span></span> <span data-ttu-id="8be39-137">Дополнительные сведения и статье [подключение tooan подписки Azure из hello Azure CLI](../../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="8be39-137">For details, read [Connect tooan Azure subscription from hello Azure CLI](../../../xplat-cli-connect.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="8be39-138">В hello портал Azure войдите в портал toohello.</span><span class="sxs-lookup"><span data-stu-id="8be39-138">In hello Azure portal, log in toohello portal.</span></span>

6. <span data-ttu-id="8be39-139">Убедитесь, что вы находитесь в режиме управления службами:</span><span class="sxs-lookup"><span data-stu-id="8be39-139">Make sure you are in Service Management mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

7. <span data-ttu-id="8be39-140">Завершите работу виртуальной Машины, которая уже удалена hello.</span><span class="sxs-lookup"><span data-stu-id="8be39-140">Shut down hello VM that is already deprovisioned.</span></span> <span data-ttu-id="8be39-141">Hello следующий пример завершает работу виртуальной Машины с именем hello `myVM`:</span><span class="sxs-lookup"><span data-stu-id="8be39-141">hello following example shuts down hello VM named `myVM`:</span></span>

    ```azurecli
    azure vm shutdown myVM
    ```
   <span data-ttu-id="8be39-142">При необходимости можно просмотреть список всех hello виртуальные машины создаются в подписке с помощью`azure vm list`</span><span class="sxs-lookup"><span data-stu-id="8be39-142">If needed, you can view a list all hello VMs created in your subscription by using `azure vm list`</span></span>

   > [!NOTE]
   > <span data-ttu-id="8be39-143">Если вы используете hello портал Azure, выберите hello виртуальной Машины и нажмите кнопку **остановить** завершение работы виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="8be39-143">If you're using hello Azure portal, select hello VM and click **Stop** to shut down hello VM.</span></span>

8. <span data-ttu-id="8be39-144">При остановке hello ВМ образа hello.</span><span class="sxs-lookup"><span data-stu-id="8be39-144">When hello VM is stopped, capture hello image.</span></span> <span data-ttu-id="8be39-145">Следующий пример получает Hello hello виртуальной Машины с именем `myVM` и создает обобщенный образ с именем `myNewVM`:</span><span class="sxs-lookup"><span data-stu-id="8be39-145">hello following example captures hello VM named `myVM` and creates a generalized image named `myNewVM`:</span></span>

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    <span data-ttu-id="8be39-146">Hello `-t` подкоманда удалений hello исходной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8be39-146">hello `-t` subcommand deletes hello original virtual machine.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8be39-147">В hello портал Azure, можно записать образ, выбрав **изображения** меню hello концентратора.</span><span class="sxs-lookup"><span data-stu-id="8be39-147">In hello Azure portal, you can capture an image by selecting **Image** from hello hub menu.</span></span> <span data-ttu-id="8be39-148">Требуется toosupply hello следующую информацию для образа hello: имя группы ресурсов, расположение, тип операционной системы и путь к хранилищу больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="8be39-148">You need toosupply hello following information for hello image: name, resource group, location, operating system type, and storage blob path.</span></span>

9. <span data-ttu-id="8be39-149">Hello новый образ будет теперь доступны в списке изображений, которые могут быть hello используются tooconfigure любой новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8be39-149">hello new image is now available in hello list of images that can be used tooconfigure any new VM.</span></span> <span data-ttu-id="8be39-150">Вы можете просмотреть с помощью команды hello:</span><span class="sxs-lookup"><span data-stu-id="8be39-150">You can view it with hello command:</span></span>

   ```azurecli
   azure vm image list
   ```

   <span data-ttu-id="8be39-151">На hello [портал Azure](http://portal.azure.com), hello новое изображение отображается в hello **образов виртуальных Машин (классические)** , принадлежит toohello **вычислений** служб.</span><span class="sxs-lookup"><span data-stu-id="8be39-151">On hello [Azure portal](http://portal.azure.com), hello new image appears in hello **VM images (classic)** that belongs toohello **Compute** services.</span></span> <span data-ttu-id="8be39-152">Вы можете получить доступ к **образов виртуальных Машин (классические)** , щелкнув _дополнительные службы_ внизу hello hello Azure службы списка и затем проверив hello **вычислений** служб.</span><span class="sxs-lookup"><span data-stu-id="8be39-152">You can access **VM images (classic)** by clicking _More services_ at hello bottom of hello Azure service list, and then looking in hello **Compute** services.</span></span>   

   ![Успешная запись образа](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="8be39-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8be39-154">Next steps</span></span>
<span data-ttu-id="8be39-155">изображение Hello является toocreate готовности toobe использовать виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="8be39-155">hello image is ready toobe used toocreate VMs.</span></span> <span data-ttu-id="8be39-156">Можно использовать команду hello Azure CLI `azure vm create` и вы создали имя образа hello питания.</span><span class="sxs-lookup"><span data-stu-id="8be39-156">You can use hello Azure CLI command `azure vm create` and supply hello image name you created.</span></span> <span data-ttu-id="8be39-157">Дополнительные сведения см. в разделе [использование hello Azure CLI классической модели развертывания](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="8be39-157">For more information, see [Using hello Azure CLI with Classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

<span data-ttu-id="8be39-158">Можно также использовать hello [портал Azure](http://portal.azure.com) toocreate пользовательских виртуальных Машин с помощью hello **изображения** метод и выбрав hello образ был создан.</span><span class="sxs-lookup"><span data-stu-id="8be39-158">Alternatively, use hello [Azure portal](http://portal.azure.com) toocreate a custom VM by using hello **Image** method and selecting hello image you created.</span></span> <span data-ttu-id="8be39-159">Дополнительные сведения см. в разделе [как tooCreate специальной виртуальной Машины][How tooCreate a Custom Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="8be39-159">For more information, see [How tooCreate a Custom VM][How tooCreate a Custom Virtual Machine].</span></span>

<span data-ttu-id="8be39-160">**См. также:** [Руководство пользователя агента Linux для Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8be39-160">**See also:** [Azure Linux Agent User Guide](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How tooCreate a Custom Virtual Machine]:create-custom.md
[How tooAttach a Data Disk tooa Virtual Machine]:attach-disk.md
[How tooCreate a Linux Virtual Machine]:create-custom.md
