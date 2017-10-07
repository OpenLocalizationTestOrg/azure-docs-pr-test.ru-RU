---
title: "Преобразование данных: обработка и преобразование данных | Документация Майкрософт"
description: "Узнайте, как tootransform данных или обработки данных в фабрике данных Azure с помощью машинного обучения, аналитика Озера данных Azure или Hadoop."
keywords: "преобразование данных, обработка данных, преобразование данных, действие преобразования"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 39786731-1e4b-40a4-81b7-d06e127427aa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 917d617259699b0e71de3a0e0c17463d00f2e0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-in-azure-data-factory"></a>Преобразование данных в фабрике данных Azure
> [!div class="op_single_selector"]
> * [Hive](data-factory-hive-activity.md)  
> * [Pig](data-factory-pig-activity.md)  
> * [MapReduce](data-factory-map-reduce.md)  
> * [Потоковая передача Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Машинное обучение](data-factory-azure-ml-batch-execution-activity.md) 
> * [Хранимая процедура](data-factory-stored-proc-activity.md)
> * [Аналитика озера данных U-SQL](data-factory-usql-activity.md)
> * [Пользовательские действия .NET](data-factory-use-custom-activities.md)

## <a name="overview"></a>Обзор
В этой статье описываются действия преобразования данных в фабрике данных Azure, можно использовать tootransform и обрабатывает необработанные данные, создавая прогнозы и аналитики. Действие преобразования выполняется в вычислительной среде, например в кластере Azure HDInsight или пакетной службе Azure. Он предоставляет подробные сведения о каждом действии преобразования tooarticles ссылки.

Фабрика данных поддерживает следующие действия преобразования данных, которые могут быть добавлены слишком hello[конвейеры](data-factory-create-pipelines.md) либо по отдельности или привязанные с другим действием.

> [!NOTE]
> Пошаговое руководство см. в статье [Учебник. Создание первого конвейера для обработки данных с помощью кластера Hadoop](data-factory-build-your-first-pipeline.md).  
> 
> 

## <a name="hdinsight-hive-activity"></a>Действие Hive HDInsight
Hello действие Hive в HDInsight из конвейера фабрики данных выполняет запросы Hive самостоятельно или кластера HDInsight под управлением Windows и Linux по требованию. Дополнительные сведения об этом действии см. в разделе [Действие Hive](data-factory-hive-activity.md). 

## <a name="hdinsight-pig-activity"></a>Действие Pig HDInsight
Hello действие Pig с HDInsight из конвейера фабрики данных выполняет собственную запросов Pig или кластера HDInsight под управлением Windows и Linux по требованию. Дополнительные сведения об этом действии см. в разделе [Действие Pig](data-factory-pig-activity.md). 

## <a name="hdinsight-mapreduce-activity"></a>Действие MapReduce HDInsight
Hello действие MapReduce в HDInsight из конвейера фабрики данных выполняет программ MapReduce самостоятельно или кластера HDInsight под управлением Windows и Linux по требованию. Дополнительные сведения об этом действии см. в разделе [Действие MapReduce](data-factory-map-reduce.md).

## <a name="hdinsight-streaming-activity"></a>Действие потоковой передачи HDInsight
Hello действие потоковой передачи HDInsight из конвейера фабрики данных выполняет программ потоковой передачи Hadoop на локальном или кластера HDInsight под управлением Windows и Linux по требованию. Дополнительные сведения об этом действии см. в разделе [Потоковая активность Hadoop](data-factory-hadoop-streaming-activity.md).

## <a name="hdinsight-spark-activity"></a>Действие HDInsight Spark
Hello действия HDInsight Spark в конвейере фабрики данных выполняет программы Spark в кластере HDInsight. Дополнительные сведения см. в разделе [Вызов программ Spark из фабрики данных](data-factory-spark.md). 

## <a name="machine-learning-activities"></a>Действия машинного обучения
Azure позволяет фабрики данных, вы tooeasily создавать конвейеры, использующих опубликованные машинного обучения Azure веб-службы для прогнозирования. С помощью hello [действие выполнения пакета](data-factory-azure-ml-batch-execution-activity.md#invoking-a-web-service-using-batch-execution-activity) в конвейере фабрики данных Azure, можно вызвать прогнозы машинного обучения веб-службы toomake на hello данных в пакете.

Со временем hello прогнозных моделей в hello машинного обучения, оценки экспериментов требуется toobe повторное обучение с помощью нового входных наборов данных. После завершения переподготовки, вы хотите tooupdate hello оценки веб-службы с hello повторное Обучение модели машинного обучения. Можно использовать hello [действия ресурса обновления](data-factory-azure-ml-batch-execution-activity.md#updating-models-using-update-resource-activity) tooupdate hello веб-службы с hello вновь обученной модели.  

Дополнительные сведения об этих действиях машинного обучения см. в разделе [Создание прогнозных конвейеров с помощью действий машинного обучения Azure](data-factory-azure-ml-batch-execution-activity.md). 

## <a name="stored-procedure-activity"></a>Действие хранимой процедуры
Можно использовать действие hello хранимую процедуру SQL Server в tooinvoke конвейера фабрики данных хранимой процедуры в одном hello, следуя хранилищ данных: базы данных SQL Azure, хранилище данных SQL Azure, база данных SQL Server в вашей организации или Виртуальной машине Azure. Дополнительные сведения см. в разделе [Действие хранимой процедуры](data-factory-stored-proc-activity.md).  

## <a name="data-lake-analytics-u-sql-activity"></a>Действие U-SQL Data Lake Analytics
Действие U-SQL Data Lake Analytics запускает сценарий U-SQL для кластера Azure Data Lake Analytics. Дополнительные сведения см. в разделе [Запуск скрипта U-SQL в аналитике озера данных Azure из фабрики данных Azure](data-factory-usql-activity.md). 

## <a name="net-custom-activity"></a>Настраиваемое действие .NET
Если требуются данные tootransform способом, не поддерживаемый фабрики данных, можно создать пользовательское действие с свою собственную логику для обработки данных и использовать hello действия в конвейере hello. Вы можете настроить toorun .NET действие hello для пользовательских с помощью пакетной службы Azure или кластере Azure HDInsight. Дополнительные сведения см. в разделе [Использование настраиваемых действий в конвейере фабрики данных Azure](data-factory-use-custom-activities.md). 

Можно создать настраиваемое действие toorun R-скриптов в кластере HDInsight с помощью R установлен. Ознакомьтесь с примером в репозитории GitHub [Run R Script using Azure Data Factory](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample) (Запуск сценария R с помощью фабрики данных Azure). 

## <a name="compute-environments"></a>Вычислительные среды
Создать связанную службу для среды вычислений hello и затем использовать службу hello связаны при определении действия преобразования. Фабрика данных поддерживает вычислительные среды двух типов. 

1. **По запросу**: В этом случае hello вычислительной среды полностью управляются фабрики данных. Она автоматически создается путем hello служба фабрики данных до задания tooprocess отправленных данных и удалены после завершения задания hello. Можно настроить и управлять детализированные параметры hello по требованию вычислительную среду для выполнения задания, управления кластером и начальную загрузку действия. 
2. **Собственная**— в этом случае вы регистрируете собственную вычислительную среду (например, кластер HDInsight) и используете ее в качестве связанной службы в фабрике данных. вычислительная среда Hello управляется вами и hello служба фабрики данных использует tooexecute hello действий. 

В разделе [связанные службы вычислений](data-factory-compute-linked-services.md) toolearn статьи о вычислений поддерживаемые фабрикой данных службы. 

## <a name="summary"></a>Сводка
Azure поддерживает фабрики данных hello следующие действия преобразования данных и hello вычислительных сред для hello действий. Hello преобразования действия могут быть добавлены toopipelines либо по отдельности или объединении в цепочку с другим действием.

| Действия по преобразованию данных | Вычислительная среда |
|:--- |:--- |
| [Hive](data-factory-hive-activity.md) |HDInsight [Hadoop] |
| [Pig](data-factory-pig-activity.md) |HDInsight [Hadoop] |
| [MapReduce](data-factory-map-reduce.md) |HDInsight [Hadoop] |
| [Потоковая передача Hadoop](data-factory-hadoop-streaming-activity.md) |HDInsight [Hadoop] |
| [Действия машинного обучения: выполнение пакета и обновление ресурса](data-factory-azure-ml-batch-execution-activity.md) |Azure |
| [Хранимая процедура](data-factory-stored-proc-activity.md) |Azure SQL, хранилище данных Azure SQL или SQL Server |
| [Аналитика озера данных U-SQL](data-factory-usql-activity.md) |Аналитика озера данных Azure |
| [DotNet](data-factory-use-custom-activities.md) |HDInsight [Hadoop] или пакетная служба Azure |

