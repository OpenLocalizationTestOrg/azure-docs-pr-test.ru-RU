---
title: "Настройка среды источника hello (tooAzure физических серверов) | Документы Microsoft"
description: "В этой статье описывается как tooset копирование toostart вашей локальной среде, репликация физических серверов под управлением Windows или Linux в Azure."
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
ms.openlocfilehash: d4702265bf36910015685d2bba99d6e577531bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-physical-server-tooazure"></a><span data-ttu-id="5196a-103">Настройка среды источника hello (физический сервер tooAzure)</span><span class="sxs-lookup"><span data-stu-id="5196a-103">Set up hello source environment (physical server tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5196a-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="5196a-104">VMware tooAzure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="5196a-105">Физический tooAzure</span><span class="sxs-lookup"><span data-stu-id="5196a-105">Physical tooAzure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="5196a-106">В этой статье описывается как tooset копирование toostart вашей локальной среде, репликация физических серверов под управлением Windows или Linux в Azure.</span><span class="sxs-lookup"><span data-stu-id="5196a-106">This article describes how tooset up your on-premises environment toostart replicating physical servers running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5196a-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5196a-107">Prerequisites</span></span>

<span data-ttu-id="5196a-108">Hello статьи предполагается, что уже:</span><span class="sxs-lookup"><span data-stu-id="5196a-108">hello article assumes that you already have:</span></span>
1. <span data-ttu-id="5196a-109">Хранилище служб восстановления в hello [портал Azure](http://portal.azure.com "портал Azure").</span><span class="sxs-lookup"><span data-stu-id="5196a-109">A Recovery Services vault in hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
3. <span data-ttu-id="5196a-110">Физический компьютер сервера, на котором tooinstall hello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5196a-110">A physical computer on which tooinstall hello configuration server.</span></span>

### <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="5196a-111">Минимальные требования к серверу конфигурации</span><span class="sxs-lookup"><span data-stu-id="5196a-111">Configuration server minimum requirements</span></span>
<span data-ttu-id="5196a-112">Привет, в следующей таблице перечислены hello минимумом оборудования, программного обеспечения и требования к сети для сервера конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5196a-112">hello following table lists hello minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="5196a-113">На основе HTTPS прокси-серверы не поддерживаются сервером конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="5196a-113">HTTPS-based proxy servers are not supported by hello configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="5196a-114">Выбор целевых объектов для защиты</span><span class="sxs-lookup"><span data-stu-id="5196a-114">Choose your protection goals</span></span>

1. <span data-ttu-id="5196a-115">В hello портал Azure, перейдите toohello **службы восстановления** хранилищ колонки и выберите вашего хранилища.</span><span class="sxs-lookup"><span data-stu-id="5196a-115">In hello Azure portal, go toohello **Recovery Services** vaults blade and select your vault.</span></span>
2. <span data-ttu-id="5196a-116">В hello **ресурсов** хранилища hello, выберите пункт **Приступая к работе** > **Site Recovery** > **шаг 1: Подготовка Инфраструктура** > **цель защиты**.</span><span class="sxs-lookup"><span data-stu-id="5196a-116">In hello **Resource** menu of hello vault, click **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Выбор цели](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. <span data-ttu-id="5196a-118">В **цель защиты**выберите **tooAzure** и **не виртуализированных, другие**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5196a-118">In **Protection goal**, select **tooAzure** and **Not virtualized/Other**, and then click **OK**.</span></span>

    ![Выбор цели](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="5196a-120">Настройка среды источника hello</span><span class="sxs-lookup"><span data-stu-id="5196a-120">Set up hello source environment</span></span>

1. <span data-ttu-id="5196a-121">В **Подготовка источника**, если у вас нет сервера конфигурации, щелкните **+ сервер конфигурации** tooadd один.</span><span class="sxs-lookup"><span data-stu-id="5196a-121">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** tooadd one.</span></span>

  ![Настройка источника](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. <span data-ttu-id="5196a-123">В hello **добавить сервер** колонки, убедитесь, что **сервер конфигурации** отображается в **тип сервера**.</span><span class="sxs-lookup"><span data-stu-id="5196a-123">In hello **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="5196a-124">Загрузите файл установки hello установка единой Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="5196a-124">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="5196a-125">Загрузите ключ регистрации в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="5196a-125">Download hello vault registration key.</span></span> <span data-ttu-id="5196a-126">При запуске программы установки единой необходим ключ регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="5196a-126">You need hello registration key when you run Unified Setup.</span></span> <span data-ttu-id="5196a-127">Hello ключ действителен в течение пяти дней после его создания.</span><span class="sxs-lookup"><span data-stu-id="5196a-127">hello key is valid for five days after you generate it.</span></span>

    ![Настройка источника](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. <span data-ttu-id="5196a-129">На компьютере hello используется в качестве сервера конфигурации hello выполните **Установка Azure Site Recovery единой** tooinstall hello конфигурации сервера, сервера обработки hello и образец hello целевого сервера.</span><span class="sxs-lookup"><span data-stu-id="5196a-129">On hello machine you’re using as hello configuration server, run **Azure Site Recovery Unified Setup** tooinstall hello configuration server, hello process server, and hello master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="5196a-130">Выполнение единой установки Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="5196a-130">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="5196a-131">Регистрация сервера конфигурации не выполняется, если время hello на системные часы компьютера — более пяти минут от местного времени.</span><span class="sxs-lookup"><span data-stu-id="5196a-131">Configuration server registration fails if hello time on your computer's system clock is more than five minutes off of local time.</span></span> <span data-ttu-id="5196a-132">Синхронизацию системных часов с [сервер времени](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) перед началом установки hello.</span><span class="sxs-lookup"><span data-stu-id="5196a-132">Synchronize your system clock with a [time server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting hello installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="5196a-133">Сервер конфигурации Hello могут устанавливаться через командную строку.</span><span class="sxs-lookup"><span data-stu-id="5196a-133">hello configuration server can be installed via a command line.</span></span> <span data-ttu-id="5196a-134">Изучите дополнительные сведения об [установке сервера конфигурации с помощью программ командной строки](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="5196a-134">For more information, see [Installing configuration server using command-line tools](http://aka.ms/installconfigsrv).</span></span>


## <a name="common-issues"></a><span data-ttu-id="5196a-135">Распространенные проблемы</span><span class="sxs-lookup"><span data-stu-id="5196a-135">Common issues</span></span>

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="5196a-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5196a-136">Next steps</span></span>

<span data-ttu-id="5196a-137">Следующий этап заключается в [настройке целевой среды](./site-recovery-prepare-target-physical-to-azure.md) в Azure.</span><span class="sxs-lookup"><span data-stu-id="5196a-137">Next step involves [setting up your target environment](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span></span>
