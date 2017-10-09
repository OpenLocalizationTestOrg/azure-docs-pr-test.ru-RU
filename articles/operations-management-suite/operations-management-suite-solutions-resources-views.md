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
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a><span data-ttu-id="dc8b4-104">Представления в Operations Management Suite (OMS) (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="dc8b4-104">Views in Operations Management Suite (OMS) management solutions (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="dc8b4-105">Это предварительная документация для создания решений для управления в консоли OMS, которая доступна в данный момент в режиме предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="dc8b4-106">Ни одной схеме, описанной ниже — toochange субъекта.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-106">Any schema described below is subject toochange.</span></span>    
>
>

<span data-ttu-id="dc8b4-107">[Решения для управления в Operations Management Suite (OMS)](operations-management-suite-solutions.md) как правило, включает один или несколько данных toovisualize представления.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-107">[Management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions.md) will typically include one or more views toovisualize data.</span></span>  <span data-ttu-id="dc8b4-108">В этой статье описывается, как tooexport создано представление с hello [конструктор представлений](../log-analytics/log-analytics-view-designer.md) и включите его в решении для управления.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-108">This article describes how tooexport a view created by hello [View Designer](../log-analytics/log-analytics-view-designer.md) and include it in a management solution.</span></span>  

> [!NOTE]
> <span data-ttu-id="dc8b4-109">Hello примеры в этой статье с помощью параметров и переменные, которые либо обязательными или общие toomanagement решений и описано в [создание решений для управления в Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="dc8b4-109">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="dc8b4-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="dc8b4-110">Prerequisites</span></span>
<span data-ttu-id="dc8b4-111">В этой статье предполагается, что вы уже знакомы с работой слишком[создать решение управления](operations-management-suite-solutions-creating.md) и hello структуру файла решения.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-111">This article assumes that you're already familiar with how too[create a management solution](operations-management-suite-solutions-creating.md) and hello structure of a solution file.</span></span>

## <a name="overview"></a><span data-ttu-id="dc8b4-112">Обзор</span><span class="sxs-lookup"><span data-stu-id="dc8b4-112">Overview</span></span>
<span data-ttu-id="dc8b4-113">Создание tooinclude представления в решении для управления **ресурсов** для него в hello [файл решения](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="dc8b4-113">tooinclude a view in a management solution, you create a **resource** for it in hello [solution file](operations-management-suite-solutions-creating.md).</span></span>  <span data-ttu-id="dc8b4-114">Hello JSON, описывающий hello представление подробных сведений о конфигурации обычно сложные хотя и не что-нибудь, автор обычным решением будет toocreate может вручную.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-114">hello JSON that describes hello view's detailed configuration is typically complex though and not something that a typical solution author would be able toocreate manually.</span></span>  <span data-ttu-id="dc8b4-115">Hello наиболее распространенный метод — toocreate hello представление с помощью hello [конструктор представлений](../log-analytics/log-analytics-view-designer.md), экспортируйте его, а затем добавьте его решение toohello подробных сведений о конфигурации.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-115">hello most common method is toocreate hello view using hello [View Designer](../log-analytics/log-analytics-view-designer.md), export it, and then add its detailed configuration toohello solution.</span></span>

<span data-ttu-id="dc8b4-116">Ниже приведены основные шаги Hello tooadd решения tooa представление.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-116">hello basic steps tooadd a view tooa solution are as follows.</span></span>  <span data-ttu-id="dc8b4-117">Каждый шаг описан более подробно в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-117">Each step is described in further detail in hello sections below.</span></span>

1. <span data-ttu-id="dc8b4-118">Экспортируйте файл tooa представления hello.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-118">Export hello view tooa file.</span></span>
2. <span data-ttu-id="dc8b4-119">Создайте представление ресурсов hello в решении hello.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-119">Create hello view resource in hello solution.</span></span>
3. <span data-ttu-id="dc8b4-120">Добавьте сведения о представлении hello.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-120">Add hello view details.</span></span>

## <a name="export-hello-view-tooa-file"></a><span data-ttu-id="dc8b4-121">Экспорт файла tooa представления hello</span><span class="sxs-lookup"><span data-stu-id="dc8b4-121">Export hello view tooa file</span></span>
<span data-ttu-id="dc8b4-122">Следуйте инструкциям hello в [конструктор представлений аналитика журналов](../log-analytics/log-analytics-view-designer.md) tooexport файл tooa представления.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-122">Follow hello instructions at [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) tooexport a view tooa file.</span></span>  <span data-ttu-id="dc8b4-123">Hello экспортированный файл будет иметь в формате JSON с hello же [элементы, что и файл решения hello](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="dc8b4-123">hello exported file will be in JSON format with hello same [elements as hello solution file](operations-management-suite-solutions-solution-file.md).</span></span>  

<span data-ttu-id="dc8b4-124">Hello **ресурсов** элемент файла hello представление будет иметь ресурс с типом **Microsoft.OperationalInsights/workspaces** hello, представляет рабочую область OMS.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-124">hello **resources** element of hello view file will have a resource with a type of **Microsoft.OperationalInsights/workspaces** that represents hello OMS workspace.</span></span>  <span data-ttu-id="dc8b4-125">Этот элемент будет иметь дочерний элемент, с типом **представления** , представляющая hello и содержит его подробных сведений о конфигурации.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-125">This element will have a subelement with a type of **views** that represents hello view and contains its detailed configuration.</span></span>  <span data-ttu-id="dc8b4-126">Скопировать сведения hello этого элемента и скопировать его в решении.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-126">You will copy hello details of this element and then copy it into your solution.</span></span>

## <a name="create-hello-view-resource-in-hello-solution"></a><span data-ttu-id="dc8b4-127">Создайте представление ресурсов hello в решении hello</span><span class="sxs-lookup"><span data-stu-id="dc8b4-127">Create hello view resource in hello solution</span></span>
<span data-ttu-id="dc8b4-128">Добавьте следующие представления ресурсов toohello hello **ресурсов** элементе файла решения.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-128">Add hello following view resource toohello **resources** element of your solution file.</span></span>  <span data-ttu-id="dc8b4-129">Он использует переменные, описанные ниже, которые также необходимо добавить.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-129">This uses variables that are described below that you must also add.</span></span>  <span data-ttu-id="dc8b4-130">Обратите внимание, что hello **мониторинга** и **OverviewTile** свойства являются заполнителями, которые перезапишет hello соответствующие свойства из hello экспортируемого файла представления.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-130">Note that hello **Dashboard** and **OverviewTile** properties are placeholders that you will overwrite with hello corresponding properties from hello exported view file.</span></span>

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

<span data-ttu-id="dc8b4-131">Добавьте следующие переменные toohello переменные элемента файла решения hello hello и замените toothose hello значения для вашего решения.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-131">Add hello following variables toohello variables element of hello solution file and replace hello values toothose for your solution.</span></span>

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of hello view."
    "ViewName": "Provide a name for hello view here."


<span data-ttu-id="dc8b4-132">Обратите внимание, что hello всего представления ресурсов можно скопировать из файла экспортированного представления, но потребовалось бы следующие изменения для него hello toomake toowork в решении.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-132">Note that you could copy hello entire view resource from your exported view file, but you would need toomake hello following changes for it toowork in your solution.</span></span>  

* <span data-ttu-id="dc8b4-133">Hello **тип** для представления hello потребностей в ресурсах, изменено с toobe **представления** слишком**Microsoft.OperationalInsights/workspaces**.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-133">hello **type** for hello view resource needs toobe changed from **views** too**Microsoft.OperationalInsights/workspaces**.</span></span>
* <span data-ttu-id="dc8b4-134">Hello **имя** свойство для ресурса hello представление нужно изменить toobe tooinclude hello рабочей имя.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-134">hello **name** property for hello view resource needs toobe changed tooinclude hello workspace name.</span></span>
* <span data-ttu-id="dc8b4-135">Hello зависимость от hello рабочей области должен toobe удалены, так как ресурс рабочей hello не определен в решении hello.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-135">hello dependency on hello workspace needs toobe removed since hello workspace resource isn't defined in hello solution.</span></span>
* <span data-ttu-id="dc8b4-136">**Отображаемое имя** toobe потребностей свойство добавлено представление toohello.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-136">**DisplayName** property needs toobe added toohello view.</span></span>  <span data-ttu-id="dc8b4-137">Hello **идентификатор**, **имя**, и **DisplayName** должен соответствовать всем.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-137">hello **Id**, **Name**, and **DisplayName** must all match.</span></span>
* <span data-ttu-id="dc8b4-138">Имена параметров необходимо изменить toomatch hello требуется набор параметров.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-138">Parameter names must be changed toomatch hello required set of parameters.</span></span>
* <span data-ttu-id="dc8b4-139">Переменные должны определенные в решении hello и использовать в соответствующих свойств hello.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-139">Variables should be defined in hello solution and used in hello appropriate properties.</span></span>

## <a name="add-hello-view-details"></a><span data-ttu-id="dc8b4-140">Добавить сведения о представлении hello</span><span class="sxs-lookup"><span data-stu-id="dc8b4-140">Add hello view details</span></span>
<span data-ttu-id="dc8b4-141">Hello представление ресурса в hello экспортированный файл будет содержать два элемента в hello представление **свойства** элемента с именем **мониторинга** и **OverviewTile** которой содержат hello hello представления подробных сведений о конфигурации.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-141">hello view resource in hello exported view file will contain two elements in hello **properties** element named **Dashboard** and **OverviewTile** which contain hello detailed configuration of hello view.</span></span>  <span data-ttu-id="dc8b4-142">Скопируйте эти два элемента и их содержимое в hello **свойства** элемент hello представление ресурса в файл решения.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-142">Copy these two elements and their contents into hello **properties** element of hello view resource in your solution file.</span></span>

## <a name="example"></a><span data-ttu-id="dc8b4-143">Пример</span><span class="sxs-lookup"><span data-stu-id="dc8b4-143">Example</span></span>
<span data-ttu-id="dc8b4-144">Например следующий образец hello показан файл простое решение с представлением.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-144">For example, hello following sample shows a simple solution file with a view.</span></span>  <span data-ttu-id="dc8b4-145">Многоточие (...) для hello показаны **панели мониторинга** и **OverviewTile** содержимое по причинам пространства.</span><span class="sxs-lookup"><span data-stu-id="dc8b4-145">Ellipses (...) are shown for hello **Dashboard** and **OverviewTile** contents for space reasons.</span></span>

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




## <a name="next-steps"></a><span data-ttu-id="dc8b4-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dc8b4-146">Next steps</span></span>
* <span data-ttu-id="dc8b4-147">Узнайте подробнее о создании [решений для управления](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="dc8b4-147">Learn complete details of creating [management solutions](operations-management-suite-solutions-creating.md).</span></span>
* <span data-ttu-id="dc8b4-148">Добавьте [модули Runbook службы автоматизации в решение для управления](operations-management-suite-solutions-resources-automation.md).</span><span class="sxs-lookup"><span data-stu-id="dc8b4-148">Include [Automation runbooks in your management solution](operations-management-suite-solutions-resources-automation.md).</span></span>
