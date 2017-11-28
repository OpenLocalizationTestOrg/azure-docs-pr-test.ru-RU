---
title: "AAA(deprecated) лексики на основе анализа мнений - Azure | Документы Microsoft"
description: "Лексический анализ тональности (устаревшая версия)"
services: machine-learning
documentationcenter: 
author: pengxia
manager: jhubbard
editor: cgronlun
ms.assetid: 912f41af-966c-4d79-a413-6f9fc02823df
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: pengxia
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 1ed7e19441c6a8ad270a0c0f567b4aea588a583e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-lexicon-based-sentiment-analysis"></a><span data-ttu-id="47b8e-103">Лексический анализ тональности (устаревшая версия)</span><span class="sxs-lookup"><span data-stu-id="47b8e-103">(deprecated) Lexicon Based Sentiment Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="47b8e-104">Hello Microsoft DataMarket прекращено, и этот API устарел.</span><span class="sxs-lookup"><span data-stu-id="47b8e-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="47b8e-105">Можно найти множество полезный пример экспериментов и API-интерфейсы в hello [коллекции аналитики Cortana](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="47b8e-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="47b8e-106">Дополнительные сведения о коллекции hello. в разделе [общего ресурса и поиска ресурсов в коллекции Cortana аналитики hello](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="47b8e-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="47b8e-107">Как можно измерить мнения пользователей и их отношение к торговым маркам или темам в социальных сетях, например публикациях в Facebook, твитах, рецензиях и т. д.?</span><span class="sxs-lookup"><span data-stu-id="47b8e-107">How can you measure users’ opinions and attitudes toward brands or topics in online social networks, such as Facebook posts, tweets, reviews, etc.?</span></span> <span data-ttu-id="47b8e-108">Анализ мнений позволяет изучать такие вопросы.</span><span class="sxs-lookup"><span data-stu-id="47b8e-108">Sentiment analysis provides a method for analyzing such questions.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="47b8e-109">Можно выделить два основных метода анализа мнений.</span><span class="sxs-lookup"><span data-stu-id="47b8e-109">There are generally two methods for sentiment analysis.</span></span> <span data-ttu-id="47b8e-110">Один с помощью алгоритма обучения с учителем и hello другие могут рассматриваться как неконтролируемого обучения.</span><span class="sxs-lookup"><span data-stu-id="47b8e-110">One is using a supervised learning algorithm, and hello other can be treated as unsupervised learning.</span></span> <span data-ttu-id="47b8e-111">Алгоритм контролируемого обучения строит модель классификации на основе большой совокупности данных с примечаниями.</span><span class="sxs-lookup"><span data-stu-id="47b8e-111">A supervised learning algorithm generally builds a classification model on a large annotated corpus.</span></span> <span data-ttu-id="47b8e-112">Точность главным образом основан на качество hello заметки hello и обычно процесс обучения hello займет много времени.</span><span class="sxs-lookup"><span data-stu-id="47b8e-112">Its accuracy is mainly based on hello quality of hello annotation, and usually hello training process will take a long time.</span></span> <span data-ttu-id="47b8e-113">Помимо, при применении домена tooanother алгоритм hello, результат hello не обычно.</span><span class="sxs-lookup"><span data-stu-id="47b8e-113">Besides that, when we apply hello algorithm tooanother domain, hello result is usually not good.</span></span> <span data-ttu-id="47b8e-114">Сравнение toosupervised обучения, лексики основе неконтролируемого обучения использует мнений словаря, который не требует хранения совокупности большие объемы данных и обучения — что делает hello весь процесс гораздо быстрее.</span><span class="sxs-lookup"><span data-stu-id="47b8e-114">Compared toosupervised learning, lexicon-based unsupervised learning uses a sentiment dictionary, which doesn’t require storing a large data corpus and training - which makes hello whole process much faster.</span></span> 

<span data-ttu-id="47b8e-115">Наш [службы](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) основана на hello лексики Subjectivity MPQA (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), которое является одним из наиболее часто используемых hello subjectivity словари.</span><span class="sxs-lookup"><span data-stu-id="47b8e-115">Our [service](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) is built on hello MPQA Subjectivity Lexicon (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), which is one of hello most commonly used subjectivity lexicons.</span></span> <span data-ttu-id="47b8e-116">Он включает 5097 слов для отрицательной оценки и 2533 слова — для положительной.</span><span class="sxs-lookup"><span data-stu-id="47b8e-116">There are 5097 negative and 2533 positive words in MPQA.</span></span> <span data-ttu-id="47b8e-117">Все они обозначены как имеющие сильную или слабую полярность.</span><span class="sxs-lookup"><span data-stu-id="47b8e-117">And all of these words are annotated as strong or weak polarity.</span></span> <span data-ttu-id="47b8e-118">Hello всей совокупности находится в режиме публичной лицензии GNU.</span><span class="sxs-lookup"><span data-stu-id="47b8e-118">hello whole corpus is under GNU General Public License.</span></span> <span data-ttu-id="47b8e-119">Hello веб-службы может быть применен tooany короткое предложения, например твитов и Facebook в блогах.</span><span class="sxs-lookup"><span data-stu-id="47b8e-119">hello web service can be applied tooany short sentences, such as tweets and Facebook posts.</span></span> 

> <span data-ttu-id="47b8e-120">Пользователи могут работать с этой веб-службой через мобильное приложение, веб-сайт или даже локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="47b8e-120">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer for example.</span></span> <span data-ttu-id="47b8e-121">Но hello hello веб-службы служит также tooserve в качестве примера как машинного обучения Azure можно использовать toocreate веб-служб на основе кода R.</span><span class="sxs-lookup"><span data-stu-id="47b8e-121">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="47b8e-122">Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="47b8e-122">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="47b8e-123">Hello веб-службы может быть опубликованным toohello Azure Marketplace и используемые пользователями и устройствами через Здравствуй, мир без настройки инфраструктуры автором hello hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="47b8e-123">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="47b8e-124">Использование веб-службы</span><span class="sxs-lookup"><span data-stu-id="47b8e-124">Consumption of web service</span></span>
<span data-ttu-id="47b8e-125">Hello входных данных может быть любой текст, но веб-службу hello лучше работает с короткий предложений.</span><span class="sxs-lookup"><span data-stu-id="47b8e-125">hello input data can be any text, but hello web service works better with short sentences.</span></span> <span data-ttu-id="47b8e-126">Hello выходных данных является числовым значением от -1 до 1.</span><span class="sxs-lookup"><span data-stu-id="47b8e-126">hello output is a numeric value between -1 and 1.</span></span> <span data-ttu-id="47b8e-127">Любое значение меньше 0 обозначает, что мнений hello текста hello является отрицательным; Если это положительное значение больше 0.</span><span class="sxs-lookup"><span data-stu-id="47b8e-127">Any value below 0 denotes that hello sentiment of hello text is negative; positive if above 0.</span></span> <span data-ttu-id="47b8e-128">абсолютное значение результата hello Hello обозначает hello стойкость hello связанные мнений.</span><span class="sxs-lookup"><span data-stu-id="47b8e-128">hello absolute value of hello result denotes hello strength of hello associated sentiment.</span></span> 

> <span data-ttu-id="47b8e-129">Эта служба, размещенного на hello Azure Marketplace, — это служба OData; Это может быть вызвана через методы POST или GET.</span><span class="sxs-lookup"><span data-stu-id="47b8e-129">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="47b8e-130">Существует несколько способов использования службы hello в автоматическом режиме (пример приложения — [здесь](http://microsoftazuremachinelearning.azurewebsites.net/)).</span><span class="sxs-lookup"><span data-stu-id="47b8e-130">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="47b8e-131">Начало кода C# для использования веб-службы:</span><span class="sxs-lookup"><span data-stu-id="47b8e-131">Starting C# code for web service consumption:</span></span>
    public class ScoreResult
    {
            [DataMember]
            public double result
            {
                get;
                set;
            }
    }

    void main()
    {
            using (var wb = new WebClient())
            {
                var acitionUri = new Uri("PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score");
                DataServiceContext ctx = new DataServiceContext(acitionUri);
                var cred = new NetworkCredential("PutEmailAddressHere", "ChangeToAPIKey");
                var cache = new CredentialCache();

                cache.Add(acitionUri, "Basic", cred);
                ctx.Credentials = cache;
                var query = ctx.Execute<ScoreResult>(acitionUri, "POST", true, new BodyOperationParameter("Text", TextBox1.Text));
                ScoreResult scoreResult = query.ElementAt(0);
                double result = scoreResult.result;
            }
    }



<span data-ttu-id="47b8e-132">входные данные Hello выглядит «сегодня хорошо день».</span><span class="sxs-lookup"><span data-stu-id="47b8e-132">hello input is “Today is a good day.”</span></span> <span data-ttu-id="47b8e-133">Hello выводится «1», который указывает положительных отзывов, связанные с входное предложение hello.</span><span class="sxs-lookup"><span data-stu-id="47b8e-133">hello output is “1”, which indicates a positive sentiment associated with hello input sentence.</span></span> 

## <a name="creation-of-web-service"></a><span data-ttu-id="47b8e-134">Создание веб-службы</span><span class="sxs-lookup"><span data-stu-id="47b8e-134">Creation of web service</span></span>
> <span data-ttu-id="47b8e-135">Эта веб-служба была создана с помощью системы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="47b8e-135">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="47b8e-136">Чтобы получить бесплатную пробную версию и вводные видеоматериалы по созданию экспериментов и [публикации веб-служб](machine-learning-publish-a-machine-learning-web-service.md), посетите веб-страницу [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="47b8e-136">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="47b8e-137">Ниже приведен снимок экрана приветствия эксперимента, созданные для каждого из модулей hello в эксперименте hello hello веб-службы и пример кода.</span><span class="sxs-lookup"><span data-stu-id="47b8e-137">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="47b8e-138">В службах машинного обучения Azure создан пустой эксперимент.</span><span class="sxs-lookup"><span data-stu-id="47b8e-138">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="47b8e-139">на следующем рисунке Hello показан поток эксперимента hello анализ мнений лексики.</span><span class="sxs-lookup"><span data-stu-id="47b8e-139">hello figure below shows hello experiment flow of lexicon-based sentiment analysis.</span></span> <span data-ttu-id="47b8e-140">файл «sent_dict.csv» Hello лексики subjectivity MPQA hello и задан в качестве одного из входов hello [выполнение скрипта R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="47b8e-140">hello “sent_dict.csv” file is hello MPQA subjectivity lexicon, and is set as one of hello inputs of [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="47b8e-141">Другой вход — проверку выборки из набора данных проверки hello Amazon для теста, где выполняется выделение, изменение имени столбца и операцию разбиения.</span><span class="sxs-lookup"><span data-stu-id="47b8e-141">Another input is a sampled review from hello Amazon review dataset for test, where we performed selection, column name modification, and split operations.</span></span> <span data-ttu-id="47b8e-142">Мы используем лексики subjectivity пакета toostore хэш hello в памяти hello и ускорить процесс вычисления оценка hello.</span><span class="sxs-lookup"><span data-stu-id="47b8e-142">We use a hash package toostore hello subjectivity lexicon in hello memory and accelerate hello score computation process.</span></span> <span data-ttu-id="47b8e-143">весь текст Hello будет токеном для пакета «tm» и сравнивается с слово hello в словаре мнений hello.</span><span class="sxs-lookup"><span data-stu-id="47b8e-143">hello whole text will be tokenized by “tm” package and compared with hello word in hello sentiment dictionary.</span></span> <span data-ttu-id="47b8e-144">Наконец оценка будет вычисляться путем добавления hello вес каждого Субъективная слова в тексте hello.</span><span class="sxs-lookup"><span data-stu-id="47b8e-144">Finally, a score will be calculated by adding hello weight of each subjective word in hello text.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="47b8e-145">Ход эксперимента:</span><span class="sxs-lookup"><span data-stu-id="47b8e-145">Experiment flow:</span></span>
![Ход эксперимента][2]

#### <a name="module-1"></a><span data-ttu-id="47b8e-147">Модуль 1:</span><span class="sxs-lookup"><span data-stu-id="47b8e-147">Module 1:</span></span>
    # Map 1-based optional input ports toovariables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a><span data-ttu-id="47b8e-148">Установка пакета функций хэширования</span><span class="sxs-lookup"><span data-stu-id="47b8e-148">Install hash package</span></span>
    install.packages("src/hash_2.2.6.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("hash", lib.loc = ".", logical.return = TRUE, verbose = TRUE)
    library(tm)
    library(stringr)

    #create sentiment dictionary
    negation_word <- c("not","nor", "no")
    result <- c()
    sent_dict <- hash()
    sent_dict <- hash(sent_dict_data$word, sent_dict_data$polarity)

    #  Compute sentiment score for each document
    for (m in 1:nrow(dataset2)){
    polarity_ratio <- 0
    polarity_total <- 0
    not <- 0
    sentence <- tolower(dataset2[m,1])
    if (nchar(sentence) > 0){
        token_array <- scan_tokenizer(sentence)
        for (j in 1:length(token_array)){
            word = str_replace_all(token_array[j], "[^[:alnum:]]", "")
            for (k in 1:length(negation_word)){
              if (word == negation_word[k]){
                not <- (not+1) %% 2

              }
            }
            if (word != ""){
                if (!is.null(sent_dict[[word]])){
                  polarity_ratio <- polarity_ratio + (-2*not+1)*sent_dict[[word]]
                  polarity_total <- polarity_total + abs(sent_dict[[word]])
                }
            }

        }
    }
    if (polarity_total > 0){
        result <- c(result, polarity_ratio/polarity_total)
    }else{
        result<- c(result,0)
    }
    }

    # Sample operation
    data.set <- data.frame(result)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("data.set")



## <a name="limitations"></a><span data-ttu-id="47b8e-149">Ограничения</span><span class="sxs-lookup"><span data-stu-id="47b8e-149">Limitations</span></span>
<span data-ttu-id="47b8e-150">С точки зрения алгоритма анализ мнений лексики является средством анализа основная идея не работают быстрее, чем метод классификации hello для отдельных полей.</span><span class="sxs-lookup"><span data-stu-id="47b8e-150">From an algorithm perspective, lexicon-based sentiment analysis is a general sentiment analysis tool, which may not perform better than hello classification method for specific fields.</span></span> <span data-ttu-id="47b8e-151">Задача Hello отрицания не также решается с.</span><span class="sxs-lookup"><span data-stu-id="47b8e-151">hello negation problem is not well dealt with.</span></span> <span data-ttu-id="47b8e-152">Мы внесли несколько слов отрицания в код программы, однако вместо этого следовало бы использовать словарь отрицаний в сочетании с некоторым набором правил.</span><span class="sxs-lookup"><span data-stu-id="47b8e-152">We hardcode several negation words in our program, but a better way is using a negation dictionary and build some rules.</span></span> <span data-ttu-id="47b8e-153">веб-службу Hello лучшие короткие и простые предложения, например твитов и сообщениях Facebook, чем длинные и сложные предложения, например Amazon отзывы.</span><span class="sxs-lookup"><span data-stu-id="47b8e-153">hello web service performs better on short and simple sentences, such as tweets and Facebook posts, than on long and complex sentences such as Amazon reviews.</span></span> 

## <a name="faq"></a><span data-ttu-id="47b8e-154">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="47b8e-154">FAQ</span></span>
<span data-ttu-id="47b8e-155">Часто задаваемые вопросы о потреблении hello веб-службы или публикации toohello Azure Marketplace в разделе [здесь](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="47b8e-155">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


