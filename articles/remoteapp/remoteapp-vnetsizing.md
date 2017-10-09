---
title: "сведения о aaaSizing для виртуальной сети в Azure RemoteApp | Документы Microsoft"
description: "Дополнительные сведения о hello IP адрес требования для Azure RemoteApp, выполнив виртуальной сети"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b6e1c4ba-0236-42b2-bced-69353bf211be
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: f98b831af32c41740b258d122b3e18765be08d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a><span data-ttu-id="cf261-103">Выбор размера виртуальной сети при работе в среде Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="cf261-103">Sizing information for a VNET in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cf261-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="cf261-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="cf261-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="cf261-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="cf261-106">При использовании Azure RemoteApp с помощью виртуальной сети (VNET) RemoteApp использует IP-адресов в подсети hello.</span><span class="sxs-lookup"><span data-stu-id="cf261-106">When you use Azure RemoteApp with a virtual network (VNET), RemoteApp uses IP addresses within hello subnet.</span></span> <span data-ttu-id="cf261-107">На основе hello масштаба службы RemoteApp, необходимо, чтобы tooensure, что подсеть имеет достаточно IP-адресов, доступных для удаленных приложений RemoteApp виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="cf261-107">Based on hello scale of your RemoteApp service, you need tooensure that your subnet has enough IP addresses available for RemoteApp virtual machines.</span></span> <span data-ttu-id="cf261-108">Это руководство по определению размеров сети не является идеальным с учетом того факта, что среда RemoteApp динамически подключает и отключает виртуальные машины в пределах коллекции, однако оно поможет вам подобрать оптимальный диапазон для своей подсети.</span><span class="sxs-lookup"><span data-stu-id="cf261-108">While this sizing guidance isn’t perfect given how RemoteApp dynamically spins up and spins down virtual machines within a collection, it will help you estimate your subnet range.</span></span> <span data-ttu-id="cf261-109">Это особенно важно, как после размещения службы RemoteApp в виртуальную сеть невозможно увеличить размер подсети hello без удаления удаленных приложений RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="cf261-109">This is especially important as, once a RemoteApp service is placed in a VNET, you cannot increase hello subnet size without removing RemoteApp.</span></span>

<span data-ttu-id="cf261-110">Для каждой коллекции RemoteApp, что требуется toorun с максимальной нагрузкой должны иметь 100 IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="cf261-110">For each RemoteApp collection that you want toorun at maximum capacity, you should have 100 IP addresses available.</span></span> <span data-ttu-id="cf261-111">Например при наличии одной коллекции RemoteApp в плана Standard hello и требуется toohave hello максимум 500 пользователей, должен иметь 100 IP-адресов для этой коллекции.</span><span class="sxs-lookup"><span data-stu-id="cf261-111">For example, if you have one RemoteApp collection in hello Standard plan and you want toohave hello maximum 500 users, you should have 100 IP addresses for that collection.</span></span> <span data-ttu-id="cf261-112">Подобным образом необходимо 100 IP-адресов для коллекции RemoteApp в базовый план hello 800 пользователей.</span><span class="sxs-lookup"><span data-stu-id="cf261-112">Similarly, you need 100 IP addresses for a RemoteApp collection in hello Basic plan that has 800 users.</span></span> <span data-ttu-id="cf261-113">Если планируется toohave меньшее число пользователей (меньше, чем максимальное hello), можно уменьшить hello IP-адреса, необходимые для коллекции.</span><span class="sxs-lookup"><span data-stu-id="cf261-113">If you plan toohave fewer users (less than hello maximum), you can reduce hello IP addresses needed per collection.</span></span> <span data-ttu-id="cf261-114">требования к размеру Hello минимальное подсети — 30 IP-адресов (/ 27).</span><span class="sxs-lookup"><span data-stu-id="cf261-114">hello minimum subnet size requirement is 30 IP addresses (/27).</span></span>

<span data-ttu-id="cf261-115">Ознакомьтесь с hello, следуя toomake сведения о том, что виртуальная сеть настроена и работает в реестре должным образом:</span><span class="sxs-lookup"><span data-stu-id="cf261-115">Check out hello following information toomake sure your VNET is configured and working propertly:</span></span>

* [<span data-ttu-id="cf261-116">Перенос из личных tooan виртуальная сеть виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="cf261-116">Migrate from a personal VNET tooan Azure VNET</span></span>](remoteapp-migratevnet.md)
* [<span data-ttu-id="cf261-117">Проверка toouse виртуальной сети Azure hello Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="cf261-117">Validate hello Azure VNET toouse with Azure RemoteApp</span></span>](remoteapp-vnet.md)

