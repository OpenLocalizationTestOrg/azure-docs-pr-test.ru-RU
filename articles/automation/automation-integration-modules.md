---
title: "Модуль интеграции службы автоматизации Azure aaaCreate | Документы Microsoft"
description: "Учебник, пошагово hello создания, тестирования и пример использования модули интеграции в службе автоматизации Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 27798efb-08b9-45d9-9b41-5ad91a3df41e
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/13/2017
ms.author: magoedte
ms.openlocfilehash: d4064d8b106496f4dab442024131886c4affccab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-integration-modules"></a>Модули интеграции службы автоматизации Azure
PowerShell — основные технологии hello за автоматизации Azure. Поскольку службы автоматизации Azure выполняется на основе PowerShell, модули PowerShell — расширяемость ключа toohello автоматизации Azure. В этой статье мы поможет hello особенности использования автоматизации Azure модули PowerShell, называется tooas «Модули интеграции» и рекомендации для создания собственных модулей toomake PowerShell, убедиться, что они работают как модули интеграции в Служба автоматизации Azure. 

## <a name="what-is-a-powershell-module"></a>Что такое модуль PowerShell?
Модуль PowerShell — это группа командлеты PowerShell, как **Get-Date** или **Copy-Item**, который может использоваться из консоли PowerShell hello, сценарии, рабочие процессы, модули Runbook и ресурсов PowerShell DSC, таких как WindowsFeature или файл, который можно использовать в конфигурациях PowerShell DSC. Все функциональные возможности PowerShell hello предоставляется с помощью командлетов и ресурсов DSC и каждого командлета и ресурса резервируется модуля PowerShell многие которого поставляются вместе с PowerShell сам. Здравствуйте, например, **Get-Date** является частью модуля Microsoft.PowerShell.Utility PowerShell hello и **Copy-Item** является частью hello модуль Microsoft.PowerShell.Management PowerShell и Hello ресурса DSC пакета является частью модуля PSDesiredStateConfiguration PowerShell hello. Эти модули поставляются с PowerShell. Но не входят в состав PowerShell много модулей PowerShell и вместо них поставляется с первой или сторонних продуктов, как System Center 2012 Configuration Manager или сообществом hello vast PowerShell в местах, например в коллекции PowerShell.  модули Hello полезны, так как они упростить сложные задачи инкапсулированный функциональные возможности.  Дополнительные сведения о модулях PowerShell см. в [библиотеке MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx). 

## <a name="what-is-an-azure-automation-integration-module"></a>Что такое модуль интеграции службы автоматизации Azure?
Модуль интеграции не сильно отличается от модуля PowerShell. Его просто модуль PowerShell, который может содержать один дополнительный файл - файл метаданных, указав тип toobe подключения автоматизации Azure, при использовании модуля hello командлеты в модулях Runbook. Необязательный файл или нет, PowerShell, эти модули могут быть импортированы в автоматизации Azure toomake их командлеты, доступные для использования в Runbook и их ресурсы DSC, доступные для использования в конфигурации DSC. В фоновом hello автоматизации Azure хранит эти модули и задание runbook и время выполнения задания компиляции DSC, загружает их в hello Azure Automation "песочницы" где компиляции конфигурации DSC и модули Runbook выполняются.  Все ресурсы DSC в модулях также автоматически помещаются в опрашивающего сервера DSC службы автоматизации hello, чтобы извлечь машинами попытка tooapply конфигураций DSC.  

Поэтому вы можете начать работу прямо сейчас автоматизация управления Azure, но вы можете импортировать модули PowerShell для любой системы, службы или инструмент toointegrate с стандартной hello в службе автоматизации Azure для вас toouse поставляемых несколько модулей Azure PowerShell. 

> [!NOTE]
> Некоторые модули поставляются как «глобальные модули» в службе автоматизации hello. Эти глобальные модули будут доступны tooyou при создании учетной записи автоматизации, и мы обновления иногда которого автоматически применяет их tooyour учетной записи автоматизации. Если вы не хотите их toobe автоматически обновлены, всегда можно импортировать hello одного модуля самостоятельно и, имеют приоритет над версия глобального модуля hello этого модуля, поставляемых в службе hello. 

Hello формат, в котором импортировать модуль интеграции пакета — это сжатый файл с hello одинаковые имена, как модуль hello и расширение на ZIP. Он содержит модуль Windows PowerShell hello и все вспомогательные файлы, включая файл манифеста (psd1), если модуль hello имеет один.

Если модуль hello должен содержать тип подключения службы автоматизации Azure, он также должен содержать файл с именем hello `<ModuleName>-Automation.json` , указывающий тип свойства hello соединения. Это json-файл в папке модуля hello сжатый ZIP-файла и содержит hello поля «соединения», не требуется tooconnect toohello системы или представляет модуль hello службы. Таким образом в службе автоматизации Azure создается тип соединения. С помощью этого файла можно задать приветствия имен полей, типов, и ли поля hello зашифрованные и / или необязательные для типа соединения hello модуля "hello". Hello ниже приведен шаблон в формате json hello.

```
{ 
   "ConnectionFields": [
   {
      "IsEncrypted":  false,
      "IsOptional":  false,
      "Name":  "ComputerName",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  false,
      "IsOptional":  true,
      "Name":  "Username",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  true,
      "IsOptional":  false,
      "Name":  "Password",
   "TypeName":  "System.String"
   }],
   "ConnectionTypeName":  "DataProtectionManager",
   "IntegrationModuleName":  "DataProtectionManager"
}
```

Если вы развернули Service Management Automation и создан пакеты интеграции модулей для автоматизации Runbook, это выглядит знакомо tooyou. 

## <a name="authoring-best-practices"></a>Рекомендации по созданию
Даже если модули интеграции — это по сути модули PowerShell, по-прежнему есть несколько проблем, рекомендуется учитывать при разработке модуля PowerShell toomake он наиболее можно использовать в службе автоматизации Azure. Некоторые из них являются определенные службы автоматизации Azure, и некоторые из них являются полезным просто toomake модули хорошо работают в рабочий процесс PowerShell, независимо от того, является ли вы используете автоматизации. 

1. Включить краткий обзор, описание и помогают URI для каждого командлета в модуле hello. В PowerShell, можно определить определенные справочную информацию для справки tooreceive пользователя hello tooallow командлеты на их использование с hello **Get-Help** командлета. Например, вот как можно определить краткие сведения и справочный URI для модуля PowerShell, записанного в файле с расширением PSM1:<br>  
   
    ```
    <#
        .SYNOPSIS
         Gets all outgoing phone numbers for this Twilio account 
    #>
    function Get-TwilioPhoneNumbers {
    [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
    HelpUri='http://www.twilio.com/docs/api/rest/outgoing-caller-ids')]
    param(
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AccountSid,
   
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AuthToken,
   
       [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [Hashtable]
       $Connection
    )
   
    $cred = CreateTwilioCredential -Connection $Connection -AccountSid $AccountSid -AuthToken $AuthToken
   
    $uri = "$TWILIO_BASE_URL/Accounts/" + $cred.UserName + "/IncomingPhoneNumbers"
   
    $response = Invoke-RestMethod -Method Get -Uri $uri -Credential $cred
   
    $response.TwilioResponse.IncomingPhoneNumbers.IncomingPhoneNumber
    }
    ```
   <br> Предоставляет эти сведения не будет только отображать справки с помощью hello **Get-Help** в командлет Здравствуйте консоли PowerShell, он также будет предоставлять этой функции справки в автоматизации Azure.  (например, при вставке действий во время создания модуля Runbook). Нажав кнопку «Просмотреть подробную справку» будет Привет открыть справку URI на другой вкладке hello веб-браузер используется tooaccess автоматизации Azure.<br>![Справка по модулям интеграции](media/automation-integration-modules/automation-integration-module-activitydesc.png)
2. Если модуль hello выполняет к удаленной системе,

    а. Он должен содержать файл метаданных модуля интеграции, определяющий hello сведения, необходимые tooconnect toothat удаленной системе, то есть тип подключения hello.  
    b. Каждый командлет в модуле hello должен быть доступ tootake в объект соединения (экземпляр данного типа соединений) как параметр.  

    Командлеты в модуле hello становятся проще toouse в службе автоматизации Azure, если разрешить передачи объекта с полями hello hello соединений типа как параметра toohello командлета. Этот способ не иметь параметры toomap активов toohello hello подключения командлет соответствующих параметров каждый раз, они вызывают командлета. На основании приведенном выше примере runbook hello, используются средства подключения Twilio, вызывается CorpTwilio tooaccess Twilio и возвращать все телефонные номера hello в учетной записи hello.  Обратите внимание на то, как он является сопоставление полей hello hello подключения toohello параметров командлета hello?<br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    Способ проще и лучше tooapproach это непосредственно передается командлета toohello объект connection hello-
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    Чтобы включить поведение следующим образом для вашего командлетов, позволяя tooaccept объект соединения непосредственно в качестве параметра, а не просто полей для параметров подключения. Обычно нужно задать для каждого параметра, чтобы пользователь не с помощью службы автоматизации Azure можно вызвать к командлеты без построения хэш-таблицы tooact как hello объекта соединения. Набор параметров **SpecifyConnectionFields** ниже приведен используемый toopass свойства поля hello соединение по одному. **UseConnectionObject** позволяет передать hello непосредственно через соединение. Как видите, hello в hello командлет Send-TwilioSMS [модуль Twilio PowerShell](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) позволяет передавать в любом случае: 
   
    ```
    function Send-TwilioSMS {
      [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
      HelpUri='http://www.twilio.com/docs/api/rest/sending-sms')]
      param(
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AccountSid,
   
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AuthToken,
   
         [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [Hashtable]
         $Connection
   
       )
    }
    ```
   <br>
3. Определите тип выходных данных для всех командлетов в модуле hello. Определение тип выходных данных для командлета позволяет IntelliSense во время разработки определить hello toohelp выходные свойства hello командлета, для использования во время разработки. Это особенно полезно во время автоматизации runbook графический разработки, где база знаний времени разработки — ключа tooan легко эффективность работы модуля.<br><br> ![Тип выходных данных графического модуля Runbook](media/automation-integration-modules/runbook-graphical-module-output-type.png)<br> Это аналогично функции «типа вперед» toohello командлета выходных данных в интегрированной среде Сценариев PowerShell без необходимости toorun его.<br><br> ![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)<br>
4. Командлеты в модуле hello не должен принимать сложный объект типы параметров. Рабочий процесс PowerShell отличается от PowerShell, так как сложные типы объектов хранятся в нем в десериализованной форме. Типы-примитивы остается как примитивы, но сложные типы — это преобразованное tootheir десериализовать версии, являющиеся по существу контейнеры свойств. Например, если вы использовали hello **Get-Process** командлета в книгу (или рабочий процесс PowerShell по этой причине), он возвращают объект типа [Deserialized.System.Diagnostic.Process], не Здравствуйте, ожидаемый [ Тип System.Diagnostic.Process, возвращаемыми]. Этот тип содержит все hello и те же свойства, как hello-десериализации типа, но ни один из методов hello. Если при попытке toopass это значение как параметр командлета tooa, где hello для командлета ожидается значение [System.Diagnostic.Process, возвращаемыми] для этого параметра, вы сможете получать hello следующая ошибка: *не удается обработать преобразования аргумент для параметра «процесс» . Ошибка: «не удается преобразовать значение «System.Diagnostics.Process (CcmExec)» hello типа «Deserialized.System.Diagnostics.Process» tootype «System.Diagnostics.Process».*   Причина в том, что несоответствие типов между hello ожидается тип [System.Diagnostic.Process, возвращаемыми] и hello указанный тип [Deserialized.System.Diagnostic.Process]. Hello способом разрешения этой проблемы — командлеты hello tooensure своего модуля не выполняют сложные типы параметров. Вот toodo hello неправильный способ его.
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    А вот hello вправо, получения примитив, который используется внутренне командлетом hello toograb hello сложный объект и использовать его. Так как командлеты выполняются в контексте hello PowerShell, не рабочий процесс PowerShell, в командлет hello $process становится hello правильный тип [System.Diagnostic.Process, возвращаемыми].  
   
    ```
    function Get-ProcessDescription {
      param (
            [String] $processName
      )
      $process = Get-Process -Name $processName
   
      $process.Description
    }
    ```
   <br>
   Средства подключения в Runbook — это хэш-таблицы, которые входят в сложный тип, и еще эти хэш-таблицы показаться может toobe toobe передан в командлеты для их — параметр подключения полностью, за исключением без приведения. С технической точки зрения, некоторые PowerShell типы могли toocast должным образом из их формы tootheir десериализовать сериализованную форму и таким образом могут быть переданы в командлеты для принятия hello-десериализовать тип параметров. Один из таких типов — хэш-таблица. Для автора модуля определенные типы toobe реализован в виде, они правильно выполнить десериализацию также возможна, но существуют некоторые tooconsider преимущества и недостатки. Здравствуйте toohave потребности типа конструктор по умолчанию, все его открытых свойств, а также иметь PSTypeConverter. Тем не менее, для типов, уже определен, автора модуля hello не владеет, не слишком «исправить» их, поэтому hello рекомендация tooavoid сложных типов для параметров, которые все вместе. Разработка Runbook Совет: Если для какой-то причине к командлеты требуется tootake сложного типа, или вы используете другой модуль, который требует сложного параметра типа, решение hello в модулях Runbook рабочего процесса PowerShell и рабочими процессами PowerShell в локальной PowerShell, — toowrap hello командлета, приводит к возникновению ошибки hello сложный тип или hello, использующий hello сложного типа в hello одного действия InlineScript. Поскольку InlineScript выполняет его содержимое как PowerShell, а не рабочего процесса PowerShell, командлет hello формировании сложного типа hello приведет к получению правильного типа, не hello десериализовать сложного типа.
5. Сделать все командлеты в модуле hello без сохранения состояния. Рабочий процесс PowerShell выполняется каждый командлет вызван в рабочем процессе hello в другом сеансе. Это значит, все командлеты, которые зависят от состояния сеанса создан или изменен другими командлетами hello одного модуля не смогут работать в модулях Runbook рабочего процесса PowerShell.  Ниже приведен пример того, что не toodo.
   
    ```
    $globalNum = 0
    function Set-GlobalNum {
       param(
           [int] $num
       )
   
       $globalNum = $num
    }
    function Get-GlobalNumTimesTwo {
       $output = $globalNum * 2
   
       $output
    }
    ```
   <br>
6. модуль Hello должен полностью содержаться в пакет может Xcopy. Так как модули автоматизации Azure "песочницы" автоматизации распределенных toohello при модулей Runbook должны tooexecute, они должны toowork независимо от hello узла, на котором работают на. Это означает, что должна быть может tooZip пакет модуля hello, переместите его tooany другому узлу с hello же или более новой версии PowerShell и его работать в обычном режиме, при импорте в среде PowerShell, на которых размещены. В порядке, toohappen модуль hello следует не зависят от вне hello модуля (папка hello, возвращает сжаты при импорте в Azure Automation) файлы или на любой уникальный реестр на узле, например были заданы параметрами hello установки продукта. При несоблюдении этой рекомендации, hello модуль не будет доступна в службе автоматизации Azure.  

## <a name="next-steps"></a>Дальнейшие действия

* tooget к работе с PowerShell модули Runbook рабочего процесса, в разделе [Мой первый runbook рабочего процесса PowerShell](automation-first-runbook-textual.md)
* . в разделе toolearn Дополнительные сведения о создании модулей PowerShell [написание модуля Windows PowerShell](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)

