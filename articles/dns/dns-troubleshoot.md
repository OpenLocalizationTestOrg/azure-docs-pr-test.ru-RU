---
title: "Руководство по устранению неполадок службы DNS Azure | Документация Майкрософт"
description: "Описывается, как устранять распространенные неполадки службы DNS Azure."
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
ms.openlocfilehash: 1d9bb681a864bdc3e5a2f9c9a531d9566b16ada4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-dns-troubleshooting-guide"></a><span data-ttu-id="0f9f0-103">Руководство по устранению неполадок службы DNS Azure</span><span class="sxs-lookup"><span data-stu-id="0f9f0-103">Azure DNS troubleshooting guide</span></span>

<span data-ttu-id="0f9f0-104">На этой странице представлены сведения об устранении распространенных неполадок службы DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-104">This page provides troubleshooting information for common Azure DNS questions.</span></span>

<span data-ttu-id="0f9f0-105">Если с помощью описанных выше шагов не удалось решить проблему, то воспользуйтесь поиском или сообщите о свой проблеме на нашем [форуме поддержки сообщества на сайте MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span><span class="sxs-lookup"><span data-stu-id="0f9f0-105">If these steps don't resolve your issue, you can also search for or post your issue on our [community support forum on MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span></span> <span data-ttu-id="0f9f0-106">Вы также можете отправить запрос в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-106">Alternatively, open an Azure support request.</span></span>


## <a name="i-cant-create-a-dns-zone"></a><span data-ttu-id="0f9f0-107">Не удается создать зону DNS</span><span class="sxs-lookup"><span data-stu-id="0f9f0-107">I can't create a DNS zone</span></span>

<span data-ttu-id="0f9f0-108">Устранить распространенные неполадки можно с помощью одного или нескольких описанных ниже методов.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-108">To resolve common issues, try one or more of the following steps:</span></span>

1.  <span data-ttu-id="0f9f0-109">Просмотрите журналы аудита службы DNS Azure, чтобы определить причину сбоя.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-109">Review the Azure DNS audit logs to determine the failure reason.</span></span>
2.  <span data-ttu-id="0f9f0-110">Каждое имя зоны DNS должно быть уникальным в пределах соответствующей группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-110">Each DNS zone name must be unique within its resource group.</span></span> <span data-ttu-id="0f9f0-111">То есть две зоны DNS с одним и тем же именем не могут совместно использовать одну группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-111">That is, two DNS zones with the same name cannot share a resource group.</span></span> <span data-ttu-id="0f9f0-112">Попробуйте использовать другое имя зоны или другую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-112">Try using a different zone name, or a different resource group.</span></span>
3.  <span data-ttu-id="0f9f0-113">Может появиться сообщение об ошибке "Достигнуто или превышено максимально допустимое число зон в подписке {идентификатор подписки}".</span><span class="sxs-lookup"><span data-stu-id="0f9f0-113">You may see an error "You have reached or exceeded the maximum number of zones in subscription {subscription id}."</span></span> <span data-ttu-id="0f9f0-114">Используйте другую подписку Azure, удалите несколько зон или обратитесь в службу поддержки Azure, чтобы расширить ограничения для подписки.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-114">Either use a different Azure subscription, delete some zones, or contact Azure Support to raise your subscription limit.</span></span>
4.  <span data-ttu-id="0f9f0-115">Может появиться сообщение об ошибке "Зона "{имя зоны}" недоступна".</span><span class="sxs-lookup"><span data-stu-id="0f9f0-115">You may see an error "The zone '{zone name}' is not available."</span></span> <span data-ttu-id="0f9f0-116">Эта ошибка означает, что службе DNS Azure не удалось выделить серверы имен для этой зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-116">This error means that Azure DNS was unable to allocate name servers for this DNS zone.</span></span> <span data-ttu-id="0f9f0-117">Попробуйте использовать другое имя зоны.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-117">Try using a different zone name.</span></span> <span data-ttu-id="0f9f0-118">Если вы являетесь владельцем доменного имени, обратитесь в службу поддержки Azure с просьбой выделить для вас серверы имен.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-118">Alternatively, if you are the domain name owner, contact Azure support, who can allocate name servers for you.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="0f9f0-119">**Рекомендуемые документы**</span><span class="sxs-lookup"><span data-stu-id="0f9f0-119">**Recommended documents**</span></span>

<span data-ttu-id="0f9f0-120">[DNS zones and records](dns-zones-records.md)
 (Зоны и записи DNS)</span><span class="sxs-lookup"><span data-stu-id="0f9f0-120">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="0f9f0-121">
[Создание зоны DNS на портале Azure](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="0f9f0-121">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>

## <a name="i-cant-create-a-dns-record"></a><span data-ttu-id="0f9f0-122">Не удается создать запись DNS</span><span class="sxs-lookup"><span data-stu-id="0f9f0-122">I can't create a DNS record</span></span>

<span data-ttu-id="0f9f0-123">Устранить распространенные неполадки можно с помощью одного или нескольких описанных ниже методов.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-123">To resolve common issues, try one or more of the following steps:</span></span>

1.  <span data-ttu-id="0f9f0-124">Просмотрите журналы аудита службы DNS Azure, чтобы определить причину сбоя.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-124">Review the Azure DNS audit logs to determine the failure reason.</span></span>
2.  <span data-ttu-id="0f9f0-125">Набор записей уже существует?</span><span class="sxs-lookup"><span data-stu-id="0f9f0-125">Does the record set exist already?</span></span>  <span data-ttu-id="0f9f0-126">Azure DNS управляет записями с помощью *наборов* записей. Это коллекция записей одного типа и с одинаковыми именами.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-126">Azure DNS manages records using record *sets*, which are the collection of records of the same name and the same type.</span></span> <span data-ttu-id="0f9f0-127">Если запись того же типа и с тем же именем уже существует, для добавления другой такой записи следует изменить существующий набор записей.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-127">If a record with the same name and type already exists, then to add another such record you should edit the existing record set.</span></span>
3.  <span data-ttu-id="0f9f0-128">Вы пытаетесь создать запись на вершине зоны DNS (в "корне" зоны)?</span><span class="sxs-lookup"><span data-stu-id="0f9f0-128">Are you trying to create a record at the DNS zone apex (the ‘root’ of the zone)?</span></span> <span data-ttu-id="0f9f0-129">Если это так, в соответствии с DNS-соглашением в качестве имени записи используется символ @.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-129">If so, the DNS convention is to use the ‘@’ character as the record name.</span></span> <span data-ttu-id="0f9f0-130">Также обратите внимание, что стандарты DNS запрещают создавать записи CNAME на вершине зоны.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-130">Also note that the DNS standards do not permit CNAME records at the zone apex.</span></span>
4.  <span data-ttu-id="0f9f0-131">Возник конфликт CNAME?</span><span class="sxs-lookup"><span data-stu-id="0f9f0-131">Do you have a CNAME conflict?</span></span>  <span data-ttu-id="0f9f0-132">Стандарты DNS запрещают создавать записи CNAME с тем же именем, относящиеся к любому другом типу.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-132">The DNS standards do not allow a CNAME record with the same name as a record of any other type.</span></span> <span data-ttu-id="0f9f0-133">Если у вас уже есть запись CNAME, создание записи другого типа с тем же именем завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-133">If you have an existing CNAME, creating a record with the same name of a different type fails.</span></span>  <span data-ttu-id="0f9f0-134">Точно так же не удастся создать запись CNAME, если ее имя совпадает с именем существующей записи другого типа.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-134">Likewise, creating a CNAME fails if the name matches an existing record of a different type.</span></span> <span data-ttu-id="0f9f0-135">Чтобы устранить конфликт, удалите другие записи или выберите для записи другое имя.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-135">Remove the conflict by removing the other record or choosing a different record name.</span></span>
5.  <span data-ttu-id="0f9f0-136">Достигнуто предельное число наборов записей, разрешенных в зоне DNS?</span><span class="sxs-lookup"><span data-stu-id="0f9f0-136">Have you reached the limit on the number of record sets permitted in a DNS zone?</span></span> <span data-ttu-id="0f9f0-137">Текущее и максимальное число наборов записей отображаются на портале Azure в разделе "Свойства" для зоны.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-137">The current number of record sets and the maximum number of record sets are shown in the Azure portal, under the 'Properties' for the zone.</span></span> <span data-ttu-id="0f9f0-138">Если этот предел достигнут, удалите некоторые наборы записей или обратитесь в службу поддержки Azure, чтобы увеличить лимит набора записей для этой зоны, а затем повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-138">If you have reached this limit, then either delete some record sets or contact Azure Support to raise your record set limit for this zone, then try again.</span></span> 


### <a name="recommended-documents"></a><span data-ttu-id="0f9f0-139">**Рекомендуемые документы**</span><span class="sxs-lookup"><span data-stu-id="0f9f0-139">**Recommended documents**</span></span>

<span data-ttu-id="0f9f0-140">[DNS zones and records](dns-zones-records.md)
 (Зоны и записи DNS)</span><span class="sxs-lookup"><span data-stu-id="0f9f0-140">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="0f9f0-141">
[Создание зоны DNS на портале Azure](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="0f9f0-141">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>



## <a name="i-cant-resolve-my-dns-record"></a><span data-ttu-id="0f9f0-142">Не удается разрешить новую запись DNS</span><span class="sxs-lookup"><span data-stu-id="0f9f0-142">I can't resolve my DNS record</span></span>

<span data-ttu-id="0f9f0-143">Разрешение DNS-имен — это многоэтапный процесс, который может завершиться ошибкой по многим причинам.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-143">DNS name resolution is a multi-step process, which can fail for many reasons.</span></span> <span data-ttu-id="0f9f0-144">Приведенные ниже действия помогут вам выяснить, почему не удается разрешить запись DNS в зоне, размещенной в службе DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-144">The following steps help you investigate why DNS resolution is failing for a DNS record in a zone hosted in Azure DNS.</span></span>

1.  <span data-ttu-id="0f9f0-145">Проверьте, правильно ли настроены записи DNS в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-145">Confirm that the DNS records have been configured correctly in Azure DNS.</span></span> <span data-ttu-id="0f9f0-146">Просмотрите записи DNS на портале Azure и проверьте, правильно ли указаны имя зоны, имя записи и тип записи.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-146">Review the DNS records in the Azure portal, checking that the zone name, record name, and record type are correct.</span></span>
2.  <span data-ttu-id="0f9f0-147">Проверьте, правильно ли разрешаются записи DNS на DNS-серверах Azure.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-147">Confirm that the DNS records resolve correctly on the Azure DNS name servers.</span></span>
    - <span data-ttu-id="0f9f0-148">Если вы создаете запросы DNS на локальном компьютере, могут появляться кэшированные результаты, которые не отражают текущее состояние серверов имен.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-148">If you make DNS queries from your local PC, you may see cached results that don’t reflect the current state of the name servers.</span></span>  <span data-ttu-id="0f9f0-149">Кроме того, в корпоративных сетях часто используются прокси-серверы DNS, препятствующие направлению запросов DNS на определенные серверы имен.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-149">Also, corporate networks often use DNS proxy servers, which prevent DNS queries from being directed to specific name servers.</span></span>  <span data-ttu-id="0f9f0-150">Чтобы избежать этих проблем, используйте веб-службу разрешения имен, например [digwebinterface](http://digwebinterface.com).</span><span class="sxs-lookup"><span data-stu-id="0f9f0-150">To avoid these problems, use a web-based name resolution service such as [digwebinterface](http://digwebinterface.com).</span></span>
    - <span data-ttu-id="0f9f0-151">Обязательно указывайте правильные серверы имен для своей зоны DNS (их можно проверить на портале Azure).</span><span class="sxs-lookup"><span data-stu-id="0f9f0-151">Be sure to specify the correct name servers for your DNS zone, as shown in the Azure portal.</span></span>
    - <span data-ttu-id="0f9f0-152">Убедитесь, что DNS-имя (полное доменное имя, включающее имя зоны) и тип записи указаны правильно.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-152">Check that the DNS name is correct (you have to specify the fully qualified name, including the zone name) and the record type is correct</span></span>
3.  <span data-ttu-id="0f9f0-153">Убедитесь, что DNS-имя домена правильно [делегировано DNS-серверам Azure](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="0f9f0-153">Confirm that the DNS domain name has been correctly [delegated to the Azure DNS name servers](dns-domain-delegation.md).</span></span> <span data-ttu-id="0f9f0-154">[Существует множество сторонних веб-сайтов для проверки делегирования DNS](https://www.bing.com/search?q=dns+check+tool).</span><span class="sxs-lookup"><span data-stu-id="0f9f0-154">There are a [many 3rd-party web sites that offer DNS delegation validation](https://www.bing.com/search?q=dns+check+tool).</span></span> <span data-ttu-id="0f9f0-155">Это тест делегирования *зоны*, поэтому следует вводить только имя зоны DNS, а не полное имя записи.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-155">This test is a *zone* delegation test, so you should only enter the DNS zone name and not the fully qualified record name.</span></span>
4.  <span data-ttu-id="0f9f0-156">После выполнения этих шагов запись DNS должна разрешаться правильно.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-156">Having completed the above, your DNS record should now resolve correctly.</span></span> <span data-ttu-id="0f9f0-157">Чтобы проверить, так ли это, можно повторно использовать [digwebinterface](http://digwebinterface.com) — на этот раз с использованием стандартных параметров сервера имен.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-157">To verify, you can again use [digwebinterface](http://digwebinterface.com), this time using the default name server settings.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="0f9f0-158">**Рекомендуемые документы**</span><span class="sxs-lookup"><span data-stu-id="0f9f0-158">**Recommended documents**</span></span>

[<span data-ttu-id="0f9f0-159">Делегирование домена в Azure DNS</span><span class="sxs-lookup"><span data-stu-id="0f9f0-159">Delegate a domain to Azure DNS</span></span>](dns-domain-delegation.md)



## <a name="how-do-i-specify-the-service-and-protocol-for-an-srv-record"></a><span data-ttu-id="0f9f0-160">Как указать службу и протокол для записи SRV</span><span class="sxs-lookup"><span data-stu-id="0f9f0-160">How do I specify the ‘service’ and ‘protocol’ for an SRV record?</span></span>

<span data-ttu-id="0f9f0-161">Azure DNS управляет записями DNS как наборами записей. Это коллекции записей одного типа и с одинаковыми именами.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-161">Azure DNS manages DNS records as record sets—the collection of records with the same name and the same type.</span></span> <span data-ttu-id="0f9f0-162">Для набора записей SRV службу и протокол необходимо указывать как часть имени набора записей.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-162">For an SRV record set, the 'service' and 'protocol' need to be specified as part of the record set name.</span></span> <span data-ttu-id="0f9f0-163">Другие параметры SRV (приоритет, вес, порт и целевое значение) указываются отдельно для каждой записи в наборе записей.</span><span class="sxs-lookup"><span data-stu-id="0f9f0-163">The other SRV parameters ('priority', 'weight', 'port' and 'target') are specified separately for each record in the record set.</span></span>

<span data-ttu-id="0f9f0-164">Примеры имен записей SRV (имя службы — SIP, протокол — TCP):</span><span class="sxs-lookup"><span data-stu-id="0f9f0-164">Example SRV record names (service name 'sip', protocol 'tcp'):</span></span>

- <span data-ttu-id="0f9f0-165">\_sip.\_tcp (создает набор записей на вершине зоны);</span><span class="sxs-lookup"><span data-stu-id="0f9f0-165">\_sip.\_tcp (creates a record set at the zone apex)</span></span>
- <span data-ttu-id="0f9f0-166">\_sip.\_tcp.sipservice (создает набор записей с именем sipservice).</span><span class="sxs-lookup"><span data-stu-id="0f9f0-166">\_sip.\_tcp.sipservice (creates a record set named 'sipservice')</span></span>

### <a name="recommended-documents"></a><span data-ttu-id="0f9f0-167">**Рекомендуемые документы**</span><span class="sxs-lookup"><span data-stu-id="0f9f0-167">**Recommended documents**</span></span>

<span data-ttu-id="0f9f0-168">[DNS zones and records](dns-zones-records.md)
 (Зоны и записи DNS)</span><span class="sxs-lookup"><span data-stu-id="0f9f0-168">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="0f9f0-169">
[Создание наборов записей и записей DNS с помощью портала Azure](dns-getstarted-create-recordset-portal.md)
</span><span class="sxs-lookup"><span data-stu-id="0f9f0-169">
[Create DNS record sets and records by using the Azure portal](dns-getstarted-create-recordset-portal.md)
</span></span><br><span data-ttu-id="0f9f0-170">
[SRV-запись (Википедия)](https://en.wikipedia.org/wiki/SRV_record)</span><span class="sxs-lookup"><span data-stu-id="0f9f0-170">
[SRV record type (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span></span>


## <a name="next-steps"></a><span data-ttu-id="0f9f0-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0f9f0-171">Next steps</span></span>

* <span data-ttu-id="0f9f0-172">Ознакомьтесь со статьей [Зоны и записи DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="0f9f0-172">Learn about [Azure DNS zones and records](dns-zones-records.md)</span></span>
* <span data-ttu-id="0f9f0-173">Чтобы начать работу с Azure DNS, узнайте, как [создать зону DNS](dns-getstarted-create-dnszone-portal.md) и [записи DNS](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0f9f0-173">To start using Azure DNS, learn how to [create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span></span>
* <span data-ttu-id="0f9f0-174">Чтобы перенести имеющуюся зону DNS, узнайте, как [импортировать и экспортировать файл зоны DNS](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="0f9f0-174">To migrate an existing DNS zone, learn how to [import and export a DNS zone file](dns-import-export.md).</span></span>

