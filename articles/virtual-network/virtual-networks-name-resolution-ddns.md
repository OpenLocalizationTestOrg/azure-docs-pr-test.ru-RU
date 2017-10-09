---
title: "aaaUsing имена узлов tooregister динамической DNS"
description: "На этой странице приведены сведения о том, как tooset копирование имена узлов tooregister динамической DNS в DNS-серверы."
services: dns
documentationcenter: na
author: GarethBradshawMSFT
manager: timlt
editor: 
ms.assetid: c315961a-fa33-45cf-82b9-4551e70d32dd
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2017
ms.author: garbrad
ms.openlocfilehash: 8d4b44265714e6976f26bfb3446e8101aa70996a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-dynamic-dns-tooregister-hostnames-in-your-own-dns-server"></a><span data-ttu-id="79616-103">Использование имен узлов tooregister динамической DNS в DNS-сервере</span><span class="sxs-lookup"><span data-stu-id="79616-103">Using Dynamic DNS tooregister hostnames in your own DNS server</span></span>
<span data-ttu-id="79616-104">[Azure предоставляет разрешение имен](virtual-networks-name-resolution-for-vms-and-role-instances.md) для виртуальных машин и экземпляров ролей.</span><span class="sxs-lookup"><span data-stu-id="79616-104">[Azure provides name resolution](virtual-networks-name-resolution-for-vms-and-role-instances.md) for virtual machines (VMs) and role instances.</span></span> <span data-ttu-id="79616-105">Однако, если разрешение имен должно выходить за рамки возможностей Azure, вы можете предоставить свои DNS-серверы.</span><span class="sxs-lookup"><span data-stu-id="79616-105">However, when your name resolution needs go beyond those provided by Azure, you can provide your own DNS servers.</span></span> <span data-ttu-id="79616-106">Это дает hello power tootailor вашей toosuit решение DNS конкретных целей.</span><span class="sxs-lookup"><span data-stu-id="79616-106">This gives you hello power tootailor your DNS solution toosuit your own specific needs.</span></span> <span data-ttu-id="79616-107">Например может потребоваться tooaccess локальным ресурсам через контроллер домена Active Directory.</span><span class="sxs-lookup"><span data-stu-id="79616-107">For example, you may need tooaccess on-premises resources via your Active Directory domain controller.</span></span>

<span data-ttu-id="79616-108">Когда пользовательские DNS-серверы размещены как ВМ Azure, можно передать имя узла запрашивает hello же имен узлов tooresolve tooAzure виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="79616-108">When your custom DNS servers are hosted as Azure VMs you can forward hostname queries for hello same vnet tooAzure tooresolve hostnames.</span></span> <span data-ttu-id="79616-109">Если вы не готовы toouse этот маршрут, имена узлов вашей виртуальной Машины можно зарегистрировать в DNS-сервере с помощью динамической DNS.</span><span class="sxs-lookup"><span data-stu-id="79616-109">If you do not wish toouse this route, you can register your VM hostnames in your DNS server using Dynamic DNS.</span></span>  <span data-ttu-id="79616-110">Azure не имеет toodirectly возможность (например, учетные данные) hello создания записей в DNS-серверы, поэтому часто требуются альтернативные расположения.</span><span class="sxs-lookup"><span data-stu-id="79616-110">Azure doesn't have hello ability (e.g. credentials) toodirectly create records in your DNS servers, so alternative arrangements are often needed.</span></span> <span data-ttu-id="79616-111">Ниже приведены некоторые распространенные сценарии и альтернативные варианты.</span><span class="sxs-lookup"><span data-stu-id="79616-111">Here are some common scenarios with alternatives.</span></span>

## <a name="windows-clients"></a><span data-ttu-id="79616-112">Клиенты Windows</span><span class="sxs-lookup"><span data-stu-id="79616-112">Windows clients</span></span>
<span data-ttu-id="79616-113">Не входящие в домен клиенты Windows пытаются выполнить небезопасные обновления динамических DNS (DDNS) при загрузке или изменении своего IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="79616-113">Non-domain-joined Windows clients attempt unsecured Dynamic DNS (DDNS) updates when they boot or when their IP address changes.</span></span> <span data-ttu-id="79616-114">имя DNS Hello является hello имя узла и основной DNS-суффикс hello.</span><span class="sxs-lookup"><span data-stu-id="79616-114">hello DNS name is hello hostname plus hello primary DNS suffix.</span></span> <span data-ttu-id="79616-115">Azure оставляет пустым hello основной DNS-суффикс, но это можно задать в hello виртуальной Машины, через hello [пользовательского интерфейса](https://technet.microsoft.com/library/cc794784.aspx) или [с помощью автоматизации](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span><span class="sxs-lookup"><span data-stu-id="79616-115">Azure leaves hello primary DNS suffix blank, but you can set this in hello VM, via hello [UI](https://technet.microsoft.com/library/cc794784.aspx) or [by using automation](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span></span>

<span data-ttu-id="79616-116">Присоединенных к домену клиенты Windows зарегистрировать свои IP-адреса контроллера домена hello, используя безопасной динамической DNS.</span><span class="sxs-lookup"><span data-stu-id="79616-116">Domain-joined Windows clients register their IP addresses with hello domain controller by using secure Dynamic DNS.</span></span> <span data-ttu-id="79616-117">процесс присоединения к домену Hello задает hello основной DNS-суффикс на клиенте hello и создает и поддерживает hello доверительные отношения.</span><span class="sxs-lookup"><span data-stu-id="79616-117">hello domain-join process sets hello primary DNS suffix on hello client and creates and maintains hello trust relationship.</span></span>

## <a name="linux-clients"></a><span data-ttu-id="79616-118">Клиенты Linux</span><span class="sxs-lookup"><span data-stu-id="79616-118">Linux clients</span></span>
<span data-ttu-id="79616-119">Клиенты Linux обычно не регистрирует себя с помощью hello DNS-сервера при запуске, они предполагается, что hello DHCP-сервер работает.</span><span class="sxs-lookup"><span data-stu-id="79616-119">Linux clients generally don't register themselves with hello DNS server on startup, they assume hello DHCP server does it.</span></span> <span data-ttu-id="79616-120">DHCP-серверов в Azure имеют способность hello или учетные данные tooregister записей в DNS-сервере.</span><span class="sxs-lookup"><span data-stu-id="79616-120">Azure's DHCP servers do not have hello ability or credentials tooregister records in your DNS server.</span></span>  <span data-ttu-id="79616-121">Можно использовать инструмент, который называется *nsupdate*, входящей в пакет привязки hello, обновляет toosend динамической DNS.</span><span class="sxs-lookup"><span data-stu-id="79616-121">You can use a tool called *nsupdate*, which is included in hello Bind package, toosend Dynamic DNS updates.</span></span> <span data-ttu-id="79616-122">Поскольку Стандартизован hello протокол динамической DNS можно использовать *nsupdate* даже если вы не используете Bind на DNS-сервере hello.</span><span class="sxs-lookup"><span data-stu-id="79616-122">Because hello Dynamic DNS protocol is standardized, you can use *nsupdate* even when you're not using Bind on hello DNS server.</span></span>

<span data-ttu-id="79616-123">Можно использовать обработчики hello, предоставляемые toocreate клиента DHCP hello и поддерживать запись для имени узла hello hello DNS-сервере.</span><span class="sxs-lookup"><span data-stu-id="79616-123">You can use hello hooks that are provided by hello DHCP client toocreate and maintain hello hostname entry in hello DNS server.</span></span> <span data-ttu-id="79616-124">Во время цикла DHCP hello, hello клиент выполняет сценарии hello в */etc/dhcp/dhclient-exit-hooks.d/*.</span><span class="sxs-lookup"><span data-stu-id="79616-124">During hello DHCP cycle, hello client executes hello scripts in */etc/dhcp/dhclient-exit-hooks.d/*.</span></span> <span data-ttu-id="79616-125">Это может быть использовано tooregister hello новый IP-адрес с помощью *nsupdate*.</span><span class="sxs-lookup"><span data-stu-id="79616-125">This can be used tooregister hello new IP address by using *nsupdate*.</span></span> <span data-ttu-id="79616-126">Например:</span><span class="sxs-lookup"><span data-stu-id="79616-126">For example:</span></span>

        #!/bin/sh
        requireddomain=mydomain.local

        # only execute on hello primary nic
        if [ "$interface" != "eth0" ]
        then
            return
        fi

        # when we have a new IP, perform nsupdate
        if [ "$reason" = BOUND ] || [ "$reason" = RENEW ] ||
           [ "$reason" = REBIND ] || [ "$reason" = REBOOT ]
        then
            host=`hostname`
            nsupdatecmds=/var/tmp/nsupdatecmds
              echo "update delete $host.$requireddomain a" > $nsupdatecmds
              echo "update add $host.$requireddomain 3600 a $new_ip_address" >> $nsupdatecmds
              echo "send" >> $nsupdatecmds

              nsupdate $nsupdatecmds
        fi

        
        

<span data-ttu-id="79616-127">Можно также использовать hello *nsupdate* tooperform команда обновляет безопасного динамического DNS.</span><span class="sxs-lookup"><span data-stu-id="79616-127">You can also use hello *nsupdate* command tooperform secure Dynamic DNS updates.</span></span> <span data-ttu-id="79616-128">Например, при использовании DNS-сервера Bind [создается](http://linux.yyz.us/nsupdate/)пара открытого и закрытого ключей.</span><span class="sxs-lookup"><span data-stu-id="79616-128">For example, when you're using a Bind DNS server, a public-private key pair is [generated](http://linux.yyz.us/nsupdate/).</span></span>  <span data-ttu-id="79616-129">DNS-сервер, Hello [настроен](http://linux.yyz.us/dns/ddns-server.html) с hello открытую часть ключа hello, так что он может проверить подпись hello в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="79616-129">hello DNS server is [configured](http://linux.yyz.us/dns/ddns-server.html) with hello public part of hello key so that it can verify hello signature on hello request.</span></span> <span data-ttu-id="79616-130">Необходимо использовать hello *-k* tooprovide параметр hello пары ключей слишком*nsupdate* в порядке для hello динамического обновления DNS подписи toobe запроса.</span><span class="sxs-lookup"><span data-stu-id="79616-130">You must use hello *-k* option tooprovide hello key-pair too*nsupdate* in order for hello Dynamic DNS update request toobe signed.</span></span>

<span data-ttu-id="79616-131">Если вы используете Windows DNS-сервер, можно использовать проверку подлинности Kerberos с hello *-g* параметр в *nsupdate* (недоступно в версии Windows hello *nsupdate* ).</span><span class="sxs-lookup"><span data-stu-id="79616-131">When you're using a Windows DNS server, you can use Kerberos authentication with hello *-g* parameter in *nsupdate* (not available in hello Windows version of *nsupdate*).</span></span> <span data-ttu-id="79616-132">toodo это, используйте *kinit* учетные данные hello tooload (например, из [файла keytab](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span><span class="sxs-lookup"><span data-stu-id="79616-132">toodo this, use *kinit* tooload hello credentials (e.g. from a [keytab file](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span></span> <span data-ttu-id="79616-133">Затем *nsupdate -g* получат hello учетные данные из кэша hello.</span><span class="sxs-lookup"><span data-stu-id="79616-133">Then *nsupdate -g* will pick up hello credentials from hello cache.</span></span>

<span data-ttu-id="79616-134">При необходимости можно добавить tooyour суффикс поиска DNS виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="79616-134">If needed, you can add a DNS search suffix tooyour VMs.</span></span> <span data-ttu-id="79616-135">Указанный DNS-суффикс Hello в hello */etc/resolv.conf* файла.</span><span class="sxs-lookup"><span data-stu-id="79616-135">hello DNS suffix is specified in hello */etc/resolv.conf* file.</span></span> <span data-ttu-id="79616-136">Большинство дистрибутивы Linux автоматически управлять hello содержимое этого файла, поэтому обычно нельзя редактировать.</span><span class="sxs-lookup"><span data-stu-id="79616-136">Most Linux distros automatically manage hello content of this file, so usually you can't edit it.</span></span> <span data-ttu-id="79616-137">Тем не менее, суффикс hello можно переопределить с помощью DHCP-клиента hello *заменяет* команды.</span><span class="sxs-lookup"><span data-stu-id="79616-137">However, you can override hello suffix by using hello DHCP client's *supersede* command.</span></span> <span data-ttu-id="79616-138">toodo это в */etc/dhcp/dhclient.conf*, добавить:</span><span class="sxs-lookup"><span data-stu-id="79616-138">toodo this, in */etc/dhcp/dhclient.conf*, add:</span></span>

        supersede domain-name <required-dns-suffix>;

