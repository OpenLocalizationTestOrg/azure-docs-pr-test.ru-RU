---
title: "aaaHow toodeploy веб-службы областей toomultiple | Документы Microsoft"
description: "Действия toodeploy (копия) регионов tooother веб-службу."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: cgronlun
ms.assetid: 36c60411-f2db-4ee2-9b66-b1f1d77a8f44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 21fcdb96f118c60ed98b60b1b2df833766c7c8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-web-service-toomultiple-regions"></a><span data-ttu-id="b5bee-103">Как toodeploy веб-службы toomultiple областей</span><span class="sxs-lookup"><span data-stu-id="b5bee-103">How toodeploy a Web Service toomultiple regions</span></span>
<span data-ttu-id="b5bee-104">Hello новый веб-службы Azure позволяют tooeasily развертывание web service toomultiple области без необходимости использовать несколько подписок или рабочие области.</span><span class="sxs-lookup"><span data-stu-id="b5bee-104">hello New Azure Web Services allow you tooeasily deploy a web service toomultiple regions without needing multiple subscriptions or workspaces.</span></span> 

<span data-ttu-id="b5bee-105">Цены — область конкретного, поэтому необходимо определить план выставления счетов для каждого региона, в которых выполняется развертывание hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="b5bee-105">Pricing is region specific, therefore you must define a billing plan for each region in which you will deploy hello web service.</span></span>

## <a name="toocreate-a-plan-in-another-region"></a><span data-ttu-id="b5bee-106">toocreate плана в другой регион</span><span class="sxs-lookup"><span data-stu-id="b5bee-106">toocreate a plan in another region</span></span>
1. <span data-ttu-id="b5bee-107">Выполните вход в [веб-службы Машинного обучения Microsoft Azure](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="b5bee-107">Sign into [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).</span></span>
2. <span data-ttu-id="b5bee-108">Нажмите кнопку hello **планы** пункт меню.</span><span class="sxs-lookup"><span data-stu-id="b5bee-108">Click hello **Plans** menu option.</span></span>
3. <span data-ttu-id="b5bee-109">В планах hello через представление страницы, нажмите кнопку **New**.</span><span class="sxs-lookup"><span data-stu-id="b5bee-109">On hello Plans over view page, click **New**.</span></span>
4. <span data-ttu-id="b5bee-110">Из hello **подписки** раскрывающийся список, в какие hello новый план будет находиться подписки выберите hello.</span><span class="sxs-lookup"><span data-stu-id="b5bee-110">From hello **Subscription** dropdown, select hello subscription in which hello new plan will reside.</span></span>
5. <span data-ttu-id="b5bee-111">Из hello **область** раскрывающийся список, выберите регион для hello новый план.</span><span class="sxs-lookup"><span data-stu-id="b5bee-111">From hello **Region** dropdown, select a region for hello new plan.</span></span> <span data-ttu-id="b5bee-112">Hello параметры плана для hello выбранной области будут отображаться в hello **параметры плана** раздел страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="b5bee-112">hello Plan Options for hello selected region will display in hello **Plan Options** section of hello page.</span></span>
6. <span data-ttu-id="b5bee-113">Из hello **группы ресурсов** раскрывающийся список, выберите группу ресурсов для hello плана.</span><span class="sxs-lookup"><span data-stu-id="b5bee-113">From hello **Resource Group** dropdown, select a resource group for hello plan.</span></span> <span data-ttu-id="b5bee-114">Дополнительные сведения о группах ресурсов см. в статье [Общие сведения об Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b5bee-114">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
7. <span data-ttu-id="b5bee-115">В **имя плана** имя типа hello hello плана.</span><span class="sxs-lookup"><span data-stu-id="b5bee-115">In **Plan Name** type hello name of hello plan.</span></span>
8. <span data-ttu-id="b5bee-116">В разделе **параметры плана**, выберите уровень выставления счетов hello для hello новый план.</span><span class="sxs-lookup"><span data-stu-id="b5bee-116">Under **Plan Options**, click hello billing level for hello new plan.</span></span>
9. <span data-ttu-id="b5bee-117">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b5bee-117">Click **Create**.</span></span>

## <a name="deploying-hello-web-service-tooanother-region"></a><span data-ttu-id="b5bee-118">Развертывание hello web service tooanother области</span><span class="sxs-lookup"><span data-stu-id="b5bee-118">Deploying hello web service tooanother region</span></span>
1. <span data-ttu-id="b5bee-119">Нажмите кнопку hello **веб-службы** пункт меню.</span><span class="sxs-lookup"><span data-stu-id="b5bee-119">Click hello **Web Services** menu option.</span></span>
2. <span data-ttu-id="b5bee-120">Выберите веб-служба развертывается новая область tooa hello.</span><span class="sxs-lookup"><span data-stu-id="b5bee-120">Select hello Web Service you are deploying tooa new region.</span></span>
3. <span data-ttu-id="b5bee-121">Нажмите **Копировать**.</span><span class="sxs-lookup"><span data-stu-id="b5bee-121">Click **Copy**.</span></span>
4. <span data-ttu-id="b5bee-122">В **имя веб-службы**, введите новое имя для hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="b5bee-122">In **Web Service Name**, type a new name for hello web service.</span></span>
5. <span data-ttu-id="b5bee-123">В **веб-службы описание**, введите описание для hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="b5bee-123">In **Web service description**, type a description for hello web service.</span></span>
6. <span data-ttu-id="b5bee-124">Из hello **подписки** раскрывающийся список, выберите hello подписки, в которой hello будет находиться веб-службу.</span><span class="sxs-lookup"><span data-stu-id="b5bee-124">From hello **Subscription** dropdown, select hello subscription in which hello new web service will reside.</span></span>
7. <span data-ttu-id="b5bee-125">Из hello **группы ресурсов** раскрывающийся список, выберите группу ресурсов для hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="b5bee-125">From hello **Resource Group** dropdown, select a resource group for hello web service.</span></span> <span data-ttu-id="b5bee-126">Дополнительные сведения о группах ресурсов см. в статье [Общие сведения об Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b5bee-126">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="b5bee-127">Из hello **область** раскрывающийся список, выберите hello региона, в какие toodeploy hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="b5bee-127">From hello **Region** dropdown, select hello region in which toodeploy hello web service.</span></span>
9. <span data-ttu-id="b5bee-128">Из hello **учетной записи хранилища** раскрывающийся список, выберите учетную запись хранения в которых hello toostore веб-службы.</span><span class="sxs-lookup"><span data-stu-id="b5bee-128">From hello **Storage account** dropdown, select a storage account in which toostore hello web service.</span></span>
10. <span data-ttu-id="b5bee-129">Из hello **цена плана** раскрывающийся список, выберите план в регионе hello, выбранная на шаге 8.</span><span class="sxs-lookup"><span data-stu-id="b5bee-129">From hello **Price Plan** dropdown, select a plan in hello region you selected in step 8.</span></span>
11. <span data-ttu-id="b5bee-130">Нажмите **Копировать**.</span><span class="sxs-lookup"><span data-stu-id="b5bee-130">Click **Copy**.</span></span>

