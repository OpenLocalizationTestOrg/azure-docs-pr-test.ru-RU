---
title: "руководство по устранению неполадок DNS aaaAzure | Документы Microsoft"
description: "Как tootroubleshoot распространенные проблемы с Azure DNS"
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: 95b01dc3-ee69-4575-a259-4227131e4f9c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/20/2017
ms.author: jonatul
ms.openlocfilehash: 944aa1811c980063f739268cd2c79b647b2754a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-troubleshooting-guide"></a>Руководство по устранению неполадок службы DNS Azure

На этой странице представлены сведения об устранении распространенных неполадок службы DNS Azure.

Если с помощью описанных выше шагов не удалось решить проблему, то воспользуйтесь поиском или сообщите о свой проблеме на нашем [форуме поддержки сообщества на сайте MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork). Вы также можете отправить запрос в службу поддержки Azure.


## <a name="i-cant-create-a-dns-zone"></a>Не удается создать зону DNS

tooresolve распространенные проблемы, выполните одно или несколько действий hello.

1.  Просмотр приветствия аудита Azure DNS заносит в журнал toodetermine причина сбоя hello.
2.  Каждое имя зоны DNS должно быть уникальным в пределах соответствующей группы ресурсов. То есть два DNS-зоны с hello таким же именем, не могут совместно использовать группу ресурсов. Попробуйте использовать другое имя зоны или другую группу ресурсов.
3.  Может появиться ошибка «Достигнуто или превышено максимальное число зон в подписке {subscription id} hello.» Используйте другую подписку Azure, удалите некоторые зоны или обратитесь в службу поддержки Azure tooraise лимита подписки.
4.  Появится сообщение об ошибке «hello зоны «{зоны name}» не доступен.» Эта ошибка означает, что Azure DNS не удается tooallocate серверы имен для этой зоны DNS. Попробуйте использовать другое имя зоны. Кроме того Если вы являетесь владельцем имя домена hello, обратитесь в службу поддержки Azure, который можно выделить серверы имен автоматически.


### <a name="recommended-documents"></a>**Рекомендуемые документы**

[DNS zones and records](dns-zones-records.md)
 (Зоны и записи DNS)<br>
[Создание зоны DNS на портале Azure](dns-getstarted-create-dnszone-portal.md)

## <a name="i-cant-create-a-dns-record"></a>Не удается создать запись DNS

tooresolve распространенные проблемы, выполните одно или несколько действий hello.

1.  Просмотр приветствия аудита Azure DNS заносит в журнал toodetermine причина сбоя hello.
2.  Набор записей hello существует ли?  Azure DNS управляет записей с помощью записи *задает*, которые являются hello коллекцию записей hello совпадают имя и hello таким же типа. Если запись с hello совпадают имя и тип уже существует, tooadd другой такой записи, рекомендуется изменить существующую запись hello задайте.
3.  Вы пытаетесь toocreate запись на вершине зоны DNS hello (hello 'root' hello зоны)? Если таким образом, hello DNS соглашение toouse hello ' @' символ имени записи hello. Также Обратите внимание, что стандартах DNS hello не разрешать записи CNAME в зоне вершина hello.
4.  Возник конфликт CNAME?  Hello стандартах DNS не разрешать запись CNAME с hello одинаковые имена, как запись с любого другого типа. При наличии существующего CNAME, создается запись с hello завершается с ошибкой, именем другого типа.  Аналогичным образом Создание CNAME завершается сбоем, если имя hello соответствует существующей записи другого типа. Удалите hello конфликт, удалив hello, другие записи или выбрать другую запись имя.
5.  Достигнуто максимально hello hello количество наборы записей, которые могут использоваться в зоне DNS? Привет текущее число наборов записей и hello максимальное число наборов записей отображаются в hello портал Azure, в разделе hello «свойства» hello зоны. Если этот предел достигнут, затем либо удалить некоторые наборы записей или обратитесь в службу поддержки Azure tooraise лимита набора записей для данной зоны, и повторите попытку. 


### <a name="recommended-documents"></a>**Рекомендуемые документы**

[DNS zones and records](dns-zones-records.md)
 (Зоны и записи DNS)<br>
[Создание зоны DNS на портале Azure](dns-getstarted-create-dnszone-portal.md)



## <a name="i-cant-resolve-my-dns-record"></a>Не удается разрешить новую запись DNS

Разрешение DNS-имен — это многоэтапный процесс, который может завершиться ошибкой по многим причинам. Hello следующие действия помогут изучить, почему происходит сбой разрешения DNS для записи DNS в зоне, размещенной в Azure DNS.

1.  Убедитесь, что записи DNS hello настроены правильно в Azure DNS. Просмотрите записи DNS hello в hello портал Azure, проверьте правильность имени зоны hello, именем записи и тип записи.
2.  Убедитесь, правильно разрешать DNS-записи hello на hello Azure DNS-серверами.
    - Если DNS-запросы с локального компьютера, может появиться кэшированные результаты, которые не отражают текущее состояние серверов имен hello hello.  Кроме того, корпоративной сети часто используют прокси-серверов DNS, который препятствует DNS-запросы направляются toospecific серверы имен.  tooavoid этих проблем, использовать службу разрешения имен, веб сервера, такие как [digwebinterface](http://digwebinterface.com).
    - Быть убедиться, что toospecify hello правильное имя серверов для зоны DNS, как показано в hello портал Azure.
    - Убедитесь, что hello DNS-имя указано правильно (имеется toospecify hello полное доменное имя, включая имя зоны hello) и правильный тип записи hello
3.  Подтвердите hello DNS-имени домена был правильно [делегированы toohello Azure DNS-серверами](dns-domain-delegation.md). [Существует множество сторонних веб-сайтов для проверки делегирования DNS](https://www.bing.com/search?q=dns+check+tool). Этот тест *зоны* проверку делегирования, поэтому следует ввести только имя зоны DNS hello и не hello полное имя записи.
4.  Прохождения hello выше записи DNS должны теперь правильно обработать. tooverify, можно повторно использовать [digwebinterface](http://digwebinterface.com), на этот раз hello параметрами по умолчанию имя сервера.


### <a name="recommended-documents"></a>**Рекомендуемые документы**

[Делегат tooAzure домена DNS](dns-domain-delegation.md)



## <a name="how-do-i-specify-hello-service-and-protocol-for-an-srv-record"></a>Как указать hello «службы» и «протокол» для записи SRV?

Azure DNS управляет записями DNS в качестве наборов записей — hello коллекцию записей с hello совпадают имя и hello же типа. Набор записей типа SRV hello «службы» и «протокол» должны toobe, заданный как часть hello имя набора записей. Hello SRV указаны другие параметры («приоритет», «weight», «порт» и «целевой объект») отдельно для каждой записи в наборе записей hello.

Примеры имен записей SRV (имя службы — SIP, протокол — TCP):

- \_SIP. \_tcp (создает набор в вершине зоны hello записей)
- \_sip.\_tcp.sipservice (создает набор записей с именем sipservice).

### <a name="recommended-documents"></a>**Рекомендуемые документы**

[DNS zones and records](dns-zones-records.md)
 (Зоны и записи DNS)<br>
[Создание наборов записей DNS и записей с помощью hello портал Azure](dns-getstarted-create-recordset-portal.md)
<br>
[SRV-запись (Википедия)](https://en.wikipedia.org/wiki/SRV_record)


## <a name="next-steps"></a>Дальнейшие действия

* Ознакомьтесь со статьей [Зоны и записи DNS](dns-zones-records.md).
* toostart с помощью Azure DNS, узнайте, как слишком[создать зону DNS](dns-getstarted-create-dnszone-portal.md) и [Создание записей DNS](dns-getstarted-create-recordset-portal.md).
* toomigrate существующую зону DNS, узнайте, как слишком[импорта и экспорта файла зоны DNS](dns-import-export.md).

