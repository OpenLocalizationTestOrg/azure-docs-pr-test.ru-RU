---
title: "aaaDebug модели в машинном обучении Azure | Документы Microsoft"
description: "Как toodebug ошибки, возникшие по Обучение модели и оценка модели модулей в машинном обучении Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 629dc45e-ac1e-4b7d-b120-08813dc448be
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bradsev;garye
ms.openlocfilehash: ee38ca8ce38d4fc7add5ba70c80ab9bb2ceaf1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-model-in-azure-machine-learning"></a><span data-ttu-id="8f477-103">Отладка машинного обучения модели в Azure</span><span class="sxs-lookup"><span data-stu-id="8f477-103">Debug your Model in Azure Machine Learning</span></span>

<span data-ttu-id="8f477-104">В этой статье описываются hello потенциальных причин, почему либо после двух отказов hello может возникать при работе модели:</span><span class="sxs-lookup"><span data-stu-id="8f477-104">This article explains hello potential reasons why either of hello following two failures might be encountered when running a model:</span></span>

* <span data-ttu-id="8f477-105">Hello [Обучение модели] [ train-model] модуля приводит к ошибке</span><span class="sxs-lookup"><span data-stu-id="8f477-105">hello [Train Model][train-model] module produces an error</span></span> 
* <span data-ttu-id="8f477-106">Hello [модель оценки] [ score-model] модуль выдает неверные результаты</span><span class="sxs-lookup"><span data-stu-id="8f477-106">hello [Score Model][score-model] module produces incorrect results</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a><span data-ttu-id="8f477-107">Модуль "Обучение модели" выдает ошибку</span><span class="sxs-lookup"><span data-stu-id="8f477-107">Train Model Module produces an error</span></span>

![рисунок 1](./media/machine-learning-debug-models/train_model-1.png)

<span data-ttu-id="8f477-109">Hello [Обучение модели] [ train-model] модуль ожидает два входа:</span><span class="sxs-lookup"><span data-stu-id="8f477-109">hello [Train Model][train-model] Module expects two inputs:</span></span>

1. <span data-ttu-id="8f477-110">Тип Hello модели машинного обучения из коллекции hello моделях, предоставляемых машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="8f477-110">hello type of machine learning model from hello collection of models provided by Azure Machine Learning.</span></span>
2. <span data-ttu-id="8f477-111">Hello обучающие данные с указанного столбца метки, который указывает hello переменной toopredict (hello других столбцов, считаются toobe функции).</span><span class="sxs-lookup"><span data-stu-id="8f477-111">hello training data with a specified Label column which specifies hello variable toopredict (hello other columns are assumed toobe Features).</span></span>

<span data-ttu-id="8f477-112">Этот модуль может вызвать ошибку в hello в следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="8f477-112">This module can produce an error in hello following cases:</span></span>

1. <span data-ttu-id="8f477-113">столбец метки Hello указан неправильно.</span><span class="sxs-lookup"><span data-stu-id="8f477-113">hello Label column is specified incorrectly.</span></span> <span data-ttu-id="8f477-114">Это может произойти, если более чем один столбец выбран в качестве метки hello или выбран неправильный столбца индекса.</span><span class="sxs-lookup"><span data-stu-id="8f477-114">This can happen if either more than one column is selected as hello Label or an incorrect column index is selected.</span></span> <span data-ttu-id="8f477-115">Например второй вариант hello будет применяться, если индекс столбца 30 используется с входного набора данных, содержащей только 25 столбцов.</span><span class="sxs-lookup"><span data-stu-id="8f477-115">For example, hello second case would apply if a column index of 30 is used with an input dataset which has only 25 columns.</span></span>

2. <span data-ttu-id="8f477-116">Hello набора данных не содержит какие-либо столбцы компонентов.</span><span class="sxs-lookup"><span data-stu-id="8f477-116">hello dataset does not contain any Feature columns.</span></span> <span data-ttu-id="8f477-117">Например если hello входной набор данных содержит только один столбец, который помечен как столбец метки hello, будет нет функций с какую модель toobuild hello.</span><span class="sxs-lookup"><span data-stu-id="8f477-117">For example, if hello input dataset has only one column, which is marked as hello Label column, there would be no features with which toobuild hello model.</span></span> <span data-ttu-id="8f477-118">В этом случае hello [Обучение модели] [ train-model] модуль выдает ошибку.</span><span class="sxs-lookup"><span data-stu-id="8f477-118">In this case, hello [Train Model][train-model] module produces an error.</span></span>

3. <span data-ttu-id="8f477-119">Hello входного набора данных (функций или метку) содержит значение бесконечности.</span><span class="sxs-lookup"><span data-stu-id="8f477-119">hello input dataset (Features or Label) contains Infinity as a value.</span></span>

## <a name="score-model-module-produces-incorrect-results"></a><span data-ttu-id="8f477-120">Модуль "Score Model" (Оценка модели) выдает неправильные результаты</span><span class="sxs-lookup"><span data-stu-id="8f477-120">Score Model Module produces incorrect results</span></span>

![рисунок 2](./media/machine-learning-debug-models/train_test-2.png)

<span data-ttu-id="8f477-122">В обычной обучение и тестирование эксперименте для контролируемого обучения, hello [разбиение данных] [ split] модуль hello исходный набор данных разделяется на две части: одной части модели используется tootrain hello и используется одна часть tooscore, насколько хорошо выполняется hello обученной модели.</span><span class="sxs-lookup"><span data-stu-id="8f477-122">In a typical training/testing experiment for supervised learning, hello [Split Data][split] module divides hello original dataset into two parts: one part is used tootrain hello model and one part is used tooscore how well hello trained model performs.</span></span> <span data-ttu-id="8f477-123">Hello обученной модели является используется tooscore hello проверочных данных, после чего результаты hello, вычисленное toodetermine hello точность модели hello.</span><span class="sxs-lookup"><span data-stu-id="8f477-123">hello trained model is then used tooscore hello test data, after which hello results are evaluated toodetermine hello accuracy of hello model.</span></span>

<span data-ttu-id="8f477-124">Hello [модель оценки] [ score-model] модуль требует наличия двух входных значений:</span><span class="sxs-lookup"><span data-stu-id="8f477-124">hello [Score Model][score-model] module requires two inputs:</span></span>

1. <span data-ttu-id="8f477-125">Вывод hello обученной модели [Обучение модели] [ train-model] модуля.</span><span class="sxs-lookup"><span data-stu-id="8f477-125">A trained model output from hello [Train Model][train-model] module.</span></span>
2. <span data-ttu-id="8f477-126">Оценки набора данных, отличный от hello набора данных используется модель tootrain hello.</span><span class="sxs-lookup"><span data-stu-id="8f477-126">A scoring dataset that is different from hello dataset used tootrain hello model.</span></span>

<span data-ttu-id="8f477-127">Он, возможно, что даже если эксперимент hello завершится успешно, hello [модель оценки] [ score-model] модуль выдает неверные результаты.</span><span class="sxs-lookup"><span data-stu-id="8f477-127">It's possible that even though hello experiment succeeds, hello [Score Model][score-model] module produces incorrect results.</span></span> <span data-ttu-id="8f477-128">Несколько сценариев возможно возникновение этого toohappen:</span><span class="sxs-lookup"><span data-stu-id="8f477-128">Several scenarios may cause this toohappen:</span></span>

1. <span data-ttu-id="8f477-129">Если hello указанная категориальные метки и модель регрессии проводится на данных hello, неверные выходные данные будут получены с hello [модель оценки] [ score-model] модуля.</span><span class="sxs-lookup"><span data-stu-id="8f477-129">If hello specified Label is categorical and a regression model is trained on hello data, an incorrect output would be produced by hello [Score Model][score-model] module.</span></span> <span data-ttu-id="8f477-130">Это обусловлено тем, что для регрессии требуется непрерывная переменная ответа.</span><span class="sxs-lookup"><span data-stu-id="8f477-130">This is because regression requires a continuous response variable.</span></span> <span data-ttu-id="8f477-131">В этом случае было бы более подходящими toouse модели классификации.</span><span class="sxs-lookup"><span data-stu-id="8f477-131">In this case, it would be more suitable toouse a classification model.</span></span> 

2. <span data-ttu-id="8f477-132">Аналогично Если для набора данных наличие чисел с плавающей запятой в столбец метки hello является обученной модели классификации, может привести к нежелательным результатам.</span><span class="sxs-lookup"><span data-stu-id="8f477-132">Similarly, if a classification model is trained on a dataset having floating point numbers in hello Label column, it may produce undesirable results.</span></span> <span data-ttu-id="8f477-133">Это обусловлено тем, что для классификации требуется дискретная переменная отклика, с которой можно использовать только значения, соответствующие конечному и обычно несколько малому набору классов.</span><span class="sxs-lookup"><span data-stu-id="8f477-133">This is because classification requires a discrete response variable that only allows values that range over a finite, and usually somewhat small, set of classes.</span></span>

3. <span data-ttu-id="8f477-134">Здравствуйте, если hello оценки набора данных не содержит все модели hello tootrain hello используемых функций, [модель оценки] [ score-model] приводит к ошибке.</span><span class="sxs-lookup"><span data-stu-id="8f477-134">If hello scoring dataset does not contain all hello features used tootrain hello model, hello [Score Model][score-model] produces an error.</span></span>

4. <span data-ttu-id="8f477-135">Здравствуйте, если строка hello оценки набор данных содержит отсутствующее значение или бесконечное значение для любой из его компонентов, [модель оценки] [ score-model] не приводят к соответствующей toothat строки все выходные данные.</span><span class="sxs-lookup"><span data-stu-id="8f477-135">If a row in hello scoring dataset contains a missing value or an infinite value for any of its features, hello [Score Model][score-model] will not produce any output corresponding toothat row.</span></span>

5. <span data-ttu-id="8f477-136">Hello [модель оценки] [ score-model] может привести к одинаковых выходов для всех строк в hello оценки набора данных.</span><span class="sxs-lookup"><span data-stu-id="8f477-136">hello [Score Model][score-model] may produce identical outputs for all rows in hello scoring dataset.</span></span> <span data-ttu-id="8f477-137">Это может произойти, например, при попытке классификации с помощью леса принятия решений, если вы выбрали toobe больше, чем hello количеству обучающих примеров доступных hello минимальное число выборок для конечного узла.</span><span class="sxs-lookup"><span data-stu-id="8f477-137">This could occur, for example, when attempting classification using Decision Forests if hello minimum number of samples per leaf node is chosen toobe more than hello number of training examples available.</span></span>

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

