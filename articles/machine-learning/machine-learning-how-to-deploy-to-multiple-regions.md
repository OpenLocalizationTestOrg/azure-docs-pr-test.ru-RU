---
title: "Развертывание веб-службы в нескольких регионах | Документация Майкрософт"
description: "Действия по развертыванию (копированию) новой веб-службы в других регионах."
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
ms.openlocfilehash: 3895537bbca72e687838ff5013c291dfee3be707
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-web-service-to-multiple-regions"></a><span data-ttu-id="655b5-103">Развертывание веб-службы в нескольких регионах</span><span class="sxs-lookup"><span data-stu-id="655b5-103">How to deploy a Web Service to multiple regions</span></span>
<span data-ttu-id="655b5-104">Новые веб-службы Azure позволяют легко развернуть веб-службу в нескольких регионах. При этом не требуется иметь несколько подписок или рабочих областей.</span><span class="sxs-lookup"><span data-stu-id="655b5-104">The New Azure Web Services allow you to easily deploy a web service to multiple regions without needing multiple subscriptions or workspaces.</span></span> 

<span data-ttu-id="655b5-105">Цены зависят от региона, поэтому план выставления счетов необходимо определить для каждого региона, в котором будет выполняется развертывание веб-службы.</span><span class="sxs-lookup"><span data-stu-id="655b5-105">Pricing is region specific, therefore you must define a billing plan for each region in which you will deploy the web service.</span></span>

## <a name="to-create-a-plan-in-another-region"></a><span data-ttu-id="655b5-106">Создание плана в другом регионе</span><span class="sxs-lookup"><span data-stu-id="655b5-106">To create a plan in another region</span></span>
1. <span data-ttu-id="655b5-107">Выполните вход в [веб-службы Машинного обучения Microsoft Azure](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="655b5-107">Sign into [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).</span></span>
2. <span data-ttu-id="655b5-108">Щелкните пункт меню **Plans** (Планы).</span><span class="sxs-lookup"><span data-stu-id="655b5-108">Click the **Plans** menu option.</span></span>
3. <span data-ttu-id="655b5-109">На странице Plans overview (Обзор планов) нажмите кнопку **New**(Создать).</span><span class="sxs-lookup"><span data-stu-id="655b5-109">On the Plans over view page, click **New**.</span></span>
4. <span data-ttu-id="655b5-110">В раскрывающемся списке **Subscription** (Подписка) выберите подписку, в которой будет располагаться новый план.</span><span class="sxs-lookup"><span data-stu-id="655b5-110">From the **Subscription** dropdown, select the subscription in which the new plan will reside.</span></span>
5. <span data-ttu-id="655b5-111">В раскрывающемся списке **Region** (Регион) выберите регион для нового плана.</span><span class="sxs-lookup"><span data-stu-id="655b5-111">From the **Region** dropdown, select a region for the new plan.</span></span> <span data-ttu-id="655b5-112">Параметры плана для выбранного региона отобразятся в разделе **Plan Options** (Параметры плана) этой страницы.</span><span class="sxs-lookup"><span data-stu-id="655b5-112">The Plan Options for the selected region will display in the **Plan Options** section of the page.</span></span>
6. <span data-ttu-id="655b5-113">В раскрывающемся списке **Resource Group** (Группа ресурсов) выберите для плана группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="655b5-113">From the **Resource Group** dropdown, select a resource group for the plan.</span></span> <span data-ttu-id="655b5-114">Дополнительные сведения о группах ресурсов см. в статье [Общие сведения об Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="655b5-114">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
7. <span data-ttu-id="655b5-115">В поле **Plan Name** (Имя плана) введите имя плана.</span><span class="sxs-lookup"><span data-stu-id="655b5-115">In **Plan Name** type the name of the plan.</span></span>
8. <span data-ttu-id="655b5-116">В разделе **Plan Options**(Параметры плана) выберите уровень выставления счетов для нового плана.</span><span class="sxs-lookup"><span data-stu-id="655b5-116">Under **Plan Options**, click the billing level for the new plan.</span></span>
9. <span data-ttu-id="655b5-117">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="655b5-117">Click **Create**.</span></span>

## <a name="deploying-the-web-service-to-another-region"></a><span data-ttu-id="655b5-118">Развертывание веб-службы в другом регионе</span><span class="sxs-lookup"><span data-stu-id="655b5-118">Deploying the web service to another region</span></span>
1. <span data-ttu-id="655b5-119">Щелкните пункт меню **Web Services** (Веб-службы).</span><span class="sxs-lookup"><span data-stu-id="655b5-119">Click the **Web Services** menu option.</span></span>
2. <span data-ttu-id="655b5-120">Выберите веб-службу, которую требуется развернуть в новом регионе.</span><span class="sxs-lookup"><span data-stu-id="655b5-120">Select the Web Service you are deploying to a new region.</span></span>
3. <span data-ttu-id="655b5-121">Нажмите **Копировать**.</span><span class="sxs-lookup"><span data-stu-id="655b5-121">Click **Copy**.</span></span>
4. <span data-ttu-id="655b5-122">В поле **Web Service Name**(Имя веб-службы) введите новое имя веб-службы.</span><span class="sxs-lookup"><span data-stu-id="655b5-122">In **Web Service Name**, type a new name for the web service.</span></span>
5. <span data-ttu-id="655b5-123">В поле **Web service description**(Описание веб-службы) введите описание веб-службы.</span><span class="sxs-lookup"><span data-stu-id="655b5-123">In **Web service description**, type a description for the web service.</span></span>
6. <span data-ttu-id="655b5-124">В раскрывающемся списке **Subscription** (Подписка) выберите подписку, в которой будет располагаться новая веб-служба.</span><span class="sxs-lookup"><span data-stu-id="655b5-124">From the **Subscription** dropdown, select the subscription in which the new web service will reside.</span></span>
7. <span data-ttu-id="655b5-125">В раскрывающемся списке **Resource Group** (Группа ресурсов) выберите для веб-службы группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="655b5-125">From the **Resource Group** dropdown, select a resource group for the web service.</span></span> <span data-ttu-id="655b5-126">Дополнительные сведения о группах ресурсов см. в статье [Общие сведения об Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="655b5-126">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="655b5-127">В раскрывающемся списке **Region** (Регион) выберите регион, в котором требуется развернуть веб-службу.</span><span class="sxs-lookup"><span data-stu-id="655b5-127">From the **Region** dropdown, select the region in which to deploy the web service.</span></span>
9. <span data-ttu-id="655b5-128">В раскрывающемся списке **Storage account** (Учетная запись хранения) выберите учетную запись, в которой будет храниться веб-служба.</span><span class="sxs-lookup"><span data-stu-id="655b5-128">From the **Storage account** dropdown, select a storage account in which to store the web service.</span></span>
10. <span data-ttu-id="655b5-129">В раскрывающемся списке **Price Plan** (Ценовой план) выберите план в регионе, который вы выбрали в действии 8.</span><span class="sxs-lookup"><span data-stu-id="655b5-129">From the **Price Plan** dropdown, select a plan in the region you selected in step 8.</span></span>
11. <span data-ttu-id="655b5-130">Нажмите **Копировать**.</span><span class="sxs-lookup"><span data-stu-id="655b5-130">Click **Copy**.</span></span>

