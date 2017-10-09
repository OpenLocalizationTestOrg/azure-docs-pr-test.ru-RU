---
title: "Hello командного процесса обработки и анализа данных в действие — с помощью кластера Azure HDInsight Hadoop для набора данных 1 ТБ | Документы Microsoft"
description: "С помощью hello процесс обработки и анализа данных для команды сценария конца в конец данных, построенных на HDInsight Hadoop кластера toobuild и развертывания модели с помощью большого набора данных общедоступным (1 ТБ)"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 72d958c4-3205-49b9-ad82-47998d400d2b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 59b2af02e7840cb60a4b5b2f2c8ab0611df198ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a>Hello командного процесса обработки и анализа данных в действие — с помощью кластера Azure HDInsight Hadoop для набора данных 1 ТБ

В этом пошаговом руководстве показано использование hello командного процесса обработки и анализа данных в сценарии с начала до конца [кластера Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, изучение, инженер компонентов и публично вниз образец данных из одного hello Доступные [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) наборов данных. Мы используем машинного обучения Azure toobuild модель двоичной классификации на основе этих данных. Также мы покажем, как toopublish одну из этих моделей как веб-службы.

Это также возможно toouse задачи hello tooaccomplish ноутбук IPython, представленных в данном пошаговом руководстве. Пользователей, которые бы как tootry, такой подход следует обратиться к hello [Criteo Пошаговое руководство по использованию соединений Hive ODBC](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) раздела.

## <a name="dataset"></a>Описание набора данных Criteo
Hello Criteo данных является прогноз щелкните набор данных, составляет приблизительно 370 gzip сжатых файлов TSV (~1.3TB несжатых данных), составляющие 4.3 миллиард записей. Эти данные получены на основе данных о переходах по ссылкам за 24 дня, предоставленных [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/). Для удобства hello специалистами по анализу данных мы распаковал tooexperiment toous доступных данных с.

Каждая запись в этом наборе данных содержит 40 столбцов:

* Hello первый столбец является столбцом метки, указывающее, является ли пользователь щелкает **добавить** (значение 1) или не см (значение 0)
* следующие 13 столбцов являются числовыми;
* последние 26 столбцов категориальные.

Hello столбцы являются анонимны и использовать ряд перечисленные имена: «Col1» (для столбца меток hello) слишком "Col40» (для последнего столбца категорий hello).            

Ниже приведен фрагмент hello сначала 20 столбцы двух наблюдения (строк) из этого набора данных.

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

Отсутствуют некоторые значения в обоих столбцах числовых и категориальные hello в этом наборе данных. Чтобы описать простой метод для обработки недостающих значений hello. Дополнительные сведения о данных hello изучаются при их хранения в таблицах Hive.

**Определение:** *скорость с дополнительной информацией (CTR):* это процент hello щелчков мыши hello данных. В этом наборе Criteo данных hello CTR — около % 3.3 или 0.033.

## <a name="mltasks"></a>Примеры задач прогнозирования
В этом пошаговом руководстве рассмотрены два примера задач по прогнозированию:

1. **Двоичная классификация**— прогнозирует, щелкнет ли пользователь рекламное объявление:
   
   * класс 0 — не щелкнул;
   * класс 1 — щелкнул.
2. **Регрессия**: прогнозирует вероятность hello и нажмите кнопку ad из признаки пользователя.

## <a name="setup"></a>Настройка кластера HDInsight Hadoop для обработки и анализа данных
**Примечание.** Эту задачу обычно выполняет **администратор**.

Настройте среду обработки и анализа данных Azure, чтобы создавать решения для прогнозной аналитики с помощью кластеров HDInsight, выполнив три шага:

1. [Создать учетную запись хранилища](../storage/common/storage-create-storage-account.md): этой учетной записи хранения — используется toostore данные в хранилище больших двоичных объектов Azure. Здесь хранятся данные Hello, используемые в кластерах HDInsight.
2. [Настройка кластеров Azure HDInsight Hadoop для обработки и анализа данных.](machine-learning-data-science-customize-hadoop-cluster.md) На этом шаге создается кластер Azure HDInsight Hadoop и на всех узлах устанавливается 64-разрядный дистрибутив Anaconda Python 2.7. При настройке кластера HDInsight hello существуют два toocomplete важные действия (как описано в этом разделе).
   
   * Необходимо связать учетную запись хранения hello, созданной на шаге 1 с кластером HDInsight, при его создании. Эта учетная запись используется для доступа к данным, которое может быть обработано в кластере hello.
   * Необходимо включить удаленный доступ toohello головного узла кластера hello после его создания. Запоминать учетные данные удаленного доступа hello, указанные здесь (отличающиеся от параметров, указанных для hello кластера при его создании): при необходимости toocomplete hello следующие процедуры.
3. [Создайте рабочую область машинного Обучения Azure](machine-learning-create-workspace.md): рабочая область машинного обучения этот Azure используется для построения моделей машинного обучения, после просмотра исходных данных, а также работу выборки в кластере HDInsight hello.

## <a name="getdata"></a>Получение и использование данных из общедоступного источника
Hello [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) набор данных может осуществляться, щелкнув ссылку hello, принимая hello условия использования и предоставления имени. Ниже показан снимок того, как это выглядит.

![Принятие условий использования Criteo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

Нажмите кнопку **tooDownload Продолжить** tooread Дополнительные сведения о hello набора данных и его доступности.

Hello данные находятся в открытом [хранилище больших двоичных объектов](../storage/blobs/storage-dotnet-how-to-use-blobs.md) расположение: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/. Hello «wasb» ссылается tooAzure место хранения большого двоичного объекта. 

1. Hello данные в это хранилище BLOB-объект открытого состоит из трех во вложенных данных в распакованную.
   
   1. Здравствуйте, вложенная папка *необработанные и числа объектов/* содержит hello первый 21 день данных — от дня\_00 tooday\_20
   2. Здравствуйте, вложенная папка *raw/Обучение/* состоит из одного дня данных, день\_21
   3. Здравствуйте, вложенная папка *необработанные и тестирования или* состоит из двух дней данных, день\_22 и день\_23
2. Для теми, кто toostart с hello gzip необработанных данных, они также доступны в главную папку hello *raw /* как day_NN.gz, где NN находятся значения от 00 too23.

Альтернативный подход tooaccess, просматривайте и модели данных, которые не требуются все локальные файлы для загрузки описан далее в этом пошаговом руководстве при создании таблицы Hive.

## <a name="login"></a>Войдите в головному узлу кластера toohello
toolog в toohello головному узлу кластера hello, используйте hello [портал Azure](https://ms.portal.azure.com) toolocate hello кластера. Щелкните значок elephant HDInsight hello hello слева, а затем дважды щелкните имя кластера hello. Перейдите toohello **конфигурации** вкладку, дважды щелкните значок CONNECT hello hello нижней части страницы hello и введите свои учетные данные удаленного доступа при появлении запроса. Это занимает toohello головному узлу кластера hello.

Ниже приведен типичный первый вход головному узлу кластера toohello выглядит как:

![Войдите в toocluster](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

В левой части экрана приветствия мы видим hello «Hadoop Command Line», которая является нашей workhorse для просмотра данных hello. На экране также отображаются два полезных URL-адреса — «Состояние Hadoop Yarn» и «Узел имен Hadoop». URL-адрес состояния yarn Hello показывает ход выполнения задания и URL-адрес узла hello имя подробные сведения о конфигурации кластера hello.

Теперь мы настроены и готовы toobegin первой части пошагового руководства hello: Просмотр данных с помощью Hive и Подготовка данных для машинного обучения Azure.

## <a name="hive-db-tables"></a> Создание базы данных и таблиц Hive
таблицы toocreate Hive для наших Criteo dataset, откройте hello ***командной строки Hadoop*** hello desktop hello головного узла, а также введите hello Hive каталог, введя команду hello

    cd %hive_home%\bin

> [!NOTE]
> Выполнить все команды Hive в этом пошаговом руководстве из ячейки Hive hello / directory строки. Таким образом вы сможете автоматически избежать любых проблем с путем. Мы используем условия hello «Hive каталога prompt», «Hive bin / подсказки директории» и «командной строки Hadoop» попеременно.
> 
> [!NOTE]
> tooexecute любого запроса Hive можно всегда использовать hello, следующие команды:
> 
> 

        cd %hive_home%\bin
        hive

После hello Hive REPL отображается с «hive > "войти, просто Вырезать и вставить запрос tooexecute hello его.

Hello следующий код создает базу данных «criteo» и затем создает 4 таблиц:

* *таблицы для создания счетчиков* лежит дней день\_00 tooday\_20,
* *как hello обучающего набора данных на таблицу для использования* лежит день\_21, и
* два *таблицы для использования в качестве hello проверочных наборов данных* лежит день\_22 и день\_23 соответственно.

Мы разбить нашей проверочный набор данных двух различных таблиц, так как один из дней hello является выходным днем, и мы стремимся toodetermine Если hello модели можно определить различия между праздников и не праздничных от частоты hello с дополнительной информацией.

Здравствуйте, сценарий [образец &#95; hive &#95; Создание &#95; criteo &#95; базы данных &#95; и &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) будет отображена здесь для удобства:

    CREATE DATABASE IF NOT EXISTS criteo;
    DROP TABLE IF EXISTS criteo.criteo_count;
    CREATE TABLE criteo.criteo_count (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/count';

    DROP TABLE IF EXISTS criteo.criteo_train;
    CREATE TABLE criteo.criteo_train (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/train';

    DROP TABLE IF EXISTS criteo.criteo_test_day_22;
    CREATE TABLE criteo.criteo_test_day_22 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_22';

    DROP TABLE IF EXISTS criteo.criteo_test_day_23;
    CREATE TABLE criteo.criteo_test_day_23 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_23';

Мы Обратите внимание, что эти таблицы внешнего как мы просто tooAzure точка расположения хранилища больших двоичных объектов (wasb).

**Существует два способа tooexecute ANY Hive запрос, который теперь упоминается.**

1. **С помощью Hive REPL командной строки "hello"**: hello сначала является tooissue команда «hive» и скопируйте и вставьте запрос в hello Hive REPL командной строки. toodo этой, выполните:
   
        cd %hive_home%\bin
        hive
   
     Теперь в hello REPL командной строки, вырезание и вставка запроса hello выполняет его.
2. **Сохранение запросов tooa файла и выполнении команды hello**: hello, второй — toosave hello запросы tooa .hql файла ([образец &#95; hive &#95; Создание &#95; criteo &#95; базы данных &#95; и &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) и затем проблема hello следующая команда tooexecute hello запроса:
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a>Подтверждение создания базы данных и таблицы
Далее мы подтвердить создание hello hello базы данных с hello следующую команду из ячейки Hive hello / directory строки:

        hive -e "show databases;"

Результат выполнения команды:

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

Это подтверждает Создание hello hello новую базу данных, «criteo».

toosee какие таблицы мы создали, мы просто выполните команду hello здесь из ячейки Hive hello / directory строки:

        hive -e "show tables in criteo;"

Затем мы видим hello следующие выходные данные:

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <a name="exploration"></a> Просмотр данных в Hive
Теперь мы готовы toodo просмотра некоторых основных данных в кусте. Мы начните с инвентаризации hello количество примеров в hello обучение и таблицы данных теста.

### <a name="number-of-train-examples"></a>Количество примеров для обучения
Здравствуйте, содержимое [образец &#95; hive &#95; число &#95; обучение &#95; таблицы &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) показано ниже:

        SELECT COUNT(*) FROM criteo.criteo_train;

Мы получаем такой результат:

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

Кроме того, один также может выдать следующую команду из ячейки Hive hello hello / directory строки:

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-hello-two-test-datasets"></a>Количество примеров теста в наборах данных hello два теста
Теперь мы счетчик hello количество примеров в hello двух наборов данных теста. Здравствуйте, содержимое [образец & #95 hive & #95 счетчик &#95; criteo &#95; тестовые &#95; & #95 день; 22 &#95; #95;examples.hql & таблицы](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) рассматриваются следующие вопросы:

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

Мы получаем такой результат:

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

Как обычно, мы также может выполнять вызов сценария hello из ячейки Hive hello / directory приглашения, выполнив команду hello:

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

Наконец, мы изучаем hello количество примеров теста в проверочном наборе данных hello, в зависимости от дня\_23.

Hello команда toodo это аналогичный toohello просто показанной (см. слишком[образец &#95; hive &#95; число &#95; criteo &#95; тестовые &#95; день &#95; 23 &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

Результат выполнения команды:

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-hello-train-dataset"></a>Метка распространения в наборе данных обучение hello
Hello распространения метки в наборе данных обучение hello представляет интерес. toosee это, мы Показать содержимое [образец &#95; hive &#95; criteo &#95; метка &#95; распространения &#95; обучение &#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

Это дает hello метки распространения:

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

Обратите внимание, что процент hello положительное метки около 3.3% (согласуется с hello исходный набор данных).

### <a name="histogram-distributions-of-some-numeric-variables-in-hello-train-dataset"></a>Набор данных обучения Гистограмма распределения некоторых числовых переменных в hello
Можно использовать собственный куста «гистограммы\_числовых» функции toofind out какие hello распределение числовых переменных hello выглядит следующим образом. Вот содержимое hello [образец &#95; hive &#95; criteo &#95; гистограммы &#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

Это дает ниже hello:

        26      155878415
        2606    92753
        6755    22086
        11202   6922
        14432   4163
        17815   2488
        21072   1901
        24113   1283
        27429   1225
        30818   906
        34512   723
        38026   387
        41007   290
        43417   312
        45797   571
        49819   428
        53505   328
        56853   527
        61004   160
        65510   3446
        Time taken: 317.851 seconds, Fetched: 20 row(s)

ПРЕДСТАВЛЕНИЕ — БОКОВОЕ Hello разрезать сочетание в куст служит tooproduce SQL-подобного выходные данные вместо обычного списка hello. Обратите внимание, что в hello этой таблицы, первый столбец hello соответствует toohello bin center и hello второй toohello bin частоты.

### <a name="approximate-percentiles-of-some-numeric-variables-in-hello-train-dataset"></a>Приблизительное процентилем некоторых числовых переменных в hello обучения набора данных
Также интереса с числовых переменных, вычисление приблизительное процентилем hello. Функция Hive percentile\_approx делает это автоматически. Здравствуйте, содержимое [образец &#95; hive &#95; criteo &#95; приблизительное &#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) являются:

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

Мы получаем такой результат:

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

Мы оператор комментария hello распределение процентилем обычно является тесно связанных toohello гистограммы распространения любой числовой переменной.         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-hello-train-dataset"></a>Найти количество уникальных значений для некоторых категориальных столбцов в наборе данных обучение hello
Продолжить просмотр данных hello, мы теперь доступны, для некоторых категориальных столбцов hello количество уникальных значений, которые они принимают. toodo это, мы Показать содержимое [образец &#95; hive &#95; criteo &#95; уникальный &#95; значения &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

Мы получаем такой результат:

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

Обратите внимание, что в столбце Col15 найдено 19 млн. уникальных значений! С помощью упрощенного такие методы, как «горячая один кодировка» tooencode таких многомерными категориальных переменных невозможна. Для эффективного решения этой проблемы объясняется и демонстрируется эффективный и надежный метод, называемый [обучение с использованием счетчиков](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx).

Этот подраздел мы последний, просмотрев hello количество уникальных значений для некоторых других категориальных столбцов также. Здравствуйте, содержимое [образец &#95; hive &#95; criteo &#95; уникальный &#95; значения &#95; несколько &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) являются:

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

Мы получаем такой результат:

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

Опять же мы видим, за исключением Col20, все hello другие столбцы имеют много уникальных значений.

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-hello-train-dataset"></a>Количество вхождений сопутствующего пар категориальных переменных в наборе данных обучение hello

количество вхождений сопутствующего Hello пары категориальные переменные также представляет интерес. Это может быть определено с помощью кода hello в [образец &#95; hive &#95; criteo &#95; парной &#95; категориальные &#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

Мы обратном hello числа заказов по их вхождения и в этом случае просмотрите hello top 15. Результат выполнения команды:

        ad98e872        cea68cd3        8964458
        ad98e872        3dbb483e        8444762
        ad98e872        43ced263        3082503
        ad98e872        420acc05        2694489
        ad98e872        ac4c5591        2559535
        ad98e872        fb1e95da        2227216
        ad98e872        8af1edc8        1794955
        ad98e872        e56937ee        1643550
        ad98e872        d1fade1c        1348719
        ad98e872        977b4431        1115528
        e5f3fd8d        a15d1051        959252
        ad98e872        dd86c04a        872975
        349b3fec        a52ef97d        821062
        e5f3fd8d        a0aaffa6        792250
        265366bf        6f5c7c41        782142
        Time taken: 560.22 seconds, Fetched: 15 row(s)

## <a name="downsample"></a>Вниз hello образцы наборов данных для машинного обучения Azure
При необходимости изучать hello наборы данных и показано, как может сделать этот тип для просмотра всех переменных (включая комбинаций), мы теперь вниз образцы наборов данных hello, что мы можно создавать модели в машинном обучении Azure. Помните, мы сосредоточим внимание на проблему hello является: при заданном наборе образцы атрибутов (значения компонента из Col2 - Col40), мы прогнозировать, является ли Col1 0 (нет щелкните) или 1 (щелкните).

toodown образца нашей обучения и тестирования, наборов данных too1% от исходного размера hello, мы используем куста собственной функции RAND(). Здравствуйте следующему сценарию [образец &#95; hive &#95; criteo &#95; понижение разрешения &#95; обучение &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) делает это для набора данных для обучения hello:

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

Мы получаем такой результат:

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

Здравствуйте, сценарий [образец &#95; hive &#95; criteo &#95; понижение разрешения &#95; тестовые &#95; & #95 день; 22 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) делает это для проверочных данных, день\_22:

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

Мы получаем такой результат:

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


Наконец, hello скрипт [образец &#95; hive &#95; criteo &#95; понижение разрешения &#95; тестовые &#95; & #95 день; 23 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) делает это для проверочных данных, день\_23:

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

Мы получаем такой результат:

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

Таким образом, мы будут готовы toouse наш список выборки обучения и проверочных наборов данных для построения моделей в машинном обучении Azure.

Прежде чем мы перейдем tooAzure машинного обучения, являющийся таблицы счетчиков hello проблемы нет окончательного важным компонентом. В следующем разделе вложенных hello мы обсудим это некоторые сведения.

## <a name="count"></a>Краткое описание для таблицы счетчиков hello
Как было видно, несколько категориальных переменных обладают очень высокой размерностью. В нашем пошаговом руководстве рассматриваются мощный метод, называемый [обучения с подсчитывает](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode эти переменные эффективным и надежным способом. Дополнительные сведения об этом приеме — hello ссылке.

[!NOTE]
>В этом пошаговом руководстве мы связана с использованием число таблиц tooproduce compact представления многомерными категориальных признаков. Это не hello единственным способом tooencode категориальных признаков; Дополнительные сведения о других возможностях интерес пользователи могут извлекать [один горячей encoding](http://en.wikipedia.org/wiki/One-hot) и [хэширование признаков](http://en.wikipedia.org/wiki/Feature_hashing).
>

таблицы счетчиков toobuild hello количество данных, мы используем данные hello в hello raw или число папок. В hello моделирования разделе, демонстрируется пользователей как toobuild они подсчитывают таблицы для категориальных признаков с нуля, или в качестве альтернативы toouse таблицу готовые счетчиков для их изучения. В том, что следующим образом, когда мы ссылаемся слишком «готовые таблицы счетчиков», имеется в виду с помощью таблиц счетчиков hello, мы предоставляем. Подробные инструкции по как tooaccess эти таблицы приведены в следующем разделе hello.

## <a name="aml"></a> Создание моделей с помощью Машинного обучения Azure
Процесс создания моделей в Машинном обучении Azure состоит из следующих шагов:

1. [Получать данные hello из таблицы Hive в машинном обучении Azure](#step1)
2. [Создайте эксперимент hello: очистка данных hello и создания признаков с помощью таблиц счетчиков](#step2)
3. [Сборки, обучение и hello оценка модели](#step3)
4. [Hello модель оценки](#step4)
5. [Опубликовать как веб служба модели hello](#step5)

Теперь мы все готово toobuild моделей в студии машинного обучения Azure. Наши вниз выборки данных сохраняется как таблицы Hive в кластере hello. Мы используем hello машинного обучения Azure **импорта данных** модуль tooread эти данные. Учетная запись хранения Hello учетные данные с tooaccess hello этого кластера приведены в какие следующим образом.

### <a name="step1"></a>Шаг 1: Получение данных из таблицы Hive в машинном обучении Azure с помощью модуля hello импорта данных и выбрать его для эксперимента машинного обучения
Для начала выберите **+Создать** -> **Эксперимент** -> **Пустой эксперимент**. Затем из hello **поиска** поле на hello вверху слева, поиск «Импорт данных». Перетаскивание hello **импорта данных** модуль toohello эксперимента canvas (hello средней части экрана приветствия) toouse hello модуля для доступа к данным.

Это связано с какой hello **импорта данных** выглядит как при получении данных из таблицы Hive hello:

![Модуль "Импорт данных" получает данные](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

Для hello **импорта данных** tooprovide требуется модуль hello значения параметров "hello", предоставляемые в hello график — это только примеры hello сортировку значений. Ниже приведены некоторые общие рекомендации по установке toofill hello параметр out для hello **импорта данных** модуля.

1. В поле **Источник данных**
2. В hello **запроса базы данных Hive** поле простой запрос SELECT * FROM < ваш\_базы данных\_name.your\_таблицы\_имя >-достаточно.
3. **URI сервера Hcatalog** — если используется кластер abc, введите адрес https://abc.azurehdinsight.net.
4. **Имя учетной записи пользователя Hadoop**: hello имени пользователя, выбранного во время hello commissioning hello кластера. (Не hello именем пользователя удаленного доступа!)
5. **Пароль учетной записи пользователя Hadoop**: hello пароль для имени пользователя hello, выбранного во время hello commissioning hello кластера. (Не hello пароля для удаленного доступа!)
6. **Расположение выходных данных**: выберите Azure.
7. **Имя учетной записи хранилища Azure**: hello учетной записи хранилища, связанного с кластером hello
8. **Ключ учетной записи хранилища Azure**: hello ключ учетной записи хранилища hello, связанной с кластером hello.
9. **Имя контейнера Azure**: Если имя кластера hello «abc», то обычно это просто «abc»,.

Здравствуйте, один раз **импорта данных** окончания получения данных (отображается зеленый hello делений на hello модуля), сохранить эти данные как набор данных (с именем по своему усмотрению). Это выглядит так:

![Модуль "Импорт данных" сохраняет данные](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

Щелкните правой кнопкой мыши hello выходной порт hello **импорта данных** модуля. Отобразятся параметры **Сохранение набора данных** и **Визуализировать**. Hello **визуализировать** параметр, если выбран вариант, отображает 100 строк данных hello, вместе с правой панели, который удобен для некоторых сводные статистические данные. toosave данных, просто выберите **Сохранить как набор данных** и следуйте инструкциям.

dataset tooselect hello сохранен для использования в образовательных эксперименте машины, найдите hello наборов данных при помощи hello **поиска** поле показано hello следующий рисунок. Затем просто ввести имя hello Вы дали hello dataset частично tooaccess его и перетащите hello набора данных в hello главной панели. На место hello главной панели выбирает для использования в моделировании машины обучения.

![Набор данных сводной на главной панели hello](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> Сделайте это для обучения hello и наборы данных теста hello. Кроме того помните, имя базы данных toouse hello и имена таблиц, которые вы присвоили для этой цели. Hello значения, используемые на рисунке hello предназначены исключительно для иллюстрации purposes.* *
> 
> 

### <a name="step2"></a>Шаг 2: Создание простого эксперимента машинного обучения Azure движениями toopredict и не щелкает
Наш эксперимент Машинного обучения Azure выглядит следующим образом:

![Эксперимент машинного обучения](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

Рассматриваются основные компоненты этого эксперимента hello. Напоминаем нам нужна toodrag наши сохраненные обучения и проверочных наборов данных на холст эксперимента tooour сначала.

#### <a name="clean-missing-data"></a>Очистка недостающих данных
Hello **Очистка недостающих данных** модуль делает его названия: он удаляет отсутствующие данные таким образом, может задаваться пользователем. Если посмотреть на модуль, мы увидим следующее:

![Очистка недостающих данных](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

Здесь мы выбрали tooreplace все отсутствующие значения с 0. Существуют другие параметры, в том, которые можно увидеть, просмотрев hello раскрывающихся списков в модуле hello.

#### <a name="feature-engineering-on-hello-data"></a>Конструируются hello данных
Некоторые категориальные функции крупных наборов данных могут иметь миллионы уникальных значений. Использовать для представления таких многомерных функций упрощенные методы, например метод "прямого кодирования", нецелесообразно. В этом пошаговом руководстве показано, как toouse число компонентов, с помощью встроенных toogenerate модули машинного обучения Azure compact представления этих многомерными категориальные переменные. Hello конечным результатом является меньший размер модели, сократить время обучения и метрики производительности, которые довольно сопоставимых toousing других методов.

##### <a name="building-counting-transforms"></a>Построение преобразований счетчиков
toobuild число функций, мы используем hello **построения подсчета преобразования** модуль, который доступен в машинном обучении Azure. модуль Hello выглядит следующим образом:

![Модуль построения преобразования счетчика](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Модуль построения преобразования счетчика](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)

> [!IMPORTANT] 
> В hello **число столбцов** , мы введите в поле желаем tooperform учитывается на столбцы. Обычно это (как уже говорилось) — многомерные категориальные столбцы. Во время запуска hello, мы уже упоминали Criteo hello набор данных имеет 26 категориальных столбцов: из Col15 tooCol40. Здесь мы подсчета на всех из них и предоставлять их индексы (из 15 too40, разделенных запятыми, как показано).
> 

модуль toouse hello в Здравствуйте MapReduce режиме (подходит для больших наборов данных), мы должны получить доступ к кластера HDInsight Hadoop tooan (одно для исследования компонент может быть повторно использован для этой цели также приветствия) и его учетные данные. Hello предыдущих рисунках показаны hello заполняться значениями выглядеть следующим образом (Замените hello значений, заданных для сочетается с другими, соответствующими для собственных варианта использования).

![Параметры модуля](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

В hello выше рисунке показано, как tooenter hello входного BLOB-объект расположения. Это расположение содержит данные hello, выделенная для создания таблиц счетчиков.

После завершения этого модуля, мы сможем Сохранить преобразование hello для более поздней версии, щелкните правой кнопкой мыши модуль hello и выбрав hello **сохранение преобразования** параметр:

![Параметр Save as Transform (Сохранить как преобразование)](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

В нашей архитектуры эксперимента, показанном выше hello dataset «ytransform2» соответствует точно tooa Сохранить преобразование count. Hello оставшейся части этого эксперимента, предполагается, что используемое чтения hello **построения подсчета преобразования** модуля на некоторые счетчики toogenerate данных и затем может использовать эти функции count toogenerate счетчиков hello обучения и проверочных наборов данных.

##### <a name="choosing-what-count-features-tooinclude-as-part-of-hello-train-and-test-datasets"></a>Выбор, что подсчет tooinclude функции как часть обучения hello и проверочных наборов данных
После получения счетчик преобразования готовности hello пользователь может выбрать какие функции tooinclude в их поезда и проверочных наборов данных с помощью hello **изменить параметры таблицы счетчик** модуля. Этот модуль показан для полноты информации, но в целях упрощения в данном эксперименте он фактически не используется.

![Modify Count Table Parameters (Изменение параметров таблицы счетчиков)](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

Таким образом как можно увидеть, мы выбрали toouse вероятность журнала просто hello и tooignore hello пассивный режим столбца. Мы также можно настроить параметры, например пороговое значение контейнера для сборки мусора hello, сколько tooadd псевдослучайных предыдущие примеры для сглаживания, и ли toouse любой Лапласа помех или нет. Все эти — это дополнительные возможности и что toobe целый значения по умолчанию hello хорошей отправной точкой для пользователей, имеющих возможность создания нового типа toothis.

##### <a name="data-transformation-before-generating-hello-count-features"></a>Преобразование данных перед созданием функции count hello
Теперь мы сосредоточить внимание на важное правило о преобразовании нашей обучение и проверить данные предыдущих tooactually создания функции count. Обратите внимание, что два **выполнение скрипта R** модули, используемые, прежде чем мы применить преобразование tooour hello количество данных.

![Модули "Выполнить сценарий R"](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

Вот первый сценарий R hello.

![Первый сценарий R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

В этом сценарии R переименуем нашей toonames столбцы «Col1» слишком «Col40». Это так, как преобразование числа hello ожидает имена этого формата.

В hello второй скрипт R, мы распределить hello распространения между классами положительные и отрицательные (классы 1 и 0 соответственно) с отрицательным класса понижение hello. Hello R сценарии здесь показано, как toodo это:

![Второй сценарий R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

В этой простой сценарий R, мы используем «pos\_neg\_отношение» tooset hello объем баланс между hello положительные и отрицательные классы hello. Это важно, что toodo, поскольку улучшение дисбаланс класс обычно дает преимущества в производительности для проблем классификации, где распространения класс hello синхронизована (Напомним, что в нашем случае у нас есть положительные и отрицательные класса 96.7% 3.3%).

##### <a name="applying-hello-count-transformation-on-our-data"></a>Применение преобразования числа hello с нашими данными
Наконец, мы используем hello **применение преобразования** tooapply модуль hello число преобразований на нашем обучения и проверочных наборов данных. Этот модуль принимает преобразования числа hello сохранен как один вход и hello обучения или тестирования наборы данных, как hello другие входные данные и возвращает данные с помощью функции count. Вот как это работает:

![Модуль применения преобразования](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-hello-count-features-look-like"></a>Фрагмент кода как выглядеть функции count hello
Бывает полезным toosee, какие функции count hello выглядеть в нашем случае. Вот его фрагмент:

![Функции счетчика](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

В данном отрывке Далее показано, что для hello столбцов, которые мы подсчитаны, мы получить количество hello вход шансов соответствующие backoffs tooany сложения.

Мы стали готовы toobuild модель машинного обучения Azure, используя эти преобразованный наборы данных. В следующем разделе hello показано, как это сделать.

### <a name="step3"></a>Шаг 3: Построение, обучения и оценка модели hello

#### <a name="choice-of-learner"></a>Выбор ученика
Во-первых мы должны toochoose ученика. Как наш ученик не будет toouse два класса повышенного дерева принятия решений. Ниже приведены параметры по умолчанию hello для этого ученика.

![Параметры двухклассового увеличивающегося дерева принятия решений](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

В нашем эксперименте не значения по умолчанию hello toochoose постоянной. Мы Обратите внимание, что значения по умолчанию, hello, являются обычно значимые и удобным способом tooget быстрого базовых показателей производительности. На производительность можно повысить, широкими параметры при выборе tooonce вами базового плана.

#### <a name="train-hello-model"></a>Обучение модели hello
Для обучения мы просто вызовем модуль **Обучение модели** . два входных данных tooit Hello: hello ученик Двухклассового повышенного дерева принятия решений и наши обучающего набора данных. Вот как это работает:

![Модуль "Обучение модели"](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-hello-model"></a>Модель оценки hello
После обучения модели, мы готовы tooscore на hello проверки набора данных и tooevaluate его производительности. Это делается с помощью hello **модель оценки** показано hello следующий рисунок, вместе с модулем **модель оценки** модуля:

![Модуль "Оценка модели"](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <a name="step4"></a>Шаг 4: Оценка модели hello
Наконец мы хотели бы tooanalyze модели производительности. Как правило для проблем классификации (двоичный) двух классов, хорошей мерой — hello AUC. toovisualize это, мы подключить hello **модель оценки** tooan модуль **модель оценки** модуля для этого. Щелкнув **визуализировать** на hello **модель оценки** модуль создает график как hello, выполнив одно:

![Модуль «Анализ модели» и «Увеличивающееся дерево принятия решений»](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

В двоичный файл (или два класса) проблем классификации, хорошо степень точности прогнозов является hello области под кривой (AUC). Ниже будут показаны результаты использования этой модели на основе нашего тестового набора данных. tooget это, щелкните правой кнопкой мыши порт вывода hello hello **модель оценки** модуля и затем **визуализировать**.

![Визуализация модуля «Анализ модели»](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <a name="step5"></a>Шаг 5: Публикация hello модели веб-службы
возможность Hello toopublish модель машинного обучения Azure как веб-службы с минимальными усилиями ценные функция для создания широко доступны. После этого, любой пользователь может создать вызовы toohello веб-службы с входными данными, они должны прогнозы для, что hello веб-служба использует модель tooreturn hello этих прогнозов.

toodo это, мы сначала сохраните нашей обученной модели в виде обученной модели объекта. Это можно сделать, щелкнув правой кнопкой мыши hello **Обучение модели** модуль и с помощью hello **Сохранить как Обученную модель** параметр.

Теперь нам нужны toocreate ввод и вывод портов для веб-узле службы:

* порта ввода принимает данные в hello же форму как hello данные, необходимые для прогнозы
* порт вывода возвращает связанные hello вероятности и метки оцененных hello.

#### <a name="select-a-few-rows-of-data-for-hello-input-port"></a>Выберите несколько строк данных для входного порта hello
Это удобный toouse **применение преобразования SQL** tooserve модуль tooselect только 10 строк, как hello входные данные порт. Выберите только этих строк данных для наших входного порта с помощью запроса SQL hello, показано ниже:

![Данные порта ввода](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a>Веб-служба
Теперь мы готовы toorun небольшой эксперимент, который можно использовать toopublish веб-узле службы.

#### <a name="generate-input-data-for-webservice"></a>Создание входных данных для веб-службы
В качестве шага нулевого поскольку таблицы счетчиков hello велик, мы занять всего несколько строк данных теста и создавать выходные данные из них с помощью функции count. Это может служить форматом hello входные данные для наших веб-службы. Вот как это работает:

![Создание входных данных модуля «Увеличивающееся дерево принятия решений»](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> Формат входных данных hello, теперь мы используем hello выходные данные hello **Характеризатора** модуля. После завершения это поэкспериментировать, сохранить выходные данные hello из hello **Характеризатора** модуль в качестве набора данных. Этот набор данных будет использоваться для hello входных данных в hello webservice.
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a>Оценка эксперимента для публикации веб-службы
Сначала мы покажем, как это выглядит. Структура essential Hello **модель оценки** модуля, который принимает объект нашей обученной модели и несколько строк входных данных, мы создали на предыдущих шагах hello, с помощью hello **Характеризатора** модуля. Мы используем tooproject «Выберите столбцы в наборе данных» hello Оцененный метки и Оценка вероятности hello.

![Выбор столбцов в наборе данных](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

Обратите внимание, каким образом hello **Выбор столбцов в наборе данных** модуль можно использовать для «фильтрации» данные из набора данных. Мы Показать содержимое hello здесь:

![Фильтрация с помощью hello Выбор столбцов в модуле набора данных](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

порты tooget hello синий входных и выходных данных, нужно просто щелкнуть **Подготовка веб-службы** внизу hello справа. Запуск этого эксперимента также позволяет нам toopublish hello веб-службы: щелкните hello **публикации веб-службы** значок hello нижней правой, показанный здесь:

![Publish web service](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

После публикации веб-службы hello мы получаем перенаправленный tooa страницу, которая выглядит таким образом:

![Панель мониторинга веб-службы](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

В левой части hello видно две ссылки для веб-службы:

* Hello **запрос-ОТВЕТ** службы (или записи Ресурсов) предназначена для единичные прогнозы и будет использовать в этом цеху.
* Hello **ПАКЕТНОЕ выполнение** службы (BES) используется для пакетных прогнозов и требует наличия, прогнозы toomake hello входные данные находились в хранилище больших двоичных объектов Azure.

Щелкнув ссылку hello **запрос-ОТВЕТ** отсылает tooa страницы, которая дает нам предустановленных кода на C#, python и R. Этот код можно использовать для создания веб-службы toohello вызовы удобным образом. Обратите внимание, что hello ключ API на этой странице требуется toobe, используемый для проверки подлинности.

Это удобный toocopy этот python code через tooa новую ячейку в записной книжке IPython hello.

Здесь показано сегмент кода python, с hello правильный ключ API.

![Код Python](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

Обратите внимание, что мы заменены ключ API по умолчанию hello ключ API наш веб-службы. Щелкнув **запуска** в данную ячейку в IPython записной книжки дает hello следующий ответ:

![Ответ iPython](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

Мы видим, что для hello двух тестовых примеры, которые мы спросили (в framework JSON hello hello сценария python), мы получаем ответы в форме hello «Оцененный метки, Оцененный вероятности». Обратите внимание, что в этом случае мы выбрали значения по умолчанию hello предустановленных кода hello предоставляет (0 для всех числовых столбцов и строку hello «значение» для всех категориальных столбцов).

Это заключительный шаг нашей отображение Пошаговое руководство с начала до конца как toohandle крупномасштабных набора данных, с помощью машинного обучения Azure. Мы начали с терабайт данных, создается модель прогнозирования и развернуть его как веб-службы в облаке hello.

