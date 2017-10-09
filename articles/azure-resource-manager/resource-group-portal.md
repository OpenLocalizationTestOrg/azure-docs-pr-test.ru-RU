---
title: "aaaUse Azure портала toomanage ресурсы Azure | Документы Microsoft"
description: "Используйте портал Azure и управление ресурсов Azure toomanage ресурсы. Показано, как toowork с ресурсами toomonitor панелей мониторинга."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0725bbf2-5913-4c07-af6e-24e11d957fbc
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 0c89a197a31c5b6dd03ba457cb4d1fdf9f6d00f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-resources-through-portal"></a><span data-ttu-id="f07aa-104">Управление ресурсами Azure через портал</span><span class="sxs-lookup"><span data-stu-id="f07aa-104">Manage Azure resources through portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f07aa-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f07aa-105">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="f07aa-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="f07aa-106">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="f07aa-107">Портал</span><span class="sxs-lookup"><span data-stu-id="f07aa-107">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="f07aa-108">REST API</span><span class="sxs-lookup"><span data-stu-id="f07aa-108">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="f07aa-109">В этом разделе показано, как toouse hello [портал Azure](https://portal.azure.com) с [диспетчера ресурсов Azure](resource-group-overview.md) toomanage ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="f07aa-109">This topic shows how toouse hello [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) toomanage your Azure resources.</span></span> <span data-ttu-id="f07aa-110">toolearn о развертывании ресурсы с помощью портала hello. в разделе [развертывания ресурсов с помощью шаблонов диспетчера ресурсов и портал Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f07aa-110">toolearn about deploying resources through hello portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>

<span data-ttu-id="f07aa-111">В настоящее время не каждая служба поддерживает hello портала или диспетчер ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f07aa-111">Currently, not every service supports hello portal or Resource Manager.</span></span> <span data-ttu-id="f07aa-112">Для этих служб требуется toouse hello [классический портал](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="f07aa-112">For those services, you need toouse hello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="f07aa-113">Состояние каждой службы hello см [диаграммы доступности Azure портала](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="f07aa-113">For hello status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="manage-resource-groups"></a><span data-ttu-id="f07aa-114">Управление группами ресурсов</span><span class="sxs-lookup"><span data-stu-id="f07aa-114">Manage resource groups</span></span>

<span data-ttu-id="f07aa-115">Группа ресурсов — это контейнер, содержащий связанные ресурсы для решения Azure.</span><span class="sxs-lookup"><span data-stu-id="f07aa-115">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="f07aa-116">Hello группы ресурсов может содержать все hello ресурсы для решения hello и доступны только те ресурсы, которые должны toomanage как группа.</span><span class="sxs-lookup"><span data-stu-id="f07aa-116">hello resource group can include all hello resources for hello solution, or only those resources that you want toomanage as a group.</span></span> <span data-ttu-id="f07aa-117">Можно выбрать способ tooallocate ресурсы группы tooresource основаны на то, что hello больше смысла для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="f07aa-117">You decide how you want tooallocate resources tooresource groups based on what makes hello most sense for your organization.</span></span> <span data-ttu-id="f07aa-118">Как правило, добавьте ресурсы, которые совместно используют hello же toohello жизненного цикла, сгруппировать того же ресурса, чтобы легко развертывать, обновлять и удалять их в группу.</span><span class="sxs-lookup"><span data-stu-id="f07aa-118">Generally, add resources that share hello same lifecycle toohello same resource group so you can easily deploy, update, and delete them as a group.</span></span> 

<span data-ttu-id="f07aa-119">Группа ресурсов Hello хранит метаданные о ресурсах hello.</span><span class="sxs-lookup"><span data-stu-id="f07aa-119">hello resource group stores metadata about hello resources.</span></span> <span data-ttu-id="f07aa-120">Таким образом при указании расположения для группы ресурсов hello указывается, где хранятся эти метаданные.</span><span class="sxs-lookup"><span data-stu-id="f07aa-120">Therefore, when you specify a location for hello resource group, you are specifying where that metadata is stored.</span></span> <span data-ttu-id="f07aa-121">Для обеспечения соответствия, может потребоваться tooensure, ваши данные сохранены в определенном регионе.</span><span class="sxs-lookup"><span data-stu-id="f07aa-121">For compliance reasons, you may need tooensure that your data is stored in a particular region.</span></span>

1. <span data-ttu-id="f07aa-122">Выберите все группы ресурсов hello в вашей подписке toosee **групп ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="f07aa-122">toosee all hello resource groups in your subscription, select **Resource groups**.</span></span>
   
    ![просмотр групп ресурсов](./media/resource-group-portal/browse-groups.png)
2. <span data-ttu-id="f07aa-124">Выберите toocreate группы пустой ресурсов **добавить**.</span><span class="sxs-lookup"><span data-stu-id="f07aa-124">toocreate an empty resource group, select **Add**.</span></span>
   
    ![добавление группы ресурсов](./media/resource-group-portal/add-resource-group.png)
3. <span data-ttu-id="f07aa-126">Укажите имя и расположение для новой группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="f07aa-126">Provide a name and location for hello new resource group.</span></span> <span data-ttu-id="f07aa-127">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f07aa-127">Select **Create**.</span></span>
   
    ![Создать группу ресурсов](./media/resource-group-portal/create-empty-group.png)
4. <span data-ttu-id="f07aa-129">Может потребоваться tooselect **обновление** группы ресурсов toosee hello создан недавно.</span><span class="sxs-lookup"><span data-stu-id="f07aa-129">You may need tooselect **Refresh** toosee hello recently created resource group.</span></span>
   
    ![обновление группы ресурсов](./media/resource-group-portal/refresh-resource-groups.png)
5. <span data-ttu-id="f07aa-131">Выберите toocustomize hello данные, отображаемые для вашей группы ресурсов **столбцы**.</span><span class="sxs-lookup"><span data-stu-id="f07aa-131">toocustomize hello information displayed for your resource groups, select **Columns**.</span></span>
   
    ![настройка столбцов](./media/resource-group-portal/select-columns.png)
6. <span data-ttu-id="f07aa-133">Выберите столбцы tooadd hello, а затем выберите **обновление**.</span><span class="sxs-lookup"><span data-stu-id="f07aa-133">Select hello columns tooadd, and then select **Update**.</span></span>
   
    ![добавление столбцов](./media/resource-group-portal/add-columns.png)
7. <span data-ttu-id="f07aa-135">toolearn о развертывании ресурсов tooyour новую группу ресурсов, в разделе [развертывания ресурсов с помощью шаблонов диспетчера ресурсов и портал Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f07aa-135">toolearn about deploying resources tooyour new resource group, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
8. <span data-ttu-id="f07aa-136">Для группы ресурсов tooa быстрого доступа можно закрепить панель tooyour колонке hello.</span><span class="sxs-lookup"><span data-stu-id="f07aa-136">For quick access tooa resource group, you can pin hello blade tooyour dashboard.</span></span>
   
    ![закрепление группы ресурсов](./media/resource-group-portal/pin-group.png)
9. <span data-ttu-id="f07aa-138">панель мониторинга Hello отображает hello группы ресурсов и его ресурсам.</span><span class="sxs-lookup"><span data-stu-id="f07aa-138">hello dashboard displays hello resource group and its resources.</span></span> <span data-ttu-id="f07aa-139">Можно выбрать hello группы ресурсов или любой из его элемент toohello toonavigate ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f07aa-139">You can select either hello resource groups or any of its resources toonavigate toohello item.</span></span>
   
    ![закрепление группы ресурсов](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a><span data-ttu-id="f07aa-141">Добавление тегов к ресурсам</span><span class="sxs-lookup"><span data-stu-id="f07aa-141">Tag resources</span></span>
<span data-ttu-id="f07aa-142">Можно применить теги tooresource групп и toologically ресурсы организации активов.</span><span class="sxs-lookup"><span data-stu-id="f07aa-142">You can apply tags tooresource groups and resources toologically organize your assets.</span></span> <span data-ttu-id="f07aa-143">Сведения о работе с тегами см. в разделе [использование теги tooorganize ресурсам Azure](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="f07aa-143">For information about working with tags, see [Using tags tooorganize your Azure resources](resource-group-using-tags.md).</span></span>

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a><span data-ttu-id="f07aa-144">Мониторинг ресурсов</span><span class="sxs-lookup"><span data-stu-id="f07aa-144">Monitor resources</span></span>
<span data-ttu-id="f07aa-145">При выборе ресурса колонки ресурсов hello предоставляет по умолчанию диаграмм и таблиц для отслеживания типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="f07aa-145">When you select a resource, hello resource blade presents default graphs and tables for monitoring that resource type.</span></span>

1. <span data-ttu-id="f07aa-146">Выберите ресурс и уведомление hello **мониторинг** раздела.</span><span class="sxs-lookup"><span data-stu-id="f07aa-146">Select a resource and notice hello **Monitoring** section.</span></span> <span data-ttu-id="f07aa-147">Он включает диаграммы, соответствующие toohello типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="f07aa-147">It includes graphs that are relevant toohello resource type.</span></span> <span data-ttu-id="f07aa-148">Hello рисунке показаны наблюдение за данными для учетной записи хранения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="f07aa-148">hello following image shows hello default monitoring data for a storage account.</span></span>
   
    ![показать мониторинг](./media/resource-group-portal/show-monitoring.png)
2. <span data-ttu-id="f07aa-150">Вы можете закрепить раздел hello колонке tooyour мониторинга, выбрав hello многоточие (...) над разделом hello.</span><span class="sxs-lookup"><span data-stu-id="f07aa-150">You can pin a section of hello blade tooyour dashboard by selecting hello ellipsis (...) above hello section.</span></span> <span data-ttu-id="f07aa-151">Можно также настроить раздел hello размер hello в колонке hello или полностью удалить.</span><span class="sxs-lookup"><span data-stu-id="f07aa-151">You can also customize hello size hello section in hello blade or remove it completely.</span></span> <span data-ttu-id="f07aa-152">Hello следующем рисунке показано, как toopin, настроить или удалить hello ЦП и памяти раздела.</span><span class="sxs-lookup"><span data-stu-id="f07aa-152">hello following image shows how toopin, customize, or remove hello CPU and Memory section.</span></span>
   
    ![закрепление раздела](./media/resource-group-portal/pin-cpu-section.png)
3. <span data-ttu-id="f07aa-154">После закрепления панели мониторинга toohello раздел hello, вы увидите hello сводки на панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="f07aa-154">After pinning hello section toohello dashboard, you will see hello summary on hello dashboard.</span></span> <span data-ttu-id="f07aa-155">И выбрав его сразу же осуществляется toomore подробные сведения о данных hello.</span><span class="sxs-lookup"><span data-stu-id="f07aa-155">And, selecting it immediately takes you toomore details about hello data.</span></span>
   
    ![просмотр панели мониторинга](./media/resource-group-portal/view-startboard.png)
4. <span data-ttu-id="f07aa-157">toocompletely настроить hello данные мониторинга через портал hello, перейдите на панель мониторинга по умолчанию tooyour и выберите **новая панель мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="f07aa-157">toocompletely customize hello data you monitor through hello portal, navigate tooyour default dashboard, and select **New dashboard**.</span></span>
   
    !["Веб-транзакции"](./media/resource-group-portal/dashboard.png)
5. <span data-ttu-id="f07aa-159">Присвойте имя новой информационной панели и перетащите плитки на панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="f07aa-159">Give your new dashboard a name and drag tiles onto hello dashboard.</span></span> <span data-ttu-id="f07aa-160">Плитка приветствия фильтруются по различные параметры.</span><span class="sxs-lookup"><span data-stu-id="f07aa-160">hello tiles are filtered by different options.</span></span>
   
    !["Веб-транзакции"](./media/resource-group-portal/create-dashboard.png)
   
     <span data-ttu-id="f07aa-162">в разделе toolearn о работе с панелями мониторинга, [Создание и совместное использование панели мониторинга на портал Azure hello](../azure-portal/azure-portal-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="f07aa-162">toolearn about working with dashboards, see [Creating and sharing dashboards in hello Azure portal](../azure-portal/azure-portal-dashboards.md).</span></span>

## <a name="manage-resources"></a><span data-ttu-id="f07aa-163">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="f07aa-163">Manage resources</span></span>
<span data-ttu-id="f07aa-164">В колонке hello для ресурса вы видите hello параметры для управления hello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f07aa-164">In hello blade for a resource, you see hello options for managing hello resource.</span></span> <span data-ttu-id="f07aa-165">портал Hello показывает возможности управления для этого определенного типа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f07aa-165">hello portal presents management options for that particular resource type.</span></span> <span data-ttu-id="f07aa-166">Команды управления hello разделе hello верхней части колонки ресурсов hello и левой стороны hello.</span><span class="sxs-lookup"><span data-stu-id="f07aa-166">You see hello management commands across hello top of hello resource blade and on hello left side.</span></span>

![Управление ресурсами](./media/resource-group-portal/manage-resources.png)

<span data-ttu-id="f07aa-168">Из этих параметров можно выполнять операции, такие как запуск и остановка виртуальной машины или повторной настройки свойств hello hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f07aa-168">From these options, you can perform operations such as starting and stopping a virtual machine, or reconfiguring hello properties of hello virtual machine.</span></span>

## <a name="move-resources"></a><span data-ttu-id="f07aa-169">Перемещение ресурсов</span><span class="sxs-lookup"><span data-stu-id="f07aa-169">Move resources</span></span>
<span data-ttu-id="f07aa-170">Группы ресурсов tooanother ресурсов toomove или другая подписка, в статье [переместить группу ресурсов toonew ресурсов или подписку](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="f07aa-170">If you need toomove resources tooanother resource group or another subscription, see [Move resources toonew resource group or subscription](resource-group-move-resources.md).</span></span>

## <a name="lock-resources"></a><span data-ttu-id="f07aa-171">Блокировка ресурсов</span><span class="sxs-lookup"><span data-stu-id="f07aa-171">Lock resources</span></span>
<span data-ttu-id="f07aa-172">Можно заблокировать подписки, группы ресурсов или ресурсов tooprevent другим пользователям в организации от случайного удаления или изменения критическим ресурсам.</span><span class="sxs-lookup"><span data-stu-id="f07aa-172">You can lock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="f07aa-173">Дополнительные сведения см. в статье [Блокировка ресурсов с помощью диспетчера ресурсов Azure](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="f07aa-173">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a><span data-ttu-id="f07aa-174">Просмотр сведений о подписке и затратах</span><span class="sxs-lookup"><span data-stu-id="f07aa-174">View your subscription and costs</span></span>
<span data-ttu-id="f07aa-175">Можно просмотреть сведения о подписке и hello сведенные затраты для всех ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f07aa-175">You can view information about your subscription and hello rolled-up costs for all your resources.</span></span> <span data-ttu-id="f07aa-176">Выберите **подписки** и вы хотите toosee подписки hello.</span><span class="sxs-lookup"><span data-stu-id="f07aa-176">Select **Subscriptions** and hello subscription you want toosee.</span></span> <span data-ttu-id="f07aa-177">Может иметь только один tooselect подписки.</span><span class="sxs-lookup"><span data-stu-id="f07aa-177">You might only have one subscription tooselect.</span></span>

![Подписка](./media/resource-group-portal/select-subscription.png)

<span data-ttu-id="f07aa-179">В колонке подписки hello видеть скорость темпа работ.</span><span class="sxs-lookup"><span data-stu-id="f07aa-179">Within hello subscription blade, you see a burn rate.</span></span>

![график расходов](./media/resource-group-portal/burn-rate.png)

<span data-ttu-id="f07aa-181">а также разбивка расходов по типам ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f07aa-181">And, a breakdown of costs by resource type.</span></span>

![стоимость ресурсов](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a><span data-ttu-id="f07aa-183">Экспорт шаблона</span><span class="sxs-lookup"><span data-stu-id="f07aa-183">Export template</span></span>
<span data-ttu-id="f07aa-184">После настройки группы ресурсов, вы можете шаблона диспетчера ресурсов hello tooview для группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="f07aa-184">After setting up your resource group, you may want tooview hello Resource Manager template for hello resource group.</span></span> <span data-ttu-id="f07aa-185">Экспорт шаблона hello имеет два преимущества:</span><span class="sxs-lookup"><span data-stu-id="f07aa-185">Exporting hello template offers two benefits:</span></span>

1. <span data-ttu-id="f07aa-186">Можно легко автоматизировать будущих развертываний hello решения, так как шаблон hello содержит все всей инфраструктурой hello.</span><span class="sxs-lookup"><span data-stu-id="f07aa-186">You can easily automate future deployments of hello solution because hello template contains all hello complete infrastructure.</span></span>
2. <span data-ttu-id="f07aa-187">Ознакомьтесь с синтаксисом шаблона, просмотрев hello JavaScript Object Notation (JSON), представляющий решения.</span><span class="sxs-lookup"><span data-stu-id="f07aa-187">You can become familiar with template syntax by looking at hello JavaScript Object Notation (JSON) that represents your solution.</span></span>

<span data-ttu-id="f07aa-188">Пошаговое руководство см. в статье [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md) (Экспорт шаблона Azure Resource Manager из существующих ресурсов).</span><span class="sxs-lookup"><span data-stu-id="f07aa-188">For step-by-step guidance, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

## <a name="delete-resource-group-or-resources"></a><span data-ttu-id="f07aa-189">Удаление ресурсов или группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="f07aa-189">Delete resource group or resources</span></span>
<span data-ttu-id="f07aa-190">При удалении группы ресурсов удаляет все hello ресурсы, содержащиеся в нем.</span><span class="sxs-lookup"><span data-stu-id="f07aa-190">Deleting a resource group deletes all hello resources contained within it.</span></span> <span data-ttu-id="f07aa-191">Из группы ресурсов можно также удалить отдельные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="f07aa-191">You can also delete individual resources within a resource group.</span></span> <span data-ttu-id="f07aa-192">Требуется tooexercise осторожны при удалении группы ресурсов, из-за возможной ресурсы в других групп ресурсов, связанных tooit.</span><span class="sxs-lookup"><span data-stu-id="f07aa-192">You want tooexercise caution when you delete a resource group because there might be resources in other resource groups that are linked tooit.</span></span> <span data-ttu-id="f07aa-193">Диспетчер ресурсов не приводит к удалению связанных ресурсов, но они могут не работать должным образом без hello ожидается ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f07aa-193">Resource Manager does not delete linked resources, but they may not operate correctly without hello expected resources.</span></span>

![удаление группы](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a><span data-ttu-id="f07aa-195">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f07aa-195">Next steps</span></span>
* <span data-ttu-id="f07aa-196">см. журналы действий tooview, [аудит операций с помощью диспетчера ресурсов](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="f07aa-196">tooview activity logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="f07aa-197">tooview сведения о состоянии развертывания см. [просмотреть операции развертывания](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="f07aa-197">tooview details about a deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="f07aa-198">ресурсы toodeploy через портал hello см [развертывания ресурсов с помощью шаблонов диспетчера ресурсов и портал Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f07aa-198">toodeploy resources through hello portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
* <span data-ttu-id="f07aa-199">tooresources toomanage доступ, в разделе [использовать tooyour роли назначения toomanage доступ к ресурсам подписки Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f07aa-199">toomanage access tooresources, see [Use role assignments toomanage access tooyour Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="f07aa-200">Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="f07aa-200">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

