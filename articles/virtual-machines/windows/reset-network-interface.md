---
title: "aaaHow tooreset сетевого интерфейса для виртуальной Машины Windows Azure | Документы Microsoft"
description: "Показано, как tooreset сетевой интерфейс для виртуальной Машины Windows Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: genli
ms.openlocfilehash: 1b653820927ef4c3bb8f384a7e752846a8be3da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-network-interface-for-azure-windows-vm"></a>Как tooreset сетевой интерфейс для виртуальной Машины Windows Azure 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Не удается подключиться к виртуальной машине Windows Azure (ВМ) tooMicrosoft после отключения по умолчанию hello сетевого интерфейса (NIC) или вручную устанавливает статический IP-адрес для сетевого адаптера hello. В этой статье показано, как tooreset hello сетевого интерфейса для виртуальной Машины Windows Azure, которая hello удаленного подключения проблема будет устранена.

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a>Сброс сетевого интерфейса

### <a name="for-classic-vms"></a>Классические виртуальные машины

tooreset сетевого интерфейса, выполните следующие действия:

1.  Go toohello [портал Azure]( https://ms.portal.azure.com).
2.  Выберите **Виртуальные машины (классика)**.
3.  Выберите hello влияет на виртуальной машине.
4.  Выберите **IP-адреса**.
5.  Если hello **частный IP-адрес назначения** не **статических**, измените его слишком**статических**.
6.  Изменение hello **IP-адрес** tooanother IP-адрес, доступный в подсети hello.
7.  Щелкните "Сохранить".
8.  Hello виртуальная машина будет перезагружена toohello системы tooinitialize hello новый сетевой Адаптер.
9.  Попробуйте tooRDP tooyour машины. В случае успешного выполнения при желании можно изменить hello частный IP-адрес адрес обратной toohello исходного. или использовать прежний. 

### <a name="for-vms-deployed-in-resource-group-model"></a>Виртуальные машины, развернутые в модели группы ресурсов

1.  Go toohello [портал Azure]( https://ms.portal.azure.com).
2.  Выберите hello влияет на виртуальной машине.
3.  Выберите **Сетевые интерфейсы**.
4.  Выберите hello сетевого интерфейса, связанного с компьютера
5.  Щелкните **IP configurations** (Конфигурации IP).
6.  Выберите IP-адрес hello. 
7.  Если hello **частный IP-адрес назначения** не **статических**, измените его слишком**статических**.
8.  Изменение hello **IP-адрес** tooanother IP-адрес, доступный в подсети hello.
9. Hello виртуальная машина будет перезагружена toohello системы tooinitialize hello новый сетевой Адаптер.
10. Попробуйте tooRDP tooyour машины. В случае успешного выполнения при желании можно изменить hello частный IP-адрес адрес обратной toohello исходного. или использовать прежний. 

## <a name="delete-hello-unavailable-nics"></a>Удалить hello недоступен сетевых адаптеров
После можно удаленного рабочего стола toohello машины необходимо удалить hello старых сетевых адаптеров tooavoid hello потенциальная проблема:

1.  Откройте диспетчер устройств.
2.  Выберите **Просмотреть** > **Показать скрытые устройства**.
3.  Выберите **Сетевые адаптеры**. 
4.  Проверьте наличие hello адаптеров с именем «Сетевой адаптер Microsoft Hyper-V».
5.  Вы можете увидеть неактивный адаптер. Щелкните правой кнопкой мыши hello адаптера, а затем выберите Удалить.

    ![изображение Hello hello сетевого Адаптера](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > Удаление только hello недоступен адаптеры с именами hello «Сетевой адаптер Microsoft Hyper-V». При удалении любой hello другие скрытые адаптеры, может возникнуть дополнительные проблемы.
    >
    >

6.  Теперь все отключенные адаптеры должны быть удалены из системы.