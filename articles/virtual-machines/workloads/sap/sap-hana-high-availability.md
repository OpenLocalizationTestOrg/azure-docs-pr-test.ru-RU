---
title: "aaaHigh доступности из SAP HANA на виртуальных машинах Azure (ВМ) | Документы Microsoft"
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
ms.openlocfilehash: dcb9bb70594f9d97f8a888cec76300bcbe0bf1ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a><span data-ttu-id="cfc21-103">Высокий уровень доступности SAP HANA на виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="cfc21-103">High Availability of SAP HANA on Azure Virtual Machines (VMs)</span></span>

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

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

<span data-ttu-id="cfc21-113">Локально, можно использовать либо HANA системы репликации или использовать общее хранилище tooestablish высокого уровня доступности для SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="cfc21-113">On-premises, you can use either HANA System Replication or use shared storage tooestablish high availability for SAP HANA.</span></span>
<span data-ttu-id="cfc21-114">В настоящее время в Azure поддерживается только настройка системной репликации HANA.</span><span class="sxs-lookup"><span data-stu-id="cfc21-114">We currently only support setting up HANA System Replication on Azure.</span></span> <span data-ttu-id="cfc21-115">Для репликации SAP HANA используются один главный узел и по крайней мере один подчиненный узел.</span><span class="sxs-lookup"><span data-stu-id="cfc21-115">SAP HANA Replication consists of one master node and at least one slave node.</span></span> <span data-ttu-id="cfc21-116">Toohello изменения данных на главном узле hello, реплицируются узлы ведомый toohello синхронно или асинхронно.</span><span class="sxs-lookup"><span data-stu-id="cfc21-116">Changes toohello data on hello master node are replicated toohello slave nodes synchronously or asynchronously.</span></span>

<span data-ttu-id="cfc21-117">В этой статье описывается, как toodeploy hello виртуальных машин, Настройка hello виртуальных машин, установите framework hello кластера, Установка и настройка репликации системы SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="cfc21-117">This article describes how toodeploy hello virtual machines, configure hello virtual machines, install hello cluster framework, install and configure SAP HANA System Replication.</span></span>
<span data-ttu-id="cfc21-118">В конфигурациях пример hello установки команд номер экземпляра и т.д. 03 и используется идентификатор HDB HANA системы.</span><span class="sxs-lookup"><span data-stu-id="cfc21-118">In hello example configurations, installation commands etc. instance number 03 and HANA System ID HDB is used.</span></span>

<span data-ttu-id="cfc21-119">Следующие примечания по SAP и документы сначала hello чтения</span><span class="sxs-lookup"><span data-stu-id="cfc21-119">Read hello following SAP Notes and papers first</span></span>

* <span data-ttu-id="cfc21-120">примечание к SAP [1928533], которое содержит:</span><span class="sxs-lookup"><span data-stu-id="cfc21-120">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="cfc21-121">Список размеров виртуальных Машин Azure, которые поддерживаются для развертывания по SAP hello</span><span class="sxs-lookup"><span data-stu-id="cfc21-121">List of Azure VM sizes that are supported for hello deployment of SAP software</span></span>
  * <span data-ttu-id="cfc21-122">важные сведения о доступных ресурсах для каждого размера виртуальной машины Azure;</span><span class="sxs-lookup"><span data-stu-id="cfc21-122">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="cfc21-123">сведения о поддерживаемом программном обеспечении SAP и сочетаниях операционных систем и баз данных;</span><span class="sxs-lookup"><span data-stu-id="cfc21-123">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="cfc21-124">сведения о требуемой версии ядра SAP для Windows и Linux в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cfc21-124">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>
* <span data-ttu-id="cfc21-125">примечание к SAP [2015553], в котором описываются предварительные требования к SAP при развертывании программного обеспечения SAP в Azure;</span><span class="sxs-lookup"><span data-stu-id="cfc21-125">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="cfc21-126">Примечание SAP [2205917] содержит рекомендуемые параметры ОС для SUSE Linux Enterprise Server для приложений SAP.</span><span class="sxs-lookup"><span data-stu-id="cfc21-126">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="cfc21-127">Примечание SAP [1944799] содержит рекомендации для SAP HANA в SUSE Linux Enterprise Server для приложений SAP.</span><span class="sxs-lookup"><span data-stu-id="cfc21-127">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="cfc21-128">примечание к SAP [2178632], содержащее подробные сведения обо всех доступных метриках мониторинга для SAP в Azure;</span><span class="sxs-lookup"><span data-stu-id="cfc21-128">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="cfc21-129">Примечание SAP [2191498] имеет hello требуемая версия агента узла SAP для Linux в Azure.</span><span class="sxs-lookup"><span data-stu-id="cfc21-129">SAP Note [2191498] has hello required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="cfc21-130">примечание к SAP [2243692], содержащее сведения о лицензировании SAP в Linux в Azure;</span><span class="sxs-lookup"><span data-stu-id="cfc21-130">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="cfc21-131">примечание к SAP [1984787], содержащее общие сведения о SUSE Linux Enterprise Server 12;</span><span class="sxs-lookup"><span data-stu-id="cfc21-131">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="cfc21-132">Примечание SAP [1999351] имеет дополнительные диагностические сведения для hello расширение мониторинга Azure для SAP.</span><span class="sxs-lookup"><span data-stu-id="cfc21-132">SAP Note [1999351] has additional troubleshooting information for hello Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="cfc21-133">[вики-сайт сообщества SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes), содержащий все необходимые примечания к SAP для Linux;</span><span class="sxs-lookup"><span data-stu-id="cfc21-133">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="cfc21-134">[SAP NetWeaver на виртуальных машинах Windows. Руководство по планированию и внедрению][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="cfc21-134">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="cfc21-135">[Развертывание программного обеспечения SAP на виртуальных машинах Linux в Azure (эта статья)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="cfc21-135">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="cfc21-136">[SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию СУБД][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="cfc21-136">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="cfc21-137">[Сценарии оптимизированными SAP HANA SR производительности] [ suse-hana-ha-guide] hello руководство содержит все необходимые сведения tooset копирование репликации системы SAP HANA в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="cfc21-137">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] hello guide contains all required information tooset up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="cfc21-138">Используйте это руководство как основу.</span><span class="sxs-lookup"><span data-stu-id="cfc21-138">Use this guide as a baseline.</span></span>

## <a name="deploying-linux"></a><span data-ttu-id="cfc21-139">Развертывание Linux</span><span class="sxs-lookup"><span data-stu-id="cfc21-139">Deploying Linux</span></span>

<span data-ttu-id="cfc21-140">агент Hello ресурсов для SAP HANA включается в SUSE Linux Enterprise Server для приложений SAP.</span><span class="sxs-lookup"><span data-stu-id="cfc21-140">hello resource agent for SAP HANA is included in SUSE Linux Enterprise Server for SAP Applications.</span></span>
<span data-ttu-id="cfc21-141">Hello Azure Marketplace содержит изображение для SUSE Linux Enterprise Server 12 приложений SAP с BYOS (переведите свои собственные подписки), можно использовать toodeploy новых виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="cfc21-141">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 with BYOS (Bring Your Own Subscription) that you can use toodeploy new virtual machines.</span></span>

### <a name="manual-deployment"></a><span data-ttu-id="cfc21-142">Развертывание вручную</span><span class="sxs-lookup"><span data-stu-id="cfc21-142">Manual Deployment</span></span>

1. <span data-ttu-id="cfc21-143">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="cfc21-143">Create a Resource Group</span></span>
1. <span data-ttu-id="cfc21-144">Создайте виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="cfc21-144">Create a Virtual Network</span></span>
1. <span data-ttu-id="cfc21-145">Создание двух учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="cfc21-145">Create two Storage Accounts</span></span>
1. <span data-ttu-id="cfc21-146">Создание группы доступности.</span><span class="sxs-lookup"><span data-stu-id="cfc21-146">Create an Availability Set</span></span>  
   <span data-ttu-id="cfc21-147">Настройка максимального числа доменов обновления.</span><span class="sxs-lookup"><span data-stu-id="cfc21-147">Set max update domain</span></span>
1. <span data-ttu-id="cfc21-148">Создание подсистемы балансировки нагрузки (внутренней).</span><span class="sxs-lookup"><span data-stu-id="cfc21-148">Create a Load Balancer (internal)</span></span>  
   <span data-ttu-id="cfc21-149">Выбор виртуальной сети, созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="cfc21-149">Select VNET of step above</span></span>
1. <span data-ttu-id="cfc21-150">Создание виртуальной машины 1.</span><span class="sxs-lookup"><span data-stu-id="cfc21-150">Create Virtual Machine 1</span></span>  
   <span data-ttu-id="cfc21-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="cfc21-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="cfc21-152">SLES For SAP Applications 12 SP1 (BYOS).</span><span class="sxs-lookup"><span data-stu-id="cfc21-152">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="cfc21-153">Выбор учетной записи хранения 1.</span><span class="sxs-lookup"><span data-stu-id="cfc21-153">Select Storage Account 1</span></span>  
   <span data-ttu-id="cfc21-154">Выбор группы доступности.</span><span class="sxs-lookup"><span data-stu-id="cfc21-154">Select Availability Set</span></span>  
1. <span data-ttu-id="cfc21-155">Создание виртуальной машины 2.</span><span class="sxs-lookup"><span data-stu-id="cfc21-155">Create Virtual Machine 2</span></span>  
   <span data-ttu-id="cfc21-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="cfc21-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="cfc21-157">SLES For SAP Applications 12 SP1 (BYOS).</span><span class="sxs-lookup"><span data-stu-id="cfc21-157">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="cfc21-158">Выбор учетной записи хранения 2.</span><span class="sxs-lookup"><span data-stu-id="cfc21-158">Select Storage Account 2</span></span>   
   <span data-ttu-id="cfc21-159">Выбор группы доступности.</span><span class="sxs-lookup"><span data-stu-id="cfc21-159">Select Availability Set</span></span>  
1. <span data-ttu-id="cfc21-160">Добавление дисков данных.</span><span class="sxs-lookup"><span data-stu-id="cfc21-160">Add Data Disks</span></span>
1. <span data-ttu-id="cfc21-161">Настройка балансировки нагрузки hello</span><span class="sxs-lookup"><span data-stu-id="cfc21-161">Configure hello load balancer</span></span>
    1. <span data-ttu-id="cfc21-162">Создание пула внешних IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="cfc21-162">Create a frontend IP pool</span></span>
        1. <span data-ttu-id="cfc21-163">Откройте hello балансировки нагрузки, выберите пул IP-адресов переднего плана и нажмите кнопку Добавить</span><span class="sxs-lookup"><span data-stu-id="cfc21-163">Open hello load balancer, select frontend IP pool and click Add</span></span>
        1. <span data-ttu-id="cfc21-164">Введите имя hello hello нового внешнего интерфейса пула IP-адресов (например, hana-frontend)</span><span class="sxs-lookup"><span data-stu-id="cfc21-164">Enter hello name of hello new frontend IP pool (for example hana-frontend)</span></span>
       1. <span data-ttu-id="cfc21-165">Нажмите кнопку "ОК"</span><span class="sxs-lookup"><span data-stu-id="cfc21-165">Click OK</span></span>
        1. <span data-ttu-id="cfc21-166">После создания hello нового внешнего интерфейса пула IP-адресов, запишите его IP-адрес</span><span class="sxs-lookup"><span data-stu-id="cfc21-166">After hello new frontend IP pool is created, write down its IP address</span></span>
    1. <span data-ttu-id="cfc21-167">Создание внутреннего пула.</span><span class="sxs-lookup"><span data-stu-id="cfc21-167">Create a backend pool</span></span>
        1. <span data-ttu-id="cfc21-168">Откройте hello балансировки нагрузки, выберите внутренние пулы и нажмите кнопку Добавить</span><span class="sxs-lookup"><span data-stu-id="cfc21-168">Open hello load balancer, select backend pools and click Add</span></span>
        1. <span data-ttu-id="cfc21-169">Введите имя hello hello нового внутреннего пула (например hana-серверное приложение)</span><span class="sxs-lookup"><span data-stu-id="cfc21-169">Enter hello name of hello new backend pool (for example hana-backend)</span></span>
        1. <span data-ttu-id="cfc21-170">Щелкните "Добавить виртуальную машину".</span><span class="sxs-lookup"><span data-stu-id="cfc21-170">Click Add a virtual machine</span></span>
        1. <span data-ttu-id="cfc21-171">Выберите группу доступности, созданной ранее hello</span><span class="sxs-lookup"><span data-stu-id="cfc21-171">Select hello Availability Set you created earlier</span></span>
        1. <span data-ttu-id="cfc21-172">Выберите hello виртуальных машин кластера hello SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cfc21-172">Select hello virtual machines of hello SAP HANA cluster</span></span>
        1. <span data-ttu-id="cfc21-173">Нажмите кнопку "ОК"</span><span class="sxs-lookup"><span data-stu-id="cfc21-173">Click OK</span></span>
    1. <span data-ttu-id="cfc21-174">Создание пробы работоспособности</span><span class="sxs-lookup"><span data-stu-id="cfc21-174">Create a health probe</span></span>
       1. <span data-ttu-id="cfc21-175">Откройте hello балансировки нагрузки, выберите проверках работоспособности и нажмите кнопку Добавить</span><span class="sxs-lookup"><span data-stu-id="cfc21-175">Open hello load balancer, select health probes and click Add</span></span>
        1. <span data-ttu-id="cfc21-176">Введите имя hello hello новые проверки работоспособности (например, hana-hp)</span><span class="sxs-lookup"><span data-stu-id="cfc21-176">Enter hello name of hello new health probe (for example hana-hp)</span></span>
        1. <span data-ttu-id="cfc21-177">Выберите протокол TCP, порт 625**03**, интервал, равный 5, и порог состояния неработоспособности, равный 2.</span><span class="sxs-lookup"><span data-stu-id="cfc21-177">Select TCP as protocol, port 625**03**, keep Interval 5 and Unhealthy threshold 2</span></span>
        1. <span data-ttu-id="cfc21-178">Нажмите кнопку "ОК"</span><span class="sxs-lookup"><span data-stu-id="cfc21-178">Click OK</span></span>
    1. <span data-ttu-id="cfc21-179">Создание правил балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="cfc21-179">Create load balancing rules</span></span>
        1. <span data-ttu-id="cfc21-180">Откройте hello балансировки нагрузки, выберите правил балансировки нагрузки и нажмите кнопку Добавить</span><span class="sxs-lookup"><span data-stu-id="cfc21-180">Open hello load balancer, select load balancing rules and click Add</span></span>
        1. <span data-ttu-id="cfc21-181">Введите имя hello hello новое правило подсистемы балансировки нагрузки (например hana-балансировки нагрузки-3**03**15)</span><span class="sxs-lookup"><span data-stu-id="cfc21-181">Enter hello name of hello new load balancer rule (for example hana-lb-3**03**15)</span></span>
        1. <span data-ttu-id="cfc21-182">Выберите hello интерфейсный IP-адрес, внутренний пул и работоспособности проверки, созданную ранее (например, hana-frontend)</span><span class="sxs-lookup"><span data-stu-id="cfc21-182">Select hello frontend IP address, backend pool and health probe you created earlier (for example hana-frontend)</span></span>
        1. <span data-ttu-id="cfc21-183">Оставьте выбранным протокол TCP и введите порт 3**03**15.</span><span class="sxs-lookup"><span data-stu-id="cfc21-183">Keep protocol TCP, enter port 3**03**15</span></span>
        1. <span data-ttu-id="cfc21-184">Увеличьте время ожидания простоя too30 минут</span><span class="sxs-lookup"><span data-stu-id="cfc21-184">Increase idle timeout too30 minutes</span></span>
       1. <span data-ttu-id="cfc21-185">**Убедитесь, что tooenable плавающий IP-адрес**</span><span class="sxs-lookup"><span data-stu-id="cfc21-185">**Make sure tooenable Floating IP**</span></span>
        1. <span data-ttu-id="cfc21-186">Нажмите кнопку "ОК"</span><span class="sxs-lookup"><span data-stu-id="cfc21-186">Click OK</span></span>
        1. <span data-ttu-id="cfc21-187">Повторите приведенные выше действия hello для порта 3**03**17</span><span class="sxs-lookup"><span data-stu-id="cfc21-187">Repeat hello steps above for port 3**03**17</span></span>

### <a name="deploy-with-template"></a><span data-ttu-id="cfc21-188">Развертывание с помощью шаблона</span><span class="sxs-lookup"><span data-stu-id="cfc21-188">Deploy with template</span></span>
<span data-ttu-id="cfc21-189">Можно использовать один из шаблонов hello быстрого запуска на github toodeploy все необходимые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="cfc21-189">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="cfc21-190">шаблон Hello развертывает hello виртуальных машин, подсистемы балансировки нагрузки hello, доступности, и т. д. Выполните эти шаги toodeploy hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="cfc21-190">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="cfc21-191">Откройте hello [шаблона базы данных] [ template-multisid-db] или hello [схождение выполнено шаблона] [ template-converged] на портале Azure hello hello шаблона базы данных создает только hello правила балансировки нагрузки для базы данных, а также создает шаблон схождением hello hello правила балансировки нагрузки для ASCS/SCS и экземпляр ющих Методов (Linux).</span><span class="sxs-lookup"><span data-stu-id="cfc21-191">Open hello [database template][template-multisid-db] or hello [converged template][template-converged] on hello Azure Portal hello database template only creates hello load-balancing rules for a database whereas hello converged template also creates hello load-balancing rules for an ASCS/SCS and ERS (Linux only) instance.</span></span> <span data-ttu-id="cfc21-192">Если планируется tooinstall системы на основе SAP NetWeaver, а также tooinstall hello ASCS/SCS экземпляра на hello же машины, используйте hello [схождение выполнено шаблона][template-converged].</span><span class="sxs-lookup"><span data-stu-id="cfc21-192">If you plan tooinstall an SAP NetWeaver based system and you also want tooinstall hello ASCS/SCS instance on hello same machines, use hello [converged template][template-converged].</span></span>
1. <span data-ttu-id="cfc21-193">Введите следующие параметры hello</span><span class="sxs-lookup"><span data-stu-id="cfc21-193">Enter hello following parameters</span></span>
    1. <span data-ttu-id="cfc21-194">Идентификатор системы SAP</span><span class="sxs-lookup"><span data-stu-id="cfc21-194">Sap System Id</span></span>  
       <span data-ttu-id="cfc21-195">Введите системы SAP hello идентификатор hello требуется tooinstall системы SAP.</span><span class="sxs-lookup"><span data-stu-id="cfc21-195">Enter hello SAP system Id of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="cfc21-196">Hello идентификатор будет использоваться в качестве префикса hello ресурсы, которые развертываются.</span><span class="sxs-lookup"><span data-stu-id="cfc21-196">hello Id will be used as a prefix for hello resources that are deployed.</span></span>
    1. <span data-ttu-id="cfc21-197">Тип стека (применимо, только если используется шаблон конвергентной hello).</span><span class="sxs-lookup"><span data-stu-id="cfc21-197">Stack Type (only applicable if you use hello converged template)</span></span>  
       <span data-ttu-id="cfc21-198">Выберите тип стека SAP NetWeaver hello</span><span class="sxs-lookup"><span data-stu-id="cfc21-198">Select hello SAP NetWeaver stack type</span></span>
    1. <span data-ttu-id="cfc21-199">Тип ОС</span><span class="sxs-lookup"><span data-stu-id="cfc21-199">Os Type</span></span>  
       <span data-ttu-id="cfc21-200">Выберите один из hello ОС Linux.</span><span class="sxs-lookup"><span data-stu-id="cfc21-200">Select one of hello Linux distributions.</span></span> <span data-ttu-id="cfc21-201">Для этого примера выберите SLES 12 BYOS.</span><span class="sxs-lookup"><span data-stu-id="cfc21-201">For this example, select SLES 12 BYOS</span></span>
    1. <span data-ttu-id="cfc21-202">Тип базы данных.</span><span class="sxs-lookup"><span data-stu-id="cfc21-202">Db Type</span></span>  
       <span data-ttu-id="cfc21-203">Выберите HANA.</span><span class="sxs-lookup"><span data-stu-id="cfc21-203">Select HANA</span></span>
    1. <span data-ttu-id="cfc21-204">Размер системы SAP</span><span class="sxs-lookup"><span data-stu-id="cfc21-204">Sap System Size</span></span>  
       <span data-ttu-id="cfc21-205">предоставляет Hello объем SAPS hello новую систему.</span><span class="sxs-lookup"><span data-stu-id="cfc21-205">hello amount of SAPS hello new system will provide.</span></span> <span data-ttu-id="cfc21-206">Если вы не уверены, сколько SAPS hello систему необходимо, попросите вашего партнера технологии SAP или системные интеграторы</span><span class="sxs-lookup"><span data-stu-id="cfc21-206">If you are not sure how many SAPS hello system will require, please ask your SAP Technology Partner or System Integrator</span></span>
    1. <span data-ttu-id="cfc21-207">Доступность системы</span><span class="sxs-lookup"><span data-stu-id="cfc21-207">System Availability</span></span>  
       <span data-ttu-id="cfc21-208">Выберите высокую доступность</span><span class="sxs-lookup"><span data-stu-id="cfc21-208">Select HA</span></span>
    1. <span data-ttu-id="cfc21-209">Имя пользователя и пароль администратора</span><span class="sxs-lookup"><span data-stu-id="cfc21-209">Admin Username and Admin Password</span></span>  
       <span data-ttu-id="cfc21-210">Создать нового пользователя, можно использовать toolog на компьютере toohello.</span><span class="sxs-lookup"><span data-stu-id="cfc21-210">A new user is created that can be used toolog on toohello machine.</span></span>
    1. <span data-ttu-id="cfc21-211">Новая или имеющаяся подсеть</span><span class="sxs-lookup"><span data-stu-id="cfc21-211">New Or Existing Subnet</span></span>  
       <span data-ttu-id="cfc21-212">Определяет, следует ли создать виртуальную сеть и подсеть или использовать имеющуюся подсеть.</span><span class="sxs-lookup"><span data-stu-id="cfc21-212">Determines whether a new virtual network and subnet should be created or an existing subnet should be used.</span></span> <span data-ttu-id="cfc21-213">При наличии виртуальной сети, подключенной tooyour локальную сеть, выберите существующий.</span><span class="sxs-lookup"><span data-stu-id="cfc21-213">If you already have a virtual network that is connected tooyour on-premises network, select existing.</span></span>
    1. <span data-ttu-id="cfc21-214">Идентификатор подсети</span><span class="sxs-lookup"><span data-stu-id="cfc21-214">Subnet Id</span></span>  
    <span data-ttu-id="cfc21-215">Идентификатор Hello hello подсети toowhich hello виртуальных машин должен быть подключен к.</span><span class="sxs-lookup"><span data-stu-id="cfc21-215">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span> <span data-ttu-id="cfc21-216">Выберите подсеть hello VPN или Express Route виртуальной сети tooconnect hello виртуальной машины tooyour в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="cfc21-216">Select hello subnet of your VPN or Express Route virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="cfc21-217">Идентификатор Hello обычно выглядит /subscriptions/`<subscription id`> /resourceGroups/`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`></span><span class="sxs-lookup"><span data-stu-id="cfc21-217">hello ID usually looks like /subscriptions/`<subscription id`>/resourceGroups/`<resource group name`>/providers/Microsoft.Network/virtualNetworks/`<virtual network name`>/subnets/`<subnet name`></span></span>

## <a name="setting-up-linux-ha"></a><span data-ttu-id="cfc21-218">Настройка высокого уровня доступности Linux</span><span class="sxs-lookup"><span data-stu-id="cfc21-218">Setting up Linux HA</span></span>

<span data-ttu-id="cfc21-219">Hello следующих элементов начинаются с префикса либо [A] - применимо tooall узлов, [1] применяется только в случае toonode - применяется только в случае toonode 1 "или" [2] - 2.</span><span class="sxs-lookup"><span data-stu-id="cfc21-219">hello following items are prefixed with either [A] - applicable tooall nodes, [1] - only applicable toonode 1 or [2] - only applicable toonode 2.</span></span>

1. <span data-ttu-id="cfc21-220">[A] SLES для SAP BYOS только - регистрация SLES toobe может toouse hello репозиториев</span><span class="sxs-lookup"><span data-stu-id="cfc21-220">[A] SLES for SAP BYOS only - Register SLES toobe able toouse hello repositories</span></span>
1. <span data-ttu-id="cfc21-221">[A] Только SLES for SAP BYOS. Добавьте модуль public-cloud.</span><span class="sxs-lookup"><span data-stu-id="cfc21-221">[A] SLES for SAP BYOS only - Add public-cloud module</span></span>
1. <span data-ttu-id="cfc21-222">[A] Обновите SLES.</span><span class="sxs-lookup"><span data-stu-id="cfc21-222">[A] Update SLES</span></span>
    ```bash
    sudo zypper update

    ```

1. <span data-ttu-id="cfc21-223">[1] Включите доступ по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="cfc21-223">[1] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. <span data-ttu-id="cfc21-224">[2] Включите доступ по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="cfc21-224">[2] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa

    # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. <span data-ttu-id="cfc21-225">[1] Включите доступ по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="cfc21-225">[1] Enable ssh access</span></span>
    ```bash
    # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. <span data-ttu-id="cfc21-226">[A] Установите расширение для обеспечения высокого уровня доступности.</span><span class="sxs-lookup"><span data-stu-id="cfc21-226">[A] Install HA extension</span></span>
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. <span data-ttu-id="cfc21-227">[A] Настройте разметку дисков.</span><span class="sxs-lookup"><span data-stu-id="cfc21-227">[A] Setup disk layout</span></span>
    1. <span data-ttu-id="cfc21-228">Диспетчер логических томов</span><span class="sxs-lookup"><span data-stu-id="cfc21-228">LVM</span></span>  
    <span data-ttu-id="cfc21-229">Как правило, рекомендуется toouse LVM для томов, которые хранят данные и файлы журнала.</span><span class="sxs-lookup"><span data-stu-id="cfc21-229">We generally recommend toouse LVM for volumes that store data and log files.</span></span> <span data-ttu-id="cfc21-230">Hello примере предполагается, что hello виртуальные машины имеют четыре дисков данных, следует использовать toocreate два тома.</span><span class="sxs-lookup"><span data-stu-id="cfc21-230">hello example below assumes that hello virtual machines have four data disks attached that should be used toocreate two volumes.</span></span>
        * <span data-ttu-id="cfc21-231">Создание физических томов для всех дисков, которые должны toouse.</span><span class="sxs-lookup"><span data-stu-id="cfc21-231">Create physical volumes for all disks that you want toouse.</span></span>
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * <span data-ttu-id="cfc21-232">Создание группы томов для файлов данных hello, одна группа томов для файлов журнала hello и один для общей папки hello SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cfc21-232">Create a volume group for hello data files, one volume group for hello log files and one for hello shared directory of SAP HANA</span></span>
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * <span data-ttu-id="cfc21-233">Создать логические тома hello</span><span class="sxs-lookup"><span data-stu-id="cfc21-233">Create hello logical volumes</span></span>
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * <span data-ttu-id="cfc21-234">Создайте каталоги подключения hello и скопируйте hello UUID всех логических томов</span><span class="sxs-lookup"><span data-stu-id="cfc21-234">Create hello mount directories and copy hello UUID of all logical volumes</span></span>
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * <span data-ttu-id="cfc21-235">Создайте записи fstab для hello трех логических томах.</span><span class="sxs-lookup"><span data-stu-id="cfc21-235">Create fstab entries for hello three logical volumes</span></span>
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    <span data-ttu-id="cfc21-236">Вставьте этот строки слишком/и т. д/fstab</span><span class="sxs-lookup"><span data-stu-id="cfc21-236">Insert this line too/etc/fstab</span></span>
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * <span data-ttu-id="cfc21-237">Подключите новый тома hello</span><span class="sxs-lookup"><span data-stu-id="cfc21-237">Mount hello new volumes</span></span>
    <pre><code>
    sudo mount -a
    </code></pre>
    1. <span data-ttu-id="cfc21-238">Обычные диски</span><span class="sxs-lookup"><span data-stu-id="cfc21-238">Plain Disks</span></span>  
       <span data-ttu-id="cfc21-239">Для небольших или демонстрационных систем файлы данных и журналов HANA можно поместить на один диск.</span><span class="sxs-lookup"><span data-stu-id="cfc21-239">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="cfc21-240">Hello следующие команды создают секции на /dev/sdc и отформатируйте его xfs.</span><span class="sxs-lookup"><span data-stu-id="cfc21-240">hello following commands create a partition on /dev/sdc and format it with xfs.</span></span>
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-hello-id-of-devsdc1"></a><span data-ttu-id="cfc21-241">Запишите идентификатор hello /dev/sdc1</span><span class="sxs-lookup"><span data-stu-id="cfc21-241">write down hello id of /dev/sdc1</span></span>
    <span data-ttu-id="cfc21-242">sudo /sbin/blkid  sudo vi /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="cfc21-242">sudo /sbin/blkid  sudo vi /etc/fstab</span></span>
    ```

    Insert this line too/etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create hello target directory and mount hello disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. <span data-ttu-id="cfc21-243">[A] Настройте разрешение имен узлов для всех узлов.</span><span class="sxs-lookup"><span data-stu-id="cfc21-243">[A] Setup host name resolution for all hosts</span></span>  
    <span data-ttu-id="cfc21-244">Можно использовать DNS-сервер или измените hello/etc/hosts, на всех узлах.</span><span class="sxs-lookup"><span data-stu-id="cfc21-244">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="cfc21-245">В этом примере показано, как toouse hello файл/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="cfc21-245">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="cfc21-246">Замените hello IP-адрес и имя узла hello в hello, следующие команды</span><span class="sxs-lookup"><span data-stu-id="cfc21-246">Replace hello IP address and hello hostname in hello following commands</span></span>
    ```bash
    sudo vi /etc/hosts
    ```
    <span data-ttu-id="cfc21-247">Вставьте следующие строки слишком/и т. д/узлы hello.</span><span class="sxs-lookup"><span data-stu-id="cfc21-247">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="cfc21-248">Изменение среды toomatch hello IP адрес и имя узла</span><span class="sxs-lookup"><span data-stu-id="cfc21-248">Change hello IP address and hostname toomatch your environment</span></span>    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. <span data-ttu-id="cfc21-249">[1] Установите кластер.</span><span class="sxs-lookup"><span data-stu-id="cfc21-249">[1] Install Cluster</span></span>
    ```bash
    sudo ha-cluster-init
    
    # Do you want toocontinue anyway? [y/N] -> y
    # Network address toobind too(e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish toouse SBD? [y/N] -> N
    # Do you wish tooconfigure an administration IP? [y/N] -> N
    ```
        
1. <span data-ttu-id="cfc21-250">[2] Добавление toocluster узла</span><span class="sxs-lookup"><span data-stu-id="cfc21-250">[2] Add node toocluster</span></span>
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured toostart at system boot.
    # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
    # Do you want toocontinue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. <span data-ttu-id="cfc21-251">[A] toohello пароль hacluster изменить пароль</span><span class="sxs-lookup"><span data-stu-id="cfc21-251">[A] Change hacluster password toohello same password</span></span>
    ```bash
    sudo passwd hacluster
    
    ```

1. <span data-ttu-id="cfc21-252">[A] настройте corosync toouse других транспорта и добавьте набору узлов.</span><span class="sxs-lookup"><span data-stu-id="cfc21-252">[A] Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="cfc21-253">Иначе кластер не будет работать.</span><span class="sxs-lookup"><span data-stu-id="cfc21-253">Cluster will not work otherwise.</span></span>
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

    <span data-ttu-id="cfc21-254">Добавьте следующие полужирным содержимого toohello файл hello.</span><span class="sxs-lookup"><span data-stu-id="cfc21-254">Add hello following bold content toohello file.</span></span>
    
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

    <span data-ttu-id="cfc21-255">Затем перезапустите службу corosync hello</span><span class="sxs-lookup"><span data-stu-id="cfc21-255">Then restart hello corosync service</span></span>

    ```bash
    sudo service corosync restart
    
    ```

1. <span data-ttu-id="cfc21-256">[A] Установите пакеты для обеспечения высокого уровня доступности HANA.</span><span class="sxs-lookup"><span data-stu-id="cfc21-256">[A] Install HANA HA packages</span></span>  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a><span data-ttu-id="cfc21-257">Установка SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cfc21-257">Installing SAP HANA</span></span>

<span data-ttu-id="cfc21-258">Выполните главе 4 hello [SAP HANA SR производительности оптимизированных Scenario guide] [ suse-hana-ha-guide] tooinstall репликации системы SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="cfc21-258">Follow chapter 4 of hello [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] tooinstall SAP HANA System Replication.</span></span>

1. <span data-ttu-id="cfc21-259">[A] Запустите hdblcm из hello HANA DVD-диска</span><span class="sxs-lookup"><span data-stu-id="cfc21-259">[A] Run hdblcm from hello HANA DVD</span></span>
    * <span data-ttu-id="cfc21-260">Выберите установку (1).</span><span class="sxs-lookup"><span data-stu-id="cfc21-260">Choose installation -> 1</span></span>
    * <span data-ttu-id="cfc21-261">Выберите дополнительные компоненты для установки (1).</span><span class="sxs-lookup"><span data-stu-id="cfc21-261">Select additional components for installation -> 1</span></span>
    * <span data-ttu-id="cfc21-262">Введите путь установки [/hana/shared] и нажмите клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="cfc21-262">Enter Installation Path [/hana/shared]: -> ENTER</span></span>
    * <span data-ttu-id="cfc21-263">Введите имя локального узла [..] и нажмите клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="cfc21-263">Enter Local Host Name [..]: -> ENTER</span></span>
    * <span data-ttu-id="cfc21-264">Вы хотите, чтобы система toohello tooadd дополнительных узлов?</span><span class="sxs-lookup"><span data-stu-id="cfc21-264">Do you want tooadd additional hosts toohello system?</span></span> <span data-ttu-id="cfc21-265">(Вы хотите добавить дополнительные узлы в систему? (Да/нет)). Нажмите клавишу n и клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="cfc21-265">(y/n) [n]: -> ENTER</span></span>
    * <span data-ttu-id="cfc21-266">Введите идентификатор системы SAP HANA: <SID of HANA e.g. HDB></span><span class="sxs-lookup"><span data-stu-id="cfc21-266">Enter SAP HANA System ID: <SID of HANA e.g. HDB></span></span>
    * <span data-ttu-id="cfc21-267">Введите номер экземпляра [00].</span><span class="sxs-lookup"><span data-stu-id="cfc21-267">Enter Instance Number [00]:</span></span>   
  <span data-ttu-id="cfc21-268">Номер экземпляра HANA.</span><span class="sxs-lookup"><span data-stu-id="cfc21-268">HANA Instance number.</span></span> <span data-ttu-id="cfc21-269">Используйте 03 при использовании hello шаблона Azure или за приведенном выше примере hello</span><span class="sxs-lookup"><span data-stu-id="cfc21-269">Use 03 if you used hello Azure Template or followed hello example above</span></span>
    * <span data-ttu-id="cfc21-270">Выберите режим базы данных и введите индекс [1], затем нажмите клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="cfc21-270">Select Database Mode / Enter Index [1]: -> ENTER</span></span>
    * <span data-ttu-id="cfc21-271">Выберите использование системы и введите индекс [4].</span><span class="sxs-lookup"><span data-stu-id="cfc21-271">Select System Usage / Enter Index [4]:</span></span>  
  <span data-ttu-id="cfc21-272">Выберите систему hello использования</span><span class="sxs-lookup"><span data-stu-id="cfc21-272">Select hello system Usage</span></span>
    * <span data-ttu-id="cfc21-273">Введите расположение томов данных [/hana/data/HDB], затем нажмите клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="cfc21-273">Enter Location of Data Volumes [/hana/data/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="cfc21-274">Введите расположение томов журнала [/hana/log/HDB], затем нажмите клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="cfc21-274">Enter Location of Log Volumes [/hana/log/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="cfc21-275">"Restrict maximum memory allocation?"</span><span class="sxs-lookup"><span data-stu-id="cfc21-275">Restrict maximum memory allocation?</span></span> <span data-ttu-id="cfc21-276">(Перезапустить систему после перезагрузки компьютера?) Нажмите клавишу n и клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="cfc21-276">[n]: -> ENTER</span></span>
    * <span data-ttu-id="cfc21-277">Введите имя узла сертификат для узла «...» [...]: Введите "->"</span><span class="sxs-lookup"><span data-stu-id="cfc21-277">Enter Certificate Host Name For Host '...' [...]: -> ENTER</span></span>
    * <span data-ttu-id="cfc21-278">Введите пароль пользователя агента узла SAP (sapadm).</span><span class="sxs-lookup"><span data-stu-id="cfc21-278">Enter SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="cfc21-279">Подтвердите пароль пользователя агента узла SAP (sapadm).</span><span class="sxs-lookup"><span data-stu-id="cfc21-279">Confirm SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="cfc21-280">Введите пароль системного администратора (hdbadm).</span><span class="sxs-lookup"><span data-stu-id="cfc21-280">Enter System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="cfc21-281">Подтвердите пароль системного администратора (hdbadm).</span><span class="sxs-lookup"><span data-stu-id="cfc21-281">Confirm System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="cfc21-282">Введите домашний каталог системного администратора [/usr/sap/HDB/home], затем нажмите клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="cfc21-282">Enter System Administrator Home Directory [/usr/sap/HDB/home]: -> ENTER</span></span>
    * <span data-ttu-id="cfc21-283">Укажите оболочку для входа администратора системы [/bin/sh] и нажмите клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="cfc21-283">Enter System Administrator Login Shell [/bin/sh]: -> ENTER</span></span>
    * <span data-ttu-id="cfc21-284">Введите идентификатор пользователя администратора системы [1001] и нажмите клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="cfc21-284">Enter System Administrator User ID [1001]: -> ENTER</span></span>
    * <span data-ttu-id="cfc21-285">Введите идентификатор для группы пользователей (sapsys) [79], затем нажмите клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="cfc21-285">Enter ID of User Group (sapsys) [79]: -> ENTER</span></span>
    * <span data-ttu-id="cfc21-286">Введите пароль пользователя базы данных (SYSTEM).</span><span class="sxs-lookup"><span data-stu-id="cfc21-286">Enter Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="cfc21-287">Подтвердите пароль пользователя базы данных (SYSTEM).</span><span class="sxs-lookup"><span data-stu-id="cfc21-287">Confirm Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="cfc21-288">"Restart system after machine reboot?"</span><span class="sxs-lookup"><span data-stu-id="cfc21-288">Restart system after machine reboot?</span></span> <span data-ttu-id="cfc21-289">(Перезапустить систему после перезагрузки компьютера?) Нажмите клавишу n и клавишу "ВВОД".</span><span class="sxs-lookup"><span data-stu-id="cfc21-289">[n]: -> ENTER</span></span>
    * <span data-ttu-id="cfc21-290">Вы хотите, чтобы toocontinue?</span><span class="sxs-lookup"><span data-stu-id="cfc21-290">Do you want toocontinue?</span></span> <span data-ttu-id="cfc21-291">(Вы действительно хотите продолжить? (Да/нет)).</span><span class="sxs-lookup"><span data-stu-id="cfc21-291">(y/n):</span></span>  
  <span data-ttu-id="cfc21-292">Проверьте сводки hello и введите y toocontinue</span><span class="sxs-lookup"><span data-stu-id="cfc21-292">Validate hello summary and enter y toocontinue</span></span>
1. <span data-ttu-id="cfc21-293">[A] Обновите агент узла SAP.</span><span class="sxs-lookup"><span data-stu-id="cfc21-293">[A] Upgrade SAP Host Agent</span></span>  
  <span data-ttu-id="cfc21-294">Загрузить последний архив агента узла SAP hello hello [SAP Softwarecenter] [ sap-swcenter] и выполнения hello следующие команды tooupgrade hello агента.</span><span class="sxs-lookup"><span data-stu-id="cfc21-294">Download hello latest SAP Host Agent archive from hello [SAP Softwarecenter][sap-swcenter] and run hello following command tooupgrade hello agent.</span></span> <span data-ttu-id="cfc21-295">Замените hello путь toohello архив toopoint toohello загруженный файл.</span><span class="sxs-lookup"><span data-stu-id="cfc21-295">Replace hello path toohello archive toopoint toohello file you downloaded.</span></span>
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path tooSAP Host Agent SAR>
    ```

1. <span data-ttu-id="cfc21-296">[1] Создайте репликацию HANA (в качестве привилегированного пользователя).</span><span class="sxs-lookup"><span data-stu-id="cfc21-296">[1] Create HANA replication (as root)</span></span>  
    <span data-ttu-id="cfc21-297">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="cfc21-297">Run hello following command.</span></span> <span data-ttu-id="cfc21-298">Убедитесь, что tooreplace полужирным шрифтом строки (идентификатор HDB HANA системы и номера экземпляра 03) со значениями hello установки SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="cfc21-298">Make sure tooreplace bold strings (HANA System ID HDB and instance number 03) with hello values of your SAP HANA installation.</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. <span data-ttu-id="cfc21-299">[A] Создайте запись хранилища ключей (в качестве привилегированного пользователя).</span><span class="sxs-lookup"><span data-stu-id="cfc21-299">[A] Create keystore entry (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. <span data-ttu-id="cfc21-300">[1] Создайте резервную копию базы данных (в качестве привилегированного пользователя).</span><span class="sxs-lookup"><span data-stu-id="cfc21-300">[1] Backup database (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. <span data-ttu-id="cfc21-301">[1] коммутатора toohello sapsid пользователя (например hdbadm), а для создания первичного сайта hello.</span><span class="sxs-lookup"><span data-stu-id="cfc21-301">[1] Switch toohello sapsid user (for example hdbadm) and create hello primary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. <span data-ttu-id="cfc21-302">[2] коммутатора toohello sapsid пользователя (например hdbadm), а для создания вторичного сайта hello.</span><span class="sxs-lookup"><span data-stu-id="cfc21-302">[2] Switch toohello sapsid user (for example hdbadm) and create hello secondary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a><span data-ttu-id="cfc21-303">Настройка платформы кластера</span><span class="sxs-lookup"><span data-stu-id="cfc21-303">Configure Cluster Framework</span></span>

<span data-ttu-id="cfc21-304">Изменение параметров по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="cfc21-304">Change hello default settings</span></span>

<pre>
sudo vi crm-defaults.txt
# enter hello following toocrm-defaults.txt
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

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="cfc21-305">Теперь мы можем загрузить hello файл toohello кластера</span><span class="sxs-lookup"><span data-stu-id="cfc21-305">now we load hello file toohello cluster</span></span>
<span data-ttu-id="cfc21-306">sudo crm configure load update crm-defaults.txt</span><span class="sxs-lookup"><span data-stu-id="cfc21-306">sudo crm configure load update crm-defaults.txt</span></span>
</pre>

### <a name="create-stonith-device"></a><span data-ttu-id="cfc21-307">Создание устройства STONITH</span><span class="sxs-lookup"><span data-stu-id="cfc21-307">Create STONITH device</span></span>

<span data-ttu-id="cfc21-308">Hello STONITH устройство использует tooauthorize участника-службы для Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cfc21-308">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="cfc21-309">Выполните эти шаги toocreate участника службы.</span><span class="sxs-lookup"><span data-stu-id="cfc21-309">Please follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="cfc21-310">Go слишком<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="cfc21-310">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="cfc21-311">Привет открыть колонку Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cfc21-311">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="cfc21-312">Go tooProperties и запишите hello идентификатор каталога. Это hello **ИД клиента**.</span><span class="sxs-lookup"><span data-stu-id="cfc21-312">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="cfc21-313">Щелкните "Регистрация приложений".</span><span class="sxs-lookup"><span data-stu-id="cfc21-313">Click App registrations</span></span>
1. <span data-ttu-id="cfc21-314">Нажмите "Добавить"</span><span class="sxs-lookup"><span data-stu-id="cfc21-314">Click Add</span></span>
1. <span data-ttu-id="cfc21-315">Введите имя, выберите тип приложения "Веб-приложения или API", введите URL-адрес входа (например. http://localhost) и нажмите кнопку "Создать".</span><span class="sxs-lookup"><span data-stu-id="cfc21-315">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="cfc21-316">Hello URL-адрес входа не используется и может быть любой допустимый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="cfc21-316">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="cfc21-317">Здравствуйте, выберите новое приложение и щелкните на вкладке Параметры hello ключи</span><span class="sxs-lookup"><span data-stu-id="cfc21-317">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="cfc21-318">Введите описание нового ключа, выберите "Срок действия не ограничен" и нажмите кнопку "Сохранить".</span><span class="sxs-lookup"><span data-stu-id="cfc21-318">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="cfc21-319">Запишите значение hello.</span><span class="sxs-lookup"><span data-stu-id="cfc21-319">Write down hello Value.</span></span> <span data-ttu-id="cfc21-320">Он используется как hello **пароль** для hello участника-службы</span><span class="sxs-lookup"><span data-stu-id="cfc21-320">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="cfc21-321">Запишите hello идентификатор приложения. Он используется как hello username (**идентификатора входа** в hello действия) для hello участника-службы</span><span class="sxs-lookup"><span data-stu-id="cfc21-321">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="cfc21-322">Hello участника-службы не имеет разрешения tooaccess ресурсам Azure по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cfc21-322">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="cfc21-323">Необходимые субъекта-службы разрешений toogive hello toostart и остановить (освободить) всех виртуальных машин кластера hello.</span><span class="sxs-lookup"><span data-stu-id="cfc21-323">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="cfc21-324">Go toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="cfc21-324">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="cfc21-325">Здравствуйте, откройте колонку все ресурсы</span><span class="sxs-lookup"><span data-stu-id="cfc21-325">Open hello All resources blade</span></span>
1. <span data-ttu-id="cfc21-326">Выберите виртуальную машину, hello</span><span class="sxs-lookup"><span data-stu-id="cfc21-326">Select hello virtual machine</span></span>
1. <span data-ttu-id="cfc21-327">Выберите "Управление доступом (IAM)".</span><span class="sxs-lookup"><span data-stu-id="cfc21-327">Click Access control (IAM)</span></span>
1. <span data-ttu-id="cfc21-328">Нажмите "Добавить"</span><span class="sxs-lookup"><span data-stu-id="cfc21-328">Click Add</span></span>
1. <span data-ttu-id="cfc21-329">Выберите роль hello владельца</span><span class="sxs-lookup"><span data-stu-id="cfc21-329">Select hello role Owner</span></span>
1. <span data-ttu-id="cfc21-330">Введите имя приложения hello, созданной выше hello</span><span class="sxs-lookup"><span data-stu-id="cfc21-330">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="cfc21-331">Нажмите кнопку "ОК"</span><span class="sxs-lookup"><span data-stu-id="cfc21-331">Click OK</span></span>

<span data-ttu-id="cfc21-332">После редактирования hello разрешения для виртуальных машин hello hello STONITH устройства можно настроить в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="cfc21-332">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre>
sudo vi crm-fencing.txt
# enter hello following toocrm-fencing.txt
# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="cfc21-333">Теперь мы можем загрузить hello файл toohello кластера</span><span class="sxs-lookup"><span data-stu-id="cfc21-333">now we load hello file toohello cluster</span></span>
<span data-ttu-id="cfc21-334">sudo crm configure load update crm-fencing.txt</span><span class="sxs-lookup"><span data-stu-id="cfc21-334">sudo crm configure load update crm-fencing.txt</span></span>
</pre>

### <a name="create-sap-hana-resources"></a><span data-ttu-id="cfc21-335">Создание ресурсов SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cfc21-335">Create SAP HANA resources</span></span>

<pre>
sudo vi crm-saphanatop.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number and HANA system id
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

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="cfc21-336">Теперь мы можем загрузить hello файл toohello кластера</span><span class="sxs-lookup"><span data-stu-id="cfc21-336">now we load hello file toohello cluster</span></span>
<span data-ttu-id="cfc21-337">sudo crm configure load update crm-saphanatop.txt</span><span class="sxs-lookup"><span data-stu-id="cfc21-337">sudo crm configure load update crm-saphanatop.txt</span></span>
</pre>

<pre>
sudo vi crm-saphana.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
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

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="cfc21-338">Теперь мы можем загрузить hello файл toohello кластера</span><span class="sxs-lookup"><span data-stu-id="cfc21-338">now we load hello file toohello cluster</span></span>
<span data-ttu-id="cfc21-339">sudo crm configure load update crm-saphana.txt</span><span class="sxs-lookup"><span data-stu-id="cfc21-339">sudo crm configure load update crm-saphana.txt</span></span>
</pre>

### <a name="test-cluster-setup"></a><span data-ttu-id="cfc21-340">Проверка установки кластера</span><span class="sxs-lookup"><span data-stu-id="cfc21-340">Test cluster setup</span></span>
<span data-ttu-id="cfc21-341">Hello следующие главы описывают, как можно проверить настройки программы установки.</span><span class="sxs-lookup"><span data-stu-id="cfc21-341">hello following chapter describe how you can test your setup.</span></span> <span data-ttu-id="cfc21-342">Каждый тест предполагается, что являются корнем и SAP HANA образец hello выполняется на виртуальной машине saphanavm1 hello.</span><span class="sxs-lookup"><span data-stu-id="cfc21-342">Every test assumes that you are root and hello SAP HANA master is running on hello virtual machine saphanavm1.</span></span>

#### <a name="fencing-test"></a><span data-ttu-id="cfc21-343">Тестирование ограждения</span><span class="sxs-lookup"><span data-stu-id="cfc21-343">Fencing Test</span></span>

<span data-ttu-id="cfc21-344">Можно проверить hello установки агента разграничения hello, отключив hello сетевого интерфейса на saphanavm1 узла.</span><span class="sxs-lookup"><span data-stu-id="cfc21-344">You can test hello setup of hello fencing agent by disabling hello network interface on node saphanavm1.</span></span>

<pre><code>
sudo ifdown eth0
</code></pre>

<span data-ttu-id="cfc21-345">Теперь Hello виртуальной машины следует получить перезапуске или остановке в зависимости от конфигурации кластера.</span><span class="sxs-lookup"><span data-stu-id="cfc21-345">hello virtual machine should now get restarted or stopped depending on your cluster configuration.</span></span>
<span data-ttu-id="cfc21-346">Если задать toooff stonith действие hello hello виртуальной машины будет остановлена и ресурсы hello, перенесенных toohello выполняющаяся виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="cfc21-346">If you set hello stonith-action toooff, hello virtual machine will be stopped and hello resources are migrated toohello running virtual machine.</span></span>

<span data-ttu-id="cfc21-347">После повторного запуска виртуальной машины hello hello SAP HANA ресурсов не удастся toostart дополнительный — при выборе AUTOMATED_REGISTER = «false».</span><span class="sxs-lookup"><span data-stu-id="cfc21-347">Once you start hello virtual machine again, hello SAP HANA resource will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="cfc21-348">В этом случае необходимые tooconfigure hello HANA экземпляр в качестве получателя, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="cfc21-348">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a><span data-ttu-id="cfc21-349">Тестирование отработки отказа вручную</span><span class="sxs-lookup"><span data-stu-id="cfc21-349">Testing a manual failover</span></span>

<span data-ttu-id="cfc21-350">Отработка отказа вручную можно проверить, остановка службы pacemaker hello на saphanavm1 узла.</span><span class="sxs-lookup"><span data-stu-id="cfc21-350">You can test a manual failover by stopping hello pacemaker service on node saphanavm1.</span></span>
<pre><code>
service pacemaker stop
</code></pre>

<span data-ttu-id="cfc21-351">После отработки отказа hello можно снова запустить службу hello.</span><span class="sxs-lookup"><span data-stu-id="cfc21-351">After hello failover, you can start hello service again.</span></span> <span data-ttu-id="cfc21-352">Hello ресурсов SAP HANA на saphanavm1 не удастся toostart дополнительный — при выборе AUTOMATED_REGISTER = «false».</span><span class="sxs-lookup"><span data-stu-id="cfc21-352">hello SAP HANA resource on saphanavm1 will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="cfc21-353">В этом случае необходимые tooconfigure hello HANA экземпляр в качестве получателя, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="cfc21-353">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a><span data-ttu-id="cfc21-354">Тестирование переноса</span><span class="sxs-lookup"><span data-stu-id="cfc21-354">Testing a migration</span></span>

<span data-ttu-id="cfc21-355">Можно перенести главного узла hello SAP HANA, выполнив следующую команду hello</span><span class="sxs-lookup"><span data-stu-id="cfc21-355">You can migrate hello SAP HANA master node by executing hello following command</span></span>
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="cfc21-356">Это необходимо перенести главного узла SAP HANA hello и hello группу, содержащую hello виртуальных IP адресов toosaphanavm2.</span><span class="sxs-lookup"><span data-stu-id="cfc21-356">This should migrate hello SAP HANA master node and hello group that contains hello virtual IP address toosaphanavm2.</span></span>
<span data-ttu-id="cfc21-357">Hello ресурсов SAP HANA на saphanavm1 не удастся toostart дополнительный — при выборе AUTOMATED_REGISTER = «false».</span><span class="sxs-lookup"><span data-stu-id="cfc21-357">hello SAP HANA resource on saphanavm1 will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="cfc21-358">В этом случае необходимые tooconfigure hello HANA экземпляр в качестве получателя, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="cfc21-358">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

<span data-ttu-id="cfc21-359">При миграции Hello создается расположение ограничений, которые должны toobe снова удалены.</span><span class="sxs-lookup"><span data-stu-id="cfc21-359">hello migration creates location contraints that need toobe deleted again.</span></span>

<pre><code>
crm configure edited

# delete location contraints that are named like hello following contraint. You should have two contraints, one for hello SAP HANA resource and one for hello IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="cfc21-360">Необходимо также toocleanup состояние hello hello дополнительного узла ресурса</span><span class="sxs-lookup"><span data-stu-id="cfc21-360">You also need toocleanup hello state of hello secondary node resource</span></span>

<pre><code>
# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a><span data-ttu-id="cfc21-361">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cfc21-361">Next steps</span></span>
* <span data-ttu-id="cfc21-362">[SAP NetWeaver на виртуальных машинах Windows. Руководство по планированию и внедрению][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="cfc21-362">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="cfc21-363">[Развертывание программного обеспечения SAP на виртуальных машинах Azure][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="cfc21-363">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="cfc21-364">[SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию СУБД][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="cfc21-364">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="cfc21-365">tooestablish высокого уровня доступности и план аварийного восстановления из SAP HANA в Azure (большие экземпляры). в статье toolearn [SAP HANA (крупных экземпляров) высокой доступности и аварийного восстановления в Azure](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="cfc21-365">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span> 
