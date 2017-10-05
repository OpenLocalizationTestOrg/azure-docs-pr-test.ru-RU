---
title: "Использование Interactive Hive в HDInsight — Azure | Документы Майкрософт"
description: "Сведения об использовании Interactive Hive (Hive в LLAP) в HDInsight."
keywords: 
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0957643c-4936-48a3-84a3-5dc83db4ab1a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: e7874b55fc72f14d8e2c801872359e823cb2ba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a>Использование Interactive Hive в HDInsight (предварительная версия)
Interactive Hive (также называемый [Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) является новым [типом кластера](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) HDInsight.  Interactive Hive обеспечивает кэширование в памяти, благодаря чему запросы Hive становятся более интерактивными и быстрыми. Эта новая функция делает HDInsight одним из самых производительных, гибких и открытых решений для работы с большими данными в облаке с кэш-памятью (с использованием Hive и Spark). Она также предоставляет расширенную аналитику благодаря тесной интеграции со службами R. 

Кластер Interactive Hive отличается от кластера Hadoop. Он содержит только службу Hive. 

> [!NOTE]
> MapReduce, Pig, Sqoop, Oozie и другие службы скоро будут удалены из кластера этого типа.
> Служба Hive в кластере Interactive Hive доступна только через представление Ambari Hive, Beeline и Hive ODBC. К ней невозможно получить доступ через консоль Hive, Templeton, интерфейс командной строки Azure и Azure PowerShell. 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a>Создание кластера Interactive Hive
Кластер Interactive Hive поддерживается только на кластерах под управлением Linux. Дополнительные сведения о создании кластеров HDInsight см. в статье [Создание кластеров Hadoop под управлением Linux в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="execute-hive-from-interactive-hive"></a>Выполнение Hive из Interactive Hive
Существуют различные варианты выполнения запросов Hive.

* Запуск Hive с помощью представления Ambari Hive.
  
    Сведения об использовании представления Hive см. в статье [Использование представления Hive с Hadoop в HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).
* Запуск Hive с помощью Beeline.
  
    Дополнительные сведения об использовании Beeline в HDInsight см. в статье [Использование Hive с Hadoop в HDInsight с применением Beeline](hdinsight-hadoop-use-hive-beeline.md).
  
    Используйте Beeline на головном узле или на пустом граничном узле.  Рекомендуется использовать Beeline на пустом граничном узле.  Дополнительные сведения о создании кластера HDInsight с пустым граничным узлом см. в статье [Использование пустых граничных узлов в HDInsight](hdinsight-apps-use-edge-node.md).
* Запуск Hive с помощью Hive ODBC.
  
    Дополнительные сведения об использовании Hive ODBC см. в статье [Подключение Excel к Hadoop с помощью драйвера Microsoft Hive ODBC](hdinsight-connect-excel-hive-odbc-driver.md).

**Чтобы узнать строку подключения JDBC:**

1. Войдите в Ambari, используя следующий URL-адрес: https://<ClusterName>. AzureHDInsight.net.
2. Щелкните **Hive** в меню слева.
3. Щелкните выделенный значок, чтобы скопировать URL-адрес.
   
   ![JDBC для HDInsight Hadoop типа Interactive Hive на LLAP](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a>Дополнительные материалы
* [Создание кластеров Hadoop под управлением Linux в HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Использование Hive с Hadoop в HDInsight с применением Beeline](hdinsight-hadoop-use-hive-beeline.md)
* [Подключение Excel к Hadoop с помощью драйвера Microsoft Hive ODBC](hdinsight-connect-excel-hive-odbc-driver.md)

