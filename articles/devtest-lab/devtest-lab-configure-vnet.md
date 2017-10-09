---
title: "aaaConfigure виртуальной сети в Azure DevTest Labs | Документы Microsoft"
description: "Узнайте, как tooconfigure существующую виртуальную сеть и подсети и использовать их на виртуальной машине с Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 6cda99c2-b87e-4047-90a0-5df10d8e9e14
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: a11ce8315e3c540e44aeacc9c5ee3dde014d4621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a>Настройка виртуальной сети в Azure DevTest Labs
Как описано в статье hello [добавить виртуальную Машину с артефакты лаборатории tooa](devtest-lab-add-vm-with-artifacts.md)при создании виртуальной Машины в лаборатории, можно указать настроенная виртуальная сеть. Один сценарий для этого является hello при необходимости tooaccess ресурсам корпоративной сети из виртуальных машин с помощью виртуальной сети, которая была настроена с помощью ExpressRoute или VPN сайтами. Hello следующих разделах приведены как tooadd существующей виртуальной сети в параметры виртуальной сети лаборатории, чтобы он был доступен toochoose при создании виртуальных машин.

## <a name="configure-a-virtual-network-for-a-lab-using-hello-azure-portal"></a>Настройка виртуальной сети для лаборатории, используя hello портал Azure
Hello следующие шаги содержат пошаговые инструкции по добавлению существующей виртуальной сети (и подсети) tooa лаборатории, чтобы его можно использовать при создании виртуальной Машины в hello же лаборатории. 

1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Выберите **более служб**, а затем выберите **DevTest Labs** из списка hello.
3. Выберите из списка hello лабораториям hello требуемой лаборатории. 
4. В колонке hello лаборатории выберите **конфигурации**.
5. В лаборатории hello **конфигурации** колонке выберите **виртуальные сети**.
6. На hello **виртуальные сети** колонки, отображается список виртуальных сетей, настроенных для текущей лаборатории hello, а также виртуальной сети по умолчанию hello, который создается для лаборатории. 
7. Щелкните **+ Добавить**.
   
    ![Добавление существующей виртуальной сети лаборатории tooyour](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. На hello **виртуальная сеть** колонке выберите **[выберите виртуальную сеть]**.
   
    ![Выбор существующей виртуальной сети](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. На hello **виртуальной сети выберите** колонки, выберите hello требуемой виртуальной сети. Hello колонке показывает все hello виртуальными сетями, которые находятся в группе hello же региона в подписке hello hello лаборатории.  
10. После выбора виртуальной сети, возвращаются toohello **виртуальная сеть** выберите подсеть hello в списке hello hello нижней части колонки hello.

    ![Список подсетей](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    Откроется колонка подсети лаборатории Hello.

    ![Колонка "Lab Subnet" (Подсеть лаборатории)](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. Укажите **Lab subnet name** (Имя подсети лаборатории).
12. Выберите tooallow toobe подсети, используемых в лаборатории Создание виртуальной Машины **используется при создании виртуальной машины**.
13. tooenable [общих общедоступный IP-адрес](devtest-lab-shared-ip.md)выберите **включить общую общедоступный IP-адрес**.
14. Выберите tooallow общих IP-адресов в подсети, **разрешение на создание открытый IP**.
15. В hello **максимум виртуальных машин на пользователя** укажите hello максимальное виртуальных машин на пользователя для каждой подсети. Чтобы разрешить использовать неограниченное число виртуальных машин, оставьте это поле пустым.
16. Выберите **ОК** tooclose hello подсети лаборатории колонку.
17. Выберите **Сохранить** tooclose hello виртуальной сети колонку.
18. Теперь, когда hello виртуальная сеть настроена, ее можно выбрать при создании виртуальной Машины. 
    toosee как toocreate виртуальной Машины и указания виртуальной сети см. в статье toohello [добавить виртуальную Машину с артефакты лаборатории tooa](devtest-lab-add-vm-with-artifacts.md). 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Дальнейшие действия
После добавления hello требуемого виртуальной сети лаборатории tooyour hello следующим шагом является слишком[добавления виртуальных Машин лаборатории tooyour](devtest-lab-add-vm-with-artifacts.md).

