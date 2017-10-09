---
title: "aaaValidate toouse виртуальной сети Azure hello Azure RemoteApp. | Документы Microsoft"
description: "Узнайте, как toomake убедитесь, что виртуальная сеть Azure готова toouse Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b573ba02-4587-4be5-9821-27bd891a73b2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 5587556c264356e6ab6039b983a38cb2b95ed268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="validate-hello-azure-vnet-toouse-with-azure-remoteapp"></a><span data-ttu-id="5a955-103">Проверка toouse виртуальной сети Azure hello Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5a955-103">Validate hello Azure VNET toouse with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5a955-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="5a955-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="5a955-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="5a955-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="5a955-106">Прежде чем использовать виртуальной сети Azure с Azure RemoteApp, может потребоваться toovalidate hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="5a955-106">Before you use an Azure VNET with Azure RemoteApp, you might want toovalidate hello VNET.</span></span> <span data-ttu-id="5a955-107">Это помогает избежать проблем с подключением.</span><span class="sxs-lookup"><span data-stu-id="5a955-107">This helps prevent issues with connectivity.</span></span>

<span data-ttu-id="5a955-108">toovalidate сети Azure hello следующие:</span><span class="sxs-lookup"><span data-stu-id="5a955-108">toovalidate your Azure VNET, do hello following:</span></span>

1. <span data-ttu-id="5a955-109">Создание виртуальной машины Azure в подсети hello hello виртуальной сети Azure, требуется toouse с Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5a955-109">Create an Azure virtual machine inside hello subnet of hello Azure VNET you want toouse with Azure RemoteApp.</span></span>
2. <span data-ttu-id="5a955-110">Подключение toothat виртуальной Машины с помощью hello **Connect** параметр на портале управления hello.</span><span class="sxs-lookup"><span data-stu-id="5a955-110">Connect toothat VM by using hello **Connect** option in hello management portal.</span></span>
3. <span data-ttu-id="5a955-111">Присоединение виртуальной машины toohello hello того же домена, что toouse с Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5a955-111">Join hello virtual machine toohello same domain that you want toouse with Azure RemoteApp.</span></span> <span data-ttu-id="5a955-112">При создании гибридной коллекции, который подключается tooyour локальной сети, присоедините hello виртуальной машины tooyour локального домена.</span><span class="sxs-lookup"><span data-stu-id="5a955-112">If you are creating a hybrid collection that connects tooyour on-premises network, join hello virtual machine tooyour local domain.</span></span>

<span data-ttu-id="5a955-113">При успешном выполнении это hello виртуальной сети Azure — Готово toouse с RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5a955-113">If this is successful, hello Azure VNET is ready toouse with RemoteApp.</span></span>

<span data-ttu-id="5a955-114">Дополнительные сведения о рабочем процессе сбора гибридного конца в конец hello см. следующие статьи hello:</span><span class="sxs-lookup"><span data-stu-id="5a955-114">For more information about hello end-to-end hybrid collection workflow, see hello following articles:</span></span>

* [<span data-ttu-id="5a955-115">Как tooplan виртуальной сети Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="5a955-115">How tooplan your virtual network for Azure RemoteApp</span></span>](remoteapp-planvnet.md)
* [<span data-ttu-id="5a955-116">Создание гибридной коллекции</span><span class="sxs-lookup"><span data-stu-id="5a955-116">Create a hybrid collection</span></span>](remoteapp-create-hybrid-deployment.md)
* [<span data-ttu-id="5a955-117">Развертывание Azure RemoteApp коллекции tooyour виртуальной сети Azure (с поддержкой ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="5a955-117">Deploy Azure RemoteApp collection tooyour Azure Virtual Network (with support for ExpressRoute)</span></span>](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)

