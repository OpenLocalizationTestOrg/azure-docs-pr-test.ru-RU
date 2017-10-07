---
title: "aaaCreating образ виртуальной машины в локальной среде для hello Azure Marketplace | Документы Microsoft"
description: "Понимание и выполните шаги hello toocreate образ виртуальной Машины в локальной и развернуть toohello Azure Marketplace для других toopurchase."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 26dfbd5a-8685-4b19-987e-c20ca60540ec
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c7a265330f1e494db8d0e981a38ee00d85746bb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-hello-azure-marketplace"></a>Разработка образ виртуальной машины в локальной среде для hello Azure Marketplace
Настоятельно рекомендуется разрабатывать непосредственно в облаке hello Azure виртуальные жесткие диски (VHD) с помощью протокола удаленного рабочего стола. Тем не менее если необходимо, она является возможные toodownload виртуального жесткого диска и разработки с помощью локальной инфраструктуры.  

Для разработки приложений в локальной среде, необходимо загрузить hello операционной системы hello создать виртуальный жесткий ДИСК виртуальной Машины. Эти действия входят в шаг 3.3, описанный ранее.  

## <a name="download-a-vhd-image"></a>Загрузка образа VHD
### <a name="locate-a-blob-url"></a>Поиск URL-адреса BLOB-объектов
В порядке toodownload hello виртуальный жесткий ДИСК сначала найдите URL-адрес большого двоичного объекта hello для диска операционной системы hello.

Найдите новый URL-адрес большого двоичного объекта hello из hello [портал Microsoft Azure](https://portal.azure.com):

1. Go слишком**Обзор** > **виртуальные машины**, и затем выберите hello развертывания ВМ.
2. В разделе **Настройка**выберите hello **дисков** плитки, который открывает колонку диски hello.
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. Выберите hello **диска ОС**, который открывается другая панель, отображающий свойства диска, включая расположение виртуального жесткого диска hello.
4. Скопируйте этот URL-адрес большого двоичного объекта.
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. Теперь, удалить hello развертывания ВМ без удаления hello резервного дисков. Также можно остановить hello виртуальной Машины, а не удаляйте его. Не загружать hello операционной системы при запуске hello виртуальной Машины.
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a>Загрузка VHD
После того, как URL-адрес большого двоичного объекта hello, hello виртуального жесткого диска можно загрузить с помощью hello [портал Azure](http://manage.windowsazure.com/) или PowerShell.  

> [!NOTE]
> Во время создания в этом руководстве hello toodownload функции hello виртуального жесткого диска еще не присутствуют в hello новый портал Microsoft Azure.  
> 
> 

**Загрузка операционной системы hello виртуальный жесткий ДИСК через hello текущей [портал Azure](http://manage.windowsazure.com/)**

1. Войдите в портал Azure toohello, если вы еще не сделано.
2. Нажмите кнопку hello **хранения** вкладки.
3. Выберите учетную запись хранения hello, в течение которого hello хранится виртуальный жесткий ДИСК.
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. Откроются свойства учетной записи хранения. Выберите hello **контейнеры** вкладки.
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. Выберите контейнер hello, в которой hello хранится виртуальный жесткий ДИСК. По умолчанию при создании из портала hello hello виртуального жесткого диска хранится в контейнере VHD-файлов.
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. Выберите подходящую операционную систему hello виртуального жесткого диска путем сравнения toohello hello URL-адрес, который был сохранен.
7. Щелкните элемент **Загрузить**.
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a>Загрузка VHD с помощью PowerShell
В дополнение к этому toousing hello портал Azure, вы можете использовать hello [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) командлет toodownload hello операционной системы.

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
Например: Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String>

> [!NOTE]
> **Save-AzureVhd** также имеет **NumberOfThreads** , возможность использовать tooincrease toomake параллелизма hello эффективно использовать доступную пропускную способность для скачивания hello.
> 
> 

## <a name="upload-vhds-tooan-azure-storage-account"></a>Отправить учетную запись хранилища Azure tooan виртуальных жестких дисков
Если подготовки виртуальных жестких дисков в локальной необходимо tooupload их в хранилища учетной записи в Azure. Это действие выполняется после локального создания VHD, но до сертификации образа виртуальной машины.

### <a name="create-a-storage-account-and-container"></a>Создание учетной записи хранения и контейнера
Мы рекомендуем, что виртуальные жесткие диски будет передан в учетной записи хранения в регионе США hello. Все VHD для одного и того же SKU необходимо поместить в один и тот же контейнер в одной и той же учетной записи хранения.

toocreate учетной записи хранилища можно использовать hello [портал Microsoft Azure](https://portal.azure.com/), PowerShell или средство командной строки hello Linux.  

**Создать учетную запись хранилища с портала Microsoft Azure hello**

1. Нажмите кнопку **Создать**.
2. Выберите **Хранилище**.
3. Введите имя учетной записи хранения hello и выберите местоположение.
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. Щелкните **Создать**.
5. Hello колонке hello, учетная запись хранения создана должен быть открыт. Если это не произошло, последовательно выберите **Обзор** > **Учетные записи хранения**. Hello хранения промежуточных колонки, выберите создать учетную запись хранения hello.
6. Выберите **Контейнеры**.
   
   ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. В колонке контейнеры hello, выберите **добавить**, а затем введите имя и hello контейнера разрешениями для контейнера. Для разрешений контейнера выберите вариант **Частный** .

> [!TIP]
> Рекомендуется создать один контейнер на планировании toopublish SKU.
> 
> 

  ![рисунок](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a>Создание учетной записи хранения с помощью PowerShell
С помощью PowerShell, создать учетную запись хранилища с помощью hello [New AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) командлета.

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

Затем вы можете создать контейнер в этой учетной записи хранения с помощью hello [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) командлета.

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> Эти команды предполагают, что этот контекст учетной записи хранилища текущего hello уже задано в PowerShell.   См. слишком[Настройка Azure PowerShell](marketplace-publishing-powershell-setup.md) Дополнительные сведения об установке PowerShell.  
> 
> ### <a name="create-a-storage-account-by-using-hello-command-line-tool-for-mac-and-linux"></a>Создать учетную запись хранилища с помощью средства командной строки hello для Mac и Linux
> В [программе командной строки Linux](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)создайте учетную запись хранения следующим образом.
> 
> 

        azure storage account create mystorageaccount --location "West US"

Создайте контейнер следующим образом.

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a>Отправка VHD
После создания учетной записи хранилища hello и контейнер можно передать подготовленные виртуальные жесткие диски. Можно использовать PowerShell, средства командной строки hello Linux или других средств управления в хранилище Azure.

### <a name="upload-a-vhd-via-powershell"></a>Отправка VHD с помощью PowerShell
Используйте hello [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) командлета.

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-hello-command-line-tool-for-mac-and-linux"></a>Отправить VHD с помощью средства командной строки hello для Mac и Linux
С hello [средство командной строки Linux](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), используйте ниже hello: Создание образа виртуальной машины azure <image name> --расположение <Location of hello data center> --ОС Linux<LocationOfLocalVHD>

## <a name="see-also"></a>См. также
* [Создание образа виртуальной машины для hello Marketplace](marketplace-publishing-vm-image-creation.md)
* [Настройка Azure PowerShell](marketplace-publishing-powershell-setup.md)

