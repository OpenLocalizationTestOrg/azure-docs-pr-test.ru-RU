---
title: "aaaChild Runbook в автоматизации Azure | Документы Microsoft"
description: "Описывает различные методы hello запуск runbook в автоматизации Azure из другого модуля runbook и совместного использования информации между ними."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 919887b9-43e2-4c16-883c-f81807fe37db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2017
ms.author: magoedte;bwren
ms.openlocfilehash: d3d06818d344b565d53cc4f4705b41dcfcf9a376
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="child-runbooks-in-azure-automation"></a>Дочерние модули Runbook в службе автоматизации Azure
Рекомендуется в автоматизации Azure toowrite многоразовые, модульные Runbook с дискретной функцией, который может использоваться другими модулями Runbook. Родительский модуль runbook часто вызывает один или несколько дочерних модулей Runbook tooperform необходимые функциональные возможности. Существует два способа toocall дочернего модуля runbook, и каждый имеет уникальные отличия, которые следует понимать, чтобы определить, что подойдет лучше всего для различных сценариев.

## <a name="invoking-a-child-runbook-using-inline-execution"></a>Вызов дочернего Runbook с использованием встроенного выполнения
tooinvoke встроенной функции модуля runbook из другого модуля runbook используйте имя hello hello runbook и укажите значения для параметров такие же используется для действия или командлета.  Здравствуйте, все модули Runbook в одной учетной записи автоматизации еще доступны tooall других toobe используемые таким образом. Hello родительский модуль runbook будет ожидать hello дочерних runbook toocomplete перед перемещением toohello следующую строку и любые выходные данные возвращаются непосредственно toohello родительского.

При вызове встроенной функции модуля runbook он выполняется в hello же задание как hello родительский модуль runbook. Изменений в журнале заданий hello hello дочернего модуля runbook, он был запущен не будет. Любые исключения и любые выходные данные hello дочернего модуля будут связаны с родительским hello. Это приводит к меньшему числу заданий и упрощает их tootrack и tootroubleshoot после исключения, вызываемые hello дочернего модуля runbook и все выходные потока связаны с заданием родительского hello.

При публикации Runbook все дочерние Runbook, которые он вызывает, уже должны быть опубликованы. Это связано с тем, что служба автоматизации Azure создает связь с любыми дочерними Runbook при компиляции Runbook. В противном случае hello родительский модуль runbook будет правильно отображаться toopublish, но будет создавать исключение при запуске. В этом случае можно повторно опубликовать родительский модуль runbook в hello в порядке tooproperly ссылка hello дочерние модули. Toorepublish hello родительский модуль runbook не требуется, если изменены какие-либо дочерние модули hello поскольку hello связь уже была создана.

Параметры дочернего модуля runbook с вызовом встроенной Hello могут иметь любой тип данных, включая сложные объекты и имеется не [сериализации JSON](automation-starting-a-runbook.md#runbook-parameters) как при запуске runbook hello, с помощью портала управления Azure hello, или с hello Командлет Start-AzureRmAutomationRunbook.

### <a name="runbook-types"></a>Типы Runbook
Какие типы могут вызывать друг друга?

* [Runbook PowerShell](automation-runbook-types.md#powershell-runbooks)и [графические модули Runbook](automation-runbook-types.md#graphical-runbooks) могут вызывать друг друга с помощью встроенного вызова (на основе PowerShell).
* [Runbook рабочего процесса PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) и графические модули Runbook рабочего процесса PowerShell могут вызывать друг друга с помощью встроенного вызова (на основе рабочих процессов PowerShell).
* Здравствуйте типы PowerShell и приветствия типы рабочего процесса PowerShell не может вызвать друг с другом, а также должны использовать AzureRmAutomationRunbook начала.

Когда имеет значение порядок публикации?

* Hello публикации порядок имеет значение только модули Runbook для Runbook PowerShell и рабочими процессами графического рабочего процесса PowerShell.

При вызове графический или рабочий процесс PowerShell дочернего модуля runbook с использованием встроенного выполнения, просто используйте имя hello runbook hello.  При вызове дочернего модуля runbook PowerShell, необходимо перед его имя с *.\\*  toospecify, hello сценарий находится в локальном каталоге hello. 

### <a name="example"></a>Пример
Следующий пример Hello вызывается тестовый дочерний модуль runbook, принимающий три параметра, сложный объект, целое число и логическое значение. выходные данные дочернего модуля hello Hello назначается переменной tooa.  В этом случае hello дочерний модуль является runbook рабочего процесса PowerShell

    $vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
    $output = PSWF-ChildRunbook –VM $vm –RepeatCount 2 –Restart $true

Ниже приведен hello же пример с использованием модуля PowerShell как дочерний hello.

    $vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
    $output = .\PS-ChildRunbook.ps1 –VM $vm –RepeatCount 2 –Restart $true


## <a name="starting-a-child-runbook-using-cmdlet"></a>Запуск дочернего Runbook с помощью командлета
Можно использовать hello [начала AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart командлет runbook, как описано в [toostart runbook с помощью Windows PowerShell](automation-starting-a-runbook.md#starting-a-runbook-with-windows-powershell). Этот командлет можно использовать в двух режимах.  В одном режиме hello командлет возвращает идентификатор задания hello, сразу после создания hello дочерние задания для hello дочернего модуля.  В другом режиме можно включить, указав hello Здравствуйте, **-ожидания** параметр, командлет hello период ожидания hello дочерние задания завершается и возвращает hello выходные данные из дочернего модуля runbook hello.

Задание Hello из дочернего модуля runbook, запущенное с помощью командлета будет выполняться в отдельном задании из родительского модуля hello. Это приводит к увеличению числа заданий, чем при вызове встроенной функции модуля runbook hello и делает их более сложным tootrack. родительский Hello можно запустить несколько дочерних модулей асинхронно без ожидания завершения каждого toocomplete. Для такого же вида параллельного выполнения вызова hello дочерние модули Runbook встроенной функции hello родительский модуль runbook, потребуется toouse hello [параллельных ключевое слово](automation-powershell-workflow.md#parallel-processing).

Параметры дочернего Runbook, запускаемого с помощью командлета, предоставляются в виде хэш-таблицы, как описано в статье [Параметры Runbook](automation-starting-a-runbook.md#runbook-parameters). Можно использовать только простые типы данных. Если hello runbook имеет параметр со сложным типом данных, затем его необходимо вызывать в коде.

### <a name="example"></a>Пример
Hello следующем примере запускается дочерний модуль runbook с параметрами и затем ожидает toocomplete с помощью hello Start AzureRmAutomationRunbook-ожидания параметра. После завершения его выходные данные из дочернего модуля hello.

    $params = @{"VMName"="MyVM";"RepeatCount"=2;"Restart"=$true} 
    $joboutput = Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-ChildRunbook" -ResourceGroupName "LabRG" –Parameters $params –wait


## <a name="comparison-of-methods-for-calling-a-child-runbook"></a>Сравнение методов вызова дочернего Runbook
Hello следующей таблице представлены различия hello hello два метода для вызова модуля runbook из другого модуля runbook.

|  | Встроенный | Командлет |
|:--- |:--- |:--- |
| Задание |Дочерние модули Runbook выполняются в hello же задание как родительский hello. |Для hello дочернего модуля runbook создается отдельное задание. |
| Выполнение |Родительский модуль runbook ожидает hello дочерних runbook toocomplete перед продолжением. |Родительский модуль runbook продолжает работу сразу после запуска дочернего модуля runbook *или* родительский модуль runbook ожидает hello дочерние задания toofinish. |
| Выходные данные |Родительский Runbook может получить выходные данные непосредственно из дочернего Runbook. |Родительский модуль Runbook должен получить выходные данные из задания дочернего модуля Runbook *или* может получить выходные данные непосредственно из дочернего модуля Runbook. |
| Параметры |Значения для параметров hello дочерних модулей runbook указываются отдельно и могут использовать любой тип данных. |Значения для дочернего модуля hello параметры должны быть объединены в одну хэш-таблицу и могут содержать только простой, массива или объекта, что типы данных, использующие сериализацию JSON. |
| Учетная запись службы автоматизации |Родительский модуль runbook можно использовать только дочерний модуль в hello одной учетной записи автоматизации. |Родительский модуль runbook можно использовать дочерний модуль из любой учетной записи автоматизации hello одной подписке Azure и даже в других подписках при наличии tooit соединения. |
| Публикация |Перед публикацией родительского Runbook должен быть опубликован дочерний Runbook. |Дочерний Runbook должен быть опубликован в любое время до запуска родительского Runbook. |

## <a name="next-steps"></a>Дальнейшие действия
* [Запуск модуля Runbook в службе автоматизации Azure](automation-starting-a-runbook.md)
* [Выходные данные и сообщения Runbook в службе автоматизации Azure](automation-runbook-output-and-messages.md)

