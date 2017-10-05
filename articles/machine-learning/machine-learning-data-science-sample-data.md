---
title: "Выборка данных в контейнерах больших двоичных объектов Azure, SQL Server и таблицах Hive | Документация Майкрософт"
description: "Изучение данных, хранящихся в различных средах Azure."
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
ms.openlocfilehash: 0683be564a88ef54882e8d882d196851ecac243d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="8c834-103"><a name="heading"></a>Выборка данных в контейнерах больших двоичных объектов Azure, SQL Server и таблицах Hive</span><span class="sxs-lookup"><span data-stu-id="8c834-103"><a name="heading"></a>Sample data in Azure blob containers, SQL Server, and Hive tables</span></span>
<span data-ttu-id="8c834-104">Этот документ содержит ссылки на статьи, рассказывающие, как получить выборку данных из одного из трех расположений Azure.</span><span class="sxs-lookup"><span data-stu-id="8c834-104">This document links to topics that covers how to sample data that is stored in one of three different Azure locations:</span></span>

* <span data-ttu-id="8c834-105">**данных контейнера больших двоичных объектов Azure** осуществляется путем их программного скачивания и последующей выборки с помощью примера кода на языке Python.</span><span class="sxs-lookup"><span data-stu-id="8c834-105">**Azure blob container data** is sampled by downloading it programmatically and then sampling it with sample Python code.</span></span>
* <span data-ttu-id="8c834-106">**данных SQL Server** осуществляется с помощью как SQL, так и языка программирования Python.</span><span class="sxs-lookup"><span data-stu-id="8c834-106">**SQL Server data** is sampled using both SQL and the Python Programming Language.</span></span> 
* <span data-ttu-id="8c834-107">**данных таблицы Hive** осуществляется с помощью запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="8c834-107">**Hive table data** is sampled using Hive queries.</span></span>

<span data-ttu-id="8c834-108">**Меню** ниже содержит ссылки на разделы, в которых описан процесс выборки данных из каждой среды хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="8c834-108">The following **menu** links to the topics that describe how to sample data from each of these Azure storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="8c834-109">Эта задача выборки является одним из этапов [процесса обработки и анализа данных группы (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="8c834-109">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

<span data-ttu-id="8c834-110">**Для чего нужна выборка данных?**</span><span class="sxs-lookup"><span data-stu-id="8c834-110">**Why sample data?**</span></span>

<span data-ttu-id="8c834-111">Если размер набора данных, который планируется проанализировать, слишком большой, обычно рекомендуется уменьшить выборку данных до размера, который останется репрезентативным и будет более управляемым.</span><span class="sxs-lookup"><span data-stu-id="8c834-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="8c834-112">Это способствует пониманию данных, их исследованию и проектированию характеристик.</span><span class="sxs-lookup"><span data-stu-id="8c834-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="8c834-113">Роль этой операции в процессе аналитики Кортаны заключается в том, чтобы сделать возможным быстрое прототипирование функций обработки данных и моделей машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="8c834-113">Its role in the Cortana Analytics Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

