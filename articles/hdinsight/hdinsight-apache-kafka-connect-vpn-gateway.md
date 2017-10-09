---
title: "с помощью виртуальных сетей - Azure HDInsight tooKafka aaaConnect | Документы Microsoft"
description: "Узнайте, как toodirectly подключаться tooKafka на HDInsight через виртуальную сеть Azure. Узнайте, как tooKafka tooconnect разработки клиентов, используя VPN-шлюза, или от клиентов в вашей локальной сети, с помощью устройство шлюза VPN."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.custom: hdinsightactive
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/01/2017
ms.author: larryfr
ms.openlocfilehash: 03542fe14b9a1d010dffa22a8f8d96b098a1576e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tookafka-on-hdinsight-preview-through-an-azure-virtual-network"></a>Подключение через виртуальную сеть Azure tooKafka на HDInsight (Предварительная версия)

Узнайте, как toodirectly подключаться tooKafka на HDInsight с помощью виртуальных сетей Azure. Этот документ содержит сведения о подключении с помощью конфигурации hello tooKafka:

* Из ресурсов в локальной сети. Это подключение устанавливается с помощью VPN-устройства (программного или аппаратного) в локальной сети.
* Из среды разработки с помощью программного VPN-клиента.

## <a name="architecture-and-planning"></a>Архитектура и планирование

HDInsight не допускает tooKafka прямое подключение через hello общедоступный Интернет. Вместо этого Kafka клиентов (отправителями и получателями) необходимо использовать один из hello следующие способы подключения:

* Запуск клиента hello в hello же виртуальной сети Kafka на HDInsight. Эта конфигурация используется в hello [начинаться с Apache Kafka (Предварительная версия) на HDInsight](hdinsight-apache-kafka-get-started.md) документа. Hello клиента запускается непосредственно hello HDInsight узлы кластера или на другой виртуальной машины в hello же сети.

* Подключение частной сети, например в локальной сети, toohello виртуальной сети. Эта конфигурация позволяет клиентам в локальной сети toodirectly работу с Kafka. tooenable этой конфигурации выполните hello следующие задачи:

    1. Создайте виртуальную сеть.
    2. Создайте VPN-шлюз, использующий конфигурацию типа "сеть — сеть". Hello конфигурацию, используемую в этом документе подключается tooa устройство шлюза VPN в вашей локальной сети.
    3. Создайте DNS-сервер в виртуальной сети hello.
    4. Настройка перенаправления между hello DNS-сервера в каждой сети.
    5. Установите Kafka на HDInsight в виртуальной сети hello.

    Дополнительные сведения см. в разделе hello [подключение из локальной сети tooKafka](#on-premises) раздела. 

* Подключение отдельных машин toohello виртуальной сети с помощью шлюза VPN и VPN-клиента. tooenable этой конфигурации выполните hello следующие задачи:

    1. Создайте виртуальную сеть.
    2. Создайте VPN-шлюз, использующий конфигурацию типа "точка — сеть". Такая конфигурация предоставляет VPN-клиент, который можно установить на клиентах Windows.
    3. Установите Kafka на HDInsight в виртуальной сети hello.
    4. Настройте Kafka для объявления IP-адресов. Эта конфигурация обеспечивает tooconnect hello клиента, с помощью IP-адресов, а не имена доменов.
    5. Загрузите и используйте hello VPN-клиента в системе разработки hello.

    Дополнительные сведения см. в разделе hello [подключения к VPN-клиент tooKafka](#vpnclient) раздела.

    > [!WARNING]
    > Эта конфигурация рекомендуется только для целей разработки из-за hello следующие ограничения:
    >
    > * Каждый клиент должен подключиться с помощью программного VPN-клиента. Azure предоставляет только клиент Windows.
    > * Hello клиента не передает имя разрешения запросов toohello виртуальной сети, поэтому необходимо использовать IP-адресов с Kafka toocommunicate. Связи через пакеты Интеграции требуется дополнительная конфигурация кластера Kafka hello.

Дополнительные сведения об использовании HDInsight в виртуальной сети см. в статье [Расширение возможностей HDInsight с помощью виртуальной сети Azure](./hdinsight-extend-hadoop-virtual-network.md).

## <a id="on-premises"></a>Подключение tooKafka из локальной сети

toocreate Kafka кластера, который обменивается данными с вашей локальной сети, выполните действия hello в hello [HDInsight подключения tooyour локальной сети](./connect-on-premises-network.md) документа.

> [!IMPORTANT]
> При создании кластера HDInsight hello выберите hello __Kafka__ кластера типа.

Эти шаги создают hello следующая конфигурация:

* Виртуальная сеть Azure
* VPN-шлюз типа "сеть — сеть";
* учетная запись хранения Azure (используемая HDInsight);
* Kafka HDInsight

что toohello кластера может подключаться клиент Kafka от локальной, используйте шаги hello hello tooverify [пример: клиента Python](#python-client) раздела.

## <a id="vpnclient"></a>Подключение tooKafka с VPN-клиента

Выполните шаги hello в этот раздел toocreate hello, следующая конфигурация.

* Виртуальная сеть Azure
* VPN-шлюз типа "точка — сеть"
* Учетная запись хранения Azure (используется HDInsight)
* Kafka HDInsight

1. Следуйте указаниям hello hello [работа с самозаверяющие сертификаты для подключений точки сайтами](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) документа. В этом документе создает hello сертификаты, необходимые для шлюза hello.

2. Открыть командную строку PowerShell и используйте следующий код toolog в tooyour подписки Azure hello:

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment tooset hello subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. Используйте следующие hello кода toocreate переменные, содержащие сведения о конфигурации:

    ```powershell
    # Prompt for generic information
    $resourceGroupName = Read-Host "What is hello resource group name?"
    $baseName = Read-Host "What is hello base name? It is used toocreate names for resources, such as 'net-basename' and 'kafka-basename':"
    $location = Read-Host "What Azure Region do you want toocreate hello resources in?"
    $rootCert = Read-Host "What is hello file path toohello root certificate? It is used toosecure hello VPN gateway."

    # Prompt for HDInsight credentials
    $adminCreds = Get-Credential -Message "Enter hello HTTPS user name and password for hello HDInsight cluster" -UserName "admin"
    $sshCreds = Get-Credential -Message "Enter hello SSH user name and password for hello HDInsight cluster" -UserName "sshuser"

    # Names for Azure resources
    $networkName = "net-$baseName"
    $clusterName = "kafka-$baseName"
    $storageName = "store$baseName" # Can't use dashes in storage names
    $defaultContainerName = $clusterName
    $defaultSubnetName = "default"
    $gatewaySubnetName = "GatewaySubnet"
    $gatewayPublicIpName = "GatewayIp"
    $gatewayIpConfigName = "GatewayConfig"
    $vpnRootCertName = "rootcert"
    $vpnName = "VPNGateway"

    # Network settings
    $networkAddressPrefix = "10.0.0.0/16"
    $defaultSubnetPrefix = "10.0.0.0/24"
    $gatewaySubnetPrefix = "10.0.1.0/24"
    $vpnClientAddressPool = "172.16.201.0/24"

    # HDInsight settings
    $HdiWorkerNodes = 4
    $hdiVersion = "3.5"
    $hdiType = "Kafka"
    ```

4. Используйте hello следующий код группы ресурсов Azure toocreate hello и виртуальной сети:

    ```powershell
    # Create hello resource group that contains everything
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello subnet configuration
    $defaultSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -AddressPrefix $defaultSubnetPrefix
    $gatewaySubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -AddressPrefix $gatewaySubnetPrefix

    # Create hello subnet
    New-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AddressPrefix $networkAddressPrefix `
        -Subnet $defaultSubnetConfig, $gatewaySubnetConfig

    # Get hello network & subnet that were created
    $network = Get-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName
    $gatewaySubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -VirtualNetwork $network
    $defaultSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -VirtualNetwork $network

    # Set a dynamic public IP address for hello gateway subnet
    $gatewayPublicIp = New-AzureRmPublicIpAddress -Name $gatewayPublicIpName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AllocationMethod Dynamic
    $gatewayIpConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $gatewayIpConfigName `
        -Subnet $gatewaySubnet `
        -PublicIpAddress $gatewayPublicIp

    # Get hello certificate info
    # Get hello full path in case a relative path was passed
    $rootCertFile = Get-ChildItem $rootCert
    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($rootCertFile)
    $certBase64 = [System.Convert]::ToBase64String($cert.RawData)
    $p2sRootCert = New-AzureRmVpnClientRootCertificate -Name $vpnRootCertName `
        -PublicCertData $certBase64

    # Create hello VPN gateway
    New-AzureRmVirtualNetworkGateway -Name $vpnName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -IpConfigurations $gatewayIpConfig `
        -GatewayType Vpn `
        -VpnType RouteBased `
        -EnableBgp $false `
        -GatewaySku Standard `
        -VpnClientAddressPool $vpnClientAddressPool `
        -VpnClientRootCertificates $p2sRootCert
    ```

    > [!WARNING]
    > Он может занять несколько минут для toocomplete этот процесс.

5. Используйте следующий код toocreate hello учетной записи хранилища Azure и BLOB-контейнере hello.

    ```powershell
    # Create hello storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $storageName `
        -Type Standard_GRS `
        -Location $location

    # Get hello storage account keys and create a context
    $defaultStorageKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName `
        -Name $storageName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageName `
        -StorageAccountKey $defaultStorageKey

    # Create hello default storage container
    New-AzureStorageContainer -Name $defaultContainerName `
        -Context $storageContext
    ```

6. Используйте следующие кластера HDInsight hello toocreate кода hello.

    ```powershell
    # Create hello HDInsight cluster
    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $hdiWorkerNodes `
        -ClusterType $hdiType `
        -OSType Linux `
        -Version $hdiVersion `
        -HttpCredential $adminCreds `
        -SshCredential $sshCreds `
        -DefaultStorageAccountName "$storageName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageKey `
        -DefaultStorageContainer $defaultContainerName `
        -VirtualNetworkId $network.Id `
        -SubnetName $defaultSubnet.Id
    ```

  > [!WARNING]
  > Этот процесс занимает около 20 минут toocomplete.

8. Используйте следующий командлет tooretrieve hello URL-адрес клиента VPN в Windows hello для виртуальной сети hello hello.

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    toodownload hello VPN-клиента Windows, используйте hello возвращается URI в веб-браузере.

### <a name="configure-kafka-for-ip-advertising"></a>Настройка Kafka для объявления IP-адресов

По умолчанию Zookeeper возвращает имя домена hello hello tooclients брокеров Kafka. Эта конфигурация не работает с hello VPN-клиента программного обеспечения, как он не может использовать разрешение имен для сущностей в виртуальной сети hello. Для этой конфигурации необходимо использовать следующие hello tooconfigure действия Kafka tooadvertise IP адресов, а не имена домена:

1. С помощью веб-браузер, перейти toohttps://CLUSTERNAME.azurehdinsight.net. Замените __CLUSTERNAME__ с именем hello hello Kafka в кластере HDInsight.

    При появлении запроса используйте hello HTTPS имя и пароль пользователя для кластера hello. отображается Hello Ambari веб-интерфейса для hello кластера.

2. Выберите tooview сведения о Kafka, __Kafka__ из списка hello слева hello.

    ![Список служб с выделенной службой Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. Выберите tooview конфигурации Kafka __Configs__ из средней верхней hello.

    ![Ссылка на пункт "Configs" (Конфигурации) для Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. toofind hello __kafka env__ конфигурации, введите `kafka-env` в hello __фильтра__ в правом верхнем углу hello.

    ![Конфигурация Kafka, kafka-env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. tooconfigure Kafka tooadvertise IP адреса, добавьте следующий текст toohello внизу hello hello __kafka env шаблона__ поля:

    ```
    # Configure Kafka tooadvertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. Введите tooconfigure hello интерфейс, который прослушивает Kafka `listeners` в hello __фильтра__ в правом верхнем углу hello.

7. tooconfigure toolisten Kafka по всем сетевым интерфейсам, изменение значения hello в hello __прослушиватели__ поле слишком`PLAINTEXT://0.0.0.0:9092`.

8. изменения конфигурации toosave hello, использовать hello __Сохранить__ кнопки. Введите текстовое сообщение, описывающее изменения hello. Выберите __ОК__ после сохранения изменений hello.

    ![Кнопка сохранения конфигурации](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. ошибки tooprevent при перезапуске Kafka, использовать hello __действий службы__ и выберите пункт __включить в режим обслуживания__. Выберите ОК toocomplete этой операции.

    ![Кнопка "Service Actions" (Действия со службой) с выделенной командой "Turn On Maintenance Mode" (Включить режим обслуживания)](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. toorestart Kafka, использовать hello __перезапустите__ и выберите пункт __перезапуска все затронутые__. Подтвердить перезапуск hello, а затем использовать hello __ОК__ кнопку после завершения операции hello.

    ![Кнопка "Restart" (Перезапустить) с выделенной командой "Restart All Affected" (Перезапустить все затронутые)](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. режим обслуживания toodisable, используйте hello __действий службы__ и выберите пункт __включить выключение режима обслуживания__. Выберите **ОК** toocomplete этой операции.

### <a name="connect-toohello-vpn-gateway"></a>Шлюз VPN toohello подключения

шлюз VPN toohello tooconnect из __клиента Windows__, использовать hello __подключения tooAzure__ раздел hello [настроить подключение точка-сеть](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) документа.

## <a id="python-client"></a> Пример: клиент Python

tooKafka toovalidate подключения, используйте следующие шаги toocreate hello и выполните Python производитель и потребитель.

1. Используйте один из hello следующие методы tooretrieve hello полностью полное доменное имя (FQDN) и IP-адреса узлов hello в hello Kafka кластера:

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

    Этот сценарий предполагает, что `$resourceGroupName` является именем hello hello группы ресурсов Azure, которая содержит hello виртуальной сети.

    Сохраните hello, возвращаются сведения для использования в hello дальнейшие действия.

2. Используйте hello, следуя tooinstall hello [kafka python](http://kafka-python.readthedocs.io/) клиента:

        pip install kafka-python

3. tooKafka toosend данных, используйте hello после кода Python:

  ```python
  from kafka import KafkaProducer
  # Replace hello `ip_address` entries with hello IP address of your worker nodes
  # NOTE: you don't need hello full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    Замените hello `'kafka_broker'` записи с адресами hello, возвращенного в шаге 1 в этом разделе:

    * При использовании __программного обеспечения VPN-клиента__, замените hello `kafka_broker` операции с IP-адрес вашего рабочих узлов hello.

    * Если у вас есть __включено разрешение имен через пользовательского DNS-сервера__, замените hello `kafka_broker` записей с hello hello рабочих узлов полное доменное имя.

    > [!NOTE]
    > Этот код отправляет строку hello `test message` toohello разделе `testtopic`. Конфигурация по умолчанию Hello Kafka на HDInsight — тема hello toocreate, если он не существует.

4. сообщения hello tooretrieve Kafka hello используйте следующий код Python:

   ```python
   from kafka import KafkaConsumer
   # Replace hello `ip_address` entries with hello IP address of your worker nodes
   # Again, you only need one or two, not hello full list.
   # Note: auto_offset_reset='earliest' resets hello starting offset toohello beginning
   #       of hello topic
   consumer = KafkaConsumer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'],auto_offset_reset='earliest')
   consumer.subscribe(['testtopic'])
   for msg in consumer:
     print (msg)
   ```

    Замените hello `'kafka_broker'` записи с адресами hello, возвращенного в шаге 1 в этом разделе:

    * При использовании __программного обеспечения VPN-клиента__, замените hello `kafka_broker` операции с IP-адрес вашего рабочих узлов hello.

    * Если у вас есть __включено разрешение имен через пользовательского DNS-сервера__, замените hello `kafka_broker` записей с hello hello рабочих узлов полное доменное имя.

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения об использовании HDInsight с помощью виртуальной сети см. в разделе hello [расширить Azure HDInsight с помощью виртуальной сети Azure](hdinsight-extend-hadoop-virtual-network.md) документа.

См. Дополнительные сведения о создании виртуальной сети Azure со шлюзом VPN точки сайтами hello следующие документы:

* [Настроить подключение точка-сеть с помощью портала Azure hello](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [Настройка подключения типа "точка — сеть" к виртуальной сети с помощью PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

См. Дополнительные сведения о работе с Kafka на HDInsight hello следующие документы:

* [Get started with Apache Kafka on HDInsight (preview)](hdinsight-apache-kafka-get-started.md) (Приступая к работе с Apache Kafka в HDInsight (предварительная версия))
* [Создание реплики Kafka в кластере HDInsight с помощью MirrorMaker (предварительная версия)](hdinsight-apache-kafka-mirroring.md)
