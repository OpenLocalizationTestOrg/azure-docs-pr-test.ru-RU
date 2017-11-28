---
title: "Как управлять хранилищем файлов Azure с помощью PowerShell | Документация Майкрософт"
description: "Узнайте, как использовать PowerShell для управления хранилищем файлов Azure."
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
ms.openlocfilehash: 148375b156c4ae1aa4bf203d215f7ed607a71b89
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="how-to-use-powershell-to-manage-azure-file-storage"></a><span data-ttu-id="48c9b-103">Как использовать PowerShell для управления хранилищем файлов Azure</span><span class="sxs-lookup"><span data-stu-id="48c9b-103">How to use PowerShell to manage Azure File storage</span></span>
<span data-ttu-id="48c9b-104">Вы можете использовать Azure PowerShell для создания общих папок и управления ими.</span><span class="sxs-lookup"><span data-stu-id="48c9b-104">You can use Azure PowerShell to create and manage file shares.</span></span>

## <a name="install-the-powershell-cmdlets-for-azure-storage"></a><span data-ttu-id="48c9b-105">Установите командлеты PowerShell для хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="48c9b-105">Install the PowerShell cmdlets for Azure Storage</span></span>
<span data-ttu-id="48c9b-106">Для подготовки к использованию PowerShell загрузите и установите командлеты Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="48c9b-106">To prepare to use PowerShell, download and install the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="48c9b-107">Инструкции по установке см. в статье [Установка и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="48c9b-107">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for the install point and installation instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="48c9b-108">Рекомендуется загрузить и установить или обновить версию модуля Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="48c9b-108">It's recommended that you download and install or upgrade to the latest Azure PowerShell module.</span></span>
> 
> 

<span data-ttu-id="48c9b-109">Откройте окно Azure PowerShell. Для этого нажмите кнопку **Запустить** и введите **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="48c9b-109">Open an Azure PowerShell window by clicking **Start** and typing **Windows PowerShell**.</span></span> <span data-ttu-id="48c9b-110">Окно PowerShell выполнит загрузку модуля Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="48c9b-110">The PowerShell window loads the Azure Powershell module for you.</span></span>

## <a name="create-a-context-for-your-storage-account-and-key"></a><span data-ttu-id="48c9b-111">Создание объекта контекста и ключа для учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="48c9b-111">Create a context for your storage account and key</span></span>
<span data-ttu-id="48c9b-112">Создайте объект контекста учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="48c9b-112">Create the storage account context.</span></span> <span data-ttu-id="48c9b-113">Контекст включает имя учетной записи хранения и ключ.</span><span class="sxs-lookup"><span data-stu-id="48c9b-113">The context encapsulates the storage account name and account key.</span></span> <span data-ttu-id="48c9b-114">Инструкции по копированию ключа учетной записи с [портала Azure](https://portal.azure.com) см. в разделе [Просмотр и копирование ключей доступа к хранилищу](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="48c9b-114">For instructions on copying your account key from the [Azure portal](https://portal.azure.com), see [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>

<span data-ttu-id="48c9b-115">В следующем примере вместо `storage-account-name` и `storage-account-key` используйте имя и ключ своей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="48c9b-115">Replace `storage-account-name` and `storage-account-key` with your storage account name and key in the following example.</span></span>

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a><span data-ttu-id="48c9b-116">Создание нового ресурса совместно используемых файлов</span><span class="sxs-lookup"><span data-stu-id="48c9b-116">Create a new file share</span></span>
<span data-ttu-id="48c9b-117">Создайте новый файловый ресурс с именем `logs`.</span><span class="sxs-lookup"><span data-stu-id="48c9b-117">Create the new share, named `logs`.</span></span>

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

<span data-ttu-id="48c9b-118">У вас появится новый общий ресурс в хранилище файлов.</span><span class="sxs-lookup"><span data-stu-id="48c9b-118">You now have a file share in File storage.</span></span> <span data-ttu-id="48c9b-119">Далее мы добавим каталог и файл.</span><span class="sxs-lookup"><span data-stu-id="48c9b-119">Next we'll add a directory and a file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48c9b-120">Имя общей папки должно состоять из символов в нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="48c9b-120">The name of your file share must be all lowercase.</span></span> <span data-ttu-id="48c9b-121">Дополнительные сведения о присвоении имен общим папкам и файлам см. в статье [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx) (Именование общих ресурсов, каталогов, файлов и метаданных и ссылка на них).</span><span class="sxs-lookup"><span data-stu-id="48c9b-121">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>
> 
> 

## <a name="create-a-directory-in-the-file-share"></a><span data-ttu-id="48c9b-122">Создание каталога в ресурсе совместно используемых файлов</span><span class="sxs-lookup"><span data-stu-id="48c9b-122">Create a directory in the file share</span></span>
<span data-ttu-id="48c9b-123">Создайте каталог в ресурсе совместно используемых файлов.</span><span class="sxs-lookup"><span data-stu-id="48c9b-123">Create a directory in the share.</span></span> <span data-ttu-id="48c9b-124">В данном примере используется каталог с именем `CustomLogs`:</span><span class="sxs-lookup"><span data-stu-id="48c9b-124">In the following example, the directory is named `CustomLogs`.</span></span>

```powershell
# create a directory in the share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-to-the-directory"></a><span data-ttu-id="48c9b-125">Отправка локального файла в каталог</span><span class="sxs-lookup"><span data-stu-id="48c9b-125">Upload a local file to the directory</span></span>
<span data-ttu-id="48c9b-126">Затем загрузите локальный файл в хранилище файлов.</span><span class="sxs-lookup"><span data-stu-id="48c9b-126">Now upload a local file to the directory.</span></span> <span data-ttu-id="48c9b-127">В данном примере файл передается из `C:\temp\Log1.txt`.</span><span class="sxs-lookup"><span data-stu-id="48c9b-127">The following example uploads a file from `C:\temp\Log1.txt`.</span></span> <span data-ttu-id="48c9b-128">Отредактируйте путь к файлу, чтобы он соответствовал пути к существующему файлу на локальном компьютере:</span><span class="sxs-lookup"><span data-stu-id="48c9b-128">Edit the file path so that it points to a valid file on your local machine.</span></span>

```powershell
# upload a local file to the new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-the-files-in-the-directory"></a><span data-ttu-id="48c9b-129">Просмотр списка файлов в каталоге</span><span class="sxs-lookup"><span data-stu-id="48c9b-129">List the files in the directory</span></span>
<span data-ttu-id="48c9b-130">Чтобы просмотреть файлы в каталоге, можно вывести список файлов.</span><span class="sxs-lookup"><span data-stu-id="48c9b-130">To see the file in the directory, you can list all of the directory's files.</span></span> <span data-ttu-id="48c9b-131">Эта команда возвращает файлы и подкаталоги (если таковые имеются) в каталоге CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="48c9b-131">This command returns the files and subdirectories (if there are any) in the CustomLogs directory.</span></span>

```powershell
# list files in the new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

<span data-ttu-id="48c9b-132">Get-AzureStorageFile возвращает список файлов и каталогов в каталоге, в который отправлен объект.</span><span class="sxs-lookup"><span data-stu-id="48c9b-132">Get-AzureStorageFile returns a list of files and directories for whatever directory object is passed in.</span></span> <span data-ttu-id="48c9b-133">Get-AzureStorageFile -Share $s возвращает список файлов и каталогов в корневой папке.</span><span class="sxs-lookup"><span data-stu-id="48c9b-133">"Get-AzureStorageFile -Share $s" returns a list of files and directories in the root directory.</span></span> <span data-ttu-id="48c9b-134">Чтобы получить список файлов в подкаталоге, необходимо передать подкаталог команде Get-AzureStorageFile.</span><span class="sxs-lookup"><span data-stu-id="48c9b-134">To get a list of files in a subdirectory, you have to pass the subdirectory to Get-AzureStorageFile.</span></span> <span data-ttu-id="48c9b-135">Как это работает: первая часть команды возвращает экземпляр каталога подкаталога CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="48c9b-135">That's what this does -- the first part of the command up to the pipe returns a directory instance of the subdirectory CustomLogs.</span></span> <span data-ttu-id="48c9b-136">Затем этот экземпляр передается команде Get-AzureStorageFile, которая возвращает файлы и каталоги в CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="48c9b-136">Then that is passed into Get-AzureStorageFile, which returns the files and directories in CustomLogs.</span></span>

## <a name="copy-files"></a><span data-ttu-id="48c9b-137">Копирование файлов</span><span class="sxs-lookup"><span data-stu-id="48c9b-137">Copy files</span></span>
<span data-ttu-id="48c9b-138">Начиная с версии 0.9.7 Azure PowerShell, можно скопировать файл в другой файл, файл в большой двоичный объект или BLOB-объект в файл.</span><span class="sxs-lookup"><span data-stu-id="48c9b-138">Beginning with version 0.9.7 of Azure PowerShell, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="48c9b-139">Ниже показано, как выполнить копирование с помощью командлетов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="48c9b-139">Below we demonstrate how to perform these copy operations using PowerShell cmdlets.</span></span>

```powershell
# copy a file to the new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob to a file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a><span data-ttu-id="48c9b-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="48c9b-140">Next steps</span></span>
<span data-ttu-id="48c9b-141">Дополнительную информацию о хранилище файлов Azure см. по этим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="48c9b-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="48c9b-142">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="48c9b-142">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="48c9b-143">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="48c9b-143">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)