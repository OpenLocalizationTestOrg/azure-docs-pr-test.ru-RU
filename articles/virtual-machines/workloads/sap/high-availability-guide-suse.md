---
title: "высокий уровень доступности виртуальных машин для SAP NetWeaver в SUSE Linux Enterprise Server для приложений SAP aaaAzure | Документы Microsoft"
description: "Руководство по обеспечению высокой доступности для SAP NetWeaver на SUSE Linux Enterprise Server для приложений SAP"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: mssedusch
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
ms.date: 04/27/2017
ms.author: sedusch
ms.openlocfilehash: e944103df92d5ffec9196189f138e25972bea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a><span data-ttu-id="e8ae0-103">Руководство по обеспечению высокого уровня доступности виртуальных машин Azure для SAP NetWeaver на SUSE Linux Enterprise Server для приложений SAP</span><span class="sxs-lookup"><span data-stu-id="e8ae0-103">High availability for SAP NetWeaver on Azure VMs on SUSE Linux Enterprise Server for SAP applications</span></span>

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

[2205917]:https://launchpad.support.sap.com/#/notes/2205917
[1944799]:https://launchpad.support.sap.com/#/notes/1944799
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[1410736]:https://launchpad.support.sap.com/#/notes/1410736

[sap-swcenter]:https://support.sap.com/en/my-support/software-downloads.html

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[suse-drbd-guide]:https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha_techguides/book_sleha_techguides.html

[template-multisid-xscs]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged-md%2Fazuredeploy.json
[template-file-server]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-file-server-md%2Fazuredeploy.json

[sap-hana-ha]:sap-hana-high-availability.md

<span data-ttu-id="e8ae0-113">В этой статье описывается toodeploy hello виртуальных машин, Настройка hello виртуальных машин, установите framework кластера hello и установка высокой доступности системы SAP NetWeaver 7,50.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-113">This article describes how toodeploy hello virtual machines, configure hello virtual machines, install hello cluster framework and install a highly available SAP NetWeaver 7.50 system.</span></span>
<span data-ttu-id="e8ae0-114">В конфигурациях hello пример команды для установки и т. д. используется экземпляр ASCS номер 00, экземпляр ERS номер 02 и идентификатор системы SAP NWS.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-114">In hello example configurations, installation commands etc. ASCS instance number 00, ERS instance number 02 and SAP System ID NWS is used.</span></span> <span data-ttu-id="e8ae0-115">Hello имена hello ресурсов (например, виртуальных машин, виртуальных сетей), в примере hello предполагается, что используется hello [схождение выполнено шаблона] [ template-converged] с ресурсы hello toocreate NWS идентификатор системы SAP.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-115">hello names of hello resources (for example virtual machines, virtual networks) in hello example assume that you have used hello [converged template][template-converged] with SAP system ID NWS toocreate hello resources.</span></span>

<span data-ttu-id="e8ae0-116">Следующие примечания по SAP и документы сначала hello чтения</span><span class="sxs-lookup"><span data-stu-id="e8ae0-116">Read hello following SAP Notes and papers first</span></span>

* <span data-ttu-id="e8ae0-117">примечание к SAP [1928533], которое содержит:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-117">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="e8ae0-118">Список размеров виртуальных Машин Azure, которые поддерживаются для развертывания по SAP hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-118">List of Azure VM sizes that are supported for hello deployment of SAP software</span></span>
  * <span data-ttu-id="e8ae0-119">важные сведения о доступных ресурсах для каждого размера виртуальной машины Azure;</span><span class="sxs-lookup"><span data-stu-id="e8ae0-119">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="e8ae0-120">сведения о поддерживаемом программном обеспечении SAP и сочетаниях операционных систем и баз данных;</span><span class="sxs-lookup"><span data-stu-id="e8ae0-120">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="e8ae0-121">сведения о требуемой версии ядра SAP для Windows и Linux в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-121">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>

* <span data-ttu-id="e8ae0-122">примечание к SAP [2015553], в котором описываются предварительные требования к SAP при развертывании программного обеспечения SAP в Azure;</span><span class="sxs-lookup"><span data-stu-id="e8ae0-122">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="e8ae0-123">Примечание SAP [2205917] содержит рекомендуемые параметры ОС для SUSE Linux Enterprise Server для приложений SAP.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-123">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="e8ae0-124">Примечание SAP [1944799] содержит рекомендации для SAP HANA в SUSE Linux Enterprise Server для приложений SAP.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-124">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="e8ae0-125">примечание к SAP [2178632], содержащее подробные сведения обо всех доступных метриках мониторинга для SAP в Azure;</span><span class="sxs-lookup"><span data-stu-id="e8ae0-125">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="e8ae0-126">Примечание SAP [2191498] имеет hello требуемая версия агента узла SAP для Linux в Azure.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-126">SAP Note [2191498] has hello required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="e8ae0-127">примечание к SAP [2243692], содержащее сведения о лицензировании SAP в Linux в Azure;</span><span class="sxs-lookup"><span data-stu-id="e8ae0-127">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="e8ae0-128">примечание к SAP [1984787], содержащее общие сведения о SUSE Linux Enterprise Server 12;</span><span class="sxs-lookup"><span data-stu-id="e8ae0-128">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="e8ae0-129">Примечание SAP [1999351] имеет дополнительные диагностические сведения для hello расширение мониторинга Azure для SAP.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-129">SAP Note [1999351] has additional troubleshooting information for hello Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="e8ae0-130">[вики-сайт сообщества SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes), содержащий все необходимые примечания к SAP для Linux;</span><span class="sxs-lookup"><span data-stu-id="e8ae0-130">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="e8ae0-131">[SAP NetWeaver на виртуальных машинах Windows. Руководство по планированию и внедрению][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="e8ae0-131">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="e8ae0-132">[Развертывание программного обеспечения SAP на виртуальных машинах Linux в Azure (эта статья)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="e8ae0-132">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="e8ae0-133">[SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию СУБД][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="e8ae0-133">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="e8ae0-134">[Сценарий оптимизации производительности системной репликации SAP HANA][suse-hana-ha-guide]:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-134">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide]</span></span>  
  <span data-ttu-id="e8ae0-135">Справочник по Hello содержит все необходимые сведения tooset копирование репликации системы SAP HANA в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-135">hello guide contains all required information tooset up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="e8ae0-136">Используйте это руководство как основу.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-136">Use this guide as a baseline.</span></span>
* <span data-ttu-id="e8ae0-137">[Высокой доступные хранилища NFS с DRBD и Pacemaker] [ suse-drbd-guide] hello руководство содержит все необходимые сведения tooset высокой доступности сервер NFS.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-137">[Highly Available NFS Storage with DRBD and Pacemaker][suse-drbd-guide] hello guide contains all required information tooset up a highly available NFS server.</span></span> <span data-ttu-id="e8ae0-138">Используйте это руководство как основу.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-138">Use this guide as a baseline.</span></span>


## <a name="overview"></a><span data-ttu-id="e8ae0-139">Обзор</span><span class="sxs-lookup"><span data-stu-id="e8ae0-139">Overview</span></span>

<span data-ttu-id="e8ae0-140">tooachieve высокого уровня доступности и SAP NetWeaver требует NFS-сервера.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-140">tooachieve high availability, SAP NetWeaver requires an NFS server.</span></span> <span data-ttu-id="e8ae0-141">Hello NFS-сервер настраивается в отдельный кластер и может использоваться несколькими системами SAP.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-141">hello NFS server is configured in a separate cluster and can be used by multiple SAP systems.</span></span>

![Общие сведения о высоком уровне доступности SAP NetWeaver](./media/high-availability-guide-suse/img_001.png)

<span data-ttu-id="e8ae0-143">Hello NFS-сервера, SAP NetWeaver ASCS, SAP NetWeaver SCS, ющих Методов SAP NetWeaver и база данных SAP HANA hello с помощью виртуального имени узла и виртуальных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-143">hello NFS server, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver ERS and hello SAP HANA database use virtual hostname and virtual IP addresses.</span></span> <span data-ttu-id="e8ae0-144">В Azure подсистемы балансировки нагрузки является обязательным toouse виртуальный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-144">On Azure, a load balancer is required toouse a virtual IP address.</span></span> <span data-ttu-id="e8ae0-145">Hello ниже перечислены hello конфигурации подсистемы балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-145">hello following list shows hello configuration of hello load balancer.</span></span>

### <a name="nfs-server"></a><span data-ttu-id="e8ae0-146">Сервер NFS</span><span class="sxs-lookup"><span data-stu-id="e8ae0-146">NFS Server</span></span>
* <span data-ttu-id="e8ae0-147">Конфигурация внешнего интерфейса:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-147">Frontend configuration</span></span>
  * <span data-ttu-id="e8ae0-148">IP-адрес 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-148">IP address 10.0.0.4</span></span>
* <span data-ttu-id="e8ae0-149">Конфигурация серверной части:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-149">Backend configuration</span></span>
  * <span data-ttu-id="e8ae0-150">Подключенных сетевых интерфейсах tooprimary всех виртуальных машин, которые должны быть частью кластера NFS hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-150">Connected tooprimary network interfaces of all virtual machines that should be part of hello NFS cluster</span></span>
* <span data-ttu-id="e8ae0-151">Порт пробы:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-151">Probe Port</span></span>
  * <span data-ttu-id="e8ae0-152">порт 61000.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-152">Port 61000</span></span>
* <span data-ttu-id="e8ae0-153">Правила балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-153">Loadbalancing rules</span></span>
  * <span data-ttu-id="e8ae0-154">2049 TCP;</span><span class="sxs-lookup"><span data-stu-id="e8ae0-154">2049 TCP</span></span> 
  * <span data-ttu-id="e8ae0-155">2049 UDP.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-155">2049 UDP</span></span>

### <a name="ascs"></a><span data-ttu-id="e8ae0-156">(A)SCS</span><span class="sxs-lookup"><span data-stu-id="e8ae0-156">(A)SCS</span></span>
* <span data-ttu-id="e8ae0-157">Конфигурация внешнего интерфейса:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-157">Frontend configuration</span></span>
  * <span data-ttu-id="e8ae0-158">IP-адрес 10.0.0.10.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-158">IP address 10.0.0.10</span></span>
* <span data-ttu-id="e8ae0-159">Конфигурация серверной части:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-159">Backend configuration</span></span>
  * <span data-ttu-id="e8ae0-160">Сетевые интерфейсы подключенных tooprimary всех виртуальных машин, которые должны быть частью кластера hello (A) SCS/ющих Методов</span><span class="sxs-lookup"><span data-stu-id="e8ae0-160">Connected tooprimary network interfaces of all virtual machines that should be part of hello (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="e8ae0-161">Порт пробы:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-161">Probe Port</span></span>
  * <span data-ttu-id="e8ae0-162">порт 620**&lt;nr&gt;**.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-162">Port 620**&lt;nr&gt;**</span></span>
* <span data-ttu-id="e8ae0-163">Правила балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-163">Loadbalancing rules</span></span>
  * <span data-ttu-id="e8ae0-164">32**&lt;nr&gt;** TCP;</span><span class="sxs-lookup"><span data-stu-id="e8ae0-164">32**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="e8ae0-165">36**&lt;nr&gt;** TCP;</span><span class="sxs-lookup"><span data-stu-id="e8ae0-165">36**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="e8ae0-166">39**&lt;nr&gt;** TCP;</span><span class="sxs-lookup"><span data-stu-id="e8ae0-166">39**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="e8ae0-167">81**&lt;nr&gt;** TCP;</span><span class="sxs-lookup"><span data-stu-id="e8ae0-167">81**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="e8ae0-168">5**&lt;nr&gt;**13 TCP;</span><span class="sxs-lookup"><span data-stu-id="e8ae0-168">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="e8ae0-169">5**&lt;nr&gt;**14 TCP;</span><span class="sxs-lookup"><span data-stu-id="e8ae0-169">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="e8ae0-170">5**&lt;nr&gt;**16 TCP.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-170">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="ers"></a><span data-ttu-id="e8ae0-171">ERS</span><span class="sxs-lookup"><span data-stu-id="e8ae0-171">ERS</span></span>
* <span data-ttu-id="e8ae0-172">Конфигурация внешнего интерфейса:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-172">Frontend configuration</span></span>
  * <span data-ttu-id="e8ae0-173">IP-адрес 10.0.0.11.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-173">IP address 10.0.0.11</span></span>
* <span data-ttu-id="e8ae0-174">Конфигурация серверной части:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-174">Backend configuration</span></span>
  * <span data-ttu-id="e8ae0-175">Сетевые интерфейсы подключенных tooprimary всех виртуальных машин, которые должны быть частью кластера hello (A) SCS/ющих Методов</span><span class="sxs-lookup"><span data-stu-id="e8ae0-175">Connected tooprimary network interfaces of all virtual machines that should be part of hello (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="e8ae0-176">Порт пробы:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-176">Probe Port</span></span>
  * <span data-ttu-id="e8ae0-177">Порт 621**&lt;nr&gt;**.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-177">Port 621**&lt;nr&gt;**</span></span>
* <span data-ttu-id="e8ae0-178">Правила балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-178">Loadbalancing rules</span></span>
  * <span data-ttu-id="e8ae0-179">33**&lt;nr&gt;** TCP;</span><span class="sxs-lookup"><span data-stu-id="e8ae0-179">33**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="e8ae0-180">5**&lt;nr&gt;**13 TCP;</span><span class="sxs-lookup"><span data-stu-id="e8ae0-180">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="e8ae0-181">5**&lt;nr&gt;**14 TCP;</span><span class="sxs-lookup"><span data-stu-id="e8ae0-181">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="e8ae0-182">5**&lt;nr&gt;**16 TCP.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-182">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="sap-hana"></a><span data-ttu-id="e8ae0-183">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="e8ae0-183">SAP HANA</span></span>
* <span data-ttu-id="e8ae0-184">Конфигурация внешнего интерфейса:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-184">Frontend configuration</span></span>
  * <span data-ttu-id="e8ae0-185">IP-адрес 10.0.0.12.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-185">IP address 10.0.0.12</span></span>
* <span data-ttu-id="e8ae0-186">Конфигурация серверной части:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-186">Backend configuration</span></span>
  * <span data-ttu-id="e8ae0-187">Подключенных сетевых интерфейсах tooprimary всех виртуальных машин, которые должны быть частью кластера HANA hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-187">Connected tooprimary network interfaces of all virtual machines that should be part of hello HANA cluster</span></span>
* <span data-ttu-id="e8ae0-188">Порт пробы:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-188">Probe Port</span></span>
  * <span data-ttu-id="e8ae0-189">порт 625**&lt;nr&gt;**.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-189">Port 625**&lt;nr&gt;**</span></span>
* <span data-ttu-id="e8ae0-190">Правила балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-190">Loadbalancing rules</span></span>
  * <span data-ttu-id="e8ae0-191">3**&lt;nr&gt;**15 TCP;</span><span class="sxs-lookup"><span data-stu-id="e8ae0-191">3**&lt;nr&gt;**15 TCP</span></span>
  * <span data-ttu-id="e8ae0-192">3**&lt;nr&gt;**17 TCP.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-192">3**&lt;nr&gt;**17 TCP</span></span>

## <a name="setting-up-a-highly-available-nfs-server"></a><span data-ttu-id="e8ae0-193">Настройка сервера NFS высокой доступности</span><span class="sxs-lookup"><span data-stu-id="e8ae0-193">Setting up a highly available NFS server</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="e8ae0-194">Развертывание Linux</span><span class="sxs-lookup"><span data-stu-id="e8ae0-194">Deploying Linux</span></span>

<span data-ttu-id="e8ae0-195">Hello Azure Marketplace содержит изображение для SUSE Linux Enterprise Server 12 приложений SAP, которые используются toodeploy новых виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-195">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use toodeploy new virtual machines.</span></span>
<span data-ttu-id="e8ae0-196">Можно использовать один из шаблонов hello быстрого запуска на github toodeploy все необходимые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-196">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="e8ae0-197">шаблон Hello развертывает hello виртуальных машин, подсистемы балансировки нагрузки hello, доступности, и т. д. Выполните эти шаги toodeploy hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-197">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="e8ae0-198">Откройте hello [шаблона сервера SAP файл] [ template-file-server] в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="e8ae0-198">Open hello [SAP file server template][template-file-server] in hello Azure portal</span></span>   
1. <span data-ttu-id="e8ae0-199">Введите следующие параметры hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-199">Enter hello following parameters</span></span>
   1. <span data-ttu-id="e8ae0-200">Префикс ресурса</span><span class="sxs-lookup"><span data-stu-id="e8ae0-200">Resource Prefix</span></span>  
      <span data-ttu-id="e8ae0-201">Введите префикс hello требуется toouse.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-201">Enter hello prefix you want toouse.</span></span> <span data-ttu-id="e8ae0-202">Hello значение используется как префикс для hello ресурсы, которые развертываются.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-202">hello value is used as a prefix for hello resources that are deployed.</span></span>
   2. <span data-ttu-id="e8ae0-203">Тип ОС</span><span class="sxs-lookup"><span data-stu-id="e8ae0-203">Os Type</span></span>  
      <span data-ttu-id="e8ae0-204">Выберите один из hello ОС Linux.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-204">Select one of hello Linux distributions.</span></span> <span data-ttu-id="e8ae0-205">Для этого примера выберите SLES 12.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-205">For this example, select SLES 12</span></span>
   3. <span data-ttu-id="e8ae0-206">Имя пользователя и пароль администратора</span><span class="sxs-lookup"><span data-stu-id="e8ae0-206">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="e8ae0-207">Создать нового пользователя, можно использовать toolog на компьютере toohello.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-207">A new user is created that can be used toolog on toohello machine.</span></span>
   4. <span data-ttu-id="e8ae0-208">Идентификатор подсети</span><span class="sxs-lookup"><span data-stu-id="e8ae0-208">Subnet Id</span></span>  
      <span data-ttu-id="e8ae0-209">Идентификатор Hello hello подсети toowhich hello виртуальных машин должен быть подключен к.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-209">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span> <span data-ttu-id="e8ae0-210">Оставьте пустым, если требуется toocreate новую виртуальную сеть или выберите подсеть hello VPN или Express Route виртуальной сети tooconnect hello виртуальной машины tooyour в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-210">Leave empty if you want toocreate a new virtual network or select hello subnet of your VPN or Express Route virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="e8ae0-211">Идентификатор Hello обычно выглядит /subscriptions/**&lt;код_подписки&gt;**/resourceGroups/**&lt;имя группы ресурсов&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;имя виртуальной сети&gt;**/subnets/**&lt;имя подсети&gt;**</span><span class="sxs-lookup"><span data-stu-id="e8ae0-211">hello ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="e8ae0-212">Установка</span><span class="sxs-lookup"><span data-stu-id="e8ae0-212">Installation</span></span>

<span data-ttu-id="e8ae0-213">Hello следующие элементы имеют префикс либо **[A]** -узлы применимо tooall **[1]** -только применимые toonode 1 или **[2]** -только применимые toonode 2.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-213">hello following items are prefixed with either **[A]** - applicable tooall nodes, **[1]** - only applicable toonode 1 or **[2]** - only applicable toonode 2.</span></span>

1. <span data-ttu-id="e8ae0-214">**[A]** Обновите SLES.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-214">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="e8ae0-215">**[1]** Включите доступ по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-215">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="e8ae0-216">**[2]** Включите доступ по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-216">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="e8ae0-217">**[1]** Включите доступ по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-217">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="e8ae0-218">**[A]** Установите расширение для обеспечения высокого уровня доступности.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-218">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="e8ae0-219">**[A]** Установите разрешения имен.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-219">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="e8ae0-220">Можно использовать DNS-сервер или измените hello/etc/hosts, на всех узлах.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-220">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="e8ae0-221">В этом примере показано, как toouse hello файл/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-221">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="e8ae0-222">Замените hello IP-адрес и имя узла hello в hello, следующие команды</span><span class="sxs-lookup"><span data-stu-id="e8ae0-222">Replace hello IP address and hello hostname in hello following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="e8ae0-223">Вставьте следующие строки слишком/и т. д/узлы hello.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-223">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="e8ae0-224">Изменение среды toomatch hello IP адрес и имя узла</span><span class="sxs-lookup"><span data-stu-id="e8ae0-224">Change hello IP address and hostname toomatch your environment</span></span>   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. <span data-ttu-id="e8ae0-225">**[1]** Установите кластер.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-225">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="e8ae0-226">**[2]**  Добавить узел toocluster</span><span class="sxs-lookup"><span data-stu-id="e8ae0-226">**[2]** Add node toocluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="e8ae0-227">**[A]**  Toohello пароль hacluster изменить пароль</span><span class="sxs-lookup"><span data-stu-id="e8ae0-227">**[A]** Change hacluster password toohello same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="e8ae0-228">**[A]**  Настройка corosync toouse других транспорта и добавьте набору узлов.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-228">**[A]** Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="e8ae0-229">Иначе кластер не будет работать.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-229">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="e8ae0-230">Добавьте следующие полужирным содержимого toohello файл hello.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-230">Add hello following bold content toohello file.</span></span>
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>prod-nfs-0</b>
      ring0_addr:10.0.0.5
     }
     node {
      # IP address of <b>prod-nfs-1</b>
      ring0_addr:10.0.0.6
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   <span data-ttu-id="e8ae0-231">Затем перезапустите службу corosync hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-231">Then restart hello corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="e8ae0-232">**[A]** Установите компоненты DRBD.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-232">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="e8ae0-233">**[A]**  Создание раздела для hello drbd устройства</span><span class="sxs-lookup"><span data-stu-id="e8ae0-233">**[A]** Create a partition for hello drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="e8ae0-234">**[A]** Создайте конфигурации LVM.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-234">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. <span data-ttu-id="e8ae0-235">**[A]**  Создание hello NFS drbd устройства</span><span class="sxs-lookup"><span data-stu-id="e8ae0-235">**[A]** Create hello NFS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   <span data-ttu-id="e8ae0-236">Вставка hello конфигурации для нового устройства drbd hello и выход</span><span class="sxs-lookup"><span data-stu-id="e8ae0-236">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_nfs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>prod-nfs-0</b> {
         address   <b>10.0.0.5</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
      on <b>prod-nfs-1</b> {
         address   <b>10.0.0.6</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="e8ae0-237">Создание устройства drbd hello и запустите ее</span><span class="sxs-lookup"><span data-stu-id="e8ae0-237">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="e8ae0-238">**[1]** Пропустите начальную синхронизацию.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-238">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="e8ae0-239">**[1]**  Основного узла набора hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-239">**[1]** Set hello primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="e8ae0-240">**[1]**  Подождите, пока не синхронизируются новых устройств drbd hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-240">**[1]** Wait until hello new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="e8ae0-241">**[1]**  Создания drbd устройств hello файловых систем</span><span class="sxs-lookup"><span data-stu-id="e8ae0-241">**[1]** Create file systems on hello drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="e8ae0-242">Настройка платформы кластера</span><span class="sxs-lookup"><span data-stu-id="e8ae0-242">Configure Cluster Framework</span></span>

1. <span data-ttu-id="e8ae0-243">**[1]**  Изменить параметры по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-243">**[1]** Change hello default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="e8ae0-244">**[1]**  Toohello конфигурации кластера NFS drbd добавить hello устройства</span><span class="sxs-lookup"><span data-stu-id="e8ae0-244">**[1]** Add hello NFS drbd device toohello cluster configuration</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_nfs \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_nfs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_nfs drbd_<b>NWS</b>_nfs \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="e8ae0-245">**[1]**  Создание hello NFS-сервера</span><span class="sxs-lookup"><span data-stu-id="e8ae0-245">**[1]** Create hello NFS server</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="e8ae0-246">**[1]**  Создать ресурсы файловой системы NFS hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-246">**[1]** Create hello NFS File System resources</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive fs_<b>NWS</b>_sapmnt \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/srv/nfs/<b>NWS</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# group g-<b>NWS</b>_nfs fs_<b>NWS</b>_sapmnt

   crm(live)configure# order o-<b>NWS</b>_drbd_before_nfs inf: \
     ms-drbd_<b>NWS</b>_nfs:promote g-<b>NWS</b>_nfs:start
   
   crm(live)configure# colocation col-<b>NWS</b>_nfs_on_drbd inf: \
     g-<b>NWS</b>_nfs ms-drbd_<b>NWS</b>_nfs:Master

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="e8ae0-247">**[1]**  Создание экспортирует NFS hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-247">**[1]** Create hello NFS exports</span></span>

   <pre><code>
   sudo mkdir /srv/nfs/<b>NWS</b>/sidsys
   sudo mkdir /srv/nfs/<b>NWS</b>/sapmntsid
   sudo mkdir /srv/nfs/<b>NWS</b>/trans

   sudo crm configure

   crm(live)configure# primitive exportfs_<b>NWS</b> \
     ocf:heartbeat:exportfs \
     params directory="/srv/nfs/<b>NWS</b>" \
     options="rw,no_root_squash" \
     clientspec="*" fsid=0 \
     wait_for_leasetime_on_stop=true \
     op monitor interval="30s"

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add exportfs_<b>NWS</b>

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="e8ae0-248">**[1]**  Создание виртуального IP-ресурс и зонд работоспособности для hello внутренняя Подсистема балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="e8ae0-248">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive vip_<b>NWS</b>_nfs IPaddr2 \
     params ip=<b>10.0.0.4</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_nfs anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 610<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add nc_<b>NWS</b>_nfs
   crm(live)configure# modgroup g-<b>NWS</b>_nfs add vip_<b>NWS</b>_nfs

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

### <a name="create-stonith-device"></a><span data-ttu-id="e8ae0-249">Создание устройства STONITH</span><span class="sxs-lookup"><span data-stu-id="e8ae0-249">Create STONITH device</span></span>

<span data-ttu-id="e8ae0-250">Hello STONITH устройство использует tooauthorize участника-службы для Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-250">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="e8ae0-251">Выполните эти шаги toocreate участника службы.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-251">Follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="e8ae0-252">Go слишком<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="e8ae0-252">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="e8ae0-253">Привет открыть колонку Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e8ae0-253">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="e8ae0-254">Go tooProperties и запишите hello идентификатор каталога. Это hello **ИД клиента**.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-254">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="e8ae0-255">Щелкните "Регистрация приложений".</span><span class="sxs-lookup"><span data-stu-id="e8ae0-255">Click App registrations</span></span>
1. <span data-ttu-id="e8ae0-256">Нажмите "Добавить"</span><span class="sxs-lookup"><span data-stu-id="e8ae0-256">Click Add</span></span>
1. <span data-ttu-id="e8ae0-257">Введите имя, выберите тип приложения "Веб-приложения или API", введите URL-адрес входа (например. http://localhost) и нажмите кнопку "Создать".</span><span class="sxs-lookup"><span data-stu-id="e8ae0-257">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="e8ae0-258">Hello URL-адрес входа не используется и может быть любой допустимый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="e8ae0-258">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="e8ae0-259">Здравствуйте, выберите новое приложение и щелкните на вкладке Параметры hello ключи</span><span class="sxs-lookup"><span data-stu-id="e8ae0-259">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="e8ae0-260">Введите описание нового ключа, выберите "Срок действия не ограничен" и нажмите кнопку "Сохранить".</span><span class="sxs-lookup"><span data-stu-id="e8ae0-260">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="e8ae0-261">Запишите значение hello.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-261">Write down hello Value.</span></span> <span data-ttu-id="e8ae0-262">Он используется как hello **пароль** для hello участника-службы</span><span class="sxs-lookup"><span data-stu-id="e8ae0-262">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="e8ae0-263">Запишите hello идентификатор приложения. Он используется как hello username (**идентификатора входа** в hello действия) для hello участника-службы</span><span class="sxs-lookup"><span data-stu-id="e8ae0-263">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="e8ae0-264">Hello участника-службы не имеет разрешения tooaccess ресурсам Azure по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-264">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="e8ae0-265">Необходимые субъекта-службы разрешений toogive hello toostart и остановить (освободить) всех виртуальных машин кластера hello.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-265">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="e8ae0-266">Go toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="e8ae0-266">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="e8ae0-267">Здравствуйте, откройте колонку все ресурсы</span><span class="sxs-lookup"><span data-stu-id="e8ae0-267">Open hello All resources blade</span></span>
1. <span data-ttu-id="e8ae0-268">Выберите виртуальную машину, hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-268">Select hello virtual machine</span></span>
1. <span data-ttu-id="e8ae0-269">Выберите "Управление доступом (IAM)".</span><span class="sxs-lookup"><span data-stu-id="e8ae0-269">Click Access control (IAM)</span></span>
1. <span data-ttu-id="e8ae0-270">Нажмите "Добавить"</span><span class="sxs-lookup"><span data-stu-id="e8ae0-270">Click Add</span></span>
1. <span data-ttu-id="e8ae0-271">Выберите роль hello владельца</span><span class="sxs-lookup"><span data-stu-id="e8ae0-271">Select hello role Owner</span></span>
1. <span data-ttu-id="e8ae0-272">Введите имя приложения hello, созданной выше hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-272">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="e8ae0-273">Нажмите кнопку "ОК"</span><span class="sxs-lookup"><span data-stu-id="e8ae0-273">Click OK</span></span>

#### <a name="1-create-hello-stonith-devices"></a><span data-ttu-id="e8ae0-274">**[1]**  Создайте hello STONITH устройства</span><span class="sxs-lookup"><span data-stu-id="e8ae0-274">**[1]** Create hello STONITH devices</span></span>

<span data-ttu-id="e8ae0-275">После редактирования hello разрешения для виртуальных машин hello hello STONITH устройства можно настроить в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-275">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a><span data-ttu-id="e8ae0-276">**[1]**  Включить использование hello STONITH устройства</span><span class="sxs-lookup"><span data-stu-id="e8ae0-276">**[1]** Enable hello use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a><span data-ttu-id="e8ae0-277">Настройка (A)SCS</span><span class="sxs-lookup"><span data-stu-id="e8ae0-277">Setting up (A)SCS</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="e8ae0-278">Развертывание Linux</span><span class="sxs-lookup"><span data-stu-id="e8ae0-278">Deploying Linux</span></span>

<span data-ttu-id="e8ae0-279">Hello Azure Marketplace содержит изображение для SUSE Linux Enterprise Server 12 приложений SAP, которые используются toodeploy новых виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-279">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use toodeploy new virtual machines.</span></span> <span data-ttu-id="e8ae0-280">образ marketplace Hello содержит hello ресурсов агента для SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-280">hello marketplace image contains hello resource agent for SAP NetWeaver.</span></span>

<span data-ttu-id="e8ae0-281">Можно использовать один из шаблонов hello быстрого запуска на github toodeploy все необходимые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-281">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="e8ae0-282">шаблон Hello развертывает hello виртуальных машин, подсистемы балансировки нагрузки hello, доступности, и т. д. Выполните эти шаги toodeploy hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-282">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="e8ae0-283">Откройте hello [ASCS/SCS Multi SID шаблона] [ template-multisid-xscs] или hello [схождение выполнено шаблона] [ template-converged] ASCS/SCS шаблона на hello Azure портала hello Создает hello балансировки нагрузки правила для SAP NetWeaver ASCS/SCS hello и экземпляров ющих Методов (Linux), тогда как hello схождением шаблон также создает правила балансировки нагрузки hello для базы данных (например, Microsoft SQL Server или SAP HANA).</span><span class="sxs-lookup"><span data-stu-id="e8ae0-283">Open hello [ASCS/SCS Multi SID template][template-multisid-xscs] or hello [converged template][template-converged] on hello Azure portal hello ASCS/SCS template only creates hello load-balancing rules for hello SAP NetWeaver ASCS/SCS and ERS (Linux only) instances whereas hello converged template also creates hello load-balancing rules for a database (for example Microsoft SQL Server or SAP HANA).</span></span> <span data-ttu-id="e8ae0-284">Если планируется tooinstall системы на основе SAP NetWeaver, а также базы данных hello tooinstall на hello одной машины, используйте hello [схождение выполнено шаблона][template-converged].</span><span class="sxs-lookup"><span data-stu-id="e8ae0-284">If you plan tooinstall an SAP NetWeaver based system and you also want tooinstall hello database on hello same machines, use hello [converged template][template-converged].</span></span>
1. <span data-ttu-id="e8ae0-285">Введите следующие параметры hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-285">Enter hello following parameters</span></span>
   1. <span data-ttu-id="e8ae0-286">Префикс ресурса (только шаблон нескольких ИД безопасности ASCS/SCS).</span><span class="sxs-lookup"><span data-stu-id="e8ae0-286">Resource Prefix (ASCS/SCS Multi SID template only)</span></span>  
      <span data-ttu-id="e8ae0-287">Введите префикс hello требуется toouse.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-287">Enter hello prefix you want toouse.</span></span> <span data-ttu-id="e8ae0-288">Hello значение используется как префикс для hello ресурсы, которые развертываются.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-288">hello value is used as a prefix for hello resources that are deployed.</span></span>
   3. <span data-ttu-id="e8ae0-289">Идентификатор системы SAP (только конвергированный шаблон).</span><span class="sxs-lookup"><span data-stu-id="e8ae0-289">Sap System Id (converged template only)</span></span>  
      <span data-ttu-id="e8ae0-290">Введите системы SAP hello идентификатор hello требуется tooinstall системы SAP.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-290">Enter hello SAP system Id of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="e8ae0-291">Hello идентификатор используется в качестве префикса для hello ресурсы, которые развертываются.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-291">hello Id is used as a prefix for hello resources that are deployed.</span></span>
   4. <span data-ttu-id="e8ae0-292">Тип стека</span><span class="sxs-lookup"><span data-stu-id="e8ae0-292">Stack Type</span></span>  
      <span data-ttu-id="e8ae0-293">Выберите тип стека SAP NetWeaver hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-293">Select hello SAP NetWeaver stack type</span></span>
   5. <span data-ttu-id="e8ae0-294">Тип ОС</span><span class="sxs-lookup"><span data-stu-id="e8ae0-294">Os Type</span></span>  
      <span data-ttu-id="e8ae0-295">Выберите один из hello ОС Linux.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-295">Select one of hello Linux distributions.</span></span> <span data-ttu-id="e8ae0-296">Для этого примера выберите SLES 12 BYOS.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-296">For this example, select SLES 12 BYOS</span></span>
   6. <span data-ttu-id="e8ae0-297">Тип базы данных.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-297">Db Type</span></span>  
      <span data-ttu-id="e8ae0-298">Выберите HANA.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-298">Select HANA</span></span>
   7. <span data-ttu-id="e8ae0-299">Размер системы SAP</span><span class="sxs-lookup"><span data-stu-id="e8ae0-299">Sap System Size</span></span>  
      <span data-ttu-id="e8ae0-300">предоставляет Hello объем SAPS hello новую систему.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-300">hello amount of SAPS hello new system provides.</span></span> <span data-ttu-id="e8ae0-301">Если вы не уверены, сколько SAPS hello система требует, попросите вашего партнера технологии SAP или системные интеграторы</span><span class="sxs-lookup"><span data-stu-id="e8ae0-301">If you are not sure how many SAPS hello system requires, please ask your SAP Technology Partner or System Integrator</span></span>
   8. <span data-ttu-id="e8ae0-302">Доступность системы</span><span class="sxs-lookup"><span data-stu-id="e8ae0-302">System Availability</span></span>  
      <span data-ttu-id="e8ae0-303">Выберите высокую доступность</span><span class="sxs-lookup"><span data-stu-id="e8ae0-303">Select HA</span></span>
   9. <span data-ttu-id="e8ae0-304">Имя пользователя и пароль администратора</span><span class="sxs-lookup"><span data-stu-id="e8ae0-304">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="e8ae0-305">Создать нового пользователя, можно использовать toolog на компьютере toohello.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-305">A new user is created that can be used toolog on toohello machine.</span></span>
   10. <span data-ttu-id="e8ae0-306">Идентификатор подсети</span><span class="sxs-lookup"><span data-stu-id="e8ae0-306">Subnet Id</span></span>  
   <span data-ttu-id="e8ae0-307">Идентификатор Hello hello подсети toowhich hello виртуальных машин должен быть подключен к.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-307">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span>  <span data-ttu-id="e8ae0-308">Оставьте пустым, если требуется, чтобы toocreate новую виртуальную сеть или выберите hello одной подсети, используемые или созданный как часть развертывания сервера для NFS hello.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-308">Leave empty if you want toocreate a new virtual network or select hello same subnet that you used or created as part of hello NFS server deployment.</span></span> <span data-ttu-id="e8ae0-309">Идентификатор Hello обычно выглядит /subscriptions/**&lt;код_подписки&gt;**/resourceGroups/**&lt;имя группы ресурсов&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;имя виртуальной сети&gt;**/subnets/**&lt;имя подсети&gt;**</span><span class="sxs-lookup"><span data-stu-id="e8ae0-309">hello ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="e8ae0-310">Установка</span><span class="sxs-lookup"><span data-stu-id="e8ae0-310">Installation</span></span>

<span data-ttu-id="e8ae0-311">Hello следующие элементы имеют префикс либо **[A]** -узлы применимо tooall **[1]** -только применимые toonode 1 или **[2]** -только применимые toonode 2.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-311">hello following items are prefixed with either **[A]** - applicable tooall nodes, **[1]** - only applicable toonode 1 or **[2]** - only applicable toonode 2.</span></span>

1. <span data-ttu-id="e8ae0-312">**[A]** Обновите SLES.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-312">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="e8ae0-313">**[1]** Включите доступ по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-313">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="e8ae0-314">**[2]** Включите доступ по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-314">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="e8ae0-315">**[1]** Включите доступ по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-315">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="e8ae0-316">**[A]** Установите расширение для обеспечения высокого уровня доступности.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-316">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="e8ae0-317">**[A]** Обновите агенты ресурсов SAP.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-317">**[A]** Update SAP resource agents</span></span>  
   
   <span data-ttu-id="e8ae0-318">Исправление для hello агентов ресурсов пакета — необходимые toouse hello новой конфигурации, описанной в этой статье.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-318">A patch for hello resource-agents package is required toouse hello new configuration, that is described in this article.</span></span> <span data-ttu-id="e8ae0-319">Можно проверить, если уже установлено исправление hello с hello следующую команду</span><span class="sxs-lookup"><span data-stu-id="e8ae0-319">You can check, if hello patch is already installed with hello following command</span></span>

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   <span data-ttu-id="e8ae0-320">Hello вывода должен быть аналогичен</span><span class="sxs-lookup"><span data-stu-id="e8ae0-320">hello output should be similar to</span></span>

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   <span data-ttu-id="e8ae0-321">Если команда grep hello не удается найти параметр IS_ERS hello, необходимо исправление tooinstall hello, перечисленные на [hello SUSE страницу загрузки](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span><span class="sxs-lookup"><span data-stu-id="e8ae0-321">If hello grep command does not find hello IS_ERS parameter, you need tooinstall hello patch listed on [hello SUSE download page](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span></span>

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. <span data-ttu-id="e8ae0-322">**[A]** Установите разрешения имен.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-322">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="e8ae0-323">Можно использовать DNS-сервер или измените hello/etc/hosts, на всех узлах.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-323">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="e8ae0-324">В этом примере показано, как toouse hello файл/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-324">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="e8ae0-325">Замените hello IP-адрес и имя узла hello в hello, следующие команды</span><span class="sxs-lookup"><span data-stu-id="e8ae0-325">Replace hello IP address and hello hostname in hello following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="e8ae0-326">Вставьте следующие строки слишком/и т. д/узлы hello.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-326">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="e8ae0-327">Изменение среды toomatch hello IP адрес и имя узла</span><span class="sxs-lookup"><span data-stu-id="e8ae0-327">Change hello IP address and hostname toomatch your environment</span></span>   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   </code></pre>

1. <span data-ttu-id="e8ae0-328">**[1]** Установите кластер.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-328">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="e8ae0-329">**[2]**  Добавить узел toocluster</span><span class="sxs-lookup"><span data-stu-id="e8ae0-329">**[2]** Add node toocluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="e8ae0-330">**[A]**  Toohello пароль hacluster изменить пароль</span><span class="sxs-lookup"><span data-stu-id="e8ae0-330">**[A]** Change hacluster password toohello same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="e8ae0-331">**[A]**  Настройка corosync toouse других транспорта и добавьте набору узлов.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-331">**[A]** Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="e8ae0-332">Иначе кластер не будет работать.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-332">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="e8ae0-333">Добавьте следующие полужирным содержимого toohello файл hello.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-333">Add hello following bold content toohello file.</span></span>
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>nws-cl-0</b>
      ring0_addr:     10.0.0.14
     }
     node {
      # IP address of <b>nws-cl-1</b>
      ring0_addr:     10.0.0.13
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   <span data-ttu-id="e8ae0-334">Затем перезапустите службу corosync hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-334">Then restart hello corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="e8ae0-335">**[A]** Установите компоненты DRBD.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-335">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="e8ae0-336">**[A]**  Создание раздела для hello drbd устройства</span><span class="sxs-lookup"><span data-stu-id="e8ae0-336">**[A]** Create a partition for hello drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="e8ae0-337">**[A]** Создайте конфигурации LVM.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-337">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. <span data-ttu-id="e8ae0-338">**[A]**  Создание hello SCS drbd устройства</span><span class="sxs-lookup"><span data-stu-id="e8ae0-338">**[A]** Create hello SCS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   <span data-ttu-id="e8ae0-339">Вставка hello конфигурации для нового устройства drbd hello и выход</span><span class="sxs-lookup"><span data-stu-id="e8ae0-339">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_ascs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="e8ae0-340">Создание устройства drbd hello и запустите ее</span><span class="sxs-lookup"><span data-stu-id="e8ae0-340">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. <span data-ttu-id="e8ae0-341">**[A]**  Создание hello ющих Методов drbd устройства</span><span class="sxs-lookup"><span data-stu-id="e8ae0-341">**[A]** Create hello ERS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   <span data-ttu-id="e8ae0-342">Вставка hello конфигурации для нового устройства drbd hello и выход</span><span class="sxs-lookup"><span data-stu-id="e8ae0-342">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_ers {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="e8ae0-343">Создание устройства drbd hello и запустите ее</span><span class="sxs-lookup"><span data-stu-id="e8ae0-343">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="e8ae0-344">**[1]** Пропустите начальную синхронизацию.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-344">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="e8ae0-345">**[1]**  Основного узла набора hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-345">**[1]** Set hello primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="e8ae0-346">**[1]**  Подождите, пока не синхронизируются новых устройств drbd hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-346">**[1]** Wait until hello new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:93991268 nr:0 dw:93991268 dr:93944920 al:383 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 1: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:6047920 nr:0 dw:6047920 dr:6039112 al:34 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 2: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:5142732 nr:0 dw:5142732 dr:5133924 al:30 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="e8ae0-347">**[1]**  Создания drbd устройств hello файловых систем</span><span class="sxs-lookup"><span data-stu-id="e8ae0-347">**[1]** Create file systems on hello drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="e8ae0-348">Настройка платформы кластера</span><span class="sxs-lookup"><span data-stu-id="e8ae0-348">Configure Cluster Framework</span></span>

<span data-ttu-id="e8ae0-349">**[1]**  Изменить параметры по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-349">**[1]** Change hello default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a><span data-ttu-id="e8ae0-350">Подготовка к установке SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="e8ae0-350">Prepare for SAP NetWeaver installation</span></span>

1. <span data-ttu-id="e8ae0-351">**[A]**  Hello создание общих каталогов</span><span class="sxs-lookup"><span data-stu-id="e8ae0-351">**[A]** Create hello shared directories</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. <span data-ttu-id="e8ae0-352">**[A]** Настройте autofs.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-352">**[A]** Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="e8ae0-353">Создайте файл со следующим текстом:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-353">Create a file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   <span data-ttu-id="e8ae0-354">Перезапустите toomount autofs hello новые общие папки</span><span class="sxs-lookup"><span data-stu-id="e8ae0-354">Restart autofs toomount hello new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="e8ae0-355">**[A]** Настройте файл подкачки.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-355">**[A]** Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="e8ae0-356">Перезапустите hello агента tooactivate hello изменений</span><span class="sxs-lookup"><span data-stu-id="e8ae0-356">Restart hello Agent tooactivate hello change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a><span data-ttu-id="e8ae0-357">Установка SAP NetWeaver ASCS/ERS</span><span class="sxs-lookup"><span data-stu-id="e8ae0-357">Installing SAP NetWeaver ASCS/ERS</span></span>

1. <span data-ttu-id="e8ae0-358">**[1]**  Создание виртуального IP-ресурс и зонд работоспособности для hello внутренняя Подсистема балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="e8ae0-358">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm node standby <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ASCS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ascs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ASCS drbd_<b>NWS</b>_ASCS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ASCS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/usr/sap/<b>NWS</b>/ASCS<b>00</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ASCS IPaddr2 \
     params ip=<b>10.0.0.10</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ASCS anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 620<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0
   
   crm(live)configure# group g-<b>NWS</b>_ASCS nc_<b>NWS</b>_ASCS vip_<b>NWS</b>_ASCS fs_<b>NWS</b>_ASCS \
      meta resource-stickiness=3000

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ASCS inf: \
     ms-drbd_<b>NWS</b>_ASCS:promote g-<b>NWS</b>_ASCS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ASCS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ASCS:Master g-<b>NWS</b>_ASCS
   
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   <span data-ttu-id="e8ae0-359">Убедитесь, что состояние кластера hello в норме и что запущены все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-359">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="e8ae0-360">Не важно, на какие ресурсы узла hello выполняются.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-360">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Node nws-cl-1: standby
   # <b>Online: [ nws-cl-0 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      Stopped: [ nws-cl-1 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   </code></pre>

1. <span data-ttu-id="e8ae0-361">**[1]** Установите SAP NetWeaver ASCS.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-361">**[1]** Install SAP NetWeaver ASCS</span></span>  

   <span data-ttu-id="e8ae0-362">Установите SAP NetWeaver ASCS в качестве корневого на первом узле hello, с помощью виртуального имени узла, например сопоставляет IP-адрес toohello hello конфигурации переднего плана подсистемы балансировки нагрузки для hello ASCS <b>nws ascs</b>, <b>10.0.0.10</b>и hello номера экземпляра, который использовался для hello пробы подсистемы балансировки нагрузки hello, например <b>00</b>.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-362">Install SAP NetWeaver ASCS as root on hello first node using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello ASCS for example <b>nws-ascs</b>, <b>10.0.0.10</b> and hello instance number that you used for hello probe of hello load balancer for example <b>00</b>.</span></span>

   <span data-ttu-id="e8ae0-363">Можно использовать hello sapinst параметр SAPINST_REMOTE_ACCESS_USER tooallow toosapinst tooconnect непривилегированным пользователем.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-363">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="e8ae0-364">**[1]**  Создание виртуального IP-ресурс и зонд работоспособности для hello внутренняя Подсистема балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="e8ae0-364">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm node standby <b>nws-cl-0</b>
   sudo crm node online <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ERS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ers" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ERS drbd_<b>NWS</b>_ERS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ERS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd1 \
     directory=/usr/sap/<b>NWS</b>/ERS<b>02</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ERS IPaddr2 \
     params ip=<b>10.0.0.11</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ERS anything \
    params binfile="/usr/bin/nc" cmdline_options="-l -k 621<b>02</b>" \
    op monitor timeout=20s interval=10 depth=0

   crm(live)configure# group g-<b>NWS</b>_ERS nc_<b>NWS</b>_ERS vip_<b>NWS</b>_ERS fs_<b>NWS</b>_ERS

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ERS inf: \
     ms-drbd_<b>NWS</b>_ERS:promote g-<b>NWS</b>_ERS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ERS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ERS:Master g-<b>NWS</b>_ERS
   
   crm(live)configure# commit
   # WARNING: Resources nc_NWS_ASCS,nc_NWS_ERS,nc_NWS_nfs violate uniqueness for parameter "binfile": "/usr/bin/nc"
   # Do you still want toocommit (y/n)? y

   crm(live)configure# exit
   
   </code></pre>
 
   <span data-ttu-id="e8ae0-365">Убедитесь, что состояние кластера hello в норме и что запущены все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-365">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="e8ae0-366">Не важно, на какие ресурсы узла hello выполняются.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-366">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Node <b>nws-cl-0: standby</b>
   # <b>Online: [ nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   </code></pre>

1. <span data-ttu-id="e8ae0-367">**[2]** Установите SAP NetWeaver ERS.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-367">**[2]** Install SAP NetWeaver ERS</span></span>  

   <span data-ttu-id="e8ae0-368">Установите ющих Методов SAP NetWeaver в качестве корневого на второй узел hello, с помощью виртуального имени узла, которое сопоставляет IP-адрес toohello hello конфигурации переднего плана подсистемы балансировки нагрузки для hello ющих Методов, например <b>ющих методов nws</b>, <b>10.0.0.11</b> и hello номера экземпляра, который использовался для hello пробы подсистемы балансировки нагрузки hello, например <b>02</b>.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-368">Install SAP NetWeaver ERS as root on hello second node using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello ERS for example <b>nws-ers</b>, <b>10.0.0.11</b> and hello instance number that you used for hello probe of hello load balancer for example <b>02</b>.</span></span>

   <span data-ttu-id="e8ae0-369">Можно использовать hello sapinst параметр SAPINST_REMOTE_ACCESS_USER tooallow toosapinst tooconnect непривилегированным пользователем.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-369">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > <span data-ttu-id="e8ae0-370">Используйте SWPM SP 20 PL 05 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-370">Please use SWPM SP 20 PL 05 or higher.</span></span> <span data-ttu-id="e8ae0-371">Более ранние версии не правильно установить разрешения hello и hello установка завершится с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-371">Lower versions do not set hello permissions correctly and hello installation will fail.</span></span>
   > 

1. <span data-ttu-id="e8ae0-372">**[1]**  Адаптировать hello ASCS/SCS и ющих Методов экземпляра профили</span><span class="sxs-lookup"><span data-stu-id="e8ae0-372">**[1]** Adapt hello ASCS/SCS and ERS instance profiles</span></span>
 
   * <span data-ttu-id="e8ae0-373">Профиль ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e8ae0-373">ASCS/SCS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_<b>ASCS00</b>_<b>nws-ascs</b>

   # Change hello restart command tooa start command
   #Restart_Program_01 = local $(_EN) pf=$(_PF)
   Start_Program_01 = local $(_EN) pf=$(_PF)

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector

   # Add hello keep alive parameter
   enque/encni/set_so_keepalive = true
   </code></pre>

   * <span data-ttu-id="e8ae0-374">Профиль ERS</span><span class="sxs-lookup"><span data-stu-id="e8ae0-374">ERS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. <span data-ttu-id="e8ae0-375">**[A]** Настройте активность.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-375">**[A]** Configure Keep Alive</span></span>

   <span data-ttu-id="e8ae0-376">Hello взаимодействие сервера приложений SAP NetWeaver hello и hello ASCS/SCS будет проходить через подсистему балансировки нагрузки программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-376">hello communication between hello SAP NetWeaver application server and hello ASCS/SCS is routed through a software load balancer.</span></span> <span data-ttu-id="e8ae0-377">Подсистема балансировки нагрузки Hello отключает неактивные соединения после истечения времени ожидания можно настроить.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-377">hello load balancer disconnects inactive connections after a configurable timeout.</span></span> <span data-ttu-id="e8ae0-378">tooprevent это нужно tooset параметр в профиль SAP NetWeaver ASCS/SCS hello и изменить параметры системы Linux hello.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-378">tooprevent this you need tooset a parameter in hello SAP NetWeaver ASCS/SCS profile and change hello Linux system settings.</span></span> <span data-ttu-id="e8ae0-379">Дополнительные сведения см. в примечании к SAP [1410736][1410736].</span><span class="sxs-lookup"><span data-stu-id="e8ae0-379">Please read [SAP Note 1410736][1410736] for more information.</span></span>
   
   <span data-ttu-id="e8ae0-380">на последнем шаге hello Hello параметр профиля ASCS/SCS поставить в очередь/encni/set_so_keepalive уже добавлена.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-380">hello ASCS/SCS profile parameter enque/encni/set_so_keepalive was already added in hello last step.</span></span>

   <pre><code> 
   # Change hello Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. <span data-ttu-id="e8ae0-381">**[A]**  Настройка пользователей SAP hello после установки hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-381">**[A]** Configure hello SAP users after hello installation</span></span>
 
   <pre><code>
   # Add sidadm toohello haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. <span data-ttu-id="e8ae0-382">**[1]**  Добавить hello ASCS и SAP ющих Методов службы toohello sapservice файл</span><span class="sxs-lookup"><span data-stu-id="e8ae0-382">**[1]** Add hello ASCS and ERS SAP services toohello sapservice file</span></span>

   <span data-ttu-id="e8ae0-383">Добавьте hello ASCS службы запись toohello второй узел и копировать hello ющих Методов службы запись toohello первый узел.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-383">Add hello ASCS service entry toohello second node and copy hello ERS service entry toohello first node.</span></span>

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. <span data-ttu-id="e8ae0-384">**[1]**  Создать ресурсы кластера hello SAP</span><span class="sxs-lookup"><span data-stu-id="e8ae0-384">**[1]** Create hello SAP cluster resources</span></span>

   <pre><code>
   sudo crm configure property maintenance-mode="true"

   sudo crm configure

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ASCS<b>00</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ASCS<b>00</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b>" \
    AUTOMATIC_RECOVER=false \
    meta resource-stickiness=5000 failure-timeout=60 migration-threshold=1 priority=10

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ERS<b>02</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ERS<b>02</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>" AUTOMATIC_RECOVER=false IS_ERS=true \
    meta priority=1000

   crm(live)configure# modgroup g-<b>NWS</b>_ASCS add rsc_sap_<b>NWS</b>_ASCS<b>00</b>
   crm(live)configure# modgroup g-<b>NWS</b>_ERS add rsc_sap_<b>NWS</b>_ERS<b>02</b>

   crm(live)configure# colocation col_sap_<b>NWS</b>_no_both -5000: g-<b>NWS</b>_ERS g-<b>NWS</b>_ASCS
   crm(live)configure# location loc_sap_<b>NWS</b>_failover_to_ers rsc_sap_<b>NWS</b>_ASCS<b>00</b> rule 2000: runs_ers_<b>NWS</b> eq 1
   crm(live)configure# order ord_sap_<b>NWS</b>_first_start_ascs Optional: rsc_sap_<b>NWS</b>_ASCS<b>00</b>:start rsc_sap_<b>NWS</b>_ERS<b>02</b>:stop symmetrical=false

   crm(live)configure# commit
   crm(live)configure# exit

   sudo crm configure property maintenance-mode="false"
   sudo crm node online <b>nws-cl-0</b>
   </code></pre>

   <span data-ttu-id="e8ae0-385">Убедитесь, что состояние кластера hello в норме и что запущены все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-385">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="e8ae0-386">Не важно, на какие ресурсы узла hello выполняются.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-386">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Online: <b>[ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   </code></pre>

### <a name="create-stonith-device"></a><span data-ttu-id="e8ae0-387">Создание устройства STONITH</span><span class="sxs-lookup"><span data-stu-id="e8ae0-387">Create STONITH device</span></span>

<span data-ttu-id="e8ae0-388">Hello STONITH устройство использует tooauthorize участника-службы для Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-388">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="e8ae0-389">Выполните эти шаги toocreate участника службы.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-389">Follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="e8ae0-390">Go слишком<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="e8ae0-390">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="e8ae0-391">Привет открыть колонку Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e8ae0-391">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="e8ae0-392">Go tooProperties и запишите hello идентификатор каталога. Это hello **ИД клиента**.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-392">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="e8ae0-393">Щелкните "Регистрация приложений".</span><span class="sxs-lookup"><span data-stu-id="e8ae0-393">Click App registrations</span></span>
1. <span data-ttu-id="e8ae0-394">Нажмите "Добавить"</span><span class="sxs-lookup"><span data-stu-id="e8ae0-394">Click Add</span></span>
1. <span data-ttu-id="e8ae0-395">Введите имя, выберите тип приложения "Веб-приложения или API", введите URL-адрес входа (например. http://localhost) и нажмите кнопку "Создать".</span><span class="sxs-lookup"><span data-stu-id="e8ae0-395">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="e8ae0-396">Hello URL-адрес входа не используется и может быть любой допустимый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="e8ae0-396">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="e8ae0-397">Здравствуйте, выберите новое приложение и щелкните на вкладке Параметры hello ключи</span><span class="sxs-lookup"><span data-stu-id="e8ae0-397">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="e8ae0-398">Введите описание нового ключа, выберите "Срок действия не ограничен" и нажмите кнопку "Сохранить".</span><span class="sxs-lookup"><span data-stu-id="e8ae0-398">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="e8ae0-399">Запишите значение hello.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-399">Write down hello Value.</span></span> <span data-ttu-id="e8ae0-400">Он используется как hello **пароль** для hello участника-службы</span><span class="sxs-lookup"><span data-stu-id="e8ae0-400">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="e8ae0-401">Запишите hello идентификатор приложения. Он используется как hello username (**идентификатора входа** в hello действия) для hello участника-службы</span><span class="sxs-lookup"><span data-stu-id="e8ae0-401">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="e8ae0-402">Hello участника-службы не имеет разрешения tooaccess ресурсам Azure по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-402">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="e8ae0-403">Необходимые субъекта-службы разрешений toogive hello toostart и остановить (освободить) всех виртуальных машин кластера hello.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-403">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="e8ae0-404">Go toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="e8ae0-404">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="e8ae0-405">Здравствуйте, откройте колонку все ресурсы</span><span class="sxs-lookup"><span data-stu-id="e8ae0-405">Open hello All resources blade</span></span>
1. <span data-ttu-id="e8ae0-406">Выберите виртуальную машину, hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-406">Select hello virtual machine</span></span>
1. <span data-ttu-id="e8ae0-407">Выберите "Управление доступом (IAM)".</span><span class="sxs-lookup"><span data-stu-id="e8ae0-407">Click Access control (IAM)</span></span>
1. <span data-ttu-id="e8ae0-408">Нажмите "Добавить"</span><span class="sxs-lookup"><span data-stu-id="e8ae0-408">Click Add</span></span>
1. <span data-ttu-id="e8ae0-409">Выберите роль hello владельца</span><span class="sxs-lookup"><span data-stu-id="e8ae0-409">Select hello role Owner</span></span>
1. <span data-ttu-id="e8ae0-410">Введите имя приложения hello, созданной выше hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-410">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="e8ae0-411">Нажмите кнопку "ОК"</span><span class="sxs-lookup"><span data-stu-id="e8ae0-411">Click OK</span></span>

#### <a name="1-create-hello-stonith-devices"></a><span data-ttu-id="e8ae0-412">**[1]**  Создайте hello STONITH устройства</span><span class="sxs-lookup"><span data-stu-id="e8ae0-412">**[1]** Create hello STONITH devices</span></span>

<span data-ttu-id="e8ae0-413">После редактирования hello разрешения для виртуальных машин hello hello STONITH устройства можно настроить в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-413">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a><span data-ttu-id="e8ae0-414">**[1]**  Включить использование hello STONITH устройства</span><span class="sxs-lookup"><span data-stu-id="e8ae0-414">**[1]** Enable hello use of a STONITH device</span></span>

<span data-ttu-id="e8ae0-415">Разрешить использование hello STONITH устройства</span><span class="sxs-lookup"><span data-stu-id="e8ae0-415">Enable hello use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a><span data-ttu-id="e8ae0-416">Установка базы данных</span><span class="sxs-lookup"><span data-stu-id="e8ae0-416">Install database</span></span>

<span data-ttu-id="e8ae0-417">В этом примере устанавливается и настраивается репликация системы SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-417">In this example an SAP HANA System Replication is installed and configured.</span></span> <span data-ttu-id="e8ae0-418">SAP HANA будет выполняться в hello же кластера в качестве hello SAP NetWeaver ASCS/SCS и ющих Методов.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-418">SAP HANA will run in hello same cluster as hello SAP NetWeaver ASCS/SCS and ERS.</span></span> <span data-ttu-id="e8ae0-419">SAP HANA можно также установить на выделенный кластер.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-419">You can also install SAP HANA on a dedicated cluster.</span></span> <span data-ttu-id="e8ae0-420">Дополнительные сведения см. в статье [Высокий уровень доступности SAP HANA на виртуальных машинах Azure][sap-hana-ha].</span><span class="sxs-lookup"><span data-stu-id="e8ae0-420">See [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha] for more information.</span></span>

### <a name="prepare-for-sap-hana-installation"></a><span data-ttu-id="e8ae0-421">Подготовка к установке SAP HANA</span><span class="sxs-lookup"><span data-stu-id="e8ae0-421">Prepare for SAP HANA installation</span></span>

<span data-ttu-id="e8ae0-422">Обычно для томов, предназначенных для хранения данных и файлов журнала, рекомендуется использовать LVM.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-422">We generally recommend using LVM for volumes that store data and log files.</span></span> <span data-ttu-id="e8ae0-423">В целях тестирования можно также выбрать toostore hello файла журнала и данных непосредственно на обычный диск.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-423">For testing purposes, you can also choose toostore hello data and log file directly on a plain disk.</span></span>

1. <span data-ttu-id="e8ae0-424">**[A]** LVM.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-424">**[A]** LVM</span></span>  
   <span data-ttu-id="e8ae0-425">Hello примере предполагается, что hello виртуальные машины имеют четыре дисков данных, следует использовать toocreate два тома.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-425">hello example below assumes that hello virtual machines have four data disks attached that should be used toocreate two volumes.</span></span>
   
   <span data-ttu-id="e8ae0-426">Создание физических томов для всех дисков, которые должны toouse.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-426">Create physical volumes for all disks that you want toouse.</span></span>
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   <span data-ttu-id="e8ae0-427">Создание группы томов для файлов данных hello, одна группа томов для файлов журнала hello и один для общей папки hello SAP HANA</span><span class="sxs-lookup"><span data-stu-id="e8ae0-427">Create a volume group for hello data files, one volume group for hello log files and one for hello shared directory of SAP HANA</span></span>
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   <span data-ttu-id="e8ae0-428">Создать логические тома hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-428">Create hello logical volumes</span></span>
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   <span data-ttu-id="e8ae0-429">Создайте каталоги подключения hello и скопируйте hello UUID всех логических томов</span><span class="sxs-lookup"><span data-stu-id="e8ae0-429">Create hello mount directories and copy hello UUID of all logical volumes</span></span>
   
   <pre><code>
   sudo mkdir -p /hana/data
   sudo mkdir -p /hana/log
   sudo mkdir -p /hana/shared
   sudo chattr +i /hana/data
   sudo chattr +i /hana/log
   sudo chattr +i /hana/shared
   # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
   sudo blkid
   </code></pre>
   
   <span data-ttu-id="e8ae0-430">Создайте записи autofs для hello трех логических томах.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-430">Create autofs entries for hello three logical volumes</span></span>
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   <span data-ttu-id="e8ae0-431">Вставьте этот /etc/auto.direct vi toosudo строки</span><span class="sxs-lookup"><span data-stu-id="e8ae0-431">Insert this line toosudo vi /etc/auto.direct</span></span>
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   <span data-ttu-id="e8ae0-432">Подключите новый тома hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-432">Mount hello new volumes</span></span>
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. <span data-ttu-id="e8ae0-433">**[A]** Обычные диски.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-433">**[A]** Plain Disks</span></span>  

   <span data-ttu-id="e8ae0-434">Для небольших или демонстрационных систем файлы данных и журналов HANA можно поместить на один диск.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-434">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="e8ae0-435">Hello следующие команды создают секции на /dev/sdc и отформатируйте его xfs.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-435">hello following commands create a partition on /dev/sdc and format it with xfs.</span></span>
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down hello id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   <span data-ttu-id="e8ae0-436">Вставьте этот too/etc/auto.direct строки</span><span class="sxs-lookup"><span data-stu-id="e8ae0-436">Insert this line too/etc/auto.direct</span></span>
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   <span data-ttu-id="e8ae0-437">Создать каталог назначения hello и подключите диск hello.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-437">Create hello target directory and mount hello disk.</span></span>
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a><span data-ttu-id="e8ae0-438">Установка SAP HANA</span><span class="sxs-lookup"><span data-stu-id="e8ae0-438">Installing SAP HANA</span></span>

<span data-ttu-id="e8ae0-439">Hello следующие действия на основе главе 4 hello [SAP HANA SR производительности оптимизированных Scenario guide] [ suse-hana-ha-guide] tooinstall репликации системы SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-439">hello following steps are based on chapter 4 of hello [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] tooinstall SAP HANA System Replication.</span></span> <span data-ttu-id="e8ae0-440">Прочитайте его перед продолжением установки hello.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-440">Please read it before you continue hello installation.</span></span>

1. <span data-ttu-id="e8ae0-441">**[A]**  Запустите hdblcm из hello HANA DVD-диска</span><span class="sxs-lookup"><span data-stu-id="e8ae0-441">**[A]** Run hdblcm from hello HANA DVD</span></span>
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. <span data-ttu-id="e8ae0-442">**[A]** Обновите агент узла SAP.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-442">**[A]** Upgrade SAP Host Agent</span></span>

   <span data-ttu-id="e8ae0-443">Загрузить последний архив агента узла SAP hello hello [SAP Softwarecenter] [ sap-swcenter] и выполнения hello следующие команды tooupgrade hello агента.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-443">Download hello latest SAP Host Agent archive from hello [SAP Softwarecenter][sap-swcenter] and run hello following command tooupgrade hello agent.</span></span> <span data-ttu-id="e8ae0-444">Замените hello путь toohello архив toopoint toohello загруженный файл.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-444">Replace hello path toohello archive toopoint toohello file you downloaded.</span></span>
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path tooSAP Host Agent SAR&gt;</b> 
   </code></pre>

1. <span data-ttu-id="e8ae0-445">**[1]** Создайте репликацию HANA (в качестве привилегированного пользователя).</span><span class="sxs-lookup"><span data-stu-id="e8ae0-445">**[1]** Create HANA replication (as root)</span></span>  

   <span data-ttu-id="e8ae0-446">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-446">Run hello following command.</span></span> <span data-ttu-id="e8ae0-447">Убедитесь, что tooreplace полужирным шрифтом строки (идентификатор HDB HANA системы и номера экземпляра 03) со значениями hello установки SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-447">Make sure tooreplace bold strings (HANA System ID HDB and instance number 03) with hello values of your SAP HANA installation.</span></span>
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. <span data-ttu-id="e8ae0-448">**[A]** Создайте запись хранилища ключей (в качестве привилегированного пользователя).</span><span class="sxs-lookup"><span data-stu-id="e8ae0-448">**[A]** Create keystore entry (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. <span data-ttu-id="e8ae0-449">**[1]** Создайте резервную копию базы данных (в качестве привилегированного пользователя).</span><span class="sxs-lookup"><span data-stu-id="e8ae0-449">**[1]** Backup database (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. <span data-ttu-id="e8ae0-450">**[1]**  Смена пользователя sapsid HANA toohello и создания hello первичного сайта.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-450">**[1]** Switch toohello HANA sapsid user and create hello primary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. <span data-ttu-id="e8ae0-451">**[2]**  Смена пользователя sapsid HANA toohello и создания вторичного сайта hello.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-451">**[2]** Switch toohello HANA sapsid user and create hello secondary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. <span data-ttu-id="e8ae0-452">**[1]** Создайте кластерные ресурсы SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-452">**[1]** Create SAP HANA cluster resources</span></span>

   <span data-ttu-id="e8ae0-453">Во-первых создайте hello топологии.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-453">First, create hello topology.</span></span>
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number and HANA system id
   
   crm(live)configure# primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b>   ocf:suse:SAPHanaTopology \
     operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
     op monitor interval="10" timeout="600" \
     op start interval="0" timeout="600" \
     op stop interval="0" timeout="300" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"
    
   crm(live)configure# clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>
   
   <span data-ttu-id="e8ae0-454">Создайте hello HANA ресурсы</span><span class="sxs-lookup"><span data-stu-id="e8ae0-454">Next, create hello HANA resources</span></span>
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
    
   crm(live)configure# primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
     operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
     op start interval="0" timeout="3600" \
     op stop interval="0" timeout="3600" \
     op promote interval="0" timeout="3600" \
     op monitor interval="60" role="Master" timeout="700" \
     op monitor interval="61" role="Slave" timeout="700" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
     DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"
    
   crm(live)configure# ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
     target-role="Started" interleave="true"
    
   crm(live)configure# primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
     meta target-role="Started" is-managed="true" \ 
     operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
     op monitor interval="10s" timeout="20s" \ 
     params ip="<b>10.0.0.12</b>" 

   crm(live)configure# primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
     params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
     op monitor timeout=20s interval=10 depth=0 

   crm(live)configure# group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  

   crm(live)configure# order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   <span data-ttu-id="e8ae0-455">Убедитесь, что состояние кластера hello в норме и что запущены все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-455">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="e8ae0-456">Не важно, на какие ресурсы узла hello выполняются.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-456">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # <b>Online: [ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Clone Set: cln_SAPHanaTopology_HDB_HDB03 [rsc_SAPHanaTopology_HDB_HDB03]
   #      <b>Started: [ nws-cl-0 nws-cl-1 ]</b>
   #  Master/Slave Set: msl_SAPHana_HDB_HDB03 [rsc_SAPHana_HDB_HDB03]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g_ip_HDB_HDB03
   #      rsc_ip_HDB_HDB03   (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      rsc_nc_HDB_HDB03   (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   # rsc_st_azure_1  (stonith:fence_azure_arm):      <b>Started nws-cl-0</b>
   # rsc_st_azure_2  (stonith:fence_azure_arm):      <b>Started nws-cl-1</b>
   </code></pre>

1. <span data-ttu-id="e8ae0-457">**[1]**  Экземпляр базы данных SAP NetWeaver hello установки</span><span class="sxs-lookup"><span data-stu-id="e8ae0-457">**[1]** Install hello SAP NetWeaver database instance</span></span>

   <span data-ttu-id="e8ae0-458">Установка экземпляра базы данных SAP NetWeaver hello как корневой каталог с помощью виртуального имени узла, которое сопоставляет IP-адрес toohello hello конфигурации переднего плана подсистемы балансировки нагрузки для hello базы данных, например <b>nws db</b> и <b>10.0.0.12</b>.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-458">Install hello SAP NetWeaver database instance as root using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello database for example <b>nws-db</b> and <b>10.0.0.12</b>.</span></span>

   <span data-ttu-id="e8ae0-459">Можно использовать hello sapinst параметр SAPINST_REMOTE_ACCESS_USER tooallow toosapinst tooconnect непривилегированным пользователем.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-459">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a><span data-ttu-id="e8ae0-460">Установка сервера приложений SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="e8ae0-460">SAP NetWeaver application server installation</span></span>

<span data-ttu-id="e8ae0-461">Выполните эти шаги tooinstall сервера приложений SAP.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-461">Follow these steps tooinstall an SAP application server.</span></span> <span data-ttu-id="e8ae0-462">приведенных ниже шагов Hello предполагается установить hello сервера приложений на сервере отличается от hello ASCS/SCS и HANA серверов.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-462">hello steps bellow assume that you install hello application server on a server different from hello ASCS/SCS and HANA servers.</span></span> <span data-ttu-id="e8ae0-463">В противном случае некоторые шаги hello ниже (например, при настройке разрешения имени узла) не требуются.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-463">Otherwise some of hello steps below (like configuring host name resolution) are not needed.</span></span>

1. <span data-ttu-id="e8ae0-464">Настройте разрешение имен.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-464">Setup host name resolution</span></span>    
   <span data-ttu-id="e8ae0-465">Можно использовать DNS-сервер или измените hello/etc/hosts, на всех узлах.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-465">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="e8ae0-466">В этом примере показано, как toouse hello файл/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-466">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="e8ae0-467">Замените hello IP-адрес и имя узла hello в hello, следующие команды</span><span class="sxs-lookup"><span data-stu-id="e8ae0-467">Replace hello IP address and hello hostname in hello following commands</span></span>
   ```bash
   sudo vi /etc/hosts
   ```
   <span data-ttu-id="e8ae0-468">Вставьте следующие строки слишком/и т. д/узлы hello.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-468">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="e8ae0-469">Изменение среды toomatch hello IP адрес и имя узла</span><span class="sxs-lookup"><span data-stu-id="e8ae0-469">Change hello IP address and hostname toomatch your environment</span></span>    
    
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   # IP address of hello application server
   <b>10.0.0.8 nws-di-0</b>
   </code></pre>

1. <span data-ttu-id="e8ae0-470">Создать каталог sapmnt hello</span><span class="sxs-lookup"><span data-stu-id="e8ae0-470">Create hello sapmnt directory</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. <span data-ttu-id="e8ae0-471">Настройте autofs:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-471">Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="e8ae0-472">Создайте файл со следующим текстом:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-472">Create a new file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   <span data-ttu-id="e8ae0-473">Перезапустите toomount autofs hello новые общие папки</span><span class="sxs-lookup"><span data-stu-id="e8ae0-473">Restart autofs toomount hello new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="e8ae0-474">Настройте файл подкачки:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-474">Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="e8ae0-475">Перезапустите hello агента tooactivate hello изменений</span><span class="sxs-lookup"><span data-stu-id="e8ae0-475">Restart hello Agent tooactivate hello change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. <span data-ttu-id="e8ae0-476">Установите сервер приложений SAP NetWeaver:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-476">Install SAP NetWeaver application server</span></span>

   <span data-ttu-id="e8ae0-477">Установите основной и дополнительный сервер приложений SAP NetWeaver:</span><span class="sxs-lookup"><span data-stu-id="e8ae0-477">Install a primary or additional SAP NetWeaver applications server.</span></span>

   <span data-ttu-id="e8ae0-478">Можно использовать hello sapinst параметр SAPINST_REMOTE_ACCESS_USER tooallow toosapinst tooconnect непривилегированным пользователем.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-478">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="e8ae0-479">Обновите безопасное хранилище SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-479">Update SAP HANA secure store</span></span>

   <span data-ttu-id="e8ae0-480">Обновление hello SAP HANA безопасного хранения toopoint toohello виртуальное имя настройки репликации системы SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="e8ae0-480">Update hello SAP HANA secure store toopoint toohello virtual name of hello SAP HANA System Replication setup.</span></span>
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a><span data-ttu-id="e8ae0-481">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e8ae0-481">Next steps</span></span>
* <span data-ttu-id="e8ae0-482">[SAP NetWeaver на виртуальных машинах Windows. Руководство по планированию и внедрению][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="e8ae0-482">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="e8ae0-483">[Развертывание программного обеспечения SAP на виртуальных машинах Azure][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="e8ae0-483">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="e8ae0-484">[SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию СУБД][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="e8ae0-484">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="e8ae0-485">tooestablish высокого уровня доступности и план аварийного восстановления из SAP HANA в Azure (большие экземпляры). в статье toolearn [SAP HANA (крупных экземпляров) высокой доступности и аварийного восстановления в Azure](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="e8ae0-485">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span>
* <span data-ttu-id="e8ae0-486">toolearn tooestablish высокий уровень доступности и план аварийного восстановления из SAP HANA на виртуальных машинах Azure, в статье [высокого уровня доступности SAP HANA на виртуальных машинах Azure (ВМ)][sap-hana-ha]</span><span class="sxs-lookup"><span data-stu-id="e8ae0-486">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure VMs, see [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha]</span></span>
