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
# <a name="monitor-hadoop-clusters-in-hdinsight-using-hello-ambari-api"></a><span data-ttu-id="835e1-104">Монитор кластеров Hadoop в HDInsight с помощью Ambari API hello</span><span class="sxs-lookup"><span data-stu-id="835e1-104">Monitor Hadoop clusters in HDInsight using hello Ambari API</span></span>
<span data-ttu-id="835e1-105">Узнайте, как кластеры toomonitor HDInsight с помощью Ambari API.</span><span class="sxs-lookup"><span data-stu-id="835e1-105">Learn how toomonitor HDInsight clusters by using Ambari APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="835e1-106">Hello сведения в этой статье используется главным образом для кластеров HDInsight под управлением Windows, которые предоставляет только для чтения версию hello Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="835e1-106">hello information in this article is primarily for Windows-based HDInsight clusters, which provide a read-only version of hello Ambari REST API.</span></span> <span data-ttu-id="835e1-107">Сведения о кластерах под управлением Linux см. в статье [Управление кластерами HDInsight с помощью веб-интерфейса Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="835e1-107">For Linux-based clusters, see [Manage Hadoop clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
> 
> 

## <a name="what-is-ambari"></a><span data-ttu-id="835e1-108">Что такое Ambari?</span><span class="sxs-lookup"><span data-stu-id="835e1-108">What is Ambari?</span></span>
<span data-ttu-id="835e1-109">[Apache Ambari][ambari-home] используется для подготовки, мониторинга кластеров Apache Hadoop и управления ими.</span><span class="sxs-lookup"><span data-stu-id="835e1-109">[Apache Ambari][ambari-home] is used for provisioning, managing, and monitoring Apache Hadoop clusters.</span></span> <span data-ttu-id="835e1-110">Содержит коллекцию интуитивно оператор средств и широкий набор API, которые скрывают сложность hello объекта Hadoop, упрощая операции hello кластеров.</span><span class="sxs-lookup"><span data-stu-id="835e1-110">It includes an intuitive collection of operator tools and a robust set of APIs that hide hello complexity of Hadoop, simplifying hello operation of clusters.</span></span> <span data-ttu-id="835e1-111">Дополнительные сведения об API-интерфейсы hello см. в разделе [Справочник по API Ambari][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="835e1-111">For more information about hello APIs, see [Ambari API Reference][ambari-api-reference].</span></span> 

<span data-ttu-id="835e1-112">HDInsight в настоящее время поддерживает только hello Ambari компонент наблюдения.</span><span class="sxs-lookup"><span data-stu-id="835e1-112">HDInsight currently supports only hello Ambari monitoring feature.</span></span> <span data-ttu-id="835e1-113">Ambari API 1.0 поддерживается кластерами HDInsight версии 3.0 и 2.1.</span><span class="sxs-lookup"><span data-stu-id="835e1-113">Ambari API 1.0 is supported by HDInsight version 3.0 and 2.1 clusters.</span></span> <span data-ttu-id="835e1-114">В этой статье описывается доступ к интерфейсам Ambari API в кластерах HDInsight версии 3.1 и 2.1.</span><span class="sxs-lookup"><span data-stu-id="835e1-114">This article covers accessing Ambari APIs on HDInsight version 3.1 and 2.1 clusters.</span></span> <span data-ttu-id="835e1-115">Hello ключевое различие между двумя hello — некоторые компоненты hello изменились с введением hello новые возможности (такие как hello сервер журнала заданий).</span><span class="sxs-lookup"><span data-stu-id="835e1-115">hello key difference between hello two is that some of hello components have changed with hello introduction of new capabilities (such as hello Job History Server).</span></span> 

<span data-ttu-id="835e1-116">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="835e1-116">**Prerequisites**</span></span>

<span data-ttu-id="835e1-117">Прежде чем начать работу с учебником, необходимо иметь hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="835e1-117">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="835e1-118">**Рабочая станция с Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="835e1-118">**A workstation with Azure PowerShell**.</span></span>
* <span data-ttu-id="835e1-119">[cURL][curl] (необязательно).</span><span class="sxs-lookup"><span data-stu-id="835e1-119">(Optional) [cURL][curl].</span></span> <span data-ttu-id="835e1-120">tooinstall, в разделе [cURL выпусков и загружаемые файлы][curl-download].</span><span class="sxs-lookup"><span data-stu-id="835e1-120">tooinstall it, see [cURL Releases and Downloads][curl-download].</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="835e1-121">Если команда hello перелистывание в Windows, используйте двойные кавычки вместо одного кавычки для значений параметра hello.</span><span class="sxs-lookup"><span data-stu-id="835e1-121">When use hello cURL command in Windows, use double-quotation marks instead of single-quotation marks for hello option values.</span></span>
  > 
  > 
* <span data-ttu-id="835e1-122">**Кластер Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="835e1-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="835e1-123">Указания по подготовке кластеров см. в статье [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started] или [Создание кластеров Hadoop под управлением Windows в HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="835e1-123">For instructions about cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="835e1-124">Необходимы следующие toogo данных в учебнике hello hello.</span><span class="sxs-lookup"><span data-stu-id="835e1-124">You need hello following data toogo through hello tutorial:</span></span>
  
  | <span data-ttu-id="835e1-125">Свойство кластера</span><span class="sxs-lookup"><span data-stu-id="835e1-125">Cluster property</span></span> | <span data-ttu-id="835e1-126">Имя переменной Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="835e1-126">Azure PowerShell variable name</span></span> | <span data-ttu-id="835e1-127">Значение</span><span class="sxs-lookup"><span data-stu-id="835e1-127">Value</span></span> | <span data-ttu-id="835e1-128">Описание</span><span class="sxs-lookup"><span data-stu-id="835e1-128">Description</span></span> |
  | --- | --- | --- | --- |
  |   <span data-ttu-id="835e1-129">Имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="835e1-129">HDInsight cluster name</span></span> |<span data-ttu-id="835e1-130">$clusterName</span><span class="sxs-lookup"><span data-stu-id="835e1-130">$clusterName</span></span> | |<span data-ttu-id="835e1-131">Имя кластера HDInsight Hello.</span><span class="sxs-lookup"><span data-stu-id="835e1-131">hello name of your HDInsight cluster.</span></span> |
  |   <span data-ttu-id="835e1-132">Имя пользователя кластера</span><span class="sxs-lookup"><span data-stu-id="835e1-132">Cluster username</span></span> |<span data-ttu-id="835e1-133">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="835e1-133">$clusterUsername</span></span> | |<span data-ttu-id="835e1-134">Имя пользователя кластера указан при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="835e1-134">Cluster user name specified when hello cluster was created.</span></span> |
  |   <span data-ttu-id="835e1-135">Пароль кластера</span><span class="sxs-lookup"><span data-stu-id="835e1-135">Cluster password</span></span> |<span data-ttu-id="835e1-136">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="835e1-136">$clusterPassword</span></span> | |<span data-ttu-id="835e1-137">Пароль пользователя кластера.</span><span class="sxs-lookup"><span data-stu-id="835e1-137">Cluster user password.</span></span> |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a><span data-ttu-id="835e1-138">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="835e1-138">Jump-start</span></span>
<span data-ttu-id="835e1-139">Существует несколько способов кластеров HDInsight toomonitor toouse Ambari.</span><span class="sxs-lookup"><span data-stu-id="835e1-139">There are several ways toouse Ambari toomonitor HDInsight clusters.</span></span>

<span data-ttu-id="835e1-140">**Использование Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="835e1-140">**Use Azure PowerShell**</span></span>

<span data-ttu-id="835e1-141">Следующий сценарий Azure PowerShell Hello возвращает сведениях задания MapReduce hello *в кластере HDInsight 3.5.*</span><span class="sxs-lookup"><span data-stu-id="835e1-141">hello following Azure PowerShell script gets hello MapReduce job tracker information *in an HDInsight 3.5 cluster.*</span></span>  <span data-ttu-id="835e1-142">Hello ключевое различие состоит в том, что мы извлекли этих сведений из службы YARN hello (а не MapReduce).</span><span class="sxs-lookup"><span data-stu-id="835e1-142">hello key difference is that we pull these details from hello YARN service (rather than MapReduce).</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

<span data-ttu-id="835e1-143">Привет, следующий сценарий PowerShell возвращает сведениях задания MapReduce hello *в кластере HDInsight 2.1*:</span><span class="sxs-lookup"><span data-stu-id="835e1-143">hello following PowerShell script gets hello MapReduce job tracker information *in an HDInsight 2.1 cluster*:</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

<span data-ttu-id="835e1-144">Hello отобразится следующее.</span><span class="sxs-lookup"><span data-stu-id="835e1-144">hello output is:</span></span>

![Вывод Jobtracker][img-jobtracker-output]

<span data-ttu-id="835e1-146">**Использование cURL**</span><span class="sxs-lookup"><span data-stu-id="835e1-146">**Use cURL**</span></span>

<span data-ttu-id="835e1-147">Hello следующий пример возвращает сведения о кластере с помощью перелистывание:</span><span class="sxs-lookup"><span data-stu-id="835e1-147">hello following example gets cluster information by using cURL:</span></span>

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

<span data-ttu-id="835e1-148">Hello отобразится следующее.</span><span class="sxs-lookup"><span data-stu-id="835e1-148">hello output is:</span></span>

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

<span data-ttu-id="835e1-149">**В выпуске 10/8/2014 hello**:</span><span class="sxs-lookup"><span data-stu-id="835e1-149">**For hello 10/8/2014 release**:</span></span>

<span data-ttu-id="835e1-150">Если с помощью Ambari hello конечной точки, «https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}» hello *host_name* поля Возвращает hello полное доменное имя (FQDN) узла hello вместо имени узла hello.</span><span class="sxs-lookup"><span data-stu-id="835e1-150">When using hello Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", hello *host_name* field returns hello fully qualified domain name (FQDN) of hello node instead of hello host name.</span></span> <span data-ttu-id="835e1-151">До выпуска 10/8/2014 hello, в этом примере возвращается просто «**headnode0**».</span><span class="sxs-lookup"><span data-stu-id="835e1-151">Before hello 10/8/2014 release, this example returned simply "**headnode0**".</span></span> <span data-ttu-id="835e1-152">После выпуска 10/8/2014 hello, вы получаете hello полное доменное имя "**headnode0. {} ClusterDNS} .azurehdinsight .net**«, как показано в предыдущем примере hello.</span><span class="sxs-lookup"><span data-stu-id="835e1-152">After hello 10/8/2014 release, you get hello FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**", as shown in hello previous example.</span></span> <span data-ttu-id="835e1-153">Это изменение было необходимые toofacilitate сценарии, где может развертываться несколько типов кластера (например, HBase и Hadoop) в одной виртуальной сети (VNET).</span><span class="sxs-lookup"><span data-stu-id="835e1-153">This change was required toofacilitate scenarios where multiple cluster types (such as HBase and Hadoop) can be deployed in one virtual network (VNET).</span></span> <span data-ttu-id="835e1-154">Такая необходимость может возникнуть, например, при использовании HBase в качестве вспомогательной платформы для Hadoop.</span><span class="sxs-lookup"><span data-stu-id="835e1-154">This happens, for example, when using HBase as a back-end platform for Hadoop.</span></span>

## <a name="ambari-monitoring-apis"></a><span data-ttu-id="835e1-155">Интерфейсы Ambari API для мониторинга</span><span class="sxs-lookup"><span data-stu-id="835e1-155">Ambari monitoring APIs</span></span>
<span data-ttu-id="835e1-156">Hello следующей таблице перечислены некоторые hello наиболее распространенные Ambari мониторинга вызовов API.</span><span class="sxs-lookup"><span data-stu-id="835e1-156">hello following table lists some of hello most common Ambari monitoring API calls.</span></span> <span data-ttu-id="835e1-157">Дополнительные сведения о hello API см. в разделе [Справочник по API Ambari][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="835e1-157">For more information about hello API, see [Ambari API Reference][ambari-api-reference].</span></span>

| <span data-ttu-id="835e1-158">Отслеживание вызова API</span><span class="sxs-lookup"><span data-stu-id="835e1-158">Monitor API call</span></span> | <span data-ttu-id="835e1-159">URI</span><span class="sxs-lookup"><span data-stu-id="835e1-159">URI</span></span> | <span data-ttu-id="835e1-160">Описание</span><span class="sxs-lookup"><span data-stu-id="835e1-160">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="835e1-161">Получение кластеров</span><span class="sxs-lookup"><span data-stu-id="835e1-161">Get clusters</span></span> |`/api/v1/clusters` | |
| <span data-ttu-id="835e1-162">Получение сведений о кластере.</span><span class="sxs-lookup"><span data-stu-id="835e1-162">Get cluster info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |<span data-ttu-id="835e1-163">кластеры, службы, узлы</span><span class="sxs-lookup"><span data-stu-id="835e1-163">clusters, services, hosts</span></span> |
| <span data-ttu-id="835e1-164">Получение служб</span><span class="sxs-lookup"><span data-stu-id="835e1-164">Get services</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |<span data-ttu-id="835e1-165">Службы включают в себя: hdfs, mapreduce</span><span class="sxs-lookup"><span data-stu-id="835e1-165">Services include: hdfs, mapreduce</span></span> |
| <span data-ttu-id="835e1-166">Получение сведений о службах.</span><span class="sxs-lookup"><span data-stu-id="835e1-166">Get services info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| <span data-ttu-id="835e1-167">Получение компонентов службы</span><span class="sxs-lookup"><span data-stu-id="835e1-167">Get service components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |<span data-ttu-id="835e1-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span><span class="sxs-lookup"><span data-stu-id="835e1-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span></span> |
| <span data-ttu-id="835e1-169">Получение сведений о компонентах.</span><span class="sxs-lookup"><span data-stu-id="835e1-169">Get component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |<span data-ttu-id="835e1-170">ServiceComponentInfo, host-components, metrics</span><span class="sxs-lookup"><span data-stu-id="835e1-170">ServiceComponentInfo, host-components, metrics</span></span> |
| <span data-ttu-id="835e1-171">Получение узлов</span><span class="sxs-lookup"><span data-stu-id="835e1-171">Get hosts</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |<span data-ttu-id="835e1-172">headnode0, workernode0</span><span class="sxs-lookup"><span data-stu-id="835e1-172">headnode0, workernode0</span></span> |
| <span data-ttu-id="835e1-173">Получение сведений об узлах.</span><span class="sxs-lookup"><span data-stu-id="835e1-173">Get host info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| <span data-ttu-id="835e1-174">Получение компонентов узлов</span><span class="sxs-lookup"><span data-stu-id="835e1-174">Get host components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |<span data-ttu-id="835e1-175">namenode, resourcemanager</span><span class="sxs-lookup"><span data-stu-id="835e1-175">namenode, resourcemanager</span></span> |
| <span data-ttu-id="835e1-176">Получение сведений о компонентах узла.</span><span class="sxs-lookup"><span data-stu-id="835e1-176">Get host component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |<span data-ttu-id="835e1-177">HostRoles, component, host, metrics</span><span class="sxs-lookup"><span data-stu-id="835e1-177">HostRoles, component, host, metrics</span></span> |
| <span data-ttu-id="835e1-178">Получение конфигураций</span><span class="sxs-lookup"><span data-stu-id="835e1-178">Get configurations</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |<span data-ttu-id="835e1-179">Типы настройки: core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="835e1-179">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |
| <span data-ttu-id="835e1-180">Получение сведений о конфигурации.</span><span class="sxs-lookup"><span data-stu-id="835e1-180">Get configuration info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |<span data-ttu-id="835e1-181">Типы настройки: core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="835e1-181">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |

## <a name="next-steps"></a><span data-ttu-id="835e1-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="835e1-182">Next Steps</span></span>
<span data-ttu-id="835e1-183">Теперь вы узнали, как toouse вызывает Ambari мониторинг API.</span><span class="sxs-lookup"><span data-stu-id="835e1-183">Now you have learned how toouse Ambari monitoring API calls.</span></span> <span data-ttu-id="835e1-184">toolearn более, см.:</span><span class="sxs-lookup"><span data-stu-id="835e1-184">toolearn more, see:</span></span>

* <span data-ttu-id="835e1-185">[Управление кластерами HDInsight с помощью портала Azure hello][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="835e1-185">[Manage HDInsight clusters using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="835e1-186">[Управление кластерами Hadoop в HDInsight с помощью Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="835e1-186">[Manage HDInsight clusters using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="835e1-187">[Управление кластерами Hadoop в HDInsight с помощью интерфейса командной строки (CLI) Azure][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="835e1-187">[Manage HDInsight clusters using command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="835e1-188">[Документация по HDInsight][hdinsight-documentation]</span><span class="sxs-lookup"><span data-stu-id="835e1-188">[HDInsight documentation][hdinsight-documentation]</span></span>
* <span data-ttu-id="835e1-189">[Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="835e1-189">[Get started with HDInsight][hdinsight-get-started]</span></span>

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
