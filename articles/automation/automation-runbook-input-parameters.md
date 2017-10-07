---
title: "aaaRunbook входных параметров | Документы Microsoft"
description: "Входные параметры Runbook повысить гибкость hello модулей Runbook, позволяя toopass данных tooa runbook при его запуске. В этой статье описаны различные сценарии использования входных параметров в модулях Runbook."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 4d3dff2c-1f55-498d-9a0e-eee497e5bedb
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: sngun
ms.openlocfilehash: f3abaf92382e7d41019616bafb14af23cf98dd9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-input-parameters"></a>Входные параметры Runbook
Входные параметры Runbook повысить гибкость hello модулей Runbook, позволяя tooit toopass данных при его запуске. Параметры Hello позволяют toobe действия runbook hello, предназначенные для конкретных сценариях и средах. В этой статье подробно описаны различные сценарии использования входных параметров в модулях Runbook.

## <a name="configure-input-parameters"></a>Настройка входных параметров
Входные параметры настраиваются в модулях Runbook PowerShell рабочих процессов PowerShell и в графических модулях Runbook. Runbook может использовать несколько параметров с разными типами данных или вообще не использовать параметры. Входные параметры могут быть обязательными или необязательными. Необязательным параметрам можно назначать значения по умолчанию. Можно назначить значения toohello входных параметров для модуля runbook при запуске через один из доступных методов hello. Это может быть запуск runbook из hello портал или веб-службы. Модуль можно также запустить как дочерний модуль Runbook, который вызывается с помощью встроенного вызова в другом Runbook.

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a>Настройка входных параметров в модулях Runbook PowerShell и рабочих процессов PowerShell
PowerShell и [модулях Runbook рабочего процесса PowerShell](automation-first-runbook-textual.md) в службе автоматизации Azure поддерживают входных параметров, определенных с помощью hello следующие атрибуты.  

| **Свойство** | **Описание** |
|:--- |:--- |
| Тип |Обязательный элемент. Hello предполагаемый тип данных для значения параметра hello. Допускаются любые типы .NET. |
| Имя |Обязательный элемент. Имя параметра hello Hello. Это должно быть уникальным в пределах hello runbook и может содержать только буквы, цифры или символы подчеркивания. Оно должно начинаться с буквы. |
| Обязательно |необязательный параметр. Указывает, должно быть указано значение для параметра hello. Если это значение слишком**$true**, то при запуске hello runbook должно быть указано значение. Если это значение слишком**$false**, а затем значение является необязательным. |
| Значение по умолчанию |необязательный параметр.  Задает значение, которое будет использоваться для параметра hello, если значение не передается при запуске hello runbook. Значение по умолчанию можно задать для любого параметра и автоматически внесет hello параметр необязательным независимо от hello обязательный параметр. |

Наряду с перечисленными здесь входными параметрами Windows PowerShell поддерживает дополнительные атрибуты входных параметров, например проверки, псевдонимы наборы параметров. Тем не менее службы автоматизации Azure в настоящее время поддерживает только hello входные параметры, приведенные выше.

Определение параметров в модулях Runbook рабочего процесса PowerShell имеет hello, следуя общую форму, где несколько параметров разделяются запятыми.

   ```
     Param
     (
         [Parameter (Mandatory= $true/$false)]
         [Type] Name1 = <Default value>,

         [Parameter (Mandatory= $true/$false)]
         [Type] Name2 = <Default value>
     )
   ```

> [!NOTE]
> При определении параметров, если не указать hello **обязательные** атрибута, то по умолчанию hello параметр считается необязательным. Кроме того, если задано значение по умолчанию для параметра в модулях Runbook рабочего процесса PowerShell, они рассматриваются в PowerShell как необязательный параметр, независимо от того, hello **обязательные** значение атрибута.
> 
> 

Например настроим hello входные параметры для runbook рабочего процесса PowerShell, который выводит сведения о виртуальных машин одной виртуальной Машины или всех виртуальных машин в группе ресурсов. Этот runbook имеет два параметра, как показано на следующий снимок экрана приветствия: hello имя виртуальной машины и имя группы ресурсов hello hello.

![Рабочий процесс PowerShell службы автоматизации](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

В этом определении параметра hello параметры **$VMName** и **$resourceGroupName** параметров простого строкового типа. Однако модули Runbook PowerShell и рабочих процессов PowerShell поддерживают все простые и сложные типы, например **object** или **PSCredential**, для входных параметров.

Если runbook имеет входной параметр типа объекта, затем с помощью PowerShell хэш-таблицы (имя, значение) пар toopass в значении. Например, если имеется следующий параметр в модуле runbook hello:

     [Parameter (Mandatory = $true)]
     [object] $FullName

Затем можно передать следующую параметром toohello значение hello:

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a>Настройка входных параметров в графических модулях Runbook
слишком[настроить графический runbook](automation-first-runbook-graphical.md) с входными параметрами, создадим графический модуль runbook, который выводит сведения о виртуальных машинах, либо одной виртуальной Машины или всех виртуальных машин в группе ресурсов. Настройка модуля состоит из двух основных операций, как описано ниже.

[**Проверки подлинности модулей Runbook в учетной записи запуска от имени Azure** ](automation-sec-configure-azure-runas-account.md) tooauthenticate с Azure.

[**Get-AzureRmVm** ](https://msdn.microsoft.com/library/mt603718.aspx) tooget hello свойства виртуальных машин.

Можно использовать hello [ **Write-Output** ](https://technet.microsoft.com/library/hh849921.aspx) действия toooutput приветствия имен виртуальных машин. Здравствуйте, действие **Get AzureRmVm** принимает два параметра hello **имя виртуальной машины** и hello **имя группы ресурсов**. Поскольку эти параметры могут потребовать различных значений каждый раз при запуске hello runbook, можно добавить runbook tooyour входных параметров. Ниже приведены hello действия tooadd входных параметров.

1. Выберите hello графический runbook из hello **Runbooks** колонку и нажмите кнопку [ **изменить** ](automation-graphical-authoring-intro.md) его.
2. Из редактора hello runbook, нажмите кнопку **ввод и вывод** tooopen hello **ввод и вывод** колонку.
   
    ![Графический модуль Runbook службы автоматизации](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. Hello **ввод и вывод** колонке отображается список входных параметров, которые определены для hello runbook. В этой колонке можно добавить новый входной параметр или изменить конфигурацию hello существующего входного параметра. Щелкните tooadd новый параметр для hello runbook **добавить входные данные** tooopen hello **входной параметр модуля Runbook** колонку. Нет можно настроить следующие параметры hello:
   
   | **Свойство** | **Описание** |
   |:--- |:--- |
   | Имя |Обязательный элемент.  Имя параметра hello Hello. Это должно быть уникальным в пределах hello runbook и может содержать только буквы, цифры или символы подчеркивания. Оно должно начинаться с буквы. |
   | Описание |необязательный параметр. Описание цели hello входного параметра. |
   | Тип |необязательный параметр. Тип данных Hello, которая ожидается для значения параметра hello. Поддерживаются параметры **строкового**, **логического**, **объектного** типа, а также типа **Int32**, **Int64**, **DateTime** и типа **десятичного** числа. Если тип данных не выбран, то по умолчанию слишком**строка**. |
   | Обязательно |необязательный параметр. Указывает, должно быть указано значение для параметра hello. При выборе **Да**, то при запуске hello runbook должно быть указано значение. При выборе **не**, а затем значение не является обязательным при запуске модуля hello и может быть установлено значение по умолчанию. |
   | По умолчанию |необязательный параметр. Задает значение, которое будет использоваться для параметра hello, если значение не передается при запуске hello runbook. Для необязательного параметра можно задать значение по умолчанию. Выберите значение по умолчанию tooset **настраиваемый**. Это значение используется в том случае, если не задано другое значение, при запуске hello runbook. Выберите **нет** Если вы не хотите tooprovide любое значение по умолчанию. |
   
    ![Добавление новых входных данных](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. Создайте два параметра с hello следующие свойства, которые будут использоваться hello **Get AzureRmVm** действия:
   
   * **Параметр 1:**
     
     * Имя — VMName.
     * Тип: строчный.
     * Необязательный параметр.
   * **Параметр 2:**
     
     * Имя — resourceGroupName.
     * Тип: строчный.
     * Необязательный параметр.
     * Настраиваемое значение по умолчанию.
     * Значение по умолчанию — \<имя группы ресурсов hello, содержащем виртуальные машины hello >
5. После добавления параметров приветствия щелкните **ОК**.  Теперь их можно просмотреть в hello **ввода и вывода колонке**. Нажмите кнопку **ОК** еще раз, а затем — **Сохранить** и **Опубликовать**, чтобы сохранить параметры и опубликовать модуль Runbook.

## <a name="assign-values-tooinput-parameters-in-runbooks"></a>Назначить значения параметров tooinput в модулях Runbook
Можно передавать значения параметров tooinput в Runbook в hello следующие сценарии.

### <a name="start-a-runbook-and-assign-parameters"></a>Запуск Runbook и назначение параметров
Runbook можно запустить различными способами: через портал Azure, веб-перехватчика, с помощью командлетов PowerShell, с помощью API-интерфейса REST hello или hello SDK hello. Ниже рассмотрены различные методы запуска модуля Runbook и назначения параметров.

#### <a name="start-a-published-runbook-by-using-hello-azure-portal-and-assign-parameters"></a>Запуск опубликованном модуле runbook с помощью портала Azure hello и назначение параметров
Когда вы [запустить hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **запустить Runbook** открывает колонку и вы можете настроить значения для параметров hello, которые вы только что создали.

![Запустить с помощью портала hello](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

Hello метку под hello поля ввода вы увидите hello атрибуты, которые были установлены для параметра hello. Атрибуты являются обязательными или необязательными и содержат тип и значение по умолчанию. Hello справки всплывающей Далее toohello имени параметра вы увидите все hello ключевые сведения, необходимые toomake решения о входных значениях параметров. Эти сведения указывают, является параметр обязательным или нет. Она также включает hello тип и значение по умолчанию (если таковые имеются) и другие полезные примечания.

![Всплывающая справка](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> Параметры строкового типа поддерживают **пустые** строковые значения.  Ввод **[EmptyString]** в входной параметр hello поле будет передать параметр toohello пустая строка. Параметры строкового типа не поддерживают передачу значений **NULL** . Если не передать любое значение toohello строковый параметр, затем PowerShell интерпретирует его как допускающий значения null.
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a>Запуск опубликованного модуля Runbook с помощью командлетов PowerShell и назначение параметров
* **Командлеты Azure Resource Manager**. Модуль Runbook службы автоматизации, созданный в группе ресурсов, можно запустить с помощью командлета [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).
  
  **Пример**
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* **Командлеты для управления службами Azure.** Модуль Runbook службы автоматизации, созданный в группе ресурсов по умолчанию, можно запустить с помощью командлета [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).
  
  **Пример**
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> При запуске модуля runbook с помощью командлетов PowerShell, параметр по умолчанию, **MicrosoftApplicationManagementStartedBy** создана с использованием hello **PowerShell**. Этот параметр можно просмотреть в hello **сведения о задании** колонку.  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a>Запуск Runbook с использованием пакета SDK и назначение параметров
* **Метод Azure диспетчера ресурсов:** runbook можно запустить с помощью hello SDK от языка программирования. Ниже приведен фрагмент кода C# для запуска модуля Runbook в вашей учетной записи службы автоматизации. Вы можете просмотреть все код hello в нашем [репозитории GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).  
  
  ```
   public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
      {
        var response = AutomationClient.Jobs.Create(resourceGroupName, automationAccount, new JobCreateParameters
         {
            Properties = new JobCreateProperties
             {
                Runbook = new RunbookAssociationProperty
                 {
                   Name = runbookName
                 },
                   Parameters = parameters
             }
         });
      return response.Job;
      }
  ```
* **Метод Azure управления службами:** runbook можно запустить с помощью hello SDK от языка программирования. Ниже приведен фрагмент кода C# для запуска модуля Runbook в вашей учетной записи службы автоматизации. Вы можете просмотреть все код hello в нашем [репозитории GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).
  
  ```      
  public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
    {
      var response = AutomationClient.Jobs.Create(automationAccount, new JobCreateParameters
    {
      Properties = new JobCreateProperties
         {
           Runbook = new RunbookAssociationProperty
         {
           Name = runbookName
              },
                Parameters = parameters
              }
       });
      return response.Job;
    }
  ```
  
  toostart этот метод создания hello toostore словарь параметров runbook **VMName** и **resourceGroupName**и их значения. Затем запустите hello runbook. Ниже приведен hello фрагмент кода C# для вызова метода hello, определенный выше.
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters toohello dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call hello StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-hello-rest-api-and-assign-parameters"></a>Запустить модуль runbook с помощью API-интерфейса REST hello и назначение параметров
Задание runbook может быть создан и работы с hello Azure Automation REST API с помощью hello **ПОМЕСТИТЬ** метод с hello следующий URI запроса.

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

В URI запроса hello замените hello следующие параметры:

* **subscription-id** — идентификатором своей подписки Azure.  
* **Имя облачной службы:** имя hello hello облачной службы toowhich hello запроса должно быть отправлено.  
* **Automation-account-name:** hello вашей учетной записи автоматизации, размещенному в hello имя облачной службы.  
* **Идентификатор задания:** hello GUID для задания hello. Идентификаторы GUID в PowerShell могут быть созданы с помощью hello **[GUID]::NewGuid(). ToString()** команды.

В порядке toopass параметры toohello runbook задания используйте текст запроса hello. Он принимает следующие два свойства, представленные в формате JSON hello:

* **Runbook Name** — обязательный параметр. Hello имя hello runbook toostart задания hello.  
* **Runbook Parameters** — необязательный параметр. Словарь список параметров hello в (имя, значение) формате, где имя должно быть строкового типа, а значение может быть любым допустимым значением JSON.

Если требуется toostart hello **Get AzureVMTextual** runbook, который был создан ранее с **VMName** и **resourceGroupName** как параметры, используйте следующий формат JSON hello для hello текст запроса.

   ```
    {
      "properties":{
        "runbook":{
        "name":"Get-AzureVMTextual"},
      "parameters":{
         "VMName":"WSVMClassic",
         "resourceGroupName":”WSCS1”}
        }
    }
   ```

Код состояния HTTP 201 возвращается в том случае, если задание hello успешно создан. Дополнительные сведения о hello текст ответа и заголовки ответов см. в статье toohello о том, как слишком[создать задание runbook с помощью API-интерфейса REST hello.](https://msdn.microsoft.com/library/azure/mt163849.aspx)

### <a name="test-a-runbook-and-assign-parameters"></a>Тестирование Runbook и назначение параметров
При вы [теста hello черновик runbook](automation-testing-runbook.md) с помощью параметра тестирования hello hello **тестирования** открывает колонку и вы можете настроить значения для параметров hello, которые вы только что создали.

![Тестирование и назначение параметров](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-tooa-runbook-and-assign-parameters"></a>Связать runbook tooa расписание и параметры назначить
Вы можете [связать расписание](automation-schedules.md) tooyour runbook, так что runbook hello запускается в определенное время. При создании расписания hello и hello runbook будет использовать эти значения при запуске по расписанию hello, назначьте входных параметров. Не удается сохранить расписание hello, пока не будут предоставлены значения всех обязательных параметров.

![Создание расписания и назначение параметров](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a>Создание объекта Webhook для модуля Runbook и назначение параметров
Для модуля Runbook можно создать объект [Webhook](automation-webhooks.md) и настроить входные параметры. Не удается сохранить веб-перехватчика hello, пока не будут предоставлены значения всех обязательных параметров.

![Создание Webhook и назначение параметров](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

При выполнении модуля runbook с помощью веб-перехватчика hello предопределенные входной параметр  **[Webhookdata](automation-webhooks.md#details-of-a-webhook)**  отправляется вместе с hello входные параметры, которые были определены. Можно щелкнуть tooexpand hello **WebhookData** параметр для получения дополнительных сведений.

![Параметр WebhookData](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о входных и выходных данных Runbook см. в записи блога [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/) (Служба автоматизации Azure. Входные и выходные данные Runbook. Вложенные модули Runbook).
* Дополнительные сведения о различных способов toostart runbook см. в разделе [запуск runbook](automation-starting-a-runbook.md).
* tooedit текстовое runbook, см. слишком[редактирование текстовое runbooks](automation-edit-textual-runbook.md).
* слишком ссылаться tooedit графический runbook[графический разработки в Azure Automation](automation-graphical-authoring-intro.md).

