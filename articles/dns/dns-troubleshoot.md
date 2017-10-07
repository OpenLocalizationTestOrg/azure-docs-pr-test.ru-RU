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
# <a name="azure-dns-troubleshooting-guide"></a><span data-ttu-id="fe705-103">Руководство по устранению неполадок службы DNS Azure</span><span class="sxs-lookup"><span data-stu-id="fe705-103">Azure DNS troubleshooting guide</span></span>

<span data-ttu-id="fe705-104">На этой странице представлены сведения об устранении распространенных неполадок службы DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="fe705-104">This page provides troubleshooting information for common Azure DNS questions.</span></span>

<span data-ttu-id="fe705-105">Если с помощью описанных выше шагов не удалось решить проблему, то воспользуйтесь поиском или сообщите о свой проблеме на нашем [форуме поддержки сообщества на сайте MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span><span class="sxs-lookup"><span data-stu-id="fe705-105">If these steps don't resolve your issue, you can also search for or post your issue on our [community support forum on MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span></span> <span data-ttu-id="fe705-106">Вы также можете отправить запрос в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="fe705-106">Alternatively, open an Azure support request.</span></span>


## <a name="i-cant-create-a-dns-zone"></a><span data-ttu-id="fe705-107">Не удается создать зону DNS</span><span class="sxs-lookup"><span data-stu-id="fe705-107">I can't create a DNS zone</span></span>

<span data-ttu-id="fe705-108">tooresolve распространенные проблемы, выполните одно или несколько действий hello.</span><span class="sxs-lookup"><span data-stu-id="fe705-108">tooresolve common issues, try one or more of hello following steps:</span></span>

1.  <span data-ttu-id="fe705-109">Просмотр приветствия аудита Azure DNS заносит в журнал toodetermine причина сбоя hello.</span><span class="sxs-lookup"><span data-stu-id="fe705-109">Review hello Azure DNS audit logs toodetermine hello failure reason.</span></span>
2.  <span data-ttu-id="fe705-110">Каждое имя зоны DNS должно быть уникальным в пределах соответствующей группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fe705-110">Each DNS zone name must be unique within its resource group.</span></span> <span data-ttu-id="fe705-111">То есть два DNS-зоны с hello таким же именем, не могут совместно использовать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fe705-111">That is, two DNS zones with hello same name cannot share a resource group.</span></span> <span data-ttu-id="fe705-112">Попробуйте использовать другое имя зоны или другую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fe705-112">Try using a different zone name, or a different resource group.</span></span>
3.  <span data-ttu-id="fe705-113">Может появиться ошибка «Достигнуто или превышено максимальное число зон в подписке {subscription id} hello.»</span><span class="sxs-lookup"><span data-stu-id="fe705-113">You may see an error "You have reached or exceeded hello maximum number of zones in subscription {subscription id}."</span></span> <span data-ttu-id="fe705-114">Используйте другую подписку Azure, удалите некоторые зоны или обратитесь в службу поддержки Azure tooraise лимита подписки.</span><span class="sxs-lookup"><span data-stu-id="fe705-114">Either use a different Azure subscription, delete some zones, or contact Azure Support tooraise your subscription limit.</span></span>
4.  <span data-ttu-id="fe705-115">Появится сообщение об ошибке «hello зоны «{зоны name}» не доступен.»</span><span class="sxs-lookup"><span data-stu-id="fe705-115">You may see an error "hello zone '{zone name}' is not available."</span></span> <span data-ttu-id="fe705-116">Эта ошибка означает, что Azure DNS не удается tooallocate серверы имен для этой зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="fe705-116">This error means that Azure DNS was unable tooallocate name servers for this DNS zone.</span></span> <span data-ttu-id="fe705-117">Попробуйте использовать другое имя зоны.</span><span class="sxs-lookup"><span data-stu-id="fe705-117">Try using a different zone name.</span></span> <span data-ttu-id="fe705-118">Кроме того Если вы являетесь владельцем имя домена hello, обратитесь в службу поддержки Azure, который можно выделить серверы имен автоматически.</span><span class="sxs-lookup"><span data-stu-id="fe705-118">Alternatively, if you are hello domain name owner, contact Azure support, who can allocate name servers for you.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="fe705-119">**Рекомендуемые документы**</span><span class="sxs-lookup"><span data-stu-id="fe705-119">**Recommended documents**</span></span>

<span data-ttu-id="fe705-120">[DNS zones and records](dns-zones-records.md)
 (Зоны и записи DNS)</span><span class="sxs-lookup"><span data-stu-id="fe705-120">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="fe705-121">
[Создание зоны DNS на портале Azure](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="fe705-121">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>

## <a name="i-cant-create-a-dns-record"></a><span data-ttu-id="fe705-122">Не удается создать запись DNS</span><span class="sxs-lookup"><span data-stu-id="fe705-122">I can't create a DNS record</span></span>

<span data-ttu-id="fe705-123">tooresolve распространенные проблемы, выполните одно или несколько действий hello.</span><span class="sxs-lookup"><span data-stu-id="fe705-123">tooresolve common issues, try one or more of hello following steps:</span></span>

1.  <span data-ttu-id="fe705-124">Просмотр приветствия аудита Azure DNS заносит в журнал toodetermine причина сбоя hello.</span><span class="sxs-lookup"><span data-stu-id="fe705-124">Review hello Azure DNS audit logs toodetermine hello failure reason.</span></span>
2.  <span data-ttu-id="fe705-125">Набор записей hello существует ли?</span><span class="sxs-lookup"><span data-stu-id="fe705-125">Does hello record set exist already?</span></span>  <span data-ttu-id="fe705-126">Azure DNS управляет записей с помощью записи *задает*, которые являются hello коллекцию записей hello совпадают имя и hello таким же типа.</span><span class="sxs-lookup"><span data-stu-id="fe705-126">Azure DNS manages records using record *sets*, which are hello collection of records of hello same name and hello same type.</span></span> <span data-ttu-id="fe705-127">Если запись с hello совпадают имя и тип уже существует, tooadd другой такой записи, рекомендуется изменить существующую запись hello задайте.</span><span class="sxs-lookup"><span data-stu-id="fe705-127">If a record with hello same name and type already exists, then tooadd another such record you should edit hello existing record set.</span></span>
3.  <span data-ttu-id="fe705-128">Вы пытаетесь toocreate запись на вершине зоны DNS hello (hello 'root' hello зоны)?</span><span class="sxs-lookup"><span data-stu-id="fe705-128">Are you trying toocreate a record at hello DNS zone apex (hello ‘root’ of hello zone)?</span></span> <span data-ttu-id="fe705-129">Если таким образом, hello DNS соглашение toouse hello ' @' символ имени записи hello.</span><span class="sxs-lookup"><span data-stu-id="fe705-129">If so, hello DNS convention is toouse hello ‘@’ character as hello record name.</span></span> <span data-ttu-id="fe705-130">Также Обратите внимание, что стандартах DNS hello не разрешать записи CNAME в зоне вершина hello.</span><span class="sxs-lookup"><span data-stu-id="fe705-130">Also note that hello DNS standards do not permit CNAME records at hello zone apex.</span></span>
4.  <span data-ttu-id="fe705-131">Возник конфликт CNAME?</span><span class="sxs-lookup"><span data-stu-id="fe705-131">Do you have a CNAME conflict?</span></span>  <span data-ttu-id="fe705-132">Hello стандартах DNS не разрешать запись CNAME с hello одинаковые имена, как запись с любого другого типа.</span><span class="sxs-lookup"><span data-stu-id="fe705-132">hello DNS standards do not allow a CNAME record with hello same name as a record of any other type.</span></span> <span data-ttu-id="fe705-133">При наличии существующего CNAME, создается запись с hello завершается с ошибкой, именем другого типа.</span><span class="sxs-lookup"><span data-stu-id="fe705-133">If you have an existing CNAME, creating a record with hello same name of a different type fails.</span></span>  <span data-ttu-id="fe705-134">Аналогичным образом Создание CNAME завершается сбоем, если имя hello соответствует существующей записи другого типа.</span><span class="sxs-lookup"><span data-stu-id="fe705-134">Likewise, creating a CNAME fails if hello name matches an existing record of a different type.</span></span> <span data-ttu-id="fe705-135">Удалите hello конфликт, удалив hello, другие записи или выбрать другую запись имя.</span><span class="sxs-lookup"><span data-stu-id="fe705-135">Remove hello conflict by removing hello other record or choosing a different record name.</span></span>
5.  <span data-ttu-id="fe705-136">Достигнуто максимально hello hello количество наборы записей, которые могут использоваться в зоне DNS? Привет текущее число наборов записей и hello максимальное число наборов записей отображаются в hello портал Azure, в разделе hello «свойства» hello зоны.</span><span class="sxs-lookup"><span data-stu-id="fe705-136">Have you reached hello limit on hello number of record sets permitted in a DNS zone? hello current number of record sets and hello maximum number of record sets are shown in hello Azure portal, under hello 'Properties' for hello zone.</span></span> <span data-ttu-id="fe705-137">Если этот предел достигнут, затем либо удалить некоторые наборы записей или обратитесь в службу поддержки Azure tooraise лимита набора записей для данной зоны, и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="fe705-137">If you have reached this limit, then either delete some record sets or contact Azure Support tooraise your record set limit for this zone, then try again.</span></span> 


### <a name="recommended-documents"></a><span data-ttu-id="fe705-138">**Рекомендуемые документы**</span><span class="sxs-lookup"><span data-stu-id="fe705-138">**Recommended documents**</span></span>

<span data-ttu-id="fe705-139">[DNS zones and records](dns-zones-records.md)
 (Зоны и записи DNS)</span><span class="sxs-lookup"><span data-stu-id="fe705-139">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="fe705-140">
[Создание зоны DNS на портале Azure](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="fe705-140">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>



## <a name="i-cant-resolve-my-dns-record"></a><span data-ttu-id="fe705-141">Не удается разрешить новую запись DNS</span><span class="sxs-lookup"><span data-stu-id="fe705-141">I can't resolve my DNS record</span></span>

<span data-ttu-id="fe705-142">Разрешение DNS-имен — это многоэтапный процесс, который может завершиться ошибкой по многим причинам.</span><span class="sxs-lookup"><span data-stu-id="fe705-142">DNS name resolution is a multi-step process, which can fail for many reasons.</span></span> <span data-ttu-id="fe705-143">Hello следующие действия помогут изучить, почему происходит сбой разрешения DNS для записи DNS в зоне, размещенной в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="fe705-143">hello following steps help you investigate why DNS resolution is failing for a DNS record in a zone hosted in Azure DNS.</span></span>

1.  <span data-ttu-id="fe705-144">Убедитесь, что записи DNS hello настроены правильно в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="fe705-144">Confirm that hello DNS records have been configured correctly in Azure DNS.</span></span> <span data-ttu-id="fe705-145">Просмотрите записи DNS hello в hello портал Azure, проверьте правильность имени зоны hello, именем записи и тип записи.</span><span class="sxs-lookup"><span data-stu-id="fe705-145">Review hello DNS records in hello Azure portal, checking that hello zone name, record name, and record type are correct.</span></span>
2.  <span data-ttu-id="fe705-146">Убедитесь, правильно разрешать DNS-записи hello на hello Azure DNS-серверами.</span><span class="sxs-lookup"><span data-stu-id="fe705-146">Confirm that hello DNS records resolve correctly on hello Azure DNS name servers.</span></span>
    - <span data-ttu-id="fe705-147">Если DNS-запросы с локального компьютера, может появиться кэшированные результаты, которые не отражают текущее состояние серверов имен hello hello.</span><span class="sxs-lookup"><span data-stu-id="fe705-147">If you make DNS queries from your local PC, you may see cached results that don’t reflect hello current state of hello name servers.</span></span>  <span data-ttu-id="fe705-148">Кроме того, корпоративной сети часто используют прокси-серверов DNS, который препятствует DNS-запросы направляются toospecific серверы имен.</span><span class="sxs-lookup"><span data-stu-id="fe705-148">Also, corporate networks often use DNS proxy servers, which prevent DNS queries from being directed toospecific name servers.</span></span>  <span data-ttu-id="fe705-149">tooavoid этих проблем, использовать службу разрешения имен, веб сервера, такие как [digwebinterface](http://digwebinterface.com).</span><span class="sxs-lookup"><span data-stu-id="fe705-149">tooavoid these problems, use a web-based name resolution service such as [digwebinterface](http://digwebinterface.com).</span></span>
    - <span data-ttu-id="fe705-150">Быть убедиться, что toospecify hello правильное имя серверов для зоны DNS, как показано в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="fe705-150">Be sure toospecify hello correct name servers for your DNS zone, as shown in hello Azure portal.</span></span>
    - <span data-ttu-id="fe705-151">Убедитесь, что hello DNS-имя указано правильно (имеется toospecify hello полное доменное имя, включая имя зоны hello) и правильный тип записи hello</span><span class="sxs-lookup"><span data-stu-id="fe705-151">Check that hello DNS name is correct (you have toospecify hello fully qualified name, including hello zone name) and hello record type is correct</span></span>
3.  <span data-ttu-id="fe705-152">Подтвердите hello DNS-имени домена был правильно [делегированы toohello Azure DNS-серверами](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="fe705-152">Confirm that hello DNS domain name has been correctly [delegated toohello Azure DNS name servers](dns-domain-delegation.md).</span></span> <span data-ttu-id="fe705-153">[Существует множество сторонних веб-сайтов для проверки делегирования DNS](https://www.bing.com/search?q=dns+check+tool).</span><span class="sxs-lookup"><span data-stu-id="fe705-153">There are a [many 3rd-party web sites that offer DNS delegation validation](https://www.bing.com/search?q=dns+check+tool).</span></span> <span data-ttu-id="fe705-154">Этот тест *зоны* проверку делегирования, поэтому следует ввести только имя зоны DNS hello и не hello полное имя записи.</span><span class="sxs-lookup"><span data-stu-id="fe705-154">This test is a *zone* delegation test, so you should only enter hello DNS zone name and not hello fully qualified record name.</span></span>
4.  <span data-ttu-id="fe705-155">Прохождения hello выше записи DNS должны теперь правильно обработать.</span><span class="sxs-lookup"><span data-stu-id="fe705-155">Having completed hello above, your DNS record should now resolve correctly.</span></span> <span data-ttu-id="fe705-156">tooverify, можно повторно использовать [digwebinterface](http://digwebinterface.com), на этот раз hello параметрами по умолчанию имя сервера.</span><span class="sxs-lookup"><span data-stu-id="fe705-156">tooverify, you can again use [digwebinterface](http://digwebinterface.com), this time using hello default name server settings.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="fe705-157">**Рекомендуемые документы**</span><span class="sxs-lookup"><span data-stu-id="fe705-157">**Recommended documents**</span></span>

[<span data-ttu-id="fe705-158">Делегат tooAzure домена DNS</span><span class="sxs-lookup"><span data-stu-id="fe705-158">Delegate a domain tooAzure DNS</span></span>](dns-domain-delegation.md)



## <a name="how-do-i-specify-hello-service-and-protocol-for-an-srv-record"></a><span data-ttu-id="fe705-159">Как указать hello «службы» и «протокол» для записи SRV?</span><span class="sxs-lookup"><span data-stu-id="fe705-159">How do I specify hello ‘service’ and ‘protocol’ for an SRV record?</span></span>

<span data-ttu-id="fe705-160">Azure DNS управляет записями DNS в качестве наборов записей — hello коллекцию записей с hello совпадают имя и hello же типа.</span><span class="sxs-lookup"><span data-stu-id="fe705-160">Azure DNS manages DNS records as record sets—hello collection of records with hello same name and hello same type.</span></span> <span data-ttu-id="fe705-161">Набор записей типа SRV hello «службы» и «протокол» должны toobe, заданный как часть hello имя набора записей.</span><span class="sxs-lookup"><span data-stu-id="fe705-161">For an SRV record set, hello 'service' and 'protocol' need toobe specified as part of hello record set name.</span></span> <span data-ttu-id="fe705-162">Hello SRV указаны другие параметры («приоритет», «weight», «порт» и «целевой объект») отдельно для каждой записи в наборе записей hello.</span><span class="sxs-lookup"><span data-stu-id="fe705-162">hello other SRV parameters ('priority', 'weight', 'port' and 'target') are specified separately for each record in hello record set.</span></span>

<span data-ttu-id="fe705-163">Примеры имен записей SRV (имя службы — SIP, протокол — TCP):</span><span class="sxs-lookup"><span data-stu-id="fe705-163">Example SRV record names (service name 'sip', protocol 'tcp'):</span></span>

- <span data-ttu-id="fe705-164">\_SIP. \_tcp (создает набор в вершине зоны hello записей)</span><span class="sxs-lookup"><span data-stu-id="fe705-164">\_sip.\_tcp (creates a record set at hello zone apex)</span></span>
- <span data-ttu-id="fe705-165">\_sip.\_tcp.sipservice (создает набор записей с именем sipservice).</span><span class="sxs-lookup"><span data-stu-id="fe705-165">\_sip.\_tcp.sipservice (creates a record set named 'sipservice')</span></span>

### <a name="recommended-documents"></a><span data-ttu-id="fe705-166">**Рекомендуемые документы**</span><span class="sxs-lookup"><span data-stu-id="fe705-166">**Recommended documents**</span></span>

<span data-ttu-id="fe705-167">[DNS zones and records](dns-zones-records.md)
 (Зоны и записи DNS)</span><span class="sxs-lookup"><span data-stu-id="fe705-167">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="fe705-168">
[Создание наборов записей DNS и записей с помощью hello портал Azure](dns-getstarted-create-recordset-portal.md)
</span><span class="sxs-lookup"><span data-stu-id="fe705-168">
[Create DNS record sets and records by using hello Azure portal](dns-getstarted-create-recordset-portal.md)
</span></span><br><span data-ttu-id="fe705-169">
[SRV-запись (Википедия)](https://en.wikipedia.org/wiki/SRV_record)</span><span class="sxs-lookup"><span data-stu-id="fe705-169">
[SRV record type (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span></span>


## <a name="next-steps"></a><span data-ttu-id="fe705-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fe705-170">Next steps</span></span>

* <span data-ttu-id="fe705-171">Ознакомьтесь со статьей [Зоны и записи DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="fe705-171">Learn about [Azure DNS zones and records](dns-zones-records.md)</span></span>
* <span data-ttu-id="fe705-172">toostart с помощью Azure DNS, узнайте, как слишком[создать зону DNS](dns-getstarted-create-dnszone-portal.md) и [Создание записей DNS](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fe705-172">toostart using Azure DNS, learn how too[create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span></span>
* <span data-ttu-id="fe705-173">toomigrate существующую зону DNS, узнайте, как слишком[импорта и экспорта файла зоны DNS](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="fe705-173">toomigrate an existing DNS zone, learn how too[import and export a DNS zone file](dns-import-export.md).</span></span>

