---
title: "aaaAzure данных Озера хранилища Hive производительности рекомендации по настройке | Документы Microsoft"
description: "Рекомендации по настройке производительности Hive в Azure Data Lake Store"
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
ms.openlocfilehash: e44daeb6ad3b64e893c709df63b56444a330729f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-hive-on-hdinsight-and-azure-data-lake-store"></a>Рекомендации по настройке производительности Hive в HDInsight и Azure Data Lake Store

параметры по умолчанию Hello были заданы tooprovide хорошую производительность для многих различных вариантов использования.  Для запросов, большим объемом операций ввода-вывода куст может быть настраиваемой tooget более высокую производительность с ADLS.  

## <a name="prerequisites"></a>Предварительные требования

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Учетная запись Azure Data Lake Store.** Инструкции о том, как один, см. в разделе toocreate [Приступая к работе с хранилища Озера данных Azure](data-lake-store-get-started-portal.md)
* **Кластер Azure HDInsight** с tooa доступа к учетной записи хранилища Озера данных. См. статью [Создание кластера HDInsight с Data Lake Store с помощью портала Azure](data-lake-store-hdinsight-hadoop-use-portal.md). Убедитесь, что включить удаленный рабочий стол для кластера hello.
* **Запустите Hive в HDInsight**.  toolearn о выполнении задания Hive в HDInsight, в разделе [используйте Hive в HDInsight] (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)
* **Рекомендации по настройке производительности в Azure Data Lake Store**.  См. [рекомендации по настройке производительности для Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance).

## <a name="parameters"></a>Параметры

Ниже приведены параметры tootune hello для наиболее важных для повышения производительности ADLS.

* **Hive.tez.Container.Size** — hello объем памяти, используемой каждой задачи

* **tez.grouping.min-size** — минимальный размер каждого модуля сопоставления;

* **tez.grouping.max-size** — максимальный размер каждого модуля сопоставления;

* **hive.exec.reducer.bytes.per.reducer** — размер каждого модуля уменьшения.

**Hive.tez.Container.Size** -размер контейнера hello определяет объем памяти доступен для каждой задачи.  Это основной вход hello для управления параллелизмом hello в кусте.  

**размер tez.GROUPING.Min** — этот параметр позволяет tooset hello минимальный размер каждого сопоставления.  Если количество hello модули сопоставления, которые выбирает Tez меньше, чем значение этого параметра hello, Tez будет использовать заданное здесь значение hello.  

**размер tez.GROUPING.max** — параметр hello позволяет tooset hello максимальный размер каждого сопоставления.  Если количество hello модули сопоставления, которые выбирает Tez больше, чем значение этого параметра hello, Tez будет использовать заданное здесь значение hello.  

**Hive.Exec.reducer.Bytes.per.reducer** — этот параметр задает размер hello каждого редуктора.  По умолчанию используется размер 256 МБ.  

## <a name="guidance"></a>Руководство

**Задать hive.exec.reducer.bytes.per.reducer** — значение по умолчанию hello работает хорошо, когда hello данных без сжатия.  Для данных, сжимается необходимо уменьшить размер hello hello редуктора.  

**Задайте hive.tez.container.size** — объем памяти для каждого узла, который определяется параметром yarn.nodemanager.resource.memory-mb (должен быть правильно определен для кластера HDI по умолчанию).  Дополнительные сведения об установке соответствующих памяти hello в YARN разделе [учет](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom).

Интенсивных рабочих нагрузок ввода-вывода можно повысить степень параллелизма, уменьшив размер контейнера Tez hello. Это дает пользователю hello дополнительные контейнеры, которые, увеличивает параллелизм.  Но некоторые запросы Hive требуют значительного объема памяти (например, MapJoin).  Если задачу hello не имеет достаточно памяти, вы получите исключению нехватки памяти во время выполнения.  При получении исключений нехватки памяти, следует увеличить hello памяти.   

общий объем памяти YARN hello будут привязаны Hello числа параллельных задач, выполняющихся или параллелизма.  Hello число контейнеров YARN будет указывать, сколько параллельные задачи могут выполняться.  toofind hello YARN памяти на узел, вы можете перейти tooAmbari.  Перейти tooYARN и открыть вкладку конфигураций hello.  в этом окне отображается Hello YARN памяти.  

        Total YARN memory = nodes * YARN memory per node
        # of YARN containers = Total YARN memory / Tez container size
Hello ключа tooimproving производительности с помощью ADLS — максимальной степени параллелизма hello tooincrease.  Tez автоматически вычисляет hello число задач, которые должны быть созданы, поэтому нет необходимости tooset его.   

## <a name="example-calculation"></a>Пример вычисления

Предположим, что у вас есть кластер D14 с 8 узлами.  

    Total YARN memory = nodes * YARN memory per node
    Total YARN memory = 8 nodes * 96GB = 768GB
    # of YARN containers = 768GB / 3072MB = 256

## <a name="limitations"></a>Ограничения
**Регулирование Azure Data Lake Store** 

UIf попаданий hello ограничения пропускной способности, предоставляемых по ADLS, будет начинаться toosee неудачно завершившихся задач. Это можно заметить, отслеживая ошибки регулирования в журналах задач.  Hello параллелизма можно уменьшить путем увеличения размера контейнеров Tez.  Если для обработки задания требуется больший параллелизм, свяжитесь с нами.   

toocheck, если вы начало регулируются, необходимо tooenable hello ведение журнала отладки на клиентской стороне hello. Вот как это сделать.

1. Поместите следующие свойства в конфигурации куст свойства log4j hello hello. Это можно сделать из представления Ambari: log4j.logger.com.microsoft.azure.datalake.store=DEBUG перезапустите все hello узлов или службу hello config tootake эффект.

2. Если вы начало регулируются, вы увидите код ошибки HTTP 429 hello в файле журнала hive hello. файл журнала hive Hello находится в /tmp/&lt;пользователя&gt;/hive.log

## <a name="further-information-on-hive-tuning"></a>Дополнительные сведения о настройке Hive

Ниже приведены некоторые блоги, которые помогут в настройке производительности запросов Hive.
* [Оптимизация запросов Hive для Hadoop в HDInsight](https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-optimize-hive-query/)
* [Troubleshooting Hive query performance](https://blogs.msdn.microsoft.com/bigdatasupport/2015/08/13/troubleshooting-hive-query-performance-in-hdinsight-hadoop-cluster/) (Устранение неполадок с производительностью запросов Hive)
* [Примите участие в дискуссии об оптимизации Hive на HDInsight](https://channel9.msdn.com/events/Machine-Learning-and-Data-Sciences-Conference/Data-Science-Summit-2016/MSDSS25)
