---
title: "Общие сведения о работоспособности ресурсов aaaAzure | Документы Microsoft"
description: "Обзор службы работоспособности ресурсов Azure"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 06/01/2016
ms.author: BernardoAMunoz
ms.openlocfilehash: b920241b2f64a0695ba2c32e9ccb0c2c3739986d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-overview"></a><span data-ttu-id="30627-103">Обзор службы работоспособности ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="30627-103">Azure resource health overview</span></span>
 
<span data-ttu-id="30627-104">Служба работоспособности ресурсов позволяет выполнять диагностику и получать поддержку, если проблема Azure влияет на ресурсы.</span><span class="sxs-lookup"><span data-stu-id="30627-104">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="30627-105">Он предоставляет информацию о работоспособности hello текущие и прошлые ресурсы и помогает избежать проблем.</span><span class="sxs-lookup"><span data-stu-id="30627-105">It informs you about hello current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="30627-106">Служба работоспособности ресурсов обеспечивает поддержку, если вам необходима помощь в решении проблемы со службой Azure.</span><span class="sxs-lookup"><span data-stu-id="30627-106">Resource health provides technical support when you need help with Azure service issues.</span></span>

<span data-ttu-id="30627-107">В то время как [состояние Azure](https://status.azure.com) сообщает о проблемах службы, которые влияют на широкий спектр клиентам Azure, исправность ресурсов предоставляет персонализированные панели мониторинга работоспособности hello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="30627-107">Whereas [Azure Status](https://status.azure.com) informs you about service issues that affect a broad set of Azure customers, resource health provides you with a personalized dashboard of hello health of your resources.</span></span> <span data-ttu-id="30627-108">Исправности ресурсов показывает все значения времени hello ресурсы были недоступны в hello просрочен платеж за tooAzure проблем со службой.</span><span class="sxs-lookup"><span data-stu-id="30627-108">Resource health shows you all hello times your resources were unavailable in hello past due tooAzure service issues.</span></span> <span data-ttu-id="30627-109">Это упрощает вы toounderstand Если было нарушено соглашение об уровне ОБСЛУЖИВАНИЯ.</span><span class="sxs-lookup"><span data-stu-id="30627-109">This makes it simple for you toounderstand if an SLA was violated.</span></span> 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a><span data-ttu-id="30627-110">Что представляет собой ресурс и каким образом служба работоспособности ресурсов определяет его состояние?</span><span class="sxs-lookup"><span data-stu-id="30627-110">What is considered a resource and how does resource health decides if a resource is healthy or not?</span></span>
<span data-ttu-id="30627-111">Ресурс — это экземпляр ресурса, предлагаемый службой Azure посредством Azure Resource Manager, например виртуальная машина, веб-приложение или база данных SQL.</span><span class="sxs-lookup"><span data-stu-id="30627-111">A resource is an instance of a resource type offered by an Azure service through Azure Resource Manager, for example: a virtual machine, a web app, or a SQL database.</span></span>

<span data-ttu-id="30627-112">Исправности ресурсов полагается на сигналы, генерируемой tooassess hello различных служб Azure, если ресурс находится в работоспособном состоянии или нет.</span><span class="sxs-lookup"><span data-stu-id="30627-112">Resource health relies on signals emitted by hello different Azure services tooassess if a resource is healthy or not.</span></span> <span data-ttu-id="30627-113">Если ресурс принимает неисправное состояние, исправность ресурсов анализирует дополнительных сведений toodetermine hello источник проблемы hello.</span><span class="sxs-lookup"><span data-stu-id="30627-113">If a resource is unhealthy, resource health analyzes additional information toodetermine hello source of hello problem.</span></span> <span data-ttu-id="30627-114">Он также определяет действия, которые Microsoft занимает toofix hello проблему или вызвать проблемы hello действия можно выполнять tooaddress hello.</span><span class="sxs-lookup"><span data-stu-id="30627-114">It also identifies actions Microsoft is taking toofix hello issue or what actions you can take tooaddress hello cause of hello problem.</span></span> 

<span data-ttu-id="30627-115">Просмотрите hello полный список типов ресурсов и работоспособности проверяет [работоспособности ресурсов Azure](resource-health-checks-resource-types.md) для получения дополнительной информации об оценкой работоспособности.</span><span class="sxs-lookup"><span data-stu-id="30627-115">Review hello full list of resource types and health checks in [Azure resource health](resource-health-checks-resource-types.md) for additional details on how health is assessed.</span></span>

## <a name="health-status-provided-by-resource-health"></a><span data-ttu-id="30627-116">Состояние работоспособности, сообщаемое службой работоспособности ресурсов</span><span class="sxs-lookup"><span data-stu-id="30627-116">Health status provided by resource health</span></span>
<span data-ttu-id="30627-117">Hello работоспособности ресурса является одним из следующих статусов hello:</span><span class="sxs-lookup"><span data-stu-id="30627-117">hello health of a resource is one of hello following statuses:</span></span>

### <a name="available"></a><span data-ttu-id="30627-118">Доступна</span><span class="sxs-lookup"><span data-stu-id="30627-118">Available</span></span>
<span data-ttu-id="30627-119">Служба Hello не обнаружила любые события, влияющие на работоспособность hello hello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="30627-119">hello service has not detected any events impacting hello health of hello resource.</span></span> <span data-ttu-id="30627-120">В случаях, где ресурсов hello восстановлена после незапланированных простоев во время hello последние 24 часа, вы увидите hello **восстановлена** уведомления.</span><span class="sxs-lookup"><span data-stu-id="30627-120">In cases where hello resource has recovered from unplanned downtime during hello last 24 hours you will see hello **recently recovered** notification.</span></span>

![Служба работоспособности ресурсов: виртуальная машина доступна](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a><span data-ttu-id="30627-122">Рекомендации недоступны</span><span class="sxs-lookup"><span data-stu-id="30627-122">Unavailable</span></span>
<span data-ttu-id="30627-123">Служба Hello обнаружила платформы или hello работоспособности ресурса hello, влияющие на событие не платформы.</span><span class="sxs-lookup"><span data-stu-id="30627-123">hello service has detected an ongoing platform or non-platform event impacting hello health of hello resource.</span></span>

#### <a name="platform-events"></a><span data-ttu-id="30627-124">События на платформе</span><span class="sxs-lookup"><span data-stu-id="30627-124">Platform events</span></span>
<span data-ttu-id="30627-125">Эти события запускается в нескольких компонентах hello инфраструктуры Azure и включают как запланированных действий, таких как планового обслуживания и Непредвиденная инцидентов, например узла незапланированной перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="30627-125">These events are triggered by multiple components of hello Azure infrastructure and include both scheduled actions like planned maintenance and unexpected incidents like an unplanned host reboot.</span></span>

<span data-ttu-id="30627-126">Исправности ресурсов содержит дополнительные сведения о событий hello, процесс восстановления hello и включает поддержку toocontact даже при отсутствии активного поддержки соглашение Microsoft.</span><span class="sxs-lookup"><span data-stu-id="30627-126">Resource health provides additional details on hello event, hello recovery process and enables you toocontact support even if you don't have an active Microsoft support agreement.</span></span>

![Ресурс работоспособности недоступен виртуальной машины из-за tooplatform событий](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a><span data-ttu-id="30627-128">События за пределами платформы</span><span class="sxs-lookup"><span data-stu-id="30627-128">Non-Platform events</span></span>
<span data-ttu-id="30627-129">Эти события, связанные с действия, выполняемые пользователями, например остановка виртуальной машины или достижение hello максимальное число подключений tooa кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="30627-129">These events are triggered by actions taken by users, for example stopping a virtual machine or reaching hello maximum number of connections tooa Redis Cache.</span></span>

![Ресурс работоспособности недоступен виртуальной машины из-за события toonon платформы](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a><span data-ttu-id="30627-131">Unknown</span><span class="sxs-lookup"><span data-stu-id="30627-131">Unknown</span></span>
<span data-ttu-id="30627-132">Это состояние указывает на то, что служба работоспособности ресурсов не получала сведений об этом ресурсе более 10 минут.</span><span class="sxs-lookup"><span data-stu-id="30627-132">This health status indicates that resource health has not received information about this resource for more than 10 minutes.</span></span> <span data-ttu-id="30627-133">Это состояние не является более точную указанием hello состояние ресурса hello, он является точкой важные данные в hello, поиск и устранение неполадок:</span><span class="sxs-lookup"><span data-stu-id="30627-133">While this status is not a definitive indication of hello state of hello resource, it is an important data point in hello troubleshooting process:</span></span>
* <span data-ttu-id="30627-134">Если ресурс hello выполняется как hello ожидаемое состояние ресурса hello обновит tooAvailable через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="30627-134">If hello resource is running as expected hello status of hello resource will update tooAvailable after a few minutes.</span></span>
* <span data-ttu-id="30627-135">При возникновении проблем с ресурсом hello hello Unknown состояние работоспособности может предложить ресурсов hello затронут событие платформы hello.</span><span class="sxs-lookup"><span data-stu-id="30627-135">If you are experiencing problems with hello resource, hello Unknown health status may suggest hello resource is impacted by an event in hello platform.</span></span>

![Служба работоспособности ресурсов: неизвестно (виртуальная машина)](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a><span data-ttu-id="30627-137">Сообщение о неправильном состоянии</span><span class="sxs-lookup"><span data-stu-id="30627-137">Report an incorrect status</span></span>
<span data-ttu-id="30627-138">Если в любой момент вы считаете, что неверный hello текущее состояние работоспособности, сообщите нам вы узнаете, щелкнув **сообщения о состоянии работоспособности неправильное**.</span><span class="sxs-lookup"><span data-stu-id="30627-138">If at any point you believe hello current health status is incorrect, you can let us know by clicking **Report incorrect health status**.</span></span> <span data-ttu-id="30627-139">В случаях, где будут затронуты проблемой Azure мы рекомендуем вам поддержки toocontact из колонки работоспособности ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="30627-139">In cases where you are impacted by an Azure problem, we encourage you toocontact support from hello resource health blade.</span></span> 

![Служба работоспособности ресурсов: сообщение о неправильном состоянии](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a><span data-ttu-id="30627-141">Накопленные сведения</span><span class="sxs-lookup"><span data-stu-id="30627-141">Historical Information</span></span>
<span data-ttu-id="30627-142">Получить данные журнала работоспособности дней too14 щелкнуть **Просмотр журнала** в колонки работоспособности ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="30627-142">You can access up too14 days of historical health data by clicking **View History** in hello Resource health blade.</span></span> 

![Служба работоспособности ресурсов: просмотр журнала](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a><span data-ttu-id="30627-144">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="30627-144">Getting started</span></span>
<span data-ttu-id="30627-145">tooopen исправности ресурсов для одного ресурса</span><span class="sxs-lookup"><span data-stu-id="30627-145">tooopen Resource health for one resource</span></span>
1.  <span data-ttu-id="30627-146">Войдите hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="30627-146">Sign in into hello Azure portal.</span></span>
2.  <span data-ttu-id="30627-147">Перейдите tooyour ресурсов.</span><span class="sxs-lookup"><span data-stu-id="30627-147">Navigate tooyour resource.</span></span>
3.  <span data-ttu-id="30627-148">В меню ресурса hello, расположенный в левой части hello, нажмите кнопку **исправности ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="30627-148">In hello resource menu located in hello left-hand side, click **Resource health**.</span></span>

![Открытие сведений о работоспособности ресурса из колонки ресурса](./media/resource-health-overview/from-resource-blade.png)

<span data-ttu-id="30627-150">Исправности ресурсов можно также перейти, щелкнув **дополнительные службы**и введя **исправности ресурсов** в фильтр текстовое поле tooopen hello **справки и поддержки** колонку.</span><span class="sxs-lookup"><span data-stu-id="30627-150">You can also access resource health by clicking **More services**, and typing **resource health** in filter text box tooopen hello **Help + Support** blade.</span></span> <span data-ttu-id="30627-151">Затем выберите [**Работоспособность ресурсов**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span><span class="sxs-lookup"><span data-stu-id="30627-151">Finally click [**Resource health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span></span>

![Открытие службы работоспособности ресурсов из меню "Больше служб"](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a><span data-ttu-id="30627-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="30627-153">Next steps</span></span>

<span data-ttu-id="30627-154">Извлечь эти ресурсы toolearn Дополнительные сведения о работоспособности ресурсов:</span><span class="sxs-lookup"><span data-stu-id="30627-154">Check out these resources toolearn more about resource health:</span></span>
-  <span data-ttu-id="30627-155">[Resource types and health checks in Azure resource health](resource-health-checks-resource-types.md) (Типы ресурсов и проверки работоспособности в службе работоспособности ресурсов Azure)</span><span class="sxs-lookup"><span data-stu-id="30627-155">[Resource types and health checks in Azure resource health](resource-health-checks-resource-types.md)</span></span>
-  [<span data-ttu-id="30627-156">Часто задаваемые вопросы о службе работоспособности ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="30627-156">Frequently asked questions about Azure resource health</span></span>](resource-health-faq.md)




