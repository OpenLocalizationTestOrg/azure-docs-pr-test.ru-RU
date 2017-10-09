---
title: "aaaCreating или импорт модуля runbook в автоматизации Azure"
description: "В этой статье описывается как toocreate новый модуль runbook в автоматизации Azure или один Импорт из файла."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 24414362-b690-4474-8ca7-df18e30fc31d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: d45f44cf15fbcacdd0de2977668502c2e1671063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-or-importing-a-runbook-in-azure-automation"></a>Создание или импорт модуля Runbook в службе автоматизации Azure
Можно добавить tooAzure runbook автоматизации с помощью [созданием нового](#creating-a-new-runbook) или путем импорта существующего модуля runbook из файла или из hello [коллекции модулей Runbook](automation-runbook-gallery.md). В этой статье рассказывается, как создавать и импортировать модули Runbook из файла.  Можно получить все hello сведения о доступе к сообществу Runbook и модули в [Runbook и модулей галерей для службы автоматизации Azure](automation-runbook-gallery.md).

## <a name="creating-a-new-runbook"></a>Создание нового модуля Runbook
Можно создать новый модуль runbook в автоматизации Azure с помощью одного из hello Azure порталы или Windows PowerShell. После создания hello runbook можно изменить, используя информацию в [рабочего процесса PowerShell обучения](automation-powershell-workflow.md) и [графический разработки в Azure Automation](automation-graphical-authoring-intro.md).

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-classic-portal"></a>toocreate runbook службы автоматизации Azure с портала Azure Classic hello
Можно работать только с [модулях Runbook рабочего процесса PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) в hello портал Azure.

1. Hello Azure классическом портале нажмите кнопку, **New**, **службы приложений**, **автоматизации**, **Runbook**, **быстрое создание**.
2. Введите hello необходимые сведения и нажмите кнопку **создать**. Имя runbook Hello должно начинаться с буквы и может иметь буквы, цифры, знаки подчеркивания и тире.
3. Если вы хотите tooedit hello runbook сейчас, нажмите кнопку **изменить Runbook**. В противном случае нажмите кнопку **ОК**.
4. Новый модуль runbook появится на hello **Runbooks** вкладки.

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-portal"></a>toocreate runbook службы автоматизации Azure с hello портал Azure
1. Откройте в hello портал Azure, ваша учетная запись автоматизации.
2. Hello концентратора, выберите **Runbooks** tooopen hello список модулей Runbook.
3. Щелкните hello **добавить модуль runbook** кнопки и затем **создать новый runbook**.
4. Введите значение **имя** для hello runbook и выберите его [типа](automation-runbook-types.md). Имя runbook Hello должно начинаться с буквы и может иметь буквы, цифры, знаки подчеркивания и тире.
5. Нажмите кнопку **создать** toocreate hello runbook и Привет открыть редактор.

### <a name="toocreate-a-new-azure-automation-runbook-with-windows-powershell"></a>toocreate runbook службы автоматизации Azure с помощью Windows PowerShell
Можно использовать hello [New AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt619376.aspx) toocreate командлет пустой [runbook рабочего процесса PowerShell](automation-runbook-types.md#powershell-workflow-runbooks). Можно либо указать hello **имя** toocreate параметр пустой модуль runbook, можно изменить позже, или можно указать hello **путь** параметр tooimport файл runbook. Hello **тип** параметр также должен быть включен toospecify один из типов runbook 4 hello.

Hello следующем образце команд Показать как toocreate новый пустой runbook.

    New-AzureRmAutomationRunbook -AutomationAccountName MyAccount `
    -Name NewRunbook -ResourceGroupName MyResourceGroup -Type PowerShell

## <a name="importing-a-runbook-from-a-file-into-azure-automation"></a>Импорт модуля из файла в службу автоматизации Azure
Для создания модуля Runbook в службе автоматизации Azure можно импортировать сценарий или рабочий процесс PowerShell (с расширением PS1) или экспортировать графический модуль Runbook (с расширением GRAPHRUNBOOK).  Необходимо указать hello [тип runbook](automation-runbook-types.md) , будет создан на основе импорта hello, учитывая следующие рекомендации hello учетной записи.

* Файл GRAPHRUNBOOK может быть импортирован только в новый [графический модуль Runbook](automation-runbook-types.md#graphical-runbooks), а графические модули Runbook могут быть созданы только из файла GRAPHRUNBOOK.
* Файл PS1 с рабочим процессом PowerShell можно импортировать только в [модуль Runbook рабочего процесса PowerShell](automation-runbook-types.md#powershell-workflow-runbooks).  Если файл hello содержит несколько рабочих процессов PowerShell, затем hello Импорт завершится ошибкой. Необходимо сохранить каждый рабочий процесс tooits собственный файл и импортировать их раздельно.
* Файл PS1 без рабочего процесса можно импортировать либо в [модуль Runbook PowerShell](automation-runbook-types.md#powershell-runbooks), либо в [модуль Runbook рабочего процесса PowerShell](automation-runbook-types.md#powershell-workflow-runbooks).  Если импортируется в runbook рабочего процесса PowerShell, то оно будет преобразованный tooa рабочего процесса и комментарии будут включены в runbook hello, указав hello изменений, внесенных.

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-classic-portal"></a>tooimport runbook из файла с портала Azure Classic hello
Можно использовать следующие процедуры tooimport файл скрипта в автоматизации Azure hello.  Обратите внимание, что с помощью этого портала файл PS1 можно импортировать только в модуль Runbook рабочего процесса PowerShell.  Hello портала Azure необходимо использовать для других типов.

1. На портале управления Azure hello, выберите **автоматизации** и выберите учетную запись автоматизации.
2. Щелкните **Импорт**.
3. Нажмите кнопку **поиск файла** и найдите tooimport файл скрипта hello.
4. Если вы хотите tooedit hello runbook сейчас, нажмите кнопку **изменить Runbook**. В противном случае нажмите кнопку «ОК».
5. Hello новый модуль runbook появится на hello **Runbooks** вкладке hello учетной записи автоматизации.
6. Вы должны [опубликовать hello runbook](#publishing-a-runbook) перед его запуском.

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-portal"></a>tooimport runbook из файла с hello портал Azure
Можно использовать следующие процедуры tooimport файл скрипта в автоматизации Azure hello.  

> [!NOTE]
> Обратите внимание, что ps1-файл можно импортировать только в runbook рабочего процесса PowerShell с помощью портала hello.
> 
> 

1. Откройте в hello портал Azure, ваша учетная запись автоматизации.
2. Hello концентратора, выберите **Runbooks** tooopen hello список модулей Runbook.
3. Щелкните hello **добавить модуль runbook** кнопки и затем **импорта**.
4. Нажмите кнопку **файл Runbook** файл tooimport tooselect hello
5. Если hello **имя** поля включено, то у вас есть параметр toochange hello его.  Имя runbook Hello должно начинаться с буквы и может иметь буквы, цифры, знаки подчеркивания и тире.
6. Hello [тип runbook](automation-runbook-types.md) выбирается автоматически, но можно изменить тип hello после перевода hello применимые ограничения в учетную запись. 
7. Hello новый модуль runbook будет отображаться в списке hello модулей Runbook для hello учетной записи автоматизации.
8. Вы должны [опубликовать hello runbook](#publishing-a-runbook) перед его запуском.

> [!NOTE]
> После импорта графический runbook или графический runbook рабочих процессов PowerShell имеется toohello tooconvert параметр hello другого типа переход. Не удается преобразовать tootextual.
> 
> 

### <a name="tooimport-a-runbook-from-a-script-file-with-windows-powershell"></a>tooimport runbook из файла сценария с помощью Windows PowerShell
Можно использовать hello [AzureRMAutomationRunbook импорта](https://msdn.microsoft.com/library/mt603735.aspx) tooimport командлет файл скрипта как черновик runbook рабочего процесса PowerShell. Если hello runbook уже существует, hello Импорт завершится ошибкой, если вы не используете hello *-Force* параметра. 

Привет, следующие примеры команд показывают, как файл tooimport сценария в модуль runbook.

    $automationAccountName =  "AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $scriptPath = "C:\Runbooks\Sample_TestRunbook.ps1"
    $RGName = "ResourceGroup"

    Import-AzureRMAutomationRunbook -Name $runbookName -Path $scriptPath `
    -ResourceGroupName $RGName -AutomationAccountName $automationAccountName `
    -Type PowerShellWorkflow 


## <a name="publishing-a-runbook"></a>Публикация модуля Runbook
Перед запуском вновь созданного или импортированного модуля Runbook его необходимо опубликовать.  У каждого Runbook в службе автоматизации есть черновая и опубликованная версия. Hello только опубликованная версия является доступной toobe запуска, и можно изменить только hello черновую версию. не влияет на все изменения toohello черновую версию Hello опубликованную версию. Когда hello черновой версии должны быть доступны, опубликуйте hello черновик заменяет опубликованную версию hello.

## <a name="toopublish-a-runbook-using-hello-azure-classic-portal"></a>toopublish a runbook с помощью портала Azure Classic hello
1. Откройте hello hello Azure классического портала.
2. Hello в верхней части экрана приветствия, нажмите кнопку **автор**.
3. Hello нижней части экрана приветствия, нажмите кнопку **публикации** и затем **Да** toohello проверочном сообщении.

## <a name="toopublish-a-runbook-using-hello-azure-portal"></a>toopublish a runbook с помощью портала Azure hello
1. Откройте hello в hello портал Azure.
2. Нажмите кнопку hello **изменить** кнопки.
3. Нажмите кнопку hello **публикации** кнопки и затем **Да** toohello проверочном сообщении.

## <a name="toopublish-a-runbook-using-windows-powershell"></a>toopublish модуля runbook с помощью Windows PowerShell
Можно использовать hello [AzureRmAutomationRunbook публикации](https://msdn.microsoft.com/library/mt603705.aspx) командлет toopublish runbook с помощью Windows PowerShell. Hello следующем образце команд Показать как toopublish пример модуля runbook.

    $automationAccountName =  AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $RGName = "ResourceGroup"

    Publish-AzureRmAutomationRunbook -AutomationAccountName $automationAccountName `
    -Name $runbookName -ResourceGroupName $RGName


## <a name="next-steps"></a>Дальнейшие действия
* в разделе toolearn о том, как вы можете выиграть от hello Runbook и PowerShell в коллекции модулей, [Runbook и модулей галерей для службы автоматизации Azure](automation-runbook-gallery.md)
* toolearn Дополнительные сведения о редактирования модулей Runbook PowerShell и рабочий процесс PowerShell с помощью текстового редактора в разделе [редактирования текстовое Runbook в автоматизации Azure](automation-edit-textual-runbook.md)
* в разделе toolearn Дополнительные сведения о создании графического модуля runbook, [графический разработки автоматизации Azure](automation-graphical-authoring-intro.md)

