---
title: "aaaExplore данные в Hadoop кластера и создания моделей в машинном обучении Azure | Документы Microsoft"
description: "С помощью hello процесс обработки и анализа данных для команды сценария конца в конец данных, построенных на HDInsight Hadoop кластера toobuild и развертывания модели с помощью общедоступных набора данных."
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e9e76c91-d0f6-483d-bae7-2d3157b86aa0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: a371032e356ffc366af0d6fbe364af281b6efd19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a>Hello командного процесса обработки и анализа данных в действии: использование Azure HDInsight Hadoop кластеров
В этом пошаговом руководстве мы используем hello [процесса обработки и анализа данных Team (TDSP)](data-science-process-overview.md) -сквозной сценарий, используя [кластера Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, исследовать и публично компонентов инженер данные из hello Доступные [NYC такси приема-передачи](http://www.andresmh.com/nyctaxitrips/) набора данных и toodown образец hello данных. Модели данных hello создаются с помощью машинного обучения Azure toohandle двоичными и мультиклассовой классификации и регрессии задач прогнозирования.

Пошаговое руководство показывает, как toohandle большего набора данных (1 ТБ), аналогичный сценарий с помощью HDInsight Hadoop кластеры для обработки данных см. в разделе [процесс обработки и анализа данных для команды - с помощью Azure HDInsight Hadoop кластеров на набор данных 1 ТБ](machine-learning-data-science-process-hive-criteo-walkthrough.md).

Это также возможно toouse hello tooaccomplish ноутбук IPython задач представленному hello Пошаговое руководство по использованию набора данных hello 1 ТБ. Пользователей, которые бы как tootry, такой подход следует обратиться к hello [Criteo Пошаговое руководство по использованию соединений Hive ODBC](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) раздела.

## <a name="dataset"></a>Описание набора данных «Поездки такси Нью-Йорка»
Hello Trip такси NYC данных составляет около 20 ГБ файлы сжатых значений с разделителями запятыми (CSV) (~ 48 ГБ несжатого), включающего в себя более миллиона 173 отдельных приема-передачи и hello цен платная для каждого маршрута. Каждая запись маршрута включает hello раскладки и истощение место и время, анонимные hack (драйвер) номер лицензии и medallion (уникальный идентификатор элемента такси) номер. данные Hello охватывает все приема-передачи в 2013 году, hello и предоставляется в следующих двух наборов данных для каждого месяца hello:

1. Hello «trip_data» CSV-файлы содержат обработки таких сведений, как количество пассажиров, раскладки и dropoff точек, длительность обработки и длина пути. Вот несколько примеров записей:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. CSV-файлы «trip_fare» Hello содержат подробные сведения о тариф авиакомпании hello платная для каждого маршрута, например тип платежа, сумма тариф авиакомпании, излишнюю нагрузку налоги, советы и тарифы и hello общей оплаты. Вот несколько примеров записей:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Hello trip уникальных ключей toojoin\_данных и обработки\_тариф авиакомпании состоит из полей hello: medallion hack\_лицензии и раскладки\_даты и времени.

tooget все hello сведения о соответствующих tooa конкретного маршрута, он является достаточно toojoin с тремя ключами: «medallion» hello «hack\_лицензии» и «раскладки\_datetime».

Когда мы хранить их в таблицы Hive вскоре описаны некоторые дополнительные сведения о данных hello.

## <a name="mltasks"></a>Примеры задач прогнозирования
При приближении к данным, определение типа hello прогнозов необходимо toomake на основе его анализа помогает прояснить hello задачи, которые понадобятся tooinclude в процессе.
Ниже приведены три примера прогноза проблемы, которые мы адрес в этом пошаговом руководстве, формирование основан на hello *совет\_сумма*:

1. **Двоичная классификация**: спрогнозировать, были ли оставлены чаевые после поездку, т. е. значение *tip\_amount* больше 0 $ является позитивным примером, а значение *tip\_amount* 0 $ является негативным примером.
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. **Мультиклассовая классификация**: диапазон hello toopredict совет суммы оплаты hello trip. Разделен hello *совет\_сумма* в пять ячеек или классы:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. **Задача регрессии**: оплачена сумма hello toopredict hello подсказки для маршрута.  

## <a name="setup"></a>Настройка кластера HDInsight Hadoop для расширенной аналитики
> [!NOTE]
> Эту задачу обычно выполняет **администратор** .
> 
> 

Настроить среду Azure для использования расширенной аналитики, в которой задействуется кластер HDInsight, вы можете в три этапа.

1. [Создание учетной записи хранения](../storage/common/storage-create-storage-account.md). Эта учетная запись используется для хранения данных в хранилище больших двоичных объектов Azure. Здесь также находится Hello данные, используемые в кластерах HDInsight.
2. [Настройка Azure HDInsight Hadoop кластеры для hello Advanced Analytics процесса и технологии](machine-learning-data-science-customize-hadoop-cluster.md). На этом этапе создается кластер Azure HDInsight Hadoop, на всех узлах которого установлена 64-разрядная версия Anaconda Python 2.7. Существует два важных шага tooremember при настройке кластера HDInsight.
   
   * Не забывайте toolink учетной записи хранилища hello созданной на шаге 1 с кластером HDInsight, при его создании. Эта учетная запись хранения — используется tooaccess данных, обрабатываемых в кластере hello.
   * После создания кластера hello, включите удаленный доступ toohello головного узла кластера hello. Перейдите toohello **конфигурации** и нажмите кнопку **включить удаленный**. Этот шаг определяет hello учетные данные пользователя для удаленного входа.
3. [Создайте рабочую область машинного обучения Azure](machine-learning-create-workspace.md): рабочей области машинного обучения этот Azure — используется toobuild машинного обучения моделей. Эта задача решается после завершения просмотра исходных данных и работу выборки с использованием кластера HDInsight hello.

## <a name="getdata"></a>Получение данных hello из открытого источника
> [!NOTE]
> Эту задачу обычно выполняет **администратор** .
> 
> 

tooget hello [NYC такси приема-передачи](http://www.andresmh.com/nyctaxitrips/) набора данных из открытых расположения можно использовать любую из hello методов, описанных в [tooand перемещение данных из хранилища больших двоичных объектов](machine-learning-data-science-move-azure-blob.md) машина tooyour toocopy hello данных.

Здесь описывается, как использование AzCopy tootransfer hello файлов содержат данные. toodownload и AzCopy установки следуйте инструкциям hello в [Приступая к работе с hello служебной программы командной строки AzCopy](../storage/common/storage-use-azcopy.md).

1. Окно командной строки выполните hello следующие команды AzCopy, заменив *< path_to_data_folder >* с целевой hello:

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. По завершении копирования hello всего 24 ZIP-файлы находятся в выбранной папки данных hello. Распакуйте файлы toohello загружаются hello один каталог на локальном компьютере. Запишите hello папку, где находятся файлы сжимаются hello. Эта папка будет hello ссылка tooas *< путь\_для\_unzipped_data\_файлы\>*  — ниже.

## <a name="upload"></a>Отправка контейнер по умолчанию hello данных toohello кластера Azure HDInsight Hadoop
> [!NOTE]
> Эту задачу обычно выполняет **администратор** .
> 
> 

Следующие команды AzCopy, замените hello следующие параметры фактическими значениями hello, указанный при создании кластера Hadoop hello и распаковки файлов данных hello в hello.

* ***&#60; path_to_data_folder >*** directory hello (а также путь) на этом компьютере, которые содержат файлы данных распаковал hello  
* ***&#60; имя учетной записи хранения кластера Hadoop >*** hello учетной записи хранилища, связанной с кластером HDInsight
* ***&#60; контейнер по умолчанию для кластера Hadoop >*** контейнера по умолчанию hello, используемого кластера. Hello имя по умолчанию hello является контейнер обычно hello точно такое же имя в качестве самого кластера hello. Например если кластер hello называется «abc123.azurehdinsight.net», контейнера по умолчанию hello — abc123.
* ***&#60; ключ учетной записи хранения >*** hello ключ учетной записи хранения hello, используемый в кластере

Из командной строки или окно Windows PowerShell на компьютере выполните следующие две команды AzCopy hello.

Эта команда отправляет данные маршрута hello слишком***nyctaxitripraw*** каталог в контейнере по умолчанию hello hello кластера Hadoop.

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

Эта команда отправляет данные тариф авиакомпании hello слишком***nyctaxifareraw*** каталог в контейнере по умолчанию hello hello кластера Hadoop.

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

Hello данных должны теперь в хранилище больших двоичных объектов Azure и готов toobe потребляет внутри кластера HDInsight hello.

## <a name="#download-hql-files"></a>Войти в hello головного узла кластера Hadoop и и подготовка для исследовательского анализа
> [!NOTE]
> Эту задачу обычно выполняет **администратор** .
> 
> 

tooaccess hello головного узла кластера hello для исследовательского анализа и вниз выборки данных hello выполните hello процедуры, описанной в [доступа hello головного узла кластера Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

В этом пошаговом руководстве мы в первую очередь использовать запросы, написанные [Hive](https://hive.apache.org/), SQL-подобного языка запросов, tooperform предварительные данные исследования. запросы Hive Hello хранятся в файлах .hql. Мы затем вниз образец этого toobe данных, используемых в машинном обучении Azure для построения моделей.

tooprepare hello кластера для исследовательского анализа, мы загружать файлы .hql hello, содержащие соответствующие скрипты Hive hello из [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa локальный каталог (например, C:\temp) на головном узле hello. toodo это, откройте hello **командной строки** изнутри hello головного узла hello кластера и проблема hello, следующие две команды:

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

Эти две команды будут загружать все .hql файлы, необходимые в локальном каталоге этого пошагового руководства toohello ***C:\temp &#92;*** в hello головного узла.

## <a name="#hive-db-tables"></a>Создание базы данных Hive и таблиц, секционированных по месяцам
> [!NOTE]
> Эту задачу обычно выполняет **администратор** .
> 
> 

Мы — теперь готовы toocreate Hive таблицы для наших NYC такси dataset.
В hello головного узла кластера Hadoop hello, откройте hello ***командной строки Hadoop*** hello desktop hello головного узла, а также введите hello Hive каталог, введя команду hello

    cd %hive_home%\bin

> [!NOTE]
> **Выполнить все команды Hive в этом пошаговом руководстве из hello выше Hive bin / directory строки. Таким образом вы сможете автоматически избежать любых проблем с путем. Мы используем условия hello «Hive каталога prompt», «Hive bin / directory строки» и «Hadoop Командная строка», попеременно в этом пошаговом руководстве.**
> 
> 

Hello Hive каталога строке введите следующую команду в Hadoop Командная строка hello головного узла toosubmit hello Hive запроса toocreate Hive базы данных и таблиц hello:

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

Вот содержимое hello hello ***C:\temp\sample\_куст\_создания\_db\_и\_tables.hql*** файл, который создает базу данных Hive ***nyctaxidb *** и таблицы ***trip*** и ***тариф авиакомпании***.

    create database if not exists nyctaxidb;

    create external table if not exists nyctaxidb.trip
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double)  
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');

    create external table if not exists nyctaxidb.fare
    (
        medallion string,
        hack_license string,
        vendor_id string,
        pickup_datetime string,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double)
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');

Этот сценарий Hive создает две таблицы:

* Таблица «маршрут» Hello содержит trip подробные сведения о каждом расстояния (сведения о драйвере, время отправки, расстояние маршрута и времени)
* Таблица «тариф авиакомпании» Hello сведениями тариф авиакомпании (тариф авиакомпании сумма, сумма совет, тарифы и сборы).

Если требуется получить любые дополнительную помощь с помощью этих процедур или tooinvestigate альтернативные методы, см. раздел hello [отправить Hive запросы непосредственно из hello командной строки Hadoop ](machine-learning-data-science-move-hive-tables.md#submit).

## <a name="#load-data"></a>Загрузка данных tooHive таблиц с секций
> [!NOTE]
> Эту задачу обычно выполняет **администратор** .
> 
> 

набор данных такси Hello NYC имеет, естественным секционированием по месяцам, который мы используем tooenable запросов и обработки ускоряется. Здравствуйте ниже команды PowerShell (из каталога hello Hive, с помощью hello **командной строки Hadoop**) Загрузка данных toohello «маршрут» и «тариф авиакомпании» Hive таблиц секционированной по месяцам.

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

Hello *пример\_куст\_загрузить\_данные\_по\_partitions.hql* файл содержит следующие hello **загрузить** команд.

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

Обратите внимание, что количество запросов Hive в процессе исследования hello вариант включают выглядит в одной секции или две секции. Однако эти запросы, может быть запущен через hello все данные.

### <a name="#show-db"></a>Показать базы данных в кластере HDInsight Hadoop hello
tooshow hello баз данных, созданных в кластере HDInsight Hadoop в окне командной строки Hadoop hello, запустите следующую команду в командной строке Hadoop hello:

    hive -e "show databases;"

### <a name="#show-tables"></a>Показать hello Hive таблицы в базе данных nyctaxidb hello
tooshow hello таблицы в базе данных nyctaxidb hello, запустите следующую команду в командной строке Hadoop hello:

    hive -e "show tables in nyctaxidb;"

Мы можете подтвердить, что hello таблицы секционированы, выполнив следующую команду hello:

    hive -e "show partitions nyctaxidb.trip;"

Hello тесты на ожидаемые выходные данные приведены ниже:

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 2.075 seconds, Fetched: 12 row(s)

Аналогичным образом можно гарантировать, что этой таблицы тариф авиакомпании hello секционирована, выполнив следующую команду hello:

    hive -e "show partitions nyctaxidb.fare;"

Hello тесты на ожидаемые выходные данные приведены ниже:

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 1.887 seconds, Fetched: 12 row(s)

## <a name="#explore-hive"></a>Исследование данных и проектирование признаков в Hive
> [!NOTE]
> Обычно эту задачу выполняет **специалист по обработке и анализу данных** .
> 
> 

Здравствуйте, просмотр данных и компонентов технических задач, для данных, загруженных в таблицах Hive hello может выполняться с помощью запросов Hive hello. Вот примеры задач, о которых пойдет речь в этом разделе:

* Просмотр hello top 10 записей в обеих таблицах.
* Просмотрим распределение данных по нескольким полям в различных временных окнах.
* Проверка качества данных полей hello широты и долготы.
* Создание двоичного и мультиклассовой классификации меток, основываясь на hello **совет\_сумма**.
* Создание функции путем вычисления расстояния hello прямого маршрута.

### <a name="exploration-view-hello-top-10-records-in-table-trip"></a>Просмотр: Просмотр hello top 10 записей в таблице обработки
> [!NOTE]
> Обычно эту задачу выполняет **специалист по обработке и анализу данных** .
> 
> 

как выглядят данные hello toosee, мы изучаем 10 записей из каждой таблицы. Выполните следующие два запроса отдельно из строки directory Hive hello hello командной строки Hadoop консоли tooinspect hello записей hello.

tooget hello top 10 записей в таблице hello «маршрут» из hello первого месяца:

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

tooget hello top 10 записей в таблице hello» успешного» из hello первого месяца:

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

Часто бывает полезным toosave записей hello tooa файл удобный просмотр. Небольшое изменение toohello выше запрос выполняет эту процедуру:

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-hello-number-of-records-in-each-of-hello-12-partitions"></a>Просмотр: Просмотр hello число записей в каждом из 12 разделов hello
> [!NOTE]
> Обычно эту задачу выполняет **специалист по обработке и анализу данных** .
> 
> 

Интерес представляет hello, как изменяется номер hello приема-передачи данных во время hello календарного года. Группирование по месяцам позволяет нам toosee как выглядит этот распространения приема-передачи данных.

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

Это дает нам hello выходные данные:

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 283.406 seconds, Fetched: 12 row(s)

Здесь, hello первый столбец месяц hello и hello второй номер hello приема-передачи данных за данный месяц.

Мы также могут считаться hello общее количество записей в наш набор данных маршрута, выполнив следующую команду в строке directory Hive hello hello.

    hive -e "select count(*) from nyctaxidb.trip;"

Мы получаем такой результат:

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

Аналогичные toothose команды для набора данных trip hello показаны мы можем выпустить запросов Hive из строки directory hello Hive для hello тариф авиакомпании набора данных toovalidate hello количество записей.

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

Это дает нам hello выходные данные:

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 253.955 seconds, Fetched: 12 row(s)

Обратите внимание, что для обоих наборов данных возвращается hello точное одинаковое количество обращений в месяц. Это обеспечивает проверку первый hello приветствия, данные были правильно загружены.

Подсчет hello общее число записей в наборе данных тариф авиакомпании hello можно сделать с помощью команды hello ниже hello Hive каталога строке:

    hive -e "select count(*) from nyctaxidb.fare;"

Мы получаем такой результат.

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

Общее число записей в обеих таблицах Hello также является hello же. Вторая проверка обеспечивает приветствия, данные были правильно загружены.

### <a name="exploration-trip-distribution-by-medallion"></a>Просмотр: Распределение поездок по параметру medallion
> [!NOTE]
> Обычно эту задачу выполняет **специалист по обработке и анализу данных** .
> 
> 

В этом примере определяет medallion hello (номера такси) с более чем 100 приема-передачи данных в течение заданного периода времени. преимущества hello запроса Hello секционированы доступа к таблице с момента обусловлено hello секции переменной **месяц**. Hello результатов запроса на языке queryoutput.tsv локальный файл tooa `C:\temp` на головном узле hello.

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

Вот содержимое hello *пример\_куст\_trip\_число\_по\_medallion.hql* файла для проверки.

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

medallion Hello в наборе данных такси NYC hello определяет уникальный CAB-файлов. Мы можем определить, какие автомобили востребованы, запросив, какие из них выполнили более определенного количества поездок за определенный период времени. Hello следующий пример определяет CAB-файлов, которые сделаны приема-передачи более чем на ста hello первые три месяца и сохраняет hello запроса результаты tooa локального файла, C:\temp\queryoutput.tsv.

Вот содержимое hello *пример\_куст\_trip\_число\_по\_medallion.hql* файла для проверки.

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

Из hello куста подсказки директории, проблема hello следующую команду:

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Просмотр: распределение поездок по параметрам medallion и hack_license
> [!NOTE]
> Обычно эту задачу выполняет **специалист по обработке и анализу данных** .
> 
> 

Изучение набора данных, мы в большинстве случаев используется tooexamine hello число вхождений co групп значений. В этом разделе приведены примеры как toodo для CAB-файлы и драйверы.

Hello *пример\_куст\_trip\_число\_по\_medallion\_license.hql* группы файлов данных тариф авиакомпании hello задания «medallion» и «hack_license» и возвращает количество всех возможных сочетаний. Ниже приведено его содержимое.

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

Этот запрос возвращает комбинации автомобиля и конкретного водителя, упорядоченных по убыванию количества поездок.

Из hello Hive каталога строки, запустите:

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

локальный файл tooa C:\temp\queryoutput.tsv записываются результаты запроса Hello.

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a>Исследование: оценка качества данных через проверку наличия недопустимых записей долготы и широты
> [!NOTE]
> Обычно эту задачу выполняет **специалист по обработке и анализу данных** .
> 
> 

Общие цель разведочном анализе данных — tooweed неверный записей. Hello пример в этом разделе определяет ли hello поля широты и долготы содержать либо значение далеко за пределами области NYC hello. Так как это, вероятно, такие записи значения ошибочные долготы широты, мы хотим tooeliminate их из всех данных toobe используется для моделирования.

Вот содержимое hello *пример\_куст\_качество\_assessment.hql* файла для проверки.

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


Из hello Hive каталога строки, запустите:

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

Hello *-S* аргумент, включенных в этой команде подавляет распечатку экрана hello состояние задания Hive Map/Reduce hello. Это полезно, поскольку это делает печать экрана приветствия hello Hive выходных данных запроса более удобном для чтения.

### <a name="exploration-binary-class-distributions-of-trip-tips"></a>Исследования: двоичные классовые распределения чаевых за поездки
> [!NOTE]
> Обычно эту задачу выполняет **специалист по обработке и анализу данных** .
> 
> 

Для проблемы бинарной классификации hello появлялся hello [примеры задач прогнозирования](machine-learning-data-science-process-hive-walkthrough.md#mltasks) разделе ли совет было задано или не является полезным tooknow. Распределение чаевых является двоичным:

* чаевые оставлены (класс 1, tip\_amount > $0);  
* чаевые не оставлены (класс 0, tip\_amount = $0).

Hello *пример\_куст\_чаевых оставил зависимости\_frequencies.hql* приведенный ниже файла делает это.

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

Из hello Hive каталога строки, запустите:

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-hello-multiclass-setting"></a>Просмотр: Класс распределения в мультиклассовой приветствия
> [!NOTE]
> Обычно эту задачу выполняет **специалист по обработке и анализу данных** .
> 
> 

Для hello мультиклассовой классификации проблемы, описанные в hello [примеры задач прогнозирования](machine-learning-data-science-process-hive-walkthrough.md#mltasks) этот набор данных также решается tooa естественное классификации, где мы предлагаем toopredict hello объем hello советы по заданному раздела. Совет диапазоны ячеек toodefine можно использовать в запросе hello. tooget Здравствуйте класса распределения для hello различные диапазоны совет, мы используем hello *пример\_куст\_совет\_диапазон\_frequencies.hql* файла. Ниже приведено его содержимое.

    SELECT tip_class, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount=0, 0,
            if(tip_amount>0 and tip_amount<=5, 1,
            if(tip_amount>5 and tip_amount<=10, 2,
            if(tip_amount>10 and tip_amount<=20, 3, 4)))) as tip_class, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tip_class;

Выполните следующую команду из командной строки Hadoop консоли hello.

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a>Исследование: вычисление расстояния по прямой между двумя местоположениями, заданными долготой и широтой
> [!NOTE]
> Обычно эту задачу выполняет **специалист по обработке и анализу данных** .
> 
> 

Наличие меру расстояния прямой hello позволяет нам toofind out hello несоответствие между ним и hello фактическое быть расстояние. Эта функция мы мотивации, указав, что пассажира может быть меньше tootip скорее всего, если они понять, что драйвер hello намеренно было их с гораздо более длинный путь.

Сравнение hello toosee trip фактическое расстояние и hello [гаверсинуса](http://en.wikipedia.org/wiki/Haversine_formula) между двумя точками широты долготы (расстояние hello «circle отлично»), мы используем hello тригонометрические функции, доступные в пределах Hive, таким образом:

    set R=3959;
    set pi=radians(180);

    insert overwrite directory 'wasb:///queryoutputdir'

    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
    ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
     *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
     *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
     /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
     +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
     pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
    from nyctaxidb.trip
    where month=1
    and pickup_longitude between -90 and -30
    and pickup_latitude between 30 and 90
    and dropoff_longitude between -90 and -30
    and dropoff_latitude between 30 and 90;

В приведенном выше запросе hello R hello радиус hello Земли в милях, который pi преобразованный tooradians. Обратите внимание, что hello долготы широту точки «фильтрация» tooremove значения, которые могут значительно отличаться от области NYC hello.

В этом случае мы записи наши результаты tooa каталог с именем «queryoutputdir». Hello последовательность команд, приведенных ниже сначала создает этот каталог выходных данных, а затем запускается команда Hive hello.

Из hello Hive каталога строки, запустите:

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


Hello результаты запроса записываются больших двоичных объектов too9 Azure ***queryoutputdir/000000\_0*** слишком ***queryoutputdir/000008\_0*** в контейнере по умолчанию hello hello кластера Hadoop.

размер hello toosee hello отдельных больших двоичных объектов, мы выполните следующую команду из каталога строки hello Hive hello:

    hdfs dfs -ls wasb:///queryoutputdir

toosee hello содержимое заданного файла, например 000000\_0, мы используем Hadoop `copyToLocal` команды, таким образом.

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> `copyToLocal` может выполняться очень медленно для больших файлов, и использовать его с ними не рекомендуется.  
> 
> 

Ключевое преимущество всех данных находятся в большом двоичном объекте Azure — что мы может исследовать данные hello машинного обучения Azure с помощью hello [импорта данных] [ import-data] модуля.

## <a name="#downsample"></a>Сокращение выборки и построение моделей в машинном обучении Azure
> [!NOTE]
> Обычно эту задачу выполняет **специалист по обработке и анализу данных** .
> 
> 

После этапа анализа данных произвольного hello не теперь готовы toodown образец hello данных для построения моделей в машинном обучении Azure. В этом разделе рассказывается, как toouse куст запрос toodown hello данные, которые затем осуществляется из hello [импорта данных] [ import-data] модуль в машинном обучении Azure.

### <a name="down-sampling-hello-data"></a>Вниз hello данных выборки
Эта процедура состоит из двух шагов. Сначала мы присоединить hello **nyctaxidb.trip** и **nyctaxidb.fare** таблиц на три ключа, которые представлены во всех записях: «medallion», «hack\_лицензии», и «раскладки\_datetime». Затем мы создаем метку двоичной классификации **tipped** и метку мультиклассовой классификации **tip\_class**.

hello может toouse toobe работу выборки данных непосредственно из hello [импорта данных] [ import-data] модуля машинного обучения Azure, при необходимости toostore результаты hello hello выше запрос tooan внутренней таблицы Hive. В ниже создайте внутреннюю таблицу Hive и заполнить его содержимое с объединить hello "и" вниз данных выборки.

Hello запросов применяет стандартные функции Hive непосредственно toogenerate hello час дня, недели года, дня недели (понедельник е. 1 и воскресенье. 7 е.) из hello» раскладки\_datetime» поля и hello прямой расстояние между раскладки hello и dropoff расположения. Пользователи могут ссылаться слишком[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) полный список таких функций.

Здравствуйте, запрос, а затем вниз образцы данных hello, чтобы результаты запроса hello помещается в студии машинного обучения Azure hello. Лишь около 1% от исходного набора данных hello импортируется в hello Studio.

Ниже приведены hello содержимое *пример\_куст\_Подготовка\_для\_aml\_full.hql* файл, который подготавливает данные для модели сборки в машинном обучении Azure.

        set R = 3959;
        set pi=radians(180);

        create table if not exists nyctaxidb.nyctaxi_downsampled_dataset (

        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\n'
        stored as textfile;

        --- now insert contents of hello join into hello above internal table

        insert overwrite table nyctaxidb.nyctaxi_downsampled_dataset
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class

        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
        *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
        +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance,
        rand() as sample_key

        from nyctaxidb.trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from nyctaxidb.fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01

запрос для этого запроса из каталога Hive hello toorun:

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

Теперь у нас есть внутренняя таблица «nyctaxidb.nyctaxi_downsampled_dataset», к которому можно получить с помощью hello [импорта данных] [ import-data] модуля из машинного обучения Azure. Кроме того, мы можем использовать этот набор данных для построения моделей машинного обучения.  

### <a name="use-hello-import-data-module-in-azure-machine-learning-tooaccess-hello-down-sampled-data"></a>Использование модуля hello импорта данных в hello tooaccess машинного обучения Azure вниз выборки данных
В качестве необходимых компонентов для выдачи запросов Hive в hello [импорта данных] [ import-data] модуля машинного обучения Azure, необходимо получить доступ к рабочей области машинного обучения Azure tooan и доступ к параметрам toohello hello кластер и его соответствующей учетной записи.

Некоторые сведения о hello [импорта данных] [ import-data] tooinput параметры модуля и hello:

**URI сервера HCatalog**: Если имя кластера hello abc123, то это просто: https://abc123.azurehdinsight.net

**Имя учетной записи пользователя Hadoop** : hello имени пользователя, выбранного для кластера hello (**не** hello имя пользователя удаленного доступа)

**Пароль учетной записи пользователя Hadoop** : hello пароль, выбранные для кластера hello (**не** hello пароль удаленного доступа)

**Расположение выходных данных** : это выбирается toobe Azure.

**Имя учетной записи хранилища Azure** : имя учетной записи хранения по умолчанию hello связанные с кластером hello.

**Имя контейнера Azure** : это имя контейнера по умолчанию hello hello кластера и обычно является Здравствуйте таким же, как имя кластера hello. Для кластера с именем «abc123» это будет просто abc123.

> [!IMPORTANT]
> **Любой таблицы, мы обратиться с помощью hello tooquery [импорта данных] [ import-data] модуль в машинном обучении Azure должен быть внутренней таблицы.** Определить, является ли таблица T в базе данных D.db внутренней таблицей, можно приведенным ниже образом.
> 
> 

Из hello куста каталога строке команды hello проблемы:

    hdfs dfs -ls wasb:///D.db/T

Если таблица hello является внутренней таблицей, а он заполняется, его содержимое необходимо отображены здесь. Другой способ toodetermine ли таблицы во внутреннюю таблицу — toouse hello обозреватель хранилища Azure. Использовать имя контейнера по умолчанию toohello toonavigate hello кластера, а затем отфильтровать по имени таблицы hello. Если hello таблицы и ее содержимое отображается, это подтверждает, что это внутренней таблицы.

Ниже приведен снимок запроса Hive hello и hello [импорта данных] [ import-data] модуля:

![Запрос Hive для модуля "Импорт данных"](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

Обратите внимание, что с момента наш список выборки данных располагается в контейнер по умолчанию hello, hello результирующий запрос Hive из машинного обучения Azure очень проста и только» ВЫБЕРИТЕ * из nyctaxidb.nyctaxi\_понижению разрешения\_данных».

набор данных Hello теперь может использоваться как начальная точка для построения моделей машинного обучения hello.

### <a name="mlmodel"></a>Построение моделей в компоненте машинного обучения Azure
Мы стали может tooproceed toomodel построение и развертывание модели в [машинного обучения Azure](https://studio.azureml.net). Hello данных готова к нам toouse в устранению проблем прогноза hello, указанных выше:

**1. Двоичная классификация**: toopredict ли уплаченной Совет для маршрута.

**Используемое средство обучения:** двухклассовая логистическая регрессия.

а. Для нашей задачи целевой меткой (меткой класса) будет «tipped» (чаевые выплачены). В нашем исходном наборе данных с сокращенной выборкой есть несколько столбцов, содержащих целевые утечки сведений для данного эксперимента по классификации. В частности: совет\_класса, совет\_сумма и общая\_сумма раскрывать информацию о целевой метке hello, который доступен не во время тестирования. Удалим эти столбцы из рассмотрения с помощью hello [Выбор столбцов в наборе данных] [ select-columns] модуля.

моментальный снимок Hello ниже показано нашей toopredict эксперимента ли уплаченной Совет для данного маршрута.

![Моментальный снимок эксперимента](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

b. Для этого эксперимента распределение наших целевых меток составляло примерно 1:1.

моментальный снимок Hello ниже показано распределение hello меток класса подсказки для проблемы бинарной классификации hello.

![Распределение меток класса чаевых](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

В результате мы получаем AUC 0.987, как показано на следующем рисунке hello.

![Значение AUC](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

**2. Мультиклассовая классификация**: hello диапазон toopredict совет суммы оплаты trip hello, ранее с помощью hello определенных классов.

**Используемое средство обучения:** мультиклассовая логистическая регрессия.

а. Для этой задачи нашей целевой меткой (меткой класса) будет tip\_class, которая может принимать одно из пяти значений (0, 1, 2, 3, 4). Как и случае hello двоичной классификации у нас есть несколько столбцов, целевой утечки в этом эксперименте. В частности: чаевых оставил зависимости, совет\_сумма, общее\_сумма раскрывать информацию о целевой метке hello, который доступен не во время тестирования. Мы удаляем этих столбцов с помощью hello [Выбор столбцов в наборе данных] [ select-columns] модуля.

Hello снимок ниже показан нашей toopredict эксперимент, в какие ячейки совет является вероятностью toofall (класса 0: совет = $0, класс 1: совет > $0 и совет < = $5, класса 2: совет > $5 и совет < = 10, 3 класса: совет > 10 и подсказки < = 20 Класс 4: совет > 20)

![Моментальный снимок эксперимента](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

Теперь мы покажем, как выглядит наше фактическое тестовое классовое распределение. Мы видим, хотя класса 0 и 1 класс распространено, hello другие классы происходят редко.

![Тестовое классовое распределение](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

b. В этом эксперименте мы используем toolook матрицы путаницы в нашем точности прогноза. Такой способ показан ниже.

![Матрица неточностей](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

Обратите внимание, что пока наш класс точности для наиболее распространенных классов hello достаточно хороша, hello модели не хорошие «обучение» для некоторых классов hello.

**3. Задача регрессии**: оплачена сумма hello toopredict подсказки для маршрута.

**Используемое средство обучения:** повышенное дерево принятия решений.

а. Для нашей задачи целевой меткой (меткой класса) будет "tip\_amount" (сумма чаевых). Утечки нашей цели в данном случае являются: чаевых оставил зависимости, совет\_класса, общее\_сумма; эти переменные позволяют просматривать информацию о сумма hello подсказки, которая обычно недоступна во время тестирования. Мы удаляем этих столбцов с помощью hello [Выбор столбцов в наборе данных] [ select-columns] модуля.

belows Hello моментальных снимков отображается нашей эксперимента toopredict hello объем hello заданному подсказки.

![Моментальный снимок эксперимента](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

b. Для проблем регрессии мы измерения точности hello нашей прогноза, просмотрев ошибки hello квадрат в прогнозах hello hello коэффициент смешанной корреляции и hello как. Они показаны ниже.

![Статистические данные прогноза](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

Мы видим, что о hello коэффициент детерминации это 0.709, подразумевая около 71% дисперсию hello объясняется коэффициенты нашей модели.

> [!IMPORTANT]
> Дополнительные сведения о машинного обучения Azure toolearn и как tooaccess и использовать его, воспользуйтесь слишком[возможности машинного обучения?](machine-learning-what-is-machine-learning.md). Очень полезным ресурсом для воспроизведения с кучей экспериментах машинного обучения на машинном обучении Azure — hello [коллекции аналитики Cortana](https://gallery.cortanaintelligence.com/). Коллекция Hello охватывает охват экспериментов и подробное введение в hello диапазон возможностей машинного обучения Azure.
> 
> 

## <a name="license-information"></a>Сведения о лицензии
Это пошаговое руководство по примеру и его соответствующие сценарии совместно корпорацией Майкрософт в рамках лицензии MIT hello. Проверьте файл LICENSE.txt hello в каталоге hello hello образца кода на GitHub для получения дополнительных сведений.

## <a name="references"></a>Ссылки
•    [Страница загрузки данных о поездках такси Нью-Йорка (Andrés Monroy)](http://www.andresmh.com/nyctaxitrips/)  
•    [Получение данных о поездках такси Нью-Йорка на основании FOIL (Chris Whong)](http://chriswhong.com/open-data/foil_nyc_taxi/)   
•    [Статистические данные о комиссионных сборах за аренду такси и лимузинов Нью-Йорка](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
