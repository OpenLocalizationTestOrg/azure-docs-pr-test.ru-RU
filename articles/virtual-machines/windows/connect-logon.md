---
title: "aaaConnect tooa виртуальной Машины Windows Server | Документы Microsoft"
description: "Узнайте, как tooconnect и вход в систему с помощью виртуальной Машины Windows tooa hello Azure портал и hello модели развертывания диспетчера ресурсов."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ef62b02e-bf35-468d-b4c3-71b63fe7f409
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/01/2017
ms.author: cynthn
ms.openlocfilehash: dc397f435ef165ae5af09f1d037ad3d520bb7ac3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-and-log-on-tooan-azure-virtual-machine-running-windows"></a><span data-ttu-id="66e1c-103">Как tooconnect и вход в систему tooan Azure виртуальные машины под управлением Windows</span><span class="sxs-lookup"><span data-stu-id="66e1c-103">How tooconnect and log on tooan Azure virtual machine running Windows</span></span>
<span data-ttu-id="66e1c-104">Вы воспользуетесь hello **Connect** кнопку в hello Azure портала toostart сеансы удаленного рабочего стола (RDP) с рабочего стола Windows.</span><span class="sxs-lookup"><span data-stu-id="66e1c-104">You'll use hello **Connect** button in hello Azure portal toostart a Remote Desktop (RDP) session from a Windows desktop.</span></span> <span data-ttu-id="66e1c-105">Сначала подключите toohello виртуальную машину, затем войти в систему.</span><span class="sxs-lookup"><span data-stu-id="66e1c-105">First you connect toohello virtual machine, then you log on.</span></span>

<span data-ttu-id="66e1c-106">Если вы пытаетесь tooconnect tooa виртуальной Машине Windows на Mac, необходимо tooinstall клиентом RDP для Mac, например [удаленный рабочий стол Майкрософт](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span><span class="sxs-lookup"><span data-stu-id="66e1c-106">If you are trying tooconnect tooa Windows VM from a Mac, you need tooinstall an RDP client for Mac like [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span></span>

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="66e1c-107">Подключение toohello виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="66e1c-107">Connect toohello virtual machine</span></span>
1. <span data-ttu-id="66e1c-108">Если это еще не сделано, войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="66e1c-108">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="66e1c-109">Hello концентратора меню **виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="66e1c-109">On hello Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="66e1c-110">Выберите виртуальную машину hello из списка hello.</span><span class="sxs-lookup"><span data-stu-id="66e1c-110">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="66e1c-111">В колонке hello для hello виртуальной машины, нажмите кнопку **Connect**.</span><span class="sxs-lookup"><span data-stu-id="66e1c-111">On hello blade for hello virtual machine, click **Connect**.</span></span>
   
    ![Снимок экрана: hello Azure портала отображение как tooconnect tooyour виртуальной Машины.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > <span data-ttu-id="66e1c-113">Если hello **Connect** неактивна кнопка hello портале и вы не подключенных tooAzure через [Express Route](../../expressroute/expressroute-introduction.md) или [через виртуальную Частную сеть для](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) подключения, необходимо toocreate и Назначьте ВМ общедоступный IP-адрес для использования протокола удаленного рабочего СТОЛА.</span><span class="sxs-lookup"><span data-stu-id="66e1c-113">If hello **Connect** button in hello portal is greyed out and you are not connected tooAzure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need toocreate and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="66e1c-114">Дополнительные сведения см. в статье [IP-адреса в Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="66e1c-114">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>
   > 
   > 

## <a name="log-on-toohello-virtual-machine"></a><span data-ttu-id="66e1c-115">Войдите на виртуальную машину toohello</span><span class="sxs-lookup"><span data-stu-id="66e1c-115">Log on toohello virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="66e1c-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="66e1c-116">Next steps</span></span>
<span data-ttu-id="66e1c-117">Если возникли проблемы при попытке tooconnect, см. раздел [подключений удаленного рабочего стола на устранение](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="66e1c-117">If you run into trouble when you try tooconnect, see [Troubleshoot Remote Desktop connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="66e1c-118">В ней описывается процесс диагностики и решения распространенных проблем.</span><span class="sxs-lookup"><span data-stu-id="66e1c-118">This article walks you through diagnosing and resolving common problems.</span></span>

