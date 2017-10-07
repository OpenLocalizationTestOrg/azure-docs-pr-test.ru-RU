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
# <a name="explore-data-in-hive-tables-with-hive-queries"></a>Просмотр данных в таблицах Hive с помощью запросов Hive
Этот документ содержит примеры сценариев Hive, используемые tooexplore данные в таблицах Hive в кластере HDInsight Hadoop.

следующие Hello **меню** связывает tootopics, описывающих, как toouse средств tooexplore данные из различных средах хранилища.

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается, что вы:

* Создали учетную запись хранения Azure. Инструкции см. в разделе [Создание учетной записи хранения](../storage/common/storage-create-storage-account.md#create-a-storage-account).
* Подготовить настроенные кластеру с hello службы HDInsight. Инструкции см. в статье [Настройка кластеров Azure HDInsight Hadoop для процесса обработки и анализа данных группы](machine-learning-data-science-customize-hadoop-cluster.md).
* Hello данные были отправленного tooHive таблиц в Azure HDInsight Hadoop кластеров. Если она не установлена, следуйте инструкциям hello [Создание и загрузка таблиц данных tooHive](machine-learning-data-science-move-hive-tables.md) tooHive tooupload данных сначала таблиц.
* Включить toohello кластера удаленного доступа. При необходимости инструкции в разделе [доступа hello головного узла кластера Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).
* При необходимости инструкции toosubmit запросов Hive, в разделе [как tooSubmit запросов Hive](machine-learning-data-science-move-hive-tables.md#submit)

## <a name="example-hive-query-scripts-for-data-exploration"></a>Пример сценариев запроса Hive для просмотра данных
1. Получение числа hello наблюдения на секцию`SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`
2. Получение числа hello наблюдения за день`SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`
3. Получить уровней hello в категориальный столбец  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. Получить hello количество уровней в сочетании с двумя категориальные столбцы`SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`
5. Получить hello распространения для числовых столбцов.  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. Извлечение записей из двух объединенных таблиц
   
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

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a>Дополнительные сценарии запросов для сценариев данных о поездках такси
Примеры запросов, которые являются определенной[NYC такси обработки данных](http://chriswhong.com/open-data/foil_nyc_taxi/) сценарии также приведены в [репозитории GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts). Эти запросы уже есть указана схема данных и будут готовы toobe отправлен toorun.

