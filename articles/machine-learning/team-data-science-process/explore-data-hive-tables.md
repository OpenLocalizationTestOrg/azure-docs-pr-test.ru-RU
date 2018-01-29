---
title: "Просмотр данных в таблицах Hive с помощью запросов Hive | Документация Майкрософт"
description: "Просмотр данных в таблицах Hive с помощью запросов Hive."
services: machine-learning
documentationcenter: 
author: bradsev
manager: cgronlun
editor: cgronlun
ms.assetid: 0d46cea5-2b4c-4384-9bfa-fa20f6f75148
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/09/2017
ms.author: bradsev
ms.openlocfilehash: 9cf205abcf9782ceac4d9ac5a920e136b69c57b6
ms.sourcegitcommit: bc8d39fa83b3c4a66457fba007d215bccd8be985
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2017
---
# <a name="explore-data-in-hive-tables-with-hive-queries"></a>Просмотр данных в таблицах Hive с помощью запросов Hive
В этом документе представлено несколько примеров сценариев Hive, которые используются для анализа данных в таблицах Hive в кластере HDInsight Hadoop.

Следующее **меню** содержит ссылки на статьи, описывающие использование средств для просмотра данных из различных сред хранения.

[!INCLUDE [cap-explore-data-selector](../../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается, что вы:

* Создали учетную запись хранения Azure. Инструкции см. в разделе [Создание учетной записи хранения](../../storage/common/storage-create-storage-account.md#create-a-storage-account).
* Подготовили настраиваемый кластер Hadoop с помощью службы HDInsight. Инструкции см. в статье [Настройка кластеров Azure HDInsight Hadoop для процесса обработки и анализа данных группы](customize-hadoop-cluster.md).
* Отправили данные в таблицы Hive, которые находятся в кластерах Azure HDInsight Hadoop. Если данные не загружены, необходимо предварительно загрузить их в таблицы Hive, воспользовавшись инструкциями из статьи [Создание и загрузка данных в таблицы Hive из хранилища больших двоичных объектов Azure](move-hive-tables.md) .
* Включили удаленный доступ к кластеру. Инструкции можно найти в разделе [Доступ к головному узлу в кластере Hadoop](customize-hadoop-cluster.md).
* Инструкции по отправке запросов Hive см. в разделе [Отправка запросов Hive](move-hive-tables.md#submit).

## <a name="example-hive-query-scripts-for-data-exploration"></a>Пример сценариев запроса Hive для просмотра данных
1. Узнайте количество наблюдений на раздел `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`
2. Узнайте количество наблюдений в день `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`
3. Получение уровней в столбце категорий   
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. Узнайте число уровней в сочетании двух столбцов категорий `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`
5. Получение распределения для числовых столбцов   
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
Кроме того, в [репозитории GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) приведены примеры запросов, которые используются для сценариев наподобие [Данные о поездках в такси по Нью-Йорку](http://chriswhong.com/open-data/foil_nyc_taxi/). Для этих запросов уже задана схема данных, и они готовы к отправке и запуску.

