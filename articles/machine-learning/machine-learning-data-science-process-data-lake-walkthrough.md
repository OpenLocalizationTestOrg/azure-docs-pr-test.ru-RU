---
title: "Полное пошаговое руководство по масштабируемому анализу данных с помощью Azure Data Lake | Документация Майкрософт"
description: "Как toouse Озера данных Azure toodo исследования и двоичной классификации данных задач для набора данных."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 91a8207f-1e57-4570-b7fc-7c5fa858ffeb
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: bradsev;weig
ms.openlocfilehash: 8b05457ae7045a7aaed350a7502469f2247161e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a>Полное пошаговое руководство по масштабируемому анализу данных с помощью Azure Data Lake
В этом пошаговом руководстве показано, как просмотр данных toodo toouse Озера данных Azure и задачи двоичной классификации образца hello NYC такси маршрута и тариф авиакомпании toopredict набора данных независимо от того, имеется ли подсказка будет оплачиваться тариф авиакомпании. Он поможет выполнить шаги hello hello [командного процесса обработки и анализа данных](http://aka.ms/datascienceprocess), узел узел, из данных приобретения toomodel обучения, а затем toohello развертывания веб-службы, которая публикует модели hello.

### <a name="azure-data-lake-analytics"></a>Аналитика озера данных Azure
Hello [Озера данных Microsoft Azure](https://azure.microsoft.com/solutions/data-lake/) имеет все необходимые toomake возможности hello легко toostore специалистами по анализу данных любого размера, формы и скорость и tooconduct обработки данных, advanced analytics и моделирования машины обучения с высокой масштабируемостью экономичным способом.   Плата взимается за задание, и только если данные обработаны фактически. Azure аналитики Озера данных включает U-SQL, язык, что переходы hello декларативной природы SQL с hello выразительных возможностей C# tooprovide масштабируемой распределенного запроса возможностей. Благодаря этому можно tooprocess неструктурированные данные, применив схему на чтение, вставка пользовательской логики и определяемые пользователем функции (UDF) и включает расширения tooenable нормально точный контроль над тем, как tooexecute в масштабе. toolearn Дополнительные сведения о принципы разработки hello за U-SQL, в разделе [блоге Visual Studio](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).

Аналитика озера данных — это также ключевая часть Cortana Analytics Suite. Она поддерживает работу с хранилищем данных SQL Azure, Power BI и фабрикой данных. Это создает всеобъемлющую облачную платформу для работы с большими данными и углубленной аналитики.

В этом пошаговом руководстве начинается с описания hello необходимые компоненты и ресурсы, необходимые toocomplete hello задач с помощью аналитики Озера данных этой формы процесса обработки и анализа данных hello и каким образом tooinstall их. Затем оно описано hello обработки данных с помощью U-SQL и завершается, показывая, как toouse Python и Hive с toobuild студии машинного обучения Azure и развернуть hello прогнозных моделей. 

### <a name="u-sql-and-visual-studio"></a>U-SQL и Visual Studio
Рекомендуется использовать Visual Studio tooedit U-SQL скрипты tooprocess hello набора данных. сценарии Hello U-SQL описаны здесь и в отдельном файле. процесс Hello включает обработки, просмотра и выборки данных hello. Здесь также показано, как toorun U-SQL в скрипт задание из hello портал Azure. Куст таблицы создаются для hello данных в связанных HDInsight кластера toofacilitate hello построение и развертывание модели двоичной классификации в студии машинного обучения Azure.  

### <a name="python"></a>Python
В этом пошаговом руководстве также содержит раздел, описывающий, каким образом toobuild и развертывание прогнозную модель с помощью Python с студии машинного обучения Azure.  Мы предоставляем записной книжке Jupyter hello Python скрипты для этих шагов в этом процессе. ноутбук Hello включает код некоторые этапы проектирования дополнительных компонентов и построения моделей, например мультиклассовой классификации и регрессии, кроме моделирования toohello модель двоичной классификации, описанную. Задача Hello регрессии — toopredict hello объем hello подсказки на основе других функций подсказки. 

### <a name="azure-machine-learning"></a>Машинное обучение Azure
Студия машинного обучения используется toobuild и разверните hello прогнозных моделей. Для этого используется два подхода: первый — с помощью сценариев Python, а второй — с использованием таблиц Hive на кластере HDInsight (Hadoop).

### <a name="scripts"></a>Сценарии
В этом пошаговом руководстве описаны только основные шаги hello. Вы можете скачать полный hello **скрипт U-SQL** и **книжке Jupyter** из [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).

## <a name="prerequisites"></a>Предварительные требования
Прежде чем начать эти разделы, необходимо иметь следующие hello.

* Подписка Azure. Если у вас ее нет, см. статью [о получении бесплатной пробной версии Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* [Рекомендуется] Visual Studio 2013 или более поздней версии. Если вы еще не установили одну из этих версий, можно скачать бесплатную версию Community с сайта [Visual Studio Community](https://www.visualstudio.com/vs/community/).

> [!NOTE]
> Вместо Visual Studio также можно использовать запросы Озера данных Azure toosubmit портала Azure hello. Корпорация Майкрософт предоставляет инструкции о том, как toodo так как с помощью Visual Studio, так и на портале hello в разделе "hello" под названием **обработки данных с помощью U-SQL**. 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a>Подготовка среды анализа данных для озера данных Azure
среда обработки и анализа данных tooprepare hello в данном пошаговом руководстве создайте hello следующие ресурсы:

* хранилище озера данных Azure; 
* Аналитику озера данных Azure;
* учетную запись хранения BLOB-объектов;
* учетную запись Студии машинного обучения Azure;
* средства озера данных Azure для Visual Studio (рекомендуется).

Этот раздел содержит инструкции о том, как toocreate каждого из этих ресурсов. Если выбрать toouse Hive таблиц с помощью машинного обучения Azure, вместо Python, toobuild модели, необходимо также tooprovision кластер HDInsight (Hadoop). Альтернативные процедура, описанная в описанной в соответствующем разделе hello ниже.


> [!NOTE]
> Hello **хранилища Озера данных Azure** могут создаваться либо отдельно, либо при создании hello **аналитики Озера данных Azure** хранения по умолчанию hello. Для создания каждого из этих ресурсов отдельно ниже ссылаются инструкции, но hello учетной записи хранилища Озера данных не должны создаваться отдельно.
>
> 

### <a name="create-an-azure-data-lake-store"></a>Создание хранилища озера данных Azure


Создать из hello ADLS [портала Azure](http://portal.azure.com). Дополнительные сведения см. в статье [Создание кластера HDInsight с Data Lake Store с помощью портала Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md). Быть убедиться, что tooset копирование hello удостоверение кластера AAD в hello **DataSource** колонке hello **необязательная конфигурация** колонке описано существует. 

 ![3](./media/machine-learning-data-science-process-data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a>Создание учетной записи Аналитики озера данных Azure
Создайте учетную запись ADLA из hello [портала Azure](http://portal.azure.com). Дополнительные сведения см. в статье [Руководство. Начало работы с Azure Data Lake Analytics с помощью портала Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md). 

 ![4](./media/machine-learning-data-science-process-data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a>Создание учетной записи хранения BLOB-объектов Azure
Создать учетную запись службы хранилища больших двоичных объектов Azure из hello [портала Azure](http://portal.azure.com). Дополнительные сведения см. в разделе hello создать учетную запись хранилища раздела [учетных записей хранилища Azure о](../storage/common/storage-create-storage-account.md).

 ![5](./media/machine-learning-data-science-process-data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a>Настройка учетной записи Студии машинного обучения Azure
Войти в студию машинного обучения Azure из hello [машинного обучения Azure](https://azure.microsoft.com/services/machine-learning/) страницы. Щелкните hello **начните** кнопку и выберите «Бесплатную рабочую область» или «Стандартные рабочую область». После этого можно будет toocreate экспериментов в Azure ML Studio.  

### <a name="install-azure-data-lake-tools-recommended"></a>Установка инструментов озера данных Azure [рекомендуется]
Установите инструменты озера данных Azure в зависимости от своей версии Visual Studio со страницы [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504)(Инструменты озера данных Azure для Visual Studio).

 ![6](./media/machine-learning-data-science-process-data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

После успешного завершения установки hello, откройте Visual Studio. Вы увидите hello Озера данных вкладке hello меню вверху hello. Ресурсы Azure должны появиться в левой панели hello при входе в учетную запись Azure.

 ![7](./media/machine-learning-data-science-process-data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="hello-nyc-taxi-trips-dataset"></a>набор Hello NYC такси приема-передачи данных
Hello набора данных, мы использовали здесь является общедоступным набор данных — hello [NYC такси приема-передачи набора данных](http://www.andresmh.com/nyctaxitrips/). Hello NYC такси обработки данных состоит из примерно 20 ГБ сжатые файлы CSV (~ 48 ГБ несжатого), запись более миллиона 173 отдельных приема-передачи и hello цен платная для каждого маршрута. Каждая запись маршрута включает hello раскладки и истощение расположений и времени, анонимен hack номер лицензии (драйвер) и hello номер medallion (уникальный идентификатор элемента такси). данные Hello охватывает все приема-передачи в 2013 году, hello и предоставляется в следующих двух наборов данных для каждого месяца hello:

* Hello «trip_data» CSV содержит обработки таких сведений, как количество пассажиров, раскладки и dropoff точек, длительность обработки и длина пути. Вот несколько примеров записей:
  
       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count, trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
* Здравствуйте, trip_fare CSV содержит подробные сведения о тариф авиакомпании hello платная для каждого маршрута, например тип платежа, сумма тариф авиакомпании, излишнюю нагрузку налоги, советы и тарифы и hello общей оплаты. Вот несколько примеров записей:
  
       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Hello trip уникальных ключей toojoin\_данных и обработки\_тариф авиакомпании состоит из следующих трех полей hello: medallion hack\_лицензии и раскладки\_даты и времени. Hello необработанные CSV-файлов может осуществляться из большой двоичный объект открытого хранилища Azure. Здравствуйте скрипт U-SQL для этого соединения находятся в hello [соединения таблиц маршрута и тариф авиакомпании](#join) раздела.

## <a name="process-data-with-u-sql"></a>Обработка данных с использованием U-SQL
Hello задач обработки данных, приведенных в этом разделе включают передаче, проверка качества, исследование и выборки данных hello. Мы также показано, как toojoin маршрута и тариф авиакомпании таблицы. Последний сегмент Hello показывает выполнения созданное задание U-SQL из hello портал Azure. Ниже приведены ссылки tooeach подраздела.

* [Прием данных: чтение из общедоступного большого двоичного объекта](#ingest)
* [Проверка качества данных](#quality)
* [Исследование данных](#explore)
* [Объединение таблиц trip и fare](#join)
* [Выборка данных](#sample)
* [Выполнение заданий U-SQL](#run)

сценарии Hello U-SQL описаны здесь и в отдельном файле. Вы можете скачать полный hello **U-SQL скрипты** из [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).

tooexecute U-SQL, откройте Visual Studio, нажмите кнопку **файл--> Создать проект-->**, выберите **проекта U-SQL**, имя и сохранить его в папку tooa.

![8](./media/machine-learning-data-science-process-data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> Это возможно toouse hello портала Azure tooexecute U-SQL вместо Visual Studio. Можно переходить toohello ресурсов аналитики Озера данных Azure на портале hello и отправлять запросы напрямую, как показано в следующий рисунок hello.
> 
> 

![9](./media/machine-learning-data-science-process-data-lake-walkthrough/9-portal-submit-job.PNG)

### <a name="ingest"></a>Прием данных: чтение из общедоступного большого двоичного объекта
Hello расположение данных hello в hello BLOB-объектов Azure есть ссылки как  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**  и можно извлечь при помощи **Extractors.Csv()**. Замените имя контейнера и имя учетной записи хранения в следующем сценарии для container_name@blob_storage_account_name в адресе wasb hello. Поскольку имена файлов hello в одном формате, можно использовать **trip\_data_ {\*\}.csv** tooread во всех файлах 12 маршрута. 

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

Так как существуют заголовки в первой строке hello, мы должны tooremove hello заголовки и изменить типы столбцов в соответствующие столбцы. Мы можем либо сохранить hello обработки данных tooAzure хранилища Озера данных с помощью **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ или tooAzure хранилища BLOB-объектов учетной записи с помощью  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** . 

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

    ////output data tooADL
    OUTPUT @trip   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data tooblob
    OUTPUT @trip   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

Аналогичным образом мы чтения в наборах данных тариф авиакомпании hello. Щелкните правой кнопкой мыши хранилища Озера данных Azure, вы можете toolook данные в **портала Azure--> обозреватель данных** или **проводнике** в среде Visual Studio. 

 ![10](./media/machine-learning-data-science-process-data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/machine-learning-data-science-process-data-lake-walkthrough/11-data-in-ADL.PNG)

### <a name="quality"></a>Проверка качества данных
После считывания маршрута и тариф авиакомпании таблиц в проверок качества данных может осуществляться в hello следующими способами. Hello, возникающие в CSV-файлы могут быть хранилища больших двоичных объектов tooAzure выходных данных или хранилища Озера данных Azure. 

Найти число hello medallions и уникальный номер medallions:

    ///check hello number of medallions and unique number of medallions
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
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
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
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

Найдите записи, недопустимые в отношении pickup_longitude:

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
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
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <a name="explore"></a>Просмотр данных
Мы можем некоторые tooget исследования данных лучше понять hello данных.

Найти распространения hello скошенные и не чаевых оставил зависимости приема-передачи данных:

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
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

Найти hello распределение суммы подсказка со значениями среза: 0,5,10 и 20 долларов.

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
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
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
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

Найти процентилем hello trip расстояния:

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
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

    //// output tooblob
    OUTPUT @model_data_full   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data tooADL
    OUTPUT @model_data_full   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


Для каждого уровня пассажира число рассчитайте hello количество записей, среднюю сумму чаевых, дисперсия суммы совет, процент скошенные приема-передачи данных.

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
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <a name="sample"></a>Выборка данных
Сначала мы случайным образом выбрать 0,1% hello данных из hello соединяемую таблицу:

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
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

Затем мы выполним стратифицированную выборку по двоичной переменной tip_class:

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output tooblob
    OUTPUT @model_data_stratified_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data tooADL
    OUTPUT @model_data_stratified_sample_1_1000   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <a name="run"></a>Выполнение заданий U-SQL
После завершения редактирования скриптов U-SQL, вы можете отправить их toohello сервера с помощью учетной записи аналитики Озера данных Azure. Выберите вкладку **Data Lake**, щелкните **Отправить задание**, а затем выберите свою учетную запись в поле **Analytics Account** (Учетная запись Аналитики), значение параметра **Параллелизм** и нажмите кнопку **Отправить**.  

 ![12](./media/machine-learning-data-science-process-data-lake-walkthrough/12-submit-USQL.PNG)

Когда успешно проверьте соответствие задания hello hello состояние задания отображается в Visual Studio для наблюдения. После завершения задания hello, вы можете даже воспроизведения hello задания процесс выполнения и узнать hello возникать узкие места действия tooimprove эффективность работы. Вы можете перейти tooAzure портала toocheck hello состояния заданий U-SQL.

 ![13.](./media/machine-learning-data-science-process-data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/machine-learning-data-science-process-data-lake-walkthrough/14-USQL-jobs-portal.PNG)

Теперь можно проверить hello выходные файлы в хранилище больших двоичных объектов Azure или портала Azure. Мы используем данные образца hello стратифицированным для наших моделирования в следующем шаге hello.

 ![15](./media/machine-learning-data-science-process-data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/machine-learning-data-science-process-data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a>Создание и развертывание моделей в Машинном обучении Azure
Продемонстрированы два параметра, доступные для вас данных toopull в toobuild машинного обучения Azure и 

* В hello первый вариант — использовать hello выборки данных, написанных tooan больших двоичных объектов Azure (в hello **выборки данных** шага выше) и использовать Python toobuild и развертывания модели на основе машинного обучения Azure. 
* В случае второй hello запрос hello данных Озера данных Azure непосредственно с помощью запроса Hive. Этот параметр требует создания нового кластера HDInsight или использовать существующий кластер HDInsight, где hello Hive таблиц данных такси NY toohello точки в хранилище Озера данных Azure.  Мы рассмотрим оба варианта ниже. 

## <a name="option-1-use-python-toobuild-and-deploy-machine-learning-models"></a>Вариант 1: Использование Python toobuild и развертывания моделей машинного обучения
toobuild и развертывания моделей машинного обучения с помощью Python, создайте записной книжке Jupyter на локальном компьютере или в студии машинного обучения Azure. Hello книжке Jupyter представленные на [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) содержит Здравствуйте tooexplore весь код, визуализация данных, конструируются, моделирования и развертывания. В этой статье показано, просто hello моделирования и развертывания. 

### <a name="import-python-libraries"></a>Импорт библиотек Python
В порядке toorun hello образец книжке Jupyter или Здравствуйте файл сценария Python, hello Python требуются следующие пакеты. При использовании hello записной книжки AzureML службы были установлены эти пакеты.

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


### <a name="read-in-hello-data-from-blob"></a>Чтение данных hello из большого двоичного объекта
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
        print(("It takes %s seconds tooread in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/machine-learning-data-science-process-data-lake-walkthrough/17-python_readin_csv.PNG)    
* Добавьте имена столбцов и отделите столбцы:
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* Изменить некоторые столбцы toonumeric
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a>Создание моделей машинного обучения
Здесь мы создаем модель двоичной классификации toopredict ли trip Подрезанный, или нет. В записной книжке Jupyter hello можно найти другие две модели: мультиклассовой классификации и моделями регрессии.

* Сначала мы должны toocreate фиктивный переменные, которые могут использоваться в scikit-узнать моделей
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* Создайте кадр данных для моделирования hello
  
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
  
       ![c1](./media/machine-learning-data-science-process-data-lake-walkthrough/c1-py-logit-coefficient.PNG)
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
  
       ![c2](./media/machine-learning-data-science-process-data-lake-walkthrough/c2-py-logit-evaluation.PNG)

### <a name="build-web-service-api-and-consume-it-in-python"></a>Создание API веб-службы и его использование в Python
Мы хотим toooperationalize hello модели машинного обучения после его построения. Здесь в качестве примера мы используем двоичная модель логистической hello. Убедитесь, что scikit hello-сведения о версии в локальном компьютере 0.15.1. Не нужно tooworry об этом при использовании службы Azure ML studio.

* Найдите учетные данные своей рабочей области в настройках Студии машинного обучения Microsoft Azure. В Студии машинного обучения Azure выберите **Параметры** --> **Имя** --> **Authorization Tokens** (Маркеры авторизации). 
  
    ![c3](./media/machine-learning-data-science-process-data-lake-walkthrough/c3-workspace-id.PNG)

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
* Вызовите API веб-службы. У вас есть toowait 5-10 секунд после выполнения предыдущего шага hello.
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/machine-learning-data-science-process-data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a>Вариант 2. Создание и развертывание моделей прямо в Машинном обучении Azure
Студия машинного обучения можно считывать данные непосредственно из хранилища Озера данных Azure и используется toocreate и развертывания моделей. Этот подход использует таблицу Hive, которая указывает на hello хранилища Озера данных Azure. Для этого необходимо подготовить отдельный кластер Azure HDInsight, на какие hello Hive создается таблица. Здравствуйте, следующие разделы Показать как toodo это. 

### <a name="create-an-hdinsight-linux-cluster"></a>Создание кластера HDInsight на платформе Linux
Создание кластера HDInsight (Linux) из hello [портала Azure](http://portal.azure.com). Дополнительные сведения см. в разделе hello **создать кластер HDInsight с tooAzure доступа хранилища Озера данных** статьи [создать кластер HDInsight в хранилище Озера данных с помощью портала Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

 ![18](./media/machine-learning-data-science-process-data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a>Создание таблицы Hive в HDInsight
Теперь создадим toobe таблицы Hive используется в студии машинного обучения Azure в кластере HDInsight hello на hello данные, хранящиеся в хранилище Озера данных Azure hello предыдущего шага. Go toohello только что созданный кластер HDInsight. Нажмите кнопку **параметры** --> **свойства** --> **кластера удостоверений AAD** --> **доступом ADLS**, Убедитесь, что учетная запись хранилища Озера данных Azure добавляется в список hello чтение, запись и выполнение права. 

 ![19](./media/machine-learning-data-science-process-data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

Нажмите кнопку **мониторинга** Далее toohello **параметры** кнопка и окно появится всплывающее окно. Нажмите кнопку **Hive представление** в hello в правом верхнем углу страницы приветствия и вы увидите hello **редактора запросов**.

 ![20](./media/machine-learning-data-science-process-data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/machine-learning-data-science-process-data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

Вставьте следующие toocreate скрипты Hive hello таблицы. Hello источник данных находится в хранилище Озера данных Azure ссылке таким образом: **adl://data_lake_store_name.azuredatalakestore.net:443/имя_папки/имя_файла**.

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


По завершении выполнения запроса hello вы увидите результаты hello следующим образом:

 ![22](./media/machine-learning-data-science-process-data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a>Создание и развертывание моделей в Студии машинного обучения Azure
Мы теперь готовы toobuild и развернуть модель, которая прогнозирует, оплачивается ли подсказка с машинного обучения Azure. Hello стратифицированной выборки данных будет готова toobe, используемых в этой двоичной классификации (Совет или нет) проблему. Здравствуйте, прогнозных моделей мультиклассовой классификации (tip_class) с помощью регрессии (tip_amount) можно также следует создавать и развертывать с студии машинного обучения Azure, а здесь только показано, как с помощью варианта toohandle hello hello модель двоичной классификации.

1. Получение данных hello в Azure ML с помощью hello **импорта данных** модуля, доступные в hello **ввод и вывод данных** раздела. Дополнительные сведения см. в разделе hello [модуль импорта данных](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) справочной странице.
2. Выберите **запроса Hive** как hello **источника данных** в hello **свойства** панель.
3. Следующий скрипт Hive в hello hello вставить **запроса базы данных Hive** редактора
   
        select * from nyc_stratified_sample;
4. Введите hello URI HDInsight кластера (это можно найти на портале Azure), учетные данные Hadoop, расположение выходных данных и имя контейнера или ключа и имени учетной записи хранилища Azure.
   
   ![23](./media/machine-learning-data-science-process-data-lake-walkthrough/23-reader-module-v3.PNG)  

Пример эксперимента двоичной классификации, чтение данных из таблицы Hive показан в приведенном ниже рисунке hello.

 ![24](./media/machine-learning-data-science-process-data-lake-walkthrough/24-AML-exp.PNG)

После создания эксперимента hello щелкните **настройки веб-службы** --> **прогнозной веб-службы**

 ![25](./media/machine-learning-data-science-process-data-lake-walkthrough/25-AML-exp-deploy.PNG)

Оценки экспериментов, по окончании нажмите кнопку выполнения hello автоматически создается **развертывание веб-службы**

 ![26](./media/machine-learning-data-science-process-data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

скоро будет отображаться Hello мониторинга веб-службы:

 ![27](./media/machine-learning-data-science-process-data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a>Сводка
После завершения этого пошагового руководства у вас будет создана среда анализа данных для создания всеобъемлющих масштабируемых решений озера данных Azure. Эта среда была используется tooanalyze большого открытого набора данных, сделав hello канонические шагов по hello процесса обработки и анализа данных, от получения данных через Обучение модели и развертывания toohello hello моделирование веб-службы. U-SQL была используется tooprocess, исследовать и образец hello данных. Python и Hive использовались в студии машинного обучения Azure toobuild и развернуть прогнозных моделей.

## <a name="whats-next"></a>Что дальше?
Схема обучения для Hello [процесса обработки и анализа данных Team (TDSP)](http://aka.ms/datascienceprocess) предоставляет ссылки tootopics описание каждого шага в hello advanced analytics процесса. Существует ряд пошаговых руководств, перечислено на hello [пошаговые руководства процесса обработки и анализа данных командного](data-science-process-walkthroughs.md) как страница этой демонстрации toouse ресурсов и служб в различных сценариях прогнозной аналитики:

* [Hello командного процесса обработки и анализа данных в действии: с помощью хранилища данных SQL](machine-learning-data-science-process-sqldw-walkthrough.md)
* [Hello командного процесса обработки и анализа данных в действии: с использованием кластеров HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md)
* [Hello командного процесса обработки и анализа данных: с помощью SQL Server](machine-learning-data-science-process-sql-walkthrough.md)
* [Общие сведения об использовании процесса обработки и анализа данных hello усилить на Azure HDInsight](machine-learning-data-science-spark-overview.md)

