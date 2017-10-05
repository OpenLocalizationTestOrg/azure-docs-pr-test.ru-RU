---
title: "Подготовка System Center VMM для репликации Hyper-V в Azure | Документация Майкрософт"
description: "Здесь описывается, как подготовить сервер System Center VMM к репликации Hyper-V в Azure с помощью Azure Site Recovery."
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
ms.openlocfilehash: ec118ed837dbf140083b3ae1e4ecd41c81562018
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-to-azure"></a><span data-ttu-id="32f2d-103">Шаг 6. Подготовка серверов VMM и узлов Hyper-V к репликации Hyper-V в Azure</span><span class="sxs-lookup"><span data-stu-id="32f2d-103">Step 6: Prepare VMM servers and Hyper-V hosts for Hyper-V replication to Azure</span></span>

<span data-ttu-id="32f2d-104">После настройки [компонентов Azure](vmm-to-azure-walkthrough-prepare-azure.md) для развертывания выполните инструкции в этой статье, чтоб подготовить локальные серверы VMM и узлы Hyper-V для взаимодействия с Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="32f2d-104">After setting up [Azure components](vmm-to-azure-walkthrough-prepare-azure.md) for the deployment, use the instructions in this article to prepare on-premises VMM servers and Hyper-V hosts to interact with Azure Site Recovery.</span></span>

<span data-ttu-id="32f2d-105">Комментарии или вопросы технического характера можно добавить в конце этой статьи или на [форуме по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="32f2d-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-vmm-servers"></a><span data-ttu-id="32f2d-106">Подготовка серверов VMM</span><span class="sxs-lookup"><span data-stu-id="32f2d-106">Prepare VMM servers</span></span>

- <span data-ttu-id="32f2d-107">Необходим по крайней мере один сервер VMM, соответствующий требованиям к поддержке для репликации Site Recovery (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span><span class="sxs-lookup"><span data-stu-id="32f2d-107">You need at least one VMM server that meet the support requirements for Site Recovery replication (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span></span>
- <span data-ttu-id="32f2d-108">Убедитесь, что сервер VMM подготовлен к [сетевому сопоставлению](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span><span class="sxs-lookup"><span data-stu-id="32f2d-108">Make sure you've prepared the VMM server for [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="32f2d-109">Убедитесь, что сервер VMM может получить доступ к этим URL-адресам.</span><span class="sxs-lookup"><span data-stu-id="32f2d-109">Make sure that the VMM server can access these URLs</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="32f2d-110">При использовании правил брандмауэра на основе IP-адресов убедитесь, что эти правила разрешают обмен данными с Azure.</span><span class="sxs-lookup"><span data-stu-id="32f2d-110">If you have IP address-based firewall rules, ensure they allow communication to Azure.</span></span>
- <span data-ttu-id="32f2d-111">Разрешите доступ для [диапазонов IP-адресов центра обработки данных Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) и использование порта HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="32f2d-111">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and the HTTPS (443) port.</span></span>
- <span data-ttu-id="32f2d-112">Необходимо разрешить доступ для диапазонов IP-адресов региона Azure, в котором располагается ваша подписка, и региона "Западная часть США" (используется для контроля доступа и управления удостоверениями).</span><span class="sxs-lookup"><span data-stu-id="32f2d-112">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="32f2d-113">Во время развертывания Site Recovery скачайте поставщик Site Recovery и установите его на каждом сервере VMM.</span><span class="sxs-lookup"><span data-stu-id="32f2d-113">During Site Recovery deployment, you download the Site Recovery Provider and install it on each VMM server.</span></span> <span data-ttu-id="32f2d-114">Сервер VMM регистрируется в хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="32f2d-114">The VMM server is registered in the Recovery Services vault.</span></span>




## <a name="next-steps"></a><span data-ttu-id="32f2d-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="32f2d-115">Next steps</span></span>

<span data-ttu-id="32f2d-116">Перейдите к статье [Шаг 7. Настройка хранилища для репликации Hyper-V](vmm-to-azure-walkthrough-create-vault.md).</span><span class="sxs-lookup"><span data-stu-id="32f2d-116">Go to [Step 7: Create a vault](vmm-to-azure-walkthrough-create-vault.md)</span></span>

