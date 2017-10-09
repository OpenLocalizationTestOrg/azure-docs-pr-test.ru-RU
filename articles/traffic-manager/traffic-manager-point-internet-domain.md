---
title: "aaaPoint корпоративного домена tooa диспетчера трафика доменном имени Интернета | Документы Microsoft"
description: "Эта статья поможет точки домена имя tooa диспетчера трафика доменного имени вашей компании."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 29822946-2d45-4434-ba47-fc180a445cc3
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: kumud
ms.openlocfilehash: 84c428f60a1dc70452bf957d98a68c95e0b51715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="point-a-company-internet-domain-tooan-azure-traffic-manager-domain"></a>Направление домена диспетчера трафика Azure tooan домена Интернета компании

Когда вы создаете профиль диспетчера трафика, Azure автоматически присваивает этому профилю имя DNS. toouse имя из вашего зоны DNS создать запись CNAME DNS, которая сопоставляет toohello доменное имя вашего профиля диспетчера трафика. Имя домена диспетчера трафика hello можно найти в hello **Общие** раздел на странице конфигурации hello hello профиля диспетчера трафика.

Например www.contoso.com toohello имя toopoint contoso.trafficmanager.net имя DNS диспетчера трафика, вы создадите hello следующая запись ресурса DNS:

    www.contoso.com IN CNAME contoso.trafficmanager.net

Весь трафик запросов слишком*www.contoso.com* получить направленный слишком*contoso.trafficmanager.net*.

> [!IMPORTANT]
> Не может указывать домена второго уровня, таких как *contoso.com*, toohello домен диспетчера трафика. Стандарты протокола DNS не позволяют использовать записи CNAME для имен домена второго уровня.

## <a name="next-steps"></a>Дальнейшие действия

* [Методы маршрутизации диспетчера трафика](traffic-manager-routing-methods.md)
* [Диспетчер трафика — включение, отключение или удаление профиля диспетчера трафика](disable-enable-or-delete-a-profile.md)
* [Диспетчер трафика — отключение и включение конечной точки диспетчера трафика](disable-or-enable-an-endpoint.md)
