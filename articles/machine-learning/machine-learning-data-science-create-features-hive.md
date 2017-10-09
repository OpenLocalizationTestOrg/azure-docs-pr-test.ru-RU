---
title: "функции aaaCreate для данных в кластер Hadoop, с помощью запросов Hive | Документы Microsoft"
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
ms.openlocfilehash: 686282bf0fb84ea82758d3c5b7de2bd90f0cf159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-an-hadoop-cluster-using-hive-queries"></a><span data-ttu-id="f801f-103">Создание характеристик для данных в кластере Hadoop с помощью запросов Hive</span><span class="sxs-lookup"><span data-stu-id="f801f-103">Create features for data in an Hadoop cluster using Hive queries</span></span>
<span data-ttu-id="f801f-104">В этом документе показано, как функции toocreate для данных, сохранить в кластер Azure HDInsight Hadoop, с помощью запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="f801f-104">This document shows how toocreate features for data stored in an Azure HDInsight Hadoop cluster using Hive queries.</span></span> <span data-ttu-id="f801f-105">Эти запросы Hive использовать внедренные Hive определяемых пользователем функций (UDFs), сценарии hello, для которого предоставляются.</span><span class="sxs-lookup"><span data-stu-id="f801f-105">These Hive queries use embedded Hive User Defined Functions (UDFs), hello scripts for which are provided.</span></span>

<span data-ttu-id="f801f-106">Hello требуемых операций toocreate функции могут быть большим объемом памяти.</span><span class="sxs-lookup"><span data-stu-id="f801f-106">hello operations needed toocreate features can be memory intensive.</span></span> <span data-ttu-id="f801f-107">производительность запросов Hive Hello возрастает в таких случаях и можно повысить путем настройки определенных параметров.</span><span class="sxs-lookup"><span data-stu-id="f801f-107">hello performance of Hive queries becomes more critical in such cases and can be improved by tuning certain parameters.</span></span> <span data-ttu-id="f801f-108">Hello помощник по настройке этих параметров рассматривается в последнем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="f801f-108">hello tuning of these parameters is discussed in hello final section.</span></span>

<span data-ttu-id="f801f-109">Hello запросы, которые представлены ниже приведены несколько конкретных toohello [NYC такси обработки данных](http://chriswhong.com/open-data/foil_nyc_taxi/) сценарии также приведены в [репозитории GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span><span class="sxs-lookup"><span data-stu-id="f801f-109">Examples of hello queries that are presented are specific toohello [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="f801f-110">Эти запросы уже есть указана схема данных и будут готовы toobe отправлен toorun.</span><span class="sxs-lookup"><span data-stu-id="f801f-110">These queries already have data schema specified and are ready toobe submitted toorun.</span></span> <span data-ttu-id="f801f-111">В последнем разделе hello также описаны параметры, которые пользователи могут настраивать, чтобы можно повысить производительность запросов Hive hello.</span><span class="sxs-lookup"><span data-stu-id="f801f-111">In hello final section, parameters that users can tune so that hello performance of Hive queries can be improved are  also discussed.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="f801f-112">Это **меню** связывает tootopics, описано, как toocreate функции для данных в различных средах.</span><span class="sxs-lookup"><span data-stu-id="f801f-112">This **menu** links tootopics that describe how toocreate features for data in various environments.</span></span> <span data-ttu-id="f801f-113">Эта задача является этапом hello [процесса обработки и анализа данных Team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="f801f-113">This task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f801f-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f801f-114">Prerequisites</span></span>
<span data-ttu-id="f801f-115">В этой статье предполагается, что вы:</span><span class="sxs-lookup"><span data-stu-id="f801f-115">This article assumes that you have:</span></span>

* <span data-ttu-id="f801f-116">Создали учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="f801f-116">Created an Azure storage account.</span></span> <span data-ttu-id="f801f-117">Инструкции см. в разделе [Создание учетной записи хранения](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="f801f-117">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="f801f-118">Подготовить настроенные кластеру с hello службы HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f801f-118">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span>  <span data-ttu-id="f801f-119">Инструкции см. в статье [Настройка кластеров Azure HDInsight Hadoop для процесса обработки и анализа данных группы](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="f801f-119">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="f801f-120">Hello данные были отправленного tooHive таблиц в Azure HDInsight Hadoop кластеров.</span><span class="sxs-lookup"><span data-stu-id="f801f-120">hello data has been uploaded tooHive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="f801f-121">Если нет, выполните [Создание и загрузка таблиц данных tooHive](machine-learning-data-science-move-hive-tables.md) tooHive tooupload данных сначала таблиц.</span><span class="sxs-lookup"><span data-stu-id="f801f-121">If it has not, please follow [Create and load data tooHive tables](machine-learning-data-science-move-hive-tables.md) tooupload data tooHive tables first.</span></span>
* <span data-ttu-id="f801f-122">Включить toohello кластера удаленного доступа.</span><span class="sxs-lookup"><span data-stu-id="f801f-122">Enabled remote access toohello cluster.</span></span> <span data-ttu-id="f801f-123">При необходимости инструкции в разделе [доступа hello головного узла кластера Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="f801f-123">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <span data-ttu-id="f801f-124"><a name="hive-featureengineering"></a>Создание функций</span><span class="sxs-lookup"><span data-stu-id="f801f-124"><a name="hive-featureengineering"></a>Feature Generation</span></span>
<span data-ttu-id="f801f-125">В этом разделе описаны некоторые примеры использования hello способами, в котором функции могут использоваться для создания использовании запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="f801f-125">In this section, several examples of hello ways in which features can be generating using Hive queries are described.</span></span> <span data-ttu-id="f801f-126">После того, как дополнительные функции, можно добавить их в качестве столбцов toohello существующую таблицу или создать новую таблицу с дополнительные функции hello и первичным ключом, который можно объединить с исходной таблицей hello.</span><span class="sxs-lookup"><span data-stu-id="f801f-126">Once you have generated additional features, you can either add them as columns toohello existing table or create a new table with hello additional features and primary key, which can then be joined with hello original table.</span></span> <span data-ttu-id="f801f-127">Ниже приведены примеры hello.</span><span class="sxs-lookup"><span data-stu-id="f801f-127">Here are hello examples presented:</span></span>

1. [<span data-ttu-id="f801f-128">Возможность создания функций на основе частоты</span><span class="sxs-lookup"><span data-stu-id="f801f-128">Frequency based Feature Generation</span></span>](#hive-frequencyfeature)
2. [<span data-ttu-id="f801f-129">Риски категориальных переменных в двоичной классификации</span><span class="sxs-lookup"><span data-stu-id="f801f-129">Risks of Categorical Variables in Binary Classification</span></span>](#hive-riskfeature)
3. [<span data-ttu-id="f801f-130">Извлечение признаков из полей даты и времени</span><span class="sxs-lookup"><span data-stu-id="f801f-130">Extract features from Datetime Field</span></span>](#hive-datefeatures)
4. [<span data-ttu-id="f801f-131">Извлечение признаков из текстовых полей</span><span class="sxs-lookup"><span data-stu-id="f801f-131">Extract features from Text Field</span></span>](#hive-textfeatures)
5. [<span data-ttu-id="f801f-132">Вычисления расстояния между координатами GPS</span><span class="sxs-lookup"><span data-stu-id="f801f-132">Calculate distance between GPS coordinates</span></span>](#hive-gpsdistance)

### <span data-ttu-id="f801f-133"><a name="hive-frequencyfeature"></a>Возможность создания функций на основе частоты</span><span class="sxs-lookup"><span data-stu-id="f801f-133"><a name="hive-frequencyfeature"></a>Frequency based Feature Generation</span></span>
<span data-ttu-id="f801f-134">Часто бывает полезным toocalculate частоты hello hello уровни категориальной переменной, или частоты hello определенные комбинации уровней — от нескольких категориальные переменные.</span><span class="sxs-lookup"><span data-stu-id="f801f-134">It is often useful toocalculate hello frequencies of hello levels of a categorical variable, or hello frequencies of certain combinations of levels from multiple categorical variables.</span></span> <span data-ttu-id="f801f-135">Пользователи могут использовать эти частот hello, выполнив сценарий toocalculate:</span><span class="sxs-lookup"><span data-stu-id="f801f-135">Users can use hello following script toocalculate these frequencies:</span></span>

        select
            a.<column_name1>, a.<column_name2>, a.sub_count/sum(a.sub_count) over () as frequency
        from
        (
            select
                <column_name1>,<column_name2>, count(*) as sub_count
            from <databasename>.<tablename> group by <column_name1>, <column_name2>
        )a
        order by frequency desc;


### <span data-ttu-id="f801f-136"><a name="hive-riskfeature"></a>Риски категориальных переменных в двоичной классификации</span><span class="sxs-lookup"><span data-stu-id="f801f-136"><a name="hive-riskfeature"></a>Risks of Categorical Variables in Binary Classification</span></span>
<span data-ttu-id="f801f-137">В двоичной классификации нам нужна tooconvert нечисловые категориальные переменные в числовые признаки, когда hello модели используется только числовые функции.</span><span class="sxs-lookup"><span data-stu-id="f801f-137">In binary classification, we need tooconvert non-numeric categorical variables into numeric features when hello models being used only take numeric features.</span></span> <span data-ttu-id="f801f-138">Чтобы это сделать, нужно заменить каждый нечисловой уровень числовым риском.</span><span class="sxs-lookup"><span data-stu-id="f801f-138">This is done by replacing each non-numeric level with a numeric risk.</span></span> <span data-ttu-id="f801f-139">В этом разделе демонстрируется некоторые универсальные запросов Hive, которые вычисляют значения риск hello (вероятность журнала) категориальные переменной.</span><span class="sxs-lookup"><span data-stu-id="f801f-139">In this section, we show some generic Hive queries that calculate hello risk values (log odds) of a categorical variable.</span></span>

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

<span data-ttu-id="f801f-140">В этом примере переменные `smooth_param1` и `smooth_param2` toosmooth hello риск значения вычисляются на основе данных hello.</span><span class="sxs-lookup"><span data-stu-id="f801f-140">In this example, variables `smooth_param1` and `smooth_param2` are set toosmooth hello risk values calculated from hello data.</span></span> <span data-ttu-id="f801f-141">Риски имеют диапазон от -Inf до Inf.</span><span class="sxs-lookup"><span data-stu-id="f801f-141">Risks have a range between -Inf and Inf.</span></span> <span data-ttu-id="f801f-142">Риски > 0 указывает на hello вероятность того, что что hello целевой сервер равно too1 больше 0,5.</span><span class="sxs-lookup"><span data-stu-id="f801f-142">A risks > 0 indicates that hello probability that hello target is equal too1 is greater than 0.5.</span></span>

<span data-ttu-id="f801f-143">После расчета таблицы риск hello, пользователи могут назначать таблица tooa значений риска, присоединив ее с таблицей риск hello.</span><span class="sxs-lookup"><span data-stu-id="f801f-143">After hello risk table is calculated, users can assign risk values tooa table by joining it with hello risk table.</span></span> <span data-ttu-id="f801f-144">присоединяемый запроса Hive Hello был представлен в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="f801f-144">hello Hive joining query was provided in previous section.</span></span>

### <span data-ttu-id="f801f-145"><a name="hive-datefeatures"></a>Извлечение функций из полей даты и времени</span><span class="sxs-lookup"><span data-stu-id="f801f-145"><a name="hive-datefeatures"></a>Extract features from Datetime Fields</span></span>
<span data-ttu-id="f801f-146">Язык Hive включает в себя набор функций, определяемых пользователем, для обработки полей даты и времени.</span><span class="sxs-lookup"><span data-stu-id="f801f-146">Hive comes with a set of UDFs for processing datetime fields.</span></span> <span data-ttu-id="f801f-147">В кусте, формат даты и времени по умолчанию hello является "гггг мм дд 00:00:00" ("1970-01-01 12:21:32" пример).</span><span class="sxs-lookup"><span data-stu-id="f801f-147">In Hive, hello default datetime format is 'yyyy-MM-dd 00:00:00' ('1970-01-01 12:21:32' for example).</span></span> <span data-ttu-id="f801f-148">В этом разделе показано, примеры, извлечь hello день месяца, hello месяца из поля даты и времени и другие примеры, преобразующие Строка даты и времени в формате, отличного от Строка даты и времени tooa формата по умолчанию hello в используемом по умолчанию форматирование.</span><span class="sxs-lookup"><span data-stu-id="f801f-148">In this section, we show examples that extract hello day of a month, hello month from a datetime field, and other examples that convert a datetime string in a format other than hello default format tooa datetime string in default format.</span></span>

        select day(<datetime field>), month(<datetime field>)
        from <databasename>.<tablename>;

<span data-ttu-id="f801f-149">Hive в запросе предполагается, что hello *&#60; поля datetime >* в формате даты и времени по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="f801f-149">This Hive query assumes that hello *&#60;datetime field>* is in hello default datetime format.</span></span>

<span data-ttu-id="f801f-150">Если поля datetime не в формате по умолчанию hello, необходимые поля даты и времени tooconvert hello в отметку времени Unix сначала, а затем время Unix hello преобразования, Строка даты tooa и отметки времени, которая по умолчанию hello формата.</span><span class="sxs-lookup"><span data-stu-id="f801f-150">If a datetime field is not in hello default format, you need tooconvert hello datetime field into Unix time stamp first, and then convert hello Unix time stamp tooa datetime string that is in hello default format.</span></span> <span data-ttu-id="f801f-151">Когда hello datetime в основной формат, пользователям можно применять hello внедренных datetime определяемых пользователем функций tooextract компоненты.</span><span class="sxs-lookup"><span data-stu-id="f801f-151">When hello datetime is in default format, users can apply hello embedded datetime UDFs tooextract features.</span></span>

        select from_unixtime(unix_timestamp(<datetime field>,'<pattern of hello datetime field>'))
        from <databasename>.<tablename>;

<span data-ttu-id="f801f-152">В этом запросе, если hello *&#60; поля даты и времени >* имеет шаблон hello like *03/26/2015 12:04:39*, hello *"&#60; шаблон поля datetime hello >"* должно быть `'MM/dd/yyyy HH:mm:ss'`.</span><span class="sxs-lookup"><span data-stu-id="f801f-152">In this query, if hello *&#60;datetime field>* has hello pattern like *03/26/2015 12:04:39*, hello *'&#60;pattern of hello datetime field>'* should be `'MM/dd/yyyy HH:mm:ss'`.</span></span> <span data-ttu-id="f801f-153">tootest, пользователи могут запускать</span><span class="sxs-lookup"><span data-stu-id="f801f-153">tootest it, users can run</span></span>

        select from_unixtime(unix_timestamp('05/15/2015 09:32:10','MM/dd/yyyy HH:mm:ss'))
        from hivesampletable limit 1;

<span data-ttu-id="f801f-154">Hello *hivesampletable* в этом запросе предустанавливается на всех кластеров Azure HDInsight Hadoop по умолчанию при инициализации hello кластеров.</span><span class="sxs-lookup"><span data-stu-id="f801f-154">hello *hivesampletable* in this query comes preinstalled on all Azure HDInsight Hadoop clusters by default when hello clusters are provisioned.</span></span>

### <span data-ttu-id="f801f-155"><a name="hive-textfeatures"></a>Извлечение функций из текстовых полей</span><span class="sxs-lookup"><span data-stu-id="f801f-155"><a name="hive-textfeatures"></a>Extract features from Text Fields</span></span>
<span data-ttu-id="f801f-156">Если hello Hive таблицы есть текстовое поле, содержащее строку слов, которые разделяются пробелами, hello следующий запрос извлекает длину hello строку hello и hello количество слов в строке приветствия.</span><span class="sxs-lookup"><span data-stu-id="f801f-156">When hello Hive table has a text field that contains a string of words that are delimited by spaces, hello following query extracts hello length of hello string, and hello number of words in hello string.</span></span>

        select length(<text field>) as str_len, size(split(<text field>,' ')) as word_num
        from <databasename>.<tablename>;

### <span data-ttu-id="f801f-157"><a name="hive-gpsdistance"></a>Вычисление расстояния между координатами GPS</span><span class="sxs-lookup"><span data-stu-id="f801f-157"><a name="hive-gpsdistance"></a>Calculate distances between sets of GPS coordinates</span></span>
<span data-ttu-id="f801f-158">Hello запроса, приведенные в этом разделе можно непосредственно примененных toohello NYC такси обработки данных.</span><span class="sxs-lookup"><span data-stu-id="f801f-158">hello query given in this section can be directly applied toohello NYC Taxi Trip Data.</span></span> <span data-ttu-id="f801f-159">Hello этот запрос предназначен tooshow как встроенный tooapply математические функции в функции toogenerate Hive.</span><span class="sxs-lookup"><span data-stu-id="f801f-159">hello purpose of this query is tooshow how tooapply an embedded mathematical functions in Hive toogenerate features.</span></span>

<span data-ttu-id="f801f-160">Hello поля, используемые в этом запросе, координаты GPS hello раскладки и dropoff расположения с именем *раскладки\_долготы*, *раскладки\_широты*,  *dropoff\_долготы*, и *dropoff\_широты*.</span><span class="sxs-lookup"><span data-stu-id="f801f-160">hello fields that are used in this query are hello GPS coordinates of pickup and dropoff locations, named *pickup\_longitude*, *pickup\_latitude*, *dropoff\_longitude*, and *dropoff\_latitude*.</span></span> <span data-ttu-id="f801f-161">Hello запросы, которые вычисляют hello прямой расстояние между hello координаты раскладки и dropoff являются:</span><span class="sxs-lookup"><span data-stu-id="f801f-161">hello queries that calculate hello direct distance between hello pickup and dropoff coordinates are:</span></span>

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

<span data-ttu-id="f801f-162">Hello математических формул, которые вычисляют hello расстояние между двумя Координаты GPS можно найти на hello <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">сценарии тип доступные</a> сайтов, созданных Питер Lapisu.</span><span class="sxs-lookup"><span data-stu-id="f801f-162">hello mathematical equations that calculate hello distance between two GPS coordinates can be found on hello <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">Movable Type Scripts</a> site, authored by Peter Lapisu.</span></span> <span data-ttu-id="f801f-163">В его Javascript hello функция `toRad()` только *lat_or_lon*pi/180 *, который преобразует tooradians градусов.</span><span class="sxs-lookup"><span data-stu-id="f801f-163">In his Javascript, hello function `toRad()` is just *lat_or_lon*pi/180*, which converts degrees tooradians.</span></span> <span data-ttu-id="f801f-164">Здесь *lat_or_lon* — hello Широта и долгота.</span><span class="sxs-lookup"><span data-stu-id="f801f-164">Here, *lat_or_lon* is hello latitude or longitude.</span></span> <span data-ttu-id="f801f-165">Поскольку куст обеспечивают функции hello `atan2`, но предоставляет функции hello `atan`, hello `atan2` реализуется функция `atan` функции hello выше запрос Hive, с использованием определения hello в <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank"> Википедии</a>.</span><span class="sxs-lookup"><span data-stu-id="f801f-165">Since Hive does not provide hello function `atan2`, but provides hello function `atan`, hello `atan2` function is implemented by `atan` function in hello above Hive query using hello definition provided in <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank">Wikipedia</a>.</span></span>

![Создание рабочей области](./media/machine-learning-data-science-create-features-hive/atan2new.png)

<span data-ttu-id="f801f-167">Полный список внедренных определяемые пользователем функции можно найти в hello куста **встроенные функции** раздела, посвященного hello <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive вики-сайте</a>).</span><span class="sxs-lookup"><span data-stu-id="f801f-167">A full list of Hive embedded UDFs can be found in hello **Built-in Functions** section on hello <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).</span></span>  

## <span data-ttu-id="f801f-168"><a name="tuning"></a>Дополнительные разделы: Настройка параметров Hive tooImprove скорость обработки запросов</span><span class="sxs-lookup"><span data-stu-id="f801f-168"><a name="tuning"></a> Advanced topics: Tune Hive Parameters tooImprove Query Speed</span></span>
<span data-ttu-id="f801f-169">Здравствуйте, параметр по умолчанию параметры Hive кластера может быть подходит для запросов Hive hello и hello данных, которые обрабатывают запросы hello.</span><span class="sxs-lookup"><span data-stu-id="f801f-169">hello default parameter settings of Hive cluster might not be suitable for hello Hive queries and hello data that hello queries are processing.</span></span> <span data-ttu-id="f801f-170">В этом разделе мы рассмотрим некоторые параметры, которые пользователи могут настраивать, повышающие производительность hello запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="f801f-170">In this section, we discuss some parameters that users can tune that improve hello performance of Hive queries.</span></span> <span data-ttu-id="f801f-171">Пользователи должны tooadd hello параметр настройки запросов перед hello запросы обработки данных.</span><span class="sxs-lookup"><span data-stu-id="f801f-171">Users need tooadd hello parameter tuning queries before hello queries of processing data.</span></span>

1. <span data-ttu-id="f801f-172">**Размер кучи Java**: для запросов, включающих соединение больших наборов данных или обработки длинных записях **хватает размера кучи** является одной из распространенных ошибок hello.</span><span class="sxs-lookup"><span data-stu-id="f801f-172">**Java heap space**: For queries involving joining large datasets, or processing long records, **running out of heap space** is one of hello common error.</span></span> <span data-ttu-id="f801f-173">Это можно настроить, задав параметры *mapreduce.map.java.opts* и *mapreduce.task.io.sort.mb* toodesired значения.</span><span class="sxs-lookup"><span data-stu-id="f801f-173">This can be tuned by setting parameters *mapreduce.map.java.opts* and *mapreduce.task.io.sort.mb* toodesired values.</span></span> <span data-ttu-id="f801f-174">Пример:</span><span class="sxs-lookup"><span data-stu-id="f801f-174">Here is an example:</span></span>
   
        set mapreduce.map.java.opts=-Xmx4096m;
        set mapreduce.task.io.sort.mb=-Xmx1024m;

    <span data-ttu-id="f801f-175">Этот параметр выделяет пространства кучи tooJava 4 ГБ памяти, а также делает сортировки более эффективно, выделив дополнительную память для него.</span><span class="sxs-lookup"><span data-stu-id="f801f-175">This parameter allocates 4GB memory tooJava heap space and also makes sorting more efficient by allocating more memory for it.</span></span> <span data-ttu-id="f801f-176">Это разумно tooplay с выделение памяти при наличии пробелов связанные tooheap ошибки сбоя задания.</span><span class="sxs-lookup"><span data-stu-id="f801f-176">It is a good idea tooplay with these allocations if there are any job failure errors related tooheap space.</span></span>

1. <span data-ttu-id="f801f-177">**Размер блока DFS** : этот параметр задает hello наименьшая единица данных, hello хранилища системных файлов.</span><span class="sxs-lookup"><span data-stu-id="f801f-177">**DFS block size** : This parameter sets hello smallest unit of data that hello file system stores.</span></span> <span data-ttu-id="f801f-178">Например если размер блока DFS hello составляет 128 МБ то любые данные, размер вверх too128MB и меньше, чем сохраняется в одном блоке, при данных, больше, чем 128 МБ будет выделено дополнительное блоки.</span><span class="sxs-lookup"><span data-stu-id="f801f-178">As an example, if hello DFS block size is 128MB, then any data of size less than and up too128MB is stored in a single block, while data that is larger than 128MB is allotted extra blocks.</span></span> <span data-ttu-id="f801f-179">Выбор размера очень небольшой блок вызывает большие накладные расходы в Hadoop, так как узел с именем hello tooprocess многие дополнительные запросы toofind hello соответствующего блока относится файл toohello.</span><span class="sxs-lookup"><span data-stu-id="f801f-179">Choosing a very small block size causes large overheads in Hadoop since hello name node has tooprocess many more requests toofind hello relevant block pertaining toohello file.</span></span> <span data-ttu-id="f801f-180">При работе с гигабайтами (или большими объемами) данных рекомендуем такую настройку:</span><span class="sxs-lookup"><span data-stu-id="f801f-180">A recommended setting when dealing with gigabytes (or larger) data is :</span></span>
   
        set dfs.block.size=128m;
2. <span data-ttu-id="f801f-181">**Оптимизация операции соединения в кусте** : во время операции объединения в framework сопоставления и сокращения hello, обычно выполняются в hello уменьшить этап, иногда, огромным увеличится, запланировав соединения в этапе сопоставления hello (также называется «mapjoins»).</span><span class="sxs-lookup"><span data-stu-id="f801f-181">**Optimizing join operation in Hive** : While join operations in hello map/reduce framework typically take place in hello reduce phase, sometimes, enormous gains can be achieved by scheduling joins in hello map phase (also called "mapjoins").</span></span> <span data-ttu-id="f801f-182">toodirect куста toodo, это когда это возможно, можно выбрать вариант:</span><span class="sxs-lookup"><span data-stu-id="f801f-182">toodirect Hive toodo this whenever possible, we can set :</span></span>
   
        set hive.auto.convert.join=true;
3. <span data-ttu-id="f801f-183">**Указание числа hello модули сопоставления tooHive** : во время Hadoop позволяет hello пользователя tooset hello число reducers, обычно является число hello модули сопоставления не задается пользователем hello.</span><span class="sxs-lookup"><span data-stu-id="f801f-183">**Specifying hello number of mappers tooHive** : While Hadoop allows hello user tooset hello number of reducers, hello number of mappers is typically not be set by hello user.</span></span> <span data-ttu-id="f801f-184">Прием, обеспечивает определенную степень управления на этот номер является toochoose hello Hadoop переменные, *mapred.min.split.size* и *mapred.max.split.size* как hello размер каждой карты определяется задач:</span><span class="sxs-lookup"><span data-stu-id="f801f-184">A trick that allows some degree of control on this number is toochoose hello Hadoop variables, *mapred.min.split.size* and *mapred.max.split.size* as hello size of each map task is determined by :</span></span>
   
        num_maps = max(mapred.min.split.size, min(mapred.max.split.size, dfs.block.size))
   
    <span data-ttu-id="f801f-185">Здравствуйте, как правило, значение по умолчанию *mapred.min.split.size* равно 0, что *mapred.max.split.size* — **Long.MAX** , а *dfs.block.size* составляет 64 МБ.</span><span class="sxs-lookup"><span data-stu-id="f801f-185">Typically, hello default value of *mapred.min.split.size* is 0, that of *mapred.max.split.size* is **Long.MAX** and that of *dfs.block.size* is 64MB.</span></span> <span data-ttu-id="f801f-186">Как видите, размер данных заданного hello, помощник по настройке этих параметров следует «Подготовка» их мы сможем tootune hello число использовать модули сопоставления.</span><span class="sxs-lookup"><span data-stu-id="f801f-186">As we can see, given hello data size, tuning these parameters by "setting" them allows us tootune hello number of mappers used.</span></span>
4. <span data-ttu-id="f801f-187">Ниже приведены некоторые другие **дополнительные возможности** по оптимизации производительности Hive.</span><span class="sxs-lookup"><span data-stu-id="f801f-187">A few other more **advanced options** for optimizing Hive performance are mentioned below.</span></span> <span data-ttu-id="f801f-188">Эти возможности toomap памяти, выделенной tooset hello и сокращать задачи и можно использовать в настройке производительности.</span><span class="sxs-lookup"><span data-stu-id="f801f-188">These allow you tooset hello memory allocated toomap and reduce tasks, and can be useful in tweaking performance.</span></span> <span data-ttu-id="f801f-189">Следует помнить, hello *mapreduce.reduce.memory.mb* не может превышать размер физической памяти hello каждый рабочий узел в кластере Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="f801f-189">Please keep in mind that hello *mapreduce.reduce.memory.mb* cannot be greater than hello physical memory size of each worker node in hello Hadoop cluster.</span></span>
   
        set mapreduce.map.memory.mb = 2048;
        set mapreduce.reduce.memory.mb=6144;
        set mapreduce.reduce.java.opts=-Xmx8192m;
        set mapred.reduce.tasks=128;
        set mapred.tasktracker.reduce.tasks.maximum=128;

