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
# <a name="tools-for-azure-stack-storage"></a>Набор средств для хранения стек Azure

Стека Microsoft Azure предоставляет набор дисков, больших двоичных объектов, таблиц, очередей и функции управления учетной записи службы хранилища. Набор средств хранилища Azure можно использовать, если вы хотите управлять, или переместить данные или из стека хранилища Azure. Также приводятся общие сведения об инструментах.

Средство, которое лучше всего подходит для вас зависит от требований:
* [AzCopy](#azcopy)

    Программа командной строки специфичные для хранилища, которую можно загрузить для копирования данных из одного объекта в другой в вашей учетной записи хранения или между учетными записями хранения.

* [Azure PowerShell](#azure-powershell)

    Оболочка командной строки на основе задач и язык сценариев, предназначенный специально для системного администрирования.

* [Интерфейс командной строки Azure](#azure-cli)

    Открытая, кросс платформенных в это средство, которое предоставляет набор команд для работы с платформы Azure и Azure стека.

* [Обозреватель хранилищ Microsoft (Предварительная версия)](#microsoft-azure-storage-explorer)

    Простой в использовании автономные приложения с пользовательским интерфейсом.

Из-за различий служб хранения данных между Azure и Azure стека может возникнуть определенные требования для каждого средства, описанные в следующих разделах. Сравнение между Azure и хранилищем Azure стека см. в разделе [стек хранилища Azure: различия и рекомендации](azure-stack-acs-differences.md).


## <a name="azcopy"></a>AzCopy
AzCopy является командной строки служебная программа, разработанная для копирования данных из больших двоичных объектов Microsoft Azure и хранилище таблиц с помощью простой команды с оптимальной производительностью. Кроме того, она позволяет копировать данные из одного объекта в другой в пределах одной учетной записи хранения или из одной такой записи в другую. Существует две версии AzCopy: AzCopy в Windows и AzCopy в Linux. Стек Azure поддерживает только версии Windows. 
 
### <a name="download-and-install-azcopy"></a>Скачивание и установка AzCopy 
[Загрузить](https://aka.ms/azcopyforazurestack) AzCopy для стека Azure о поддерживаемых версиях Windows. Можно установить и использовать AzCopy в стеке Azure так же, как Azure. Дополнительные сведения см. в разделе [передачи данных с помощью служебной программы командной строки AzCopy](../storage/common/storage-use-azcopy.md). 

### <a name="azcopy-command-examples-for-data-transfer"></a>Примеры команды AzCopy для передачи данных
В следующих примерах демонстрируется несколько типичных сценариях для передачи данных между стек Azure BLOB-объектов. Дополнительные сведения см. в разделе [передачи данных с помощью служебной программы командной строки AzCopy](../storage/storage-use-azcopy.md). 
#### <a name="download-all-blobs-to-local-disk"></a>Загрузить все большие двоичные объекты на локальный диск
```azcopy
AzCopy.exe /source:https://myaccount.blob.local.azurestack.external/mycontainer /dest:C:\myfolder /sourcekey:<key> /S
```
#### <a name="upload-single-file-to-virtual-directory"></a>Отправка одного файла в виртуальный каталог 
```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.local.azurestack.external/mycontainer/vd /DestKey:key /Pattern:abc.txt
```
#### <a name="move-data-between-azure-and-azure-stack-storage"></a>Перемещение данных между Azure и стек хранилища Azure 
Асинхронную передачу данных между хранилища Azure и Azure стека не поддерживается. необходимо указать передачу данных с `/SyncCopy` параметр. 
```azcopy 
Azcopy /Source:https://myaccount.blob.local.azurestack.external/mycontainer /Dest:https://myaccount2.blob.core.windows.net/mycontainer2 /SourceKey:AzSKey /DestKey:Azurekey /S /SyncCopy
```

### <a name="azcopy-known-issues"></a>Azcopy. Известные проблемы
* Любая операция AzCopy для хранения файлов не доступен, поскольку еще не доступен в Azure стек хранилища файлов.
* Асинхронную передачу данных между хранилища Azure и Azure стека не поддерживается. Можно указать передачу данных с `/SyncCopy` параметр, чтобы скопировать данные.
* Azcopy версию Linux не поддерживается для стека хранилища Azure. 

## <a name="azure-powershell"></a>Azure PowerShell
Azure PowerShell — это модуль, который предоставляет командлеты для управления службами в Azure и Azure стека. Это оболочка командной строки для выполнения задач и язык сценариев, разработанный специально для администрирования системы.

### <a name="install-and-configure-powershell-for-azure-stack"></a>Установите и настройте PowerShell для Azure стека
Совместимые модули Azure PowerShell Azure стека необходимых для работы с Azure стека. Дополнительные сведения см. в разделе [Установка PowerShell для Azure стека](azure-stack-powershell-install.md) и [настройки среды PowerShell Azure стека пользователя](azure-stack-powershell-configure-user.md) для получения дополнительных сведений.

### <a name="powershell-sample-script-for-azure-stack"></a>Сценарий PowerShell для Azure стека 
В этом примере предположим, что успешно [Установка PowerShell для Azure стека](azure-stack-powershell-install.md). Этот сценарий способствуют conplete конфигурации и попросите вашего клиента Azure стека учетные данные, чтобы добавить свою учетную запись локального environemnt PowerShell. Затем скрипт будет задать значение по умолчанию подписки Azure, создание новой учетной записи хранения в Azure, создать контейнер в этой новой учетной записи хранения и передачи существующего файла изображения (blob) в конкретном контейнере. После этого сценарий выводит список всех BLOB-объектов в этом контейнере, создает новый каталог назначения на локальном компьютере и загружает файл образа.

1. Установка [модули Azure PowerShell Azure стека совместимой](azure-stack-powershell-install.md).  
2. Загрузить [инструменты, необходимые для работы с Azure стека](azure-stack-powershell-download.md).  
3. Откройте **интегрированной среды Сценариев Windows PowerShell** и **Запуск от имени администратора**, нажмите кнопку **файл** > **New** для создания нового файла описания.
4. Скопируйте приведенный ниже скрипт и вставьте в новый файл скрипта.
5. Обновите переменные сценария, на основе заданных параметров конфигурации. 
6. Примечание: этот скрипт должен быть запущен в корне загруженный **AzureStack_Tools**. 

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

### <a name="powershell-known-issues"></a>PowerShell известные проблемы 
Текущий совместимую версию модуля Azure PowerShell для Azure стека — 1.2.10. Оно отличается от последней версии Azure PowerShell. Это различие влияет на операции службы хранилища:

* Формат возвращаемого значения `Get-AzureRmStorageAccountKey` в версии 1.2.10 имеет два свойства: `Key1` и `Key2`, а в текущей версии Azure возвращает массив, содержащий все ключи учетной записи.
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
   Дополнительные сведения см. в разделе [Get AzureRmStorageAccountKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0).

## <a name="azure-cli"></a>Инфраструктура CLI Azure
Azure CLI оказывается Azure командной строки для управления ресурсами Azure. Можно установить на Windows, Linux и macOS и запустите его из командной строки. 

Azure CLI оптимизирована для управления и администрирования ресурсы Azure из командной строки, а также для создания сценариев автоматизации, которые работают от диспетчера ресурсов Azure. Он поддерживает многие функции, найти на портале Azure стека, включая доступ сложных данных.

Стек Azure требует Azure CLI версии 2.0. Дополнительные сведения об установке и настройке Azure CLI со стеком Azure см. в разделе [установить и настроить Azure CLI стека](azure-stack-connect-cli.md). Дополнительные сведения об использовании Azure CLI 2.0 для выполнения нескольких задач, работы с ресурсами в вашей учетной записи хранилища Azure стека см. в разделе [с помощью Azure CLI2.0 со службой хранилища Azure](../storage/storage-azure-cli.md)

### <a name="azure-cli-sample-script-for-azure-stack"></a>Образец сценария Azure CLI для стека Azure 
После завершения установки CLI и настройки вы выполните следующие действия для работы с небольшой образец сценарий для взаимодействия с ресурсами стек хранилища Azure. Скрипт сначала создает новый контейнер в учетной записи затем загружает существующий файл (в виде больших двоичных объектов) в конкретном контейнере, перечислены все большие двоичные объекты в контейнере и и, наконец, загружает файл в место назначения на локальном компьютере, который можно указать. Прежде чем запустить этот сценарий, убедитесь, что подключение выполнено успешно и подключение к конечному объекту Azure стека. 
1. Откройте текстовый редактор по выбору, а затем скопируйте и вставьте в него предыдущий скрипт.
2. Обновите переменные сценария в соответствии параметров конфигурации. 
3. После обновления необходимых переменных сохраните скрипт и выйдите из редактора. Далее предполагается, что действия с названием my_storage_sample.sh ваш скрипт.
4. При необходимости пометьте скрипт как исполняемый файл: `chmod +x my_storage_sample.sh`
5. Выполните скрипт, например в Bash: `./my_storage_sample.sh`

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

## <a name="microsoft-azure-storage-explorer"></a>Обозреватель службы хранилища Microsoft Azure

Обозреватель хранилищ Microsoft Azure — отдельное приложение от Майкрософт. Он позволяет легко работать с хранилища Azure и Azure стек хранилища данных в Windows, macOS и Linux. Если требуется простой способ управления данные стека хранилища Azure, рассмотрите возможность использования обозревателя хранилища Microsoft Azure.

Дополнительные сведения о настройке обозреватель хранилища Azure для работы со стеком Azure см. в разделе [подключить обозреватель хранилища с подпиской Azure стека](azure-stack-storage-connect-se.md).

Дополнительные сведения об обозревателе хранилища Microsoft Azure см. в разделе [приступить к работе с помощью обозревателя хранилища (Предварительная версия)](../vs-azure-tools-storage-manage-with-storage-explorer.md)

## <a name="next-steps"></a>Дальнейшие действия
* [Подключаться к подписке Azure стека обозреватель хранилищ](azure-stack-storage-connect-se.md)
* [Приступая к работе с обозреватель хранилищ (Предварительная версия)](../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [Хранилище Azure согласованное: различия и рекомендации](azure-stack-acs-differences.md)
* [Введение в службу хранилища Microsoft Azure](../storage/common/storage-introduction.md)

