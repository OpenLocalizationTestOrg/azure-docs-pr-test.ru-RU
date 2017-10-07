---
title: "новые возможности Azure стека aaaWhat | Документы Microsoft"
description: "Новые возможности в стек Azure"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 872b0651-0a92-4d28-b2e6-07d0a4a9a25a
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/13/2017
ms.author: helaw
ms.openlocfilehash: 32b4bd7deebb12a92e4abbdaacdbcebaa5125e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="whats-new-in-azure-stack"></a><span data-ttu-id="36da8-103">Новые возможности в стек Azure</span><span class="sxs-lookup"><span data-stu-id="36da8-103">What's new in Azure Stack</span></span>
<span data-ttu-id="36da8-104">Этот выпуск предоставляет новые функции для клиентов и администраторов.</span><span class="sxs-lookup"><span data-stu-id="36da8-104">This release provides new features for both tenants and administrators.</span></span>

## <a name="content-services-and-tools"></a><span data-ttu-id="36da8-105">Содержимое, служб и средств</span><span class="sxs-lookup"><span data-stu-id="36da8-105">Content, services, and tools</span></span>
* <span data-ttu-id="36da8-106">[Службы федерации Active Directory (AD FS)](azure-stack-key-features.md#identity) поддержка предоставляет параметры удостоверений для сценариев, где сетевое подключение ограниченное или периодические.</span><span class="sxs-lookup"><span data-stu-id="36da8-106">[Active Directory Federation Services (AD FS)](azure-stack-key-features.md#identity) support provides identity options for scenarios where network connectivity is limited or intermittent.</span></span>
* <span data-ttu-id="36da8-107">Можно использовать масштабирования tooprovide управляемые наборы масштабирования виртуальных машин Azure и в масштаб рабочих нагрузок на ВМ IaaS.</span><span class="sxs-lookup"><span data-stu-id="36da8-107">You can use Azure Virtual Machine Scale Sets tooprovide managed scale-out and scale-in of IaaS VM-based workloads.</span></span> 
* <span data-ttu-id="36da8-108">Размер ВМ серии D Azure можно используйте для повышения производительности и согласованности.</span><span class="sxs-lookup"><span data-stu-id="36da8-108">Use Azure D-Series VM sizes for increased performance and consistency.</span></span>
* <span data-ttu-id="36da8-109">Развертывание и создание шаблонов с дисками Temp, согласованные с Azure.</span><span class="sxs-lookup"><span data-stu-id="36da8-109">Deploy and create templates with Temp Disks that are consistent with Azure.</span></span>
* <span data-ttu-id="36da8-110">[Marketplace синдикации](azure-stack-download-azure-marketplace-item.md) позволяет toouse содержимое из hello Azure Marketplace и сделать доступными в стеке Azure.</span><span class="sxs-lookup"><span data-stu-id="36da8-110">[Marketplace Syndication](azure-stack-download-azure-marketplace-item.md) allows you toouse content from hello Azure Marketplace and make available in Azure Stack.</span></span>

## <a name="infrastructure-and-operations"></a><span data-ttu-id="36da8-111">Инфраструктуры и действий</span><span class="sxs-lookup"><span data-stu-id="36da8-111">Infrastructure and operations</span></span>
* <span data-ttu-id="36da8-112">Изолированные администратора и пользователя [порталы](azure-stack-manage-portals.md) и API-интерфейсы позволяют повысить безопасность.</span><span class="sxs-lookup"><span data-stu-id="36da8-112">Isolated administrator and user [portals](azure-stack-manage-portals.md) and APIs provide enhanced security.</span></span>
* <span data-ttu-id="36da8-113">Используйте функциональность Улучшенная инфраструктура управления, такие как улучшенные предупреждения.</span><span class="sxs-lookup"><span data-stu-id="36da8-113">Use enhanced infrastructure management functionality, such as improved alerting.</span></span>
* <span data-ttu-id="36da8-114">С помощью hello [соединителя пакет Windows Azure](azure-stack-manage-windows-azure-pack.md), можно просматривать и управлять виртуальными машинами IaaS, которые размещаются в Windows Azure Pack.</span><span class="sxs-lookup"><span data-stu-id="36da8-114">Using hello [Windows Azure Pack Connector](azure-stack-manage-windows-azure-pack.md), you can view and manage IaaS virtual machines that are hosted on Windows Azure Pack.</span></span> <span data-ttu-id="36da8-115">Для этой предварительной версии попробуйте этот сценарий только в тестовой среде (пакет Windows Azure и Azure стека).</span><span class="sxs-lookup"><span data-stu-id="36da8-115">For this preview release, try this scenario only in test environments (both Windows Azure Pack and Azure Stack).</span></span> <span data-ttu-id="36da8-116">Дополнительная настройка не требуется.</span><span class="sxs-lookup"><span data-stu-id="36da8-116">Additional configuration is required.</span></span>
* <span data-ttu-id="36da8-117">Azure теперь поддерживает стек [Мультитенантность](azure-stack-enable-multitenancy.md) для сценариев, где требуется tooprovide IaaS и PaaS служб toousers за пределами домена Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="36da8-117">Azure Stack now supports [multi-tenancy](azure-stack-enable-multitenancy.md) for scenarios where you need tooprovide IaaS and PaaS services toousers outside of your Azure Active Directory domain.</span></span>  <span data-ttu-id="36da8-118">Например может потребоваться tooprovide стека Azure службы tooa партнерской компании, с использованием их идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="36da8-118">For example, you may want tooprovide Azure Stack services tooa partner company using their identities.</span></span> <span data-ttu-id="36da8-119">Можно настроить стек Azure tootrust hello удостоверения другой организации и пользователи из этой toosign организации для подписки и использовать службы.</span><span class="sxs-lookup"><span data-stu-id="36da8-119">You can configure Azure Stack tootrust hello other organization's identities, and enable users from that organization toosign up for subscriptions and consume services.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="36da8-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="36da8-120">Next steps</span></span>
* [<span data-ttu-id="36da8-121">Описание архитектуры подтверждения Концепции стек Azure</span><span class="sxs-lookup"><span data-stu-id="36da8-121">Understand Azure Stack POC architecture</span></span>](azure-stack-architecture.md)      
* [<span data-ttu-id="36da8-122">Понять, предварительные условия для развертывания</span><span class="sxs-lookup"><span data-stu-id="36da8-122">Understand deployment prerequisites</span></span>](azure-stack-deploy.md)
* [<span data-ttu-id="36da8-123">Развертывание стек Azure</span><span class="sxs-lookup"><span data-stu-id="36da8-123">Deploy Azure Stack</span></span>](azure-stack-run-powershell-script.md)

