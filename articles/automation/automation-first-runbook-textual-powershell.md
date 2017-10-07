---
title: "aaaMy первый runbook PowerShell в службе автоматизации Azure | Документы Microsoft"
description: "Учебник, в котором описывается создание hello, тестированию и публикации из простого модуля runbook PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "Azure PowerShell, руководство по скриптам PowerShell, инструменты автоматизации PowerShell"
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/26/2017
ms.author: magoedte;sngun
ms.openlocfilehash: abff94abe666cd8423c35b970b4162ba9247bcf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-powershell-runbook"></a>Мой первый модуль Runbook PowerShell

> [!div class="op_single_selector"]
> * [Графический](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [Рабочий процесс PowerShell](automation-first-runbook-textual.md)
> 
> 

Этот учебник поможет выполнить создание hello [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) в службе автоматизации Azure. Мы начнем с простого модуля runbook, мы протестировать и опубликовать, пока мы объясним, как tootrack hello состояния задания runbook hello. Затем мы измените hello runbook tooactually управления ресурсами Azure, в этом случае запуск виртуальной машины Azure. Наконец мы предоставим hello runbook более надежными, добавив параметры модуля runbook.

## <a name="prerequisites"></a>Предварительные требования
toocomplete этого учебника требуется hello следующие:

* Подписка Azure. Если у вас ее нет, [активируйте преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или <a href="/pricing/free-account/" target="_blank">[зарегистрируйте бесплатную учетную запись](https://azure.microsoft.com/free/).
* [Учетная запись службы автоматизации](automation-sec-configure-azure-runas-account.md) toohold hello runbook и проверить подлинность tooAzure ресурсов.  Этой учетной записи необходимо разрешение toostart и остановить виртуальную машину hello.
* Виртуальная машина Azure. Это не должна быть рабочая виртуальная машина, так как в процессе изучения этого руководства ее нужно будет остановить и запустить заново.

## <a name="step-1---create-new-runbook"></a>Шаг 1. Создание нового модуля Runbook
Мы начнем с создания простого модуля runbook, который выводит текст hello *Hello World*.

1. Откройте в hello портал Azure, ваша учетная запись автоматизации.  
   страница учетной записи автоматизации Hello предоставляет быстрый просмотр hello ресурсов в этой учетной записи. Некоторые ресурсы уже должны быть доступны. Большинство из них являются hello модули, которые автоматически включаются в новую учетную запись автоматизации. Вы также должны hello ресурс учетных данных, которая упоминается в hello [необходимых компонентов](#prerequisites).
2. Нажмите кнопку hello **Runbooks** плитки tooopen hello список модулей Runbook.<br><br> ![Управление модулями Runbook](media/automation-first-runbook-textual-powershell/runbooks-control-tiles.png)  
3. Создать новый runbook, щелкнув hello **добавить модуль runbook** кнопки и затем **создать новый runbook**.
4. Присвойте имя hello hello runbook *MyFirstRunbook PowerShell*.
5. В этом случае мы будем toocreate [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) поэтому выберите **Powershell** для **тип Runbook**.<br><br> ![Runbook Type](media/automation-first-runbook-textual-powershell/automation-runbook-type.png)  
6. Нажмите кнопку **создать** toocreate hello runbook и откройте hello текстового редактора.

## <a name="step-2---add-code-toohello-runbook"></a>Шаг 2 — Добавление кода toohello runbook
Можно любой тип кода непосредственно в hello runbook, или можно выбрать из hello элемент управления из библиотеки командлетов, модули Runbook и ресурсов и их добавления runbook toohello связанные параметры. В данном пошаговом руководстве мы ввести непосредственно в hello runbook.

1. Сейчас модуль Runbook пуст, поэтому введите *Write-Output "Hello World."*.<br><br> ![Привет, мир!](media/automation-first-runbook-textual-powershell/automation-helloworld.png)  
2. Сохранить hello runbook, установив **Сохранить**.<br><br> ![Кнопка "Сохранить"](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-save.png)  

## <a name="step-3---test-hello-runbook"></a>Шаг 3. при проверке runbook hello
Прежде чем мы опубликовать hello runbook toomake он доступен в рабочей среде, нам нужно tootest его toomake убедиться, что он работает правильно. Чтобы протестировать модуль Runbook, нужно запустить его **черновую** версию и проверить его работу в интерактивном режиме.

1. Нажмите кнопку **области тестов** tooopen hello тестовой области.<br><br> ![Test Pane](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-test.png)  
2. Нажмите кнопку **запустить** toostart hello теста. Это должно быть включено только hello вариантом.
3. При этом создается [задание Runbook](automation-runbook-execution.md) и отображается его состояние.  
   состояние задания Hello для запуска в качестве *в очереди* означает, что он ожидает runbook worker в доступных toocome облака hello. Он будет двигаться слишком*запуск* когда исполнитель задания hello, а затем *под управлением* при hello runbook фактически начинает выполнение.  
4. По завершении заданий runbook hello его вывода. В нашем случае это должен быть текст *Привет, мир!*.<br><br> ![Вывод области тестирования](media/automation-first-runbook-textual-powershell/automation-testpane-output.png)  
5. Закройте hello тестирования области tooreturn toohello холста.

## <a name="step-4---publish-and-start-hello-runbook"></a>Шаг 4. Публикация и запуск модуля runbook hello
runbook Hello, созданную по-прежнему черновом режиме. Мы должны toopublish перед его можно было запустить в рабочей среде.  При публикации модуля runbook, можно заменить hello существующей опубликованной версии hello черновую версию.  В нашем случае мы опубликованную версию еще нет, потому что мы только что создали hello runbook.

1. Нажмите кнопку **публикации** toopublish hello runbook и затем **Да** при появлении запроса.<br><br> ![Кнопка "Опубликовать"](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-publish.png)  
2. При прокрутке левой tooview runbook hello в hello **Runbooks** области, он будет отображаться **состояние создания** из **опубликовано**.
3. Панель hello правой tooview задней toohello прокрутки для **MyFirstRunbook PowerShell**.  
   Hello параметры сверху hello позволит нам toostart hello runbook, просмотра hello runbook, запланировать toostart в некоторый момент в будущем hello или создания [веб-перехватчика](automation-webhooks.md) , оно может начаться через вызов HTTP.
4. Мы должны toostart hello runbook, нажмите **запустить** и нажмите кнопку **ОК** при открытии колонке hello запустить Runbook.<br><br> ![Кнопка "Запуск"](media/automation-first-runbook-textual-powershell/automation-runbook-controls-start.png)<br>    
5. Открывается область задание для hello задание runbook, который мы создали. В этой области можно закрыть, но в этом случае мы оставить его открытым, поэтому мы можно отслеживать ход выполнения задания hello.
6. отображается состояние заданий Hello в **Сводка заданий** и совпадений hello состояния, мы видели, когда мы протестировали hello runbook.<br><br> ![Сводные данные задания](media/automation-first-runbook-textual-powershell/job-pane-status-blade-jobsummary.png)<br>  
7. Один раз hello показано состояние runbook *завершено*, нажмите кнопку **вывода**. открыть область вывода Hello, и мы видим нашей *Hello World*.<br><br> ![Выходные данные задания](media/automation-first-runbook-textual-powershell/job-pane-status-blade-outputtile.png)<br> 
8. Закрыть hello области вывода.
9. Нажмите кнопку **все журналы** tooopen hello потоки области для задания runbook hello. Мы должны видеть только *Hello World* в выходных данных hello потока, но это может показывать другие потоки для задания runbook, например Verbose и ошибка записывает toothem hello runbook.<br><br> ![Все журналы](media/automation-first-runbook-textual-powershell/job-pane-status-blade-alllogstile.png)<br>   
10. Закройте hello потоки области и hello задания области tooreturn toohello MyFirstRunbook PowerShell.
11. Нажмите кнопку **заданий** tooopen hello задания области для этого модуля runbook. Перечисляет все задания hello, созданные этим модулем runbook. Мы должны видеть только одно задание, так как мы только запуска задания hello один раз в списке.<br><br> ![Список заданий](media/automation-first-runbook-textual-powershell/runbook-control-job-tile.png)  
12. Можно щелкнуть это задание tooopen hello одной области задания, которые мы просматривать, когда мы начали hello runbook. Это позволяет toogo обратно в времени и просмотреть подробные сведения hello любого задания, который был создан для конкретного модуля runbook.

## <a name="step-5---add-authentication-toomanage-azure-resources"></a>Шаг 5 — Добавление toomanage проверки подлинности ресурсов Azure
Мы протестировали и опубликовали свой модуль Runbook, но пока он не выполняет никаких полезных действий. Мы хотим toohave его управления ресурсами Azure. Он не будет возможности toodo на то, что если у нас нет проверки подлинности с использованием учетных данных hello, называется tooin hello [необходимых компонентов](#prerequisites). Что мы делаем с hello **AzureRmAccount добавить** командлета.

1. Откройте hello текстового редактора, щелкнув **изменить** на панели hello MyFirstRunbook PowerShell.<br><br> ![Изменение модуля Runbook](media/automation-first-runbook-textual-powershell/automation-runbook-controls-edit.png)<br>   
2. Нам не нужен hello **Write-Output** строки больше, поэтому действуйте и удалите его.
3. Введите или скопируйте и вставьте следующий код, который обрабатывает hello проверку подлинности с помощью учетной записи запуска от автоматизации hello:
   
   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   ```
   <br>
4. Нажмите кнопку **области тестов** , чтобы мы смогли проверить hello runbook.
5. Нажмите кнопку **запустить** toostart hello теста. После ее завершения, должно появиться примерно toohello выходных данных после, отображение основных сведений из вашей учетной записи. Это подтверждает, что эти учетные данные hello является допустимым.<br><br> ![Проверка подлинности](media/automation-first-runbook-textual-powershell/runbook-auth-output.png)

## <a name="step-6---add-code-toostart-a-virtual-machine"></a>Шаг 6 — Добавление кода toostart виртуальной машины
Теперь, когда наши runbook проверяет подлинность tooour подписки Azure, мы управление ресурсами. Мы добавляем команда toostart виртуальной машины. Можно выбрать любой виртуальной машине в вашей подписке Azure, и сейчас мы будут жестко это имя в hello runbook.

1. После *AzureRmAccount добавить*, тип *Start AzureRmVM-имя «VMName» - ResourceGroupName «NameofResourceGroup»* указания имени hello и имя группы ресурсов toostart hello виртуальной машины.  
   
   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name 'VMName' -ResourceGroupName 'ResourceGroupName'
   ```
   <br>
2. Сохранить hello runbook и нажмите кнопку **области тестов** , чтобы мы смогли проверить его.
3. Нажмите кнопку **запустить** toostart hello теста. После ее завершения, убедитесь, что виртуальная машина, hello была запущена.

## <a name="step-7---add-an-input-parameter-toohello-runbook"></a>Шаг 7 - добавьте входной параметр toohello runbook
В настоящее время наши runbook запускает hello виртуальной машины, что мы жестко задано в hello runbook, но было бы более полезным, если при запуске hello runbook указывается hello виртуальной машины. Теперь добавим tooprovide runbook toohello входных параметров эта функция.

1. Добавление параметров для *VMName* и *ResourceGroupName* toohello runbook и использовать эти переменные с hello **AzureRmVM начала** командлет, как показано в приведенном ниже примере hello.  
   
   ```
   Param(
    [string]$VMName,
    [string]$ResourceGroupName
   )
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name $VMName -ResourceGroupName $ResourceGroupName
   ```
   <br>
2. Сохраните hello runbook и откройте панель тестовых hello. Вам могут предоставлять значения для hello две входные переменные, используемые в тесте hello.
3. Закрыть hello тестовой области.
4. Нажмите кнопку **публикации** toopublish hello hello runbook в новой версии.
5. Остановите hello виртуальную машину, которая запущена на предыдущем шаге hello.
6. Нажмите кнопку **запустить** toostart hello runbook. Тип в hello **VMName** и **ResourceGroupName** для виртуальной машины hello ты toostart.<br><br> ![Передача параметра](media/automation-first-runbook-textual-powershell/automation-pass-params.png)<br>  
7. После завершения hello runbook, убедитесь, что виртуальная машина, hello была запущена.

## <a name="differences-from-powershell-workflow"></a>Отличия от рабочего процесса PowerShell
Модули Runbook PowerShell имеют hello же жизненного цикла, возможности и управление как модули PowerShell рабочего процесса, но существуют некоторые отличия и ограничения:

1. PowerShell выполняются быстро сравниваемых tooPowerShell модулях Runbook рабочего процесса, они не имеют шага компиляции.
2. Модули Runbook рабочий процесс PowerShell поддерживает контрольные точки, с помощью контрольных точек, можно возобновить рабочий процесс PowerShell модули Runbook из любой точки в hello runbook в то время как модули Runbook PowerShell может возобновлять только с начала hello.
3. Модули Runbook PowerShell поддерживают параллельное и последовательное выполнение, тогда как модули Runbook рабочих процессов PowerShell могут выполнять команды только последовательно.
4. В модуле runbook рабочего процесса PowerShell действие, команда или блок скрипта могут иметь свои собственные пространства выполнения, тогда как в модуле runbook PowerShell все содержимое скрипта выполняется в одном пространстве выполнения. Кроме того, существуют некоторые [синтаксические различия](https://technet.microsoft.com/magazine/dn151046.aspx) между собственным модулем Runbook PowerShell и модулем Runbook рабочих процессов PowerShell.

## <a name="next-steps"></a>Дальнейшие действия
* tooget к работе с графический Runbook в разделе [Мой первый графический runbook](automation-first-runbook-graphical.md)
* tooget к работе с PowerShell модули Runbook рабочего процесса, в разделе [Мой первый runbook рабочего процесса PowerShell](automation-first-runbook-textual.md)
* в разделе tooknow Дополнительные сведения о типах runbook, их преимущества и ограничения, [типов runbook службы автоматизации Azure](automation-runbook-types.md)
* Дополнительные сведения о функции поддержки скриптов PowerShell см. в статье [Announcing Native PowerShell Script Support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/) (Встроенная поддержка скриптов PowerShell в службе автоматизации Azure).

