---
title: "aaaSQL сервера обработки и анализа примеры доступа к данным с помощью T-SQL и R, Python | Документы Microsoft"
description: "Примеры, демонстрирующие через hello использовать R, Python и T-SQL в SQL Server toodo прогнозной аналитике."
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
ms.openlocfilehash: 009354304da6cd02c4fd3cf948b7fa7d488cc4e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-data-science-walkthroughs-using-r-python-and-t-sql"></a><span data-ttu-id="0ef06-103">Пошаговые руководства по обработке и анализу данных в SQL Server с помощью T-SQL, R и Python</span><span class="sxs-lookup"><span data-stu-id="0ef06-103">SQL Server data science walkthroughs using R, Python and T-SQL</span></span>

<span data-ttu-id="0ef06-104">В этих пошаговых руководствах используется SQL Server, SQL Server R Services и служб SQL Server Python toodo прогнозирования.</span><span class="sxs-lookup"><span data-stu-id="0ef06-104">These walkthroughs use SQL Server, SQL Server R Services, and SQL Server Python Services toodo predictive analytics.</span></span> <span data-ttu-id="0ef06-105">Код R и Python развертывается в хранимых процедурах.</span><span class="sxs-lookup"><span data-stu-id="0ef06-105">R and Python code is deployed in stored procedures.</span></span> <span data-ttu-id="0ef06-106">Они следуют hello действия, описанные в hello командного процесса обработки и анализа данных.</span><span class="sxs-lookup"><span data-stu-id="0ef06-106">They follow hello steps outlined in hello Team Data Science Process.</span></span> <span data-ttu-id="0ef06-107">Обзор hello командного процесса обработки и анализа данных см. в разделе [процесса обработки и анализа данных](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0ef06-107">For an overview of hello Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> 

<span data-ttu-id="0ef06-108">Примеры обработки и анализа дополнительных данных, выполняемых hello командного процесса обработки и анализа данных будут сгруппированы по hello **платформы** используемой ими:</span><span class="sxs-lookup"><span data-stu-id="0ef06-108">Additional data science walkthroughs that execute hello Team Data Science Process are grouped by hello **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-python-and-sql-queries-with-sql-server"></a><span data-ttu-id="0ef06-109">Прогнозирование чаевых за поездку в такси с помощью запросов Python и SQL с SQL Server</span><span class="sxs-lookup"><span data-stu-id="0ef06-109">Predict taxi tips using Python and SQL queries with SQL Server</span></span> 

<span data-ttu-id="0ef06-110">Hello [использование SQL Server](machine-learning-data-science-process-sql-walkthrough.md) пошаговом руководстве показано создание и развертывание машины обучения классификации и модели регрессии с помощью SQL Server и общедоступным NYC такси маршрута и тариф авиакомпании набора данных.</span><span class="sxs-lookup"><span data-stu-id="0ef06-110">hello [Use SQL Server](machine-learning-data-science-process-sql-walkthrough.md) walkthrough shows how you build and deploy machine learning classification and regression models using SQL Server and a publicly available NYC taxi trip and fare dataset.</span></span>


## <a name="predict-taxi-tips-using-microsoft-r-with-sql-server"></a><span data-ttu-id="0ef06-111">Прогнозирование чаевых за поездку в такси с помощью Microsoft R с SQL Server</span><span class="sxs-lookup"><span data-stu-id="0ef06-111">Predict taxi tips using Microsoft R with SQL Server</span></span> 

<span data-ttu-id="0ef06-112">Hello [использование SQL Server R Services](https://msdn.microsoft.com/library/mt612857.aspx) Пошаговое руководство содержит специалистами по анализу данных с помощью комбинации элементов кода R, данных SQL Server и SQL пользовательские функции toobuild и развернуть tooSQL модели R Server.</span><span class="sxs-lookup"><span data-stu-id="0ef06-112">hello [Use SQL Server R Services](https://msdn.microsoft.com/library/mt612857.aspx) walkthrough provides data scientists with a combination of R code, SQL Server data, and custom SQL functions toobuild and deploy an R model tooSQL Server.</span></span> <span data-ttu-id="0ef06-113">Здравствуйте, пошаговое руководство — разработчики спроектированный toointroduce R tooR службы (в базе данных).</span><span class="sxs-lookup"><span data-stu-id="0ef06-113">hello walkthrough is designed toointroduce R developers tooR Services (In-Database).</span></span>


## <a name="predict-taxi-tips-using-r-from-t-sql-or-stored-procedures-with-sql-server"></a><span data-ttu-id="0ef06-114">Прогнозирование чаевых за поездку в такси с помощью R из T-SQL или хранимых процедур с SQL Server</span><span class="sxs-lookup"><span data-stu-id="0ef06-114">Predict taxi tips using R from T-SQL or stored procedures with SQL Server</span></span>

<span data-ttu-id="0ef06-115">Hello [Пошаговое руководство обработки и анализа данных для R и SQL Server](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/walkthrough-data-science-end-to-end-walkthrough) предоставляет программисты SQL опыт создания решения углубленной аналитики с помощью Transact-SQL с помощью решения toooperationalize R SQL Server R Services.</span><span class="sxs-lookup"><span data-stu-id="0ef06-115">hello [Data science walkthrough for R and SQL Server](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/walkthrough-data-science-end-to-end-walkthrough) provides SQL programmers with experience building an advanced analytics solution with Transact-SQL using SQL Server R Services toooperationalize an R solution.</span></span> 


## <a name="predict-taxi-tips-using-python-in-sql-server-stored-procedures"></a><span data-ttu-id="0ef06-116">Прогнозирование чаевых за поездку в такси с помощью Python в хранимых процедурах SQL Server</span><span class="sxs-lookup"><span data-stu-id="0ef06-116">Predict taxi tips using Python in SQL Server stored procedures</span></span>

<span data-ttu-id="0ef06-117">Hello [T-SQL используется со службами SQL Server Python](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers) Пошаговое руководство содержит программисты SQL с опыт создания машинного обучения решения в SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0ef06-117">hello [Use T-SQL with SQL Server Python Services](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers) walkthrough provides SQL programmers with experience building a machine learning solution in SQL Server.</span></span> <span data-ttu-id="0ef06-118">Здесь показано, как tooincorporate Python в приложение, добавив процедуры toostored кода Python.</span><span class="sxs-lookup"><span data-stu-id="0ef06-118">It demonstrates how tooincorporate Python into an application by adding Python code toostored procedures.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0ef06-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0ef06-119">Next steps</span></span>

<span data-ttu-id="0ef06-120">Обсуждение hello ключевые компоненты, которые составляют hello командного процесса обработки и анализа данных см. в разделе [Обзор процесса обработки и анализа данных командного](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0ef06-120">For a discussion of hello key components that comprise hello Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="0ef06-121">Обсуждение hello жизненного цикла командного процесса обработки и анализа данных, которые можно использовать toostructure проектами обработки и анализа данных, в разделе [жизненного цикла командного процесса обработки и анализа данных](data-science-process-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="0ef06-121">For a discussion of hello Team Data Science Process lifecycle that you can use toostructure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="0ef06-122">жизненный цикл Hello описаны шаги, hello, из начала toofinish, обычно выполняют проекты при их выполнении.</span><span class="sxs-lookup"><span data-stu-id="0ef06-122">hello lifecycle outlines hello steps, from start toofinish, that projects usually follow when they are executed.</span></span> 
