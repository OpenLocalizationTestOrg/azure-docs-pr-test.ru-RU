---
title: "aaaConnection средств автоматизации Azure | Документы Microsoft"
description: "Ресурсы подключения в службе автоматизации Azure содержат hello сведения, необходимые tooconnect tooan внешней службе или приложению из модуля runbook или конфигурации DSC. В этой статье подробно описывается hello подключений и как toowork с ними в текстовых и графических разработки."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: f0239017-5c66-4165-8cca-5dcb249b8091
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/13/2017
ms.author: magoedte; bwren
ms.openlocfilehash: f0f6b9fb960789b34af7b60eb1069313fdcf071c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connection-assets-in-azure-automation"></a>Ресурсы подключений в службе автоматизации Azure

Ресурс подключения автоматизации содержит hello сведения, необходимые tooconnect tooan внешней службе или приложению из модуля runbook или конфигурации DSC. Это может включать сведения, необходимые для проверки подлинности, такие как имя пользователя и пароль в tooconnection сведения, такие как URL-адрес или порт. Hello значение подключения хранит все свойства hello для подключения конкретного приложения в одном ресурсе, в противоположность toocreating tooa несколько переменных. Hello пользователь может редактировать значения hello для подключения в одном месте и hello имя runbook tooa подключения или конфигурации DSC можно передать в один параметр. Здравствуйте свойства для соединения осуществляется в конфигурации DSC с hello или hello runbook **Get-AutomationConnection** действия.

При создании подключения необходимо указать его *тип*. Тип соединения Hello является шаблон, определяющий набор свойств. Hello подключение задает значения для каждого свойства, определенного в типе подключения. Типы подключений будут добавлены tooAzure автоматизации в модулях интеграции или создается hello [API автоматизации Azure](http://msdn.microsoft.com/library/azure/mt163818.aspx) Если модуль интеграции hello включает тип соединения и импортируется в вашей учетной записи автоматизации. В противном случае вам потребуется toocreate toospecify файл метаданных типа подключения автоматизации.  Дополнительные сведения по этому вопросу см. в статье о [модулях интеграции](automation-integration-modules.md).  

>[!NOTE] 
>Безопасные средства в службе автоматизации Azure включают учетные данные, сертификаты, подключения и зашифрованные переменные. Эти ресурсы шифруются и хранятся в hello автоматизации Azure, используя уникальный ключ, который создается для каждой учетной записи автоматизации. Ключ шифруется главным сертификатом и хранится в службе автоматизации Azure. Перед сохранением безопасного ресурса, hello ключ для учетной записи автоматизации hello расшифровывается с помощью шаблона сертификата hello и затем использовать tooencrypt hello активов.

## <a name="windows-powershell-cmdlets"></a>Командлеты Windows PowerShell

командлеты Hello в следующей таблице hello, используемые toocreate подключениях и управлении ими автоматизации с помощью Windows PowerShell. Они поставляются как часть hello [модуля Azure PowerShell](/powershell/azure/overview) доступный для использования в Runbook автоматизации и конфигураций DSC.

|Командлет|Описание|
|:---|:---|
|[Get-AzureRmAutomationConnection](/powershell/module/azurerm.automation/get-azurermautomationconnection)|Извлекает подключение. Содержит хэш-таблицу со значениями полей подключения hello hello.|
|[New-AzureRmAutomationConnection](/powershell/module/azurerm.automation/new-azurermautomationconnection)|Создает новое подключение.|
|[Remove-AzureRmAutomationConnection](/powershell/module/azurerm.automation/remove-azurermautomationconnection)|Удаляет существующее подключение.|
|[Set-AzureRmAutomationConnectionFieldValue](/powershell/module/azurerm.automation/set-azurermautomationconnectionfieldvalue)|Задает значение определенного поля для существующего подключения hello.|

## <a name="activities"></a>Действия

Hello действия в следующей таблице hello, используемые tooaccess подключения в runbook или конфигурации DSC.

|Действия|Описание|
|---|---|
|[Get-AutomationConnection](/powershell/module/azure/get-azureautomationconnection?view=azuresmps-3.7.0)|Возвращает toouse соединения. Возвращает хэш-таблицу с hello свойств соединения hello.|

>[!NOTE] 
>Следует избегать использования переменных с hello – имя параметра **Get - AutomationConnection** так, как это может усложнить обнаружение зависимостей между модулями Runbook или конфигураций DSC и ресурсы подключения во время разработки.

## <a name="creating-a-new-connection"></a>Создание нового подключения

### <a name="toocreate-a-new-connection-with-hello-azure-portal"></a>toocreate новое соединение с hello портал Azure

1. Из учетной записи автоматизации, нажмите кнопку hello **активы** hello часть tooopen **активы** колонку.
2. Щелкните hello **подключений** hello часть tooopen **подключений** колонку.
3. Нажмите кнопку **добавить подключение** hello верхней части колонки hello.
4. В hello **тип** раскрывающийся список, выберите hello тип подключения требуется toocreate. Hello формы будет представлять свойства hello для конкретного типа.
5. Заполните форму hello и нажмите кнопку **создать** toosave hello новое соединение.

### <a name="toocreate-a-new-connection-with-hello-azure-classic-portal"></a>toocreate новое соединение с hello классический портал Azure

1. Ваша учетная запись автоматизации щелкните **активы** hello верхней части окна hello.
2. Hello нижней части окна hello, нажмите кнопку **добавить параметр**.
3. Щелкните **Добавить подключение**.
4. В hello **тип подключения** раскрывающийся список, выберите hello тип подключения требуется toocreate.  Мастер Hello представит hello свойства для конкретного типа.
5. Завершение мастера hello и щелкните hello флажок toosave hello новое подключение.

### <a name="toocreate-a-new-connection-with-windows-powershell"></a>toocreate новое подключение с помощью Windows PowerShell

Создайте новое подключение с помощью Windows PowerShell с помощью hello [New AzureRmAutomationConnection](/powershell/module/azurerm.automation/new-azurermautomationconnection) командлета. Этот командлет имеет параметр с именем **ConnectionFieldValues** , ожидает [хэш-таблицу](http://technet.microsoft.com/library/hh847780.aspx) определения значений для каждого из свойств hello, определенные типом подключения hello.

Если вы знакомы с hello автоматизации [учетная запись запуска от имени](automation-sec-configure-azure-runas-account.md) hello участника-службы, с помощью модулей Runbook tooauthenticate hello сценарий PowerShell, как альтернативный toocreating hello hello запуска от имени учетной записи с портала hello Создает новый актив подключения, используя следующие примеры команд hello.  

    $ConnectionAssetName = "AzureRunAsConnection"
    $ConnectionFieldValues = @{"ApplicationId" = $Application.ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Cert.Thumbprint; "SubscriptionId" = $SubscriptionId}
    New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $AutomationAccountName -Name $ConnectionAssetName -ConnectionTypeName AzureServicePrincipal -ConnectionFieldValues $ConnectionFieldValues 

Являются соединения может toouse hello сценария toocreate hello активов, поскольку при создании учетной записи автоматизации, автоматически включает в себя несколько глобальных модулей по умолчанию, а также тип подключения hello **AzurServicePrincipal**toocreate hello **AzureRunAsConnection** активов соединения.  Это tookeep важно помнить, поскольку при попытке toocreate новую службу tooa tooconnect активов подключения или приложения с помощью метода проверки подлинности, отличный он завершится ошибкой, поскольку тип соединения hello уже не определен в вашей учетной записи автоматизации.  Дополнительные сведения о как toocreate собственный тип подключения для пользовательских или модуля из hello [коллекции PowerShell](https://www.powershellgallery.com), в разделе [модули интеграции](automation-integration-modules.md)
  
## <a name="using-a-connection-in-a-runbook-or-dsc-configuration"></a>Использование подключения в модуле Runbook или конфигурации DSC

Вернуть подключение в runbook или конфигурация DSC с hello **Get-AutomationConnection** командлета.  Нельзя использовать hello [Get AzureRmAutomationConnection](https://docs.microsoft.com/powershell/resourcemanager/azurerm.automation/v1.0.12/Get-AzureRmAutomationConnection?redirectedfrom=msdn) действия.  Это действие извлекает значения hello hello разных полей в подключении hello и возвращает их в виде [хэш-таблицу](http://go.microsoft.com/fwlink/?LinkID=324844) которой затем могут использоваться с hello соответствующими командами в hello runbook или конфигурации DSC.

### <a name="textual-runbook-sample"></a>Пример текстового Runbook

Hello следующие примеры команд показывают, как toouse hello учетная запись запуска от имени уже упоминалось ранее, tooauthenticate с ресурсами Azure Resource Manager в модуле runbook.  Он использует соединение hello активов, представляющий hello запуска от имени учетной записи, которая ссылается на hello участника службы на основе сертификата, не учетные данные.  

    $Conn = Get-AutomationConnection -Name AzureRunAsConnection 
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint 

### <a name="graphical-runbook-samples"></a>Графические примеры для модуля Runbook

Добавить **Get-AutomationConnection** действия tooa графический runbook щелкните правой кнопкой мыши в соединении hello hello библиотеки панели графического редактора hello и выбора **добавить toocanvas**.

![](media/automation-connections/connection-add-canvas.png)

Hello следующем рисунке показан пример использования подключения в графический runbook.  Это hello примера, показанного выше, для проверки подлинности с помощью hello запуска от имени учетной записи с текстовым runbook.  В этом примере используется hello **постоянное значение** набора данных для hello **получить подключение RunAs** действия, которое использует объект соединения для проверки подлинности.  Объект [связь с конвейером](automation-graphical-authoring-intro.md#links-and-workflow) используется здесь, поскольку набор параметров ServicePrincipalCertificate hello ожидает один объект.

![](media/automation-connections/automation-get-connection-object.png)

## <a name="next-steps"></a>Дальнейшие действия

- Просмотрите [ссылки в графический разработки](automation-graphical-authoring-intro.md#links-and-workflow) toounderstand направление hello toodirect и контроль логики в модулях Runbook.  

- toolearn Дополнительные сведения о автоматизации Azure использование модулей PowerShell и рекомендации для создания собственных toowork модули PowerShell в виде модули интеграции в службе автоматизации Azure в разделе [модули интеграции](automation-integration-modules.md).  
