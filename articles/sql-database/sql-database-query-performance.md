---
title: "aaaQuery подробных сведений о производительности для базы данных SQL Azure | Документы Microsoft"
description: "Наблюдение за производительностью запросов идентифицирует hello большинство использование ЦП запрашивает в базе данных SQL Azure."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: c2f580b2-3835-453f-89f5-140e02dd2ea7
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 01cca26f85193c679365585cd676449c9db00e1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-query-performance-insight"></a><span data-ttu-id="58429-103">Анализ производительности запросов базы данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="58429-103">Azure SQL Database Query Performance Insight</span></span>
<span data-ttu-id="58429-104">Управление и настройка производительности hello реляционных баз данных является сложной задачу, которая требуется значительный опыт и время.</span><span class="sxs-lookup"><span data-stu-id="58429-104">Managing and tuning hello performance of relational databases is a challenging task that requires significant expertise and time investment.</span></span> <span data-ttu-id="58429-105">Анализ производительности запросов позволяет toospend меньше времени, устранение неполадок производительности базы данных, предоставляя hello следующее:</span><span class="sxs-lookup"><span data-stu-id="58429-105">Query Performance Insight allows you toospend less time troubleshooting database performance by providing hello following:</span></span>

* <span data-ttu-id="58429-106">Более глубокое понимание потребления ресурсов базы данных (DTU).</span><span class="sxs-lookup"><span data-stu-id="58429-106">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="58429-107">Hello первых запросах по количеству ЦП или длительность или выполнения, который потенциально может настраиваться для повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="58429-107">hello top queries by CPU/Duration/Execution count, which can potentially be tuned for improved performance.</span></span>
* <span data-ttu-id="58429-108">Здравствуйте возможность toodrill вниз hello Дополнительные сведения о запросе, просмотреть его текст и журнал использования ресурсов.</span><span class="sxs-lookup"><span data-stu-id="58429-108">hello ability toodrill down into hello details of a query, view its text and history of resource utilization.</span></span> 
* <span data-ttu-id="58429-109">Заметки к настройке производительности, отображающие действия [помощника по базам данных SQL Azure](sql-database-advisor.md)</span><span class="sxs-lookup"><span data-stu-id="58429-109">Performance tuning annotations that show actions performed by [SQL Azure Database Advisor](sql-database-advisor.md)</span></span>  



## <a name="prerequisites"></a><span data-ttu-id="58429-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="58429-110">Prerequisites</span></span>
* <span data-ttu-id="58429-111">Для анализа производительности запросов в базе данных должно быть активно [хранилище запросов](https://msdn.microsoft.com/library/dn817826.aspx) .</span><span class="sxs-lookup"><span data-stu-id="58429-111">Query Performance Insight requires that [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) is active on your database.</span></span> <span data-ttu-id="58429-112">Если хранилище запросов не выполняется, портал hello запрашивает tooturn ее на.</span><span class="sxs-lookup"><span data-stu-id="58429-112">If Query Store is not running, hello portal prompts you tooturn it on.</span></span>

## <a name="permissions"></a><span data-ttu-id="58429-113">Разрешения</span><span class="sxs-lookup"><span data-stu-id="58429-113">Permissions</span></span>
<span data-ttu-id="58429-114">следующие Hello [управления доступом на основе ролей](../active-directory/role-based-access-control-what-is.md) разрешения, необходимые toouse анализ производительности запросов:</span><span class="sxs-lookup"><span data-stu-id="58429-114">hello following [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions are required toouse Query Performance Insight:</span></span> 

* <span data-ttu-id="58429-115">**Модуль чтения**, **владельца**, **участника**, **участника базы данных SQL**, или **участника SQL Server** разрешения требуется tooview hello потреблением ресурсов запросы и диаграммы.</span><span class="sxs-lookup"><span data-stu-id="58429-115">**Reader**, **Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required tooview hello top resource consuming queries and charts.</span></span> 
* <span data-ttu-id="58429-116">**Владелец**, **участника**, **участника базы данных SQL**, или **участника SQL Server** разрешения, необходимые tooview текст запроса.</span><span class="sxs-lookup"><span data-stu-id="58429-116">**Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required tooview query text.</span></span>

## <a name="using-query-performance-insight"></a><span data-ttu-id="58429-117">Использование анализа производительности запросов</span><span class="sxs-lookup"><span data-stu-id="58429-117">Using Query Performance Insight</span></span>
<span data-ttu-id="58429-118">Анализ производительности запросов является простой toouse:</span><span class="sxs-lookup"><span data-stu-id="58429-118">Query Performance Insight is easy toouse:</span></span>

* <span data-ttu-id="58429-119">Откройте [портал Azure](https://portal.azure.com/) и базы данных поиска, которые должны tooexamine.</span><span class="sxs-lookup"><span data-stu-id="58429-119">Open [Azure portal](https://portal.azure.com/) and find database that you want tooexamine.</span></span> 
  * <span data-ttu-id="58429-120">В меню слева, в разделе поддержки и устранения неполадок, выберите "Анализ производительности запросов".</span><span class="sxs-lookup"><span data-stu-id="58429-120">From left-hand side menu, under support and troubleshooting, select “Query Performance Insight”.</span></span>
* <span data-ttu-id="58429-121">На первой вкладке hello просмотрите список hello ведущих ресурсоемких запросов.</span><span class="sxs-lookup"><span data-stu-id="58429-121">On hello first tab, review hello list of top resource-consuming queries.</span></span>
* <span data-ttu-id="58429-122">Выберите tooview отдельного запроса сведений о нем.</span><span class="sxs-lookup"><span data-stu-id="58429-122">Select an individual query tooview its details.</span></span>
* <span data-ttu-id="58429-123">Откройте [помощник по базам данных SQL Azure](sql-database-advisor.md) и проверьте наличие рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="58429-123">Open [SQL Azure Database Advisor](sql-database-advisor.md) and check if any recommendations are available.</span></span>
* <span data-ttu-id="58429-124">С помощью ползунков или масштабирования toochange значки наблюдается интервал.</span><span class="sxs-lookup"><span data-stu-id="58429-124">Use sliders or zoom icons toochange observed interval.</span></span>
  
    ![панель мониторинга производительности](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> <span data-ttu-id="58429-126">На пару часов данных должен toobe, записываемого хранилищем запросов для подробных сведений о производительности запросов tooprovide базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="58429-126">A couple hours of data needs toobe captured by Query Store for SQL Database tooprovide query performance insights.</span></span> <span data-ttu-id="58429-127">Если hello базы данных не содержит действий или хранилище запросов не работало в течение определенного периода времени, hello диаграммы будет пустым при отображении этого периода времени.</span><span class="sxs-lookup"><span data-stu-id="58429-127">If hello database has no activity or Query Store was not active during a certain time period, hello charts will be empty when displaying that time period.</span></span> <span data-ttu-id="58429-128">Можно включить хранилище запросов в любой момент, если оно не запущено.</span><span class="sxs-lookup"><span data-stu-id="58429-128">You may enable Query Store at any time if it is not running.</span></span>   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a><span data-ttu-id="58429-129">Просмотр запросов, максимально использующих ресурсы процессора</span><span class="sxs-lookup"><span data-stu-id="58429-129">Review top CPU consuming queries</span></span>
<span data-ttu-id="58429-130">В hello [портала](http://portal.azure.com) hello следующие:</span><span class="sxs-lookup"><span data-stu-id="58429-130">In hello [portal](http://portal.azure.com) do hello following:</span></span>

1. <span data-ttu-id="58429-131">Обзор tooa базы данных SQL и нажмите кнопку **все параметры** > **поддержки + Устранение неполадок** > **анализу производительности запросов**.</span><span class="sxs-lookup"><span data-stu-id="58429-131">Browse tooa SQL database and click **All settings** > **Support + Troubleshooting** > **Query performance insight**.</span></span> 
   
    ![Анализ производительности запросов][1]
   
    <span data-ttu-id="58429-133">Откроется представление первых запросов Hello и перечислены hello первых ЦП много запросов.</span><span class="sxs-lookup"><span data-stu-id="58429-133">hello top queries view opens and hello top CPU consuming queries are listed.</span></span>
2. <span data-ttu-id="58429-134">Щелкните вокруг диаграммы hello подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="58429-134">Click around hello chart for details.</span></span><br><span data-ttu-id="58429-135">Hello верхняя строка показывает общую % DTU для базы данных hello, а hello полосы показывают % ЦП, используемые запросами hello выбраны во время выбранного интервала hello (например, если **прошлая неделя** выбран каждый столбец представляет один день).</span><span class="sxs-lookup"><span data-stu-id="58429-135">hello top line shows overall DTU% for hello database, while hello bars show CPU% consumed by hello selected queries during hello selected interval (for example, if **Past week** is selected each bar represents one day).</span></span>
   
    ![наиболее ресурсоемкие запросы][2]
   
    <span data-ttu-id="58429-137">Hello нижней сетке представляет статистические данные для запросов видимым hello.</span><span class="sxs-lookup"><span data-stu-id="58429-137">hello bottom grid represents aggregated information for hello visible queries.</span></span>
   
   * <span data-ttu-id="58429-138">Идентификатор запроса — уникальный идентификатор запроса внутри базы данных.</span><span class="sxs-lookup"><span data-stu-id="58429-138">Query ID - unique identifier of query inside database.</span></span>
   * <span data-ttu-id="58429-139">Загрузка ЦП на запрос за период наблюдения (зависит от статистической функции).</span><span class="sxs-lookup"><span data-stu-id="58429-139">CPU per query during observable interval (depends on aggregation function).</span></span>
   * <span data-ttu-id="58429-140">Длительность запроса (зависит от статистической функции).</span><span class="sxs-lookup"><span data-stu-id="58429-140">Duration per query (depends on aggregation function).</span></span>
   * <span data-ttu-id="58429-141">Общее число выполнений определенного запроса.</span><span class="sxs-lookup"><span data-stu-id="58429-141">Total number of executions for a particular query.</span></span>
     
     <span data-ttu-id="58429-142">Установите или снимите tooinclude отдельные запросы или исключить их из диаграммы hello, с помощью флажков.</span><span class="sxs-lookup"><span data-stu-id="58429-142">Select or clear individual queries tooinclude or exclude them from hello chart using checkboxes.</span></span>
3. <span data-ttu-id="58429-143">Если данные устаревает, щелкните hello **обновление** кнопки.</span><span class="sxs-lookup"><span data-stu-id="58429-143">If your data becomes stale, click hello **Refresh** button.</span></span>
4. <span data-ttu-id="58429-144">Можно использовать ползунки и интервал toochange кнопки масштаба и исследовать пики: ![параметры](./media/sql-database-query-performance/zoom.png)</span><span class="sxs-lookup"><span data-stu-id="58429-144">You can use sliders and zoom buttons toochange observation interval and investigate spikes:  ![settings](./media/sql-database-query-performance/zoom.png)</span></span>
5. <span data-ttu-id="58429-145">При необходимости, если требуется другое представление, можно выбрать вкладку **Пользовательские** и задать:</span><span class="sxs-lookup"><span data-stu-id="58429-145">Optionally, if you want a different view, you can select **Custom** tab and set:</span></span>
   
   * <span data-ttu-id="58429-146">метрику (ЦП, длительность, число выполнений);</span><span class="sxs-lookup"><span data-stu-id="58429-146">Metric (CPU, duration, execution count)</span></span>
   * <span data-ttu-id="58429-147">интервал времени (последние 24 часа, за прошлую неделю, за прошлый месяц);</span><span class="sxs-lookup"><span data-stu-id="58429-147">Time interval (Last 24 hours, Past week, Past month).</span></span> 
   * <span data-ttu-id="58429-148">количество запросов;</span><span class="sxs-lookup"><span data-stu-id="58429-148">Number of queries.</span></span>
   * <span data-ttu-id="58429-149">статистическую функцию.</span><span class="sxs-lookup"><span data-stu-id="58429-149">Aggregation function.</span></span>
     
     ![Параметры](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a><span data-ttu-id="58429-151">Просмотр подробных сведений для отдельного запроса</span><span class="sxs-lookup"><span data-stu-id="58429-151">Viewing individual query details</span></span>
<span data-ttu-id="58429-152">сведения о запросе tooview:</span><span class="sxs-lookup"><span data-stu-id="58429-152">tooview query details:</span></span>

1. <span data-ttu-id="58429-153">Щелкните любой запрос в списке hello первых запросов.</span><span class="sxs-lookup"><span data-stu-id="58429-153">Click any query in hello list of top queries.</span></span>
   
    ![сведения](./media/sql-database-query-performance/details.png)
2. <span data-ttu-id="58429-155">Откроется представление сведений Hello и разбивкой число потребления или длительность или выполнения ЦП hello запросов со временем.</span><span class="sxs-lookup"><span data-stu-id="58429-155">hello details view opens and hello queries CPU consumption/Duration/Execution count is broken down over time.</span></span>
3. <span data-ttu-id="58429-156">Щелкните вокруг диаграммы hello подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="58429-156">Click around hello chart for details.</span></span>
   
   * <span data-ttu-id="58429-157">Верхней диаграмме показано строки с общей базы данных % DTU и гистограммы hello — % ЦП, использованное hello выбранного запроса.</span><span class="sxs-lookup"><span data-stu-id="58429-157">Top chart shows line with overall database DTU%, and hello bars are CPU% consumed by hello selected query.</span></span>
   * <span data-ttu-id="58429-158">Второй диаграмме показана общая длительность при hello выбранного запроса.</span><span class="sxs-lookup"><span data-stu-id="58429-158">Second chart shows total duration by hello selected query.</span></span>
   * <span data-ttu-id="58429-159">Нижней диаграмме показано общее число выполнений при hello выбранного запроса.</span><span class="sxs-lookup"><span data-stu-id="58429-159">Bottom chart shows total number of executions by hello selected query.</span></span>
     
     ![сведения о запросе][3]
4. <span data-ttu-id="58429-161">При необходимости используйте ползунки, кнопки масштаба или **параметры** toocustomize отображением данных, запросов или toopick к другому периоду времени.</span><span class="sxs-lookup"><span data-stu-id="58429-161">Optionally, use sliders, zoom buttons or click **Settings** toocustomize how query data is displayed, or toopick a different time period.</span></span>

## <a name="review-top-queries-per-duration"></a><span data-ttu-id="58429-162">Просмотр запросов с наибольшей длительностью</span><span class="sxs-lookup"><span data-stu-id="58429-162">Review top queries per duration</span></span>
<span data-ttu-id="58429-163">В hello последнее обновление анализ производительности запросов, мы представили два новых метрики, которые могут помочь выявить потенциальные узкие места: счетчика длительности и выполнения.</span><span class="sxs-lookup"><span data-stu-id="58429-163">In hello recent update of Query Performance Insight, we introduced two new metrics that can help you identify potential bottlenecks: duration and execution count.</span></span><br>

<span data-ttu-id="58429-164">Длительные запросы имеют наибольшую вероятность блокировки больше ресурсов, блокировки других пользователей и ограничение масштабируемости hello.</span><span class="sxs-lookup"><span data-stu-id="58429-164">Long-running queries have hello greatest potential for locking resources longer, blocking other users, and limiting scalability.</span></span> <span data-ttu-id="58429-165">Они также являются hello наиболее подходящих для оптимизации.</span><span class="sxs-lookup"><span data-stu-id="58429-165">They are also hello best candidates for optimization.</span></span><br>

<span data-ttu-id="58429-166">tooidentify длительных запросов:</span><span class="sxs-lookup"><span data-stu-id="58429-166">tooidentify long running queries:</span></span>

1. <span data-ttu-id="58429-167">Откройте вкладку **Пользовательские** в колонке "Анализ производительности запросов" для выбранной базы данных.</span><span class="sxs-lookup"><span data-stu-id="58429-167">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="58429-168">Изменение метрики toobe **длительность**</span><span class="sxs-lookup"><span data-stu-id="58429-168">Change metrics toobe **duration**</span></span>
3. <span data-ttu-id="58429-169">Выберите количество запросов и интервал наблюдения.</span><span class="sxs-lookup"><span data-stu-id="58429-169">Select number of queries and observation interval</span></span>
4. <span data-ttu-id="58429-170">Выберите статистическую функцию.</span><span class="sxs-lookup"><span data-stu-id="58429-170">Select aggregation function</span></span>
   
   * <span data-ttu-id="58429-171">**Сумма** суммирует время выполнения запроса на протяжении всего интервала наблюдения.</span><span class="sxs-lookup"><span data-stu-id="58429-171">**Sum** adds up all query execution time during whole observation interval.</span></span>
   * <span data-ttu-id="58429-172">**Максимум** находит запросы, время выполнения которых было максимальным на всем интервале наблюдения.</span><span class="sxs-lookup"><span data-stu-id="58429-172">**Max** finds queries which execution time was maximum at whole observation interval.</span></span>
   * <span data-ttu-id="58429-173">**AVG** находит среднее время выполнения всех выполнений запрос и Показать hello верхней вне эти средние значения.</span><span class="sxs-lookup"><span data-stu-id="58429-173">**Avg** finds average execution time of all query executions and show you hello top out of these averages.</span></span> 
     
     ![Длительность запроса][4]

## <a name="review-top-queries-per-execution-count"></a><span data-ttu-id="58429-175">Просмотр запросов с наибольшим числом выполнений</span><span class="sxs-lookup"><span data-stu-id="58429-175">Review top queries per execution count</span></span>
<span data-ttu-id="58429-176">Большое число выполнений может не влиять на саму базу данных, и использование ресурсов может быть небольшим, но общая производительность приложения может понизиться.</span><span class="sxs-lookup"><span data-stu-id="58429-176">High number of executions might not be affecting database itself and resources usage can be low, but overall application might get slow.</span></span>

<span data-ttu-id="58429-177">В некоторых случаях большое число выполнений может вызвать tooincrease сети циклов приема-передачи.</span><span class="sxs-lookup"><span data-stu-id="58429-177">In some cases, very high execution count may lead tooincrease of network round trips.</span></span> <span data-ttu-id="58429-178">Круговые пути существенно влияют на производительность.</span><span class="sxs-lookup"><span data-stu-id="58429-178">Round trips significantly affect performance.</span></span> <span data-ttu-id="58429-179">Они являются задержки toonetwork субъекта и задержка toodownstream сервера.</span><span class="sxs-lookup"><span data-stu-id="58429-179">They are subject toonetwork latency and toodownstream server latency.</span></span> 

<span data-ttu-id="58429-180">Например многие веб-сайты, управляемые данными сильно доступа к базе данных hello для каждого запроса пользователя.</span><span class="sxs-lookup"><span data-stu-id="58429-180">For example, many data-driven Web sites heavily access hello database for every user request.</span></span> <span data-ttu-id="58429-181">При организации пулов соединений помогает, hello увеличить сетевой трафик и нагрузку на сервер базы данных hello может отрицательно сказаться на производительности.</span><span class="sxs-lookup"><span data-stu-id="58429-181">While connection pooling helps, hello increased network traffic and processing load on hello database server can adversely affect performance.</span></span>  <span data-ttu-id="58429-182">Общие рекомендации — tookeep round абсолютному минимуму tooan приема-передачи.</span><span class="sxs-lookup"><span data-stu-id="58429-182">General advice is tookeep round trips tooan absolute minimum.</span></span>

<span data-ttu-id="58429-183">tooidentify часто выполняемые запросы («нестабильной») запросы:</span><span class="sxs-lookup"><span data-stu-id="58429-183">tooidentify frequently executed queries (“chatty”) queries:</span></span>

1. <span data-ttu-id="58429-184">Откройте вкладку **Пользовательские** в колонке "Анализ производительности запросов" для выбранной базы данных.</span><span class="sxs-lookup"><span data-stu-id="58429-184">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="58429-185">Изменение метрики toobe **число выполнений**</span><span class="sxs-lookup"><span data-stu-id="58429-185">Change metrics toobe **execution count**</span></span>
3. <span data-ttu-id="58429-186">Выберите количество запросов и интервал наблюдения.</span><span class="sxs-lookup"><span data-stu-id="58429-186">Select number of queries and observation interval</span></span>
   
    ![Число выполнений запроса][5]

## <a name="understanding-performance-tuning-annotations"></a><span data-ttu-id="58429-188">Основные сведения о заметках к настройке производительности</span><span class="sxs-lookup"><span data-stu-id="58429-188">Understanding performance tuning annotations</span></span>
<span data-ttu-id="58429-189">При просмотре в анализ производительности запросов рабочей нагрузки, можно заметить значков с вертикальной линии в верхней части диаграммы hello.</span><span class="sxs-lookup"><span data-stu-id="58429-189">While exploring your workload in Query Performance Insight, you might notice icons with vertical line on top of hello chart.</span></span><br>

<span data-ttu-id="58429-190">Эти значки — заметки. Они представляют действия, влияющие на производительность, которые выполняет [помощник по базам данных SQL Azure](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="58429-190">These icons are annotations; they represent performance affecting actions performed by [SQL Azure Database Advisor](sql-database-advisor.md).</span></span> <span data-ttu-id="58429-191">Путем наведения указателя заметки получить основные сведения о действии hello:</span><span class="sxs-lookup"><span data-stu-id="58429-191">By hovering annotation, you get basic information about hello action:</span></span>

![Заметка к запросу][6]

<span data-ttu-id="58429-193">Если требуется несколько tooknow или применить рекомендации, щелкните значок hello.</span><span class="sxs-lookup"><span data-stu-id="58429-193">If you want tooknow more or apply advisor recommendation, click hello icon.</span></span> <span data-ttu-id="58429-194">Отобразятся подробные сведения о действии.</span><span class="sxs-lookup"><span data-stu-id="58429-194">It will open details of action.</span></span> <span data-ttu-id="58429-195">При наличии активной рекомендации ее можно немедленно применить с помощью команды.</span><span class="sxs-lookup"><span data-stu-id="58429-195">If it’s an active recommendation you can apply it straight away using command.</span></span>

![Сведения заметки к запросу][7]

### <a name="multiple-annotations"></a><span data-ttu-id="58429-197">Несколько заметок</span><span class="sxs-lookup"><span data-stu-id="58429-197">Multiple annotations.</span></span>
<span data-ttu-id="58429-198">Это возможно, что из-за уровень масштаба заметки, закрыть tooeach других будет получить сворачиваться в один.</span><span class="sxs-lookup"><span data-stu-id="58429-198">It’s possible, that because of zoom level, annotations that are close tooeach other will get collapsed into one.</span></span> <span data-ttu-id="58429-199">В этом случае отображается специальный значок. Если щелкнуть его, откроется новая колонка со списком сгруппированных заметок.</span><span class="sxs-lookup"><span data-stu-id="58429-199">This will be represented by special icon, clicking it will open new blade where list of grouped annotations will be shown.</span></span>
<span data-ttu-id="58429-200">Корреляция запросов и действий по настройке производительности могут помочь toobetter сведения о рабочей нагрузке.</span><span class="sxs-lookup"><span data-stu-id="58429-200">Correlating queries and performance tuning actions can help toobetter understand your workload.</span></span> 

## <a name="optimizing-hello-query-store-configuration-for-query-performance-insight"></a><span data-ttu-id="58429-201">Оптимизация hello конфигурацию хранилища запросов для анализ производительности запросов</span><span class="sxs-lookup"><span data-stu-id="58429-201">Optimizing hello Query Store configuration for Query Performance Insight</span></span>
<span data-ttu-id="58429-202">Во время использования анализ производительности запросов могут возникнуть следующие хранилища запросов сообщений hello:</span><span class="sxs-lookup"><span data-stu-id="58429-202">During your use of Query Performance Insight, you might encounter hello following Query Store messages:</span></span>

* <span data-ttu-id="58429-203">"Хранилище запросов настроено неоптимальным образом для этой базы данных.</span><span class="sxs-lookup"><span data-stu-id="58429-203">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="58429-204">Щелкните здесь, дополнительные toolearn.»</span><span class="sxs-lookup"><span data-stu-id="58429-204">Click here toolearn more."</span></span>
* <span data-ttu-id="58429-205">"Хранилище запросов настроено неоптимальным образом для этой базы данных.</span><span class="sxs-lookup"><span data-stu-id="58429-205">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="58429-206">Щелкните здесь параметры toochange.»</span><span class="sxs-lookup"><span data-stu-id="58429-206">Click here toochange settings."</span></span> 

<span data-ttu-id="58429-207">Эти сообщения обычно отображаются, когда хранилище запросов не может toocollect новых данных.</span><span class="sxs-lookup"><span data-stu-id="58429-207">These messages usually appear when Query Store is not able toocollect new data.</span></span> 

<span data-ttu-id="58429-208">Первый случай происходит, когда хранилище запросов находится в состоянии "только чтение" и заданы оптимальные параметры.</span><span class="sxs-lookup"><span data-stu-id="58429-208">First case happens when Query Store is in Read-Only state and parameters are set optimally.</span></span> <span data-ttu-id="58429-209">Это можно исправить, увеличив размер хранилища запросов или очистив его.</span><span class="sxs-lookup"><span data-stu-id="58429-209">You can fix this by increasing size of Query Store or clearing Query Store.</span></span>

![Кнопка для qds][8]

<span data-ttu-id="58429-211">Второй случай происходит, когда хранилище запросов отключено или не заданы оптимальные параметры.</span><span class="sxs-lookup"><span data-stu-id="58429-211">Second case happens when Query Store is Off or parameters aren’t set optimally.</span></span> <br><span data-ttu-id="58429-212">Hello хранения и отслеживания политик и включить хранилище запросов можно изменить, выполнив приведенную ниже команду, или непосредственно с портала:</span><span class="sxs-lookup"><span data-stu-id="58429-212">You can change hello Retention and Capture policy and enable Query Store by executing commands below or directly from portal:</span></span>

![Кнопка для qds][9]

### <a name="recommended-retention-and-capture-policy"></a><span data-ttu-id="58429-214">Рекомендуемая политика хранения и отслеживания</span><span class="sxs-lookup"><span data-stu-id="58429-214">Recommended retention and capture policy</span></span>
<span data-ttu-id="58429-215">Политики хранения бывают двух видов.</span><span class="sxs-lookup"><span data-stu-id="58429-215">There are two types of retention policies:</span></span>

* <span data-ttu-id="58429-216">Размер от - при достижении tooAUTO набора, он будет очистить данные автоматически при рядом с максимальным размером.</span><span class="sxs-lookup"><span data-stu-id="58429-216">Size based - if set tooAUTO it will clean data automatically when near max size is reached.</span></span>
* <span data-ttu-id="58429-217">На основе - времени по умолчанию, мы установим too30 дней, означающее, что, если хранилище запросов будет не останется свободного места, он приведет к удалению запрашивать данные старше 30 дней</span><span class="sxs-lookup"><span data-stu-id="58429-217">Time based - by default we will set it too30 days, which means, if Query Store will run out of space, it will delete query information older than 30 days</span></span>

<span data-ttu-id="58429-218">Для политики отслеживания доступны следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="58429-218">Capture policy could be set to:</span></span>

* <span data-ttu-id="58429-219">**All** — фиксируются все запросы.</span><span class="sxs-lookup"><span data-stu-id="58429-219">**All** - Captures all queries.</span></span>
* <span data-ttu-id="58429-220">**Auto** — редкие запросы и запросы с незначительным временем компиляции и выполнения игнорируются.</span><span class="sxs-lookup"><span data-stu-id="58429-220">**Auto** - Infrequent queries and queries with insignificant compile and execution duration are ignored.</span></span> <span data-ttu-id="58429-221">Пороговые значения счетчика, а также времени компиляции и выполнения определяются внутренним образом.</span><span class="sxs-lookup"><span data-stu-id="58429-221">Thresholds for execution count, compile and runtime duration are internally determined.</span></span> <span data-ttu-id="58429-222">Это параметр по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="58429-222">This is hello default option.</span></span>
* <span data-ttu-id="58429-223">**Нет** — хранилище запросов прекращает запись новых запросов, однако по-прежнему собирает статистику выполнения уже записанных запросов.</span><span class="sxs-lookup"><span data-stu-id="58429-223">**None** - Query Store stops capturing new queries, however runtime stats for already captured queries are still collected.</span></span>

<span data-ttu-id="58429-224">Рекомендуется установить все tooAUTO политики и политики чистой too30 дней:</span><span class="sxs-lookup"><span data-stu-id="58429-224">We recommend setting all policies tooAUTO and clean policy too30 days:</span></span>

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

<span data-ttu-id="58429-225">Увеличение размера хранилища запросов.</span><span class="sxs-lookup"><span data-stu-id="58429-225">Increase size of Query Store.</span></span> <span data-ttu-id="58429-226">Это может быть выполнено подключение базы данных tooa и выдают следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="58429-226">This could be performed by connecting tooa database and issuing following query:</span></span>

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

<span data-ttu-id="58429-227">Применение этих параметров в конечном счете хранилище запросов, сбор новых запросов, однако если вы не хотите toowait можно очистить хранилище запросов.</span><span class="sxs-lookup"><span data-stu-id="58429-227">Applying these settings will eventually make Query Store collecting new queries, however if you don’t want toowait you can clear Query Store.</span></span> 

> [!NOTE]
> <span data-ttu-id="58429-228">Выполнение следующего запроса приведет к удалению всех текущие данные в хранилище запросов hello.</span><span class="sxs-lookup"><span data-stu-id="58429-228">Executing following query will delete all current information in hello Query Store.</span></span> 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a><span data-ttu-id="58429-229">Сводка</span><span class="sxs-lookup"><span data-stu-id="58429-229">Summary</span></span>
<span data-ttu-id="58429-230">Анализ производительности запросов помогает понять влияние рабочей нагрузки запросов hello и его связь toodatabase потребления ресурсов.</span><span class="sxs-lookup"><span data-stu-id="58429-230">Query Performance Insight helps you understand hello impact of your query workload and how it relates toodatabase resource consumption.</span></span> <span data-ttu-id="58429-231">С помощью этой функции будет Узнайте о hello самые ресурсоемкие запросы и легко определять toofix hello из них, прежде чем они станут проблемы.</span><span class="sxs-lookup"><span data-stu-id="58429-231">With this feature, you will learn about hello top consuming queries, and easily identify hello ones toofix before they become a problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58429-232">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="58429-232">Next steps</span></span>
<span data-ttu-id="58429-233">Дополнительные рекомендации о повышении производительности hello вашей базы данных SQL щелкните [рекомендации](sql-database-advisor.md) на hello **анализ производительности запросов** колонку.</span><span class="sxs-lookup"><span data-stu-id="58429-233">For additional recommendations about improving hello performance of your SQL database, click [Recommendations](sql-database-advisor.md) on hello **Query Performance Insight** blade.</span></span>

![Помощник по производительности](./media/sql-database-query-performance/ia.png)

<!--Image references-->
[1]: ./media/sql-database-query-performance/tile.png
[2]: ./media/sql-database-query-performance/top-queries.png
[3]: ./media/sql-database-query-performance/query-details.png
[4]: ./media/sql-database-query-performance/top-duration.png
[5]: ./media/sql-database-query-performance/top-execution.png
[6]: ./media/sql-database-query-performance/annotation.png
[7]: ./media/sql-database-query-performance/annotation-details.png
[8]: ./media/sql-database-query-performance/qds-off.png
[9]: ./media/sql-database-query-performance/qds-button.png

