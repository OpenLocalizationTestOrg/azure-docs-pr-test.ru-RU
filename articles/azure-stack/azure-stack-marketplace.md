---
title: "aaaPublish элемент пользовательского marketplace в стек Azure (оператор облака) | Документы Microsoft"
description: "Оператор облака Узнайте, как toopublish пользовательские marketplace элемента в стек Azure."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 60871cbb-eed2-433c-a76d-d605c7aec06c
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: erikje
ms.openlocfilehash: e33e1c6574d43ada1c1c85bf77df7d0d191116aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hello-azure-stack-marketplace-overview"></a><span data-ttu-id="5ae6e-103">Обзор Azure Marketplace стека Hello</span><span class="sxs-lookup"><span data-stu-id="5ae6e-103">hello Azure Stack Marketplace overview</span></span>
<span data-ttu-id="5ae6e-104">Hello Marketplace — это совокупность служб, приложений и ресурсы, настроенные для стека Azure как сетей, виртуальных машин, хранилища и т. д.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-104">hello Marketplace is a collection of services, applications, and resources customized for Azure Stack, like networks, virtual machines, storage, and so on.</span></span> <span data-ttu-id="5ae6e-105">Пользователи приглашением toocreate новые ресурсы и разворачивать новые приложения.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-105">Users come here toocreate new resources and deploy new applications.</span></span> <span data-ttu-id="5ae6e-106">Трактовать как корзину каталога, где пользователям можно просмотреть и выбрать элементы hello, они выполнялись toouse.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-106">Think of it as a shopping catalog where users can browse and choose hello items they want toouse.</span></span> <span data-ttu-id="5ae6e-107">toouse элемент Marketplace, пользователям необходимо подписаться tooan предложение, которое предоставит им доступ toohello элемента.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-107">toouse a Marketplace item, users must subscribe tooan offer that grants them access toohello item.</span></span>

<span data-ttu-id="5ae6e-108">В качестве оператор облака, решите, какие элементы tooadd toohello Marketplace (публикации).</span><span class="sxs-lookup"><span data-stu-id="5ae6e-108">As a cloud operator, you decide which items tooadd (publish) toohello Marketplace.</span></span> <span data-ttu-id="5ae6e-109">Вы можете опубликовать таких вещей, как базы данных, службы приложений и т. д.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-109">You can publish things like databases, App Services, and so on.</span></span> <span data-ttu-id="5ae6e-110">Это делает их видимыми tooall пользователей.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-110">This makes them visible tooall your users.</span></span> <span data-ttu-id="5ae6e-111">Вы можете опубликовать создаваемые пользовательские элементы.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-111">You can publish custom items that you create.</span></span> <span data-ttu-id="5ae6e-112">Также можно опубликовать элементы рост [список элементов Azure Marketplace](azure-stack-marketplace-azure-items.md).</span><span class="sxs-lookup"><span data-stu-id="5ae6e-112">You can also publish items from a growing [list of Azure Marketplace items](azure-stack-marketplace-azure-items.md).</span></span> <span data-ttu-id="5ae6e-113">При публикации элемента toohello Marketplace, пользователи могут видеть его в течение пяти минут.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-113">When you publish an item toohello Marketplace, users can see it within five minutes.</span></span>

<span data-ttu-id="5ae6e-114">Щелкните tooopen hello Marketplace, **New**.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-114">tooopen hello Marketplace, click **New**.</span></span>

![](media/azure-stack-publish-custom-marketplace-item/image1.png)

## <a name="marketplace-items"></a><span data-ttu-id="5ae6e-115">Элементы Marketplace</span><span class="sxs-lookup"><span data-stu-id="5ae6e-115">Marketplace items</span></span>
<span data-ttu-id="5ae6e-116">Элемент стека Azure Marketplace — службы, приложения или ресурса, который пользователи могут загрузить и использовать.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-116">An Azure Stack Marketplace item is a service, application, or resource that your users can download and use.</span></span> <span data-ttu-id="5ae6e-117">Все элементы стека Azure Marketplace являются видимыми tooall пользователей.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-117">All Azure Stack Marketplace items are visible tooall your users.</span></span>

<span data-ttu-id="5ae6e-118">У каждого элемента Marketplace есть:</span><span class="sxs-lookup"><span data-stu-id="5ae6e-118">Every Marketplace item has:</span></span>

* <span data-ttu-id="5ae6e-119">Шаблон диспетчера ресурсов для подготовки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-119">An Azure Resource Manager template for resource provisioning</span></span>
* <span data-ttu-id="5ae6e-120">Метаданные, например строки, значки и другие маркетинговые материалы.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-120">Metadata, like strings, icons, and other marketing collateral</span></span>
* <span data-ttu-id="5ae6e-121">Форматирование элемента hello toodisplay сведения на портале hello</span><span class="sxs-lookup"><span data-stu-id="5ae6e-121">Formatting information toodisplay hello item in hello portal</span></span>

<span data-ttu-id="5ae6e-122">Каждый элемент опубликованного toohello Marketplace использует формат вызываемой hello пакет коллекции Azure (azpkg).</span><span class="sxs-lookup"><span data-stu-id="5ae6e-122">Every item published toohello Marketplace uses a format called hello Azure Gallery Package (azpkg).</span></span> <span data-ttu-id="5ae6e-123">Добавление ресурсов развертывания и среды выполнения (например, код ZIP-файлов с программным обеспечением и образы виртуальных машин) tooAzure стека отдельно, не являющийся частью hello Marketplace элемента.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-123">Add deployment or runtime resources (like code, zip files with software, or virtual machine images) tooAzure Stack separately, not as part of hello Marketplace Item.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5ae6e-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5ae6e-124">Next steps</span></span>
[<span data-ttu-id="5ae6e-125">Создание и публикация элементов marketplace</span><span class="sxs-lookup"><span data-stu-id="5ae6e-125">Create and publish a marketplace item</span></span>](azure-stack-create-and-publish-marketplace-item.md)

