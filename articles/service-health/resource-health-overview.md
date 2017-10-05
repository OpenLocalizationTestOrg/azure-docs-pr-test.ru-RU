---
title: "Обзор службы работоспособности ресурсов Azure | Документация Майкрософт"
description: "Обзор службы работоспособности ресурсов Azure"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/01/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: 040d58a81a9b41fe660e4276d698bf884f90bb6c
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="azure-resource-health-overview"></a><span data-ttu-id="4a286-103">Обзор службы работоспособности ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="4a286-103">Azure resource health overview</span></span>
 
<span data-ttu-id="4a286-104">Служба работоспособности ресурсов позволяет выполнять диагностику и получать поддержку, если проблема Azure влияет на ресурсы.</span><span class="sxs-lookup"><span data-stu-id="4a286-104">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="4a286-105">Она представляет сведения о текущем состоянии работоспособности ресурсов и о состоянии работоспособности ресурсов за прошедший период, а также помогает устранить проблемы.</span><span class="sxs-lookup"><span data-stu-id="4a286-105">It informs you about the current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="4a286-106">Служба работоспособности ресурсов обеспечивает поддержку, если вам необходима помощь в решении проблемы со службой Azure.</span><span class="sxs-lookup"><span data-stu-id="4a286-106">Resource health provides technical support when you need help with Azure service issues.</span></span>

<span data-ttu-id="4a286-107">Служба [Состояние Azure](https://status.azure.com) информирует о проблемах, влияющих на обслуживание множества клиентов Azure, а служба работоспособности ресурсов предоставляет персонализированную панель мониторинга для контроля работоспособности ваших ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4a286-107">Whereas [Azure Status](https://status.azure.com) informs you about service issues that affect a broad set of Azure customers, resource health provides you with a personalized dashboard of the health of your resources.</span></span> <span data-ttu-id="4a286-108">В службе работоспособности ресурсов отображаются все случаи, когда ресурсы были недоступны в прошлом из-за проблем со службами Azure.</span><span class="sxs-lookup"><span data-stu-id="4a286-108">Resource health shows you all the times your resources were unavailable in the past due to Azure service issues.</span></span> <span data-ttu-id="4a286-109">С помощью этой службы просто определить, было ли нарушено Соглашение об уровне обслуживания.</span><span class="sxs-lookup"><span data-stu-id="4a286-109">This makes it simple for you to understand if an SLA was violated.</span></span> 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a><span data-ttu-id="4a286-110">Что представляет собой ресурс и каким образом служба работоспособности ресурсов определяет его состояние?</span><span class="sxs-lookup"><span data-stu-id="4a286-110">What is considered a resource and how does resource health decides if a resource is healthy or not?</span></span>
<span data-ttu-id="4a286-111">Ресурс — это экземпляр ресурса, предлагаемый службой Azure посредством Azure Resource Manager, например виртуальная машина, веб-приложение или база данных SQL.</span><span class="sxs-lookup"><span data-stu-id="4a286-111">A resource is an instance of a resource type offered by an Azure service through Azure Resource Manager, for example: a virtual machine, a web app, or a SQL database.</span></span>

<span data-ttu-id="4a286-112">Для определения состояния ресурса в службе работоспособности ресурсов используются сигналы, генерируемые различными службами Azure.</span><span class="sxs-lookup"><span data-stu-id="4a286-112">Resource health relies on signals emitted by the different Azure services to assess if a resource is healthy or not.</span></span> <span data-ttu-id="4a286-113">Если ресурс не работает, то служба работоспособности ресурсов анализирует дополнительные сведения для определения источника проблемы.</span><span class="sxs-lookup"><span data-stu-id="4a286-113">If a resource is unhealthy, resource health analyzes additional information to determine the source of the problem.</span></span> <span data-ttu-id="4a286-114">Она также определяет действия, предпринимаемые корпорацией Майкрософт для решения проблемы, или действия, которые вы можете выполнить для устранения причины проблемы.</span><span class="sxs-lookup"><span data-stu-id="4a286-114">It also identifies actions Microsoft is taking to fix the issue or what actions you can take to address the cause of the problem.</span></span> 

<span data-ttu-id="4a286-115">Дополнительные сведения о том, как оценивается работоспособность, приведены в полном списке типов ресурсов и проверок работоспособности в [этой статье](resource-health-checks-resource-types.md).</span><span class="sxs-lookup"><span data-stu-id="4a286-115">Review the full list of resource types and health checks in [Azure resource health](resource-health-checks-resource-types.md) for additional details on how health is assessed.</span></span>

## <a name="health-status-provided-by-resource-health"></a><span data-ttu-id="4a286-116">Состояние работоспособности, сообщаемое службой работоспособности ресурсов</span><span class="sxs-lookup"><span data-stu-id="4a286-116">Health status provided by resource health</span></span>
<span data-ttu-id="4a286-117">Работоспособность ресурса может иметь одно из следующих состояний:</span><span class="sxs-lookup"><span data-stu-id="4a286-117">The health of a resource is one of the following statuses:</span></span>

### <a name="available"></a><span data-ttu-id="4a286-118">Доступна</span><span class="sxs-lookup"><span data-stu-id="4a286-118">Available</span></span>
<span data-ttu-id="4a286-119">Служба не обнаружила никаких событий, влияющих на работоспособность ресурса.</span><span class="sxs-lookup"><span data-stu-id="4a286-119">The service has not detected any events impacting the health of the resource.</span></span> <span data-ttu-id="4a286-120">Если ресурс был восстановлен после незапланированного простоя в течение последних 24 часов, то отобразится уведомление о том, что проблема **недавно решена**.</span><span class="sxs-lookup"><span data-stu-id="4a286-120">In cases where the resource has recovered from unplanned downtime during the last 24 hours you will see the **recently recovered** notification.</span></span>

![Служба работоспособности ресурсов: виртуальная машина доступна](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a><span data-ttu-id="4a286-122">Рекомендации недоступны</span><span class="sxs-lookup"><span data-stu-id="4a286-122">Unavailable</span></span>
<span data-ttu-id="4a286-123">Служба обнаружила на платформе или за ее пределами текущее событие, влияющее на работоспособность ресурса.</span><span class="sxs-lookup"><span data-stu-id="4a286-123">The service has detected an ongoing platform or non-platform event impacting the health of the resource.</span></span>

#### <a name="platform-events"></a><span data-ttu-id="4a286-124">События на платформе</span><span class="sxs-lookup"><span data-stu-id="4a286-124">Platform events</span></span>
<span data-ttu-id="4a286-125">Эти события вызываются несколькими компонентами инфраструктуры Azure и включают в себя как запланированные действия (например плановое обслуживание), так и непредвиденные инциденты (например внеплановая перезагрузка узла).</span><span class="sxs-lookup"><span data-stu-id="4a286-125">These events are triggered by multiple components of the Azure infrastructure and include both scheduled actions like planned maintenance and unexpected incidents like an unplanned host reboot.</span></span>

<span data-ttu-id="4a286-126">Служба работоспособности ресурсов предоставляет дополнительные сведения о событии, процессе восстановления и позволяет связаться со службой поддержки, даже если у вас нет действующего соглашения о поддержке с корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="4a286-126">Resource health provides additional details on the event, the recovery process and enables you to contact support even if you don't have an active Microsoft support agreement.</span></span>

![Служба работоспособности ресурсов: виртуальная машина недоступна (событие на платформе)](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a><span data-ttu-id="4a286-128">События за пределами платформы</span><span class="sxs-lookup"><span data-stu-id="4a286-128">Non-Platform events</span></span>
<span data-ttu-id="4a286-129">Эти события вызываются действиями, которые выполняют пользователи. Например, пользователь останавливает работу виртуальной машины, или достигается максимальное число подключений к кэшу Redis.</span><span class="sxs-lookup"><span data-stu-id="4a286-129">These events are triggered by actions taken by users, for example stopping a virtual machine or reaching the maximum number of connections to a Redis Cache.</span></span>

![Служба работоспособности ресурсов: виртуальная машина недоступна (событие за пределами платформы)](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a><span data-ttu-id="4a286-131">Unknown</span><span class="sxs-lookup"><span data-stu-id="4a286-131">Unknown</span></span>
<span data-ttu-id="4a286-132">Это состояние указывает на то, что служба работоспособности ресурсов не получала сведений об этом ресурсе более 10 минут.</span><span class="sxs-lookup"><span data-stu-id="4a286-132">This health status indicates that resource health has not received information about this resource for more than 10 minutes.</span></span> <span data-ttu-id="4a286-133">Несмотря на то, что это значение не указывает состояние ресурса определенно, оно является важной информацией в процессе устранения неполадок:</span><span class="sxs-lookup"><span data-stu-id="4a286-133">While this status is not a definitive indication of the state of the resource, it is an important data point in the troubleshooting process:</span></span>
* <span data-ttu-id="4a286-134">Если ресурс работает должным образом, то через несколько минут его состояния изменится на "Доступно".</span><span class="sxs-lookup"><span data-stu-id="4a286-134">If the resource is running as expected the status of the resource will update to Available after a few minutes.</span></span>
* <span data-ttu-id="4a286-135">Если ресурс испытывает проблемы, то состояние работоспособности "Неизвестно" может означать, что на ресурс влияет какое-то событие на платформе.</span><span class="sxs-lookup"><span data-stu-id="4a286-135">If you are experiencing problems with the resource, the Unknown health status may suggest the resource is impacted by an event in the platform.</span></span>

![Служба работоспособности ресурсов: неизвестно (виртуальная машина)](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a><span data-ttu-id="4a286-137">Сообщение о неправильном состоянии</span><span class="sxs-lookup"><span data-stu-id="4a286-137">Report an incorrect status</span></span>
<span data-ttu-id="4a286-138">Если вы считаете, что в какой-то момент служба неправильно отображает текущее состояние работоспособности ресурса, то сообщите нам об этом, щелкнув ссылку **Сообщить неправильное состояние работоспособности**.</span><span class="sxs-lookup"><span data-stu-id="4a286-138">If at any point you believe the current health status is incorrect, you can let us know by clicking **Report incorrect health status**.</span></span> <span data-ttu-id="4a286-139">В случаях, когда возникают проблемы с работоспособностью ресурсов Azure, рекомендуется обратиться в службу поддержки, используя колонку работоспособности ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4a286-139">In cases where you are impacted by an Azure problem, we encourage you to contact support from the resource health blade.</span></span> 

![Служба работоспособности ресурсов: сообщение о неправильном состоянии](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a><span data-ttu-id="4a286-141">Накопленные сведения</span><span class="sxs-lookup"><span data-stu-id="4a286-141">Historical Information</span></span>
<span data-ttu-id="4a286-142">Вы можете просмотреть сведения о работоспособности ресурсов, накопленные за последние 14 дней. Для этого щелкните **Просмотреть журнал** в колонке работоспособности ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4a286-142">You can access up to 14 days of historical health data by clicking **View History** in the Resource health blade.</span></span> 

![Служба работоспособности ресурсов: просмотр журнала](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a><span data-ttu-id="4a286-144">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="4a286-144">Getting started</span></span>
<span data-ttu-id="4a286-145">Чтобы открыть служба работоспособности ресурсов для одного ресурса, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4a286-145">To open Resource health for one resource</span></span>
1.  <span data-ttu-id="4a286-146">Войдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4a286-146">Sign in into the Azure portal.</span></span>
2.  <span data-ttu-id="4a286-147">Перейдите к нужному ресурсу.</span><span class="sxs-lookup"><span data-stu-id="4a286-147">Navigate to your resource.</span></span>
3.  <span data-ttu-id="4a286-148">В меню ресурса, расположенном слева, щелкните **Работоспособность ресурса**.</span><span class="sxs-lookup"><span data-stu-id="4a286-148">In the resource menu located in the left-hand side, click **Resource health**.</span></span>

![Открытие сведений о работоспособности ресурса из колонки ресурса](./media/resource-health-overview/from-resource-blade.png)

<span data-ttu-id="4a286-150">Службу работоспособности ресурсов также можно найти, щелкнув пункт **Больше служб** и введя в текстовое поле фильтра текст **работоспособность ресурсов**, чтобы открыть колонку **Справка и поддержка**.</span><span class="sxs-lookup"><span data-stu-id="4a286-150">You can also access resource health by clicking **More services**, and typing **resource health** in filter text box to open the **Help + Support** blade.</span></span> <span data-ttu-id="4a286-151">Затем выберите [**Работоспособность ресурсов**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span><span class="sxs-lookup"><span data-stu-id="4a286-151">Finally click [**Resource health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span></span>

![Открытие службы работоспособности ресурсов из меню "Больше служб"](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a><span data-ttu-id="4a286-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4a286-153">Next steps</span></span>

<span data-ttu-id="4a286-154">Ознакомьтесь с этими материалами, чтобы узнать больше о работоспособности ресурсов:</span><span class="sxs-lookup"><span data-stu-id="4a286-154">Check out these resources to learn more about resource health:</span></span>
-  <span data-ttu-id="4a286-155">[Resource types and health checks in Azure resource health](resource-health-checks-resource-types.md) (Типы ресурсов и проверки работоспособности в службе работоспособности ресурсов Azure)</span><span class="sxs-lookup"><span data-stu-id="4a286-155">[Resource types and health checks in Azure resource health](resource-health-checks-resource-types.md)</span></span>
-  [<span data-ttu-id="4a286-156">Часто задаваемые вопросы о службе работоспособности ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="4a286-156">Frequently asked questions about Azure resource health</span></span>](resource-health-faq.md)




