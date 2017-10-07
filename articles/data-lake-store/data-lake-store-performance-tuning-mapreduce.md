---
title: "aaaAzure данных Озера хранилища MapReduce производительности рекомендации по настройке | Документы Microsoft"
description: "Рекомендации по настройке производительности для MapReduce в Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: e21414a23530e65613c85156af0209c88ec54d2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-mapreduce-on-hdinsight-and-azure-data-lake-store"></a>Рекомендации по настройке производительности для MapReduce в HDInsight и Azure Data Lake Store


## <a name="prerequisites"></a>Предварительные требования

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Учетная запись Azure Data Lake Store.** Инструкции о том, как один, см. в разделе toocreate [Приступая к работе с хранилища Озера данных Azure](data-lake-store-get-started-portal.md)
* **Кластер Azure HDInsight** с tooa доступа к учетной записи хранилища Озера данных. См. статью [Создание кластера HDInsight с Data Lake Store с помощью портала Azure](data-lake-store-hdinsight-hadoop-use-portal.md). Убедитесь, что включить удаленный рабочий стол для кластера hello.
* **Использование MapReduce в HDInsight**.  См. дополнительные сведения об [использовании MapReduce в Hadoop и HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-mapreduce)  
* **Рекомендации по настройке производительности в Azure Data Lake Store**.  См. [рекомендации по настройке производительности для Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance).  

## <a name="parameters"></a>Параметры

При выполнении задания MapReduce, вот наиболее важные параметры hello, можно настроить производительность tooincrease на ADLS.

* **MapReduce.map.Memory.MB** — hello объем памяти tooallocate tooeach сопоставления
* **MapReduce.Job.Maps** — hello число задач карты по заданиям
* **MapReduce.reduce.Memory.MB** — hello объем памяти tooallocate tooeach редуктора
* **MapReduce.Job.reduces** — hello число задач, сократите по заданиям

**MapReduce.map.Memory / Mapreduce.reduce.memory** это число следует настраивать с учетом на объем памяти, необходимой для карты hello, или уменьшите значение параметра задачи.  можно просмотреть значения по умолчанию Hello mapreduce.map.memory и mapreduce.reduce.memory в Ambari через конфигурацию Yarn hello.  В Ambari перейти tooYARN и открыть вкладку конфигураций hello.  Hello YARN памяти будет отображаться.  

**MapReduce.Job.Maps / Mapreduce.job.reduces** это определяет максимальное количество hello модули сопоставления или reducers toobe создан.  Hello число разбиений определит, сколько модули сопоставления, которые будут созданы для задания MapReduce hello.  Таким образом можно получить меньше модули сопоставления, чем запрошено, если существует меньше разбиений hello запрошенный модули сопоставления больше, чем.       

## <a name="guidance"></a>Руководство

**Шаг 1: Определение количество выполняемых заданий** -по умолчанию MapReduce будет использовать весь кластер hello для задания.  Можно использовать меньше hello кластера с помощью меньше модули сопоставления, чем число доступных контейнеров.  Hello рекомендации в этом документе предполагается, что приложение является hello только приложение, выполняющееся в кластере.      

**Шаг 2: Установка mapreduce.map.memory/mapreduce.reduce.memory** — hello размер памяти hello для карты и уменьшить задач будет зависеть от конкретного задания.  Можно уменьшить размер памяти hello, если требуется, чтобы tooincrease параллелизма.  Hello число параллельно выполняемых задач зависит от hello число контейнеров.  За счет уменьшения hello объем памяти на каждом сопоставления и редуктора, дополнительные контейнеры могут создаваться, которые поддерживают дополнительные модули сопоставления или reducers toorun одновременно.  Слишком много уменьшающегося hello объем памяти может привести к toorun некоторых процессов не хватает памяти.  Если при выполнении задания возникает ошибка кучи, следует увеличить hello объем памяти для сопоставления и редуктора.  При этом следует учитывать следующее. Добавление нескольких контейнеров ведет к увеличению нагрузки для каждого дополнительного контейнера, из-за которой может снизиться производительность.  Другой альтернативой является tooget больше памяти, используя кластер с высоким объемом памяти или увеличения hello количество узлов в кластере.  Больший объем памяти будет включить дополнительные контейнеры toobe используется, что означает более параллелизма.  

**Шаг 3: Определение памяти общее YARN** -tootune mapreduce.job.maps/mapreduce.job.reduces следует hello общее YARN доступный объем памяти для использования.  Эта информация доступна в Ambari.  Перейти tooYARN и открыть вкладку конфигураций hello.  в этом окне отображается Hello YARN памяти.  Следует умножьте hello YARN памяти с hello числа узлов в кластере tooget hello общее YARN памяти.

    Total YARN memory = nodes * YARN memory per node
Если вы используете пустой кластера, память может быть общая память YARN hello для кластера.  Если используются другими приложениями памяти, вы можете выбрать использование tooonly часть вашего кластера памяти за счет сокращения числа hello модули сопоставления или reducers toohello число контейнеров, которые должны toouse.  

**Шаг 4: Вычисление число контейнеров YARN** — контейнеры YARN определяют уровень hello параллельной обработки, доступных для задания hello.  Разделите общий объем памяти YARN на значение mapreduce.map.memory.  

    # of YARN containers = total YARN memory / mapreduce.map.memory

**Шаг 5: Установка mapreduce.job.maps/mapreduce.job.reduces** задать mapreduce.job.maps/mapreduce.job.reduces tooat наименьшее количество hello доступные контейнеры.  Можно поэкспериментировать дальнейших увеличив количество hello модули сопоставления и reducers toosee Если добиться более высокой производительности.  Имейте в виду, что большое число модулей сопоставления может увеличить нагрузку, что, в свою очередь, может привести к снижению производительности.  

Планирование ЦП и ЦП изоляции отключены по умолчанию, hello число контейнеров YARN ограничен объемом памяти.

## <a name="example-calculation"></a>Пример вычисления

Предположим, что в настоящее время имеется кластер, состоящий из 8 узлов D14 и требуется toorun задание большим объемом операций ввода-вывода.  Ниже приведены hello вычисления, которые нужно выполнить.

**Шаг 1: Определение количество выполняемых заданий** -в нашем примере мы предполагаем, что наши задания является hello только под управлением.  

**Шаг 2: Настройка mapreduce.map.memory/mapreduce.reduce.memory**. В нашем примере выполняется задание с большим объемом операций ввода-вывода. Следовательно, выделить 3 ГБ памяти для задач сопоставления будет достаточно.

    mapreduce.map.memory = 3GB
**Шаг 3. Определение общей памяти YARN**

    total memory from hello cluster is 8 nodes * 96GB of YARN memory for a D14 = 768GB
**Шаг 4. Расчет числа контейнеров YARN**

    # of YARN containers = 768GB of available memory / 3 GB of memory =   256

**Шаг 5. Установка mapreduce.job.maps/mapreduce.job.reduces**

    mapreduce.map.jobs = 256

## <a name="limitations"></a>Ограничения

**Регулирование Azure Data Lake Store**

Как мультитенантная служба, ADLS определяет ограничения пропускной способности на уровне учетной записи.  Если эти ограничения, сначала toosee неудачно завершившихся задач. Это можно определить, отслеживая ошибки регулирования в журналах задач.  Если для обработки задания требуется большая пропускная способность, свяжитесь с нами.   

toocheck, если вы начало регулируются, необходимо tooenable hello ведение журнала отладки на клиентской стороне hello. Вот как это сделать.

1. PUT hello следующие свойства в свойства log4j hello Ambari > YARN > настройки > Дополнительно yarn log4j: log4j.logger.com.microsoft.azure.datalake.store=DEBUG

2. Перезапустите все hello узлы или службы hello config tootake эффект.

3. Если вы начало регулируются, вы увидите код ошибки HTTP 429 hello в файле журнала YARN hello. файл журнала YARN Hello находится в /tmp/&lt;пользователя&gt;/yarn.log

## <a name="examples-toorun"></a>Примеры tooRun

toodemonstrate о том, как выполняется MapReduce в хранилище Озера данных Azure, ниже приведен пример кода, была запущена на кластере с hello следующие параметры:

* 16 узлов D14v2;
* кластер Hadoop под управлением HDI 3.6.

Для начальной точки Вот некоторые пример команды toorun MapReduce Teragen, Terasort и Teravalidate.  Эти команды можно настроить в соответствии с имеющимися ресурсами.

**Teragen**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 10000000000 adl://example/data/1TB-sort-input

**Terasort**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 -Dmapreduce.job.reduces=512 -Dmapreduce.reduce.memory.mb=3072 adl://example/data/1TB-sort-input adl://example/data/1TB-sort-output

**Teravalidate**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapreduce.job.maps=512 -Dmapreduce.map.memory.mb=3072 adl://example/data/1TB-sort-output adl://example/data/1TB-sort-validate
