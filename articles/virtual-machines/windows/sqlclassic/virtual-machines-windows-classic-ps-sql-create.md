---
title: "aaaCreate виртуальной машины SQL Server PowerShell Azure (классические) | Документы Microsoft"
description: "Содержит описание действий и сценарии PowerShell для создания виртуальной машины Azure на основе образа из коллекции образов виртуальных машин SQL Server. В этом разделе используется режим классическое развертывание hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: b73be387-9323-4e08-be53-6e5928e3786e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: b14d5d9bc192fa0a21126395ee20ffd06b3bf47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a>Подготовка виртуальной машины SQL Server к работе с помощью Azure PowerShell (классическая модель)

В этой статье шаги как toocreate виртуальной машины SQL Server в Azure с помощью hello командлеты PowerShell.

> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.

Hello диспетчера ресурсов версию этого раздела в разделе [подготовки виртуальной машины SQL Server с помощью диспетчера ресурсов Azure PowerShell](../sql/virtual-machines-windows-ps-sql-create.md).

### <a name="install-and-configure-powershell"></a>Установка и настройка PowerShell
1. Если у вас нет учетной записи Azure, используйте [бесплатную пробную версию Azure](https://azure.microsoft.com/pricing/free-trial/).
2. [Загрузите и установите последнюю команд Azure PowerShell hello](/powershell/azure/overview).
3. Запустите Windows PowerShell и подключите его tooyour подписки Azure с hello **Add-AzureAccount** команды.

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a>Определение целевого региона Azure

Ваша виртуальная машина SQL Server будет размещаться в облачной службе, которая находится в определенном регионе Azure. Hello следующих шагов помочь toodetermine вы свой регион, учетной записи хранилища и облачную службу, которая будет использоваться для hello конца учебника hello.

1. Определите hello центра обработки данных требуется toouse toohost ВМ SQL Server. Hello следующую команду PowerShell отображает список доступных регионов.

   ```powershell
   (Get-AzureLocation).Name
   ```

2. После определения вашей предпочтительного источника задайте переменную с именем **$dcLocation** toothat области. Здравствуйте, например, следующая команда задает hello области слишком «Восток США»:

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a>Указание подписки и учетной записи хранения

1. Определите hello подписки Azure, которая будет использоваться для новой виртуальной машины hello.

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. Назначить подписки Azure к целевой toohello **$subscr** переменной. Затем установите ее как текущую подписку Azure.

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. После этого проверьте наличие существующих учетных записей хранения. Hello следующий сценарий отображает все учетные записи хранения, которые существуют в вашем регионе выбранной:

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > Если требуется учетной записи хранения, следует сначала создайте имя учетной записи хранения все строчные с помощью команды New-AzureStorageAccount hello как следующий пример hello:`New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`

4. Назначить hello целевого хранилища учетной записи имя toohello **$staccount**. Затем с помощью **Set-AzureSubscription** tooset hello подписки и текущей учетной записи хранилища.

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a>Выбор образа виртуальной машины SQL Server

1. Определить список доступных образов виртуальных машин SQL Server из коллекции hello hello. Свойство **ImageFamily** для этих образов начинается с «SQL». Hello следующий запрос отображает hello образ семейства доступных tooyou, имеют предварительно установить SQL Server.

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. Найдя семейства образ виртуальной машины hello, может иметься несколько образов, опубликованных в этом семействе. Используйте hello следующий скрипт имя образа toofind hello последней опубликованной виртуальной машины для вашей семьи выбранное изображение (например, **SQL Server 2016 RTM Enterprise на Windows Server 2012 R2**):

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-hello-virtual-machine"></a>Создание виртуальной машины hello

Наконец Создание hello виртуальной машины с помощью PowerShell.

1. Создание облака service toohost hello новой виртуальной Машины. Обратите внимание, что также возможно toouse существующую облачную службу вместо него. Создать новую переменную **$svcname** с hello короткое имя hello облачной службы.

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. Укажите имя виртуальной машины hello и размер. Дополнительные сведения о размерах виртуальных машин см. в разделе [Размеры виртуальных машин в Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see hello link toohello other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. Укажите учетную запись локального администратора hello и пароль.

   ```powershell
   $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. Выполнения hello следующий скрипт toocreate hello виртуальной машины.

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> Дополнительные пояснения и параметры конфигурации см. в разделе hello **создайте свой набор команд** статьи [toocreate использование Azure PowerShell и предварительной настройки виртуальных машин на основе Windows](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="example-powershell-script"></a>Пример сценария PowerShell

Hello следующий сценарий является примером полный скрипт, который создает **SQL Server 2016 RTM Enterprise на Windows Server 2012 R2** виртуальной машины. Если вы используете этот сценарий, необходимо настроить hello начальной переменных, основанных на предыдущих шагах hello в этом разделе.

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set hello current subscription and storage account
# Comment out hello New-AzureStorageAccount line if hello account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select hello most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create hello new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create hello VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create hello SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a>Подключение к удаленному рабочему столу

1. Создание файлов RDP hello в toolaunch папке текущего пользователя hello документа установки toocomplete эти виртуальные машины:

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. В каталоге "документы" hello запустите hello RDP-файл. Связь с hello имя пользователя администратора и пароль, предоставленные ранее (например, если имя пользователя было VMAdmin, укажите «\VMAdmin» в качестве пользователя hello и предоставить пароль hello).

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-hello-configuration-of-hello-sql-server-machine-for-remote-access"></a>Настройка завершения hello hello машины SQL Server для удаленного доступа

После входа в систему компьютера toohello с удаленным рабочим столом, настройте SQL Server в соответствии с инструкциями hello в [действия для настройки подключения к SQL Server на виртуальной Машине Azure](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).

## <a name="next-steps"></a>Дальнейшие действия

Имеются дополнительные инструкции для подготовки виртуальных машин с помощью PowerShell в hello [документация по виртуальным машинам](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Во многих случаях hello следующим шагом является toomigrate toothis вашей базы данных новую виртуальную Машину SQL Server. Руководство по миграции базы данных см. в разделе [миграция tooSQL базы данных сервера на Виртуальной машине Azure](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).

Если вы хотите использовать hello Azure портала toocreate виртуальных машин SQL, см. раздел [подготовки виртуальной машины SQL Server в Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md). Обратите внимание, что учебника hello hello, проходит через портал hello создает виртуальных машин с помощью модели рекомендуется диспетчера ресурсов, а не hello классической модели, используемые в данном разделе PowerShell.

Кроме toothese ресурсов, рекомендуется изучить [другие разделы, посвященные toorunning SQL Server в виртуальных машинах Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).
