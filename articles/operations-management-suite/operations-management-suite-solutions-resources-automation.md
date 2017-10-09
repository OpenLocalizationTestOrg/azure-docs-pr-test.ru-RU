---
title: "ресурсы автоматизации aaaAzure решения OMS | Документы Microsoft"
description: "Как правило, решения в OMS включает модули Runbook в автоматизации Azure tooautomate процессов, таких как сбор и обработку данных мониторинга.  В этой статье описывается как tooinclude модулей Runbook и их связанные ресурсы в решении."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 5281462e-f480-4e5e-9c19-022f36dce76d
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 82a156f89bf77ce25e52e5e4596261ec07a24dae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-automation-resources-tooan-oms-management-solution-preview"></a>Добавление решение управления OMS tooan ресурсы службы автоматизации Azure (Предварительная версия)
> [!NOTE]
> Это предварительная документация для создания решений для управления в консоли OMS, которая доступна в данный момент в режиме предварительной версии. Ни одной схеме, описанной ниже — toochange субъекта.   


[Решения для управления в OMS](operations-management-suite-solutions.md) как правило, включают модули Runbook в автоматизации Azure tooautomate процессов, таких как сбор и обработку данных мониторинга.  В дополнение к этому toorunbooks, учетные записи автоматизации включает средства, такие как переменные и расписаний, которые поддерживают hello модулей Runbook используется в решении hello.  В этой статье описывается как tooinclude модулей Runbook и их связанные ресурсы в решении.

> [!NOTE]
> Hello примеры в этой статье с помощью параметров и переменные, которые либо обязательными или общие toomanagement решений и описано в [создание решений для управления в Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md) 


## <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается, что вы уже знакомы с hello следующую информацию.

- Как слишком[создать решение для управления](operations-management-suite-solutions-creating.md).
- Здравствуйте, структура [файл решения](operations-management-suite-solutions-solution-file.md).
- Как слишком[создании шаблонов диспетчера ресурсов](../azure-resource-manager/resource-group-authoring-templates.md)

## <a name="automation-account"></a>Учетная запись службы автоматизации
Все ресурсы в службе автоматизации Azure содержатся в [учетной записи службы автоматизации](../automation/automation-security-overview.md#automation-account-overview).  Как описано в [OMS рабочей области и учетной записи автоматизации](operations-management-suite-solutions.md#oms-workspace-and-automation-account) не включен в решение по управлению hello hello учетной записи автоматизации, но должна существовать до установки решения hello.  Если эти сведения недоступны, то произойдет сбой установки решения hello.

Hello имя каждого ресурса автоматизации содержит hello собственной учетной записи автоматизации.  Для этого в решении hello с hello **accountName** параметра как следующий пример runbook ресурса hello.

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a>Модули Runbook
Следует включить все модули Runbook, используемых решении hello в файле решения hello, чтобы они создаются при установке решения hello.  Не может содержать текст hello runbook hello в шаблоне hello, поэтому следует опубликовать hello runbook tooa общедоступное расположение которых может осуществляться любым пользователем, установка решения.

[Azure Automation runbook](../automation/automation-runbook-types.md) ресурсы имеют тип **Microsoft.Automation/automationAccounts/runbooks** и имеют следующие структуры hello. Сюда входят общие переменные и параметры, чтобы скопировать и вставить этот фрагмент кода в файл решения и измените имена параметров hello. 

    {
        "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
        "type": "Microsoft.Automation/automationAccounts/runbooks",
        "apiVersion": "[variables('AutomationApiVersion')]",
        "dependsOn": [
        ],
        "location": "[parameters('regionId')]",
        "tags": { },
        "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
                "uri": "[variables('Runbook').Uri]",
                "version": [variables('Runbook').Version]"
            }
        }
    }


в hello в следующей таблице описаны свойства Hello для модулей Runbook.

| Свойство | Описание |
|:--- |:--- |
| runbookType |Указывает типы hello hello runbook. <br><br> Script — сценарий PowerShell <br>PowerShell — рабочий процесс PowerShell <br> GraphPowerShell — графический модуль сценария PowerShell <br> GraphPowerShellWorkflow — графический модуль Runbook рабочего процесса PowerShell |
| logProgress |Указывает ли [записей хода выполнения](../automation/automation-runbook-output-and-messages.md) должно создаваться для hello runbook. |
| logVerbose |Указывает, является ли [подробные записи](../automation/automation-runbook-output-and-messages.md) должно создаваться для hello runbook. |
| Описание |Необязательное описание для hello runbook. |
| publishContentLink |Указывает содержимое hello hello runbook. <br><br>URI - Uri содержимого toohello hello runbook.  Это будет PS1-файл для модулей Runbook PowerShell и сценариев, а также файл экспортированного графического модуля Runbook для графического модуля Runbook.  <br> версия - версии hello runbook для собственных отслеживания. |


## <a name="automation-jobs"></a>Задания службы автоматизации
При запуске модуля Runbook в службе автоматизации Azure создается задание службы автоматизации.  Можно добавить runbook автоматизации задания tooyour решения tooautomatically начало ресурса, при установке решения по управлению hello.  Этот метод является типовыми toostart модулей Runbook, которые используются для начальной настройки решения hello.  Создание toostart runbook через регулярные интервалы [расписания](#schedules) и [расписания задания](#job-schedules)

Задание ресурсы имеют тип **Microsoft.Automation/automationAccounts/jobs** и имеют следующие структуры hello.  Сюда входят общие переменные и параметры, чтобы скопировать и вставить этот фрагмент кода в файл решения и измените имена параметров hello. 

    {
      "name": "[concat(parameters('accountName'), '/', parameters('Runbook').JobGuid)]",
      "type": "Microsoft.Automation/automationAccounts/jobs",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
      ],
      "tags": { },
      "properties": {
        "runbook": {
          "name": "[variables('Runbook').Name]"
        },
        "parameters": {
          "Parameter1": "[[variables('Runbook').Parameter1]",
          "Parameter2": "[[variables('Runbook').Parameter2]"
        }
      }
    }

в hello в следующей таблице описаны свойства Hello для автоматизации заданий.

| Свойство | Description (Описание) |
|:--- |:--- |
| runbook |Одно имя сущности с именем hello hello runbook toostart. |
| parameters |Сущность для каждого значения параметра, предусмотренного hello runbook. |

Задание Hello включает имя runbook hello и toobe значения любого параметра, отправляемых toohello runbook.  Задание Hello следует [зависят от](operations-management-suite-solutions-solution-file.md#resources) hello runbook, он начинается с момента hello runbook должен быть создан до задания hello.  При наличии нескольких модулей Runbook, которые нужно запустить, порядок их запуска можно определить, создав зависимость между заданием и другими заданиями, которые должны выполняться в первую очередь.

Имя ресурса задания Hello должен содержать идентификатор GUID, который обычно назначается один из параметров.  Дополнительные сведения о параметрах GUID см. в статье [Создание решений для управления в Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).  


## <a name="certificates"></a>Сертификаты
[Azure сертификаты автоматизации](../automation/automation-certificates.md) имеют тип **Microsoft.Automation/automationAccounts/certificates** и имеют следующие структуры hello. Сюда входят общие переменные и параметры, чтобы скопировать и вставить этот фрагмент кода в файл решения и измените имена параметров hello. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
      "type": "Microsoft.Automation/automationAccounts/certificates",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "base64Value": "[variables('Certificate').Base64Value]",
        "thumbprint": "[variables('Certificate').Thumbprint]"
      }
    }



в hello в следующей таблице описаны Hello свойств ресурсов сертификаты.

| Свойство | Описание |
|:--- |:--- |
| base64Value |Значение Base 64 для сертификата hello. |
| thumbprint |Отпечаток сертификата hello. |



## <a name="credentials"></a>Учетные данные
[Учетные данные Azure Automation](../automation/automation-credentials.md) имеют тип **Microsoft.Automation/automationAccounts/credentials** и имеют следующие структуры hello.  Сюда входят общие переменные и параметры, чтобы скопировать и вставить этот фрагмент кода в файл решения и измените имена параметров hello. 


    {
      "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
      "type": "Microsoft.Automation/automationAccounts/credentials",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "userName": "[parameters('credentialUsername')]",
        "password": "[parameters('credentialPassword')]"
      }
    }

в hello в следующей таблице описаны Hello свойства учетных данных ресурсов.

| Свойство | Description (Описание) |
|:--- |:--- |
| userName |Имя пользователя для учетных данных hello. |
| пароль |Пароль для учетных данных hello. |


## <a name="schedules"></a>Расписания
[Azure расписания автоматизации](../automation/automation-schedules.md) имеют тип **Microsoft.Automation/automationAccounts/schedules** и имеют следующие структуры hello hello. Сюда входят общие переменные и параметры, чтобы скопировать и вставить этот фрагмент кода в файл решения и измените имена параметров hello. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
      "type": "microsoft.automation/automationAccounts/schedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Schedule').Description]",
        "startTime": "[parameters('scheduleStartTime')]",
        "timeZone": "[parameters('scheduleTimeZone')]",
        "isEnabled": "[variables('Schedule').IsEnabled]",
        "interval": "[variables('Schedule').Interval]",
        "frequency": "[variables('Schedule').Frequency]"
      }
    }

в hello в следующей таблице описаны свойства Hello планирование ресурсов.

| Свойство | Description (Описание) |
|:--- |:--- |
| Описание |Необязательное описание для hello расписания. |
| startTime |Указывает hello время начала расписания в виде объекта DateTime. Можно указать строку, если преобразованное tooa действительное значение DateTime. |
| isEnabled |Указывает, включено ли расписание hello. |
| interval |Тип интервала для расписания hello Hello.<br><br>day<br>hour |
| frequency |Частоту, расписание hello должен срабатывать в число дней или часов. |

Расписания должны иметь время начала со значением больше hello текущее время.  Нельзя задавать это значение с переменной, поскольку невозможно узнать, когда это toobe будет установлен.

Используйте одну из hello, следующие две стратегии при использовании планирование ресурсов в решении.

- Используйте параметр для hello время начала расписания hello.  При установке решения hello, предложит tooprovide hello пользователем значение.  Если у вас есть несколько расписаний, для них можно использовать одно значение параметра.
- Создание расписания hello, с помощью runbook, который начинается после установки решения hello.  Эта функция удаляет требование hello hello пользователя toospecify время, но не может содержать расписания hello в вашем решении, поэтому он будет удален при удалении решения hello.


### <a name="job-schedules"></a>Расписания заданий
Ресурсы расписания заданий связывают модуль Runbook с расписанием.  Они имеют тип **Microsoft.Automation/automationAccounts/jobSchedules** и имеют следующие структуры hello hello.  Сюда входят общие переменные и параметры, чтобы скопировать и вставить этот фрагмент кода в файл решения и измените имена параметров hello. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
      "type": "microsoft.automation/automationAccounts/jobSchedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
        "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
      ],
      "tags": {
      },
      "properties": {
        "schedule": {
          "name": "[variables('Schedule').Name]"
        },
        "runbook": {
          "name": "[variables('Runbook').Name]"
        }
      }
    }


свойства Hello для расписания задания описаны в следующей таблице hello.

| Свойство | Описание |
|:--- |:--- |
| schedule name |Один **имя** сущность с именем hello hello расписания. |
| runbook name  |Один **имя** сущность с именем hello hello модуля runbook.  |



## <a name="variables"></a>Переменные
[Azure переменные автоматизации](../automation/automation-variables.md) имеют тип **Microsoft.Automation/automationAccounts/variables** и имеют следующие структуры hello.  Сюда входят общие переменные и параметры, чтобы скопировать и вставить этот фрагмент кода в файл решения и измените имена параметров hello.

    {
      "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
      "type": "microsoft.automation/automationAccounts/variables",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Variable').Description]",
        "isEncrypted": "[variables('Variable').Encrypted]",
        "type": "[variables('Variable').Type]",
        "value": "[variables('Variable').Value]"
      }
    }

в hello в следующей таблице описаны Hello свойств переменной ресурсов.

| Свойство | Description (Описание) |
|:--- |:--- |
| Описание | Необязательное описание для переменной hello. |
| isEncrypted | Указывает, нужно ли шифровать hello переменной. |
| type | Сейчас это свойство ни на что не влияет.  Тип данных Hello hello переменной определяется hello начальное значение. |
| value | Значение для переменной hello. |

> [!NOTE]
> Hello **тип** свойство в настоящее время не оказывает влияния на создание переменной hello.  Тип данных Hello для hello переменной определяется значение hello.  

Если задать начальное значение переменной hello hello, его необходимо настроить как hello правильный тип данных.  Hello в следующей таблице приводится hello различных типов данных допустимый и их синтаксис.  Обратите внимание, что значения в JSON ожидаемый tooalways заключаться в кавычки с специальные символы в кавычках hello.  Например, строковое значение может быть задано в кавычки строку hello (с помощью escape-символ hello (\\)) во время может быть задано числовое значение с одним набором квот.

| Тип данных | Описание | Пример | Разрешает слишком|
|:--|:--|:--|:--|
| string   | Заключает значение в две пары кавычек.  | "\"Hello world\"" | "Hello world" |
| numeric  | Числовое значение с одной парой кавычек.| "64" | 64 |
| Логическое  | Значение **true** или **false** в кавычках.  Обратите внимание, что это значение должно быть в нижнем регистре. | True | Да |
| Datetime | Сериализованное значение даты.<br>Командлет ConvertTo-Json hello в PowerShell toogenerate можно использовать это значение для определенной даты.<br>Пример: get-date "5/24/2017 13:14:57" \| ConvertTo-Json | "\\/Date(1495656897378)\\/" | 2017-05-24 13:14:57 |

## <a name="modules"></a>модули
Решения управления не обязательно toodefine [глобальных модулей](../automation/automation-integration-modules.md) используемых модулей Runbook, так как они всегда будут доступны в учетной записи автоматизации.  Вам нужен tooinclude ресурса для любого модуля, используемые модули Runbook.

[Модули интеграции](../automation/automation-integration-modules.md) имеют тип **Microsoft.Automation/automationAccounts/modules** и имеют следующие структуры hello.  Сюда входят общие переменные и параметры, чтобы скопировать и вставить этот фрагмент кода в файл решения и измените имена параметров hello.

    {
      "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
      "type": "Microsoft.Automation/automationAccounts/modules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "dependsOn": [
      ],
      "properties": {
        "contentLink": {
          "uri": "[variables('Module').Uri]"
        }
      }
    }


в hello в следующей таблице описаны свойства Hello модуля ресурсов.

| Свойство | Description (Описание) |
|:--- |:--- |
| contentLink |Указывает содержимое hello модуля "hello". <br><br>URI - содержимое toohello Uri модуля "hello".  Это будет PS1-файл для модулей Runbook PowerShell и сценариев, а также файл экспортированного графического модуля Runbook для графического модуля Runbook.  <br> версия - версия модуля "hello" для собственных отслеживания. |

Hello runbook должны зависеть от tooensure hello модуля ресурсов, которых он создан до hello runbook.

### <a name="updating-modules"></a>Обновление модулей
Если обновить решение управления, включающее runbook, использующий расписание, а hello новая версия решения имеет новый модуль, используемый этого модуля, hello runbook может использовать hello старая версия модуля "hello".  Следует включать следующие модули Runbook в вашем решении hello и создать toorun задания их перед другими модулями Runbook.  Это позволит гарантировать, что модули обновляются как обязательный перед hello загрузки модулей Runbook.

* [Обновление ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) проверит все модули hello использовать модули Runbook в вашем решении hello последнюю версию.  
* [ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) будет повторно зарегистрировать все ресурсы tooensure hello расписание, что модули Runbook hello связаны toothem с модулями последнюю hello используйте.




## <a name="sample"></a>Образец
Ниже приведен образец, включают решение, включающее hello следующие ресурсы:

- Модуль Runbook.  Это пример модуля Runbook, хранящийся в общедоступном репозитории GitHub.
- Задание службы автоматизации, начинающийся hello runbook после установки решения hello.
- Расписание и задание расписания toostart hello runbook через регулярные интервалы.
- Сертификат.
- Учетные данные.
- Переменная.
- Модуль.  Это hello [OMSIngestionAPI модуль](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) для записи данных tooLog Analytics. 

Здравствуйте, образец использует [параметры стандартное решение](operations-management-suite-solutions-solution-file.md#parameters) переменные, которые часто используются в решении, что отличие от значений toohardcoding в hello определения ресурсов.


    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "workspaceName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Log Analytics workspace."
          }
        },
        "accountName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Automation account."
          }
        },
        "workspaceregionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Log Analytics workspace."
          }
        },
        "regionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Automation account."
          }
        },
        "pricingTier": {
          "type": "string",
          "metadata": {
            "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account."
          }
        },
        "certificateBase64Value": {
          "type": "string",
          "metadata": {
            "Description": "Base 64 value for certificate."
          }
        },
        "certificateThumbprint": {
          "type": "securestring",
          "metadata": {
            "Description": "Thumbprint for certificate."
          }
        },
        "credentialUsername": {
          "type": "string",
          "metadata": {
            "Description": "Username for credential."
          }
        },
        "credentialPassword": {
          "type": "securestring",
          "metadata": {
            "Description": "Password for credential."
          }
        },
        "scheduleStartTime": {
          "type": "string",
          "metadata": {
            "Description": "Start time for shedule."
          }
        },
        "scheduleTimeZone": {
          "type": "string",
          "metadata": {
            "Description": "Time zone for schedule."
          }
        },
        "scheduleLinkGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello schedule link toorunbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello runbook job.",
            "control": "guid"
          }
        }
      },
      "variables": {
        "SolutionName": "MySolution",
        "SolutionVersion": "1.0",
        "SolutionPublisher": "Contoso",
        "ProductName": "SampleSolution",
    
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31",
    
        "Runbook": {
          "Name": "MyRunbook",
          "Description": "Sample runbook",
          "Type": "PowerShell",
          "Uri": "https://raw.githubusercontent.com/user/myrepo/master/samples/MyRunbook.ps1",
          "JobGuid": "[parameters('runbookJobGuid')]"
        },
    
        "Certificate": {
          "Name": "MyCertificate",
          "Base64Value": "[parameters('certificateBase64Value')]",
          "Thumbprint": "[parameters('certificateThumbprint')]"
        },
    
        "Credential": {
          "Name": "MyCredential",
          "UserName": "[parameters('credentialUsername')]",
          "Password": "[parameters('credentialPassword')]"
        },
    
        "Schedule": {
          "Name": "MySchedule",
          "Description": "Sample schedule",
          "IsEnabled": "true",
          "Interval": "1",
          "Frequency": "hour",
          "StartTime": "[parameters('scheduleStartTime')]",
          "TimeZone": "[parameters('scheduleTimeZone')]",
          "LinkGuid": "[parameters('scheduleLinkGuid')]"
        },
    
        "Variable": {
          "Name": "MyVariable",
          "Description": "Sample variable",
          "Encrypted": 0,
          "Type": "string",
          "Value": "'This is my string value.'"
        },
    
        "Module": {
          "Name": "OMSIngestionAPI",
          "Uri": "https://devopsgallerystorage.blob.core.windows.net/packages/omsingestionapi.1.3.0.nupkg"
        }
      },
      "resources": [
        {
          "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
          "location": "[parameters('workspaceRegionId')]",
          "tags": { },
          "type": "Microsoft.OperationsManagement/solutions",
          "apiVersion": "[variables('LogAnalyticsApiVersion')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
            "referencedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
            ],
            "containedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]"
            ]
          },
          "plan": {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
            "Version": "[variables('SolutionVersion')]",
            "product": "[variables('ProductName')]",
            "publisher": "[variables('SolutionPublisher')]",
            "promotionCode": ""
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
          "type": "Microsoft.Automation/automationAccounts/runbooks",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "location": "[parameters('regionId')]",
          "tags": { },
          "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
              "uri": "[variables('Runbook').Uri]",
              "version": "1.0.0.0"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').JobGuid)]",
          "type": "Microsoft.Automation/automationAccounts/jobs",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
          ],
          "tags": { },
          "properties": {
            "runbook": {
              "name": "[variables('Runbook').Name]"
            },
            "parameters": {
              "targetSubscriptionId": "[subscription().subscriptionId]",
              "resourcegroup": "[resourceGroup().name]",
              "automationaccount": "[parameters('accountName')]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
          "type": "Microsoft.Automation/automationAccounts/certificates",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "Base64Value": "[variables('Certificate').Base64Value]",
            "Thumbprint": "[variables('Certificate').Thumbprint]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
          "type": "Microsoft.Automation/automationAccounts/credentials",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "userName": "[variables('Credential').UserName]",
            "password": "[variables('Credential').Password]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
          "type": "microsoft.automation/automationAccounts/schedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Schedule').Description]",
            "startTime": "[variables('Schedule').StartTime]",
            "timeZone": "[variables('Schedule').TimeZone]",
            "isEnabled": "[variables('Schedule').IsEnabled]",
            "interval": "[variables('Schedule').Interval]",
            "frequency": "[variables('Schedule').Frequency]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
          "type": "microsoft.automation/automationAccounts/jobSchedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
          ],
          "tags": {
          },
          "properties": {
            "schedule": {
              "name": "[variables('Schedule').Name]"
            },
            "runbook": {
              "name": "[variables('Runbook').Name]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
          "type": "microsoft.automation/automationAccounts/variables",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Variable').Description]",
            "isEncrypted": "[variables('Variable').Encrypted]",
            "type": "[variables('Variable').Type]",
            "value": "[variables('Variable').Value]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
          "type": "Microsoft.Automation/automationAccounts/modules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "properties": {
            "contentLink": {
              "uri": "[variables('Module').Uri]"
            }
          }
        }
    
      ],
      "outputs": { }
    }




## <a name="next-steps"></a>Дальнейшие действия
* [Добавление решения tooyour представление](operations-management-suite-solutions-resources-views.md) toovisualize собранных данных.
