---
title: "Подготовка узлов Hyper-V (без System Center VMM) для репликации в Azure | Документация Майкрософт"
description: "В этой статье описывается подготовка узлов Hyper-V для репликации в Azure с помощью Azure Site Recovery."
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
ms.openlocfilehash: f9bcaa8e55be6e8fddaf88ebc3f18f5dbb2811e4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-to-azure"></a><span data-ttu-id="fd5bb-103">Шаг 6. Подготовка узлов Hyper-V для репликации в Azure</span><span class="sxs-lookup"><span data-stu-id="fd5bb-103">Step 6: Prepare Hyper-V hosts for replication to Azure</span></span>

<span data-ttu-id="fd5bb-104">Используйте инструкции в этой статье, чтобы подготовить локальные узлы Hyper-V к взаимодействию со службой Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="fd5bb-104">Use the instructions in this article to prepare on-premises Hyper-V hosts to interact with Azure Site Recovery.</span></span>

<span data-ttu-id="fd5bb-105">Комментарии или вопросы технического характера можно добавить в конце этой статьи или на [форуме по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="fd5bb-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-hosts"></a><span data-ttu-id="fd5bb-106">Подготовка узлов</span><span class="sxs-lookup"><span data-stu-id="fd5bb-106">Prepare hosts</span></span>

- <span data-ttu-id="fd5bb-107">Убедитесь, что узлы Hyper-V соответствуют [предварительным требованиям](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span><span class="sxs-lookup"><span data-stu-id="fd5bb-107">Make sure that the Hyper-V hosts meet the [prerequisites](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span></span>
- <span data-ttu-id="fd5bb-108">Убедитесь, что узлы имеют доступ к нужным URL-адресам.</span><span class="sxs-lookup"><span data-stu-id="fd5bb-108">Make sure that the hosts can access the required URLs:</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="fd5bb-109">При использовании правил брандмауэра на основе IP-адресов убедитесь, что эти правила разрешают обмен данными с Azure.</span><span class="sxs-lookup"><span data-stu-id="fd5bb-109">If you have IP address-based firewall rules, ensure they allow communication to Azure.</span></span>
- <span data-ttu-id="fd5bb-110">Разрешите доступ для [диапазонов IP-адресов центра обработки данных Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) и использование порта HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="fd5bb-110">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and the HTTPS (443) port.</span></span>
- <span data-ttu-id="fd5bb-111">Необходимо разрешить доступ для диапазонов IP-адресов региона Azure, в котором располагается ваша подписка, и региона "Западная часть США" (используется для контроля доступа и управления удостоверениями).</span><span class="sxs-lookup"><span data-stu-id="fd5bb-111">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="fd5bb-112">При развертывании Site Recovery вы добавляете узлы Hyper-V, содержащие виртуальные машины, которые необходимо реплицировать на сайт Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="fd5bb-112">During Site Recovery deployment, you add Hyper-V hosts that contain VMs you want to replicate to a Hyper-V site.</span></span> <span data-ttu-id="fd5bb-113">Поставщик Site Recovery и агент служб восстановления устанавливаются на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="fd5bb-113">The Site Recovery Provider, and Recovery Services agent are installed on each host.</span></span> <span data-ttu-id="fd5bb-114">Сайт Hyper-V регистрируется в хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="fd5bb-114">The Hyper-V site is registered in the Recovery Services vault.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd5bb-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fd5bb-115">Next steps</span></span>

<span data-ttu-id="fd5bb-116">Перейдите к статье [Шаг 7. Настройка хранилища для репликации Hyper-V](hyper-v-site-walkthrough-create-vault.md).</span><span class="sxs-lookup"><span data-stu-id="fd5bb-116">Go to [Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

