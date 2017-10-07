---
title: "Интерактивный Hive в HDInsight - Azure aaaUse | Документы Microsoft"
description: "Узнайте, как интерактивный Hive (Hive на LLAP) в HDInsight toouse."
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
ms.openlocfilehash: 9e751a08091d18bc1b3d070468feef87f6828c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a>Использование Interactive Hive в HDInsight (предварительная версия)
Interactive Hive (также называемый [Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) является новым [типом кластера](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) HDInsight.  Interactive Hive обеспечивает кэширование в памяти, благодаря чему запросы Hive становятся более интерактивными и быстрыми. Эта новая возможность делает HDInsight один hello мире большинство производительными, гибкий и открытый больших данных решений в облаке hello с кэшем в памяти (с помощью Hive и Spark) и advanced analytics через глубокую интеграцию со службами R Services. 

Интерактивный Hive кластера Hello отличается от кластера Hadoop hello. Он содержит только службы Hive hello. 

> [!NOTE]
> MapReduce, Pig, Sqoop, Oozie и другие службы скоро будут удалены из кластера этого типа.
> Hello службы Hive в кластере интерактивный Hive hello доступен только через hello представление Ambari Hive, Beeline и Hive ODBC. К ней невозможно получить доступ через консоль Hive, Templeton, интерфейс командной строки Azure и Azure PowerShell. 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a>Создание кластера Interactive Hive
Кластер Interactive Hive поддерживается только на кластерах под управлением Linux. Дополнительные сведения о создании кластеров HDInsight см. в статье [Создание кластеров Hadoop под управлением Linux в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="execute-hive-from-interactive-hive"></a>Выполнение Hive из Interactive Hive
Существуют различные варианты выполнения запросов Hive.

* Запустите Hive с помощью hello куст Ambari представление
  
    Hello сведения об использовании hello Hive представления см. в разделе [hello используйте представление Hive с Hadoop в HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).
* Запуск Hive с помощью Beeline.
  
    Hello сведения об использовании Beeline на HDInsight см. в разделе [используйте Hive в с Hadoop в HDInsight с Beeline](hdinsight-hadoop-use-hive-beeline.md).
  
    Используйте Beeline из головному узлу hello или пустой граничного узла.  Рекомендуется использовать Beeline на пустом граничном узле.  Дополнительные сведения о создании кластера HDInsight с пустым граничным узлом см. в статье [Использование пустых граничных узлов в HDInsight](hdinsight-apps-use-edge-node.md).
* Запуск Hive с помощью Hive ODBC.
  
    Hello сведения об использовании Hive ODBC см. в разделе [tooHadoop Excel подключиться с помощью драйвера Microsoft Hive ODBC hello](hdinsight-connect-excel-hive-odbc-driver.md).

**hello toofind строку подключения JDBC:**

1. Вход с помощью URL-адреса hello tooAmbari: https://<ClusterName>. AzureHDInsight.net.
2. Нажмите кнопку **Hive** из меню слева hello.
3. Щелкните URL-адрес toocopy значок hello выделяются hello:
   
   ![JDBC для HDInsight Hadoop типа Interactive Hive на LLAP](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a>См. также
* [Создавать кластеры под управлением Linux Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Узнайте, как кластеры toocreate интерактивного Hive в HDInsight.
* [Используйте Hive в с Hadoop в HDInsight с Beeline](hdinsight-hadoop-use-hive-beeline.md): Узнайте, как запросы Hive toosubmit Beeline toouse.
* [Подключение Excel tooHadoop с помощью драйвера Microsoft Hive ODBC hello](hdinsight-connect-excel-hive-odbc-driver.md): Узнайте, как tooconnect Excel tooHive.

