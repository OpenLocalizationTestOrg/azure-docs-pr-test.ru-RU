---
title: "Вертикальное масштабирование виртуальных машин Windows c помощью службы автоматизации Azure | Документация Майкрософт"
description: "Вертикальное масштабирование виртуальной машины Windows в ответ на оповещения мониторинга c помощью службы автоматизации Azure"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4f964713-fb67-4bcc-8246-3431452ddf7d
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: kasing
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ea5169c1a95f00e78ae3f5f177812466eb7a0deb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="vertically-scale-windows-vms-with-azure-automation"></a><span data-ttu-id="b2389-103">Вертикальное масштабирование виртуальных машин Windows с помощью службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="b2389-103">Vertically scale Windows VMs with Azure Automation</span></span>

<span data-ttu-id="b2389-104">Вертикальное масштабирование — это процесс увеличения или уменьшения объема ресурсов виртуальной машины в зависимости от рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="b2389-104">Vertical scaling is the process of increasing or decreasing the resources of a machine in response to the workload.</span></span> <span data-ttu-id="b2389-105">В Azure это можно сделать, изменив размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b2389-105">In Azure this can be accomplished by changing the size of the Virtual Machine.</span></span> <span data-ttu-id="b2389-106">Вертикальное масштабирование можно использовать в следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="b2389-106">This can help in the following scenarios</span></span>

* <span data-ttu-id="b2389-107">если виртуальная машина используется редко, вы можете уменьшить ее размер, чтобы сократить ежемесячные затраты;</span><span class="sxs-lookup"><span data-stu-id="b2389-107">If the Virtual Machine is not being used frequently, you can resize it down to a smaller size to reduce your monthly costs</span></span>
* <span data-ttu-id="b2389-108">если виртуальная машина испытывает пиковые нагрузки, ее размер можно увеличить, чтобы расширить емкость.</span><span class="sxs-lookup"><span data-stu-id="b2389-108">If the Virtual Machine is seeing a peak load, it can be resized to a larger size to increase its capacity</span></span>

<span data-ttu-id="b2389-109">Ниже представлены шаги для реализации вертикального масштабирования.</span><span class="sxs-lookup"><span data-stu-id="b2389-109">The outline for the steps to accomplish this is as below</span></span>

1. <span data-ttu-id="b2389-110">Настройка службы автоматизации Azure для доступа к виртуальным машинам.</span><span class="sxs-lookup"><span data-stu-id="b2389-110">Setup Azure Automation to access your Virtual Machines</span></span>
2. <span data-ttu-id="b2389-111">Импорт модулей Runbook службы автоматизации Azure для вертикального масштабирования в подписку</span><span class="sxs-lookup"><span data-stu-id="b2389-111">Import the Azure Automation Vertical Scale runbooks into your subscription</span></span>
3. <span data-ttu-id="b2389-112">Добавление веб-перехватчика в модуль Runbook.</span><span class="sxs-lookup"><span data-stu-id="b2389-112">Add a webhook to your runbook</span></span>
4. <span data-ttu-id="b2389-113">Добавление правила оповещения для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b2389-113">Add an alert to your Virtual Machine</span></span>

> [!NOTE]
> <span data-ttu-id="b2389-114">Размеры, до которых можно масштабировать виртуальную машину, могут быть ограничены из-за размера первой виртуальной машины ввиду поддерживаемых размеров кластера, в котором развернута текущая виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="b2389-114">Because of the size of the first Virtual Machine, the sizes it can be scaled to, may be limited due to the availability of the other sizes in the cluster current Virtual Machine is deployed in.</span></span> <span data-ttu-id="b2389-115">В этой статье мы учли эту особенность и в опубликованных модулях Runbook службы автоматизации использовали для масштабирования только приведенные ниже примеры размеров виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b2389-115">In the published automation runbooks used in this article we take care of this case and only scale within the below VM size pairs.</span></span> <span data-ttu-id="b2389-116">Это означает, что нельзя внезапно увеличить виртуальную машину размером Standard_D1v2 до размера Standard_G5 или уменьшить до Basic_A0.</span><span class="sxs-lookup"><span data-stu-id="b2389-116">This means that a Standard_D1v2 Virtual Machine will not suddenly be scaled up to Standard_G5 or scaled down to Basic_A0.</span></span>
> 
> | <span data-ttu-id="b2389-117">Пары размеров виртуальных машин, для которых можно применять вертикальное масштабирование</span><span class="sxs-lookup"><span data-stu-id="b2389-117">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="b2389-118">Basic_A0</span><span class="sxs-lookup"><span data-stu-id="b2389-118">Basic_A0</span></span> |<span data-ttu-id="b2389-119">Basic_A4</span><span class="sxs-lookup"><span data-stu-id="b2389-119">Basic_A4</span></span> |
> | <span data-ttu-id="b2389-120">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="b2389-120">Standard_A0</span></span> |<span data-ttu-id="b2389-121">Standard_A4</span><span class="sxs-lookup"><span data-stu-id="b2389-121">Standard_A4</span></span> |
> | <span data-ttu-id="b2389-122">Standard_A5</span><span class="sxs-lookup"><span data-stu-id="b2389-122">Standard_A5</span></span> |<span data-ttu-id="b2389-123">Standard_A7</span><span class="sxs-lookup"><span data-stu-id="b2389-123">Standard_A7</span></span> |
> | <span data-ttu-id="b2389-124">Standard_A8</span><span class="sxs-lookup"><span data-stu-id="b2389-124">Standard_A8</span></span> |<span data-ttu-id="b2389-125">Standard_A9</span><span class="sxs-lookup"><span data-stu-id="b2389-125">Standard_A9</span></span> |
> | <span data-ttu-id="b2389-126">Standard_A10</span><span class="sxs-lookup"><span data-stu-id="b2389-126">Standard_A10</span></span> |<span data-ttu-id="b2389-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="b2389-127">Standard_A11</span></span> |
> | <span data-ttu-id="b2389-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="b2389-128">Standard_D1</span></span> |<span data-ttu-id="b2389-129">Standard_D4</span><span class="sxs-lookup"><span data-stu-id="b2389-129">Standard_D4</span></span> |
> | <span data-ttu-id="b2389-130">Standard_D11</span><span class="sxs-lookup"><span data-stu-id="b2389-130">Standard_D11</span></span> |<span data-ttu-id="b2389-131">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="b2389-131">Standard_D14</span></span> |
> | <span data-ttu-id="b2389-132">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="b2389-132">Standard_DS1</span></span> |<span data-ttu-id="b2389-133">Standard_DS4</span><span class="sxs-lookup"><span data-stu-id="b2389-133">Standard_DS4</span></span> |
> | <span data-ttu-id="b2389-134">Standard_DS11</span><span class="sxs-lookup"><span data-stu-id="b2389-134">Standard_DS11</span></span> |<span data-ttu-id="b2389-135">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="b2389-135">Standard_DS14</span></span> |
> | <span data-ttu-id="b2389-136">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="b2389-136">Standard_D1v2</span></span> |<span data-ttu-id="b2389-137">Standard_D5v2</span><span class="sxs-lookup"><span data-stu-id="b2389-137">Standard_D5v2</span></span> |
> | <span data-ttu-id="b2389-138">Standard_D11v2</span><span class="sxs-lookup"><span data-stu-id="b2389-138">Standard_D11v2</span></span> |<span data-ttu-id="b2389-139">Standard_D14v2</span><span class="sxs-lookup"><span data-stu-id="b2389-139">Standard_D14v2</span></span> |
> | <span data-ttu-id="b2389-140">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="b2389-140">Standard_G1</span></span> |<span data-ttu-id="b2389-141">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="b2389-141">Standard_G5</span></span> |
> | <span data-ttu-id="b2389-142">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="b2389-142">Standard_GS1</span></span> |<span data-ttu-id="b2389-143">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="b2389-143">Standard_GS5</span></span> |
> 
> 

## <a name="setup-azure-automation-to-access-your-virtual-machines"></a><span data-ttu-id="b2389-144">Настройка службы автоматизации Azure для доступа к виртуальным машинам.</span><span class="sxs-lookup"><span data-stu-id="b2389-144">Setup Azure Automation to access your Virtual Machines</span></span>
<span data-ttu-id="b2389-145">Первое, что вам нужно сделать, — создать учетную запись службы автоматизации Azure, где будут размещаться модули Runbook, используемые для масштабирования виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b2389-145">The first thing you need to do is create an Azure Automation account that will host the runbooks used to scale a Virtual Machine.</span></span> <span data-ttu-id="b2389-146">Недавно в службе автоматизации появилась функция "Запуск от имени...", которая упрощает настройку субъекта-службы для автоматического запуска модулей Runbook от имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="b2389-146">Recently the Automation service introduced the "Run As account" feature which makes setting up the Service Principal for automatically running the runbooks on the user's behalf very easy.</span></span> <span data-ttu-id="b2389-147">Дополнительные сведения об этом см. в следующей статье:</span><span class="sxs-lookup"><span data-stu-id="b2389-147">You can read more about this in the article below:</span></span>

* [<span data-ttu-id="b2389-148">Проверка подлинности модулей Runbook в Azure с помощью учетной записи запуска от имени</span><span class="sxs-lookup"><span data-stu-id="b2389-148">Authenticate Runbooks with Azure Run As account</span></span>](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-the-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="b2389-149">Импорт модулей Runbook службы автоматизации Azure для вертикального масштабирования в подписку</span><span class="sxs-lookup"><span data-stu-id="b2389-149">Import the Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="b2389-150">Модули Runbook, необходимые для вертикального масштабирования виртуальной машины, уже опубликованы в коллекции Runbook службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="b2389-150">The runbooks that are needed for Vertically Scaling your Virtual Machine are already published in the Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="b2389-151">Вам потребуется импортировать их в подписку.</span><span class="sxs-lookup"><span data-stu-id="b2389-151">You will need to import them into your subscription.</span></span> <span data-ttu-id="b2389-152">Дополнительные сведения об импорте модулей Runbook см. в статье:</span><span class="sxs-lookup"><span data-stu-id="b2389-152">You can learn how to import runbooks by reading the following article.</span></span>

* [<span data-ttu-id="b2389-153">Runbook и коллекции модулей для службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="b2389-153">Runbook and module galleries for Azure Automation</span></span>](../../automation/automation-runbook-gallery.md)

<span data-ttu-id="b2389-154">На приведенном ниже рисунке показаны модули Runbook, которые необходимо импортировать.</span><span class="sxs-lookup"><span data-stu-id="b2389-154">The runbooks that need to be imported are shown in the image below</span></span>

![Импорт модулей Runbook](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-to-your-runbook"></a><span data-ttu-id="b2389-156">Добавление веб-перехватчика в модуль Runbook.</span><span class="sxs-lookup"><span data-stu-id="b2389-156">Add a webhook to your runbook</span></span>
<span data-ttu-id="b2389-157">После импорта модулей Runbook в них необходимо добавить веб-перехватчик. Этого может потребовать система оповещений виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b2389-157">Once you've imported the runbooks you'll need to add a webhook to the runbook so it can be triggered by an alert from a Virtual Machine.</span></span> <span data-ttu-id="b2389-158">Дополнительные сведения о создании веб-перехватчика для вашего модуля Runbook см. в статье:</span><span class="sxs-lookup"><span data-stu-id="b2389-158">The details of creating a webhook for your Runbook can be read here</span></span>

* [<span data-ttu-id="b2389-159">Объекты Webhook в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="b2389-159">Azure Automation webhooks</span></span>](../../automation/automation-webhooks.md)

<span data-ttu-id="b2389-160">Прежде чем закрывать диалоговое окно, убедитесь, что вы скопировали веб-перехватчик. Он понадобится в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="b2389-160">Make sure you copy the webhook before closing the webhook dialog as you will need this in the next section.</span></span>

## <a name="add-an-alert-to-your-virtual-machine"></a><span data-ttu-id="b2389-161">Добавление правила оповещения для виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="b2389-161">Add an alert to your Virtual Machine</span></span>
1. <span data-ttu-id="b2389-162">Перейдите в раздел параметров виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b2389-162">Select Virtual Machine settings</span></span>
2. <span data-ttu-id="b2389-163">Щелкните "Правила оповещения".</span><span class="sxs-lookup"><span data-stu-id="b2389-163">Select "Alert rules"</span></span>
3. <span data-ttu-id="b2389-164">Щелкните "Добавить оповещение".</span><span class="sxs-lookup"><span data-stu-id="b2389-164">Select "Add alert"</span></span>
4. <span data-ttu-id="b2389-165">Выберите метрику, на основе значения которой будут срабатывать оповещения.</span><span class="sxs-lookup"><span data-stu-id="b2389-165">Select a metric to fire the alert on</span></span>
5. <span data-ttu-id="b2389-166">Выберите условие, при выполнении которого будет срабатывать оповещение.</span><span class="sxs-lookup"><span data-stu-id="b2389-166">Select a condition, which when fulfilled will cause the alert to fire</span></span>
6. <span data-ttu-id="b2389-167">Установите пороговое значение для условия,</span><span class="sxs-lookup"><span data-stu-id="b2389-167">Select a threshold for the condition in Step 5.</span></span> <span data-ttu-id="b2389-168">упомянутого выше.</span><span class="sxs-lookup"><span data-stu-id="b2389-168">to be fulfilled</span></span>
7. <span data-ttu-id="b2389-169">Выберите период для проверки условий и порогового значения, упомянутых выше.</span><span class="sxs-lookup"><span data-stu-id="b2389-169">Select a period over which the monitoring service will check for the condition and threshold in Steps 5 & 6</span></span>
8. <span data-ttu-id="b2389-170">Вставьте скопированный веб-перехватчик, описанный в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="b2389-170">Paste in the webhook you copied from the previous section.</span></span>

![Добавить правило оповещения для виртуальной машины 1](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Добавить правило оповещения для виртуальной машины 2](./media/vertical-scaling-automation/add-alert-webhook-2.png)

