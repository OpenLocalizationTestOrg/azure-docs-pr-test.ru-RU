---
title: "aaaEditing текстовое Runbook в автоматизации Azure"
description: "Также приводятся различные процедуры для работы с PowerShell и рабочий процесс PowerShell модули Runbook в автоматизации Azure с помощью текстового редактора hello."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: 6f5b48fb-6f30-4e99-9e14-9061b5554b08
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 3fd87d457838f300ca6c94bc345e82c679a0e011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="editing-textual-runbooks-in-azure-automation"></a>Изменение текстовых модулей Runbook в службе автоматизации Azure
Hello текстового редактора в службе автоматизации Azure можно использовать tooedit [PowerShell модули Runbook](automation-runbook-types.md#powershell-runbooks) и [модулях Runbook рабочего процесса PowerShell](automation-runbook-types.md#powershell-workflow-runbooks). Это имеет стандартные функции hello другие редакторы кода, такие как intellisense и выделение цветом с tooassist Дополнительные специальные возможности вам в доступе к toorunbooks общие ресурсы.  В этой статье подробно описано, как использовать этот редактор для выполнения разнообразных задач.

Hello текстового редактора включает код функции tooinsert для действий, средств и дочерние модули Runbook в runbook. Вместо того чтобы вводить код hello самостоятельно, можно выбрать из списка доступных ресурсов и hello вставить соответствующий код в hello runbook.

У каждого модуля Runbook в службе автоматизации Azure есть черновая и опубликованная версия. Изменить hello черновик hello runbook и затем опубликовать с возможностью выполнения. Hello опубликованную версию невозможно редактировать. Дополнительные сведения см. в статье [Публикация модуля Runbook](automation-creating-importing-runbook.md#publishing-a-runbook).

toowork с [графические модули Runbook](automation-runbook-types.md#graphical-runbooks), в разделе [графический разработки в Azure Automation](automation-graphical-authoring-intro.md).

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a>tooedit runbook с hello портал Azure
Используйте следующие процедуры tooopen runbook для редактирования в текстовом редакторе hello hello.

1. В hello портал Azure выберите учетную запись автоматизации.
2. Нажмите кнопку hello **Runbooks** плитки tooopen hello список модулей Runbook.
3. Щелкните имя hello hello модуля Runbook вы хотите tooedit, а затем нажмите кнопку hello **изменить** кнопки.
4. Выполните необходимые изменения hello.
5. Закончив изменения, нажмите кнопку **Сохранить** .
6. Нажмите кнопку **публикации** Если hello последнюю версию черновика toobe runbook hello публикации.

### <a name="tooinsert-a-cmdlet-into-a-runbook"></a>tooinsert командлета в модуле runbook
1. В hello холст hello текстового редактора поместите курсор hello место, где tooplace hello командлета.
2. Разверните hello **командлеты** узел в hello элемент управления из библиотеки.
3. Разверните hello модуль, содержащий требуется toouse командлет hello.
4. Щелкните правой кнопкой мыши tooinsert командлет hello и выберите **добавить toocanvas**.  Если командлет hello имеет более одного набора параметров, будет добавлен набор по умолчанию hello.  Также можно развернуть tooselect командлет hello другие параметры задать.
5. Код Hello для командлета hello вставляется с весь список параметров.
6. Укажите соответствующее значение вместо типа данных hello, заключенных в фигурные скобки <> для все необходимые параметры.  Все ненужные параметры удалите.

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a>Код tooinsert для дочернего модуля runbook в runbook
1. В hello холст hello текстового редактора, поместите курсор hello место кода hello tooplace для hello [дочернего модуля](automation-child-runbooks.md).
2. Разверните hello **Runbooks** узел в hello элемент управления из библиотеки.
3. Щелкните правой кнопкой мыши hello runbook tooinsert и выберите **добавить toocanvas**.
4. любой местозаполнители для любых параметров модуля runbook будет вставлен код Hello hello дочернего модуля runbook.
5. Замените заполнители hello соответствующие значения для каждого параметра.

### <a name="tooinsert-an-asset-into-a-runbook"></a>tooinsert актива в модуль runbook
1. В hello холст hello текстового редактора поместите курсор hello место кода hello tooplace для hello дочернего модуля.
2. Разверните hello **активы** узел в hello элемент управления из библиотеки.
3. Разверните узел hello hello тип ресурса.
4. Щелкните правой кнопкой мыши tooinsert активов hello и выберите **добавить toocanvas**.  Для [ресурсы переменных](automation-variables.md), выберите либо **добавить «Получить переменную» toocanvas** или **toocanvas «Задать переменную» добавить** в зависимости от того, вы хотите tooget или задайте переменную hello.
5. Код Hello средства hello вставляется hello runbook.

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a>tooedit runbook с hello портал Azure
Используйте следующие процедуры tooopen runbook для редактирования в текстовом редакторе hello hello.

1. В hello портал Azure, выберите **автоматизации** и нажмите кнопку hello имя учетной записи автоматизации.
2. Выберите hello **Runbooks** вкладки.
3. Щелкните имя hello hello модуля Runbook tooedit и затем выберите hello **автор** вкладки.
4. Нажмите кнопку hello **изменить** кнопку hello нижней части экрана приветствия.
5. Выполните необходимые изменения hello.
6. Закончив изменения, нажмите кнопку **Сохранить** .
7. Нажмите кнопку **публикации** Если hello последнюю версию черновика toobe runbook hello публикации.

### <a name="tooinsert-an-activity-into-a-runbook"></a>tooinsert действие в Runbook
1. В hello холст hello текстового редактора поместите курсор hello место, где tooplace hello действия.
2. Hello нижней части экрана приветствия, нажмите кнопку **вставить** и затем **действия**.
3. В hello **модуль интеграции** столбец, выберите hello модуль, содержащий действие hello.
4. В hello **действия** области, выберите действие.
5. В hello **описание** столбец Примечание hello описание действия hello. При необходимости можно щелкнуть подробные справки toolaunch Справка для действия "hello" в браузере hello.
6. Нажмите кнопку со стрелкой вправо hello.  Если hello действии есть параметры, они будут указаны для справки.
7. Нажмите кнопку "Проверить" hello ".  Действие hello toorun кода будет вставлен в hello runbook.
8. Если действие hello требуются параметры, укажите соответствующее значение вместо типа данных hello, заключенных в фигурные скобки <>.

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a>Код tooinsert для дочернего модуля runbook в runbook
1. В hello холст hello текстового редактора, поместите курсор hello место tooplace hello [дочернего модуля](automation-child-runbooks.md).
2. Hello нижней части экрана приветствия, нажмите кнопку **вставить** и затем **Runbook**.
3. Выберите hello runbook tooinsert hello центрального столбца и нажмите кнопку со стрелкой вправо hello.
4. Если hello runbook имеет параметры, они будут указаны для справки.
5. Нажмите кнопку "Проверить" hello ".  Код toorun hello выбран runbook будет вставлен в текущий runbook hello.
6. Если hello runbook требуются параметры, укажите соответствующее значение вместо типа данных hello, заключенных в фигурные скобки <>.

### <a name="tooinsert-an-asset-into-a-runbook"></a>tooinsert актива в модуль runbook
1. В hello холст hello текстового редактора поместите курсор hello место, где tooplace hello действия tooretrieve hello активов.
2. Hello нижней части экрана приветствия, нажмите кнопку **вставить** и затем **параметр**.
3. В hello **действие параметра** столбец, выберите hello действие, которое требуется.
4. Выберите из доступных ресурсов hello в центральном столбце hello.
5. Нажмите кнопку "Проверить" hello ".  Код tooget или набор средств hello будет вставлен в hello runbook.

## <a name="tooedit-an-azure-automation-runbook-using-windows-powershell"></a>tooedit runbook службы автоматизации Azure с помощью Windows PowerShell
tooedit runbook с помощью Windows PowerShell можно использовать любой редактор hello и сохраните его tooa ps1-файл. Можно использовать hello [Get-AzureAutomationRunbookDefinition](http://aka.ms/runbookauthor/cmdlet/getazurerunbookdefinition) командлет tooretrieve hello содержимого hello runbook и затем [Set-AzureAutomationRunbookDefinition](http://aka.ms/runbookauthor/cmdlet/setazurerunbookdefinition) существующие hello tooreplace командлета черновик runbook с hello изменен один.

### <a name="tooretrieve-hello-contents-of-a-runbook-using-windows-powershell"></a>Здравствуйте, tooRetrieve содержимое модуля Runbook с помощью Windows PowerShell
Привет, следующие примеры команд показывают, как tooretrieve hello сценария для модуля runbook и сохранить его в файл сценария tooa. В этом примере выполняется получение черновика hello. Это также возможно tooretrieve hello опубликованную версию модуля runbook hello, несмотря на то, что эта версия не может изменяться.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    $runbookDefinition = Get-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Slot Draft
    $runbookContent = $runbookDefinition.Content

    Out-File -InputObject $runbookContent -FilePath $scriptPath

### <a name="toochange-hello-contents-of-a-runbook-using-windows-powershell"></a>Здравствуйте, tooChange содержимое модуля Runbook с помощью Windows PowerShell
Hello следующие примеры команд показывают, как tooreplace hello существующее содержимое модуля runbook с hello содержимым файла сценария. Обратите внимание, что это hello же пример процедуры в качестве [tooimport runbook из файла сценария с помощью Windows PowerShell](automation-creating-importing-runbook.md).

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    Set-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Path $scriptPath -Overwrite
    Publish-AzureAutomationRunbook –AutomationAccountName $automationAccountName –Name $runbookName

## <a name="related-articles"></a>Связанные статьи
* [Создание или импорт модуля Runbook в службе автоматизации Azure](automation-creating-importing-runbook.md)
* [Изучение рабочего процесса PowerShell](automation-powershell-workflow.md)
* [Графическая разработка в службе автоматизации Azure](automation-graphical-authoring-intro.md)
* [Сертификаты](automation-certificates.md)
* [Подключения](automation-connections.md)
* [Учетные данные](automation-credentials.md)
* [Расписания](automation-schedules.md)
* [Переменные](automation-variables.md)
