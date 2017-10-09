---
title: "aaaViews в системах управления Operations Management Suite (OMS) | Документы Microsoft"
description: "Решения для управления в Operations Management Suite (OMS), как правило, включает один или несколько данных toovisualize представления.  В этой статье описывается, как tooexport создано представление с Привет открыть в конструкторе и включите его в решении для управления. "
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 570b278c-2d47-4e5a-9828-7f01f31ddf8c
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 303861465014a27289f831332b3d95925c0ae66d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a>Представления в Operations Management Suite (OMS) (предварительная версия)
> [!NOTE]
> Это предварительная документация для создания решений для управления в консоли OMS, которая доступна в данный момент в режиме предварительной версии. Ни одной схеме, описанной ниже — toochange субъекта.    
>
>

[Решения для управления в Operations Management Suite (OMS)](operations-management-suite-solutions.md) как правило, включает один или несколько данных toovisualize представления.  В этой статье описывается, как tooexport создано представление с hello [конструктор представлений](../log-analytics/log-analytics-view-designer.md) и включите его в решении для управления.  

> [!NOTE]
> Hello примеры в этой статье с помощью параметров и переменные, которые либо обязательными или общие toomanagement решений и описано в [создание решений для управления в Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)
>
>

## <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается, что вы уже знакомы с работой слишком[создать решение управления](operations-management-suite-solutions-creating.md) и hello структуру файла решения.

## <a name="overview"></a>Обзор
Создание tooinclude представления в решении для управления **ресурсов** для него в hello [файл решения](operations-management-suite-solutions-creating.md).  Hello JSON, описывающий hello представление подробных сведений о конфигурации обычно сложные хотя и не что-нибудь, автор обычным решением будет toocreate может вручную.  Hello наиболее распространенный метод — toocreate hello представление с помощью hello [конструктор представлений](../log-analytics/log-analytics-view-designer.md), экспортируйте его, а затем добавьте его решение toohello подробных сведений о конфигурации.

Ниже приведены основные шаги Hello tooadd решения tooa представление.  Каждый шаг описан более подробно в следующих разделах hello.

1. Экспортируйте файл tooa представления hello.
2. Создайте представление ресурсов hello в решении hello.
3. Добавьте сведения о представлении hello.

## <a name="export-hello-view-tooa-file"></a>Экспорт файла tooa представления hello
Следуйте инструкциям hello в [конструктор представлений аналитика журналов](../log-analytics/log-analytics-view-designer.md) tooexport файл tooa представления.  Hello экспортированный файл будет иметь в формате JSON с hello же [элементы, что и файл решения hello](operations-management-suite-solutions-solution-file.md).  

Hello **ресурсов** элемент файла hello представление будет иметь ресурс с типом **Microsoft.OperationalInsights/workspaces** hello, представляет рабочую область OMS.  Этот элемент будет иметь дочерний элемент, с типом **представления** , представляющая hello и содержит его подробных сведений о конфигурации.  Скопировать сведения hello этого элемента и скопировать его в решении.

## <a name="create-hello-view-resource-in-hello-solution"></a>Создайте представление ресурсов hello в решении hello
Добавьте следующие представления ресурсов toohello hello **ресурсов** элементе файла решения.  Он использует переменные, описанные ниже, которые также необходимо добавить.  Обратите внимание, что hello **мониторинга** и **OverviewTile** свойства являются заполнителями, которые перезапишет hello соответствующие свойства из hello экспортируемого файла представления.

    {
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
        "type": "Microsoft.OperationalInsights/workspaces/views",
        "location": "[parameters('workspaceregionId')]",
        "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
        "dependson": [
            ],
        "properties": {
            "Id": "[variables('ViewName')]",
            "Name": "[variables('ViewName')]",
            "DisplayName": "[variables('ViewName')]",
            "Description": "",
            "Author": "[variables('ViewAuthor')]",
            "Source": "Local",
            "Dashboard": ,
            "OverviewTile":
        }
    }

Добавьте следующие переменные toohello переменные элемента файла решения hello hello и замените toothose hello значения для вашего решения.

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of hello view."
    "ViewName": "Provide a name for hello view here."


Обратите внимание, что hello всего представления ресурсов можно скопировать из файла экспортированного представления, но потребовалось бы следующие изменения для него hello toomake toowork в решении.  

* Hello **тип** для представления hello потребностей в ресурсах, изменено с toobe **представления** слишком**Microsoft.OperationalInsights/workspaces**.
* Hello **имя** свойство для ресурса hello представление нужно изменить toobe tooinclude hello рабочей имя.
* Hello зависимость от hello рабочей области должен toobe удалены, так как ресурс рабочей hello не определен в решении hello.
* **Отображаемое имя** toobe потребностей свойство добавлено представление toohello.  Hello **идентификатор**, **имя**, и **DisplayName** должен соответствовать всем.
* Имена параметров необходимо изменить toomatch hello требуется набор параметров.
* Переменные должны определенные в решении hello и использовать в соответствующих свойств hello.

## <a name="add-hello-view-details"></a>Добавить сведения о представлении hello
Hello представление ресурса в hello экспортированный файл будет содержать два элемента в hello представление **свойства** элемента с именем **мониторинга** и **OverviewTile** которой содержат hello hello представления подробных сведений о конфигурации.  Скопируйте эти два элемента и их содержимое в hello **свойства** элемент hello представление ресурса в файл решения.

## <a name="example"></a>Пример
Например следующий образец hello показан файл простое решение с представлением.  Многоточие (...) для hello показаны **панели мониторинга** и **OverviewTile** содержимое по причинам пространства.

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspaceName": {
                "type": "string"
            },
            "accountName": {
                "type": "string"
            },
            "workspaceRegionId": {
                "type": "string"
            },
            "regionId": {
                "type": "string"
            },
            "pricingTier": {
                "type": "string"
            }
        },
        "variables": {
            "SolutionVersion": "1.1",
            "SolutionPublisher": "Contoso",
            "SolutionName": "Contoso Solution",
            "LogAnalyticsApiVersion": "2015-11-01-preview",
            "ViewAuthor":  "user@contoso.com",
            "ViewDescription":  "This is a sample view.",
            "ViewName":  "Contoso View"
        },
        "resources": [
            {
                "name": "[concat(variables('SolutionName'), '(' ,parameters('workspacename'), ')')]",
                "location": "[parameters('workspaceRegionId')]",
                "tags": { },
                "type": "Microsoft.OperationsManagement/solutions",
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "dependsOn": [
                    "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspacename'), '/views/', variables('ViewName'))]"
                ],
                "properties": {
                    "workspaceResourceId": "[concat(resourceGroup().id, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspacename'))]",
                    "referencedResources": [
                    ],
                    "containedResources": [
                        "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/views/', variables('ViewName'))]"
                    ]
                },
                "plan": {
                    "name": "[concat(variables('SolutionName'), '(' ,parameters('workspaceName'), ')')]",
                    "Version": "[variables('SolutionVersion')]",
                    "product": "ContosoSolution",
                    "publisher": "[variables('SolutionPublisher')]",
                    "promotionCode": ""
                }
            },
            {
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
                "type": "Microsoft.OperationalInsights/workspaces/views",
                "location": "[parameters('workspaceregionId')]",
                "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
                "dependson": [
                ],
                "properties": {
                    "Id": "[variables('ViewName')]",
                    "Name": "[variables('ViewName')]",
                    "DisplayName": "[variables('ViewName')]",
                    "Description": "[variables('ViewDescription')]",
                    "Author": "[variables('ViewAuthor')]",
                    "Source": "Local",
                    "Dashboard": ...,
                    "OverviewTile": ...
                }
            }
          ]
    }




## <a name="next-steps"></a>Дальнейшие действия
* Узнайте подробнее о создании [решений для управления](operations-management-suite-solutions-creating.md).
* Добавьте [модули Runbook службы автоматизации в решение для управления](operations-management-suite-solutions-resources-automation.md).
