---
title: "портал aaaAzure для политики ресурсов | Документы Microsoft"
description: "Описывает способ toouse Azure портала toocreate политик диспетчера ресурсов и управление ими. Политики могут применяться для групп hello подписка или ресурс."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: ce6413386317e532b63761a24458b85c996af4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-tooassign-and-manage-resource-policies"></a><span data-ttu-id="18cb7-104">Использование Azure портала tooassign политики и управлять ими ресурсов</span><span class="sxs-lookup"><span data-stu-id="18cb7-104">Use Azure portal tooassign and manage resource policies</span></span>
<span data-ttu-id="18cb7-105">Hello портал Azure позволяет вам tooassign политики tooresource групп ресурсов и подписки.</span><span class="sxs-lookup"><span data-stu-id="18cb7-105">hello Azure portal enables you tooassign resource policies tooresource groups and subscriptions.</span></span> <span data-ttu-id="18cb7-106">Hello пользовательский интерфейс позволяет легко tooselect hello политики требуется tooassign и укажите значения параметров для этого toocustomize hello политика.</span><span class="sxs-lookup"><span data-stu-id="18cb7-106">hello user interface makes it easy tooselect hello policy that you want tooassign, and specify parameter values for that policy toocustomize hello policy settings.</span></span> 

<span data-ttu-id="18cb7-107">tooassign политики через портал hello определения политики hello должна существовать в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="18cb7-107">tooassign a policy through hello portal, hello policy definition must already exist in your subscription.</span></span> <span data-ttu-id="18cb7-108">Ваша подписка имеет несколько определений встроенных политик, готовых для вас tooassign tooresource группы или подписки.</span><span class="sxs-lookup"><span data-stu-id="18cb7-108">Your subscription has several built-in policy definitions that are ready for you tooassign tooresource groups or subscriptions.</span></span> <span data-ttu-id="18cb7-109">Вы увидите этих встроенных политик и пользовательских политик, определенных при использовании портала tooassign политики hello.</span><span class="sxs-lookup"><span data-stu-id="18cb7-109">You see these built-in policies and any custom policies you have defined when using hello portal tooassign policies.</span></span> <span data-ttu-id="18cb7-110">Toopolicies введение и как toodefine настроить политики см. в разделе [Общие сведения о политике ресурсов](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="18cb7-110">For an introduction toopolicies and how toodefine customized policy, see [Resource policy overview](resource-manager-policy.md).</span></span>

<span data-ttu-id="18cb7-111">Политики наследуются всеми дочерними ресурсами.</span><span class="sxs-lookup"><span data-stu-id="18cb7-111">Policies are inherited by all child resources.</span></span> <span data-ttu-id="18cb7-112">Таким образом Если политика не применяется tooa группы ресурсов, это применимо tooall hello ресурсов в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="18cb7-112">So, if a policy is applied tooa resource group, it is applicable tooall hello resources in that resource group.</span></span> <span data-ttu-id="18cb7-113">В этой статье термин hello **область** ссылается toohello группы ресурсов или подписку, которая будет назначена политика hello.</span><span class="sxs-lookup"><span data-stu-id="18cb7-113">In this article, hello term **scope** refers toohello resource group or subscription that is assigned hello policy.</span></span> 

<span data-ttu-id="18cb7-114">Политики оцениваются при создании и обновлении ресурсов (операции PUT и PATCH).</span><span class="sxs-lookup"><span data-stu-id="18cb7-114">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

## <a name="assign-a-policy"></a><span data-ttu-id="18cb7-115">Назначение политики</span><span class="sxs-lookup"><span data-stu-id="18cb7-115">Assign a policy</span></span>

1. <span data-ttu-id="18cb7-116">tooassign tooeither политики группу ресурсов или подписку, выберите этой группы ресурсов или подписки.</span><span class="sxs-lookup"><span data-stu-id="18cb7-116">tooassign a policy tooeither a resource group or subscription, select that resource group or subscription.</span></span> <span data-ttu-id="18cb7-117">В параметрах hello выберите **политики**.</span><span class="sxs-lookup"><span data-stu-id="18cb7-117">In hello settings, select **Policies**.</span></span>

   ![выбор политик](./media/resource-manager-policy-portal/select-policies.png)

2. <span data-ttu-id="18cb7-119">Выберите назначение политики для этой области toocreate **добавить назначение**.</span><span class="sxs-lookup"><span data-stu-id="18cb7-119">toocreate a policy assignment for this scope, select **Add assignment**.</span></span>

   ![добавление назначения](./media/resource-manager-policy-portal/add-assignment.png)

3. <span data-ttu-id="18cb7-121">Выберите политику hello требуется tooassign.</span><span class="sxs-lookup"><span data-stu-id="18cb7-121">Select hello policy you want tooassign.</span></span> <span data-ttu-id="18cb7-122">Даже если вы не добавили любую подписку tooyour определения политики, может появиться hello встроенных политик, доступных для назначения.</span><span class="sxs-lookup"><span data-stu-id="18cb7-122">Even if you have not added any policy definitions tooyour subscription, you see hello built-in policies that are available for assignment.</span></span> <span data-ttu-id="18cb7-123">Эти встроенные политики охватывают множество распространенных сценариев.</span><span class="sxs-lookup"><span data-stu-id="18cb7-123">These built-in policies cover many common scenarios.</span></span>

   ![выбор определения](./media/resource-manager-policy-portal/select-definition.png)

4. <span data-ttu-id="18cb7-125">После выбора политики, то см. описание политики hello и все параметры этой политики.</span><span class="sxs-lookup"><span data-stu-id="18cb7-125">After selecting a policy, you see a description of hello policy, and any parameters for that policy.</span></span> <span data-ttu-id="18cb7-126">Hello следующем рисунке показано, hello **допускается расположения** параметр, который требуется для hello политику, которая ограничивает hello доступных расположений.</span><span class="sxs-lookup"><span data-stu-id="18cb7-126">For example, hello following image shows hello **Allowed locations** parameter, which is required for hello policy that restricts hello available locations.</span></span>

   ![отображение параметров](./media/resource-manager-policy-portal/show-parameters.png)

5. <span data-ttu-id="18cb7-128">Пользовательским интерфейсом приложения hello выберите hello toospecify значения для параметров политики hello (например, размещение hello, которые могут использоваться для развертывания).</span><span class="sxs-lookup"><span data-stu-id="18cb7-128">Through hello user interface, select hello values toospecify for hello policy parameters (such as hello locations that can be used for deployment).</span></span>

   ![выбор значений параметров](./media/resource-manager-policy-portal/select-parameters.png)

6. <span data-ttu-id="18cb7-130">Укажите значения для hello другие параметры.</span><span class="sxs-lookup"><span data-stu-id="18cb7-130">Provide values for hello other parameters.</span></span> <span data-ttu-id="18cb7-131">область Hello задается автоматически в колонке hello, выбранным при запуске назначения политики hello.</span><span class="sxs-lookup"><span data-stu-id="18cb7-131">hello scope is automatically assigned based on hello blade you selected when starting hello policy assignment.</span></span> <span data-ttu-id="18cb7-132">По окончании нажмите кнопку **ОК** .</span><span class="sxs-lookup"><span data-stu-id="18cb7-132">Select **OK** when done.</span></span>

   ![определение параметров](./media/resource-manager-policy-portal/define-parameters.png)

  <span data-ttu-id="18cb7-134">Назначена политика hello toohello указан области.</span><span class="sxs-lookup"><span data-stu-id="18cb7-134">You have assigned hello policy toohello specified scope.</span></span>

## <a name="view-policy-assignments"></a><span data-ttu-id="18cb7-135">Просмотр назначенных политик</span><span class="sxs-lookup"><span data-stu-id="18cb7-135">View policy assignments</span></span>

<span data-ttu-id="18cb7-136">После назначения политики, найдите его в списке hello политик для данной области.</span><span class="sxs-lookup"><span data-stu-id="18cb7-136">After assigning a policy, you see it in hello list of policies for that scope.</span></span> <span data-ttu-id="18cb7-137">Hello **сведения** вкладка со сводкой назначения политики hello.</span><span class="sxs-lookup"><span data-stu-id="18cb7-137">hello **Details** tab shows a summary of hello policy assignment.</span></span>

![отображение сведений](./media/resource-manager-policy-portal/show-details.png)

<span data-ttu-id="18cb7-139">Hello **правила назначения** вкладке отображается hello JSON для определения политики hello.</span><span class="sxs-lookup"><span data-stu-id="18cb7-139">hello **Assignment rule** tab shows hello JSON for hello policy definition.</span></span>

![отображение правила назначения](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a><span data-ttu-id="18cb7-141">Изменение существующего назначения политики</span><span class="sxs-lookup"><span data-stu-id="18cb7-141">Change an existing policy assignment</span></span>

<span data-ttu-id="18cb7-142">Выберите политику, toochange **изменить назначение** или **удалить**</span><span class="sxs-lookup"><span data-stu-id="18cb7-142">toochange a policy, select **Edit assignment** or **Delete**</span></span>

![изменение или удаление назначения](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a><span data-ttu-id="18cb7-144">Назначение пользовательских политик</span><span class="sxs-lookup"><span data-stu-id="18cb7-144">Assign custom policies</span></span>

<span data-ttu-id="18cb7-145">Если в вашей подписке определены настраиваемые политики, эти политики доступны для назначения через портал hello.</span><span class="sxs-lookup"><span data-stu-id="18cb7-145">If you have defined custom policies in your subscription, those policies are available for assignment through hello portal.</span></span> <span data-ttu-id="18cb7-146">Эти политики содержат в своем названии приставку **[Custom]**.</span><span class="sxs-lookup"><span data-stu-id="18cb7-146">Those policies are prefaced with **[Custom]**</span></span>

![пользовательские политики](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a><span data-ttu-id="18cb7-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="18cb7-148">Next steps</span></span>
* <span data-ttu-id="18cb7-149">toolearn о синтаксисе hello JSON для определения политик, в разделе [Общие сведения о политике ресурсов](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="18cb7-149">toolearn about hello JSON syntax for defining policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="18cb7-150">Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="18cb7-150">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="18cb7-151">Схема политики Hello опубликованы по адресу [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="18cb7-151">hello policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

