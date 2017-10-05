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
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a><span data-ttu-id="c3e00-104">Представления в Operations Management Suite (OMS) (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="c3e00-104">Views in Operations Management Suite (OMS) management solutions (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="c3e00-105">Это предварительная документация для создания решений для управления в консоли OMS, которая доступна в данный момент в режиме предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="c3e00-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="c3e00-106">Любые схемы, приведенные ниже, могут измениться.</span><span class="sxs-lookup"><span data-stu-id="c3e00-106">Any schema described below is subject to change.</span></span>    
>
>

<span data-ttu-id="c3e00-107">Как правило, [решения для управления в Operations Management Suite (OMS)](operations-management-suite-solutions.md) включают одно или несколько представлений для визуализации данных.</span><span class="sxs-lookup"><span data-stu-id="c3e00-107">[Management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions.md) will typically include one or more views to visualize data.</span></span>  <span data-ttu-id="c3e00-108">В этой статье описывается, как экспортировать представление, созданное в [конструкторе представлений](../log-analytics/log-analytics-view-designer.md), и добавить его в решение для управления.</span><span class="sxs-lookup"><span data-stu-id="c3e00-108">This article describes how to export a view created by the [View Designer](../log-analytics/log-analytics-view-designer.md) and include it in a management solution.</span></span>  

> [!NOTE]
> <span data-ttu-id="c3e00-109">В примерах здесь используются обязательные или общие параметры и переменные для решений по управлению, описанные в статье [Создание решений для управления в Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="c3e00-109">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="c3e00-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c3e00-110">Prerequisites</span></span>
<span data-ttu-id="c3e00-111">В этой статье предполагается, что вы уже знаете, как [создать решение для управления](operations-management-suite-solutions-creating.md) и структуру файла решения.</span><span class="sxs-lookup"><span data-stu-id="c3e00-111">This article assumes that you're already familiar with how to [create a management solution](operations-management-suite-solutions-creating.md) and the structure of a solution file.</span></span>

## <a name="overview"></a><span data-ttu-id="c3e00-112">Обзор</span><span class="sxs-lookup"><span data-stu-id="c3e00-112">Overview</span></span>
<span data-ttu-id="c3e00-113">Чтобы добавить представление в решение для управления, создайте для него **ресурс** в [файле решения](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="c3e00-113">To include a view in a management solution, you create a **resource** for it in the [solution file](operations-management-suite-solutions-creating.md).</span></span>  <span data-ttu-id="c3e00-114">JSON, описывающий подробную конфигурацию представления, как правило, сложный. Обычный разработчик решений не сможет создать его вручную.</span><span class="sxs-lookup"><span data-stu-id="c3e00-114">The JSON that describes the view's detailed configuration is typically complex though and not something that a typical solution author would be able to create manually.</span></span>  <span data-ttu-id="c3e00-115">Самый распространенный способ — создать представление с помощью [конструктора представлений](../log-analytics/log-analytics-view-designer.md), экспортировать его и добавить его подробную конфигурацию в решение.</span><span class="sxs-lookup"><span data-stu-id="c3e00-115">The most common method is to create the view using the [View Designer](../log-analytics/log-analytics-view-designer.md), export it, and then add its detailed configuration to the solution.</span></span>

<span data-ttu-id="c3e00-116">Ниже приведены основные действия по добавлению представления в решение.</span><span class="sxs-lookup"><span data-stu-id="c3e00-116">The basic steps to add a view to a solution are as follows.</span></span>  <span data-ttu-id="c3e00-117">Каждое из этих действий подробно описано в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="c3e00-117">Each step is described in further detail in the sections below.</span></span>

1. <span data-ttu-id="c3e00-118">Экспортируйте представление в файл.</span><span class="sxs-lookup"><span data-stu-id="c3e00-118">Export the view to a file.</span></span>
2. <span data-ttu-id="c3e00-119">Создайте ресурс представления в решении.</span><span class="sxs-lookup"><span data-stu-id="c3e00-119">Create the view resource in the solution.</span></span>
3. <span data-ttu-id="c3e00-120">Добавьте сведения о представлении.</span><span class="sxs-lookup"><span data-stu-id="c3e00-120">Add the view details.</span></span>

## <a name="export-the-view-to-a-file"></a><span data-ttu-id="c3e00-121">Экспорт представления в файл</span><span class="sxs-lookup"><span data-stu-id="c3e00-121">Export the view to a file</span></span>
<span data-ttu-id="c3e00-122">Чтобы экспортировать представление в файл, следуйте инструкциям [конструктора представлений Log Analytics](../log-analytics/log-analytics-view-designer.md).</span><span class="sxs-lookup"><span data-stu-id="c3e00-122">Follow the instructions at [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) to export a view to a file.</span></span>  <span data-ttu-id="c3e00-123">Экспортированный файл будет в формате JSON с теми же [элементами, что и в файле решения](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="c3e00-123">The exported file will be in JSON format with the same [elements as the solution file](operations-management-suite-solutions-solution-file.md).</span></span>  

<span data-ttu-id="c3e00-124">Элемент **resources** в файле представления будет содержать ресурс типа **Microsoft.OperationalInsights/workspaces**, представляющий рабочую область OMS.</span><span class="sxs-lookup"><span data-stu-id="c3e00-124">The **resources** element of the view file will have a resource with a type of **Microsoft.OperationalInsights/workspaces** that represents the OMS workspace.</span></span>  <span data-ttu-id="c3e00-125">Этот элемент будет содержать подэлемент типа **views**, представляющий представление и содержащий его подробную конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="c3e00-125">This element will have a subelement with a type of **views** that represents the view and contains its detailed configuration.</span></span>  <span data-ttu-id="c3e00-126">Скопируйте сведения этого элемента и сам элемент в решение.</span><span class="sxs-lookup"><span data-stu-id="c3e00-126">You will copy the details of this element and then copy it into your solution.</span></span>

## <a name="create-the-view-resource-in-the-solution"></a><span data-ttu-id="c3e00-127">Создание ресурса представления в решении</span><span class="sxs-lookup"><span data-stu-id="c3e00-127">Create the view resource in the solution</span></span>
<span data-ttu-id="c3e00-128">Добавьте следующий ресурс представления в элемент **resources** файла решения.</span><span class="sxs-lookup"><span data-stu-id="c3e00-128">Add the following view resource to the **resources** element of your solution file.</span></span>  <span data-ttu-id="c3e00-129">Он использует переменные, описанные ниже, которые также необходимо добавить.</span><span class="sxs-lookup"><span data-stu-id="c3e00-129">This uses variables that are described below that you must also add.</span></span>  <span data-ttu-id="c3e00-130">Обратите внимание, что свойства **Dashboard** и **OverviewTile** представляют собой заполнители, которые вы перезапишете с помощью соответствующих свойств из экспортированного файла представления.</span><span class="sxs-lookup"><span data-stu-id="c3e00-130">Note that the **Dashboard** and **OverviewTile** properties are placeholders that you will overwrite with the corresponding properties from the exported view file.</span></span>

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

<span data-ttu-id="c3e00-131">Добавьте следующие переменные в элемент variables файла решения и замените значения соответствующими значениями для своего решения.</span><span class="sxs-lookup"><span data-stu-id="c3e00-131">Add the following variables to the variables element of the solution file and replace the values to those for your solution.</span></span>

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of the view."
    "ViewName": "Provide a name for the view here."


<span data-ttu-id="c3e00-132">Обратите внимание, что можно скопировать весь ресурс представления из экспортированного файла представления. Однако для этого в решение необходимо внести следующие изменения.</span><span class="sxs-lookup"><span data-stu-id="c3e00-132">Note that you could copy the entire view resource from your exported view file, but you would need to make the following changes for it to work in your solution.</span></span>  

* <span data-ttu-id="c3e00-133">Значение свойства **type** ресурса представления нужно изменить с **views** на **Microsoft.OperationalInsights/workspaces**.</span><span class="sxs-lookup"><span data-stu-id="c3e00-133">The **type** for the view resource needs to be changed from **views** to **Microsoft.OperationalInsights/workspaces**.</span></span>
* <span data-ttu-id="c3e00-134">В значение свойства **name** ресурса представления нужно добавить имя рабочей области.</span><span class="sxs-lookup"><span data-stu-id="c3e00-134">The **name** property for the view resource needs to be changed to include the workspace name.</span></span>
* <span data-ttu-id="c3e00-135">Зависимость от рабочей области нужно удалить, так как ресурс рабочей области не определен в решении.</span><span class="sxs-lookup"><span data-stu-id="c3e00-135">The dependency on the workspace needs to be removed since the workspace resource isn't defined in the solution.</span></span>
* <span data-ttu-id="c3e00-136">В представление нужно добавить свойство **DisplayName**.</span><span class="sxs-lookup"><span data-stu-id="c3e00-136">**DisplayName** property needs to be added to the view.</span></span>  <span data-ttu-id="c3e00-137">Значения свойств **Id**, **Name** и **DisplayName** должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="c3e00-137">The **Id**, **Name**, and **DisplayName** must all match.</span></span>
* <span data-ttu-id="c3e00-138">Имена параметров необходимо изменить в соответствии с необходимым набором параметров.</span><span class="sxs-lookup"><span data-stu-id="c3e00-138">Parameter names must be changed to match the required set of parameters.</span></span>
* <span data-ttu-id="c3e00-139">Переменные нужно определить в решении и использовать в соответствующих свойствах.</span><span class="sxs-lookup"><span data-stu-id="c3e00-139">Variables should be defined in the solution and used in the appropriate properties.</span></span>

## <a name="add-the-view-details"></a><span data-ttu-id="c3e00-140">Добавление сведений о представлении</span><span class="sxs-lookup"><span data-stu-id="c3e00-140">Add the view details</span></span>
<span data-ttu-id="c3e00-141">Ресурс представления в экспортированном файле представления будет содержать два элемента в элементе **properties** с именем **Dashboard** и **OverviewTile**, включающие подробную конфигурацию представления.</span><span class="sxs-lookup"><span data-stu-id="c3e00-141">The view resource in the exported view file will contain two elements in the **properties** element named **Dashboard** and **OverviewTile** which contain the detailed configuration of the view.</span></span>  <span data-ttu-id="c3e00-142">Скопируйте эти два элемента и их содержимое в элемент **properties** ресурса представления в файле решения.</span><span class="sxs-lookup"><span data-stu-id="c3e00-142">Copy these two elements and their contents into the **properties** element of the view resource in your solution file.</span></span>

## <a name="example"></a><span data-ttu-id="c3e00-143">Пример</span><span class="sxs-lookup"><span data-stu-id="c3e00-143">Example</span></span>
<span data-ttu-id="c3e00-144">Ниже приведен пример файла простого решения с представлением.</span><span class="sxs-lookup"><span data-stu-id="c3e00-144">For example, the following sample shows a simple solution file with a view.</span></span>  <span data-ttu-id="c3e00-145">В содержимом свойств **Dashboard** и **OverviewTile** многоточие (...) отображается для экономии пространства.</span><span class="sxs-lookup"><span data-stu-id="c3e00-145">Ellipses (...) are shown for the **Dashboard** and **OverviewTile** contents for space reasons.</span></span>

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




## <a name="next-steps"></a><span data-ttu-id="c3e00-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c3e00-146">Next steps</span></span>
* <span data-ttu-id="c3e00-147">Узнайте подробнее о создании [решений для управления](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="c3e00-147">Learn complete details of creating [management solutions](operations-management-suite-solutions-creating.md).</span></span>
* <span data-ttu-id="c3e00-148">Добавьте [модули Runbook службы автоматизации в решение для управления](operations-management-suite-solutions-resources-automation.md).</span><span class="sxs-lookup"><span data-stu-id="c3e00-148">Include [Automation runbooks in your management solution](operations-management-suite-solutions-resources-automation.md).</span></span>
