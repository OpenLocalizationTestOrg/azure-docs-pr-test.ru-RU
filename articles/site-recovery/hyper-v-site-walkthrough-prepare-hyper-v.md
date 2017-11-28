---
title: "размещает aaaPrepare Hyper-V (без System Center VMM) для репликации tooAzure | Документы Microsoft"
description: "Описывает способ размещения tooprepare Hyper-V для tooAzure репликации с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0f204e24-8d78-4076-95c5-8137d1be9c01
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 714b229d5efbd66a9844bd09e36ac3f69919a6bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-tooazure"></a><span data-ttu-id="518e3-103">Шаг 6: Подготовка узлов Hyper-V для репликации tooAzure</span><span class="sxs-lookup"><span data-stu-id="518e3-103">Step 6: Prepare Hyper-V hosts for replication tooAzure</span></span>

<span data-ttu-id="518e3-104">Используйте инструкции hello в этой статье tooprepare локальной toointeract узлов Hyper-V с помощью Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="518e3-104">Use hello instructions in this article tooprepare on-premises Hyper-V hosts toointeract with Azure Site Recovery.</span></span>

<span data-ttu-id="518e3-105">После считывания в этой статье, отправлять любые комментарии внизу hello или задавайте технические вопросы на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="518e3-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-hosts"></a><span data-ttu-id="518e3-106">Подготовка узлов</span><span class="sxs-lookup"><span data-stu-id="518e3-106">Prepare hosts</span></span>

- <span data-ttu-id="518e3-107">Убедитесь, что узлы Hyper-V hello соответствуют hello [необходимых компонентов](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span><span class="sxs-lookup"><span data-stu-id="518e3-107">Make sure that hello Hyper-V hosts meet hello [prerequisites](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span></span>
- <span data-ttu-id="518e3-108">Убедитесь, что доступность узлов hello hello требуется URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="518e3-108">Make sure that hello hosts can access hello required URLs:</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="518e3-109">Если правила брандмауэра на основе адресов IP, убедитесь, что они позволяют tooAzure связи.</span><span class="sxs-lookup"><span data-stu-id="518e3-109">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span>
- <span data-ttu-id="518e3-110">Разрешить hello [диапазоны IP-адресов центра обработки данных Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)и hello порта HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="518e3-110">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span>
- <span data-ttu-id="518e3-111">Разрешить диапазоны IP-адресов для hello регион Azure, подписки и Запад США (используется для контроля доступа и удостоверений).</span><span class="sxs-lookup"><span data-stu-id="518e3-111">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="518e3-112">Во время развертывания службы восстановления сайтов Добавление узлов Hyper-V, содержащие виртуальные машины, вы хотите узел tooreplicate tooa Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="518e3-112">During Site Recovery deployment, you add Hyper-V hosts that contain VMs you want tooreplicate tooa Hyper-V site.</span></span> <span data-ttu-id="518e3-113">Hello поставщика Site Recovery и агента служб восстановления устанавливаются на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="518e3-113">hello Site Recovery Provider, and Recovery Services agent are installed on each host.</span></span> <span data-ttu-id="518e3-114">узел Hyper-V Hello зарегистрирован в hello в хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="518e3-114">hello Hyper-V site is registered in hello Recovery Services vault.</span></span>

## <a name="next-steps"></a><span data-ttu-id="518e3-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="518e3-115">Next steps</span></span>

<span data-ttu-id="518e3-116">Go слишком[шаг 7: Создание хранилища](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="518e3-116">Go too[Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

