---
title: "aaaDesired конфигурации состояния Обзор Azure | Документы Microsoft"
description: "Обзор использования hello обработчик расширений Microsoft Azure для настройки требуемого состояния PowerShell. В ней описаны обязательные требования, архитектура, командлеты и многое другое."
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: bbacbc93-1e7b-4611-a3ec-e3320641f9ba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 01/09/2017
ms.author: zachal
ms.openlocfilehash: b0337a2f1124f35e5e40c1478bd7530427e59d44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-desired-state-configuration-extension-handler"></a>Обработчик расширений Azure настройки требуемого состояния toohello введение
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Hello агент ВМ и связанные с ним расширения являются частью hello службах инфраструктуры Microsoft Azure. Расширения ВМ — программные компоненты, расширяющие функциональные возможности виртуальной Машины hello и упрощения различные операции управления виртуальной Машины. Например, hello расширения VMAccess можно использовать tooreset пароль администратора или hello пользовательский сценарий используется tooexecute сценария на hello виртуальная машина может иметь расширение.

В этой статье описаны hello расширения конфигурации требуемого состояния PowerShell (DSC) для виртуальных машин Azure в рамках hello Azure PowerShell SDK. Можно использовать новые командлеты tooupload и применение конфигурации PowerShell DSC на виртуальной Машине Azure включено с hello расширение PowerShell DSC. вызовы расширение PowerShell DSC Hello в PowerShell DSC tooenact hello полученную конфигурацию DSC на hello виртуальной Машины. Эта функция также доступна через портал Azure hello.

## <a name="prerequisites"></a>Предварительные требования
**Локальный компьютер** toointeract с Здравствуйте расширения виртуальной Машины Windows Azure, необходимо либо hello портал Azure toouse или hello Azure PowerShell SDK. 

**Гостевой агент** hello виртуальной Машине Azure, настроенный в конфигурации hello DSC должен toobe ОС, которая поддерживает либо Windows Management Framework (WMF) 4.0 и 5.0. Hello полный список поддерживаемых версий операционной системы можно найти в hello [журнал версий расширения DSC](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).

## <a name="terms-and-concepts"></a>Термины и основные понятия
Это руководство предполагает знание hello следующие понятия:

Конфигурация — документ конфигурации DSC. 

Узел — целевой объект для конфигурации DSC. В этом документе «узел» всегда ссылается tooan виртуальной Машине Azure.

Данные конфигурации — PSD1-файл, содержащий данные среды для конфигурации.

## <a name="architectural-overview"></a>Основные сведения об архитектуре
Hello расширение Azure DSC использует toodeliver framework hello агента ВМ Azure, применения и отчет о конфигурации DSC, работающих на виртуальных машинах Azure. Hello расширение DSC ожидает ZIP-файл, содержащий по крайней мере в документе конфигурации и набор параметров предоставляется посредством hello Azure PowerShell SDK или hello портал Azure.

Расширение hello вызывается для hello первый раз, запускается процесс установки. Этот процесс устанавливает версию hello Windows Management Framework (WMF) с помощью hello следующая логика:

1. Если hello Azure ОС виртуальной Машины Windows Server 2016, никакие действия не выполняются. Windows Server 2016 уже hello последняя установленная версия PowerShell.
2. Если hello `wmfVersion` свойство указано, что hello WMF версии, если только он не совместим с ОС виртуальной Машины hello.
3. Если не `wmfVersion` свойство указано, hello последние применимые hello WMF версии.

Установка hello WMF требуется перезагрузка. После перезагрузки, расширение hello загружает hello ZIP-файл, указанный в hello `modulesUrl` свойство. Если это расположение находится в хранилище больших двоичных объектов, маркер SAS может быть указан в hello `sasToken` tooaccess свойство hello файла. После загрузки и распаковать hello .zip, hello функцию конфигурации, определенные в `configurationFunction` выполняется toogenerate hello MOF-файл. расширение Hello запускает `Start-DscConfiguration -Force` on hello созданный MOF-файл. расширение Hello записывает выходные данные и записывает ее обратно toohello Azure состояние канала. С этого момента, hello DSC LCM обрабатывает мониторинг и исправление обычным образом. 

## <a name="powershell-cmdlets"></a>Командлеты PowerShell
Командлеты PowerShell можно использовать с помощью диспетчера ресурсов Azure или hello toopackage модели классическое развертывание, публикация и отслеживать развертывание расширения DSC. Hello перечисленные ниже командлеты представляют Привет классическое развертывание модули, но «Azure» можно заменить «AzureRm» toouse hello Azure Resource Manager модели. Например `Publish-AzureVMDscConfiguration` использует hello классической модели развертывания, где `Publish-AzureRmVMDscConfiguration` использует диспетчера ресурсов Azure. 

`Publish-AzureVMDscConfiguration`Вставляет в файл конфигурации, ищет зависимые ресурсы DSC и создает ZIP-файл, содержащий конфигурации hello и конфигурации hello tooenact необходимые ресурсы DSC. Его можно также создать hello локально с помощью hello `-ConfigurationArchivePath` параметра. В противном случае публикует хранилища больших двоичных объектов tooAzure файла .zip hello и защищает его с помощью токена SAS.

Hello ZIP-файл, созданных этим командлетом имеет hello ps1-скрипт конфигурации на корень hello hello архивной папки. Ресурсы имеют папке модуля hello помещены в архив hello. 

`Set-AzureVMDscExtension`внедряет hello параметры, необходимые hello расширение PowerShell DSC в объект конфигурации виртуальной Машины. В hello классической модели развертывания, изменения hello ВМ должен быть применен tooan ВМ Azure с `Update-AzureVM`. 

`Get-AzureVMDscExtension`Извлекает состояние расширения DSC hello конкретной виртуальной Машины. 

`Get-AzureVMDscExtensionStatus`Извлекает состояние hello hello конфигурации DSC, активированная обработчиком расширения DSC hello. Это действие может выполняться с одной виртуальной машиной или с группой виртуальных машин.

`Remove-AzureVMDscExtension`Удаляет обработчик расширения hello данной виртуальной машине. Этот командлет не **не** удалить конфигурацию hello, удалите hello WMF или изменить параметры hello применения на виртуальной машине hello. Удаляет только обработчик расширений hello. 

**Основные отличия между командлетами для ASM и Azure Resource Manager**

* Командлеты Azure Resource Manager выполняются синхронно. а командлеты ASM — асинхронными.
* ResourceGroupName, VMName, ArchiveStorageAccountName, Version, Location — это обязательные параметры в Azure Resource Manager.
* ArchiveResourceGroupName — новый необязательный параметр для Azure Resource Manager. Этот параметр можно указать, когда учетной записи хранилища относится tooa группы ресурсов, отличной от hello один, где создается виртуальная машина hello.
* ConfigurationArchive — это ArchiveBlobName в Azure Resource Manager.
* ContainerName — это ArchiveContainerName в Azure Resource Manager.
* StorageEndpointSuffix — это ArchiveStorageEndpointSuffix в Azure Resource Manager.
* Hello AutoUpdate добавлен параметр tooAzure tooenable диспетчера ресурсов, автоматическое обновление hello расширение обработчика toohello последнюю версию, что и если оно доступно. Обратите внимание, что этот параметр имеет hello возможны перезагрузки toocause hello виртуальной Машины, когда новая версия выпуска WMF hello. 

## <a name="azure-portal-functionality"></a>Использование портала Azure
Обзор tooa виртуальной Машины. В разделе "Параметры" > "Общие" щелкните "Расширения". Будет создана новая панель. Щелкните "Добавить" и выберите DSC PowerShell.

портал Hello должен входных данных.
**Configuration Modules or Script**(Модули или сценарий конфигурации) — обязательное поле. Требуется ps1-файл, содержащий сценарий конфигурации или ZIP-файл с помощью сценария конфигурации .ps1 корне hello и все зависимые ресурсы в папках модуля в пределах hello .zip. Он может быть создан с hello `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` командлетов, включенных в пакет SDK для Azure PowerShell hello. ZIP-файл Hello передаются в хранилище BLOB-объектов пользователя, защищенным с помощью маркера SAS. 

**Configuration Data PSD1 File**(PSD1-файл данных конфигурации) — необязательное поле. Если конфигурации требуется файл данных конфигурации в .psd1, используйте это поле tooselect его и отправьте его в хранилище больших двоичных объектов tooyour пользователя, где он защищен с помощью маркера SAS. 

**Module-Qualified Name of Configuration**(Полное имя модуля конфигурации) — PS1-файлы могут включать в себя несколько функций конфигурации. Введите имя hello скрипт .ps1 конфигурации hello, за которым следует "\' и hello имя функции hello конфигурации. Например если ps1-скрипт имеет hello имя «configuration.ps1», а конфигурация hello — «IisInstall», введите:`configuration.ps1\IisInstall`

**Аргументы конфигурации**: Если функция конфигурации hello принимает аргументы, укажите их здесь в формате hello `argumentName1=value1,argumentName2=value2`. Обратите внимание, что этот формат отличается от того, в котором аргументы конфигурации принимаются через командлеты PowerShell или шаблоны Resource Manager. 

## <a name="getting-started"></a>Приступая к работе
расширение Azure DSC Hello принимает документы конфигурации DSC и их применения на виртуальных машинах Azure. Ниже приведен простой пример конфигурации. Сохраните его локально как файл IisInstall.ps1.

```powershell
configuration IISInstall 
{ 
    node "localhost"
    { 
        WindowsFeature IIS 
        { 
            Ensure = "Present" 
            Name = "Web-Server"                       
        } 
    } 
}
```

следующие шаги месте hello IisInstall.ps1 скрипт на hello Hello указан виртуальной Машины, выполнить конфигурацию hello и выдавать отчеты о состоянии.
###<a name="classic-model"></a>Классическая модель
```powershell
#Azure PowerShell cmdlets are required
Import-Module Azure

#Use an existing Azure Virtual Machine, 'DscDemo1'
$demoVM = Get-AzureVM DscDemo1

#Publish hello configuration script into user storage.
Publish-AzureVMDscConfiguration -ConfigurationPath ".\IisInstall.ps1" -StorageContext $storageContext -Verbose -Force

#Set hello VM toorun hello DSC configuration
Set-AzureVMDscExtension -VM $demoVM -ConfigurationArchive "IisInstall.ps1.zip" -StorageContext $storageContext -ConfigurationName "IisInstall" -Verbose

#Update hello configuration of an Azure Virtual Machine
$demoVM | Update-AzureVM -Verbose

#check on status
Get-AzureVMDscExtensionStatus -VM $demovm -Verbose
```
###<a name="azure-resource-manager-model"></a>Модель Azure Resource Manager

```powershell
$resourceGroup = "dscVmDemo"
$location = "westus"
$vmName = "myVM"
$storageName = "demostorage"
#Publish hello configuration script into user storage
Publish-AzureRmVMDscConfiguration -ConfigurationPath .\iisInstall.ps1 -ResourceGroupName $resourceGroup -StorageAccountName $storageName -force
#Set hello VM toorun hello DSC configuration
Set-AzureRmVmDscExtension -Version 2.21 -ResourceGroupName $resourceGroup -VMName $vmName -ArchiveStorageAccountName $storageName -ArchiveBlobName iisInstall.ps1.zip -AutoUpdate:$true -ConfigurationName "IISInstall"

```

## <a name="logging"></a>Ведение журналов
Журналы размещаются в следующем каталоге:

C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[номер версии]

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о PowerShell DSC [посетите центр документации PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview). 

Изучите hello [шаблона Azure Resource Manager для расширения hello DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Дополнительные функциональные возможности toofind можно управлять с помощью PowerShell DSC [Обзор коллекции PowerShell hello](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) дополнительные ресурсы DSC.

Дополнительные сведения о передаче конфиденциальные параметры в конфигурации в разделе [управление учетными данными безопасно с обработчиком расширения hello DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

