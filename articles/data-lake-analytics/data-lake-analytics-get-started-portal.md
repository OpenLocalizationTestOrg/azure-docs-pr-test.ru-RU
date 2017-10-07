---
title: "aaaGet работает с аналитики Озера данных Azure, с помощью портала Azure | Документы Microsoft"
description: "Узнайте, как создать задание аналитики Озера данных с помощью U-SQL toouse hello Azure портала toocreate учетную запись аналитики Озера данных и отправить задание hello. "
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: b1584d16-e0d2-4019-ad1f-f04be8c5b430
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: edmaca
ms.openlocfilehash: 6bb54404fa42cfed25b18bc2bfb7c72e6c361149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a><span data-ttu-id="2f89b-103">Начало работы с Azure Data Lake Analytics с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="2f89b-103">Get started with Azure Data Lake Analytics using Azure portal</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="2f89b-104">Узнайте, как toouse hello учетных записей Azure портала toocreate аналитики Озера данных Azure, определить задания в [U-SQL](data-lake-analytics-u-sql-get-started.md)и служба аналитики Озера данных toohello задания отправки.</span><span class="sxs-lookup"><span data-stu-id="2f89b-104">Learn how toouse hello Azure portal toocreate Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs toohello Data Lake Analytics service.</span></span> <span data-ttu-id="2f89b-105">Дополнительные сведения о Data Lake Analytics см. в [обзоре Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2f89b-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f89b-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2f89b-106">Prerequisites</span></span>

<span data-ttu-id="2f89b-107">Прежде чем приступать к изучению этого руководства, необходимо оформить **подписку Azure**.</span><span class="sxs-lookup"><span data-stu-id="2f89b-107">Before you begin this tutorial, you must have an **Azure subscription**.</span></span> <span data-ttu-id="2f89b-108">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f89b-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="2f89b-109">Создание учетной записи аналитики озера данных</span><span class="sxs-lookup"><span data-stu-id="2f89b-109">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="2f89b-110">Теперь вы создадите аналитики Озера данных и хранилище Озера данных учетной записи в hello же время.</span><span class="sxs-lookup"><span data-stu-id="2f89b-110">Now, you will create a Data Lake Analytics and a Data Lake Store account at hello same time.</span></span>  <span data-ttu-id="2f89b-111">Этот шаг является простым и только занимает около toofinish 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="2f89b-111">This step is simple and only takes about 60 seconds toofinish.</span></span>

1. <span data-ttu-id="2f89b-112">Войдите на toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2f89b-112">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2f89b-113">Щелкните **Создать** >  **Данные+аналитика** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="2f89b-113">Click **New** >  **Data + Analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="2f89b-114">Выберите значения для hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="2f89b-114">Select values for hello following items:</span></span>
   * <span data-ttu-id="2f89b-115">**Имя**: имя учетной записи Data Lake Analytics (разрешены только строчные буквы и цифры).</span><span class="sxs-lookup"><span data-stu-id="2f89b-115">**Name**: Name your Data Lake Analytics account (Only lower case letters and numbers allowed).</span></span>
   * <span data-ttu-id="2f89b-116">**Подписки**: выберите hello подписку Azure, используемую для hello Analytics учетной записи.</span><span class="sxs-lookup"><span data-stu-id="2f89b-116">**Subscription**: Choose hello Azure subscription used for hello Analytics account.</span></span>
   * <span data-ttu-id="2f89b-117">**Группа ресурсов**: выберите существующую группу ресурсов Azure или создайте новую группу.</span><span class="sxs-lookup"><span data-stu-id="2f89b-117">**Resource Group**.</span></span> <span data-ttu-id="2f89b-118">Обычно приложения состоят из множества компонентов, например веб-приложения, базы данных, сервера базы данных, хранилища и служб сторонних поставщиков.</span><span class="sxs-lookup"><span data-stu-id="2f89b-118">Select an existing Azure Resource Group or create a new one.</span></span>
   * <span data-ttu-id="2f89b-119">**Расположение.**</span><span class="sxs-lookup"><span data-stu-id="2f89b-119">**Location**.</span></span> <span data-ttu-id="2f89b-120">Выберите центр данных Azure для учетной записи аналитики Озера данных hello.</span><span class="sxs-lookup"><span data-stu-id="2f89b-120">Select an Azure data center for hello Data Lake Analytics account.</span></span>
   * <span data-ttu-id="2f89b-121">**Хранилище Озера данных**: следуйте toocreate hello инструкция новую учетную запись хранилища Озера данных, или выберите существующий.</span><span class="sxs-lookup"><span data-stu-id="2f89b-121">**Data Lake Store**: Follow hello instruction toocreate a new Data Lake Store account, or select an existing one.</span></span> 
4. <span data-ttu-id="2f89b-122">При необходимости выберите ценовую категорию для учетной записи Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2f89b-122">Optionally, select a pricing tier for your Data Lake Analytics account.</span></span>
5. <span data-ttu-id="2f89b-123">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2f89b-123">Click **Create**.</span></span> 


## <a name="your-first-u-sql-script"></a><span data-ttu-id="2f89b-124">Первый скрипт U-SQL</span><span class="sxs-lookup"><span data-stu-id="2f89b-124">Your first U-SQL script</span></span>

<span data-ttu-id="2f89b-125">После текста Hello является очень простой скрипт U-SQL.</span><span class="sxs-lookup"><span data-stu-id="2f89b-125">hello following text is a very simple U-SQL script.</span></span> <span data-ttu-id="2f89b-126">Он осуществляет — определить небольшой набор данных в рамках скрипта hello, а затем написать этот набор данных в хранилище Озера данных по умолчанию toohello как файл с именем `/data.csv`.</span><span class="sxs-lookup"><span data-stu-id="2f89b-126">All it does is define a small dataset within hello script and then write that dataset out toohello default Data Lake Store as a file called `/data.csv`.</span></span>

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

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="2f89b-127">Отправка задания U-SQL</span><span class="sxs-lookup"><span data-stu-id="2f89b-127">Submit a U-SQL job</span></span>

1. <span data-ttu-id="2f89b-128">Hello учетной записи аналитики Озера данных, щелкните **новое задание**.</span><span class="sxs-lookup"><span data-stu-id="2f89b-128">From hello Data Lake Analytics account, click **New Job**.</span></span>
2. <span data-ttu-id="2f89b-129">Вставьте текст hello hello скрипт U-SQL, показанном выше.</span><span class="sxs-lookup"><span data-stu-id="2f89b-129">Paste in hello text of hello U-SQL script shown above.</span></span> 
3. <span data-ttu-id="2f89b-130">Щелкните **Отправить задание**.</span><span class="sxs-lookup"><span data-stu-id="2f89b-130">Click **Submit Job**.</span></span>   
4. <span data-ttu-id="2f89b-131">Подождите, пока изменения состояния задания hello слишком**успешно**.</span><span class="sxs-lookup"><span data-stu-id="2f89b-131">Wait until hello job status changes too**Succeeded**.</span></span>
5. <span data-ttu-id="2f89b-132">Если не удалось выполнить задание hello, см. раздел [монитора и диагностика заданий аналитики Озера данных](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="2f89b-132">If hello job failed, see [Monitor and troubleshoot Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>
6. <span data-ttu-id="2f89b-133">Нажмите кнопку hello **вывода** , а затем щелкните `data.csv`.</span><span class="sxs-lookup"><span data-stu-id="2f89b-133">Click hello **Output** tab, and then click `data.csv`.</span></span> 

## <a name="see-also"></a><span data-ttu-id="2f89b-134">См. также</span><span class="sxs-lookup"><span data-stu-id="2f89b-134">See also</span></span>

* <span data-ttu-id="2f89b-135">tooget к разработке приложений U-SQL, в разделе [сценариев разработки U-SQL, с помощью средства Озера данных для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2f89b-135">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="2f89b-136">в разделе toolearn U-SQL [Приступая к работе с Azure аналитика Озера данных U-SQL языка](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2f89b-136">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="2f89b-137">Задачи управления описываются в руководстве по [управлению Azure Data Lake Analytics с помощью портала Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2f89b-137">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
