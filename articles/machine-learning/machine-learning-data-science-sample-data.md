---
title: "aaaSample данные в Azure, контейнеры, SQL Server, больших двоичных объектов и куст таблицы | Документы Microsoft"
description: "Управление хранением данных tooexplore в различных enviromnents Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 80a9dfae-e3a6-4cfb-aecc-5701cfc7e39d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5a5295b59fa02f91da680fc7495a92ca135e26c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="229ef-103"><a name="heading"></a>Выборка данных в контейнерах больших двоичных объектов Azure, SQL Server и таблицах Hive</span><span class="sxs-lookup"><span data-stu-id="229ef-103"><a name="heading"></a>Sample data in Azure blob containers, SQL Server, and Hive tables</span></span>
<span data-ttu-id="229ef-104">В этом документе связывает tootopics, рассматриваются как toosample данные, которые хранятся в одном из трех разных местах Azure:</span><span class="sxs-lookup"><span data-stu-id="229ef-104">This document links tootopics that covers how toosample data that is stored in one of three different Azure locations:</span></span>

* <span data-ttu-id="229ef-105">**данных контейнера больших двоичных объектов Azure** осуществляется путем их программного скачивания и последующей выборки с помощью примера кода на языке Python.</span><span class="sxs-lookup"><span data-stu-id="229ef-105">**Azure blob container data** is sampled by downloading it programmatically and then sampling it with sample Python code.</span></span>
* <span data-ttu-id="229ef-106">**Данные SQL Server** выборки с помощью SQL и hello языка программирования Python.</span><span class="sxs-lookup"><span data-stu-id="229ef-106">**SQL Server data** is sampled using both SQL and hello Python Programming Language.</span></span> 
* <span data-ttu-id="229ef-107">**данных таблицы Hive** осуществляется с помощью запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="229ef-107">**Hive table data** is sampled using Hive queries.</span></span>

<span data-ttu-id="229ef-108">следующие Hello **меню** связывает toohello разделы, описывающие, как toosample данных от каждого из этих сред хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="229ef-108">hello following **menu** links toohello topics that describe how toosample data from each of these Azure storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="229ef-109">Эта задача выборка является этапом hello [процесса обработки и анализа данных Team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="229ef-109">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

<span data-ttu-id="229ef-110">**Для чего нужна выборка данных?**</span><span class="sxs-lookup"><span data-stu-id="229ef-110">**Why sample data?**</span></span>

<span data-ttu-id="229ef-111">При планировании tooanalyze dataset hello имеет большой размер, это обычно tooreduce данных рекомендуется toodown образец hello его tooa размер меньший, но репрезентативный и управляемость.</span><span class="sxs-lookup"><span data-stu-id="229ef-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="229ef-112">Это способствует пониманию данных, их исследованию и проектированию характеристик.</span><span class="sxs-lookup"><span data-stu-id="229ef-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="229ef-113">Его роль в hello процесса Cortana Analytics — tooenable быстрого создания прототипов функций обработки данных hello и машинного обучения моделей.</span><span class="sxs-lookup"><span data-stu-id="229ef-113">Its role in hello Cortana Analytics Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

