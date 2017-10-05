---
title: "Загрузка данных в среды службы хранилища Azure для аналитики | Документация Майкрософт"
description: "Перемещение данных в хранилище больших двоичных объектов Azure и из него"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b8fbef77-3e80-4911-8e84-23dbf42c9bee
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 7fbf3bfedca8fa57a5e9428c9399558992b4acbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-into-storage-environments-for-analytics"></a><span data-ttu-id="755bb-103">Загрузка данных в среды хранения для аналитики</span><span class="sxs-lookup"><span data-stu-id="755bb-103">Load data into storage environments for analytics</span></span>
<span data-ttu-id="755bb-104">Процесс обработки и анализа данных группы требует приема или загрузки данных в различные среды хранения для обработки или анализа наиболее подходящим способом на каждом этапе процесса.</span><span class="sxs-lookup"><span data-stu-id="755bb-104">The Team Data Science Process requires that data be ingested or loaded into a variety of different storage environments to be processed or analyzed in the most appropriate way in each stage of the process.</span></span> <span data-ttu-id="755bb-105">Для обработки обычно используются следующие места хранения данных: хранилище больших двоичных объектов Azure, базы данных SQL Azure, SQL Server на виртуальной машине Azure, HDInsight (Hadoop) и Машинное обучение Azure.</span><span class="sxs-lookup"><span data-stu-id="755bb-105">Data destinations commonly used for processing include Azure Blob Storage, SQL Azure databases, SQL Server on Azure VM, HDInsight (Hadoop), and Azure Machine Learning.</span></span> 

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="755bb-106">Это **меню** содержит ссылки на статьи, описывающие прием данных в эти целевые среды, где они могут храниться и обрабатываться.</span><span class="sxs-lookup"><span data-stu-id="755bb-106">This **menu** links to topics that describe how to ingest data into these target environments where the data is stored and processed.</span></span>

<span data-ttu-id="755bb-107">Целевые среды, в которые требуется принять данные, чтобы достичь целей анализа определят технические требования и потребности бизнеса, а также исходное расположение, формат и размер данных.</span><span class="sxs-lookup"><span data-stu-id="755bb-107">Technical and business needs, as well as the initial location, format and size of your data will determine the target environments into which the data needs to be ingested to achieve the goals of your analysis.</span></span> <span data-ttu-id="755bb-108">Нередки сценарии, когда требуется перемещать данные между несколькими средами для выполнения различных задач, необходимых для построения прогнозирующей модели.</span><span class="sxs-lookup"><span data-stu-id="755bb-108">It is not uncommon for a scenario to require data to be moved between several environments to achieve the variety of tasks required to construct a predictive model.</span></span> <span data-ttu-id="755bb-109">Эта последовательность задач может включать в себя, например, просмотр данных, предварительную обработку, очистку, понижение частоты выборки и обучение модели.</span><span class="sxs-lookup"><span data-stu-id="755bb-109">This sequence of tasks can include, for example, data exploration, pre-processing, cleaning, down-sampling, and model training.</span></span>

