---
title: "aaaPorts, используемый службами Hadoop в HDInsight - Azure | Документы Microsoft"
description: "Список портов, которые используются службами Hadoop, работающими в кластере HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd14aed9-ec25-4bb3-a20c-e29562735a7d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: 0abc5c1c678aa79816e3e82a74538d2fb6db40ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="ports-used-by-hadoop-services-on-hdinsight"></a>Порты, используемые службами Hadoop в HDInsight

Этот документ предоставляет список hello порты, используемые службами Hadoop, работающих в кластерах HDInsight под управлением Linux. Он также предоставляет сведения о портах, используемых tooconnect toohello кластера с помощью SSH.

## <a name="public-ports-vs-non-public-ports"></a>Общедоступные и необщедоступные порты

Здравствуйте, HDInsight под управлением Linux, кластеры предоставляют только три порта публично на Интернет; 22, 23 и 443. Эти порты, используемые toosecurely доступа hello кластера с помощью SSH и служб, доступных по протоколу HTTPS безопасного hello.

Внутренне HDInsight реализуется на нескольких виртуальных машинах Azure (hello узлы в кластере hello) на виртуальную сеть Azure. Из hello виртуальной сети, можно вызвать порты, не предоставляется через hello Интернета. Например при подключении tooone hello головного узлов с помощью SSH из головного узла hello затем непосредственно доступны служб, работающих на узлах кластера hello.

> [!IMPORTANT]
> Если не указать виртуальную сеть Azure с помощью параметра конфигурации для HDInsight, она будет создана автоматически. Тем не менее нельзя соединить виртуальную сеть toothis других машин (например, другие виртуальные машины Azure или клиентского компьютера разработки).


toojoin дополнительных компьютеров toohello виртуальной сети, необходимо сначала создать виртуальную сеть hello и затем указать его при создании кластера HDInsight. Дополнительные сведения см. в статье [Расширение возможностей HDInsight с помощью виртуальной сети Azure](hdinsight-extend-hadoop-virtual-network.md).

## <a name="public-ports"></a>Общедоступные порты

Hello все узлы в кластере HDInsight находятся в виртуальной сети Azure и нельзя получить доступ напрямую из hello Интернета. Открытые шлюза предоставляет следующие порты, которые являются общими для всех типов кластера HDInsight toohello доступа к Интернету.

| служба | Порт | Протокол | Описание |
| --- | --- | --- | --- | --- |
| sshd |22 |SSH |Подключение клиентов toosshd на основной головному узлу hello. Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md). |
| sshd |22 |SSH |Подключение клиентов toosshd на hello граничного узла. Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md). |
| sshd |23 |SSH |Подключение клиентов toosshd на вторичный головному узлу hello. Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md). |
| Ambari |443 |HTTPS |Веб-интерфейс Ambari. В разделе [управление HDInsight с помощью hello Ambari веб-интерфейса](hdinsight-hadoop-manage-ambari.md) |
| Ambari |443 |HTTPS |REST API Ambari. В разделе [управление HDInsight с помощью API-интерфейса REST Ambari "hello"](hdinsight-hadoop-manage-ambari-rest-api.md) |
| WebHCat |443 |HTTPS |REST API HCatalog. См. статьи [Выполнение заданий Pig с помощью Curl с использованием Hadoop в HDInsight](hdinsight-hadoop-use-pig-curl.md), [Выполнение заданий Pig с помощью Curl с использованием Hadoop в HDInsight](hdinsight-hadoop-use-pig-curl.md) и [Выполнение заданий MapReduce с помощью Curl с использованием Hadoop в HDInsight](hdinsight-hadoop-use-mapreduce-curl.md). |
| HiveServer2 |443 |ODBC |Подключение с использованием ODBC tooHive. В разделе [tooHDInsight Excel подключиться с помощью драйвера Microsoft ODBC hello](hdinsight-connect-excel-hive-odbc-driver.md). |
| HiveServer2 |443 |JDBC |Подключение с использованием JDBC tooHive. В разделе [подключения tooHive на HDInsight с помощью драйвера Hive JDBC hello](hdinsight-connect-hive-jdbc-driver.md) |

Hello ниже приведены доступные для конкретного кластера типов.

| служба | Порт | Протокол | Тип кластера | Описание |
| --- | --- | --- | --- | --- |
| Stargate |443 |HTTPS |HBase |REST API HBase. См. статью [Руководство по HBase. Приступая к работе с Apache HBase на Hadoop под управлением Linux в HDInsight](hdinsight-hbase-tutorial-get-started-linux.md). |
| Livy |443 |HTTPS |Spark |Spark REST API. См. статью [Удаленная отправка заданий Spark в кластер Apache Spark в HDInsight на платформе Linux с помощью Livy](hdinsight-apache-spark-livy-rest-interface.md). |
| Storm |443 |HTTPS |Storm |Веб-интерфейс Storm. См. статью [Развертывание топологий Apache Storm в HDInsight под управлением Linux и управление ими](hdinsight-storm-deploy-monitor-topology-linux.md). |

### <a name="authentication"></a>Аутентификация

Все службы, открытым на приветствия Интернета должны пройти проверку подлинности.

| Порт | Учетные данные |
| --- | --- |
| 22 или 23 |Hello SSH пользователя учетные данные, указанные во время создания кластера |
| 443 |Имя входа Hello (по умолчанию: администратора) и пароль, которые были заданы при создании кластера |

## <a name="non-public-ports"></a>Необщедоступные порты

> [!NOTE]
> Некоторые службы доступны только в кластерах определенных типов. Например, служба HBase доступна только на кластерах типа HBase.

> [!IMPORTANT]
> Некоторые службы могут работать только на одном головном узле одновременно. Если попытка службы toohello tooconnect на основной головному узлу hello и получать сообщение об ошибке 404, повторите попытку, используя вторичный головному узлу hello.

### <a name="ambari"></a>Ambari

| служба | Nodes | Порт | URL-адрес | Протокол | 
| --- | --- | --- | --- | --- |
| Веб-интерфейс Ambari | Головные узлы | 8080 | / | HTTP |
| Ambari REST API | Головные узлы | 8080 | /api/v1 | HTTP |

Примеры:

* Ambari REST API: `curl -u admin "http://10.0.0.11:8080/api/v1/clusters"`

### <a name="hdfs-ports"></a>Порты HDFS

| служба | Nodes | Порт | Протокол | Описание |
| --- | --- | --- | --- | --- |
| Веб-интерфейс узла имен |Головные узлы |30070 |HTTPS |Состояние tooview Web пользовательского интерфейса |
| Служба метаданных на узле имен |Головные узлы |8020 |IPC |Метаданные файловой системы |
| Узел данных |Все рабочие узлы |30075 |HTTPS |Состояние tooview Web пользовательского интерфейса, журналы, и т. д. |
| Узел данных |Все рабочие узлы |30010 |&nbsp; |Передача данных |
| Узел данных |Все рабочие узлы |30020 |IPC |Операции с метаданными |
| Дополнительный узел имен |Головные узлы |50090 |HTTP |Контрольная точка для метаданных узла имен |

### <a name="yarn-ports"></a>Порты YARN

| служба | Nodes | Порт | Протокол | Описание |
| --- | --- | --- | --- | --- |
| Веб-интерфейс для диспетчера Resource Manager |Головные узлы |8088 |HTTP |Веб-интерфейс для диспетчера Resource Manager |
| Веб-интерфейс для диспетчера Resource Manager |Головные узлы |8090 |HTTPS |Веб-интерфейс для диспетчера Resource Manager |
| Интерфейс администратора для Resource Manager |Головные узлы |8141 |IPC |Для отправки приложений (Hive, Hive Server, Pig и т. д.) |
| Планировщик Resource Manager |Головные узлы |8030 |HTTP |Интерфейс администратора |
| Интерфейс приложения Resource Manager |Головные узлы |8050 |HTTP |Адрес интерфейса диспетчера приложения hello |
| Диспетчер узлов |Все рабочие узлы |30050 |&nbsp; |адрес Hello диспетчер контейнеров для hello |
| Веб-интерфейс диспетчера узлов |Все рабочие узлы |30060 |HTTP |Интерфейс Resource Manager |
| Адрес временной шкалы |Головные узлы |10200 |RPC |Здравствуйте, временная шкала службы RPC. |
| Веб-интерфейс временной шкалы |Головные узлы |8181 |HTTP |Hello временная шкала службы веб-интерфейса |

### <a name="hive-ports"></a>Порты Hive

| служба | Nodes | Порт | Протокол | Описание |
| --- | --- | --- | --- | --- |
| HiveServer2 |Головные узлы |10001 |Thrift |Службы для подключения tooHive (Thrift/JDBC) |
| Метахранилище Hive |Головные узлы |9083 |Thrift |Службы для подключения tooHive метаданных (Thrift/JDBC) |

### <a name="webhcat-ports"></a>Порты WebHCat

| служба | Nodes | Порт | Протокол | Описание |
| --- | --- | --- | --- | --- |
| Сервер WebHCat |Головные узлы |30111 |HTTP |Веб-API на базе HCatalog и других служб Hadoop |

### <a name="mapreduce-ports"></a>Порты MapReduce

| служба | Nodes | Порт | Протокол | Описание |
| --- | --- | --- | --- | --- |
| Журнал заданий |Головные узлы |19888 |HTTP |Веб-интерфейс журнала заданий MapReduce |
| Журнал заданий |Головные узлы |10020 |&nbsp; |Сервер журнала заданий MapReduce |
| Обработчик перемещений |&nbsp; |13562 |&nbsp; |Промежуточные карты передачи выводит toorequesting Reducers |

### <a name="oozie"></a>Oozie,

| служба | Nodes | Порт | Протокол | Описание |
| --- | --- | --- | --- | --- |
| Сервер Oozie |Головные узлы |11000 |HTTP |URL-адрес службы Oozie |
| Сервер Oozie |Головные узлы |11001 |HTTP |Порт для администрирования Oozie |

### <a name="ambari-metrics"></a>Метрики Ambari

| служба | Nodes | Порт | Протокол | Описание |
| --- | --- | --- | --- | --- |
| Временная шкала (журнал приложения) |Головные узлы |6188 |HTTP |Hello временная шкала службы веб-интерфейса |
| Временная шкала (журнал приложения) |Головные узлы |30200 |RPC |Hello временная шкала службы веб-интерфейса |

### <a name="hbase-ports"></a>Порты HBase

| служба | Nodes | Порт | Протокол | Описание |
| --- | --- | --- | --- | --- |
| HMaster |Головные узлы |16000 |&nbsp; |&nbsp; |
| Веб-интерфейс информационного сервера HMaster |Головные узлы |16010 |HTTP |Hello порта для веб-HBase образец hello пользовательского интерфейса |
| Региональный сервер |Все рабочие узлы |16020 |&nbsp; |&nbsp; |
| &nbsp; |&nbsp; |2181 |&nbsp; |Hello порта, которую клиенты используют tooconnect tooZooKeeper |

### <a name="kafka-ports"></a>Порты Kafka

| служба | Nodes | Порт | Протокол | Описание |
| --- | --- | --- | --- | --- |
| Broker |Рабочие узлы |9092 |[Сетевой протокол Kafka](http://kafka.apache.org/protocol.html) |Используется для связи с клиентами |
| &nbsp; |Узлы Zookeeper |2181 |&nbsp; |Hello порта, которую клиенты используют tooconnect tooZookeeper |

### <a name="spark-ports"></a>Порты Spark

| служба | Nodes | Порт | Протокол | URL-адрес | Описание |
| --- | --- | --- | --- | --- | --- |
| Серверы Thrift Spark |Головные узлы |10002 |Thrift | &nbsp; | Службы для подключения tooSpark SQL (Thrift/JDBC) |
| Сервер Livy | Головные узлы | 8998 | HTTP | /пакеты | Служба для запуска инструкций, заданий и приложений |

Примеры:

* Livy: `curl "http://10.0.0.11:8998/batches"`. В этом примере `10.0.0.11` — IP-адрес hello hello головному узлу, на котором размещена служба Livy hello.
