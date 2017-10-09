---
title: "журналы потока группы безопасности сети aaaManage с Наблюдатель сети Azure | Документы Microsoft"
description: "На этой странице объясняется, как toomanage группы безопасности сети поток входит в Наблюдатель сети Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 01606cbf-d70b-40ad-bc1d-f03bb642e0af
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fb250337ab9d1a0c0d0d3569c00bc221dd102a3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-group-flow-logs-in-hello-azure-portal"></a><span data-ttu-id="2202b-103">Управление журналами потока группы безопасности сети в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="2202b-103">Manage network security group flow logs in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="2202b-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="2202b-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="2202b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2202b-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="2202b-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="2202b-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="2202b-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2202b-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="2202b-108">REST API</span><span class="sxs-lookup"><span data-stu-id="2202b-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="2202b-109">Журналы потока группы безопасности сети являются возможностью Наблюдатель сети, благодаря которой вы tooview сведения о входящего и исходящего IP-трафика через группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="2202b-109">Network security group flow logs are a feature of Network Watcher that enables you tooview information about ingress and egress IP traffic through a network security group.</span></span> <span data-ttu-id="2202b-110">Эти журналы потоков сохраняются в формате JSON и содержат следующие важные сведения:</span><span class="sxs-lookup"><span data-stu-id="2202b-110">These flow logs are written in JSON format and provide important information, including:</span></span> 

- <span data-ttu-id="2202b-111">Входящие и исходящие потоки для каждого правила.</span><span class="sxs-lookup"><span data-stu-id="2202b-111">Outbound and inbound flows on a per-rule basis.</span></span>
- <span data-ttu-id="2202b-112">применяет Hello сетевого Адаптера, hello потока.</span><span class="sxs-lookup"><span data-stu-id="2202b-112">hello NIC that hello flow applies to.</span></span>
- <span data-ttu-id="2202b-113">5-фрагментному сведения о потоке hello (исходный и конечный IP-адрес, порт источника и назначения, протокол).</span><span class="sxs-lookup"><span data-stu-id="2202b-113">5-tuple information about hello flow (source/destination IP, source/destination port, protocol).</span></span>
- <span data-ttu-id="2202b-114">Информация о том, разрешен или запрещен трафик.</span><span class="sxs-lookup"><span data-stu-id="2202b-114">Information about whether traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2202b-115">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="2202b-115">Before you begin</span></span>

<span data-ttu-id="2202b-116">Этот сценарий предполагает уже были выполнены шаги hello в [создать экземпляр Наблюдатель сети](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="2202b-116">This scenario assumes you have already followed hello steps in [Create a Network Watcher instance](network-watcher-create.md).</span></span> <span data-ttu-id="2202b-117">сценарий Hello также предполагается, что группа ресурсов с действительной виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="2202b-117">hello scenario also assumes that a you have a resource group with a valid virtual machine.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="2202b-118">Регистрация поставщика Microsoft Insights</span><span class="sxs-lookup"><span data-stu-id="2202b-118">Register Insights provider</span></span>

<span data-ttu-id="2202b-119">Для потока toowork ведения журнала успешно, hello **помощью Microsoft.Insights** должен быть зарегистрирован поставщик.</span><span class="sxs-lookup"><span data-stu-id="2202b-119">For flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="2202b-120">Поставщик tooregister hello, hello выполните следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="2202b-120">tooregister hello provider, take hello following steps:</span></span> 

1. <span data-ttu-id="2202b-121">Go слишком**подписки**и выберите hello подписки, для которого требуется журналы tooenable потока.</span><span class="sxs-lookup"><span data-stu-id="2202b-121">Go too**Subscriptions**, and then select hello subscription for which you want tooenable flow logs.</span></span> 
2. <span data-ttu-id="2202b-122">На hello **подписки** колонке выберите **поставщиков ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="2202b-122">On hello **Subscription** blade, select **Resource Providers**.</span></span> 
3. <span data-ttu-id="2202b-123">Просмотрите список поставщиков hello и убедитесь, что hello **помощью microsoft.insights** зарегистрирован поставщик.</span><span class="sxs-lookup"><span data-stu-id="2202b-123">Look at hello list of providers, and verify that hello **microsoft.insights** provider is registered.</span></span> <span data-ttu-id="2202b-124">Если он не зарегистрирован, то выберите **Зарегистрировать**.</span><span class="sxs-lookup"><span data-stu-id="2202b-124">If not, then select **Register**.</span></span>

![Просмотр поставщиков][providers]

## <a name="enable-flow-logs"></a><span data-ttu-id="2202b-126">Включение журналов потоков</span><span class="sxs-lookup"><span data-stu-id="2202b-126">Enable flow logs</span></span>

<span data-ttu-id="2202b-127">Следующие действия помогут выполнить процесс hello включения потока журналы на группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="2202b-127">These steps take you through hello process of enabling flow logs on a network security group.</span></span>

### <a name="step-1"></a><span data-ttu-id="2202b-128">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="2202b-128">Step 1</span></span>

<span data-ttu-id="2202b-129">Перейти экземпляр tooa Наблюдатель сети, а затем выберите **NSG потока журналы**.</span><span class="sxs-lookup"><span data-stu-id="2202b-129">Go tooa Network Watcher instance, and then select **NSG Flow logs**.</span></span>

![Обзор журналов потоков][1]

### <a name="step-2"></a><span data-ttu-id="2202b-131">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="2202b-131">Step 2</span></span>

<span data-ttu-id="2202b-132">Выберите группу безопасности сети из списка hello.</span><span class="sxs-lookup"><span data-stu-id="2202b-132">Select a network security group from hello list.</span></span>

![Обзор журналов потоков][2]

### <a name="step-3"></a><span data-ttu-id="2202b-134">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="2202b-134">Step 3</span></span> 

<span data-ttu-id="2202b-135">На hello **параметры журналов потока** колонке задать состояние hello слишком**на**и затем настроить учетную запись хранилища.</span><span class="sxs-lookup"><span data-stu-id="2202b-135">On hello **Flow logs settings** blade, set hello status too**On**, and then configure a storage account.</span></span>  <span data-ttu-id="2202b-136">Закончив, нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="2202b-136">When you're done, select **OK**.</span></span> <span data-ttu-id="2202b-137">Затем выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2202b-137">Then select **Save**.</span></span>

![Обзор журналов потоков][3]

## <a name="download-flow-logs"></a><span data-ttu-id="2202b-139">Скачивание журналов потоков</span><span class="sxs-lookup"><span data-stu-id="2202b-139">Download flow logs</span></span>

<span data-ttu-id="2202b-140">Журналы потоков хранятся в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="2202b-140">Flow logs are saved in a storage account.</span></span> <span data-ttu-id="2202b-141">Загрузить журналы вашего потока tooview их.</span><span class="sxs-lookup"><span data-stu-id="2202b-141">Download your flow logs tooview them.</span></span>

### <a name="step-1"></a><span data-ttu-id="2202b-142">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="2202b-142">Step 1</span></span>

<span data-ttu-id="2202b-143">Выберите журналы потока toodownload, **вы можете загрузить журналы потока из заданного хранилища учетных записей**.</span><span class="sxs-lookup"><span data-stu-id="2202b-143">toodownload flow logs, select **You can download flow logs from configured storage accounts**.</span></span> <span data-ttu-id="2202b-144">Этот шаг принимает вид учетной записи хранилища tooa здесь можно выбрать, какие журналы toodownload.</span><span class="sxs-lookup"><span data-stu-id="2202b-144">This step takes you tooa storage account view where you can choose which logs toodownload.</span></span>

![Параметры журналов потоков][4]

### <a name="step-2"></a><span data-ttu-id="2202b-146">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="2202b-146">Step 2</span></span>

<span data-ttu-id="2202b-147">Go toohello правильного хранения счета.</span><span class="sxs-lookup"><span data-stu-id="2202b-147">Go toohello correct storage account.</span></span> <span data-ttu-id="2202b-148">Выберите **Контейнеры** > **insights-log-networksecuritygroupflowevent**.</span><span class="sxs-lookup"><span data-stu-id="2202b-148">Then select **Containers** > **insights-log-networksecuritygroupflowevent**.</span></span>

![Параметры журналов потоков][5]

### <a name="step-3"></a><span data-ttu-id="2202b-150">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="2202b-150">Step 3</span></span>

<span data-ttu-id="2202b-151">Перейдите в расположение toohello hello потока журнала, выберите его и выберите **загрузить**.</span><span class="sxs-lookup"><span data-stu-id="2202b-151">Go toohello location of hello flow log, select it, and then select **Download**.</span></span>

![Параметры журналов потоков][6]

<span data-ttu-id="2202b-153">Сведения о структуре журнала hello hello [Обзор журнала потока группы безопасности сети](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2202b-153">For information about hello structure of hello log, visit [Network security group flow log overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2202b-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2202b-154">Next steps</span></span>

<span data-ttu-id="2202b-155">Узнайте, каким образом слишком[визуализировать NSG потока журналов с PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="2202b-155">Learn how too[visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
