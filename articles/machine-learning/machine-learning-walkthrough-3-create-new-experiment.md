---
title: "Шаг 3. Создание эксперимента машинного обучения | Документация Майкрософт"
description: "Шаг 3 из hello разработка прогнозирующего решения Пошаговое руководство: Создание нового эксперимента обучения в студии машинного обучения Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 660e3c27-55ef-4c33-a4e9-dff4d1224630
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 4697d461a205c50c8d2aa6a3bd56697840cb30f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a>Шаг 3. Создание эксперимента машинного обучения Azure
Это третий шаг hello hello пошагового руководства, [разрабатывать решения для прогнозирующего анализа в машинном обучении Azure](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Создание рабочей области машинного обучения](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Отправка существующих данных](machine-learning-walkthrough-2-upload-data.md)
3. **Создание нового эксперимента**
4. [Обучать и оценивать модели hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Развернуть веб-службу hello](machine-learning-walkthrough-5-publish-web-service.md)
6. [Доступ к веб-службе hello](machine-learning-walkthrough-6-access-web-service.md)

- - -
следующим шагом Hello в этом пошаговом руководстве является toocreate эксперимента в студии машинного обучения, использующий hello набор данных, которые мы отправлен.  

1. В Studio щелкните **+ создать** hello нижней части окна hello.
2. Выберите **ЭКСПЕРИМЕНТА**, а затем выберите "Пустой эксперимент". 

    ![Создание нового эксперимента][0]

2. По умолчанию выберите hello поэкспериментировать имя hello верхней части холста hello и переименуйте его toosomething смысла.

    ![Переименование эксперимента][5]
   
   > [!TIP]
   > Это toofill рекомендаций в **Сводка** и **описание** в эксперименте hello в hello **свойства** области. Эти свойства, присвойте hello эксперимента hello toodocument вероятность того, кто просматривает его позже будет понять цели и методологии.
   > 
   > ![Свойства эксперимента][6]
   > 
3. Hello модуля палитры toohello слева холст эксперимента hello, разверните **сохраненные наборы данных**.
4. Созданный в набор данных поиска hello **Мои наборы данных** и перетащите его на холсте hello. Hello набор данных также можно найти, введя имя hello в hello **поиска** поле над hello палитры.  

    ![Добавить toohello эксперимента hello набора данных][7]

## <a name="prepare-hello-data"></a>Подготовка данных hello
Можно просмотреть hello первые 100 строк данных hello и некоторые статистические данные для всего набора данных hello: щелкните порт вывода hello hello набора данных (hello маленький кружок hello нижней) и выберите **визуализировать**.  

Файл данных hello не поставляются с заголовками столбцов, Studio разработала универсальный заголовки (Col1, Col2 *т. д.*). Хороший заголовки не essential toocreating модели, но они позволяют проще toowork с данными hello в эксперименте hello. Кроме того при со временем мы опубликовать эту модель в веб-службе, заголовки hello выяснить hello столбцы toohello пользователем службы hello.  

Можно добавить заголовки столбцов с помощью hello [редактирование метаданных] [ edit-metadata] модуля.
Использовать hello [редактирование метаданных] [ edit-metadata] toochange метаданных модуля, связанные с набором данных. В этом случае мы используем его tooprovide более понятные имена для заголовков столбцов. 

toouse [редактирование метаданных][edit-metadata], сначала необходимо указать, какие столбцы toomodify (в этом случае все из них.) Затем укажите действие toobe hello, для этих столбцов (в данном случае изменение заголовков столбцов.)

1. В палитре hello модуль, введите «метаданные» в hello **поиска** поле. Hello [редактирование метаданных] [ edit-metadata] отображается в списке модулей hello.

2. Щелкните и перетащите hello [редактирование метаданных] [ edit-metadata] модуля на hello холст и разместите его под hello набора данных, мы добавили в более ранних версий.

3. Подключения hello dataset toohello [редактирование метаданных][edit-metadata]: щелкните порт вывода hello hello набора данных (hello маленький кружок внизу hello hello набора данных), перетащите toohello входному порту [редактирование метаданных ] [ edit-metadata] (hello маленький кружок вверху hello модуля "hello"), затем отпустите кнопку мыши hello. набор данных Hello и модуль оставались подключенными, даже если перемещать либо на холсте hello.
   
   Hello эксперимента теперь должна выглядеть примерно следующим образом:  
   
   ![Добавление модуля "Изменение метаданных"][1]
   
   Hello красный восклицательный знак указывает, что мы не задали еще hello свойства для этого модуля. Мы сделаем это позже.
   
   > [!TIP]
   > Можно добавить модуль tooa комментарий, дважды щелкните модуль hello и вводить текст. Это может помочь быстро выяснить делает какой модуль hello в эксперименте. В этом случае дважды щелкните hello [редактирование метаданных] [ edit-metadata] модуля и типа hello комментарий «добавить заголовки столбцов». Щелкните любой другой hello холст tooclose hello текстовое поле. toodisplay Здравствуйте комментарий, щелкните hello со стрелкой вниз в модуле hello.
   > 
   > ![Модуль Edit Metadata (Изменение метаданных) с добавленными комментариями][8]
   > 
4. Выберите [редактирование метаданных][edit-metadata]и в hello **свойства** toohello панели справа от холста hello щелкните **запуска средства выбора столбцов**.

5. В hello **выберите столбцы** диалоговое окно, выберите все hello строк в **доступные столбцы** и нажмите кнопку > toomove их слишком**выбранные столбцы**.
   диалоговое окно приветствия должен выглядеть следующим образом:

   ![Селектор столбцов, где выделены все столбцы][2]

6. Нажмите кнопку hello **ОК** флажок.

7. Вернитесь в hello **свойства** панели найдите hello **новые имена столбцов** параметра. В этом поле введите список имен для hello 21 столбцов в наборе данных hello, разделенных запятыми и в порядке столбцов. Имена столбцов hello можно получить из документации hello набора данных на веб-сайте UCI hello, или для удобства можно скопировать и вставить hello после списка:  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   Панель свойств Hello выглядит следующим образом:
   
   ![Свойства модуля "Изменение метаданных"][3]

> [!TIP]
> Заголовки столбцов tooverify hello, выполните эксперимент hello (щелкните **ЗАПУСКА** ниже холст эксперимента hello). При ее работы (зеленая галочка на [редактирование метаданных][edit-metadata]), щелкните выходной порт hello hello [редактирование метаданных] [ edit-metadata] модуль, а затем выберите **визуализировать**. Можно просмотреть выходные данные hello любого модуля в hello же выполняется hello tooview способом hello данных через эксперимент hello.
> 
> 

## <a name="create-training-and-test-datasets"></a>Создание обучающих и тестовых наборов данных
Необходимы некоторые tootrain hello модели данных и некоторые tootest его.
Поэтому следующий шаг hello hello эксперимента, мы разделить hello набора данных на два отдельных набора данных: один — для изучения нашей модели, а второй для ее проверки.

toodo это, мы используем hello [разбиение данных] [ split] модуля.  

1. Найти hello [разбиение данных] [ split] модуля, перетащите его на холсте hello и подключите его toohello [редактирование метаданных] [ edit-metadata] модуля.

2. По умолчанию hello пропорции разделения является 0.5 и hello **случайного разбиения** параметр имеет значение. Это означает, что случайные половина данных hello выходных данных через один порт hello [разбиение данных] [ split] модуль и половина через hello других. Вы можете настроить эти параметры, а также hello **случайное начальное значение** параметр toochange hello разделены на обучающие и проверочные данные. Для этого примера оставим их как есть.
   
   > [!TIP]
   > Здравствуйте, свойство **часть строк в hello сначала выходной набор данных** определяет, какая часть данных hello выходных данных через hello *левой* порта вывода. Для экземпляра Если too0.7 отношение hello, 70% hello данных является выходных данных через hello оставить порт и 30% через порт правой hello.  
   > 
   > 

3. Дважды щелкните hello [разбиение данных] [ split] модуля и ввести комментарий hello, «обучение и тестирование данные разделены на 50%». 

Мы можем использовать выходные данные hello hello [разбиение данных] [ split] модуль тем не менее мы, например, но позволяет выбрать toouse hello левой выходные данные в виде обучающих данных и правом hello выходные данные как проверочных данных.  

Как упоминалось в hello [ранее](machine-learning-walkthrough-2-upload-data.md), ошибочную высокой кредитного риска в качестве низкая стоимость hello пять раз выше, чем стоимость hello ошибочную низкий кредитного риска в как high. tooaccount для этого мы создаем новый набор данных, отражающий эта функция затрат. В hello новый набор данных в каждом примере высокого риска реплицируются пять раз, пока не реплицируются в каждом примере низким уровнем риска.   

Эту репликацию можно выполнить с помощью кода R:  

1. Поиск и перетащите hello [выполнение скрипта R] [ execute-r-script] модуля на холст эксперимента hello. 

2. Подключение hello слева выходной порт hello [разбиение данных] [ split] toohello модуль сначала входному порту («Dataset1») для hello [выполнение скрипта R] [ execute-r-script] модуль.

3. Дважды щелкните hello [выполнение скрипта R] [ execute-r-script] модуля и ввести комментарий hello, «Набор Корректировка себестоимости».

4. В hello **свойства** области, удалите текст по умолчанию hello в hello **R-сценарий** параметр и введите этот скрипт:
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![Сценарий R в модуле hello выполнение скрипта R][9]

Мы должны toodo этой же репликации операции для каждого выхода hello [разбиение данных] [ split] Корректировка себестоимости модуль, так что hello обучающих и проверочных данных имеют hello таким же. Здравствуйте, наиболее простым способом toodo, это путем дублирования hello [выполнение скрипта R] [ execute-r-script] модуля мы только что внесли и подключения его toohello других выходных портом hello [разбиение данных] [ split] модуля.

1. Щелкните правой кнопкой мыши hello [выполнение скрипта R] [ execute-r-script] модуль и выберите **копирования**.

2. Щелкните правой кнопкой мыши на холст эксперимента hello и выберите **вставить**.

3. Перетащите новый модуль hello в положение, а затем подключите hello правой выходной порт hello [разбиение данных] [ split] toohello модуль сначала входному порту этого нового [выполнение скрипта R] [ execute-r-script] модуля. 

4. Hello нижней части холста hello, нажмите кнопку **запуска**. 

> [!TIP]
> Hello копии hello выполнение скрипта R модуля содержит hello же сценариев в hello исходного модуля. При копировании и вставке модуля на холсте hello, hello копирования сохраняет все свойства hello исходного hello.  
> 
> 

На эксперимент теперь выглядит приблизительно так:

![Добавление модуля Разделение и скриптов R][4]

Подробнее об использовании сценариев R в экспериментах см. в разделе [Расширение возможностей эксперимента с помощью R](machine-learning-extend-your-experiment-with-r.md).

**Далее: [обучения и оценки моделей hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)**

[0]: ./media/machine-learning-walkthrough-3-create-new-experiment/create-new-experiment.png
[5]: ./media/machine-learning-walkthrough-3-create-new-experiment/rename-experiment.png
[6]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-properties.png
[7]: ./media/machine-learning-walkthrough-3-create-new-experiment/add-dataset-to-experiment.png
[8]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-with-comment.png
[9]: ./media/machine-learning-walkthrough-3-create-new-experiment/execute-r-script.png
[1]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-with-edit-metadata-module.png
[2]: ./media/machine-learning-walkthrough-3-create-new-experiment/select-columns.png
[3]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-properties.png
[4]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
