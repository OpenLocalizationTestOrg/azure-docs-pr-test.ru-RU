---
title: "aaaStarting runbook в автоматизации Azure | Документы Microsoft"
description: "Обобщает hello различные методы, которые можно использовать toostart runbook в автоматизации Azure и предоставляет сведения об использовании обоих hello портал Azure и Windows PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6ee756b4-9200-4eb2-9bda-ec156853803b
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: e44bce5b56b8e803f9247fbb4f3d4db7ab35c913
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a>Запуск модуля Runbook в службе автоматизации Azure
в следующей таблице Hello помогают определить hello метод toostart runbook в автоматизации Azure, наиболее подходящий tooyour определенного сценария. Эта статья содержит сведения о запуске модуля runbook с hello портал Azure и Windows PowerShell. Подробные сведения на hello другие методы предоставляются в другую документацию, можно получить доступ из приведенные ниже ссылки hello.

| **МЕТОД** | **ХАРАКТЕРИСТИКИ** |
| --- | --- |
| [Портал Azure](#starting-a-runbook-with-the-azure-portal) |<li>Простейший способ с интерактивным пользовательским интерфейсом.<br> <li>Значения параметра простой tooprovide формы.<br> <li>Легко отслеживать состояние задания.<br> <li>Доступ с аутентификацией в Azure. |
| [Windows PowerShell](https://msdn.microsoft.com/library/dn690259.aspx) |<li>Вызов из командной строки с помощью командлетов Windows PowerShell.<br> <li>Может быть добавлено в автоматическое решение, состоящее из нескольких шагов.<br> <li>Запрос проходит проверку подлинности с помощью сертификата или по протоколу OAuth.<br> <li>Необходимо предоставить значения простых и сложных параметров.<br> <li>Отслеживание состояния задания.<br> <li>Клиент требуется toosupport командлеты PowerShell. |
| [API-интерфейс в службе автоматизации Azure](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li>Наиболее гибкий и наиболее сложный метод.<br> <li>Вызов из любого пользовательского кода, который может выполнять HTTP-запросы.<br> <li>Запрос проходит проверку подлинности с помощью сертификата или по протоколу OAuth.<br> <li>Необходимо предоставить значения простых и сложных параметров.<br> <li>Отслеживание состояния задания. |
| [Объекты Webhook](automation-webhooks.md) |<li>Запуск Runbook из одного HTTP-запроса.<br> <li>Проверка подлинности с помощью токена безопасности в URL-адресе.<br> <li>Клиент не может переопределять значения параметров, указанные при создании Webhook. Runbook можно определить один параметр, который содержит сведения о запросе HTTP hello.<br> <li>Состояние задания отсутствует возможность tootrack через URL-адрес веб-перехватчика. |
| [Ответ tooAzure предупреждения](../log-analytics/log-analytics-alerts.md) |<li>Запуск runbook в ответ tooAzure предупреждение.<br> <li>Настройка веб-перехватчика для runbook и связывать их tooalert.<br> <li>Проверка подлинности с помощью токена безопасности в URL-адресе. |
| [Расписание](automation-schedules.md) |<li>Автоматический запуск Runbook по ежечасному, ежедневному, еженедельному или ежемесячному расписанию.<br> <li>Управление расписанием с помощью портала Azure, командлетов PowerShell или API-интерфейса Azure.<br> <li>Укажите параметр toobe значения, используемые вместе с расписанием. |
| [Из другого модуля Runbook](automation-child-runbooks.md) |<li>Использование одного модуля Runbook в качестве процесса в другом модуле Runbook.<br> <li>Подходит для функций, используемых в нескольких модулях Runbook.<br> <li>Укажите runbook toochild значения параметра и использовать результаты в родительский модуль runbook. |

Hello следующем рисунке показан Подробное пошаговое описание жизненного цикла hello модуля Runbook. Он включает в себя различные способы запуска модуля runbook в автоматизации Azure, компонентов, необходимых для Runbook службы автоматизации Azure tooexecute гибридной рабочей ролью Runbook и взаимодействие между разными компонентами. toolearn о выполнении модулей автоматизации Runbook в центре обработки данных, см. слишком[гибридных рабочих ролей runbook](automation-hybrid-runbook-worker.md)

![Архитектура Runbook](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-hello-azure-portal"></a>Запуск модуля runbook с hello портал Azure
1. В hello портал Azure, выберите **автоматизации** и нажмите кнопку hello имя учетной записи автоматизации.
2. Выберите меню концентратора hello **Runbooks**.
3. На hello **Runbooks** колонке выберите runbook и нажмите кнопку **запустить**.
4. Если hello runbook имеет параметры, можно tooprovide запрашиваемые значения с текстовым полем для каждого параметра. Дополнительные сведения о параметрах см. в разделе [Параметры модуля Runbook](#Runbook-parameters) ниже.
5. На hello **задания** колонки, можно просмотреть состояние задания runbook hello hello.

## <a name="starting-a-runbook-with-windows-powershell"></a>Запуск модуля Runbook с помощью Windows PowerShell
Можно использовать hello [начала AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart runbook с помощью Windows PowerShell. Hello следующий пример кода запускает модуль runbook с именем Test-Runbook.

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

Возвращает AzureRmAutomationRunbook начала задания объекта, можно использовать tootrack его состояние после запуска hello runbook. Затем можно использовать этот объект задания с [Get AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine hello состояние задания hello и [Get AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget свои выходные данные. Hello, следующий пример кода запускает модуль runbook с именем Test-Runbook, Ожидание его завершения, а затем отображает выходные данные.

```
$runbookName = "Test-Runbook"
$ResourceGroup = "ResourceGroup01"
$AutomationAcct = "MyAutomationAccount"

$job = Start-AzureRmAutomationRunbook –AutomationAccountName $AutomationAcct -Name $runbookName -ResourceGroupName $ResourceGroup

$doLoop = $true
While ($doLoop) {
   $job = Get-AzureRmAutomationJob –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup
   $status = $job.Status
   $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped"))
}

Get-AzureRmAutomationJobOutput –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup –Stream Output
```

Если hello runbook требуются параметры, то необходимо указать их в виде [hashtable](http://technet.microsoft.com/library/hh847780.aspx) где ключ hello hello хэш-таблицы совпадает с именем hello и значением hello — значением параметра hello. Hello следующем примере показано, как toostart runbook с двумя строковыми параметрами с именем FirstName и LastName, целочисленным параметром repeatCount и логическим параметром show. Дополнительные сведения о параметрах см. в разделе [Параметры Runbook](#Runbook-parameters) ниже.

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a>Параметры модуля Runbook
При запуске модуля runbook из hello портала Azure или Windows PowerShell hello команда отправляется через веб-службы автоматизации Azure hello. Эта служба не поддерживает параметры со сложными типами данных. Если требуется tooprovide значение для сложного параметра, то следует вызвать его из другого модуля runbook как описано в [дочерние модули Runbook в автоматизации Azure](automation-child-runbooks.md).

Hello веб-служба автоматизации Azure предоставляет специальные функции для параметров с помощью определенных типов данных, как описано в следующих разделах hello.

### <a name="named-values"></a>Именованные значения
Если hello параметр имеет тип [object], то можно использовать hello после его список именованных значений toosend формат JSON: *{Name1: «Значение1», имя2: «Значение2», Имя3: значение «3»}*. Значения должны быть простого типа. Hello модуль runbook получит параметр hello как [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) со свойствами, соответствующими tooeach с именем value.

Рассмотрим следующий Тестовый модуль runbook, который принимает параметр с именем пользователя hello.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][object]$user
   )
    $userObject = $user | ConvertFrom-JSON
    if ($userObject.Show) {
        foreach ($i in 1..$userObject.RepeatCount) {
            $userObject.FirstName
            $userObject.LastName
        }
    }
}
```

Hello следующий текст может использоваться для параметра пользователя hello.

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

Это приводит к hello следующие выходные данные.

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a>Массивы
Если параметр hello представляет собой массив, например [array] или [string []], то можно использовать hello следующие toosend формат JSON его список значений: *[значение1, значение2, значение3]*. Значения должны быть простого типа.

Рассмотрим следующий Тестовый модуль runbook, который принимает параметр с именем hello *пользователя*.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][array]$user
   )
    if ($user[3]) {
        foreach ($i in 1..$user[2]) {
            $ user[0]
            $ user[1]
        }
    }
}
```

Hello следующий текст может использоваться для параметра пользователя hello.

```
["Joe","Smith",2,true]
```

Это приводит к hello следующие выходные данные.

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a>Учетные данные
Если тип данных параметра hello **PSCredential**, то можно указать имя hello объекта автоматизации Azure [актива учетных данных](automation-credentials.md). Hello модуль runbook извлечет hello учетные данные с именем hello.

Рассмотрим следующий Тестовый модуль runbook, который принимает параметр с именем учетных данных hello.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

Hello следующий текст можно использовать для параметра пользователя hello, при наличии актива учетных данных с именем *мои учетные данные*.

```
My Credential
```

Предполагается, что имя пользователя hello в учетных данных hello — *jsmith*, это приведет к hello следующие выходные данные.

```
jsmith
```

## <a name="next-steps"></a>Дальнейшие действия
* Архитектура Hello runbook в текущей статьи предоставляет высокоуровневый обзор модулей Runbook управление ресурсами в Azure и локальными с hello гибридной рабочей ролью Runbook.  toolearn о выполнении модулей автоматизации Runbook в центре обработки данных, см. слишком[гибридных рабочих ролей Runbook](automation-hybrid-runbook-worker.md).
* toolearn Дополнительные сведения о hello Создание toobe модульной модулей Runbook, использовать другие модули Runbook для конкретной или общие функции, см. слишком[дочерние модули Runbook](automation-child-runbooks.md).

