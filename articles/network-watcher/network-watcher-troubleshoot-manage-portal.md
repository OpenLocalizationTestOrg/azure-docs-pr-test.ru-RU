---
title: "aaaTroubleshoot шлюз виртуальной сети Azure и соединения — PowerShell | Документы Microsoft"
description: "На этой странице объясняется, как toouse hello Наблюдатель сети Azure устранения командлет PowerShell"
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
ms.openlocfilehash: bd568d34091209390c57d22475559bdb99ad2c59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="ced9f-103">Устранение неполадок шлюза виртуальной сети и подключений с помощью Наблюдателя за сетями Azure и PowerShell</span><span class="sxs-lookup"><span data-stu-id="ced9f-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="ced9f-104">Портал</span><span class="sxs-lookup"><span data-stu-id="ced9f-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="ced9f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ced9f-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="ced9f-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="ced9f-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="ced9f-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ced9f-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="ced9f-108">REST API</span><span class="sxs-lookup"><span data-stu-id="ced9f-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="ced9f-109">Наблюдатель сети предоставляет множество возможностей, по отношению к сетевым ресурсам в Azure toounderstanding.</span><span class="sxs-lookup"><span data-stu-id="ced9f-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="ced9f-110">Одна из этих возможностей — устранение неполадок в ресурсах.</span><span class="sxs-lookup"><span data-stu-id="ced9f-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="ced9f-111">Устранение неполадок ресурсов можно вызвать через портал hello, PowerShell, CLI или REST API.</span><span class="sxs-lookup"><span data-stu-id="ced9f-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="ced9f-112">При вызове Наблюдатель сети проверяет работоспособность hello шлюза виртуальной сети или подключения и возвращает результаты.</span><span class="sxs-lookup"><span data-stu-id="ced9f-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ced9f-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="ced9f-113">Before you begin</span></span>

<span data-ttu-id="ced9f-114">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="ced9f-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="ced9f-115">Список поддерживаемых типов шлюзов см. в разделе [Поддерживаемые типы шлюзов](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="ced9f-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="ced9f-116">Обзор</span><span class="sxs-lookup"><span data-stu-id="ced9f-116">Overview</span></span>

<span data-ttu-id="ced9f-117">Устранение неполадок ресурсов предоставляет возможность hello Устранение неполадок, возникающих с подключениями и шлюзах виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ced9f-117">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="ced9f-118">При запросе tooresource Устранение неполадок, журналы, запросы и проверен.</span><span class="sxs-lookup"><span data-stu-id="ced9f-118">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="ced9f-119">После завершения проверки hello результатов.</span><span class="sxs-lookup"><span data-stu-id="ced9f-119">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="ced9f-120">Запрашивает ресурс, который долго выполняющиеся запросы по устранению неполадок, которой может занять несколько минут tooreturn результат.</span><span class="sxs-lookup"><span data-stu-id="ced9f-120">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="ced9f-121">Устранение неполадок журналы Hello хранятся в контейнер в учетной записи хранилища, который указан.</span><span class="sxs-lookup"><span data-stu-id="ced9f-121">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="troubleshoot-a-gateway-or-connection"></a><span data-ttu-id="ced9f-122">Устранение неполадок шлюза или подключения</span><span class="sxs-lookup"><span data-stu-id="ced9f-122">Troubleshoot a gateway or connection</span></span>

1. <span data-ttu-id="ced9f-123">Перейдите toohello [портал Azure](https://portal.azure.com) и нажмите кнопку **сети** > **Наблюдатель сети** > **диагностики VPN**</span><span class="sxs-lookup"><span data-stu-id="ced9f-123">Navigate toohello [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **VPN Diagnostics**</span></span>
2. <span data-ttu-id="ced9f-124">Выберите **подписку**, **группу ресурсов** и **расположение**.</span><span class="sxs-lookup"><span data-stu-id="ced9f-124">Select a **Subscription**, **Resource Group**, and **Location**.</span></span>
3. <span data-ttu-id="ced9f-125">Устранение неполадок ресурсов возвращает данные о работоспособности hello hello ресурса.</span><span class="sxs-lookup"><span data-stu-id="ced9f-125">Resource troubleshooting returns data about hello health of hello resource.</span></span> <span data-ttu-id="ced9f-126">Он также сохраняет журналы учетной записи хранилища tooa toobe проверены.</span><span class="sxs-lookup"><span data-stu-id="ced9f-126">It also saves relevant logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="ced9f-127">Нажмите кнопку **учетной записи хранилища** tooselect учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="ced9f-127">Click **Storage Account** tooselect a storage account.</span></span>
4. <span data-ttu-id="ced9f-128">На hello **учетные записи хранения** колонке выберите существующую учетную запись хранения или нажмите кнопку **+ учетная запись хранения** toocreate новый.</span><span class="sxs-lookup"><span data-stu-id="ced9f-128">On hello **Storage accounts** blade, select an existing storage account or click **+ Storage account** toocreate a new one.</span></span>
5. <span data-ttu-id="ced9f-129">На hello **контейнеры** колонке выберите существующий контейнер или **+ контейнер** toocreate новый контейнер.</span><span class="sxs-lookup"><span data-stu-id="ced9f-129">On hello **Containers** blade, choose an existing container or click **+ Container** toocreate a new container.</span></span> <span data-ttu-id="ced9f-130">По завершении нажмите кнопку **Выбрать**</span><span class="sxs-lookup"><span data-stu-id="ced9f-130">When complete click **Select**</span></span>
6. <span data-ttu-id="ced9f-131">Выберите ресурсы tootroubleshoot hello шлюза и подключение и нажмите кнопку **запуск устранения неполадок**</span><span class="sxs-lookup"><span data-stu-id="ced9f-131">Select hello Gateway and Connection resources tootroubleshoot and click **Start Troubleshooting**</span></span>

<span data-ttu-id="ced9f-132">Если выбрано несколько ресурсов, в ресурсах шлюза устранение неполадок выполняется одновременно.</span><span class="sxs-lookup"><span data-stu-id="ced9f-132">If multiple resources are selected, troubleshooting is run concurrently on gateway resources.</span></span> <span data-ttu-id="ced9f-133">Он может не работать на подключение и его соответствующее шлюзе hello то же время.</span><span class="sxs-lookup"><span data-stu-id="ced9f-133">It can not run on a connection and it's associated gateway at hello same time.</span></span> <span data-ttu-id="ced9f-134">Шлюзы tootroubleshoot, рекомендуется сначала Устранение неполадок при подключении занимает больше времени.</span><span class="sxs-lookup"><span data-stu-id="ced9f-134">It is recommended tootroubleshoot gateways first as connection troubleshooting is a longer process.</span></span> <span data-ttu-id="ced9f-135">При диагностике VPN от hello ресурсов **Устранение неполадок СОСТОЯНИЯ** столбце будет отображаться статус **под управлением**</span><span class="sxs-lookup"><span data-stu-id="ced9f-135">While VPN Diagnostics is running on a resource hello **TROUBLESHOOTING STATUS** column will show a status of **Running**</span></span>

<span data-ttu-id="ced9f-136">По завершении hello изменения состояния столбцов слишком**Исправен** или **Unhealthy**.</span><span class="sxs-lookup"><span data-stu-id="ced9f-136">When complete, hello status column changes too**Healthy** or **Unhealthy**.</span></span>

![Устранение неполадок завершено][2]

## <a name="understanding-hello-results"></a><span data-ttu-id="ced9f-138">Основные сведения о результатах hello</span><span class="sxs-lookup"><span data-stu-id="ced9f-138">Understanding hello results</span></span>

<span data-ttu-id="ced9f-139">В hello **сведения** разделе окна hello hello **состояние** вкладке отображается состояние последнего Устранение неполадок hello hello выполнения hello выбранного ресурса.</span><span class="sxs-lookup"><span data-stu-id="ced9f-139">In hello **Details** section of hello window, hello **Status** tab shows hello status of hello last troubleshooting run on hello selected resource.</span></span> <span data-ttu-id="ced9f-140">Результаты последних диагностики hello, показано xx минут после последнего выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="ced9f-140">Results of hello latest diagnostic are shown xx minutes after hello last run.</span></span>

|<span data-ttu-id="ced9f-141">Свойство</span><span class="sxs-lookup"><span data-stu-id="ced9f-141">Property</span></span>  |<span data-ttu-id="ced9f-142">Описание</span><span class="sxs-lookup"><span data-stu-id="ced9f-142">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="ced9f-143">Ресурс</span><span class="sxs-lookup"><span data-stu-id="ced9f-143">Resource</span></span>     | <span data-ttu-id="ced9f-144">Ресурс toohello ссылку.</span><span class="sxs-lookup"><span data-stu-id="ced9f-144">A link toohello resource.</span></span>        |
|<span data-ttu-id="ced9f-145">Путь к хранилищу</span><span class="sxs-lookup"><span data-stu-id="ced9f-145">Storage path</span></span>     |  <span data-ttu-id="ced9f-146">Учетная запись хранения toohello путь и контейнера, содержащие hello журналы (если они все были созданы во время выполнения hello).</span><span class="sxs-lookup"><span data-stu-id="ced9f-146">Path toohello storage account and container that contain hello logs (if any were produced during hello run).</span></span> <span data-ttu-id="ced9f-147">Этот параметр не сохраняется после выхода из портала hello.</span><span class="sxs-lookup"><span data-stu-id="ced9f-147">This setting does not persist after you leave hello portal.</span></span>        |
|<span data-ttu-id="ced9f-148">Сводка</span><span class="sxs-lookup"><span data-stu-id="ced9f-148">Summary</span></span>     | <span data-ttu-id="ced9f-149">Сводка об исправности ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="ced9f-149">Summary of hello resource health.</span></span>        |
|<span data-ttu-id="ced9f-150">Описание</span><span class="sxs-lookup"><span data-stu-id="ced9f-150">Detail</span></span>     | <span data-ttu-id="ced9f-151">Подробные сведения о работоспособности ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="ced9f-151">Detailed information on hello resource health.</span></span>        |
|<span data-ttu-id="ced9f-152">Последний запуск</span><span class="sxs-lookup"><span data-stu-id="ced9f-152">Last run</span></span>     | <span data-ttu-id="ced9f-153">Здравствуйте hello времени последнего неполадок была выполнена.</span><span class="sxs-lookup"><span data-stu-id="ced9f-153">hello time hello last time troubleshooting was ran.</span></span>        |


<span data-ttu-id="ced9f-154">Hello **действия** вкладку даются общие рекомендации по как tooresolve hello проблему.</span><span class="sxs-lookup"><span data-stu-id="ced9f-154">hello **Action** tab provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="ced9f-155">Если действие может устранить проблему hello, ссылка предоставляется с Дополнительные рекомендации.</span><span class="sxs-lookup"><span data-stu-id="ced9f-155">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="ced9f-156">В случае hello которых нет Дополнительные рекомендации, ответ hello предоставляет tooopen URL-адрес hello обращение в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="ced9f-156">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="ced9f-157">Дополнительные сведения о свойствах hello ответа hello и которые не включены [Общие сведения об устранении Наблюдатель сети](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ced9f-157">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>


## <a name="next-steps"></a><span data-ttu-id="ced9f-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ced9f-158">Next steps</span></span>

<span data-ttu-id="ced9f-159">Если параметры были изменены, остановите подключения VPN, см. раздел [Управление группами безопасности сети](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack вниз hello правила сетевой безопасности группы и безопасности, возможно, в вопросе.</span><span class="sxs-lookup"><span data-stu-id="ced9f-159">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>


[2]: ./media/network-watcher-troubleshoot-manage-portal/2.png
