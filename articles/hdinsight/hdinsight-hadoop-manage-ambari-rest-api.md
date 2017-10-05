---
title: "Мониторинг и управление Hadoop с помощью Ambari REST API в Azure HDInsight | Документация Майкрософт"
description: "Сведения об использовании Ambari для отслеживания и администрирования кластеров Hadoop в Azure HDInsight. В этом документе рассказывается об использовании интерфейса REST API Ambari, предоставляемого с кластерами HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2400530f-92b3-47b7-aa48-875f028765ff
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 7960d83bce22d4f671d61e9aaf55561bc24308f8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="manage-hdinsight-clusters-by-using-the-ambari-rest-api"></a><span data-ttu-id="495f9-104">Управление кластерами HDInsight с помощью REST API Ambari</span><span class="sxs-lookup"><span data-stu-id="495f9-104">Manage HDInsight clusters by using the Ambari REST API</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="495f9-105">Узнайте, как использовать Ambari REST API для отслеживания и администрирования кластеров Hadoop в Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="495f9-105">Learn how to use the Ambari REST API to manage and monitor Hadoop clusters in Azure HDInsight.</span></span>

<span data-ttu-id="495f9-106">Apache Ambari упрощает управление кластером Hadoop и его мониторинг за счет удобного пользовательского веб-интерфейса и интерфейса REST API.</span><span class="sxs-lookup"><span data-stu-id="495f9-106">Apache Ambari simplifies the management and monitoring of a Hadoop cluster by providing an easy to use web UI and REST API.</span></span> <span data-ttu-id="495f9-107">Ambari предоставляется с кластерами HDInsight, которые работают под управлением операционной системы Linux.</span><span class="sxs-lookup"><span data-stu-id="495f9-107">Ambari is included on HDInsight clusters that use the Linux operating system.</span></span> <span data-ttu-id="495f9-108">Ambari можно использовать для мониторинга кластера и внесения изменений в его конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="495f9-108">You can use Ambari to monitor the cluster and make configuration changes.</span></span>

## <span data-ttu-id="495f9-109"><a id="whatis"></a>Что такое Ambari</span><span class="sxs-lookup"><span data-stu-id="495f9-109"><a id="whatis"></a>What is Ambari</span></span>

<span data-ttu-id="495f9-110">[Apache Ambari](http://ambari.apache.org) предоставляет веб-интерфейс, который можно использовать для подготовки и мониторинга кластеров Hadoop, а также управления их функционированием.</span><span class="sxs-lookup"><span data-stu-id="495f9-110">[Apache Ambari](http://ambari.apache.org) provides web UI that can be used to provision, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="495f9-111">Разработчики могут интегрировать эти возможности в своих приложениях с помощью [интерфейсов REST API Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="495f9-111">Developers can integrate these capabilities into their applications by using the [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="495f9-112">Ambari предоставляется по умолчанию с кластерами HDInsight на платформе Linux.</span><span class="sxs-lookup"><span data-stu-id="495f9-112">Ambari is provided by default with Linux-based HDInsight clusters.</span></span>

## <a name="how-to-use-the-ambari-rest-api"></a><span data-ttu-id="495f9-113">Как использовать интерфейс REST API Ambari</span><span class="sxs-lookup"><span data-stu-id="495f9-113">How to use the Ambari REST API</span></span>

> [!IMPORTANT]
> <span data-ttu-id="495f9-114">Чтобы использовать сведения и примеры, описанные в этом документе, нужен кластер HDInsight с операционной системой Linux.</span><span class="sxs-lookup"><span data-stu-id="495f9-114">The information and examples in this document require an HDInsight cluster that uses Linux operating system.</span></span> <span data-ttu-id="495f9-115">Дополнительные сведения см. в статье [Руководство по Hadoop. Приступая к работе с Hadoop в HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="495f9-115">For more information, see [Get started with HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

<span data-ttu-id="495f9-116">Этот документ содержит примеры для оболочек Bourne (Bash) и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="495f9-116">The examples in this document are provided for both the Bourne shell (bash) and PowerShell.</span></span> <span data-ttu-id="495f9-117">Примеры Bash протестированы с помощью GNU Bash 4.3.11, но они должны работать и с другими оболочками Unix.</span><span class="sxs-lookup"><span data-stu-id="495f9-117">The bash examples were tested with GNU bash 4.3.11, but should work with other Unix shells.</span></span> <span data-ttu-id="495f9-118">Примеры PowerShell проверялись с помощью PowerShell 5.0, но они должны работать с PowerShell 3.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="495f9-118">The PowerShell examples were tested with PowerShell 5.0, but should work with PowerShell 3.0 or higher.</span></span>

<span data-ttu-id="495f9-119">Если вы используете __оболочку Bourne__ (Bash), установите следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="495f9-119">If using the __Bourne shell__ (Bash), you must have the following installed:</span></span>

* <span data-ttu-id="495f9-120">[cURL](http://curl.haxx.se/) — это служебная программа для работы с интерфейсами REST API из командной строки.</span><span class="sxs-lookup"><span data-stu-id="495f9-120">[cURL](http://curl.haxx.se/): cURL is a utility that can be used to work with REST APIs from the command line.</span></span> <span data-ttu-id="495f9-121">В этом документе она используется для взаимодействия с REST API Ambari.</span><span class="sxs-lookup"><span data-stu-id="495f9-121">In this document, it is used to communicate with the Ambari REST API.</span></span>

<span data-ttu-id="495f9-122">Если вы используете Bash или PowerShell, установите также [jq](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="495f9-122">Whether using Bash or PowerShell, you must also have [jq](https://stedolan.github.io/jq/) installed.</span></span> <span data-ttu-id="495f9-123">jq — это служебная программа для работы с документами JSON.</span><span class="sxs-lookup"><span data-stu-id="495f9-123">Jq is a utility for working with JSON documents.</span></span> <span data-ttu-id="495f9-124">Она используется во **всех** примерах Bash и в **одном** примере PowerShell.</span><span class="sxs-lookup"><span data-stu-id="495f9-124">It is used in **all** the Bash examples, and **one** of the PowerShell examples.</span></span>

### <a name="base-uri-for-ambari-rest-api"></a><span data-ttu-id="495f9-125">Базовый универсальный код ресурса для REST API Ambari</span><span class="sxs-lookup"><span data-stu-id="495f9-125">Base URI for Ambari Rest API</span></span>

<span data-ttu-id="495f9-126">Базовый универсальный код ресурса (URI) для REST API Ambari в кластерах HDInsight выглядит следующим образом: https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, где **CLUSTERNAME** — это имя вашего кластера.</span><span class="sxs-lookup"><span data-stu-id="495f9-126">The base URI for the Ambari REST API on HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="495f9-127">Хотя имя кластера в полном доменном имени в URI (CLUSTERNAME.azurehdinsight.net) указывается без учета регистра, другие вхождения этого URI учитывают регистр.</span><span class="sxs-lookup"><span data-stu-id="495f9-127">While the cluster name in the fully qualified domain name (FQDN) part of the URI (CLUSTERNAME.azurehdinsight.net) is case-insensitive, other occurrences in the URI are case-sensitive.</span></span> <span data-ttu-id="495f9-128">Например, если кластер называется `MyCluster`, допустимые URI выглядят так:</span><span class="sxs-lookup"><span data-stu-id="495f9-128">For example, if your cluster is named `MyCluster`, the following are valid URIs:</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> <span data-ttu-id="495f9-129">Приведенные ниже URI возвратят ошибку, так как второе вхождение имени имеет неправильный регистр.</span><span class="sxs-lookup"><span data-stu-id="495f9-129">The following URIs return an error because the second occurrence of the name is not the correct case.</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a><span data-ttu-id="495f9-130">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="495f9-130">Authentication</span></span>

<span data-ttu-id="495f9-131">Подключение к Ambari в HDInsight выполняется по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="495f9-131">Connecting to Ambari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="495f9-132">Используйте имя учетной записи администратора (по умолчанию — **admin**) и пароль, указанные при создании кластера.</span><span class="sxs-lookup"><span data-stu-id="495f9-132">Use the admin account name (the default is **admin**) and password you provided during cluster creation.</span></span>

## <a name="examples-authentication-and-parsing-json"></a><span data-ttu-id="495f9-133">Примеры. Проверка подлинности и анализ JSON</span><span class="sxs-lookup"><span data-stu-id="495f9-133">Examples: Authentication and parsing JSON</span></span>

<span data-ttu-id="495f9-134">В следующих примерах показано, как отправить запрос GET к базовому интерфейсу REST API Ambari:</span><span class="sxs-lookup"><span data-stu-id="495f9-134">The following examples demonstrate how to make a GET request against the base Ambari REST API:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> <span data-ttu-id="495f9-135">Примеры Bash в этом документе основаны на следующих допущениях.</span><span class="sxs-lookup"><span data-stu-id="495f9-135">The Bash examples in this document make the following assumptions:</span></span>
>
> * <span data-ttu-id="495f9-136">Имя входа в кластер по умолчанию имеет значение `admin`.</span><span class="sxs-lookup"><span data-stu-id="495f9-136">The login name for the cluster is the default value of `admin`.</span></span>
> * <span data-ttu-id="495f9-137">`$PASSWORD` содержит пароль для команды входа HDInsight.</span><span class="sxs-lookup"><span data-stu-id="495f9-137">`$PASSWORD` contains the password for the HDInsight login command.</span></span> <span data-ttu-id="495f9-138">Это значение можно задать с помощью команды `PASSWORD='mypassword'`.</span><span class="sxs-lookup"><span data-stu-id="495f9-138">You can set this value by using `PASSWORD='mypassword'`.</span></span>
> * <span data-ttu-id="495f9-139">`$CLUSTERNAME` содержит имя кластера.</span><span class="sxs-lookup"><span data-stu-id="495f9-139">`$CLUSTERNAME` contains the name of the cluster.</span></span> <span data-ttu-id="495f9-140">Это значение можно задать с помощью команды `set CLUSTERNAME='clustername'`.</span><span class="sxs-lookup"><span data-stu-id="495f9-140">You can set this value by using `set CLUSTERNAME='clustername'`</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> <span data-ttu-id="495f9-141">Примеры PowerShell в этом документе основаны на следующих допущениях.</span><span class="sxs-lookup"><span data-stu-id="495f9-141">The PowerShell examples in this document make the following assumptions:</span></span>
>
> * <span data-ttu-id="495f9-142">`$creds` — объект учетных данных, который содержит имя входа администратора и пароль для кластера.</span><span class="sxs-lookup"><span data-stu-id="495f9-142">`$creds` is a credential object that contains the admin login and password for the cluster.</span></span> <span data-ttu-id="495f9-143">Это значение можно задать с помощью команды `$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"`, а затем указать учетные данные при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="495f9-143">You can set this value by using `$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"` and providing the credentials when prompted.</span></span>
> * <span data-ttu-id="495f9-144">`$clusterName` — строка, которая содержит имя кластера.</span><span class="sxs-lookup"><span data-stu-id="495f9-144">`$clusterName` is a string that contains the name of the cluster.</span></span> <span data-ttu-id="495f9-145">Это значение можно задать с помощью команды `$clusterName="clustername"`.</span><span class="sxs-lookup"><span data-stu-id="495f9-145">You can set this value by using `$clusterName="clustername"`.</span></span>

<span data-ttu-id="495f9-146">Оба примера возвращают документ JSON, который начинается со следующих сведений:</span><span class="sxs-lookup"><span data-stu-id="495f9-146">Both examples return a JSON document that begins with information similar to the following example:</span></span>

```json
{
"href" : "http://10.0.0.10:8080/api/v1/clusters/CLUSTERNAME",
"Clusters" : {
    "cluster_id" : 2,
    "cluster_name" : "CLUSTERNAME",
    "health_report" : {
    "Host/stale_config" : 0,
    "Host/maintenance_state" : 0,
    "Host/host_state/HEALTHY" : 7,
    "Host/host_state/UNHEALTHY" : 0,
    "Host/host_state/HEARTBEAT_LOST" : 0,
    "Host/host_state/INIT" : 0,
    "Host/host_status/HEALTHY" : 7,
    "Host/host_status/UNHEALTHY" : 0,
    "Host/host_status/UNKNOWN" : 0,
    "Host/host_status/ALERT" : 0
    ...
```

### <a name="parsing-json-data"></a><span data-ttu-id="495f9-147">Анализ данных JSON</span><span class="sxs-lookup"><span data-stu-id="495f9-147">Parsing JSON data</span></span>

<span data-ttu-id="495f9-148">В следующем примере используется программа `jq` для анализа документа ответа JSON и отображения из результатов только сведений `health_report`.</span><span class="sxs-lookup"><span data-stu-id="495f9-148">The following example uses `jq` to parse the JSON response document and display only the `health_report` information from the results.</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

<span data-ttu-id="495f9-149">В PowerShell 3.0 и более поздних версий доступен командлет `ConvertFrom-Json`, преобразующий документ JSON в объект, который лучше работает с PowerShell.</span><span class="sxs-lookup"><span data-stu-id="495f9-149">PowerShell 3.0 and higher provides the `ConvertFrom-Json` cmdlet, which converts the JSON document into an object that is easier to work with from PowerShell.</span></span> <span data-ttu-id="495f9-150">В следующем примере используется программа `ConvertFrom-Json` для отображения из результатов только сведений `health_report`.</span><span class="sxs-lookup"><span data-stu-id="495f9-150">The following example uses `ConvertFrom-Json` to display only the `health_report` information from the results.</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> <span data-ttu-id="495f9-151">Хотя большинство примеров в этом документе используют `ConvertFrom-Json` для отображения элементов из документа ответа, пример [конфигурации обновления Ambari ](#example-update-ambari-configuration) использует jq.</span><span class="sxs-lookup"><span data-stu-id="495f9-151">While most examples in this document use `ConvertFrom-Json` to display elements from the response document, the [Update Ambari configuration](#example-update-ambari-configuration) example uses jq.</span></span> <span data-ttu-id="495f9-152">jq используется в этом примере для создания нового шаблона из документа ответа JSON.</span><span class="sxs-lookup"><span data-stu-id="495f9-152">Jq is used in this example to construct a new template from the JSON response document.</span></span>

<span data-ttu-id="495f9-153">Полный справочник по REST API см. [здесь](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="495f9-153">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

## <a name="example-get-the-fqdn-of-cluster-nodes"></a><span data-ttu-id="495f9-154">Пример. Получение полного доменного имени для узлов кластера</span><span class="sxs-lookup"><span data-stu-id="495f9-154">Example: Get the FQDN of cluster nodes</span></span>

<span data-ttu-id="495f9-155">При работе с HDInsight вам может потребоваться полное доменное имя (FQDN) узла кластера.</span><span class="sxs-lookup"><span data-stu-id="495f9-155">When working with HDInsight, you may need to know the fully qualified domain name (FQDN) of a cluster node.</span></span> <span data-ttu-id="495f9-156">FQDN можно легко получить для разных узлов в кластере с помощью следующих команд.</span><span class="sxs-lookup"><span data-stu-id="495f9-156">You can easily retrieve the FQDN for the various nodes in the cluster using the following examples:</span></span>

* <span data-ttu-id="495f9-157">**Все узлы**</span><span class="sxs-lookup"><span data-stu-id="495f9-157">**All nodes**</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" \
    | jq '.items[].Hosts.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.Hosts.host_name
    ```

* <span data-ttu-id="495f9-158">**Головные узлы**</span><span class="sxs-lookup"><span data-stu-id="495f9-158">**Head nodes**</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HDFS/components/NAMENODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/NAMENODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* <span data-ttu-id="495f9-159">**Рабочие узлы**</span><span class="sxs-lookup"><span data-stu-id="495f9-159">**Worker nodes**</span></span>

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/DATANODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/DATANODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* <span data-ttu-id="495f9-160">**Узлы Zookeeper**</span><span class="sxs-lookup"><span data-stu-id="495f9-160">**Zookeeper nodes**</span></span>

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

## <a name="example-get-the-internal-ip-address-of-cluster-nodes"></a><span data-ttu-id="495f9-161">Пример. Получение внутреннего IP-адреса узлов кластера</span><span class="sxs-lookup"><span data-stu-id="495f9-161">Example: Get the internal IP address of cluster nodes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="495f9-162">IP-адреса, возвращенные в примерах из этого раздела, недоступны напрямую через Интернет.</span><span class="sxs-lookup"><span data-stu-id="495f9-162">The IP addresses returned by the examples in this section are not directly accessible over the internet.</span></span> <span data-ttu-id="495f9-163">Они доступны только в пределах виртуальной сети Azure, содержащей кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="495f9-163">They are only accessible within the Azure Virtual Network that contains the HDInsight cluster.</span></span>
>
> <span data-ttu-id="495f9-164">Дополнительные сведения о работе с виртуальными сетями и HDInsight см. в статье [Расширение возможностей HDInsight с помощью виртуальной сети Azure](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="495f9-164">For more information on working with HDInsight and virtual networks, see [Extend HDInsight capabilities by using a custom Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

<span data-ttu-id="495f9-165">Чтобы найти IP-адрес, необходимо знать внутренние полные доменные имена (FQDN) узлов кластера.</span><span class="sxs-lookup"><span data-stu-id="495f9-165">To find the IP address, you must know the internal fully qualified domain name (FQDN) of the cluster nodes.</span></span> <span data-ttu-id="495f9-166">Если у вас есть полное доменное имя, вы можете получить IP-адрес узла.</span><span class="sxs-lookup"><span data-stu-id="495f9-166">Once you have the FQDN, you can then get the IP address of the host.</span></span> <span data-ttu-id="495f9-167">В следующих примерах у Ambari сначала запрашивается полное доменное имя для всех узлов, а затем — IP-адрес каждого узла.</span><span class="sxs-lookup"><span data-stu-id="495f9-167">The following examples first query Ambari for the FQDN of all the host nodes, then query Ambari for the IP address of each host.</span></span>

```bash
for HOSTNAME in $(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" | jq -r '.items[].Hosts.host_name')
do
    IP=$(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts/$HOSTNAME" | jq -r '.Hosts.ip')
  echo "$HOSTNAME <--> $IP"
done
```

```powershell
$uri = "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts"
$resp = Invoke-WebRequest -Uri $uri -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
foreach($item in $respObj.items) {
    $hostName = [string]$item.Hosts.host_name
    $hostInfoResp = Invoke-WebRequest -Uri "$uri/$hostName" `
        -Credential $creds
    $hostInfoObj = ConvertFrom-Json $hostInfoResp 
    $hostIp = $hostInfoObj.Hosts.ip
    "$hostName <--> $hostIp"
}
```

## <a name="example-get-the-default-storage"></a><span data-ttu-id="495f9-168">Пример. Получение хранилища по умолчанию</span><span class="sxs-lookup"><span data-stu-id="495f9-168">Example: Get the default storage</span></span>

<span data-ttu-id="495f9-169">При создании кластера HDInsight в качестве хранилища по умолчанию для кластера необходимо использовать учетную запись хранения Azure или Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="495f9-169">When you create an HDInsight cluster, you must use an Azure Storage Account or Data Lake Store as the default storage for the cluster.</span></span> <span data-ttu-id="495f9-170">Для получения этой информации после создания кластера можно использовать Ambari.</span><span class="sxs-lookup"><span data-stu-id="495f9-170">You can use Ambari to retrieve this information after the cluster has been created.</span></span> <span data-ttu-id="495f9-171">Например, если нужно выполнить операции чтения или записи в контейнере за пределами HDInsight.</span><span class="sxs-lookup"><span data-stu-id="495f9-171">For example, if you want to read/write data to the container outside HDInsight.</span></span>

<span data-ttu-id="495f9-172">Следующие примеры извлекают конфигурацию хранилища, используемого в кластере по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="495f9-172">The following examples retrieve the default storage configuration from the cluster:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
| jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'
```

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties.'fs.defaultFS'
```

> [!IMPORTANT]
> <span data-ttu-id="495f9-173">Эти примеры возвращают первую конфигурацию, применяемую к серверу (`service_config_version=1`), который содержит эти сведения.</span><span class="sxs-lookup"><span data-stu-id="495f9-173">These examples return the first configuration applied to the server (`service_config_version=1`) which contains this information.</span></span> <span data-ttu-id="495f9-174">Чтобы получить значение, которое было изменено после создания кластера, может потребоваться перечислить версии конфигурации и получить последнюю из них.</span><span class="sxs-lookup"><span data-stu-id="495f9-174">If you retrieve a value that has been modified after cluster creation, you may need to list the configuration versions and retrieve the latest one.</span></span>

<span data-ttu-id="495f9-175">Возвращаемое значение будет выглядеть, как один из следующих примеров:</span><span class="sxs-lookup"><span data-stu-id="495f9-175">The return value is similar to one of the following examples:</span></span>

* <span data-ttu-id="495f9-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` — это значение указывает, что кластер использует учетную запись хранения Azure в качестве хранилища по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="495f9-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - This value indicates that the cluster is using an Azure Storage account for default storage.</span></span> <span data-ttu-id="495f9-177">Значение `ACCOUNTNAME` — имя учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="495f9-177">The `ACCOUNTNAME` value is the name of the storage account.</span></span> <span data-ttu-id="495f9-178">Часть `CONTAINER` — это имя контейнера больших двоичных объектов в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="495f9-178">The `CONTAINER` portion is the name of the blob container in the storage account.</span></span> <span data-ttu-id="495f9-179">Контейнер является корнем совместимого хранилища HDFS для кластера.</span><span class="sxs-lookup"><span data-stu-id="495f9-179">The container is the root of the HDFS compatible storage for the cluster.</span></span>

* <span data-ttu-id="495f9-180">`adl://home` — это значение указывает, что кластер использует Azure Data Lake Store в качестве хранилища по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="495f9-180">`adl://home` - This value indicates that the cluster is using an Azure Data Lake Store for default storage.</span></span>

    <span data-ttu-id="495f9-181">Чтобы найти имя учетной записи Data Lake Store, используйте следующие примеры:</span><span class="sxs-lookup"><span data-stu-id="495f9-181">To find the Data Lake Store account name, use the following examples:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.hostname'
    ```

    <span data-ttu-id="495f9-182">Возвращается похожее значение: `ACCOUNTNAME.azuredatalakestore.net`, где `ACCOUNTNAME` — имя учетной записи Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="495f9-182">The return value is similar to `ACCOUNTNAME.azuredatalakestore.net`, where `ACCOUNTNAME` is the name of the Data Lake Store account.</span></span>

    <span data-ttu-id="495f9-183">Чтобы найти каталог в Data Lake Store, содержащий хранилище кластера, используйте следующие примеры:</span><span class="sxs-lookup"><span data-stu-id="495f9-183">To find the directory within Data Lake Store that contains the storage for the cluster, use the following examples:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.mountpoint'
    ```

    <span data-ttu-id="495f9-184">Вернется похожее значение: `/clusters/CLUSTERNAME/`.</span><span class="sxs-lookup"><span data-stu-id="495f9-184">The return value is similar to `/clusters/CLUSTERNAME/`.</span></span> <span data-ttu-id="495f9-185">Это значение представляет путь в учетной записи Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="495f9-185">This value is a path within the Data Lake Store account.</span></span> <span data-ttu-id="495f9-186">Путь является корнем совместимой файловой системы HDFS для кластера.</span><span class="sxs-lookup"><span data-stu-id="495f9-186">This path is the root of the HDFS compatible file system for the cluster.</span></span> 

> [!NOTE]
> <span data-ttu-id="495f9-187">Командлет `Get-AzureRmHDInsightCluster`, доступный в [Azure PowerShell](/powershell/azure/overview), также возвращает сведения о хранилище для кластера.</span><span class="sxs-lookup"><span data-stu-id="495f9-187">The `Get-AzureRmHDInsightCluster` cmdlet provided by [Azure PowerShell](/powershell/azure/overview) also returns the storage information for the cluster.</span></span>


## <a name="example-get-configuration"></a><span data-ttu-id="495f9-188">Пример. Получение конфигурации</span><span class="sxs-lookup"><span data-stu-id="495f9-188">Example: Get configuration</span></span>

1. <span data-ttu-id="495f9-189">Получите конфигурации, которые доступны для кластера.</span><span class="sxs-lookup"><span data-stu-id="495f9-189">Get the configurations that are available for your cluster.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    <span data-ttu-id="495f9-190">Этот пример возвращает документ JSON с текущей конфигурацией (идентифицируется по значению *tag*) для компонентов, установленных в кластере.</span><span class="sxs-lookup"><span data-stu-id="495f9-190">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span></span> <span data-ttu-id="495f9-191">Ниже приведен пример фрагмента данных, возвращаемых из типа кластера Spark.</span><span class="sxs-lookup"><span data-stu-id="495f9-191">The following example is an excerpt from the data returned from a Spark cluster type.</span></span>
   
   ```json
   "spark-metrics-properties" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-fairscheduler" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-sparkconf" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   }
   ```

2. <span data-ttu-id="495f9-192">Извлеките конфигурацию для интересующего вас компонента.</span><span class="sxs-lookup"><span data-stu-id="495f9-192">Get the configuration for the component that you are interested in.</span></span> <span data-ttu-id="495f9-193">В следующем примере замените `INITIAL` значением тега, возвращенным из предыдущего запроса.</span><span class="sxs-lookup"><span data-stu-id="495f9-193">In the following example, replace `INITIAL` with the tag value returned from the previous request.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    <span data-ttu-id="495f9-194">Этот пример возвращает документ JSON, содержащий текущую конфигурацию для компонента `core-site`.</span><span class="sxs-lookup"><span data-stu-id="495f9-194">This example returns a JSON document containing the current configuration for the `core-site` component.</span></span>

## <a name="example-update-configuration"></a><span data-ttu-id="495f9-195">Пример. Обновление конфигурации</span><span class="sxs-lookup"><span data-stu-id="495f9-195">Example: Update configuration</span></span>

1. <span data-ttu-id="495f9-196">Получите текущую конфигурацию, которую Ambari хранит в виде "требуемой конфигурации":</span><span class="sxs-lookup"><span data-stu-id="495f9-196">Get the current configuration, which Ambari stores as the "desired configuration":</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    <span data-ttu-id="495f9-197">Этот пример возвращает документ JSON с текущей конфигурацией (идентифицируется по значению *tag*) для компонентов, установленных в кластере.</span><span class="sxs-lookup"><span data-stu-id="495f9-197">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span></span> <span data-ttu-id="495f9-198">Ниже приведен пример фрагмента данных, возвращаемых из типа кластера Spark.</span><span class="sxs-lookup"><span data-stu-id="495f9-198">The following example is an excerpt from the data returned from a Spark cluster type.</span></span>
   
    ```json
    "spark-metrics-properties" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-fairscheduler" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-sparkconf" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    }
    ```
   
    <span data-ttu-id="495f9-199">Из этого списка нужно скопировать имя компонента (например, **spark\_thrift\_sparkconf**) и значение **tag**.</span><span class="sxs-lookup"><span data-stu-id="495f9-199">From this list, you need to copy the name of the component (for example, **spark\_thrift\_sparkconf** and the **tag** value.</span></span>

2. <span data-ttu-id="495f9-200">Извлеките конфигурацию для компонента и значение tag с помощью следующих команд:</span><span class="sxs-lookup"><span data-stu-id="495f9-200">Retrieve the configuration for the component and tag by using the following commands:</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=spark-thrift-sparkconf&tag=INITIAL" \
    | jq --arg newtag $(echo version$(date +%s%N)) '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    ```powershell
    $epoch = Get-Date -Year 1970 -Month 1 -Day 1 -Hour 0 -Minute 0 -Second 0
    $now = Get-Date
    $unixTimeStamp = [math]::truncate($now.ToUniversalTime().Subtract($epoch).TotalMilliSeconds)
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=spark-thrift-sparkconf&tag=INITIAL" `
        -Credential $creds
    $resp.Content | jq --arg newtag "version$unixTimeStamp" '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    > [!NOTE]
    > <span data-ttu-id="495f9-201">Замените **spark-thrift-sparkconf** и **INITIAL** на компонент и значение tag, по которым хотите получить конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="495f9-201">Replace **spark-thrift-sparkconf** and **INITIAL** with the component and tag that you want to retrieve the configuration for.</span></span>
   
    <span data-ttu-id="495f9-202">jq используется для преобразования данных, извлеченных из HDInsight в новый шаблон конфигурации.</span><span class="sxs-lookup"><span data-stu-id="495f9-202">Jq is used to turn the data retrieved from HDInsight into a new configuration template.</span></span> <span data-ttu-id="495f9-203">В частности, эти примеры выполняют следующие действия.</span><span class="sxs-lookup"><span data-stu-id="495f9-203">Specifically, these examples perform the following actions:</span></span>
   
    * <span data-ttu-id="495f9-204">Создает уникальное значение, содержащее строку version и дату, хранящуюся в `newtag`.</span><span class="sxs-lookup"><span data-stu-id="495f9-204">Creates a unique value containing the string "version" and the date, which is stored in `newtag`.</span></span>

    * <span data-ttu-id="495f9-205">Создает корневой документ для новой требуемой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="495f9-205">Creates a root document for the new desired configuration.</span></span>

    * <span data-ttu-id="495f9-206">Возвращает содержимое массива `.items[]` и добавляет его в элемент **desired_config**.</span><span class="sxs-lookup"><span data-stu-id="495f9-206">Gets the contents of the `.items[]` array and adds it under the **desired_config** element.</span></span>

    * <span data-ttu-id="495f9-207">Удаляет элементы `href`, `version` и `Config`, так как они не нужны для отправки новой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="495f9-207">Deletes the `href`, `version`, and `Config` elements, as these elements aren't needed to submit a new configuration.</span></span>

    * <span data-ttu-id="495f9-208">Добавляет элемент `tag` со значением `version#################`.</span><span class="sxs-lookup"><span data-stu-id="495f9-208">Adds a `tag` element with a value of `version#################`.</span></span> <span data-ttu-id="495f9-209">Числовая часть основана на текущей дате.</span><span class="sxs-lookup"><span data-stu-id="495f9-209">The numeric portion is based on the current date.</span></span> <span data-ttu-id="495f9-210">Каждая конфигурация должна иметь уникальное значение tag.</span><span class="sxs-lookup"><span data-stu-id="495f9-210">Each configuration must have a unique tag.</span></span>
     
    <span data-ttu-id="495f9-211">Наконец, данные сохраняются в документе `newconfig.json`.</span><span class="sxs-lookup"><span data-stu-id="495f9-211">Finally, the data is saved to the `newconfig.json` document.</span></span> <span data-ttu-id="495f9-212">Структура документа должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="495f9-212">The document structure should appear similar to the following example:</span></span>
     
     ```json
    {
        "Clusters": {
            "desired_config": {
            "tag": "version1459260185774265400",
            "type": "spark-thrift-sparkconf",
            "properties": {
                ....
            },
            "properties_attributes": {
                ....
            }
        }
    }
    ```

3. <span data-ttu-id="495f9-213">Откройте документ `newconfig.json` и измените или добавьте значения в объекте `properties`.</span><span class="sxs-lookup"><span data-stu-id="495f9-213">Open the `newconfig.json` document and modify/add values in the `properties` object.</span></span> <span data-ttu-id="495f9-214">Следующий пример изменяет значение `"spark.yarn.am.memory"` с `"1g"` на `"3g"`.</span><span class="sxs-lookup"><span data-stu-id="495f9-214">The following example changes the value of `"spark.yarn.am.memory"` from `"1g"` to `"3g"`.</span></span> <span data-ttu-id="495f9-215">Он также добавляет `"spark.kryoserializer.buffer.max"` со значением `"256m"`.</span><span class="sxs-lookup"><span data-stu-id="495f9-215">It also adds `"spark.kryoserializer.buffer.max"` with a value of `"256m"`.</span></span>
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    <span data-ttu-id="495f9-216">После завершения работы сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="495f9-216">Save the file once you are done making modifications.</span></span>

4. <span data-ttu-id="495f9-217">Выполните следующие команды, чтобы отправить обновленную конфигурацию в Ambari:</span><span class="sxs-lookup"><span data-stu-id="495f9-217">Use the following commands to submit the updated configuration to Ambari.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" -X PUT -d @newconfig.json "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
    ```

    ```powershell
    $newConfig = Get-Content .\newconfig.json
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body $newConfig
    $resp.Content
    ```
   
    <span data-ttu-id="495f9-218">Эти команды передают содержимое файла **newconfig.json** в кластер в качестве новой требуемой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="495f9-218">These commands submit the contents of the **newconfig.json** file to the cluster as the new desired configuration.</span></span> <span data-ttu-id="495f9-219">Запрос возвращает документ JSON.</span><span class="sxs-lookup"><span data-stu-id="495f9-219">The request returns a JSON document.</span></span> <span data-ttu-id="495f9-220">Элемент **versionTag** в этом документе должен совпадать с отправленной версией, а объект **configs** содержит запрошенные изменения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="495f9-220">The **versionTag** element in this document should match the version you submitted, and the **configs** object contains the configuration changes you requested.</span></span>

### <a name="example-restart-a-service-component"></a><span data-ttu-id="495f9-221">Пример. Перезапуск компонента службы</span><span class="sxs-lookup"><span data-stu-id="495f9-221">Example: Restart a service component</span></span>

<span data-ttu-id="495f9-222">На этом этапе веб-интерфейс Ambari указывает на то, что вам необходимо перезапустить службу Spark, чтобы новая конфигурация вступила в силу.</span><span class="sxs-lookup"><span data-stu-id="495f9-222">At this point, if you look at the Ambari web UI, the Spark service indicates that it needs to be restarted before the new configuration can take effect.</span></span> <span data-ttu-id="495f9-223">Для перезапуска службы выполните приведенные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="495f9-223">Use the following steps to restart the service.</span></span>

1. <span data-ttu-id="495f9-224">Выполните следующую команду, чтобы перевести службу Spark в режим обслуживания.</span><span class="sxs-lookup"><span data-stu-id="495f9-224">Use the following to enable maintenance mode for the Spark service:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}'
    $resp.Content
    ```
   
    <span data-ttu-id="495f9-225">Эти команды отправляют документ JSON на сервер, который включает режим обслуживания.</span><span class="sxs-lookup"><span data-stu-id="495f9-225">These commands send a JSON document to the server that turns on maintenance mode.</span></span> <span data-ttu-id="495f9-226">Проверить, находится ли служба в этом режиме, можно с помощью следующего запроса.</span><span class="sxs-lookup"><span data-stu-id="495f9-226">You can verify that the service is now in maintenance mode using the following request:</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK" \
    | jq .ServiceInfo.maintenance_state
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK2" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.ServiceInfo.maintenance_state
    ```
   
    <span data-ttu-id="495f9-227">Возвращается значение `ON`.</span><span class="sxs-lookup"><span data-stu-id="495f9-227">The return value is `ON`.</span></span>

2. <span data-ttu-id="495f9-228">Затем выполните следующую команду, чтобы отключить службу.</span><span class="sxs-lookup"><span data-stu-id="495f9-228">Next, use the following to turn off the service:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}'
    $resp.Content
    ```
    
    <span data-ttu-id="495f9-229">Ответ будет выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="495f9-229">The response is similar to the following example:</span></span>
   
    ```json
    {
        "href" : "http://10.0.0.18:8080/api/v1/clusters/CLUSTERNAME/requests/29",
        "Requests" : {
            "id" : 29,
            "status" : "Accepted"
        }
    }
    ```
    
    > [!IMPORTANT]
    > <span data-ttu-id="495f9-230">Значение `href` , возвращенное этим универсальным кодом ресурса (URI), использует внутренний IP-адрес узла кластера.</span><span class="sxs-lookup"><span data-stu-id="495f9-230">The `href` value returned by this URI is using the internal IP address of the cluster node.</span></span> <span data-ttu-id="495f9-231">Чтобы использовать его извне кластера, замените часть "10.0.0.18:8080" на полное доменное имя кластера.</span><span class="sxs-lookup"><span data-stu-id="495f9-231">To use it from outside the cluster, replace the \`10.0.0.18:8080' portion with the FQDN of the cluster.</span></span> 
    
    <span data-ttu-id="495f9-232">Например, следующие команды получают состояние запроса:</span><span class="sxs-lookup"><span data-stu-id="495f9-232">The following commands retrieve the status of the request:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/requests/29" \
    | jq .Requests.request_status
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/requests/29" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.Requests.request_status
    ```

    <span data-ttu-id="495f9-233">Ответ `COMPLETED` указывает, что запрос завершен.</span><span class="sxs-lookup"><span data-stu-id="495f9-233">A response of `COMPLETED` indicates that the request has finished.</span></span>

3. <span data-ttu-id="495f9-234">После завершения предыдущего запроса используйте следующую команду для запуска службы.</span><span class="sxs-lookup"><span data-stu-id="495f9-234">Once the previous request completes, use the following to start the service.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```
   
    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}'
    ```
    <span data-ttu-id="495f9-235">Теперь служба использует новую конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="495f9-235">The service is now using the new configuration.</span></span>

4. <span data-ttu-id="495f9-236">Наконец, используйте следующую команду для отключения режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="495f9-236">Finally, use the following to turn off maintenance mode.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}'
    ```

## <a name="next-steps"></a><span data-ttu-id="495f9-237">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="495f9-237">Next steps</span></span>

<span data-ttu-id="495f9-238">Полный справочник по REST API см. [здесь](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="495f9-238">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

