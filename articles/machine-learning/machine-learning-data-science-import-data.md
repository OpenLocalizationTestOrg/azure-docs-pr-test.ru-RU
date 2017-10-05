---
title: "Импорт данных в Студию машинного обучения | Документация Майкрософт"
description: "Импорт данных в студию машинного обучения Azure из разных источников данных Узнайте, какие типы данных и форматы данных поддерживаются."
keywords: "импорт данных, формат данных, типы данных, источники данных, обучающие данные"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c194ee3b-838c-4efe-bb2a-c1d052326216
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: garye;bradsev
ms.openlocfilehash: b92b480e62f4ce4f4836dc5d0f6afbe80c6b664a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a><span data-ttu-id="3d0d5-105">Импорт обучающих данных в Студию машинного обучения Azure из разных источников данных</span><span class="sxs-lookup"><span data-stu-id="3d0d5-105">Import your training data into Azure Machine Learning Studio from various data sources</span></span>
<span data-ttu-id="3d0d5-106">Чтобы при разработке решения прогнозной аналитики и обучении работе с таким решением использовать в студии машинного обучения собственные данные, можно выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="3d0d5-106">To use your own data in Machine Learning Studio to develop and train a predictive analytics solution, you can:</span></span> 

* <span data-ttu-id="3d0d5-107">заранее отправить данные из **локального файла** на жестком диске, чтобы создать модуль набора данных в рабочей области;</span><span class="sxs-lookup"><span data-stu-id="3d0d5-107">upload data from a **local file** ahead of time from your hard drive to create a dataset module in your workspace</span></span>
* <span data-ttu-id="3d0d5-108">получить доступ к данным из одного из нескольких **источников данных в Интернете** во время запуска эксперимента с помощью модуля [Импорт данных][import-data];</span><span class="sxs-lookup"><span data-stu-id="3d0d5-108">access data from one of several **online data sources** while your experiment is running using the [Import Data][import-data] module</span></span> 
* <span data-ttu-id="3d0d5-109">использовать данные из другого эксперимента машинного обучения Azure, сохраненные в виде **набора данных**;</span><span class="sxs-lookup"><span data-stu-id="3d0d5-109">use data from another Azure Machine learning **experiment** saved as a dataset</span></span>
* <span data-ttu-id="3d0d5-110">использовать данные из локальной **базы данных SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="3d0d5-110">use data from an on-premises **SQL Server database**</span></span>

<span data-ttu-id="3d0d5-111">Каждое из этих действий подробно описано в разделах, перечисленных в меню выше.</span><span class="sxs-lookup"><span data-stu-id="3d0d5-111">Each of these options is described in one of the topics on the menu below.</span></span> <span data-ttu-id="3d0d5-112">В этом разделе показано, как импортировать в Студию машинного обучения данные из различных источников.</span><span class="sxs-lookup"><span data-stu-id="3d0d5-112">These topics show you how to import data from these various data sources to use in Machine Learning Studio.</span></span> 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> <span data-ttu-id="3d0d5-113">В Студии машинного обучения есть множество примеров наборов данных, которые можно использовать для обучающих данных.</span><span class="sxs-lookup"><span data-stu-id="3d0d5-113">There are a number of sample datasets available in Machine Learning Studio that you can use for training data.</span></span> <span data-ttu-id="3d0d5-114">Подробнее в статье [Использование образцов наборов данных в Студии машинного обучения Azure](machine-learning-use-sample-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="3d0d5-114">For information on these, see [Use the sample datasets in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span></span>
> 
> 

<span data-ttu-id="3d0d5-115">Во вводном разделе описывается также подготовка данных для использования в Студии машинного обучения, а также поддерживаемые форматы и типы данных.</span><span class="sxs-lookup"><span data-stu-id="3d0d5-115">This introductory topic also discusses how to get data ready for use in Machine Learning Studio and describes which data formats and data types are supported.</span></span> 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a><span data-ttu-id="3d0d5-116">Подготовка данных для использования в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="3d0d5-116">Get data ready for use in Azure Machine Learning Studio</span></span>
<span data-ttu-id="3d0d5-117">Студия машинного обучения Microsoft Azure предназначена для работы с прямоугольными массивами или таблицами данных, такими как текстовые данные с разделителями или структурированные данные из базы данных, хотя в некоторых случаях могут быть использованы данные из непрямоугольных массивов.</span><span class="sxs-lookup"><span data-stu-id="3d0d5-117">Machine Learning Studio is designed to work with rectangular or tabular data, such as text data that's delimited or structured data from a database, though in some circumstances non-rectangular data may be used.</span></span>

<span data-ttu-id="3d0d5-118">Лучше, если данные относительно очищены.</span><span class="sxs-lookup"><span data-stu-id="3d0d5-118">It's best if your data is relatively clean.</span></span> <span data-ttu-id="3d0d5-119">То есть, перед передачей данных в эксперимент необходимо позаботиться о трудностях, например строках без кавычек.</span><span class="sxs-lookup"><span data-stu-id="3d0d5-119">That is, you'll want to take care of issues such as unquoted strings before you upload the data into your experiment.</span></span>

<span data-ttu-id="3d0d5-120">Тем не менее в студии машинного обучения Microsoft Azure доступны модули, позволяющие выполнить некоторую обработку данных в рамках вашего эксперимента.</span><span class="sxs-lookup"><span data-stu-id="3d0d5-120">However, there are modules available in Machine Learning Studio that enable some manipulation of data within your experiment.</span></span> <span data-ttu-id="3d0d5-121">В зависимости от алгоритмов машинного обучения, которые вы будете использовать, необходимо решить, как будут обрабатываться структурные трудности в данных, например отсутствующие значения и разреженные данные, и существуют ли модули, которые могут здесь помочь.</span><span class="sxs-lookup"><span data-stu-id="3d0d5-121">Depending on the machine learning algorithms you'll be using, you may need to decide how you'll handle data structural issues such as missing values and sparse data, and there are modules that can help with that.</span></span> <span data-ttu-id="3d0d5-122">В разделе **Преобразование данных** палитры модулей найдите модули, которые выполняют такие функции.</span><span class="sxs-lookup"><span data-stu-id="3d0d5-122">Look in the **Data Transformation** section of the module palette for modules that perform these functions.</span></span>

<span data-ttu-id="3d0d5-123">В любой точке вашего эксперимента можно просмотреть или скачать данные, созданные модулем, щелкнув правой кнопкой мыши порт вывода.</span><span class="sxs-lookup"><span data-stu-id="3d0d5-123">At any point in your experiment you can view or download the data that's produced by a module by clicking the output port.</span></span> <span data-ttu-id="3d0d5-124">В зависимости от модуля могут быть доступны разные варианты скачивания или вы сможете просмотреть данные в веб-браузере в Студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="3d0d5-124">Depending on the module, there may be different download options available, or you may be able to visualize the data within your web browser in Machine Learning Studio.</span></span>

## <a name="data-formats-and-data-types-supported"></a><span data-ttu-id="3d0d5-125">Поддерживаемые форматы и типы данных</span><span class="sxs-lookup"><span data-stu-id="3d0d5-125">Data formats and data types supported</span></span>
<span data-ttu-id="3d0d5-126">В свой эксперимент можно импортировать значительное количество типов данных, в зависимости от того, какая система используется для импорта данных и каков источник этих данных:</span><span class="sxs-lookup"><span data-stu-id="3d0d5-126">You can import a number of data types into your experiment, depending on what mechanism you use to import data and where it's coming from:</span></span>

* <span data-ttu-id="3d0d5-127">Обычный текст (TXT)</span><span class="sxs-lookup"><span data-stu-id="3d0d5-127">Plain text (.txt)</span></span>
* <span data-ttu-id="3d0d5-128">Текст с разделителями-запятыми с заголовком (CSV) или без заголовка (NH.CSV)</span><span class="sxs-lookup"><span data-stu-id="3d0d5-128">Comma-separated values (CSV) with a header (.csv) or without (.nh.csv)</span></span>
* <span data-ttu-id="3d0d5-129">Текст с разделителями-табуляциями с заголовком (TSV) или без заголовка (NH.TSV)</span><span class="sxs-lookup"><span data-stu-id="3d0d5-129">Tab-separated values (TSV) with a header (.tsv) or without (.nh.tsv)</span></span>
* <span data-ttu-id="3d0d5-130">Файл Excel</span><span class="sxs-lookup"><span data-stu-id="3d0d5-130">Excel file</span></span>
* <span data-ttu-id="3d0d5-131">таблицу Azure;</span><span class="sxs-lookup"><span data-stu-id="3d0d5-131">Azure table</span></span>
* <span data-ttu-id="3d0d5-132">Таблица Hive</span><span class="sxs-lookup"><span data-stu-id="3d0d5-132">Hive table</span></span>
* <span data-ttu-id="3d0d5-133">Таблицы базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="3d0d5-133">SQL database table</span></span>
* <span data-ttu-id="3d0d5-134">Значения OData</span><span class="sxs-lookup"><span data-stu-id="3d0d5-134">OData values</span></span>
* <span data-ttu-id="3d0d5-135">данные SVMLight (SVMLIGHT) (подробнее о формате см. в [определении SVMLight](http://svmlight.joachims.org/));</span><span class="sxs-lookup"><span data-stu-id="3d0d5-135">SVMLight data (.svmlight) (see the [SVMLight definition](http://svmlight.joachims.org/) for format information)</span></span>
* <span data-ttu-id="3d0d5-136">данные в формате ARFF (подробнее о формате см. в [определении ARFF](http://weka.wikispaces.com/ARFF));</span><span class="sxs-lookup"><span data-stu-id="3d0d5-136">Attribute Relation File Format (ARFF) data (.arff) (see the [ARFF definition](http://weka.wikispaces.com/ARFF) for format information)</span></span>
* <span data-ttu-id="3d0d5-137">ZIP-файл (ZIP)</span><span class="sxs-lookup"><span data-stu-id="3d0d5-137">Zip file (.zip)</span></span>
* <span data-ttu-id="3d0d5-138">Файл объекта или рабочей области R (RData)</span><span class="sxs-lookup"><span data-stu-id="3d0d5-138">R object or workspace file (.RData)</span></span>

<span data-ttu-id="3d0d5-139">При импорте данных в содержащем метаданные формате (например ARFF) Студия машинного обучения Microsoft Azure использует эти метаданные для определения заголовка и типа данных каждого столбца.</span><span class="sxs-lookup"><span data-stu-id="3d0d5-139">If you import data in a format such as ARFF that includes metadata, Machine Learning Studio uses this metadata to define the heading and data type of each column.</span></span>

<span data-ttu-id="3d0d5-140">При импорте данных в формате, например, TSV или CSV, который не содержит этих метаданных, Студия машинного обучения Microsoft Azure при выборке данных пытается определить тип данных для каждого столбца.</span><span class="sxs-lookup"><span data-stu-id="3d0d5-140">If you import data such as TSV or CSV format that doesn't include this metadata, Machine Learning Studio infers the data type for each column by sampling the data.</span></span> <span data-ttu-id="3d0d5-141">Если данные не содержат заголовки столбцов, Студия машинного обучения Microsoft Azure использует имена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3d0d5-141">If the data also doesn't have column headings, Machine Learning Studio provides default names.</span></span>

<span data-ttu-id="3d0d5-142">Вы можете явно указать или изменить заголовки и типы данных для столбцов с помощью функции [изменения метаданных][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="3d0d5-142">You can explicitly specify or change the headings and data types for columns using the [Edit Metadata][edit-metadata].</span></span>

<span data-ttu-id="3d0d5-143">Студия машинного обучения распознает следующие **типы данных** :</span><span class="sxs-lookup"><span data-stu-id="3d0d5-143">The following **data types** are recognized by Machine Learning Studio:</span></span>

* <span data-ttu-id="3d0d5-144">Строка</span><span class="sxs-lookup"><span data-stu-id="3d0d5-144">String</span></span>
* <span data-ttu-id="3d0d5-145">Число</span><span class="sxs-lookup"><span data-stu-id="3d0d5-145">Integer</span></span>
* <span data-ttu-id="3d0d5-146">Double</span><span class="sxs-lookup"><span data-stu-id="3d0d5-146">Double</span></span>
* <span data-ttu-id="3d0d5-147">Логический</span><span class="sxs-lookup"><span data-stu-id="3d0d5-147">Boolean</span></span>
* <span data-ttu-id="3d0d5-148">DateTime</span><span class="sxs-lookup"><span data-stu-id="3d0d5-148">DateTime</span></span>
* <span data-ttu-id="3d0d5-149">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="3d0d5-149">TimeSpan</span></span>

<span data-ttu-id="3d0d5-150">Для передачи данных между модулями Студия машинного обучения Microsoft Azure использует внутренний тип данных, который называется ***Data Table***.</span><span class="sxs-lookup"><span data-stu-id="3d0d5-150">Machine Learning Studio uses an internal data type called ***Data Table*** to pass data between modules.</span></span> <span data-ttu-id="3d0d5-151">Данные можно явно преобразовать в формат Data Table с использованием модуля [Convert to Dataset][convert-to-dataset] (Преобразование в набор данных).</span><span class="sxs-lookup"><span data-stu-id="3d0d5-151">You can explicitly convert your data into Data Table format using the [Convert to Dataset][convert-to-dataset] module.</span></span>

<span data-ttu-id="3d0d5-152">Любой модуль, который принимает форматы, отличные от Data Table, перед передачей данных в следующий модуль преобразует данные в формат Data Table без вмешательства пользователя.</span><span class="sxs-lookup"><span data-stu-id="3d0d5-152">Any module that accepts formats other than Data Table will convert the data to Data Table silently before passing it to the next module.</span></span>

<span data-ttu-id="3d0d5-153">При необходимости можно преобразовать данные Data Table обратно в формат CSV, TSV, ARFF или SVMLight, используя другие модули преобразования.</span><span class="sxs-lookup"><span data-stu-id="3d0d5-153">If necessary, you can convert Data Table format back into CSV, TSV, ARFF, or SVMLight format using other conversion modules.</span></span>
<span data-ttu-id="3d0d5-154">Узнать о модулях, которые выполняют эти функции, можно узнать в разделе **Преобразование форматов данных** палитры модулей.</span><span class="sxs-lookup"><span data-stu-id="3d0d5-154">Look in the **Data Format Conversions** section of the module palette for modules that perform these functions.</span></span>

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
