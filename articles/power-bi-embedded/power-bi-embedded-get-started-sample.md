---
title: "Начало работы с примером"
description: "Power BI Embedded, использование пакета SDK для добавления интерактивных отчетов Power BI в приложение бизнес-аналитики"
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
ms.openlocfilehash: c3cb1763f807220a4a829f410d7eb77974b25776
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-power-bi-embedded-sample"></a><span data-ttu-id="bea10-103">Начало работы с примером Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="bea10-103">Get started with Power BI Embedded sample</span></span>

<span data-ttu-id="bea10-104">С помощью **Microsoft Power BI Embedded**можно интегрировать отчеты Power BI прямо в веб- или мобильные приложения.</span><span class="sxs-lookup"><span data-stu-id="bea10-104">With **Microsoft Power BI Embedded**, you can integrate Power BI reports right into your web or mobile applications.</span></span> <span data-ttu-id="bea10-105">В этой статье приведены общие сведения о примере для начала работы с **Power BI Embedded** .</span><span class="sxs-lookup"><span data-stu-id="bea10-105">In this article, we'll introduce you to the **Power BI Embedded** get started sample.</span></span>

<span data-ttu-id="bea10-106">Прежде чем мы продолжим, вам следует сохранить приведенные ниже ресурсы.</span><span class="sxs-lookup"><span data-stu-id="bea10-106">Before we go any further, you'll probably want to save the following resources.</span></span> <span data-ttu-id="bea10-107">Они помогут вам при интеграции отчетов Power BI в пример приложения, а также в собственные приложения.</span><span class="sxs-lookup"><span data-stu-id="bea10-107">They'll help you when integrating Power BI reports into the sample app and your own apps too.</span></span>

* [<span data-ttu-id="bea10-108">Пример веб-приложения рабочей области</span><span class="sxs-lookup"><span data-stu-id="bea10-108">Sample workspace web app</span></span>](http://go.microsoft.com/fwlink/?LinkId=761493)
* [<span data-ttu-id="bea10-109">Справочник по API Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="bea10-109">Power BI Embedded API reference</span></span>](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* <span data-ttu-id="bea10-110">[Пакет SDK Power BI Embedded для .NET ](http://go.microsoft.com/fwlink/?LinkId=746472) (доступен в NuGet)</span><span class="sxs-lookup"><span data-stu-id="bea10-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (available via NuGet)</span></span>
* [<span data-ttu-id="bea10-111">Пример внедрения отчета JavaScript</span><span class="sxs-lookup"><span data-stu-id="bea10-111">JavaScript Report Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> <span data-ttu-id="bea10-112">Перед настройкой и запуском примера Power BI Embedded необходимо создать по крайней мере одну **коллекцию рабочих областей** в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="bea10-112">Before you can configure and run the Power BI Embedded get started sample, you need to create at least one **Workspace Collection** in your Azure subscription.</span></span> <span data-ttu-id="bea10-113">Сведения о создании **коллекции рабочей области** на портале Azure см. в статье [Начало работы с Microsoft Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bea10-113">To learn how to create a **Workspace Collection** in the Azure Portal see [Getting Started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="configure-the-sample-app"></a><span data-ttu-id="bea10-114">Настройка примера приложения</span><span class="sxs-lookup"><span data-stu-id="bea10-114">Configure the sample app</span></span>

<span data-ttu-id="bea10-115">Давайте подробнее рассмотрим действия по настройке среды разработки Visual Studio для доступа к компонентам, необходимым для запуска примера приложения.</span><span class="sxs-lookup"><span data-stu-id="bea10-115">Let's walk through setting up your Visual Studio development environment to access the  components needed to run the sample app.</span></span>

1. <span data-ttu-id="bea10-116">Загрузите и распакуйте пример [Power BI Embedded — интеграция отчета в веб-приложение](http://go.microsoft.com/fwlink/?LinkId=761493) в GitHub.</span><span class="sxs-lookup"><span data-stu-id="bea10-116">Download and unzip the [Power BI Embedded - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) sample on GitHub.</span></span>
2. <span data-ttu-id="bea10-117">Откройте файл **PowerBI-embedded.sln** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bea10-117">Open **PowerBI-embedded.sln** in Visual Studio.</span></span> <span data-ttu-id="bea10-118">Может потребоваться выполнить команду **Update-Package** в консоли диспетчера пакетов NuGET, чтобы обновить пакеты, используемые в этом решении.</span><span class="sxs-lookup"><span data-stu-id="bea10-118">You may need to execute the **Update-Package** command in the NuGET Package Manager Console in order to update the packages used in this solution.</span></span>
3. <span data-ttu-id="bea10-119">Выполните сборку решения.</span><span class="sxs-lookup"><span data-stu-id="bea10-119">Build the solution.</span></span>
4. <span data-ttu-id="bea10-120">Запустите консольное приложение **ProvisionSample** .</span><span class="sxs-lookup"><span data-stu-id="bea10-120">Run the **ProvisionSample** console app.</span></span> <span data-ttu-id="bea10-121">В примере консольного приложения необходимо подготовить рабочую область и импортировать файл PBIX.</span><span class="sxs-lookup"><span data-stu-id="bea10-121">In the sample console app, you provision a workspace and import a PBIX file.</span></span>
5. <span data-ttu-id="bea10-122">Чтобы подготовить новую **рабочую область**, выберите параметр 1 — **Collection management** (Управление коллекциями), а затем параметр 6 — **Provision a new Workspace** (Подготовка новой рабочей области).</span><span class="sxs-lookup"><span data-stu-id="bea10-122">To provision a new **Workspace**, select option 1, **Collection management**, and then select option 6, **Provision a new Workspace**</span></span>
6. <span data-ttu-id="bea10-123">Чтобы импортировать новый **отчет**, выберите параметр 2 — **Report management** (Управление отчетами), а затем параметр 3 — **Import PBIX Desktop file into a workspace** (Импорт PBIX-файла рабочего стола в рабочую область).</span><span class="sxs-lookup"><span data-stu-id="bea10-123">To import a new **Report**, select option 2, **Report management**, and then select option 3, **Import PBIX Desktop file into a workspace**.</span></span>

7. <span data-ttu-id="bea10-124">Введите имя **коллекции рабочих областей** и **ключ доступа**.</span><span class="sxs-lookup"><span data-stu-id="bea10-124">Enter your **Workspace Collection** name, and **Access Key**.</span></span> <span data-ttu-id="bea10-125">Их можно получить на **портале Azure**.</span><span class="sxs-lookup"><span data-stu-id="bea10-125">You can get these in the **Azure Portal**.</span></span> <span data-ttu-id="bea10-126">Дополнительные сведения о том, как получить **ключ доступа**, см. в разделе [Просмотр ключей доступа для вызова API Power BI](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) статьи "Начало работы с Microsoft Power BI Embedded".</span><span class="sxs-lookup"><span data-stu-id="bea10-126">To learn more about how to get your **Access Key**, see [View Power BI API Access Keys](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in Get started with Microsoft Power BI Embedded.</span></span>

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. <span data-ttu-id="bea10-127">Скопируйте и сохраните созданный **идентификатор рабочей области** для дальнейшего использования в этой статье.</span><span class="sxs-lookup"><span data-stu-id="bea10-127">Copy and save the newly created **Workspace ID** to use later in this article.</span></span> <span data-ttu-id="bea10-128">После создания **идентификатора рабочей области** его можно найти на **портале Azure**.</span><span class="sxs-lookup"><span data-stu-id="bea10-128">After the **Workspace ID** is created, you can find it the **Azure Portal**.</span></span>

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. <span data-ttu-id="bea10-129">Чтобы импортировать PBIX-файл в свою **рабочую область**, выберите вариант **6. Импорт файла PBIX рабочего стола в существующую рабочую область**.</span><span class="sxs-lookup"><span data-stu-id="bea10-129">To import a PBIX file into your **Workspace**, select option **6. Import PBIX Desktop file into an existing workspace**.</span></span> <span data-ttu-id="bea10-130">Если у вас нет PBIX-файла, то можете скачать [PBIX-файл примера анализа розничной торговли](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="bea10-130">If you don't have a PBIX file handy, you can download the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>
10. <span data-ttu-id="bea10-131">При появлении запроса укажите понятное имя для своего **набора данных**.</span><span class="sxs-lookup"><span data-stu-id="bea10-131">If prompted, enter a friendly name for your **Dataset**.</span></span>

<span data-ttu-id="bea10-132">Вы должны получить примерно следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="bea10-132">You should see a response like:</span></span>

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> <span data-ttu-id="bea10-133">Если файл PBIX содержит подключения для прямых запросов, выберите вариант 7 для обновления строк подключения.</span><span class="sxs-lookup"><span data-stu-id="bea10-133">If your PBIX file contains any direct query connections, run option 7 to update the connection strings.</span></span>

<span data-ttu-id="bea10-134">На этом этапе у вас есть PBIX-файл отчета Power BI, импортированный в **рабочую область**.</span><span class="sxs-lookup"><span data-stu-id="bea10-134">At this point, you have a Power BI PBIX report imported into your **Workspace**.</span></span> <span data-ttu-id="bea10-135">Теперь рассмотрим, как запустить пример веб-приложения **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="bea10-135">Now, let's look at how to run the **Power BI Embedded** get started sample web app.</span></span>

## <a name="run-the-sample-web-app"></a><span data-ttu-id="bea10-136">Запуск примера веб-приложения</span><span class="sxs-lookup"><span data-stu-id="bea10-136">Run the sample web app</span></span>
<span data-ttu-id="bea10-137">Пример веб-приложения представляет собой приложение, в котором отображаются отчеты, импортированные в **рабочую область**.</span><span class="sxs-lookup"><span data-stu-id="bea10-137">The web app sample is a sample application that renders reports imported into your **Workspace**.</span></span> <span data-ttu-id="bea10-138">Вот как настроить пример веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="bea10-138">Here's how to configure the web app sample.</span></span>

1. <span data-ttu-id="bea10-139">В решении **PowerBI-embedded** Visual Studio щелкните веб-приложение **EmbedSample** правой кнопкой мыши и выберите **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="bea10-139">In the **PowerBI-embedded** Visual Studio solution, right click the **EmbedSample** web application, and choose **Set as StartUp project**.</span></span>
2. <span data-ttu-id="bea10-140">В файле **web.config** в веб-приложении **EmbedSample** измените параметры приложения **appSettings**: ключ доступа **AccessKey**, имя коллекции рабочих областей **WorkspaceCollection** и идентификатор рабочей области **WorkspaceId**.</span><span class="sxs-lookup"><span data-stu-id="bea10-140">In **web.config**, in the **EmbedSample** web application, edit the **appSettings**: **AccessKey**, **WorkspaceCollection** name, and **WorkspaceId**.</span></span>

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. <span data-ttu-id="bea10-141">Запустите веб-приложение **EmbedSample**.</span><span class="sxs-lookup"><span data-stu-id="bea10-141">Run the **EmbedSample** web application.</span></span>

<span data-ttu-id="bea10-142">После запуска веб-приложения **EmbedSample** в левой навигационной панели должно появиться меню **Отчеты**.</span><span class="sxs-lookup"><span data-stu-id="bea10-142">Once you run the **EmbedSample** web application, the left navigation panel should contain a **Reports** menu.</span></span> <span data-ttu-id="bea10-143">Чтобы просмотреть отчет, который был импортирован, разверните **Отчеты** и щелкните отчет.</span><span class="sxs-lookup"><span data-stu-id="bea10-143">To view the report you imported, expand **Reports**, and click a report.</span></span> <span data-ttu-id="bea10-144">Если вы импортировали [PBIX-файл примера анализа розничной торговли](http://go.microsoft.com/fwlink/?LinkID=780547), пример веб-приложения будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="bea10-144">If you imported the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), the sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

<span data-ttu-id="bea10-145">После выбора отчета веб-приложение **EmbedSample** должно выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="bea10-145">After you click a report, the **EmbedSample** web application should look something this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-the-sample-code"></a><span data-ttu-id="bea10-146">Изучение примера кода</span><span class="sxs-lookup"><span data-stu-id="bea10-146">Explore the sample code</span></span>

<span data-ttu-id="bea10-147">Пример **Microsoft Power BI Embedded** представляет собой веб-приложение и показывает, как интегрировать отчеты **Power BI** в приложение.</span><span class="sxs-lookup"><span data-stu-id="bea10-147">The **Microsoft Power BI Embedded** sample is an example web app that shows you how to integrate **Power BI** reports into your app.</span></span> <span data-ttu-id="bea10-148">Для демонстрации рекомендаций в нем используется шаблон проектирования "модель-представление-контроллер" (MVC).</span><span class="sxs-lookup"><span data-stu-id="bea10-148">It uses a Model-View-Controller (MVC) design pattern to demonstrate best practices.</span></span> <span data-ttu-id="bea10-149">В этом разделе описаны части примера кода, которые можно изучить в решении веб-приложения **PowerBI-embedded**.</span><span class="sxs-lookup"><span data-stu-id="bea10-149">This section highlights parts of the sample code that you can explore within the **PowerBI-embedded** web app solution.</span></span> <span data-ttu-id="bea10-150">Шаблон "модель-представление-контроллер" (MVC) разбивает модель домена, представление и действия на основе ввода пользователя на три различных класса: модель, представление и контроллер.</span><span class="sxs-lookup"><span data-stu-id="bea10-150">The Model-View-Controller (MVC) pattern separates the modeling of the domain, the presentation, and the actions based on user input into three separate classes: Model, View, and Control.</span></span> <span data-ttu-id="bea10-151">Дополнительные сведения о MVC см. в документации [ASP.NET](http://www.asp.net/mvc).</span><span class="sxs-lookup"><span data-stu-id="bea10-151">To learn more about MVC, see [Learn About ASP.NET](http://www.asp.net/mvc).</span></span>

<span data-ttu-id="bea10-152">Пример кода **Microsoft Power BI Embedded** разбивается следующим образом.</span><span class="sxs-lookup"><span data-stu-id="bea10-152">The **Microsoft Power BI Embedded** sample code is separated as follows.</span></span> <span data-ttu-id="bea10-153">Каждая часть включает имя файла для решения PowerBI-embedded.sln, поэтому вы легко найдете соответствующий код в примере.</span><span class="sxs-lookup"><span data-stu-id="bea10-153">Each section includes the file name in the PowerBI-embedded.sln solution so that you can easily find the code in the sample.</span></span>

> [!NOTE]
> <span data-ttu-id="bea10-154">В этом разделе приведены общие сведения о примере кода, которые показывают, как был написан этот код.</span><span class="sxs-lookup"><span data-stu-id="bea10-154">This section is a summary of the sample code that shows how the code was written.</span></span> <span data-ttu-id="bea10-155">Чтобы просмотреть полный пример, загрузите решение PowerBI-embedded.sln в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bea10-155">To view the complete sample, please load the PowerBI-embedded.sln solution in Visual Studio.</span></span>

### <a name="model"></a><span data-ttu-id="bea10-156">Модель</span><span class="sxs-lookup"><span data-stu-id="bea10-156">Model</span></span>

<span data-ttu-id="bea10-157">Пример содержит следующие модели: **ReportsViewModel** и **ReportViewModel**.</span><span class="sxs-lookup"><span data-stu-id="bea10-157">The sample has a **ReportsViewModel** and **ReportViewModel**.</span></span>

<span data-ttu-id="bea10-158">**ReportsViewModel.cs**: представляет отчеты Power BI.</span><span class="sxs-lookup"><span data-stu-id="bea10-158">**ReportsViewModel.cs**: Represents Power BI Reports.</span></span>

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

<span data-ttu-id="bea10-159">**ReportViewModel.cs**: представляет отчет Power BI.</span><span class="sxs-lookup"><span data-stu-id="bea10-159">**ReportViewModel.cs**: Represents a Power BI Report.</span></span>

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a><span data-ttu-id="bea10-160">Строка подключения</span><span class="sxs-lookup"><span data-stu-id="bea10-160">Connection string</span></span>

<span data-ttu-id="bea10-161">Строка подключения должна быть в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="bea10-161">The connection string must be in the following format:</span></span>

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

<span data-ttu-id="bea10-162">Попытка использования общих атрибутов сервера и базы данных завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="bea10-162">Using common server and database attributes will fail.</span></span> <span data-ttu-id="bea10-163">Например: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span><span class="sxs-lookup"><span data-stu-id="bea10-163">For example: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span></span>

### <a name="view"></a><span data-ttu-id="bea10-164">Просмотр</span><span class="sxs-lookup"><span data-stu-id="bea10-164">View</span></span>

<span data-ttu-id="bea10-165">**Представление** управляет отображением **отчетов** и **отчета** Power BI.</span><span class="sxs-lookup"><span data-stu-id="bea10-165">The **View** manages the display of Power BI **Reports** and a Power BI **Report**.</span></span>

<span data-ttu-id="bea10-166">**Reports.cshtml**: выполняет итерацию по отчетам **Model.Reports**, чтобы создать **ActionLink**.</span><span class="sxs-lookup"><span data-stu-id="bea10-166">**Reports.cshtml**: Iterate over **Model.Reports** to create an **ActionLink**.</span></span> <span data-ttu-id="bea10-167">**ActionLink** формируется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="bea10-167">The **ActionLink** is composed as follows:</span></span>

| <span data-ttu-id="bea10-168">Часть</span><span class="sxs-lookup"><span data-stu-id="bea10-168">Part</span></span> | <span data-ttu-id="bea10-169">Описание</span><span class="sxs-lookup"><span data-stu-id="bea10-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bea10-170">Название</span><span class="sxs-lookup"><span data-stu-id="bea10-170">Title</span></span> |<span data-ttu-id="bea10-171">Имя отчета.</span><span class="sxs-lookup"><span data-stu-id="bea10-171">Name of the Report.</span></span> |
| <span data-ttu-id="bea10-172">QueryString</span><span class="sxs-lookup"><span data-stu-id="bea10-172">QueryString</span></span> |<span data-ttu-id="bea10-173">Ссылка на идентификатор отчета.</span><span class="sxs-lookup"><span data-stu-id="bea10-173">A link to the Report ID.</span></span> |

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

<span data-ttu-id="bea10-174">Report.cshtml: устанавливает **Model.AccessToken** и лямбда-выражение для **PowerBIReportFor**.</span><span class="sxs-lookup"><span data-stu-id="bea10-174">Report.cshtml: Set the **Model.AccessToken**, and the Lambda expression for **PowerBIReportFor**.</span></span>

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a><span data-ttu-id="bea10-175">Controller</span><span class="sxs-lookup"><span data-stu-id="bea10-175">Controller</span></span>

<span data-ttu-id="bea10-176">**DashboardController.cs**: создает PowerBIClient, передающий **маркер приложения**.</span><span class="sxs-lookup"><span data-stu-id="bea10-176">**DashboardController.cs**: Creates a PowerBIClient passing an **app token**.</span></span> <span data-ttu-id="bea10-177">Для получения **учетных данных** создается JSON Web Token (JWT) на основе **ключа подписывания**.</span><span class="sxs-lookup"><span data-stu-id="bea10-177">A JSON Web Token (JWT) is generated from the **Signing Key** to get the **Credentials**.</span></span> <span data-ttu-id="bea10-178">**Учетные данные** используются для создания экземпляра **PowerBIClient**.</span><span class="sxs-lookup"><span data-stu-id="bea10-178">The **Credentials** are used to create an instance of **PowerBIClient**.</span></span> <span data-ttu-id="bea10-179">После создания экземпляра **PowerBIClient** можно вызвать методы GetReports() и GetReportsAsync().</span><span class="sxs-lookup"><span data-stu-id="bea10-179">Once you have an instance of **PowerBIClient**, you can call GetReports() and GetReportsAsync().</span></span>

<span data-ttu-id="bea10-180">CreatePowerBIClient()</span><span class="sxs-lookup"><span data-stu-id="bea10-180">CreatePowerBIClient()</span></span>

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

<span data-ttu-id="bea10-181">ActionResult Reports()</span><span class="sxs-lookup"><span data-stu-id="bea10-181">ActionResult Reports()</span></span>

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


<span data-ttu-id="bea10-182">Задача<ActionResult> Report(string reportId)</span><span class="sxs-lookup"><span data-stu-id="bea10-182">Task<ActionResult> Report(string reportId)</span></span>

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

### <a name="integrate-a-report-into-your-app"></a><span data-ttu-id="bea10-183">Интеграция отчета в приложение</span><span class="sxs-lookup"><span data-stu-id="bea10-183">Integrate a report into your app</span></span>

<span data-ttu-id="bea10-184">После получения **отчета** можно использовать **IFrame** для внедрения **отчета** Power BI.</span><span class="sxs-lookup"><span data-stu-id="bea10-184">Once you have a **Report**, you use an **IFrame** to embed the Power BI **Report**.</span></span> <span data-ttu-id="bea10-185">Ниже приведен фрагмент кода из файла powerbi.js в примере **Microsoft Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="bea10-185">Here is a code snippet from  powerbi.js in the **Microsoft Power BI Embedded** sample.</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a><span data-ttu-id="bea10-186">Фильтрация отчетов, внедренных в приложение</span><span class="sxs-lookup"><span data-stu-id="bea10-186">Filter reports embedded in your application</span></span>

<span data-ttu-id="bea10-187">Можно отфильтровать внедренный отчет, используя синтаксис URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="bea10-187">You can filter an embedded report using a URL syntax.</span></span> <span data-ttu-id="bea10-188">Для этого добавьте параметр строки запроса **$filter** с оператором **eq** в исходный URL-адрес iFrame с указанием фильтра.</span><span class="sxs-lookup"><span data-stu-id="bea10-188">To do this, you add a **$filter** query string parameter with an **eq** operator to your iFrame src url with the filter specified.</span></span> <span data-ttu-id="bea10-189">Ниже приведен синтаксис запроса фильтра.</span><span class="sxs-lookup"><span data-stu-id="bea10-189">Here is the filter query syntax:</span></span>

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> <span data-ttu-id="bea10-190">{tableName/fieldName} не может содержать пробелы или специальные знаки.</span><span class="sxs-lookup"><span data-stu-id="bea10-190">{tableName/fieldName} cannot include spaces or special characters.</span></span> <span data-ttu-id="bea10-191">{FieldValue} принимает одно дискретное значение.</span><span class="sxs-lookup"><span data-stu-id="bea10-191">The {fieldValue} accepts a single categorical value.</span></span>  

## <a name="see-also"></a><span data-ttu-id="bea10-192">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="bea10-192">See also</span></span>

[<span data-ttu-id="bea10-193">Типичные сценарии использования Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="bea10-193">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="bea10-194">Аутентификация и авторизация в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="bea10-194">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="bea10-195">Внедрение отчета в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="bea10-195">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="bea10-196">Создание отчета из набора данных</span><span class="sxs-lookup"><span data-stu-id="bea10-196">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="bea10-197">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="bea10-197">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="bea10-198">Пример внедрения JavaScript</span><span class="sxs-lookup"><span data-stu-id="bea10-198">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="bea10-199">У вас имеются и другие вопросы?</span><span class="sxs-lookup"><span data-stu-id="bea10-199">More questions?</span></span> [<span data-ttu-id="bea10-200">Попробуйте задать их в сообществе Power BI</span><span class="sxs-lookup"><span data-stu-id="bea10-200">Try the Power BI Community</span></span>](http://community.powerbi.com/)
