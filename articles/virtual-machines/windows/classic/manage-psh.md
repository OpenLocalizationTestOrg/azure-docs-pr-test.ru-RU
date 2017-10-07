---
title: "aaaManage виртуальные машины с помощью Azure PowerShell | Документы Microsoft"
description: "Дополнительные команды, которые можно использовать задачи tooautomate в управлении виртуальными машинами."
services: virtual-machines-windows
documentationcenter: windows
author: singhkays
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 7cdf9bd3-6578-4069-8a95-e8585f04a394
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 10/12/2016
ms.author: kasing
ms.openlocfilehash: e4ca6f098519243a321eac98b6692790fe18c22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a>Управление виртуальными машинами с помощью Azure PowerShell
> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Стандартные команды PowerShell с помощью модели hello диспетчера ресурсов, в разделе [здесь](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

С помощью командлетов Azure PowerShell можно автоматизировать многие задачи, выполните каждый день toomanage виртуальных машин. В этой статье приводятся примеры команд для более простые задачи и tooarticles ссылок, отображение hello команд для более сложных задач.

> [!NOTE]
> Если вы еще не установлен и настроен Azure PowerShell, но инструкции можно получить в статье hello [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).
> 
> 

## <a name="how-toouse-hello-example-commands"></a>Как toouse hello примеры команд
Вам потребуется tooreplace некоторые из текста hello в hello команды с текстом, который подходит для вашей среды. Hello < и > символы указывают текст, необходимо tooreplace. При замене текста hello, удалите символы hello, но hello кавычки следует оставить на месте.

## <a name="get-a-vm"></a>Получение виртуальной машины
Вы будете выполнять эту основную задачу очень часто. Использовать tooget сведения о виртуальной Машине, выполнять задачи на виртуальной Машине или получить toostore выходные данные в переменной.

tooget сведения о hello виртуальной Машины, выполните следующую команду, заменив все, что заключено в кавычки hello, включая hello < и > символов:

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

выходные данные в переменной $vm hello toostore выполните:

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-tooa-windows-based-vm"></a>Войдите на tooa виртуальной Машины на основе Windows
Выполните следующие команды:

> [!NOTE]
> Hello виртуальной машины и имя облачной службы можно получить из отображения hello hello **Get-AzureVM** команды.
> 
> $svcName = "<cloud service name>» $vmName ="<virtual machine name>» $localPath = «< диск и папку расположения toostore hello загрузить RDP-файл, пример: c:\temp >» $localFile = $localPath + "\" + $vmname + «.rdp» Get-AzureRemoteDesktopFile - ServiceName $svcName-имя $vmName - LocalPath $localFile-запуск
> 
> 

## <a name="stop-a-vm"></a>Остановка виртуальной машины
Выполните следующую команду:

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> Использовать этот параметр tookeep hello, виртуальный IP-адрес (VIP) hello облачных служб в случае hello последняя виртуальная машина в указанной облачной службе. <br><br> При использовании параметра StayProvisioned hello, вам будет выставляться за hello виртуальной Машины.
> 
> 

## <a name="start-a-vm"></a>Запуск виртуальной машины
Выполните следующую команду:

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a>Присоединение диска данных
Для этой задачи требуется несколько шагов. Во-первых, используйте hello *** Add-AzureDataDisk *** командлет tooadd hello toohello $vm объект диска. Затем можно с помощью **Update-AzureVM** командлет tooupdate hello конфигурацию hello виртуальной Машины.

Кроме того, потребуется toodecide tooattach новый диск или один, содержит ли данные. Для нового диска hello команда создает hello VHD-файл и присоединяет его.

tooattach новый диск, выполните следующую команду:

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

tooattach существующий диск данных, выполните следующую команду:

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

tooattach диски с данными из существующего файла VHD в хранилище больших двоичных объектов, выполните следующую команду:

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a>Создание виртуальной машины под управлением Windows
новый на основе Windows виртуальной машины в Azure, используйте инструкции hello в toocreate [toocreate использовать Azure PowerShell и предварительной настройки виртуальных машин на основе Windows](create-powershell.md). Этот раздел действия можно выполнить с помощью Azure PowerShell, набор команд, создание hello создает к виртуальной Машине под управлением Windows, могут быть предварительно настроены:

* членство в домене Active Directory;
* дополнительные диски;
* членство в существующем наборе балансировки нагрузки;
* статический IP-адрес.

