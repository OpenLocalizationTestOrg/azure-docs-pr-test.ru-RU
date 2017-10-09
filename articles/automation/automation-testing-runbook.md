---
title: "aaaTesting runbook в автоматизации Azure | Документы Microsoft"
description: "Прежде чем опубликовать книгу в службе автоматизации Azure, можно проверить его tooensure, который работает как ожидалось.  В этой статье описывается как tootest runbook и просмотра его результатов."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 7f7db785-52c0-4613-aa12-b02fd32a5182
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 8c531f702699d586f8215d4c171cb0ecf94732b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="testing-a-runbook-in-azure-automation"></a>Тестирование модуля Runbook в службе автоматизации Azure
При тестировании модуля hello [черновую версию](automation-creating-importing-runbook.md#publishing-a-runbook) выполняется и все действия, которые он выполняет. Журнал заданий не создается, но hello [вывода](automation-runbook-output-and-messages.md#output-stream) и [предупреждения и ошибки](automation-runbook-output-and-messages.md#message-streams) отображаются потоки в hello область вывода теста. Сообщения toohello [Verbose Stream](automation-runbook-output-and-messages.md#message-streams) отображаются в области вывода hello, только если hello [переменной $VerbosePreference](automation-runbook-output-and-messages.md#preference-variables) имеет значение tooContinue.

Несмотря на то, что выполняется hello черновик hello runbook по-прежнему обычно запускает рабочий процесс hello и выполняет все действия — в ресурсах в среде hello. В связи с этим тестировать модули Runbook можно только в непроизводственных ресурсах.

Здравствуйте, процедура tootest [тип runbook](automation-runbook-types.md) же hello и нет никаких различий в тестировании hello текстового редактора и hello графического редактора в hello портал Azure.  

## <a name="tootest-a-runbook-in-hello-azure-portal"></a>tootest runbook в hello портал Azure
Можно работать с любым [тип runbook](automation-runbook-types.md) в hello портал Azure.

1. Hello откройте черновик runbook hello в любом hello [текстового редактора](automation-edit-textual-runbook.md) или [графического редактора](automation-graphical-authoring-intro.md).
2. Щелкните hello **тест** кнопку tooopen hello теста колонку.
3. Если hello runbook имеет параметры, они отображаются в левой области hello, где можно ввести toobe значения, используемые для тестирования hello.
4. Если тест hello toorun на [гибридной рабочей ролью Runbook](automation-hybrid-runbook-worker.md), затем измените **параметры запуска** слишком**гибридной рабочей роли** и выберите hello имя целевой группы hello.  В противном случае оставьте по умолчанию hello **Azure** toorun hello тестирования в облаке hello.
5. Нажмите кнопку hello **запустить** тест hello toostart кнопок.
6. Если hello runbook [рабочего процесса PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) или [Graphical](automation-runbook-types.md#graphical-runbooks), то можно остановить или приостановить его, пока проверяется с кнопки hello hello области вывода. При приостановке hello runbook сначала завершает текущее действие hello. После приостановки hello runbook можно остановить или перезапустить его.
7. Анализировать результаты hello runbook hello в области вывода hello.

## <a name="next-steps"></a>Дальнейшие действия
* toolearn toocreate или импорт модуля runbook. в статье [Создание или импорт модуля runbook в автоматизации Azure](automation-creating-importing-runbook.md)
* toolearn Дополнительные сведения о графических разработки. в разделе [графический разработки автоматизации Azure](automation-graphical-authoring-intro.md)
* tooget к работе с PowerShell модули Runbook рабочего процесса, в разделе [Мой первый runbook рабочего процесса PowerShell](automation-first-runbook-textual.md)
* toolearn подробные сведения о настройке runboks tooreturn сообщения о состоянии и ошибках, включая рекомендации см. в разделе [Runbook выходные данные и сообщения в службе автоматизации Azure](automation-runbook-output-and-messages.md)

