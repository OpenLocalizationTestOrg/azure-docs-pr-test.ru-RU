---
title: "aaaProtecting сети в центр безопасности Azure | Документы Microsoft"
description: "В этом документе рассматриваются рекомендации из центра безопасности Azure, которые помогают защитить вашу сеть Azure и обеспечить соответствие политикам безопасности."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 96c55a02-afd6-478b-9c1f-039528f3dea0
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: terrylan
ms.openlocfilehash: 053738da432edf13b40172fb44d2044702dd8211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a>Защита сети в центре безопасности Azure.
Центр безопасности Azure анализирует состояние безопасности hello ресурсам Azure. Когда центр обеспечения безопасности выявляет потенциальные уязвимости системы безопасности, он создает рекомендации, которые hello процесс настройки hello необходимые элементы управления.  Рекомендации относятся типы ресурсов tooAzure: виртуальных машин (ВМ), сети, SQL и приложениями.

В этой статье рассматриваются рекомендации, которые применяются tooyour сети.  Основное внимание в рекомендациях для сети уделено брандмауэрам следующего поколения, группам безопасности сети, настройке правил входящего трафика и другим аспектам.  Использовать таблицу hello ниже как toohelp ссылку, вы понимаете рекомендации доступную сеть hello и назначение каждого из них при его применении.

## <a name="available-network-recommendations"></a>Доступные рекомендации для сети
| Рекомендации | Описание |
| --- | --- |
| [Добавить брандмауэр следующего поколения](security-center-add-next-generation-firewall.md) |Рекомендует добавить брандмауэра следующего поколения (NGFW) от партнера Майкрософт tooincrease мер по обеспечению безопасности. |
| [Route traffic through NGFW only (Маршрутизировать трафик только через NGFW)](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |Рекомендует настраивать группы (NSG) правила сетевой безопасности, заставляющие tooyour входящий трафик ВМ с помощью вашей NGFW. |
| [Enable Network Security Groups on subnets or virtual machines (Включить группы безопасности сети для подсетей или виртуальных машин)](security-center-enable-network-security-groups.md) |Рекомендует включить группы безопасности сети для подсетей или виртуальных машин. |
| [Restrict access through Internet facing endpoint (Ограничить доступ через подключенную к Интернету конечную точку)](security-center-restrict-access-through-internet-facing-endpoints.md) |Рекомендует настроить правила входящего трафика для групп безопасности сети. |

## <a name="see-also"></a>См. также
Дополнительные сведения о рекомендации, которые применяются tooother типы ресурсов Azure см. в разделе ниже hello toolearn:

* [Защита виртуальных машин в центре безопасности Azure.](security-center-virtual-machine-recommendations.md)
* [Защита приложений в центре безопасности Azure](security-center-application-recommendations.md)
* [Защита службы SQL Azure в центре безопасности Azure.](security-center-sql-service-recommendations.md)

toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:

* [Установка политики безопасности в центр безопасности Azure](security-center-policies.md) — Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.
* [Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) --Узнайте, как предупреждения toosecurity toomanage и отправки ответа.
* [Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.
