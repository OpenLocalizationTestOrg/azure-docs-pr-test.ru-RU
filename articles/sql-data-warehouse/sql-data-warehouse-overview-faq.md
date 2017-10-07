---
title: "aaaAzure SQL данные хранилища часто задаваемые вопросы | Документы Microsoft"
description: "В этой статье собраны вопросы о хранилище данных SQL Azure, часто задаваемые пользователями и разработчиками."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 812CA525-3BF3-49DF-8DF3-FB4342464F4F
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 3/1/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 09fd3f65d9507b09fcb8f477742c7d020add2755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a><span data-ttu-id="48064-103">Часто задаваемые вопросы о хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="48064-103">SQL Data Warehouse Frequently asked questions</span></span>

## <a name="general"></a><span data-ttu-id="48064-104">Общие сведения</span><span class="sxs-lookup"><span data-stu-id="48064-104">General</span></span>

<span data-ttu-id="48064-105">В.</span><span class="sxs-lookup"><span data-stu-id="48064-105">Q.</span></span> <span data-ttu-id="48064-106">Какие возможности защиты данных предлагаются в хранилище данных SQL?</span><span class="sxs-lookup"><span data-stu-id="48064-106">What does SQL DW offer for data security?</span></span>

<span data-ttu-id="48064-107">О.</span><span class="sxs-lookup"><span data-stu-id="48064-107">A.</span></span> <span data-ttu-id="48064-108">Хранилище данных SQL предлагает несколько решений для защиты данных, таких как прозрачное шифрование данных (TDE) и аудит.</span><span class="sxs-lookup"><span data-stu-id="48064-108">SQL DW offers several solutions for protecting data such as TDE and auditing.</span></span> <span data-ttu-id="48064-109">Дополнительные сведения см. в статье [Безопасность].</span><span class="sxs-lookup"><span data-stu-id="48064-109">For more information, see [Security].</span></span>

<span data-ttu-id="48064-110">В.</span><span class="sxs-lookup"><span data-stu-id="48064-110">Q.</span></span> <span data-ttu-id="48064-111">Где можно выяснить, каким правовым нормам или бизнес-стандартам соответствует хранилище данных SQL?</span><span class="sxs-lookup"><span data-stu-id="48064-111">Where can I find out what legal or business standards is SQL DW compliant with?</span></span>

<span data-ttu-id="48064-112">О.</span><span class="sxs-lookup"><span data-stu-id="48064-112">A.</span></span> <span data-ttu-id="48064-113">Посетите hello [соответствия Microsoft] страницы для различных предложений соответствия по продукту, например SOC и ISO.</span><span class="sxs-lookup"><span data-stu-id="48064-113">Visit hello [Microsoft Compliance] page for various compliance offerings by product such as SOC and ISO.</span></span> <span data-ttu-id="48064-114">Сначала выберите соответствия наименования, а затем разверните Azure hello корпорации Майкрософт в области облачных служб hello правой стороны из раздела toosee страницы приветствия список служб, служб Azure являются совместимыми.</span><span class="sxs-lookup"><span data-stu-id="48064-114">First choose by Compliance title, then expand Azure in hello Microsoft in-scope cloud services section on hello right side of hello page toosee what services are Azure services are compliant.</span></span>

<span data-ttu-id="48064-115">В.</span><span class="sxs-lookup"><span data-stu-id="48064-115">Q.</span></span> <span data-ttu-id="48064-116">Можно ли подключить PowerBI?</span><span class="sxs-lookup"><span data-stu-id="48064-116">Can I connect PowerBI?</span></span>

<span data-ttu-id="48064-117">О.</span><span class="sxs-lookup"><span data-stu-id="48064-117">A.</span></span> <span data-ttu-id="48064-118">Да!</span><span class="sxs-lookup"><span data-stu-id="48064-118">Yes!</span></span> <span data-ttu-id="48064-119">Служба PowerBI поддерживает прямые запросы, выполняемые из хранилища данных SQL, но она не предназначена для большого количества пользователей или данных в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="48064-119">Though PowerBI supports direct query with SQL DW, it’s not intended for large number of users or real-time data.</span></span> <span data-ttu-id="48064-120">В рабочей среде PowerBI рекомендуется использовать службу PowerBI поверх служб Azure Analysis Services или Analysis Service IaaS.</span><span class="sxs-lookup"><span data-stu-id="48064-120">For production use of PowerBI, we recommend using PowerBI on top of Azure Analysis Services or Analysis Service IaaS.</span></span> 

<span data-ttu-id="48064-121">В.</span><span class="sxs-lookup"><span data-stu-id="48064-121">Q.</span></span> <span data-ttu-id="48064-122">Какие ограничения емкости имеет хранилище данных SQL?</span><span class="sxs-lookup"><span data-stu-id="48064-122">What are SQL Data Warehouse Capacity Limits?</span></span>

<span data-ttu-id="48064-123">О.</span><span class="sxs-lookup"><span data-stu-id="48064-123">A.</span></span> <span data-ttu-id="48064-124">Текущие ограничения см. на странице [Ограничения емкости хранилища данных SQL].</span><span class="sxs-lookup"><span data-stu-id="48064-124">See our current [capacity limits] page.</span></span> 

<span data-ttu-id="48064-125">В.</span><span class="sxs-lookup"><span data-stu-id="48064-125">Q.</span></span> <span data-ttu-id="48064-126">Почему операция масштабирования, приостановки или возобновления занимает так много времени?</span><span class="sxs-lookup"><span data-stu-id="48064-126">Why is my Scale/Pause/Resume taking so long?</span></span>

<span data-ttu-id="48064-127">О.</span><span class="sxs-lookup"><span data-stu-id="48064-127">A.</span></span> <span data-ttu-id="48064-128">Ряд факторов может влиять на время hello для вычислительных операций управления.</span><span class="sxs-lookup"><span data-stu-id="48064-128">A variety of factors can influence hello time for compute management operations.</span></span> <span data-ttu-id="48064-129">Как правило, продолжительность операций обусловлена откатом транзакций.</span><span class="sxs-lookup"><span data-stu-id="48064-129">A common case for  long running operations is transactional rollback.</span></span> <span data-ttu-id="48064-130">При инициации операции масштабирования или приостановки блокируются все входящие сеансы, и запросы утрачиваются.</span><span class="sxs-lookup"><span data-stu-id="48064-130">When a scale or pause operation is initiated, all incoming sessions are blocked and queries are drained.</span></span> <span data-ttu-id="48064-131">В системе hello tooleave заказа в стабильном состоянии транзакции должен быть выполнен до может начаться операция.</span><span class="sxs-lookup"><span data-stu-id="48064-131">In order tooleave hello system in a stable state, transactions must be rolled back before an operation can commence.</span></span> <span data-ttu-id="48064-132">Здравствуйте, количество больше hello и больший размер hello журнала транзакций, hello дольше hello операции будут остановлены восстановление hello системы tooa стабильного состояния.</span><span class="sxs-lookup"><span data-stu-id="48064-132">hello greater hello number and larger hello log size of transactions, hello longer hello operation will be stalled restoring hello system tooa stable state.</span></span>

## <a name="user-support"></a><span data-ttu-id="48064-133">Поддержка пользователей</span><span class="sxs-lookup"><span data-stu-id="48064-133">User support</span></span>

<span data-ttu-id="48064-134">В.</span><span class="sxs-lookup"><span data-stu-id="48064-134">Q.</span></span> <span data-ttu-id="48064-135">Куда я могу отправить свой запрос на функцию?</span><span class="sxs-lookup"><span data-stu-id="48064-135">I have a feature request, where do I submit it?</span></span>

<span data-ttu-id="48064-136">О.</span><span class="sxs-lookup"><span data-stu-id="48064-136">A.</span></span> <span data-ttu-id="48064-137">Если у вас есть запрос на функцию, отправьте его на нашей странице [UserVoice].</span><span class="sxs-lookup"><span data-stu-id="48064-137">If you have a feature request, submit it on our [UserVoice] page</span></span>

<span data-ttu-id="48064-138">В.</span><span class="sxs-lookup"><span data-stu-id="48064-138">Q.</span></span> <span data-ttu-id="48064-139">Как я могу разрабатывать свои решения?</span><span class="sxs-lookup"><span data-stu-id="48064-139">How can I do x?</span></span>

<span data-ttu-id="48064-140">О.</span><span class="sxs-lookup"><span data-stu-id="48064-140">A.</span></span> <span data-ttu-id="48064-141">Для получения помощи при разработке с помощью хранилища данных SQL задайте свои вопросы на нашей странице [Stack Overflow].</span><span class="sxs-lookup"><span data-stu-id="48064-141">For help in developing with SQL Data Warehouse, you can ask questions on our [Stack Overflow] page.</span></span> 

<span data-ttu-id="48064-142">В.</span><span class="sxs-lookup"><span data-stu-id="48064-142">Q.</span></span> <span data-ttu-id="48064-143">Как отправить запрос в службу поддержки?</span><span class="sxs-lookup"><span data-stu-id="48064-143">How do I submit a support ticket?</span></span>

<span data-ttu-id="48064-144">О.</span><span class="sxs-lookup"><span data-stu-id="48064-144">A.</span></span> <span data-ttu-id="48064-145">[Запросы в службу поддержки] можно отправить на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="48064-145">[Support Tickets] can be filed through Azure portal.</span></span>

## <a name="sql-languagefeature-support"></a><span data-ttu-id="48064-146">Поддержка языка или функций SQL</span><span class="sxs-lookup"><span data-stu-id="48064-146">SQL language/feature support</span></span> 

<span data-ttu-id="48064-147">В.</span><span class="sxs-lookup"><span data-stu-id="48064-147">Q.</span></span> <span data-ttu-id="48064-148">Какие типы данных поддерживает хранилище данных SQL?</span><span class="sxs-lookup"><span data-stu-id="48064-148">What datatypes does SQL Data Warehouse support?</span></span>

<span data-ttu-id="48064-149">О.</span><span class="sxs-lookup"><span data-stu-id="48064-149">A.</span></span> <span data-ttu-id="48064-150">Типы данных, поддерживаемые хранилищем данных SQL, перечислены [здесь].</span><span class="sxs-lookup"><span data-stu-id="48064-150">See SQL Data Warehouse [data types].</span></span>

<span data-ttu-id="48064-151">В.</span><span class="sxs-lookup"><span data-stu-id="48064-151">Q.</span></span> <span data-ttu-id="48064-152">Какие функции таблиц поддерживаются?</span><span class="sxs-lookup"><span data-stu-id="48064-152">What table features do you support?</span></span>

<span data-ttu-id="48064-153">О.</span><span class="sxs-lookup"><span data-stu-id="48064-153">A.</span></span> <span data-ttu-id="48064-154">Хранилище данных SQL поддерживает множество функций, а те немногие функции, которые не поддерживаются, перечислены в разделе [Неподдерживаемые функции таблиц].</span><span class="sxs-lookup"><span data-stu-id="48064-154">While SQL Data Warehouse supports many features, some are not supported and are documented in [Unsupported Table Features].</span></span>

## <a name="tooling-and-administration"></a><span data-ttu-id="48064-155">Инструментарий и администрирование</span><span class="sxs-lookup"><span data-stu-id="48064-155">Tooling and administration</span></span>

<span data-ttu-id="48064-156">В.</span><span class="sxs-lookup"><span data-stu-id="48064-156">Q.</span></span> <span data-ttu-id="48064-157">Поддерживается ли создание проектов Базы данных в Visual Studio?</span><span class="sxs-lookup"><span data-stu-id="48064-157">Do you support Database projects in Visual Studio.</span></span>

<span data-ttu-id="48064-158">О.</span><span class="sxs-lookup"><span data-stu-id="48064-158">A.</span></span> <span data-ttu-id="48064-159">В настоящее время создание в Visual Studio проектов Базы данных для хранилища данных SQL не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="48064-159">We currently do not support Database projects in Visual Studio for SQL Data Warehouse.</span></span> <span data-ttu-id="48064-160">Если вы хотите toocast tooget голос эту возможность, посетите наш User Voice [проекты базы данных компонентов запроса].</span><span class="sxs-lookup"><span data-stu-id="48064-160">If you'd like toocast a vote tooget this feature, visit our User Voice [Database projects feature request].</span></span>

<span data-ttu-id="48064-161">В.</span><span class="sxs-lookup"><span data-stu-id="48064-161">Q.</span></span> <span data-ttu-id="48064-162">Поддерживает ли хранилище данных SQL интерфейсы REST API?</span><span class="sxs-lookup"><span data-stu-id="48064-162">Does SQL Data Warehouse support REST APIs?</span></span>

<span data-ttu-id="48064-163">О.</span><span class="sxs-lookup"><span data-stu-id="48064-163">A.</span></span> <span data-ttu-id="48064-164">Да.</span><span class="sxs-lookup"><span data-stu-id="48064-164">Yes.</span></span> <span data-ttu-id="48064-165">Большинство функции REST, которые могут использоваться в Базе данных SQL, также доступны в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="48064-165">Most REST functionality that can be used with SQL Database is also available with SQL Data Warehouse.</span></span> <span data-ttu-id="48064-166">Сведения об API можно найти в документации REST или на сайте [MSDN].</span><span class="sxs-lookup"><span data-stu-id="48064-166">You can find API information within REST documentation pages or [MSDN].</span></span>


## <a name="loading"></a><span data-ttu-id="48064-167">Загрузка</span><span class="sxs-lookup"><span data-stu-id="48064-167">Loading</span></span>

<span data-ttu-id="48064-168">В.</span><span class="sxs-lookup"><span data-stu-id="48064-168">Q.</span></span> <span data-ttu-id="48064-169">Какие драйверы клиента поддерживаются?</span><span class="sxs-lookup"><span data-stu-id="48064-169">What client drivers do you support?</span></span>

<span data-ttu-id="48064-170">О.</span><span class="sxs-lookup"><span data-stu-id="48064-170">A.</span></span> <span data-ttu-id="48064-171">Поддержка драйверов для хранилища данных можно найти на hello [строки подключения] страницы</span><span class="sxs-lookup"><span data-stu-id="48064-171">Driver support for DW can be found on hello [Connection Strings] page</span></span>

<span data-ttu-id="48064-172">В. Какие форматы файлов поддерживает PolyBase при работе с хранилищем данных SQL?</span><span class="sxs-lookup"><span data-stu-id="48064-172">Q: What file formats are supported by PolyBase with SQL Data Warehouse?</span></span>

<span data-ttu-id="48064-173">О. Orc, RC, Parquet и неструктурированный текст с разделителями.</span><span class="sxs-lookup"><span data-stu-id="48064-173">A: Orc, RC, Parquet, and flat delimited text</span></span>

<span data-ttu-id="48064-174">Вопрос. что можно подключиться с помощью PolyBase хранилища данных SQL toofrom?</span><span class="sxs-lookup"><span data-stu-id="48064-174">Q: What can I connect toofrom SQL DW using PolyBase?</span></span> 

<span data-ttu-id="48064-175">О. К [Azure Data Lake Store] и [большим двоичным объектам службы хранилища Azure].</span><span class="sxs-lookup"><span data-stu-id="48064-175">A: [Azure Data Lake Store] and [Azure Storage Blobs]</span></span>

<span data-ttu-id="48064-176">Вопрос. есть вычисление pushdown возможно при подключении tooAzure хранилища больших двоичных объектов или ADLS?</span><span class="sxs-lookup"><span data-stu-id="48064-176">Q: Is computation pushdown possible  when connecting tooAzure Storage Blobs or ADLS?</span></span> 

<span data-ttu-id="48064-177">Ответ PolyBase хранилища данных SQL, нет, взаимодействует только компоненты хранения hello.</span><span class="sxs-lookup"><span data-stu-id="48064-177">A: No, SQL DW PolyBase only interacts hello storage components.</span></span> 

<span data-ttu-id="48064-178">Вопрос. можно ли подключиться tooHDI?</span><span class="sxs-lookup"><span data-stu-id="48064-178">Q: Can I connect tooHDI?</span></span>

<span data-ttu-id="48064-179">Ответ HDI можно использовать ADLS или WASB как слой HDFS hello.</span><span class="sxs-lookup"><span data-stu-id="48064-179">A: HDI can use either ADLS or WASB as hello HDFS layer.</span></span> <span data-ttu-id="48064-180">Если одна из этих служб используется в качестве уровня HDFS, то можно загрузить данные в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="48064-180">If you have either as your HDFS layer, then you can load that data into SQL DW.</span></span> <span data-ttu-id="48064-181">Тем не менее не удается создать экземпляр HDI toohello вычисление pushdown.</span><span class="sxs-lookup"><span data-stu-id="48064-181">However, you cannot generate pushdown computation toohello HDI instance.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="48064-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="48064-182">Next steps</span></span>
<span data-ttu-id="48064-183">Дополнительные сведения о хранилище данных SQL в целом см. на [этой странице].</span><span class="sxs-lookup"><span data-stu-id="48064-183">For more information on SQL Data Warehouse as a whole, see our [Overview] page.</span></span>


<!-- Article references -->
[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[строки подключения]: ./sql-data-warehouse-connection-strings.md
[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Запросы в службу поддержки]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Безопасность]: ./sql-data-warehouse-overview-manage-security.md
[соответствия Microsoft]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings
[Ограничения емкости хранилища данных SQL]: ./sql-data-warehouse-service-capacity-limits.md
[здесь]: ./sql-data-warehouse-tables-data-types.md
[Неподдерживаемые функции таблиц]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md
[большим двоичным объектам службы хранилища Azure]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[проекты базы данных компонентов запроса]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu
[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx
[этой странице]: ./sql-data-warehouse-overview-faq.md