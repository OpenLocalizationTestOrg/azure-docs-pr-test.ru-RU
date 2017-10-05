---
title: "Развертывание ресурсов Azure с помощью портала Azure | Документация Майкрософт"
description: "Узнайте, как использовать портал Azure для развертывания ресурсов и управления ими."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 2c98a4aa-8d9f-4a0a-b764-214dbe8ed009
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: a4cac5834c667976b0a2d1f2748e4309a166d16a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a><span data-ttu-id="4f3a6-103">Развертывание ресурсов с использованием шаблонов Resource Manager и портала Azure</span><span class="sxs-lookup"><span data-stu-id="4f3a6-103">Deploy resources with Resource Manager templates and Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4f3a6-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f3a6-104">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="4f3a6-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="4f3a6-105">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="4f3a6-106">Портал</span><span class="sxs-lookup"><span data-stu-id="4f3a6-106">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="4f3a6-107">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="4f3a6-107">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="4f3a6-108">В этой статье показано, как использовать [портал Azure](https://portal.azure.com) и [Azure Resource Manager](resource-group-overview.md) для развертывания ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-108">This topic shows how to use the [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) to deploy your Azure resources.</span></span> <span data-ttu-id="4f3a6-109">Сведения об управлении ресурсами см. в статье [Управление ресурсами Azure через портал](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4f3a6-109">To learn about managing your resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

<span data-ttu-id="4f3a6-110">В настоящее время не все службы поддерживают текущую версию портала или диспетчер ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-110">Currently, not every service supports the portal or Resource Manager.</span></span> <span data-ttu-id="4f3a6-111">Для некоторых служб необходимо использовать [классический портал](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="4f3a6-111">For those services, you need to use the [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="4f3a6-112">Состояние каждой службы можно просмотреть в [таблице доступности портала Azure](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="4f3a6-112">For the status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="4f3a6-113">Создать группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="4f3a6-113">Create resource group</span></span>
1. <span data-ttu-id="4f3a6-114">Чтобы создать пустую группу ресурсов, выберите **Создать** > **Управление** > **Группа ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-114">To create an empty resource group, select **New** > **Management** > **Resource Group**.</span></span>
   
    ![создание группы ресурсов](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. <span data-ttu-id="4f3a6-116">Укажите имя группы, ее расположение и при необходимости выберите подписку.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-116">Give it a name and location, and, if necessary, select a subscription.</span></span> <span data-ttu-id="4f3a6-117">Вам нужно указать расположение группы, так как она хранит метаданные ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-117">You need to provide a location for the resource group because the resource group stores metadata about the resources.</span></span> <span data-ttu-id="4f3a6-118">Для соответствия требованиям вам, возможно, нужно указать, где хранятся эти метаданные.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-118">For compliance reasons, you may want to specify where that metadata is stored.</span></span> <span data-ttu-id="4f3a6-119">Обычно мы рекомендуем указывать расположение, в котором будет храниться большинство ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-119">In general, we recommend that you specify a location where most of your resources will reside.</span></span> <span data-ttu-id="4f3a6-120">Используя одно и то же расположение, можно упростить шаблон.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-120">Using the same location can simplify your template.</span></span>
   
    ![настройка значений группы](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a><span data-ttu-id="4f3a6-122">Развертывание ресурсов из Marketplace</span><span class="sxs-lookup"><span data-stu-id="4f3a6-122">Deploy resources from Marketplace</span></span>
<span data-ttu-id="4f3a6-123">Создав группу ресурсов, вы можете развернуть в ней ресурсы из Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-123">After you create a resource group, you can deploy resources to it from the Marketplace.</span></span> <span data-ttu-id="4f3a6-124">Marketplace предоставляет предварительно определенные решения для распространенных сценариев использования.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-124">The Marketplace provides pre-defined solutions for common scenarios.</span></span>

1. <span data-ttu-id="4f3a6-125">Чтобы начать развертывание, щелкните **Создать** и выберите тип ресурса, который хотите развернуть.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-125">To start a deployment, select **New** and the type of resource you would like to deploy.</span></span> <span data-ttu-id="4f3a6-126">Затем найдите определенную версию ресурса, которую требуется развернуть.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-126">Then, look for the particular version of the resource you would like to deploy.</span></span>
   
    ![развертывание ресурсов](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. <span data-ttu-id="4f3a6-128">Если конкретное решение, которое вы хотите развернуть, отсутствует, его можно поискать в Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-128">If you do not see the particular solution you would like to deploy, you can search the Marketplace for it.</span></span>
   
    ![поиск в Marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. <span data-ttu-id="4f3a6-130">В зависимости от выбранного типа ресурса вам потребуется задать набор соответствующих свойств, прежде чем начинать развертывание.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-130">Depending on the type of selected resource, you have a collection of relevant properties to set before deployment.</span></span> <span data-ttu-id="4f3a6-131">Здесь эти свойства не показаны, так как они варьируются в зависимости от типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-131">Those options are not shown here, as they vary based on resource type.</span></span> <span data-ttu-id="4f3a6-132">Для всех типов необходимо выбрать целевую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-132">For all types, you must select a destination resource group.</span></span> <span data-ttu-id="4f3a6-133">Ниже показано создание веб-приложения и его развертывание в уже созданной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-133">The following image shows how to create a web app and deploy it to the resource group you created.</span></span>
   
    ![Создать группу ресурсов](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    <span data-ttu-id="4f3a6-135">Кроме того, можно создать новую группу ресурсов непосредственно при развертывании ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-135">Alternatively, you can decide to create a resource group when deploying your resources.</span></span> <span data-ttu-id="4f3a6-136">Щелкните **Создать** и укажите имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-136">Select **Create new** and give the resource group a name.</span></span>
   
    ![создание новой группы ресурсов](./media/resource-group-template-deploy-portal/select-new-group.png)
4. <span data-ttu-id="4f3a6-138">Начнется развертывание.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-138">Your deployment begins.</span></span> <span data-ttu-id="4f3a6-139">Это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-139">The deployment could take a few minutes.</span></span> <span data-ttu-id="4f3a6-140">По окончании развертывания появится уведомление.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-140">When the deployment has finished, you see a notification.</span></span>
   
    ![просмотр уведомления](./media/resource-group-template-deploy-portal/view-notification.png)
5. <span data-ttu-id="4f3a6-142">Развернув ресурсы, вы можете добавлять в группу другие ресурсы с помощью команды **Добавить** в колонке этой группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-142">After deploying your resources, you can add more resources to the resource group by using the **Add** command on the resource group blade.</span></span>
   
    ![Добавить ресурсы](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a><span data-ttu-id="4f3a6-144">Развертывание ресурсов с помощью настраиваемого шаблона</span><span class="sxs-lookup"><span data-stu-id="4f3a6-144">Deploy resources from custom template</span></span>
<span data-ttu-id="4f3a6-145">Если вы хотите выполнить развертывание без использования шаблонов из Marketplace, создайте настраиваемый шаблон, определяющий инфраструктуру для вашего решения.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-145">If you want to execute a deployment but not use any of the templates in the Marketplace, you can create a customized template that defines the infrastructure for your solution.</span></span> <span data-ttu-id="4f3a6-146">Сведения о создании шаблонов см. в статье [Создание шаблонов диспетчера ресурсов Azure](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4f3a6-146">To learn about creating templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

1. <span data-ttu-id="4f3a6-147">Чтобы развернуть настроенный шаблон на портале, выберите **Создать** и начните поиск по словам **Развертывание шаблона**, пока не появится соответствующий пункт.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-147">To deploy a customized template through the portal, select **New**, and start searching for **Template Deployment** until you can select it from the options.</span></span>
   
    ![поиск развертывания шаблона](./media/resource-group-template-deploy-portal/search-template.png)
2. <span data-ttu-id="4f3a6-149">В списке доступных ресурсов выберите **Развертывание шаблона** .</span><span class="sxs-lookup"><span data-stu-id="4f3a6-149">Select **Template Deployment** from the available resources.</span></span>
   
    ![выберите "развертывание шаблона"](./media/resource-group-template-deploy-portal/select-template.png)
3. <span data-ttu-id="4f3a6-151">После запуска развертывания шаблона откройте пустой шаблон, доступный для настройки.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-151">After launching the template deployment, open the blank template that is available for customizing.</span></span>
   
    ![создание шаблона](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    <span data-ttu-id="4f3a6-153">В редакторе добавьте данные в формате JSON, определяющие ресурсы, которые требуется развернуть.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-153">In the editor, add the JSON syntax that defines the resources you want to deploy.</span></span> <span data-ttu-id="4f3a6-154">По завершении нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-154">Select **Save** when done.</span></span> <span data-ttu-id="4f3a6-155">Рекомендации по созданию данных в формате JSON см. в [пошаговом руководстве по созданию шаблона Resource Manager](resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="4f3a6-155">For guidance on writing the JSON syntax, see [Resource Manager template walkthrough](resource-manager-template-walkthrough.md).</span></span>
   
    ![изменение шаблона](./media/resource-group-template-deploy-portal/edit-template.png)
4. <span data-ttu-id="4f3a6-157">Кроме того, можно выбрать готовый шаблон на странице [шаблонов быстрого запуска Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="4f3a6-157">Or, you can select a pre-existing template from the [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="4f3a6-158">Эти шаблоны предоставлены сообществом.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-158">These templates are contributed by the community.</span></span> <span data-ttu-id="4f3a6-159">Они охватывают множество распространенных сценариев, а кто-то мог добавить шаблон, который подходит и вам.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-159">They cover many common scenarios, and someone may have added a template that is similar to what you are trying to deploy.</span></span> <span data-ttu-id="4f3a6-160">Выполните поиск, чтобы найти шаблон, соответствующий вашему сценарию.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-160">You can search the templates to find something that matches your scenario.</span></span>
   
    ![выбор шаблона быстрого запуска](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    <span data-ttu-id="4f3a6-162">Выбранный шаблон можно просмотреть в редакторе.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-162">You can view the selected template in the editor.</span></span>
5. <span data-ttu-id="4f3a6-163">Указав все остальные значения, нажмите кнопку **Создать** , чтобы развернуть шаблон.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-163">After providing all the other values, select **Create** to deploy the template.</span></span> 
   
    ![развертывание шаблона](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-to-your-account"></a><span data-ttu-id="4f3a6-165">Развертывание ресурсов с помощью шаблона, сохраненного в учетной записи</span><span class="sxs-lookup"><span data-stu-id="4f3a6-165">Deploy resources from a template saved to your account</span></span>
<span data-ttu-id="4f3a6-166">Портал позволяет сохранить шаблон в свою учетную запись Azure для последующего повторного развертывания.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-166">The portal enables you to save a template to your Azure account, and redeploy it later.</span></span> <span data-ttu-id="4f3a6-167">Дополнительные сведения о работе с сохраненными шаблонами см. в статье [Начало работы с частными шаблонами на портале Azure](../marketplace-consumer/mytemplates-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="4f3a6-167">For more information about working with these saved templates, [Get started with private templates on the Azure portal](../marketplace-consumer/mytemplates-getstarted.md).</span></span>

1. <span data-ttu-id="4f3a6-168">Чтобы найти сохраненные шаблоны, выберите **Обзор** > **Шаблоны**.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-168">To find your saved templates, select **Browse** > **Templates**.</span></span>
   
    ![просмотр шаблонов](./media/resource-group-template-deploy-portal/browse-templates.png)
2. <span data-ttu-id="4f3a6-170">Из списка шаблонов, сохраненных в вашей учетной записи, выберите тот, с которым вы хотите работать.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-170">From the list of templates saved to your account, select the one you wish to work on.</span></span>
   
    ![сохраненные шаблоны](./media/resource-group-template-deploy-portal/saved-templates.png)
3. <span data-ttu-id="4f3a6-172">Нажмите кнопку **Развернуть** , чтобы повторно развернуть этот сохраненный шаблон.</span><span class="sxs-lookup"><span data-stu-id="4f3a6-172">Select **Deploy** to redeploy this saved template.</span></span>
   
    ![развертывание сохраненного шаблона](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a><span data-ttu-id="4f3a6-174">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4f3a6-174">Next steps</span></span>
* <span data-ttu-id="4f3a6-175">Сведения о просмотре журналов аудита см. в статье [Операции аудита с помощью Resource Manager](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="4f3a6-175">To view audit logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="4f3a6-176">Сведения об устранении неполадок развертывания см. в статье [Просмотр операций развертывания с помощью Azure Resource Manager](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="4f3a6-176">To troubleshoot deployment errors, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="4f3a6-177">Чтобы извлечь шаблон из развернутой службы или группы ресурсов, ознакомьтесь со статьей [Экспорт шаблона Azure Resource Manager из существующих ресурсов](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="4f3a6-177">To retrieve a template from a deployment or resource group, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="4f3a6-178">Руководство по использованию Resource Manager для эффективного управления подписками в организациях см [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Шаблон Azure для организаций. Рекомендуемая система управления подпиской).</span><span class="sxs-lookup"><span data-stu-id="4f3a6-178">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

