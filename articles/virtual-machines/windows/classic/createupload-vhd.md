---
title: "изображений с aaaCreate и отправки виртуальной Машины с помощью Powershell | Документы Microsoft"
description: "Узнайте toocreate и отправить обобщенный образа Windows Server (VHD) с помощью hello классической модели развертывания и Azure Powershell."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8c4a08fe-7714-4bf0-be87-c728a7806d3f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: 093b57c9157cea5f348c8ba02b5700c917adbcdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-windows-server-vhd-tooazure"></a><span data-ttu-id="2c7e9-103">Создание и отправка tooAzure виртуального жесткого диска Windows Server</span><span class="sxs-lookup"><span data-stu-id="2c7e9-103">Create and upload a Windows Server VHD tooAzure</span></span>
<span data-ttu-id="2c7e9-104">В этой статье показано, как tooupload ВМ обобщенный образ как виртуальный жесткий диск (VHD) чтобы вы могли использовать toocreate виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-104">This article shows you how tooupload your own generalized VM image as a virtual hard disk (VHD) so you can use it toocreate virtual machines.</span></span> <span data-ttu-id="2c7e9-105">Дополнительные сведения о дисках и виртуальных жестких дисках в Microsoft Azure см. в статье [О дисках и виртуальных жестких дисках для виртуальных машин](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c7e9-105">For more details about disks and VHDs in Microsoft Azure, see [About Disks and VHDs for Virtual Machines](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c7e9-106">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2c7e9-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2c7e9-107">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="2c7e9-108">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="2c7e9-109">Вы также можете [отправить](../upload-generalized-managed.md) виртуальную машину, используя модель hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-109">You can also [upload](../upload-generalized-managed.md) a virtual machine using hello Resource Manager model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c7e9-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2c7e9-110">Prerequisites</span></span>
<span data-ttu-id="2c7e9-111">В этой статье предполагается, что у вас есть следующие компоненты.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-111">This article assumes you have:</span></span>

* <span data-ttu-id="2c7e9-112">**Подписка Azure.** Если подписка отсутствует, можно [создать учетную запись Azure бесплатно](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="2c7e9-112">**An Azure subscription** - If you don't have one, you can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
* <span data-ttu-id="2c7e9-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)**  -у вас есть hello Microsoft Azure PowerShell модуль установлен и настроен toouse вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)** - You have hello Microsoft Azure PowerShell module installed and configured toouse your subscription.</span></span>
* <span data-ttu-id="2c7e9-114">**ОБЪЕКТ. VHD-файл** — поддерживаемые версии операционной системы, хранящиеся в VHD-файл и вложенные tooa виртуальной машины Windows.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-114">**A .VHD file** - supported Windows operating system stored in a .vhd file and attached tooa virtual machine.</span></span> <span data-ttu-id="2c7e9-115">Проверьте toosee Если hello серверных ролей на hello виртуального жесткого диска поддерживаются Sysprep.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-115">Check toosee if hello server roles running on hello VHD are supported by Sysprep.</span></span> <span data-ttu-id="2c7e9-116">Дополнительные сведения см. в разделе [Поддержка ролей сервера в Sysprep](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="2c7e9-116">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2c7e9-117">Hello формат VHDX не поддерживается в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-117">hello VHDX format is not supported in Microsoft Azure.</span></span> <span data-ttu-id="2c7e9-118">Вы можете преобразовать формат tooVHD hello диска, с помощью диспетчера Hyper-V или hello [командлет Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c7e9-118">You can convert hello disk tooVHD format using Hyper-V Manager or hello [Convert-VHD cmdlet](http://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="2c7e9-119">Дополнительные сведения см. в [этом блоге](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c7e9-119">For details, see this [blogpost](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span></span>

## <a name="step-1-prep-hello-vhd"></a><span data-ttu-id="2c7e9-120">Шаг 1: Подготовьте hello виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="2c7e9-120">Step 1: Prep hello VHD</span></span>
<span data-ttu-id="2c7e9-121">Перед отправкой tooAzure hello виртуального жесткого диска, он должен toobe обобщить с помощью средства Sysprep hello.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-121">Before you upload hello VHD tooAzure, it needs toobe generalized by using hello Sysprep tool.</span></span> <span data-ttu-id="2c7e9-122">Это подготавливает toobe hello виртуального жесткого диска, используемое в качестве изображения.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-122">This prepares hello VHD toobe used as an image.</span></span> <span data-ttu-id="2c7e9-123">Дополнительные сведения о программе Sysprep см. в разделе [как tooUse Sysprep: введение](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c7e9-123">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span> <span data-ttu-id="2c7e9-124">Резервное копирование hello виртуальной Машины перед запуском Sysprep.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-124">Back up hello VM before running Sysprep.</span></span>

<span data-ttu-id="2c7e9-125">С помощью hello виртуальную машину, которая hello операционной системы был установлен для завершения процедуры hello:</span><span class="sxs-lookup"><span data-stu-id="2c7e9-125">From hello virtual machine that hello operating system was installed to, complete hello following procedure:</span></span>

1. <span data-ttu-id="2c7e9-126">Войдите в toohello операционной системы.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-126">Sign in toohello operating system.</span></span>
2. <span data-ttu-id="2c7e9-127">Откройте окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-127">Open a command prompt window as an administrator.</span></span> <span data-ttu-id="2c7e9-128">Измените каталог hello слишком**%windir%\system32\sysprep**, а затем запустите `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-128">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>

    ![Откройте окно командной строки.](./media/createupload-vhd/sysprep_commandprompt.png)
3. <span data-ttu-id="2c7e9-130">Hello **средство подготовки системы** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-130">hello **System Preparation Tool** dialog box appears.</span></span>

   ![Запуск Sysprep](./media/createupload-vhd/sysprepgeneral.png)
4. <span data-ttu-id="2c7e9-132">В hello **средство подготовки системы**выберите **переход в окно приветствия системы (OOBE)** и убедитесь, что **Generalize** проверяется.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-132">In hello **System Preparation Tool**, select **Enter System Out of Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span>
5. <span data-ttu-id="2c7e9-133">В разделе **Параметры завершения работы** выберите **Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-133">In **Shutdown Options**, select **Shutdown**.</span></span>
6. <span data-ttu-id="2c7e9-134">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-134">Click **OK**.</span></span>

## <a name="step-2-create-a-storage-account-and-a-container"></a><span data-ttu-id="2c7e9-135">Шаг 2. Создание учетной записи хранения и контейнера</span><span class="sxs-lookup"><span data-stu-id="2c7e9-135">Step 2: Create a storage account and a container</span></span>
<span data-ttu-id="2c7e9-136">Необходимо учетной записи хранилища в Azure, чтобы у вас есть место tooupload hello VHD-файл.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-136">You need a storage account in Azure so you have a place tooupload hello .vhd file.</span></span> <span data-ttu-id="2c7e9-137">В этом шаге показано, как toocreate учетную запись или get hello сведения из существующей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-137">This step shows you how toocreate an account, or get hello info you need from an existing account.</span></span> <span data-ttu-id="2c7e9-138">Замените переменные hello в &lsaquo; скобки &rsaquo; со своих собственных сведений.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-138">Replace hello variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

1. <span data-ttu-id="2c7e9-139">Вход</span><span class="sxs-lookup"><span data-stu-id="2c7e9-139">Login</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="2c7e9-140">Настройте свою подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-140">Set your Azure subscription.</span></span>

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. <span data-ttu-id="2c7e9-141">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-141">Create a new storage account.</span></span> <span data-ttu-id="2c7e9-142">Имя Hello hello учетной записи хранения должно быть уникальным, 3 до 24 символов.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-142">hello name of hello storage account should be unique, 3-24 characters.</span></span> <span data-ttu-id="2c7e9-143">Hello имя может быть любым сочетанием букв и цифр.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-143">hello name can be any combination of letters and numbers.</span></span> <span data-ttu-id="2c7e9-144">Необходимо также toospecify местоположение, например «East US»</span><span class="sxs-lookup"><span data-stu-id="2c7e9-144">You also need toospecify a location like "East US"</span></span>

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. <span data-ttu-id="2c7e9-145">Установить hello новой учетной записи хранения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-145">Set hello new storage account as hello default.</span></span>

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. <span data-ttu-id="2c7e9-146">Создайте новый контейнер.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-146">Create a new container.</span></span>

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-hello-vhd-file"></a><span data-ttu-id="2c7e9-147">Шаг 3: Отправка hello VHD-файл</span><span class="sxs-lookup"><span data-stu-id="2c7e9-147">Step 3: Upload hello .vhd file</span></span>
<span data-ttu-id="2c7e9-148">Используйте hello [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) tooupload hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-148">Use hello [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) tooupload hello VHD.</span></span>

<span data-ttu-id="2c7e9-149">Из окна Azure PowerShell hello, используемый в предыдущем шаге hello, тип hello следующую команду и замените переменные hello в &lsaquo; скобки &rsaquo; со своих собственных сведений.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-149">From hello Azure PowerShell window you used in hello previous step, type hello following command and replace hello variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-hello-image-tooyour-list-of-custom-images"></a><span data-ttu-id="2c7e9-150">Шаг 4: Добавление hello изображения tooyour список пользовательских образов</span><span class="sxs-lookup"><span data-stu-id="2c7e9-150">Step 4: Add hello image tooyour list of custom images</span></span>
<span data-ttu-id="2c7e9-151">Используйте hello [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) командлет tooadd hello изображения toohello список пользовательских образов.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-151">Use hello [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) cmdlet tooadd hello image toohello list of your custom images.</span></span>

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a><span data-ttu-id="2c7e9-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2c7e9-152">Next steps</span></span>
<span data-ttu-id="2c7e9-153">Теперь вы можете [Создание пользовательской виртуальной Машины](createportal.md) загружен с помощью hello образа.</span><span class="sxs-lookup"><span data-stu-id="2c7e9-153">You can now [create a custom VM](createportal.md) using hello image you uploaded.</span></span>
