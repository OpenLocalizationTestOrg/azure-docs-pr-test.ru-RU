---
title: "Лексический анализ тональности (устаревшая версия) | Документация Майкрософт"
description: "Сведения о лексическом анализе тональности (устаревшая версия)."
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
redirect_document_id: TRUE
ms.openlocfilehash: 7bc80a1e1067296528eca1a843ea30b0c27af616
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-lexicon-based-sentiment-analysis"></a><span data-ttu-id="1bdda-103">Лексический анализ тональности (устаревшая версия)</span><span class="sxs-lookup"><span data-stu-id="1bdda-103">(deprecated) Lexicon Based Sentiment Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="1bdda-104">Работа Microsoft DataMarket прекращается, и этот API больше не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="1bdda-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="1bdda-105">Много полезных примеров экспериментов и API можно найти в [коллекции Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="1bdda-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="1bdda-106">Дополнительные сведения о коллекции см. в статье [Поиск ресурсов в коллекции Cortana Intelligence и обмен ими](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="1bdda-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="1bdda-107">Как можно измерить мнения пользователей и их отношение к торговым маркам или темам в социальных сетях, например публикациях в Facebook, твитах, рецензиях и т. д.?</span><span class="sxs-lookup"><span data-stu-id="1bdda-107">How can you measure users’ opinions and attitudes toward brands or topics in online social networks, such as Facebook posts, tweets, reviews, etc.?</span></span> <span data-ttu-id="1bdda-108">Анализ мнений позволяет изучать такие вопросы.</span><span class="sxs-lookup"><span data-stu-id="1bdda-108">Sentiment analysis provides a method for analyzing such questions.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="1bdda-109">Можно выделить два основных метода анализа мнений.</span><span class="sxs-lookup"><span data-stu-id="1bdda-109">There are generally two methods for sentiment analysis.</span></span> <span data-ttu-id="1bdda-110">Один из них — алгоритм контролируемого обучения, а другой можно рассматривать как неконтролируемое.</span><span class="sxs-lookup"><span data-stu-id="1bdda-110">One is using a supervised learning algorithm, and the other can be treated as unsupervised learning.</span></span> <span data-ttu-id="1bdda-111">Алгоритм контролируемого обучения строит модель классификации на основе большой совокупности данных с примечаниями.</span><span class="sxs-lookup"><span data-stu-id="1bdda-111">A supervised learning algorithm generally builds a classification model on a large annotated corpus.</span></span> <span data-ttu-id="1bdda-112">Его точность в основном зависит от качества примечаний, а процесс обучения обычно занимает долгое время.</span><span class="sxs-lookup"><span data-stu-id="1bdda-112">Its accuracy is mainly based on the quality of the annotation, and usually the training process will take a long time.</span></span> <span data-ttu-id="1bdda-113">Кроме того, при применении этого алгоритма к другой предметной области результат, как правило, оказывается не очень хорошим.</span><span class="sxs-lookup"><span data-stu-id="1bdda-113">Besides that, when we apply the algorithm to another domain, the result is usually not good.</span></span> <span data-ttu-id="1bdda-114">В отличие от контролируемого обучения, лексический метод неконтролируемого обучения использует словарь мнений и не требует хранения большого объема данных и обучения, что существенно ускоряет весь процесс.</span><span class="sxs-lookup"><span data-stu-id="1bdda-114">Compared to supervised learning, lexicon-based unsupervised learning uses a sentiment dictionary, which doesn’t require storing a large data corpus and training - which makes the whole process much faster.</span></span> 

<span data-ttu-id="1bdda-115">Наша [служба](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) создана на основе MPQA Subjectivity Lexicon (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), одного из самых распространенных лексиконов субъективных мнений.</span><span class="sxs-lookup"><span data-stu-id="1bdda-115">Our [service](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) is built on the MPQA Subjectivity Lexicon (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), which is one of the most commonly used subjectivity lexicons.</span></span> <span data-ttu-id="1bdda-116">Он включает 5097 слов для отрицательной оценки и 2533 слова — для положительной.</span><span class="sxs-lookup"><span data-stu-id="1bdda-116">There are 5097 negative and 2533 positive words in MPQA.</span></span> <span data-ttu-id="1bdda-117">Все они обозначены как имеющие сильную или слабую полярность.</span><span class="sxs-lookup"><span data-stu-id="1bdda-117">And all of these words are annotated as strong or weak polarity.</span></span> <span data-ttu-id="1bdda-118">Весь массив предоставляется на условиях универсальной общедоступной лицензии GNU.</span><span class="sxs-lookup"><span data-stu-id="1bdda-118">The whole corpus is under GNU General Public License.</span></span> <span data-ttu-id="1bdda-119">Веб-службу можно применять к любым коротким фразам, таким как твиты и записи в Facebook.</span><span class="sxs-lookup"><span data-stu-id="1bdda-119">The web service can be applied to any short sentences, such as tweets and Facebook posts.</span></span> 

> <span data-ttu-id="1bdda-120">Пользователи могут работать с этой веб-службой через мобильное приложение, веб-сайт или даже локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="1bdda-120">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer for example.</span></span> <span data-ttu-id="1bdda-121">Веб-служба также служит примером того, как машинное обучение Azure можно использовать для создания веб-служб на основе кода R.</span><span class="sxs-lookup"><span data-stu-id="1bdda-121">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="1bdda-122">Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="1bdda-122">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="1bdda-123">Затем веб-службу можно опубликовать в Azure Marketplace, и ее смогут применять пользователи и устройства по всему миру, при этом автору веб-службы не придется настраивать инфраструктуру.</span><span class="sxs-lookup"><span data-stu-id="1bdda-123">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="1bdda-124">Использование веб-службы</span><span class="sxs-lookup"><span data-stu-id="1bdda-124">Consumption of web service</span></span>
<span data-ttu-id="1bdda-125">Входными данными может быть любой текст, но веб-служба показывает лучшие результаты для коротких фраз.</span><span class="sxs-lookup"><span data-stu-id="1bdda-125">The input data can be any text, but the web service works better with short sentences.</span></span> <span data-ttu-id="1bdda-126">На выходе она выдает числовое значение в диапазоне от -1 до 1.</span><span class="sxs-lookup"><span data-stu-id="1bdda-126">The output is a numeric value between -1 and 1.</span></span> <span data-ttu-id="1bdda-127">Любое значение меньше 0 означает отрицательный характер текста, больше 0 — положительный.</span><span class="sxs-lookup"><span data-stu-id="1bdda-127">Any value below 0 denotes that the sentiment of the text is negative; positive if above 0.</span></span> <span data-ttu-id="1bdda-128">Абсолютное значение результата определяет степень уверенности данного мнения.</span><span class="sxs-lookup"><span data-stu-id="1bdda-128">The absolute value of the result denotes the strength of the associated sentiment.</span></span> 

> <span data-ttu-id="1bdda-129">Эта служба, размещенная в Azure Marketplace, является службой на основе OData. Вызвать ее можно методами POST и GET.</span><span class="sxs-lookup"><span data-stu-id="1bdda-129">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="1bdda-130">Есть несколько способов использования службы в автоматическом режиме (см. пример приложения [здесь](http://microsoftazuremachinelearning.azurewebsites.net/)).</span><span class="sxs-lookup"><span data-stu-id="1bdda-130">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="1bdda-131">Начало кода C# для использования веб-службы:</span><span class="sxs-lookup"><span data-stu-id="1bdda-131">Starting C# code for web service consumption:</span></span>
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



<span data-ttu-id="1bdda-132">Входные данные: "Сегодня хороший день".</span><span class="sxs-lookup"><span data-stu-id="1bdda-132">The input is “Today is a good day.”</span></span> <span data-ttu-id="1bdda-133">Служба возвращает значение 1, указывая на положительное мнение, высказанное в исходной фразе.</span><span class="sxs-lookup"><span data-stu-id="1bdda-133">The output is “1”, which indicates a positive sentiment associated with the input sentence.</span></span> 

## <a name="creation-of-web-service"></a><span data-ttu-id="1bdda-134">Создание веб-службы</span><span class="sxs-lookup"><span data-stu-id="1bdda-134">Creation of web service</span></span>
> <span data-ttu-id="1bdda-135">Эта веб-служба была создана с помощью системы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="1bdda-135">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="1bdda-136">Чтобы получить бесплатную пробную версию и вводные видеоматериалы по созданию экспериментов и [публикации веб-служб](machine-learning-publish-a-machine-learning-web-service.md), посетите веб-страницу [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="1bdda-136">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="1bdda-137">Ниже приведен снимок экрана эксперимента, в результате которого была создана веб-служба, и пример кода для каждого модуля в эксперименте.</span><span class="sxs-lookup"><span data-stu-id="1bdda-137">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="1bdda-138">В службах машинного обучения Azure создан пустой эксперимент.</span><span class="sxs-lookup"><span data-stu-id="1bdda-138">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="1bdda-139">На рисунке ниже показан ход эксперимента лексического анализа мнений.</span><span class="sxs-lookup"><span data-stu-id="1bdda-139">The figure below shows the experiment flow of lexicon-based sentiment analysis.</span></span> <span data-ttu-id="1bdda-140">Файл sent_dict.csv — это лексикон субъективных мнений MPQA, который передается на ввод модуля [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="1bdda-140">The “sent_dict.csv” file is the MPQA subjectivity lexicon, and is set as one of the inputs of [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="1bdda-141">Еще один входной аргумент — проверяемый образец из набора данных обзоров Amazon, для которого была проведена выборка, изменены названия столбцов и выполнено разделение.</span><span class="sxs-lookup"><span data-stu-id="1bdda-141">Another input is a sampled review from the Amazon review dataset for test, where we performed selection, column name modification, and split operations.</span></span> <span data-ttu-id="1bdda-142">Для хранения в памяти лексикона субъективных мнений и ускорения расчета оценки мы использовали пакет функций хэширования.</span><span class="sxs-lookup"><span data-stu-id="1bdda-142">We use a hash package to store the subjectivity lexicon in the memory and accelerate the score computation process.</span></span> <span data-ttu-id="1bdda-143">Пакет tm выполняет разметку текста, после чего он сравнивается со словом в словаре мнений.</span><span class="sxs-lookup"><span data-stu-id="1bdda-143">The whole text will be tokenized by “tm” package and compared with the word in the sentiment dictionary.</span></span> <span data-ttu-id="1bdda-144">Итоговая оценка рассчитывается путем применения весовой характеристики каждого слова субъективной оценки в тексте.</span><span class="sxs-lookup"><span data-stu-id="1bdda-144">Finally, a score will be calculated by adding the weight of each subjective word in the text.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="1bdda-145">Ход эксперимента:</span><span class="sxs-lookup"><span data-stu-id="1bdda-145">Experiment flow:</span></span>
![Ход эксперимента][2]

#### <a name="module-1"></a><span data-ttu-id="1bdda-147">Модуль 1:</span><span class="sxs-lookup"><span data-stu-id="1bdda-147">Module 1:</span></span>
    # Map 1-based optional input ports to variables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a><span data-ttu-id="1bdda-148">Установка пакета функций хэширования</span><span class="sxs-lookup"><span data-stu-id="1bdda-148">Install hash package</span></span>
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

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("data.set")



## <a name="limitations"></a><span data-ttu-id="1bdda-149">Ограничения</span><span class="sxs-lookup"><span data-stu-id="1bdda-149">Limitations</span></span>
<span data-ttu-id="1bdda-150">С алгоритмической точки зрения лексический анализ мнений — это общий инструмент анализа мнений, показывающий результаты не лучше, чем метод классификации на основе определенных полей.</span><span class="sxs-lookup"><span data-stu-id="1bdda-150">From an algorithm perspective, lexicon-based sentiment analysis is a general sentiment analysis tool, which may not perform better than the classification method for specific fields.</span></span> <span data-ttu-id="1bdda-151">Проблема отрицания не была решена качественным образом.</span><span class="sxs-lookup"><span data-stu-id="1bdda-151">The negation problem is not well dealt with.</span></span> <span data-ttu-id="1bdda-152">Мы внесли несколько слов отрицания в код программы, однако вместо этого следовало бы использовать словарь отрицаний в сочетании с некоторым набором правил.</span><span class="sxs-lookup"><span data-stu-id="1bdda-152">We hardcode several negation words in our program, but a better way is using a negation dictionary and build some rules.</span></span> <span data-ttu-id="1bdda-153">Веб-служба показывает лучшие результаты на коротких и простых предложениях, таких как твиты и записи в Facebook, чем на длинных и сложных предложениях, таких как обзоры Amazon.</span><span class="sxs-lookup"><span data-stu-id="1bdda-153">The web service performs better on short and simple sentences, such as tweets and Facebook posts, than on long and complex sentences such as Amazon reviews.</span></span> 

## <a name="faq"></a><span data-ttu-id="1bdda-154">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="1bdda-154">FAQ</span></span>
<span data-ttu-id="1bdda-155">Ознакомиться с часто задаваемыми вопросами по использованию веб-службы и публикации в Azure Marketplace можно [здесь](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="1bdda-155">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


