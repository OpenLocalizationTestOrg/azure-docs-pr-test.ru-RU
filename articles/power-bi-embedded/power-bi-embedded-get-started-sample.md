---
title: "aaaGet работу с примером"
description: "Power BI Embedded, используйте пакет SDK tooadd интерактивных отчетов Power BI в приложение бизнес-аналитики"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: d8a9ef78-ad4e-4bc7-9711-89172dc5c548
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/02/2017
ms.author: asaxton
ms.openlocfilehash: 1fef9dd8e0f734b748b930d3f85ad4b517d9661e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-power-bi-embedded-sample"></a>Начало работы с примером Microsoft Power BI Embedded

С помощью **Microsoft Power BI Embedded**можно интегрировать отчеты Power BI прямо в веб- или мобильные приложения. В этой статье описываются toohello **Power BI Embedded** работы образца get.

Прежде чем мы продолжим, вы, вероятно, захотите hello toosave следующие ресурсы. Они поможем вам при слишком интеграции отчетов Power BI в пример приложения hello и собственных приложений.

* [Пример веб-приложения рабочей области](http://go.microsoft.com/fwlink/?LinkId=761493)
* [Справочник по API Power BI Embedded](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* [Пакет SDK Power BI Embedded для .NET ](http://go.microsoft.com/fwlink/?LinkId=746472) (доступен в NuGet)
* [Пример внедрения отчета JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> Для настройки и выполнения hello Power BI Embedded получить пример работы, необходимо, чтобы toocreate по крайней мере один **коллекции рабочей** в вашей подписке Azure. toolearn как toocreate **коллекции рабочей** в hello портала Azure. в разделе [Приступая к работе с Power BI Embedded](power-bi-embedded-get-started.md).

## <a name="configure-hello-sample-app"></a>Настройка примера приложения hello

Давайте рассмотрим настройку Visual Studio development среды tooaccess hello компоненты необходимые toorun hello образца приложения.

1. Загрузите и распакуйте hello [Power BI Embedded - интеграции отчета в веб-приложении](http://go.microsoft.com/fwlink/?LinkId=761493) на GitHub.
2. Откройте файл **PowerBI-embedded.sln** в Visual Studio. Может потребоваться tooexecute hello **пакет обновления** в консоли диспетчера пакетов NuGET в пакетах hello tooupdate порядок, используемый в этом решении hello.
3. Выполните сборку решения hello.
4. Запустите hello **ProvisionSample** консольного приложения. В консольном приложении образец hello подготовить рабочую область и импортируйте файл pbix-ФАЙЛ.
5. tooprovision новый **рабочей**, выберите параметр 1, **управления коллекции**, а затем выберите вариант 6, **подготовить новую рабочую область**
6. tooimport новый **отчетов**, выберите вариант 2, **отчетов управления**, а затем выберите вариант 3, **рабочего стола pbix-ФАЙЛ для импорта файла в рабочей области**.

7. Введите имя **коллекции рабочих областей** и **ключ доступа**. Можно получить в виде hello **портала Azure**. Дополнительные сведения о том, как toolearn tooget вашей **ключ доступа**, см. [Просмотр ключей доступа к Power BI API](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) в начало работы с Microsoft Power BI Embedded.

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. Скопируйте и сохраните только что созданный hello **идентификатор рабочей области** toouse далее в этой статье. После hello **идентификатор рабочей области** будет создан, его можно будет найти hello **портала Azure**.

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. tooimport PBIX файла в вашей **рабочей**, выберите параметр **6. Импорт файла PBIX рабочего стола в существующую рабочую область**. Если у вас нет под рукой файл PBIX, можно загрузить hello [PBIX пример анализа розничной торговли](http://go.microsoft.com/fwlink/?LinkID=780547).
10. При появлении запроса укажите понятное имя для своего **набора данных**.

Вы должны получить примерно следующий ответ:

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> Если в pbix-файл содержит все подключения прямых запросов, запустите строки подключения параметр 7 tooupdate hello.

На этом этапе у вас есть PBIX-файл отчета Power BI, импортированный в **рабочую область**. Теперь давайте рассмотрим, как toorun hello **Power BI Embedded** получить работы образца веб-приложения.

## <a name="run-hello-sample-web-app"></a>Запустите hello образец веб-приложения
Пример веб-приложения Hello содержится образец приложения, подготавливает отчеты, которые импортируются в ваш **рабочей**. Ниже показано, как tooconfigure hello примера веб-приложения.

1. В hello **внедренных PowerBI** решения Visual Studio, справа щелкните hello **EmbedSample** веб-приложение и выберите **Назначить запускаемым проектом**.
2. В **web.config**, в hello **EmbedSample** веб-приложение, изменить hello **appSettings**: **AccessKey**,  **WorkspaceCollection** имя, и **ИД рабочей области**.

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. Запустите hello **EmbedSample** веб-приложения.

После выполнения hello **EmbedSample** веб-приложение hello левой навигационной панели должна содержать **отчеты** меню. Разверните отчет hello tooview вы импортировали **отчетов**и щелкните отчет. Если вы импортировали hello [PBIX пример анализа розничной торговли](http://go.microsoft.com/fwlink/?LinkID=780547), hello образец веб-приложение будет выглядеть следующим образом:

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

После нажатия кнопки отчета hello **EmbedSample** веб-приложения должны выглядеть это:

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-hello-sample-code"></a>Просмотр образца кода hello

Hello **Microsoft Power BI Embedded** образец представляет пример веб-приложения, которое показывает, как toointegrate **Power BI** отчеты в приложение. Она использует Model-View-Controller (MVC) разработать рекомендации по toodemonstrate шаблону. В этом разделе описываются части hello пример кода, который можно просмотреть в hello **PowerBI внедренных** веб-приложение. Hello шаблон Model-View-Controller (MVC) разделяет моделирования hello hello домена, презентации hello и hello действия в зависимости от входных данных пользователя в трех отдельных классов: модель, представление и управления. toolearn Дополнительные сведения о платформе MVC. в разделе [Дополнительные сведения о ASP.NET](http://www.asp.net/mvc).

Hello **Microsoft Power BI Embedded** образец кода отделен следующим образом. Каждый раздел включает имя файла hello в hello решения PowerBI embedded.sln, чтобы можно было легко находить кода hello в образце hello.

> [!NOTE]
> В этом разделе приведена сводка примеров кода hello, показано, как при написании кода hello. hello tooview полный образец, загрузите hello PowerBI embedded.sln решения в Visual Studio.

### <a name="model"></a>Модель

Образец Hello имеет **ReportsViewModel** и **ReportViewModel**.

**ReportsViewModel.cs**: представляет отчеты Power BI.

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

**ReportViewModel.cs**: представляет отчет Power BI.

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a>Строка подключения

Строка подключения Hello должны быть hello следующий формат:

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

Попытка использования общих атрибутов сервера и базы данных завершится ошибкой. Например: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,

### <a name="view"></a>Просмотр

Hello **представление** управляет отображением hello Power BI **отчеты** и Power BI **отчета**.

**Reports.cshtml**: перебора **Model.Reports** toocreate **ActionLink**. Hello **ActionLink** составляется следующим образом:

| Часть | Описание |
| --- | --- |
| Название |Имя отчета hello. |
| QueryString |Toohello ссылку отчета. |

    <div id="reports-nav" class="panel-collapse collapse">
        <div class="panel-body">
            <ul class="nav navbar-nav">
                @foreach (var report in Model.Reports)
                {
                    var reportClass = Request.QueryString["reportId"] == report.Id ? "active" : "";
                    <li class="@reportClass">
                        @Html.ActionLink(report.Name, "Report", new { reportId = report.Id })
                    </li>
                }
            </ul>
        </div>
    </div>

Report.cshtml: Задать hello **Model.AccessToken**, и лямбда-выражение для hello **PowerBIReportFor**.

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a>Controller

**DashboardController.cs**: создает PowerBIClient, передающий **маркер приложения**. JSON Web Token (JWT) создается на основе hello **ключа подписи** tooget hello **учетные данные**. Hello **учетные данные** являются экземпляра используется toocreate **PowerBIClient**. После создания экземпляра **PowerBIClient** можно вызвать методы GetReports() и GetReportsAsync().

CreatePowerBIClient()

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

ActionResult Reports()

    public ActionResult Reports()
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = client.Reports.GetReports(this.workspaceCollection, this.workspaceId);

            var viewModel = new ReportsViewModel
            {
                Reports = reportsResponse.Value.ToList()
            };

            return PartialView(viewModel);
        }
    }


Задача<ActionResult> Report(string reportId)

    public async Task<ActionResult> Report(string reportId)
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = await client.Reports.GetReportsAsync(this.workspaceCollection, this.workspaceId);
            var report = reportsResponse.Value.FirstOrDefault(r => r.Id == reportId);
            var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

            var viewModel = new ReportViewModel
            {
                Report = report,
                AccessToken = embedToken.Generate(this.accessKey)
            };

            return View(viewModel);
        }
    }

### <a name="integrate-a-report-into-your-app"></a>Интеграция отчета в приложение

После получения **отчетов**, используется **IFrame** tooembed hello Power BI **отчета**. Ниже приведен фрагмент кода из powerbi.js в hello **Microsoft Power BI Embedded** образца.

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a>Фильтрация отчетов, внедренных в приложение

Можно отфильтровать внедренный отчет, используя синтаксис URL-адреса. toodo, добавлении **$filter** параметр строки запроса с **eq** tooyour URL-адреса iFrame src с фильтром hello указан оператор. Ниже приведен синтаксис запроса фильтра hello.

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> {tableName/fieldName} не может содержать пробелы или специальные знаки. Hello {fieldValue} принимает одно значение категориальных.  

## <a name="see-also"></a>См. также

[Типичные сценарии использования Microsoft Power BI Embedded](power-bi-embedded-scenarios.md)  
[Аутентификация и авторизация в Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Внедрение отчета в Power BI Embedded](power-bi-embedded-embed-report.md)  
[Создание отчета из набора данных](power-bi-embedded-create-report-from-dataset.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Пример внедрения JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
У вас имеются и другие вопросы? [Повторите hello сообщества Power BI](http://community.powerbi.com/)
