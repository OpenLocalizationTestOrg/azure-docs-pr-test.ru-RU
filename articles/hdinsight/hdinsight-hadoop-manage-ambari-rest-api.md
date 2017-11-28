---
title: "aaaMonitor и управление Hadoop с помощью API REST Ambari - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse Ambari toomonitor кластеров Hadoop в Azure HDInsight и управления ими. В этом документе вы узнаете, как кластеры hello toouse Ambari API REST, входящий в состав HDInsight."
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
ms.openlocfilehash: 1866a77c8e402231bccbcfba7174253aca41339b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-rest-api"></a><span data-ttu-id="60576-104">Управление кластерами HDInsight с помощью API-интерфейса REST Ambari hello</span><span class="sxs-lookup"><span data-stu-id="60576-104">Manage HDInsight clusters by using hello Ambari REST API</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="60576-105">Узнайте, как toouse hello toomanage Ambari API-Интерфейс REST и наблюдения за кластерами Hadoop в Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="60576-105">Learn how toouse hello Ambari REST API toomanage and monitor Hadoop clusters in Azure HDInsight.</span></span>

<span data-ttu-id="60576-106">Apache Ambari упрощает управление hello и мониторинг кластера Hadoop, предоставляя простой toouse веб-интерфейса пользователя и REST API.</span><span class="sxs-lookup"><span data-stu-id="60576-106">Apache Ambari simplifies hello management and monitoring of a Hadoop cluster by providing an easy toouse web UI and REST API.</span></span> <span data-ttu-id="60576-107">Ambari включается в кластерах HDInsight, использующих операционной системы Linux hello.</span><span class="sxs-lookup"><span data-stu-id="60576-107">Ambari is included on HDInsight clusters that use hello Linux operating system.</span></span> <span data-ttu-id="60576-108">Можно использовать Ambari toomonitor hello кластера и внести изменения в конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="60576-108">You can use Ambari toomonitor hello cluster and make configuration changes.</span></span>

## <span data-ttu-id="60576-109"><a id="whatis"></a>Что такое Ambari</span><span class="sxs-lookup"><span data-stu-id="60576-109"><a id="whatis"></a>What is Ambari</span></span>

<span data-ttu-id="60576-110">[Apache Ambari](http://ambari.apache.org) предоставляет веб-Интерфейс, который может быть используется tooprovision, управления и наблюдения за кластерами Hadoop.</span><span class="sxs-lookup"><span data-stu-id="60576-110">[Apache Ambari](http://ambari.apache.org) provides web UI that can be used tooprovision, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="60576-111">Разработчики могут интегрировать эти возможности в свои приложения с помощью hello [API-интерфейс REST Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="60576-111">Developers can integrate these capabilities into their applications by using hello [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="60576-112">Ambari предоставляется по умолчанию с кластерами HDInsight на платформе Linux.</span><span class="sxs-lookup"><span data-stu-id="60576-112">Ambari is provided by default with Linux-based HDInsight clusters.</span></span>

## <a name="how-toouse-hello-ambari-rest-api"></a><span data-ttu-id="60576-113">Как toouse hello Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="60576-113">How toouse hello Ambari REST API</span></span>

> [!IMPORTANT]
> <span data-ttu-id="60576-114">Hello сведения и примеры в этом документе требуется кластер HDInsight, который использует операционная система Linux.</span><span class="sxs-lookup"><span data-stu-id="60576-114">hello information and examples in this document require an HDInsight cluster that uses Linux operating system.</span></span> <span data-ttu-id="60576-115">Дополнительные сведения см. в статье [Руководство по Hadoop. Приступая к работе с Hadoop в HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="60576-115">For more information, see [Get started with HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

<span data-ttu-id="60576-116">Hello в этом документе приведены примеры для как hello sh (bash) и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60576-116">hello examples in this document are provided for both hello Bourne shell (bash) and PowerShell.</span></span> <span data-ttu-id="60576-117">Hello bash, примеры, были проверены с GNU bash 4.3.11, но должно работать с другими оболочками Unix.</span><span class="sxs-lookup"><span data-stu-id="60576-117">hello bash examples were tested with GNU bash 4.3.11, but should work with other Unix shells.</span></span> <span data-ttu-id="60576-118">Примеры PowerShell Hello были протестированы в PowerShell 5.0, но должны работать вместе с PowerShell 3.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="60576-118">hello PowerShell examples were tested with PowerShell 5.0, but should work with PowerShell 3.0 or higher.</span></span>

<span data-ttu-id="60576-119">При использовании hello __Bourne оболочки__ (Bash), необходимо иметь hello установлены следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="60576-119">If using hello __Bourne shell__ (Bash), you must have hello following installed:</span></span>

* <span data-ttu-id="60576-120">[cURL](http://curl.haxx.se/): перелистывание — это программа, может быть используется toowork с API REST с hello командной строки.</span><span class="sxs-lookup"><span data-stu-id="60576-120">[cURL](http://curl.haxx.se/): cURL is a utility that can be used toowork with REST APIs from hello command line.</span></span> <span data-ttu-id="60576-121">В этом документе это используется toocommunicate с hello Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="60576-121">In this document, it is used toocommunicate with hello Ambari REST API.</span></span>

<span data-ttu-id="60576-122">Если вы используете Bash или PowerShell, установите также [jq](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="60576-122">Whether using Bash or PowerShell, you must also have [jq](https://stedolan.github.io/jq/) installed.</span></span> <span data-ttu-id="60576-123">jq — это служебная программа для работы с документами JSON.</span><span class="sxs-lookup"><span data-stu-id="60576-123">Jq is a utility for working with JSON documents.</span></span> <span data-ttu-id="60576-124">Он используется в **все** hello примеры Bash и **один** примеров PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="60576-124">It is used in **all** hello Bash examples, and **one** of hello PowerShell examples.</span></span>

### <a name="base-uri-for-ambari-rest-api"></a><span data-ttu-id="60576-125">Базовый универсальный код ресурса для REST API Ambari</span><span class="sxs-lookup"><span data-stu-id="60576-125">Base URI for Ambari Rest API</span></span>

<span data-ttu-id="60576-126">Hello базовый URI для hello Ambari API-интерфейса REST на HDInsight — https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, где **CLUSTERNAME** — hello имя кластера.</span><span class="sxs-lookup"><span data-stu-id="60576-126">hello base URI for hello Ambari REST API on HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="60576-127">Хотя полное доменное имя кластера hello в hello часть имени (FQDN) домена hello URI (CLUSTERNAME.azurehdinsight.net) без учета регистра, других экземпляров в hello URI чувствительны к регистру.</span><span class="sxs-lookup"><span data-stu-id="60576-127">While hello cluster name in hello fully qualified domain name (FQDN) part of hello URI (CLUSTERNAME.azurehdinsight.net) is case-insensitive, other occurrences in hello URI are case-sensitive.</span></span> <span data-ttu-id="60576-128">Например, если кластер называется `MyCluster`, hello ниже приведены допустимые URI:</span><span class="sxs-lookup"><span data-stu-id="60576-128">For example, if your cluster is named `MyCluster`, hello following are valid URIs:</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> <span data-ttu-id="60576-129">Hello следующие идентификаторы URI возвращает ошибку, так как hello второго вхождения имени hello не hello исправьте регистр.</span><span class="sxs-lookup"><span data-stu-id="60576-129">hello following URIs return an error because hello second occurrence of hello name is not hello correct case.</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a><span data-ttu-id="60576-130">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="60576-130">Authentication</span></span>

<span data-ttu-id="60576-131">Подключение tooAmbari на HDInsight требуется протокол HTTPS.</span><span class="sxs-lookup"><span data-stu-id="60576-131">Connecting tooAmbari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="60576-132">Имя учетной записи администратора используйте hello (по умолчанию hello — **администратора**) и пароль, указанный во время создания кластера.</span><span class="sxs-lookup"><span data-stu-id="60576-132">Use hello admin account name (hello default is **admin**) and password you provided during cluster creation.</span></span>

## <a name="examples-authentication-and-parsing-json"></a><span data-ttu-id="60576-133">Примеры. Проверка подлинности и анализ JSON</span><span class="sxs-lookup"><span data-stu-id="60576-133">Examples: Authentication and parsing JSON</span></span>

<span data-ttu-id="60576-134">Hello следующие примеры демонстрируют, как toomake запроса GET к hello базовая Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="60576-134">hello following examples demonstrate how toomake a GET request against hello base Ambari REST API:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> <span data-ttu-id="60576-135">Hello Bash примеры в этом документе сделать hello следующие допущения:</span><span class="sxs-lookup"><span data-stu-id="60576-135">hello Bash examples in this document make hello following assumptions:</span></span>
>
> * <span data-ttu-id="60576-136">Hello имя входа для hello кластера является значением по умолчанию hello `admin`.</span><span class="sxs-lookup"><span data-stu-id="60576-136">hello login name for hello cluster is hello default value of `admin`.</span></span>
> * <span data-ttu-id="60576-137">`$PASSWORD`содержит пароль hello для hello команда входа HDInsight.</span><span class="sxs-lookup"><span data-stu-id="60576-137">`$PASSWORD` contains hello password for hello HDInsight login command.</span></span> <span data-ttu-id="60576-138">Это значение можно задать с помощью команды `PASSWORD='mypassword'`.</span><span class="sxs-lookup"><span data-stu-id="60576-138">You can set this value by using `PASSWORD='mypassword'`.</span></span>
> * <span data-ttu-id="60576-139">`$CLUSTERNAME`содержит имя кластера hello hello.</span><span class="sxs-lookup"><span data-stu-id="60576-139">`$CLUSTERNAME` contains hello name of hello cluster.</span></span> <span data-ttu-id="60576-140">Это значение можно задать с помощью команды `set CLUSTERNAME='clustername'`.</span><span class="sxs-lookup"><span data-stu-id="60576-140">You can set this value by using `set CLUSTERNAME='clustername'`</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> <span data-ttu-id="60576-141">Примеры PowerShell Hello в этом документе сделать hello следующие допущения:</span><span class="sxs-lookup"><span data-stu-id="60576-141">hello PowerShell examples in this document make hello following assumptions:</span></span>
>
> * <span data-ttu-id="60576-142">`$creds`представляет собой объект учетных данных, содержащий имя входа администратора hello и пароль для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="60576-142">`$creds` is a credential object that contains hello admin login and password for hello cluster.</span></span> <span data-ttu-id="60576-143">Это значение можно задать с помощью `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` указанием hello учетных данных при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="60576-143">You can set this value by using `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` and providing hello credentials when prompted.</span></span>
> * <span data-ttu-id="60576-144">`$clusterName`представляет собой строку, содержащую имя кластера hello hello.</span><span class="sxs-lookup"><span data-stu-id="60576-144">`$clusterName` is a string that contains hello name of hello cluster.</span></span> <span data-ttu-id="60576-145">Это значение можно задать с помощью команды `$clusterName="clustername"`.</span><span class="sxs-lookup"><span data-stu-id="60576-145">You can set this value by using `$clusterName="clustername"`.</span></span>

<span data-ttu-id="60576-146">В обоих примерах возвращает документ JSON, который начинается с toohello аналогичные сведения, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="60576-146">Both examples return a JSON document that begins with information similar toohello following example:</span></span>

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

### <a name="parsing-json-data"></a><span data-ttu-id="60576-147">Анализ данных JSON</span><span class="sxs-lookup"><span data-stu-id="60576-147">Parsing JSON data</span></span>

<span data-ttu-id="60576-148">Hello следующий пример использует `jq` tooparse hello документ ответа JSON и отображать только hello `health_report` сведения из результатов hello.</span><span class="sxs-lookup"><span data-stu-id="60576-148">hello following example uses `jq` tooparse hello JSON response document and display only hello `health_report` information from hello results.</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

<span data-ttu-id="60576-149">PowerShell 3.0 и более поздних версиях предоставляет hello `ConvertFrom-Json` , который преобразует hello документа JSON в объект, являющийся проще toowork с из PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60576-149">PowerShell 3.0 and higher provides hello `ConvertFrom-Json` cmdlet, which converts hello JSON document into an object that is easier toowork with from PowerShell.</span></span> <span data-ttu-id="60576-150">Hello следующий пример использует `ConvertFrom-Json` toodisplay только hello `health_report` сведения из результатов hello.</span><span class="sxs-lookup"><span data-stu-id="60576-150">hello following example uses `ConvertFrom-Json` toodisplay only hello `health_report` information from hello results.</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> <span data-ttu-id="60576-151">Хотя большинство примеров в этом документе используется `ConvertFrom-Json` toodisplay элементов из документа ответа hello, hello [Ambari обновление конфигурации](#example-update-ambari-configuration) примере jq.</span><span class="sxs-lookup"><span data-stu-id="60576-151">While most examples in this document use `ConvertFrom-Json` toodisplay elements from hello response document, hello [Update Ambari configuration](#example-update-ambari-configuration) example uses jq.</span></span> <span data-ttu-id="60576-152">В этом примере tooconstruct используется Jq шаблона из документа ответ JSON hello.</span><span class="sxs-lookup"><span data-stu-id="60576-152">Jq is used in this example tooconstruct a new template from hello JSON response document.</span></span>

<span data-ttu-id="60576-153">Полный перечень hello REST API см. [V1 Справочник по API Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="60576-153">For a complete reference of hello REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

## <a name="example-get-hello-fqdn-of-cluster-nodes"></a><span data-ttu-id="60576-154">Пример: Получение hello полное доменное имя кластера узлов</span><span class="sxs-lookup"><span data-stu-id="60576-154">Example: Get hello FQDN of cluster nodes</span></span>

<span data-ttu-id="60576-155">При работе с HDInsight, может возникнуть необходимость hello tooknow полное доменное имя (FQDN) узла кластера.</span><span class="sxs-lookup"><span data-stu-id="60576-155">When working with HDInsight, you may need tooknow hello fully qualified domain name (FQDN) of a cluster node.</span></span> <span data-ttu-id="60576-156">Можно легко получить hello полное доменное имя для hello различных узлов в кластере hello, используя следующие примеры hello:</span><span class="sxs-lookup"><span data-stu-id="60576-156">You can easily retrieve hello FQDN for hello various nodes in hello cluster using hello following examples:</span></span>

* <span data-ttu-id="60576-157">**Все узлы**</span><span class="sxs-lookup"><span data-stu-id="60576-157">**All nodes**</span></span>

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

* <span data-ttu-id="60576-158">**Головные узлы**</span><span class="sxs-lookup"><span data-stu-id="60576-158">**Head nodes**</span></span>

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

* <span data-ttu-id="60576-159">**Рабочие узлы**</span><span class="sxs-lookup"><span data-stu-id="60576-159">**Worker nodes**</span></span>

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

* <span data-ttu-id="60576-160">**Узлы Zookeeper**</span><span class="sxs-lookup"><span data-stu-id="60576-160">**Zookeeper nodes**</span></span>

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

## <a name="example-get-hello-internal-ip-address-of-cluster-nodes"></a><span data-ttu-id="60576-161">Пример: Получение hello внутренний IP-адрес кластера узлов</span><span class="sxs-lookup"><span data-stu-id="60576-161">Example: Get hello internal IP address of cluster nodes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="60576-162">Hello IP-адресов, возвращенных hello в примерах этого раздела, не напрямую Здравствуйте, доступны через Интернет.</span><span class="sxs-lookup"><span data-stu-id="60576-162">hello IP addresses returned by hello examples in this section are not directly accessible over hello internet.</span></span> <span data-ttu-id="60576-163">Они доступны только в пределах hello виртуальной сети Azure, содержащей hello кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="60576-163">They are only accessible within hello Azure Virtual Network that contains hello HDInsight cluster.</span></span>
>
> <span data-ttu-id="60576-164">Дополнительные сведения о работе с виртуальными сетями и HDInsight см. в статье [Расширение возможностей HDInsight с помощью виртуальной сети Azure](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="60576-164">For more information on working with HDInsight and virtual networks, see [Extend HDInsight capabilities by using a custom Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

<span data-ttu-id="60576-165">toofind hello IP-адрес, необходимо знать hello внутренней полное доменное имя (FQDN) hello узлы кластера.</span><span class="sxs-lookup"><span data-stu-id="60576-165">toofind hello IP address, you must know hello internal fully qualified domain name (FQDN) of hello cluster nodes.</span></span> <span data-ttu-id="60576-166">Получив hello полное доменное имя, можно получить hello IP-адрес узла hello.</span><span class="sxs-lookup"><span data-stu-id="60576-166">Once you have hello FQDN, you can then get hello IP address of hello host.</span></span> <span data-ttu-id="60576-167">Hello следующие примеры сначала запросить Ambari hello все узлы узла hello полное доменное имя, а затем запросить Ambari hello IP-адрес каждого узла.</span><span class="sxs-lookup"><span data-stu-id="60576-167">hello following examples first query Ambari for hello FQDN of all hello host nodes, then query Ambari for hello IP address of each host.</span></span>

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

## <a name="example-get-hello-default-storage"></a><span data-ttu-id="60576-168">Пример: Получение хранилища по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="60576-168">Example: Get hello default storage</span></span>

<span data-ttu-id="60576-169">При создании кластера HDInsight, необходимо использовать учетную запись хранилища Azure или хранилища Озера данных хранения по умолчанию hello для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="60576-169">When you create an HDInsight cluster, you must use an Azure Storage Account or Data Lake Store as hello default storage for hello cluster.</span></span> <span data-ttu-id="60576-170">Можно использовать эти сведения Ambari tooretrieve, после создания кластера hello.</span><span class="sxs-lookup"><span data-stu-id="60576-170">You can use Ambari tooretrieve this information after hello cluster has been created.</span></span> <span data-ttu-id="60576-171">Например, если требуется, чтобы контейнер toohello tooread и запись данных за пределами HDInsight.</span><span class="sxs-lookup"><span data-stu-id="60576-171">For example, if you want tooread/write data toohello container outside HDInsight.</span></span>

<span data-ttu-id="60576-172">Hello следующие примеры извлечь конфигурацию хранилища по умолчанию hello hello кластера:</span><span class="sxs-lookup"><span data-stu-id="60576-172">hello following examples retrieve hello default storage configuration from hello cluster:</span></span>

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
> <span data-ttu-id="60576-173">Эти примеры возвращают hello первого применения конфигурации toohello сервера (`service_config_version=1`) которого содержит эту информацию.</span><span class="sxs-lookup"><span data-stu-id="60576-173">These examples return hello first configuration applied toohello server (`service_config_version=1`) which contains this information.</span></span> <span data-ttu-id="60576-174">При извлечении значения, который был изменен после создания кластера можно требуются версии конфигурации toolist hello и получить последнюю версию hello.</span><span class="sxs-lookup"><span data-stu-id="60576-174">If you retrieve a value that has been modified after cluster creation, you may need toolist hello configuration versions and retrieve hello latest one.</span></span>

<span data-ttu-id="60576-175">Возвращаемое значение Hello — примерно tooone hello следующие примеры:</span><span class="sxs-lookup"><span data-stu-id="60576-175">hello return value is similar tooone of hello following examples:</span></span>

* <span data-ttu-id="60576-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net`-Это значение указывает, что данный кластер hello с учетной записью хранилища Azure для хранилища по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="60576-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - This value indicates that hello cluster is using an Azure Storage account for default storage.</span></span> <span data-ttu-id="60576-177">Hello `ACCOUNTNAME` значение является именем hello hello учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="60576-177">hello `ACCOUNTNAME` value is hello name of hello storage account.</span></span> <span data-ttu-id="60576-178">Hello `CONTAINER` часть — имя hello hello контейнер больших двоичных объектов в учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="60576-178">hello `CONTAINER` portion is hello name of hello blob container in hello storage account.</span></span> <span data-ttu-id="60576-179">контейнер Hello — основной hello hello HDFS совместимый хранилища для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="60576-179">hello container is hello root of hello HDFS compatible storage for hello cluster.</span></span>

* <span data-ttu-id="60576-180">`adl://home`-Это значение указывает, что данный кластер hello использует хранилище Озера данных Azure для хранилища по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="60576-180">`adl://home` - This value indicates that hello cluster is using an Azure Data Lake Store for default storage.</span></span>

    <span data-ttu-id="60576-181">hello toofind имя учетной записи хранилища Озера данных, используйте следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="60576-181">toofind hello Data Lake Store account name, use hello following examples:</span></span>

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

    <span data-ttu-id="60576-182">Hello возвращаемое значение аналогично слишком`ACCOUNTNAME.azuredatalakestore.net`, где `ACCOUNTNAME` — имя hello hello хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="60576-182">hello return value is similar too`ACCOUNTNAME.azuredatalakestore.net`, where `ACCOUNTNAME` is hello name of hello Data Lake Store account.</span></span>

    <span data-ttu-id="60576-183">каталог toofind hello в хранилище Озера данных, содержащем hello хранилища для кластера hello, hello используйте следующие примеры:</span><span class="sxs-lookup"><span data-stu-id="60576-183">toofind hello directory within Data Lake Store that contains hello storage for hello cluster, use hello following examples:</span></span>

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

    <span data-ttu-id="60576-184">Hello возвращаемое значение аналогично слишком`/clusters/CLUSTERNAME/`.</span><span class="sxs-lookup"><span data-stu-id="60576-184">hello return value is similar too`/clusters/CLUSTERNAME/`.</span></span> <span data-ttu-id="60576-185">Это значение представляет собой путь в пределах hello хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="60576-185">This value is a path within hello Data Lake Store account.</span></span> <span data-ttu-id="60576-186">Этот путь является корнем hello hello совместимые файловой системы HDFS для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="60576-186">This path is hello root of hello HDFS compatible file system for hello cluster.</span></span> 

> [!NOTE]
> <span data-ttu-id="60576-187">Hello `Get-AzureRmHDInsightCluster` командлета, предоставляемые [Azure PowerShell](/powershell/azure/overview) также возвращает hello данные хранилища для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="60576-187">hello `Get-AzureRmHDInsightCluster` cmdlet provided by [Azure PowerShell](/powershell/azure/overview) also returns hello storage information for hello cluster.</span></span>


## <a name="example-get-configuration"></a><span data-ttu-id="60576-188">Пример. Получение конфигурации</span><span class="sxs-lookup"><span data-stu-id="60576-188">Example: Get configuration</span></span>

1. <span data-ttu-id="60576-189">Возвращение конфигураций hello, доступные для кластера.</span><span class="sxs-lookup"><span data-stu-id="60576-189">Get hello configurations that are available for your cluster.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    <span data-ttu-id="60576-190">Этот пример возвращает документ JSON, содержащий текущую конфигурацию hello (определяется hello *тега* значение) для hello компонентов, установленных на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="60576-190">This example returns a JSON document containing hello current configuration (identified by hello *tag* value) for hello components installed on hello cluster.</span></span> <span data-ttu-id="60576-191">Hello ниже приведен фрагмент кода hello данным, возвращаемым типом кластера Spark.</span><span class="sxs-lookup"><span data-stu-id="60576-191">hello following example is an excerpt from hello data returned from a Spark cluster type.</span></span>
   
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

2. <span data-ttu-id="60576-192">Получите конфигурацию hello для hello компонента, которые вас интересуют.</span><span class="sxs-lookup"><span data-stu-id="60576-192">Get hello configuration for hello component that you are interested in.</span></span> <span data-ttu-id="60576-193">Следующий пример, замените в hello `INITIAL` с hello тег значение, возвращаемое из предыдущего запроса hello.</span><span class="sxs-lookup"><span data-stu-id="60576-193">In hello following example, replace `INITIAL` with hello tag value returned from hello previous request.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    <span data-ttu-id="60576-194">Этот пример возвращает документ JSON, содержащий hello текущую конфигурацию для hello `core-site` компонента.</span><span class="sxs-lookup"><span data-stu-id="60576-194">This example returns a JSON document containing hello current configuration for hello `core-site` component.</span></span>

## <a name="example-update-configuration"></a><span data-ttu-id="60576-195">Пример. Обновление конфигурации</span><span class="sxs-lookup"><span data-stu-id="60576-195">Example: Update configuration</span></span>

1. <span data-ttu-id="60576-196">Получите текущую конфигурацию hello, где хранятся Ambari как hello» требуемой конфигурацией»:</span><span class="sxs-lookup"><span data-stu-id="60576-196">Get hello current configuration, which Ambari stores as hello "desired configuration":</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    <span data-ttu-id="60576-197">Этот пример возвращает документ JSON, содержащий текущую конфигурацию hello (определяется hello *тега* значение) для hello компонентов, установленных на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="60576-197">This example returns a JSON document containing hello current configuration (identified by hello *tag* value) for hello components installed on hello cluster.</span></span> <span data-ttu-id="60576-198">Hello ниже приведен фрагмент кода hello данным, возвращаемым типом кластера Spark.</span><span class="sxs-lookup"><span data-stu-id="60576-198">hello following example is an excerpt from hello data returned from a Spark cluster type.</span></span>
   
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
   
    <span data-ttu-id="60576-199">Из этого списка требуется имя hello toocopy hello компонента (например, **spark\_thrift\_sparkconf** и hello **тега** значение.</span><span class="sxs-lookup"><span data-stu-id="60576-199">From this list, you need toocopy hello name of hello component (for example, **spark\_thrift\_sparkconf** and hello **tag** value.</span></span>

2. <span data-ttu-id="60576-200">Получить конфигурацию hello для компонента hello и тег с помощью hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="60576-200">Retrieve hello configuration for hello component and tag by using hello following commands:</span></span>
   
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
    > <span data-ttu-id="60576-201">Замените **spark thrift-sparkconf** и **начальной** с компонентом hello и тег, который необходимо tooretrieve hello конфигурация для.</span><span class="sxs-lookup"><span data-stu-id="60576-201">Replace **spark-thrift-sparkconf** and **INITIAL** with hello component and tag that you want tooretrieve hello configuration for.</span></span>
   
    <span data-ttu-id="60576-202">Jq является данных используется tooturn hello, полученного из HDInsight в новый шаблон конфигурации.</span><span class="sxs-lookup"><span data-stu-id="60576-202">Jq is used tooturn hello data retrieved from HDInsight into a new configuration template.</span></span> <span data-ttu-id="60576-203">В частности эти примеры выполнения hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="60576-203">Specifically, these examples perform hello following actions:</span></span>
   
    * <span data-ttu-id="60576-204">Создает уникальное значение, содержащее строку hello «версия» и hello Дата, которая хранится в `newtag`.</span><span class="sxs-lookup"><span data-stu-id="60576-204">Creates a unique value containing hello string "version" and hello date, which is stored in `newtag`.</span></span>

    * <span data-ttu-id="60576-205">Создает документ корневой hello новой требуемой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="60576-205">Creates a root document for hello new desired configuration.</span></span>

    * <span data-ttu-id="60576-206">Возвращает hello содержимое hello `.items[]` массива и добавляет его в разделе hello **desired_config** элемента.</span><span class="sxs-lookup"><span data-stu-id="60576-206">Gets hello contents of hello `.items[]` array and adds it under hello **desired_config** element.</span></span>

    * <span data-ttu-id="60576-207">Удаляет hello `href`, `version`, и `Config` элементы, как эти элементы не требуется toosubmit новую конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="60576-207">Deletes hello `href`, `version`, and `Config` elements, as these elements aren't needed toosubmit a new configuration.</span></span>

    * <span data-ttu-id="60576-208">Добавляет элемент `tag` со значением `version#################`.</span><span class="sxs-lookup"><span data-stu-id="60576-208">Adds a `tag` element with a value of `version#################`.</span></span> <span data-ttu-id="60576-209">Hello числовую часть зависит hello текущую дату.</span><span class="sxs-lookup"><span data-stu-id="60576-209">hello numeric portion is based on hello current date.</span></span> <span data-ttu-id="60576-210">Каждая конфигурация должна иметь уникальное значение tag.</span><span class="sxs-lookup"><span data-stu-id="60576-210">Each configuration must have a unique tag.</span></span>
     
    <span data-ttu-id="60576-211">Наконец, данные hello сохраняются toohello `newconfig.json` документа.</span><span class="sxs-lookup"><span data-stu-id="60576-211">Finally, hello data is saved toohello `newconfig.json` document.</span></span> <span data-ttu-id="60576-212">Структура документа Hello должен выглядеть примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="60576-212">hello document structure should appear similar toohello following example:</span></span>
     
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

3. <span data-ttu-id="60576-213">Откройте hello `newconfig.json` документа и изменить или добавить значения в hello `properties` объекта.</span><span class="sxs-lookup"><span data-stu-id="60576-213">Open hello `newconfig.json` document and modify/add values in hello `properties` object.</span></span> <span data-ttu-id="60576-214">Hello следующий пример изменяет hello значение `"spark.yarn.am.memory"` из `"1g"` слишком`"3g"`.</span><span class="sxs-lookup"><span data-stu-id="60576-214">hello following example changes hello value of `"spark.yarn.am.memory"` from `"1g"` too`"3g"`.</span></span> <span data-ttu-id="60576-215">Он также добавляет `"spark.kryoserializer.buffer.max"` со значением `"256m"`.</span><span class="sxs-lookup"><span data-stu-id="60576-215">It also adds `"spark.kryoserializer.buffer.max"` with a value of `"256m"`.</span></span>
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    <span data-ttu-id="60576-216">Сохраните файл hello, после завершения внесения изменений.</span><span class="sxs-lookup"><span data-stu-id="60576-216">Save hello file once you are done making modifications.</span></span>

4. <span data-ttu-id="60576-217">Используйте следующие команды toosubmit hello обновлена конфигурация tooAmbari hello.</span><span class="sxs-lookup"><span data-stu-id="60576-217">Use hello following commands toosubmit hello updated configuration tooAmbari.</span></span>
   
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
   
    <span data-ttu-id="60576-218">Эти команды Отправить содержимое hello hello **newconfig.json** файл toohello кластера как hello новые требуемой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="60576-218">These commands submit hello contents of hello **newconfig.json** file toohello cluster as hello new desired configuration.</span></span> <span data-ttu-id="60576-219">Hello запрос возвращает документ JSON.</span><span class="sxs-lookup"><span data-stu-id="60576-219">hello request returns a JSON document.</span></span> <span data-ttu-id="60576-220">Hello **versionTag** элемент в этом документе должна соответствовать версии hello отправки, а hello **configs** объект содержит запрошенные изменения конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="60576-220">hello **versionTag** element in this document should match hello version you submitted, and hello **configs** object contains hello configuration changes you requested.</span></span>

### <a name="example-restart-a-service-component"></a><span data-ttu-id="60576-221">Пример. Перезапуск компонента службы</span><span class="sxs-lookup"><span data-stu-id="60576-221">Example: Restart a service component</span></span>

<span data-ttu-id="60576-222">На этом этапе при рассмотрении hello Ambari web пользовательского интерфейса hello службу Spark показывает, что он требует toobe перезапуска, чтобы новая конфигурация hello вступило в силу.</span><span class="sxs-lookup"><span data-stu-id="60576-222">At this point, if you look at hello Ambari web UI, hello Spark service indicates that it needs toobe restarted before hello new configuration can take effect.</span></span> <span data-ttu-id="60576-223">Используйте следующие шаги toorestart hello службы hello.</span><span class="sxs-lookup"><span data-stu-id="60576-223">Use hello following steps toorestart hello service.</span></span>

1. <span data-ttu-id="60576-224">Используйте следующие tooenable в режиме обслуживания для hello службу Spark hello.</span><span class="sxs-lookup"><span data-stu-id="60576-224">Use hello following tooenable maintenance mode for hello Spark service:</span></span>

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
   
    <span data-ttu-id="60576-225">Эти команды передают сервере toohello документа JSON, который включает режим обслуживания.</span><span class="sxs-lookup"><span data-stu-id="60576-225">These commands send a JSON document toohello server that turns on maintenance mode.</span></span> <span data-ttu-id="60576-226">Можно проверить, служба hello теперь находится в режиме обслуживания с помощью hello, следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="60576-226">You can verify that hello service is now in maintenance mode using hello following request:</span></span>
   
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
   
    <span data-ttu-id="60576-227">Hello возвращаемым значением является `ON`.</span><span class="sxs-lookup"><span data-stu-id="60576-227">hello return value is `ON`.</span></span>

2. <span data-ttu-id="60576-228">Затем выполните следующие tooturn выключение службы hello hello.</span><span class="sxs-lookup"><span data-stu-id="60576-228">Next, use hello following tooturn off hello service:</span></span>

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
    
    <span data-ttu-id="60576-229">Hello ответ — аналогично toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="60576-229">hello response is similar toohello following example:</span></span>
   
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
    > <span data-ttu-id="60576-230">Hello `href` значения, возвращенного этот URI используется hello внутренний IP-адрес узла кластера hello.</span><span class="sxs-lookup"><span data-stu-id="60576-230">hello `href` value returned by this URI is using hello internal IP address of hello cluster node.</span></span> <span data-ttu-id="60576-231">toouse его из кластера вне hello, замены части hello «10.0.0.18:8080» hello полное доменное имя кластера hello.</span><span class="sxs-lookup"><span data-stu-id="60576-231">toouse it from outside hello cluster, replace hello \`10.0.0.18:8080' portion with hello FQDN of hello cluster.</span></span> 
    
    <span data-ttu-id="60576-232">Привет, следующие команды получить состояние hello hello запроса:</span><span class="sxs-lookup"><span data-stu-id="60576-232">hello following commands retrieve hello status of hello request:</span></span>

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

    <span data-ttu-id="60576-233">Ответ `COMPLETED` указывает завершил этот запрос hello.</span><span class="sxs-lookup"><span data-stu-id="60576-233">A response of `COMPLETED` indicates that hello request has finished.</span></span>

3. <span data-ttu-id="60576-234">После завершения предыдущего запроса hello, используйте следующие службы hello toostart hello.</span><span class="sxs-lookup"><span data-stu-id="60576-234">Once hello previous request completes, use hello following toostart hello service.</span></span>
   
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
    <span data-ttu-id="60576-235">Служба Hello теперь использует hello новую конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="60576-235">hello service is now using hello new configuration.</span></span>

4. <span data-ttu-id="60576-236">Наконец используйте следующие tooturn отключение режима обслуживания hello.</span><span class="sxs-lookup"><span data-stu-id="60576-236">Finally, use hello following tooturn off maintenance mode.</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="60576-237">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="60576-237">Next steps</span></span>

<span data-ttu-id="60576-238">Полный перечень hello REST API см. [V1 Справочник по API Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="60576-238">For a complete reference of hello REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

