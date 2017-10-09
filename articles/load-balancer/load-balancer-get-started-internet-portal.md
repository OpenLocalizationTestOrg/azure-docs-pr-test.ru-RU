---
title: "Подсистема балансировки нагрузки aaaCreate с выходом в Интернет - портал Azure | Документы Microsoft"
description: "Узнайте, как Подсистема балансировки нагрузки toocreate с выходом в Интернет с помощью диспетчера ресурсов hello портал Azure"
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: aa9d26ca-3d8a-4a99-83b7-c410dd20b9d0
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: annahar
ms.openlocfilehash: 390ba8ec1474c54cf2c0022c4a3c219d21b1a659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-hello-azure-portal"></a>Создание балансировки нагрузки с выходом в Интернет с помощью портала Azure hello

> [!div class="op_single_selector"]
> * [Портал](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Интерфейс командной строки Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Шаблон](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

В этой статье рассматриваются hello модели развертывания диспетчера ресурсов. Вы также можете [Узнайте, как с помощью классического развертывания подсистемы балансировки нагрузки, toocreate из Интернета](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

Это соответствует последовательности hello отдельных задач, которые имеют toocreate toobe сделать подсистемы балансировки нагрузки и подробно работы tooaccomplish hello цели.

## <a name="what-is-required-toocreate-an-internet-facing-load-balancer"></a>Что такое необходимые toocreate балансировки нагрузки с выходом в Интернет?

Требуется toocreate и настроить hello следующие объекты toodeploy подсистемы балансировки нагрузки.

* Конфигурация интерфейсных IP-адресов. Содержит общедоступные IP-адреса для входящего сетевого трафика.
* Пул адресов серверной части - содержит сетевых интерфейсов (NIC) для hello виртуальные машины tooreceive сетевой трафик от подсистемы балансировки нагрузки hello.
* Правила балансировки нагрузки — содержит правила сопоставления открытый порт hello tooport подсистемы балансировки нагрузки в пул адресов серверной части hello.
* Правила NAT для входящих подключений — содержит правила, сопоставление порта открытый порт tooa подсистемы балансировки нагрузки hello для конкретной виртуальной машины в пул адресов серверной части hello.
* Проверяет — содержит доступность toocheck проверки, используемые работоспособности экземпляров виртуальных машин в пул адресов серверной части hello.

Дополнительные сведения о настройке компонентов балансировщика нагрузки с помощью Azure Resource Manager см. в статье [Поддержка диспетчера ресурсов Azure для подсистемы балансировки нагрузки](load-balancer-arm.md).

## <a name="set-up-a-load-balancer-in-azure-portal"></a>Настройка балансировщика нагрузки на портале Azure

> [!IMPORTANT]
> В этом примере предполагается, что у вас уже есть виртуальная сеть с именем **myVNet**. См. слишком[создать виртуальную сеть](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) toodo это. Он также предполагает, что имеется подсети в пределах **myVNet** вызывается **балансировки Нагрузки подсеть быть** и две виртуальные машины вызывается **web1** и **web2** соответственно в Здравствуйте же доступности, вызванной **myAvailSet** в **myVNet**. См. слишком[эту ссылку](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toocreate виртуальных машин.

1. В браузере перейдите toohello портала Azure: [http://portal.azure.com](http://portal.azure.com) и выполните вход с учетной записью Azure.
2. Hello верхней левой части экрана приветствия выберите **New** > **сети** > **подсистемы балансировки нагрузки.**
3. В hello **балансировки нагрузки создать** колонки, введите имя для балансировки нагрузки. Здесь он назван **myLoadBalancer**.
4. В разделе **Тип** выберите **Общедоступный**.
5. В разделе **Общедоступный IP-адрес** создайте общедоступный IP-адрес с именем **myPublicIP**.
6. В разделе "Группа ресурсов" выберите **myRG**. Затем укажите соответствующее **Расположение** и нажмите кнопку **ОК**. Подсистема балансировки нагрузки Hello запускается toodeploy и займет несколько минут toosuccessfully полное развертывание.

    ![Обновление группы ресурсов балансировщика нагрузки](./media/load-balancer-get-started-internet-portal/1-load-balancer.png)

## <a name="create-a-back-end-address-pool"></a>Создание серверного пула адресов

1. После успешного развертывания балансировщика нагрузки выберите его в списке ресурсов. В разделе "Параметры" выберите "Серверные пулы". Введите имя для серверного пула. Нажмите кнопку на hello **добавить** кнопку сторону hello верхней части колонки hello, которая проявится.
2. Щелкните **добавить виртуальную машину** в hello **Добавление внутреннего пула** колонку.  В разделе **Группа доступности** щелкните **Выберите группу доступности**, а затем выберите **myAvailSet**. Затем выберите **выберите виртуальные машины hello** в разделе hello виртуальные машины в разделе колонке hello и щелкнет **web1** и **web2**, hello две виртуальные машины, созданные для балансировки нагрузки. Убедитесь, что оба toohello синий флажки слева, как показано в приведенном ниже рисунке hello. Нажмите кнопку **выберите** в этой колонке следуют ОК в hello **выберите виртуальные машины** колонки и затем **ОК** в hello **Добавление внутреннего пула** колонки.

    ![Добавление пула адресов серверной части toohello- ](./media/load-balancer-get-started-internet-portal/3-load-balancer-backend-02.png)

3. Проверьте toomake убедиться, что уведомления раскрывающийся список содержит обновления для обоих hello виртуальных машин в отношении сохранение внутреннего пула балансировщика hello нагрузки в дополнение tooupdating hello сетевой интерфейс **web1** и **web2**.

## <a name="create-a-probe-lb-rule-and-nat-rules"></a>Создание пробы, правила балансировщика нагрузки и правил NAT

1. Создайте пробу работоспособности.

    В параметрах балансировщика нагрузки выберите "Пробы". Нажмите кнопку **добавить** , расположенный hello верхней части колонки hello.

    Существует два способа tooconfigure зонда: HTTP или TCP. В этот примере показан способ HTTP, но и через TCP настройка выполняется подобным образом.
    Обновление сведений о необходимости hello. Как уже упоминалось, балансировщик **myLoadBalancer** будет выполнять балансировку трафика, проходящего через порт 80. Выбранный путь Hello — HealthProbe.aspx, интервал составляет 15 секунд, а порог состояния неработоспособности — 2. По завершении нажмите кнопку **ОК** toocreate hello пробы.

    Наведите указатель мыши на дополнительные сведения об этих отдельных конфигураций и способов их измененные toocater tooyour требования toolearn значок hello 'i'.

    ![Добавление пробы](./media/load-balancer-get-started-internet-portal/4-load-balancer-probes.png)

2. Создайте правило балансировщика нагрузки.

    Щелкните правил в hello балансировки нагрузки, подсистема балансировки нагрузки «параметры». В hello Новая колонка, щелкните **добавить**. Введите имя для правила. В этом примере используется имя HTTP. Выберите hello интерфейсный порт и внутренний порт. В этом примере для обоих портов выбрано значение 80. Выберите **балансировки Нагрузки серверной** как внутреннего пула и ранее созданные hello **HealthProbe** как hello пробы. Другие конфигурации можно задать в соответствии с требованиями tooyour. Щелкните правило балансировки нагрузки ОК toosave hello.

    ![Добавление правила балансировки нагрузки](./media/load-balancer-get-started-internet-portal/5-load-balancing-rules.png)

3. Создание правила NAT для входящего трафика

    Щелкните правила NAT для входящего трафика в разделе "hello" параметры балансировки нагрузки. В hello Новая колонка, щелкните **добавить**. Введите имя для своего правила NAT для входящего трафика. В этом примере правило названо **inboundNATrule1**. Hello назначения должен быть общедоступный IP-адрес, ранее созданные приветствия. Выберите настраиваемый в рамках службы и хотелось бы toouse протокола hello. В этом примере выбран TCP. Введите порт hello 3441 и hello целевой порт, в этом случае 3389. Нажмите кнопку ОК toosave это правило.

    После создания первого правила hello, повторите этот шаг для hello второе правило входящего трафика NAT вызова inboundNATrule2 из порта 3442 tooTarget порт 3389.

    ![Добавление правила NAT для входящего трафика](./media/load-balancer-get-started-internet-portal/6-load-balancer-inbound-nat-rules.png)

## <a name="remove-a-load-balancer"></a>Удаление балансировщика нагрузки

toodelete балансировки нагрузки, выберите hello подсистемы балансировки нагрузки требуется tooremove. В hello *балансировки нагрузки* колонка, щелкните здесь **удалить** , расположенный hello верхней части колонки hello. При появлении запроса выберите **Да** .

## <a name="next-steps"></a>Дальнейшие действия

[Приступая к настройке внутренней подсистемы балансировки нагрузки](load-balancer-get-started-ilb-arm-cli.md)

[Настройка режима распределения подсистемы балансировки нагрузки](load-balancer-distribution-mode.md)

[Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки](load-balancer-tcp-idle-timeout.md)
