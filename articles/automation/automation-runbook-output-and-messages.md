---
title: "aaaRunbook выходные данные и сообщения в службе автоматизации Azure | Документы Microsoft"
description: "Описывает подготовку способ toocreate и извлечь выход и ошибки сообщений из модулей Runbook в автоматизации Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 13a414f5-0e2c-4be2-9558-a3e3ec84b6b2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: magoedte;bwren
ms.openlocfilehash: c1505fa889473766bfa47e43aaed2449d60ad851
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-output-and-messages-in-azure-automation"></a>Выходные данные и сообщения Runbook в службе автоматизации Azure
В большинстве модулей Runbook службы автоматизации Azure будут иметь определенный формат выходных данных, например ошибка сообщения toohello пользователя или сложный объект, предназначенный toobe использования другим рабочим процессом. Windows PowerShell предоставляет [несколько потоков](http://blogs.technet.com/heyscriptingguy/archive/2014/03/30/understanding-streams-redirection-and-write-host-in-powershell.aspx) toosend выходные данные сценария или рабочего процесса. Автоматизации Azure работает с каждым из этих потоков по-разному, и необходимо следовать индивидуальным рекомендациям toouse каждого при создании модуля runbook.

Hello ниже приводится краткое описание каждого из потоков hello и их поведение в hello портала управления Azure при выполнении опубликованного модуля runbook и последующем [тестировании модуля runbook](automation-testing-runbook.md). В последующих разделах приведены дополнительные сведения о каждом потоке.

| Поток | Описание | Опубликовано | Тест |
|:--- |:--- |:--- |:--- |
| Выходные данные |Объекты, предназначенные toobe использования другими модулями Runbook. |Записать журнал заданий toohello. |Отображается в тестовой области вывода hello. |
| Предупреждение |Предупреждения, предназначенные для пользователя hello. |Записать журнал заданий toohello. |Отображается в тестовой области вывода hello. |
| Ошибка |Сообщение об ошибке, предназначенные для пользователя hello. В отличие от возникновения исключения hello модуль runbook продолжает работу после сообщения об ошибке по умолчанию. |Записать журнал заданий toohello. |Отображается в тестовой области вывода hello. |
| Подробная информация |Сообщения, содержащие общую или отладочную информацию. |Запись журнала toojob только если подробное ведение журнала включено для hello runbook. |Только в том случае, если $VerbosePreference задано tooContinue hello runbook отображается в области вывода теста hello. |
| Ход выполнения |Записи, автоматически созданные до и после каждого действия в hello runbook. Hello runbook не должны предпринимать попытки toocreate свои собственные записи о ходе выполнения, поскольку они предназначены для интерактивного пользователя. |Запись журнала toojob только если выполняется ведение журнала включено для hello runbook. |Не отображается в тестовой области вывода hello. |
| Отладка |Сообщения, предназначенные для интерактивного пользователя. Не следует использовать в Runbook. |Не записывается журнал toojob. |Не записывается tooTest области вывода. |

## <a name="output-stream"></a>Поток вывода
Hello выходной поток предназначен для вывода объектов, созданных скриптом или рабочим процессом, когда он работает правильно. В службе автоматизации Azure этот поток в основном используется для объектов, предназначенных toobe занятая [родительских модулей Runbook, которые вызывают текущий модуль runbook hello](automation-child-runbooks.md). Когда вы [вызова встроенной функции модуля runbook](automation-child-runbooks.md#invoking-a-child-runbook-using-inline-execution) из родительского модуля, возвращаются данные из родительского toohello потока вывода hello. Назад toohello hello выходной поток toocommunicate Общие сведения пользователя следует использовать только в том случае, если известно, что hello runbook не будет вызван другим модулем runbook. Рекомендуется, однако обычно следует использовать hello [Verbose Stream](#Verbose) пользователя toohello toocommunicate Общие сведения.

Можно написать данных toohello выходного потока с помощью [Write-Output](http://technet.microsoft.com/library/hh849921.aspx) или путем помещения hello объекта в собственную строку в hello runbook.

    #hello following lines both write an object toohello output stream.
    Write-Output –InputObject $object
    $object

### <a name="output-from-a-function"></a>Выходные данные функции
При написании toohello выходной поток в функцию, которая включается в модуле runbook hello выходные данные передаются назад toohello runbook. Если hello runbook присваивает этой переменной tooa выходные данные, они не записываются toohello выходной поток. Написание tooany другие потоки в функции hello напишете toohello соответствующий поток для hello runbook.

Рассмотрим следующий пример модуля runbook hello.

    Workflow Test-Runbook
    {
        Write-Verbose "Verbose outside of function" -Verbose
        Write-Output "Output outside of function"
        $functionOutput = Test-Function
        $functionOutput

    Function Test-Function
     {
        Write-Verbose "Verbose inside of function" -Verbose
        Write-Output "Output inside of function"
      }
    }


Hello выходной поток для hello задания runbook будет следующим:

    Output inside of function
    Output outside of function

поток вывода Hello hello задания runbook будет:

    Verbose outside of function
    Verbose inside of function

После публикации hello runbook и до его начала, необходимо также включить подробное ведение журнала, в параметрах runbook hello в порядке tooget hello выходной поток подробных сведений.

### <a name="declaring-output-data-type"></a>Объявление типа выходных данных
Рабочий процесс можно указать тип данных hello его выходные данные с помощью hello [атрибута OutputType](http://technet.microsoft.com/library/hh847785.aspx). Этот атрибут не оказывает влияния во время выполнения, но он предоставляет автору runbook toohello указание во время разработки выходные данные hello ожидается hello runbook. По мере tooevolve hello набор инструментов для модулей Runbook важность объявления типов выходных данных во время разработки hello увеличит по важности. В результате это рекомендациям tooinclude это объявление во все модули Runbook, который вы создаете.

Вот список с примерами типов выходных данных:

* System.String
* System.Int32
* System.Collections.Hashtable
* Microsoft.Azure.Commands.Compute.Models.PSVirtualMachine

Hello следующий пример модуля runbook выводит объект string и включает объявление выходного типа. Если модуль runbook выводит массив определенного типа, необходимо по-прежнему указать тип hello как противоположность tooan массив типа hello.

    Workflow Test-Runbook
    {
       [OutputType([string])]

       $output = "This is some string output."
       Write-Output $output
    }

toodeclare вывод типа в модулях Runbook Grapical или графического рабочего процесса PowerShell, можно выбрать hello **входной и выходной** пункт меню и введите имя hello hello тип выходного файла.  Мы рекомендуем использовать hello полный .NET класс имя toomake его понятными, при ссылке на нее из родительского модуля.  Это предоставляет все свойства этого класса шины данных toohello в hello runbook hello и обеспечивает большую гибкость при их использовании для условную логику, ведение журнала, а также привязку как значения для других действий в hello runbook.<br> ![Runbook: раздел "Входные и выходные данные"](media/automation-runbook-output-and-messages/runbook-menu-input-and-output-option.png)

В следующем примере hello у нас есть два графических модулей Runbook toodemonstrate эту функцию.  Если применить hello модульной runbook проектирования модели, у нас есть один runbook, который служит в качестве hello *шаблона Runbook проверки подлинности* управление проверкой подлинности с помощью Azure hello Запуск от имени учетной записи.  Наш второй runbook, который, как правило, выполняет hello основной логики tooautomate данного сценария, в этом случае происходит tooexecute hello *шаблона Runbook проверки подлинности* и отображения результатов tooyour hello **теста** области вывода.  В обычных условиях мы бы этот каким-либо от ресурса путем использования hello выходные данные из hello дочернего модуля runbook.    

Вот основные логику hello hello **AuthenticateTo Azure** runbook.<br> ![Runbook: пример шаблона аутентификации](media/automation-runbook-output-and-messages/runbook-authentication-template.png).  

Он включает тип выходных данных hello *Microsoft.Azure.Commands.Profile.Models.PSAzureContext*, возвращающий hello свойства профиля проверки подлинности.<br> ![Runbook: пример типа выходных данных](media/automation-runbook-output-and-messages/runbook-input-and-output-add-blade.png) 

Хотя этот runbook очень прост, имеется один toocall элемента конфигурации out здесь.  последнее действие Hello выполняется hello **Write-Output** командлета и записи hello профиль tooa $_ переменной с помощью выражения PowerShell для hello **Inputobject** параметр, который требуется для этого командлет.  

Для второго модуля hello в этом примере, с именем *ChildOutputType тест*, мы просто иметь два действия.<br> ![Runbook: пример типа выходных данных дочернего модуля](media/automation-runbook-output-and-messages/runbook-display-authentication-results-example.png) 

Первое действие Hello вызывает hello **AuthenticateTo Azure** runbook и hello второго действия выполняется hello **Write-Verbose** командлет с hello **источника данных** из  **Выходные данные действия** , а значение hello **путь к полю** — **Context.Subscription.SubscriptionName**, которой указание hello контекста вывод hello  **AuthenticateTo Azure** runbook.<br> ![Командлет Write-Verbose: источник данных параметров](media/automation-runbook-output-and-messages/runbook-write-verbose-parameters-config.png)    

Hello результат — имя hello hello подписки.<br> ![Runbook: результаты командлета Test-ChildOutputType](media/automation-runbook-output-and-messages/runbook-test-childoutputtype-results.png)

Одно примечание о hello поведение hello тип выходных данных элемента управления.  Ввести значение в поле Тип выходных данных hello на hello входных данных и выходного свойства колонке после tooclick за пределами элемента управления hello после ввода, чтобы ваш toobe входа распознается элементом управления hello.  

## <a name="message-streams"></a>Потоки сообщений
В отличие от потока вывода hello потоки сообщений являются предполагаемого toocommunicate информации toohello пользователя. Существует несколько потоков сообщений для различных типов информации, и каждый по-разному обрабатываются службой автоматизации Azure.

### <a name="warning-and-error-streams"></a>Потоки предупреждений и ошибок
потоки предупреждений и ошибок Hello являются предполагаемого toolog проблем, возникающих в модуле runbook. Они записываются toohello журнал заданий при выполнении runbook и включаются в hello тестовой области вывода в hello портала управления Azure при тестировании модуля runbook. По умолчанию hello runbook продолжит выполнение после предупреждения или ошибки. Можно указать, hello runbook следует приостановить при возникновении предупреждения или ошибки, задав [привилегированной переменной](#PreferenceVariables) в hello runbook перед созданием приветственное сообщение. Например, toocause toosuspend runbook при возникновении ошибки как исключения, задайте **$ErrorActionPreference** tooStop.

Создать предупреждение или сообщение об ошибке с помощью hello [Write-Warning](https://technet.microsoft.com/library/hh849931.aspx) или [Write-Error](http://technet.microsoft.com/library/hh849962.aspx) командлета. Действия также могут записывать toothese потоков.

    #hello following lines create a warning message and then an error message that will suspend hello runbook.

    $ErrorActionPreference = "Stop"
    Write-Warning –Message "This is a warning message."
    Write-Error –Message "This is an error message that will stop hello runbook because of hello preference variable."

### <a name="verbose-stream"></a>Подробный поток
поток подробных сообщений Hello — Общие сведения о задаче hello. С момента hello [поток отладки](#Debug) недоступна в модуле runbook, подробные сообщения следует использовать для отладочной информации. По умолчанию подробные сообщения из опубликованных модулей Runbook не сохраняются в журнале заданий hello. toostore подробные сообщения, настройте опубликованные модули Runbook tooLog подробные записи на вкладке Настройка hello runbook hello в hello портала управления Azure. В большинстве случаев следует сохранить значение по умолчанию hello не вести журнал подробных сведений для модуля runbook для повышения производительности. Включите этот параметр только tootroubleshoot или отладки модуля runbook.

Когда [тестировании модуля runbook](automation-testing-runbook.md), подробные сообщения не отображаются, даже если hello runbook настроенных toolog подробные записи. toodisplay подробные сообщения при [тестировании модуля runbook](automation-testing-runbook.md), необходимо задать tooContinue переменной hello $VerbosePreference. Эта переменная задана подробные сообщения будут отображаться в тестовой области вывода портала Azure hello hello.

Создайте подробное сообщение с помощью hello [Write-Verbose](http://technet.microsoft.com/library/hh849951.aspx) командлета.

    #hello following line creates a verbose message.

    Write-Verbose –Message "This is a verbose message."

### <a name="debug-stream"></a>Поток отладки
Hello Отладка потока предназначена для использования текущим пользователем и не должны использоваться в модулях Runbook.

## <a name="progress-records"></a>Записи о ходе выполнения
Если задан элемент ход выполнения runbook toolog регистрирует (на вкладке Настройка hello runbook hello в hello портал Azure), а затем сообщение будет записано toohello журнал заданий до и после выполнения каждого действия. В большинстве случаев следует сохранить значение по умолчанию hello не вести журнал хода выполнения для модуля runbook в порядке toomaximize производительности. Включите этот параметр только tootroubleshoot или отладки модуля runbook. При тестировании модуля runbook сообщения о ходе выполнения не отображаются, даже если hello runbook настроенных toolog записи о ходе выполнения.

Hello [Write-Progress](http://technet.microsoft.com/library/hh849902.aspx) недопустим в модуле runbook, поскольку он предназначен для использования с текущим пользователем.

## <a name="preference-variables"></a>Привилегированные переменные
Windows PowerShell использует [привилегированные переменные](http://technet.microsoft.com/library/hh847796.aspx) toodetermine как toodifferent toodata отправлено toorespond потока вывода. Эти переменные можно задать в toocontrol runbook, реакцией toodata, отправленные в разные потоки.

Hello следующей таблице перечислены hello привилегированные переменные, которые можно использовать в Runbook с их допустимыми и значения по умолчанию. Обратите внимание, что эта таблица содержит только hello значений, которые являются допустимыми в модуле runbook. Дополнительные значения допустимы для hello привилегированных переменных при использовании в Windows PowerShell за пределами Azure Automation.

| Переменная | Значение по умолчанию | Допустимые значения |
|:--- |:--- |:--- |
| WarningPreference |Continue |Stop<br>Continue<br>SilentlyContinue |
| ErrorActionPreference |Continue |Stop<br>Continue<br>SilentlyContinue |
| VerbosePreference |SilentlyContinue |Stop<br>Continue<br>SilentlyContinue |

Привет, в следующей таблице перечислены hello поведение для hello предпочтений значения переменных, которые являются допустимыми в модулях Runbook.

| Значение | Поведение |
|:--- |:--- |
| Continue |Записывает в журнал сообщение hello и продолжает выполнение hello runbook. |
| SilentlyContinue |Продолжает выполнение hello runbook без ведения журнала сообщений hello. Это приводит hello сообщение hello игнорируется. |
| Остановить |Записывает приветственное сообщение и приостанавливает модуль runbook hello. |

## <a name="retrieving-runbook-output-and-messages"></a>Извлечение выходных данных и сообщений Runbook
### <a name="azure-portal"></a>Портал Azure
Для просмотра сведений hello задания runbook в hello портал Azure hello вкладки заданий runbook. Отображает Hello Сводка hello задания входных параметров hello и hello [выходной поток](#Output) в toogeneral сведения о задании hello и любые исключения, если они. Hello журнал будет содержать сообщения из hello [выходной поток](#Output) и [потоки предупреждений и ошибок](#WarningError) в дополнение toohello [Verbose Stream](#Verbose) и [хода выполнения Записи](#Progress) Если hello runbook настроенных toolog verbose и записи о ходе выполнения.

### <a name="windows-powershell"></a>Windows PowerShell
В Windows PowerShell можно получить выходные данные и сообщения из модуля runbook с помощью hello [Get-AzureAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) командлета. Для этого командлета требуется идентификатор задания hello Здравствуйте, и имеет параметр потока, где указать, какой поток tooreturn. Можно указать любой tooreturn все потоки задания hello.

Следующий пример Hello запускается пример модуля runbook, а затем ожидает ее toocomplete. После завершения поток вывода собирается из задания hello.

    $job = Start-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook"

    $doLoop = $true
    While ($doLoop) {
       $job = Get-AzureRmAutomationJob -ResourceGroupName "ResourceGroup01" `
       –AutomationAccountName "MyAutomationAccount" -Id $job.JobId
       $status = $job.Status
       $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped")
    }

    Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" -Id $job.JobId –Stream Output

### <a name="graphical-authoring"></a>Графическая разработка
Для графических модулей Runbook дополнительное ведение журнала доступно в форме hello трассировки уровня активности.  Существует два уровня трассировки: базовая и подробная.  В базовый уровень, можно увидеть hello запуска и время окончания каждого действия в hello runbook, а также сведения, связанные с повторными попытками действия tooany, такие как число попыток и время начала действия hello.  Подробная трассировка включает те же данные, что и базовая, плюс входные и выходные данные каждого действия.  Обратите внимание, что в данный момент записи трассировки hello записываются с помощью hello поток вывода, поэтому необходимо включить подробное ведение журнала при включении трассировки.  Для графических модулей Runbook с включенной трассировкой нет необходимости toolog записи о ходе выполнения, так как базовый уровень служит hello hello той же цели и более подробное сообщение.

![Представление потоков заданий графической разработки](media/automation-runbook-output-and-messages/job-streams-view-blade.png)

Вы увидите из hello выше снимке экрана, при включении Verbose ведения журнала и трассировки для графических модулей Runbook больше информации, был доступен в производственные hello просматривать потоки задания.  Эти дополнительные сведения могут пригодиться во время поиска и устранения неисправностей, связанных с модулем Runbook. Включайте их только для этой цели, в обычном режиме подобная детализация не требуется.    
Hello записи трассировки может быть особенно многочисленные.  С использованием графического модуля runbook вы трассировки для получения двух записей toofour в действие в зависимости от настройки трассировки обычный или подробный.  Если не требуется этот сведения tootrack hello ход выполнения runbook. для устранения неполадок может потребоваться tookeep трассировка отключена.

**tooenable уровня активности трассировки, выполните hello следующие шаги.**

1. Откройте в hello портал Azure, ваша учетная запись автоматизации.
2. Щелкните hello **Runbooks** плитки tooopen hello список модулей Runbook.
3. В колонке hello модулей Runbook щелкните tooselect графический runbook из списка модулей Runbook.
4. В колонке параметров hello для hello выбранного модуля runbook, нажмите кнопку **ведения журнала и трассировки**.
5. Hello ведения журнала и трассировки колонке под подробные записи в журнале, щелкните **на** tooenable подробное ведение журнала и трассировки udner уровне активности, изменить уровень трассировки hello слишком**основные** или **Detailed**  в зависимости от уровня hello требуется трассировки.<br>
   
   ![Колонка ведения журналов и трассировки графической разработки](media/automation-runbook-output-and-messages/logging-and-tracing-settings-blade.png)

### <a name="microsoft-operations-management-suite-oms-log-analytics"></a>Log Analytics в Microsoft Operations Management Suite (OMS)
Автоматизация может отправлять runbook задания состояние задания потоки tooyour анализа журналов Microsoft Operations Management Suite (OMS) рабочей области и.  С помощью Log Analytics можно:

* получить информацию о заданиях службы автоматизации; 
* активировать отправку электронного сообщения или оповещения в соответствии с состоянием задания Runbook (например, сбой или приостановка); 
* создавать сложные запросы для потоков заданий; 
* коррелировать задания и учетные записи службы автоматизации; 
* визуализировать журнал задания по прошествии времени.    

Дополнительные сведения о корреляции и реагировать на данные задания tooconfigure интеграция с toocollect анализа журналов см. в разделе [вперед от tooLog автоматизации Analytics (OMS) состояние задания и задания потоки](automation-manage-send-joblogs-log-analytics.md).

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о выполнение модуля runbook, как toomonitor заданиях и другие технические сведения см. в разделе toolearn [отследить задание runbook](automation-runbook-execution.md)
* toounderstand toodesign и использование дочерние модули. в статье [дочерние модули Runbook в автоматизации Azure](automation-child-runbooks.md)

