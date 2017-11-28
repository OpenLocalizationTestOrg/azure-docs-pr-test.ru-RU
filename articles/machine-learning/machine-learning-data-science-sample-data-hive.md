---
title: "Выборка данных в таблицах Azure HDInsight Hive | Документация Майкрософт"
description: "Уменьшение выборки данных в таблицах Hive Azure HDInsight (Hadopop)"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f31e8d01-0fd4-4a10-b1a7-35de3c327521
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: d46297dfaf85976114fbf610803e5f1a997041e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a><span data-ttu-id="bd451-103">Выборка данных в таблицах Azure HDInsight Hive</span><span class="sxs-lookup"><span data-stu-id="bd451-103">Sample data in Azure HDInsight Hive tables</span></span>
<span data-ttu-id="bd451-104">В этой статье мы опишем, как уменьшить размер выборки данных, хранящихся в таблицах Azure HDInsight Hive, с помощью запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="bd451-104">In this article, we describe how to down-sample data stored in Azure HDInsight Hive tables using Hive queries.</span></span> <span data-ttu-id="bd451-105">Мы охватим три распространенных метода выборки:</span><span class="sxs-lookup"><span data-stu-id="bd451-105">We cover three popularly used sampling methods:</span></span>

* <span data-ttu-id="bd451-106">Универсальная случайная выборка</span><span class="sxs-lookup"><span data-stu-id="bd451-106">Uniform random sampling</span></span>
* <span data-ttu-id="bd451-107">Случайная выборка по группам</span><span class="sxs-lookup"><span data-stu-id="bd451-107">Random sampling by groups</span></span>
* <span data-ttu-id="bd451-108">Стратифицированная выборка</span><span class="sxs-lookup"><span data-stu-id="bd451-108">Stratified sampling</span></span>

<span data-ttu-id="bd451-109">**Меню** ниже содержит ссылки на разделы, в которых описана выборка данных из различных сред хранения.</span><span class="sxs-lookup"><span data-stu-id="bd451-109">The following **menu** links to topics that describe how to sample data from various storage environments.</span></span>

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="bd451-110">**Для чего нужна выборка данных?**</span><span class="sxs-lookup"><span data-stu-id="bd451-110">**Why sample your data?**</span></span>
<span data-ttu-id="bd451-111">Если размер набора данных, который планируется проанализировать, слишком большой, обычно рекомендуется уменьшить выборку данных до размера, который останется репрезентативным и будет более управляемым.</span><span class="sxs-lookup"><span data-stu-id="bd451-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="bd451-112">Это способствует пониманию данных, их исследованию и проектированию характеристик.</span><span class="sxs-lookup"><span data-stu-id="bd451-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="bd451-113">Роль этой операции в процессе обработки и анализа данных группы состоит в том, чтобы сделать возможным быстрое прототипирование функций обработки данных и моделей машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="bd451-113">Its role in the Team Data Science Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

<span data-ttu-id="bd451-114">Эта задача выборки является одним из этапов [процесса обработки и анализа данных группы (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="bd451-114">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="how-to-submit-hive-queries"></a><span data-ttu-id="bd451-115">Отправка запросов Hive</span><span class="sxs-lookup"><span data-stu-id="bd451-115">How to submit Hive queries</span></span>
<span data-ttu-id="bd451-116">Запросы Hive можно отправлять из окна командной строки Hadoop на головном узле кластера Hadoop.</span><span class="sxs-lookup"><span data-stu-id="bd451-116">Hive queries can be submitted from the Hadoop Command Line console on the head node of the Hadoop cluster.</span></span> <span data-ttu-id="bd451-117">Для этого войдите в головной узел кластера Hadoop, откройте окно командной строки Hadoop и отправьте оттуда запросы Hive.</span><span class="sxs-lookup"><span data-stu-id="bd451-117">To do this, log into the head node of the Hadoop cluster, open the Hadoop Command Line console, and submit the Hive queries from there.</span></span> <span data-ttu-id="bd451-118">Инструкции по отправке запросов Hive в консоли командной строки Hadoop см. в статье [Отправка запросов Hive](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="bd451-118">For instructions on submitting Hive queries in the Hadoop Command Line console, see [How to Submit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="bd451-119"><a name="uniform"></a> Универсальная случайная выборка</span><span class="sxs-lookup"><span data-stu-id="bd451-119"><a name="uniform"></a> Uniform random sampling</span></span>
<span data-ttu-id="bd451-120">Универсальная случайная выборка означает, что каждая строка в наборе данных может попасть в выборку с одинаковой вероятностью.</span><span class="sxs-lookup"><span data-stu-id="bd451-120">Uniform random sampling means that each row in the data set has an equal chance of being sampled.</span></span> <span data-ttu-id="bd451-121">Это можно реализовать, добавив дополнительное поле rand() в набор данных во внутреннем запросе "select", а также во внешнем запросе "select" с условной зависимостью от этого случайного поля.</span><span class="sxs-lookup"><span data-stu-id="bd451-121">This can be implemented by adding an extra field rand() to the data set in the inner "select" query, and in the outer "select" query that condition on that random field.</span></span>

<span data-ttu-id="bd451-122">Вот пример запроса:</span><span class="sxs-lookup"><span data-stu-id="bd451-122">Here is an example query:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, …, fieldN
    from
        (
        select
            field1, field2, …, fieldN, rand() as samplekey
        from <hive table name>
        )a
    where samplekey<='${hiveconf:sampleRate}'

<span data-ttu-id="bd451-123">Здесь `<sample rate, 0-1>` указывает долю записей, которые пользователи желают включить в выборку.</span><span class="sxs-lookup"><span data-stu-id="bd451-123">Here, `<sample rate, 0-1>` specifies the proportion of records that the users want to sample.</span></span>

## <span data-ttu-id="bd451-124"><a name="group"></a> Случайная выборка по группам</span><span class="sxs-lookup"><span data-stu-id="bd451-124"><a name="group"></a> Random sampling by groups</span></span>
<span data-ttu-id="bd451-125">При выборке данных о категориях может быть необходимо либо включить, либо исключить все экземпляры определенного значения переменной категории.</span><span class="sxs-lookup"><span data-stu-id="bd451-125">When sampling categorical data, you may want to either include or exclude all of the instances of some particular value of a categorical variable.</span></span> <span data-ttu-id="bd451-126">Это называется "выборкой по группам".</span><span class="sxs-lookup"><span data-stu-id="bd451-126">This is what is meant by "sampling by group".</span></span>
<span data-ttu-id="bd451-127">Например, если имеется переменная категории "Штат" со значениями NY, MA, CA, NJ, PA и т. д., необходимо, чтобы записи одного и того же штата всегда были вместе, независимо от их включения в выборку.</span><span class="sxs-lookup"><span data-stu-id="bd451-127">For example, if you have a categorical variable "State", which has values NY, MA, CA, NJ, PA, etc, you want records of the same state be always together, whether they are sampled or not.</span></span>

<span data-ttu-id="bd451-128">Вот пример запроса с выборкой по группам:</span><span class="sxs-lookup"><span data-stu-id="bd451-128">Here is an example query that samples by group:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        b.field1, b.field2, …, b.catfield, …, b.fieldN
    from
        (
        select
            field1, field2, …, catfield, …, fieldN
        from <table name>
        )b
    join
        (
        select
            catfield
        from
            (
            select
                catfield, rand() as samplekey
            from <table name>
            group by catfield
            )a
        where samplekey<='${hiveconf:sampleRate}'
        )c
    on b.catfield=c.catfield

## <span data-ttu-id="bd451-129"><a name="stratified"></a>Стратифицированная выборка</span><span class="sxs-lookup"><span data-stu-id="bd451-129"><a name="stratified"></a>Stratified sampling</span></span>
<span data-ttu-id="bd451-130">Случайная выборка является стратифицированной по отношению к переменной категории, когда выбранные данные имеют значения этой категории, содержащиеся в такой же пропорции, как и в родительской популяции, из которой была получена выборка.</span><span class="sxs-lookup"><span data-stu-id="bd451-130">Random sampling is stratified with respect to a categorical variable when the samples obtained have values of that categorical that are in the same ratio as in the parent population from which the samples were obtained.</span></span> <span data-ttu-id="bd451-131">Используя тот же вышеупомянутый пример, предположим, что в данных имеются субпопуляции по штатам, например для NJ имеется 100 наблюдений, для NY — 60 наблюдений, для WA — 300.</span><span class="sxs-lookup"><span data-stu-id="bd451-131">Using the same example as above, suppose your data has sub-populations by states, say NJ has 100 observations, NY has 60 observations, and WA has 300 observations.</span></span> <span data-ttu-id="bd451-132">Если указать коэффициент стратифицированной выборки 0,5, то в полученной выборке должно быть примерно по 50, 30 и 150 наблюдений из штатов NJ, NY и WA соответственно.</span><span class="sxs-lookup"><span data-stu-id="bd451-132">If you specify the rate of stratified sampling to be 0.5, then the sample obtained should have approximately 50, 30, and 150 observations of NJ, NY, and WA respectively.</span></span>

<span data-ttu-id="bd451-133">Вот пример запроса:</span><span class="sxs-lookup"><span data-stu-id="bd451-133">Here is an example query:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, field3, ..., fieldN, state
    from
        (
        select
            field1, field2, field3, ..., fieldN, state,
            count(*) over (partition by state) as state_cnt,
              rank() over (partition by state order by rand()) as state_rank
          from <table name>
        ) a
    where state_rank <= state_cnt*'${hiveconf:sampleRate}'


<span data-ttu-id="bd451-134">Сведения о дополнительных методах выборки, доступных в Hive, см. на странице [руководства по выборке](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span><span class="sxs-lookup"><span data-stu-id="bd451-134">For information on more advanced sampling methods that are available in Hive, see [LanguageManual Sampling](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span></span>

