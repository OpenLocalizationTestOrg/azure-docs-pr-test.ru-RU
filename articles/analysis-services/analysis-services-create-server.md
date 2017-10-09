---
title: "aaaCreate серверу служб Analysis Services в Azure | Документы Microsoft"
description: "Узнайте, как экземпляр toocreate серверу служб Analysis Services в Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 7f560216-8a9a-4d06-852e-48cf24deab19
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 3668f659039f79f3dd71498d1066e8682bf33228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a><span data-ttu-id="9bf1f-103">Создание сервера Azure Analysis Services на портале Azure</span><span class="sxs-lookup"><span data-stu-id="9bf1f-103">Create an Azure Analysis Services server in Azure portal</span></span>
<span data-ttu-id="9bf1f-104">В этой статье приведено пошаговое руководство по созданию ресурса сервера служб Analysis Services в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="9bf1f-104">This article walks you through creating an Analysis Services server resource in your Azure subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9bf1f-105">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="9bf1f-105">Before you begin</span></span>
<span data-ttu-id="9bf1f-106">toocomplete краткого руководства, необходимо:</span><span class="sxs-lookup"><span data-stu-id="9bf1f-106">toocomplete this quickstart, you need:</span></span>

* <span data-ttu-id="9bf1f-107">**Подписка Azure**: посетите [бесплатная пробная версия](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate учетную запись.</span><span class="sxs-lookup"><span data-stu-id="9bf1f-107">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate an account.</span></span>
* <span data-ttu-id="9bf1f-108">**Azure Active Directory**: ваша подписка должна быть связана с клиентом Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9bf1f-108">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant.</span></span> <span data-ttu-id="9bf1f-109">И требуется toobe вход tooAzure с учетной записью в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9bf1f-109">And, you need toobe signed in tooAzure with an account in that Azure Active Directory.</span></span> <span data-ttu-id="9bf1f-110">Учетные записи Майкрософт не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="9bf1f-110">Microsoft accounts are not supported.</span></span> <span data-ttu-id="9bf1f-111">toolearn более, в разделе [проверки подлинности и пользовательские разрешения](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="9bf1f-111">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>
* <span data-ttu-id="9bf1f-112">**Группа ресурсов**: используйте уже имеющуюся группу ресурсов или [создайте новую](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9bf1f-112">**Resource group**: Use a resource group you already have or [create a new one](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9bf1f-113">При создании сервера вам могут выставляться счета за новую службу.</span><span class="sxs-lookup"><span data-stu-id="9bf1f-113">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="9bf1f-114">toolearn более, в разделе [цены служб Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="9bf1f-114">toolearn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
> 
> 

## <a name="toocreate-a-server-in-azure-portal"></a><span data-ttu-id="9bf1f-115">toocreate сервера на портале Azure</span><span class="sxs-lookup"><span data-stu-id="9bf1f-115">toocreate a server in Azure portal</span></span>
1. <span data-ttu-id="9bf1f-116">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9bf1f-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="9bf1f-117">Щелкните **+ Создать** > **Данные и аналитика** > **Службы Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="9bf1f-117">Click **+ New** > **Data + analytics** > **Analysis Services**.</span></span>
3. <span data-ttu-id="9bf1f-118">В hello **служб Analysis Services** колонки, заполните поля требуется hello и нажмите клавишу **создать**.</span><span class="sxs-lookup"><span data-stu-id="9bf1f-118">In hello **Analysis Services** blade, fill in hello required fields, and then press **Create**.</span></span>
   
    ![Создание сервера](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * <span data-ttu-id="9bf1f-120">**Имя сервера**: Введите уникальное имя, используемое tooreference hello сервер.</span><span class="sxs-lookup"><span data-stu-id="9bf1f-120">**Server name**: Type a unique name used tooreference hello server.</span></span>
   * <span data-ttu-id="9bf1f-121">**Подписки**: выберите подписку hello выставляет счет этого сервера для.</span><span class="sxs-lookup"><span data-stu-id="9bf1f-121">**Subscription**: Select hello subscription this server bills to.</span></span>
   * <span data-ttu-id="9bf1f-122">**Группа ресурсов**: эти контейнеры являются спроектированный toohelp управлять коллекцией ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="9bf1f-122">**Resource group**: These containers are designed toohelp you manage a collection of Azure resources.</span></span> <span data-ttu-id="9bf1f-123">toolearn более, в разделе [групп ресурсов](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9bf1f-123">toolearn more, see [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="9bf1f-124">**Расположение**: узлы расположение центра обработки данных Azure этот hello server.</span><span class="sxs-lookup"><span data-stu-id="9bf1f-124">**Location**: This Azure datacenter location hosts hello server.</span></span> <span data-ttu-id="9bf1f-125">Выберите расположение, ближайшее к крупнейшей имеющейся базе пользователей.</span><span class="sxs-lookup"><span data-stu-id="9bf1f-125">Choose a location nearest your largest user base.</span></span>
   * <span data-ttu-id="9bf1f-126">**Ценовая категория**: выберите ценовую категорию.</span><span class="sxs-lookup"><span data-stu-id="9bf1f-126">**Pricing tier**: Select a pricing tier.</span></span> <span data-ttu-id="9bf1f-127">Поддерживаются табличные модели too400 Гбайт.</span><span class="sxs-lookup"><span data-stu-id="9bf1f-127">Tabular models up too400 GB are supported.</span></span> <span data-ttu-id="9bf1f-128">toolearn более, в разделе [ценообразования Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="9bf1f-128">toolearn more, see [Azure Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
4. <span data-ttu-id="9bf1f-129">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9bf1f-129">Click **Create**.</span></span>

<span data-ttu-id="9bf1f-130">Создание обычно занимает меньше минуты, чаще всего несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="9bf1f-130">Create usually takes under a minute; often just a few seconds.</span></span> <span data-ttu-id="9bf1f-131">Если вы выбрали **добавить tooPortal**, перейти на новый сервер портала toosee tooyour.</span><span class="sxs-lookup"><span data-stu-id="9bf1f-131">If you selected **Add tooPortal**, navigate tooyour portal toosee your new server.</span></span> <span data-ttu-id="9bf1f-132">Или перейдите слишком**дополнительные службы** > **служб Analysis Services** toosee, если сервер готов.</span><span class="sxs-lookup"><span data-stu-id="9bf1f-132">Or, navigate too**More services** > **Analysis Services** toosee if your server is ready.</span></span>

 ![Панель мониторинга](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a><span data-ttu-id="9bf1f-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9bf1f-134">Next steps</span></span>
<span data-ttu-id="9bf1f-135">После создания сервера, вы можете [развернуть модель](analysis-services-deploy.md) tooit посредством SSDT или с помощью среды SSMS.</span><span class="sxs-lookup"><span data-stu-id="9bf1f-135">Once you've created your server, you can [deploy a model](analysis-services-deploy.md) tooit by using SSDT or with SSMS.</span></span>

<span data-ttu-id="9bf1f-136">При развертывании сервера tooyour модель подключается tooon локальные источники данных, необходимо tooinstall [локального шлюза данных](analysis-services-gateway.md) на компьютере в сети.</span><span class="sxs-lookup"><span data-stu-id="9bf1f-136">If a model you deploy tooyour server connects tooon-premises data sources, you need tooinstall an [On-premises data gateway](analysis-services-gateway.md) on a computer in your network.</span></span>

