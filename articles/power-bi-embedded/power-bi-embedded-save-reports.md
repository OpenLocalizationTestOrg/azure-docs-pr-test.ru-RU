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
# <a name="save-reports-in-power-bi-embedded"></a>Сохранение отчетов в Power BI Embedded

Узнайте, как внедренные toosave отчеты в Power BI. Это требует соответствующие разрешения в порядке toowork успешно.

В Power BI Embedded можно изменить существующие отчеты и сохранить их. Можно также создать новый отчет и сохранить как новый отчет toocreate, один.

В порядке toosave отчета необходимо сначала toocreate маркер для конкретного отчета hello hello правой области:

* tooenable сохранить Report.ReadWrite область является обязательным
* tooenable Сохранить как Report.Read и Workspace.Report.Copy областей являются обязательными
* Сохранить tooenable и сохранить как, Report.ReadWrite и Workspace.Report.Copy будут requierd

Соответственно в порядке tooenable hello правой сохранения и сохранения как кнопки в меню "файл" требуется tooprovide hello правой разрешение в конфигурации внедрения hello при можно внедрить hello отчета:

* models.Permissions.ReadWrite
* models.Permissions.Copy
* models.Permissions.All

> [!NOTE]
> Срок действия токена доступа также должен hello соответствующие области. Дополнительные сведения см. в разделе [Области](power-bi-embedded-app-token-flow.md#scopes).

## <a name="embed-report-in-edit-mode"></a>Внедрение отчета в режиме правки

Давайте предположим нужно tooEmbed отчетов в режиме редактирования, внутри приложения, toodo, поэтому просто передать свойства прав hello в конфигурации внедрения и вызвать powerbi.embed(). Необходимо будет toosupply разрешения и viewMode в hello toosee порядок сохранения и сохраните как кнопки в режиме редактирования. Дополнительные сведения см. в статье [Embed Configuration Details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details) (Сведения о конфигурации внедрения).

Например, в JavaScript:

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

Теперь отчет будет внедрен в приложение в режиме правки.

## <a name="save-report"></a>Сохранение отчета

После изменения отчета hello Embbeding в режиме с правом маркера hello и разрешения можно сохранить hello отчетов из меню "файл" hello, или из кода javascript:

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a>Сохранить как

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
> Создание отчета завершается только после выполнения команды *Сохранить как*. После сохранения hello, hello холст по-прежнему отображаются hello старого отчета в изменить режим и не hello новый отчет. Вам потребуется tooembed hello новый отчет был создан. Для этого потребуется новый маркер доступа, так как они создаются отдельно для каждого отчета.

Затем необходимо будет tooload hello новый отчет после *сохранение*. Это — примерно tooembedding любой отчет.

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

## <a name="see-also"></a>См. также

[Приступая к работе с примером Microsoft Power BI Embedded](power-bi-embedded-get-started-sample.md)  
[Внедрение отчета в Power BI Embedded](power-bi-embedded-embed-report.md)  
[Создание отчета из набора данных](power-bi-embedded-create-report-from-dataset.md)  
[Аутентификация и авторизация в Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Пример внедрения JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
У вас имеются и другие вопросы? [Повторите hello сообщества Power BI](http://community.powerbi.com/)

