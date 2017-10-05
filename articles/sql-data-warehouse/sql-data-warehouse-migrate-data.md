---
title: "Перенос данных в хранилище данных SQL | Документация Майкрософт"
description: "Советы по переносу данных в хранилище данных SQL Azure для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: d78f954a-f54c-4aa4-9040-919bc6414887
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/29/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: dbdf1696cd169aa7e5e23f116027a1170347f4ea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="migrate-your-data"></a><span data-ttu-id="1af29-103">Перенос данных</span><span class="sxs-lookup"><span data-stu-id="1af29-103">Migrate Your Data</span></span>
<span data-ttu-id="1af29-104">Данные из различных источников можно переместить в хранилище данных SQL с помощью различных инструментов.</span><span class="sxs-lookup"><span data-stu-id="1af29-104">Data can be moved from different sources into your SQL Data Warehouse with a variety tools.</span></span>  <span data-ttu-id="1af29-105">Для достижения этой цели можно использовать ADF Copy, службы SSIS и bcp.</span><span class="sxs-lookup"><span data-stu-id="1af29-105">ADF Copy, SSIS, and bcp can all be used to achieve this goal.</span></span> <span data-ttu-id="1af29-106">Тем не менее по мере увеличения объема данных есть смысл подумать о разделении процесса переноса на несколько этапов.</span><span class="sxs-lookup"><span data-stu-id="1af29-106">However, as the amount of data increases you should think about breaking down the data migration process into steps.</span></span> <span data-ttu-id="1af29-107">Это позволит оптимизировать каждый этап как в плане производительности, так и в плане гибкости, обеспечивая плавный перенос данных.</span><span class="sxs-lookup"><span data-stu-id="1af29-107">This affords you the opportunity to optimize each step both for performance and for resilience to ensure a smooth data migration.</span></span>

<span data-ttu-id="1af29-108">В этой статье сначала будут рассмотрены простые сценарии переноса данных с помощью ADF Copy, служб SSIS и bcp.</span><span class="sxs-lookup"><span data-stu-id="1af29-108">This article first discusses the simple migration scenarios of ADF Copy, SSIS, and bcp.</span></span> <span data-ttu-id="1af29-109">Затем мы поговорим об аспектах оптимизации переноса данных.</span><span class="sxs-lookup"><span data-stu-id="1af29-109">It then look a little deeper into how the migration can be optimized.</span></span>

## <a name="azure-data-factory-adf-copy"></a><span data-ttu-id="1af29-110">Копирование с помощью фабрики данных Azure (ADF)</span><span class="sxs-lookup"><span data-stu-id="1af29-110">Azure Data Factory (ADF) copy</span></span>
<span data-ttu-id="1af29-111">[ADF Copy][ADF Copy] входит в [фабрику данных Azure][Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="1af29-111">[ADF Copy][ADF Copy] is part of [Azure Data Factory][Azure Data Factory].</span></span> <span data-ttu-id="1af29-112">ADF Copy позволяет перенести данные в неструктурированные файлы на локальном диске, в удаленные неструктурированные файлы в хранилище больших двоичных объектов Azure или напрямую в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="1af29-112">You can use ADF Copy to export your data to flat files residing on local storage, to remote flat files held in Azure blob storage or directly into SQL Data Warehouse.</span></span>

<span data-ttu-id="1af29-113">Если данные хранятся в неструктурированных файлах, то сначала их нужно перенести в большой двоичный объект службы хранилища Azure, а затем загрузить в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="1af29-113">If your data starts in flat files, then you will first need to transfer it to Azure storage blob before initiating a load it into SQL Data Warehouse.</span></span> <span data-ttu-id="1af29-114">После переноса данных в хранилище больших двоичных объектов Azure можно еще раз воспользоваться [ADF Copy][ADF Copy], чтобы перенести данные в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="1af29-114">Once the data is transferred into Azure blob storage you can choose to use [ADF Copy][ADF Copy] again to push the data into SQL Data Warehouse.</span></span>

<span data-ttu-id="1af29-115">PolyBase также обеспечивает возможность высокопроизводительной загрузки данных.</span><span class="sxs-lookup"><span data-stu-id="1af29-115">PolyBase also provides a high-performance option for loading the data.</span></span> <span data-ttu-id="1af29-116">Однако в этом случае придется использовать два средства вместо одного.</span><span class="sxs-lookup"><span data-stu-id="1af29-116">However, that does mean using two tools instead of one.</span></span> <span data-ttu-id="1af29-117">Если требуется более высокая степень производительности, воспользуйтесь PolyBase.</span><span class="sxs-lookup"><span data-stu-id="1af29-117">If you need the best performance then use PolyBase.</span></span> <span data-ttu-id="1af29-118">Если необходимо использовать одно средство (и объем данных небольшой), ADF вполне подойдет.</span><span class="sxs-lookup"><span data-stu-id="1af29-118">If you want a single tool experience (and the data is not massive) then ADF is your answer.</span></span>


> 
> 

<span data-ttu-id="1af29-119">[Примеры использования ADF][ADF samples] см. в следующей статье.</span><span class="sxs-lookup"><span data-stu-id="1af29-119">Head over to the following article for some great [ADF samples][ADF samples].</span></span>

## <a name="integration-services"></a><span data-ttu-id="1af29-120">Службы интеграции</span><span class="sxs-lookup"><span data-stu-id="1af29-120">Integration Services</span></span>
<span data-ttu-id="1af29-121">Службы Integration Services (SSIS) — это мощное и гибкое средство загрузки данных, которое поддерживает сложные рабочие потоки, преобразование данных и разные параметры загрузки.</span><span class="sxs-lookup"><span data-stu-id="1af29-121">Integration Services (SSIS) is a powerful and flexible Extract Transform and Load (ETL) tool that supports complex workflows, data transformation, and several data loading options.</span></span> <span data-ttu-id="1af29-122">Службы SSIS позволяют упростить перенос данных в Azure; службы также можно использовать как часть более сложного переноса данных.</span><span class="sxs-lookup"><span data-stu-id="1af29-122">Use SSIS to simply transfer data to Azure or as part of a broader migration.</span></span>

> [!NOTE]
> <span data-ttu-id="1af29-123">Службы SSIS могут экспортировать данные в UTF-8 без маркера последовательности байтов в файле.</span><span class="sxs-lookup"><span data-stu-id="1af29-123">SSIS can export to UTF-8 without the byte order mark in the file.</span></span> <span data-ttu-id="1af29-124">Чтобы настроить это, сначала нужно преобразовать символьные данные в поток данных с помощью компонента производного столбца и подготовить их для использования кодовой страницы 65001 UTF-8.</span><span class="sxs-lookup"><span data-stu-id="1af29-124">To configure this you must first use the derived column component to convert the character data in the data flow to use the 65001 UTF-8 code page.</span></span> <span data-ttu-id="1af29-125">После преобразования столбцов запишите данные в целевой адаптер неструктурированного файла, выбрав 65001 в качестве кодовой страницы для файла.</span><span class="sxs-lookup"><span data-stu-id="1af29-125">Once the columns have been converted, write the data to the flat file destination adapter ensuring that 65001 has also been selected as the code page for the file.</span></span>
> 
> 

<span data-ttu-id="1af29-126">Службы SSIS подключаются к хранилищу данных SQL так же, как и к SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1af29-126">SSIS connects to SQL Data Warehouse just as it would connect to a SQL Server deployment.</span></span> <span data-ttu-id="1af29-127">Однако для подключения потребуется диспетчер соединений ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="1af29-127">However, your connections will need to be using an ADO.NET connection manager.</span></span> <span data-ttu-id="1af29-128">Также нужно не забыть настроить параметр "Использовать массовую вставку, когда она доступна", чтобы довести пропускную способность до максимума.</span><span class="sxs-lookup"><span data-stu-id="1af29-128">You should also take care to configure the "Use bulk insert when available" setting to maximize throughput.</span></span> <span data-ttu-id="1af29-129">Дополнительные сведения об этом свойстве см. в статье об [адаптере загрузки данных ADO.NET][ADO.NET destination adapter].</span><span class="sxs-lookup"><span data-stu-id="1af29-129">Please refer to the [ADO.NET destination adapter][ADO.NET destination adapter] article to learn more about this property</span></span>

> [!NOTE]
> <span data-ttu-id="1af29-130">Подключение к хранилищу данных SQL Azure с помощью OLE DB не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="1af29-130">Connecting to Azure SQL Data Warehouse by using OLEDB is not supported.</span></span>
> 
> 

<span data-ttu-id="1af29-131">Кроме того, всегда существует возможность того, что пакет будет поврежден из-за регулирования или проблем с сетью.</span><span class="sxs-lookup"><span data-stu-id="1af29-131">In addition, there is always the possibility that a package might fail due to throttling or network issues.</span></span> <span data-ttu-id="1af29-132">Создавайте пакеты таким образом, чтобы можно было возобновить работу с точки сбоя без необходимости повторять уже выполненную работу.</span><span class="sxs-lookup"><span data-stu-id="1af29-132">Design packages so they can be resumed at the point of failure, without redoing work that completed before the failure.</span></span>

<span data-ttu-id="1af29-133">Дополнительные сведения см. в [документации по службам SSIS][SSIS documentation].</span><span class="sxs-lookup"><span data-stu-id="1af29-133">For more information consult the [SSIS documentation][SSIS documentation].</span></span>

## <a name="bcp"></a><span data-ttu-id="1af29-134">bcp</span><span class="sxs-lookup"><span data-stu-id="1af29-134">bcp</span></span>
<span data-ttu-id="1af29-135">Программа bcp — средство командной строки, предназначенное для импорта и экспорта данных неструктурированных файлов.</span><span class="sxs-lookup"><span data-stu-id="1af29-135">bcp is a command-line utility that is designed for flat file data import and export.</span></span> <span data-ttu-id="1af29-136">Во время экспорта можно выполнять преобразование.</span><span class="sxs-lookup"><span data-stu-id="1af29-136">Some transformation can take place during data export.</span></span> <span data-ttu-id="1af29-137">Для выполнения простого преобразования воспользуйтесь запросом, который выбирает и преобразует данные.</span><span class="sxs-lookup"><span data-stu-id="1af29-137">To perform simple transformations use a query to select and transform the data.</span></span> <span data-ttu-id="1af29-138">После выполнения экспорта неструктурированные файлы можно загрузить напрямую в целевую базу данных хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="1af29-138">Once exported, the flat files can then be loaded directly into the target the SQL Data Warehouse database.</span></span>

> [!NOTE]
> <span data-ttu-id="1af29-139">Рекомендуется включать преобразования, используемые во время экспорта данных, в представления в исходной системе.</span><span class="sxs-lookup"><span data-stu-id="1af29-139">It is often a good idea to encapsulate the transformations used during data export in a view on the source system.</span></span> <span data-ttu-id="1af29-140">В этом случае логика будет сохранена и процесс можно будет повторить.</span><span class="sxs-lookup"><span data-stu-id="1af29-140">This ensures that the logic is retained and the process is repeatable.</span></span>
> 
> 

<span data-ttu-id="1af29-141">Программа bcp обладает следующими преимуществами.</span><span class="sxs-lookup"><span data-stu-id="1af29-141">Advantages of bcp are:</span></span>

* <span data-ttu-id="1af29-142">Простота.</span><span class="sxs-lookup"><span data-stu-id="1af29-142">Simplicity.</span></span> <span data-ttu-id="1af29-143">Команды bcp просты для построения и выполнения.</span><span class="sxs-lookup"><span data-stu-id="1af29-143">bcp commands are simple to build and execute</span></span>
* <span data-ttu-id="1af29-144">Процесс загрузки можно повторять.</span><span class="sxs-lookup"><span data-stu-id="1af29-144">Re-startable load process.</span></span> <span data-ttu-id="1af29-145">После выполнения экспорта загрузку можно выполнять любое количество раз.</span><span class="sxs-lookup"><span data-stu-id="1af29-145">Once exported the load can be executed any number of times</span></span>

<span data-ttu-id="1af29-146">Программа bcp имеет следующие ограничения.</span><span class="sxs-lookup"><span data-stu-id="1af29-146">Limitations of bcp are:</span></span>

* <span data-ttu-id="1af29-147">Программа bcp работает только с табличными неструктурированными файлами.</span><span class="sxs-lookup"><span data-stu-id="1af29-147">bcp works with tabulated flat files only.</span></span> <span data-ttu-id="1af29-148">Программа bcp не работает с такими файлами, как XML или JSON.</span><span class="sxs-lookup"><span data-stu-id="1af29-148">It does not work with files such as xml or JSON</span></span>
* <span data-ttu-id="1af29-149">Возможности преобразования данных ограничены этапом экспорта и простые по своей природе.</span><span class="sxs-lookup"><span data-stu-id="1af29-149">Data transformation capabilities are limited to the export stage only and are simple in nature</span></span>
* <span data-ttu-id="1af29-150">Программа bcp не является надежным средством для загрузки данных через Интернет.</span><span class="sxs-lookup"><span data-stu-id="1af29-150">bcp has not been adapted to be robust when loading data over the internet.</span></span> <span data-ttu-id="1af29-151">Любой сетевой сбой приводит к ошибке загрузки.</span><span class="sxs-lookup"><span data-stu-id="1af29-151">Any network instability may cause a load error.</span></span>
* <span data-ttu-id="1af29-152">Программа bcp зависит от схемы, которая присутствует в целевой базе данных до загрузки.</span><span class="sxs-lookup"><span data-stu-id="1af29-152">bcp relies on the schema being present in the target database prior to the load</span></span>

<span data-ttu-id="1af29-153">Дополнительные сведения см. в статье [Загрузка данных с помощью bcp][Use bcp to load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="1af29-153">For more information, see [Use bcp to load data into SQL Data Warehouse][Use bcp to load data into SQL Data Warehouse].</span></span>

## <a name="optimizing-data-migration"></a><span data-ttu-id="1af29-154">Оптимизация переноса данных</span><span class="sxs-lookup"><span data-stu-id="1af29-154">Optimizing data migration</span></span>
<span data-ttu-id="1af29-155">Процесс переноса данных с помощью SQLDW можно эффективно разделить на три этапа:</span><span class="sxs-lookup"><span data-stu-id="1af29-155">A SQLDW data migration process can be effectively broken down into three discrete steps:</span></span>

1. <span data-ttu-id="1af29-156">Экспорт исходных данных</span><span class="sxs-lookup"><span data-stu-id="1af29-156">Export of source data</span></span>
2. <span data-ttu-id="1af29-157">Передача данных в Azure</span><span class="sxs-lookup"><span data-stu-id="1af29-157">Transfer of data to Azure</span></span>
3. <span data-ttu-id="1af29-158">Загрузка в целевую базу данных SQLDW</span><span class="sxs-lookup"><span data-stu-id="1af29-158">Load into the target SQLDW database</span></span>

<span data-ttu-id="1af29-159">Каждый этап можно оптимизировать для создания надежного, повторяемого и гибкого процесса переноса данных, который обеспечивает максимальную производительность на каждом отдельном этапе.</span><span class="sxs-lookup"><span data-stu-id="1af29-159">Each step can be individually optimized to create a robust, re-startable and resilient migration process that maximizes performance at each step.</span></span>

## <a name="optimizing-data-load"></a><span data-ttu-id="1af29-160">Оптимизация загрузки данных</span><span class="sxs-lookup"><span data-stu-id="1af29-160">Optimizing data load</span></span>
<span data-ttu-id="1af29-161">Если посмотреть на этапы в обратном порядке, самый быстрый способ загрузки данных — использовать PolyBase.</span><span class="sxs-lookup"><span data-stu-id="1af29-161">Looking at these in reverse order for a moment; the fastest way to load data is via PolyBase.</span></span> <span data-ttu-id="1af29-162">Оптимизация процесса загрузки с помощью PolyBase накладывает ряд требований к предыдущим этапам, поэтому лучше сразу их рассмотреть.</span><span class="sxs-lookup"><span data-stu-id="1af29-162">Optimizing for a PolyBase load process places prerequisites on the preceding steps so it's best to understand this upfront.</span></span> <span data-ttu-id="1af29-163">К ним относятся:</span><span class="sxs-lookup"><span data-stu-id="1af29-163">They are:</span></span>

1. <span data-ttu-id="1af29-164">Кодирование файлов данных</span><span class="sxs-lookup"><span data-stu-id="1af29-164">Encoding of data files</span></span>
2. <span data-ttu-id="1af29-165">Форматирование файлов данных</span><span class="sxs-lookup"><span data-stu-id="1af29-165">Format of data files</span></span>
3. <span data-ttu-id="1af29-166">Размещение файлов данных</span><span class="sxs-lookup"><span data-stu-id="1af29-166">Location of data files</span></span>

### <a name="encoding"></a><span data-ttu-id="1af29-167">Кодирование</span><span class="sxs-lookup"><span data-stu-id="1af29-167">Encoding</span></span>
<span data-ttu-id="1af29-168">Для PolyBase файлы данных должны иметь кодировку UTF-8 или UTF-16FE.</span><span class="sxs-lookup"><span data-stu-id="1af29-168">PolyBase requires data files to be UTF-8 or UTF-16FE.</span></span> 



### <a name="format-of-data-files"></a><span data-ttu-id="1af29-169">Форматирование файлов данных</span><span class="sxs-lookup"><span data-stu-id="1af29-169">Format of data files</span></span>
<span data-ttu-id="1af29-170">PolyBase требует наличия признака конца строки \n или новой строки.</span><span class="sxs-lookup"><span data-stu-id="1af29-170">PolyBase mandates a fixed row terminator of \n or newline.</span></span> <span data-ttu-id="1af29-171">Файлы данных должны соответствовать этому стандарту.</span><span class="sxs-lookup"><span data-stu-id="1af29-171">Your data files must conform to this standard.</span></span> <span data-ttu-id="1af29-172">Нет ограничений для признаков конца строки или столбца.</span><span class="sxs-lookup"><span data-stu-id="1af29-172">There aren't any restrictions on string or column terminators.</span></span>

<span data-ttu-id="1af29-173">В PolyBase необходимо определить каждый столбец в файле как часть внешней таблицы.</span><span class="sxs-lookup"><span data-stu-id="1af29-173">You will have to define every column in the file as part of your external table in PolyBase.</span></span> <span data-ttu-id="1af29-174">Убедитесь, что все экспортируемые столбцы обязательные и что типы соответствуют требуемым стандартам.</span><span class="sxs-lookup"><span data-stu-id="1af29-174">Make sure that all exported columns are required and that the types conform to the required standards.</span></span>

<span data-ttu-id="1af29-175">Сведения о поддерживаемых типах данных см. в предыдущей статье "Перенос схемы".</span><span class="sxs-lookup"><span data-stu-id="1af29-175">Please refer back to the [migrate your schema] article for detail on supported data types.</span></span>

### <a name="location-of-data-files"></a><span data-ttu-id="1af29-176">Размещение файлов данных</span><span class="sxs-lookup"><span data-stu-id="1af29-176">Location of data files</span></span>
<span data-ttu-id="1af29-177">Хранилище данных SQL использует PolyBase для загрузки данных только из хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="1af29-177">SQL Data Warehouse uses PolyBase to load data from Azure Blob Storage exclusively.</span></span> <span data-ttu-id="1af29-178">Следовательно, данные должны быть перенесены в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="1af29-178">Consequently, the data must have been first transferred into blob storage.</span></span>

## <a name="optimizing-data-transfer"></a><span data-ttu-id="1af29-179">Оптимизация переноса данных</span><span class="sxs-lookup"><span data-stu-id="1af29-179">Optimizing data transfer</span></span>
<span data-ttu-id="1af29-180">Один из самых медленных процессов переноса данных — это перенос данных в Azure.</span><span class="sxs-lookup"><span data-stu-id="1af29-180">One of the slowest parts of data migration is the transfer of the data to Azure.</span></span> <span data-ttu-id="1af29-181">Проблемой может стать не только пропускная способность сети, но и ее стабильная работа.</span><span class="sxs-lookup"><span data-stu-id="1af29-181">Not only can network bandwidth be an issue but also network reliability can seriously hamper progress.</span></span> <span data-ttu-id="1af29-182">По умолчанию перенос данных в Azure выполняется через Интернет, поэтому риск ошибок во время переноса довольно высокий.</span><span class="sxs-lookup"><span data-stu-id="1af29-182">By default migrating data to Azure is over the internet so the chances of transfer errors occurring are reasonably likely.</span></span> <span data-ttu-id="1af29-183">Тем не менее из-за этих ошибок может потребоваться переслать повторно все данные или их часть.</span><span class="sxs-lookup"><span data-stu-id="1af29-183">However, these errors may require data to be re-sent either in whole or in part.</span></span>

<span data-ttu-id="1af29-184">К счастью, существует несколько вариантов для повышения быстродействия и устойчивости этого процесса.</span><span class="sxs-lookup"><span data-stu-id="1af29-184">Fortunately you have several options to improve the speed and resilience of this process:</span></span>

### <a name="expressrouteexpressroute"></a><span data-ttu-id="1af29-185">[ExpressRoute][ExpressRoute]</span><span class="sxs-lookup"><span data-stu-id="1af29-185">[ExpressRoute][ExpressRoute]</span></span>
<span data-ttu-id="1af29-186">Чтобы ускорить перенос данных, вы можете воспользоваться [ExpressRoute][ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="1af29-186">You may want to consider using [ExpressRoute][ExpressRoute] to speed up the transfer.</span></span> <span data-ttu-id="1af29-187">[ExpressRoute][ExpressRoute] предоставляет установленное частное подключение к Azure, то есть подключение не будет проходить через Интернет.</span><span class="sxs-lookup"><span data-stu-id="1af29-187">[ExpressRoute][ExpressRoute] provides you with an established private connection to Azure so the connection does not go over the public internet.</span></span> <span data-ttu-id="1af29-188">Это отнюдь не является обязательным этапом.</span><span class="sxs-lookup"><span data-stu-id="1af29-188">This is by no means a mandatory step.</span></span> <span data-ttu-id="1af29-189">Тем не менее это улучшит пропускную способность при передаче данных в Azure с локальных или совместно используемых серверов.</span><span class="sxs-lookup"><span data-stu-id="1af29-189">However, it will improve throughput when pushing data to Azure from an on-premises or co-location facility.</span></span>

<span data-ttu-id="1af29-190">[ExpressRoute][ExpressRoute] обладает следующими преимуществами.</span><span class="sxs-lookup"><span data-stu-id="1af29-190">The benefits of using [ExpressRoute][ExpressRoute] are:</span></span>

1. <span data-ttu-id="1af29-191">Повышенная надежность</span><span class="sxs-lookup"><span data-stu-id="1af29-191">Increased reliability</span></span>
2. <span data-ttu-id="1af29-192">Более высокая скорость сети</span><span class="sxs-lookup"><span data-stu-id="1af29-192">Faster network speed</span></span>
3. <span data-ttu-id="1af29-193">Низкая задержка сети</span><span class="sxs-lookup"><span data-stu-id="1af29-193">Lower network latency</span></span>
4. <span data-ttu-id="1af29-194">Более высокая степень сетевой безопасности</span><span class="sxs-lookup"><span data-stu-id="1af29-194">higher network security</span></span>

<span data-ttu-id="1af29-195">[ExpressRoute][ExpressRoute] целесообразно использовать в целом ряде сценариев, а не только для переноса данных.</span><span class="sxs-lookup"><span data-stu-id="1af29-195">[ExpressRoute][ExpressRoute] is beneficial for a number of scenarios; not just the migration.</span></span>

<span data-ttu-id="1af29-196">Заинтересовались?</span><span class="sxs-lookup"><span data-stu-id="1af29-196">Interested?</span></span> <span data-ttu-id="1af29-197">Дополнительные сведения и цены см. в [документации по ExpressRoute][ExpressRoute documentation].</span><span class="sxs-lookup"><span data-stu-id="1af29-197">For more information and pricing please visit the [ExpressRoute documentation][ExpressRoute documentation].</span></span>

### <a name="azure-import-and-export-service"></a><span data-ttu-id="1af29-198">Служба импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="1af29-198">Azure Import and Export Service</span></span>
<span data-ttu-id="1af29-199">Служба импорта и экспорта Azure — это процесс переноса данных, предназначенный для больших (гигабайты данных) и очень больших (терабайты данных) объемов данных.</span><span class="sxs-lookup"><span data-stu-id="1af29-199">The Azure Import and Export Service is a data transfer process designed for large (GB++) to massive (TB++) transfers of data into Azure.</span></span> <span data-ttu-id="1af29-200">Процесс предполагает запись данных на диски с последующей пересылкой в центр обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="1af29-200">It involves writing your data to disks and shipping them to an Azure data center.</span></span> <span data-ttu-id="1af29-201">Содержимое дисков затем загружается в большие двоичные объекты службы хранилища Azure от вашего имени.</span><span class="sxs-lookup"><span data-stu-id="1af29-201">The disk contents will then be loaded into Azure Storage Blobs on your behalf.</span></span>

<span data-ttu-id="1af29-202">Общая схема процесса импорта и экспорта выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="1af29-202">A high-level view of the import export process is as follows:</span></span>

1. <span data-ttu-id="1af29-203">Настройка контейнера хранилища больших двоичных объектов Azure для получения данных</span><span class="sxs-lookup"><span data-stu-id="1af29-203">Configure an Azure Blob Storage container to receive the data</span></span>
2. <span data-ttu-id="1af29-204">Экспорт данных в локальное хранилище</span><span class="sxs-lookup"><span data-stu-id="1af29-204">Export your data to local storage</span></span>
3. <span data-ttu-id="1af29-205">Копирование данных на жесткие диски формата 3,5 дюйма SATA II/III с помощью средства импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="1af29-205">Copy the data to 3.5 inch SATA II/III hard disk drives using the [Azure Import/Export Tool]</span></span>
4. <span data-ttu-id="1af29-206">Создание задания импорта с помощью службы импорта и экспорта Azure с предоставлением файлов журналов, созданных средством импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="1af29-206">Create an Import Job using the Azure Import and Export Service providing the journal files produced by the [Azure Import/Export Tool]</span></span>
5. <span data-ttu-id="1af29-207">Пересылка дисков в указанный центр обработки данных Azure</span><span class="sxs-lookup"><span data-stu-id="1af29-207">Ship the disks your nominated Azure data center</span></span>
6. <span data-ttu-id="1af29-208">Данные перемещаются в контейнер хранилища больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="1af29-208">Your data is transferred to your Azure Blob Storage container</span></span>
7. <span data-ttu-id="1af29-209">Загрузка данных в SQLDW с помощью PolyBase</span><span class="sxs-lookup"><span data-stu-id="1af29-209">Load the data into SQLDW using PolyBase</span></span>

### <a name="azcopyazcopy-utility"></a><span data-ttu-id="1af29-210">Служебная программа [AZCopy][AZCopy]</span><span class="sxs-lookup"><span data-stu-id="1af29-210">[AZCopy][AZCopy] utility</span></span>
<span data-ttu-id="1af29-211">Служебная программа [AZCopy][AZCopy] прекрасно подходит для передачи данных в большие двоичные объекты службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="1af29-211">The [AZCopy][AZCopy] utility is a great tool for getting your data transferred into Azure Storage Blobs.</span></span> <span data-ttu-id="1af29-212">Средство предназначено для небольших (мегабайты данных) и очень больших (гигабайты данных) объемов данных.</span><span class="sxs-lookup"><span data-stu-id="1af29-212">It is designed for small (MB++) to very large (GB++) data transfers.</span></span> <span data-ttu-id="1af29-213">[AZCopy] также обеспечивает гибкую пропускную способность во время переноса данных в Azure, поэтому подходит для этапа переноса данных.</span><span class="sxs-lookup"><span data-stu-id="1af29-213">[AZCopy] has also been designed to provide good resilient throughput when transferring data to Azure and so is a great choice for the data transfer step.</span></span> <span data-ttu-id="1af29-214">После выполнения переноса данные можно загрузить с помощью PolyBase в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="1af29-214">Once transferred you can load the data using PolyBase into SQL Data Warehouse.</span></span> <span data-ttu-id="1af29-215">Средство AZCopy можно также добавить в пакеты служб SSIS с помощью задания "Выполнить процесс".</span><span class="sxs-lookup"><span data-stu-id="1af29-215">You can also incorporate AZCopy into your SSIS packages using an "Execute Process" task.</span></span>

<span data-ttu-id="1af29-216">Чтобы использовать AZCopy, сначала необходимо загрузить это средство и установить его.</span><span class="sxs-lookup"><span data-stu-id="1af29-216">To use AZCopy you will first need to download and install it.</span></span> <span data-ttu-id="1af29-217">Существует [рабочая версия][production version] и [пробная версия][preview version].</span><span class="sxs-lookup"><span data-stu-id="1af29-217">There is a [production version][production version] and a [preview version][preview version] available.</span></span>

<span data-ttu-id="1af29-218">Для загрузки файла из файловой системы потребуется командная строка, как та, что представлена ниже.</span><span class="sxs-lookup"><span data-stu-id="1af29-218">To upload a file from your file system you will need a command like the one below:</span></span>

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="1af29-219">В целом процесс может выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="1af29-219">A high-level process summary could be:</span></span>

1. <span data-ttu-id="1af29-220">Настройка контейнера большого двоичного объекта хранилища Azure для получения данных</span><span class="sxs-lookup"><span data-stu-id="1af29-220">Configure an Azure storage blob container to receive the data</span></span>
2. <span data-ttu-id="1af29-221">Экспорт данных в локальное хранилище</span><span class="sxs-lookup"><span data-stu-id="1af29-221">Export your data to local storage</span></span>
3. <span data-ttu-id="1af29-222">Копирование данных с помощью AZCopy в контейнер хранилища больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="1af29-222">AZCopy your data in the Azure Blob Storage container</span></span>
4. <span data-ttu-id="1af29-223">Загрузка данных в хранилище данных SQL с помощью PolyBase</span><span class="sxs-lookup"><span data-stu-id="1af29-223">Load the data into SQL Data Warehouse using PolyBase</span></span>

<span data-ttu-id="1af29-224">См. полную документацию по [AZCopy][AZCopy].</span><span class="sxs-lookup"><span data-stu-id="1af29-224">Full documentation available: [AZCopy][AZCopy].</span></span>

## <a name="optimizing-data-export"></a><span data-ttu-id="1af29-225">Оптимизация экспорта данных</span><span class="sxs-lookup"><span data-stu-id="1af29-225">Optimizing data export</span></span>
<span data-ttu-id="1af29-226">Помимо соблюдения требований PolyBase к экспорту данных, рекомендуется оптимизировать экспорт данных, чтобы еще больше улучшить процесс.</span><span class="sxs-lookup"><span data-stu-id="1af29-226">In addition to ensuring that the export conforms to the requirements laid out by PolyBase you can also seek to optimize the export of the data to improve the process further.</span></span>



### <a name="data-compression"></a><span data-ttu-id="1af29-227">Сжатие данных</span><span class="sxs-lookup"><span data-stu-id="1af29-227">Data compression</span></span>
<span data-ttu-id="1af29-228">PolyBase может читать данные, сжатые с помощью gzip.</span><span class="sxs-lookup"><span data-stu-id="1af29-228">PolyBase can read gzip compressed data.</span></span> <span data-ttu-id="1af29-229">Если есть возможность сжать файлы с помощью gzip, это позволит минимизировать объем данных, пересылаемый по сети.</span><span class="sxs-lookup"><span data-stu-id="1af29-229">If you are able to compress your data to gzip files then you will minimize the amount of data being pushed over the network.</span></span>

### <a name="multiple-files"></a><span data-ttu-id="1af29-230">Разделение на несколько файлов</span><span class="sxs-lookup"><span data-stu-id="1af29-230">Multiple files</span></span>
<span data-ttu-id="1af29-231">Разделение больших таблиц на несколько файлов не только повышает скорость экспорта, но и обеспечивает возможность повторного запуска и общую управляемость данных после переноса в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="1af29-231">Breaking up large tables into several files not only helps to improve export speed, it also helps with transfer re-startability, and the overall manageability of the data once in the Azure blob storage.</span></span> <span data-ttu-id="1af29-232">Одно из преимуществ PolyBase заключается в том, что средство позволяет читать все файлы внутри папки и обрабатывать их в виде одной таблицы.</span><span class="sxs-lookup"><span data-stu-id="1af29-232">One of the many nice features of PolyBase is that it will read all the files inside a folder and treat it as one table.</span></span> <span data-ttu-id="1af29-233">Поэтому рекомендуется разложить файлы для каждой таблицы в разные папки.</span><span class="sxs-lookup"><span data-stu-id="1af29-233">It is therefore a good idea to isolate the files for each table into its own folder.</span></span>

<span data-ttu-id="1af29-234">PolyBase также поддерживает так называемую функцию рекурсивного перебора папок.</span><span class="sxs-lookup"><span data-stu-id="1af29-234">PolyBase also supports a feature known as "recursive folder traversal".</span></span> <span data-ttu-id="1af29-235">Функция позволяет улучшить организацию экспортируемых данных и управление данными.</span><span class="sxs-lookup"><span data-stu-id="1af29-235">You can use this feature to further enhance the organization of your exported data to improve your data management.</span></span>

<span data-ttu-id="1af29-236">Дополнительные сведения о загрузке данных с помощью PolyBase в хранилище данных SQL см. в [этой статье][Use PolyBase to load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="1af29-236">To learn more about loading data with PolyBase, see [Use PolyBase to load data into SQL Data Warehouse][Use PolyBase to load data into SQL Data Warehouse].</span></span>

## <a name="next-steps"></a><span data-ttu-id="1af29-237">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1af29-237">Next steps</span></span>
<span data-ttu-id="1af29-238">Дополнительные сведения о переносе данных см. в статье [Перенос решения в хранилище данных SQL][Migrate your solution to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="1af29-238">For more about migration, see [Migrate your solution to SQL Data Warehouse][Migrate your solution to SQL Data Warehouse].</span></span>
<span data-ttu-id="1af29-239">Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][development overview].</span><span class="sxs-lookup"><span data-stu-id="1af29-239">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution to SQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp to load data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase to load data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
