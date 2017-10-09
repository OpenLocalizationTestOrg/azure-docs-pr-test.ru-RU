---
title: "aaaCapture образ виртуальной Машины Windows Azure | Документы Microsoft"
description: "Запись образа виртуальной машины Microsoft Azure, созданных с помощью hello классической модели развертывания."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: a5986eac-4cf3-40bd-9b79-7c811806b880
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: b9bbc437012aa44295f90941c9d72e39509df28f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-hello-classic-deployment-model"></a><span data-ttu-id="b7274-103">Запись образа виртуальной машины Microsoft Azure, созданных с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="b7274-103">Capture an image of an Azure Windows virtual machine created with hello classic deployment model.</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b7274-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b7274-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b7274-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="b7274-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="b7274-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b7274-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="b7274-107">Сведения о модели диспетчера ресурсов см. в разделе [Запись управляемого образа универсальной виртуальной машины в Azure](../capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="b7274-107">For Resource Manager model information, see [Capture a managed image of a generalized VM in Azure](../capture-image-resource.md).</span></span>

<span data-ttu-id="b7274-108">В этой статье показано, как toocapture виртуальной машине Azure под управлением Windows, ее можно использовать в качестве образа toocreate других виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b7274-108">This article shows you how toocapture an Azure virtual machine running Windows so you can use it as an image toocreate other virtual machines.</span></span> <span data-ttu-id="b7274-109">Этот образ содержит hello диска операционной системы и диски с данными, которые являются присоединенного toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b7274-109">This image includes hello operating system disk and any data disks that are attached toohello virtual machine.</span></span> <span data-ttu-id="b7274-110">Они не включают конфигурации сети, поэтому вам понадобится tooset конфигурации сети, при создании других виртуальных машин, использующих изображения hello hello.</span><span class="sxs-lookup"><span data-stu-id="b7274-110">It doesn't include networking configurations, so you'll need tooset up network configurations when you create hello other virtual machines that use hello image.</span></span>

<span data-ttu-id="b7274-111">Хранилища Azure hello образ в столбце **образов виртуальных Машин (классические)**, **вычислений** службу, которая отображается при просмотре всех hello служб Azure.</span><span class="sxs-lookup"><span data-stu-id="b7274-111">Azure stores hello image under **VM images (classic)**, a **Compute** service that is listed when you view all hello Azure services.</span></span> <span data-ttu-id="b7274-112">Это hello же месте, где хранятся все отправленные образы.</span><span class="sxs-lookup"><span data-stu-id="b7274-112">This is hello same place where any images you've uploaded are stored.</span></span> <span data-ttu-id="b7274-113">Дополнительные сведения об образах см. в разделе [Об образах виртуальных машин](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b7274-113">For details about images, see [About images for virtual machines](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b7274-114">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="b7274-114">Before you begin</span></span>
<span data-ttu-id="b7274-115">Эти шаги предполагают, что уже создана виртуальная машина Azure и настроить hello операционной системы, включая присоединение диски с данными.</span><span class="sxs-lookup"><span data-stu-id="b7274-115">These steps assume that you've already created an Azure virtual machine and configured hello operating system, including attaching any data disks.</span></span> <span data-ttu-id="b7274-116">Если вы еще не сделали это, см. следующие статьи для получения сведений о создании и Подготовка виртуальной машины hello hello:</span><span class="sxs-lookup"><span data-stu-id="b7274-116">If you haven't done this yet, see hello following articles for information on creating and preparing hello virtual machine:</span></span>

* [<span data-ttu-id="b7274-117">Создание виртуальной машины из образа</span><span class="sxs-lookup"><span data-stu-id="b7274-117">Create a virtual machine from an image</span></span>](createportal.md)
* [<span data-ttu-id="b7274-118">Как tooattach данных на диске tooa виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="b7274-118">How tooattach a data disk tooa virtual machine</span></span>](attach-disk.md)
* <span data-ttu-id="b7274-119">Убедитесь, что ролей сервера hello поддерживается с помощью средства Sysprep.</span><span class="sxs-lookup"><span data-stu-id="b7274-119">Make sure hello server roles are supported with Sysprep.</span></span> <span data-ttu-id="b7274-120">Дополнительные сведения см. в разделе [Поддержка ролей сервера в Sysprep](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="b7274-120">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

> [!WARNING]
> <span data-ttu-id="b7274-121">Этот процесс удаляет hello исходной виртуальной машины, после его снятия.</span><span class="sxs-lookup"><span data-stu-id="b7274-121">This process deletes hello original virtual machine after it's captured.</span></span>
>
>

<span data-ttu-id="b7274-122">Предыдущий toocapturing образа виртуальной машины Azure рекомендуется hello целевая виртуальная машина резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="b7274-122">Prior toocapturing an image of an Azure virtual machine, it is recommended hello target virtual machine be backed up.</span></span> <span data-ttu-id="b7274-123">Это можно сделать с помощью службы архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="b7274-123">Azure virtual machines can be backed up using Azure Backup.</span></span> <span data-ttu-id="b7274-124">Дополнительные сведения см. в статье [Архивация виртуальных машин Azure](../../../backup/backup-azure-vms.md).</span><span class="sxs-lookup"><span data-stu-id="b7274-124">For details, see [Back up Azure virtual machines](../../../backup/backup-azure-vms.md).</span></span> <span data-ttu-id="b7274-125">Доступны другие решения от сертифицированных партнеров.</span><span class="sxs-lookup"><span data-stu-id="b7274-125">Other solutions are available from certified partners.</span></span> <span data-ttu-id="b7274-126">toofind о том, что в настоящее время недоступно, найдите hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b7274-126">toofind out what’s currently available, search hello Azure Marketplace.</span></span>

## <a name="capture-hello-virtual-machine"></a><span data-ttu-id="b7274-127">Запись hello виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="b7274-127">Capture hello virtual machine</span></span>
1. <span data-ttu-id="b7274-128">В hello [портал Azure](http://portal.azure.com), **Connect** toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b7274-128">In hello [Azure portal](http://portal.azure.com), **Connect** toohello virtual machine.</span></span> <span data-ttu-id="b7274-129">Инструкции см. в разделе [как toosign tooa виртуальной машине под управлением Windows Server][How toosign in tooa virtual machine running Windows Server].</span><span class="sxs-lookup"><span data-stu-id="b7274-129">For instructions, see [How toosign in tooa virtual machine running Windows Server][How toosign in tooa virtual machine running Windows Server].</span></span>
2. <span data-ttu-id="b7274-130">Откройте окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="b7274-130">Open a Command Prompt window as an administrator.</span></span>
3. <span data-ttu-id="b7274-131">Измените каталог hello слишком`%windir%\system32\sysprep`, а затем запустите sysprep.exe.</span><span class="sxs-lookup"><span data-stu-id="b7274-131">Change hello directory too`%windir%\system32\sysprep`, and then run sysprep.exe.</span></span>
4. <span data-ttu-id="b7274-132">Hello **средство подготовки системы** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="b7274-132">hello **System Preparation Tool** dialog box appears.</span></span> <span data-ttu-id="b7274-133">Здравствуйте, следующие:</span><span class="sxs-lookup"><span data-stu-id="b7274-133">Do hello following:</span></span>

   * <span data-ttu-id="b7274-134">В разделе **Действие по очистке системы** выберите **Запуск при первом включении компьютера (OOBE)** и убедитесь, что установлен флажок **Обобщить**.</span><span class="sxs-lookup"><span data-stu-id="b7274-134">In **System Cleanup Action**, select **Enter System Out-of-Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span> <span data-ttu-id="b7274-135">Дополнительные сведения об использовании Sysprep см. в разделе [как tooUse Sysprep: введение][How tooUse Sysprep: An Introduction].</span><span class="sxs-lookup"><span data-stu-id="b7274-135">For more information about using Sysprep, see [How tooUse Sysprep: An Introduction][How tooUse Sysprep: An Introduction].</span></span>
   * <span data-ttu-id="b7274-136">В разделе **Параметры завершения работы** выберите **Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="b7274-136">In **Shutdown Options**, select **Shutdown**.</span></span>
   * <span data-ttu-id="b7274-137">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b7274-137">Click **OK**.</span></span>

   ![Запуск Sysprep](./media/capture-image/SysprepGeneral.png)
5. <span data-ttu-id="b7274-139">Sysprep завершает работу виртуальной машины hello, изменяющая состояние hello hello виртуальной машины в Azure portal hello слишком**остановлена**.</span><span class="sxs-lookup"><span data-stu-id="b7274-139">Sysprep shuts down hello virtual machine, which changes hello status of hello virtual machine in hello Azure portal too**Stopped**.</span></span>
6. <span data-ttu-id="b7274-140">В hello портал Azure, щелкните **виртуальные машины (классические)** и выберите hello виртуальную машину будет toocapture.</span><span class="sxs-lookup"><span data-stu-id="b7274-140">In hello Azure portal, click **Virtual Machines (classic)** and select hello virtual machine you want toocapture.</span></span> <span data-ttu-id="b7274-141">Hello **образов виртуальных Машин (классические)** группа указана в разделе **вычислений** при просмотре **дополнительные службы**.</span><span class="sxs-lookup"><span data-stu-id="b7274-141">hello **VM images (classic)** group is listed under **Compute** when you view **More services**.</span></span>

7. <span data-ttu-id="b7274-142">На панели команд hello, нажмите кнопку **записи**.</span><span class="sxs-lookup"><span data-stu-id="b7274-142">On hello command bar, click **Capture**.</span></span>

   ![Запись виртуальной машины](./media/capture-image/CaptureVM.png)

   <span data-ttu-id="b7274-144">Hello **hello записи виртуальной машины** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="b7274-144">hello **Capture hello Virtual Machine** dialog box appears.</span></span>

8. <span data-ttu-id="b7274-145">В **имя образа**, введите имя для нового образа hello.</span><span class="sxs-lookup"><span data-stu-id="b7274-145">In **Image name**, type a name for hello new image.</span></span> <span data-ttu-id="b7274-146">В **метка образа**, введите метку для нового образа hello.</span><span class="sxs-lookup"><span data-stu-id="b7274-146">In **Image label**, type a label for hello new image.</span></span>

9. <span data-ttu-id="b7274-147">Нажмите кнопку **запущено средство Sysprep на виртуальной машине hello**.</span><span class="sxs-lookup"><span data-stu-id="b7274-147">Click **I've run Sysprep on hello virtual machine**.</span></span> <span data-ttu-id="b7274-148">Этот флажок указывает toohello действия с помощью средства Sysprep в шагах 3 – 5.</span><span class="sxs-lookup"><span data-stu-id="b7274-148">This checkbox refers toohello actions with Sysprep in steps 3-5.</span></span> <span data-ttu-id="b7274-149">Изображение _должен_ обобщить, запустив программу Sysprep перед добавлением Windows Server tooyour набор пользовательских образов.</span><span class="sxs-lookup"><span data-stu-id="b7274-149">An image _must_ be generalized by running Sysprep before you add a Windows Server image tooyour set of custom images.</span></span>

10. <span data-ttu-id="b7274-150">После завершения записи hello hello новый образ не станет доступным в hello **Marketplace**, в hello **вычислений**, **образов виртуальных Машин (классические)** контейнера.</span><span class="sxs-lookup"><span data-stu-id="b7274-150">Once hello capture completes, hello new image becomes available in hello **Marketplace**, in hello **Compute**, **VM images (classic)** container.</span></span>

    ![Успешная запись образа](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="b7274-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b7274-152">Next steps</span></span>
<span data-ttu-id="b7274-153">изображение Hello — Готово toobe используется toocreate виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b7274-153">hello image is ready toobe used toocreate virtual machines.</span></span> <span data-ttu-id="b7274-154">toodo это, вы создадите виртуальную машину, выбрав hello **дополнительные службы** пункта меню hello нижней части меню служб hello, затем **образов виртуальных Машин (классические)** в hello **вычислений**группы.</span><span class="sxs-lookup"><span data-stu-id="b7274-154">toodo this, you'll create a virtual machine by selecting hello **More services** menu item at hello bottom of hello services menu, then **VM images (classic)** in hello **Compute** group.</span></span> <span data-ttu-id="b7274-155">Инструкции см. в статье [Создание виртуальной машины из образа](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="b7274-155">For instructions, see [Create a virtual machine from an image](createportal.md).</span></span>

[How toosign in tooa virtual machine running Windows Server]:connect-logon.md
[How tooUse Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: ./media/capture-image/SysprepGeneral.png
[hello virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of hello virtual machine]: ./media/capture-image/CaptureVM.png
[Enter hello image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use hello captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png
