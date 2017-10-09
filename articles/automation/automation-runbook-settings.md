---
title: "Параметры aaaRunbook | Документы Microsoft"
description: "Описывает hello параметры конфигурации для модуля runbook в автоматизации Azure и как toochange их с помощью обоих hello портал управления Azure и Windows PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: a726f20c-a952-48b8-88ee-36d76aa3ac61
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: bwren
ms.openlocfilehash: 6f0ef09c148355a351464424c22c33df9300f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-settings"></a>Параметры модуля Runbook
Каждый модуль runbook в автоматизации Azure имеется несколько параметров, помочь идентифицировать toobe и toochange его поведение при входе. Каждый из этих параметров описан ниже следуют процедуры о том, как toomodify их.

## <a name="settings"></a>данных
### <a name="name-and-description"></a>Имя и описание
Hello имя модуля runbook невозможно изменить после его создания. Hello описание является необязательным и может быть вверх too512 символов.

### <a name="tags"></a>Теги
Разрешить теги вы tooassign отдельные слова и фразы toohelp идентификации модуля runbook. Например, при отправке runbook toohello [коллекции PowerShell](https://www.powershellgallery.com/), укажите tooidentify теги определенной категории hello runbook должны быть перечислены в. Вы можете указать несколько тегов модуля Runbook, разделив их запятой.

### <a name="logging"></a>Ведение журналов
По умолчанию записи Verbose и Progress не записываются toojob журнала. Параметры hello для toolog конкретного модуля runbook можно изменить эти записи. Дополнительные сведения об этих записях см. в статье [Выходные данные и сообщения Runbook в службе автоматизации Azure](automation-runbook-output-and-messages.md).

## <a name="changing-runbook-settings"></a>Изменение параметров модуля Runbook

### <a name="changing-runbook-settings-with-hello-azure-portal"></a>Изменение параметров модуля runbook с hello портал Azure
Можно изменить параметры модуля Runbook на портал Azure hello из hello **параметры** колонке hello runbook.

1. В hello портал Azure, выберите **автоматизации** и нажмите кнопку hello имя учетной записи автоматизации.
2. Выберите hello **Runbooks** вкладки.
3. Щелкните имя runbook hello и являются направленной toohello колонку параметров для модуля runbook hello. Здесь можно указать или изменять теги, hello описание runbook, настройте ведение журнала и параметры трассировки и toohelp средства поддержки устранения проблем доступа к.     

### <a name="changing-runbook-settings-with-windows-powershell"></a>Изменение параметров модуля Runbook с помощью Windows PowerShell
Можно использовать hello [AzureRmAutomationRunbook набор](https://msdn.microsoft.com/library/mt603786.aspx) командлет toochange hello параметров модуля runbook. Если вы хотите toospecify несколько тегов, можно либо добавить массив или одной строки с параметром теги toohello значений с разделителями-запятыми. Вы можете получить текущие теги hello с hello [Get AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).

Привет, следующие примеры команд показывают, как tooset hello свойств для модуля runbook. В этом примере добавляется три тега toohello существующие теги и указывает, что подробные записи следует вносить в журнал.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a>Дальнейшие действия
* toolearn toocreate и получение выходных данных и сообщения об ошибках из модулей Runbook, в статье [Runbook Output and Messages](automation-runbook-output-and-messages.md) 
* toounderstand tooadd runbook, который уже разрабатывался hello сообщества или другой источник или toocreate собственные runbook. в статье [Создание или импорт модуля Runbook](automation-creating-importing-runbook.md) 

