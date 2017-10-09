---
title: "aaaUse Финиксе Apache & белка с HBase - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse Финиксе Apache в HDInsight и как tooinstall и настройте белка на кластер рабочей станции tooconnect tooan HBase на HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: cda0f33b-a2e8-494c-972f-ae0bb482b818
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/26/2017
ms.author: jgao
ms.openlocfilehash: a63e8c8212b7a992453ec94fa638ec3863a0ede3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a>Использование Apache Phoenix с кластерами HBase под управлением Linux в HDInsight
Узнайте, как toouse [Финиксе Apache](http://phoenix.apache.org/) в HDInsight и как toouse SQLLine. Дополнительные сведения о Phoenix см. в статье [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html) (Phoenix за 15 минут или меньше). Hello Финиксе грамматики. в разделе [грамматики Финиксе](http://phoenix.apache.org/language/index.html).

> [!NOTE]
> Hello Финиксе сведения о версии в HDInsight, в разделе [новые возможности, предоставляемые HDInsight версиями кластеров Hadoop hello?](hdinsight-component-versioning.md).
>
>

## <a name="use-sqlline"></a>Использование SQLLine
[SQLLine](http://sqlline.sourceforge.net/) является tooexecute программы командной строки SQL.

### <a name="prerequisites"></a>Предварительные требования
Прежде чем использовать SQLLine, необходимо иметь следующие hello.

* **Кластер HBase в HDInsight.** Сведения о подготовке кластера HBase см. в статье [Руководство по HBase. Приступая к работе с Apache HBase на Hadoop под управлением Windows в HDInsight][hdinsight-hbase-get-started].
* **Подключите кластер HBase toohello посредством протокола удаленного рабочего стола hello**. Инструкции см. в разделе [кластеров управление Hadoop в HDInsight с помощью hello портал Azure][hdinsight-manage-portal].

При подключении tooan HBase кластера необходимо tooone tooconnect из hello Zookeepers. Каждый кластер HDInsight содержит три узла Zookeeper.

**toofind имя узла Zookeeper hello**

1. Откройте Ambari перейдя слишком**https://<ClusterName>. azurehdinsight.net**.
2. Введите имя пользователя и пароль toologin hello HTTP (кластер).
3. Нажмите кнопку **ZooKeeper** из меню слева hello. В списке будет три сервера **ZooKeeper Server**.
4. Выберите один из hello **ZooKeeper сервера** в списке. На сводной панели hello найти hello **Hostname**. Это аналогично слишком*zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.

**toouse SQLLine**

1. Подключите кластер toohello с помощью SSH. Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. В SSH выполните следующие команды toorun SQLLine hello.

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. Запустите следующие команды toocreate hello таблице HBase и вставить некоторые данные.

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

Дополнительные сведения см. в разделе [SQLLine manual](http://sqlline.sourceforge.net/#manual) (Руководство по SQLLine) и [Phoenix Grammar](http://phoenix.apache.org/language/index.html) (Грамматика Phoenix).

## <a name="next-steps"></a>Дальнейшие действия
В этой статье вы узнали как toouse Финиксе Apache в HDInsight.  toolearn более, см.:

* [Что такое HBase в HDInsight][hdinsight-hbase-overview]. HBase — это база данных NoSQL с открытым исходным кодом Apache, разработанная в рамках проекта Hadoop, которая обеспечивает произвольный доступ и строгую согласованность больших объемов неструктурированных и частично структурированных данных.
* [Подготовка кластеров HBase в виртуальной сети Azure][hdinsight-hbase-provision-vnet]: С интеграцией виртуальной сети кластеров HBase может быть развернутой toohello виртуальных сетевых как приложения таким образом, приложения могут взаимодействовать с HBase напрямую.
* [Настройка репликации HBase HDInsight](hdinsight-hbase-replication.md): Узнайте, как tooconfigure HBase репликации между двумя центрами обработки данных Azure.
* [Анализ мнений Twitter с HBase в HDInsight][hbase-twitter-sentiment]: Узнайте, как toodo в режиме реального времени [анализ мнений](http://en.wikipedia.org/wiki/Sentiment_analysis) больших данных с помощью кластера Hadoop в HDInsight HBase.

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
