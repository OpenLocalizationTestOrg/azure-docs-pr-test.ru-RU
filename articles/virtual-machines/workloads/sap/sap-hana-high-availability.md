---
title: "Высокий уровень доступности SAP HANA на виртуальных машинах Azure | Документация Майкрософт"
description: "Обеспечение высокого уровня доступности SAP HANA на виртуальных машинах Azure."
services: virtual-machines-linux
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: sedusch
ms.openlocfilehash: 951150e621d21037b0adde7287b9f985290d8d11
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a><span data-ttu-id="b74ee-103">Высокий уровень доступности SAP HANA на виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="b74ee-103">High Availability of SAP HANA on Azure Virtual Machines (VMs)</span></span>

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

<span data-ttu-id="b74ee-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span><span class="sxs-lookup"><span data-stu-id="b74ee-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span></span>
<span data-ttu-id="b74ee-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span><span class="sxs-lookup"><span data-stu-id="b74ee-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span></span>
<span data-ttu-id="b74ee-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span><span class="sxs-lookup"><span data-stu-id="b74ee-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span></span>
<span data-ttu-id="b74ee-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span><span class="sxs-lookup"><span data-stu-id="b74ee-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span></span>
<span data-ttu-id="b74ee-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span><span class="sxs-lookup"><span data-stu-id="b74ee-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span></span>
<span data-ttu-id="b74ee-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span><span class="sxs-lookup"><span data-stu-id="b74ee-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span></span>
<span data-ttu-id="b74ee-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span><span class="sxs-lookup"><span data-stu-id="b74ee-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span></span>
<span data-ttu-id="b74ee-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span><span class="sxs-lookup"><span data-stu-id="b74ee-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span></span>
<span data-ttu-id="b74ee-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span><span class="sxs-lookup"><span data-stu-id="b74ee-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span></span>

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

<span data-ttu-id="b74ee-113">В локальной среде для обеспечения высокого уровня доступности SAP HANA можно использовать либо системную репликацию HANA, либо общее хранилище.</span><span class="sxs-lookup"><span data-stu-id="b74ee-113">On-premises, you can use either HANA System Replication or use shared storage to establish high availability for SAP HANA.</span></span>
<span data-ttu-id="b74ee-114">В настоящее время в Azure поддерживается только настройка системной репликации HANA.</span><span class="sxs-lookup"><span data-stu-id="b74ee-114">We currently only support setting up HANA System Replication on Azure.</span></span> <span data-ttu-id="b74ee-115">Для репликации SAP HANA используются один главный узел и по крайней мере один подчиненный узел.</span><span class="sxs-lookup"><span data-stu-id="b74ee-115">SAP HANA Replication consists of one master node and at least one slave node.</span></span> <span data-ttu-id="b74ee-116">Изменения данных на главном узле синхронно или асинхронно реплицируются на подчиненные узлы.</span><span class="sxs-lookup"><span data-stu-id="b74ee-116">Changes to the data on the master node are replicated to the slave nodes synchronously or asynchronously.</span></span>

<span data-ttu-id="b74ee-117">В этой статье описывается развертывание виртуальных машин, их настройка, установка платформы кластера, а также установка и настройка системной репликации SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="b74ee-117">This article describes how to deploy the virtual machines, configure the virtual machines, install the cluster framework, install and configure SAP HANA System Replication.</span></span>
<span data-ttu-id="b74ee-118">В примерах конфигурации, командах для установки и т. д. используется экземпляр номер 03 и идентификатор системы HANA HDB.</span><span class="sxs-lookup"><span data-stu-id="b74ee-118">In the example configurations, installation commands etc. instance number 03 and HANA System ID HDB is used.</span></span>

<span data-ttu-id="b74ee-119">Сначала прочитайте следующие примечания и документы SAP:</span><span class="sxs-lookup"><span data-stu-id="b74ee-119">Read the following SAP Notes and papers first</span></span>

* <span data-ttu-id="b74ee-120">примечание к SAP [1928533], которое содержит:</span><span class="sxs-lookup"><span data-stu-id="b74ee-120">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="b74ee-121">список размеров виртуальных машин Azure, поддерживаемых для развертывания ПО SAP;</span><span class="sxs-lookup"><span data-stu-id="b74ee-121">List of Azure VM sizes that are supported for the deployment of SAP software</span></span>
  * <span data-ttu-id="b74ee-122">важные сведения о доступных ресурсах для каждого размера виртуальной машины Azure;</span><span class="sxs-lookup"><span data-stu-id="b74ee-122">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="b74ee-123">сведения о поддерживаемом программном обеспечении SAP и сочетаниях операционных систем и баз данных;</span><span class="sxs-lookup"><span data-stu-id="b74ee-123">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="b74ee-124">сведения о требуемой версии ядра SAP для Windows и Linux в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b74ee-124">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>
* <span data-ttu-id="b74ee-125">примечание к SAP [2015553], в котором описываются предварительные требования к SAP при развертывании программного обеспечения SAP в Azure;</span><span class="sxs-lookup"><span data-stu-id="b74ee-125">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="b74ee-126">Примечание SAP [2205917] содержит рекомендуемые параметры ОС для SUSE Linux Enterprise Server для приложений SAP.</span><span class="sxs-lookup"><span data-stu-id="b74ee-126">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="b74ee-127">Примечание SAP [1944799] содержит рекомендации для SAP HANA в SUSE Linux Enterprise Server для приложений SAP.</span><span class="sxs-lookup"><span data-stu-id="b74ee-127">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="b74ee-128">примечание к SAP [2178632], содержащее подробные сведения обо всех доступных метриках мониторинга для SAP в Azure;</span><span class="sxs-lookup"><span data-stu-id="b74ee-128">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="b74ee-129">примечание к SAP [2191498], содержащее сведения о необходимой версии агента SAP Host Agent для Linux в Azure;</span><span class="sxs-lookup"><span data-stu-id="b74ee-129">SAP Note [2191498] has the required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="b74ee-130">примечание к SAP [2243692], содержащее сведения о лицензировании SAP в Linux в Azure;</span><span class="sxs-lookup"><span data-stu-id="b74ee-130">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="b74ee-131">примечание к SAP [1984787], содержащее общие сведения о SUSE Linux Enterprise Server 12;</span><span class="sxs-lookup"><span data-stu-id="b74ee-131">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="b74ee-132">примечание к SAP [1999351], содержащее дополнительные сведения об устранении неполадок, связанных с расширением для расширенного мониторинга Azure для SAP;</span><span class="sxs-lookup"><span data-stu-id="b74ee-132">SAP Note [1999351] has additional troubleshooting information for the Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="b74ee-133">[вики-сайт сообщества SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes), содержащий все необходимые примечания к SAP для Linux;</span><span class="sxs-lookup"><span data-stu-id="b74ee-133">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="b74ee-134">[SAP NetWeaver на виртуальных машинах Windows. Руководство по планированию и внедрению][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="b74ee-134">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="b74ee-135">[Развертывание программного обеспечения SAP на виртуальных машинах Linux в Azure (эта статья)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="b74ee-135">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="b74ee-136">[SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию СУБД][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="b74ee-136">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="b74ee-137">[Сценарий оптимизации производительности системной репликации SAP HANA][suse-hana-ha-guide]: это руководство содержит все сведения, необходимые для настройки системной репликации SAP HANA в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="b74ee-137">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] The guide contains all required information to set up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="b74ee-138">Используйте это руководство как основу.</span><span class="sxs-lookup"><span data-stu-id="b74ee-138">Use this guide as a baseline.</span></span>

## <a name="deploying-linux"></a><span data-ttu-id="b74ee-139">Развертывание Linux</span><span class="sxs-lookup"><span data-stu-id="b74ee-139">Deploying Linux</span></span>

<span data-ttu-id="b74ee-140">Агент ресурсов для SAP HANA включен в состав SUSE Linux Enterprise Server for SAP Applications.</span><span class="sxs-lookup"><span data-stu-id="b74ee-140">The resource agent for SAP HANA is included in SUSE Linux Enterprise Server for SAP Applications.</span></span>
<span data-ttu-id="b74ee-141">В Azure Marketplace доступен образ SUSE Linux Enterprise Server for SAP Applications 12 с BYOS (использование собственной подписки), который можно использовать для развертывания новых виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b74ee-141">The Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 with BYOS (Bring Your Own Subscription) that you can use to deploy new virtual machines.</span></span>

### <a name="manual-deployment"></a><span data-ttu-id="b74ee-142">Развертывание вручную</span><span class="sxs-lookup"><span data-stu-id="b74ee-142">Manual Deployment</span></span>

1. <span data-ttu-id="b74ee-143">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="b74ee-143">Create a Resource Group</span></span>
1. <span data-ttu-id="b74ee-144">Создайте виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="b74ee-144">Create a Virtual Network</span></span>
1. <span data-ttu-id="b74ee-145">Создание двух учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="b74ee-145">Create two Storage Accounts</span></span>
1. <span data-ttu-id="b74ee-146">Создание группы доступности.</span><span class="sxs-lookup"><span data-stu-id="b74ee-146">Create an Availability Set</span></span>  
   <span data-ttu-id="b74ee-147">Настройка максимального числа доменов обновления.</span><span class="sxs-lookup"><span data-stu-id="b74ee-147">Set max update domain</span></span>
1. <span data-ttu-id="b74ee-148">Создание подсистемы балансировки нагрузки (внутренней).</span><span class="sxs-lookup"><span data-stu-id="b74ee-148">Create a Load Balancer (internal)</span></span>  
   <span data-ttu-id="b74ee-149">Выбор виртуальной сети, созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="b74ee-149">Select VNET of step above</span></span>
1. <span data-ttu-id="b74ee-150">Создание виртуальной машины 1.</span><span class="sxs-lookup"><span data-stu-id="b74ee-150">Create Virtual Machine 1</span></span>  
   <span data-ttu-id="b74ee-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="b74ee-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="b74ee-152">SLES For SAP Applications 12 SP1 (BYOS).</span><span class="sxs-lookup"><span data-stu-id="b74ee-152">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="b74ee-153">Выбор учетной записи хранения 1.</span><span class="sxs-lookup"><span data-stu-id="b74ee-153">Select Storage Account 1</span></span>  
   <span data-ttu-id="b74ee-154">Выбор группы доступности.</span><span class="sxs-lookup"><span data-stu-id="b74ee-154">Select Availability Set</span></span>  
1. <span data-ttu-id="b74ee-155">Создание виртуальной машины 2.</span><span class="sxs-lookup"><span data-stu-id="b74ee-155">Create Virtual Machine 2</span></span>  
   <span data-ttu-id="b74ee-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="b74ee-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="b74ee-157">SLES For SAP Applications 12 SP1 (BYOS).</span><span class="sxs-lookup"><span data-stu-id="b74ee-157">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="b74ee-158">Выбор учетной записи хранения 2.</span><span class="sxs-lookup"><span data-stu-id="b74ee-158">Select Storage Account 2</span></span>   
   <span data-ttu-id="b74ee-159">Выбор группы доступности.</span><span class="sxs-lookup"><span data-stu-id="b74ee-159">Select Availability Set</span></span>  
1. <span data-ttu-id="b74ee-160">Добавление дисков данных.</span><span class="sxs-lookup"><span data-stu-id="b74ee-160">Add Data Disks</span></span>
1. <span data-ttu-id="b74ee-161">Настройка подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="b74ee-161">Configure the load balancer</span></span>
    1. <span data-ttu-id="b74ee-162">Создание пула внешних IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="b74ee-162">Create a frontend IP pool</span></span>
        1. <span data-ttu-id="b74ee-163">Откройте подсистему балансировки нагрузки, выберите пул внешних IP-адресов и щелкните "Добавить".</span><span class="sxs-lookup"><span data-stu-id="b74ee-163">Open the load balancer, select frontend IP pool and click Add</span></span>
        1. <span data-ttu-id="b74ee-164">Введите имя нового пула внешних IP-адресов (например, hana-frontend).</span><span class="sxs-lookup"><span data-stu-id="b74ee-164">Enter the name of the new frontend IP pool (for example hana-frontend)</span></span>
       1. <span data-ttu-id="b74ee-165">Нажмите кнопку "ОК"</span><span class="sxs-lookup"><span data-stu-id="b74ee-165">Click OK</span></span>
        1. <span data-ttu-id="b74ee-166">После создания пула внешних IP-адресов запишите его IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="b74ee-166">After the new frontend IP pool is created, write down its IP address</span></span>
    1. <span data-ttu-id="b74ee-167">Создание внутреннего пула.</span><span class="sxs-lookup"><span data-stu-id="b74ee-167">Create a backend pool</span></span>
        1. <span data-ttu-id="b74ee-168">Выберите подсистему балансировки нагрузки, щелкните "Серверные пулы" и нажмите кнопку "Добавить".</span><span class="sxs-lookup"><span data-stu-id="b74ee-168">Open the load balancer, select backend pools and click Add</span></span>
        1. <span data-ttu-id="b74ee-169">Введите имя нового внутреннего пула (например, hana-backend).</span><span class="sxs-lookup"><span data-stu-id="b74ee-169">Enter the name of the new backend pool (for example hana-backend)</span></span>
        1. <span data-ttu-id="b74ee-170">Щелкните "Добавить виртуальную машину".</span><span class="sxs-lookup"><span data-stu-id="b74ee-170">Click Add a virtual machine</span></span>
        1. <span data-ttu-id="b74ee-171">Выберите ранее созданную группу доступности.</span><span class="sxs-lookup"><span data-stu-id="b74ee-171">Select the Availability Set you created earlier</span></span>
        1. <span data-ttu-id="b74ee-172">Выберите виртуальные машины кластера SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="b74ee-172">Select the virtual machines of the SAP HANA cluster</span></span>
        1. <span data-ttu-id="b74ee-173">Нажмите кнопку "ОК"</span><span class="sxs-lookup"><span data-stu-id="b74ee-173">Click OK</span></span>
    1. <span data-ttu-id="b74ee-174">Создание пробы работоспособности</span><span class="sxs-lookup"><span data-stu-id="b74ee-174">Create a health probe</span></span>
       1. <span data-ttu-id="b74ee-175">Выберите подсистему балансировки нагрузки, щелкните "Зонды работоспособности" и нажмите кнопку "Добавить".</span><span class="sxs-lookup"><span data-stu-id="b74ee-175">Open the load balancer, select health probes and click Add</span></span>
        1. <span data-ttu-id="b74ee-176">Введите имя новой пробы работоспособности (например, hana-hp).</span><span class="sxs-lookup"><span data-stu-id="b74ee-176">Enter the name of the new health probe (for example hana-hp)</span></span>
        1. <span data-ttu-id="b74ee-177">Выберите протокол TCP, порт 625**03**, интервал, равный 5, и порог состояния неработоспособности, равный 2.</span><span class="sxs-lookup"><span data-stu-id="b74ee-177">Select TCP as protocol, port 625**03**, keep Interval 5 and Unhealthy threshold 2</span></span>
        1. <span data-ttu-id="b74ee-178">Нажмите кнопку "ОК"</span><span class="sxs-lookup"><span data-stu-id="b74ee-178">Click OK</span></span>
    1. <span data-ttu-id="b74ee-179">Создание правил балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="b74ee-179">Create load balancing rules</span></span>
        1. <span data-ttu-id="b74ee-180">Выберите подсистему балансировки нагрузки, щелкните "Правила балансировки нагрузки" и нажмите кнопку "Добавить".</span><span class="sxs-lookup"><span data-stu-id="b74ee-180">Open the load balancer, select load balancing rules and click Add</span></span>
        1. <span data-ttu-id="b74ee-181">Введите имя нового правила балансировки нагрузки (например hana-lb-3**03**15).</span><span class="sxs-lookup"><span data-stu-id="b74ee-181">Enter the name of the new load balancer rule (for example hana-lb-3**03**15)</span></span>
        1. <span data-ttu-id="b74ee-182">Выберите пул внешних IP-адресов, внутренний пул и пробу работоспособности, созданные ранее (например, hana-frontend).</span><span class="sxs-lookup"><span data-stu-id="b74ee-182">Select the frontend IP address, backend pool and health probe you created earlier (for example hana-frontend)</span></span>
        1. <span data-ttu-id="b74ee-183">Оставьте выбранным протокол TCP и введите порт 3**03**15.</span><span class="sxs-lookup"><span data-stu-id="b74ee-183">Keep protocol TCP, enter port 3**03**15</span></span>
        1. <span data-ttu-id="b74ee-184">Увеличьте время ожидания до 30 минут.</span><span class="sxs-lookup"><span data-stu-id="b74ee-184">Increase idle timeout to 30 minutes</span></span>
       1. <span data-ttu-id="b74ee-185">**Не забудьте включить плавающий IP-адрес**.</span><span class="sxs-lookup"><span data-stu-id="b74ee-185">**Make sure to enable Floating IP**</span></span>
        1. <span data-ttu-id="b74ee-186">Нажмите кнопку "ОК"</span><span class="sxs-lookup"><span data-stu-id="b74ee-186">Click OK</span></span>
        1. <span data-ttu-id="b74ee-187">Повторите предыдущие шаги для порта 3**03**17.</span><span class="sxs-lookup"><span data-stu-id="b74ee-187">Repeat the steps above for port 3**03**17</span></span>

### <a name="deploy-with-template"></a><span data-ttu-id="b74ee-188">Развертывание с помощью шаблона</span><span class="sxs-lookup"><span data-stu-id="b74ee-188">Deploy with template</span></span>
<span data-ttu-id="b74ee-189">Шаблоны быстрого запуска с сайта GitHub можно использовать для развертывания всех необходимых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b74ee-189">You can use one of the quick start templates on github to deploy all required resources.</span></span> <span data-ttu-id="b74ee-190">Шаблон развертывает виртуальные машины, подсистему балансировки нагрузки, группу доступности и т. д. Выполните следующее, чтобы развернуть шаблон.</span><span class="sxs-lookup"><span data-stu-id="b74ee-190">The template deploys the virtual machines, the load balancer, availability set etc. Follow these steps to deploy the template:</span></span>

1. <span data-ttu-id="b74ee-191">Откройте [шаблон базы данных][template-multisid-db] или [конвергированный шаблон][template-converged] на портале Azure. Шаблон базы данных создает только правила балансировки нагрузки для базы данных, а конвергированный шаблон дополнительно создает правила балансировки нагрузки для экземпляра ASCS/SCS и ERS (только Linux).</span><span class="sxs-lookup"><span data-stu-id="b74ee-191">Open the [database template][template-multisid-db] or the [converged template][template-converged] on the Azure Portal The database template only creates the load-balancing rules for a database whereas the converged template also creates the load-balancing rules for an ASCS/SCS and ERS (Linux only) instance.</span></span> <span data-ttu-id="b74ee-192">Если вы планируете установить систему на основе SAP NetWeaver и экземпляр ASCS/SCS на одних и тех же компьютерах, используйте [конвергированный шаблон][template-converged].</span><span class="sxs-lookup"><span data-stu-id="b74ee-192">If you plan to install an SAP NetWeaver based system and you also want to install the ASCS/SCS instance on the same machines, use the [converged template][template-converged].</span></span>
1. <span data-ttu-id="b74ee-193">Задайте следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="b74ee-193">Enter the following parameters</span></span>
    1. <span data-ttu-id="b74ee-194">Идентификатор системы SAP</span><span class="sxs-lookup"><span data-stu-id="b74ee-194">Sap System Id</span></span>  
       <span data-ttu-id="b74ee-195">Введите идентификатор системы SAP, которую требуется установить.</span><span class="sxs-lookup"><span data-stu-id="b74ee-195">Enter the SAP system Id of the SAP system you want to install.</span></span> <span data-ttu-id="b74ee-196">Идентификатор будет использоваться в качестве префикса для развертываемых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b74ee-196">The Id will be used as a prefix for the resources that are deployed.</span></span>
    1. <span data-ttu-id="b74ee-197">Тип стека (указывается только при использовании конвергированного шаблона).</span><span class="sxs-lookup"><span data-stu-id="b74ee-197">Stack Type (only applicable if you use the converged template)</span></span>  
       <span data-ttu-id="b74ee-198">Выберите тип стека SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="b74ee-198">Select the SAP NetWeaver stack type</span></span>
    1. <span data-ttu-id="b74ee-199">Тип ОС</span><span class="sxs-lookup"><span data-stu-id="b74ee-199">Os Type</span></span>  
       <span data-ttu-id="b74ee-200">Выберите один из дистрибутивов Linux.</span><span class="sxs-lookup"><span data-stu-id="b74ee-200">Select one of the Linux distributions.</span></span> <span data-ttu-id="b74ee-201">Для этого примера выберите SLES 12 BYOS.</span><span class="sxs-lookup"><span data-stu-id="b74ee-201">For this example, select SLES 12 BYOS</span></span>
    1. <span data-ttu-id="b74ee-202">Тип базы данных.</span><span class="sxs-lookup"><span data-stu-id="b74ee-202">Db Type</span></span>  
       <span data-ttu-id="b74ee-203">Выберите HANA.</span><span class="sxs-lookup"><span data-stu-id="b74ee-203">Select HANA</span></span>
    1. <span data-ttu-id="b74ee-204">Размер системы SAP</span><span class="sxs-lookup"><span data-stu-id="b74ee-204">Sap System Size</span></span>  
       <span data-ttu-id="b74ee-205">Количество систем SAP, которые будет содержать система.</span><span class="sxs-lookup"><span data-stu-id="b74ee-205">The amount of SAPS the new system will provide.</span></span> <span data-ttu-id="b74ee-206">Если вы не знаете, сколько систем SAP потребуется для системы, обратитесь к партнеру по технологиям SAP или к системному интегратору SAP.</span><span class="sxs-lookup"><span data-stu-id="b74ee-206">If you are not sure how many SAPS the system will require, please ask your SAP Technology Partner or System Integrator</span></span>
    1. <span data-ttu-id="b74ee-207">Доступность системы</span><span class="sxs-lookup"><span data-stu-id="b74ee-207">System Availability</span></span>  
       <span data-ttu-id="b74ee-208">Выберите высокую доступность</span><span class="sxs-lookup"><span data-stu-id="b74ee-208">Select HA</span></span>
    1. <span data-ttu-id="b74ee-209">Имя пользователя и пароль администратора</span><span class="sxs-lookup"><span data-stu-id="b74ee-209">Admin Username and Admin Password</span></span>  
       <span data-ttu-id="b74ee-210">Создается учетная запись пользователя, которую можно использовать для входа на компьютер.</span><span class="sxs-lookup"><span data-stu-id="b74ee-210">A new user is created that can be used to log on to the machine.</span></span>
    1. <span data-ttu-id="b74ee-211">Новая или имеющаяся подсеть</span><span class="sxs-lookup"><span data-stu-id="b74ee-211">New Or Existing Subnet</span></span>  
       <span data-ttu-id="b74ee-212">Определяет, следует ли создать виртуальную сеть и подсеть или использовать имеющуюся подсеть.</span><span class="sxs-lookup"><span data-stu-id="b74ee-212">Determines whether a new virtual network and subnet should be created or an existing subnet should be used.</span></span> <span data-ttu-id="b74ee-213">При наличии виртуальной сети, подключенной к локальной сети, выберите ее.</span><span class="sxs-lookup"><span data-stu-id="b74ee-213">If you already have a virtual network that is connected to your on-premises network, select existing.</span></span>
    1. <span data-ttu-id="b74ee-214">Идентификатор подсети</span><span class="sxs-lookup"><span data-stu-id="b74ee-214">Subnet Id</span></span>  
    <span data-ttu-id="b74ee-215">Идентификатор подсети, к которой следует подключить виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="b74ee-215">The ID of the subnet to which the virtual machines should be connected to.</span></span> <span data-ttu-id="b74ee-216">Выберите подсеть виртуальной сети VPN или Express Route, чтобы подключить виртуальную машину к локальной сети.</span><span class="sxs-lookup"><span data-stu-id="b74ee-216">Select the subnet of your VPN or Express Route virtual network to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="b74ee-217">Идентификатор обычно выглядит следующим образом: /subscriptions/`<subscription id`>/resourceGroups/`<resource group name`>/providers/Microsoft.Network/virtualNetworks/`<virtual network name`>/subnets/`<subnet name`>.</span><span class="sxs-lookup"><span data-stu-id="b74ee-217">The ID usually looks like /subscriptions/`<subscription id`>/resourceGroups/`<resource group name`>/providers/Microsoft.Network/virtualNetworks/`<virtual network name`>/subnets/`<subnet name`></span></span>

## <a name="setting-up-linux-ha"></a><span data-ttu-id="b74ee-218">Настройка высокого уровня доступности Linux</span><span class="sxs-lookup"><span data-stu-id="b74ee-218">Setting up Linux HA</span></span>

<span data-ttu-id="b74ee-219">Ниже приведены элементы с префиксами: [A] — применяется ко всем узлам, [1] — применяется только к узлу 1, [2] — применяется только к узлу 2.</span><span class="sxs-lookup"><span data-stu-id="b74ee-219">The following items are prefixed with either [A] - applicable to all nodes, [1] - only applicable to node 1 or [2] - only applicable to node 2.</span></span>

1. <span data-ttu-id="b74ee-220">[A] Только SLES for SAP BYOS. Зарегистрируйте SLES, чтобы иметь возможность использовать репозитории.</span><span class="sxs-lookup"><span data-stu-id="b74ee-220">[A] SLES for SAP BYOS only - Register SLES to be able to use the repositories</span></span>
1. <span data-ttu-id="b74ee-221">[A] Только SLES for SAP BYOS. Добавьте модуль public-cloud.</span><span class="sxs-lookup"><span data-stu-id="b74ee-221">[A] SLES for SAP BYOS only - Add public-cloud module</span></span>
1. <span data-ttu-id="b74ee-222">[A] Обновите SLES.</span><span class="sxs-lookup"><span data-stu-id="b74ee-222">[A] Update SLES</span></span>
    ```bash
    sudo zypper update

    ```

1. <span data-ttu-id="b74ee-223">[1] Включите доступ по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="b74ee-223">[1] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy the public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. <span data-ttu-id="b74ee-224">[2] Включите доступ по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="b74ee-224">[2] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa

    # insert the public key you copied in the last step into the authorized keys file on the second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy the public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. <span data-ttu-id="b74ee-225">[1] Включите доступ по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="b74ee-225">[1] Enable ssh access</span></span>
    ```bash
    # insert the public key you copied in the last step into the authorized keys file on the first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. <span data-ttu-id="b74ee-226">[A] Установите расширение для обеспечения высокого уровня доступности.</span><span class="sxs-lookup"><span data-stu-id="b74ee-226">[A] Install HA extension</span></span>
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. <span data-ttu-id="b74ee-227">[A] Настройте разметку дисков.</span><span class="sxs-lookup"><span data-stu-id="b74ee-227">[A] Setup disk layout</span></span>
    1. <span data-ttu-id="b74ee-228">Диспетчер логических томов</span><span class="sxs-lookup"><span data-stu-id="b74ee-228">LVM</span></span>  
    <span data-ttu-id="b74ee-229">Обычно для томов, предназначенных для хранения данных и файлов журнала, рекомендуется использовать LVM.</span><span class="sxs-lookup"><span data-stu-id="b74ee-229">We generally recommend to use LVM for volumes that store data and log files.</span></span> <span data-ttu-id="b74ee-230">В приведенном ниже примере предполагается, что к виртуальным машинам подключены четыре диска данных, которые следует использовать для создания двух томов.</span><span class="sxs-lookup"><span data-stu-id="b74ee-230">The example below assumes that the virtual machines have four data disks attached that should be used to create two volumes.</span></span>
        * <span data-ttu-id="b74ee-231">Создайте физические тома для всех дисков, которые вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="b74ee-231">Create physical volumes for all disks that you want to use.</span></span>
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * <span data-ttu-id="b74ee-232">Создайте группу томов для файлов данных, одну группу томов для файлов журнала и одну — для общей папки SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="b74ee-232">Create a volume group for the data files, one volume group for the log files and one for the shared directory of SAP HANA</span></span>
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * <span data-ttu-id="b74ee-233">Создайте логические тома.</span><span class="sxs-lookup"><span data-stu-id="b74ee-233">Create the logical volumes</span></span>
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * <span data-ttu-id="b74ee-234">Создайте каталоги подключения и скопируйте UUID всех логических томов.</span><span class="sxs-lookup"><span data-stu-id="b74ee-234">Create the mount directories and copy the UUID of all logical volumes</span></span>
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down the id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * <span data-ttu-id="b74ee-235">Создайте записи fstab для трех логических томов.</span><span class="sxs-lookup"><span data-stu-id="b74ee-235">Create fstab entries for the three logical volumes</span></span>
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    <span data-ttu-id="b74ee-236">Вставьте эту строку в /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="b74ee-236">Insert this line to /etc/fstab</span></span>
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * <span data-ttu-id="b74ee-237">Подключите новые тома.</span><span class="sxs-lookup"><span data-stu-id="b74ee-237">Mount the new volumes</span></span>
    <pre><code>
    sudo mount -a
    </code></pre>
    1. <span data-ttu-id="b74ee-238">Обычные диски</span><span class="sxs-lookup"><span data-stu-id="b74ee-238">Plain Disks</span></span>  
       <span data-ttu-id="b74ee-239">Для небольших или демонстрационных систем файлы данных и журналов HANA можно поместить на один диск.</span><span class="sxs-lookup"><span data-stu-id="b74ee-239">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="b74ee-240">Приведенные ниже команды создают раздел/dev/sdc и форматируют его для файловой системы XFS.</span><span class="sxs-lookup"><span data-stu-id="b74ee-240">The following commands create a partition on /dev/sdc and format it with xfs.</span></span>
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-the-id-of-devsdc1"></a><span data-ttu-id="b74ee-241">write down the id of /dev/sdc1</span><span class="sxs-lookup"><span data-stu-id="b74ee-241">write down the id of /dev/sdc1</span></span>
    <span data-ttu-id="b74ee-242">sudo /sbin/blkid  sudo vi /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="b74ee-242">sudo /sbin/blkid  sudo vi /etc/fstab</span></span>
    ```

    Insert this line to /etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create the target directory and mount the disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. <span data-ttu-id="b74ee-243">[A] Настройте разрешение имен узлов для всех узлов.</span><span class="sxs-lookup"><span data-stu-id="b74ee-243">[A] Setup host name resolution for all hosts</span></span>  
    <span data-ttu-id="b74ee-244">Можно использовать DNS-сервер или внести изменения в файл /etc/hosts на всех узлах.</span><span class="sxs-lookup"><span data-stu-id="b74ee-244">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="b74ee-245">В этом примере показано, как использовать файл /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="b74ee-245">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="b74ee-246">Замените IP-адрес и имя узла в следующих командах.</span><span class="sxs-lookup"><span data-stu-id="b74ee-246">Replace the IP address and the hostname in the following commands</span></span>
    ```bash
    sudo vi /etc/hosts
    ```
    <span data-ttu-id="b74ee-247">Вставьте следующие строки в /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="b74ee-247">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="b74ee-248">Измените IP-адрес и имя узла в соответствии со своей средой.</span><span class="sxs-lookup"><span data-stu-id="b74ee-248">Change the IP address and hostname to match your environment</span></span>    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. <span data-ttu-id="b74ee-249">[1] Установите кластер.</span><span class="sxs-lookup"><span data-stu-id="b74ee-249">[1] Install Cluster</span></span>
    ```bash
    sudo ha-cluster-init
    
    # Do you want to continue anyway? [y/N] -> y
    # Network address to bind to (e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish to use SBD? [y/N] -> N
    # Do you wish to configure an administration IP? [y/N] -> N
    ```
        
1. <span data-ttu-id="b74ee-250">[2] Добавьте узел в кластер.</span><span class="sxs-lookup"><span data-stu-id="b74ee-250">[2] Add node to cluster</span></span>
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured to start at system boot.
    # WARNING: No watchdog device found. If SBD is used, the cluster will be unable to start without a watchdog.
    # Do you want to continue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. <span data-ttu-id="b74ee-251">[A] Измените пароль hacluster, введя тот же пароль.</span><span class="sxs-lookup"><span data-stu-id="b74ee-251">[A] Change hacluster password to the same password</span></span>
    ```bash
    sudo passwd hacluster
    
    ```

1. <span data-ttu-id="b74ee-252">[A] Настройте corosync для использование другого транспорта и добавьте список узлов.</span><span class="sxs-lookup"><span data-stu-id="b74ee-252">[A] Configure corosync to use other transport and add nodelist.</span></span> <span data-ttu-id="b74ee-253">Иначе кластер не будет работать.</span><span class="sxs-lookup"><span data-stu-id="b74ee-253">Cluster will not work otherwise.</span></span>
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

    <span data-ttu-id="b74ee-254">Добавьте в этот файл приведенное ниже содержимое, выделенное полужирным шрифтом.</span><span class="sxs-lookup"><span data-stu-id="b74ee-254">Add the following bold content to the file.</span></span>
    
    <pre><code> 
    [...]
      interface { 
          [...] 
      }
      <b>transport:      udpu</b>
    } 
    <b>nodelist {
      node {
        ring0_addr:     < ip address of node 1 >
      }
      node {
        ring0_addr:     < ip address of node 2 > 
      } 
    }</b>
    logging {
      [...]
    </code></pre>

    <span data-ttu-id="b74ee-255">Затем перезапустите службу corosync.</span><span class="sxs-lookup"><span data-stu-id="b74ee-255">Then restart the corosync service</span></span>

    ```bash
    sudo service corosync restart
    
    ```

1. <span data-ttu-id="b74ee-256">[A] Установите пакеты для обеспечения высокого уровня доступности HANA.</span><span class="sxs-lookup"><span data-stu-id="b74ee-256">[A] Install HANA HA packages</span></span>  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a><span data-ttu-id="b74ee-257">Установка SAP HANA</span><span class="sxs-lookup"><span data-stu-id="b74ee-257">Installing SAP HANA</span></span>

<span data-ttu-id="b74ee-258">Выполните указания в главе 4 [руководства по оптимизации производительности системной репликации SAP HANA][suse-hana-ha-guide], чтобы установить системную репликацию SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="b74ee-258">Follow chapter 4 of the [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] to install SAP HANA System Replication.</span></span>

1. <span data-ttu-id="b74ee-259">[A] Запустите hdblcm с DVD-диска HANA.</span><span class="sxs-lookup"><span data-stu-id="b74ee-259">[A] Run hdblcm from the HANA DVD</span></span>
    * <span data-ttu-id="b74ee-260">Выберите установку (1).</span><span class="sxs-lookup"><span data-stu-id="b74ee-260">Choose installation -> 1</span></span>
    * <span data-ttu-id="b74ee-261">Выберите дополнительные компоненты для установки (1).</span><span class="sxs-lookup"><span data-stu-id="b74ee-261">Select additional components for installation -> 1</span></span>
    * <span data-ttu-id="b74ee-262">Введите путь установки [/hana/shared] и нажмите клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="b74ee-262">Enter Installation Path [/hana/shared]: -> ENTER</span></span>
    * <span data-ttu-id="b74ee-263">Введите имя локального узла [..] и нажмите клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="b74ee-263">Enter Local Host Name [..]: -> ENTER</span></span>
    * <span data-ttu-id="b74ee-264">"Do you want to add additional hosts to the system? (y/n)"</span><span class="sxs-lookup"><span data-stu-id="b74ee-264">Do you want to add additional hosts to the system?</span></span> <span data-ttu-id="b74ee-265">(Вы хотите добавить дополнительные узлы в систему? (Да/нет)). Нажмите клавишу n и клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="b74ee-265">(y/n) [n]: -> ENTER</span></span>
    * <span data-ttu-id="b74ee-266">Введите идентификатор системы SAP HANA: <SID of HANA e.g. HDB></span><span class="sxs-lookup"><span data-stu-id="b74ee-266">Enter SAP HANA System ID: <SID of HANA e.g. HDB></span></span>
    * <span data-ttu-id="b74ee-267">Введите номер экземпляра [00].</span><span class="sxs-lookup"><span data-stu-id="b74ee-267">Enter Instance Number [00]:</span></span>   
  <span data-ttu-id="b74ee-268">Номер экземпляра HANA.</span><span class="sxs-lookup"><span data-stu-id="b74ee-268">HANA Instance number.</span></span> <span data-ttu-id="b74ee-269">Введите 03, если вы использовали шаблон Azure или пример выше.</span><span class="sxs-lookup"><span data-stu-id="b74ee-269">Use 03 if you used the Azure Template or followed the example above</span></span>
    * <span data-ttu-id="b74ee-270">Выберите режим базы данных и введите индекс [1], затем нажмите клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="b74ee-270">Select Database Mode / Enter Index [1]: -> ENTER</span></span>
    * <span data-ttu-id="b74ee-271">Выберите использование системы и введите индекс [4].</span><span class="sxs-lookup"><span data-stu-id="b74ee-271">Select System Usage / Enter Index [4]:</span></span>  
  <span data-ttu-id="b74ee-272">Выберите использование системы.</span><span class="sxs-lookup"><span data-stu-id="b74ee-272">Select the system Usage</span></span>
    * <span data-ttu-id="b74ee-273">Введите расположение томов данных [/hana/data/HDB], затем нажмите клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="b74ee-273">Enter Location of Data Volumes [/hana/data/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="b74ee-274">Введите расположение томов журнала [/hana/log/HDB], затем нажмите клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="b74ee-274">Enter Location of Log Volumes [/hana/log/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="b74ee-275">"Restrict maximum memory allocation?"</span><span class="sxs-lookup"><span data-stu-id="b74ee-275">Restrict maximum memory allocation?</span></span> <span data-ttu-id="b74ee-276">(Ограничить максимальный объем выделяемой памяти?) Нажмите клавишу n и клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="b74ee-276">[n]: -> ENTER</span></span>
    * <span data-ttu-id="b74ee-277">Введите имя узла сертификатов для узла "…".</span><span class="sxs-lookup"><span data-stu-id="b74ee-277">Enter Certificate Host Name For Host '...'</span></span> <span data-ttu-id="b74ee-278">[...]: нажмите клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="b74ee-278">[...]: -> ENTER</span></span>
    * <span data-ttu-id="b74ee-279">Введите пароль пользователя агента узла SAP (sapadm).</span><span class="sxs-lookup"><span data-stu-id="b74ee-279">Enter SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="b74ee-280">Подтвердите пароль пользователя агента узла SAP (sapadm).</span><span class="sxs-lookup"><span data-stu-id="b74ee-280">Confirm SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="b74ee-281">Введите пароль системного администратора (hdbadm).</span><span class="sxs-lookup"><span data-stu-id="b74ee-281">Enter System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="b74ee-282">Подтвердите пароль системного администратора (hdbadm).</span><span class="sxs-lookup"><span data-stu-id="b74ee-282">Confirm System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="b74ee-283">Введите домашний каталог системного администратора [/usr/sap/HDB/home], затем нажмите клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="b74ee-283">Enter System Administrator Home Directory [/usr/sap/HDB/home]: -> ENTER</span></span>
    * <span data-ttu-id="b74ee-284">Укажите оболочку для входа администратора системы [/bin/sh] и нажмите клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="b74ee-284">Enter System Administrator Login Shell [/bin/sh]: -> ENTER</span></span>
    * <span data-ttu-id="b74ee-285">Введите идентификатор пользователя администратора системы [1001] и нажмите клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="b74ee-285">Enter System Administrator User ID [1001]: -> ENTER</span></span>
    * <span data-ttu-id="b74ee-286">Введите идентификатор для группы пользователей (sapsys) [79], затем нажмите клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="b74ee-286">Enter ID of User Group (sapsys) [79]: -> ENTER</span></span>
    * <span data-ttu-id="b74ee-287">Введите пароль пользователя базы данных (SYSTEM).</span><span class="sxs-lookup"><span data-stu-id="b74ee-287">Enter Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="b74ee-288">Подтвердите пароль пользователя базы данных (SYSTEM).</span><span class="sxs-lookup"><span data-stu-id="b74ee-288">Confirm Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="b74ee-289">"Restart system after machine reboot?"</span><span class="sxs-lookup"><span data-stu-id="b74ee-289">Restart system after machine reboot?</span></span> <span data-ttu-id="b74ee-290">(Перезапустить систему после перезагрузки компьютера?) Нажмите клавишу n и клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="b74ee-290">[n]: -> ENTER</span></span>
    * <span data-ttu-id="b74ee-291">"Do you want to continue? (y/n)"</span><span class="sxs-lookup"><span data-stu-id="b74ee-291">Do you want to continue?</span></span> <span data-ttu-id="b74ee-292">(Вы действительно хотите продолжить? (Да/нет)).</span><span class="sxs-lookup"><span data-stu-id="b74ee-292">(y/n):</span></span>  
  <span data-ttu-id="b74ee-293">Просмотрите сводку и нажмите клавишу y, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="b74ee-293">Validate the summary and enter y to continue</span></span>
1. <span data-ttu-id="b74ee-294">[A] Обновите агент узла SAP.</span><span class="sxs-lookup"><span data-stu-id="b74ee-294">[A] Upgrade SAP Host Agent</span></span>  
  <span data-ttu-id="b74ee-295">Скачайте последний архив агента узла SAP с сайта [SAP Softwarecenter][sap-swcenter] и выполните следующую команду, чтобы обновить агент.</span><span class="sxs-lookup"><span data-stu-id="b74ee-295">Download the latest SAP Host Agent archive from the [SAP Softwarecenter][sap-swcenter] and run the following command to upgrade the agent.</span></span> <span data-ttu-id="b74ee-296">Замените путь к архиву, указав скачанный файл.</span><span class="sxs-lookup"><span data-stu-id="b74ee-296">Replace the path to the archive to point to the file you downloaded.</span></span>
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path to SAP Host Agent SAR>
    ```

1. <span data-ttu-id="b74ee-297">[1] Создайте репликацию HANA (в качестве привилегированного пользователя).</span><span class="sxs-lookup"><span data-stu-id="b74ee-297">[1] Create HANA replication (as root)</span></span>  
    <span data-ttu-id="b74ee-298">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b74ee-298">Run the following command.</span></span> <span data-ttu-id="b74ee-299">Обязательно замените строки, выделенные полужирным шрифтом (идентификатор системы HANA HDB и номер экземпляра 03), значениями для своей устанавливаемой системы.</span><span class="sxs-lookup"><span data-stu-id="b74ee-299">Make sure to replace bold strings (HANA System ID HDB and instance number 03) with the values of your SAP HANA installation.</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN TO <b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. <span data-ttu-id="b74ee-300">[A] Создайте запись хранилища ключей (в качестве привилегированного пользователя).</span><span class="sxs-lookup"><span data-stu-id="b74ee-300">[A] Create keystore entry (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. <span data-ttu-id="b74ee-301">[1] Создайте резервную копию базы данных (в качестве привилегированного пользователя).</span><span class="sxs-lookup"><span data-stu-id="b74ee-301">[1] Backup database (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. <span data-ttu-id="b74ee-302">[1] Переключитесь на пользователя sapsid (например, hdbadm) и создайте первичный сайт.</span><span class="sxs-lookup"><span data-stu-id="b74ee-302">[1] Switch to the sapsid user (for example hdbadm) and create the primary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. <span data-ttu-id="b74ee-303">[2] Переключитесь на пользователя sapsid (например, hdbadm) и создайте вторичный сайт.</span><span class="sxs-lookup"><span data-stu-id="b74ee-303">[2] Switch to the sapsid user (for example hdbadm) and create the secondary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a><span data-ttu-id="b74ee-304">Настройка платформы кластера</span><span class="sxs-lookup"><span data-stu-id="b74ee-304">Configure Cluster Framework</span></span>

<span data-ttu-id="b74ee-305">Измените параметры по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b74ee-305">Change the default settings</span></span>

<pre>
sudo vi crm-defaults.txt
# enter the following to crm-defaults.txt
<code>
property $id="cib-bootstrap-options" \
  no-quorum-policy="ignore" \
  stonith-enabled="true" \
  stonith-action="reboot" \
  stonith-timeout="150s"
rsc_defaults $id="rsc-options" \
  resource-stickiness="1000" \
  migration-threshold="5000"
op_defaults $id="op-options" \
  timeout="600"
</code>

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="b74ee-306">now we load the file to the cluster</span><span class="sxs-lookup"><span data-stu-id="b74ee-306">now we load the file to the cluster</span></span>
<span data-ttu-id="b74ee-307">sudo crm configure load update crm-defaults.txt</span><span class="sxs-lookup"><span data-stu-id="b74ee-307">sudo crm configure load update crm-defaults.txt</span></span>
</pre>

### <a name="create-stonith-device"></a><span data-ttu-id="b74ee-308">Создание устройства STONITH</span><span class="sxs-lookup"><span data-stu-id="b74ee-308">Create STONITH device</span></span>

<span data-ttu-id="b74ee-309">Устройство STONITH использует субъект-службу для авторизации в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b74ee-309">The STONITH device uses a Service Principal to authorize against Microsoft Azure.</span></span> <span data-ttu-id="b74ee-310">Чтобы создать субъект-службу, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="b74ee-310">Please follow these steps to create a Service Principal.</span></span>

1. <span data-ttu-id="b74ee-311">Перейдите на портал <https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="b74ee-311">Go to <https://portal.azure.com></span></span>
1. <span data-ttu-id="b74ee-312">Откройте колонку "Azure Active Directory".</span><span class="sxs-lookup"><span data-stu-id="b74ee-312">Open the Azure Active Directory blade</span></span>  
   <span data-ttu-id="b74ee-313">Перейдите в колонку "Свойства" и запишите идентификатор каталога.</span><span class="sxs-lookup"><span data-stu-id="b74ee-313">Go to Properties and write down the Directory Id.</span></span> <span data-ttu-id="b74ee-314">Это **идентификатор клиента**.</span><span class="sxs-lookup"><span data-stu-id="b74ee-314">This is the **tenant id**.</span></span>
1. <span data-ttu-id="b74ee-315">Щелкните "Регистрация приложений".</span><span class="sxs-lookup"><span data-stu-id="b74ee-315">Click App registrations</span></span>
1. <span data-ttu-id="b74ee-316">Нажмите "Добавить"</span><span class="sxs-lookup"><span data-stu-id="b74ee-316">Click Add</span></span>
1. <span data-ttu-id="b74ee-317">Введите имя, выберите тип приложения "Веб-приложения или API", введите URL-адрес входа (например. http://localhost) и нажмите кнопку "Создать".</span><span class="sxs-lookup"><span data-stu-id="b74ee-317">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="b74ee-318">URL-адрес входа не используется и может быть любым допустимым URL-адресом.</span><span class="sxs-lookup"><span data-stu-id="b74ee-318">The sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="b74ee-319">Выберите новое приложение и щелкните "Ключи" на вкладке "Параметры".</span><span class="sxs-lookup"><span data-stu-id="b74ee-319">Select the new App and click Keys in the Settings tab</span></span>
1. <span data-ttu-id="b74ee-320">Введите описание нового ключа, выберите "Срок действия не ограничен" и нажмите кнопку "Сохранить".</span><span class="sxs-lookup"><span data-stu-id="b74ee-320">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="b74ee-321">Запишите его значение.</span><span class="sxs-lookup"><span data-stu-id="b74ee-321">Write down the Value.</span></span> <span data-ttu-id="b74ee-322">Он используется в качестве **пароля** субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="b74ee-322">It is used as the **password** for the Service Principal</span></span>
1. <span data-ttu-id="b74ee-323">Запишите идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="b74ee-323">Write down the Application Id.</span></span> <span data-ttu-id="b74ee-324">Он используется в качестве имени пользователя (**идентификатора для входа** в следующих шагах) субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="b74ee-324">It is used as the username (**login id** in the steps below) of the Service Principal</span></span>

<span data-ttu-id="b74ee-325">У субъекта-службы по умолчанию нет разрешений на доступ к ресурсам Azure.</span><span class="sxs-lookup"><span data-stu-id="b74ee-325">The Service Principal does not have permissions to access your Azure resources by default.</span></span> <span data-ttu-id="b74ee-326">Необходимо предоставить ему разрешения на запуск и остановку (освобождение) всех виртуальных машин кластера.</span><span class="sxs-lookup"><span data-stu-id="b74ee-326">You need to give the Service Principal permissions to start and stop (deallocate) all virtual machines of the cluster.</span></span>

1. <span data-ttu-id="b74ee-327">Перейдите на портал https://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="b74ee-327">Go to https://portal.azure.com</span></span>
1. <span data-ttu-id="b74ee-328">Откройте колонку "Все ресурсы".</span><span class="sxs-lookup"><span data-stu-id="b74ee-328">Open the All resources blade</span></span>
1. <span data-ttu-id="b74ee-329">Выберите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="b74ee-329">Select the virtual machine</span></span>
1. <span data-ttu-id="b74ee-330">Выберите "Управление доступом (IAM)".</span><span class="sxs-lookup"><span data-stu-id="b74ee-330">Click Access control (IAM)</span></span>
1. <span data-ttu-id="b74ee-331">Нажмите "Добавить"</span><span class="sxs-lookup"><span data-stu-id="b74ee-331">Click Add</span></span>
1. <span data-ttu-id="b74ee-332">Выберите роль "Владелец".</span><span class="sxs-lookup"><span data-stu-id="b74ee-332">Select the role Owner</span></span>
1. <span data-ttu-id="b74ee-333">Введите имя созданного ранее приложения.</span><span class="sxs-lookup"><span data-stu-id="b74ee-333">Enter the name of the application you created above</span></span>
1. <span data-ttu-id="b74ee-334">Нажмите кнопку "ОК"</span><span class="sxs-lookup"><span data-stu-id="b74ee-334">Click OK</span></span>

<span data-ttu-id="b74ee-335">После изменения разрешений для виртуальных машин можно настроить устройства STONITH в кластере.</span><span class="sxs-lookup"><span data-stu-id="b74ee-335">After you edited the permissions for the virtual machines, you can configure the STONITH devices in the cluster.</span></span>

<pre>
sudo vi crm-fencing.txt
# enter the following to crm-fencing.txt
# replace the bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="b74ee-336">now we load the file to the cluster</span><span class="sxs-lookup"><span data-stu-id="b74ee-336">now we load the file to the cluster</span></span>
<span data-ttu-id="b74ee-337">sudo crm configure load update crm-fencing.txt</span><span class="sxs-lookup"><span data-stu-id="b74ee-337">sudo crm configure load update crm-fencing.txt</span></span>
</pre>

### <a name="create-sap-hana-resources"></a><span data-ttu-id="b74ee-338">Создание ресурсов SAP HANA</span><span class="sxs-lookup"><span data-stu-id="b74ee-338">Create SAP HANA resources</span></span>

<pre>
sudo vi crm-saphanatop.txt
# enter the following to crm-saphana.txt
# replace the bold string with your instance number and HANA system id
<code>
primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHanaTopology \
    operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
    op monitor interval="10" timeout="600" \
    op start interval="0" timeout="600" \
    op stop interval="0" timeout="300" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"

clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"
</code>

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="b74ee-339">now we load the file to the cluster</span><span class="sxs-lookup"><span data-stu-id="b74ee-339">now we load the file to the cluster</span></span>
<span data-ttu-id="b74ee-340">sudo crm configure load update crm-saphanatop.txt</span><span class="sxs-lookup"><span data-stu-id="b74ee-340">sudo crm configure load update crm-saphanatop.txt</span></span>
</pre>

<pre>
sudo vi crm-saphana.txt
# enter the following to crm-saphana.txt
# replace the bold string with your instance number, HANA system id and the frontend IP address of the Azure load balancer. 
<code>
primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
    operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
    op start interval="0" timeout="3600" \
    op stop interval="0" timeout="3600" \
    op promote interval="0" timeout="3600" \
    op monitor interval="60" role="Master" timeout="700" \
    op monitor interval="61" role="Slave" timeout="700" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
    DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"

ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
    target-role="Started" interleave="true"

primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
    meta target-role="Started" is-managed="true" \ 
    operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
    op monitor interval="10s" timeout="20s" \ 
    params ip="<b>10.0.0.21</b>" 
primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
    params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
    op monitor timeout=20s interval=10 depth=0 
group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
 
colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  
order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
</code>

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="b74ee-341">now we load the file to the cluster</span><span class="sxs-lookup"><span data-stu-id="b74ee-341">now we load the file to the cluster</span></span>
<span data-ttu-id="b74ee-342">sudo crm configure load update crm-saphana.txt</span><span class="sxs-lookup"><span data-stu-id="b74ee-342">sudo crm configure load update crm-saphana.txt</span></span>
</pre>

### <a name="test-cluster-setup"></a><span data-ttu-id="b74ee-343">Проверка установки кластера</span><span class="sxs-lookup"><span data-stu-id="b74ee-343">Test cluster setup</span></span>
<span data-ttu-id="b74ee-344">В следующей главе описывается, как можно проверить конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="b74ee-344">The following chapter describe how you can test your setup.</span></span> <span data-ttu-id="b74ee-345">Для каждого теста предполагается, что он выполняется от имени привилегированного пользователя, а главный узел SAP HANA выполняется на виртуальной машине saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="b74ee-345">Every test assumes that you are root and the SAP HANA master is running on the virtual machine saphanavm1.</span></span>

#### <a name="fencing-test"></a><span data-ttu-id="b74ee-346">Тестирование ограждения</span><span class="sxs-lookup"><span data-stu-id="b74ee-346">Fencing Test</span></span>

<span data-ttu-id="b74ee-347">Можно проверить конфигурацию агента ограждения, отключив сетевой интерфейс на узле saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="b74ee-347">You can test the setup of the fencing agent by disabling the network interface on node saphanavm1.</span></span>

<pre><code>
sudo ifdown eth0
</code></pre>

<span data-ttu-id="b74ee-348">Виртуальная машина должна быть перезагружена или остановлена, в зависимости от конфигурации кластера.</span><span class="sxs-lookup"><span data-stu-id="b74ee-348">The virtual machine should now get restarted or stopped depending on your cluster configuration.</span></span>
<span data-ttu-id="b74ee-349">Если для параметра stonith-action задано значение off, то виртуальная машина будет остановлена, а ресурсы перенесены на работающую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="b74ee-349">If you set the stonith-action to off, the virtual machine will be stopped and the resources are migrated to the running virtual machine.</span></span>

<span data-ttu-id="b74ee-350">Если для параметра AUTOMATED_REGISTER задано значение false, то после повторного запуска виртуальной машины не удастся запустить ресурс SAP HANA на вторичном узле.</span><span class="sxs-lookup"><span data-stu-id="b74ee-350">Once you start the virtual machine again, the SAP HANA resource will fail to start as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="b74ee-351">В этом случае необходимо настроить экземпляр HANA как вторичный узел, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="b74ee-351">In this case, you need to configure the HANA instance as secondary by executing the following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop the HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back to root and cleanup the failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a><span data-ttu-id="b74ee-352">Тестирование отработки отказа вручную</span><span class="sxs-lookup"><span data-stu-id="b74ee-352">Testing a manual failover</span></span>

<span data-ttu-id="b74ee-353">Можно проверить отработку отказа вручную, остановив службу pacemaker на узле saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="b74ee-353">You can test a manual failover by stopping the pacemaker service on node saphanavm1.</span></span>
<pre><code>
service pacemaker stop
</code></pre>

<span data-ttu-id="b74ee-354">После отработки отказа можно снова запустить эту службу.</span><span class="sxs-lookup"><span data-stu-id="b74ee-354">After the failover, you can start the service again.</span></span> <span data-ttu-id="b74ee-355">Если для параметра AUTOMATED_REGISTER задано значение false, то ресурс SAP HANA на узле saphanavm1 не удастся запустить на вторичном узле.</span><span class="sxs-lookup"><span data-stu-id="b74ee-355">The SAP HANA resource on saphanavm1 will fail to start as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="b74ee-356">В этом случае необходимо настроить экземпляр HANA как вторичный узел, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="b74ee-356">In this case, you need to configure the HANA instance as secondary by executing the following command:</span></span>

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop the HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back to root and cleanup the failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a><span data-ttu-id="b74ee-357">Тестирование переноса</span><span class="sxs-lookup"><span data-stu-id="b74ee-357">Testing a migration</span></span>

<span data-ttu-id="b74ee-358">Можно перенести на главный узел SAP HANA, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="b74ee-358">You can migrate the SAP HANA master node by executing the following command</span></span>
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="b74ee-359">Она перенесет главный узел SAP HANA и группу, которая содержит виртуальный IP-адрес, на узел saphanavm2.</span><span class="sxs-lookup"><span data-stu-id="b74ee-359">This should migrate the SAP HANA master node and the group that contains the virtual IP address to saphanavm2.</span></span>
<span data-ttu-id="b74ee-360">Если для параметра AUTOMATED_REGISTER задано значение false, то ресурс SAP HANA на узле saphanavm1 не удастся запустить на вторичном узле.</span><span class="sxs-lookup"><span data-stu-id="b74ee-360">The SAP HANA resource on saphanavm1 will fail to start as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="b74ee-361">В этом случае необходимо настроить экземпляр HANA как вторичный узел, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="b74ee-361">In this case, you need to configure the HANA instance as secondary by executing the following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop the HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

<span data-ttu-id="b74ee-362">При переносе устанавливаются ограничения расположения, которые должны быть удалены.</span><span class="sxs-lookup"><span data-stu-id="b74ee-362">The migration creates location contraints that need to be deleted again.</span></span>

<pre><code>
crm configure edited

# delete location contraints that are named like the following contraint. You should have two contraints, one for the SAP HANA resource and one for the IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="b74ee-363">Необходимо также очистить состояние ресурса на вторичном узле.</span><span class="sxs-lookup"><span data-stu-id="b74ee-363">You also need to cleanup the state of the secondary node resource</span></span>

<pre><code>
# switch back to root and cleanup the failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a><span data-ttu-id="b74ee-364">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b74ee-364">Next steps</span></span>
* <span data-ttu-id="b74ee-365">[SAP NetWeaver на виртуальных машинах Windows. Руководство по планированию и внедрению][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="b74ee-365">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="b74ee-366">[Развертывание программного обеспечения SAP на виртуальных машинах Azure][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="b74ee-366">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="b74ee-367">[SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию СУБД][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="b74ee-367">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="b74ee-368">Дополнительные сведения об обеспечении высокого уровня доступности и планировании аварийного восстановления SAP HANA в Azure (крупные экземпляры) см. в [этой статье](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="b74ee-368">To learn how to establish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span> 
