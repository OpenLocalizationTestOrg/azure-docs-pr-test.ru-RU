---
title: "aaaRun аналитические запросы к нескольким базам данных Azure SQL | Документы Microsoft"
description: "Извлечение данных из баз данных клиента в базу данных аналитики для автономного анализа."
keywords: "руководство по базе данных sql"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: billgib; sstein
ms.openlocfilehash: f2664e4aafd2fecc98d20d229342bca19b0b08c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a><span data-ttu-id="998f5-104">Извлечение данных из баз данных клиента в базу данных аналитики для автономного анализа.</span><span class="sxs-lookup"><span data-stu-id="998f5-104">Extract data from tenant databases into an analytics database for offline analysis</span></span>

<span data-ttu-id="998f5-105">В этом учебнике используется запросов toorun эластичной заданий для каждой базы данных клиента.</span><span class="sxs-lookup"><span data-stu-id="998f5-105">In this tutorial, you use an elastic job toorun queries against each tenant database.</span></span> <span data-ttu-id="998f5-106">Hello задание извлекает данные о продажах билета и загружает их в базу данных аналитики (или хранилище данных) для анализа.</span><span class="sxs-lookup"><span data-stu-id="998f5-106">hello job extracts ticket sales data and loads it into an analytics database (or data warehouse) for analysis.</span></span> <span data-ttu-id="998f5-107">Hello базы данных аналитики будет запрашивать tooextract полезные сведения из этого повседневных рабочих данных всех клиентов.</span><span class="sxs-lookup"><span data-stu-id="998f5-107">hello analytics database is then queried tooextract insights from this day-to-day operational data of all tenants.</span></span>


<span data-ttu-id="998f5-108">Из этого руководства вы узнаете, как выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="998f5-108">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="998f5-109">Создать базу данных аналитики клиента hello</span><span class="sxs-lookup"><span data-stu-id="998f5-109">Create hello tenant analytics database</span></span>
> * <span data-ttu-id="998f5-110">Создание запланированного задания tooretrieve данных и заполнить базу данных аналитики hello</span><span class="sxs-lookup"><span data-stu-id="998f5-110">Create a scheduled job tooretrieve data and populate hello analytics database</span></span>

<span data-ttu-id="998f5-111">toocomplete этого учебника, убедитесь, что hello следующие необходимые условия выполнены:</span><span class="sxs-lookup"><span data-stu-id="998f5-111">toocomplete this tutorial, make sure hello following prerequisites are met:</span></span>

* <span data-ttu-id="998f5-112">приложение Wingtip SaaS Hello развертывается.</span><span class="sxs-lookup"><span data-stu-id="998f5-112">hello Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="998f5-113">toodeploy менее чем за пять минут. в разделе [развертывание и просмотр приложения Wingtip SaaS hello](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="998f5-113">toodeploy in less than five minutes, see [Deploy and explore hello Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="998f5-114">Установите Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="998f5-114">Azure PowerShell is installed.</span></span> <span data-ttu-id="998f5-115">Дополнительные сведения см. в статье [Начало работы с Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="998f5-115">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="998f5-116">будет установлена последняя версия Hello объекта SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="998f5-116">hello latest version of SQL Server Management Studio (SSMS) is installed.</span></span> <span data-ttu-id="998f5-117">[Download SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (Скачивание SQL Server Management Studio (SSMS))</span><span class="sxs-lookup"><span data-stu-id="998f5-117">[Download and Install SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)</span></span>

## <a name="tenant-operational-analytics-pattern"></a><span data-ttu-id="998f5-118">Шаблон операционной аналитики клиента</span><span class="sxs-lookup"><span data-stu-id="998f5-118">Tenant Operational Analytics pattern</span></span>

<span data-ttu-id="998f5-119">Одним из hello значительные возможности с приложениями SaaS является toouse hello многофункциональный клиентский данные, хранящиеся в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="998f5-119">One of hello great opportunities with SaaS applications is toouse hello rich tenant data that is stored in hello cloud.</span></span> <span data-ttu-id="998f5-120">Используйте этот данных toogain анализировать операции hello и использования приложения и клиенты.</span><span class="sxs-lookup"><span data-stu-id="998f5-120">Use this data toogain insights into hello operation and usage of your application, and your tenants.</span></span> <span data-ttu-id="998f5-121">Эти данные проводит разработки функции, улучшения удобства использования и прочие вложения в приложение hello и платформы.</span><span class="sxs-lookup"><span data-stu-id="998f5-121">This data can guide feature development, usability improvements, and other investments in hello app and platform.</span></span> <span data-ttu-id="998f5-122">Доступ к этим данным получить очень просто, если они содержатся в отдельной мультитенантной базе данных, но не так просто, если они распределены по тысячам масштабируемых баз данных.</span><span class="sxs-lookup"><span data-stu-id="998f5-122">Accessing this data when it's in a single multi-tenant database is easy, but not so easy when distributed at scale across potentially thousands of databases.</span></span> <span data-ttu-id="998f5-123">Один подход tooaccessing эти данные являются toouse эластичной заданий, позволяющие возвращение результата от toobe выполнения задания, записанные в выходных данных базы данных и таблицы результатов запроса.</span><span class="sxs-lookup"><span data-stu-id="998f5-123">One approach tooaccessing this data is toouse Elastic jobs, which enable result-returning query results from job execution toobe captured in an output database and table.</span></span>

## <a name="get-hello-wingtip-application-scripts"></a><span data-ttu-id="998f5-124">Получение скриптов приложения Wingtip hello</span><span class="sxs-lookup"><span data-stu-id="998f5-124">Get hello Wingtip application scripts</span></span>

<span data-ttu-id="998f5-125">Hello Wingtip SaaS скриптов и исходный код приложения были доступны в hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) в репозитории github.</span><span class="sxs-lookup"><span data-stu-id="998f5-125">hello Wingtip SaaS scripts and application source code are available in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="998f5-126">[Действия скриптов Wingtip SaaS hello toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span><span class="sxs-lookup"><span data-stu-id="998f5-126">[Steps toodownload hello Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="deploy-a-database-for-tenant-analytics-results"></a><span data-ttu-id="998f5-127">Развертывание базы данных для результатов аналитики клиента</span><span class="sxs-lookup"><span data-stu-id="998f5-127">Deploy a database for tenant analytics results</span></span>

<span data-ttu-id="998f5-128">Этот учебник требует toohave, hello toocapture развернутой базы данных полученный в результате выполнения скриптов, которые содержат запросы, возвращающие результаты задания.</span><span class="sxs-lookup"><span data-stu-id="998f5-128">This tutorial requires you toohave a database deployed toocapture hello results from job execution of scripts, which contain results-returning queries.</span></span> <span data-ttu-id="998f5-129">Для этого давайте создадим базу данных с именем tenantanalytics.</span><span class="sxs-lookup"><span data-stu-id="998f5-129">Let's create a database called tenantanalytics for this purpose.</span></span>

1. <span data-ttu-id="998f5-130">Открыть... \\Модулей обучения\\оперативной аналитики\\аналитика клиента\\*Демонстрация TenantAnalyticsDB.ps1* в hello *интегрированной среды Сценариев PowerShell* и задайте Здравствуйте, следующие значения:</span><span class="sxs-lookup"><span data-stu-id="998f5-130">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in hello *PowerShell ISE* and set hello following value:</span></span>
   * <span data-ttu-id="998f5-131">**$DemoScenario** = **2**, чтобы *развернуть базы данных операционной аналитики*.</span><span class="sxs-lookup"><span data-stu-id="998f5-131">**$DemoScenario** = **2** *Deploy operational analytics database*</span></span>
1. <span data-ttu-id="998f5-132">Нажмите клавишу **F5** toorun hello демонстрационный сценарий (hello, вызовы *TenantAnalyticsDB.ps1 развернуть* сценария) создает базы данных аналитики hello клиента.</span><span class="sxs-lookup"><span data-stu-id="998f5-132">Press **F5** toorun hello demo script (that calls hello *Deploy-TenantAnalyticsDB.ps1* script) which creates hello tenant analytics database.</span></span>

## <a name="create-some-data-for-hello-demo"></a><span data-ttu-id="998f5-133">Создание некоторых данных для образца hello</span><span class="sxs-lookup"><span data-stu-id="998f5-133">Create some data for hello demo</span></span>

1. <span data-ttu-id="998f5-134">Открыть... \\Модулей обучения\\оперативной аналитики\\аналитика клиента\\*Демонстрация TenantAnalyticsDB.ps1* в hello *интегрированной среды Сценариев PowerShell* и задайте Здравствуйте, следующие значения:</span><span class="sxs-lookup"><span data-stu-id="998f5-134">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in hello *PowerShell ISE* and set hello following value:</span></span>
   * <span data-ttu-id="998f5-135">**$DemoScenario** = **1**, чтобы *приобрести билеты на мероприятия во всех местах проведения*.</span><span class="sxs-lookup"><span data-stu-id="998f5-135">**$DemoScenario** = **1** *Purchase tickets for events at all venues*</span></span>
1. <span data-ttu-id="998f5-136">Нажмите клавишу **F5** toorun hello скрипт и создать журнал приобретения билета.</span><span class="sxs-lookup"><span data-stu-id="998f5-136">Press **F5** toorun hello script and create ticket purchasing history.</span></span>


## <a name="create-a-scheduled-job-tooretrieve-tenant-analytics-about-ticket-purchases"></a><span data-ttu-id="998f5-137">Создание аналитика клиента tooretrieve запланированного задания, о покупках билета</span><span class="sxs-lookup"><span data-stu-id="998f5-137">Create a scheduled job tooretrieve tenant analytics about ticket purchases</span></span>

<span data-ttu-id="998f5-138">Этот скрипт создает задание информации о приобретении tooretrieve билетов от всех клиентов.</span><span class="sxs-lookup"><span data-stu-id="998f5-138">This script creates a job tooretrieve ticket purchase information from all tenants.</span></span> <span data-ttu-id="998f5-139">После статистическую обработку в одну таблицу, можно получить форматированного информативные метрики о билет приобретение шаблоны hello клиентов.</span><span class="sxs-lookup"><span data-stu-id="998f5-139">Once aggregated into a single table, you can gain rich insightful metrics about ticket purchasing patterns across hello tenants.</span></span>

1. <span data-ttu-id="998f5-140">Откройте SSMS и подключите каталог toohello -&lt;пользователя&gt;. database.windows.net сервера</span><span class="sxs-lookup"><span data-stu-id="998f5-140">Open SSMS and connect toohello catalog-&lt;user&gt;.database.windows.net server</span></span>
1. <span data-ttu-id="998f5-141">Откройте файл ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*.</span><span class="sxs-lookup"><span data-stu-id="998f5-141">Open ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="998f5-142">Изменить &lt;пользователя&gt;, используйте hello имя пользователя при развертывании приложение Wingtip SaaS hello hello верхней части сценария hello **sp\_добавить\_целевой\_группы\_член** и **sp\_добавить\_шага задания**</span><span class="sxs-lookup"><span data-stu-id="998f5-142">Modify &lt;User&gt;, use hello user name used when you deployed hello Wingtip SaaS app at hello top of hello script, **sp\_add\_target\_group\_member** and **sp\_add\_jobstep**</span></span>
1. <span data-ttu-id="998f5-143">Щелкните правой кнопкой мыши, выберите **подключения**и подключите каталог toohello -&lt;пользователя&gt;. database.windows.net сервер, если еще не подключены</span><span class="sxs-lookup"><span data-stu-id="998f5-143">Right click, select **Connection**, and connect toohello catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="998f5-144">Убедитесь, подключенных toohello **jobaccount** базы данных и нажмите клавишу **F5** для выполнения сценария hello</span><span class="sxs-lookup"><span data-stu-id="998f5-144">Ensure you are connected toohello **jobaccount** database and press **F5** to run hello script</span></span>

* <span data-ttu-id="998f5-145">**SP\_добавить\_целевой\_группы** создает имя целевой группы hello *TenantGroup*, теперь мы должны tooadd целевые элементы.</span><span class="sxs-lookup"><span data-stu-id="998f5-145">**sp\_add\_target\_group** creates hello target group name *TenantGroup*, now we need tooadd target members.</span></span>
* <span data-ttu-id="998f5-146">**SP\_добавить\_целевой\_группы\_член** добавляет *сервера* целевой тип члена, который рассматривается всех баз данных в пределах сервера (Обратите внимание, это hello customer1 - &lt;Пользователя&gt; сервер, содержащий базы данных клиента hello) во время задания выполнения должны быть включены в задание hello.</span><span class="sxs-lookup"><span data-stu-id="998f5-146">**sp\_add\_target\_group\_member** adds a *server* target member type, which deems all databases within that server (note this is hello customer1-&lt;User&gt; server containing hello tenant databases) at time of job execution should be included in hello job.</span></span>
* <span data-ttu-id="998f5-147">**sp\_add\_job** создает еженедельное запланированное задание "Покупка билетов клиентами".</span><span class="sxs-lookup"><span data-stu-id="998f5-147">**sp\_add\_job** creates a new weekly scheduled job called “Ticket Purchases from all Tenants”</span></span>
* <span data-ttu-id="998f5-148">**SP\_добавить\_jobstep** создает все hello билета закупки hello шаг задания, содержащий tooretrieve текст команды T-SQL со всех клиентов и возвращение результирующего набора в таблицу с именем hello копирования  *AllTicketsPurchasesfromAllTenants*</span><span class="sxs-lookup"><span data-stu-id="998f5-148">**sp\_add\_jobstep** creates hello job step containing T-SQL command text tooretrieve all hello ticket purchase information from all tenants and copy hello returning result set into a table called *AllTicketsPurchasesfromAllTenants*</span></span>
* <span data-ttu-id="998f5-149">Оставшиеся представления Hello в скрипте hello отображают существование hello hello объектов и монитор выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="998f5-149">hello remaining views in hello script display hello existence of hello objects and monitor job execution.</span></span> <span data-ttu-id="998f5-150">Просмотрите значение состояния hello из hello **жизненного цикла** состояние hello toomonitor столбца.</span><span class="sxs-lookup"><span data-stu-id="998f5-150">Review hello status value from hello **lifecycle** column toomonitor hello status.</span></span> <span data-ttu-id="998f5-151">Один раз прошло успешно, задание hello успешного завершения работы для всех баз данных клиента и hello два дополнительных баз данных, содержащих hello ссылаются на таблицу.</span><span class="sxs-lookup"><span data-stu-id="998f5-151">Once, Succeeded, hello job has successfully finished on all tenant databases and hello two additional databases containing hello reference table.</span></span>

<span data-ttu-id="998f5-152">Успешно запустить скрипт hello следует результат такой же результат:</span><span class="sxs-lookup"><span data-stu-id="998f5-152">Successfully running hello script should result in similar results:</span></span>

![results](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-tooretrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a><span data-ttu-id="998f5-154">Создание задания tooretrieve, общее число билет покупки от всех клиентов</span><span class="sxs-lookup"><span data-stu-id="998f5-154">Create a job tooretrieve a summary count of ticket purchases from all tenants</span></span>

<span data-ttu-id="998f5-155">Этот скрипт создает задание tooretrieve сумму всех покупок билет от всех клиентов.</span><span class="sxs-lookup"><span data-stu-id="998f5-155">This script creates a job tooretrieve sum of all ticket purchases from all tenants.</span></span>

1. <span data-ttu-id="998f5-156">Откройте SSMS и подключите toohello *каталога -&lt;пользователя&gt;. database.windows.net* сервера</span><span class="sxs-lookup"><span data-stu-id="998f5-156">Open SSMS and connect toohello *catalog-&lt;User&gt;.database.windows.net* server</span></span>
1. <span data-ttu-id="998f5-157">Привет открыть файл... \\Модулях обучения\\подготовки и каталога\\оперативной аналитики\\клиента Analytics\\*TicketPurchasesfromAllTenants.sql результатов*</span><span class="sxs-lookup"><span data-stu-id="998f5-157">Open hello file …\\Learning Modules\\Provision and Catalog\\Operational Analytics\\Tenant Analytics\\*Results-TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="998f5-158">Изменить &lt;пользователя&gt;, используйте hello имя пользователя при развертывании приложения Wingtip SaaS hello в скрипте hello в hello **sp\_добавить\_шага задания** хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="998f5-158">Modify &lt;User&gt;, use hello user name used when you deployed hello Wingtip SaaS app in hello script, in hello **sp\_add\_jobstep** stored procedure</span></span>
1. <span data-ttu-id="998f5-159">Щелкните правой кнопкой мыши, выберите **подключения**и подключите каталог toohello -&lt;пользователя&gt;. database.windows.net сервер, если еще не подключены</span><span class="sxs-lookup"><span data-stu-id="998f5-159">Right click, select **Connection**, and connect toohello catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="998f5-160">Убедитесь, подключенных toohello **tenantanalytics** базы данных и нажмите клавишу **F5** для выполнения сценария hello</span><span class="sxs-lookup"><span data-stu-id="998f5-160">Ensure you are connected toohello **tenantanalytics** database and press **F5** to run hello script</span></span>

<span data-ttu-id="998f5-161">Успешно запустить скрипт hello следует результат такой же результат:</span><span class="sxs-lookup"><span data-stu-id="998f5-161">Successfully running hello script should result in similar results:</span></span>

![results](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* <span data-ttu-id="998f5-163">**sp\_add\_job** создает еженедельное запланированное задание ResultsTicketsOrders.</span><span class="sxs-lookup"><span data-stu-id="998f5-163">**sp\_add\_job** creates a new weekly scheduled job called “ResultsTicketsOrders”</span></span>

* <span data-ttu-id="998f5-164">**SP\_добавить\_шага задания** создает все hello билета закупки hello шаг задания, содержащий tooretrieve текст команды T-SQL со всех клиентов и возвращение результирующего набора в таблицу с именем CountofTicketOrders hello копирования</span><span class="sxs-lookup"><span data-stu-id="998f5-164">**sp\_add\_jobstep** creates hello job step containing T-SQL command text tooretrieve all hello ticket purchase information from all tenants and copy hello returning result set into a table called CountofTicketOrders</span></span>

* <span data-ttu-id="998f5-165">Оставшиеся представления Hello в скрипте hello отображают существование hello hello объектов и монитор выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="998f5-165">hello remaining views in hello script display hello existence of hello objects and monitor job execution.</span></span> <span data-ttu-id="998f5-166">Просмотрите значение состояния hello из hello **жизненного цикла** состояние hello toomonitor столбца.</span><span class="sxs-lookup"><span data-stu-id="998f5-166">Review hello status value from hello **lifecycle** column toomonitor hello status.</span></span> <span data-ttu-id="998f5-167">Один раз прошло успешно, задание hello успешного завершения работы для всех баз данных клиента и hello два дополнительных баз данных, содержащих hello ссылаются на таблицу.</span><span class="sxs-lookup"><span data-stu-id="998f5-167">Once, Succeeded, hello job has successfully finished on all tenant databases and hello two additional databases containing hello reference table.</span></span>


## <a name="next-steps"></a><span data-ttu-id="998f5-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="998f5-168">Next steps</span></span>

<span data-ttu-id="998f5-169">Из этого руководства вы узнали, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="998f5-169">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="998f5-170">Развертывание базы данных аналитики клиента.</span><span class="sxs-lookup"><span data-stu-id="998f5-170">Deploy a tenant analytics database</span></span>
> * <span data-ttu-id="998f5-171">Создать запланированное задание tooretrieve аналитических данных в другие клиенты</span><span class="sxs-lookup"><span data-stu-id="998f5-171">Create a scheduled job tooretrieve analytical data across tenants</span></span>

<span data-ttu-id="998f5-172">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="998f5-172">Congratulations!</span></span>

## <a name="additional-resources"></a><span data-ttu-id="998f5-173">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="998f5-173">Additional resources</span></span>

* <span data-ttu-id="998f5-174">Дополнительные [учебники, которые созданы на основе Wingtip SaaS приложения hello](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="998f5-174">Additional [tutorials that build upon hello Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="998f5-175">Управление масштабируемыми облачными базами данных</span><span class="sxs-lookup"><span data-stu-id="998f5-175">Elastic Jobs</span></span>](sql-database-elastic-jobs-overview.md)
