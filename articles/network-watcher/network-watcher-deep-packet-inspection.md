---
title: "aaaPacket проверок с использованием Наблюдатель сети Azure | Документы Microsoft"
description: "В этой статье описывается, как собирает toouse Наблюдатель сети tooperform глубокую проверку пакетов из виртуальной Машины"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b907d00-9c35-40f5-a61e-beb7b782276f
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4aeddcd482edc4df3d63e87b5c4b0788c540850b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="packet-inspection-with-azure-network-watcher"></a><span data-ttu-id="a25da-103">Проверка пакетов в службе наблюдения за сетями Azure</span><span class="sxs-lookup"><span data-stu-id="a25da-103">Packet inspection with Azure Network Watcher</span></span>

<span data-ttu-id="a25da-104">С помощью функции отслеживания пакетов hello Наблюдатель сети, можно инициировать и управления сеансами снимки виртуальных машин Azure hello портале PowerShell, CLI и программно через hello SDK и API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="a25da-104">Using hello packet capture feature of Network Watcher, you can initiate and manage captures sessions on your Azure VMs from hello portal, PowerShell, CLI, and programmatically through hello SDK and REST API.</span></span> <span data-ttu-id="a25da-105">Захват пакетов позволяет tooaddress сценариев, требующих данных на уровне пакетов, предоставляя информацию hello в формате легче работать.</span><span class="sxs-lookup"><span data-stu-id="a25da-105">Packet capture allows you tooaddress scenarios that require packet level data by providing hello information in a readily usable format.</span></span> <span data-ttu-id="a25da-106">Использование средств tooinspect hello данных, можно проверить связям tooand из виртуальных машин и проанализировать сетевой трафик.</span><span class="sxs-lookup"><span data-stu-id="a25da-106">Leveraging freely available tools tooinspect hello data, you can examine communications sent tooand from your VMs and gain insights into your network traffic.</span></span> <span data-ttu-id="a25da-107">Вот некоторые примеры использования данных о собранных пакетах: анализ проблем с сетью или приложениями, обнаружение попыток вторжения и нарушений в сети, поддержание соответствия нормативным требованиям.</span><span class="sxs-lookup"><span data-stu-id="a25da-107">Some example uses of packet capture data include: investigating network or application issues, detecting network misuse and intrusion attempts, or maintaining regulatory compliance.</span></span> <span data-ttu-id="a25da-108">В этой статье показано, как tooopen файл записи пакетов предоставляемые Наблюдатель сети с помощью средства с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="a25da-108">In this article, we show how tooopen a packet capture file provided by Network Watcher using a popular open source tool.</span></span> <span data-ttu-id="a25da-109">Корпорация Майкрософт также предоставляет примеры, показывающие, как идентифицировать нестандартных трафика toocalculate с задержкой подключения и изучить сетевой статистики.</span><span class="sxs-lookup"><span data-stu-id="a25da-109">We will also provide examples showing how toocalculate a connection latency, identify abnormal traffic, and examine networking statistics.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a25da-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="a25da-110">Before you begin</span></span>

<span data-ttu-id="a25da-111">В этой статье рассматривается несколько предварительно настроенных сценариев на основе ранее выполненной операции записи пакетов.</span><span class="sxs-lookup"><span data-stu-id="a25da-111">This article goes through some pre-configured scenarios on a packet capture that was run previously.</span></span> <span data-ttu-id="a25da-112">Эти сценарии демонстрируют возможности, связанные с использованием функции записи пакетов.</span><span class="sxs-lookup"><span data-stu-id="a25da-112">These scenarios illustrate capabilities that can be accessed by reviewing a packet capture.</span></span> <span data-ttu-id="a25da-113">В этом сценарии используется [WireShark](https://www.wireshark.org/) захват пакетов tooinspect hello.</span><span class="sxs-lookup"><span data-stu-id="a25da-113">This scenario uses [WireShark](https://www.wireshark.org/) tooinspect hello packet capture.</span></span>

<span data-ttu-id="a25da-114">Предполагается, что вы уже выполнили запись пакетов на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="a25da-114">This scenario assumes you already ran a packet capture on a virtual machine.</span></span> <span data-ttu-id="a25da-115">как см захват пакетов toocreate toolearn [hello портале снимки пакетов управление](network-watcher-packet-capture-manage-portal.md) или с REST, посетив [управление снимки пакетов с помощью REST API](network-watcher-packet-capture-manage-rest.md).</span><span class="sxs-lookup"><span data-stu-id="a25da-115">toolearn how toocreate a packet capture visit [Manage packet captures with hello portal](network-watcher-packet-capture-manage-portal.md) or with REST by visiting [Managing Packet Captures with REST API](network-watcher-packet-capture-manage-rest.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="a25da-116">Сценарий</span><span class="sxs-lookup"><span data-stu-id="a25da-116">Scenario</span></span>

<span data-ttu-id="a25da-117">В рамках этого сценария вы выполните:</span><span class="sxs-lookup"><span data-stu-id="a25da-117">In this scenario, you:</span></span>

* <span data-ttu-id="a25da-118">анализ записи пакетов;</span><span class="sxs-lookup"><span data-stu-id="a25da-118">Review a packet capture</span></span>

## <a name="calculate-network-latency"></a><span data-ttu-id="a25da-119">расчет задержки в сети.</span><span class="sxs-lookup"><span data-stu-id="a25da-119">Calculate network latency</span></span>

<span data-ttu-id="a25da-120">В этом сценарии показано, как tooview hello начальной кругового пути время Передачи между двумя конечными точками диалога протокола управления передачей (TCP).</span><span class="sxs-lookup"><span data-stu-id="a25da-120">In this scenario, we show how tooview hello initial Round Trip Time (RTT) of a Transmission Control Protocol (TCP) conversation occurring between two endpoints.</span></span>

<span data-ttu-id="a25da-121">При установлении соединения TCP hello первые три пакетов, отправленных в соединении hello выполните шаблон часто называется tooas hello трехэтапного.</span><span class="sxs-lookup"><span data-stu-id="a25da-121">When a TCP connection is established, hello first three packets sent in hello connection follow a pattern commonly referred tooas hello three-way handshake.</span></span> <span data-ttu-id="a25da-122">При этом соединение было установлено, изучив hello отправленных этой подтверждения, начального запроса от клиента hello и ответа от сервера hello первых двух пакетов, можно вычислить hello задержки.</span><span class="sxs-lookup"><span data-stu-id="a25da-122">By examining hello first two packets sent in this handshake, an initial request from hello client and a response from hello server, we can calculate hello latency when this connection was established.</span></span> <span data-ttu-id="a25da-123">Эта задержка — ссылка tooas hello времени кругового пути (Передачи).</span><span class="sxs-lookup"><span data-stu-id="a25da-123">This latency is referred tooas hello Round Trip Time (RTT).</span></span> <span data-ttu-id="a25da-124">Дополнительные сведения о TCP-протокол hello и hello трехэтапного ссылаться toohello следующих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a25da-124">For more information on hello TCP protocol and hello three-way handshake refer toohello following resource.</span></span> <span data-ttu-id="a25da-125">https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span><span class="sxs-lookup"><span data-stu-id="a25da-125">https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span></span>

### <a name="step-1"></a><span data-ttu-id="a25da-126">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="a25da-126">Step 1</span></span>

<span data-ttu-id="a25da-127">Запустите WireShark</span><span class="sxs-lookup"><span data-stu-id="a25da-127">Launch WireShark</span></span>

### <a name="step-2"></a><span data-ttu-id="a25da-128">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="a25da-128">Step 2</span></span>

<span data-ttu-id="a25da-129">Hello нагрузки **.cap** файл из получения пакетов.</span><span class="sxs-lookup"><span data-stu-id="a25da-129">Load hello **.cap** file from your packet capture.</span></span> <span data-ttu-id="a25da-130">Этот файл можно найти в большом двоичном объекте hello, он был сохранен в нашем локально на hello виртуальной машины, в зависимости от того, как настроить.</span><span class="sxs-lookup"><span data-stu-id="a25da-130">This file can be found in hello blob it was saved in our locally on hello virtual machine, depending on how you configured it.</span></span>

### <a name="step-3"></a><span data-ttu-id="a25da-131">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="a25da-131">Step 3</span></span>

<span data-ttu-id="a25da-132">tooview Здравствуйте начальной кругового пути время Передачи в диалогах TCP, мы только увидите приветственных первых двух пакетов, участвующих в подтверждение TCP hello.</span><span class="sxs-lookup"><span data-stu-id="a25da-132">tooview hello initial Round Trip Time (RTT) in TCP conversations, we will only be looking at hello first two packets involved in hello TCP handshake.</span></span> <span data-ttu-id="a25da-133">Мы будем использовать приветственных первых двух пакетов в hello трехэтапного, являющиеся hello [SYN], [SYN, ACK] пакеты.</span><span class="sxs-lookup"><span data-stu-id="a25da-133">We will be using hello first two packets in hello three-way handshake, which are hello [SYN], [SYN, ACK] packets.</span></span> <span data-ttu-id="a25da-134">Они были указаны флаги, установленные в заголовке TCP hello.</span><span class="sxs-lookup"><span data-stu-id="a25da-134">They are named for flags set in hello TCP header.</span></span> <span data-ttu-id="a25da-135">последний пакет приветствия в подтверждении hello, пакет приветствия [ACK], не будет использоваться в этом сценарии.</span><span class="sxs-lookup"><span data-stu-id="a25da-135">hello last packet in hello handshake, hello [ACK] packet, will not be used in this scenario.</span></span> <span data-ttu-id="a25da-136">При отправке пакета Hello [SYN] hello клиента.</span><span class="sxs-lookup"><span data-stu-id="a25da-136">hello [SYN] packet is sent by hello client.</span></span> <span data-ttu-id="a25da-137">После получения hello сервер отправляет пакет приветствия [ACK] как подтверждение получения hello SYN от клиента hello.</span><span class="sxs-lookup"><span data-stu-id="a25da-137">Once it is received hello server sends hello [ACK] packet as an acknowledgement of receiving hello SYN from hello client.</span></span> <span data-ttu-id="a25da-138">Используя hello том, что ответ сервера hello минимальными накладными расходами, вычислять приветствия времени приема-Передачи путем вычитания hello раз, когда пакет приветствия [SYN, ACK] было получено клиентом hello hello времени [SYN] пакетов отправлено клиентом hello.</span><span class="sxs-lookup"><span data-stu-id="a25da-138">Leveraging hello fact that hello server’s response requires very little overhead, we calculate hello RTT by subtracting hello time hello [SYN, ACK] packet was received by hello client by hello time [SYN] packet was sent by hello client.</span></span>

<span data-ttu-id="a25da-139">Это значение мы можем получить с помощью средства WireShark.</span><span class="sxs-lookup"><span data-stu-id="a25da-139">Using WireShark this value is calculated for us.</span></span>

<span data-ttu-id="a25da-140">toomore просматривать первых двух пакетов приветствия в hello TCP трехэтапного, мы будет использовать фильтрацию возможности, предоставляемые WireShark hello.</span><span class="sxs-lookup"><span data-stu-id="a25da-140">toomore easily view hello first two packets in hello TCP three-way handshake, we will utilize hello filtering capability provided by WireShark.</span></span>

<span data-ttu-id="a25da-141">Фильтр tooapply hello в WireShark, разверните hello сегмент «Протокол» пакета [SYN] в вашей записи и просмотрите hello флаги, установленные в заголовке TCP hello.</span><span class="sxs-lookup"><span data-stu-id="a25da-141">tooapply hello filter in WireShark, expand hello “Transmission Control Protocol” Segment of a [SYN] packet in your capture and examine hello flags set in hello TCP header.</span></span>

<span data-ttu-id="a25da-142">Поскольку мы ищем toofilter на всех [SYN] и [SYN, ACK] пакеты в группе флаги cofirm что hello Syn бита too1, а затем щелкните правой кнопкой мыши на бит Syn hello -> применить как фильтр -> выбранные.</span><span class="sxs-lookup"><span data-stu-id="a25da-142">Since we are looking toofilter on all [SYN] and [SYN, ACK] packets, under flags cofirm that hello Syn bit is set too1, then right click on hello Syn bit -> Apply as Filter -> Selected.</span></span>

![Рис. 7.][7]

### <a name="step-4"></a><span data-ttu-id="a25da-144">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="a25da-144">Step 4</span></span>

<span data-ttu-id="a25da-145">Теперь, когда фильтрации пакетов см. в разделе tooonly окно приветствия с hello [SYN] бит, можно легко выбрать диалогов, которые вас интересуют tooview hello начального времени приема-Передачи.</span><span class="sxs-lookup"><span data-stu-id="a25da-145">Now that you have filtered hello window tooonly see packets with hello [SYN] bit set, you can easily select conversations you are interested in tooview hello initial RTT.</span></span> <span data-ttu-id="a25da-146">Простой способ tooview hello времени приема-Передачи в WireShark просто откройте раскрывающийся список hello, помеченные анализа «SEQ/ACK».</span><span class="sxs-lookup"><span data-stu-id="a25da-146">A simple way tooview hello RTT in WireShark simply click hello dropdown marked “SEQ/ACK” analysis.</span></span> <span data-ttu-id="a25da-147">Вы увидите hello отображения времени приема-Передачи.</span><span class="sxs-lookup"><span data-stu-id="a25da-147">You will then see hello RTT displayed.</span></span> <span data-ttu-id="a25da-148">В этом случае hello времени приема-Передачи было 0.0022114 секунд или 2.211 мс.</span><span class="sxs-lookup"><span data-stu-id="a25da-148">In this case, hello RTT was 0.0022114 seconds, or 2.211 ms.</span></span>

![Рис. 8.][8]

## <a name="unwanted-protocols"></a><span data-ttu-id="a25da-150">Нежелательные протоколы</span><span class="sxs-lookup"><span data-stu-id="a25da-150">Unwanted protocols</span></span>

<span data-ttu-id="a25da-151">На вашем экземпляре виртуальной машины, развернутом в Azure, может работать множество приложений.</span><span class="sxs-lookup"><span data-stu-id="a25da-151">You can have many applications running on a virtual machine instance you have deployed in Azure.</span></span> <span data-ttu-id="a25da-152">Многие из этих приложений обмениваются данными по сети hello, возможно без явного разрешения.</span><span class="sxs-lookup"><span data-stu-id="a25da-152">Many of these applications communicate over hello network, perhaps without your explicit permission.</span></span> <span data-ttu-id="a25da-153">С помощью пакета отслеживания toostore сетевого взаимодействия, мы рассмотрим как приложения, идет речь в сети hello и найдите все проблемы.</span><span class="sxs-lookup"><span data-stu-id="a25da-153">Using packet capture toostore network communication, we can investigate how application are talking on hello network and look for any issues.</span></span>

<span data-ttu-id="a25da-154">В этом примере мы проанализируем уже выполненный захват пакетов, чтобы проверить наличие нежелательных протоколов, которые могут указывать на несанкционированное сетевое взаимодействие запущенных на компьютере приложений.</span><span class="sxs-lookup"><span data-stu-id="a25da-154">In this example, we review a previous ran packet capture for unwanted protocols that may indicate unauthorized communication from an application running on your machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="a25da-155">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="a25da-155">Step 1</span></span>

<span data-ttu-id="a25da-156">С помощью hello же выделение в предыдущем сценарии щелкните hello **статистики** > **протокола иерархии**</span><span class="sxs-lookup"><span data-stu-id="a25da-156">Using hello same capture in hello previous scenario click **Statistics** > **Protocol Hierarchy**</span></span>

![Пункт меню "Иерархия протоколов"][2]

<span data-ttu-id="a25da-158">Появится окно иерархии протокола Hello.</span><span class="sxs-lookup"><span data-stu-id="a25da-158">hello protocol hierarchy window appears.</span></span> <span data-ttu-id="a25da-159">Это представление содержит список всех hello протоколы, используемые во время сеанса захвата hello и hello число пакетов, отправленных и полученных с помощью протоколов hello.</span><span class="sxs-lookup"><span data-stu-id="a25da-159">This view provides a list of all hello protocols that were in use during hello capture session and hello number of packets transmitted and received using hello protocols.</span></span> <span data-ttu-id="a25da-160">Это представление позволяет обнаруживать нежелательный трафик на виртуальных машинах или в сети.</span><span class="sxs-lookup"><span data-stu-id="a25da-160">This view can be useful for finding unwanted network traffic on your virtual machines or network.</span></span>

![Открытое представление иерархии протоколов][3]

<span data-ttu-id="a25da-162">Как видно в следующий снимок экрана приветствия произошла трафика с помощью протокола отправляемому BitTorrent hello, который используется для одноранговых toopeer общий доступ к файлам.</span><span class="sxs-lookup"><span data-stu-id="a25da-162">As you can see in hello following screen capture, there was traffic using hello BitTorrent protocol, which is used for peer toopeer file sharing.</span></span> <span data-ttu-id="a25da-163">Как администратор предполагается, что трафик отправляемому BitTorrent toosee этой конкретной виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="a25da-163">As an administrator you do not expect toosee BitTorrent traffic on this particular virtual machines.</span></span> <span data-ttu-id="a25da-164">Теперь можно учитывать трафик, можно будет удалить hello одноранговых toopeer по, установленный на этой виртуальной машины или блок hello трафика с помощью групп безопасности сети или брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="a25da-164">Now you aware of this traffic, you can remove hello peer toopeer software that installed on this virtual machine, or block hello traffic using Network Security Groups or a Firewall.</span></span> <span data-ttu-id="a25da-165">Кроме того вы можете еще toorun захват пакетов по расписанию, что использование протокола hello регулярно можно просмотреть на виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="a25da-165">Additionally, you may elect toorun packet captures on a schedule, so you can review hello protocol use on your virtual machines regularly.</span></span> <span data-ttu-id="a25da-166">Пример на выполнение задач tooautomate сети в azure посещение [отслеживать ресурсы сети со службой автоматизации azure](network-watcher-monitor-with-azure-automation.md)</span><span class="sxs-lookup"><span data-stu-id="a25da-166">For an example on how tooautomate network tasks in azure visit [Monitor network resources with azure automation](network-watcher-monitor-with-azure-automation.md)</span></span>

## <a name="finding-top-destinations-and-ports"></a><span data-ttu-id="a25da-167">Поиск самых активных адресов назначения и портов</span><span class="sxs-lookup"><span data-stu-id="a25da-167">Finding top destinations and ports</span></span>

<span data-ttu-id="a25da-168">Основные сведения о hello типы трафика, hello конечные точки и порты hello по является очень важным при отслеживании и устранения неполадок приложений и ресурсов в сети.</span><span class="sxs-lookup"><span data-stu-id="a25da-168">Understanding hello types of traffic, hello endpoints, and hello ports communicated over is an important when monitoring or troubleshooting applications and resources on your network.</span></span> <span data-ttu-id="a25da-169">Использование файла записи пакетов выше, можно быстро узнать hello основные пункты назначения нашей виртуальной Машины взаимодействует и порты используемого hello.</span><span class="sxs-lookup"><span data-stu-id="a25da-169">Utilizing a packet capture file from above, we can quickly learn hello top destinations our VM is communicating with and hello ports being utilized.</span></span>

### <a name="step-1"></a><span data-ttu-id="a25da-170">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="a25da-170">Step 1</span></span>

<span data-ttu-id="a25da-171">С помощью hello же выделение в предыдущем сценарии щелкните hello **статистики** > **статистику IPv4** > **назначения и порты**</span><span class="sxs-lookup"><span data-stu-id="a25da-171">Using hello same capture in hello previous scenario click **Statistics** > **IPv4 Statistics** > **Destinations and Ports**</span></span>

![Окно захвата пакетов][4]

### <a name="step-2"></a><span data-ttu-id="a25da-173">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="a25da-173">Step 2</span></span>

<span data-ttu-id="a25da-174">Как мы будем по результатам hello строки важные моменты, было несколько подключений через порт 111.</span><span class="sxs-lookup"><span data-stu-id="a25da-174">As we look through hello results a line stands out, there were multiple connections on port 111.</span></span> <span data-ttu-id="a25da-175">наиболее используемых Hello порт был 3389, удаленный рабочий стол, а оставшиеся hello являются динамические порты RPC.</span><span class="sxs-lookup"><span data-stu-id="a25da-175">hello most used port was 3389, which is remote desktop, and hello remaining are RPC dynamic ports.</span></span>

<span data-ttu-id="a25da-176">Этот трафик может ничего не значат, но это порт, который использовался для количества подключений и Неизвестный toohello администратором.</span><span class="sxs-lookup"><span data-stu-id="a25da-176">While this traffic may mean nothing, it is a port that was used for many connections and is unknown toohello administrator.</span></span>

![Рис. 5.][5]

### <a name="step-3"></a><span data-ttu-id="a25da-178">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="a25da-178">Step 3</span></span>

<span data-ttu-id="a25da-179">Теперь, после определения недостаточно, можно отфильтровать нашей отслеживания учетом hello порта порта месте.</span><span class="sxs-lookup"><span data-stu-id="a25da-179">Now that we have determined an out of place port we can filter our capture based on hello port.</span></span>

<span data-ttu-id="a25da-180">Фильтр Hello в этом сценарии будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="a25da-180">hello filter in this scenario would be:</span></span>

```
tcp.port == 111
```

<span data-ttu-id="a25da-181">Мы введите текст фильтра hello выше в текстовом поле фильтра hello и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="a25da-181">We enter hello filter text from above in hello filter textbox and hit enter.</span></span>

![Рис. 6.][6]

<span data-ttu-id="a25da-183">На основе результатов hello видно hello трафик поступает от локальной виртуальной машины на hello одной подсети.</span><span class="sxs-lookup"><span data-stu-id="a25da-183">From hello results, we can see all hello traffic is coming from a local virtual machine on hello same subnet.</span></span> <span data-ttu-id="a25da-184">Если мы по-прежнему не понять, почему происходит этот трафик, мы дальнейшей проверки toodetermine пакетов hello, почему он выполняет эти вызовы на порту 111.</span><span class="sxs-lookup"><span data-stu-id="a25da-184">If we still don’t understand why this traffic is occurring, we can further inspect hello packets toodetermine why it is making these calls on port 111.</span></span> <span data-ttu-id="a25da-185">Эта информация может занять hello соответствующее действие.</span><span class="sxs-lookup"><span data-stu-id="a25da-185">With this information we can take hello appropriate action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a25da-186">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a25da-186">Next steps</span></span>

<span data-ttu-id="a25da-187">Дополнительные сведения о hello других возможностей отладки Наблюдатель сети, посетив [Обзор монитора сети Azure](network-watcher-monitoring-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a25da-187">Learn about hello other diagnostic features of Network Watcher by visiting [Azure network monitoring overview](network-watcher-monitoring-overview.md)</span></span>

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













