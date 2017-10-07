---
title: "часто задаваемые вопросы о DNS aaaAzure | Документы Microsoft"
description: "Часто задаваемые вопросы об Azure DNS."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: jonatul
ms.openlocfilehash: 55006e9d8b311f1e94678eb9d35ce3448b936488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-faq"></a>Вопросы и ответы об Azure DNS

## <a name="about-azure-dns"></a>Сведения об Azure DNS

### <a name="what-is-azure-dns"></a>Что такое Azure DNS?

Hello доменных имен или DNS, отвечает за преобразование (или разрешение) веб-сайта или службы имя tooits IP-адрес. Azure DNS является службой размещения для доменов DNS, предоставляющей разрешение имен с помощью инфраструктуры Microsoft Azure. При размещении ваших доменов в Azure, вы можете управлять DNS hello записей с помощью учетных данных, API-интерфейсы, средства и выставление счетов как других служб Azure.

Домены DNS в Azure DNS размещаются в глобальной сети DNS-серверов Azure. Мы используем произвольной рассылки к сети, чтобы каждый запрос DNS будет отвечать на ближайший доступный сервер DNS hello. Это обеспечивает высокую производительность и высокий уровень доступности для вашего домена.

Hello служба Azure DNS основан на Azure Resource Manager. Таким образом она использует преимущества Resource Manager, такие как управление доступом на основе ролей, журналы аудита и блокировка ресурсов. Ваших доменов и записей можно управлять с помощью hello портал Azure, командлеты Azure PowerShell и hello кросс платформенных Azure CLI. Приложений, которым требуется автоматическое управление DNS можно интегрировать со службой hello через hello REST API и пакеты SDK.

### <a name="how-much-does-azure-dns-cost"></a>Сколько стоит использование Azure DNS?

модель выставления счетов Hello Azure DNS основан на hello число зон DNS, размещенных в Azure DNS и hello количество запросов DNS, который они получают. На основе использования предоставляются скидки.

Дополнительные сведения см. в разделе hello [DNS Azure странице цен](https://azure.microsoft.com/pricing/details/dns/).

### <a name="what-is-hello-sla-for-azure-dns"></a>Что такое hello SLA для Azure DNS?

Мы гарантируем, что допустимый DNS-запросы получите ответ из по крайней мере один сервер Azure DNS по крайней мере 99,99% времени hello.

Дополнительные сведения см. в разделе hello [страницы соглашения об уровне ОБСЛУЖИВАНИЯ Azure DNS](https://azure.microsoft.com/support/legal/sla/dns).

### <a name="what-is-a-dns-zone-is-it-hello-same-as-a-dns-domain"></a>Что такое "зона DNS"? Такое hello же, как домен DNS 

Домен имеет уникальное имя в hello доменных имен, например «contoso.com».

Зоны DNS-записей DNS используется toohost hello для определенного домена. Например hello доменом «contoso.com» может содержать несколько записей DNS, такие как «mail.contoso.com» (для почтового сервера) и «www.contoso.com» (для веб-сайта). Это будет размещена в зоне DNS hello «contoso.com».

Доменное имя — *просто имя*, тогда как зоны DNS представляет собой ресурс данных, содержащий hello записи DNS для имени домена. Azure DNS позволяет toohost зоны DNS и управлять hello записей DNS для домена в Azure. Он также предоставляет DNS-серверами tooanswer DNS-запросы из Интернета hello.

### <a name="do-i-need-toopurchase-a-dns-domain-name-toouse-azure-dns"></a>Требуется toopurchase toouse имя домена DNS Azure DNS? 

Не обязательно.

Не обязательно toopurchase домена toohost зоны DNS в Azure DNS. Можно создать зону DNS в любое время без владельца hello доменное имя. Запросы DNS для данной зоны разрешается только если они будут направляться toohello Azure DNS-серверами, назначенных toohello зоны.

Требуется имя домена toopurchase hello, если требуется toolink вашей зоны DNS в hello глобального иерархию DNS — это позволяет DNS-запросы из в любом месте в hello world toofind вашей зоны DNS и ответ с DNS-записей.

## <a name="azure-dns-features"></a>Возможности Azure DNS

### <a name="does-azure-dns-support-dns-based-traffic-routing-or-endpoint-failover"></a>Azure DNS поддерживает маршрутизацию трафика на основе DNS и отработку отказа конечных точек?

Маршрутизацию трафика на основе DNS и отработку отказа конечных точек обеспечивает диспетчер трафика Azure. Это отдельная служба Azure, которая может использоваться вместе с Azure DNS. Дополнительные сведения см. в разделе hello [Обзор диспетчера трафика](../traffic-manager/traffic-manager-overview.md).

Azure DNS поддерживает только размещение «static» доменов DNS, в которой каждый запрос DNS для определенной записи DNS всегда получает hello же ответ DNS.

### <a name="does-azure-dns-support-domain-name-registration"></a>Поддерживает ли Azure DNS регистрацию доменных имен?

№ Azure DNS в настоящее время не поддерживает приобретение доменных имен. Если вы хотите toopurchase доменов, необходимо toouse регистратора сторонних доменных имен. как правило, Hello регистратора оплата годовой небольшую плату. Hello доменов может размещаться в Azure DNS для управления DNS-записей. В разделе [делегировать tooAzure домена DNS](dns-domain-delegation.md) подробные сведения.

Это функция, которую мы отслеживаем в очереди невыполненной работы. Можно использовать наш веб-сайт отзывов слишком[регистрации вашего поддержка этой функции](https://feedback.azure.com/forums/217313-networking/suggestions/4996615-azure-should-be-its-own-domain-registrar).

### <a name="does-azure-dns-support-private-domains"></a>Поддерживает ли Azure DNS "частные" домены?

Нет. В настоящее время Azure DNS поддерживает только домены для Интернета.

Это функция, которую мы отслеживаем в очереди невыполненной работы. Можно использовать наш веб-сайт отзывов слишком[регистрации вашего поддержка этой функции](https://feedback.azure.com/forums/217313-networking/suggestions/10737696-enable-split-dns-for-providing-both-public-and-int).

Сведения о внутренних параметрах DNS в Azure см. в разделе [Разрешение имен для ВМ и экземпляров ролей](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

### <a name="does-azure-dns-support-dnssec"></a>Поддерживает ли Azure DNS набор DNSSEC?

Нет. Сейчас Azure DNS не поддерживает DNSSEC.

Это функция, которую мы отслеживаем в очереди невыполненной работы. Можно использовать наш веб-сайт отзывов слишком[регистрации вашего поддержка этой функции](https://feedback.azure.com/forums/217313-networking/suggestions/13284393-azure-dns-needs-dnssec-support).

### <a name="does-azure-dns-support-zone-transfers-axfrixfr"></a>Поддерживает ли Azure DNS передачу зон (AXFR-IXFR)?

№ Сейчас Azure DNS не поддерживает передачу зон. Зоны DNS-сервера может быть [импортируются в Azure DNS, с помощью Azure CLI hello](dns-import-export.md). DNS-записи можно управлять через hello [портала управления Azure DNS](dns-operations-recordsets-portal.md)наш [API-интерфейса REST](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [командлеты PowerShell](dns-operations-recordsets.md), или [ Средство CLI](dns-operations-recordsets-cli.md).

Это функция, которую мы отслеживаем в очереди невыполненной работы. Можно использовать наш веб-сайт отзывов слишком[регистрации вашего поддержка этой функции](https://feedback.azure.com/forums/217313-networking/suggestions/12925503-extend-azure-dns-to-support-zone-transfers-so-it-c).

### <a name="does-azure-dns-support-url-redirects"></a>Поддерживает ли Azure DNS перенаправление URL-адресов?

Нет. URL-адрес перенаправления службы не фактически служба DNS — они работают на уровне HTTP hello, а не hello уровне DNS. Некоторые toobundle поставщики DNS URL-адрес перенаправления службу как часть их общей предложения. На данный момент эта функция не поддерживается Azure DNS.

Она отслеживается в очереди невыполненной работы. Можно использовать наш веб-сайт отзывов слишком[регистрации вашего поддержка этой функции](https://feedback.azure.com/forums/217313-networking/suggestions/10109736-provide-a-301-permanent-redirect-service-for-ape).

## <a name="using-azure-dns"></a>Использование Azure DNS

### <a name="can-i-co-host-a-domain-using-azure-dns-and-another-dns-provider"></a>Можно ли реализовать совместное размещение домена с помощью Azure DNS и другого поставщика DNS?

Да. Azure DNS поддерживает совместное размещение доменов с другими службами DNS.

toodo таким образом, для домена hello (какой элемент управления поставщиков, получающих DNS запрашивает hello домена) необходимо записей hello NS toomodify серверы имен toohello toopoint обоих поставщиков. Эти записи NS требуется toobe изменения в 3 местах: в Azure DNS в hello другого поставщика и в родительской зоне hello (обычно настроены с помощью регистратора доменных имен hello). Дополнительные сведения о делегировании DNS см. в разделе [Делегирование зон DNS с помощью Azure DNS](dns-domain-delegation.md).

Кроме того необходимо tooensure, что hello записи DNS для домена hello синхронизированы между оба поставщика DNS. Сейчас Azure DNS не поддерживает передачу зон DNS. Требуется toosynchronize DNS-записи, используя либо hello [портала управления Azure DNS](dns-operations-recordsets-portal.md)наш [API-интерфейса REST](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [командлеты PowerShell](dns-operations-recordsets.md) , или [CLI средство](dns-operations-recordsets-cli.md).

### <a name="do-i-have-toodelegate-my-domain-tooall-4-azure-dns-name-servers"></a>Нужно ли toodelegate Azure DNS-имя домена tooall 4 серверы?

Да. Azure DNS назначает 4 серверы имен tooeach зоны DNS, изоляцию от сбоев и повышения устойчивости. Здравствуйте, tooqualify для соглашения об уровне ОБСЛУЖИВАНИЯ Azure DNS, необходимо toodelegate tooall 4 вашего DNS-серверов.

### <a name="what-are-hello-usage-limits-for-azure-dns"></a>Каковы ограничения на использование hello для Azure DNS?

При использовании Azure DNS применяются следующие ограничения по умолчанию Hello.

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

### <a name="can-i-move-an-azure-dns-zone-between-resource-groups-or-between-subscriptions"></a>Можно ли перемещать зону Azure DNS между группами ресурсов или подписками?

Да. Зоны Azure DNS можно перемещать между группами ресурсов или подписками.

Это не влияет на запросы DNS. серверы имен Hello, назначенный toohello зоны остаются совпадают и DNS-запросы обрабатываются в обычном режиме на протяжении приветствия.

Дополнительные сведения и инструкции о том, как toomove зоны DNS, в разделе [переместить ресурсы tooa группы ресурсов или подписку](../azure-resource-manager/resource-group-move-resources.md).

### <a name="how-long-does-it-take-for-dns-changes-tootake-effect"></a>Сколько времени требуется для эффекта tootake изменения DNS?

Новый зон DNS и DNS-записи обычно отражаются на hello Azure DNS-серверами быстро, через несколько секунд.

Изменения tooexisting DNS-записи может занять больше времени, но по-прежнему должно быть отражено на hello Azure DNS-серверами в течение 60 секунд. В этом случае DNS-кэширование за пределами Azure DNS (по DNS-клиенты и рекурсивные распознаватели DNS) также может повлиять hello время, затраченное на изменение DNS toobe эффективным. Длительность этого кэша можно контролировать использование свойства hello срока жизни (TTL) для каждого набора записей.

### <a name="how-can-i-protect-my-dns-zones-against-accidental-deletion"></a>Как защитить мои зоны DNS от ненамеренного удаления?

Azure DNS управляется с помощью диспетчера ресурсов Azure, и преимущества hello доступа к функциям управления этого диспетчера ресурсов Azure предоставляет. Управление доступом на основе ролей можно использовать toocontrol, какие пользователи имеют чтения или записи зоны tooDNS и наборы записей. Блокировки ресурсов может быть применен tooprevent случайное изменение или удаление зон DNS и наборы записей.

Дополнительные сведения см. в разделе [Как защитить зоны и записи DNS](dns-protect-zones-recordsets.md).

### <a name="how-do-i-set-up-spf-records-in-azure-dns"></a>Как настроить записи SPF в Azure DNS?

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="how-do-i-set-up-an-international-domain-name-idn-in-azure-dns"></a>Как настроить международное доменное имя (IDN) в Azure DNS?

Международные доменные имена (IDN) создаются путем кодирования DNS-имен в формат [Punycode](https://en.wikipedia.org/wiki/Punycode). Запросы DNS выполняются с использованием этих имен в формате Punycode.

Можно настроить международные доменные имена (IDN) в Azure DNS, первое преобразование имя зоны hello или имя toopunycode набор записей. Azure DNS в настоящее время не поддерживает встроенное преобразование в Punycode.

## <a name="next-steps"></a>Дальнейшие действия

[Дополнительные сведения об Azure DNS](dns-overview.md)
<br>
[Дополнительные сведения о зонах и записях DNS](dns-zones-records.md)
<br>
[Приступая к работе с Azure DNS](dns-getstarted-portal.md)

