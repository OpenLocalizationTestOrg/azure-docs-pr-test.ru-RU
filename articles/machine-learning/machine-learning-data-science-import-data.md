---
title: "данные aaaImport в студию машинного обучения | Документы Microsoft"
description: "Как tooimport данные в студии машинного обучения Azure из различных источников данных. Узнайте, какие типы данных и форматы данных поддерживаются."
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
ms.openlocfilehash: 830dcdde9d43809900c520a41d6d94a65731ca3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a><span data-ttu-id="d1516-105">Импорт обучающих данных в Студию машинного обучения Azure из разных источников данных</span><span class="sxs-lookup"><span data-stu-id="d1516-105">Import your training data into Azure Machine Learning Studio from various data sources</span></span>
<span data-ttu-id="d1516-106">toouse данные в студии машинного обучения toodevelop и обучение решения для прогнозирующего анализа, вы можете:</span><span class="sxs-lookup"><span data-stu-id="d1516-106">toouse your own data in Machine Learning Studio toodevelop and train a predictive analytics solution, you can:</span></span> 

* <span data-ttu-id="d1516-107">передать данные из **локального файла** опережают время из toocreate на жестком диске модуля набору данных в рабочей области</span><span class="sxs-lookup"><span data-stu-id="d1516-107">upload data from a **local file** ahead of time from your hard drive toocreate a dataset module in your workspace</span></span>
* <span data-ttu-id="d1516-108">доступ к данным из одного из нескольких **источники данных в сети** запущенном эксперимента с помощью hello [импорта данных] [ import-data] модуля</span><span class="sxs-lookup"><span data-stu-id="d1516-108">access data from one of several **online data sources** while your experiment is running using hello [Import Data][import-data] module</span></span> 
* <span data-ttu-id="d1516-109">использовать данные из другого эксперимента машинного обучения Azure, сохраненные в виде **набора данных**;</span><span class="sxs-lookup"><span data-stu-id="d1516-109">use data from another Azure Machine learning **experiment** saved as a dataset</span></span>
* <span data-ttu-id="d1516-110">использовать данные из локальной **базы данных SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="d1516-110">use data from an on-premises **SQL Server database**</span></span>

<span data-ttu-id="d1516-111">Каждый из этих параметров описан в разделах hello в меню "hello" ниже.</span><span class="sxs-lookup"><span data-stu-id="d1516-111">Each of these options is described in one of hello topics on hello menu below.</span></span> <span data-ttu-id="d1516-112">Эти разделы описывают, каким образом tooimport данные из этих различных данных источники toouse в студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="d1516-112">These topics show you how tooimport data from these various data sources toouse in Machine Learning Studio.</span></span> 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> <span data-ttu-id="d1516-113">В Студии машинного обучения есть множество примеров наборов данных, которые можно использовать для обучающих данных.</span><span class="sxs-lookup"><span data-stu-id="d1516-113">There are a number of sample datasets available in Machine Learning Studio that you can use for training data.</span></span> <span data-ttu-id="d1516-114">Сведения об этом см. в разделе [использования наборов данных образец hello в студии машинного обучения Azure](machine-learning-use-sample-datasets.md)).</span><span class="sxs-lookup"><span data-stu-id="d1516-114">For information on these, see [Use hello sample datasets in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span></span>
> 
> 

<span data-ttu-id="d1516-115">В этом вводном разделе также рассматривается tooget данных готова для использования в студии машинного обучения и описывается, какие форматы данных и типы данных поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="d1516-115">This introductory topic also discusses how tooget data ready for use in Machine Learning Studio and describes which data formats and data types are supported.</span></span> 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a><span data-ttu-id="d1516-116">Подготовка данных для использования в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="d1516-116">Get data ready for use in Azure Machine Learning Studio</span></span>
<span data-ttu-id="d1516-117">Студия машинного обучения — спроектированный toowork с прямоугольный или табличные данные, такие как текстовые данные, с разделителями или структурированные данные из базы данных, хотя в некоторых случаях может использоваться непрямоугольные данных.</span><span class="sxs-lookup"><span data-stu-id="d1516-117">Machine Learning Studio is designed toowork with rectangular or tabular data, such as text data that's delimited or structured data from a database, though in some circumstances non-rectangular data may be used.</span></span>

<span data-ttu-id="d1516-118">Лучше, если данные относительно очищены.</span><span class="sxs-lookup"><span data-stu-id="d1516-118">It's best if your data is relatively clean.</span></span> <span data-ttu-id="d1516-119">То есть будет необходимо tootake заботиться о проблемах, например, не заключенные в кавычки строки перед отправкой данных hello в эксперименте.</span><span class="sxs-lookup"><span data-stu-id="d1516-119">That is, you'll want tootake care of issues such as unquoted strings before you upload hello data into your experiment.</span></span>

<span data-ttu-id="d1516-120">Тем не менее в студии машинного обучения Microsoft Azure доступны модули, позволяющие выполнить некоторую обработку данных в рамках вашего эксперимента.</span><span class="sxs-lookup"><span data-stu-id="d1516-120">However, there are modules available in Machine Learning Studio that enable some manipulation of data within your experiment.</span></span> <span data-ttu-id="d1516-121">В зависимости от того, вы будете использовать алгоритмов машинного обучения hello, может потребоваться toodecide как будет обрабатывать данные структурных проблем, таких как отсутствующие значения и разреженных данных, и существует модули, которые помогут в.</span><span class="sxs-lookup"><span data-stu-id="d1516-121">Depending on hello machine learning algorithms you'll be using, you may need toodecide how you'll handle data structural issues such as missing values and sparse data, and there are modules that can help with that.</span></span> <span data-ttu-id="d1516-122">Искать в hello **Data Transformation** части палитру hello модуль для модулей, которые выполняют эти функции.</span><span class="sxs-lookup"><span data-stu-id="d1516-122">Look in hello **Data Transformation** section of hello module palette for modules that perform these functions.</span></span>

<span data-ttu-id="d1516-123">В любой момент в эксперименте можно просмотреть или загрузить данные hello, произведенное модуля, щелкнув порт вывода hello.</span><span class="sxs-lookup"><span data-stu-id="d1516-123">At any point in your experiment you can view or download hello data that's produced by a module by clicking hello output port.</span></span> <span data-ttu-id="d1516-124">В зависимости от модуля hello может существовать варианты загрузки для различных или может toovisualize hello данных может быть веб-обозревателя в студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="d1516-124">Depending on hello module, there may be different download options available, or you may be able toovisualize hello data within your web browser in Machine Learning Studio.</span></span>

## <a name="data-formats-and-data-types-supported"></a><span data-ttu-id="d1516-125">Поддерживаемые форматы и типы данных</span><span class="sxs-lookup"><span data-stu-id="d1516-125">Data formats and data types supported</span></span>
<span data-ttu-id="d1516-126">Количество типов данных можно импортировать в свой эксперимент, в зависимости от того, какой механизм используется tooimport данных и где он поступает из:</span><span class="sxs-lookup"><span data-stu-id="d1516-126">You can import a number of data types into your experiment, depending on what mechanism you use tooimport data and where it's coming from:</span></span>

* <span data-ttu-id="d1516-127">Обычный текст (TXT)</span><span class="sxs-lookup"><span data-stu-id="d1516-127">Plain text (.txt)</span></span>
* <span data-ttu-id="d1516-128">Текст с разделителями-запятыми с заголовком (CSV) или без заголовка (NH.CSV)</span><span class="sxs-lookup"><span data-stu-id="d1516-128">Comma-separated values (CSV) with a header (.csv) or without (.nh.csv)</span></span>
* <span data-ttu-id="d1516-129">Текст с разделителями-табуляциями с заголовком (TSV) или без заголовка (NH.TSV)</span><span class="sxs-lookup"><span data-stu-id="d1516-129">Tab-separated values (TSV) with a header (.tsv) or without (.nh.tsv)</span></span>
* <span data-ttu-id="d1516-130">Файл Excel</span><span class="sxs-lookup"><span data-stu-id="d1516-130">Excel file</span></span>
* <span data-ttu-id="d1516-131">таблицу Azure;</span><span class="sxs-lookup"><span data-stu-id="d1516-131">Azure table</span></span>
* <span data-ttu-id="d1516-132">Таблица Hive</span><span class="sxs-lookup"><span data-stu-id="d1516-132">Hive table</span></span>
* <span data-ttu-id="d1516-133">Таблицы базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="d1516-133">SQL database table</span></span>
* <span data-ttu-id="d1516-134">Значения OData</span><span class="sxs-lookup"><span data-stu-id="d1516-134">OData values</span></span>
* <span data-ttu-id="d1516-135">SVMLight данных (.svmlight) (см. hello [SVMLight определение](http://svmlight.joachims.org/) сведения о формате)</span><span class="sxs-lookup"><span data-stu-id="d1516-135">SVMLight data (.svmlight) (see hello [SVMLight definition](http://svmlight.joachims.org/) for format information)</span></span>
* <span data-ttu-id="d1516-136">Формат файла связи (ARFF) данные (.arff) атрибутов (см. hello [ARFF определение](http://weka.wikispaces.com/ARFF) сведения о формате)</span><span class="sxs-lookup"><span data-stu-id="d1516-136">Attribute Relation File Format (ARFF) data (.arff) (see hello [ARFF definition](http://weka.wikispaces.com/ARFF) for format information)</span></span>
* <span data-ttu-id="d1516-137">ZIP-файл (ZIP)</span><span class="sxs-lookup"><span data-stu-id="d1516-137">Zip file (.zip)</span></span>
* <span data-ttu-id="d1516-138">Файл объекта или рабочей области R (RData)</span><span class="sxs-lookup"><span data-stu-id="d1516-138">R object or workspace file (.RData)</span></span>

<span data-ttu-id="d1516-139">При импорте данных в формате, например ARFF, содержащего метаданные студии машинного обучения использует этот заголовок hello toodefine метаданных и тип данных каждого столбца.</span><span class="sxs-lookup"><span data-stu-id="d1516-139">If you import data in a format such as ARFF that includes metadata, Machine Learning Studio uses this metadata toodefine hello heading and data type of each column.</span></span>

<span data-ttu-id="d1516-140">При импорте данных, таких как формат TSV или CSV, который не включает эти метаданные студии машинного обучения выводит тип данных hello для каждого столбца с помощью выборки данных hello.</span><span class="sxs-lookup"><span data-stu-id="d1516-140">If you import data such as TSV or CSV format that doesn't include this metadata, Machine Learning Studio infers hello data type for each column by sampling hello data.</span></span> <span data-ttu-id="d1516-141">Если hello данных не содержит заголовки столбцов, в студии машинного обучения предоставляет имена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d1516-141">If hello data also doesn't have column headings, Machine Learning Studio provides default names.</span></span>

<span data-ttu-id="d1516-142">Можно явным образом задать или изменить hello заголовки и типы данных для столбцов с помощью hello [редактирование метаданных][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="d1516-142">You can explicitly specify or change hello headings and data types for columns using hello [Edit Metadata][edit-metadata].</span></span>

<span data-ttu-id="d1516-143">следующие Hello **типы данных** распознаются студии машинного обучения:</span><span class="sxs-lookup"><span data-stu-id="d1516-143">hello following **data types** are recognized by Machine Learning Studio:</span></span>

* <span data-ttu-id="d1516-144">Строка</span><span class="sxs-lookup"><span data-stu-id="d1516-144">String</span></span>
* <span data-ttu-id="d1516-145">Число</span><span class="sxs-lookup"><span data-stu-id="d1516-145">Integer</span></span>
* <span data-ttu-id="d1516-146">Double</span><span class="sxs-lookup"><span data-stu-id="d1516-146">Double</span></span>
* <span data-ttu-id="d1516-147">Логический</span><span class="sxs-lookup"><span data-stu-id="d1516-147">Boolean</span></span>
* <span data-ttu-id="d1516-148">DateTime</span><span class="sxs-lookup"><span data-stu-id="d1516-148">DateTime</span></span>
* <span data-ttu-id="d1516-149">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="d1516-149">TimeSpan</span></span>

<span data-ttu-id="d1516-150">Студия машинного обучения использует тип внутренних данных называется ***таблицы данных*** toopass данных между модулями.</span><span class="sxs-lookup"><span data-stu-id="d1516-150">Machine Learning Studio uses an internal data type called ***Data Table*** toopass data between modules.</span></span> <span data-ttu-id="d1516-151">Можно явно преобразовать данные в формат таблицы данных с помощью hello [преобразовать tooDataset] [ convert-to-dataset] модуля.</span><span class="sxs-lookup"><span data-stu-id="d1516-151">You can explicitly convert your data into Data Table format using hello [Convert tooDataset][convert-to-dataset] module.</span></span>

<span data-ttu-id="d1516-152">Любой модуль, который принимает форматах, отличных от таблицы данных преобразует tooData hello данных таблицы без вмешательства пользователя перед его передачей toohello следующий модуль.</span><span class="sxs-lookup"><span data-stu-id="d1516-152">Any module that accepts formats other than Data Table will convert hello data tooData Table silently before passing it toohello next module.</span></span>

<span data-ttu-id="d1516-153">При необходимости можно преобразовать данные Data Table обратно в формат CSV, TSV, ARFF или SVMLight, используя другие модули преобразования.</span><span class="sxs-lookup"><span data-stu-id="d1516-153">If necessary, you can convert Data Table format back into CSV, TSV, ARFF, or SVMLight format using other conversion modules.</span></span>
<span data-ttu-id="d1516-154">Искать в hello **преобразования формата данных** части палитру hello модуль для модулей, которые выполняют эти функции.</span><span class="sxs-lookup"><span data-stu-id="d1516-154">Look in hello **Data Format Conversions** section of hello module palette for modules that perform these functions.</span></span>

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
