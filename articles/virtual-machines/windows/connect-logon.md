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
# <a name="how-tooconnect-and-log-on-tooan-azure-virtual-machine-running-windows"></a>Как tooconnect и вход в систему tooan Azure виртуальные машины под управлением Windows
Вы воспользуетесь hello **Connect** кнопку в hello Azure портала toostart сеансы удаленного рабочего стола (RDP) с рабочего стола Windows. Сначала подключите toohello виртуальную машину, затем войти в систему.

Если вы пытаетесь tooconnect tooa виртуальной Машине Windows на Mac, необходимо tooinstall клиентом RDP для Mac, например [удаленный рабочий стол Майкрософт](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).

## <a name="connect-toohello-virtual-machine"></a>Подключение toohello виртуальной машины
1. Если это еще не сделано, войдите в toohello [портал Azure](https://portal.azure.com/).
2. Hello концентратора меню **виртуальные машины**.
3. Выберите виртуальную машину hello из списка hello.
4. В колонке hello для hello виртуальной машины, нажмите кнопку **Connect**.
   
    ![Снимок экрана: hello Azure портала отображение как tooconnect tooyour виртуальной Машины.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > Если hello **Connect** неактивна кнопка hello портале и вы не подключенных tooAzure через [Express Route](../../expressroute/expressroute-introduction.md) или [через виртуальную Частную сеть для](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) подключения, необходимо toocreate и Назначьте ВМ общедоступный IP-адрес для использования протокола удаленного рабочего СТОЛА. Дополнительные сведения см. в статье [IP-адреса в Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).
   > 
   > 

## <a name="log-on-toohello-virtual-machine"></a>Войдите на виртуальную машину toohello
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a>Дальнейшие действия
Если возникли проблемы при попытке tooconnect, см. раздел [подключений удаленного рабочего стола на устранение](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). В ней описывается процесс диагностики и решения распространенных проблем.

