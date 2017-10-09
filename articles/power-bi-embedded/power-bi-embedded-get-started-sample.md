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
# <a name="get-started-with-power-bi-embedded-sample"></a><span data-ttu-id="49488-103">Начало работы с примером Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="49488-103">Get started with Power BI Embedded sample</span></span>

<span data-ttu-id="49488-104">С помощью **Microsoft Power BI Embedded**можно интегрировать отчеты Power BI прямо в веб- или мобильные приложения.</span><span class="sxs-lookup"><span data-stu-id="49488-104">With **Microsoft Power BI Embedded**, you can integrate Power BI reports right into your web or mobile applications.</span></span> <span data-ttu-id="49488-105">В этой статье описываются toohello **Power BI Embedded** работы образца get.</span><span class="sxs-lookup"><span data-stu-id="49488-105">In this article, we'll introduce you toohello **Power BI Embedded** get started sample.</span></span>

<span data-ttu-id="49488-106">Прежде чем мы продолжим, вы, вероятно, захотите hello toosave следующие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="49488-106">Before we go any further, you'll probably want toosave hello following resources.</span></span> <span data-ttu-id="49488-107">Они поможем вам при слишком интеграции отчетов Power BI в пример приложения hello и собственных приложений.</span><span class="sxs-lookup"><span data-stu-id="49488-107">They'll help you when integrating Power BI reports into hello sample app and your own apps too.</span></span>

* [<span data-ttu-id="49488-108">Пример веб-приложения рабочей области</span><span class="sxs-lookup"><span data-stu-id="49488-108">Sample workspace web app</span></span>](http://go.microsoft.com/fwlink/?LinkId=761493)
* [<span data-ttu-id="49488-109">Справочник по API Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="49488-109">Power BI Embedded API reference</span></span>](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* <span data-ttu-id="49488-110">[Пакет SDK Power BI Embedded для .NET ](http://go.microsoft.com/fwlink/?LinkId=746472) (доступен в NuGet)</span><span class="sxs-lookup"><span data-stu-id="49488-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (available via NuGet)</span></span>
* [<span data-ttu-id="49488-111">Пример внедрения отчета JavaScript</span><span class="sxs-lookup"><span data-stu-id="49488-111">JavaScript Report Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> <span data-ttu-id="49488-112">Для настройки и выполнения hello Power BI Embedded получить пример работы, необходимо, чтобы toocreate по крайней мере один **коллекции рабочей** в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="49488-112">Before you can configure and run hello Power BI Embedded get started sample, you need toocreate at least one **Workspace Collection** in your Azure subscription.</span></span> <span data-ttu-id="49488-113">toolearn как toocreate **коллекции рабочей** в hello портала Azure. в разделе [Приступая к работе с Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="49488-113">toolearn how toocreate a **Workspace Collection** in hello Azure Portal see [Getting Started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="configure-hello-sample-app"></a><span data-ttu-id="49488-114">Настройка примера приложения hello</span><span class="sxs-lookup"><span data-stu-id="49488-114">Configure hello sample app</span></span>

<span data-ttu-id="49488-115">Давайте рассмотрим настройку Visual Studio development среды tooaccess hello компоненты необходимые toorun hello образца приложения.</span><span class="sxs-lookup"><span data-stu-id="49488-115">Let's walk through setting up your Visual Studio development environment tooaccess hello  components needed toorun hello sample app.</span></span>

1. <span data-ttu-id="49488-116">Загрузите и распакуйте hello [Power BI Embedded - интеграции отчета в веб-приложении](http://go.microsoft.com/fwlink/?LinkId=761493) на GitHub.</span><span class="sxs-lookup"><span data-stu-id="49488-116">Download and unzip hello [Power BI Embedded - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) sample on GitHub.</span></span>
2. <span data-ttu-id="49488-117">Откройте файл **PowerBI-embedded.sln** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="49488-117">Open **PowerBI-embedded.sln** in Visual Studio.</span></span> <span data-ttu-id="49488-118">Может потребоваться tooexecute hello **пакет обновления** в консоли диспетчера пакетов NuGET в пакетах hello tooupdate порядок, используемый в этом решении hello.</span><span class="sxs-lookup"><span data-stu-id="49488-118">You may need tooexecute hello **Update-Package** command in hello NuGET Package Manager Console in order tooupdate hello packages used in this solution.</span></span>
3. <span data-ttu-id="49488-119">Выполните сборку решения hello.</span><span class="sxs-lookup"><span data-stu-id="49488-119">Build hello solution.</span></span>
4. <span data-ttu-id="49488-120">Запустите hello **ProvisionSample** консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="49488-120">Run hello **ProvisionSample** console app.</span></span> <span data-ttu-id="49488-121">В консольном приложении образец hello подготовить рабочую область и импортируйте файл pbix-ФАЙЛ.</span><span class="sxs-lookup"><span data-stu-id="49488-121">In hello sample console app, you provision a workspace and import a PBIX file.</span></span>
5. <span data-ttu-id="49488-122">tooprovision новый **рабочей**, выберите параметр 1, **управления коллекции**, а затем выберите вариант 6, **подготовить новую рабочую область**</span><span class="sxs-lookup"><span data-stu-id="49488-122">tooprovision a new **Workspace**, select option 1, **Collection management**, and then select option 6, **Provision a new Workspace**</span></span>
6. <span data-ttu-id="49488-123">tooimport новый **отчетов**, выберите вариант 2, **отчетов управления**, а затем выберите вариант 3, **рабочего стола pbix-ФАЙЛ для импорта файла в рабочей области**.</span><span class="sxs-lookup"><span data-stu-id="49488-123">tooimport a new **Report**, select option 2, **Report management**, and then select option 3, **Import PBIX Desktop file into a workspace**.</span></span>

7. <span data-ttu-id="49488-124">Введите имя **коллекции рабочих областей** и **ключ доступа**.</span><span class="sxs-lookup"><span data-stu-id="49488-124">Enter your **Workspace Collection** name, and **Access Key**.</span></span> <span data-ttu-id="49488-125">Можно получить в виде hello **портала Azure**.</span><span class="sxs-lookup"><span data-stu-id="49488-125">You can get these in hello **Azure Portal**.</span></span> <span data-ttu-id="49488-126">Дополнительные сведения о том, как toolearn tooget вашей **ключ доступа**, см. [Просмотр ключей доступа к Power BI API](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) в начало работы с Microsoft Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="49488-126">toolearn more about how tooget your **Access Key**, see [View Power BI API Access Keys](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in Get started with Microsoft Power BI Embedded.</span></span>

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. <span data-ttu-id="49488-127">Скопируйте и сохраните только что созданный hello **идентификатор рабочей области** toouse далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="49488-127">Copy and save hello newly created **Workspace ID** toouse later in this article.</span></span> <span data-ttu-id="49488-128">После hello **идентификатор рабочей области** будет создан, его можно будет найти hello **портала Azure**.</span><span class="sxs-lookup"><span data-stu-id="49488-128">After hello **Workspace ID** is created, you can find it hello **Azure Portal**.</span></span>

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. <span data-ttu-id="49488-129">tooimport PBIX файла в вашей **рабочей**, выберите параметр **6. Импорт файла PBIX рабочего стола в существующую рабочую область**.</span><span class="sxs-lookup"><span data-stu-id="49488-129">tooimport a PBIX file into your **Workspace**, select option **6. Import PBIX Desktop file into an existing workspace**.</span></span> <span data-ttu-id="49488-130">Если у вас нет под рукой файл PBIX, можно загрузить hello [PBIX пример анализа розничной торговли](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="49488-130">If you don't have a PBIX file handy, you can download hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>
10. <span data-ttu-id="49488-131">При появлении запроса укажите понятное имя для своего **набора данных**.</span><span class="sxs-lookup"><span data-stu-id="49488-131">If prompted, enter a friendly name for your **Dataset**.</span></span>

<span data-ttu-id="49488-132">Вы должны получить примерно следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="49488-132">You should see a response like:</span></span>

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> <span data-ttu-id="49488-133">Если в pbix-файл содержит все подключения прямых запросов, запустите строки подключения параметр 7 tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="49488-133">If your PBIX file contains any direct query connections, run option 7 tooupdate hello connection strings.</span></span>

<span data-ttu-id="49488-134">На этом этапе у вас есть PBIX-файл отчета Power BI, импортированный в **рабочую область**.</span><span class="sxs-lookup"><span data-stu-id="49488-134">At this point, you have a Power BI PBIX report imported into your **Workspace**.</span></span> <span data-ttu-id="49488-135">Теперь давайте рассмотрим, как toorun hello **Power BI Embedded** получить работы образца веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="49488-135">Now, let's look at how toorun hello **Power BI Embedded** get started sample web app.</span></span>

## <a name="run-hello-sample-web-app"></a><span data-ttu-id="49488-136">Запустите hello образец веб-приложения</span><span class="sxs-lookup"><span data-stu-id="49488-136">Run hello sample web app</span></span>
<span data-ttu-id="49488-137">Пример веб-приложения Hello содержится образец приложения, подготавливает отчеты, которые импортируются в ваш **рабочей**.</span><span class="sxs-lookup"><span data-stu-id="49488-137">hello web app sample is a sample application that renders reports imported into your **Workspace**.</span></span> <span data-ttu-id="49488-138">Ниже показано, как tooconfigure hello примера веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="49488-138">Here's how tooconfigure hello web app sample.</span></span>

1. <span data-ttu-id="49488-139">В hello **внедренных PowerBI** решения Visual Studio, справа щелкните hello **EmbedSample** веб-приложение и выберите **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="49488-139">In hello **PowerBI-embedded** Visual Studio solution, right click hello **EmbedSample** web application, and choose **Set as StartUp project**.</span></span>
2. <span data-ttu-id="49488-140">В **web.config**, в hello **EmbedSample** веб-приложение, изменить hello **appSettings**: **AccessKey**,  **WorkspaceCollection** имя, и **ИД рабочей области**.</span><span class="sxs-lookup"><span data-stu-id="49488-140">In **web.config**, in hello **EmbedSample** web application, edit hello **appSettings**: **AccessKey**, **WorkspaceCollection** name, and **WorkspaceId**.</span></span>

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. <span data-ttu-id="49488-141">Запустите hello **EmbedSample** веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="49488-141">Run hello **EmbedSample** web application.</span></span>

<span data-ttu-id="49488-142">После выполнения hello **EmbedSample** веб-приложение hello левой навигационной панели должна содержать **отчеты** меню.</span><span class="sxs-lookup"><span data-stu-id="49488-142">Once you run hello **EmbedSample** web application, hello left navigation panel should contain a **Reports** menu.</span></span> <span data-ttu-id="49488-143">Разверните отчет hello tooview вы импортировали **отчетов**и щелкните отчет.</span><span class="sxs-lookup"><span data-stu-id="49488-143">tooview hello report you imported, expand **Reports**, and click a report.</span></span> <span data-ttu-id="49488-144">Если вы импортировали hello [PBIX пример анализа розничной торговли](http://go.microsoft.com/fwlink/?LinkID=780547), hello образец веб-приложение будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="49488-144">If you imported hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), hello sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

<span data-ttu-id="49488-145">После нажатия кнопки отчета hello **EmbedSample** веб-приложения должны выглядеть это:</span><span class="sxs-lookup"><span data-stu-id="49488-145">After you click a report, hello **EmbedSample** web application should look something this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-hello-sample-code"></a><span data-ttu-id="49488-146">Просмотр образца кода hello</span><span class="sxs-lookup"><span data-stu-id="49488-146">Explore hello sample code</span></span>

<span data-ttu-id="49488-147">Hello **Microsoft Power BI Embedded** образец представляет пример веб-приложения, которое показывает, как toointegrate **Power BI** отчеты в приложение.</span><span class="sxs-lookup"><span data-stu-id="49488-147">hello **Microsoft Power BI Embedded** sample is an example web app that shows you how toointegrate **Power BI** reports into your app.</span></span> <span data-ttu-id="49488-148">Она использует Model-View-Controller (MVC) разработать рекомендации по toodemonstrate шаблону.</span><span class="sxs-lookup"><span data-stu-id="49488-148">It uses a Model-View-Controller (MVC) design pattern toodemonstrate best practices.</span></span> <span data-ttu-id="49488-149">В этом разделе описываются части hello пример кода, который можно просмотреть в hello **PowerBI внедренных** веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="49488-149">This section highlights parts of hello sample code that you can explore within hello **PowerBI-embedded** web app solution.</span></span> <span data-ttu-id="49488-150">Hello шаблон Model-View-Controller (MVC) разделяет моделирования hello hello домена, презентации hello и hello действия в зависимости от входных данных пользователя в трех отдельных классов: модель, представление и управления.</span><span class="sxs-lookup"><span data-stu-id="49488-150">hello Model-View-Controller (MVC) pattern separates hello modeling of hello domain, hello presentation, and hello actions based on user input into three separate classes: Model, View, and Control.</span></span> <span data-ttu-id="49488-151">toolearn Дополнительные сведения о платформе MVC. в разделе [Дополнительные сведения о ASP.NET](http://www.asp.net/mvc).</span><span class="sxs-lookup"><span data-stu-id="49488-151">toolearn more about MVC, see [Learn About ASP.NET](http://www.asp.net/mvc).</span></span>

<span data-ttu-id="49488-152">Hello **Microsoft Power BI Embedded** образец кода отделен следующим образом.</span><span class="sxs-lookup"><span data-stu-id="49488-152">hello **Microsoft Power BI Embedded** sample code is separated as follows.</span></span> <span data-ttu-id="49488-153">Каждый раздел включает имя файла hello в hello решения PowerBI embedded.sln, чтобы можно было легко находить кода hello в образце hello.</span><span class="sxs-lookup"><span data-stu-id="49488-153">Each section includes hello file name in hello PowerBI-embedded.sln solution so that you can easily find hello code in hello sample.</span></span>

> [!NOTE]
> <span data-ttu-id="49488-154">В этом разделе приведена сводка примеров кода hello, показано, как при написании кода hello.</span><span class="sxs-lookup"><span data-stu-id="49488-154">This section is a summary of hello sample code that shows how hello code was written.</span></span> <span data-ttu-id="49488-155">hello tooview полный образец, загрузите hello PowerBI embedded.sln решения в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="49488-155">tooview hello complete sample, please load hello PowerBI-embedded.sln solution in Visual Studio.</span></span>

### <a name="model"></a><span data-ttu-id="49488-156">Модель</span><span class="sxs-lookup"><span data-stu-id="49488-156">Model</span></span>

<span data-ttu-id="49488-157">Образец Hello имеет **ReportsViewModel** и **ReportViewModel**.</span><span class="sxs-lookup"><span data-stu-id="49488-157">hello sample has a **ReportsViewModel** and **ReportViewModel**.</span></span>

<span data-ttu-id="49488-158">**ReportsViewModel.cs**: представляет отчеты Power BI.</span><span class="sxs-lookup"><span data-stu-id="49488-158">**ReportsViewModel.cs**: Represents Power BI Reports.</span></span>

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

<span data-ttu-id="49488-159">**ReportViewModel.cs**: представляет отчет Power BI.</span><span class="sxs-lookup"><span data-stu-id="49488-159">**ReportViewModel.cs**: Represents a Power BI Report.</span></span>

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a><span data-ttu-id="49488-160">Строка подключения</span><span class="sxs-lookup"><span data-stu-id="49488-160">Connection string</span></span>

<span data-ttu-id="49488-161">Строка подключения Hello должны быть hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="49488-161">hello connection string must be in hello following format:</span></span>

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

<span data-ttu-id="49488-162">Попытка использования общих атрибутов сервера и базы данных завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="49488-162">Using common server and database attributes will fail.</span></span> <span data-ttu-id="49488-163">Например: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span><span class="sxs-lookup"><span data-stu-id="49488-163">For example: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span></span>

### <a name="view"></a><span data-ttu-id="49488-164">Просмотр</span><span class="sxs-lookup"><span data-stu-id="49488-164">View</span></span>

<span data-ttu-id="49488-165">Hello **представление** управляет отображением hello Power BI **отчеты** и Power BI **отчета**.</span><span class="sxs-lookup"><span data-stu-id="49488-165">hello **View** manages hello display of Power BI **Reports** and a Power BI **Report**.</span></span>

<span data-ttu-id="49488-166">**Reports.cshtml**: перебора **Model.Reports** toocreate **ActionLink**.</span><span class="sxs-lookup"><span data-stu-id="49488-166">**Reports.cshtml**: Iterate over **Model.Reports** toocreate an **ActionLink**.</span></span> <span data-ttu-id="49488-167">Hello **ActionLink** составляется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="49488-167">hello **ActionLink** is composed as follows:</span></span>

| <span data-ttu-id="49488-168">Часть</span><span class="sxs-lookup"><span data-stu-id="49488-168">Part</span></span> | <span data-ttu-id="49488-169">Описание</span><span class="sxs-lookup"><span data-stu-id="49488-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="49488-170">Название</span><span class="sxs-lookup"><span data-stu-id="49488-170">Title</span></span> |<span data-ttu-id="49488-171">Имя отчета hello.</span><span class="sxs-lookup"><span data-stu-id="49488-171">Name of hello Report.</span></span> |
| <span data-ttu-id="49488-172">QueryString</span><span class="sxs-lookup"><span data-stu-id="49488-172">QueryString</span></span> |<span data-ttu-id="49488-173">Toohello ссылку отчета.</span><span class="sxs-lookup"><span data-stu-id="49488-173">A link toohello Report ID.</span></span> |

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

<span data-ttu-id="49488-174">Report.cshtml: Задать hello **Model.AccessToken**, и лямбда-выражение для hello **PowerBIReportFor**.</span><span class="sxs-lookup"><span data-stu-id="49488-174">Report.cshtml: Set hello **Model.AccessToken**, and hello Lambda expression for **PowerBIReportFor**.</span></span>

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a><span data-ttu-id="49488-175">Controller</span><span class="sxs-lookup"><span data-stu-id="49488-175">Controller</span></span>

<span data-ttu-id="49488-176">**DashboardController.cs**: создает PowerBIClient, передающий **маркер приложения**.</span><span class="sxs-lookup"><span data-stu-id="49488-176">**DashboardController.cs**: Creates a PowerBIClient passing an **app token**.</span></span> <span data-ttu-id="49488-177">JSON Web Token (JWT) создается на основе hello **ключа подписи** tooget hello **учетные данные**.</span><span class="sxs-lookup"><span data-stu-id="49488-177">A JSON Web Token (JWT) is generated from hello **Signing Key** tooget hello **Credentials**.</span></span> <span data-ttu-id="49488-178">Hello **учетные данные** являются экземпляра используется toocreate **PowerBIClient**.</span><span class="sxs-lookup"><span data-stu-id="49488-178">hello **Credentials** are used toocreate an instance of **PowerBIClient**.</span></span> <span data-ttu-id="49488-179">После создания экземпляра **PowerBIClient** можно вызвать методы GetReports() и GetReportsAsync().</span><span class="sxs-lookup"><span data-stu-id="49488-179">Once you have an instance of **PowerBIClient**, you can call GetReports() and GetReportsAsync().</span></span>

<span data-ttu-id="49488-180">CreatePowerBIClient()</span><span class="sxs-lookup"><span data-stu-id="49488-180">CreatePowerBIClient()</span></span>

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

<span data-ttu-id="49488-181">ActionResult Reports()</span><span class="sxs-lookup"><span data-stu-id="49488-181">ActionResult Reports()</span></span>

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


<span data-ttu-id="49488-182">Задача<ActionResult> Report(string reportId)</span><span class="sxs-lookup"><span data-stu-id="49488-182">Task<ActionResult> Report(string reportId)</span></span>

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

### <a name="integrate-a-report-into-your-app"></a><span data-ttu-id="49488-183">Интеграция отчета в приложение</span><span class="sxs-lookup"><span data-stu-id="49488-183">Integrate a report into your app</span></span>

<span data-ttu-id="49488-184">После получения **отчетов**, используется **IFrame** tooembed hello Power BI **отчета**.</span><span class="sxs-lookup"><span data-stu-id="49488-184">Once you have a **Report**, you use an **IFrame** tooembed hello Power BI **Report**.</span></span> <span data-ttu-id="49488-185">Ниже приведен фрагмент кода из powerbi.js в hello **Microsoft Power BI Embedded** образца.</span><span class="sxs-lookup"><span data-stu-id="49488-185">Here is a code snippet from  powerbi.js in hello **Microsoft Power BI Embedded** sample.</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a><span data-ttu-id="49488-186">Фильтрация отчетов, внедренных в приложение</span><span class="sxs-lookup"><span data-stu-id="49488-186">Filter reports embedded in your application</span></span>

<span data-ttu-id="49488-187">Можно отфильтровать внедренный отчет, используя синтаксис URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="49488-187">You can filter an embedded report using a URL syntax.</span></span> <span data-ttu-id="49488-188">toodo, добавлении **$filter** параметр строки запроса с **eq** tooyour URL-адреса iFrame src с фильтром hello указан оператор.</span><span class="sxs-lookup"><span data-stu-id="49488-188">toodo this, you add a **$filter** query string parameter with an **eq** operator tooyour iFrame src url with hello filter specified.</span></span> <span data-ttu-id="49488-189">Ниже приведен синтаксис запроса фильтра hello.</span><span class="sxs-lookup"><span data-stu-id="49488-189">Here is hello filter query syntax:</span></span>

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> <span data-ttu-id="49488-190">{tableName/fieldName} не может содержать пробелы или специальные знаки.</span><span class="sxs-lookup"><span data-stu-id="49488-190">{tableName/fieldName} cannot include spaces or special characters.</span></span> <span data-ttu-id="49488-191">Hello {fieldValue} принимает одно значение категориальных.</span><span class="sxs-lookup"><span data-stu-id="49488-191">hello {fieldValue} accepts a single categorical value.</span></span>  

## <a name="see-also"></a><span data-ttu-id="49488-192">См. также</span><span class="sxs-lookup"><span data-stu-id="49488-192">See also</span></span>

[<span data-ttu-id="49488-193">Типичные сценарии использования Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="49488-193">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="49488-194">Аутентификация и авторизация в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="49488-194">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="49488-195">Внедрение отчета в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="49488-195">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="49488-196">Создание отчета из набора данных</span><span class="sxs-lookup"><span data-stu-id="49488-196">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="49488-197">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="49488-197">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="49488-198">Пример внедрения JavaScript</span><span class="sxs-lookup"><span data-stu-id="49488-198">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="49488-199">У вас имеются и другие вопросы?</span><span class="sxs-lookup"><span data-stu-id="49488-199">More questions?</span></span> [<span data-ttu-id="49488-200">Повторите hello сообщества Power BI</span><span class="sxs-lookup"><span data-stu-id="49488-200">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
