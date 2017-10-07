---
title: "Приступая к работе aaaAzure хранилище данных SQL - учебник | Документы Microsoft"
description: "В этом учебнике показано как tooprovision и загрузка данных в хранилище данных SQL Azure. Вы также узнаете hello основные сведения о масштабировании, приостановка и настройке."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: barbkess
ms.assetid: 52DFC191-E094-4B04-893F-B64D5828A900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: quickstart
ms.date: 01/26/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: edd2a21b0fe49ca8e9792c7c512310339a822c55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-data-warehouse"></a>Начало работы с хранилищем данных SQL

В этом учебнике показано как tooprovision и загрузка данных в хранилище данных SQL Azure. Вы также узнаете hello основные сведения о масштабировании, приостановка и настройке. После завершения вам быть готовы tooquery и просмотр хранилища данных.

**Предполагаемое время toocomplete:** это учебник законченный пример кода, принимающий toocomplete около 30 минут после выполнены необходимые условия hello. 

## <a name="prerequisites"></a>Предварительные требования

Hello учебнике предполагается, что вы знакомы с основными понятиями хранилище данных SQL. Если это не так, рекомендуем прочитать статью [Что такое хранилище данных SQL](sql-data-warehouse-overview-what-is.md). 

### <a name="sign-up-for-microsoft-azure"></a>Зарегистрируйтесь для Microsoft Azure
Если у вас еще нет учетной записи Microsoft Azure, вы должны toosign для использования одного toouse этой службы. Если у вас уже есть учетная запись, этот шаг можно пропустить. 

1. Переходить по страницам учетной записи toohello [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)
2. Создайте бесплатную учетную запись Azure или купите платную.
3. Следуйте инструкциям hello

### <a name="install-appropriate-sql-client-drivers-and-tools"></a>Установка соответствующих клиентских драйверов и средств SQL

Большая часть клиентских средств SQL можно подключаться tooSQL хранилища данных с помощью JDBC, ODBC или ADO.NET. Из-за toohello большое количество функций T-SQL, которые поддерживает хранилище данных SQL для некоторых клиентских приложений не полностью совместимы с хранилищем данных SQL.

Если вы работаете с ОС Windows, рекомендуем использовать либо [Visual Studio], либо [SQL Server Management Studio].

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a>Создание хранилища данных SQL

Хранилище данных SQL — это специальный тип базы данных, предназначенный для вычислений массовым параллелизмом. Hello базы данных, распределенные по нескольким узлам и обрабатывает запросы параллельно. Хранилище данных SQL имеет узел элемента управления, который координирует действия hello всех узлов hello. сами по себе узлы Hello использования базы данных SQL toomanage данных.  

> [!NOTE]
> Создание хранилища данных SQL может привести к дополнительным расходам.  Дополнительные сведения см. на странице [цен на хранилище данных SQL](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).
>

### <a name="create-a-data-warehouse"></a>Создание хранилища данных

1. Вход в hello [портал Azure](https://portal.azure.com).
2. Последовательно выберите **Создать** > **Базы данных** > **Хранилище данных SQL**.

    ![Новая колонка](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![Выбор хранилища данных](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)

3. Укажите сведения о развертывании.

    **Имя базы данных**: выберите любое имя. При наличии нескольких хранилищ данных, рекомендуется в именах включают сведения, например по региону hello, среда, например *mydw-westus-1-тестирование*.

    **Подписка**: ваша подписка Azure.

    **Группа ресурсов**: создайте группу ресурсов или выберите имеющуюся.
    > [!NOTE]
    > Группы ресурсов можно использовать для администрирования ресурсов, например для определения области управления доступом или развертывания по шаблону. Дополнительные сведения о группах ресурсов Azure и рекомендации см. [здесь](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).

    **Источник**: пустая база данных.

    **Сервер**: выберите hello сервера, созданный в [необходимых компонентов].

    **Параметры сортировки**: оставьте параметры сортировки по умолчанию hello SQL_Latin1_General_CP1_CI_AS.

    **Выберите «производительность»**: рекомендуется начинать с Стандартная 400DWU hello.

4. Выберите **toodashboard ПИН-код** ![tooDashboard ПИН-кода](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)

5. Получайте и подождите, пока ваш toodeploy хранилища данных! Это нормально, этот процесс tootake несколько минут. Hello портала уведомляет о готовности toouse является хранилищем данных. 

## <a name="connect-toosql-data-warehouse"></a>Подключение tooSQL хранилища данных

В этом учебнике используется хранилище данных SQL Server Management Studio (SSMS) tooconnect toohello. TooSQL хранилища данных могут подключаться через эти поддерживаемые соединители: ADO.NET, JDBC, PHP и ODBC. Помните, что функциональные возможности средств, не поддерживаемых Майкрософт, могут быть ограничены.


### <a name="get-connection-information"></a>Получение сведений о подключении

хранилище данных tooyour tooconnect, требуется tooconnect посредством hello логических SQL server был создан в [необходимых компонентов].

1. Выберите хранилище данных из панели мониторинга hello или выполните поиск в файлы ресурсов.

    ![Панель мониторинга хранилища данных SQL](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. Найти hello полное имя для логического сервера SQL hello.

    ![Выбор имени сервера](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. Откройте SSMS и использовать объект explorer tooconnect toothis сервер с использованием учетных данных администратора сервера hello вы создали в [необходимых компонентов]

    ![Подключение с помощью SSMS](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

Если все сделано правильно, должна появиться подключенных tooyour логического сервера SQL. Так как вы вошли в как Здравствуйте, администратор сервера, можно подключить tooany базы данных, размещенные на сервере hello, включая базы данных master hello. 

Учетная запись администратора только один сервер, и имеет hello большинство права пользователя. Будьте внимательны не tooallow слишком много пользователей в вашей организации пароль администратора hello tooknow. 

Также у вас может быть учетная запись администратора Azure Active Directory. Мы не предоставляем hello здесь сведения о нем. Дополнительные сведения об использовании проверки подлинности Azure Active Directory toolearn см [проверки подлинности Azure AD](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).

Далее мы рассмотрим создание дополнительных пользователей и имен для входа.


## <a name="create-a-database-user"></a>Создание пользователя базы данных

На этом шаге создается tooaccess учетной записи пользователя хранилища данных. Мы также показано, как toogive toorun возможность hello этот пользователь запрашивает с большим объемом памяти и ресурсов ЦП.

### <a name="notes-about-resource-classes-for-allocating-resources-tooqueries"></a>Заметки о классах ресурсов при выделении ресурсов tooqueries

- tookeep safe, данные не используются hello сервера администрирования toorun запросы на производственных баз данных. Он имеет hello большинство привилегий любой пользователь, и с помощью tooperform операции с данными пользователя помещает данные под угрозой. Кроме того поскольку Здравствуйте, администратор сервера должен tooperform операций управления, он выполняет операции с небольшой выделения памяти и ресурсов ЦП. 

- Хранилище данных SQL использует роли предварительно определенные базы данных, вызывается классами ресурсов, tooallocate различного объема памяти, ресурсы ЦП и toousers слоты параллелизма. Каждый пользователь может принадлежать tooa небольшой, средний, большой или очень большой ресурсов класса. Hello класс ресурсов пользователя определяет hello ресурсы hello пользователя toorun запросов и операций загрузки.

- При использовании сжатия данных оптимальной hello пользователя, необходимо tooload с большими или очень больших выделений. Дополнительные сведения о классах ресурсов см. [здесь](./sql-data-warehouse-develop-concurrency.md#resource-classes).

### <a name="create-an-account-that-can-control-a-database"></a>Создание учетной записи, позволяющей управлять базой данных

Поскольку вы выполнили вход в Здравствуйте, администратор сервера имеется разрешения toocreate входа и пользователей.

1. Используя SSMS или другой клиент запросов, откройте новый запрос к базе данных **master**.

    ![Создание запроса к базе данных master](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![Создание запроса к базе данных master1](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. В окне запроса hello запустите этот toocreate команды T-SQL, имя MedRCLogin входа и пользователя с именем LoadingUser. Это имя входа можно подключиться toohello логического сервера SQL.

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. Теперь запрос hello *базы данных хранилища данных SQL*, создание пользователя базы данных, на hello входа, созданного tooaccess и выполнять операции над hello базы данных.

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. Дать hello базы данных пользовательского элемента управления разрешения toohello базы данных называется NYT. 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] tooLoadingUser;
    ```
    > [!NOTE]
    > Если имя базы данных содержит дефисы, быть toowrap убедиться, что его в квадратные скобки. 
    >

### <a name="give-hello-user-medium-resource-allocations"></a>Предоставьте hello пользователя средний выделений

1. Запустите этот toomake команды T-SQL ИТ член класса средний ресурсов hello, которая называется mediumrc. 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > Нажмите кнопку [здесь](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn Дополнительные сведения о классах параллелизма и ресурсов. 
    >

2. Подключение toohello логическом сервере с новыми учетными данными hello

    ![Вход с помощью новых учетных данных](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a>Загрузка данных из хранилища больших двоичных объектов Azure

Теперь вы находитесь tooload готовности данных в хранилище данных. Этот шаг показывает, как tooload Нью-Йорк такси CAB-файла данных из открытых хранилища Azure BLOB-объектов. 

- Чаще всего tooload данных в хранилище данных SQL является toofirst переместить хранилище больших двоичных объектов tooAzure данных hello и затем загрузить в хранилище данных. toomake его проще toounderstand как tooload, у нас есть Нью-Йорк такси CAB-файла данных, уже размещенные в большой двоичный объект открытого хранилища Azure. 

- Для дальнейшего использования, toolearn как tooget вашей tooAzure данные больших двоичных объектов хранилища или tooload его непосредственно из источника в хранилище данных SQL, в разделе hello [Общие сведения о загрузке](sql-data-warehouse-overview-load.md).


### <a name="define-external-data"></a>Определение внешних данных

1. Создайте главный ключ. Требуется только toocreate главного ключа, чем один раз в базе данных. 

    ```sql
    CREATE MASTER KEY;
    ```

2. Определение расположения hello hello Azure BLOB-объект, содержащий hello такси CAB-файла данных.  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. Определение hello внешние форматы файлов

    Hello ```CREATE EXTERNAL FILE FORMAT``` команда является toospecify используется формат файлов, содержащих hello внешних данных. Эти файлы содержат текст, разделенный одним или несколькими символами, которые называются разделителями. В целях демонстрации hello такси CAB-файла данных хранится как несжатых данных и как gzip сжатых данных.

    Выполнение этих двух различных форматов toodefine команды T-SQL: распаковки и сжатые.

    ```sql
    CREATE EXTERNAL FILE FORMAT uncompressedcsv
    WITH (
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( 
            FIELD_TERMINATOR = ',',
            STRING_DELIMITER = '',
            DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        )
    );

    CREATE EXTERNAL FILE FORMAT compressedcsv
    WITH ( 
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( FIELD_TERMINATOR = '|',
            STRING_DELIMITER = '',
        DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        ),
        DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
    );
    ```

4.  Создайте схему для формата внешних файлов. 

    ```sql
    CREATE SCHEMA ext;
    ```
5. Создание внешних таблиц hello. Эти таблицы ссылаются на данные, содержащиеся в хранилище BLOB-объектов Azure. Запустите hello, следуя toocreate команды T-SQL несколько внешних таблиц, что все точки toohello BLOB-объектов Azure мы определили ранее в нашем внешнего источника данных.

```sql
    CREATE EXTERNAL TABLE [ext].[Date] 
    (
        [DateID] int NOT NULL,
        [Date] datetime NULL,
        [DateBKey] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DaySuffix] varchar(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeek] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfQuarter] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfYear] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfMonth] varchar(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Month] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Quarter] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [QuarterName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Year] char(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [YearName] char(7) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthYear] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MMYYYY] char(6) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FirstDayOfMonth] date NULL,
        [LastDayOfMonth] date NULL,
        [FirstDayOfQuarter] date NULL,
        [LastDayOfQuarter] date NULL,
        [FirstDayOfYear] date NULL,
        [LastDayOfYear] date NULL,
        [IsHolidayUSA] bit NULL,
        [IsWeekday] bit NULL,
        [HolidayUSA] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Date',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    );
    
    CREATE EXTERNAL TABLE [ext].[Geography]
    (
        [GeographyID] int NOT NULL,
        [ZipCodeBKey] varchar(10) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [County] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [City] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [State] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Country] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [ZipCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Geography',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0 
    );
        
    
    CREATE EXTERNAL TABLE [ext].[HackneyLicense]
    (
        [HackneyLicenseID] int NOT NULL,
        [HackneyLicenseBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HackneyLicenseCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'HackneyLicense',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    
    CREATE EXTERNAL TABLE [ext].[Medallion]
    (
        [MedallionID] int NOT NULL,
        [MedallionBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [MedallionCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Medallion',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    CREATE EXTERNAL TABLE [ext].[Time]
    (
        [TimeID] int NOT NULL,
        [TimeBKey] varchar(8) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HourNumber] tinyint NOT NULL,
        [MinuteNumber] tinyint NOT NULL,
        [SecondNumber] tinyint NOT NULL,
        [TimeInSecond] int NOT NULL,
        [HourlyBucket] varchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [DayTimeBucketGroupKey] int NOT NULL,
        [DayTimeBucket] varchar(100) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL
    )
    WITH
    (
        LOCATION = 'Time',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    
    CREATE EXTERNAL TABLE [ext].[Trip]
    (
        [DateID] int NOT NULL,
        [MedallionID] int NOT NULL,
        [HackneyLicenseID] int NOT NULL,
        [PickupTimeID] int NOT NULL,
        [DropoffTimeID] int NOT NULL,
        [PickupGeographyID] int NULL,
        [DropoffGeographyID] int NULL,
        [PickupLatitude] float NULL,
        [PickupLongitude] float NULL,
        [PickupLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DropoffLatitude] float NULL,
        [DropoffLongitude] float NULL,
        [DropoffLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [PassengerCount] int NULL,
        [TripDurationSeconds] int NULL,
        [TripDistanceMiles] float NULL,
        [PaymentType] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FareAmount] money NULL,
        [SurchargeAmount] money NULL,
        [TaxAmount] money NULL,
        [TipAmount] money NULL,
        [TollsAmount] money NULL,
        [TotalAmount] money NULL
    )
    WITH
    (
        LOCATION = 'Trip2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = compressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    CREATE EXTERNAL TABLE [ext].[Weather]
    (
        [DateID] int NOT NULL,
        [GeographyID] int NOT NULL,
        [PrecipitationInches] float NOT NULL,
        [AvgTemperatureFahrenheit] float NOT NULL
    )
    WITH
    (
        LOCATION = 'Weather2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
```

### <a name="import-hello-data-from-azure-blob-storage"></a>Импорт данных hello из хранилища BLOB-объектов Azure.

Хранилище данных SQL поддерживает ключевую инструкцию CREATE TABLE AS SELECT (CTAS). Эта инструкция создает новую таблицу на основе результатов hello инструкции select. Hello новая таблица содержит hello же столбцы и типы данных, как инструкция select hello результаты hello.  Это данные может надлежащим образом tooimport из хранилища BLOB-объектов Azure в хранилище данных SQL.

1. Запустите этот скрипт tooimport данных.

    ```sql
    CREATE TABLE [dbo].[Date]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Date]
    OPTION (LABEL = 'CTAS : Load [dbo].[Date]')
    ;
    
    CREATE TABLE [dbo].[Geography]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS
    SELECT * FROM [ext].[Geography]
    OPTION (LABEL = 'CTAS : Load [dbo].[Geography]')
    ;
    
    CREATE TABLE [dbo].[HackneyLicense]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[HackneyLicense]
    OPTION (LABEL = 'CTAS : Load [dbo].[HackneyLicense]')
    ;
    
    CREATE TABLE [dbo].[Medallion]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Medallion]
    OPTION (LABEL = 'CTAS : Load [dbo].[Medallion]')
    ;
    
    CREATE TABLE [dbo].[Time]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Time]
    OPTION (LABEL = 'CTAS : Load [dbo].[Time]')
    ;
    
    CREATE TABLE [dbo].[Weather]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Weather]
    OPTION (LABEL = 'CTAS : Load [dbo].[Weather]')
    ;
    
    CREATE TABLE [dbo].[Trip]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Trip]
    OPTION (LABEL = 'CTAS : Load [dbo].[Trip]')
    ;
    ```

2. Просмотрите данные при загрузке.

   Вы загружаете несколько гигабайт данных и сжимаете их в высокопроизводительные кластеризованные индексы Columnstore. Выполните следующий запрос, использующий hello динамические административные представления (DMV) tooshow состояние загрузки hello hello. После запуска запроса hello, захватите кофе и перекусить, а хранилище данных SQL некоторых сложных задач.
    
    ```sql
    SELECT
        r.command,
        s.request_id,
        r.status,
        count(distinct input_name) as nbr_files,
        sum(s.bytes_processed)/1024/1024/1024 as gb_processed
    FROM 
        sys.dm_pdw_exec_requests r
        INNER JOIN sys.dm_pdw_dms_external_work s
        ON r.request_id = s.request_id
    WHERE
        r.[label] = 'CTAS : Load [dbo].[Date]' OR
        r.[label] = 'CTAS : Load [dbo].[Geography]' OR
        r.[label] = 'CTAS : Load [dbo].[HackneyLicense]' OR
        r.[label] = 'CTAS : Load [dbo].[Medallion]' OR
        r.[label] = 'CTAS : Load [dbo].[Time]' OR
        r.[label] = 'CTAS : Load [dbo].[Weather]' OR
        r.[label] = 'CTAS : Load [dbo].[Trip]'
    GROUP BY
        r.command,
        s.request_id,
        r.status
    ORDER BY
        nbr_files desc, 
        gb_processed desc;
    ```

3. Просмотрите все запросы в системе.

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. Посмотрите, как данные упорядоченно загружаются в хранилище данных SQL Azure.

    ![Просмотр загрузки данных](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a>Повышение производительности запросов

Существует несколько способов tooimprove производительность и tooachieve hello высокоскоростной производительность хранилище данных SQL — предназначен tooprovide.  

### <a name="see-hello-effect-of-scaling-on-query-performance"></a>В разделе hello влияние на производительность запросов 

Одним из способов tooimprove производительность запросов является tooscale ресурсы, изменив hello DWU уровня обслуживания хранилища данных. Каждый уровень обслуживания стоит дороже, но вы можете выполнить обратное масштабирование или приостановить ресурсы в любое время. 

На этом шаге сравнивается производительность при двух различных настройках DWU.

Во-первых, давайте масштабировать изменения размера hello вниз too100 DWU, поэтому мы можем получить представление о влиянии одного вычислительного узла может выполняться самостоятельно.

1. Портал toohello перейти и выбрать хранилище данных SQL.

2. Выберите масштаб в колонке hello хранилище данных SQL. 

    ![Масштабирование хранилища данных на портале](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. Масштабировать производительность hello панели too100 DWU и нажмите Сохранить.

    ![Масштабирование и сохранение](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. Подождите, пока ваш toofinish операции масштабирования.

    > [!NOTE]
    > Запросы, не может выполняться при изменении масштаба hello. Процедура масштабирования **прерывает** выполняющиеся запросы. Вы можете перезапустить их после завершения операции hello.
    >
    
5. Выполните операцию просмотра данных trip hello и выборе hello top миллионов записей для всех столбцов hello. Если вы упреждающая toomove на быстро, вы бесплатно tooselect меньшее число строк. Запишите hello время, затрачиваемое toorun этой операции.

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. Масштабировать хранилища данных обратно too400 DWU. Помните, что каждый 100 DWU состоит в добавлении другой вычислительный узел tooyour хранилище данных SQL Azure.

7. Снова запустите запрос hello! Вы заметите существенную разницу. 

    > [!NOTE]
    > Поскольку hello запрос возвращает большое количество данных, доступной пропускной способности hello машины hello SSMS может быть узким местом производительности. Это может привести к тому, что вы вообще не заметите повышения производительности.

> [!NOTE]
> Хранилище данных SQL использует массовую параллельную обработку. Запросы, которые сканирования или выполнять аналитические функции на миллионы строк использовать hello true возможности хранилища данных SQL Azure.
>

### <a name="see-hello-effect-of-statistics-on-query-performance"></a>Увидеть эффект hello статистики по производительности запросов

1. Выполнить запрос, что соединения hello таблицы дат с таблицей Trip hello

    ```sql
    SELECT TOP (1000000) 
        dt.[DayOfWeek],
        tr.[MedallionID],
        tr.[HackneyLicenseID],
        tr.[PickupTimeID],
        tr.[DropoffTimeID],
        tr.[PickupGeographyID],
        tr.[DropoffGeographyID],
        tr.[PickupLatitude],
        tr.[PickupLongitude],
        tr.[PickupLatLong],
        tr.[DropoffLatitude],
        tr.[DropoffLongitude],
        tr.[DropoffLatLong],
        tr.[PassengerCount],
        tr.[TripDurationSeconds],
        tr.[TripDistanceMiles],
        tr.[PaymentType],
        tr.[FareAmount],
        tr.[SurchargeAmount],
        tr.[TaxAmount],
        tr.[TipAmount],
        tr.[TollsAmount],
        tr.[TotalAmount]
    FROM [dbo].[Trip] as tr
        JOIN dbo.[Date] as dt
        ON  tr.DateID = dt.DateID
    ```

    Этот запрос требует некоторое время, так как хранилище данных SQL имеет tooshuffle данных, прежде чем выполнить hello соединения. Соединения не содержат данных tooshuffle одинаковых данных спроектированный toojoin в hello так же, как он распространяется. Для этого вопроса следует ознакомиться с более подробной информацией. 

2. Статистика имеет значение. 
3. Запустите toocreate этой инструкции статистику по столбцам соединения hello.

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > Хранилище данных SQL не управляет статистикой автоматически. Статистика важна для производительности запросов, поэтому мы настоятельно рекомендуем создавать и обновлять статистику.
    > 
    > **Вы получите hello максимальную выгоду, наличие статистики для столбцов, участвующих в соединениях, столбцов, используемых в hello обнаружено предложение и столбцы в GROUP BY.**
    >

3. Снова запустите запрос hello необходимых компонентов и понаблюдайте за разницу в производительности. При hello различия в производительности запросов не будет как радикальных как вертикальное масштабирование, вы заметите, что индексацию. 

## <a name="next-steps"></a>Дальнейшие действия

Теперь вы готовы tooquery и исследование. Ознакомьтесь с нашими советами и рекомендациями.

После завершения работы изучение день hello, сделать toopause убедиться, что экземпляр! В рабочей среде, то могут экономить огромные путем приостановки и масштабирование toomeet потребностям бизнеса.

![Приостановить](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a>Полезные ссылки

[Управление параллелизмом и рабочей нагрузкой в хранилище данных SQL][]

[Рекомендации по использованию хранилища данных SQL Azure][]

[Мониторинг рабочей нагрузки с помощью динамических административных представлений][]

[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][] (10 лучших рекомендаций по созданию реляционного хранилища данных большого объема)

[Миграция данных tooAzure хранилище данных SQL][]

[Управление параллелизмом и рабочей нагрузкой в хранилище данных SQL]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Рекомендации по использованию хранилища данных SQL Azure]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[Мониторинг рабочей нагрузки с помощью динамических административных представлений]: sql-data-warehouse-manage-monitor.md
[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/ (10 лучших рекомендаций по созданию реляционного хранилища данных большого объема)
[Миграция данных tooAzure хранилище данных SQL]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[необходимых компонентов]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
