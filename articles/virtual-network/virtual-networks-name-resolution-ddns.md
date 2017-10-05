---
title: "Использование динамических DNS для регистрации имен узлов"
description: "На этой странице приведены сведения о настройке динамических DNS для регистрации имен узлов на собственных DNS-серверах."
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
ms.openlocfilehash: 440a062e5fff73526b2d77d7d0a7c52ca72a66f1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="using-dynamic-dns-to-register-hostnames-in-your-own-dns-server"></a><span data-ttu-id="248e8-103">Использование динамических DNS для регистрации имен узлов на собственном DNS-сервере</span><span class="sxs-lookup"><span data-stu-id="248e8-103">Using Dynamic DNS to register hostnames in your own DNS server</span></span>
<span data-ttu-id="248e8-104">[Azure предоставляет разрешение имен](virtual-networks-name-resolution-for-vms-and-role-instances.md) для виртуальных машин и экземпляров ролей.</span><span class="sxs-lookup"><span data-stu-id="248e8-104">[Azure provides name resolution](virtual-networks-name-resolution-for-vms-and-role-instances.md) for virtual machines (VMs) and role instances.</span></span> <span data-ttu-id="248e8-105">Однако, если разрешение имен должно выходить за рамки возможностей Azure, вы можете предоставить свои DNS-серверы.</span><span class="sxs-lookup"><span data-stu-id="248e8-105">However, when your name resolution needs go beyond those provided by Azure, you can provide your own DNS servers.</span></span> <span data-ttu-id="248e8-106">В этом случае ваше решение DNS можно настроить в соответствии с конкретными потребностями.</span><span class="sxs-lookup"><span data-stu-id="248e8-106">This gives you the power to tailor your DNS solution to suit your own specific needs.</span></span> <span data-ttu-id="248e8-107">Например, вам может понадобиться доступ к локальным ресурсам через контроллер домена Active Directory.</span><span class="sxs-lookup"><span data-stu-id="248e8-107">For example, you may need to access on-premises resources via your Active Directory domain controller.</span></span>

<span data-ttu-id="248e8-108">Если пользовательские DNS-серверы размещены как виртуальные машины Azure, вы можете направлять запросы имени узла (в той же виртуальной сети) в Azure для разрешения имен узлов.</span><span class="sxs-lookup"><span data-stu-id="248e8-108">When your custom DNS servers are hosted as Azure VMs you can forward hostname queries for the same vnet to Azure to resolve hostnames.</span></span> <span data-ttu-id="248e8-109">Если вы не хотите использовать этот маршрут, можно зарегистрировать имена узлов своих виртуальных машин на DNS-сервере с помощью динамических DNS.</span><span class="sxs-lookup"><span data-stu-id="248e8-109">If you do not wish to use this route, you can register your VM hostnames in your DNS server using Dynamic DNS.</span></span>  <span data-ttu-id="248e8-110">Azure не может (не имеет учетных данных) регистрировать записи непосредственно на DNS-серверах, поэтому часто требуется прибегать к альтернативным вариантам.</span><span class="sxs-lookup"><span data-stu-id="248e8-110">Azure doesn't have the ability (e.g. credentials) to directly create records in your DNS servers, so alternative arrangements are often needed.</span></span> <span data-ttu-id="248e8-111">Ниже приведены некоторые распространенные сценарии и альтернативные варианты.</span><span class="sxs-lookup"><span data-stu-id="248e8-111">Here are some common scenarios with alternatives.</span></span>

## <a name="windows-clients"></a><span data-ttu-id="248e8-112">Клиенты Windows</span><span class="sxs-lookup"><span data-stu-id="248e8-112">Windows clients</span></span>
<span data-ttu-id="248e8-113">Не входящие в домен клиенты Windows пытаются выполнить небезопасные обновления динамических DNS (DDNS) при загрузке или изменении своего IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="248e8-113">Non-domain-joined Windows clients attempt unsecured Dynamic DNS (DDNS) updates when they boot or when their IP address changes.</span></span> <span data-ttu-id="248e8-114">DNS-именем является имя узла и основной DNS-суффикс.</span><span class="sxs-lookup"><span data-stu-id="248e8-114">The DNS name is the hostname plus the primary DNS suffix.</span></span> <span data-ttu-id="248e8-115">Azure оставляет основной DNS-суффикс пустым, но вы можете определить это на виртуальной машине с помощью [пользовательского интерфейса](https://technet.microsoft.com/library/cc794784.aspx) или [службы автоматизации](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span><span class="sxs-lookup"><span data-stu-id="248e8-115">Azure leaves the primary DNS suffix blank, but you can set this in the VM, via the [UI](https://technet.microsoft.com/library/cc794784.aspx) or [by using automation](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span></span>

<span data-ttu-id="248e8-116">Входящие в домен клиенты Windows регистрируют свои IP-адреса на контроллере домена, используя защищенные динамические DNS.</span><span class="sxs-lookup"><span data-stu-id="248e8-116">Domain-joined Windows clients register their IP addresses with the domain controller by using secure Dynamic DNS.</span></span> <span data-ttu-id="248e8-117">Процесс присоединения к домену задает основной DNS-суффикс на стороне клиента, создавая и поддерживая отношение доверия.</span><span class="sxs-lookup"><span data-stu-id="248e8-117">The domain-join process sets the primary DNS suffix on the client and creates and maintains the trust relationship.</span></span>

## <a name="linux-clients"></a><span data-ttu-id="248e8-118">Клиенты Linux</span><span class="sxs-lookup"><span data-stu-id="248e8-118">Linux clients</span></span>
<span data-ttu-id="248e8-119">Клиенты Linux обычно не регистрируются на DNS-сервере при запуске — предполагается, что это делает DHCP-сервер.</span><span class="sxs-lookup"><span data-stu-id="248e8-119">Linux clients generally don't register themselves with the DNS server on startup, they assume the DHCP server does it.</span></span> <span data-ttu-id="248e8-120">DHCP-серверы Azure не имеют возможности регистрировать записи на вашем DNS-сервере.</span><span class="sxs-lookup"><span data-stu-id="248e8-120">Azure's DHCP servers do not have the ability or credentials to register records in your DNS server.</span></span>  <span data-ttu-id="248e8-121">Для отправки обновлений динамических DNS можно использовать средство *nsupdate*, которое входит в пакет Bind.</span><span class="sxs-lookup"><span data-stu-id="248e8-121">You can use a tool called *nsupdate*, which is included in the Bind package, to send Dynamic DNS updates.</span></span> <span data-ttu-id="248e8-122">Так как протокол динамических DNS является стандартизованным, средство *nsupdate* можно применять даже в том случае, если Bind не используется на DNS-сервере.</span><span class="sxs-lookup"><span data-stu-id="248e8-122">Because the Dynamic DNS protocol is standardized, you can use *nsupdate* even when you're not using Bind on the DNS server.</span></span>

<span data-ttu-id="248e8-123">Чтобы создавать и поддерживать записи имени узла на DNS-сервере, можно использовать обработчики, предоставляемые DHCP-клиентом.</span><span class="sxs-lookup"><span data-stu-id="248e8-123">You can use the hooks that are provided by the DHCP client to create and maintain the hostname entry in the DNS server.</span></span> <span data-ttu-id="248e8-124">Во время цикла DHCP клиент выполняет скрипты в расположении */etc/dhcp/dhclient-exit-hooks.d/*.</span><span class="sxs-lookup"><span data-stu-id="248e8-124">During the DHCP cycle, the client executes the scripts in */etc/dhcp/dhclient-exit-hooks.d/*.</span></span> <span data-ttu-id="248e8-125">Это можно использовать для регистрации нового IP-адреса с помощью *nsupdate*.</span><span class="sxs-lookup"><span data-stu-id="248e8-125">This can be used to register the new IP address by using *nsupdate*.</span></span> <span data-ttu-id="248e8-126">Например:</span><span class="sxs-lookup"><span data-stu-id="248e8-126">For example:</span></span>

        #!/bin/sh
        requireddomain=mydomain.local

        # only execute on the primary nic
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

        
        

<span data-ttu-id="248e8-127">Для выполнения безопасных обновлений динамических DNS можно также использовать команду *nsupdate* .</span><span class="sxs-lookup"><span data-stu-id="248e8-127">You can also use the *nsupdate* command to perform secure Dynamic DNS updates.</span></span> <span data-ttu-id="248e8-128">Например, при использовании DNS-сервера Bind [создается](http://linux.yyz.us/nsupdate/)пара открытого и закрытого ключей.</span><span class="sxs-lookup"><span data-stu-id="248e8-128">For example, when you're using a Bind DNS server, a public-private key pair is [generated](http://linux.yyz.us/nsupdate/).</span></span>  <span data-ttu-id="248e8-129">DNS-сервер [настраивается](http://linux.yyz.us/dns/ddns-server.html) с использованием открытой части ключа, что делает возможным проверку подписи запроса.</span><span class="sxs-lookup"><span data-stu-id="248e8-129">The DNS server is [configured](http://linux.yyz.us/dns/ddns-server.html) with the public part of the key so that it can verify the signature on the request.</span></span> <span data-ttu-id="248e8-130">Чтобы подписать запрос на обновление динамических DNS, в средстве *nsupdate* необходимо указать пару ключей с помощью параметра *-k*.</span><span class="sxs-lookup"><span data-stu-id="248e8-130">You must use the *-k* option to provide the key-pair to *nsupdate* in order for the Dynamic DNS update request to be signed.</span></span>

<span data-ttu-id="248e8-131">При использовании DNS-сервера Windows в *nsupdate* можно выполнять проверку подлинности Kerberos с параметром *-g* (недоступно в версии средства *nsupdate* для Windows).</span><span class="sxs-lookup"><span data-stu-id="248e8-131">When you're using a Windows DNS server, you can use Kerberos authentication with the *-g* parameter in *nsupdate* (not available in the Windows version of *nsupdate*).</span></span> <span data-ttu-id="248e8-132">Для этого используйте команду *kinit* , чтобы скачать учетные данные (например, из [файла keytab](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span><span class="sxs-lookup"><span data-stu-id="248e8-132">To do this, use *kinit* to load the credentials (e.g. from a [keytab file](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span></span> <span data-ttu-id="248e8-133">Затем выполните команду *nsupdate -g* , чтобы получить учетные данные из кэша.</span><span class="sxs-lookup"><span data-stu-id="248e8-133">Then *nsupdate -g* will pick up the credentials from the cache.</span></span>

<span data-ttu-id="248e8-134">При необходимости в виртуальные машины можно добавить суффикс поиска DNS.</span><span class="sxs-lookup"><span data-stu-id="248e8-134">If needed, you can add a DNS search suffix to your VMs.</span></span> <span data-ttu-id="248e8-135">DNS-суффикс указан в файле */etc/resolv.conf* .</span><span class="sxs-lookup"><span data-stu-id="248e8-135">The DNS suffix is specified in the */etc/resolv.conf* file.</span></span> <span data-ttu-id="248e8-136">Большинство дистрибутивов Linux управляет содержимым этого файла автоматически, поэтому его обычно нельзя изменить.</span><span class="sxs-lookup"><span data-stu-id="248e8-136">Most Linux distros automatically manage the content of this file, so usually you can't edit it.</span></span> <span data-ttu-id="248e8-137">Тем не менее, вы можете переопределить суффикс с помощью команды *supersede* DHCP-клиента.</span><span class="sxs-lookup"><span data-stu-id="248e8-137">However, you can override the suffix by using the DHCP client's *supersede* command.</span></span> <span data-ttu-id="248e8-138">Для этого в файле */etc/dhcp/dhclient.conf*добавьте:</span><span class="sxs-lookup"><span data-stu-id="248e8-138">To do this, in */etc/dhcp/dhclient.conf*, add:</span></span>

        supersede domain-name <required-dns-suffix>;

