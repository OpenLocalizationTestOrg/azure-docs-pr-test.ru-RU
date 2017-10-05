---
title: "Отслеживать работоспособность и оповещений в стек Azure | Документы Microsoft"
description: "Узнайте, как для мониторинга работоспособности и предупреждений в стек Azure."
services: azure-stack
documentationcenter: 
author: chasat-MS
manager: dsavage
editor: 
ms.assetid: 69901c7b-4673-4bd8-acf2-8c6bdd9d1546
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: chasat
ms.openlocfilehash: 93835eabcf9622735aada0f5dfa46028553c25bd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="monitor-health-and-alerts-in-azure-stack"></a><span data-ttu-id="cf111-103">Монитор работоспособности и предупреждений в стек Azure</span><span class="sxs-lookup"><span data-stu-id="cf111-103">Monitor health and alerts in Azure Stack</span></span>

<span data-ttu-id="cf111-104">Стек Azure включает в себя возможности, позволяющие оператор облака для просмотра работоспособности и предупреждений для области стека Azure мониторинг инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="cf111-104">Azure Stack includes infrastructure monitoring capabilities that enable a cloud operator to view health and alerts for an Azure Stack region.</span></span>

<span data-ttu-id="cf111-105">Стек Azure имеет набор возможностей управления области, доступные в **область управления** плитки.</span><span class="sxs-lookup"><span data-stu-id="cf111-105">Azure Stack has a set of region management capabilities available in the **Region management** tile.</span></span> <span data-ttu-id="cf111-106">Этой плитки, закрепленные по умолчанию на портале администратора для подписки поставщика по умолчанию, список всех развернутых областей Azure стека.</span><span class="sxs-lookup"><span data-stu-id="cf111-106">This tile, pinned by default in the administrator portal for the Default Provider Subscription, lists all the deployed regions of Azure Stack.</span></span> <span data-ttu-id="cf111-107">Также показывает число активные предупреждения и критические оповещения для каждого региона.</span><span class="sxs-lookup"><span data-stu-id="cf111-107">It also shows the count of active critical and warning alerts for each region.</span></span> <span data-ttu-id="cf111-108">Эта Плитка представляет точку входа в функцию работоспособности и предупреждений стек Azure.</span><span class="sxs-lookup"><span data-stu-id="cf111-108">This tile is your entry point into the health and alert functionality of Azure Stack.</span></span>

 ![Область управления плитки](media/azure-stack-monitor-health/image1.png)

 ## <a name="understand-health-in-azure-stack"></a><span data-ttu-id="cf111-110">Понимание работоспособности в стек Azure</span><span class="sxs-lookup"><span data-stu-id="cf111-110">Understand health in Azure Stack</span></span>

 <span data-ttu-id="cf111-111">Оповещения и работоспособности осуществляется в стек Azure поставщиком ресурсов работоспособности.</span><span class="sxs-lookup"><span data-stu-id="cf111-111">Health and alerts are managed in Azure Stack by the Health resource provider.</span></span> <span data-ttu-id="cf111-112">Компоненты инфраструктуры Azure стека зарегистрировать поставщик ресурсов работоспособности во время развертывания стека Azure и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="cf111-112">Azure Stack infrastructure components register with the Health resource provider during Azure Stack deployment and configuration.</span></span> <span data-ttu-id="cf111-113">Регистрация позволяет отображение работоспособности и предупреждений для каждого компонента.</span><span class="sxs-lookup"><span data-stu-id="cf111-113">This registration enables the display of health and alerts for each component.</span></span> <span data-ttu-id="cf111-114">Работоспособность стека Azure — это простое понятие.</span><span class="sxs-lookup"><span data-stu-id="cf111-114">Health in Azure Stack is a simple concept.</span></span> <span data-ttu-id="cf111-115">Если существует предупреждения для зарегистрированных экземпляров компонента, состояние работоспособности компонента отражает наихудшее active серьезность оповещения; Предупреждение или критическое.</span><span class="sxs-lookup"><span data-stu-id="cf111-115">If alerts for a registered instance of a component exist, the health state of that component reflects the worst active alert severity; warning, or critical.</span></span>
 
 ## <a name="view-and-manage-component-health-state"></a><span data-ttu-id="cf111-116">Просмотр и управление состояние работоспособности компонента</span><span class="sxs-lookup"><span data-stu-id="cf111-116">View and manage component health state</span></span>
 
 <span data-ttu-id="cf111-117">Можно просмотреть состояние работоспособности компонентов в обоих портал администратора Azure стека и с помощью Rest API и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cf111-117">You can view the health state of components in both the Azure Stack administrator portal and through Rest API and PowerShell.</span></span>
 
<span data-ttu-id="cf111-118">Чтобы просмотреть состояние работоспособности на портале, щелкните область, для просмотра в **область управления** плитки.</span><span class="sxs-lookup"><span data-stu-id="cf111-118">To view the health state in the portal, click the region that you want to view in the **Region management** tile.</span></span> <span data-ttu-id="cf111-119">Можно просмотреть состояние работоспособности инфраструктуры ролей и поставщиков ресурсов.</span><span class="sxs-lookup"><span data-stu-id="cf111-119">You can view the health state of infrastructure roles and of resource providers.</span></span> <span data-ttu-id="cf111-120">Обратите внимание, что в этом выпуске поставщика ресурсов вычислений не сообщает состояние работоспособности.</span><span class="sxs-lookup"><span data-stu-id="cf111-120">Note that in this release, the Compute resource provider does not report health state.</span></span>

![Список ролей инфраструктуры](media/azure-stack-monitor-health/image2.png)

<span data-ttu-id="cf111-122">Можно щелкнуть поставщика ресурсов или роли инфраструктуры для просмотра подробных сведений.</span><span class="sxs-lookup"><span data-stu-id="cf111-122">You can click a resource provider or infrastructure role to view more detailed information.</span></span>

> [!WARNING]
><span data-ttu-id="cf111-123">Если вы щелкните роль инфраструктуры и выберите экземпляр роли, существуют варианты в **экземпляра роли** колонку для начала, перезагрузка или завершение работы.</span><span class="sxs-lookup"><span data-stu-id="cf111-123">If you click an infrastructure role, and then click the role instance, there are options in the **Role instance** blade to Start, Restart, or Shutdown.</span></span> <span data-ttu-id="cf111-124">Сделать **не** эти параметры используются в среде Azure стека Development Kit.</span><span class="sxs-lookup"><span data-stu-id="cf111-124">Do **not** use these options in an Azure Stack Development Kit environment.</span></span> <span data-ttu-id="cf111-125">Эти параметры предназначены только для среды с несколькими узлами, где имеется более одного экземпляра роли на каждую роль службы инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="cf111-125">These options are designed only for a multi-node environment, where there is more than one role instance per infrastructure role.</span></span> <span data-ttu-id="cf111-126">Экземпляр роли (особенно AzS-Xrp01) в пакете средств разработки при перезапуске нестабильность системы.</span><span class="sxs-lookup"><span data-stu-id="cf111-126">Restarting a role instance (especially AzS-Xrp01) in the development kit causes system instability.</span></span> <span data-ttu-id="cf111-127">Сведения об устранении неполадок, можно оставить в ошибке в [форум Azure стека](https://aka.ms/azurestackforum).</span><span class="sxs-lookup"><span data-stu-id="cf111-127">For troubleshooting assistance, please post your issue to the [Azure Stack forum](https://aka.ms/azurestackforum).</span></span>
>
 
## <a name="view-alerts"></a><span data-ttu-id="cf111-128">Просмотр оповещений</span><span class="sxs-lookup"><span data-stu-id="cf111-128">View alerts</span></span>

<span data-ttu-id="cf111-129">Список активных оповещений для каждого региона Azure стека доступен непосредственно из **область управления** колонку.</span><span class="sxs-lookup"><span data-stu-id="cf111-129">The list of active alerts for each Azure Stack region is available directly from the **Region management** blade.</span></span> <span data-ttu-id="cf111-130">Первый фрагмент в конфигурации по умолчанию — **оповещения** плитку, которая отображает сводку по критически важные и предупреждающие оповещения для области.</span><span class="sxs-lookup"><span data-stu-id="cf111-130">The first tile in the default configuration is the **Alerts** tile, which displays a summary of the critical and warning alerts for the region.</span></span> <span data-ttu-id="cf111-131">Вы можете закрепить плитки оповещения, как и любой другой плитки в этой колонке, на панель мониторинга для быстрого доступа.</span><span class="sxs-lookup"><span data-stu-id="cf111-131">You can pin the Alerts tile, like any other tile on this blade, to the dashboard for quick access.</span></span>   

![Предупреждения плитка, показано предупреждение](media/azure-stack-monitor-health/image3.png)

<span data-ttu-id="cf111-133">Выбрав в верхней части **оповещения** плитки, перейдите в список все активные предупреждения для региона.</span><span class="sxs-lookup"><span data-stu-id="cf111-133">By selecting the top portion of the **Alerts** tile, you navigate to the list of all active alerts for the region.</span></span> <span data-ttu-id="cf111-134">Если выбран один **критическое** или **предупреждение** позиции строки во фрагменте, перейдите в отфильтрованный список оповещений (критическое или предупреждение).</span><span class="sxs-lookup"><span data-stu-id="cf111-134">If you select either the **Critical** or **Warning** line item within the tile, you navigate to a filtered list of alerts (Critical or Warning).</span></span> 

![Отфильтрованные предупреждающие оповещения](media/azure-stack-monitor-health/image4.png)
  
<span data-ttu-id="cf111-136">**Оповещения** колонке поддерживает фильтрацию на состояние (активные или закрытые) и серьезности ("критический" или "Предупреждение").</span><span class="sxs-lookup"><span data-stu-id="cf111-136">The **Alerts** blade supports the ability to filter both on status (Active or Closed) and severity (Critical or Warning).</span></span> <span data-ttu-id="cf111-137">Представление по умолчанию отображаются все активные предупреждения.</span><span class="sxs-lookup"><span data-stu-id="cf111-137">The default view displays all Active alerts.</span></span> <span data-ttu-id="cf111-138">Все закрытые оповещения удаляются из системы через семь дней.</span><span class="sxs-lookup"><span data-stu-id="cf111-138">All closed alerts are removed from the system after seven days.</span></span>

![Фильтровать по критические или состояние предупреждения «фильтр»](media/azure-stack-monitor-health/image5.png)

<span data-ttu-id="cf111-140">В колонке оповещения также предоставляет **представление API** действие, которое отображает API Rest, который использовался для создания представления списка.</span><span class="sxs-lookup"><span data-stu-id="cf111-140">The Alerts blade also exposes the **View API** action, which displays the Rest API that was used to generate the list view.</span></span> <span data-ttu-id="cf111-141">Это действие позволяет быстро ознакомиться с синтаксисом Rest API, который можно использовать для запроса предупреждений.</span><span class="sxs-lookup"><span data-stu-id="cf111-141">This action provides a quick way to become familiar with the Rest API syntax that you can use to query alerts.</span></span> <span data-ttu-id="cf111-142">Этот API можно использовать в службе автоматизации и интеграции с существующие центра обработки данных мониторинга, отчетов и отслеживания решения.</span><span class="sxs-lookup"><span data-stu-id="cf111-142">You can use this API in automation or for integration with your existing datacenter monitoring, reporting, and ticketing solutions.</span></span> 

![Параметр API представления, отображающего API-интерфейса Rest](media/azure-stack-monitor-health/image6.png)

<span data-ttu-id="cf111-144">В колонке оповещения можно выбрать оповещение для перехода к **сведения об предупреждении** колонку.</span><span class="sxs-lookup"><span data-stu-id="cf111-144">From the Alerts blade, you can select an alert to navigate to the **Alert details** blade.</span></span> <span data-ttu-id="cf111-145">Эту колонку отображает все поля, которые связаны с предупреждением и предоставляет быстрый переход к уязвимым компонентом и источником предупреждения.</span><span class="sxs-lookup"><span data-stu-id="cf111-145">This blade displays all fields that are associated with the alert, and enables quick navigation to the affected component and source of the alert.</span></span> <span data-ttu-id="cf111-146">Например следующее оповещение возникает, если один из экземпляров роли инфраструктуры переходит в автономный режим или недоступен.</span><span class="sxs-lookup"><span data-stu-id="cf111-146">For example, the following alert occurs if one of the infrastructure role instances goes offline or is not accessible.</span></span>  

![В колонке сведений о предупреждении](media/azure-stack-monitor-health/image7.png)

<span data-ttu-id="cf111-148">После инфраструктуры экземпляр роли не вернется в оперативный режим, это оповещение автоматически закрывается.</span><span class="sxs-lookup"><span data-stu-id="cf111-148">After the infrastructure role instance is back online, this alert automatically closes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf111-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cf111-149">Next steps</span></span>

[<span data-ttu-id="cf111-150">Управление обновлениями в стек Azure</span><span class="sxs-lookup"><span data-stu-id="cf111-150">Manage updates in Azure Stack</span></span>](azure-stack-updates.md)

[<span data-ttu-id="cf111-151">Область управления в стек Azure</span><span class="sxs-lookup"><span data-stu-id="cf111-151">Region management in Azure Stack</span></span>](azure-stack-region-management.md)
