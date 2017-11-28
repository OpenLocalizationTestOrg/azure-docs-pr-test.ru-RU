---
title: "Подготовка целевого (физический tooAzure) | Документы Microsoft"
description: "В этой статье описывается как tooprepare toostart вашей среды Azure, репликация физических серверов под управлением Windows или Linux tooAzure."
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
ms.openlocfilehash: 126fb86133e1a00f5669410943565c4cd78e4369
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-target-vmware-tooazure"></a><span data-ttu-id="a689a-103">Подготовка целевого (VMware tooAzure)</span><span class="sxs-lookup"><span data-stu-id="a689a-103">Prepare target (VMware tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a689a-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="a689a-104">VMware tooAzure</span></span>](./site-recovery-prepare-target-vmware-to-azure.md)
> * [<span data-ttu-id="a689a-105">Физический tooAzure</span><span class="sxs-lookup"><span data-stu-id="a689a-105">Physical tooAzure</span></span>](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="a689a-106">В этой статье описывается как tooprepare toostart вашей среды Azure, репликация физических серверов (x 64) под управлением Windows или Linux в Azure.</span><span class="sxs-lookup"><span data-stu-id="a689a-106">This article describes how tooprepare your Azure environment toostart replicating physical servers (x64) running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a689a-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a689a-107">Prerequisites</span></span>

<span data-ttu-id="a689a-108">Hello предполагается hello следующее:</span><span class="sxs-lookup"><span data-stu-id="a689a-108">hello article assumes hello following:</span></span>
- <span data-ttu-id="a689a-109">Вы создали tooprotect хранилище служб восстановления физических серверов.</span><span class="sxs-lookup"><span data-stu-id="a689a-109">You have created a Recovery Services Vault tooprotect your physical servers.</span></span> <span data-ttu-id="a689a-110">Можно создать хранилище служб восстановления из hello [портал Azure](http://portal.azure.com "портал Azure").</span><span class="sxs-lookup"><span data-stu-id="a689a-110">You can create a Recovery Services Vault from hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="a689a-111">У вас есть [установки в локальной среде](./site-recovery-set-up-physical-to-azure.md) tooAzure tooreplicate физических серверов.</span><span class="sxs-lookup"><span data-stu-id="a689a-111">You have [setup your on-premises environment](./site-recovery-set-up-physical-to-azure.md) tooreplicate physical servers tooAzure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="a689a-112">Подготовка цели</span><span class="sxs-lookup"><span data-stu-id="a689a-112">Prepare target</span></span>

<span data-ttu-id="a689a-113">После завершения hello **цель защиты 1:Select шаг** и **шаг 2: Подготовка источника**, вы попадаете слишком**Step 3: целевой**</span><span class="sxs-lookup"><span data-stu-id="a689a-113">After completing hello **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken too**Step 3: Target**</span></span>

![Подготовка цели](./media/site-recovery-prepare-target-physical-to-azure/prepare-target-physical-to-azure.png)

1. <span data-ttu-id="a689a-115">**Подписки:** из hello раскрывающееся меню, выберите hello подписку, которую нужно tooreplicate физических серверов.</span><span class="sxs-lookup"><span data-stu-id="a689a-115">**Subscription:** From hello drop down menu, select hello Subscription that you want tooreplicate your physical servers to.</span></span>
2. <span data-ttu-id="a689a-116">**Модель развертывания:** hello выберите модель развертывания (классический или диспетчер ресурсов)</span><span class="sxs-lookup"><span data-stu-id="a689a-116">**Deployment Model:** Select hello deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="a689a-117">На основании выбранной модели развертывания hello, проверка выполняется tooensure, у вас есть по крайней мере один совместимую учетную запись хранения и виртуальная сеть в tooreplicate подписки целевой hello и отработки отказа физических серверов.</span><span class="sxs-lookup"><span data-stu-id="a689a-117">Based on hello chosen deployment model, a validation is run tooensure that you have at least one compatible storage account and virtual network in hello target subscription tooreplicate and failover your physical servers to.</span></span>

<span data-ttu-id="a689a-118">По завершении проверки приветствия нажмите кнопку ОК toogo toohello следующий шаг.</span><span class="sxs-lookup"><span data-stu-id="a689a-118">Once hello validations complete successfully, click OK toogo toohello next step.</span></span>

<span data-ttu-id="a689a-119">Если у вас нет совместимых учетной записи диспетчера ресурсов хранилища или виртуальной сети или хотите tooadd дополнительные, это можно сделать, щелкнув hello **+ учетная запись хранения** или **+ сети** кнопками над hello hello колонки.</span><span class="sxs-lookup"><span data-stu-id="a689a-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like tooadd more, you can do so by clicking hello **+ Storage Account** or **+ Network** buttons on hello top of hello blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a689a-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a689a-120">Next steps</span></span>
<span data-ttu-id="a689a-121">[Настройка параметров репликации](./site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="a689a-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>
