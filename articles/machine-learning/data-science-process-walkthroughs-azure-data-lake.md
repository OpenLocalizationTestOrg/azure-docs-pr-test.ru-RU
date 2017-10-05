---
title: "Пошаговые руководства по обработке и анализу данных в Azure Data Lake с помощью U-SQL | Документация Майкрософт"
description: "Примеры, демонстрирующие использование U-SQL в Azure Data Lake для выполнения прогнозной аналитики."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: 118fd5167e67b8259cde8b6e672be325a41a842d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-data-lake-data-science-walkthroughs-using-u-sql"></a><span data-ttu-id="612c7-103">Пошаговые руководства по обработке и анализу данных в Azure Data Lake с помощью U-SQL</span><span class="sxs-lookup"><span data-stu-id="612c7-103">Azure Data Lake data science walkthroughs using U-SQL</span></span>

<span data-ttu-id="612c7-104">В этих пошаговых руководствах для выполнения прогнозной аналитики используется U-SQL с Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="612c7-104">These walkthroughs use U-SQL with Azure Data Lake to do predictive analytics.</span></span> <span data-ttu-id="612c7-105">Выполните шаги, описанные в процессе обработки и анализа данных группы.</span><span class="sxs-lookup"><span data-stu-id="612c7-105">They follow the steps outlined in the Team Data Science Process.</span></span> <span data-ttu-id="612c7-106">Процесс обработки и анализа данных группы представлен в статье [Жизненный цикл процесса обработки и анализа данных группы](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="612c7-106">For an overview of the Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> <span data-ttu-id="612c7-107">Общие сведения об Azure Data Lake см. в статье [Обзор хранилища озера данных Azure](../data-lake-store/data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="612c7-107">For an introduction to Azure Data Lake, see [Overview of Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>

<span data-ttu-id="612c7-108">Дополнительные пошаговые руководства, в которых выполняется процесс обработки и анализа данных группы, объединены по используемой **платформе**:</span><span class="sxs-lookup"><span data-stu-id="612c7-108">Additional data science walkthroughs that execute the Team Data Science Process are grouped by the **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-u-sql-with-azure-data-lake"></a><span data-ttu-id="612c7-109">Прогнозирование чаевых за такси с помощью U-SQL с Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="612c7-109">Predict taxi tips using U-SQL with Azure Data Lake</span></span>

<span data-ttu-id="612c7-110">В статье [Полное пошаговое руководство по масштабируемому анализу данных с помощью Azure Data Lake](machine-learning-data-science-process-data-lake-walkthrough.md) на примере набора данных такси Нью-Йорка показано, как использовать Azure Data Lake для выполнения задач по исследованию и двоичной классификации данных, чтобы спрогнозировать вероятность уплаты чаевых клиентом.</span><span class="sxs-lookup"><span data-stu-id="612c7-110">The [Use Azure Data Lake for data science](machine-learning-data-science-process-data-lake-walkthrough.md) walkthrough shows how to use Azure Data Lake to do data exploration and binary classification tasks on a sample of the NYC taxi dataset to predict whether or not a tip is paid by a customer.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="612c7-111">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="612c7-111">Next steps</span></span>

<span data-ttu-id="612c7-112">Описание ключевых компонентов, составляющих процесс обработки и анализа данных группы, см. в статье [Жизненный цикл процесса обработки и анализа данных группы](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="612c7-112">For a discussion of the key components that comprise the Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="612c7-113">Описание жизненного цикла процесса обработки и анализа данных группы, который можно использовать для структурирования проектов по обработке и анализу данных, см. в статье [Жизненный цикл процесса обработки и анализа данных группы](data-science-process-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="612c7-113">For a discussion of the Team Data Science Process lifecycle that you can use to structure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="612c7-114">Этот жизненный цикл представляет стандартные этапы выполнения проектов, от самого начала и до завершения.</span><span class="sxs-lookup"><span data-stu-id="612c7-114">The lifecycle outlines the steps, from start to finish, that projects usually follow when they are executed.</span></span> 