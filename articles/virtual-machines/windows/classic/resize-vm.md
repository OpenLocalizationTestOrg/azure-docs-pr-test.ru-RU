---
title: "aaaResize виртуальной Машины Windows в hello классической модели развертывания - Azure | Документы Microsoft"
description: "Измените размер виртуальной машины Windows, созданных в hello классической модели развертывания, с помощью Azure Powershell."
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e3038215-001c-406e-904d-e0f4e326a4c7
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 39fab14431e2351c9515b0611e850eccfec7a798
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm-created-in-hello-classic-deployment-model"></a>Изменение размера виртуальной Машины Windows, созданных в hello классической модели развертывания
В этой статье показано, как tooresize ВМ Windows, созданные в hello классической модели развертывания с помощью Azure Powershell.

При рассмотрении возможности tooresize hello виртуальной Машины, существует два понятия, которые управляют hello диапазон размеров доступных tooresize hello виртуальной машины. Первое базовое понятие Hello — hello регион, в котором развернута ВМ. Список доступных размеров виртуальных Машин в регионе Hello находится под hello вкладку "службы" Привет регионы Azure веб-страницы. Концепция второй Hello является hello физического оборудования, в настоящее время размещения виртуальной Машины. физические серверы Hello размещение виртуальных машин группируются в кластеры общих физического оборудования. метод Hello изменение размера виртуальной Машины отличается в зависимости от того, если hello желательный размер новой виртуальной Машины поддерживается hello оборудования кластера в настоящее время размещается hello виртуальной Машины.

> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Вы также можете [изменения размера виртуальных Машин, созданных в модели развертывания диспетчера ресурсов hello](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="add-your-account"></a>Добавление учетной записи
Необходимо настроить Azure PowerShell toowork классические ресурсы Azure. Выполните действия hello ниже tooconfigure Azure PowerShell toomanage классические ресурсы.

1. Введите в командной строке PowerShell hello `Add-AzureAccount` и нажмите кнопку **ввод**. 
2. Введите адрес электронной почты hello, связанных с подпиской Azure и нажмите кнопку **Продолжить**. 
3. Введите в hello пароль своей учетной записи. 
4. Щелкните **Войти**. 

## <a name="resize-in-hello-same-hardware-cluster"></a>Изменение размеров в hello же оборудования кластера
tooresize tooa размер виртуальной Машины, доступных в кластере оборудования hello размещение hello виртуальной Машины, выполните следующие шаги hello.

1. Выполните следующую команду PowerShell, что в кластере оборудования hello размещение hello облачную службу, которая содержит размеры виртуальных Машин hello toolist hello виртуальной Машины hello.
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. Выполните следующие команды tooresize hello ВМ hello.
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a>Изменение размера в новом кластере оборудования
tooresize tooa размер виртуальной Машины, недоступен в hello оборудования кластера размещения Здравствуйте виртуальной Машины, hello облачную службу и все виртуальные машины в облачной службе hello должны быть созданы заново. Каждая облачная служба размещается в кластере один аппаратный поэтому все виртуальные машины в облачной службе hello должно иметь размер, который поддерживается в кластере оборудования. Hello Далее будет описывается, как tooresize к виртуальной Машине по удалению и повторному созданию затем hello облачной службы.

1. Запустите следующие PowerShell команды toolist hello ВМ размеры, доступные в области hello hello. 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. Запишите все параметры конфигурации для каждой виртуальной Машины в hello облачную службу, которая содержит toobe ВМ hello изменения размеров. 
3. Удалите все виртуальные машины в облачной службе hello, выбрав hello параметр tooretain hello дисков для каждой виртуальной Машины.
4. Повторно создайте hello ВМ toobe изменяется с помощью hello желаемый размер виртуальной Машины.
5. Повторное создание других виртуальных машин, которые были в облачной службе hello размер виртуальной Машины, доступных в кластере оборудования hello, теперь размещение hello облачной службы с помощью.

Пример сценария для удаления и повторного создания облачной службы с использованием нового размера виртуальной машины можно найти [здесь](https://github.com/Azure/azure-vm-scripts). 

## <a name="next-steps"></a>Дальнейшие действия
* [Изменить размер виртуальных Машин, созданных в модели развертывания диспетчера ресурсов hello](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

