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
# <a name="connect-tookafka-on-hdinsight-preview-through-an-azure-virtual-network"></a><span data-ttu-id="c657a-104">Подключение через виртуальную сеть Azure tooKafka на HDInsight (Предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="c657a-104">Connect tooKafka on HDInsight (preview) through an Azure Virtual Network</span></span>

<span data-ttu-id="c657a-105">Узнайте, как toodirectly подключаться tooKafka на HDInsight с помощью виртуальных сетей Azure.</span><span class="sxs-lookup"><span data-stu-id="c657a-105">Learn how toodirectly connect tooKafka on HDInsight using Azure Virtual Networks.</span></span> <span data-ttu-id="c657a-106">Этот документ содержит сведения о подключении с помощью конфигурации hello tooKafka:</span><span class="sxs-lookup"><span data-stu-id="c657a-106">This document provides information on connecting tooKafka using hello following configurations:</span></span>

* <span data-ttu-id="c657a-107">Из ресурсов в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="c657a-107">From resources in an on-premises network.</span></span> <span data-ttu-id="c657a-108">Это подключение устанавливается с помощью VPN-устройства (программного или аппаратного) в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="c657a-108">This connection is established by using a VPN device (software or hardware) on your local network.</span></span>
* <span data-ttu-id="c657a-109">Из среды разработки с помощью программного VPN-клиента.</span><span class="sxs-lookup"><span data-stu-id="c657a-109">From a development environment using a VPN software client.</span></span>

## <a name="architecture-and-planning"></a><span data-ttu-id="c657a-110">Архитектура и планирование</span><span class="sxs-lookup"><span data-stu-id="c657a-110">Architecture and planning</span></span>

<span data-ttu-id="c657a-111">HDInsight не допускает tooKafka прямое подключение через hello общедоступный Интернет.</span><span class="sxs-lookup"><span data-stu-id="c657a-111">HDInsight does not allow direct connection tooKafka over hello public internet.</span></span> <span data-ttu-id="c657a-112">Вместо этого Kafka клиентов (отправителями и получателями) необходимо использовать один из hello следующие способы подключения:</span><span class="sxs-lookup"><span data-stu-id="c657a-112">Instead, Kafka clients (producers and consumers) must use one of hello following connection methods:</span></span>

* <span data-ttu-id="c657a-113">Запуск клиента hello в hello же виртуальной сети Kafka на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c657a-113">Run hello client in hello same virtual network as Kafka on HDInsight.</span></span> <span data-ttu-id="c657a-114">Эта конфигурация используется в hello [начинаться с Apache Kafka (Предварительная версия) на HDInsight](hdinsight-apache-kafka-get-started.md) документа.</span><span class="sxs-lookup"><span data-stu-id="c657a-114">This configuration is used in hello [Start with Apache Kafka (preview) on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span> <span data-ttu-id="c657a-115">Hello клиента запускается непосредственно hello HDInsight узлы кластера или на другой виртуальной машины в hello же сети.</span><span class="sxs-lookup"><span data-stu-id="c657a-115">hello client runs directly on hello HDInsight cluster nodes or on another virtual machine in hello same network.</span></span>

* <span data-ttu-id="c657a-116">Подключение частной сети, например в локальной сети, toohello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c657a-116">Connect a private network, such as your on-premises network, toohello virtual network.</span></span> <span data-ttu-id="c657a-117">Эта конфигурация позволяет клиентам в локальной сети toodirectly работу с Kafka.</span><span class="sxs-lookup"><span data-stu-id="c657a-117">This configuration allows clients in your on-premises network toodirectly work with Kafka.</span></span> <span data-ttu-id="c657a-118">tooenable этой конфигурации выполните hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="c657a-118">tooenable this configuration, perform hello following tasks:</span></span>

    1. <span data-ttu-id="c657a-119">Создайте виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="c657a-119">Create a virtual network.</span></span>
    2. <span data-ttu-id="c657a-120">Создайте VPN-шлюз, использующий конфигурацию типа "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="c657a-120">Create a VPN gateway that uses a site-to-site configuration.</span></span> <span data-ttu-id="c657a-121">Hello конфигурацию, используемую в этом документе подключается tooa устройство шлюза VPN в вашей локальной сети.</span><span class="sxs-lookup"><span data-stu-id="c657a-121">hello configuration used in this document connects tooa VPN gateway device in your on-premises network.</span></span>
    3. <span data-ttu-id="c657a-122">Создайте DNS-сервер в виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="c657a-122">Create a DNS server in hello virtual network.</span></span>
    4. <span data-ttu-id="c657a-123">Настройка перенаправления между hello DNS-сервера в каждой сети.</span><span class="sxs-lookup"><span data-stu-id="c657a-123">Configure forwarding between hello DNS server in each network.</span></span>
    5. <span data-ttu-id="c657a-124">Установите Kafka на HDInsight в виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="c657a-124">Install Kafka on HDInsight into hello virtual network.</span></span>

    <span data-ttu-id="c657a-125">Дополнительные сведения см. в разделе hello [подключение из локальной сети tooKafka](#on-premises) раздела.</span><span class="sxs-lookup"><span data-stu-id="c657a-125">For more information, see hello [Connect tooKafka from an on-premises network](#on-premises) section.</span></span> 

* <span data-ttu-id="c657a-126">Подключение отдельных машин toohello виртуальной сети с помощью шлюза VPN и VPN-клиента.</span><span class="sxs-lookup"><span data-stu-id="c657a-126">Connect individual machines toohello virtual network using a VPN gateway and VPN client.</span></span> <span data-ttu-id="c657a-127">tooenable этой конфигурации выполните hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="c657a-127">tooenable this configuration, perform hello following tasks:</span></span>

    1. <span data-ttu-id="c657a-128">Создайте виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="c657a-128">Create a virtual network.</span></span>
    2. <span data-ttu-id="c657a-129">Создайте VPN-шлюз, использующий конфигурацию типа "точка — сеть".</span><span class="sxs-lookup"><span data-stu-id="c657a-129">Create a VPN gateway that uses a point-to-site configuration.</span></span> <span data-ttu-id="c657a-130">Такая конфигурация предоставляет VPN-клиент, который можно установить на клиентах Windows.</span><span class="sxs-lookup"><span data-stu-id="c657a-130">This configuration provides a VPN client that can be installed on Windows clients.</span></span>
    3. <span data-ttu-id="c657a-131">Установите Kafka на HDInsight в виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="c657a-131">Install Kafka on HDInsight into hello virtual network.</span></span>
    4. <span data-ttu-id="c657a-132">Настройте Kafka для объявления IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="c657a-132">Configure Kafka for IP advertising.</span></span> <span data-ttu-id="c657a-133">Эта конфигурация обеспечивает tooconnect hello клиента, с помощью IP-адресов, а не имена доменов.</span><span class="sxs-lookup"><span data-stu-id="c657a-133">This configuration allows hello client tooconnect using IP addressing instead of domain names.</span></span>
    5. <span data-ttu-id="c657a-134">Загрузите и используйте hello VPN-клиента в системе разработки hello.</span><span class="sxs-lookup"><span data-stu-id="c657a-134">Download and use hello VPN client on hello development system.</span></span>

    <span data-ttu-id="c657a-135">Дополнительные сведения см. в разделе hello [подключения к VPN-клиент tooKafka](#vpnclient) раздела.</span><span class="sxs-lookup"><span data-stu-id="c657a-135">For more information, see hello [Connect tooKafka with a VPN client](#vpnclient) section.</span></span>

    > [!WARNING]
    > <span data-ttu-id="c657a-136">Эта конфигурация рекомендуется только для целей разработки из-за hello следующие ограничения:</span><span class="sxs-lookup"><span data-stu-id="c657a-136">This configuration is only recommended for development purposes because of hello following limitations:</span></span>
    >
    > * <span data-ttu-id="c657a-137">Каждый клиент должен подключиться с помощью программного VPN-клиента.</span><span class="sxs-lookup"><span data-stu-id="c657a-137">Each client must connect using a VPN software client.</span></span> <span data-ttu-id="c657a-138">Azure предоставляет только клиент Windows.</span><span class="sxs-lookup"><span data-stu-id="c657a-138">Azure only provides a Windows-based client.</span></span>
    > * <span data-ttu-id="c657a-139">Hello клиента не передает имя разрешения запросов toohello виртуальной сети, поэтому необходимо использовать IP-адресов с Kafka toocommunicate.</span><span class="sxs-lookup"><span data-stu-id="c657a-139">hello client does not pass name resolution requests toohello virtual network, so you must use IP addressing toocommunicate with Kafka.</span></span> <span data-ttu-id="c657a-140">Связи через пакеты Интеграции требуется дополнительная конфигурация кластера Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="c657a-140">IP communication requires additional configuration on hello Kafka cluster.</span></span>

<span data-ttu-id="c657a-141">Дополнительные сведения об использовании HDInsight в виртуальной сети см. в статье [Расширение возможностей HDInsight с помощью виртуальной сети Azure](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="c657a-141">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <span data-ttu-id="c657a-142"><a id="on-premises"></a>Подключение tooKafka из локальной сети</span><span class="sxs-lookup"><span data-stu-id="c657a-142"><a id="on-premises"></a> Connect tooKafka from an on-premises network</span></span>

<span data-ttu-id="c657a-143">toocreate Kafka кластера, который обменивается данными с вашей локальной сети, выполните действия hello в hello [HDInsight подключения tooyour локальной сети](./connect-on-premises-network.md) документа.</span><span class="sxs-lookup"><span data-stu-id="c657a-143">toocreate a Kafka cluster that communicates with your on-premises network, follow hello steps in hello [Connect HDInsight tooyour on-premises network](./connect-on-premises-network.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c657a-144">При создании кластера HDInsight hello выберите hello __Kafka__ кластера типа.</span><span class="sxs-lookup"><span data-stu-id="c657a-144">When creating hello HDInsight cluster, select hello __Kafka__ cluster type.</span></span>

<span data-ttu-id="c657a-145">Эти шаги создают hello следующая конфигурация:</span><span class="sxs-lookup"><span data-stu-id="c657a-145">These steps create hello following configuration:</span></span>

* <span data-ttu-id="c657a-146">Виртуальная сеть Azure</span><span class="sxs-lookup"><span data-stu-id="c657a-146">Azure Virtual Network</span></span>
* <span data-ttu-id="c657a-147">VPN-шлюз типа "сеть — сеть";</span><span class="sxs-lookup"><span data-stu-id="c657a-147">Site-to-site VPN gateway</span></span>
* <span data-ttu-id="c657a-148">учетная запись хранения Azure (используемая HDInsight);</span><span class="sxs-lookup"><span data-stu-id="c657a-148">Azure Storage account (used by HDInsight)</span></span>
* <span data-ttu-id="c657a-149">Kafka HDInsight</span><span class="sxs-lookup"><span data-stu-id="c657a-149">Kafka on HDInsight</span></span>

<span data-ttu-id="c657a-150">что toohello кластера может подключаться клиент Kafka от локальной, используйте шаги hello hello tooverify [пример: клиента Python](#python-client) раздела.</span><span class="sxs-lookup"><span data-stu-id="c657a-150">tooverify that a Kafka client can connect toohello cluster from on-premises, use hello steps in hello [Example: Python client](#python-client) section.</span></span>

## <span data-ttu-id="c657a-151"><a id="vpnclient"></a>Подключение tooKafka с VPN-клиента</span><span class="sxs-lookup"><span data-stu-id="c657a-151"><a id="vpnclient"></a> Connect tooKafka with a VPN client</span></span>

<span data-ttu-id="c657a-152">Выполните шаги hello в этот раздел toocreate hello, следующая конфигурация.</span><span class="sxs-lookup"><span data-stu-id="c657a-152">Use hello steps in this section toocreate hello following configuration:</span></span>

* <span data-ttu-id="c657a-153">Виртуальная сеть Azure</span><span class="sxs-lookup"><span data-stu-id="c657a-153">Azure Virtual Network</span></span>
* <span data-ttu-id="c657a-154">VPN-шлюз типа "точка — сеть"</span><span class="sxs-lookup"><span data-stu-id="c657a-154">Point-to-site VPN gateway</span></span>
* <span data-ttu-id="c657a-155">Учетная запись хранения Azure (используется HDInsight)</span><span class="sxs-lookup"><span data-stu-id="c657a-155">Azure Storage Account (used by HDInsight)</span></span>
* <span data-ttu-id="c657a-156">Kafka HDInsight</span><span class="sxs-lookup"><span data-stu-id="c657a-156">Kafka on HDInsight</span></span>

1. <span data-ttu-id="c657a-157">Следуйте указаниям hello hello [работа с самозаверяющие сертификаты для подключений точки сайтами](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) документа.</span><span class="sxs-lookup"><span data-stu-id="c657a-157">Follow hello steps in hello [Working with self-signed certificates for Point-to-site connections](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span></span> <span data-ttu-id="c657a-158">В этом документе создает hello сертификаты, необходимые для шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="c657a-158">This document creates hello certificates needed for hello gateway.</span></span>

2. <span data-ttu-id="c657a-159">Открыть командную строку PowerShell и используйте следующий код toolog в tooyour подписки Azure hello:</span><span class="sxs-lookup"><span data-stu-id="c657a-159">Open a PowerShell prompt and use hello following code toolog in tooyour Azure subscription:</span></span>

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment tooset hello subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. <span data-ttu-id="c657a-160">Используйте следующие hello кода toocreate переменные, содержащие сведения о конфигурации:</span><span class="sxs-lookup"><span data-stu-id="c657a-160">Use hello following code toocreate variables that contain configuration information:</span></span>

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

4. <span data-ttu-id="c657a-161">Используйте hello следующий код группы ресурсов Azure toocreate hello и виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="c657a-161">Use hello following code toocreate hello Azure resource group and virtual network:</span></span>

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
    > <span data-ttu-id="c657a-162">Он может занять несколько минут для toocomplete этот процесс.</span><span class="sxs-lookup"><span data-stu-id="c657a-162">It can take several minutes for this process toocomplete.</span></span>

5. <span data-ttu-id="c657a-163">Используйте следующий код toocreate hello учетной записи хранилища Azure и BLOB-контейнере hello.</span><span class="sxs-lookup"><span data-stu-id="c657a-163">Use hello following code toocreate hello Azure Storage Account and blob container:</span></span>

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

6. <span data-ttu-id="c657a-164">Используйте следующие кластера HDInsight hello toocreate кода hello.</span><span class="sxs-lookup"><span data-stu-id="c657a-164">Use hello following code toocreate hello HDInsight cluster:</span></span>

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
  > <span data-ttu-id="c657a-165">Этот процесс занимает около 20 минут toocomplete.</span><span class="sxs-lookup"><span data-stu-id="c657a-165">This process takes around 20 minutes toocomplete.</span></span>

8. <span data-ttu-id="c657a-166">Используйте следующий командлет tooretrieve hello URL-адрес клиента VPN в Windows hello для виртуальной сети hello hello.</span><span class="sxs-lookup"><span data-stu-id="c657a-166">Use hello following cmdlet tooretrieve hello URL for hello Windows VPN client for hello virtual network:</span></span>

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    <span data-ttu-id="c657a-167">toodownload hello VPN-клиента Windows, используйте hello возвращается URI в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="c657a-167">toodownload hello Windows VPN client, use hello returned URI in your web browser.</span></span>

### <a name="configure-kafka-for-ip-advertising"></a><span data-ttu-id="c657a-168">Настройка Kafka для объявления IP-адресов</span><span class="sxs-lookup"><span data-stu-id="c657a-168">Configure Kafka for IP advertising</span></span>

<span data-ttu-id="c657a-169">По умолчанию Zookeeper возвращает имя домена hello hello tooclients брокеров Kafka.</span><span class="sxs-lookup"><span data-stu-id="c657a-169">By default, Zookeeper returns hello domain name of hello Kafka brokers tooclients.</span></span> <span data-ttu-id="c657a-170">Эта конфигурация не работает с hello VPN-клиента программного обеспечения, как он не может использовать разрешение имен для сущностей в виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="c657a-170">This configuration does not work with hello VPN software client, as it cannot use name resolution for entities in hello virtual network.</span></span> <span data-ttu-id="c657a-171">Для этой конфигурации необходимо использовать следующие hello tooconfigure действия Kafka tooadvertise IP адресов, а не имена домена:</span><span class="sxs-lookup"><span data-stu-id="c657a-171">For this configuration, use hello following steps tooconfigure Kafka tooadvertise IP addresses instead of domain names:</span></span>

1. <span data-ttu-id="c657a-172">С помощью веб-браузер, перейти toohttps://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="c657a-172">Using a web browser, go toohttps://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="c657a-173">Замените __CLUSTERNAME__ с именем hello hello Kafka в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c657a-173">Replace __CLUSTERNAME__ with hello name of hello Kafka on HDInsight cluster.</span></span>

    <span data-ttu-id="c657a-174">При появлении запроса используйте hello HTTPS имя и пароль пользователя для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="c657a-174">When prompted, use hello HTTPS user name and password for hello cluster.</span></span> <span data-ttu-id="c657a-175">отображается Hello Ambari веб-интерфейса для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="c657a-175">hello Ambari Web UI for hello cluster is displayed.</span></span>

2. <span data-ttu-id="c657a-176">Выберите tooview сведения о Kafka, __Kafka__ из списка hello слева hello.</span><span class="sxs-lookup"><span data-stu-id="c657a-176">tooview information on Kafka, select __Kafka__ from hello list on hello left.</span></span>

    ![Список служб с выделенной службой Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. <span data-ttu-id="c657a-178">Выберите tooview конфигурации Kafka __Configs__ из средней верхней hello.</span><span class="sxs-lookup"><span data-stu-id="c657a-178">tooview Kafka configuration, select __Configs__ from hello top middle.</span></span>

    ![Ссылка на пункт "Configs" (Конфигурации) для Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. <span data-ttu-id="c657a-180">toofind hello __kafka env__ конфигурации, введите `kafka-env` в hello __фильтра__ в правом верхнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="c657a-180">toofind hello __kafka-env__ configuration, enter `kafka-env` in hello __Filter__ field on hello upper right.</span></span>

    ![Конфигурация Kafka, kafka-env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. <span data-ttu-id="c657a-182">tooconfigure Kafka tooadvertise IP адреса, добавьте следующий текст toohello внизу hello hello __kafka env шаблона__ поля:</span><span class="sxs-lookup"><span data-stu-id="c657a-182">tooconfigure Kafka tooadvertise IP addresses, add hello following text toohello bottom of hello __kafka-env-template__ field:</span></span>

    ```
    # Configure Kafka tooadvertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. <span data-ttu-id="c657a-183">Введите tooconfigure hello интерфейс, который прослушивает Kafka `listeners` в hello __фильтра__ в правом верхнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="c657a-183">tooconfigure hello interface that Kafka listens on, enter `listeners` in hello __Filter__ field on hello upper right.</span></span>

7. <span data-ttu-id="c657a-184">tooconfigure toolisten Kafka по всем сетевым интерфейсам, изменение значения hello в hello __прослушиватели__ поле слишком`PLAINTEXT://0.0.0.0:9092`.</span><span class="sxs-lookup"><span data-stu-id="c657a-184">tooconfigure Kafka toolisten on all network interfaces, change hello value in hello __listeners__ field too`PLAINTEXT://0.0.0.0:9092`.</span></span>

8. <span data-ttu-id="c657a-185">изменения конфигурации toosave hello, использовать hello __Сохранить__ кнопки.</span><span class="sxs-lookup"><span data-stu-id="c657a-185">toosave hello configuration changes, use hello __Save__ button.</span></span> <span data-ttu-id="c657a-186">Введите текстовое сообщение, описывающее изменения hello.</span><span class="sxs-lookup"><span data-stu-id="c657a-186">Enter a text message describing hello changes.</span></span> <span data-ttu-id="c657a-187">Выберите __ОК__ после сохранения изменений hello.</span><span class="sxs-lookup"><span data-stu-id="c657a-187">Select __OK__ once hello changes have been saved.</span></span>

    ![Кнопка сохранения конфигурации](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. <span data-ttu-id="c657a-189">ошибки tooprevent при перезапуске Kafka, использовать hello __действий службы__ и выберите пункт __включить в режим обслуживания__.</span><span class="sxs-lookup"><span data-stu-id="c657a-189">tooprevent errors when restarting Kafka, use hello __Service Actions__ button and select __Turn On Maintenance Mode__.</span></span> <span data-ttu-id="c657a-190">Выберите ОК toocomplete этой операции.</span><span class="sxs-lookup"><span data-stu-id="c657a-190">Select OK toocomplete this operation.</span></span>

    ![Кнопка "Service Actions" (Действия со службой) с выделенной командой "Turn On Maintenance Mode" (Включить режим обслуживания)](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. <span data-ttu-id="c657a-192">toorestart Kafka, использовать hello __перезапустите__ и выберите пункт __перезапуска все затронутые__.</span><span class="sxs-lookup"><span data-stu-id="c657a-192">toorestart Kafka, use hello __Restart__ button and select __Restart All Affected__.</span></span> <span data-ttu-id="c657a-193">Подтвердить перезапуск hello, а затем использовать hello __ОК__ кнопку после завершения операции hello.</span><span class="sxs-lookup"><span data-stu-id="c657a-193">Confirm hello restart, and then use hello __OK__ button after hello operation has completed.</span></span>

    ![Кнопка "Restart" (Перезапустить) с выделенной командой "Restart All Affected" (Перезапустить все затронутые)](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. <span data-ttu-id="c657a-195">режим обслуживания toodisable, используйте hello __действий службы__ и выберите пункт __включить выключение режима обслуживания__.</span><span class="sxs-lookup"><span data-stu-id="c657a-195">toodisable maintenance mode, use hello __Service Actions__ button and select __Turn Off Maintenance Mode__.</span></span> <span data-ttu-id="c657a-196">Выберите **ОК** toocomplete этой операции.</span><span class="sxs-lookup"><span data-stu-id="c657a-196">Select **OK** toocomplete this operation.</span></span>

### <a name="connect-toohello-vpn-gateway"></a><span data-ttu-id="c657a-197">Шлюз VPN toohello подключения</span><span class="sxs-lookup"><span data-stu-id="c657a-197">Connect toohello VPN gateway</span></span>

<span data-ttu-id="c657a-198">шлюз VPN toohello tooconnect из __клиента Windows__, использовать hello __подключения tooAzure__ раздел hello [настроить подключение точка-сеть](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) документа.</span><span class="sxs-lookup"><span data-stu-id="c657a-198">tooconnect toohello VPN gateway from a __Windows client__, use hello __Connect tooAzure__ section of hello [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.</span></span>

## <span data-ttu-id="c657a-199"><a id="python-client"></a> Пример: клиент Python</span><span class="sxs-lookup"><span data-stu-id="c657a-199"><a id="python-client"></a> Example: Python client</span></span>

<span data-ttu-id="c657a-200">tooKafka toovalidate подключения, используйте следующие шаги toocreate hello и выполните Python производитель и потребитель.</span><span class="sxs-lookup"><span data-stu-id="c657a-200">toovalidate connectivity tooKafka, use hello following steps toocreate and run a Python producer and consumer:</span></span>

1. <span data-ttu-id="c657a-201">Используйте один из hello следующие методы tooretrieve hello полностью полное доменное имя (FQDN) и IP-адреса узлов hello в hello Kafka кластера:</span><span class="sxs-lookup"><span data-stu-id="c657a-201">Use one of hello following methods tooretrieve hello fully qualified domain name (FQDN) and IP addresses of hello nodes in hello Kafka cluster:</span></span>

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

    <span data-ttu-id="c657a-202">Этот сценарий предполагает, что `$resourceGroupName` является именем hello hello группы ресурсов Azure, которая содержит hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c657a-202">This script assumes that `$resourceGroupName` is hello name of hello Azure resource group that contains hello virtual network.</span></span>

    <span data-ttu-id="c657a-203">Сохраните hello, возвращаются сведения для использования в hello дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="c657a-203">Save hello returned information for use in hello next steps.</span></span>

2. <span data-ttu-id="c657a-204">Используйте hello, следуя tooinstall hello [kafka python](http://kafka-python.readthedocs.io/) клиента:</span><span class="sxs-lookup"><span data-stu-id="c657a-204">Use hello following tooinstall hello [kafka-python](http://kafka-python.readthedocs.io/) client:</span></span>

        pip install kafka-python

3. <span data-ttu-id="c657a-205">tooKafka toosend данных, используйте hello после кода Python:</span><span class="sxs-lookup"><span data-stu-id="c657a-205">toosend data tooKafka, use hello following Python code:</span></span>

  ```python
  from kafka import KafkaProducer
  # Replace hello `ip_address` entries with hello IP address of your worker nodes
  # NOTE: you don't need hello full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    <span data-ttu-id="c657a-206">Замените hello `'kafka_broker'` записи с адресами hello, возвращенного в шаге 1 в этом разделе:</span><span class="sxs-lookup"><span data-stu-id="c657a-206">Replace hello `'kafka_broker'` entries with hello addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="c657a-207">При использовании __программного обеспечения VPN-клиента__, замените hello `kafka_broker` операции с IP-адрес вашего рабочих узлов hello.</span><span class="sxs-lookup"><span data-stu-id="c657a-207">If you are using a __Software VPN client__, replace hello `kafka_broker` entries with hello IP address of your worker nodes.</span></span>

    * <span data-ttu-id="c657a-208">Если у вас есть __включено разрешение имен через пользовательского DNS-сервера__, замените hello `kafka_broker` записей с hello hello рабочих узлов полное доменное имя.</span><span class="sxs-lookup"><span data-stu-id="c657a-208">If you have __enabled name resolution through a custom DNS server__, replace hello `kafka_broker` entries with hello FQDN of hello worker nodes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c657a-209">Этот код отправляет строку hello `test message` toohello разделе `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="c657a-209">This code sends hello string `test message` toohello topic `testtopic`.</span></span> <span data-ttu-id="c657a-210">Конфигурация по умолчанию Hello Kafka на HDInsight — тема hello toocreate, если он не существует.</span><span class="sxs-lookup"><span data-stu-id="c657a-210">hello default configuration of Kafka on HDInsight is toocreate hello topic if it does not exist.</span></span>

4. <span data-ttu-id="c657a-211">сообщения hello tooretrieve Kafka hello используйте следующий код Python:</span><span class="sxs-lookup"><span data-stu-id="c657a-211">tooretrieve hello messages from Kafka, use hello following Python code:</span></span>

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

    <span data-ttu-id="c657a-212">Замените hello `'kafka_broker'` записи с адресами hello, возвращенного в шаге 1 в этом разделе:</span><span class="sxs-lookup"><span data-stu-id="c657a-212">Replace hello `'kafka_broker'` entries with hello addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="c657a-213">При использовании __программного обеспечения VPN-клиента__, замените hello `kafka_broker` операции с IP-адрес вашего рабочих узлов hello.</span><span class="sxs-lookup"><span data-stu-id="c657a-213">If you are using a __Software VPN client__, replace hello `kafka_broker` entries with hello IP address of your worker nodes.</span></span>

    * <span data-ttu-id="c657a-214">Если у вас есть __включено разрешение имен через пользовательского DNS-сервера__, замените hello `kafka_broker` записей с hello hello рабочих узлов полное доменное имя.</span><span class="sxs-lookup"><span data-stu-id="c657a-214">If you have __enabled name resolution through a custom DNS server__, replace hello `kafka_broker` entries with hello FQDN of hello worker nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c657a-215">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c657a-215">Next steps</span></span>

<span data-ttu-id="c657a-216">Дополнительные сведения об использовании HDInsight с помощью виртуальной сети см. в разделе hello [расширить Azure HDInsight с помощью виртуальной сети Azure](hdinsight-extend-hadoop-virtual-network.md) документа.</span><span class="sxs-lookup"><span data-stu-id="c657a-216">For more information on using HDInsight with a virtual network, see hello [Extend Azure HDInsight using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

<span data-ttu-id="c657a-217">См. Дополнительные сведения о создании виртуальной сети Azure со шлюзом VPN точки сайтами hello следующие документы:</span><span class="sxs-lookup"><span data-stu-id="c657a-217">For more information on creating an Azure Virtual Network with Point-to-Site VPN gateway, see hello following documents:</span></span>

* [<span data-ttu-id="c657a-218">Настроить подключение точка-сеть с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="c657a-218">Configure a Point-to-Site connection using hello Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [<span data-ttu-id="c657a-219">Настройка подключения типа "точка — сеть" к виртуальной сети с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="c657a-219">Configure a Point-to-Site connection using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

<span data-ttu-id="c657a-220">См. Дополнительные сведения о работе с Kafka на HDInsight hello следующие документы:</span><span class="sxs-lookup"><span data-stu-id="c657a-220">For more information on working with Kafka on HDInsight, see hello following documents:</span></span>

* <span data-ttu-id="c657a-221">[Get started with Apache Kafka on HDInsight (preview)](hdinsight-apache-kafka-get-started.md) (Приступая к работе с Apache Kafka в HDInsight (предварительная версия))</span><span class="sxs-lookup"><span data-stu-id="c657a-221">[Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md)</span></span>
* [<span data-ttu-id="c657a-222">Создание реплики Kafka в кластере HDInsight с помощью MirrorMaker (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="c657a-222">Use mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
