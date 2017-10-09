---
title: "aaaMonitor кластеров Hadoop в HDInsight с помощью hello API Ambari — Azure | Документы Microsoft"
description: "Используйте hello Apache Ambari API-интерфейсы для создания, управления и наблюдения за кластерами Hadoop. Оператор интуитивно понятные средства и API-интерфейсы скрыть сложность hello Hadoop."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
editor: cgronlun
manager: jhubbard
ms.assetid: 052135b3-d497-4acc-92ff-71cee49356ff
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: d61a8aae5ddfcd7d44f2e4cc899e0a4da5e5fdcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hadoop-clusters-in-hdinsight-using-hello-ambari-api"></a>Монитор кластеров Hadoop в HDInsight с помощью Ambari API hello
Узнайте, как кластеры toomonitor HDInsight с помощью Ambari API.

> [!NOTE]
> Hello сведения в этой статье используется главным образом для кластеров HDInsight под управлением Windows, которые предоставляет только для чтения версию hello Ambari REST API. Сведения о кластерах под управлением Linux см. в статье [Управление кластерами HDInsight с помощью веб-интерфейса Ambari](hdinsight-hadoop-manage-ambari.md).
> 
> 

## <a name="what-is-ambari"></a>Что такое Ambari?
[Apache Ambari][ambari-home] используется для подготовки, мониторинга кластеров Apache Hadoop и управления ими. Содержит коллекцию интуитивно оператор средств и широкий набор API, которые скрывают сложность hello объекта Hadoop, упрощая операции hello кластеров. Дополнительные сведения об API-интерфейсы hello см. в разделе [Справочник по API Ambari][ambari-api-reference]. 

HDInsight в настоящее время поддерживает только hello Ambari компонент наблюдения. Ambari API 1.0 поддерживается кластерами HDInsight версии 3.0 и 2.1. В этой статье описывается доступ к интерфейсам Ambari API в кластерах HDInsight версии 3.1 и 2.1. Hello ключевое различие между двумя hello — некоторые компоненты hello изменились с введением hello новые возможности (такие как hello сервер журнала заданий). 

**Предварительные требования**

Прежде чем начать работу с учебником, необходимо иметь hello следующих элементов:

* **Рабочая станция с Azure PowerShell**.
* [cURL][curl] (необязательно). tooinstall, в разделе [cURL выпусков и загружаемые файлы][curl-download].
  
  > [!NOTE]
  > Если команда hello перелистывание в Windows, используйте двойные кавычки вместо одного кавычки для значений параметра hello.
  > 
  > 
* **Кластер Azure HDInsight**. Указания по подготовке кластеров см. в статье [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started] или [Создание кластеров Hadoop под управлением Windows в HDInsight][hdinsight-provision]. Необходимы следующие toogo данных в учебнике hello hello.
  
  | Свойство кластера | Имя переменной Azure PowerShell | Значение | Описание |
  | --- | --- | --- | --- |
  |   Имя кластера HDInsight. |$clusterName | |Имя кластера HDInsight Hello. |
  |   Имя пользователя кластера |$clusterUsername | |Имя пользователя кластера указан при создании кластера hello. |
  |   Пароль кластера |$clusterPassword | |Пароль пользователя кластера. |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a>Приступая к работе
Существует несколько способов кластеров HDInsight toomonitor toouse Ambari.

**Использование Azure PowerShell**

Следующий сценарий Azure PowerShell Hello возвращает сведениях задания MapReduce hello *в кластере HDInsight 3.5.*  Hello ключевое различие состоит в том, что мы извлекли этих сведений из службы YARN hello (а не MapReduce).

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

Привет, следующий сценарий PowerShell возвращает сведениях задания MapReduce hello *в кластере HDInsight 2.1*:

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

Hello отобразится следующее.

![Вывод Jobtracker][img-jobtracker-output]

**Использование cURL**

Hello следующий пример возвращает сведения о кластере с помощью перелистывание:

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

Hello отобразится следующее.

    {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/",
     "Clusters":{"cluster_name":"hdi0211v2.azurehdinsight.net","version":"2.1.3.0.432823"},
     "services"[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/hdfs",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"hdfs"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/mapreduce",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"mapreduce"}}],
     "hosts":[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/headnode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/workernode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0.{ClusterDNS}.azurehdinsight.net"}}]}

**В выпуске 10/8/2014 hello**:

Если с помощью Ambari hello конечной точки, «https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}» hello *host_name* поля Возвращает hello полное доменное имя (FQDN) узла hello вместо имени узла hello. До выпуска 10/8/2014 hello, в этом примере возвращается просто «**headnode0**». После выпуска 10/8/2014 hello, вы получаете hello полное доменное имя "**headnode0. {} ClusterDNS} .azurehdinsight .net**«, как показано в предыдущем примере hello. Это изменение было необходимые toofacilitate сценарии, где может развертываться несколько типов кластера (например, HBase и Hadoop) в одной виртуальной сети (VNET). Такая необходимость может возникнуть, например, при использовании HBase в качестве вспомогательной платформы для Hadoop.

## <a name="ambari-monitoring-apis"></a>Интерфейсы Ambari API для мониторинга
Hello следующей таблице перечислены некоторые hello наиболее распространенные Ambari мониторинга вызовов API. Дополнительные сведения о hello API см. в разделе [Справочник по API Ambari][ambari-api-reference].

| Отслеживание вызова API | URI | Описание |
| --- | --- | --- |
| Получение кластеров |`/api/v1/clusters` | |
| Получение сведений о кластере. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |кластеры, службы, узлы |
| Получение служб |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |Службы включают в себя: hdfs, mapreduce |
| Получение сведений о службах. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| Получение компонентов службы |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker |
| Получение сведений о компонентах. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |ServiceComponentInfo, host-components, metrics |
| Получение узлов |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |headnode0, workernode0 |
| Получение сведений об узлах. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| Получение компонентов узлов |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |namenode, resourcemanager |
| Получение сведений о компонентах узла. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |HostRoles, component, host, metrics |
| Получение конфигураций |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |Типы настройки: core-site, hdfs-site, mapred-site, hive-site |
| Получение сведений о конфигурации. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |Типы настройки: core-site, hdfs-site, mapred-site, hive-site |

## <a name="next-steps"></a>Дальнейшие действия
Теперь вы узнали, как toouse вызывает Ambari мониторинг API. toolearn более, см.:

* [Управление кластерами HDInsight с помощью портала Azure hello][hdinsight-admin-portal]
* [Управление кластерами Hadoop в HDInsight с помощью Azure PowerShell][hdinsight-admin-powershell]
* [Управление кластерами Hadoop в HDInsight с помощью интерфейса командной строки (CLI) Azure][hdinsight-admin-cli]
* [Документация по HDInsight][hdinsight-documentation]
* [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]

[ambari-home]: http://ambari.apache.org/
[ambari-api-reference]: https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[microsoft-hadoop-SDK]: http://hadoopsdk.codeplex.com/wikipage?title=Ambari%20Monitoring%20Client

[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-documentation]: https://docs.microsoft.com/azure/hdinsight/
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[img-jobtracker-output]: ./media/hdinsight-monitor-use-ambari-api/hdi.ambari.monitor.jobtracker.output.png
