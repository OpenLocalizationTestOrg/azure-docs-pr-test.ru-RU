---
title: "aaaCredential средств автоматизации Azure | Документы Microsoft"
description: "Ресурсы учетных данных в службе автоматизации Azure содержат учетные данные безопасности, которые могут быть tooresources используется tooauthenticate обращаются hello runbook или конфигурации DSC. В этой статье описывается toocreate активы учетных данных и использовать их в runbook или конфигурации DSC."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 3209bf73-c208-425e-82b6-df49860546dd
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/14/2017
ms.author: bwren
ms.openlocfilehash: 46f23a8f79d5863265af9cf84f6003e30f8e7d39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="credential-assets-in-azure-automation"></a>Ресурсы учетных данных в службе автоматизации Azure
В ресурсе-контейнере учетных данных службы автоматизации хранится объект [PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential), содержащий учетные данные безопасности, например имя пользователя и пароль. Конфигурации модулей Runbook и DSC могут использовать командлеты, которые принимают объект PSCredential для проверки подлинности, или они могут извлечь hello имя пользователя и пароль hello tooprovide toosome PSCredential объект приложения или службы, требующей проверки подлинности. Hello свойства учетных данных безопасно хранятся в службе автоматизации Azure и доступны в конфигурации DSC с hello или hello runbook [Get-AutomationPSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) действия.

> [!NOTE]
> Безопасные средства в службе автоматизации Azure включают учетные данные, сертификаты, подключения и зашифрованные переменные. Эти ресурсы шифруются и хранятся в hello автоматизации Azure, используя уникальный ключ, который создается для каждой учетной записи автоматизации. Ключ шифруется главным сертификатом и хранится в службе автоматизации Azure. Перед сохранением безопасного ресурса, hello ключ для учетной записи автоматизации hello расшифровывается с помощью шаблона сертификата hello и затем использовать tooencrypt hello активов.  

## <a name="windows-powershell-cmdlets"></a>Командлеты Windows PowerShell
командлеты Hello в следующей таблице hello, используемые toocreate ресурсов и управления ими автоматизации учетных данных с помощью Windows PowerShell.  Они поставляются как часть hello [модуля Azure PowerShell](/powershell/azure/overview) доступный для использования в Runbook автоматизации и конфигураций DSC.

| Командлеты | Описание |
|:--- |:--- |
| [Get-AzureAutomationCredential](/powershell/module/azure/get-azureautomationcredential?view=azuresmps-3.7.0) |Извлекает сведения о ресурсе учетных данных. Сами hello учетные данные можно получить только из **Get-AutomationPSCredential** действия. |
| [New-AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Создает новые учетные данные службы автоматизации. |
| [Remove- AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Удаляет учетные данные службы автоматизации. |
| [Set- AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Задает hello свойства существующей учетной записи автоматизации. |

## <a name="runbook-activities"></a>Действия Runbook
Hello действия в следующей таблице hello, используемые tooaccess учетные данные в книгу и конфигураций DSC.

| Действия | Описание |
|:--- |:--- |
| Get-AutomationPSCredential |Возвращает учетные данные toouse в runbook или конфигурации DSC. Возвращает объект [System.Management.Automation.PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) . |

> [!NOTE]
> Следует избегать использования переменных в hello — параметр Name командлета Get-AutomationPSCredential, так как это может усложнить обнаружение зависимостей между модулями Runbook или конфигураций DSC и учетных данных ресурсов во время разработки.
> 
> 

## <a name="creating-a-new-credential-asset"></a>Создание нового ресурса учетных данных

### <a name="toocreate-a-new-credential-asset-with-hello-azure-portal"></a>toocreate ресурс учетных данных с hello портал Azure
1. Из учетной записи автоматизации, нажмите кнопку hello **активы** hello часть tooopen **активы** колонку.
2. Нажмите кнопку hello **учетные данные** hello tooopen часть **учетные данные** колонку.
3. Нажмите кнопку **добавления учетных данных** hello верхней части колонки hello.
4. Заполните форму hello и нажмите кнопку **создать** toosave hello новые учетные данные.

### <a name="toocreate-a-new-credential-asset-with-windows-powershell"></a>toocreate ресурс учетных данных с помощью Windows PowerShell
Hello следующие примеры команд показывают, как toocreate новый автоматизации учетных данных. Объект PSCredential сначала создается с именем hello и пароля и затем использовать ресурс учетных данных toocreate hello. Кроме того, можно использовать hello **Get-Credential** toobe командлет запрос tootype имени и пароля.

    $user = "MyDomain\MyUser"
    $pw = ConvertTo-SecureString "PassWord!" -AsPlainText -Force
    $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $user, $pw
    New-AzureAutomationCredential -AutomationAccountName "MyAutomationAccount" -Name "MyCredential" -Value $cred

### <a name="toocreate-a-new-credential-asset-with-hello-azure-classic-portal"></a>toocreate ресурс учетных данных с hello классический портал Azure
1. Ваша учетная запись автоматизации щелкните **активы** hello верхней части окна hello.
2. Hello нижней части окна hello, нажмите кнопку **добавить параметр**.
3. Щелкните **Добавить учетные данные**.
4. В hello **тип учетных данных** раскрывающийся список, выберите **учетные данные PowerShell**.
5. Завершение мастера hello и нажмите кнопку hello флажок toosave hello новые учетные данные.

## <a name="using-a-powershell-credential"></a>Использование учетных данных PowerShell
Получение актива учетных данных в конфигурации DSC с hello или runbook **Get-AutomationPSCredential** действия. Оно возвращает [объект PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx), который можно использовать в действии или командлете, требующем параметр PSCredential. Можно также извлекать свойства hello объекта toouse hello учетных данных по отдельности. Hello объекта имеет свойство для hello имя пользователя и надежный пароль hello, или можно использовать hello **GetNetworkCredential** tooreturn метод [NetworkCredential](http://msdn.microsoft.com/library/system.net.networkcredential.aspx) объект, предоставляющий небезопасную версия hello пароль.

### <a name="textual-runbook-sample"></a>Пример текстового Runbook
Hello следующие примеры команд показывают, как toouse PowerShell учетные данные в книгу. В этом примере возвращаются учетные данные hello и его имя пользователя и пароль назначаются toovariables.

    $myCredential = Get-AutomationPSCredential -Name 'MyCredential'
    $userName = $myCredential.UserName
    $securePassword = $myCredential.Password
    $password = $myCredential.GetNetworkCredential().Password


### <a name="graphical-runbook-sample"></a>Пример графического Runbook
Добавить **Get-AutomationPSCredential** действия tooa графического модуля runbook, щелкнув hello учетных данных в области библиотеки hello графического редактора hello и выбрав **добавить toocanvas**.

![Добавить toocanvas учетных данных](media/automation-credentials/credential-add-canvas.png)

Hello следующем рисунке показан пример использования учетных данных в графический runbook.  В этом случае время проверки подлинности используется tooprovide ресурсов tooAzure runbook как описано в [проверки подлинности модулей Runbook с помощью учетной записи пользователя Azure AD](automation-create-aduser-account.md).  Первое действие Hello извлекает hello учетными данными, имеющими доступ toohello подписки Azure.  Hello **Add-AzureAccount** действия затем используется этой проверки подлинности tooprovide учетных данных для всех действий, которые идти после нее.  Здесь используется [конвейерная связь](automation-graphical-authoring-intro.md#links-and-workflow) , так как **Get-AutomationPSCredential** ожидает один объект.  

![Добавить toocanvas учетных данных](media/automation-credentials/get-credential.png)

## <a name="using-a-powershell-credential-in-dsc"></a>Использование учетных данных PowerShell в DSC
Хотя конфигурации DSC в службе автоматизации Azure могут ссылаться на ресурсы-контейнеры учетных данных с помощью командлета **Get-AutomationPSCredential**, при необходимости эти ресурсы-контейнеры можно передавать и в качестве параметров. Дополнительные сведения см. в статье [Компилирование конфигураций в Azure Automation DSC](automation-dsc-compile.md#credential-assets).

## <a name="next-steps"></a>Дальнейшие действия
* toolearn Дополнительные сведения о связи в графический разработки, в разделе [ссылки в графический разработки](automation-graphical-authoring-intro.md#links-and-workflow)
* toounderstand hello разными методами проверки подлинности с помощью автоматизации см. в разделе [безопасности автоматизации Azure](automation-security-overview.md)
* tooget к работе с графический Runbook в разделе [Мой первый графический runbook](automation-first-runbook-graphical.md)
* tooget к работе с PowerShell модули Runbook рабочего процесса, в разделе [Мой первый runbook рабочего процесса PowerShell](automation-first-runbook-textual.md) 

