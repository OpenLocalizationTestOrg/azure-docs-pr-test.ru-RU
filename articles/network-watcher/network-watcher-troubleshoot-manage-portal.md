---
title: "Устранение неполадок шлюза виртуальной сети и подключений Azure (PowerShell) | Документация Майкрософт"
description: "На этой странице объясняется, как устранить неполадки с помощью Наблюдателя за сетями Azure и командлетов PowerShell."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: e135e719d8f267f6a189d0f8a903a49980a5a035
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="9fe7e-103">Устранение неполадок шлюза виртуальной сети и подключений с помощью Наблюдателя за сетями Azure и PowerShell</span><span class="sxs-lookup"><span data-stu-id="9fe7e-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="9fe7e-104">Портал</span><span class="sxs-lookup"><span data-stu-id="9fe7e-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="9fe7e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9fe7e-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="9fe7e-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="9fe7e-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="9fe7e-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9fe7e-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="9fe7e-108">REST API</span><span class="sxs-lookup"><span data-stu-id="9fe7e-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="9fe7e-109">Наблюдатель за сетями предоставляет множество возможностей, так как он позволяет проанализировать сетевые ресурсы в Azure.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="9fe7e-110">Одна из этих возможностей — устранение неполадок в ресурсах.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="9fe7e-111">Процедуру устранения неполадок с ресурсами можно вызывать с помощью портала, PowerShell, интерфейса командной строки или API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="9fe7e-112">При вызове Наблюдатель за сетями проверяет работоспособность шлюза виртуальной сети или подключения и возвращает результаты.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9fe7e-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="9fe7e-113">Before you begin</span></span>

<span data-ttu-id="9fe7e-114">В этом сценарии предполагается, что вы создали Наблюдатель за сетями в соответствии с инструкциями в статье [Create an Azure Network Watcher instance](network-watcher-create.md) (Наблюдатель за сетями: создание экземпляра службы).</span><span class="sxs-lookup"><span data-stu-id="9fe7e-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="9fe7e-115">Список поддерживаемых типов шлюзов см. в разделе [Поддерживаемые типы шлюзов](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="9fe7e-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="9fe7e-116">Обзор</span><span class="sxs-lookup"><span data-stu-id="9fe7e-116">Overview</span></span>

<span data-ttu-id="9fe7e-117">В ходе устранения неполадок с ресурсами вы можете устранить проблемы, возникающие со шлюзами виртуальной сети и подключениями.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-117">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="9fe7e-118">При запросе на устранение неполадок с ресурсами запрашиваются и проверяются журналы.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-118">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="9fe7e-119">По завершении проверки возвращаются результаты.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-119">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="9fe7e-120">Запросы на устранение неполадок с ресурсами выполняются долго, поэтому для возвращения результатов может потребоваться несколько минут.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-120">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="9fe7e-121">Журналы, используемые при устранении неполадок, хранятся в контейнере указанной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-121">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="troubleshoot-a-gateway-or-connection"></a><span data-ttu-id="9fe7e-122">Устранение неполадок шлюза или подключения</span><span class="sxs-lookup"><span data-stu-id="9fe7e-122">Troubleshoot a gateway or connection</span></span>

1. <span data-ttu-id="9fe7e-123">Перейдите на [портал Azure](https://portal.azure.com) и последовательно нажмите **Сети** > **Наблюдатель за сетями** > **Диагностика VPN**</span><span class="sxs-lookup"><span data-stu-id="9fe7e-123">Navigate to the [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **VPN Diagnostics**</span></span>
2. <span data-ttu-id="9fe7e-124">Выберите **подписку**, **группу ресурсов** и **расположение**.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-124">Select a **Subscription**, **Resource Group**, and **Location**.</span></span>
3. <span data-ttu-id="9fe7e-125">Средство устранения неполадок ресурсов возвращает данные о работоспособности ресурса.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-125">Resource troubleshooting returns data about the health of the resource.</span></span> <span data-ttu-id="9fe7e-126">Оно также сохраняет соответствующие журналы в учетную запись хранения для анализа.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-126">It also saves relevant logs to a storage account to be reviewed.</span></span> <span data-ttu-id="9fe7e-127">Щелкните элемент **Учетная запись хранения**, чтобы выбрать учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-127">Click **Storage Account** to select a storage account.</span></span>
4. <span data-ttu-id="9fe7e-128">В колонке **Учетные записи хранения** выберите существующую учетную запись хранения или щелкните **+ Учетная запись хранения**, чтобы создать новую.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-128">On the **Storage accounts** blade, select an existing storage account or click **+ Storage account** to create a new one.</span></span>
5. <span data-ttu-id="9fe7e-129">В колонке **Контейнеры** выберите существующий контейнер или щелкните **+ Контейнер**, чтобы создать новый.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-129">On the **Containers** blade, choose an existing container or click **+ Container** to create a new container.</span></span> <span data-ttu-id="9fe7e-130">По завершении нажмите кнопку **Выбрать**</span><span class="sxs-lookup"><span data-stu-id="9fe7e-130">When complete click **Select**</span></span>
6. <span data-ttu-id="9fe7e-131">Выберите ресурсы Gateway (Шлюз) и Connection (Подключение) для устранения неполадок и нажмите **Start Troubleshooting** (Начать устранение неполадок).</span><span class="sxs-lookup"><span data-stu-id="9fe7e-131">Select the Gateway and Connection resources to troubleshoot and click **Start Troubleshooting**</span></span>

<span data-ttu-id="9fe7e-132">Если выбрано несколько ресурсов, в ресурсах шлюза устранение неполадок выполняется одновременно.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-132">If multiple resources are selected, troubleshooting is run concurrently on gateway resources.</span></span> <span data-ttu-id="9fe7e-133">Но оно не может одновременно выполняться в ресурсах подключения и соответствующего шлюза.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-133">It can not run on a connection and it's associated gateway at the same time.</span></span> <span data-ttu-id="9fe7e-134">Рекомендуется сначала устранять неполадки шлюза, так как устранение неполадок подключения — более долгий процесс.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-134">It is recommended to troubleshoot gateways first as connection troubleshooting is a longer process.</span></span> <span data-ttu-id="9fe7e-135">Когда в ресурсе выполняется диагностика VPN, в столбце **TROUBLESHOOTING STATUS** (Состояние устранения неполадок) отображается состояние **Running** (Выполняется).</span><span class="sxs-lookup"><span data-stu-id="9fe7e-135">While VPN Diagnostics is running on a resource the **TROUBLESHOOTING STATUS** column will show a status of **Running**</span></span>

<span data-ttu-id="9fe7e-136">После завершения устранения неполадок состояние в этом столбце изменяется на **Healthy** (Исправен) или на **Unhealthy** (Неисправен).</span><span class="sxs-lookup"><span data-stu-id="9fe7e-136">When complete, the status column changes to **Healthy** or **Unhealthy**.</span></span>

![Устранение неполадок завершено][2]

## <a name="understanding-the-results"></a><span data-ttu-id="9fe7e-138">Анализ результатов</span><span class="sxs-lookup"><span data-stu-id="9fe7e-138">Understanding the results</span></span>

<span data-ttu-id="9fe7e-139">В окне в разделе **Сведения** на вкладке **Состояние** отображается состояние в результате последнего устранения неполадок, выполненного в выбранном ресурсе.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-139">In the **Details** section of the window, the **Status** tab shows the status of the last troubleshooting run on the selected resource.</span></span> <span data-ttu-id="9fe7e-140">В результатах последней диагностики отображается число минут, прошедших с последнего выполнения.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-140">Results of the latest diagnostic are shown xx minutes after the last run.</span></span>

|<span data-ttu-id="9fe7e-141">Свойство</span><span class="sxs-lookup"><span data-stu-id="9fe7e-141">Property</span></span>  |<span data-ttu-id="9fe7e-142">Описание</span><span class="sxs-lookup"><span data-stu-id="9fe7e-142">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="9fe7e-143">Ресурс</span><span class="sxs-lookup"><span data-stu-id="9fe7e-143">Resource</span></span>     | <span data-ttu-id="9fe7e-144">Ссылка на ресурс.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-144">A link to the resource.</span></span>        |
|<span data-ttu-id="9fe7e-145">Путь к хранилищу</span><span class="sxs-lookup"><span data-stu-id="9fe7e-145">Storage path</span></span>     |  <span data-ttu-id="9fe7e-146">Путь к учетной записи хранения и контейнеру, содержащему журналы (если они были созданы во время выполнения).</span><span class="sxs-lookup"><span data-stu-id="9fe7e-146">Path to the storage account and container that contain the logs (if any were produced during the run).</span></span> <span data-ttu-id="9fe7e-147">Этот параметр не сохраняется после выхода из портала.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-147">This setting does not persist after you leave the portal.</span></span>        |
|<span data-ttu-id="9fe7e-148">Сводка</span><span class="sxs-lookup"><span data-stu-id="9fe7e-148">Summary</span></span>     | <span data-ttu-id="9fe7e-149">Сводка по работоспособности ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-149">Summary of the resource health.</span></span>        |
|<span data-ttu-id="9fe7e-150">Описание</span><span class="sxs-lookup"><span data-stu-id="9fe7e-150">Detail</span></span>     | <span data-ttu-id="9fe7e-151">Подробные сведения о работоспособности ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-151">Detailed information on the resource health.</span></span>        |
|<span data-ttu-id="9fe7e-152">Последний запуск</span><span class="sxs-lookup"><span data-stu-id="9fe7e-152">Last run</span></span>     | <span data-ttu-id="9fe7e-153">Время последнего выполнения устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-153">The time the last time troubleshooting was ran.</span></span>        |


<span data-ttu-id="9fe7e-154">На вкладке **Действие** содержатся общие рекомендации по устранению проблемы.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-154">The **Action** tab provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="9fe7e-155">Если для устранения проблемы можно что-то сделать, предоставляется ссылка на дополнительные инструкции.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-155">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="9fe7e-156">Если дополнительных рекомендаций нет, в ответе указывается URL-адрес, открыв который можно отправить запрос в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-156">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="9fe7e-157">Дополнительные сведения о свойствах ответа, а также о данных, которые он содержит, см. в статье [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md) (Обзор устранения неполадок наблюдателя за сетями).</span><span class="sxs-lookup"><span data-stu-id="9fe7e-157">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>


## <a name="next-steps"></a><span data-ttu-id="9fe7e-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9fe7e-158">Next steps</span></span>

<span data-ttu-id="9fe7e-159">Если изменены параметры, которые мешают VPN-подключению, см. статью [Управление группами безопасности сети с помощью портала](../virtual-network/virtual-network-manage-nsg-arm-portal.md), чтобы найти сведения о группах безопасности сети и соответствующие правила безопасности.</span><span class="sxs-lookup"><span data-stu-id="9fe7e-159">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>


[2]: ./media/network-watcher-troubleshoot-manage-portal/2.png
