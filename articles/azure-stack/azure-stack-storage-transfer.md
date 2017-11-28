---
title: "aaaTools для хранилища Azure стека"
description: "Дополнительные сведения о данных из хранилища Azure стека средств переноса"
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/16/2017
ms.author: xiaofmao
ms.openlocfilehash: 184a1a51b4267e913aae823df31df3704d8e7b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tools-for-azure-stack-storage"></a><span data-ttu-id="bc1fd-103">Набор средств для хранения стек Azure</span><span class="sxs-lookup"><span data-stu-id="bc1fd-103">Tools for Azure Stack Storage</span></span>

<span data-ttu-id="bc1fd-104">Стека Microsoft Azure предоставляет набор служб хранилища hello дисков, больших двоичных объектов, таблиц, очередей и функции управления учетной записи.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-104">Microsoft Azure Stack provides a set of hello storage services for disks, blobs, tables, queues, and account management functionality.</span></span> <span data-ttu-id="bc1fd-105">Набор средств хранилища Azure можно использовать при необходимости toomanage или при перемещении данных tooor из стека хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-105">You can use a set of Azure Storage tools if you want toomanage or move data tooor from Azure Stack Storage.</span></span> <span data-ttu-id="bc1fd-106">В этой статье предоставляет краткий обзор средств hello.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-106">This article provides a quick overview of hello tools available.</span></span>

<span data-ttu-id="bc1fd-107">Hello средство, которое лучше всего подходит для вас зависит от требований:</span><span class="sxs-lookup"><span data-stu-id="bc1fd-107">hello tool that works best for you depends on your requirements:</span></span>
* [<span data-ttu-id="bc1fd-108">AzCopy</span><span class="sxs-lookup"><span data-stu-id="bc1fd-108">AzCopy</span></span>](#azcopy)

    <span data-ttu-id="bc1fd-109">Программа командной строки специфичные для хранилища, что toocopy данных можно загрузить из tooanother один объект в вашей учетной записи хранения или между учетными записями хранения.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-109">A storage-specific command-line utility that you can download toocopy data from one object tooanother within your storage account, or between storage accounts.</span></span>

* [<span data-ttu-id="bc1fd-110">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc1fd-110">Azure PowerShell</span></span>](#azure-powershell)

    <span data-ttu-id="bc1fd-111">Оболочка командной строки на основе задач и язык сценариев, предназначенный специально для системного администрирования.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-111">A task-based command-line shell and scripting language designed especially for system administration.</span></span>

* [<span data-ttu-id="bc1fd-112">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="bc1fd-112">Azure CLI</span></span>](#azure-cli)

    <span data-ttu-id="bc1fd-113">Открытая, кросс платформенных в это средство, которое предоставляет набор команд для работы с платформы Azure и Azure стека hello.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-113">An open-source, cross-platform tool that provides a set of commands for working with hello Azure and Azure Stack platforms.</span></span>

* [<span data-ttu-id="bc1fd-114">Обозреватель хранилищ Microsoft (Предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="bc1fd-114">Microsoft Storage Explorer (Preview)</span></span>](#microsoft-azure-storage-explorer)

    <span data-ttu-id="bc1fd-115">Отдельное приложение легко toouse с пользовательским интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-115">An easy toouse standalone app with a user interface.</span></span>

<span data-ttu-id="bc1fd-116">Из-за toohello хранилища служб различия между Azure и Azure стека может возникнуть определенные требования для каждого средства, описанные в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-116">Due toohello Storage services differences between Azure and Azure Stack, there might be some specific requirements for each tool described in hello following sections.</span></span> <span data-ttu-id="bc1fd-117">Сравнение между Azure и хранилищем Azure стека см. в разделе [стек хранилища Azure: различия и рекомендации](azure-stack-acs-differences.md).</span><span class="sxs-lookup"><span data-stu-id="bc1fd-117">For a comparison between Azure Stack storage and Azure storage, see [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md).</span></span>


## <a name="azcopy"></a><span data-ttu-id="bc1fd-118">AzCopy</span><span class="sxs-lookup"><span data-stu-id="bc1fd-118">AzCopy</span></span>
<span data-ttu-id="bc1fd-119">AzCopy является tooand данные командной строки служебная программа разработанная toocopy из хранилища больших двоичных объектов Microsoft Azure и таблицы с помощью простой команды с оптимальной производительностью.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-119">AzCopy is a command-line utility designed toocopy data tooand from Microsoft Azure Blob and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="bc1fd-120">Можно скопировать данные из одного объекта tooanother в вашей учетной записи хранения или между учетными записями хранения.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-120">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span> <span data-ttu-id="bc1fd-121">Существует две версии hello AzCopy: AzCopy в Windows и AzCopy в Linux.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-121">There are two version of hello AzCopy: AzCopy on Windows and AzCopy on Linux.</span></span> <span data-ttu-id="bc1fd-122">Стек Azure поддерживает только версия Windows hello.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-122">Azure Stack only supports hello Windows version.</span></span> 
 
### <a name="download-and-install-azcopy"></a><span data-ttu-id="bc1fd-123">Скачивание и установка AzCopy</span><span class="sxs-lookup"><span data-stu-id="bc1fd-123">Download and install AzCopy</span></span> 
<span data-ttu-id="bc1fd-124">[Загрузите](https://aka.ms/azcopyforazurestack) версию Windows hello поддерживается AzCopy для Azure стека.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-124">[Download](https://aka.ms/azcopyforazurestack) hello supported Windows version of AzCopy for Azure Stack.</span></span> <span data-ttu-id="bc1fd-125">Можно установить и использовать AzCopy на hello стек Azure так же, как Azure.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-125">You can install and use AzCopy on Azure Stack hello same way as Azure.</span></span> <span data-ttu-id="bc1fd-126">toolearn более, в разделе [перенесите данные с помощью служебной программы командной строки AzCopy hello](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="bc1fd-126">toolearn more, see [Transfer data with hello AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="azcopy-command-examples-for-data-transfer"></a><span data-ttu-id="bc1fd-127">Примеры команды AzCopy для передачи данных</span><span class="sxs-lookup"><span data-stu-id="bc1fd-127">AzCopy command examples for data transfer</span></span>
<span data-ttu-id="bc1fd-128">Привет, следующие примеры демонстрируют несколько типичных сценариях для копирования данных tooand из стека Azure BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-128">hello following examples demonstrate a few typical scenarios for copying data tooand from Azure Stack blobs.</span></span> <span data-ttu-id="bc1fd-129">toolearn более, в разделе [перенесите данные с помощью служебной программы командной строки AzCopy hello](../storage/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="bc1fd-129">toolearn more, see [Transfer data with hello AzCopy Command-Line Utility](../storage/storage-use-azcopy.md).</span></span> 
#### <a name="download-all-blobs-toolocal-disk"></a><span data-ttu-id="bc1fd-130">Загрузка диска toolocal все большие двоичные объекты</span><span class="sxs-lookup"><span data-stu-id="bc1fd-130">Download all blobs toolocal disk</span></span>
```azcopy
AzCopy.exe /source:https://myaccount.blob.local.azurestack.external/mycontainer /dest:C:\myfolder /sourcekey:<key> /S
```
#### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="bc1fd-131">Отправка одного файла каталога toovirtual</span><span class="sxs-lookup"><span data-stu-id="bc1fd-131">Upload single file toovirtual directory</span></span> 
```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.local.azurestack.external/mycontainer/vd /DestKey:key /Pattern:abc.txt
```
#### <a name="move-data-between-azure-and-azure-stack-storage"></a><span data-ttu-id="bc1fd-132">Перемещение данных между Azure и стек хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="bc1fd-132">Move data between Azure and Azure Stack Storage</span></span> 
<span data-ttu-id="bc1fd-133">Асинхронную передачу данных между хранилища Azure и Azure стека не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-133">Asynchronous data transfer between Azure Storage and Azure Stack is not supported.</span></span> <span data-ttu-id="bc1fd-134">требуется передача hello toospecify с hello `/SyncCopy` параметр.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-134">you need toospecify hello transfer with hello `/SyncCopy` option.</span></span> 
```azcopy 
Azcopy /Source:https://myaccount.blob.local.azurestack.external/mycontainer /Dest:https://myaccount2.blob.core.windows.net/mycontainer2 /SourceKey:AzSKey /DestKey:Azurekey /S /SyncCopy
```

### <a name="azcopy-known-issues"></a><span data-ttu-id="bc1fd-135">Azcopy. Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="bc1fd-135">Azcopy Known issues</span></span>
* <span data-ttu-id="bc1fd-136">Любая операция AzCopy для хранения файлов не доступен, поскольку еще не доступен в Azure стек хранилища файлов.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-136">Any AzCopy operation on File storage is not available because File Storage is not yet available in Azure Stack.</span></span>
* <span data-ttu-id="bc1fd-137">Асинхронную передачу данных между хранилища Azure и Azure стека не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-137">Asynchronous data transfer between Azure Storage and Azure Stack is not supported.</span></span> <span data-ttu-id="bc1fd-138">Можно указать hello передачи с hello `/SyncCopy` toocopy hello данные.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-138">You can specify hello transfer with hello `/SyncCopy` option toocopy hello data.</span></span>
* <span data-ttu-id="bc1fd-139">версии Linux Hello Azcopy не поддерживается для стека хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-139">hello Linux version of Azcopy is not supported for Azure Stack Storage.</span></span> 

## <a name="azure-powershell"></a><span data-ttu-id="bc1fd-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc1fd-140">Azure PowerShell</span></span>
<span data-ttu-id="bc1fd-141">Azure PowerShell — это модуль, который предоставляет командлеты для управления службами в Azure и Azure стека.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-141">Azure PowerShell is a module that provides cmdlets for managing services on both Azure and Azure Stack.</span></span> <span data-ttu-id="bc1fd-142">Это оболочка командной строки для выполнения задач и язык сценариев, разработанный специально для администрирования системы.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-142">It's a task-based command-line shell and scripting language designed especially for system administration.</span></span>

### <a name="install-and-configure-powershell-for-azure-stack"></a><span data-ttu-id="bc1fd-143">Установите и настройте PowerShell для Azure стека</span><span class="sxs-lookup"><span data-stu-id="bc1fd-143">Install and Configure PowerShell for Azure Stack</span></span>
<span data-ttu-id="bc1fd-144">Совместимые модули Azure PowerShell Azure стека являются обязательным toowork со стеком Azure.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-144">Azure Stack compatible Azure PowerShell modules are required toowork with Azure Stack.</span></span> <span data-ttu-id="bc1fd-145">Дополнительные сведения см. в разделе [Установка PowerShell для Azure стека](azure-stack-powershell-install.md) и [настройки среды PowerShell hello Azure стека пользователя](azure-stack-powershell-configure-user.md) toolearn дополнительные.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-145">For more information, see [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) and [Configure hello Azure Stack user's PowerShell environment](azure-stack-powershell-configure-user.md) toolearn more.</span></span>

### <a name="powershell-sample-script-for-azure-stack"></a><span data-ttu-id="bc1fd-146">Сценарий PowerShell для Azure стека</span><span class="sxs-lookup"><span data-stu-id="bc1fd-146">PowerShell Sample script for Azure Stack</span></span> 
<span data-ttu-id="bc1fd-147">В этом примере предположим, что успешно [Установка PowerShell для Azure стека](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="bc1fd-147">This sample assume you have successfully [Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span> <span data-ttu-id="bc1fd-148">Этот скрипт будет помогают conplete hello конфигурации и попросите вашего клиента Azure стека учетных данных tooadd вашей учетной записи toohello локального PowerShell environemnt.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-148">This script will help you conplete hello configuration and ask your Azure Stack tenant credentials tooadd your account toohello local PowerShell environemnt.</span></span> <span data-ttu-id="bc1fd-149">Затем сценарий hello будет по умолчанию hello подписки Azure, создание новой учетной записи хранения в Azure, создать контейнер в этой новой учетной записи хранения и отправить существующий контейнер toothat образ файла (blob).</span><span class="sxs-lookup"><span data-stu-id="bc1fd-149">Then, hello script will set hello default Azure subscription, create a new storage account in Azure, create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="bc1fd-150">После hello скрипт перечисляет все большие двоичные объекты в этом контейнере, создает новый каталог назначения на своем локальном компьютере и загрузите файл изображения hello.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-150">After hello script lists all blobs in that container, it will create a new destination directory in your local computer and download hello image file.</span></span>

1. <span data-ttu-id="bc1fd-151">Установка [модули Azure PowerShell Azure стека совместимой](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="bc1fd-151">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
2. <span data-ttu-id="bc1fd-152">Загрузите hello [toowork необходимые средства с Azure стека](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="bc1fd-152">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span>  
3. <span data-ttu-id="bc1fd-153">Откройте **интегрированной среды Сценариев Windows PowerShell** и **Запуск от имени администратора**, нажмите кнопку **файл** > **New** toocreate новый файл скрипта.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-153">Open **Windows PowerShell ISE** and **Run as Administrator**, click **File** > **New** toocreate a new script file.</span></span>
4. <span data-ttu-id="bc1fd-154">Скопируйте приведенный ниже сценарий hello и вставьте toohello новый файл скрипта.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-154">Copy hello script below and paste toohello new script file.</span></span>
5. <span data-ttu-id="bc1fd-155">Обновление переменных сценария hello на основании параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-155">Update hello script variables based on your configuration settings.</span></span> 
6. <span data-ttu-id="bc1fd-156">Примечание: этот скрипт содержит toobe запуска в корне hello загруженный **AzureStack_Tools**.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-156">Note: this script has toobe run under hello root of downloaded **AzureStack_Tools**.</span></span> 

```PowerShell 
# begin

$ARMEvnName = "AzureStackUser" # set AzureStackUser as your Azure Stack environemnt name
$ARMEndPoint = "https://management.local.azurestack.external" 
$GraphAudiance = "https://graph.windows.net/" 
$AADTenantName = "<myDirectoryTenantName>.onmicrosoft.com" 

$SubscriptionName = "basic" # Update with hello name of your subscription.
$ResourceGroupName = "myTestRG" # Give a name tooyour new resource group.
$StorageAccountName = "azsblobcontainer" # Give a name tooyour new storage account. It must be lowercase!
$Location = "Local" # Choose "Local" as an example.
$ContainerName = "photo" # Give a name tooyour new container.
$ImageToUpload = "C:\temp\Hello.jpg" # Prepare an image file and a source directory in your local computer.
$DestinationFolder = "C:\temp\downlaod" # A destination directory in your local computer.

# Import hello Connect PowerShell module"
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
Import-Module .\Connect\AzureStack.Connect.psm1

# Configure hello PowerShell environment
# Register an AzureRM environment that targets your Azure Stack instance
Add-AzureRmEnvironment -Name $ARMEvnName -ARMEndpoint $ARMEndPoint 

# Set hello GraphEndpointResourceId value
Set-AzureRmEnvironment -Name $ARMEvnName -GraphEndpoint $GraphAudiance

# Login
$TenantID = Get-AzsDirectoryTenantId -AADTenantName $AADTenantName -EnvironmentName $ARMEvnName
Login-AzureRmAccount -EnvironmentName $ARMEvnName -TenantId $TenantID 

# Set a default Azure subscription.
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Create a new Resource Group 
New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

# Create a new storage account.
New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS

# Set a default storage account.
Set-AzureRmCurrentStorageAccount -StorageAccountName $StorageAccountName -ResourceGroupName $ResourceGroupName 

# Create a new container.
New-AzureStorageContainer -Name $ContainerName -Permission Off

# Upload a blob into a container.
Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload

# List all blobs in a container.
Get-AzureStorageBlob -Container $ContainerName

# Download blobs from hello container:
# Get a reference tooa list of all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName

# Create hello destination directory.
New-Item -Path $DestinationFolder -ItemType Directory -Force  

# Download blobs into hello local destination directory.
$blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder

# end
```

### <a name="powershell-known-issues"></a><span data-ttu-id="bc1fd-157">PowerShell известные проблемы</span><span class="sxs-lookup"><span data-stu-id="bc1fd-157">PowerShell Known Issues</span></span> 
<span data-ttu-id="bc1fd-158">Hello текущего совместимые Azure PowerShell модуль для стека Azure имеет версию 1.2.10.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-158">hello current compatible Azure PowerShell module version for Azure Stack is 1.2.10.</span></span> <span data-ttu-id="bc1fd-159">Оно отличается от hello последнюю версию Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-159">It’s different from hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="bc1fd-160">Это различие влияет на операции службы хранилища:</span><span class="sxs-lookup"><span data-stu-id="bc1fd-160">This difference impacts storage services operation:</span></span>

* <span data-ttu-id="bc1fd-161">Формат возвращаемого значения Hello `Get-AzureRmStorageAccountKey` в версии 1.2.10 имеет два свойства: `Key1` и `Key2`, а в текущей версии Azure hello возвращает массив, содержащий все ключи учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-161">hello return value format of `Get-AzureRmStorageAccountKey` in version 1.2.10 has two properties: `Key1` and `Key2`, while hello current Azure version returns an array containing all hello account keys.</span></span>
   ```
   # This command gets a specific key for a Storage account, 
   # and works for Azure PowerShell version 1.4, and later versions.
   (Get-AzureRmStorageAccountKey -ResourceGroupName "RG01" `
   -AccountName "MyStorageAccount").Value[0]

   # This command gets a specific key for a Storage account, 
   # and works for Azure PowerShell version 1.3.2, and previous versions.
   (Get-AzureRmStorageAccountKey -ResourceGroupName "RG01" `
   -AccountName "MyStorageAccount").Key1

   ```
   <span data-ttu-id="bc1fd-162">Дополнительные сведения см. в разделе [Get AzureRmStorageAccountKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0).</span><span class="sxs-lookup"><span data-stu-id="bc1fd-162">For more information, see [Get-AzureRmStorageAccountKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0).</span></span>

## <a name="azure-cli"></a><span data-ttu-id="bc1fd-163">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="bc1fd-163">Azure CLI</span></span>
<span data-ttu-id="bc1fd-164">Hello Azure CLI оказывается Azure командной строки для управления ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-164">hello Azure CLI is Azure’s command-line experience for managing Azure resources.</span></span> <span data-ttu-id="bc1fd-165">Можно установить на Windows, Linux и macOS и запустите его из командной строки hello.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-165">You can install it on macOS, Linux, and Windows and run it from hello command line.</span></span> 

<span data-ttu-id="bc1fd-166">Azure CLI оптимизирована для управления и администрирования из командной строки hello ресурсы Azure, а также для создания сценариев автоматизации, которые работают с hello диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-166">Azure CLI is optimized for managing and administering Azure resources from hello command line, and for building automation scripts that work against hello Azure Resource Manager.</span></span> <span data-ttu-id="bc1fd-167">Он предоставляет многие hello найти на портале Azure стека hello, включая доступ сложных данных те же функции.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-167">It provides many of hello same functions found in hello Azure Stack portal, including rich data access.</span></span>

<span data-ttu-id="bc1fd-168">Стек Azure требует Azure CLI версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-168">Azure Stack requires Azure CLI version 2.0.</span></span> <span data-ttu-id="bc1fd-169">Дополнительные сведения об установке и настройке Azure CLI со стеком Azure см. в разделе [установить и настроить Azure CLI стека](azure-stack-connect-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bc1fd-169">For more information about installing and configuring Azure CLI with Azure Stack, see [Install and configure Azure Stack CLI](azure-stack-connect-cli.md).</span></span> <span data-ttu-id="bc1fd-170">Дополнительные сведения о том, как tooperform hello Azure CLI 2.0 toouse несколько задач, работы с ресурсами в вашей учетной записи хранилища Azure стека, отображается [Using hello Azure CLI2.0 со службой хранилища Azure](../storage/storage-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="bc1fd-170">For more information about how toouse hello Azure CLI 2.0 tooperform several tasks working with resources in your Azure Stack Storage account, see [Using hello Azure CLI2.0 with Azure Storage](../storage/storage-azure-cli.md)</span></span>

### <a name="azure-cli-sample-script-for-azure-stack"></a><span data-ttu-id="bc1fd-171">Образец сценария Azure CLI для стека Azure</span><span class="sxs-lookup"><span data-stu-id="bc1fd-171">Azure CLI sample script for Azure Stack</span></span> 
<span data-ttu-id="bc1fd-172">После завершения установки CLI hello и настройки можно попробовать следующие шаги toowork с toointeract сценария небольшой оболочки образец с ресурсов хранилища Azure стека hello.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-172">Once you complete hello CLI installation and configuration, you can try hello following steps toowork with a small shell sample script toointeract with Azure Stack Storage resources.</span></span> <span data-ttu-id="bc1fd-173">Hello скрипт сначала создает новый контейнер в учетной записи затем загружает существующий контейнер toothat файла (в виде больших двоичных объектов), перечислены все большие двоичные объекты в контейнере hello и и, наконец, загружает hello назначения tooa файл на локальном компьютере, который можно указать.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-173">hello script first creates a new container in your storage account, then uploads an existing file (as a blob) toothat container, lists all blobs in hello container, and finally, downloads hello file tooa destination on your local computer that you specify.</span></span> <span data-ttu-id="bc1fd-174">Прежде чем запустить этот сценарий, убедитесь, что подключение выполнено успешно и целевой toohello входа Azure стека.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-174">Before you run this script, make sure you successfully connect and login toohello target Azure Stack.</span></span> 
1. <span data-ttu-id="bc1fd-175">Откройте текстовый редактор, затем скопируйте и вставьте hello предшествующий скрипт в редактор hello.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-175">Open your favorite text editor, then copy and paste hello preceding script into hello editor.</span></span>
2. <span data-ttu-id="bc1fd-176">Обновление параметров конфигурации tooreflect переменные сценария hello.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-176">Update hello script's variables tooreflect your configuration settings.</span></span> 
3. <span data-ttu-id="bc1fd-177">После обновления hello необходимые переменные, сохранить сценарий hello и выйти из редактора.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-177">After you've updated hello necessary variables, save hello script and exit your editor.</span></span> <span data-ttu-id="bc1fd-178">Hello Далее предполагается, что действия с названием my_storage_sample.sh вашего сценария.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-178">hello next steps assume you've named your script my_storage_sample.sh.</span></span>
4. <span data-ttu-id="bc1fd-179">Пометка hello скрипта как исполняемый файл и при необходимости:`chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="bc1fd-179">Mark hello script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>
5. <span data-ttu-id="bc1fd-180">Выполнение скрипта hello.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-180">Execute hello script.</span></span> <span data-ttu-id="bc1fd-181">например в Bash: `./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="bc1fd-181">For example, in Bash: `./my_storage_sample.sh`</span></span>

```bash
#!/bin/bash
# A simple Azure Stack Storage example script

export AZURESTACK_RESOURCE_GROUP=<resource_group_name>
export AZURESTACK_RG_LOCATION="local"
export AZURESTACK_STORAGE_ACCOUNT_NAME=<storage_account_name>
export AZURESTACK_STORAGE_CONTAINER_NAME=<container_name>
export AZURESTACK_STORAGE_BLOB_NAME=<blob_name>
export FILE_TO_UPLOAD=<file_to_upload>
export DESTINATION_FILE=<destination_file>

echo "Creating hello resource group..."
az group create --name $AZURESTACK_RESOURCE_GROUP --location $AZURESTACK_RG_LOCATION

echo "Creating hello storage account..."
az storage account create --name $AZURESTACK_STORAGE_ACCOUNT_NAME --resource-group $AZURESTACK_RESOURCE_GROUP --account-type Standard_LRS

echo "Creating hello blob container..."
az storage container create --name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME

echo "Uploading hello file..."
az storage blob upload --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --file $FILE_TO_UPLOAD --name $AZURESTACK_STORAGE_BLOB_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME

echo "Listing hello blobs..."
az storage blob list --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME --output table

echo "Downloading hello file..."
az storage blob download --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME --name $AZURESTACK_STORAGE_BLOB_NAME --file $DESTINATION_FILE --output table

echo "Done"
```

## <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="bc1fd-182">Обозреватель службы хранилища Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="bc1fd-182">Microsoft Azure Storage Explorer</span></span>

<span data-ttu-id="bc1fd-183">Обозреватель хранилищ Microsoft Azure — отдельное приложение от Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-183">Microsoft Azure Storage Explorer is a standalone app from Microsoft.</span></span> <span data-ttu-id="bc1fd-184">Она позволяет tooeasily при обработке хранилища Azure и Azure стек хранилища данных в Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-184">It allows you tooeasily work with both Azure Storage and Azure Stack Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="bc1fd-185">Если требуется простой способ toomanage данные стека хранилища Azure, рассмотрите возможность использования обозревателя хранилища Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="bc1fd-185">If you want an easy way toomanage your Azure Stack Storage data, then consider using Microsoft Azure Storage Explorer.</span></span>

<span data-ttu-id="bc1fd-186">Дополнительные сведения о настройке toowork обозреватель хранилищ Azure со стеком Azure в разделе [tooan подключить обозреватель хранилища Azure стека подписки](azure-stack-storage-connect-se.md).</span><span class="sxs-lookup"><span data-stu-id="bc1fd-186">For more information about configuring Azure Storage Explorer toowork with Azure Stack, see [Connect Storage Explorer tooan Azure Stack subscription](azure-stack-storage-connect-se.md).</span></span>

<span data-ttu-id="bc1fd-187">Дополнительные сведения об обозревателе хранилища Microsoft Azure см. в разделе [приступить к работе с помощью обозревателя хранилища (Предварительная версия)](../vs-azure-tools-storage-manage-with-storage-explorer.md)</span><span class="sxs-lookup"><span data-stu-id="bc1fd-187">For more information about Microsoft Azure Storage Explorer, see [Get started with Storage Explorer (Preview)](../vs-azure-tools-storage-manage-with-storage-explorer.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc1fd-188">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bc1fd-188">Next steps</span></span>
* [<span data-ttu-id="bc1fd-189">Подключение подписки Azure стека tooan обозреватель хранилищ</span><span class="sxs-lookup"><span data-stu-id="bc1fd-189">Connect Storage Explorer tooan Azure Stack subscription</span></span>](azure-stack-storage-connect-se.md)
* [<span data-ttu-id="bc1fd-190">Приступая к работе с обозреватель хранилищ (Предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="bc1fd-190">Get started with Storage Explorer (Preview)</span></span>](../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [<span data-ttu-id="bc1fd-191">Хранилище Azure согласованное: различия и рекомендации</span><span class="sxs-lookup"><span data-stu-id="bc1fd-191">Azure-consistent storage: differences and considerations</span></span>](azure-stack-acs-differences.md)
* [<span data-ttu-id="bc1fd-192">Введение tooMicrosoft хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="bc1fd-192">Introduction tooMicrosoft Azure Storage</span></span>](../storage/common/storage-introduction.md)

