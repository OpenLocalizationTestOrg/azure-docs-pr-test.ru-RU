---
title: "aaaLoad данных в хранилище Azure среды для аналитики | Документы Microsoft"
description: "Tooand перемещения данных из хранилища больших двоичных объектов"
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
ms.openlocfilehash: 0fea2290991f9fa63d9e46c3a657000e27d95289
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-storage-environments-for-analytics"></a><span data-ttu-id="33cb8-103">Загрузка данных в среды хранения для аналитики</span><span class="sxs-lookup"><span data-stu-id="33cb8-103">Load data into storage environments for analytics</span></span>
<span data-ttu-id="33cb8-104">Hello командного процесса обработки и анализа данных требуется, полученный или данные загружаются в различные хранилища различных сред toobe обработки или проанализировать в наиболее подходящий способ hello на каждом этапе процесса hello.</span><span class="sxs-lookup"><span data-stu-id="33cb8-104">hello Team Data Science Process requires that data be ingested or loaded into a variety of different storage environments toobe processed or analyzed in hello most appropriate way in each stage of hello process.</span></span> <span data-ttu-id="33cb8-105">Для обработки обычно используются следующие места хранения данных: хранилище больших двоичных объектов Azure, базы данных SQL Azure, SQL Server на виртуальной машине Azure, HDInsight (Hadoop) и Машинное обучение Azure.</span><span class="sxs-lookup"><span data-stu-id="33cb8-105">Data destinations commonly used for processing include Azure Blob Storage, SQL Azure databases, SQL Server on Azure VM, HDInsight (Hadoop), and Azure Machine Learning.</span></span> 

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="33cb8-106">Это **меню** связывает tootopics, которые описывают, как tooingest данные в этих целевых средах, где hello данные хранятся и обрабатываются.</span><span class="sxs-lookup"><span data-stu-id="33cb8-106">This **menu** links tootopics that describe how tooingest data into these target environments where hello data is stored and processed.</span></span>

<span data-ttu-id="33cb8-107">Технические и бизнес-требований, а также hello исходное расположение, форматирования и объемом данных определяют hello целевых средах, в которых hello данные должны toobe полученный tooachieve hello целей анализа.</span><span class="sxs-lookup"><span data-stu-id="33cb8-107">Technical and business needs, as well as hello initial location, format and size of your data will determine hello target environments into which hello data needs toobe ingested tooachieve hello goals of your analysis.</span></span> <span data-ttu-id="33cb8-108">Довольно часто для данных toobe toorequire сценарий, перемещать между несколько сред tooachieve hello разнообразных задач требуется tooconstruct прогнозной модели.</span><span class="sxs-lookup"><span data-stu-id="33cb8-108">It is not uncommon for a scenario toorequire data toobe moved between several environments tooachieve hello variety of tasks required tooconstruct a predictive model.</span></span> <span data-ttu-id="33cb8-109">Эта последовательность задач может включать в себя, например, просмотр данных, предварительную обработку, очистку, понижение частоты выборки и обучение модели.</span><span class="sxs-lookup"><span data-stu-id="33cb8-109">This sequence of tasks can include, for example, data exploration, pre-processing, cleaning, down-sampling, and model training.</span></span>

