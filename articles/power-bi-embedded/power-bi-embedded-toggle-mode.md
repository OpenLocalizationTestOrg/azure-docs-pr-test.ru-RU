---
title: "aaaToggle между режимами просмотра и изменения отчетов в Azure Power BI Embedded | Документы Microsoft"
description: "Узнайте, как tootoggle между режимами просмотра и изменения отчетов в Power BI Embedded."
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
ms.openlocfilehash: c9e3da5f9ae74d221af650adebde7c9d83b38a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="toggle-between-view-and-edit-mode-for-reports-in-power-bi-embedded"></a><span data-ttu-id="a7674-103">Переключение между режимами просмотра и правки отчетов в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="a7674-103">Toggle between view and edit mode for reports in Power BI Embedded</span></span>

<span data-ttu-id="a7674-104">Узнайте, как tootoggle между режимами просмотра и изменения отчетов в Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="a7674-104">Learn how tootoggle between view and edit mode for your reports within Power BI Embedded.</span></span>

## <a name="creating-an-access-token"></a><span data-ttu-id="a7674-105">Создание маркера доступа</span><span class="sxs-lookup"><span data-stu-id="a7674-105">Creating an access token</span></span>

<span data-ttu-id="a7674-106">Вам потребуется toocreate маркер доступа, позволяет hello возможность tooboth Просмотр и изменение отчета.</span><span class="sxs-lookup"><span data-stu-id="a7674-106">You will need toocreate an access token that gives you hello ability tooboth view and edit a report.</span></span> <span data-ttu-id="a7674-107">tooedit и сохраните отчет, необходимо будет hello **Report.ReadWrite** токен разрешение.</span><span class="sxs-lookup"><span data-stu-id="a7674-107">tooedit and save a report, you will need hello **Report.ReadWrite** token permission.</span></span> <span data-ttu-id="a7674-108">Дополнительные сведения см. в статье [Аутентификация и авторизация в Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="a7674-108">For more information, see [Authenticating and authorizing in Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a7674-109">Это позволят вам tooedit и сохранить изменения tooan существующего отчета.</span><span class="sxs-lookup"><span data-stu-id="a7674-109">This will allow you tooedit and save changes tooan existing report.</span></span> <span data-ttu-id="a7674-110">Если также требуется функции hello поддерживать **Сохранить как**, необходимо будет toosupply дополнительные разрешения.</span><span class="sxs-lookup"><span data-stu-id="a7674-110">If you would also like hello function of supporting **Save As**, you will need toosupply additional permissions.</span></span> <span data-ttu-id="a7674-111">Дополнительные сведения см. в разделе [Области](power-bi-embedded-app-token-flow.md#scopes).</span><span class="sxs-lookup"><span data-stu-id="a7674-111">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Report.ReadWrite";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="embed-configuration"></a><span data-ttu-id="a7674-112">Конфигурация внедрения</span><span class="sxs-lookup"><span data-stu-id="a7674-112">Embed configuration</span></span>

<span data-ttu-id="a7674-113">Потребуются разрешения toosupply и viewMode в hello toosee порядок сохранения кнопки в режиме редактирования.</span><span class="sxs-lookup"><span data-stu-id="a7674-113">You will need toosupply permissions and a viewMode in order toosee hello save button when in edit mode.</span></span> <span data-ttu-id="a7674-114">Дополнительные сведения см. в статье [Embed Configuration Details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details) (Сведения о конфигурации внедрения).</span><span class="sxs-lookup"><span data-stu-id="a7674-114">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="a7674-115">Например, в JavaScript:</span><span class="sxs-lookup"><span data-stu-id="a7674-115">For example in JavaScript:</span></span>

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
        permissions: models.Permissions.ReadWrite /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.View,
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

<span data-ttu-id="a7674-116">Это будет указывать tooembed hello отчетов в режиме представления на основе **viewMode** устанавливается слишком**моделей. ViewMode.View**.</span><span class="sxs-lookup"><span data-stu-id="a7674-116">This will indicate tooembed hello report in view mode based on **viewMode** being set too**models.ViewMode.View**.</span></span>

## <a name="view-mode"></a><span data-ttu-id="a7674-117">Режим просмотра</span><span class="sxs-lookup"><span data-stu-id="a7674-117">View mode</span></span>

<span data-ttu-id="a7674-118">Привет, следуя JavaScript tooswitch в режим просмотра, можно использовать при работе в режиме редактирования.</span><span class="sxs-lookup"><span data-stu-id="a7674-118">You can use hello following JavaScript tooswitch into view mode, if you are in edit mode.</span></span>

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooview mode.
report.switchMode("view");

```

## <a name="edit-mode"></a><span data-ttu-id="a7674-119">Режим правки</span><span class="sxs-lookup"><span data-stu-id="a7674-119">Edit mode</span></span>

<span data-ttu-id="a7674-120">Hello, следуя JavaScript tooswitch в режим редактирования, можно использовать при работе в представлении режиме.</span><span class="sxs-lookup"><span data-stu-id="a7674-120">You can use hello following JavaScript tooswitch into edit mode, if you are in view mode.</span></span>

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooedit mode.
report.switchMode("edit");

```

## <a name="see-also"></a><span data-ttu-id="a7674-121">См. также</span><span class="sxs-lookup"><span data-stu-id="a7674-121">See also</span></span>

[<span data-ttu-id="a7674-122">Приступая к работе с примером Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="a7674-122">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="a7674-123">Внедрение отчета в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="a7674-123">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="a7674-124">Аутентификация и авторизация в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="a7674-124">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="a7674-125">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="a7674-125">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="a7674-126">Пример внедрения JavaScript</span><span class="sxs-lookup"><span data-stu-id="a7674-126">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="a7674-127">Репозиторий PowerBI-CSharp на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="a7674-127">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="a7674-128">Репозиторий PowerBI-Node на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="a7674-128">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="a7674-129">У вас имеются и другие вопросы?</span><span class="sxs-lookup"><span data-stu-id="a7674-129">More questions?</span></span> [<span data-ttu-id="a7674-130">Повторите hello сообщества Power BI</span><span class="sxs-lookup"><span data-stu-id="a7674-130">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
