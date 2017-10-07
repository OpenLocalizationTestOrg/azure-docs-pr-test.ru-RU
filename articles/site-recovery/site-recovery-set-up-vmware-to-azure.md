---
title: "Настройка среды источника hello (VMware tooAzure) | Документы Microsoft"
description: "В этой статье описывается, как tooset копирование вашей локальной среды toostart, репликация VMware виртуальной машины tooAzure."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: cbeeffc1061b11223e12ff3e237fa7e55b999aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-vmware-tooazure"></a><span data-ttu-id="03b38-103">Настройка среды источника hello (VMware tooAzure)</span><span class="sxs-lookup"><span data-stu-id="03b38-103">Set up hello source environment (VMware tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="03b38-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="03b38-104">VMware tooAzure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="03b38-105">Физический tooAzure</span><span class="sxs-lookup"><span data-stu-id="03b38-105">Physical tooAzure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="03b38-106">В этой статье описывается, как tooset копирование toostart вашей локальной среды, репликация виртуальных машин выполняется на VMware tooAzure.</span><span class="sxs-lookup"><span data-stu-id="03b38-106">This article describes how tooset up your on-premises environment toostart replicating virtual machines running on VMware tooAzure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03b38-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="03b38-107">Prerequisites</span></span>

<span data-ttu-id="03b38-108">Hello предполагается, что вы уже создали:</span><span class="sxs-lookup"><span data-stu-id="03b38-108">hello article assumes that you have already created:</span></span>
- <span data-ttu-id="03b38-109">Хранилище служб восстановления в hello [портал Azure](http://portal.azure.com "портал Azure").</span><span class="sxs-lookup"><span data-stu-id="03b38-109">A Recovery Services Vault in hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="03b38-110">Специальная учетная запись на сервере VMware vCenter, которую можно использовать для [автоматического обнаружения](./site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="03b38-110">A dedicated account in your VMware vCenter that can be used for [automatic discovery](./site-recovery-vmware-to-azure.md).</span></span>
- <span data-ttu-id="03b38-111">Виртуальная машина сервера, на котором tooinstall hello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="03b38-111">A virtual machine on which tooinstall hello configuration server.</span></span>

## <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="03b38-112">Минимальные требования к серверу конфигурации</span><span class="sxs-lookup"><span data-stu-id="03b38-112">Configuration server minimum requirements</span></span>
<span data-ttu-id="03b38-113">программное обеспечение сервера Hello конфигурации должен быть развернут на высокодоступной виртуальной машины VMware.</span><span class="sxs-lookup"><span data-stu-id="03b38-113">hello configuration server software should be deployed on a highly available VMware virtual machine.</span></span> <span data-ttu-id="03b38-114">Привет, в следующей таблице перечислены hello минимумом оборудования, программного обеспечения и требования к сети для сервера конфигурации.</span><span class="sxs-lookup"><span data-stu-id="03b38-114">hello following table lists hello minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="03b38-115">На основе HTTPS прокси-серверы не поддерживаются сервером конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="03b38-115">HTTPS-based proxy servers are not supported by hello configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="03b38-116">Выбор целевых объектов для защиты</span><span class="sxs-lookup"><span data-stu-id="03b38-116">Choose your protection goals</span></span>

1. <span data-ttu-id="03b38-117">В hello портал Azure, перейдите toohello **службы восстановления** хранилище колонки и выберите вашего хранилища.</span><span class="sxs-lookup"><span data-stu-id="03b38-117">In hello Azure portal, go toohello **Recovery Services** vault blade and select your vault.</span></span>
2. <span data-ttu-id="03b38-118">Меню hello ресурсов хранилища hello go слишком**Приступая к работе** > **Site Recovery** > **шаг 1: Подготовка инфраструктуры**  >  **Цель защиты**.</span><span class="sxs-lookup"><span data-stu-id="03b38-118">On hello resource menu of hello vault, go too**Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Выбор цели](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. <span data-ttu-id="03b38-120">В **цель защиты**выберите **tooAzure**и выберите **Да, с VMware vSphere низкоуровневой оболочки**.</span><span class="sxs-lookup"><span data-stu-id="03b38-120">In **Protection goal**, select **tooAzure**, and choose **Yes, with VMware vSphere Hypervisor**.</span></span> <span data-ttu-id="03b38-121">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="03b38-121">Then click **OK**.</span></span>

    ![Выбор цели](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="03b38-123">Настройка среды источника hello</span><span class="sxs-lookup"><span data-stu-id="03b38-123">Set up hello source environment</span></span>
<span data-ttu-id="03b38-124">Настройка среды hello источника включает в себя два основных действия:</span><span class="sxs-lookup"><span data-stu-id="03b38-124">Setting up hello source environment involves two main activities:</span></span>

- <span data-ttu-id="03b38-125">Установка и регистрация сервера конфигурации в службе Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="03b38-125">Install and register a configuration server with Site Recovery.</span></span>
- <span data-ttu-id="03b38-126">Обнаружение локальных виртуальных машин, подключившись Site Recovery tooyour локальной VMware vCenter или vSphere EXSi узлов.</span><span class="sxs-lookup"><span data-stu-id="03b38-126">Discover your on-premises virtual machines by connecting Site Recovery tooyour on-premises VMware vCenter or vSphere EXSi hosts.</span></span>

### <a name="step-1-install-and-register-a-configuration-server"></a><span data-ttu-id="03b38-127">Этап 1. Установка и регистрация сервера конфигурации</span><span class="sxs-lookup"><span data-stu-id="03b38-127">Step 1: Install and register a configuration server</span></span>

1. <span data-ttu-id="03b38-128">Щелкните **Шаг 1. Подготовка инфраструктуры** > **Источник**.</span><span class="sxs-lookup"><span data-stu-id="03b38-128">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span> <span data-ttu-id="03b38-129">В **Подготовка источника**, если у вас нет сервера конфигурации, щелкните **+ сервер конфигурации** tooadd один.</span><span class="sxs-lookup"><span data-stu-id="03b38-129">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** tooadd one.</span></span>

    ![Настройка источника](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. <span data-ttu-id="03b38-131">На hello **добавить сервер** колонки, убедитесь, что **сервер конфигурации** отображается в **тип сервера**.</span><span class="sxs-lookup"><span data-stu-id="03b38-131">On hello **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="03b38-132">Загрузите файл установки hello установка единой Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="03b38-132">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="03b38-133">Загрузите ключ регистрации в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="03b38-133">Download hello vault registration key.</span></span> <span data-ttu-id="03b38-134">При запуске программы установки единой необходим ключ регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="03b38-134">You need hello registration key when you run Unified Setup.</span></span> <span data-ttu-id="03b38-135">Hello ключ действителен в течение пяти дней после его создания.</span><span class="sxs-lookup"><span data-stu-id="03b38-135">hello key is valid for five days after you generate it.</span></span>

    ![Настройка источника](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. <span data-ttu-id="03b38-137">На компьютере hello используется в качестве сервера конфигурации hello выполните **Установка Azure Site Recovery единой** tooinstall hello конфигурации сервера, сервера обработки hello и образец hello целевого сервера.</span><span class="sxs-lookup"><span data-stu-id="03b38-137">On hello machine you’re using as hello configuration server, run **Azure Site Recovery Unified Setup** tooinstall hello configuration server, hello process server, and hello master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="03b38-138">Выполнение единой установки Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="03b38-138">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="03b38-139">Регистрация сервера конфигурации не выполняется, если время hello на системные часы компьютера отличается от местного времени более пяти минут.</span><span class="sxs-lookup"><span data-stu-id="03b38-139">Configuration server registration fails if hello time on your computer's system clock differs from local time by more than five minutes.</span></span> <span data-ttu-id="03b38-140">Синхронизацию системных часов с [сервер времени](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) перед началом установки hello.</span><span class="sxs-lookup"><span data-stu-id="03b38-140">Synchronize your system clock with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting hello installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="03b38-141">Сервер конфигурации Hello могут устанавливаться через командную строку.</span><span class="sxs-lookup"><span data-stu-id="03b38-141">hello configuration server can be installed via command line.</span></span> <span data-ttu-id="03b38-142">Дополнительные сведения см. в разделе [Установка hello конфигурации сервера с помощью средства командной строки](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="03b38-142">For more information, see [Installing hello configuration server using Command-line tools](http://aka.ms/installconfigsrv).</span></span>

#### <a name="add-hello-vmware-account-for-automatic-discovery"></a><span data-ttu-id="03b38-143">Добавьте учетную запись VMware hello автоматического обнаружения</span><span class="sxs-lookup"><span data-stu-id="03b38-143">Add hello VMware account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a><span data-ttu-id="03b38-144">Этап 2. Добавление сервера vCenter</span><span class="sxs-lookup"><span data-stu-id="03b38-144">Step 2: Add a vCenter</span></span>
<span data-ttu-id="03b38-145">tooallow Azure Site Recovery toodiscover виртуальных машин, работающих в локальной среде, необходимо tooconnect VMware vCenter Server или узлы vSphere ESXi с Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="03b38-145">tooallow Azure Site Recovery toodiscover virtual machines running in your on-premises environment, you need tooconnect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span>

<span data-ttu-id="03b38-146">Выберите **+ vCenter** toostart подключение сервера VMware vCenter server или узла ESXi VMware vSphere.</span><span class="sxs-lookup"><span data-stu-id="03b38-146">Select **+vCenter** toostart connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a><span data-ttu-id="03b38-147">Распространенные проблемы</span><span class="sxs-lookup"><span data-stu-id="03b38-147">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="03b38-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="03b38-148">Next steps</span></span>
<span data-ttu-id="03b38-149">[Настройка целевой среды](./site-recovery-prepare-target-vmware-to-azure.md) в Azure.</span><span class="sxs-lookup"><span data-stu-id="03b38-149">[Set up your target environment](./site-recovery-prepare-target-vmware-to-azure.md) in Azure.</span></span>
