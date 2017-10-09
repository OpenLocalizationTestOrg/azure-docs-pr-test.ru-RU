---
title: "aaaSet hello исходного и целевого объекта для VMware tooAzure репликации с помощью Azure Site Recovery | Документы Microsoft"
description: "Перечислены tooset действия hello исходных и целевых параметров репликации виртуальных машин VMware tooAzure хранилища с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99e422e-daf7-4fa8-af3c-af2340340136
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ef33a44bc5da17afb0442be63f576925f5b9a8b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-vmware-replication-tooazure"></a><span data-ttu-id="b65c2-103">Шаг 8: Настройка hello исходной и целевой для VMware tooAzure репликации</span><span class="sxs-lookup"><span data-stu-id="b65c2-103">Step 8: Set up hello source and target for VMware replication tooAzure</span></span>

<span data-ttu-id="b65c2-104">В этой статье описывается, как tooconfigure источника и целевых параметров при репликации локально tooAzure виртуальные машины VMware, с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b65c2-104">This article describes how tooconfigure source and target settings when replicating on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="b65c2-105">Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="b65c2-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="b65c2-106">Настройка среды источника hello</span><span class="sxs-lookup"><span data-stu-id="b65c2-106">Set up hello source environment</span></span>

<span data-ttu-id="b65c2-107">Настройка сервера конфигурации hello, зарегистрируйте его в хранилище hello и обнаружение виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b65c2-107">Set up hello configuration server, register it in hello vault, and discover VMs.</span></span>

1. <span data-ttu-id="b65c2-108">Щелкните **Site Recovery** > **Шаг 1. Подготовка инфраструктуры** > **Источник**.</span><span class="sxs-lookup"><span data-stu-id="b65c2-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="b65c2-109">Если у вас нет сервера конфигурации, щелкните **+Configuration server** (+ Сервер конфигурации).</span><span class="sxs-lookup"><span data-stu-id="b65c2-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="b65c2-110">В колонке **Добавление сервера** в поле **Тип сервера** должно быть указано **Сервер конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="b65c2-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="b65c2-111">Загрузите файл установки hello установка единой Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="b65c2-111">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="b65c2-112">Загрузите ключ регистрации в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="b65c2-112">Download hello vault registration key.</span></span> <span data-ttu-id="b65c2-113">Он потребуется при запуске единой установки.</span><span class="sxs-lookup"><span data-stu-id="b65c2-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="b65c2-114">Hello ключ действителен в течение пяти дней после его создания.</span><span class="sxs-lookup"><span data-stu-id="b65c2-114">hello key is valid for five days after you generate it.</span></span>

   ![Настройка источника](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a><span data-ttu-id="b65c2-116">Зарегистрируйте сервер конфигурации hello в хранилище hello</span><span class="sxs-lookup"><span data-stu-id="b65c2-116">Register hello configuration server in hello vault</span></span>

<span data-ttu-id="b65c2-117">Следующие hello, прежде чем начать, а затем выполните tooinstall hello конфигурации сервера, сервера обработки hello и главный целевой сервер hello единой программы установки.</span><span class="sxs-lookup"><span data-stu-id="b65c2-117">Do hello following before you start, then run Unified Setup tooinstall hello configuration server, hello process server, and hello master target server.</span></span>
    - <span data-ttu-id="b65c2-118">Посмотрите краткий видеообзор:</span><span class="sxs-lookup"><span data-stu-id="b65c2-118">Get a quick video overview</span></span>

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - <span data-ttu-id="b65c2-119">На сервере конфигурации hello виртуальной Машины, убедитесь, что системные часы, hello синхронизируется с [сервер времени](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="b65c2-119">On hello configuration server VM, make sure that hello system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="b65c2-120">Значения времени должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="b65c2-120">It should match.</span></span> <span data-ttu-id="b65c2-121">Если системные часы отстают или спешат в пределах 15 минут, установка может завершиться ошибкой.</span><span class="sxs-lookup"><span data-stu-id="b65c2-121">If it's 15 minutes in front or behind, setup might fail.</span></span>
    - <span data-ttu-id="b65c2-122">Запустите программу установки с учетной записью локального администратора на сервере hello конфигурации виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="b65c2-122">Run setup as a Local Administrator on hello configuration server VM.</span></span>
    - <span data-ttu-id="b65c2-123">Убедитесь в том, что протоколы TLS 1.0 включен в hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="b65c2-123">Make sure TLS 1.0 is enabled on hello VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="b65c2-124">также можно установить сервер конфигурации Hello [из командной строки hello](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="b65c2-124">hello configuration server can also be installed [from hello command line](http://aka.ms/installconfigsrv).</span></span>



## <a name="connect-toovmware-servers"></a><span data-ttu-id="b65c2-125">Подключение серверов tooVMware</span><span class="sxs-lookup"><span data-stu-id="b65c2-125">Connect tooVMware servers</span></span>

<span data-ttu-id="b65c2-126">tooallow Azure Site Recovery toodiscover виртуальных машин, работающих в локальной среде, необходимо tooconnect VMware vCenter Server или узлы vSphere ESXi с Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="b65c2-126">tooallow Azure Site Recovery toodiscover virtual machines running in your on-premises environment, you need tooconnect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span> <span data-ttu-id="b65c2-127">Прежде чем начать, обратите внимание hello следующие:</span><span class="sxs-lookup"><span data-stu-id="b65c2-127">Note hello following before you start:</span></span>

- <span data-ttu-id="b65c2-128">При добавлении сервера vCenter hello или узлы vSphere tooSite восстановления с помощью учетной записи без прав администратора на сервере hello, учетная запись hello должна включены следующие права доступа:</span><span class="sxs-lookup"><span data-stu-id="b65c2-128">If you add hello vCenter server or vSphere hosts tooSite Recovery with an account without administrator privileges on hello server, hello account needs these privileges enabled:</span></span>
    - <span data-ttu-id="b65c2-129">привилегии центра обработки данных, хранилища данных, папки, узла, сети, ресурса, виртуальной машины и распределенного коммутатора vSphere;</span><span class="sxs-lookup"><span data-stu-id="b65c2-129">Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, vSphere Distributed Switch.</span></span>
    - <span data-ttu-id="b65c2-130">сервер vCenter Hello необходимы разрешения представления хранилища.</span><span class="sxs-lookup"><span data-stu-id="b65c2-130">hello vCenter server needs Storage views permissions.</span></span>
- <span data-ttu-id="b65c2-131">При добавлении серверов VMware tooSite восстановления может потребоваться 15 минут или больше времени для них tooappear hello портала.</span><span class="sxs-lookup"><span data-stu-id="b65c2-131">When you add VMware servers tooSite Recovery, it can take 15 minutes or longer for them tooappear in hello portal.</span></span>

### <a name="add-hello-account-for-automatic-discovery"></a><span data-ttu-id="b65c2-132">Добавьте учетную запись hello автоматического обнаружения</span><span class="sxs-lookup"><span data-stu-id="b65c2-132">Add hello account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a><span data-ttu-id="b65c2-133">Настройка подключения</span><span class="sxs-lookup"><span data-stu-id="b65c2-133">Set up a connection</span></span>

<span data-ttu-id="b65c2-134">Подключение tooservers следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b65c2-134">Connect tooservers as follows:</span></span>

1. <span data-ttu-id="b65c2-135">Выберите **+ vCenter** toostart подключение сервера VMware vCenter server или узла ESXi VMware vSphere.</span><span class="sxs-lookup"><span data-stu-id="b65c2-135">Select **+vCenter** toostart connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>
2. <span data-ttu-id="b65c2-136">В **добавьте vCenter**, укажите понятное имя для сервера узла или vCenter vSphere hello, а затем укажите hello IP-адрес или полное доменное имя сервера hello.</span><span class="sxs-lookup"><span data-stu-id="b65c2-136">In **Add vCenter**, specify a friendly name for hello vSphere host or vCenter server, and then specify hello IP address or FQDN of hello server.</span></span>
3. <span data-ttu-id="b65c2-137">Если серверы VMware, настроенных toolisten для запросов на другой порт оставьте hello порт 443.</span><span class="sxs-lookup"><span data-stu-id="b65c2-137">Leave hello port as 443 unless your VMware servers are configured toolisten for requests on a different port.</span></span> <span data-ttu-id="b65c2-138">Выберите учетную запись hello tooconnect toohello VMware vCenter или vSphere ESXi сервера.</span><span class="sxs-lookup"><span data-stu-id="b65c2-138">Select hello account that is tooconnect toohello VMware vCenter or vSphere ESXi server.</span></span> <span data-ttu-id="b65c2-139">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b65c2-139">Click **OK**.</span></span>
4. <span data-ttu-id="b65c2-140">Site Recovery подключает tooVMware серверы с помощью hello указаны параметры и выполняет обнаружение виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b65c2-140">Site Recovery connects tooVMware servers using hello specified settings, and discovers VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="b65c2-141">При добавлении сервера или узел с учетной записью, не имеет прав администратора на сервере vCenter или узла hello, убедитесь, что учетная запись hello имеет включены следующие права доступа: центра обработки данных, хранилище данных, папки, узла, сети, ресурс виртуальной машины и vSphere распределенных коммутатора.</span><span class="sxs-lookup"><span data-stu-id="b65c2-141">If you're adding a server or host with an account that doesn't have administrator privileges on hello vCenter or host server, make sure that hello account has these privileges enabled: Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, and vSphere Distributed Switch.</span></span> <span data-ttu-id="b65c2-142">Кроме того hello VMware vCenter server должен включены привилегий представления хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="b65c2-142">In addition, hello VMware vCenter server needs hello Storage Views privilege enabled.</span></span>


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="b65c2-143">Настройка целевой среды hello</span><span class="sxs-lookup"><span data-stu-id="b65c2-143">Set up hello target environment</span></span>

<span data-ttu-id="b65c2-144">Перед настройкой hello целевой среде, убедитесь, что у вас есть учетная запись хранения Azure и настройка виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b65c2-144">Before you set up hello target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="b65c2-145">Нажмите кнопку **подготовки инфраструктуры** > **целевой**, и выберите hello требуется toouse подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="b65c2-145">Click **Prepare infrastructure** > **Target**, and select hello Azure subscription you want toouse.</span></span>
2. <span data-ttu-id="b65c2-146">Укажите, какая целевая модель развертывания используется: классическая или Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b65c2-146">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="b65c2-147">Site Recovery проверяет наличие одной или нескольких совместимых учетных записей хранения и сетей Azure.</span><span class="sxs-lookup"><span data-stu-id="b65c2-147">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![Цель](./media/vmware-walkthrough-source-target/gs-target.png)
4. <span data-ttu-id="b65c2-149">Если вы еще не создали учетную запись хранения или сети, нажмите кнопку **+ учетная запись хранения** или **+ сети**, toocreate диспетчера ресурсов учетной записи или сети встроенной.</span><span class="sxs-lookup"><span data-stu-id="b65c2-149">If you haven't created a storage account or network, click **+Storage account** or **+Network**, toocreate a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b65c2-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b65c2-150">Next steps</span></span>

<span data-ttu-id="b65c2-151">Go слишком[шаг 9: настроить политику репликации](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="b65c2-151">Go too[Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>
