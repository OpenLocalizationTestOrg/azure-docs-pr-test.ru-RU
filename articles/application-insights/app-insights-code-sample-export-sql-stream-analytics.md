---
title: "Экспорт из Azure Application Insights tooSQL | Документы Microsoft"
description: "Постоянно Экспорт данных tooSQL Application Insights, с помощью Stream Analytics."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 48903032-2c99-4987-9948-d6e4559b4a63
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/06/2015
ms.author: bwren
ms.openlocfilehash: 58b579499113751a088dc7e66cbec71529773322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-export-toosql-from-application-insights-using-stream-analytics"></a><span data-ttu-id="ed01b-103">Пошаговое руководство: Экспорт tooSQL из Application Insights с помощью Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ed01b-103">Walkthrough: Export tooSQL from Application Insights using Stream Analytics</span></span>
<span data-ttu-id="ed01b-104">В этой статье показано, как toomove данные телеметрии из [Azure Application Insights] [ start] в базе данных Azure SQL с помощью [непрерывный Экспорт] [ export] и [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="ed01b-104">This article shows how toomove your telemetry data from [Azure Application Insights][start] into an Azure SQL database by using [Continuous Export][export] and [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> 

<span data-ttu-id="ed01b-105">Непрерывный экспорт позволяет переместить данные телеметрии в службу хранилища Azure в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="ed01b-105">Continuous export moves your telemetry data into Azure Storage in JSON format.</span></span> <span data-ttu-id="ed01b-106">Мы анализ hello объектов JSON, использование Azure Stream Analytics и создайте строки в таблицу базы данных.</span><span class="sxs-lookup"><span data-stu-id="ed01b-106">We'll parse hello JSON objects using Azure Stream Analytics and create rows in a database table.</span></span>

<span data-ttu-id="ed01b-107">(Как правило, непрерывного экспорта — toodo hello способом анализа телеметрии hello ваши приложения отправлять tooApplication аналитики.</span><span class="sxs-lookup"><span data-stu-id="ed01b-107">(More generally, Continuous Export is hello way toodo your own analysis of hello telemetry your apps send tooApplication Insights.</span></span> <span data-ttu-id="ed01b-108">Можно адаптировать этот toodo образец кода прочего с hello экспортировать данные телеметрии, такие как статистическая обработка данных.)</span><span class="sxs-lookup"><span data-stu-id="ed01b-108">You could adapt this code sample toodo other things with hello exported telemetry, such as aggregation of data.)</span></span>

<span data-ttu-id="ed01b-109">Мы начнем с уже есть приложение hello требуется toomonitor допущения hello.</span><span class="sxs-lookup"><span data-stu-id="ed01b-109">We'll start with hello assumption that you already have hello app you want toomonitor.</span></span>

<span data-ttu-id="ed01b-110">В этом примере мы используем данные представления страницы приветствия, но hello же шаблон можно легко расширить tooother типов данных, таких как пользовательские события и исключения.</span><span class="sxs-lookup"><span data-stu-id="ed01b-110">In this example, we will be using hello page view data, but hello same pattern can easily be extended tooother data types such as custom events and exceptions.</span></span> 

## <a name="add-application-insights-tooyour-application"></a><span data-ttu-id="ed01b-111">Добавить приложение tooyour Application Insights</span><span class="sxs-lookup"><span data-stu-id="ed01b-111">Add Application Insights tooyour application</span></span>
<span data-ttu-id="ed01b-112">tooget работы.</span><span class="sxs-lookup"><span data-stu-id="ed01b-112">tooget started:</span></span>

1. <span data-ttu-id="ed01b-113">[Настройте Application Insights для веб-страниц](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="ed01b-113">[Set up Application Insights for your web pages](app-insights-javascript.md).</span></span> 
   
    <span data-ttu-id="ed01b-114">(В этом примере мы сосредоточимся на обработку данных представления страницы из hello клиентскими браузерами, но можно также настроить Application Insights для hello серверную часть вашей [Java](app-insights-java-get-started.md) или [ASP.NET](app-insights-asp-net.md) приложения и процесса запроса. зависимости и другие телеметрии server.)</span><span class="sxs-lookup"><span data-stu-id="ed01b-114">(In this example, we'll focus on processing page view data from hello client browsers, but you could also set up Application Insights for hello server side of your [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md) app and process request, dependency and other server telemetry.)</span></span>
2. <span data-ttu-id="ed01b-115">Опубликуйте свое приложение и просмотрите данные телеметрии, появившиеся в ресурсе Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ed01b-115">Publish your app, and watch telemetry data appearing in your Application Insights resource.</span></span>

## <a name="create-storage-in-azure"></a><span data-ttu-id="ed01b-116">Создание хранилища в Azure</span><span class="sxs-lookup"><span data-stu-id="ed01b-116">Create storage in Azure</span></span>
<span data-ttu-id="ed01b-117">Непрерывный Экспорт всегда выдает учетной записи хранилища Azure tooan данных, поэтому сначала требуется toocreate hello хранилища.</span><span class="sxs-lookup"><span data-stu-id="ed01b-117">Continuous export always outputs data tooan Azure Storage account, so you need toocreate hello storage first.</span></span>

1. <span data-ttu-id="ed01b-118">Создать учетную запись хранилища в подписке в hello [портал Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="ed01b-118">Create a storage account in your subscription in hello [Azure portal][portal].</span></span>
   
    ![На портале Azure выберите «Создать», «Данные», «Хранилище».](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. <span data-ttu-id="ed01b-122">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="ed01b-122">Create a container</span></span>
   
    ![В новое хранилище hello выберите контейнеры, щелкните плитку hello контейнеров, а затем добавить](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. <span data-ttu-id="ed01b-124">Скопируйте ключ доступа к хранилищу hello</span><span class="sxs-lookup"><span data-stu-id="ed01b-124">Copy hello storage access key</span></span>
   
    <span data-ttu-id="ed01b-125">Вам потребуется его скоро tooset hello ввода toohello stream analytics службы.</span><span class="sxs-lookup"><span data-stu-id="ed01b-125">You'll need it soon tooset up hello input toohello stream analytics service.</span></span>
   
    ![В хранилище hello откройте параметры, ключи и сделайте копию hello первичный ключ доступа](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-tooazure-storage"></a><span data-ttu-id="ed01b-127">Запуск хранилища tooAzure непрерывный Экспорт</span><span class="sxs-lookup"><span data-stu-id="ed01b-127">Start continuous export tooAzure storage</span></span>
1. <span data-ttu-id="ed01b-128">В hello портал Azure найдите ресурс Application Insights toohello, созданный для приложения.</span><span class="sxs-lookup"><span data-stu-id="ed01b-128">In hello Azure portal, browse toohello Application Insights resource you created for your application.</span></span>
   
    ![Выберите "Обзор", Application Insights, а затем выберите свое приложение.](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. <span data-ttu-id="ed01b-130">Создайте непрерывный экспорт.</span><span class="sxs-lookup"><span data-stu-id="ed01b-130">Create a continuous export.</span></span>
   
    ![Выберите "Параметры", "Непрерывный экспорт", "Добавить".](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    <span data-ttu-id="ed01b-132">Выберите учетную запись хранения hello, созданную ранее:</span><span class="sxs-lookup"><span data-stu-id="ed01b-132">Select hello storage account you created earlier:</span></span>

    ![Задать назначение экспорта hello](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    <span data-ttu-id="ed01b-134">Установите нужные типы событий hello toosee:</span><span class="sxs-lookup"><span data-stu-id="ed01b-134">Set hello event types you want toosee:</span></span>

    ![Выберите типы событий.](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. <span data-ttu-id="ed01b-136">Пусть данные накопятся.</span><span class="sxs-lookup"><span data-stu-id="ed01b-136">Let some data accumulate.</span></span> <span data-ttu-id="ed01b-137">Предоставьте пользователям возможность поработать с приложением на протяжении некоторого времени.</span><span class="sxs-lookup"><span data-stu-id="ed01b-137">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="ed01b-138">После получения данных телеметрии в [обозревателе метрик](app-insights-metrics-explorer.md) отобразятся статистические диаграммы, а в разделе [поиска по журналу диагностики](app-insights-diagnostic-search.md) — отдельные события.</span><span class="sxs-lookup"><span data-stu-id="ed01b-138">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="ed01b-139">И Кроме того, будет Экспорт tooyour хранилища данных hello.</span><span class="sxs-lookup"><span data-stu-id="ed01b-139">And also, hello data will export tooyour storage.</span></span> 
2. <span data-ttu-id="ed01b-140">Проверки hello экспорта данных, либо на портале hello: Выбор **Обзор**, выберите учетную запись хранения, а затем **контейнеры** - или в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ed01b-140">Inspect hello exported data, either in hello portal - choose **Browse**, select your storage account, and then **Containers** - or in Visual Studio.</span></span> <span data-ttu-id="ed01b-141">В Visual Studio откройте меню **"Вид" или "Обозреватель облака"**и выберите элемент "Azure" или "Хранилище".</span><span class="sxs-lookup"><span data-stu-id="ed01b-141">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="ed01b-142">(Если у вас нет этот пункт меню, необходимо tooinstall hello Azure SDK: Откройте диалоговое окно нового проекта hello и откройте Visual C# / облако / получить Microsoft Azure SDK для .NET.)</span><span class="sxs-lookup"><span data-stu-id="ed01b-142">(If you don't have this menu option, you need tooinstall hello Azure SDK: Open hello New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![В Visual Studio откройте "Обозреватель сервера", "Azure", "Хранилище".](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    <span data-ttu-id="ed01b-144">Запишите hello общую часть hello путь, который является производным от hello приложения имя и ключ инструментирования.</span><span class="sxs-lookup"><span data-stu-id="ed01b-144">Make a note of hello common part of hello path name, which is derived from hello application name and instrumentation key.</span></span> 

<span data-ttu-id="ed01b-145">Hello события записываются tooblob файлы в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="ed01b-145">hello events are written tooblob files in JSON format.</span></span> <span data-ttu-id="ed01b-146">Каждый файл может содержать одно или несколько событий.</span><span class="sxs-lookup"><span data-stu-id="ed01b-146">Each file may contain one or more events.</span></span> <span data-ttu-id="ed01b-147">Поэтому мы предлагаем данных события tooread hello и отфильтровать hello поля, которые должны.</span><span class="sxs-lookup"><span data-stu-id="ed01b-147">So we'd like tooread hello event data and filter out hello fields we want.</span></span> <span data-ttu-id="ed01b-148">Существуют все виды вещей, которые можно было бы сделать с данными hello, но мы планируем на сегодняшний день является toouse Stream Analytics toomove hello данных tooa базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="ed01b-148">There are all kinds of things we could do with hello data, but our plan today is toouse Stream Analytics toomove hello data tooa SQL database.</span></span> <span data-ttu-id="ed01b-149">Чтобы легко toorun множество интересных запросов.</span><span class="sxs-lookup"><span data-stu-id="ed01b-149">That will make it easy toorun lots of interesting queries.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="ed01b-150">Создание базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="ed01b-150">Create an Azure SQL Database</span></span>
<span data-ttu-id="ed01b-151">Еще раз, начиная с подпиской в [портал Azure][portal], создание hello базы данных (и новый сервер, пока у нас уже есть) toowhich вы напишете hello данных.</span><span class="sxs-lookup"><span data-stu-id="ed01b-151">Once again starting from your subscription in [Azure portal][portal], create hello database (and a new server, unless you've already got one) toowhich you'll write hello data.</span></span>

!["Создать", "Данные", SQL.](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

<span data-ttu-id="ed01b-153">Убедитесь, что этот сервер базы данных hello разрешает доступ tooAzure служб:</span><span class="sxs-lookup"><span data-stu-id="ed01b-153">Make sure that hello database server allows access tooAzure services:</span></span>

![Обзор, серверы, server, параметры, брандмауэра tooAzure разрешить доступ](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a><span data-ttu-id="ed01b-155">Создание таблицы в базе данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="ed01b-155">Create a table in Azure SQL DB</span></span>
<span data-ttu-id="ed01b-156">Подключите toohello базу данных, созданную в предыдущем разделе hello со средством управления предпочтительным.</span><span class="sxs-lookup"><span data-stu-id="ed01b-156">Connect toohello database created in hello previous section with your preferred management tool.</span></span> <span data-ttu-id="ed01b-157">В этом пошаговом руководстве мы используем [инструменты управления SQL Server](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="ed01b-157">In this walkthrough, we will be using [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

<span data-ttu-id="ed01b-158">Создайте новый запрос и выполните следующий T-SQL hello:</span><span class="sxs-lookup"><span data-stu-id="ed01b-158">Create a new query, and execute hello following T-SQL:</span></span>

```SQL

CREATE TABLE [dbo].[PageViewsTable](
    [pageName] [nvarchar](max) NOT NULL,
    [viewCount] [int] NOT NULL,
    [url] [nvarchar](max) NULL,
    [urlDataPort] [int] NULL,
    [urlDataprotocol] [nvarchar](50) NULL,
    [urlDataHost] [nvarchar](50) NULL,
    [urlDataBase] [nvarchar](50) NULL,
    [urlDataHashTag] [nvarchar](max) NULL,
    [eventTime] [datetime] NOT NULL,
    [isSynthetic] [nvarchar](50) NULL,
    [deviceId] [nvarchar](50) NULL,
    [deviceType] [nvarchar](50) NULL,
    [os] [nvarchar](50) NULL,
    [osVersion] [nvarchar](50) NULL,
    [locale] [nvarchar](50) NULL,
    [userAgent] [nvarchar](max) NULL,
    [browser] [nvarchar](50) NULL,
    [browserVersion] [nvarchar](50) NULL,
    [screenResolution] [nvarchar](50) NULL,
    [sessionId] [nvarchar](max) NULL,
    [sessionIsFirst] [nvarchar](50) NULL,
    [clientIp] [nvarchar](50) NULL,
    [continent] [nvarchar](50) NULL,
    [country] [nvarchar](50) NULL,
    [province] [nvarchar](50) NULL,
    [city] [nvarchar](50) NULL
)

CREATE CLUSTERED INDEX [pvTblIdx] ON [dbo].[PageViewsTable]
(
    [eventTime] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, SORT_IN_TEMPDB = OFF, DROP_EXISTING = OFF, ONLINE = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON)

```

![](./media/app-insights-code-sample-export-sql-stream-analytics/34-create-table.png)

<span data-ttu-id="ed01b-159">В этом примере мы используем данные из представлений страниц.</span><span class="sxs-lookup"><span data-stu-id="ed01b-159">In this sample, we are using data from page views.</span></span> <span data-ttu-id="ed01b-160">toosee hello другие данные, доступные, проверьте выходные данные JSON и разделе hello [Экспорт модели данных](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="ed01b-160">toosee hello other data available, inspect your JSON output, and see hello [export data model](app-insights-export-data-model.md).</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="ed01b-161">Создание экземпляра Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ed01b-161">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="ed01b-162">Из hello [классический портал Azure](https://manage.windowsazure.com/), выберите службу hello Azure Stream Analytics и создайте новое задание Stream Analytics:</span><span class="sxs-lookup"><span data-stu-id="ed01b-162">From hello [Classic Azure Portal](https://manage.windowsazure.com/), select hello Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

<span data-ttu-id="ed01b-163">Когда создается новое задание hello, разверните его данные:</span><span class="sxs-lookup"><span data-stu-id="ed01b-163">When hello new job is created, expand its details:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a><span data-ttu-id="ed01b-164">Установка расположения большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="ed01b-164">Set blob location</span></span>
<span data-ttu-id="ed01b-165">Задайте tootake входные данные из вашей непрерывного экспорта больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="ed01b-165">Set it tootake input from your Continuous Export blob:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

<span data-ttu-id="ed01b-166">Теперь вам требуется hello первичный ключ доступа из вашей учетной записи хранилища, в котором записанные ранее.</span><span class="sxs-lookup"><span data-stu-id="ed01b-166">Now you'll need hello Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="ed01b-167">Настроить его как hello ключ учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="ed01b-167">Set this as hello Storage Account Key.</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a><span data-ttu-id="ed01b-168">Установка шаблона префикса пути</span><span class="sxs-lookup"><span data-stu-id="ed01b-168">Set path prefix pattern</span></span>
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

<span data-ttu-id="ed01b-169">Быть hello убедиться, что tooset формат даты слишком**гггг-мм-дд** (с **тире**).</span><span class="sxs-lookup"><span data-stu-id="ed01b-169">Be sure tooset hello Date Format too**YYYY-MM-DD** (with **dashes**).</span></span>

<span data-ttu-id="ed01b-170">Шаблон префикс пути Hello указывает, как Stream Analytics находит hello входных файлов в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="ed01b-170">hello Path Prefix Pattern specifies how Stream Analytics finds hello input files in hello storage.</span></span> <span data-ttu-id="ed01b-171">Требуется tooset его toohow toocorrespond непрерывный Экспорт хранит данные hello.</span><span class="sxs-lookup"><span data-stu-id="ed01b-171">You need tooset it toocorrespond toohow Continuous Export stores hello data.</span></span> <span data-ttu-id="ed01b-172">Задайте следующее значение:</span><span class="sxs-lookup"><span data-stu-id="ed01b-172">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="ed01b-173">В данном примере:</span><span class="sxs-lookup"><span data-stu-id="ed01b-173">In this example:</span></span>

* <span data-ttu-id="ed01b-174">`webapplication27`— Имя hello hello ресурс Application Insights **в нижнем регистре**.</span><span class="sxs-lookup"><span data-stu-id="ed01b-174">`webapplication27` is hello name of hello Application Insights resource, **all in lower case**.</span></span> 
* <span data-ttu-id="ed01b-175">`1234...`ключ инструментирования hello hello ресурс Application Insights **удалены два дефиса**.</span><span class="sxs-lookup"><span data-stu-id="ed01b-175">`1234...` is hello instrumentation key of hello Application Insights resource **with dashes removed**.</span></span> 
* <span data-ttu-id="ed01b-176">`PageViews`hello тип данных, мы хотим tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="ed01b-176">`PageViews` is hello type of data we want tooanalyze.</span></span> <span data-ttu-id="ed01b-177">Доступные типы Hello зависят от фильтра hello, заданные в непрерывный экспорт.</span><span class="sxs-lookup"><span data-stu-id="ed01b-177">hello available types depend on hello filter you set in Continuous Export.</span></span> <span data-ttu-id="ed01b-178">Просмотрите другие доступные типы hello экспортированных данных toosee hello и hello в разделе [Экспорт модели данных](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="ed01b-178">Examine hello exported data toosee hello other available types, and see hello [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="ed01b-179">`/{date}/{time}` – шаблон, записанный буквально.</span><span class="sxs-lookup"><span data-stu-id="ed01b-179">`/{date}/{time}` is a pattern written literally.</span></span>

<span data-ttu-id="ed01b-180">Имя tooget hello и iKey ресурса Application Insights, откройте Essentials на его «Обзор», или параметры.</span><span class="sxs-lookup"><span data-stu-id="ed01b-180">tooget hello name and iKey of your Application Insights resource, open Essentials on its overview page, or open Settings.</span></span>

#### <a name="finish-initial-setup"></a><span data-ttu-id="ed01b-181">Завершение начальной настройки</span><span class="sxs-lookup"><span data-stu-id="ed01b-181">Finish initial setup</span></span>
<span data-ttu-id="ed01b-182">Подтверждение hello формат сериализации:</span><span class="sxs-lookup"><span data-stu-id="ed01b-182">Confirm hello serialization format:</span></span>

![Подтвердите выбор и закройте мастер.](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

<span data-ttu-id="ed01b-184">Закройте мастер hello и дождитесь toocomplete установки hello.</span><span class="sxs-lookup"><span data-stu-id="ed01b-184">Close hello wizard and wait for hello setup toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="ed01b-185">Используйте toocheck функция образец hello, правильно задать hello входного пути.</span><span class="sxs-lookup"><span data-stu-id="ed01b-185">Use hello Sample function toocheck that you have set hello input path correctly.</span></span> <span data-ttu-id="ed01b-186">В случае неудачи: Убедитесь, что в хранилище hello для выбранного диапазона времени образец hello данных.</span><span class="sxs-lookup"><span data-stu-id="ed01b-186">If it fails: Check that there is data in hello storage for hello sample time range you chose.</span></span> <span data-ttu-id="ed01b-187">Изменить определение ввода hello и проверить набора hello учетной записи хранилища, префикс пути и Дата формат правильно.</span><span class="sxs-lookup"><span data-stu-id="ed01b-187">Edit hello input definition and check you set hello storage account, path prefix and date format correctly.</span></span>
> 
> 

## <a name="set-query"></a><span data-ttu-id="ed01b-188">Настройка запроса</span><span class="sxs-lookup"><span data-stu-id="ed01b-188">Set query</span></span>
<span data-ttu-id="ed01b-189">Откройте раздел hello запроса:</span><span class="sxs-lookup"><span data-stu-id="ed01b-189">Open hello query section:</span></span>

![В Stream Analytics выберите "Запрос".](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

<span data-ttu-id="ed01b-191">Замените запросов по умолчанию hello с:</span><span class="sxs-lookup"><span data-stu-id="ed01b-191">Replace hello default query with:</span></span>

```SQL

    SELECT flat.ArrayValue.name as pageName
    , flat.ArrayValue.count as viewCount
    , flat.ArrayValue.url as url
    , flat.ArrayValue.urlData.port as urlDataPort
    , flat.ArrayValue.urlData.protocol as urlDataprotocol
    , flat.ArrayValue.urlData.host as urlDataHost
    , flat.ArrayValue.urlData.base as urlDataBase
    , flat.ArrayValue.urlData.hashTag as urlDataHashTag
      ,A.context.data.eventTime as eventTime
      ,A.context.data.isSynthetic as isSynthetic
      ,A.context.device.id as deviceId
      ,A.context.device.type as deviceType
      ,A.context.device.os as os
      ,A.context.device.osVersion as osVersion
      ,A.context.device.locale as locale
      ,A.context.device.userAgent as userAgent
      ,A.context.device.browser as browser
      ,A.context.device.browserVersion as browserVersion
      ,A.context.device.screenResolution.value as screenResolution
      ,A.context.session.id as sessionId
      ,A.context.session.isFirst as sessionIsFirst
      ,A.context.location.clientip as clientIp
      ,A.context.location.continent as continent
      ,A.context.location.country as country
      ,A.context.location.province as province
      ,A.context.location.city as city
    INTO
      AIOutput
    FROM AIinput A
    CROSS APPLY GetElements(A.[view]) as flat


```

<span data-ttu-id="ed01b-192">Обратите внимание, что сначала hello несколько свойств, определенных toopage представление данных.</span><span class="sxs-lookup"><span data-stu-id="ed01b-192">Notice that hello first few properties are specific toopage view data.</span></span> <span data-ttu-id="ed01b-193">При экспорте телеметрии других типов будут получены другие свойства.</span><span class="sxs-lookup"><span data-stu-id="ed01b-193">Exports of other telemetry types will have different properties.</span></span> <span data-ttu-id="ed01b-194">В разделе hello [подробные справочные материалы по модели данных для значений и типы свойств hello.](app-insights-export-data-model.md)</span><span class="sxs-lookup"><span data-stu-id="ed01b-194">See hello [detailed data model reference for hello property types and values.](app-insights-export-data-model.md)</span></span>

## <a name="set-up-output-toodatabase"></a><span data-ttu-id="ed01b-195">Настройка вывода toodatabase</span><span class="sxs-lookup"><span data-stu-id="ed01b-195">Set up output toodatabase</span></span>
<span data-ttu-id="ed01b-196">Выберите SQL в качестве выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="ed01b-196">Select SQL as hello output.</span></span>

![В Stream Analytics выберите "Выходные данные".](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

<span data-ttu-id="ed01b-198">Укажите базу данных SQL hello.</span><span class="sxs-lookup"><span data-stu-id="ed01b-198">Specify hello SQL database.</span></span>

![Введите сведения о hello базы данных](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

<span data-ttu-id="ed01b-200">Закройте мастер hello и ожидание уведомления, которые были настроены hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="ed01b-200">Close hello wizard and wait for a notification that hello output has been set up.</span></span>

## <a name="start-processing"></a><span data-ttu-id="ed01b-201">Начало обработки</span><span class="sxs-lookup"><span data-stu-id="ed01b-201">Start processing</span></span>
<span data-ttu-id="ed01b-202">Запустите задание hello hello панели действий:</span><span class="sxs-lookup"><span data-stu-id="ed01b-202">Start hello job from hello action bar:</span></span>

![В Stream Analytics щелкните "Запуск".](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

<span data-ttu-id="ed01b-204">Вы можете hello ли toostart обработки данных, начиная с сейчас или toostart с более ранние данные.</span><span class="sxs-lookup"><span data-stu-id="ed01b-204">You can choose whether toostart processing hello data starting from now, or toostart with earlier data.</span></span> <span data-ttu-id="ed01b-205">последний Hello полезно в том случае, если у вас уже есть непрерывный экспорт, уже запущена в течение некоторого времени.</span><span class="sxs-lookup"><span data-stu-id="ed01b-205">hello latter is useful if you have had Continuous Export already running for a while.</span></span>

![В Stream Analytics щелкните "Запуск".](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

<span data-ttu-id="ed01b-207">Через несколько минут средства управления сервером tooSQL вернуться назад и посмотрите, hello обмен данными в.</span><span class="sxs-lookup"><span data-stu-id="ed01b-207">After a few minutes, go back tooSQL Server Management Tools and watch hello data flowing in.</span></span> <span data-ttu-id="ed01b-208">Например, используйте запрос наподобие этого:</span><span class="sxs-lookup"><span data-stu-id="ed01b-208">For example, use a query like this:</span></span>

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a><span data-ttu-id="ed01b-209">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="ed01b-209">Related articles</span></span>
* [<span data-ttu-id="ed01b-210">С помощью Stream Analytics tooPowerBI экспорта</span><span class="sxs-lookup"><span data-stu-id="ed01b-210">Export tooPowerBI using Stream Analytics</span></span>](app-insights-export-power-bi.md)
* [<span data-ttu-id="ed01b-211">Подробные данные модели ссылок для значений и типы свойств hello.</span><span class="sxs-lookup"><span data-stu-id="ed01b-211">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="ed01b-212">Непрерывный экспорт в Application Insights</span><span class="sxs-lookup"><span data-stu-id="ed01b-212">Continuous Export in Application Insights</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="ed01b-213">Application Insights</span><span class="sxs-lookup"><span data-stu-id="ed01b-213">Application Insights</span></span>](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

