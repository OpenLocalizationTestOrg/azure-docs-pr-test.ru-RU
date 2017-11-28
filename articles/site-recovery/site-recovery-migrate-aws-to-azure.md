---
title: "Миграция виртуальных машин из AWS в Azure | Документация Майкрософт"
description: "В этой статье описано, как перенести виртуальные машины, запущенные в Amazon Web Services (AWS), в Azure с помощью Azure Site Recovery."
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
ms.openlocfilehash: b3c0727a279649f4f7dae30d41027129ce5b04ee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-to-azure-with-azure-site-recovery"></a><span data-ttu-id="04e87-103">Перенос виртуальных машин из Amazon Web Services (AWS) в Azure с помощью Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="04e87-103">Migrate virtual machines in Amazon Web Services (AWS) to Azure with Azure Site Recovery</span></span>

<span data-ttu-id="04e87-104">В этой статье описано, как перенести экземпляры Windows из Amazon Web Services (AWS) в Виртуальные машины Azure с помощью службы [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="04e87-104">This article describes how to migrate AWS Windows instances to Azure virtual machines with the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="04e87-105">Миграция фактически является отработкой отказа из AWS в Azure.</span><span class="sxs-lookup"><span data-stu-id="04e87-105">Migration is effectively a failover from AWS to Azure.</span></span> <span data-ttu-id="04e87-106">Однако восстановить размещение машин в AWS невозможно, и репликация данных не выполняется.</span><span class="sxs-lookup"><span data-stu-id="04e87-106">You can't failback machines to AWS, and there's no ongoing replication.</span></span> <span data-ttu-id="04e87-107">Эта статья содержит инструкции по миграции с помощью портала Azure, которые основаны на [инструкциях по репликации физического компьютера в Azure](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="04e87-107">This article describes the steps for migration in the Azure portal, and are based on the instructions for [replicating a physical machine to Azure](site-recovery-vmware-to-azure.md).</span></span>

<span data-ttu-id="04e87-108">Все комментарии или вопросы можно добавить в конце этой статьи или на [форуме по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="04e87-108">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="04e87-109">Поддерживаемые операционные системы</span><span class="sxs-lookup"><span data-stu-id="04e87-109">Supported operating systems</span></span>

<span data-ttu-id="04e87-110">Site Recovery можно использовать для переноса экземпляров EC2, работающих на любой из следующих операционных систем.</span><span class="sxs-lookup"><span data-stu-id="04e87-110">Site Recovery can be used to migrate EC2 instances running any of the following operating systems:</span></span>

- <span data-ttu-id="04e87-111">Windows (только 64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="04e87-111">Windows(64 bit only)</span></span>
    - <span data-ttu-id="04e87-112">Windows Server 2008 R2 с пакетом обновления 1 или более поздняя версия (Поддерживаются только драйверы Citrix PV и драйверы AWS PV.</span><span class="sxs-lookup"><span data-stu-id="04e87-112">Windows Server 2008 R2 SP1+ (Citrix PV drivers or AWS PV drivers only.</span></span> <span data-ttu-id="04e87-113">**Экземпляры с драйверами RedHat PV не поддерживаются**.) Windows Server 2012, Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="04e87-113">**Instances running RedHat PV drivers are not supported**) Windows Server 2012 Windows Server 2012 R2</span></span>
- <span data-ttu-id="04e87-114">Linux (только 64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="04e87-114">Linux (64 bit only)</span></span>
    - <span data-ttu-id="04e87-115">Red Hat Enterprise Linux 6.7 (только виртуализированные экземпляры HVM).</span><span class="sxs-lookup"><span data-stu-id="04e87-115">Red Hat Enterprise Linux 6.7 (HVM virtualized instances only)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04e87-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="04e87-116">Prerequisites</span></span>

<span data-ttu-id="04e87-117">Вот что нужно для этого развертывания:</span><span class="sxs-lookup"><span data-stu-id="04e87-117">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="04e87-118">**Сервер конфигурации.** Виртуальная машина Amazon EC2 под управлением Windows Server 2012 EC2, развернутая в качестве сервера конфигурации.</span><span class="sxs-lookup"><span data-stu-id="04e87-118">**Configuration server**: An Amazon EC2 VM running Windows Server 2012 R2 is deployed as the configuration server.</span></span> <span data-ttu-id="04e87-119">По умолчанию при развертывании сервера конфигурации устанавливаются другие компоненты Azure Site Recovery (сервер обработки и главный целевой сервер).</span><span class="sxs-lookup"><span data-stu-id="04e87-119">By default, the other Azure Site Recovery components (process server and master target server) are installed when you deploy the configuration server.</span></span> <span data-ttu-id="04e87-120">Эта статья содержит инструкции по миграции с помощью портала Azure, которые основаны на сведениях, приведенных в [этом разделе](site-recovery-components.md).</span><span class="sxs-lookup"><span data-stu-id="04e87-120">This article describes the steps for migration in the Azure portal, and are based on the instructions for  [Learn more](site-recovery-components.md)</span></span>

* <span data-ttu-id="04e87-121">**Экземпляры EC2.** Экземпляры виртуальных машин Amazon EC2, которые требуется перенести.</span><span class="sxs-lookup"><span data-stu-id="04e87-121">**EC2 instances**: The Amazon EC2 virtual machines instances that you want to migrate.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="04e87-122">Шаги по развертыванию</span><span class="sxs-lookup"><span data-stu-id="04e87-122">Deployment steps</span></span>

1. <span data-ttu-id="04e87-123">Создайте хранилище служб восстановления,</span><span class="sxs-lookup"><span data-stu-id="04e87-123">Create a Recovery Services vault.</span></span>
2. <span data-ttu-id="04e87-124">В группе безопасности для экземпляров EC2 должны быть настроены правила, чтобы обеспечить обмен данными между экземпляром EC2, который требуется перенести, и экземпляром, на котором планируется развернуть сервер конфигурации.</span><span class="sxs-lookup"><span data-stu-id="04e87-124">The Security Group of your EC2 instances should have rules configured to allow communication between the EC2 instance that you want to migrate, and the instance on which you plan to deploy the Configuration Server.</span></span>

3. <span data-ttu-id="04e87-125">Разверните сервер конфигурации ASR на том же виртуальном частном облаке Amazon, что и экземпляры EC2.</span><span class="sxs-lookup"><span data-stu-id="04e87-125">On the same Amazon Virtual Private Cloud as your EC2 instances, deploy an ASR configuration server.</span></span> <span data-ttu-id="04e87-126">Требования для развертывания сервера конфигурации см. в предварительных требованиях для развертывания виртуальной машины VMware или физического компьютера в Azure.</span><span class="sxs-lookup"><span data-stu-id="04e87-126">Refer the VMware / Physical to Azure prerequisites for configuration server deployment requirements.</span></span>

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  <span data-ttu-id="04e87-128">После того как сервер конфигурации будет развернут в AWS и зарегистрирован в хранилище служб восстановления, сервер конфигурации и сервер обработки отобразятся в инфраструктуре Site Recovery, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="04e87-128">Once your configuration server is deployed in AWS and registered with your Recovery Services vault, you should see the configuration server and process server under Site Recovery infrastructure as shown below:</span></span>

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. <span data-ttu-id="04e87-130">После развертывания сервера конфигурации (для его отображения может потребоваться до 15 минут) убедитесь, что он может обмениваться данными с виртуальными машинами, которые требуется перенести.</span><span class="sxs-lookup"><span data-stu-id="04e87-130">After you've deployed the configuration server (it might take up to 15 minustes for it to appear), validate that it can communicate with the VMs that you want to migrate.</span></span>

6. <span data-ttu-id="04e87-131">[Настройте параметры репликации](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="04e87-131">[Set up replication settings](site-recovery-setup-replication-settings-vmware.md).</span></span>

7. <span data-ttu-id="04e87-132">Включите репликацию для виртуальных машин, которые требуется перенести.</span><span class="sxs-lookup"><span data-stu-id="04e87-132">Enable replication: Enable replication for the VMs you want to migrate.</span></span> <span data-ttu-id="04e87-133">Вы можете просмотреть экземпляры EC2, используя их частные IP-адреса, сведения о которых доступны в консоли EC2.</span><span class="sxs-lookup"><span data-stu-id="04e87-133">You can discover the EC2 instances using the private IP addresses, which you can get from the EC2 console.</span></span>

    ![Выбор виртуальной машины](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. <span data-ttu-id="04e87-135">Как только экземпляры EC2 будут защищены, а репликация в Azure завершена, [запустите тестовую отработку отказа](site-recovery-test-failover-to-azure.md) для проверки производительности приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="04e87-135">Once the EC2 instances have been protected and the replication to Azure is complete, [run a Test Failover](site-recovery-test-failover-to-azure.md) to validate your application's performance in Azure.</span></span>

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. <span data-ttu-id="04e87-137">Запустите отработку отказа из AWS в Azure для каждой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="04e87-137">Run a Failover from AWS to Azure for each VM.</span></span> <span data-ttu-id="04e87-138">При необходимости вы можете создать план восстановления и запустить отработку отказа, чтобы перенести несколько виртуальных машин из AWS в Azure.</span><span class="sxs-lookup"><span data-stu-id="04e87-138">Optionally, you can create a recovery plan and run a Failover, to migrate multiple virtual machines from AWS to Azure.</span></span> <span data-ttu-id="04e87-139">[Узнайте подробнее](site-recovery-create-recovery-plans.md) о планах восстановления.</span><span class="sxs-lookup"><span data-stu-id="04e87-139">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

10. <span data-ttu-id="04e87-140">Чтобы перенести машины, не нужно выполнять отработку отказа.</span><span class="sxs-lookup"><span data-stu-id="04e87-140">For migration, you don't need to commit a failover.</span></span> <span data-ttu-id="04e87-141">Для каждой машины, которую нужно перенести, выберите параметр "Завершение миграции".</span><span class="sxs-lookup"><span data-stu-id="04e87-141">Instead, you select the Complete Migration option for each machine you want to migrate.</span></span> <span data-ttu-id="04e87-142">При завершении миграции выполняется перенос виртуальной машины, удаляется репликация и прекращается выставление счетов за использование Site Recovery для этой машины.</span><span class="sxs-lookup"><span data-stu-id="04e87-142">The Complete Migration action finishes up the migration process, removes replication for the machine, and stops Site Recovery billing for the machine.</span></span>

    ![Миграция](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a><span data-ttu-id="04e87-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="04e87-144">Next steps</span></span>

- <span data-ttu-id="04e87-145">[Подготовьте перенесенные виртуальные машины для включения репликации](site-recovery-azure-to-azure-after-migration.md) в другой регион в целях аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="04e87-145">[Prepare migrated machines to enable replication](site-recovery-azure-to-azure-after-migration.md) to another region for disaster recovery needs.</span></span>
- <span data-ttu-id="04e87-146">Включите защиту рабочих нагрузок, [выполнив репликацию виртуальных машин Azure.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="04e87-146">Start protecting your workloads by [replicating Azure virtual machines.](site-recovery-azure-to-azure.md)</span></span>
