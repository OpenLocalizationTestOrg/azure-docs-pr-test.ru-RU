---
title: "aaaLog на tooa классической виртуальной Машине Azure | Документы Microsoft"
description: "Используйте hello Azure портала toolog на виртуальной машине Windows tooa, созданных с помощью hello классической модели развертывания."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 3c1239ed-07dc-48b8-8b3d-dc8c5f0ab20e
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 2e32b7036c2538e73b46580e0f5f8f4979e8a685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="log-on-tooa-windows-virtual-machine-using-hello-azure-portal"></a>Войдите на tooa виртуальной машины Windows с помощью портала Azure hello
Hello портал Azure, используется в hello **Connect** кнопку toostart сеанс удаленного рабочего стола и войдите в систему виртуальной Машины Windows tooa.

Вы хотите, чтобы tooconnect tooa виртуальных Машин Linux? В разделе [как toolog на tooa виртуальной машине под управлением Linux](../../linux/mac-create-ssh-keys.md).

<!--
Deleting, but not 100% sure
Learn how too[perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Сведения о как toolog на tooa виртуальной Машины с помощью hello диспетчера ресурсов модели см. в разделе [здесь](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="connect-toohello-virtual-machine"></a>Подключение toohello виртуальной машины
1. Войдите в систему toohello портал Azure.
2. Щелкните на виртуальной машине hello, tooaccess. Hello имя указано в hello **все ресурсы** области.

    ![Расположения виртуальных машин](./media/connect-logon/azureportaldashboard.png)

3. Нажмите кнопку **Connect** на панели команд hello поверх панели мониторинга виртуальной машины hello.

    ![Значок для виртуальной машины hello подключения](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If hello **Connect** button isn't available, see hello troubleshooting tips at hello end of this article.
>
>
-->

## <a name="log-on-toohello-virtual-machine"></a>Войдите на виртуальную машину toohello
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a>Дальнейшие действия
* Если hello **Connect** кнопка неактивна, или возникли другие проблемы с подключением удаленного рабочего стола hello, попробуйте сбросить настройки hello. Нажмите кнопку **сбросьте удаленный доступ** из панели мониторинга виртуальной машины hello.

    ![Сброс удаленного доступа](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* Если возникли проблемы с паролем, попробуйте сбросить его. Нажмите кнопку **сброс пароля** вдоль hello левого края панели мониторинга виртуальной машины, в разделе **поддержки + Устранение неполадок**.

    ![Сброс пароля](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

Если эти советы не работают или не то, что нужно, в разделе [tooa подключений удаленного рабочего стола на устранение неполадок виртуальной машины на основе Windows Azure](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). В ней описывается процесс диагностики и решения распространенных проблем.
