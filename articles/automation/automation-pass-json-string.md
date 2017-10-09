---
title: "aaaPass JSON объект runbook службы автоматизации Azure tooan | Документы Microsoft"
description: "Как toopass параметры tooa runbook как объект JSON"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "powershell, runbook, json, служба автоматизации azure"
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 8229a16015d549927ead5496c70e9fb391d35498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="pass-a-json-object-tooan-azure-automation-runbook"></a>Передайте объект JSON tooan модуля runbook службы автоматизации Azure

Это может быть полезным toostore данных, что runbook tooa toopass в файле JSON.
Например, можно создать файл JSON, содержащий все параметры hello требуется toopass tooa runbook.
toodo, имеют tooconvert hello JSON tooa строку и затем преобразовывать hello строка tooa PowerShell перед передачей его содержимое toohello runbook.

В этом примере мы создадим сценария PowerShell, который вызывает [начала AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart runbook PowerShell, передавая hello содержимого hello JSON toohello runbook.
Виртуальной машине Azure, получения параметров hello для hello виртуальной Машины из hello JSON, который был передан в запуске Hello PowerShell runbook.

## <a name="prerequisites"></a>Предварительные требования
toocomplete этого учебника требуется hello следующие:

* Подписка Azure. Если у вас ее нет, [активируйте преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или <a href="/pricing/free-account/" target="_blank">[зарегистрируйте бесплатную учетную запись](https://azure.microsoft.com/free/).
* [Учетная запись службы автоматизации](automation-sec-configure-azure-runas-account.md) toohold hello runbook и проверить подлинность tooAzure ресурсов.  Этой учетной записи необходимо разрешение toostart и остановить виртуальную машину hello.
* Виртуальная машина Azure. Это не должна быть рабочая виртуальная машина, так как в процессе изучения этого руководства ее нужно будет остановить и запустить заново.
* Azure PowerShell, установленный на локальном компьютере. В разделе [Установка и настройка Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) сведения о том, как tooget Azure PowerShell.

## <a name="create-hello-json-file"></a>Создать файл JSON hello

Введите следующее hello тестирования в текстовый файл и сохраните его как `test.json` где-либо на локальном компьютере.

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-hello-runbook"></a>Создание hello runbook

Создайте новый модуль runbook PowerShell с именем Test-Json в службе автоматизации Azure.
toocreate новый модуль runbook PowerShell в статье toolearn [Мой первый runbook PowerShell](automation-first-runbook-textual-powershell.md).

данные JSON tooaccept hello, hello runbook должен получить объект в качестве входного параметра.

Hello runbook можно использовать свойства hello, определенные в hello JSON.

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect tooAzure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object tooactual JSON
$json = $json | ConvertFrom-Json

# Use hello values from hello JSON object as hello parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 Сохраните и опубликуйте этот модуль runbook в учетной записи службы автоматизации.

## <a name="call-hello-runbook-from-powershell"></a>Вызов hello runbook из PowerShell

Теперь можно вызвать hello runbook с локального компьютера с помощью Azure PowerShell.
Выполните следующие команды PowerShell hello.

1. Вход tooAzure:
   ```powershell
   Login-AzureRmAccount
   ```
    Вы являются tooenter запрашиваемые учетные данные Azure.
1. Получение содержимого hello hello JSON-файл и преобразовать его в строку tooa:
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    `JsonPath`— путь hello, где был сохранен файл JSON hello.
1. Преобразовать содержимое строки hello `$json` tooa объект PowerShell:
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. Создать хэш-таблицу для параметров hello `Start-AzureRmAutomstionRunbook`:
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   Обратите внимание, что вы задаете значение hello `Parameters` toohello объект PowerShell, содержащий значения hello из файла JSON hello. 
1. Запустить hello runbook
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

Hello runbook используются значения hello из toostart файла JSON hello виртуальной Машины.

## <a name="next-steps"></a>Дальнейшие действия

* toolearn Дополнительные сведения о редактирования модулей Runbook PowerShell и рабочий процесс PowerShell с помощью текстового редактора в разделе [редактирования текстовое Runbook в автоматизации Azure](automation-edit-textual-runbook.md) 
* в разделе toolearn Дополнительные сведения о создании и импорт модулей Runbook, [Создание или импорт модуля runbook в автоматизации Azure](automation-creating-importing-runbook.md)


