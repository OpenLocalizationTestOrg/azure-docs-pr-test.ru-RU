---
title: "журналы aaaAnalyze веб-сайта, с помощью аналитики Озера данных Azure | Документы Microsoft"
description: "Узнайте, каким образом ведет журнал tooanalyze веб-сайта с помощью аналитики Озера данных. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 3a196735-d0d9-4deb-ba68-c4b3f3be8403
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: saveenr
ms.openlocfilehash: d27aaca95ed2b643cfed7a17b0066bf7fa4a1bf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a>Анализ журналов веб-сайта с помощью Azure Data Lake Analytics
Узнайте, как tooanalyze журналы веб-сайта, с помощью аналитики Озера данных, особенно для выяснения, какие источники возникли ошибки когда он пытался toovisit hello веб-сайта.

## <a name="prerequisites"></a>Предварительные требования
* **Visual Studio 2015 или Visual Studio 2013**.
* **[Средства Data Lake для Visual Studio](http://aka.ms/adltoolsvs)**.

    После установки средств Озера данных для Visual Studio, вы увидите **Озера данных** элемента в hello **средства** меню в Visual Studio:

    ![Меню U-SQL в Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* **Базовые знания об аналитике Озера данных и hello средства Озера данных для Visual Studio**. tooget к работе, см.:

  * [Разработка сценария U-SQL с помощью средств озера данных для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
* **Учетная запись Data Lake Analytics**.  Ознакомьтесь с разделом [Создание учетной записи Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).
* **Отправьте учетной записи аналитики Озера данных toohello hello образца данных.** В разделе [toocopy файлы образцов данных](data-lake-analytics-get-started-portal.md).

    toorun задания аналитики Озера данных, необходимо будет некоторые данные. Несмотря на то, что hello средств Озера данных поддерживает загрузку данных, используется hello портала tooupload hello образец данных toomake этого учебника toofollow проще.

## <a name="connect-tooazure"></a>Подключение tooAzure
Прежде чем создавать и тестировать сценарии любой U-SQL, необходимо сначала подключиться tooAzure.

**tooconnect tooData аналитики Озера**

1. Откройте Visual Studio.
2. Щелкните **Data Lake > Параметры и настройки**.
3. Нажмите кнопку **входа**, или **сменить пользователя** Если кто-то входа в систему и следуйте инструкциям hello.
4. Нажмите кнопку **ОК** tooclose hello диалогового окна Параметры и настройки.

**toobrowse учетные записи аналитики Озера данных**

1. В Visual Studio откройте **обозреватель серверов**, нажав клавиши **CTRL + ALT + S**.
2. В **обозревателе серверов** разверните **Azure**, а затем — **Data Lake Analytics**. Будет выведен список учетных записей аналитики озера данных, если они есть. Невозможно создать учетные записи аналитики Озера данных из hello studio. в разделе toocreate учетную запись, [Приступая к работе с аналитики Озера данных Azure, с помощью портала Azure](data-lake-analytics-get-started-portal.md) или [Приступая к работе с аналитики Озера данных Azure, с помощью Azure PowerShell](data-lake-analytics-get-started-powershell.md).

## <a name="develop-u-sql-application"></a>Разработка приложения U-SQL
Приложение U-SQL представляет собой главным образом сценарий U-SQL. toolearn Дополнительные сведения о U-SQL, в разделе [Приступая к работе с U-SQL](data-lake-analytics-u-sql-get-started.md).

Вы можете добавить приложение toohello определяемые пользователем операторы сложения.  Дополнительные сведения см. в статье [Разработка пользовательских операторов U-SQL для заданий аналитики озера данных](data-lake-analytics-u-sql-develop-user-defined-operators.md).

**toocreate и отправить задание аналитики Озера данных**

1. Нажмите кнопку hello **файл > Создать > проект**.
2. Выберите тип проекта U-SQL hello.

    ![Новый проект U-SQL в Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. Нажмите кнопку **ОК**. Visual Studio создает решение с помощью файла Script.usql.
4. Введите следующий скрипт в файл Script.usql hello hello:

        // Create a database for easy reuse, so you don't need tooread from a file every time.
        CREATE DATABASE IF NOT EXISTS SampleDBTutorials;

        // Create a Table valued function. TVF ensures that your jobs fetch data from hello weblog file with hello correct schema.
        DROP FUNCTION IF EXISTS SampleDBTutorials.dbo.WeblogsView;
        CREATE FUNCTION SampleDBTutorials.dbo.WeblogsView()
        RETURNS @result TABLE
        (
            s_date DateTime,
            s_time string,
            s_sitename string,
            cs_method string,
            cs_uristem string,
            cs_uriquery string,
            s_port int,
            cs_username string,
            c_ip string,
            cs_useragent string,
            cs_cookie string,
            cs_referer string,
            cs_host string,
            sc_status int,
            sc_substatus int,
            sc_win32status int,
            sc_bytes int,
            cs_bytes int,
            s_timetaken int
        )
        AS
        BEGIN

            @result = EXTRACT
                s_date DateTime,
                s_time string,
                s_sitename string,
                cs_method string,
                cs_uristem string,
                cs_uriquery string,
                s_port int,
                cs_username string,
                c_ip string,
                cs_useragent string,
                cs_cookie string,
                cs_referer string,
                cs_host string,
                sc_status int,
                sc_substatus int,
                sc_win32status int,
                sc_bytes int,
                cs_bytes int,
                s_timetaken int
            FROM @"/Samples/Data/WebLog.log"
            USING Extractors.Text(delimiter:' ');
            RETURN;
        END;

        // Create a table for storing referrers and status
        DROP TABLE IF EXISTS SampleDBTutorials.dbo.ReferrersPerDay;
        @weblog = SampleDBTutorials.dbo.WeblogsView();
        CREATE TABLE SampleDBTutorials.dbo.ReferrersPerDay
        (
            INDEX idx1
            CLUSTERED(Year ASC)
            DISTRIBUTED BY HASH(Year)
        ) AS

        SELECT s_date.Year AS Year,
            s_date.Month AS Month,
            s_date.Day AS Day,
            cs_referer,
            sc_status,
            COUNT(DISTINCT c_ip) AS cnt
        FROM @weblog
        GROUP BY s_date,
                cs_referer,
                sc_status;

    hello toounderstand U-SQL, в разделе [приступить к работе с языком U-SQL аналитики Озера данных](data-lake-analytics-u-sql-get-started.md).    
5. Добавьте новый проект tooyour скрипт U-SQL и введите hello следующие данные:

        // Query hello referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        too@"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. Перейдите назад toohello первый скрипт U-SQL и далее toohello **отправить** кнопку, укажите учетную запись аналитики.
7. В **обозревателе решений** щелкните правой кнопкой мыши файл **Script.usql** и выберите команду **Build Script** (Создать сценарий). Проверьте результаты hello в области вывода hello.
8. В **обозревателе решений** щелкните правой кнопкой мыши файл **Script.usql** и выберите команду **Submit Script** (Отправить сценарий).
9. Проверьте hello **учетной записи аналитики** — hello одно где toorun hello задание и нажмите кнопку **отправить**. Отправка результатов и ссылку на задание доступны в hello Озера Data Tools для Visual Studio результаты окна, после завершения отправки hello.
10. Дождитесь успешного завершения задания hello.  Если произошел сбой задания hello, скорее всего отсутствует hello исходного файла.  См. в разделе hello готовности к установке разделе этого учебника. Дополнительные сведения об устранении неполадок см. в статье [Мониторинг и устранение неполадок заданий аналитики озера данных Azure](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).

    После завершения задания hello отобразится следующий экран приветствия:

    ![аналитика озера данных анализ веб-журналов журналы веб-сайтов](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. Теперь повторите шаги 7–10 для файла **Script1.usql**.

**выходные данные задания toosee hello**

1. Из **обозревателя серверов**, разверните **Azure**, разверните **аналитики Озера данных**разверните учетной записи аналитики Озера данных, разверните **учетных записей хранилища**, щелкните правой кнопкой мыши учетную запись хранилища Озера данных по умолчанию hello и нажмите кнопку **Explorer**.
2. Дважды щелкните **образцы** tooopen hello папки, а затем дважды щелкните **выходов**.
3. Дважды щелкните файл **UnsuccessfulResponsees.log**.
4. Можно также дважды щелкнуть hello выходного файла в представление графика hello задания hello в порядке toonavigate напрямую toohello выходных данных.

## <a name="see-also"></a>См. также
в разделе tooget к выполнению аналитики Озера данных с помощью различных средств:

* [Начало работы с аналитикой озера данных с помощью портала Azure](data-lake-analytics-get-started-portal.md)
* [Начало работы с аналитикой озера данных с помощью Azure PowerShell](data-lake-analytics-get-started-powershell.md)
* [Начало работы с аналитикой озера данных с помощью пакета SDK .NET.](data-lake-analytics-get-started-net-sdk.md)
