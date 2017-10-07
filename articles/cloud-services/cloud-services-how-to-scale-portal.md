---
title: "aaaAuto масштабирование облачной службы в портале hello | Документы Microsoft"
description: "Узнайте, как toouse hello портала tooconfigure автоматического масштабирования правила для облака службы веб-роли или рабочей роли в Azure."
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
ms.openlocfilehash: 265f4c8ec5e1ec2f85585df25f18cd0d0c9946a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-portal"></a><span data-ttu-id="fb23d-103">Как tooconfigure автоматическое масштабирование для облачной службы в портале hello</span><span class="sxs-lookup"><span data-stu-id="fb23d-103">How tooconfigure auto scaling for a Cloud Service in hello portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fb23d-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="fb23d-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="fb23d-105">Классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="fb23d-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="fb23d-106">Для рабочей роли облачной службы можно задать условия, которые активируют операции масштабировании.</span><span class="sxs-lookup"><span data-stu-id="fb23d-106">Conditions can be set for a cloud service worker role that trigger a scale in or out operation.</span></span> <span data-ttu-id="fb23d-107">Hello условия для hello роли могут основываться на hello ЦП, диск или сетевой нагрузки hello роли.</span><span class="sxs-lookup"><span data-stu-id="fb23d-107">hello conditions for hello role can be based on hello CPU, disk, or network load of hello role.</span></span> <span data-ttu-id="fb23d-108">Можно также задать условие основании сообщения очереди или hello метрикой другой Azure ресурс связанную с вашей подпиской.</span><span class="sxs-lookup"><span data-stu-id="fb23d-108">You can also set a condition based on a message queue or hello metric of some other Azure resource associated with your subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="fb23d-109">Эта статья посвящена веб-ролям и рабочим ролям облачной службы.</span><span class="sxs-lookup"><span data-stu-id="fb23d-109">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="fb23d-110">Виртуальные машины (классические), создаваемые напрямую, размещаются в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="fb23d-110">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="fb23d-111">Стандартную виртуальную машину можно масштабировать, связав ее с [группой доступности](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) и включив или отключив ее вручную.</span><span class="sxs-lookup"><span data-stu-id="fb23d-111">You can scale a standard virtual machine by associating it with an [availability set](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) and manually turn them on or off.</span></span>

## <a name="considerations"></a><span data-ttu-id="fb23d-112">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="fb23d-112">Considerations</span></span>
<span data-ttu-id="fb23d-113">Рекомендуется использовать следующую информацию, прежде чем настраивать масштабирование приложения hello.</span><span class="sxs-lookup"><span data-stu-id="fb23d-113">You should consider hello following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="fb23d-114">Масштабирование зависит от использования ядер.</span><span class="sxs-lookup"><span data-stu-id="fb23d-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="fb23d-115">Более крупные экземпляры ролей задействуют больше ядер.</span><span class="sxs-lookup"><span data-stu-id="fb23d-115">Larger role instances use more cores.</span></span> <span data-ttu-id="fb23d-116">Можно масштабировать приложения только в течение ограниченного hello ядер для подписки.</span><span class="sxs-lookup"><span data-stu-id="fb23d-116">You can scale an application only within hello limit of cores for your subscription.</span></span> <span data-ttu-id="fb23d-117">Предположим, что ваша подписка имеет ограничение в 20 ядер.</span><span class="sxs-lookup"><span data-stu-id="fb23d-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="fb23d-118">При запуске приложения с двух средних облачные службы (всего 4 ядра) можно только увеличивать масштаб другие развертывания облачной службы в подписке, hello оставшиеся 16 ядер.</span><span class="sxs-lookup"><span data-stu-id="fb23d-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by hello remaining 16 cores.</span></span> <span data-ttu-id="fb23d-119">Дополнительные сведения о размерах см. в статье [Размеры для облачных служб](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="fb23d-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="fb23d-120">Можно настроить масштабирование на основе порогового значения очереди сообщений.</span><span class="sxs-lookup"><span data-stu-id="fb23d-120">You can scale based on a queue message threshold.</span></span> <span data-ttu-id="fb23d-121">Дополнительные сведения о том, как toouse очереди, разделе [как toouse hello службы хранилища очередей](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="fb23d-121">For more information about how toouse queues, see [How toouse hello Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="fb23d-122">Можно также масштабировать другие ресурсы, связанные с подпиской.</span><span class="sxs-lookup"><span data-stu-id="fb23d-122">You can also scale other resources associated with your subscription.</span></span>

* <span data-ttu-id="fb23d-123">tooenable высокий уровень доступности приложения, следует убедиться, развертывается с двумя или более экземпляров роли.</span><span class="sxs-lookup"><span data-stu-id="fb23d-123">tooenable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="fb23d-124">Дополнительные сведения см. в разделе [Соглашения об уровне обслуживания](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="fb23d-124">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>


## <a name="where-scale-is-located"></a><span data-ttu-id="fb23d-125">Где находится функция масштабирования?</span><span class="sxs-lookup"><span data-stu-id="fb23d-125">Where scale is located</span></span>
<span data-ttu-id="fb23d-126">После выбора облачной службы, должен иметь hello облачной службы колонке видимым.</span><span class="sxs-lookup"><span data-stu-id="fb23d-126">After you select your cloud service, you should have hello cloud service blade visible.</span></span>

1. <span data-ttu-id="fb23d-127">В колонке службы облака hello на hello **роли и экземпляры** плитки, выберите hello имя hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="fb23d-127">On hello cloud service blade, on hello **Roles and Instances** tile, select hello name of hello cloud service.</span></span>   
   <span data-ttu-id="fb23d-128">**ВАЖНЫЕ**: сделать убедиться, что облако hello tooclick службы роли, не hello экземпляра роли под hello роли.</span><span class="sxs-lookup"><span data-stu-id="fb23d-128">**IMPORTANT**: Make sure tooclick hello cloud service role, not hello role instance that is below hello role.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. <span data-ttu-id="fb23d-129">Выберите hello **шкалы** плитки.</span><span class="sxs-lookup"><span data-stu-id="fb23d-129">Select hello **scale** tile.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a><span data-ttu-id="fb23d-130">Автоматическое масштабирование</span><span class="sxs-lookup"><span data-stu-id="fb23d-130">Automatic scale</span></span>
<span data-ttu-id="fb23d-131">Параметры масштабирования для роли можно настроить с помощью двух режимов — **ручной** или **автоматический**.</span><span class="sxs-lookup"><span data-stu-id="fb23d-131">You can configure scale settings for a role with either two modes **manual** or **automatic**.</span></span> <span data-ttu-id="fb23d-132">Руководства — как и следовало ожидать, задать hello абсолютное количество экземпляров.</span><span class="sxs-lookup"><span data-stu-id="fb23d-132">Manual is as you would expect, you set hello absolute count of instances.</span></span> <span data-ttu-id="fb23d-133">Однако, автоматическое позволяет tooset, правила, управляющие, как и на гораздо вам следует использовать масштабирование.</span><span class="sxs-lookup"><span data-stu-id="fb23d-133">Automatic however allows you tooset rules that govern how and by how much you should scale.</span></span>

<span data-ttu-id="fb23d-134">Набор hello **масштабирования по** параметр слишком**правила расписания и производительности**.</span><span class="sxs-lookup"><span data-stu-id="fb23d-134">Set hello **Scale by** option too**schedule and performance rules**.</span></span>

![Параметры масштабирования облачных служб с профилем и правилом](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. <span data-ttu-id="fb23d-136">Существующий профиль.</span><span class="sxs-lookup"><span data-stu-id="fb23d-136">An existing profile.</span></span>
2. <span data-ttu-id="fb23d-137">Добавьте правило для hello родительским профилем.</span><span class="sxs-lookup"><span data-stu-id="fb23d-137">Add a rule for hello parent profile.</span></span>
3. <span data-ttu-id="fb23d-138">Добавьте другой профиль.</span><span class="sxs-lookup"><span data-stu-id="fb23d-138">Add another profile.</span></span>

<span data-ttu-id="fb23d-139">Выберите **Добавить профиль**.</span><span class="sxs-lookup"><span data-stu-id="fb23d-139">Select **Add Profile**.</span></span> <span data-ttu-id="fb23d-140">Hello профиль определяет режим, который требуется toouse hello шкалы: **всегда**, **повторения**, **фиксированной даты**.</span><span class="sxs-lookup"><span data-stu-id="fb23d-140">hello profile determines which mode you want toouse for hello scale: **always**, **recurrence**, **fixed date**.</span></span>

<span data-ttu-id="fb23d-141">После настройки профиля hello и правила, выберите hello **Сохранить** значок вверху hello.</span><span class="sxs-lookup"><span data-stu-id="fb23d-141">After you have configured hello profile and rules, select hello **Save** icon at hello top.</span></span>

#### <a name="profile"></a><span data-ttu-id="fb23d-142">Профиль</span><span class="sxs-lookup"><span data-stu-id="fb23d-142">Profile</span></span>
<span data-ttu-id="fb23d-143">профиль Hello задает минимальное и максимальное экземпляров для hello масштабирования и также когда активна этого диапазона шкалы.</span><span class="sxs-lookup"><span data-stu-id="fb23d-143">hello profile sets minimum and maximum instances for hello scale, and also when this scale range is active.</span></span>

* <span data-ttu-id="fb23d-144">**Всегда**</span><span class="sxs-lookup"><span data-stu-id="fb23d-144">**Always**</span></span>

    <span data-ttu-id="fb23d-145">Всегда сохраняйте этот диапазон доступных экземпляров.</span><span class="sxs-lookup"><span data-stu-id="fb23d-145">Always keep this range of instances available.</span></span>  

    ![Облачная служба, которая масштабируется всегда](./media/cloud-services-how-to-scale-portal/select-always.png)
* <span data-ttu-id="fb23d-147">**Периодичность**</span><span class="sxs-lookup"><span data-stu-id="fb23d-147">**Recurrence**</span></span>

    <span data-ttu-id="fb23d-148">Выберите набор дней недели tooscale hello.</span><span class="sxs-lookup"><span data-stu-id="fb23d-148">Choose a set of days of hello week tooscale.</span></span>

    ![Облачная служба, которая масштабируется с заданной периодичностью](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* <span data-ttu-id="fb23d-150">**Фиксированная дата**</span><span class="sxs-lookup"><span data-stu-id="fb23d-150">**Fixed Date**</span></span>

    <span data-ttu-id="fb23d-151">Роль hello tooscale диапазон фиксированной даты.</span><span class="sxs-lookup"><span data-stu-id="fb23d-151">A fixed date range tooscale hello role.</span></span>

    ![Облачная служба, которая масштабируется в фиксированную дату](./media/cloud-services-how-to-scale-portal/select-fixed.png)

<span data-ttu-id="fb23d-153">После настройки профиля hello выберите hello **ОК** кнопку в нижней части hello колонка профиля hello.</span><span class="sxs-lookup"><span data-stu-id="fb23d-153">After you have configured hello profile, select hello **OK** button at hello bottom of hello profile blade.</span></span>

#### <a name="rule"></a><span data-ttu-id="fb23d-154">правило;</span><span class="sxs-lookup"><span data-stu-id="fb23d-154">Rule</span></span>
<span data-ttu-id="fb23d-155">Правила будут добавлены tooa профиль и представляют условие, которое запускает hello шкалы.</span><span class="sxs-lookup"><span data-stu-id="fb23d-155">Rules are added tooa profile and represent a condition that triggers hello scale.</span></span>

<span data-ttu-id="fb23d-156">триггер правила Hello основан на метрику hello облачной службы (ЦП, активности диска или сетевой активности) можно добавить условное значение toowhich.</span><span class="sxs-lookup"><span data-stu-id="fb23d-156">hello rule trigger is based on a metric of hello cloud service (CPU usage, disk activity, or network activity) toowhich you can add a conditional value.</span></span> <span data-ttu-id="fb23d-157">Кроме того, может иметь триггер hello основании сообщения очереди или hello метрикой другой Azure ресурс связанную с вашей подпиской.</span><span class="sxs-lookup"><span data-stu-id="fb23d-157">Additionally you can have hello trigger based on a message queue or hello metric of some other Azure resource associated with your subscription.</span></span>

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

<span data-ttu-id="fb23d-158">После настройки правила hello выберите hello **ОК** кнопку в нижней части hello колонка правило hello.</span><span class="sxs-lookup"><span data-stu-id="fb23d-158">After you have configured hello rule, select hello **OK** button at hello bottom of hello rule blade.</span></span>

## <a name="back-toomanual-scale"></a><span data-ttu-id="fb23d-159">Масштаб toomanual назад</span><span class="sxs-lookup"><span data-stu-id="fb23d-159">Back toomanual scale</span></span>
<span data-ttu-id="fb23d-160">Перейдите toohello [параметры масштабирования](#where-scale-is-located) и набор hello **масштабирования по** параметр слишком**число экземпляров, вводимое вручную**.</span><span class="sxs-lookup"><span data-stu-id="fb23d-160">Navigate toohello [scale settings](#where-scale-is-located) and set hello **Scale by** option too**an instance count that I enter manually**.</span></span>

![Параметры масштабирования облачных служб с профилем и правилом](./media/cloud-services-how-to-scale-portal/manual-basics.png)

<span data-ttu-id="fb23d-162">Этот параметр удаляет автоматического масштабирования из роли hello и вы можете задать число экземпляров hello напрямую.</span><span class="sxs-lookup"><span data-stu-id="fb23d-162">This setting removes automated scaling from hello role and then you can set hello instance count directly.</span></span>

1. <span data-ttu-id="fb23d-163">параметр масштабирования (ручные или автоматические) Hello.</span><span class="sxs-lookup"><span data-stu-id="fb23d-163">hello scale (manual or automated) option.</span></span>
2. <span data-ttu-id="fb23d-164">Роль экземпляра ползунок tooset hello экземпляров tooscale для.</span><span class="sxs-lookup"><span data-stu-id="fb23d-164">A role instance slider tooset hello instances tooscale to.</span></span>
3. <span data-ttu-id="fb23d-165">Экземпляры hello tooscale роли для.</span><span class="sxs-lookup"><span data-stu-id="fb23d-165">Instances of hello role tooscale to.</span></span>

<span data-ttu-id="fb23d-166">После настройки параметров масштабирования hello выберите hello **Сохранить** значок вверху hello.</span><span class="sxs-lookup"><span data-stu-id="fb23d-166">After you have configured hello scale settings, select hello **Save** icon at hello top.</span></span>
