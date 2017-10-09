---
title: "aaaCreate конфигурации multi-SID SAP в Azure | Документы Microsoft"
description: "Конфигурации multi-SID руководство toohigh доступности SAP NetWeaver на виртуальных машинах"
services: virtual-machines-windows, virtual-network, storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 0b89b4f8-6d6c-45d7-8d20-fe93430217ca
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e2a4b12928231743c59af86dab72595ad38d364b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-sap-netweaver-multi-sid-configuration"></a><span data-ttu-id="3353c-103">Создание конфигурации с несколькими идентификаторами безопасности SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="3353c-103">Create an SAP NetWeaver multi-SID configuration</span></span>

[load-balancer-multivip-overview]:../../../load-balancer/load-balancer-multivip-overview.md
[sap-ha-guide]:sap-high-availability-guide.md 
[sap-ha-guide-figure-6001]:./media/virtual-machines-shared-sap-high-availability-guide/6001-sap-multi-sid-ascs-scs-sid1.png
[sap-ha-guide-figure-6002]:./media/virtual-machines-shared-sap-high-availability-guide/6002-sap-multi-sid-ascs-scs.png
[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png
[sap-ha-guide-figure-6004]:./media/virtual-machines-shared-sap-high-availability-guide/6004-sap-multi-sid-dns.png
[sap-ha-guide-figure-6005]:./media/virtual-machines-shared-sap-high-availability-guide/6005-sap-multi-sid-azure-portal.png
[sap-ha-guide-figure-6006]:./media/virtual-machines-shared-sap-high-availability-guide/6006-sap-multi-sid-sios-replication.png
[networking-limits-azure-resource-manager]:../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits
[sap-ha-guide-9.1.1]:sap-high-availability-guide.md#a97ad604-9094-44fe-a364-f89cb39bf097 
[sap-ha-guide-8.8]:sap-high-availability-guide.md#f19bd997-154d-4583-a46e-7f5a69d0153c
[sap-ha-guide-8.12.3.3]:sap-high-availability-guide.md#d9c1fc8e-8710-4dff-bec2-1f535db7b006 
[sap-ha-guide-9]:sap-high-availability-guide.md#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:sap-high-availability-guide.md#31c6bd4f-51df-4057-9fdf-3fcbc619c170 
[sap-ha-guide-9.1.2]:sap-high-availability-guide.md#eb5af918-b42f-4803-bb50-eff41f84b0b0 
[sap-ha-guide-9.1.3]:sap-high-availability-guide.md#e4caaab2-e90f-4f2c-bc84-2cd2e12a9556 
[sap-ha-guide-9.1.4]:sap-high-availability-guide.md#10822f4f-32e7-4871-b63a-9b86c76ce761 
[sap-ha-guide-9.4]:sap-high-availability-guide.md#094bc895-31d4-4471-91cc-1513b64e406a 
[sap-ha-guide-9.5]:sap-high-availability-guide.md#2477e58f-c5a7-4a5d-9ae3-7b91022cafb5 
[sap-ha-guide-9.6]:sap-high-availability-guide.md#0ba4a6c1-cc37-4bcf-a8dc-025de4263772 
[sap-ha-guide-10]:sap-high-availability-guide.md#18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9

<span data-ttu-id="3353c-104">В сентябре 2016 г. корпорация Майкрософт выпустила функцию, которая дает возможность управлять несколькими виртуальными IP-адресами с помощью внутренней подсистемы балансировки нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="3353c-104">In September 2016, Microsoft released a feature where you can manage multiple virtual IP addresses by using an Azure internal load balancer.</span></span> <span data-ttu-id="3353c-105">Эта функция уже существует в hello Azure внешней подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="3353c-105">This functionality already exists in hello Azure external load balancer.</span></span>

<span data-ttu-id="3353c-106">При наличии развертывания SAP можно использовать toocreate подсистемы балансировки нагрузки внутренней конфигурации кластера Windows для SAP ASCS/SCS, как описано в hello [руководство для высокого уровня доступности SAP NetWeaver на виртуальных машинах Windows] [ sap-ha-guide].</span><span class="sxs-lookup"><span data-stu-id="3353c-106">If you have an SAP deployment, you can use an internal load balancer toocreate a Windows cluster configuration for SAP ASCS/SCS, as documented in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide].</span></span>

<span data-ttu-id="3353c-107">Эта статья посвящена как toomove из одного ASCS/SCS установки tooan SAP multi-SID конфигурации, установив дополнительные SAP ASCS/SCS кластеризованных экземпляров в существующий кластер сервера отказоустойчивой кластеризации Windows (WSFC).</span><span class="sxs-lookup"><span data-stu-id="3353c-107">This article focuses on how toomove from a single ASCS/SCS installation tooan SAP multi-SID configuration by installing additional SAP ASCS/SCS clustered instances into an existing Windows Server Failover Clustering (WSFC) cluster.</span></span> <span data-ttu-id="3353c-108">Выполнив эти действия, вы настроите кластер SAP с несколькими ИД безопасности.</span><span class="sxs-lookup"><span data-stu-id="3353c-108">When this process is completed, you will have configured an SAP multi-SID cluster.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="3353c-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3353c-109">Prerequisites</span></span>
<span data-ttu-id="3353c-110">Вы уже настроили кластер WSFC, который используется для одного экземпляра SAP ASCS/SCS, как описано в hello [руководство для высокого уровня доступности SAP NetWeaver на виртуальных машинах Windows] [ sap-ha-guide] и, как показано на этой диаграмме.</span><span class="sxs-lookup"><span data-stu-id="3353c-110">You have already configured a WSFC cluster that is used for one SAP ASCS/SCS instance, as discussed in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide] and as shown in this diagram.</span></span>

![Высокодоступный экземпляр SAP ASCS/SCS][sap-ha-guide-figure-6001]

## <a name="target-architecture"></a><span data-ttu-id="3353c-112">Целевая архитектура</span><span class="sxs-lookup"><span data-stu-id="3353c-112">Target architecture</span></span>

<span data-ttu-id="3353c-113">Hello цель — tooinstall несколько ABAP SAP ASCS или SAP Java SCS кластеризованных экземпляров в hello же кластера WSFC, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="3353c-113">hello goal is tooinstall multiple SAP ABAP ASCS or SAP Java SCS clustered instances in hello same WSFC cluster, as illustrated here:</span></span>

![Несколько кластеризованных экземпляров SAP ASCS/SCS в Azure][sap-ha-guide-figure-6002]

> [!NOTE]
><span data-ttu-id="3353c-115">Нет toohello предельное число частных IP-адресов интерфейса для каждого Azure внутренней подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="3353c-115">There is a limit toohello number of private front-end IPs for each Azure internal load balancer.</span></span>
>
><span data-ttu-id="3353c-116">Hello максимального числа экземпляров SAP ASCS/SCS в одном кластере WSFC — максимальное количество равно toohello частного IP-адреса переднего плана для каждого Azure внутренней подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="3353c-116">hello maximum number of SAP ASCS/SCS instances in one WSFC cluster is equal toohello maximum number of private front-end IPs for each Azure internal load balancer.</span></span>
>

<span data-ttu-id="3353c-117">Дополнительные сведения об ограничениях подсистемы балансировки нагрузки см. в пункте "Частный внешний IP-адрес на балансировщик нагрузки" раздела [Ограничения сети — Azure Resource Manager][networking-limits-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="3353c-117">For more information about load-balancer limits, see "Private front end IP per load balancer" in [Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager].</span></span>

<span data-ttu-id="3353c-118">Полный список Hello с двумя системами SAP высокого уровня доступности будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3353c-118">hello complete landscape with two high-availability SAP systems would look like this:</span></span>

![Установка SAP высокого уровня доступности с несколькими ИД безопасности и с двумя ИД безопасности системы SAP][sap-ha-guide-figure-6003]

> [!IMPORTANT]
> <span data-ttu-id="3353c-120">Программа установки Hello должен соответствовать hello следующие условия:</span><span class="sxs-lookup"><span data-stu-id="3353c-120">hello setup must meet hello following conditions:</span></span>
> - <span data-ttu-id="3353c-121">Hello SAP ASCS/SCS экземпляры должны совместно использовать hello же кластера WSFC.</span><span class="sxs-lookup"><span data-stu-id="3353c-121">hello SAP ASCS/SCS instances must share hello same WSFC cluster.</span></span>
> - <span data-ttu-id="3353c-122">Для каждого ИД безопасности СУБД должен быть выделен кластер WSFC.</span><span class="sxs-lookup"><span data-stu-id="3353c-122">Each DBMS SID must have its own dedicated WSFC cluster.</span></span>
> - <span data-ttu-id="3353c-123">Серверы приложений SAP, принадлежащих системе SAP tooone SID должен иметь свои собственные выделенные виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="3353c-123">SAP application servers that belong tooone SAP system SID must have their own dedicated VMs.</span></span>


## <a name="prepare-hello-infrastructure"></a><span data-ttu-id="3353c-124">Подготовка инфраструктуры hello</span><span class="sxs-lookup"><span data-stu-id="3353c-124">Prepare hello infrastructure</span></span>
<span data-ttu-id="3353c-125">tooprepare инфраструктуры, можно установить дополнительный экземпляр SAP ASCS/SCS с hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="3353c-125">tooprepare your infrastructure, you can install an additional SAP ASCS/SCS instance with hello following parameters:</span></span>

| <span data-ttu-id="3353c-126">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="3353c-126">Parameter name</span></span> | <span data-ttu-id="3353c-127">Значение</span><span class="sxs-lookup"><span data-stu-id="3353c-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3353c-128">ИД безопасности SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="3353c-128">SAP ASCS/SCS SID</span></span> |<span data-ttu-id="3353c-129">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="3353c-129">pr1-lb-ascs</span></span> |
| <span data-ttu-id="3353c-130">Внутренний балансировщик нагрузки экземпляра СУБД SAP</span><span class="sxs-lookup"><span data-stu-id="3353c-130">SAP DBMS internal load balancer</span></span> | <span data-ttu-id="3353c-131">PR5</span><span class="sxs-lookup"><span data-stu-id="3353c-131">PR5</span></span> |
| <span data-ttu-id="3353c-132">Имя виртуального узла SAP</span><span class="sxs-lookup"><span data-stu-id="3353c-132">SAP virtual host name</span></span> | <span data-ttu-id="3353c-133">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="3353c-133">pr5-sap-cl</span></span> |
| <span data-ttu-id="3353c-134">IP-адрес виртуального узла SAP ASCS/SCS (IP-адрес дополнительной подсистемы Azure Load Balancer)</span><span class="sxs-lookup"><span data-stu-id="3353c-134">SAP ASCS/SCS virtual host IP address (additional Azure load balancer IP address)</span></span> | <span data-ttu-id="3353c-135">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="3353c-135">10.0.0.50</span></span> |
| <span data-ttu-id="3353c-136">Количество экземпляров SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="3353c-136">SAP ASCS/SCS instance number</span></span> | <span data-ttu-id="3353c-137">50</span><span class="sxs-lookup"><span data-stu-id="3353c-137">50</span></span> |
| <span data-ttu-id="3353c-138">Порт пробы внутренней подсистемы балансировки нагрузки для дополнительного экземпляра SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="3353c-138">ILB probe port for additional SAP ASCS/SCS instance</span></span> | <span data-ttu-id="3353c-139">62350</span><span class="sxs-lookup"><span data-stu-id="3353c-139">62350</span></span> |

> [!NOTE]
> <span data-ttu-id="3353c-140">В случае с экземплярами кластера SAP ASCS/SCS каждому IP-адресу требуется уникальный порт пробы.</span><span class="sxs-lookup"><span data-stu-id="3353c-140">For SAP ASCS/SCS cluster instances, each IP address requires a unique probe port.</span></span> <span data-ttu-id="3353c-141">Например, если один IP-адрес во внутренней подсистеме балансировки нагрузки Azure использует порт пробы 62300, другой IP-адрес не может использовать этот порт.</span><span class="sxs-lookup"><span data-stu-id="3353c-141">For example, if one IP address on an Azure internal load balancer uses probe port 62300, no other IP address on that load balancer can use probe port 62300.</span></span>
>
><span data-ttu-id="3353c-142">Так как порт пробы 62300 уже зарезервирован, для наших целей мы используем порт пробы 62350.</span><span class="sxs-lookup"><span data-stu-id="3353c-142">For our purposes, because probe port 62300 is already reserved, we are using probe port 62350.</span></span>

<span data-ttu-id="3353c-143">Можно установить дополнительные экземпляры SAP ASCS/SCS hello существующего кластера WSFC, состоящие из двух узлов:</span><span class="sxs-lookup"><span data-stu-id="3353c-143">You can install additional SAP ASCS/SCS instances in hello existing WSFC cluster with two nodes:</span></span>

| <span data-ttu-id="3353c-144">Роль виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="3353c-144">Virtual machine role</span></span> | <span data-ttu-id="3353c-145">Имя узла виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="3353c-145">Virtual machine host name</span></span> | <span data-ttu-id="3353c-146">Статический IP-адрес</span><span class="sxs-lookup"><span data-stu-id="3353c-146">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3353c-147">1-й узел кластера для экземпляра ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="3353c-147">1st cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="3353c-148">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="3353c-148">pr1-ascs-0</span></span> |<span data-ttu-id="3353c-149">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="3353c-149">10.0.0.10</span></span> |
| <span data-ttu-id="3353c-150">2-й узел кластера для экземпляра ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="3353c-150">2nd cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="3353c-151">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="3353c-151">pr1-ascs-1</span></span> |<span data-ttu-id="3353c-152">10.0.0.9</span><span class="sxs-lookup"><span data-stu-id="3353c-152">10.0.0.9</span></span> |

### <a name="create-a-virtual-host-name-for-hello-clustered-sap-ascsscs-instance-on-hello-dns-server"></a><span data-ttu-id="3353c-153">Создание виртуального имени узла для экземпляра SAP ASCS/SCS hello clustered на DNS-сервере hello</span><span class="sxs-lookup"><span data-stu-id="3353c-153">Create a virtual host name for hello clustered SAP ASCS/SCS instance on hello DNS server</span></span>

<span data-ttu-id="3353c-154">Можно создать запись DNS для имени виртуального узла hello hello ASCS/SCS экземпляра с помощью hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="3353c-154">You can create a DNS entry for hello virtual host name of hello ASCS/SCS instance by using hello following parameters:</span></span>

| <span data-ttu-id="3353c-155">Новое имя виртуального узла SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="3353c-155">New SAP ASCS/SCS virtual host name</span></span> | <span data-ttu-id="3353c-156">Связанный IP-адрес</span><span class="sxs-lookup"><span data-stu-id="3353c-156">Associated IP address</span></span> |
| --- | --- | --- |
|<span data-ttu-id="3353c-157">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="3353c-157">pr5-sap-cl</span></span> |<span data-ttu-id="3353c-158">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="3353c-158">10.0.0.50</span></span> |

<span data-ttu-id="3353c-159">Hello новым именем узла и IP-адреса отображаются в hello диспетчер DNS, как показано на следующий снимок экрана приветствия:</span><span class="sxs-lookup"><span data-stu-id="3353c-159">hello new host name and IP address are displayed in hello DNS Manager, as shown in hello following screenshot:</span></span>

![Определить список диспетчер DNS, выделение hello запись DNS для hello новый SAP ASCS/SCS виртуальное имя кластера и TCP/IP-адрес][sap-ha-guide-figure-6004]

<span data-ttu-id="3353c-161">Hello процедура создания записи DNS является также подробно в главном hello [руководство для высокого уровня доступности SAP NetWeaver на виртуальных машинах Windows][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="3353c-161">hello procedure for creating a DNS entry is also described in detail in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9.1.1].</span></span>

> [!NOTE]
> <span data-ttu-id="3353c-162">Hello назначении toohello виртуальное имя узла экземпляра hello дополнительных ASCS/SCS новый IP-адрес должен быть hello то же, что новый IP-адрес hello назначенный toohello балансировки нагрузки Azure для SAP.</span><span class="sxs-lookup"><span data-stu-id="3353c-162">hello new IP address that you assign toohello virtual host name of hello additional ASCS/SCS instance must be hello same as hello new IP address that you assigned toohello SAP Azure load balancer.</span></span>
>
><span data-ttu-id="3353c-163">В нашем сценарии hello IP-адрес — 10.0.0.50.</span><span class="sxs-lookup"><span data-stu-id="3353c-163">In our scenario, hello IP address is 10.0.0.50.</span></span>

### <a name="add-an-ip-address-tooan-existing-azure-internal-load-balancer-by-using-powershell"></a><span data-ttu-id="3353c-164">Добавьте IP адрес tooan существующие внутренней балансировки нагрузки Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="3353c-164">Add an IP address tooan existing Azure internal load balancer by using PowerShell</span></span>

<span data-ttu-id="3353c-165">Здравствуйте, же WSFC toocreate более одного экземпляра SAP ASCS/SCS, в кластер, используйте PowerShell tooadd tooan IP адрес, существующие Azure внутренней подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="3353c-165">toocreate more than one SAP ASCS/SCS instance in hello same WSFC cluster, use PowerShell tooadd an IP address tooan existing Azure internal load balancer.</span></span> <span data-ttu-id="3353c-166">Каждому IP-адресу требуются собственные правила балансировки нагрузки, порт пробы, пул внешних IP-адресов и внутренний пул.</span><span class="sxs-lookup"><span data-stu-id="3353c-166">Each IP address requires its own load-balancing rules, probe port, front-end IP pool, and back-end pool.</span></span>

<span data-ttu-id="3353c-167">Hello следующий сценарий добавляет новый IP адрес tooan существующей подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="3353c-167">hello following script adds a new IP address tooan existing load balancer.</span></span> <span data-ttu-id="3353c-168">Обновите переменные PowerShell hello для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="3353c-168">Update hello PowerShell variables for your environment.</span></span> <span data-ttu-id="3353c-169">Hello скрипт создает все необходимые правила балансировки нагрузки для всех портов SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="3353c-169">hello script will create all needed load-balancing rules for all SAP ASCS/SCS ports.</span></span>

```powershell

# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>
Clear-Host
$ResourceGroupName = "SAP-MULTI-SID-Landscape"      # Existing resource group name
$VNetName = "pr2-vnet"                        # Existing virtual network name
$SubnetName = "Subnet"                        # Existing subnet name
$ILBName = "pr2-lb-ascs"                      # Existing ILB name                      
$ILBIP = "10.0.0.50"                          # New IP address
$VMNames = "pr2-ascs-0","pr2-ascs-1"          # Existing cluster virtual machine names
$SAPInstanceNumber = 50                       # SAP ASCS/SCS instance number: must be a unique value for each cluster
[int]$ProbePort = "623$SAPInstanceNumber"     # Probe port: must be a unique value for each IP and load balancer

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName

$count = $ILB.FrontendIpConfigurations.Count + 1
$FrontEndConfigurationName ="lbFrontendASCS$count"
$LBProbeName = "lbProbeASCS$count"

# Get hello Azure VNet and subnet
$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

# Add second front-end and probe configuration
Write-Host "Adding new front end IP Pool '$FrontEndConfigurationName' ..." -ForegroundColor Green
$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id
$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 10  | Set-AzureRmLoadBalancer

# Get new updated configuration
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
# Get new updated LP FrontendIP COnfig
$FEConfig = Get-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

# Add new back-end configuration into existing ILB
$BackEndConfigurationName  = "backendPoolASCS$count"
Write-Host "Adding new backend Pool '$BackEndConfigurationName' ..." -ForegroundColor Green
$BEConfig = Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB | Set-AzureRmLoadBalancer

# Get new updated config
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

# Assign VM NICs toobackend pool
$BEPool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
foreach($VMName in $VMNames){
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName
        $NICName = ($VM.NetworkInterfaceIDs[0].Split('/') | select -last 1)        
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName                
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools += $BEPool
        Write-Host "Assigning network card '$NICName' of hello '$VMName' VM toohello backend pool '$BackEndConfigurationName' ..." -ForegroundColor Green
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        #start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name
}


# Create load-balancing rules
$Ports = "445","32$SAPInstanceNumber","33$SAPInstanceNumber","36$SAPInstanceNumber","39$SAPInstanceNumber","5985","81$SAPInstanceNumber","5$SAPInstanceNumber`13","5$SAPInstanceNumber`14","5$SAPInstanceNumber`16"
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

Write-Host "Creating load balancing rules for hello ports: '$Ports' ... " -ForegroundColor Green

foreach ($Port in $Ports) {

        $LBConfigrulename = "lbrule$Port" + "_$count"
        Write-Host "Creating load balancing rule '$LBConfigrulename' for hello port '$Port' ..." -ForegroundColor Green

        $ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $HealthProbe -Protocol tcp -FrontendPort  $Port -BackendPort $Port -IdleTimeoutInMinutes 30 -LoadDistribution Default -EnableFloatingIP   
}

$ILB | Set-AzureRmLoadBalancer

Write-Host "Succesfully added new IP '$ILBIP' toohello internal load balancer '$ILBName'!" -ForegroundColor Green

```
<span data-ttu-id="3353c-170">После завершения выполнения сценария hello, hello, отображаются результаты hello портал Azure, как показано на следующий снимок экрана приветствия:</span><span class="sxs-lookup"><span data-stu-id="3353c-170">After hello script has run, hello results are displayed in hello Azure portal, as shown in hello following screenshot:</span></span>

![Новый пул интерфейсный IP в hello портал Azure][sap-ha-guide-figure-6005]

### <a name="add-disks-toocluster-machines-and-configure-hello-sios-cluster-share-disk"></a><span data-ttu-id="3353c-172">Добавление машины toocluster дисков и настройка диска общего ресурса кластера SIOS hello</span><span class="sxs-lookup"><span data-stu-id="3353c-172">Add disks toocluster machines, and configure hello SIOS cluster share disk</span></span>

<span data-ttu-id="3353c-173">Для каждого дополнительного экземпляра SAP ASCS/SCS необходимо добавить новый общий диск кластера.</span><span class="sxs-lookup"><span data-stu-id="3353c-173">You must add a new cluster share disk for each additional SAP ASCS/SCS instance.</span></span> <span data-ttu-id="3353c-174">Для Windows Server 2012 R2 диск общего ресурса кластера WSFC hello в настоящее время — hello SIOS DataKeeper программное решение.</span><span class="sxs-lookup"><span data-stu-id="3353c-174">For Windows Server 2012 R2, hello WSFC cluster share disk currently in use is hello SIOS DataKeeper software solution.</span></span>

<span data-ttu-id="3353c-175">Здравствуйте, следующие:</span><span class="sxs-lookup"><span data-stu-id="3353c-175">Do hello following:</span></span>
1. <span data-ttu-id="3353c-176">Добавить дополнительный диск или диски hello одинакового размера (необходимо toostripe) tooeach из hello узлы кластера и отформатировать его.</span><span class="sxs-lookup"><span data-stu-id="3353c-176">Add an additional disk or disks of hello same size (which you need toostripe) tooeach of hello cluster nodes, and format them.</span></span>
2. <span data-ttu-id="3353c-177">Настройте репликацию хранилища с помощью SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="3353c-177">Configure storage replication with SIOS DataKeeper.</span></span>

<span data-ttu-id="3353c-178">Эта процедура предполагает, что SIOS DataKeeper на машин кластера WSFC hello уже установлены.</span><span class="sxs-lookup"><span data-stu-id="3353c-178">This procedure assumes that you have already installed SIOS DataKeeper on hello WSFC cluster machines.</span></span> <span data-ttu-id="3353c-179">Если он установлен, теперь необходимо настроить репликацию между машинами hello.</span><span class="sxs-lookup"><span data-stu-id="3353c-179">If you have installed it, you must now configure replication between hello machines.</span></span> <span data-ttu-id="3353c-180">Hello процесс описан в главном hello подробно [руководство для высокого уровня доступности SAP NetWeaver на виртуальных машинах Windows][sap-ha-guide-8.12.3.3].</span><span class="sxs-lookup"><span data-stu-id="3353c-180">hello process is described in detail in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.12.3.3].</span></span>  

![DataKeeper синхронного зеркального отображения для hello новый диск SAP ASCS/SCS общей папки][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-dbms-cluster"></a><span data-ttu-id="3353c-182">Развертывание виртуальных машин для серверов приложений SAP и кластера СУБД</span><span class="sxs-lookup"><span data-stu-id="3353c-182">Deploy VMs for SAP application servers and DBMS cluster</span></span>

<span data-ttu-id="3353c-183">Подготовка инфраструктуры hello toocomplete для hello второй системы SAP, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="3353c-183">toocomplete hello infrastructure preparation for hello second SAP system, do hello following:</span></span>

1. <span data-ttu-id="3353c-184">Разверните выделенные виртуальные машины для серверов приложений SAP и поместите их в отдельную выделенную группу доступности.</span><span class="sxs-lookup"><span data-stu-id="3353c-184">Deploy dedicated VMs for SAP application servers and put them in their own dedicated availability group.</span></span>
2. <span data-ttu-id="3353c-185">Разверните выделенные виртуальные машины для кластера СУБД и поместите их в отдельную выделенную группу доступности.</span><span class="sxs-lookup"><span data-stu-id="3353c-185">Deploy dedicated VMs for DBMS cluster and put them in their own dedicated availability group.</span></span>


## <a name="install-hello-second-sap-sid2-netweaver-system"></a><span data-ttu-id="3353c-186">Установка второго системы SAP SID2 NetWeaver hello</span><span class="sxs-lookup"><span data-stu-id="3353c-186">Install hello second SAP SID2 NetWeaver system</span></span>

<span data-ttu-id="3353c-187">Hello завершения процесса установки второй системы SAP SID2 описан в главном hello [руководство для высокого уровня доступности SAP NetWeaver на виртуальных машинах Windows][sap-ha-guide-9].</span><span class="sxs-lookup"><span data-stu-id="3353c-187">hello complete process of installing a second SAP SID2 system is described in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9].</span></span>

<span data-ttu-id="3353c-188">высокоуровневые процедуры Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3353c-188">hello high-level procedure is as follows:</span></span>

1. <span data-ttu-id="3353c-189">[Установите первый узел кластера hello SAP][sap-ha-guide-9.1.2].</span><span class="sxs-lookup"><span data-stu-id="3353c-189">[Install hello SAP first cluster node][sap-ha-guide-9.1.2].</span></span>  
 <span data-ttu-id="3353c-190">На этом шаге вы устанавливаете SAP ASCS/SCS экземпляр высокой доступности на hello **СУЩЕСТВУЮЩИХ WSFC узлу кластера 1**.</span><span class="sxs-lookup"><span data-stu-id="3353c-190">In this step, you are installing SAP with a high-availability ASCS/SCS instance on hello **EXISTING WSFC cluster node 1**.</span></span>

2. <span data-ttu-id="3353c-191">[Изменение профиля hello SAP ASCS/SCS экземпляра hello][sap-ha-guide-9.1.3].</span><span class="sxs-lookup"><span data-stu-id="3353c-191">[Modify hello SAP profile of hello ASCS/SCS instance][sap-ha-guide-9.1.3].</span></span>

3. <span data-ttu-id="3353c-192">[Настройка порта пробы][sap-ha-guide-9.1.4].</span><span class="sxs-lookup"><span data-stu-id="3353c-192">[Configure a probe port][sap-ha-guide-9.1.4].</span></span>  
 <span data-ttu-id="3353c-193">На этом шаге настраивается порт пробы SAP-SID2-IP кластерного ресурса SAP с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3353c-193">In this step, you are configuring an SAP cluster resource SAP-SID2-IP probe port by using PowerShell.</span></span> <span data-ttu-id="3353c-194">Выполнение этой конфигурации на одном из узлов кластера SAP ASCS/SCS hello.</span><span class="sxs-lookup"><span data-stu-id="3353c-194">Execute this configuration on one of hello SAP ASCS/SCS cluster nodes.</span></span>

4. <span data-ttu-id="3353c-195">[Установка hello экземпляр базы данных] [sap-ha руководство-9.2].</span><span class="sxs-lookup"><span data-stu-id="3353c-195">[Install hello database instance][sap-ha-guide-9.2].</span></span>  
 <span data-ttu-id="3353c-196">На этом шаге в выделенном кластере WSFC устанавливается СУБД.</span><span class="sxs-lookup"><span data-stu-id="3353c-196">In this step, you are installing DBMS on a dedicated WSFC cluster.</span></span>

5. <span data-ttu-id="3353c-197">[Установка hello второго узла кластер] [sap-ha руководство-9.3].</span><span class="sxs-lookup"><span data-stu-id="3353c-197">[Install hello second cluster node][sap-ha-guide-9.3].</span></span>  
 <span data-ttu-id="3353c-198">На этом шаге вы устанавливаете SAP ASCS/SCS экземпляр высокой доступности на hello существующего узла WSFC 2.</span><span class="sxs-lookup"><span data-stu-id="3353c-198">In this step, you are installing SAP with a high-availability ASCS/SCS instance on hello existing WSFC cluster node 2.</span></span>

6. <span data-ttu-id="3353c-199">Открыть порты брандмауэра Windows для экземпляра SAP ASCS/SCS hello и ProbePort.</span><span class="sxs-lookup"><span data-stu-id="3353c-199">Open Windows Firewall ports for hello SAP ASCS/SCS instance and ProbePort.</span></span>  
 <span data-ttu-id="3353c-200">На обоих узлах кластера, используемых для экземпляров SAP ASCS/SCS, откройте все порты брандмауэра Windows, используемые SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="3353c-200">On both cluster nodes that are used for SAP ASCS/SCS instances, you are opening all Windows Firewall ports that are used by SAP ASCS/SCS.</span></span> <span data-ttu-id="3353c-201">Эти порты, перечислены в hello [руководство для высокого уровня доступности SAP NetWeaver на виртуальных машинах Windows][sap-ha-guide-8.8].</span><span class="sxs-lookup"><span data-stu-id="3353c-201">These ports are listed in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.8].</span></span>  
 <span data-ttu-id="3353c-202">Также можно откройте hello нагрузки Azure внутренней балансировки пробы портом 62350 в нашем сценарии.</span><span class="sxs-lookup"><span data-stu-id="3353c-202">Also open hello Azure internal load balancer probe port, which is 62350 in our scenario.</span></span>

7. <span data-ttu-id="3353c-203">[Изменить тип запуска hello экземпляра службы SAP ющих Методов Windows hello][sap-ha-guide-9.4].</span><span class="sxs-lookup"><span data-stu-id="3353c-203">[Change hello start type of hello SAP ERS Windows service instance][sap-ha-guide-9.4].</span></span>

8. <span data-ttu-id="3353c-204">[Установка сервера основного приложения SAP hello] [ sap-ha-guide-9.5] на hello новой выделенной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="3353c-204">[Install hello SAP primary application server][sap-ha-guide-9.5] on hello new dedicated VM.</span></span>

9. <span data-ttu-id="3353c-205">[Установка сервера дополнительное приложение hello SAP] [ sap-ha-guide-9.6] на hello новой выделенной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="3353c-205">[Install hello SAP additional application server][sap-ha-guide-9.6] on hello new dedicated VM.</span></span>

10. <span data-ttu-id="3353c-206">[Тестирование отработки отказа экземпляра SAP ASCS/SCS hello и репликации SIOS][sap-ha-guide-10].</span><span class="sxs-lookup"><span data-stu-id="3353c-206">[Test hello SAP ASCS/SCS instance failover and SIOS replication][sap-ha-guide-10].</span></span>

## <a name="next-steps"></a><span data-ttu-id="3353c-207">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3353c-207">Next steps</span></span>

- <span data-ttu-id="3353c-208">[Ограничения сети — Azure Resource Manager][networking-limits-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="3353c-208">[Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager]</span></span>
- <span data-ttu-id="3353c-209">[Несколько виртуальных IP-адресов для Azure Load Balancer][load-balancer-multivip-overview]</span><span class="sxs-lookup"><span data-stu-id="3353c-209">[Multiple VIPs for Azure Load Balancer][load-balancer-multivip-overview]</span></span>
- <span data-ttu-id="3353c-210">[SAP NetWeaver на виртуальных машинах Windows. Руководство по обеспечению высокого уровня доступности][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="3353c-210">[Guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide]</span></span>
