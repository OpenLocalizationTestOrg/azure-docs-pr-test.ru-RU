---
title: "aaaBuild и развернуть модель машинного обучения, с помощью SQL Server на Виртуальной машине Azure | Документы Microsoft"
description: "Расширенный процесс аналитики и технологии в действии"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6066b083-262c-4453-a712-a5c05acc3df8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: fashah;bradsev
ms.openlocfilehash: 30ba9a9e3cf65f75015e13f9c7876dcbccc5bc47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-server"></a>Hello командного процесса обработки и анализа данных в действии: с помощью SQL Server
В этом учебнике перемещайтесь hello процесс построения и развертывания модели машинного обучения с помощью SQL Server и общедоступным набор данных — hello [NYC такси приема-передачи](http://www.andresmh.com/nyctaxitrips/) набора данных. рабочий процесс обработки и анализа данных, ниже представлена процедура Hello: приема и исследовать данные hello, проектировать возможности toofacilitate обучения, а затем построения и развертывания модели.

## <a name="dataset"></a>Описание набора данных "Поездки такси Нью-Йорка"
Hello Trip такси NYC данных составляет около 20 ГБ сжатые файлы CSV (~ 48 ГБ несжатого), включающего в себя более миллиона 173 отдельных приема-передачи и hello цен платная для каждого маршрута. Каждая запись маршрута включает hello раскладки и истощение место и время, анонимные hack (драйвер) номер лицензии и medallion (уникальный идентификатор элемента такси) номер. данные Hello охватывает все приема-передачи в 2013 году, hello и предоставляется в следующих двух наборов данных для каждого месяца hello:

1. Hello «trip_data» CSV содержит обработки таких сведений, как количество пассажиров, раскладки и dropoff точек, длительность обработки и длина пути. Вот несколько примеров записей:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. Здравствуйте, trip_fare CSV содержит подробные сведения о тариф авиакомпании hello платная для каждого маршрута, например тип платежа, сумма тариф авиакомпании, излишнюю нагрузку налоги, советы и тарифы и hello общей оплаты. Вот несколько примеров записей:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Hello trip уникальных ключей toojoin\_данных и обработки\_тариф авиакомпании состоит из полей hello: medallion hack\_лицензии и раскладки\_даты и времени.

## <a name="mltasks"></a>Примеры задач прогнозирования
Мы сможет сформулировать три прогноза проблемы с учетом hello *совет\_сумма*, а именно:

1. Двоичная классификация. Позволяет спрогнозировать, были ли оставлены чаевые после поездки, т. е. значение *tip\_amount* > 0 $ — это положительный пример, а значение *tip\_amount* = 0 $ — отрицательный пример.
2. Мультиклассовая классификация: диапазон hello toopredict подсказки оплаты hello trip. Разделен hello *совет\_сумма* в пять ячеек или классы:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. Задача регрессии: оплачена сумма hello toopredict подсказки для маршрута.  

## <a name="setup"></a>Установка hello данных Azure обработки и анализа среды для расширенной аналитики
Как видно из hello [планирование среды](machine-learning-data-science-plan-your-environment.md) руководства, существует несколько вариантов toowork с набором данных приема-передачи такси NYC hello в Azure:

* Работать с данным hello в BLOB-объекты Azure, а затем модель в машинном обучении Azure
* Загрузка данных hello в базе данных SQL Server, а затем модель в машинном обучении Azure

В этом учебнике мы покажем, параллельный массовый импорт tooa hello данных SQL Server, просмотра данных, функция проектирование и работу выборки с помощью SQL Server Management Studio, а также с помощью ноутбук IPython. [Примеры скриптов](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) и файлы [IPython Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) предоставлены в общий доступ на GitHub. Toowork записной книжки образец IPython с данными hello в BLOB-объекты Azure доступен также в hello местоположения.

tooset настройку среды обработки и анализа данных Azure:

1. [создать учетную запись хранения;](../storage/common/storage-create-storage-account.md)
2. [Создание рабочей области машинного обучения Azure](machine-learning-create-workspace.md)
3. [Подготовьте виртуальную машину для обработки и анализа данных](machine-learning-data-science-setup-sql-server-virtual-machine.md), которая будет служить сервером SQL Server и сервером IPython Notebook.
   
   > [!NOTE]
   > Примеры сценариев Hello и IPython Notebook будет загруженный tooyour обработки и анализа данных виртуальной машины во время процесса установки hello. По завершении hello ВМ после установки скрипт hello образцы будут в библиотеке документов Виртуальной машины:  
   > 
   > * Примеры сценариев: `C:\Users\<user_name>\Documents\Data Science Scripts`  
   > * Примеры IPython Notebook: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`  
   >   where `<user_name>` является именем для входа Windows виртуальной машины. Мы будем называть папки образца toohello **примеры сценариев** и **ноутбуков IPython пример**.
   > 
   > 

На основании hello размер набора данных, расположение источника данных и hello выбранного Azure целевой среды, этот случай похож слишком[сценарий \#5: больших наборов данных в локальных файлах, целевой сервер SQL Server в виртуальной Машине Azure](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).

## <a name="getdata"></a>Получить hello данных из открытых источника
tooget hello [NYC такси приема-передачи](http://www.andresmh.com/nyctaxitrips/) набора данных из открытых расположения можно использовать любую из hello методов, описанных в [tooand перемещение данных из хранилища больших двоичных объектов](machine-learning-data-science-move-azure-blob.md) toocopy hello данных tooyour новой виртуальной машины.

toocopy hello данных с помощью AzCopy:

1. Войдите в tooyour виртуальной машины (VM)
2. Создать новый каталог в диска данных виртуальной Машины hello (Примечание: не используйте hello временного диска, который поставляется вместе с hello виртуальную Машину в качестве диска с данными).
3. В окне командной строки запустите hello следующей командной строкой Azcopy, заменив < path_to_data_folder > в папке данных, созданный на (2):
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    По завершении hello AzCopy всего 24 ZIP-файлы CSV (12 для обработки\_данных и 12 для обработки\_тариф авиакомпании) должны находиться в папке данных hello.
4. Распакуйте файлы загружаются hello. Обратите внимание, hello папку, где находятся файлы сжимаются hello. Эта папка будет ссылка tooas hello < путь\_для\_данные\_файлы\>.

## <a name="dbload"></a>Выполните массовый импорт данных в базу данных SQL Server
Hello производительности передачи или загрузки больших объемов данных базы данных SQL tooan и последующие запросы, может быть повышена путем использования *секционированных таблиц и представлений*. В этом разделе мы будем следовать hello инструкциям, описанным в [параллельного массового импорта с помощью SQL секционирования таблиц данных](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate новой базы данных и загрузки данных hello в секционированные таблицы в параллельном режиме.

1. Войдя в систему tooyour виртуальных Машин, запустите **SQL Server Management Studio**.
2. Подключитесь с использованием проверки подлинности Windows.
   
    ![Подключение SSMS][12]
3. Если вы еще не изменить режим проверки подлинности SQL Server hello и создать новое имя входа пользователя SQL, откройте файл скрипта hello с именем **изменить\_auth.sql** в hello **примеры сценариев** папки. Изменение hello по умолчанию имя пользователя и пароль. Нажмите кнопку **! Выполнение** в скрипте hello toorun инструментов hello.
   
    ![Выполнение сценария][13]
4. Проверка или изменение hello SQL Server по умолчанию базы данных и журнала папки tooensure, вновь создаваемых баз данных сохраняются на диск с данными. образ виртуальной Машины SQL Server Hello, оптимизированный для загрузки datawarehousing предварительно настраивается с дисками данных и журналов. Если ВМ не содержит диск данных, и добавление новых виртуальных жестких дисков во время hello процесс установки виртуальной Машины, измените папки по умолчанию hello следующим образом.
   
   * Щелкните правой кнопкой мыши имя сервера SQL Server hello в hello слева панели и нажмите кнопку **свойства**.
     
       ![Свойства сервера SQL][14]
   * Выберите **параметры базы данных** из hello **Выбор страницы** списка toohello влево.
   * Проверьте или измените hello **базы данных по умолчанию расположений** toohello **диск данных** расположения по своему усмотрению. Это местоположение новых баз данных, если при создании параметры расположения по умолчанию hello.
     
       ![База данных SQL по умолчанию][15]  
5. toocreate новую базу данных и набор toohold файловые группы hello секционированных таблиц, откройте образец скрипта hello **создания\_db\_default.sql**. Hello скрипт создает новую базу данных с именем **TaxiNYC** и 12 файловых групп в расположении данных по умолчанию hello. Каждая файловая группа будет содержать данные trip\_data и trip\_fare за один месяц. Измените имя базы данных hello, если требуется. Нажмите кнопку **! Выполнение** toorun hello скрипта.
6. Создайте две секции таблицы, один для обработки hello\_данных и другой для обработки hello\_тариф авиакомпании. Откройте образец скрипта hello **создания\_секционированных\_table.sql**, которой будет:
   
   * Создание данных hello toosplit функции секционирования по месяцам.
   * Создайте схему секционирования toomap данных каждого месяца tooa другую файловую группу.
   * Создать схему секционирования сопоставленных toohello два секционированных таблиц: **nyctaxi\_trip** будет содержать hello trip\_данных и **nyctaxi\_тариф авиакомпании** будет содержать hello trip \_успешного данных.
     
     Нажмите кнопку **! Выполнение** toorun hello скрипта и создания hello секционированных таблиц.
7. В hello **примеры сценариев** папке, есть два примера скриптов PowerShell предоставленный toodemonstrate параллельный массовый импорт данных tooSQL Server таблиц.
   
   * **BCP\_параллельных\_generic.ps1** является Универсальный сценарий tooparallel массового импорта данных в таблицу. Изменение этого сценария tooset hello входных данных и целевой переменных как указано в hello строки комментариев в скрипте hello.
   * **BCP\_параллельных\_nyctaxi.ps1** имеет предварительно настроенную версию универсального сценария hello и может принимать используется tootooload обе таблицы для hello NYC такси приема-передачи данных.  
8. Щелкните правой кнопкой мыши hello **bcp\_параллельных\_nyctaxi.ps1** имя скрипта и нажмите кнопку **изменить** tooopen в PowerShell. Просмотрите hello предустановленный набор переменных и изменить имя выбранной базы данных соответствующим tooyour, папка входных данных, целевую папку журнала и пути toohello образцы файлов форматирования **nyctaxi_trip.xml** и **nyctaxi\_ fare.XML** (в hello **примеры сценариев** папки).
   
    ![Массовый импорт данных][16]
   
    Можно также выбрать режим проверки подлинности hello, по умолчанию используется проверка подлинности Windows. Нажмите стрелку зеленый hello в toorun инструментов hello. сценарий Hello запустит 24 операций массового импорта в параллельных, 12 для каждой секционированной таблицы. Может отслеживать ход выполнения импорта данных hello путем открытия папки данных по умолчанию hello SQL Server как набор выше.
9. отчеты сценария PowerShell Hello hello времени начала и окончания. При всех массового импорта завершения, сообщается hello времени окончания. Проверьте hello журнала целевой папки tooverify, массовый импорт hello выполнено успешно, т. е., ошибки не обнаружены в папке журналов целевой hello.
10. Теперь база данных готова к просмотру, проектированию характеристик и другим операциям. Поскольку hello таблиц секционируются в соответствии с toohello **раскладки\_datetime** поле запросы, включающие **раскладки\_datetime** условия в hello  **ГДЕ** предложение будет обеспечен hello схемы секционирования.
11. В **SQL Server Management Studio**, исследовать hello предоставленный пример сценария **пример\_queries.sql**. toorun любой из запросов образец hello, hello выделение строки запроса, затем щелкните **! Выполнение** инструментов hello.
12. загружаются Hello NYC такси приема-передачи данных в двух отдельных таблицах. tooimprove операций соединения, настоятельно рекомендуется tooindex hello таблиц. Hello пример сценария **создания\_секционированных\_index.sql** создает секционированные индексы для ключа составным hello **medallion hack\_лицензии и раскладки\_datetime**.

## <a name="dbexplore"></a>Просмотр данных и проектирование характеристик в SQL Server
В этом разделе мы выполним возможности просмотра и создания данных с помощью запросов SQL непосредственно в hello **SQL Server Management Studio** hello базы данных SQL Server с помощью созданного ранее. Пример сценария с именем **пример\_queries.sql** предоставляется в hello **примеры сценариев** папки. Изменить имя базы данных hello toochange сценария hello, если он отличается от значения по умолчанию hello: **TaxiNYC**.

В этом упражнении мы выполним такие действия.

* Подключение слишком**SQL Server Management Studio** используется проверка подлинности Windows или проверки подлинности SQL и hello имени входа SQL и пароля.
* Просмотрим распределение данных по нескольким полям в различных временных окнах.
* Проверка качества данных полей hello широты и долготы.
* Создание двоичного и мультиклассовой классификации меток, основываясь на hello **совет\_сумма**.
* Создадим характеристики и вычислим/сравним расстояния поездок.
* Объединение hello двух таблиц и извлеките случайную выборку, который будет использоваться toobuild моделей.

Когда вы будете готовы tooproceed tooAzure машинного обучения, можно либо:  

1. Сохранить hello окончательного SQL запроса tooextract и образец hello данных и копирования и вставки hello запрос непосредственно в [импорта данных] [ import-data] в машинном обучении Azure, или
2. Сохранять hello выборки и социотехники данных планируется toouse для построения в новую базу данных модели и использовать новую таблицу hello в hello [импорта данных] [ import-data] модуль в машинном обучении Azure.

В этом разделе мы сохранит hello окончательный запрос tooextract и образец hello данных. Второй метод Hello демонстрируется hello [исследование данных и разработки компонентов в записной книжке IPython](#ipnb) раздела.

Для быстрой проверки количества строк и столбцов в hello hello таблиц заполняется ранее с помощью параллельный массовый импорт

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a>Просмотр: Распределение поездок по параметру medallion
В этом примере определяет medallion hello (номера такси) с более чем 100 приема-передачи данных в течение заданного периода времени. запрос Hello получают преимущества от доступа hello секционированные таблицы с момента обусловлено схему секционирования hello **раскладки\_datetime**. Запрос hello полного набора данных следует использовать hello секционированные таблицы и/или сканирование индекса.

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Просмотр: распределение поездок по параметрам medallion и hack_license
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a>Оценка качества данных: Проверка записей с неверными значениями долготы и/или широты
В этом примере анализируется, если любая из поля долготы и широты hello либо содержит недопустимое значение (градусов в радианах должно быть от -90 до 90), или иметь (0, 0) координаты.

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a>Просмотр: Выплаченные чаевые против Распределение поездок с чаевыми и без чаевых
Этот пример возвращает числовой hello приема-передачи, которые были чаевых оставил зависимости и не чаевых оставил зависимости в определенный момент времени периода (или hello полного набора данных Если охватывающие hello полный год). Это распределение отражает hello двоичных метки распространения toobe впоследствии использовать для моделирования двоичной классификации.

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a>Просмотр: распределение классов/диапазонов чаевых
Этот пример вычисляет распределение hello диапазоны подсказки в определенный момент времени периода (или hello полного набора данных Если охватывающие hello полный год). Это распределение hello hello метки классы, которые будут использоваться позже для моделирования мультиклассовой классификации.

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

#### <a name="exploration-compute-and-compare-trip-distance"></a>Просмотр: Вычисление и сравнение расстояния поездок
Этот пример преобразует hello раскладки и истощение долготы и широты tooSQL geography указывает, вычисляет расстояние trip hello, с помощью точек различие SQL geography и возвращает случайную выборку hello результатов для сравнения. пример Hello ограничивает результаты hello, координирует toovalid только с помощью hello качества данных оценки запроса, описанные выше.

    SELECT
    pickup_location=geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326)
    ,dropoff_location=geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326)
    ,trip_distance
    ,computedist=round(geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326).STDistance(geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326))/1000, 2)
    FROM nyctaxi_trip
    tablesample(0.01 percent)
    WHERE CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND   CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

#### <a name="feature-engineering-in-sql-queries"></a>Проектирование характеристик в запросах SQL
Hello метки поколения geography преобразования просмотра запросов и также может быть используется toogenerate метки или компоненты, удалив подсчета часть hello. Дополнительные функции проектирования SQL приведены примеры в hello [исследование данных и разработки компонентов в записной книжке IPython](#ipnb) раздела. Это более эффективные запросы toorun hello возможность формирования на hello полного набора данных или подмножества его с помощью SQL-запросов, которые выполняются непосредственно в экземпляре базы данных SQL Server hello. Hello запросы могут производиться в **SQL Server Management Studio**, ноутбук IPython или любого средства и среда разработки доступ к которому hello базы данных, локально или удаленно.

#### <a name="preparing-data-for-model-building"></a>Подготовка данных для построения модели
Hello следующий запрос соединения hello **nyctaxi\_trip** и **nyctaxi\_тариф авиакомпании** таблицы, приводит к возникновению ошибки двоичной классификации метки **чаевых оставил зависимости**, Метка многоклассовый классификатор **совет\_класса**и извлекает из полного объединенном наборе данных hello случайной выборки 1%. Этот запрос можно скопировать, затем вставить непосредственно в hello [студии машинного обучения Azure](https://studio.azureml.net) [импорта данных] [ import-data] модуль для приема прямой данных из базы данных SQL Server hello экземпляр в Azure. запрос Hello исключает записи с неверным (0, 0) координаты.

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_trip t, nyctaxi_fare f
    TABLESAMPLE (1 percent)
    WHERE t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'


## <a name="ipnb"></a>Просмотр данных и проектирование характеристик в IPython Notebook
В этом разделе мы выполним исследование данных и создание функции, с помощью запросов Python и SQL для базы данных SQL Server hello, созданного ранее. Образец ноутбук IPython с именем **machine-Learning-data-science-process-sql-story.ipynb** предоставляется в hello **ноутбуков IPython пример** папки. Этот файл также доступен на [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).

Привет, рекомендуется последовательность при работе с большими данными необходимо hello в следующем:

* Чтение в небольшую выборку данных hello в кадр данных в памяти.
* Выполните некоторые визуализации и исследования с помощью hello выборки данных.
* Поэкспериментируйте с помощью hello конструируются выборке данных.
* Для просмотра данных большего размера обработку данных и конструируются, использовать tooissue Python SQL-запросы непосредственно к базе данных SQL Server hello в hello виртуальной Машине Azure.
* Решите, toouse размер образца hello для построения модели машинного обучения Azure.

Окончании tooproceed tooAzure машинного обучения, вы можете либо:  

1. Сохранить hello окончательного SQL запроса tooextract и образец hello данных и копирования и вставки hello запрос непосредственно в [импорта данных] [ import-data] модуль в машинном обучении Azure. Этот метод, представленный в hello [построение моделей в машинном обучении Azure](#mlmodel) раздела.    
2. Hello выборки и сохранялись социотехники планирование toouse для построения таблицы базы данных модели, а затем использовать новую таблицу hello в hello [импорта данных] [ import-data] модуля.

Hello ниже приведены несколько исследования данных, визуализация данных и проектирование примеры компонентов. Дополнительные примеры см. в разделе ноутбук SQL IPython образец hello в hello **ноутбуков IPython пример** папки.

#### <a name="initialize-database-credentials"></a>Инициализация учетных данных базы данных
Инициализируйте параметры подключения к базе данных в hello следующие переменные:

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a>Создание подключения к базе данных
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a>Сообщение числа строк и столбцов в таблице nyctaxi_trip
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('nyctaxi_trip')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('nyctaxi_trip')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* Общее число строк = 173179759  
* Общее число столбцов = 14

#### <a name="read-in-a-small-data-sample-from-hello-sql-server-database"></a>Чтение в образец небольшой данных из базы данных SQL Server hello
    t0 = time.time()

    query = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (0.05 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

Время tooread hello образец таблицы — 6.492000 секунд  
Число извлеченных строк и столбцов = (84952, 21)

#### <a name="descriptive-statistics"></a>Описательная статистика
Теперь все готово tooexplore hello выборки данных. Мы начнем с рассмотрения Описательная статистика для hello **trip\_расстояние** (или любой другой) полей:

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a>Визуализация: Пример блочной диаграммы
Теперь рассмотрим hello Блочная для hello trip расстояние toovisualize hello квантилей

    df1.boxplot(column='trip_distance',return_type='dict')

![График #1][1]

#### <a name="visualization-distribution-plot-example"></a>Визуализация: Пример графика распределения
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![График #2][2]

#### <a name="visualization-bar-and-line-plots"></a>Визуализация: Гистограммы и линейные графики
В этом примере мы bin расстояние trip hello в пять ячеек и визуализировать hello группирование результатов.

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

Мы построения hello выше распространения ячейки в строку или строки построения, как показано ниже

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![График #3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![График #4][4]

#### <a name="visualization-scatterplot-example"></a>Визуализация: Пример точечной диаграммы
Мы покажем точечной диаграммы между **trip\_время\_в\_сек** и **trip\_расстояние** toosee при наличии корреляции

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![График #6][6]

Аналогичным образом можно проверить hello связь между **скорость\_кода** и **trip\_расстояние**.

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![График #8][8]

### <a name="sub-sampling-hello-data-in-sql"></a>Hello вложенных выборки данных в SQL
При подготовке данных для построения модели [студии машинного обучения Azure](https://studio.azureml.net), либо можно на hello **toouse запроса SQL непосредственно в модуль импорта данных hello** или сохранить hello разработан и выборки данные в новую таблицу, которая может использоваться при hello [импорта данных] [ import-data] модуля с помощью простого **ВЫБЕРИТЕ * FROM < ваш\_новый\_таблицы\_имя >**.

В этом разделе мы создадим новый hello toohold таблицу выборки и разработан данных. Приводятся примеры прямых запросов SQL для построения модели в hello [Engineering функции в SQL Server и просмотра данных](#dbexplore) раздела.

#### <a name="create-a-sample-table-and-populate-with-1-of-hello-joined-tables-drop-table-first-if-it-exists"></a>Создайте образец таблицы и заполнить с % 1, hello объединить таблиц. Сначала удалите таблицу, если она существует.
В этом разделе мы соединения таблиц hello **nyctaxi\_trip** и **nyctaxi\_тариф авиакомпании**, извлечь случайной выборки 1%, и сохранения данных выборки hello в новое имя таблицы  **nyctaxi\_один\_процентов**:

    cursor = conn.cursor()

    drop_table_if_exists = '''
        IF OBJECT_ID('nyctaxi_one_percent', 'U') IS NOT NULL DROP TABLE nyctaxi_one_percent
    '''

    nyctaxi_one_percent_insert = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount
        INTO nyctaxi_one_percent
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (1 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
        AND   pickup_longitude <> '0' AND dropoff_longitude <> '0'
    '''

    cursor.execute(drop_table_if_exists)
    cursor.execute(nyctaxi_one_percent_insert)
    cursor.commit()

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a>Просмотр данных с помощью SQL-запросов в IPython Notebook
В этом разделе мы исследуем распределения данных с использованием данных hello выборки % 1, который сохраняется в новой таблице hello, созданной ранее. Обратите внимание, что аналогично просмотров может осуществляться с помощью hello исходных таблиц, при необходимости используя **TABLESAMPLE** tooa данный период времени с помощью hello результаты просмотра hello toolimit, образец или ограничивая hello **раскладки \_datetime** секции, как показано в hello [Engineering функции в SQL Server и просмотра данных](#dbexplore) раздела.

#### <a name="exploration-daily-distribution-of-trips"></a>Исследование: ежедневное распределение поездок
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a>Исследование: распределение поездок по параметру medallion
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a>Создание характеристик с помощью SQL-запросов в IPython Notebook
В этом разделе мы создадим новые метки и компонентов непосредственно с использованием SQL-запросов, на 1% Образец таблицы hello созданную в предыдущем разделе hello.

#### <a name="label-generation-generate-class-labels"></a>Создание метки: Создать метки классов
В следующем примере hello мы создаем два набора toouse метки для моделирования:

1. Метки двоичной классификации **tipped** (прогнозирование, будут ли выплачены чаевые).
2. Метки мультиклассовой **совет\_класс** (прогнозирование hello совет bin или диапазона)
   
        nyctaxi_one_percent_add_col = '''
            ALTER TABLE nyctaxi_one_percent ADD tipped bit, tip_class int
        '''
   
        cursor.execute(nyctaxi_one_percent_add_col)
        cursor.commit()
   
        nyctaxi_one_percent_update_col = '''
            UPDATE nyctaxi_one_percent
            SET
               tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
               tip_class = CASE WHEN (tip_amount = 0) THEN 0
                                WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                                WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                                WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                                ELSE 4
                            END
        '''
   
        cursor.execute(nyctaxi_one_percent_update_col)
        cursor.commit()

#### <a name="feature-engineering-count-features-for-categorical-columns"></a>Проектирование характеристик: Количественные характеристики для столбцов категорий
Этот пример преобразует поле категории в числовое поле, заменяя hello число вхождений в данных hello каждой категории.

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD cmt_count int, vts_count int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B AS
        (
            SELECT medallion, hack_license,
                SUM(CASE WHEN vendor_id = 'cmt' THEN 1 ELSE 0 END) AS cmt_count,
                SUM(CASE WHEN vendor_id = 'vts' THEN 1 ELSE 0 END) AS vts_count
            FROM nyctaxi_one_percent
            GROUP BY medallion, hack_license
        )

        UPDATE nyctaxi_one_percent
        SET nyctaxi_one_percent.cmt_count = B.cmt_count,
            nyctaxi_one_percent.vts_count = B.vts_count
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion AND A.hack_license = B.hack_license
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a>Проектирование характеристик: Ячейка характеристик для числовых столбцов
Этот пример преобразует непрерывное числовое поле в предустановленные диапазоны категорий, т. е. преобразует числовое поле в поле категории.

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD trip_time_bin int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B(medallion,hack_license,pickup_datetime,trip_time_in_secs, BinNumber ) AS
        (
            SELECT medallion,hack_license,pickup_datetime,trip_time_in_secs,
            NTILE(5) OVER (ORDER BY trip_time_in_secs) AS BinNumber from nyctaxi_one_percent
        )

        UPDATE nyctaxi_one_percent
        SET trip_time_bin = B.BinNumber
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion
        AND A.hack_license = B.hack_license
        AND A.pickup_datetime = B.pickup_datetime
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a>Проектирование характеристик: Извлечение характеристик местоположения из десятичных значений широты/долготы
В этом примере разбивает hello десятичное представление поля широты и долготы в нескольких полей области с различной степенью детализации, например, страны, города, города, блок, и т. д. Обратите внимание, что новый hello geo поля не сопоставлены tooactual расположения. Дополнительные сведения о сопоставлении местоположений геокодов см. в статье о [службах REST карт Bing](https://msdn.microsoft.com/library/ff701710.aspx).

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent
        ADD l1 varchar(6), l2 varchar(3), l3 varchar(3), l4 varchar(3),
            l5 varchar(3), l6 varchar(3), l7 varchar(3)
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        UPDATE nyctaxi_one_percent
        SET l1=round(pickup_longitude,0)
            , l2 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 1 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),1,1) ELSE '0' END     
            , l3 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 2 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),2,1) ELSE '0' END     
            , l4 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 3 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),3,1) ELSE '0' END     
            , l5 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 4 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),4,1) ELSE '0' END     
            , l6 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 5 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),5,1) ELSE '0' END     
            , l7 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 6 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),6,1) ELSE '0' END
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a>Проверьте hello конечная форма hello признак таблицы
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

Мы стали готовы tooproceed toomodel построение и развертывание модели в [машинного обучения Azure](https://studio.azureml.net). Hello данных готов для hello прогноза причинами, описанных выше, а именно:

1. Двоичная классификация: toopredict ли уплаченной Совет для маршрута.
2. Мультиклассовая классификация: диапазон hello toopredict совета оплачен, в соответствии с toohello ранее определенных классов.
3. Задача регрессии: оплачена сумма hello toopredict подсказки для маршрута.  

## <a name="mlmodel"></a>Построение моделей в машинном обучении Azure
toobegin hello моделирования упражнения журнала в рабочей области машинного обучения Azure tooyour. Если вы еще не создали рабочую область машинного обучения, см. статью [Создание рабочей области машинного обучения Azure и предоставление к ней общего доступа](machine-learning-create-workspace.md).

1. tooget к выполнению машинного обучения Azure в разделе [возможности студии машинного обучения Azure?](machine-learning-what-is-ml-studio.md)
2. Войдите в слишком[студии машинного обучения Azure](https://studio.azureml.net).
3. Hello Studio домашней странице предоставляет широкий набор сведений, видео, учебники, ссылки toohello Справочник по модулям и другие ресурсы. Дополнительные сведения о машинного обучения Azure обратитесь к hello [центр документации машинного обучения Azure](https://azure.microsoft.com/documentation/services/machine-learning/).

Эксперимента обучения обычно состоит из следующих hello.

1. Создать **+НОВЫЙ** эксперимент.
2. Получение данных hello tooAzure машинного обучения.
3. Предварительно обработать, преобразование данных и управления ими hello при необходимости.
4. Создать необходимые характеристики.
5. Разбиение данных hello в набор данных, обучения и проверки и тестирования (или иметь отдельный набор данных для каждого).
6. Выберите один или несколько алгоритмов машинного обучения в зависимости от hello обучения toosolve проблему. Например, двоичная классификация, мультиклассовая классификация, регрессия.
7. Обучение одной или нескольких моделей с помощью hello обучающий набор данных.
8. Оценка hello проверочного набора данных с помощью обученной модели hello.
9. Оцените hello модели toocompute hello соответствующие метрики для изучения проблемы hello.
10. Настройка модели hello и выберите hello наиболее toodeploy модели.

В этом упражнении мы уже изучена разработан hello данных в SQL Server и решили tooingest размер образца hello в машинном обучении Azure. toobuild один или несколько моделей прогнозирования hello мы решили:

1. Получение данных hello tooAzure машинного обучения с помощью hello [импорта данных] [ import-data] модуля, доступные в hello **ввод и вывод данных** раздела. Дополнительные сведения см. в разделе hello [импорта данных] [ import-data] справочной странице модуля.
   
    ![Импорт данных в Машинное обучение Azure][17]
2. Выберите **базы данных SQL Azure** как hello **источника данных** в hello **свойства** панель.
3. Введите имя DNS hello базы данных в hello **имя сервера базы данных** поля. Формат: `tcp:<your_virtual_machine_DNS_name>,1433`
4. Введите hello **имя базы данных** в соответствующее поле hello.
5. Введите hello **имя пользователя SQL** в hello ** aqccount имени пользователя и пароль hello в hello **пароль учетной записи пользователя сервера**.
6. Установите флажок **Принимать любой сертификат сервера** .
7. В hello **запроса базы данных** Измените текстовое поле, вставьте запрос hello какие извлекает hello необходимые поля (включая все вычисляемые поля, такие как метки hello) базы данных и вниз образцы размер выборки toohello требуемого hello данных.

Примером бинарной классификации эксперимент, чтение данных непосредственно из базы данных SQL Server hello является hello рис. ниже. Подобные эксперименты можно сконструировать для задач мультиклассовой классификации и регрессии.

![Обучение моделей Машинного обучения Azure][10]

> [!IMPORTANT]
> В hello моделирования данных по извлечению и выборки запроса примеры, приведенные в предыдущих разделах **все метки для моделирования упражнений hello трех включаются в запрос hello**. (Обязательный) в каждом hello моделирования упражнения важно слишком**исключить** hello ненужные метки для hello другие две проблемы и любые другие **целевой утечки**. Для например, при использовании двоичной классификации, используйте метки hello **чаевых оставил зависимости** и исключить hello поля **совет\_класса**, **совет\_сумма**, и **общее\_сумма**. последний Hello оплачиваются утечки целевой, так как они предполагают совет hello.
> 
> tooexclude ненужных столбцов и/или целевой утечки, можно использовать hello [Выбор столбцов в наборе данных] [ select-columns] модуля или hello [редактирование метаданных] [ edit-metadata]. Дополнительные сведения см. на страницах справки модулей [Select Columns in Dataset][select-columns] (Выбор столбцов в наборе данных) и [Edit Metadata][edit-metadata] (Изменение метаданных).
> 
> 

## <a name="mldeploy"></a>Развертывание моделей в машинном обучении Azure
Когда модель готова, можно легко развернуть его веб-службы непосредственно из эксперимента hello. Дополнительные сведения см. в статье [Развертывание веб-службы машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md).

toodeploy веб-службу, необходимо:

1. Создать эксперимент по количественной оценке.
2. Развертывание веб-службы hello.

оценки поэкспериментировать с toocreate **завершен** обучения, эксперимента, нажмите кнопку **создать ЭКСПЕРИМЕНТ ОЦЕНКИ** hello нижней панели действий.

![Система оценок Azure][18]

Машинное обучение Azure попытается toocreate эксперимент оценки на основе компонентов hello эксперимента обучения hello. В частности, она:

1. Сохранить обученную модель hello и удалите hello модели обучающих модулей.
2. Определение логических **входному порту** toorepresent hello требуется схема входных данных.
3. Определение логических **выходного порта** toorepresent hello ожидаемый web службы выходные данные схемы.

При создании hello эксперимент оценки, просмотра и при необходимости измените. Типичные корректировки — входного набора данных hello tooreplace или запроса с одним, что исключает поля меток, их будет недоступен при вызове службы hello. Это также размером хорошей практикой tooreduce hello hello входной набор данных или запроса tooa несколько записей, достаточно tooindicate hello входной схемы. Для порта вывода hello, он общие tooexclude всех полей ввода и включать только hello **меток оцененных значений** и **оцененных вероятностей** в выходных данных с помощью hello hello [Выбор столбцов в наборе данных ] [ select-columns] модуля.

Пример оценки экспериментов — hello рис. ниже. Окончании toodeploy, нажмите кнопку hello **публикации веб-службы** кнопку hello нижней панели действий.

![Публикация в Машинном обучении Azure][11]

toorecap, в этом учебнике пошаговом руководстве вы создали среде обработки и анализа данных Azure, работали с большим набором данных открытый все возможности hello со toomodel приобретения данных обучения и развертывание веб-службы машинного обучения Azure.

### <a name="license-information"></a>Сведения о лицензии
Это пошаговое руководство по примеру и соответствующую ему коллекцию скриптов и IPython notebook(s) совместно корпорацией Майкрософт в рамках лицензии MIT hello. Проверьте файл LICENSE.txt hello в каталоге hello hello образца кода на GitHub для получения дополнительных сведений.

### <a name="references"></a>Ссылки
•    [Страница загрузки данных о поездках такси Нью-Йорка (Andrés Monroy)](http://www.andresmh.com/nyctaxitrips/)  
•    [Получение данных о поездках такси Нью-Йорка на основании FOIL (Chris Whong)](http://chriswhong.com/open-data/foil_nyc_taxi/)   
•    [Статистические данные о комиссионных сборах за аренду такси и лимузинов Нью-Йорка](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[1]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sql-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sql-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sql-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sql-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sql-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sql-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sql-walkthrough/amlscoring.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
