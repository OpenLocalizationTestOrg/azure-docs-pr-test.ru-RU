---
title: "aaaPrepare System Center VMM для tooAzure репликации Hyper-V | Документы Microsoft"
description: "Описывает способ tooprepare сервера System Center VMM для tooAzure репликации Hyper-V, с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: afcd81ae-d192-4013-a0af-3dac45b3c7e9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 773b06afaf7d3eea1fe64f050bf3970943cf466a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-tooazure"></a><span data-ttu-id="6a3fe-103">Шаг 6: Подготовка серверов VMM и узлы Hyper-V для tooAzure репликации Hyper-V</span><span class="sxs-lookup"><span data-stu-id="6a3fe-103">Step 6: Prepare VMM servers and Hyper-V hosts for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="6a3fe-104">После настройки [компонентов Azure](vmm-to-azure-walkthrough-prepare-azure.md) hello развертывания, используйте инструкции hello в этой статье tooprepare локальных серверов VMM и toointeract узлов Hyper-V с помощью Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="6a3fe-104">After setting up [Azure components](vmm-to-azure-walkthrough-prepare-azure.md) for hello deployment, use hello instructions in this article tooprepare on-premises VMM servers and Hyper-V hosts toointeract with Azure Site Recovery.</span></span>

<span data-ttu-id="6a3fe-105">После считывания в этой статье, отправлять любые комментарии внизу hello или задавайте технические вопросы на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="6a3fe-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-vmm-servers"></a><span data-ttu-id="6a3fe-106">Подготовка серверов VMM</span><span class="sxs-lookup"><span data-stu-id="6a3fe-106">Prepare VMM servers</span></span>

- <span data-ttu-id="6a3fe-107">Необходим по крайней мере один сервер VMM, который отвечает требованиям hello поддержки для восстановления сайта репликации (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span><span class="sxs-lookup"><span data-stu-id="6a3fe-107">You need at least one VMM server that meet hello support requirements for Site Recovery replication (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span></span>
- <span data-ttu-id="6a3fe-108">Убедитесь, что вы подготовили hello сервера VMM для [сетевое сопоставление](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span><span class="sxs-lookup"><span data-stu-id="6a3fe-108">Make sure you've prepared hello VMM server for [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="6a3fe-109">Убедитесь, что этот сервер VMM hello доступны такие URL-адреса</span><span class="sxs-lookup"><span data-stu-id="6a3fe-109">Make sure that hello VMM server can access these URLs</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="6a3fe-110">Если правила брандмауэра на основе адресов IP, убедитесь, что они позволяют tooAzure связи.</span><span class="sxs-lookup"><span data-stu-id="6a3fe-110">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span>
- <span data-ttu-id="6a3fe-111">Разрешить hello [диапазоны IP-адресов центра обработки данных Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)и hello порта HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="6a3fe-111">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span>
- <span data-ttu-id="6a3fe-112">Разрешить диапазоны IP-адресов для hello регион Azure, подписки и Запад США (используется для контроля доступа и удостоверений).</span><span class="sxs-lookup"><span data-stu-id="6a3fe-112">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="6a3fe-113">Во время развертывания службы восстановления сайтов Загрузите hello поставщика восстановления сайта и установить его на каждом сервере VMM.</span><span class="sxs-lookup"><span data-stu-id="6a3fe-113">During Site Recovery deployment, you download hello Site Recovery Provider and install it on each VMM server.</span></span> <span data-ttu-id="6a3fe-114">Hello сервер VMM зарегистрирован в hello в хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="6a3fe-114">hello VMM server is registered in hello Recovery Services vault.</span></span>




## <a name="next-steps"></a><span data-ttu-id="6a3fe-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6a3fe-115">Next steps</span></span>

<span data-ttu-id="6a3fe-116">Go слишком[шаг 7: Создание хранилища](vmm-to-azure-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="6a3fe-116">Go too[Step 7: Create a vault](vmm-to-azure-walkthrough-create-vault.md)</span></span>

