---
title: "требования изображения RemoteApp aaaAzure | Документы Microsoft"
description: "Дополнительные сведения о hello требования для создания образов toobe использовать Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7cbb90f4-6dc9-462c-a429-088cdb57414e
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 4e35203eb93a866d4e0bd591d42b34746c7ffa4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a><span data-ttu-id="3ea2a-103">Требования к образам Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="3ea2a-103">Requirements for Azure RemoteApp images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3ea2a-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="3ea2a-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3ea2a-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="3ea2a-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3ea2a-106">Azure RemoteApp использует toohost образа Windows Server 2012 R2 все программы hello требуется tooshare с вашими пользователями.</span><span class="sxs-lookup"><span data-stu-id="3ea2a-106">Azure RemoteApp uses a Windows Server 2012 R2 image toohost all hello programs that you want tooshare with your users.</span></span> <span data-ttu-id="3ea2a-107">toocreate пользовательского образа, можно начать с существующего образа или [создайте новую](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="3ea2a-107">toocreate a custom image, you can start with an existing image or [create a new one](remoteapp-create-custom-image.md).</span></span>

> [!TIP]
> <span data-ttu-id="3ea2a-108">Вы знаете hello, к Azure RemoteApp подписки обеспечивает доступ tooa образа Windows Server 2012 R2 в коллекции виртуальных Машин Azure, которые можно использовать toocreate образ шаблона?</span><span class="sxs-lookup"><span data-stu-id="3ea2a-108">Did you know that your Azure RemoteApp subscription gives you access tooa Windows Server 2012 R2 image in hello Azure VM gallery that you can use toocreate your own template image?</span></span> <span data-ttu-id="3ea2a-109">[Узнайте об этом подробнее](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="3ea2a-109">[Check it out](remoteapp-image-on-azurevm.md).</span></span>  
> 
> 

<span data-ttu-id="3ea2a-110">Существуют следующие требования Hello для hello образ, который можно загрузить для использования с Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="3ea2a-110">hello requirements for hello image that can be uploaded for use with Azure RemoteApp are:</span></span>

* <span data-ttu-id="3ea2a-111">Пользовательские приложения не хранить данные локально на изображении hello.</span><span class="sxs-lookup"><span data-stu-id="3ea2a-111">Custom applications don’t store data locally on hello image.</span></span> <span data-ttu-id="3ea2a-112">Эти образы не имеют состояний и должны содержать только приложения.</span><span class="sxs-lookup"><span data-stu-id="3ea2a-112">These images are stateless and should only contain applications.</span></span>
* <span data-ttu-id="3ea2a-113">изображение Hello не содержит данных, которые могут быть потеряны.</span><span class="sxs-lookup"><span data-stu-id="3ea2a-113">hello image does not contain data that can be lost.</span></span>
* <span data-ttu-id="3ea2a-114">размер образа Hello должно быть кратно МБ.</span><span class="sxs-lookup"><span data-stu-id="3ea2a-114">hello image size should be a multiple of MBs.</span></span> <span data-ttu-id="3ea2a-115">При попытке tooupload изображение, которое не является точным кратным hello отправка завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="3ea2a-115">If you try tooupload an image that is not an exact multiple, hello upload will fail.</span></span>
* <span data-ttu-id="3ea2a-116">Hello размер изображения должен быть 127 ГБ или меньше.</span><span class="sxs-lookup"><span data-stu-id="3ea2a-116">hello image size must be 127 GB or smaller.</span></span>
* <span data-ttu-id="3ea2a-117">он должен быть помещен в VHD-файл (файлы VHDX в настоящее время не поддерживаются).</span><span class="sxs-lookup"><span data-stu-id="3ea2a-117">It must be on a VHD file (VHDX files are not currently supported).</span></span>
* <span data-ttu-id="3ea2a-118">Hello виртуального жесткого диска не должен быть виртуальной машины поколения 2.</span><span class="sxs-lookup"><span data-stu-id="3ea2a-118">hello VHD must not be a generation 2 virtual machine.</span></span>
* <span data-ttu-id="3ea2a-119">Hello виртуального жесткого диска может быть фиксированного размера или динамически расширяемых.</span><span class="sxs-lookup"><span data-stu-id="3ea2a-119">hello VHD can be either fixed-size or dynamically expanding.</span></span> <span data-ttu-id="3ea2a-120">Динамически расширяемый виртуальный жесткий ДИСК рекомендуется, так как он принимает tooAzure tooupload меньше времени, чем файл VHD фиксированного размера.</span><span class="sxs-lookup"><span data-stu-id="3ea2a-120">A dynamically expanding VHD is recommended because it takes less time tooupload tooAzure than a fixed-size VHD file.</span></span>
* <span data-ttu-id="3ea2a-121">Hello диск должен быть инициализирован с помощью стиля разделов hello основная загрузочная запись (MBR).</span><span class="sxs-lookup"><span data-stu-id="3ea2a-121">hello disk must be initialized using hello Master Boot Record (MBR) partitioning style.</span></span> <span data-ttu-id="3ea2a-122">Hello стилем разделов таблицы Разделов GUID разделов не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="3ea2a-122">hello GUID partition table (GPT) partition style is not supported.</span></span>
* <span data-ttu-id="3ea2a-123">Hello виртуальный жесткий ДИСК должен содержать одной установке Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="3ea2a-123">hello VHD must contain a single installation of Windows Server 2012 R2.</span></span> <span data-ttu-id="3ea2a-124">Он может содержать несколько томов, но только один из них может содержать установку Windows.</span><span class="sxs-lookup"><span data-stu-id="3ea2a-124">It can contain multiple volumes, but only one that contains an installation of Windows.</span></span>
* <span data-ttu-id="3ea2a-125">необходимо установить роль узла сеансов удаленных рабочих столов (RDSH) Hello и возможности рабочего стола hello.</span><span class="sxs-lookup"><span data-stu-id="3ea2a-125">hello Remote Desktop Session Host (RDSH) role and hello Desktop Experience feature must be installed.</span></span>
* <span data-ttu-id="3ea2a-126">Hello роли посредника подключений к удаленному рабочему столу необходимо *не* установить.</span><span class="sxs-lookup"><span data-stu-id="3ea2a-126">hello Remote Desktop Connection Broker role must *not* be installed.</span></span>
* <span data-ttu-id="3ea2a-127">необходимо отключить Hello шифрованной файловой системы (EFS).</span><span class="sxs-lookup"><span data-stu-id="3ea2a-127">hello Encrypting File System (EFS) must be disabled.</span></span>
* <span data-ttu-id="3ea2a-128">Hello изображение должно быть обработанной командой Sysprep, используя параметры hello **/oobe / generalize/shutdown** (hello, не используйте **/mode:vm** параметр).</span><span class="sxs-lookup"><span data-stu-id="3ea2a-128">hello image must be SYSPREPed using hello parameters **/oobe /generalize /shutdown** (DO NOT use hello **/mode:vm** parameter).</span></span>
* <span data-ttu-id="3ea2a-129">Отправка VHD из цепочки моментальных снимков не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="3ea2a-129">Uploading your VHD from a snapshot chain is not supported.</span></span>

<span data-ttu-id="3ea2a-130">Сведения о создании образов для Azure RemoteApp см. в статье [Создание образа Azure RemoteApp](remoteapp-imageoptions.md).</span><span class="sxs-lookup"><span data-stu-id="3ea2a-130">See [Create an Azure RemoteApp image](remoteapp-imageoptions.md) for more information about creating images for Azure RemoteApp.</span></span>

