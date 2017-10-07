---
title: "aaaManage DNS-зоны в DNS Azure - портал Azure | Документы Microsoft"
description: "Можно управлять с помощью портала Azure hello зон DNS. В этой статье описывается, как tooupdate, удалите и создайте зон DNS на Azure DNS"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/18/2017
ms.author: gwallace
ms.openlocfilehash: 0d8ce302bb7126dfe8077a6f3e33418e16fcea64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-hello-azure-portal"></a>Как toomanage зоны DNS в hello портал Azure

> [!div class="op_single_selector"]
> * [Портал](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)

В этой статье показано, как toomanage DNS-зоны с помощью портала Azure hello. Также можно управлять с помощью hello кросс платформенных зон DNS [Azure CLI](dns-operations-dnszones-cli.md) или hello Azure [PowerShell](dns-operations-dnszones.md).

## <a name="create-a-dns-zone"></a>Создание зоны DNS

1. Войдите в toohello портал Azure
2. Hello концентратора меню и нажмите кнопку **Создать > Сетевые подключения >** и нажмите кнопку **зоны DNS** tooopen hello создать DNS-зоны колонку.

    ![Зона DNS](./media/dns-operations-dnszones-portal/openzone650.png)

4. На hello **создать DNS-зоны** колонки введите следующие значения hello, затем щелкните **создать**:


   | **Параметр** | **Значение** | **Дополнительные сведения** |
   |---|---|---|
   |**Имя**|contoso.com|Имя зоны DNS hello Hello|
   |**Подписка**|[Ваша подписка]|Выберите зону DNS toocreate hello подписки в.|
   |**Группа ресурсов**|**Создать:** contosoDNSRG|Создайте группу ресурсов. Имя группы ресурсов Hello должно быть уникальным в пределах hello подписки, выбранной. Дополнительные сведения о группах ресурсов, чтение hello toolearn [диспетчера ресурсов](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) обзорную статью.|
   |**Расположение**|Запад США||

> [!NOTE]
> Группа ресурсов Hello относится toohello расположение группы ресурсов hello, а не оказывает влияния на hello зоны DNS. расположение зоны DNS Hello всегда «глобальные» и не отображается.

## <a name="list-dns-zones"></a>Перечисление зон DNS

В hello портал Azure, перейдите в слишком**дополнительные службы** > **сети** > **зон DNS**. Каждая зона DNS является отдельным ресурсом. В этом представлении отображаются такие сведения, как число наборов записей и серверы имен. столбец Hello **СЕРВЕРЫ ИМЕН** не находится в представлении по умолчанию hello tooadd его щелкните **столбцы**выберите **серверов имен** и нажмите кнопку **сделать**.

![Перечисление зон DNS](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a>Удаление зоны DNS

Перейдите tooa зоны DNS в портале hello. На hello **зоны DNS** колонка, щелкните **удалить зону**. Все запрашиваемые tooconfirm Желательное toodelete hello DNS-зоны. Зоны DNS при удалении также удаляются все записи hello, содержащихся в зоне hello.

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как toowork с зоной DNS и записи, посетив [Приступая к работе с Azure DNS, с помощью портала Azure hello](dns-getstarted-portal.md).
