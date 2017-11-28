---
title: "Управление журналами потоков для групп безопасности сети с помощью наблюдателя за сетями | Документы Майкрософт"
description: "На этой странице объясняется, как управлять журналами потоков для групп безопасности сети с помощью Наблюдателя за сетями."
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
ms.openlocfilehash: 41cb5ffab9bd3a3bed75ffdb6a7383ca1690f810
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-group-flow-logs-in-the-azure-portal"></a><span data-ttu-id="eee94-103">Управление журналами потоков для групп безопасности сети на портале Azure</span><span class="sxs-lookup"><span data-stu-id="eee94-103">Manage network security group flow logs in the Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="eee94-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="eee94-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="eee94-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eee94-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="eee94-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="eee94-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="eee94-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="eee94-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="eee94-108">REST API</span><span class="sxs-lookup"><span data-stu-id="eee94-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="eee94-109">Журналы потоков для групп безопасности сети — это компонент наблюдателя за сетями, который позволяет просматривать сведения о входящем и исходящем IP-трафике через группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="eee94-109">Network security group flow logs are a feature of Network Watcher that enables you to view information about ingress and egress IP traffic through a network security group.</span></span> <span data-ttu-id="eee94-110">Эти журналы потоков сохраняются в формате JSON и содержат следующие важные сведения:</span><span class="sxs-lookup"><span data-stu-id="eee94-110">These flow logs are written in JSON format and provide important information, including:</span></span> 

- <span data-ttu-id="eee94-111">Входящие и исходящие потоки для каждого правила.</span><span class="sxs-lookup"><span data-stu-id="eee94-111">Outbound and inbound flows on a per-rule basis.</span></span>
- <span data-ttu-id="eee94-112">Сетевой адаптер, к которому относится данный поток.</span><span class="sxs-lookup"><span data-stu-id="eee94-112">The NIC that the flow applies to.</span></span>
- <span data-ttu-id="eee94-113">5 видов информации о потоке (исходный и конечный IP-адрес, исходный и конечный порт, протокол).</span><span class="sxs-lookup"><span data-stu-id="eee94-113">5-tuple information about the flow (source/destination IP, source/destination port, protocol).</span></span>
- <span data-ttu-id="eee94-114">Информация о том, разрешен или запрещен трафик.</span><span class="sxs-lookup"><span data-stu-id="eee94-114">Information about whether traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="eee94-115">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="eee94-115">Before you begin</span></span>

<span data-ttu-id="eee94-116">Этот сценарий предполагает, что вы уже выполнили действия, описанные в разделе [Наблюдатель за сетями: создание экземпляра службы](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="eee94-116">This scenario assumes you have already followed the steps in [Create a Network Watcher instance](network-watcher-create.md).</span></span> <span data-ttu-id="eee94-117">Предполагается также, что у вас имеется группа ресурсов с допустимой виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="eee94-117">The scenario also assumes that a you have a resource group with a valid virtual machine.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="eee94-118">Регистрация поставщика Microsoft Insights</span><span class="sxs-lookup"><span data-stu-id="eee94-118">Register Insights provider</span></span>

<span data-ttu-id="eee94-119">Для успешного ведения журналов потоков должен быть зарегистрирован поставщик **Microsoft.Insights**.</span><span class="sxs-lookup"><span data-stu-id="eee94-119">For flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="eee94-120">Чтобы зарегистрировать поставщик, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="eee94-120">To register the provider, take the following steps:</span></span> 

1. <span data-ttu-id="eee94-121">Перейдите в раздел **Подписки** и выберите подписку, для которой требуется включить журналы потока.</span><span class="sxs-lookup"><span data-stu-id="eee94-121">Go to **Subscriptions**, and then select the subscription for which you want to enable flow logs.</span></span> 
2. <span data-ttu-id="eee94-122">В колонке **Подписки** выберите **Поставщики ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="eee94-122">On the **Subscription** blade, select **Resource Providers**.</span></span> 
3. <span data-ttu-id="eee94-123">Просмотрите список поставщиков и убедитесь, что поставщик **microsoft.insights** зарегистрирован.</span><span class="sxs-lookup"><span data-stu-id="eee94-123">Look at the list of providers, and verify that the **microsoft.insights** provider is registered.</span></span> <span data-ttu-id="eee94-124">Если он не зарегистрирован, то выберите **Зарегистрировать**.</span><span class="sxs-lookup"><span data-stu-id="eee94-124">If not, then select **Register**.</span></span>

![Просмотр поставщиков][providers]

## <a name="enable-flow-logs"></a><span data-ttu-id="eee94-126">Включение журналов потоков</span><span class="sxs-lookup"><span data-stu-id="eee94-126">Enable flow logs</span></span>

<span data-ttu-id="eee94-127">Чтобы включить журналы потоков в группе безопасности сети, выполните приведенные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="eee94-127">These steps take you through the process of enabling flow logs on a network security group.</span></span>

### <a name="step-1"></a><span data-ttu-id="eee94-128">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="eee94-128">Step 1</span></span>

<span data-ttu-id="eee94-129">Перейдите к экземпляру наблюдателя за сетями и выберите **Журналы потоков для группы безопасности сети (NSG)**.</span><span class="sxs-lookup"><span data-stu-id="eee94-129">Go to a Network Watcher instance, and then select **NSG Flow logs**.</span></span>

![Обзор журналов потоков][1]

### <a name="step-2"></a><span data-ttu-id="eee94-131">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="eee94-131">Step 2</span></span>

<span data-ttu-id="eee94-132">Выберите в списке нужную группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="eee94-132">Select a network security group from the list.</span></span>

![Обзор журналов потоков][2]

### <a name="step-3"></a><span data-ttu-id="eee94-134">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="eee94-134">Step 3</span></span> 

<span data-ttu-id="eee94-135">В колонке **Параметры журналов потоков**  установите для состояния значение **Вкл.** и настройте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="eee94-135">On the **Flow logs settings** blade, set the status to **On**, and then configure a storage account.</span></span>  <span data-ttu-id="eee94-136">Закончив, нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="eee94-136">When you're done, select **OK**.</span></span> <span data-ttu-id="eee94-137">Затем выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="eee94-137">Then select **Save**.</span></span>

![Обзор журналов потоков][3]

## <a name="download-flow-logs"></a><span data-ttu-id="eee94-139">Скачивание журналов потоков</span><span class="sxs-lookup"><span data-stu-id="eee94-139">Download flow logs</span></span>

<span data-ttu-id="eee94-140">Журналы потоков хранятся в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="eee94-140">Flow logs are saved in a storage account.</span></span> <span data-ttu-id="eee94-141">Для просмотра журналов потоков их необходимо скачать.</span><span class="sxs-lookup"><span data-stu-id="eee94-141">Download your flow logs to view them.</span></span>

### <a name="step-1"></a><span data-ttu-id="eee94-142">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="eee94-142">Step 1</span></span>

<span data-ttu-id="eee94-143">Чтобы скачать журналы потоков, выберите **Журналы потоков можно скачать в настроенных учетных записях хранения**.</span><span class="sxs-lookup"><span data-stu-id="eee94-143">To download flow logs, select **You can download flow logs from configured storage accounts**.</span></span> <span data-ttu-id="eee94-144">После этого в представлении учетной записи хранения выберите, какие журналы следует скачать.</span><span class="sxs-lookup"><span data-stu-id="eee94-144">This step takes you to a storage account view where you can choose which logs to download.</span></span>

![Параметры журналов потоков][4]

### <a name="step-2"></a><span data-ttu-id="eee94-146">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="eee94-146">Step 2</span></span>

<span data-ttu-id="eee94-147">Перейдите к нужной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="eee94-147">Go to the correct storage account.</span></span> <span data-ttu-id="eee94-148">Выберите **Контейнеры** > **insights-log-networksecuritygroupflowevent**.</span><span class="sxs-lookup"><span data-stu-id="eee94-148">Then select **Containers** > **insights-log-networksecuritygroupflowevent**.</span></span>

![Параметры журналов потоков][5]

### <a name="step-3"></a><span data-ttu-id="eee94-150">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="eee94-150">Step 3</span></span>

<span data-ttu-id="eee94-151">Перейдите к расположению журнала потока, выберите его, затем выберите **Скачать**.</span><span class="sxs-lookup"><span data-stu-id="eee94-151">Go to the location of the flow log, select it, and then select **Download**.</span></span>

![Параметры журналов потоков][6]

<span data-ttu-id="eee94-153">Сведения о структуре журнала см. в разделе [Обзор журнала потоков для группы безопасности сети](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eee94-153">For information about the structure of the log, visit [Network security group flow log overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eee94-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eee94-154">Next steps</span></span>

<span data-ttu-id="eee94-155">Узнайте, как [визуализировать журналы потоков для группы безопасности сети с помощью PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="eee94-155">Learn how to [visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
