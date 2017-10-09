---
title: "aaaManage баз данных в хранилище данных SQL Azure | Документы Microsoft"
description: "Общие сведения об управлении базами данных в хранилище данных SQL. Рассматриваются средства управления, динамические административные представления и масштабирование производительности, устранение неполадок с запросами, создание надлежащих политик безопасности и восстановление базы данных после повреждения данных или регионального сбоя."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 8576fdb3-71fe-4b3b-a4e0-5e8a7f148acf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: caec6572c4ab395107c3b095adc69a53eae8bd88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-databases-in-azure-sql-data-warehouse"></a><span data-ttu-id="c9eb5-104">Управление базами данных в хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="c9eb5-104">Manage databases in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="c9eb5-105">Хранилище данных SQL позволяет автоматизировать многие аспекты управления базами данных.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-105">SQL Data Warehouse automates many aspects of managing your databases.</span></span> <span data-ttu-id="c9eb5-106">Например производительности tooscale достаточно tooadjust и платить за hello справа уровня вычислительных ресурсов и подождите, пока хранилище данных SQL выполните все процессы hello масштабное развертывание и масштабирование назад.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-106">For example, tooscale performance you only need tooadjust and pay for hello right level of compute resources, and then let SQL Data Warehouse do all hello work of scaling out and scaling back.</span></span>

<span data-ttu-id="c9eb5-107">Без сомнения требуется toomonitor вашей рабочей нагрузки tooidentify производительность требуется, а также устранение неполадок длительных запросов.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-107">You will undoubtedly want toomonitor your workload tooidentify your performance needs as well as troubleshoot long-running queries.</span></span> <span data-ttu-id="c9eb5-108">Необходимо также tooperform несколько задач toomanage права доступа для пользователей и имена входа.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-108">You will also need tooperform a few security tasks toomanage permissions for users and logins.</span></span>

<span data-ttu-id="c9eb5-109">В этом обзоре рассматриваются следующие аспекты управления хранилищем данных SQL.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-109">This overview covers these aspects of managing SQL Data Warehouse.</span></span>

* <span data-ttu-id="c9eb5-110">Средства управления</span><span class="sxs-lookup"><span data-stu-id="c9eb5-110">Management tools</span></span>
* <span data-ttu-id="c9eb5-111">Масштабирование вычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="c9eb5-111">Scale Compute</span></span>
* <span data-ttu-id="c9eb5-112">Остановка и возобновление</span><span class="sxs-lookup"><span data-stu-id="c9eb5-112">Pause and Resume</span></span>
* <span data-ttu-id="c9eb5-113">Рекомендации по производительности</span><span class="sxs-lookup"><span data-stu-id="c9eb5-113">Performance Best Practices</span></span>
* <span data-ttu-id="c9eb5-114">Мониторинг запросов</span><span class="sxs-lookup"><span data-stu-id="c9eb5-114">Query Monitoring</span></span>
* <span data-ttu-id="c9eb5-115">Безопасность</span><span class="sxs-lookup"><span data-stu-id="c9eb5-115">Security</span></span>
* <span data-ttu-id="c9eb5-116">Архивация и восстановление</span><span class="sxs-lookup"><span data-stu-id="c9eb5-116">Backup and restore</span></span>

## <a name="management-tools"></a><span data-ttu-id="c9eb5-117">Средства управления</span><span class="sxs-lookup"><span data-stu-id="c9eb5-117">Management tools</span></span>
<span data-ttu-id="c9eb5-118">Можно использовать различные базы данных toomanage средства в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-118">You can use a variety of tools toomanage databases in SQL Data Warehouse.</span></span> <span data-ttu-id="c9eb5-119">При управлении баз данных, будет разрабатывать средства настройки для каждого типа задач необходимо tooperform.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-119">As you manage databases, you will develop tool preferences for each type of task you need tooperform.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="c9eb5-120">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="c9eb5-120">Azure portal</span></span>
<span data-ttu-id="c9eb5-121">Hello [портал Azure] [ Azure portal] является веб-порталом, где можно создавать, обновлять и удаление баз данных и отслеживать ресурсы базы данных.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-121">hello [Azure portal][Azure portal] is a web-based portal where you can create, update, and delete databases and monitor database resources.</span></span> <span data-ttu-id="c9eb5-122">Это средство удобно — Если вы новичок в Azure, управлять небольшим числом баз данных хранилища данных, либо требуется tooquickly каким-либо.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-122">This tool is great is if you're just getting started with Azure, managing a small number of data warehouse databases, or need tooquickly do something.</span></span>

<span data-ttu-id="c9eb5-123">tooget к работе с hello портал Azure в разделе [Создание хранилища данных SQL (портал Azure)][Create a SQL Data Warehouse (Azure portal)].</span><span class="sxs-lookup"><span data-stu-id="c9eb5-123">tooget started with hello Azure portal, see [Create a SQL Data Warehouse (Azure portal)][Create a SQL Data Warehouse (Azure portal)].</span></span>

### <a name="sql-server-data-tools-in-visual-studio"></a><span data-ttu-id="c9eb5-124">SQL Server Data Tools в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c9eb5-124">SQL Server Data Tools in Visual Studio</span></span>
<span data-ttu-id="c9eb5-125">[SQL Server Data Tools] [ SQL Server Data Tools] (SSDT) в Visual Studio позволяет вам tooconnect для управления и разработки баз данных.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-125">[SQL Server Data Tools][SQL Server Data Tools] (SSDT) in Visual Studio allows you tooconnect to, manage, and develop your databases.</span></span> <span data-ttu-id="c9eb5-126">Если вы не новичок в разработке приложений и уже знакомы с Visual Studio или другими интегрированными средами разработки (IDE), предлагаем обратить внимание на SSDT в составе Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-126">If you're an application developer familiar with Visual Studio or other integrated development environments (IDEs), try using SSDT in Visual Studio.</span></span>

<span data-ttu-id="c9eb5-127">Средства SSDT включают hello обозреватель объектов SQL Server, позволяющий toovisualize, подключитесь и выполните сценарий на основе баз данных хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-127">SSDT includes hello SQL Server Object Explorer which enables you toovisualize, connect, and execute scripts against SQL Data Warehouse databases.</span></span> <span data-ttu-id="c9eb5-128">tooquickly подключения tooSQL хранилища данных, можно просто щелкнуть hello **в среде Visual Studio** кнопки на панели команд hello при просмотре сведений базы данных hello в hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-128">tooquickly connect tooSQL Data Warehouse, you can simply click hello **Open in Visual Studio** button in hello command bar when viewing hello database details in hello Azure Classic Portal.</span></span>  

<span data-ttu-id="c9eb5-129">tooget к работе с SSDT в Visual Studio в разделе [запросов хранилища данных SQL Azure с помощью Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="c9eb5-129">tooget started with SSDT in Visual Studio, see [Query Azure SQL Data Warehouse with Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].</span></span>

### <a name="command-line-tools"></a><span data-ttu-id="c9eb5-130">Программы командной строки</span><span class="sxs-lookup"><span data-stu-id="c9eb5-130">Command-line tools</span></span>
<span data-ttu-id="c9eb5-131">Средства командной строки идеально подходят для автоматизации рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-131">Command line tools are ideal for automating your workloads.</span></span>  <span data-ttu-id="c9eb5-132">PowerShell и sqlcmd являются двумя tooautomate замечательные возможности процессы.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-132">PowerShell and sqlcmd are two great ways tooautomate your processes.</span></span>  <span data-ttu-id="c9eb5-133">Рекомендуется, чтобы эти средства для управления большим числом логических серверов и развертывание изменения ресурсов в рабочей среде, как можно в скрипт и затем автоматизировать необходимые задачи hello.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-133">We recommend these tools for managing a large number of logical servers and deploying resource changes in a production environment as hello tasks necessary can be scripted and then automated.</span></span>

### <a name="dynamic-management-views"></a><span data-ttu-id="c9eb5-134">Динамические административные представления</span><span class="sxs-lookup"><span data-stu-id="c9eb5-134">Dynamic management views</span></span>
<span data-ttu-id="c9eb5-135">Динамические административные представления являются hello хлеб совершенно необходимые для управления хранилищем данных SQL.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-135">DMVs are hello bread and butter of managing SQL Data Warehouse.</span></span> <span data-ttu-id="c9eb5-136">Почти все сведения, который предоставляет доступ к порталу hello полагается на динамические административные представления.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-136">Almost all information that surfaces in hello portal relies on DMVs.</span></span> <span data-ttu-id="c9eb5-137">toosee список DMV хранилища данных SQL, в разделе [системных представлений SQL Data Warehouse][SQL Data Warehouse system views].</span><span class="sxs-lookup"><span data-stu-id="c9eb5-137">toosee a list of SQL Data Warehouse DMVs, see [SQL Data Warehouse system views][SQL Data Warehouse system views].</span></span>

<span data-ttu-id="c9eb5-138">tooget работы см. в разделе [подключение и запрос с помощью sqlcmd][Connect and query with sqlcmd], и [Создание базы данных (PowerShell)][Create a database (PowerShell)].</span><span class="sxs-lookup"><span data-stu-id="c9eb5-138">tooget started, see [Connect and query with sqlcmd][Connect and query with sqlcmd], and [Create a database (PowerShell)][Create a database (PowerShell)].</span></span>

## <a name="scale-compute"></a><span data-ttu-id="c9eb5-139">Масштабирование вычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="c9eb5-139">Scale compute</span></span>
<span data-ttu-id="c9eb5-140">В хранилище данных SQL можно быстро увеличить или уменьшить производительность, настроив объем вычислительных ресурсов ЦП, памяти и пропускной способности ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-140">In SQL Data Warehouse, you can quickly scale performance out or back by increasing or decreasing compute resources of CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="c9eb5-141">производительность tooscale все что нужно toodo — задайте число hello единицы хранилища данных (Dwu), что хранилище данных SQL выделяет tooyour базы данных.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-141">tooscale performance, all you need toodo is adjust hello number of data warehouse units (DWUs) that SQL Data Warehouse allocates tooyour database.</span></span> <span data-ttu-id="c9eb5-142">Хранилище данных SQL быстро делает изменить hello и обрабатывает все базовые изменения toohardware hello или программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-142">SQL Data Warehouse quickly makes hello change and handles all hello underlying changes toohardware or software.</span></span>

<span data-ttu-id="c9eb5-143">. в разделе toolearn Дополнительные сведения о масштабировании Dwu, [масштабирования производительности].</span><span class="sxs-lookup"><span data-stu-id="c9eb5-143">toolearn more about scaling DWUs, see [Scale performance].</span></span>

## <a name="pause-and-resume"></a><span data-ttu-id="c9eb5-144">Остановка и возобновление</span><span class="sxs-lookup"><span data-stu-id="c9eb5-144">Pause and resume</span></span>
<span data-ttu-id="c9eb5-145">toosave затраты, можно приостановить и возобновить вычислительные ресурсы по требованию.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-145">toosave costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="c9eb5-146">Например если не будет использоваться hello базы данных во время ночь hello и по выходным, можно приостановить ее работу в то время и возобновите ее работу в течение дня hello.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-146">For example, if you won't be using hello database during hello night and on weekends, you can pause it during those times, and resume it during hello day.</span></span> <span data-ttu-id="c9eb5-147">Вы не будете платить за Dwu во время приостановки базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-147">You won't be charged for DWUs while hello database is paused.</span></span>

<span data-ttu-id="c9eb5-148">Дополнительные сведения см. в статьях [Приостановка работы вычислительных ресурсов][Pause compute] и [Возобновление работы вычислительных ресурсов][Resume compute].</span><span class="sxs-lookup"><span data-stu-id="c9eb5-148">For more information, see [Pause compute][Pause compute], and [Resume compute][Resume compute].</span></span>

## <a name="performance-best-practices"></a><span data-ttu-id="c9eb5-149">Рекомендации по производительности</span><span class="sxs-lookup"><span data-stu-id="c9eb5-149">Performance Best Practices</span></span>
<span data-ttu-id="c9eb5-150">Когда Приступая к работе с новой технологией, обнаружение hello советы и рекомендации, которые работают наилучшим справа от начала hello может сэкономить много времени.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-150">When getting started with a new technology, discovering hello tips and tricks that work best right from hello start can save you lots of time.</span></span>  <span data-ttu-id="c9eb5-151">Рекомендации приводятся во многих наших разделах.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-151">You will find best practices throughout many of our topics.</span></span>

<span data-ttu-id="c9eb5-152">toosee много Сводка hello наиболее важные вопросы при разработке рабочей нагрузки в разделе [рекомендации данных SQL хранилища][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="c9eb5-152">toosee many a summary of hello most important considerations when developing your workload, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

## <a name="query-monitoring"></a><span data-ttu-id="c9eb5-153">Мониторинг запросов</span><span class="sxs-lookup"><span data-stu-id="c9eb5-153">Query Monitoring</span></span>
<span data-ttu-id="c9eb5-154">Иногда запрос выполняется слишком много времени, но точно не известно, какой из них является причиной hello.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-154">Sometimes a query is running too long, but you aren't sure of which one is hello culprit.</span></span> <span data-ttu-id="c9eb5-155">Хранилище данных SQL содержит динамические административные представления (DMV), которые можно использовать toofigure ожидания какой запрос занимает слишком много времени.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-155">SQL Data Warehouse has dynamic management views (DMVs) that you can use toofigure out which query is taking too long.</span></span>

<span data-ttu-id="c9eb5-156">toofind долго выполняющихся запросов, в разделе [мониторинг рабочей нагрузки с помощью динамических административных представлений][Monitor your workload using DMVs].</span><span class="sxs-lookup"><span data-stu-id="c9eb5-156">toofind long-running queries, see [Monitor your workload using DMVs][Monitor your workload using DMVs].</span></span>

## <a name="security"></a><span data-ttu-id="c9eb5-157">Безопасность</span><span class="sxs-lookup"><span data-stu-id="c9eb5-157">Security</span></span>
<span data-ttu-id="c9eb5-158">toomaintain система безопасности, должен быть предупреждение hello и защиты от несанкционированного доступа любого типа.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-158">toomaintain a secure system, you must be on hello alert and guard against any type of unauthorized access.</span></span> <span data-ttu-id="c9eb5-159">Система безопасности должна toomake убедитесь, что правила брандмауэра на месте, что только авторизованных можно подключиться с помощью IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-159">A security system needs toomake sure firewall rules are in place so only authorized IP addresses can connect.</span></span> <span data-ttu-id="c9eb5-160">Также требуется надлежащая проверка подлинности учетных данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-160">It needs proper authentication of user credentials.</span></span> <span data-ttu-id="c9eb5-161">После подключения пользователя базы данных toohello hello пользователя должна иметь только разрешения tooperform минимальное количество действий.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-161">After a user has connected toohello database, hello user should only have permissions tooperform a minimal number of actions.</span></span> <span data-ttu-id="c9eb5-162">toosecure данных, можно использовать шифрование.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-162">toosecure data, you can use encryption.</span></span> <span data-ttu-id="c9eb5-163">Это также важно toohave аудит и отслеживание, поэтому вы сможете события, если все подозрительные действия.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-163">It's also important toohave auditing and tracking so you can retrace events if there is any suspicious activity.</span></span>

<span data-ttu-id="c9eb5-164">toolearn об управлении безопасностью заголовок над toohello [Общие сведения о безопасности][Security overview].</span><span class="sxs-lookup"><span data-stu-id="c9eb5-164">toolearn about managing security, head over toohello [Security overview][Security overview].</span></span>

## <a name="backup-and-restore"></a><span data-ttu-id="c9eb5-165">Архивация и восстановление</span><span class="sxs-lookup"><span data-stu-id="c9eb5-165">Backup and restore</span></span>
<span data-ttu-id="c9eb5-166">Наличие надежных резервных копий данных является важной частью любой рабочей базы данных.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-166">Having reliable backps of your data is an essential part of any production database.</span></span> <span data-ttu-id="c9eb5-167">Хранилище данных SQL защищает ваши данные за счет автоматической архивации активных баз данных через регулярные интервалы.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-167">SQL Data Warehouse keeps your data safe by automatically backing up your active databases at regular intervals.</span></span> <span data-ttu-id="c9eb5-168">Эти резервные копии позволяют toorecover из сценариев, где были повреждены данные или случайному удалению данных или базы данных.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-168">These backups allow you toorecover from scenarios where you've corrupted your data or accidentally dropped your data or database.</span></span>  <span data-ttu-id="c9eb5-169">Для hello данных расписания резервного копирования, политика хранения и как увидеть toorestore базы данных, [восстановление из снимка][Restore from snapshot].</span><span class="sxs-lookup"><span data-stu-id="c9eb5-169">For hello data backup schedule, retention policy and how toorestore a database, see [Restore from snapshot][Restore from snapshot].</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9eb5-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c9eb5-170">Next steps</span></span>
<span data-ttu-id="c9eb5-171">Применение принципы проектирования базы данных позволит упростить toomanage баз данных в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-171">Using good database design principles will make it easier toomanage your databases in SQL Data Warehouse.</span></span> <span data-ttu-id="c9eb5-172">Дополнительные, toolearn head через toohello [Общие сведения о разработке][Development overview].</span><span class="sxs-lookup"><span data-stu-id="c9eb5-172">toolearn more, head over toohello [Development overview][Development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse (Azure Portal)]: sql-data-warehouse-get-started-provision.md
[Create a database (PowerShell)]: sql-data-warehouse-get-started-provision-powershell.md
[connection]: sql-data-warehouse-develop-connections.md
[Query Azure SQL Data Warehouse with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[Connect and query with sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md
[Development overview]: sql-data-warehouse-overview-develop.md
[Monitor your workload using DMVs]: sql-data-warehouse-manage-monitor.md
[Pause compute]: sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Restore from snapshot]: sql-data-warehouse-restore-database-overview.md
[Resume compute]: sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[масштабирования производительности]: sql-data-warehouse-manage-compute-overview.md#scale-compute
[Security overview]: sql-data-warehouse-overview-manage-security.md
[SQL Data Warehouse Best Practices]: sql-data-warehouse-best-practices.md
[SQL Data Warehouse system views]: sql-data-warehouse-reference-tsql-system-views.md

<!--MSDN references-->
[SQL Server Data Tools]: https://msdn.microsoft.com/library/mt204009.aspx

<!--Other web references-->
[Azure portal]: http://portal.azure.com/
