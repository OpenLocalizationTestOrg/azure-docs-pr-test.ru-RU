---
title: "Полное пошаговое руководство по масштабируемому анализу данных с помощью Azure Data Lake | Документация Майкрософт"
description: "В этой статье описано, как выполнять задания по исследованию и двоичной классификации данных на основе набора данных озера данных Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: cgronlun
editor: cgronlun
ms.assetid: 91a8207f-1e57-4570-b7fc-7c5fa858ffeb
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/13/2017
ms.author: bradsev; weig
ms.openlocfilehash: b18b454d1fcdfb2b6e8ea77508f779aeabdc87a0
ms.sourcegitcommit: 732e5df390dea94c363fc99b9d781e64cb75e220
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/14/2017
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a>Полное пошаговое руководство по масштабируемому анализу данных с помощью Azure Data Lake
В этом пошаговом руководстве на примере набора данных о поездках и тарифах такси в Нью-Йорке показано, как использовать Azure Data Lake для выполнения задач по исследованию и двоичной классификации данных, чтобы спрогнозировать вероятность получения чаевых за поездку. Здесь подробно описаны шаги [процесса обработки и анализа данных группы](http://aka.ms/datascienceprocess)— от получения данных для обучения модели и до развертывания веб-службы, которая публикует модель.

### <a name="azure-data-lake-analytics"></a>Аналитика озера данных Azure
[Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) предусматривает все необходимые возможности для аналитиков, упрощающие хранение данных любого размера, формата и скорости обработки и обеспечивающие высокую гибкость и экономичность обработки данных, углубленной аналитики и создания моделей машинного обучения.   Плата взимается за задание, и только если данные обработаны фактически. Аналитика озера данных Azure предполагает использование U-SQL, языка, который объединяет декларативную природу SQL с выразительностью C#, чтобы позволить создавать масштабируемые распределенные запросы. Она позволяет обрабатывать неструктурированные данные, применяя схему для чтения, вставки пользовательской логики и определяемых пользователем функций (UDF), и предполагает возможности расширения, обеспечивающие точный контроль над выполнением в масштабе. Дополнительные сведения о принципах разработки U-SQL см. в [записи блога о Visual Studio](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).

Аналитика озера данных — это также ключевая часть Cortana Analytics Suite. Она поддерживает работу с хранилищем данных SQL Azure, Power BI и фабрикой данных. Это создает всеобъемлющую облачную платформу для работы с большими данными и углубленной аналитики.

В начале этого пошагового руководства описано, как установить необходимые компоненты и ресурсы, которые требуются для выполнения задач обработки и анализа данных. Затем здесь описаны шаги по обработке данных, выполняемые с использованием U-SQL. В конце статьи показано, как использовать Python и Hive со студией машинного обучения Azure для создания и развертывания прогнозных моделей. 

### <a name="u-sql-and-visual-studio"></a>U-SQL и Visual Studio
В этом пошаговом руководстве рекомендуется использовать Visual Studio, чтобы изменять сценарии U-SQL для обработки набора данных. Сценарии U-SQL, описанные в документе, приводятся в отдельном файле. Процесс включает в себя прием, исследование и выборку данных. Также здесь показывается, как выполнить задание со сценарием U-SQL на портале Azure. Для данных в связанном кластере HDInsight создаются таблицы Hive, которые упрощают сборку и развертывание модели двоичной классификации в Студии машинного обучения Azure.  

### <a name="python"></a>Python
В этом пошаговом руководстве также содержится раздел, в котором показано, как создавать и развертывать прогнозную модель с помощью Python и студии машинного обучения Azure. Здесь предоставлена записная книжка Jupyter со скриптами Python для шагов в этом процессе. Этот Notebook включает в себя код для некоторых дополнительных шагов проектирования признаков и создания моделей, например многоклассовой классификации и регрессии, в дополнение к модели двоичной классификации, описанной здесь. Задача регрессии: спрогнозировать сумму чаевых в зависимости от других признаков. 

### <a name="azure-machine-learning"></a>Машинное обучение Azure
Студия машинного обучения Azure используется для создания и развертывания прогнозных моделей. Для этого используется два подхода: первый — с помощью сценариев Python, а второй — с использованием таблиц Hive на кластере HDInsight (Hadoop).

### <a name="scripts"></a>Сценарии
В этом пошаговом руководстве описаны только основные шаги. Вы можете скачать полный **скрипт U-SQL**, а также **записную книжку Jupyter** из [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).

## <a name="prerequisites"></a>Предварительные требования
Прежде чем начать работу по этим разделам, необходимо обеспечить наличие следующего:

* Подписка Azure. Если у вас ее нет, см. статью [о получении бесплатной пробной версии Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* [Рекомендуется] Visual Studio 2013 или более поздней версии. Если вы еще не установили одну из этих версий, можно скачать бесплатную версию Community с сайта [Visual Studio Community](https://www.visualstudio.com/vs/community/).

> [!NOTE]
> Чтобы отправлять запросы Azure Data Lake, можно использовать не только Visual Studio, но и портал Azure. Инструкции о том, как сделать это с помощью Visual Studio и на портале, см. в разделе **Обработка данных с использованием U-SQL**. 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a>Подготовка среды анализа данных для озера данных Azure
Чтобы подготовить среду анализа данных для этого пошагового руководства, создайте следующие ресурсы:

* хранилище озера данных Azure; 
* Аналитику озера данных Azure;
* учетную запись хранения BLOB-объектов;
* учетную запись Студии машинного обучения Azure;
* средства озера данных Azure для Visual Studio (рекомендуется).

Этот раздел содержит указания о том, как создать каждый из этих ресурсов. Если для создания модели вы решили вместо Python использовать таблицы Hive и службу "Машинное обучение Azure", то вам следует подготовить кластер HDInsight (Hadoop). Этот альтернативный способ описан в разделе "Вариант 2" ниже.


> [!NOTE]
> **Azure Data Lake Store** можно создать отдельно или вместе с **Azure Data Lake Analytics** в качестве хранилища по умолчанию. В предлагаемых инструкциях эти ресурсы создаются отдельно, но для учетной записи хранения Data Lake это не обязательно.
>
> 

### <a name="create-an-azure-data-lake-store"></a>Создание хранилища озера данных Azure


Создайте ADLS на [портале Azure](http://portal.azure.com). Дополнительные сведения см. в статье [Создание кластеров HDInsight, использующих Data Lake Store, с помощью портала Azure](../../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md). Обязательно настройте удостоверение кластера AAD в колонке **Источник данных** колонки **Необязательная конфигурация**, показанной здесь. 

 ![3](./media/data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a>Создание учетной записи Аналитики озера данных Azure
Создайте учетную запись ADLA на [портале Azure](http://portal.azure.com). Дополнительные сведения см. в статье [Руководство. Начало работы с Azure Data Lake Analytics с помощью портала Azure](../../data-lake-analytics/data-lake-analytics-get-started-portal.md). 

 ![4](./media/data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a>Создание учетной записи хранения BLOB-объектов Azure
Создайте учетную запись хранилища BLOB-объектов Azure на [портале Azure](http://portal.azure.com). Дополнительные сведения см. в разделе "Создайте учетную запись хранения" в статье [Об учетных записях хранения Azure](../../storage/common/storage-create-storage-account.md).

 ![5](./media/data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a>Настройка учетной записи Студии машинного обучения Azure
Войдите в студию машинного обучения со страницы [Машинного обучения Azure](https://azure.microsoft.com/services/machine-learning/) . Нажмите кнопку **Начните прямо сейчас** и выберите Free Workspace ("Бесплатная рабочая область") или Standard Workspace ("Стандартная рабочая область"). Теперь вы можете создавать эксперименты в Студии машинного обучения Azure.  

### <a name="install-azure-data-lake-tools-recommended"></a>Установка инструментов озера данных Azure [рекомендуется]
Установите инструменты озера данных Azure в зависимости от своей версии Visual Studio со страницы [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504)(Инструменты озера данных Azure для Visual Studio).

 ![6](./media/data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

После успешного завершения установки откройте Visual Studio. Вы должны увидеть вкладку Data Lake ("Озеро данных") в меню вверху. Ресурсы Azure должны отобразиться на левой панели при входе в учетную запись Azure.

 ![7](./media/data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="the-nyc-taxi-trips-dataset"></a>Набор данных "Поездки такси Нью-Йорка"
Здесь используется общедоступный набор данных [Поездки такси Нью-Йорка](http://www.andresmh.com/nyctaxitrips/). Данные о поездках такси Нью-Йорка содержатся в сжатых CSV-файлах размером около 20 ГБ (примерно 48 ГБ в распакованном виде), которые включают в себя сведения о более 173 млн отдельных поездок и платежах за каждую поездку. В каждой записи о поездке есть следующие данные: расположение пунктов посадки и высадки, время посадки и высадки, анонимизированный номер лицензии водителя, номер медальона (уникальный идентификатор такси). Данные включают в себя все поездки за 2013 год и предоставляются в виде следующих двух наборов данных за каждый месяц:

CSV-файл trip_data содержит подробную информацию о поездке, например число пассажиров, пункты отправления и назначения, продолжительность поездки и ее расстояние. Вот несколько примеров записей:

       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868



CSV-файл trip_fare содержит подробную информацию об оплате каждой поездки, такие как тип оплаты, сумма тарифа, надбавка и налоги, чаевые и пошлины, а также общая выплаченная сумма. Вот несколько примеров записей:

       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Уникальный ключ для объединения trip\_data и trip\_fare состоит из следующих трех полей: medallion, hack\_license и pickup\_datetime. Необработанные файлы в формате CSV можно получать из общедоступных больших двоичных объектов хранилища Azure. Сценарий U-SQL для этого объединения находится в разделе [Объединение таблиц trip и fare](#join) .

## <a name="process-data-with-u-sql"></a>Обработка данных с использованием U-SQL
Задачи обработки данных в этом разделе предусматривают прием, проверку качества, исследование и выборку данных. Также показано, как объединить таблицы trip и fare. В последнем разделе показано, как выполнить задание со сценарием U-SQL на портале Azure. Ниже приведены ссылки на каждый подраздел.

* [Прием данных: чтение из общедоступного большого двоичного объекта](#ingest)
* [Проверка качества данных](#quality)
* [Исследование данных](#explore)
* [Объединение таблиц trip и fare](#join)
* [Выборка данных](#sample)
* [Выполнение заданий U-SQL](#run)

Сценарии U-SQL, описанные в документе, приводятся в отдельном файле. Можно скачать полные **сценарии U-SQL** из [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).

Чтобы выполнить сценарий U-SQL, откройте Visual Studio, выберите **Файл --> Создать --> Проект**, щелкните **U-SQL Project** (Проект U-SQL), укажите имя и сохраните проект в папке.

![8](./media/data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> Для выполнения сценариев U-SQL вместо Visual Studio можно использовать портал Azure. Вы можете перейти к ресурсу Azure Data Lake Analytics на портале и отправить запросы напрямую, как показано на следующем рисунке.
> 
> 

![9](./media/data-lake-walkthrough/9-portal-submit-job.PNG)

### <a name="ingest"></a>Прием данных: чтение из общедоступного большого двоичного объекта
Данные большого двоичного объекта Azure расположены по адресу **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**, и их можно извлечь, используя **Extractors.Csv()**. В следующих скриптах подставьте имена своих контейнера и учетной записи хранения для container_name@blob_storage_account_name в адресе wasb. Благодаря тому, что файлы имеют одинаковый формат имен, вы можете считать все 12 файлов поездок сразу, используя шаблон **trip\_data_{\*\}}.csv**. 

    ///Read in Trip data
    @trip0 =
        EXTRACT 
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string
    // This is reading 12 trip data from blob
    FROM "wasb://container_name@blob_storage_account_name.blob.core.windows.net/nyctaxitrip/trip_data_{*}.csv"
    USING Extractors.Csv();

В первой строке содержатся заголовки, поэтому необходимо их удалить и заменить типы столбцов на соответствующие. Обработанные данные вы можете сохранить в хранилище Azure Data Lake с помощью **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/имя_папки/имя_файла**_ или в учетной записи хранилища BLOB-объектов Azure с помощью **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**. 

    // change data types
    @trip =
        SELECT 
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        DateTime.Parse(pickup_datetime) AS pickup_datetime,
        DateTime.Parse(dropoff_datetime) AS dropoff_datetime,
        Int32.Parse(passenger_count) AS passenger_count,
        Double.Parse(trip_time_in_secs) AS trip_time_in_secs,
        Double.Parse(trip_distance) AS trip_distance,
        (pickup_longitude==string.Empty ? 0: float.Parse(pickup_longitude)) AS pickup_longitude,
        (pickup_latitude==string.Empty ? 0: float.Parse(pickup_latitude)) AS pickup_latitude,
        (dropoff_longitude==string.Empty ? 0: float.Parse(dropoff_longitude)) AS dropoff_longitude,
        (dropoff_latitude==string.Empty ? 0: float.Parse(dropoff_latitude)) AS dropoff_latitude
    FROM @trip0
    WHERE medallion != "medallion";

    ////output data to ADL
    OUTPUT @trip   
    TO "swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data to blob
    OUTPUT @trip   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

Аналогичным образом можно выполнить чтение наборов данных о тарифах. Чтобы просмотреть данные, щелкните Azure Data Lake Store правой кнопкой мыши и выберите **Портал Azure --> Обозреватель данных** или **Проводник** в Visual Studio. 

 ![10](./media/data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/data-lake-walkthrough/11-data-in-ADL.PNG)

### <a name="quality"></a>Проверка качества данных
После считывания таблиц trip и fare можно проверить качество данных следующим образом. Полученные файлы в формате CSV можно поместить в хранилище BLOB-объектов Azure или хранилище озера данных Azure. 

Узнайте количество медальонов и их уникальные номера:

    ///check the number of medallions and unique number of medallions
    @trip2 =
        SELECT
        medallion,
        vendor_id,
        pickup_datetime.Month AS pickup_month
        FROM @trip;

    @ex_1 =
        SELECT
        pickup_month, 
        COUNT(medallion) AS cnt_medallion,
        COUNT(DISTINCT(medallion)) AS unique_medallion
        FROM @trip2
        GROUP BY pickup_month;
        OUTPUT @ex_1   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
    USING Outputters.Csv(); 

Определите медальоны, которые принадлежат такси, осуществившим более 100 поездок:

    ///find those medallions that had more than 100 trips
    @ex_2 =
        SELECT medallion,
               COUNT(medallion) AS cnt_medallion
        FROM @trip2
        //where pickup_datetime >= "2013-01-01t00:00:00.0000000" and pickup_datetime <= "2013-04-01t00:00:00.0000000"
        GROUP BY medallion
        HAVING COUNT(medallion) > 100;
        OUTPUT @ex_2   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

Найдите записи, недопустимые в отношении pickup_longitude:

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
    USING Outputters.Csv(); 

Найдите отсутствующие значения некоторых переменных:

    //check missing values
    @res =
        SELECT *,
               (medallion == null? 1 : 0) AS missing_medallion
        FROM @trip;

    @trip_summary6 =
        SELECT 
            vendor_id,
        SUM(missing_medallion) AS medallion_empty, 
        COUNT(medallion) AS medallion_total,
        COUNT(DISTINCT(medallion)) AS medallion_total_unique  
        FROM @res
        GROUP BY vendor_id;
    OUTPUT @trip_summary6
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <a name="explore"></a>Просмотр данных
Чтобы лучше понять эти данные, исследуйте их с помощью следующих скриптов.

Получите распределение поездок с чаевыми и без них:

    ///tipped vs. not tipped distribution
    @tip_or_not =
        SELECT *,
               (tip_amount > 0 ? 1: 0) AS tipped
        FROM @fare;

    @ex_4 =
        SELECT tipped,
               COUNT(*) AS tip_freq
        FROM @tip_or_not
        GROUP BY tipped;
        OUTPUT @ex_4   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

Получите распределение сумм чаевых с пороговыми значениями 0, 5, 10 и 20 долларов.

    //tip class/range distribution
    @tip_class =
        SELECT *,
               (tip_amount >20? 4: (tip_amount >10? 3:(tip_amount >5 ? 2:(tip_amount > 0 ? 1: 0)))) AS tip_class
        FROM @fare;
    @ex_5 =
        SELECT tip_class,
               COUNT(*) AS tip_freq
        FROM @tip_class
        GROUP BY tip_class;
        OUTPUT @ex_5   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
    USING Outputters.Csv(); 

Получите базовые статистические данные о расстоянии поездок:

    // find basic statistics for trip_distance
    @trip_summary4 =
        SELECT 
            vendor_id,
            COUNT(*) AS cnt_row,
            MIN(trip_distance) AS min_trip_distance,
            MAX(trip_distance) AS max_trip_distance,
            AVG(trip_distance) AS avg_trip_distance 
        FROM @trip
        GROUP BY vendor_id;
    OUTPUT @trip_summary4
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

Узнайте процентили расстояния поездок.

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
    USING Outputters.Csv(); 


### <a name="join"></a>Объединение таблиц trip и fare
Таблицы trip и fare можно объединить по medallion, hack_license и pickup_time.

    //join trip and fare table

    @model_data_full =
    SELECT t.*, 
    f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
    (f.tip_amount > 0 ? 1: 0) AS tipped,
    (f.tip_amount >20? 4: (f.tip_amount >10? 3:(f.tip_amount >5 ? 2:(f.tip_amount > 0 ? 1: 0)))) AS tip_class
    FROM @trip AS t JOIN  @fare AS f
    ON   (t.medallion == f.medallion AND t.hack_license == f.hack_license AND t.pickup_datetime == f.pickup_datetime)
    WHERE   (pickup_longitude != 0 AND dropoff_longitude != 0 );

    //// output to blob
    OUTPUT @model_data_full   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data to ADL
    OUTPUT @model_data_full   
    TO "swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


Вычислите количество записей, среднюю сумму чаевых, дисперсию суммы чаевых и процент поездок, за которые выплатили чаевые, для каждого уровня количества пассажиров.

    // contigency table
    @trip_summary8 =
        SELECT passenger_count,
               COUNT(*) AS cnt,
               AVG(tip_amount) AS avg_tip_amount,
               VAR(tip_amount) AS var_tip_amount,
               SUM(tipped) AS cnt_tipped,
               (float)SUM(tipped)/COUNT(*) AS pct_tipped
        FROM @model_data_full
        GROUP BY passenger_count;
        OUTPUT @trip_summary8
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <a name="sample"></a>Выборка данных
Сначала случайным образом выберите 0,1 % данных из объединенной таблицы:

    //random select 1/1000 data for modeling purpose
    @addrownumberres_randomsample =
    SELECT *,
            ROW_NUMBER() OVER() AS rownum
    FROM @model_data_full;

    @model_data_random_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_randomsample
    WHERE rownum % 1000 == 0;

    OUTPUT @model_data_random_sample_1_1000   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

Затем выполните стратифицированную выборку по двоичной переменной tip_class:

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output to blob
    OUTPUT @model_data_stratified_sample_1_1000   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data to ADL
    OUTPUT @model_data_stratified_sample_1_1000   
    TO "swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <a name="run"></a>Выполнение заданий U-SQL
Завершив редактировать сценарии U-SQL, вы можете отправить их на сервер, используя учетную запись Аналитики озера данных Azure. Выберите вкладку **Data Lake**, щелкните **Отправить задание**, а затем выберите свою учетную запись в поле **Analytics Account** (Учетная запись Аналитики), значение параметра **Параллелизм** и нажмите кнопку **Отправить**.  

 ![12](./media/data-lake-walkthrough/12-submit-USQL.PNG)

Если задание успешно компилируется, вы сможете наблюдать за его состоянием в Visual Studio. После завершения задания можно даже воспроизвести его выполнение и определить, на каких шагах возникают узкие места, чтобы повысить эффективность работы. Вы также можете открыть портал Azure, чтобы проверить состояние заданий U-SQL.

 ![13.](./media/data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/data-lake-walkthrough/14-USQL-jobs-portal.PNG)

Теперь можно проверить выходные файлы в хранилище BLOB-объектов Azure или на портале Azure. Данные стратифицированной выборки пригодятся на следующем шаге для моделирования.

 ![15](./media/data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a>Создание и развертывание моделей в Машинном обучении Azure
Доступны два варианта извлечения данных в службу "Машинное обучение Azure" для создания и развертывания моделей. 

* Первый вариант предусматривает использование данных выборки, записанных в большой двоичный объект Azure (на шаге **Выборка данных** выше), и Python, чтобы создать и развернуть модели из Машинного обучения Azure. 
* Второй вариант предполагает, что вы запрашиваете данные озера данных Azure напрямую с помощью запроса Hive. При выборе такого варианта необходимо создать новый кластер HDInsight или использовать кластер HDInsight, который уже есть. Таблицы Hive кластера должны указывать на данные о такси Нью-Йорка в хранилище озера данных Azure.  В следующих разделах рассматриваются оба варианта. 

## <a name="option-1-use-python-to-build-and-deploy-machine-learning-models"></a>Вариант 1. Использование Python для создания и развертывания моделей машинного обучения
Для создания и развертывания моделей машинного обучения, используя Python, создайте записную книжки Jupyter на локальном компьютере или в студии машинного обучения Azure. Записная книжка Jupyter, которая доступна на сайте [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough), содержит полный код для исследования и визуализации данных, проектирования признаков, моделирования и развертывания. В этой статье описаны только моделирование и развертывание. 

### <a name="import-python-libraries"></a>Импорт библиотек Python
Чтобы запустить пример Jupyter Notebook или файл сценария Python, необходимо установить следующие пакеты Python. Если вы используете службу Notebook Машинного обучения Azure, эти пакеты уже установлены.

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random
    import sklearn
    from sklearn.linear_model import LogisticRegression
    from sklearn.cross_validation import train_test_split
    from sklearn import metrics
    from __future__ import division
    from sklearn import linear_model
    from azureml import services


### <a name="read-in-the-data-from-blob"></a>Считывание данных из большого двоичного объекта
* Строка подключения   
  
        CONTAINERNAME = 'test1'
        STORAGEACCOUNTNAME = 'XXXXXXXXX'
        STORAGEACCOUNTKEY = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYY'
        BLOBNAME = 'demo_ex_9_stratified_1_1000_copy.csv'
        blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
* Считайте данные в качестве текста:
  
        t1 = time.time()
        data = blob_service.get_blob_to_text(CONTAINERNAME,BLOBNAME).split("\n")
        t2 = time.time()
        print(("It takes %s seconds to read in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/data-lake-walkthrough/17-python_readin_csv.PNG)    
* Добавьте имена столбцов и отделите столбцы:
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* Измените значения в некоторых столбцах на числовые:
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a>Создание моделей машинного обучения
В этом разделе вы создадите модель двоичной классификации, чтобы спрогнозировать вероятность получения чаевых за поездку. В Jupyter Notebook можно найти две другие модели: многоклассовой классификации и регрессии.

* Сначала вам следует создать фиктивные переменные, которые можно использовать в моделях scikit-learn:
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* Создайте кадр данных для моделирования:
  
        cols_to_keep = ['tipped', 'trip_distance', 'passenger_count']
        data = df1[cols_to_keep].join([df1_payment_type_dummy,df1_vendor_id_dummy])
  
        X = data.iloc[:,1:]
        Y = data.tipped
* Обучите и протестируйте разбиение на 60/40:
  
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.4, random_state=0)
* Получите логистическую регрессию в обучающем наборе:
  
        model = LogisticRegression()
        logit_fit = model.fit(X_train, Y_train)
        print ('Coefficients: \n', logit_fit.coef_)
        Y_train_pred = logit_fit.predict(X_train)
  
       ![c1](./media/data-lake-walkthrough/c1-py-logit-coefficient.PNG)
* Оцените тестируемый набор данных:
  
        Y_test_pred = logit_fit.predict(X_test)
* Выполните вычисление метрик оценки:
  
        fpr_train, tpr_train, thresholds_train = metrics.roc_curve(Y_train, Y_train_pred)
        print fpr_train, tpr_train, thresholds_train
  
        fpr_test, tpr_test, thresholds_test = metrics.roc_curve(Y_test, Y_test_pred) 
        print fpr_test, tpr_test, thresholds_test
  
        #AUC
        print metrics.auc(fpr_train,tpr_train)
        print metrics.auc(fpr_test,tpr_test)
  
        #Confusion Matrix
        print metrics.confusion_matrix(Y_train,Y_train_pred)
        print metrics.confusion_matrix(Y_test,Y_test_pred)
  
       ![c2](./media/data-lake-walkthrough/c2-py-logit-evaluation.PNG)

### <a name="build-web-service-api-and-consume-it-in-python"></a>Создание API веб-службы и его использование в Python
Когда вы завершите создание модели машинного обучения, ее можно ввести в эксплуатацию. В качестве примера используется двоичная логистическая модель. Убедитесь, что на локальном компьютере установлена версия scikit-learn 0.15.1. Если вы используете службу Студии машинного обучения Microsoft Azure, этого делать не нужно.

* Найдите учетные данные своей рабочей области в настройках Студии машинного обучения Microsoft Azure. В Студии машинного обучения Azure выберите **Параметры** --> **Имя** --> **Authorization Tokens** (Маркеры авторизации). 
  
    ![c3](./media/data-lake-walkthrough/c3-workspace-id.PNG)

        workspaceid = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'

* Создайте веб-службу:
  
        @services.publish(workspaceid, auth_token) 
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float, payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(int) #0, or 1
        def predictNYCTAXI(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            inputArray = [trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH, payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS]
            return logit_fit.predict(inputArray)
* Получите учетные данные веб-службы:
  
        url = predictNYCTAXI.service.url
        api_key =  predictNYCTAXI.service.api_key
  
        print url
        print api_key
  
        @services.service(url, api_key)
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float,payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(float)
        def NYCTAXIPredictor(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            pass
* Вызовите API веб-службы. После выполнения предыдущего шага нужно будет подождать 5–10 секунд.
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a>Вариант 2. Создание и развертывание моделей прямо в Машинном обучении Azure
Студия машинного обучения Azure может считывать данные прямо из хранилища озера данных Azure, а затем использоваться для создания и развертывания моделей. Этот подход использует таблицу Hive, которая указывает на хранилище озера данных Azure. Для этого необходимо подготовить отдельный кластер Azure HDInsight, а в нем создать таблицу Hive. В следующих разделах показано, как это сделать. 

### <a name="create-an-hdinsight-linux-cluster"></a>Создание кластера HDInsight на платформе Linux
Создайте кластер HDInsight (Linux) с помощью [портала Azure](http://portal.azure.com). Дополнительные сведения см. в разделе о **создании кластера Azure HDInsight с доступом к Azure Data Lake Store** в статье [Создание кластеров HDInsight, использующих Data Lake Store, с помощью портала Azure](../../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

 ![18](./media/data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a>Создание таблицы Hive в HDInsight
Теперь создайте в кластере HDInsight таблицы Hive для Студии машинного обучения Azure, используя данные из Azure Data Lake Store, сохраненные на предыдущем шаге. Перейдите к новому кластеру HDInsight. Выберите **Параметры** --> **Свойства** --> **Удостоверение кластера AAD** --> **ADLS Access** (Доступ ADLS), убедитесь, что учетная запись Azure Data Lake Store добавлена в список и есть права на чтение, запись и выполнение. 

 ![19](./media/data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

Щелкните **Панель мониторинга** рядом с кнопкой **Параметры**. Откроется новое окно. Щелкните **Представление Hive** в правом верхнем углу страницы, чтобы открыть **Редактор запросов**.

 ![20](./media/data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

Вставьте следующие сценарии Hive, чтобы создать таблицу. Источник данных находится в ссылке на Azure Data Lake Store в таком формате: **adl://data_lake_store_name.azuredatalakestore.net:443/имя_папки/имя_файла**.

    CREATE EXTERNAL TABLE nyc_stratified_sample
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string,
      payment_type string,
      fare_amount string,
      surcharge string,
      mta_tax string,
      tolls_amount string,
      total_amount string,
      tip_amount string,
      tipped string,
      tip_class string,
      rownum string
      )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    LOCATION 'adl://data_lake_storage_name.azuredatalakestore.net:443/nyctaxi_folder/demo_ex_9_stratified_1_1000_copy.csv';


После выполнения запроса отобразятся такие результаты:

 ![22](./media/data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a>Создание и развертывание моделей в Студии машинного обучения Azure
Теперь вы готовы создать и развернуть в службе "Машинное обучение Microsoft Azure" модель, которая прогнозирует выплату чаевых. Данные стратифицированной выборки готовы к использованию в этой задаче двоичной классификации (поездка с чаевыми или без чаевых). Также в Студии машинного обучения Microsoft Azure можно создать и развернуть прогнозные модели, использующие многоклассовую классификацию (tip_class) и регрессию (tip_amount). Здесь мы продемонстрировали только применение модели двоичной классификации.

1. Загрузите данные в Машинное обучение Azure, используя модуль **Импорт данных**, доступный в разделе **Ввод и вывод данных**. Дополнительные сведения см. на странице справки [Импорт данных](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/).
2. Выберите значение **Hive Query** (Запрос Hive) для параметра **Источник данных** на панели **Свойства**.
3. Вставьте следующий сценарий Hive в редактор **Hive database query** (Запрос к базе данных Hive):
   
        select * from nyc_stratified_sample;
4. Введите универсальный код ресурса (URI) кластера HDInsight (его можно найти на портале Azure), учетные данные Hadoop, расположение выходных данных и имя контейнера, ключа или учетной записи хранения Azure.
   
   ![23](./media/data-lake-walkthrough/23-reader-module-v3.PNG)  

На следующем рисунке показан пример эксперимента по двоичной классификации, связанного с считыванием данных из таблицы Hive.

 ![24](./media/data-lake-walkthrough/24-AML-exp.PNG)

После создания эксперимента выберите **Set Up Web Service** -->  (Настройка веб-службы) **Predictive Web Service** (Прогнозная веб-служба).

 ![25](./media/data-lake-walkthrough/25-AML-exp-deploy.PNG)

Запустите автоматически созданный оценивающий эксперимент, а по его завершении нажмите кнопку **Deploy Web Service**

 ![26](./media/data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

Вскоре появится панель мониторинга веб-службы:

 ![27](./media/data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a>Сводка
После завершения этого пошагового руководства у вас будет создана среда анализа данных для создания всеобъемлющих масштабируемых решений озера данных Azure. Эта среда использовалась для анализа большого набора данных, в отношении которого выполнены ключевые шаги по обработке данных — от получения данных и обучения модели до развертывания модели в качестве веб-службы. Язык U-SQL использовался для обработки, просмотра и выборки данных. Python и Hive использовались со студией машинного обучения Azure для создания и развертывания прогнозных моделей.

## <a name="whats-next"></a>Что дальше?
Схема обучения для [процесса обработки и анализа данных группы (TDSP)](http://aka.ms/datascienceprocess) содержит ссылки на разделы, описывающие каждый шаг в процессе расширенной аналитики. Существует ряд пошаговых руководств, упорядоченных на странице [Пошаговые руководства по процессу обработки и анализа данных](walkthroughs.md) , которые демонстрируют, как использовать ресурсы и службы в различных сценариях прогнозной аналитики.

* [Процесс обработки и анализа данных группы на практике: использование хранилища данных SQL](sqldw-walkthrough.md)
* [Процесс обработки и анализа данных группы на практике: использование кластеров HDInsight Hadoop](hive-walkthrough.md)
* [Процесс обработки и анализа данных группы на практике: использование SQL Server](sql-walkthrough.md)
* [Общие сведения об обработке и анализе данных с помощью платформы Spark в Azure HDInsight](spark-overview.md)
