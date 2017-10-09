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
# <a name="azure-automation-integration-modules"></a><span data-ttu-id="12a63-103">Модули интеграции службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="12a63-103">Azure Automation Integration Modules</span></span>
<span data-ttu-id="12a63-104">PowerShell — основные технологии hello за автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="12a63-104">PowerShell is hello fundamental technology behind Azure Automation.</span></span> <span data-ttu-id="12a63-105">Поскольку службы автоматизации Azure выполняется на основе PowerShell, модули PowerShell — расширяемость ключа toohello автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="12a63-105">Since Azure Automation is built on PowerShell, PowerShell modules are key toohello extensibility of Azure Automation.</span></span> <span data-ttu-id="12a63-106">В этой статье мы поможет hello особенности использования автоматизации Azure модули PowerShell, называется tooas «Модули интеграции» и рекомендации для создания собственных модулей toomake PowerShell, убедиться, что они работают как модули интеграции в Служба автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="12a63-106">In this article, we will guide you through hello specifics of Azure Automation’s use of PowerShell modules, referred tooas “Integration Modules”, and best practices for creating your own PowerShell modules toomake sure they work as Integration Modules within Azure Automation.</span></span> 

## <a name="what-is-a-powershell-module"></a><span data-ttu-id="12a63-107">Что такое модуль PowerShell?</span><span class="sxs-lookup"><span data-stu-id="12a63-107">What is a PowerShell Module?</span></span>
<span data-ttu-id="12a63-108">Модуль PowerShell — это группа командлеты PowerShell, как **Get-Date** или **Copy-Item**, который может использоваться из консоли PowerShell hello, сценарии, рабочие процессы, модули Runbook и ресурсов PowerShell DSC, таких как WindowsFeature или файл, который можно использовать в конфигурациях PowerShell DSC.</span><span class="sxs-lookup"><span data-stu-id="12a63-108">A PowerShell module is a group of PowerShell cmdlets like **Get-Date** or **Copy-Item**, that can be used from hello PowerShell console, scripts, workflows, runbooks, and PowerShell DSC resources like WindowsFeature or File, that can be used from PowerShell DSC configurations.</span></span> <span data-ttu-id="12a63-109">Все функциональные возможности PowerShell hello предоставляется с помощью командлетов и ресурсов DSC и каждого командлета и ресурса резервируется модуля PowerShell многие которого поставляются вместе с PowerShell сам.</span><span class="sxs-lookup"><span data-stu-id="12a63-109">All of hello functionality of PowerShell is exposed through cmdlets and DSC resources, and every cmdlet/DSC resource is backed by a PowerShell module, many of which ship with PowerShell itself.</span></span> <span data-ttu-id="12a63-110">Здравствуйте, например, **Get-Date** является частью модуля Microsoft.PowerShell.Utility PowerShell hello и **Copy-Item** является частью hello модуль Microsoft.PowerShell.Management PowerShell и Hello ресурса DSC пакета является частью модуля PSDesiredStateConfiguration PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="12a63-110">For example, hello **Get-Date** cmdlet is part of hello Microsoft.PowerShell.Utility PowerShell module, and **Copy-Item** cmdlet is part of hello Microsoft.PowerShell.Management PowerShell module and hello Package DSC resource is part of hello PSDesiredStateConfiguration PowerShell module.</span></span> <span data-ttu-id="12a63-111">Эти модули поставляются с PowerShell.</span><span class="sxs-lookup"><span data-stu-id="12a63-111">Both of these modules ship with PowerShell.</span></span> <span data-ttu-id="12a63-112">Но не входят в состав PowerShell много модулей PowerShell и вместо них поставляется с первой или сторонних продуктов, как System Center 2012 Configuration Manager или сообществом hello vast PowerShell в местах, например в коллекции PowerShell.</span><span class="sxs-lookup"><span data-stu-id="12a63-112">But many PowerShell modules do not ship as part of PowerShell, and are instead distributed with first or third-party products like System Center 2012 Configuration Manager or by hello vast PowerShell community on places like PowerShell Gallery.</span></span>  <span data-ttu-id="12a63-113">модули Hello полезны, так как они упростить сложные задачи инкапсулированный функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="12a63-113">hello modules are useful because they make complex tasks simpler through encapsulated functionality.</span></span>  <span data-ttu-id="12a63-114">Дополнительные сведения о модулях PowerShell см. в [библиотеке MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="12a63-114">You can learn more about [PowerShell modules on MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span></span> 

## <a name="what-is-an-azure-automation-integration-module"></a><span data-ttu-id="12a63-115">Что такое модуль интеграции службы автоматизации Azure?</span><span class="sxs-lookup"><span data-stu-id="12a63-115">What is an Azure Automation Integration Module?</span></span>
<span data-ttu-id="12a63-116">Модуль интеграции не сильно отличается от модуля PowerShell.</span><span class="sxs-lookup"><span data-stu-id="12a63-116">An Integration Module isn't very different from a PowerShell module.</span></span> <span data-ttu-id="12a63-117">Его просто модуль PowerShell, который может содержать один дополнительный файл - файл метаданных, указав тип toobe подключения автоматизации Azure, при использовании модуля hello командлеты в модулях Runbook.</span><span class="sxs-lookup"><span data-stu-id="12a63-117">Its simply a PowerShell module that optionally contains one additional file - a metadata file specifying an Azure Automation connection type toobe used with hello module's cmdlets in runbooks.</span></span> <span data-ttu-id="12a63-118">Необязательный файл или нет, PowerShell, эти модули могут быть импортированы в автоматизации Azure toomake их командлеты, доступные для использования в Runbook и их ресурсы DSC, доступные для использования в конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="12a63-118">Optional file or not, these PowerShell modules can be imported into Azure Automation toomake their cmdlets available for use within runbooks and their DSC resources available for use within DSC configurations.</span></span> <span data-ttu-id="12a63-119">В фоновом hello автоматизации Azure хранит эти модули и задание runbook и время выполнения задания компиляции DSC, загружает их в hello Azure Automation "песочницы" где компиляции конфигурации DSC и модули Runbook выполняются.</span><span class="sxs-lookup"><span data-stu-id="12a63-119">Behind hello scenes, Azure Automation stores these modules, and at runbook job and DSC compilation job execution time, loads them into hello Azure Automation sandboxes where runbooks are executed and DSC configurations are compiled.</span></span>  <span data-ttu-id="12a63-120">Все ресурсы DSC в модулях также автоматически помещаются в опрашивающего сервера DSC службы автоматизации hello, чтобы извлечь машинами попытка tooapply конфигураций DSC.</span><span class="sxs-lookup"><span data-stu-id="12a63-120">Any DSC resources in modules are also automatically placed on hello Automation DSC pull server, so that they can be pulled by machines attempting tooapply DSC configurations.</span></span>  

<span data-ttu-id="12a63-121">Поэтому вы можете начать работу прямо сейчас автоматизация управления Azure, но вы можете импортировать модули PowerShell для любой системы, службы или инструмент toointegrate с стандартной hello в службе автоматизации Azure для вас toouse поставляемых несколько модулей Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="12a63-121">We ship a number of Azure  PowerShell modules out of hello box in Azure Automation for you toouse so you can get started automating Azure management right away, but you can import PowerShell modules for whatever system, service, or tool you want toointegrate with.</span></span> 

> [!NOTE]
> <span data-ttu-id="12a63-122">Некоторые модули поставляются как «глобальные модули» в службе автоматизации hello.</span><span class="sxs-lookup"><span data-stu-id="12a63-122">Certain modules are shipped as “global modules” in hello Automation service.</span></span> <span data-ttu-id="12a63-123">Эти глобальные модули будут доступны tooyou при создании учетной записи автоматизации, и мы обновления иногда которого автоматически применяет их tooyour учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="12a63-123">These global modules are available tooyou when you create an automation account, and we update them sometimes which automatically pushes them out tooyour automation account.</span></span> <span data-ttu-id="12a63-124">Если вы не хотите их toobe автоматически обновлены, всегда можно импортировать hello одного модуля самостоятельно и, имеют приоритет над версия глобального модуля hello этого модуля, поставляемых в службе hello.</span><span class="sxs-lookup"><span data-stu-id="12a63-124">If you don’t want them toobe auto-updated, you can always import hello same module yourself, and that will take precedence over hello global module version of that module that we ship in hello service.</span></span> 

<span data-ttu-id="12a63-125">Hello формат, в котором импортировать модуль интеграции пакета — это сжатый файл с hello одинаковые имена, как модуль hello и расширение на ZIP.</span><span class="sxs-lookup"><span data-stu-id="12a63-125">hello format in which you import an Integration Module package is a compressed file with hello same name as hello module and a .zip extension.</span></span> <span data-ttu-id="12a63-126">Он содержит модуль Windows PowerShell hello и все вспомогательные файлы, включая файл манифеста (psd1), если модуль hello имеет один.</span><span class="sxs-lookup"><span data-stu-id="12a63-126">It contains hello Windows PowerShell module and any supporting files, including a manifest file (.psd1) if hello module has one.</span></span>

<span data-ttu-id="12a63-127">Если модуль hello должен содержать тип подключения службы автоматизации Azure, он также должен содержать файл с именем hello `<ModuleName>-Automation.json` , указывающий тип свойства hello соединения.</span><span class="sxs-lookup"><span data-stu-id="12a63-127">If hello module should contain an Azure Automation connection type, it must also contain a file with hello name `<ModuleName>-Automation.json` that specifies hello connection type properties.</span></span> <span data-ttu-id="12a63-128">Это json-файл в папке модуля hello сжатый ZIP-файла и содержит hello поля «соединения», не требуется tooconnect toohello системы или представляет модуль hello службы.</span><span class="sxs-lookup"><span data-stu-id="12a63-128">This is a json file placed within hello module folder of your compressed .zip file, and contains hello fields of a “connection” that is required tooconnect toohello system or service hello module represents.</span></span> <span data-ttu-id="12a63-129">Таким образом в службе автоматизации Azure создается тип соединения.</span><span class="sxs-lookup"><span data-stu-id="12a63-129">This will end up creating a connection type in Azure Automation.</span></span> <span data-ttu-id="12a63-130">С помощью этого файла можно задать приветствия имен полей, типов, и ли поля hello зашифрованные и / или необязательные для типа соединения hello модуля "hello".</span><span class="sxs-lookup"><span data-stu-id="12a63-130">Using this file you can set hello field names, types, and whether hello fields should be encrypted and / or optional, for hello connection type of hello module.</span></span> <span data-ttu-id="12a63-131">Hello ниже приведен шаблон в формате json hello.</span><span class="sxs-lookup"><span data-stu-id="12a63-131">hello following is a template in hello json file format:</span></span>

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

<span data-ttu-id="12a63-132">Если вы развернули Service Management Automation и создан пакеты интеграции модулей для автоматизации Runbook, это выглядит знакомо tooyou.</span><span class="sxs-lookup"><span data-stu-id="12a63-132">If you have deployed Service Management Automation and created Integration Modules packages for your automation runbooks, this should look very familiar tooyou.</span></span> 

## <a name="authoring-best-practices"></a><span data-ttu-id="12a63-133">Рекомендации по созданию</span><span class="sxs-lookup"><span data-stu-id="12a63-133">Authoring Best Practices</span></span>
<span data-ttu-id="12a63-134">Даже если модули интеграции — это по сути модули PowerShell, по-прежнему есть несколько проблем, рекомендуется учитывать при разработке модуля PowerShell toomake он наиболее можно использовать в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="12a63-134">Even though Integration Modules are essentially PowerShell modules, there’s still a number of things we recommend you consider while authoring a PowerShell module, toomake it most usable in Azure Automation.</span></span> <span data-ttu-id="12a63-135">Некоторые из них являются определенные службы автоматизации Azure, и некоторые из них являются полезным просто toomake модули хорошо работают в рабочий процесс PowerShell, независимо от того, является ли вы используете автоматизации.</span><span class="sxs-lookup"><span data-stu-id="12a63-135">Some of these are Azure Automation specific, and some of them are useful just toomake your modules work well in PowerShell Workflow, regardless of whether or not you’re using Automation.</span></span> 

1. <span data-ttu-id="12a63-136">Включить краткий обзор, описание и помогают URI для каждого командлета в модуле hello.</span><span class="sxs-lookup"><span data-stu-id="12a63-136">Include a synopsis, description, and help URI for every cmdlet in hello module.</span></span> <span data-ttu-id="12a63-137">В PowerShell, можно определить определенные справочную информацию для справки tooreceive пользователя hello tooallow командлеты на их использование с hello **Get-Help** командлета.</span><span class="sxs-lookup"><span data-stu-id="12a63-137">In PowerShell, you can define certain help information for cmdlets tooallow hello user tooreceive help on using them with hello **Get-Help** cmdlet.</span></span> <span data-ttu-id="12a63-138">Например, вот как можно определить краткие сведения и справочный URI для модуля PowerShell, записанного в файле с расширением PSM1:</span><span class="sxs-lookup"><span data-stu-id="12a63-138">For example, here’s how you can define a synopsis and help URI for a PowerShell module written in a .psm1 file.</span></span><br>  
   
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
   <br> <span data-ttu-id="12a63-139">Предоставляет эти сведения не будет только отображать справки с помощью hello **Get-Help** в командлет Здравствуйте консоли PowerShell, он также будет предоставлять этой функции справки в автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="12a63-139">Providing this info will not only show this help using hello **Get-Help** cmdlet in hello PowerShell console, it will also expose this help functionality within Azure Automation.</span></span>  <span data-ttu-id="12a63-140">(например, при вставке действий во время создания модуля Runbook).</span><span class="sxs-lookup"><span data-stu-id="12a63-140">For example, when inserting activities during runbook authoring.</span></span> <span data-ttu-id="12a63-141">Нажав кнопку «Просмотреть подробную справку» будет Привет открыть справку URI на другой вкладке hello веб-браузер используется tooaccess автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="12a63-141">Clicking “View detailed help” will open hello help URI in another tab of hello web browser you’re using tooaccess Azure Automation.</span></span><br><span data-ttu-id="12a63-142">![Справка по модулям интеграции](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span><span class="sxs-lookup"><span data-stu-id="12a63-142">![Integration Module Help](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span></span>
2. <span data-ttu-id="12a63-143">Если модуль hello выполняет к удаленной системе,</span><span class="sxs-lookup"><span data-stu-id="12a63-143">If hello module runs against a remote system,</span></span>

    <span data-ttu-id="12a63-144">а.</span><span class="sxs-lookup"><span data-stu-id="12a63-144">a.</span></span> <span data-ttu-id="12a63-145">Он должен содержать файл метаданных модуля интеграции, определяющий hello сведения, необходимые tooconnect toothat удаленной системе, то есть тип подключения hello.</span><span class="sxs-lookup"><span data-stu-id="12a63-145">It should contain an Integration Module metadata file that defines hello information needed tooconnect toothat remote system, meaning hello connection type.</span></span>  
    <span data-ttu-id="12a63-146">b.</span><span class="sxs-lookup"><span data-stu-id="12a63-146">b.</span></span> <span data-ttu-id="12a63-147">Каждый командлет в модуле hello должен быть доступ tootake в объект соединения (экземпляр данного типа соединений) как параметр.</span><span class="sxs-lookup"><span data-stu-id="12a63-147">Each cmdlet in hello module should be able tootake in a connection object (an instance of that connection type) as a parameter.</span></span>  

    <span data-ttu-id="12a63-148">Командлеты в модуле hello становятся проще toouse в службе автоматизации Azure, если разрешить передачи объекта с полями hello hello соединений типа как параметра toohello командлета.</span><span class="sxs-lookup"><span data-stu-id="12a63-148">Cmdlets in hello module become easier toouse in Azure Automation if you allow passing an object with hello fields of hello connection type as a parameter toohello cmdlet.</span></span> <span data-ttu-id="12a63-149">Этот способ не иметь параметры toomap активов toohello hello подключения командлет соответствующих параметров каждый раз, они вызывают командлета.</span><span class="sxs-lookup"><span data-stu-id="12a63-149">This way users don’t have toomap parameters of hello connection asset toohello cmdlet's corresponding parameters each time they call a cmdlet.</span></span> <span data-ttu-id="12a63-150">На основании приведенном выше примере runbook hello, используются средства подключения Twilio, вызывается CorpTwilio tooaccess Twilio и возвращать все телефонные номера hello в учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="12a63-150">Based on hello runbook example above, it uses a Twilio connection asset called CorpTwilio tooaccess Twilio and return all hello phone numbers in hello account.</span></span>  <span data-ttu-id="12a63-151">Обратите внимание на то, как он является сопоставление полей hello hello подключения toohello параметров командлета hello?</span><span class="sxs-lookup"><span data-stu-id="12a63-151">Notice how it is mapping hello fields of hello connection toohello parameters of hello cmdlet?</span></span><br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    <span data-ttu-id="12a63-152">Способ проще и лучше tooapproach это непосредственно передается командлета toohello объект connection hello-</span><span class="sxs-lookup"><span data-stu-id="12a63-152">An easier and better way tooapproach this is directly passing hello connection object toohello cmdlet -</span></span>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    <span data-ttu-id="12a63-153">Чтобы включить поведение следующим образом для вашего командлетов, позволяя tooaccept объект соединения непосредственно в качестве параметра, а не просто полей для параметров подключения.</span><span class="sxs-lookup"><span data-stu-id="12a63-153">You can enable behavior like this for your cmdlets by allowing them tooaccept a connection object directly as a parameter, instead of just connection fields for parameters.</span></span> <span data-ttu-id="12a63-154">Обычно нужно задать для каждого параметра, чтобы пользователь не с помощью службы автоматизации Azure можно вызвать к командлеты без построения хэш-таблицы tooact как hello объекта соединения.</span><span class="sxs-lookup"><span data-stu-id="12a63-154">Usually you’ll want a parameter set for each, so that a user not using Azure Automation can call your cmdlets without constructing a hashtable tooact as hello connection object.</span></span> <span data-ttu-id="12a63-155">Набор параметров **SpecifyConnectionFields** ниже приведен используемый toopass свойства поля hello соединение по одному.</span><span class="sxs-lookup"><span data-stu-id="12a63-155">Parameter set **SpecifyConnectionFields** below is used toopass hello connection field properties one by one.</span></span> <span data-ttu-id="12a63-156">**UseConnectionObject** позволяет передать hello непосредственно через соединение.</span><span class="sxs-lookup"><span data-stu-id="12a63-156">**UseConnectionObject** lets you pass hello connection straight through.</span></span> <span data-ttu-id="12a63-157">Как видите, hello в hello командлет Send-TwilioSMS [модуль Twilio PowerShell](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) позволяет передавать в любом случае:</span><span class="sxs-lookup"><span data-stu-id="12a63-157">As you can see, hello Send-TwilioSMS cmdlet in hello [Twilio PowerShell module](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) allows passing either way:</span></span> 
   
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
3. <span data-ttu-id="12a63-158">Определите тип выходных данных для всех командлетов в модуле hello.</span><span class="sxs-lookup"><span data-stu-id="12a63-158">Define output type for all cmdlets in hello module.</span></span> <span data-ttu-id="12a63-159">Определение тип выходных данных для командлета позволяет IntelliSense во время разработки определить hello toohelp выходные свойства hello командлета, для использования во время разработки.</span><span class="sxs-lookup"><span data-stu-id="12a63-159">Defining an output type for a cmdlet allows design-time IntelliSense toohelp you determine hello output properties of hello cmdlet, for use during authoring.</span></span> <span data-ttu-id="12a63-160">Это особенно полезно во время автоматизации runbook графический разработки, где база знаний времени разработки — ключа tooan легко эффективность работы модуля.</span><span class="sxs-lookup"><span data-stu-id="12a63-160">It is especially helpful during Automation runbook graphical authoring, where design time knowledge is key tooan easy user experience with your module.</span></span><br><br> <span data-ttu-id="12a63-161">![Тип выходных данных графического модуля Runbook](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span><span class="sxs-lookup"><span data-stu-id="12a63-161">![Graphical Runbook Output Type](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span></span><br> <span data-ttu-id="12a63-162">Это аналогично функции «типа вперед» toohello командлета выходных данных в интегрированной среде Сценариев PowerShell без необходимости toorun его.</span><span class="sxs-lookup"><span data-stu-id="12a63-162">This is similar toohello "type ahead" functionality of a cmdlet's output in PowerShell ISE without having toorun it.</span></span><br><br> <span data-ttu-id="12a63-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span><span class="sxs-lookup"><span data-stu-id="12a63-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span></span><br>
4. <span data-ttu-id="12a63-164">Командлеты в модуле hello не должен принимать сложный объект типы параметров.</span><span class="sxs-lookup"><span data-stu-id="12a63-164">Cmdlets in hello module should not take complex object types for parameters.</span></span> <span data-ttu-id="12a63-165">Рабочий процесс PowerShell отличается от PowerShell, так как сложные типы объектов хранятся в нем в десериализованной форме.</span><span class="sxs-lookup"><span data-stu-id="12a63-165">PowerShell Workflow is different from PowerShell in that it stores complex types in deserialized form.</span></span> <span data-ttu-id="12a63-166">Типы-примитивы остается как примитивы, но сложные типы — это преобразованное tootheir десериализовать версии, являющиеся по существу контейнеры свойств.</span><span class="sxs-lookup"><span data-stu-id="12a63-166">Primitive types will stay as primitives, but complex types are converted tootheir deserialized versions, which are essentially property bags.</span></span> <span data-ttu-id="12a63-167">Например, если вы использовали hello **Get-Process** командлета в книгу (или рабочий процесс PowerShell по этой причине), он возвращают объект типа [Deserialized.System.Diagnostic.Process], не Здравствуйте, ожидаемый [ Тип System.Diagnostic.Process, возвращаемыми].</span><span class="sxs-lookup"><span data-stu-id="12a63-167">For example, if you used hello **Get-Process** cmdlet in a runbook (or a PowerShell Workflow for that matter), it would return an object of type [Deserialized.System.Diagnostic.Process], not hello expected [System.Diagnostic.Process] type.</span></span> <span data-ttu-id="12a63-168">Этот тип содержит все hello и те же свойства, как hello-десериализации типа, но ни один из методов hello.</span><span class="sxs-lookup"><span data-stu-id="12a63-168">This type has all hello same properties as hello non-deserialized type, but none of hello methods.</span></span> <span data-ttu-id="12a63-169">Если при попытке toopass это значение как параметр командлета tooa, где hello для командлета ожидается значение [System.Diagnostic.Process, возвращаемыми] для этого параметра, вы сможете получать hello следующая ошибка: *не удается обработать преобразования аргумент для параметра «процесс» . Ошибка: «не удается преобразовать значение «System.Diagnostics.Process (CcmExec)» hello типа «Deserialized.System.Diagnostics.Process» tootype «System.Diagnostics.Process».*</span><span class="sxs-lookup"><span data-stu-id="12a63-169">And if you try toopass this value as a parameter tooa cmdlet, where hello cmdlet expects a [System.Diagnostic.Process] value for this parameter, you’ll receive hello following error: *Cannot process argument transformation on parameter 'process'. Error: "Cannot convert hello "System.Diagnostics.Process (CcmExec)" value of type  "Deserialized.System.Diagnostics.Process" tootype "System.Diagnostics.Process".*</span></span>   <span data-ttu-id="12a63-170">Причина в том, что несоответствие типов между hello ожидается тип [System.Diagnostic.Process, возвращаемыми] и hello указанный тип [Deserialized.System.Diagnostic.Process].</span><span class="sxs-lookup"><span data-stu-id="12a63-170">This is because there is a type mismatch between hello expected [System.Diagnostic.Process] type and hello given [Deserialized.System.Diagnostic.Process] type.</span></span> <span data-ttu-id="12a63-171">Hello способом разрешения этой проблемы — командлеты hello tooensure своего модуля не выполняют сложные типы параметров.</span><span class="sxs-lookup"><span data-stu-id="12a63-171">hello way around this issue is tooensure hello cmdlets of your module do not take complex types for parameters.</span></span> <span data-ttu-id="12a63-172">Вот toodo hello неправильный способ его.</span><span class="sxs-lookup"><span data-stu-id="12a63-172">Here is hello wrong way toodo it.</span></span>
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    <span data-ttu-id="12a63-173">А вот hello вправо, получения примитив, который используется внутренне командлетом hello toograb hello сложный объект и использовать его.</span><span class="sxs-lookup"><span data-stu-id="12a63-173">And here is hello right way, taking in a primitive that can be used internally by hello cmdlet toograb hello complex object and use it.</span></span> <span data-ttu-id="12a63-174">Так как командлеты выполняются в контексте hello PowerShell, не рабочий процесс PowerShell, в командлет hello $process становится hello правильный тип [System.Diagnostic.Process, возвращаемыми].</span><span class="sxs-lookup"><span data-stu-id="12a63-174">Since cmdlets execute in hello context of PowerShell, not PowerShell Workflow, inside hello cmdlet $process becomes hello correct [System.Diagnostic.Process] type.</span></span>  
   
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
   <span data-ttu-id="12a63-175">Средства подключения в Runbook — это хэш-таблицы, которые входят в сложный тип, и еще эти хэш-таблицы показаться может toobe toobe передан в командлеты для их — параметр подключения полностью, за исключением без приведения.</span><span class="sxs-lookup"><span data-stu-id="12a63-175">Connection assets in runbooks are hashtables, which are a complex type, and yet these hashtables seem toobe able toobe passed into cmdlets for their –Connection parameter perfectly, with no cast exception.</span></span> <span data-ttu-id="12a63-176">С технической точки зрения, некоторые PowerShell типы могли toocast должным образом из их формы tootheir десериализовать сериализованную форму и таким образом могут быть переданы в командлеты для принятия hello-десериализовать тип параметров.</span><span class="sxs-lookup"><span data-stu-id="12a63-176">Technically, some PowerShell types are able toocast properly from their serialized form tootheir deserialized form, and hence can be passed into cmdlets for parameters accepting hello non-deserialized type.</span></span> <span data-ttu-id="12a63-177">Один из таких типов — хэш-таблица.</span><span class="sxs-lookup"><span data-stu-id="12a63-177">Hashtable is one of these.</span></span> <span data-ttu-id="12a63-178">Для автора модуля определенные типы toobe реализован в виде, они правильно выполнить десериализацию также возможна, но существуют некоторые tooconsider преимущества и недостатки.</span><span class="sxs-lookup"><span data-stu-id="12a63-178">It’s possible for a module author’s defined types toobe implemented in a way that they can correctly deserialize as well, but there are some trade-offs tooconsider.</span></span> <span data-ttu-id="12a63-179">Здравствуйте toohave потребности типа конструктор по умолчанию, все его открытых свойств, а также иметь PSTypeConverter.</span><span class="sxs-lookup"><span data-stu-id="12a63-179">hello type needs toohave a default constructor, have all of its properties public, and have a PSTypeConverter.</span></span> <span data-ttu-id="12a63-180">Тем не менее, для типов, уже определен, автора модуля hello не владеет, не слишком «исправить» их, поэтому hello рекомендация tooavoid сложных типов для параметров, которые все вместе.</span><span class="sxs-lookup"><span data-stu-id="12a63-180">However, for already-defined types that hello module author does not own, there is no way too“fix” them, hence hello recommendation tooavoid complex types for parameters all together.</span></span> <span data-ttu-id="12a63-181">Разработка Runbook Совет: Если для какой-то причине к командлеты требуется tootake сложного типа, или вы используете другой модуль, который требует сложного параметра типа, решение hello в модулях Runbook рабочего процесса PowerShell и рабочими процессами PowerShell в локальной PowerShell, — toowrap hello командлета, приводит к возникновению ошибки hello сложный тип или hello, использующий hello сложного типа в hello одного действия InlineScript.</span><span class="sxs-lookup"><span data-stu-id="12a63-181">Runbook Authoring tip: If for some reason your cmdlets need tootake a complex type parameter, or you are using someone else’s module that requires a complex type parameter, hello workaround in PowerShell Workflow runbooks and PowerShell Workflows in local PowerShell, is toowrap hello cmdlet that generates hello complex type and hello cmdlet that consumes hello complex type in hello same InlineScript activity.</span></span> <span data-ttu-id="12a63-182">Поскольку InlineScript выполняет его содержимое как PowerShell, а не рабочего процесса PowerShell, командлет hello формировании сложного типа hello приведет к получению правильного типа, не hello десериализовать сложного типа.</span><span class="sxs-lookup"><span data-stu-id="12a63-182">Since InlineScript executes its contents as PowerShell rather than PowerShell Workflow, hello cmdlet generating hello complex type would produce that correct type, not hello deserialized complex type.</span></span>
5. <span data-ttu-id="12a63-183">Сделать все командлеты в модуле hello без сохранения состояния.</span><span class="sxs-lookup"><span data-stu-id="12a63-183">Make all cmdlets in hello module stateless.</span></span> <span data-ttu-id="12a63-184">Рабочий процесс PowerShell выполняется каждый командлет вызван в рабочем процессе hello в другом сеансе.</span><span class="sxs-lookup"><span data-stu-id="12a63-184">PowerShell Workflow runs every cmdlet called in hello workflow in a different session.</span></span> <span data-ttu-id="12a63-185">Это значит, все командлеты, которые зависят от состояния сеанса создан или изменен другими командлетами hello одного модуля не смогут работать в модулях Runbook рабочего процесса PowerShell.</span><span class="sxs-lookup"><span data-stu-id="12a63-185">This means any cmdlets that depend on session state created / modified by other cmdlets in hello same module will not work in PowerShell Workflow runbooks.</span></span>  <span data-ttu-id="12a63-186">Ниже приведен пример того, что не toodo.</span><span class="sxs-lookup"><span data-stu-id="12a63-186">Here is an example of what not toodo.</span></span>
   
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
6. <span data-ttu-id="12a63-187">модуль Hello должен полностью содержаться в пакет может Xcopy.</span><span class="sxs-lookup"><span data-stu-id="12a63-187">hello module should be fully contained in an Xcopy-able package.</span></span> <span data-ttu-id="12a63-188">Так как модули автоматизации Azure "песочницы" автоматизации распределенных toohello при модулей Runbook должны tooexecute, они должны toowork независимо от hello узла, на котором работают на.</span><span class="sxs-lookup"><span data-stu-id="12a63-188">Because Azure Automation modules are distributed toohello Automation sandboxes when runbooks need tooexecute, they need toowork independently of hello host they are running on.</span></span> <span data-ttu-id="12a63-189">Это означает, что должна быть может tooZip пакет модуля hello, переместите его tooany другому узлу с hello же или более новой версии PowerShell и его работать в обычном режиме, при импорте в среде PowerShell, на которых размещены.</span><span class="sxs-lookup"><span data-stu-id="12a63-189">What this means is that you should be able tooZip up hello module package, move it tooany other host with hello same or newer PowerShell version, and have it function as normal when imported into that host’s PowerShell environment.</span></span> <span data-ttu-id="12a63-190">В порядке, toohappen модуль hello следует не зависят от вне hello модуля (папка hello, возвращает сжаты при импорте в Azure Automation) файлы или на любой уникальный реестр на узле, например были заданы параметрами hello установки продукта.</span><span class="sxs-lookup"><span data-stu-id="12a63-190">In order for that toohappen, hello module should not depend on any files outside hello module folder (hello folder that gets zipped up when importing into Azure Automation), or on any unique registry settings on a host, such as those set by hello install of a product.</span></span> <span data-ttu-id="12a63-191">При несоблюдении этой рекомендации, hello модуль не будет доступна в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="12a63-191">If this best practice is not followed, hello module will not be usable in Azure Automation.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="12a63-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="12a63-192">Next steps</span></span>

* <span data-ttu-id="12a63-193">tooget к работе с PowerShell модули Runbook рабочего процесса, в разделе [Мой первый runbook рабочего процесса PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="12a63-193">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="12a63-194">. в разделе toolearn Дополнительные сведения о создании модулей PowerShell [написание модуля Windows PowerShell](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="12a63-194">toolearn more about creating PowerShell Modules, see [Writing a Windows PowerShell Module](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span></span>

