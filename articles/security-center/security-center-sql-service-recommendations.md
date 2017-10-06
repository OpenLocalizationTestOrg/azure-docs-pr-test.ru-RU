---
title: "aaaProtecting Azure SQL службы и данных в центр безопасности Azure | Документы Microsoft"
description: "В этом документе рассматриваются рекомендации из центра безопасности Azure, которые помогают защитить ваши данные и службу SQL Azure, а также обеспечить соответствие политикам безопасности."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: bcae6987-05d0-4208-bca8-6a6ce7c9a1e3
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/03/2017
ms.author: terrylan
ms.openlocfilehash: 75d782d3c2418f9645139e4cd6ecb7765c488f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a>Защита службы SQL Azure и данных в центре безопасности Azure
Центр безопасности Azure анализирует состояние безопасности hello ресурсам Azure. Когда центр обеспечения безопасности выявляет потенциальные уязвимости системы безопасности, он создает рекомендации, которые hello процесс настройки hello необходимые элементы управления.  Рекомендации относятся типы ресурсов tooAzure: виртуальных машин (ВМ), сети, SQL и данных и приложений.

В этой статье рассматриваются рекомендации, которые применяются tooAzure службы SQL и данных. а также рекомендации включения аудита для серверов и баз данных SQL Azure, включения шифрования для баз данных SQL и включения шифрования учетной записи хранения Azure.  Использовать таблицу hello ниже как toohelp ссылку, вы понимаете hello доступных служб и данных рекомендации по SQL и назначение каждого из них при его применении.

## <a name="available-sql-service-and-data-recommendations"></a>Доступные рекомендации для службы SQL и данных
| Рекомендации | Описание |
| --- | --- |
| [Включение аудита и обнаружения угроз на серверах SQL Server](security-center-enable-auditing-on-sql-servers.md) |Рекомендует включить аудит и обнаружение угроз для серверов SQL Azure (только для службы SQL Azure, не включая экземпляры SQL, работающие на виртуальных машинах). |
| [Включение аудита и обнаружения угроз для баз данных SQL](security-center-enable-auditing-on-sql-databases.md) |Рекомендует включить аудит и обнаружение угроз для баз данных SQL в Azure (только для службы SQL Azure, не включая экземпляры SQL, работающие на виртуальных машинах). |
| [Включение прозрачного шифрования данных в базах данных SQL](security-center-enable-transparent-data-encryption.md) |Рекомендует включить шифрование для баз данных SQL (только для службы SQL Azure). |

## <a name="see-also"></a>См. также
Дополнительные сведения о рекомендации, которые применяются tooother типы ресурсов Azure см. в разделе ниже hello toolearn:

* [Защита виртуальных машин в центре безопасности Azure.](security-center-virtual-machine-recommendations.md)
* [Защита приложений в центре безопасности Azure](security-center-application-recommendations.md)
* [Защита сети в центре безопасности Azure.](security-center-network-recommendations.md)

toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:

* [Установка политики безопасности в центр безопасности Azure](security-center-policies.md) — Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.
* [Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) --Узнайте, как предупреждения toosecurity toomanage и отправки ответа.
* [Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.
