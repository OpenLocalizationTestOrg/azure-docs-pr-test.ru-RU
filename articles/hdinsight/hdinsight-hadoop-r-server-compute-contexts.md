---
title: "Параметры контекстного aaaCompute для R Server HDInsight — Azure | Документы Microsoft"
description: "Дополнительные сведения о hello различных вычислительных контекста параметры доступные toousers с сервером R в HDInsight"
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0deb0b1c-4094-459b-94fc-ec9b774c1f8a
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: b3b0d0cc3caa390797dcff8c73d66cd3ad78bcaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="compute-context-options-for-r-server-on-hdinsight"></a>Варианты контекста вычислений для R Server в HDInsight

Microsoft R Server на Azure HDInsight управляет выполнением вызовов, параметр контекста вычислений hello. В этой статье рассматриваются параметры hello, будут ли доступны toospecify и как удалось распараллелить выполнения между ядрами hello граничного узла или кластера HDInsight.

Hello граничного узла кластера обеспечивает удобное место tooconnect toohello кластера и toorun R-сценарии. С граничного узла у вас есть hello функций ScaleR возможность выполнения hello параллелизован распределенных между ядрами hello hello edge узел сервера. Также выполнять их на узлах hello hello кластера с помощью элемента ScaleR Map-Reduce Hadoop или Spark контекстов вычислений.

## <a name="microsoft-r-server-on-azure-hdinsight"></a>Microsoft R Server в Azure HDInsight
[Microsoft R Server на Azure HDInsight](hdinsight-hadoop-r-server-overview.md) предоставляет hello новейшим возможностям для анализа на основе R. Он может использовать данные, хранящиеся в контейнере HDFS в вашей [больших двоичных объектов Azure](../storage/common/storage-introduction.md "хранилища больших двоичных объектов Azure") учетной записи хранилища, хранилища Озера данных или hello локальной файловой системе Linux. Поскольку R Server встроена в R с открытым кодом, hello R-приложений, создаваемые можно применять какие-либо hello 8000 + пакеты R с открытым кодом. Они могут также использовать подпрограммы hello в [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler), пакет аналитики большие наборы данных корпорации Майкрософт, входит в состав R Server.  

## <a name="compute-contexts-for-an-edge-node"></a>Контексты вычислений для граничного узла
Как правило сценарий R, выполняемой в R Server на hello граничного узла выполняется в интерпретатора hello R на этом узле. Hello исключениями являются шагов, которые вызывают функцию ScaleR. Hello ScaleR вызовы выполняются в среде вычислений, которая определяется как задать контекст вычислений ScaleR hello.  При выполнении сценария R из граничного узла hello возможных значений hello вычислений, контекста:

- локальный последовательный (*‘local’*);
- локальный параллельный (*‘localpar’*);
- Map Reduce
- Spark

Hello *'local'* и *«localpar»* параметры отличаются только в том, как **rxExec** вызовы выполняются. Они оба выполняются другие вызовы функций rx параллельных образом для всех доступных ядер Если не указано иное с помощью hello ScaleR **numCoresToUse** вариант, например `rxOptions(numCoresToUse=6)`. Параметры параллельного выполнения обеспечивают оптимальную производительность.

Hello в следующей таблице перечислены различные вычислений tooset параметры контекста выполнения вызовов hello.

| Контекст вычислений  | Как tooset                      | Контекст выполнения                        |
| ---------------- | ------------------------------- | ---------------------------------------- |
| Локальный последовательный | rxSetComputeContext(‘local’)    | Параллелизованный выполнения между ядрами hello hello пограничного узел сервера, за исключением rxExec вызовы, которые обрабатываются последовательно |
| Локальный параллельный   | rxSetComputeContext(‘localpar’) | Параллелизованный выполнения между ядрами hello hello пограничный сервер узла |
| Spark            | RxSpark()                       | Параллельно распределенное выполнение через Spark на узлах hello hello кластер HDI |
| Map Reduce       | RxHadoopMR()                    | Параллельно распределенное выполнение через Map Reduce по узлам hello hello кластер HDI |

## <a name="guidelines-for-deciding-on-a-compute-context"></a>Рекомендации по выбору контекста вычислений

Какой из трех вариантов hello выборе, предоставляющие Параллелизованный выполнения зависит от природы hello работы аналитика, размер hello и hello расположения данных. Нет нет простой формулы, информирующее о которой toouse контекст вычислений. Однако, существуют некоторые основные принципы, которые помогут вам сделать правильный выбор hello, или по крайней мере, помочь сузить выбранные параметры перед запуском теста производительности. К ним относятся следующие:

- локальная файловая система Linux Hello выполняется быстрее, чем HDFS.
- Повторяющиеся анализ работают быстрее, если локальные данные hello и если он находится в XDF.
- Он является более предпочтительным, чем toostream небольших объемов данных из источника данных text. Если размер hello объем данных, преобразуйте его tooXDF перед анализом.
- издержки Hello копирование или потоковая передача граничного узла toohello hello данных для анализа становится неудобными для очень больших объемов данных.
- Spark работает быстрее, чем MapReduce для анализа в Hadoop.

Учитывая эти принципы, hello в последующих разделах приводятся некоторые общие правила выбора контекст вычислений.

### <a name="local"></a>Local
* Если не требуется повторный анализ hello объем данных tooanalyze мал, затем потоковой его непосредственно в hello анализ сопоставление с помощью *'local'* или *«localpar»*.
* Если объем hello tooanalyze данных небольшого или среднего размера и требует повторного анализа, затем скопируйте его toohello локальной файловой системе, импортировать его tooXDF и проанализировать их через *'local'* или *«localpar»*.

### <a name="hadoop-spark"></a>Hadoop Spark
* Если объем hello tooanalyze данных имеет большой размер, затем импортировать его tooa Spark кадр данных с помощью **RxHiveData** или **RxParquetData**, или tooXDF в HDFS (если хранилище не проблемы) и проанализировать его с помощью hello Spark контекста вычислений.

### <a name="hadoop-map-reduce"></a>Hadoop Map Reduce
* Используйте контекст вычислений Map Reduce hello только в случае проблемы непреодолимые с контекстом вычислений Spark hello так как это обычно медленнее.  

## <a name="inline-help-on-rxsetcomputecontext"></a>Встроенная справка по rxSetComputeContext
Дополнительные сведения и примеры ScaleR контекстов вычислений см. в разделе hello встроенной справки в R в методе rxSetComputeContext hello, например:

    > ?rxSetComputeContext

Можно также ссылаться toohello»[руководство распределенных вычислений ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)", которое доступно из hello [R Server MSDN](https://msdn.microsoft.com/library/mt674634.aspx "R Server на сайте MSDN") библиотеки.

## <a name="next-steps"></a>Дальнейшие действия
В этой статье вы узнали о параметрах hello доступных toospecify способ и выполнения параллелизации подвергается между ядрами hello граничного узла или кластера HDInsight. toolearn Дополнительные сведения о как кластеры toouse R Server с HDInsight, в разделе hello следующие вопросы:

* [Общие сведения об R Server в HDInsight (предварительная версия)](hdinsight-hadoop-r-server-overview.md)
* [Приступая к работе с R Server в HDInsight (предварительная версия)](hdinsight-hadoop-r-server-get-started.md)
* [Добавление сервера RStudio tooHDInsight (если не добавлен во время создания кластера)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Параметры службы хранилища Azure для R Server в HDInsight (предварительная версия)](hdinsight-hadoop-r-server-storage.md)

