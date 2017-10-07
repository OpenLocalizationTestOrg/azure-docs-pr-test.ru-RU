---
title: "репликация кластер HBase aaaConfigure внутри виртуальных сетей - Azure | Документы Microsoft"
description: "Узнайте, как tooconfigure HBase репликации для балансировки нагрузки, высокий уровень доступности, миграция или обновление простоев из одного tooanother версии HDInsight и аварийного восстановления."
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ba1c44f26b7cbf4a7a88159b12b3e064ea9f9a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a>Настройка репликации кластера HBase в виртуальных сетях

Узнайте, как tooconfigure HBase репликации в одной виртуальной сети (VNet) или между двумя виртуальными сетями.

Репликация кластера использует методологию source-push. Кластер HBase может быть исходным, кластером назначения или выполнять обе роли одновременно. Репликация выполняется асинхронно, а целью hello репликации является окончательной согласованности. Получив исходный hello семейство изменить tooa столбца с включенной репликацией, изменению — распространенный tooall конечных кластеров. При репликации данных из одного кластера tooanother hello исходного кластера и всех кластеров, которые уже потреблено hello данных являются отслеживаемых tooprevent циклов репликации.

В этом руководстве показано, как настроить репликацию "источник — назначение". Другие топологии кластеров см. в документе [Справочное руководство по Apache HBase](http://hbase.apache.org/book.html#_cluster_replication).

Примеры использования репликации HBase для одной виртуальной сети:

* Балансировка нагрузки — например, выполнение проверки одного или нескольких заданий MapReduce hello целевом кластере и передаче данных на исходном кластере hello
* высокую доступность;
* Перенос данных из одного tooanother кластер HBase
* Обновление кластера Azure HDInsight с одной версии tooanother

Примеры использования репликации HBase для двух виртуальных сетей:

* Аварийное восстановление
* Балансировка нагрузки и секционирования приложения hello
* высокую доступность;

Репликация кластеров осуществляется с помощью скриптов [действий сценария](hdinsight-hadoop-customize-cluster-linux.md), которые можно найти на веб-сайте [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).

## <a name="prerequisites"></a>Предварительные требования
Прежде чем приступать к изучению этого руководства, необходимо оформить подписку Azure. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="configure-hello-environments"></a>Настройка сред hello

Доступны три варианта конфигурации:

- два кластера HBase в одной виртуальной сети Azure;
- Два HBase кластеров в двух разных виртуальных сетей в hello одного региона
- два кластера HBase в двух виртуальных сетях в двух регионах (георепликация).

toomake его проще tooconfigure hello средах, мы создали некоторые [шаблоны Azure Resource Manager](../azure-resource-manager/resource-group-overview.md). Если вы предпочитаете tooconfigure hello сред с помощью других методов, см.:

- [Создание кластеров Hadoop под управлением Linux в HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
- [Создание кластеров HBase в виртуальной сети Azure](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a>Настройка одной виртуальной сети

Выберите следующие изображения toocreate HBase кластерами в hello hello одной виртуальной сети. Hello шаблон хранится в [шаблоны быстрый запуск Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

### <a name="configure-two-virtual-networks-in-hello-same-region"></a>Настройка двух виртуальных сетей в hello одного региона

Выберите следующие изображения toocreate двух виртуальных сетей с пиринга виртуальной сети и два кластера HBase в hello hello одного региона. Hello шаблон хранится в [шаблоны быстрый запуск Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>



В этом случае необходима [пиринговая связь между виртуальными сетями](../virtual-network/virtual-network-peering-overview.md). Hello шаблон позволяет пиринг виртуальной сети.   

Репликация HBase использует IP-адреса виртуальных машин ZooKeeper hello. Необходимо настроить статические IP-адреса для узлов HBase ZooKeeper hello назначения.

**tooconfigure статические IP-адреса**

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Hello в левом меню, щелкните **групп ресурсов**.
3. Выберите группу ресурсов, содержащий hello целевой кластер HBase. Это группа ресурсов hello, указанный вами при использовании среды hello toocreate шаблонов диспетчера ресурсов hello. Можно использовать toonarrow фильтра hello списку hello. Вы увидите список ресурсов, содержащий hello двух виртуальных сетей.
4. Щелкните hello виртуальной сети, содержащей hello целевой кластер HBase. Например, щелкните **xxxx-vnet2**. Вы увидите три устройства с именами, которые начинаются с **nic-zookeepermode -**. Эти устройства, hello трех ZooKeeper ВМ.
5. Выберите один из виртуальных машин ZooKeeper hello.
6. Щелкните **IP configurations** (Конфигурации IP).
7. Нажмите кнопку **ipConfig1** из списка hello.
8. Нажмите кнопку **статических**и запишите hello фактический IP-адрес. Необходимо будет hello IP-адрес при запуске действия tooenable hello сценария репликации.

  ![репликация HDInsight HBase, статический IP-адрес узла ZooKeeper](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. Повторите шаг 6 tooset hello статический IP-адрес для hello двух остальных узлов ZooKeeper.

Для сценария виртуальной сети между hello, необходимо использовать hello **- ip** переключение при вызове hello **hdi_enable_replication.sh** записать действие в скрипт.

### <a name="configure-two-virtual-networks-in-two-different-regions"></a>Настройка двух виртуальных сетей в двух регионах

Щелкните hello после изображения toocreate двух виртуальных сетей в двух разных регионах. Hello шаблон хранится в открытый контейнер больших двоичных объектов Azure.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

Создайте шлюз VPN между двумя виртуальными сетями hello. Инструкции см. в статье [Создание виртуальной сети с подключением типа "сеть — сеть" с помощью портала Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).

Репликация HBase использует IP-адреса виртуальных машин ZooKeeper hello. Необходимо настроить статические IP-адреса для узлов HBase ZooKeeper hello назначения. tooconfigure статический IP-адрес см. раздел «Настройка двух виртуальных сетей в hello одного региона» hello в этой статье.

Для сценария виртуальной сети между hello, необходимо использовать hello **- ip** переключение при вызове hello **hdi_enable_replication.sh** записать действие в скрипт.

## <a name="load-test-data"></a>Загрузка тестовых данных

При репликации кластера, необходимо указать tooreplicate таблиц hello. В этом разделе будет загружать некоторые данные в исходном кластере hello. В следующем разделе hello будет включить репликацию между двумя кластерами hello.

Следуйте инструкциям в разделе hello [учебника HBase: начало работы с Apache HBase на основе Linux Hadoop в HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) toocreate **контактов** таблицы и вставить некоторые данные в таблицу hello.

## <a name="enable-replication"></a>Включение репликации

Привет, следующие шаги показывают, как toocall hello сценарий действия сценария из hello портал Azure. Выполняется действие скрипта с помощью Azure PowerShell и hello Azure командной строки (CLI), в разделе [HDInsight под управлением Linux, настроить кластеры, использующие действие сценария](hdinsight-hadoop-customize-cluster-linux.md).

**репликация HBase tooenable из hello портал Azure**

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Откройте hello исходного HBase кластера.
3. Меню hello кластера, нажмите кнопку **действия скрипта**.
4. Нажмите кнопку **отправить новый** из hello верхней части колонки hello.
5. Выберите или введите hello следующую информацию:

  - **Имя:** введите **Включение репликации**.
  - **URL-адрес bash-скрипта:** введите **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.
  - **Головной узел:** выбран. Здравствуйте, снимите флажок для других типов узлов.
  - **Параметры**: hello следующие образцы параметры Включение репликации для всех существующих таблиц hello и скопируйте все данные hello из hello источника toohello назначения кластера:

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. Щелкните **Создать**. Hello скрипт может занять некоторое время, особенно при использовании аргумента - copydata hello.

Ниже приведены обязательные аргументы.

|Имя|Описание|
|----|-----------|
|-s, --src-cluster | Укажите DNS-имя кластера HBase источника hello hello. например -s hbsrccluster, --src-cluster=hbsrccluster. |
|-d, --dst-cluster | Укажите DNS-имя hello назначения «hello» (реплики) HBase кластера. например -s dsthbcluster, --src-cluster=dsthbcluster. |
|-sp, --src-ambari-password | Укажите пароль администратора hello для Ambari на кластер HBase источника hello. |
|-dp, --dst-ambari-password | Укажите пароль администратора hello для Ambari hello целевом кластере HBase.|

Необязательные аргументы для этой команды.

|Имя|Описание|
|----|-----------|
|-su, --src-ambari-user | Укажите имя пользователя администратора hello для Ambari hello источника HBase кластере. значение по умолчанию Hello — **администратора**. |
|-du, --dst-ambari-user | Укажите имя пользователя администратора hello для Ambari hello целевом кластере HBase. значение по умолчанию Hello — **администратора**. |
|-t, --table-list | Укажите toobe таблиц hello репликации. например --table-list="table1;table2;table3". Если не указать таблицы, будут реплицированы все существующие таблицы HBase.|
|-m, --machine | Укажите hello головной узел, где будет выполняться действие сценария hello. значение Hello — hn1 или hn0. Так как узел hn0 обычно более загружен, рекомендуется использовать hn1. Используйте этот параметр при запуске сценария hello $0 как действие сценария с портала HDInsight hello или Azure PowerShell.|
|-ip | Этот аргумент является обязательным, если вы включаете репликацию между двумя виртуальными сетями. Данный аргумент действует как переключатель toouse hello статические IP-адреса ZooKeeper узлы из кластеров реплики, а не полные ДОМЕННЫЕ имена. Hello статического IP-адреса должны toobe, заранее настроенный перед включением репликации. |
|-cp, -copydata | Включите hello миграцию существующих данных в таблицах hello, где включена репликация. |
|-rpm, -replicate-phoenix-meta | Включает репликацию для системных таблиц Phoenix. <br><br>*Используйте этот параметр с осторожностью.* Рекомендуется повторно создать таблицы Phoenix в реплицированных кластерах перед использованием этого скрипта. |
|-h, --help | Отображает сведения об использовании. |

Здравствуйте, раздел print_usage() hello [сценарий](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) дано подробное описание параметров.

После hello скрипт действии успешно развернута, можно использовать кластер HBase назначения toohello tooconnect SSH и убедитесь, что были реплицированы данные hello.

### <a name="replication-scenarios"></a>Сценарии репликации

Hello следующем списке перечислены некоторые общие способы применения и настройки их параметров.

- **Включение репликации для всех таблиц между кластерами hello двух**. В этом сценарии требуется копировать hello/миграции существующих данных в таблицах hello и не использует Финиксе таблиц. Используйте hello следующие параметры:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- **Включение репликации для отдельных таблиц.** Используйте следующие параметры репликации tooenable на table1, table2 и Таблица3 hello.

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- **Включение репликации для отдельных таблиц и копировать существующие данные hello**. Используйте следующие параметры репликации tooenable на table1, table2 и Таблица3 hello.

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- **Включение репликации для всех таблиц с помощью репликации Финиксе метаданных из источника toodestination**. Репликация метаданных Phoenix работает не идеально, ее следует использовать с осторожностью.

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a>Копирование и перенос данных

Существует два отдельных скрипта действия сценария для копирования или переноса данных после включения репликации:

- [Скрипт для небольших таблиц](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (несколько гигабайт копирования размер, а также общем — ожидаемое toofinish менее чем за один час)

- [Скрипт для больших таблиц](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (требуется больше времени, чем один час toocopy tootake)

Можно выполнить hello же процедуру в [включить репликацию](#enable-replication) действие сценария hello toocall с hello следующие параметры:

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

Здравствуйте, раздел print_usage() hello [сценарий](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) содержит подробное описание параметров.

### <a name="scenarios"></a>Сценарии

- **Копирование определенных таблиц (test1, test2 и test3) для всех строк, измененных до настоящего момента (текущая отметка времени):**

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  или

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- **Копирование определенных таблиц с указанным интервалом времени:**

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a>Отключение репликации

репликация toodisable, используйте другой сценарий действия сценария, расположенный в [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh). Можно выполнить hello же процедуру в [включить репликацию](#enable-replication) действие сценария hello toocall с hello следующие параметры:

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

Здравствуйте, раздел print_usage() hello [сценарий](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) дано подробное описание параметров.

### <a name="scenarios"></a>Сценарии

- **Отключение репликации для всех таблиц:**

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  или

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- **Отключение репликации для определенных таблиц (table1, table2 и table3):**

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике вы узнали, как tooconfigure HBase репликации между двумя центрами обработки данных. toolearn Дополнительные сведения о HDInsight и HBase, см.:

* [Руководство по HBase. Приступая к работе с Apache HBase на Hadoop под управлением Windows в HDInsight][hdinsight-hbase-get-started]
* [Что такое HBase в HDInsight: база данных NoSQL, которая предоставляет возможности, схожие с BigTable, для Hadoop][hdinsight-hbase-overview]
* [Создание кластеров HBase в виртуальной сети Azure][hdinsight-hbase-provision-vnet]
* [Анализ мнений пользователей Twitter в режиме реального времени с использованием HBase в HDInsight][hdinsight-hbase-twitter-sentiment]
* [Анализ полученных с датчиков данных с использованием Apache Storm, концентратора событий и базы данных HBase в службе HDInsight (Hadoop)][hdinsight-sensor-data]

[hdinsight-hbase-geo-replication-vnet]: hdinsight-hbase-geo-replication-configure-vnets.md
[hdinsight-hbase-geo-replication-dns]: ../hdinsight-hbase-geo-replication-configure-VNet.md


[img-vnet-diagram]: ./media/hdinsight-hbase-geo-replication/HDInsight.HBase.Replication.Network.diagram.png

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[hdinsight-sensor-data]: hdinsight-storm-sensor-data-analysis.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
