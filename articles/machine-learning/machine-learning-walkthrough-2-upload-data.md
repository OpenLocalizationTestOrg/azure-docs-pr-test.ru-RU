---
title: "Шаг 2. Отправка данных в эксперимент машинного обучения | Документация Майкрософт"
description: "Шаг 2 из hello разработка прогнозирующего решения Пошаговое руководство: отправка общих данных сохраняются в студии машинного обучения Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 9f4bc52e-9919-4dea-90ea-5cf7cc506d85
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 0ea21dcca2d0934ed06508560cf85cf31b48ce6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a>Шаг 2 пошагового руководства: отправка существующих данных в эксперимент Машинного обучения Azure
Это второй шаг hello hello пошагового руководства, [разрабатывать решения для прогнозирующего анализа в машинном обучении Azure](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Создание рабочей области машинного обучения](machine-learning-walkthrough-1-create-ml-workspace.md)
2. **Отправка существующих данных**
3. [Создание нового эксперимента](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Обучать и оценивать модели hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Развернуть веб-службу hello](machine-learning-walkthrough-5-publish-web-service.md)
6. [Доступ к веб-службе hello](machine-learning-walkthrough-6-access-web-service.md)

- - -
toodevelop прогнозной модели для кредитного риска, мы должны данные, которые мы использовать tootrain и проверить модель hello. В данном пошаговом руководстве мы будем использовать hello «Набора данных UCI Statlog (немецкий данные кредитной)» из репозитория машинного обучения компании Irvine UC hello. Его можно найти по следующей ссылке:   
<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a>.

Мы будем использовать hello файл с именем **german.data**. Загрузите этот файл tooyour локальный жесткий диск.  

Hello **german.data** набор данных содержит строки 20 переменных для 1000 последних кандидатов для кредита. Эти 20 переменные представляют набор функций hello dataset (hello *вектора компонента*), который предоставляет идентифицирующие характеристики для каждого кандидата кредит. Дополнительный столбец в каждой строке представляет hello кандидата вычисляемые кредитного риска, с 700 кандидатами, которые определены как низкий кредитного риска и 300 как высокого риска.

веб-сайт UCI Hello содержит описание атрибутов hello hello вектора компонента для этих данных. Сюда входят финансовые сведения, кредитная история, занятость и личные сведения. Для каждого претендента приведен двоичный рейтинг, указывающий низкий или высокий кредитный риск. 

Мы будем использовать этот tootrain данных модели прогнозирования. Закончив, нашей модели необходимо будет tooaccept вектора компонента для нового пользователя и прогнозировать, является ли он или она высокое или низкое кредитного риска.  

Есть один интересный момент. Здравствуйте описания hello набора данных на веб-сайте упоминания hello UCI расходы Если мы misclassify человека кредитного риска.
Если hello модель прогнозирует высокой кредитного риска для тех, кто является фактически низкий кредитного риска, hello модели внес misclassification.
Пять раз больше toohello финансового учреждения, то обратная misclassification hello: Если hello модель прогнозирует низкий кредитного риска для тех, кто является фактически высокой кредитного риска.

Таким образом мы хотим tootrain нашей модели, чтобы hello этот последний тип misclassification обходится в пять раз выше, чем ошибочную hello другим способом.
Один простой способ toodo это при обучении модели hello в нашем эксперименте — путем дублирования (пять раз) те операции, которые представляют кого-либо с высокой кредитного риска. Затем если hello модели misclassifies кто-то как низкий кредитного риска, когда они фактически высокого риска, hello модели не этой же misclassification пять раз, один раз для каждого дубликата. Это увеличит стоимость hello эту ошибку в результаты обучения hello.


## <a name="convert-hello-dataset-format"></a>Преобразовать формат набора данных hello
Hello исходный набор данных используется формат разделенных пустым. Студия машинного обучения лучше работает с файл значений с разделителями запятыми (CSV), мы будем преобразования набора данных hello, заменив пробелы с запятыми.  

Существует много способов tooconvert эти данные. Одним из способов является использование hello следующую команду Windows PowerShell:   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

Другим способом является использование команды sed hello Unix:  

    sed 's/ /,/g' german.data > german.csv  

В любом случае мы создали CSV-версию hello данных в файл с именем **german.csv** , можно использовать в наших эксперимента.

## <a name="upload-hello-dataset-toomachine-learning-studio"></a>Отправка tooMachine hello набор данных Studio обучения
После того, как данные hello были преобразованный tooCSV формата, мы должны tooupload его в студии машинного обучения. 

1. Домашняя страница Привет открыть студии машинного обучения ([https://studio.azureml.net](https://studio.azureml.net)). 

2. Щелкните меню hello ![меню][1] hello верхнего левого угла окна hello, щелкните **машинного обучения Azure**выберите **Studio**и выполните вход.

3. Нажмите кнопку **+ создать** hello нижней части окна hello.

4. Выберите **НАБОР ДАННЫХ**.

5. Выберите **ИЗ ЛОКАЛЬНОГО ФАЙЛА**.

    ![Добавление набора данных из локального файла][2]

6. В hello **отправить новый набор данных** диалоговое окно, нажмите кнопку **Обзор** и найти hello **german.csv** созданный файл.

7. Введите имя для набора данных hello. В этом пошаговом руководстве назовем его UCI German Credit Card Data.

8. Для типа данных выберите **Универсальный CSV-файл без заголовка (.nh.csv)**.

9. При желании добавьте описание.

10. Нажмите кнопку hello **ОК** флажок.  

    ![Передача hello набора данных][3]

Это передает данные hello в модуль набора данных, который можно использовать в эксперименте.

Можно управлять наборами данных, щелкнув hello загруженные tooStudio **наборы данных** toohello вкладка левой части окна Studio hello.

![Управление наборами данных][4]

Дополнительные сведения об импорте других типов данных в эксперимент см. в статье [Импорт обучающих данных в Студию машинного обучения Azure из разных источников данных](machine-learning-data-science-import-data.md).

**Далее:[ создание эксперимента](machine-learning-walkthrough-3-create-new-experiment.md)**

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
