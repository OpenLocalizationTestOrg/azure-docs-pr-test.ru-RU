---
title: "aaaCreating решения для управления в Operations Management Suite (OMS) | Документы Microsoft"
description: "Решения для управления расширить функциональность hello Operations Management Suite (OMS), предоставляя сценариев пакете управления, клиентам можно добавить tootheir рабочей области OMS.  Эта статья содержит сведения по созданию toobe решений управления используется в вашей рабочей среде или сделаны доступными tooyour клиентов."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/30/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f408df1b21f519fd1eb2cbeb19cca18f6c4161f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a>Создание файла решения по управлению в Operations Management Suite (OMS) (предварительная версия)
> [!NOTE]
> Это предварительная документация для создания решений для управления в консоли OMS, которая доступна в данный момент в режиме предварительной версии. Ни одной схеме, описанной ниже — toochange субъекта.  

Решения по управлению в Operations Management Suite (OMS) реализованы в виде [шаблонов Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md).  Основная задача Hello при изучении способ обучения tooauthor решения для управления как слишком[создания шаблона](../azure-resource-manager/resource-group-authoring-templates.md).  Эта статья содержит уникальные сведения шаблонов, используемых решениями и каким образом ресурсы tooconfigure стандартного решения.


## <a name="tools"></a>Средства

Можно использовать любой текстовый редактор toowork файлы решений, но рекомендуется использование возможностей hello, представлены в Visual Studio или кода Visual Studio, как описано в следующих статей hello.

- [Создание и развертывание групп ресурсов Azure с помощью Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [Работа с шаблонами Azure Resource Manager в Visual Studio Code](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a>structure
Базовая структура файла решения управления Hello Здравствуйте, таким же, как [шаблона диспетчера ресурсов](../azure-resource-manager/resource-group-authoring-templates.md#template-format) которой выглядит следующим образом.  В следующих разделах hello описаны элементы верхнего уровня hello и и их содержимое в решении.  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a>Параметры
[Параметры](../azure-resource-manager/resource-group-authoring-templates.md#parameters) являются значениями, которые требуют от пользователя hello при установке решения по управлению hello.  Существуют стандартные параметры для всех решений. При необходимости можно добавить дополнительные параметры для конкретного решения.  Как пользователи будут указывать значения параметров при установке решения будет зависеть от определенного параметра hello и установка решения hello.

Если пользователь устанавливает решение управления через hello [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) или [быстрый запуск Azure шаблоны](operations-management-suite-solutions.md#finding-and-installing-management-solutions) они являются запрашиваемые tooselect [OMS рабочей области и учетной записи автоматизации ](operations-management-suite-solutions.md#oms-workspace-and-automation-account).  Это используется toopopulate hello значения каждого из стандартных параметров hello.  Hello пользователю не предлагается toodirectly указать значения для стандартных параметров hello, но они запрашиваемые tooprovide значения для всех дополнительных параметров.

Когда hello пользователь устанавливает решение [другой метод](operations-management-suite-solutions.md#finding-and-installing-management-solutions), они должны предоставить значение для всех стандартных параметров и все дополнительные параметры.

Ниже приведен пример параметра.  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

Привет, в следующей таблице описываются атрибуты hello параметра.

| Атрибут | Description (Описание) |
|:--- |:--- |
| type |Тип данных параметра hello. Hello управления вводом, отображаемый для пользователя hello зависит от типа данных hello.<br><br>bool — раскрывающийся список<br>string — текстовое поле<br>int — текстовое поле<br>securestring — поле для ввода пароля<br> |
| category |Необязательный категорию параметра hello.  Параметры в одной категории группируются hello. |
| control |Дополнительная функция для строковых параметров.<br><br>datetime — отображается элемент управления для даты и времени.<br>Идентификатор GUID - значение идентификатора Guid формируется автоматически и не отображается параметр hello. |
| Описание |Необязательное описание для параметра hello.  Отображаются сведения всплывающей Далее toohello параметр. |

### <a name="standard-parameters"></a>Стандартные параметры
Hello следующей таблице перечислены стандартные параметры hello для всех решений управления.  Эти значения будут заполнены пользователем hello вместо запроса их при установке решения на основе шаблонов hello Azure Marketplace или краткое руководство.  необходимо указать значения для них Hello пользователя, если hello решение устанавливается с помощью другого метода.

> [!NOTE]
> пользовательский интерфейс Hello в шаблонах Azure Marketplace и примеры использования hello ожидает hello имена параметров в таблице hello.  Если вы используете разные имена параметров затем hello пользователя будет запрашиваться их и они будут заполнены автоматически.
>
>

| Параметр | Тип | Description (Описание) |
|:--- |:--- |:--- |
| accountName |строка |Учетная запись службы автоматизации Azure. |
| pricingTier |string |Ценовая категория рабочей области Log Analytics и учетной записи службы автоматизации Azure. |
| regionId |string |Область hello учетной записи службы автоматизации Azure. |
| solutionName |string |Имя решения hello.  При развертывании решения через примеры использования шаблонов, то следует определить имя_решения как параметр, можно определить строку, вместо необходимости toospecify пользователя hello один. |
| workspaceName |строка |Имя рабочей области Log Analytics. |
| workspaceRegionId |string |Области рабочей области аналитики журналов hello. |


Ниже приведен структуры hello hello стандартных параметров, которые можно скопировать и вставить в файл решения.  

    "parameters": {
        "workspaceName": {
            "type": "string",
            "metadata": {
                "description": "A valid Log Analytics workspace name"
            }
        },
        "accountName": {
               "type": "string",
               "metadata": {
                   "description": "A valid Azure Automation account name"
               }
        },
        "workspaceRegionId": {
               "type": "string",
               "metadata": {
                   "description": "Region of hello Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of hello Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


Ссылки tooparameter значения в других элементах hello решения с использованием синтаксиса hello **параметры ("имя параметра")**.  Например, tooaccess Здравствуйте имя рабочей области, можно использовать **parameters('workspaceName')**

## <a name="variables"></a>Переменные
[Переменные](../azure-resource-manager/resource-group-authoring-templates.md#variables) — это значения, которые будут использоваться в hello остальной части решения по управлению hello.  Эти значения не предоставляется toohello пользователь, устанавливающий hello решения.  Они являются предполагаемого tooprovide hello автору, с одного места, где ими значения, которые могут использоваться несколько раз на протяжении hello решения. Решения определенных tooyour значения должны быть помещены в переменные как противоположность toohard кодировать их в hello **ресурсов** элемента.  Это повышает удобочитаемость кода hello и предоставляет tooeasily изменения этих значений в более поздних версиях.

Ниже приведен пример элемента **variables** с типичные параметрами, используемыми в решениях.

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

Ссылки toovariable значений с помощью решения hello синтаксису hello **переменных ("имя переменной")**.  Например, tooaccess Здравствуйте имя_решения переменной, следует использовать **variables('SolutionName')**.

Кроме того, можно определить сложные переменные как несколько наборов значений.  Это особенно удобно в решениях по управлению, где для разных типов ресурсов определяется несколько свойств.  Например вы измените показанный выше toohello следующие переменные решения hello.

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

В этом случае ссылки toovariable значений с помощью решения hello синтаксису hello **variables('variable name').property**.  Например, tooaccess Здравствуйте переменной имя решения, следует использовать **variables('Solution'). Имя**.

## <a name="resources"></a>Ресурсы
[Ресурсы](../azure-resource-manager/resource-group-authoring-templates.md#resources) определить hello различных ресурсов, которые будут устанавливать и настраивать решения по управлению.  Это будет наибольшее hello и самые сложные части шаблона hello.  Можно получить структуру hello и полное описание элементов ресурсов в [шаблоны разработки Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md#resources).  В других статьях этой документации описаны различные ресурсы, которые обычно определяются. 


### <a name="dependencies"></a>Зависимости
Hello **dependsOn** указывает элементы [зависимостей](../azure-resource-manager/resource-group-define-dependencies.md) на другой ресурс.  При установке решения hello ресурса не создается, пока все его зависимости были созданы.  Например, при установке решение может [запустить модуль Runbook](operations-management-suite-solutions-resources-automation.md#runbooks) с помощью [ресурса задания](operations-management-suite-solutions-resources-automation.md#automation-jobs).  ресурс Hello заданий будет зависеть от hello runbook ресурсов toomake том, что для этого модуля hello создается перед созданием задания hello.

### <a name="oms-workspace-and-automation-account"></a>Рабочая область OMS и учетная запись службы автоматизации
Решения управления требуют [рабочей области OMS](../log-analytics/log-analytics-manage-access.md) toocontain представления и [учетной записи автоматизации](../automation/automation-security-overview.md#automation-account-overview) toocontain модулей Runbook и ресурсы, связанные с.  Они должны быть доступны перед hello ресурсы в hello решения создаются и не должен быть определен в самом решении hello.  Hello пользователя будет [укажите рабочую область и учетную запись](operations-management-suite-solutions.md#oms-workspace-and-automation-account) при развертывании решения, но разработчики hello следует после точки hello.

## <a name="solution-resource"></a>Ресурс решения
Каждое решение требует запись ресурса в hello **ресурсов** элемент, определяющий само решение hello.  Это будет иметь тип **Microsoft.OperationsManagement/solutions** и имеют следующие структуры hello. Сюда входят [стандартные параметры](#parameters) и [переменных](#variables) , являются типовыми toodefine свойствами hello решения.


    {
      "name": "[concat(variables('Solution').Name, '[' ,parameters('workspacename'), ']')]",
      "location": "[parameters('workspaceRegionId')]",
      "tags": { },
      "type": "Microsoft.OperationsManagement/solutions",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
        <list-of-resources>
      ],
      "properties": {
        "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
        "referencedResources": [
            <list-of-referenced-resources>
        ],
        "containedResources": [
            <list-of-contained-resources>
        ]
      },
      "plan": {
        "name": "[concat(variables('Solution').Name, '[' ,parameters('workspaceName'), ']')]",
        "Version": "[variables('Solution').Version]",
        "product": "[variables('ProductName')]",
        "publisher": "[variables('Solution').Publisher]",
        "promotionCode": ""
      }
    }




### <a name="dependencies"></a>Зависимости
Hello решения ресурс должен иметь [зависимостей](../azure-resource-manager/resource-group-define-dependencies.md) на каждый ресурс в решении hello, так как они должны tooexist перед созданием hello решения.  Это делается путем добавления записи для каждого ресурса в hello **dependsOn** элемента.

### <a name="properties"></a>Свойства
Библиотека ресурсов Hello имеет свойства hello в следующей таблице hello.  Сюда входят ресурсы hello ссылки и принадлежащих hello решение, которое определяет управление hello ресурсов после установки решения для hello.  Каждый ресурс в решении hello должна быть указана в любом hello **referencedResources** или hello **containedResources** свойство.

| Свойство | Описание |
|:--- |:--- |
| workspaceResourceId |Идентификатор рабочей области аналитики журналов hello в форме hello  *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<имя рабочей области\>*. |
| referencedResources |Список ресурсов в решении hello, который не должен быть удален при удалении решения hello. |
| containedResources |Список ресурсов в решении hello, который должен быть удален при удалении решения hello. |

пример Hello выше предназначен для решения с runbook, расписание и представления.  расписание Hello и runbook *упоминаемого* в hello **свойства** элемента, поэтому они не удаляются при удалении решения hello.  представление Hello *содержится* , он удаляется при удалении решения hello.

### <a name="plan"></a>План
Hello **плана** сущность hello решения ресурса имеет свойства hello в hello в следующей таблице.

| Свойство | Description (Описание) |
|:--- |:--- |
| name |Имя решения hello. |
| версия |Версия решения hello определяется автором hello. |
| product |Уникальная строка tooidentify hello решения. |
| publisher |Издатель решения hello. |



## <a name="sample"></a>Образец
Образцы файлов решения с ресурсом решения можно просмотреть в следующих расположения hello.

- [Ресурсы службы автоматизации](operations-management-suite-solutions-resources-automation.md#sample)
- [Сохраненные поиски и оповещения Log Analytics в решениях OMS (предварительная версия)](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a>Дальнейшие действия
* [Добавьте сохраненные поисковые запросы и оповещения](operations-management-suite-solutions-resources-searches-alerts.md) tooyour решение для управления.
* [Добавление представления](operations-management-suite-solutions-resources-views.md) tooyour решение для управления.
* [Добавление модулей Runbook и другие ресурсы автоматизации](operations-management-suite-solutions-resources-automation.md) tooyour решение для управления.
* Узнайте подробности hello [шаблоны разработки Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).
* Найдите в коллекции [шаблонов быстрого запуска Azure](https://azure.microsoft.com/documentation/templates) примеры разных шаблонов Resource Manager.
