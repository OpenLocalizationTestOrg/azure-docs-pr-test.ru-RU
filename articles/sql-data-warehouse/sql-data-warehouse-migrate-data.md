---
title: "aaaMigrate вашей tooSQL данных хранилища данных | Документы Microsoft"
description: "Советы по переносу вашей tooAzure данных хранилища данных SQL для разработки решений."
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
ms.openlocfilehash: fe4c6b7e82094c59c45e06be6da225fee1b707ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data"></a><span data-ttu-id="fbe9f-103">Перенос данных</span><span class="sxs-lookup"><span data-stu-id="fbe9f-103">Migrate Your Data</span></span>
<span data-ttu-id="fbe9f-104">Данные из различных источников можно переместить в хранилище данных SQL с помощью различных инструментов.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-104">Data can be moved from different sources into your SQL Data Warehouse with a variety tools.</span></span>  <span data-ttu-id="fbe9f-105">Копировать ADF, SSIS и bcp можно все используемые tooachieve этой цели.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-105">ADF Copy, SSIS, and bcp can all be used tooachieve this goal.</span></span> <span data-ttu-id="fbe9f-106">Однако с увеличением hello объем данных следует подумать о Дробление hello процесса миграции данных в действия.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-106">However, as hello amount of data increases you should think about breaking down hello data migration process into steps.</span></span> <span data-ttu-id="fbe9f-107">Это предоставляет hello toooptimize возможности каждого шага для производительности и устойчивости tooensure переноса smooth данных.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-107">This affords you hello opportunity toooptimize each step both for performance and for resilience tooensure a smooth data migration.</span></span>

<span data-ttu-id="fbe9f-108">Сценарии переноса простой hello Копировать ADF, SSIS и bcp сначала описаны в этой статье.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-108">This article first discusses hello simple migration scenarios of ADF Copy, SSIS, and bcp.</span></span> <span data-ttu-id="fbe9f-109">Он затем изучить более детально как можно оптимизировать hello миграции.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-109">It then look a little deeper into how hello migration can be optimized.</span></span>

## <a name="azure-data-factory-adf-copy"></a><span data-ttu-id="fbe9f-110">Копирование с помощью фабрики данных Azure (ADF)</span><span class="sxs-lookup"><span data-stu-id="fbe9f-110">Azure Data Factory (ADF) copy</span></span>
<span data-ttu-id="fbe9f-111">[ADF Copy][ADF Copy] входит в [фабрику данных Azure][Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="fbe9f-111">[ADF Copy][ADF Copy] is part of [Azure Data Factory][Azure Data Factory].</span></span> <span data-ttu-id="fbe9f-112">Можно использовать копию ADF tooexport tooflat файлы данных, находящиеся в локальном хранилище tooremote неструктурированных файлов, хранящихся в хранилище больших двоичных объектов или непосредственно в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-112">You can use ADF Copy tooexport your data tooflat files residing on local storage, tooremote flat files held in Azure blob storage or directly into SQL Data Warehouse.</span></span>

<span data-ttu-id="fbe9f-113">Если запускается данные в неструктурированные файлы, то необходимо сначала tootransfer его BLOB-объекта хранилища tooAzure перед запуском нагрузочного его в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-113">If your data starts in flat files, then you will first need tootransfer it tooAzure storage blob before initiating a load it into SQL Data Warehouse.</span></span> <span data-ttu-id="fbe9f-114">После hello данные передаются в хранилище больших двоичных объектов можно выбрать toouse [ADF копирования] [ ADF Copy] снова toopush hello данных в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-114">Once hello data is transferred into Azure blob storage you can choose toouse [ADF Copy][ADF Copy] again toopush hello data into SQL Data Warehouse.</span></span>

<span data-ttu-id="fbe9f-115">PolyBase также позволяет высокой производительности загрузки данных hello.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-115">PolyBase also provides a high-performance option for loading hello data.</span></span> <span data-ttu-id="fbe9f-116">Однако в этом случае придется использовать два средства вместо одного.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-116">However, that does mean using two tools instead of one.</span></span> <span data-ttu-id="fbe9f-117">Если требуется hello наилучшей производительности с помощью PolyBase.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-117">If you need hello best performance then use PolyBase.</span></span> <span data-ttu-id="fbe9f-118">Если требуется один интерфейс (и не больших объемов данных hello) ADF представляет решение этой задачи.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-118">If you want a single tool experience (and hello data is not massive) then ADF is your answer.</span></span>


> 
> 

<span data-ttu-id="fbe9f-119">Головной по следующей статьей некоторые превосходная toohello [образцы ADF][ADF samples].</span><span class="sxs-lookup"><span data-stu-id="fbe9f-119">Head over toohello following article for some great [ADF samples][ADF samples].</span></span>

## <a name="integration-services"></a><span data-ttu-id="fbe9f-120">Службы интеграции</span><span class="sxs-lookup"><span data-stu-id="fbe9f-120">Integration Services</span></span>
<span data-ttu-id="fbe9f-121">Службы Integration Services (SSIS) — это мощное и гибкое средство загрузки данных, которое поддерживает сложные рабочие потоки, преобразование данных и разные параметры загрузки.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-121">Integration Services (SSIS) is a powerful and flexible Extract Transform and Load (ETL) tool that supports complex workflows, data transformation, and several data loading options.</span></span> <span data-ttu-id="fbe9f-122">Используйте перенос данных служб SSIS toosimply tooAzure или как часть более широкой миграции.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-122">Use SSIS toosimply transfer data tooAzure or as part of a broader migration.</span></span>

> [!NOTE]
> <span data-ttu-id="fbe9f-123">Службы SSIS можно экспортировать tooUTF-8 без отметки порядка байтов hello в файле hello.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-123">SSIS can export tooUTF-8 without hello byte order mark in hello file.</span></span> <span data-ttu-id="fbe9f-124">tooconfigure, это необходимо, с помощью hello производный столбец компонента tooconvert hello символьные данные в hello данных потока toouse hello 65001 UTF-8 кодовую страницу.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-124">tooconfigure this you must first use hello derived column component tooconvert hello character data in hello data flow toouse hello 65001 UTF-8 code page.</span></span> <span data-ttu-id="fbe9f-125">После преобразования hello столбцы записи hello данных toohello неструктурированный файл назначения адаптера обеспечение 65001 также был выбран как hello кодовой страницы для файла hello.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-125">Once hello columns have been converted, write hello data toohello flat file destination adapter ensuring that 65001 has also been selected as hello code page for hello file.</span></span>
> 
> 

<span data-ttu-id="fbe9f-126">Службы SSIS подключается tooSQL хранилища данных, так же, как он должен быть подключен tooa развертывания сервера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-126">SSIS connects tooSQL Data Warehouse just as it would connect tooa SQL Server deployment.</span></span> <span data-ttu-id="fbe9f-127">Тем не менее подключениями потребуется toobe, используя диспетчер соединений ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-127">However, your connections will need toobe using an ADO.NET connection manager.</span></span> <span data-ttu-id="fbe9f-128">Следует также обратить внимание hello tooconfigure «Использование инструкции bulk insert при наличии» пропускная способность toomaximize параметр.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-128">You should also take care tooconfigure hello "Use bulk insert when available" setting toomaximize throughput.</span></span> <span data-ttu-id="fbe9f-129">См. toohello [адаптер назначения ADO.NET] [ ADO.NET destination adapter] toolearn статье Дополнительные об этом свойстве</span><span class="sxs-lookup"><span data-stu-id="fbe9f-129">Please refer toohello [ADO.NET destination adapter][ADO.NET destination adapter] article toolearn more about this property</span></span>

> [!NOTE]
> <span data-ttu-id="fbe9f-130">Подключение tooAzure хранилище данных SQL с помощью OLE DB не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-130">Connecting tooAzure SQL Data Warehouse by using OLEDB is not supported.</span></span>
> 
> 

<span data-ttu-id="fbe9f-131">Кроме того, всегда есть возможность hello, что пакет может завершиться ошибкой из-за проблем с toothrottling или сети.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-131">In addition, there is always hello possibility that a package might fail due toothrottling or network issues.</span></span> <span data-ttu-id="fbe9f-132">Конструктор пакетов, их можно было возобновить в точке сбоя hello без возврат работы, выполненной до сбоя hello.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-132">Design packages so they can be resumed at hello point of failure, without redoing work that completed before hello failure.</span></span>

<span data-ttu-id="fbe9f-133">Дополнительные сведения можно найти hello [документации служб SSIS][SSIS documentation].</span><span class="sxs-lookup"><span data-stu-id="fbe9f-133">For more information consult hello [SSIS documentation][SSIS documentation].</span></span>

## <a name="bcp"></a><span data-ttu-id="fbe9f-134">bcp</span><span class="sxs-lookup"><span data-stu-id="fbe9f-134">bcp</span></span>
<span data-ttu-id="fbe9f-135">Программа bcp — средство командной строки, предназначенное для импорта и экспорта данных неструктурированных файлов.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-135">bcp is a command-line utility that is designed for flat file data import and export.</span></span> <span data-ttu-id="fbe9f-136">Во время экспорта можно выполнять преобразование.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-136">Some transformation can take place during data export.</span></span> <span data-ttu-id="fbe9f-137">простой преобразования tooperform использовать tooselect запроса и преобразования данных hello.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-137">tooperform simple transformations use a query tooselect and transform hello data.</span></span> <span data-ttu-id="fbe9f-138">После экспорта hello неструктурированные файлы затем можно загрузить непосредственно в hello хранилище данных SQL hello целевой базы данных.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-138">Once exported, hello flat files can then be loaded directly into hello target hello SQL Data Warehouse database.</span></span>

> [!NOTE]
> <span data-ttu-id="fbe9f-139">Часто бывает hello tooencapsulate смысл, экспортировать преобразований, использованной для данных в представлении в исходной системе hello.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-139">It is often a good idea tooencapsulate hello transformations used during data export in a view on hello source system.</span></span> <span data-ttu-id="fbe9f-140">Это гарантирует, что логика hello сохраняется и hello процесса необходимо повторять.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-140">This ensures that hello logic is retained and hello process is repeatable.</span></span>
> 
> 

<span data-ttu-id="fbe9f-141">Программа bcp обладает следующими преимуществами.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-141">Advantages of bcp are:</span></span>

* <span data-ttu-id="fbe9f-142">Простота.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-142">Simplicity.</span></span> <span data-ttu-id="fbe9f-143">команды bcp простой toobuild и выполнение</span><span class="sxs-lookup"><span data-stu-id="fbe9f-143">bcp commands are simple toobuild and execute</span></span>
* <span data-ttu-id="fbe9f-144">Процесс загрузки можно повторять.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-144">Re-startable load process.</span></span> <span data-ttu-id="fbe9f-145">Один раз экспортированного hello загрузки может оказаться выполняться любое количество раз</span><span class="sxs-lookup"><span data-stu-id="fbe9f-145">Once exported hello load can be executed any number of times</span></span>

<span data-ttu-id="fbe9f-146">Программа bcp имеет следующие ограничения.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-146">Limitations of bcp are:</span></span>

* <span data-ttu-id="fbe9f-147">Программа bcp работает только с табличными неструктурированными файлами.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-147">bcp works with tabulated flat files only.</span></span> <span data-ttu-id="fbe9f-148">Программа bcp не работает с такими файлами, как XML или JSON.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-148">It does not work with files such as xml or JSON</span></span>
* <span data-ttu-id="fbe9f-149">Возможности по преобразованию данных являются только ограниченный toohello этапе экспорта и просты по своей природе</span><span class="sxs-lookup"><span data-stu-id="fbe9f-149">Data transformation capabilities are limited toohello export stage only and are simple in nature</span></span>
* <span data-ttu-id="fbe9f-150">bcp не был адаптирован toobe надежным при загрузке данных через hello internet.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-150">bcp has not been adapted toobe robust when loading data over hello internet.</span></span> <span data-ttu-id="fbe9f-151">Любой сетевой сбой приводит к ошибке загрузки.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-151">Any network instability may cause a load error.</span></span>
* <span data-ttu-id="fbe9f-152">bcp зависит от схемы hello их присутствия в загрузки предыдущих toohello hello целевой базы данных</span><span class="sxs-lookup"><span data-stu-id="fbe9f-152">bcp relies on hello schema being present in hello target database prior toohello load</span></span>

<span data-ttu-id="fbe9f-153">Дополнительные сведения см. в разделе [использовать bcp tooload данные в хранилище данных SQL][Use bcp tooload data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="fbe9f-153">For more information, see [Use bcp tooload data into SQL Data Warehouse][Use bcp tooload data into SQL Data Warehouse].</span></span>

## <a name="optimizing-data-migration"></a><span data-ttu-id="fbe9f-154">Оптимизация переноса данных</span><span class="sxs-lookup"><span data-stu-id="fbe9f-154">Optimizing data migration</span></span>
<span data-ttu-id="fbe9f-155">Процесс переноса данных с помощью SQLDW можно эффективно разделить на три этапа:</span><span class="sxs-lookup"><span data-stu-id="fbe9f-155">A SQLDW data migration process can be effectively broken down into three discrete steps:</span></span>

1. <span data-ttu-id="fbe9f-156">Экспорт исходных данных</span><span class="sxs-lookup"><span data-stu-id="fbe9f-156">Export of source data</span></span>
2. <span data-ttu-id="fbe9f-157">Передача данных tooAzure</span><span class="sxs-lookup"><span data-stu-id="fbe9f-157">Transfer of data tooAzure</span></span>
3. <span data-ttu-id="fbe9f-158">Загрузить в базу данных SQLDW целевой hello</span><span class="sxs-lookup"><span data-stu-id="fbe9f-158">Load into hello target SQLDW database</span></span>

<span data-ttu-id="fbe9f-159">Каждый шаг можно по отдельности оптимизированного toocreate процесса миграции надежной, повторно запустить и гибкой, позволяет повысить производительность на каждом шаге.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-159">Each step can be individually optimized toocreate a robust, re-startable and resilient migration process that maximizes performance at each step.</span></span>

## <a name="optimizing-data-load"></a><span data-ttu-id="fbe9f-160">Оптимизация загрузки данных</span><span class="sxs-lookup"><span data-stu-id="fbe9f-160">Optimizing data load</span></span>
<span data-ttu-id="fbe9f-161">Просматривая их в обратном порядке для некоторое время; Hello самый быстрый способ tooload данных осуществляется через PolyBase.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-161">Looking at these in reverse order for a moment; hello fastest way tooload data is via PolyBase.</span></span> <span data-ttu-id="fbe9f-162">Оптимизация для загрузки процесса PolyBase помещает необходимые компоненты на предыдущих шагах, поэтому наиболее toounderstand это hello переднего плана.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-162">Optimizing for a PolyBase load process places prerequisites on hello preceding steps so it's best toounderstand this upfront.</span></span> <span data-ttu-id="fbe9f-163">К ним относятся:</span><span class="sxs-lookup"><span data-stu-id="fbe9f-163">They are:</span></span>

1. <span data-ttu-id="fbe9f-164">Кодирование файлов данных</span><span class="sxs-lookup"><span data-stu-id="fbe9f-164">Encoding of data files</span></span>
2. <span data-ttu-id="fbe9f-165">Форматирование файлов данных</span><span class="sxs-lookup"><span data-stu-id="fbe9f-165">Format of data files</span></span>
3. <span data-ttu-id="fbe9f-166">Размещение файлов данных</span><span class="sxs-lookup"><span data-stu-id="fbe9f-166">Location of data files</span></span>

### <a name="encoding"></a><span data-ttu-id="fbe9f-167">Кодирование</span><span class="sxs-lookup"><span data-stu-id="fbe9f-167">Encoding</span></span>
<span data-ttu-id="fbe9f-168">PolyBase требуется toobe файлы данных UTF-8 или UTF-16FE.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-168">PolyBase requires data files toobe UTF-8 or UTF-16FE.</span></span> 



### <a name="format-of-data-files"></a><span data-ttu-id="fbe9f-169">Форматирование файлов данных</span><span class="sxs-lookup"><span data-stu-id="fbe9f-169">Format of data files</span></span>
<span data-ttu-id="fbe9f-170">PolyBase требует наличия признака конца строки \n или новой строки.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-170">PolyBase mandates a fixed row terminator of \n or newline.</span></span> <span data-ttu-id="fbe9f-171">Файлы данных должны соответствовать toothis standard.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-171">Your data files must conform toothis standard.</span></span> <span data-ttu-id="fbe9f-172">Нет ограничений для признаков конца строки или столбца.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-172">There aren't any restrictions on string or column terminators.</span></span>

<span data-ttu-id="fbe9f-173">Вы получите toodefine каждый столбец в файле hello как часть в PolyBase внешней таблицы.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-173">You will have toodefine every column in hello file as part of your external table in PolyBase.</span></span> <span data-ttu-id="fbe9f-174">Убедитесь, что все экспортированные столбцы являются обязательными и соответствия стандартам toohello необходимые типы hello.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-174">Make sure that all exported columns are required and that hello types conform toohello required standards.</span></span>

<span data-ttu-id="fbe9f-175">Можно найти toohello [миграция схемы] статьи, сведения о поддерживаемых типах данных.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-175">Please refer back toohello [migrate your schema] article for detail on supported data types.</span></span>

### <a name="location-of-data-files"></a><span data-ttu-id="fbe9f-176">Размещение файлов данных</span><span class="sxs-lookup"><span data-stu-id="fbe9f-176">Location of data files</span></span>
<span data-ttu-id="fbe9f-177">Хранилище данных SQL используются только данные tooload PolyBase из хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-177">SQL Data Warehouse uses PolyBase tooload data from Azure Blob Storage exclusively.</span></span> <span data-ttu-id="fbe9f-178">Следовательно hello данных необходимо сначала перенесены в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-178">Consequently, hello data must have been first transferred into blob storage.</span></span>

## <a name="optimizing-data-transfer"></a><span data-ttu-id="fbe9f-179">Оптимизация переноса данных</span><span class="sxs-lookup"><span data-stu-id="fbe9f-179">Optimizing data transfer</span></span>
<span data-ttu-id="fbe9f-180">Одна из самых медленных частей hello переноса данных — перенос hello tooAzure данных hello.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-180">One of hello slowest parts of data migration is hello transfer of hello data tooAzure.</span></span> <span data-ttu-id="fbe9f-181">Проблемой может стать не только пропускная способность сети, но и ее стабильная работа.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-181">Not only can network bandwidth be an issue but also network reliability can seriously hamper progress.</span></span> <span data-ttu-id="fbe9f-182">По умолчанию tooAzure перенос данных превышает hello Интернет так hello возможность передачи ошибок могут быть достаточно.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-182">By default migrating data tooAzure is over hello internet so hello chances of transfer errors occurring are reasonably likely.</span></span> <span data-ttu-id="fbe9f-183">Однако этих ошибок может потребоваться повторно отправлять целиком или частично toobe данных.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-183">However, these errors may require data toobe re-sent either in whole or in part.</span></span>

<span data-ttu-id="fbe9f-184">К счастью, имеется несколько параметров tooimprove hello скорость и отказоустойчивость этого процесса:</span><span class="sxs-lookup"><span data-stu-id="fbe9f-184">Fortunately you have several options tooimprove hello speed and resilience of this process:</span></span>

### <a name="expressrouteexpressroute"></a><span data-ttu-id="fbe9f-185">[ExpressRoute][ExpressRoute]</span><span class="sxs-lookup"><span data-stu-id="fbe9f-185">[ExpressRoute][ExpressRoute]</span></span>
<span data-ttu-id="fbe9f-186">Вы можете с помощью tooconsider [ExpressRoute] [ ExpressRoute] toospeed копирование hello передачи.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-186">You may want tooconsider using [ExpressRoute][ExpressRoute] toospeed up hello transfer.</span></span> <span data-ttu-id="fbe9f-187">[ExpressRoute] [ ExpressRoute] предоставляет вам tooAzure частного подключения, подключения hello не передается по hello общедоступный Интернет.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-187">[ExpressRoute][ExpressRoute] provides you with an established private connection tooAzure so hello connection does not go over hello public internet.</span></span> <span data-ttu-id="fbe9f-188">Это отнюдь не является обязательным этапом.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-188">This is by no means a mandatory step.</span></span> <span data-ttu-id="fbe9f-189">Тем не менее, он будет повысить пропускную способность, при принудительной установке tooAzure данных из локальной или совместно используемой.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-189">However, it will improve throughput when pushing data tooAzure from an on-premises or co-location facility.</span></span>

<span data-ttu-id="fbe9f-190">Здравствуйте, преимущества использования [ExpressRoute] [ ExpressRoute] являются:</span><span class="sxs-lookup"><span data-stu-id="fbe9f-190">hello benefits of using [ExpressRoute][ExpressRoute] are:</span></span>

1. <span data-ttu-id="fbe9f-191">Повышенная надежность</span><span class="sxs-lookup"><span data-stu-id="fbe9f-191">Increased reliability</span></span>
2. <span data-ttu-id="fbe9f-192">Более высокая скорость сети</span><span class="sxs-lookup"><span data-stu-id="fbe9f-192">Faster network speed</span></span>
3. <span data-ttu-id="fbe9f-193">Низкая задержка сети</span><span class="sxs-lookup"><span data-stu-id="fbe9f-193">Lower network latency</span></span>
4. <span data-ttu-id="fbe9f-194">Более высокая степень сетевой безопасности</span><span class="sxs-lookup"><span data-stu-id="fbe9f-194">higher network security</span></span>

<span data-ttu-id="fbe9f-195">[ExpressRoute] [ ExpressRoute] является полезным для некоторых сценариев; не только hello миграции.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-195">[ExpressRoute][ExpressRoute] is beneficial for a number of scenarios; not just hello migration.</span></span>

<span data-ttu-id="fbe9f-196">Заинтересовались?</span><span class="sxs-lookup"><span data-stu-id="fbe9f-196">Interested?</span></span> <span data-ttu-id="fbe9f-197">Дополнительные сведения и ценах обратитесь по адресу hello [документации по ExpressRoute][ExpressRoute documentation].</span><span class="sxs-lookup"><span data-stu-id="fbe9f-197">For more information and pricing please visit hello [ExpressRoute documentation][ExpressRoute documentation].</span></span>

### <a name="azure-import-and-export-service"></a><span data-ttu-id="fbe9f-198">Служба импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="fbe9f-198">Azure Import and Export Service</span></span>
<span data-ttu-id="fbe9f-199">Hello службы Azure импорта и экспорта является процесса передачи данных, предназначенных для больших (ГБ ++) toomassive (ТБ ++) передач данных в Azure.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-199">hello Azure Import and Export Service is a data transfer process designed for large (GB++) toomassive (TB++) transfers of data into Azure.</span></span> <span data-ttu-id="fbe9f-200">Он включает в себя записи вашей toodisks данных и доставку их tooan центр обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-200">It involves writing your data toodisks and shipping them tooan Azure data center.</span></span> <span data-ttu-id="fbe9f-201">Затем содержимое диска Hello будут загружены в хранилище BLOB-объектов Azure от вашего имени.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-201">hello disk contents will then be loaded into Azure Storage Blobs on your behalf.</span></span>

<span data-ttu-id="fbe9f-202">Высокоуровневый обзор процесса экспорта импорта hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="fbe9f-202">A high-level view of hello import export process is as follows:</span></span>

1. <span data-ttu-id="fbe9f-203">Настройка данных hello tooreceive контейнер хранилища больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="fbe9f-203">Configure an Azure Blob Storage container tooreceive hello data</span></span>
2. <span data-ttu-id="fbe9f-204">Экспорт toolocal хранилище данных</span><span class="sxs-lookup"><span data-stu-id="fbe9f-204">Export your data toolocal storage</span></span>
3. <span data-ttu-id="fbe9f-205">Скопируйте hello данных too3.5 дюйма SATA II или III жестких дисков с помощью hello [средство импорта и экспорта Azure]</span><span class="sxs-lookup"><span data-stu-id="fbe9f-205">Copy hello data too3.5 inch SATA II/III hard disk drives using hello [Azure Import/Export Tool]</span></span>
4. <span data-ttu-id="fbe9f-206">Создание задания импорта с помощью hello Azure импорта и экспорта службы, предоставляющей hello файлы журнала, созданные hello [средство импорта и экспорта Azure]</span><span class="sxs-lookup"><span data-stu-id="fbe9f-206">Create an Import Job using hello Azure Import and Export Service providing hello journal files produced by hello [Azure Import/Export Tool]</span></span>
5. <span data-ttu-id="fbe9f-207">Переслать диски hello назначенный ЦОД Azure</span><span class="sxs-lookup"><span data-stu-id="fbe9f-207">Ship hello disks your nominated Azure data center</span></span>
6. <span data-ttu-id="fbe9f-208">Данные не переносятся tooyour контейнер хранилища больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="fbe9f-208">Your data is transferred tooyour Azure Blob Storage container</span></span>
7. <span data-ttu-id="fbe9f-209">Загрузка данных с помощью PolyBase SQLDW hello</span><span class="sxs-lookup"><span data-stu-id="fbe9f-209">Load hello data into SQLDW using PolyBase</span></span>

### <a name="azcopyazcopy-utility"></a><span data-ttu-id="fbe9f-210">Служебная программа [AZCopy][AZCopy]</span><span class="sxs-lookup"><span data-stu-id="fbe9f-210">[AZCopy][AZCopy] utility</span></span>
<span data-ttu-id="fbe9f-211">Hello [AZCopy][AZCopy] программа — это мощный инструмент для получения данных передано в BLOB-объектов хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-211">hello [AZCopy][AZCopy] utility is a great tool for getting your data transferred into Azure Storage Blobs.</span></span> <span data-ttu-id="fbe9f-212">Она предназначена для небольших (МБ ++) toovery больших (ГБ ++) передачи данных.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-212">It is designed for small (MB++) toovery large (GB++) data transfers.</span></span> <span data-ttu-id="fbe9f-213">[AZCopy] был спроектированный tooprovide устойчивым повышению производительности при передаче данных tooAzure и поэтому отлично подходит для шага передачи данных hello.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-213">[AZCopy] has also been designed tooprovide good resilient throughput when transferring data tooAzure and so is a great choice for hello data transfer step.</span></span> <span data-ttu-id="fbe9f-214">Один раз переносятся можно загрузить данные hello, используя PolyBase в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-214">Once transferred you can load hello data using PolyBase into SQL Data Warehouse.</span></span> <span data-ttu-id="fbe9f-215">Средство AZCopy можно также добавить в пакеты служб SSIS с помощью задания "Выполнить процесс".</span><span class="sxs-lookup"><span data-stu-id="fbe9f-215">You can also incorporate AZCopy into your SSIS packages using an "Execute Process" task.</span></span>

<span data-ttu-id="fbe9f-216">toouse AZCopy, то сначала необходимо toodownload и установить его.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-216">toouse AZCopy you will first need toodownload and install it.</span></span> <span data-ttu-id="fbe9f-217">Существует [рабочая версия][production version] и [пробная версия][preview version].</span><span class="sxs-lookup"><span data-stu-id="fbe9f-217">There is a [production version][production version] and a [preview version][preview version] available.</span></span>

<span data-ttu-id="fbe9f-218">tooupload файл из файловой системы достаточно команды, аналогичной hello один ниже:</span><span class="sxs-lookup"><span data-stu-id="fbe9f-218">tooupload a file from your file system you will need a command like hello one below:</span></span>

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="fbe9f-219">В целом процесс может выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-219">A high-level process summary could be:</span></span>

1. <span data-ttu-id="fbe9f-220">Настройка хранилища Azure данные большого двоичного объекта контейнера tooreceive hello</span><span class="sxs-lookup"><span data-stu-id="fbe9f-220">Configure an Azure storage blob container tooreceive hello data</span></span>
2. <span data-ttu-id="fbe9f-221">Экспорт toolocal хранилище данных</span><span class="sxs-lookup"><span data-stu-id="fbe9f-221">Export your data toolocal storage</span></span>
3. <span data-ttu-id="fbe9f-222">AZCopy данных в контейнер хранилища больших двоичных объектов hello</span><span class="sxs-lookup"><span data-stu-id="fbe9f-222">AZCopy your data in hello Azure Blob Storage container</span></span>
4. <span data-ttu-id="fbe9f-223">Hello данные загружаются в хранилище данных SQL с помощью PolyBase</span><span class="sxs-lookup"><span data-stu-id="fbe9f-223">Load hello data into SQL Data Warehouse using PolyBase</span></span>

<span data-ttu-id="fbe9f-224">См. полную документацию по [AZCopy][AZCopy].</span><span class="sxs-lookup"><span data-stu-id="fbe9f-224">Full documentation available: [AZCopy][AZCopy].</span></span>

## <a name="optimizing-data-export"></a><span data-ttu-id="fbe9f-225">Оптимизация экспорта данных</span><span class="sxs-lookup"><span data-stu-id="fbe9f-225">Optimizing data export</span></span>
<span data-ttu-id="fbe9f-226">В дополнение к этому tooensuring соответствие требованиям toohello располагаются с PolyBase вы hello экспорта можно выполнять поиск экспорта hello toooptimize процесса hello данных tooimprove hello дальнейшей.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-226">In addition tooensuring that hello export conforms toohello requirements laid out by PolyBase you can also seek toooptimize hello export of hello data tooimprove hello process further.</span></span>



### <a name="data-compression"></a><span data-ttu-id="fbe9f-227">Сжатие данных</span><span class="sxs-lookup"><span data-stu-id="fbe9f-227">Data compression</span></span>
<span data-ttu-id="fbe9f-228">PolyBase может читать данные, сжатые с помощью gzip.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-228">PolyBase can read gzip compressed data.</span></span> <span data-ttu-id="fbe9f-229">Если вы не можете toocompress toogzip файлов данных, то можно будет свести к минимуму hello объем данных, отправленных по сети hello.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-229">If you are able toocompress your data toogzip files then you will minimize hello amount of data being pushed over hello network.</span></span>

### <a name="multiple-files"></a><span data-ttu-id="fbe9f-230">Разделение на несколько файлов</span><span class="sxs-lookup"><span data-stu-id="fbe9f-230">Multiple files</span></span>
<span data-ttu-id="fbe9f-231">Разбиение большой таблицы на несколько файлов не только tooimprove Экспорт скорости, также позволяет передавать re-startability и hello общей управляемости hello данных один раз в хранилище больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-231">Breaking up large tables into several files not only helps tooimprove export speed, it also helps with transfer re-startability, and hello overall manageability of hello data once in hello Azure blob storage.</span></span> <span data-ttu-id="fbe9f-232">Одно из hello множество удобных функций PolyBase является будет читать все hello файлы в папку и рассматривать его как одна таблица.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-232">One of hello many nice features of PolyBase is that it will read all hello files inside a folder and treat it as one table.</span></span> <span data-ttu-id="fbe9f-233">Именно поэтому файлов hello tooisolate хорошей идеей для каждой таблицы в отдельную папку.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-233">It is therefore a good idea tooisolate hello files for each table into its own folder.</span></span>

<span data-ttu-id="fbe9f-234">PolyBase также поддерживает так называемую функцию рекурсивного перебора папок.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-234">PolyBase also supports a feature known as "recursive folder traversal".</span></span> <span data-ttu-id="fbe9f-235">Эту функцию можно использовать toofurther улучшения организации hello вашей tooimprove экспортированных данных на управление данными.</span><span class="sxs-lookup"><span data-stu-id="fbe9f-235">You can use this feature toofurther enhance hello organization of your exported data tooimprove your data management.</span></span>

<span data-ttu-id="fbe9f-236">в разделе toolearn Дополнительные сведения о загрузке данных с помощью PolyBase, [PolyBase используйте tooload данных в хранилище данных SQL][Use PolyBase tooload data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="fbe9f-236">toolearn more about loading data with PolyBase, see [Use PolyBase tooload data into SQL Data Warehouse][Use PolyBase tooload data into SQL Data Warehouse].</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbe9f-237">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fbe9f-237">Next steps</span></span>
<span data-ttu-id="fbe9f-238">Дополнительные сведения о миграции см. в разделе [перенести tooSQL вашего решения хранилища данных][Migrate your solution tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="fbe9f-238">For more about migration, see [Migrate your solution tooSQL Data Warehouse][Migrate your solution tooSQL Data Warehouse].</span></span>
<span data-ttu-id="fbe9f-239">Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][development overview].</span><span class="sxs-lookup"><span data-stu-id="fbe9f-239">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution tooSQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp tooload data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase tooload data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
