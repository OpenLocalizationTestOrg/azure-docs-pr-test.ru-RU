---
title: "Учебник по aaaQuickstart для языка R для машинного обучения | Документы Microsoft"
description: "Используйте этот программирования учебника tooget работы быстро с помощью языка hello R с toocreate студии машинного обучения Azure прогнозирования решения R."
keywords: "краткое руководство, язык r, язык программирования r, руководство по программированию на языке r"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 99a3a0fd-b359-481a-b236-66868deccd96
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9995f8728f4d7bf9a5c15412015e4cf769cdac96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-tutorial-for-hello-r-programming-language-for-azure-machine-learning"></a>Учебник по языку программирования hello R для машинного обучения Azure

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a>Введение
Этот учебник помогает быстро запустить расширение машинного обучения Azure, используя язык программирования hello R. Выполните этот программирования учебника toocreate R, тестирования и выполнять код R в машинном обучении Azure. При работе с учебником, вы создадите законченное решение прогнозирования с помощью языка hello R в машинном обучении Azure.  

Машинное обучение Microsoft Azure содержит множество эффективных модулей машинного обучения и обработки данных. мощный язык R Hello был описан как общепринятый язык глобальной hello аналитики. К счастью аналитики и данных для работы в машинном обучении Azure можно расширить с помощью R. Это сочетание предоставляет гибкость hello и глубокого анализа R. hello масштабируемость и простота использования машинного обучения Azure

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-hello-dataset"></a>Прогнозирование и hello набора данных
Прогнозирование — широко распространенный и чрезвычайно полезный метод аналитики. Распространенные варианты в диапазоне от создать прогноз продаж сезонных элементов, определения оптимальной единиц на складе, toopredicting macroeconomic переменных. Преимущественно при прогнозировании используются модели временных рядов.

Данные временных рядов является данных, в котором значения hello имеют индекс времени. Индекс Hello времени может быть regular, например ежемесячно или каждую минуту или нерегулярным. Модель временных рядов основана на данных временных рядов. язык программирования Hello R содержит гибкую среду и расширенная аналитика для временного ряда данных.

В этом руководстве мы будем использовать данные о производстве молочных продуктов в Калифорнии и ценах на них. Сюда входят ежемесячные данные по hello производства несколько товаров и цене hello milk файловой системы FAT, товарного тест производительности.

Hello данные, используемые в этой статье, а также сценарии R, могут быть [загрузить здесь][download]. Эти данные были первоначально полученные из информации, доступной из hello университета Wisconsin на http://future.aae.wisc.edu/tab/production.html.

### <a name="organization"></a>План
Будет прохождения несколько шагов вы узнаете, как toocreate, тестирование и выполнять код R обработки аналитических и данных в среде машинного обучения Azure hello.  

* Сначала мы рассмотрим hello основы использования языка hello R в студии машинного обучения Azure среде hello.
* Затем мы хода выполнения toodiscussing различные аспекты операций ввода-вывода для данных, код R и графики в среде машинного обучения Azure hello.
* Затем мы формируется hello первую часть наших прогнозирования решение путем создания кода для очистки данных и преобразования данных.
* Наши данные подготовки будет выполнять анализ hello корреляции между несколько переменных hello в наш набор данных.
* Наконец, мы создадим прогнозную модель сезонного временного ряда для молочного производства.

## <a id="mlstudio"></a>Работа с языком R в Студии машинного обучения
В этом разделе представлены некоторые основные вопросы взаимодействия и язык программирования hello R в студии машинного обучения среде hello. язык Hello R предоставляет мощное средство toocreate настроить аналитики и данных манипуляции модулей в среде машинного обучения Azure hello.

Я использую RStudio toodevelop, тестирования и отладки кода R в небольших масштабах. Этот код, который затем вырезать и вставить в [выполнение скрипта R] [ execute-r-script] модуля в студии машинного обучения готов toorun.  

### <a name="hello-execute-r-script-module"></a>Выполнение скрипта R модуля Hello
В студии машинного обучения, R-скриптов, выполняются в hello [выполнение скрипта R] [ execute-r-script] модуля. Пример hello [выполнение скрипта R] [ execute-r-script] модуля в студии машинного обучения, приведенный на рисунке 1.

 ![Язык программирования R: hello выполнение скрипта R модуля, выбранного в студии машинного обучения][1]

*Рисунок 1. Среда студии машинного обучения Hello Отображение выбранного модуля выполнение скрипта R hello.*

Ссылающаяся tooFigure 1, давайте рассмотрим некоторые основные части hello hello студии машинного обучения среду для работы с hello [выполнение скрипта R] [ execute-r-script] модуля.

* модули Hello в эксперименте hello отображаются в центральной области hello.
* Hello верхнюю часть hello правая панель содержит tooview окна и редактирования сценариев R.  
* Hello нижней части правой панели показаны некоторые свойства hello [выполнение скрипта R][execute-r-script]. Журналы ошибок и вывода hello можно просмотреть, щелкнув соответствующий участков hello в этой области.

Мы будем Конечно, обсуждать hello [выполнение скрипта R] [ execute-r-script] более подробно в hello остальной части этого документа.

При работе с более сложными функциями R для изменения, тестирования и отладки кода я рекомендую использовать RStudio. Как и в случае разработки любого программного обеспечения, создавайте код пошагово, отдельными фрагментами, и тестируйте его на небольших, простых проверочных примерах. Вырежьте и вставьте в окно скрипта hello R hello функций [выполнение скрипта R] [ execute-r-script] модуля. Такой подход позволяет tooharness как hello RStudio интегрированной среды разработки (IDE) и hello power машинного обучения Azure.  

#### <a name="execute-r-code"></a>Выполнение кода R
Любой код R в hello [выполнение скрипта R] [ execute-r-script] модуль будет выполняться при запуске эксперимента hello, щелкнув hello **запуска** кнопки. По завершении выполнения флажок будет отображаться на hello [выполнение скрипта R] [ execute-r-script] значок.

#### <a name="defensive-r-coding-for-azure-machine-learning"></a>Защищенное программирование на R для Машинного обучения Azure
При разработке кода на R для, скажем, какой-нибудь веб-службы с помощью Машинного обучения Azure необходимо предусмотреть, как ваш код будет реагировать на непредвиденные входные данные и исключения. ясности toomaintain не включены в hello способ проверки и обработки исключений в большинство примеров кода hello показано. Однако далее я приведу несколько примеров функций, использующих возможности языка R для обработки исключений.  

Если требуется более полную обработку R обработки исключений, рекомендуется прочитать hello соответствующих разделах hello книги по Wickham, перечисленных в [приложение B — Дополнительные материалы](#appendixb).

#### <a name="debug-and-test-r-in-machine-learning-studio"></a>Отладка и тестирование кода R в Студии машинного обучения
tooreiterate, я рекомендую тестирования и отладки кода R в RStudio небольших масштабах. Однако бывают случаи, когда будет необходимо tootrack проблем кода R в hello [выполнение скрипта R] [ execute-r-script] сам. Кроме того, он является хорошей практикой toocheck результатов в студии машинного обучения.

В основном в файл output.log найдены выходные данные hello выполнения кода R и на платформе hello машинного обучения Azure. Дополнительная информация отображается в файле error.log.  

Если во время выполнения кода R в студии машинного обучения происходит ошибка, первое действие должно быть toolook на error.log. Этот файл может содержать полезные ошибки сообщения toohelp понять и исправить ошибки. error.log tooview, если щелкнуть **Просмотр журнала ошибок** на hello **панели «свойства»** для hello [выполнение скрипта R] [ execute-r-script] hello ошибкой.

Например, нужно ли устанавливать hello, выполнив кода R, а также не определено y переменной, в [выполнение скрипта R] [ execute-r-script] модуля:

    x <- 1.0
    z <- x + y

Этот код вызывает ошибку tooexecute, возникающие в случае ошибки. Щелкнув **Просмотр журнала ошибок** на hello **панель свойств** создает hello экран, показанный на рисунке 2.

  ![Всплывающее окно сообщения об ошибке][2]

*Рис. 2. Всплывающее окно сообщения об ошибке*

Похоже, мы должны toolook в файл output.log toosee hello R сообщение. Щелкните hello [выполнение скрипта R] [ execute-r-script] и выберите команду hello **просматривать файл output.log** элемент hello **панели «свойства»** toohello справа. Откроется новое окно браузера, и я вижу следующее hello.

    [Critical]     Error: Error 0063: hello following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

Это сообщение об ошибке содержит исключить неожиданные результаты и четко определяет проблему hello.

значение hello tooinspect любого объекта в R, можно напечатать файл файл output.log toohello этих значений. Hello правил для проверки объектов, значения в основном являются hello же, как и в интерактивном сеансе R. Например при вводе имени переменной в строке значение hello hello объекта будет напечатан toohello файл output.log файла.  

#### <a name="packages-in-machine-learning-studio"></a>Пакеты в Студии машинного обучения
Служба машинного обучения Azure содержит более 350 предустановленных пакетов на языке R. Можно использовать следующий код в hello hello [выполнение скрипта R] [ execute-r-script] tooretrieve модуль список hello предустановлен пакетов.

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

Если вы не понимаете hello последняя строка кода в момент hello, читайте дальше. В hello оставшейся части документа мы активно рассмотрим использование R в среде машинного обучения Azure hello.

### <a name="introduction-toorstudio"></a>Введение tooRStudio
RStudio является широко используемым интегрированной среды разработки для R. Я использую RStudio для редактирования, тестирование и отладка некоторой части кода hello R, используемых в этом кратком руководстве. После тестирования и готов код R, просто копировать и вставлять из редактора RStudio hello в студию машинного обучения [выполнение скрипта R] [ execute-r-script] модуля.  

Если у вас установлена на настольном компьютере язык программирования hello R, я рекомендую сделать это сейчас. Бесплатные файлы для загрузки языка R с открытым кодом можно найти по адресу hello сети полный архив R (CRAN) в [http://www.r-project.org/](http://www.r-project.org/). Доступны файлы для скачивания для Windows, Mac OS и Linux или UNIX. Выберите близлежащих зеркала и следуйте приведенным инструкциям загрузки hello. CRAN также содержит множество полезных пакетов для аналитики и обработки данных.

Если новый tooRStudio, необходимо загрузить и установить версию для настольного компьютера hello. Можно найти RStudio загружаемые файлы для Windows, Mac OS и Linux и UNIX на http://www.rstudio.com/products/RStudio/ приветствия. Следуйте приведенным инструкциям hello, предоставляемые tooinstall RStudio на настольном компьютере.  

Введение в учебник tooRStudio находится в https://support.rstudio.com/hc/sections/200107586-Using-RStudio.

Дополнительные сведения по использованию RStudio можно найти в [Приложении А][appendixa].  

## <a id="scriptmodule"></a>Получение данных из модуля hello выполнение скрипта R
В этом разделе мы рассмотрим, как получить данные в действие и из hello [выполнение скрипта R] [ execute-r-script] модуля. Мы рассмотрим, как toohandle различные типы данных считывать в действие и из hello [выполнение скрипта R] [ execute-r-script] модуля.

Hello полный код для этого раздела находится в hello ZIP-файл, загруженный ранее.

### <a name="load-and-check-data-in-machine-learning-studio"></a>Загрузка и проверка данных в Студии машинного обучения
#### <a id="loading"></a>Загрузить набор данных hello
Начнем с загрузкой hello **csdairydata.csv** файла в студии машинного обучения Azure.

* Запустите среду Студии машинного обучения Azure.
* Щелкните **+ создать** в hello понизить левой части экрана и выберите **набора данных**.
* Выберите **из локального файла**, а затем **Обзор** tooselect hello файла.
* Убедитесь, что вы выбрали **универсального CSV-файл с заголовком (.csv)** hello тип для набора данных hello.
* Щелкните флажок hello.
* После передачи hello набора данных вы увидите новый набор данных hello, щелкнув hello **наборы данных** вкладки.  

#### <a name="create-an-experiment"></a>Создание эксперимента
Теперь, когда у нас есть некоторые данные в студии машинного обучения, нам нужна toocreate анализ hello toodo эксперимента.  

* Щелкните **+ создать** в списке hello левому нижнему углу и выберите **эксперимента**, затем **пустой эксперимента**.
* Назовите эксперимента, выбрав и изменение, hello **эксперимента создан на...**  заголовок вверху hello страницы приветствия. Например, изменение слишком**ЦС Молоко Analysis**.
* Слева hello hello эксперимента страницы разверните **сохраненные наборы данных**, а затем **Мои наборы данных**. Вы увидите hello **cadairydata.csv** загруженный ранее.
* Перетаскивание hello **csdairydata.csv dataset** на hello эксперимента.
* В hello **поиска поэкспериментировать элементы** поле в верхней части hello hello левой панели, то тип [выполнение скрипта R][execute-r-script]. Вы увидите, отображаются в списке поиска hello модуля hello.
* Перетаскивание hello [выполнение скрипта R] [ execute-r-script] модуля на вашей палитра.  
* Подсоедините hello выход hello **csdairydata.csv dataset** toohello крайний левый вход (**Dataset1**) из hello [выполнение скрипта R][execute-r-script].
* **Не забывайте tooclick на «Сохранить»**  

На этом этапе ваш эксперимент должен выглядеть, как показано на рисунке 3.

![Hello анализа Молоко ЦС поэкспериментировать с набора данных и выполнение скрипта R модуля][3]

*Рис. 3. Hello анализа Молоко ЦС поэкспериментировать с набора данных и выполнение скрипта R модуля.*

#### <a name="check-on-hello-data"></a>Проверка данных hello
Давайте посмотрим на hello данные, которые мы загрузили в нашем эксперимент. В эксперименте hello, щелкните на результате hello hello **cadairydata.csv dataset** и выберите **визуализировать**. Вы увидите нечто вроде этого (рис. 4):  

![Сводка по набору данных cadairydata.csv hello][4]

*Рис. 4. Сводка hello cadairydata.csv dataset.*

Здесь представлено много полезной информации. Мы видим hello первые несколько строк того же набора данных. Если выбирается столбец hello раздел статистики показывает Дополнительные сведения о столбце hello. Например строка hello тип компонента показывает, какие типы данных столбца toohello назначенный студии машинного обучения Azure. Наличие быстрого выглядят следующим образом — хороший проверочной, прежде чем начать toodo серьезные несохраненные.

### <a name="first-r-script"></a>Первый сценарий R
Давайте создадим простой первый tooexperiment R-скрипт с в студии машинного обучения Azure. Я создания и тестирования hello, выполнив скрипт в RStudio.  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

Осталось tootransfer этот сценарий tooAzure студии машинного обучения. Можно было бы его просто вырезать и вставить. Но в данном случае я перенесу свой скрипт R при помощи ZIP-файла.

### <a name="data-input-toohello-execute-r-script-module"></a>Модуль выполнение скрипта R toohello входных данных
Давайте посмотрим на toohello входов hello [выполнение скрипта R] [ execute-r-script] модуля. В этом примере мы будет считываются данные молока Калифорния hello hello [выполнение скрипта R] [ execute-r-script] модуля.  

Существует три возможных входных значений для hello [выполнение скрипта R] [ execute-r-script] модуля. В зависимости от приложения можно использовать любой из них или все. Это вполне разумным toouse R-сценарий, который не принимает входные данные во всех.  

Давайте рассмотрим каждый из входных данных, поступающих из левой tooright. Вы увидите hello имена каждого входа hello, наведя курсор на hello входных данных и чтение hello всплывающей подсказки.  

#### <a name="script-bundle"></a>Пакет скриптов
Hello пакет сценария ввода позволяет toopass hello содержимое ZIP-файл в [выполнение скрипта R] [ execute-r-script] модуля. Используются следующие команды tooread hello содержимое hello ZIP-файл в коде R hello.

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> Машинное обучение Azure обрабатывает файлы в архив hello, как если бы они находятся в hello src / directory, поэтому требуется tooprefix имена файл с таким именем каталога. Например, если hello zip содержит файлы hello `yourfile.R` и `yourData.rdata` в корне hello zip hello, можно по адресу их как `src/yourfile.R` и `src/yourData.rdata` при использовании `source` и `load`.
> 
> 

Мы уже рассмотрели Загрузка наборов данных в [загрузке набора данных hello](#loading). После создания и проверки hello R сценарий, показанный в предыдущем разделе hello hello следующие:

1. Сохранить скрипт hello R в. R-файл. Я назвал свой файл скрипта "simpleplot.R". Вот содержимое hello.
   
        ## Only one of hello following two lines should be used
        ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
        ## If in RStudio, use hello second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## hello following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. Создайте ZIP-файл и скопируйте в него свой скрипт. В Windows, правой кнопкой мыши файл hello и выберите **отправки**, а затем **сжатая папка**. Это создаст новый ZIP-файл, содержащий hello «simpleplot. Файл R».
3. Добавьте в файл toohello **наборы данных** в студии машинного обучения, указав тип hello как **zip**. Теперь вы увидите hello ZIP-файл в наборах данных.
4. Перетаскивание hello ZIP-файл из **наборы данных** на hello **холст ML Studio**.
5. Подсоедините hello выход hello **ZIP-архив данных** toohello значок **пакет сценария** вводу hello [выполнение скрипта R] [ execute-r-script] модуля.
6. Тип hello `source()` функция с именем zip файл в окне кода hello для hello [выполнение скрипта R] [ execute-r-script] модуля. В данном случае введено `source("src/simpleplot.R")`.  
7. Обязательно щелкните **Сохранить**.

После выполнения этих действий, hello [выполнение скрипта R] [ execute-r-script] модуль будет выполняться скрипт hello R в ZIP-файле hello при запуске эксперимента hello. На этом этапе ваш эксперимент должен выглядеть, как изображено на рисунке 5.

![Эксперимент с использованием сценария R, сжатого в ZIP-файл][6]

*Рис. 5. Эксперимент с использованием сценария R, сжатого в ZIP-файл*

#### <a name="dataset1"></a>Набор данных 1
Прямоугольный таблицу tooyour R код данных можно передавать с помощью ввода hello Dataset1. В нашей hello простой сценарий `maml.mapInputPort(1)` функция считывает hello данные из порта 1. Эти данные затем присваивается имя переменной tooa кадр данных в коде. В нашем сценарии простой hello первой строки кода выполняет hello назначения.

    cadairydata <- maml.mapInputPort(1)

Выполнение эксперимента, щелкнув hello **запуска** кнопки. После завершения выполнения hello, щелкните hello [выполнение скрипта R] [ execute-r-script] модуля, а затем нажмите кнопку **просмотреть выходной журнал** на панели свойств hello. Новая страница откроется в браузере, показывающая hello содержимое файла файл output.log hello. При прокрутке вы увидите примерно hello следующим образом.

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

Дальше вниз hello страница является более подробные сведения о hello столбцы, которые будет выглядеть примерно hello следующим образом.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput]
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput]
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month            : chr  "Jan" "Feb" "Mar" "Apr" ...
    [ModuleOutput]
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput]
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput]
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput]
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...

Эти результаты, главным образом, как и ожидалось, с 228 наблюдения и 9 столбцами в кадр данных hello. Мы видим hello имена столбцов, тип данных hello R и образец каждого столбца.

> [!NOTE]
> Этот же вывода на печать удобно доступен из hello выходные данные устройства R hello [выполнение скрипта R] [ execute-r-script] модуля. Мы обсудим hello выходы hello [выполнение скрипта R] [ execute-r-script] модуля в следующем разделе hello.  
> 
> 

#### <a name="dataset2"></a>Набор данных 2
Hello поведение hello Dataset2 входные данные не идентичные toothat Dataset1. С помощью этого порта можно передать еще одну прямоугольную таблицу данных в код на R. Здравствуйте, функция `maml.mapInputPort(2)`, с аргументом hello 2, является используется toopass эти данные.  

### <a name="execute-r-script-outputs"></a>Порты вывода модуля "Выполнение скрипта R"
#### <a name="output-a-dataframe"></a>Вывод таблицы данных
Можно вывести содержимое hello кадр данных R как таблицу прямоугольный через порт hello Dataset1 результат с помощью hello `maml.mapOutputPort()` функции. В нашей простой сценарий R это выполняется по следующей строкой hello.

    maml.mapOutputPort('cadairydata')

После выполнения эксперимента hello, щелкните порт вывода результата Dataset1 hello и выберите команду **визуализировать**. Вы увидите нечто вроде этого (рис. 6):

![визуализация Hello hello выходной hello молока данных Калифорния][7]

*Рис. 6. визуализация Hello hello выходной hello молока данных Калифорнии.*

Это выходные данные выглядят идентичными toohello данные, точно так, как ожидалось.  

### <a name="r-device-output"></a>Порт вывода "Устройство R"
Здравствуйте, выходные данные устройства hello [выполнение скрипта R] [ execute-r-script] модуль выходными данными сообщения и графики. Оба стандартный выход и Стандартная ошибка сообщения из R отправляются toohello устройство R выходной порт.  

hello tooview R вывода на устройство, щелкните на порту hello, а затем на **визуализировать**. Мы видим hello стандартный вывод и стандартную ошибку из сценария hello R на рис. 7.

![Стандартный выход и Стандартная ошибка из hello порт устройства R][8]

*Рис. 7. Стандартный выход и Стандартная ошибка из hello порт устройство R.*

Прокрутка вниз мы вывод hello графики из наших сценария R на рис. 8.  

![Вывод графики hello порт устройства R][9]

*Рис. 8. Выходные данные hello порт устройства R графики.*  

## <a id="filtering"></a>Фильтрация и преобразование данных
В этом разделе мы выполним некоторые операции преобразования hello Калифорния молока данных и фильтрации данных. Концу hello в этом разделе будет иметь данные в формате, удобном для построения аналитических моделей.  

В частности, в этом разделе мы выполним несколько распространенных задач по очистке и преобразованию данных: преобразование типа данных, фильтрацию кадров данных, добавление новых вычисляемых столбцов и преобразование значений. Этот цвет фона поможет вам работать с hello множество вариантов, в реальных проблем.

Hello полный код R для этого раздела, доступен в hello ZIP-файл, загруженный ранее.

### <a name="type-transformations"></a>Преобразование типов данных
Теперь, когда мы могут считывать данные молока Калифорния hello выполнения кода hello R в hello [выполнение скрипта R] [ execute-r-script] модуля, нам нужно tooensure наличие hello данные в столбцах hello hello предназначен тип и формат.  

R — это динамически типизированный язык, это означает, что типы данных преобразуются из одного tooanother при необходимости. типы атомарных данных Hello в R: числовые, логические и символ. Тип Hello фактор — категориальные данные в хранилище используется toocompactly. Гораздо Дополнительные сведения о типах данных можно найти в ссылках hello в [приложение B - дальнейшего изучения](#appendixb).

При считывании табличных данных в R из внешнего источника, всегда является хорошей идеей hello toocheck, возникающие в типы столбцов hello. Зачастую может оказаться, что данные в столбце не символьного типа, как предполагалось, а относятся к типу фактор (или наоборот). В других случаях столбец, который должен содержать числовые данные, содержит символьные данные, например «1,23» вместо 1,23 — числа с плавающей запятой.  

К счастью это просто tooconvert один тип tooanother, при условии, что сопоставление возможно. Например «Невада» нельзя преобразовать в числовое значение, но ее можно будет преобразовать tooa коэффициент (категориальной переменной). Еще один пример. Числовое значение 1 можно преобразовать в символ '1' или в фактор.  

простой синтаксис Hello для любого из этих преобразований: `as.datatype()`. Эти функции преобразования типов включают следующие hello.

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

Просмотрев hello типы данных столбцов hello, мы входные данные в предыдущем разделе hello: все столбцы имеют тип числовой, за исключением столбца hello с меткой «Месяц», тип символа. Давайте преобразовать этот коэффициент tooa и hello результаты теста.  

Я удалил строку hello, матрица scatterplot hello созданы и добавлены строки, преобразование коэффициент tooa столбец «Month» hello. В моей эксперименте я будет просто вырежьте и вставьте hello R код в окно кода hello hello [выполнение скрипта R] [ execute-r-script] модуля. Можно также обновить hello ZIP-файл и отправьте его tooAzure студии машинного обучения, но это занимает несколько шагов.  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check hello result
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

Давайте выполните этот код и посмотрите на hello выходном файле журнала hello R-сценария. на рис. 9 показан Hello необходимые данные из журнала hello.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 14 levels "Apr","April",..: 6 5 9 1 11 8 7 3 14 13 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Рис. 9. Сводка hello кадр данных с переменной коэффициент.*

должно появиться сообщение Hello тип для месяца "**коэффициент с 14 уровней**". Это проблема, поскольку существуют только в течение 12 месяцев года hello. Можно также проверить, hello типа toosee в **визуализировать** hello результирующий набор данных является порт "**категориальная**".

Hello проблема в том, «Month», столбец не был закодирован систематически hello. В некоторых случаях месяц назван April, а в других — сокращенно Apr. Эту проблему можно решить путем обрезки символов too3 строку hello. Строка кода Hello теперь выглядит hello следующим образом:

    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

Повторно запустите эксперимент hello и просмотреть журнал выходных данных hello. Hello тесты на ожидаемые результаты показаны на рис. 10.  

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Рис. 10. Сводные сведения о кадре данных hello с правильное число уровней коэффициент.*

Наш переменной коэффициент теперь имеет hello требуемого 12 уровней.

### <a name="basic-data-frame-filtering"></a>Базовая фильтрация таблицы данных
Таблицы данных R поддерживают массу возможностей фильтрации. Наборы данных можно разбивать на подмножества, используя логическую фильтрацию по строкам или столбцам. Во многих случаях вам потребуются сложные критерии фильтрации. ссылки на Hello в [приложение B - дальнейшего изучения](#appendixb) содержат сложные примеры фильтрации блоки данных.  

Выполним операцию фильтрации в нашем наборе данных. Если взглянуть на столбцы hello в кадр данных cadairydata hello, вы увидите два ненужных столбцов. Hello первый столбец содержит только число строк, не очень удобен. второй столбец Hello, Year.Month, содержит избыточные сведения. Мы легко можно исключить эти столбцы, используя следующий код R hello.

> [!NOTE]
> Из теперь на этот раздел будет просто показано hello дополнительный код, добавленный в hello [выполнение скрипта R] [ execute-r-script] модуля. Каждой новой строки будут добавлены **перед** hello `str()` функции. Я использую это функция tooverify результаты в студии машинного обучения Azure.
> 
> 

Добавить следующие строки кода toomy R в hello hello [выполнение скрипта R] [ execute-r-script] модуля.

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

Запустите этот код в эксперименте и проверяет результат hello из hello выходные данные журнала. Результат приведен на рис. 11.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  7 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Рис. 11. Удалить сводку hello кадр данных с двумя столбцами.*

Отличная новость! Мы получаем hello ожидалось результатов.

### <a name="add-a-new-column"></a>Добавление нового столбца
модели временных рядов toocreate будет удобный toohave столбце, содержащем hello месяцев с момента запуска hello hello временных рядов. Мы создадим столбец Month.Count (Количество месяцев).

toohelp организации кода hello, мы создадим нашей первой простая функция `num.month()`. Затем будет применена toocreate этой функции в новом столбце в кадр данных hello. новый код Hello выглядит следующим образом.

    ## Create a new column with hello month count
    ## Function toofind hello number of months from hello first
    ## month of hello time series
    num.month <- function(Year, Month) {
      ## Find hello starting year
      min.year  <- min(Year)

      ## Compute hello number of months from hello start of hello time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute hello new column for hello dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

Теперь запустите эксперимент hello обновлены и использовать результаты hello выходные данные журнала tooview hello. Этот результат приведен на рисунке 12.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Рис. 12. Сводка hello кадр данных с hello дополнительного столбца.*

Похоже, все работает. У нас есть hello новый столбец с ожидаемыми значениями hello в нашем кадр данных.

### <a name="value-transformations"></a>Преобразование значений
В этом разделе мы выполним некоторых простых преобразований по значениям hello в некоторых столбцах hello из наших кадр данных. язык Hello R поддерживает почти произвольное значение преобразования. ссылки на Hello в [приложение B — Дополнительные материалы](#appendixb) содержат сложные примеры.

Если взглянуть на значения hello в hello сводки по нашей кадр данных вы увидите нечто нечетное здесь. Неужели мороженого в Калифорнии производят больше, чем молока? Нет, конечно не так, как это не имеет никакого смысла, как этот факт жаль, что может быть toosome нас lovers мороженого. единицы Hello отличаются. Цена Hello измеряется в нам фунты milk в единицах 1 млн фунты США, мороженого измеряется в 1000 нам галлоны и cottage Цилиндрическая измеряется в 1000 фунты США. При условии, что мороженого взвешивается около 6,5 фунты на галлон, мы можем легко hello эти значения, поэтому все они находятся в равных единиц 1000 фунты tooconvert умножения.

В нашей модели прогнозирования мы используем мультипликативную модель для корректировки этих данных. Преобразование журнала позволяет нам toouse линейной модели, что упрощает этот процесс. Можно применить преобразование журнала hello в hello же функции, где применяется множитель hello.

В hello после кода, определить новую функцию `log.transform()`и примените его toohello строки, содержащие hello числовых значений. Hello R `Map()` функции — hello используется tooapply `log.transform()` toohello функция выбранные столбцы из hello кадр данных. `Map()`Аналогично слишком`apply()` , но позволяет более одного списка аргументов функции toohello. Обратите внимание, что список множители предоставляет hello второй аргумент toohello `log.transform()` функции. Hello `na.omit()` немного tooensure очистки мы нет отсутствующих или неопределенные значения в hello кадр данных используется функция.

    log.transform <- function(invec, multiplier = 1) {
      ## Function for hello transformation, which is hello log
      ## of hello input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments toofunction log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier toofuncition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check hello input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap hello multiplication in tryCatch
      ## If there is an exception, print hello warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply hello transformation function toohello 4 columns
    ## of hello dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

Нет происходит довольно бит в hello `log.transform()` функции. Большая часть кода поиск потенциальных проблем с аргументами hello, или работа с исключениями, которые по-прежнему могут возникнуть во время вычисления hello. Фактически только несколько строк кода hello вычислений.

Задача Hello hello защитного программирования — сбой hello tooprevent одну функцию, которая предотвращает обработку продолжение. Внезапный сбой продолжительного анализа — вещь довольно неприятная. tooavoid, который ограничит этой ситуации возвращаемых значений необходимо выбрать, по умолчанию повредить toodownstream обработки. Сообщение также является произведенных tooalert пользователей, которые пошло так.

Если вы не используется toodefensive программирование на языке R, этот код может показаться немного невозможной. Я поможет hello основных шагов:

1. Определяется вектор четырех сообщений. Эти сообщения являются используется toocommunicate сведения о некоторых возможных ошибок hello и исключениях, возникающих с этим кодом.
2. Во всех этих случаях возвращается значение NA (нет данных). Есть и другие возможности, у которых может быть меньше побочных эффектов. Может возвратить вектор из нулей или исходного вектора входного hello, например.
3. Проверка выполняется в функции toohello аргументы hello. В каждом случае, если обнаруживается ошибка, возвращается значение по умолчанию и создается сообщение hello `warning()` функции. Я использую `warning()` вместо `stop()` как последний hello нарушит выполнения, точно удается tooavoid. Обратите внимание, что при написании этого кода я использовал процедуры, поскольку использование функций сделало бы его сложнее и непонятнее.
4. Hello журнала вычислений упаковываются в `tryCatch()` , чтобы исключения не приведет к остановке внезапные tooprocessing. Без функции `tryCatch()` большинство ошибок, вызванных функциями R, вызывает сигнал остановки, что приводит именно к прерыванию.

Выполните этот код R в эксперименте и рассмотрим hello напечатанных выходные данные в файле файл output.log hello. Значения преобразования hello hello журнала четырех столбцов в hello, теперь будут видеть, как показано на рис. 13.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Рис. 13. Сводка hello преобразования значения в кадр данных hello.*

Мы увидим, что значения hello были преобразованы. Теперь производство молока значительно превышает по объемам производство остальных молочных продуктов (не забывайте, что мы используем логарифмическую шкалу).

Теперь все наши данные в порядке и мы можем приступать к моделированию. Просмотрев hello визуализации сводки для hello выходных данных результирующего набора данных из наших [выполнение скрипта R] [ execute-r-script] модуля, вы увидите столбец «Month» hello «Категориальная» с уникальными значениями, 12, снова так же, как мы старались .

## <a id="timeseries"></a>Объекты временного ряда и корреляционный анализ
В этом разделе мы исследовать несколько основных объектов R ряда времени и анализировать hello корреляции между некоторыми hello переменных. Наша цель — toooutput кадр данных содержащего hello парные сведений о корреляции в несколько задержки.

Hello полный код R для этого раздела находится в hello ZIP-файл, загруженный ранее.

### <a name="time-series-objects-in-r"></a>Объекты временных рядов в языке R
Как уже упоминалось, временные ряды представляют собой ряды значений данных, индексированные по времени. R время ряд объектов, используемых toocreate индекса и управления им hello времени. Существует несколько преимуществ toousing время ряда объектов. Объекты ряда времени освободить вас от hello многие элементы управления hello временных индекс значения, инкапсулированным в hello объекта. Кроме того, время ряда объекты позволяют toouse hello много методов ряда времени для отображения на диаграмме, печать, моделирования и т. д.

Hello POSIXct времени серии класс обычно используется и относительно проста. Этот класс ряда времени измеряет время от начала эпохи hello, 1 января 1970 года hello. В этом примере мы будем использовать объекты временных рядов POSIXct. Другие распространенные классы объектов временных рядов включают zoo и xts (расширяемые временные ряды).
<!-- Additional information on R time series objects is provided in hello references in Section 5.7. [commenting because this section doesn't exist, even in hello original] -->

### <a name="time-series-object-example"></a>Пример объекта временных рядов
Приступим к разбору примера. Перетащим **новый** модуль [Выполнить сценарий R][execute-r-script] в свой эксперимент. Подключения hello Dataset1 результат выходной порт hello существующих [выполнение скрипта R] [ execute-r-script] toohello модуль Dataset1 входному порту hello новый [выполнение скрипта R] [ execute-r-script] модуля.

Как это делалось для первого примеры hello, как мы ход примере hello в некоторые моменты, которые будет показано только hello добавочное дополнительных строк кода R на каждом шаге.  

#### <a name="reading-hello-dataframe"></a>Чтение кадр данных hello
В качестве первого шага давайте чтения в кадр данных и убедитесь, что мы получаем hello ожидалось результатов. Hello следующий код должен выполнять задания hello.

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check hello results

Теперь запустите эксперимент hello. Журнал Hello hello новую фигуру выполнение скрипта R должна выглядеть как на рис. 14.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...

*Рис. 14. Сводные сведения о кадре данных hello в модуле выполнение скрипта R hello.*

Эти данные являются типов ожидается hello и формат. Обратите внимание, что столбец «Month» hello имеет коэффициент тип имеет hello требуется число уровней.

#### <a name="creating-a-time-series-object"></a>Создание объекта временных рядов
Мы должны tooadd время кадр данных tooour рядов объекта. Замените текущий код hello hello следующее, что добавляется новый столбец класса POSIXct.

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check hello results

Теперь в журнале hello. Результат приведен на рисунке 15.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

*Рис. 15. Сводные сведения о кадре данных hello с объектом ряда времени.*

Мы увидим из сводки hello hello нового столбца на самом деле относится к классу POSIXct.

### <a name="exploring-and-transforming-hello-data"></a>Исследование и преобразование данных hello
Рассмотрим некоторые из переменных hello в этом наборе данных. Матрица scatterplot — хороший способ tooproduce быстрого просмотра. Я замена hello `str()` функции в предыдущем коде R hello со следующей строкой hello.

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

Выполним этот код и посмотрим на результат. Hello построения, произведенные hello порт устройства R должна выглядеть как на рисунке 16.

![Точечная диаграмма выбранных переменных][17]

*Рис. 16. Матрица точечной диаграммы выбранных переменных*

Есть некоторые odd-looking структуры в связях hello между этими переменными. Возможно это возникает из тренды в данных hello и hello факт, что мы не стандартизованы hello переменных.

### <a name="correlation-analysis"></a>Корреляционный анализ
tooperform analysis корреляции, необходимые tooboth отменяется тенденций и стандартизировать hello переменных. Можно просто использовать hello R `scale()` функции, которая центров и масштабирует переменных. Возможно, это было бы быстрее. Тем не менее, я хочу tooshow вы примером защитного программирования в среде R.

Hello `ts.detrend()` показанную ниже функцию выполняет обе операции. Hello две следующие строки кода отменяется трендов данных hello и затем стандартизации значений hello.

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function toode-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time toohave hello same length',
                    'ERROR: ts.detrend requires argument ts toobe of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros tooreturn as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # hello input arguments are not of hello same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If hello ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If hello ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that hello Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend hello time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply hello detrend.ts function toohello variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot hello results toolook at hello relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

Нет происходит довольно бит в hello `ts.detrend()` функции. Большая часть кода поиск потенциальных проблем с аргументами hello, или работа с исключениями, которые по-прежнему могут возникнуть во время вычисления hello. Фактически только несколько строк кода hello вычислений.

Мы уже обсуждали пример защищенного программирования в разделе [Преобразование значений](#valuetransformations). Оба блока вычислений выполняются внутри функции `tryCatch()`. Для некоторых ошибок, это делает смысле tooreturn hello исходного входного вектора, и в других случаях возвратить вектора нули.  

Обратите внимание, что hello Линейная регрессия используется для отмены сведения о тенденциях Регрессия ряда времени. Hello прогнозирующих переменных представляет собой объект ряда времени.  

Один раз `ts.detrend()` определяется мы применить переменные toohello интересуют наши кадр данных. Мы должны привести hello полученный список созданных `lapply()` toodata кадр данных с помощью `as.data.frame()`. Из-за защитного аспектов `ts.detrend()`, tooprocess сбой одной из переменных hello не помешает исправить обработку hello другим пользователям.  

Последняя строка кода Hello создает парные scatterplot. После выполнения кода hello R hello результаты hello scatterplot показаны на рис.

![Попарная точечная диаграмма после вычитания тренда и стандартизации временных рядов][18]

*Рис. 17. Попарная точечная диаграмма после вычитания тренда и стандартизации временных рядов*

Вы можете сравнить эти toothose результаты, показанные на рис. Удалены тренда hello и hello переменные стандартизованы, мы увидим гораздо меньше структуры в hello связи между этими переменными.

корреляции hello toocompute кода Hello как объекты R ccf выглядит следующим образом.

    ## A function toocompute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of hello pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute hello list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

Выполнение этого кода создает журнал hello показано на рис.

    [ModuleOutput] Loading objects:
    [ModuleOutput]   port1
    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] [[1]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.148 0.358 0.317 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[2]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.395 -0.186 -0.238 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[3]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.059 -0.089 -0.127 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[4]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.140 0.294 0.293 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[5]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.002 -0.074 -0.124 

*Рис. 18. Список ccf объектов из анализа парный корреляции hello.*

Каждой задержке соответствует значение корреляции. Ни один из этих значений корреляции не достаточно большой toobe значительные. Таким образом, можно заключить, что каждую переменную можно моделировать независимо от других.

### <a name="output-a-dataframe"></a>Вывод таблицы данных
Как список объектов R ccf, рассчитанное hello парные корреляции. Это представляет немного проблемы как hello порт вывода результирующего набора данных, которая требует кадр данных. Кроме того hello объекта ccf является списком, мы хотим только значения hello в первый элемент hello этого списка hello корреляции в hello различные проблемы.

Hello следующую hello запаздывания код извлекает значения из списка hello ccf объектов, которые сами являются списками.

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with hello row names column and the
    ## correlation data frame and assign hello column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## hello following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

Первая строка кода Hello немного сложнее и объяснения помогут понять его. Работа с hello вдоль и поперек у нас есть hello следующее:

1. Hello "**[[**«оператор с аргументом hello»**1**" выбирает hello вектор корреляции в задержка hello из первого элемента списка объектов ccf hello hello.
2. Hello `do.call()` применяется функций hello `rbind()` функции hello элементы списка hello возвращают, `lapply()`.
3. Hello `data.frame()` функция относит hello результата, формируемого `do.call()` tooa кадр данных.

Обратите внимание, что строка hello имена в столбце hello кадр данных. Это сохраняет имена строку hello, когда они выводятся из hello [выполнение скрипта R][execute-r-script].

Выполнение кода hello вывод hello показано на рисунке 19 когда я **визуализировать** hello выходные данные в hello порт результирующего набора данных. Hello строк, называются в первом столбце hello, как планировалось.

![Вывод результатов анализа корреляции hello][20]

*Рис. 19. Результаты вывода analysis корреляции hello.*

## <a id="seasonalforecasting"></a>Пример временных рядов: сезонное прогнозирование
Наши данные теперь находится в форме, подходящей для анализа и обнаружено, что нет не значительные взаимосвязи между переменными hello. Пойдем дальше и создадим прогностическую модель временных рядов. С помощью этой модели будет спрогнозировать Калифорния milk производства для hello 12 месяцев 2013.

У нашей прогностической модели будет два компонента: тренд и сезонный компонент. Полный прогноз Hello — hello совокупность этих двух компонентов. Модели такого типа называются мультипликативными. альтернативой Hello представляет собой аддитивный модель. Мы уже применены переменных toohello преобразования журнала интерес, что делает этот анализ работы со.

Hello полный код R для этого раздела находится в hello ZIP-файл, загруженный ранее.

### <a name="creating-hello-dataframe-for-analysis"></a>Создание hello кадр данных для анализа
Начните с добавления **новый** [выполнение скрипта R] [ execute-r-script] модуль tooyour эксперимента. Подключение hello **результирующего набора данных** вывода hello существующих [выполнение скрипта R] [ execute-r-script] toohello модуль **Dataset1** ввода нового модуля hello. Hello результат должен выглядеть примерно как на рис.

![Hello поэкспериментировать с hello добавлен новый модуль выполнение скрипта R][21]

*Рис. 20. Hello поэкспериментировать с hello добавлен новый модуль выполнение R-сценария.*

Как и для анализа hello корреляции, который мы только что выполнили, мы нужен tooadd столбца с объектом ряда времени POSIXct. просто это необходимо сделать после кода Hello.

    # If running in Machine Learning Studio, uncomment hello first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

Запустите этот код и просмотрите журнал hello. Рисунок 21 вид Hello результата.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

*Рис. 21. Сводка hello кадр данных.*

С данным результатом Приносим toostart готовности в ходе анализа.

### <a name="create-a-training-dataset"></a>Создание набора данных для обучения
Созданный кадр данных hello мы должны toocreate обучающий набор данных. Эти данные будут включены все hello наблюдения за исключением hello последние 12 hello года 2013, являющееся нашей проверочном наборе данных. Hello ниже программный код кадр данных подмножеств hello и создает графики hello молока производства и цена переменных. Затем создать точечное hello четыре переменных производства и ценой. Анонимная функция имеет некоторые делается дополнение для построения используется toodefine и затем выполните итерацию через список hello hello двух других аргументов с `Map()`. Если вам кажется, что здесь пригодилась бы структура for ... loop, вы совершенно правы. Но поскольку язык R оперирует функциями, я продемонстрирую решение с использованием функций.

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

В результате выполнения кода hello возникает ряд временных рядов диаграммы из выходных данных устройство R hello, показаны на рисунке 22 hello. Обратите внимание, что этой оси времени hello измеряется в даты, приятным преимуществом hello время метод построения ряда.

![Первая диаграмма временных рядов данных по ценам и производству молочных продуктов в Калифорнии](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![Вторая диаграмма временных рядов данных по ценам и производству молочных продуктов в Калифорнии](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![Третья диаграмма временных рядов данных по ценам и производству молочных продуктов в Калифорнии](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![Четвертая диаграмма временных рядов данных по ценам и производству молочных продуктов в Калифорнии](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

*Рис. 22. Диаграммы временных рядов данных по ценам и производству молочных продуктов в Калифорнии*

### <a name="a-trend-model"></a>Модель тренда
После создания объект ряда времени и только что рассмотрели данных hello, начнем tooconstruct модель тренда для hello Калифорния milk производственных данных. Для этого можно использовать регрессию временного ряда. Тем не менее это видно из диаграммы hello, мы должны более Наклон и пересечение tooaccurately моделировать hello наблюдается тенденция в hello обучающих данных.

Имея hello малого масштаба данных hello, я будет построена модель hello для тренда в RStudio и затем вырезать и вставить результирующую модель hello в машинном обучении Azure. RStudio предоставляет интерактивную среду для такого рода интерактивного анализа.

В качестве первой попытки попытается полиномиальная Регрессия с питание too3. При создании таких моделей существует высокая вероятность образования лжевзаимосвязей. Таким образом это наиболее условия tooavoid высокого порядка. Hello `I()` функция подавляет интерпретацию содержимое hello (интерпретирует содержимое hello «как есть») и позволяет toowrite буквально интерпретируемых функции в формуле регрессии.

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

Этот код создает следующие hello.

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3),
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12667 -0.02730  0.00236  0.02943  0.10586
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.33e+00   1.45e-01   43.60   <2e-16 ***
    ## Time              1.63e-09   1.72e-10    9.47   <2e-16 ***
    ## I(Month.Count^2) -1.71e-06   4.89e-06   -0.35    0.726
    ## I(Month.Count^3) -3.24e-08   1.49e-08   -2.17    0.031 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0418 on 212 degrees of freedom
    ## Multiple R-squared:  0.941,    Adjusted R-squared:  0.94
    ## F-statistic: 1.12e+03 on 3 and 212 DF,  p-value: <2e-16

На основе значений P (Pr (> | t |)) в этих выходных данных видно, что hello квадрат термин может быть незначительной. Я использую hello `update()` функции toomodify этой модели, удаление hello квадрат термин.

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

Этот код создает следующие hello.

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12597 -0.02659  0.00185  0.02963  0.10696
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.38e+00   4.07e-02   156.6   <2e-16 ***
    ## Time              1.57e-09   4.32e-11    36.3   <2e-16 ***
    ## I(Month.Count^3) -3.76e-08   2.50e-09   -15.1   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0417 on 213 degrees of freedom
    ## Multiple R-squared:  0.941,  Adjusted R-squared:  0.94
    ## F-statistic: 1.69e+03 on 2 and 213 DF,  p-value: <2e-16

Теперь значительно лучше. Значимыми являются все слова hello. Тем не менее значение 2e 16 hello это значение по умолчанию и не следует принимать слишком серьезно.  

Для проверки работоспособности сделаем график ряда времени hello Калифорния подсчет рабочих данных показано кривой тренда hello. Я добавил hello, следующий код в hello машинного обучения Azure [выполнение скрипта R] [ execute-r-script] toocreate модели (не RStudio) hello модели и сделать построение. Hello результат показан на рисунке 23.

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![Данные молочного производства Калифорнии с моделью тренда](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

*Рис. 23. Данные молочного производства Калифорнии с моделью тренда*

Похоже, hello тренда модель соответствует данным hello довольно хорошо. Кроме того существует не toobe свидетельство чрезмерное Подгонка, такие как нечетными wiggles кривой hello модели.  

### <a name="seasonal-model"></a>Сезонная модель
С моделью тренда в наличии нам нужна toopush на и включать сезонных эффектов hello. Мы будем использовать hello месяц года hello как фиктивный действующему hello Линейная модель toocapture hello по месяцам. Обратите внимание, что при вводе коэффициент переменных в модель отсекаемый отрезок hello не вычисляемые. Если этого не сделать, формула hello чрезмерно указанным, а также приведет к удалению R один hello требуемого факторов, но сохранить hello свободный член.

Поскольку у нас есть удовлетворительные тренда модели можно использовать hello `update()` функция tooadd hello новые термины toohello существующей модели. Hello -1 в формуле hello обновления удаляет hello свободный член. До момента hello в RStudio:

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

Этот код создает следующие hello.

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3) + Month - 1,
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.06879 -0.01693  0.00346  0.01543  0.08726
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## Time              1.57e-09   2.72e-11    57.7   <2e-16 ***
    ## I(Month.Count^3) -3.74e-08   1.57e-09   -23.8   <2e-16 ***
    ## MonthApr          6.40e+00   2.63e-02   243.3   <2e-16 ***
    ## MonthAug          6.38e+00   2.63e-02   242.2   <2e-16 ***
    ## MonthDec          6.38e+00   2.64e-02   241.9   <2e-16 ***
    ## MonthFeb          6.31e+00   2.63e-02   240.1   <2e-16 ***
    ## MonthJan          6.39e+00   2.63e-02   243.1   <2e-16 ***
    ## MonthJul          6.39e+00   2.63e-02   242.6   <2e-16 ***
    ## MonthJun          6.38e+00   2.63e-02   242.4   <2e-16 ***
    ## MonthMar          6.42e+00   2.63e-02   244.2   <2e-16 ***
    ## MonthMay          6.43e+00   2.63e-02   244.3   <2e-16 ***
    ## MonthNov          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## MonthOct          6.37e+00   2.63e-02   241.8   <2e-16 ***
    ## MonthSep          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0263 on 202 degrees of freedom
    ## Multiple R-squared:     1,    Adjusted R-squared:     1
    ## F-statistic: 1.42e+06 on 14 and 202 DF,  p-value: <2e-16

Мы видим, эту модель hello больше не имеет свободный член и имеет 12 факторов значительные месяца. Это именно то, чего мы старались toosee.

Создадим другой рисунка ряда времени hello Калифорния молока производственных данных toosee того, насколько хорошо работает hello сезонных модели. Я добавил hello, следующий код в hello машинного обучения Azure [выполнение скрипта R] [ execute-r-script] toocreate hello модели и сделать построение.

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

Этот код запускается в машинном обучении Azure создает построения hello показано на рис.

![Данные молочного производства Калифорнии с моделью, включающей сезонные составляющие](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

*Рис. 24. Данные молочного производства Калифорнии с моделью, включающей сезонные составляющие*

Hello соответствия toohello данных показано на рис. 24 вместо поощряя. Тренд hello и влияние сезонных hello (ежемесячно вариант) найдите разумного.

Как проверку еще раз на нашей модели давайте взглянем на остатков hello. Hello следующее выражение вычисляет код hello прогнозируемые значения из наших двух моделей, вычисляет hello остатки для hello сезонных модели, а затем отображает эти остатки для hello обучающих данных.

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot hello residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

Hello остаточные рисунка показана на рис. 25.

![Остатки hello сезонных модели для hello обучающих данных](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

*Рис. 25. Остатки hello сезонных модель для hello обучающих данных.*

Выглядит вполне логично. Нет нет определенной структуры, за исключением hello эффект recession hello 2008-2009 г., который не учитывает нашей модели особенно хорошо.

показано на рис. 25 построения Hello полезно для определения шаблоны, зависящие от времени в остатков hello. явный подход Hello вычисление и отображение остатков hello, я использовал помещает остатков hello в порядке времени на диаграмме hello. Если на hello другой стороны, я графически в `milk.lm$residuals`, построения hello не было бы в порядке времени.

Можно также использовать `plot.lm()` tooproduce ряд диагностики графики.

    ## Show hello diagnostic plots for hello model
    plot(milk.lm2, ask = FALSE)

Пример ряда диагностических диаграмм, созданных с помощью этого кода, приведен на рис. 26.

![Первый из диагностики графики для hello сезонных модели](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Второе из диагностики графики для hello сезонных модели](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Третья из диагностики графики для hello сезонных модели](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Четвертая из диагностики графики для hello сезонных модели](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

*Рис. 26. Диагностика которых служат для hello сезонных модели.*

Существует несколько высокой влиятельные точек, указанных в этих графики, но ничего не toocause большую важность. Кроме того мы видим из построения обычный Q-Q hello, остатков hello закрыть распределенных, toonormally допущение важные для линейной модели.

### <a name="forecasting-and-model-evaluation"></a>Прогнозирование и оценка моделей
Имеется только один дополнительные toocomplete toodo самое нашего примера. Нам нужна toocompute прогнозов и сравнивать hello ошибки с hello фактические данные. Наш прогноз будет для hello 12 месяцев 2013. Мы можно вычислить меру ошибки для этого прогноза toohello фактические данные, не является частью нашей обучающий набор данных. Кроме того мы можно сравнить производительность на hello 18 лет обучающих данных toohello 12 месяцев тестовых данных.  

Используется несколько метрик производительности hello toomeasure модели временных рядов. В нашем случае мы будем использовать ошибка hello среднеквадратическое (RMS). Hello следующая функция вычисляет погрешность hello RMS между два ряда.  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function toocompute hello RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments toofunction RMS.error of wrong type encountered",
                    "ERROR: Input vector toofunction RMS.error is too short",
                    "ERROR: Input vectors toofunction RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check hello arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate hello values, else just copy
      if(is.log) {
        tryCatch( {
          temp1 <- exp(series1)
          temp2 <- exp(series2) },
          error = function(e){warning(messages[4]); NA}
        )
      } else {
        temp1 <- series1
        temp2 <- series2
      }

     ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute hello RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

Как и в hello `log.transform()` функция обсуждалось Здравствуйте, «Value преобразования» раздела, много ошибок проверки и исключение код восстановления в этой функции. принципы Hello, применяемых являются hello же. Hello работа выполняется в двух местах в оболочку `tryCatch()`. Во-первых hello временных рядов, exponentiated, так как мы работаем с журналами hello hello значений. Во-вторых обнаруженная ошибка RMS hello является вычисляемым.  

Давайте оснащенном hello toomeasure функция ошибки RMS, построения и выходных кадр данных, содержащая ошибки hello RMS. Мы будет включать термины hello тренда предназначенный только для модели и hello полную модель с сезонных факторов. Hello следующий код hello задания с помощью двух hello линейной модели, мы создания.

    ## Compute hello RMS error in a dataframe
    ## Include hello row names in hello first column so they will
    ## appear in hello output of hello Execute R Script
    RMS.df  <-  data.frame(
    rowNames = c("Trend Model", "Seasonal Model"),
      Traing = c(
      RMS.error(predict1[1:216], cadairydata$Milk.Prod[1:216]),
      RMS.error(predict2[1:216], cadairydata$Milk.Prod[1:216])),
      Forecast = c(
        RMS.error(predict1[217:228], cadairydata$Milk.Prod[217:228]),
        RMS.error(predict2[217:228], cadairydata$Milk.Prod[217:228]))
    )
    RMS.df

    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

Выполнение этого кода выводятся данные hello, показанный на рисунке 27 в hello порт вывода результирующего набора данных.

![Сравнение ошибок RMS для моделей hello][26]

*Рис. 27. Сравнение ошибок RMS для моделей hello.*

Эти результаты мы увидим, что добавление toohello сезонных факторов hello модель сокращает ошибки RMS hello значительно. Не слишком удивительно, но ошибка hello RMS для обучающих данных hello немного меньше hello прогноза.

## <a id="appendixa"></a>ПРИЛОЖЕНИИ a. Руководство по tooRStudio
RStudio хорошо задокументированы, поэтому в этом приложении я предоставлю некоторые ссылки toohello ключевые разделы документации tooget hello RStudio, которого вы начали.

1. Создание проектов
   
   С помощью RStudio можно организовывать свой код на R в проекты и управлять ими. Hello документацию, которая использует проектов можно найти на https://support.rstudio.com/hc/articles/200526207-Using-Projects.
   
   Я рекомендую, выполните следующую инструкцию и создать проект для примеров кода hello R в этом документе.  
2. Изменение и выполнение кода на R
   
   RStudio предоставляет интегрированную среду для изменения и выполнения кода на R. Документацию можно найти по адресу https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.
3. Отладка
   
   RStudio располагает эффективными возможностями отладки. Документацию по этим функциям можно найти по адресу https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.
   
   функции устранения неполадок Hello точки останова, задокументированы в https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.

## <a id="appendixb"></a>ПРИЛОЖЕНИЕ Б. Дополнительные материалы
Это программирования учебника описаны основы hello R действий требуется toouse hello язык R с студии машинного обучения Azure. Если вы еще не знакомы с языком R, на ресурсе CRAN можно найти два вводных курса:

* R для начинающих по Emmanuel Paradis это хорошая toostart на http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.  
* Введение tooR по N. Вт. Венаблес (W. N. Venables) и др. — немного более углубленный курс, доступный по адресу http://cran.r-project.org/doc/manuals/R-intro.html.

По языку R написано много книг, которые могут помочь в его освоении. Вот некоторые из них, которые показались мне наиболее полезными:

* Hello Art R программирования: Обзор из статистического программного обеспечения по Norman Matloff является tooprogramming отличным введением в R.  
* Рецепты R, Пол Teetor предоставляет и решение подход toousing R.  
* «R в действии» Роберта Кабакова (Robert Kabacoff) — еще одна полезная книга. веб-сайт быстрого R дополнительное Hello — полезным ресурсом на http://www.statmethods.net/.
* Является доступны бесплатно на http://www.burns-stat.com/documents/books/the-r-inferno/ Inferno R, Патрик Бернс удивительно пришлите книги, которое отвечает за ряд сложных и трудно разделы, которые могут быть обнаружены при программировании в книге R. hello.
* Если требуется глубокое погружение в дополнительные разделы в R, взглянем на книги hello Дополнительно R, Hadley Wickham. Hello Интернет-версию эта книга доступна бесплатно в http://adv-r.had.co.nz/.

Каталог пакетов ряда времени R можно найти в hello CRAN представление задач для анализа временных рядов: http://cran.r-project.org/web/views/TimeSeries.html. Сведения о пакеты объектов ряда определенное время должен указывать toohello документации для этого пакета.

Книга Hello вводные временных рядов с помощью R, Пол Cowpertwait и Эндрю Metcalfe предоставляет введение toousing R для анализа временных рядов. Множество других теоретических работ содержат примеры на языке R.

Некоторые полезные ресурсы в Интернете:

* DataCamp: DataCamp учебные R в удобства hello браузера с видео занятия и кодирования упражнений. Нет интерактивной учебники по hello последнюю методы R и пакеты. Время https://www.datacamp.com/courses/introduction-to-r выполнить hello свободного интерактивный учебник по языку R
* Руководство по началу работы с R из Programiz: https://www.programiz.com/r-programming
* Краткое руководство по R от Келли Блэк (Kelly Black) из университета Кларксон по адресу http://www.cyclismo.org/tutorial/R/.
* Ссылки на более чем 60 ресурсов по R: http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html.

<!--Image references-->
[1]: ./media/machine-learning-r-quickstart/fig1.png
[2]: ./media/machine-learning-r-quickstart/fig2.png
[3]: ./media/machine-learning-r-quickstart/fig3.png
[4]: ./media/machine-learning-r-quickstart/fig4.png
[5]: ./media/machine-learning-r-quickstart/fig5.png
[6]: ./media/machine-learning-r-quickstart/fig6.png
[7]: ./media/machine-learning-r-quickstart/fig7.png
[8]: ./media/machine-learning-r-quickstart/fig8.png
[9]: ./media/machine-learning-r-quickstart/fig9.png
[10]: ./media/machine-learning-r-quickstart/fig10.png
[11]: ./media/machine-learning-r-quickstart/fig11.png
[12]: ./media/machine-learning-r-quickstart/fig12.png
[13]: ./media/machine-learning-r-quickstart/fig13.png
[14]: ./media/machine-learning-r-quickstart/fig14.png
[15]: ./media/machine-learning-r-quickstart/fig15.png
[16]: ./media/machine-learning-r-quickstart/fig16.png
[17]: ./media/machine-learning-r-quickstart/fig17.png
[18]: ./media/machine-learning-r-quickstart/fig18.png
[19]: ./media/machine-learning-r-quickstart/fig19.png
[20]: ./media/machine-learning-r-quickstart/fig20.png
[21]: ./media/machine-learning-r-quickstart/fig21.png
[22]: ./media/machine-learning-r-quickstart/fig22.png

[26]: ./media/machine-learning-r-quickstart/fig26.png

<!--links-->
[appendixa]: #appendixa
[download]: https://azurebigdatatutorials.blob.core.windows.net/rquickstart/RFiles.zip


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
