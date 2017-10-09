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
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a><span data-ttu-id="267be-103">Анализ журналов веб-сайта с помощью Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="267be-103">Analyze Website logs using Azure Data Lake Analytics</span></span>
<span data-ttu-id="267be-104">Узнайте, как tooanalyze журналы веб-сайта, с помощью аналитики Озера данных, особенно для выяснения, какие источники возникли ошибки когда он пытался toovisit hello веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="267be-104">Learn how tooanalyze website logs using Data Lake Analytics, especially on finding out which referrers ran into errors when they tried toovisit hello website.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="267be-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="267be-105">Prerequisites</span></span>
* <span data-ttu-id="267be-106">**Visual Studio 2015 или Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="267be-106">**Visual Studio 2015 or Visual Studio 2013**.</span></span>
* <span data-ttu-id="267be-107">**[Средства Data Lake для Visual Studio](http://aka.ms/adltoolsvs)**.</span><span class="sxs-lookup"><span data-stu-id="267be-107">**[Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)**.</span></span>

    <span data-ttu-id="267be-108">После установки средств Озера данных для Visual Studio, вы увидите **Озера данных** элемента в hello **средства** меню в Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="267be-108">Once Data Lake Tools for Visual Studio is installed, you will see a **Data Lake** item in hello **Tools** menu in Visual Studio:</span></span>

    ![Меню U-SQL в Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* <span data-ttu-id="267be-110">**Базовые знания об аналитике Озера данных и hello средства Озера данных для Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="267be-110">**Basic knowledge of Data Lake Analytics and hello Data Lake Tools for Visual Studio**.</span></span> <span data-ttu-id="267be-111">tooget к работе, см.:</span><span class="sxs-lookup"><span data-stu-id="267be-111">tooget started, see:</span></span>

  * <span data-ttu-id="267be-112">[Разработка сценария U-SQL с помощью средств озера данных для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="267be-112">[Develop U-SQL script using Data Lake tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="267be-113">**Учетная запись Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="267be-113">**A Data Lake Analytics account.**</span></span>  <span data-ttu-id="267be-114">Ознакомьтесь с разделом [Создание учетной записи Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="267be-114">See [Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="267be-115">**Отправьте учетной записи аналитики Озера данных toohello hello образца данных.**</span><span class="sxs-lookup"><span data-stu-id="267be-115">**Upload hello sample data toohello Data Lake Analytics account.**</span></span> <span data-ttu-id="267be-116">В разделе [toocopy файлы образцов данных](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="267be-116">See [toocopy sample data files](data-lake-analytics-get-started-portal.md).</span></span>

    <span data-ttu-id="267be-117">toorun задания аналитики Озера данных, необходимо будет некоторые данные.</span><span class="sxs-lookup"><span data-stu-id="267be-117">toorun a Data Lake Analytics job, you will need some data.</span></span> <span data-ttu-id="267be-118">Несмотря на то, что hello средств Озера данных поддерживает загрузку данных, используется hello портала tooupload hello образец данных toomake этого учебника toofollow проще.</span><span class="sxs-lookup"><span data-stu-id="267be-118">Even though hello Data Lake Tools supports uploading data, you will use hello portal tooupload hello sample data toomake this tutorial easier toofollow.</span></span>

## <a name="connect-tooazure"></a><span data-ttu-id="267be-119">Подключение tooAzure</span><span class="sxs-lookup"><span data-stu-id="267be-119">Connect tooAzure</span></span>
<span data-ttu-id="267be-120">Прежде чем создавать и тестировать сценарии любой U-SQL, необходимо сначала подключиться tooAzure.</span><span class="sxs-lookup"><span data-stu-id="267be-120">Before you can build and test any U-SQL scripts, you must first connect tooAzure.</span></span>

<span data-ttu-id="267be-121">**tooconnect tooData аналитики Озера**</span><span class="sxs-lookup"><span data-stu-id="267be-121">**tooconnect tooData Lake Analytics**</span></span>

1. <span data-ttu-id="267be-122">Откройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="267be-122">Open Visual Studio.</span></span>
2. <span data-ttu-id="267be-123">Щелкните **Data Lake > Параметры и настройки**.</span><span class="sxs-lookup"><span data-stu-id="267be-123">Click **Data Lake > Options and Settings**.</span></span>
3. <span data-ttu-id="267be-124">Нажмите кнопку **входа**, или **сменить пользователя** Если кто-то входа в систему и следуйте инструкциям hello.</span><span class="sxs-lookup"><span data-stu-id="267be-124">Click **Sign In**, or **Change User** if someone has signed in, and follow hello instructions.</span></span>
4. <span data-ttu-id="267be-125">Нажмите кнопку **ОК** tooclose hello диалогового окна Параметры и настройки.</span><span class="sxs-lookup"><span data-stu-id="267be-125">Click **OK** tooclose hello Options and Settings dialog.</span></span>

<span data-ttu-id="267be-126">**toobrowse учетные записи аналитики Озера данных**</span><span class="sxs-lookup"><span data-stu-id="267be-126">**toobrowse your Data Lake Analytics accounts**</span></span>

1. <span data-ttu-id="267be-127">В Visual Studio откройте **обозреватель серверов**, нажав клавиши **CTRL + ALT + S**.</span><span class="sxs-lookup"><span data-stu-id="267be-127">From Visual Studio, open **Server Explorer** by press **CTRL+ALT+S**.</span></span>
2. <span data-ttu-id="267be-128">В **обозревателе серверов** разверните **Azure**, а затем — **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="267be-128">From **Server Explorer**, expand **Azure**, and then expand **Data Lake Analytics**.</span></span> <span data-ttu-id="267be-129">Будет выведен список учетных записей аналитики озера данных, если они есть.</span><span class="sxs-lookup"><span data-stu-id="267be-129">You shall see a list of your Data Lake Analytics accounts if there are any.</span></span> <span data-ttu-id="267be-130">Невозможно создать учетные записи аналитики Озера данных из hello studio.</span><span class="sxs-lookup"><span data-stu-id="267be-130">You cannot create Data Lake Analytics accounts from hello studio.</span></span> <span data-ttu-id="267be-131">в разделе toocreate учетную запись, [Приступая к работе с аналитики Озера данных Azure, с помощью портала Azure](data-lake-analytics-get-started-portal.md) или [Приступая к работе с аналитики Озера данных Azure, с помощью Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="267be-131">toocreate an account, see [Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md) or [Get Started with Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span></span>

## <a name="develop-u-sql-application"></a><span data-ttu-id="267be-132">Разработка приложения U-SQL</span><span class="sxs-lookup"><span data-stu-id="267be-132">Develop U-SQL application</span></span>
<span data-ttu-id="267be-133">Приложение U-SQL представляет собой главным образом сценарий U-SQL.</span><span class="sxs-lookup"><span data-stu-id="267be-133">A U-SQL application is mostly a U-SQL script.</span></span> <span data-ttu-id="267be-134">toolearn Дополнительные сведения о U-SQL, в разделе [Приступая к работе с U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="267be-134">toolearn more about U-SQL, see [Get started with U-SQL](data-lake-analytics-u-sql-get-started.md).</span></span>

<span data-ttu-id="267be-135">Вы можете добавить приложение toohello определяемые пользователем операторы сложения.</span><span class="sxs-lookup"><span data-stu-id="267be-135">You can add addition user-defined operators toohello application.</span></span>  <span data-ttu-id="267be-136">Дополнительные сведения см. в статье [Разработка пользовательских операторов U-SQL для заданий аналитики озера данных](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span><span class="sxs-lookup"><span data-stu-id="267be-136">For more information, see [Develop U-SQL user defined operators for Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span></span>

<span data-ttu-id="267be-137">**toocreate и отправить задание аналитики Озера данных**</span><span class="sxs-lookup"><span data-stu-id="267be-137">**toocreate and submit a Data Lake Analytics job**</span></span>

1. <span data-ttu-id="267be-138">Нажмите кнопку hello **файл > Создать > проект**.</span><span class="sxs-lookup"><span data-stu-id="267be-138">Click hello **File > New > Project**.</span></span>
2. <span data-ttu-id="267be-139">Выберите тип проекта U-SQL hello.</span><span class="sxs-lookup"><span data-stu-id="267be-139">Select hello U-SQL Project type.</span></span>

    ![Новый проект U-SQL в Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. <span data-ttu-id="267be-141">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="267be-141">Click **OK**.</span></span> <span data-ttu-id="267be-142">Visual Studio создает решение с помощью файла Script.usql.</span><span class="sxs-lookup"><span data-stu-id="267be-142">Visual studio creates a solution with a Script.usql file.</span></span>
4. <span data-ttu-id="267be-143">Введите следующий скрипт в файл Script.usql hello hello:</span><span class="sxs-lookup"><span data-stu-id="267be-143">Enter hello following script into hello Script.usql file:</span></span>

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

    <span data-ttu-id="267be-144">hello toounderstand U-SQL, в разделе [приступить к работе с языком U-SQL аналитики Озера данных](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="267be-144">toounderstand hello U-SQL, see [Get started with Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>    
5. <span data-ttu-id="267be-145">Добавьте новый проект tooyour скрипт U-SQL и введите hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="267be-145">Add a new U-SQL script tooyour project and enter hello following:</span></span>

        // Query hello referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        too@"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. <span data-ttu-id="267be-146">Перейдите назад toohello первый скрипт U-SQL и далее toohello **отправить** кнопку, укажите учетную запись аналитики.</span><span class="sxs-lookup"><span data-stu-id="267be-146">Switch back toohello first U-SQL script and next toohello **Submit** button, specify your Analytics account.</span></span>
7. <span data-ttu-id="267be-147">В **обозревателе решений** щелкните правой кнопкой мыши файл **Script.usql** и выберите команду **Build Script** (Создать сценарий).</span><span class="sxs-lookup"><span data-stu-id="267be-147">From **Solution Explorer**, right click **Script.usql**, and then click **Build Script**.</span></span> <span data-ttu-id="267be-148">Проверьте результаты hello в области вывода hello.</span><span class="sxs-lookup"><span data-stu-id="267be-148">Verify hello results in hello Output pane.</span></span>
8. <span data-ttu-id="267be-149">В **обозревателе решений** щелкните правой кнопкой мыши файл **Script.usql** и выберите команду **Submit Script** (Отправить сценарий).</span><span class="sxs-lookup"><span data-stu-id="267be-149">From **Solution Explorer**, right click **Script.usql**, and then click **Submit Script**.</span></span>
9. <span data-ttu-id="267be-150">Проверьте hello **учетной записи аналитики** — hello одно где toorun hello задание и нажмите кнопку **отправить**.</span><span class="sxs-lookup"><span data-stu-id="267be-150">Verify hello **Analytics Account** is hello one where you want toorun hello job, and then click **Submit**.</span></span> <span data-ttu-id="267be-151">Отправка результатов и ссылку на задание доступны в hello Озера Data Tools для Visual Studio результаты окна, после завершения отправки hello.</span><span class="sxs-lookup"><span data-stu-id="267be-151">Submission results and job link are available in hello Data Lake Tools for Visual Studio Results window when hello submission is completed.</span></span>
10. <span data-ttu-id="267be-152">Дождитесь успешного завершения задания hello.</span><span class="sxs-lookup"><span data-stu-id="267be-152">Wait until hello job is completed successfully.</span></span>  <span data-ttu-id="267be-153">Если произошел сбой задания hello, скорее всего отсутствует hello исходного файла.</span><span class="sxs-lookup"><span data-stu-id="267be-153">If hello job failed, it is most likely missing hello source file.</span></span>  <span data-ttu-id="267be-154">См. в разделе hello готовности к установке разделе этого учебника.</span><span class="sxs-lookup"><span data-stu-id="267be-154">Please see hello Prerequisite section of this tutorial.</span></span> <span data-ttu-id="267be-155">Дополнительные сведения об устранении неполадок см. в статье [Мониторинг и устранение неполадок заданий аналитики озера данных Azure](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="267be-155">For additional troubleshooting information, see [Monitor and troubleshoot Azure Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>

    <span data-ttu-id="267be-156">После завершения задания hello отобразится следующий экран приветствия:</span><span class="sxs-lookup"><span data-stu-id="267be-156">When hello job is completed, you shall see hello following screen:</span></span>

    ![аналитика озера данных анализ веб-журналов журналы веб-сайтов](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. <span data-ttu-id="267be-158">Теперь повторите шаги 7–10 для файла **Script1.usql**.</span><span class="sxs-lookup"><span data-stu-id="267be-158">Now repeat steps 7- 10 for **Script1.usql**.</span></span>

<span data-ttu-id="267be-159">**выходные данные задания toosee hello**</span><span class="sxs-lookup"><span data-stu-id="267be-159">**toosee hello job output**</span></span>

1. <span data-ttu-id="267be-160">Из **обозревателя серверов**, разверните **Azure**, разверните **аналитики Озера данных**разверните учетной записи аналитики Озера данных, разверните **учетных записей хранилища**, щелкните правой кнопкой мыши учетную запись хранилища Озера данных по умолчанию hello и нажмите кнопку **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="267be-160">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click hello default Data Lake Storage account, and then click **Explorer**.</span></span>
2. <span data-ttu-id="267be-161">Дважды щелкните **образцы** tooopen hello папки, а затем дважды щелкните **выходов**.</span><span class="sxs-lookup"><span data-stu-id="267be-161">Double-click **Samples** tooopen hello folder, and then double-click **Outputs**.</span></span>
3. <span data-ttu-id="267be-162">Дважды щелкните файл **UnsuccessfulResponsees.log**.</span><span class="sxs-lookup"><span data-stu-id="267be-162">Double-click **UnsuccessfulResponsees.log**.</span></span>
4. <span data-ttu-id="267be-163">Можно также дважды щелкнуть hello выходного файла в представление графика hello задания hello в порядке toonavigate напрямую toohello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="267be-163">You can also double-click hello output file inside hello graph view of hello job in order toonavigate directly toohello output.</span></span>

## <a name="see-also"></a><span data-ttu-id="267be-164">См. также</span><span class="sxs-lookup"><span data-stu-id="267be-164">See also</span></span>
<span data-ttu-id="267be-165">в разделе tooget к выполнению аналитики Озера данных с помощью различных средств:</span><span class="sxs-lookup"><span data-stu-id="267be-165">tooget started with Data Lake Analytics using different tools, see:</span></span>

* [<span data-ttu-id="267be-166">Начало работы с аналитикой озера данных с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="267be-166">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="267be-167">Начало работы с аналитикой озера данных с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="267be-167">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="267be-168">Начало работы с аналитикой озера данных с помощью пакета SDK .NET.</span><span class="sxs-lookup"><span data-stu-id="267be-168">Get started with Data Lake Analytics using .NET SDK</span></span>](data-lake-analytics-get-started-net-sdk.md)
