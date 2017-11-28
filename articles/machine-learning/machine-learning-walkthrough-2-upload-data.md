---
title: "Шаг 2. Отправка данных в эксперимент машинного обучения | Документация Майкрософт"
description: "Шаг 2 из hello разработка прогнозирующего решения Пошаговое руководство: отправка общих данных сохраняются в студии машинного обучения Azure."
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
ms.openlocfilehash: 0ea21dcca2d0934ed06508560cf85cf31b48ce6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a><span data-ttu-id="c262b-103">Шаг 2 пошагового руководства: отправка существующих данных в эксперимент Машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="c262b-103">Walkthrough Step 2: Upload existing data into an Azure Machine Learning experiment</span></span>
<span data-ttu-id="c262b-104">Это второй шаг hello hello пошагового руководства, [разрабатывать решения для прогнозирующего анализа в машинном обучении Azure](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="c262b-104">This is hello second step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="c262b-105">Создание рабочей области машинного обучения</span><span class="sxs-lookup"><span data-stu-id="c262b-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. <span data-ttu-id="c262b-106">**Отправка существующих данных**</span><span class="sxs-lookup"><span data-stu-id="c262b-106">**Upload existing data**</span></span>
3. [<span data-ttu-id="c262b-107">Создание нового эксперимента</span><span class="sxs-lookup"><span data-stu-id="c262b-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="c262b-108">Обучать и оценивать модели hello</span><span class="sxs-lookup"><span data-stu-id="c262b-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="c262b-109">Развернуть веб-службу hello</span><span class="sxs-lookup"><span data-stu-id="c262b-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="c262b-110">Доступ к веб-службе hello</span><span class="sxs-lookup"><span data-stu-id="c262b-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="c262b-111">toodevelop прогнозной модели для кредитного риска, мы должны данные, которые мы использовать tootrain и проверить модель hello.</span><span class="sxs-lookup"><span data-stu-id="c262b-111">toodevelop a predictive model for credit risk, we need data that we can use tootrain and then test hello model.</span></span> <span data-ttu-id="c262b-112">В данном пошаговом руководстве мы будем использовать hello «Набора данных UCI Statlog (немецкий данные кредитной)» из репозитория машинного обучения компании Irvine UC hello.</span><span class="sxs-lookup"><span data-stu-id="c262b-112">For this walkthrough, we'll use hello "UCI Statlog (German Credit Data) Data Set" from hello UC Irvine Machine Learning repository.</span></span> <span data-ttu-id="c262b-113">Его можно найти по следующей ссылке: </span><span class="sxs-lookup"><span data-stu-id="c262b-113">You can find it here:</span></span>  
<span data-ttu-id="c262b-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a>.</span><span class="sxs-lookup"><span data-stu-id="c262b-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span></span>

<span data-ttu-id="c262b-115">Мы будем использовать hello файл с именем **german.data**.</span><span class="sxs-lookup"><span data-stu-id="c262b-115">We'll use hello file named **german.data**.</span></span> <span data-ttu-id="c262b-116">Загрузите этот файл tooyour локальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="c262b-116">Download this file tooyour local hard drive.</span></span>  

<span data-ttu-id="c262b-117">Hello **german.data** набор данных содержит строки 20 переменных для 1000 последних кандидатов для кредита.</span><span class="sxs-lookup"><span data-stu-id="c262b-117">hello **german.data** dataset contains rows of 20 variables for 1000 past applicants for credit.</span></span> <span data-ttu-id="c262b-118">Эти 20 переменные представляют набор функций hello dataset (hello *вектора компонента*), который предоставляет идентифицирующие характеристики для каждого кандидата кредит.</span><span class="sxs-lookup"><span data-stu-id="c262b-118">These 20 variables represent hello dataset's set of features (hello *feature vector*), which provides identifying characteristics for each credit applicant.</span></span> <span data-ttu-id="c262b-119">Дополнительный столбец в каждой строке представляет hello кандидата вычисляемые кредитного риска, с 700 кандидатами, которые определены как низкий кредитного риска и 300 как высокого риска.</span><span class="sxs-lookup"><span data-stu-id="c262b-119">An additional column in each row represents hello applicant's calculated credit risk, with 700 applicants identified as a low credit risk and 300 as a high risk.</span></span>

<span data-ttu-id="c262b-120">веб-сайт UCI Hello содержит описание атрибутов hello hello вектора компонента для этих данных.</span><span class="sxs-lookup"><span data-stu-id="c262b-120">hello UCI website provides a description of hello attributes of hello feature vector for this data.</span></span> <span data-ttu-id="c262b-121">Сюда входят финансовые сведения, кредитная история, занятость и личные сведения.</span><span class="sxs-lookup"><span data-stu-id="c262b-121">This includes financial information, credit history, employment status, and personal information.</span></span> <span data-ttu-id="c262b-122">Для каждого претендента приведен двоичный рейтинг, указывающий низкий или высокий кредитный риск.</span><span class="sxs-lookup"><span data-stu-id="c262b-122">For each applicant, a binary rating has been given indicating whether they are a low or high credit risk.</span></span> 

<span data-ttu-id="c262b-123">Мы будем использовать этот tootrain данных модели прогнозирования.</span><span class="sxs-lookup"><span data-stu-id="c262b-123">We'll use this data tootrain a predictive analytics model.</span></span> <span data-ttu-id="c262b-124">Закончив, нашей модели необходимо будет tooaccept вектора компонента для нового пользователя и прогнозировать, является ли он или она высокое или низкое кредитного риска.</span><span class="sxs-lookup"><span data-stu-id="c262b-124">When we're done, our model should be able tooaccept a feature vector for a new individual and predict whether he or she is a low or high credit risk.</span></span>  

<span data-ttu-id="c262b-125">Есть один интересный момент.</span><span class="sxs-lookup"><span data-stu-id="c262b-125">Here's an interesting twist.</span></span> <span data-ttu-id="c262b-126">Здравствуйте описания hello набора данных на веб-сайте упоминания hello UCI расходы Если мы misclassify человека кредитного риска.</span><span class="sxs-lookup"><span data-stu-id="c262b-126">hello description of hello dataset on hello UCI website mentions what it costs if we misclassify a person's credit risk.</span></span>
<span data-ttu-id="c262b-127">Если hello модель прогнозирует высокой кредитного риска для тех, кто является фактически низкий кредитного риска, hello модели внес misclassification.</span><span class="sxs-lookup"><span data-stu-id="c262b-127">If hello model predicts a high credit risk for someone who is actually a low credit risk, hello model has made a misclassification.</span></span>
<span data-ttu-id="c262b-128">Пять раз больше toohello финансового учреждения, то обратная misclassification hello: Если hello модель прогнозирует низкий кредитного риска для тех, кто является фактически высокой кредитного риска.</span><span class="sxs-lookup"><span data-stu-id="c262b-128">But hello reverse misclassification is five times more costly toohello financial institution: if hello model predicts a low credit risk for someone who is actually a high credit risk.</span></span>

<span data-ttu-id="c262b-129">Таким образом мы хотим tootrain нашей модели, чтобы hello этот последний тип misclassification обходится в пять раз выше, чем ошибочную hello другим способом.</span><span class="sxs-lookup"><span data-stu-id="c262b-129">So, we want tootrain our model so that hello cost of this latter type of misclassification is five times higher than misclassifying hello other way.</span></span>
<span data-ttu-id="c262b-130">Один простой способ toodo это при обучении модели hello в нашем эксперименте — путем дублирования (пять раз) те операции, которые представляют кого-либо с высокой кредитного риска.</span><span class="sxs-lookup"><span data-stu-id="c262b-130">One simple way toodo this when training hello model in our experiment is by duplicating (five times) those entries that represent someone with a high credit risk.</span></span> <span data-ttu-id="c262b-131">Затем если hello модели misclassifies кто-то как низкий кредитного риска, когда они фактически высокого риска, hello модели не этой же misclassification пять раз, один раз для каждого дубликата.</span><span class="sxs-lookup"><span data-stu-id="c262b-131">Then, if hello model misclassifies someone as a low credit risk when they're actually a high risk, hello model does that same misclassification five times, once for each duplicate.</span></span> <span data-ttu-id="c262b-132">Это увеличит стоимость hello эту ошибку в результаты обучения hello.</span><span class="sxs-lookup"><span data-stu-id="c262b-132">This will increase hello cost of this error in hello training results.</span></span>


## <a name="convert-hello-dataset-format"></a><span data-ttu-id="c262b-133">Преобразовать формат набора данных hello</span><span class="sxs-lookup"><span data-stu-id="c262b-133">Convert hello dataset format</span></span>
<span data-ttu-id="c262b-134">Hello исходный набор данных используется формат разделенных пустым.</span><span class="sxs-lookup"><span data-stu-id="c262b-134">hello original dataset uses a blank-separated format.</span></span> <span data-ttu-id="c262b-135">Студия машинного обучения лучше работает с файл значений с разделителями запятыми (CSV), мы будем преобразования набора данных hello, заменив пробелы с запятыми.</span><span class="sxs-lookup"><span data-stu-id="c262b-135">Machine Learning Studio works better with a comma-separated value (CSV) file, so we'll convert hello dataset by replacing spaces with commas.</span></span>  

<span data-ttu-id="c262b-136">Существует много способов tooconvert эти данные.</span><span class="sxs-lookup"><span data-stu-id="c262b-136">There are many ways tooconvert this data.</span></span> <span data-ttu-id="c262b-137">Одним из способов является использование hello следующую команду Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c262b-137">One way is by using hello following Windows PowerShell command:</span></span>   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

<span data-ttu-id="c262b-138">Другим способом является использование команды sed hello Unix:</span><span class="sxs-lookup"><span data-stu-id="c262b-138">Another way is by using hello Unix sed command:</span></span>  

    sed 's/ /,/g' german.data > german.csv  

<span data-ttu-id="c262b-139">В любом случае мы создали CSV-версию hello данных в файл с именем **german.csv** , можно использовать в наших эксперимента.</span><span class="sxs-lookup"><span data-stu-id="c262b-139">In either case, we have created a comma-separated version of hello data in a file named **german.csv** that we can use in our experiment.</span></span>

## <a name="upload-hello-dataset-toomachine-learning-studio"></a><span data-ttu-id="c262b-140">Отправка tooMachine hello набор данных Studio обучения</span><span class="sxs-lookup"><span data-stu-id="c262b-140">Upload hello dataset tooMachine Learning Studio</span></span>
<span data-ttu-id="c262b-141">После того, как данные hello были преобразованный tooCSV формата, мы должны tooupload его в студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="c262b-141">Once hello data has been converted tooCSV format, we need tooupload it into Machine Learning Studio.</span></span> 

1. <span data-ttu-id="c262b-142">Домашняя страница Привет открыть студии машинного обучения ([https://studio.azureml.net](https://studio.azureml.net)).</span><span class="sxs-lookup"><span data-stu-id="c262b-142">Open hello Machine Learning Studio home page ([https://studio.azureml.net](https://studio.azureml.net)).</span></span> 

2. <span data-ttu-id="c262b-143">Щелкните меню hello ![меню][1] hello верхнего левого угла окна hello, щелкните **машинного обучения Azure**выберите **Studio**и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="c262b-143">Click hello menu ![Menu][1] in hello upper-left corner of hello window, click **Azure Machine Learning**, select **Studio**, and sign in.</span></span>

3. <span data-ttu-id="c262b-144">Нажмите кнопку **+ создать** hello нижней части окна hello.</span><span class="sxs-lookup"><span data-stu-id="c262b-144">Click **+NEW** at hello bottom of hello window.</span></span>

4. <span data-ttu-id="c262b-145">Выберите **НАБОР ДАННЫХ**.</span><span class="sxs-lookup"><span data-stu-id="c262b-145">Select **DATASET**.</span></span>

5. <span data-ttu-id="c262b-146">Выберите **ИЗ ЛОКАЛЬНОГО ФАЙЛА**.</span><span class="sxs-lookup"><span data-stu-id="c262b-146">Select **FROM LOCAL FILE**.</span></span>

    ![Добавление набора данных из локального файла][2]

6. <span data-ttu-id="c262b-148">В hello **отправить новый набор данных** диалоговое окно, нажмите кнопку **Обзор** и найти hello **german.csv** созданный файл.</span><span class="sxs-lookup"><span data-stu-id="c262b-148">In hello **Upload a new dataset** dialog, click **Browse** and find hello **german.csv** file you created.</span></span>

7. <span data-ttu-id="c262b-149">Введите имя для набора данных hello.</span><span class="sxs-lookup"><span data-stu-id="c262b-149">Enter a name for hello dataset.</span></span> <span data-ttu-id="c262b-150">В этом пошаговом руководстве назовем его UCI German Credit Card Data.</span><span class="sxs-lookup"><span data-stu-id="c262b-150">For this walkthrough, call it "UCI German Credit Card Data".</span></span>

8. <span data-ttu-id="c262b-151">Для типа данных выберите **Универсальный CSV-файл без заголовка (.nh.csv)**.</span><span class="sxs-lookup"><span data-stu-id="c262b-151">For data type, select **Generic CSV File With no header (.nh.csv)**.</span></span>

9. <span data-ttu-id="c262b-152">При желании добавьте описание.</span><span class="sxs-lookup"><span data-stu-id="c262b-152">Add a description if you’d like.</span></span>

10. <span data-ttu-id="c262b-153">Нажмите кнопку hello **ОК** флажок.</span><span class="sxs-lookup"><span data-stu-id="c262b-153">Click hello **OK** check mark.</span></span>  

    ![Передача hello набора данных][3]

<span data-ttu-id="c262b-155">Это передает данные hello в модуль набора данных, который можно использовать в эксперименте.</span><span class="sxs-lookup"><span data-stu-id="c262b-155">This uploads hello data into a dataset module that we can use in an experiment.</span></span>

<span data-ttu-id="c262b-156">Можно управлять наборами данных, щелкнув hello загруженные tooStudio **наборы данных** toohello вкладка левой части окна Studio hello.</span><span class="sxs-lookup"><span data-stu-id="c262b-156">You can manage datasets that you've uploaded tooStudio by clicking hello **DATASETS** tab toohello left of hello Studio window.</span></span>

![Управление наборами данных][4]

<span data-ttu-id="c262b-158">Дополнительные сведения об импорте других типов данных в эксперимент см. в статье [Импорт обучающих данных в Студию машинного обучения Azure из разных источников данных](machine-learning-data-science-import-data.md).</span><span class="sxs-lookup"><span data-stu-id="c262b-158">For more information about importing other types of data into an experiment, see [Import your training data into Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span></span>

<span data-ttu-id="c262b-159">**Далее:[ создание эксперимента](machine-learning-walkthrough-3-create-new-experiment.md)**</span><span class="sxs-lookup"><span data-stu-id="c262b-159">**Next: [Create a new experiment](machine-learning-walkthrough-3-create-new-experiment.md)**</span></span>

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
