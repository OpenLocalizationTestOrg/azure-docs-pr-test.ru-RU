---
title: "Шаг 2. Отправка данных в эксперимент машинного обучения | Документация Майкрософт"
description: "Второй этап разработки прогнозного решения: передача сохраненных общедоступных данных в Студию машинного обучения Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 9f4bc52e-9919-4dea-90ea-5cf7cc506d85
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: c2ab5f5252e1ea1ec51f6c3bd489826c70ff011c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a><span data-ttu-id="ce998-103">Шаг 2 пошагового руководства: отправка существующих данных в эксперимент Машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="ce998-103">Walkthrough Step 2: Upload existing data into an Azure Machine Learning experiment</span></span>
<span data-ttu-id="ce998-104">Это второй этап из пошагового руководства [Разработка решения для прогнозной аналитики в службе машинного обучения Azure](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="ce998-104">This is the second step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="ce998-105">Создание рабочей области машинного обучения</span><span class="sxs-lookup"><span data-stu-id="ce998-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. <span data-ttu-id="ce998-106">**Отправка существующих данных**</span><span class="sxs-lookup"><span data-stu-id="ce998-106">**Upload existing data**</span></span>
3. [<span data-ttu-id="ce998-107">Создание нового эксперимента</span><span class="sxs-lookup"><span data-stu-id="ce998-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="ce998-108">Обучение и анализ моделей</span><span class="sxs-lookup"><span data-stu-id="ce998-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="ce998-109">Развертывание веб-службы</span><span class="sxs-lookup"><span data-stu-id="ce998-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="ce998-110">Доступ к веб-службе</span><span class="sxs-lookup"><span data-stu-id="ce998-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="ce998-111">Для разработки модели прогнозирования кредитного риска потребуются данные, которые можно использовать для обучения и последующей проверки модели.</span><span class="sxs-lookup"><span data-stu-id="ce998-111">To develop a predictive model for credit risk, we need data that we can use to train and then test the model.</span></span> <span data-ttu-id="ce998-112">В данном случае будет использоваться набор данных UCI Statlog (German Credit Data) Data Set из репозитория машинного обучения UC Irvine Machine Learning Repository.</span><span class="sxs-lookup"><span data-stu-id="ce998-112">For this walkthrough, we'll use the "UCI Statlog (German Credit Data) Data Set" from the UC Irvine Machine Learning repository.</span></span> <span data-ttu-id="ce998-113">Его можно найти по следующей ссылке: </span><span class="sxs-lookup"><span data-stu-id="ce998-113">You can find it here:</span></span>  
<span data-ttu-id="ce998-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a>.</span><span class="sxs-lookup"><span data-stu-id="ce998-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span></span>

<span data-ttu-id="ce998-115">Будет использоваться файл с именем **german.data**.</span><span class="sxs-lookup"><span data-stu-id="ce998-115">We'll use the file named **german.data**.</span></span> <span data-ttu-id="ce998-116">Загрузите этот файл на свой жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="ce998-116">Download this file to your local hard drive.</span></span>  

<span data-ttu-id="ce998-117">Набор данных **german.data** содержит строки из 20 переменных для 1000 претендентов на получение кредита.</span><span class="sxs-lookup"><span data-stu-id="ce998-117">The **german.data** dataset contains rows of 20 variables for 1000 past applicants for credit.</span></span> <span data-ttu-id="ce998-118">Эти 20 переменных представляют набор свойств набора данных (*характеристический вектор*), обеспечивающих определяющие характеристики каждого претендента на кредит.</span><span class="sxs-lookup"><span data-stu-id="ce998-118">These 20 variables represent the dataset's set of features (the *feature vector*), which provides identifying characteristics for each credit applicant.</span></span> <span data-ttu-id="ce998-119">Дополнительный столбец в каждой строке представляет расчетный кредитный риск претендента, причем 700 претендентов идентифицированы с низким уровнем кредитного риска, а 300 — с высоким уровнем риска.</span><span class="sxs-lookup"><span data-stu-id="ce998-119">An additional column in each row represents the applicant's calculated credit risk, with 700 applicants identified as a low credit risk and 300 as a high risk.</span></span>

<span data-ttu-id="ce998-120">На веб-сайте UCI представлено описание атрибутов вектора свойств для этих данных.</span><span class="sxs-lookup"><span data-stu-id="ce998-120">The UCI website provides a description of the attributes of the feature vector for this data.</span></span> <span data-ttu-id="ce998-121">Сюда входят финансовые сведения, кредитная история, занятость и личные сведения.</span><span class="sxs-lookup"><span data-stu-id="ce998-121">This includes financial information, credit history, employment status, and personal information.</span></span> <span data-ttu-id="ce998-122">Для каждого претендента приведен двоичный рейтинг, указывающий низкий или высокий кредитный риск.</span><span class="sxs-lookup"><span data-stu-id="ce998-122">For each applicant, a binary rating has been given indicating whether they are a low or high credit risk.</span></span> 

<span data-ttu-id="ce998-123">Эти данные будут использоваться для обучения модели прогнозирующей аналитики.</span><span class="sxs-lookup"><span data-stu-id="ce998-123">We'll use this data to train a predictive analytics model.</span></span> <span data-ttu-id="ce998-124">По завершении наша модель должна уметь принимать вектор свойств для новых претендентов и прогнозировать для них степень кредитного риска.</span><span class="sxs-lookup"><span data-stu-id="ce998-124">When we're done, our model should be able to accept a feature vector for a new individual and predict whether he or she is a low or high credit risk.</span></span>  

<span data-ttu-id="ce998-125">Есть один интересный момент.</span><span class="sxs-lookup"><span data-stu-id="ce998-125">Here's an interesting twist.</span></span> <span data-ttu-id="ce998-126">В описании набора данных на веб-сайте UCI упоминается, какой ценой обходится ошибка классификации кредитного риска человека.</span><span class="sxs-lookup"><span data-stu-id="ce998-126">The description of the dataset on the UCI website mentions what it costs if we misclassify a person's credit risk.</span></span>
<span data-ttu-id="ce998-127">Если модель прогнозирует высокий кредитный риск для тех, у кого он на самом деле низкий, это означает, что модель допустила ошибку классификации.</span><span class="sxs-lookup"><span data-stu-id="ce998-127">If the model predicts a high credit risk for someone who is actually a low credit risk, the model has made a misclassification.</span></span>
<span data-ttu-id="ce998-128">Но для финансового учреждения в пять раз дороже обходится обратная ошибка классификации: когда модель прогнозирует низкий кредитный риск для тех, у кого он на самом деле высокий.</span><span class="sxs-lookup"><span data-stu-id="ce998-128">But the reverse misclassification is five times more costly to the financial institution: if the model predicts a low credit risk for someone who is actually a high credit risk.</span></span>

<span data-ttu-id="ce998-129">Поэтому необходимо обучить модель таким образом, чтобы стоимость ошибки классификации второго типа была в пять раз выше, чем прочих ошибок классификации.</span><span class="sxs-lookup"><span data-stu-id="ce998-129">So, we want to train our model so that the cost of this latter type of misclassification is five times higher than misclassifying the other way.</span></span>
<span data-ttu-id="ce998-130">Один простой способ сделать это при обучении модели в нашем эксперименте заключается в том, чтобы 5 раз повторять записи, представляющие претендента с высоким кредитным риском.</span><span class="sxs-lookup"><span data-stu-id="ce998-130">One simple way to do this when training the model in our experiment is by duplicating (five times) those entries that represent someone with a high credit risk.</span></span> <span data-ttu-id="ce998-131">Если модель ошибочно отнесет к категории низкого кредитного риска кого-либо, чей кредитный риск на самом деле высокий, то модель допустит эту ошибку классификации пять раз, по одному разу для каждой повторяющейся записи.</span><span class="sxs-lookup"><span data-stu-id="ce998-131">Then, if the model misclassifies someone as a low credit risk when they're actually a high risk, the model does that same misclassification five times, once for each duplicate.</span></span> <span data-ttu-id="ce998-132">Это увеличит стоимость ошибки в результатах подготовки.</span><span class="sxs-lookup"><span data-stu-id="ce998-132">This will increase the cost of this error in the training results.</span></span>


## <a name="convert-the-dataset-format"></a><span data-ttu-id="ce998-133">Преобразование формата набора данных</span><span class="sxs-lookup"><span data-stu-id="ce998-133">Convert the dataset format</span></span>
<span data-ttu-id="ce998-134">В исходном наборе данных используется формат с разделителями-пробелами.</span><span class="sxs-lookup"><span data-stu-id="ce998-134">The original dataset uses a blank-separated format.</span></span> <span data-ttu-id="ce998-135">Студия машинного обучения лучше работает с файлами, в которых используются разделители-запятые (CSV-файлами), поэтому мы преобразуем набор данных, заменив пробелы запятыми.</span><span class="sxs-lookup"><span data-stu-id="ce998-135">Machine Learning Studio works better with a comma-separated value (CSV) file, so we'll convert the dataset by replacing spaces with commas.</span></span>  

<span data-ttu-id="ce998-136">Преобразовать эти данные можно разными способами.</span><span class="sxs-lookup"><span data-stu-id="ce998-136">There are many ways to convert this data.</span></span> <span data-ttu-id="ce998-137">Один из них — с помощью следующей команды Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ce998-137">One way is by using the following Windows PowerShell command:</span></span>   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

<span data-ttu-id="ce998-138">Другой — с помощью команды sed Unix:</span><span class="sxs-lookup"><span data-stu-id="ce998-138">Another way is by using the Unix sed command:</span></span>  

    sed 's/ /,/g' german.data > german.csv  

<span data-ttu-id="ce998-139">В любом случае мы создаем версию разделенных запятыми данных в файле **german.csv**, который мы будем использовать в эксперименте.</span><span class="sxs-lookup"><span data-stu-id="ce998-139">In either case, we have created a comma-separated version of the data in a file named **german.csv** that we can use in our experiment.</span></span>

## <a name="upload-the-dataset-to-machine-learning-studio"></a><span data-ttu-id="ce998-140">Передача набора данных в Студию машинного обучения</span><span class="sxs-lookup"><span data-stu-id="ce998-140">Upload the dataset to Machine Learning Studio</span></span>
<span data-ttu-id="ce998-141">После преобразования данных в формат CSV необходимо отправить их в Студию машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="ce998-141">Once the data has been converted to CSV format, we need to upload it into Machine Learning Studio.</span></span> 

1. <span data-ttu-id="ce998-142">Откройте домашнюю страницу Студии машинного обучения ([https://studio.azureml.net/Home](https://studio.azureml.net)).</span><span class="sxs-lookup"><span data-stu-id="ce998-142">Open the Machine Learning Studio home page ([https://studio.azureml.net](https://studio.azureml.net)).</span></span> 

2. <span data-ttu-id="ce998-143">В ![меню][1] в верхнем левом углу окна щелкните **Машинное обучение Azure**, **Студия** и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="ce998-143">Click the menu ![Menu][1] in the upper-left corner of the window, click **Azure Machine Learning**, select **Studio**, and sign in.</span></span>

3. <span data-ttu-id="ce998-144">В нижней части окна щелкните **+СОЗДАТЬ** .</span><span class="sxs-lookup"><span data-stu-id="ce998-144">Click **+NEW** at the bottom of the window.</span></span>

4. <span data-ttu-id="ce998-145">Выберите **НАБОР ДАННЫХ**.</span><span class="sxs-lookup"><span data-stu-id="ce998-145">Select **DATASET**.</span></span>

5. <span data-ttu-id="ce998-146">Выберите **ИЗ ЛОКАЛЬНОГО ФАЙЛА**.</span><span class="sxs-lookup"><span data-stu-id="ce998-146">Select **FROM LOCAL FILE**.</span></span>

    ![Добавление набора данных из локального файла][2]

6. <span data-ttu-id="ce998-148">В диалоговом окне **Upload a new dataset** (Отправка нового набора данных) нажмите кнопку **Обзор** и найдите созданный ранее файл **german.csv**.</span><span class="sxs-lookup"><span data-stu-id="ce998-148">In the **Upload a new dataset** dialog, click **Browse** and find the **german.csv** file you created.</span></span>

7. <span data-ttu-id="ce998-149">Введите имя для набора данных.</span><span class="sxs-lookup"><span data-stu-id="ce998-149">Enter a name for the dataset.</span></span> <span data-ttu-id="ce998-150">В этом пошаговом руководстве назовем его UCI German Credit Card Data.</span><span class="sxs-lookup"><span data-stu-id="ce998-150">For this walkthrough, call it "UCI German Credit Card Data".</span></span>

8. <span data-ttu-id="ce998-151">Для типа данных выберите **Универсальный CSV-файл без заголовка (.nh.csv)**.</span><span class="sxs-lookup"><span data-stu-id="ce998-151">For data type, select **Generic CSV File With no header (.nh.csv)**.</span></span>

9. <span data-ttu-id="ce998-152">При желании добавьте описание.</span><span class="sxs-lookup"><span data-stu-id="ce998-152">Add a description if you’d like.</span></span>

10. <span data-ttu-id="ce998-153">Нажмите кнопку с флажком **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ce998-153">Click the **OK** check mark.</span></span>  

    ![Передача набора данных][3]

<span data-ttu-id="ce998-155">Данные будут отправлены в модуль набора данных, который можно использовать в эксперименте.</span><span class="sxs-lookup"><span data-stu-id="ce998-155">This uploads the data into a dataset module that we can use in an experiment.</span></span>

<span data-ttu-id="ce998-156">Для управления отправленными в Студию наборами данных откройте вкладку **Наборы данных** в левой части окна Студии.</span><span class="sxs-lookup"><span data-stu-id="ce998-156">You can manage datasets that you've uploaded to Studio by clicking the **DATASETS** tab to the left of the Studio window.</span></span>

![Управление наборами данных][4]

<span data-ttu-id="ce998-158">Дополнительные сведения об импорте других типов данных в эксперимент см. в статье [Импорт обучающих данных в Студию машинного обучения Azure из разных источников данных](machine-learning-data-science-import-data.md).</span><span class="sxs-lookup"><span data-stu-id="ce998-158">For more information about importing other types of data into an experiment, see [Import your training data into Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span></span>

<span data-ttu-id="ce998-159">**Далее:[ создание эксперимента](machine-learning-walkthrough-3-create-new-experiment.md)**</span><span class="sxs-lookup"><span data-stu-id="ce998-159">**Next: [Create a new experiment](machine-learning-walkthrough-3-create-new-experiment.md)**</span></span>

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
