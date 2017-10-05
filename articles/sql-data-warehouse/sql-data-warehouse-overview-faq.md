---
title: "Часто задаваемые вопросы о хранилище данных SQL Azure | Документация Майкрософт"
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
ms.openlocfilehash: 4c00710ecc0c91f8407eca81b78176075fcbd6ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a><span data-ttu-id="9798a-103">Часто задаваемые вопросы о хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="9798a-103">SQL Data Warehouse Frequently asked questions</span></span>

## <a name="general"></a><span data-ttu-id="9798a-104">Общие сведения</span><span class="sxs-lookup"><span data-stu-id="9798a-104">General</span></span>

<span data-ttu-id="9798a-105">В.</span><span class="sxs-lookup"><span data-stu-id="9798a-105">Q.</span></span> <span data-ttu-id="9798a-106">Какие возможности защиты данных предлагаются в хранилище данных SQL?</span><span class="sxs-lookup"><span data-stu-id="9798a-106">What does SQL DW offer for data security?</span></span>

<span data-ttu-id="9798a-107">О.</span><span class="sxs-lookup"><span data-stu-id="9798a-107">A.</span></span> <span data-ttu-id="9798a-108">Хранилище данных SQL предлагает несколько решений для защиты данных, таких как прозрачное шифрование данных (TDE) и аудит.</span><span class="sxs-lookup"><span data-stu-id="9798a-108">SQL DW offers several solutions for protecting data such as TDE and auditing.</span></span> <span data-ttu-id="9798a-109">Дополнительные сведения см. в статье [Безопасность].</span><span class="sxs-lookup"><span data-stu-id="9798a-109">For more information, see [Security].</span></span>

<span data-ttu-id="9798a-110">В.</span><span class="sxs-lookup"><span data-stu-id="9798a-110">Q.</span></span> <span data-ttu-id="9798a-111">Где можно выяснить, каким правовым нормам или бизнес-стандартам соответствует хранилище данных SQL?</span><span class="sxs-lookup"><span data-stu-id="9798a-111">Where can I find out what legal or business standards is SQL DW compliant with?</span></span>

<span data-ttu-id="9798a-112">О.</span><span class="sxs-lookup"><span data-stu-id="9798a-112">A.</span></span> <span data-ttu-id="9798a-113">На странице [соответствия требованиям корпорации Майкрософт] доступны различные сертификаты соответствия (такие как SOC и ISO), которые можно отфильтровать по продукту.</span><span class="sxs-lookup"><span data-stu-id="9798a-113">Visit the [Microsoft Compliance] page for various compliance offerings by product such as SOC and ISO.</span></span> <span data-ttu-id="9798a-114">Сначала выберите сертификат соответствия, а затем в правой части страницы в разделе "Microsoft in-scope cloud services" (Охваченные облачные службы корпорации Майкрософт) разверните "Azure", чтобы просмотреть службы Azure, которые соответствуют выбранным требованиям.</span><span class="sxs-lookup"><span data-stu-id="9798a-114">First choose by Compliance title, then expand Azure in the Microsoft in-scope cloud services section on the right side of the page to see what services are Azure services are compliant.</span></span>

<span data-ttu-id="9798a-115">В.</span><span class="sxs-lookup"><span data-stu-id="9798a-115">Q.</span></span> <span data-ttu-id="9798a-116">Можно ли подключить PowerBI?</span><span class="sxs-lookup"><span data-stu-id="9798a-116">Can I connect PowerBI?</span></span>

<span data-ttu-id="9798a-117">О.</span><span class="sxs-lookup"><span data-stu-id="9798a-117">A.</span></span> <span data-ttu-id="9798a-118">Да!</span><span class="sxs-lookup"><span data-stu-id="9798a-118">Yes!</span></span> <span data-ttu-id="9798a-119">Служба PowerBI поддерживает прямые запросы, выполняемые из хранилища данных SQL, но она не предназначена для большого количества пользователей или данных в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="9798a-119">Though PowerBI supports direct query with SQL DW, it’s not intended for large number of users or real-time data.</span></span> <span data-ttu-id="9798a-120">В рабочей среде PowerBI рекомендуется использовать службу PowerBI поверх служб Azure Analysis Services или Analysis Service IaaS.</span><span class="sxs-lookup"><span data-stu-id="9798a-120">For production use of PowerBI, we recommend using PowerBI on top of Azure Analysis Services or Analysis Service IaaS.</span></span> 

<span data-ttu-id="9798a-121">В.</span><span class="sxs-lookup"><span data-stu-id="9798a-121">Q.</span></span> <span data-ttu-id="9798a-122">Какие ограничения емкости имеет хранилище данных SQL?</span><span class="sxs-lookup"><span data-stu-id="9798a-122">What are SQL Data Warehouse Capacity Limits?</span></span>

<span data-ttu-id="9798a-123">О.</span><span class="sxs-lookup"><span data-stu-id="9798a-123">A.</span></span> <span data-ttu-id="9798a-124">Текущие ограничения см. на странице [Ограничения емкости хранилища данных SQL].</span><span class="sxs-lookup"><span data-stu-id="9798a-124">See our current [capacity limits] page.</span></span> 

<span data-ttu-id="9798a-125">В.</span><span class="sxs-lookup"><span data-stu-id="9798a-125">Q.</span></span> <span data-ttu-id="9798a-126">Почему операция масштабирования, приостановки или возобновления занимает так много времени?</span><span class="sxs-lookup"><span data-stu-id="9798a-126">Why is my Scale/Pause/Resume taking so long?</span></span>

<span data-ttu-id="9798a-127">О.</span><span class="sxs-lookup"><span data-stu-id="9798a-127">A.</span></span> <span data-ttu-id="9798a-128">На длительность операций управления вычислениями может влиять ряд факторов.</span><span class="sxs-lookup"><span data-stu-id="9798a-128">A variety of factors can influence the time for compute management operations.</span></span> <span data-ttu-id="9798a-129">Как правило, продолжительность операций обусловлена откатом транзакций.</span><span class="sxs-lookup"><span data-stu-id="9798a-129">A common case for  long running operations is transactional rollback.</span></span> <span data-ttu-id="9798a-130">При инициации операции масштабирования или приостановки блокируются все входящие сеансы, и запросы утрачиваются.</span><span class="sxs-lookup"><span data-stu-id="9798a-130">When a scale or pause operation is initiated, all incoming sessions are blocked and queries are drained.</span></span> <span data-ttu-id="9798a-131">Чтобы оставить систему в стабильном состоянии, перед началом операции необходимо выполнить откат транзакций.</span><span class="sxs-lookup"><span data-stu-id="9798a-131">In order to leave the system in a stable state, transactions must be rolled back before an operation can commence.</span></span> <span data-ttu-id="9798a-132">Чем больше число транзакций и размер их журналов, тем дольше будет задержка операции при восстановлении стабильного состояния системы.</span><span class="sxs-lookup"><span data-stu-id="9798a-132">The greater the number and larger the log size of transactions, the longer the operation will be stalled restoring the system to a stable state.</span></span>

## <a name="user-support"></a><span data-ttu-id="9798a-133">Поддержка пользователей</span><span class="sxs-lookup"><span data-stu-id="9798a-133">User support</span></span>

<span data-ttu-id="9798a-134">В.</span><span class="sxs-lookup"><span data-stu-id="9798a-134">Q.</span></span> <span data-ttu-id="9798a-135">Куда я могу отправить свой запрос на функцию?</span><span class="sxs-lookup"><span data-stu-id="9798a-135">I have a feature request, where do I submit it?</span></span>

<span data-ttu-id="9798a-136">О.</span><span class="sxs-lookup"><span data-stu-id="9798a-136">A.</span></span> <span data-ttu-id="9798a-137">Если у вас есть запрос на функцию, отправьте его на нашей странице [UserVoice].</span><span class="sxs-lookup"><span data-stu-id="9798a-137">If you have a feature request, submit it on our [UserVoice] page</span></span>

<span data-ttu-id="9798a-138">В.</span><span class="sxs-lookup"><span data-stu-id="9798a-138">Q.</span></span> <span data-ttu-id="9798a-139">Как я могу разрабатывать свои решения?</span><span class="sxs-lookup"><span data-stu-id="9798a-139">How can I do x?</span></span>

<span data-ttu-id="9798a-140">О.</span><span class="sxs-lookup"><span data-stu-id="9798a-140">A.</span></span> <span data-ttu-id="9798a-141">Для получения помощи при разработке с помощью хранилища данных SQL задайте свои вопросы на нашей странице [Stack Overflow].</span><span class="sxs-lookup"><span data-stu-id="9798a-141">For help in developing with SQL Data Warehouse, you can ask questions on our [Stack Overflow] page.</span></span> 

<span data-ttu-id="9798a-142">В.</span><span class="sxs-lookup"><span data-stu-id="9798a-142">Q.</span></span> <span data-ttu-id="9798a-143">Как отправить запрос в службу поддержки?</span><span class="sxs-lookup"><span data-stu-id="9798a-143">How do I submit a support ticket?</span></span>

<span data-ttu-id="9798a-144">О.</span><span class="sxs-lookup"><span data-stu-id="9798a-144">A.</span></span> <span data-ttu-id="9798a-145">[Запросы в службу поддержки] можно отправить на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="9798a-145">[Support Tickets] can be filed through Azure portal.</span></span>

## <a name="sql-languagefeature-support"></a><span data-ttu-id="9798a-146">Поддержка языка или функций SQL</span><span class="sxs-lookup"><span data-stu-id="9798a-146">SQL language/feature support</span></span> 

<span data-ttu-id="9798a-147">В.</span><span class="sxs-lookup"><span data-stu-id="9798a-147">Q.</span></span> <span data-ttu-id="9798a-148">Какие типы данных поддерживает хранилище данных SQL?</span><span class="sxs-lookup"><span data-stu-id="9798a-148">What datatypes does SQL Data Warehouse support?</span></span>

<span data-ttu-id="9798a-149">О.</span><span class="sxs-lookup"><span data-stu-id="9798a-149">A.</span></span> <span data-ttu-id="9798a-150">Типы данных, поддерживаемые хранилищем данных SQL, перечислены [здесь].</span><span class="sxs-lookup"><span data-stu-id="9798a-150">See SQL Data Warehouse [data types].</span></span>

<span data-ttu-id="9798a-151">В.</span><span class="sxs-lookup"><span data-stu-id="9798a-151">Q.</span></span> <span data-ttu-id="9798a-152">Какие функции таблиц поддерживаются?</span><span class="sxs-lookup"><span data-stu-id="9798a-152">What table features do you support?</span></span>

<span data-ttu-id="9798a-153">О.</span><span class="sxs-lookup"><span data-stu-id="9798a-153">A.</span></span> <span data-ttu-id="9798a-154">Хранилище данных SQL поддерживает множество функций, а те немногие функции, которые не поддерживаются, перечислены в разделе [Неподдерживаемые функции таблиц].</span><span class="sxs-lookup"><span data-stu-id="9798a-154">While SQL Data Warehouse supports many features, some are not supported and are documented in [Unsupported Table Features].</span></span>

## <a name="tooling-and-administration"></a><span data-ttu-id="9798a-155">Инструментарий и администрирование</span><span class="sxs-lookup"><span data-stu-id="9798a-155">Tooling and administration</span></span>

<span data-ttu-id="9798a-156">В.</span><span class="sxs-lookup"><span data-stu-id="9798a-156">Q.</span></span> <span data-ttu-id="9798a-157">Поддерживается ли создание проектов Базы данных в Visual Studio?</span><span class="sxs-lookup"><span data-stu-id="9798a-157">Do you support Database projects in Visual Studio.</span></span>

<span data-ttu-id="9798a-158">О.</span><span class="sxs-lookup"><span data-stu-id="9798a-158">A.</span></span> <span data-ttu-id="9798a-159">В настоящее время создание в Visual Studio проектов Базы данных для хранилища данных SQL не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="9798a-159">We currently do not support Database projects in Visual Studio for SQL Data Warehouse.</span></span> <span data-ttu-id="9798a-160">Если вы хотите проголосовать за то, чтобы поддержка проектов Базы данных была добавлена, то посетите нашу страницу UserVoice и [отправьте запрос на эту функцию].</span><span class="sxs-lookup"><span data-stu-id="9798a-160">If you'd like to cast a vote to get this feature, visit our User Voice [Database projects feature request].</span></span>

<span data-ttu-id="9798a-161">В.</span><span class="sxs-lookup"><span data-stu-id="9798a-161">Q.</span></span> <span data-ttu-id="9798a-162">Поддерживает ли хранилище данных SQL интерфейсы REST API?</span><span class="sxs-lookup"><span data-stu-id="9798a-162">Does SQL Data Warehouse support REST APIs?</span></span>

<span data-ttu-id="9798a-163">О.</span><span class="sxs-lookup"><span data-stu-id="9798a-163">A.</span></span> <span data-ttu-id="9798a-164">Да.</span><span class="sxs-lookup"><span data-stu-id="9798a-164">Yes.</span></span> <span data-ttu-id="9798a-165">Большинство функции REST, которые могут использоваться в Базе данных SQL, также доступны в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="9798a-165">Most REST functionality that can be used with SQL Database is also available with SQL Data Warehouse.</span></span> <span data-ttu-id="9798a-166">Сведения об API можно найти в документации REST или на сайте [MSDN].</span><span class="sxs-lookup"><span data-stu-id="9798a-166">You can find API information within REST documentation pages or [MSDN].</span></span>


## <a name="loading"></a><span data-ttu-id="9798a-167">Загрузка</span><span class="sxs-lookup"><span data-stu-id="9798a-167">Loading</span></span>

<span data-ttu-id="9798a-168">В.</span><span class="sxs-lookup"><span data-stu-id="9798a-168">Q.</span></span> <span data-ttu-id="9798a-169">Какие драйверы клиента поддерживаются?</span><span class="sxs-lookup"><span data-stu-id="9798a-169">What client drivers do you support?</span></span>

<span data-ttu-id="9798a-170">О.</span><span class="sxs-lookup"><span data-stu-id="9798a-170">A.</span></span> <span data-ttu-id="9798a-171">Сведения о поддержке драйверов для хранилища данных можно найти в статье [Драйверы для хранилища данных SQL Azure].</span><span class="sxs-lookup"><span data-stu-id="9798a-171">Driver support for DW can be found on the [Connection Strings] page</span></span>

<span data-ttu-id="9798a-172">В. Какие форматы файлов поддерживает PolyBase при работе с хранилищем данных SQL?</span><span class="sxs-lookup"><span data-stu-id="9798a-172">Q: What file formats are supported by PolyBase with SQL Data Warehouse?</span></span>

<span data-ttu-id="9798a-173">О. Orc, RC, Parquet и неструктурированный текст с разделителями.</span><span class="sxs-lookup"><span data-stu-id="9798a-173">A: Orc, RC, Parquet, and flat delimited text</span></span>

<span data-ttu-id="9798a-174">В. К чему можно подключиться из хранилища данных SQL, используя PolyBase?</span><span class="sxs-lookup"><span data-stu-id="9798a-174">Q: What can I connect to from SQL DW using PolyBase?</span></span> 

<span data-ttu-id="9798a-175">О. К [Azure Data Lake Store] и [большим двоичным объектам службы хранилища Azure].</span><span class="sxs-lookup"><span data-stu-id="9798a-175">A: [Azure Data Lake Store] and [Azure Storage Blobs]</span></span>

<span data-ttu-id="9798a-176">В. Возможно ли вычисление со стековой памятью при подключении к большим двоичным объектам службы хранилища Azure или Azure Data Lake Store?</span><span class="sxs-lookup"><span data-stu-id="9798a-176">Q: Is computation pushdown possible  when connecting to Azure Storage Blobs or ADLS?</span></span> 

<span data-ttu-id="9798a-177">О. Нет, PolyBase в хранилище данных SQL взаимодействует только с компонентами хранилища.</span><span class="sxs-lookup"><span data-stu-id="9798a-177">A: No, SQL DW PolyBase only interacts the storage components.</span></span> 

<span data-ttu-id="9798a-178">В. Можно ли подключиться к HDI?</span><span class="sxs-lookup"><span data-stu-id="9798a-178">Q: Can I connect to HDI?</span></span>

<span data-ttu-id="9798a-179">О. HDI может использовать Azure Data Lake Store или WASB в качестве уровня HDFS.</span><span class="sxs-lookup"><span data-stu-id="9798a-179">A: HDI can use either ADLS or WASB as the HDFS layer.</span></span> <span data-ttu-id="9798a-180">Если одна из этих служб используется в качестве уровня HDFS, то можно загрузить данные в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="9798a-180">If you have either as your HDFS layer, then you can load that data into SQL DW.</span></span> <span data-ttu-id="9798a-181">Тем не менее, создание вычислений со стековой памятью для экземпляра HDI невозможно.</span><span class="sxs-lookup"><span data-stu-id="9798a-181">However, you cannot generate pushdown computation to the HDI instance.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9798a-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9798a-182">Next steps</span></span>
<span data-ttu-id="9798a-183">Дополнительные сведения о хранилище данных SQL в целом см. на [этой странице].</span><span class="sxs-lookup"><span data-stu-id="9798a-183">For more information on SQL Data Warehouse as a whole, see our [Overview] page.</span></span>


<!-- Article references -->
<span data-ttu-id="9798a-184">[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse</span><span class="sxs-lookup"><span data-stu-id="9798a-184">[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse</span></span>
<span data-ttu-id="9798a-185">[Драйверы для хранилища данных SQL Azure]: ./sql-data-warehouse-connection-strings.md</span><span class="sxs-lookup"><span data-stu-id="9798a-185">[Connection Strings]: ./sql-data-warehouse-connection-strings.md</span></span>
<span data-ttu-id="9798a-186">[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw</span><span class="sxs-lookup"><span data-stu-id="9798a-186">[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw</span></span>
<span data-ttu-id="9798a-187">[Запросы в службу поддержки]: ./sql-data-warehouse-get-started-create-support-ticket.md</span><span class="sxs-lookup"><span data-stu-id="9798a-187">[Support Tickets]: ./sql-data-warehouse-get-started-create-support-ticket.md</span></span>
<span data-ttu-id="9798a-188">[Безопасность]: ./sql-data-warehouse-overview-manage-security.md</span><span class="sxs-lookup"><span data-stu-id="9798a-188">[Security]: ./sql-data-warehouse-overview-manage-security.md</span></span>
<span data-ttu-id="9798a-189">[соответствия требованиям корпорации Майкрософт]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings</span><span class="sxs-lookup"><span data-stu-id="9798a-189">[Microsoft Compliance]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings</span></span>
<span data-ttu-id="9798a-190">[Ограничения емкости хранилища данных SQL]: ./sql-data-warehouse-service-capacity-limits.md</span><span class="sxs-lookup"><span data-stu-id="9798a-190">[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md</span></span>
<span data-ttu-id="9798a-191">[здесь]: ./sql-data-warehouse-tables-data-types.md</span><span class="sxs-lookup"><span data-stu-id="9798a-191">[data types]: ./sql-data-warehouse-tables-data-types.md</span></span>
<span data-ttu-id="9798a-192">[Неподдерживаемые функции таблиц]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features</span><span class="sxs-lookup"><span data-stu-id="9798a-192">[Unsupported Table Features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features</span></span>
<span data-ttu-id="9798a-193">[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md</span><span class="sxs-lookup"><span data-stu-id="9798a-193">[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md</span></span>
<span data-ttu-id="9798a-194">[большим двоичным объектам службы хранилища Azure]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md</span><span class="sxs-lookup"><span data-stu-id="9798a-194">[Azure Storage Blobs]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md</span></span>
<span data-ttu-id="9798a-195">[отправьте запрос на эту функцию]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu</span><span class="sxs-lookup"><span data-stu-id="9798a-195">[Database projects feature request]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu</span></span>
<span data-ttu-id="9798a-196">[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx</span><span class="sxs-lookup"><span data-stu-id="9798a-196">[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx</span></span>
<span data-ttu-id="9798a-197">[этой странице]: ./sql-data-warehouse-overview-faq.md</span><span class="sxs-lookup"><span data-stu-id="9798a-197">[Overview]: ./sql-data-warehouse-overview-faq.md</span></span>