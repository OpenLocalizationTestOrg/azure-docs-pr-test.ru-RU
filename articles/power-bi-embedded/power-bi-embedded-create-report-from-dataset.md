---
title: "Создание отчета из набора данных в Azure Power BI Embedded | Документация Майкрософт"
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
ms.openlocfilehash: 457f53aa76059dbb2faed6b264102f1f59b9918a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a><span data-ttu-id="00ca0-103">Создание отчета из набора данных в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="00ca0-103">Create a new report from a dataset in Power BI Embedded</span></span>

<span data-ttu-id="00ca0-104">Отчеты Power BI Embedded теперь можно создавать из набора данных в собственном приложении.</span><span class="sxs-lookup"><span data-stu-id="00ca0-104">Power BI Embedded reports can now be created from a dataset in your own application.</span></span> 

<span data-ttu-id="00ca0-105">Метод проверки подлинности аналогичен методу при внедрении запроса.</span><span class="sxs-lookup"><span data-stu-id="00ca0-105">The authentication method is similar to that of report embed.</span></span> <span data-ttu-id="00ca0-106">Он основан на маркерах доступа, относящихся к конкретному набору данных.</span><span class="sxs-lookup"><span data-stu-id="00ca0-106">It is based on access tokens that are specific to a dataset.</span></span> <span data-ttu-id="00ca0-107">Маркеры, используемые для PowerBI.com, выдаются Azure Active Directory (AAD), а маркеры Power BI Embedded — самой службой.</span><span class="sxs-lookup"><span data-stu-id="00ca0-107">Tokens used for PowerBI.com are issued by Azure Active Directory (AAD) and Power BI Embedded tokens are issued by your own service.</span></span>

<span data-ttu-id="00ca0-108">При создании внедренного отчета выдаваемые маркеры предназначены для конкретного набора данных.</span><span class="sxs-lookup"><span data-stu-id="00ca0-108">When createing an Embedded report, the tokens issued are for a specific dataset.</span></span> <span data-ttu-id="00ca0-109">Маркеры должны быть связаны с URL-адресом внедрения в том же элементе, чтобы каждый имел свой уникальный маркер.</span><span class="sxs-lookup"><span data-stu-id="00ca0-109">Tokens should be associated with the embed URL on the same element to ensure each has a unique token.</span></span> <span data-ttu-id="00ca0-110">Чтобы создать внедренный отчет, в маркере доступа необходимо предоставить области *Dataset.Read и Workspace.Report.Create*.</span><span class="sxs-lookup"><span data-stu-id="00ca0-110">In order to create an Embedded report, *Dataset.Read and Workspace.Report.Create* scopes must be provided in the access token.</span></span>

## <a name="create-access-token-needed-to-create-new-report"></a><span data-ttu-id="00ca0-111">Создание маркера доступа, необходимого для создания отчета</span><span class="sxs-lookup"><span data-stu-id="00ca0-111">Create access token needed to create new report</span></span>

<span data-ttu-id="00ca0-112">Power BI Embedded использует маркеры внедрения, которые являются подписанными веб-маркерами JSON (JSON Web Token) с поддержкой HMAC.</span><span class="sxs-lookup"><span data-stu-id="00ca0-112">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="00ca0-113">Маркеры подписываются с помощью ключа доступа из коллекции рабочих областей Azure Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="00ca0-113">The tokens are signed with the access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="00ca0-114">По умолчанию маркеры внедрения используются для предоставления доступа к отчету с правами только для чтения, чтобы внедрить его в приложение.</span><span class="sxs-lookup"><span data-stu-id="00ca0-114">Embed tokens, by default, are used to provide read only access to a report to embed into an application.</span></span> <span data-ttu-id="00ca0-115">Маркеры внедрения выдаются для конкретного отчета и должны быть связаны с URL-адресом внедрения.</span><span class="sxs-lookup"><span data-stu-id="00ca0-115">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="00ca0-116">Маркеры доступа должны создаваться на сервере, так как ключи доступа используются для подписания или шифрования маркеров.</span><span class="sxs-lookup"><span data-stu-id="00ca0-116">Access tokens should be created on the server as the access keys are used to sign/encrypt the tokens.</span></span> <span data-ttu-id="00ca0-117">Дополнительные сведения о создании маркера доступа см. в статье [Аутентификация и авторизация в Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="00ca0-117">For information on how to create an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="00ca0-118">Вы также можете ознакомиться с методом [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_).</span><span class="sxs-lookup"><span data-stu-id="00ca0-118">You can also review the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="00ca0-119">Здесь приведен пример с использованием пакета SDK для Power BI (.NET).</span><span class="sxs-lookup"><span data-stu-id="00ca0-119">Here is an example of what this would look like using the .NET SDK for Power BI.</span></span>

<span data-ttu-id="00ca0-120">В этом примере у нас есть идентификатор набора данных, на основе которого требуется создать отчет.</span><span class="sxs-lookup"><span data-stu-id="00ca0-120">In this example, we have our dataset id that we want to creat the new report on.</span></span> <span data-ttu-id="00ca0-121">Необходимо также добавить области *Dataset.Read и Workspace.Report.Create*.</span><span class="sxs-lookup"><span data-stu-id="00ca0-121">We also need to add the scopes for *Dataset.Read and Workspace.Report.Create*.</span></span>

<span data-ttu-id="00ca0-122">Для *класса PowerBIToken* необходимо установить [пакет NuGet для Power BI (Core)](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="00ca0-122">The *PowerBIToken class* requires that you install the [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="00ca0-123">**Установка пакета NuGet**</span><span class="sxs-lookup"><span data-stu-id="00ca0-123">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="00ca0-124">**Код C#**</span><span class="sxs-lookup"><span data-stu-id="00ca0-124">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a><span data-ttu-id="00ca0-125">Создание пустого отчета</span><span class="sxs-lookup"><span data-stu-id="00ca0-125">Create a new blank report</span></span>

<span data-ttu-id="00ca0-126">Чтобы создать отчет, необходимо предоставить конфигурацию создания.</span><span class="sxs-lookup"><span data-stu-id="00ca0-126">In order to create a new report, the create configuration should be provided.</span></span> <span data-ttu-id="00ca0-127">В нее входят маркер доступа, embedURL и datasetID, на основе которых требуется создать отчет.</span><span class="sxs-lookup"><span data-stu-id="00ca0-127">This should include the access token, the embedURL and the datasetID that we want to create the report against.</span></span> <span data-ttu-id="00ca0-128">Для этого необходимо установить [пакет NuGet для Power BI (JavaScript)](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="00ca0-128">This requires that you install the nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="00ca0-129">Параметр embedUrl будет иметь значение https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="00ca0-129">The embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="00ca0-130">Чтобы протестировать функциональные возможности, можно использовать [пример внедрения отчета JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/).</span><span class="sxs-lookup"><span data-stu-id="00ca0-130">You can use the [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) to test functionality.</span></span> <span data-ttu-id="00ca0-131">В нем также приводятся примеры кода для различных операций, которые доступны.</span><span class="sxs-lookup"><span data-stu-id="00ca0-131">It also gives code examples for the different operations that are available.</span></span>

<span data-ttu-id="00ca0-132">**Установка пакета NuGet**</span><span class="sxs-lookup"><span data-stu-id="00ca0-132">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="00ca0-133">**Код JavaScript**</span><span class="sxs-lookup"><span data-stu-id="00ca0-133">**JavaScript code**</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

<span data-ttu-id="00ca0-134">Вызов *powerbi.createReport()* приведет к тому, что пустой холст в режиме правки отобразится в элементе *div*.</span><span class="sxs-lookup"><span data-stu-id="00ca0-134">Calling *powerbi.createReport()* will make a blank canvas in edit mode appear within the *div* element.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a><span data-ttu-id="00ca0-135">Сохранение новых отчетов</span><span class="sxs-lookup"><span data-stu-id="00ca0-135">Save new reports</span></span>

<span data-ttu-id="00ca0-136">Отчет фактически не будет создан, пока вы не вызовите операцию **Сохранить как**.</span><span class="sxs-lookup"><span data-stu-id="00ca0-136">The report will not actually be created until you call the **save as** operation.</span></span> <span data-ttu-id="00ca0-137">Это можно сделать, используя меню "Файл" или JavaScript.</span><span class="sxs-lookup"><span data-stu-id="00ca0-137">This can be done from file menu or from JavaScript.</span></span>

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
> <span data-ttu-id="00ca0-138">Отчет создается только после вызова операции **Сохранить как**.</span><span class="sxs-lookup"><span data-stu-id="00ca0-138">A new report is created only after **save as** is called.</span></span> <span data-ttu-id="00ca0-139">После сохранения на холсте по-прежнему будет отображаться набор данных в режиме правки, а не отчет.</span><span class="sxs-lookup"><span data-stu-id="00ca0-139">After you save, the canvas will still show the dataset in edit mode and not the report.</span></span> <span data-ttu-id="00ca0-140">Необходимо перезагрузить новый отчет так же, как любой другой отчет.</span><span class="sxs-lookup"><span data-stu-id="00ca0-140">You will need to reload the new report like you would any other report.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-the-new-report"></a><span data-ttu-id="00ca0-141">Загрузка нового отчета</span><span class="sxs-lookup"><span data-stu-id="00ca0-141">Load the new report</span></span>

<span data-ttu-id="00ca0-142">Для взаимодействия с новым отчетом необходимо внедрить его таким же образом, как приложение внедряет обычный отчет. Таким образом, специально для нового отчета должен быть выдан новый маркер, а затем вызван метод embed.</span><span class="sxs-lookup"><span data-stu-id="00ca0-142">In order to interact with the new report you need to embed it in the same way the application embeds a regular report, meaning, a new token must be issued specifically for the new report and then call the embed method.</span></span>

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

## <a name="automate-save-and-load-of-a-new-report-using-the-saved-event"></a><span data-ttu-id="00ca0-143">Автоматизация сохранения и загрузки нового отчета с помощью "сохраненного" события</span><span class="sxs-lookup"><span data-stu-id="00ca0-143">Automate save and load of a new report using the "saved" event</span></span>

<span data-ttu-id="00ca0-144">Чтобы автоматизировать процесс "Сохранить как", а затем загрузить новый отчет, можно воспользоваться "сохраненным" событием.</span><span class="sxs-lookup"><span data-stu-id="00ca0-144">In order to automate the process of "save as" and then loading the new report you can make use of the "saved" Event.</span></span> <span data-ttu-id="00ca0-145">Это событие срабатывает, когда операция сохранения завершена и возвращает объект JSON, содержащий новый идентификатор reportId, имя отчета, старый идентификатор reportId (если он был), а также сведения об операции ("Сохранить как" или "Сохранить").</span><span class="sxs-lookup"><span data-stu-id="00ca0-145">This event is fired when the save operation is complete and it returns a Json object containing the new reportId, report name, the old reportId(if there was one) and if the operation was saveAs or save.</span></span>

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

<span data-ttu-id="00ca0-146">Для автоматизации процесса дождитесь передачи "сохраненного" события, возьмите из него новый идентификатор reportId, создайте маркер и внедрите новый отчет с этим маркером.</span><span class="sxs-lookup"><span data-stu-id="00ca0-146">To Automate the process you can listen on the "saved" event, take the new reportId, create the new token and embed the new report with it.</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints to Log window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that the application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide the wanted scopes*/);
        
        
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

## <a name="see-also"></a><span data-ttu-id="00ca0-147">См. также</span><span class="sxs-lookup"><span data-stu-id="00ca0-147">See also</span></span>

[<span data-ttu-id="00ca0-148">Приступая к работе с примером Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="00ca0-148">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="00ca0-149">Сохранение отчетов</span><span class="sxs-lookup"><span data-stu-id="00ca0-149">Save reports</span></span>](power-bi-embedded-save-reports.md)  
[<span data-ttu-id="00ca0-150">Внедрение отчета в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="00ca0-150">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="00ca0-151">Аутентификация и авторизация в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="00ca0-151">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="00ca0-152">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="00ca0-152">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="00ca0-153">Пример внедрения JavaScript</span><span class="sxs-lookup"><span data-stu-id="00ca0-153">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="00ca0-154">Пакет NuGet для Power BI (Core)</span><span class="sxs-lookup"><span data-stu-id="00ca0-154">Power BI Core NuGut Package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[<span data-ttu-id="00ca0-155">Пакет NuGet для Power BI (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="00ca0-155">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="00ca0-156">У вас имеются и другие вопросы?</span><span class="sxs-lookup"><span data-stu-id="00ca0-156">More questions?</span></span> [<span data-ttu-id="00ca0-157">Попробуйте задать их в сообществе Power BI</span><span class="sxs-lookup"><span data-stu-id="00ca0-157">Try the Power BI Community</span></span>](http://community.powerbi.com/)