---
title: "aaaClusterize MySQL с балансировкой нагрузки наборами | Документы Microsoft"
description: "Настройка балансировки нагрузки, высокий уровень доступности, создать кластер Linux MySQL с hello классической модели развертывания в Azure"
services: virtual-machines-linux
documentationcenter: 
author: bureado
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6c413a16-e9b5-4ffe-a8a3-ae67046bbdf3
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/14/2015
ms.author: jparrel
ms.openlocfilehash: 1829fd877c4b0ed177b23a8e3404dbb3db746561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-load-balanced-sets-tooclusterize-mysql-on-linux"></a><span data-ttu-id="11672-103">Использование наборов с балансировкой нагрузки tooclusterize MySQL в Linux</span><span class="sxs-lookup"><span data-stu-id="11672-103">Use load-balanced sets tooclusterize MySQL on Linux</span></span>
> [!IMPORTANT]
> <span data-ttu-id="11672-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager](../../../resource-manager-deployment-model.md) и классическая модель.</span><span class="sxs-lookup"><span data-stu-id="11672-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="11672-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="11672-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="11672-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="11672-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="11672-107">Объект [шаблона диспетчера ресурсов](https://azure.microsoft.com/documentation/templates/mysql-replication/) доступен, если вам требуется toodeploy кластер MySQL.</span><span class="sxs-lookup"><span data-stu-id="11672-107">A [Resource Manager template](https://azure.microsoft.com/documentation/templates/mysql-replication/) is available if you need toodeploy a MySQL cluster.</span></span>

<span data-ttu-id="11672-108">В этой статье исследуются и иллюстрируется hello различные подходы доступных toodeploy высокой доступности на базе Linux службы в Microsoft Azure, изучение высокого уровня доступности сервера MySQL как учебник.</span><span class="sxs-lookup"><span data-stu-id="11672-108">This article explores and illustrates hello different approaches available toodeploy highly available Linux-based services on Microsoft Azure, exploring MySQL Server high availability as a primer.</span></span> <span data-ttu-id="11672-109">Видеоролик, демонстрирующий этот подход, см. на [канале 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span><span class="sxs-lookup"><span data-stu-id="11672-109">A video illustrating this approach is available on [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span></span>

<span data-ttu-id="11672-110">Мы рассмотрим не использующее общие ресурсы высокодоступное решение MySQL с двумя узлами и одним владельцем на основе DRBD, Corosync и Pacemaker.</span><span class="sxs-lookup"><span data-stu-id="11672-110">We will outline a shared-nothing, two-node, single-master MySQL high availability solution based on DRBD, Corosync, and Pacemaker.</span></span> <span data-ttu-id="11672-111">Одновременно MySQL работает только в одном узле.</span><span class="sxs-lookup"><span data-stu-id="11672-111">Only one node runs MySQL at a time.</span></span> <span data-ttu-id="11672-112">Чтение и запись из hello ресурсов DRBD ограниченного tooonly узлом является один одновременно.</span><span class="sxs-lookup"><span data-stu-id="11672-112">Reading and writing from hello DRBD resource is also limited tooonly one node at a time.</span></span>

<span data-ttu-id="11672-113">Нет необходимости для решения виртуальных IP-адресов, как LVS, так как вы воспользуетесь балансировкой нагрузки наборов в Microsoft Azure tooprovide циклического функциональные возможности и конечной точки обнаружения, удаления, мягкое восстановление hello виртуальных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="11672-113">There's no need for a VIP solution like LVS, because you'll use load-balanced sets in Microsoft Azure tooprovide round-robin functionality and endpoint detection, removal, and graceful recovery of hello VIP.</span></span> <span data-ttu-id="11672-114">Hello виртуальных IP-адресов является глобально маршрутизируемым IPv4-адрес, назначенный при создании hello облачной службы Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="11672-114">hello VIP is a globally routable IPv4 address assigned by Microsoft Azure when you first create hello cloud service.</span></span>

<span data-ttu-id="11672-115">Существуют и другие доступные архитектуры для MySQL, в том числе NBD Cluster, Percona и Galera, а также несколько решений ПО промежуточного слоя, включая по крайней мере одно, доступное в качестве виртуальной машины на сайте [VM Depot](http://vmdepot.msopentech.com).</span><span class="sxs-lookup"><span data-stu-id="11672-115">There are other possible architectures for MySQL, including NBD Cluster, Percona, Galera, and several middleware solutions, including at least one available as a VM on [VM Depot](http://vmdepot.msopentech.com).</span></span> <span data-ttu-id="11672-116">При условии, что эти решения можно реплицировать на одноадресной и многоадресной или широковещательной рассылки и не используют общее хранилище или несколько сетевых интерфейсов, hello сценариев должно быть легко toodeploy в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="11672-116">As long as these solutions can replicate on unicast vs. multicast or broadcast and don't rely on shared storage or multiple network interfaces, hello scenarios should be easy toodeploy on Microsoft Azure.</span></span>

<span data-ttu-id="11672-117">Эти кластеризации архитектуры можно расширить tooother продуктах, например PostgreSQL и OpenLDAP таким же образом.</span><span class="sxs-lookup"><span data-stu-id="11672-117">These clustering architectures can be extended tooother products like PostgreSQL and OpenLDAP in a similar fashion.</span></span> <span data-ttu-id="11672-118">Например, данная процедура балансировки нагрузки без использования общих ресурсов была успешно протестирована с OpenLDAP с несколькими хозяевами, и это можно увидеть в нашем блоге "Канал 9".</span><span class="sxs-lookup"><span data-stu-id="11672-118">For example, this load-balancing procedure with shared nothing was successfully tested with multi-master OpenLDAP, and you can watch it on our Channel 9 blog.</span></span>

## <a name="get-ready"></a><span data-ttu-id="11672-119">Подготовка</span><span class="sxs-lookup"><span data-stu-id="11672-119">Get ready</span></span>
<span data-ttu-id="11672-120">Требуются следующие hello ресурсов и возможности:</span><span class="sxs-lookup"><span data-stu-id="11672-120">You need hello following resources and abilities:</span></span>

  - <span data-ttu-id="11672-121">Microsoft Azure счета с действительной подпиской, будет toocreate по крайней мере две виртуальные машины (в этом примере использовался XS)</span><span class="sxs-lookup"><span data-stu-id="11672-121">A Microsoft Azure account with a valid subscription, able toocreate at least two VMs (XS was used in this example)</span></span>
  - <span data-ttu-id="11672-122">сеть и подсеть;</span><span class="sxs-lookup"><span data-stu-id="11672-122">A network and a subnet</span></span>
  - <span data-ttu-id="11672-123">территориальная группа;</span><span class="sxs-lookup"><span data-stu-id="11672-123">An affinity group</span></span>
  - <span data-ttu-id="11672-124">группа доступности;</span><span class="sxs-lookup"><span data-stu-id="11672-124">An availability set</span></span>
  - <span data-ttu-id="11672-125">Здравствуйте возможность toocreate виртуальные жесткие диски в hello же регионе, что облачная служба hello и присоединить их toohello виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="11672-125">hello ability toocreate VHDs in hello same region as hello cloud service and attach them toohello Linux VMs</span></span>

### <a name="tested-environment"></a><span data-ttu-id="11672-126">Тестовая среда</span><span class="sxs-lookup"><span data-stu-id="11672-126">Tested environment</span></span>
* <span data-ttu-id="11672-127">Ubuntu 13.10</span><span class="sxs-lookup"><span data-stu-id="11672-127">Ubuntu 13.10</span></span>
  * <span data-ttu-id="11672-128">DRBD</span><span class="sxs-lookup"><span data-stu-id="11672-128">DRBD</span></span>
  * <span data-ttu-id="11672-129">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="11672-129">MySQL Server</span></span>
  * <span data-ttu-id="11672-130">Corosync и Pacemaker</span><span class="sxs-lookup"><span data-stu-id="11672-130">Corosync and Pacemaker</span></span>

### <a name="affinity-group"></a><span data-ttu-id="11672-131">Территориальная группа</span><span class="sxs-lookup"><span data-stu-id="11672-131">Affinity group</span></span>
<span data-ttu-id="11672-132">Создание территориальной группы для решения hello при входе в toohello классический портал Azure, при выборе **параметры**и создать группу сходства.</span><span class="sxs-lookup"><span data-stu-id="11672-132">Create an affinity group for hello solution by signing in toohello Azure classic portal, selecting **Settings**, and creating an affinity group.</span></span> <span data-ttu-id="11672-133">Выделенные ресурсы, созданные в более поздней версии будут назначаться toothis территориальную группу.</span><span class="sxs-lookup"><span data-stu-id="11672-133">Allocated resources created later will be assigned toothis affinity group.</span></span>

### <a name="networks"></a><span data-ttu-id="11672-134">Сети</span><span class="sxs-lookup"><span data-stu-id="11672-134">Networks</span></span>
<span data-ttu-id="11672-135">Создать новую сеть и подсеть создается внутри сети hello.</span><span class="sxs-lookup"><span data-stu-id="11672-135">A new network is created, and a subnet is created inside hello network.</span></span> <span data-ttu-id="11672-136">В этом примере используется сеть 10.10.10.0/24 только с одной подсетью /24.</span><span class="sxs-lookup"><span data-stu-id="11672-136">This example uses a 10.10.10.0/24 network with only one /24 subnet inside.</span></span>

### <a name="virtual-machines"></a><span data-ttu-id="11672-137">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="11672-137">Virtual machines</span></span>
<span data-ttu-id="11672-138">Hello первая виртуальная машина 13.10 Ubuntu создается с помощью образа коллекции Ubuntu Endorsed и называется `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="11672-138">hello first Ubuntu 13.10 VM is created by using an Endorsed Ubuntu Gallery image and is called `hadb01`.</span></span> <span data-ttu-id="11672-139">В процесс hello, называемый hadb создается новой облачной службы.</span><span class="sxs-lookup"><span data-stu-id="11672-139">A new cloud service is created in hello process, called hadb.</span></span> <span data-ttu-id="11672-140">Это имя показан общий доступ, hello характера балансировки нагрузки, которые hello службы будет отображаться, если добавляются дополнительные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="11672-140">This name illustrates hello shared, load-balanced nature that hello service will have when more resources are added.</span></span> <span data-ttu-id="11672-141">Здравствуйте, создание `hadb01` имеет процедура и заполняется с помощью портала hello.</span><span class="sxs-lookup"><span data-stu-id="11672-141">hello creation of `hadb01` is uneventful and completed by using hello portal.</span></span> <span data-ttu-id="11672-142">Конечной точки для SSH создается автоматически, и выбран hello новой сети.</span><span class="sxs-lookup"><span data-stu-id="11672-142">An endpoint for SSH is automatically created, and hello new network is selected.</span></span> <span data-ttu-id="11672-143">Теперь можно создать набор доступности для виртуальных машин hello.</span><span class="sxs-lookup"><span data-stu-id="11672-143">Now you can create an availability set for hello VMs.</span></span>

<span data-ttu-id="11672-144">После hello первая виртуальная машина создается (с технической точки зрения при создании hello облачной службы), создайте второй ВМ hello `hadb02`.</span><span class="sxs-lookup"><span data-stu-id="11672-144">After hello first VM is created (technically, when hello cloud service is created), create hello second VM, `hadb02`.</span></span> <span data-ttu-id="11672-145">Для hello второй виртуальной Машины, используйте Ubuntu 13.10 ВМ из hello коллекции с помощью портала hello, но использовать существующую облачную службу, `hadb.cloudapp.net`, вместо создания нового.</span><span class="sxs-lookup"><span data-stu-id="11672-145">For hello second VM, use Ubuntu 13.10 VM from hello Gallery by using hello portal, but use an existing cloud service, `hadb.cloudapp.net`, instead of creating a new one.</span></span> <span data-ttu-id="11672-146">Hello сети и доступность набор должен быть выбран автоматически.</span><span class="sxs-lookup"><span data-stu-id="11672-146">hello network and availability set should be automatically selected.</span></span> <span data-ttu-id="11672-147">Также будет создана конечная точка SSH.</span><span class="sxs-lookup"><span data-stu-id="11672-147">An SSH endpoint will be created, too.</span></span>

<span data-ttu-id="11672-148">После создания обе виртуальные машины, возьмите на заметку hello портом SSH для `hadb01` (TCP-ПОРТ 22) и `hadb02` (автоматически назначаемый в Azure).</span><span class="sxs-lookup"><span data-stu-id="11672-148">After both VMs have been created, take note of hello SSH port for `hadb01` (TCP 22) and `hadb02` (automatically assigned by Azure).</span></span>

### <a name="attached-storage"></a><span data-ttu-id="11672-149">Подключаемое хранилище</span><span class="sxs-lookup"><span data-stu-id="11672-149">Attached storage</span></span>
<span data-ttu-id="11672-150">Подключить новый диск-tooboth виртуальные машины и создавать диски размером 5 ГБ в процессе hello.</span><span class="sxs-lookup"><span data-stu-id="11672-150">Attach a new disk tooboth VMs and create 5-GB disks in hello process.</span></span> <span data-ttu-id="11672-151">диски Hello размещаются в контейнере VHD hello используется для дисков основной операционной системы.</span><span class="sxs-lookup"><span data-stu-id="11672-151">hello disks are hosted in hello VHD container in use for your main operating system disks.</span></span> <span data-ttu-id="11672-152">После создаются и присоединенные диски, происходит без необходимости toorestart Linux, поскольку hello новое устройство будет отображено hello ядра.</span><span class="sxs-lookup"><span data-stu-id="11672-152">After disks are created and attached, there is no need toorestart Linux because hello kernel will see hello new device.</span></span> <span data-ttu-id="11672-153">Обычно это `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="11672-153">This device is usually `/dev/sdc`.</span></span> <span data-ttu-id="11672-154">Проверьте `dmesg` для вывода hello.</span><span class="sxs-lookup"><span data-stu-id="11672-154">Check `dmesg` for hello output.</span></span>

<span data-ttu-id="11672-155">На каждой виртуальной Машины, создать раздел с помощью `cfdisk` (основной, раздел Linux) и записи hello новой секции таблицы.</span><span class="sxs-lookup"><span data-stu-id="11672-155">On each VM, create a partition by using `cfdisk` (primary, Linux partition) and write hello new partition table.</span></span> <span data-ttu-id="11672-156">Файловую систему в этом разделе создавать не нужно.</span><span class="sxs-lookup"><span data-stu-id="11672-156">Do not create a file system on this partition.</span></span>

## <a name="set-up-hello-cluster"></a><span data-ttu-id="11672-157">Настройка кластера hello</span><span class="sxs-lookup"><span data-stu-id="11672-157">Set up hello cluster</span></span>
<span data-ttu-id="11672-158">Используйте APT tooinstall Corosync, Pacemaker и DRBD на обоих Ubuntu виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="11672-158">Use APT tooinstall Corosync, Pacemaker, and DRBD on both Ubuntu VMs.</span></span> <span data-ttu-id="11672-159">toodo с `apt-get`, запустите hello следующий код:</span><span class="sxs-lookup"><span data-stu-id="11672-159">toodo so with `apt-get`, run hello following code:</span></span>

    sudo apt-get install corosync pacemaker drbd8-utils.

<span data-ttu-id="11672-160">Откажитесь от установки MySQL в это время.</span><span class="sxs-lookup"><span data-stu-id="11672-160">Do not install MySQL at this time.</span></span> <span data-ttu-id="11672-161">Debian и Ubuntu сценарии установки будет инициализировать каталог данных MySQL на `/var/lib/mysql`, но поскольку hello каталогов будет заменен DRBD файловой системы, вам потребуется позже tooinstall MySQL.</span><span class="sxs-lookup"><span data-stu-id="11672-161">Debian and Ubuntu installation scripts will initialize a MySQL data directory on `/var/lib/mysql`, but because hello directory will be superseded by a DRBD file system, you need tooinstall MySQL later.</span></span>

<span data-ttu-id="11672-162">Проверка (с помощью `/sbin/ifconfig`), обе виртуальные машины используют адресов в подсети 10.10.10.0/24 hello и что они могут выполнить команду ping друг с другом по имени.</span><span class="sxs-lookup"><span data-stu-id="11672-162">Verify (by using `/sbin/ifconfig`) that both VMs are using addresses in hello 10.10.10.0/24 subnet and that they can ping each other by name.</span></span> <span data-ttu-id="11672-163">Можно также использовать `ssh-keygen` и `ssh-copy-id` toomake убедиться, что обе виртуальные машины могут взаимодействовать по протоколу SSH не требуется пароль.</span><span class="sxs-lookup"><span data-stu-id="11672-163">You can also use `ssh-keygen` and `ssh-copy-id` toomake sure both VMs can communicate via SSH without requiring a password.</span></span>

### <a name="set-up-drbd"></a><span data-ttu-id="11672-164">Настройка DRBD</span><span class="sxs-lookup"><span data-stu-id="11672-164">Set up DRBD</span></span>
<span data-ttu-id="11672-165">Создать DRBD ресурс, который использует базовый hello `/dev/sdc1` секции tooproduce `/dev/drbd1` ресурс, который отформатирован с помощью ext3 и использовать в первичных и вторичных узлах.</span><span class="sxs-lookup"><span data-stu-id="11672-165">Create a DRBD resource that uses hello underlying `/dev/sdc1` partition tooproduce a `/dev/drbd1` resource that can be formatted by using ext3 and used in both primary and secondary nodes.</span></span>

1. <span data-ttu-id="11672-166">Откройте `/etc/drbd.d/r0.res` и копирования hello после определения ресурса на обеих виртуальных машин:</span><span class="sxs-lookup"><span data-stu-id="11672-166">Open `/etc/drbd.d/r0.res` and copy hello following resource definition on both VMs:</span></span>

        resource r0 {
          on `hadb01` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.4:7789;
            meta-disk internal;
          }
          on `hadb02` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.5:7789;
            meta-disk internal;
          }
        }

2. <span data-ttu-id="11672-167">Инициализация hello ресурсов с помощью `drbdadm` на обеих виртуальных машинах:</span><span class="sxs-lookup"><span data-stu-id="11672-167">Initialize hello resource by using `drbdadm` on both VMs:</span></span>

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. <span data-ttu-id="11672-168">На основной виртуальной Машины hello (`hadb01`), принудительно владения hello DRBD ресурс (первичный):</span><span class="sxs-lookup"><span data-stu-id="11672-168">On hello primary VM (`hadb01`), force ownership (primary) of hello DRBD resource:</span></span>

        sudo drbdadm primary --force r0

<span data-ttu-id="11672-169">Если изучить содержимое hello/proc/drbd (`sudo cat /proc/drbd`) на обеих виртуальных машинах, вы должны увидеть `Primary/Secondary` на `hadb01` и `Secondary/Primary` на `hadb02`, согласованные с hello решения на этом этапе.</span><span class="sxs-lookup"><span data-stu-id="11672-169">If you examine hello contents of /proc/drbd (`sudo cat /proc/drbd`) on both VMs, you should see `Primary/Secondary` on `hadb01` and `Secondary/Primary` on `hadb02`, consistent with hello solution at this point.</span></span> <span data-ttu-id="11672-170">диск размером 5 ГБ Hello синхронизируются по сети 10.10.10.0/24 hello в toocustomers не взимается.</span><span class="sxs-lookup"><span data-stu-id="11672-170">hello 5-GB disk is synchronized over hello 10.10.10.0/24 network at no charge toocustomers.</span></span>

<span data-ttu-id="11672-171">По завершении синхронизации hello диск можно создать hello файловой системы на `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="11672-171">After hello disk is synchronized, you can create hello file system on `hadb01`.</span></span> <span data-ttu-id="11672-172">В целях тестирования мы использовали ext2, но после кода hello создаст ext3 файловой системы:</span><span class="sxs-lookup"><span data-stu-id="11672-172">For testing purposes, we used ext2, but hello following code will create an ext3 file system:</span></span>

    mkfs.ext3 /dev/drbd1

### <a name="mount-hello-drbd-resource"></a><span data-ttu-id="11672-173">Подключить ресурс DRBD hello</span><span class="sxs-lookup"><span data-stu-id="11672-173">Mount hello DRBD resource</span></span>
<span data-ttu-id="11672-174">Вы теперь готовы toomount hello DRBD ресурсов на `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="11672-174">You're now ready toomount hello DRBD resources on `hadb01`.</span></span> <span data-ttu-id="11672-175">В Debian и производных дистрибутивах в качестве каталога данных MySQL используется `/var/lib/mysql` .</span><span class="sxs-lookup"><span data-stu-id="11672-175">Debian and derivatives use `/var/lib/mysql` as MySQL's data directory.</span></span> <span data-ttu-id="11672-176">Поскольку вы не установили MySQL, создайте каталог hello и подключения hello DRBD ресурсов.</span><span class="sxs-lookup"><span data-stu-id="11672-176">Because you haven't installed MySQL, create hello directory and mount hello DRBD resource.</span></span> <span data-ttu-id="11672-177">tooperform этот параметр запуска hello, следующий код `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="11672-177">tooperform this option, run hello following code on `hadb01`:</span></span>

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a><span data-ttu-id="11672-178">Настройка MySQL</span><span class="sxs-lookup"><span data-stu-id="11672-178">Set up MySQL</span></span>
<span data-ttu-id="11672-179">Теперь вы готовы tooinstall MySQL на `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="11672-179">Now you're ready tooinstall MySQL on `hadb01`:</span></span>

    sudo apt-get install mysql-server

<span data-ttu-id="11672-180">Для `hadb02`существует два варианта.</span><span class="sxs-lookup"><span data-stu-id="11672-180">For `hadb02`, you have two options.</span></span> <span data-ttu-id="11672-181">Можно установить mysql server, чтобы создать /var/lib/mysql, заполнить его в новый каталог данных и затем удалить содержимое hello.</span><span class="sxs-lookup"><span data-stu-id="11672-181">You can install mysql-server, which will create /var/lib/mysql, fill it with a new data directory, and then remove hello contents.</span></span> <span data-ttu-id="11672-182">tooperform этот параметр запуска hello, следующий код `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="11672-182">tooperform this option, run hello following code on `hadb02`:</span></span>

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

<span data-ttu-id="11672-183">второй вариант Hello — toofailover слишком`hadb02` , а затем установите mysql server существует.</span><span class="sxs-lookup"><span data-stu-id="11672-183">hello second option is toofailover too`hadb02` and then install mysql-server there.</span></span> <span data-ttu-id="11672-184">Сценарии установки заметить hello существующую установку и не трогайте его.</span><span class="sxs-lookup"><span data-stu-id="11672-184">Installation scripts will notice hello existing installation and won't touch it.</span></span>

<span data-ttu-id="11672-185">Выполнения hello следующий код на `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="11672-185">Run hello following code on `hadb01`:</span></span>

    sudo drbdadm secondary –force r0

<span data-ttu-id="11672-186">Выполнения hello следующий код на `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="11672-186">Run hello following code on `hadb02`:</span></span>

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

<span data-ttu-id="11672-187">Если вы не собираетесь toofailover DRBD, несмотря на то что возможно менее элегантное проще hello первый параметр.</span><span class="sxs-lookup"><span data-stu-id="11672-187">If you don't plan toofailover DRBD now, hello first option is easier although arguably less elegant.</span></span> <span data-ttu-id="11672-188">После выполнения этой установки можно начинать работу с базой данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="11672-188">After you set this up, you can start working on your MySQL database.</span></span> <span data-ttu-id="11672-189">Выполнения hello следующий код на `hadb02` (или любым из серверов hello активен, в соответствии с tooDRBD):</span><span class="sxs-lookup"><span data-stu-id="11672-189">Run hello following code on `hadb02` (or whichever one of hello servers is active, according tooDRBD):</span></span>

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* tooroot;

> [!WARNING]
> <span data-ttu-id="11672-190">Это последняя инструкция эффективно отключает проверку подлинности для пользователя root hello в этой таблице.</span><span class="sxs-lookup"><span data-stu-id="11672-190">This last statement effectively disables authentication for hello root user in this table.</span></span> <span data-ttu-id="11672-191">Она включена только для иллюстрации, и в инструкциях GRANT для рабочей среды это необходимо изменить.</span><span class="sxs-lookup"><span data-stu-id="11672-191">This should be replaced by your production-grade GRANT statements and is included only for illustrative purposes.</span></span>

<span data-ttu-id="11672-192">Если требуется toomake запросы из виртуальных машин с внешней hello (что hello цель данного руководства), необходимо также tooenable сети для MySQL.</span><span class="sxs-lookup"><span data-stu-id="11672-192">If you want toomake queries from outside hello VMs (which is hello purpose of this guide), you also need tooenable networking for MySQL.</span></span> <span data-ttu-id="11672-193">Откройте на обе виртуальные машины `/etc/mysql/my.cnf` и перейти слишком`bind-address`.</span><span class="sxs-lookup"><span data-stu-id="11672-193">On both VMs, open `/etc/mysql/my.cnf` and go too`bind-address`.</span></span> <span data-ttu-id="11672-194">Измените hello адрес 127.0.0.1 too0.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="11672-194">Change hello address from 127.0.0.1 too0.0.0.0.</span></span> <span data-ttu-id="11672-195">После сохранения файла hello выдавать `sudo service mysql restart` на вашей текущей первичной реплике.</span><span class="sxs-lookup"><span data-stu-id="11672-195">After saving hello file, issue a `sudo service mysql restart` on your current primary.</span></span>

### <a name="create-hello-mysql-load-balanced-set"></a><span data-ttu-id="11672-196">Создать набор балансировки нагрузки hello MySQL</span><span class="sxs-lookup"><span data-stu-id="11672-196">Create hello MySQL load-balanced set</span></span>
<span data-ttu-id="11672-197">Вернитесь toohello портала, go слишком`hadb01`и выберите **конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="11672-197">Go back toohello portal, go too`hadb01`, and choose **Endpoints**.</span></span> <span data-ttu-id="11672-198">toocreate конечной точки, выберите MySQL (порт TCP 3306) из раскрывающегося списка hello и выберите **набор с балансировкой нагрузки новый создать**.</span><span class="sxs-lookup"><span data-stu-id="11672-198">toocreate an endpoint, choose MySQL (TCP 3306) from hello drop-down list and select **Create new load balanced set**.</span></span> <span data-ttu-id="11672-199">Конечная точка с балансировкой нагрузки hello имя `lb-mysql`.</span><span class="sxs-lookup"><span data-stu-id="11672-199">Name hello load-balanced endpoint `lb-mysql`.</span></span> <span data-ttu-id="11672-200">Задать **время** too5 секунд минимальным.</span><span class="sxs-lookup"><span data-stu-id="11672-200">Set **Time** too5 seconds, minimum.</span></span>

<span data-ttu-id="11672-201">После создания конечной точки hello go слишком`hadb02`, выберите **конечные точки**и создайте конечную точку.</span><span class="sxs-lookup"><span data-stu-id="11672-201">After you create hello endpoint, go too`hadb02`, choose **Endpoints**, and create an endpoint.</span></span> <span data-ttu-id="11672-202">Выберите `lb-mysql`и выберите из раскрывающегося списка hello MySQL.</span><span class="sxs-lookup"><span data-stu-id="11672-202">Choose `lb-mysql`, and then select MySQL from hello drop-down list.</span></span> <span data-ttu-id="11672-203">На этом шаге можно также использовать hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="11672-203">You can also use hello Azure CLI for this step.</span></span>

<span data-ttu-id="11672-204">Теперь у вас есть все необходимое для ручной работы кластера hello.</span><span class="sxs-lookup"><span data-stu-id="11672-204">You now have everything you need for manual operation of hello cluster.</span></span>

### <a name="test-hello-load-balanced-set"></a><span data-ttu-id="11672-205">Проверить набор балансировки нагрузки hello</span><span class="sxs-lookup"><span data-stu-id="11672-205">Test hello load-balanced set</span></span>
<span data-ttu-id="11672-206">Тестирование можно выполнять с внешнего компьютера с помощью клиента MySQL или с использованием приложений, например приложения phpMyAdmin, работающего в качестве веб-сайта Azure.</span><span class="sxs-lookup"><span data-stu-id="11672-206">Tests can be performed from an outside machine by using any MySQL client, or by using certain applications, like phpMyAdmin running as an Azure website.</span></span> <span data-ttu-id="11672-207">В этом случае использовалась программа командной строки MySQL, запущенная на другом компьютере Linux.</span><span class="sxs-lookup"><span data-stu-id="11672-207">In this case, you used MySQL's command-line tool on another Linux box:</span></span>

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a><span data-ttu-id="11672-208">Переход на другой ресурс вручную</span><span class="sxs-lookup"><span data-stu-id="11672-208">Manually failing over</span></span>
<span data-ttu-id="11672-209">Вы можете смоделировать отработку отказа, завершив работу MySQL, переключившись на владельца DRBD и запустив MySQL снова.</span><span class="sxs-lookup"><span data-stu-id="11672-209">You can simulate failovers by shutting down MySQL, switching DRBD's primary, and starting MySQL again.</span></span>

<span data-ttu-id="11672-210">tooperform этой задачи, запустите следующий код на hadb01 hello:</span><span class="sxs-lookup"><span data-stu-id="11672-210">tooperform this task, run hello following code on hadb01:</span></span>

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

<span data-ttu-id="11672-211">Затем на hadb02:</span><span class="sxs-lookup"><span data-stu-id="11672-211">Then, on hadb02:</span></span>

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

<span data-ttu-id="11672-212">После выполнения перехода на другой ресурс вручную вы можете повторить удаленный запрос, и он должен работать без проблем.</span><span class="sxs-lookup"><span data-stu-id="11672-212">After you fail over manually, you can repeat your remote query and it should work perfectly.</span></span>

## <a name="set-up-corosync"></a><span data-ttu-id="11672-213">Установка Corosync</span><span class="sxs-lookup"><span data-stu-id="11672-213">Set up Corosync</span></span>
<span data-ttu-id="11672-214">Corosync — hello базового кластера инфраструктуры для Pacemaker toowork.</span><span class="sxs-lookup"><span data-stu-id="11672-214">Corosync is hello underlying cluster infrastructure required for Pacemaker toowork.</span></span> <span data-ttu-id="11672-215">Для пульса (и другие виды как Ultramonkey) Corosync является разбиение функциональные возможности CRM hello, оставив более похожими tooHeartbeat Pacemaker функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="11672-215">For Heartbeat (and other methodologies like Ultramonkey), Corosync is a split of hello CRM functionalities, while Pacemaker remains more similar tooHeartbeat in functionality.</span></span>

<span data-ttu-id="11672-216">основным ограничением Hello для Corosync в Azure является Corosync предпочитает многоадресную рассылку через вещания одноадресной рассылки связи, что сеть Microsoft Azure поддерживает только одноадресной рассылки.</span><span class="sxs-lookup"><span data-stu-id="11672-216">hello main constraint for Corosync on Azure is that Corosync prefers multicast over broadcast over unicast communications, but Microsoft Azure networking only supports unicast.</span></span>

<span data-ttu-id="11672-217">К счастью, в Corosync имеется рабочий одноадресный режим.</span><span class="sxs-lookup"><span data-stu-id="11672-217">Fortunately, Corosync has a working unicast mode.</span></span> <span data-ttu-id="11672-218">единственной реальной ограничение Hello —, так как все узлы не обмениваются данными друг с другом, необходимость toodefine hello узлы в файлах конфигурации, включая их IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="11672-218">hello only real constraint is that because all nodes are not communicating among themselves, you need toodefine hello nodes in your configuration files, including their IP addresses.</span></span> <span data-ttu-id="11672-219">Hello Corosync примеры файлов можно использовать для одноадресной рассылки или изменение привязки, адреса, списки узлов и каталогах ведения журнала (использует Ubuntu `/var/log/corosync` хотя пример hello файлами `/var/log/cluster`) и включить средства кворума.</span><span class="sxs-lookup"><span data-stu-id="11672-219">We can use hello Corosync example files for Unicast and change bind address, node lists, and logging directories (Ubuntu uses `/var/log/corosync` while hello example files use `/var/log/cluster`), and enable quorum tools.</span></span>

> [!NOTE]
> <span data-ttu-id="11672-220">Используйте следующие hello `transport: udpu` директивы и hello определенные вручную IP-адреса для обоих узлов.</span><span class="sxs-lookup"><span data-stu-id="11672-220">Use hello following `transport: udpu` directive and hello manually defined IP addresses for both nodes.</span></span>

<span data-ttu-id="11672-221">Выполнения hello следующий код в `/etc/corosync/corosync.conf` для обоих узлов:</span><span class="sxs-lookup"><span data-stu-id="11672-221">Run hello following code on `/etc/corosync/corosync.conf` for both nodes:</span></span>

    totem {
      version: 2
      crypto_cipher: none
      crypto_hash: none
      interface {
        ringnumber: 0
        bindnetaddr: 10.10.10.0
        mcastport: 5405
        ttl: 1
      }
      transport: udpu
    }

    logging {
      fileline: off
      to_logfile: yes
      to_syslog: yes
      logfile: /var/log/corosync/corosync.log
      debug: off
      timestamp: on
      logger_subsys {
        subsys: QUORUM
        debug: off
        }
      }

    nodelist {
      node {
        ring0_addr: 10.10.10.4
        nodeid: 1
      }

      node {
        ring0_addr: 10.10.10.5
        nodeid: 2
      }
    }

    quorum {
      provider: corosync_votequorum
    }

<span data-ttu-id="11672-222">Скопируйте этот файл конфигурации на обе виртуальные машины и запустите Corosync в обоих узлах.</span><span class="sxs-lookup"><span data-stu-id="11672-222">Copy this configuration file on both VMs and start Corosync in both nodes:</span></span>

    sudo service start corosync

<span data-ttu-id="11672-223">Вскоре после запуска службы hello, hello кластера следует установить в текущей кольцо hello и следует круглую кворума.</span><span class="sxs-lookup"><span data-stu-id="11672-223">Shortly after starting hello service, hello cluster should be established in hello current ring, and quorum should be constituted.</span></span> <span data-ttu-id="11672-224">Эту функцию можно проверить, просмотрев журналы или запустив hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="11672-224">We can check this functionality by reviewing logs or by running hello following code:</span></span>

    sudo corosync-quorumtool –l

<span data-ttu-id="11672-225">Вы увидите примерно toohello выходных данных после изображения.</span><span class="sxs-lookup"><span data-stu-id="11672-225">You will see output similar toohello following image:</span></span>

![corosync-quorumtool -l sample output](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a><span data-ttu-id="11672-227">Установка Pacemaker</span><span class="sxs-lookup"><span data-stu-id="11672-227">Set up Pacemaker</span></span>
<span data-ttu-id="11672-228">Использует pacemaker hello toomonitor кластера для ресурсов, определить, когда в источниках вышли из строя и переключение toosecondaries эти ресурсы.</span><span class="sxs-lookup"><span data-stu-id="11672-228">Pacemaker uses hello cluster toomonitor for resources, define when primaries go down, and switch those resources toosecondaries.</span></span> <span data-ttu-id="11672-229">Ресурсы можно задавать с помощью ряда доступных скриптов или с помощью скриптов LSB (подобных init), а также другими способами.</span><span class="sxs-lookup"><span data-stu-id="11672-229">Resources can be defined from a set of available scripts or from LSB (init-like) scripts, among other choices.</span></span>

<span data-ttu-id="11672-230">Мы хотим Pacemaker ресурсов DRBD слишком «собственные» hello, точки подключения hello и службу MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="11672-230">We want Pacemaker too"own" hello DRBD resource, hello mount point, and hello MySQL service.</span></span> <span data-ttu-id="11672-231">Если Pacemaker можно включать и отключать DRBD, подключения и отключить его и затем запускать и останавливать MySQL в hello правой порядок каких-либо неправильный происходит с hello первичных, Настройка завершена.</span><span class="sxs-lookup"><span data-stu-id="11672-231">If Pacemaker can turn on and off DRBD, mount and unmount it, and then start and stop MySQL in hello right order when something bad happens with hello primary, setup is complete.</span></span>

<span data-ttu-id="11672-232">При первой установке Pacemaker конфигурация должна быть довольно простой, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="11672-232">When you first install Pacemaker, your configuration should be simple enough, something like:</span></span>

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. <span data-ttu-id="11672-233">Проверьте конфигурацию hello, запустив `sudo crm configure show`.</span><span class="sxs-lookup"><span data-stu-id="11672-233">Check hello configuration by running `sudo crm configure show`.</span></span>
2. <span data-ttu-id="11672-234">Затем создайте файл (например `/tmp/cluster.conf`) с hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="11672-234">Then create a file (like `/tmp/cluster.conf`) with hello following resources:</span></span>

        primitive drbd_mysql ocf:linbit:drbd \
              params drbd_resource="r0" \
              op monitor interval="29s" role="Master" \
              op monitor interval="31s" role="Slave"

        ms ms_drbd_mysql drbd_mysql \
              meta master-max="1" master-node-max="1" \
                clone-max="2" clone-node-max="1" \
                notify="true"

        primitive fs_mysql ocf:heartbeat:Filesystem \
              params device="/dev/drbd/by-res/r0" \
              directory="/var/lib/mysql" fstype="ext3"

        primitive mysqld lsb:mysql

        group mysql fs_mysql mysqld

        colocation mysql_on_drbd \
               inf: mysql ms_drbd_mysql:Master

        order mysql_after_drbd \
               inf: ms_drbd_mysql:promote mysql:start

        property stonith-enabled=false

        property no-quorum-policy=ignore

3. <span data-ttu-id="11672-235">Загрузите hello в конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="11672-235">Load hello file into hello configuration.</span></span> <span data-ttu-id="11672-236">Требуется только toodo это в один узел.</span><span class="sxs-lookup"><span data-stu-id="11672-236">You only need toodo this in one node.</span></span>

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. <span data-ttu-id="11672-237">Убедитесь, что Pacemaker запускается при загрузке в обоих узлах.</span><span class="sxs-lookup"><span data-stu-id="11672-237">Make sure that Pacemaker starts at boot in both nodes:</span></span>

        sudo update-rc.d pacemaker defaults

5. <span data-ttu-id="11672-238">С помощью `sudo crm_mon –L`, убедитесь, что один из узлов становится master hello для кластера hello и управлением ресурсами hello.</span><span class="sxs-lookup"><span data-stu-id="11672-238">By using `sudo crm_mon –L`, verify that one of your nodes has become hello master for hello cluster and is running all hello resources.</span></span> <span data-ttu-id="11672-239">Можно использовать подключения и ps toocheck работающие ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="11672-239">You can use mount and ps toocheck that hello resources are running.</span></span>

<span data-ttu-id="11672-240">Привет, следуя снимке экрана показано `crm_mon` с одним узлом остановлена (выход, нажав сочетание клавиш Ctrl + C):</span><span class="sxs-lookup"><span data-stu-id="11672-240">hello following screenshot shows `crm_mon` with one node stopped (exit by selecting Ctrl+C):</span></span>

![crm_mon node stopped](./media/mysql-cluster/image002.png)

<span data-ttu-id="11672-242">На следующем снимке экрана показаны оба узла, один из которых главный, а второй подчиненный.</span><span class="sxs-lookup"><span data-stu-id="11672-242">This screenshot shows both nodes, one master and one slave:</span></span>

![crm_mon operational master/slave](./media/mysql-cluster/image003.png)

## <a name="testing"></a><span data-ttu-id="11672-244">Тестирование</span><span class="sxs-lookup"><span data-stu-id="11672-244">Testing</span></span>
<span data-ttu-id="11672-245">Теперь все готово для моделирования автоматической отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="11672-245">You're ready for an automatic failover simulation.</span></span> <span data-ttu-id="11672-246">Существует два способа toodo это: мягких и жестких.</span><span class="sxs-lookup"><span data-stu-id="11672-246">There are two ways toodo this: soft and hard.</span></span>

<span data-ttu-id="11672-247">Hello мягкий способ использует функции завершения работы кластера hello: ``crm_standby -U `uname -n` -v on``.</span><span class="sxs-lookup"><span data-stu-id="11672-247">hello soft way uses hello cluster's shutdown function: ``crm_standby -U `uname -n` -v on``.</span></span> <span data-ttu-id="11672-248">Если вы используете образец hello, переходит ведомый hello.</span><span class="sxs-lookup"><span data-stu-id="11672-248">If you use this on hello master, hello slave takes over.</span></span> <span data-ttu-id="11672-249">Помните, tooset этот toooff назад.</span><span class="sxs-lookup"><span data-stu-id="11672-249">Remember tooset this back toooff.</span></span> <span data-ttu-id="11672-250">Если вы этого не сделаете, crm_mon будет сообщать, что один из узлов находится в резервном режиме.</span><span class="sxs-lookup"><span data-stu-id="11672-250">If you don't, crm_mon will show one node on standby.</span></span>

<span data-ttu-id="11672-251">Hello трудным способом завершает работу hello основной ВМ (hadb01) через портал hello или изменяя hello runlevel на hello виртуальной Машины (то есть, остановка, завершение работы).</span><span class="sxs-lookup"><span data-stu-id="11672-251">hello hard way is shutting down hello primary VM (hadb01) via hello portal or by changing hello runlevel on hello VM (that is, halt, shutdown).</span></span> <span data-ttu-id="11672-252">Это помогает Corosync и Pacemaker путем передачи сигналов, образец hello переход вниз.</span><span class="sxs-lookup"><span data-stu-id="11672-252">This helps Corosync and Pacemaker by signaling that hello master's going down.</span></span> <span data-ttu-id="11672-253">Это можно проверить (полезно для окна обслуживания), но можно также принудительно сценарий hello, закрепление hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="11672-253">You can test this (useful for maintenance windows), but you can also force hello scenario by freezing hello VM.</span></span>

## <a name="stonith"></a><span data-ttu-id="11672-254">STONITH</span><span class="sxs-lookup"><span data-stu-id="11672-254">STONITH</span></span>
<span data-ttu-id="11672-255">Оно должно быть возможно tooissue завершение работы виртуальной Машины через hello Azure CLI вместо STONITH скрипт, который управляет физического устройства.</span><span class="sxs-lookup"><span data-stu-id="11672-255">It should be possible tooissue a VM shutdown via hello Azure CLI in lieu of a STONITH script that controls a physical device.</span></span> <span data-ttu-id="11672-256">Можно использовать `/usr/lib/stonith/plugins/external/ssh` как базового и включить STONITH в конфигурации кластера hello.</span><span class="sxs-lookup"><span data-stu-id="11672-256">You can use `/usr/lib/stonith/plugins/external/ssh` as a base and enable STONITH in hello cluster's configuration.</span></span> <span data-ttu-id="11672-257">Azure CLI глобально должны быть установлены и параметры публикации hello и загружать профиль пользователя hello кластера.</span><span class="sxs-lookup"><span data-stu-id="11672-257">Azure CLI should be globally installed, and hello publish settings and profile should be loaded for hello cluster's user.</span></span>

<span data-ttu-id="11672-258">Образцы кода для hello ресурс доступен на [GitHub](https://github.com/bureado/aztonith).</span><span class="sxs-lookup"><span data-stu-id="11672-258">Sample code for hello resource is available on [GitHub](https://github.com/bureado/aztonith).</span></span> <span data-ttu-id="11672-259">Изменения конфигурации кластера hello, добавив hello слишком следующие`sudo crm configure`:</span><span class="sxs-lookup"><span data-stu-id="11672-259">Change hello cluster's configuration by adding hello following too`sudo crm configure`:</span></span>

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> <span data-ttu-id="11672-260">сценарий Hello не выполняет проверок вверх или вниз.</span><span class="sxs-lookup"><span data-stu-id="11672-260">hello script doesn't perform up/down checks.</span></span> <span data-ttu-id="11672-261">Исходный ресурс SSH Hello присутствовал 15 проверки ping, однако время восстановления для виртуальной Машины Azure может быть несколько переменной.</span><span class="sxs-lookup"><span data-stu-id="11672-261">hello original SSH resource had 15 ping checks, but recovery time for an Azure VM might be more variable.</span></span>

## <a name="limitations"></a><span data-ttu-id="11672-262">Ограничения</span><span class="sxs-lookup"><span data-stu-id="11672-262">Limitations</span></span>
<span data-ttu-id="11672-263">применяются следующие ограничения Hello.</span><span class="sxs-lookup"><span data-stu-id="11672-263">hello following limitations apply:</span></span>

* <span data-ttu-id="11672-264">Здравствуйте, linbit DRBD ресурсов скрипт, который управляет DRBD как ресурс в Pacemaker использует `drbdadm down` при выключении узел, даже если просто hello узел в режим ожидания.</span><span class="sxs-lookup"><span data-stu-id="11672-264">hello linbit DRBD resource script that manages DRBD as a resource in Pacemaker uses `drbdadm down` when shutting down a node, even if hello node is just going on standby.</span></span> <span data-ttu-id="11672-265">Это не идеальное решение, поскольку ведомый hello не синхронизироваться будут hello DRBD ресурсов во время записи возвращает образец hello.</span><span class="sxs-lookup"><span data-stu-id="11672-265">This is not ideal because hello slave will not be synchronizing hello DRBD resource while hello master gets writes.</span></span> <span data-ttu-id="11672-266">Образец hello не позволяет любезно, ведомый hello может взять на себя более старые состояния файловой системы.</span><span class="sxs-lookup"><span data-stu-id="11672-266">If hello master does not fail graciously, hello slave can take over an older file system state.</span></span> <span data-ttu-id="11672-267">Имеется два способа разрешения этой проблемы:</span><span class="sxs-lookup"><span data-stu-id="11672-267">There are two potential ways of solving this:</span></span>
  * <span data-ttu-id="11672-268">принудительное выполнение `drbdadm up r0` во всех узлах кластера с помощью локальной (не кластерной) программы наблюдения watchdog;</span><span class="sxs-lookup"><span data-stu-id="11672-268">Enforcing a `drbdadm up r0` in all cluster nodes via a local (not clusterized) watchdog</span></span>
  * <span data-ttu-id="11672-269">Изменение сценария DRBD linbit hello, убедившись, что `down` не вызывается в`/usr/lib/ocf/resource.d/linbit/drbd`</span><span class="sxs-lookup"><span data-stu-id="11672-269">Editing hello linbit DRBD script, making sure that `down` is not called in `/usr/lib/ocf/resource.d/linbit/drbd`</span></span>
* <span data-ttu-id="11672-270">Подсистема балансировки нагрузки Hello требуется toorespond по крайней мере пять секунд, приложения должны быть кластеры и должны быть более нечувствительного к ошибкам времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="11672-270">hello load balancer needs at least five seconds toorespond, so applications should be cluster-aware and be more tolerant of timeout.</span></span> <span data-ttu-id="11672-271">Другие архитектуры, например очереди в приложении и ПО промежуточного слоя запроса, также могут быть полезными.</span><span class="sxs-lookup"><span data-stu-id="11672-271">Other architectures, like in-app queues and query middlewares, can also help.</span></span>
* <span data-ttu-id="11672-272">MySQL тонкая настройка — необходимые tooensure, запись осуществляется в управляемую темпе и кэшей будут сброшены toodisk так же часто, как потеря возможных toominimize памяти.</span><span class="sxs-lookup"><span data-stu-id="11672-272">MySQL tuning is necessary tooensure that writing is done at a manageable pace and caches are flushed toodisk as frequently as possible toominimize memory loss.</span></span>
* <span data-ttu-id="11672-273">Запись в виртуальной Машине зависит производительность соединений hello виртуального коммутатора, поскольку это hello механизм, используемый устройством hello DRBD tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="11672-273">Write performance is dependent in VM interconnect in hello virtual switch because this is hello mechanism used by DRBD tooreplicate hello device.</span></span>
