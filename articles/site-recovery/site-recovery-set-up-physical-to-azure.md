---
title: "Настройка исходной среды (репликация физических серверов в Azure) | Документация Майкрософт"
description: "В этой статье приведены сведения о настройке локальной среды для запуска репликации физических серверов под управлением Windows или Linux в Azure."
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
ms.openlocfilehash: 49b9d2e21dbcb612828a25f21ed4382327d6f64c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-the-source-environment-physical-server-to-azure"></a><span data-ttu-id="e55b3-103">Настройка исходной среды (репликация физических серверов в Azure)</span><span class="sxs-lookup"><span data-stu-id="e55b3-103">Set up the source environment (physical server to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e55b3-104">VMware в VMware</span><span class="sxs-lookup"><span data-stu-id="e55b3-104">VMware to Azure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="e55b3-105">Из физического расположения в Azure</span><span class="sxs-lookup"><span data-stu-id="e55b3-105">Physical to Azure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="e55b3-106">В этой статье приведены сведения о настройке локальной среды для запуска репликации физических серверов под управлением Windows или Linux в Azure.</span><span class="sxs-lookup"><span data-stu-id="e55b3-106">This article describes how to set up your on-premises environment to start replicating physical servers running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e55b3-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e55b3-107">Prerequisites</span></span>

<span data-ttu-id="e55b3-108">В этой статье предполагается, что у вас уже имеется:</span><span class="sxs-lookup"><span data-stu-id="e55b3-108">The article assumes that you already have:</span></span>
1. <span data-ttu-id="e55b3-109">Хранилище служб восстановления на [портале Azure](http://portal.azure.com "портал Azure").</span><span class="sxs-lookup"><span data-stu-id="e55b3-109">A Recovery Services vault in the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
3. <span data-ttu-id="e55b3-110">Физический компьютер для установки сервера конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e55b3-110">A physical computer on which to install the configuration server.</span></span>

### <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="e55b3-111">Минимальные требования к серверу конфигурации</span><span class="sxs-lookup"><span data-stu-id="e55b3-111">Configuration server minimum requirements</span></span>
<span data-ttu-id="e55b3-112">В следующей таблице перечислены минимальные требования к оборудованию, программному обеспечению и сети сервера конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e55b3-112">The following table lists the minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="e55b3-113">Сервер конфигурации не поддерживает прокси-серверы на основе HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e55b3-113">HTTPS-based proxy servers are not supported by the configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="e55b3-114">Выбор целевых объектов для защиты</span><span class="sxs-lookup"><span data-stu-id="e55b3-114">Choose your protection goals</span></span>

1. <span data-ttu-id="e55b3-115">На портале Azure откройте колонку **Хранилища служб восстановления** и выберите свое хранилище.</span><span class="sxs-lookup"><span data-stu-id="e55b3-115">In the Azure portal, go to the **Recovery Services** vaults blade and select your vault.</span></span>
2. <span data-ttu-id="e55b3-116">В меню **Ресурс** хранилища выберите **Приступая к работе** > **Site Recovery** > **Шаг 1. Подготовка инфраструктуры** > **Цель защиты**.</span><span class="sxs-lookup"><span data-stu-id="e55b3-116">In the **Resource** menu of the vault, click **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Выбор цели](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. <span data-ttu-id="e55b3-118">На странице **Цель защиты** выберите **To Azure** (В Azure), а затем — **Без виртуализации или иное**. Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e55b3-118">In **Protection goal**, select **To Azure** and **Not virtualized/Other**, and then click **OK**.</span></span>

    ![Выбор цели](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-the-source-environment"></a><span data-ttu-id="e55b3-120">Настройка исходной среды</span><span class="sxs-lookup"><span data-stu-id="e55b3-120">Set up the source environment</span></span>

1. <span data-ttu-id="e55b3-121">Если у вас нет сервера конфигурации, в окне **Prepare source** (Подготовка источника) щелкните **+Configuration server** (+Сервер конфигурации).</span><span class="sxs-lookup"><span data-stu-id="e55b3-121">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** to add one.</span></span>

  ![Настройка источника](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. <span data-ttu-id="e55b3-123">В колонке **Добавление сервера** в поле **Тип сервера** должно быть указано **Сервер конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="e55b3-123">In the **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="e55b3-124">Скачайте файл единой установки Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="e55b3-124">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="e55b3-125">Скачайте ключ регистрации хранилища.</span><span class="sxs-lookup"><span data-stu-id="e55b3-125">Download the vault registration key.</span></span> <span data-ttu-id="e55b3-126">При запуске программы единой установки вам потребуется ключ регистрации.</span><span class="sxs-lookup"><span data-stu-id="e55b3-126">You need the registration key when you run Unified Setup.</span></span> <span data-ttu-id="e55b3-127">Ключ действителен в течение пяти дней после создания.</span><span class="sxs-lookup"><span data-stu-id="e55b3-127">The key is valid for five days after you generate it.</span></span>

    ![Настройка источника](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. <span data-ttu-id="e55b3-129">На компьютере, используемом в качестве сервера конфигурации, запустите **программу единой установки Azure Site Recovery**, чтобы установить сервер конфигурации, сервер обработки и главный целевой сервер.</span><span class="sxs-lookup"><span data-stu-id="e55b3-129">On the machine you’re using as the configuration server, run **Azure Site Recovery Unified Setup** to install the configuration server, the process server, and the master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="e55b3-130">Выполнение единой установки Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="e55b3-130">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="e55b3-131">Если системное время на компьютере отличается от местного более чем на 5 минут, то регистрация сервера конфигурации завершится сбоем.</span><span class="sxs-lookup"><span data-stu-id="e55b3-131">Configuration server registration fails if the time on your computer's system clock is more than five minutes off of local time.</span></span> <span data-ttu-id="e55b3-132">Перед началом установки синхронизируйте системное время с [сервером времени](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="e55b3-132">Synchronize your system clock with a [time server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting the installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="e55b3-133">Сервер конфигурации можно установить с помощью командной строки.</span><span class="sxs-lookup"><span data-stu-id="e55b3-133">The configuration server can be installed via a command line.</span></span> <span data-ttu-id="e55b3-134">Изучите дополнительные сведения об [установке сервера конфигурации с помощью программ командной строки](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="e55b3-134">For more information, see [Installing configuration server using command-line tools](http://aka.ms/installconfigsrv).</span></span>


## <a name="common-issues"></a><span data-ttu-id="e55b3-135">Распространенные проблемы</span><span class="sxs-lookup"><span data-stu-id="e55b3-135">Common issues</span></span>

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="e55b3-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e55b3-136">Next steps</span></span>

<span data-ttu-id="e55b3-137">Следующий этап заключается в [настройке целевой среды](./site-recovery-prepare-target-physical-to-azure.md) в Azure.</span><span class="sxs-lookup"><span data-stu-id="e55b3-137">Next step involves [setting up your target environment](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span></span>
