---
title: "Представления в Operations Management Suite (OMS) | Документация Майкрософт"
description: "Как правило, решения для управления в Operations Management Suite (OMS) включают одно или несколько представлений для визуализации данных.  В этой статье описывается, как экспортировать представление, созданное в конструкторе представлений, и добавить его в решение для управления. "
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
ms.openlocfilehash: 533b5564a805e0b41f2b1a4ad92e12b133220952
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a>Представления в Operations Management Suite (OMS) (предварительная версия)
> [!NOTE]
> Это предварительная документация для создания решений для управления в консоли OMS, которая доступна в данный момент в режиме предварительной версии. Любые схемы, приведенные ниже, могут измениться.    
>
>

Как правило, [решения для управления в Operations Management Suite (OMS)](operations-management-suite-solutions.md) включают одно или несколько представлений для визуализации данных.  В этой статье описывается, как экспортировать представление, созданное в [конструкторе представлений](../log-analytics/log-analytics-view-designer.md), и добавить его в решение для управления.  

> [!NOTE]
> В примерах здесь используются обязательные или общие параметры и переменные для решений по управлению, описанные в статье [Создание решений для управления в Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md).
>
>

## <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается, что вы уже знаете, как [создать решение для управления](operations-management-suite-solutions-creating.md) и структуру файла решения.

## <a name="overview"></a>Обзор
Чтобы добавить представление в решение для управления, создайте для него **ресурс** в [файле решения](operations-management-suite-solutions-creating.md).  JSON, описывающий подробную конфигурацию представления, как правило, сложный. Обычный разработчик решений не сможет создать его вручную.  Самый распространенный способ — создать представление с помощью [конструктора представлений](../log-analytics/log-analytics-view-designer.md), экспортировать его и добавить его подробную конфигурацию в решение.

Ниже приведены основные действия по добавлению представления в решение.  Каждое из этих действий подробно описано в следующих разделах.

1. Экспортируйте представление в файл.
2. Создайте ресурс представления в решении.
3. Добавьте сведения о представлении.

## <a name="export-the-view-to-a-file"></a>Экспорт представления в файл
Чтобы экспортировать представление в файл, следуйте инструкциям [конструктора представлений Log Analytics](../log-analytics/log-analytics-view-designer.md).  Экспортированный файл будет в формате JSON с теми же [элементами, что и в файле решения](operations-management-suite-solutions-solution-file.md).  

Элемент **resources** в файле представления будет содержать ресурс типа **Microsoft.OperationalInsights/workspaces**, представляющий рабочую область OMS.  Этот элемент будет содержать подэлемент типа **views**, представляющий представление и содержащий его подробную конфигурацию.  Скопируйте сведения этого элемента и сам элемент в решение.

## <a name="create-the-view-resource-in-the-solution"></a>Создание ресурса представления в решении
Добавьте следующий ресурс представления в элемент **resources** файла решения.  Он использует переменные, описанные ниже, которые также необходимо добавить.  Обратите внимание, что свойства **Dashboard** и **OverviewTile** представляют собой заполнители, которые вы перезапишете с помощью соответствующих свойств из экспортированного файла представления.

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

Добавьте следующие переменные в элемент variables файла решения и замените значения соответствующими значениями для своего решения.

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of the view."
    "ViewName": "Provide a name for the view here."


Обратите внимание, что можно скопировать весь ресурс представления из экспортированного файла представления. Однако для этого в решение необходимо внести следующие изменения.  

* Значение свойства **type** ресурса представления нужно изменить с **views** на **Microsoft.OperationalInsights/workspaces**.
* В значение свойства **name** ресурса представления нужно добавить имя рабочей области.
* Зависимость от рабочей области нужно удалить, так как ресурс рабочей области не определен в решении.
* В представление нужно добавить свойство **DisplayName**.  Значения свойств **Id**, **Name** и **DisplayName** должны совпадать.
* Имена параметров необходимо изменить в соответствии с необходимым набором параметров.
* Переменные нужно определить в решении и использовать в соответствующих свойствах.

## <a name="add-the-view-details"></a>Добавление сведений о представлении
Ресурс представления в экспортированном файле представления будет содержать два элемента в элементе **properties** с именем **Dashboard** и **OverviewTile**, включающие подробную конфигурацию представления.  Скопируйте эти два элемента и их содержимое в элемент **properties** ресурса представления в файле решения.

## <a name="example"></a>Пример
Ниже приведен пример файла простого решения с представлением.  В содержимом свойств **Dashboard** и **OverviewTile** многоточие (...) отображается для экономии пространства.

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
