---
title: "выполнение aaaRunbook в службе автоматизации Azure | Документы Microsoft"
description: "Описывает hello сведения об обработке runbook в автоматизации Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d10c8ce2-2c0b-4ea7-ba3c-d20e09b2c9ca
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2017
ms.author: bwren
ms.openlocfilehash: bdb535675443353d44640bc7773de3f9dac5e42c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-execution-in-azure-automation"></a>Выполнение модуля Runbook в службе автоматизации Azure
При запуске модуля Runbook в службе автоматизации Azure создается задание. Задание — это одиночный выполняемый экземпляр модуля Runbook. Рабочая роль Azure автоматизации назначенный toorun каждого задания. Пока рабочие процессы используются несколькими учетными записями Azure, задания от различных учетных записей службы автоматизации изолируются друг от друга. У вас контроль над какой рабочий служб hello запрос для задания.  В одном модуле Runbook могут иметься несколько запущенных заданий одновременно. При просмотре списка hello модулей Runbook в hello портал Azure, в нем перечислены hello состояния всех заданий, которые были запущены для каждого модуля runbook. Можно просмотреть список hello задания для каждого модуля в порядке tootrack hello состояние каждого. Описание hello различных состояний задания см. в разделе [состояний задания](#job-statuses).

Hello следующей диаграмме показан жизненный цикл hello задания для runbook [графические модули Runbook](automation-runbook-types.md#graphical-runbooks) и [модулях Runbook рабочего процесса PowerShell](automation-runbook-types.md#powershell-workflow-runbooks).

![Состояния задания — рабочий процесс PowerShell](./media/automation-runbook-execution/job-statuses.png)

Hello следующей диаграмме показан жизненный цикл hello задания для runbook [PowerShell модули Runbook](automation-runbook-types.md#powershell-runbooks).

![Состояния задания — сценарий PowerShell](./media/automation-runbook-execution/job-statuses-script.png)

Ваш задания имеют доступ tooyour Azure ресурсы, делая соединения tooyour подписки Azure. Они достаточно tooresources доступа в центре обработки данных, если эти ресурсы были доступны из общедоступного облака hello.

## <a name="job-statuses"></a>Состояния заданий
Hello следующей таблице описаны hello различные возможные состояния для задания.

| Состояние | Описание |
|:--- |:--- |
| Завершено |Hello задание успешно завершено. |
| Сбой |Для [Graphical и рабочий процесс PowerShell модули Runbook](automation-runbook-types.md), toocompile сбой hello runbook.  Для [сценарий PowerShell модули Runbook](automation-runbook-types.md), hello runbook сбой toostart или hello задания возникло исключение. |
| Задание не выполнено. Ожидание ресурсов. |Сбой задания Hello, так как он достиг hello [справедливое](#fairshare) ограничить три раза и запускать из hello же контрольной точки или из hello hello модуля Runbook каждый раз запускать. |
| Поставлено в очередь |Hello задание ожидает ресурсов на доступные toocome работника автоматизации, чтобы оно смогло запуститься. |
| Starting |Hello задание было назначено tooa работника и hello система находится в процессе его запуска hello. |
| Возобновление |Hello система находится в hello процесс возобновления hello задания после его приостановки. |
| Выполнение |Hello задание выполняется. |
| Задание выполняется. Ожидание ресурсов. |Hello задание был выгружено, так как он достиг hello [справедливое](#fairshare) ограничение. Задание будет возобновлено позже с его последней контрольной точки. |
| Остановлено |Hello задание остановлено пользователем hello, до его завершения. |
| Остановка |Hello система находится в hello процесс остановки задания hello. |
| Приостановлено |Hello задание было приостановлено пользователем hello, hello системой или с помощью команды в hello runbook. Приостановленное задание можно запустить снова и возобновить с последней контрольной точки или hello начало hello runbook при отсутствии контрольных точек. Hello runbook будет приостановлен только системой hello при возникновении исключения. По умолчанию, ErrorActionPreference задано слишком**Продолжить**, то есть задания hello продолжит выполнение при возникновении ошибки. Если эта Привилегированная переменная имеет значение слишком**остановить**, а затем приостанавливает задание hello в случае ошибки.  Также применяется[Graphical и рабочий процесс PowerShell модули Runbook](automation-runbook-types.md) только. |
| Приостановка |Hello система пытается toosuspend hello задания по запросу hello hello пользователя. Прежде чем можно будет приостановить, Hello runbook должен достичь своей следующей контрольной точки. Если последняя контрольная точка уже пройдена, задание будет завершено, прежде чем оно будет приостановлено.  Также применяется[Graphical и рабочий процесс PowerShell модули Runbook](automation-runbook-types.md) только. |

## <a name="viewing-job-status-from-hello-azure-portal"></a>Просмотр состояния задания из hello портал Azure
Можно просмотреть сводные данные состояния всех заданий runbook или детализировать сведения об указанном задании runbook в hello портал Azure или с настройкой интеграции с состояние задания runbook tooforward рабочей области аналитики журналов Microsoft Operations Management Suite (OMS) и потоки задания.  Дополнительные сведения об интеграции с помощью аналитики журналов OMS см. в разделе [вперед от tooLog автоматизации Analytics (OMS) состояние задания и задания потоки](automation-manage-send-joblogs-log-analytics.md).  

### <a name="automation-runbook-jobs-summary"></a>Сводные данные заданий Runbook службы автоматизации
На hello справа от выбранной учетной записи автоматизации, можно просмотреть сводку по всем hello заданиях для выбранной учетной записи автоматизации в **статистике** плитки.<br><br> ![Элемент "Статистика по заданиям"](./media/automation-runbook-execution/automation-account-job-status-summary.png).<br> Эта Плитка отображается число и графическое представление о состоянии задания hello для всех выполненных заданий.  

При щелчке плитки приветствия представляется hello **заданий** колонки, включая сводные список всех выполненных заданий, с состояние выполнения задания и время начала и завершения.<br><br> ![Колонка "Задания" учетной записи службы автоматизации](./media/automation-runbook-execution/automation-account-jobs-status-blade.png)<br><br>  Можно фильтровать список заданий hello, выбрав **Фильтрация заданий** и фильтрации определенного модуля runbook, состояние задания, или из раскрывающегося списка hello, hello toosearch диапазон даты и времени в пределах.<br><br> ![Фильтрация по состоянию задания](./media/automation-runbook-execution/automation-account-jobs-filter.png)

Кроме того, можно просмотреть сводные данные задания для определенного модуля runbook, выбрав этого модуля из hello **Runbooks** колонки в вашей учетной записи автоматизации и выберите hello **заданий** плитку.  Это представляет hello **заданий** колонке и из него можно щелкнуть hello задания записи tooview сведения о нем и выходных данных.<br><br> ![Колонка "Задания" учетной записи службы автоматизации](./media/automation-runbook-execution/automation-runbook-job-summary-blade.png)<br> 

### <a name="job-summary"></a>Сводные данные задания
Можно просмотреть список всех заданий hello, которые были созданы для конкретного модуля runbook и их самое последнее состояние. Этот список можно фильтровать по состоянию заданий и hello диапазон дат для hello последнее изменение toohello задания. tooview его подробные сведения и выходных данных, щелкните имя hello задания. Hello подробном представлении задания hello указаны hello значения для параметров runbook hello, которые были указаны toothat задания.

Можно использовать следующие шаги tooview hello задания для модуля runbook hello.

1. В hello портал Azure, выберите **автоматизации** и выберите имя учетной записи автоматизации hello.
2. Концентратор приветствия выберите **Runbooks** и затем на hello **модулей Runbook** колонке выберите книгу из списка hello.
3. В колонке hello для hello выбранного модуля runbook, щелкните hello **заданий** плитки.
4. Выберите одну из заданий hello в списке hello и колонки сведений задания hello runbook можно просмотреть сведения о нем и выходных данных.

## <a name="retrieving-job-status-using-windows-powershell"></a>Получение состояния задания с помощью Windows PowerShell
Можно использовать hello [Get AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) tooretrieve hello заданий, созданных runbook и hello сведений о конкретном задании. При запуске модуля runbook с помощью Windows PowerShell [AzureRmAutomationRunbook начала](https://msdn.microsoft.com/library/mt603661.aspx), то возвращается hello результирующее задание. Используйте [Get AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx)tooget вывода выходных данных задания.

Hello ниже примеры команд извлечения hello последнего задания для runbook и отображает его состояние, значения hello, предоставленный для параметров runbook hello и выходные данные задания hello hello.

    $job = (Get-AzureRmAutomationJob –AutomationAccountName "MyAutomationAccount" `
    –RunbookName "Test-Runbook" -ResourceGroupName "ResourceGroup01" | sort LastModifiedDate –desc)[0]
    $job.Status
    $job.JobParameters
    Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAcct" -Id $job.JobId –Stream Output

## <a name="fair-share"></a>доли
В порядке tooshare ресурсов среди всех модулей Runbook в облаке hello службы автоматизации Azure будет временно выгружать любое задание после его выполнения в течение трех часов.  В течение этого времени задания для [модулей Runbook на основе PowerShell](automation-runbook-types.md#powershell-runbooks) останавливаются и не будут перезапускаться.  Показывает состояние задания Hello **остановлена**.  Этот тип runbook всегда перезапускается с начала hello, так как они не поддерживают контрольные точки.  

[Модули Runbook на основе рабочего процесса PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) будут возобновлены из последней [контрольной точки](https://docs.microsoft.com/system-center/sma/overview-powershell-workflows#bk_Checkpoints).  После выполнения три часа, будет приостановить задание runbook hello службой и его состояние hello показывает **выполняется; ожидание ресурсов**.  Если "песочницу" станет доступной, hello runbook будет перезапущена автоматически службой автоматизации hello и выхода из последней контрольной точки hello.  Это нормальное поведение рабочего процесса PowerShell для приостановки или перезапуска.  Если hello runbook еще раз превышает три часа среды выполнения, hello процесс повторяется, toothree времени.  После третьего перезапуска hello, если по-прежнему hello runbook не завершена в течение трех часов, то не удалось выполнить задание runbook hello и показывает состояние задания hello **завершилось сбоем; Ожидание ресурсов**.  В этом случае появляется после исключения с ошибкой hello hello.

*Задание Hello не может продолжать выполнение, так как оно постоянно исключалось с hello же контрольной точки. Убедитесь, что модуль Runbook не выполняет продолжительные операции без сохранения состояния.*

Это служба hello tooprotect запуск модулей Runbook бесконечно без завершения, как они не могут toomake его toohello следующей контрольной точки без повторной выгрузки.

Если hello runbook имеет нет контрольных точек или задание hello не достигло первой контрольной точки hello до выгрузки, он перезапустит с начала hello.  

При создании модуля runbook следует убедиться, toorun время hello, любые действия между двумя контрольными точками не превышает 3 часа. Может потребоваться tooyour runbook контрольные точки tooadd tooensure, что она не достигнут этот предел три часа или разбить долго выполняющиеся операции. Например, модуль Runbook может выполнять повторную индексацию в крупной базе данных SQL. Если эта операция не завершается в течение hello удовлетворительные предел общего ресурса, а затем задание hello выгружен и перезапущен с начала hello. В этом случае необходимо разбить hello операцию на несколько этапов, например, повторное индексирование одной таблицы одновременно и затем вставить контрольную точку после каждой операции для hello задание возобновления после последней операции toocomplete hello.

## <a name="next-steps"></a>Дальнейшие действия
* toolearn Дополнительные сведения о hello различные методы, которые можно использовать toostart runbook в автоматизации Azure в разделе [запуск runbook в автоматизации Azure](automation-starting-a-runbook.md)

