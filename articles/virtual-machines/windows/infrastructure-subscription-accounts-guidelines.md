---
title: "Подписка и учетные записи для виртуальных машин Windows в Azure | Документация Майкрософт"
description: "Изучите основные рекомендации по проектированию и реализации, касающиеся подписок и учетных записей в Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 761fa847-78b0-4078-a33a-d95d198d1029
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8b54e18ed6ecef26a059a6ce742bca03a6434183
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-windows-vms"></a>Рекомендации по подпискам и учетным записям Azure для виртуальных машин Windows

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Эта статья посвящена различным подходам к управлению подписками и учетными записями по мере расширения среды и базы пользователей.

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a>Рекомендации по реализации подписок и учетных записей
Решения

* Какие подписки и учетные записи необходимы для размещения рабочей нагрузки ИТ-среды или ИТ-инфраструктуры?
* Что должна включать в себя иерархия в соответствии с потребностями вашей организации?

Задачи

* Определите логическую иерархию организации с точки зрения управления на уровне подписки.
* В соответствии с этой логической иерархией определите необходимые учетные записи и подписки в каждой из них.
* Создайте набор подписок и учетных записей с использованием соглашения об именовании.

## <a name="subscriptions-and-accounts"></a>Подписки и учетные записи
Для работы с Azure требуется одна или несколько подписок Azure. В них размещаются такие ресурсы, как виртуальные машины или виртуальные сети.

* Как правило, у корпоративных клиентов есть Соглашение о регистрации Enterprise, которое считается ресурсом самого верхнего уровня в иерархии и сопоставлено с одной или несколькими учетными записями.
* Для клиентов без Соглашения о регистрации Enterprise ресурсом верхнего уровня считается учетная запись.
* Подписки сопоставлены с учетными записями. С одной учетной записью может быть связано несколько подписок. Azure хранит данные для выставления счетов на уровне подписки.

Так как количество уровней иерархии для связи между учетной записью и подпиской ограничено двумя, важно, чтобы соглашение об именовании для учетных записей и подписок соответствовало требованиям к выставлению счетов. Например, если в транснациональной компании используется Azure, то можно создать по одной учетной записи на регион и управлять подписками на уровне региона.

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

Например, можно использовать указанную ниже структуру.

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

Если нужно сопоставить несколько подписок для региона с определенной группой, то соглашение об именовании должно предусматривать способ указания дополнительных данных в имени учетной записи или подписки. Такая организация позволяет уплотнять данные для выставления счетов, чтобы можно было создавать уровни иерархии во время отправки отчетов о выставлении счетов.

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

Организация может выглядеть следующим образом.

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

Мы выставляем детализированные счета в виде скачиваемого файла для одной учетной записи или для всех учетных записей, включенных в Соглашение Enterprise.

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

