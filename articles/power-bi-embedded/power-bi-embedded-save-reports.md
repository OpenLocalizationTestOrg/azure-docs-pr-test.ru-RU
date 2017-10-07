---
title: "aaaSave отчеты в Azure Power BI Embedded | Документы Microsoft"
description: "Узнайте, как внедренные toosave отчеты в Power BI. Это требует соответствующие разрешения в порядке toowork успешно."
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
ms.openlocfilehash: 984537ce1ce1afc787d6c6c9f61ae8d6226d1171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="save-reports-in-power-bi-embedded"></a><span data-ttu-id="3925a-104">Сохранение отчетов в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="3925a-104">Save reports in Power BI Embedded</span></span>

<span data-ttu-id="3925a-105">Узнайте, как внедренные toosave отчеты в Power BI.</span><span class="sxs-lookup"><span data-stu-id="3925a-105">Learn how toosave reports within Power BI embedded.</span></span> <span data-ttu-id="3925a-106">Это требует соответствующие разрешения в порядке toowork успешно.</span><span class="sxs-lookup"><span data-stu-id="3925a-106">This requires proper permissions in order toowork successfully.</span></span>

<span data-ttu-id="3925a-107">В Power BI Embedded можно изменить существующие отчеты и сохранить их.</span><span class="sxs-lookup"><span data-stu-id="3925a-107">Within Power BI Embedded, you can edit existing reports and save them.</span></span> <span data-ttu-id="3925a-108">Можно также создать новый отчет и сохранить как новый отчет toocreate, один.</span><span class="sxs-lookup"><span data-stu-id="3925a-108">You can also create a new report and save as a new report toocreate one.</span></span>

<span data-ttu-id="3925a-109">В порядке toosave отчета необходимо сначала toocreate маркер для конкретного отчета hello hello правой области:</span><span class="sxs-lookup"><span data-stu-id="3925a-109">In order toosave a report you first need toocreate a token for hello specific report with hello right scopes:</span></span>

* <span data-ttu-id="3925a-110">tooenable сохранить Report.ReadWrite область является обязательным</span><span class="sxs-lookup"><span data-stu-id="3925a-110">tooenable save Report.ReadWrite scope is required</span></span>
* <span data-ttu-id="3925a-111">tooenable Сохранить как Report.Read и Workspace.Report.Copy областей являются обязательными</span><span class="sxs-lookup"><span data-stu-id="3925a-111">tooenable save as, Report.Read and Workspace.Report.Copy scopes are required</span></span>
* <span data-ttu-id="3925a-112">Сохранить tooenable и сохранить как, Report.ReadWrite и Workspace.Report.Copy будут requierd</span><span class="sxs-lookup"><span data-stu-id="3925a-112">tooenable save and save as, Report.ReadWrite and Workspace.Report.Copy are requierd</span></span>

<span data-ttu-id="3925a-113">Соответственно в порядке tooenable hello правой сохранения и сохранения как кнопки в меню "файл" требуется tooprovide hello правой разрешение в конфигурации внедрения hello при можно внедрить hello отчета:</span><span class="sxs-lookup"><span data-stu-id="3925a-113">Respectively in order tooenable hello right save/save as buttons in file menu you need tooprovide hello right permission in hello Embed configuration when you Embed hello report:</span></span>

* <span data-ttu-id="3925a-114">models.Permissions.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="3925a-114">models.Permissions.ReadWrite</span></span>
* <span data-ttu-id="3925a-115">models.Permissions.Copy</span><span class="sxs-lookup"><span data-stu-id="3925a-115">models.Permissions.Copy</span></span>
* <span data-ttu-id="3925a-116">models.Permissions.All</span><span class="sxs-lookup"><span data-stu-id="3925a-116">models.Permissions.All</span></span>

> [!NOTE]
> <span data-ttu-id="3925a-117">Срок действия токена доступа также должен hello соответствующие области.</span><span class="sxs-lookup"><span data-stu-id="3925a-117">Your access token also needs hello appropriate scopes.</span></span> <span data-ttu-id="3925a-118">Дополнительные сведения см. в разделе [Области](power-bi-embedded-app-token-flow.md#scopes).</span><span class="sxs-lookup"><span data-stu-id="3925a-118">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

## <a name="embed-report-in-edit-mode"></a><span data-ttu-id="3925a-119">Внедрение отчета в режиме правки</span><span class="sxs-lookup"><span data-stu-id="3925a-119">Embed report in edit mode</span></span>

<span data-ttu-id="3925a-120">Давайте предположим нужно tooEmbed отчетов в режиме редактирования, внутри приложения, toodo, поэтому просто передать свойства прав hello в конфигурации внедрения и вызвать powerbi.embed().</span><span class="sxs-lookup"><span data-stu-id="3925a-120">Let's say you want tooEmbed a report in edit mode inside your app, toodo so just pass hello right properties in Embed configuration and call powerbi.embed().</span></span> <span data-ttu-id="3925a-121">Необходимо будет toosupply разрешения и viewMode в hello toosee порядок сохранения и сохраните как кнопки в режиме редактирования.</span><span class="sxs-lookup"><span data-stu-id="3925a-121">You will need toosupply permissions and a viewMode in order toosee hello save and save as buttons when in edit mode.</span></span> <span data-ttu-id="3925a-122">Дополнительные сведения см. в статье [Embed Configuration Details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details) (Сведения о конфигурации внедрения).</span><span class="sxs-lookup"><span data-stu-id="3925a-122">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="3925a-123">Например, в JavaScript:</span><span class="sxs-lookup"><span data-stu-id="3925a-123">For example in JavaScript:</span></span>

```
   <div id="reportContainer"></div>

    // Get models. Models, it contains enums that can be used.
    var models = window['powerbi-client'].models;

    // Embed configuration used toodescribe hello what and how tooembed.
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

    // Get a reference toohello embedded report HTML element
    var reportContainer = $('#reportContainer')[0];

    // Embed hello report and display it within hello div container.
    var report = powerbi.embed(reportContainer, config);
```

<span data-ttu-id="3925a-124">Теперь отчет будет внедрен в приложение в режиме правки.</span><span class="sxs-lookup"><span data-stu-id="3925a-124">Now a report will be embedded in your app in edit mode.</span></span>

## <a name="save-report"></a><span data-ttu-id="3925a-125">Сохранение отчета</span><span class="sxs-lookup"><span data-stu-id="3925a-125">Save report</span></span>

<span data-ttu-id="3925a-126">После изменения отчета hello Embbeding в режиме с правом маркера hello и разрешения можно сохранить hello отчетов из меню "файл" hello, или из кода javascript:</span><span class="sxs-lookup"><span data-stu-id="3925a-126">After Embbeding hello report in edit mode with hello right token and permissions you can save hello report from hello file menu or from javascript:</span></span>

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a><span data-ttu-id="3925a-127">Сохранить как</span><span class="sxs-lookup"><span data-stu-id="3925a-127">Save as</span></span>

```
// Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> <span data-ttu-id="3925a-128">Создание отчета завершается только после выполнения команды *Сохранить как*.</span><span class="sxs-lookup"><span data-stu-id="3925a-128">Only after *save as* is a new report created.</span></span> <span data-ttu-id="3925a-129">После сохранения hello, hello холст по-прежнему отображаются hello старого отчета в изменить режим и не hello новый отчет.</span><span class="sxs-lookup"><span data-stu-id="3925a-129">After hello save, hello canvas is still showing hello old report in edit mode and not hello new report.</span></span> <span data-ttu-id="3925a-130">Вам потребуется tooembed hello новый отчет был создан.</span><span class="sxs-lookup"><span data-stu-id="3925a-130">You will need tooembed hello new report that was created.</span></span> <span data-ttu-id="3925a-131">Для этого потребуется новый маркер доступа, так как они создаются отдельно для каждого отчета.</span><span class="sxs-lookup"><span data-stu-id="3925a-131">This requires a new access token as they are created per report.</span></span>

<span data-ttu-id="3925a-132">Затем необходимо будет tooload hello новый отчет после *сохранение*.</span><span class="sxs-lookup"><span data-stu-id="3925a-132">You will then need tooload hello new report after a *save as*.</span></span> <span data-ttu-id="3925a-133">Это — примерно tooembedding любой отчет.</span><span class="sxs-lookup"><span data-stu-id="3925a-133">This is similar tooembedding any report.</span></span>

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="see-also"></a><span data-ttu-id="3925a-134">См. также</span><span class="sxs-lookup"><span data-stu-id="3925a-134">See also</span></span>

[<span data-ttu-id="3925a-135">Приступая к работе с примером Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="3925a-135">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="3925a-136">Внедрение отчета в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="3925a-136">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="3925a-137">Создание отчета из набора данных</span><span class="sxs-lookup"><span data-stu-id="3925a-137">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="3925a-138">Аутентификация и авторизация в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="3925a-138">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="3925a-139">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="3925a-139">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="3925a-140">Пример внедрения JavaScript</span><span class="sxs-lookup"><span data-stu-id="3925a-140">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="3925a-141">У вас имеются и другие вопросы?</span><span class="sxs-lookup"><span data-stu-id="3925a-141">More questions?</span></span> [<span data-ttu-id="3925a-142">Повторите hello сообщества Power BI</span><span class="sxs-lookup"><span data-stu-id="3925a-142">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

