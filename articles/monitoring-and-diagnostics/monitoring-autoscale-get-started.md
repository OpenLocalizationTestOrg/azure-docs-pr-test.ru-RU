---
title: "aaaGet к выполнению автоматического масштабирования в Azure | Документы Microsoft"
description: "Узнайте, как tooscale ресурс в Azure."
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
ms.openlocfilehash: 6b3c3f4529018dcaf9691c538fec63dfbb3cea06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-autoscale-in-azure"></a><span data-ttu-id="eb2ea-103">Начало работы с автомасштабированием в Azure</span><span class="sxs-lookup"><span data-stu-id="eb2ea-103">Get started with Autoscale in Azure</span></span>
<span data-ttu-id="eb2ea-104">В этой статье описывается как tooset копию параметров автоматического масштабирования для ресурса на портале Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-104">This article describes how tooset up your Autoscale settings for your resource in hello Microsoft Azure portal.</span></span>

<span data-ttu-id="eb2ea-105">Azure автомасштабирования монитор применяется только наборы масштабирования toovirtual машины, облачных служб, планы службы приложений Azure и среды службы приложений.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-105">Azure Monitor Autoscale applies only toovirtual machine scale sets, cloud services, Azure App Service plans, and App Service environments.</span></span> 

## <a name="discover-hello-autoscale-settings-in-your-subscription"></a><span data-ttu-id="eb2ea-106">Обнаружение параметров автоматического масштабирования hello в подписке</span><span class="sxs-lookup"><span data-stu-id="eb2ea-106">Discover hello Autoscale settings in your subscription</span></span>
<span data-ttu-id="eb2ea-107">Вы можете узнать все ресурсы hello, для которых применяется автоматического масштабирования в Azure монитора.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-107">You can discover all hello resources for which Autoscale is applicable in Azure Monitor.</span></span> <span data-ttu-id="eb2ea-108">Используйте следующие шаги для пошагового руководства hello.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-108">Use hello following steps for a step-by-step walkthrough:</span></span>

1. <span data-ttu-id="eb2ea-109">Откройте hello [портал Azure.][1]</span><span class="sxs-lookup"><span data-stu-id="eb2ea-109">Open hello [Azure portal.][1]</span></span>
2. <span data-ttu-id="eb2ea-110">Щелкните значок монитора Azure hello в левой области hello.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-110">Click hello Azure Monitor icon in hello left pane.</span></span>
  <span data-ttu-id="eb2ea-111">![Открытие Azure Monitor][2]</span><span class="sxs-lookup"><span data-stu-id="eb2ea-111">![Open Azure Monitor][2]</span></span>
3. <span data-ttu-id="eb2ea-112">Нажмите кнопку **автомасштабирования** tooview все hello ресурсы для какой автомасштабирования применяется вместе с их текущее состояние автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-112">Click **Autoscale** tooview all hello resources for which Autoscale is applicable, along with their current Autoscale status.</span></span>
  <span data-ttu-id="eb2ea-113">![Открытие раздела "Автомасштабирование" в Azure Monitor][3]</span><span class="sxs-lookup"><span data-stu-id="eb2ea-113">![Discover Autoscale in Azure Monitor][3]</span></span>

<span data-ttu-id="eb2ea-114">Можно использовать панель фильтра hello в верхнем tooscope hello вниз hello список tooselect ресурсы в определенной группе ресурсов, конкретные типы ресурсов или конкретный ресурс.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-114">You can use hello filter pane at hello top tooscope down hello list tooselect resources in a specific resource group, specific resource types, or a specific resource.</span></span>

<span data-ttu-id="eb2ea-115">Для каждого ресурса можно найти текущее количество экземпляров hello и состояние автомасштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-115">For each resource, you will find hello current instance count and hello Autoscale status.</span></span> <span data-ttu-id="eb2ea-116">состояние автомасштабирования Hello может быть:</span><span class="sxs-lookup"><span data-stu-id="eb2ea-116">hello Autoscale status can be:</span></span>

- <span data-ttu-id="eb2ea-117">**Не настроено**. Автомасштабирование еще не настроено для этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-117">**Not configured**: You have not enabled Autoscale yet for this resource.</span></span>
- <span data-ttu-id="eb2ea-118">**Включено**. Автомасштабирование включено для этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-118">**Enabled**: You have enabled Autoscale for this resource.</span></span>
- <span data-ttu-id="eb2ea-119">**Отключено**. Автомасштабирование отключено для этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-119">**Disabled**: You have disabled Autoscale for this resource.</span></span>

## <a name="create-your-first-autoscale-setting"></a><span data-ttu-id="eb2ea-120">Создание параметра автомасштабирования</span><span class="sxs-lookup"><span data-stu-id="eb2ea-120">Create your first Autoscale setting</span></span>

<span data-ttu-id="eb2ea-121">Теперь давайте через toocreate простые пошаговые первого параметра автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-121">Let's now go through a simple step-by-step walkthrough toocreate your first Autoscale setting.</span></span>

1. <span data-ttu-id="eb2ea-122">Откройте hello **автомасштабирования** колонки в монитор Azure и выберите ресурс, которые должны tooscale.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-122">Open hello **Autoscale** blade in Azure Monitor and select a resource that you want tooscale.</span></span> <span data-ttu-id="eb2ea-123">(hello Далее используется план служб приложений, связанных с веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-123">(hello following steps use an App Service plan associated with a web app.</span></span> <span data-ttu-id="eb2ea-124">Вы можете [за пять минут создать первое веб-приложение ASP.NET в Azure][4]).</span><span class="sxs-lookup"><span data-stu-id="eb2ea-124">You can [create your first ASP.NET web app in Azure in 5 minutes.][4])</span></span>
2. <span data-ttu-id="eb2ea-125">Обратите внимание, что текущее количество экземпляров hello 1.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-125">Note that hello current instance count is 1.</span></span> <span data-ttu-id="eb2ea-126">Щелкните **Включить автомасштабирование**.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-126">Click **Enable autoscale**.</span></span>
  <span data-ttu-id="eb2ea-127">![Параметр масштабирования для нового веб-приложения][5]</span><span class="sxs-lookup"><span data-stu-id="eb2ea-127">![Scale setting for new web app][5]</span></span>
3. <span data-ttu-id="eb2ea-128">Укажите имя для параметра масштаба hello и нажмите кнопку **добавить правило**.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-128">Provide a name for hello scale setting, and then click **Add a rule**.</span></span> <span data-ttu-id="eb2ea-129">Обратите внимание, параметров правил масштабирования hello, откройте в контексте области hello правой стороны.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-129">Notice hello scale rule options that open as a context pane on hello right side.</span></span> <span data-ttu-id="eb2ea-130">По умолчанию это задает tooscale параметр hello экземпляру счетчика на 1, если процент использования ЦП ресурсов hello hello превышает 70 процентов.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-130">By default, this sets hello option tooscale your instance count by 1 if hello CPU percentage of hello resource exceeds 70 percent.</span></span> <span data-ttu-id="eb2ea-131">Не изменяйте эти значения по умолчанию, а просто нажмите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-131">Leave it at its default values and click **Add**.</span></span>
  <span data-ttu-id="eb2ea-132">![Создание параметра масштабирования для веб-приложения][6]</span><span class="sxs-lookup"><span data-stu-id="eb2ea-132">![Create scale setting for a web app][6]</span></span>
4. <span data-ttu-id="eb2ea-133">Итак, вы создали первое правило масштабирования.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-133">You've now created your first scale rule.</span></span> <span data-ttu-id="eb2ea-134">Обратите внимание, что hello UX рекомендует лучших рекомендаций и состояний, «рекомендуется toohave по крайней мере одну шкалу в правиле.»</span><span class="sxs-lookup"><span data-stu-id="eb2ea-134">Note that hello UX recommends best practices and states that "It is recommended toohave at least one scale in rule."</span></span> <span data-ttu-id="eb2ea-135">toodo так:</span><span class="sxs-lookup"><span data-stu-id="eb2ea-135">toodo so:</span></span>
  
    <span data-ttu-id="eb2ea-136">а.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-136">a.</span></span> <span data-ttu-id="eb2ea-137">Щелкните **Добавить правило**.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-137">Click **Add a rule**.</span></span> 

    <span data-ttu-id="eb2ea-138">b.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-138">b.</span></span> <span data-ttu-id="eb2ea-139">Задать **оператор** слишком**меньше, чем**.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-139">Set **Operator** too**Less than**.</span></span>

    <span data-ttu-id="eb2ea-140">c.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-140">c.</span></span> <span data-ttu-id="eb2ea-141">Задать **пороговое значение** слишком**20**.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-141">Set **Threshold** too**20**.</span></span>

    <span data-ttu-id="eb2ea-142">d.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-142">d.</span></span> <span data-ttu-id="eb2ea-143">Задать **операции** слишком**уменьшить число по**.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-143">Set **Operation** too**Decrease count by**.</span></span>

   <span data-ttu-id="eb2ea-144">Теперь у вас есть параметр масштабирования, который изменяет масштаб в зависимости от показателей загрузки ЦП.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-144">You should now have a scale setting that scales out/scales in based on CPU usage.</span></span>
   <span data-ttu-id="eb2ea-145">![Масштабирование на основе загрузки ЦП][8]</span><span class="sxs-lookup"><span data-stu-id="eb2ea-145">![Scale based on CPU][8]</span></span>
5. <span data-ttu-id="eb2ea-146">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-146">Click **Save**.</span></span>

<span data-ttu-id="eb2ea-147">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="eb2ea-147">Congratulations!</span></span> <span data-ttu-id="eb2ea-148">Теперь успешно создана ваш первый параметр tooautoscale шкалы, веб-приложения в зависимости от использования ЦП.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-148">You've now successfully created your first scale setting tooautoscale your web app based on CPU usage.</span></span>

> [!NOTE] 
> <span data-ttu-id="eb2ea-149">Hello же шаги, применимые tooget масштабирования виртуальных машин к выполнению набора или облачной службы роли.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-149">hello same steps are applicable tooget started with a virtual machine scale set or cloud service role.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="eb2ea-150">Дополнительные рекомендации</span><span class="sxs-lookup"><span data-stu-id="eb2ea-150">Other considerations</span></span>
### <a name="scale-based-on-a-schedule"></a><span data-ttu-id="eb2ea-151">Масштабирование на основе расписания</span><span class="sxs-lookup"><span data-stu-id="eb2ea-151">Scale based on a schedule</span></span>
<span data-ttu-id="eb2ea-152">В дополнение к этому tooscale основании ЦП, можно задать шкалу по-разному для определенных дней недели hello.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-152">In addition tooscale based on CPU, you can set your scale differently for specific days of hello week.</span></span>

1. <span data-ttu-id="eb2ea-153">Щелкните **Add a scale condition** (Добавить условие масштабирования).</span><span class="sxs-lookup"><span data-stu-id="eb2ea-153">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="eb2ea-154">Задание режима и hello правил масштабирования hello hello же, как условие по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-154">Setting hello scale mode and hello rules is hello same as hello default condition.</span></span>
3. <span data-ttu-id="eb2ea-155">Выберите **повторите конкретные дни** hello расписания.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-155">Select **Repeat specific days** for hello schedule.</span></span>
4. <span data-ttu-id="eb2ea-156">Выберите дни hello и начальное и конечное время hello применяться условие hello шкалы.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-156">Select hello days and hello start/end time for when hello scale condition should be applied.</span></span>

![Условие масштабирования на основе расписания][9]
### <a name="scale-differently-on-specific-dates"></a><span data-ttu-id="eb2ea-158">Масштабирование в определенные даты</span><span class="sxs-lookup"><span data-stu-id="eb2ea-158">Scale differently on specific dates</span></span>
<span data-ttu-id="eb2ea-159">В дополнение к этому tooscale основании ЦП, можно задать шкалу по-разному для определенных дат.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-159">In addition tooscale based on CPU, you can set your scale differently for specific dates.</span></span>

1. <span data-ttu-id="eb2ea-160">Щелкните **Add a scale condition** (Добавить условие масштабирования).</span><span class="sxs-lookup"><span data-stu-id="eb2ea-160">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="eb2ea-161">Задание режима и hello правил масштабирования hello hello же, как условие по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-161">Setting hello scale mode and hello rules is hello same as hello default condition.</span></span>
3. <span data-ttu-id="eb2ea-162">Выберите **даты начала и окончания укажите** для hello расписания.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-162">Select **Specify start/end dates** for hello schedule.</span></span>
4. <span data-ttu-id="eb2ea-163">Выберите даты начала и завершения hello и начальное и конечное время hello применяться условие hello шкалы.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-163">Select hello start/end dates and hello start/end time for when hello scale condition should be applied.</span></span>

![Условие масштабирования на основе дат][10]

### <a name="view-hello-scale-history-of-your-resource"></a><span data-ttu-id="eb2ea-165">Просмотр журнала шкалы hello ресурса</span><span class="sxs-lookup"><span data-stu-id="eb2ea-165">View hello scale history of your resource</span></span>
<span data-ttu-id="eb2ea-166">Каждый раз, когда ресурс масштабируется вверх или вниз, событие заносится в журнал действий hello.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-166">Whenever your resource is scaled up or down, an event is logged in hello activity log.</span></span> <span data-ttu-id="eb2ea-167">Можно просмотреть hello шкалы историю ресурса для hello за последние 24 часа, переключившись toohello **журнал выполнения** вкладки.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-167">You can view hello scale history of your resource for hello past 24 hours by switching toohello **Run history** tab.</span></span>

![Журнал выполнения][11]

<span data-ttu-id="eb2ea-169">Если требуется tooview hello шкалы полный журнал (для вверх too90 дней), выберите **щелкните здесь toosee Дополнительные сведения о**.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-169">If you want tooview hello complete scale history (for up too90 days), select **Click here toosee more details**.</span></span> <span data-ttu-id="eb2ea-170">Открывает журнал действий Hello Автомасштабирование заранее выбранные для ресурсов и категории.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-170">hello activity log opens, with Autoscale pre-selected for your resource and category.</span></span>

### <a name="view-hello-scale-definition-of-your-resource"></a><span data-ttu-id="eb2ea-171">Просмотр определения шкалы hello ресурса</span><span class="sxs-lookup"><span data-stu-id="eb2ea-171">View hello scale definition of your resource</span></span>
<span data-ttu-id="eb2ea-172">Автомасштабирование считается ресурсом Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-172">Autoscale is an Azure Resource Manager resource.</span></span> <span data-ttu-id="eb2ea-173">Можно просмотреть определение шкалы hello в JSON, переключившись toohello **JSON** вкладки.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-173">You can view hello scale definition in JSON by switching toohello **JSON** tab.</span></span>

![Определение масштабирования][12]

<span data-ttu-id="eb2ea-175">При необходимости можно внести изменения в JSON напрямую.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-175">You can make changes in JSON directly, if required.</span></span> <span data-ttu-id="eb2ea-176">Эти изменения будут применены, как только вы их сохраните.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-176">These changes will be reflected after you save them.</span></span>

### <a name="disable-autoscale-and-manually-scale-your-instances"></a><span data-ttu-id="eb2ea-177">Отключение автомасштабирования и масштабирование экземпляров вручную</span><span class="sxs-lookup"><span data-stu-id="eb2ea-177">Disable Autoscale and manually scale your instances</span></span>
<span data-ttu-id="eb2ea-178">Может возникнуть раз при необходимости toodisable текущие параметры масштабирования и масштабировать ресурс вручную.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-178">There might be times when you want toodisable your current scale setting and manually scale your resource.</span></span>

<span data-ttu-id="eb2ea-179">Нажмите кнопку hello **отключения автоматического масштабирования** кнопку вверху hello.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-179">Click hello **Disable autoscale** button at hello top.</span></span>
<span data-ttu-id="eb2ea-180">![Отключение автомасштабирования][13]</span><span class="sxs-lookup"><span data-stu-id="eb2ea-180">![Disable Autoscale][13]</span></span>

> [!NOTE] 
> <span data-ttu-id="eb2ea-181">Это действие отключает настроенную конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-181">This option disables your configuration.</span></span> <span data-ttu-id="eb2ea-182">Тем не менее вы можете вернуться tooit при включении автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-182">However, you can get back tooit after you enable Autoscale again.</span></span> 

<span data-ttu-id="eb2ea-183">Теперь можно задать hello число экземпляров, что требуется tooscale toomanually.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-183">You can now set hello number of instances that you want tooscale toomanually.</span></span>

![Настройка масштабирования вручную][14]

<span data-ttu-id="eb2ea-185">TooAutoscale всегда можно вернуться, щелкнув **включите Автомасштабирование** и затем **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="eb2ea-185">You can always return tooAutoscale by clicking **Enable autoscale** and then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb2ea-186">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eb2ea-186">Next steps</span></span>
- [<span data-ttu-id="eb2ea-187">Создать предупреждение журналов действий toomonitor всех операций автомасштабирования обработчика для одной подписки</span><span class="sxs-lookup"><span data-stu-id="eb2ea-187">Create an Activity Log Alert toomonitor all Autoscale engine operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [<span data-ttu-id="eb2ea-188">Создать предупреждение журналов действий toomonitor всех неудачных операций масштабирования в/scale out автомасштабирования по подписке</span><span class="sxs-lookup"><span data-stu-id="eb2ea-188">Create an Activity Log Alert toomonitor all failed Autoscale scale-in/scale-out operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

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

