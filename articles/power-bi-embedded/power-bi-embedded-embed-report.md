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
# <a name="embed-a-report-in-power-bi-embedded"></a>Внедрение отчета в Power BI Embedded

Узнайте, как tooembed к отчету, находящемуся в Power BI Embedded в приложение.

Мы рассмотрим, каким образом tooactually внедрения отчета в приложение. Предполагается, что у вас уже есть отчет, который находится в рабочей области в коллекции рабочих областей. Если вы еще не выполнили этот шаг, то см. статью [Начало работы с Microsoft Power BI Embedded](power-bi-embedded-get-started.md).

Можно использовать hello .NET (C#) или пакет SDK для Node.js, а также JavaScript, tooeasily сборки приложения с Power BI Embedded. 

## <a name="using-hello-access-keys-toouse-rest-apis"></a>С помощью toouse ключи доступа hello API-интерфейс REST

В порядке toocall hello REST API можно передать hello ключ доступа, который можно получить из hello портал Azure для коллекции данную рабочую область. Дополнительные сведения см. в статье [Начало работы с Microsoft Power BI Embedded](power-bi-embedded-get-started.md).

## <a name="get-a-report-id"></a>Получение идентификатора отчета

Каждый маркер доступа основан на отчете. Указанный идентификатор отчета для отчета hello, что требуется tooembed hello tooget потребуется. Это можно сделать на основе на вызовы toohello [Получение отчетов](https://msdn.microsoft.com/library/azure/mt711510.aspx) API-интерфейса REST. Возвращает идентификатор и hello внедрить URL-адрес отчета hello. Это можно сделать с помощью Power BI .NET SDK hello или прямой вызов API-интерфейса REST hello.

### <a name="using-hello-power-bi-net-sdk"></a>С помощью пакета SDK для .NET Power BI hello

При использовании hello .NET SDK, необходимо будет toocreate маркеров учетных данных, основанной на ключ доступа hello, получаемых из hello портал Azure. Для этого необходимо установить hello [пакет NuGet интерфейса API Power BI](https://www.nuget.org/profiles/powerbi).

**Установка пакета NuGet**

```
Install-Package Microsoft.PowerBI.Api
```

**Код C#**

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select hello report that you want toowork with from hello collection of reports.
```

### <a name="calling-hello-rest-api-directly"></a>Непосредственно hello вызова интерфейса API REST

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

## <a name="create-an-access-token"></a>Создание маркера доступа

Power BI Embedded использует маркеры внедрения, которые являются подписанными веб-маркерами JSON (JSON Web Token) с поддержкой HMAC. Hello токены подписываются с ключом доступа hello Azure Power BI Embedded коллекции рабочей области. Внедряйте маркеры, по умолчанию, являются используется tooprovide чтения доступ только к tooembed tooa отчета в приложение. Маркеры внедрения выдаются для конкретного отчета и должны быть связаны с URL-адресом внедрения.

Маркеры доступа должны создаваться на сервере hello как ключи доступа hello используется toosign на шифрование токенов hello. Сведения о том, как toocreate маркер доступа в разделе [аутентификации и авторизации с Power BI Embedded](power-bi-embedded-app-token-flow.md). Можно также просмотреть hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) метод. Ниже приведен пример этого она будет выглядеть подобно использованию hello .NET SDK для Power BI.

Идентификатор используется при hello отчетов, полученный ранее. После внедрения hello создается маркер, будет использоваться hello маркер hello доступа toogenerate ключа, который можно использовать с точки зрения hello javascript. Hello *класса PowerBIToken* необходимо установить hello [NuGut основного пакета для Power BI](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).

**Установка пакета NuGet**

```
Install-Package Microsoft.PowerBI.Core
```

**Код C#**

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-tooembed-tokens"></a>Добавление токенов tooembed разрешение области

При использовании маркеров внедрения, вы можете toorestrict использование hello ресурсы, которые обеспечивают доступ к. Для этого можно создать маркер с заданной областью разрешений. Дополнительные сведения см. в разделе [Области](power-bi-embedded-app-token-flow.md#scopes).

## <a name="embed-using-javascript"></a>Внедрение с помощью JavaScript

После получения маркера доступа hello и идентификатор hello отчета, мы внедрить hello отчетов с использованием JavaScript. Для этого необходимо установить hello nuget [пакета Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/). URL-адрес внедрения Hello станет https://embedded.powerbi.com/appTokenReportEmbed.

> [!NOTE]
> Можно использовать hello [пример внедрения отчета JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest функциональные возможности. Также приводятся примеры кода для hello различных операций, которые доступны.

**Установка пакета NuGet**

```
Install-Package Microsoft.PowerBI.JavaScript
```

**Код JavaScript**

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

### <a name="set-hello-size-of-embedded-elements"></a>Задать размер hello внедренные элементы

Hello отчета автоматически внедряются в зависимости от размера hello его контейнера. размер по умолчанию hello toooverride hello внедряет просто добавить класс атрибута или встроенные стили CSS для ширины и высоты.

## <a name="see-also"></a>См. также

[Приступая к работе с примером Microsoft Power BI Embedded](power-bi-embedded-get-started-sample.md)  
[Аутентификация и авторизация в Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[Пример внедрения JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Пакет NuGet для Power BI (JavaScript)](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
[Пакет NuGet для API Power BI](https://www.nuget.org/profiles/powerbi)
[Пакет NuGet для Power BI (Core)](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[Репозиторий PowerBI-CSharp на сайте GitHub](https://github.com/Microsoft/PowerBI-CSharp)  
[Репозиторий PowerBI-Node на сайте GitHub](https://github.com/Microsoft/PowerBI-Node)  
У вас имеются и другие вопросы? [Повторите hello сообщества Power BI](http://community.powerbi.com/)
