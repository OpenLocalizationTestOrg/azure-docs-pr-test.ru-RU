---
title: "Выполнение запросов аналитики к нескольким базам данных SQL Azure | Документация Майкрософт"
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
ms.openlocfilehash: 4e32407d5f321198358e07980907c3420aaf56c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a><span data-ttu-id="ab486-104">Извлечение данных из баз данных клиента в базу данных аналитики для автономного анализа.</span><span class="sxs-lookup"><span data-stu-id="ab486-104">Extract data from tenant databases into an analytics database for offline analysis</span></span>

<span data-ttu-id="ab486-105">В этом руководстве описывается, как использовать эластичное задание для выполнения запросов к каждой базе данных клиента.</span><span class="sxs-lookup"><span data-stu-id="ab486-105">In this tutorial, you use an elastic job to run queries against each tenant database.</span></span> <span data-ttu-id="ab486-106">Это задание извлекает данные о продаже билетов и загружает их в базу данных аналитики (или хранилище данных) для анализа.</span><span class="sxs-lookup"><span data-stu-id="ab486-106">The job extracts ticket sales data and loads it into an analytics database (or data warehouse) for analysis.</span></span> <span data-ttu-id="ab486-107">Затем к этой базе данных выполняются запросы для получения сведений, которые содержатся в данных ежедневных операций всех клиентов.</span><span class="sxs-lookup"><span data-stu-id="ab486-107">The analytics database is then queried to extract insights from this day-to-day operational data of all tenants.</span></span>


<span data-ttu-id="ab486-108">Из этого руководства вы узнаете, как выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="ab486-108">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ab486-109">Создание базы данных аналитики клиента.</span><span class="sxs-lookup"><span data-stu-id="ab486-109">Create the tenant analytics database</span></span>
> * <span data-ttu-id="ab486-110">Создание запланированного задания для получения данных и заполнения базы данных аналитики.</span><span class="sxs-lookup"><span data-stu-id="ab486-110">Create a scheduled job to retrieve data and populate the analytics database</span></span>

<span data-ttu-id="ab486-111">Для работы с этим руководством выполните следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="ab486-111">To complete this tutorial, make sure the following prerequisites are met:</span></span>

* <span data-ttu-id="ab486-112">Разверните приложение SaaS Wingtip.</span><span class="sxs-lookup"><span data-stu-id="ab486-112">The Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="ab486-113">Чтобы развернуть его менее чем за пять минут, см. сведения в статье [Развертывание и изучение мультитенантного приложения SaaS, использующего базу данных SQL Azure](sql-database-saas-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="ab486-113">To deploy in less than five minutes, see [Deploy and explore the Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="ab486-114">Установите Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ab486-114">Azure PowerShell is installed.</span></span> <span data-ttu-id="ab486-115">Дополнительные сведения см. в статье [Начало работы с Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="ab486-115">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="ab486-116">Установите последнюю версию SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="ab486-116">The latest version of SQL Server Management Studio (SSMS) is installed.</span></span> <span data-ttu-id="ab486-117">[Download SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (Скачивание SQL Server Management Studio (SSMS))</span><span class="sxs-lookup"><span data-stu-id="ab486-117">[Download and Install SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)</span></span>

## <a name="tenant-operational-analytics-pattern"></a><span data-ttu-id="ab486-118">Шаблон операционной аналитики клиента</span><span class="sxs-lookup"><span data-stu-id="ab486-118">Tenant Operational Analytics pattern</span></span>

<span data-ttu-id="ab486-119">Одной из основных возможностей приложений SaaS является использование форматированных данных клиента, хранящихся в облаке.</span><span class="sxs-lookup"><span data-stu-id="ab486-119">One of the great opportunities with SaaS applications is to use the rich tenant data that is stored in the cloud.</span></span> <span data-ttu-id="ab486-120">С помощью этих данных можно проанализировать работу и использование приложения и клиентов.</span><span class="sxs-lookup"><span data-stu-id="ab486-120">Use this data to gain insights into the operation and usage of your application, and your tenants.</span></span> <span data-ttu-id="ab486-121">Они могут помочь в разработке функций, повысить удобство использования, а также обеспечить вложение дополнительных средств в приложение и платформу.</span><span class="sxs-lookup"><span data-stu-id="ab486-121">This data can guide feature development, usability improvements, and other investments in the app and platform.</span></span> <span data-ttu-id="ab486-122">Доступ к этим данным получить очень просто, если они содержатся в отдельной мультитенантной базе данных, но не так просто, если они распределены по тысячам масштабируемых баз данных.</span><span class="sxs-lookup"><span data-stu-id="ab486-122">Accessing this data when it's in a single multi-tenant database is easy, but not so easy when distributed at scale across potentially thousands of databases.</span></span> <span data-ttu-id="ab486-123">Один из способов доступа к таким данным заключается в использовании заданий обработки эластичных баз данных, которые позволяют записать результаты выполнения задания запроса, возвращающего результаты, в выходной базе данных и таблице.</span><span class="sxs-lookup"><span data-stu-id="ab486-123">One approach to accessing this data is to use Elastic jobs, which enable result-returning query results from job execution to be captured in an output database and table.</span></span>

## <a name="get-the-wingtip-application-scripts"></a><span data-ttu-id="ab486-124">Получение сценариев приложения Wingtip</span><span class="sxs-lookup"><span data-stu-id="ab486-124">Get the Wingtip application scripts</span></span>

<span data-ttu-id="ab486-125">Скрипты и исходный код приложения SaaS Wingtip доступны в репозитории GitHub [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS).</span><span class="sxs-lookup"><span data-stu-id="ab486-125">The Wingtip SaaS scripts and application source code are available in the [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="ab486-126">Указания по скачиванию скриптов SaaS Wingtip см. [здесь](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span><span class="sxs-lookup"><span data-stu-id="ab486-126">[Steps to download the Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="deploy-a-database-for-tenant-analytics-results"></a><span data-ttu-id="ab486-127">Развертывание базы данных для результатов аналитики клиента</span><span class="sxs-lookup"><span data-stu-id="ab486-127">Deploy a database for tenant analytics results</span></span>

<span data-ttu-id="ab486-128">Для работы с данным руководством необходимо развернуть базу данных для записи результатов выполнения скриптов задания, которая содержит запросы, возвращающие результаты.</span><span class="sxs-lookup"><span data-stu-id="ab486-128">This tutorial requires you to have a database deployed to capture the results from job execution of scripts, which contain results-returning queries.</span></span> <span data-ttu-id="ab486-129">Для этого давайте создадим базу данных с именем tenantanalytics.</span><span class="sxs-lookup"><span data-stu-id="ab486-129">Let's create a database called tenantanalytics for this purpose.</span></span>

1. <span data-ttu-id="ab486-130">Откройте файл ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* в *интегрированной среде скриптов PowerShell* и задайте следующее значение:</span><span class="sxs-lookup"><span data-stu-id="ab486-130">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in the *PowerShell ISE* and set the following value:</span></span>
   * <span data-ttu-id="ab486-131">**$DemoScenario** = **2**, чтобы *развернуть базы данных операционной аналитики*.</span><span class="sxs-lookup"><span data-stu-id="ab486-131">**$DemoScenario** = **2** *Deploy operational analytics database*</span></span>
1. <span data-ttu-id="ab486-132">Нажмите клавишу **F5** для запуска демонстрационного скрипта (который вызывает скрипт *Deploy-TenantAnalyticsDB.ps1*), создающего базу данных аналитики клиента.</span><span class="sxs-lookup"><span data-stu-id="ab486-132">Press **F5** to run the demo script (that calls the *Deploy-TenantAnalyticsDB.ps1* script) which creates the tenant analytics database.</span></span>

## <a name="create-some-data-for-the-demo"></a><span data-ttu-id="ab486-133">Создание данных для демонстрации</span><span class="sxs-lookup"><span data-stu-id="ab486-133">Create some data for the demo</span></span>

1. <span data-ttu-id="ab486-134">Откройте файл ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* в *интегрированной среде скриптов PowerShell* и задайте следующее значение:</span><span class="sxs-lookup"><span data-stu-id="ab486-134">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in the *PowerShell ISE* and set the following value:</span></span>
   * <span data-ttu-id="ab486-135">**$DemoScenario** = **1**, чтобы *приобрести билеты на мероприятия во всех местах проведения*.</span><span class="sxs-lookup"><span data-stu-id="ab486-135">**$DemoScenario** = **1** *Purchase tickets for events at all venues*</span></span>
1. <span data-ttu-id="ab486-136">Нажмите клавишу **F5** для запуска скрипта и создания журнала покупок билетов.</span><span class="sxs-lookup"><span data-stu-id="ab486-136">Press **F5** to run the script and create ticket purchasing history.</span></span>


## <a name="create-a-scheduled-job-to-retrieve-tenant-analytics-about-ticket-purchases"></a><span data-ttu-id="ab486-137">Создание запланированного задания для получения аналитики клиента о покупках билетов</span><span class="sxs-lookup"><span data-stu-id="ab486-137">Create a scheduled job to retrieve tenant analytics about ticket purchases</span></span>

<span data-ttu-id="ab486-138">Этот скрипт создает задание, чтобы получить сведения о покупке билета клиентами.</span><span class="sxs-lookup"><span data-stu-id="ab486-138">This script creates a job to retrieve ticket purchase information from all tenants.</span></span> <span data-ttu-id="ab486-139">После объединения данных в одну таблицу можно получить обширные детальные метрики о шаблонах покупки билетов для всех клиентов.</span><span class="sxs-lookup"><span data-stu-id="ab486-139">Once aggregated into a single table, you can gain rich insightful metrics about ticket purchasing patterns across the tenants.</span></span>

1. <span data-ttu-id="ab486-140">Откройте среду SSMS и подключитесь к серверу catalog-&lt;пользователь&gt;.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="ab486-140">Open SSMS and connect to the catalog-&lt;user&gt;.database.windows.net server</span></span>
1. <span data-ttu-id="ab486-141">Откройте файл ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*.</span><span class="sxs-lookup"><span data-stu-id="ab486-141">Open ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="ab486-142">Измените &lt;пользователь&gt;. Используйте имя пользователя, примененное при развертывании приложения SaaS Wingtip, в верхней части скрипта: **sp\_add\_target\_group\_member** и **sp\_add\_jobstep**.</span><span class="sxs-lookup"><span data-stu-id="ab486-142">Modify &lt;User&gt;, use the user name used when you deployed the Wingtip SaaS app at the top of the script, **sp\_add\_target\_group\_member** and **sp\_add\_jobstep**</span></span>
1. <span data-ttu-id="ab486-143">Щелкните правой кнопкой мыши, выберите **Подключение** и подключитесь к серверу catalog-&lt;пользователь&gt;.database.windows.net, если вы еще не сделали этого.</span><span class="sxs-lookup"><span data-stu-id="ab486-143">Right click, select **Connection**, and connect to the catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="ab486-144">Убедитесь, что вы подключены к базе данных **jobaccount**, и нажмите клавишу **F5** для запуска скрипта.</span><span class="sxs-lookup"><span data-stu-id="ab486-144">Ensure you are connected to the **jobaccount** database and press **F5** to run the script</span></span>

* <span data-ttu-id="ab486-145">**sp\_add\_target\_group** создает целевую группу с именем *TenantGroup*. Теперь нам требуется добавить целевые элементы.</span><span class="sxs-lookup"><span data-stu-id="ab486-145">**sp\_add\_target\_group** creates the target group name *TenantGroup*, now we need to add target members.</span></span>
* <span data-ttu-id="ab486-146">**sp\_add\_target\_group\_member** добавляет целевой тип элемента *server*, который считает, что базы данных на сервере (обратите внимание, что сервер customer1-&lt;пользователь&gt; содержит базы данных клиентов) во время выполнения задания должны быть включены в задание.</span><span class="sxs-lookup"><span data-stu-id="ab486-146">**sp\_add\_target\_group\_member** adds a *server* target member type, which deems all databases within that server (note this is the customer1-&lt;User&gt; server containing the tenant databases) at time of job execution should be included in the job.</span></span>
* <span data-ttu-id="ab486-147">**sp\_add\_job** создает еженедельное запланированное задание "Покупка билетов клиентами".</span><span class="sxs-lookup"><span data-stu-id="ab486-147">**sp\_add\_job** creates a new weekly scheduled job called “Ticket Purchases from all Tenants”</span></span>
* <span data-ttu-id="ab486-148">**sp\_add\_jobstep** создает шаг задания, содержащий текст команды T-SQL для получения сведений о всех покупках билетов клиентами и копирования набора, возвращающего результат, в таблицу с именем *AllTicketsPurchasesfromAllTenants*.</span><span class="sxs-lookup"><span data-stu-id="ab486-148">**sp\_add\_jobstep** creates the job step containing T-SQL command text to retrieve all the ticket purchase information from all tenants and copy the returning result set into a table called *AllTicketsPurchasesfromAllTenants*</span></span>
* <span data-ttu-id="ab486-149">Остальные представления в скрипте отображают сведения о существовании объектов и отслеживают выполнение задания мониторинга.</span><span class="sxs-lookup"><span data-stu-id="ab486-149">The remaining views in the script display the existence of the objects and monitor job execution.</span></span> <span data-ttu-id="ab486-150">Обратите внимание на значение из столбца **lifecycle** для мониторинга состояния.</span><span class="sxs-lookup"><span data-stu-id="ab486-150">Review the status value from the **lifecycle** column to monitor the status.</span></span> <span data-ttu-id="ab486-151">Когда состояние изменится на "Завершено", это будет означать, что задание успешно завершено на всех базах данных клиентов и двух дополнительных базах данных, содержащих справочную таблицу.</span><span class="sxs-lookup"><span data-stu-id="ab486-151">Once, Succeeded, the job has successfully finished on all tenant databases and the two additional databases containing the reference table.</span></span>

<span data-ttu-id="ab486-152">Успешное выполнение скрипта приведет к тем же результатам:</span><span class="sxs-lookup"><span data-stu-id="ab486-152">Successfully running the script should result in similar results:</span></span>

![results](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-to-retrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a><span data-ttu-id="ab486-154">Создание задания для получения общего числа покупок билетов клиентами</span><span class="sxs-lookup"><span data-stu-id="ab486-154">Create a job to retrieve a summary count of ticket purchases from all tenants</span></span>

<span data-ttu-id="ab486-155">Этот скрипт создает задание, чтобы получить общее количество покупок билетов клиентами.</span><span class="sxs-lookup"><span data-stu-id="ab486-155">This script creates a job to retrieve sum of all ticket purchases from all tenants.</span></span>

1. <span data-ttu-id="ab486-156">Откройте среду SSMS и подключитесь к серверу *catalog-&lt;пользователь&gt;.database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="ab486-156">Open SSMS and connect to the *catalog-&lt;User&gt;.database.windows.net* server</span></span>
1. <span data-ttu-id="ab486-157">Откройте файл ...\\Learning Modules\\Provision and Catalog\\Operational Analytics\\Tenant Analytics\\*Results-TicketPurchasesfromAllTenants.sql*.</span><span class="sxs-lookup"><span data-stu-id="ab486-157">Open the file …\\Learning Modules\\Provision and Catalog\\Operational Analytics\\Tenant Analytics\\*Results-TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="ab486-158">Измените &lt;пользователь&gt;. Используйте имя пользователя, примененное при развертывании приложения SaaS Wingtip в скрипте, в хранимой процедуре **sp\_add\_jobstep**.</span><span class="sxs-lookup"><span data-stu-id="ab486-158">Modify &lt;User&gt;, use the user name used when you deployed the Wingtip SaaS app in the script, in the **sp\_add\_jobstep** stored procedure</span></span>
1. <span data-ttu-id="ab486-159">Щелкните правой кнопкой мыши, выберите **Подключение** и подключитесь к серверу catalog-&lt;пользователь&gt;.database.windows.net, если вы еще не сделали этого.</span><span class="sxs-lookup"><span data-stu-id="ab486-159">Right click, select **Connection**, and connect to the catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="ab486-160">Убедитесь, что вы подключены к базе данных **tenantanalytics**, и нажмите клавишу **F5** для запуска скрипта.</span><span class="sxs-lookup"><span data-stu-id="ab486-160">Ensure you are connected to the **tenantanalytics** database and press **F5** to run the script</span></span>

<span data-ttu-id="ab486-161">Успешное выполнение скрипта приведет к тем же результатам:</span><span class="sxs-lookup"><span data-stu-id="ab486-161">Successfully running the script should result in similar results:</span></span>

![results](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* <span data-ttu-id="ab486-163">**sp\_add\_job** создает еженедельное запланированное задание ResultsTicketsOrders.</span><span class="sxs-lookup"><span data-stu-id="ab486-163">**sp\_add\_job** creates a new weekly scheduled job called “ResultsTicketsOrders”</span></span>

* <span data-ttu-id="ab486-164">**sp\_add\_jobstep** создает шаг задания, содержащий текст команды T-SQL для получения сведений о всех покупках билетов клиентами и копирования набора, возвращающего результат, в таблицу с именем CountofTicketOrders.</span><span class="sxs-lookup"><span data-stu-id="ab486-164">**sp\_add\_jobstep** creates the job step containing T-SQL command text to retrieve all the ticket purchase information from all tenants and copy the returning result set into a table called CountofTicketOrders</span></span>

* <span data-ttu-id="ab486-165">Остальные представления в скрипте отображают сведения о существовании объектов и отслеживают выполнение задания мониторинга.</span><span class="sxs-lookup"><span data-stu-id="ab486-165">The remaining views in the script display the existence of the objects and monitor job execution.</span></span> <span data-ttu-id="ab486-166">Обратите внимание на значение из столбца **lifecycle** для мониторинга состояния.</span><span class="sxs-lookup"><span data-stu-id="ab486-166">Review the status value from the **lifecycle** column to monitor the status.</span></span> <span data-ttu-id="ab486-167">Когда состояние изменится на "Завершено", это будет означать, что задание успешно завершено на всех базах данных клиентов и двух дополнительных базах данных, содержащих справочную таблицу.</span><span class="sxs-lookup"><span data-stu-id="ab486-167">Once, Succeeded, the job has successfully finished on all tenant databases and the two additional databases containing the reference table.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ab486-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ab486-168">Next steps</span></span>

<span data-ttu-id="ab486-169">Из этого руководства вы узнали, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="ab486-169">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ab486-170">Развертывание базы данных аналитики клиента.</span><span class="sxs-lookup"><span data-stu-id="ab486-170">Deploy a tenant analytics database</span></span>
> * <span data-ttu-id="ab486-171">Создание запланированного задания для получения аналитических данных для всех клиентов.</span><span class="sxs-lookup"><span data-stu-id="ab486-171">Create a scheduled job to retrieve analytical data across tenants</span></span>

<span data-ttu-id="ab486-172">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="ab486-172">Congratulations!</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ab486-173">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ab486-173">Additional resources</span></span>

* <span data-ttu-id="ab486-174">[Руководства по SaaS WTP базы данных SQL](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="ab486-174">Additional [tutorials that build upon the Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="ab486-175">Управление масштабируемыми облачными базами данных</span><span class="sxs-lookup"><span data-stu-id="ab486-175">Elastic Jobs</span></span>](sql-database-elastic-jobs-overview.md)
