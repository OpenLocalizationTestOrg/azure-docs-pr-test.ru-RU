---
title: "Подключение к Kafka с помощью виртуальных сетей в Azure HDInsight | Документация Майкрософт"
description: "Узнайте, как подключиться напрямую к Kafka в HDInsight с помощью виртуальной сети Azure. Узнайте, как подключиться к Kafka из клиентов разработки с помощью шлюза VPN или из клиентов в локальной сети, используя устройство шлюза VPN."
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
ms.openlocfilehash: 245bee7c1dbb0236afdc2506e7ab84b5573cbc85
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-kafka-on-hdinsight-preview-through-an-azure-virtual-network"></a><span data-ttu-id="67b42-104">Подключение к Kafka HDInsight (предварительная версия) с помощью виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="67b42-104">Connect to Kafka on HDInsight (preview) through an Azure Virtual Network</span></span>

<span data-ttu-id="67b42-105">Узнайте, как напрямую подключиться к Kafka в HDInsight с помощью виртуальных сетей Azure.</span><span class="sxs-lookup"><span data-stu-id="67b42-105">Learn how to directly connect to Kafka on HDInsight using Azure Virtual Networks.</span></span> <span data-ttu-id="67b42-106">В этой статье приведены сведения о подключении к Kafka с использованием приведенных ниже конфигураций.</span><span class="sxs-lookup"><span data-stu-id="67b42-106">This document provides information on connecting to Kafka using the following configurations:</span></span>

* <span data-ttu-id="67b42-107">Из ресурсов в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="67b42-107">From resources in an on-premises network.</span></span> <span data-ttu-id="67b42-108">Это подключение устанавливается с помощью VPN-устройства (программного или аппаратного) в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="67b42-108">This connection is established by using a VPN device (software or hardware) on your local network.</span></span>
* <span data-ttu-id="67b42-109">Из среды разработки с помощью программного VPN-клиента.</span><span class="sxs-lookup"><span data-stu-id="67b42-109">From a development environment using a VPN software client.</span></span>

## <a name="architecture-and-planning"></a><span data-ttu-id="67b42-110">Архитектура и планирование</span><span class="sxs-lookup"><span data-stu-id="67b42-110">Architecture and planning</span></span>

<span data-ttu-id="67b42-111">HDInsight не разрешает прямое подключение к Kafka через общедоступный Интернет.</span><span class="sxs-lookup"><span data-stu-id="67b42-111">HDInsight does not allow direct connection to Kafka over the public internet.</span></span> <span data-ttu-id="67b42-112">Вместо этого клиенты Kafka (производители и потребители) должны использовать один из следующих методов подключения.</span><span class="sxs-lookup"><span data-stu-id="67b42-112">Instead, Kafka clients (producers and consumers) must use one of the following connection methods:</span></span>

* <span data-ttu-id="67b42-113">Запустите клиент в той же виртуальной сети, что и Kafka в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="67b42-113">Run the client in the same virtual network as Kafka on HDInsight.</span></span> <span data-ttu-id="67b42-114">Сведения об использовании этой конфигурации см. в статье [Приступая к работе с Apache Kafka (предварительная версия) в HDInsight](hdinsight-apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="67b42-114">This configuration is used in the [Start with Apache Kafka (preview) on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span> <span data-ttu-id="67b42-115">Клиент работает непосредственно на узлах кластера HDInsight или на другой виртуальной машине в той же сети.</span><span class="sxs-lookup"><span data-stu-id="67b42-115">The client runs directly on the HDInsight cluster nodes or on another virtual machine in the same network.</span></span>

* <span data-ttu-id="67b42-116">Подключите частную сеть, например локальную, к виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="67b42-116">Connect a private network, such as your on-premises network, to the virtual network.</span></span> <span data-ttu-id="67b42-117">Эта конфигурация разрешает клиентам в локальной сети напрямую работать с Kafka.</span><span class="sxs-lookup"><span data-stu-id="67b42-117">This configuration allows clients in your on-premises network to directly work with Kafka.</span></span> <span data-ttu-id="67b42-118">Чтобы включить эту конфигурацию, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="67b42-118">To enable this configuration, perform the following tasks:</span></span>

    1. <span data-ttu-id="67b42-119">Создайте виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="67b42-119">Create a virtual network.</span></span>
    2. <span data-ttu-id="67b42-120">Создайте VPN-шлюз, использующий конфигурацию типа "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="67b42-120">Create a VPN gateway that uses a site-to-site configuration.</span></span> <span data-ttu-id="67b42-121">Конфигурация, используемая в этой статье, подключается к устройству шлюза VPN в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="67b42-121">The configuration used in this document connects to a VPN gateway device in your on-premises network.</span></span>
    3. <span data-ttu-id="67b42-122">Создайте DNS-сервер в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="67b42-122">Create a DNS server in the virtual network.</span></span>
    4. <span data-ttu-id="67b42-123">Настройте переадресацию между DNS-серверами в каждой сети.</span><span class="sxs-lookup"><span data-stu-id="67b42-123">Configure forwarding between the DNS server in each network.</span></span>
    5. <span data-ttu-id="67b42-124">Установите Kafka HDInsight в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="67b42-124">Install Kafka on HDInsight into the virtual network.</span></span>

    <span data-ttu-id="67b42-125">Дополнительные сведения см. в разделе [Подключение к Kafka из локальной сети](#on-premises).</span><span class="sxs-lookup"><span data-stu-id="67b42-125">For more information, see the [Connect to Kafka from an on-premises network](#on-premises) section.</span></span> 

* <span data-ttu-id="67b42-126">Подключите отдельные виртуальные машины к виртуальной сети с помощью VPN-шлюза и VPN-клиента.</span><span class="sxs-lookup"><span data-stu-id="67b42-126">Connect individual machines to the virtual network using a VPN gateway and VPN client.</span></span> <span data-ttu-id="67b42-127">Чтобы включить эту конфигурацию, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="67b42-127">To enable this configuration, perform the following tasks:</span></span>

    1. <span data-ttu-id="67b42-128">Создайте виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="67b42-128">Create a virtual network.</span></span>
    2. <span data-ttu-id="67b42-129">Создайте VPN-шлюз, использующий конфигурацию типа "точка — сеть".</span><span class="sxs-lookup"><span data-stu-id="67b42-129">Create a VPN gateway that uses a point-to-site configuration.</span></span> <span data-ttu-id="67b42-130">Такая конфигурация предоставляет VPN-клиент, который можно установить на клиентах Windows.</span><span class="sxs-lookup"><span data-stu-id="67b42-130">This configuration provides a VPN client that can be installed on Windows clients.</span></span>
    3. <span data-ttu-id="67b42-131">Установите Kafka HDInsight в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="67b42-131">Install Kafka on HDInsight into the virtual network.</span></span>
    4. <span data-ttu-id="67b42-132">Настройте Kafka для объявления IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="67b42-132">Configure Kafka for IP advertising.</span></span> <span data-ttu-id="67b42-133">Такая конфигурация позволяет клиенту подключаться с помощью IP-адресов вместо доменных имен.</span><span class="sxs-lookup"><span data-stu-id="67b42-133">This configuration allows the client to connect using IP addressing instead of domain names.</span></span>
    5. <span data-ttu-id="67b42-134">Скачайте и используйте VPN-клиент в системе разработки.</span><span class="sxs-lookup"><span data-stu-id="67b42-134">Download and use the VPN client on the development system.</span></span>

    <span data-ttu-id="67b42-135">Дополнительные сведения см. в разделе [Подключение к Kafka с помощью VPN-клиента](#vpnclient).</span><span class="sxs-lookup"><span data-stu-id="67b42-135">For more information, see the [Connect to Kafka with a VPN client](#vpnclient) section.</span></span>

    > [!WARNING]
    > <span data-ttu-id="67b42-136">Эта конфигурация рекомендуется только для целей разработки из-за следующих ограничений:</span><span class="sxs-lookup"><span data-stu-id="67b42-136">This configuration is only recommended for development purposes because of the following limitations:</span></span>
    >
    > * <span data-ttu-id="67b42-137">Каждый клиент должен подключиться с помощью программного VPN-клиента.</span><span class="sxs-lookup"><span data-stu-id="67b42-137">Each client must connect using a VPN software client.</span></span> <span data-ttu-id="67b42-138">Azure предоставляет только клиент Windows.</span><span class="sxs-lookup"><span data-stu-id="67b42-138">Azure only provides a Windows-based client.</span></span>
    > * <span data-ttu-id="67b42-139">Клиент не передает запросы на разрешения имен в виртуальную сеть, поэтому для обмена данными с Kafka необходимо использовать IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="67b42-139">The client does not pass name resolution requests to the virtual network, so you must use IP addressing to communicate with Kafka.</span></span> <span data-ttu-id="67b42-140">Для взаимодействия с IP-адресом требуется дополнительная настройка кластера Kafka.</span><span class="sxs-lookup"><span data-stu-id="67b42-140">IP communication requires additional configuration on the Kafka cluster.</span></span>

<span data-ttu-id="67b42-141">Дополнительные сведения об использовании HDInsight в виртуальной сети см. в статье [Расширение возможностей HDInsight с помощью виртуальной сети Azure](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="67b42-141">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <span data-ttu-id="67b42-142"><a id="on-premises"></a> Подключение к Kafka из локальной сети</span><span class="sxs-lookup"><span data-stu-id="67b42-142"><a id="on-premises"></a> Connect to Kafka from an on-premises network</span></span>

<span data-ttu-id="67b42-143">Чтобы создать кластер Kafka, который взаимодействует с локальной сетью, выполните действия, описанные в статье [Подключение HDInsight к локальной сети](./connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="67b42-143">To create a Kafka cluster that communicates with your on-premises network, follow the steps in the [Connect HDInsight to your on-premises network](./connect-on-premises-network.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67b42-144">При создании кластера HDInsight выберите тип кластера __Kafka__.</span><span class="sxs-lookup"><span data-stu-id="67b42-144">When creating the HDInsight cluster, select the __Kafka__ cluster type.</span></span>

<span data-ttu-id="67b42-145">Выполнив эти действия, вы создадите следующую конфигурацию:</span><span class="sxs-lookup"><span data-stu-id="67b42-145">These steps create the following configuration:</span></span>

* <span data-ttu-id="67b42-146">Виртуальная сеть Azure</span><span class="sxs-lookup"><span data-stu-id="67b42-146">Azure Virtual Network</span></span>
* <span data-ttu-id="67b42-147">VPN-шлюз типа "сеть — сеть";</span><span class="sxs-lookup"><span data-stu-id="67b42-147">Site-to-site VPN gateway</span></span>
* <span data-ttu-id="67b42-148">учетная запись хранения Azure (используемая HDInsight);</span><span class="sxs-lookup"><span data-stu-id="67b42-148">Azure Storage account (used by HDInsight)</span></span>
* <span data-ttu-id="67b42-149">Kafka HDInsight</span><span class="sxs-lookup"><span data-stu-id="67b42-149">Kafka on HDInsight</span></span>

<span data-ttu-id="67b42-150">Чтобы убедиться, что клиент Kafka может подключиться к кластеру из локальной сети, ознакомьтесь с разделом [Пример: клиент Python](#python-client).</span><span class="sxs-lookup"><span data-stu-id="67b42-150">To verify that a Kafka client can connect to the cluster from on-premises, use the steps in the [Example: Python client](#python-client) section.</span></span>

## <span data-ttu-id="67b42-151"><a id="vpnclient"></a> Подключение к Kafka с помощью VPN-клиента</span><span class="sxs-lookup"><span data-stu-id="67b42-151"><a id="vpnclient"></a> Connect to Kafka with a VPN client</span></span>

<span data-ttu-id="67b42-152">В этом разделе описаны действия по созданию следующей конфигурации:</span><span class="sxs-lookup"><span data-stu-id="67b42-152">Use the steps in this section to create the following configuration:</span></span>

* <span data-ttu-id="67b42-153">Виртуальная сеть Azure</span><span class="sxs-lookup"><span data-stu-id="67b42-153">Azure Virtual Network</span></span>
* <span data-ttu-id="67b42-154">VPN-шлюз типа "точка — сеть"</span><span class="sxs-lookup"><span data-stu-id="67b42-154">Point-to-site VPN gateway</span></span>
* <span data-ttu-id="67b42-155">Учетная запись хранения Azure (используется HDInsight)</span><span class="sxs-lookup"><span data-stu-id="67b42-155">Azure Storage Account (used by HDInsight)</span></span>
* <span data-ttu-id="67b42-156">Kafka HDInsight</span><span class="sxs-lookup"><span data-stu-id="67b42-156">Kafka on HDInsight</span></span>

1. <span data-ttu-id="67b42-157">Дополнительные сведения см. в статье [Создание и экспорт сертификатов для подключений типа "точка — сеть" с помощью PowerShell в Windows 10](../vpn-gateway/vpn-gateway-certificates-point-to-site.md).</span><span class="sxs-lookup"><span data-stu-id="67b42-157">Follow the steps in the [Working with self-signed certificates for Point-to-site connections](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span></span> <span data-ttu-id="67b42-158">Там приведены действия по созданию сертификатов, необходимых для шлюза.</span><span class="sxs-lookup"><span data-stu-id="67b42-158">This document creates the certificates needed for the gateway.</span></span>

2. <span data-ttu-id="67b42-159">Откройте командную строку PowerShell и используйте следующий код, чтобы войти в подписку Azure:</span><span class="sxs-lookup"><span data-stu-id="67b42-159">Open a PowerShell prompt and use the following code to log in to your Azure subscription:</span></span>

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment to set the subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. <span data-ttu-id="67b42-160">Используйте следующий код, чтобы создать переменные, которые содержат сведения о конфигурации:</span><span class="sxs-lookup"><span data-stu-id="67b42-160">Use the following code to create variables that contain configuration information:</span></span>

    ```powershell
    # Prompt for generic information
    $resourceGroupName = Read-Host "What is the resource group name?"
    $baseName = Read-Host "What is the base name? It is used to create names for resources, such as 'net-basename' and 'kafka-basename':"
    $location = Read-Host "What Azure Region do you want to create the resources in?"
    $rootCert = Read-Host "What is the file path to the root certificate? It is used to secure the VPN gateway."

    # Prompt for HDInsight credentials
    $adminCreds = Get-Credential -Message "Enter the HTTPS user name and password for the HDInsight cluster" -UserName "admin"
    $sshCreds = Get-Credential -Message "Enter the SSH user name and password for the HDInsight cluster" -UserName "sshuser"

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

4. <span data-ttu-id="67b42-161">Используйте следующий код, чтобы создать группу ресурсов и виртуальную сеть Azure:</span><span class="sxs-lookup"><span data-stu-id="67b42-161">Use the following code to create the Azure resource group and virtual network:</span></span>

    ```powershell
    # Create the resource group that contains everything
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create the subnet configuration
    $defaultSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -AddressPrefix $defaultSubnetPrefix
    $gatewaySubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -AddressPrefix $gatewaySubnetPrefix

    # Create the subnet
    New-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AddressPrefix $networkAddressPrefix `
        -Subnet $defaultSubnetConfig, $gatewaySubnetConfig

    # Get the network & subnet that were created
    $network = Get-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName
    $gatewaySubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -VirtualNetwork $network
    $defaultSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -VirtualNetwork $network

    # Set a dynamic public IP address for the gateway subnet
    $gatewayPublicIp = New-AzureRmPublicIpAddress -Name $gatewayPublicIpName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AllocationMethod Dynamic
    $gatewayIpConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $gatewayIpConfigName `
        -Subnet $gatewaySubnet `
        -PublicIpAddress $gatewayPublicIp

    # Get the certificate info
    # Get the full path in case a relative path was passed
    $rootCertFile = Get-ChildItem $rootCert
    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($rootCertFile)
    $certBase64 = [System.Convert]::ToBase64String($cert.RawData)
    $p2sRootCert = New-AzureRmVpnClientRootCertificate -Name $vpnRootCertName `
        -PublicCertData $certBase64

    # Create the VPN gateway
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
    > <span data-ttu-id="67b42-162">Этот процесс может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="67b42-162">It can take several minutes for this process to complete.</span></span>

5. <span data-ttu-id="67b42-163">Используйте следующий код, чтобы создать учетную запись хранения Azure и контейнер BLOB-объектов:</span><span class="sxs-lookup"><span data-stu-id="67b42-163">Use the following code to create the Azure Storage Account and blob container:</span></span>

    ```powershell
    # Create the storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $storageName `
        -Type Standard_GRS `
        -Location $location

    # Get the storage account keys and create a context
    $defaultStorageKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName `
        -Name $storageName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageName `
        -StorageAccountKey $defaultStorageKey

    # Create the default storage container
    New-AzureStorageContainer -Name $defaultContainerName `
        -Context $storageContext
    ```

6. <span data-ttu-id="67b42-164">Используйте следующий код, чтобы создать кластер HDInsight:</span><span class="sxs-lookup"><span data-stu-id="67b42-164">Use the following code to create the HDInsight cluster:</span></span>

    ```powershell
    # Create the HDInsight cluster
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
  > <span data-ttu-id="67b42-165">Эта процедура занимает около 20 минут.</span><span class="sxs-lookup"><span data-stu-id="67b42-165">This process takes around 20 minutes to complete.</span></span>

8. <span data-ttu-id="67b42-166">Используйте следующий командлет, чтобы получить URL-адрес VPN-клиента Windows для виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="67b42-166">Use the following cmdlet to retrieve the URL for the Windows VPN client for the virtual network:</span></span>

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    <span data-ttu-id="67b42-167">Чтобы скачать VPN-клиент Windows, используйте возвращаемый универсальный код ресурса (URI) в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="67b42-167">To download the Windows VPN client, use the returned URI in your web browser.</span></span>

### <a name="configure-kafka-for-ip-advertising"></a><span data-ttu-id="67b42-168">Настройка Kafka для объявления IP-адресов</span><span class="sxs-lookup"><span data-stu-id="67b42-168">Configure Kafka for IP advertising</span></span>

<span data-ttu-id="67b42-169">По умолчанию Zookeeper возвращает клиентам доменное имя брокеров Kafka.</span><span class="sxs-lookup"><span data-stu-id="67b42-169">By default, Zookeeper returns the domain name of the Kafka brokers to clients.</span></span> <span data-ttu-id="67b42-170">Эта конфигурация не работает для программного VPN-клиента, так как он не может использовать разрешение имен для сущностей в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="67b42-170">This configuration does not work with the VPN software client, as it cannot use name resolution for entities in the virtual network.</span></span> <span data-ttu-id="67b42-171">Для этой конфигурации выполните следующие действия, чтобы настроить Kafka для объявления IP-адресов вместо доменных имен:</span><span class="sxs-lookup"><span data-stu-id="67b42-171">For this configuration, use the following steps to configure Kafka to advertise IP addresses instead of domain names:</span></span>

1. <span data-ttu-id="67b42-172">С помощью веб-браузера перейдите по адресу: https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="67b42-172">Using a web browser, go to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="67b42-173">Замените __CLUSTERNAME__ именем кластера Kafka HDInsight.</span><span class="sxs-lookup"><span data-stu-id="67b42-173">Replace __CLUSTERNAME__ with the name of the Kafka on HDInsight cluster.</span></span>

    <span data-ttu-id="67b42-174">При появлении запроса введите имя пользователя и пароль HTTPS для кластера.</span><span class="sxs-lookup"><span data-stu-id="67b42-174">When prompted, use the HTTPS user name and password for the cluster.</span></span> <span data-ttu-id="67b42-175">Отобразится веб-интерфейс Ambari для кластера.</span><span class="sxs-lookup"><span data-stu-id="67b42-175">The Ambari Web UI for the cluster is displayed.</span></span>

2. <span data-ttu-id="67b42-176">Чтобы просмотреть сведения о Kafka, из списка слева выберите __Kafka__.</span><span class="sxs-lookup"><span data-stu-id="67b42-176">To view information on Kafka, select __Kafka__ from the list on the left.</span></span>

    ![Список служб с выделенной службой Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. <span data-ttu-id="67b42-178">Чтобы просмотреть конфигурацию Kafka, выберите пункт __Configs__ (Конфигурации) в верхней части окна.</span><span class="sxs-lookup"><span data-stu-id="67b42-178">To view Kafka configuration, select __Configs__ from the top middle.</span></span>

    ![Ссылка на пункт "Configs" (Конфигурации) для Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. <span data-ttu-id="67b42-180">Чтобы найти конфигурацию __kafka-env__, введите `kafka-env` в поле __фильтра__ в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="67b42-180">To find the __kafka-env__ configuration, enter `kafka-env` in the __Filter__ field on the upper right.</span></span>

    ![Конфигурация Kafka, kafka-env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. <span data-ttu-id="67b42-182">Чтобы настроить Kafka для объявления IP-адресов, добавьте следующий текст в нижнюю часть поля __kafka-env template__ (шаблон kafka-env):</span><span class="sxs-lookup"><span data-stu-id="67b42-182">To configure Kafka to advertise IP addresses, add the following text to the bottom of the __kafka-env-template__ field:</span></span>

    ```
    # Configure Kafka to advertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. <span data-ttu-id="67b42-183">Чтобы настроить интерфейс, через который Kafka ожидает передачи данных, введите `listeners` в поле __фильтра__ в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="67b42-183">To configure the interface that Kafka listens on, enter `listeners` in the __Filter__ field on the upper right.</span></span>

7. <span data-ttu-id="67b42-184">Чтобы настроить Kafka для ожидания передачи данных через все сетевые интерфейсы, измените значение в поле __listeners__ на `PLAINTEXT://0.0.0.0:9092`.</span><span class="sxs-lookup"><span data-stu-id="67b42-184">To configure Kafka to listen on all network interfaces, change the value in the __listeners__ field to `PLAINTEXT://0.0.0.0:9092`.</span></span>

8. <span data-ttu-id="67b42-185">Нажмите кнопку __Save__ (Сохранить), чтобы сохранить изменения в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="67b42-185">To save the configuration changes, use the __Save__ button.</span></span> <span data-ttu-id="67b42-186">Введите текст, описывающий изменения.</span><span class="sxs-lookup"><span data-stu-id="67b42-186">Enter a text message describing the changes.</span></span> <span data-ttu-id="67b42-187">После сохранения изменений нажмите кнопку __ОК__.</span><span class="sxs-lookup"><span data-stu-id="67b42-187">Select __OK__ once the changes have been saved.</span></span>

    ![Кнопка сохранения конфигурации](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. <span data-ttu-id="67b42-189">Для предотвращения ошибок при перезапуске Kafka нажмите кнопку __Service Actions__ (Действия со службой) и выберите __Turn On Maintenance Mode__ (Включить режим обслуживания).</span><span class="sxs-lookup"><span data-stu-id="67b42-189">To prevent errors when restarting Kafka, use the __Service Actions__ button and select __Turn On Maintenance Mode__.</span></span> <span data-ttu-id="67b42-190">Чтобы завершить эту операцию, нажмите кнопку "ОК".</span><span class="sxs-lookup"><span data-stu-id="67b42-190">Select OK to complete this operation.</span></span>

    ![Кнопка "Service Actions" (Действия со службой) с выделенной командой "Turn On Maintenance Mode" (Включить режим обслуживания)](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. <span data-ttu-id="67b42-192">Чтобы перезапустить Kafka, нажмите кнопку __Restart__ (Перезапустить) и выберите __Restart All Affected__ (Перезапустить все затронутые).</span><span class="sxs-lookup"><span data-stu-id="67b42-192">To restart Kafka, use the __Restart__ button and select __Restart All Affected__.</span></span> <span data-ttu-id="67b42-193">Подтвердите перезапуск, а после завершения операции нажмите кнопку __ОК__.</span><span class="sxs-lookup"><span data-stu-id="67b42-193">Confirm the restart, and then use the __OK__ button after the operation has completed.</span></span>

    ![Кнопка "Restart" (Перезапустить) с выделенной командой "Restart All Affected" (Перезапустить все затронутые)](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. <span data-ttu-id="67b42-195">Чтобы отключить режим обслуживания нажмите кнопку __Service Actions__ (Действия со службой) и выберите __Turn Off Maintenance Mode__ (Отключить режим обслуживания).</span><span class="sxs-lookup"><span data-stu-id="67b42-195">To disable maintenance mode, use the __Service Actions__ button and select __Turn Off Maintenance Mode__.</span></span> <span data-ttu-id="67b42-196">Чтобы завершить эту операцию, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="67b42-196">Select **OK** to complete this operation.</span></span>

### <a name="connect-to-the-vpn-gateway"></a><span data-ttu-id="67b42-197">Подключение к VPN-шлюзу</span><span class="sxs-lookup"><span data-stu-id="67b42-197">Connect to the VPN gateway</span></span>

<span data-ttu-id="67b42-198">Для подключения к VPN-шлюзу из __клиента Windows__ используйте раздел __Подключение к Azure__ статьи [Настройка подключения типа "точка — сеть" к виртуальной сети с помощью PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate).</span><span class="sxs-lookup"><span data-stu-id="67b42-198">To connect to the VPN gateway from a __Windows client__, use the __Connect to Azure__ section of the [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.</span></span>

## <span data-ttu-id="67b42-199"><a id="python-client"></a> Пример: клиент Python</span><span class="sxs-lookup"><span data-stu-id="67b42-199"><a id="python-client"></a> Example: Python client</span></span>

<span data-ttu-id="67b42-200">Чтобы проверить подключение к Kafka, выполните следующие действия для создания и запуска производителя и потребителя Python:</span><span class="sxs-lookup"><span data-stu-id="67b42-200">To validate connectivity to Kafka, use the following steps to create and run a Python producer and consumer:</span></span>

1. <span data-ttu-id="67b42-201">Чтобы получить полное доменное имя (FQDN) и IP-адреса узлов кластера Kafka, используйте один из следующих методов.</span><span class="sxs-lookup"><span data-stu-id="67b42-201">Use one of the following methods to retrieve the fully qualified domain name (FQDN) and IP addresses of the nodes in the Kafka cluster:</span></span>

    ```powershell
    $resourceGroupName = "The resource group that contains the virtual network used with HDInsight"

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

    <span data-ttu-id="67b42-202">В этом сценарии предполагается, что `$resourceGroupName` — это имя группы ресурсов Azure, содержащей виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="67b42-202">This script assumes that `$resourceGroupName` is the name of the Azure resource group that contains the virtual network.</span></span>

    <span data-ttu-id="67b42-203">Сохраните полученные данные для использования на последующих шагах.</span><span class="sxs-lookup"><span data-stu-id="67b42-203">Save the returned information for use in the next steps.</span></span>

2. <span data-ttu-id="67b42-204">Чтобы установить клиент [kafka-python](http://kafka-python.readthedocs.io/), используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="67b42-204">Use the following to install the [kafka-python](http://kafka-python.readthedocs.io/) client:</span></span>

        pip install kafka-python

3. <span data-ttu-id="67b42-205">Чтобы отправить данные в Kafka, используйте следующий код Python:</span><span class="sxs-lookup"><span data-stu-id="67b42-205">To send data to Kafka, use the following Python code:</span></span>

  ```python
  from kafka import KafkaProducer
  # Replace the `ip_address` entries with the IP address of your worker nodes
  # NOTE: you don't need the full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    <span data-ttu-id="67b42-206">Замените записи `'kafka_broker'` адресами, полученными на шаге 1 этого раздела.</span><span class="sxs-lookup"><span data-stu-id="67b42-206">Replace the `'kafka_broker'` entries with the addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="67b42-207">При использовании __программного VPN-клиента__ замените записи `kafka_broker` IP-адресом рабочих узлов.</span><span class="sxs-lookup"><span data-stu-id="67b42-207">If you are using a __Software VPN client__, replace the `kafka_broker` entries with the IP address of your worker nodes.</span></span>

    * <span data-ttu-id="67b42-208">Если вы включили __разрешение имен через пользовательский DNS-сервер__, замените записи `kafka_broker` полным доменным именем рабочих узлов.</span><span class="sxs-lookup"><span data-stu-id="67b42-208">If you have __enabled name resolution through a custom DNS server__, replace the `kafka_broker` entries with the FQDN of the worker nodes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="67b42-209">Этот код отправляет строку `test message` в раздел `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="67b42-209">This code sends the string `test message` to the topic `testtopic`.</span></span> <span data-ttu-id="67b42-210">По умолчанию Kafka HDInsight создает раздел, если он не существует.</span><span class="sxs-lookup"><span data-stu-id="67b42-210">The default configuration of Kafka on HDInsight is to create the topic if it does not exist.</span></span>

4. <span data-ttu-id="67b42-211">Для получения сообщений от Kafka используйте следующий код Python:</span><span class="sxs-lookup"><span data-stu-id="67b42-211">To retrieve the messages from Kafka, use the following Python code:</span></span>

   ```python
   from kafka import KafkaConsumer
   # Replace the `ip_address` entries with the IP address of your worker nodes
   # Again, you only need one or two, not the full list.
   # Note: auto_offset_reset='earliest' resets the starting offset to the beginning
   #       of the topic
   consumer = KafkaConsumer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'],auto_offset_reset='earliest')
   consumer.subscribe(['testtopic'])
   for msg in consumer:
     print (msg)
   ```

    <span data-ttu-id="67b42-212">Замените записи `'kafka_broker'` адресами, полученными на шаге 1 этого раздела.</span><span class="sxs-lookup"><span data-stu-id="67b42-212">Replace the `'kafka_broker'` entries with the addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="67b42-213">При использовании __программного VPN-клиента__ замените записи `kafka_broker` IP-адресом рабочих узлов.</span><span class="sxs-lookup"><span data-stu-id="67b42-213">If you are using a __Software VPN client__, replace the `kafka_broker` entries with the IP address of your worker nodes.</span></span>

    * <span data-ttu-id="67b42-214">Если вы включили __разрешение имен через пользовательский DNS-сервер__, замените записи `kafka_broker` полным доменным именем рабочих узлов.</span><span class="sxs-lookup"><span data-stu-id="67b42-214">If you have __enabled name resolution through a custom DNS server__, replace the `kafka_broker` entries with the FQDN of the worker nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67b42-215">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="67b42-215">Next steps</span></span>

<span data-ttu-id="67b42-216">Дополнительные сведения об использовании HDInsight c виртуальными сетями см. в статье [Расширение возможностей HDInsight с помощью виртуальной сети Azure](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="67b42-216">For more information on using HDInsight with a virtual network, see the [Extend Azure HDInsight using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

<span data-ttu-id="67b42-217">Дополнительные сведения о создании виртуальной сети Azure с VPN-шлюзом типа "точка — сеть" см. в следующих документах:</span><span class="sxs-lookup"><span data-stu-id="67b42-217">For more information on creating an Azure Virtual Network with Point-to-Site VPN gateway, see the following documents:</span></span>

* [<span data-ttu-id="67b42-218">Настройка подключения типа "точка — сеть" к виртуальной сети с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="67b42-218">Configure a Point-to-Site connection using the Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [<span data-ttu-id="67b42-219">Настройка подключения типа "точка — сеть" к виртуальной сети с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="67b42-219">Configure a Point-to-Site connection using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

<span data-ttu-id="67b42-220">Дополнительные сведения о работе с Kafka HDInsight см. в следующих документах:</span><span class="sxs-lookup"><span data-stu-id="67b42-220">For more information on working with Kafka on HDInsight, see the following documents:</span></span>

* <span data-ttu-id="67b42-221">[Get started with Apache Kafka on HDInsight (preview)](hdinsight-apache-kafka-get-started.md) (Приступая к работе с Apache Kafka в HDInsight (предварительная версия))</span><span class="sxs-lookup"><span data-stu-id="67b42-221">[Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md)</span></span>
* [<span data-ttu-id="67b42-222">Создание реплики Kafka в кластере HDInsight с помощью MirrorMaker (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="67b42-222">Use mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
