---
title: "Начало работы с Azure Data Lake Analytics с помощью портала Azure | Документация Майкрософт"
description: "Узнайте, как использовать портал Azure для создания учетной записи Data Lake Analytics, создания задания Data Lake Analytics с помощью U-SQL и его отправки. "
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
ms.openlocfilehash: 2722a2d72ed90ea0005362563ecaee30750c040a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a><span data-ttu-id="2da30-103">Начало работы с Azure Data Lake Analytics с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="2da30-103">Get started with Azure Data Lake Analytics using Azure portal</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="2da30-104">Узнайте, как с помощью портала Azure создавать учетные записи Azure Data Lake Analytics, определять задания в [U-SQL](data-lake-analytics-u-sql-get-started.md) и отправлять их в службу Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2da30-104">Learn how to use the Azure portal to create Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to the Data Lake Analytics service.</span></span> <span data-ttu-id="2da30-105">Дополнительные сведения о Data Lake Analytics см. в [обзоре Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2da30-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2da30-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2da30-106">Prerequisites</span></span>

<span data-ttu-id="2da30-107">Прежде чем приступать к изучению этого руководства, необходимо оформить **подписку Azure**.</span><span class="sxs-lookup"><span data-stu-id="2da30-107">Before you begin this tutorial, you must have an **Azure subscription**.</span></span> <span data-ttu-id="2da30-108">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2da30-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="2da30-109">Создание учетной записи аналитики озера данных</span><span class="sxs-lookup"><span data-stu-id="2da30-109">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="2da30-110">Теперь мы одновременно создадим учетные записи Data Lake Analytics и Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2da30-110">Now, you will create a Data Lake Analytics and a Data Lake Store account at the same time.</span></span>  <span data-ttu-id="2da30-111">Этот простой шаг занимает около минуты.</span><span class="sxs-lookup"><span data-stu-id="2da30-111">This step is simple and only takes about 60 seconds to finish.</span></span>

1. <span data-ttu-id="2da30-112">Выполните вход на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2da30-112">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2da30-113">Щелкните **Создать** >  **Данные+аналитика** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="2da30-113">Click **New** >  **Data + Analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="2da30-114">Выберите значения для следующих параметров:</span><span class="sxs-lookup"><span data-stu-id="2da30-114">Select values for the following items:</span></span>
   * <span data-ttu-id="2da30-115">**Имя**: имя учетной записи Data Lake Analytics (разрешены только строчные буквы и цифры).</span><span class="sxs-lookup"><span data-stu-id="2da30-115">**Name**: Name your Data Lake Analytics account (Only lower case letters and numbers allowed).</span></span>
   * <span data-ttu-id="2da30-116">**Подписка**: выберите подписку Azure, которая используется для учетной записи аналитики.</span><span class="sxs-lookup"><span data-stu-id="2da30-116">**Subscription**: Choose the Azure subscription used for the Analytics account.</span></span>
   * <span data-ttu-id="2da30-117">**Группа ресурсов**: выберите существующую группу ресурсов Azure или создайте новую группу.</span><span class="sxs-lookup"><span data-stu-id="2da30-117">**Resource Group**.</span></span> <span data-ttu-id="2da30-118">Обычно приложения состоят из множества компонентов, например веб-приложения, базы данных, сервера базы данных, хранилища и служб сторонних поставщиков.</span><span class="sxs-lookup"><span data-stu-id="2da30-118">Select an existing Azure Resource Group or create a new one.</span></span>
   * <span data-ttu-id="2da30-119">**Расположение.**</span><span class="sxs-lookup"><span data-stu-id="2da30-119">**Location**.</span></span> <span data-ttu-id="2da30-120">выберите центр обработки данных Azure для учетной записи аналитики озера данных.</span><span class="sxs-lookup"><span data-stu-id="2da30-120">Select an Azure data center for the Data Lake Analytics account.</span></span>
   * <span data-ttu-id="2da30-121">**Data Lake Store.** Следуйте инструкциям для создания учетной записи Data Lake Store или выберите имеющуюся.</span><span class="sxs-lookup"><span data-stu-id="2da30-121">**Data Lake Store**: Follow the instruction to create a new Data Lake Store account, or select an existing one.</span></span> 
4. <span data-ttu-id="2da30-122">При необходимости выберите ценовую категорию для учетной записи Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2da30-122">Optionally, select a pricing tier for your Data Lake Analytics account.</span></span>
5. <span data-ttu-id="2da30-123">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2da30-123">Click **Create**.</span></span> 


## <a name="your-first-u-sql-script"></a><span data-ttu-id="2da30-124">Первый скрипт U-SQL</span><span class="sxs-lookup"><span data-stu-id="2da30-124">Your first U-SQL script</span></span>

<span data-ttu-id="2da30-125">Ниже приводится очень простой скрипт U-SQL.</span><span class="sxs-lookup"><span data-stu-id="2da30-125">The following text is a very simple U-SQL script.</span></span> <span data-ttu-id="2da30-126">Он определяет небольшой набор данных (в рамках скрипта) и записывает его в Azure Data Lake Store по умолчанию как файл с именем `/data.csv`.</span><span class="sxs-lookup"><span data-stu-id="2da30-126">All it does is define a small dataset within the script and then write that dataset out to the default Data Lake Store as a file called `/data.csv`.</span></span>

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

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="2da30-127">Отправка задания U-SQL</span><span class="sxs-lookup"><span data-stu-id="2da30-127">Submit a U-SQL job</span></span>

1. <span data-ttu-id="2da30-128">В учетной записи Data Lake Analytics щелкните **Новое задание**.</span><span class="sxs-lookup"><span data-stu-id="2da30-128">From the Data Lake Analytics account, click **New Job**.</span></span>
2. <span data-ttu-id="2da30-129">Вставьте в текст скрипт U-SQL, представленный выше.</span><span class="sxs-lookup"><span data-stu-id="2da30-129">Paste in the text of the U-SQL script shown above.</span></span> 
3. <span data-ttu-id="2da30-130">Щелкните **Отправить задание**.</span><span class="sxs-lookup"><span data-stu-id="2da30-130">Click **Submit Job**.</span></span>   
4. <span data-ttu-id="2da30-131">Подождите, пока состояние задания не изменится на **Успешно**.</span><span class="sxs-lookup"><span data-stu-id="2da30-131">Wait until the job status changes to **Succeeded**.</span></span>
5. <span data-ttu-id="2da30-132">Если задание завершилось сбоем, см. сведения о [мониторинге и устранении неполадок с заданиями Azure Data Lake Analytics](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="2da30-132">If the job failed, see [Monitor and troubleshoot Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>
6. <span data-ttu-id="2da30-133">Перейдите на вкладку **Выходные данные** и щелкните `data.csv`.</span><span class="sxs-lookup"><span data-stu-id="2da30-133">Click the **Output** tab, and then click `data.csv`.</span></span> 

## <a name="see-also"></a><span data-ttu-id="2da30-134">См. также</span><span class="sxs-lookup"><span data-stu-id="2da30-134">See also</span></span>

* <span data-ttu-id="2da30-135">Чтобы приступить к разработке приложений U-SQL, ознакомьтесь со статьей [Разработка скриптов U-SQL с помощью средств озера данных для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2da30-135">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="2da30-136">Для знакомства с U-SQL см. статью о [начале работы с языком U-SQL для Azure Data Lake Analytics](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2da30-136">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="2da30-137">Задачи управления описываются в руководстве по [управлению Azure Data Lake Analytics с помощью портала Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2da30-137">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
