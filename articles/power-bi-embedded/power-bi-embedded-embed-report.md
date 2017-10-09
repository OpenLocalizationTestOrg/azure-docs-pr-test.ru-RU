---
title: "aaaEmbed отчета в Azure Power BI Embedded | Документы Microsoft"
description: "Узнайте, как tooembed к отчету, находящемуся в Power BI Embedded в приложение."
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
ms.openlocfilehash: f25344bbd0b9c092ef19da04d0b455d453b426a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="embed-a-report-in-power-bi-embedded"></a><span data-ttu-id="11f1c-103">Внедрение отчета в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="11f1c-103">Embed a report in Power BI Embedded</span></span>

<span data-ttu-id="11f1c-104">Узнайте, как tooembed к отчету, находящемуся в Power BI Embedded в приложение.</span><span class="sxs-lookup"><span data-stu-id="11f1c-104">Learn how tooembed a report that is in Power BI Embedded into your application.</span></span>

<span data-ttu-id="11f1c-105">Мы рассмотрим, каким образом tooactually внедрения отчета в приложение.</span><span class="sxs-lookup"><span data-stu-id="11f1c-105">We will look at how tooactually embed a report into your application.</span></span> <span data-ttu-id="11f1c-106">Предполагается, что у вас уже есть отчет, который находится в рабочей области в коллекции рабочих областей.</span><span class="sxs-lookup"><span data-stu-id="11f1c-106">This is assuming you already have a report that exists within a workspace in your workspace collection.</span></span> <span data-ttu-id="11f1c-107">Если вы еще не выполнили этот шаг, то см. статью [Начало работы с Microsoft Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="11f1c-107">If you haven't done that step yet, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

<span data-ttu-id="11f1c-108">Можно использовать hello .NET (C#) или пакет SDK для Node.js, а также JavaScript, tooeasily сборки приложения с Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="11f1c-108">You can use hello .NET (C#) or Node.js SDK, along with JavaScript, tooeasily build your application with Power BI Embedded.</span></span> 

## <a name="using-hello-access-keys-toouse-rest-apis"></a><span data-ttu-id="11f1c-109">С помощью toouse ключи доступа hello API-интерфейс REST</span><span class="sxs-lookup"><span data-stu-id="11f1c-109">Using hello access keys toouse REST APIs</span></span>

<span data-ttu-id="11f1c-110">В порядке toocall hello REST API можно передать hello ключ доступа, который можно получить из hello портал Azure для коллекции данную рабочую область.</span><span class="sxs-lookup"><span data-stu-id="11f1c-110">In order toocall hello REST API, you can pass hello access key which you can get from hello Azure portal for a given workspace collection.</span></span> <span data-ttu-id="11f1c-111">Дополнительные сведения см. в статье [Начало работы с Microsoft Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="11f1c-111">For more information, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="get-a-report-id"></a><span data-ttu-id="11f1c-112">Получение идентификатора отчета</span><span class="sxs-lookup"><span data-stu-id="11f1c-112">Get a report id</span></span>

<span data-ttu-id="11f1c-113">Каждый маркер доступа основан на отчете.</span><span class="sxs-lookup"><span data-stu-id="11f1c-113">Every access token is based on a report.</span></span> <span data-ttu-id="11f1c-114">Указанный идентификатор отчета для отчета hello, что требуется tooembed hello tooget потребуется.</span><span class="sxs-lookup"><span data-stu-id="11f1c-114">You will need tooget hello given report id for hello report that you want tooembed.</span></span> <span data-ttu-id="11f1c-115">Это можно сделать на основе на вызовы toohello [Получение отчетов](https://msdn.microsoft.com/library/azure/mt711510.aspx) API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="11f1c-115">This can be done based on calls toohello [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API.</span></span> <span data-ttu-id="11f1c-116">Возвращает идентификатор и hello внедрить URL-адрес отчета hello.</span><span class="sxs-lookup"><span data-stu-id="11f1c-116">This will return hello report id and hello embed url.</span></span> <span data-ttu-id="11f1c-117">Это можно сделать с помощью Power BI .NET SDK hello или прямой вызов API-интерфейса REST hello.</span><span class="sxs-lookup"><span data-stu-id="11f1c-117">This can be done using hello Power BI .NET SDK or calling hello REST API directly.</span></span>

### <a name="using-hello-power-bi-net-sdk"></a><span data-ttu-id="11f1c-118">С помощью пакета SDK для .NET Power BI hello</span><span class="sxs-lookup"><span data-stu-id="11f1c-118">Using hello Power BI .NET SDK</span></span>

<span data-ttu-id="11f1c-119">При использовании hello .NET SDK, необходимо будет toocreate маркеров учетных данных, основанной на ключ доступа hello, получаемых из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="11f1c-119">When using hello .NET SDK, you will need toocreate a token credential which is based on hello access key you get from hello Azure portal.</span></span> <span data-ttu-id="11f1c-120">Для этого необходимо установить hello [пакет NuGet интерфейса API Power BI](https://www.nuget.org/profiles/powerbi).</span><span class="sxs-lookup"><span data-stu-id="11f1c-120">This requires that you install hello [Power BI API NuGet package](https://www.nuget.org/profiles/powerbi).</span></span>

<span data-ttu-id="11f1c-121">**Установка пакета NuGet**</span><span class="sxs-lookup"><span data-stu-id="11f1c-121">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Api
```

<span data-ttu-id="11f1c-122">**Код C#**</span><span class="sxs-lookup"><span data-stu-id="11f1c-122">**C# code**</span></span>

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select hello report that you want toowork with from hello collection of reports.
```

### <a name="calling-hello-rest-api-directly"></a><span data-ttu-id="11f1c-123">Непосредственно hello вызова интерфейса API REST</span><span class="sxs-lookup"><span data-stu-id="11f1c-123">Calling hello REST API directly</span></span>

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response tooget hello report you want toowork with.
    }

}
```

## <a name="create-an-access-token"></a><span data-ttu-id="11f1c-124">Создание маркера доступа</span><span class="sxs-lookup"><span data-stu-id="11f1c-124">Create an access token</span></span>

<span data-ttu-id="11f1c-125">Power BI Embedded использует маркеры внедрения, которые являются подписанными веб-маркерами JSON (JSON Web Token) с поддержкой HMAC.</span><span class="sxs-lookup"><span data-stu-id="11f1c-125">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="11f1c-126">Hello токены подписываются с ключом доступа hello Azure Power BI Embedded коллекции рабочей области.</span><span class="sxs-lookup"><span data-stu-id="11f1c-126">hello tokens are signed with hello access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="11f1c-127">Внедряйте маркеры, по умолчанию, являются используется tooprovide чтения доступ только к tooembed tooa отчета в приложение.</span><span class="sxs-lookup"><span data-stu-id="11f1c-127">Embed tokens, by default, are used tooprovide read only access tooa report tooembed into an application.</span></span> <span data-ttu-id="11f1c-128">Маркеры внедрения выдаются для конкретного отчета и должны быть связаны с URL-адресом внедрения.</span><span class="sxs-lookup"><span data-stu-id="11f1c-128">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="11f1c-129">Маркеры доступа должны создаваться на сервере hello как ключи доступа hello используется toosign на шифрование токенов hello.</span><span class="sxs-lookup"><span data-stu-id="11f1c-129">Access tokens should be created on hello server as hello access keys are used toosign/encrypt hello tokens.</span></span> <span data-ttu-id="11f1c-130">Сведения о том, как toocreate маркер доступа в разделе [аутентификации и авторизации с Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="11f1c-130">For information on how toocreate an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="11f1c-131">Можно также просмотреть hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) метод.</span><span class="sxs-lookup"><span data-stu-id="11f1c-131">You can also review hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="11f1c-132">Ниже приведен пример этого она будет выглядеть подобно использованию hello .NET SDK для Power BI.</span><span class="sxs-lookup"><span data-stu-id="11f1c-132">Here is an example of what this would look like using hello .NET SDK for Power BI.</span></span>

<span data-ttu-id="11f1c-133">Идентификатор используется при hello отчетов, полученный ранее.</span><span class="sxs-lookup"><span data-stu-id="11f1c-133">You will use hello report id that you retrieved earlier.</span></span> <span data-ttu-id="11f1c-134">После внедрения hello создается маркер, будет использоваться hello маркер hello доступа toogenerate ключа, который можно использовать с точки зрения hello javascript.</span><span class="sxs-lookup"><span data-stu-id="11f1c-134">Once hello embed token is created, you will then use hello access key toogenerate hello token which you can use from hello javascript perspective.</span></span> <span data-ttu-id="11f1c-135">Hello *класса PowerBIToken* необходимо установить hello [NuGut основного пакета для Power BI](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="11f1c-135">hello *PowerBIToken class* requires that you install hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="11f1c-136">**Установка пакета NuGet**</span><span class="sxs-lookup"><span data-stu-id="11f1c-136">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="11f1c-137">**Код C#**</span><span class="sxs-lookup"><span data-stu-id="11f1c-137">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-tooembed-tokens"></a><span data-ttu-id="11f1c-138">Добавление токенов tooembed разрешение области</span><span class="sxs-lookup"><span data-stu-id="11f1c-138">Adding permission scopes tooembed tokens</span></span>

<span data-ttu-id="11f1c-139">При использовании маркеров внедрения, вы можете toorestrict использование hello ресурсы, которые обеспечивают доступ к.</span><span class="sxs-lookup"><span data-stu-id="11f1c-139">When using Embed tokens, you may want toorestrict usage of hello resources you give access to.</span></span> <span data-ttu-id="11f1c-140">Для этого можно создать маркер с заданной областью разрешений.</span><span class="sxs-lookup"><span data-stu-id="11f1c-140">For this reason, you can generate a token with scoped permissions.</span></span> <span data-ttu-id="11f1c-141">Дополнительные сведения см. в разделе [Области](power-bi-embedded-app-token-flow.md#scopes).</span><span class="sxs-lookup"><span data-stu-id="11f1c-141">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes)</span></span>

## <a name="embed-using-javascript"></a><span data-ttu-id="11f1c-142">Внедрение с помощью JavaScript</span><span class="sxs-lookup"><span data-stu-id="11f1c-142">Embed using JavaScript</span></span>

<span data-ttu-id="11f1c-143">После получения маркера доступа hello и идентификатор hello отчета, мы внедрить hello отчетов с использованием JavaScript.</span><span class="sxs-lookup"><span data-stu-id="11f1c-143">After you have hello access token and hello report id, we can embed hello report using JavaScript.</span></span> <span data-ttu-id="11f1c-144">Для этого необходимо установить hello nuget [пакета Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="11f1c-144">This requires that you install hello nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="11f1c-145">URL-адрес внедрения Hello станет https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="11f1c-145">hello embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="11f1c-146">Можно использовать hello [пример внедрения отчета JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="11f1c-146">You can use hello [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest functionality.</span></span> <span data-ttu-id="11f1c-147">Также приводятся примеры кода для hello различных операций, которые доступны.</span><span class="sxs-lookup"><span data-stu-id="11f1c-147">It also gives code examples for hello different operations that are available.</span></span>

<span data-ttu-id="11f1c-148">**Установка пакета NuGet**</span><span class="sxs-lookup"><span data-stu-id="11f1c-148">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="11f1c-149">**Код JavaScript**</span><span class="sxs-lookup"><span data-stu-id="11f1c-149">**JavaScript code**</span></span>

```
<script src="/scripts/powerbi.js"></script>
<div id="reportContainer"></div>

var embedConfiguration = {
    type: 'report',
    accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
    id: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed'
};

var $reportContainer = $('#reportContainer');
var report = powerbi.embed($reportContainer.get(0), embedConfiguration);
```

### <a name="set-hello-size-of-embedded-elements"></a><span data-ttu-id="11f1c-150">Задать размер hello внедренные элементы</span><span class="sxs-lookup"><span data-stu-id="11f1c-150">Set hello size of embedded elements</span></span>

<span data-ttu-id="11f1c-151">Hello отчета автоматически внедряются в зависимости от размера hello его контейнера.</span><span class="sxs-lookup"><span data-stu-id="11f1c-151">hello report will automatically be embedded based on hello size of its container.</span></span> <span data-ttu-id="11f1c-152">размер по умолчанию hello toooverride hello внедряет просто добавить класс атрибута или встроенные стили CSS для ширины и высоты.</span><span class="sxs-lookup"><span data-stu-id="11f1c-152">toooverride hello default size of hello embeds simply add a CSS class attribute or inline styles for width & height.</span></span>

## <a name="see-also"></a><span data-ttu-id="11f1c-153">См. также</span><span class="sxs-lookup"><span data-stu-id="11f1c-153">See also</span></span>

[<span data-ttu-id="11f1c-154">Приступая к работе с примером Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="11f1c-154">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="11f1c-155">Аутентификация и авторизация в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="11f1c-155">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="11f1c-156">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="11f1c-156">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="11f1c-157">Пример внедрения JavaScript</span><span class="sxs-lookup"><span data-stu-id="11f1c-157">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="11f1c-158">Пакет NuGet для Power BI (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="11f1c-158">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="11f1c-159">[Пакет NuGet для API Power BI](https://www.nuget.org/profiles/powerbi)
[Пакет NuGet для Power BI (Core)](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span><span class="sxs-lookup"><span data-stu-id="11f1c-159">[Power BI API NuGet package](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span></span>  
[<span data-ttu-id="11f1c-160">Репозиторий PowerBI-CSharp на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="11f1c-160">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="11f1c-161">Репозиторий PowerBI-Node на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="11f1c-161">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="11f1c-162">У вас имеются и другие вопросы?</span><span class="sxs-lookup"><span data-stu-id="11f1c-162">More questions?</span></span> [<span data-ttu-id="11f1c-163">Повторите hello сообщества Power BI</span><span class="sxs-lookup"><span data-stu-id="11f1c-163">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
