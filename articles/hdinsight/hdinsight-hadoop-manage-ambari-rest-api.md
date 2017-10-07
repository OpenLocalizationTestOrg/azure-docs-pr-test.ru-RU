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
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-rest-api"></a>Управление кластерами HDInsight с помощью API-интерфейса REST Ambari hello

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

Узнайте, как toouse hello toomanage Ambari API-Интерфейс REST и наблюдения за кластерами Hadoop в Azure HDInsight.

Apache Ambari упрощает управление hello и мониторинг кластера Hadoop, предоставляя простой toouse веб-интерфейса пользователя и REST API. Ambari включается в кластерах HDInsight, использующих операционной системы Linux hello. Можно использовать Ambari toomonitor hello кластера и внести изменения в конфигурацию.

## <a id="whatis"></a>Что такое Ambari

[Apache Ambari](http://ambari.apache.org) предоставляет веб-Интерфейс, который может быть используется tooprovision, управления и наблюдения за кластерами Hadoop. Разработчики могут интегрировать эти возможности в свои приложения с помощью hello [API-интерфейс REST Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

Ambari предоставляется по умолчанию с кластерами HDInsight на платформе Linux.

## <a name="how-toouse-hello-ambari-rest-api"></a>Как toouse hello Ambari REST API

> [!IMPORTANT]
> Hello сведения и примеры в этом документе требуется кластер HDInsight, который использует операционная система Linux. Дополнительные сведения см. в статье [Руководство по Hadoop. Приступая к работе с Hadoop в HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).

Hello в этом документе приведены примеры для как hello sh (bash) и PowerShell. Hello bash, примеры, были проверены с GNU bash 4.3.11, но должно работать с другими оболочками Unix. Примеры PowerShell Hello были протестированы в PowerShell 5.0, но должны работать вместе с PowerShell 3.0 или более поздней версии.

При использовании hello __Bourne оболочки__ (Bash), необходимо иметь hello установлены следующие компоненты:

* [cURL](http://curl.haxx.se/): перелистывание — это программа, может быть используется toowork с API REST с hello командной строки. В этом документе это используется toocommunicate с hello Ambari REST API.

Если вы используете Bash или PowerShell, установите также [jq](https://stedolan.github.io/jq/). jq — это служебная программа для работы с документами JSON. Он используется в **все** hello примеры Bash и **один** примеров PowerShell hello.

### <a name="base-uri-for-ambari-rest-api"></a>Базовый универсальный код ресурса для REST API Ambari

Hello базовый URI для hello Ambari API-интерфейса REST на HDInsight — https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, где **CLUSTERNAME** — hello имя кластера.

> [!IMPORTANT]
> Хотя полное доменное имя кластера hello в hello часть имени (FQDN) домена hello URI (CLUSTERNAME.azurehdinsight.net) без учета регистра, других экземпляров в hello URI чувствительны к регистру. Например, если кластер называется `MyCluster`, hello ниже приведены допустимые URI:
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> Hello следующие идентификаторы URI возвращает ошибку, так как hello второго вхождения имени hello не hello исправьте регистр.
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a>Аутентификация

Подключение tooAmbari на HDInsight требуется протокол HTTPS. Имя учетной записи администратора используйте hello (по умолчанию hello — **администратора**) и пароль, указанный во время создания кластера.

## <a name="examples-authentication-and-parsing-json"></a>Примеры. Проверка подлинности и анализ JSON

Hello следующие примеры демонстрируют, как toomake запроса GET к hello базовая Ambari REST API.

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> Hello Bash примеры в этом документе сделать hello следующие допущения:
>
> * Hello имя входа для hello кластера является значением по умолчанию hello `admin`.
> * `$PASSWORD`содержит пароль hello для hello команда входа HDInsight. Это значение можно задать с помощью команды `PASSWORD='mypassword'`.
> * `$CLUSTERNAME`содержит имя кластера hello hello. Это значение можно задать с помощью команды `set CLUSTERNAME='clustername'`.

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> Примеры PowerShell Hello в этом документе сделать hello следующие допущения:
>
> * `$creds`представляет собой объект учетных данных, содержащий имя входа администратора hello и пароль для hello кластера. Это значение можно задать с помощью `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` указанием hello учетных данных при появлении запроса.
> * `$clusterName`представляет собой строку, содержащую имя кластера hello hello. Это значение можно задать с помощью команды `$clusterName="clustername"`.

В обоих примерах возвращает документ JSON, который начинается с toohello аналогичные сведения, следующий пример:

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

### <a name="parsing-json-data"></a>Анализ данных JSON

Hello следующий пример использует `jq` tooparse hello документ ответа JSON и отображать только hello `health_report` сведения из результатов hello.

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

PowerShell 3.0 и более поздних версиях предоставляет hello `ConvertFrom-Json` , который преобразует hello документа JSON в объект, являющийся проще toowork с из PowerShell. Hello следующий пример использует `ConvertFrom-Json` toodisplay только hello `health_report` сведения из результатов hello.

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> Хотя большинство примеров в этом документе используется `ConvertFrom-Json` toodisplay элементов из документа ответа hello, hello [Ambari обновление конфигурации](#example-update-ambari-configuration) примере jq. В этом примере tooconstruct используется Jq шаблона из документа ответ JSON hello.

Полный перечень hello REST API см. [V1 Справочник по API Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

## <a name="example-get-hello-fqdn-of-cluster-nodes"></a>Пример: Получение hello полное доменное имя кластера узлов

При работе с HDInsight, может возникнуть необходимость hello tooknow полное доменное имя (FQDN) узла кластера. Можно легко получить hello полное доменное имя для hello различных узлов в кластере hello, используя следующие примеры hello:

* **Все узлы**

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

* **Головные узлы**

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

* **Рабочие узлы**

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

* **Узлы Zookeeper**

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

## <a name="example-get-hello-internal-ip-address-of-cluster-nodes"></a>Пример: Получение hello внутренний IP-адрес кластера узлов

> [!IMPORTANT]
> Hello IP-адресов, возвращенных hello в примерах этого раздела, не напрямую Здравствуйте, доступны через Интернет. Они доступны только в пределах hello виртуальной сети Azure, содержащей hello кластера HDInsight.
>
> Дополнительные сведения о работе с виртуальными сетями и HDInsight см. в статье [Расширение возможностей HDInsight с помощью виртуальной сети Azure](hdinsight-extend-hadoop-virtual-network.md).

toofind hello IP-адрес, необходимо знать hello внутренней полное доменное имя (FQDN) hello узлы кластера. Получив hello полное доменное имя, можно получить hello IP-адрес узла hello. Hello следующие примеры сначала запросить Ambari hello все узлы узла hello полное доменное имя, а затем запросить Ambari hello IP-адрес каждого узла.

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

## <a name="example-get-hello-default-storage"></a>Пример: Получение хранилища по умолчанию hello

При создании кластера HDInsight, необходимо использовать учетную запись хранилища Azure или хранилища Озера данных хранения по умолчанию hello для hello кластера. Можно использовать эти сведения Ambari tooretrieve, после создания кластера hello. Например, если требуется, чтобы контейнер toohello tooread и запись данных за пределами HDInsight.

Hello следующие примеры извлечь конфигурацию хранилища по умолчанию hello hello кластера:

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
> Эти примеры возвращают hello первого применения конфигурации toohello сервера (`service_config_version=1`) которого содержит эту информацию. При извлечении значения, который был изменен после создания кластера можно требуются версии конфигурации toolist hello и получить последнюю версию hello.

Возвращаемое значение Hello — примерно tooone hello следующие примеры:

* `wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net`-Это значение указывает, что данный кластер hello с учетной записью хранилища Azure для хранилища по умолчанию. Hello `ACCOUNTNAME` значение является именем hello hello учетной записи хранения. Hello `CONTAINER` часть — имя hello hello контейнер больших двоичных объектов в учетной записи хранения hello. контейнер Hello — основной hello hello HDFS совместимый хранилища для кластера hello.

* `adl://home`-Это значение указывает, что данный кластер hello использует хранилище Озера данных Azure для хранилища по умолчанию.

    hello toofind имя учетной записи хранилища Озера данных, используйте следующие примеры hello.

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

    Hello возвращаемое значение аналогично слишком`ACCOUNTNAME.azuredatalakestore.net`, где `ACCOUNTNAME` — имя hello hello хранилища Озера данных.

    каталог toofind hello в хранилище Озера данных, содержащем hello хранилища для кластера hello, hello используйте следующие примеры:

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

    Hello возвращаемое значение аналогично слишком`/clusters/CLUSTERNAME/`. Это значение представляет собой путь в пределах hello хранилища Озера данных. Этот путь является корнем hello hello совместимые файловой системы HDFS для hello кластера. 

> [!NOTE]
> Hello `Get-AzureRmHDInsightCluster` командлета, предоставляемые [Azure PowerShell](/powershell/azure/overview) также возвращает hello данные хранилища для кластера hello.


## <a name="example-get-configuration"></a>Пример. Получение конфигурации

1. Возвращение конфигураций hello, доступные для кластера.

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    Этот пример возвращает документ JSON, содержащий текущую конфигурацию hello (определяется hello *тега* значение) для hello компонентов, установленных на кластере hello. Hello ниже приведен фрагмент кода hello данным, возвращаемым типом кластера Spark.
   
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

2. Получите конфигурацию hello для hello компонента, которые вас интересуют. Следующий пример, замените в hello `INITIAL` с hello тег значение, возвращаемое из предыдущего запроса hello.

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    Этот пример возвращает документ JSON, содержащий hello текущую конфигурацию для hello `core-site` компонента.

## <a name="example-update-configuration"></a>Пример. Обновление конфигурации

1. Получите текущую конфигурацию hello, где хранятся Ambari как hello» требуемой конфигурацией»:

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    Этот пример возвращает документ JSON, содержащий текущую конфигурацию hello (определяется hello *тега* значение) для hello компонентов, установленных на кластере hello. Hello ниже приведен фрагмент кода hello данным, возвращаемым типом кластера Spark.
   
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
   
    Из этого списка требуется имя hello toocopy hello компонента (например, **spark\_thrift\_sparkconf** и hello **тега** значение.

2. Получить конфигурацию hello для компонента hello и тег с помощью hello, следующие команды:
   
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
    > Замените **spark thrift-sparkconf** и **начальной** с компонентом hello и тег, который необходимо tooretrieve hello конфигурация для.
   
    Jq является данных используется tooturn hello, полученного из HDInsight в новый шаблон конфигурации. В частности эти примеры выполнения hello, следующие действия:
   
    * Создает уникальное значение, содержащее строку hello «версия» и hello Дата, которая хранится в `newtag`.

    * Создает документ корневой hello новой требуемой конфигурации.

    * Возвращает hello содержимое hello `.items[]` массива и добавляет его в разделе hello **desired_config** элемента.

    * Удаляет hello `href`, `version`, и `Config` элементы, как эти элементы не требуется toosubmit новую конфигурацию.

    * Добавляет элемент `tag` со значением `version#################`. Hello числовую часть зависит hello текущую дату. Каждая конфигурация должна иметь уникальное значение tag.
     
    Наконец, данные hello сохраняются toohello `newconfig.json` документа. Структура документа Hello должен выглядеть примерно toohello следующий пример:
     
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

3. Откройте hello `newconfig.json` документа и изменить или добавить значения в hello `properties` объекта. Hello следующий пример изменяет hello значение `"spark.yarn.am.memory"` из `"1g"` слишком`"3g"`. Он также добавляет `"spark.kryoserializer.buffer.max"` со значением `"256m"`.
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    Сохраните файл hello, после завершения внесения изменений.

4. Используйте следующие команды toosubmit hello обновлена конфигурация tooAmbari hello.
   
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
   
    Эти команды Отправить содержимое hello hello **newconfig.json** файл toohello кластера как hello новые требуемой конфигурации. Hello запрос возвращает документ JSON. Hello **versionTag** элемент в этом документе должна соответствовать версии hello отправки, а hello **configs** объект содержит запрошенные изменения конфигурации hello.

### <a name="example-restart-a-service-component"></a>Пример. Перезапуск компонента службы

На этом этапе при рассмотрении hello Ambari web пользовательского интерфейса hello службу Spark показывает, что он требует toobe перезапуска, чтобы новая конфигурация hello вступило в силу. Используйте следующие шаги toorestart hello службы hello.

1. Используйте следующие tooenable в режиме обслуживания для hello службу Spark hello.

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
   
    Эти команды передают сервере toohello документа JSON, который включает режим обслуживания. Можно проверить, служба hello теперь находится в режиме обслуживания с помощью hello, следующий запрос:
   
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
   
    Hello возвращаемым значением является `ON`.

2. Затем выполните следующие tooturn выключение службы hello hello.

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
    
    Hello ответ — аналогично toohello в следующем примере:
   
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
    > Hello `href` значения, возвращенного этот URI используется hello внутренний IP-адрес узла кластера hello. toouse его из кластера вне hello, замены части hello «10.0.0.18:8080» hello полное доменное имя кластера hello. 
    
    Привет, следующие команды получить состояние hello hello запроса:

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

    Ответ `COMPLETED` указывает завершил этот запрос hello.

3. После завершения предыдущего запроса hello, используйте следующие службы hello toostart hello.
   
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
    Служба Hello теперь использует hello новую конфигурацию.

4. Наконец используйте следующие tooturn отключение режима обслуживания hello.
   
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

## <a name="next-steps"></a>Дальнейшие действия

Полный перечень hello REST API см. [V1 Справочник по API Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

