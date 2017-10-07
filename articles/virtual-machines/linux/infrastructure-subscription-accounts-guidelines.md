---
title: "aaaSubscription и учетной записи для виртуальных машин Linux в Azure | Документы Microsoft"
description: "Дополнительные сведения о hello ключевые проектирования и реализации рекомендации для подписок и учетных записей в Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19343826-7eef-42a1-98be-4ec65b0f377a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9025a40783c008310ebd0f674deb4a9001ae974a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-linux-vms"></a>Рекомендации по подпискам и учетным записям Azure для виртуальных машин Linux

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Это статье рассматриваются основные сведения о том, как растет tooapproach подписки и управление учетными записями в вашей среде и пользовательской базы.

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a>Рекомендации по реализации подписок и учетных записей
Решения

* Какой набор подписок и учетных записей необходимо toohost рабочей нагрузки ИТ или инфраструктуры?
* Как toobreak работу toofit иерархии hello вашей организации?

Задачи

* Определение иерархии логическую организацию как toomanage его из уровня подписки.
* toomatch этой логической иерархии определения hello требуются учетные записи и подписки в каждой учетной записи.
* Создайте набор hello подписками и учетными записями с помощью имен.

## <a name="subscriptions-and-accounts"></a>Подписки и учетные записи
toowork с Azure требуется один или несколько подписок Azure. В них размещаются такие ресурсы, как виртуальные машины или виртуальные сети.

* Корпоративные клиенты обычно имеют регистрации на предприятии, который hello ресурсов верхнего уровня в иерархии hello и связанные tooone или несколько учетных записей.
* Для клиентов без регистрации на предприятии потребителей ресурсов hello верхнего уровня — учетная запись hello.
* Подписки, связанные tooaccounts и может быть один или несколько подписок на учетную запись. Выставление счетов сведения на уровне подписки hello Azure записей.

Из-за предел toohello две иерархии уровней на связь hello учетной записи и подписки это важно tooalign hello именования toohello учетными записями и подписками, выставление счетов потребностей. Для экземпляра глобальной компании использует Azure, они могут выбрать учетную запись toohave один по регионам, и иметь подписок, управляемых в hello уровень регион:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

Например можно использовать hello следующие структуры:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

Если область решает toohave больше, чем одной подписке связанного tooa определенной группы, соглашение об именовании hello должно учитываться tooencode способом hello дополнительные данные в учетной записи hello или имя подписки hello. Такая организация позволяет уплотнения выставления счетов данных toogenerate hello новых уровней иерархии во время выставления счетов отчетов:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

Hello организации может выглядеть как следующий пример hello.

![](media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

Мы выставляем детализированные счета в виде скачиваемого файла для одной учетной записи или для всех учетных записей, включенных в Соглашение Enterprise.

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

