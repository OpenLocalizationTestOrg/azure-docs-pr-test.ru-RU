---
title: "Сохранение отчетов в Azure Power BI Embedded | Документация Майкрософт"
description: "Узнайте, как сохранять отчеты в Power BI Embedded. Для выполнения этого действия необходимы соответствующие разрешения."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: ad895004cc2972f2ded81566186325a16d401151
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="save-reports-in-power-bi-embedded"></a><span data-ttu-id="1d1ca-104">Сохранение отчетов в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="1d1ca-104">Save reports in Power BI Embedded</span></span>

<span data-ttu-id="1d1ca-105">Узнайте, как сохранять отчеты в Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="1d1ca-105">Learn how to save reports within Power BI embedded.</span></span> <span data-ttu-id="1d1ca-106">Для выполнения этого действия необходимы соответствующие разрешения.</span><span class="sxs-lookup"><span data-stu-id="1d1ca-106">This requires proper permissions in order to work successfully.</span></span>

<span data-ttu-id="1d1ca-107">В Power BI Embedded можно изменить существующие отчеты и сохранить их.</span><span class="sxs-lookup"><span data-stu-id="1d1ca-107">Within Power BI Embedded, you can edit existing reports and save them.</span></span> <span data-ttu-id="1d1ca-108">Также можно создать отчет и сохранить его как новый отчет.</span><span class="sxs-lookup"><span data-stu-id="1d1ca-108">You can also create a new report and save as a new report to create one.</span></span>

<span data-ttu-id="1d1ca-109">Чтобы сохранить отчет, сначала необходимо создать маркер для определенного отчета с соответствующими областями:</span><span class="sxs-lookup"><span data-stu-id="1d1ca-109">In order to save a report you first need to create a token for the specific report with the right scopes:</span></span>

* <span data-ttu-id="1d1ca-110">для использования команды "Сохранить" необходима область Report.ReadWrite;</span><span class="sxs-lookup"><span data-stu-id="1d1ca-110">To enable save Report.ReadWrite scope is required</span></span>
* <span data-ttu-id="1d1ca-111">для использования команды "Сохранить как" необходимы области Report.Read и Workspace.Report.Copy;</span><span class="sxs-lookup"><span data-stu-id="1d1ca-111">To enable save as, Report.Read and Workspace.Report.Copy scopes are required</span></span>
* <span data-ttu-id="1d1ca-112">для использования команд "Сохранить" и "Сохранить как" необходимы области Report.ReadWrite и Workspace.Report.Copy.</span><span class="sxs-lookup"><span data-stu-id="1d1ca-112">To enable save and save as, Report.ReadWrite and Workspace.Report.Copy are requierd</span></span>

<span data-ttu-id="1d1ca-113">Соответственно, чтобы правильно добавить в меню "Файл" кнопки "Сохранить" и "Сохранить как", при внедрении отчета необходимо предоставить правильные разрешения в конфигурации внедрения:</span><span class="sxs-lookup"><span data-stu-id="1d1ca-113">Respectively in order to enable the right save/save as buttons in file menu you need to provide the right permission in the Embed configuration when you Embed the report:</span></span>

* <span data-ttu-id="1d1ca-114">models.Permissions.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="1d1ca-114">models.Permissions.ReadWrite</span></span>
* <span data-ttu-id="1d1ca-115">models.Permissions.Copy</span><span class="sxs-lookup"><span data-stu-id="1d1ca-115">models.Permissions.Copy</span></span>
* <span data-ttu-id="1d1ca-116">models.Permissions.All</span><span class="sxs-lookup"><span data-stu-id="1d1ca-116">models.Permissions.All</span></span>

> [!NOTE]
> <span data-ttu-id="1d1ca-117">Для маркера доступа также требуются соответствующие области.</span><span class="sxs-lookup"><span data-stu-id="1d1ca-117">Your access token also needs the appropriate scopes.</span></span> <span data-ttu-id="1d1ca-118">Дополнительные сведения см. в разделе [Области](power-bi-embedded-app-token-flow.md#scopes).</span><span class="sxs-lookup"><span data-stu-id="1d1ca-118">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

## <a name="embed-report-in-edit-mode"></a><span data-ttu-id="1d1ca-119">Внедрение отчета в режиме правки</span><span class="sxs-lookup"><span data-stu-id="1d1ca-119">Embed report in edit mode</span></span>

<span data-ttu-id="1d1ca-120">Предположим, что вам требуется внедрить отчет в свое приложение в режиме правки. Для этого просто передайте необходимые свойства в конфигурацию внедрения и выполните вызов powerbi.embed().</span><span class="sxs-lookup"><span data-stu-id="1d1ca-120">Let's say you want to Embed a report in edit mode inside your app, to do so just pass the right properties in Embed configuration and call powerbi.embed().</span></span> <span data-ttu-id="1d1ca-121">Необходимо будет предоставить разрешения и параметр viewMode, чтобы кнопки "Сохранить" и "Сохранить как" отображались в режиме правки.</span><span class="sxs-lookup"><span data-stu-id="1d1ca-121">You will need to supply permissions and a viewMode in order to see the save and save as buttons when in edit mode.</span></span> <span data-ttu-id="1d1ca-122">Дополнительные сведения см. в статье [Embed Configuration Details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details) (Сведения о конфигурации внедрения).</span><span class="sxs-lookup"><span data-stu-id="1d1ca-122">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="1d1ca-123">Например, в JavaScript:</span><span class="sxs-lookup"><span data-stu-id="1d1ca-123">For example in JavaScript:</span></span>

```
   <div id="reportContainer"></div>

    // Get models. Models, it contains enums that can be used.
    var models = window['powerbi-client'].models;

    // Embed configuration used to describe the what and how to embed.
    // This object is used when calling powerbi.embed.
    // This also includes settings and options such as filters.
    // You can find more information at https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details.
    var config= {
        type: 'report',
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        id:  '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
        permissions: models.Permissions.All /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.Edit,
        settings: {
            filterPaneEnabled: true,
            navContentPaneEnabled: true
        }
    };

    // Get a reference to the embedded report HTML element
    var reportContainer = $('#reportContainer')[0];

    // Embed the report and display it within the div container.
    var report = powerbi.embed(reportContainer, config);
```

<span data-ttu-id="1d1ca-124">Теперь отчет будет внедрен в приложение в режиме правки.</span><span class="sxs-lookup"><span data-stu-id="1d1ca-124">Now a report will be embedded in your app in edit mode.</span></span>

## <a name="save-report"></a><span data-ttu-id="1d1ca-125">Сохранение отчета</span><span class="sxs-lookup"><span data-stu-id="1d1ca-125">Save report</span></span>

<span data-ttu-id="1d1ca-126">После внедрения отчета в режиме правки с правильными разрешениями и маркером можно сохранить этот отчет, используя меню "Файл" или JavaScript:</span><span class="sxs-lookup"><span data-stu-id="1d1ca-126">After Embbeding the report in edit mode with the right token and permissions you can save the report from the file menu or from javascript:</span></span>

```
 // Get a reference to the embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a><span data-ttu-id="1d1ca-127">Сохранить как</span><span class="sxs-lookup"><span data-stu-id="1d1ca-127">Save as</span></span>

```
// Get a reference to the embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> <span data-ttu-id="1d1ca-128">Создание отчета завершается только после выполнения команды *Сохранить как*.</span><span class="sxs-lookup"><span data-stu-id="1d1ca-128">Only after *save as* is a new report created.</span></span> <span data-ttu-id="1d1ca-129">Если выбрать команду "Сохранить", то на холсте продолжает отображаться старый отчет в режиме правки, а не новый отчет.</span><span class="sxs-lookup"><span data-stu-id="1d1ca-129">After the save, the canvas is still showing the old report in edit mode and not the new report.</span></span> <span data-ttu-id="1d1ca-130">Необходимо будет внедрить отчет, который был создан.</span><span class="sxs-lookup"><span data-stu-id="1d1ca-130">You will need to embed the new report that was created.</span></span> <span data-ttu-id="1d1ca-131">Для этого потребуется новый маркер доступа, так как они создаются отдельно для каждого отчета.</span><span class="sxs-lookup"><span data-stu-id="1d1ca-131">This requires a new access token as they are created per report.</span></span>

<span data-ttu-id="1d1ca-132">После выполнения команды *Сохранить как* необходимо будет загрузить новый отчет.</span><span class="sxs-lookup"><span data-stu-id="1d1ca-132">You will then need to load the new report after a *save as*.</span></span> <span data-ttu-id="1d1ca-133">Данная процедура аналогична процедуре внедрения любого отчета.</span><span class="sxs-lookup"><span data-stu-id="1d1ca-133">This is similar to embedding any report.</span></span>

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="see-also"></a><span data-ttu-id="1d1ca-134">См. также</span><span class="sxs-lookup"><span data-stu-id="1d1ca-134">See also</span></span>

[<span data-ttu-id="1d1ca-135">Приступая к работе с примером Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="1d1ca-135">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="1d1ca-136">Внедрение отчета в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="1d1ca-136">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="1d1ca-137">Создание отчета из набора данных</span><span class="sxs-lookup"><span data-stu-id="1d1ca-137">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="1d1ca-138">Аутентификация и авторизация в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="1d1ca-138">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="1d1ca-139">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="1d1ca-139">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="1d1ca-140">Пример внедрения JavaScript</span><span class="sxs-lookup"><span data-stu-id="1d1ca-140">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="1d1ca-141">У вас имеются и другие вопросы?</span><span class="sxs-lookup"><span data-stu-id="1d1ca-141">More questions?</span></span> [<span data-ttu-id="1d1ca-142">Попробуйте задать их в сообществе Power BI</span><span class="sxs-lookup"><span data-stu-id="1d1ca-142">Try the Power BI Community</span></span>](http://community.powerbi.com/)

