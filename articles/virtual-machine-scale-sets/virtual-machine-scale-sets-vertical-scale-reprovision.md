---
title: "наборы масштабирования виртуальной машины Azure шкалы aaaVertically | Документы Microsoft"
description: "Как toovertically масштабирования виртуальной машины в ответ toomonitoring предупреждения в службе автоматизации Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: madhana
editor: 
tags: azure-resource-manager
ms.assetid: 16b17421-6b8f-483e-8a84-26327c44e9d3
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: guybo
ms.openlocfilehash: 1cc35a805b6a5742252a89c21588ca451ff547a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a><span data-ttu-id="7a75c-103">Вертикальное автомасштабирование масштабируемых наборов виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="7a75c-103">Vertical autoscale with Virtual Machine Scale sets</span></span>
<span data-ttu-id="7a75c-104">В этой статье описывается, как toovertically масштабирования Azure [наборы масштабирования виртуальных машин](https://azure.microsoft.com/services/virtual-machine-scale-sets/) с или без инициализацию.</span><span class="sxs-lookup"><span data-stu-id="7a75c-104">This article describes how toovertically scale Azure [Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/) with or without reprovisioning.</span></span> <span data-ttu-id="7a75c-105">Вертикального масштабирования виртуальных машин, которые отсутствуют в наборы масштабирования, см. в разделе слишком[вертикальное масштабирование виртуальной машины Azure в службе автоматизации Azure](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7a75c-105">For vertical scaling of VMs which are not in scale sets, refer too[Vertically scale Azure virtual machine with Azure Automation](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="7a75c-106">Вертикальное масштабирование, также известный как *масштабировать* и *масштабировать*, означает увеличение или уменьшение размеров виртуальных машин (ВМ) в рабочей нагрузки tooa ответа.</span><span class="sxs-lookup"><span data-stu-id="7a75c-106">Vertical scaling, also known as *scale up* and *scale down*, means increasing or decreasing virtual machine (VM) sizes in response tooa workload.</span></span> <span data-ttu-id="7a75c-107">Сравните это с [горизонтальное масштабирование](virtual-machine-scale-sets-autoscale-overview.md), также называется tooas *горизонтальное масштабирование* и *масштабирования в*, где hello число виртуальных машин, изменяется в зависимости от нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="7a75c-107">Compare this with [horizontal scaling](virtual-machine-scale-sets-autoscale-overview.md), also referred tooas *scale out* and *scale in*, where hello number of VMs is altered depending on hello workload.</span></span>

<span data-ttu-id="7a75c-108">Повторная подготовка означает удаление существующей виртуальной машины и ее замену новой.</span><span class="sxs-lookup"><span data-stu-id="7a75c-108">Reprovisioning means removing an existing VM and replacing it with a new one.</span></span> <span data-ttu-id="7a75c-109">При увеличении или уменьшении размера hello виртуальных машин в наборе масштабирования виртуальных Машин, в некоторых случаях вы хотите tooresize существующие виртуальные машины и сохранить данные, а в других случаях необходимо toodeploy новых виртуальных машин, новый размер hello.</span><span class="sxs-lookup"><span data-stu-id="7a75c-109">When you increase or decrease hello size of VMs in a VM Scale Set, in some cases you want tooresize existing VMs and retain your data, while in other cases you need toodeploy new VMs of hello new size.</span></span> <span data-ttu-id="7a75c-110">В этом документе описываются оба сценария.</span><span class="sxs-lookup"><span data-stu-id="7a75c-110">This document covers both cases.</span></span>

<span data-ttu-id="7a75c-111">Когда полезно выполнять вертикальное масштабирование:</span><span class="sxs-lookup"><span data-stu-id="7a75c-111">Vertical scaling can be useful when:</span></span>

* <span data-ttu-id="7a75c-112">Если служба, работающая на базе виртуальных машин, мало используется (например, в выходные).</span><span class="sxs-lookup"><span data-stu-id="7a75c-112">A service built on virtual machines is under-utilized (for example at weekends).</span></span> <span data-ttu-id="7a75c-113">Уменьшение размера виртуальной Машины hello можно сократить ежемесячные расходы.</span><span class="sxs-lookup"><span data-stu-id="7a75c-113">Reducing hello VM size can reduce monthly costs.</span></span>
* <span data-ttu-id="7a75c-114">Увеличение toocope размер виртуальной Машины с требованиями большего размера без создания дополнительных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="7a75c-114">Increasing VM size toocope with larger demand without creating additional VMs.</span></span>

<span data-ttu-id="7a75c-115">Можно настроить по вертикали масштабирование toobe активации на основе метрики на основе предупреждений из набора масштабирования виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="7a75c-115">You can set up vertical scaling toobe triggered based on metric based alerts from your VM Scale Set.</span></span> <span data-ttu-id="7a75c-116">Активируется hello оповещение срабатывает, веб-перехватчика, которая инициирует runbook, который можно масштабировать шкалу значение вверх или вниз.</span><span class="sxs-lookup"><span data-stu-id="7a75c-116">When hello alert is activated it fires a webhook that triggers a runbook which can scale your scale set up or down.</span></span> <span data-ttu-id="7a75c-117">Вертикальное масштабирование можно настроить так:</span><span class="sxs-lookup"><span data-stu-id="7a75c-117">Vertical scaling can be configured by following these steps:</span></span>

1. <span data-ttu-id="7a75c-118">Создайте учетную запись службы автоматизации Azure с возможностью запуска от имени.</span><span class="sxs-lookup"><span data-stu-id="7a75c-118">Create an Azure Automation account with run-as capability.</span></span>
2. <span data-ttu-id="7a75c-119">Импортируйте в подписку модули Runbook службы автоматизации Azure для вертикального масштабирования.</span><span class="sxs-lookup"><span data-stu-id="7a75c-119">Import Azure Automation Vertical Scale runbooks for VM Scale Sets into your subscription.</span></span>
3. <span data-ttu-id="7a75c-120">Добавьте веб-перехватчика tooyour runbook.</span><span class="sxs-lookup"><span data-stu-id="7a75c-120">Add a webhook tooyour runbook.</span></span>
4. <span data-ttu-id="7a75c-121">Добавление оповещений tooyour, набора масштабирования виртуальных Машин с помощью веб-перехватчика уведомление.</span><span class="sxs-lookup"><span data-stu-id="7a75c-121">Add an alert tooyour VM Scale Set using a webhook notification.</span></span>

> [!NOTE]
> <span data-ttu-id="7a75c-122">Вертикальное автомасштабирование поддерживается только для виртуальных машин определенных размеров.</span><span class="sxs-lookup"><span data-stu-id="7a75c-122">Vertical autoscaling can only take place within certain ranges of VM sizes.</span></span> <span data-ttu-id="7a75c-123">Сравните спецификации hello каждого размера перед принятием решения об tooscale из одного tooanother (большее число не всегда обеспечивает больший размер виртуальной Машины).</span><span class="sxs-lookup"><span data-stu-id="7a75c-123">Compare hello specifications of each size before deciding tooscale from one tooanother (higher number does not always indicate bigger VM size).</span></span> <span data-ttu-id="7a75c-124">Вы можете tooscale между hello следующие пары размеров:</span><span class="sxs-lookup"><span data-stu-id="7a75c-124">You can choose tooscale between hello following pairs of sizes:</span></span>
> 
> | <span data-ttu-id="7a75c-125">Пары размеров виртуальных машин, для которых можно применять вертикальное масштабирование</span><span class="sxs-lookup"><span data-stu-id="7a75c-125">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="7a75c-126">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="7a75c-126">Standard_A0</span></span> |<span data-ttu-id="7a75c-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="7a75c-127">Standard_A11</span></span> |
> | <span data-ttu-id="7a75c-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="7a75c-128">Standard_D1</span></span> |<span data-ttu-id="7a75c-129">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="7a75c-129">Standard_D14</span></span> |
> | <span data-ttu-id="7a75c-130">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="7a75c-130">Standard_DS1</span></span> |<span data-ttu-id="7a75c-131">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="7a75c-131">Standard_DS14</span></span> |
> | <span data-ttu-id="7a75c-132">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="7a75c-132">Standard_D1v2</span></span> |<span data-ttu-id="7a75c-133">Standard_D15v2</span><span class="sxs-lookup"><span data-stu-id="7a75c-133">Standard_D15v2</span></span> |
> | <span data-ttu-id="7a75c-134">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="7a75c-134">Standard_G1</span></span> |<span data-ttu-id="7a75c-135">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="7a75c-135">Standard_G5</span></span> |
> | <span data-ttu-id="7a75c-136">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="7a75c-136">Standard_GS1</span></span> |<span data-ttu-id="7a75c-137">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="7a75c-137">Standard_GS5</span></span> |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a><span data-ttu-id="7a75c-138">Создание учетной записи службы автоматизации Azure с возможностью запуска от имени</span><span class="sxs-lookup"><span data-stu-id="7a75c-138">Create an Azure Automation Account with run-as capability</span></span>
<span data-ttu-id="7a75c-139">Hello первое, что необходимо toodo — создать учетную запись службы автоматизации Azure, где будет размещаться hello модулей Runbook используется tooscale hello набора масштабирования виртуальных Машин экземпляры.</span><span class="sxs-lookup"><span data-stu-id="7a75c-139">hello first thing you need toodo is create an Azure Automation account that will host hello runbooks used tooscale hello VM Scale Set instances.</span></span> <span data-ttu-id="7a75c-140">Недавно [автоматизации Azure](https://azure.microsoft.com/services/automation/) появилась возможность «Запуск от имени учетной записи» hello, что делает настройку hello участника-службы для автоматического запуска модулей Runbook hello от имени пользователя очень просто.</span><span class="sxs-lookup"><span data-stu-id="7a75c-140">Recently [Azure Automation](https://azure.microsoft.com/services/automation/) introduced hello "Run As account" feature which makes setting up hello Service Principal for automatically running hello runbooks on a user's behalf very easy.</span></span> <span data-ttu-id="7a75c-141">Можно прочитать подробнее об этом в статье hello ниже:</span><span class="sxs-lookup"><span data-stu-id="7a75c-141">You can read more about this in hello article below:</span></span>

* [<span data-ttu-id="7a75c-142">Проверка подлинности модулей Runbook в Azure с помощью учетной записи запуска от имени</span><span class="sxs-lookup"><span data-stu-id="7a75c-142">Authenticate Runbooks with Azure Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="7a75c-143">Импорт в подписку модулей Runbook службы автоматизации Azure для вертикального масштабирования</span><span class="sxs-lookup"><span data-stu-id="7a75c-143">Import Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="7a75c-144">модули Runbook Hello требуется toovertically масштабирования вашего набора масштабирования виртуальных Машин уже публикуются в коллекции модулей Runbook службы автоматизации Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7a75c-144">hello runbooks needed toovertically scale your VM Scale Sets are already published in hello Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="7a75c-145">tooimport их в подписке hello, выполните шаги в этой статье:</span><span class="sxs-lookup"><span data-stu-id="7a75c-145">tooimport them into your subscription follow hello steps in this article:</span></span>

* [<span data-ttu-id="7a75c-146">Runbook и коллекции модулей для службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="7a75c-146">Runbook and module galleries for Azure Automation</span></span>](../automation/automation-runbook-gallery.md)

<span data-ttu-id="7a75c-147">Выберите вариант обзора коллекции hello меню hello модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="7a75c-147">Choose hello Browse Gallery option from hello Runbooks menu:</span></span>

![Toobe модули Runbook импортированы][runbooks]

<span data-ttu-id="7a75c-149">Hello Runbook, которые требуется импортировать toobe отображаются.</span><span class="sxs-lookup"><span data-stu-id="7a75c-149">hello runbooks that need toobe imported are shown.</span></span> <span data-ttu-id="7a75c-150">Выберите runbook hello, в зависимости от того, нужно ли вертикальное масштабирование с или без инициализацию:</span><span class="sxs-lookup"><span data-stu-id="7a75c-150">Select hello runbook based on whether you want vertical scaling with or without reprovisioning:</span></span>

![Коллекция модулей Runbook][gallery]

## <a name="add-a-webhook-tooyour-runbook"></a><span data-ttu-id="7a75c-152">Добавить модуль runbook tooyour веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="7a75c-152">Add a webhook tooyour runbook</span></span>
<span data-ttu-id="7a75c-153">После импорта модулей Runbook hello необходимо tooadd runbook toohello веб-перехватчика, может быть вызвано предупреждение от набора масштабирования виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="7a75c-153">Once you've imported hello runbooks you'll need tooadd a webhook toohello runbook so it can be triggered by an alert from a VM Scale Set.</span></span> <span data-ttu-id="7a75c-154">в этой статье описаны Hello подробные сведения о создании веб-перехватчика для модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="7a75c-154">hello details of creating a webhook for your Runbook are described in this article:</span></span>

* [<span data-ttu-id="7a75c-155">Объекты Webhook в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="7a75c-155">Azure Automation webhooks</span></span>](../automation/automation-webhooks.md)

> [!NOTE]
> <span data-ttu-id="7a75c-156">Убедитесь, что копирование веб-перехватчика hello URI перед закрытием диалогового окна веб-перехватчика hello, как он потребуется в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="7a75c-156">Make sure you copy hello webhook URI before closing hello webhook dialog as you will need this in hello next section.</span></span>
> 
> 

## <a name="add-an-alert-tooyour-vm-scale-set"></a><span data-ttu-id="7a75c-157">Добавление оповещений tooyour, набора масштабирования виртуальных Машин</span><span class="sxs-lookup"><span data-stu-id="7a75c-157">Add an alert tooyour VM Scale Set</span></span>
<span data-ttu-id="7a75c-158">Ниже приведен сценарий PowerShell, котором показывается, как tooadd предупреждения tooa, набора масштабирования виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="7a75c-158">Below is a PowerShell script which shows how tooadd an alert tooa VM Scale Set.</span></span> <span data-ttu-id="7a75c-159">Ссылаться после имени hello tooget статье hello метрики toofire hello предупреждения toohello: [общих метрик автоматическое масштабирование Azure монитор](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="7a75c-159">Refer toohello following article tooget hello name of hello metric toofire hello alert on: [Azure Monitor autoscaling common metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span>

```
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail user@contoso.com
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri <uri-of-the-webhook>
$threshold = <value-of-the-threshold>
$rg = <resource-group-name>
$id = <resource-id-to-add-the-alert-to>
$location = <location-of-the-resource>
$alertName = <name-of-the-resource>
$metricName = <metric-to-fire-the-alert-on>
$timeWindow = <time-window-in-hh:mm:ss-format>
$condition = <condition-for-the-threshold> # Other valid values are LessThanOrEqual, GreaterThan, GreaterThanOrEqual
$description = <description-for-the-alert>

Add-AzureRmMetricAlertRule  -Name  $alertName `
                            -Location  $location `
                            -ResourceGroup $rg `
                            -TargetResourceId $id `
                            -MetricName $metricName `
                            -Operator  $condition `
                            -Threshold $threshold `
                            -WindowSize  $timeWindow `
                            -TimeAggregationOperator Average `
                            -Actions $actionEmail, $actionWebhook `
                            -Description $description
```

> [!NOTE]
> <span data-ttu-id="7a75c-160">Это рекомендуется tooconfigure окна слишком много времени для предупреждения hello в tooavoid порядок запуска вертикального масштабирования, вместе со всеми связанными перерыва в обслуживании, слишком часто.</span><span class="sxs-lookup"><span data-stu-id="7a75c-160">It is recommended tooconfigure a reasonable time window for hello alert in order tooavoid triggering vertical scaling, and any associated service interruption, too often.</span></span> <span data-ttu-id="7a75c-161">Начните с интервала минимум в 20–30 минут.</span><span class="sxs-lookup"><span data-stu-id="7a75c-161">Consider a window of least 20-30 minutes or more.</span></span> <span data-ttu-id="7a75c-162">Рассмотрите возможность горизонтальное масштабирование, при необходимости tooavoid нарушения работы.</span><span class="sxs-lookup"><span data-stu-id="7a75c-162">Consider horizontal scaling if you need tooavoid any interruption.</span></span>
> 
> 

<span data-ttu-id="7a75c-163">Дополнительные сведения о как toocreate предупреждений см. следующие статьи toohello:</span><span class="sxs-lookup"><span data-stu-id="7a75c-163">For more information on how toocreate alerts refer toohello following articles:</span></span>

* [<span data-ttu-id="7a75c-164">Примеры для быстрого запуска Azure Insights с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a75c-164">Azure Monitor PowerShell quick start samples</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md)
* [<span data-ttu-id="7a75c-165">Примеры команд для межплатформенного интерфейса командной строки Azure Insights</span><span class="sxs-lookup"><span data-stu-id="7a75c-165">Azure Monitor Cross-platform CLI quick start samples</span></span>](../monitoring-and-diagnostics/insights-cli-samples.md)

## <a name="summary"></a><span data-ttu-id="7a75c-166">Сводка</span><span class="sxs-lookup"><span data-stu-id="7a75c-166">Summary</span></span>
<span data-ttu-id="7a75c-167">В этой статье описан простой способ вертикального масштабирования.</span><span class="sxs-lookup"><span data-stu-id="7a75c-167">This article showed simple vertical scaling examples.</span></span> <span data-ttu-id="7a75c-168">Указанные блоки (работа с учетной записью службы автоматизации, модулями Runbook, веб-перехватчиками и оповещениями) позволяют включить в настраиваемый набор действий самые разные события.</span><span class="sxs-lookup"><span data-stu-id="7a75c-168">With these building blocks - Automation account, runbooks, webhooks, alerts - you can connect a rich variety of events with a customized set of actions.</span></span>

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
