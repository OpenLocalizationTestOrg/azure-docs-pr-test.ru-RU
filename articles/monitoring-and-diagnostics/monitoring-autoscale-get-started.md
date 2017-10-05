---
title: "Начало работы с автомасштабированием в Azure | Документация Майкрософт"
description: "Сведения о масштабировании ресурсов в Azure."
author: rajram
manager: rboucher
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: rajram
ms.openlocfilehash: 68cb624b3ef4a77e7cfc949979e0b1949c2e5535
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-autoscale-in-azure"></a><span data-ttu-id="494b2-103">Начало работы с автомасштабированием в Azure</span><span class="sxs-lookup"><span data-stu-id="494b2-103">Get started with Autoscale in Azure</span></span>
<span data-ttu-id="494b2-104">В этой статье описывается, как настроить автомасштабирование для ресурса на портале Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="494b2-104">This article describes how to set up your Autoscale settings for your resource in the Microsoft Azure portal.</span></span>

<span data-ttu-id="494b2-105">Автомасштабирование Azure Monitor применяется только к масштабируемым наборам виртуальных машин, облачным службам, планам и средам службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="494b2-105">Azure Monitor Autoscale applies only to virtual machine scale sets, cloud services, Azure App Service plans, and App Service environments.</span></span> 

## <a name="discover-the-autoscale-settings-in-your-subscription"></a><span data-ttu-id="494b2-106">Обнаружение параметров автомасштабирования в подписках</span><span class="sxs-lookup"><span data-stu-id="494b2-106">Discover the Autoscale settings in your subscription</span></span>
<span data-ttu-id="494b2-107">Azure Monitor дает возможность обнаружить все ресурсы, для которых можно применить автомасштабирование.</span><span class="sxs-lookup"><span data-stu-id="494b2-107">You can discover all the resources for which Autoscale is applicable in Azure Monitor.</span></span> <span data-ttu-id="494b2-108">Для этой цели вам нужно выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="494b2-108">Use the following steps for a step-by-step walkthrough:</span></span>

1. <span data-ttu-id="494b2-109">Откройте [портал Azure.][1]</span><span class="sxs-lookup"><span data-stu-id="494b2-109">Open the [Azure portal.][1]</span></span>
2. <span data-ttu-id="494b2-110">Щелкните значок Azure на левой панели.</span><span class="sxs-lookup"><span data-stu-id="494b2-110">Click the Azure Monitor icon in the left pane.</span></span>
  <span data-ttu-id="494b2-111">![Открытие Azure Monitor][2]</span><span class="sxs-lookup"><span data-stu-id="494b2-111">![Open Azure Monitor][2]</span></span>
3. <span data-ttu-id="494b2-112">Выберите раздел **Автомасштабирование**, чтобы просмотреть все ресурсы, для которых применимо автомасштабирование, и текущее состояние этой настройки для них.</span><span class="sxs-lookup"><span data-stu-id="494b2-112">Click **Autoscale** to view all the resources for which Autoscale is applicable, along with their current Autoscale status.</span></span>
  <span data-ttu-id="494b2-113">![Открытие раздела "Автомасштабирование" в Azure Monitor][3]</span><span class="sxs-lookup"><span data-stu-id="494b2-113">![Discover Autoscale in Azure Monitor][3]</span></span>

<span data-ttu-id="494b2-114">Панель фильтрации в верхней части страницы позволяет сузить список до определенной группы ресурсов, отдельных типов ресурсов или одного конкретного ресурса.</span><span class="sxs-lookup"><span data-stu-id="494b2-114">You can use the filter pane at the top to scope down the list to select resources in a specific resource group, specific resource types, or a specific resource.</span></span>

<span data-ttu-id="494b2-115">Для каждого ресурса вы увидите здесь текущее количество экземпляров и состояние автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="494b2-115">For each resource, you will find the current instance count and the Autoscale status.</span></span> <span data-ttu-id="494b2-116">Состояние автомасштабирования может принимать одно из перечисленных ниже значений.</span><span class="sxs-lookup"><span data-stu-id="494b2-116">The Autoscale status can be:</span></span>

- <span data-ttu-id="494b2-117">**Не настроено**. Автомасштабирование еще не настроено для этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="494b2-117">**Not configured**: You have not enabled Autoscale yet for this resource.</span></span>
- <span data-ttu-id="494b2-118">**Включено**. Автомасштабирование включено для этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="494b2-118">**Enabled**: You have enabled Autoscale for this resource.</span></span>
- <span data-ttu-id="494b2-119">**Отключено**. Автомасштабирование отключено для этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="494b2-119">**Disabled**: You have disabled Autoscale for this resource.</span></span>

## <a name="create-your-first-autoscale-setting"></a><span data-ttu-id="494b2-120">Создание параметра автомасштабирования</span><span class="sxs-lookup"><span data-stu-id="494b2-120">Create your first Autoscale setting</span></span>

<span data-ttu-id="494b2-121">Теперь выполним простые пошаговые инструкции для создания параметра автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="494b2-121">Let's now go through a simple step-by-step walkthrough to create your first Autoscale setting.</span></span>

1. <span data-ttu-id="494b2-122">В Azure Monitor откройте колонку **Автомасштабирование** и выберите ресурс, который нужно масштабировать.</span><span class="sxs-lookup"><span data-stu-id="494b2-122">Open the **Autoscale** blade in Azure Monitor and select a resource that you want to scale.</span></span> <span data-ttu-id="494b2-123">(В примере ниже используется план службы приложений, связанный с веб-приложением.</span><span class="sxs-lookup"><span data-stu-id="494b2-123">(The following steps use an App Service plan associated with a web app.</span></span> <span data-ttu-id="494b2-124">Вы можете [за пять минут создать первое веб-приложение ASP.NET в Azure][4]).</span><span class="sxs-lookup"><span data-stu-id="494b2-124">You can [create your first ASP.NET web app in Azure in 5 minutes.][4])</span></span>
2. <span data-ttu-id="494b2-125">Как видите, текущее количество экземпляров имеет значение 1.</span><span class="sxs-lookup"><span data-stu-id="494b2-125">Note that the current instance count is 1.</span></span> <span data-ttu-id="494b2-126">Щелкните **Включить автомасштабирование**.</span><span class="sxs-lookup"><span data-stu-id="494b2-126">Click **Enable autoscale**.</span></span>
  <span data-ttu-id="494b2-127">![Параметр масштабирования для нового веб-приложения][5]</span><span class="sxs-lookup"><span data-stu-id="494b2-127">![Scale setting for new web app][5]</span></span>
3. <span data-ttu-id="494b2-128">Укажите имя для параметра масштабирования и щелкните **Добавить правило**.</span><span class="sxs-lookup"><span data-stu-id="494b2-128">Provide a name for the scale setting, and then click **Add a rule**.</span></span> <span data-ttu-id="494b2-129">Параметры правила масштабирования откроются в виде контекстной области справа.</span><span class="sxs-lookup"><span data-stu-id="494b2-129">Notice the scale rule options that open as a context pane on the right side.</span></span> <span data-ttu-id="494b2-130">По умолчанию устанавливается следующее правило: количество экземпляров увеличивается на 1, когда загрузка ЦП для ресурса превышает уровень 70 %.</span><span class="sxs-lookup"><span data-stu-id="494b2-130">By default, this sets the option to scale your instance count by 1 if the CPU percentage of the resource exceeds 70 percent.</span></span> <span data-ttu-id="494b2-131">Не изменяйте эти значения по умолчанию, а просто нажмите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="494b2-131">Leave it at its default values and click **Add**.</span></span>
  <span data-ttu-id="494b2-132">![Создание параметра масштабирования для веб-приложения][6]</span><span class="sxs-lookup"><span data-stu-id="494b2-132">![Create scale setting for a web app][6]</span></span>
4. <span data-ttu-id="494b2-133">Итак, вы создали первое правило масштабирования.</span><span class="sxs-lookup"><span data-stu-id="494b2-133">You've now created your first scale rule.</span></span> <span data-ttu-id="494b2-134">В этом же интерфейсе вы увидите некоторые рекомендация по настройке, например: "Рекомендуется настроить не меньше одного правила увеличения масштаба".</span><span class="sxs-lookup"><span data-stu-id="494b2-134">Note that the UX recommends best practices and states that "It is recommended to have at least one scale in rule."</span></span> <span data-ttu-id="494b2-135">Для этого выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="494b2-135">To do so:</span></span>
  
    <span data-ttu-id="494b2-136">а.</span><span class="sxs-lookup"><span data-stu-id="494b2-136">a.</span></span> <span data-ttu-id="494b2-137">Щелкните **Добавить правило**.</span><span class="sxs-lookup"><span data-stu-id="494b2-137">Click **Add a rule**.</span></span> 

    <span data-ttu-id="494b2-138">b.</span><span class="sxs-lookup"><span data-stu-id="494b2-138">b.</span></span> <span data-ttu-id="494b2-139">Для параметра **Оператор** установите значение **Меньше, чем**.</span><span class="sxs-lookup"><span data-stu-id="494b2-139">Set **Operator** to **Less than**.</span></span>

    <span data-ttu-id="494b2-140">c.</span><span class="sxs-lookup"><span data-stu-id="494b2-140">c.</span></span> <span data-ttu-id="494b2-141">Для параметра **Пороговое значение** задайте значение **20**.</span><span class="sxs-lookup"><span data-stu-id="494b2-141">Set **Threshold** to **20**.</span></span>

    <span data-ttu-id="494b2-142">d.</span><span class="sxs-lookup"><span data-stu-id="494b2-142">d.</span></span> <span data-ttu-id="494b2-143">Для параметра **Операция** установите значение **Уменьшить счетчик на**.</span><span class="sxs-lookup"><span data-stu-id="494b2-143">Set **Operation** to **Decrease count by**.</span></span>

   <span data-ttu-id="494b2-144">Теперь у вас есть параметр масштабирования, который изменяет масштаб в зависимости от показателей загрузки ЦП.</span><span class="sxs-lookup"><span data-stu-id="494b2-144">You should now have a scale setting that scales out/scales in based on CPU usage.</span></span>
   <span data-ttu-id="494b2-145">![Масштабирование на основе загрузки ЦП][8]</span><span class="sxs-lookup"><span data-stu-id="494b2-145">![Scale based on CPU][8]</span></span>
5. <span data-ttu-id="494b2-146">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="494b2-146">Click **Save**.</span></span>

<span data-ttu-id="494b2-147">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="494b2-147">Congratulations!</span></span> <span data-ttu-id="494b2-148">Вы успешно создали первый параметр масштабирования, который будет автомасштабировать веб-приложение, исходя из загрузки ЦП.</span><span class="sxs-lookup"><span data-stu-id="494b2-148">You've now successfully created your first scale setting to autoscale your web app based on CPU usage.</span></span>

> [!NOTE] 
> <span data-ttu-id="494b2-149">Эти действия можно применить для настройки масштабируемого набора виртуальных машин или ролей облачной службы.</span><span class="sxs-lookup"><span data-stu-id="494b2-149">The same steps are applicable to get started with a virtual machine scale set or cloud service role.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="494b2-150">Дополнительные рекомендации</span><span class="sxs-lookup"><span data-stu-id="494b2-150">Other considerations</span></span>
### <a name="scale-based-on-a-schedule"></a><span data-ttu-id="494b2-151">Масштабирование на основе расписания</span><span class="sxs-lookup"><span data-stu-id="494b2-151">Scale based on a schedule</span></span>
<span data-ttu-id="494b2-152">Помимо загрузки ЦП, в параметрах автомасштабирования можно учитывать определенные дни недели.</span><span class="sxs-lookup"><span data-stu-id="494b2-152">In addition to scale based on CPU, you can set your scale differently for specific days of the week.</span></span>

1. <span data-ttu-id="494b2-153">Щелкните **Add a scale condition** (Добавить условие масштабирования).</span><span class="sxs-lookup"><span data-stu-id="494b2-153">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="494b2-154">Настройка режима масштабирования и правил выполняется так же, как и для условий по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="494b2-154">Setting the scale mode and the rules is the same as the default condition.</span></span>
3. <span data-ttu-id="494b2-155">Выберите **Повторять в определенные дни**, чтобы настроить расписание.</span><span class="sxs-lookup"><span data-stu-id="494b2-155">Select **Repeat specific days** for the schedule.</span></span>
4. <span data-ttu-id="494b2-156">Выберите дни и время для начала и окончания периода, в который будет применяться условие масштабирования.</span><span class="sxs-lookup"><span data-stu-id="494b2-156">Select the days and the start/end time for when the scale condition should be applied.</span></span>

![Условие масштабирования на основе расписания][9]
### <a name="scale-differently-on-specific-dates"></a><span data-ttu-id="494b2-158">Масштабирование в определенные даты</span><span class="sxs-lookup"><span data-stu-id="494b2-158">Scale differently on specific dates</span></span>
<span data-ttu-id="494b2-159">Помимо загрузки ЦП, в параметрах автомасштабирования можно учитывать определенные даты.</span><span class="sxs-lookup"><span data-stu-id="494b2-159">In addition to scale based on CPU, you can set your scale differently for specific dates.</span></span>

1. <span data-ttu-id="494b2-160">Щелкните **Add a scale condition** (Добавить условие масштабирования).</span><span class="sxs-lookup"><span data-stu-id="494b2-160">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="494b2-161">Настройка режима масштабирования и правил выполняется так же, как и для условий по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="494b2-161">Setting the scale mode and the rules is the same as the default condition.</span></span>
3. <span data-ttu-id="494b2-162">Выберите **Укажите даты начала и окончания**, чтобы настроить расписание.</span><span class="sxs-lookup"><span data-stu-id="494b2-162">Select **Specify start/end dates** for the schedule.</span></span>
4. <span data-ttu-id="494b2-163">Выберите даты для начала и окончания периода, в который будет применяться условие масштабирования.</span><span class="sxs-lookup"><span data-stu-id="494b2-163">Select the start/end dates and the start/end time for when the scale condition should be applied.</span></span>

![Условие масштабирования на основе дат][10]

### <a name="view-the-scale-history-of-your-resource"></a><span data-ttu-id="494b2-165">Просмотр журнала масштабирования ресурса</span><span class="sxs-lookup"><span data-stu-id="494b2-165">View the scale history of your resource</span></span>
<span data-ttu-id="494b2-166">Каждый раз, когда масштабируется ресурс, в журнале действий регистрируется событие.</span><span class="sxs-lookup"><span data-stu-id="494b2-166">Whenever your resource is scaled up or down, an event is logged in the activity log.</span></span> <span data-ttu-id="494b2-167">Вы можете просмотреть журнал масштабирования ресурса за последние 24 часа, открыв вкладку **Журнал запусков**.</span><span class="sxs-lookup"><span data-stu-id="494b2-167">You can view the scale history of your resource for the past 24 hours by switching to the **Run history** tab.</span></span>

![Журнал выполнения][11]

<span data-ttu-id="494b2-169">Если вы хотите просмотреть полный журнал масштабирования (до 90 дней), выберите действие **Щелкните здесь, чтобы просмотреть дополнительные сведения**.</span><span class="sxs-lookup"><span data-stu-id="494b2-169">If you want to view the complete scale history (for up to 90 days), select **Click here to see more details**.</span></span> <span data-ttu-id="494b2-170">Откроется журнал действий автомасштабирования, в котором уже выбраны нужный ресурс и категория.</span><span class="sxs-lookup"><span data-stu-id="494b2-170">The activity log opens, with Autoscale pre-selected for your resource and category.</span></span>

### <a name="view-the-scale-definition-of-your-resource"></a><span data-ttu-id="494b2-171">Просмотр определения масштабирования для ресурса</span><span class="sxs-lookup"><span data-stu-id="494b2-171">View the scale definition of your resource</span></span>
<span data-ttu-id="494b2-172">Автомасштабирование считается ресурсом Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="494b2-172">Autoscale is an Azure Resource Manager resource.</span></span> <span data-ttu-id="494b2-173">Определение масштабирования можно просмотреть в формате JSON. Для этого откройте вкладку **JSON**.</span><span class="sxs-lookup"><span data-stu-id="494b2-173">You can view the scale definition in JSON by switching to the **JSON** tab.</span></span>

![Определение масштабирования][12]

<span data-ttu-id="494b2-175">При необходимости можно внести изменения в JSON напрямую.</span><span class="sxs-lookup"><span data-stu-id="494b2-175">You can make changes in JSON directly, if required.</span></span> <span data-ttu-id="494b2-176">Эти изменения будут применены, как только вы их сохраните.</span><span class="sxs-lookup"><span data-stu-id="494b2-176">These changes will be reflected after you save them.</span></span>

### <a name="disable-autoscale-and-manually-scale-your-instances"></a><span data-ttu-id="494b2-177">Отключение автомасштабирования и масштабирование экземпляров вручную</span><span class="sxs-lookup"><span data-stu-id="494b2-177">Disable Autoscale and manually scale your instances</span></span>
<span data-ttu-id="494b2-178">Иногда необходимо отключить действующий параметр масштабирования и масштабировать ресурс вручную.</span><span class="sxs-lookup"><span data-stu-id="494b2-178">There might be times when you want to disable your current scale setting and manually scale your resource.</span></span>

<span data-ttu-id="494b2-179">Для этого нажмите **Отключить автомасштабирование** в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="494b2-179">Click the **Disable autoscale** button at the top.</span></span>
<span data-ttu-id="494b2-180">![Отключение автомасштабирования][13]</span><span class="sxs-lookup"><span data-stu-id="494b2-180">![Disable Autoscale][13]</span></span>

> [!NOTE] 
> <span data-ttu-id="494b2-181">Это действие отключает настроенную конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="494b2-181">This option disables your configuration.</span></span> <span data-ttu-id="494b2-182">Вы всегда можете вернуть прежний режим, включив автомасштабирование.</span><span class="sxs-lookup"><span data-stu-id="494b2-182">However, you can get back to it after you enable Autoscale again.</span></span> 

<span data-ttu-id="494b2-183">При отключенном автомасштабировании вы можете вручную задать нужное количество экземпляров.</span><span class="sxs-lookup"><span data-stu-id="494b2-183">You can now set the number of instances that you want to scale to manually.</span></span>

![Настройка масштабирования вручную][14]

<span data-ttu-id="494b2-185">Автомасштабирование можно возобновить в любой момент, щелкнув здесь же **Включить автомасштабирование**, а затем — **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="494b2-185">You can always return to Autoscale by clicking **Enable autoscale** and then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="494b2-186">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="494b2-186">Next steps</span></span>
- <span data-ttu-id="494b2-187">[Создайте оповещение журнала действий, чтобы отслеживать все операции системы автомасштабирования в подписке](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="494b2-187">[Create an Activity Log Alert to monitor all Autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)</span></span>
- <span data-ttu-id="494b2-188">[Создайте оповещение журнала действий, чтобы отслеживать все сбои автомасштабирования в подписке](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="494b2-188">[Create an Activity Log Alert to monitor all failed Autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)</span></span>

<!--Reference-->
[1]:https://portal.azure.com
[2]: ./media/monitoring-autoscale-get-started/azure-monitor-launch.png
[3]: ./media/monitoring-autoscale-get-started/discover-autoscale-azure-monitor.png
[4]: https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-get-started-dotnet
[5]: ./media/monitoring-autoscale-get-started/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-get-started/create-scale-setting-web-app.png
[7]: ./media/monitoring-autoscale-get-started/scale-in-recommendation.png
[8]: ./media/monitoring-autoscale-get-started/scale-based-on-cpu.png
[9]: ./media/monitoring-autoscale-get-started/scale-condition-schedule.png
[10]: ./media/monitoring-autoscale-get-started/scale-condition-dates.png
[11]: ./media/monitoring-autoscale-get-started/scale-history.png
[12]: ./media/monitoring-autoscale-get-started/scale-definition-json.png
[13]: ./media/monitoring-autoscale-get-started/disable-autoscale.png
[14]: ./media/monitoring-autoscale-get-started/set-manualscale.png

