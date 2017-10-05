---
title: "Выбор размера виртуальной сети при работе в Azure RemoteApp | Документация Майкрософт"
description: "Узнайте о требованиях к IP-адресам для Azure RemoteApp в виртуальной сети"
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
ms.openlocfilehash: 9375981db64ec4a1ae523e958423b5f5787cec33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a><span data-ttu-id="f2cf9-103">Выбор размера виртуальной сети при работе в среде Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="f2cf9-103">Sizing information for a VNET in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f2cf9-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="f2cf9-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f2cf9-105">Дополнительные сведения см. в [объявлении](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="f2cf9-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f2cf9-106">Когда вы работаете с платформой Azure RemoteApp в виртуальной сети (VNET-сети), RemoteApp использует IP-адреса в пределах некоторой подсети.</span><span class="sxs-lookup"><span data-stu-id="f2cf9-106">When you use Azure RemoteApp with a virtual network (VNET), RemoteApp uses IP addresses within the subnet.</span></span> <span data-ttu-id="f2cf9-107">В связи с этим необходимо обеспечить наличие в подсети достаточного количества IP-адресов для виртуальных машин RemoteApp с учетом масштаба развертывания службы RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f2cf9-107">Based on the scale of your RemoteApp service, you need to ensure that your subnet has enough IP addresses available for RemoteApp virtual machines.</span></span> <span data-ttu-id="f2cf9-108">Это руководство по определению размеров сети не является идеальным с учетом того факта, что среда RemoteApp динамически подключает и отключает виртуальные машины в пределах коллекции, однако оно поможет вам подобрать оптимальный диапазон для своей подсети.</span><span class="sxs-lookup"><span data-stu-id="f2cf9-108">While this sizing guidance isn’t perfect given how RemoteApp dynamically spins up and spins down virtual machines within a collection, it will help you estimate your subnet range.</span></span> <span data-ttu-id="f2cf9-109">Это особенно важно в связи с тем, что после развертывания службы RemoteApp в виртуальной сети увеличить размер подсети без удаления RemoteApp невозможно.</span><span class="sxs-lookup"><span data-stu-id="f2cf9-109">This is especially important as, once a RemoteApp service is placed in a VNET, you cannot increase the subnet size without removing RemoteApp.</span></span>

<span data-ttu-id="f2cf9-110">Для каждой коллекции RemoteApp, которая должна поддерживать максимальное число пользователей, необходимо выделить по 100 IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="f2cf9-110">For each RemoteApp collection that you want to run at maximum capacity, you should have 100 IP addresses available.</span></span> <span data-ttu-id="f2cf9-111">Например, если у вас есть одна коллекция RemoteApp в рамках стандартного плана, а максимальное число пользователей составляет 500, для этой коллекции вам потребуется 100 IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="f2cf9-111">For example, if you have one RemoteApp collection in the Standard plan and you want to have the maximum 500 users, you should have 100 IP addresses for that collection.</span></span> <span data-ttu-id="f2cf9-112">И аналогично, вам потребуется 100 IP-адресов для коллекции RemoteApp в рамках базового плана с 800 пользователями.</span><span class="sxs-lookup"><span data-stu-id="f2cf9-112">Similarly, you need 100 IP addresses for a RemoteApp collection in the Basic plan that has 800 users.</span></span> <span data-ttu-id="f2cf9-113">Если количество ваших пользователей будет меньше максимального, число IP-адресов можно сократить.</span><span class="sxs-lookup"><span data-stu-id="f2cf9-113">If you plan to have fewer users (less than the maximum), you can reduce the IP addresses needed per collection.</span></span> <span data-ttu-id="f2cf9-114">Минимальный размер подсети составляет 30 IP-адресов (/27).</span><span class="sxs-lookup"><span data-stu-id="f2cf9-114">The minimum subnet size requirement is 30 IP addresses (/27).</span></span>

<span data-ttu-id="f2cf9-115">Ознакомьтесь со следующими сведениями, чтобы убедиться, что виртуальная сеть настроена и работает должным образом:</span><span class="sxs-lookup"><span data-stu-id="f2cf9-115">Check out the following information to make sure your VNET is configured and working propertly:</span></span>

* [<span data-ttu-id="f2cf9-116">Переход с личной виртуальной сети на виртуальную сеть Azure</span><span class="sxs-lookup"><span data-stu-id="f2cf9-116">Migrate from a personal VNET to an Azure VNET</span></span>](remoteapp-migratevnet.md)
* [<span data-ttu-id="f2cf9-117">Проверка виртуальной сети Azure для использования с Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="f2cf9-117">Validate the Azure VNET to use with Azure RemoteApp</span></span>](remoteapp-vnet.md)

