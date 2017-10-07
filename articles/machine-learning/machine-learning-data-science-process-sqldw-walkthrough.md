---
title: "Hello командного процесса обработки и анализа данных в действии: хранилище данных SQL с помощью | Документы Microsoft"
description: "Расширенный процесс аналитики и технологии в действии"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 88ba8e28-0bd7-49fe-8320-5dfa83b65724
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;hangzh;weig
ms.openlocfilehash: b1b6371583a023d32e33db59464cafd8c3b767d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-data-warehouse"></a>Hello командного процесса обработки и анализа данных в действии: с помощью хранилища данных SQL
В этом учебнике мы пошаговыми руководствами по сборке и развертывании хранилища данных SQL (хранилища данных SQL) с помощью модели машинного обучения для набора данных общедоступным--hello [NYC такси приема-передачи](http://www.andresmh.com/nyctaxitrips/) набора данных. Hello модели двоичной классификации, созданной прогнозирует ли совет оплачивается для обработки и для предсказания hello распространения для Оплаченные суммы совет hello также описаны моделей мультиклассовой классификации и регрессии.

Привет, ниже представлена процедура Hello [процесса обработки и анализа данных Team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) рабочего процесса. Далее показано, как toosetup среды обработки и анализа данных, как tooload hello данных в хранилища данных SQL, а также использование хранилища данных SQL или ноутбук IPython tooexplore hello данных и инженерам функции toomodel. Затем показывается как toobuild и развертывания модели с машинного обучения Azure.

## <a name="dataset"></a>набор Hello NYC такси приема-передачи данных
Hello NYC такси обработки данных состоит из примерно 20 ГБ сжатые файлы CSV (~ 48 ГБ несжатого), запись более миллиона 173 отдельных приема-передачи и hello цен платная для каждого маршрута. Каждая запись маршрута включает hello раскладки и истощение расположений и времени, анонимен hack номер лицензии (драйвер) и hello номер medallion (уникальный идентификатор элемента такси). данные Hello охватывает все приема-передачи в 2013 году, hello и предоставляется в следующих двух наборов данных для каждого месяца hello:

1. Hello **trip_data.csv** файл содержит сведения о обработки, например количество пассажиров, отправки и dropoff точек, длительность обработки и длина маршрута. Вот несколько примеров записей:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. Hello **trip_fare.csv** файл содержит подробные сведения о тариф авиакомпании hello платная для каждого маршрута, например тип платежа, сумма тариф авиакомпании, излишнюю нагрузку налоги, советы и тарифы и hello общей оплаты. Вот несколько примеров записей:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Hello **уникальный ключ** используется toojoin trip\_данных и обработки\_тариф авиакомпании состоит из следующих трех полей hello:

* medallion,
* hack\_license и
* pickup\_datetime.

## <a name="mltasks"></a>Определение трех типов задач прогнозирования
Мы сформулировать три прогноза проблемы с учетом hello *совет\_сумма* задачи моделирования tooillustrate трех типов:

1. **Двоичной классификации**: toopredict ли совет уплаченной поездки, т. е. *совет\_сумма* , которое больше, чем $0 — положительные пример, тогда как *совет\_сумма* $ 0 представляет собой отрицательное пример.
2. **Мультиклассовая классификация**: диапазон hello toopredict подсказки оплаты hello trip. Разделен hello *совет\_сумма* в пять ячеек или классы:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. **Задача регрессии**: оплачена сумма hello toopredict подсказки для маршрута.  

## <a name="setup"></a>Настройка среды обработки и анализа данных Azure hello для расширенной аналитики
tooset настройку среды обработки и анализа данных Azure, выполните следующие действия.

**Создайте собственную учетную запись хранилища BLOB-объектов Azure**

* При подготовке хранилища BLOB-объектов Azure, выберите географическое расположение для хранилища BLOB-объектов Azure в или как можно ближе слишком**центральных штатах юга США**, который здесь хранятся hello такси NYC данных. с помощью AzCopy из контейнера tooa контейнер хранилища BLOB-объект открытого hello в учетной записи будут копироваться данные Hello. Hello ближе к хранилищу больших двоичных объектов tooSouth центральной части США, hello быстрее этой задачи (шаг 4) будет завершено.
* toocreate собственные учетной записи хранилища Azure, hello выполните шаги, описанные в [учетных записей хранилища Azure о](../storage/common/storage-create-storage-account.md). Быть убедиться, что примечания toomake hello значения для следующих учетных данных учетной записи хранилища, как они потребуется позже в этом пошаговом руководстве.
  
  * **Имя учетной записи хранения**
  * **Ключ учетной записи хранения**
  * **Имя контейнера** (который вы хотите toobe hello данные, хранящиеся в hello хранилище больших двоичных объектов)

**Подготовьте экземпляр хранилища данных SQL Azure.**
Выполните hello документации на [создать хранилище данных SQL](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision экземпляр хранилища данных SQL. Убедитесь, что вносимые нотации на hello следующие учетные данные хранилища данных SQL, которые будут использоваться на последующих этапах.

* **Имя сервера**: <server Name>.database.windows.net.
* **имя (базы данных) хранилища данных SQL;**
* **Имя пользователя**
* **Пароль**

**Установите Visual Studio и SQL Server Data Tools.** Инструкции можно найти в статье [Установка Visual Studio 2015 и SSDT для хранилища данных SQL](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).

**Подключение tooyour хранилища данных SQL Azure с помощью Visual Studio.** Инструкции см. шаги 1 и 2 в [подключения tooAzure хранилище данных SQL с помощью Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).

> [!NOTE]
> Выполнения hello следующий запрос SQL в базе данных hello, созданных в хранилище данных SQL (вместо hello запрос, приведенный в шаге 3 hello подключиться разделе) слишком**создайте главный ключ**.
> 
> 

    BEGIN TRY
           --Try toocreate hello master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If hello master key exists, do nothing
    END CATCH;

**Создайте рабочую область Машинного обучения Azure, используя подписку Azure.** Инструкции можно найти в статье [Создание рабочей области машинного обучения Azure](machine-learning-create-workspace.md).

## <a name="getdata"></a>Hello данные загружаются в хранилище данных SQL
Откройте командную консоль Windows PowerShell. Hello следующей команды PowerShell toodownload hello примере файлы скрипта SQL, мы поделиться с вами в локальный каталог tooa GitHub, который указывается с помощью параметра hello *- DestDir*. Можно изменить значение параметра hello *- DestDir* tooany локальный каталог. Если *- DestDir* не существует, он будет создан hello сценарий PowerShell.

> [!NOTE]
> Может потребоваться слишком**Запуск от имени администратора** при выполнении следующего сценария PowerShell if Здравствуй вашей *DestDir* каталог должен tooit toocreate или toowrite прав администратора.
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

После успешного выполнения изменяет текущий рабочий каталог слишком*- DestDir*. Можно toosee экран, подобный ниже:

![][19]

В вашей *- DestDir*, выполните следующий сценарий PowerShell с правами администратора hello:

    ./SQLDW_Data_Import.ps1

Hello сценария PowerShell для hello первый раз, запускаемый запрашивается tooinput hello сведения из вашего хранилища данных SQL Azure и вашей учетной записи хранилища BLOB-объектов Azure. По завершении этого скрипта PowerShell под управлением для hello впервые, учетные данные hello входных данных можно будет были записаны файл конфигурации tooa SQLDW.conf в hello имеется рабочий каталог. Hello будущих выполнения этот файл сценария PowerShell имеет параметр tooread hello всех необходимых параметров из файла конфигурации. Если вам требуется toochange некоторые параметры, вы можете tooinput hello параметров на экране приветствия после строки, удаление этого файла конфигурации и ввод значений параметров hello в ответ на приглашение или значений параметров hello toochange путем редактирования файла SQLDW.conf hello в вашей *- DestDir* каталога.

> [!NOTE]
> В порядке tooavoid схемы имя конфликтует с уже существующих в вашей хранилища данных SQL Azure при чтении параметров непосредственно из файла SQLDW.conf hello случайное число из 3 цифр добавляется имя схемы toohello из файла SQLDW.conf hello как имя схемы по умолчанию hello для Каждое выполнение. Hello сценарий PowerShell может запросить имя схемы: hello имя может быть указан по своему усмотрению пользователя.
> 
> 

Это **сценарий PowerShell** файл завершения hello следующие задачи:

* **Скачивание и установка AzCopy**, если она еще не установлена.
  
        $AzCopy_path = SearchAzCopy
        if ($AzCopy_path -eq $null){
               Write-Host "AzCopy.exe is not found in C:\Program Files*. Now, start installing AzCopy..." -ForegroundColor "Yellow"
            InstallAzCopy
            $AzCopy_path = SearchAzCopy
        }
            $env_path = $env:Path
            for ($i=0; $i -lt $AzCopy_path.count; $i++){
                if ($AzCopy_path.count -eq 1){
                    $AzCopy_path_i = $AzCopy_path
                } else {
                    $AzCopy_path_i = $AzCopy_path[$i]
                }
                if ($env_path -notlike '*' +$AzCopy_path_i+'*'){
                    Write-Host $AzCopy_path_i 'not in system path, add it...'
                    [Environment]::SetEnvironmentVariable("Path", "$AzCopy_path_i;$env_path", "Machine")
                    $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
                    $env_path = $env:Path
                }
* **Копирование учетной записи хранилища данных tooyour закрытый большой двоичный объект** из hello общедоступный BLOB-объект с помощью AzCopy
  
        Write-Host "AzCopy is copying data from public blob tooyo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account tooverify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob tooyour storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* **Загружает данные с помощью Polybase (путем выполнения LoadDataToSQLDW.sql) tooyour хранилища данных SQL Azure** из вашей учетной записи хранилища закрытый большой двоичный объект с hello, следующие команды.
  
  * Создание схемы
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * Создание учетных данных для определенной базы данных
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * Создание внешнего источника данных для BLOB-объекта хранилища Azure
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_trip_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_fare_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
  * Создание формата внешнего файла для CSV-файла. Без сжатия данных и поля разделены символом вертикальной черты hello.
    
          CREATE EXTERNAL FILE FORMAT {csv_file_format}
          WITH
          (   
              FORMAT_TYPE = DELIMITEDTEXT,
              FORMAT_OPTIONS  
              (
                  FIELD_TERMINATOR ='','',
                  USE_TYPE_DEFAULT = TRUE
              )
          )
          ;
  * Создание внешних таблиц (trip и fare) для хранения набора данных такси Нью-Йорка в хранилище BLOB-объектов Azure.
    
          CREATE EXTERNAL TABLE {external_nyctaxi_fare}
          (
              medallion varchar(50) not null,
              hack_license varchar(50) not null,
              vendor_id char(3),
              pickup_datetime datetime not null,
              payment_type char(3),
              fare_amount float,
              surcharge float,
              mta_tax float,
              tip_amount float,
              tolls_amount float,
              total_amount float
          )
          with (
              LOCATION    = ''/nyctaxifare/'',
              DATA_SOURCE = {nyctaxi_fare_storage},
              FILE_FORMAT = {csv_file_format},
              REJECT_TYPE = VALUE,
              REJECT_VALUE = 12     
          )  

            CREATE EXTERNAL TABLE {external_nyctaxi_trip}
            (
                   medallion varchar(50) not null,
                   hack_license varchar(50)  not null,
                   vendor_id char(3),
                   rate_code char(3),
                   store_and_fwd_flag char(3),
                   pickup_datetime datetime  not null,
                   dropoff_datetime datetime,
                   passenger_count int,
                   trip_time_in_secs bigint,
                   trip_distance float,
                   pickup_longitude varchar(30),
                   pickup_latitude varchar(30),
                   dropoff_longitude varchar(30),
                   dropoff_latitude varchar(30)
            )
            with (
                LOCATION    = ''/nyctaxitrip/'',
                DATA_SOURCE = {nyctaxi_trip_storage},
                FILE_FORMAT = {csv_file_format},
                REJECT_TYPE = VALUE,
                REJECT_VALUE = 12         
            )

    - Загрузка данных из внешних таблиц в хранилище BLOB-объектов Azure tooSQL хранилища данных

            CREATE TABLE {schemaname}.{nyctaxi_fare}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_fare}
            ;

            CREATE TABLE {schemaname}.{nyctaxi_trip}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_trip}
            ;

    - Создать образец таблицы данных (NYCTaxi_Sample) и вставки данных tooit от выбора SQL-запросы таблиц маршрута и тариф авиакомпании hello. (Некоторые шаги в этом пошаговом руководстве должен toouse этот образец таблицы.)

            CREATE TABLE {schemaname}.{nyctaxi_sample}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            (
                SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount,
                tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
                tip_class = CASE
                        WHEN (tip_amount = 0) THEN 0
                        WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                        WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                        WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                        ELSE 4
                    END
                FROM {schemaname}.{nyctaxi_trip} t, {schemaname}.{nyctaxi_fare} f
                WHERE datepart("mi",t.pickup_datetime) = 1
                AND t.medallion = f.medallion
                AND   t.hack_license = f.hack_license
                AND   t.pickup_datetime = f.pickup_datetime
                AND   pickup_longitude <> ''0''
                AND   dropoff_longitude <> ''0''
            )
            ;

географическое расположение Hello учетные записи хранения влияет на время загрузки.

> [!NOTE]
> В зависимости от географического расположения hello вашей учетной записи хранилища закрытый большой двоичный объект, hello процесс копирования данных из большой двоичный объект открытого tooyour личной учетной записи хранения может занять около 15 минут или даже больше и hello обработать загрузки данных из вашей учетной записи хранения tooyour хранилища данных SQL Azure может занять до 20 минут или больше.  
> 
> 

Что делать, если у вас есть дублирования источника и назначения файлов будет иметь toodecide.

> [!NOTE]
> Если toobe файлы CSV-файл hello, скопированные из учетной записи хранилища закрытый большой двоичный объект tooyour в хранилище BLOB-объект открытого hello уже существуют в вашей учетной записи хранилища закрытый большой двоичный объект, AzCopy запрашивает, следует ли вы toooverwrite их. Если вы не хотите toooverwrite их, входные  **n**  при появлении запроса. Если требуется, чтобы toooverwrite **все** из них, ввода **** при появлении запроса. Также можно ввести **y** toooverwrite .csv файлы по отдельности.
> 
> 

![График № 21][21]

Можно использовать собственные данные. Если данные хранятся в локальном компьютере, в реальной жизни приложения, по-прежнему можно использовать закрытый большой двоичный объект Azure AzCopy tooupload локальных данных tooyour хранилища. Требуется только toochange hello **источника** расположение, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, в hello команды AzCopy hello PowerShell скрипт файл toohello локальный каталог, содержащий данные.

> [!TIP]
> Если данные уже находится в хранилище BLOB-объектов Azure закрытый в реальной жизни приложения, можно пропустить hello AzCopy hello сценарий PowerShell и тем самым непосредственно передать tooAzure hello данных хранилища данных SQL. Потребуются дополнительные редактирует из сценария tootailor hello его toohello формат данных.
> 
> 

Этот сценарий Powershell также подключает hello сведения хранилища данных SQL Azure в hello исследования примере файлы данных SQLDW_Explorations.sql, SQLDW_Explorations.ipynb и SQLDW_Explorations_Scripts.py, чтобы эти три файла будут готовы toobe испытан мгновенно После завершения hello сценарий PowerShell.

После успешного выполнения вы увидите экран, аналогичный этому:

![][20]

## <a name="dbexplore"></a>Изучение данных и проектирование признаков в хранилище данных SQL Azure
В этом разделе мы исследуем данные и создадим признаки, используя SQL-запросы для хранилища данных SQL Azure с помощью **средств работы с данными Visual Studio**. Все запросы SQL, используемые в этом разделе можно найти в hello пример сценария с именем *SQLDW_Explorations.sql*. Этот файл уже загруженные tooyour локальный каталог для скрипта PowerShell hello. Кроме того, его также можно получить на сайте [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql). Но в GitHub в файл hello отсутствуют сведения hello хранилища данных SQL Azure, попадет в систему.

Подключение tooyour хранилища данных SQL Azure с помощью Visual Studio с именем входа hello хранилища данных SQL и пароля и откройте hello **обозреватель объектов SQL** базу данных tooconfirm hello и таблицы были импортированы. Получить hello *SQLDW_Explorations.sql* файла.

> [!NOTE]
> tooopen редактор запросов хранилища параллельных данных (PDW), использовать hello **новый запрос** команду в это время ваш PDW выбран hello **обозреватель объектов SQL**. PDW Hello стандартный редактор SQL-запросов не поддерживается.
> 
> 

Ниже приведены hello тип данных, возможности просмотра и создания задачи, выполняемые в этом разделе:

* Просмотрим распределение данных по нескольким полям в различных временных окнах.
* Проверка качества данных полей hello широты и долготы.
* Создание двоичного и мультиклассовой классификации меток, основываясь на hello **совет\_сумма**.
* Создадим характеристики и вычислим/сравним расстояния поездок.
* Объединение hello двух таблиц и извлеките случайную выборку, который будет использоваться toobuild моделей.

### <a name="data-import-verification"></a>Проверка импорта данных
Эти запросы обеспечивают быстрой проверки количества строк и столбцов в таблицах, заполнять ранее с помощью Polybase параллельный массовый импорт, приветствия hello

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

**Выходные данные.** Вы должны получить 173 179 759 строк и 14 столбцов.

### <a name="exploration-trip-distribution-by-medallion"></a>Просмотр: Распределение поездок по параметру medallion
Следующий пример запроса определяет medallions hello (номера такси) завершенных более 100 приема-передачи данных в течение указанного периода времени. запрос Hello получают преимущества от доступа hello секционированные таблицы с момента обусловлено схему секционирования hello **раскладки\_datetime**. Запрос hello полного набора данных следует использовать hello секционированные таблицы и/или сканирование индекса.

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

**Вывод:** hello запросов должны возвращать таблицу со строками, указав hello 13,369 medallions (такси) и hello количество выполненных их в 2013 trip. последний столбец Hello содержит hello число hello приема-передачи завершена.

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Просмотр: распределение поездок по параметрам medallion и hack_license
Этот пример определяет medallions hello (номера такси) и hack_license цифры (драйверы) выполнения больше, чем 100 приема-передачи данных в течение указанного периода времени.

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

**Вывод:** hello запрос должен возвращать таблицу со строками 13,369, указав идентификаторы выполненными более, 100 приема-передачи в 2013 драйвер или автомобиль hello 13,369. последний столбец Hello содержит hello число hello приема-передачи завершена.

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a>Оценка качества данных: проверка записей с неправильными значениями долготы и/или широты
В этом примере анализируется, если любая из поля долготы и широты hello либо содержит недопустимое значение (градусов в радианах должно быть от -90 до 90), или иметь (0, 0) координаты.

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

**Вывод:** hello запрос возвращает 837,467 приема-передачи, которые имеют недопустимые поля долготы и широты.

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a>Изучение: распределение поездок с чаевыми и без чаевых
Этот пример возвращает числовой hello приема-передачи, были чаевых оставил зависимости и номер hello, не были Подрезанный за указанный период времени (или hello полного набора данных Если охватывающие hello полный год, которая будет настроена здесь). Это распределение отражает hello двоичных метки распространения toobe впоследствии использовать для моделирования двоичной классификации.

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

**Вывод:** hello запроса следует следующие возвращаемого hello совет частот hello годом 2013: 90,447,622 чаевых оставил зависимости и 82,264,709 чаевых оставил зависимости не.

### <a name="exploration-tip-classrange-distribution"></a>Изучение: распределение классов и диапазонов чаевых
Этот пример вычисляет распределение hello диапазоны подсказки в определенный момент времени периода (или hello полного набора данных Если охватывающие hello полный год). Это распределение hello hello метки классы, которые будут использоваться позже для моделирования мультиклассовой классификации.

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

**Выходные данные:**

| tip_class | tip_freq |
| --- | --- |
| 1 |82230915 |
| 2 |6198803 |
| 3 |1932223 |
| 0 |82264625 |
| 4 |85765 |

### <a name="exploration-compute-and-compare-trip-distance"></a>Изучение: вычисление и сравнение расстояния поездок
Этот пример преобразует hello раскладки и истощение долготы и широты tooSQL geography указывает, вычисляет расстояние trip hello, с помощью точек различие SQL geography и возвращает случайную выборку hello результатов для сравнения. пример Hello ограничивает результаты hello, координирует toovalid только с помощью hello качества данных оценки запроса, описанные выше.

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function toocalculate hello direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

### <a name="feature-engineering-using-sql-functions"></a>Проектирование признаков с помощью функций SQL
Иногда функции SQL могут быть полезны при проектировании признаков. В этом пошаговом руководстве мы определили SQL функция toocalculate hello прямой расстояние между расположениями отправки и dropoff hello. Можно выполнить следующие сценарии SQL в hello **данных средств Visual Studio**.

Вот hello скрипт SQL, который определяет функции hello расстояние.

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate hello direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

Ниже приведен пример toocall функции toogenerate этой функции в SQL-запросе:

    -- Sample query toocall hello function toocreate features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

**Вывод:** этот запрос создает таблицу (с 2,803,538 строк) с раскладки и dropoff latitudes и долгот и соответствующий hello направлять расстояние в милях. Ниже приведены результаты hello первыми тремя строками.

|  | pickup_latitude | pickup_longitude | dropoff_latitude | dropoff_longitude | DirectDistance |
| --- | --- | --- | --- | --- | --- |
| 1 |40,731804 |–74,001083 |40,736622 |–73,988953 |0,7169601222 |
| 2 |40,715794 |–74,010635 |40,725338 |–74,00399 |0,7448343721 |
| 3 |40,761456 |–73,999886 |40,766544 |–73,988228 |0,7037227967 |

### <a name="prepare-data-for-model-building"></a>Подготовка данных для построения модели
Hello следующий запрос соединения hello **nyctaxi\_trip** и **nyctaxi\_тариф авиакомпании** таблицы, приводит к возникновению ошибки двоичной классификации метки **чаевых оставил зависимости**, Метка многоклассовый классификатор **совет\_класса**и извлекает образец из hello полный объединенном наборе данных. Hello выборка выполняется путем извлечения подмножества hello приема-передачи данных на основе времени раскладки.  Этот запрос можно скопировать, затем вставить непосредственно в hello [студии машинного обучения Azure](https://studio.azureml.net) [импорта данных] [ import-data] модуль для приема прямой данных из экземпляра базы данных SQL hello в Azure. запрос Hello исключает записи с неверным (0, 0) координаты.

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
    WHERE datepart("mi",t.pickup_datetime) = 1
    AND   t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

Когда вы будете готовы tooproceed tooAzure машинного обучения, можно либо:  

1. Сохранить hello окончательного SQL запроса tooextract и образец hello данных и копирования и вставки hello запрос непосредственно в [импорта данных] [ import-data] в машинном обучении Azure, или
2. Сохранять hello выборки и социотехники данных планируется toouse для построения в новые хранилища данных SQL модели и использовать новую таблицу hello в hello [импорта данных] [ import-data] модуль в машинном обучении Azure. Hello сценария PowerShell в предыдущем шаге это сделано автоматически. Можно считывать данные непосредственно из этой таблицы в модуле hello импорта данных.

## <a name="ipnb"></a>Просмотр данных и проектирование характеристик в IPython Notebook
В этом разделе мы выполним создание функции, с помощью обоих Python и просмотра данных и запросов SQL к hello хранилища данных SQL создана ранее. Образец ноутбук IPython с именем **SQLDW_Explorations.ipynb** и файл сценария Python **SQLDW_Explorations_Scripts.py** были загруженный tooyour локальный каталог. Они также доступны на веб-сайте [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW). В сценариях Python эти два файла идентичны. файл сценария Python Hello предоставляется tooyou, если у вас на сервер ноутбук IPython. Эти два примера файлов Python предназначены для использования с **Python 2.7**.

Здравствуйте, необходимой информации хранилища данных SQL Azure в образце hello ноутбук IPython и hello сценария файл загруженный tooyour локального компьютера было подключено сценарием PowerShell hello ранее Python. Они выполняются без изменений.

Если заранее настроенных рабочую область машинного обучения Azure, можно непосредственно загрузить пример hello ноутбук IPython toohello ноутбук IPython AzureML службы и начать его выполнение. Ниже приведены hello действия tooupload tooAzureML ноутбук IPython службы.

1. Войдите в рабочей области машинного обучения Azure tooyour, нажмите кнопку «Studio» в верхнем hello и нажмите кнопку «НОУТБУКИ» hello левой части веб-страницы приветствия.
   
    ![График № 22][22]
2. Щелкните «Создать» hello левый нижний угол hello веб-страницы и выберите пункт «Python 2». Затем предоставьте записной книжке toohello имя и щелкните hello флажок toocreate hello нового пустым ноутбук IPython.
   
    ![График № 23][23]
3. Щелкните символ «Jupyter» hello в левом верхнем углу hello hello новый ноутбук IPython.
   
    ![График № 24][24]
4. Перетаскивание toohello ноутбук IPython образец hello **дерева** ноутбук IPython AzureML службы и нажмите кнопку **отправить**. Затем образец hello ноутбук IPython будет отправленного toohello ноутбук IPython AzureML службы.
   
    ![График № 25][25]

В порядке toorun hello образец ноутбук IPython или Здравствуйте файл сценария Python, hello Python требуются следующие пакеты. При использовании службы AzureML ноутбук IPython hello эти пакеты были предварительно установлены.

    - pandas
    - numpy
    - matplotlib
    - pyodbc
    - PyTables

При создании дополнительных аналитических решений на AzureML с большим объемом данных, рекомендуется использовать последовательность Hello необходимо hello в следующем:

* Чтение в небольшую выборку данных hello в кадр данных в памяти.
* Выполните некоторые визуализации и исследования с помощью hello выборки данных.
* Поэкспериментируйте с помощью hello конструируются выборке данных.
* Для просмотра большего размера данных, обработки данных и конструируются используйте Python tooissue SQL-запросы непосредственно к hello хранилища данных SQL.
* Определите, подходит для построения модели машинного обучения Azure toobe размер образца hello.

Hello Далее приведены несколько исследования данных, визуализация данных и примеры технических возможностей. Дополнительные исследования данных можно найти в образце hello ноутбук IPython и файл сценария Python образец hello.

### <a name="initialize-database-credentials"></a>Инициализация учетных данных базы данных
Инициализируйте параметры подключения к базе данных в hello следующие переменные:

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a>Создание подключения к базе данных
Вот hello строку подключения, которая создает базу данных toohello подключения hello.

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a>Сообщение числа строк и столбцов в таблице <nyctaxi_trip>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_trip>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* Общее число строк = 173179759  
* Общее число столбцов = 14

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a>Сообщение числа строк и столбцов в таблице <nyctaxi_fare>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_fare>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_fare>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* Общее число строк = 173179759  
* Общее количество столбцов — 11.

### <a name="read-in-a-small-data-sample-from-hello-sql-data-warehouse-database"></a>Чтение в образец небольшой данных из базы данных хранилища данных SQL hello
    t0 = time.time()

    query = '''
        SELECT TOP 10000 t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
        WHERE datepart("mi",t.pickup_datetime) = 1
        AND   t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

Время tooread hello образец таблицы — 14.096495 секунд.  
Количество полученных строк и столбцов — 1000 и 21.

### <a name="descriptive-statistics"></a>Описательная статистика
Теперь все готово tooexplore hello выборки данных. Мы начнем с рассмотрения некоторых описательных статистических показателей для hello **trip\_расстояние** (или другие поля нажмите toospecify).

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a>Визуализация: пример блочной диаграммы
Теперь рассмотрим hello Блочная для hello trip расстояние toovisualize hello квантилей.

    df1.boxplot(column='trip_distance',return_type='dict')

![График #1][1]

### <a name="visualization-distribution-plot-example"></a>Визуализация: пример графика распределения
Графики, отображающие распределение hello и гистограммы для hello выборки trip расстояния.

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![График #2][2]

### <a name="visualization-bar-and-line-plots"></a>Визуализация: гистограммы и линейные графики
В этом примере мы bin расстояние trip hello в пять ячеек и визуализировать hello группирование результатов.

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

Можно построить hello выше распространения ячейки в строке или строки построения с:

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![График #3][3]

и

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![График #4][4]

### <a name="visualization-scatterplot-examples"></a>Визуализация: примеры точечных диаграмм
Мы покажем точечной диаграммы между **trip\_время\_в\_сек** и **trip\_расстояние** toosee при наличии корреляции

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![График #6][6]

Аналогичным образом можно проверить hello связь между **скорость\_кода** и **trip\_расстояние**.

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![График #8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a>Изучение выборки данных с помощью SQL-запросов в IPython Notebook
В этом разделе мы исследуем распределения данных с помощью hello выборки данных, который сохраняется в новой таблице hello, созданной ранее. Обратите внимание, что аналогичные просмотров может осуществляться с помощью hello исходных таблиц.

#### <a name="exploration-report-number-of-rows-and-columns-in-hello-sampled-table"></a>Просмотр: Количество отчетов строк и столбцов в hello выбранных таблицы
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a>Исследование: распределение поездок с чаевыми и без чаевых
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a>Изучение: распределение классов чаевых
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-hello-tip-distribution-by-class"></a>Просмотр: Построения распространения совет hello классом
    tip_class_dist['tip_freq'].plot(kind='bar')

![График № 26][26]

#### <a name="exploration-daily-distribution-of-trips"></a>Исследование: ежедневное распределение поездок
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a>Исследование: распределение поездок по параметру medallion
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a>Изучение: распределение поездок по медальону и номеру лицензии водителя
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a>Просмотр: распределение поездок по времени
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a>Изучение: распределение поездок по расстоянию
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a>Изучение: распределение поездок по типу оплаты
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a>Проверьте hello конечная форма hello признак таблицы
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <a name="mlmodel"></a>Построение моделей в компоненте машинного обучения Azure
Мы стали готовы tooproceed toomodel построение и развертывание модели в [машинного обучения Azure](https://studio.azureml.net). Hello данных — Готово toobe используется ни в одном hello прогноза проблем, описанных выше, а именно:

1. **Двоичная классификация**: toopredict ли уплаченной Совет для маршрута.
2. **Мультиклассовая классификация**: диапазон hello toopredict совета оплачен, в соответствии с toohello ранее определенных классов.
3. **Задача регрессии**: оплачена сумма hello toopredict подсказки для маршрута.  

toobegin hello моделированию, войдите в tooyour **машинного обучения Azure** рабочей области. Если вы еще не создали рабочую область Машинного обучения, см. статью [Создание рабочей области Машинного обучения Azure и предоставление к ней общего доступа](machine-learning-create-workspace.md).

1. tooget к выполнению машинного обучения Azure в разделе [возможности студии машинного обучения Azure?](machine-learning-what-is-ml-studio.md)
2. Войдите в слишком[студии машинного обучения Azure](https://studio.azureml.net).
3. Hello Studio домашней странице предоставляет широкий набор сведений, видео, учебники, ссылки toohello Справочник по модулям и другие ресурсы. Дополнительные сведения о машинном обучении Azure можно найти hello [центр документации машинного обучения Azure](https://azure.microsoft.com/documentation/services/machine-learning/).

Эксперимента обучения обычно состоит из hello следующие шаги:

1. Создать **+НОВЫЙ** эксперимент.
2. Получите данные hello в Azure ML.
3. Предварительно обработать, преобразование данных и управления ими hello при необходимости.
4. Создать необходимые характеристики.
5. Разбиение данных hello в набор данных, обучения и проверки и тестирования (или иметь отдельный набор данных для каждого).
6. Выберите один или несколько алгоритмов машинного обучения в зависимости от hello обучения toosolve проблему. Например, двоичная классификация, мультиклассовая классификация, регрессия.
7. Обучение одной или нескольких моделей с помощью hello обучающий набор данных.
8. Оценка hello проверочного набора данных с помощью обученной модели hello.
9. Оцените hello модели toocompute hello соответствующие метрики для изучения проблемы hello.
10. Настройка модели hello и выберите hello наиболее toodeploy модели.

В этом упражнении мы уже изучена разработан hello данные в хранилище данных SQL и решили tooingest размер образца hello в Azure ML. Вот toobuild процедуры hello один или несколько моделей прогнозирования hello.

1. Получение данных hello в Azure ML с помощью hello [импорта данных] [ import-data] модуля, доступные в hello **ввод и вывод данных** раздела. Дополнительные сведения см. в разделе hello [импорта данных] [ import-data] справочной странице модуля.
   
    ![Модуль "Импорт данных" в Машинном обучении Azure][17]
2. Выберите **базы данных SQL Azure** как hello **источника данных** в hello **свойства** панель.
3. Введите имя DNS hello базы данных в hello **имя сервера базы данных** поля. Формат: `tcp:<your_virtual_machine_DNS_name>,1433`
4. Введите hello **имя базы данных** в соответствующее поле hello.
5. Введите hello *имя пользователя SQL* в hello **имя учетной записи пользователя сервера**и hello *пароль* в hello **пароль учетной записи пользователя сервера**.
6. Проверьте hello **принимать любой сертификат сервера** параметр.
7. В hello **запроса базы данных** Измените текстовое поле, вставьте запрос hello какие извлекает hello необходимые поля (включая все вычисляемые поля, такие как метки hello) базы данных и вниз образцы размер выборки toohello требуемого hello данных.

Пример эксперимента двоичной классификации, чтение данных непосредственно из базы данных хранилища данных SQL hello: hello рисунке (Помните tooreplace hello имена таблиц nyctaxi_trip и nyctaxi_fare схемой hello имя и hello имена таблиц, который использовался в вашей Пошаговое руководство). Подобные эксперименты можно сконструировать для задач мультиклассовой классификации и регрессии.

![Чат Машинного обучения Azure][10]

> [!IMPORTANT]
> В hello моделирования данных по извлечению и выборки запроса примеры, приведенные в предыдущих разделах **все метки для моделирования упражнений hello трех включаются в запрос hello**. (Обязательный) в каждом hello моделирования упражнения важно слишком**исключить** hello ненужные метки для hello другие две проблемы и любые другие **целевой утечки**. Например, при использовании двоичной классификации, используйте метки hello **чаевых оставил зависимости** и исключить hello поля **совет\_класса**, **совет\_сумма**, и **общее\_сумма**. последний Hello оплачиваются утечки целевой, так как они предполагают совет hello.
> 
> tooexclude утечек целевой, или ненужных столбцов могут использовать hello [Выбор столбцов в наборе данных] [ select-columns] модуля или hello [редактирование метаданных] [ edit-metadata]. Дополнительные сведения см. на страницах справки модулей [Select Columns in Dataset][select-columns] (Выбор столбцов в наборе данных) и [Edit Metadata][edit-metadata] (Изменение метаданных).
> 
> 

## <a name="mldeploy"></a>Развертывание моделей в службе Машинного обучения Azure
Когда модель готова, можно легко развернуть его веб-службы непосредственно из эксперимента hello. Дополнительные сведения о развертывании веб-служб Azure ML см. в статье [Развертывание веб-службы Машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md).

toodeploy веб-службу, необходимо:

1. Создать эксперимент по количественной оценке.
2. Развертывание веб-службы hello.

оценки поэкспериментировать с toocreate **завершен** обучения, эксперимента, нажмите кнопку **создать ЭКСПЕРИМЕНТ ОЦЕНКИ** hello нижней панели действий.

![Система оценок Azure][18]

Машинное обучение Azure попытается toocreate эксперимент оценки на основе компонентов hello эксперимента обучения hello. В частности, она:

1. Сохранить обученную модель hello и удалите hello модели обучающих модулей.
2. Определение логических **входному порту** toorepresent hello требуется схема входных данных.
3. Определение логических **выходного порта** toorepresent hello ожидаемый web службы выходные данные схемы.

При создании оценки экспериментов hello, проверьте его и сделать при необходимости измените. Типичные корректировки — входного набора данных hello tooreplace или запроса с одним, что исключает поля меток, их будет недоступен при вызове службы hello. Это также размером хорошей практикой tooreduce hello hello входной набор данных или запроса tooa несколько записей, достаточно tooindicate hello входной схемы. Для порта вывода hello, он общие tooexclude всех полей ввода и включать только hello **меток оцененных значений** и **оцененных вероятностей** в выходных данных с помощью hello hello [Выбор столбцов в наборе данных ] [ select-columns] модуля.

В приведенном ниже рисунке hello предоставляется образец эксперимент оценки. Окончании toodeploy, нажмите кнопку hello **публикации веб-службы** кнопку hello нижней панели действий.

![Публикация Машинного обучения Azure][11]

## <a name="summary"></a>Сводка
toorecap то было выполнено в этом учебнике Пошаговое руководство, вы создали среде обработки и анализа данных Azure, работали с большой открытый набор данных переводить его через hello процесс обработки и анализа данных для группы, все возможности hello со обучение toomodel получения данных, а затем toohello развертывание веб-службы машинного обучения Azure.

### <a name="license-information"></a>Сведения о лицензии
Это пошаговое руководство по примеру и соответствующую ему коллекцию скриптов и IPython notebook(s) совместно корпорацией Майкрософт в рамках лицензии MIT hello. Проверьте файл LICENSE.txt hello в каталоге hello hello образца кода на GitHub для получения дополнительных сведений.

## <a name="references"></a>Ссылки
•    [Страница загрузки данных о поездках такси Нью-Йорка (Andrés Monroy)](http://www.andresmh.com/nyctaxitrips/)  
•    [Получение данных о поездках такси Нью-Йорка на основании FOIL (Chris Whong)](http://chriswhong.com/open-data/foil_nyc_taxi/)   
•    [Статистические данные о комиссионных сборах за аренду такси и лимузинов Нью-Йорка](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[1]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sqldw-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sqldw-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlscoring.png
[19]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_download_scripts.png
[20]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_load_data.png
[21]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azcopy-overwrite.png
[22]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-1.png
[23]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-2.png
[24]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-3.png
[25]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-4.png
[26]: ./media/machine-learning-data-science-process-sqldw-walkthrough/tip_class_hist_1.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
