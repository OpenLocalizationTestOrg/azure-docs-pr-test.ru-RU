---
title: "Использование машинного обучения Azure с хранилищем данных SQL | Документация Майкрософт"
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
ms.openlocfilehash: c19860c6b5b1c15d1e29ddc67f9cf9ad4618725b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a><span data-ttu-id="4deb7-103">Использование машинного обучения Azure с хранилищем данных SQL</span><span class="sxs-lookup"><span data-stu-id="4deb7-103">Use Azure Machine Learning with SQL Data Warehouse</span></span>
<span data-ttu-id="4deb7-104">Машинное обучение Azure — это полностью управляемая служба прогнозной аналитики, которая позволяет создавать прогнозные модели с данными из хранилища данных SQL и публиковать их в виде готовых веб-служб.</span><span class="sxs-lookup"><span data-stu-id="4deb7-104">Azure Machine Learning is a fully managed predictive analytics service that you can use to create predictive models against your data in SQL Data Warehouse, and then publish as ready-to-consume web services.</span></span> <span data-ttu-id="4deb7-105">Ознакомиться с основами прогнозной аналитики и машинного обучения можно в статье [Введение в машинное обучение в облаке][Introduction to Machine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="4deb7-105">You can learn the basics of predictive analytics and machine learning by reading [Introduction to Machine Learning on Azure][Introduction to Machine Learning on Azure].</span></span>  <span data-ttu-id="4deb7-106">Сведения о создании, обучении, оценке и тестировании модели машинного обучения см. в статье [Руководство по машинному обучению. Создание первого эксперимента по обработке и анализу данных в Студии машинного обучения Azure][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="4deb7-106">You can then learn how to create, train, score and test a machine learning model using the [Create experiment tutorial][Create experiment tutorial].</span></span>

<span data-ttu-id="4deb7-107">В этой статье вы узнаете, как выполнить следующие задачи с помощью [Студии машинного обучения Microsoft Azure][Azure Machine Learning Studio]:</span><span class="sxs-lookup"><span data-stu-id="4deb7-107">In this article, you will learn how to do the following using the [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span></span>

* <span data-ttu-id="4deb7-108">Чтение данных из базы данных для создания, обучения и оценки прогнозной модели</span><span class="sxs-lookup"><span data-stu-id="4deb7-108">Read data from your database to create, train and score a predictive model</span></span>
* <span data-ttu-id="4deb7-109">Запись данных в базу данных</span><span class="sxs-lookup"><span data-stu-id="4deb7-109">Write data to your database</span></span>

## <a name="read-data-from-sql-data-warehouse"></a><span data-ttu-id="4deb7-110">Чтение данных из хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="4deb7-110">Read data from SQL Data Warehouse</span></span>
<span data-ttu-id="4deb7-111">Данные будут получены из таблицы Product в базе данных AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="4deb7-111">We will read data from Product table in the AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="4deb7-112">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="4deb7-112">Step 1</span></span>
<span data-ttu-id="4deb7-113">Запустите новый эксперимент, щелкнув "+СОЗДАТЬ" в нижней части окна студии машинного обучения, и выберите "ЭКСПЕРИМЕНТ", а затем "Пустой эксперимент".</span><span class="sxs-lookup"><span data-stu-id="4deb7-113">Start a new experiment by clicking +NEW at the bottom of the Machine Learning Studio window, select EXPERIMENT, and then select Blank Experiment.</span></span> <span data-ttu-id="4deb7-114">В верхней части области выберите имя эксперимента по умолчанию и присвойте ему понятное имя, например "Прогнозирование цен на велосипеды".</span><span class="sxs-lookup"><span data-stu-id="4deb7-114">Select the default experiment name at the top of the canvas and rename it to something meaningful, for example, Bicycle price prediction.</span></span>

### <a name="step-2"></a><span data-ttu-id="4deb7-115">Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="4deb7-115">Step 2</span></span>
<span data-ttu-id="4deb7-116">Найдите модуль чтения в палитре наборов данных и модулей слева от области эксперимента.</span><span class="sxs-lookup"><span data-stu-id="4deb7-116">Look for the Reader module in the palette of datasets and modules on the left of the experiment canvas.</span></span> <span data-ttu-id="4deb7-117">Перетащите модуль в область эксперимента.</span><span class="sxs-lookup"><span data-stu-id="4deb7-117">Drag the module to the experiment canvas.</span></span>
![][drag_reader]

### <a name="step-3"></a><span data-ttu-id="4deb7-118">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="4deb7-118">Step 3</span></span>
<span data-ttu-id="4deb7-119">Выберите модуль чтения и заполните область свойств.</span><span class="sxs-lookup"><span data-stu-id="4deb7-119">Select the Reader module and fill out the properties pane.</span></span>

1. <span data-ttu-id="4deb7-120">Выберите базу данных SQL Azure в качестве базы данных-источника.</span><span class="sxs-lookup"><span data-stu-id="4deb7-120">Select Azure SQL Database as the Data Source.</span></span>
2. <span data-ttu-id="4deb7-121">Имя сервера баз данных: введите имя сервера.</span><span class="sxs-lookup"><span data-stu-id="4deb7-121">Database server name: Type the server name.</span></span> <span data-ttu-id="4deb7-122">Эти сведения можно узнать на [портале Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="4deb7-122">You can use the [Azure portal][Azure portal] to find this.</span></span>

![][server_name]

1. <span data-ttu-id="4deb7-123">Имя базы данных: введите имя базы данных на сервере, который только что был указан.</span><span class="sxs-lookup"><span data-stu-id="4deb7-123">Database name: Type the name of a database on the server you just specified.</span></span>
2. <span data-ttu-id="4deb7-124">Имя учетной записи пользователя сервера: введите имя пользователя учетной записи, которая имеет разрешения на доступ к базе данных.</span><span class="sxs-lookup"><span data-stu-id="4deb7-124">Server user account name:  Type the user name of an account that has access permissions for the database.</span></span>
3. <span data-ttu-id="4deb7-125">Пароль учетной записи пользователя сервера: введите пароль для учетной записи указанного пользователя.</span><span class="sxs-lookup"><span data-stu-id="4deb7-125">Server user account password: Provide the password for the specified user account.</span></span>
4. <span data-ttu-id="4deb7-126">Принимать любые сертификаты сервера: используйте этот параметр (не рекомендуется), если вы хотите пропускать просмотр сертификата веб-сайта перед чтением данных.</span><span class="sxs-lookup"><span data-stu-id="4deb7-126">Accept any server certificate: Use this option (less secure) if you want to skip reviewing the site certificate before you read your data.</span></span>
5. <span data-ttu-id="4deb7-127">Запрос к базе данных: введите инструкцию SQL, описывающую данные, которые необходимо получить.</span><span class="sxs-lookup"><span data-stu-id="4deb7-127">Database query: Enter a SQL statement that describes the data you want to read.</span></span> <span data-ttu-id="4deb7-128">В этом случае данные будут считаны из таблицы Product с помощью следующего запроса.</span><span class="sxs-lookup"><span data-stu-id="4deb7-128">In this case, we will read data from Product table using the following query.</span></span>

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a><span data-ttu-id="4deb7-129">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="4deb7-129">Step 4</span></span>
1. <span data-ttu-id="4deb7-130">Запустите эксперимент, щелкнув "Пуск" под областью эксперимента.</span><span class="sxs-lookup"><span data-stu-id="4deb7-130">Run the experiment by clicking Run under the experiment canvas.</span></span>
2. <span data-ttu-id="4deb7-131">После выполнения эксперимента у модуля чтения должен появиться зеленый флажок, означающий успешное завершение.</span><span class="sxs-lookup"><span data-stu-id="4deb7-131">When the experiment finishes, the Reader module will have a green check mark to indicate that it has completed successfully.</span></span> <span data-ttu-id="4deb7-132">Обратите также внимание на состояние Работа завершена в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="4deb7-132">Notice also the Finished running status in the upper-right corner.</span></span>

![][run]

1. <span data-ttu-id="4deb7-133">Чтобы просмотреть импортированные данные, щелкните порт вывода в нижней части набора данных по автомобилям и выберите "Показать".</span><span class="sxs-lookup"><span data-stu-id="4deb7-133">To see the imported data, click the output port at the bottom of the automobile dataset and select Visualize.</span></span>

## <a name="create-train-and-score-a-model"></a><span data-ttu-id="4deb7-134">Создание, обучение и оценка модели</span><span class="sxs-lookup"><span data-stu-id="4deb7-134">Create, train and score a model</span></span>
<span data-ttu-id="4deb7-135">Теперь этот набор данных можно использовать для выполнения следующих задач.</span><span class="sxs-lookup"><span data-stu-id="4deb7-135">Now you can use this dataset to:</span></span>

* <span data-ttu-id="4deb7-136">Создание модели: обработка данных и задание параметров</span><span class="sxs-lookup"><span data-stu-id="4deb7-136">Create a Model: Process data and define features</span></span>
* <span data-ttu-id="4deb7-137">Обучение модели: выбор и применение алгоритма обучения</span><span class="sxs-lookup"><span data-stu-id="4deb7-137">Train the model: Choose and apply a learning algorithm</span></span>
* <span data-ttu-id="4deb7-138">Оценка и тестирование модели: прогнозирование новой цены велосипедов</span><span class="sxs-lookup"><span data-stu-id="4deb7-138">Score and test the model: Predict new bicycle price</span></span>

![][model]

<span data-ttu-id="4deb7-139">Сведения о создании, обучении, оценке и тестировании модели машинного обучения см. в статье [Руководство по машинному обучению. Создание первого эксперимента по обработке и анализу данных в Студии машинного обучения Azure][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="4deb7-139">To learn more about how to create, train, score and test a machine learning model use the [Create experiment tutorial][Create experiment tutorial].</span></span>

## <a name="write-data-to-azure-sql-data-warehouse"></a><span data-ttu-id="4deb7-140">Запись данных в хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="4deb7-140">Write data to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="4deb7-141">Мы запишем результирующий набор в таблицу ProductPriceForecast в базе данных AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="4deb7-141">We will write the result set to ProductPriceForecast table in the AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="4deb7-142">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="4deb7-142">Step 1</span></span>
<span data-ttu-id="4deb7-143">Найдите модуль записи в палитре наборов данных и модулей слева от области эксперимента.</span><span class="sxs-lookup"><span data-stu-id="4deb7-143">Look for the Writer module in the palette of datasets and modules on the left of the experiment canvas.</span></span> <span data-ttu-id="4deb7-144">Перетащите модуль в область эксперимента.</span><span class="sxs-lookup"><span data-stu-id="4deb7-144">Drag the module to the experiment canvas.</span></span>

![][drag_writer]

### <a name="step-2"></a><span data-ttu-id="4deb7-145">Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="4deb7-145">Step 2</span></span>
<span data-ttu-id="4deb7-146">Выберите модуль записи и заполните панель свойств.</span><span class="sxs-lookup"><span data-stu-id="4deb7-146">Select the Writer module and fill out the properties pane.</span></span>

1. <span data-ttu-id="4deb7-147">Выберите базу данных SQL Azure в качестве целевой базы данных.</span><span class="sxs-lookup"><span data-stu-id="4deb7-147">Select Azure SQL Database as the Data Destination.</span></span>
2. <span data-ttu-id="4deb7-148">Имя сервера баз данных: введите имя сервера.</span><span class="sxs-lookup"><span data-stu-id="4deb7-148">Database server name: Type the server name.</span></span> <span data-ttu-id="4deb7-149">Эти сведения можно узнать на [портале Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="4deb7-149">You can use the [Azure portal][Azure portal] to find this.</span></span>
3. <span data-ttu-id="4deb7-150">Имя базы данных: введите имя базы данных на сервере, который только что был указан.</span><span class="sxs-lookup"><span data-stu-id="4deb7-150">Database name: Type the name of a database on the server you just specified.</span></span>
4. <span data-ttu-id="4deb7-151">Имя учетной записи пользователя сервера: введите имя пользователя учетной записи, которая имеет разрешение на запись в базу данных.</span><span class="sxs-lookup"><span data-stu-id="4deb7-151">Server user account name:  Type the user name of an account that has write permissions for the database.</span></span>
5. <span data-ttu-id="4deb7-152">Пароль учетной записи пользователя сервера: введите пароль для учетной записи указанного пользователя.</span><span class="sxs-lookup"><span data-stu-id="4deb7-152">Server user account password: Provide the password for the specified user account.</span></span>
6. <span data-ttu-id="4deb7-153">Принимать любые сертификаты сервера (не рекомендуется): выберите этот параметр, чтобы не просматривать сертификаты.</span><span class="sxs-lookup"><span data-stu-id="4deb7-153">Accept any server certificate (insecure): Select this option if you don’t want to view the certificate.</span></span>
7. <span data-ttu-id="4deb7-154">Разделенный запятыми список столбцов, которые нужно сохранить: список набора данных или результирующие столбцы, которые нужно вывести.</span><span class="sxs-lookup"><span data-stu-id="4deb7-154">Comma-separated list of columns to be saved: Provide a list of the dataset or result columns that you want to output.</span></span>
8. <span data-ttu-id="4deb7-155">Имя таблицы данных: укажите имя таблицы данных.</span><span class="sxs-lookup"><span data-stu-id="4deb7-155">Data table name: Specify the name of the data table.</span></span>
9. <span data-ttu-id="4deb7-156">Разделенный запятыми список столбцов таблицы данных: укажите имя столбца для использования в новой таблице.</span><span class="sxs-lookup"><span data-stu-id="4deb7-156">Comma-separated list of datatable columns:  Specify the column names to use in the new table.</span></span> <span data-ttu-id="4deb7-157">Имена столбцов должны отличаться от имен столбцов в исходном наборе данных, однако следует использовать такое же количество столбцов, что и в таблице вывода.</span><span class="sxs-lookup"><span data-stu-id="4deb7-157">The column names can be different from the ones in the source dataset, but you must list the same number of columns here that you define for the output table.</span></span>
10. <span data-ttu-id="4deb7-158">Количество строк, записываемых в одной операции SQL Azure: можно настроить количество строк, которые записываются в базу данных SQL в одной операции.</span><span class="sxs-lookup"><span data-stu-id="4deb7-158">Number of rows written per SQL Azure operation: You can configure the number of rows that are written to a SQL database in one operation.</span></span>

![][writer_properties]

### <a name="step-3"></a><span data-ttu-id="4deb7-159">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="4deb7-159">Step 3</span></span>
1. <span data-ttu-id="4deb7-160">Запустите эксперимент, щелкнув "Пуск" под областью эксперимента.</span><span class="sxs-lookup"><span data-stu-id="4deb7-160">Run the experiment by clicking Run under the experiment canvas.</span></span>
2. <span data-ttu-id="4deb7-161">После выполнения эксперимента у всех модулей должен появиться зеленый флажок, означающий их успешное завершение.</span><span class="sxs-lookup"><span data-stu-id="4deb7-161">When the experiment finishes, all modules will have a green check mark to indicate that they completed successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4deb7-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4deb7-162">Next steps</span></span>
<span data-ttu-id="4deb7-163">Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="4deb7-163">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
[Introduction to machine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
