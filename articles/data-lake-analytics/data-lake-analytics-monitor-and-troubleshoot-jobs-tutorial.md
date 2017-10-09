---
title: "задания aaaTroubleshoot аналитики Озера данных Azure, с помощью портала Azure | Документы Microsoft"
description: "Узнайте, как toouse hello задания аналитики Озера данных tootroubleshoot портала Azure. "
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
ms.openlocfilehash: e810d56bab8f1a8254721ec9906bb6a4508dc22a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a><span data-ttu-id="5cfd2-103">Устранение неполадок с заданиями аналитики озера данных Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="5cfd2-103">Troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>
<span data-ttu-id="5cfd2-104">Узнайте, как toouse hello задания аналитики Озера данных tootroubleshoot портала Azure.</span><span class="sxs-lookup"><span data-stu-id="5cfd2-104">Learn how toouse hello Azure Portal tootroubleshoot Data Lake Analytics jobs.</span></span>

<span data-ttu-id="5cfd2-105">В этом учебнике будет настроить проблемы отсутствующего файла источника и использовать hello портала Azure tootroubleshoot hello проблему.</span><span class="sxs-lookup"><span data-stu-id="5cfd2-105">In this tutorial, you will setup a missing source file problem, and use hello Azure Portal tootroubleshoot hello problem.</span></span>

## <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="5cfd2-106">Отправка задания аналитики озера данных</span><span class="sxs-lookup"><span data-stu-id="5cfd2-106">Submit a Data Lake Analytics job</span></span>

<span data-ttu-id="5cfd2-107">Отправьте hello после задания U-SQL:</span><span class="sxs-lookup"><span data-stu-id="5cfd2-107">Submit hello following U-SQL job:</span></span>

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
   too"/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
<span data-ttu-id="5cfd2-108">Hello является исходным файлом, определенных в скрипте hello **/Samples/Data/SearchLog.tsv1**, где она должна быть **/Samples/Data/SearchLog.tsv**.</span><span class="sxs-lookup"><span data-stu-id="5cfd2-108">hello source file defined in hello script is **/Samples/Data/SearchLog.tsv1**, where it should be **/Samples/Data/SearchLog.tsv**.</span></span>


## <a name="troubleshoot-hello-job"></a><span data-ttu-id="5cfd2-109">Диагностика заданий hello</span><span class="sxs-lookup"><span data-stu-id="5cfd2-109">Troubleshoot hello job</span></span>

<span data-ttu-id="5cfd2-110">**toosee все hello заданий**</span><span class="sxs-lookup"><span data-stu-id="5cfd2-110">**toosee all hello jobs**</span></span>

1. <span data-ttu-id="5cfd2-111">Hello портал Azure, щелкните **Microsoft Azure** в верхнем левом углу hello.</span><span class="sxs-lookup"><span data-stu-id="5cfd2-111">From hello Azure portal, click **Microsoft Azure** in hello upper left corner.</span></span>
2. <span data-ttu-id="5cfd2-112">Щелкните плитку hello имя вашей учетной записи аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="5cfd2-112">Click hello tile with your Data Lake Analytics account name.</span></span>  <span data-ttu-id="5cfd2-113">Сводка по заданию Hello отображается на hello **управление заданиями** плитки.</span><span class="sxs-lookup"><span data-stu-id="5cfd2-113">hello job summary is shown on hello **Job Management** tile.</span></span>

    ![Аналитика озера данных Azure: управление заданиями](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    <span data-ttu-id="5cfd2-115">Задание Hello управления позволяет быстро hello состояние задания.</span><span class="sxs-lookup"><span data-stu-id="5cfd2-115">hello job Management gives you a glance of hello job status.</span></span> <span data-ttu-id="5cfd2-116">Обратите внимание, что здесь имеется задание, завершившееся сбоем.</span><span class="sxs-lookup"><span data-stu-id="5cfd2-116">Notice there is a failed job.</span></span>
3. <span data-ttu-id="5cfd2-117">Нажмите кнопку hello **управление заданиями** плитки toosee hello заданий.</span><span class="sxs-lookup"><span data-stu-id="5cfd2-117">Click hello **Job Management** tile toosee hello jobs.</span></span> <span data-ttu-id="5cfd2-118">задания Hello разделены на **под управлением**, **в очереди**, и **завершено**.</span><span class="sxs-lookup"><span data-stu-id="5cfd2-118">hello jobs are categorized in **Running**, **Queued**, and **Ended**.</span></span> <span data-ttu-id="5cfd2-119">Вы увидите сбоя задания в hello **завершено** раздела.</span><span class="sxs-lookup"><span data-stu-id="5cfd2-119">You shall see your failed job in hello **Ended** section.</span></span> <span data-ttu-id="5cfd2-120">Это должен быть первый в списке hello.</span><span class="sxs-lookup"><span data-stu-id="5cfd2-120">It shall be first one in hello list.</span></span> <span data-ttu-id="5cfd2-121">Если у вас много заданий, можно щелкнуть **фильтра** toohelp вы toolocate заданий.</span><span class="sxs-lookup"><span data-stu-id="5cfd2-121">When you have a lot of jobs, you can click **Filter** toohelp you toolocate jobs.</span></span>

    ![Аналитика озера данных Azure: фильтрация заданий](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. <span data-ttu-id="5cfd2-123">Щелкните hello невыполненного задания с hello tooopen список hello сведений о задании в Новая колонка:</span><span class="sxs-lookup"><span data-stu-id="5cfd2-123">Click hello failed job from hello list tooopen hello job details in a new blade:</span></span>

    ![Аналитика озера данных Azure: невыполненное задание](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    <span data-ttu-id="5cfd2-125">Обратите внимание hello **повторно отправить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="5cfd2-125">Notice hello **Resubmit** button.</span></span> <span data-ttu-id="5cfd2-126">После устранения проблемы hello, можно повторно отправить задания hello.</span><span class="sxs-lookup"><span data-stu-id="5cfd2-126">After you fix hello problem, you can resubmit hello job.</span></span>
5. <span data-ttu-id="5cfd2-127">Щелкните выделенную часть из hello предыдущего экрана tooopen hello сведения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="5cfd2-127">Click highlighted part from hello previous screenshot tooopen hello error details.</span></span>  <span data-ttu-id="5cfd2-128">Отобразится примерно следующий текст:</span><span class="sxs-lookup"><span data-stu-id="5cfd2-128">You shall see something like:</span></span>

    ![Аналитика озера данных Azure: сведения о невыполненном задании](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    <span data-ttu-id="5cfd2-130">Оно сообщает, что исходная папка hello не найден.</span><span class="sxs-lookup"><span data-stu-id="5cfd2-130">It tells you hello source folder is not found.</span></span>
6. <span data-ttu-id="5cfd2-131">Щелкните **Дублировать скрипт**.</span><span class="sxs-lookup"><span data-stu-id="5cfd2-131">Click **Duplicate Script**.</span></span>
7. <span data-ttu-id="5cfd2-132">Обновление hello **FROM** toohello следующие пути:</span><span class="sxs-lookup"><span data-stu-id="5cfd2-132">Update hello **FROM** path toohello following:</span></span>

    <span data-ttu-id="5cfd2-133">/Samples/Data/SearchLog.tsv</span><span class="sxs-lookup"><span data-stu-id="5cfd2-133">"/Samples/Data/SearchLog.tsv"</span></span>
8. <span data-ttu-id="5cfd2-134">Щелкните **Отправить задание**.</span><span class="sxs-lookup"><span data-stu-id="5cfd2-134">Click **Submit Job**.</span></span>

## <a name="see-also"></a><span data-ttu-id="5cfd2-135">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="5cfd2-135">See also</span></span>
* [<span data-ttu-id="5cfd2-136">Обзор аналитики озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="5cfd2-136">Azure Data Lake Analytics overview</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="5cfd2-137">Начало работы с аналитикой озера данных Azure с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5cfd2-137">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="5cfd2-138">Начало работы с аналитикой озера данных Azure и U-SQL с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5cfd2-138">Get started with Azure Data Lake Analytics and U-SQL using Visual Studio</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="5cfd2-139">Управление аналитикой озера данных Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="5cfd2-139">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
