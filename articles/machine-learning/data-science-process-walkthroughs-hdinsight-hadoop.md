---
title: "Пошаговое руководство по обработке и анализу данных HDInsight Hadoop с использованием Hive в Azure | Документация Майкрософт"
description: "Примеры процесса обработки и анализа данных группы, которые объясняют, как использовать Hive в Azure HDInsight Hadoop для прогнозной аналитики."
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
ms.openlocfilehash: fb06c3c1b1ae30d970a2e4d45a49e22e9d78b876
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="hdinsight-hadoop-data-science-walkthroughs-using-hive-on-azure"></a><span data-ttu-id="280e9-103">Пошаговое руководство по обработке и анализу данных HDInsight Hadoop с использованием Hive в Azure</span><span class="sxs-lookup"><span data-stu-id="280e9-103">HDInsight Hadoop data science walkthroughs using Hive on Azure</span></span> 

<span data-ttu-id="280e9-104">В этих пошаговых руководствах для прогнозной аналитики с кластером HDInsight Hadoop используется Hive.</span><span class="sxs-lookup"><span data-stu-id="280e9-104">These walkthroughs use Hive with an HDInsight Hadoop cluster to do predictive analytics.</span></span> <span data-ttu-id="280e9-105">Они предусматривают выполнение инструкций, описанных в процессе обработки и анализа данных группы.</span><span class="sxs-lookup"><span data-stu-id="280e9-105">They follow the steps outlined in the Team Data Science Process.</span></span> <span data-ttu-id="280e9-106">Процесс обработки и анализа данных группы представлен в статье [Жизненный цикл процесса обработки и анализа данных группы](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="280e9-106">For an overview of the Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> <span data-ttu-id="280e9-107">Обзор Azure HDInsight см. в статье [Общие сведения об Azure HDInsight, технологической платформе Hadoop и кластерах Hadoop](../hdinsight/hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="280e9-107">For an introduction to Azure HDInsight, see [Introduction to Azure HDInsight, the Hadoop technology stack, and Hadoop clusters](../hdinsight/hdinsight-hadoop-introduction.md).</span></span>

<span data-ttu-id="280e9-108">Дополнительные пошаговые инструкции по обработке и анализу данных группы объединены по используемой **платформе**:</span><span class="sxs-lookup"><span data-stu-id="280e9-108">Additional data science walkthroughs that execute the Team Data Science Process are grouped by the **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="280e9-109">Прогнозирование чаевых за поездку в такси при помощи Hive с HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="280e9-109">Predict taxi tips using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="280e9-110">В пошаговом руководстве [Процесс обработки и анализа данных группы на практике: использование кластеров Azure HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md) для прогнозирования используются данные такси Нью-Йорка:</span><span class="sxs-lookup"><span data-stu-id="280e9-110">The [Use HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) walkthrough uses data from New York taxis to predict:</span></span> 

- <span data-ttu-id="280e9-111">Оставлены ли чаевые</span><span class="sxs-lookup"><span data-stu-id="280e9-111">Whether a tip is paid</span></span> 
- <span data-ttu-id="280e9-112">Распределение сумм чаевых</span><span class="sxs-lookup"><span data-stu-id="280e9-112">The distribution of tip amounts</span></span>

<span data-ttu-id="280e9-113">Сценарий реализуется с помощью Hive и [кластера Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="280e9-113">The scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/).</span></span> <span data-ttu-id="280e9-114">Вы узнаете, как хранить, изучать и проектировать признаки данных из общедоступного набора данных о поездках и тарифах в такси Нью-Йорка.</span><span class="sxs-lookup"><span data-stu-id="280e9-114">You learn how to store, explore, and feature engineer data from a publicly available NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="280e9-115">Для сборки и развертывания моделей вы будет использовать машинное обучение Azure.</span><span class="sxs-lookup"><span data-stu-id="280e9-115">You also use Azure Machine Learning to build and deploy the models.</span></span>

## <a name="predict-advertisement-clicks-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="280e9-116">Прогнозирование переходов по рекламным объявлениям с помощью Hive с HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="280e9-116">Predict advertisement clicks using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="280e9-117">В пошаговом руководстве [Процесс обработки и анализа данных группы на практике: использование кластера Azure HDInsight Hadoop с набором данных объемом 1 ТБ](machine-learning-data-science-process-hive-criteo-walkthrough.md) используется общедоступный набор данных переходов [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/), чтобы спрогнозировать, будут ли оставлены чаевые, и определить диапазон ожидаемых сумм.</span><span class="sxs-lookup"><span data-stu-id="280e9-117">The [Use Azure HDInsight Hadoop Clusters on a 1-TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md) walkthrough uses a publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) click dataset to predict whether a tip is paid and the range of amounts expected.</span></span> <span data-ttu-id="280e9-118">Сценарий реализуется с помощью Hive с [кластером Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) и используется для хранения, изучения, проектирования признаков и сокращения выборки данных.</span><span class="sxs-lookup"><span data-stu-id="280e9-118">The scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, feature engineer, and down sample data.</span></span> <span data-ttu-id="280e9-119">В сценарии применяется машинное обучение Azure для создания, обучения и оценки модели двоичной классификации, прогнозирующей, щелкнет ли пользователь рекламное объявление.</span><span class="sxs-lookup"><span data-stu-id="280e9-119">It uses Azure Machine Learning to build, train, and score a binary classification model predicting whether a user clicks on an advertisement.</span></span> <span data-ttu-id="280e9-120">В конце пошагового руководства показано, как опубликовать одну из этих моделей в качестве веб-службы.</span><span class="sxs-lookup"><span data-stu-id="280e9-120">The walkthrough concludes showing how to publish one of these models as a Web service.</span></span>


## <a name="next-steps"></a><span data-ttu-id="280e9-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="280e9-121">Next steps</span></span>

<span data-ttu-id="280e9-122">Описание ключевых компонентов, составляющих процесс обработки и анализа данных группы, см. в статье [Жизненный цикл процесса обработки и анализа данных группы](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="280e9-122">For a discussion of the key components that comprise the Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="280e9-123">Описание жизненного цикла процесса обработки и анализа данных группы, который можно использовать для структурирования проектов по обработке и анализу данных, см. в статье [Жизненный цикл процесса обработки и анализа данных группы](data-science-process-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="280e9-123">For a discussion of the Team Data Science Process lifecycle that you can use to structure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="280e9-124">Этот жизненный цикл представляет стандартные этапы выполнения проектов, от самого начала и до завершения.</span><span class="sxs-lookup"><span data-stu-id="280e9-124">The lifecycle outlines the steps, from start to finish, that projects usually follow when they are executed.</span></span> 

