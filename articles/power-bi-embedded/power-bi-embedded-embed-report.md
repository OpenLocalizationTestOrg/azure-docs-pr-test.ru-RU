---
title: "Внедрение отчета в Azure Power BI Embedded | Документация Майкрософт"
description: "Узнайте, как внедрить отчет Azure Power BI Embedded в приложение."
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
ms.openlocfilehash: 3d865af2418c9c557c861a379766a125d75cebf1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="embed-a-report-in-power-bi-embedded"></a><span data-ttu-id="7edf2-103">Внедрение отчета в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="7edf2-103">Embed a report in Power BI Embedded</span></span>

<span data-ttu-id="7edf2-104">Узнайте, как внедрить отчет Azure Power BI Embedded в приложение.</span><span class="sxs-lookup"><span data-stu-id="7edf2-104">Learn how to embed a report that is in Power BI Embedded into your application.</span></span>

<span data-ttu-id="7edf2-105">В этой статье мы рассмотрим, как внедрить в приложение отчет.</span><span class="sxs-lookup"><span data-stu-id="7edf2-105">We will look at how to actually embed a report into your application.</span></span> <span data-ttu-id="7edf2-106">Предполагается, что у вас уже есть отчет, который находится в рабочей области в коллекции рабочих областей.</span><span class="sxs-lookup"><span data-stu-id="7edf2-106">This is assuming you already have a report that exists within a workspace in your workspace collection.</span></span> <span data-ttu-id="7edf2-107">Если вы еще не выполнили этот шаг, то см. статью [Начало работы с Microsoft Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7edf2-107">If you haven't done that step yet, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

<span data-ttu-id="7edf2-108">Можно воспользоваться пакетом SDK для .NET (C#) или Node.js, параллельно с JavaScript, чтобы быстро интегрировать в свое приложение службу Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="7edf2-108">You can use the .NET (C#) or Node.js SDK, along with JavaScript, to easily build your application with Power BI Embedded.</span></span> 

## <a name="using-the-access-keys-to-use-rest-apis"></a><span data-ttu-id="7edf2-109">Использование ключей доступа для интерфейсов REST API</span><span class="sxs-lookup"><span data-stu-id="7edf2-109">Using the access keys to use REST APIs</span></span>

<span data-ttu-id="7edf2-110">Чтобы вызвать REST API, можно передать ключ доступа, который получается на портале Azure для заданной коллекции рабочих областей.</span><span class="sxs-lookup"><span data-stu-id="7edf2-110">In order to call the REST API, you can pass the access key which you can get from the Azure portal for a given workspace collection.</span></span> <span data-ttu-id="7edf2-111">Дополнительные сведения см. в статье [Начало работы с Microsoft Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7edf2-111">For more information, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="get-a-report-id"></a><span data-ttu-id="7edf2-112">Получение идентификатора отчета</span><span class="sxs-lookup"><span data-stu-id="7edf2-112">Get a report id</span></span>

<span data-ttu-id="7edf2-113">Каждый маркер доступа основан на отчете.</span><span class="sxs-lookup"><span data-stu-id="7edf2-113">Every access token is based on a report.</span></span> <span data-ttu-id="7edf2-114">Необходимо получить данный идентификатор для отчета, который требуется внедрить.</span><span class="sxs-lookup"><span data-stu-id="7edf2-114">You will need to get the given report id for the report that you want to embed.</span></span> <span data-ttu-id="7edf2-115">Это можно сделать на основе вызовов к интерфейсу REST API [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) (Получить отчеты).</span><span class="sxs-lookup"><span data-stu-id="7edf2-115">This can be done based on calls to the [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API.</span></span> <span data-ttu-id="7edf2-116">В результате будут возвращены идентификатор отчета и URL-адрес внедрения.</span><span class="sxs-lookup"><span data-stu-id="7edf2-116">This will return the report id and the embed url.</span></span> <span data-ttu-id="7edf2-117">Это можно сделать с помощью пакета SDK Power BI для .NET или прямого вызова REST API.</span><span class="sxs-lookup"><span data-stu-id="7edf2-117">This can be done using the Power BI .NET SDK or calling the REST API directly.</span></span>

### <a name="using-the-power-bi-net-sdk"></a><span data-ttu-id="7edf2-118">Использование пакета SDK Power BI для .NET</span><span class="sxs-lookup"><span data-stu-id="7edf2-118">Using the Power BI .NET SDK</span></span>

<span data-ttu-id="7edf2-119">При использовании пакета SDK для .NET необходимо создать учетные данные маркера, основанные на ключе доступа, который можно получить на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="7edf2-119">When using the .NET SDK, you will need to create a token credential which is based on the access key you get from the Azure portal.</span></span> <span data-ttu-id="7edf2-120">Для этого необходимо установить [пакет NuGet для API Power BI](https://www.nuget.org/profiles/powerbi).</span><span class="sxs-lookup"><span data-stu-id="7edf2-120">This requires that you install the [Power BI API NuGet package](https://www.nuget.org/profiles/powerbi).</span></span>

<span data-ttu-id="7edf2-121">**Установка пакета NuGet**</span><span class="sxs-lookup"><span data-stu-id="7edf2-121">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Api
```

<span data-ttu-id="7edf2-122">**Код C#**</span><span class="sxs-lookup"><span data-stu-id="7edf2-122">**C# code**</span></span>

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select the report that you want to work with from the collection of reports.
```

### <a name="calling-the-rest-api-directly"></a><span data-ttu-id="7edf2-123">Прямой вызов REST API</span><span class="sxs-lookup"><span data-stu-id="7edf2-123">Calling the REST API directly</span></span>

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response to get the report you want to work with.
    }

}
```

## <a name="create-an-access-token"></a><span data-ttu-id="7edf2-124">Создание маркера доступа</span><span class="sxs-lookup"><span data-stu-id="7edf2-124">Create an access token</span></span>

<span data-ttu-id="7edf2-125">Power BI Embedded использует маркеры внедрения, которые являются подписанными веб-маркерами JSON (JSON Web Token) с поддержкой HMAC.</span><span class="sxs-lookup"><span data-stu-id="7edf2-125">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="7edf2-126">Маркеры подписываются с помощью ключа доступа из коллекции рабочих областей Azure Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="7edf2-126">The tokens are signed with the access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="7edf2-127">По умолчанию маркеры внедрения используются для предоставления доступа к отчету с правами только для чтения, чтобы внедрить его в приложение.</span><span class="sxs-lookup"><span data-stu-id="7edf2-127">Embed tokens, by default, are used to provide read only access to a report to embed into an application.</span></span> <span data-ttu-id="7edf2-128">Маркеры внедрения выдаются для конкретного отчета и должны быть связаны с URL-адресом внедрения.</span><span class="sxs-lookup"><span data-stu-id="7edf2-128">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="7edf2-129">Маркеры доступа должны создаваться на сервере, так как ключи доступа используются для подписания или шифрования маркеров.</span><span class="sxs-lookup"><span data-stu-id="7edf2-129">Access tokens should be created on the server as the access keys are used to sign/encrypt the tokens.</span></span> <span data-ttu-id="7edf2-130">Дополнительные сведения о создании маркера доступа см. в статье [Аутентификация и авторизация в Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="7edf2-130">For information on how to create an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="7edf2-131">Вы также можете ознакомиться с методом [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_).</span><span class="sxs-lookup"><span data-stu-id="7edf2-131">You can also review the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="7edf2-132">Здесь приведен пример с использованием пакета SDK для Power BI (.NET).</span><span class="sxs-lookup"><span data-stu-id="7edf2-132">Here is an example of what this would look like using the .NET SDK for Power BI.</span></span>

<span data-ttu-id="7edf2-133">Будет использоваться ранее полученный идентификатор отчета.</span><span class="sxs-lookup"><span data-stu-id="7edf2-133">You will use the report id that you retrieved earlier.</span></span> <span data-ttu-id="7edf2-134">После создания маркера внедрения воспользуйтесь ключом доступа для создания маркера, который вы сможете использовать в javascript.</span><span class="sxs-lookup"><span data-stu-id="7edf2-134">Once the embed token is created, you will then use the access key to generate the token which you can use from the javascript perspective.</span></span> <span data-ttu-id="7edf2-135">Для *класса PowerBIToken* необходимо установить [пакет NuGet для Power BI (Core)](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="7edf2-135">The *PowerBIToken class* requires that you install the [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="7edf2-136">**Установка пакета NuGet**</span><span class="sxs-lookup"><span data-stu-id="7edf2-136">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="7edf2-137">**Код C#**</span><span class="sxs-lookup"><span data-stu-id="7edf2-137">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-to-embed-tokens"></a><span data-ttu-id="7edf2-138">Добавление областей разрешений в маркеры внедрения</span><span class="sxs-lookup"><span data-stu-id="7edf2-138">Adding permission scopes to embed tokens</span></span>

<span data-ttu-id="7edf2-139">При использовании маркеров внедрения может потребоваться ограничить использование ресурсов, к которым предоставляется доступ.</span><span class="sxs-lookup"><span data-stu-id="7edf2-139">When using Embed tokens, you may want to restrict usage of the resources you give access to.</span></span> <span data-ttu-id="7edf2-140">Для этого можно создать маркер с заданной областью разрешений.</span><span class="sxs-lookup"><span data-stu-id="7edf2-140">For this reason, you can generate a token with scoped permissions.</span></span> <span data-ttu-id="7edf2-141">Дополнительные сведения см. в разделе [Области](power-bi-embedded-app-token-flow.md#scopes).</span><span class="sxs-lookup"><span data-stu-id="7edf2-141">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes)</span></span>

## <a name="embed-using-javascript"></a><span data-ttu-id="7edf2-142">Внедрение с помощью JavaScript</span><span class="sxs-lookup"><span data-stu-id="7edf2-142">Embed using JavaScript</span></span>

<span data-ttu-id="7edf2-143">Когда у вас уже есть маркер доступа и идентификатор отчета, можно внедрить отчет с помощью JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7edf2-143">After you have the access token and the report id, we can embed the report using JavaScript.</span></span> <span data-ttu-id="7edf2-144">Для этого необходимо установить [пакет NuGet для Power BI (JavaScript)](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="7edf2-144">This requires that you install the nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="7edf2-145">Параметр embedUrl будет иметь значение https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="7edf2-145">The embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="7edf2-146">Чтобы протестировать функциональные возможности, можно использовать [пример внедрения отчета JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/).</span><span class="sxs-lookup"><span data-stu-id="7edf2-146">You can use the [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) to test functionality.</span></span> <span data-ttu-id="7edf2-147">В нем также приводятся примеры кода для различных операций, которые доступны.</span><span class="sxs-lookup"><span data-stu-id="7edf2-147">It also gives code examples for the different operations that are available.</span></span>

<span data-ttu-id="7edf2-148">**Установка пакета NuGet**</span><span class="sxs-lookup"><span data-stu-id="7edf2-148">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="7edf2-149">**Код JavaScript**</span><span class="sxs-lookup"><span data-stu-id="7edf2-149">**JavaScript code**</span></span>

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

### <a name="set-the-size-of-embedded-elements"></a><span data-ttu-id="7edf2-150">Выбор размера внедряемых элементов</span><span class="sxs-lookup"><span data-stu-id="7edf2-150">Set the size of embedded elements</span></span>

<span data-ttu-id="7edf2-151">Отчет будет автоматически внедрен, исходя из размера его контейнера.</span><span class="sxs-lookup"><span data-stu-id="7edf2-151">The report will automatically be embedded based on the size of its container.</span></span> <span data-ttu-id="7edf2-152">Чтобы переопределить заданный по умолчанию размер внедряемых элементов, просто добавьте атрибут класса CSS или встроенные стили для ширины и высоты.</span><span class="sxs-lookup"><span data-stu-id="7edf2-152">To override the default size of the embeds simply add a CSS class attribute or inline styles for width & height.</span></span>

## <a name="see-also"></a><span data-ttu-id="7edf2-153">См. также</span><span class="sxs-lookup"><span data-stu-id="7edf2-153">See also</span></span>

[<span data-ttu-id="7edf2-154">Приступая к работе с примером Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="7edf2-154">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="7edf2-155">Аутентификация и авторизация в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="7edf2-155">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="7edf2-156">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="7edf2-156">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="7edf2-157">Пример внедрения JavaScript</span><span class="sxs-lookup"><span data-stu-id="7edf2-157">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="7edf2-158">Пакет NuGet для Power BI (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="7edf2-158">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="7edf2-159">[Пакет NuGet для API Power BI](https://www.nuget.org/profiles/powerbi)
[Пакет NuGet для Power BI (Core)](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span><span class="sxs-lookup"><span data-stu-id="7edf2-159">[Power BI API NuGet package](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span></span>  
[<span data-ttu-id="7edf2-160">Репозиторий PowerBI-CSharp на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="7edf2-160">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="7edf2-161">Репозиторий PowerBI-Node на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="7edf2-161">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="7edf2-162">У вас имеются и другие вопросы?</span><span class="sxs-lookup"><span data-stu-id="7edf2-162">More questions?</span></span> [<span data-ttu-id="7edf2-163">Попробуйте задать их в сообществе Power BI</span><span class="sxs-lookup"><span data-stu-id="7edf2-163">Try the Power BI Community</span></span>](http://community.powerbi.com/)
