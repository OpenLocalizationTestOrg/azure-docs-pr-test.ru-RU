---
title: "Просмотр данных в таблицах Hive с помощью запросов Hive | Документация Майкрософт"
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
ms.openlocfilehash: 67a33a9abc3d3dcdd2fc7205e11feff97e3582a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="explore-data-in-hive-tables-with-hive-queries"></a><span data-ttu-id="b3e10-103">Просмотр данных в таблицах Hive с помощью запросов Hive</span><span class="sxs-lookup"><span data-stu-id="b3e10-103">Explore data in Hive tables with Hive queries</span></span>
<span data-ttu-id="b3e10-104">В этом документе представлено несколько примеров сценариев Hive, которые используются для анализа данных в таблицах Hive в кластере HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b3e10-104">This document provides sample Hive scripts that are used to explore data in Hive tables in an HDInsight Hadoop cluster.</span></span>

<span data-ttu-id="b3e10-105">Следующее **меню** содержит ссылки на статьи, описывающие использование средств для просмотра данных из различных сред хранения.</span><span class="sxs-lookup"><span data-stu-id="b3e10-105">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="b3e10-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b3e10-106">Prerequisites</span></span>
<span data-ttu-id="b3e10-107">В этой статье предполагается, что вы:</span><span class="sxs-lookup"><span data-stu-id="b3e10-107">This article assumes that you have:</span></span>

* <span data-ttu-id="b3e10-108">Создали учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="b3e10-108">Created an Azure storage account.</span></span> <span data-ttu-id="b3e10-109">Инструкции см. в разделе [Создание учетной записи хранения](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="b3e10-109">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="b3e10-110">Подготовили настраиваемый кластер Hadoop с помощью службы HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b3e10-110">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span> <span data-ttu-id="b3e10-111">Инструкции см. в статье [Настройка кластеров Azure HDInsight Hadoop для процесса обработки и анализа данных группы](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="b3e10-111">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="b3e10-112">Отправили данные в таблицы Hive, которые находятся в кластерах Azure HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b3e10-112">The data has been uploaded to Hive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="b3e10-113">Если данные не загружены, необходимо предварительно загрузить их в таблицы Hive, воспользовавшись инструкциями из статьи [Создание и загрузка данных в таблицы Hive из хранилища больших двоичных объектов Azure](machine-learning-data-science-move-hive-tables.md) .</span><span class="sxs-lookup"><span data-stu-id="b3e10-113">If it has not, follow the instructions in [Create and load data to Hive tables](machine-learning-data-science-move-hive-tables.md) to upload data to Hive tables first.</span></span>
* <span data-ttu-id="b3e10-114">Включили удаленный доступ к кластеру.</span><span class="sxs-lookup"><span data-stu-id="b3e10-114">Enabled remote access to the cluster.</span></span> <span data-ttu-id="b3e10-115">Инструкции можно найти в разделе [Доступ к головному узлу в кластере Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="b3e10-115">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>
* <span data-ttu-id="b3e10-116">Инструкции по отправке запросов Hive см. в разделе [Отправка запросов Hive](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="b3e10-116">If you need instructions on how to submit Hive queries, see [How to Submit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit)</span></span>

## <a name="example-hive-query-scripts-for-data-exploration"></a><span data-ttu-id="b3e10-117">Пример сценариев запроса Hive для просмотра данных</span><span class="sxs-lookup"><span data-stu-id="b3e10-117">Example Hive query scripts for data exploration</span></span>
1. <span data-ttu-id="b3e10-118">Узнайте количество наблюдений на раздел `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span><span class="sxs-lookup"><span data-stu-id="b3e10-118">Get the count of observations per partition  `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span></span>
2. <span data-ttu-id="b3e10-119">Узнайте количество наблюдений в день `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span><span class="sxs-lookup"><span data-stu-id="b3e10-119">Get the count of observations per day  `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span></span>
3. <span data-ttu-id="b3e10-120">Получение уровней в столбце категорий </span><span class="sxs-lookup"><span data-stu-id="b3e10-120">Get the levels in a categorical column</span></span>  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. <span data-ttu-id="b3e10-121">Узнайте число уровней в сочетании двух столбцов категорий `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span><span class="sxs-lookup"><span data-stu-id="b3e10-121">Get the number of levels in combination of two categorical columns  `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span></span>
5. <span data-ttu-id="b3e10-122">Получение распределения для числовых столбцов </span><span class="sxs-lookup"><span data-stu-id="b3e10-122">Get the distribution for numerical columns</span></span>  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. <span data-ttu-id="b3e10-123">Извлечение записей из двух объединенных таблиц</span><span class="sxs-lookup"><span data-stu-id="b3e10-123">Extract records from joining two tables</span></span>
   
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

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a><span data-ttu-id="b3e10-124">Дополнительные сценарии запросов для сценариев данных о поездках такси</span><span class="sxs-lookup"><span data-stu-id="b3e10-124">Additional query scripts for taxi trip data scenarios</span></span>
<span data-ttu-id="b3e10-125">Кроме того, в [репозитории GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) приведены примеры запросов, которые используются для сценариев наподобие [Данные о поездках в такси по Нью-Йорку](http://chriswhong.com/open-data/foil_nyc_taxi/).</span><span class="sxs-lookup"><span data-stu-id="b3e10-125">Examples of queries that are specific to [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="b3e10-126">Для этих запросов уже задана схема данных, и они готовы к отправке и запуску.</span><span class="sxs-lookup"><span data-stu-id="b3e10-126">These queries already have data schema specified and are ready to be submitted to run.</span></span>

