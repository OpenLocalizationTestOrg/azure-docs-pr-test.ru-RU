---
title: "Виртуальные машины высокой доступности для SAP NetWeaver aaaAzure | Документы Microsoft"
description: "Руководство по обеспечению высокого уровня доступности для SAP NetWeaver на виртуальных машинах Azure"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 662dd793390d7f6138b160ed86259d13391336aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-high-availability-for-sap-netweaver"></a><span data-ttu-id="e260a-103">Руководство по обеспечению высокого уровня доступности SAP NetWeaver на виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="e260a-103">Azure Virtual Machines high availability for SAP NetWeaver</span></span>

[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[sap-installation-guides]:http://service.sap.com/instguides

[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md

[deployment-guide]:deployment-guide.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md

[ha-guide]:sap-high-availability-guide.md

[planning-guide]:planning-guide.md
[planning-guide-11]:planning-guide.md
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10

[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[sap-ha-guide]:sap-high-availability-guide.md
[sap-ha-guide-2]:#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-4]:#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-8]:#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.9]:#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.11]:#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.3]:#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:#a97ad604-9094-44fe-a364-f89cb39bf097

[sap-ha-multi-sid-guide]:sap-high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:./media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:./media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:./media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:./media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:./media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:./media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:./media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:./media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:./media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:./media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:./media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:./media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:./media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:./media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:./media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:./media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:./media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:./media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:./media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:./media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:./media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:./media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:./media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:./media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:./media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:./media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:./media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:./media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:./media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:./media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:./media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:./media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:./media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:./media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:./media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:./media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:./media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:./media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:./media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:./media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:./media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:./media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:./media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:./media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:./media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:./media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:./media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:./media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:./media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:./media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:./media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:./media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:./media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:./media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:./media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:./media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:./media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:./media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:./media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:./media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:./media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:./media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:./media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps-md%2Fazuredeploy.json

[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager

[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md



<span data-ttu-id="e260a-109">Виртуальные машины Azure является hello решением для организаций, которым требуется вычислений, хранения и сетевые ресурсы, минимальное время и без длительных процессов поставки.</span><span class="sxs-lookup"><span data-stu-id="e260a-109">Azure Virtual Machines is hello solution for organizations that need compute, storage, and network resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="e260a-110">Можно использовать виртуальные машины Azure toodeploy классических приложений на основе SAP NetWeaver ABAP, Java и стек ABAP + Java.</span><span class="sxs-lookup"><span data-stu-id="e260a-110">You can use Azure Virtual Machines toodeploy classic applications like SAP NetWeaver-based ABAP, Java, and an ABAP+Java stack.</span></span> <span data-ttu-id="e260a-111">Повысьте уровень надежности и доступности без привлечения дополнительных локальных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e260a-111">Extend reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="e260a-112">Виртуальные машины Azure поддерживают распределенные подключения. Это позволяет интегрировать их в локальные домены, частные облака и системный ландшафт SAP вашей организации.</span><span class="sxs-lookup"><span data-stu-id="e260a-112">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="e260a-113">В этой статье мы рассмотрим hello действия, которые можно предпринять toodeploy высокого уровня доступности систем SAP в Azure с помощью модели развертывания диспетчера ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-113">In this article, we cover hello steps that you can take toodeploy high-availability SAP systems in Azure by using hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="e260a-114">Здесь рассматриваются следующие основные задачи:</span><span class="sxs-lookup"><span data-stu-id="e260a-114">We walk you through these major tasks:</span></span>

* <span data-ttu-id="e260a-115">Найти hello правой примечания по SAP и установки руководства, перечисленные в hello [ресурсов] [ sap-ha-guide-2] раздела.</span><span class="sxs-lookup"><span data-stu-id="e260a-115">Find hello right SAP Notes and installation guides, listed in hello [Resources][sap-ha-guide-2] section.</span></span> <span data-ttu-id="e260a-116">В этой статье дополняет документацию по установке SAP и примечания по SAP, которые являются hello основными ресурсами, которые могут помочь при установке и развертывании по SAP на конкретных платформах.</span><span class="sxs-lookup"><span data-stu-id="e260a-116">This article complements SAP installation documentation and SAP Notes, which are hello primary resources that can help you install and deploy SAP software on specific platforms.</span></span>
* <span data-ttu-id="e260a-117">Узнайте различия hello hello модели развертывания диспетчера ресурсов Azure и hello Azure классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="e260a-117">Learn hello differences between hello Azure Resource Manager deployment model and hello Azure classic deployment model.</span></span>
* <span data-ttu-id="e260a-118">Дополнительные сведения о отказоустойчивой кластеризации Windows Server режимы кворума, чтобы вы могли выбрать hello модели, которая подходит для развертывания в Azure.</span><span class="sxs-lookup"><span data-stu-id="e260a-118">Learn about Windows Server Failover Clustering quorum modes, so you can select hello model that is right for your Azure deployment.</span></span>
* <span data-ttu-id="e260a-119">Понимание принципов работы общего хранилища отказоустойчивого кластера Windows Server в Azure.</span><span class="sxs-lookup"><span data-stu-id="e260a-119">Learn about Windows Server Failover Clustering shared storage in Azure services.</span></span>
* <span data-ttu-id="e260a-120">Узнайте, как toohelp защиты компонентов одной точки из сбоя как расширенный бизнеса приложения программирования (ABAP) SAP центра служб (ASC) или центра служб SAP (SCS) и систем управления базами данных (СУБД) и избыточные компоненты, такие как SAP Сервер приложений в Azure.</span><span class="sxs-lookup"><span data-stu-id="e260a-120">Learn how toohelp protect single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server, in Azure.</span></span>
* <span data-ttu-id="e260a-121">Выполнение пошаговых инструкций по установке и настройке системы SAP с высоким уровнем доступности в отказоустойчивом кластере Windows Server в Azure с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e260a-121">Follow a step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure by using Azure Resource Manager.</span></span>
* <span data-ttu-id="e260a-122">Дополнительные сведения о дополнительных шагов требуется toouse отказоустойчивой кластеризации Windows Server в Azure, но не нужны в развертывании на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="e260a-122">Learn about additional steps required toouse Windows Server Failover Clustering in Azure, but which are not needed in an on-premises deployment.</span></span>

<span data-ttu-id="e260a-123">toosimplify развертывания и конфигурации, в этой статье мы используем hello шаблоны диспетчера ресурсов SAP трехуровневой высокого уровня доступности.</span><span class="sxs-lookup"><span data-stu-id="e260a-123">toosimplify deployment and configuration, in this article, we use hello SAP three-tier high-availability Resource Manager templates.</span></span> <span data-ttu-id="e260a-124">шаблоны Hello Автоматизация развертывания hello всей инфраструктуры, необходимый для высокого уровня доступности системы SAP.</span><span class="sxs-lookup"><span data-stu-id="e260a-124">hello templates automate deployment of hello entire infrastructure that you need for a high-availability SAP system.</span></span> <span data-ttu-id="e260a-125">Инфраструктура Hello также поддерживает изменение размеров SAP приложения производительности Standard (SAPS) системы SAP.</span><span class="sxs-lookup"><span data-stu-id="e260a-125">hello infrastructure also supports SAP Application Performance Standard (SAPS) sizing of your SAP system.</span></span>

## <span data-ttu-id="e260a-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e260a-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Prerequisites</span></span>
<span data-ttu-id="e260a-127">Прежде чем начать, убедитесь, что выполнены предварительные требования hello, описанные в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-127">Before you start, make sure that you meet hello prerequisites that are described in hello following sections.</span></span> <span data-ttu-id="e260a-128">Кроме того, следует убедиться, что toocheck все ресурсы, перечисленные в hello [ресурсов] [ sap-ha-guide-2] раздела.</span><span class="sxs-lookup"><span data-stu-id="e260a-128">Also, be sure toocheck all resources listed in hello [Resources][sap-ha-guide-2] section.</span></span>

<span data-ttu-id="e260a-129">В этой статье мы используем шаблоны Azure Resource Manager для [трехуровневой платформы SAP NetWeaver, использующей управляемые диски](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/).</span><span class="sxs-lookup"><span data-stu-id="e260a-129">In this article, we use Azure Resource Manager templates for [three-tier SAP NetWeaver using Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/).</span></span> <span data-ttu-id="e260a-130">Обзор шаблонов представлен в статье о [шаблонах Azure Resource Manager для SAP](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span><span class="sxs-lookup"><span data-stu-id="e260a-130">For a helpful overview of templates, see [SAP Azure Resource Manager templates](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span></span>

## <span data-ttu-id="e260a-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Материалы</span><span class="sxs-lookup"><span data-stu-id="e260a-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Resources</span></span>
<span data-ttu-id="e260a-132">Дополнительные сведения о развертывании SAP в Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="e260a-132">These articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="e260a-133">[SAP NetWeaver на виртуальных машинах Windows. Руководство по планированию и внедрению][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="e260a-133">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="e260a-134">[SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="e260a-134">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide]</span></span>
* <span data-ttu-id="e260a-135">[SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию СУБД][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="e260a-135">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
* <span data-ttu-id="e260a-136">[Руководство по обеспечению высокого уровня доступности SAP NetWeaver на виртуальных машинах Azure (это руководство)][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="e260a-136">[Azure Virtual Machines high availability for SAP NetWeaver (this guide)][sap-ha-guide]</span></span>

> [!NOTE]
> <span data-ttu-id="e260a-137">Когда это возможно, мы предоставим вам toohello связи, ссылающиеся на руководство по установке SAP (см. hello [руководства по установке SAP][sap-installation-guides]).</span><span class="sxs-lookup"><span data-stu-id="e260a-137">Whenever possible, we give you a link toohello referring SAP installation guide (see hello [SAP installation guides][sap-installation-guides]).</span></span> <span data-ttu-id="e260a-138">Предварительные условия и сведения о процессе установки hello, это всего установки SAP NetWeaver hello tooread рекомендуется тщательно проводит.</span><span class="sxs-lookup"><span data-stu-id="e260a-138">For prerequisites and information about hello installation process, it's a good idea tooread hello SAP NetWeaver installation guides carefully.</span></span> <span data-ttu-id="e260a-139">В этой статье рассматриваются только отдельные задачи для систем на основе SAP NetWeaver, устанавливаемых на виртуальные машины Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e260a-139">This article covers only specific tasks for SAP NetWeaver-based systems that you can use with Azure Virtual Machines.</span></span>
>
>

<span data-ttu-id="e260a-140">Примечания по SAP, связанные toohello тема SAP в Azure:</span><span class="sxs-lookup"><span data-stu-id="e260a-140">These SAP Notes are related toohello topic of SAP in Azure:</span></span>

| <span data-ttu-id="e260a-141">Номер примечания</span><span class="sxs-lookup"><span data-stu-id="e260a-141">Note number</span></span> | <span data-ttu-id="e260a-142">Название</span><span class="sxs-lookup"><span data-stu-id="e260a-142">Title</span></span> |
| --- | --- |
| <span data-ttu-id="e260a-143">[1928533]</span><span class="sxs-lookup"><span data-stu-id="e260a-143">[1928533]</span></span> |<span data-ttu-id="e260a-144">Приложения SAP в Azure: поддерживаемые продукты и размеры</span><span class="sxs-lookup"><span data-stu-id="e260a-144">SAP Applications on Azure: Supported Products and Sizing</span></span> |
| <span data-ttu-id="e260a-145">[2015553]</span><span class="sxs-lookup"><span data-stu-id="e260a-145">[2015553]</span></span> |<span data-ttu-id="e260a-146">SAP в Microsoft Azure: требования</span><span class="sxs-lookup"><span data-stu-id="e260a-146">SAP on Microsoft Azure: Support Prerequisites</span></span> |
| <span data-ttu-id="e260a-147">[1999351]</span><span class="sxs-lookup"><span data-stu-id="e260a-147">[1999351]</span></span> |<span data-ttu-id="e260a-148">Расширенный мониторинг Azure для SAP</span><span class="sxs-lookup"><span data-stu-id="e260a-148">Enhanced Azure Monitoring for SAP</span></span> |
| <span data-ttu-id="e260a-149">[2178632]</span><span class="sxs-lookup"><span data-stu-id="e260a-149">[2178632]</span></span> |<span data-ttu-id="e260a-150">Ключевые метрики мониторинга для SAP в Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e260a-150">Key Monitoring Metrics for SAP on Microsoft Azure</span></span> |
| <span data-ttu-id="e260a-151">[1999351]</span><span class="sxs-lookup"><span data-stu-id="e260a-151">[1999351]</span></span> |<span data-ttu-id="e260a-152">Виртуализация в Windows: расширенный мониторинг</span><span class="sxs-lookup"><span data-stu-id="e260a-152">Virtualization on Windows: Enhanced Monitoring</span></span> |
| <span data-ttu-id="e260a-153">[2243692]</span><span class="sxs-lookup"><span data-stu-id="e260a-153">[2243692]</span></span> |<span data-ttu-id="e260a-154">Использование хранилища SSD класса Premium Azure для экземпляра СУБД SAP</span><span class="sxs-lookup"><span data-stu-id="e260a-154">Use of Azure Premium SSD Storage for SAP DBMS Instance</span></span> |

<span data-ttu-id="e260a-155">Дополнительные сведения о hello [ограничения подписки Azure][azure-subscription-service-limits-subscription], включая ограничения по умолчанию общие и максимального ограничения.</span><span class="sxs-lookup"><span data-stu-id="e260a-155">Learn more about hello [limitations of Azure subscriptions][azure-subscription-service-limits-subscription], including general default limitations and maximum limitations.</span></span>

## <span data-ttu-id="e260a-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>Высокого уровня доступности SAP с помощью диспетчера ресурсов Azure и hello Azure классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="e260a-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>High-availability SAP with Azure Resource Manager vs. hello Azure classic deployment model</span></span>
<span data-ttu-id="e260a-157">в следующих областях hello различаются Hello диспетчера ресурсов Azure и Azure классическое развертывание моделей:</span><span class="sxs-lookup"><span data-stu-id="e260a-157">hello Azure Resource Manager and Azure classic deployment models are different in hello following areas:</span></span>

- <span data-ttu-id="e260a-158">Группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="e260a-158">Resource groups</span></span>
- <span data-ttu-id="e260a-159">Внутренняя Azure загрузить зависимость балансировки группы ресурсов Azure hello</span><span class="sxs-lookup"><span data-stu-id="e260a-159">Azure internal load balancer dependency on hello Azure resource group</span></span>
- <span data-ttu-id="e260a-160">Поддержка сценариев с несколькими идентификаторами безопасности SAP</span><span class="sxs-lookup"><span data-stu-id="e260a-160">Support for SAP multi-SID scenarios</span></span>

### <span data-ttu-id="e260a-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="e260a-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Resource groups</span></span>
<span data-ttu-id="e260a-162">В диспетчере ресурсов Azure можно использовать toomanage группы ресурсов все ресурсы приложения hello в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="e260a-162">In Azure Resource Manager, you can use resource groups toomanage all hello application resources in your Azure subscription.</span></span> <span data-ttu-id="e260a-163">Комплексный подход, в группе ресурсов, все ресурсы имеют hello же жизненного цикла.</span><span class="sxs-lookup"><span data-stu-id="e260a-163">An integrated approach, in a resource group, all resources have hello same life cycle.</span></span> <span data-ttu-id="e260a-164">Например, все ресурсы создаются в hello же времени и они удаляются при hello то же время.</span><span class="sxs-lookup"><span data-stu-id="e260a-164">For example, all resources are created at hello same time and they are deleted at hello same time.</span></span> <span data-ttu-id="e260a-165">Дополнительная информация о [группах ресурсов](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="e260a-165">Learn more about [resource groups](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

### <span data-ttu-id="e260a-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Внутренняя Azure загрузить зависимость балансировки группы ресурсов Azure hello</span><span class="sxs-lookup"><span data-stu-id="e260a-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Azure internal load balancer dependency on hello Azure resource group</span></span>

<span data-ttu-id="e260a-167">В hello Azure классической модели развертывания имеется зависимость между hello Azure внутренней подсистемы балансировки нагрузки (служба балансировки нагрузки Azure) и hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="e260a-167">In hello Azure classic deployment model, there is a dependency between hello Azure internal load balancer (Azure Load Balancer service) and hello cloud service.</span></span> <span data-ttu-id="e260a-168">Для каждого внутреннего балансировщика нагрузки требуется одна облачная служба.</span><span class="sxs-lookup"><span data-stu-id="e260a-168">Every internal load balancer needs one cloud service.</span></span>

<span data-ttu-id="e260a-169">В диспетчере ресурсов Azure каждый ресурс Azure должен toobe помещаются в группе ресурсов Azure и это также является допустимым для балансировки нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="e260a-169">In Azure Resource Manager, every Azure resource needs toobe placed into an Azure resource group, and this is valid for Azure Load Balancer as well.</span></span> <span data-ttu-id="e260a-170">Однако группы нет необходимости toohave один ресурс Azure на балансировки нагрузки Azure, например одну группу ресурсов Azure может содержать несколько подсистем балансировки нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="e260a-170">However, there is no need toohave one Azure resource group per Azure load balancer, e.g. one Azure resource group can contain multiple Azure Load Balancers.</span></span> <span data-ttu-id="e260a-171">Среда Hello стало проще и гибче.</span><span class="sxs-lookup"><span data-stu-id="e260a-171">hello environment is simpler and more flexible.</span></span> 

### <a name="support-for-sap-multi-sid-scenarios"></a><span data-ttu-id="e260a-172">Поддержка сценариев с несколькими идентификаторами безопасности SAP</span><span class="sxs-lookup"><span data-stu-id="e260a-172">Support for SAP multi-SID scenarios</span></span>

<span data-ttu-id="e260a-173">В модели Azure Resource Manager в одном кластере можно установить несколько экземпляров SAP ASCS/SCS с системными идентификаторами (идентификаторами безопасности).</span><span class="sxs-lookup"><span data-stu-id="e260a-173">In Azure Resource Manager, you can install multiple SAP system identifier (SID) ASCS/SCS instances in one cluster.</span></span> <span data-ttu-id="e260a-174">Это возможно за счет поддержки каждым внутренним балансировщиком нагрузки Azure нескольких IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="e260a-174">Multi-SID instances are possible because of support for multiple IP addresses for each Azure internal load balancer.</span></span>

<span data-ttu-id="e260a-175">toouse hello Azure классической модели развертывания, выполните описанные hello в [SAP NetWeaver в Azure: кластеризации SAP ASCS/SCS экземпляров с помощью отказоустойчивой кластеризации Windows Server в Azure с помощью sios DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span><span class="sxs-lookup"><span data-stu-id="e260a-175">toouse hello Azure classic deployment model, follow hello procedures described in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e260a-176">Настоятельно рекомендуется использовать модель развертывания диспетчера ресурсов Azure hello для установленных приложений SAP.</span><span class="sxs-lookup"><span data-stu-id="e260a-176">We strongly recommend that you use hello Azure Resource Manager deployment model for your SAP installations.</span></span> <span data-ttu-id="e260a-177">Он предлагает множество преимуществ, которые недоступны в hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="e260a-177">It offers many benefits that are not available in hello classic deployment model.</span></span> <span data-ttu-id="e260a-178">Дополнительные сведения о моделях развертывания Azure см. [здесь][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span><span class="sxs-lookup"><span data-stu-id="e260a-178">Learn more about Azure [deployment models][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span></span>   
>
>

## <span data-ttu-id="e260a-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Отказоустойчивый кластер Windows Server (WSFC)</span><span class="sxs-lookup"><span data-stu-id="e260a-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span></span>
<span data-ttu-id="e260a-180">Отказоустойчивая кластеризация Windows Server — foundation hello установки SAP ASCS/SCS высокого уровня доступности и СУБД в Windows.</span><span class="sxs-lookup"><span data-stu-id="e260a-180">Windows Server Failover Clustering is hello foundation of a high-availability SAP ASCS/SCS installation and DBMS in Windows.</span></span>

<span data-ttu-id="e260a-181">Отказоустойчивый кластер — группу 1 + n независимых серверов (узлов), работающих совместно tooincrease hello доступности приложений и служб.</span><span class="sxs-lookup"><span data-stu-id="e260a-181">A failover cluster is a group of 1+n independent servers (nodes) that work together tooincrease hello availability of applications and services.</span></span> <span data-ttu-id="e260a-182">В случае сбоя узла отказоустойчивой кластеризации Windows Server вычисляет hello количество сбоев, которые могут возникнуть при сохранении исправное состояние кластера tooprovide приложений и служб.</span><span class="sxs-lookup"><span data-stu-id="e260a-182">If a node failure occurs, Windows Server Failover Clustering calculates hello number of failures that can occur while maintaining a healthy cluster tooprovide applications and services.</span></span> <span data-ttu-id="e260a-183">Можно выбрать другой кворума режимы tooachieve отказоустойчивого кластера.</span><span class="sxs-lookup"><span data-stu-id="e260a-183">You can choose from different quorum modes tooachieve failover clustering.</span></span>

### <span data-ttu-id="e260a-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Режимы кворума</span><span class="sxs-lookup"><span data-stu-id="e260a-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Quorum modes</span></span>
<span data-ttu-id="e260a-185">При использовании WSFC доступно четыре режима кворума.</span><span class="sxs-lookup"><span data-stu-id="e260a-185">You can choose from four quorum modes when you use Windows Server Failover Clustering:</span></span>

* <span data-ttu-id="e260a-186">**Большинство узлов**.</span><span class="sxs-lookup"><span data-stu-id="e260a-186">**Node Majority**.</span></span> <span data-ttu-id="e260a-187">Каждый узел кластера hello может голосовать.</span><span class="sxs-lookup"><span data-stu-id="e260a-187">Each node of hello cluster can vote.</span></span> <span data-ttu-id="e260a-188">функции Hello кластера только с большинством голосов, то есть с более половины hello голоса.</span><span class="sxs-lookup"><span data-stu-id="e260a-188">hello cluster functions only with a majority of votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="e260a-189">Этот вариант рекомендуется при наличии нечетного числа узлов.</span><span class="sxs-lookup"><span data-stu-id="e260a-189">We recommend this option for clusters that have an uneven number of nodes.</span></span> <span data-ttu-id="e260a-190">Например три узла в кластер из семи узлов может завершиться ошибкой, и прежнему hello кластера позволяет достичь большей и по-прежнему toorun.</span><span class="sxs-lookup"><span data-stu-id="e260a-190">For example, three nodes in a seven-node cluster can fail, and hello cluster stills achieves a majority and continues toorun.</span></span>  
* <span data-ttu-id="e260a-191">**Большинство узлов и диска**.</span><span class="sxs-lookup"><span data-stu-id="e260a-191">**Node and Disk Majority**.</span></span> <span data-ttu-id="e260a-192">Каждый узел и указанный диск (диск-свидетель) в хранилище кластера hello смогут проголосовать они становятся доступны и в связи.</span><span class="sxs-lookup"><span data-stu-id="e260a-192">Each node and a designated disk (a disk witness) in hello cluster storage can vote when they are available and in communication.</span></span> <span data-ttu-id="e260a-193">более половины голоса hello голосов функции Hello кластера только с большинством hello т. е.</span><span class="sxs-lookup"><span data-stu-id="e260a-193">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="e260a-194">Этот режим целесообразно использовать в среде кластера с четным числом узлов.</span><span class="sxs-lookup"><span data-stu-id="e260a-194">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="e260a-195">Если hello половины узлов и hello диска подключены к сети, кластер hello находится в работоспособном состоянии.</span><span class="sxs-lookup"><span data-stu-id="e260a-195">If half hello nodes and hello disk are online, hello cluster remains in a healthy state.</span></span>
* <span data-ttu-id="e260a-196">**Большинство узлов и файлового ресурса**.</span><span class="sxs-lookup"><span data-stu-id="e260a-196">**Node and File Share Majority**.</span></span> <span data-ttu-id="e260a-197">Каждый узел плюс, назначенный общую папку (файловый ресурс-свидетель), Здравствуйте, администратор создает может голосовать, независимо от того, hello узлов и общую папку доступны ли и доступны для связи.</span><span class="sxs-lookup"><span data-stu-id="e260a-197">Each node plus a designated file share (a file share witness) that hello administrator creates can vote, regardless of whether hello nodes and file share are available and in communication.</span></span> <span data-ttu-id="e260a-198">более половины голоса hello голосов функции Hello кластера только с большинством hello т. е.</span><span class="sxs-lookup"><span data-stu-id="e260a-198">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="e260a-199">Этот режим целесообразно использовать в среде кластера с четным числом узлов.</span><span class="sxs-lookup"><span data-stu-id="e260a-199">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="e260a-200">Аналогичные toohello узла и режим большинства диска, но следящая общая папка используется вместо диска-свидетеля.</span><span class="sxs-lookup"><span data-stu-id="e260a-200">It's similar toohello Node and Disk Majority mode, but it uses a witness file share instead of a witness disk.</span></span> <span data-ttu-id="e260a-201">Данный режим может легко tooimplement, но если hello общая папка сам не обеспечивает высокую доступность, ее можно будет единая точка отказа.</span><span class="sxs-lookup"><span data-stu-id="e260a-201">This mode is easy tooimplement, but if hello file share itself is not highly available, it might become a single point of failure.</span></span>
* <span data-ttu-id="e260a-202">**Отсутствие большинства — только диск**.</span><span class="sxs-lookup"><span data-stu-id="e260a-202">**No Majority: Disk Only**.</span></span> <span data-ttu-id="e260a-203">Hello кластер имеет кворум, если один узел доступен и в связи с определенным диском в хранилище кластера hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-203">hello cluster has a quorum if one node is available and in communication with a specific disk in hello cluster storage.</span></span> <span data-ttu-id="e260a-204">Только узлы hello, которые также находятся в связи с этого диска можно соединить hello кластера.</span><span class="sxs-lookup"><span data-stu-id="e260a-204">Only hello nodes that also are in communication with that disk can join hello cluster.</span></span> <span data-ttu-id="e260a-205">Использовать этот режим не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="e260a-205">We recommend that you do not use this mode.</span></span>
 

## <span data-ttu-id="e260a-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Отказоустойчивый кластер Windows Server в локальной среде</span><span class="sxs-lookup"><span data-stu-id="e260a-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering on-premises</span></span>
<span data-ttu-id="e260a-207">На рис. 1 показан кластер, состоящий из двух узлов.</span><span class="sxs-lookup"><span data-stu-id="e260a-207">Figure 1 shows a cluster of two nodes.</span></span> <span data-ttu-id="e260a-208">Если hello сетевого подключения между узлами hello и работать обоих узлов и запущена, диск или файловый ресурс кворума определяет продолжится, какой из узлов кластера hello tooprovide приложений и служб.</span><span class="sxs-lookup"><span data-stu-id="e260a-208">If hello network connection between hello nodes fails and both nodes stay up and running, a quorum disk or file share determines which node will continue tooprovide hello cluster's applications and services.</span></span> <span data-ttu-id="e260a-209">Hello узел, имеющий доступ toohello кворума диск или общая папка будет hello гарантирует, что службы продолжать.</span><span class="sxs-lookup"><span data-stu-id="e260a-209">hello node that has access toohello quorum disk or file share is hello node that ensures that services continue.</span></span>

<span data-ttu-id="e260a-210">Поскольку в этом примере используется двухузлового кластера, мы используем hello узла и режим кворума большинства общей папки для файла.</span><span class="sxs-lookup"><span data-stu-id="e260a-210">Because this example uses a two-node cluster, we use hello Node and File Share Majority quorum mode.</span></span> <span data-ttu-id="e260a-211">Hello узла и большинству дисков также является допустимым параметром.</span><span class="sxs-lookup"><span data-stu-id="e260a-211">hello Node and Disk Majority also is a valid option.</span></span> <span data-ttu-id="e260a-212">В рабочей среде рекомендуется использовать диск кворума.</span><span class="sxs-lookup"><span data-stu-id="e260a-212">In a production environment, we recommend that you use a quorum disk.</span></span> <span data-ttu-id="e260a-213">Можно использовать сети и хранилища toomake технологии системы его высокой доступности.</span><span class="sxs-lookup"><span data-stu-id="e260a-213">You can use network and storage system technology toomake it highly available.</span></span>

![Рис. 1. Пример конфигурации отказоустойчивого кластера Windows Server для SAP ASCS/SCS в Azure][sap-ha-guide-figure-1000]

<span data-ttu-id="e260a-215">_**Рис. 1.** Пример конфигурации отказоустойчивого кластера Windows Server для SAP ASCS/SCS в Azure_</span><span class="sxs-lookup"><span data-stu-id="e260a-215">_**Figure 1:** Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure_</span></span>

### <span data-ttu-id="e260a-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Общее хранилище</span><span class="sxs-lookup"><span data-stu-id="e260a-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Shared storage</span></span>
<span data-ttu-id="e260a-217">На рис. 1 также показано общее хранилище кластера с двумя узлами.</span><span class="sxs-lookup"><span data-stu-id="e260a-217">Figure 1 also shows a two-node shared storage cluster.</span></span> <span data-ttu-id="e260a-218">В общее хранилище локального кластера все узлы в кластере hello обнаруживает общего хранилища.</span><span class="sxs-lookup"><span data-stu-id="e260a-218">In an on-premises shared storage cluster, all nodes in hello cluster detect shared storage.</span></span> <span data-ttu-id="e260a-219">Механизм блокировки для защиты hello данных от повреждения.</span><span class="sxs-lookup"><span data-stu-id="e260a-219">A locking mechanism protects hello data from corruption.</span></span> <span data-ttu-id="e260a-220">Каждый узел может обнаружить отказ другого узла.</span><span class="sxs-lookup"><span data-stu-id="e260a-220">All nodes can detect if another node fails.</span></span> <span data-ttu-id="e260a-221">При сбое одного узла, оставшийся узел hello принимает право на владение ресурсов хранилища hello и гарантирует hello доступность служб.</span><span class="sxs-lookup"><span data-stu-id="e260a-221">If one node fails, hello remaining node takes ownership of hello storage resources and ensures hello availability of services.</span></span>

> [!NOTE]
> <span data-ttu-id="e260a-222">В некоторых СУБД, например SQL Server, общие диски не требуются для достижения высокого уровня доступности.</span><span class="sxs-lookup"><span data-stu-id="e260a-222">You don't need shared disks for high availability with some DBMS applications, like with SQL Server.</span></span> <span data-ttu-id="e260a-223">SQL Server Always On реплицирует файлы данных и журналов СУБД с локального диска Привет одному кластеру узел toohello локального диска другой узел кластера.</span><span class="sxs-lookup"><span data-stu-id="e260a-223">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="e260a-224">В этом случае настройки кластера Windows hello не требуется общий диск.</span><span class="sxs-lookup"><span data-stu-id="e260a-224">In that case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="e260a-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Сетевые подключения и разрешение имен</span><span class="sxs-lookup"><span data-stu-id="e260a-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Networking and name resolution</span></span>
<span data-ttu-id="e260a-226">Клиентские компьютеры достичь hello кластера через виртуальный IP-адрес и имя виртуального узла, DNS-сервер предоставляет приветствия.</span><span class="sxs-lookup"><span data-stu-id="e260a-226">Client computers reach hello cluster over a virtual IP address and a virtual host name that hello DNS server provides.</span></span> <span data-ttu-id="e260a-227">Hello локальных узлов и hello DNS-сервер может обрабатывать несколько IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="e260a-227">hello on-premises nodes and hello DNS server can handle multiple IP addresses.</span></span>

<span data-ttu-id="e260a-228">В стандартной конфигурации используется от двух сетевых подключений:</span><span class="sxs-lookup"><span data-stu-id="e260a-228">In a typical setup, you use two or more network connections:</span></span>

* <span data-ttu-id="e260a-229">Выделенное соединение toohello хранилища</span><span class="sxs-lookup"><span data-stu-id="e260a-229">A dedicated connection toohello storage</span></span>
* <span data-ttu-id="e260a-230">Внутренняя кластера сетевое подключение для подтверждения hello</span><span class="sxs-lookup"><span data-stu-id="e260a-230">A cluster-internal network connection for hello heartbeat</span></span>
* <span data-ttu-id="e260a-231">Общедоступной сети, которую клиенты используют tooconnect toohello кластера</span><span class="sxs-lookup"><span data-stu-id="e260a-231">A public network that clients use tooconnect toohello cluster</span></span>

## <span data-ttu-id="e260a-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Отказоустойчивый кластер Windows Server в Azure</span><span class="sxs-lookup"><span data-stu-id="e260a-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="e260a-233">Сравнение развертывания toobare исходного или частного облака, виртуальные машины Azure требуются дополнительные действия tooconfigure отказоустойчивой кластеризации Windows Server.</span><span class="sxs-lookup"><span data-stu-id="e260a-233">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="e260a-234">При создании общего диска кластера, необходимо несколько IP-адресов и виртуальный узел имена tooset для экземпляра SAP ASCS/SCS hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-234">When you build a shared cluster disk, you need tooset several IP addresses and virtual host names for hello SAP ASCS/SCS instance.</span></span>

<span data-ttu-id="e260a-235">В этой статье рассматриваются основные понятия и hello toobuild необходимые дополнительные действия кластер служб центра высокой доступности SAP в Azure.</span><span class="sxs-lookup"><span data-stu-id="e260a-235">In this article, we discuss key concepts and hello additional steps required toobuild an SAP high-availability central services cluster in Azure.</span></span> <span data-ttu-id="e260a-236">Мы покажем, как Подсистема балансировки нагрузки tooset копирование hello стороннего средства SIOS DataKeeper и как tooconfigure hello Azure внутренней.</span><span class="sxs-lookup"><span data-stu-id="e260a-236">We show you how tooset up hello third-party tool SIOS DataKeeper, and how tooconfigure hello Azure internal load balancer.</span></span> <span data-ttu-id="e260a-237">Эти средства toocreate отказоустойчивый кластер Windows можно использовать с файловый ресурс-свидетель в Azure.</span><span class="sxs-lookup"><span data-stu-id="e260a-237">You can use these tools toocreate a Windows failover cluster with a file share witness in Azure.</span></span>

![Рис. 2. Конфигурация отказоустойчивого кластера Windows Server в Azure без общего диска][sap-ha-guide-figure-1001]

<span data-ttu-id="e260a-239">_**Рис. 2.** Конфигурация отказоустойчивого кластера Windows Server в Azure без общего диска_</span><span class="sxs-lookup"><span data-stu-id="e260a-239">_**Figure 2:** Windows Server Failover Clustering configuration in Azure without a shared disk_</span></span>

### <span data-ttu-id="e260a-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Создание общего диска в Azure с помощью SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="e260a-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Shared disk in Azure with SIOS DataKeeper</span></span>
<span data-ttu-id="e260a-241">Общее хранилище кластера необходимо для экземпляра SAP ASCS/SCS с высоким уровнем доступности.</span><span class="sxs-lookup"><span data-stu-id="e260a-241">You need cluster shared storage for a high-availability SAP ASCS/SCS instance.</span></span> <span data-ttu-id="e260a-242">Как в сентябре 2016 года Azure не предоставляет общее хранилище, можно использовать toocreate кластера общего хранилища.</span><span class="sxs-lookup"><span data-stu-id="e260a-242">As of September 2016, Azure doesn't offer shared storage that you can use toocreate a shared storage cluster.</span></span> <span data-ttu-id="e260a-243">Можно использовать стороннее программное обеспечение SIOS DataKeeper Cluster Edition toocreate зеркальных хранилища, которое имитирует общее хранилище кластера.</span><span class="sxs-lookup"><span data-stu-id="e260a-243">You can use third-party software SIOS DataKeeper Cluster Edition toocreate a mirrored storage that simulates cluster shared storage.</span></span> <span data-ttu-id="e260a-244">Hello SIOS решение предоставляет данные в реальном времени синхронной репликации.</span><span class="sxs-lookup"><span data-stu-id="e260a-244">hello SIOS solution provides real-time synchronous data replication.</span></span> <span data-ttu-id="e260a-245">Вот как можно создать общий дисковый ресурс для кластера.</span><span class="sxs-lookup"><span data-stu-id="e260a-245">This is how you can create a shared disk resource for a cluster:</span></span>

1. <span data-ttu-id="e260a-246">Подключите дополнительный диск tooeach hello виртуальных машин (ВМ) в кластере Windows.</span><span class="sxs-lookup"><span data-stu-id="e260a-246">Attach an additional disk tooeach of hello virtual machines (VMs) in a Windows cluster configuration.</span></span>
2. <span data-ttu-id="e260a-247">Запустите SIOS DataKeeper Cluster Edition на обоих узлах виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e260a-247">Run SIOS DataKeeper Cluster Edition on both virtual machine nodes.</span></span>
3. <span data-ttu-id="e260a-248">Настройте SIOS DataKeeper Cluster Edition, таким образом, чтобы он отражает содержимое hello hello дополнительный диск, подключенный том из hello виртуальной машины toohello дополнительных присоединенного тома hello целевой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e260a-248">Configure SIOS DataKeeper Cluster Edition so that it mirrors hello content of hello additional disk attached volume from hello source virtual machine toohello additional disk attached volume of hello target virtual machine.</span></span> <span data-ttu-id="e260a-249">SIOS DataKeeper абстрагирует hello исходных и целевых локальных томов и представляет их tooWindows Server отказоустойчивый кластер в один общий диск.</span><span class="sxs-lookup"><span data-stu-id="e260a-249">SIOS DataKeeper abstracts hello source and target local volumes, and then presents them tooWindows Server Failover Clustering as one shared disk.</span></span>

<span data-ttu-id="e260a-250">Дополнительные сведения о SIOS DataKeeper см. [здесь](http://us.sios.com/products/datakeeper-cluster/).</span><span class="sxs-lookup"><span data-stu-id="e260a-250">Get more information about [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span></span>

![Рис. 3. Конфигурация отказоустойчивой кластеризации Windows Server в Azure с использованием SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="e260a-252">_**Рис. 3.** Конфигурация отказоустойчивого кластера Windows Server в Azure с использованием SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="e260a-252">_**Figure 3:** Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper_</span></span>

> [!NOTE]
> <span data-ttu-id="e260a-253">В некоторых СУБД, например SQL Server, общие диски не требуются для достижения высокого уровня доступности.</span><span class="sxs-lookup"><span data-stu-id="e260a-253">You don't need shared disks for high availability with some DBMS products, like SQL Server.</span></span> <span data-ttu-id="e260a-254">SQL Server Always On реплицирует файлы данных и журналов СУБД с локального диска Привет одному кластеру узел toohello локального диска другой узел кластера.</span><span class="sxs-lookup"><span data-stu-id="e260a-254">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="e260a-255">В этом случае настройки кластера Windows hello не требуется общий диск.</span><span class="sxs-lookup"><span data-stu-id="e260a-255">In this case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="e260a-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Разрешение имен в Azure</span><span class="sxs-lookup"><span data-stu-id="e260a-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Name resolution in Azure</span></span>
<span data-ttu-id="e260a-257">Hello Azure облачной платформы не предлагает hello параметр tooconfigure виртуальных IP-адресов, например с плавающей запятой IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="e260a-257">hello Azure cloud platform doesn't offer hello option tooconfigure virtual IP addresses, such as floating IP addresses.</span></span> <span data-ttu-id="e260a-258">Требуется альтернативное решение tooset копии виртуальных IP адресов tooreach hello ресурса кластера в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-258">You need an alternative solution tooset up a virtual IP address tooreach hello cluster resource in hello cloud.</span></span>
<span data-ttu-id="e260a-259">Azure имеет внутренний балансировщик нагрузки в hello службы балансировки нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="e260a-259">Azure has an internal load balancer in hello Azure Load Balancer service.</span></span> <span data-ttu-id="e260a-260">С hello внутренней подсистемы балансировки нагрузки клиентам подключиться hello кластера через hello кластера виртуального IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="e260a-260">With hello internal load balancer, clients reach hello cluster over hello cluster virtual IP address.</span></span>
<span data-ttu-id="e260a-261">Необходимо toodeploy hello внутренней подсистемы балансировки нагрузки в группе ресурсов hello, содержащий hello узлов кластера.</span><span class="sxs-lookup"><span data-stu-id="e260a-261">You need toodeploy hello internal load balancer in hello resource group that contains hello cluster nodes.</span></span> <span data-ttu-id="e260a-262">Настройте все необходимые правила перенаправления с пробы hello порты hello внутренней подсистемы балансировки нагрузки портов.</span><span class="sxs-lookup"><span data-stu-id="e260a-262">Then, configure all necessary port forwarding rules with hello probe ports of hello internal load balancer.</span></span>
<span data-ttu-id="e260a-263">Hello клиенты могут подключаться через hello виртуальное имя узла.</span><span class="sxs-lookup"><span data-stu-id="e260a-263">hello clients can connect via hello virtual host name.</span></span> <span data-ttu-id="e260a-264">Hello DNS-сервер разрешает в IP-адрес кластера hello и перенаправления toohello активный узел кластера hello дескрипторы портов hello внутренней нагрузки балансировки.</span><span class="sxs-lookup"><span data-stu-id="e260a-264">hello DNS server resolves hello cluster IP address, and hello internal load balancer handles port forwarding toohello active node of hello cluster.</span></span>

## <span data-ttu-id="e260a-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> Высокий уровень доступности SAP NetWeaver в Azure IaaS</span><span class="sxs-lookup"><span data-stu-id="e260a-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> SAP NetWeaver high availability in Azure Infrastructure-as-a-Service (IaaS)</span></span>
<span data-ttu-id="e260a-266">tooachieve SAP высокий уровень доступности приложения, например для компонентов программного обеспечения SAP, должны tooprotect hello следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="e260a-266">tooachieve SAP application high availability, such as for SAP software components, you need tooprotect hello following components:</span></span>

* <span data-ttu-id="e260a-267">экземпляр сервера приложений SAP;</span><span class="sxs-lookup"><span data-stu-id="e260a-267">SAP Application Server instance</span></span>
* <span data-ttu-id="e260a-268">экземпляров ASCS/SCS SAP,</span><span class="sxs-lookup"><span data-stu-id="e260a-268">SAP ASCS/SCS instance</span></span>
* <span data-ttu-id="e260a-269">сервер СУБД.</span><span class="sxs-lookup"><span data-stu-id="e260a-269">DBMS server</span></span>

<span data-ttu-id="e260a-270">Дополнительные сведения о защите компонентов SAP в сценариях обеспечения высокого уровня доступности см. в статье [SAP NetWeaver на виртуальных машинах Windows. Руководство по планированию и внедрению][planning-guide-11].</span><span class="sxs-lookup"><span data-stu-id="e260a-270">For more information about protecting SAP components in high-availability scenarios, see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide-11].</span></span>

### <span data-ttu-id="e260a-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> Высокая доступность серверов приложений SAP</span><span class="sxs-lookup"><span data-stu-id="e260a-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> High-availability SAP Application Server</span></span>
<span data-ttu-id="e260a-272">Обычно не требуется конкретного решения высокого уровня доступности для экземпляров сервера приложений SAP и диалоговое окно приветствия.</span><span class="sxs-lookup"><span data-stu-id="e260a-272">You usually don't need a specific high-availability solution for hello SAP Application Server and dialog instances.</span></span> <span data-ttu-id="e260a-273">Высокий уровень доступности достигается за счет избыточности, то есть на разных экземплярах виртуальных машин Azure настраивается несколько диалоговых экземпляров.</span><span class="sxs-lookup"><span data-stu-id="e260a-273">You achieve high availability by redundancy, and you'll configure multiple dialog instances in different instances of Azure Virtual Machines.</span></span> <span data-ttu-id="e260a-274">Необходимо установить как минимум два экземпляра приложения SAP на два экземпляра виртуальных машин Azure.</span><span class="sxs-lookup"><span data-stu-id="e260a-274">You should have at least two SAP application instances installed in two instances of Azure Virtual Machines.</span></span>

![Рис. 4. Высокая доступность сервера приложений SAP][sap-ha-guide-figure-2000]

<span data-ttu-id="e260a-276">_**Рис. 4.** Высокая доступность сервера приложений SAP_</span><span class="sxs-lookup"><span data-stu-id="e260a-276">_**Figure 4:** High-availability SAP Application Server_</span></span>

<span data-ttu-id="e260a-277">Необходимо разместить все виртуальные машины, hello, экземплярах сервера приложений SAP в одной группе доступности Azure.</span><span class="sxs-lookup"><span data-stu-id="e260a-277">You must place all virtual machines that host SAP Application Server instances in hello same Azure availability set.</span></span> <span data-ttu-id="e260a-278">Группа доступности Azure гарантирует следующее.</span><span class="sxs-lookup"><span data-stu-id="e260a-278">An Azure availability set ensures that:</span></span>

* <span data-ttu-id="e260a-279">Все виртуальные машины являются частью hello домену обновления.</span><span class="sxs-lookup"><span data-stu-id="e260a-279">All virtual machines are part of hello same upgrade domain.</span></span> <span data-ttu-id="e260a-280">Домен обновления, например, гарантирует, что, hello виртуальных машин не обновляются через hello одновременно во время планового обслуживания.</span><span class="sxs-lookup"><span data-stu-id="e260a-280">An upgrade domain, for example, makes sure that hello virtual machines aren't updated at hello same time during planned maintenance downtime.</span></span>
* <span data-ttu-id="e260a-281">Все виртуальные машины являются частью hello одного домена.</span><span class="sxs-lookup"><span data-stu-id="e260a-281">All virtual machines are part of hello same fault domain.</span></span> <span data-ttu-id="e260a-282">Домен сбоя, например, гарантирует, что развернуты виртуальные машины, чтобы единственной точки отказа влияет на доступность hello всех виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e260a-282">A fault domain, for example, makes sure that virtual machines are deployed so that no single point of failure affects hello availability of all virtual machines.</span></span>

<span data-ttu-id="e260a-283">Дополнительные сведения о том, как слишком[Управление доступностью виртуальных машин hello][virtual-machines-manage-availability].</span><span class="sxs-lookup"><span data-stu-id="e260a-283">Learn more about how too[manage hello availability of virtual machines][virtual-machines-manage-availability].</span></span>

<span data-ttu-id="e260a-284">Только диск неуправляемые: поскольку hello учетной записи хранилища Azure потенциальных узких мест, является важным toohave по крайней мере две учетные записи хранилища Azure, в которых распределяются по крайней мере два виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e260a-284">Unmanaged disk only: Because hello Azure storage account is a potential single point of failure, it's important toohave at least two Azure storage accounts, in which at least two virtual machines are distributed.</span></span> <span data-ttu-id="e260a-285">В идеале hello дисков каждой виртуальной машины, на котором выполняется экземпляр диалога SAP будет разворачиваться в другую учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="e260a-285">In an ideal setup, hello disks of each virtual machine that is running an SAP dialog instance would be deployed in a different storage account.</span></span>

### <span data-ttu-id="e260a-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> Высокая доступность экземпляра SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e260a-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> High-availability SAP ASCS/SCS instance</span></span>
<span data-ttu-id="e260a-287">На рис. 5 приведен пример высокой доступности экземпляра SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e260a-287">Figure 5 is an example of a high-availability SAP ASCS/SCS instance.</span></span>

![Рис. 5. Высокая доступность экземпляра SAP ASCS/SCS][sap-ha-guide-figure-2001]

<span data-ttu-id="e260a-289">_**Рис. 5.** Высокая доступность экземпляра SAP ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="e260a-289">_**Figure 5:** High-availability SAP ASCS/SCS instance_</span></span>

#### <span data-ttu-id="e260a-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> Обеспечение высокого уровня доступности экземпляра SAP ASCS/SCS с помощью отказоустойчивой кластеризации Windows Server в Azure</span><span class="sxs-lookup"><span data-stu-id="e260a-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> SAP ASCS/SCS instance high availability with Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="e260a-291">Сравнение развертывания toobare исходного или частного облака, виртуальные машины Azure требуются дополнительные действия tooconfigure отказоустойчивой кластеризации Windows Server.</span><span class="sxs-lookup"><span data-stu-id="e260a-291">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="e260a-292">toobuild отказоустойчивого кластера Windows, требуется общий диск кластера, несколько IP-адресов, несколько имен виртуального узла и Azure внутренний балансировщик нагрузки для кластеризация экземпляра SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="e260a-292">toobuild a Windows failover cluster, you need a shared cluster disk, several IP addresses, several virtual host names, and an Azure internal load balancer for clustering an SAP ASCS/SCS instance.</span></span> <span data-ttu-id="e260a-293">Мы рассмотрим это более подробно далее в статье hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-293">We discuss this in more detail later in hello article.</span></span>

![Рис. 6. Конфигурация отказоустойчивого кластера Windows Server для SAP ASCS/SCS в Azure с использованием SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="e260a-295">_**Рис. 6.** Конфигурация отказоустойчивого кластера Windows Server для SAP ASCS/SCS в Azure с использованием SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="e260a-295">_**Figure 6:** Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure with SIOS DataKeeper_</span></span>

### <span data-ttu-id="e260a-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a> Высокий уровень доступности экземпляра СУБД</span><span class="sxs-lookup"><span data-stu-id="e260a-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>High-availability DBMS instance</span></span>
<span data-ttu-id="e260a-297">Hello СУБД также является единая точка контакта в системе SAP.</span><span class="sxs-lookup"><span data-stu-id="e260a-297">hello DBMS also is a single point of contact in an SAP system.</span></span> <span data-ttu-id="e260a-298">Требуется tooprotect его с помощью решений высокой доступности.</span><span class="sxs-lookup"><span data-stu-id="e260a-298">You need tooprotect it by using a high-availability solution.</span></span> <span data-ttu-id="e260a-299">На рисунке 7 показано решение высокой доступности AlwaysOn в SQL Server в Azure, отказоустойчивой кластеризации Windows Server и hello Azure внутренней подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e260a-299">Figure 7 shows a SQL Server Always On high-availability solution in Azure, with Windows Server Failover Clustering and hello Azure internal load balancer.</span></span> <span data-ttu-id="e260a-300">SQL Server AlwaysOn реплицирует файлы данных и журналов СУБД с помощью собственной функции репликации СУБД.</span><span class="sxs-lookup"><span data-stu-id="e260a-300">SQL Server Always On replicates DBMS data and log files by using its own DBMS replication.</span></span> <span data-ttu-id="e260a-301">В этом случае вы не требуются общие диски кластера, который упрощает настройку всей hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-301">In this case, you don't need cluster shared disks, which simplifies hello entire setup.</span></span>

![Рис. 7. Пример высокодоступного сервера СУБД SAP с SQL Server Always On][sap-ha-guide-figure-2003]

<span data-ttu-id="e260a-303">_**Рис. 7.** Пример высокодоступного сервера СУБД SAP с SQL Server Always On_</span><span class="sxs-lookup"><span data-stu-id="e260a-303">_**Figure 7:** Example of a high-availability SAP DBMS, with SQL Server Always On_</span></span>

<span data-ttu-id="e260a-304">Дополнительные сведения о кластеризации SQL Server в Azure с помощью модели развертывания диспетчера ресурсов Azure hello статьях:</span><span class="sxs-lookup"><span data-stu-id="e260a-304">For more information about clustering SQL Server in Azure by using hello Azure Resource Manager deployment model, see these articles:</span></span>

* <span data-ttu-id="e260a-305">[Настройка группы доступности AlwaysOn на виртуальных машинах Azure с использованием Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span><span class="sxs-lookup"><span data-stu-id="e260a-305">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span></span>
* <span data-ttu-id="e260a-306">[Настройка внутреннего балансировщика нагрузки для группы доступности AlwaysOn в Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span><span class="sxs-lookup"><span data-stu-id="e260a-306">[Configure an Azure internal load balancer for an Always On availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span></span>

## <span data-ttu-id="e260a-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> Сценарии комплексного развертывания с высоким уровнем доступности</span><span class="sxs-lookup"><span data-stu-id="e260a-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> End-to-end high-availability deployment scenarios</span></span>

### <a name="deployment-scenario-using-architectural-template-1"></a><span data-ttu-id="e260a-308">Сценарий развертывания с помощью шаблона 1 архитектуры</span><span class="sxs-lookup"><span data-stu-id="e260a-308">Deployment scenario using Architectural Template 1</span></span>

<span data-ttu-id="e260a-309">На рис. 8 показан пример архитектуры SAP NetWeaver с высоким уровнем доступности в Azure для **одной** системы SAP.</span><span class="sxs-lookup"><span data-stu-id="e260a-309">Figure 8 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="e260a-310">В этом сценарии используется следующая конфигурация:</span><span class="sxs-lookup"><span data-stu-id="e260a-310">This scenario is set up as follows:</span></span>

- <span data-ttu-id="e260a-311">Один выделенный кластер используется для экземпляра SAP ASCS/SCS hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-311">One dedicated cluster is used for hello SAP ASCS/SCS instance.</span></span>
- <span data-ttu-id="e260a-312">Один выделенный кластер используется для экземпляра СУБД hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-312">One dedicated cluster is used for hello DBMS instance.</span></span>
- <span data-ttu-id="e260a-313">экземпляры сервера приложений SAP развернуты на собственных выделенных виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="e260a-313">SAP Application Server instances are deployed in their own dedicated VMs.</span></span>

![Рис. 8. Шаблон 1 архитектуры SAP с высоким уровнем доступности с выделенным кластером для ASCS/SCS и СУБД][sap-ha-guide-figure-2004]

<span data-ttu-id="e260a-315">_**Рис. 8.** Шаблон 1 архитектуры SAP с высоким уровнем доступности с выделенным кластером для ASCS/SCS и СУБД_</span><span class="sxs-lookup"><span data-stu-id="e260a-315">_**Figure 8:** SAP high-availability Architectural Template 1, dedicated clusters for ASCS/SCS and DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-2"></a><span data-ttu-id="e260a-316">Сценарий развертывания с помощью шаблона 2 архитектуры</span><span class="sxs-lookup"><span data-stu-id="e260a-316">Deployment scenario using Architectural Template 2</span></span>

<span data-ttu-id="e260a-317">На рис. 9 показан пример архитектуры SAP NetWeaver с высоким уровнем доступности в Azure для **одной** системы SAP.</span><span class="sxs-lookup"><span data-stu-id="e260a-317">Figure 9 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="e260a-318">В этом сценарии используется следующая конфигурация:</span><span class="sxs-lookup"><span data-stu-id="e260a-318">This scenario is set up as follows:</span></span>

- <span data-ttu-id="e260a-319">Один выделенный кластер используется для **оба** hello SAP ASCS/SCS экземпляра и hello СУБД.</span><span class="sxs-lookup"><span data-stu-id="e260a-319">One dedicated cluster is used for **both** hello SAP ASCS/SCS instance and hello DBMS.</span></span>
- <span data-ttu-id="e260a-320">экземпляры сервера приложений SAP развернуты на собственных выделенных виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="e260a-320">SAP Application Server instances are deployed in own dedicated VMs.</span></span>

![Рис. 9. Шаблон 2 архитектуры SAP с высоким уровнем доступности с выделенным кластером для ASCS/SCS и СУБД][sap-ha-guide-figure-2005]

<span data-ttu-id="e260a-322">_**Рис. 9.** Шаблон 2 архитектуры SAP с высоким уровнем доступности с выделенным кластером для ASCS/SCS и СУБД_</span><span class="sxs-lookup"><span data-stu-id="e260a-322">_**Figure 9:** SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-3"></a><span data-ttu-id="e260a-323">Сценарий развертывания с помощью шаблона 3 архитектуры</span><span class="sxs-lookup"><span data-stu-id="e260a-323">Deployment scenario using Architectural Template 3</span></span>

<span data-ttu-id="e260a-324">На рис. 10 показан пример архитектуры SAP NetWeaver с высоким уровнем доступности в Azure для **двух** систем SAP с &lt;SID1&gt; и &lt;SID2&gt;.</span><span class="sxs-lookup"><span data-stu-id="e260a-324">Figure 10 shows an example of an SAP NetWeaver high-availability architecture in Azure for **two** SAP systems, with &lt;SID1&gt; and &lt;SID2&gt;.</span></span> <span data-ttu-id="e260a-325">В этом сценарии используется следующая конфигурация:</span><span class="sxs-lookup"><span data-stu-id="e260a-325">This scenario is set up as follows:</span></span>

- <span data-ttu-id="e260a-326">Один выделенный кластер используется для **оба** экземпляр hello SAP ASCS/SCS SID1 *и* экземпляра SAP ASCS/SCS SID2 hello (один кластер).</span><span class="sxs-lookup"><span data-stu-id="e260a-326">One dedicated cluster is used for **both** hello SAP ASCS/SCS SID1 instance *and* hello SAP ASCS/SCS SID2 instance (one cluster).</span></span>
- <span data-ttu-id="e260a-327">один выделенный кластер для SID1 СУБД и другой выделенный кластер для SID2 СУБД (два кластера);</span><span class="sxs-lookup"><span data-stu-id="e260a-327">One dedicated cluster is used for DBMS SID1, and another dedicated cluster is used for DBMS SID2 (two clusters).</span></span>
- <span data-ttu-id="e260a-328">Экземпляры сервера приложений SAP для hello системы SAP SID1 имеют свои собственные выделенных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e260a-328">SAP Application Server instances for hello SAP system SID1 have their own dedicated VMs.</span></span>
- <span data-ttu-id="e260a-329">Экземпляры сервера приложений SAP для hello системы SAP SID2 имеют свои собственные выделенных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e260a-329">SAP Application Server instances for hello SAP system SID2 have their own dedicated VMs.</span></span>

![Рис. 10. Шаблон 3 архитектуры SAP с высоким уровнем доступности с выделенным кластером для разных экземпляров ASCS/SCS][sap-ha-guide-figure-6003]

<span data-ttu-id="e260a-331">_**Рис. 10.** Шаблон 3 архитектуры SAP с высоким уровнем доступности с выделенным кластером для разных экземпляров ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="e260a-331">_**Figure 10:** SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances_</span></span>

## <span data-ttu-id="e260a-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Подготовка инфраструктуры hello</span><span class="sxs-lookup"><span data-stu-id="e260a-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> Prepare hello infrastructure</span></span>

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a><span data-ttu-id="e260a-333">Подготовка инфраструктуры hello для архитектуры шаблона 1</span><span class="sxs-lookup"><span data-stu-id="e260a-333">Prepare hello infrastructure for Architectural Template 1</span></span>
<span data-ttu-id="e260a-334">Шаблоны Azure Resource Manager для SAP помогают упростить развертывание необходимых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e260a-334">Azure Resource Manager templates for SAP help simplify deployment of required resources.</span></span>

<span data-ttu-id="e260a-335">шаблоны трехуровневой Hello диспетчера ресурсов Azure также поддерживают сценарии высокой доступности, такие как в архитектуре 1 шаблона, которое имеет два кластера.</span><span class="sxs-lookup"><span data-stu-id="e260a-335">hello three-tier templates in Azure Resource Manager also support high-availability scenarios, such as in Architectural Template 1, which has two clusters.</span></span> <span data-ttu-id="e260a-336">Каждый кластер является единой точкой отказа SAP для SAP ASCS/SCS и СУБД.</span><span class="sxs-lookup"><span data-stu-id="e260a-336">Each cluster is an SAP single point of failure for SAP ASCS/SCS and DBMS.</span></span>

<span data-ttu-id="e260a-337">Вот, где можно получить шаблоны Azure Resource Manager hello пример сценария описаны в этой статье.</span><span class="sxs-lookup"><span data-stu-id="e260a-337">Here's where you can get Azure Resource Manager templates for hello example scenario we describe in this article:</span></span>

* [<span data-ttu-id="e260a-338">Образ Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="e260a-338">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [<span data-ttu-id="e260a-339">Образ Azure Marketplace, использующий управляемые диски</span><span class="sxs-lookup"><span data-stu-id="e260a-339">Azure Marketplace image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md)  
* [<span data-ttu-id="e260a-340">Пользовательский образ</span><span class="sxs-lookup"><span data-stu-id="e260a-340">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)
* [<span data-ttu-id="e260a-341">Пользовательский образ, использующий управляемые диски</span><span class="sxs-lookup"><span data-stu-id="e260a-341">Custom image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-md)

<span data-ttu-id="e260a-342">Инфраструктура hello tooprepare для архитектуры шаблон 1:</span><span class="sxs-lookup"><span data-stu-id="e260a-342">tooprepare hello infrastructure for Architectural Template 1:</span></span>

- <span data-ttu-id="e260a-343">В hello в hello портала Azure **параметры** колонки в hello **SYSTEMAVAILABILITY** выберите **высокого уровня ДОСТУПНОСТИ**.</span><span class="sxs-lookup"><span data-stu-id="e260a-343">In hello Azure portal, on hello **Parameters** blade, in hello **SYSTEMAVAILABILITY** box, select **HA**.</span></span>

  ![Рис. 11. Настройка параметров Azure Resource Manager для SAP с высоким уровнем доступности][sap-ha-guide-figure-3000]

<span data-ttu-id="e260a-345">_**Рис. 11.** Настройка параметров Azure Resource Manager для SAP с высоким уровнем доступности_</span><span class="sxs-lookup"><span data-stu-id="e260a-345">_**Figure 11:** Set SAP high-availability Azure Resource Manager parameters_</span></span>


  <span data-ttu-id="e260a-346">Создайте шаблоны Hello:</span><span class="sxs-lookup"><span data-stu-id="e260a-346">hello templates create:</span></span>

  * <span data-ttu-id="e260a-347">**Виртуальные машины**:</span><span class="sxs-lookup"><span data-stu-id="e260a-347">**Virtual machines**:</span></span>
    * <span data-ttu-id="e260a-348">виртуальные машины сервера приложений SAP: <*SAPSystemSID*>-di-<*Number*>;</span><span class="sxs-lookup"><span data-stu-id="e260a-348">SAP Application Server virtual machines: <*SAPSystemSID*>-di-<*Number*></span></span>
    * <span data-ttu-id="e260a-349">виртуальные машины кластера SCS/SCS <*SAPSystemSID*>-ascs-<*Number*>;</span><span class="sxs-lookup"><span data-stu-id="e260a-349">ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-ascs-<*Number*></span></span>
    * <span data-ttu-id="e260a-350">виртуальные машины кластера СУБД: <*SID_системы_SAP*>-db-<*номер*>.</span><span class="sxs-lookup"><span data-stu-id="e260a-350">DBMS cluster: <*SAPSystemSID*>-db-<*Number*></span></span>

  * <span data-ttu-id="e260a-351">**Сетевые карты для всех виртуальных машин с соответствующими IP-адресами**:</span><span class="sxs-lookup"><span data-stu-id="e260a-351">**Network cards for all virtual machines, with associated IP addresses**:</span></span>
    * <span data-ttu-id="e260a-352"><*SAPSystemSID*>-nic-di-<*Number*>;</span><span class="sxs-lookup"><span data-stu-id="e260a-352"><*SAPSystemSID*>-nic-di-<*Number*></span></span>
    * <span data-ttu-id="e260a-353"><*SAPSystemSID*>-nic-ascs-<*Number*>;</span><span class="sxs-lookup"><span data-stu-id="e260a-353"><*SAPSystemSID*>-nic-ascs-<*Number*></span></span>
    * <span data-ttu-id="e260a-354"><*SAPSystemSID*>-nic-db-<*Number*>.</span><span class="sxs-lookup"><span data-stu-id="e260a-354"><*SAPSystemSID*>-nic-db-<*Number*></span></span>

  * <span data-ttu-id="e260a-355">**Учетные записи хранения (только неуправляемые диски)**</span><span class="sxs-lookup"><span data-stu-id="e260a-355">**Azure storage accounts (unmanaged disks only)**</span></span>

  * <span data-ttu-id="e260a-356">**Группы доступности** для:</span><span class="sxs-lookup"><span data-stu-id="e260a-356">**Availability groups** for:</span></span>
    * <span data-ttu-id="e260a-357">виртуальных машин сервера приложений SAP: <*SAPSystemSID*>-avset-di;</span><span class="sxs-lookup"><span data-stu-id="e260a-357">SAP Application Server virtual machines: <*SAPSystemSID*>-avset-di</span></span>
    * <span data-ttu-id="e260a-358">виртуальных машин кластера SCS/SCS: <*SAPSystemSID*>-avset-ascs;</span><span class="sxs-lookup"><span data-stu-id="e260a-358">SAP ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-avset-ascs</span></span>
    * <span data-ttu-id="e260a-359">виртуальных машин кластера СУБД: <*SAPSystemSID*>-avset-db.</span><span class="sxs-lookup"><span data-stu-id="e260a-359">DBMS cluster virtual machines: <*SAPSystemSID*>-avset-db</span></span>

  * <span data-ttu-id="e260a-360">**Внутренний балансировщик нагрузки Azure**:</span><span class="sxs-lookup"><span data-stu-id="e260a-360">**Azure internal load balancer**:</span></span>
    * <span data-ttu-id="e260a-361">Все порты для экземпляра ASCS/SCS hello и IP-адрес <*SAPSystemSID*> - балансировки нагрузки - ascs</span><span class="sxs-lookup"><span data-stu-id="e260a-361">With all ports for hello ASCS/SCS instance and IP address <*SAPSystemSID*>-lb-ascs</span></span>
    * <span data-ttu-id="e260a-362">Все порты для hello СУБД SQL Server и IP-адреса <*SAPSystemSID*> - балансировки нагрузки - db</span><span class="sxs-lookup"><span data-stu-id="e260a-362">With all ports for hello SQL Server DBMS and IP address <*SAPSystemSID*>-lb-db</span></span>

  * <span data-ttu-id="e260a-363">**Группа безопасности сети**: <*SAPSystemSID*>-nsg-ascs-0;</span><span class="sxs-lookup"><span data-stu-id="e260a-363">**Network security group**: <*SAPSystemSID*>-nsg-ascs-0</span></span>  
    * <span data-ttu-id="e260a-364">С открытым внешних toohello порт протокола удаленного рабочего стола (RDP) <*SAPSystemSID*> - ascs - 0 виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e260a-364">With an open external Remote Desktop Protocol (RDP) port toohello <*SAPSystemSID*>-ascs-0 virtual machine</span></span>

> [!NOTE]
> <span data-ttu-id="e260a-365">Все IP-адреса сетевых адаптеров hello и Azure внутренних подсистем балансировки нагрузки, **динамическое** по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e260a-365">All IP addresses of hello network cards and Azure internal load balancers are **dynamic** by default.</span></span> <span data-ttu-id="e260a-366">Изменить их слишком**статических** IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="e260a-366">Change them too**static** IP addresses.</span></span> <span data-ttu-id="e260a-367">Описано, как toodo это hello статьи.</span><span class="sxs-lookup"><span data-stu-id="e260a-367">We describe how toodo this later in hello article.</span></span>
>
>

### <span data-ttu-id="e260a-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>Развертывание виртуальных машин с toouse (между организациями) подключения к корпоративной сети в производственной среде</span><span class="sxs-lookup"><span data-stu-id="e260a-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> Deploy virtual machines with corporate network connectivity (cross-premises) toouse in production</span></span>
<span data-ttu-id="e260a-369">Для рабочих систем SAP виртуальные машины Azure развертываются с [подключением к корпоративной сети (распределенное развертывание)][planning-guide-2.2] с помощью VPN типа "сеть — сеть" Azure или канала Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e260a-369">For production SAP systems, deploy Azure virtual machines with [corporate network connectivity (cross-premises)][planning-guide-2.2] by using Azure Site-to-Site VPN or Azure ExpressRoute.</span></span>

> [!NOTE]
> <span data-ttu-id="e260a-370">Можно использовать имеющийся экземпляр виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="e260a-370">You can use your Azure Virtual Network instance.</span></span> <span data-ttu-id="e260a-371">Hello виртуальной сети и подсети уже созданы и подготовлен.</span><span class="sxs-lookup"><span data-stu-id="e260a-371">hello virtual network and subnet have already been created and prepared.</span></span>
>
>

1.  <span data-ttu-id="e260a-372">В hello в hello портала Azure **параметры** колонки в hello **NEWOREXISTINGSUBNET** выберите **существующие**.</span><span class="sxs-lookup"><span data-stu-id="e260a-372">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **existing**.</span></span>
2.  <span data-ttu-id="e260a-373">В hello **SUBNETID** добавьте полную строку hello сети подготовленный Azure SubnetID, где планируется toodeploy виртуальных машин Azure.</span><span class="sxs-lookup"><span data-stu-id="e260a-373">In hello **SUBNETID** box, add hello full string of your prepared Azure network SubnetID where you plan toodeploy your Azure virtual machines.</span></span>
3.  <span data-ttu-id="e260a-374">tooget список всех подсетей сети Azure, выполните следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e260a-374">tooget a list of all Azure network subnets, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  <span data-ttu-id="e260a-375">Hello **идентификатор** поле показывает hello **SUBNETID**.</span><span class="sxs-lookup"><span data-stu-id="e260a-375">hello **ID** field shows hello **SUBNETID**.</span></span>
4. <span data-ttu-id="e260a-376">список всех tooget **SUBNETID** значения, выполните следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e260a-376">tooget a list of all **SUBNETID** values, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  <span data-ttu-id="e260a-377">Hello **SUBNETID** выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e260a-377">hello **SUBNETID** looks like this:</span></span>

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <span data-ttu-id="e260a-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Развертывание облачных экземпляров SAP для тестирования и демонстрации</span><span class="sxs-lookup"><span data-stu-id="e260a-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Deploy cloud-only SAP instances for test and demo</span></span>
<span data-ttu-id="e260a-379">Систему SAP с высоким уровнем доступности можно развернуть в модели полностью облачного развертывания.</span><span class="sxs-lookup"><span data-stu-id="e260a-379">You can deploy your high-availability SAP system in a cloud-only deployment model.</span></span> <span data-ttu-id="e260a-380">Этот тип развертывания больше подходит для демонстрации и тестирования использования.</span><span class="sxs-lookup"><span data-stu-id="e260a-380">This kind of deployment primarily is useful for demo and test use cases.</span></span> <span data-ttu-id="e260a-381">Он не поддерживается для использования в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="e260a-381">It's not suited for production use cases.</span></span>

- <span data-ttu-id="e260a-382">В hello в hello портала Azure **параметры** колонки в hello **NEWOREXISTINGSUBNET** выберите **новый**.</span><span class="sxs-lookup"><span data-stu-id="e260a-382">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **new**.</span></span> <span data-ttu-id="e260a-383">Оставьте hello **SUBNETID** пустым.</span><span class="sxs-lookup"><span data-stu-id="e260a-383">Leave hello **SUBNETID** field empty.</span></span>

  <span data-ttu-id="e260a-384">шаблон автоматически создает диспетчер ресурсов Azure SAP Hello hello Azure виртуальной сети и подсети.</span><span class="sxs-lookup"><span data-stu-id="e260a-384">hello SAP Azure Resource Manager template automatically creates hello Azure virtual network and subnet.</span></span>

> [!NOTE]
> <span data-ttu-id="e260a-385">Необходимо также toodeploy по крайней мере один выделенных виртуальных машин для Active Directory и DNS-сервер в hello того же экземпляра виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="e260a-385">You also need toodeploy at least one dedicated virtual machine for Active Directory and DNS in hello same Azure Virtual Network instance.</span></span> <span data-ttu-id="e260a-386">Эти виртуальные машины не приводит к созданию шаблона Hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-386">hello template doesn't create these virtual machines.</span></span>
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a><span data-ttu-id="e260a-387">Подготовка инфраструктуры hello для архитектуры шаблона 2</span><span class="sxs-lookup"><span data-stu-id="e260a-387">Prepare hello infrastructure for Architectural Template 2</span></span>

<span data-ttu-id="e260a-388">Можно использовать этот шаблон диспетчера ресурсов Azure для SAP toohelp упростить развертывание ресурсов инфраструктура, необходимая для архитектуры шаблона 2 SAP.</span><span class="sxs-lookup"><span data-stu-id="e260a-388">You can use this Azure Resource Manager template for SAP toohelp simplify deployment of required infrastructure resources for SAP Architectural Template 2.</span></span>

<span data-ttu-id="e260a-389">Шаблоны Azure Resource Manager для сценария развертывания доступны здесь:</span><span class="sxs-lookup"><span data-stu-id="e260a-389">Here's where you can get Azure Resource Manager templates for this deployment scenario:</span></span>

* [<span data-ttu-id="e260a-390">Образ Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="e260a-390">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [<span data-ttu-id="e260a-391">Образ Azure Marketplace, использующий управляемые диски</span><span class="sxs-lookup"><span data-stu-id="e260a-391">Azure Marketplace image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged-md)  
* [<span data-ttu-id="e260a-392">Пользовательский образ</span><span class="sxs-lookup"><span data-stu-id="e260a-392">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)
* [<span data-ttu-id="e260a-393">Пользовательский образ, использующий управляемые диски</span><span class="sxs-lookup"><span data-stu-id="e260a-393">Custom image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged-md)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a><span data-ttu-id="e260a-394">Подготовка инфраструктуры hello для архитектуры шаблона 3</span><span class="sxs-lookup"><span data-stu-id="e260a-394">Prepare hello infrastructure for Architectural Template 3</span></span>

<span data-ttu-id="e260a-395">Можно подготовить инфраструктуру hello и настроить SAP для **multi-SID**.</span><span class="sxs-lookup"><span data-stu-id="e260a-395">You can prepare hello infrastructure and configure SAP for **multi-SID**.</span></span> <span data-ttu-id="e260a-396">Например, вы можете добавить дополнительный экземпляр SAP ASCS/SCS в *имеющуюся* конфигурацию кластера.</span><span class="sxs-lookup"><span data-stu-id="e260a-396">For example, you can add an additional SAP ASCS/SCS instance into an *existing* cluster configuration.</span></span> <span data-ttu-id="e260a-397">Дополнительные сведения см. в разделе [Настройка дополнительного экземпляра SAP ASCS/SCS в существующей конфигурации кластера toocreate multi-SID конфигурации SAP в диспетчере ресурсов Azure][sap-ha-multi-sid-guide].</span><span class="sxs-lookup"><span data-stu-id="e260a-397">For more information, see [Configure an additional SAP ASCS/SCS instance into an existing cluster configuration toocreate an SAP multi-SID configuration in Azure Resource Manager][sap-ha-multi-sid-guide].</span></span>

<span data-ttu-id="e260a-398">Если вы хотите toocreate на новый кластер с несколькими SID, можно использовать hello multi-SID [примеры использования шаблонов на GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="e260a-398">If you want toocreate a new multi-SID cluster, you can use hello multi-SID [quickstart templates on GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="e260a-399">toocreate на новый кластер с несколькими SID требуется hello toodeploy следующие три шаблона:</span><span class="sxs-lookup"><span data-stu-id="e260a-399">toocreate a new multi-SID cluster, you need toodeploy hello following three templates:</span></span>

* <span data-ttu-id="e260a-400">[шаблон ASCS/SCS](#ASCS-SCS-template);</span><span class="sxs-lookup"><span data-stu-id="e260a-400">[ASCS/SCS template](#ASCS-SCS-template)</span></span>
* <span data-ttu-id="e260a-401">[шаблон базы данных](#database-template);</span><span class="sxs-lookup"><span data-stu-id="e260a-401">[Database template](#database-template)</span></span>
* <span data-ttu-id="e260a-402">[шаблон серверов приложений](#application-servers-template).</span><span class="sxs-lookup"><span data-stu-id="e260a-402">[Application servers template](#application-servers-template)</span></span>

<span data-ttu-id="e260a-403">Hello следующих разделах содержатся дополнительные сведения о шаблонах hello и hello параметрами, необходимыми tooprovide в шаблонах hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-403">hello following sections have more details about hello templates and hello parameters you need tooprovide in hello templates.</span></span>

#### <span data-ttu-id="e260a-404"><a name="ASCS-SCS-template"></a> Шаблон ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e260a-404"><a name="ASCS-SCS-template"></a> ASCS/SCS template</span></span>

<span data-ttu-id="e260a-405">шаблон ASCS/SCS Hello развертывает две виртуальные машины, которые можно использовать toocreate отказоустойчивого кластера Windows Server, которая содержит несколько экземпляров ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="e260a-405">hello ASCS/SCS template deploys two virtual machines that you can use toocreate a Windows Server failover cluster that hosts multiple ASCS/SCS instances.</span></span>

<span data-ttu-id="e260a-406">tooset hello ASCS/SCS multi-SID для шаблона, в hello [ASCS/SCS multi-SID шаблона] [ sap-templates-3-tier-multisid-xscs-marketplace-image] или [ASCS/SCS multi-SID шаблона с помощью управляемых дисков] [ sap-templates-3-tier-multisid-xscs-marketplace-image-md], введите значения для hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="e260a-406">tooset up hello ASCS/SCS multi-SID template, in hello [ASCS/SCS multi-SID template][sap-templates-3-tier-multisid-xscs-marketplace-image] or [ASCS/SCS multi-SID template using Managed Disks][sap-templates-3-tier-multisid-xscs-marketplace-image-md], enter values for hello following parameters:</span></span>

  - <span data-ttu-id="e260a-407">**Префикс ресурса.**</span><span class="sxs-lookup"><span data-stu-id="e260a-407">**Resource Prefix**.</span></span>  <span data-ttu-id="e260a-408">Задайте hello ресурсов префикса, используемые tooprefix все ресурсы, которые создаются во время развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-408">Set hello resource prefix, which is used tooprefix all resources that are created during hello deployment.</span></span> <span data-ttu-id="e260a-409">Поскольку ресурсы hello не принадлежат одной системы SAP tooonly, префикс hello hello ресурса не hello SID из одной системы SAP.</span><span class="sxs-lookup"><span data-stu-id="e260a-409">Because hello resources do not belong tooonly one SAP system, hello prefix of hello resource is not hello SID of one SAP system.</span></span>  <span data-ttu-id="e260a-410">Hello префикс должен быть в диапазоне **трех до шести символов**.</span><span class="sxs-lookup"><span data-stu-id="e260a-410">hello prefix must be between **three and six characters**.</span></span>
  - <span data-ttu-id="e260a-411">**Тип стека.**</span><span class="sxs-lookup"><span data-stu-id="e260a-411">**Stack Type**.</span></span> <span data-ttu-id="e260a-412">Выберите тип стека hello hello системы SAP.</span><span class="sxs-lookup"><span data-stu-id="e260a-412">Select hello stack type of hello SAP system.</span></span> <span data-ttu-id="e260a-413">В зависимости от типа hello стека Подсистема балансировки нагрузки Azure имеет один (ABAP или Java только) или две (ABAP + Java) частных IP-адресов в системе SAP.</span><span class="sxs-lookup"><span data-stu-id="e260a-413">Depending on hello stack type, Azure Load Balancer has one (ABAP or Java only) or two (ABAP+Java) private IP addresses per SAP system.</span></span>
  -  <span data-ttu-id="e260a-414">**Тип ОС.**</span><span class="sxs-lookup"><span data-stu-id="e260a-414">**OS Type**.</span></span> <span data-ttu-id="e260a-415">Выберите операционную систему hello hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e260a-415">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="e260a-416">**Количество систем SAP.**</span><span class="sxs-lookup"><span data-stu-id="e260a-416">**SAP System Count**.</span></span> <span data-ttu-id="e260a-417">Выберите номер hello систем SAP требуется tooinstall в этом кластере.</span><span class="sxs-lookup"><span data-stu-id="e260a-417">Select hello number of SAP systems you want tooinstall in this cluster.</span></span>
  -  <span data-ttu-id="e260a-418">**Доступность системы.**</span><span class="sxs-lookup"><span data-stu-id="e260a-418">**System Availability**.</span></span> <span data-ttu-id="e260a-419">Выберите **высокую доступность**.</span><span class="sxs-lookup"><span data-stu-id="e260a-419">Select **HA**.</span></span>
  -  <span data-ttu-id="e260a-420">**Имя пользователя и пароль администратора.**</span><span class="sxs-lookup"><span data-stu-id="e260a-420">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="e260a-421">Создайте нового пользователя, который может быть используется toosign toohello машине.</span><span class="sxs-lookup"><span data-stu-id="e260a-421">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="e260a-422">**Новая или имеющаяся подсеть.**</span><span class="sxs-lookup"><span data-stu-id="e260a-422">**New Or Existing Subnet**.</span></span> <span data-ttu-id="e260a-423">Определите, следует ли создать виртуальную сеть и подсеть или использовать имеющуюся подсеть.</span><span class="sxs-lookup"><span data-stu-id="e260a-423">Set whether a new virtual network and subnet should be created, or an existing subnet should be used.</span></span> <span data-ttu-id="e260a-424">При наличии виртуальной сети, подключенной tooyour локальную сеть, выберите **существующие**.</span><span class="sxs-lookup"><span data-stu-id="e260a-424">If you already have a virtual network that is connected tooyour on-premises network, select **existing**.</span></span>
  -  <span data-ttu-id="e260a-425">**Идентификатор подсети.** Задайте идентификатор hello toowhich hello hello подсети, которые должны быть подключены виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="e260a-425">**Subnet Id**. Set hello ID of hello subnet toowhich hello virtual machines should be connected.</span></span> <span data-ttu-id="e260a-426">Выберите подсеть hello виртуальной частной сети (VPN) или ExpressRoute виртуальной сети tooconnect hello виртуальной машины tooyour локальной сети.</span><span class="sxs-lookup"><span data-stu-id="e260a-426">Select hello subnet of your virtual private network (VPN) or ExpressRoute virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="e260a-427">Идентификатор Hello обычно выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e260a-427">hello ID usually looks like this:</span></span>

   <span data-ttu-id="e260a-428">/subscriptions/<*идентификатор_подписки*>/resourceGroups/<*имя_группы_ресурсов*>/providers/Microsoft.Network/virtualNetworks/<*имя_виртуальной_сети*>/subnets/<*имя_подсети*></span><span class="sxs-lookup"><span data-stu-id="e260a-428">/subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span></span>

<span data-ttu-id="e260a-429">шаблон Hello развертывает один экземпляр подсистемы балансировки нагрузки Azure, которая поддерживает несколько систем SAP.</span><span class="sxs-lookup"><span data-stu-id="e260a-429">hello template deploys one Azure Load Balancer instance, which supports multiple SAP systems.</span></span>

- <span data-ttu-id="e260a-430">экземпляры ASCS Hello настроены для номера экземпляра 00, 10, 20...</span><span class="sxs-lookup"><span data-stu-id="e260a-430">hello ASCS instances are configured for instance number 00, 10, 20...</span></span>
- <span data-ttu-id="e260a-431">экземпляры SCS Hello настроены для номера экземпляра 01, 11, 21...</span><span class="sxs-lookup"><span data-stu-id="e260a-431">hello SCS instances are configured for instance number 01, 11, 21...</span></span>
- <span data-ttu-id="e260a-432">экземпляры Hello ASCS постановки в очередь репликации сервера (ющих Методов) (Linux) настроены для номера экземпляра 02, 12, 22...</span><span class="sxs-lookup"><span data-stu-id="e260a-432">hello ASCS Enqueue Replication Server (ERS) (Linux only) instances are configured for instance number 02, 12, 22...</span></span>
- <span data-ttu-id="e260a-433">экземпляры Hello SCS ющих Методов (Linux) настроены для номера экземпляра 03, 13, 23...</span><span class="sxs-lookup"><span data-stu-id="e260a-433">hello SCS ERS (Linux only) instances are configured for instance number 03, 13, 23...</span></span>

<span data-ttu-id="e260a-434">Hello балансировки нагрузки содержит 1 (2 для Linux) VIP(s), 1 x виртуальных IP-адресов для ASCS/SCS и 1 x виртуальных IP-адресов для ющих Методов (Linux).</span><span class="sxs-lookup"><span data-stu-id="e260a-434">hello load balancer contains 1 (2 for Linux) VIP(s), 1x VIP for ASCS/SCS and 1x VIP for ERS (Linux only).</span></span>

<span data-ttu-id="e260a-435">Hello следующий список содержит все правила, (где x — номер hello hello системы SAP, например, 1, 2, 3...) подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e260a-435">hello following list contains all load balancing rules (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="e260a-436">порты, связанные с Windows, для каждой системы SAP: 445, 5985;</span><span class="sxs-lookup"><span data-stu-id="e260a-436">Windows-specific ports for every SAP system: 445, 5985</span></span>
- <span data-ttu-id="e260a-437">порты ASCS (номер экземпляра x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016;</span><span class="sxs-lookup"><span data-stu-id="e260a-437">ASCS ports (instance number x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span></span>
- <span data-ttu-id="e260a-438">порты SCS (номер экземпляра x 1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116;</span><span class="sxs-lookup"><span data-stu-id="e260a-438">SCS ports (instance number x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span></span>
- <span data-ttu-id="e260a-439">порты ASCS ERS на Linux (номер экземпляра x 2): 33x2, 5x213, 5x214, 5x216;</span><span class="sxs-lookup"><span data-stu-id="e260a-439">ASCS ERS ports on Linux (instance number x2): 33x2, 5x213, 5x214, 5x216</span></span>
- <span data-ttu-id="e260a-440">порты SCS ERS на Linux (номер экземпляра x 3): 33x3, 5x313, 5x314, 5x316.</span><span class="sxs-lookup"><span data-stu-id="e260a-440">SCS ERS ports on Linux (instance number x3): 33x3, 5x313, 5x314, 5x316</span></span>

<span data-ttu-id="e260a-441">Подсистема балансировки нагрузки Hello — настроенное toouse hello, следующие порты проверки (где x — номер hello hello системы SAP, например, 1, 2, 3...):</span><span class="sxs-lookup"><span data-stu-id="e260a-441">hello load balancer is configured toouse hello following probe ports (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="e260a-442">порт пробы внутреннего балансировщика нагрузки ASCS/SCS: 620x0;</span><span class="sxs-lookup"><span data-stu-id="e260a-442">ASCS/SCS internal load balancer probe port: 620x0</span></span>
- <span data-ttu-id="e260a-443">порт пробы внутреннего балансировщика нагрузки ERS (только Linux): 621x2.</span><span class="sxs-lookup"><span data-stu-id="e260a-443">ERS internal load balancer probe port (Linux only): 621x2</span></span>

#### <span data-ttu-id="e260a-444"><a name="database-template"></a> Шаблон базы данных</span><span class="sxs-lookup"><span data-stu-id="e260a-444"><a name="database-template"></a> Database template</span></span>

<span data-ttu-id="e260a-445">Шаблон базы данных Hello развертывает одну или две виртуальные машины, которые можно использовать tooinstall hello система управления реляционными базами данных (RDBMS) для одной системы SAP.</span><span class="sxs-lookup"><span data-stu-id="e260a-445">hello database template deploys one or two virtual machines that you can use tooinstall hello relational database management system (RDBMS) for one SAP system.</span></span> <span data-ttu-id="e260a-446">Например при развертывании шаблона ASCS/SCS для пяти систем SAP, необходимо toodeploy этот шаблон пять раз.</span><span class="sxs-lookup"><span data-stu-id="e260a-446">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="e260a-447">tooset шаблон multi-SID базы данных hello в hello [шаблона базы данных несколькими SID] [ sap-templates-3-tier-multisid-db-marketplace-image] или [multi-SID шаблона базы данных, с помощью управляемых дисков] [ sap-templates-3-tier-multisid-db-marketplace-image-md], введите значения для hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="e260a-447">tooset up hello database multi-SID template, in hello [database multi-SID template][sap-templates-3-tier-multisid-db-marketplace-image] or [database multi-SID template using Managed Disks][sap-templates-3-tier-multisid-db-marketplace-image-md], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="e260a-448">**Идентификатор системы SAP.** Введите идентификатор системы SAP hello hello требуется tooinstall системы SAP.</span><span class="sxs-lookup"><span data-stu-id="e260a-448">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="e260a-449">Идентификатор Hello будет использоваться в качестве префикса hello ресурсы, которые развертываются.</span><span class="sxs-lookup"><span data-stu-id="e260a-449">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="e260a-450">**Тип ОС.**</span><span class="sxs-lookup"><span data-stu-id="e260a-450">**Os Type**.</span></span> <span data-ttu-id="e260a-451">Выберите операционную систему hello hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e260a-451">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="e260a-452">**Тип базы данных.**</span><span class="sxs-lookup"><span data-stu-id="e260a-452">**Dbtype**.</span></span> <span data-ttu-id="e260a-453">Выберите тип hello hello базы данных требуется tooinstall на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-453">Select hello type of hello database you want tooinstall on hello cluster.</span></span> <span data-ttu-id="e260a-454">Выберите **SQL** Если tooinstall Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e260a-454">Select **SQL** if you want tooinstall Microsoft SQL Server.</span></span> <span data-ttu-id="e260a-455">Выберите **HANA** при планировании tooinstall SAP HANA hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e260a-455">Select **HANA** if you plan tooinstall SAP HANA on hello virtual machines.</span></span> <span data-ttu-id="e260a-456">Убедитесь, что tooselect hello правильный тип операционной системы: выберите **Windows** для SQL, а затем выберите ОС Linux для HANA.</span><span class="sxs-lookup"><span data-stu-id="e260a-456">Make sure tooselect hello correct operating system type: select **Windows** for SQL, and select a Linux distribution for HANA.</span></span> <span data-ttu-id="e260a-457">Hello подсистемы балансировки нагрузки Azure, подключенной toohello виртуальные машины будут настроены toosupport hello выбранной базы данных типа:</span><span class="sxs-lookup"><span data-stu-id="e260a-457">hello Azure Load Balancer that is connected toohello virtual machines will be configured toosupport hello selected database type:</span></span>
    * <span data-ttu-id="e260a-458">**SQL.**</span><span class="sxs-lookup"><span data-stu-id="e260a-458">**SQL**.</span></span> <span data-ttu-id="e260a-459">Подсистема балансировки нагрузки Hello будет балансировать нагрузку порт 1433.</span><span class="sxs-lookup"><span data-stu-id="e260a-459">hello load balancer will load-balance port 1433.</span></span> <span data-ttu-id="e260a-460">Убедитесь, что toouse этот порт для настройки SQL Server Always On.</span><span class="sxs-lookup"><span data-stu-id="e260a-460">Make sure toouse this port for your SQL Server Always On setup.</span></span>
    * <span data-ttu-id="e260a-461">**HANA.**</span><span class="sxs-lookup"><span data-stu-id="e260a-461">**HANA**.</span></span> <span data-ttu-id="e260a-462">Подсистема балансировки нагрузки Hello будет балансировать нагрузку порты 35015 и 35017.</span><span class="sxs-lookup"><span data-stu-id="e260a-462">hello load balancer will load-balance ports 35015 and 35017.</span></span> <span data-ttu-id="e260a-463">Убедитесь, что tooinstall SAP HANA с номером экземпляра **50**.</span><span class="sxs-lookup"><span data-stu-id="e260a-463">Make sure tooinstall SAP HANA with instance number **50**.</span></span>
    <span data-ttu-id="e260a-464">порт пробы 62550 будет использоваться службой балансировки нагрузки Hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-464">hello load balancer will use probe port 62550.</span></span>
  -  <span data-ttu-id="e260a-465">**Размер системы SAP.**</span><span class="sxs-lookup"><span data-stu-id="e260a-465">**Sap System Size**.</span></span> <span data-ttu-id="e260a-466">Предоставляет набор hello число SAPS hello новую систему.</span><span class="sxs-lookup"><span data-stu-id="e260a-466">Set hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="e260a-467">Если вы не уверены, сколько SAPS hello систему необходимо, обратитесь к партнеру технологии SAP или системные интеграторы.</span><span class="sxs-lookup"><span data-stu-id="e260a-467">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="e260a-468">**Доступность системы.**</span><span class="sxs-lookup"><span data-stu-id="e260a-468">**System Availability**.</span></span> <span data-ttu-id="e260a-469">Выберите **высокую доступность**.</span><span class="sxs-lookup"><span data-stu-id="e260a-469">Select **HA**.</span></span>
  -  <span data-ttu-id="e260a-470">**Имя пользователя и пароль администратора.**</span><span class="sxs-lookup"><span data-stu-id="e260a-470">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="e260a-471">Создайте нового пользователя, который может быть используется toosign toohello машине.</span><span class="sxs-lookup"><span data-stu-id="e260a-471">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="e260a-472">**Идентификатор подсети.** Введите идентификатор hello hello подсети, который использовался во время развертывания hello шаблона ASCS/SCS hello, или идентификатор hello hello подсети, в которой была создана как часть развертывания шаблона ASCS/SCS hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-472">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>

#### <span data-ttu-id="e260a-473"><a name="application-servers-template"></a> Шаблон серверов приложений</span><span class="sxs-lookup"><span data-stu-id="e260a-473"><a name="application-servers-template"></a> Application servers template</span></span>

<span data-ttu-id="e260a-474">шаблон серверы приложений Hello развертывает два или более виртуальных машин, которые могут использоваться как экземпляры сервера приложений SAP для одной системы SAP.</span><span class="sxs-lookup"><span data-stu-id="e260a-474">hello application servers template deploys two or more virtual machines that can be used as SAP Application Server instances for one SAP system.</span></span> <span data-ttu-id="e260a-475">Например при развертывании шаблона ASCS/SCS для пяти систем SAP, необходимо toodeploy этот шаблон пять раз.</span><span class="sxs-lookup"><span data-stu-id="e260a-475">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="e260a-476">tooset hello приложения серверов multi-SID для шаблона, в hello [шаблон SID нескольких серверов приложений] [ sap-templates-3-tier-multisid-apps-marketplace-image] или [шаблон SID нескольких серверов приложений, с помощью управляемых дисков] [ sap-templates-3-tier-multisid-apps-marketplace-image-md], введите значения для hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="e260a-476">tooset up hello application servers multi-SID template, in hello [application servers multi-SID template][sap-templates-3-tier-multisid-apps-marketplace-image] or [application servers multi-SID template using Managed Disks][sap-templates-3-tier-multisid-apps-marketplace-image-md], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="e260a-477">**Идентификатор системы SAP.** Введите идентификатор системы SAP hello hello требуется tooinstall системы SAP.</span><span class="sxs-lookup"><span data-stu-id="e260a-477">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="e260a-478">Идентификатор Hello будет использоваться в качестве префикса hello ресурсы, которые развертываются.</span><span class="sxs-lookup"><span data-stu-id="e260a-478">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="e260a-479">**Тип ОС.**</span><span class="sxs-lookup"><span data-stu-id="e260a-479">**Os Type**.</span></span> <span data-ttu-id="e260a-480">Выберите операционную систему hello hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e260a-480">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="e260a-481">**Размер системы SAP.**</span><span class="sxs-lookup"><span data-stu-id="e260a-481">**Sap System Size**.</span></span> <span data-ttu-id="e260a-482">предоставляет Hello число SAPS hello новую систему.</span><span class="sxs-lookup"><span data-stu-id="e260a-482">hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="e260a-483">Если вы не уверены, сколько SAPS hello систему необходимо, обратитесь к партнеру технологии SAP или системные интеграторы.</span><span class="sxs-lookup"><span data-stu-id="e260a-483">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="e260a-484">**Доступность системы.**</span><span class="sxs-lookup"><span data-stu-id="e260a-484">**System Availability**.</span></span> <span data-ttu-id="e260a-485">Выберите **высокую доступность**.</span><span class="sxs-lookup"><span data-stu-id="e260a-485">Select **HA**.</span></span>
  -  <span data-ttu-id="e260a-486">**Имя пользователя и пароль администратора.**</span><span class="sxs-lookup"><span data-stu-id="e260a-486">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="e260a-487">Создайте нового пользователя, который может быть используется toosign toohello машине.</span><span class="sxs-lookup"><span data-stu-id="e260a-487">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="e260a-488">**Идентификатор подсети.** Введите идентификатор hello hello подсети, который использовался во время развертывания hello шаблона ASCS/SCS hello, или идентификатор hello hello подсети, в которой была создана как часть развертывания шаблона ASCS/SCS hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-488">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>


### <span data-ttu-id="e260a-489"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Виртуальная сеть Azure</span><span class="sxs-lookup"><span data-stu-id="e260a-489"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure virtual network</span></span>
<span data-ttu-id="e260a-490">В нашем примере hello адресное пространство виртуальной сети Azure hello — 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="e260a-490">In our example, hello address space of hello Azure virtual network is 10.0.0.0/16.</span></span> <span data-ttu-id="e260a-491">Существует одна подсеть **Subnet** с диапазоном адресов 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="e260a-491">There is one subnet called **Subnet**, with an address range of 10.0.0.0/24.</span></span> <span data-ttu-id="e260a-492">Все виртуальные машины и внутренние балансировщики нагрузки развертываются в этой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e260a-492">All virtual machines and internal load balancers are deployed in this virtual network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e260a-493">Не вносите никаких изменений параметров сети toohello внутри hello гостевой операционной системы.</span><span class="sxs-lookup"><span data-stu-id="e260a-493">Don't make any changes toohello network settings inside hello guest operating system.</span></span> <span data-ttu-id="e260a-494">Например, IP-адреса, DNS-серверы и подсети.</span><span class="sxs-lookup"><span data-stu-id="e260a-494">This includes IP addresses, DNS servers, and subnet.</span></span> <span data-ttu-id="e260a-495">Все параметры сети настраиваются с помощью Azure.</span><span class="sxs-lookup"><span data-stu-id="e260a-495">Configure all your network settings in Azure.</span></span> <span data-ttu-id="e260a-496">Hello протокол динамической настройки узла (DHCP) служба передает параметры.</span><span class="sxs-lookup"><span data-stu-id="e260a-496">hello Dynamic Host Configuration Protocol (DHCP) service propagates your settings.</span></span>
>
>

### <span data-ttu-id="e260a-497"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> IP-адреса DNS</span><span class="sxs-lookup"><span data-stu-id="e260a-497"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP addresses</span></span>

<span data-ttu-id="e260a-498">tooset hello требуемые DNS IP-адресов, hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="e260a-498">tooset hello required DNS IP addresses, do hello following steps.</span></span>

1.  <span data-ttu-id="e260a-499">В hello в hello портала Azure **DNS-серверы** колонки, убедитесь, что виртуальной сети **DNS-серверы** был установлен слишком**настраиваемый DNS**.</span><span class="sxs-lookup"><span data-stu-id="e260a-499">In hello Azure portal, on hello **DNS servers** blade, make sure that your virtual network **DNS servers** option is set too**Custom DNS**.</span></span>
2.  <span data-ttu-id="e260a-500">Выберите параметры на основе типа сети, к которой у вас есть hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-500">Select your settings based on hello type of network you have.</span></span> <span data-ttu-id="e260a-501">Дополнительные сведения см. в разделе hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="e260a-501">For more information, see hello following resources:</span></span>
    * <span data-ttu-id="e260a-502">[Подключение к корпоративной сети (между организациями)][planning-guide-2.2]: добавьте hello IP-адреса DNS-серверов в локальной среде hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-502">[Corporate network connectivity (cross-premises)][planning-guide-2.2]: Add hello IP addresses of hello on-premises DNS servers.</span></span>  
    <span data-ttu-id="e260a-503">Вы можете расширить локальные DNS серверов toohello виртуальных машин, работающих в Azure.</span><span class="sxs-lookup"><span data-stu-id="e260a-503">You can extend on-premises DNS servers toohello virtual machines that are running in Azure.</span></span> <span data-ttu-id="e260a-504">В этом случае можно добавить IP-адреса hello hello Azure виртуальные машины, на которых выполняется служба DNS hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-504">In that scenario, you can add hello IP addresses of hello Azure virtual machines on which you run hello DNS service.</span></span>
    * <span data-ttu-id="e260a-505">[Развертывание только в облаке][planning-guide-2.1]: развертывание дополнительную виртуальную машину в hello же экземпляр виртуальной сети, который служит в качестве DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="e260a-505">[Cloud-only deployment][planning-guide-2.1]: Deploy an additional virtual machine in hello same Virtual Network instance that serves as a DNS server.</span></span> <span data-ttu-id="e260a-506">Добавление IP-адреса hello hello Azure виртуальных машин, которые вы настроили службу toorun DNS.</span><span class="sxs-lookup"><span data-stu-id="e260a-506">Add hello IP addresses of hello Azure virtual machines that you've set up toorun DNS service.</span></span>

    ![Рис. 12. Настройка DNS-серверов для виртуальной сети Azure][sap-ha-guide-figure-3001]

    <span data-ttu-id="e260a-508">_**Рис. 12.** Настройка DNS-серверов для виртуальной сети Azure_</span><span class="sxs-lookup"><span data-stu-id="e260a-508">_**Figure 12:** Configure DNS servers for Azure Virtual Network_</span></span>

  > [!NOTE]
  > <span data-ttu-id="e260a-509">При изменении IP-адреса hello hello DNS-серверов необходимо tooapply виртуальных машин Azure hello toorestart Здравствуйте, изменение и распространение hello новый DNS-серверов.</span><span class="sxs-lookup"><span data-stu-id="e260a-509">If you change hello IP addresses of hello DNS servers, you need toorestart hello Azure virtual machines tooapply hello change and propagate hello new DNS servers.</span></span>
  >
  >

<span data-ttu-id="e260a-510">В нашем примере hello служба DNS установлен и настроен на этих виртуальных машинах:</span><span class="sxs-lookup"><span data-stu-id="e260a-510">In our example, hello DNS service is installed and configured on these Windows virtual machines:</span></span>

| <span data-ttu-id="e260a-511">Роль виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e260a-511">Virtual machine role</span></span> | <span data-ttu-id="e260a-512">Имя узла виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e260a-512">Virtual machine host name</span></span> | <span data-ttu-id="e260a-513">Имя сетевой карты</span><span class="sxs-lookup"><span data-stu-id="e260a-513">Network card name</span></span> | <span data-ttu-id="e260a-514">Статический IP-адрес</span><span class="sxs-lookup"><span data-stu-id="e260a-514">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e260a-515">1-й DNS-сервер</span><span class="sxs-lookup"><span data-stu-id="e260a-515">First DNS server</span></span> |<span data-ttu-id="e260a-516">domcontr-0</span><span class="sxs-lookup"><span data-stu-id="e260a-516">domcontr-0</span></span> |<span data-ttu-id="e260a-517">pr1-nic-domcontr-0</span><span class="sxs-lookup"><span data-stu-id="e260a-517">pr1-nic-domcontr-0</span></span> |<span data-ttu-id="e260a-518">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="e260a-518">10.0.0.10</span></span> |
| <span data-ttu-id="e260a-519">2-й DNS-сервер</span><span class="sxs-lookup"><span data-stu-id="e260a-519">Second DNS server</span></span> |<span data-ttu-id="e260a-520">domcontr-1</span><span class="sxs-lookup"><span data-stu-id="e260a-520">domcontr-1</span></span> |<span data-ttu-id="e260a-521">pr1-nic-domcontr-1</span><span class="sxs-lookup"><span data-stu-id="e260a-521">pr1-nic-domcontr-1</span></span> |<span data-ttu-id="e260a-522">10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="e260a-522">10.0.0.11</span></span> |

### <span data-ttu-id="e260a-523"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>Имена узлов и статические IP-адреса для кластеризованного экземпляра SAP ASCS/SCS hello и кластеризованного экземпляра СУБД</span><span class="sxs-lookup"><span data-stu-id="e260a-523"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> Host names and static IP addresses for hello SAP ASCS/SCS clustered instance and DBMS clustered instance</span></span>

<span data-ttu-id="e260a-524">Для локального развертывания необходимы следующие зарезервированные имена узлов и IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="e260a-524">For on-premises deployment, you need these reserved host names and IP addresses:</span></span>

| <span data-ttu-id="e260a-525">Роль имени виртуального узла</span><span class="sxs-lookup"><span data-stu-id="e260a-525">Virtual host name role</span></span> | <span data-ttu-id="e260a-526">Имя виртуального узла</span><span class="sxs-lookup"><span data-stu-id="e260a-526">Virtual host name</span></span> | <span data-ttu-id="e260a-527">Виртуальный статический IP-адрес</span><span class="sxs-lookup"><span data-stu-id="e260a-527">Virtual static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e260a-528">Имя 1-го виртуального узла кластера SAP ASCS/SCS (используется для управления кластером)</span><span class="sxs-lookup"><span data-stu-id="e260a-528">SAP ASCS/SCS first cluster virtual host name (for cluster management)</span></span> |<span data-ttu-id="e260a-529">pr1-ascs-vir</span><span class="sxs-lookup"><span data-stu-id="e260a-529">pr1-ascs-vir</span></span> |<span data-ttu-id="e260a-530">10.0.0.42</span><span class="sxs-lookup"><span data-stu-id="e260a-530">10.0.0.42</span></span> |
| <span data-ttu-id="e260a-531">Имя виртуального узла экземпляра SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e260a-531">SAP ASCS/SCS instance virtual host name</span></span> |<span data-ttu-id="e260a-532">pr1-ascs-sap</span><span class="sxs-lookup"><span data-stu-id="e260a-532">pr1-ascs-sap</span></span> |<span data-ttu-id="e260a-533">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="e260a-533">10.0.0.43</span></span> |
| <span data-ttu-id="e260a-534">Имя 2-го виртуального узла кластера SAP ASCS/SCS (используется для управления кластером)</span><span class="sxs-lookup"><span data-stu-id="e260a-534">SAP DBMS second cluster virtual host name (cluster management)</span></span> |<span data-ttu-id="e260a-535">pr1-dbms-vir</span><span class="sxs-lookup"><span data-stu-id="e260a-535">pr1-dbms-vir</span></span> |<span data-ttu-id="e260a-536">10.0.0.32</span><span class="sxs-lookup"><span data-stu-id="e260a-536">10.0.0.32</span></span> |

<span data-ttu-id="e260a-537">При создании кластера hello создать hello имена виртуальных узлов **pr1 ascs-vir** и **pr1 СУБД vir** и hello соответствующие IP-адреса, которые управляют самого кластера hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-537">When you create hello cluster, create hello virtual host names **pr1-ascs-vir** and **pr1-dbms-vir** and hello associated IP addresses that manage hello cluster itself.</span></span> <span data-ttu-id="e260a-538">Сведения о том, как toodo, см. в разделе [сбора узлы кластера в кластере][sap-ha-guide-8.12.1].</span><span class="sxs-lookup"><span data-stu-id="e260a-538">For information about how toodo this, see [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1].</span></span>

<span data-ttu-id="e260a-539">Можно вручную создать hello другие два имени виртуального узла **pr1 ascs sap** и **pr1 СУБД sap**, и hello связанные IP-адресов на DNS-сервере hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-539">You can manually create hello other two virtual host names, **pr1-ascs-sap** and **pr1-dbms-sap**, and hello associated IP addresses, on hello DNS server.</span></span> <span data-ttu-id="e260a-540">Hello кластеризованного экземпляра SAP ASCS/SCS и hello кластеризованный экземпляр СУБД используйте следующие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="e260a-540">hello clustered SAP ASCS/SCS instance and hello clustered DBMS instance use these resources.</span></span> <span data-ttu-id="e260a-541">Сведения о том, как toodo, см. в разделе [Создание виртуального имени узла для кластеризованного экземпляра SAP ASCS/SCS][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="e260a-541">For information about how toodo this, see [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1].</span></span>

### <span data-ttu-id="e260a-542"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>Задать статический IP-адресов для виртуальных машин hello SAP</span><span class="sxs-lookup"><span data-stu-id="e260a-542"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> Set static IP addresses for hello SAP virtual machines</span></span>
<span data-ttu-id="e260a-543">После развертывания toouse hello виртуальных машин в кластере, необходимо tooset статические IP-адреса для всех виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e260a-543">After you deploy hello virtual machines toouse in your cluster, you need tooset static IP addresses for all virtual machines.</span></span> <span data-ttu-id="e260a-544">Для этого в конфигурации виртуальной сети Azure hello, а не в hello гостевой операционной системы.</span><span class="sxs-lookup"><span data-stu-id="e260a-544">Do this in hello Azure Virtual Network configuration, and not in hello guest operating system.</span></span>

1.  <span data-ttu-id="e260a-545">В hello портал Azure, выберите **группы ресурсов** > **сетевой карты** > **параметры** > **IP-адрес** .</span><span class="sxs-lookup"><span data-stu-id="e260a-545">In hello Azure portal, select **Resource Group** > **Network Card** > **Settings** > **IP Address**.</span></span>
2.  <span data-ttu-id="e260a-546">На hello **IP-адреса** колонки в разделе **назначения**выберите **статических**.</span><span class="sxs-lookup"><span data-stu-id="e260a-546">On hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span> <span data-ttu-id="e260a-547">В hello **IP-адрес** введите hello IP-адреса, которые должны toouse.</span><span class="sxs-lookup"><span data-stu-id="e260a-547">In hello **IP address** box, enter hello IP address that you want toouse.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e260a-548">При изменении IP-адрес сетевой карты hello hello необходимо tooapply виртуальных машин Azure hello toorestart hello изменений.</span><span class="sxs-lookup"><span data-stu-id="e260a-548">If you change hello IP address of hello network card, you need toorestart hello Azure virtual machines tooapply hello change.</span></span>  
  >
  >

  ![Рис. 13: Задать статический IP-адресов для сетевой карты hello каждой виртуальной машины][sap-ha-guide-figure-3002]

  <span data-ttu-id="e260a-550">_**Рис. 13:** набор статических IP-адресов для сетевой карты hello каждой виртуальной машины_</span><span class="sxs-lookup"><span data-stu-id="e260a-550">_**Figure 13:** Set static IP addresses for hello network card of each virtual machine_</span></span>

  <span data-ttu-id="e260a-551">Повторите этот шаг для всех сетевых интерфейсов, то есть для всех виртуальных машин, включая виртуальные машины, которые требуется toouse для службы DNS и Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e260a-551">Repeat this step for all network interfaces, that is, for all virtual machines, including virtual machines that you want toouse for your Active Directory/DNS service.</span></span>

<span data-ttu-id="e260a-552">В нашем примере используются следующие виртуальные машины и статические IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="e260a-552">In our example, we have these virtual machines and static IP addresses:</span></span>

| <span data-ttu-id="e260a-553">Роль виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e260a-553">Virtual machine role</span></span> | <span data-ttu-id="e260a-554">Имя узла виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e260a-554">Virtual machine host name</span></span> | <span data-ttu-id="e260a-555">Имя сетевой карты</span><span class="sxs-lookup"><span data-stu-id="e260a-555">Network card name</span></span> | <span data-ttu-id="e260a-556">Статический IP-адрес</span><span class="sxs-lookup"><span data-stu-id="e260a-556">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e260a-557">Первый экземпляр сервера приложений SAP</span><span class="sxs-lookup"><span data-stu-id="e260a-557">First SAP Application Server instance</span></span> |<span data-ttu-id="e260a-558">pr1-di-0</span><span class="sxs-lookup"><span data-stu-id="e260a-558">pr1-di-0</span></span> |<span data-ttu-id="e260a-559">pr1-nic-di-0</span><span class="sxs-lookup"><span data-stu-id="e260a-559">pr1-nic-di-0</span></span> |<span data-ttu-id="e260a-560">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="e260a-560">10.0.0.50</span></span> |
| <span data-ttu-id="e260a-561">Второй экземпляр сервера приложений SAP</span><span class="sxs-lookup"><span data-stu-id="e260a-561">Second SAP Application Server instance</span></span> |<span data-ttu-id="e260a-562">pr1-di-1</span><span class="sxs-lookup"><span data-stu-id="e260a-562">pr1-di-1</span></span> |<span data-ttu-id="e260a-563">pr1-nic-di-1</span><span class="sxs-lookup"><span data-stu-id="e260a-563">pr1-nic-di-1</span></span> |<span data-ttu-id="e260a-564">10.0.0.51</span><span class="sxs-lookup"><span data-stu-id="e260a-564">10.0.0.51</span></span> |
| <span data-ttu-id="e260a-565">...</span><span class="sxs-lookup"><span data-stu-id="e260a-565">...</span></span> |<span data-ttu-id="e260a-566">...</span><span class="sxs-lookup"><span data-stu-id="e260a-566">...</span></span> |<span data-ttu-id="e260a-567">...</span><span class="sxs-lookup"><span data-stu-id="e260a-567">...</span></span> |<span data-ttu-id="e260a-568">...</span><span class="sxs-lookup"><span data-stu-id="e260a-568">...</span></span> |
| <span data-ttu-id="e260a-569">Последний экземпляр сервера приложений SAP</span><span class="sxs-lookup"><span data-stu-id="e260a-569">Last SAP Application Server instance</span></span> |<span data-ttu-id="e260a-570">pr1-di-5</span><span class="sxs-lookup"><span data-stu-id="e260a-570">pr1-di-5</span></span> |<span data-ttu-id="e260a-571">pr1-nic-di-5</span><span class="sxs-lookup"><span data-stu-id="e260a-571">pr1-nic-di-5</span></span> |<span data-ttu-id="e260a-572">10.0.0.55</span><span class="sxs-lookup"><span data-stu-id="e260a-572">10.0.0.55</span></span> |
| <span data-ttu-id="e260a-573">1-й узел кластера для экземпляра ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e260a-573">First cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="e260a-574">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="e260a-574">pr1-ascs-0</span></span> |<span data-ttu-id="e260a-575">pr1-nic-ascs-0</span><span class="sxs-lookup"><span data-stu-id="e260a-575">pr1-nic-ascs-0</span></span> |<span data-ttu-id="e260a-576">10.0.0.40</span><span class="sxs-lookup"><span data-stu-id="e260a-576">10.0.0.40</span></span> |
| <span data-ttu-id="e260a-577">2-й узел кластера для экземпляра ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e260a-577">Second cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="e260a-578">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="e260a-578">pr1-ascs-1</span></span> |<span data-ttu-id="e260a-579">pr1-nic-ascs-1</span><span class="sxs-lookup"><span data-stu-id="e260a-579">pr1-nic-ascs-1</span></span> |<span data-ttu-id="e260a-580">10.0.0.41</span><span class="sxs-lookup"><span data-stu-id="e260a-580">10.0.0.41</span></span> |
| <span data-ttu-id="e260a-581">1-й узел кластера для экземпляра СУБД</span><span class="sxs-lookup"><span data-stu-id="e260a-581">First cluster node for DBMS instance</span></span> |<span data-ttu-id="e260a-582">pr1-db-0</span><span class="sxs-lookup"><span data-stu-id="e260a-582">pr1-db-0</span></span> |<span data-ttu-id="e260a-583">pr1-nic-db-0</span><span class="sxs-lookup"><span data-stu-id="e260a-583">pr1-nic-db-0</span></span> |<span data-ttu-id="e260a-584">10.0.0.30</span><span class="sxs-lookup"><span data-stu-id="e260a-584">10.0.0.30</span></span> |
| <span data-ttu-id="e260a-585">2-й узел кластера для экземпляра СУБД</span><span class="sxs-lookup"><span data-stu-id="e260a-585">Second cluster node for DBMS instance</span></span> |<span data-ttu-id="e260a-586">pr1-db-1</span><span class="sxs-lookup"><span data-stu-id="e260a-586">pr1-db-1</span></span> |<span data-ttu-id="e260a-587">pr1-nic-db-1</span><span class="sxs-lookup"><span data-stu-id="e260a-587">pr1-nic-db-1</span></span> |<span data-ttu-id="e260a-588">10.0.0.31</span><span class="sxs-lookup"><span data-stu-id="e260a-588">10.0.0.31</span></span> |

### <span data-ttu-id="e260a-589"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Задать статический IP-адрес для hello Azure внутренняя Подсистема балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="e260a-589"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Set a static IP address for hello Azure internal load balancer</span></span>

<span data-ttu-id="e260a-590">шаблон диспетчера ресурсов Azure для SAP Hello создает Azure внутренний балансировщик нагрузки, используемый в кластере экземпляра SAP ASCS/SCS hello и кластеризации СУБД hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-590">hello SAP Azure Resource Manager template creates an Azure internal load balancer that is used for hello SAP ASCS/SCS instance cluster and hello DBMS cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e260a-591">Hello именем виртуального узла hello hello SAP ASCS/SCS — это IP-адрес hello же, как IP-адрес hello hello SAP ASCS/SCS внутренней подсистемы балансировки нагрузки: **pr1 балансировки нагрузки ascs**.</span><span class="sxs-lookup"><span data-stu-id="e260a-591">hello IP address of hello virtual host name of hello SAP ASCS/SCS is hello same as hello IP address of hello SAP ASCS/SCS internal load balancer: **pr1-lb-ascs**.</span></span>
> <span data-ttu-id="e260a-592">Hello IP-адрес hello виртуальное имя СУБД — hello hello же, как IP-адрес hello hello СУБД внутренней подсистемы балансировки нагрузки: **pr1 балансировки нагрузки СУБД**.</span><span class="sxs-lookup"><span data-stu-id="e260a-592">hello IP address of hello virtual name of hello DBMS is hello same as hello IP address of hello DBMS internal load balancer: **pr1-lb-dbms**.</span></span>
>
>

<span data-ttu-id="e260a-593">tooset статический IP-адрес для hello Azure внутренняя Подсистема балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="e260a-593">tooset a static IP address for hello Azure internal load balancer:</span></span>

1.  <span data-ttu-id="e260a-594">Hello первоначального развертывания задает hello внутренний адрес подсистемы балансировки нагрузки IP слишком**динамическое**.</span><span class="sxs-lookup"><span data-stu-id="e260a-594">hello initial deployment sets hello internal load balancer IP address too**Dynamic**.</span></span> <span data-ttu-id="e260a-595">В hello в hello портала Azure **IP-адреса** колонки в разделе **назначения**выберите **статических**.</span><span class="sxs-lookup"><span data-stu-id="e260a-595">In hello Azure portal, on hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span>
2.  <span data-ttu-id="e260a-596">Задать IP-адрес hello hello внутренней подсистемы балансировки нагрузки **pr1 балансировки нагрузки ascs** toohello IP-адрес hello виртуальное имя узла экземпляра SAP ASCS/SCS hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-596">Set hello IP address of hello internal load balancer **pr1-lb-ascs** toohello IP address of hello virtual host name of hello SAP ASCS/SCS instance.</span></span>
3.  <span data-ttu-id="e260a-597">Задать IP-адрес hello hello внутренней подсистемы балансировки нагрузки **pr1 балансировки нагрузки СУБД** toohello IP-адрес hello виртуальное имя узла экземпляра СУБД hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-597">Set hello IP address of hello internal load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

  ![Рис. 14: Набор статических IP-адресов для hello внутренней подсистемы балансировки нагрузки для экземпляра SAP ASCS/SCS hello][sap-ha-guide-figure-3003]

  <span data-ttu-id="e260a-599">_**Рис. 14:** набор статических IP-адресов для hello внутренней подсистемы балансировки нагрузки для экземпляра SAP ASCS/SCS hello_</span><span class="sxs-lookup"><span data-stu-id="e260a-599">_**Figure 14:** Set static IP addresses for hello internal load balancer for hello SAP ASCS/SCS instance_</span></span>

<span data-ttu-id="e260a-600">В нашем примере есть два внутренних балансировщика нагрузки Azure со следующими статическими IP-адресами.</span><span class="sxs-lookup"><span data-stu-id="e260a-600">In our example, we have two Azure internal load balancers that have these static IP addresses:</span></span>

| <span data-ttu-id="e260a-601">Роль внутреннего балансировщика нагрузки Azure</span><span class="sxs-lookup"><span data-stu-id="e260a-601">Azure internal load balancer role</span></span> | <span data-ttu-id="e260a-602">Имя внутреннего балансировщика нагрузки Azure</span><span class="sxs-lookup"><span data-stu-id="e260a-602">Azure internal load balancer name</span></span> | <span data-ttu-id="e260a-603">Статический IP-адрес</span><span class="sxs-lookup"><span data-stu-id="e260a-603">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e260a-604">Внутренний балансировщик нагрузки экземпляра SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e260a-604">SAP ASCS/SCS instance internal load balancer</span></span> |<span data-ttu-id="e260a-605">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="e260a-605">pr1-lb-ascs</span></span> |<span data-ttu-id="e260a-606">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="e260a-606">10.0.0.43</span></span> |
| <span data-ttu-id="e260a-607">Внутренний балансировщик нагрузки экземпляра СУБД SAP</span><span class="sxs-lookup"><span data-stu-id="e260a-607">SAP DBMS internal load balancer</span></span> |<span data-ttu-id="e260a-608">pr1-lb-dbms</span><span class="sxs-lookup"><span data-stu-id="e260a-608">pr1-lb-dbms</span></span> |<span data-ttu-id="e260a-609">10.0.0.33</span><span class="sxs-lookup"><span data-stu-id="e260a-609">10.0.0.33</span></span> |


### <span data-ttu-id="e260a-610"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>По умолчанию правила для hello Azure внутренней подсистемы балансировки нагрузки подсистемы балансировки нагрузки ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e260a-610"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Default ASCS/SCS load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="e260a-611">шаблон диспетчера ресурсов Azure для SAP Hello создает hello портов:</span><span class="sxs-lookup"><span data-stu-id="e260a-611">hello SAP Azure Resource Manager template creates hello ports you need:</span></span>
* <span data-ttu-id="e260a-612">Экземпляр ABAP ASCS с номером экземпляра по умолчанию hello **00**</span><span class="sxs-lookup"><span data-stu-id="e260a-612">An ABAP ASCS instance, with hello default instance number **00**</span></span>
* <span data-ttu-id="e260a-613">Экземпляр Java SCS с номера экземпляра по умолчанию hello **01**</span><span class="sxs-lookup"><span data-stu-id="e260a-613">A Java SCS instance, with hello default instance number **01**</span></span>

<span data-ttu-id="e260a-614">При установке экземпляра SAP ASCS/SCS, необходимо использовать номер экземпляра по умолчанию hello **00** для вашей ABAP ASCS экземпляра и hello по умолчанию номер экземпляра **01** для конкретного экземпляра Java SCS.</span><span class="sxs-lookup"><span data-stu-id="e260a-614">When you install your SAP ASCS/SCS instance, you must use hello default instance number **00** for your ABAP ASCS instance and hello default instance number **01** for your Java SCS instance.</span></span>

<span data-ttu-id="e260a-615">Создайте необходимые внутренней конечных точек для портов SAP NetWeaver hello балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e260a-615">Next, create required internal load balancing endpoints for hello SAP NetWeaver ports.</span></span>

<span data-ttu-id="e260a-616">Обязательные toocreate балансировки нагрузки внутренних конечных точек, сначала создайте эти балансировки конечных точек для hello SAP NetWeaver ABAP ASCS порты:</span><span class="sxs-lookup"><span data-stu-id="e260a-616">toocreate required internal load balancing endpoints, first, create these load balancing endpoints for hello SAP NetWeaver ABAP ASCS ports:</span></span>

| <span data-ttu-id="e260a-617">Служба, имя правила балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="e260a-617">Service/load balancing rule name</span></span> | <span data-ttu-id="e260a-618">Номера портов по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e260a-618">Default port numbers</span></span> | <span data-ttu-id="e260a-619">Определенные порты для (экземпляра ASCS с номером экземпляра 00) (ERS с номером 10)</span><span class="sxs-lookup"><span data-stu-id="e260a-619">Concrete ports for (ASCS instance with instance number 00) (ERS with 10)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e260a-620">Сервер постановки в очередь, *lbrule3200*</span><span class="sxs-lookup"><span data-stu-id="e260a-620">Enqueue Server / *lbrule3200*</span></span> |<span data-ttu-id="e260a-621">32<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="e260a-621">32<*InstanceNumber*></span></span> |<span data-ttu-id="e260a-622">3200</span><span class="sxs-lookup"><span data-stu-id="e260a-622">3200</span></span> |
| <span data-ttu-id="e260a-623">Сервер сообщений ABAP, *lbrule3600*</span><span class="sxs-lookup"><span data-stu-id="e260a-623">ABAP Message Server / *lbrule3600*</span></span> |<span data-ttu-id="e260a-624">36<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="e260a-624">36<*InstanceNumber*></span></span> |<span data-ttu-id="e260a-625">3600</span><span class="sxs-lookup"><span data-stu-id="e260a-625">3600</span></span> |
| <span data-ttu-id="e260a-626">Внутренняя служба сообщений ABAP, *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="e260a-626">Internal ABAP Message / *lbrule3900*</span></span> |<span data-ttu-id="e260a-627">39<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="e260a-627">39<*InstanceNumber*></span></span> |<span data-ttu-id="e260a-628">3900</span><span class="sxs-lookup"><span data-stu-id="e260a-628">3900</span></span> |
| <span data-ttu-id="e260a-629">Сервер сообщений (HTTP), *Lbrule8100*</span><span class="sxs-lookup"><span data-stu-id="e260a-629">Message Server HTTP / *Lbrule8100*</span></span> |<span data-ttu-id="e260a-630">81<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="e260a-630">81<*InstanceNumber*></span></span> |<span data-ttu-id="e260a-631">8100</span><span class="sxs-lookup"><span data-stu-id="e260a-631">8100</span></span> |
| <span data-ttu-id="e260a-632">Служба запуска SAP ASCS (HTTP), *Lbrule50013*</span><span class="sxs-lookup"><span data-stu-id="e260a-632">SAP Start Service ASCS HTTP / *Lbrule50013*</span></span> |<span data-ttu-id="e260a-633">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="e260a-633">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="e260a-634">50013</span><span class="sxs-lookup"><span data-stu-id="e260a-634">50013</span></span> |
| <span data-ttu-id="e260a-635">Служба запуска SAP ASCS (HTTPS), *Lbrule50014*</span><span class="sxs-lookup"><span data-stu-id="e260a-635">SAP Start Service ASCS HTTPS / *Lbrule50014*</span></span> |<span data-ttu-id="e260a-636">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="e260a-636">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="e260a-637">50014</span><span class="sxs-lookup"><span data-stu-id="e260a-637">50014</span></span> |
| <span data-ttu-id="e260a-638">Служба постановки в очередь для репликации, *Lbrule50016*</span><span class="sxs-lookup"><span data-stu-id="e260a-638">Enqueue Replication / *Lbrule50016*</span></span> |<span data-ttu-id="e260a-639">5<*InstanceNumber*>16</span><span class="sxs-lookup"><span data-stu-id="e260a-639">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="e260a-640">50016</span><span class="sxs-lookup"><span data-stu-id="e260a-640">50016</span></span> |
| <span data-ttu-id="e260a-641">Служба запуска SAP ERS (HTTP), *Lbrule51013*</span><span class="sxs-lookup"><span data-stu-id="e260a-641">SAP Start Service ERS HTTP *Lbrule51013*</span></span> |<span data-ttu-id="e260a-642">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="e260a-642">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="e260a-643">51013</span><span class="sxs-lookup"><span data-stu-id="e260a-643">51013</span></span> |
| <span data-ttu-id="e260a-644">Служба запуска SAP ERS (HTTPS), *Lbrule51014*</span><span class="sxs-lookup"><span data-stu-id="e260a-644">SAP Start Service ERS HTTP *Lbrule51014*</span></span> |<span data-ttu-id="e260a-645">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="e260a-645">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="e260a-646">51014</span><span class="sxs-lookup"><span data-stu-id="e260a-646">51014</span></span> |
| <span data-ttu-id="e260a-647">Win RM, *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="e260a-647">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="e260a-648">5985</span><span class="sxs-lookup"><span data-stu-id="e260a-648">5985</span></span> |
| <span data-ttu-id="e260a-649">Общий доступ к файлам, *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="e260a-649">File Share *Lbrule445*</span></span> | |<span data-ttu-id="e260a-650">445</span><span class="sxs-lookup"><span data-stu-id="e260a-650">445</span></span> |

<span data-ttu-id="e260a-651">_**Таблица 1:** номера экземпляров SAP NetWeaver ABAP ASCS hello портов_</span><span class="sxs-lookup"><span data-stu-id="e260a-651">_**Table 1:** Port numbers of hello SAP NetWeaver ABAP ASCS instances_</span></span>

<span data-ttu-id="e260a-652">Затем создайте эти балансировки конечных точек для hello SAP NetWeaver Java SCS порты:</span><span class="sxs-lookup"><span data-stu-id="e260a-652">Then, create these load balancing endpoints for hello SAP NetWeaver Java SCS ports:</span></span>

| <span data-ttu-id="e260a-653">Служба, имя правила балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="e260a-653">Service/load balancing rule name</span></span> | <span data-ttu-id="e260a-654">Номера портов по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e260a-654">Default port numbers</span></span> | <span data-ttu-id="e260a-655">Определенные порты для (экземпляра SCS с номером экземпляра 01) (ERS с номером 11)</span><span class="sxs-lookup"><span data-stu-id="e260a-655">Concrete ports for (SCS instance with instance number 01) (ERS with 11)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e260a-656">Сервер постановки в очередь, *lbrule3201*</span><span class="sxs-lookup"><span data-stu-id="e260a-656">Enqueue Server / *lbrule3201*</span></span> |<span data-ttu-id="e260a-657">32<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="e260a-657">32<*InstanceNumber*></span></span> |<span data-ttu-id="e260a-658">3201</span><span class="sxs-lookup"><span data-stu-id="e260a-658">3201</span></span> |
| <span data-ttu-id="e260a-659">Сервер шлюза, *lbrule3301*</span><span class="sxs-lookup"><span data-stu-id="e260a-659">Gateway Server / *lbrule3301*</span></span> |<span data-ttu-id="e260a-660">33<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="e260a-660">33<*InstanceNumber*></span></span> |<span data-ttu-id="e260a-661">3301</span><span class="sxs-lookup"><span data-stu-id="e260a-661">3301</span></span> |
| <span data-ttu-id="e260a-662">Сервер сообщений Java, *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="e260a-662">Java Message Server / *lbrule3900*</span></span> |<span data-ttu-id="e260a-663">39<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="e260a-663">39<*InstanceNumber*></span></span> |<span data-ttu-id="e260a-664">3901</span><span class="sxs-lookup"><span data-stu-id="e260a-664">3901</span></span> |
| <span data-ttu-id="e260a-665">Сервер сообщений (HTTP), *Lbrule8101*</span><span class="sxs-lookup"><span data-stu-id="e260a-665">Message Server HTTP / *Lbrule8101*</span></span> |<span data-ttu-id="e260a-666">81<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="e260a-666">81<*InstanceNumber*></span></span> |<span data-ttu-id="e260a-667">8101</span><span class="sxs-lookup"><span data-stu-id="e260a-667">8101</span></span> |
| <span data-ttu-id="e260a-668">Служба запуска SAP SCS (HTTP), *Lbrule50113*</span><span class="sxs-lookup"><span data-stu-id="e260a-668">SAP Start Service SCS HTTP / *Lbrule50113*</span></span> |<span data-ttu-id="e260a-669">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="e260a-669">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="e260a-670">50113</span><span class="sxs-lookup"><span data-stu-id="e260a-670">50113</span></span> |
| <span data-ttu-id="e260a-671">Служба запуска SAP SCS (HTTPS), *Lbrule50114*</span><span class="sxs-lookup"><span data-stu-id="e260a-671">SAP Start Service SCS HTTPS / *Lbrule50114*</span></span> |<span data-ttu-id="e260a-672">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="e260a-672">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="e260a-673">50114</span><span class="sxs-lookup"><span data-stu-id="e260a-673">50114</span></span> |
| <span data-ttu-id="e260a-674">Служба постановки в очередь для репликации, *Lbrule50116*</span><span class="sxs-lookup"><span data-stu-id="e260a-674">Enqueue Replication / *Lbrule50116*</span></span> |<span data-ttu-id="e260a-675">5<*InstanceNumber*>16</span><span class="sxs-lookup"><span data-stu-id="e260a-675">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="e260a-676">50116</span><span class="sxs-lookup"><span data-stu-id="e260a-676">50116</span></span> |
| <span data-ttu-id="e260a-677">Служба запуска SAP ERS (HTTP), *Lbrule51113*</span><span class="sxs-lookup"><span data-stu-id="e260a-677">SAP Start Service ERS HTTP *Lbrule51113*</span></span> |<span data-ttu-id="e260a-678">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="e260a-678">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="e260a-679">51113</span><span class="sxs-lookup"><span data-stu-id="e260a-679">51113</span></span> |
| <span data-ttu-id="e260a-680">Служба запуска SAP ERS (HTTPS), *Lbrule51114*</span><span class="sxs-lookup"><span data-stu-id="e260a-680">SAP Start Service ERS HTTP *Lbrule51114*</span></span> |<span data-ttu-id="e260a-681">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="e260a-681">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="e260a-682">51114</span><span class="sxs-lookup"><span data-stu-id="e260a-682">51114</span></span> |
| <span data-ttu-id="e260a-683">Win RM, *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="e260a-683">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="e260a-684">5985</span><span class="sxs-lookup"><span data-stu-id="e260a-684">5985</span></span> |
| <span data-ttu-id="e260a-685">Общий доступ к файлам, *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="e260a-685">File Share *Lbrule445*</span></span> | |<span data-ttu-id="e260a-686">445</span><span class="sxs-lookup"><span data-stu-id="e260a-686">445</span></span> |

<span data-ttu-id="e260a-687">_**Таблица 2:** номера экземпляров SAP NetWeaver Java SCS hello портов_</span><span class="sxs-lookup"><span data-stu-id="e260a-687">_**Table 2:** Port numbers of hello SAP NetWeaver Java SCS instances_</span></span>

![Рис. 15: Правила для hello Azure внутренней подсистемы балансировки нагрузки подсистемы балансировки нагрузки по умолчанию ASCS/SCS][sap-ha-guide-figure-3004]

<span data-ttu-id="e260a-689">_**Рис. 15:** правила для hello Azure внутренней подсистемы балансировки нагрузки подсистемы балансировки нагрузки по умолчанию ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="e260a-689">_**Figure 15:** Default ASCS/SCS load balancing rules for hello Azure internal load balancer_</span></span>

<span data-ttu-id="e260a-690">Задать hello IP-адрес подсистемы балансировки нагрузки hello **pr1 балансировки нагрузки СУБД** toohello IP-адрес hello виртуальное имя узла экземпляра СУБД hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-690">Set hello IP address of hello load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

### <span data-ttu-id="e260a-691"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>Изменение правил для hello Azure внутренней подсистемы балансировки нагрузки балансировки нагрузки, по умолчанию hello ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e260a-691"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="e260a-692">Следует toouse различное для hello SAP ASCS или экземпляров SCS необходимо изменить hello имена и значения их порты от значений по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e260a-692">If you want toouse different numbers for hello SAP ASCS or SCS instances, you must change hello names and values of their ports from default values.</span></span>

1.  <span data-ttu-id="e260a-693">В hello портал Azure, выберите  **<* SID*> загрузить ascs - балансировки нагрузки - балансировки ** > **правила балансировки нагрузки**.</span><span class="sxs-lookup"><span data-stu-id="e260a-693">In hello Azure portal, select **<*SID*>-lb-ascs load balancer** > **Load Balancing Rules**.</span></span>
2.  <span data-ttu-id="e260a-694">Для правил, принадлежащим toohello SAP ASCS или экземпляра SCS балансировки нагрузки, все измените эти значения.</span><span class="sxs-lookup"><span data-stu-id="e260a-694">For all load balancing rules that belong toohello SAP ASCS or SCS instance, change these values:</span></span>

  * <span data-ttu-id="e260a-695">Имя</span><span class="sxs-lookup"><span data-stu-id="e260a-695">Name</span></span>
  * <span data-ttu-id="e260a-696">Порт</span><span class="sxs-lookup"><span data-stu-id="e260a-696">Port</span></span>
  * <span data-ttu-id="e260a-697">Внутренний порт</span><span class="sxs-lookup"><span data-stu-id="e260a-697">Back-end port</span></span>

  <span data-ttu-id="e260a-698">Например если номер экземпляра ASCS по умолчанию hello toochange от 00 too31, необходимо toomake hello изменения для всех портов, указанных в таблице 1.</span><span class="sxs-lookup"><span data-stu-id="e260a-698">For example, if you want toochange hello default ASCS instance number from 00 too31, you need toomake hello changes for all ports listed in Table 1.</span></span>

  <span data-ttu-id="e260a-699">Ниже приведен пример обновления *lbrule3200*для порта.</span><span class="sxs-lookup"><span data-stu-id="e260a-699">Here's an example of an update for port *lbrule3200*.</span></span>

  ![На рисунке 16: Изменение правил для hello Azure внутренней подсистемы балансировки нагрузки балансировки нагрузки, по умолчанию hello ASCS/SCS][sap-ha-guide-figure-3005]

  <span data-ttu-id="e260a-701">_**На рисунке 16:** изменение hello ASCS/SCS по умолчанию правил балансировки нагрузки, для hello Azure внутренняя Подсистема балансировки нагрузки_</span><span class="sxs-lookup"><span data-stu-id="e260a-701">_**Figure 16:** Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer_</span></span>

### <span data-ttu-id="e260a-702"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Добавление домена toohello виртуальные машины Windows</span><span class="sxs-lookup"><span data-stu-id="e260a-702"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> Add Windows virtual machines toohello domain</span></span>

<span data-ttu-id="e260a-703">После назначения статических IP адрес toohello виртуальных машин, добавьте домен toohello hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e260a-703">After you assign a static IP address toohello virtual machines, add hello virtual machines toohello domain.</span></span>

![Рисунок 17: Добавление домена tooa виртуальной машины][sap-ha-guide-figure-3006]

<span data-ttu-id="e260a-705">_**Рисунок 17:** добавить домен tooa виртуальной машины_</span><span class="sxs-lookup"><span data-stu-id="e260a-705">_**Figure 17:** Add a virtual machine tooa domain_</span></span>

### <span data-ttu-id="e260a-706"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Добавление записей реестра на обоих узлах кластера экземпляра SAP ASCS/SCS hello</span><span class="sxs-lookup"><span data-stu-id="e260a-706"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance</span></span>

<span data-ttu-id="e260a-707">Подсистема балансировки нагрузки Azure имеет внутренний балансировщик нагрузки, закрытия подключения при бездействии hello соединений, для определенного периода времени (время ожидания простоя).</span><span class="sxs-lookup"><span data-stu-id="e260a-707">Azure Load Balancer has an internal load balancer that closes connections when hello connections are idle for a set period of time (an idle timeout).</span></span> <span data-ttu-id="e260a-708">SAP рабочие процессы в диалоговом окне экземпляров открытых соединений toohello SAP постановки в очередь обработки как можно скорее hello первый постановки в очередь и вывода из очереди запросов отправлено toobe потребностей.</span><span class="sxs-lookup"><span data-stu-id="e260a-708">SAP work processes in dialog instances open connections toohello SAP enqueue process as soon as hello first enqueue/dequeue request needs toobe sent.</span></span> <span data-ttu-id="e260a-709">Эти подключения обычно останется установленным до hello рабочего процесса или hello постановки в очередь перезапускается.</span><span class="sxs-lookup"><span data-stu-id="e260a-709">These connections usually remain established until hello work process or hello enqueue process restarts.</span></span> <span data-ttu-id="e260a-710">Тем не менее если соединение hello простоя в течение времени, hello нагрузки Azure внутренней балансировки закрывает hello подключений.</span><span class="sxs-lookup"><span data-stu-id="e260a-710">However, if hello connection is idle for a set period of time, hello Azure internal load balancer closes hello connections.</span></span> <span data-ttu-id="e260a-711">Это не проблема, поскольку hello SAP рабочего процесса восстанавливает время постановки в очередь toohello hello подключения, если он больше не существует.</span><span class="sxs-lookup"><span data-stu-id="e260a-711">This isn't a problem because hello SAP work process reestablishes hello connection toohello enqueue process if it no longer exists.</span></span> <span data-ttu-id="e260a-712">Эти действия описаны в трассировках developer Привет процессов SAP, но они создают большой объем дополнительное содержимое в таких трассировок.</span><span class="sxs-lookup"><span data-stu-id="e260a-712">These activities are documented in hello developer traces of SAP processes, but they create a large amount of extra content in those traces.</span></span> <span data-ttu-id="e260a-713">Это рекомендуется toochange hello TCP/IP `KeepAliveTime` и `KeepAliveInterval` на обоих узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="e260a-713">It's a good idea toochange hello TCP/IP `KeepAliveTime` and `KeepAliveInterval` on both cluster nodes.</span></span> <span data-ttu-id="e260a-714">Объединить эти изменения в параметры TCP/IP hello с параметрами профиля SAP, описанные в статье hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-714">Combine these changes in hello TCP/IP parameters with SAP profile parameters, described later in hello article.</span></span>

<span data-ttu-id="e260a-715">записи реестра tooadd на обоих узлах кластера экземпляра SAP ASCS/SCS hello, сначала добавьте эти записи реестра Windows на обоих узлах кластера Windows для SAP ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="e260a-715">tooadd registry entries on both cluster nodes of hello SAP ASCS/SCS instance, first, add these Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="e260a-716">Путь</span><span class="sxs-lookup"><span data-stu-id="e260a-716">Path</span></span> | <span data-ttu-id="e260a-717">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="e260a-717">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="e260a-718">Имя переменной</span><span class="sxs-lookup"><span data-stu-id="e260a-718">Variable name</span></span> |`KeepAliveTime` |
| <span data-ttu-id="e260a-719">Тип переменной</span><span class="sxs-lookup"><span data-stu-id="e260a-719">Variable type</span></span> |<span data-ttu-id="e260a-720">REG_DWORD (десятичное)</span><span class="sxs-lookup"><span data-stu-id="e260a-720">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="e260a-721">Значение</span><span class="sxs-lookup"><span data-stu-id="e260a-721">Value</span></span> |<span data-ttu-id="e260a-722">120000</span><span class="sxs-lookup"><span data-stu-id="e260a-722">120000</span></span> |
| <span data-ttu-id="e260a-723">Toodocumentation связи</span><span class="sxs-lookup"><span data-stu-id="e260a-723">Link toodocumentation</span></span> |[<span data-ttu-id="e260a-724">https://technet.microsoft.com/en-us/library/cc957549.aspx</span><span class="sxs-lookup"><span data-stu-id="e260a-724">https://technet.microsoft.com/en-us/library/cc957549.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

<span data-ttu-id="e260a-725">_**Таблица 3.** изменение hello первый параметр TCP/IP_</span><span class="sxs-lookup"><span data-stu-id="e260a-725">_**Table 3:** Change hello first TCP/IP parameter_</span></span>

<span data-ttu-id="e260a-726">Затем добавьте следующие записи реестра Windows на обоих узлах кластера Windows для SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="e260a-726">Then, add this Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="e260a-727">Путь</span><span class="sxs-lookup"><span data-stu-id="e260a-727">Path</span></span> | <span data-ttu-id="e260a-728">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="e260a-728">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="e260a-729">Имя переменной</span><span class="sxs-lookup"><span data-stu-id="e260a-729">Variable name</span></span> |`KeepAliveInterval` |
| <span data-ttu-id="e260a-730">Тип переменной</span><span class="sxs-lookup"><span data-stu-id="e260a-730">Variable type</span></span> |<span data-ttu-id="e260a-731">REG_DWORD (десятичное)</span><span class="sxs-lookup"><span data-stu-id="e260a-731">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="e260a-732">Значение</span><span class="sxs-lookup"><span data-stu-id="e260a-732">Value</span></span> |<span data-ttu-id="e260a-733">120000</span><span class="sxs-lookup"><span data-stu-id="e260a-733">120000</span></span> |
| <span data-ttu-id="e260a-734">Toodocumentation связи</span><span class="sxs-lookup"><span data-stu-id="e260a-734">Link toodocumentation</span></span> |[<span data-ttu-id="e260a-735">https://technet.microsoft.com/en-us/library/cc957548.aspx</span><span class="sxs-lookup"><span data-stu-id="e260a-735">https://technet.microsoft.com/en-us/library/cc957548.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

<span data-ttu-id="e260a-736">_**Таблица 4.** изменение hello второй параметр TCP/IP_</span><span class="sxs-lookup"><span data-stu-id="e260a-736">_**Table 4:** Change hello second TCP/IP parameter_</span></span>

<span data-ttu-id="e260a-737">**tooapply hello изменения, перезапустите обоих узлов кластера**.</span><span class="sxs-lookup"><span data-stu-id="e260a-737">**tooapply hello changes, restart both cluster nodes**.</span></span>

### <span data-ttu-id="e260a-738"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Установка отказоустойчивого кластера Windows Server для экземпляра SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e260a-738"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Set up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance</span></span>

<span data-ttu-id="e260a-739">Настройка отказоустойчивого кластера Windows Server для экземпляра SAP ASCS/SCS состоит из следующих заданий:</span><span class="sxs-lookup"><span data-stu-id="e260a-739">Setting up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="e260a-740">Сбор данных об узлах кластера hello в конфигурации кластера</span><span class="sxs-lookup"><span data-stu-id="e260a-740">Collecting hello cluster nodes in a cluster configuration</span></span>
- <span data-ttu-id="e260a-741">настройка файлового ресурса-свидетеля кластера.</span><span class="sxs-lookup"><span data-stu-id="e260a-741">Configuring a cluster file share witness</span></span>

#### <span data-ttu-id="e260a-742"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>Собирать hello узлы кластера в конфигурации кластера</span><span class="sxs-lookup"><span data-stu-id="e260a-742"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> Collect hello cluster nodes in a cluster configuration</span></span>

1.  <span data-ttu-id="e260a-743">В мастере компонентов и добавить роль hello добавьте функцию отказоустойчивой кластеризации tooboth узлов кластера.</span><span class="sxs-lookup"><span data-stu-id="e260a-743">In hello Add Role and Features Wizard, add failover clustering tooboth cluster nodes.</span></span>
2.  <span data-ttu-id="e260a-744">Установка hello отказоустойчивого кластера с помощью диспетчера отказоустойчивости кластеров.</span><span class="sxs-lookup"><span data-stu-id="e260a-744">Set up hello failover cluster by using Failover Cluster Manager.</span></span> <span data-ttu-id="e260a-745">В диспетчере отказоустойчивости кластеров выберите **создания кластеров**, а затем добавьте только hello имя hello первый кластер, узел а. Не добавляйте hello второго узла еще; мы добавим второй узел hello позже.</span><span class="sxs-lookup"><span data-stu-id="e260a-745">In Failover Cluster Manager, select **Create Cluster**, and then add only hello name of hello first cluster, node A. Do not add hello second node yet; you'll add hello second node in a later step.</span></span>

  ![На рисунке 18: Добавление сервера hello или имя виртуальной машины hello первого узла кластера][sap-ha-guide-figure-3007]

  <span data-ttu-id="e260a-747">_**На рисунке 18:** добавить hello имя сервера или виртуальной машины hello первого узла кластера_</span><span class="sxs-lookup"><span data-stu-id="e260a-747">_**Figure 18:** Add hello server or virtual machine name of hello first cluster node_</span></span>

3.  <span data-ttu-id="e260a-748">Введите имя сети hello (имя виртуального узла) hello кластера.</span><span class="sxs-lookup"><span data-stu-id="e260a-748">Enter hello network name (virtual host name) of hello cluster.</span></span>

  ![На рисунке 19: Введите имя кластера hello][sap-ha-guide-figure-3008]

  <span data-ttu-id="e260a-750">_**На рисунке 19:** введите имя кластера hello_</span><span class="sxs-lookup"><span data-stu-id="e260a-750">_**Figure 19:** Enter hello cluster name_</span></span>

4.  <span data-ttu-id="e260a-751">После создания кластера hello, запустите тест проверки кластера.</span><span class="sxs-lookup"><span data-stu-id="e260a-751">After you've created hello cluster, run a cluster validation test.</span></span>

  ![Рис. 20: Проверка hello кластера][sap-ha-guide-figure-3009]

  <span data-ttu-id="e260a-753">_**Рис. 20:** проверка кластера hello_</span><span class="sxs-lookup"><span data-stu-id="e260a-753">_**Figure 20:** Run hello cluster validation check_</span></span>

  <span data-ttu-id="e260a-754">Можно игнорировать любые предупреждения о дисках, на этом этапе в процессе hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-754">You can ignore any warnings about disks at this point in hello process.</span></span> <span data-ttu-id="e260a-755">Вам предстоит добавить файловый ресурс-свидетель и hello SIOS общих дисков позже.</span><span class="sxs-lookup"><span data-stu-id="e260a-755">You'll add a file share witness and hello SIOS shared disks later.</span></span> <span data-ttu-id="e260a-756">На этой стадии не требуется tooworry о кворум.</span><span class="sxs-lookup"><span data-stu-id="e260a-756">At this stage, you don't need tooworry about having a quorum.</span></span>

  ![Рис. 21. Предупреждение об отсутствии диска кворума][sap-ha-guide-figure-3010]

  <span data-ttu-id="e260a-758">_**Рис. 21.** Предупреждение об отсутствии диска кворума_</span><span class="sxs-lookup"><span data-stu-id="e260a-758">_**Figure 21:** No quorum disk is found_</span></span>

  ![Рис. 22. Определение основного ресурса кластера с IP-адресом (требуется новый IP-адрес)][sap-ha-guide-figure-3011]

  <span data-ttu-id="e260a-760">_**Рис. 22.** Определение основного ресурса кластера с IP-адресом (требуется новый IP-адрес)_</span><span class="sxs-lookup"><span data-stu-id="e260a-760">_**Figure 22:** Core cluster resource needs a new IP address_</span></span>

5.  <span data-ttu-id="e260a-761">Изменение IP-адреса hello службы кластеров core hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-761">Change hello IP address of hello core cluster service.</span></span> <span data-ttu-id="e260a-762">Hello кластера не удается запустить пока не изменить IP-адрес hello hello основная служба кластера, поскольку hello IP-адрес сервера hello указывает tooone hello узлов виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e260a-762">hello cluster can't start until you change hello IP address of hello core cluster service, because hello IP address of hello server points tooone of hello virtual machine nodes.</span></span> <span data-ttu-id="e260a-763">Это можно сделать на hello **свойства** страница hello ядра кластера службы IP-ресурс.</span><span class="sxs-lookup"><span data-stu-id="e260a-763">Do this on hello **Properties** page of hello core cluster service's IP resource.</span></span>

  <span data-ttu-id="e260a-764">Например, нам нужно tooassign IP-адрес (в нашем примере **10.0.0.42**) для имени виртуального узла кластера hello **pr1 ascs-vir**.</span><span class="sxs-lookup"><span data-stu-id="e260a-764">For example, we need tooassign an IP address (in our example, **10.0.0.42**) for hello cluster virtual host name **pr1-ascs-vir**.</span></span>

  ![На рисунке 23: В диалоговом окне Свойства hello, изменение hello IP-адреса][sap-ha-guide-figure-3012]

  <span data-ttu-id="e260a-766">_**На рисунке 23:** в hello **свойства** диалоговое окно, изменения hello IP-адреса_</span><span class="sxs-lookup"><span data-stu-id="e260a-766">_**Figure 23:** In hello **Properties** dialog box, change hello IP address_</span></span>

  ![Рис. 24: Назначить hello IP-адрес, который зарезервирован для кластера hello][sap-ha-guide-figure-3013]

  <span data-ttu-id="e260a-768">_**Рис. 24:** назначения hello IP-адреса, зарезервированные для кластера hello_</span><span class="sxs-lookup"><span data-stu-id="e260a-768">_**Figure 24:** Assign hello IP address that is reserved for hello cluster_</span></span>

6.  <span data-ttu-id="e260a-769">Перевести имя виртуального узла кластера hello через Интернет.</span><span class="sxs-lookup"><span data-stu-id="e260a-769">Bring hello cluster virtual host name online.</span></span>

  ![Рис. 25: Основная служба кластера запущен и работает, а также hello исправьте IP-адрес][sap-ha-guide-figure-3014]

  <span data-ttu-id="e260a-771">_**Рис. 25:** основная служба кластеров работает и запущен и с hello исправьте IP-адрес_</span><span class="sxs-lookup"><span data-stu-id="e260a-771">_**Figure 25:** Cluster core service is up and running, and with hello correct IP address_</span></span>

7.  <span data-ttu-id="e260a-772">Добавьте второй узел кластера hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-772">Add hello second cluster node.</span></span>

  <span data-ttu-id="e260a-773">Теперь, когда hello основная служба кластеров запущена, можно добавить второй узел кластера hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-773">Now that hello core cluster service is up and running, you can add hello second cluster node.</span></span>

  ![Рис. 26: Добавление второго узла кластера hello][sap-ha-guide-figure-3015]

  <span data-ttu-id="e260a-775">_**Рис. 26:** добавить hello второго узла кластера_</span><span class="sxs-lookup"><span data-stu-id="e260a-775">_**Figure 26:** Add hello second cluster node_</span></span>

8.  <span data-ttu-id="e260a-776">Введите имя для hello второй узел узла кластера.</span><span class="sxs-lookup"><span data-stu-id="e260a-776">Enter a name for hello second cluster node host.</span></span>

  ![Рис. 27: Введите hello второе имя узла кластера узлов][sap-ha-guide-figure-3016]

  <span data-ttu-id="e260a-778">_**Рис. 27:** ввод hello второе имя узла кластера узлов_</span><span class="sxs-lookup"><span data-stu-id="e260a-778">_**Figure 27:** Enter hello second cluster node host name_</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="e260a-779">Убедитесь, что hello **Добавление всех допустимых хранилищ toohello кластера** флажок **не** выбранных.</span><span class="sxs-lookup"><span data-stu-id="e260a-779">Be sure that hello **Add all eligible storage toohello cluster** check box is **NOT** selected.</span></span>  
  >
  >

  ![Рис. 28: Не устанавливайте флажок hello][sap-ha-guide-figure-3017]

  <span data-ttu-id="e260a-781">_**Рис. 28:** сделать **не** Здравствуйте, установите флажок_</span><span class="sxs-lookup"><span data-stu-id="e260a-781">_**Figure 28:** Do **not** select hello check box_</span></span>

  <span data-ttu-id="e260a-782">Предупреждения о кворуме и дисках можно игнорировать.</span><span class="sxs-lookup"><span data-stu-id="e260a-782">You can ignore warnings about quorum and disks.</span></span> <span data-ttu-id="e260a-783">Диск hello hello кворума и общая папка будет установить позже, как описано в [установки SIOS DataKeeper Cluster Edition для диска общего ресурса кластера SAP ASCS/SCS][sap-ha-guide-8.12.3].</span><span class="sxs-lookup"><span data-stu-id="e260a-783">You'll set hello quorum and share hello disk later, as described in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3].</span></span>

  ![Рис. 29: Пропускать предупреждения о hello диска кворума][sap-ha-guide-figure-3018]

  <span data-ttu-id="e260a-785">_**Рис. 29:** пропускать предупреждения о hello диска кворума_</span><span class="sxs-lookup"><span data-stu-id="e260a-785">_**Figure 29:** Ignore warnings about hello disk quorum_</span></span>


#### <span data-ttu-id="e260a-786"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Настройка файлового ресурса-свидетеля кластера</span><span class="sxs-lookup"><span data-stu-id="e260a-786"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configure a cluster file share witness</span></span>

<span data-ttu-id="e260a-787">Настройка файлового ресурса-свидетеля кластера состоит из следующих заданий:</span><span class="sxs-lookup"><span data-stu-id="e260a-787">Configuring a cluster file share witness involves these tasks:</span></span>

- <span data-ttu-id="e260a-788">создание файлового ресурса;</span><span class="sxs-lookup"><span data-stu-id="e260a-788">Creating a file share</span></span>
- <span data-ttu-id="e260a-789">Настройка следящего сервера кворума hello общих папок в диспетчере отказоустойчивости кластеров</span><span class="sxs-lookup"><span data-stu-id="e260a-789">Setting hello file share witness quorum in Failover Cluster Manager</span></span>

##### <span data-ttu-id="e260a-790"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Создание файлового ресурса</span><span class="sxs-lookup"><span data-stu-id="e260a-790"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Create a file share</span></span>

1.  <span data-ttu-id="e260a-791">Вместо диска кворума нужно выбрать файловый ресурс-свидетель.</span><span class="sxs-lookup"><span data-stu-id="e260a-791">Select a file share witness instead of a quorum disk.</span></span> <span data-ttu-id="e260a-792">SIOS DataKeeper поддерживает такой вариант.</span><span class="sxs-lookup"><span data-stu-id="e260a-792">SIOS DataKeeper supports this option.</span></span>

  <span data-ttu-id="e260a-793">В примерах в этой статье hello hello файловый ресурс-свидетель включен hello Active Directory или DNS-сервера, на котором работает в Azure.</span><span class="sxs-lookup"><span data-stu-id="e260a-793">In hello examples in this article, hello file share witness is on hello Active Directory/DNS server that is running in Azure.</span></span> <span data-ttu-id="e260a-794">Hello файловый ресурс-свидетель называется **domcontr 0**.</span><span class="sxs-lookup"><span data-stu-id="e260a-794">hello file share witness is called **domcontr-0**.</span></span> <span data-ttu-id="e260a-795">Так как будут настроены tooAzure подключения VPN (через сеть-сеть VPN или Azure ExpressRoute), ваш DNS Active Directory и службы в локальной среде, не подходящий toorun файл ресурс-свидетель.</span><span class="sxs-lookup"><span data-stu-id="e260a-795">Because you would have configured a VPN connection tooAzure (via Site-to-Site VPN or Azure ExpressRoute), your Active Directory/DNS service is on-premises and isn't suitable toorun a file share witness.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e260a-796">Если служба DNS и Active Directory работает только в локальной среде, не настроить файловый ресурс-свидетель в операционной системе Windows Active Directory или DNS-hello, на котором выполняется локально.</span><span class="sxs-lookup"><span data-stu-id="e260a-796">If your Active Directory/DNS service runs only on-premises, don't configure your file share witness on hello Active Directory/DNS Windows operating system that is running on-premises.</span></span> <span data-ttu-id="e260a-797">Задержка сети между узлами кластера, работающими в Azure, и локальной средой служб Active Directory и DNS, может быть слишком большой и вызвать проблемы с подключением.</span><span class="sxs-lookup"><span data-stu-id="e260a-797">Network latency between cluster nodes running in Azure and Active Directory/DNS on-premises might be too large and cause connectivity issues.</span></span> <span data-ttu-id="e260a-798">Быть убедиться, что tooconfigure hello файловый ресурс-свидетель на виртуальной машине Azure, на котором выполняется закрыть toohello узла кластера.</span><span class="sxs-lookup"><span data-stu-id="e260a-798">Be sure tooconfigure hello file share witness on an Azure virtual machine that is running close toohello cluster node.</span></span>  
  >
  >

  <span data-ttu-id="e260a-799">диск кворума Hello требуется по крайней мере 1 024 МБ свободного места.</span><span class="sxs-lookup"><span data-stu-id="e260a-799">hello quorum drive needs at least 1,024 MB of free space.</span></span> <span data-ttu-id="e260a-800">Мы рекомендуем 2048 МБ свободного места для hello диска кворума.</span><span class="sxs-lookup"><span data-stu-id="e260a-800">We recommend 2,048 MB of free space for hello quorum drive.</span></span>

2.  <span data-ttu-id="e260a-801">Добавьте объект имени кластера hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-801">Add hello cluster name object.</span></span>

  ![Рис. 30: Назначить hello разрешения для общей папки hello для hello объект имени кластера][sap-ha-guide-figure-3019]

  <span data-ttu-id="e260a-803">_**Рис. 30:** назначить hello разрешения для общей папки hello для hello объект имени кластера_</span><span class="sxs-lookup"><span data-stu-id="e260a-803">_**Figure 30:** Assign hello permissions on hello share for hello cluster name object_</span></span>

  <span data-ttu-id="e260a-804">Убедитесь, что разрешения hello входит hello центра toochange данных в общую папку hello для hello объект имени кластера (в нашем примере **pr1 ascs-vir$**).</span><span class="sxs-lookup"><span data-stu-id="e260a-804">Be sure that hello permissions include hello authority toochange data in hello share for hello cluster name object (in our example, **pr1-ascs-vir$**).</span></span>

3.  <span data-ttu-id="e260a-805">tooadd hello кластера имя объекта toohello выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="e260a-805">tooadd hello cluster name object toohello list, select **Add**.</span></span> <span data-ttu-id="e260a-806">Изменить toocheck hello фильтр для объектов-компьютеров, в добавление toothose показано на рис. 31.</span><span class="sxs-lookup"><span data-stu-id="e260a-806">Change hello filter toocheck for computer objects, in addition toothose shown in Figure 31.</span></span>

  ![Рис. 31: Изменить компьютеров tooinclude hello типов объектов][sap-ha-guide-figure-3020]

  <span data-ttu-id="e260a-808">_**Рис. 31:** изменить tooinclude компьютеров hello типов объектов_</span><span class="sxs-lookup"><span data-stu-id="e260a-808">_**Figure 31:** Change hello Object Types tooinclude computers_</span></span>

  ![Рис. 32: Флажок hello компьютеров][sap-ha-guide-figure-3021]

  <span data-ttu-id="e260a-810">_**Рис. 32:** выберите hello **компьютеров** флажок_</span><span class="sxs-lookup"><span data-stu-id="e260a-810">_**Figure 32:** Select hello **Computers** check box_</span></span>

4.  <span data-ttu-id="e260a-811">Введите имя объекта hello кластера, как показано на рис. 31.</span><span class="sxs-lookup"><span data-stu-id="e260a-811">Enter hello cluster name object as shown in Figure 31.</span></span> <span data-ttu-id="e260a-812">Так как запись hello уже создана, можно изменить разрешения hello, как показано на рисунке 30.</span><span class="sxs-lookup"><span data-stu-id="e260a-812">Because hello record has already been created, you can change hello permissions, as shown in Figure 30.</span></span>

5.  <span data-ttu-id="e260a-813">Выберите hello **безопасности** вкладке hello общей папки, а затем задайте более подробные разрешения для hello объект имени кластера.</span><span class="sxs-lookup"><span data-stu-id="e260a-813">Select hello **Security** tab of hello share, and then set more detailed permissions for hello cluster name object.</span></span>

  ![На рисунке 33: Установить атрибуты безопасности hello для hello объект имени кластера для кворума hello общих папок][sap-ha-guide-figure-3022]

  <span data-ttu-id="e260a-815">_**На рисунке 33:** установить атрибуты безопасности hello для hello объект имени кластера для кворума hello общих папок_</span><span class="sxs-lookup"><span data-stu-id="e260a-815">_**Figure 33:** Set hello security attributes for hello cluster name object on hello file share quorum_</span></span>

##### <span data-ttu-id="e260a-816"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>Задайте следящий сервер кворума hello общих папок в диспетчере отказоустойчивости кластеров</span><span class="sxs-lookup"><span data-stu-id="e260a-816"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> Set hello file share witness quorum in Failover Cluster Manager</span></span>

1.  <span data-ttu-id="e260a-817">Откройте hello параметр мастера настройки кворума.</span><span class="sxs-lookup"><span data-stu-id="e260a-817">Open hello Configure Quorum Setting Wizard.</span></span>

  ![Рисунок 34: Запустите мастер настройки кворума кластера Настройка hello][sap-ha-guide-figure-3023]

  <span data-ttu-id="e260a-819">_**Рисунок 34:** начала hello параметр мастером настройки кворума кластера_</span><span class="sxs-lookup"><span data-stu-id="e260a-819">_**Figure 34:** Start hello Configure Cluster Quorum Setting Wizard_</span></span>

2.  <span data-ttu-id="e260a-820">На hello **Выбор конфигурации кворума** выберите **Выбор свидетеля кворума hello**.</span><span class="sxs-lookup"><span data-stu-id="e260a-820">On hello **Select Quorum Configuration** page, select **Select hello quorum witness**.</span></span>

  ![Рис. 35. Экран выбора различных конфигураций кворума][sap-ha-guide-figure-3024]

  <span data-ttu-id="e260a-822">_**Рис. 35.** Экран выбора различных конфигураций кворума_</span><span class="sxs-lookup"><span data-stu-id="e260a-822">_**Figure 35:** Quorum configurations you can choose from_</span></span>

3.  <span data-ttu-id="e260a-823">На hello **Выбор свидетеля кворума** выберите **настроить файловый ресурс-свидетель**.</span><span class="sxs-lookup"><span data-stu-id="e260a-823">On hello **Select Quorum Witness** page, select **Configure a file share witness**.</span></span>

  ![Рисунок 36: Hello выберите файловый ресурс-свидетель][sap-ha-guide-figure-3025]

  <span data-ttu-id="e260a-825">_**Рисунок 36:** выберите hello файловый ресурс-свидетель_</span><span class="sxs-lookup"><span data-stu-id="e260a-825">_**Figure 36:** Select hello file share witness_</span></span>

4.  <span data-ttu-id="e260a-826">Введите hello UNC путь toohello общей папки (в нашем примере \\domcontr 0\FSW).</span><span class="sxs-lookup"><span data-stu-id="e260a-826">Enter hello UNC path toohello file share (in our example, \\domcontr-0\FSW).</span></span> <span data-ttu-id="e260a-827">Список изменений hello, можно делать, выберите toosee **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e260a-827">toosee a list of hello changes you can make, select **Next**.</span></span>

  ![На рисунке 37: Определение общей папки hello в общей папке следящего сервера hello][sap-ha-guide-figure-3026]

  <span data-ttu-id="e260a-829">_**На рисунке 37:** определения общей папки hello в общей папке следящего сервера hello_</span><span class="sxs-lookup"><span data-stu-id="e260a-829">_**Figure 37:** Define hello file share location for hello witness share_</span></span>

5.  <span data-ttu-id="e260a-830">Выберите изменения hello и установите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e260a-830">Select hello changes you want, and then select **Next**.</span></span> <span data-ttu-id="e260a-831">Требуется toosuccessfully перенастроить hello конфигурации кластера, как показано на рисунке 38.</span><span class="sxs-lookup"><span data-stu-id="e260a-831">You need toosuccessfully reconfigure hello cluster configuration as shown in Figure 38.</span></span>  

  ![Рисунок 38: Подтверждение повторно настроить кластер hello][sap-ha-guide-figure-3027]

  <span data-ttu-id="e260a-833">_**На рисунке 38:** подтверждение повторно настроить кластер hello_</span><span class="sxs-lookup"><span data-stu-id="e260a-833">_**Figure 38:** Confirmation that you've reconfigured hello cluster_</span></span>

<span data-ttu-id="e260a-834">Отказоустойчивый кластер Windows hello после успешного завершения установки, изменения должны toobe внесенные toosome пороговые значения tooadapt отработки отказа обнаружения tooconditions в Azure.</span><span class="sxs-lookup"><span data-stu-id="e260a-834">After installing hello Windows Failover Cluster successfully, changes need toobe made toosome thresholds tooadapt failover detection tooconditions in Azure.</span></span> <span data-ttu-id="e260a-835">Hello toobe параметры изменения описаны в этом блоге: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/.</span><span class="sxs-lookup"><span data-stu-id="e260a-835">hello parameters toobe changed are documented in this blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span></span> <span data-ttu-id="e260a-836">При условии, что две виртуальные машины сборки hello конфигурации кластера Windows для ASCS/SCS находятся в Здравствуйте одной подсети, hello следующие параметры должны изменить toobe toothese значения:</span><span class="sxs-lookup"><span data-stu-id="e260a-836">Assuming that your two VMs that build hello Windows Cluster Configuration for ASCS/SCS are in hello same SubNet, hello following parameters need toobe changed toothese values:</span></span>
- <span data-ttu-id="e260a-837">SameSubNetDelay = 2</span><span class="sxs-lookup"><span data-stu-id="e260a-837">SameSubNetDelay = 2</span></span>
- <span data-ttu-id="e260a-838">SameSubNetThreshold = 15</span><span class="sxs-lookup"><span data-stu-id="e260a-838">SameSubNetThreshold = 15</span></span>

<span data-ttu-id="e260a-839">Эти параметры, протестированных с клиентами и предоставляемые toobe объединять, достаточно гибкой на одной стороне hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-839">These settings were tested with customers and provided a good compromise toobe resilient enough on hello one side.</span></span> <span data-ttu-id="e260a-840">На hello другой стороны эти параметры предоставление быстрого достаточно отработки отказа в реальной ошибки при сбое программного обеспечения или узел или ВМ SAP.</span><span class="sxs-lookup"><span data-stu-id="e260a-840">On hello other hand those settings were providing fast enough failover in real error conditions on SAP software or node/VM failure.</span></span> 

### <span data-ttu-id="e260a-841"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>Установить для диска общего ресурса кластера SAP ASCS/SCS hello SIOS DataKeeper Cluster Edition</span><span class="sxs-lookup"><span data-stu-id="e260a-841"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> Install SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk</span></span>

<span data-ttu-id="e260a-842">Теперь у вас есть рабочая конфигурация отказоустойчивого кластера Windows Server в Azure.</span><span class="sxs-lookup"><span data-stu-id="e260a-842">You now have a working Windows Server Failover Clustering configuration in Azure.</span></span> <span data-ttu-id="e260a-843">Но tooinstall экземпляра SAP ASCS/SCS, необходим общий дисковый ресурс.</span><span class="sxs-lookup"><span data-stu-id="e260a-843">But, tooinstall an SAP ASCS/SCS instance, you need a shared disk resource.</span></span> <span data-ttu-id="e260a-844">Не удается создать hello общие дисковые ресурсы, необходимые в Azure.</span><span class="sxs-lookup"><span data-stu-id="e260a-844">You cannot create hello shared disk resources you need in Azure.</span></span> <span data-ttu-id="e260a-845">SIOS DataKeeper Cluster Edition — это решение независимых производителей, можно использовать toocreate общие дисковые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="e260a-845">SIOS DataKeeper Cluster Edition is a third-party solution you can use toocreate shared disk resources.</span></span>

<span data-ttu-id="e260a-846">Установка SIOS DataKeeper Cluster Edition для hello SAP ASCS/SCS общий ресурс диска кластера включает следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="e260a-846">Installing SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk involves these tasks:</span></span>

- <span data-ttu-id="e260a-847">Добавление hello .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="e260a-847">Adding hello .NET Framework 3.5</span></span>
- <span data-ttu-id="e260a-848">Установка SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="e260a-848">Installing SIOS DataKeeper</span></span>
- <span data-ttu-id="e260a-849">настройка SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="e260a-849">Setting up SIOS DataKeeper</span></span>

#### <span data-ttu-id="e260a-850"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>Добавить hello .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="e260a-850"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> Add hello .NET Framework 3.5</span></span>
<span data-ttu-id="e260a-851">Hello Microsoft .NET Framework 3.5 автоматически не активирована или установить на Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="e260a-851">hello Microsoft .NET Framework 3.5 isn't automatically activated or installed on Windows Server 2012 R2.</span></span> <span data-ttu-id="e260a-852">Поскольку SIOS DataKeeper требует toobe hello .NET Framework на всех узлах, устанавливающие DataKeeper на, необходимо установить .NET Framework 3.5 hello hello гостевой операционной системе всех виртуальных машин в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-852">Because SIOS DataKeeper requires hello .NET Framework toobe on all nodes that you install DataKeeper on, you must install hello .NET Framework 3.5 on hello guest operating system of all virtual machines in hello cluster.</span></span>

<span data-ttu-id="e260a-853">Существует два способа tooadd hello .NET Framework 3.5.</span><span class="sxs-lookup"><span data-stu-id="e260a-853">There are two ways tooadd hello .NET Framework 3.5:</span></span>

- <span data-ttu-id="e260a-854">Использование мастера hello добавления ролей и компонентов в Windows, как показано на рисунке 39.</span><span class="sxs-lookup"><span data-stu-id="e260a-854">Use hello Add Roles and Features Wizard in Windows as shown in Figure 39.</span></span>

  ![На рисунке 39: Установка hello .NET Framework 3.5 с помощью мастера hello добавления ролей и компонентов][sap-ha-guide-figure-3028]

  <span data-ttu-id="e260a-856">_**На рисунке 39:** hello установки .NET Framework 3.5 с помощью мастера hello добавления ролей и компонентов_</span><span class="sxs-lookup"><span data-stu-id="e260a-856">_**Figure 39:** Install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

  ![Рисунок 40: Индикатор установки при установке hello .NET Framework 3.5 с помощью мастера hello добавления ролей и компонентов][sap-ha-guide-figure-3029]

  <span data-ttu-id="e260a-858">_**На рисунке 40:** индикатор установки при установке hello .NET Framework 3.5 с помощью мастера hello добавления ролей и компонентов_</span><span class="sxs-lookup"><span data-stu-id="e260a-858">_**Figure 40:** Installation progress bar when you install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

- <span data-ttu-id="e260a-859">Используйте средство командной строки dism.exe hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-859">Use hello command-line tool dism.exe.</span></span> <span data-ttu-id="e260a-860">Для этого типа установки потребуется каталогу SxS hello tooaccess на установочном носителе Windows hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-860">For this type of installation, you need tooaccess hello SxS directory on hello Windows installation media.</span></span> <span data-ttu-id="e260a-861">В командной строке с повышенными привилегиями выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e260a-861">At an elevated command prompt, type:</span></span>

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <span data-ttu-id="e260a-862"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Установка SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="e260a-862"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Install SIOS DataKeeper</span></span>

<span data-ttu-id="e260a-863">Установите SIOS DataKeeper Cluster Edition на каждом узле в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-863">Install SIOS DataKeeper Cluster Edition on each node in hello cluster.</span></span> <span data-ttu-id="e260a-864">toocreate виртуального хранилища с помощью sios DataKeeper создания синхронизированных зеркального отображения и затем имитировать общее хранилище кластера.</span><span class="sxs-lookup"><span data-stu-id="e260a-864">toocreate virtual shared storage with SIOS DataKeeper, create a synced mirror and then simulate cluster shared storage.</span></span>

<span data-ttu-id="e260a-865">Прежде чем устанавливать программное обеспечение SIOS hello, создайте пользователя домена hello **DataKeeperSvc**.</span><span class="sxs-lookup"><span data-stu-id="e260a-865">Before you install hello SIOS software, create hello domain user **DataKeeperSvc**.</span></span>

> [!NOTE]
> <span data-ttu-id="e260a-866">Добавить hello **DataKeeperSvc** toohello пользователя **локального администратора** на обоих узлов кластера.</span><span class="sxs-lookup"><span data-stu-id="e260a-866">Add hello **DataKeeperSvc** user toohello **Local Administrator** group on both cluster nodes.</span></span>
>
>

<span data-ttu-id="e260a-867">tooinstall SIOS DataKeeper:</span><span class="sxs-lookup"><span data-stu-id="e260a-867">tooinstall SIOS DataKeeper:</span></span>

1.  <span data-ttu-id="e260a-868">Установите программное обеспечение hello SIOS на обоих узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="e260a-868">Install hello SIOS software on both cluster nodes.</span></span>

  ![Установщик SIOS][sap-ha-guide-figure-3030]

  ![На рисунке 41: Первая страница hello SIOS DataKeeper установки][sap-ha-guide-figure-3031]

  <span data-ttu-id="e260a-871">_**На рисунке 41:** первая страница hello установки SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="e260a-871">_**Figure 41:** First page of hello SIOS DataKeeper installation_</span></span>

2.  <span data-ttu-id="e260a-872">В диалоговое окно «hello» показано на рисунке 42, выберите **Да**.</span><span class="sxs-lookup"><span data-stu-id="e260a-872">In hello dialog box shown in Figure 42, select **Yes**.</span></span>

  ![Рис. 42. DataKeeper информирует об отключении службы][sap-ha-guide-figure-3032]

  <span data-ttu-id="e260a-874">_**Рис. 42.** DataKeeper информирует об отключении службы_</span><span class="sxs-lookup"><span data-stu-id="e260a-874">_**Figure 42:** DataKeeper informs you that a service will be disabled_</span></span>

3.  <span data-ttu-id="e260a-875">Диалоговое окно «hello» показано на рисунке 43, мы рекомендуем выбрать **учетную запись домена или сервера**.</span><span class="sxs-lookup"><span data-stu-id="e260a-875">In hello dialog box shown in Figure 43, we recommend that you select **Domain or Server account**.</span></span>

  ![Рис. 43. Выбор пользователя для SIOS DataKeeper][sap-ha-guide-figure-3033]

  <span data-ttu-id="e260a-877">_**Рис. 43.** Выбор пользователя для SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="e260a-877">_**Figure 43:** User selection for SIOS DataKeeper_</span></span>

4.  <span data-ttu-id="e260a-878">Введите имя пользователя учетной записи домена hello и пароли, которые созданы для SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="e260a-878">Enter hello domain account user name and passwords that you created for SIOS DataKeeper.</span></span>

  ![На рисунке 44: Введите hello доменное имя пользователя и пароль для hello установки SIOS DataKeeper][sap-ha-guide-figure-3034]

  <span data-ttu-id="e260a-880">_**На рисунке 44:** введите hello доменное имя пользователя и пароль для hello установки SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="e260a-880">_**Figure 44:** Enter hello domain user name and password for hello SIOS DataKeeper installation_</span></span>

5.  <span data-ttu-id="e260a-881">Установите hello лицензионный ключ для конкретного экземпляра SIOS DataKeeper, как показано на рисунке 45.</span><span class="sxs-lookup"><span data-stu-id="e260a-881">Install hello license key for your SIOS DataKeeper instance as shown in Figure 45.</span></span>

  ![Рис. 45. Указание ключа лицензии на использование SIOS DataKeeper][sap-ha-guide-figure-3035]

  <span data-ttu-id="e260a-883">_**Рис. 45.** Указание ключа лицензии на использование SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="e260a-883">_**Figure 45:** Enter your SIOS DataKeeper license key_</span></span>

6.  <span data-ttu-id="e260a-884">При появлении запроса перезапустите виртуальную машину hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-884">When prompted, restart hello virtual machine.</span></span>

#### <span data-ttu-id="e260a-885"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Настройка SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="e260a-885"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Set up SIOS DataKeeper</span></span>

<span data-ttu-id="e260a-886">После установки SIOS DataKeeper на обоих узлах, необходимо toostart hello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e260a-886">After you install SIOS DataKeeper on both nodes, you need toostart hello configuration.</span></span> <span data-ttu-id="e260a-887">Цель Hello hello конфигурации — toohave синхронные данные репликации между дополнительные диски hello присоединен tooeach hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e260a-887">hello goal of hello configuration is toohave synchronous data replication between hello additional disks attached tooeach of hello virtual machines.</span></span>

1.  <span data-ttu-id="e260a-888">Запуск hello DataKeeper управления и средство настройки, а затем выберите **подключение серверу**.</span><span class="sxs-lookup"><span data-stu-id="e260a-888">Start hello DataKeeper Management and Configuration tool, and then select **Connect Server**.</span></span> <span data-ttu-id="e260a-889">(На рис. 46 эта ссылка обведена красным.)</span><span class="sxs-lookup"><span data-stu-id="e260a-889">(In Figure 46, this option is circled in red.)</span></span>

  ![Рис. 46. Инструмент управления и настройки DataKeeper][sap-ha-guide-figure-3036]

  <span data-ttu-id="e260a-891">_**Рис. 46.** Инструмент управления и настройки DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="e260a-891">_**Figure 46:** SIOS DataKeeper Management and Configuration tool_</span></span>

2.  <span data-ttu-id="e260a-892">Введите имя hello или адрес TCP/IP hello первый узел hello управление и настройку средства следует установите соединение и на втором шаге hello второй узел.</span><span class="sxs-lookup"><span data-stu-id="e260a-892">Enter hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and, in a second step, hello second node.</span></span>

  ![На рисунке 47: Hello укажите имя или IP-адрес hello первый узел hello управление и настройку средства следует подключаться к, а на втором шаге, а второй узел hello][sap-ha-guide-figure-3037]

  <span data-ttu-id="e260a-894">_**На рисунке 47:** hello укажите имя или IP-адрес hello первый узел hello управление и настройку средства следует подключаться к, а на втором шаге, а второй узел hello_</span><span class="sxs-lookup"><span data-stu-id="e260a-894">_**Figure 47:** Insert hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and in a second step, hello second node_</span></span>

3.  <span data-ttu-id="e260a-895">Создание задания hello репликации между двумя узлами hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-895">Create hello replication job between hello two nodes.</span></span>

  ![Рис. 48. Создание задания репликации][sap-ha-guide-figure-3038]

  <span data-ttu-id="e260a-897">_**Рис. 48.** Создание задания репликации_</span><span class="sxs-lookup"><span data-stu-id="e260a-897">_**Figure 48:** Create a replication job_</span></span>

  <span data-ttu-id="e260a-898">Мастер помогает выполнить процесс создания задания репликации hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-898">A wizard guides you through hello process of creating a replication job.</span></span>
4.  <span data-ttu-id="e260a-899">Укажите имя hello, TCP/IP-адрес и тома hello исходного узла.</span><span class="sxs-lookup"><span data-stu-id="e260a-899">Define hello name, TCP/IP address, and disk volume of hello source node.</span></span>

  ![Рисунок 49: Определяет имя hello hello задания репликации][sap-ha-guide-figure-3039]

  <span data-ttu-id="e260a-901">_**Рисунок 49:** имя hello определение задания репликации hello_</span><span class="sxs-lookup"><span data-stu-id="e260a-901">_**Figure 49:** Define hello name of hello replication job_</span></span>

  ![На рисунке 50: Определения hello базовых данных для hello узел, который должен быть hello текущего узла источника][sap-ha-guide-figure-3040]

  <span data-ttu-id="e260a-903">_**На рисунке 50:** определения базовых данных hello hello узел, который должен быть hello текущего узла источника_</span><span class="sxs-lookup"><span data-stu-id="e260a-903">_**Figure 50:** Define hello base data for hello node, which should be hello current source node_</span></span>

5.  <span data-ttu-id="e260a-904">Укажите имя hello, TCP/IP-адрес и тома hello целевого узла.</span><span class="sxs-lookup"><span data-stu-id="e260a-904">Define hello name, TCP/IP address, and disk volume of hello target node.</span></span>

  ![Рисунок 51: Определения hello базовых данных для hello узел, который должен быть hello текущего целевого узла][sap-ha-guide-figure-3041]

  <span data-ttu-id="e260a-906">_**На рисунке 51:** определить базовые данные hello hello узел, который должен быть hello текущей целевой узел_</span><span class="sxs-lookup"><span data-stu-id="e260a-906">_**Figure 51:** Define hello base data for hello node, which should be hello current target node_</span></span>

6.  <span data-ttu-id="e260a-907">Определение алгоритма сжатия hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-907">Define hello compression algorithms.</span></span> <span data-ttu-id="e260a-908">В нашем примере мы рекомендуем сжимать hello потока репликации.</span><span class="sxs-lookup"><span data-stu-id="e260a-908">In our example, we recommend that you compress hello replication stream.</span></span> <span data-ttu-id="e260a-909">Особенно в случаях повторная синхронизация hello сжатия потока репликации hello значительно сокращает время повторной синхронизации.</span><span class="sxs-lookup"><span data-stu-id="e260a-909">Especially in resynchronization situations, hello compression of hello replication stream dramatically reduces resynchronization time.</span></span> <span data-ttu-id="e260a-910">Обратите внимание, что сжатие использует ресурсы ЦП и ОЗУ hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e260a-910">Note that compression uses hello CPU and RAM resources of a virtual machine.</span></span> <span data-ttu-id="e260a-911">При увеличении hello степень сжатия, поэтому hello объем ресурсов ЦП, используемых.</span><span class="sxs-lookup"><span data-stu-id="e260a-911">As hello compression rate increases, so does hello volume of CPU resources used.</span></span> <span data-ttu-id="e260a-912">Этот параметр можно изменить позже.</span><span class="sxs-lookup"><span data-stu-id="e260a-912">You also can adjust this setting later.</span></span>

7.  <span data-ttu-id="e260a-913">Требуется другой параметр toocheck является, происходит ли репликация hello синхронно или асинхронно.</span><span class="sxs-lookup"><span data-stu-id="e260a-913">Another setting you need toocheck is whether hello replication occurs asynchronously or synchronously.</span></span> <span data-ttu-id="e260a-914">*Для защиты конфигураций SAP ASCS/SCS требуется синхронная репликация*.</span><span class="sxs-lookup"><span data-stu-id="e260a-914">*When you protect SAP ASCS/SCS configurations, you must use synchronous replication*.</span></span>  

  ![Рис. 52. Определение сведений о репликации][sap-ha-guide-figure-3042]

  <span data-ttu-id="e260a-916">_**Рис. 52.** Определение сведений о репликации_</span><span class="sxs-lookup"><span data-stu-id="e260a-916">_**Figure 52:** Define replication details_</span></span>

8.  <span data-ttu-id="e260a-917">Указать ли том hello, реплицируется с задания репликации hello представленного tooa отказоустойчивой кластеризации Windows Server конфигурации кластера как общего диска.</span><span class="sxs-lookup"><span data-stu-id="e260a-917">Define whether hello volume that is replicated by hello replication job should be represented tooa Windows Server Failover Clustering cluster configuration as a shared disk.</span></span> <span data-ttu-id="e260a-918">Конфигурации SAP ASCS/SCS hello, выберите **Да** , чтобы видит кластера Windows hello hello реплицированных том в качестве общего диска, его можно использовать в качестве тома кластера.</span><span class="sxs-lookup"><span data-stu-id="e260a-918">For hello SAP ASCS/SCS configuration, select **Yes** so that hello Windows cluster sees hello replicated volume as a shared disk that it can use as a cluster volume.</span></span>

  ![На рисунке 53: Hello tooset выберите «Да» репликации тома томом кластера][sap-ha-guide-figure-3043]

  <span data-ttu-id="e260a-920">_**На рисунке 53:** выберите **Да** tooset hello реплицируются в качестве тома кластера_</span><span class="sxs-lookup"><span data-stu-id="e260a-920">_**Figure 53:** Select **Yes** tooset hello replicated volume as a cluster volume_</span></span>

  <span data-ttu-id="e260a-921">После создания тома hello hello DataKeeper средство управления и конфигурации показывает задания репликации hello активен.</span><span class="sxs-lookup"><span data-stu-id="e260a-921">After hello volume is created, hello DataKeeper Management and Configuration tool shows that hello replication job is active.</span></span>

  ![Рисунок 54: DataKeeper синхронной активен режим зеркального отображения для hello SAP ASCS/SCS общего ресурса диска][sap-ha-guide-figure-3044]

  <span data-ttu-id="e260a-923">_**На рисунке 54:** DataKeeper синхронной активен режим зеркального отображения для hello SAP ASCS/SCS папку диска_</span><span class="sxs-lookup"><span data-stu-id="e260a-923">_**Figure 54:** DataKeeper synchronous mirroring for hello SAP ASCS/SCS share disk is active_</span></span>

  <span data-ttu-id="e260a-924">Диспетчер отказоустойчивости кластеров теперь отображает hello диск как диск DataKeeper, как показано на рисунке 55.</span><span class="sxs-lookup"><span data-stu-id="e260a-924">Failover Cluster Manager now shows hello disk as a DataKeeper disk, as shown in Figure 55.</span></span>

  ![На рисунке 55: Hello диска, для которых репликация DataKeeper показано, диспетчера отказоустойчивого кластера][sap-ha-guide-figure-3045]

  <span data-ttu-id="e260a-926">_**На рисунке 55:** Диспетчер отказоустойчивости кластеров показывает hello диска, DataKeeper репликации_</span><span class="sxs-lookup"><span data-stu-id="e260a-926">_**Figure 55:** Failover Cluster Manager shows hello disk that DataKeeper replicated_</span></span>

## <span data-ttu-id="e260a-927"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>Установка системы SAP NetWeaver hello</span><span class="sxs-lookup"><span data-stu-id="e260a-927"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> Install hello SAP NetWeaver system</span></span>

<span data-ttu-id="e260a-928">Мы не описание настройки СУБД hello, так как параметры настройки зависят от используемой системы СУБД hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-928">We won’t describe hello DBMS setup because setups vary depending on hello DBMS system you use.</span></span> <span data-ttu-id="e260a-929">Тем не менее мы предполагаем, что опасения высокого уровня доступности СУБД hello адресуются с возможностями hello hello различных поставщиков СУБД поддержку Azure.</span><span class="sxs-lookup"><span data-stu-id="e260a-929">However, we assume that high-availability concerns with hello DBMS are addressed with hello functionalities hello different DBMS vendors support for Azure.</span></span> <span data-ttu-id="e260a-930">Например, AlwaysOn или зеркальное отображение базы данных для SQL Server и Oracle Data Guard для баз данных Oracle.</span><span class="sxs-lookup"><span data-stu-id="e260a-930">For example, Always On or database mirroring for SQL Server, and Oracle Data Guard for Oracle databases.</span></span> <span data-ttu-id="e260a-931">В случае hello мы используем в этой статье мы не добавлять дополнительные toohello защиты СУБД.</span><span class="sxs-lookup"><span data-stu-id="e260a-931">In hello scenario we use in this article, we didn't add more protection toohello DBMS.</span></span>

<span data-ttu-id="e260a-932">Особые рекомендации по взаимодействию различных СУБД с такой кластеризованной конфигурацией SAP ASCS/SCS в Azure отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="e260a-932">There are no special considerations when different DBMS services interact with this kind of clustered SAP ASCS/SCS configuration in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="e260a-933">процедуры установки Hello систем SAP NetWeaver ABAP, Java систем и систем ABAP + Java практически идентичны.</span><span class="sxs-lookup"><span data-stu-id="e260a-933">hello installation procedures of SAP NetWeaver ABAP systems, Java systems, and ABAP+Java systems are almost identical.</span></span> <span data-ttu-id="e260a-934">наиболее важное отличие Hello, имеет систему SAP ABAP один экземпляр ASCS.</span><span class="sxs-lookup"><span data-stu-id="e260a-934">hello most significant difference is that an SAP ABAP system has one ASCS instance.</span></span> <span data-ttu-id="e260a-935">Hello системы SAP Java имеет один экземпляр SCS.</span><span class="sxs-lookup"><span data-stu-id="e260a-935">hello SAP Java system has one SCS instance.</span></span> <span data-ttu-id="e260a-936">Hello системы SAP ABAP + Java имеет один экземпляр ASCS и один экземпляр SCS, работающий в hello же группы отказоустойчивого кластера Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="e260a-936">hello SAP ABAP+Java system has one ASCS instance and one SCS instance running in hello same Microsoft failover cluster group.</span></span> <span data-ttu-id="e260a-937">Любые отличия в установке для каждого стека установки SAP NetWeaver будут указаны явным образом.</span><span class="sxs-lookup"><span data-stu-id="e260a-937">Any installation differences for each SAP NetWeaver installation stack are explicitly mentioned.</span></span> <span data-ttu-id="e260a-938">Можно предположить, что все остальные элементы являются hello таким же.</span><span class="sxs-lookup"><span data-stu-id="e260a-938">You can assume that all other parts are hello same.</span></span>  
>
>

### <span data-ttu-id="e260a-939"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Установка SAP с высокодоступным экземпляром ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e260a-939"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Install SAP with a high-availability ASCS/SCS instance</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e260a-940">Убедитесь, что не tooplace файлов на странице на DataKeeper зеркальных томов.</span><span class="sxs-lookup"><span data-stu-id="e260a-940">Be sure not tooplace your page file on DataKeeper mirrored volumes.</span></span> <span data-ttu-id="e260a-941">DataKeeper не поддерживает зеркальные тома.</span><span class="sxs-lookup"><span data-stu-id="e260a-941">DataKeeper does not support mirrored volumes.</span></span> <span data-ttu-id="e260a-942">Можно оставить файл подкачки на временном диске hello D из виртуальной машины Azure которого — по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-942">You can leave your page file on hello temporary drive D of an Azure virtual machine, which is hello default.</span></span> <span data-ttu-id="e260a-943">Если он еще не существует, переместите приветствия Windows страницы файла toodrive D: Azure виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e260a-943">If it's not already there, move hello Windows page file toodrive D: of your Azure virtual machine.</span></span>
>
>

<span data-ttu-id="e260a-944">Установка SAP с высокодоступным экземпляром ASCS/SCS состоит из следующих заданий:</span><span class="sxs-lookup"><span data-stu-id="e260a-944">Installing SAP with a high-availability ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="e260a-945">Создание виртуального имени узла для hello кластеризованного экземпляра SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e260a-945">Creating a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>
- <span data-ttu-id="e260a-946">Установка первого узла кластера hello SAP</span><span class="sxs-lookup"><span data-stu-id="e260a-946">Installing hello SAP first cluster node</span></span>
- <span data-ttu-id="e260a-947">Изменение профиля hello SAP ASCS/SCS экземпляра hello</span><span class="sxs-lookup"><span data-stu-id="e260a-947">Modifying hello SAP profile of hello ASCS/SCS instance</span></span>
- <span data-ttu-id="e260a-948">добавление порта пробы;</span><span class="sxs-lookup"><span data-stu-id="e260a-948">Adding a probe port</span></span>
- <span data-ttu-id="e260a-949">Открытие порта пробы в брандмауэре Windows hello</span><span class="sxs-lookup"><span data-stu-id="e260a-949">Opening hello Windows firewall probe port</span></span>

#### <span data-ttu-id="e260a-950"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>Создание виртуального имени узла для hello кластеризованного экземпляра SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e260a-950"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> Create a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>

1.  <span data-ttu-id="e260a-951">В диспетчере Windows DNS hello создайте запись DNS для имени виртуального узла hello hello ASCS/SCS экземпляра.</span><span class="sxs-lookup"><span data-stu-id="e260a-951">In hello Windows DNS manager, create a DNS entry for hello virtual host name of hello ASCS/SCS instance.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="e260a-952">Hello IP-адрес, назначьте имя виртуального узла toohello ASCS/SCS экземпляр должен быть hello hello же, как hello IP-адрес, назначенный tooAzure балансировки нагрузки (**<*SID*> - балансировки нагрузки - ascs **).</span><span class="sxs-lookup"><span data-stu-id="e260a-952">hello IP address that you assign toohello virtual host name of hello ASCS/SCS instance must be hello same as hello IP address that you assigned tooAzure Load Balancer (**<*SID*>-lb-ascs**).</span></span>  
  >
  >

  <span data-ttu-id="e260a-953">Здравствуйте, IP-адрес hello виртуальное имя узла SAP ASCS/SCS (**pr1 ascs sap**) hello же, как hello IP-адрес подсистемы балансировки нагрузки Azure (**pr1 балансировки нагрузки ascs**).</span><span class="sxs-lookup"><span data-stu-id="e260a-953">hello IP address of hello virtual SAP ASCS/SCS host name (**pr1-ascs-sap**) is hello same as hello IP address of Azure Load Balancer (**pr1-lb-ascs**).</span></span>

  ![На рисунке 56: Определение hello DNS-запись для hello SAP ASCS/SCS виртуальное имя кластера и TCP/IP-адрес][sap-ha-guide-figure-3046]

  <span data-ttu-id="e260a-955">_**На рисунке 56:** определить hello DNS-запись для hello SAP ASCS/SCS виртуальное имя кластера и TCP/IP-адрес_</span><span class="sxs-lookup"><span data-stu-id="e260a-955">_**Figure 56:** Define hello DNS entry for hello SAP ASCS/SCS cluster virtual name and TCP/IP address_</span></span>

2.  <span data-ttu-id="e260a-956">toodefine hello IP-адреса, назначенного toohello виртуальное имя узла, выберите **диспетчер DNS** > **домена**.</span><span class="sxs-lookup"><span data-stu-id="e260a-956">toodefine hello IP address assigned toohello virtual host name, select **DNS Manager** > **Domain**.</span></span>

  ![Рис. 57. Новое виртуальное имя и TCP/IP-адрес для конфигурации кластера SAP ASCS/SCS][sap-ha-guide-figure-3047]

  <span data-ttu-id="e260a-958">_**Рис. 57.** Новое виртуальное имя и TCP/IP-адрес для конфигурации кластера SAP ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="e260a-958">_**Figure 57:** New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration_</span></span>

#### <span data-ttu-id="e260a-959"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>Установите первый узел кластера hello SAP</span><span class="sxs-lookup"><span data-stu-id="e260a-959"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> Install hello SAP first cluster node</span></span>

1.  <span data-ttu-id="e260a-960">Выполните первый вариант узла кластера hello на узле кластера, а. Например, на hello **pr1-ascs-0** узла.</span><span class="sxs-lookup"><span data-stu-id="e260a-960">Execute hello first cluster node option on cluster node A. For example, on hello **pr1-ascs-0** host.</span></span>
2.  <span data-ttu-id="e260a-961">порты по умолчанию hello tookeep для hello Azure внутренняя Подсистема балансировки нагрузки, выберите:</span><span class="sxs-lookup"><span data-stu-id="e260a-961">tookeep hello default ports for hello Azure internal load balancer, select:</span></span>

  * <span data-ttu-id="e260a-962">для **системы ABAP** — экземпляр **ASCS** с номером **00**;</span><span class="sxs-lookup"><span data-stu-id="e260a-962">**ABAP system**: **ASCS** instance number **00**</span></span>
  * <span data-ttu-id="e260a-963">для **системы Java** — экземпляр **SCS** с номером **01**;</span><span class="sxs-lookup"><span data-stu-id="e260a-963">**Java system**: **SCS** instance number **01**</span></span>
  * <span data-ttu-id="e260a-964">для **системы ABAP с Java** — экземпляр **ASCS** с номером **00** и экземпляр **SCS** с номером **01**.</span><span class="sxs-lookup"><span data-stu-id="e260a-964">**ABAP+Java system**: **ASCS** instance number **00** and **SCS** instance number **01**</span></span>

  <span data-ttu-id="e260a-965">экземпляр toouse цифры, отличный от 00 для hello ABAP ASCS экземпляра и 01 для экземпляра Java SCS hello, сначала необходимо toochange hello Azure внутренней нагрузки подсистемы балансировки нагрузки по умолчанию балансировки правил, описанных в [нагрузки по умолчанию ASCS/SCS hello изменений правила для hello Azure внутренней подсистемы балансировки нагрузки подсистемы балансировки][sap-ha-guide-8.9].</span><span class="sxs-lookup"><span data-stu-id="e260a-965">toouse instance numbers other than 00 for hello ABAP ASCS instance and 01 for hello Java SCS instance, first you need toochange hello Azure internal load balancer default load balancing rules, described in [Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer][sap-ha-guide-8.9].</span></span>

<span data-ttu-id="e260a-966">Hello Далее некоторые действия не описаны в hello Стандартная документацию по установке SAP.</span><span class="sxs-lookup"><span data-stu-id="e260a-966">hello next few tasks aren't described in hello standard SAP installation documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="e260a-967">документацию по установке SAP Hello описывает, как tooinstall hello первый узел кластера ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="e260a-967">hello SAP installation documentation describes how tooinstall hello first ASCS/SCS cluster node.</span></span>
>
>

#### <span data-ttu-id="e260a-968"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>Изменение профиля hello SAP ASCS/SCS экземпляра hello</span><span class="sxs-lookup"><span data-stu-id="e260a-968"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> Modify hello SAP profile of hello ASCS/SCS instance</span></span>

<span data-ttu-id="e260a-969">Необходимо tooadd новый параметр профиля.</span><span class="sxs-lookup"><span data-stu-id="e260a-969">You need tooadd a new profile parameter.</span></span> <span data-ttu-id="e260a-970">параметр профиля Hello предотвращает соединения между SAP рабочие процессы и сервер постановки в очередь hello закрытие при бездействии слишком долго.</span><span class="sxs-lookup"><span data-stu-id="e260a-970">hello profile parameter prevents connections between SAP work processes and hello enqueue server from closing when they are idle for too long.</span></span> <span data-ttu-id="e260a-971">Мы уже упоминали сценарий проблемы hello в [добавления записей реестра на обоих узлах кластера экземпляра SAP ASCS/SCS hello][sap-ha-guide-8.11].</span><span class="sxs-lookup"><span data-stu-id="e260a-971">We mentioned hello problem scenario in [Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance][sap-ha-guide-8.11].</span></span> <span data-ttu-id="e260a-972">В этом разделе мы также представили два изменения toosome basic TCP/IP параметры соединения.</span><span class="sxs-lookup"><span data-stu-id="e260a-972">In that section, we also introduced two changes toosome basic TCP/IP connection parameters.</span></span> <span data-ttu-id="e260a-973">На втором шаге нужно поставить в очередь сервера tooset hello toosend `keep_alive` сигнала, чтобы подключения hello не достигнуть Порог простоя подсистемы балансировки нагрузки Azure внутренней hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-973">In a second step, you need tooset hello enqueue server toosend a `keep_alive` signal so that hello connections don't hit hello Azure internal load balancer's idle threshold.</span></span>

<span data-ttu-id="e260a-974">hello toomodify профиль SAP ASCS/SCS экземпляра hello:</span><span class="sxs-lookup"><span data-stu-id="e260a-974">toomodify hello SAP profile of hello ASCS/SCS instance:</span></span>

1.  <span data-ttu-id="e260a-975">Добавьте этот профиль параметр toohello профиль экземпляра SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="e260a-975">Add this profile parameter toohello SAP ASCS/SCS instance profile:</span></span>

  ```
  enque/encni/set_so_keepalive = true
  ```
  <span data-ttu-id="e260a-976">В нашем примере — hello путь:</span><span class="sxs-lookup"><span data-stu-id="e260a-976">In our example, hello path is:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  <span data-ttu-id="e260a-977">Например профиль экземпляр toohello SAP SCS и путь к соответствующему:</span><span class="sxs-lookup"><span data-stu-id="e260a-977">For example, toohello SAP SCS instance profile and corresponding path:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  <span data-ttu-id="e260a-978">tooapply hello изменения, перезапустите экземпляр SAP ASCS /SCS hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-978">tooapply hello changes, restart hello SAP ASCS /SCS instance.</span></span>

#### <span data-ttu-id="e260a-979"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Добавление порта пробы</span><span class="sxs-lookup"><span data-stu-id="e260a-979"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Add a probe port</span></span>

<span data-ttu-id="e260a-980">Используйте hello внутренней подсистемы балансировки нагрузки проверки функциональности toomake hello весь кластер конфигурации рабочих с подсистемы балансировки нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="e260a-980">Use hello internal load balancer's probe functionality toomake hello entire cluster configuration work with Azure Load Balancer.</span></span> <span data-ttu-id="e260a-981">Hello Azure внутренней подсистемы балансировки нагрузки обычно распределяет входящие рабочей нагрузки hello поровну между участвующими виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e260a-981">hello Azure internal load balancer usually distributes hello incoming workload equally between participating virtual machines.</span></span> <span data-ttu-id="e260a-982">Однако это не будет работать в некоторых конфигурациях кластера, так как активен только один экземпляр.</span><span class="sxs-lookup"><span data-stu-id="e260a-982">However, this won't work in some cluster configurations because only one instance is active.</span></span> <span data-ttu-id="e260a-983">Hello другого экземпляра является пассивным и не может принимать любой рабочей нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-983">hello other instance is passive and can’t accept any of hello workload.</span></span> <span data-ttu-id="e260a-984">Функции проверки помогают при использовании назначает подсистемы балансировки нагрузки Azure внутренней hello работать только tooan активный экземпляр.</span><span class="sxs-lookup"><span data-stu-id="e260a-984">A probe functionality helps when hello Azure internal load balancer assigns work only tooan active instance.</span></span> <span data-ttu-id="e260a-985">Возможности проверки hello hello внутренней подсистемы балансировки нагрузки может обнаружить экземпляры, которые активны, а затем выбрать только экземпляр hello hello рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e260a-985">With hello probe functionality, hello internal load balancer can detect which instances are active, and then target only hello instance with hello workload.</span></span>

<span data-ttu-id="e260a-986">tooadd порт пробы:</span><span class="sxs-lookup"><span data-stu-id="e260a-986">tooadd a probe port:</span></span>

1.  <span data-ttu-id="e260a-987">Проверьте текущий hello **ProbePort** задание, выполнив следующую команду PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-987">Check hello current **ProbePort** setting by running hello following PowerShell command.</span></span> <span data-ttu-id="e260a-988">Выполните из в одном hello виртуальных машин в конфигурации кластера hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-988">Execute it from within one of hello virtual machines in hello cluster configuration.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  <span data-ttu-id="e260a-989">Укажите порт пробы.</span><span class="sxs-lookup"><span data-stu-id="e260a-989">Define a probe port.</span></span> <span data-ttu-id="e260a-990">номер порта пробы по умолчанию Hello **0**.</span><span class="sxs-lookup"><span data-stu-id="e260a-990">hello default probe port number is **0**.</span></span> <span data-ttu-id="e260a-991">В нашем примере мы используем порт пробы **62000**.</span><span class="sxs-lookup"><span data-stu-id="e260a-991">In our example, we use probe port **62000**.</span></span>

  ![На рисунке 58: порт пробы hello кластера конфигурации по умолчанию равно 0][sap-ha-guide-figure-3048]

  <span data-ttu-id="e260a-993">_**На рисунке 58:** порт пробы конфигурации кластера по умолчанию hello равно 0_</span><span class="sxs-lookup"><span data-stu-id="e260a-993">_**Figure 58:** hello default cluster configuration probe port is 0_</span></span>

  <span data-ttu-id="e260a-994">номер порта Hello определяется в шаблоны диспетчера ресурсов Azure для SAP.</span><span class="sxs-lookup"><span data-stu-id="e260a-994">hello port number is defined in SAP Azure Resource Manager templates.</span></span> <span data-ttu-id="e260a-995">Можно назначить hello номер порта в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e260a-995">You can assign hello port number in PowerShell.</span></span>

  <span data-ttu-id="e260a-996">новое значение для hello ProbePort tooset  **SAP <*SID*> IP ** ресурса кластера, запустите следующий сценарий PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-996">tooset a new ProbePort value for hello **SAP <*SID*> IP** cluster resource, run hello following PowerShell script.</span></span> <span data-ttu-id="e260a-997">Обновите переменные PowerShell hello для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="e260a-997">Update hello PowerShell variables for your environment.</span></span> <span data-ttu-id="e260a-998">После запуска сценария hello, вы будете tooactivate изменения hello SAP кластера запрашиваемые toorestart hello группы.</span><span class="sxs-lookup"><span data-stu-id="e260a-998">After hello script runs, you'll be prompted toorestart hello SAP cluster group tooactivate hello changes.</span></span>

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  Clear-Host
  $SAPClusterRoleName = "SAP $SAPSID"
  $SAPIPresourceName = "SAP $SAPSID IP"
  $SAPIPResourceClusterParameters =  Get-ClusterResource $SAPIPresourceName | Get-ClusterParameter
  $IPAddress = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Address" }).Value
  $NetworkName = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Network" }).Value
  $SubnetMask = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "SubnetMask" }).Value
  $OverrideAddressMatch = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "OverrideAddressMatch" }).Value
  $EnableDhcp = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "EnableDhcp" }).Value
  $OldProbePort = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "ProbePort" }).Value

  $var = Get-ClusterResource | Where-Object {  $_.name -eq $SAPIPresourceName  }

  Write-Host "Current configuration parameters for SAP IP cluster resource '$SAPIPresourceName' are:" -ForegroundColor Cyan
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter

  Write-Host
  Write-Host "Current probe port property of hello SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting hello new probe port property of hello SAP cluster resource '$SAPIPresourceName' too'$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want tootake restart SAP cluster role '$SAPClusterRoleName', tooactivate hello changes (yes/no)?"

  if($ActivateChanges -eq "yes"){
  Write-Host
  Write-Host "Activating changes..." -ForegroundColor Cyan

  Write-Host
  write-host "Taking SAP cluster IP resource '$SAPIPresourceName' offline ..." -ForegroundColor Cyan
  Stop-ClusterResource -Name $SAPIPresourceName
  sleep 5

  Write-Host "Starting SAP cluster role '$SAPClusterRoleName' ..." -ForegroundColor Cyan
  Start-ClusterGroup -Name $SAPClusterRoleName

  Write-Host "New ProbePort parameter is active." -ForegroundColor Green
  Write-Host

  Write-Host "New configuration parameters for SAP IP cluster resource '$SAPIPresourceName':" -ForegroundColor Cyan
  Write-Host
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter
  }else
  {
  Write-Host "Changes are not activated."
  }
  ```

  <span data-ttu-id="e260a-999">После переноса hello  **SAP <*SID*> ** роль сети кластера, убедитесь, что **ProbePort** задано новое значение toohello.</span><span class="sxs-lookup"><span data-stu-id="e260a-999">After you bring hello **SAP <*SID*>** cluster role online, verify that **ProbePort** is set toohello new value.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Рисунок 59: Hello кластера порта пробы, задав новое значение hello][sap-ha-guide-figure-3049]

  <span data-ttu-id="e260a-1001">_**На рисунке 59:** hello кластера порта пробы, задав новое значение hello_</span><span class="sxs-lookup"><span data-stu-id="e260a-1001">_**Figure 59:** Probe hello cluster port after you set hello new value_</span></span>

#### <span data-ttu-id="e260a-1002"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Открытие порта пробы в брандмауэре Windows hello</span><span class="sxs-lookup"><span data-stu-id="e260a-1002"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Open hello Windows firewall probe port</span></span>

<span data-ttu-id="e260a-1003">Необходимо tooopen порта пробы в брандмауэре Windows на обоих узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="e260a-1003">You need tooopen a Windows firewall probe port on both cluster nodes.</span></span> <span data-ttu-id="e260a-1004">Используйте следующий сценарий tooopen порта пробы в брандмауэре Windows hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-1004">Use hello following script tooopen a Windows firewall probe port.</span></span> <span data-ttu-id="e260a-1005">Обновите переменные PowerShell hello для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="e260a-1005">Update hello PowerShell variables for your environment.</span></span>

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

<span data-ttu-id="e260a-1006">Hello **ProbePort** задано слишком**62000**.</span><span class="sxs-lookup"><span data-stu-id="e260a-1006">hello **ProbePort** is set too**62000**.</span></span> <span data-ttu-id="e260a-1007">Теперь можно получить доступ к общей папке hello  **\\\ascsha-clsap\sapmnt** от других узлов, например, в **ascsha Администраторы**.</span><span class="sxs-lookup"><span data-stu-id="e260a-1007">Now you can access hello file share **\\\ascsha-clsap\sapmnt** from other hosts, such as from **ascsha-dbas**.</span></span>

### <span data-ttu-id="e260a-1008"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Установите экземпляр базы данных hello</span><span class="sxs-lookup"><span data-stu-id="e260a-1008"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> Install hello database instance</span></span>

<span data-ttu-id="e260a-1009">База данных hello tooinstall экземпляра, выполните hello процесс, описанный в документации по установке SAP hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-1009">tooinstall hello database instance, follow hello process described in hello SAP installation documentation.</span></span>

### <span data-ttu-id="e260a-1010"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>Установка hello второго узла кластера</span><span class="sxs-lookup"><span data-stu-id="e260a-1010"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> Install hello second cluster node</span></span>

<span data-ttu-id="e260a-1011">tooinstall hello второй кластер, повторите шаги hello в руководстве по установке SAP hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-1011">tooinstall hello second cluster, follow hello steps in hello SAP installation guide.</span></span>

### <span data-ttu-id="e260a-1012"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>Изменить тип запуска hello экземпляра службы SAP ющих Методов Windows hello</span><span class="sxs-lookup"><span data-stu-id="e260a-1012"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> Change hello start type of hello SAP ERS Windows service instance</span></span>

<span data-ttu-id="e260a-1013">Измените тип запуска службы SAP ющих Методов Windows hello hello слишком**автоматически (отложенный запуск)** на обоих узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="e260a-1013">Change hello start type of hello SAP ERS Windows service too**Automatic (Delayed Start)** on both cluster nodes.</span></span>

![Рисунок 60: Изменить тип службы hello для автоматического toodelayed экземпляра SAP ющих Методов hello][sap-ha-guide-figure-3050]

<span data-ttu-id="e260a-1015">_**На рисунке 60:** hello типа службы для автоматического toodelayed экземпляра SAP ющих Методов hello_</span><span class="sxs-lookup"><span data-stu-id="e260a-1015">_**Figure 60:** Change hello service type for hello SAP ERS instance toodelayed automatic_</span></span>

### <span data-ttu-id="e260a-1016"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>Установка hello первичного сервера приложений SAP</span><span class="sxs-lookup"><span data-stu-id="e260a-1016"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> Install hello SAP Primary Application Server</span></span>

<span data-ttu-id="e260a-1017">Установить экземпляр основного сервера приложений (PAS) hello <*SID*> hello toohost - di - 0 на виртуальной машине hello, назначенный вами PAS.</span><span class="sxs-lookup"><span data-stu-id="e260a-1017">Install hello Primary Application Server (PAS) instance <*SID*>-di-0 on hello virtual machine that you've designated toohost hello PAS.</span></span> <span data-ttu-id="e260a-1018">Какие-либо специальные зависимости от параметров Azure или DataKeeper отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="e260a-1018">There are no dependencies on Azure or DataKeeper-specific settings.</span></span>

### <span data-ttu-id="e260a-1019"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>Установка дополнительного сервера приложений SAP hello</span><span class="sxs-lookup"><span data-stu-id="e260a-1019"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> Install hello SAP Additional Application Server</span></span>

<span data-ttu-id="e260a-1020">Установите SAP дополнительные приложения сервера (Консультанты) на всех виртуальных машин hello, что был указан toohost экземпляр сервера приложений SAP.</span><span class="sxs-lookup"><span data-stu-id="e260a-1020">Install an SAP Additional Application Server (AAS) on all hello virtual machines that you've designated toohost an SAP Application Server instance.</span></span> <span data-ttu-id="e260a-1021">Например, на <*SID*> - di - 1 слишком <*SID*> - di -&lt;n&gt;.</span><span class="sxs-lookup"><span data-stu-id="e260a-1021">For example, on <*SID*>-di-1 too<*SID*>-di-&lt;n&gt;.</span></span>

> [!NOTE]
> <span data-ttu-id="e260a-1022">Это завершает установку hello в системе SAP NetWeaver высокого уровня доступности.</span><span class="sxs-lookup"><span data-stu-id="e260a-1022">This finishes hello installation of a high-availability SAP NetWeaver system.</span></span> <span data-ttu-id="e260a-1023">Затем перейдите к тестированию отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="e260a-1023">Next, proceed with failover testing.</span></span>
>


## <span data-ttu-id="e260a-1024"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>Тестирование отработки отказа экземпляра SAP ASCS/SCS hello и SIOS репликации</span><span class="sxs-lookup"><span data-stu-id="e260a-1024"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> Test hello SAP ASCS/SCS instance failover and SIOS replication</span></span>
<span data-ttu-id="e260a-1025">Он просто tootest и мониторинг экземпляра SAP ASCS/SCS перехода на другой ресурс и SIOS репликации дисков с помощью диспетчера отказоустойчивости кластеров и средства настройки и управления SIOS DataKeeper hello.</span><span class="sxs-lookup"><span data-stu-id="e260a-1025">It's easy tootest and monitor an SAP ASCS/SCS instance failover and SIOS disk replication by using Failover Cluster Manager and hello SIOS DataKeeper Management and Configuration tool.</span></span>

### <span data-ttu-id="e260a-1026"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> Экземпляр SAP ASCS/SCS выполняется на узле A кластера</span><span class="sxs-lookup"><span data-stu-id="e260a-1026"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS instance is running on cluster node A</span></span>

<span data-ttu-id="e260a-1027">Hello **SAP PR1** группы кластера выполняется на узле кластера, а. Например, на **pr1-ascs-0**.</span><span class="sxs-lookup"><span data-stu-id="e260a-1027">hello **SAP PR1** cluster group is running on cluster node A. For example, on **pr1-ascs-0**.</span></span> <span data-ttu-id="e260a-1028">Назначить hello общий диск S, который является частью hello **SAP PR1** кластера группы и использует какой экземпляр ASCS/SCS hello, а toocluster узла.</span><span class="sxs-lookup"><span data-stu-id="e260a-1028">Assign hello shared disk drive S, which is part of hello **SAP PR1** cluster group, and which hello ASCS/SCS instance uses, toocluster node A.</span></span>

![На рисунке 61: Диспетчер отказоустойчивости кластеров: hello SAP < SID > Кластерная группа работает на узле кластера A][sap-ha-guide-figure-5000]

<span data-ttu-id="e260a-1030">_**На рисунке 61:** Диспетчер отказоустойчивости кластеров: hello SAP <*SID*> группы кластера выполняется на узле кластера A_</span><span class="sxs-lookup"><span data-stu-id="e260a-1030">_**Figure 61:** Failover Cluster Manager: hello SAP <*SID*> cluster group is running on cluster node A_</span></span>

<span data-ttu-id="e260a-1031">В hello SIOS DataKeeper управления и средство настройки вы увидите этому общему диску hello синхронно репликации данных из источника hello тома диск S на узле кластера toohello целевой том диск S на узле б. Например, реплицированных с **pr1-ascs-0 [10.0.0.40]** слишком**pr1-ascs-1 [10.0.0.41]**.</span><span class="sxs-lookup"><span data-stu-id="e260a-1031">In hello SIOS DataKeeper Management and Configuration tool, you can see that hello shared disk data is synchronously replicated from hello source volume drive S on cluster node A toohello target volume drive S on cluster node B. For example, it's replicated from **pr1-ascs-0 [10.0.0.40]** too**pr1-ascs-1 [10.0.0.41]**.</span></span>

![На рисунке 62: В SIOS DataKeeper реплицировать hello локального тома с узла кластера узла toocluster B][sap-ha-guide-figure-5001]

<span data-ttu-id="e260a-1033">_**На рисунке 62:** в SIOS DataKeeper реплицировать hello локального тома с узла кластера узла toocluster B_</span><span class="sxs-lookup"><span data-stu-id="e260a-1033">_**Figure 62:** In SIOS DataKeeper, replicate hello local volume from cluster node A toocluster node B_</span></span>

### <span data-ttu-id="e260a-1034"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>Переход с узла A toonode B</span><span class="sxs-lookup"><span data-stu-id="e260a-1034"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> Failover from node A toonode B</span></span>

1.  <span data-ttu-id="e260a-1035">Выберите один из этих параметров tooinitiate отработку отказа hello SAP <*SID*> группы кластера из кластера узел A toocluster б.</span><span class="sxs-lookup"><span data-stu-id="e260a-1035">Choose one of these options tooinitiate a failover of hello SAP <*SID*> cluster group from cluster node A toocluster node B:</span></span>
  - <span data-ttu-id="e260a-1036">воспользовавшись диспетчером отказоустойчивости кластеров;</span><span class="sxs-lookup"><span data-stu-id="e260a-1036">Use Failover Cluster Manager</span></span>  
  - <span data-ttu-id="e260a-1037">воспользовавшись командами PowerShell отказоустойчивого кластера;</span><span class="sxs-lookup"><span data-stu-id="e260a-1037">Use Failover Cluster PowerShell</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  <span data-ttu-id="e260a-1038">Перезапустите объект узла кластера в hello Windows гостевой операционной системы (при этом инициируется автоматический переход hello SAP <*SID*> группы кластера из узла A toonode B).</span><span class="sxs-lookup"><span data-stu-id="e260a-1038">Restart cluster node A within hello Windows guest operating system (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
3.  <span data-ttu-id="e260a-1039">Перезапустите A узел кластера от hello портал Azure (это инициирует автоматический переход из hello SAP <*SID*> группы кластера из узла A toonode B).</span><span class="sxs-lookup"><span data-stu-id="e260a-1039">Restart cluster node A from hello Azure portal (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
4.  <span data-ttu-id="e260a-1040">Перезапустите объект узла кластера с помощью Azure PowerShell (при этом инициируется автоматический переход hello SAP <*SID*> группы кластера из узла A toonode B).</span><span class="sxs-lookup"><span data-stu-id="e260a-1040">Restart cluster node A by using Azure PowerShell (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>

  <span data-ttu-id="e260a-1041">После отработки отказа hello SAP <*SID*> группы кластера выполняется на кластерном узле б. Например, он выполняется **pr1-ascs-1**.</span><span class="sxs-lookup"><span data-stu-id="e260a-1041">After failover, hello SAP <*SID*> cluster group is running on cluster node B. For example, it's running on **pr1-ascs-1**.</span></span>

  ![На рисунке 63: В диспетчере отказоустойчивости кластеров hello SAP < SID > Кластерная группа работает на узле кластера B][sap-ha-guide-figure-5002]

  <span data-ttu-id="e260a-1043">_**На рисунке 63**: В диспетчере отказоустойчивости кластеров, hello SAP <*SID*> группы кластера выполняется на кластерном узле B_</span><span class="sxs-lookup"><span data-stu-id="e260a-1043">_**Figure 63**: In Failover Cluster Manager, hello SAP <*SID*> cluster group is running on cluster node B_</span></span>

  <span data-ttu-id="e260a-1044">Hello общий диск теперь смонтирована в кластере узла B. SIOS DataKeeper является репликация данных из исходного тома диска S на диске кластера, узел B tootarget тома S на узле кластера, а. Например, он осуществляет репликацию с **pr1-ascs-1 [10.0.0.41]** слишком**pr1-ascs-0 [10.0.0.40]**.</span><span class="sxs-lookup"><span data-stu-id="e260a-1044">hello shared disk is now mounted on cluster node B. SIOS DataKeeper is replicating data from source volume drive S on cluster node B tootarget volume drive S on cluster node A. For example, it's replicating from **pr1-ascs-1 [10.0.0.41]** too**pr1-ascs-0 [10.0.0.40]**.</span></span>

  ![На рисунке 64: SIOS DataKeeper реплицирует hello локального тома из кластера узел B toocluster A][sap-ha-guide-figure-5003]

  <span data-ttu-id="e260a-1046">_**На рисунке 64:** SIOS DataKeeper реплицирует hello локального тома из кластера узел B toocluster A_</span><span class="sxs-lookup"><span data-stu-id="e260a-1046">_**Figure 64:** SIOS DataKeeper replicates hello local volume from cluster node B toocluster node A_</span></span>
