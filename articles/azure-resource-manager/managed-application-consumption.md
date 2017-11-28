---
title: "приложения с управляемым aaaConsume Azure | Документы Microsoft"
description: "В этой статье описывается, как создавать управляемое приложение Azure с помощью опубликованных файлов."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b8510086eb05304c0e351a391b7e0cf34a467568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-internal-managed-application"></a><span data-ttu-id="25fb3-103">Использование внутреннего управляемого приложения</span><span class="sxs-lookup"><span data-stu-id="25fb3-103">Consume an internal managed application</span></span>

<span data-ttu-id="25fb3-104">Можно использовать [управляемые приложения](managed-application-overview.md) Azure, предназначенные для членов вашей организации.</span><span class="sxs-lookup"><span data-stu-id="25fb3-104">You can consume Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="25fb3-105">Например, можно выбрать управляемые приложения отдела ИТ, которые обеспечивают соответствие стандартам организации.</span><span class="sxs-lookup"><span data-stu-id="25fb3-105">For example, you can select managed applications from your IT department that ensure compliance with organizational standards.</span></span> <span data-ttu-id="25fb3-106">Эти управляемые приложения доступны через hello каталога услуг, hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="25fb3-106">These managed applications are available through hello Service Catalog, not hello Azure Marketplace.</span></span>

<span data-ttu-id="25fb3-107">Прежде чем продолжить эту статью, необходимо иметь управляемого приложения, доступные в каталог услуг hello для вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="25fb3-107">Before proceeding with this article, you must have a managed application available in hello service catalog for your subscription.</span></span> <span data-ttu-id="25fb3-108">Если кто-либо в вашей организации еще не создал управляемое приложение, ознакомьтесь с разделом [Создание и публикация управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="25fb3-108">If someone in your organization has not already created a managed application, see [Publish a managed application for internal consumption](managed-application-publishing.md).</span></span>

<span data-ttu-id="25fb3-109">В настоящее время можно использовать Azure CLI или hello Azure портала tooconsume управляемого приложения.</span><span class="sxs-lookup"><span data-stu-id="25fb3-109">Currently, you can use either Azure CLI or hello Azure portal tooconsume a managed application.</span></span>

## <a name="create-hello-managed-application-by-using-hello-portal"></a><span data-ttu-id="25fb3-110">Создание приложения hello управляемых с помощью портала hello</span><span class="sxs-lookup"><span data-stu-id="25fb3-110">Create hello managed application by using hello portal</span></span>

<span data-ttu-id="25fb3-111">toodeploy управляемого приложения через портал hello, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="25fb3-111">toodeploy a managed application through hello portal, follow these steps:</span></span>

1. <span data-ttu-id="25fb3-112">Go toohello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="25fb3-112">Go toohello Azure portal.</span></span> <span data-ttu-id="25fb3-113">Найдите **управляемое приложение из каталога услуг**.</span><span class="sxs-lookup"><span data-stu-id="25fb3-113">Search for **Service Catalog Managed Application**.</span></span>

   ![Управляемое приложение каталога услуг](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. <span data-ttu-id="25fb3-115">Выберите hello управляемого приложения, нужно toocreate из списка доступных решений hello.</span><span class="sxs-lookup"><span data-stu-id="25fb3-115">Select hello managed application you want toocreate from hello list of available solutions.</span></span> <span data-ttu-id="25fb3-116">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="25fb3-116">Select **Create**.</span></span>

   ![Выбор управляемого приложения](./media/managed-application-consumption/select-offer.png)

1. <span data-ttu-id="25fb3-118">Укажите значения для параметра hello, которые требуется tooprovision hello ресурсы.</span><span class="sxs-lookup"><span data-stu-id="25fb3-118">Provide values for hello parameters that are required tooprovision hello resources.</span></span> <span data-ttu-id="25fb3-119">Выберите расположение **Западно-центральная часть США**.</span><span class="sxs-lookup"><span data-stu-id="25fb3-119">Select **West Central US** for location.</span></span> <span data-ttu-id="25fb3-120">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="25fb3-120">Select **OK**.</span></span>

   ![Параметры управляемого приложения](./media/managed-application-consumption/input-parameters.png)

1. <span data-ttu-id="25fb3-122">шаблон Hello проверяет заданных значений hello.</span><span class="sxs-lookup"><span data-stu-id="25fb3-122">hello template validates hello values you provided.</span></span> <span data-ttu-id="25fb3-123">Если проверка прошла успешно, выберите **ОК** toostart hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="25fb3-123">If validation succeeds, select **OK** toostart hello deployment.</span></span>

   ![Проверка управляемого приложения](./media/managed-application-consumption/validation.png)

<span data-ttu-id="25fb3-125">После завершения развертывания hello в группе hello управляемых ресурсов, предоставленные подготавливаются hello соответствующие ресурсы, определенные в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="25fb3-125">After hello deployment finishes, hello appropriate resources defined in hello template are provisioned in hello managed resource group you provided.</span></span>

## <a name="create-hello-managed-application-by-using-azure-cli"></a><span data-ttu-id="25fb3-126">Создание приложения hello управляемых с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="25fb3-126">Create hello managed application by using Azure CLI</span></span>

<span data-ttu-id="25fb3-127">Существует два способа toocreate управляемого приложения с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="25fb3-127">There are two ways toocreate a managed application by using Azure CLI:</span></span>

* <span data-ttu-id="25fb3-128">Команда hello для создания управляемых приложений.</span><span class="sxs-lookup"><span data-stu-id="25fb3-128">Use hello command for creating managed applications.</span></span>
* <span data-ttu-id="25fb3-129">Команда hello обычным шаблоном развертывания.</span><span class="sxs-lookup"><span data-stu-id="25fb3-129">Use hello regular template deployment command.</span></span>

### <a name="use-hello-template-deployment-command"></a><span data-ttu-id="25fb3-130">Команда hello шаблон развертывания</span><span class="sxs-lookup"><span data-stu-id="25fb3-130">Use hello template deployment command</span></span>

<span data-ttu-id="25fb3-131">Развертывание файла applianceMainTemplate.json hello, hello поставщик создан.</span><span class="sxs-lookup"><span data-stu-id="25fb3-131">Deploy hello applianceMainTemplate.json file that hello vendor created.</span></span>

<span data-ttu-id="25fb3-132">Создайте две группы ресурсов:</span><span class="sxs-lookup"><span data-stu-id="25fb3-132">Then create two resource groups.</span></span> <span data-ttu-id="25fb3-133">Hello первая группа ресурсов находится где hello ресурсов управляемого приложения создается: Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="25fb3-133">hello first resource group is where hello managed application resource is created: Microsoft.Solutions/appliances.</span></span> <span data-ttu-id="25fb3-134">Hello вторая группа ресурсов содержит все ресурсы hello, определенные в mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="25fb3-134">hello second resource group contains all hello resources defined in mainTemplate.json.</span></span> <span data-ttu-id="25fb3-135">Эта группа ресурсов находится под управлением hello независимого поставщика программных Продуктов.</span><span class="sxs-lookup"><span data-stu-id="25fb3-135">This resource group is managed by hello ISV.</span></span>

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="25fb3-136">Используйте `westcentralus` как hello расположение группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="25fb3-136">Use `westcentralus` as hello location of hello resource group.</span></span>
>

<span data-ttu-id="25fb3-137">applianceMainTemplate.json toodeploy в mainResourceGroup hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="25fb3-137">toodeploy applianceMainTemplate.json in mainResourceGroup, use hello following command:</span></span>

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

<span data-ttu-id="25fb3-138">После hello предыдущих запусков шаблона он запрашивает hello значения параметров "hello", определенные в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="25fb3-138">After hello preceding template runs, it prompts you for hello values of hello parameters that are defined in hello template.</span></span> <span data-ttu-id="25fb3-139">В дополнение к этому toohello параметры, которые требуется tooprovision ресурсы в шаблоне, требуется два значения параметра ключа:</span><span class="sxs-lookup"><span data-stu-id="25fb3-139">In addition toohello parameters that are needed tooprovision resources in a template, you need two key parameter values:</span></span>

- <span data-ttu-id="25fb3-140">**managedResourceGroupId**: hello идентификатор hello ресурсов группы содержащего hello ресурсы, определенные в applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="25fb3-140">**managedResourceGroupId**: hello ID of hello resource group containing hello resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="25fb3-141">Идентификатор Hello имеет вид hello `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span><span class="sxs-lookup"><span data-stu-id="25fb3-141">hello ID is of hello form `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span></span> <span data-ttu-id="25fb3-142">В предыдущих пример hello, его идентификатор базы данных hello объекта `managedResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="25fb3-142">In hello preceding example, it's hello ID of `managedResourceGroup`.</span></span>
- <span data-ttu-id="25fb3-143">**applianceDefinitionId**: hello идентификатор hello управляемых определение ресурсов приложения.</span><span class="sxs-lookup"><span data-stu-id="25fb3-143">**applianceDefinitionId**: hello ID of hello managed application definition resource.</span></span> <span data-ttu-id="25fb3-144">Это значение предоставляется hello независимого поставщика программных Продуктов.</span><span class="sxs-lookup"><span data-stu-id="25fb3-144">This value is provided by hello ISV.</span></span>

> [!NOTE]
> <span data-ttu-id="25fb3-145">Hello издателя необходимо предоставить доступ toohello ресурсов группы, содержащей определение приложения hello управляемых.</span><span class="sxs-lookup"><span data-stu-id="25fb3-145">hello publisher must grant access toohello resource group that contains hello managed application definition.</span></span> <span data-ttu-id="25fb3-146">Определение ресурсов Hello создается в hello издателя подписки.</span><span class="sxs-lookup"><span data-stu-id="25fb3-146">hello definition resource is created in hello publisher subscription.</span></span> <span data-ttu-id="25fb3-147">Таким образом пользователя, группы пользователей или приложения в клиенте hello должен ресурсов toothis доступ для чтения.</span><span class="sxs-lookup"><span data-stu-id="25fb3-147">Therefore, a user, user group, or application in hello customer tenant needs read access toothis resource.</span></span>

<span data-ttu-id="25fb3-148">После успешного завершения развертывания hello вы видите hello управляемого приложения создается в mainResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="25fb3-148">After hello deployment finishes successfully, you see hello managed application is created in mainResourceGroup.</span></span> <span data-ttu-id="25fb3-149">Hello storageAccount ресурс создается в managedResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="25fb3-149">hello storageAccount resource is created in managedResourceGroup.</span></span>

### <a name="use-hello-create-command"></a><span data-ttu-id="25fb3-150">Hello используется команда «Создать»</span><span class="sxs-lookup"><span data-stu-id="25fb3-150">Use hello create command</span></span>

<span data-ttu-id="25fb3-151">Можно использовать hello `az managedapp create` команда toocreate управляемое приложение из hello управляемое определение приложения.</span><span class="sxs-lookup"><span data-stu-id="25fb3-151">You can use hello `az managedapp create` command toocreate a managed application from hello managed application definition.</span></span>

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* <span data-ttu-id="25fb3-152">**Идентификатор для определения устройства**: идентификатор ресурса hello hello управляемые определения приложения, созданные в предыдущих шага hello.</span><span class="sxs-lookup"><span data-stu-id="25fb3-152">**appliance-definition-Id**: hello resource ID of hello managed application definition created in hello preceding step.</span></span> <span data-ttu-id="25fb3-153">tooobtain этот идентификатор запуска hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="25fb3-153">tooobtain this ID, run hello following command:</span></span>

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  <span data-ttu-id="25fb3-154">Эта команда возвращает определение hello управляемого приложения.</span><span class="sxs-lookup"><span data-stu-id="25fb3-154">This command returns hello managed application definition.</span></span> <span data-ttu-id="25fb3-155">Необходимо получить значение hello hello идентификатор свойства.</span><span class="sxs-lookup"><span data-stu-id="25fb3-155">You need hello value of hello ID property.</span></span>

* <span data-ttu-id="25fb3-156">**управляемые rg-id**: hello имя hello ресурсов группы содержащего hello ресурсы, определенные в applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="25fb3-156">**managed-rg-id**: hello name of hello resource group containing hello resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="25fb3-157">Эта группа ресурсов находится группа hello управляемых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="25fb3-157">This resource group is hello managed resource group.</span></span> <span data-ttu-id="25fb3-158">Он управляет hello издателя.</span><span class="sxs-lookup"><span data-stu-id="25fb3-158">It's managed by hello publisher.</span></span> <span data-ttu-id="25fb3-159">Если эта группа не существует, она создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="25fb3-159">If it doesn't exist, it's created for you.</span></span>
* <span data-ttu-id="25fb3-160">**Группа ресурсов**: hello группа ресурсов, где hello управляемого ресурса приложения создается.</span><span class="sxs-lookup"><span data-stu-id="25fb3-160">**resource-group**: hello resource group where hello managed application resource is created.</span></span> <span data-ttu-id="25fb3-161">Hello ресурсов Microsoft.Solutions/appliance живет в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="25fb3-161">hello Microsoft.Solutions/appliance resource lives in this resource group.</span></span>
* <span data-ttu-id="25fb3-162">**Параметры**: hello параметры, необходимые для hello ресурсы, определенные в applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="25fb3-162">**parameters**: hello parameters that are needed for hello resources defined in applianceMainTemplate.json.</span></span>

## <a name="known-issues"></a><span data-ttu-id="25fb3-163">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="25fb3-163">Known issues</span></span>

<span data-ttu-id="25fb3-164">Эта предварительная версия включает hello следующих ситуаций:</span><span class="sxs-lookup"><span data-stu-id="25fb3-164">This preview release includes hello following issues:</span></span>

* <span data-ttu-id="25fb3-165">500 Внутренняя ошибка сервера отображается во время создания hello hello управляемого приложения.</span><span class="sxs-lookup"><span data-stu-id="25fb3-165">A 500 internal server error appears during hello creation of hello managed application.</span></span> <span data-ttu-id="25fb3-166">При возникновении этой проблемы, это скорее всего toobe временными.</span><span class="sxs-lookup"><span data-stu-id="25fb3-166">If you run into this issue, it's likely toobe intermittent.</span></span> <span data-ttu-id="25fb3-167">Повторите операцию hello.</span><span class="sxs-lookup"><span data-stu-id="25fb3-167">Retry hello operation.</span></span>
* <span data-ttu-id="25fb3-168">Для группы управляемых ресурсов hello требуется новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="25fb3-168">A new resource group is needed for hello managed resource group.</span></span> <span data-ttu-id="25fb3-169">Если используется существующая группа ресурсов, происходит сбой развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="25fb3-169">If you use an existing resource group, hello deployment fails.</span></span>
* <span data-ttu-id="25fb3-170">Hello группы ресурсов, содержащей hello Microsoft.Solutions/appliances ресурсов должны быть созданы в hello **westcentralus** расположение.</span><span class="sxs-lookup"><span data-stu-id="25fb3-170">hello resource group that contains hello Microsoft.Solutions/appliances resource must be created in hello **westcentralus** location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25fb3-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="25fb3-171">Next steps</span></span>

* <span data-ttu-id="25fb3-172">Введение toomanaged приложений, в разделе [Обзор управляемого приложения](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="25fb3-172">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="25fb3-173">Сведения о публикации управляемых приложений в каталоге услуг см. в разделе [Создание и публикация управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="25fb3-173">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="25fb3-174">Сведения о публикации toohello управляемые приложения Azure Marketplace см. в разделе [Azure управляемого приложения в hello Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="25fb3-174">For information about publishing managed applications toohello Azure Marketplace, see [Azure managed applications in hello Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="25fb3-175">Сведения о использование управляемого приложения из hello Marketplace в разделе [использовать Azure управляемого приложения в hello Marketplace](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="25fb3-175">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
