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
# <a name="deprecated-lexicon-based-sentiment-analysis"></a>Лексический анализ тональности (устаревшая версия)

> [!NOTE]
> Hello Microsoft DataMarket прекращено, и этот API устарел. 
> 
> Можно найти множество полезный пример экспериментов и API-интерфейсы в hello [коллекции аналитики Cortana](http://gallery.cortanaintelligence.com). Дополнительные сведения о коллекции hello. в разделе [общего ресурса и поиска ресурсов в коллекции Cortana аналитики hello](machine-learning-gallery-how-to-use-contribute-publish.md).

Как можно измерить мнения пользователей и их отношение к торговым маркам или темам в социальных сетях, например публикациях в Facebook, твитах, рецензиях и т. д.? Анализ мнений позволяет изучать такие вопросы.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Можно выделить два основных метода анализа мнений. Один с помощью алгоритма обучения с учителем и hello другие могут рассматриваться как неконтролируемого обучения. Алгоритм контролируемого обучения строит модель классификации на основе большой совокупности данных с примечаниями. Точность главным образом основан на качество hello заметки hello и обычно процесс обучения hello займет много времени. Помимо, при применении домена tooanother алгоритм hello, результат hello не обычно. Сравнение toosupervised обучения, лексики основе неконтролируемого обучения использует мнений словаря, который не требует хранения совокупности большие объемы данных и обучения — что делает hello весь процесс гораздо быстрее. 

Наш [службы](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) основана на hello лексики Subjectivity MPQA (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), которое является одним из наиболее часто используемых hello subjectivity словари. Он включает 5097 слов для отрицательной оценки и 2533 слова — для положительной. Все они обозначены как имеющие сильную или слабую полярность. Hello всей совокупности находится в режиме публичной лицензии GNU. Hello веб-службы может быть применен tooany короткое предложения, например твитов и Facebook в блогах. 

> Пользователи могут работать с этой веб-службой через мобильное приложение, веб-сайт или даже локальный компьютер. Но hello hello веб-службы служит также tooserve в качестве примера как машинного обучения Azure можно использовать toocreate веб-служб на основе кода R. Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure. Hello веб-службы может быть опубликованным toohello Azure Marketplace и используемые пользователями и устройствами через Здравствуй, мир без настройки инфраструктуры автором hello hello веб-службы.
> 
> 

## <a name="consumption-of-web-service"></a>Использование веб-службы
Hello входных данных может быть любой текст, но веб-службу hello лучше работает с короткий предложений. Hello выходных данных является числовым значением от -1 до 1. Любое значение меньше 0 обозначает, что мнений hello текста hello является отрицательным; Если это положительное значение больше 0. абсолютное значение результата hello Hello обозначает hello стойкость hello связанные мнений. 

> Эта служба, размещенного на hello Azure Marketplace, — это служба OData; Это может быть вызвана через методы POST или GET. 
> 
> 

Существует несколько способов использования службы hello в автоматическом режиме (пример приложения — [здесь](http://microsoftazuremachinelearning.azurewebsites.net/)).

### <a name="starting-c-code-for-web-service-consumption"></a>Начало кода C# для использования веб-службы:
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



входные данные Hello выглядит «сегодня хорошо день». Hello выводится «1», который указывает положительных отзывов, связанные с входное предложение hello. 

## <a name="creation-of-web-service"></a>Создание веб-службы
> Эта веб-служба была создана с помощью системы машинного обучения Azure. Чтобы получить бесплатную пробную версию и вводные видеоматериалы по созданию экспериментов и [публикации веб-служб](machine-learning-publish-a-machine-learning-web-service.md), посетите веб-страницу [azure.com/ml](http://azure.com/ml). Ниже приведен снимок экрана приветствия эксперимента, созданные для каждого из модулей hello в эксперименте hello hello веб-службы и пример кода.
> 
> 

В службах машинного обучения Azure создан пустой эксперимент. на следующем рисунке Hello показан поток эксперимента hello анализ мнений лексики. файл «sent_dict.csv» Hello лексики subjectivity MPQA hello и задан в качестве одного из входов hello [выполнение скрипта R][execute-r-script]. Другой вход — проверку выборки из набора данных проверки hello Amazon для теста, где выполняется выделение, изменение имени столбца и операцию разбиения. Мы используем лексики subjectivity пакета toostore хэш hello в памяти hello и ускорить процесс вычисления оценка hello. весь текст Hello будет токеном для пакета «tm» и сравнивается с слово hello в словаре мнений hello. Наконец оценка будет вычисляться путем добавления hello вес каждого Субъективная слова в тексте hello. 

### <a name="experiment-flow"></a>Ход эксперимента:
![Ход эксперимента][2]

#### <a name="module-1"></a>Модуль 1:
    # Map 1-based optional input ports toovariables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a>Установка пакета функций хэширования
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



## <a name="limitations"></a>Ограничения
С точки зрения алгоритма анализ мнений лексики является средством анализа основная идея не работают быстрее, чем метод классификации hello для отдельных полей. Задача Hello отрицания не также решается с. Мы внесли несколько слов отрицания в код программы, однако вместо этого следовало бы использовать словарь отрицаний в сочетании с некоторым набором правил. веб-службу Hello лучшие короткие и простые предложения, например твитов и сообщениях Facebook, чем длинные и сложные предложения, например Amazon отзывы. 

## <a name="faq"></a>Часто задаваемые вопросы
Часто задаваемые вопросы о потреблении hello веб-службы или публикации toohello Azure Marketplace в разделе [здесь](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


