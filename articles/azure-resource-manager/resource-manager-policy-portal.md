---
title: "Портал Azure для политик ресурсов | Документация Майкрософт"
description: "Описывается использование портала Azure для создания политик Resource Manager и управления ими. Политики можно применять на уровне подписки или группы ресурсов."
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
ms.openlocfilehash: 868b2cc1559053057d17b34c03e2e31347f399bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-portal-to-assign-and-manage-resource-policies"></a><span data-ttu-id="b9fd1-104">Назначение политик ресурсов и управление ими с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="b9fd1-104">Use Azure portal to assign and manage resource policies</span></span>
<span data-ttu-id="b9fd1-105">Портал Azure позволяет назначить группам ресурсов и подпискам политики ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-105">The Azure portal enables you to assign resource policies to resource groups and subscriptions.</span></span> <span data-ttu-id="b9fd1-106">Пользовательский интерфейс позволяет с легкостью выбрать политику, которую требуется назначить, и указать значения параметров политики, чтобы ее настроить.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-106">The user interface makes it easy to select the policy that you want to assign, and specify parameter values for that policy to customize the policy settings.</span></span> 

<span data-ttu-id="b9fd1-107">Для назначения политики помощью портала в вашей подписке уже должно существовать определение политики.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-107">To assign a policy through the portal, the policy definition must already exist in your subscription.</span></span> <span data-ttu-id="b9fd1-108">Подписка имеет несколько встроенных определений политики, которые можно назначить группам ресурсов или подпискам.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-108">Your subscription has several built-in policy definitions that are ready for you to assign to resource groups or subscriptions.</span></span> <span data-ttu-id="b9fd1-109">Вы увидите эти встроенные политики, а также все определенные вами пользовательские политики, когда воспользуетесь порталом для назначения политик.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-109">You see these built-in policies and any custom policies you have defined when using the portal to assign policies.</span></span> <span data-ttu-id="b9fd1-110">Введение в политики, а также сведения об определении пользовательских политик, см. в статье [Общие сведения о политике ресурсов](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="b9fd1-110">For an introduction to policies and how to define customized policy, see [Resource policy overview](resource-manager-policy.md).</span></span>

<span data-ttu-id="b9fd1-111">Политики наследуются всеми дочерними ресурсами.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-111">Policies are inherited by all child resources.</span></span> <span data-ttu-id="b9fd1-112">Это значит, что политики, применяемые к группе ресурсов, применяются также ко всем ресурсам в этой группе.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-112">So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.</span></span> <span data-ttu-id="b9fd1-113">В этой статье термин **область** обозначает группу ресурсов или подписку, которым назначена политика.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-113">In this article, the term **scope** refers to the resource group or subscription that is assigned the policy.</span></span> 

<span data-ttu-id="b9fd1-114">Политики оцениваются при создании и обновлении ресурсов (операции PUT и PATCH).</span><span class="sxs-lookup"><span data-stu-id="b9fd1-114">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

## <a name="assign-a-policy"></a><span data-ttu-id="b9fd1-115">Назначение политики</span><span class="sxs-lookup"><span data-stu-id="b9fd1-115">Assign a policy</span></span>

1. <span data-ttu-id="b9fd1-116">Чтобы назначить политику группе ресурсов или подписке, выберите соответствующую группу ресурсов или подписку.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-116">To assign a policy to either a resource group or subscription, select that resource group or subscription.</span></span> <span data-ttu-id="b9fd1-117">В разделе "Параметры" выберите **Политики**.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-117">In the settings, select **Policies**.</span></span>

   ![выбор политик](./media/resource-manager-policy-portal/select-policies.png)

2. <span data-ttu-id="b9fd1-119">Чтобы создать назначение политики для этой области, выберите **Добавить назначение**.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-119">To create a policy assignment for this scope, select **Add assignment**.</span></span>

   ![добавление назначения](./media/resource-manager-policy-portal/add-assignment.png)

3. <span data-ttu-id="b9fd1-121">Выберите политику, которую необходимо назначить.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-121">Select the policy you want to assign.</span></span> <span data-ttu-id="b9fd1-122">Даже если вы не добавили в свою подписку ни одного определения политики, отобразятся встроенные политики, которые можно назначить.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-122">Even if you have not added any policy definitions to your subscription, you see the built-in policies that are available for assignment.</span></span> <span data-ttu-id="b9fd1-123">Эти встроенные политики охватывают множество распространенных сценариев.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-123">These built-in policies cover many common scenarios.</span></span>

   ![выбор определения](./media/resource-manager-policy-portal/select-definition.png)

4. <span data-ttu-id="b9fd1-125">После того, как политика выбрана, отображается описание политики, а также ее параметры.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-125">After selecting a policy, you see a description of the policy, and any parameters for that policy.</span></span> <span data-ttu-id="b9fd1-126">Например, на следующем изображении показан параметр **Allowed locations** (Допустимые расположения), который необходим для политики, ограничивающей доступные расположения.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-126">For example, the following image shows the **Allowed locations** parameter, which is required for the policy that restricts the available locations.</span></span>

   ![отображение параметров](./media/resource-manager-policy-portal/show-parameters.png)

5. <span data-ttu-id="b9fd1-128">Через пользовательский интерфейс выберите значения для параметров политики (например, укажите расположения, которые можно использовать для развертывания).</span><span class="sxs-lookup"><span data-stu-id="b9fd1-128">Through the user interface, select the values to specify for the policy parameters (such as the locations that can be used for deployment).</span></span>

   ![выбор значений параметров](./media/resource-manager-policy-portal/select-parameters.png)

6. <span data-ttu-id="b9fd1-130">Укажите значения остальных параметров.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-130">Provide values for the other parameters.</span></span> <span data-ttu-id="b9fd1-131">Область назначается автоматически, исходя из колонки, выбранной в начале процесса назначения политики.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-131">The scope is automatically assigned based on the blade you selected when starting the policy assignment.</span></span> <span data-ttu-id="b9fd1-132">По окончании нажмите кнопку **ОК** .</span><span class="sxs-lookup"><span data-stu-id="b9fd1-132">Select **OK** when done.</span></span>

   ![определение параметров](./media/resource-manager-policy-portal/define-parameters.png)

  <span data-ttu-id="b9fd1-134">Вы назначили политику для указанной области.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-134">You have assigned the policy to the specified scope.</span></span>

## <a name="view-policy-assignments"></a><span data-ttu-id="b9fd1-135">Просмотр назначенных политик</span><span class="sxs-lookup"><span data-stu-id="b9fd1-135">View policy assignments</span></span>

<span data-ttu-id="b9fd1-136">После назначения политики она появиться в списке политик для данной области.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-136">After assigning a policy, you see it in the list of policies for that scope.</span></span> <span data-ttu-id="b9fd1-137">На вкладке **Сведения** отображается сводка по назначению политики.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-137">The **Details** tab shows a summary of the policy assignment.</span></span>

![отображение сведений](./media/resource-manager-policy-portal/show-details.png)

<span data-ttu-id="b9fd1-139">На вкладке **Правило назначения** отображается файл JSON для определения политики.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-139">The **Assignment rule** tab shows the JSON for the policy definition.</span></span>

![отображение правила назначения](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a><span data-ttu-id="b9fd1-141">Изменение существующего назначения политики</span><span class="sxs-lookup"><span data-stu-id="b9fd1-141">Change an existing policy assignment</span></span>

<span data-ttu-id="b9fd1-142">Чтобы изменить политику, щелкните **Изменить назначение** или **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-142">To change a policy, select **Edit assignment** or **Delete**</span></span>

![изменение или удаление назначения](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a><span data-ttu-id="b9fd1-144">Назначение пользовательских политик</span><span class="sxs-lookup"><span data-stu-id="b9fd1-144">Assign custom policies</span></span>

<span data-ttu-id="b9fd1-145">Если в подписке определены пользовательские политики, то их можно назначить с помощью портала.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-145">If you have defined custom policies in your subscription, those policies are available for assignment through the portal.</span></span> <span data-ttu-id="b9fd1-146">Эти политики содержат в своем названии приставку **[Custom]**.</span><span class="sxs-lookup"><span data-stu-id="b9fd1-146">Those policies are prefaced with **[Custom]**</span></span>

![пользовательские политики](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a><span data-ttu-id="b9fd1-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b9fd1-148">Next steps</span></span>
* <span data-ttu-id="b9fd1-149">Сведения о синтаксисе JSON для определений политик см. в статье [Общие сведения о политике ресурсов](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="b9fd1-149">To learn about the JSON syntax for defining policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="b9fd1-150">Руководство по использованию Resource Manager для эффективного управления подписками в организациях см [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Шаблон Azure для организаций. Рекомендуемая система управления подпиской).</span><span class="sxs-lookup"><span data-stu-id="b9fd1-150">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="b9fd1-151">Схема политики опубликована на странице [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="b9fd1-151">The policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

