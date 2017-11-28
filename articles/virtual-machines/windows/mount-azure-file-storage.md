---
title: "хранилище файлов Azure из виртуальной Машины Windows Azure aaaMount | Документы Microsoft"
description: "Файл хранится в облаке hello с хранилищем файлов Azure и подключения к общей папке облака из Azure виртуальной машины (VM)."
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 965f1c1b3f0d07fec6d86f9312a05e02e8ce7fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a><span data-ttu-id="dc29c-103">Использование общих файловых ресурсов Azure с виртуальными машинами Windows</span><span class="sxs-lookup"><span data-stu-id="dc29c-103">Use Azure file shares with Windows VMs</span></span> 

<span data-ttu-id="dc29c-104">Общие папки файлов Azure можно использовать как способ toostore и доступ к файлам из виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="dc29c-104">You can use Azure file shares as a way toostore and access files from your VM.</span></span> <span data-ttu-id="dc29c-105">Например можно хранить сценария или файла конфигурации приложения, которые должны все tooshare вашей ВМ.</span><span class="sxs-lookup"><span data-stu-id="dc29c-105">For example, you can store a script or an application configuration file that you want all your VMs tooshare.</span></span> <span data-ttu-id="dc29c-106">В этом разделе мы покажем toocreate и подключения Azure общая папка, а также и tooupload и загрузки файлов.</span><span class="sxs-lookup"><span data-stu-id="dc29c-106">In this topic, we show you how toocreate and mount an Azure file share, and how tooupload and download files.</span></span>

## <a name="connect-tooa-file-share-from-a-vm"></a><span data-ttu-id="dc29c-107">Подключение tooa общей папки из виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="dc29c-107">Connect tooa file share from a VM</span></span>

<span data-ttu-id="dc29c-108">В этом разделе предполагается, что уже имеется общего ресурса tooconnect в файл.</span><span class="sxs-lookup"><span data-stu-id="dc29c-108">This section assumes you already have a file share that you want tooconnect to.</span></span> <span data-ttu-id="dc29c-109">Получить toocreate один [создайте общую папку](#create-a-file-share) далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="dc29c-109">If you need toocreate one, see [Create a file share](#create-a-file-share) later in this topic.</span></span>

1. <span data-ttu-id="dc29c-110">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dc29c-110">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dc29c-111">Hello левого меню **учетные записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="dc29c-111">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="dc29c-112">Выберите учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="dc29c-112">Choose your storage account.</span></span>
4. <span data-ttu-id="dc29c-113">В hello **Обзор** в разделе **службы**выберите **файлы**.</span><span class="sxs-lookup"><span data-stu-id="dc29c-113">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="dc29c-114">Выберите общий файловый ресурс.</span><span class="sxs-lookup"><span data-stu-id="dc29c-114">Select a file share.</span></span>
6. <span data-ttu-id="dc29c-115">Нажмите кнопку **Connect** tooopen страницы, которая отображает hello синтаксис командной строки для монтажа hello общей папки Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="dc29c-115">Click **Connect** tooopen a page that shows hello command-line syntax for mounting hello file share from Windows or Linux.</span></span>
7. <span data-ttu-id="dc29c-116">Выделите hello синтаксис команды hello и вставьте его в блокноте или в другое место где его можно легко получить.</span><span class="sxs-lookup"><span data-stu-id="dc29c-116">Highlight hello syntax of hello command and paste it into Notepad or someplace else where you can easily access it.</span></span> 
8. <span data-ttu-id="dc29c-117">Изменить начальные hello tooremove синтаксис hello ** > ** и замените *[буква диска]* с буквой диска hello (например, **Y:**) место toomount hello общей папки.</span><span class="sxs-lookup"><span data-stu-id="dc29c-117">Edit hello syntax tooremove hello leading **> ** and replace *[drive letter]* with hello drive letter (for example, **Y:**) where you would like toomount hello file share.</span></span>
8. <span data-ttu-id="dc29c-118">Подключите tooyour ВМ и откройте командную строку.</span><span class="sxs-lookup"><span data-stu-id="dc29c-118">Connect tooyour VM and open a command prompt.</span></span>
9. <span data-ttu-id="dc29c-119">Вставить в hello изменить синтаксис соединения и нажмите кнопку **ввод**.</span><span class="sxs-lookup"><span data-stu-id="dc29c-119">Paste in hello edited connection syntax and hit **Enter**.</span></span>
10. <span data-ttu-id="dc29c-120">При создании подключения hello сообщение hello **hello команда выполнена успешно.**</span><span class="sxs-lookup"><span data-stu-id="dc29c-120">When hello connection has been created, you get hello message **hello command completed successfully.**</span></span>
11. <span data-ttu-id="dc29c-121">Проверьте подключение hello, введя в hello-указание toothat tooswitch букву диска, а затем введите **dir** содержимое hello toosee hello файлового ресурса общего доступа.</span><span class="sxs-lookup"><span data-stu-id="dc29c-121">Check hello connection by typing in hello drive letter tooswitch toothat drive and then type **dir** toosee hello contents of hello file share.</span></span>



## <a name="create-a-file-share"></a><span data-ttu-id="dc29c-122">Создайте общую папку</span><span class="sxs-lookup"><span data-stu-id="dc29c-122">Create a file share</span></span> 
1. <span data-ttu-id="dc29c-123">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dc29c-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dc29c-124">Hello левого меню **учетные записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="dc29c-124">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="dc29c-125">Выберите учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="dc29c-125">Choose your storage account.</span></span>
4. <span data-ttu-id="dc29c-126">В hello **Обзор** в разделе **службы**выберите **файлы**.</span><span class="sxs-lookup"><span data-stu-id="dc29c-126">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="dc29c-127">На странице приветствия службы файлов нажмите кнопку **+ общий файловый ресурс** toocreate совместно использовать первый файл. \\</span><span class="sxs-lookup"><span data-stu-id="dc29c-127">In hello File Service page, click **+ File share** toocreate your first file share.\\</span></span>
6. <span data-ttu-id="dc29c-128">Введите имя общей папки hello.</span><span class="sxs-lookup"><span data-stu-id="dc29c-128">Fill in hello file share name.</span></span> <span data-ttu-id="dc29c-129">В его имени можно использовать строчные буквы, цифры и отдельные дефисы.</span><span class="sxs-lookup"><span data-stu-id="dc29c-129">File share names can use lowercase letters, numbers and single hyphens.</span></span> <span data-ttu-id="dc29c-130">Hello имя не может начинаться с дефиса и не могут использовать несколько последовательных дефисов.</span><span class="sxs-lookup"><span data-stu-id="dc29c-130">hello name cannot start with a hyphen and you can't use multiple, consecutive hyphens.</span></span> 
7. <span data-ttu-id="dc29c-131">Заполните поля на ограничение на размер файла hello может быть too5120 Гбайт.</span><span class="sxs-lookup"><span data-stu-id="dc29c-131">Fill in a limit on how large hello file can be, up too5120 GB.</span></span>
8. <span data-ttu-id="dc29c-132">Нажмите кнопку **ОК** toodeploy hello общей папки.</span><span class="sxs-lookup"><span data-stu-id="dc29c-132">Click **OK** toodeploy hello file share.</span></span>
   
## <a name="upload-files"></a><span data-ttu-id="dc29c-133">Отправка файлов</span><span class="sxs-lookup"><span data-stu-id="dc29c-133">Upload files</span></span>
1. <span data-ttu-id="dc29c-134">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dc29c-134">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dc29c-135">Hello левого меню **учетные записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="dc29c-135">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="dc29c-136">Выберите учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="dc29c-136">Choose your storage account.</span></span>
4. <span data-ttu-id="dc29c-137">В hello **Обзор** в разделе **службы**выберите **файлы**.</span><span class="sxs-lookup"><span data-stu-id="dc29c-137">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="dc29c-138">Выберите общий файловый ресурс.</span><span class="sxs-lookup"><span data-stu-id="dc29c-138">Select a file share.</span></span>
6. <span data-ttu-id="dc29c-139">Нажмите кнопку **отправить** tooopen hello **передачи файлов** страницы.</span><span class="sxs-lookup"><span data-stu-id="dc29c-139">Click **Upload** tooopen hello **Upload files** page.</span></span>
7. <span data-ttu-id="dc29c-140">Щелкните значок toobrowse hello папки локальной файловой системы для tooupload файла.</span><span class="sxs-lookup"><span data-stu-id="dc29c-140">Click on hello folder icon toobrowse your local file system for a file tooupload.</span></span>   
8. <span data-ttu-id="dc29c-141">Нажмите кнопку **отправить** tooupload hello файл toohello общей папки.</span><span class="sxs-lookup"><span data-stu-id="dc29c-141">Click **Upload** tooupload hello file toohello file share.</span></span>

## <a name="download-files"></a><span data-ttu-id="dc29c-142">Скачивание файлов</span><span class="sxs-lookup"><span data-stu-id="dc29c-142">Download files</span></span>
1. <span data-ttu-id="dc29c-143">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dc29c-143">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dc29c-144">Hello левого меню **учетные записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="dc29c-144">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="dc29c-145">Выберите учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="dc29c-145">Choose your storage account.</span></span>
4. <span data-ttu-id="dc29c-146">В hello **Обзор** в разделе **службы**выберите **файлы**.</span><span class="sxs-lookup"><span data-stu-id="dc29c-146">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="dc29c-147">Выберите общий файловый ресурс.</span><span class="sxs-lookup"><span data-stu-id="dc29c-147">Select a file share.</span></span>
6. <span data-ttu-id="dc29c-148">Правой кнопкой мыши файл hello и выберите **загрузки** toodownload его tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="dc29c-148">Right-click on hello file and choose **Download** toodownload it tooyour local machine.</span></span>
   

## <a name="next-steps"></a><span data-ttu-id="dc29c-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dc29c-149">Next steps</span></span>

<span data-ttu-id="dc29c-150">Вы также можете создавать файловые ресурсы и управлять ими с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc29c-150">You can also create and manage file shares using PowerShell.</span></span> <span data-ttu-id="dc29c-151">Дополнительные сведения см. в статье [Develop for Azure File storage with .NET](../../storage/files/storage-dotnet-how-to-use-files.md) (Разработка для хранилища файлов Azure с помощью .NET).</span><span class="sxs-lookup"><span data-stu-id="dc29c-151">For more information, see [Get started with Azure File storage on Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>
