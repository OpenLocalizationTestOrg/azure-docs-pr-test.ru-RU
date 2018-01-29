---
title: "Сохранение отчетов в коллекциях рабочих областей Power BI | Документация Майкрософт"
description: "Узнайте, как сохранять отчеты в коллекциях рабочих областей Power BI. Для выполнения этого действия необходимы соответствующие разрешения."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ROBOTS: NOINDEX
ms.assetid: 
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 09/20/2017
ms.author: asaxton
ms.openlocfilehash: 94a72ba4478aa317b4a1930b2894c1346d0590c1
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="save-reports-in-power-bi-workspace-collections"></a>Сохранение отчетов в коллекциях рабочих областей Power BI

Узнайте, как сохранять отчеты в коллекциях рабочих областей Power BI. Для сохранения отчетов необходимы соответствующие разрешения.

> [!IMPORTANT]
> Использовать службу "Коллекции рабочих областей Power BI" не рекомендуется. Она будет доступна до июня 2018 года или до даты, указанной в контракте. Мы советуем спланировать перенос в Power BI Embedded, чтобы избежать прерывания в работе приложения. Сведения о том, как перенести данные из коллекций рабочих областей Power BI в Power BI Embedded, см. в [этой статье](https://powerbi.microsoft.com/documentation/powerbi-developer-migrate-from-powerbi-embedded/).

В коллекциях рабочих областей Power BI можно изменить существующие отчеты и сохранить их. Также можно создать отчет и сохранить его как новый отчет.

Чтобы сохранить отчет, сначала необходимо создать маркер для определенного отчета с соответствующими областями:

* для использования команды "Сохранить" необходима область Report.ReadWrite;
* для использования команды "Сохранить как" необходимы области Report.Read и Workspace.Report.Copy;
* для использования команд "Сохранить" и "Сохранить как" необходимы области Report.ReadWrite и Workspace.Report.Copy.

Соответственно, чтобы правильно добавить в меню "Файл" кнопки "Сохранить" и "Сохранить как", при внедрении отчета необходимо предоставить правильные разрешения в конфигурации внедрения:

* models.Permissions.ReadWrite
* models.Permissions.Copy
* models.Permissions.All

> [!NOTE]
> Для маркера доступа также требуются соответствующие области. Дополнительные сведения см. в разделе [Области](app-token-flow.md#scopes).

## <a name="embed-report-in-edit-mode"></a>Внедрение отчета в режиме правки

Предположим, что вам требуется внедрить отчет в свое приложение в режиме правки. Для этого просто передайте необходимые свойства в конфигурацию внедрения и выполните вызов powerbi.embed(). Предоставьте разрешения и параметр viewMode, чтобы кнопки "Сохранить" и "Сохранить как" отображались в режиме правки. Дополнительные сведения см. в статье [Embed Configuration Details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details) (Сведения о конфигурации внедрения).

Например, в JavaScript:

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

Теперь отчет внедрен в приложение в режиме правки.

## <a name="save-report"></a>Сохранение отчета

После внедрения отчета в режиме правки с правильными разрешениями и маркером можно сохранить этот отчет, используя меню "Файл" или JavaScript.

```
 // Get a reference to the embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a>Сохранить как

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
> Создание отчета завершается только после выполнения команды *Сохранить как*. Если выбрать команду "Сохранить", то на холсте продолжает отображаться старый отчет в режиме правки, а не новый отчет. Внедрите отчет, который был создан. Для этого потребуется новый маркер доступа, так как они создаются отдельно для каждого отчета.

После выполнения команды *Сохранить как* необходимо будет загрузить новый отчет. Загрузка нового отчета аналогична процедуре внедрения любого отчета.

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

## <a name="see-also"></a>См. также

[Приступая к работе с примером Microsoft Power BI Embedded](get-started-sample.md)  
[Внедрение отчета в Power BI Embedded](embed-report.md)  
[Создание отчета из набора данных](create-report-from-dataset.md)  
[Аутентификация и авторизация в коллекциях рабочих областей Power BI](app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Пример внедрения JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  

У вас имеются и другие вопросы? [Попробуйте задать их в сообществе Power BI](http://community.powerbi.com/)

