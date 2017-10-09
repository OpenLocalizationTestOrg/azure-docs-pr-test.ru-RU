---
title: "aaaHow toouse PowerShell toomanage хранилища Azure File | Документы Microsoft"
description: "Узнайте хранилища Azure File toomanage toouse PowerShell."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 0e30e8796cf8bbf5f9249b26179d5e0f9077c8fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-powershell-toomanage-azure-file-storage"></a><span data-ttu-id="58a47-103">Как toomanage toouse PowerShell хранилища Azure File</span><span class="sxs-lookup"><span data-stu-id="58a47-103">How toouse PowerShell toomanage Azure File storage</span></span>
<span data-ttu-id="58a47-104">Можно использовать toocreate Azure PowerShell и управлять общими папками.</span><span class="sxs-lookup"><span data-stu-id="58a47-104">You can use Azure PowerShell toocreate and manage file shares.</span></span>

## <a name="install-hello-powershell-cmdlets-for-azure-storage"></a><span data-ttu-id="58a47-105">Установка командлетов PowerShell hello для хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="58a47-105">Install hello PowerShell cmdlets for Azure Storage</span></span>
<span data-ttu-id="58a47-106">tooprepare toouse PowerShell, загрузить и установить командлеты Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="58a47-106">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="58a47-107">В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs) для hello установить точку и инструкции по установке.</span><span class="sxs-lookup"><span data-stu-id="58a47-107">See [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for hello install point and installation instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="58a47-108">Рекомендуется загрузить и установить или обновить toohello последнюю версию модуля Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="58a47-108">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>
> 
> 

<span data-ttu-id="58a47-109">Откройте окно Azure PowerShell. Для этого нажмите кнопку **Запустить** и введите **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="58a47-109">Open an Azure PowerShell window by clicking **Start** and typing **Windows PowerShell**.</span></span> <span data-ttu-id="58a47-110">окно PowerShell Hello загружает hello модуля Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="58a47-110">hello PowerShell window loads hello Azure Powershell module for you.</span></span>

## <a name="create-a-context-for-your-storage-account-and-key"></a><span data-ttu-id="58a47-111">Создание объекта контекста и ключа для учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="58a47-111">Create a context for your storage account and key</span></span>
<span data-ttu-id="58a47-112">Создайте hello контекста учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="58a47-112">Create hello storage account context.</span></span> <span data-ttu-id="58a47-113">контекст Hello инкапсулирует hello ключ учетной записи хранения имени и учетной записи.</span><span class="sxs-lookup"><span data-stu-id="58a47-113">hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="58a47-114">Инструкции по копированию ключ учетной записи из hello [портал Azure](https://portal.azure.com), в разделе [представление и скопируйте ключи доступа к хранилищу](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="58a47-114">For instructions on copying your account key from hello [Azure portal](https://portal.azure.com), see [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>

<span data-ttu-id="58a47-115">Замените `storage-account-name` и `storage-account-key` с помощью имени учетной записи хранилища и ключ в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="58a47-115">Replace `storage-account-name` and `storage-account-key` with your storage account name and key in hello following example.</span></span>

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a><span data-ttu-id="58a47-116">Создание нового ресурса совместно используемых файлов</span><span class="sxs-lookup"><span data-stu-id="58a47-116">Create a new file share</span></span>
<span data-ttu-id="58a47-117">Создание нового ресурса hello, с именем `logs`.</span><span class="sxs-lookup"><span data-stu-id="58a47-117">Create hello new share, named `logs`.</span></span>

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

<span data-ttu-id="58a47-118">У вас появится новый общий ресурс в хранилище файлов.</span><span class="sxs-lookup"><span data-stu-id="58a47-118">You now have a file share in File storage.</span></span> <span data-ttu-id="58a47-119">Далее мы добавим каталог и файл.</span><span class="sxs-lookup"><span data-stu-id="58a47-119">Next we'll add a directory and a file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="58a47-120">Hello имя файлового ресурса общего доступа должны указываться прописными буквами.</span><span class="sxs-lookup"><span data-stu-id="58a47-120">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="58a47-121">Дополнительные сведения о присвоении имен общим папкам и файлам см. в статье [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx) (Именование общих ресурсов, каталогов, файлов и метаданных и ссылка на них).</span><span class="sxs-lookup"><span data-stu-id="58a47-121">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>
> 
> 

## <a name="create-a-directory-in-hello-file-share"></a><span data-ttu-id="58a47-122">Создайте каталог в общей папке hello</span><span class="sxs-lookup"><span data-stu-id="58a47-122">Create a directory in hello file share</span></span>
<span data-ttu-id="58a47-123">Создайте каталог в общей папке hello.</span><span class="sxs-lookup"><span data-stu-id="58a47-123">Create a directory in hello share.</span></span> <span data-ttu-id="58a47-124">В следующем примере hello, hello каталог `CustomLogs`.</span><span class="sxs-lookup"><span data-stu-id="58a47-124">In hello following example, hello directory is named `CustomLogs`.</span></span>

```powershell
# create a directory in hello share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-toohello-directory"></a><span data-ttu-id="58a47-125">Отправка toohello каталог локального файла</span><span class="sxs-lookup"><span data-stu-id="58a47-125">Upload a local file toohello directory</span></span>
<span data-ttu-id="58a47-126">Теперь отправьте toohello каталог локального файла.</span><span class="sxs-lookup"><span data-stu-id="58a47-126">Now upload a local file toohello directory.</span></span> <span data-ttu-id="58a47-127">Hello следующий пример отправляет файл из `C:\temp\Log1.txt`.</span><span class="sxs-lookup"><span data-stu-id="58a47-127">hello following example uploads a file from `C:\temp\Log1.txt`.</span></span> <span data-ttu-id="58a47-128">Измените путь к файлу hello, которое указывает допустимый файл tooa на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="58a47-128">Edit hello file path so that it points tooa valid file on your local machine.</span></span>

```powershell
# upload a local file toohello new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-hello-files-in-hello-directory"></a><span data-ttu-id="58a47-129">Список файлов в каталоге hello, hello</span><span class="sxs-lookup"><span data-stu-id="58a47-129">List hello files in hello directory</span></span>
<span data-ttu-id="58a47-130">toosee hello файл в каталоге hello, можно составить список всех файлов каталога hello.</span><span class="sxs-lookup"><span data-stu-id="58a47-130">toosee hello file in hello directory, you can list all of hello directory's files.</span></span> <span data-ttu-id="58a47-131">Эта команда возвращает hello файлы и подкаталоги (если таковые имеются) в каталоге CustomLogs hello.</span><span class="sxs-lookup"><span data-stu-id="58a47-131">This command returns hello files and subdirectories (if there are any) in hello CustomLogs directory.</span></span>

```powershell
# list files in hello new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

<span data-ttu-id="58a47-132">Get-AzureStorageFile возвращает список файлов и каталогов в каталоге, в который отправлен объект.</span><span class="sxs-lookup"><span data-stu-id="58a47-132">Get-AzureStorageFile returns a list of files and directories for whatever directory object is passed in.</span></span> <span data-ttu-id="58a47-133">«Get-AzureStorageFile-совместное использование $s» возвращает список файлов и каталогов в корневой каталог hello.</span><span class="sxs-lookup"><span data-stu-id="58a47-133">"Get-AzureStorageFile -Share $s" returns a list of files and directories in hello root directory.</span></span> <span data-ttu-id="58a47-134">tooget список файлов в подкаталоге, у вас есть hello подкаталог toopass tooGet-AzureStorageFile.</span><span class="sxs-lookup"><span data-stu-id="58a47-134">tooget a list of files in a subdirectory, you have toopass hello subdirectory tooGet-AzureStorageFile.</span></span> <span data-ttu-id="58a47-135">При этом произойдет — первая часть команды hello канала toohello hello возвращает экземпляр directory hello подкаталог CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="58a47-135">That's what this does -- hello first part of hello command up toohello pipe returns a directory instance of hello subdirectory CustomLogs.</span></span> <span data-ttu-id="58a47-136">Затем, передается в Get-AzureStorageFile, который возвращает hello файлов и каталогов в CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="58a47-136">Then that is passed into Get-AzureStorageFile, which returns hello files and directories in CustomLogs.</span></span>

## <a name="copy-files"></a><span data-ttu-id="58a47-137">Копирование файлов</span><span class="sxs-lookup"><span data-stu-id="58a47-137">Copy files</span></span>
<span data-ttu-id="58a47-138">Начиная с версии 0.9.7 Azure PowerShell, можно скопировать файл tooanother, большой двоичный объект файла tooa или tooa файла большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="58a47-138">Beginning with version 0.9.7 of Azure PowerShell, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="58a47-139">Ниже показано как tooperform их копирования операции с помощью командлетов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="58a47-139">Below we demonstrate how tooperform these copy operations using PowerShell cmdlets.</span></span>

```powershell
# copy a file toohello new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob tooa file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a><span data-ttu-id="58a47-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="58a47-140">Next steps</span></span>
<span data-ttu-id="58a47-141">Дополнительную информацию о хранилище файлов Azure см. по этим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="58a47-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="58a47-142">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="58a47-142">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="58a47-143">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="58a47-143">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)