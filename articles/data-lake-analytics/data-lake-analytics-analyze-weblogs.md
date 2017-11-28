---
title: "Анализ журналов веб-сайта с помощью Azure Data Lake Analytics | Документация Майкрософт"
description: "Информация об анализе журналов веб-сайта с помощью аналитики озера данных Azure. "
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
ms.openlocfilehash: 25fbbe97d26491fc421f4821315761c18e523ec8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a><span data-ttu-id="d2ddb-103">Анализ журналов веб-сайта с помощью Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d2ddb-103">Analyze Website logs using Azure Data Lake Analytics</span></span>
<span data-ttu-id="d2ddb-104">Сведения об анализе журналов веб-сайтов с помощью службы аналитики озера, а также информация об источниках ссылок, которые столкнулись с ошибками во время попытки посетить веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-104">Learn how to analyze website logs using Data Lake Analytics, especially on finding out which referrers ran into errors when they tried to visit the website.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2ddb-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d2ddb-105">Prerequisites</span></span>
* <span data-ttu-id="d2ddb-106">**Visual Studio 2015 или Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-106">**Visual Studio 2015 or Visual Studio 2013**.</span></span>
* <span data-ttu-id="d2ddb-107">**[Средства Data Lake для Visual Studio](http://aka.ms/adltoolsvs)**.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-107">**[Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)**.</span></span>

    <span data-ttu-id="d2ddb-108">После установки Средств Data Lake для Visual Studio вы увидите пункт **Data Lake** в меню **Сервис** Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-108">Once Data Lake Tools for Visual Studio is installed, you will see a **Data Lake** item in the **Tools** menu in Visual Studio:</span></span>

    ![Меню U-SQL в Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* <span data-ttu-id="d2ddb-110">**Базовые знания о Data Lake Analytics и инструментах Data Lake для Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-110">**Basic knowledge of Data Lake Analytics and the Data Lake Tools for Visual Studio**.</span></span> <span data-ttu-id="d2ddb-111">Чтобы начать работу, см. следующие статьи.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-111">To get started, see:</span></span>

  * <span data-ttu-id="d2ddb-112">[Разработка сценария U-SQL с помощью средств озера данных для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d2ddb-112">[Develop U-SQL script using Data Lake tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="d2ddb-113">**Учетная запись Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-113">**A Data Lake Analytics account.**</span></span>  <span data-ttu-id="d2ddb-114">Ознакомьтесь с разделом [Создание учетной записи Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d2ddb-114">See [Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="d2ddb-115">**Передача примера данных в учетную запись Data Lake Analytics.**</span><span class="sxs-lookup"><span data-stu-id="d2ddb-115">**Upload the sample data to the Data Lake Analytics account.**</span></span> <span data-ttu-id="d2ddb-116">Ознакомьтесь с разделом о [копировании файлов с примерами данных](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d2ddb-116">See [To copy sample data files](data-lake-analytics-get-started-portal.md).</span></span>

    <span data-ttu-id="d2ddb-117">Чтобы выполнить задание аналитики озера данных, потребуются некоторые данные.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-117">To run a Data Lake Analytics job, you will need some data.</span></span> <span data-ttu-id="d2ddb-118">Несмотря на то, что средства озера данных поддерживают передачу данных, чтобы упростить работу с этим руководством, для передачи примера данных мы используем портал.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-118">Even though the Data Lake Tools supports uploading data, you will use the portal to upload the sample data to make this tutorial easier to follow.</span></span>

## <a name="connect-to-azure"></a><span data-ttu-id="d2ddb-119">Подключение к Azure</span><span class="sxs-lookup"><span data-stu-id="d2ddb-119">Connect to Azure</span></span>
<span data-ttu-id="d2ddb-120">Прежде чем можно будет скомпилировать и протестировать любой сценарий U-SQL, необходимо сначала подключиться к Azure.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-120">Before you can build and test any U-SQL scripts, you must first connect to Azure.</span></span>

<span data-ttu-id="d2ddb-121">**Подключение к аналитике озера данных**</span><span class="sxs-lookup"><span data-stu-id="d2ddb-121">**To connect to Data Lake Analytics**</span></span>

1. <span data-ttu-id="d2ddb-122">Откройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-122">Open Visual Studio.</span></span>
2. <span data-ttu-id="d2ddb-123">Щелкните **Data Lake > Параметры и настройки**.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-123">Click **Data Lake > Options and Settings**.</span></span>
3. <span data-ttu-id="d2ddb-124">Щелкните **Вход** или **Изменить пользователя**, если кто-то уже выполнил вход, и выполните инструкции для входа.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-124">Click **Sign In**, or **Change User** if someone has signed in, and follow the instructions.</span></span>
4. <span data-ttu-id="d2ddb-125">Нажмите кнопку **ОК** , чтобы закрыть диалоговое окно параметров и настроек.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-125">Click **OK** to close the Options and Settings dialog.</span></span>

<span data-ttu-id="d2ddb-126">**Просмотр учетных записей аналитики озера данных**</span><span class="sxs-lookup"><span data-stu-id="d2ddb-126">**To browse your Data Lake Analytics accounts**</span></span>

1. <span data-ttu-id="d2ddb-127">В Visual Studio откройте **обозреватель серверов**, нажав клавиши **CTRL + ALT + S**.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-127">From Visual Studio, open **Server Explorer** by press **CTRL+ALT+S**.</span></span>
2. <span data-ttu-id="d2ddb-128">В **обозревателе серверов** разверните **Azure**, а затем — **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-128">From **Server Explorer**, expand **Azure**, and then expand **Data Lake Analytics**.</span></span> <span data-ttu-id="d2ddb-129">Будет выведен список учетных записей аналитики озера данных, если они есть.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-129">You shall see a list of your Data Lake Analytics accounts if there are any.</span></span> <span data-ttu-id="d2ddb-130">Создать учетную запись аналитики озера данных в Studio невозможно.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-130">You cannot create Data Lake Analytics accounts from the studio.</span></span> <span data-ttu-id="d2ddb-131">Описание создания учетной записи см. в [руководстве по началу работы с Azure Data Lake Analytics с помощью портала Azure](data-lake-analytics-get-started-portal.md) или [руководстве по началу работы с Azure Data Lake Analytics с помощью Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d2ddb-131">To create an account, see [Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md) or [Get Started with Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span></span>

## <a name="develop-u-sql-application"></a><span data-ttu-id="d2ddb-132">Разработка приложения U-SQL</span><span class="sxs-lookup"><span data-stu-id="d2ddb-132">Develop U-SQL application</span></span>
<span data-ttu-id="d2ddb-133">Приложение U-SQL представляет собой главным образом сценарий U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-133">A U-SQL application is mostly a U-SQL script.</span></span> <span data-ttu-id="d2ddb-134">Дополнительные сведения о языке U-SQL см. в статье [Приступая к работе с U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d2ddb-134">To learn more about U-SQL, see [Get started with U-SQL](data-lake-analytics-u-sql-get-started.md).</span></span>

<span data-ttu-id="d2ddb-135">Вы можете добавить в приложение пользовательские операторы сложения.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-135">You can add addition user-defined operators to the application.</span></span>  <span data-ttu-id="d2ddb-136">Дополнительные сведения см. в статье [Разработка пользовательских операторов U-SQL для заданий аналитики озера данных](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span><span class="sxs-lookup"><span data-stu-id="d2ddb-136">For more information, see [Develop U-SQL user defined operators for Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span></span>

<span data-ttu-id="d2ddb-137">**Создание и отправка задания аналитики озера данных**</span><span class="sxs-lookup"><span data-stu-id="d2ddb-137">**To create and submit a Data Lake Analytics job**</span></span>

1. <span data-ttu-id="d2ddb-138">Щелкните **Файл > Создать > Проект**.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-138">Click the **File > New > Project**.</span></span>
2. <span data-ttu-id="d2ddb-139">Выберите тип «Проект U-SQL».</span><span class="sxs-lookup"><span data-stu-id="d2ddb-139">Select the U-SQL Project type.</span></span>

    ![Новый проект U-SQL в Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. <span data-ttu-id="d2ddb-141">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-141">Click **OK**.</span></span> <span data-ttu-id="d2ddb-142">Visual Studio создает решение с помощью файла Script.usql.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-142">Visual studio creates a solution with a Script.usql file.</span></span>
4. <span data-ttu-id="d2ddb-143">Скопируйте следующий сценарий в файл Script.usql.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-143">Enter the following script into the Script.usql file:</span></span>

        // Create a database for easy reuse, so you don't need to read from a file every time.
        CREATE DATABASE IF NOT EXISTS SampleDBTutorials;

        // Create a Table valued function. TVF ensures that your jobs fetch data from the weblog file with the correct schema.
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

    <span data-ttu-id="d2ddb-144">Для знакомства с U-SQL см. статью [Начало работы с языком U-SQL для аналитики озера данных Azure](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d2ddb-144">To understand the U-SQL, see [Get started with Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>    
5. <span data-ttu-id="d2ddb-145">Добавьте в проект новый скрипт U-SQL и введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d2ddb-145">Add a new U-SQL script to your project and enter the following:</span></span>

        // Query the referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        TO @"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. <span data-ttu-id="d2ddb-146">Вернитесь к первому скрипту U-SQL и рядом с кнопкой **Отправить** укажите свою учетную запись аналитики.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-146">Switch back to the first U-SQL script and next to the **Submit** button, specify your Analytics account.</span></span>
7. <span data-ttu-id="d2ddb-147">В **обозревателе решений** щелкните правой кнопкой мыши файл **Script.usql** и выберите команду **Build Script** (Создать сценарий).</span><span class="sxs-lookup"><span data-stu-id="d2ddb-147">From **Solution Explorer**, right click **Script.usql**, and then click **Build Script**.</span></span> <span data-ttu-id="d2ddb-148">Проверьте результаты на панели вывода.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-148">Verify the results in the Output pane.</span></span>
8. <span data-ttu-id="d2ddb-149">В **обозревателе решений** щелкните правой кнопкой мыши файл **Script.usql** и выберите команду **Submit Script** (Отправить сценарий).</span><span class="sxs-lookup"><span data-stu-id="d2ddb-149">From **Solution Explorer**, right click **Script.usql**, and then click **Submit Script**.</span></span>
9. <span data-ttu-id="d2ddb-150">Убедитесь, что для запуска задания выбрана правильная **учетная запись аналитики**, и нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-150">Verify the **Analytics Account** is the one where you want to run the job, and then click **Submit**.</span></span> <span data-ttu-id="d2ddb-151">Результаты отправки и ссылка на задание появятся в окне результатов средств озера данных для Visual Studio после завершения отправки.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-151">Submission results and job link are available in the Data Lake Tools for Visual Studio Results window when the submission is completed.</span></span>
10. <span data-ttu-id="d2ddb-152">Дождитесь успешного завершения задания.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-152">Wait until the job is completed successfully.</span></span>  <span data-ttu-id="d2ddb-153">Если задание не выполнено, скорее всего, отсутствует исходный файл.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-153">If the job failed, it is most likely missing the source file.</span></span>  <span data-ttu-id="d2ddb-154">См. раздел «Предварительные требования» этого руководства.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-154">Please see the Prerequisite section of this tutorial.</span></span> <span data-ttu-id="d2ddb-155">Дополнительные сведения об устранении неполадок см. в статье [Мониторинг и устранение неполадок заданий аналитики озера данных Azure](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="d2ddb-155">For additional troubleshooting information, see [Monitor and troubleshoot Azure Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>

    <span data-ttu-id="d2ddb-156">После выполнения задания вы должны увидеть такие результаты:</span><span class="sxs-lookup"><span data-stu-id="d2ddb-156">When the job is completed, you shall see the following screen:</span></span>

    ![аналитика озера данных анализ веб-журналов журналы веб-сайтов](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. <span data-ttu-id="d2ddb-158">Теперь повторите шаги 7–10 для файла **Script1.usql**.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-158">Now repeat steps 7- 10 for **Script1.usql**.</span></span>

<span data-ttu-id="d2ddb-159">**Просмотр выходных данных задания**</span><span class="sxs-lookup"><span data-stu-id="d2ddb-159">**To see the job output**</span></span>

1. <span data-ttu-id="d2ddb-160">В **обозревателе сервера** разверните узлы **Azure** и **Data Lake Analytics**, разверните учетную запись Data Lake Analytics и **учетные записи хранения**, а затем щелкните правой кнопкой мыши учетную запись хранения Data Lake по умолчанию и выберите **Обозреватель**.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-160">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click the default Data Lake Storage account, and then click **Explorer**.</span></span>
2. <span data-ttu-id="d2ddb-161">Дважды щелкните **Образцы**, чтобы открыть папку с примерами, и дважды щелкните **Выходные данные**.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-161">Double-click **Samples** to open the folder, and then double-click **Outputs**.</span></span>
3. <span data-ttu-id="d2ddb-162">Дважды щелкните файл **UnsuccessfulResponsees.log**.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-162">Double-click **UnsuccessfulResponsees.log**.</span></span>
4. <span data-ttu-id="d2ddb-163">Кроме того, вы можете дважды щелкнуть выходной файл в графическом представлении задания для перехода непосредственно к выходным данным.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-163">You can also double-click the output file inside the graph view of the job in order to navigate directly to the output.</span></span>

## <a name="see-also"></a><span data-ttu-id="d2ddb-164">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="d2ddb-164">See also</span></span>
<span data-ttu-id="d2ddb-165">Для начала работы с аналитикой озера данных с использованием различных средств см. следующие статьи.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-165">To get started with Data Lake Analytics using different tools, see:</span></span>

* [<span data-ttu-id="d2ddb-166">Начало работы с аналитикой озера данных с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="d2ddb-166">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="d2ddb-167">Начало работы с аналитикой озера данных с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2ddb-167">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="d2ddb-168">Начало работы с аналитикой озера данных с помощью пакета SDK .NET.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-168">Get started with Data Lake Analytics using .NET SDK</span></span>](data-lake-analytics-get-started-net-sdk.md)
