---
title: "на основе образа Azure RemoteApp на Виртуальной машине Azure aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate изображения для Azure RemoteApp с помощью виртуальной машины Azure."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d41583ef-6cd8-4115-8dcb-b2cd5b3d301a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 2d432bcb15be68a2946d91b5f36f41d980726338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a><span data-ttu-id="3375e-103">Создание образа Azure RemoteApp на основе виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="3375e-103">Create a Azure RemoteApp image based on an Azure virtual machine</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3375e-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="3375e-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3375e-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="3375e-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3375e-106">Можно создать образы Azure RemoteApp (которые содержат приложения hello, отправляемого в коллекции) из виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="3375e-106">You can create Azure RemoteApp images (which hold hello apps you share in your collection) from an Azure virtual machine.</span></span> <span data-ttu-id="3375e-107">Можно также выбрать toouse образ виртуальной машины, мы добавили коллекции образов виртуальных Машин Azure toohello, соответствующий всем требованиям образ Azure RemoteApp hello - можно использовать этот образ виртуальной Машины в качестве отправной точки для ВМ, если требуется.</span><span class="sxs-lookup"><span data-stu-id="3375e-107">You could also choose toouse a virtual machine image we added toohello Azure VM image gallery that meets all hello Azure RemoteApp image requirements - you can use that VM image as a starting point for your own VM, if you want.</span></span> <span data-ttu-id="3375e-108">Просто найти образ «Удаленный рабочий стол узла сеансов Windows Server» hello в библиотеке hello.</span><span class="sxs-lookup"><span data-stu-id="3375e-108">Just look for hello "Windows Server Remote Desktop Session Host" image in hello library.</span></span>

<span data-ttu-id="3375e-109">Существует два toocreate действия на основе собственного образа на Виртуальной машине Azure — создать образ hello, а затем передать его из tooAzure библиотеки hello виртуальной Машины Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="3375e-109">There are two steps toocreate your own image based on an Azure VM - create hello image and then upload it from hello Azure VM library tooAzure RemoteApp.</span></span>

## <a name="create-a-custom-image-based-on-an-azure-vm"></a><span data-ttu-id="3375e-110">Создание пользовательского образа на основе виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="3375e-110">Create a custom image based on an Azure VM</span></span>
<span data-ttu-id="3375e-111">Используйте эти шаги toocreate изображения на Виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="3375e-111">Use these steps toocreate an image based on an Azure VM.</span></span>

1. <span data-ttu-id="3375e-112">Создайте виртуальную машину Azure.</span><span class="sxs-lookup"><span data-stu-id="3375e-112">Create an Azure virtual machine.</span></span> <span data-ttu-id="3375e-113">Можно использовать hello «Удаленный рабочий стол узла сеансов Windows Server» или «Windows Server удаленного рабочего стола сеанса узла с Microsoft Office 365 профессиональный плюс» image hello из коллекции образов виртуальных машин Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3375e-113">You can use hello "Windows Server Remote Desktop Session Host" or hello "Windows Server Remote Desktop Session Host with Microsoft Office 365 ProPlus" image from hello Azure virtual machine image gallery.</span></span> <span data-ttu-id="3375e-114">Этот образ требованиям всех hello Azure RemoteApp шаблона изображения.</span><span class="sxs-lookup"><span data-stu-id="3375e-114">This image meets all hello Azure RemoteApp template image requirements.</span></span>
   
    <span data-ttu-id="3375e-115">Дополнительные сведения см. в статье [Создание первой виртуальной машины Windows на портале Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3375e-115">For details, see [Create a VM running Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="3375e-116">Подключение toohello ВМ и установить и настроить приложения hello, что требуется tooshare через RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="3375e-116">Connect toohello VM and install and configure hello apps that you want tooshare through RemoteApp.</span></span> <span data-ttu-id="3375e-117">Убедитесь, что tooperform все дополнительные конфигурации Windows, необходимые для приложения.</span><span class="sxs-lookup"><span data-stu-id="3375e-117">Make sure tooperform any additional Windows configurations required by your apps.</span></span>
   
    <span data-ttu-id="3375e-118">Дополнительные сведения см. в разделе [как tooLog на виртуальной машине под управлением Windows Server tooa](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3375e-118">For details, see [How tooLog on tooa Virtual Machine Running Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
3. <span data-ttu-id="3375e-119">При использовании одного из образов hello узла сеансов удаленных рабочих столов Windows Server, является сценарий включены проверки, который обеспечит соответствие виртуальной Машины hello RemoteApp pre-reqs.</span><span class="sxs-lookup"><span data-stu-id="3375e-119">If you are using one of hello Windows Server Remote Desktop Session Host images, there is an included validation script that will ensure your VM meets hello RemoteApp pre-reqs.</span></span> <span data-ttu-id="3375e-120">сценарий toorun дважды щелкните **ValidateRemoteAppImage** на рабочем столе hello.</span><span class="sxs-lookup"><span data-stu-id="3375e-120">toorun script, double-click **ValidateRemoteAppImage** on hello desktop.</span></span> <span data-ttu-id="3375e-121">Убедитесь, что все ошибки, о которых сообщает скрипт hello имеют фиксированную перед продолжением toohello следующий шаг.</span><span class="sxs-lookup"><span data-stu-id="3375e-121">Ensure that all errors reported by hello script are fixed before proceeding toohello next step.</span></span>
4. <span data-ttu-id="3375e-122">SYSPREP обобщения и записи образа hello.</span><span class="sxs-lookup"><span data-stu-id="3375e-122">SYSPREP generalize and capture hello image.</span></span> <span data-ttu-id="3375e-123">В разделе [как tooCapture tooUse виртуальной машине Windows, как шаблон](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) инструкции.</span><span class="sxs-lookup"><span data-stu-id="3375e-123">See [How tooCapture a Windows Virtual Machine tooUse as a Template](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) for instructions.</span></span>

## <a name="import-hello-image-into-hello-azure-remoteapp-image-library"></a><span data-ttu-id="3375e-124">Импорт изображения hello библиотека изображений hello Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="3375e-124">Import hello image into hello Azure RemoteApp image library</span></span>
<span data-ttu-id="3375e-125">Используйте эти шаги tooimport hello образ в Azure RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="3375e-125">Use these steps tooimport hello new image into Azure RemoteApp:</span></span>

1. <span data-ttu-id="3375e-126">В hello **образы шаблонов** вкладки:</span><span class="sxs-lookup"><span data-stu-id="3375e-126">In hello **Template Images** tab:</span></span>
   
   * <span data-ttu-id="3375e-127">если у вас нет образов, щелкните **Загрузить или импортировать образ шаблона**;</span><span class="sxs-lookup"><span data-stu-id="3375e-127">If you have no existing images, click **Upload or Import a Template Image**.</span></span>
   * <span data-ttu-id="3375e-128">Если у вас уже есть по крайней мере один образ, нажмите кнопку  **+**  tooadd новый образ.</span><span class="sxs-lookup"><span data-stu-id="3375e-128">If you have at least one image already, click **+** tooadd a new image.</span></span>
2. <span data-ttu-id="3375e-129">Выберите библиотеку **Импортировать образ из библиотеки виртуальных машин** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3375e-129">Select **Import an image from your Virtual Machines** library, and then click **Next**.</span></span>
3. <span data-ttu-id="3375e-130">На следующей странице приветствия выберите образ из списка hello и убедитесь, что вы выполнили шаги hello, указанные при создании образа.</span><span class="sxs-lookup"><span data-stu-id="3375e-130">On hello next page, select your custom image from hello list and confirm that you followed hello steps listed when you created your image.</span></span> <span data-ttu-id="3375e-131">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3375e-131">Click **Next**.</span></span>
4. <span data-ttu-id="3375e-132">Введите имя для нового образа RemoteApp hello и выберите расположение hello, а затем нажмите кнопку Импорт hello флажок toostart hello.</span><span class="sxs-lookup"><span data-stu-id="3375e-132">Enter a name for hello new RemoteApp image and pick hello location, then click hello checkmark toostart hello import process.</span></span>

> [!NOTE]
> <span data-ttu-id="3375e-133">Изображения можно импортировать из любого расположения Azure, поддерживаются в виртуальных машинах Azure tooany расположение Azure, поддерживаемые Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="3375e-133">You can import images from any Azure location supported by Azure Virtual Machines tooany Azure location supported by Azure RemoteApp.</span></span> <span data-ttu-id="3375e-134">В зависимости от расположения hello hello импорта может занять too25 минут.</span><span class="sxs-lookup"><span data-stu-id="3375e-134">Depending on hello locations hello import can take up too25 minutes.</span></span>
> 
> 

<span data-ttu-id="3375e-135">Теперь вы готовы toocreate новой коллекции, либо [облака](remoteapp-create-cloud-deployment.md) коллекции или [гибридных](remoteapp-create-hybrid-deployment.md), в зависимости от потребностей.</span><span class="sxs-lookup"><span data-stu-id="3375e-135">Now you are ready toocreate your new collection, either a [cloud](remoteapp-create-cloud-deployment.md) collection or [hybrid](remoteapp-create-hybrid-deployment.md), depending on your needs.</span></span>

