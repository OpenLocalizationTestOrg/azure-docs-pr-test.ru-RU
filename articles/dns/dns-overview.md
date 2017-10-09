---
title: "aaaOverview из Azure DNS | Документы Microsoft"
description: "Обзор служб размещения DNS в Microsoft Azure. Размещение домена в Microsoft Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 68747a0d-b358-4b8e-b5e2-e2570745ec3f
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: gwallace
ms.openlocfilehash: a10f87c488356469e9c04aabde31129049563891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-overview"></a>Обзор Azure DNS

Hello доменных имен или DNS, отвечает за преобразование (или разрешение) веб-сайта или службы имя tooits IP-адрес. Azure DNS является службой размещения для доменов DNS, предоставляющей разрешение имен с помощью инфраструктуры Microsoft Azure. При размещении ваших доменов в Azure, вы можете управлять DNS hello записей с помощью учетных данных, API-интерфейсы, средства и выставление счетов как других служб Azure.

![Общие сведения о DNS](./media/dns-overview/scenario.png)

## <a name="features"></a>Функции

* **Надежность и производительность**: домены DNS в Azure DNS размещаются в глобальной сети DNS-серверов Azure. Мы используем произвольной рассылки к сети, чтобы каждый запрос DNS будет отвечать на ближайший доступный сервер DNS hello. Это обеспечивает высокую производительность и высокий уровень доступности для вашего домена.

* **Полная интеграция** -hello служба Azure DNS может быть toomanage используется DNS-записи для служб Azure, а используемые tooprovide DNS для внешних ресурсов. Azure DNS интегрирован в портал Azure hello и hello использует такие же учетные данные, выставления счетов и контрактом на поддержку как других служб Azure.

* **Безопасность** -hello служба Azure DNS основан на Azure Resource Manager. Таким образом она использует преимущества Resource Manager, такие как управление доступом на основе ролей, журналы аудита и блокировка ресурсов. Ваших доменов и записей можно управлять с помощью hello портал Azure, командлеты Azure PowerShell и hello кросс платформенных Azure CLI. Приложений, которым требуется автоматическое управление DNS можно интегрировать со службой hello через hello REST API и пакеты SDK.

Azure DNS в настоящее время не поддерживает приобретение доменных имен. Если вы хотите toopurchase доменов, необходимо toouse регистратора сторонних доменных имен. как правило, Hello регистратора оплата годовой небольшую плату. Hello доменов может размещаться в Azure DNS для управления DNS-записей. В разделе [делегировать tooAzure домена DNS](dns-domain-delegation.md) подробные сведения.

## <a name="pricing"></a>Цены

DNS выставление счетов основано на hello число зон DNS, размещенных в Azure и hello число запросов DNS. Дополнительные сведения о ценах, посетите toolearn [цены на Azure DNS](https://azure.microsoft.com/pricing/details/dns/).

## <a name="faq"></a>Часто задаваемые вопросы

Часто задаваемые вопросы о Azure DNS. в разделе hello [DNS Azure часто задаваемые вопросы о](dns-faq.md).

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о записях и зонах DNS см. в [обзоре зон и записей DNS](dns-zones-records.md).

Узнайте, каким образом слишком[создать зону DNS](./dns-getstarted-create-dnszone-portal.md) в Azure DNS.

Дополнительные сведения о некоторых hello другой ключ [сетевые возможности](../networking/networking-overview.md) платформы Azure.

