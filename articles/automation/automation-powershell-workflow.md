---
title: "aaaLearning рабочий процесс PowerShell для автоматизации Azure | Документы Microsoft"
description: "Эта статья предназначена как краткий обзор для разработчиков знакомы с PowerShell toounderstand hello конкретные различия в PowerShell и рабочий процесс PowerShell и модулей Runbook применимо tooAutomation основные понятия."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 84bf133e-5343-4e0e-8d6c-bb14304a70db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 362c504eb96d31b99a826b128e6a591beecaa084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a>Изучение основных понятий рабочего процесса Windows PowerShell для модулей Runbook службы автоматизации 
Модули Runbook в службе автоматизации Azure реализованы в виде рабочих процессов Windows PowerShell.  Рабочий процесс Windows PowerShell является аналогичный сценарий Windows PowerShell tooa, но имеет ряд существенных отличий, которые могут быть сложными tooa нового пользователя.  В данной статье предполагаемого toohelp записи модулей Runbook с помощью рабочего процесса PowerShell, мы рекомендуем запись модулей Runbook с помощью PowerShell, если не требуется контрольные точки.  Существует несколько различий синтаксис при создании и настройке модулей Runbook рабочего процесса PowerShell, и эти различия требуют немного больше рабочих процессов действующие toowrite.  

Рабочий процесс — это последовательность связанных операций программируемых, в которых выполняются длительные задачи или требуют координации нескольких действий hello на нескольких устройствах или управляемых узлах. Hello преимущества рабочего процесса через обычный сценарий — возможность hello toosimultaneously выполнения действия с несколькими устройствами и tooautomatically hello возможность восстановления после сбоев. Рабочий процесс Windows PowerShell представляет собой сценарий Windows PowerShell, использующий Windows Workflow Foundation. Хотя рабочий процесс hello написанным с использованием синтаксиса Windows PowerShell и запускается Windows PowerShell, обрабатывается он Windows Workflow Foundation.

Дополнительные сведения по темам hello в этой статье в разделе [Приступая к работе с Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).

## <a name="basic-structure-of-a-workflow"></a>Базовая структура рабочего процесса
Hello tooconverting первый шаг рабочего процесса PowerShell tooa сценария PowerShell заключать с hello **рабочего процесса** ключевое слово.  Рабочий процесс начинается с hello **рабочего процесса** ключевое слово и текст hello hello сценария, заключенное в фигурные скобки. Имя рабочего процесса hello Hello соответствует hello **рабочего процесса** ключевое слово, как показано в hello, используя синтаксис:

    Workflow Test-Workflow
    {
       <Commands>
    }

Имя Hello hello рабочего процесса должно соответствовать имени hello hello Runbook службы автоматизации. Если импортируется hello runbook, то hello имя файла должно совпадать с именем hello рабочего процесса и должны оканчиваться на *.ps1*.

tooadd параметры toohello рабочего процесса используйте hello **Param** так же, как сценарий tooa ключевое слово.

## <a name="code-changes"></a>Изменения в коде
Код рабочего процесса PowerShell выглядит код скрипта tooPowerShell почти так же, за исключением несколько значительных изменений.  Hello в следующих разделах описываются изменения, что необходимый сценарий PowerShell tooa toomake toorun в рабочем процессе.

### <a name="activities"></a>Действия
Действие — это конкретная задача в рабочем процессе. Так же как скрипт состоит из одной или нескольких команд, рабочий процесс состоит из одного или нескольких действий, которые выполняются в последовательности. Рабочий процесс Windows PowerShell автоматически преобразует многие hello tooactivities командлеты Windows PowerShell при запуске рабочего процесса. При указании одного из этих командлетов в модуле runbook hello соответствующее действие выполняется в Windows Workflow Foundation. Для командлетов без соответствующего действия рабочего процесса Windows PowerShell автоматически запускает командлет hello в [InlineScript](#inlinescript) действия. Существует набор командлетов, которые исключаются и не могут использоваться в рабочем процессе, если они явно не включены в блок InlineScript. Дополнительные сведения об этих понятиях см. в статье [Использование действий в рабочих процессах сценариев](http://technet.microsoft.com/library/jj574194.aspx).

Действия рабочих процессов используют набор общих параметров tooconfigure их работу. Дополнительные сведения об общих параметрах hello рабочего процесса см. в разделе [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).

### <a name="positional-parameters"></a>Позиционные параметры
Позиционные параметры нельзя использовать с действиями и командлетами в рабочем процессе.  Это означает, что пользоваться необходимо именами параметров.

Например рассмотрим следующий код, который получает все службы, работающей hello.

     Get-Service | Where-Object {$_.Status -eq "Running"}

При попытке toorun этот же код в рабочем процессе, появится сообщение, как «Не удается разрешить набор hello указан с помощью параметра именованные параметры.»  toocorrect это, укажите имя параметра hello, как показано ниже hello.

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a>Десериализованные объекты
Объекты в рабочих процессах десериализуются.  Это означает, что их свойства по-прежнему доступны, а методы — нет.  Например рассмотрим следующий код PowerShell, который останавливает службу, с помощью метода Stop hello объекта службы hello hello.

    $Service = Get-Service -Name MyService
    $Service.Stop()

Если вы сделаете toorun это в рабочем процессе, появится сообщение об ошибке «вызов метода не поддерживается в рабочем процессе Windows PowerShell».  

Один из вариантов — toowrap эти две строки кода в [InlineScript](#inlinescript) блока, в этом случае $Service бы внутри блока hello объекта службы.

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

Другой вариант — toouse другой командлет, который выполняет hello же функциональность, что метод hello, если он доступен.  В нашем примере hello Stop-Service предоставляет hello же функциональность, что метод остановки hello и использовать следующие hello для рабочего процесса.

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a>InlineScript
Hello **InlineScript** действия полезно, если требуется toorun одной или нескольких команд как традиционный сценарий PowerShell вместо рабочего процесса PowerShell.  Во время обработки команды в рабочем процессе отправляются tooWindows Workflow Foundation, команды в блоке InlineScript обрабатываются Windows PowerShell.

InlineScript использует синтаксис, показанный ниже hello.

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

Может возвращать выходные данные из InlineScript, назначив hello выходной tooa переменной. Hello следующий пример останавливает службу и затем выводит имя службы hello.

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


Значения можно передавать в блок InlineScript, но при этом необходимо использовать модификатор области **$Using** .  Hello ниже приведен предыдущий пример идентичные toohello за исключением того, что hello службы предоставляет имя переменной.

    Workflow Stop-MyService
    {
        $ServiceName = "MyService"

        $Output = InlineScript {
            $Service = Get-Service -Name $Using:ServiceName
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


Во время действия InlineScript могут быть критическими в определенных рабочих процессов, они не поддерживают конструкции рабочего процесса и должен использоваться только при необходимости для hello следующих причин:

* [Контрольные точки](#checkpoints) в блоке InlineScript не используются. В случае сбоя в блоке hello должна быть возобновлена из hello начало блока hello.
* [Параллельное выполнение](#parallel-processing) в блоке InlineScript не используется.
* InlineScript влияет на масштабируемость hello рабочего процесса, поскольку содержит сеанс Windows PowerShell hello для hello всю длину блока InlineScript hello.

Дополнительные сведения об использовании InlineScript см. в статьях [Выполнение команд Windows PowerShell в рабочем процессе](http://technet.microsoft.com/library/jj574197.aspx) и [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).

## <a name="parallel-processing"></a>Параллельная обработка
Одно из преимуществ рабочих процессов Windows PowerShell является возможность tooperform hello набор команд параллельно, а не последовательно как и в стандартном сценарии.

Можно использовать hello **параллельных** ключевое слово toocreate блок сценария с несколькими командами, которые выполняться параллельно. В этом случае используется синтаксис, показанный ниже hello. В этом случае действия Activity1 и Activity2 начинается hello то же время. Действие Activity3 запускается только после завершения действий Activity1 и Activity2.

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


Например рассмотрим следующие команды PowerShell, предназначенных для копирования нескольких файлов tooa сетевым адресом hello.  Эти команды выполняются последовательно, поэтому данный файл необходимо завершить копирование до hello после запуска.     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

Hello следующий рабочий процесс запускает эти же параллельный команд, чтобы все они начинается копирование hello же время.  Только после того, что все они являются скопировать сообщение о завершении hello отображается.

    Workflow Copy-Files
    {
        Parallel
        {
            Copy-Item -Path "C:\LocalPath\File1.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File2.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File3.txt" -Destination "\\NetworkPath"
        }

        Write-Output "Files copied."
    }


Можно использовать hello **ForEach-Parallel** одновременно составлять команды tooprocess для каждого элемента в коллекции. Hello элементов в коллекции hello обрабатываются параллельно, а hello команды в блоке сценария hello выполняются последовательно. В этом случае используется синтаксис, показанный ниже hello. В этом случае действия Activity1 начинается hello же время для всех элементов в коллекции hello. Для каждого элемента действие Activity2 запускается после завершения действия Activity1. Действие Activity3 запускается только после завершения действий Activity1 и Activity2 для всех элементов.

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

Следующий пример Hello — аналогично предыдущего примера toohello копирование файлов в параллельном режиме.  В данном случае после копирования каждого файла отображается отдельное сообщение.  Только после того, что все они являются полностью копируются строительства приветственных сообщений отображается.

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach -Parallel ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
        }

        Write-Output "All files copied."
    }

> [!NOTE]
> Не рекомендуется параллельно выполняемого дочерние модули Runbook, так как это было показано toogive недостоверным результатам.  Hello выходные данные дочернего модуля hello иногда не отображаются, и параметры в один дочерний модуль может повлиять на другие параллельные дочерние модули hello
>

## <a name="checkpoints"></a>Контрольные точки
Объект *контрольной точки* представляет собой моментальный снимок текущего состояния hello hello рабочего процесса, включающего hello текущие значения переменных и любые выходные данные созданного toothat точки. Если рабочий процесс завершается по ошибке или приостановлена, затем hello очередном запуске он будет запущен в последней контрольной точки вместо запуска hello отсечения hello.  Можно установить контрольную точку в рабочем процессе с hello **Checkpoint-Workflow** действия.

В следующий образец кода hello исключение возникает после вызывает Activity2 hello tooend рабочего процесса. При повторном запуске hello рабочего процесса, оно начинается с запуска Activity2, поскольку это действие было сразу после hello последней заданной контрольной точки.

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

Необходимо задать контрольные точки в рабочий процесс после действия, которые могут быть подвержены tooexception и не должны повторяться при возобновлении рабочего процесса hello. Допустим, рабочий процесс создает виртуальную машину. Контрольную точку можно задать до и после hello команды toocreate hello виртуальной машины. Создание hello завершается сбоем, hello команды будет повторяется, если hello рабочий процесс запускается снова. В случае отсечения hello после успешного создания hello, затем hello виртуальной машины не создается повторно при возобновлении рабочего процесса hello.

Следующий пример Hello копирует несколько файлов tooa сетевое расположение и устанавливает контрольную точку после каждого файла.  В случае утери hello сетевое расположение hello рабочий процесс завершается по ошибке.  Когда запускается снова, она будет возобновлено в hello последней контрольной точки, это означает, что только hello файлы, которые уже были скопированы, пропускаются.

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
            Checkpoint-Workflow
        }

        Write-Output "All files copied."
    }

Поскольку учетные данные пользователя не сохраняются после вызова метода hello [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) действия или после последней контрольной точки hello должны toonull учетные данные tooset hello, а затем извлечение их снова из хранилища активов hello после  **Suspend-Workflow** или контрольной точки вызывается.  В противном случае может появиться сообщение об ошибке после hello: *hello задания рабочего процесса нельзя возобновить, либо из-за постоянного хранения данных не удалось сохранить полностью, или сохранить сохраняемости данные повреждены. Необходимо перезапустить рабочий процесс hello.*

Hello после того же кода показано, как toohandle это в модулях Runbook рабочего процесса PowerShell.

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first toocreate hello VM (code not shown)

          # Now add hello VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


Это не обязательно делать, если вы проходите проверку подлинности с помощью учетной записи запуска от имени, настроенной с помощью субъекта-службы.  

Дополнительные сведения о контрольных точках см. в разделе [tooa добавление контрольных точек рабочего процесса сценария](http://technet.microsoft.com/library/jj574114.aspx).

## <a name="next-steps"></a>Дальнейшие действия
* tooget к работе с PowerShell модули Runbook рабочего процесса, в разделе [Мой первый runbook рабочего процесса PowerShell](automation-first-runbook-textual.md)
