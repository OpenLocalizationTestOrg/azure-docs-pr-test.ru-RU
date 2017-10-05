---
title: "Отслеживание выполняющегося в памяти хранилища XTP | Документация Майкрософт"
description: "Сведения об оценке и мониторинге использования и емкости хранилища XTP в памяти и об устранении нехватки памяти 41823."
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: jodebrui
ms.openlocfilehash: 5afb2209f18b1ba2aa0a916a439509b01afd80da
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-in-memory-oltp-storage"></a><span data-ttu-id="6ed02-103">Мониторинг хранилища OLTP в памяти</span><span class="sxs-lookup"><span data-stu-id="6ed02-103">Monitor In-Memory OLTP Storage</span></span>
<span data-ttu-id="6ed02-104">При использовании [выполняющейся в памяти OLTP](sql-database-in-memory.md) данные в оптимизированных для памяти таблицах и переменные таблиц находятся в выполняющемся в памяти хранилище OLTP.</span><span class="sxs-lookup"><span data-stu-id="6ed02-104">When using [In-Memory OLTP](sql-database-in-memory.md), data in memory-optimized tables and table variables resides in In-Memory OLTP storage.</span></span> <span data-ttu-id="6ed02-105">Каждому уровню служб категории "Премиум" выделяется максимальный объем в выполняющемся в памяти хранилище OLTP. Дополнительные сведения см. в разделе [Уровни служб для отдельной базы данных и уровни производительности](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span><span class="sxs-lookup"><span data-stu-id="6ed02-105">Each Premium service tier has a maximum In-Memory OLTP storage size, which is documented in the [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span></span> <span data-ttu-id="6ed02-106">При превышении этого ограничения операции вставки и обновления могут завершаться сбоем (ошибка 41823).</span><span class="sxs-lookup"><span data-stu-id="6ed02-106">Once this limit is exceeded, insert and update operations may start failing (with error 41823).</span></span> <span data-ttu-id="6ed02-107">В таком случае вам придется либо удалить данные, чтобы освободить память, либо повысить уровень производительности базы данных.</span><span class="sxs-lookup"><span data-stu-id="6ed02-107">At that point you will need to either delete data to reclaim memory, or upgrade the performance tier of your database.</span></span>

## <a name="determine-whether-data-will-fit-within-the-in-memory-storage-cap"></a><span data-ttu-id="6ed02-108">Как определить, соответствует ли объем данных ограничениям хранилища In-Memory</span><span class="sxs-lookup"><span data-stu-id="6ed02-108">Determine whether data will fit within the in-memory storage cap</span></span>
<span data-ttu-id="6ed02-109">Подробные сведения об определении емкости хранилища уровней служб "Премиум" см. в разделе [Уровни служб для отдельной базы данных и уровни производительности](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span><span class="sxs-lookup"><span data-stu-id="6ed02-109">Determine the storage cap: consult the [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) for the storage caps of the different Premium service tiers.</span></span>

<span data-ttu-id="6ed02-110">Оценка требований к памяти для таблицы, оптимизированной для памяти, выполняется одинаково как на сервере SQL Server, так и в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6ed02-110">Estimating memory requirements for a memory-optimized table works the same way for SQL Server as it does in Azure SQL Database.</span></span> <span data-ttu-id="6ed02-111">Потратьте несколько минут, чтобы прочесть эту статью в библиотеке [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span><span class="sxs-lookup"><span data-stu-id="6ed02-111">Take a few minutes to review that topic on [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span></span>

<span data-ttu-id="6ed02-112">Обратите внимание, что, когда определяется максимальный размер данных пользователя, учитываются строки таблиц, табличных переменных и индексы.</span><span class="sxs-lookup"><span data-stu-id="6ed02-112">Note that the table and table variable rows, as well as indexes, count toward the max user data size.</span></span> <span data-ttu-id="6ed02-113">Кроме того, инструкции ALTER TABLE нужно достаточно места для создания новой версии всей таблицы и ее индексов.</span><span class="sxs-lookup"><span data-stu-id="6ed02-113">In addition, ALTER TABLE needs enough room to create a new version of the entire table and its indexes.</span></span>

## <a name="monitoring-and-alerting"></a><span data-ttu-id="6ed02-114">Мониторинг и оповещения</span><span class="sxs-lookup"><span data-stu-id="6ed02-114">Monitoring and alerting</span></span>
<span data-ttu-id="6ed02-115">На [портале](https://portal.azure.com/) Azure вы можете отслеживать использование выполняющегося в памяти хранилища, выраженное в процентах от [емкости хранилища для своего уровня производительности](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span><span class="sxs-lookup"><span data-stu-id="6ed02-115">You can monitor in-memory storage use as a percentage of the [storage cap for your performance tier](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in the Azure [portal](https://portal.azure.com/):</span></span> 

* <span data-ttu-id="6ed02-116">В колонке «База данных» найдите поле «Использование ресурсов» и щелкните «Изменить».</span><span class="sxs-lookup"><span data-stu-id="6ed02-116">On the Database blade, locate the Resource utilization box and click on Edit.</span></span>
* <span data-ttu-id="6ed02-117">Затем выберите метрику `In-Memory OLTP Storage percentage`.</span><span class="sxs-lookup"><span data-stu-id="6ed02-117">Then select the metric `In-Memory OLTP Storage percentage`.</span></span>
* <span data-ttu-id="6ed02-118">Чтобы добавить оповещение, щелкните поле «Использование ресурсов», а затем в открывшейся колонке «Метрики» нажмите кнопку «Добавить оповещение».</span><span class="sxs-lookup"><span data-stu-id="6ed02-118">To add an alert, click on the Resource Utilization box to open the Metric blade, then click on Add alert.</span></span>

<span data-ttu-id="6ed02-119">Или используйте следующий запрос, чтобы отобразить использование хранилища In-Memory:</span><span class="sxs-lookup"><span data-stu-id="6ed02-119">Or use the following query to show the in-memory storage utilization:</span></span>

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a><span data-ttu-id="6ed02-120">Исправление ситуаций с нехваткой памяти (ошибка 41823)</span><span class="sxs-lookup"><span data-stu-id="6ed02-120">Correct out-of-memory situations - Error 41823</span></span>
<span data-ttu-id="6ed02-121">Нехватка памяти приводит к тому, что операции вставки, обновления и создания завершаются сбоем с сообщением об ошибке 41823.</span><span class="sxs-lookup"><span data-stu-id="6ed02-121">Running out-of-memory results in INSERT, UPDATE, and CREATE operations failing with error message 41823.</span></span>

<span data-ttu-id="6ed02-122">Сообщение об ошибке 41823 указывает, что превышен максимальный размер оптимизированных для памяти таблиц и табличных переменных.</span><span class="sxs-lookup"><span data-stu-id="6ed02-122">Error message 41823 indicates that the memory-optimized tables and table variables have exceeded the maximum size.</span></span>

<span data-ttu-id="6ed02-123">Чтобы устранить эту ошибку, выполните одно из следующих действий.</span><span class="sxs-lookup"><span data-stu-id="6ed02-123">To resolve this error, either:</span></span>

* <span data-ttu-id="6ed02-124">Удалите данные из таблиц, оптимизированных для памяти. Это позволит разгрузить данные с помощью традиционных дисковых таблиц.</span><span class="sxs-lookup"><span data-stu-id="6ed02-124">Delete data from the memory-optimized tables, potentially offloading the data to traditional, disk-based tables; or,</span></span>
* <span data-ttu-id="6ed02-125">Если вам необходимо сохранить данные в таблицах, оптимизированных для памяти, повысьте уровень обслуживания, чтобы получить достаточный объем хранилища In-Memory.</span><span class="sxs-lookup"><span data-stu-id="6ed02-125">Upgrade the service tier to one with enough in-memory storage for the data you need to keep in memory-optimized tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ed02-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6ed02-126">Next steps</span></span>
<span data-ttu-id="6ed02-127">Инструкции по мониторингу см. в разделе [Мониторинг базы данных SQL Azure с помощью динамических представлений управления](sql-database-monitoring-with-dmvs.md).</span><span class="sxs-lookup"><span data-stu-id="6ed02-127">For monitoring guidance, see [Monitoring Azure SQL Database using dynamic management views](sql-database-monitoring-with-dmvs.md).</span></span>
