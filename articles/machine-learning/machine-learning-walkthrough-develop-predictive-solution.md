---
title: "aaaA прогнозирующего решения для кредитного риска с машинного обучения | Документы Microsoft"
description: "Подробное пошаговое руководство отображаются как toocreate решения для прогнозирующего анализа для кредита оценка рисков в студии машинного обучения Azure."
keywords: "кредитный риск, решение прогнозной аналитики, оценка рисков"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 43300854-a14e-4cd2-9bb1-c55c779e0e93
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 00ed39081e6952b8d03b37a8285d8dc3ddff2cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a><span data-ttu-id="54bcd-104">Пошаговое руководство по разработке решения для прогнозной аналитики в службе машинного обучения Azure для оценки кредитных рисков</span><span class="sxs-lookup"><span data-stu-id="54bcd-104">Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning</span></span>

<span data-ttu-id="54bcd-105">В этом пошаговом руководстве мы рассмотрим расширенные hello процесс разработки решения для прогнозирующего анализа в студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="54bcd-105">In this walkthrough, we take an extended look at hello process of developing a predictive analytics solution in Machine Learning Studio.</span></span> <span data-ttu-id="54bcd-106">Мы разработка простого модели в студии машинного обучения и затем развернуть его как веб-службы машинного обучения Azure, где hello модели можно сделать прогноз, с помощью новых данных.</span><span class="sxs-lookup"><span data-stu-id="54bcd-106">We develop a simple model in Machine Learning Studio, and then deploy it as an Azure Machine Learning web service where hello model can make predictions using new data.</span></span> 

<span data-ttu-id="54bcd-107">В этом руководстве предполагается, что вы уже работали со Студией машинного обучения и имеете некоторое представление о машинном обучении.</span><span class="sxs-lookup"><span data-stu-id="54bcd-107">This walkthrough assumes that you've used Machine Learning Studio at least once before, and that you have some understanding of machine learning concepts.</span></span> <span data-ttu-id="54bcd-108">При этом предполагается, что вы не являетесь специалистом в этой области.</span><span class="sxs-lookup"><span data-stu-id="54bcd-108">But it doesn't assume you're an expert in either.</span></span>

<span data-ttu-id="54bcd-109">Если вы раньше не использовали **студии машинного обучения Azure** перед toostart hello учебник, может потребоваться [создать первый обработки и анализа данных эксперимента в студии машинного обучения Azure](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="54bcd-109">If you've never used **Azure Machine Learning Studio** before, you might want toostart with hello tutorial, [Create your first data science experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span></span> <span data-ttu-id="54bcd-110">Этот учебник поможет выполнить студии машинного обучения для hello первый раз.</span><span class="sxs-lookup"><span data-stu-id="54bcd-110">That tutorial takes you through Machine Learning Studio for hello first time.</span></span> <span data-ttu-id="54bcd-111">Он показывает, основы hello модулей как toodrag перетаскивания в свой эксперимент соединять их запуска эксперимента hello и просмотрите результаты hello.</span><span class="sxs-lookup"><span data-stu-id="54bcd-111">It shows you hello basics of how toodrag-and-drop modules onto your experiment, connect them together, run hello experiment, and look at hello results.</span></span> <span data-ttu-id="54bcd-112">Другое средство, которое может быть полезен для Приступая к работе — это схема, общие сведения о возможностях hello студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="54bcd-112">Another tool that may be helpful for getting started is a diagram that gives an overview of hello capabilities of Machine Learning Studio.</span></span> <span data-ttu-id="54bcd-113">Ее можно скачать и распечатать в статье [Обзорная схема возможностей Студии машинного обучения Azure](machine-learning-studio-overview-diagram.md).</span><span class="sxs-lookup"><span data-stu-id="54bcd-113">You can download and print it from here: [Overview diagram of Azure Machine Learning Studio capabilities](machine-learning-studio-overview-diagram.md).</span></span>
 
<span data-ttu-id="54bcd-114">Если вы новое поле toohello машинного обучения в целом, есть ряд видео, которые могут быть полезными tooyou.</span><span class="sxs-lookup"><span data-stu-id="54bcd-114">If you're new toohello field of machine learning in general, there's a video series that might be helpful tooyou.</span></span> <span data-ttu-id="54bcd-115">Он вызывается [обработки и анализа данных для начинающих](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) и он может предоставлять обучения toomachine значительные введение, с использованием естественного языка и понятий.</span><span class="sxs-lookup"><span data-stu-id="54bcd-115">It's called [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) and it can give you a great introduction toomachine learning using everyday language and concepts.</span></span>


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="hello-problem"></a><span data-ttu-id="54bcd-116">проблема Hello</span><span class="sxs-lookup"><span data-stu-id="54bcd-116">hello problem</span></span>

<span data-ttu-id="54bcd-117">Предположим, вам необходимо toopredict отдельного кредитного риска на основе hello введенных в приложении кредит на нее.</span><span class="sxs-lookup"><span data-stu-id="54bcd-117">Suppose you need toopredict an individual's credit risk based on hello information they gave on a credit application.</span></span>  

<span data-ttu-id="54bcd-118">Оценка кредитных рисков — это сложная проблема. Для этого пошагового руководства мы немного упростим ее.</span><span class="sxs-lookup"><span data-stu-id="54bcd-118">Credit risk assessment is a complex problem, but we can simplify it a bit for this walkthrough.</span></span> <span data-ttu-id="54bcd-119">Мы используем ее в качестве примера для создания решения прогнозной аналитики с помощью машинного обучения Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="54bcd-119">We'll use it as an example of how you can create a predictive analytics solution using Microsoft Azure Machine Learning.</span></span> <span data-ttu-id="54bcd-120">toodo это, мы используем студии машинного обучения Azure и веб-службы машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="54bcd-120">toodo this, we use Azure Machine Learning Studio and a Machine Learning web service.</span></span>  

## <a name="hello-solution"></a><span data-ttu-id="54bcd-121">решение Hello</span><span class="sxs-lookup"><span data-stu-id="54bcd-121">hello solution</span></span>

<span data-ttu-id="54bcd-122">В рамках этого руководства мы начнем с общедоступных данных кредитного риска и на их основе разработаем и обучим прогнозную модель.</span><span class="sxs-lookup"><span data-stu-id="54bcd-122">In this detailed walkthrough, we start with publicly available credit risk data and develop and train a predictive model based on that data.</span></span> <span data-ttu-id="54bcd-123">Затем мы развертывание hello модели в виде веб-службы, он может использоваться другими пользователями для оценки рисков кредит.</span><span class="sxs-lookup"><span data-stu-id="54bcd-123">Then we deploy hello model as a web service so it can be used by others for credit risk assessment.</span></span>

<span data-ttu-id="54bcd-124">toocreate это решение оценки риска кредитной мы выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="54bcd-124">toocreate this credit risk assessment solution, we follow these steps:</span></span>  

1. [<span data-ttu-id="54bcd-125">Создание рабочей области машинного обучения</span><span class="sxs-lookup"><span data-stu-id="54bcd-125">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="54bcd-126">Отправка существующих данных</span><span class="sxs-lookup"><span data-stu-id="54bcd-126">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="54bcd-127">Создание эксперимента</span><span class="sxs-lookup"><span data-stu-id="54bcd-127">Create an experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="54bcd-128">Обучать и оценивать модели hello</span><span class="sxs-lookup"><span data-stu-id="54bcd-128">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="54bcd-129">Развернуть веб-службу hello</span><span class="sxs-lookup"><span data-stu-id="54bcd-129">Deploy hello web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="54bcd-130">Веб-службы доступа hello</span><span class="sxs-lookup"><span data-stu-id="54bcd-130">Access hello web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> <span data-ttu-id="54bcd-131">В этом пошаговом руководстве в hello можно найти рабочую копию hello эксперимента, в ходе разработки мы [коллекции аналитики Cortana](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="54bcd-131">You can find a working copy of hello experiment that we develop in this walkthrough in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="54bcd-132">Go слишком**[Пошаговое руководство: прогноз риска кредитной](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)**  и нажмите кнопку **в Studio** toodownload копию hello эксперимента в рабочую область студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="54bcd-132">Go too**[Walkthrough - Credit risk prediction](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** and click **Open in Studio** toodownload a copy of hello experiment into your Machine Learning Studio workspace.</span></span>
> 
> <span data-ttu-id="54bcd-133">Это пошаговое руководство основано на упрощенную версию hello примере эксперимента [двоичной классификации: кредита прогнозирования рисков](http://go.microsoft.com/fwlink/?LinkID=525270), которые также доступны в hello [коллекции](http://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="54bcd-133">This walkthrough is based on a simplified version of hello sample experiment, [Binary Classification: Credit risk prediction](http://go.microsoft.com/fwlink/?LinkID=525270), also available in hello [Gallery](http://gallery.cortanaintelligence.com/).</span></span>
