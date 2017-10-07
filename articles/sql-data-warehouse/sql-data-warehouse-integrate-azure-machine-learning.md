---
title: "aaaUse машинного обучения Azure с хранилищем данных SQL | Документы Microsoft"
description: "Учебник по использованию машинного обучения Azure с хранилищем данных SQL Azure для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: 
ms.assetid: ac6bc731-6add-47a9-b3fe-68996e656f4d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: fdfe8c936d2bb7a02163a0bbf6435e1ebd518d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a><span data-ttu-id="a22de-103">Использование машинного обучения Azure с хранилищем данных SQL</span><span class="sxs-lookup"><span data-stu-id="a22de-103">Use Azure Machine Learning with SQL Data Warehouse</span></span>
<span data-ttu-id="a22de-104">Машинное обучение Azure является службой полностью управляемая прогнозирующего анализа, можно использовать toocreate прогнозных моделей для данных в хранилище данных SQL, а затем опубликовать как готовые к использованию веб-службы.</span><span class="sxs-lookup"><span data-stu-id="a22de-104">Azure Machine Learning is a fully managed predictive analytics service that you can use toocreate predictive models against your data in SQL Data Warehouse, and then publish as ready-to-consume web services.</span></span> <span data-ttu-id="a22de-105">Вы можете основы hello прогнозирующего анализа и машинное обучение, считывая [tooMachine введение обучения в Azure][Introduction tooMachine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="a22de-105">You can learn hello basics of predictive analytics and machine learning by reading [Introduction tooMachine Learning on Azure][Introduction tooMachine Learning on Azure].</span></span>  <span data-ttu-id="a22de-106">Затем рассказывается, как toocreate, обучение, оценки и тестирования модели машинного обучения с помощью hello [создать эксперимент учебника][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="a22de-106">You can then learn how toocreate, train, score and test a machine learning model using hello [Create experiment tutorial][Create experiment tutorial].</span></span>

<span data-ttu-id="a22de-107">В этой статье вы узнаете, как после с помощью hello hello toodo [студии машинного обучения Azure][Azure Machine Learning Studio]:</span><span class="sxs-lookup"><span data-stu-id="a22de-107">In this article, you will learn how toodo hello following using hello [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span></span>

* <span data-ttu-id="a22de-108">Чтение данных из вашей базы данных toocreate, обучения и оценки прогнозной модели</span><span class="sxs-lookup"><span data-stu-id="a22de-108">Read data from your database toocreate, train and score a predictive model</span></span>
* <span data-ttu-id="a22de-109">Запись tooyour базы данных</span><span class="sxs-lookup"><span data-stu-id="a22de-109">Write data tooyour database</span></span>

## <a name="read-data-from-sql-data-warehouse"></a><span data-ttu-id="a22de-110">Чтение данных из хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="a22de-110">Read data from SQL Data Warehouse</span></span>
<span data-ttu-id="a22de-111">Мы будет считывать данные из таблицы Product базы данных AdventureWorksDW hello.</span><span class="sxs-lookup"><span data-stu-id="a22de-111">We will read data from Product table in hello AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="a22de-112">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="a22de-112">Step 1</span></span>
<span data-ttu-id="a22de-113">Запустите новый эксперимент, установив + NEW hello нижней части окна студии машинного обучения hello выберите ЭКСПЕРИМЕНТА, а затем выберите пустой поэкспериментировать.</span><span class="sxs-lookup"><span data-stu-id="a22de-113">Start a new experiment by clicking +NEW at hello bottom of hello Machine Learning Studio window, select EXPERIMENT, and then select Blank Experiment.</span></span> <span data-ttu-id="a22de-114">По умолчанию выберите hello поэкспериментировать имя hello верхней части холста hello и переименуйте его toosomething осмысленное, например, велосипед цена прогноза.</span><span class="sxs-lookup"><span data-stu-id="a22de-114">Select hello default experiment name at hello top of hello canvas and rename it toosomething meaningful, for example, Bicycle price prediction.</span></span>

### <a name="step-2"></a><span data-ttu-id="a22de-115">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="a22de-115">Step 2</span></span>
<span data-ttu-id="a22de-116">Найдите модуль считывания hello в палитре hello наборов данных и модули hello левой стороны холст эксперимента hello.</span><span class="sxs-lookup"><span data-stu-id="a22de-116">Look for hello Reader module in hello palette of datasets and modules on hello left of hello experiment canvas.</span></span> <span data-ttu-id="a22de-117">Перетащите холст эксперимента toohello модуль hello.</span><span class="sxs-lookup"><span data-stu-id="a22de-117">Drag hello module toohello experiment canvas.</span></span>
![][drag_reader]

### <a name="step-3"></a><span data-ttu-id="a22de-118">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="a22de-118">Step 3</span></span>
<span data-ttu-id="a22de-119">Выберите модуль чтения hello и заполните hello панели «Свойства».</span><span class="sxs-lookup"><span data-stu-id="a22de-119">Select hello Reader module and fill out hello properties pane.</span></span>

1. <span data-ttu-id="a22de-120">Выберите базу данных SQL Azure в качестве hello источника данных.</span><span class="sxs-lookup"><span data-stu-id="a22de-120">Select Azure SQL Database as hello Data Source.</span></span>
2. <span data-ttu-id="a22de-121">Имя сервера базы данных: имя сервера типа hello.</span><span class="sxs-lookup"><span data-stu-id="a22de-121">Database server name: Type hello server name.</span></span> <span data-ttu-id="a22de-122">Можно использовать hello [портал Azure] [ Azure portal] toofind это.</span><span class="sxs-lookup"><span data-stu-id="a22de-122">You can use hello [Azure portal][Azure portal] toofind this.</span></span>

![][server_name]

1. <span data-ttu-id="a22de-123">Имя базы данных: имя типа hello базы данных на сервере hello, только что указали.</span><span class="sxs-lookup"><span data-stu-id="a22de-123">Database name: Type hello name of a database on hello server you just specified.</span></span>
2. <span data-ttu-id="a22de-124">Имя учетной записи пользователя сервера: Введите hello имя пользователя учетной записи, которая имеет разрешения на доступ к базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="a22de-124">Server user account name:  Type hello user name of an account that has access permissions for hello database.</span></span>
3. <span data-ttu-id="a22de-125">Пароль учетной записи пользователя сервера: указать пароль hello для hello указанную учетную запись пользователя.</span><span class="sxs-lookup"><span data-stu-id="a22de-125">Server user account password: Provide hello password for hello specified user account.</span></span>
4. <span data-ttu-id="a22de-126">Принимать любой сертификат сервера: используйте этот параметр (менее безопасный), если требуется, чтобы tooskip Просмотр сертификата сайта hello перед чтением данных.</span><span class="sxs-lookup"><span data-stu-id="a22de-126">Accept any server certificate: Use this option (less secure) if you want tooskip reviewing hello site certificate before you read your data.</span></span>
5. <span data-ttu-id="a22de-127">Запрос базы данных: Введите инструкцию SQL, описывающий hello данные tooread.</span><span class="sxs-lookup"><span data-stu-id="a22de-127">Database query: Enter a SQL statement that describes hello data you want tooread.</span></span> <span data-ttu-id="a22de-128">В этом случае будет считывать данные из таблицы продукта, с помощью приветствия при следующем запросе.</span><span class="sxs-lookup"><span data-stu-id="a22de-128">In this case, we will read data from Product table using hello following query.</span></span>

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a><span data-ttu-id="a22de-129">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="a22de-129">Step 4</span></span>
1. <span data-ttu-id="a22de-130">Запустите эксперимент hello командой выполнить под холст эксперимента hello.</span><span class="sxs-lookup"><span data-stu-id="a22de-130">Run hello experiment by clicking Run under hello experiment canvas.</span></span>
2. <span data-ttu-id="a22de-131">По завершении эксперимента hello модуль считывания hello будет tooindicate Зеленый флажок, который успешно завершена.</span><span class="sxs-lookup"><span data-stu-id="a22de-131">When hello experiment finishes, hello Reader module will have a green check mark tooindicate that it has completed successfully.</span></span> <span data-ttu-id="a22de-132">Обратите внимание также hello завершен текущий статус в правом верхнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="a22de-132">Notice also hello Finished running status in hello upper-right corner.</span></span>

![][run]

1. <span data-ttu-id="a22de-133">toosee hello импортированных данных щелкните порт вывода hello внизу hello автомобиль hello набора данных и выберите визуализировать.</span><span class="sxs-lookup"><span data-stu-id="a22de-133">toosee hello imported data, click hello output port at hello bottom of hello automobile dataset and select Visualize.</span></span>

## <a name="create-train-and-score-a-model"></a><span data-ttu-id="a22de-134">Создание, обучение и оценка модели</span><span class="sxs-lookup"><span data-stu-id="a22de-134">Create, train and score a model</span></span>
<span data-ttu-id="a22de-135">Теперь этот набор данных можно использовать для выполнения следующих задач.</span><span class="sxs-lookup"><span data-stu-id="a22de-135">Now you can use this dataset to:</span></span>

* <span data-ttu-id="a22de-136">Создание модели: обработка данных и задание параметров</span><span class="sxs-lookup"><span data-stu-id="a22de-136">Create a Model: Process data and define features</span></span>
* <span data-ttu-id="a22de-137">Обучение модели hello: Выбор и применение алгоритма обучения</span><span class="sxs-lookup"><span data-stu-id="a22de-137">Train hello model: Choose and apply a learning algorithm</span></span>
* <span data-ttu-id="a22de-138">Оценка и тестирования hello модели: прогнозирования новая цена велосипеда</span><span class="sxs-lookup"><span data-stu-id="a22de-138">Score and test hello model: Predict new bicycle price</span></span>

![][model]

<span data-ttu-id="a22de-139">Дополнительные о toocreate, обучение, оценки и тестирования машинного обучения модели используйте hello toolearn [создать эксперимент учебника][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="a22de-139">toolearn more about how toocreate, train, score and test a machine learning model use hello [Create experiment tutorial][Create experiment tutorial].</span></span>

## <a name="write-data-tooazure-sql-data-warehouse"></a><span data-ttu-id="a22de-140">Запись данных tooAzure хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="a22de-140">Write data tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="a22de-141">Мы напишем hello результирующий набор tooProductPriceForecast таблицы базы данных AdventureWorksDW hello.</span><span class="sxs-lookup"><span data-stu-id="a22de-141">We will write hello result set tooProductPriceForecast table in hello AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="a22de-142">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="a22de-142">Step 1</span></span>
<span data-ttu-id="a22de-143">Найдите модуль записи hello в палитре hello наборов данных и модули hello левой стороны холст эксперимента hello.</span><span class="sxs-lookup"><span data-stu-id="a22de-143">Look for hello Writer module in hello palette of datasets and modules on hello left of hello experiment canvas.</span></span> <span data-ttu-id="a22de-144">Перетащите холст эксперимента toohello модуль hello.</span><span class="sxs-lookup"><span data-stu-id="a22de-144">Drag hello module toohello experiment canvas.</span></span>

![][drag_writer]

### <a name="step-2"></a><span data-ttu-id="a22de-145">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="a22de-145">Step 2</span></span>
<span data-ttu-id="a22de-146">Выберите модуль записи hello и заполните hello панели «Свойства».</span><span class="sxs-lookup"><span data-stu-id="a22de-146">Select hello Writer module and fill out hello properties pane.</span></span>

1. <span data-ttu-id="a22de-147">Выберите базы данных SQL Azure в качестве назначения данных hello.</span><span class="sxs-lookup"><span data-stu-id="a22de-147">Select Azure SQL Database as hello Data Destination.</span></span>
2. <span data-ttu-id="a22de-148">Имя сервера базы данных: имя сервера типа hello.</span><span class="sxs-lookup"><span data-stu-id="a22de-148">Database server name: Type hello server name.</span></span> <span data-ttu-id="a22de-149">Можно использовать hello [портал Azure] [ Azure portal] toofind это.</span><span class="sxs-lookup"><span data-stu-id="a22de-149">You can use hello [Azure portal][Azure portal] toofind this.</span></span>
3. <span data-ttu-id="a22de-150">Имя базы данных: имя типа hello базы данных на сервере hello, только что указали.</span><span class="sxs-lookup"><span data-stu-id="a22de-150">Database name: Type hello name of a database on hello server you just specified.</span></span>
4. <span data-ttu-id="a22de-151">Имя учетной записи пользователя сервера: Введите hello имя пользователя учетной записи, которая имеет разрешения на запись для базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="a22de-151">Server user account name:  Type hello user name of an account that has write permissions for hello database.</span></span>
5. <span data-ttu-id="a22de-152">Пароль учетной записи пользователя сервера: указать пароль hello для hello указанную учетную запись пользователя.</span><span class="sxs-lookup"><span data-stu-id="a22de-152">Server user account password: Provide hello password for hello specified user account.</span></span>
6. <span data-ttu-id="a22de-153">Принимать любой сертификат сервера (небезопасно): выберите этот параметр, если вы не хотите tooview hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="a22de-153">Accept any server certificate (insecure): Select this option if you don’t want tooview hello certificate.</span></span>
7. <span data-ttu-id="a22de-154">Список с разделителями запятыми столбцов toobe сохранен: предоставлять список столбцов набора данных или результат hello, которые должны toooutput.</span><span class="sxs-lookup"><span data-stu-id="a22de-154">Comma-separated list of columns toobe saved: Provide a list of hello dataset or result columns that you want toooutput.</span></span>
8. <span data-ttu-id="a22de-155">Имя таблицы данных: укажите имя hello hello данных таблицы.</span><span class="sxs-lookup"><span data-stu-id="a22de-155">Data table name: Specify hello name of hello data table.</span></span>
9. <span data-ttu-id="a22de-156">Список с разделителями запятыми столбцов datatable: Укажите имена toouse hello столбец в новой таблице hello.</span><span class="sxs-lookup"><span data-stu-id="a22de-156">Comma-separated list of datatable columns:  Specify hello column names toouse in hello new table.</span></span> <span data-ttu-id="a22de-157">Hello имена столбцов может отличаться от hello из них в hello исходный набор данных, но необходимо перечислить hello одинаковое количество столбцов здесь, определяемый для hello выходной таблицы.</span><span class="sxs-lookup"><span data-stu-id="a22de-157">hello column names can be different from hello ones in hello source dataset, but you must list hello same number of columns here that you define for hello output table.</span></span>
10. <span data-ttu-id="a22de-158">Количество строк, записываемых за одну операцию SQL Azure: можно настроить hello количество строк, которые записываются tooa базы данных SQL за одну операцию.</span><span class="sxs-lookup"><span data-stu-id="a22de-158">Number of rows written per SQL Azure operation: You can configure hello number of rows that are written tooa SQL database in one operation.</span></span>

![][writer_properties]

### <a name="step-3"></a><span data-ttu-id="a22de-159">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="a22de-159">Step 3</span></span>
1. <span data-ttu-id="a22de-160">Запустите эксперимент hello командой выполнить под холст эксперимента hello.</span><span class="sxs-lookup"><span data-stu-id="a22de-160">Run hello experiment by clicking Run under hello experiment canvas.</span></span>
2. <span data-ttu-id="a22de-161">По завершении эксперимента hello всех модулей будет tooindicate Зеленый флажок, который успешно завершена.</span><span class="sxs-lookup"><span data-stu-id="a22de-161">When hello experiment finishes, all modules will have a green check mark tooindicate that they completed successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a22de-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a22de-162">Next steps</span></span>
<span data-ttu-id="a22de-163">Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="a22de-163">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[drag_reader]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-reader.png
[server_name]: ./media/sql-data-warehouse-integrate-azure-machine-learning/dw-server-name.png
[reader_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-reader-properties.png
[run]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-finished-running.png
[model]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-create-train-score-model.png
[drag_writer]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-writer.png
[writer_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-writer-properties.png

<!--Article references-->

[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Create experiment tutorial]: https://azure.microsoft.com/documentation/articles/machine-learning-create-experiment/
[Introduction toomachine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
