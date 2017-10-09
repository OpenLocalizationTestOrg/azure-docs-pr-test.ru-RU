---
title: "aaaMonitor работоспособности и предупреждений в стек Azure | Документы Microsoft"
description: "Узнайте, как toomonitor работоспособности и предупреждений в стек Azure."
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
ms.openlocfilehash: 11e287c497e154b767c775fe4afcc78ec9e72fb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-health-and-alerts-in-azure-stack"></a><span data-ttu-id="5f592-103">Монитор работоспособности и предупреждений в стек Azure</span><span class="sxs-lookup"><span data-stu-id="5f592-103">Monitor health and alerts in Azure Stack</span></span>

<span data-ttu-id="5f592-104">Стек Azure включает в себя возможности, позволяющие оповещения области стека Azure и работоспособность облака оператор tooview мониторинг инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="5f592-104">Azure Stack includes infrastructure monitoring capabilities that enable a cloud operator tooview health and alerts for an Azure Stack region.</span></span>

<span data-ttu-id="5f592-105">Стек Azure имеет набор возможностей управления области, доступные в hello **область управления** плитки.</span><span class="sxs-lookup"><span data-stu-id="5f592-105">Azure Stack has a set of region management capabilities available in hello **Region management** tile.</span></span> <span data-ttu-id="5f592-106">Этой плитки, закрепленные в портал администратора hello для hello подписки поставщика по умолчанию, по умолчанию отображает все области развертывания hello Azure стека.</span><span class="sxs-lookup"><span data-stu-id="5f592-106">This tile, pinned by default in hello administrator portal for hello Default Provider Subscription, lists all hello deployed regions of Azure Stack.</span></span> <span data-ttu-id="5f592-107">Также показывает число hello активные предупреждения и критические оповещения для каждого региона.</span><span class="sxs-lookup"><span data-stu-id="5f592-107">It also shows hello count of active critical and warning alerts for each region.</span></span> <span data-ttu-id="5f592-108">Эта Плитка используется для перехода в работоспособности hello и функциональности оповещений Azure стека.</span><span class="sxs-lookup"><span data-stu-id="5f592-108">This tile is your entry point into hello health and alert functionality of Azure Stack.</span></span>

 ![Область управления плитки приветствия](media/azure-stack-monitor-health/image1.png)

 ## <a name="understand-health-in-azure-stack"></a><span data-ttu-id="5f592-110">Понимание работоспособности в стек Azure</span><span class="sxs-lookup"><span data-stu-id="5f592-110">Understand health in Azure Stack</span></span>

 <span data-ttu-id="5f592-111">Оповещения и работоспособности осуществляется в стек Azure поставщиком ресурсов hello работоспособности.</span><span class="sxs-lookup"><span data-stu-id="5f592-111">Health and alerts are managed in Azure Stack by hello Health resource provider.</span></span> <span data-ttu-id="5f592-112">Компоненты инфраструктуры Azure стека зарегистрировать поставщик ресурсов hello работоспособности во время развертывания стека Azure и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5f592-112">Azure Stack infrastructure components register with hello Health resource provider during Azure Stack deployment and configuration.</span></span> <span data-ttu-id="5f592-113">Регистрация позволяет hello Отображение работоспособности и предупреждений для каждого компонента.</span><span class="sxs-lookup"><span data-stu-id="5f592-113">This registration enables hello display of health and alerts for each component.</span></span> <span data-ttu-id="5f592-114">Работоспособность стека Azure — это простое понятие.</span><span class="sxs-lookup"><span data-stu-id="5f592-114">Health in Azure Stack is a simple concept.</span></span> <span data-ttu-id="5f592-115">Если предупреждения для зарегистрированных экземпляров exist компонент hello состояние этого компонента отражает hello наихудшее active серьезность предупреждения; Предупреждение или критическое.</span><span class="sxs-lookup"><span data-stu-id="5f592-115">If alerts for a registered instance of a component exist, hello health state of that component reflects hello worst active alert severity; warning, or critical.</span></span>
 
 ## <a name="view-and-manage-component-health-state"></a><span data-ttu-id="5f592-116">Просмотр и управление состояние работоспособности компонента</span><span class="sxs-lookup"><span data-stu-id="5f592-116">View and manage component health state</span></span>
 
 <span data-ttu-id="5f592-117">В обоих hello Azure стека административного портала и через API-Интерфейс Rest и PowerShell можно просмотреть hello состояния работоспособности компонентов.</span><span class="sxs-lookup"><span data-stu-id="5f592-117">You can view hello health state of components in both hello Azure Stack administrator portal and through Rest API and PowerShell.</span></span>
 
<span data-ttu-id="5f592-118">состояние работоспособности hello tooview hello портала щелкните hello области, которые должны tooview в hello **область управления** плитки.</span><span class="sxs-lookup"><span data-stu-id="5f592-118">tooview hello health state in hello portal, click hello region that you want tooview in hello **Region management** tile.</span></span> <span data-ttu-id="5f592-119">Можно просмотреть состояние работоспособности hello ролей инфраструктуры и поставщиков ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5f592-119">You can view hello health state of infrastructure roles and of resource providers.</span></span> <span data-ttu-id="5f592-120">Обратите внимание, что в этом выпуске поставщика ресурсов вычислений hello не сообщает состояние работоспособности.</span><span class="sxs-lookup"><span data-stu-id="5f592-120">Note that in this release, hello Compute resource provider does not report health state.</span></span>

![Список ролей инфраструктуры](media/azure-stack-monitor-health/image2.png)

<span data-ttu-id="5f592-122">Можно щелкнуть tooview роли поставщика или инфраструктуры ресурсов более подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="5f592-122">You can click a resource provider or infrastructure role tooview more detailed information.</span></span>

> [!WARNING]
><span data-ttu-id="5f592-123">Если вы щелкните роль инфраструктуры и выберите hello экземпляра роли, существуют варианты в hello **экземпляра роли** tooStart колонки, перезагрузка или завершение работы.</span><span class="sxs-lookup"><span data-stu-id="5f592-123">If you click an infrastructure role, and then click hello role instance, there are options in hello **Role instance** blade tooStart, Restart, or Shutdown.</span></span> <span data-ttu-id="5f592-124">Сделать **не** эти параметры используются в среде Azure стека Development Kit.</span><span class="sxs-lookup"><span data-stu-id="5f592-124">Do **not** use these options in an Azure Stack Development Kit environment.</span></span> <span data-ttu-id="5f592-125">Эти параметры предназначены только для среды с несколькими узлами, где имеется более одного экземпляра роли на каждую роль службы инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="5f592-125">These options are designed only for a multi-node environment, where there is more than one role instance per infrastructure role.</span></span> <span data-ttu-id="5f592-126">Перезапуск экземпляра роли (особенно AzS-Xrp01) в пакете средств разработки hello приведет нестабильность системы.</span><span class="sxs-lookup"><span data-stu-id="5f592-126">Restarting a role instance (especially AzS-Xrp01) in hello development kit causes system instability.</span></span> <span data-ttu-id="5f592-127">Сведения об устранении неполадок, опубликуйте вашей проблемы toohello [форум Azure стека](https://aka.ms/azurestackforum).</span><span class="sxs-lookup"><span data-stu-id="5f592-127">For troubleshooting assistance, please post your issue toohello [Azure Stack forum](https://aka.ms/azurestackforum).</span></span>
>
 
## <a name="view-alerts"></a><span data-ttu-id="5f592-128">Просмотр оповещений</span><span class="sxs-lookup"><span data-stu-id="5f592-128">View alerts</span></span>

<span data-ttu-id="5f592-129">список активных оповещений для каждого региона Azure стека Hello доступен непосредственно из hello **область управления** колонку.</span><span class="sxs-lookup"><span data-stu-id="5f592-129">hello list of active alerts for each Azure Stack region is available directly from hello **Region management** blade.</span></span> <span data-ttu-id="5f592-130">Hello первый фрагмент в конфигурации по умолчанию hello — hello **оповещения** плитки, который отображает сводку по hello критические и предупреждающие оповещения для области hello.</span><span class="sxs-lookup"><span data-stu-id="5f592-130">hello first tile in hello default configuration is hello **Alerts** tile, which displays a summary of hello critical and warning alerts for hello region.</span></span> <span data-ttu-id="5f592-131">Вы можете закрепить плитки hello оповещения, как и любой другой плитки в этой колонке toohello панель мониторинга для быстрого доступа.</span><span class="sxs-lookup"><span data-stu-id="5f592-131">You can pin hello Alerts tile, like any other tile on this blade, toohello dashboard for quick access.</span></span>   

![Предупреждения плитка, показано предупреждение](media/azure-stack-monitor-health/image3.png)

<span data-ttu-id="5f592-133">Выбрав в верхней части hello hello **оповещения** плитки, перейдите toohello список все активные предупреждения для региона hello.</span><span class="sxs-lookup"><span data-stu-id="5f592-133">By selecting hello top portion of hello **Alerts** tile, you navigate toohello list of all active alerts for hello region.</span></span> <span data-ttu-id="5f592-134">При выборе любой hello **критическое** или **предупреждение** позиции строки в плитке hello перейдите tooa Фильтрация списка оповещений (критическое или предупреждение).</span><span class="sxs-lookup"><span data-stu-id="5f592-134">If you select either hello **Critical** or **Warning** line item within hello tile, you navigate tooa filtered list of alerts (Critical or Warning).</span></span> 

![Отфильтрованные предупреждающие оповещения](media/azure-stack-monitor-health/image4.png)
  
<span data-ttu-id="5f592-136">Hello **оповещения** колонке поддерживает toofilter возможность hello на состояние (активные или закрытые) и серьезности ("критический" или "Предупреждение").</span><span class="sxs-lookup"><span data-stu-id="5f592-136">hello **Alerts** blade supports hello ability toofilter both on status (Active or Closed) and severity (Critical or Warning).</span></span> <span data-ttu-id="5f592-137">представление по умолчанию Hello отображает все активные предупреждения.</span><span class="sxs-lookup"><span data-stu-id="5f592-137">hello default view displays all Active alerts.</span></span> <span data-ttu-id="5f592-138">Все закрытые оповещения удаляются из системы hello в течение семи дней.</span><span class="sxs-lookup"><span data-stu-id="5f592-138">All closed alerts are removed from hello system after seven days.</span></span>

![Фильтр области toofilter по состоянию, предупреждения или критический](media/azure-stack-monitor-health/image5.png)

<span data-ttu-id="5f592-140">Hello колонке оповещения также предоставляет hello **представление API** действие, просматривать какие отображает hello API Rest, который был список используемых toogenerate hello.</span><span class="sxs-lookup"><span data-stu-id="5f592-140">hello Alerts blade also exposes hello **View API** action, which displays hello Rest API that was used toogenerate hello list view.</span></span> <span data-ttu-id="5f592-141">Это действие предоставляет быстрый способ toobecome, знакомы с синтаксисом API-интерфейса Rest hello, которые можно использовать tooquery предупреждения.</span><span class="sxs-lookup"><span data-stu-id="5f592-141">This action provides a quick way toobecome familiar with hello Rest API syntax that you can use tooquery alerts.</span></span> <span data-ttu-id="5f592-142">Этот API можно использовать в службе автоматизации и интеграции с существующие центра обработки данных мониторинга, отчетов и отслеживания решения.</span><span class="sxs-lookup"><span data-stu-id="5f592-142">You can use this API in automation or for integration with your existing datacenter monitoring, reporting, and ticketing solutions.</span></span> 

![Hello параметр API представления, отображающего hello Rest API](media/azure-stack-monitor-health/image6.png)

<span data-ttu-id="5f592-144">Из колонки hello оповещения, можно выбрать предупреждения toonavigate toohello **сведения об предупреждении** колонку.</span><span class="sxs-lookup"><span data-stu-id="5f592-144">From hello Alerts blade, you can select an alert toonavigate toohello **Alert details** blade.</span></span> <span data-ttu-id="5f592-145">Эту колонку отображает все поля, связанные с предупреждением, hello и обеспечивает быстрый переход toohello влияет компонентов и источника предупреждения hello.</span><span class="sxs-lookup"><span data-stu-id="5f592-145">This blade displays all fields that are associated with hello alert, and enables quick navigation toohello affected component and source of hello alert.</span></span> <span data-ttu-id="5f592-146">Например hello следующее оповещение возникает, если один из экземпляров роли инфраструктуры hello переходит в автономный режим или недоступен.</span><span class="sxs-lookup"><span data-stu-id="5f592-146">For example, hello following alert occurs if one of hello infrastructure role instances goes offline or is not accessible.</span></span>  

![сведения о предупреждении колонке Hello](media/azure-stack-monitor-health/image7.png)

<span data-ttu-id="5f592-148">После экземпляра роли инфраструктуры hello вернется в оперативный режим, это оповещение автоматически закрывается.</span><span class="sxs-lookup"><span data-stu-id="5f592-148">After hello infrastructure role instance is back online, this alert automatically closes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f592-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5f592-149">Next steps</span></span>

[<span data-ttu-id="5f592-150">Управление обновлениями в стек Azure</span><span class="sxs-lookup"><span data-stu-id="5f592-150">Manage updates in Azure Stack</span></span>](azure-stack-updates.md)

[<span data-ttu-id="5f592-151">Область управления в стек Azure</span><span class="sxs-lookup"><span data-stu-id="5f592-151">Region management in Azure Stack</span></span>](azure-stack-region-management.md)
