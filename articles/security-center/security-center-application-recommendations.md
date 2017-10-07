---
title: "aaaProtecting свои приложения в центр безопасности Azure | Документы Microsoft"
description: "В этом документе рассматриваются рекомендации в центре безопасности Azure, которые помогают защитить приложения Azure и обеспечить соответствие политикам безопасности."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: b5fc7a9e-24b1-415f-b3b5-62a53f5dd424
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: terrylan
ms.openlocfilehash: da5e02cc2bad55c64e4da14e4e10efd6ddeab39e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-applications-in-azure-security-center"></a>Защита приложений в центре безопасности Azure
Центр безопасности Azure анализирует состояние безопасности hello ресурсам Azure. Когда центр обеспечения безопасности выявляет потенциальные уязвимости системы безопасности, он создает рекомендации, которые hello процесс настройки hello необходимые элементы управления.  Рекомендации относятся типы ресурсов tooAzure: виртуальных машин (ВМ), сети, SQL и приложениями.

В этой статье рассматриваются рекомендации, которые применяются tooapplications.  Они сфокусированы в основном на развертывании брандмауэра приложения.  Использовать таблицу hello ниже как toohelp ссылку, вы понимаете рекомендации в приложения hello и назначение каждого из них при его применении.

## <a name="available-application-recommendations"></a>Доступные рекомендации по приложениям
| Рекомендации | Описание |
| --- | --- |
| [Добавление брандмауэра веб-приложения](security-center-add-web-application-firewall.md) |Рекомендует выполнить развертывание брандмауэра веб-приложения (WAF) для конечных точек веб-службы. Рекомендация развернуть WAF отображается для любого общедоступного IP-адреса (IP-адреса уровня экземпляра или IP-адреса с балансировкой нагрузки), имеющего связанную группу безопасности сети с открытыми входящими веб-портами (80, 443).</br></br>Центр обеспечения безопасности, корпорация Майкрософт рекомендует, что подготовки WAF toohelp защиту от атак на веб-приложений на виртуальных машинах и в среде службы приложений. Среда службы приложений (ASE) — это параметр плана обслуживания [Премиум](https://azure.microsoft.com/pricing/details/app-service/) в службе приложений Azure. Она обеспечивает полностью изолированную и выделенную среду для безопасного выполнения приложений службы приложений Azure. toolearn Дополнительные сведения о ASE, в разделе hello [документация среды службы приложения](../app-service/app-service-app-service-environments-readme.md).</br></br>Вы можете защитить несколько веб-приложений в центре безопасности, добавив эти приложения tooyour существующие WAF развертывания. |
| [Завершение подготовки защиты приложений](security-center-add-web-application-firewall.md#finalize-application-protection) |Конфигурация hello toocomplete WAF трафик должен быть этим toohello WAF устройства. Следуя этой рекомендации завершает hello изменения, необходимые для установки. |

## <a name="see-also"></a>См. также
Дополнительные сведения о рекомендации, которые применяются tooother типы ресурсов Azure см. в разделе ниже hello toolearn:

* [Защита виртуальных машин в центре безопасности Azure.](security-center-virtual-machine-recommendations.md)
* [Защита сети в центре безопасности Azure](security-center-network-recommendations.md)
* [Защита службы SQL Azure в центре безопасности Azure.](security-center-sql-service-recommendations.md)

toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:

* [Установка политики безопасности в центр безопасности Azure](security-center-policies.md) — Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.
* [Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) --Узнайте, как предупреждения toosecurity toomanage и отправки ответа.
* [Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.
