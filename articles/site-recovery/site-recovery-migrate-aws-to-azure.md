---
title: "aaaMigrate виртуальных машин из AWS tooAzure | Документы Microsoft"
description: "В этой статье описывается, как toomigrate виртуальных машин выполняется в tooAzure Amazon Web Services (AWS), с помощью Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: bsiva
manager: jwhit
editor: 
ms.assetid: ddb412fd-32a8-4afa-9e39-738b11b91118
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: c99b781ec9cca5b8f9a847d3fc48408062b120b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-tooazure-with-azure-site-recovery"></a><span data-ttu-id="eb8ec-103">Перенос виртуальных машин в tooAzure Amazon Web Services (AWS) с Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="eb8ec-103">Migrate virtual machines in Amazon Web Services (AWS) tooAzure with Azure Site Recovery</span></span>

<span data-ttu-id="eb8ec-104">В этой статье описывается, как toomigrate AWS Windows экземпляров tooAzure виртуальных машин с hello [Azure Site Recovery](site-recovery-overview.md) службы.</span><span class="sxs-lookup"><span data-stu-id="eb8ec-104">This article describes how toomigrate AWS Windows instances tooAzure virtual machines with hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="eb8ec-105">Миграция фактически происходит переход из AWS tooAzure.</span><span class="sxs-lookup"><span data-stu-id="eb8ec-105">Migration is effectively a failover from AWS tooAzure.</span></span> <span data-ttu-id="eb8ec-106">Вы не можете tooAWS машины восстановления размещения и нет текущей репликации.</span><span class="sxs-lookup"><span data-stu-id="eb8ec-106">You can't failback machines tooAWS, and there's no ongoing replication.</span></span> <span data-ttu-id="eb8ec-107">В этой статье описываются шаги hello для миграции в hello портал Azure и основаны на hello инструкции по [репликации tooAzure физический компьютер](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="eb8ec-107">This article describes hello steps for migration in hello Azure portal, and are based on hello instructions for [replicating a physical machine tooAzure](site-recovery-vmware-to-azure.md).</span></span>

<span data-ttu-id="eb8ec-108">Отправьте все комментарии или вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="eb8ec-108">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="eb8ec-109">Поддерживаемые операционные системы</span><span class="sxs-lookup"><span data-stu-id="eb8ec-109">Supported operating systems</span></span>

<span data-ttu-id="eb8ec-110">Site Recovery может быть под управлением любой из следующих операционных систем hello экземпляров используется toomigrate EC2:</span><span class="sxs-lookup"><span data-stu-id="eb8ec-110">Site Recovery can be used toomigrate EC2 instances running any of hello following operating systems:</span></span>

- <span data-ttu-id="eb8ec-111">Windows (только 64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="eb8ec-111">Windows(64 bit only)</span></span>
    - <span data-ttu-id="eb8ec-112">Windows Server 2008 R2 с пакетом обновления 1 или более поздняя версия (Поддерживаются только драйверы Citrix PV и драйверы AWS PV.</span><span class="sxs-lookup"><span data-stu-id="eb8ec-112">Windows Server 2008 R2 SP1+ (Citrix PV drivers or AWS PV drivers only.</span></span> <span data-ttu-id="eb8ec-113">**Экземпляры с драйверами RedHat PV не поддерживаются**.) Windows Server 2012, Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="eb8ec-113">**Instances running RedHat PV drivers are not supported**) Windows Server 2012 Windows Server 2012 R2</span></span>
- <span data-ttu-id="eb8ec-114">Linux (только 64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="eb8ec-114">Linux (64 bit only)</span></span>
    - <span data-ttu-id="eb8ec-115">Red Hat Enterprise Linux 6.7 (только виртуализированные экземпляры HVM).</span><span class="sxs-lookup"><span data-stu-id="eb8ec-115">Red Hat Enterprise Linux 6.7 (HVM virtualized instances only)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb8ec-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="eb8ec-116">Prerequisites</span></span>

<span data-ttu-id="eb8ec-117">Вот что нужно для этого развертывания:</span><span class="sxs-lookup"><span data-stu-id="eb8ec-117">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="eb8ec-118">**Сервер конфигурации**: развертывании виртуальной Машины EC2 Amazon под управлением Windows Server 2012 R2 в качестве hello конфигурации сервера.</span><span class="sxs-lookup"><span data-stu-id="eb8ec-118">**Configuration server**: An Amazon EC2 VM running Windows Server 2012 R2 is deployed as hello configuration server.</span></span> <span data-ttu-id="eb8ec-119">По умолчанию hello другие компоненты Azure Site Recovery (сервер обработки и главного целевого сервера) устанавливаются при развертывании сервера конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="eb8ec-119">By default, hello other Azure Site Recovery components (process server and master target server) are installed when you deploy hello configuration server.</span></span> <span data-ttu-id="eb8ec-120">В этой статье описываются шаги hello для миграции в hello портал Azure и основаны на hello инструкции по [Дополнительные сведения](site-recovery-components.md)</span><span class="sxs-lookup"><span data-stu-id="eb8ec-120">This article describes hello steps for migration in hello Azure portal, and are based on hello instructions for  [Learn more](site-recovery-components.md)</span></span>

* <span data-ttu-id="eb8ec-121">**Экземпляры EC2**: hello Amazon EC2 экземплярах виртуальных машин, что требуется toomigrate.</span><span class="sxs-lookup"><span data-stu-id="eb8ec-121">**EC2 instances**: hello Amazon EC2 virtual machines instances that you want toomigrate.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="eb8ec-122">Шаги по развертыванию</span><span class="sxs-lookup"><span data-stu-id="eb8ec-122">Deployment steps</span></span>

1. <span data-ttu-id="eb8ec-123">Создайте хранилище служб восстановления,</span><span class="sxs-lookup"><span data-stu-id="eb8ec-123">Create a Recovery Services vault.</span></span>
2. <span data-ttu-id="eb8ec-124">Hello группы безопасности в экземплярах EC2 должны иметь правила, настроенные tooallow взаимодействия экземпляр EC2 hello, нужно toomigrate, а экземпляр hello плана hello toodeploy сервер конфигурации.</span><span class="sxs-lookup"><span data-stu-id="eb8ec-124">hello Security Group of your EC2 instances should have rules configured tooallow communication between hello EC2 instance that you want toomigrate, and hello instance on which you plan toodeploy hello Configuration Server.</span></span>

3. <span data-ttu-id="eb8ec-125">На hello же Amazon виртуального частного облака как своих экземпляров EC2 развертывание сервера конфигурации ASR.</span><span class="sxs-lookup"><span data-stu-id="eb8ec-125">On hello same Amazon Virtual Private Cloud as your EC2 instances, deploy an ASR configuration server.</span></span> <span data-ttu-id="eb8ec-126">Ссылаться hello VMware или физических tooAzure необходимые условия для требования для развертывания сервера конфигурации.</span><span class="sxs-lookup"><span data-stu-id="eb8ec-126">Refer hello VMware / Physical tooAzure prerequisites for configuration server deployment requirements.</span></span>

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  <span data-ttu-id="eb8ec-128">Как только сервер конфигурации развертывается в AWS и зарегистрирован в хранилище служб восстановления, вы увидите hello конфигурации сервера и сервера обработки в меню инфраструктуры Site Recovery как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="eb8ec-128">Once your configuration server is deployed in AWS and registered with your Recovery Services vault, you should see hello configuration server and process server under Site Recovery infrastructure as shown below:</span></span>

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. <span data-ttu-id="eb8ec-130">После развертывания сервера конфигурации hello (он может занять too15 minustes для него tooappear), проверки, он может взаимодействовать с виртуальными машинами hello нужных toomigrate.</span><span class="sxs-lookup"><span data-stu-id="eb8ec-130">After you've deployed hello configuration server (it might take up too15 minustes for it tooappear), validate that it can communicate with hello VMs that you want toomigrate.</span></span>

6. <span data-ttu-id="eb8ec-131">[Настройте параметры репликации](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="eb8ec-131">[Set up replication settings](site-recovery-setup-replication-settings-vmware.md).</span></span>

7. <span data-ttu-id="eb8ec-132">Включение репликации: включить репликацию для виртуальных машин, которые вы хотите toomigrate hello.</span><span class="sxs-lookup"><span data-stu-id="eb8ec-132">Enable replication: Enable replication for hello VMs you want toomigrate.</span></span> <span data-ttu-id="eb8ec-133">Вы можете узнать hello EC2 экземпляров с помощью hello частного IP-адреса, можно получить из консоли EC2 hello.</span><span class="sxs-lookup"><span data-stu-id="eb8ec-133">You can discover hello EC2 instances using hello private IP addresses, which you can get from hello EC2 console.</span></span>

    ![Выбор виртуальной машины](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. <span data-ttu-id="eb8ec-135">После защищенных экземпляров hello EC2 и tooAzure hello репликации завершена, [выполнить тестовую отработку отказа](site-recovery-test-failover-to-azure.md) toovalidate производительность приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="eb8ec-135">Once hello EC2 instances have been protected and hello replication tooAzure is complete, [run a Test Failover](site-recovery-test-failover-to-azure.md) toovalidate your application's performance in Azure.</span></span>

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. <span data-ttu-id="eb8ec-137">Запуск отработки отказа из AWS tooAzure для каждой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="eb8ec-137">Run a Failover from AWS tooAzure for each VM.</span></span> <span data-ttu-id="eb8ec-138">При необходимости можно создать план восстановления и запускать несколько виртуальных машин отработки отказа, toomigrate из AWS tooAzure.</span><span class="sxs-lookup"><span data-stu-id="eb8ec-138">Optionally, you can create a recovery plan and run a Failover, toomigrate multiple virtual machines from AWS tooAzure.</span></span> <span data-ttu-id="eb8ec-139">[Узнайте подробнее](site-recovery-create-recovery-plans.md) о планах восстановления.</span><span class="sxs-lookup"><span data-stu-id="eb8ec-139">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

10. <span data-ttu-id="eb8ec-140">Для миграции не требуется toocommit отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="eb8ec-140">For migration, you don't need toocommit a failover.</span></span> <span data-ttu-id="eb8ec-141">Вместо этого выберите параметр выполнения миграции hello для каждого компьютера требуется toomigrate.</span><span class="sxs-lookup"><span data-stu-id="eb8ec-141">Instead, you select hello Complete Migration option for each machine you want toomigrate.</span></span> <span data-ttu-id="eb8ec-142">Hello выполнения миграции действие завершения процесса миграции hello, удаляет репликации для машины hello и прекращает выставления счетов для машины hello Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="eb8ec-142">hello Complete Migration action finishes up hello migration process, removes replication for hello machine, and stops Site Recovery billing for hello machine.</span></span>

    ![Миграция](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a><span data-ttu-id="eb8ec-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eb8ec-144">Next steps</span></span>

- <span data-ttu-id="eb8ec-145">[Подготовка репликации машин в процессе миграции tooenable](site-recovery-azure-to-azure-after-migration.md) tooanother регионе для аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="eb8ec-145">[Prepare migrated machines tooenable replication](site-recovery-azure-to-azure-after-migration.md) tooanother region for disaster recovery needs.</span></span>
- <span data-ttu-id="eb8ec-146">Включите защиту рабочих нагрузок, [выполнив репликацию виртуальных машин Azure.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="eb8ec-146">Start protecting your workloads by [replicating Azure virtual machines.](site-recovery-azure-to-azure.md)</span></span>
