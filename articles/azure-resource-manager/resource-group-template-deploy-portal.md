---
title: "aaaUse Azure портала toodeploy ресурсы Azure | Документы Microsoft"
description: "Используйте портал Azure и управление ресурсов Azure toodeploy ресурсы."
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
ms.openlocfilehash: 5a5217f94c8dfc0c1ebd613903ea3dcbe1197bfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a><span data-ttu-id="20646-103">Развертывание ресурсов с использованием шаблонов Resource Manager и портала Azure</span><span class="sxs-lookup"><span data-stu-id="20646-103">Deploy resources with Resource Manager templates and Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="20646-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="20646-104">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="20646-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="20646-105">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="20646-106">Портал</span><span class="sxs-lookup"><span data-stu-id="20646-106">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="20646-107">REST API</span><span class="sxs-lookup"><span data-stu-id="20646-107">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="20646-108">В этом разделе показано, как toouse hello [портал Azure](https://portal.azure.com) с [диспетчера ресурсов Azure](resource-group-overview.md) toodeploy ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="20646-108">This topic shows how toouse hello [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) toodeploy your Azure resources.</span></span> <span data-ttu-id="20646-109">в разделе toolearn об управлении вашими ресурсами, [ресурсы с помощью портала управления Azure](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="20646-109">toolearn about managing your resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

<span data-ttu-id="20646-110">В настоящее время не каждая служба поддерживает hello портала или диспетчер ресурсов.</span><span class="sxs-lookup"><span data-stu-id="20646-110">Currently, not every service supports hello portal or Resource Manager.</span></span> <span data-ttu-id="20646-111">Для этих служб требуется toouse hello [классический портал](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="20646-111">For those services, you need toouse hello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="20646-112">Состояние каждой службы hello см [диаграммы доступности Azure портала](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="20646-112">For hello status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="20646-113">Создать группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="20646-113">Create resource group</span></span>
1. <span data-ttu-id="20646-114">Выберите toocreate группы пустой ресурсов **New** > **управления** > **группы ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="20646-114">toocreate an empty resource group, select **New** > **Management** > **Resource Group**.</span></span>
   
    ![создание группы ресурсов](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. <span data-ttu-id="20646-116">Укажите имя группы, ее расположение и при необходимости выберите подписку.</span><span class="sxs-lookup"><span data-stu-id="20646-116">Give it a name and location, and, if necessary, select a subscription.</span></span> <span data-ttu-id="20646-117">Tooprovide расположение группы ресурсов hello необходимо потому, что группа ресурсов hello хранит метаданные о ресурсах hello.</span><span class="sxs-lookup"><span data-stu-id="20646-117">You need tooprovide a location for hello resource group because hello resource group stores metadata about hello resources.</span></span> <span data-ttu-id="20646-118">В целях соответствия требованиям можно toospecify, где хранятся эти метаданные.</span><span class="sxs-lookup"><span data-stu-id="20646-118">For compliance reasons, you may want toospecify where that metadata is stored.</span></span> <span data-ttu-id="20646-119">Обычно мы рекомендуем указывать расположение, в котором будет храниться большинство ресурсов.</span><span class="sxs-lookup"><span data-stu-id="20646-119">In general, we recommend that you specify a location where most of your resources will reside.</span></span> <span data-ttu-id="20646-120">С помощью hello же расположение можно упростить шаблон.</span><span class="sxs-lookup"><span data-stu-id="20646-120">Using hello same location can simplify your template.</span></span>
   
    ![настройка значений группы](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a><span data-ttu-id="20646-122">Развертывание ресурсов из Marketplace</span><span class="sxs-lookup"><span data-stu-id="20646-122">Deploy resources from Marketplace</span></span>
<span data-ttu-id="20646-123">После создания группы ресурсов, можно развернуть tooit ресурсы из hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="20646-123">After you create a resource group, you can deploy resources tooit from hello Marketplace.</span></span> <span data-ttu-id="20646-124">Hello Marketplace предоставляет предопределенные решения для распространенных сценариев.</span><span class="sxs-lookup"><span data-stu-id="20646-124">hello Marketplace provides pre-defined solutions for common scenarios.</span></span>

1. <span data-ttu-id="20646-125">Выберите toostart развертывания, **New** и hello тип ресурса хотелось бы toodeploy.</span><span class="sxs-lookup"><span data-stu-id="20646-125">toostart a deployment, select **New** and hello type of resource you would like toodeploy.</span></span> <span data-ttu-id="20646-126">Затем найдите для конкретной версии ресурса hello hello хотелось бы toodeploy.</span><span class="sxs-lookup"><span data-stu-id="20646-126">Then, look for hello particular version of hello resource you would like toodeploy.</span></span>
   
    ![развертывание ресурсов](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. <span data-ttu-id="20646-128">Если требуется toodeploy конкретного решения hello не отображается, можно искать hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="20646-128">If you do not see hello particular solution you would like toodeploy, you can search hello Marketplace for it.</span></span>
   
    ![поиск в Marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. <span data-ttu-id="20646-130">В зависимости от типа выбранного ресурса hello есть коллекция tooset соответствующие свойства перед развертыванием.</span><span class="sxs-lookup"><span data-stu-id="20646-130">Depending on hello type of selected resource, you have a collection of relevant properties tooset before deployment.</span></span> <span data-ttu-id="20646-131">Здесь эти свойства не показаны, так как они варьируются в зависимости от типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="20646-131">Those options are not shown here, as they vary based on resource type.</span></span> <span data-ttu-id="20646-132">Для всех типов необходимо выбрать целевую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="20646-132">For all types, you must select a destination resource group.</span></span> <span data-ttu-id="20646-133">Hello следующем рисунке показано, как toocreate веб-приложение и развернуть ее toohello группы ресурсов, вы создали.</span><span class="sxs-lookup"><span data-stu-id="20646-133">hello following image shows how toocreate a web app and deploy it toohello resource group you created.</span></span>
   
    ![Создать группу ресурсов](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    <span data-ttu-id="20646-135">Кроме того можно решить toocreate группы ресурсов, при развертывании имеющихся ресурсов.</span><span class="sxs-lookup"><span data-stu-id="20646-135">Alternatively, you can decide toocreate a resource group when deploying your resources.</span></span> <span data-ttu-id="20646-136">Выберите **создать новый** и присвойте имя группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="20646-136">Select **Create new** and give hello resource group a name.</span></span>
   
    ![создание новой группы ресурсов](./media/resource-group-template-deploy-portal/select-new-group.png)
4. <span data-ttu-id="20646-138">Начнется развертывание.</span><span class="sxs-lookup"><span data-stu-id="20646-138">Your deployment begins.</span></span> <span data-ttu-id="20646-139">Hello развертывания может потребоваться несколько минут.</span><span class="sxs-lookup"><span data-stu-id="20646-139">hello deployment could take a few minutes.</span></span> <span data-ttu-id="20646-140">После завершения развертывания hello, появится уведомление.</span><span class="sxs-lookup"><span data-stu-id="20646-140">When hello deployment has finished, you see a notification.</span></span>
   
    ![просмотр уведомления](./media/resource-group-template-deploy-portal/view-notification.png)
5. <span data-ttu-id="20646-142">После развертывания ресурсов, можно добавить дополнительные группы ресурсов toohello ресурсов с помощью hello **добавить** команду колонки группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="20646-142">After deploying your resources, you can add more resources toohello resource group by using hello **Add** command on hello resource group blade.</span></span>
   
    ![Добавить ресурсы](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a><span data-ttu-id="20646-144">Развертывание ресурсов с помощью настраиваемого шаблона</span><span class="sxs-lookup"><span data-stu-id="20646-144">Deploy resources from custom template</span></span>
<span data-ttu-id="20646-145">Если требуется tooexecute развертывания, но использование шаблонов hello в hello Marketplace, можно создать настраиваемый шаблон, определяющий hello инфраструктуры для вашего решения.</span><span class="sxs-lookup"><span data-stu-id="20646-145">If you want tooexecute a deployment but not use any of hello templates in hello Marketplace, you can create a customized template that defines hello infrastructure for your solution.</span></span> <span data-ttu-id="20646-146">в разделе toolearn о создании шаблонов, [шаблоны разработки Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="20646-146">toolearn about creating templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

1. <span data-ttu-id="20646-147">Выберите настроенный шаблон через портал hello toodeploy **New**и начинается поиск **развертывания шаблона** пока можно выбрать его из вариантов hello.</span><span class="sxs-lookup"><span data-stu-id="20646-147">toodeploy a customized template through hello portal, select **New**, and start searching for **Template Deployment** until you can select it from hello options.</span></span>
   
    ![поиск развертывания шаблона](./media/resource-group-template-deploy-portal/search-template.png)
2. <span data-ttu-id="20646-149">Выберите **развертывания шаблона** из доступных ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="20646-149">Select **Template Deployment** from hello available resources.</span></span>
   
    ![выберите "развертывание шаблона"](./media/resource-group-template-deploy-portal/select-template.png)
3. <span data-ttu-id="20646-151">После запуска развертывания шаблона hello, откройте пустой шаблон hello, доступные для настройки.</span><span class="sxs-lookup"><span data-stu-id="20646-151">After launching hello template deployment, open hello blank template that is available for customizing.</span></span>
   
    ![создание шаблона](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    <span data-ttu-id="20646-153">В редакторе hello добавьте hello синтаксис JSON, который определяет ресурсы hello требуется toodeploy.</span><span class="sxs-lookup"><span data-stu-id="20646-153">In hello editor, add hello JSON syntax that defines hello resources you want toodeploy.</span></span> <span data-ttu-id="20646-154">По завершении нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="20646-154">Select **Save** when done.</span></span> <span data-ttu-id="20646-155">Рекомендации по написанию синтаксис JSON hello. в разделе [Пошаговое руководство диспетчера ресурсов шаблона](resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="20646-155">For guidance on writing hello JSON syntax, see [Resource Manager template walkthrough](resource-manager-template-walkthrough.md).</span></span>
   
    ![изменение шаблона](./media/resource-group-template-deploy-portal/edit-template.png)
4. <span data-ttu-id="20646-157">Или можно выбрать существующий шаблон из hello [шаблоны Azure краткое руководство](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="20646-157">Or, you can select a pre-existing template from hello [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="20646-158">Эти шаблоны предоставляются hello сообщества.</span><span class="sxs-lookup"><span data-stu-id="20646-158">These templates are contributed by hello community.</span></span> <span data-ttu-id="20646-159">Они охватывают многих распространенных сценариев и кто-то добавить шаблон, аналогичные toowhat вы пытаетесь toodeploy.</span><span class="sxs-lookup"><span data-stu-id="20646-159">They cover many common scenarios, and someone may have added a template that is similar toowhat you are trying toodeploy.</span></span> <span data-ttu-id="20646-160">Toofind hello шаблоны можно найти что-нибудь, соответствующий вашему сценарию.</span><span class="sxs-lookup"><span data-stu-id="20646-160">You can search hello templates toofind something that matches your scenario.</span></span>
   
    ![выбор шаблона быстрого запуска](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    <span data-ttu-id="20646-162">Выбранный шаблон hello можно просмотреть в редакторе hello.</span><span class="sxs-lookup"><span data-stu-id="20646-162">You can view hello selected template in hello editor.</span></span>
5. <span data-ttu-id="20646-163">После предоставления hello все другие значения, выберите **создать** toodeploy hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="20646-163">After providing all hello other values, select **Create** toodeploy hello template.</span></span> 
   
    ![развертывание шаблона](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-tooyour-account"></a><span data-ttu-id="20646-165">Развертывание ресурсов на основе шаблона, сохранить tooyour учетной записи</span><span class="sxs-lookup"><span data-stu-id="20646-165">Deploy resources from a template saved tooyour account</span></span>
<span data-ttu-id="20646-166">портал Hello включает toosave шаблона tooyour учетная запись Azure и повторно развернуть позже.</span><span class="sxs-lookup"><span data-stu-id="20646-166">hello portal enables you toosave a template tooyour Azure account, and redeploy it later.</span></span> <span data-ttu-id="20646-167">Дополнительные сведения о работе с шаблонами, сохраненных [приступить к работе с шаблонами закрытого на портал Azure hello](../marketplace-consumer/mytemplates-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="20646-167">For more information about working with these saved templates, [Get started with private templates on hello Azure portal](../marketplace-consumer/mytemplates-getstarted.md).</span></span>

1. <span data-ttu-id="20646-168">Выберите шаблонами сохраненного toofind **Обзор** > **шаблоны**.</span><span class="sxs-lookup"><span data-stu-id="20646-168">toofind your saved templates, select **Browse** > **Templates**.</span></span>
   
    ![просмотр шаблонов](./media/resource-group-template-deploy-portal/browse-templates.png)
2. <span data-ttu-id="20646-170">Выберите из списка hello шаблонов сохранены tooyour учетной записи, с которой вы хотите toowork на hello.</span><span class="sxs-lookup"><span data-stu-id="20646-170">From hello list of templates saved tooyour account, select hello one you wish toowork on.</span></span>
   
    ![сохраненные шаблоны](./media/resource-group-template-deploy-portal/saved-templates.png)
3. <span data-ttu-id="20646-172">Выберите **развернуть** tooredeploy сохранен шаблон.</span><span class="sxs-lookup"><span data-stu-id="20646-172">Select **Deploy** tooredeploy this saved template.</span></span>
   
    ![развертывание сохраненного шаблона](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a><span data-ttu-id="20646-174">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="20646-174">Next steps</span></span>
* <span data-ttu-id="20646-175">см. журналы аудита tooview, [аудит операций с помощью диспетчера ресурсов](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="20646-175">tooview audit logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="20646-176">tootroubleshoot ошибок развертывания, в разделе [просмотреть операции развертывания](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="20646-176">tootroubleshoot deployment errors, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="20646-177">tooretrieve шаблона из развертывания или группы ресурсов, в разделе [Экспорт шаблона диспетчера ресурсов Azure с существующие ресурсы](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="20646-177">tooretrieve a template from a deployment or resource group, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="20646-178">Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="20646-178">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

