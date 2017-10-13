---
title: "Использование Apache Phoenix и SQLLine c HBase в Azure HDInsight | Документация Майкрософт"
description: "Из этой статьи вы узнаете, как использовать Apache Phoenix в HDInsight. Также здесь объясняется, как установить и настроить SQLLine на компьютере для подключения к кластеру HBase в HDInsight."
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
ms.date: 09/22/2017
ms.author: jgao
ms.openlocfilehash: 41bfef95059b7c5343d952b4fe372e3baae6f9d7
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a>Использование Apache Phoenix с кластерами HBase под управлением Linux в HDInsight
Из этой статьи вы узнаете, как использовать [Apache Phoenix](http://phoenix.apache.org/) в Azure HDInsight, а также как использовать SQLLine. Дополнительные сведения о Phoenix см. в статье [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html) (Phoenix за 15 минут или меньше). Сведения о грамматике Phoenix см. [здесь](http://phoenix.apache.org/language/index.html).

> [!NOTE]
> Сведения о версии Phoenix в HDInsight см. в статье [Что представляют собой компоненты и версии Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md)
>
>

## <a name="use-sqlline"></a>Использование SQLLine
[SQLLine](http://sqlline.sourceforge.net/) — это программа командной строки для выполнения SQL.

### <a name="prerequisites"></a>Предварительные требования
Для использования SQLLine требуются следующие компоненты:

* **Кластер HBase в HDInsight.** Чтобы создать его, см. сведения в статье [Начало работы с примером Apache HBase в HDInsight](./hdinsight-hbase-tutorial-get-started.md).

При подключении к кластеру HBase необходимо подключиться к одной из виртуальных машин Zookeeper. Каждый кластер HDInsight содержит три виртуальных машины Zookeeper.

**Получение имени узла Zookeeper**

1. Откройте Ambari, перейдя по адресу **https://\<имя кластера\>.azurehdinsight.net**.
2. Чтобы войти в систему, введите имя пользователя (кластера) HTTP и пароль.
3. В меню слева выберите **ZooKeeper**. В списке отобразятся три экземпляра **ZooKeeper Server**.
4. Выберите один из экземпляров **ZooKeeper Server**. На панели **Сводка** найдите **имя узла**. Оно аналогично *zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.

**Использование SQLLine**

1. Подключитесь к кластеру с помощью SSH. Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. В SSH используйте следующие команды для запуска SQLLine:

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ZOOKEEPER SERVER FQDN>:2181:/hbase-unsecure
3. Чтобы создать таблицу HBase и вставить данные, выполните следующие команды:

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

Дополнительные сведения см. в [руководстве по SQLLine](http://sqlline.sourceforge.net/#manual) и статье о [грамматике Phoenix](http://phoenix.apache.org/language/index.html).

## <a name="next-steps"></a>Дальнейшие действия
В этой статье вы изучили использование Apache Phoenix в HDInsight. Дополнительные сведения см. в статьях ниже:

* [Что такое HBase в HDInsight: база данных NoSQL, которая предоставляет возможности, схожие BigTable, для Hadoop][hdinsight-hbase-overview].
  HBase — это разработанная Apache база данных NoSQL с открытым исходным кодом, созданная на основе Hadoop. HBase обеспечивает произвольный доступ и строгую согласованность для больших объемов неструктурированных и слабоструктурированных данных.
* [Подготовка кластеров HBase в виртуальной сети Azure][hdinsight-hbase-provision-vnet].
  Благодаря интеграции виртуальной сети кластеры HBase могут быть развернуты в той же виртуальной сети, что и приложения. Это позволяет приложениям обмениваться данными с HBase напрямую.
* [Настройка репликации HBase в HDInsight](hdinsight-hbase-replication.md). Узнайте, как настроить репликацию HBase между двумя центрами обработки данных Azure.


[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
