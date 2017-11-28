---
title: "Создание сервера Analysis Services в Azure | Документация Майкрософт"
description: "Узнайте, как создать экземпляр сервера служб Analysis Services в Azure."
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
ms.openlocfilehash: 95b367e7cd74405088190c1fe19cf92990759d90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a><span data-ttu-id="0a17f-103">Создание сервера Azure Analysis Services на портале Azure</span><span class="sxs-lookup"><span data-stu-id="0a17f-103">Create an Azure Analysis Services server in Azure portal</span></span>
<span data-ttu-id="0a17f-104">В этой статье приведено пошаговое руководство по созданию ресурса сервера служб Analysis Services в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="0a17f-104">This article walks you through creating an Analysis Services server resource in your Azure subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0a17f-105">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="0a17f-105">Before you begin</span></span>
<span data-ttu-id="0a17f-106">Для работы с этим кратким руководством вам понадобится:</span><span class="sxs-lookup"><span data-stu-id="0a17f-106">To complete this quickstart, you need:</span></span>

* <span data-ttu-id="0a17f-107">**Подписка Azure**: откройте ссылку на [бесплатную пробную версию Azure](https://azure.microsoft.com/offers/ms-azr-0044p/), чтобы создать учетную запись.</span><span class="sxs-lookup"><span data-stu-id="0a17f-107">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) to create an account.</span></span>
* <span data-ttu-id="0a17f-108">**Azure Active Directory**: ваша подписка должна быть связана с клиентом Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0a17f-108">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant.</span></span> <span data-ttu-id="0a17f-109">И необходимо войти в Azure с учетной записью в этом Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0a17f-109">And, you need to be signed in to Azure with an account in that Azure Active Directory.</span></span> <span data-ttu-id="0a17f-110">Учетные записи Майкрософт не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="0a17f-110">Microsoft accounts are not supported.</span></span> <span data-ttu-id="0a17f-111">Дополнительные сведения см. в руководстве по [аутентификации и настройке пользовательских разрешений](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="0a17f-111">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>
* <span data-ttu-id="0a17f-112">**Группа ресурсов**: используйте уже имеющуюся группу ресурсов или [создайте новую](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0a17f-112">**Resource group**: Use a resource group you already have or [create a new one](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0a17f-113">При создании сервера вам могут выставляться счета за новую службу.</span><span class="sxs-lookup"><span data-stu-id="0a17f-113">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="0a17f-114">Дополнительные сведения см. в разделе [цен на службы Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="0a17f-114">To learn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
> 
> 

## <a name="to-create-a-server-in-azure-portal"></a><span data-ttu-id="0a17f-115">Создание сервера на портале Azure</span><span class="sxs-lookup"><span data-stu-id="0a17f-115">To create a server in Azure portal</span></span>
1. <span data-ttu-id="0a17f-116">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0a17f-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="0a17f-117">Щелкните **+ Создать** > **Данные и аналитика** > **Службы Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="0a17f-117">Click **+ New** > **Data + analytics** > **Analysis Services**.</span></span>
3. <span data-ttu-id="0a17f-118">В колонке **Службы Analysis Services** заполните обязательные поля и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0a17f-118">In the **Analysis Services** blade, fill in the required fields, and then press **Create**.</span></span>
   
    ![Создание сервера](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * <span data-ttu-id="0a17f-120">**Имя сервера**: введите уникальное имя, используемое для обращения к серверу.</span><span class="sxs-lookup"><span data-stu-id="0a17f-120">**Server name**: Type a unique name used to reference the server.</span></span>
   * <span data-ttu-id="0a17f-121">**Подписка**: выберите подписку, в рамках которой выставляются счета за сервер.</span><span class="sxs-lookup"><span data-stu-id="0a17f-121">**Subscription**: Select the subscription this server bills to.</span></span>
   * <span data-ttu-id="0a17f-122">**Группа ресурсов**: это контейнеры, которые помогают управлять коллекцией ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="0a17f-122">**Resource group**: These containers are designed to help you manage a collection of Azure resources.</span></span> <span data-ttu-id="0a17f-123">Дополнительные сведения см. в описании [групп ресурсов](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0a17f-123">To learn more, see [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="0a17f-124">**Расположение**: в этом расположении центра обработки данных Azure размещается сервер.</span><span class="sxs-lookup"><span data-stu-id="0a17f-124">**Location**: This Azure datacenter location hosts the server.</span></span> <span data-ttu-id="0a17f-125">Выберите расположение, ближайшее к крупнейшей имеющейся базе пользователей.</span><span class="sxs-lookup"><span data-stu-id="0a17f-125">Choose a location nearest your largest user base.</span></span>
   * <span data-ttu-id="0a17f-126">**Ценовая категория**: выберите ценовую категорию.</span><span class="sxs-lookup"><span data-stu-id="0a17f-126">**Pricing tier**: Select a pricing tier.</span></span> <span data-ttu-id="0a17f-127">Поддерживаются табличные модели размером до 400 ГБ.</span><span class="sxs-lookup"><span data-stu-id="0a17f-127">Tabular models up to 400 GB are supported.</span></span> <span data-ttu-id="0a17f-128">Дополнительные сведения см. в разделе [цен на службы Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="0a17f-128">To learn more, see [Azure Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
4. <span data-ttu-id="0a17f-129">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0a17f-129">Click **Create**.</span></span>

<span data-ttu-id="0a17f-130">Создание обычно занимает меньше минуты, чаще всего несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="0a17f-130">Create usually takes under a minute; often just a few seconds.</span></span> <span data-ttu-id="0a17f-131">Если был выбран параметр **Add to Portal** (Добавить на портал), перейдите на портал, чтобы просмотреть новый сервер.</span><span class="sxs-lookup"><span data-stu-id="0a17f-131">If you selected **Add to Portal**, navigate to your portal to see your new server.</span></span> <span data-ttu-id="0a17f-132">Или перейдите по адресу **Больше служб** > **Службы Analysis Services**, чтобы проверить, готов ли ваш сервер.</span><span class="sxs-lookup"><span data-stu-id="0a17f-132">Or, navigate to **More services** > **Analysis Services** to see if your server is ready.</span></span>

 ![Панель мониторинга](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a><span data-ttu-id="0a17f-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0a17f-134">Next steps</span></span>
<span data-ttu-id="0a17f-135">После создания сервера вы можете [развернуть на нем модель](analysis-services-deploy.md) с помощью SSDT или SSMS.</span><span class="sxs-lookup"><span data-stu-id="0a17f-135">Once you've created your server, you can [deploy a model](analysis-services-deploy.md) to it by using SSDT or with SSMS.</span></span>

<span data-ttu-id="0a17f-136">Если модель, развертываемая на сервере, подключается к локальным источникам данных, необходимо будет установить [локальный шлюз данных](analysis-services-gateway.md) на одном из компьютеров в вашей сети.</span><span class="sxs-lookup"><span data-stu-id="0a17f-136">If a model you deploy to your server connects to on-premises data sources, you need to install an [On-premises data gateway](analysis-services-gateway.md) on a computer in your network.</span></span>

