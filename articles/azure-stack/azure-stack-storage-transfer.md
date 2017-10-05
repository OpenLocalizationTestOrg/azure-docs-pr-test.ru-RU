---
title: "Набор средств для хранения стек Azure"
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
ms.openlocfilehash: 01069b8b7488ae0caaec4ae608c36b0f361e544c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="tools-for-azure-stack-storage"></a><span data-ttu-id="81155-103">Набор средств для хранения стек Azure</span><span class="sxs-lookup"><span data-stu-id="81155-103">Tools for Azure Stack Storage</span></span>

<span data-ttu-id="81155-104">Стека Microsoft Azure предоставляет набор дисков, больших двоичных объектов, таблиц, очередей и функции управления учетной записи службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="81155-104">Microsoft Azure Stack provides a set of the storage services for disks, blobs, tables, queues, and account management functionality.</span></span> <span data-ttu-id="81155-105">Набор средств хранилища Azure можно использовать, если вы хотите управлять, или переместить данные или из стека хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="81155-105">You can use a set of Azure Storage tools if you want to manage or move data to or from Azure Stack Storage.</span></span> <span data-ttu-id="81155-106">Также приводятся общие сведения об инструментах.</span><span class="sxs-lookup"><span data-stu-id="81155-106">This article provides a quick overview of the tools available.</span></span>

<span data-ttu-id="81155-107">Средство, которое лучше всего подходит для вас зависит от требований:</span><span class="sxs-lookup"><span data-stu-id="81155-107">The tool that works best for you depends on your requirements:</span></span>
* [<span data-ttu-id="81155-108">AzCopy</span><span class="sxs-lookup"><span data-stu-id="81155-108">AzCopy</span></span>](#azcopy)

    <span data-ttu-id="81155-109">Программа командной строки специфичные для хранилища, которую можно загрузить для копирования данных из одного объекта в другой в вашей учетной записи хранения или между учетными записями хранения.</span><span class="sxs-lookup"><span data-stu-id="81155-109">A storage-specific command-line utility that you can download to copy data from one object to another within your storage account, or between storage accounts.</span></span>

* [<span data-ttu-id="81155-110">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="81155-110">Azure PowerShell</span></span>](#azure-powershell)

    <span data-ttu-id="81155-111">Оболочка командной строки на основе задач и язык сценариев, предназначенный специально для системного администрирования.</span><span class="sxs-lookup"><span data-stu-id="81155-111">A task-based command-line shell and scripting language designed especially for system administration.</span></span>

* [<span data-ttu-id="81155-112">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="81155-112">Azure CLI</span></span>](#azure-cli)

    <span data-ttu-id="81155-113">Открытая, кросс платформенных в это средство, которое предоставляет набор команд для работы с платформы Azure и Azure стека.</span><span class="sxs-lookup"><span data-stu-id="81155-113">An open-source, cross-platform tool that provides a set of commands for working with the Azure and Azure Stack platforms.</span></span>

* [<span data-ttu-id="81155-114">Обозреватель хранилищ Microsoft (Предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="81155-114">Microsoft Storage Explorer (Preview)</span></span>](#microsoft-azure-storage-explorer)

    <span data-ttu-id="81155-115">Простой в использовании автономные приложения с пользовательским интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="81155-115">An easy to use standalone app with a user interface.</span></span>

<span data-ttu-id="81155-116">Из-за различий служб хранения данных между Azure и Azure стека может возникнуть определенные требования для каждого средства, описанные в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="81155-116">Due to the Storage services differences between Azure and Azure Stack, there might be some specific requirements for each tool described in the following sections.</span></span> <span data-ttu-id="81155-117">Сравнение между Azure и хранилищем Azure стека см. в разделе [стек хранилища Azure: различия и рекомендации](azure-stack-acs-differences.md).</span><span class="sxs-lookup"><span data-stu-id="81155-117">For a comparison between Azure Stack storage and Azure storage, see [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md).</span></span>


## <a name="azcopy"></a><span data-ttu-id="81155-118">AzCopy</span><span class="sxs-lookup"><span data-stu-id="81155-118">AzCopy</span></span>
<span data-ttu-id="81155-119">AzCopy является командной строки служебная программа, разработанная для копирования данных из больших двоичных объектов Microsoft Azure и хранилище таблиц с помощью простой команды с оптимальной производительностью.</span><span class="sxs-lookup"><span data-stu-id="81155-119">AzCopy is a command-line utility designed to copy data to and from Microsoft Azure Blob and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="81155-120">Кроме того, она позволяет копировать данные из одного объекта в другой в пределах одной учетной записи хранения или из одной такой записи в другую.</span><span class="sxs-lookup"><span data-stu-id="81155-120">You can copy data from one object to another within your storage account, or between storage accounts.</span></span> <span data-ttu-id="81155-121">Существует две версии AzCopy: AzCopy в Windows и AzCopy в Linux.</span><span class="sxs-lookup"><span data-stu-id="81155-121">There are two version of the AzCopy: AzCopy on Windows and AzCopy on Linux.</span></span> <span data-ttu-id="81155-122">Стек Azure поддерживает только версии Windows.</span><span class="sxs-lookup"><span data-stu-id="81155-122">Azure Stack only supports the Windows version.</span></span> 
 
### <a name="download-and-install-azcopy"></a><span data-ttu-id="81155-123">Скачивание и установка AzCopy</span><span class="sxs-lookup"><span data-stu-id="81155-123">Download and install AzCopy</span></span> 
<span data-ttu-id="81155-124">[Загрузить](https://aka.ms/azcopyforazurestack) AzCopy для стека Azure о поддерживаемых версиях Windows.</span><span class="sxs-lookup"><span data-stu-id="81155-124">[Download](https://aka.ms/azcopyforazurestack) the supported Windows version of AzCopy for Azure Stack.</span></span> <span data-ttu-id="81155-125">Можно установить и использовать AzCopy в стеке Azure так же, как Azure.</span><span class="sxs-lookup"><span data-stu-id="81155-125">You can install and use AzCopy on Azure Stack the same way as Azure.</span></span> <span data-ttu-id="81155-126">Дополнительные сведения см. в разделе [передачи данных с помощью служебной программы командной строки AzCopy](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="81155-126">To learn more, see [Transfer data with the AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="azcopy-command-examples-for-data-transfer"></a><span data-ttu-id="81155-127">Примеры команды AzCopy для передачи данных</span><span class="sxs-lookup"><span data-stu-id="81155-127">AzCopy command examples for data transfer</span></span>
<span data-ttu-id="81155-128">В следующих примерах демонстрируется несколько типичных сценариях для передачи данных между стек Azure BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="81155-128">The following examples demonstrate a few typical scenarios for copying data to and from Azure Stack blobs.</span></span> <span data-ttu-id="81155-129">Дополнительные сведения см. в разделе [передачи данных с помощью служебной программы командной строки AzCopy](../storage/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="81155-129">To learn more, see [Transfer data with the AzCopy Command-Line Utility](../storage/storage-use-azcopy.md).</span></span> 
#### <a name="download-all-blobs-to-local-disk"></a><span data-ttu-id="81155-130">Загрузить все большие двоичные объекты на локальный диск</span><span class="sxs-lookup"><span data-stu-id="81155-130">Download all blobs to local disk</span></span>
```azcopy
AzCopy.exe /source:https://myaccount.blob.local.azurestack.external/mycontainer /dest:C:\myfolder /sourcekey:<key> /S
```
#### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="81155-131">Отправка одного файла в виртуальный каталог</span><span class="sxs-lookup"><span data-stu-id="81155-131">Upload single file to virtual directory</span></span> 
```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.local.azurestack.external/mycontainer/vd /DestKey:key /Pattern:abc.txt
```
#### <a name="move-data-between-azure-and-azure-stack-storage"></a><span data-ttu-id="81155-132">Перемещение данных между Azure и стек хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="81155-132">Move data between Azure and Azure Stack Storage</span></span> 
<span data-ttu-id="81155-133">Асинхронную передачу данных между хранилища Azure и Azure стека не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="81155-133">Asynchronous data transfer between Azure Storage and Azure Stack is not supported.</span></span> <span data-ttu-id="81155-134">необходимо указать передачу данных с `/SyncCopy` параметр.</span><span class="sxs-lookup"><span data-stu-id="81155-134">you need to specify the transfer with the `/SyncCopy` option.</span></span> 
```azcopy 
Azcopy /Source:https://myaccount.blob.local.azurestack.external/mycontainer /Dest:https://myaccount2.blob.core.windows.net/mycontainer2 /SourceKey:AzSKey /DestKey:Azurekey /S /SyncCopy
```

### <a name="azcopy-known-issues"></a><span data-ttu-id="81155-135">Azcopy. Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="81155-135">Azcopy Known issues</span></span>
* <span data-ttu-id="81155-136">Любая операция AzCopy для хранения файлов не доступен, поскольку еще не доступен в Azure стек хранилища файлов.</span><span class="sxs-lookup"><span data-stu-id="81155-136">Any AzCopy operation on File storage is not available because File Storage is not yet available in Azure Stack.</span></span>
* <span data-ttu-id="81155-137">Асинхронную передачу данных между хранилища Azure и Azure стека не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="81155-137">Asynchronous data transfer between Azure Storage and Azure Stack is not supported.</span></span> <span data-ttu-id="81155-138">Можно указать передачу данных с `/SyncCopy` параметр, чтобы скопировать данные.</span><span class="sxs-lookup"><span data-stu-id="81155-138">You can specify the transfer with the `/SyncCopy` option to copy the data.</span></span>
* <span data-ttu-id="81155-139">Azcopy версию Linux не поддерживается для стека хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="81155-139">The Linux version of Azcopy is not supported for Azure Stack Storage.</span></span> 

## <a name="azure-powershell"></a><span data-ttu-id="81155-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="81155-140">Azure PowerShell</span></span>
<span data-ttu-id="81155-141">Azure PowerShell — это модуль, который предоставляет командлеты для управления службами в Azure и Azure стека.</span><span class="sxs-lookup"><span data-stu-id="81155-141">Azure PowerShell is a module that provides cmdlets for managing services on both Azure and Azure Stack.</span></span> <span data-ttu-id="81155-142">Это оболочка командной строки для выполнения задач и язык сценариев, разработанный специально для администрирования системы.</span><span class="sxs-lookup"><span data-stu-id="81155-142">It's a task-based command-line shell and scripting language designed especially for system administration.</span></span>

### <a name="install-and-configure-powershell-for-azure-stack"></a><span data-ttu-id="81155-143">Установите и настройте PowerShell для Azure стека</span><span class="sxs-lookup"><span data-stu-id="81155-143">Install and Configure PowerShell for Azure Stack</span></span>
<span data-ttu-id="81155-144">Совместимые модули Azure PowerShell Azure стека необходимых для работы с Azure стека.</span><span class="sxs-lookup"><span data-stu-id="81155-144">Azure Stack compatible Azure PowerShell modules are required to work with Azure Stack.</span></span> <span data-ttu-id="81155-145">Дополнительные сведения см. в разделе [Установка PowerShell для Azure стека](azure-stack-powershell-install.md) и [настройки среды PowerShell Azure стека пользователя](azure-stack-powershell-configure-user.md) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="81155-145">For more information, see [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) and [Configure the Azure Stack user's PowerShell environment](azure-stack-powershell-configure-user.md) to learn more.</span></span>

### <a name="powershell-sample-script-for-azure-stack"></a><span data-ttu-id="81155-146">Сценарий PowerShell для Azure стека</span><span class="sxs-lookup"><span data-stu-id="81155-146">PowerShell Sample script for Azure Stack</span></span> 
<span data-ttu-id="81155-147">В этом примере предположим, что успешно [Установка PowerShell для Azure стека](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="81155-147">This sample assume you have successfully [Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span> <span data-ttu-id="81155-148">Этот сценарий способствуют conplete конфигурации и попросите вашего клиента Azure стека учетные данные, чтобы добавить свою учетную запись локального environemnt PowerShell.</span><span class="sxs-lookup"><span data-stu-id="81155-148">This script will help you conplete the configuration and ask your Azure Stack tenant credentials to add your account to the local PowerShell environemnt.</span></span> <span data-ttu-id="81155-149">Затем скрипт будет задать значение по умолчанию подписки Azure, создание новой учетной записи хранения в Azure, создать контейнер в этой новой учетной записи хранения и передачи существующего файла изображения (blob) в конкретном контейнере.</span><span class="sxs-lookup"><span data-stu-id="81155-149">Then, the script will set the default Azure subscription, create a new storage account in Azure, create a new container in this new storage account and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="81155-150">После этого сценарий выводит список всех BLOB-объектов в этом контейнере, создает новый каталог назначения на локальном компьютере и загружает файл образа.</span><span class="sxs-lookup"><span data-stu-id="81155-150">After the script lists all blobs in that container, it will create a new destination directory in your local computer and download the image file.</span></span>

1. <span data-ttu-id="81155-151">Установка [модули Azure PowerShell Azure стека совместимой](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="81155-151">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
2. <span data-ttu-id="81155-152">Загрузить [инструменты, необходимые для работы с Azure стека](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="81155-152">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span>  
3. <span data-ttu-id="81155-153">Откройте **интегрированной среды Сценариев Windows PowerShell** и **Запуск от имени администратора**, нажмите кнопку **файл** > **New** для создания нового файла описания.</span><span class="sxs-lookup"><span data-stu-id="81155-153">Open **Windows PowerShell ISE** and **Run as Administrator**, click **File** > **New** to create a new script file.</span></span>
4. <span data-ttu-id="81155-154">Скопируйте приведенный ниже скрипт и вставьте в новый файл скрипта.</span><span class="sxs-lookup"><span data-stu-id="81155-154">Copy the script below and paste to the new script file.</span></span>
5. <span data-ttu-id="81155-155">Обновите переменные сценария, на основе заданных параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="81155-155">Update the script variables based on your configuration settings.</span></span> 
6. <span data-ttu-id="81155-156">Примечание: этот скрипт должен быть запущен в корне загруженный **AzureStack_Tools**.</span><span class="sxs-lookup"><span data-stu-id="81155-156">Note: this script has to be run under the root of downloaded **AzureStack_Tools**.</span></span> 

```PowerShell 
# begin

$ARMEvnName = "AzureStackUser" # set AzureStackUser as your Azure Stack environemnt name
$ARMEndPoint = "https://management.local.azurestack.external" 
$GraphAudiance = "https://graph.windows.net/" 
$AADTenantName = "<myDirectoryTenantName>.onmicrosoft.com" 

$SubscriptionName = "basic" # Update with the name of your subscription.
$ResourceGroupName = "myTestRG" # Give a name to your new resource group.
$StorageAccountName = "azsblobcontainer" # Give a name to your new storage account. It must be lowercase!
$Location = "Local" # Choose "Local" as an example.
$ContainerName = "photo" # Give a name to your new container.
$ImageToUpload = "C:\temp\Hello.jpg" # Prepare an image file and a source directory in your local computer.
$DestinationFolder = "C:\temp\downlaod" # A destination directory in your local computer.

# Import the Connect PowerShell module"
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
Import-Module .\Connect\AzureStack.Connect.psm1

# Configure the PowerShell environment
# Register an AzureRM environment that targets your Azure Stack instance
Add-AzureRmEnvironment -Name $ARMEvnName -ARMEndpoint $ARMEndPoint 

# Set the GraphEndpointResourceId value
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

# Download blobs from the container:
# Get a reference to a list of all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName

# Create the destination directory.
New-Item -Path $DestinationFolder -ItemType Directory -Force  

# Download blobs into the local destination directory.
$blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder

# end
```

### <a name="powershell-known-issues"></a><span data-ttu-id="81155-157">PowerShell известные проблемы</span><span class="sxs-lookup"><span data-stu-id="81155-157">PowerShell Known Issues</span></span> 
<span data-ttu-id="81155-158">Текущий совместимую версию модуля Azure PowerShell для Azure стека — 1.2.10.</span><span class="sxs-lookup"><span data-stu-id="81155-158">The current compatible Azure PowerShell module version for Azure Stack is 1.2.10.</span></span> <span data-ttu-id="81155-159">Оно отличается от последней версии Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="81155-159">It’s different from the latest version of Azure PowerShell.</span></span> <span data-ttu-id="81155-160">Это различие влияет на операции службы хранилища:</span><span class="sxs-lookup"><span data-stu-id="81155-160">This difference impacts storage services operation:</span></span>

* <span data-ttu-id="81155-161">Формат возвращаемого значения `Get-AzureRmStorageAccountKey` в версии 1.2.10 имеет два свойства: `Key1` и `Key2`, а в текущей версии Azure возвращает массив, содержащий все ключи учетной записи.</span><span class="sxs-lookup"><span data-stu-id="81155-161">The return value format of `Get-AzureRmStorageAccountKey` in version 1.2.10 has two properties: `Key1` and `Key2`, while the current Azure version returns an array containing all the account keys.</span></span>
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
   <span data-ttu-id="81155-162">Дополнительные сведения см. в разделе [Get AzureRmStorageAccountKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0).</span><span class="sxs-lookup"><span data-stu-id="81155-162">For more information, see [Get-AzureRmStorageAccountKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0).</span></span>

## <a name="azure-cli"></a><span data-ttu-id="81155-163">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="81155-163">Azure CLI</span></span>
<span data-ttu-id="81155-164">Azure CLI оказывается Azure командной строки для управления ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="81155-164">The Azure CLI is Azure’s command-line experience for managing Azure resources.</span></span> <span data-ttu-id="81155-165">Можно установить на Windows, Linux и macOS и запустите его из командной строки.</span><span class="sxs-lookup"><span data-stu-id="81155-165">You can install it on macOS, Linux, and Windows and run it from the command line.</span></span> 

<span data-ttu-id="81155-166">Azure CLI оптимизирована для управления и администрирования ресурсы Azure из командной строки, а также для создания сценариев автоматизации, которые работают от диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="81155-166">Azure CLI is optimized for managing and administering Azure resources from the command line, and for building automation scripts that work against the Azure Resource Manager.</span></span> <span data-ttu-id="81155-167">Он поддерживает многие функции, найти на портале Azure стека, включая доступ сложных данных.</span><span class="sxs-lookup"><span data-stu-id="81155-167">It provides many of the same functions found in the Azure Stack portal, including rich data access.</span></span>

<span data-ttu-id="81155-168">Стек Azure требует Azure CLI версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="81155-168">Azure Stack requires Azure CLI version 2.0.</span></span> <span data-ttu-id="81155-169">Дополнительные сведения об установке и настройке Azure CLI со стеком Azure см. в разделе [установить и настроить Azure CLI стека](azure-stack-connect-cli.md).</span><span class="sxs-lookup"><span data-stu-id="81155-169">For more information about installing and configuring Azure CLI with Azure Stack, see [Install and configure Azure Stack CLI](azure-stack-connect-cli.md).</span></span> <span data-ttu-id="81155-170">Дополнительные сведения об использовании Azure CLI 2.0 для выполнения нескольких задач, работы с ресурсами в вашей учетной записи хранилища Azure стека см. в разделе [с помощью Azure CLI2.0 со службой хранилища Azure](../storage/storage-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="81155-170">For more information about how to use the Azure CLI 2.0 to perform several tasks working with resources in your Azure Stack Storage account, see [Using the Azure CLI2.0 with Azure Storage](../storage/storage-azure-cli.md)</span></span>

### <a name="azure-cli-sample-script-for-azure-stack"></a><span data-ttu-id="81155-171">Образец сценария Azure CLI для стека Azure</span><span class="sxs-lookup"><span data-stu-id="81155-171">Azure CLI sample script for Azure Stack</span></span> 
<span data-ttu-id="81155-172">После завершения установки CLI и настройки вы выполните следующие действия для работы с небольшой образец сценарий для взаимодействия с ресурсами стек хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="81155-172">Once you complete the CLI installation and configuration, you can try the following steps to work with a small shell sample script to interact with Azure Stack Storage resources.</span></span> <span data-ttu-id="81155-173">Скрипт сначала создает новый контейнер в учетной записи затем загружает существующий файл (в виде больших двоичных объектов) в конкретном контейнере, перечислены все большие двоичные объекты в контейнере и и, наконец, загружает файл в место назначения на локальном компьютере, который можно указать.</span><span class="sxs-lookup"><span data-stu-id="81155-173">The script first creates a new container in your storage account, then uploads an existing file (as a blob) to that container, lists all blobs in the container, and finally, downloads the file to a destination on your local computer that you specify.</span></span> <span data-ttu-id="81155-174">Прежде чем запустить этот сценарий, убедитесь, что подключение выполнено успешно и подключение к конечному объекту Azure стека.</span><span class="sxs-lookup"><span data-stu-id="81155-174">Before you run this script, make sure you successfully connect and login to the target Azure Stack.</span></span> 
1. <span data-ttu-id="81155-175">Откройте текстовый редактор по выбору, а затем скопируйте и вставьте в него предыдущий скрипт.</span><span class="sxs-lookup"><span data-stu-id="81155-175">Open your favorite text editor, then copy and paste the preceding script into the editor.</span></span>
2. <span data-ttu-id="81155-176">Обновите переменные сценария в соответствии параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="81155-176">Update the script's variables to reflect your configuration settings.</span></span> 
3. <span data-ttu-id="81155-177">После обновления необходимых переменных сохраните скрипт и выйдите из редактора.</span><span class="sxs-lookup"><span data-stu-id="81155-177">After you've updated the necessary variables, save the script and exit your editor.</span></span> <span data-ttu-id="81155-178">Далее предполагается, что действия с названием my_storage_sample.sh ваш скрипт.</span><span class="sxs-lookup"><span data-stu-id="81155-178">The next steps assume you've named your script my_storage_sample.sh.</span></span>
4. <span data-ttu-id="81155-179">При необходимости пометьте скрипт как исполняемый файл: `chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="81155-179">Mark the script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>
5. <span data-ttu-id="81155-180">Выполните скрипт,</span><span class="sxs-lookup"><span data-stu-id="81155-180">Execute the script.</span></span> <span data-ttu-id="81155-181">например в Bash: `./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="81155-181">For example, in Bash: `./my_storage_sample.sh`</span></span>

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

echo "Creating the resource group..."
az group create --name $AZURESTACK_RESOURCE_GROUP --location $AZURESTACK_RG_LOCATION

echo "Creating the storage account..."
az storage account create --name $AZURESTACK_STORAGE_ACCOUNT_NAME --resource-group $AZURESTACK_RESOURCE_GROUP --account-type Standard_LRS

echo "Creating the blob container..."
az storage container create --name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME

echo "Uploading the file..."
az storage blob upload --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --file $FILE_TO_UPLOAD --name $AZURESTACK_STORAGE_BLOB_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME

echo "Listing the blobs..."
az storage blob list --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME --output table

echo "Downloading the file..."
az storage blob download --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME --name $AZURESTACK_STORAGE_BLOB_NAME --file $DESTINATION_FILE --output table

echo "Done"
```

## <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="81155-182">Обозреватель службы хранилища Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="81155-182">Microsoft Azure Storage Explorer</span></span>

<span data-ttu-id="81155-183">Обозреватель хранилищ Microsoft Azure — отдельное приложение от Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="81155-183">Microsoft Azure Storage Explorer is a standalone app from Microsoft.</span></span> <span data-ttu-id="81155-184">Он позволяет легко работать с хранилища Azure и Azure стек хранилища данных в Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="81155-184">It allows you to easily work with both Azure Storage and Azure Stack Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="81155-185">Если требуется простой способ управления данные стека хранилища Azure, рассмотрите возможность использования обозревателя хранилища Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="81155-185">If you want an easy way to manage your Azure Stack Storage data, then consider using Microsoft Azure Storage Explorer.</span></span>

<span data-ttu-id="81155-186">Дополнительные сведения о настройке обозреватель хранилища Azure для работы со стеком Azure см. в разделе [подключить обозреватель хранилища с подпиской Azure стека](azure-stack-storage-connect-se.md).</span><span class="sxs-lookup"><span data-stu-id="81155-186">For more information about configuring Azure Storage Explorer to work with Azure Stack, see [Connect Storage Explorer to an Azure Stack subscription](azure-stack-storage-connect-se.md).</span></span>

<span data-ttu-id="81155-187">Дополнительные сведения об обозревателе хранилища Microsoft Azure см. в разделе [приступить к работе с помощью обозревателя хранилища (Предварительная версия)](../vs-azure-tools-storage-manage-with-storage-explorer.md)</span><span class="sxs-lookup"><span data-stu-id="81155-187">For more information about Microsoft Azure Storage Explorer, see [Get started with Storage Explorer (Preview)](../vs-azure-tools-storage-manage-with-storage-explorer.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="81155-188">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="81155-188">Next steps</span></span>
* [<span data-ttu-id="81155-189">Подключаться к подписке Azure стека обозреватель хранилищ</span><span class="sxs-lookup"><span data-stu-id="81155-189">Connect Storage Explorer to an Azure Stack subscription</span></span>](azure-stack-storage-connect-se.md)
* [<span data-ttu-id="81155-190">Приступая к работе с обозреватель хранилищ (Предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="81155-190">Get started with Storage Explorer (Preview)</span></span>](../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [<span data-ttu-id="81155-191">Хранилище Azure согласованное: различия и рекомендации</span><span class="sxs-lookup"><span data-stu-id="81155-191">Azure-consistent storage: differences and considerations</span></span>](azure-stack-acs-differences.md)
* [<span data-ttu-id="81155-192">Введение в службу хранилища Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="81155-192">Introduction to Microsoft Azure Storage</span></span>](../storage/common/storage-introduction.md)

