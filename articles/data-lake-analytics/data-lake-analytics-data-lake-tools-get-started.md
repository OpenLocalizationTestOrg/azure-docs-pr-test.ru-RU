---
title: "сценарии aaaDevelop U-SQL с помощью средств Озера данных для Visual Studio | Документы Microsoft"
description: "Узнайте, как Озера данных tooinstall Tools для Visual Studio и как toodevelop и тестирования сценарии U-SQL."
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
ms.openlocfilehash: 7a0c02c275b8cefecbe784ba63969cbf24a150d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a><span data-ttu-id="d5507-103">Разработка скриптов U-SQL с помощью средств Data Lake для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d5507-103">Develop U-SQL scripts by using Data Lake Tools for Visual Studio</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


<span data-ttu-id="d5507-104">Узнайте, как учетные записи аналитики Озера данных Azure toocreate Visual Studio toouse, определить заданий в [U-SQL](data-lake-analytics-u-sql-get-started.md)и служба аналитики Озера данных toohello задания отправки.</span><span class="sxs-lookup"><span data-stu-id="d5507-104">Learn how toouse Visual Studio toocreate Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs toohello Data Lake Analytics service.</span></span> <span data-ttu-id="d5507-105">Дополнительные сведения о Data Lake Analytics см. в [обзоре Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d5507-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d5507-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d5507-106">Prerequisites</span></span>

* <span data-ttu-id="d5507-107">**Visual Studio**: поддерживаются все выпуски, кроме Express.</span><span class="sxs-lookup"><span data-stu-id="d5507-107">**Visual Studio**: All editions except Express are supported.</span></span>
    * <span data-ttu-id="d5507-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="d5507-108">Visual Studio 2017</span></span>
    * <span data-ttu-id="d5507-109">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="d5507-109">Visual Studio 2015</span></span>
    * <span data-ttu-id="d5507-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d5507-110">Visual Studio 2013</span></span>
* <span data-ttu-id="d5507-111">**Microsoft Azure SDK для .NET** (версии 2.7.1 или выше).</span><span class="sxs-lookup"><span data-stu-id="d5507-111">**Microsoft Azure SDK for .NET** version 2.7.1 or later.</span></span>  <span data-ttu-id="d5507-112">Установите его с помощью hello [установщика веб-платформы](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5507-112">Install it by using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="d5507-113">Учетная запись **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="d5507-113">A **Data Lake Analytics** account.</span></span> <span data-ttu-id="d5507-114">в разделе toocreate учетную запись, [Приступая к работе с аналитики Озера данных Azure, с помощью портала Azure](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d5507-114">toocreate an account, see [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>

## <a name="install-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="d5507-115">Установка средств Azure Data Lake для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d5507-115">Install Azure Data Lake Tools for Visual Studio</span></span> 

<span data-ttu-id="d5507-116">Загрузите и установите средства Озера данных Azure для Visual Studio [из центра загрузки Майкрософт hello](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="d5507-116">Download and install Azure Data Lake Tools for Visual Studio [from hello Download Center](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="d5507-117">После установки обратите внимание на следующее:</span><span class="sxs-lookup"><span data-stu-id="d5507-117">After installation, note that:</span></span>
* <span data-ttu-id="d5507-118">Hello **обозревателя серверов** > **Azure** узел содержит **аналитики Озера данных** узла.</span><span class="sxs-lookup"><span data-stu-id="d5507-118">hello **Server Explorer** > **Azure** node contains a **Data Lake Analytics** node.</span></span> 
* <span data-ttu-id="d5507-119">Hello **средства** меню содержит **Озера данных** элемента.</span><span class="sxs-lookup"><span data-stu-id="d5507-119">hello **Tools** menu has a **Data Lake** item.</span></span>

## <a name="connect-tooan-azure-data-lake-analytics-account"></a><span data-ttu-id="d5507-120">Учетная запись аналитики Озера данных Azure tooan подключения</span><span class="sxs-lookup"><span data-stu-id="d5507-120">Connect tooan Azure Data Lake Analytics account</span></span>

1. <span data-ttu-id="d5507-121">Откройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d5507-121">Open Visual Studio.</span></span>
2. <span data-ttu-id="d5507-122">Откройте обозреватель сервера, последовательно выбрав пункты **Представление** > **Обозреватель сервера**.</span><span class="sxs-lookup"><span data-stu-id="d5507-122">Open Server Explorer by selecting **View** > **Server Explorer**.</span></span>
3. <span data-ttu-id="d5507-123">Щелкните правой кнопкой мыши **Azure**.</span><span class="sxs-lookup"><span data-stu-id="d5507-123">Right-click **Azure**.</span></span> <span data-ttu-id="d5507-124">Выберите **подключения tooMicrosoft подписки Azure** и следуйте инструкциям, hello.</span><span class="sxs-lookup"><span data-stu-id="d5507-124">Then select **Connect tooMicrosoft Azure Subscription** and follow hello instructions.</span></span>
4. <span data-ttu-id="d5507-125">В обозревателе сервера последовательно выберите пункты **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="d5507-125">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> <span data-ttu-id="d5507-126">Отобразится список учетных записей Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="d5507-126">You see a list of your Data Lake Analytics accounts.</span></span>


## <a name="write-your-first-u-sql-script"></a><span data-ttu-id="d5507-127">Создание первого скрипта U-SQL</span><span class="sxs-lookup"><span data-stu-id="d5507-127">Write your first U-SQL script</span></span>

<span data-ttu-id="d5507-128">После текста Hello является простой скрипт U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d5507-128">hello following text is a simple U-SQL script.</span></span> <span data-ttu-id="d5507-129">Он определяет небольшой набор данных и записи, которые вызваны хранилища Озера данных по умолчанию toohello набора данных в формате `/data.csv`.</span><span class="sxs-lookup"><span data-stu-id="d5507-129">It defines a small dataset and writes that dataset toohello default Data Lake Store as a file called `/data.csv`.</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

### <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="d5507-130">Отправка задания аналитики озера данных</span><span class="sxs-lookup"><span data-stu-id="d5507-130">Submit a Data Lake Analytics job</span></span>

1. <span data-ttu-id="d5507-131">Выберите **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="d5507-131">Select **File** > **New** > **Project**.</span></span>

2. <span data-ttu-id="d5507-132">Выберите hello **проекта U-SQL** введите и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d5507-132">Select hello **U-SQL Project** type, and then click **OK**.</span></span> <span data-ttu-id="d5507-133">Visual Studio создаст решение с помощью файла **Script.usql**.</span><span class="sxs-lookup"><span data-stu-id="d5507-133">Visual Studio creates a solution with a **Script.usql** file.</span></span>

3. <span data-ttu-id="d5507-134">Вставьте предыдущий сценарий hello в hello **Script.usql** окна.</span><span class="sxs-lookup"><span data-stu-id="d5507-134">Paste hello previous script into hello **Script.usql** window.</span></span>

4. <span data-ttu-id="d5507-135">В левом верхнем углу hello hello **Script.usql** окна, укажите учетную запись аналитики Озера данных hello.</span><span class="sxs-lookup"><span data-stu-id="d5507-135">In hello upper-left corner of hello **Script.usql** window, specify hello Data Lake Analytics account.</span></span>

    ![Отправка проекта U-SQL в Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. <span data-ttu-id="d5507-137">В левом верхнем углу hello hello **Script.usql** выберите **отправить**.</span><span class="sxs-lookup"><span data-stu-id="d5507-137">In hello upper-left corner of hello **Script.usql** window, select **Submit**.</span></span>
6. <span data-ttu-id="d5507-138">Проверьте hello **учетной записи аналитики**и выберите **отправить**.</span><span class="sxs-lookup"><span data-stu-id="d5507-138">Verify hello **Analytics Account**, and then select **Submit**.</span></span> <span data-ttu-id="d5507-139">Результаты отправки доступны в hello средств Озера данных для Visual Studio результаты после завершения отправки hello.</span><span class="sxs-lookup"><span data-stu-id="d5507-139">Submission results are available in hello Data Lake Tools for Visual Studio Results after hello submission is complete.</span></span>

    ![Отправка проекта U-SQL в Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. <span data-ttu-id="d5507-141">toosee hello последние задания состояния и обновить hello экрана, нажмите кнопку **обновление**.</span><span class="sxs-lookup"><span data-stu-id="d5507-141">toosee hello latest job status and refresh hello screen, click **Refresh**.</span></span> <span data-ttu-id="d5507-142">При успешном завершении задания hello, он показывает hello **схемы заданий**, **операций с метаданными**, **журнал состояний**, и **диагностики**:</span><span class="sxs-lookup"><span data-stu-id="d5507-142">When hello job succeeds, it shows hello **Job Graph**, **MetaData Operations**, **State History**, and **Diagnostics**:</span></span>

    ![График выполнения задания аналитики озера данных U-SQL в Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * <span data-ttu-id="d5507-144">**Сводка заданий** показано hello Сводка hello задания.</span><span class="sxs-lookup"><span data-stu-id="d5507-144">**Job Summary** shows hello summary of hello job.</span></span>   
   * <span data-ttu-id="d5507-145">**Сведения о задании** показывает более конкретные сведения о задании hello, включая сценарий hello, ресурсы и вершин.</span><span class="sxs-lookup"><span data-stu-id="d5507-145">**Job Details** shows more specific information about hello job, including hello script, resources, and vertices.</span></span>
   * <span data-ttu-id="d5507-146">**График задания** визуализирует hello ход выполнения задания hello.</span><span class="sxs-lookup"><span data-stu-id="d5507-146">**Job Graph** visualizes hello progress of hello job.</span></span>
   * <span data-ttu-id="d5507-147">**Операций с метаданными** показывает все hello действия, которые были выполнены на каталог hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d5507-147">**MetaData Operations** shows all hello actions that were taken on hello U-SQL catalog.</span></span>
   * <span data-ttu-id="d5507-148">**Данные** показывает все hello входов и выходов.</span><span class="sxs-lookup"><span data-stu-id="d5507-148">**Data** shows all hello inputs and outputs.</span></span>
   * <span data-ttu-id="d5507-149">В окне **Диагностика** представлены данные расширенного анализа для выполнения задания и оптимизации производительности.</span><span class="sxs-lookup"><span data-stu-id="d5507-149">**Diagnostics** provides an advanced analysis for job execution and performance optimization.</span></span>

### <a name="toocheck-job-state"></a><span data-ttu-id="d5507-150">состояние задания toocheck</span><span class="sxs-lookup"><span data-stu-id="d5507-150">toocheck job state</span></span>

1. <span data-ttu-id="d5507-151">В обозревателе сервера последовательно выберите пункты **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="d5507-151">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> 
2. <span data-ttu-id="d5507-152">Разверните имя учетной записи аналитики Озера данных hello.</span><span class="sxs-lookup"><span data-stu-id="d5507-152">Expand hello Data Lake Analytics account name.</span></span>
3. <span data-ttu-id="d5507-153">Дважды щелкните **Задания**.</span><span class="sxs-lookup"><span data-stu-id="d5507-153">Double-click **Jobs**.</span></span>
4. <span data-ttu-id="d5507-154">Выберите ранее отправленного задания hello.</span><span class="sxs-lookup"><span data-stu-id="d5507-154">Select hello job that you previously submitted.</span></span>

### <a name="toosee-hello-output-of-a-job"></a><span data-ttu-id="d5507-155">toosee hello выходных данных задания</span><span class="sxs-lookup"><span data-stu-id="d5507-155">toosee hello output of a job</span></span>

1. <span data-ttu-id="d5507-156">В обозревателе серверов Обзор toohello задание, которое вы отправили.</span><span class="sxs-lookup"><span data-stu-id="d5507-156">In Server Explorer, browse toohello job you submitted.</span></span>
2. <span data-ttu-id="d5507-157">Нажмите кнопку hello **данные** вкладки.</span><span class="sxs-lookup"><span data-stu-id="d5507-157">Click hello **Data** tab.</span></span>
3. <span data-ttu-id="d5507-158">В hello **выходных данных задания** вкладке, выберите hello `"/data.csv"` файла.</span><span class="sxs-lookup"><span data-stu-id="d5507-158">In hello **Job Outputs** tab, select hello `"/data.csv"` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5507-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d5507-159">Next steps</span></span>

* [<span data-ttu-id="d5507-160">Тестирование и отладка заданий U-SQL с помощью локального выполнения и пакета SDK U-SQL для Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="d5507-160">Run U-SQL scripts on your own workstation for testing and debugging</span></span>](data-lake-analytics-data-lake-tools-local-run.md)
* [<span data-ttu-id="d5507-161">Отладка заданий U-SQL</span><span class="sxs-lookup"><span data-stu-id="d5507-161">Debug C# code in U-SQL jobs</span></span>](data-lake-analytics-debug-u-sql-jobs.md)
* [<span data-ttu-id="d5507-162">Используйте средства Озера данных Azure hello для кода Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d5507-162">Use hello Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
