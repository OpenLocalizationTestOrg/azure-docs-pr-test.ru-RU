---
title: "aaaUpload пользовательского изображения для Azure RemoteApp | Документы Microsoft"
description: "Узнайте, как tooupload пользовательского образа для Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: 299e0510-1a6b-4fdf-914a-3631b061a360
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: ericor
ms.openlocfilehash: 6ad40fe58795ece37f4c7900be01bc713938da87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a><span data-ttu-id="4960e-103">Отправка пользовательского образа для Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="4960e-103">Upload a custom image for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4960e-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="4960e-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="4960e-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="4960e-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="4960e-106">Теперь, когда вы создали пользовательский шаблон изображения или были обновлены с изменениями, вы должны tooupload, библиотека изображений Azure RemoteApp tooyour изображения.</span><span class="sxs-lookup"><span data-stu-id="4960e-106">Now that you have created your custom template image or have updated it with changes, you need tooupload that image tooyour Azure RemoteApp image library.</span></span> <span data-ttu-id="4960e-107">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="4960e-107">Use these steps.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="4960e-108">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="4960e-108">Before you start</span></span>
1. <span data-ttu-id="4960e-109">Проверьте настраиваемого образа соответствует hello [требования к изображению](remoteapp-imagereqs.md) и [требования приложения](remoteapp-appreqs.md).</span><span class="sxs-lookup"><span data-stu-id="4960e-109">Verify your custom image meets hello [image requirements](remoteapp-imagereqs.md) and [application requirements](remoteapp-appreqs.md).</span></span>
2. <span data-ttu-id="4960e-110">Установка hello [модуля Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4960e-110">Install hello [Azure PowerShell module](/powershell/azure/overview).</span></span>

## <a name="step-by-step-on-how-tooupload-custom-image"></a><span data-ttu-id="4960e-111">Шаг за шагом о том, как tooupload пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="4960e-111">Step by step on how tooupload custom image</span></span>
1. <span data-ttu-id="4960e-112">Открыть портал управления Azure и перейдите на страницу toohello RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="4960e-112">Open Azure Management Portal and navigate toohello RemoteApp page.</span></span>
2. <span data-ttu-id="4960e-113">На hello **образы шаблонов** щелкните **отправить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="4960e-113">On hello **Template images** tab, click **Upload** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="4960e-114">Введите понятное имя для образа и укажите расположение учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="4960e-114">Enter a friendly name for your image and specify hello storage account location.</span></span> <span data-ttu-id="4960e-115">Убедитесь, расположение hello hello местоположения коллекции RemoteApp или место toocreate одно расположение.</span><span class="sxs-lookup"><span data-stu-id="4960e-115">Ensure hello location is hello same location as your RemoteApp collection or a location where you want toocreate one.</span></span>
4. <span data-ttu-id="4960e-116">При появлении соответствующего запроса загрузите tooyour сценария hello локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="4960e-116">When prompted, download hello script tooyour local PC.</span></span>
5. <span data-ttu-id="4960e-117">Скопируйте параметры команды hello в текстовом поле hello tooyour-буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="4960e-117">Copy hello command parameters in hello text box tooyour clipboard.</span></span>
6. <span data-ttu-id="4960e-118">Откройте окно Windows PowerShell с повышенными привилегиями.</span><span class="sxs-lookup"><span data-stu-id="4960e-118">Open an elevated Windows PowerShell window.</span></span>
7. <span data-ttu-id="4960e-119">Из hello с повышенными правами окно Windows PowerShell перейдите toohello же каталоге, куда был загружен скрипт hello.</span><span class="sxs-lookup"><span data-stu-id="4960e-119">From hello elevated Windows PowerShell window, navigate toohello same directory where you downloaded hello script.</span></span>
8. <span data-ttu-id="4960e-120">Вставить hello скопировать команду и нажмите клавишу **ввод**.</span><span class="sxs-lookup"><span data-stu-id="4960e-120">Paste hello copied command and press **Enter**.</span></span>
   
   <span data-ttu-id="4960e-121">начнется процесс передачи Hello и длительность зависит от многих факторов, включая скорость сетевого подключения и размер изображения hello</span><span class="sxs-lookup"><span data-stu-id="4960e-121">hello upload process will begin and duration may depend on many factors including your network speed and size of hello image</span></span>
9. <span data-ttu-id="4960e-122">Если подобное вашей передачи завершилась сбоем из-за перебоев в работе сети или вещи, всегда можно возобновить процесс передачи hello, когда вы начали.</span><span class="sxs-lookup"><span data-stu-id="4960e-122">If your upload does not succeed because of network interruption or things like that, you can always resume hello upload process you began.</span></span> <span data-ttu-id="4960e-123">Здравствуйте tooresume передачи, запустите скрипт hello снова, используя же командной строки.</span><span class="sxs-lookup"><span data-stu-id="4960e-123">tooresume an upload, run hello script again using hello same command line.</span></span>

> [!WARNING]
> <span data-ttu-id="4960e-124">Никогда не изменяйте hello загрузки скрипта.</span><span class="sxs-lookup"><span data-stu-id="4960e-124">Never modify hello upload script.</span></span> <span data-ttu-id="4960e-125">Проверках было реализовано tooensure, hello hello образ изображения соответствуют требованиям и требованиям приложения.</span><span class="sxs-lookup"><span data-stu-id="4960e-125">Specific checks have been implemented tooensure that hello image meets hello image requirements and application requirements.</span></span>
> 
> 

## <a name="common-problems"></a><span data-ttu-id="4960e-126">Распространенные проблемы</span><span class="sxs-lookup"><span data-stu-id="4960e-126">Common problems</span></span>
* <span data-ttu-id="4960e-127">Убедитесь, что вы используете Windows PowerShell, а не Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4960e-127">Make sure you use Windows PowerShell, not Azure PowerShell.</span></span> <span data-ttu-id="4960e-128">Так как некоторые модули будут нужны во время процесса отправки hello необходимо модуля Azure PowerShell tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="4960e-128">You need tooinstall hello Azure PowerShell module because certain modules are needed during hello upload process.</span></span>
* <span data-ttu-id="4960e-129">Никогда не изменяют hello сценария, проверки существуют для вашего удобства.</span><span class="sxs-lookup"><span data-stu-id="4960e-129">Never alter hello script, validations are there for your convenience.</span></span>
* <span data-ttu-id="4960e-130">Если hello VHD-файл получает заблокирована во время загрузки, скопируйте файл hello или переместите его новое расположение и попытка передачи tooa еще раз.</span><span class="sxs-lookup"><span data-stu-id="4960e-130">If hello vhd file gets locked out during upload, copy hello file or move it tooa new location and attempt upload again.</span></span> <span data-ttu-id="4960e-131">Возможно, какой-то процесс Windows препятствует отправке.</span><span class="sxs-lookup"><span data-stu-id="4960e-131">There might be some Windows process that is preventing upload.</span></span>  

