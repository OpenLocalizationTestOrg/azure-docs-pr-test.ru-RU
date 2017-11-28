---
title: "aaaExplore данные в таблицах Hive с запросов Hive | Документы Microsoft"
description: "Просмотр данных в таблицах Hive с помощью запросов Hive."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0d46cea5-2b4c-4384-9bfa-fa20f6f75148
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 2ede3d41682aa08ced19284f7a83ec95e0c2a93a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-hive-tables-with-hive-queries"></a><span data-ttu-id="276ee-103">Просмотр данных в таблицах Hive с помощью запросов Hive</span><span class="sxs-lookup"><span data-stu-id="276ee-103">Explore data in Hive tables with Hive queries</span></span>
<span data-ttu-id="276ee-104">Этот документ содержит примеры сценариев Hive, используемые tooexplore данные в таблицах Hive в кластере HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="276ee-104">This document provides sample Hive scripts that are used tooexplore data in Hive tables in an HDInsight Hadoop cluster.</span></span>

<span data-ttu-id="276ee-105">следующие Hello **меню** связывает tootopics, описывающих, как toouse средств tooexplore данные из различных средах хранилища.</span><span class="sxs-lookup"><span data-stu-id="276ee-105">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="276ee-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="276ee-106">Prerequisites</span></span>
<span data-ttu-id="276ee-107">В этой статье предполагается, что вы:</span><span class="sxs-lookup"><span data-stu-id="276ee-107">This article assumes that you have:</span></span>

* <span data-ttu-id="276ee-108">Создали учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="276ee-108">Created an Azure storage account.</span></span> <span data-ttu-id="276ee-109">Инструкции см. в разделе [Создание учетной записи хранения](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="276ee-109">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="276ee-110">Подготовить настроенные кластеру с hello службы HDInsight.</span><span class="sxs-lookup"><span data-stu-id="276ee-110">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span> <span data-ttu-id="276ee-111">Инструкции см. в статье [Настройка кластеров Azure HDInsight Hadoop для процесса обработки и анализа данных группы](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="276ee-111">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="276ee-112">Hello данные были отправленного tooHive таблиц в Azure HDInsight Hadoop кластеров.</span><span class="sxs-lookup"><span data-stu-id="276ee-112">hello data has been uploaded tooHive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="276ee-113">Если она не установлена, следуйте инструкциям hello [Создание и загрузка таблиц данных tooHive](machine-learning-data-science-move-hive-tables.md) tooHive tooupload данных сначала таблиц.</span><span class="sxs-lookup"><span data-stu-id="276ee-113">If it has not, follow hello instructions in [Create and load data tooHive tables](machine-learning-data-science-move-hive-tables.md) tooupload data tooHive tables first.</span></span>
* <span data-ttu-id="276ee-114">Включить toohello кластера удаленного доступа.</span><span class="sxs-lookup"><span data-stu-id="276ee-114">Enabled remote access toohello cluster.</span></span> <span data-ttu-id="276ee-115">При необходимости инструкции в разделе [доступа hello головного узла кластера Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="276ee-115">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>
* <span data-ttu-id="276ee-116">При необходимости инструкции toosubmit запросов Hive, в разделе [как tooSubmit запросов Hive](machine-learning-data-science-move-hive-tables.md#submit)</span><span class="sxs-lookup"><span data-stu-id="276ee-116">If you need instructions on how toosubmit Hive queries, see [How tooSubmit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit)</span></span>

## <a name="example-hive-query-scripts-for-data-exploration"></a><span data-ttu-id="276ee-117">Пример сценариев запроса Hive для просмотра данных</span><span class="sxs-lookup"><span data-stu-id="276ee-117">Example Hive query scripts for data exploration</span></span>
1. <span data-ttu-id="276ee-118">Получение числа hello наблюдения на секцию`SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span><span class="sxs-lookup"><span data-stu-id="276ee-118">Get hello count of observations per partition  `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span></span>
2. <span data-ttu-id="276ee-119">Получение числа hello наблюдения за день`SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span><span class="sxs-lookup"><span data-stu-id="276ee-119">Get hello count of observations per day  `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span></span>
3. <span data-ttu-id="276ee-120">Получить уровней hello в категориальный столбец</span><span class="sxs-lookup"><span data-stu-id="276ee-120">Get hello levels in a categorical column</span></span>  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. <span data-ttu-id="276ee-121">Получить hello количество уровней в сочетании с двумя категориальные столбцы`SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span><span class="sxs-lookup"><span data-stu-id="276ee-121">Get hello number of levels in combination of two categorical columns  `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span></span>
5. <span data-ttu-id="276ee-122">Получить hello распространения для числовых столбцов.</span><span class="sxs-lookup"><span data-stu-id="276ee-122">Get hello distribution for numerical columns</span></span>  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. <span data-ttu-id="276ee-123">Извлечение записей из двух объединенных таблиц</span><span class="sxs-lookup"><span data-stu-id="276ee-123">Extract records from joining two tables</span></span>
   
        SELECT
            a.<common_columnname1> as <new_name1>,
            a.<common_columnname2> as <new_name2>,
            a.<a_column_name1> as <new_name3>,
            a.<a_column_name2> as <new_name4>,
            b.<b_column_name1> as <new_name5>,
            b.<b_column_name2> as <new_name6>
        FROM
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <a_column_name1>,
                <a_column_name2>,
            FROM <databasename>.<tablename1>
            ) a
            join
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <b_column_name1>,
                <b_column_name2>,
            FROM <databasename>.<tablename2>
            ) b
            ON a.<common_columnname1>=b.<common_columnname1> and a.<common_columnname2>=b.<common_columnname2>

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a><span data-ttu-id="276ee-124">Дополнительные сценарии запросов для сценариев данных о поездках такси</span><span class="sxs-lookup"><span data-stu-id="276ee-124">Additional query scripts for taxi trip data scenarios</span></span>
<span data-ttu-id="276ee-125">Примеры запросов, которые являются определенной[NYC такси обработки данных](http://chriswhong.com/open-data/foil_nyc_taxi/) сценарии также приведены в [репозитории GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span><span class="sxs-lookup"><span data-stu-id="276ee-125">Examples of queries that are specific too[NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="276ee-126">Эти запросы уже есть указана схема данных и будут готовы toobe отправлен toorun.</span><span class="sxs-lookup"><span data-stu-id="276ee-126">These queries already have data schema specified and are ready toobe submitted toorun.</span></span>

