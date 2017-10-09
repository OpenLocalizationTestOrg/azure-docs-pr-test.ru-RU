---
title: "с помощью портала Azure hello Nsg aaaManage | Документы Microsoft"
description: "Узнайте, как toomanage существующей Nsg, с помощью портала Azure hello."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: ad9a4060bd81bae4597ad5a4f59622e10cd214cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-nsgs-using-hello-portal"></a>Управление с помощью портала hello Nsg

> [!div class="op_single_selector"]
> * [Портал](virtual-network-manage-nsg-arm-portal.md)
> * [PowerShell](virtual-network-manage-nsg-arm-ps.md)
> * [интерфейс командной строки Azure](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md). В этой статье описан с помощью модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello классической модели развертывания.
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a>Извлечение информации
Вы можете просмотреть существующие группы безопасности сети, получить правила для существующей группы и узнать, с какими ресурсами она связана.

### <a name="view-existing-nsgs"></a>Просмотр существующих групп безопасности сети

tooview все существующие Nsg в подписке, полный hello, следующие шаги:

1. В браузере перейдите toohttp://portal.azure.com и при необходимости выполните вход с помощью учетной записи Azure.

2. Щелкните **Обзор >** > **Сетевые группы безопасности**.

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. Проверьте список Nsg hello в hello **сетевых групп безопасности** колонку.

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a>Просмотр групп безопасности сети в группе ресурсов

tooview списка Nsg hello в hello **RG NSG** группы ресурсов, полный hello, следующие шаги:

1. Щелкните раздел **Группы ресурсов >** > **RG-NSG** > **...**.

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. В списке ресурсов hello поиска элементов отображается значок NSG hello, как показано в hello **ресурсов** колонке ниже.

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a>Перечисление всех правил для группы безопасности сети

tooview hello правила NSG с именем **NSG-FrontEnd**полный hello следующие действия:

1. Из hello **сетевых групп безопасности** колонке или hello **ресурсов** колонки, показанном выше, нажмите кнопку **NSG-FrontEnd**.

2. В hello **параметры** щелкните **безопасности правила для входящих подключений**.

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. Hello **безопасности правила для входящих подключений** колонке отображается, как показано ниже.

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. В hello **параметры** щелкните **правила безопасности для исходящего трафика** toosee hello правила для исходящих подключений.

    > [!NOTE]
    > tooview правила по умолчанию, нажмите кнопку hello **по умолчанию правила** значок hello верхней части колонки hello, которое отображает hello правила.
    >

### <a name="view-nsgs-associations"></a>Просмотр связей для группы безопасности сети

tooview какие ресурсы hello **NSG-FrontEnd** NSG — связан с, завершенной hello, следующие шаги:

1. Из hello **сетевых групп безопасности** колонке или hello **ресурсов** колонки, показанном выше, нажмите кнопку **NSG-FrontEnd**.

2. В hello **параметры** щелкните **подсети** tooview какие подсети — это связанные toohello NSG.

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. В hello **параметры** щелкните **сетевых интерфейсов** tooview новые сетевые адаптеры — это связанные toohello NSG.

## <a name="manage-rules"></a>Управление правилами
Добавление существующей NSG tooan правила, изменять существующие правила и удалять правила.

### <a name="add-a-rule"></a>Добавление правила
tooadd правила, что позволяет **входящих** tooport трафика **443** с любого компьютера toohello **NSG-FrontEnd** NSG завершения hello, следующие шаги:

1. Из hello **сетевых групп безопасности** колонке или hello **ресурсов** колонки, показанном выше, нажмите кнопку **NSG-FrontEnd**.
2. В hello **параметры** щелкните **безопасности правила для входящих подключений**.
3. В hello **безопасности правила для входящих подключений** колонка, щелкните **добавить**. Затем в hello **добавить правило безопасности для входящего трафика** колонке заполнения hello значения, как показано ниже и нажмите кнопку **ОК**.

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    Через несколько секунд, обратите внимание, hello новое правило в hello **безопасности правила для входящих подключений** колонку.

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a>Изменение правила
правило toochange hello, созданной ранее tooallow входящий трафик от hello **Internet** только, завершенной hello, следующие шаги:

1. Из hello **сетевых групп безопасности** колонке или hello **ресурсов** колонки, показанном выше, нажмите кнопку **NSG-FrontEnd**.
2. В hello **параметры** щелкните правило hello, созданной ранее.
3. В hello **разрешить https** колонки, изменение hello **источника** свойства, как показано ниже, а затем щелкните **Сохранить**.

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a>Удаление правила

toodelete hello правило созданной выше, завершенной hello следующие шаги:

1. Из hello **сетевых групп безопасности** колонке или hello **ресурсов** колонки, показанном выше, нажмите кнопку **NSG-FrontEnd**.
2. В hello **параметры** щелкните правило hello, созданной ранее.
3. В hello **разрешить https** колонке нажмите кнопку **удаление**, а затем нажмите кнопку **Да**.

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a>Управление связями
Можно связать NSG toosubnets и сетевых адаптеров. Можно также отменить связь группы безопасности сети с любым ресурсом.

### <a name="associate-an-nsg-tooa-nic"></a>Связывание NSG tooa сетевого Адаптера
tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** сетевого Адаптера, полный hello, следующие шаги:

1. Из hello **сетевых групп безопасности** колонке или hello **ресурсов** колонки, показанном выше, нажмите кнопку **NSG-FrontEnd**.
2. В hello **параметры** щелкните **сетевых интерфейсов** > **связать** > **TestNICWeb1**.

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a>Отмена связи с сетевым адаптером для группы безопасности сети

toodissociate hello **NSG-FrontEnd** NSG из hello **TestNICWeb1** сетевого Адаптера, полный hello, следующие шаги:

1. Hello портал Azure, щелкните **групп ресурсов >** > **RG NSG** > **...**   >  **TestNICWeb1**.

2. В hello **TestNICWeb1** колонка, щелкните **изменения безопасности...**   >  **Нет**.

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> Можно также использовать этой колонке tooassociate hello Сетевых tooany существующей NSG.
>

### <a name="dissociate-an-nsg-from-a-subnet"></a>Отмена связи с подсетью для группы безопасности сети

toodissociate hello **NSG-FrontEnd** NSG из hello **переднего плана** подсети, полный hello, следующие шаги:

1. Hello портал Azure, щелкните **групп ресурсов >** > **RG NSG** > **...**   >  **TestVNet**.

2. В hello **параметры** колонка, щелкните **подсети** > **переднего плана** > **сетевой группы безопасности**  >  **Нет**.

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. В hello **переднего плана** колонка, щелкните **Сохранить**.

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-tooa-subnet"></a>Связывание NSG tooa подсети

tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** снова подсети, полный hello, следующие шаги:

1. Hello портал Azure, щелкните **групп ресурсов >** > **RG NSG** > **...**   >  **TestVNet**.
2. В hello **параметры** колонка, щелкните **подсети** > **переднего плана** > **сетевой группы безопасности**  >  **NSG-FrontEnd**.
3. В hello **переднего плана** колонка, щелкните **Сохранить**.

> [!NOTE]
> Можно также связать подсети tooa NSG из thh NSG **параметры** колонку.
>

## <a name="delete-an-nsg"></a>Удаление группы NSG
NSG можно удалить только в том случае, если она не сопоставлена tooany ресурсов. toodelete NSG, полный hello, следующие шаги:.

1. Hello портал Azure, щелкните **групп ресурсов >** > **RG NSG** > **...**   >  **NSG-FrontEnd**.
2. В hello **параметры** колонка, щелкните **сетевых интерфейсов**.
3. Если все сетевые адаптеры в списке, щелкните сетевой Адаптер hello и выполнить шаг 2 [связь между Сетевыми NSG](#Dissociate-an-NSG-from-a-NIC).
4. Повторите шаг 3 для каждого сетевого адаптера.
5. В hello **параметры** колонка, щелкните **подсети**.
6. Если в списке подсетей, выберите подсеть hello и выполните шаги 2 и 3 в [связь NSG из подсети](#Dissociate-an-NSG-from-a-subnet).
7. Прокрутка влево toohello **NSG-FrontEnd** колонке нажмите кнопку **удаление** > **Да**.

    ![Портал Azure — группы безопасности сети](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a>Дальнейшие действия
* [Включите ведение журнала](virtual-network-nsg-manage-log.md) для групп безопасности сети.
