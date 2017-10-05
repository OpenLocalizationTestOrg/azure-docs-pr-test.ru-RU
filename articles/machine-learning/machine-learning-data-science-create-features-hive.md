---
title: "Создание признаков для данных в кластере Hadoop с помощью запросов Hive | Документация Майкрософт"
description: "Примеры запросов Hive, формирующие характеристики в данных, хранящихся в кластере Azure HDInsight Hadoop."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8a94c71-979b-4707-b8fd-85b47d309a30
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: e027a6ffcb63868be13432870e484c5cbf2eef4b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-features-for-data-in-an-hadoop-cluster-using-hive-queries"></a><span data-ttu-id="44f55-103">Создание характеристик для данных в кластере Hadoop с помощью запросов Hive</span><span class="sxs-lookup"><span data-stu-id="44f55-103">Create features for data in an Hadoop cluster using Hive queries</span></span>
<span data-ttu-id="44f55-104">В этом документе показано, как создавать компоненты для данных, хранящихся в кластере Azure HDInsight Hadoop, используя запросы Hive.</span><span class="sxs-lookup"><span data-stu-id="44f55-104">This document shows how to create features for data stored in an Azure HDInsight Hadoop cluster using Hive queries.</span></span> <span data-ttu-id="44f55-105">Эти запросы Hive используют внедренные пользовательские функции, сценарии для которых предоставлены.</span><span class="sxs-lookup"><span data-stu-id="44f55-105">These Hive queries use embedded Hive User Defined Functions (UDFs), the scripts for which are provided.</span></span>

<span data-ttu-id="44f55-106">Операции, необходимые для создания функций, могут требовать большого объема памяти.</span><span class="sxs-lookup"><span data-stu-id="44f55-106">The operations needed to create features can be memory intensive.</span></span> <span data-ttu-id="44f55-107">В таких случаях производительность запросов Hive становится более значимой и может быть повышена за счет настройки определенных параметров.</span><span class="sxs-lookup"><span data-stu-id="44f55-107">The performance of Hive queries becomes more critical in such cases and can be improved by tuning certain parameters.</span></span> <span data-ttu-id="44f55-108">Эти параметры обсуждаются в последнем разделе.</span><span class="sxs-lookup"><span data-stu-id="44f55-108">The tuning of these parameters is discussed in the final section.</span></span>

<span data-ttu-id="44f55-109">Кроме того, в [репозитории GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) приведены примеры запросов, использующихся для сценариев наподобие [Данные о поездках в такси по Нью-Йорку](http://chriswhong.com/open-data/foil_nyc_taxi/).</span><span class="sxs-lookup"><span data-stu-id="44f55-109">Examples of the queries that are presented are specific to the [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="44f55-110">Для этих запросов уже задана схема данных, и они готовы к отправке и запуску.</span><span class="sxs-lookup"><span data-stu-id="44f55-110">These queries already have data schema specified and are ready to be submitted to run.</span></span> <span data-ttu-id="44f55-111">В последнем разделе также рассматриваются параметры, настроив которые можно повысить производительность запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="44f55-111">In the final section, parameters that users can tune so that the performance of Hive queries can be improved are  also discussed.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="44f55-112">Это **меню** содержит ссылки на статьи, описывающие создание характеристик для данных в различных средах.</span><span class="sxs-lookup"><span data-stu-id="44f55-112">This **menu** links to topics that describe how to create features for data in various environments.</span></span> <span data-ttu-id="44f55-113">Эта задача является одним из этапов [процесса обработки и анализа данных группы (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="44f55-113">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44f55-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="44f55-114">Prerequisites</span></span>
<span data-ttu-id="44f55-115">В этой статье предполагается, что вы:</span><span class="sxs-lookup"><span data-stu-id="44f55-115">This article assumes that you have:</span></span>

* <span data-ttu-id="44f55-116">Создали учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="44f55-116">Created an Azure storage account.</span></span> <span data-ttu-id="44f55-117">Инструкции см. в разделе [Создание учетной записи хранения](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="44f55-117">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="44f55-118">Подготовили настраиваемый кластер Hadoop с помощью службы HDInsight.</span><span class="sxs-lookup"><span data-stu-id="44f55-118">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span>  <span data-ttu-id="44f55-119">Инструкции см. в статье [Настройка кластеров Azure HDInsight Hadoop для процесса обработки и анализа данных группы](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="44f55-119">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="44f55-120">Отправили данные в таблицы Hive, которые находятся в кластерах Azure HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="44f55-120">The data has been uploaded to Hive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="44f55-121">Если данные не загружены, необходимо предварительно загрузить их в таблицы Hive, воспользовавшись инструкциями из раздела [Создание данных и их загрузка в таблицы Hive](machine-learning-data-science-move-hive-tables.md) .</span><span class="sxs-lookup"><span data-stu-id="44f55-121">If it has not, please follow [Create and load data to Hive tables](machine-learning-data-science-move-hive-tables.md) to upload data to Hive tables first.</span></span>
* <span data-ttu-id="44f55-122">Включили удаленный доступ к кластеру.</span><span class="sxs-lookup"><span data-stu-id="44f55-122">Enabled remote access to the cluster.</span></span> <span data-ttu-id="44f55-123">Инструкции можно найти в разделе [Доступ к головному узлу в кластере Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="44f55-123">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <span data-ttu-id="44f55-124"><a name="hive-featureengineering"></a>Создание функций</span><span class="sxs-lookup"><span data-stu-id="44f55-124"><a name="hive-featureengineering"></a>Feature Generation</span></span>
<span data-ttu-id="44f55-125">В этом разделе описано несколько примеров создания характеристик с помощью запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="44f55-125">In this section, several examples of the ways in which features can be generating using Hive queries are described.</span></span> <span data-ttu-id="44f55-126">После создания дополнительных признаков вы можете добавить их в виде столбцов к существующей таблице или создать новую таблицу с дополнительными возможностями и первичный ключ, который затем можно объединить с исходной таблицей.</span><span class="sxs-lookup"><span data-stu-id="44f55-126">Once you have generated additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, which can then be joined with the original table.</span></span> <span data-ttu-id="44f55-127">Здесь представлены следующие примеры.</span><span class="sxs-lookup"><span data-stu-id="44f55-127">Here are the examples presented:</span></span>

1. [<span data-ttu-id="44f55-128">Возможность создания функций на основе частоты</span><span class="sxs-lookup"><span data-stu-id="44f55-128">Frequency based Feature Generation</span></span>](#hive-frequencyfeature)
2. [<span data-ttu-id="44f55-129">Риски категориальных переменных в двоичной классификации</span><span class="sxs-lookup"><span data-stu-id="44f55-129">Risks of Categorical Variables in Binary Classification</span></span>](#hive-riskfeature)
3. [<span data-ttu-id="44f55-130">Извлечение признаков из полей даты и времени</span><span class="sxs-lookup"><span data-stu-id="44f55-130">Extract features from Datetime Field</span></span>](#hive-datefeatures)
4. [<span data-ttu-id="44f55-131">Извлечение признаков из текстовых полей</span><span class="sxs-lookup"><span data-stu-id="44f55-131">Extract features from Text Field</span></span>](#hive-textfeatures)
5. [<span data-ttu-id="44f55-132">Вычисления расстояния между координатами GPS</span><span class="sxs-lookup"><span data-stu-id="44f55-132">Calculate distance between GPS coordinates</span></span>](#hive-gpsdistance)

### <span data-ttu-id="44f55-133"><a name="hive-frequencyfeature"></a>Возможность создания функций на основе частоты</span><span class="sxs-lookup"><span data-stu-id="44f55-133"><a name="hive-frequencyfeature"></a>Frequency based Feature Generation</span></span>
<span data-ttu-id="44f55-134">Часто бывает полезным вычислить частоту уровней категориальной переменной или частоту сочетания уровней нескольких категориальных переменных.</span><span class="sxs-lookup"><span data-stu-id="44f55-134">It is often useful to calculate the frequencies of the levels of a categorical variable, or the frequencies of certain combinations of levels from multiple categorical variables.</span></span> <span data-ttu-id="44f55-135">Вот какой скрипт вы можете использовать для вычисления этих типов частоты.</span><span class="sxs-lookup"><span data-stu-id="44f55-135">Users can use the following script to calculate these frequencies:</span></span>

        select
            a.<column_name1>, a.<column_name2>, a.sub_count/sum(a.sub_count) over () as frequency
        from
        (
            select
                <column_name1>,<column_name2>, count(*) as sub_count
            from <databasename>.<tablename> group by <column_name1>, <column_name2>
        )a
        order by frequency desc;


### <span data-ttu-id="44f55-136"><a name="hive-riskfeature"></a>Риски категориальных переменных в двоичной классификации</span><span class="sxs-lookup"><span data-stu-id="44f55-136"><a name="hive-riskfeature"></a>Risks of Categorical Variables in Binary Classification</span></span>
<span data-ttu-id="44f55-137">В двоичной классификации нужно преобразовать нечисловые категориальные переменные в числовые функции, тогда как используемые модели принимают только числовые функции.</span><span class="sxs-lookup"><span data-stu-id="44f55-137">In binary classification, we need to convert non-numeric categorical variables into numeric features when the models being used only take numeric features.</span></span> <span data-ttu-id="44f55-138">Чтобы это сделать, нужно заменить каждый нечисловой уровень числовым риском.</span><span class="sxs-lookup"><span data-stu-id="44f55-138">This is done by replacing each non-numeric level with a numeric risk.</span></span> <span data-ttu-id="44f55-139">В этом разделе приведены некоторые общие запросы Hive, с помощью которых вы можете вычислить значения риска категориальной переменной.</span><span class="sxs-lookup"><span data-stu-id="44f55-139">In this section, we show some generic Hive queries that calculate the risk values (log odds) of a categorical variable.</span></span>

        set smooth_param1=1;
        set smooth_param2=20;
        select
            <column_name1>,<column_name2>,
            ln((sum_target+${hiveconf:smooth_param1})/(record_count-sum_target+${hiveconf:smooth_param2}-${hiveconf:smooth_param1})) as risk
        from
            (
            select
                <column_nam1>, <column_name2>, sum(binary_target) as sum_target, sum(1) as record_count
            from
                (
                select
                    <column_name1>, <column_name2>, if(target_column>0,1,0) as binary_target
                from <databasename>.<tablename>
                )a
            group by <column_name1>, <column_name2>
            )b

<span data-ttu-id="44f55-140">В этом примере переменные `smooth_param1` и `smooth_param2` задаются для сглаживания значений рисков, вычисленных на основе данных.</span><span class="sxs-lookup"><span data-stu-id="44f55-140">In this example, variables `smooth_param1` and `smooth_param2` are set to smooth the risk values calculated from the data.</span></span> <span data-ttu-id="44f55-141">Риски имеют диапазон от -Inf до Inf.</span><span class="sxs-lookup"><span data-stu-id="44f55-141">Risks have a range between -Inf and Inf.</span></span> <span data-ttu-id="44f55-142">Риск > 0 означает, что возможность того, что цель будет равной 1, превышает 0,5.</span><span class="sxs-lookup"><span data-stu-id="44f55-142">A risks > 0 indicates that the probability that the target is equal to 1 is greater than 0.5.</span></span>

<span data-ttu-id="44f55-143">После вычисления таблицы рисков риски можно назначить таблице, объединив ее с таблицей рисков.</span><span class="sxs-lookup"><span data-stu-id="44f55-143">After the risk table is calculated, users can assign risk values to a table by joining it with the risk table.</span></span> <span data-ttu-id="44f55-144">Запрос Hive на объединение предоставлен в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="44f55-144">The Hive joining query was provided in previous section.</span></span>

### <span data-ttu-id="44f55-145"><a name="hive-datefeatures"></a>Извлечение функций из полей даты и времени</span><span class="sxs-lookup"><span data-stu-id="44f55-145"><a name="hive-datefeatures"></a>Extract features from Datetime Fields</span></span>
<span data-ttu-id="44f55-146">Язык Hive включает в себя набор функций, определяемых пользователем, для обработки полей даты и времени.</span><span class="sxs-lookup"><span data-stu-id="44f55-146">Hive comes with a set of UDFs for processing datetime fields.</span></span> <span data-ttu-id="44f55-147">По умолчанию формат даты и времени в Hive выглядит так: yyyy-MM-dd 00:00:00 (например, 1970-01-01 12:21:32).</span><span class="sxs-lookup"><span data-stu-id="44f55-147">In Hive, the default datetime format is 'yyyy-MM-dd 00:00:00' ('1970-01-01 12:21:32' for example).</span></span> <span data-ttu-id="44f55-148">В этом разделе приведены примеры того, как из поля даты и времени извлекать день месяца и месяц, и другие примеры, в которых строка даты и времени в формате не по умолчанию преобразуется в строку в формате по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="44f55-148">In this section, we show examples that extract the day of a month, the month from a datetime field, and other examples that convert a datetime string in a format other than the default format to a datetime string in default format.</span></span>

        select day(<datetime field>), month(<datetime field>)
        from <databasename>.<tablename>;

<span data-ttu-id="44f55-149">В этом запросе Hive предполагается, что значение в поле *&#60;datetime field>* указано в стандартном формате даты и времени.</span><span class="sxs-lookup"><span data-stu-id="44f55-149">This Hive query assumes that the *&#60;datetime field>* is in the default datetime format.</span></span>

<span data-ttu-id="44f55-150">Если поле даты и времени приведено не в формате по умолчанию, нужно преобразовать его в метку времени Unix, а затем преобразовать метку времени в строку даты и времени в формате по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="44f55-150">If a datetime field is not in the default format, you need to convert the datetime field into Unix time stamp first, and then convert the Unix time stamp to a datetime string that is in the default format.</span></span> <span data-ttu-id="44f55-151">Когда дата и время указаны в формате по умолчанию, вы можете применять определяемые пользователями функции даты и времени для извлечения функций.</span><span class="sxs-lookup"><span data-stu-id="44f55-151">When the datetime is in default format, users can apply the embedded datetime UDFs to extract features.</span></span>

        select from_unixtime(unix_timestamp(<datetime field>,'<pattern of the datetime field>'))
        from <databasename>.<tablename>;

<span data-ttu-id="44f55-152">Если в этом запросе значение в поле *&#60;datetime field>* указано в формате *03/26/2015 12:04:39*, значение поля *'&#60;pattern of the datetime field>'* должно выглядеть так: `'MM/dd/yyyy HH:mm:ss'`.</span><span class="sxs-lookup"><span data-stu-id="44f55-152">In this query, if the *&#60;datetime field>* has the pattern like *03/26/2015 12:04:39*, the *'&#60;pattern of the datetime field>'* should be `'MM/dd/yyyy HH:mm:ss'`.</span></span> <span data-ttu-id="44f55-153">Чтобы проверить шаблон поля даты и времени, можно выполнить такую команду:</span><span class="sxs-lookup"><span data-stu-id="44f55-153">To test it, users can run</span></span>

        select from_unixtime(unix_timestamp('05/15/2015 09:32:10','MM/dd/yyyy HH:mm:ss'))
        from hivesampletable limit 1;

<span data-ttu-id="44f55-154">Компонент *hivesampletable* этого запроса по умолчанию предустановлен во всех подготовленных кластерах Azure HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="44f55-154">The *hivesampletable* in this query comes preinstalled on all Azure HDInsight Hadoop clusters by default when the clusters are provisioned.</span></span>

### <span data-ttu-id="44f55-155"><a name="hive-textfeatures"></a>Извлечение функций из текстовых полей</span><span class="sxs-lookup"><span data-stu-id="44f55-155"><a name="hive-textfeatures"></a>Extract features from Text Fields</span></span>
<span data-ttu-id="44f55-156">Если таблица Hive содержит текстовое поле, содержащее строку слов, разделенных пробелами, следующий запрос извлекает длину строки и число слов в строке.</span><span class="sxs-lookup"><span data-stu-id="44f55-156">When the Hive table has a text field that contains a string of words that are delimited by spaces, the following query extracts the length of the string, and the number of words in the string.</span></span>

        select length(<text field>) as str_len, size(split(<text field>,' ')) as word_num
        from <databasename>.<tablename>;

### <span data-ttu-id="44f55-157"><a name="hive-gpsdistance"></a>Вычисление расстояния между координатами GPS</span><span class="sxs-lookup"><span data-stu-id="44f55-157"><a name="hive-gpsdistance"></a>Calculate distances between sets of GPS coordinates</span></span>
<span data-ttu-id="44f55-158">Запрос, приведенный в этом разделе, вы можете напрямую применить к данным о поездках в такси в Нью-Йорке.</span><span class="sxs-lookup"><span data-stu-id="44f55-158">The query given in this section can be directly applied to the NYC Taxi Trip Data.</span></span> <span data-ttu-id="44f55-159">Цель этого запроса — продемонстрировать, как применить внедренные математические функции в Hive, чтобы создать признаки.</span><span class="sxs-lookup"><span data-stu-id="44f55-159">The purpose of this query is to show how to apply an embedded mathematical functions in Hive to generate features.</span></span>

<span data-ttu-id="44f55-160">Поля в этом запросе — это координаты GPS, обозначающие точки посадки и высадки пассажиров. Они называются так: *pickup\_longitude*, *pickup\_latitude*, *dropoff\_longitude* и *dropoff\_latitude*.</span><span class="sxs-lookup"><span data-stu-id="44f55-160">The fields that are used in this query are the GPS coordinates of pickup and dropoff locations, named *pickup\_longitude*, *pickup\_latitude*, *dropoff\_longitude*, and *dropoff\_latitude*.</span></span> <span data-ttu-id="44f55-161">Ниже приведены запросы, которые рассчитывают расстояние между координатами посадки и высадки.</span><span class="sxs-lookup"><span data-stu-id="44f55-161">The queries that calculate the direct distance between the pickup and dropoff coordinates are:</span></span>

        set R=3959;
        set pi=radians(180);
        select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude,
            ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
            *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
            *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
            /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
            +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
            pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
        from nyctaxi.trip
        where pickup_longitude between -90 and 0
        and pickup_latitude between 30 and 90
        and dropoff_longitude between -90 and 0
        and dropoff_latitude between 30 and 90
        limit 10;

<span data-ttu-id="44f55-162">Математические уравнения, с помощью которых рассчитывается расстояние между двумя координатами GPS, можно найти на сайте <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">Movable Type Scripts</a> (создатель веб-сайта — Петер Лапису (Peter Lapisu)).</span><span class="sxs-lookup"><span data-stu-id="44f55-162">The mathematical equations that calculate the distance between two GPS coordinates can be found on the <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">Movable Type Scripts</a> site, authored by Peter Lapisu.</span></span> <span data-ttu-id="44f55-163">В его коде JavaScript функция `toRad()` имеет значение *lat_or_lon*pi/180*, преобразующее градусы в радианы.</span><span class="sxs-lookup"><span data-stu-id="44f55-163">In his Javascript, the function `toRad()` is just *lat_or_lon*pi/180*, which converts degrees to radians.</span></span> <span data-ttu-id="44f55-164">Здесь *lat_or_lon* — это широта или долгота.</span><span class="sxs-lookup"><span data-stu-id="44f55-164">Here, *lat_or_lon* is the latitude or longitude.</span></span> <span data-ttu-id="44f55-165">Так как в Hive нет функции `atan2`, но есть функция `atan`, функция `atan2` в приведенном выше запросе Hive реализована функцией `atan` с помощью определения из <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank">Википедии</a>.</span><span class="sxs-lookup"><span data-stu-id="44f55-165">Since Hive does not provide the function `atan2`, but provides the function `atan`, the `atan2` function is implemented by `atan` function in the above Hive query using the definition provided in <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank">Wikipedia</a>.</span></span>

![Создание рабочей области](./media/machine-learning-data-science-create-features-hive/atan2new.png)

<span data-ttu-id="44f55-167">Полный список внедренных в Hive функций, определяемых пользователями, можно найти в разделе **Built-in Functions** (Встроенные функции) на <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">вики-сайте Apache Hive</a>.</span><span class="sxs-lookup"><span data-stu-id="44f55-167">A full list of Hive embedded UDFs can be found in the **Built-in Functions** section on the <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).</span></span>  

## <span data-ttu-id="44f55-168"><a name="tuning"></a> Дополнительный раздел: настройка параметров Hive для ускорения обработки запросов</span><span class="sxs-lookup"><span data-stu-id="44f55-168"><a name="tuning"></a> Advanced topics: Tune Hive Parameters to Improve Query Speed</span></span>
<span data-ttu-id="44f55-169">Настройки по умолчанию кластера Hive могут не подойти для запросов Hive и данных, обрабатываемых этими запросами.</span><span class="sxs-lookup"><span data-stu-id="44f55-169">The default parameter settings of Hive cluster might not be suitable for the Hive queries and the data that the queries are processing.</span></span> <span data-ttu-id="44f55-170">В этом разделе речь идет о некоторых параметрах, которые вы можете настраивать, чтобы улучшить производительность запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="44f55-170">In this section, we discuss some parameters that users can tune that improve the performance of Hive queries.</span></span> <span data-ttu-id="44f55-171">Сначала необходимо добавлять запросы настройки параметров, а затем запросы обработки данных.</span><span class="sxs-lookup"><span data-stu-id="44f55-171">Users need to add the parameter tuning queries before the queries of processing data.</span></span>

1. <span data-ttu-id="44f55-172">**Куча Java**: при работе с запросами на объединение крупных наборов данных или обработку длинных записей часто возникает ошибка, указывающая на то, что **в куче не хватает памяти**.</span><span class="sxs-lookup"><span data-stu-id="44f55-172">**Java heap space**: For queries involving joining large datasets, or processing long records, **running out of heap space** is one of the common error.</span></span> <span data-ttu-id="44f55-173">Чтобы устранить ее, задайте нужные значения для параметров *mapreduce.map.java.opts* и *mapreduce.task.io.sort.mb*.</span><span class="sxs-lookup"><span data-stu-id="44f55-173">This can be tuned by setting parameters *mapreduce.map.java.opts* and *mapreduce.task.io.sort.mb* to desired values.</span></span> <span data-ttu-id="44f55-174">Пример:</span><span class="sxs-lookup"><span data-stu-id="44f55-174">Here is an example:</span></span>
   
        set mapreduce.map.java.opts=-Xmx4096m;
        set mapreduce.task.io.sort.mb=-Xmx1024m;

    <span data-ttu-id="44f55-175">Этот параметр выделяет 4 ГБ памяти куче Java и, кроме того, выделяя на сортировку больший объем памяти, повышает эффективность сортировки.</span><span class="sxs-lookup"><span data-stu-id="44f55-175">This parameter allocates 4GB memory to Java heap space and also makes sorting more efficient by allocating more memory for it.</span></span> <span data-ttu-id="44f55-176">Мы рекомендуем заняться настройкой того, сколько памяти куда выделяется, если произошли сбои задач, связанные с размером кучи.</span><span class="sxs-lookup"><span data-stu-id="44f55-176">It is a good idea to play with these allocations if there are any job failure errors related to heap space.</span></span>

1. <span data-ttu-id="44f55-177">**Размер блока DFS** : этот параметр задает минимальную единицу измерения данных файловой системы.</span><span class="sxs-lookup"><span data-stu-id="44f55-177">**DFS block size** : This parameter sets the smallest unit of data that the file system stores.</span></span> <span data-ttu-id="44f55-178">Например, если размер блока DFS составляет 128 МБ, тогда любые данные размером не более 128 МБ хранятся в одном блоке, тогда как для данных размером более 128 МБ выделяется несколько блоков.</span><span class="sxs-lookup"><span data-stu-id="44f55-178">As an example, if the DFS block size is 128MB, then any data of size less than and up to 128MB is stored in a single block, while data that is larger than 128MB is allotted extra blocks.</span></span> <span data-ttu-id="44f55-179">Очень маленький размер блока может привести к тому, что в Hadoop будет задействовано много служебных данных, так как узлу имени, чтобы найти блок, соответствующий файлу, придется обрабатывать гораздо больше запросов.</span><span class="sxs-lookup"><span data-stu-id="44f55-179">Choosing a very small block size causes large overheads in Hadoop since the name node has to process many more requests to find the relevant block pertaining to the file.</span></span> <span data-ttu-id="44f55-180">При работе с гигабайтами (или большими объемами) данных рекомендуем такую настройку:</span><span class="sxs-lookup"><span data-stu-id="44f55-180">A recommended setting when dealing with gigabytes (or larger) data is :</span></span>
   
        set dfs.block.size=128m;
2. <span data-ttu-id="44f55-181">**Оптимизация операций объединения в Hive** : так как операции объединения на платформе Map/Reduce обычно выполняются на этапе сокращения, в некоторых случаях эффективность этих операций можно существенно повысить, запланировав объединения на этапе сопоставления (они также называются «объединениями при сопоставлении»).</span><span class="sxs-lookup"><span data-stu-id="44f55-181">**Optimizing join operation in Hive** : While join operations in the map/reduce framework typically take place in the reduce phase, sometimes, enormous gains can be achieved by scheduling joins in the map phase (also called "mapjoins").</span></span> <span data-ttu-id="44f55-182">Чтобы объединение в Hive выполнялось всегда по мере возможности, можно задать следующую настройку:</span><span class="sxs-lookup"><span data-stu-id="44f55-182">To direct Hive to do this whenever possible, we can set :</span></span>
   
        set hive.auto.convert.join=true;
3. <span data-ttu-id="44f55-183">**Определение количества модулей сопоставления в Hive** : хотя Hadoop позволяет задать число модулей сокращения, число модулей сопоставления, как правило, задать нельзя.</span><span class="sxs-lookup"><span data-stu-id="44f55-183">**Specifying the number of mappers to Hive** : While Hadoop allows the user to set the number of reducers, the number of mappers is typically not be set by the user.</span></span> <span data-ttu-id="44f55-184">Этим числом можно в некоторой степени управлять, задав значения переменных Hadoop *mapred.min.split.size* и *mapred.max.split.size*, так как размер каждой задачи сопоставления определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="44f55-184">A trick that allows some degree of control on this number is to choose the Hadoop variables, *mapred.min.split.size* and *mapred.max.split.size* as the size of each map task is determined by :</span></span>
   
        num_maps = max(mapred.min.split.size, min(mapred.max.split.size, dfs.block.size))
   
    <span data-ttu-id="44f55-185">Как правило, значение по умолчанию для *mapred.min.split.size* равно 0, для *mapred.max.split.size* — **Long.MAX** и для *dfs.block.size* — 64 МБ.</span><span class="sxs-lookup"><span data-stu-id="44f55-185">Typically, the default value of *mapred.min.split.size* is 0, that of *mapred.max.split.size* is **Long.MAX** and that of *dfs.block.size* is 64MB.</span></span> <span data-ttu-id="44f55-186">Как видно из размера данных, настройка этих параметров позволяет изменять количество используемых модулей сопоставления.</span><span class="sxs-lookup"><span data-stu-id="44f55-186">As we can see, given the data size, tuning these parameters by "setting" them allows us to tune the number of mappers used.</span></span>
4. <span data-ttu-id="44f55-187">Ниже приведены некоторые другие **дополнительные возможности** по оптимизации производительности Hive.</span><span class="sxs-lookup"><span data-stu-id="44f55-187">A few other more **advanced options** for optimizing Hive performance are mentioned below.</span></span> <span data-ttu-id="44f55-188">Они позволяют указывать объем памяти, выделяемой на сопоставление и уменьшение задач. Кроме того, с их помощью вы можете изменять производительность.</span><span class="sxs-lookup"><span data-stu-id="44f55-188">These allow you to set the memory allocated to map and reduce tasks, and can be useful in tweaking performance.</span></span> <span data-ttu-id="44f55-189">Не забывайте, что значение *mapreduce.reduce.memory.mb* не может превышать объем физической памяти каждого рабочего узла в кластере Hadoop.</span><span class="sxs-lookup"><span data-stu-id="44f55-189">Please keep in mind that the *mapreduce.reduce.memory.mb* cannot be greater than the physical memory size of each worker node in the Hadoop cluster.</span></span>
   
        set mapreduce.map.memory.mb = 2048;
        set mapreduce.reduce.memory.mb=6144;
        set mapreduce.reduce.java.opts=-Xmx8192m;
        set mapred.reduce.tasks=128;
        set mapred.tasktracker.reduce.tasks.maximum=128;

