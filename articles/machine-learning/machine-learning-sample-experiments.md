---
title: "Использование примеров экспериментов машинного обучения в Azure | Документация Майкрософт"
description: "Узнайте, как использовать примеры экспериментов машинного обучения из коллекции Cortana Intelligence для создания экспериментов с использованием Машинного обучения Microsoft Azure."
keywords: machine learning examples, sample experiment, machine learning sample
services: machine-learning
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: 81e6c1d8-682c-4db3-bfd5-d7bfb1150ff3
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/28/2017
ms.author: cgronlun
ms.openlocfilehash: 55f9bd2ed0d555a14d31bf3d262707d65bd70244
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="copy-example-experiments-to-create-new-machine-learning-experiments"></a><span data-ttu-id="68a28-104">Использование примеров экспериментов для создания новых экспериментов машинного обучения</span><span class="sxs-lookup"><span data-stu-id="68a28-104">Copy example experiments to create new machine learning experiments</span></span>
<span data-ttu-id="68a28-105">Узнайте, как использовать примеры экспериментов машинного обучения из [коллекции Cortana Intelligence](https://gallery.cortanaintelligence.com/), чтобы не создавать собственные решения с нуля.</span><span class="sxs-lookup"><span data-stu-id="68a28-105">Learn how to start with example experiments from [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) instead of creating machine learning experiments from scratch.</span></span> <span data-ttu-id="68a28-106">Эти примеры помогут вам создать решение машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="68a28-106">You can use the examples to build your own machine learning solution.</span></span>

<span data-ttu-id="68a28-107">В коллекции содержатся примеры экспериментов, предоставленные как рабочей группой Машинного обучения Microsoft Azure, так и участниками сообщества машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="68a28-107">The gallery has example experiments by the Microsoft Azure Machine Learning team as well as examples shared by the Machine Learning community.</span></span> <span data-ttu-id="68a28-108">Также можно задавать вопросы и публиковать комментарии об экспериментах.</span><span class="sxs-lookup"><span data-stu-id="68a28-108">You also can ask questions or post comments about experiments.</span></span>

<span data-ttu-id="68a28-109">Чтобы узнать, как использовать коллекцию, просмотрите 3-минутное видео [Копирование работы других пользователей для обработки и анализа данных](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) из серии [Обработка и анализ данных для начинающих](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span><span class="sxs-lookup"><span data-stu-id="68a28-109">To see how to use the gallery, watch the 3-minute video [Copy other people's work to do data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) from the series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="find-an-experiment-to-copy-in-cortana-intelligence-gallery"></a><span data-ttu-id="68a28-110">Поиск эксперимента для копирования в коллекции Cortana Intelligence</span><span class="sxs-lookup"><span data-stu-id="68a28-110">Find an experiment to copy in Cortana Intelligence Gallery</span></span>
<span data-ttu-id="68a28-111">Чтобы просмотреть доступные эксперименты, перейдите в раздел [Коллекция](https://gallery.cortanaintelligence.com/) и щелкните **Эксперименты** в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="68a28-111">To see what experiments are available, go to the [Gallery](https://gallery.cortanaintelligence.com/) and click **Experiments** at the top of the page.</span></span>

### <a name="find-the-newest-or-most-popular-experiments"></a><span data-ttu-id="68a28-112">Поиск последних и самых популярных экспериментов</span><span class="sxs-lookup"><span data-stu-id="68a28-112">Find the newest or most popular experiments</span></span>
<span data-ttu-id="68a28-113">На этой странице можно просмотреть **недавно добавленные** эксперименты, а также **популярные эксперименты** или последние **популярные эксперименты Майкрософт**.</span><span class="sxs-lookup"><span data-stu-id="68a28-113">On this page, you can see **Recently added** experiments, or scroll down to look at **What's popular** or the latest **Popular Microsoft experiments**.</span></span>

### <a name="look-for-an-experiment-that-meets-specific-requirements"></a><span data-ttu-id="68a28-114">Поиск эксперимента, соответствующего определенным требованиям</span><span class="sxs-lookup"><span data-stu-id="68a28-114">Look for an experiment that meets specific requirements</span></span>
<span data-ttu-id="68a28-115">Для просмотра всех экспериментов выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="68a28-115">To browse all experiments:</span></span>

1. <span data-ttu-id="68a28-116">В верхней части страницы щелкните **Просмотреть все** .</span><span class="sxs-lookup"><span data-stu-id="68a28-116">Click **Browse all** at the top of the page.</span></span>
2. <span data-ttu-id="68a28-117">В левой части окна в разделе **Refine by** (Отфильтровать по) в разделе **Категории** выберите **Эксперимент**, чтобы просмотреть все эксперименты в коллекции.</span><span class="sxs-lookup"><span data-stu-id="68a28-117">On the left-hand side, under **Refine by** in the **Categories** section, select **Experiment** to see all the experiments in the Gallery.</span></span>
3. <span data-ttu-id="68a28-118">Эксперименты, соответствующие определенным требованиям, можно найти несколькими различными способами.</span><span class="sxs-lookup"><span data-stu-id="68a28-118">You can find experiments that meet your requirements a couple different ways:</span></span>
   * <span data-ttu-id="68a28-119">**Выберите фильтры в левой части окна.**</span><span class="sxs-lookup"><span data-stu-id="68a28-119">**Select filters on the left.**</span></span> <span data-ttu-id="68a28-120">Например, чтобы просмотреть эксперименты, в которых используется алгоритм обнаружения аномалий на основе PCA, выберите **Эксперимент** в разделе **Категории** и щелкните **Показать все**.</span><span class="sxs-lookup"><span data-stu-id="68a28-120">For example, to browse experiments that use a PCA-based anomaly detection algorithm: With **Experiment** selected under **Categories**, click **Show all**.</span></span> <span data-ttu-id="68a28-121">Затем. в разделе **Algorithms Used** (Используемые алгоритмы) выберите **PCA-Based Anomaly Detection** (Обнаружение аномалий на основе анализа первичных компонентов).</span><span class="sxs-lookup"><span data-stu-id="68a28-121">Then, under **Algorithms Used**, choose **PCA-Based Anomaly Detection**.</span></span> <br></br><span data-ttu-id="68a28-122">
     ![Выбор фильтров](./media/machine-learning-sample-experiments/refine-the-view.png)</span><span class="sxs-lookup"><span data-stu-id="68a28-122">
![Select filters](./media/machine-learning-sample-experiments/refine-the-view.png)</span></span>
   * <span data-ttu-id="68a28-123">**Используйте поле поиска.**</span><span class="sxs-lookup"><span data-stu-id="68a28-123">**Use the search box.**</span></span> <span data-ttu-id="68a28-124">Например, чтобы найти эксперименты, предоставленные корпорацией Майкрософт и относящиеся к распознаванию цифр с использованием алгоритма двухклассовой машины опорных векторов, введите "распознавание цифр" в поле поиска.</span><span class="sxs-lookup"><span data-stu-id="68a28-124">For example, to find experiments contributed by Microsoft related to digit recognition that use a two-class support vector machine algorithm, enter "digit recognition" in the search box.</span></span> <span data-ttu-id="68a28-125">Затем выберите фильтры **Experiment** (Эксперимент), **Microsoft content only** (Только содержимое Майкрософт) и **Two-Class Support Vector Machine** (Двухклассовая машина опорных векторов).</span><span class="sxs-lookup"><span data-stu-id="68a28-125">Then, select the filters **Experiment**, **Microsoft content only**, and **Two-Class Support Vector Machine**:</span></span><br></br><span data-ttu-id="68a28-126">
     ![Используйте поле поиска.](./media/machine-learning-sample-experiments/search-for-experiments.png)</span><span class="sxs-lookup"><span data-stu-id="68a28-126">
![Use the search box](./media/machine-learning-sample-experiments/search-for-experiments.png)</span></span>
4. <span data-ttu-id="68a28-127">Щелкните эксперимент, чтобы узнать о нем подробнее.</span><span class="sxs-lookup"><span data-stu-id="68a28-127">Click an experiment to learn more about it.</span></span>
5. <span data-ttu-id="68a28-128">Чтобы запустить или изменить эксперимент, щелкните **Open in Studio** (Открыть в Студии) на странице эксперимента.</span><span class="sxs-lookup"><span data-stu-id="68a28-128">To run and/or modify the experiment, click **Open in Studio** on the experiment's page.</span></span> <br></br>

    ![Пример эксперимента](./media/machine-learning-sample-experiments/example-experiment.png)

    > [!NOTE]
    > <span data-ttu-id="68a28-130">При первом открытии эксперимента в Студии машинного обучения можно испытать его бесплатно или приобрести подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="68a28-130">When you open an experiment in Machine Learning Studio for the first time, you can try it for free or buy an Azure subscription.</span></span> <span data-ttu-id="68a28-131">Дополнительные сведения о бесплатной пробной и платной версии Студии машинного обучения см. на странице [цен на машинное обучение](https://azure.microsoft.com/pricing/details/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="68a28-131">[Learn about the Machine Learning Studio free trial vs. paid service](https://azure.microsoft.com/pricing/details/machine-learning/)</span></span>
    >
    >

## <a name="create-a-new-experiment-using-an-example-as-a-template"></a><span data-ttu-id="68a28-132">Создание эксперимента, используя в качестве шаблона пример</span><span class="sxs-lookup"><span data-stu-id="68a28-132">Create a new experiment using an example as a template</span></span>
<span data-ttu-id="68a28-133">Эксперимент в студии машинного обучения также можно создать, используя пример из коллекции в качестве шаблона.</span><span class="sxs-lookup"><span data-stu-id="68a28-133">You also can create a new experiment in Machine Learning Studio using a Gallery example as a template.</span></span>

1. <span data-ttu-id="68a28-134">Войдите в [Студию](https://studio.azureml.net) с использованием учетной записи Майкрософт, после чего щелкните **Создать**, чтобы создать эксперимент.</span><span class="sxs-lookup"><span data-stu-id="68a28-134">Sign in with your Microsoft account credentials to the [Studio](https://studio.azureml.net), and then click **New** to create an experiment.</span></span>
2. <span data-ttu-id="68a28-135">Просмотрите примеры содержимого и выберите то, что вам подходит.</span><span class="sxs-lookup"><span data-stu-id="68a28-135">Browse through the example content and click one.</span></span>

<span data-ttu-id="68a28-136">В рабочей области студии машинного обучения будет создан эксперимент на основе выбранного примера в качестве шаблона.</span><span class="sxs-lookup"><span data-stu-id="68a28-136">A new experiment is created in your Machine Learning Studio workspace using the example experiment as a template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68a28-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="68a28-137">Next steps</span></span>
* [<span data-ttu-id="68a28-138">Импорт обучающих данных в Студию машинного обучения Azure из разных источников данных</span><span class="sxs-lookup"><span data-stu-id="68a28-138">Import data from various sources</span></span>](machine-learning-data-science-import-data.md)
* [<span data-ttu-id="68a28-139">Краткое руководство по языку программирования R для службы машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="68a28-139">Quickstart tutorial for the R language in Machine Learning</span></span>](machine-learning-r-quickstart.md)
* [<span data-ttu-id="68a28-140">Развертывание веб-службы машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="68a28-140">Deploy a Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
