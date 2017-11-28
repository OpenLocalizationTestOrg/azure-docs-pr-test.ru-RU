---
title: "подключение aaaCheck с Наблюдатель сети Azure — портал Azure | Документы Microsoft"
description: "На этой странице объясняется, как проверить подключение toouse с Наблюдатель сети с помощью портала Azure hello"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: gwallace
ms.openlocfilehash: ef6ecccd688f06f70003a5b59771c15bcbe8f3e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a><span data-ttu-id="c434e-103">Убедитесь в наличии подключения с Наблюдатель сети Azure с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="c434e-103">Check connectivity with Azure Network Watcher using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="c434e-104">Портал</span><span class="sxs-lookup"><span data-stu-id="c434e-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="c434e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c434e-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="c434e-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c434e-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="c434e-107">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="c434e-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="c434e-108">Узнайте, как можно установить toouse tooverify подключения, если прямое подключение TCP от tooa виртуальной машины, заданный конечной точки.</span><span class="sxs-lookup"><span data-stu-id="c434e-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c434e-109">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="c434e-109">Before you begin</span></span>

<span data-ttu-id="c434e-110">В этой статье предполагается, что hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="c434e-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="c434e-111">Экземпляр Наблюдатель сети в регионе hello нужно toocheck подключения.</span><span class="sxs-lookup"><span data-stu-id="c434e-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="c434e-112">Виртуальные машины toocheck подключение.</span><span class="sxs-lookup"><span data-stu-id="c434e-112">Virtual machines toocheck connectivity with.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c434e-113">Для проверки возможности подключения требуется расширение виртуальной машины `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="c434e-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="c434e-114">Установка расширения hello на виртуальной Машине Windows на сайте [расширение виртуальной машины агента Наблюдатель сети Azure для Windows](../virtual-machines/windows/extensions-nwa.md) и виртуальной Машине Linux см. по адресу [расширение виртуальной машины агента Наблюдатель сети Azure для Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="c434e-114">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="c434e-115">Проверьте подключение tooa виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c434e-115">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="c434e-116">В этом примере проверяется подключение tooa целевой виртуальной машине через порт 80.</span><span class="sxs-lookup"><span data-stu-id="c434e-116">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

<span data-ttu-id="c434e-117">Найдите tooyour Наблюдатель сети и нажмите кнопку **проверку подключения (Предварительная версия)**.</span><span class="sxs-lookup"><span data-stu-id="c434e-117">Navigate tooyour Network Watcher and click **Connectivity check (Preview)**.</span></span> <span data-ttu-id="c434e-118">Выберите подключение виртуальной машины toocheck hello.</span><span class="sxs-lookup"><span data-stu-id="c434e-118">Select hello virtual machine toocheck connectivity from.</span></span> <span data-ttu-id="c434e-119">В hello **назначения** выберите **выберите виртуальную машину** и выберите hello соответствующей виртуальной машине и tootest порта.</span><span class="sxs-lookup"><span data-stu-id="c434e-119">In hello **Destination** section choose **Select a virtual machine** and choose hello correct virtual machine and port tootest.</span></span>

<span data-ttu-id="c434e-120">После нажатия кнопки **проверьте**, проверяются hello подключения между виртуальными машинами hello на указанный порт hello.</span><span class="sxs-lookup"><span data-stu-id="c434e-120">Once you click **Check**, hello connectivity between hello virtual machines on hello port specified are checked.</span></span> <span data-ttu-id="c434e-121">В примере hello hello назначения виртуальной Машины недоступен, отображаются список переходов.</span><span class="sxs-lookup"><span data-stu-id="c434e-121">In hello example, hello destination VM is unreachable, a listing of hops are shown.</span></span>

![Результаты проверки возможности подключения виртуальной машины][1]

## <a name="check-remote-endpoint-connectivity"></a><span data-ttu-id="c434e-123">Проверка возможности подключения к удаленной конечной точке</span><span class="sxs-lookup"><span data-stu-id="c434e-123">Check remote endpoint connectivity</span></span>

<span data-ttu-id="c434e-124">подключение toocheck hello и задержки tooa удаленную конечную точку, выберите hello **вручную указать** переключатель в hello **назначения** щелкните входных hello URL-адрес и порт hello, щелкните **проверки** .</span><span class="sxs-lookup"><span data-stu-id="c434e-124">toocheck hello connectivity and latency tooa remote endpoint, choose hello **Specify manually** radio button in hello **Destination** section, input hello url and hello port and click **Check**.</span></span>  <span data-ttu-id="c434e-125">Это используется для таких удаленных конечных точек, такие как конечные точки веб-сайтов и хранилищ.</span><span class="sxs-lookup"><span data-stu-id="c434e-125">This is used for remote endpoints like websites and storage endpoints.</span></span>

![Результаты проверки возможности подключения веб-сайта][2]

## <a name="next-steps"></a><span data-ttu-id="c434e-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c434e-127">Next steps</span></span>

<span data-ttu-id="c434e-128">Узнайте, как снимки tooautomate пакетов с оповещениями виртуальной машины, просмотрев [создать получения оповещений триггеру пакетов](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="c434e-128">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="c434e-129">Сведения о состоянии (разрешен или запрещен) входящего и исходящего трафика виртуальной машины см. в статье, посвященной [проверке потока IP-адресов](network-watcher-check-ip-flow-verify-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c434e-129">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
