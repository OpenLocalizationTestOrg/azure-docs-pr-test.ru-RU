---
title: "aaaGet работы с автоматическое масштабирование по метрике пользовательских в Azure | Документы Microsoft"
description: "Узнайте, как tooscale ресурс пользовательские метрики в Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: d3e268ec322698d0d367361cd9c156b21e0fb6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a><span data-ttu-id="a0786-103">Начало работы с автомасштабированием на основе пользовательской метрики в Azure</span><span class="sxs-lookup"><span data-stu-id="a0786-103">Get started with auto scale by custom metric in Azure</span></span>
<span data-ttu-id="a0786-104">В этой статье описывается как tooscale ресурс пользовательские метрики на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="a0786-104">This article describes how tooscale your resource by a custom metric in Azure portal.</span></span>

<span data-ttu-id="a0786-105">Автоматическое масштабирование Azure монитор применяется только tooVirtual задает масштаб компьютера (VMSS), облачные службы, планах службы приложений и среды службы приложений.</span><span class="sxs-lookup"><span data-stu-id="a0786-105">Azure Monitor auto scale applies only tooVirtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="a0786-106">Начало работы</span><span class="sxs-lookup"><span data-stu-id="a0786-106">Lets get started</span></span>
<span data-ttu-id="a0786-107">В данной статье предполагается, что у вас есть веб-приложение, для которого настроена среда Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a0786-107">This article assumes that you have a web app with application insights configured.</span></span> <span data-ttu-id="a0786-108">Если у вас его нет, вы можете [установить Application Insights для веб-сайта ASP.NET][1].</span><span class="sxs-lookup"><span data-stu-id="a0786-108">If you don't have one already, you can [set up Application Insights for your ASP.NET website][1]</span></span>

- <span data-ttu-id="a0786-109">Откройте [портал Azure][2].</span><span class="sxs-lookup"><span data-stu-id="a0786-109">Open [Azure portal][2]</span></span>
- <span data-ttu-id="a0786-110">Щелкните значок Azure монитора hello левой панели навигации.</span><span class="sxs-lookup"><span data-stu-id="a0786-110">Click on Azure Monitor icon in hello left navigation pane.</span></span>
  <span data-ttu-id="a0786-111">![Запуск Azure Monitor][3]</span><span class="sxs-lookup"><span data-stu-id="a0786-111">![Launch Azure Monitor][3]</span></span>
- <span data-ttu-id="a0786-112">Щелкните параметр tooview все ресурсы hello, для которого автоматически масштаб не применимо, а также ее текущее состояние автомасштабирования автомасштабирования ![обнаружение автоматическое масштабирование в Azure монитора][4]</span><span class="sxs-lookup"><span data-stu-id="a0786-112">Click on Autoscale setting tooview all hello resources for which auto scale is applicable, along with its current autoscale status ![Discover auto scale in Azure monitor][4]</span></span>
- <span data-ttu-id="a0786-113">Откройте колонку «Автомасштабирования» в мониторе Azure и выберите ресурс, нужно tooscale</span><span class="sxs-lookup"><span data-stu-id="a0786-113">Open 'Autoscale' blade in Azure Monitor and select a resource you want tooscale</span></span>
> <span data-ttu-id="a0786-114">Примечание: hello шаги использовать план обслуживания приложений, связанных с веб-приложения с настроить подробные сведения о приложении.</span><span class="sxs-lookup"><span data-stu-id="a0786-114">Note: hello steps below use an app service plan associated with a web app that has app insights configured.</span></span>
- <span data-ttu-id="a0786-115">В колонке параметр hello масштабирования для ресурса hello Обратите внимание, что текущее количество экземпляров hello 1.</span><span class="sxs-lookup"><span data-stu-id="a0786-115">In hello scale setting blade for hello resource, notice that hello current instance count is 1.</span></span> <span data-ttu-id="a0786-116">Щелкните Enable autoscale (Включить автомасштабирование).</span><span class="sxs-lookup"><span data-stu-id="a0786-116">Click on 'Enable autoscale'.</span></span>
  <span data-ttu-id="a0786-117">![Параметр масштабирования для нового веб-приложения][5]</span><span class="sxs-lookup"><span data-stu-id="a0786-117">![Scale setting for new web app][5]</span></span>
- <span data-ttu-id="a0786-118">Введите имя для параметра масштабирования hello и hello щелкните «Добавить правило».</span><span class="sxs-lookup"><span data-stu-id="a0786-118">Provide a name for hello scale setting, and hello click on "Add a rule".</span></span> <span data-ttu-id="a0786-119">Обратите внимание, параметров правил масштабирования hello, открывается в виде контекстной области в правую часть hello.</span><span class="sxs-lookup"><span data-stu-id="a0786-119">Notice hello scale rule options that opens as a context pane in hello right hand side.</span></span> <span data-ttu-id="a0786-120">По умолчанию он устанавливает экземпляр счетчика на 1, если percetage ЦП hello hello ресурса превышает 70% tooscale параметр hello.</span><span class="sxs-lookup"><span data-stu-id="a0786-120">By default, it sets hello option tooscale your instance count by 1 if hello CPU percetage of hello resource exceeds 70%.</span></span> <span data-ttu-id="a0786-121">Источник метрики hello изменение вверху hello слишком выберите «Application Insights» hello ресурсов аналитики приложений в раскрывающийся список «Resource» hello "и" hello, а затем выберите пользовательские метрики на основе tooscale для которых нужно получить.</span><span class="sxs-lookup"><span data-stu-id="a0786-121">Change hello metric source at hello top too"Application Insights", select hello app insights resource in hello 'Resource' dropdown and then select hello custom metric based on which you want tooscale.</span></span>
  <span data-ttu-id="a0786-122">![Масштабирование на основе пользовательской метрики][6]</span><span class="sxs-lookup"><span data-stu-id="a0786-122">![Scale by custom metric][6]</span></span>
- <span data-ttu-id="a0786-123">Аналогичные toohello шаг выше, добавьте правила масштабирования, которая будет масштабировать и уменьшить число hello масштабирования на 1, если пользовательская метрика hello ниже порогового значения.</span><span class="sxs-lookup"><span data-stu-id="a0786-123">Similar toohello step above, add a scale rule that will scale in and decrease hello scale count by 1 if hello custom metric is below a threshold.</span></span>
  <span data-ttu-id="a0786-124">![Масштабирование на основе использования ЦП][7]</span><span class="sxs-lookup"><span data-stu-id="a0786-124">![Scale based on cpu][7]</span></span>
- <span data-ttu-id="a0786-125">Установите экземпляр ограничения hello.</span><span class="sxs-lookup"><span data-stu-id="a0786-125">Set hello you instance limits.</span></span> <span data-ttu-id="a0786-126">Например, если требуется tooscale между экземплярами 2 – 5 в зависимости от пользовательские метрики колебания hello задать «Минимальная» слишком "2", «максимум» слишком "5" и «default» слишком "2"</span><span class="sxs-lookup"><span data-stu-id="a0786-126">For example, if you want tooscale between 2-5 instances depending on hello custom metric fluctuations, set 'minimum' too'2', 'maximum' too'5' and 'default' too'2'</span></span>
> <span data-ttu-id="a0786-127">Примечание: Если имеется проблема при чтении метрики ресурсов hello и hello текущая емкость меньше емкости по умолчанию hello, затем tooensure hello доступности ресурса hello автомасштабирования будет масштабировать toohello значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a0786-127">Note: In case there is a problem reading hello resource metrics and hello current capacity is below hello default capacity, then tooensure hello availability of hello resource, Autoscale will scale out toohello default value.</span></span> <span data-ttu-id="a0786-128">Если текущая емкость hello уже превышает емкость по умолчанию, в не масштабируется автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="a0786-128">If hello current capacity is already higher than default capacity, Autoscale will not scale in.</span></span>
- <span data-ttu-id="a0786-129">Щелкните "Сохранить".</span><span class="sxs-lookup"><span data-stu-id="a0786-129">Click on 'Save'</span></span>

<span data-ttu-id="a0786-130">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="a0786-130">Congratulations.</span></span> <span data-ttu-id="a0786-131">Теперь ваш tooauto параметр масштабирования успешно созданы масштабировать веб-приложения, в зависимости от пользовательской метрики.</span><span class="sxs-lookup"><span data-stu-id="a0786-131">You now now succesfully created your scale setting tooauto scale your web app based on a custom metric.</span></span>

> <span data-ttu-id="a0786-132">Примечание: hello же действия, применимые tooget работы с ролью VMSS или облачной службы.</span><span class="sxs-lookup"><span data-stu-id="a0786-132">Note: hello same steps are applicable tooget started with a VMSS or cloud service role.</span></span>

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
