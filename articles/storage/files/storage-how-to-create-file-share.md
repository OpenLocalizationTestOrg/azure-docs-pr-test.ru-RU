---
title: "aaaHow toocreate файловый ресурс Azure | Документы Microsoft"
description: "Как toocreate Azure общей папки в хранилище файлов Azure, с помощью hello портал Azure, PowerShell и hello Azure CLI."
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
ms.openlocfilehash: 816694e411a993dae881816fc62173e2b7afe990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a><span data-ttu-id="9e676-103">Создание общей папки в хранилище файлов Azure</span><span class="sxs-lookup"><span data-stu-id="9e676-103">Create a File Share in Azure File storage</span></span>
<span data-ttu-id="9e676-104">Можно создать общих ресурсов Azure с помощью [портал Azure](https://portal.azure.com/)hello командлеты PowerShell хранилища Azure, hello клиентских библиотек хранилища Azure или hello API REST хранилища Azure. В этом учебнике вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="9e676-104">You can create Azure File shares using [Azure portal](https://portal.azure.com/), hello Azure Storage PowerShell cmdlets, hello Azure Storage client libraries, or hello Azure Storage REST API.In this tutorial, you will learn:</span></span>
* [<span data-ttu-id="9e676-105">Как предоставить доступ toocreate файл Azure с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="9e676-105">How toocreate an Azure File share using hello Azure portal</span></span>](#Create file share through hello Portal)
* [<span data-ttu-id="9e676-106">Как toocreate Azure общей папки с помощью Powershell</span><span class="sxs-lookup"><span data-stu-id="9e676-106">How toocreate an Azure File share using Powershell</span></span>](#Create file share using PowerShell)
* [<span data-ttu-id="9e676-107">Как toocreate Azure общей папки с использованием интерфейса CLI</span><span class="sxs-lookup"><span data-stu-id="9e676-107">How toocreate an Azure File share using CLI</span></span>](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a><span data-ttu-id="9e676-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9e676-108">Prerequisites</span></span>
<span data-ttu-id="9e676-109">toocreate Azure файловый ресурс, можно использовать учетную запись хранения, которая уже существует, или [Создание учетной записи хранилища Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e676-109">toocreate an Azure File share, you can use a storage account that already exists, or [create a new Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span> <span data-ttu-id="9e676-110">toocreate Azure файловый ресурс с помощью PowerShell, потребуется ключ учетной записи hello и имя учетной записи...</span><span class="sxs-lookup"><span data-stu-id="9e676-110">toocreate an Azure File share with PowerShell, you will need hello account key and name of your storage account..</span></span> <span data-ttu-id="9e676-111">Если планируется toouse Powershell или интерфейс командной строки, вам потребуется ключ учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="9e676-111">You will need Storage account key if you plan toouse Powershell or CLI.</span></span>

## <a name="create-file-share-through-hello-portal"></a><span data-ttu-id="9e676-112">Создайте общую папку через портал hello</span><span class="sxs-lookup"><span data-stu-id="9e676-112">Create file share through hello Portal</span></span>
1. <span data-ttu-id="9e676-113">**Колонка учетной записи tooStorage перейдите на портал Azure**:</span><span class="sxs-lookup"><span data-stu-id="9e676-113">**Go tooStorage Account blade on Azure Portal**:</span></span>    
    <span data-ttu-id="9e676-114">![Колонка учетной записи хранения](./media/storage-how-to-create-file-share/create-file-share-portal1.png)</span><span class="sxs-lookup"><span data-stu-id="9e676-114">![Storage Account Blade](./media/storage-how-to-create-file-share/create-file-share-portal1.png)</span></span>

2. <span data-ttu-id="9e676-115">**Нажмите кнопку "Общая папка"**:</span><span class="sxs-lookup"><span data-stu-id="9e676-115">**Click on add File Share button**:</span></span>    
    <span data-ttu-id="9e676-116">![Нажмите кнопку hello файл общего ресурса кнопка "Добавить"](./media/storage-how-to-create-file-share/create-file-share-portal2.png)</span><span class="sxs-lookup"><span data-stu-id="9e676-116">![Click hello add file share button](./media/storage-how-to-create-file-share/create-file-share-portal2.png)</span></span>

3. <span data-ttu-id="9e676-117">**Укажите имя и квоту. В настоящее время предусмотрено ограничение квоты — не более 5 ТБ**:</span><span class="sxs-lookup"><span data-stu-id="9e676-117">**Provide Name and Quota. Quota currently can be maximum 5TB**:</span></span>    
    <span data-ttu-id="9e676-118">![Укажите имя и нужный квоты для общей папки hello](./media/storage-how-to-create-file-share/create-file-share-portal3.png)</span><span class="sxs-lookup"><span data-stu-id="9e676-118">![Provide a name and a desired quota for hello new file share](./media/storage-how-to-create-file-share/create-file-share-portal3.png)</span></span>

4. <span data-ttu-id="9e676-119">**Просмотрите новую общую папку**: ![просмотр новой общей папки](./media/storage-how-to-create-file-share/create-file-share-portal4.png)</span><span class="sxs-lookup"><span data-stu-id="9e676-119">**View your new file share**:  ![View your new file share](./media/storage-how-to-create-file-share/create-file-share-portal4.png)</span></span>

5. <span data-ttu-id="9e676-120">**Отправьте файл**: ![отправка файла](./media/storage-how-to-create-file-share/create-file-share-portal5.png)</span><span class="sxs-lookup"><span data-stu-id="9e676-120">**Upload a file**:  ![Upload a file](./media/storage-how-to-create-file-share/create-file-share-portal5.png)</span></span>

6. <span data-ttu-id="9e676-121">**Перейдите в общую папку для управления каталогами и файлами**: ![обзор общей папки](./media/storage-how-to-create-file-share/create-file-share-portal6.png)</span><span class="sxs-lookup"><span data-stu-id="9e676-121">**Browse into your file share and manage your directories and files**:  ![Browse file share](./media/storage-how-to-create-file-share/create-file-share-portal6.png)</span></span>


## <a name="create-file-share-through-powershell"></a><span data-ttu-id="9e676-122">Создание общей папки с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e676-122">Create file share through PowerShell</span></span>
<span data-ttu-id="9e676-123">tooprepare toouse PowerShell, загрузить и установить командлеты Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="9e676-123">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="9e676-124">В разделе [как tooinstall и настройка Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) для hello установить точку и инструкции по установке.</span><span class="sxs-lookup"><span data-stu-id="9e676-124">See [How tooinstall and configure Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) for hello install point and installation instructions.</span></span>

> [!Note]  
> <span data-ttu-id="9e676-125">Рекомендуется загрузить и установить или обновить toohello последнюю версию модуля Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9e676-125">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>

1. <span data-ttu-id="9e676-126">**Создать контекст для учетной записи хранилища и ключ** контекста hello инкапсулирует hello ключ учетной записи хранения имени и учетной записи.</span><span class="sxs-lookup"><span data-stu-id="9e676-126">**Create a context for your storage account and key** hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="9e676-127">Инструкции по копированию ключа учетной записи с [портала Azure](https://portal.azure.com/) см. в разделе [Просмотр и копирование ключей доступа к хранилищу](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="9e676-127">For instructions on copying your account key from the [Azure portal](https://portal.azure.com/), see [View and copy storage access keys](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span></span>

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. <span data-ttu-id="9e676-128">**Создайте новую общую папку**:</span><span class="sxs-lookup"><span data-stu-id="9e676-128">**Create a new file share**:</span></span>    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> <span data-ttu-id="9e676-129">Hello имя файлового ресурса общего доступа должны указываться прописными буквами.</span><span class="sxs-lookup"><span data-stu-id="9e676-129">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="9e676-130">Дополнительные сведения о присвоении имен общим папкам и файлам см. в статье [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx) (Именование общих ресурсов, каталогов, файлов и метаданных и ссылка на них).</span><span class="sxs-lookup"><span data-stu-id="9e676-130">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>

## <a name="create-file-share-through-command-line-interface-cli"></a><span data-ttu-id="9e676-131">Создание общей папки с помощью интерфейса командной строки (CLI)</span><span class="sxs-lookup"><span data-stu-id="9e676-131">Create file share through Command Line Interface (CLI)</span></span>
1. <span data-ttu-id="9e676-132">**tooprepare toouse интерфейс командной строки (CLI), загрузите и установите hello Azure CLI.**</span><span class="sxs-lookup"><span data-stu-id="9e676-132">**tooprepare toouse a Command Line Interface (CLI), download and install hello Azure CLI.**</span></span>  
    <span data-ttu-id="9e676-133">Дополнительные сведения см. в руководстве по [установке Azure CLI 2.0](/cli/azure/install-az-cli2.md), а также руководстве по [обзору Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9e676-133">See [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) and [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span>

2. <span data-ttu-id="9e676-134">**Создание учетной соединения строки toohello хранилища место toocreate hello папки.**</span><span class="sxs-lookup"><span data-stu-id="9e676-134">**Create a connection string toohello storage account where you want toocreate hello share.**</span></span>  
    <span data-ttu-id="9e676-135">Замените ```<storage-account>``` и ```<resource_group>``` с вашей учетной записи имени и ресурсов группы хранения в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="9e676-135">Replace ```<storage-account>``` and ```<resource_group>``` with your storage account name and resource group in hello following example.</span></span>

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. <span data-ttu-id="9e676-136">**Создайте общую папку**.</span><span class="sxs-lookup"><span data-stu-id="9e676-136">**Create file share**</span></span>
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a><span data-ttu-id="9e676-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9e676-137">Next steps</span></span>
* <span data-ttu-id="9e676-138">[Mount an Azure File share and access the share in Windows](storage-how-to-use-files-windows.md) (Подключение файлового ресурса Azure и доступ к нему в Windows)</span><span class="sxs-lookup"><span data-stu-id="9e676-138">[Connect and Mount File Share - Windows](storage-how-to-use-files-windows.md)</span></span>
* [<span data-ttu-id="9e676-139">Использование хранилища файлов Azure в Linux</span><span class="sxs-lookup"><span data-stu-id="9e676-139">Connect and Mount File Share - Linux</span></span>](../storage-how-to-use-files-linux.md)
* <span data-ttu-id="9e676-140">[Mount Azure File share over SMB with macOS](storage-how-to-use-files-mac.md) (Использование хранилища файлов Azure с помощью протокола SMB в macOS)</span><span class="sxs-lookup"><span data-stu-id="9e676-140">[Connect and Mount File Share - macOS](storage-how-to-use-files-mac.md)</span></span>

<span data-ttu-id="9e676-141">Дополнительную информацию о хранилище файлов Azure см. по этим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="9e676-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="9e676-142">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="9e676-142">FAQ</span></span>](../storage-files-faq.md)
* <span data-ttu-id="9e676-143">[Troubleshoot Azure File storage problems in Windows](storage-troubleshoot-windows-file-connection-problems.md) (Устранение неполадок хранилища файлов Azure в Windows)</span><span class="sxs-lookup"><span data-stu-id="9e676-143">[Troubleshooting on Windows](storage-troubleshoot-windows-file-connection-problems.md)</span></span>      
* <span data-ttu-id="9e676-144">[Troubleshoot Azure File storage problems in Linux](storage-troubleshoot-linux-file-connection-problems.md) (Устранение неполадок хранилища файлов Azure в Linux)</span><span class="sxs-lookup"><span data-stu-id="9e676-144">[Troubleshooting on Linux](storage-troubleshoot-linux-file-connection-problems.md)</span></span>   