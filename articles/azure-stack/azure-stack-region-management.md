---
title: "Управление aaaRegion в стек Azure | Документы Microsoft"
description: "Общие сведения об управлении регион Azure стека."
services: azure-stack
documentationcenter: 
author: efemmano
manager: dsavage
editor: 
ms.assetid: e94775d5-d473-4c03-9f4e-ae2eada67c6c
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: efemmano
ms.openlocfilehash: c20fed831267aaf0447925ac261d7ee3f235c96c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="region-management-in-azure-stack"></a><span data-ttu-id="6ee97-103">Область управления в стек Azure</span><span class="sxs-lookup"><span data-stu-id="6ee97-103">Region management in Azure Stack</span></span>
<span data-ttu-id="6ee97-104">Стек Azure имеет hello понятие областей, которые являются логическими единицами, состоящей из hello аппаратные ресурсы, которые составляют инфраструктуры Azure стека hello.</span><span class="sxs-lookup"><span data-stu-id="6ee97-104">Azure Stack has hello concept of regions, which are logical entities comprised of hello hardware resources that make up hello Azure Stack infrastructure.</span></span> <span data-ttu-id="6ee97-105">В области управления можно найти все ресурсы, необходимые toosuccessfully работать жизненного цикла инфраструктуры Azure стека hello.</span><span class="sxs-lookup"><span data-stu-id="6ee97-105">Inside Region management, you can find all resources that are required toosuccessfully operate hello Azure Stack infrastructure lifecycle.</span></span>

<span data-ttu-id="6ee97-106">Hello Azure стека Development Kit — развертывание одного узла, а также равен одной области.</span><span class="sxs-lookup"><span data-stu-id="6ee97-106">hello Azure Stack Development Kit is a single-node deployment, and equals one region.</span></span> <span data-ttu-id="6ee97-107">Если установка выполняется другой экземпляр hello пакет средств разработки Azure стека на другом оборудовании, этот экземпляр является другой регион.</span><span class="sxs-lookup"><span data-stu-id="6ee97-107">If you set up another instance of hello Azure Stack Development Kit on separate hardware, this instance is a different region.</span></span>

## <a name="information-available-through-hello-region-management-tile"></a><span data-ttu-id="6ee97-108">Сведения, доступные через область управления плитки приветствия</span><span class="sxs-lookup"><span data-stu-id="6ee97-108">Information available through hello Region Management tile</span></span>
<span data-ttu-id="6ee97-109">Стек Azure имеет набор возможностей управления области, доступные в hello **область управления** плитки.</span><span class="sxs-lookup"><span data-stu-id="6ee97-109">Azure Stack has a set of region management capabilities available in hello **Region management** tile.</span></span> <span data-ttu-id="6ee97-110">Эта Плитка — администратор облака tooa доступны на панели мониторинга по умолчанию hello в портал администратора hello.</span><span class="sxs-lookup"><span data-stu-id="6ee97-110">This tile is available tooa cloud administrator on hello default dashboard in hello administrator portal.</span></span> <span data-ttu-id="6ee97-111">Посредством этой плитки можно отслеживать и обновлять ваш регион Azure стека и его компонентов, которые зависят от конкретного региона.</span><span class="sxs-lookup"><span data-stu-id="6ee97-111">Through this tile, you can monitor and update your Azure Stack region and its components, which are region-specific.</span></span>

 ![Hello области управления плитки](media/azure-stack-manage-region/image1.png)

 <span data-ttu-id="6ee97-113">Если щелкнуть область элемента управления области hello, вы можете использовать hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="6ee97-113">If you click a region in hello Region management tile, you can access hello following information:</span></span>

  ![Описание областей в колонке управления области hello](media/azure-stack-manage-region/image2.png)

1. <span data-ttu-id="6ee97-115">**Hello ресурсов меню**.</span><span class="sxs-lookup"><span data-stu-id="6ee97-115">**hello resource menu**.</span></span> <span data-ttu-id="6ee97-116">Здесь, доступ к определенной инфраструктуры управления областей и просматривать и управлять такими ресурсами клиента как учетные записи хранилища и виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="6ee97-116">Here, you can access specific infrastructure management areas, and view and manage tenant resources such as storage accounts and virtual networks.</span></span>

2. <span data-ttu-id="6ee97-117">**Предупреждения**.</span><span class="sxs-lookup"><span data-stu-id="6ee97-117">**Alerts**.</span></span> <span data-ttu-id="6ee97-118">Эта Плитка список предупреждений для всей системы и предоставляет подробные сведения о каждой из этих предупреждений.</span><span class="sxs-lookup"><span data-stu-id="6ee97-118">This tile lists system-wide alerts and provides details on each of those alerts.</span></span>

3. <span data-ttu-id="6ee97-119">**Обновления**.</span><span class="sxs-lookup"><span data-stu-id="6ee97-119">**Updates**.</span></span> <span data-ttu-id="6ee97-120">В этой плитки можно просматривать hello текущей версии вашей инфраструктуры Azure стека.</span><span class="sxs-lookup"><span data-stu-id="6ee97-120">In this tile, you can view hello current version of your Azure Stack infrastructure.</span></span>

4. <span data-ttu-id="6ee97-121">**Поставщики ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="6ee97-121">**Resource providers**.</span></span> <span data-ttu-id="6ee97-122">Поставщики ресурсов — hello месте toomanage hello клиента функциональные возможности, предлагаемые toorun необходимые компоненты hello Azure стека.</span><span class="sxs-lookup"><span data-stu-id="6ee97-122">Resource providers is hello place toomanage hello tenant functionality offered by hello components required toorun Azure Stack.</span></span> <span data-ttu-id="6ee97-123">Каждый поставщик ресурсов поставляется с административные функции.</span><span class="sxs-lookup"><span data-stu-id="6ee97-123">Each resource provider comes with an administrative experience.</span></span> <span data-ttu-id="6ee97-124">Эти возможности можно включить предупреждения для конкретного поставщика hello, метрики и другого поставщика ресурсов определенного toohello возможности управления.</span><span class="sxs-lookup"><span data-stu-id="6ee97-124">This experience can include alerts for hello specific provider, metrics, and other management capabilities specific toohello resource provider.</span></span>
 
5. <span data-ttu-id="6ee97-125">**Роли инфраструктуры**.</span><span class="sxs-lookup"><span data-stu-id="6ee97-125">**Infrastructure roles**.</span></span> <span data-ttu-id="6ee97-126">Роли инфраструктуры, toorun необходимые компоненты hello Azure стека.</span><span class="sxs-lookup"><span data-stu-id="6ee97-126">Infrastructure roles are hello components necessary toorun Azure Stack.</span></span> <span data-ttu-id="6ee97-127">Перечислены только роли hello инфраструктуры, которые сообщают предупреждения.</span><span class="sxs-lookup"><span data-stu-id="6ee97-127">Only hello infrastructure roles that report alerts are listed.</span></span> <span data-ttu-id="6ee97-128">Щелкнув роли, можно просмотреть оповещения hello, связанные с определенной ролью hello и hello экземпляров роли, где запущена эта роль.</span><span class="sxs-lookup"><span data-stu-id="6ee97-128">By clicking a role, you can view hello alerts associated with hello specific role and hello role instances where this role is running.</span></span> <span data-ttu-id="6ee97-129">Несмотря на то, что есть возможность toostart hello, перезапустить, или завершение работы экземпляра роли инфраструктуры, выполните **не** сделать это в среде разработки пакета.</span><span class="sxs-lookup"><span data-stu-id="6ee97-129">Although there is hello capability toostart, restart, or shut down an infrastructure role instance, do **not** do this in a development kit environment.</span></span> <span data-ttu-id="6ee97-130">Эти параметры предназначены только для среды с несколькими узлами, где имеется более одного экземпляра роли на каждую роль службы инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="6ee97-130">These options are designed only for a multi-node environment, where there is more than one role instance per infrastructure role.</span></span> <span data-ttu-id="6ee97-131">Перезапуск экземпляра роли (особенно AzS-Xrp01) в пакете средств разработки hello приведет нестабильность системы.</span><span class="sxs-lookup"><span data-stu-id="6ee97-131">Restarting a role instance (especially AzS-Xrp01) in hello development kit causes system instability.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ee97-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6ee97-132">Next steps</span></span>
[<span data-ttu-id="6ee97-133">Монитор работоспособности и предупреждений в стек Azure</span><span class="sxs-lookup"><span data-stu-id="6ee97-133">Monitor health and alerts in Azure Stack</span></span>](azure-stack-monitor-health.md)

[<span data-ttu-id="6ee97-134">Управление обновлениями в стек Azure</span><span class="sxs-lookup"><span data-stu-id="6ee97-134">Manage updates in Azure Stack</span></span>](azure-stack-updates.md)






