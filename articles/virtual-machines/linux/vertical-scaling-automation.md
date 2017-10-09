---
title: "aaaVertically масштабирования виртуальной машины Azure в службе автоматизации Azure | Документы Microsoft"
description: "Как toovertically масштабирования виртуальной машины Linux в ответ toomonitoring предупреждения в службе автоматизации Azure"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dcee199e-fa25-44d5-9b25-df564cee9b45
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: singhkay
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee4c1c33a588bd907d107f1828380a8afdaa725e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="vertically-scale-azure-linux-virtual-machine-with-azure-automation"></a><span data-ttu-id="48681-103">Вертикальное масштабирование виртуальной машины Linux в Azure c помощью службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="48681-103">Vertically scale Azure Linux virtual machine with Azure Automation</span></span>
<span data-ttu-id="48681-104">Вертикальное масштабирование — процесс hello увеличения или уменьшения hello ресурсы машины в рабочей нагрузке toohello ответа.</span><span class="sxs-lookup"><span data-stu-id="48681-104">Vertical scaling is hello process of increasing or decreasing hello resources of a machine in response toohello workload.</span></span> <span data-ttu-id="48681-105">В Azure это можно сделать, изменив размер hello hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="48681-105">In Azure this can be accomplished by changing hello size of hello Virtual Machine.</span></span> <span data-ttu-id="48681-106">Это может помочь в следующие сценарии hello</span><span class="sxs-lookup"><span data-stu-id="48681-106">This can help in hello following scenarios</span></span>

* <span data-ttu-id="48681-107">Если hello виртуальной машины не используется часто, вы можете изменить ее работу меньший размер tooreduce tooa ежемесячные расходы</span><span class="sxs-lookup"><span data-stu-id="48681-107">If hello Virtual Machine is not being used frequently, you can resize it down tooa smaller size tooreduce your monthly costs</span></span>
* <span data-ttu-id="48681-108">Если hello виртуальной машины будет видеть пиковой нагрузки, он может быть большего размера tooincrease размер tooa его емкость</span><span class="sxs-lookup"><span data-stu-id="48681-108">If hello Virtual Machine is seeing a peak load, it can be resized tooa larger size tooincrease its capacity</span></span>

<span data-ttu-id="48681-109">Структура Hello для hello действия tooaccomplish это как ниже</span><span class="sxs-lookup"><span data-stu-id="48681-109">hello outline for hello steps tooaccomplish this is as below</span></span>

1. <span data-ttu-id="48681-110">Настройка виртуальных машин tooaccess автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="48681-110">Setup Azure Automation tooaccess your Virtual Machines</span></span>
2. <span data-ttu-id="48681-111">Импортировать Runbook Azure Automation вертикального масштаба hello в подписке</span><span class="sxs-lookup"><span data-stu-id="48681-111">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
3. <span data-ttu-id="48681-112">Добавить модуль runbook tooyour веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="48681-112">Add a webhook tooyour runbook</span></span>
4. <span data-ttu-id="48681-113">Добавление оповещений tooyour виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="48681-113">Add an alert tooyour Virtual Machine</span></span>

> [!NOTE]
> <span data-ttu-id="48681-114">Из-за размера hello hello первую виртуальную машину, размеры hello может масштабироваться, может быть ограничен из-за toohello доступность hello другие размеры в кластере hello текущей виртуальной машины развертывается в.</span><span class="sxs-lookup"><span data-stu-id="48681-114">Because of hello size of hello first Virtual Machine, hello sizes it can be scaled to, may be limited due toohello availability of hello other sizes in hello cluster current Virtual Machine is deployed in.</span></span> <span data-ttu-id="48681-115">В hello опубликованные модули Runbook автоматизации, используемые в этой статье мы позаботимся обращения и масштабирование только в пределах hello ниже пары размер виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="48681-115">In hello published automation runbooks used in this article we take care of this case and only scale within hello below VM size pairs.</span></span> <span data-ttu-id="48681-116">Это означает, что Standard_D1v2 виртуальной машины не внезапно будет масштабировать в сторону tooStandard_G5 или уменьшен tooBasic_A0.</span><span class="sxs-lookup"><span data-stu-id="48681-116">This means that a Standard_D1v2 Virtual Machine will not suddenly be scaled up tooStandard_G5 or scaled down tooBasic_A0.</span></span>
> 
> | <span data-ttu-id="48681-117">Пары размеров виртуальных машин, для которых можно применять вертикальное масштабирование</span><span class="sxs-lookup"><span data-stu-id="48681-117">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="48681-118">Basic_A0</span><span class="sxs-lookup"><span data-stu-id="48681-118">Basic_A0</span></span> |<span data-ttu-id="48681-119">Basic_A4</span><span class="sxs-lookup"><span data-stu-id="48681-119">Basic_A4</span></span> |
> | <span data-ttu-id="48681-120">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="48681-120">Standard_A0</span></span> |<span data-ttu-id="48681-121">Standard_A4</span><span class="sxs-lookup"><span data-stu-id="48681-121">Standard_A4</span></span> |
> | <span data-ttu-id="48681-122">Standard_A5</span><span class="sxs-lookup"><span data-stu-id="48681-122">Standard_A5</span></span> |<span data-ttu-id="48681-123">Standard_A7</span><span class="sxs-lookup"><span data-stu-id="48681-123">Standard_A7</span></span> |
> | <span data-ttu-id="48681-124">Standard_A8</span><span class="sxs-lookup"><span data-stu-id="48681-124">Standard_A8</span></span> |<span data-ttu-id="48681-125">Standard_A9</span><span class="sxs-lookup"><span data-stu-id="48681-125">Standard_A9</span></span> |
> | <span data-ttu-id="48681-126">Standard_A10</span><span class="sxs-lookup"><span data-stu-id="48681-126">Standard_A10</span></span> |<span data-ttu-id="48681-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="48681-127">Standard_A11</span></span> |
> | <span data-ttu-id="48681-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="48681-128">Standard_D1</span></span> |<span data-ttu-id="48681-129">Standard_D4</span><span class="sxs-lookup"><span data-stu-id="48681-129">Standard_D4</span></span> |
> | <span data-ttu-id="48681-130">Standard_D11</span><span class="sxs-lookup"><span data-stu-id="48681-130">Standard_D11</span></span> |<span data-ttu-id="48681-131">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="48681-131">Standard_D14</span></span> |
> | <span data-ttu-id="48681-132">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="48681-132">Standard_DS1</span></span> |<span data-ttu-id="48681-133">Standard_DS4</span><span class="sxs-lookup"><span data-stu-id="48681-133">Standard_DS4</span></span> |
> | <span data-ttu-id="48681-134">Standard_DS11</span><span class="sxs-lookup"><span data-stu-id="48681-134">Standard_DS11</span></span> |<span data-ttu-id="48681-135">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="48681-135">Standard_DS14</span></span> |
> | <span data-ttu-id="48681-136">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="48681-136">Standard_D1v2</span></span> |<span data-ttu-id="48681-137">Standard_D5v2</span><span class="sxs-lookup"><span data-stu-id="48681-137">Standard_D5v2</span></span> |
> | <span data-ttu-id="48681-138">Standard_D11v2</span><span class="sxs-lookup"><span data-stu-id="48681-138">Standard_D11v2</span></span> |<span data-ttu-id="48681-139">Standard_D14v2</span><span class="sxs-lookup"><span data-stu-id="48681-139">Standard_D14v2</span></span> |
> | <span data-ttu-id="48681-140">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="48681-140">Standard_G1</span></span> |<span data-ttu-id="48681-141">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="48681-141">Standard_G5</span></span> |
> | <span data-ttu-id="48681-142">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="48681-142">Standard_GS1</span></span> |<span data-ttu-id="48681-143">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="48681-143">Standard_GS5</span></span> |
> 
> 

## <a name="setup-azure-automation-tooaccess-your-virtual-machines"></a><span data-ttu-id="48681-144">Настройка виртуальных машин tooaccess автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="48681-144">Setup Azure Automation tooaccess your Virtual Machines</span></span>
<span data-ttu-id="48681-145">Hello первое, что необходимо toodo — создать учетную запись службы автоматизации Azure, где будет размещаться hello модулей Runbook используется tooscale hello набора масштабирования виртуальных Машин экземпляры.</span><span class="sxs-lookup"><span data-stu-id="48681-145">hello first thing you need toodo is create an Azure Automation account that will host hello runbooks used tooscale hello VM Scale Set instances.</span></span> <span data-ttu-id="48681-146">Недавно службы автоматизации hello появилась возможность «Запуск от имени учетной записи» hello, что делает настройку hello участника-службы для автоматического запуска модулей Runbook hello от имени пользователя hello очень легко.</span><span class="sxs-lookup"><span data-stu-id="48681-146">Recently hello Automation service introduced hello "Run As account" feature which makes setting up hello Service Principal for automatically running hello runbooks on hello user's behalf very easy.</span></span> <span data-ttu-id="48681-147">Можно прочитать подробнее об этом в статье hello ниже:</span><span class="sxs-lookup"><span data-stu-id="48681-147">You can read more about this in hello article below:</span></span>

* [<span data-ttu-id="48681-148">Проверка подлинности модулей Runbook в Azure с помощью учетной записи запуска от имени</span><span class="sxs-lookup"><span data-stu-id="48681-148">Authenticate Runbooks with Azure Run As account</span></span>](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-hello-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="48681-149">Импортировать Runbook Azure Automation вертикального масштаба hello в подписке</span><span class="sxs-lookup"><span data-stu-id="48681-149">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="48681-150">Hello модулей Runbook, которые необходимы для вертикальное масштабирование виртуальной машины уже опубликована в hello коллекции Runbook автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="48681-150">hello runbooks that are needed for Vertically Scaling your Virtual Machine are already published in hello Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="48681-151">Вам потребуется tooimport их в подписку.</span><span class="sxs-lookup"><span data-stu-id="48681-151">You will need tooimport them into your subscription.</span></span> <span data-ttu-id="48681-152">Вы узнаете, как модули Runbook tooimport, считывая hello следующую статью.</span><span class="sxs-lookup"><span data-stu-id="48681-152">You can learn how tooimport runbooks by reading hello following article.</span></span>

* [<span data-ttu-id="48681-153">Runbook и коллекции модулей для службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="48681-153">Runbook and module galleries for Azure Automation</span></span>](../../automation/automation-runbook-gallery.md)

<span data-ttu-id="48681-154">Hello Runbook, которые требуется импортировать toobe показаны в приведенном ниже рисунке hello</span><span class="sxs-lookup"><span data-stu-id="48681-154">hello runbooks that need toobe imported are shown in hello image below</span></span>

![Импорт модулей Runbook](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-tooyour-runbook"></a><span data-ttu-id="48681-156">Добавить модуль runbook tooyour веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="48681-156">Add a webhook tooyour runbook</span></span>
<span data-ttu-id="48681-157">После импорта модулей Runbook hello необходимо tooadd runbook toohello веб-перехватчика, может быть вызвано предупреждение из виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="48681-157">Once you've imported hello runbooks you'll need tooadd a webhook toohello runbook so it can be triggered by an alert from a Virtual Machine.</span></span> <span data-ttu-id="48681-158">Здесь могут считываться Hello подробные сведения о создании веб-перехватчика для модуля Runbook</span><span class="sxs-lookup"><span data-stu-id="48681-158">hello details of creating a webhook for your Runbook can be read here</span></span>

* [<span data-ttu-id="48681-159">Объекты Webhook в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="48681-159">Azure Automation webhooks</span></span>](../../automation/automation-webhooks.md)

<span data-ttu-id="48681-160">Убедитесь, что копирование веб-перехватчика hello перед закрытием диалогового окна веб-перехватчика hello, как он потребуется в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="48681-160">Make sure you copy hello webhook before closing hello webhook dialog as you will need this in hello next section.</span></span>

## <a name="add-an-alert-tooyour-virtual-machine"></a><span data-ttu-id="48681-161">Добавление оповещений tooyour виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="48681-161">Add an alert tooyour Virtual Machine</span></span>
1. <span data-ttu-id="48681-162">Перейдите в раздел параметров виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="48681-162">Select Virtual Machine settings</span></span>
2. <span data-ttu-id="48681-163">Щелкните "Правила оповещения".</span><span class="sxs-lookup"><span data-stu-id="48681-163">Select "Alert rules"</span></span>
3. <span data-ttu-id="48681-164">Щелкните "Добавить оповещение".</span><span class="sxs-lookup"><span data-stu-id="48681-164">Select "Add alert"</span></span>
4. <span data-ttu-id="48681-165">Выберите оповещение hello метрики toofire на</span><span class="sxs-lookup"><span data-stu-id="48681-165">Select a metric toofire hello alert on</span></span>
5. <span data-ttu-id="48681-166">Выберите условие, что после выполнения будет вызвать предупреждения toofire hello</span><span class="sxs-lookup"><span data-stu-id="48681-166">Select a condition, which when fulfilled will cause hello alert toofire</span></span>
6. <span data-ttu-id="48681-167">Установите пороговое значение для условия hello на шаге 5.</span><span class="sxs-lookup"><span data-stu-id="48681-167">Select a threshold for hello condition in Step 5.</span></span> <span data-ttu-id="48681-168">toobe выполнен</span><span class="sxs-lookup"><span data-stu-id="48681-168">toobe fulfilled</span></span>
7. <span data-ttu-id="48681-169">Выберите в течение периода через какие hello наблюдение за службой проверяет условие hello и пороговое значение в шаги 5 и 6</span><span class="sxs-lookup"><span data-stu-id="48681-169">Select a period over which hello monitoring service will check for hello condition and threshold in Steps 5 & 6</span></span>
8. <span data-ttu-id="48681-170">Вставьте в веб-перехватчика hello, скопированные из предыдущего раздела hello.</span><span class="sxs-lookup"><span data-stu-id="48681-170">Paste in hello webhook you copied from hello previous section.</span></span>

![Добавление оповещений tooVirtual машины 1](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Добавление оповещений tooVirtual Machine 2](./media/vertical-scaling-automation/add-alert-webhook-2.png)

