---
title: "Автомасштабирование облачной службы на портале | Документация Майкрософт"
description: "Узнайте, как с помощью портала настроить правила автомасштабирования для веб-роли или рабочей роли облачной службы в Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 701d4404-5cc0-454b-999c-feb94c1685c0
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: e9683d4c5779450fd67fa42ab13095c7f201b4cd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-auto-scaling-for-a-cloud-service-in-the-portal"></a><span data-ttu-id="5a29e-103">Как настроить автомасштабирование для облачной службы на портале</span><span class="sxs-lookup"><span data-stu-id="5a29e-103">How to configure auto scaling for a Cloud Service in the portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5a29e-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="5a29e-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="5a29e-105">Классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="5a29e-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="5a29e-106">Для рабочей роли облачной службы можно задать условия, которые активируют операции масштабировании.</span><span class="sxs-lookup"><span data-stu-id="5a29e-106">Conditions can be set for a cloud service worker role that trigger a scale in or out operation.</span></span> <span data-ttu-id="5a29e-107">Условия для роли могут основываться на нагрузке роли на ЦП, диск или сеть.</span><span class="sxs-lookup"><span data-stu-id="5a29e-107">The conditions for the role can be based on the CPU, disk, or network load of the role.</span></span> <span data-ttu-id="5a29e-108">Можно также задать условие на основе очереди сообщений или метрики какого-то другого ресурса Azure, связанного с подпиской.</span><span class="sxs-lookup"><span data-stu-id="5a29e-108">You can also set a condition based on a message queue or the metric of some other Azure resource associated with your subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="5a29e-109">Эта статья посвящена веб-ролям и рабочим ролям облачной службы.</span><span class="sxs-lookup"><span data-stu-id="5a29e-109">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="5a29e-110">Виртуальные машины (классические), создаваемые напрямую, размещаются в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="5a29e-110">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="5a29e-111">Стандартную виртуальную машину можно масштабировать, связав ее с [группой доступности](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) и включив или отключив ее вручную.</span><span class="sxs-lookup"><span data-stu-id="5a29e-111">You can scale a standard virtual machine by associating it with an [availability set](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) and manually turn them on or off.</span></span>

## <a name="considerations"></a><span data-ttu-id="5a29e-112">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="5a29e-112">Considerations</span></span>
<span data-ttu-id="5a29e-113">При настройке масштабирования приложения следует учитывать следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="5a29e-113">You should consider the following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="5a29e-114">Масштабирование зависит от использования ядер.</span><span class="sxs-lookup"><span data-stu-id="5a29e-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="5a29e-115">Более крупные экземпляры ролей задействуют больше ядер.</span><span class="sxs-lookup"><span data-stu-id="5a29e-115">Larger role instances use more cores.</span></span> <span data-ttu-id="5a29e-116">Масштабировать приложение можно только в пределах количества ядер для используемой подписки.</span><span class="sxs-lookup"><span data-stu-id="5a29e-116">You can scale an application only within the limit of cores for your subscription.</span></span> <span data-ttu-id="5a29e-117">Предположим, что ваша подписка имеет ограничение в 20 ядер.</span><span class="sxs-lookup"><span data-stu-id="5a29e-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="5a29e-118">Если выполняется приложение с двумя средними по размерам облачными службами (всего четыре ядра), то можно увеличить масштаб других развернутых в подписке облачных служб, охватив оставшиеся 16 ядер.</span><span class="sxs-lookup"><span data-stu-id="5a29e-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by the remaining 16 cores.</span></span> <span data-ttu-id="5a29e-119">Дополнительные сведения о размерах см. в статье [Размеры для облачных служб](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="5a29e-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="5a29e-120">Можно настроить масштабирование на основе порогового значения очереди сообщений.</span><span class="sxs-lookup"><span data-stu-id="5a29e-120">You can scale based on a queue message threshold.</span></span> <span data-ttu-id="5a29e-121">Дополнительные сведения об использовании очередей см. в статье [Приступая к работе с хранилищем очередей Azure с помощью .NET](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="5a29e-121">For more information about how to use queues, see [How to use the Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="5a29e-122">Можно также масштабировать другие ресурсы, связанные с подпиской.</span><span class="sxs-lookup"><span data-stu-id="5a29e-122">You can also scale other resources associated with your subscription.</span></span>

* <span data-ttu-id="5a29e-123">В целях обеспечения высокой доступности приложения необходимо убедиться, что приложение развернуто с двумя и более экземплярами ролей.</span><span class="sxs-lookup"><span data-stu-id="5a29e-123">To enable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="5a29e-124">Дополнительные сведения см. в разделе [Соглашения об уровне обслуживания](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="5a29e-124">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>


## <a name="where-scale-is-located"></a><span data-ttu-id="5a29e-125">Где находится функция масштабирования?</span><span class="sxs-lookup"><span data-stu-id="5a29e-125">Where scale is located</span></span>
<span data-ttu-id="5a29e-126">После выбора облачной службы должна появиться колонка облачной службы.</span><span class="sxs-lookup"><span data-stu-id="5a29e-126">After you select your cloud service, you should have the cloud service blade visible.</span></span>

1. <span data-ttu-id="5a29e-127">В колонке облачной службы в элементе **Roles and Instances** (Роли и экземпляры) выберите имя облачной службы.</span><span class="sxs-lookup"><span data-stu-id="5a29e-127">On the cloud service blade, on the **Roles and Instances** tile, select the name of the cloud service.</span></span>   
   <span data-ttu-id="5a29e-128">**ВАЖНО.** Щелкните роль облачной службы, а не экземпляр роли, который расположен под ней.</span><span class="sxs-lookup"><span data-stu-id="5a29e-128">**IMPORTANT**: Make sure to click the cloud service role, not the role instance that is below the role.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. <span data-ttu-id="5a29e-129">Выберите элемент **scale** (масштаб).</span><span class="sxs-lookup"><span data-stu-id="5a29e-129">Select the **scale** tile.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a><span data-ttu-id="5a29e-130">Автоматическое масштабирование</span><span class="sxs-lookup"><span data-stu-id="5a29e-130">Automatic scale</span></span>
<span data-ttu-id="5a29e-131">Параметры масштабирования для роли можно настроить с помощью двух режимов — **ручной** или **автоматический**.</span><span class="sxs-lookup"><span data-stu-id="5a29e-131">You can configure scale settings for a role with either two modes **manual** or **automatic**.</span></span> <span data-ttu-id="5a29e-132">Ручной: в этом режиме, как и следовало ожидать, задается абсолютное число экземпляров.</span><span class="sxs-lookup"><span data-stu-id="5a29e-132">Manual is as you would expect, you set the absolute count of instances.</span></span> <span data-ttu-id="5a29e-133">Автоматический: этот режим позволяет задать набор правил, определяющих как и насколько вы хотите масштабировать.</span><span class="sxs-lookup"><span data-stu-id="5a29e-133">Automatic however allows you to set rules that govern how and by how much you should scale.</span></span>

<span data-ttu-id="5a29e-134">Для параметра **Режим масштабирования** выберите значение **Правила расписания и производительности**.</span><span class="sxs-lookup"><span data-stu-id="5a29e-134">Set the **Scale by** option to **schedule and performance rules**.</span></span>

![Параметры масштабирования облачных служб с профилем и правилом](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. <span data-ttu-id="5a29e-136">Существующий профиль.</span><span class="sxs-lookup"><span data-stu-id="5a29e-136">An existing profile.</span></span>
2. <span data-ttu-id="5a29e-137">Добавьте правило для родительского профиля.</span><span class="sxs-lookup"><span data-stu-id="5a29e-137">Add a rule for the parent profile.</span></span>
3. <span data-ttu-id="5a29e-138">Добавьте другой профиль.</span><span class="sxs-lookup"><span data-stu-id="5a29e-138">Add another profile.</span></span>

<span data-ttu-id="5a29e-139">Выберите **Добавить профиль**.</span><span class="sxs-lookup"><span data-stu-id="5a29e-139">Select **Add Profile**.</span></span> <span data-ttu-id="5a29e-140">Профиль определяет режим, который вы хотите использовать для масштабирования: **всегда**, **периодичность** или **фиксированная дата**.</span><span class="sxs-lookup"><span data-stu-id="5a29e-140">The profile determines which mode you want to use for the scale: **always**, **recurrence**, **fixed date**.</span></span>

<span data-ttu-id="5a29e-141">После настройки профиля и правил выберите значок **Сохранить** вверху экрана.</span><span class="sxs-lookup"><span data-stu-id="5a29e-141">After you have configured the profile and rules, select the **Save** icon at the top.</span></span>

#### <a name="profile"></a><span data-ttu-id="5a29e-142">Профиль</span><span class="sxs-lookup"><span data-stu-id="5a29e-142">Profile</span></span>
<span data-ttu-id="5a29e-143">Профиль задает минимальное и максимальное число экземпляров для масштабирования, а также определяет, когда этот диапазон масштабирования активен.</span><span class="sxs-lookup"><span data-stu-id="5a29e-143">The profile sets minimum and maximum instances for the scale, and also when this scale range is active.</span></span>

* <span data-ttu-id="5a29e-144">**Всегда**</span><span class="sxs-lookup"><span data-stu-id="5a29e-144">**Always**</span></span>

    <span data-ttu-id="5a29e-145">Всегда сохраняйте этот диапазон доступных экземпляров.</span><span class="sxs-lookup"><span data-stu-id="5a29e-145">Always keep this range of instances available.</span></span>  

    ![Облачная служба, которая масштабируется всегда](./media/cloud-services-how-to-scale-portal/select-always.png)
* <span data-ttu-id="5a29e-147">**Периодичность**</span><span class="sxs-lookup"><span data-stu-id="5a29e-147">**Recurrence**</span></span>

    <span data-ttu-id="5a29e-148">Выберите дни недели для масштабирования.</span><span class="sxs-lookup"><span data-stu-id="5a29e-148">Choose a set of days of the week to scale.</span></span>

    ![Облачная служба, которая масштабируется с заданной периодичностью](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* <span data-ttu-id="5a29e-150">**Фиксированная дата**</span><span class="sxs-lookup"><span data-stu-id="5a29e-150">**Fixed Date**</span></span>

    <span data-ttu-id="5a29e-151">Фиксированный диапазон дат для масштабирования роли.</span><span class="sxs-lookup"><span data-stu-id="5a29e-151">A fixed date range to scale the role.</span></span>

    ![Облачная служба, которая масштабируется в фиксированную дату](./media/cloud-services-how-to-scale-portal/select-fixed.png)

<span data-ttu-id="5a29e-153">По завершении настройки профиля нажмите кнопку **ОК** , расположенную в нижней части колонки профиля.</span><span class="sxs-lookup"><span data-stu-id="5a29e-153">After you have configured the profile, select the **OK** button at the bottom of the profile blade.</span></span>

#### <a name="rule"></a><span data-ttu-id="5a29e-154">правило;</span><span class="sxs-lookup"><span data-stu-id="5a29e-154">Rule</span></span>
<span data-ttu-id="5a29e-155">Правила добавляются в профиль и представляют собой условие, которое будет активировать масштабирование.</span><span class="sxs-lookup"><span data-stu-id="5a29e-155">Rules are added to a profile and represent a condition that triggers the scale.</span></span>

<span data-ttu-id="5a29e-156">Триггер правила основан на метрике облачной службы (использование ЦП, активность диска или сетевая активность), к которой можно добавить условное значение.</span><span class="sxs-lookup"><span data-stu-id="5a29e-156">The rule trigger is based on a metric of the cloud service (CPU usage, disk activity, or network activity) to which you can add a conditional value.</span></span> <span data-ttu-id="5a29e-157">Дополнительно можно задать триггер на основе очереди сообщений или метрики какого-то другого ресурса Azure, связанного с подпиской.</span><span class="sxs-lookup"><span data-stu-id="5a29e-157">Additionally you can have the trigger based on a message queue or the metric of some other Azure resource associated with your subscription.</span></span>

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

<span data-ttu-id="5a29e-158">По завершении настройки правила нажмите кнопку **ОК** , расположенную в нижней части колонки правила.</span><span class="sxs-lookup"><span data-stu-id="5a29e-158">After you have configured the rule, select the **OK** button at the bottom of the rule blade.</span></span>

## <a name="back-to-manual-scale"></a><span data-ttu-id="5a29e-159">Вернемся к ручному масштабированию</span><span class="sxs-lookup"><span data-stu-id="5a29e-159">Back to manual scale</span></span>
<span data-ttu-id="5a29e-160">Перейдите к разделу [Настройки масштабирования](#where-scale-is-located) и выберите для параметра **Режим масштабирования** значение **Число экземпляров, вводимое вручную**.</span><span class="sxs-lookup"><span data-stu-id="5a29e-160">Navigate to the [scale settings](#where-scale-is-located) and set the **Scale by** option to **an instance count that I enter manually**.</span></span>

![Параметры масштабирования облачных служб с профилем и правилом](./media/cloud-services-how-to-scale-portal/manual-basics.png)

<span data-ttu-id="5a29e-162">Этот параметр позволяет удалить из роли автомасштабирование, а затем непосредственно задать число экземпляров.</span><span class="sxs-lookup"><span data-stu-id="5a29e-162">This setting removes automated scaling from the role and then you can set the instance count directly.</span></span>

1. <span data-ttu-id="5a29e-163">Параметр масштабирования (ручного или автоматического).</span><span class="sxs-lookup"><span data-stu-id="5a29e-163">The scale (manual or automated) option.</span></span>
2. <span data-ttu-id="5a29e-164">Ползунок экземпляров роли, устанавливающий число экземпляров для масштабирования.</span><span class="sxs-lookup"><span data-stu-id="5a29e-164">A role instance slider to set the instances to scale to.</span></span>
3. <span data-ttu-id="5a29e-165">Экземпляры роли для масштабирования.</span><span class="sxs-lookup"><span data-stu-id="5a29e-165">Instances of the role to scale to.</span></span>

<span data-ttu-id="5a29e-166">После настройки параметров масштабирования выберите значок **Сохранить** вверху экрана.</span><span class="sxs-lookup"><span data-stu-id="5a29e-166">After you have configured the scale settings, select the **Save** icon at the top.</span></span>
