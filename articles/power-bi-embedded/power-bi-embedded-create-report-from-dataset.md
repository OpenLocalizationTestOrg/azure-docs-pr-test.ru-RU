---
title: "новый отчет из набора данных в Azure Power BI Embedded aaaCreate | Документы Microsoft"
description: "Отчеты Power BI Embedded теперь можно создавать из набора данных в собственном приложении."
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
ms.openlocfilehash: 41a0a52e4c833313f495bb5ff14749203fef9b41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a><span data-ttu-id="2ed4a-103">Создание отчета из набора данных в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="2ed4a-103">Create a new report from a dataset in Power BI Embedded</span></span>

<span data-ttu-id="2ed4a-104">Отчеты Power BI Embedded теперь можно создавать из набора данных в собственном приложении.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-104">Power BI Embedded reports can now be created from a dataset in your own application.</span></span> 

<span data-ttu-id="2ed4a-105">Hello метод проверки подлинности аналогичен внедрить toothat отчета.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-105">hello authentication method is similar toothat of report embed.</span></span> <span data-ttu-id="2ed4a-106">Он основан на токены доступа, определенных tooa набора данных.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-106">It is based on access tokens that are specific tooa dataset.</span></span> <span data-ttu-id="2ed4a-107">Маркеры, используемые для PowerBI.com, выдаются Azure Active Directory (AAD), а маркеры Power BI Embedded — самой службой.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-107">Tokens used for PowerBI.com are issued by Azure Active Directory (AAD) and Power BI Embedded tokens are issued by your own service.</span></span>

<span data-ttu-id="2ed4a-108">При hello createing внедренный отчет, маркеры, выпущенные предназначены для конкретного набора данных.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-108">When createing an Embedded report, hello tokens issued are for a specific dataset.</span></span> <span data-ttu-id="2ed4a-109">Токены должны быть связаны с hello внедрить URL-адрес на hello же tooensure элемент имеет уникальный токен.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-109">Tokens should be associated with hello embed URL on hello same element tooensure each has a unique token.</span></span> <span data-ttu-id="2ed4a-110">Чтобы toocreate отчет внедренный *Dataset.Read и Workspace.Report.Create* области должно быть указано в маркере доступа hello.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-110">In order toocreate an Embedded report, *Dataset.Read and Workspace.Report.Create* scopes must be provided in hello access token.</span></span>

## <a name="create-access-token-needed-toocreate-new-report"></a><span data-ttu-id="2ed4a-111">Создать новый отчет access token необходимые toocreate</span><span class="sxs-lookup"><span data-stu-id="2ed4a-111">Create access token needed toocreate new report</span></span>

<span data-ttu-id="2ed4a-112">Power BI Embedded использует маркеры внедрения, которые являются подписанными веб-маркерами JSON (JSON Web Token) с поддержкой HMAC.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-112">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="2ed4a-113">Hello токены подписываются с ключом доступа hello Azure Power BI Embedded коллекции рабочей области.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-113">hello tokens are signed with hello access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="2ed4a-114">Внедряйте маркеры, по умолчанию, являются используется tooprovide чтения доступ только к tooembed tooa отчета в приложение.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-114">Embed tokens, by default, are used tooprovide read only access tooa report tooembed into an application.</span></span> <span data-ttu-id="2ed4a-115">Маркеры внедрения выдаются для конкретного отчета и должны быть связаны с URL-адресом внедрения.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-115">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="2ed4a-116">Маркеры доступа должны создаваться на сервере hello как ключи доступа hello используется toosign на шифрование токенов hello.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-116">Access tokens should be created on hello server as hello access keys are used toosign/encrypt hello tokens.</span></span> <span data-ttu-id="2ed4a-117">Сведения о том, как toocreate маркер доступа в разделе [аутентификации и авторизации с Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="2ed4a-117">For information on how toocreate an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="2ed4a-118">Можно также просмотреть hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) метод.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-118">You can also review hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="2ed4a-119">Ниже приведен пример этого она будет выглядеть подобно использованию hello .NET SDK для Power BI.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-119">Here is an example of what this would look like using hello .NET SDK for Power BI.</span></span>

<span data-ttu-id="2ed4a-120">В этом примере у нас есть нашей идентификатор набора данных, мы хотим toocreat hello новый отчет на.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-120">In this example, we have our dataset id that we want toocreat hello new report on.</span></span> <span data-ttu-id="2ed4a-121">Также нужны областей hello tooadd для *Dataset.Read и Workspace.Report.Create*.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-121">We also need tooadd hello scopes for *Dataset.Read and Workspace.Report.Create*.</span></span>

<span data-ttu-id="2ed4a-122">Hello *класса PowerBIToken* необходимо установить hello [NuGut основного пакета для Power BI](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="2ed4a-122">hello *PowerBIToken class* requires that you install hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="2ed4a-123">**Установка пакета NuGet**</span><span class="sxs-lookup"><span data-stu-id="2ed4a-123">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="2ed4a-124">**Код C#**</span><span class="sxs-lookup"><span data-stu-id="2ed4a-124">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a><span data-ttu-id="2ed4a-125">Создание пустого отчета</span><span class="sxs-lookup"><span data-stu-id="2ed4a-125">Create a new blank report</span></span>

<span data-ttu-id="2ed4a-126">В порядке toocreate нового отчета, создайте hello конфигурации необходимо указать.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-126">In order toocreate a new report, hello create configuration should be provided.</span></span> <span data-ttu-id="2ed4a-127">Оно должно включать токен доступа hello, URL-адрес внедрения hello и hello datasetID, мы хотим toocreate hello отчет.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-127">This should include hello access token, hello embedURL and hello datasetID that we want toocreate hello report against.</span></span> <span data-ttu-id="2ed4a-128">Для этого необходимо установить hello nuget [пакета Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="2ed4a-128">This requires that you install hello nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="2ed4a-129">URL-адрес внедрения Hello станет https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-129">hello embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="2ed4a-130">Можно использовать hello [пример внедрения отчета JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-130">You can use hello [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest functionality.</span></span> <span data-ttu-id="2ed4a-131">Также приводятся примеры кода для hello различных операций, которые доступны.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-131">It also gives code examples for hello different operations that are available.</span></span>

<span data-ttu-id="2ed4a-132">**Установка пакета NuGet**</span><span class="sxs-lookup"><span data-stu-id="2ed4a-132">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="2ed4a-133">**Код JavaScript**</span><span class="sxs-lookup"><span data-stu-id="2ed4a-133">**JavaScript code**</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

<span data-ttu-id="2ed4a-134">Вызов *powerbi.createReport()* сделает пустой холст в режиме редактирования отображаются внутри hello *div* элемента.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-134">Calling *powerbi.createReport()* will make a blank canvas in edit mode appear within hello *div* element.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a><span data-ttu-id="2ed4a-135">Сохранение новых отчетов</span><span class="sxs-lookup"><span data-stu-id="2ed4a-135">Save new reports</span></span>

<span data-ttu-id="2ed4a-136">отчет Hello не фактически будет создан до вызова hello **сохранение** операции.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-136">hello report will not actually be created until you call hello **save as** operation.</span></span> <span data-ttu-id="2ed4a-137">Это можно сделать, используя меню "Файл" или JavaScript.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-137">This can be done from file menu or from JavaScript.</span></span>

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
> <span data-ttu-id="2ed4a-138">Отчет создается только после вызова операции **Сохранить как**.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-138">A new report is created only after **save as** is called.</span></span> <span data-ttu-id="2ed4a-139">После сохранения изменений, hello холст по-прежнему отображаться в отчете изменить режим и не hello hello набора данных.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-139">After you save, hello canvas will still show hello dataset in edit mode and not hello report.</span></span> <span data-ttu-id="2ed4a-140">Необходимо будет tooreload hello нового отчета так же, как любой другой отчет.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-140">You will need tooreload hello new report like you would any other report.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-hello-new-report"></a><span data-ttu-id="2ed4a-141">Загрузить новый отчет hello</span><span class="sxs-lookup"><span data-stu-id="2ed4a-141">Load hello new report</span></span>

<span data-ttu-id="2ed4a-142">В порядке toointeract с hello нового отчета необходимо tooembed его так же, как приложение hello внедряет обычного отчетов, а именно, новый маркер должен быть выдан для нового отчета hello приветствия, а затем вызов hello внедрить метод.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-142">In order toointeract with hello new report you need tooembed it in hello same way hello application embeds a regular report, meaning, a new token must be issued specifically for hello new report and then call hello embed method.</span></span>

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

## <a name="automate-save-and-load-of-a-new-report-using-hello-saved-event"></a><span data-ttu-id="2ed4a-143">Автоматизация сохранения и загрузки нового отчета с помощью события «сохранить» hello</span><span class="sxs-lookup"><span data-stu-id="2ed4a-143">Automate save and load of a new report using hello "saved" event</span></span>

<span data-ttu-id="2ed4a-144">В процессе hello tooautomate заказа «Сохранить как» и затем загрузив hello новый отчет, чтобы использовать hello события «сохранить».</span><span class="sxs-lookup"><span data-stu-id="2ed4a-144">In order tooautomate hello process of "save as" and then loading hello new report you can make use of hello "saved" Event.</span></span> <span data-ttu-id="2ed4a-145">Это событие вызывается после завершения hello операции сохранения и возвращает объект Json, содержащий новый reportId hello, имя отчета, старый reportId hello (если таковое имело) и если hello была saveAs или сохранить.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-145">This event is fired when hello save operation is complete and it returns a Json object containing hello new reportId, report name, hello old reportId(if there was one) and if hello operation was saveAs or save.</span></span>

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

<span data-ttu-id="2ed4a-146">процесс hello tooAutomate может прослушивать события «сохранить» hello, выполните новый reportId hello, создать новый маркер hello и внедрение hello нового отчета с ним.</span><span class="sxs-lookup"><span data-stu-id="2ed4a-146">tooAutomate hello process you can listen on hello "saved" event, take hello new reportId, create hello new token and embed hello new report with it.</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints tooLog window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that hello application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide hello wanted scopes*/);
        
        
    var embedConfiguration = {
        accessToken: newToken ,
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: newReportId,
    };

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
       
   // report.off removes a given event handler if it exists.
   report.off("saved");
    });
```

## <a name="see-also"></a><span data-ttu-id="2ed4a-147">См. также</span><span class="sxs-lookup"><span data-stu-id="2ed4a-147">See also</span></span>

[<span data-ttu-id="2ed4a-148">Приступая к работе с примером Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="2ed4a-148">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="2ed4a-149">Сохранение отчетов</span><span class="sxs-lookup"><span data-stu-id="2ed4a-149">Save reports</span></span>](power-bi-embedded-save-reports.md)  
[<span data-ttu-id="2ed4a-150">Внедрение отчета в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="2ed4a-150">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="2ed4a-151">Аутентификация и авторизация в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="2ed4a-151">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="2ed4a-152">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="2ed4a-152">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="2ed4a-153">Пример внедрения JavaScript</span><span class="sxs-lookup"><span data-stu-id="2ed4a-153">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="2ed4a-154">Пакет NuGet для Power BI (Core)</span><span class="sxs-lookup"><span data-stu-id="2ed4a-154">Power BI Core NuGut Package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[<span data-ttu-id="2ed4a-155">Пакет NuGet для Power BI (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="2ed4a-155">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="2ed4a-156">У вас имеются и другие вопросы?</span><span class="sxs-lookup"><span data-stu-id="2ed4a-156">More questions?</span></span> [<span data-ttu-id="2ed4a-157">Повторите hello сообщества Power BI</span><span class="sxs-lookup"><span data-stu-id="2ed4a-157">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
