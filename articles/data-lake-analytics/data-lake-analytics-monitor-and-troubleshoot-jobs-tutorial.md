---
title: "Устранение неполадок с заданиями Azure Data Lake Analytics с помощью портала Azure | Документация Майкрософт"
description: "Узнайте, как использовать портал Azure для устранения неполадок с заданиями аналитики озера данных. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: b7066d81-3142-474f-8a34-32b0b39656dc
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: b9c7453cc0a94f70d0098ed83e5f127832065a62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a><span data-ttu-id="edfed-103">Устранение неполадок с заданиями аналитики озера данных Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="edfed-103">Troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>
<span data-ttu-id="edfed-104">Узнайте, как использовать портал Azure для устранения неполадок с заданиями аналитики озера данных.</span><span class="sxs-lookup"><span data-stu-id="edfed-104">Learn how to use the Azure Portal to troubleshoot Data Lake Analytics jobs.</span></span>

<span data-ttu-id="edfed-105">При прохождении этого учебника вы смоделируете проблему с отсутствующим исходным файлом и устраните ее с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="edfed-105">In this tutorial, you will setup a missing source file problem, and use the Azure Portal to troubleshoot the problem.</span></span>

## <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="edfed-106">Отправка задания аналитики озера данных</span><span class="sxs-lookup"><span data-stu-id="edfed-106">Submit a Data Lake Analytics job</span></span>

<span data-ttu-id="edfed-107">Отправьте следующее задание U-SQL:</span><span class="sxs-lookup"><span data-stu-id="edfed-107">Submit the following U-SQL job:</span></span>

```
@searchlog =
   EXTRACT UserId          int,
           Start           DateTime,
           Region          string,
           Query           string,
           Duration        int?,
           Urls            string,
           ClickedUrls     string
   FROM "/Samples/Data/SearchLog.tsv1"
   USING Extractors.Tsv();

OUTPUT @searchlog   
   TO "/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
<span data-ttu-id="edfed-108">В сценарии определен исходный файл **/Samples/Data/SearchLog.tsv1**, а должен быть **/Samples/Data/SearchLog.tsv**.</span><span class="sxs-lookup"><span data-stu-id="edfed-108">The source file defined in the script is **/Samples/Data/SearchLog.tsv1**, where it should be **/Samples/Data/SearchLog.tsv**.</span></span>


## <a name="troubleshoot-the-job"></a><span data-ttu-id="edfed-109">Устранение неполадок задания</span><span class="sxs-lookup"><span data-stu-id="edfed-109">Troubleshoot the job</span></span>

<span data-ttu-id="edfed-110">**Просмотр всех заданий**</span><span class="sxs-lookup"><span data-stu-id="edfed-110">**To see all the jobs**</span></span>

1. <span data-ttu-id="edfed-111">На портале Azure щелкните **Microsoft Azure** в левом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="edfed-111">From the Azure portal, click **Microsoft Azure** in the upper left corner.</span></span>
2. <span data-ttu-id="edfed-112">Щелкните элемент с именем вашей учетной записи аналитики озера данных.</span><span class="sxs-lookup"><span data-stu-id="edfed-112">Click the tile with your Data Lake Analytics account name.</span></span>  <span data-ttu-id="edfed-113">Сводные данные задания отображаются на элементе **Управление заданиями** .</span><span class="sxs-lookup"><span data-stu-id="edfed-113">The job summary is shown on the **Job Management** tile.</span></span>

    ![Аналитика озера данных Azure: управление заданиями](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    <span data-ttu-id="edfed-115">Элемент управления заданиями позволяет взглянуть на состояние заданий.</span><span class="sxs-lookup"><span data-stu-id="edfed-115">The job Management gives you a glance of the job status.</span></span> <span data-ttu-id="edfed-116">Обратите внимание, что здесь имеется задание, завершившееся сбоем.</span><span class="sxs-lookup"><span data-stu-id="edfed-116">Notice there is a failed job.</span></span>
3. <span data-ttu-id="edfed-117">Щелкните элемент **Управление заданиями** для просмотра заданий.</span><span class="sxs-lookup"><span data-stu-id="edfed-117">Click the **Job Management** tile to see the jobs.</span></span> <span data-ttu-id="edfed-118">Задания делятся на три категории: **Выполняется**, **В очереди** и **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="edfed-118">The jobs are categorized in **Running**, **Queued**, and **Ended**.</span></span> <span data-ttu-id="edfed-119">Задание, завершившееся сбоем, будет отображено в разделе **Завершено** .</span><span class="sxs-lookup"><span data-stu-id="edfed-119">You shall see your failed job in the **Ended** section.</span></span> <span data-ttu-id="edfed-120">Оно должно быть первым в списке.</span><span class="sxs-lookup"><span data-stu-id="edfed-120">It shall be first one in the list.</span></span> <span data-ttu-id="edfed-121">При наличии большого числа заданий можно щелкнуть **Фильтр** , чтобы упростить их поиск.</span><span class="sxs-lookup"><span data-stu-id="edfed-121">When you have a lot of jobs, you can click **Filter** to help you to locate jobs.</span></span>

    ![Аналитика озера данных Azure: фильтрация заданий](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. <span data-ttu-id="edfed-123">Щелкните невыполненное задание из списка, чтобы открыть сведения о задании в новой колонке:</span><span class="sxs-lookup"><span data-stu-id="edfed-123">Click the failed job from the list to open the job details in a new blade:</span></span>

    ![Аналитика озера данных Azure: невыполненное задание](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    <span data-ttu-id="edfed-125">Обратите внимание на кнопку **Отправить повторно** .</span><span class="sxs-lookup"><span data-stu-id="edfed-125">Notice the **Resubmit** button.</span></span> <span data-ttu-id="edfed-126">После устранения проблемы можно отправить задание повторно.</span><span class="sxs-lookup"><span data-stu-id="edfed-126">After you fix the problem, you can resubmit the job.</span></span>
5. <span data-ttu-id="edfed-127">Щелкните выделенную часть на предыдущем снимке экрана, чтобы открыть сведения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="edfed-127">Click highlighted part from the previous screenshot to open the error details.</span></span>  <span data-ttu-id="edfed-128">Отобразится примерно следующий текст:</span><span class="sxs-lookup"><span data-stu-id="edfed-128">You shall see something like:</span></span>

    ![Аналитика озера данных Azure: сведения о невыполненном задании](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    <span data-ttu-id="edfed-130">В нем сообщается, что исходная папка не найдена.</span><span class="sxs-lookup"><span data-stu-id="edfed-130">It tells you the source folder is not found.</span></span>
6. <span data-ttu-id="edfed-131">Щелкните **Дублировать скрипт**.</span><span class="sxs-lookup"><span data-stu-id="edfed-131">Click **Duplicate Script**.</span></span>
7. <span data-ttu-id="edfed-132">Измените путь **FROM** на:</span><span class="sxs-lookup"><span data-stu-id="edfed-132">Update the **FROM** path to the following:</span></span>

    <span data-ttu-id="edfed-133">/Samples/Data/SearchLog.tsv</span><span class="sxs-lookup"><span data-stu-id="edfed-133">"/Samples/Data/SearchLog.tsv"</span></span>
8. <span data-ttu-id="edfed-134">Щелкните **Отправить задание**.</span><span class="sxs-lookup"><span data-stu-id="edfed-134">Click **Submit Job**.</span></span>

## <a name="see-also"></a><span data-ttu-id="edfed-135">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="edfed-135">See also</span></span>
* [<span data-ttu-id="edfed-136">Обзор аналитики озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="edfed-136">Azure Data Lake Analytics overview</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="edfed-137">Начало работы с аналитикой озера данных Azure с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="edfed-137">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="edfed-138">Начало работы с аналитикой озера данных Azure и U-SQL с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="edfed-138">Get started with Azure Data Lake Analytics and U-SQL using Visual Studio</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="edfed-139">Управление аналитикой озера данных Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="edfed-139">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
