---
title: "Средства для хранилища Azure Stack"
description: "Сведения о средствах передачи данных хранилища Azure Stack"
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
ms.date: 9/25/2017
ms.author: xiaofmao
ms.openlocfilehash: 9799498a11449a9ed496d0fdb40312603eda064e
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="tools-for-azure-stack-storage"></a>Средства для хранилища Azure Stack

*Область применения: интегрированные системы Azure Stack и комплект разработки Azure Stack*

Microsoft Azure Stack предоставляет набор служб хранения для дисков, больших двоичных объектов, таблиц, очередей и функций управления учетными записями. Набор средств хранилища Azure можно использовать, если вы хотите управлять данными в хранилище Azure Stack или вам требуется перенести их из этого хранилища или в него. В этой статье содержится общий обзор доступных средств.

Самое оптимальное для вас средство зависит от ваших требований:
* [AzCopy](#azcopy)

    Программа командной строки, предназначенная для хранения, которую вы можете загрузить для копирования данных из одного объекта в другой в пределах одной учетной записи хранения или из одной такой записи в другую.

* [Azure PowerShell](#azure-powershell)

    Оболочка командной строки для выполнения задач и язык сценариев, разработанный специально для администрирования системы.

* [Интерфейс командной строки Azure](#azure-cli)

    Кроссплатформенное средство с открытым кодом, которое предоставляет набор команд для работы с платформами Azure и Azure Stack.

* [Обозреватель службы хранилища Microsoft (предварительная версия)](#microsoft-azure-storage-explorer)

    Простое в использовании автономное приложение с пользовательским интерфейсом.

Из-за различий служб хранения между Azure и Azure Stack для каждого средства могут существовать некоторые специфические требования, описанные в следующих разделах. Сравнение между хранилищем Azure и Azure Stack см. в статье [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md) (Хранилище Azure Stack. Отличия и рекомендации).


## <a name="azcopy"></a>AzCopy
AzCopy — это служебная программа командной строки. Она предназначена для копирования данных из хранилища BLOB-объектов и хранилища таблиц Microsoft Azure (и обратно) с помощью простых команд, обеспечивающих оптимальную производительность. Кроме того, она позволяет копировать данные из одного объекта в другой в пределах одной учетной записи хранения или из одной такой записи в другую. Существует две версии AzCopy: AzCopy в Windows и AzCopy в Linux. Azure Stack поддерживает только версию Windows. 
 
### <a name="download-and-install-azcopy"></a>Скачивание и установка AzCopy 
[Скачайте](https://aka.ms/azcopyforazurestack) поддерживаемую версию Windows AzCopy для Azure Stack. Можно установить и использовать AzCopy в Azure так же, как в Azure. Дополнительные сведения см. в статье [Передача данных с помощью служебной программы командной строки AzCopy](../../storage/common/storage-use-azcopy.md). 

### <a name="azcopy-command-examples-for-data-transfer"></a>Примеры команд AzCopy для передачи данных
В приведенных ниже примерах описаны стандартные сценарии копирования данных в большие двоичные объекты Azure Stack и обратно. Дополнительные сведения см. в статье [Передача данных с помощью служебной программы командной строки AzCopy](../../storage/storage-use-azcopy.md). 
#### <a name="download-all-blobs-to-local-disk"></a>Скачивание всех больших двоичных объектов на локальный диск
```azcopy
AzCopy.exe /source:https://myaccount.blob.local.azurestack.external/mycontainer /dest:C:\myfolder /sourcekey:<key> /S
```
#### <a name="upload-single-file-to-virtual-directory"></a>Отправка одного файла в виртуальный каталог 
```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.local.azurestack.external/mycontainer/vd /DestKey:key /Pattern:abc.txt
```
#### <a name="move-data-between-azure-and-azure-stack-storage"></a>Перемещение данных между хранилищем Azure и Azure Stack 
Асинхронная передача данных между хранилищем Azure и Azure Stack не поддерживается. Для передачи данных необходимо указать параметр `/SyncCopy`. 
```azcopy 
Azcopy /Source:https://myaccount.blob.local.azurestack.external/mycontainer /Dest:https://myaccount2.blob.core.windows.net/mycontainer2 /SourceKey:AzSKey /DestKey:Azurekey /S /SyncCopy
```

### <a name="azcopy-known-issues"></a>Известные проблемы при использовании Azcopy
* Операцию AzCopy невозможно выполнить в хранилище файлов, так как оно еще не доступно в Azure Stack.
* Асинхронная передача данных между хранилищем Azure и Azure Stack не поддерживается. Вы можете указать передачу с помощью параметра `/SyncCopy`, чтобы копировать данные.
* Версия Azcopy для Linux не поддерживается в хранилище Azure Stack. 

## <a name="azure-powershell"></a>Azure PowerShell
Azure PowerShell — это модуль, предоставляющий командлеты для управления службами Azure и Azure Stack. Это оболочка командной строки для выполнения задач и язык сценариев, разработанный специально для администрирования системы.

### <a name="install-and-configure-powershell-for-azure-stack"></a>Установка и настройка PowerShell для использования с Azure Stack
Для работы с Azure Stack необходимы модули Azure PowerShell, совместимые с Azure Stack. Дополнительные сведения см. в статьях [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) (Установка PowerShell для использования с Azure Stack) и [Настройка пользовательской среды PowerShell в Azure Stack](azure-stack-powershell-configure-user.md).

### <a name="powershell-sample-script-for-azure-stack"></a>Пример скрипта PowerShell для Azure Stack 
В этом примере предполагается, что вы успешно установили [PowerShell для Azure Stack](azure-stack-powershell-install.md). Этот скрипт поможет вам выполнить настройку и попросить учетные данные клиента Azure Stack, чтобы добавить вашу учетную запись в локальную среду PowerShell. Затем скрипт настроит подписку Azure по умолчанию, создаст учетную запись хранения в Azure, создаст контейнер в этой новой учетной записи хранения и передаст существующий файл образа (большой двоичный объект) в этот контейнер. После этого сценарий выводит список всех BLOB-объектов в этом контейнере, создает новый каталог назначения на локальном компьютере и загружает файл образа.

1. Установите [совместимые с Azure Stack модули Azure PowerShell](azure-stack-powershell-install.md).  
2. Скачайте [средства, необходимые для работы с Azure Stack](azure-stack-powershell-download.md).  
3. Откройте **Windows PowerShell ISE**, **войдите как администратор** и щелкните **Файл** > **Создать**, чтобы создать файл скрипта.
4. Скопируйте приведенный ниже скрипт и вставьте его в новый файл скрипта.
5. Обновите переменные сценария на основе заданных параметров конфигурации. 
6. Примечание: этот скрипт должен быть запущен в корневом каталоге скачанных средств **AzureStack_Tools**. 

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

### <a name="powershell-known-issues"></a>Известные проблемы при работе с PowerShell 
Текущая совместимая версия модуля Azure PowerShell для Azure Stack — 1.2.10. Она отличается от последней версии Azure PowerShell. Это различие влияет на операции служб хранилища:

* Формат возвращаемого значения `Get-AzureRmStorageAccountKey` в версии 1.2.10 имеет два свойства: `Key1` и `Key2`. Текущая версия Azure возвращает массив, содержащий все ключи учетной записи.
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
   Дополнительные сведения см. в статье [Get-AzureRmStorageAccountKey](https://docs.microsoft.com/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0).

## <a name="azure-cli"></a>Инфраструктура CLI Azure
Azure CLI — это интерфейс командной строки Azure для управления ресурсами Azure. Его можно установить на macOS, Linux и Windows и запускать из командной строки. 

Интерфейс Azure CLI предназначен для администрирования ресурсов Azure из командной строки, а также для создания скриптов автоматизации, которые работают с Azure Resource Manager. Он предоставляет практически те же функции, что и портал Azure Stack, а также различные возможности доступа к данным.

Для работы с Azure Stack требуется Azure CLI версии 2.0. Дополнительные сведения об установке и настройке Azure CLI для работы с Azure Stack см. в статье [Install and configure CLI for use with Azure Stack](azure-stack-connect-cli.md) (Установка и настройка интерфейса командной строки для использования с Azure Stack). Дополнительные сведения о том, как использовать Azure CLI 2.0 для выполнения нескольких задач с ресурсами в вашей учетной записи хранения Azure Stack, см. в статье [Использование Azure CLI 2.0 со службой хранилища Azure](../../storage/storage-azure-cli.md)

### <a name="azure-cli-sample-script-for-azure-stack"></a>Пример скрипта Azure CLI для Azure Stack 
После завершения установки и настройки CLI вы можете выполнить следующие шаги для работы с небольшим образцом скрипта оболочки, чтобы взаимодействовать с ресурсами хранилища Azure Stack. Сначала скрипт создает контейнер в вашей учетной записи хранения, затем передает существующий файл (как большой двоичный объект) в этот контейнер, перечисляет все большие двоичные объекты в контейнере и, наконец, загружает файл в место назначения на указанном вами локальном компьютере. Прежде чем выполнить этот скрипт, убедитесь, что подключение и вход в целевой среде Azure Stack выполнены успешно. 
1. Откройте текстовый редактор по выбору, а затем скопируйте и вставьте в него предыдущий скрипт.
2. Обновите переменные скрипта в соответствии с параметрами конфигурации. 
3. После обновления необходимых переменных сохраните скрипт и выйдите из редактора. В описанных ниже действиях предполагается, что скрипту присвоено имя my_storage_sample.sh.
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

Обозреватель хранилищ Microsoft Azure — это отдельное приложение от корпорации Майкрософт. Оно позволяет легко работать с данными хранилищ Azure и Azure Stack в Windows, MacOS и Linux. Если требуется простой способ управления данными хранилища Azure Stack, рассмотрите возможность использования обозревателя службы хранилища Microsoft Azure.

Дополнительные сведения о настройке обозревателя службы хранилища Azure для работы с Azure Stack см. в статье [Подключение обозревателя службы хранилища к подписке Azure Stack](azure-stack-storage-connect-se.md).

Дополнительные сведения об обозревателе службы хранилища Microsoft Azure см. в статье [Приступая к работе с обозревателем службы хранилища (предварительная версия)](../../vs-azure-tools-storage-manage-with-storage-explorer.md).

## <a name="next-steps"></a>Дальнейшие действия
* [Подключение обозревателя службы хранилища к подписке Azure Stack](azure-stack-storage-connect-se.md)
* [Приступая к работе с обозревателем службы хранилища (предварительная версия)](../../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [Хранилище Azure Stack. Отличия и рекомендации](azure-stack-acs-differences.md)
* [Введение в службу хранилища Microsoft Azure](../../storage/common/storage-introduction.md)

