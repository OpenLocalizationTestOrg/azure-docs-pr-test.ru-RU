---
title: "группы безопасности сети aaaManage - портал Azure | Документы Microsoft"
description: "Узнайте, как с помощью групп безопасности сети toomanage hello портал Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: faee5ac8-f4c4-4f97-ade5-197a37aad496
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 53fb29e60cbc2a535f6cf03e430d9e703e97b216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-portal"></a>Управление группами безопасности сети с помощью портала Azure hello

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

В этой статье рассматриваются hello модели развертывания диспетчера ресурсов. Вы также можете [создать Nsg в hello классической модели развертывания](virtual-networks-create-nsg-classic-ps.md).

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

Образец Hello PowerShell приведенную ниже команду ожидать простой среде уже создан на основании hello сценарии выше. Toorun hello команд, отображаемых в этом документе, сначала построения необходимо hello тестовой среды, развернув [этот шаблон](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), нажмите кнопку **развертывание tooAzure**, замените значения параметров по умолчанию hello При необходимости и выполнения инструкции hello в hello портала. ниже используйте шагов Hello **RG NSG** как hello имя hello ресурсов группы hello шаблона было развернуто.

## <a name="create-hello-nsg-frontend-nsg"></a>Создать hello переднего плана NSG NSG
toocreate hello **NSG-FrontEnd** NSG, как показано в приведенном выше сценарии hello, выполните шаги hello.

1. В браузере перейдите toohttp://portal.azure.com и при необходимости выполните вход с помощью учетной записи Azure.
2. Щелкните **Обзор >** > **Сетевые группы безопасности**.
   
    ![Портал Azure — группы безопасности сети](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. В hello **сетевых групп безопасности** колонка, щелкните **добавить**.
   
    ![Портал Azure — группы безопасности сети](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. В hello **создать группу безопасности сети** колонке создать NSG с именем *NSG-FrontEnd* в hello *RG NSG* группы ресурсов, а затем щелкните **создать**.
   
    ![Портал Azure — группы безопасности сети](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a>Создание правил в существующей сетевой группе безопасности
правила toocreate в существующей NSG из hello портал Azure, выполните шаги hello.

1. Щелкните **Обзор >** > **Сетевые группы безопасности**.
2. В списке hello Nsg, выберите **NSG-FrontEnd** > **безопасности правила для входящих подключений**
   
    ![Портал Azure — NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. В списке hello **безопасности правила для входящих подключений**, нажмите кнопку **добавить**.
   
    ![Портал Azure — добавление правила](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. В hello **добавить правило безопасности для входящего трафика** колонки, создать правило с именем *правило web* с приоритетом *200* доступ через *TCP* tooport *80* tooany виртуальной Машины из любого источника и нажмите кнопку **ОК**. Обратите внимание, что для большинства этих параметров уже заданы значения по умолчанию.
   
    ![Портал Azure — параметры правила](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. Через несколько секунд hello новое правило появится в hello NSG.
   
    ![Портал Azure — новое правило](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. Повторите шаги too6 toocreate входящее правило с именем *rdp правило* с приоритетом *250* доступ через *TCP* tooport *3389* tooany виртуальной Машины из любого источника.

## <a name="associate-hello-nsg-toohello-frontend-subnet"></a>Связать hello NSG toohello внешней подсети
1. Щелкните **Обзор >** > **Группы ресурсов** > **RG NSG**.
2. В hello **RG NSG** колонка, щелкните **...**   >  **TestVNet**.
   
    ![Портал Azure — TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. В hello **параметры** колонка, щелкните **подсети** > **переднего плана** > **сетевой группы безопасности**  >  **NSG-FrontEnd**.
   
    ![Портал Azure — параметры подсети](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. В hello **переднего плана** колонка, щелкните **Сохранить**.
   
    ![Портал Azure — параметры подсети](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-hello-nsg-backend-nsg"></a>Создать hello серверной NSG NSG
toocreate hello **NSG серверной** NSG и связать его toohello **серверной** подсети, выполните следующие действия hello.

1. Повторите hello шагов в [hello Создание внешнего интерфейса NSG NSG](#Create-the-NSG-FrontEnd-NSG) toocreate NSG с именем *серверной NSG*
2. Повторите hello шагов в [создавать правила в существующей NSG](#Create-rules-in-an-existing-NSG) toocreate hello **входящих** правила в следующей таблице hello.
   
   | Правило входящих подключений | Правило исходящих подключений |
   | --- | --- |
   | ![Портал Azure — правило входящих подключений](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Портал Azure — правило исходящих подключений](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. Повторите hello шагов в [связать hello NSG toohello внешней подсети](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **NSG серверной** NSG toohello **серверной** подсети.

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте, каким образом слишком[Управление существующей Nsg](virtual-network-manage-nsg-arm-portal.md)
* [Включите ведение журнала](virtual-network-nsg-manage-log.md) для групп безопасности сети.

