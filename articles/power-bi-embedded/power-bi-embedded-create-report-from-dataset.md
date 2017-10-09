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
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a>Создание отчета из набора данных в Power BI Embedded

Отчеты Power BI Embedded теперь можно создавать из набора данных в собственном приложении. 

Hello метод проверки подлинности аналогичен внедрить toothat отчета. Он основан на токены доступа, определенных tooa набора данных. Маркеры, используемые для PowerBI.com, выдаются Azure Active Directory (AAD), а маркеры Power BI Embedded — самой службой.

При hello createing внедренный отчет, маркеры, выпущенные предназначены для конкретного набора данных. Токены должны быть связаны с hello внедрить URL-адрес на hello же tooensure элемент имеет уникальный токен. Чтобы toocreate отчет внедренный *Dataset.Read и Workspace.Report.Create* области должно быть указано в маркере доступа hello.

## <a name="create-access-token-needed-toocreate-new-report"></a>Создать новый отчет access token необходимые toocreate

Power BI Embedded использует маркеры внедрения, которые являются подписанными веб-маркерами JSON (JSON Web Token) с поддержкой HMAC. Hello токены подписываются с ключом доступа hello Azure Power BI Embedded коллекции рабочей области. Внедряйте маркеры, по умолчанию, являются используется tooprovide чтения доступ только к tooembed tooa отчета в приложение. Маркеры внедрения выдаются для конкретного отчета и должны быть связаны с URL-адресом внедрения.

Маркеры доступа должны создаваться на сервере hello как ключи доступа hello используется toosign на шифрование токенов hello. Сведения о том, как toocreate маркер доступа в разделе [аутентификации и авторизации с Power BI Embedded](power-bi-embedded-app-token-flow.md). Можно также просмотреть hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) метод. Ниже приведен пример этого она будет выглядеть подобно использованию hello .NET SDK для Power BI.

В этом примере у нас есть нашей идентификатор набора данных, мы хотим toocreat hello новый отчет на. Также нужны областей hello tooadd для *Dataset.Read и Workspace.Report.Create*.

Hello *класса PowerBIToken* необходимо установить hello [NuGut основного пакета для Power BI](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).

**Установка пакета NuGet**

```
Install-Package Microsoft.PowerBI.Core
```

**Код C#**

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a>Создание пустого отчета

В порядке toocreate нового отчета, создайте hello конфигурации необходимо указать. Оно должно включать токен доступа hello, URL-адрес внедрения hello и hello datasetID, мы хотим toocreate hello отчет. Для этого необходимо установить hello nuget [пакета Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/). URL-адрес внедрения Hello станет https://embedded.powerbi.com/appTokenReportEmbed.

> [!NOTE]
> Можно использовать hello [пример внедрения отчета JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest функциональные возможности. Также приводятся примеры кода для hello различных операций, которые доступны.

**Установка пакета NuGet**

```
Install-Package Microsoft.PowerBI.JavaScript
```

**Код JavaScript**

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

Вызов *powerbi.createReport()* сделает пустой холст в режиме редактирования отображаются внутри hello *div* элемента.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a>Сохранение новых отчетов

отчет Hello не фактически будет создан до вызова hello **сохранение** операции. Это можно сделать, используя меню "Файл" или JavaScript.

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
> Отчет создается только после вызова операции **Сохранить как**. После сохранения изменений, hello холст по-прежнему отображаться в отчете изменить режим и не hello hello набора данных. Необходимо будет tooreload hello нового отчета так же, как любой другой отчет.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-hello-new-report"></a>Загрузить новый отчет hello

В порядке toointeract с hello нового отчета необходимо tooembed его так же, как приложение hello внедряет обычного отчетов, а именно, новый маркер должен быть выдан для нового отчета hello приветствия, а затем вызов hello внедрить метод.

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

## <a name="automate-save-and-load-of-a-new-report-using-hello-saved-event"></a>Автоматизация сохранения и загрузки нового отчета с помощью события «сохранить» hello

В процессе hello tooautomate заказа «Сохранить как» и затем загрузив hello новый отчет, чтобы использовать hello события «сохранить». Это событие вызывается после завершения hello операции сохранения и возвращает объект Json, содержащий новый reportId hello, имя отчета, старый reportId hello (если таковое имело) и если hello была saveAs или сохранить.

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

процесс hello tooAutomate может прослушивать события «сохранить» hello, выполните новый reportId hello, создать новый маркер hello и внедрение hello нового отчета с ним.

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

## <a name="see-also"></a>См. также

[Приступая к работе с примером Microsoft Power BI Embedded](power-bi-embedded-get-started-sample.md)  
[Сохранение отчетов](power-bi-embedded-save-reports.md)  
[Внедрение отчета в Power BI Embedded](power-bi-embedded-embed-report.md)  
[Аутентификация и авторизация в Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Пример внедрения JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Пакет NuGet для Power BI (Core)](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[Пакет NuGet для Power BI (JavaScript)](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
У вас имеются и другие вопросы? [Повторите hello сообщества Power BI](http://community.powerbi.com/)
