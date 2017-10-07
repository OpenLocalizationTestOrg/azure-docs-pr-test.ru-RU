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
# <a name="tools-for-azure-stack-storage"></a>Набор средств для хранения стек Azure

Стека Microsoft Azure предоставляет набор служб хранилища hello дисков, больших двоичных объектов, таблиц, очередей и функции управления учетной записи. Набор средств хранилища Azure можно использовать при необходимости toomanage или при перемещении данных tooor из стека хранилища Azure. В этой статье предоставляет краткий обзор средств hello.

Hello средство, которое лучше всего подходит для вас зависит от требований:
* [AzCopy](#azcopy)

    Программа командной строки специфичные для хранилища, что toocopy данных можно загрузить из tooanother один объект в вашей учетной записи хранения или между учетными записями хранения.

* [Azure PowerShell](#azure-powershell)

    Оболочка командной строки на основе задач и язык сценариев, предназначенный специально для системного администрирования.

* [Интерфейс командной строки Azure](#azure-cli)

    Открытая, кросс платформенных в это средство, которое предоставляет набор команд для работы с платформы Azure и Azure стека hello.

* [Обозреватель хранилищ Microsoft (Предварительная версия)](#microsoft-azure-storage-explorer)

    Отдельное приложение легко toouse с пользовательским интерфейсом.

Из-за toohello хранилища служб различия между Azure и Azure стека может возникнуть определенные требования для каждого средства, описанные в следующих разделах hello. Сравнение между Azure и хранилищем Azure стека см. в разделе [стек хранилища Azure: различия и рекомендации](azure-stack-acs-differences.md).


## <a name="azcopy"></a>AzCopy
AzCopy является tooand данные командной строки служебная программа разработанная toocopy из хранилища больших двоичных объектов Microsoft Azure и таблицы с помощью простой команды с оптимальной производительностью. Можно скопировать данные из одного объекта tooanother в вашей учетной записи хранения или между учетными записями хранения. Существует две версии hello AzCopy: AzCopy в Windows и AzCopy в Linux. Стек Azure поддерживает только версия Windows hello. 
 
### <a name="download-and-install-azcopy"></a>Скачивание и установка AzCopy 
[Загрузите](https://aka.ms/azcopyforazurestack) версию Windows hello поддерживается AzCopy для Azure стека. Можно установить и использовать AzCopy на hello стек Azure так же, как Azure. toolearn более, в разделе [перенесите данные с помощью служебной программы командной строки AzCopy hello](../storage/common/storage-use-azcopy.md). 

### <a name="azcopy-command-examples-for-data-transfer"></a>Примеры команды AzCopy для передачи данных
Привет, следующие примеры демонстрируют несколько типичных сценариях для копирования данных tooand из стека Azure BLOB-объектов. toolearn более, в разделе [перенесите данные с помощью служебной программы командной строки AzCopy hello](../storage/storage-use-azcopy.md). 
#### <a name="download-all-blobs-toolocal-disk"></a>Загрузка диска toolocal все большие двоичные объекты
```azcopy
AzCopy.exe /source:https://myaccount.blob.local.azurestack.external/mycontainer /dest:C:\myfolder /sourcekey:<key> /S
```
#### <a name="upload-single-file-toovirtual-directory"></a>Отправка одного файла каталога toovirtual 
```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.local.azurestack.external/mycontainer/vd /DestKey:key /Pattern:abc.txt
```
#### <a name="move-data-between-azure-and-azure-stack-storage"></a>Перемещение данных между Azure и стек хранилища Azure 
Асинхронную передачу данных между хранилища Azure и Azure стека не поддерживается. требуется передача hello toospecify с hello `/SyncCopy` параметр. 
```azcopy 
Azcopy /Source:https://myaccount.blob.local.azurestack.external/mycontainer /Dest:https://myaccount2.blob.core.windows.net/mycontainer2 /SourceKey:AzSKey /DestKey:Azurekey /S /SyncCopy
```

### <a name="azcopy-known-issues"></a>Azcopy. Известные проблемы
* Любая операция AzCopy для хранения файлов не доступен, поскольку еще не доступен в Azure стек хранилища файлов.
* Асинхронную передачу данных между хранилища Azure и Azure стека не поддерживается. Можно указать hello передачи с hello `/SyncCopy` toocopy hello данные.
* версии Linux Hello Azcopy не поддерживается для стека хранилища Azure. 

## <a name="azure-powershell"></a>Azure PowerShell
Azure PowerShell — это модуль, который предоставляет командлеты для управления службами в Azure и Azure стека. Это оболочка командной строки для выполнения задач и язык сценариев, разработанный специально для администрирования системы.

### <a name="install-and-configure-powershell-for-azure-stack"></a>Установите и настройте PowerShell для Azure стека
Совместимые модули Azure PowerShell Azure стека являются обязательным toowork со стеком Azure. Дополнительные сведения см. в разделе [Установка PowerShell для Azure стека](azure-stack-powershell-install.md) и [настройки среды PowerShell hello Azure стека пользователя](azure-stack-powershell-configure-user.md) toolearn дополнительные.

### <a name="powershell-sample-script-for-azure-stack"></a>Сценарий PowerShell для Azure стека 
В этом примере предположим, что успешно [Установка PowerShell для Azure стека](azure-stack-powershell-install.md). Этот скрипт будет помогают conplete hello конфигурации и попросите вашего клиента Azure стека учетных данных tooadd вашей учетной записи toohello локального PowerShell environemnt. Затем сценарий hello будет по умолчанию hello подписки Azure, создание новой учетной записи хранения в Azure, создать контейнер в этой новой учетной записи хранения и отправить существующий контейнер toothat образ файла (blob). После hello скрипт перечисляет все большие двоичные объекты в этом контейнере, создает новый каталог назначения на своем локальном компьютере и загрузите файл изображения hello.

1. Установка [модули Azure PowerShell Azure стека совместимой](azure-stack-powershell-install.md).  
2. Загрузите hello [toowork необходимые средства с Azure стека](azure-stack-powershell-download.md).  
3. Откройте **интегрированной среды Сценариев Windows PowerShell** и **Запуск от имени администратора**, нажмите кнопку **файл** > **New** toocreate новый файл скрипта.
4. Скопируйте приведенный ниже сценарий hello и вставьте toohello новый файл скрипта.
5. Обновление переменных сценария hello на основании параметров конфигурации. 
6. Примечание: этот скрипт содержит toobe запуска в корне hello загруженный **AzureStack_Tools**. 

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

### <a name="powershell-known-issues"></a>PowerShell известные проблемы 
Hello текущего совместимые Azure PowerShell модуль для стека Azure имеет версию 1.2.10. Оно отличается от hello последнюю версию Azure PowerShell. Это различие влияет на операции службы хранилища:

* Формат возвращаемого значения Hello `Get-AzureRmStorageAccountKey` в версии 1.2.10 имеет два свойства: `Key1` и `Key2`, а в текущей версии Azure hello возвращает массив, содержащий все ключи учетной записи hello.
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
Hello Azure CLI оказывается Azure командной строки для управления ресурсами Azure. Можно установить на Windows, Linux и macOS и запустите его из командной строки hello. 

Azure CLI оптимизирована для управления и администрирования из командной строки hello ресурсы Azure, а также для создания сценариев автоматизации, которые работают с hello диспетчера ресурсов Azure. Он предоставляет многие hello найти на портале Azure стека hello, включая доступ сложных данных те же функции.

Стек Azure требует Azure CLI версии 2.0. Дополнительные сведения об установке и настройке Azure CLI со стеком Azure см. в разделе [установить и настроить Azure CLI стека](azure-stack-connect-cli.md). Дополнительные сведения о том, как tooperform hello Azure CLI 2.0 toouse несколько задач, работы с ресурсами в вашей учетной записи хранилища Azure стека, отображается [Using hello Azure CLI2.0 со службой хранилища Azure](../storage/storage-azure-cli.md)

### <a name="azure-cli-sample-script-for-azure-stack"></a>Образец сценария Azure CLI для стека Azure 
После завершения установки CLI hello и настройки можно попробовать следующие шаги toowork с toointeract сценария небольшой оболочки образец с ресурсов хранилища Azure стека hello. Hello скрипт сначала создает новый контейнер в учетной записи затем загружает существующий контейнер toothat файла (в виде больших двоичных объектов), перечислены все большие двоичные объекты в контейнере hello и и, наконец, загружает hello назначения tooa файл на локальном компьютере, который можно указать. Прежде чем запустить этот сценарий, убедитесь, что подключение выполнено успешно и целевой toohello входа Azure стека. 
1. Откройте текстовый редактор, затем скопируйте и вставьте hello предшествующий скрипт в редактор hello.
2. Обновление параметров конфигурации tooreflect переменные сценария hello. 
3. После обновления hello необходимые переменные, сохранить сценарий hello и выйти из редактора. Hello Далее предполагается, что действия с названием my_storage_sample.sh вашего сценария.
4. Пометка hello скрипта как исполняемый файл и при необходимости:`chmod +x my_storage_sample.sh`
5. Выполнение скрипта hello. например в Bash: `./my_storage_sample.sh`

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

## <a name="microsoft-azure-storage-explorer"></a>Обозреватель службы хранилища Microsoft Azure

Обозреватель хранилищ Microsoft Azure — отдельное приложение от Майкрософт. Она позволяет tooeasily при обработке хранилища Azure и Azure стек хранилища данных в Windows, macOS и Linux. Если требуется простой способ toomanage данные стека хранилища Azure, рассмотрите возможность использования обозревателя хранилища Microsoft Azure.

Дополнительные сведения о настройке toowork обозреватель хранилищ Azure со стеком Azure в разделе [tooan подключить обозреватель хранилища Azure стека подписки](azure-stack-storage-connect-se.md).

Дополнительные сведения об обозревателе хранилища Microsoft Azure см. в разделе [приступить к работе с помощью обозревателя хранилища (Предварительная версия)](../vs-azure-tools-storage-manage-with-storage-explorer.md)

## <a name="next-steps"></a>Дальнейшие действия
* [Подключение подписки Azure стека tooan обозреватель хранилищ](azure-stack-storage-connect-se.md)
* [Приступая к работе с обозреватель хранилищ (Предварительная версия)](../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [Хранилище Azure согласованное: различия и рекомендации](azure-stack-acs-differences.md)
* [Введение tooMicrosoft хранилища Azure](../storage/common/storage-introduction.md)

