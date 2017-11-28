---
title: "Мониторинг кластеров Hadoop в HDInsight с помощью API-интерфейса Ambari — Azure | Документы Майкрософт"
description: "Набор интерфейсов API для Apache Ambari используется для создания, отслеживания кластеров Apache Hadoop и управления ими. Сложность организации Hadoop компенсируется интуитивным дизайном средств управления пользователя и интерфейсов API."
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
ms.openlocfilehash: b6fc2098027690eb76b69b1427f0e9541b8a7a69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-hadoop-clusters-in-hdinsight-using-the-ambari-api"></a><span data-ttu-id="df70c-104">Отслеживание кластеров Hadoop в HDInsight с помощью интерфейса Ambari API</span><span class="sxs-lookup"><span data-stu-id="df70c-104">Monitor Hadoop clusters in HDInsight using the Ambari API</span></span>
<span data-ttu-id="df70c-105">Узнайте, как отслеживать кластеры HDInsight с помощью интерфейсов Ambari API.</span><span class="sxs-lookup"><span data-stu-id="df70c-105">Learn how to monitor HDInsight clusters by using Ambari APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="df70c-106">Информация в этой статье касается преимущественно кластеров HDInsight на платформе Windows, которые предоставляют версию интерфейса API REST Ambari только для чтения.</span><span class="sxs-lookup"><span data-stu-id="df70c-106">The information in this article is primarily for Windows-based HDInsight clusters, which provide a read-only version of the Ambari REST API.</span></span> <span data-ttu-id="df70c-107">Сведения о кластерах под управлением Linux см. в статье [Управление кластерами HDInsight с помощью веб-интерфейса Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="df70c-107">For Linux-based clusters, see [Manage Hadoop clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
> 
> 

## <a name="what-is-ambari"></a><span data-ttu-id="df70c-108">Что такое Ambari?</span><span class="sxs-lookup"><span data-stu-id="df70c-108">What is Ambari?</span></span>
<span data-ttu-id="df70c-109">[Apache Ambari][ambari-home] используется для подготовки, мониторинга кластеров Apache Hadoop и управления ими.</span><span class="sxs-lookup"><span data-stu-id="df70c-109">[Apache Ambari][ambari-home] is used for provisioning, managing, and monitoring Apache Hadoop clusters.</span></span> <span data-ttu-id="df70c-110">Он включает в себя набор удобных средств и надежных интерфейсов API, который упрощают работу с кластерами Hadoop.</span><span class="sxs-lookup"><span data-stu-id="df70c-110">It includes an intuitive collection of operator tools and a robust set of APIs that hide the complexity of Hadoop, simplifying the operation of clusters.</span></span> <span data-ttu-id="df70c-111">Дополнительные сведения об интерфейсах API см. в [справочнике по Ambari API][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="df70c-111">For more information about the APIs, see [Ambari API Reference][ambari-api-reference].</span></span> 

<span data-ttu-id="df70c-112">В настоящее время HDInsight поддерживает только функцию мониторинга Ambari.</span><span class="sxs-lookup"><span data-stu-id="df70c-112">HDInsight currently supports only the Ambari monitoring feature.</span></span> <span data-ttu-id="df70c-113">Ambari API 1.0 поддерживается кластерами HDInsight версии 3.0 и 2.1.</span><span class="sxs-lookup"><span data-stu-id="df70c-113">Ambari API 1.0 is supported by HDInsight version 3.0 and 2.1 clusters.</span></span> <span data-ttu-id="df70c-114">В этой статье описывается доступ к интерфейсам Ambari API в кластерах HDInsight версии 3.1 и 2.1.</span><span class="sxs-lookup"><span data-stu-id="df70c-114">This article covers accessing Ambari APIs on HDInsight version 3.1 and 2.1 clusters.</span></span> <span data-ttu-id="df70c-115">Основное отличие между двумя версиями заключается в замене некоторых компонентов, что позволило обеспечить новые возможности (таких как «История задач сервера»).</span><span class="sxs-lookup"><span data-stu-id="df70c-115">The key difference between the two is that some of the components have changed with the introduction of new capabilities (such as the Job History Server).</span></span> 

<span data-ttu-id="df70c-116">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="df70c-116">**Prerequisites**</span></span>

<span data-ttu-id="df70c-117">Перед началом работы с этим руководством необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="df70c-117">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="df70c-118"><seg>
  **Рабочая станция с Azure PowerShell**.</seg></span><span class="sxs-lookup"><span data-stu-id="df70c-118">**A workstation with Azure PowerShell**.</span></span>
* <span data-ttu-id="df70c-119">[cURL][curl] (необязательно).</span><span class="sxs-lookup"><span data-stu-id="df70c-119">(Optional) [cURL][curl].</span></span> <span data-ttu-id="df70c-120">Чтобы установить cURL, перейдите на страницу [выпусков и скачиваемых файлов][curl-download].</span><span class="sxs-lookup"><span data-stu-id="df70c-120">To install it, see [cURL Releases and Downloads][curl-download].</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="df70c-121">При использовании команды cURL в Windows для значений параметров указывайте двойные кавычки вместо одинарных.</span><span class="sxs-lookup"><span data-stu-id="df70c-121">When use the cURL command in Windows, use double-quotation marks instead of single-quotation marks for the option values.</span></span>
  > 
  > 
* <span data-ttu-id="df70c-122">**Кластер Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="df70c-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="df70c-123">Указания по подготовке кластеров см. в статье [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started] или [Создание кластеров Hadoop под управлением Windows в HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="df70c-123">For instructions about cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="df70c-124">Для прохождения учебника необходимы следующие данные:</span><span class="sxs-lookup"><span data-stu-id="df70c-124">You need the following data to go through the tutorial:</span></span>
  
  | <span data-ttu-id="df70c-125">Свойство кластера</span><span class="sxs-lookup"><span data-stu-id="df70c-125">Cluster property</span></span> | <span data-ttu-id="df70c-126">Имя переменной Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="df70c-126">Azure PowerShell variable name</span></span> | <span data-ttu-id="df70c-127">Значение</span><span class="sxs-lookup"><span data-stu-id="df70c-127">Value</span></span> | <span data-ttu-id="df70c-128">Описание</span><span class="sxs-lookup"><span data-stu-id="df70c-128">Description</span></span> |
  | --- | --- | --- | --- |
  |   <span data-ttu-id="df70c-129">Имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="df70c-129">HDInsight cluster name</span></span> |<span data-ttu-id="df70c-130">$clusterName</span><span class="sxs-lookup"><span data-stu-id="df70c-130">$clusterName</span></span> | |<span data-ttu-id="df70c-131">Это имя вашего кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="df70c-131">The name of your HDInsight cluster.</span></span> |
  |   <span data-ttu-id="df70c-132">Имя пользователя кластера</span><span class="sxs-lookup"><span data-stu-id="df70c-132">Cluster username</span></span> |<span data-ttu-id="df70c-133">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="df70c-133">$clusterUsername</span></span> | |<span data-ttu-id="df70c-134">Имя пользователя кластера, указанное при создании кластера.</span><span class="sxs-lookup"><span data-stu-id="df70c-134">Cluster user name specified when the cluster was created.</span></span> |
  |   <span data-ttu-id="df70c-135">Пароль кластера</span><span class="sxs-lookup"><span data-stu-id="df70c-135">Cluster password</span></span> |<span data-ttu-id="df70c-136">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="df70c-136">$clusterPassword</span></span> | |<span data-ttu-id="df70c-137">Пароль пользователя кластера.</span><span class="sxs-lookup"><span data-stu-id="df70c-137">Cluster user password.</span></span> |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a><span data-ttu-id="df70c-138">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="df70c-138">Jump-start</span></span>
<span data-ttu-id="df70c-139">Существует несколько способов для использования Ambari для отслеживания кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="df70c-139">There are several ways to use Ambari to monitor HDInsight clusters.</span></span>

<span data-ttu-id="df70c-140">**Использование Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="df70c-140">**Use Azure PowerShell**</span></span>

<span data-ttu-id="df70c-141">Ниже приведен сценарий Azure PowerShell для получения данных модуля отслеживания заданий MapReduce *в кластере HDInsight 3.5*.</span><span class="sxs-lookup"><span data-stu-id="df70c-141">The following Azure PowerShell script gets the MapReduce job tracker information *in an HDInsight 3.5 cluster.*</span></span>  <span data-ttu-id="df70c-142">Основное отличие заключается в том, что мы получаем эти данные от службы YARN (а не от MapReduce).</span><span class="sxs-lookup"><span data-stu-id="df70c-142">The key difference is that we pull these details from the YARN service (rather than MapReduce).</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

<span data-ttu-id="df70c-143">Ниже приведен сценарий PowerShell для получения данных модуля отслеживания заданий MapReduce *в кластере HDInsight 2.1*.</span><span class="sxs-lookup"><span data-stu-id="df70c-143">The following PowerShell script gets the MapReduce job tracker information *in an HDInsight 2.1 cluster*:</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

<span data-ttu-id="df70c-144">Результаты:</span><span class="sxs-lookup"><span data-stu-id="df70c-144">The output is:</span></span>

![Вывод Jobtracker][img-jobtracker-output]

<span data-ttu-id="df70c-146">**Использование cURL**</span><span class="sxs-lookup"><span data-stu-id="df70c-146">**Use cURL**</span></span>

<span data-ttu-id="df70c-147">Ниже приведен пример получения сведений о кластере с помощью cURL:</span><span class="sxs-lookup"><span data-stu-id="df70c-147">The following example gets cluster information by using cURL:</span></span>

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

<span data-ttu-id="df70c-148">Результаты:</span><span class="sxs-lookup"><span data-stu-id="df70c-148">The output is:</span></span>

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

<span data-ttu-id="df70c-149">**Примечание к выпуску от 10.8.2014**:</span><span class="sxs-lookup"><span data-stu-id="df70c-149">**For the 10/8/2014 release**:</span></span>

<span data-ttu-id="df70c-150">При использовании конечной точки Ambari https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname} поле *host_name* в настоящее время возвращает полное доменное имя (FQDN) узла вместо имени узла.</span><span class="sxs-lookup"><span data-stu-id="df70c-150">When using the Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", the *host_name* field returns the fully qualified domain name (FQDN) of the node instead of the host name.</span></span> <span data-ttu-id="df70c-151">До выпуска от 08.10.2014 этот пример просто возвращал значение**headnode0**.</span><span class="sxs-lookup"><span data-stu-id="df70c-151">Before the 10/8/2014 release, this example returned simply "**headnode0**".</span></span> <span data-ttu-id="df70c-152">Начиная с выпуска от 08.10.2014 он возвращает полное доменное имя**headnode0.{ClusterDNS}.azurehdinsight.net**, как показано выше.</span><span class="sxs-lookup"><span data-stu-id="df70c-152">After the 10/8/2014 release, you get the FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**", as shown in the previous example.</span></span> <span data-ttu-id="df70c-153">Это изменение было продиктовано необходимостью использовать сценарии, в которых кластеры различного типа, например кластеры HBase и Hadoop, можно было бы размещать в одной виртуальной сети (VNET).</span><span class="sxs-lookup"><span data-stu-id="df70c-153">This change was required to facilitate scenarios where multiple cluster types (such as HBase and Hadoop) can be deployed in one virtual network (VNET).</span></span> <span data-ttu-id="df70c-154">Такая необходимость может возникнуть, например, при использовании HBase в качестве вспомогательной платформы для Hadoop.</span><span class="sxs-lookup"><span data-stu-id="df70c-154">This happens, for example, when using HBase as a back-end platform for Hadoop.</span></span>

## <a name="ambari-monitoring-apis"></a><span data-ttu-id="df70c-155">Интерфейсы Ambari API для мониторинга</span><span class="sxs-lookup"><span data-stu-id="df70c-155">Ambari monitoring APIs</span></span>
<span data-ttu-id="df70c-156">В следующей таблице перечислены некоторые наиболее распространенные вызовы Ambari API для мониторинга.</span><span class="sxs-lookup"><span data-stu-id="df70c-156">The following table lists some of the most common Ambari monitoring API calls.</span></span> <span data-ttu-id="df70c-157">Дополнительные сведения об API см. в [справочнике по Ambari API][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="df70c-157">For more information about the API, see [Ambari API Reference][ambari-api-reference].</span></span>

| <span data-ttu-id="df70c-158">Отслеживание вызова API</span><span class="sxs-lookup"><span data-stu-id="df70c-158">Monitor API call</span></span> | <span data-ttu-id="df70c-159">URI</span><span class="sxs-lookup"><span data-stu-id="df70c-159">URI</span></span> | <span data-ttu-id="df70c-160">Описание</span><span class="sxs-lookup"><span data-stu-id="df70c-160">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="df70c-161">Получение кластеров</span><span class="sxs-lookup"><span data-stu-id="df70c-161">Get clusters</span></span> |`/api/v1/clusters` | |
| <span data-ttu-id="df70c-162">Получение сведений о кластере.</span><span class="sxs-lookup"><span data-stu-id="df70c-162">Get cluster info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |<span data-ttu-id="df70c-163">кластеры, службы, узлы</span><span class="sxs-lookup"><span data-stu-id="df70c-163">clusters, services, hosts</span></span> |
| <span data-ttu-id="df70c-164">Получение служб</span><span class="sxs-lookup"><span data-stu-id="df70c-164">Get services</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |<span data-ttu-id="df70c-165">Службы включают в себя: hdfs, mapreduce</span><span class="sxs-lookup"><span data-stu-id="df70c-165">Services include: hdfs, mapreduce</span></span> |
| <span data-ttu-id="df70c-166">Получение сведений о службах.</span><span class="sxs-lookup"><span data-stu-id="df70c-166">Get services info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| <span data-ttu-id="df70c-167">Получение компонентов службы</span><span class="sxs-lookup"><span data-stu-id="df70c-167">Get service components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |<span data-ttu-id="df70c-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span><span class="sxs-lookup"><span data-stu-id="df70c-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span></span> |
| <span data-ttu-id="df70c-169">Получение сведений о компонентах.</span><span class="sxs-lookup"><span data-stu-id="df70c-169">Get component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |<span data-ttu-id="df70c-170">ServiceComponentInfo, host-components, metrics</span><span class="sxs-lookup"><span data-stu-id="df70c-170">ServiceComponentInfo, host-components, metrics</span></span> |
| <span data-ttu-id="df70c-171">Получение узлов</span><span class="sxs-lookup"><span data-stu-id="df70c-171">Get hosts</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |<span data-ttu-id="df70c-172">headnode0, workernode0</span><span class="sxs-lookup"><span data-stu-id="df70c-172">headnode0, workernode0</span></span> |
| <span data-ttu-id="df70c-173">Получение сведений об узлах.</span><span class="sxs-lookup"><span data-stu-id="df70c-173">Get host info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| <span data-ttu-id="df70c-174">Получение компонентов узлов</span><span class="sxs-lookup"><span data-stu-id="df70c-174">Get host components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |<span data-ttu-id="df70c-175">namenode, resourcemanager</span><span class="sxs-lookup"><span data-stu-id="df70c-175">namenode, resourcemanager</span></span> |
| <span data-ttu-id="df70c-176">Получение сведений о компонентах узла.</span><span class="sxs-lookup"><span data-stu-id="df70c-176">Get host component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |<span data-ttu-id="df70c-177">HostRoles, component, host, metrics</span><span class="sxs-lookup"><span data-stu-id="df70c-177">HostRoles, component, host, metrics</span></span> |
| <span data-ttu-id="df70c-178">Получение конфигураций</span><span class="sxs-lookup"><span data-stu-id="df70c-178">Get configurations</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |<span data-ttu-id="df70c-179">Типы настройки: core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="df70c-179">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |
| <span data-ttu-id="df70c-180">Получение сведений о конфигурации.</span><span class="sxs-lookup"><span data-stu-id="df70c-180">Get configuration info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |<span data-ttu-id="df70c-181">Типы настройки: core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="df70c-181">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |

## <a name="next-steps"></a><span data-ttu-id="df70c-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="df70c-182">Next Steps</span></span>
<span data-ttu-id="df70c-183">Теперь вы узнали, как использовать Ambari API для мониторинга.</span><span class="sxs-lookup"><span data-stu-id="df70c-183">Now you have learned how to use Ambari monitoring API calls.</span></span> <span data-ttu-id="df70c-184">Дополнительные сведения см. на следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="df70c-184">To learn more, see:</span></span>

* <span data-ttu-id="df70c-185">[Управление кластерами Hadoop в HDInsight с помощью портала Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="df70c-185">[Manage HDInsight clusters using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="df70c-186">[Управление кластерами Hadoop в HDInsight с помощью Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="df70c-186">[Manage HDInsight clusters using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="df70c-187">[Управление кластерами Hadoop в HDInsight с помощью интерфейса командной строки (CLI) Azure][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="df70c-187">[Manage HDInsight clusters using command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="df70c-188">[Документация по HDInsight][hdinsight-documentation]</span><span class="sxs-lookup"><span data-stu-id="df70c-188">[HDInsight documentation][hdinsight-documentation]</span></span>
* <span data-ttu-id="df70c-189">[Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="df70c-189">[Get started with HDInsight][hdinsight-get-started]</span></span>

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
