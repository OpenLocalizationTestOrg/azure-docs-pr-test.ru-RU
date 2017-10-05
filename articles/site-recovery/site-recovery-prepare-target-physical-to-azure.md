---
title: "Подготовка цели (репликация физических серверов в Azure) | Документация Майкрософт"
description: "В этой статье описывается, как подготовить среду Azure к запуску репликации физических серверов Windows или Linux в Azure."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 5/31/2017
ms.author: bsiva
ms.openlocfilehash: aa7a32ace8354f615a8b8cc137f6bdf48fbadf48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-target-vmware-to-azure"></a><span data-ttu-id="afb01-103">Подготовка цели (репликация виртуальных машин VMware в Azure)</span><span class="sxs-lookup"><span data-stu-id="afb01-103">Prepare target (VMware to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="afb01-104">VMware в VMware</span><span class="sxs-lookup"><span data-stu-id="afb01-104">VMware to Azure</span></span>](./site-recovery-prepare-target-vmware-to-azure.md)
> * [<span data-ttu-id="afb01-105">Из физического расположения в Azure</span><span class="sxs-lookup"><span data-stu-id="afb01-105">Physical to Azure</span></span>](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="afb01-106">В этой статье описывается, как подготовить среду Azure к запуску репликации 64-разрядных физических серверов Windows или Linux в Azure.</span><span class="sxs-lookup"><span data-stu-id="afb01-106">This article describes how to prepare your Azure environment to start replicating physical servers (x64) running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afb01-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="afb01-107">Prerequisites</span></span>

<span data-ttu-id="afb01-108">В данной статье предполагается, что выполнены следующие условия.</span><span class="sxs-lookup"><span data-stu-id="afb01-108">The article assumes the following:</span></span>
- <span data-ttu-id="afb01-109">Вы создали хранилище служб восстановления для защиты физических серверов.</span><span class="sxs-lookup"><span data-stu-id="afb01-109">You have created a Recovery Services Vault to protect your physical servers.</span></span> <span data-ttu-id="afb01-110">Хранилище служб восстановления можно создать на [портале Azure](http://portal.azure.com "Портал Azure").</span><span class="sxs-lookup"><span data-stu-id="afb01-110">You can create a Recovery Services Vault from the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="afb01-111">Вы [настроили локальную среду](./site-recovery-set-up-physical-to-azure.md) для репликации физических серверов в Azure.</span><span class="sxs-lookup"><span data-stu-id="afb01-111">You have [setup your on-premises environment](./site-recovery-set-up-physical-to-azure.md) to replicate physical servers to Azure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="afb01-112">Подготовка цели</span><span class="sxs-lookup"><span data-stu-id="afb01-112">Prepare target</span></span>

<span data-ttu-id="afb01-113">**Выбрав цель защиты** и **подготовив источник**, следует перейти к **настройке цели**.</span><span class="sxs-lookup"><span data-stu-id="afb01-113">After completing the **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken to **Step 3: Target**</span></span>

![Подготовка цели](./media/site-recovery-prepare-target-physical-to-azure/prepare-target-physical-to-azure.png)

1. <span data-ttu-id="afb01-115">**Подписка:** из раскрывающегося меню выберите подписку, в которую требуется реплицировать физические серверы.</span><span class="sxs-lookup"><span data-stu-id="afb01-115">**Subscription:** From the drop down menu, select the Subscription that you want to replicate your physical servers to.</span></span>
2. <span data-ttu-id="afb01-116">**Модель развертывания:** выберите модель развертывания (классическую модель или модель Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="afb01-116">**Deployment Model:** Select the deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="afb01-117">После выбора модели развертывания выполняется проверка наличия как минимум одной совместимой учетной записи хранения и виртуальной сети в целевой подписке, выбранной для репликации и отработки отказа физических серверов.</span><span class="sxs-lookup"><span data-stu-id="afb01-117">Based on the chosen deployment model, a validation is run to ensure that you have at least one compatible storage account and virtual network in the target subscription to replicate and failover your physical servers to.</span></span>

<span data-ttu-id="afb01-118">После успешного завершения проверки нажмите кнопку "OK", чтобы перейти к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="afb01-118">Once the validations complete successfully, click OK to go to the next step.</span></span>

<span data-ttu-id="afb01-119">Если совместимая учетная запись хранилища Resource Manager или виртуальная сеть отсутствует, либо вы хотите их добавить, вы можете это сделать, нажав кнопку **+ Storage Account** (+ Учетная запись хранения) или **+ Network** (+ Сеть) в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="afb01-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like to add more, you can do so by clicking the **+ Storage Account** or **+ Network** buttons on the top of the blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="afb01-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="afb01-120">Next steps</span></span>
<span data-ttu-id="afb01-121">[Настройка параметров репликации](./site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="afb01-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>
