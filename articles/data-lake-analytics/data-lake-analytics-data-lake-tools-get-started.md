---
title: "Разработка скриптов U-SQL с помощью средств Data Lake для Visual Studio | Документация Майкрософт"
description: "Сведения об установке средств Data Lake для Visual Studio, разработке и тестировании скриптов U-SQL."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: ad8a6992-02c7-47d4-a108-62fc5a0777a3
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/28/2017
ms.author: saveenr, yanacai
ms.openlocfilehash: 7bbbb08ff635477a88403a3ae6bd3486d31838ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a><span data-ttu-id="af6e6-103">Разработка скриптов U-SQL с помощью средств Data Lake для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="af6e6-103">Develop U-SQL scripts by using Data Lake Tools for Visual Studio</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


<span data-ttu-id="af6e6-104">Узнайте, как с помощью Visual Studio создавать учетные записи Azure Data Lake Analytics, определять задания в [U-SQL](data-lake-analytics-u-sql-get-started.md) и отправлять их в службу Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="af6e6-104">Learn how to use Visual Studio to create Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to the Data Lake Analytics service.</span></span> <span data-ttu-id="af6e6-105">Дополнительные сведения о Data Lake Analytics см. в [обзоре Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="af6e6-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="af6e6-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="af6e6-106">Prerequisites</span></span>

* <span data-ttu-id="af6e6-107">**Visual Studio**: поддерживаются все выпуски, кроме Express.</span><span class="sxs-lookup"><span data-stu-id="af6e6-107">**Visual Studio**: All editions except Express are supported.</span></span>
    * <span data-ttu-id="af6e6-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="af6e6-108">Visual Studio 2017</span></span>
    * <span data-ttu-id="af6e6-109">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="af6e6-109">Visual Studio 2015</span></span>
    * <span data-ttu-id="af6e6-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="af6e6-110">Visual Studio 2013</span></span>
* <span data-ttu-id="af6e6-111">**Microsoft Azure SDK для .NET** (версии 2.7.1 или выше).</span><span class="sxs-lookup"><span data-stu-id="af6e6-111">**Microsoft Azure SDK for .NET** version 2.7.1 or later.</span></span>  <span data-ttu-id="af6e6-112">Можно установить его с помощью [установщика веб-платформы](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="af6e6-112">Install it by using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="af6e6-113">Учетная запись **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="af6e6-113">A **Data Lake Analytics** account.</span></span> <span data-ttu-id="af6e6-114">Чтобы создать учетную запись, ознакомьтесь со статьей [Руководство. Начало работы с Azure Data Lake Analytics с помощью портала Azure](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="af6e6-114">To create an account, see [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>

## <a name="install-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="af6e6-115">Установка средств Azure Data Lake для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="af6e6-115">Install Azure Data Lake Tools for Visual Studio</span></span> 

<span data-ttu-id="af6e6-116">Загрузите и установите средства Azure Data Lake для Visual Studio [из центра загрузки](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="af6e6-116">Download and install Azure Data Lake Tools for Visual Studio [from the Download Center](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="af6e6-117">После установки обратите внимание на следующее:</span><span class="sxs-lookup"><span data-stu-id="af6e6-117">After installation, note that:</span></span>
* <span data-ttu-id="af6e6-118">узел **Обозреватель сервера** > **Azure** содержит узел **Data Lake Analytics**;</span><span class="sxs-lookup"><span data-stu-id="af6e6-118">The **Server Explorer** > **Azure** node contains a **Data Lake Analytics** node.</span></span> 
* <span data-ttu-id="af6e6-119">в меню **Средства** появился пункт **Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="af6e6-119">The **Tools** menu has a **Data Lake** item.</span></span>

## <a name="connect-to-an-azure-data-lake-analytics-account"></a><span data-ttu-id="af6e6-120">Подключение к учетной записи Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="af6e6-120">Connect to an Azure Data Lake Analytics account</span></span>

1. <span data-ttu-id="af6e6-121">Откройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="af6e6-121">Open Visual Studio.</span></span>
2. <span data-ttu-id="af6e6-122">Откройте обозреватель сервера, последовательно выбрав пункты **Представление** > **Обозреватель сервера**.</span><span class="sxs-lookup"><span data-stu-id="af6e6-122">Open Server Explorer by selecting **View** > **Server Explorer**.</span></span>
3. <span data-ttu-id="af6e6-123">Щелкните правой кнопкой мыши **Azure**.</span><span class="sxs-lookup"><span data-stu-id="af6e6-123">Right-click **Azure**.</span></span> <span data-ttu-id="af6e6-124">Затем выберите **Подключиться к подписке Microsoft Azure** и следуйте инструкциям.</span><span class="sxs-lookup"><span data-stu-id="af6e6-124">Then select **Connect to Microsoft Azure Subscription** and follow the instructions.</span></span>
4. <span data-ttu-id="af6e6-125">В обозревателе сервера последовательно выберите пункты **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="af6e6-125">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> <span data-ttu-id="af6e6-126">Отобразится список учетных записей Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="af6e6-126">You see a list of your Data Lake Analytics accounts.</span></span>


## <a name="write-your-first-u-sql-script"></a><span data-ttu-id="af6e6-127">Создание первого скрипта U-SQL</span><span class="sxs-lookup"><span data-stu-id="af6e6-127">Write your first U-SQL script</span></span>

<span data-ttu-id="af6e6-128">Ниже приводится простой скрипт U-SQL.</span><span class="sxs-lookup"><span data-stu-id="af6e6-128">The following text is a simple U-SQL script.</span></span> <span data-ttu-id="af6e6-129">Он определяет небольшой набор данных и по умолчанию записывает его в хранилище Data Lake Store как файл с именем `/data.csv`.</span><span class="sxs-lookup"><span data-stu-id="af6e6-129">It defines a small dataset and writes that dataset to the default Data Lake Store as a file called `/data.csv`.</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
```

### <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="af6e6-130">Отправка задания аналитики озера данных</span><span class="sxs-lookup"><span data-stu-id="af6e6-130">Submit a Data Lake Analytics job</span></span>

1. <span data-ttu-id="af6e6-131">Выберите **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="af6e6-131">Select **File** > **New** > **Project**.</span></span>

2. <span data-ttu-id="af6e6-132">Выберите тип **Проект U-SQL** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="af6e6-132">Select the **U-SQL Project** type, and then click **OK**.</span></span> <span data-ttu-id="af6e6-133">Visual Studio создаст решение с помощью файла **Script.usql**.</span><span class="sxs-lookup"><span data-stu-id="af6e6-133">Visual Studio creates a solution with a **Script.usql** file.</span></span>

3. <span data-ttu-id="af6e6-134">Вставьте предыдущий скрипт в окно **Script.usql**.</span><span class="sxs-lookup"><span data-stu-id="af6e6-134">Paste the previous script into the **Script.usql** window.</span></span>

4. <span data-ttu-id="af6e6-135">В левом верхнем углу окна **Script.usql** укажите учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="af6e6-135">In the upper-left corner of the **Script.usql** window, specify the Data Lake Analytics account.</span></span>

    ![Отправка проекта U-SQL в Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. <span data-ttu-id="af6e6-137">В левом верхнем углу окна **Script.usql** выберите **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="af6e6-137">In the upper-left corner of the **Script.usql** window, select **Submit**.</span></span>
6. <span data-ttu-id="af6e6-138">Проверьте **учетную запись Analytics** и выберите **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="af6e6-138">Verify the **Analytics Account**, and then select **Submit**.</span></span> <span data-ttu-id="af6e6-139">По завершении отправки ее результаты появятся в окне результатов средств Data Lake для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="af6e6-139">Submission results are available in the Data Lake Tools for Visual Studio Results after the submission is complete.</span></span>

    ![Отправка проекта U-SQL в Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. <span data-ttu-id="af6e6-141">Чтобы отобразились сведения о последнем состоянии задания, нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="af6e6-141">To see the latest job status and refresh the screen, click **Refresh**.</span></span> <span data-ttu-id="af6e6-142">Если задание завершилось успешно, отобразятся параметры **Граф задания**, **Операции с метаданными**, **Журнал состояний** и **Диагностика**:</span><span class="sxs-lookup"><span data-stu-id="af6e6-142">When the job succeeds, it shows the **Job Graph**, **MetaData Operations**, **State History**, and **Diagnostics**:</span></span>

    ![График выполнения задания аналитики озера данных U-SQL в Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * <span data-ttu-id="af6e6-144">В окне **Сводные данные задания** представлена сводка задания.</span><span class="sxs-lookup"><span data-stu-id="af6e6-144">**Job Summary** shows the summary of the job.</span></span>   
   * <span data-ttu-id="af6e6-145">В окне **Сведения о задании** содержатся более конкретные сведения о задании, в частности о скрипте, ресурсах и вершинах.</span><span class="sxs-lookup"><span data-stu-id="af6e6-145">**Job Details** shows more specific information about the job, including the script, resources, and vertices.</span></span>
   * <span data-ttu-id="af6e6-146">В окне **Граф задания** визуализируется ход выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="af6e6-146">**Job Graph** visualizes the progress of the job.</span></span>
   * <span data-ttu-id="af6e6-147">В окне **Операции с метаданными** представлены сведения обо всех действиях, выполненных в каталоге U-SQL.</span><span class="sxs-lookup"><span data-stu-id="af6e6-147">**MetaData Operations** shows all the actions that were taken on the U-SQL catalog.</span></span>
   * <span data-ttu-id="af6e6-148">В окне **Данные** отображаются все входные и выходные данные.</span><span class="sxs-lookup"><span data-stu-id="af6e6-148">**Data** shows all the inputs and outputs.</span></span>
   * <span data-ttu-id="af6e6-149">В окне **Диагностика** представлены данные расширенного анализа для выполнения задания и оптимизации производительности.</span><span class="sxs-lookup"><span data-stu-id="af6e6-149">**Diagnostics** provides an advanced analysis for job execution and performance optimization.</span></span>

### <a name="to-check-job-state"></a><span data-ttu-id="af6e6-150">Проверка состояния задания</span><span class="sxs-lookup"><span data-stu-id="af6e6-150">To check job state</span></span>

1. <span data-ttu-id="af6e6-151">В обозревателе сервера последовательно выберите пункты **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="af6e6-151">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> 
2. <span data-ttu-id="af6e6-152">Разверните окно имени учетной записи Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="af6e6-152">Expand the Data Lake Analytics account name.</span></span>
3. <span data-ttu-id="af6e6-153">Дважды щелкните **Задания**.</span><span class="sxs-lookup"><span data-stu-id="af6e6-153">Double-click **Jobs**.</span></span>
4. <span data-ttu-id="af6e6-154">Выберите задание, отправленное ранее.</span><span class="sxs-lookup"><span data-stu-id="af6e6-154">Select the job that you previously submitted.</span></span>

### <a name="to-see-the-output-of-a-job"></a><span data-ttu-id="af6e6-155">Просмотр выходных данных задания</span><span class="sxs-lookup"><span data-stu-id="af6e6-155">To see the output of a job</span></span>

1. <span data-ttu-id="af6e6-156">В обозревателе сервера перейдите к отправленному заданию.</span><span class="sxs-lookup"><span data-stu-id="af6e6-156">In Server Explorer, browse to the job you submitted.</span></span>
2. <span data-ttu-id="af6e6-157">Перейдите на вкладку **Данные** .</span><span class="sxs-lookup"><span data-stu-id="af6e6-157">Click the **Data** tab.</span></span>
3. <span data-ttu-id="af6e6-158">На вкладке **Job Outputs** (Выходные данные задания) выберите файл `"/data.csv"`.</span><span class="sxs-lookup"><span data-stu-id="af6e6-158">In the **Job Outputs** tab, select the `"/data.csv"` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af6e6-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="af6e6-159">Next steps</span></span>

* [<span data-ttu-id="af6e6-160">Тестирование и отладка заданий U-SQL с помощью локального выполнения и пакета SDK U-SQL для Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="af6e6-160">Run U-SQL scripts on your own workstation for testing and debugging</span></span>](data-lake-analytics-data-lake-tools-local-run.md)
* [<span data-ttu-id="af6e6-161">Отладка заданий U-SQL</span><span class="sxs-lookup"><span data-stu-id="af6e6-161">Debug C# code in U-SQL jobs</span></span>](data-lake-analytics-debug-u-sql-jobs.md)
* [<span data-ttu-id="af6e6-162">Использование средств Azure Data Lake для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="af6e6-162">Use the Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
