---
title: "aaaVariable средств автоматизации Azure | Документы Microsoft"
description: "Ресурсы переменных представлены значения, доступные tooall Runbook и конфигураций DSC в службе автоматизации Azure.  В этой статье подробно описывается hello переменных и как toowork с ними в текстовых и графических разработки."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: b880c15f-46f5-4881-8e98-e034cc5a66ec
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/09/2017
ms.author: magoedte;bwren
ms.openlocfilehash: f9daa49fc1dc883ffb218a9adf26e36df1d6bb27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="variable-assets-in-azure-automation"></a>Средства переменных в службе автоматизации Azure

Ресурсы переменных представлены значения, доступные tooall Runbook и конфигураций DSC в вашей учетной записи автоматизации. Их можно создать, изменить и извлечь из hello портал Azure, Windows PowerShell, а также из runbook или конфигурации DSC. Переменные автоматизации используются для hello следующие сценарии:

- совместное использование значения несколькими модулями Runbook или конфигурациями DSC;

- Совместное использование значения несколькими заданиями из hello одного модуля runbook или конфигурации DSC.

- Управление значением из портала hello или из командной строки Windows PowerShell hello, используемой модулей Runbook или конфигураций DSC, такие как набор общих элементов конфигурации как определенный список имен виртуальных Машин, определенной группы ресурсов, имя домена AD, и т. д.  

Переменные автоматизации сохраняются так, что они остаются toobe доступен даже при сбое hello runbook или конфигурации DSC.  Это также позволяет toobe значение, задайте в одном модуле runbook, который затем используется другим или используется hello одного модуля runbook или hello конфигурации DSC очередном запуске.

При создании переменной можно указать, что она должна храниться в зашифрованном виде.  Если переменная шифруется, она безопасно хранится в службе автоматизации Azure и его значение не удается получить из hello [Get AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) командлет, который поставляется в составе модуля Azure PowerShell hello.  Hello единственный способ извлечения зашифрованного значения — от hello **Get-AutomationVariable** действие в runbook или конфигурации DSC.

> [!NOTE]
> Безопасные средства в службе автоматизации Azure включают учетные данные, сертификаты, подключения и зашифрованные переменные. Эти ресурсы шифруются и хранятся в hello автоматизации Azure, используя уникальный ключ, который создается для каждой учетной записи автоматизации. Ключ шифруется главным сертификатом и хранится в службе автоматизации Azure. Перед сохранением безопасного ресурса, hello ключ для учетной записи автоматизации hello расшифровывается с помощью шаблона сертификата hello и затем использовать tooencrypt hello активов.

## <a name="variable-types"></a>Типы переменных

При создании переменной с hello портал Azure, необходимо указать тип данных из раскрывающегося списка hello, hello портале можно было отобразить соответствующий элемент управления для ввода значения переменной hello hello. переменная Hello не ограниченных toothis данных типа, но необходимо задать переменную hello, с помощью Windows PowerShell, если требуется, чтобы toospecify значение другого типа. При указании **не определен**, а затем hello hello переменной будет иметь значение слишком**$null**, и необходимо задать значение hello с hello [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) командлета или **Set-AutomationVariable** действия.  Невозможно создать или изменить hello значение для переменной сложного типа hello портала, но можно указать значение любого типа, с помощью Windows PowerShell. Сложные типы возвращаются в виде [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).

Можно сохранить несколько значений tooa отдельную переменную, создав массив или хэш-таблицы и сохранить его в переменной toohello.

Здесь представлены Hello список типов переменных автоматизации:

* Строка
* Целое число 
* DateTime
* Логический
* Null

## <a name="cmdlets-and-workflow-activities"></a>Командлеты и рабочие процессы

командлеты Hello в следующей таблице hello, используемые toocreate и управления переменными службы автоматизации с помощью Windows PowerShell. Они поставляются как часть hello [модуля Azure PowerShell](../powershell-install-configure.md) доступный для использования в Runbook автоматизации и конфигурации DSC.

|Командлеты|Описание|
|:---|:---|
|[Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx)|Извлекает значение hello существующей переменной.|
|[New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx)|Создает новую переменную и устанавливает ее значение.|
|[Remove-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt619354.aspx)|Удаляет существующую переменную.|
|[Set-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603601.aspx)|Задает значение hello для существующей переменной.|

действия рабочего процесса Hello в следующей таблице hello, используемые tooaccess переменные автоматизации в модуле runbook. Они доступны только для использования в конфигурации DSC или runbook и поставляются в составе модуля Azure PowerShell hello.

|Действия рабочего процесса|Описание|
|:---|:---|
|Get-AutomationVariable|Извлекает значение hello существующей переменной.|
|Set-AutomationVariable|Задает значение hello для существующей переменной.|

> [!NOTE] 
> Следует избегать использования переменных в hello – имя параметра **Get-AutomationVariable** в runbook или конфигурации DSC, поскольку это может усложнить обнаружение зависимостей между модулями Runbook или конфигурации DSC и автоматизации переменные во время разработки.

## <a name="creating-a-new-automation-variable"></a>Создание новой переменной автоматизации

### <a name="toocreate-a-new-variable-with-hello-azure-portal"></a>toocreate новую переменную с hello портал Azure

1. Из учетной записи автоматизации, нажмите кнопку hello **активы** плитку и затем на hello **активы** колонке выберите **переменных**.
2. На hello **переменных** плитки, выберите **добавить переменную**.
3. Настройте параметры hello на hello **новой переменной** колонку и нажмите кнопку **создать** сохранить новую переменную hello.

### <a name="toocreate-a-new-variable-with-windows-powershell"></a>toocreate новую переменную с помощью Windows PowerShell

Hello [New AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) создает новую переменную и задает ее начальное значение. Можно извлечь при помощи значение hello [Get AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx). Если hello значение простого типа, то возвращается того же типа. Если это сложный тип, возвращается **PSCustomObject** .

Hello следующем образце команд Показать как toocreate переменную типа string и возвращать его значение.

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

Hello следующем образце команд Показать как toocreate переменной с помощью сложного типа, а затем возвращают ее свойства. В данном случае используется объект виртуальной машины из **Get-AzureRmVm**.

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a>Использование переменной в модуле Runbook или конфигурации DSC

Используйте hello **Set-AutomationVariable** действия tooset hello значение переменной службы автоматизации в runbook или конфигурации DSC и hello **Get-AutomationVariable** tooretrieve его.  Не следует использовать hello **Set-AzureAutomationVariable** или **Get-AzureAutomationVariable** командлетов в runbook или конфигурации DSC, так как они менее эффективным, чем hello действий рабочего процесса.  Также не удается получить значение hello безопасного переменных с **Get-AzureAutomationVariable**.  Здравствуйте только способом toocreate новой переменной из модуля runbook или конфигурации DSC — toouse hello [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx) командлета.


### <a name="textual-runbook-samples"></a>Текстовые примеры модуля Runbook

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a>Установка и получение простого значения из переменной

Hello следующем образце команд Показать как tooset и вернуть переменную в текстовой runbook. В примере предполагается, что целочисленные переменные *NumberOfIterations* и *NumberOfRunnings* и строковая переменная *SampleMessage* уже созданы.

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a>Задание и получение сложного объекта в переменной

Hello следующем образце кода показано, как tooupdate переменной с помощью сложного значения в текстовое runbook. В этом примере извлекается виртуальная машина Azure с **Get-AzureVM** и сохраненные tooan существующей переменной службы автоматизации.  Как указано в разделе [Типы переменных](#variable-types), значение сохраняется в виде PSCustomObject.

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


В hello после кода hello значение извлекается из hello переменной и используется toostart hello виртуальной машины.

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a>Задание и получение коллекции в переменной

Hello следующем образце кода показано, как toouse переменную с коллекцией сложных значений в текстовых runbook. В этом образце несколько виртуальных машин Azure, извлекаются с помощью **Get-AzureVM** и сохраненные tooan существующей переменной службы автоматизации.  Как указано в разделе [Типы переменных](#variable-types), значение сохраняется в виде коллекции PSCustomObject.

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

В hello после кода hello коллекции извлекается из переменной hello и toostart каждой виртуальной машины.

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a>Графические примеры для модуля Runbook

В графический runbook, добавлении hello **Get-AutomationVariable** или **Set-AutomationVariable** , щелкнув правой кнопкой мыши на переменную hello в области библиотеки hello hello графического редактора и выбрав hello действие.

![Добавление переменной toocanvas](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a>Задание значений в переменной
Hello ниже приведен пример действия tooupdate переменную с простым значением в графический runbook. В этом примере извлекается одной виртуальной машины Azure с **Get AzureRmVM** и имя компьютера hello сохраняется tooan существующей переменной службы автоматизации с типом String.  Неважно, будет ли hello [ссылка относится конвейера или последовательность](automation-graphical-authoring-intro.md#links-and-workflow) так, как только ожидается, что один объект в выходных данных hello.

![Задание простой переменной](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a>Дальнейшие действия

* toolearn Дополнительные сведения о соединении действий вместе в графический разработки, в разделе [ссылки в графический разработки](automation-graphical-authoring-intro.md#links-and-workflow)
* tooget к работе с графический Runbook в разделе [Мой первый графический runbook](automation-first-runbook-graphical.md) 

