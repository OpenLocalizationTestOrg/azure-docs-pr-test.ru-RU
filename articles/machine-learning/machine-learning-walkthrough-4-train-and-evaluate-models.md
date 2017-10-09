---
title: "Шаг 4: Обучать и оценивать прогнозных моделей аналитической hello | Документы Microsoft"
description: "Шаг 4 hello разработка прогнозирующего решения Пошаговое руководство: обучение, оценки и оценить несколько моделей в студии машинного обучения Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: d905f6b3-9201-4117-b769-5f9ed5ee1cac
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: d86d7c5ae7524f71fe44d985db67c4618b7965a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-hello-predictive-analytic-models"></a>Шаг 4 пошагового руководства: Обучать и оценивать прогнозных моделей аналитической hello
В этом разделе содержатся hello четвертый шаг руководства hello [разрабатывать решения для прогнозирующего анализа в машинном обучении Azure](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Создание рабочей области машинного обучения](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Отправка существующих данных](machine-learning-walkthrough-2-upload-data.md)
3. [Создание нового эксперимента](machine-learning-walkthrough-3-create-new-experiment.md)
4. **Обучать и оценивать модели hello**
5. [Развернуть веб-службу hello](machine-learning-walkthrough-5-publish-web-service.md)
6. [Доступ к веб-службе hello](machine-learning-walkthrough-6-access-web-service.md)

- - -
Одно из преимуществ использования студии машинного обучения Azure для создания моделей машинного обучения hello не более чем один тип модели tootry возможность hello одновременно в одном эксперимента, сравнить результаты hello. Этот тип экспериментов помогает найти hello оптимальное решение для конкретной задачи.

В эксперименте hello мы разрабатываем в этом пошаговом руководстве мы создания двух разных типов моделей и сравнить их оценки результатов toodecide какой алгоритм мы хотим toouse в наших окончательного эксперимента.  

Существует множество моделей, которые можно выбрать. модели toosee hello, доступные, разверните hello **машинного обучения** узла в палитре модуля hello и разверните **модель инициализации** и hello узлы под ним. Для целей этого эксперимента hello, мы выберем hello [Двухклассовая машина опорных векторов] [ two-class-support-vector-machine] (SVM) и hello [Двухклассового повышенного дерева принятия решений] [ two-class-boosted-decision-tree] модули.    

> [!TIP]
> tooget решить, какой алгоритм машинного обучения лучше всего подходит для конкретной проблемы hello вы пытаетесь toosolve см. в разделе [как алгоритмы машинного обучения Microsoft Azure toochoose](machine-learning-algorithm-choice.md).
> 
> 

## <a name="train-hello-models"></a>Обучение моделей hello

Мы добавим обе hello [Двухклассового повышенного дерева принятия решений] [ two-class-boosted-decision-tree] модуля и [Двухклассовая машина опорных векторов] [ two-class-support-vector-machine] модуля в этом эксперимента.

### <a name="two-class-boosted-decision-tree"></a>Двухклассовое увеличивающееся дерево принятия решений;

Во-первых можно перейти к настройке модели дерева принятия решений повышенного hello.

1. Найти hello [Двухклассового повышенного дерева принятия решений] [ two-class-boosted-decision-tree] модуля в палитре модуля hello и перетащите его на холсте hello.

2. Найти hello [Обучение модели] [ train-model] модуля, перетащите его на холсте hello, а затем подключите выход hello hello [Двухклассового повышенного дерева принятия решений] [ two-class-boosted-decision-tree]toohello модуль левому входному порту hello [Обучение модели] [ train-model] модуля.
   
   Hello [Двухклассового повышенного дерева принятия решений] [ two-class-boosted-decision-tree] модуль инициализирует hello универсальная модель, и [Обучение модели] [ train-model] использует обучающих данных модель tootrain hello. 

3. Подсоедините hello левой выход слева hello [выполнение скрипта R] [ execute-r-script] toohello модуль справа входному порту hello [Обучение модели] [ train-model] модуля (мы решено в [шаг 3](machine-learning-walkthrough-3-create-new-experiment.md) это пошаговое руководство toouse hello данных, поступающих из hello левая сторона модуля hello разбиение данных для обучения).
   
   > [!TIP]
   > Нам не нужен два hello входов и один из выходов hello hello [выполнение скрипта R] [ execute-r-script] модуля в этом эксперименте, поэтому можно оставить их неприкрепленные. 
   > 
   > 

Эта часть эксперимента hello теперь выглядит примерно следующим образом:  

![Обучение модели][1]

Теперь нам нужно tootell hello [Обучение модели] [ train-model] модуля, что мы хотим значение hello модели toopredict hello кредитного риска.

1. Выберите hello [Обучение модели] [ train-model] модуля. В hello **свойства** области, нажмите кнопку **запуска средства выбора столбцов**.

2. В hello **выберите один столбец** диалоговое окно, введите в поле поиска hello в разделе «риск кредита» **доступные столбцы**, выберите «Риск кредита» ниже и нажмите кнопку со стрелкой вправо hello ( **>** ) toomove «Кредита риска» слишком**выбранные столбцы**. 

    ![Выберите столбец hello кредитного риска для hello модуль обучения модели][0]

3. Нажмите кнопку hello **ОК** флажок.

### <a name="two-class-support-vector-machine"></a>Двухклассовая машина опорных векторов;

Далее мы устанавливаем модель SVM hello.  

Сначала немного информации о SVM. "Повышенные" деревья принятия решения хорошо работают с атрибутами любого типа. Тем не менее, так как модуль SVM hello создает линейный классификатор, hello модели, который создается, имеет hello наиболее Ошибка теста после всех числовых функций hello же шкале. tooconvert все числовые функции toohello же масштабирования, мы используем преобразования «Tanh» (с hello [нормализовать данные] [ normalize-data] модуля). Это преобразует нашей числа в диапазон hello [0,1]. модуль SVM Hello преобразует строки функции toocategorical функций и затем toobinary 0 и 1, поэтому мы не требуется toomanually преобразование строки функции. Кроме того, мы не хотим tootransform hello кредитного риска в столбце (21) — это числовые, но это значение hello, мы обучения hello toopredict модели, поэтому необходимо tooleave его отдельно.  

tooset модель SVM hello, hello следующие:

1. Найти hello [Двухклассовая машина опорных векторов] [ two-class-support-vector-machine] модуля в палитре модуля hello и перетащите его на холсте hello.

2. Щелкните правой кнопкой мыши hello [Обучение модели] [ train-model] модуль, выберите **копирования**, щелкните hello полотна правой кнопкой мыши и выберите **вставить**. Здравствуйте, копия hello [Обучение модели] [ train-model] модуль имеет hello же Выбор столбцов, как исходный hello.

3. Подсоедините hello выход hello [Двухклассовая машина опорных векторов] [ two-class-support-vector-machine] toohello модуль слева входного порта hello второй [Обучение модели] [ train-model] модуль.

4. Найти hello [нормализовать данные] [ normalize-data] модуля и перетащите его на холсте hello.

5. Подсоедините hello левой выход слева hello [выполнение скрипта R] [ execute-r-script] toohello входного модуля этого модуля (Обратите внимание, что hello выходной порт модуля может быть подключенным toomore больше одного модуля).

6. Подключение hello слева выходной порт hello [нормализовать данные] [ normalize-data] модуль toohello право входному порту hello, во-вторых [Обучение модели] [ train-model] модуля.

Теперь эта часть эксперимента должна выглядеть следующим образом.  

![Второй модели обучения hello][2]  

Теперь настройка hello [нормализовать данные] [ normalize-data] модуля:

1. Нажмите кнопку tooselect hello [нормализовать данные] [ normalize-data] модуля. В hello **свойства** выберите **Tanh** для hello **метод преобразования** параметра.

2. Нажмите кнопку **запуска средства выбора столбцов**, выберите «Нет столбцов» для **начинаются с**выберите **Include** в первом раскрывающемся списке hello выберите **тип столбца**в hello второго раскрывающегося списка и выберите **числовое** в третьем раскрывающемся списке hello. Указывает, преобразуются все hello числовых столбцов (и только числовые).

3. Нажмите кнопку hello toohello знак плюс (+) слева от этой строки — это создает строку из раскрывающихся списков. Выберите **исключить** в первом раскрывающемся списке hello выберите **имена столбцов** в hello второго раскрывающегося списка и введите «Кредит риск» в поле текста hello. Это указывает, что следует игнорировать этот столбец кредитного риска hello (требуются toodo это потому, что этот столбец является числовым и поэтому будет преобразовано мы не исключения).

4. Нажмите кнопку hello **ОК** флажок.  

    ![Выберите столбцы для hello нормализовать данные модуля][5]

Hello [нормализовать данные] [ normalize-data] модуль теперь является набор tooperform Tanh преобразование для всех числовых столбцов за исключением столбца hello кредитного риска.  

## <a name="score-and-evaluate-hello-models"></a>Оценка и оценивать модели hello

Мы используем hello проверочных данных, который был в зависимости от hello [разбиение данных] [ split] tooscore модуль нашей обученных моделей. Затем можно сравнить результаты двух моделей toosee hello, создавшего лучшие результаты hello.  

### <a name="add-hello-score-model-modules"></a>Добавить модель оценки модулей hello

1. Найти hello [модель оценки] [ score-model] модуля и перетащите его на холсте hello.

2. Подключение hello [Обучение модели] [ train-model] модуль, который был подключен toohello [Двухклассового повышенного дерева принятия решений] [ two-class-boosted-decision-tree] модуль toohello левый вход порт hello [модель оценки] [ score-model] модуля.

3. Подключение правой hello [выполнение скрипта R] [ execute-r-script] toohello модуля (нашей проверочных данных) право входному порту hello [модель оценки] [ score-model] модуля.

    ![Модуль "Score Model" (Оценка модели) подключен][6]
   
   Hello [модель оценки] [ score-model] модуля, теперь могут получить сведения о кредитной hello из hello проверочных данных, запустите его через модель hello, и прогнозы hello сравнения моделей hello создаются с hello фактическое кредит риска столбец в hello проверочных данных.

4. Скопируйте и вставьте hello [модель оценки] [ score-model] toocreate модуль второй копии.

5. Подключите выход hello модели SVM hello (то есть hello выходной порт hello [Обучение модели] [ train-model] модуль, который был подключен toohello [Двухклассовая машина опорных векторов] [ two-class-support-vector-machine] модуля) toohello входному порту hello второй [модель оценки] [ score-model] модуля.

6. Hello модели опорных Векторов у нас есть toodo hello и те же данные теста toohello преобразования, как это делалось toohello обучающих данных. Таким образом, скопируйте и вставьте hello [нормализовать данные] [ normalize-data] toocreate модуль второй копии и подключите его вправо toohello [выполнение скрипта R] [ execute-r-script] модуля.

7. Затем подсоедините hello левой выход hello [нормализовать данные] [ normalize-data] toohello модуль справа входному порту hello, во-вторых [модель оценки] [ score-model] модуль.

    ![Оба модуля "Score Model" (Оценка модели) подключены][7]

### <a name="add-hello-evaluate-model-module"></a>Добавить модуль оценки модели hello

tooevaluate hello двух результатов массовой оценки и сравнить их, мы используем [модель оценки] [ evaluate-model] модуля.  

1. Найти hello [модель оценки] [ evaluate-model] модуля и перетащите его на холсте hello.

2. Подключение hello выходной порт hello [модель оценки] [ score-model] модуль, связанный с hello повышенного дерева модели toohello слева входному порту hello принятия решений [модель оценки] [ evaluate-model] модуля.

3. Подключение hello других [модель оценки] [ score-model] toohello модуль справа входному порту.  

    ![Модуль "Evaluate Model" (Анализ модели) подключен][8]

### <a name="run-hello-experiment-and-check-hello-results"></a>Запустите эксперимент hello и проверьте результаты hello

toorun Здравствуйте эксперимент, выберите hello **ЗАПУСКА** кнопки ниже hello холста. Это может занять несколько минут. Признак вращающийся для каждого модуля показывает, он работает, и затем зеленая галочка показывает завершении hello модуля. Если флажок установлен для всех модулей hello, эксперимента hello завершит работу.

Hello эксперимента теперь должна выглядеть примерно следующим образом:  

![Сравнение обеих моделей][3]

toocheck hello, щелкните выходной порт hello hello [модель оценки] [ evaluate-model] модуль и выберите **визуализировать**.  

Hello [модель оценки] [ evaluate-model] модуль создает пару кривых и метрик, которые позволяют вам toocompare hello результаты двух моделей Оцененный hello. Можно просмотреть результаты hello как оператор характеристики приемника (ROC) кривых, точности и отзыва кривых или кривых точности прогнозов. Дополнительные данные, отображаемые включает матрицей, совокупные значения для hello площадь под кривой hello (AUC) и другие показатели. Можно изменить пороговое значение hello путем перемещения hello ползунок влево или вправо и увидеть, как он влияет hello набор показателей.  

Щелкните toohello справа от диаграммы hello **Оцененный набор данных** или **Оцененный набор данных toocompare** toohighlight hello связанного кривых и toodisplay hello связанных метрик ниже. В условных обозначениях hello кривых hello, «Оцененный набор данных» соответствует toohello левому входному порту hello [модель оценки] [ evaluate-model] модуля — в нашем случае это hello повышенного модели дерева принятия решений. «Оцененный набор данных toocompare» соответствует toohello правый входной порт - модель SVM hello в нашем случае. При выборе одного из этих меток, выделяется hello кривой для данной модели, а соответствующие метрики hello отображаются, как показано в следующих график hello.  

![Кривые ROC для моделей][4]

Изучив эти значения, можно решить, какую модель является ближайшим toogiving hello результаты, которые вы ищете. Можно вернуться назад и завершение цикла эксперимента, изменив значения параметров в разных моделях hello. 

Научные Hello и искусство интерпретации этих результатов и настройка производительности hello модели используется вне области hello этого пошагового руководства. Для получения дополнительной справки может прочитать hello в следующих статьях:
- [Как tooevaluate модели производительности в машинном обучении Azure](machine-learning-evaluate-model-performance.md)
- [Выберите параметры toooptimize алгоритмов в машинном обучении Azure](machine-learning-algorithm-parameters-optimize.md)
- [Интерпретация результатов модели в машинном обучении Azure](machine-learning-interpret-model-results.md)

> [!TIP]
> Каждый раз при выполнении эксперимента hello запись этой итерации сохраняется hello журнал выполнения. Можно просматривать эти итераций и возвращать tooany из них, щелкнув **ПРОСМОТРЕТЬ ЖУРНАЛ ВЫПОЛНЕНИЯ** ниже hello холста. Можно также щелкнуть **предыдущего запуска** в hello **свойства** области tooreturn toohello итерации, непосредственно предшествующего hello один было открыто.
> 
> Можно сделать копию какой-либо итерации эксперимента, щелкнув **SAVE AS** ниже hello холста. 
> Используйте hello эксперимента **Сводка** и **описание** tookeep свойства записи были проверены в эксперименте итераций.
> 
> Дополнительные сведения см. в статье [Управление итерациями экспериментов в Студии машинного обучения Azure](machine-learning-manage-experiment-iterations.md).  
> 
> 

- - -
**Далее: [развернуть веб-службу hello](machine-learning-walkthrough-5-publish-web-service.md)**

[0]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/train-model-select-column.png
[1]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/experiment-with-train-model.png
[2]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/svm-model-added.png
[3]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/final-experiment.png
[4]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/roc-curves.png
[5]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/normalize-data-select-column.png
[6]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/score-model-connected.png
[7]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/both-score-models-added.png
[8]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/evaluate-model-added.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
