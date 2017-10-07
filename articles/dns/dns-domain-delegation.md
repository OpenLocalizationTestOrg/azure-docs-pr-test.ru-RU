---
title: "Общие сведения о делегировании DNS aaaAzure | Документы Microsoft"
description: "Понять, как toochange делегирования домена и Azure DNS используйте имя размещение домена tooprovide серверов."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: eaf2d2e345004b4d631e8d81d548b8ca23277d05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="delegation-of-dns-zones-with-azure-dns"></a>Делегирование зон DNS с помощью Azure DNS

Azure DNS позволяет toohost зоны DNS и управлять hello записей DNS для домена в Azure. Чтобы запросы DNS для домена tooreach Azure DNS, hello домен имеет toobe делегировать tooAzure DNS из родительского домена hello. Имейте в виду Azure DNS не hello регистратора домена. В этой статье объясняется, как работает делегирование домен и как tooAzure toodelegate доменов DNS.

## <a name="how-dns-delegation-works"></a>Принципы делегирования DNS

### <a name="domains-and-zones"></a>Домены и зоны

Hello доменных имен — это иерархия доменов. Иерархия Hello начинается из домена «root» hello, чье имя является просто "**.**".  Ниже находятся домены верхнего уровня, такие как com, net, org, uk и jp.  Под этими доменами верхнего уровня расположены домены второго уровня, например org.uk и co.jp.  И т. д. домены Hello в hello иерархии DNS размещаются с помощью отдельные зоны DNS. Глобально распределены этих зон, размещенных на DNS-серверах имя вокруг Здравствуй, мир!.

**Зона DNS** -домен имеет уникальное имя в системе доменных имен, например «contoso.com» hello. Зоны DNS-записей DNS используется toohost hello для определенного домена. Например домен hello «contoso.com» может содержать несколько записей DNS, такие как «mail.contoso.com» (для почтового сервера) и «www.contoso.com» (для веб-сайта).

**Регистратор доменных имен.** Регистратор доменных имен — это организация, которая может предоставлять доменные имена в Интернете. Они проверяют домен Интернета hello toouse доступны и позволяют toopurchase его. После регистрации имени домена hello вы являетесь владельцем юридических hello hello доменного имени. Если уже имеется домен Интернета, можно использовать hello текущего домена регистратора toodelegate tooAzure DNS.

toofind более подробные сведения, кто является владельцем заданного доменного имени, или сведения о том, как toobuy домена, в разделе [управление доменом Интернета в Azure AD](https://msdn.microsoft.com/library/azure/hh969248.aspx).

### <a name="resolution-and-delegation"></a>Разрешение и делегирование

Существует два следующих типа DNS-серверов.

* *Полномочный* DNS-сервер содержит зоны DNS. Он отвечает на запросы DNS для записей только в этих зонах.
* *Рекурсивный* DNS-сервер не содержит зоны DNS. Он ответы на все запросы DNS, вызвав заслуживающий доверия DNS серверов toogather hello данные.

Служба DNS Azure дает возможность пользоваться полномочной службой DNS,  а не рекурсивной. Облачные службы и виртуальные машины в Azure, автоматически настроенного toouse, реализуемая отдельно в рамках инфраструктуры Azure служба рекурсивный DNS. Сведения о toochange эти параметры DNS. в статье [разрешение имен в Azure](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

DNS-клиенты в ПК или мобильных устройств обычно вызывают рекурсивный DNS server tooperform любые запросы DNS, необходимые клиентским приложениям hello.

Когда рекурсивный DNS-сервер получает запрос на запись DNS, например, «www.contoso.com», сначала должен toofind hello имя сервера размещения hello зоны для домена «contoso.com» hello. сервер имен toofind hello, он начинается hello корневых серверов имен и из него находит серверы имен hello размещение зоны «com» hello. Затем выполняется запрос hello «com» имя toofind hello имя серверов размещения зоны «contoso.com» hello.  Наконец, это может tooquery эти серверы доменных имен для «www.contoso.com».

Эта процедура вызывается разрешение DNS-имени hello. Строго говоря разрешение DNS включает дополнительные действия, например следующих записей CNAME, но не является важным toounderstanding, как работает делегирование DNS.

Как в родительскую зону «пункт» серверы имен toohello для дочерней зоны? Для этого используются записи DNS специального типа, называемые записями NS (NS значит "сервер имен"). Например hello корневая зона содержит записи NS для «com» и hello серверы имен для зоны «com» hello. В свою очередь зона «com» hello содержит записи NS для contoso.com, показывающий hello серверы доменных имен для зоны «contoso.com» hello. Настройка hello записи NS для дочерней зоны в родительской зоне, называется делегирование домена hello.

Следующие изображения Hello показывает пример запроса DNS. Hello contoso.net и partners.contoso.net являются зоны Azure DNS.

![Сервер имен DNS](./media/dns-domain-delegation/image1.png)

1. Здравствуйте, клиентские запросы `www.partners.contoso.net` из их локального DNS-сервера.
1. Hello локальный DNS-сервер не имеет записи hello, поэтому запрос tootheir корневого имени сервера.
1. имя корня Hello не имеет записи hello, но известен адрес hello hello `.net` имя сервера, он предоставляет этот адрес toohello DNS-сервер
1. Hello DNS отправляет запрос toohello hello `.net` имя сервера, он не имеет hello записи не известен адрес hello hello contoso.net имя сервера. В данном случае это зона DNS, размещенная в Azure DNS.
1. зоны Hello `contoso.net` не имеет записи hello, но знает hello имя сервера для `partners.contoso.net` и который отвечает. В данном случае это зона DNS, размещенная в Azure DNS.
1. Hello DNS-сервер запрашивает hello IP-адрес `partners.contoso.net` из hello `partners.contoso.net` зоны. Он содержит запись hello и высылает hello IP-адрес.
1. Hello DNS-сервер предоставляет hello IP адрес toohello клиента
1. Клиент Hello подключается toohello веб-сайт `www.partners.contoso.net`.

Каждый делегирования есть две копии записей NS hello; один в родительской зоне hello указывает дочерние toohello, а другой в дочерней зоне hello сам. Зона «contoso.net» Hello содержит записи hello NS для «contoso.net» (в дополнение toohello записей «net»). Эти записи называются заслуживающих доверия NS и они располагаются на вершине hello hello дочерней зоны.

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, каким образом слишком[делегировать tooAzure вашего домена DNS](dns-delegate-domain-azure-dns.md)

