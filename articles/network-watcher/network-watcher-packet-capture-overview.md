---
title: "Захват tooPacket aaaIntroduction в Наблюдатель сети Azure | Документы Microsoft"
description: "Эта страница Общие сведения о возможности отслеживания пакетов Наблюдатель сети hello"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3a81afaa-ecd9-4004-b68e-69ab56913356
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2ce01b391b9c1a1c19aa29c8620628c55586df03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toovariable-packet-capture-in-azure-network-watcher"></a><span data-ttu-id="3b418-103">Захват пакетов toovariable введение в инспектор сети Azure</span><span class="sxs-lookup"><span data-stu-id="3b418-103">Introduction toovariable packet capture in Azure Network Watcher</span></span>

<span data-ttu-id="3b418-104">Захват переменной пакетов Наблюдатель сети позволяет toocreate пакет отслеживания сеансов tootrack трафика tooand из виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="3b418-104">Network Watcher variable packet capture allows you toocreate packet capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="3b418-105">Захват пакетов помогает toodiagnose сети аномалий обоих факту и proactivity.</span><span class="sxs-lookup"><span data-stu-id="3b418-105">Packet capture helps toodiagnose network anomalies both reactively and proactivity.</span></span> <span data-ttu-id="3b418-106">Другим пользователям включать сбор статистики сети, получение сведений о сети вторжений, toodebug клиент сервер, связи и многое другое.</span><span class="sxs-lookup"><span data-stu-id="3b418-106">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span>

<span data-ttu-id="3b418-107">Запись пакетов — это расширение виртуальной машины, которое запускается удаленно в службе наблюдения за сетями.</span><span class="sxs-lookup"><span data-stu-id="3b418-107">Packet capture is a virtual machine extension that is remotely started through Network Watcher.</span></span> <span data-ttu-id="3b418-108">Эта возможность облегчает hello нагрузку работающих захват пакетов вручную для требуемого hello виртуальной машины, чтобы экономить время.</span><span class="sxs-lookup"><span data-stu-id="3b418-108">This capability eases hello burden of running a packet capture manually on hello desired virtual machine, which saves valuable time.</span></span> <span data-ttu-id="3b418-109">Захват пакетов может запускаться через портал hello, PowerShell, CLI или REST API.</span><span class="sxs-lookup"><span data-stu-id="3b418-109">Packet capture can be triggered through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="3b418-110">Один из примеров активации записи пакетов — активация с помощью оповещений на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="3b418-110">One example of how packet capture can be triggered is with Virtual Machine alerts.</span></span> <span data-ttu-id="3b418-111">Предоставляются для hello отслеживания сеанса tooensure можно фиксировать трафик, требуется toomonitor, фильтры.</span><span class="sxs-lookup"><span data-stu-id="3b418-111">Filters are provided for hello capture session tooensure you capture traffic you want toomonitor.</span></span> <span data-ttu-id="3b418-112">В фильтрах используются сведениях о пяти кортежах (протокол, локальный IP-адрес, удаленный IP-адрес, локальный порт, удаленный порт).</span><span class="sxs-lookup"><span data-stu-id="3b418-112">Filters are based on 5-tuple (protocol, local IP address, remote IP address, local port, and remote port) information.</span></span> <span data-ttu-id="3b418-113">Hello записанные данные хранятся в hello локальный диск или BLOB-хранилища.</span><span class="sxs-lookup"><span data-stu-id="3b418-113">hello captured data is stored in hello local disk or a storage blob.</span></span> <span data-ttu-id="3b418-114">Установлено ограничение в 10 сеансов записи пакетов на подписку в регионе.</span><span class="sxs-lookup"><span data-stu-id="3b418-114">There is a limit of 10 packet capture sessions per region per subscription.</span></span> <span data-ttu-id="3b418-115">Это ограничение применяется только toohello сеансы и применяется toohello сохраненные файлы записи пакетов локально hello виртуальной Машины или в учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="3b418-115">This limit applies only toohello sessions and does not apply toohello saved packet capture files either locally on hello VM or in a storage account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3b418-116">Для записи пакетов необходимо расширение виртуальной машины `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="3b418-116">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="3b418-117">Установка расширения hello на виртуальной Машине Windows на сайте [расширение виртуальной машины агента Наблюдатель сети Azure для Windows](../virtual-machines/windows/extensions-nwa.md) и виртуальной Машине Linux см. по адресу [расширение виртуальной машины агента Наблюдатель сети Azure для Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="3b418-117">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

<span data-ttu-id="3b418-118">сведения hello tooreduce захвата нужные сведения tooonly hello, hello становятся доступными следующие параметры для сеанса записи пакетов:</span><span class="sxs-lookup"><span data-stu-id="3b418-118">tooreduce hello information you capture tooonly hello information you want, hello following options are available for a packet capture session:</span></span>

<span data-ttu-id="3b418-119">**Параметры записи**</span><span class="sxs-lookup"><span data-stu-id="3b418-119">**Capture configuration**</span></span>

|<span data-ttu-id="3b418-120">Свойство</span><span class="sxs-lookup"><span data-stu-id="3b418-120">Property</span></span>|<span data-ttu-id="3b418-121">Описание</span><span class="sxs-lookup"><span data-stu-id="3b418-121">Description</span></span>|
|---|---|
|<span data-ttu-id="3b418-122">**Максимальное число байтов на пакет (в байтах)**</span><span class="sxs-lookup"><span data-stu-id="3b418-122">**Maximum bytes per packet (bytes)**</span></span> | <span data-ttu-id="3b418-123">Здравствуйте, число байтов из каждого пакета, захваченные, регистрируются все байты, если оставить поле пустым.</span><span class="sxs-lookup"><span data-stu-id="3b418-123">hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="3b418-124">Здравствуйте, число байтов из каждого пакета, захваченные, регистрируются все байты, если оставить поле пустым.</span><span class="sxs-lookup"><span data-stu-id="3b418-124">hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="3b418-125">Если вам требуется только заголовок IPv4 hello – укажите здесь 34</span><span class="sxs-lookup"><span data-stu-id="3b418-125">If you need only hello IPv4 header – indicate 34 here</span></span> |
|<span data-ttu-id="3b418-126">**Максимальное число байтов за сеанс (в байтах)**</span><span class="sxs-lookup"><span data-stu-id="3b418-126">**Maximum bytes per session (bytes)**</span></span> | <span data-ttu-id="3b418-127">Общее число байтов, в который записываются по достижении значения hello hello окончания сеанса.</span><span class="sxs-lookup"><span data-stu-id="3b418-127">Total number of bytes in that are captured, once hello value is reached hello session ends.</span></span>|
|<span data-ttu-id="3b418-128">**Ограничение по времени (в секундах)**</span><span class="sxs-lookup"><span data-stu-id="3b418-128">**Time limit (seconds)**</span></span> | <span data-ttu-id="3b418-129">Задает ограничения времени пакет приветствия записи сеанса.</span><span class="sxs-lookup"><span data-stu-id="3b418-129">Sets a time constraint on hello packet capture session.</span></span> <span data-ttu-id="3b418-130">значение по умолчанию Hello — 18000 секунд или 5 часов.</span><span class="sxs-lookup"><span data-stu-id="3b418-130">hello default value is 18000 seconds or 5 hours.</span></span>|

<span data-ttu-id="3b418-131">**Фильтрация (необязательно)**</span><span class="sxs-lookup"><span data-stu-id="3b418-131">**Filtering (optional)**</span></span>

|<span data-ttu-id="3b418-132">Свойство</span><span class="sxs-lookup"><span data-stu-id="3b418-132">Property</span></span>|<span data-ttu-id="3b418-133">Описание</span><span class="sxs-lookup"><span data-stu-id="3b418-133">Description</span></span>|
|---|---|
|<span data-ttu-id="3b418-134">**Протокол**</span><span class="sxs-lookup"><span data-stu-id="3b418-134">**Protocol**</span></span> | <span data-ttu-id="3b418-135">записать toofilter протокола Hello hello пакета.</span><span class="sxs-lookup"><span data-stu-id="3b418-135">hello protocol toofilter for hello packet capture.</span></span> <span data-ttu-id="3b418-136">Hello доступные значения: TCP, UDP и все.</span><span class="sxs-lookup"><span data-stu-id="3b418-136">hello available values are TCP, UDP, and All.</span></span>|
|<span data-ttu-id="3b418-137">**Локальный IP-адрес**</span><span class="sxs-lookup"><span data-stu-id="3b418-137">**Local IP address**</span></span> | <span data-ttu-id="3b418-138">Это значение фильтрует toopackets захват пакетов hello, где hello локальный IP-адрес соответствует этому значению фильтра.</span><span class="sxs-lookup"><span data-stu-id="3b418-138">This value filters hello packet capture toopackets where hello local IP address matches this filter value.</span></span>|
|<span data-ttu-id="3b418-139">**Локальный порт**</span><span class="sxs-lookup"><span data-stu-id="3b418-139">**Local port**</span></span> | <span data-ttu-id="3b418-140">Этот пакет приветствия значение фильтры записи toopackets, где локальный порт hello соответствует этому значению фильтра.</span><span class="sxs-lookup"><span data-stu-id="3b418-140">This value filters hello packet capture toopackets where hello local port matches this filter value.</span></span>|
|<span data-ttu-id="3b418-141">**Удаленный IP-адрес**</span><span class="sxs-lookup"><span data-stu-id="3b418-141">**Remote IP address**</span></span> | <span data-ttu-id="3b418-142">Этот пакет приветствия значение фильтры записи toopackets, где IP удаленного hello соответствует этому значению фильтра.</span><span class="sxs-lookup"><span data-stu-id="3b418-142">This value filters hello packet capture toopackets where hello remote IP matches this filter value.</span></span>|
|<span data-ttu-id="3b418-143">**Удаленный порт**</span><span class="sxs-lookup"><span data-stu-id="3b418-143">**Remote port**</span></span> | <span data-ttu-id="3b418-144">Этот пакет приветствия значение фильтры записи toopackets, где удаленный порт hello соответствует этому значению фильтра.</span><span class="sxs-lookup"><span data-stu-id="3b418-144">This value filters hello packet capture toopackets where hello remote port matches this filter value.</span></span>|

### <a name="next-steps"></a><span data-ttu-id="3b418-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3b418-145">Next steps</span></span>

<span data-ttu-id="3b418-146">Узнайте, как можно управлять захват пакетов через портал hello, посетив [управление захват пакетов в hello портал Azure](network-watcher-packet-capture-manage-portal.md) или с помощью PowerShell, посетив [управление захвата пакетов с помощью PowerShell](network-watcher-packet-capture-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3b418-146">Learn how you can manage packet captures through hello portal by visiting [Manage packet capture in hello Azure portal](network-watcher-packet-capture-manage-portal.md) or with PowerShell by visiting [Manage Packet Capture with PowerShell](network-watcher-packet-capture-manage-powershell.md).</span></span>

<span data-ttu-id="3b418-147">Узнайте, как снимки упреждающего пакетов toocreate на основе виртуальной машины предупреждений, посетив [создать получения оповещений триггеру пакетов](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="3b418-147">Learn how toocreate proactive packet captures based on virtual machine alerts by visiting [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













