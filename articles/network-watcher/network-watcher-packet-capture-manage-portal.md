---
title: "снимки aaaManage пакетов с Наблюдатель сети Azure — портал Azure | Документы Microsoft"
description: "На этой странице объясняется, как toomanage hello функция записи пакетов Наблюдатель сети с помощью портала Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 59edd945-34ad-4008-809e-ea904781d918
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 431b145ee215b8d9421fb2aacdce08a0de90b35e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-hello-portal"></a><span data-ttu-id="3bc79-103">Управление захват пакетов с помощью Наблюдатель сети Azure с помощью портала hello</span><span class="sxs-lookup"><span data-stu-id="3bc79-103">Manage packet captures with Azure Network Watcher using hello portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="3bc79-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="3bc79-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="3bc79-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3bc79-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="3bc79-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="3bc79-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="3bc79-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3bc79-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="3bc79-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="3bc79-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="3bc79-109">Захват пакетов Наблюдатель сети позволяет tooand toocreate отслеживания сеансов tootrack трафик от виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="3bc79-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="3bc79-110">Можно записать только трафик hello нужные фильтры предоставляются для tooensure сеанс отслеживания hello.</span><span class="sxs-lookup"><span data-stu-id="3bc79-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="3bc79-111">Захват пакетов помогает аномалий toodiagnose сети как реактивный, так и заранее.</span><span class="sxs-lookup"><span data-stu-id="3bc79-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="3bc79-112">Другим пользователям включать сбор статистики сети, получение сведений о сети вторжений, toodebug клиент сервер, связи и многое другое.</span><span class="sxs-lookup"><span data-stu-id="3bc79-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="3bc79-113">Из-за захват пакетов может tooremotely триггера, эта возможность облегчает нагрузку hello выполнения захват пакетов на нужный машины hello, чтобы экономить время и вручную.</span><span class="sxs-lookup"><span data-stu-id="3bc79-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="3bc79-114">В этой статье описывается hello задачи управления, которые в настоящее время доступны для получения пакетов.</span><span class="sxs-lookup"><span data-stu-id="3bc79-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="3bc79-115">**Запуск записи пакета**</span><span class="sxs-lookup"><span data-stu-id="3bc79-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="3bc79-116">**Прекращение записи пакета**</span><span class="sxs-lookup"><span data-stu-id="3bc79-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="3bc79-117">**Удаление записи пакета**</span><span class="sxs-lookup"><span data-stu-id="3bc79-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="3bc79-118">**Скачивание записи пакета**</span><span class="sxs-lookup"><span data-stu-id="3bc79-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="3bc79-119">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="3bc79-119">Before you begin</span></span>

<span data-ttu-id="3bc79-120">В этой статье предполагается, что hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="3bc79-120">This article assumes that you have hello following resources:</span></span>

- <span data-ttu-id="3bc79-121">Экземпляр Наблюдатель сети в регионе hello нужно toocreate захват пакетов</span><span class="sxs-lookup"><span data-stu-id="3bc79-121">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="3bc79-122">Виртуальная машина с пакет приветствия записать расширение включено.</span><span class="sxs-lookup"><span data-stu-id="3bc79-122">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3bc79-123">Для записи пакетов необходимо расширение виртуальной машины `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="3bc79-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="3bc79-124">Установка расширения hello на виртуальной Машине Windows на сайте [расширение виртуальной машины агента Наблюдатель сети Azure для Windows](../virtual-machines/windows/extensions-nwa.md) и виртуальной Машине Linux см. по адресу [расширение виртуальной машины агента Наблюдатель сети Azure для Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="3bc79-124">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

### <a name="packet-capture-agent-extension-through-hello-portal"></a><span data-ttu-id="3bc79-125">Расширения агента захват пакетов через портал hello</span><span class="sxs-lookup"><span data-stu-id="3bc79-125">Packet Capture agent extension through hello portal</span></span>

<span data-ttu-id="3bc79-126">Захват пакетов hello tooinstall агент виртуальной Машины через портал hello перейдите tooyour виртуальную машину, щелкните **расширения** > **добавить** и выполните поиск **агент Наблюдатель сети для Windows**</span><span class="sxs-lookup"><span data-stu-id="3bc79-126">tooinstall hello packet capture VM agent through hello portal, navigate tooyour virtual machine, click **Extensions** > **Add** and search for **Network Watcher Agent for Windows**</span></span>

![Представление агента][agent]

## <a name="packet-capture-overview"></a><span data-ttu-id="3bc79-128">Обзор записи пакетов</span><span class="sxs-lookup"><span data-stu-id="3bc79-128">Packet Capture overview</span></span>

<span data-ttu-id="3bc79-129">Перейдите toohello [портал Azure](https://portal.azure.com) и нажмите кнопку **сети** > **Наблюдатель сети** > **записи пакетов**</span><span class="sxs-lookup"><span data-stu-id="3bc79-129">Navigate toohello [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **Packet Capture**</span></span>

<span data-ttu-id="3bc79-130">страница обзора Hello показывает список всех пакетов запись данных, которые существуют независимо от состояния hello.</span><span class="sxs-lookup"><span data-stu-id="3bc79-130">hello overview page shows a list of all packet captures that exist no matter hello state.</span></span>

> [!NOTE]
> <span data-ttu-id="3bc79-131">Захват пакетов требуется учетная запись хранения toohello подключения через порт 443.</span><span class="sxs-lookup"><span data-stu-id="3bc79-131">Packet capture requires connectivity toohello storage account over port 443.</span></span>

![Страница обзора записи пакетов][1]

## <a name="start-a-packet-capture"></a><span data-ttu-id="3bc79-133">Запуск записи пакета</span><span class="sxs-lookup"><span data-stu-id="3bc79-133">Start a packet capture</span></span>

<span data-ttu-id="3bc79-134">Нажмите кнопку **добавить** toocreate захват пакетов.</span><span class="sxs-lookup"><span data-stu-id="3bc79-134">Click **Add** toocreate a packet capture.</span></span>

<span data-ttu-id="3bc79-135">являются следующие свойства Hello, которые могут быть определены на захват пакетов.</span><span class="sxs-lookup"><span data-stu-id="3bc79-135">hello properties that can be defined on a packet capture are:</span></span>

<span data-ttu-id="3bc79-136">**Основные параметры**</span><span class="sxs-lookup"><span data-stu-id="3bc79-136">**Main settings**</span></span>

- <span data-ttu-id="3bc79-137">**Подписки** -это значение действительно hello подписки, который используется и в каждой подписке необходим экземпляр Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="3bc79-137">**Subscription** - This value is hello subscription that is used, an instance of network watcher is needed in each subscription.</span></span>
- <span data-ttu-id="3bc79-138">**Группа ресурсов** -группа ресурсов hello hello виртуальной машины, которая является целевым.</span><span class="sxs-lookup"><span data-stu-id="3bc79-138">**Resource group** - hello resource group of hello virtual machine that is being targeted.</span></span>
- <span data-ttu-id="3bc79-139">**Целевой виртуальной машины** -hello виртуальной машины, на котором выполняется захват пакетов hello</span><span class="sxs-lookup"><span data-stu-id="3bc79-139">**Target virtual machine** - hello virtual machine that is running hello packet capture</span></span>
- <span data-ttu-id="3bc79-140">**Имя пакета отслеживания** -это значение является именем hello hello записи пакетов.</span><span class="sxs-lookup"><span data-stu-id="3bc79-140">**Packet capture name** - This value is hello name of hello packet capture.</span></span>

<span data-ttu-id="3bc79-141">**Параметры записи**</span><span class="sxs-lookup"><span data-stu-id="3bc79-141">**Capture configuration**</span></span>

- <span data-ttu-id="3bc79-142">**Учетная запись хранения**. Определяет, нужно ли сохранять запись пакетов в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="3bc79-142">**Storage Account** - Determines if packet capture is saved in a storage account.</span></span>
- <span data-ttu-id="3bc79-143">**Файл** -определяет, если захват пакетов будет сохранен локально на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="3bc79-143">**File** - Determines if a packet capture is saved locally on hello virtual machine.</span></span>
- <span data-ttu-id="3bc79-144">**Учетные записи хранения** -захват пакетов hello toosave учетной записи хранения в выбранной hello.</span><span class="sxs-lookup"><span data-stu-id="3bc79-144">**Storage Accounts** - hello selected storage account toosave hello packet capture in.</span></span> <span data-ttu-id="3bc79-145">По умолчанию используется расположение такого вида: https://{имя_учетной_записи_хранения}.blob.core.windows.net/network-watcher-logs/subscriptions/{идентификатор_подписки}/resourcegroups/{имя_группы_ресурсов}/providers/microsoft.compute/virtualmachines/{имя_виртуальной_машины}/{ГГ}/{ММ}/{ДД}/packetcapture_{ЧЧ}_{ММ}_{ММ}_{XXX}.cap.</span><span class="sxs-lookup"><span data-stu-id="3bc79-145">Default location is https://{storage account name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription id}/resourcegroups/{resource group name}/providers/microsoft.compute/virtualmachines/{virtual machine name}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap.</span></span> <span data-ttu-id="3bc79-146">(Этот параметр доступен, только если выбран параметр **Хранилище**.)</span><span class="sxs-lookup"><span data-stu-id="3bc79-146">(Only enabled if **Storage** is selected)</span></span>
- <span data-ttu-id="3bc79-147">**Локальный путь к файлу** -hello локальный путь на захват пакетов hello toosave виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="3bc79-147">**Local file path** - hello local path on a virtual machine toosave hello packet capture.</span></span> <span data-ttu-id="3bc79-148">(Этот параметр доступен, только если выбран параметр **Файл**.)</span><span class="sxs-lookup"><span data-stu-id="3bc79-148">(Only enabled if **File** is selected).</span></span> <span data-ttu-id="3bc79-149">Необходимо указать допустимый путь</span><span class="sxs-lookup"><span data-stu-id="3bc79-149">A Valid path must be supplied</span></span>
- <span data-ttu-id="3bc79-150">**Максимальное число байтов в пакете** -hello число байтов из каждого пакета, захваченные, регистрируются все байты, если оставить поле пустым.</span><span class="sxs-lookup"><span data-stu-id="3bc79-150">**Maximum bytes per packet** - hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span>
- <span data-ttu-id="3bc79-151">**Максимальное число байтов для сеанса** — общее число байтов, записываемых, по достижении значения hello останавливается захват пакетов hello.</span><span class="sxs-lookup"><span data-stu-id="3bc79-151">**Maximum bytes per session** - Total number of bytes that are captured, once hello value is reached hello packet capture stops.</span></span>
- <span data-ttu-id="3bc79-152">**Предельное время (в секундах)** -задает максимальный интервал времени для отслеживания toostop hello пакетов.</span><span class="sxs-lookup"><span data-stu-id="3bc79-152">**Time limit (seconds)** - Sets a time limit for hello packet capture toostop.</span></span> <span data-ttu-id="3bc79-153">По умолчанию это 18000 секунд.</span><span class="sxs-lookup"><span data-stu-id="3bc79-153">Default is 18000 seconds.</span></span>

> [!NOTE]
> <span data-ttu-id="3bc79-154">Учетные записи хранения класса Premium сейчас не поддерживаются для сохранения записи пакетов.</span><span class="sxs-lookup"><span data-stu-id="3bc79-154">Premium storage accounts are currently not supported for storing packet captures.</span></span>

<span data-ttu-id="3bc79-155">**Фильтрация (необязательно)**</span><span class="sxs-lookup"><span data-stu-id="3bc79-155">**Filtering (Optional)**</span></span>

- <span data-ttu-id="3bc79-156">**Протокол** -hello toofilter протокола для получения пакетов hello.</span><span class="sxs-lookup"><span data-stu-id="3bc79-156">**Protocol** - hello protocol toofilter for hello packet capture.</span></span> <span data-ttu-id="3bc79-157">Hello доступные значения: TCP, UDP и любые.</span><span class="sxs-lookup"><span data-stu-id="3bc79-157">hello available values are TCP, UDP, and Any.</span></span>
- <span data-ttu-id="3bc79-158">**Локальный IP-адрес** -это значение фильтрует toopackets захват пакетов hello, где hello локальный IP-адрес соответствует этому значению фильтра.</span><span class="sxs-lookup"><span data-stu-id="3bc79-158">**Local IP address** - This value filters hello packet capture toopackets where hello local IP address matches this filter value.</span></span>
- <span data-ttu-id="3bc79-159">**Локальный порт** -это значение фильтрует toopackets захват пакетов hello, где локальный порт hello соответствует этому значению фильтра.</span><span class="sxs-lookup"><span data-stu-id="3bc79-159">**Local port** - This value filters hello packet capture toopackets where hello local port matches this filter value.</span></span>
- <span data-ttu-id="3bc79-160">**Удаленный IP-адрес** -это значение фильтрует toopackets захват пакетов hello, где IP удаленного hello соответствует этому значению фильтра.</span><span class="sxs-lookup"><span data-stu-id="3bc79-160">**Remote IP address** - This value filters hello packet capture toopackets where hello remote IP matches this filter value.</span></span>
- <span data-ttu-id="3bc79-161">**Удаленный порт** -это значение фильтрует toopackets захват пакетов hello, где удаленный порт hello соответствует этому значению фильтра.</span><span class="sxs-lookup"><span data-stu-id="3bc79-161">**Remote port** - This value filters hello packet capture toopackets where hello remote port matches this filter value.</span></span>

> [!NOTE]
> <span data-ttu-id="3bc79-162">Для портов и IP-адресов можно указать одно значение, диапазон значений или набор.</span><span class="sxs-lookup"><span data-stu-id="3bc79-162">Port and IP address values can be a single value, range of values, or a set.</span></span> <span data-ttu-id="3bc79-163">(Например, диапазон 80-1024 для значений портов.) Можно определить любое число фильтров.</span><span class="sxs-lookup"><span data-stu-id="3bc79-163">(that is, 80-1024 for port) You can define as many filters as you want.</span></span>

<span data-ttu-id="3bc79-164">После заполнения значения hello щелкните **ОК** захват пакетов toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="3bc79-164">Once hello values are filled out, click **OK** toocreate hello packet capture.</span></span>

![Создание записи пакетов][2]

<span data-ttu-id="3bc79-166">После задания hello временное ограничение на захват пакетов hello истек, захват пакетов hello будут остановлены, а также можно просмотреть.</span><span class="sxs-lookup"><span data-stu-id="3bc79-166">After hello time limit set on hello packet capture has expired, hello packet capture will stop and can be reviewed.</span></span> <span data-ttu-id="3bc79-167">Можно также вручную остановить сеансы захват пакетов hello.</span><span class="sxs-lookup"><span data-stu-id="3bc79-167">You can also manually stop hello packet captures sessions.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="3bc79-168">Удаление записи пакета</span><span class="sxs-lookup"><span data-stu-id="3bc79-168">Delete a packet capture</span></span>

<span data-ttu-id="3bc79-169">В пакет приветствия захвата представление, щелкните hello **контекстное меню** (...) или щелкните правой кнопкой мыши и выберите **удалить** захват пакетов toostop hello</span><span class="sxs-lookup"><span data-stu-id="3bc79-169">In hello packet capture view, click hello **context menu** (...) or right click, and click **delete** toostop hello packet capture</span></span>

![Удаление записи пакета][3]

> [!NOTE]
> <span data-ttu-id="3bc79-171">Удаление захват пакетов не приводит к удалению файла hello в учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="3bc79-171">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

<span data-ttu-id="3bc79-172">Будет предложено tooconfirm требуется захват пакетов toodelete hello, нажмите кнопку **Да**</span><span class="sxs-lookup"><span data-stu-id="3bc79-172">You are asked tooconfirm you want toodelete hello packet capture, click **Yes**</span></span>

![Подтверждение][4]

## <a name="stop-a-packet-capture"></a><span data-ttu-id="3bc79-174">Прекращение записи пакета</span><span class="sxs-lookup"><span data-stu-id="3bc79-174">Stop a packet capture</span></span>

<span data-ttu-id="3bc79-175">В пакет приветствия захвата представление, щелкните hello **контекстное меню** (...) или щелкните правой кнопкой мыши и выберите **остановить** захват пакетов toostop hello</span><span class="sxs-lookup"><span data-stu-id="3bc79-175">In hello packet capture view, click hello **context menu** (...) or right click, and click **Stop** toostop hello packet capture</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="3bc79-176">Скачивание записи пакета</span><span class="sxs-lookup"><span data-stu-id="3bc79-176">Download a packet capture</span></span>

<span data-ttu-id="3bc79-177">После завершения сеанса записи пакета файл записи hello — отправленного tooblob хранилища или tooa локальный файл на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="3bc79-177">Once your packet capture session has completed, hello capture file is uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="3bc79-178">место хранения Hello hello захват пакетов определяется при создании сеанса hello.</span><span class="sxs-lookup"><span data-stu-id="3bc79-178">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="3bc79-179">Tooaccess удобное средство их записывать файлы, сохраненные tooa учетную запись хранения является обозреватель хранилищ Microsoft Azure, которую можно загрузить здесь: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="3bc79-179">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="3bc79-180">При указании учетной записи хранилища пакетов отслеживания файлы сохраняются tooa учетной записи хранилища в hello следующие расположения:</span><span class="sxs-lookup"><span data-stu-id="3bc79-180">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="3bc79-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3bc79-181">Next steps</span></span>

<span data-ttu-id="3bc79-182">Узнайте, как снимки tooautomate пакетов с оповещениями виртуальной машины, просмотрев [создать получения оповещений триггеру пакетов](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="3bc79-182">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="3bc79-183">Сведения о состоянии (разрешен или запрещен) входящего и исходящего трафика виртуальной машины см. в статье, посвященной [проверке потока IP-адресов](network-watcher-check-ip-flow-verify-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3bc79-183">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













