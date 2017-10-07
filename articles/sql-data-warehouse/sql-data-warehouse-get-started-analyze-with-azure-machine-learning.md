---
title: "aaaAnalyze данных с помощью машинного обучения Azure | Документы Microsoft"
description: "Используйте машинного обучения Azure toobuild прогнозной модели машинного обучения на основе данных, хранимых в хранилище данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 95635460-150f-4a50-be9c-5ddc5797f8a9
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 03/02/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 337a2cd77aaad4467683827c56e5015b262b2554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a>Анализ данных с помощью машинного обучения Azure
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [машинное обучение Azure](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

В этом учебнике используется машинного обучения Azure toobuild прогнозной модели машинного обучения на основе данных, хранимых в хранилище данных SQL Azure. В частности для Adventure Works, велосипеда производственный hello и построен целевой маркетинговой кампании, по прогнозирование, если клиент является toobuy скорее всего, велосипед или нет.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a>Предварительные требования
toostep изучения этого руководства требуется:

* Хранилище данных SQL, в которое предварительно загружены демонстрационные данные AdventureWorksDW. tooprovision это, см. в разделе [создать хранилище данных SQL] [ Create a SQL Data Warehouse] и выберите образец hello tooload данных. Если хранилище данных уже существует, но в нем нет демонстрационных данных, вы можете [загрузить их вручную][load sample data manually].

## <a name="1-get-hello-data"></a>1. Получение данных hello
Hello данные находятся в представлении dbo.vTargetMail hello базы данных AdventureWorksDW hello. tooread эти данные:

1. Войдите в [Студию машинного обучения Azure][Azure Machine Learning studio] и щелкните My experiments (Мои эксперименты).
2. Щелкните **+ Создать** и выберите **Blank Experiment** (Пустой эксперимент).
3. Введите для своего эксперимента имя «Целевой маркетинг».
4. Перетащите hello **чтения** модуля из области модули hello в hello canvas.
5. Укажите сведения hello базы данных хранилища данных SQL на панели свойств hello.
6. Укажите базу данных hello **запроса** tooread hello данные представляют интерес.

```sql
SELECT [CustomerKey]
  ,[GeographyKey]
  ,[CustomerAlternateKey]
  ,[MaritalStatus]
  ,[Gender]
  ,cast ([YearlyIncome] as int) as SalaryYear
  ,[TotalChildren]
  ,[NumberChildrenAtHome]
  ,[EnglishEducation]
  ,[EnglishOccupation]
  ,[HouseOwnerFlag]
  ,[NumberCarsOwned]
  ,[CommuteDistance]
  ,[Region]
  ,[Age]
  ,[BikeBuyer]
FROM [dbo].[vTargetMail]
```

Запустите эксперимент hello, нажав кнопку **запуска** под холст эксперимента hello.
![Запустите эксперимент hello][1]

По завершении успешному выполнению эксперимента hello щелкните порт вывода hello внизу hello модуль считывания hello и выберите **визуализировать** toosee hello импортируемых данных.
![Просмотр импортированных данных][3]

## <a name="2-clean-hello-data"></a>2. Очистить hello данных
данные tooclean hello, удалите некоторые столбцы, которые не являются значимыми для моделей hello. toodo это:

1. Перетащите hello **столбцы проекта** модуля в hello canvas.
2. Нажмите кнопку **запуска средства выбора столбцов** в toospecify панели свойств hello, какие столбцы нужно toodrop.
   ![Столбцы проекта][4]
3. Исключите два столбца: CustomerAlternateKey и GeographyKey.
   ![Удаление ненужных столбцов][5]

## <a name="3-build-hello-model"></a>3. Построение модели hello
Разделите данные hello 80-20: 80% tootrain модели машинного обучения и 20% tootest hello модели. Будет использовать алгоритмы «Два класса» hello данной проблемы двоичной классификации.

1. Перетащите hello **разбиение** модуля в hello canvas.
2. Введите часть строк в hello первый выходной набор данных на панели свойств hello 0,8.
   ![Разделение данных на обучающую и тестовую выборки][6]
3. Перетащите hello **Двухклассового повышенного дерева принятия решений** модуля в hello canvas.
4. Перетащите hello **Обучение модели** модуля в hello холст и указания входных данных hello. Нажмите кнопку **запуска средства выбора столбцов** hello панели свойств.
   * Первый входной набор данных: алгоритм ML.
   * Во-вторых входных данных: алгоритм hello tootrain данных на.
     ![Подключение hello модуль обучения модели][7]
5. Выберите hello **BikeBuyer** столбец как столбец toopredict hello.
   ![Выберите столбец toopredict][8]

## <a name="4-score-hello-model"></a>4. Модель оценки hello
Теперь мы проверим, как выполняет hello модели к тестовым данным. Мы сравнит алгоритм hello Выбор с toosee другой алгоритм, который дает более высокую производительность.

1. Перетащите **модель оценки** модуля в hello canvas.
    Сначала ввода: обучение модели второй набор входных данных: данные теста ![hello модель оценки][9]
2. Перетащите hello **Двухклассовая Байесовская Точечная машина** на холст эксперимента hello. Мы сравнит, как работает этот алгоритм в toohello сравнения Двухклассового повышенного дерева принятия решений.
3. Копировать и вставить hello модулей Обучение модели и оценка модели hello холст.
4. Перетащите hello **модель оценки** модуля в hello холст toocompare hello двух алгоритмов.
5. **Запустите** hello эксперимента.
   ![Запустите эксперимент hello][10]
6. Щелкните порт вывода hello внизу hello hello модель оценки модуль и выберите визуализировать.
   ![Отображение результатов классификации][11]

Hello метрики, предоставляемые являются кривой ROC hello, диаграмма точности отзыв и поднимите кривой. Глядя на эти показатели, мы видим первой модели hello выполняется лучше, чем второй hello. toolook на hello hello прогнозировать первой модели, щелкните выходной порт hello модель оценки и щелкните визуализировать.
![Отображение результатов вычисления][12]

Вы увидите, что tooyour проверочный набор данных добавлено два дополнительных столбца.

* Оцененных вероятностей: hello вероятность, что пользователь является Покупатель велосипеда.
* Оцененный метки: hello классификация выполненную hello модели — «Покупатель велосипеда» (1) или нет (0). Этот порог вероятности для пометки задается too50% и могут быть изменены.

Сравнение столбцов hello BikeBuyer (фактические) с hello меток оцененных значений (прогноз), можно увидеть, насколько успешно выполнены hello модели. Как в этом случае можно использовать toomake этой модели прогнозов для новых клиентов и опубликовать эту модель веб-службы или записать результаты назад tooSQL хранилища данных.

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о создании прогнозных моделей машинного обучения, см. слишком[tooMachine введение обучения в Azure][Introduction tooMachine Learning on Azure].

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img1_reader.png
[2]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img2_visualize.png
[3]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img3_readerdata.png
[4]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img4_projectcolumns.png
[5]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img5_columnselector.png
[6]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img6_split.png
[7]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img7_train.png
[8]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img8_traincolumnselector.png
[9]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img9_score.png
[10]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img10_evaluate.png
[11]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img11_evalresults.png
[12]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img12_scoreresults.png


<!--Article references-->
[Azure Machine Learning studio]:https://studio.azureml.net/
[Introduction tooMachine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
