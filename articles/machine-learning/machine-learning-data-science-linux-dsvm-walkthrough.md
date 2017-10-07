---
title: "Научные aaaData на hello виртуальная машина анализа данных Linux | Документы Microsoft"
description: "Как tooperform несколько науки общих данных задач с hello обработки и анализа данных виртуальной Машины с Linux."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 34ef0b10-9270-474f-8800-eecb183bbce4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev;paulsh
ms.openlocfilehash: 78764825f2e834fa4ddb7fdc2f59418dbe736e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-on-hello-linux-data-science-virtual-machine"></a>Обработки и анализа данных на hello виртуальная машина анализа данных Linux
В этом пошаговом руководстве показано, как tooperform несколько науки общих данных задач с hello обработки и анализа данных виртуальной Машины с Linux. Hello виртуальной машины обработки и анализа данных Linux (DSVM) — это изображение виртуальной машины, доступный в Azure, предварительно установлены с набор средств, которые обычно используются для анализа данных и машинного обучения. Hello ключевых компонентов программного обеспечения перечислено в hello [подготовки hello виртуальная машина анализа данных Linux](machine-learning-data-science-linux-dsvm-intro.md) раздела. Hello образа виртуальной Машины позволяет легко tooget начал делать обработки и анализа данных в минутах, без необходимости tooinstall и настройка каждого из средств hello по отдельности. Можно легко масштабировать hello виртуальной Машины, при необходимости и остановите ее не во время работы. Таким образом, это гибкий и экономичный ресурс.

Hello задач обработки и анализа данных, представленный в данном руководстве, выполните hello действия, описанные в hello [процесс обработки и анализа данных для команды](https://azure.microsoft.com/documentation/learning-paths/data-science-process/). Этот процесс предоставляет систематический подход toodata обработки и анализа, созданному tooeffectively совместно работать над hello жизненным циклом разработки интеллектуальных приложений специалистами по анализу данных. процесс обработки и анализа данных Hello также предоставляет платформу последовательной обработки и анализа данных, может следовать отдельного.

В ходе анализа hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) набора данных в этом пошаговом руководстве. Это набор адресов электронной почты, которые помечены как нежелательной почты или ham (то есть они не являются нежелательной почты), и также содержит некоторые статистические данные на содержимом hello hello адресов электронной почты. Статистика Hello включены Далее рассматриваются в hello, кроме одного раздела.

## <a name="prerequisites"></a>Предварительные требования
Прежде чем использовать виртуальная машина анализа данных Linux, необходимо иметь следующие hello.

* **Подписка Azure**. Если у вас ее нет, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/).
* [**Виртуальная машина Linux для обработки и анализа данных.**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm) Сведения о подготовке этой виртуальной Машины в разделе [подготовки hello виртуальная машина анализа данных Linux](machine-learning-data-science-linux-dsvm-intro.md).
* Клиент [X2Go](http://wiki.x2go.org/doku.php), установленный на компьютере, и открытый сеанс XFCE. Сведения об установке и настройке **клиента X2Go** см. в разделе [Установка и настройка клиента X2Go](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client). 
* **Учетная запись машинного обучения Azure**. Если вы уже нет, зарегистрироваться для нового на hello [AzureML Домашняя страница](https://studio.azureml.net/). Нет toohelp уровень свободного использования, вам начать работу.

## <a name="download-hello-spambase-dataset"></a>Скачать набор данных spambase hello
Hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) набор данных является относительно небольшой набор данных, который содержит только 4601 примеры. Это toouse компактные при демонстрации того, что некоторые ключевые функции hello hello ВМ обработки и анализа данных, как оно сохраняет потребности в ресурсах hello небольшой.

> [!NOTE]
> В этом пошаговом руководстве используется виртуальная машина Linux размера D2 v2. Этот размер DSVM может обрабатывать hello процедуры в этом пошаговом руководстве.
>
>

Если вам требуется больше места для хранения, можно создать дополнительные диски и присоединить их tooyour виртуальной Машины. Эти диски с использованием постоянного хранилища Azure, поэтому их данные сохраняются даже в том случае, если выполняется повторная Подготовка hello server из-за tooresizing или завершение работы. tooadd диск и присоединить ее tooyour виртуальной Машины, следуйте инструкциям в разделе hello [добавить диск tooa ВМ Linux](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Эти шаги использовать интерфейс командной строки Azure (Azure CLI), который уже установлен на hello DSVM hello. Поэтому эти процедуры можно сделать из hello самой ВМ. Другой параметр tooincrease хранилище — toouse [файлы Azure](../storage/files/storage-how-to-use-files-linux.md).

данные hello toodownload, откройте окно терминала и выполните следующую команду:

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

загруженный файл Hello не иметь строку заголовка, поэтому давайте создадим другой файл, который имеет заголовка. Запустите файл toocreate этой команды с соответствующими заголовками hello:

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

Затем объединить два файла hello вместе с hello команды:

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

Hello набор данных содержит несколько типов статистических данных на все сообщения электронной почты:

* Столбцы, например ***word\_freq\_WORD*** указывает процент hello слова в сообщении электронной почты hello, соответствующие *WORD*. Например если *word\_freq\_сделать* имеет значение 1, а затем были 1% от всех слов в сообщении электронной почты hello *сделать*.
* Столбцы, например ***char\_freq\_CHAR*** указывает процент hello все символы hello электронной почты, которые были *CHAR*.
* ***Прописная\_запуска\_длина\_длинного*** имеет длину самой длинной hello последовательности прописных букв.
* ***Прописная\_запуска\_длина\_среднее*** — hello Средняя продолжительность всех последовательностей прописных букв.
* ***Прописная\_запуска\_длина\_общее*** — hello общая длина всех последовательностей прописных букв.
* ***нежелательной почты*** указывает hello электронной почты был считаются ли Нежелательная почта или нет (1 = нежелательной почты, 0 = не нежелательной почты).

## <a name="explore-hello-dataset-with-microsoft-r-open"></a>Просмотр набора данных hello с Microsoft R Open
Давайте исследовать данные hello и выполнять некоторые основные машинного обучения с виртуальной Машины для обработки и анализа данных поставляется с hello R. [Microsoft R Open](https://mran.revolutionanalytics.com/open/) предварительно установлен. Hello многопоточных математические библиотеки в этой версии R обеспечивают более высокую производительность, чем различные версии одним потоком. Microsoft R Open также предоставляет повторяемость с помощью моментального снимка репозитория пакетов CRAN hello.

примеры, в данном пошаговом руководстве hello клонов кода tooget копии hello **Azure-Machine-обучения--обработки и анализа данных** репозитория git, с помощью которой уже установлены на hello виртуальной Машины. Из командной строки git hello выполните следующую команду:

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

Откройте окно терминала и начать новый сеанс R с помощью интерактивной консоли hello R.

> [!NOTE]
> RStudio также можно использовать для следующих процедур hello. tooinstall RStudio, выполнение этой команды на терминала:`./Desktop/DSVM\ tools/installRStudio.sh`
>
>

tooimport hello данные и настройки среды hello, выполните:

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

toosee сводные статистические данные о каждом столбце:

    summary(data)

Новое представление данных hello:

    str(data)

Отображается тип каждой переменной hello и hello первые несколько значений в наборе данных hello.

Hello *нежелательной почты* столбца было прочитано как целое число, но это фактически категориальные переменной (или коэффициент). tooset его тип:

    data$spam <- as.factor(data$spam)

toodo некоторые исследовательский анализ, используйте hello [ggplot2](http://ggplot2.org/) пакета популярные библиотеки построения для R, уже установлены на hello виртуальной Машины. Обратите внимание, из сводных данных hello, показанным ранее, что у нас есть сводные статистические данные о частоте hello hello восклицательный знак. Давайте построения этих частот здесь с hello, следующие команды:

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

Так как строка hello ноль наклона рисунка hello, удалим его:

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

Выше показателя 1 наблюдается необычная плотность. Давайте взглянем только на эти данные.

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

Затем разобьем их на наборы с обычной и нежелательной почтой.

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

Эти примеры должны позволяют toomake аналогичные точечное hello tooexplore другие столбцы Здравствуйте, содержащиеся в них данные.

## <a name="train-and-test-an-ml-model"></a>Обучение и тестирование модели машинного обучения
Теперь давайте обучения ряд машинного обучения моделей электронные сообщения hello tooclassify hello набора данных как содержащий либо span или ham. В этом разделе мы обучим модель дерева принятия решений и модель случайного леса, а затем протестируем точность получаемых прогнозов.

> [!NOTE]
> пакет Hello rpart (рекурсивное секционирование и для дерева регрессии), используемый в после кода hello уже установлены на hello ВМ обработки и анализа данных.
>
>

Во-первых давайте разбиение hello набора данных на обучающие и проверочные наборы:

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

А затем создать hello tooclassify дерева принятия решений сообщения электронной почты.

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

Ниже приведен результат hello.

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

toodetermine, насколько хорошо выполняется на обучение hello задать, использовать hello, следующий код:

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

насколько хорошо toodetermine выполняемых в тестовом наборе hello:

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

Теперь давайте испробуем модель случайного леса. Случайные леса обучения множество дерева принятия решений и выведите класс, который является режимом hello классификаций hello из всех деревьев принятия решений отдельных hello. Они предоставляют больше возможностей машинного обучения подход, как они исправления для hello тенденцию toooverfit модели дерева принятия решений обучающий набор данных.

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-tooazure-ml"></a>Развертывание модели tooAzure машинного Обучения
[Студия машинного обучения](https://studio.azureml.net/) (AzureML) — это облачная служба, что делает его легко toobuild и развертывания моделей прогнозирования. Одной из удобных функций hello AzureML является его toopublish возможность работать любой R в качестве веб-службы. Hello AzureML R-пакет развертывания легко toodo прямо с нашей сеанса R на становится hello DSVM.

toodeploy hello код дерева принятия решений hello в предыдущем разделе, необходимо toosign в tooAzure студии машинного обучения. Требуется идентификатор вашей рабочей области и toosign маркер авторизации в. toofind эти значения и переменные AzureML hello инициализации с ними:

Выберите **параметры** в левом меню hello. Укажите значение в поле **Идентификатор рабочей области**. ![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)

Выберите **маркерах авторизации** hello издержек на меню и обратите внимание на **основного маркера авторизации**.![ 3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)

Hello нагрузки **AzureML** пакета и задайте значения переменных hello своим Идентификатором маркера и в рабочей области во время сеанса R на hello DSVM:

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


Давайте упростить toomake hello модели проще tooimplement этой демонстрации. Выберите три переменные hello в hello принятия решений ближайший toohello корневой элемент дерева и создания нового дерева, используя только эти три переменные:

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

Мы должны Прогнозирующая функция, которая принимает в качестве входных данных функции hello и возвращает hello прогнозируемые значения:

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

Публикация hello predictSpam функция tooAzureML с помощью hello **publishWebService** функции:

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

Эта функция принимает hello **predictSpam** функционировать, создает веб-службы с именем **spamWebService** с определенных входных и выходных данных и возвращает сведения о новой конечной точки hello.

Просмотр сведений о hello публикации веб-службы, включая его API конечной точки и ключами доступа с помощью команды hello:

    spamWebService[[2]]

tootry его на hello первые 10 строк hello проверочного набора:

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a>Использование других доступных средств
Hello оставшихся разделах показано, как некоторые средства hello установлены на toouse hello обработки и анализа данных виртуальной Машины с Linux. Ниже приведен список hello обсуждаются средства:

* XGBoost;
* Python;
* Jupyterhub;
* Rattle;
* PostgreSQL и Squirrel SQL;
* хранилище данных SQL Server.

## <a name="xgboost"></a>XGBoost;
[XGBoost](https://xgboost.readthedocs.org/en/latest/) — инструмент, предоставляющий быструю и точную реализацию увеличивающегося дерева.

    require(xgboost)
    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

    bst <- xgboost(data = data.matrix(trainSet[,0:57]), label = trainSet$spam, nthread = 2, nrounds = 2, objective = "binary:logistic")

    pred <- predict(bst, data.matrix(testSet[, 0:57]))
    accuracy <- 1.0 - mean(as.numeric(pred > 0.5) != testSet$spam)
    print(paste("test accuracy = ", accuracy))

Его можно вызвать из командной строки или Python.

## <a name="python"></a>Python
Для разработки приложений с помощью Python hello распределения Anaconda Python 2.7 и 3.5 были установлены в hello DSVM.

> [!NOTE]
> включает дистрибутив Anaconda Hello [Condas](http://conda.pydata.org/docs/index.html), который может быть пользовательской среды используется toocreate для Python, имеют разные версии или пакеты, установленные в них.
>
>

Давайте чтения в некоторой части набора данных spambase hello и классифицировать hello сообщения электронной почты с машины опорных векторов в scikit-Дополнительные сведения:

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

toomake прогнозов:

    clf.predict(X.ix[0:20, :])

tooshow как toopublish AzureML конечной точки, давайте создать простую модель hello три переменные, как мы делали, когда мы ранее опубликованные модели hello R.

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

tooAzureML модели hello toopublish:

    # Publish hello model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about hello resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call hello model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> Это доступно только для Python 2.7 и еще не поддерживается для версии 3.5. Выполните код с использованием **/anaconda/bin/python2.7**.
>
>

## <a name="jupyterhub"></a>Jupyterhub;
Дистрибутив Anaconda Hello в hello DSVM поставляется с записной книжке Jupyter, код Python, R или Юлия tooshare кросс платформенных среды и анализа. Hello книжке Jupyter осуществляется с помощью JupyterHub. Для входа введите учетные данные локального пользователя Linux по адресу ***https://\<DNS-имя или IP-адрес ВМ\>:8000/***. Все файлы конфигурации JupyterHub находятся в каталоге **/etc/jupyterhub**.

Некоторые примеры записных книжек уже установлены на hello виртуальной Машины:

* В разделе hello [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) для записной книжке образец Python.
* См. [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) для примера записной книжки **R**.
* В разделе hello [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) еще один пример **Python** ноутбука.

> [!NOTE]
> Hello Юлия языка также доступна из командной строки hello hello обработки и анализа данных виртуальной Машины с Linux.
>
>

## <a name="rattle"></a>Rattle
[Диска](https://cran.r-project.org/web/packages/rattle/index.html) (hello аналитические средства R tooLearn легко) — это графическое средство R для интеллектуального анализа данных. Он имеет интуитивно понятный интерфейс, который позволяет легко tooload, исследовать и преобразования данных и построения и оценивать модели.  статья Hello [диска: GUI интеллектуального анализа данных для R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) Пошаговое руководство, демонстрируются ее возможности.

Установка и запуск диска с hello, следующие команды:

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> Установка на hello DSVM не требуется. Но погремушка могут потребоваться дополнительные пакеты tooinstall при загрузке.
>
>

В Rattle используется интерфейс на основе вкладок. Большинство hello вкладок соответствует toosteps в hello [процесса обработки и анализа данных](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), такие как загрузка данных или его исследование. процесс обработки и анализа данных Hello поступает из левой tooright по вкладкам hello. Но hello последнего вкладка содержит журнал hello R команд, выполняемых погремушка.

tooload и настройки набора данных hello:

* файл hello tooload, выберите hello **данные** вкладке, нажмите
* Выберите селектор hello рядом слишком**Filename** и выберите **spambaseHeaders.data**.
* файл tooload hello. Выберите **Execute** в верхней строке hello кнопок. Должна появиться сводка каждого столбца, включая его тип данных, указанных входных данных, целевой объект или другой тип переменной и hello количество уникальных значений.
* Погремушка правильно идентифицировала hello **нежелательной почты** столбца в качестве целевой hello. Выберите hello столбца нежелательной почты, а затем набор hello **целевой тип данных** слишком**Categoric**.

данные hello tooexplore:

* Выберите hello **Проводник** вкладки.
* Нажмите кнопку **сводки**, затем **Execute**, toosee некоторые сведения о типах переменной hello и некоторые сводные статистические данные.
* tooview другие статистические данные о каждой переменной, выберите другие параметры, такие как **описания** или **основы**.

Hello **Проводник** вкладке можно также toogenerate множество полезных графиков. tooplot гистограммы hello данных:

* Установите флажок **Distributions**(Дистрибутивы).
* Выберите **Histogram** (Гистограмма) для выражений **word_freq_remove** и **word_freq_you**.
* Нажмите кнопку **Execute**(Выполнить). Вы увидите, что оба плотность отображаются в окне одной диаграммы, где было ясно, это слово hello, «вы» гораздо более часто появляется в сообщениях электронной почты, чем «удалить».

График Hello корреляции также представляют интерес. toocreate один:

* Выберите **корреляции** как hello **тип**, затем
* Нажмите кнопку **Execute**(Выполнить).
* Rattle рекомендует использовать не более 40 переменных. Выберите **Да** tooview hello построения.

Существуют некоторые содержательные корреляции, возникающие: слишком сильно зависят от «технология» «HP» и «лаборатории», например. Также настоятельно коррелирует слишком «650», так как код города hello доноров hello набора данных — 650.

в окне Просмотр hello доступны Hello числовые значения для hello корреляций между словами. Это интересно toonote, например, что «технология» отрицательно связаны с «вы» и «деньги».

Погремушка может преобразовать некоторые распространенные проблемы toohandle hello набора данных. Например, он позволяет функции toorescale, добавить отсутствующие значения, обработать выбросы и удаления переменных и наблюдений всего отсутствующих данных. Rattle также может определить правила взаимосвязей между наблюдениями и (или) переменными. Эти вкладки не рассматриваются в этом вводном пошаговом руководстве.

В Rattle также можно выполнять анализ кластеров. Давайте исключить некоторые функции toomake hello вывода проще tooread. На hello **данные** выберите **Ignore** Далее tooeach переменных hello, за исключением следующих десяти элементов:

* word_freq_hp;
* word_freq_technology;
* word_freq_george;
* word_freq_remove;
* word_freq_your;
* word_freq_dollar;
* word_freq_money;
* capital_run_length_longest;
* word_freq_business;
* spam

Затем вернитесь toohello **кластера** выберите **KMeans**и набор hello *число кластеров* too4. Затем нажмите кнопку **Execute** (Выполнить). Hello результаты отображаются в окне вывода hello. В одном кластере часто встречается слово "george" и "hp". Скорее всего, это деловое сообщение электронной почты.

toobuild модели машинного обучения дерева принятия решений простой:

* Выберите hello **модели** вкладке
* Выберите **дерева** как hello **типа**.
* Выберите **Execute** toodisplay дерева hello в текстовой форме hello окно вывода.
* Выберите hello **нарисовать** кнопку tooview графической версии. Это выглядит довольно подобного дерева toohello, были получены ранее с помощью *rpart*.

Один из удобных функций hello погремушка является его способность toorun методов несколько машинного обучения и быстро оценить их. Ниже описана процедура hello.

* Выберите **все** для hello **типа**.
* Нажмите кнопку **Execute**(Выполнить).
* После ее завершения можно щелкнуть любой отдельный **тип**, таких как **SVM**и просмотреть результаты hello.
* Вы также можете сравнить производительность hello hello моделей по результатам проверки hello, заданные с помощью hello **Evaluate** вкладки. Здравствуйте, например, **ошибка матрицы** выбора отображает hello матрицей, общая ошибка и ошибка усредненного класса для каждой модели на наборе проверки hello.
* Вы также можете построить кривые ROC, выполнить анализ чувствительности и выполнить другие оценки модели.

После завершения построения модели, выберите hello **журнала** вкладке tooview hello R средой коде погремушка во время сеанса. Можно выбрать hello **Экспорт** кнопку toosave его.

> [!NOTE]
> В текущем выпуске Rattle есть ошибка. toomodify hello скрипт, или использовать его toorepeat шагов более поздней версии, необходимо вставить символ # поверх * экспортировать этот журнал... * в тексте hello hello журнала.
>
>

## <a name="postgresql--squirrel-sql"></a>PostgreSQL и Squirrel SQL;
Hello DSVM поставляется с PostgreSQL установлен. PostgreSQL — продвинутая реляционная база данных с открытым исходным кодом. В этом разделе показано, как tooload нашей нежелательной почты набора данных в PostgreSQL и только затем запрос.

Перед загрузкой данных hello, требуется проверка пароля tooallow с hello localhost. В окне командной строки:

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

Hello нижней части файла конфигурации hello являются несколько строк, в которых подробно hello разрешенных подключений:

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

Изменить md5 toouse строку hello «IPv4 локальных соединений» вместо ident, поэтому мы можете войти с использованием имени пользователя и пароля:

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

И перезапустите службу postgres hello:

    sudo systemctl restart postgresql

psql toolaunch, интерактивные терминалов для PostgreSQL, как пользователь встроенных postgres hello, выполните следующую команду в командной строке hello.

    sudo -u postgres psql

Создание учетной записи пользователя, с помощью hello же имя пользователя как hello Linux учетной записи, которую вы выполнили вход в качестве и задайте пароль:

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

Затем войти в toopsql учетной записью пользователя:

    psql

И импортировать данные hello в новую базу данных:

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

Теперь давайте изучения данных hello и выполните несколько запросов с помощью **белка SQL**, графическое средство, которое служит для взаимодействия с базами данных через драйвер JDBC.

tooget запущен, запустите белка SQL из меню приложения hello. tooset копирование hello драйвера:

* Выберите **Windows**, а затем — **View Drivers** (Просмотреть драйверы).
* Щелкните **PostgreSQL** правой кнопкой мыши и выберите **Modify Driver** (Изменить драйвер).
* Выберите **Extra Class Path** (Путь к дополнительным классам), а затем щелкните **Добавить**.
* Введите ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** для hello **имя файла** и
* Щелкните **Open**(Открыть).
* Щелкните "Список драйверов", выберите **org.postgresql.Driver** в области **Имя класса** и нажмите кнопку **ОК**.

tooset hello подключения toohello локального сервера:

* Выберите **Windows**, а затем — **View Aliases** (Просмотреть псевдонимы).
* Выберите hello  **+**  toomake кнопку Новый псевдоним.
* Назовите его *нежелательной почты базы данных*, выберите **PostgreSQL** в hello **драйвер** раскрывающегося списка.
* Задать URL-адрес hello слишком*jdbc:postgresql://localhost/spam*.
* Введите *имя пользователя* и *пароль*.
* Нажмите кнопку **ОК**.
* tooopen hello **подключения** окно, дважды щелкните hello ***нежелательной почты базы данных*** псевдоним.
* Нажмите кнопку **Подключиться**.

toorun некоторые запросы:

* Выберите hello **SQL** вкладки.
* Введите простой запрос, например `SELECT * from data;` в текстовом поле запроса hello hello верхней части вкладки SQL hello.
* Нажмите клавишу **Ctrl + Enter** toorun его. По умолчанию SQL белка возвращает hello первые 100 строк из запроса.

Существует множество запросов, можно выполнить tooexplore эти данные. Например, как работает hello частоту слово hello *сделать* нежелательной почты и ham различаются?

    SELECT avg(word_freq_make), spam from data group by spam;

Или Каковы характеристики hello электронной почты, которые часто содержат *3d*?

    SELECT * from data order by word_freq_3d desc;

Большинство сообщений электронной почты, имеющих высокую вхождения *3d* являются внешне нежелательной почты, поэтому он может быть полезной функцией для создания сообщений электронной почты типа hello tooclassify прогнозной модели.

Если требуется tooperform машинного обучения с данными, хранящимися в базе данных PostgreSQL, рассмотрите возможность использования [MADlib](http://madlib.incubator.apache.org/).

## <a name="sql-server-data-warehouse"></a>хранилище данных SQL Server.
Хранилище данных SQL Azure — это развернутая в облаке база данных, способная обрабатывать большие объемы реляционных и нереляционных данных. Дополнительные сведения см. в статье [Что такое хранилище данных SQL Azure?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)

tooconnect toohello данных в хранилище и создайте таблицу hello выполнения hello следующую команду из командной строки:

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

Затем в строке sqlcmd hello:

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

Скопируйте данные с помощью bcp:

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> разрывы строк Hello в загруженном файле hello, стиль Windows, но bcp ожидает стиле UNIX, поэтому необходимо tootell bcp, что при использовании hello флаг - r.
>
>

Выполните запрос с использованием sqlcmd:

    select top 10 spam, char_freq_dollar from spam;
    GO

Запросы также можно выполнять с помощью Squirrel SQL. Аналогичные действия можно использовать для PostgreSQL, с помощью hello MSSQL Server драйвера JDBC, которую можно найти в ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.

## <a name="next-steps"></a>Дальнейшие действия
Обзор разделы с пошаговыми руководствами hello задачами, которые составляют hello процесса обработки и анализа данных в Azure см. в разделе [процесс обработки и анализа данных для команды](http://aka.ms/datascienceprocess).

Описание других пошаговых руководств начала до конца, демонстрирующих hello инструкциям hello командного процесса обработки и анализа данных для конкретных сценариев см. в разделе [пошаговые руководства командного процесса обработки и анализа данных](data-science-process-walkthroughs.md). Пошаговые руководства Hello также показывают, как облачные toocombine и локальных средств и служб в рабочий процесс или конвейера toocreate интеллектуальной приложения.
