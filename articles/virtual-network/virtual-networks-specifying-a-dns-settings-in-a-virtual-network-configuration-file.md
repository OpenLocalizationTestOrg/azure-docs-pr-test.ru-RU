---
title: "Параметры DNS в файле конфигурации виртуальной сети aaaSpecifying | Документы Microsoft"
description: "Как файл toochange параметры DNS-сервера в виртуальной сети, используя конфигурацию виртуальной сети в hello классической модели развертывания"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a8905927-92ac-42b5-8c33-8e42c000692c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: d53a658773e1c930b5a28a701db0be9edd26565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a><span data-ttu-id="63b39-103">Задание параметров DNS в файле конфигурации виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="63b39-103">Specifying DNS settings in a virtual network configuration file</span></span>
<span data-ttu-id="63b39-104">Файл конфигурации сети состоит из двух элементов, можно использовать параметры системы доменных имен (DNS) toospecify: **DnsServers** и **DnsServerRef**.</span><span class="sxs-lookup"><span data-stu-id="63b39-104">A network configuration file has two elements that you can use toospecify Domain Name System (DNS) settings: **DnsServers** and **DnsServerRef**.</span></span> <span data-ttu-id="63b39-105">Можно добавить список DNS-серверов, указав их IP-адреса и ссылаться на имена toohello **DnsServers** элемента.</span><span class="sxs-lookup"><span data-stu-id="63b39-105">You can add a list of DNS servers by specifying their IP addresses and reference names toohello **DnsServers** element.</span></span> <span data-ttu-id="63b39-106">Затем можно использовать **DnsServerRef** toospecify элемент, какие записи DNS-сервера из элемент DnsServers hello используются для различных сетевых сайтов в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="63b39-106">You can then use a **DnsServerRef** element toospecify which DNS server entries from hello DnsServers element are used for different network sites within your virtual network.</span></span>

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="63b39-107">В этой статье рассматриваются hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="63b39-107">This article covers hello classic deployment model.</span></span>

<span data-ttu-id="63b39-108">файл конфигурации сети Hello может содержать следующие элементы hello.</span><span class="sxs-lookup"><span data-stu-id="63b39-108">hello network configuration file may contain hello following elements.</span></span> <span data-ttu-id="63b39-109">Hello Заголовок каждого элемента является связанного tooa, предоставляющий дополнительные сведения об элементе hello значения параметров.</span><span class="sxs-lookup"><span data-stu-id="63b39-109">hello title of each element is linked tooa page that provides additional information about hello element value settings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="63b39-110">Сведения о как tooconfigure hello файла конфигурации сети см. в разделе [настройки виртуальной сети с помощью файла конфигурации сети](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="63b39-110">For information about how tooconfigure hello network configuration file, see [Configure a Virtual Network Using a Network Configuration File](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="63b39-111">Сведения о каждом элементе, содержащемся в файле конфигурации сети hello см. в разделе [схема конфигурации виртуальной сети Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="63b39-111">For information about each element contained in hello network configuration file, see [Azure Virtual Network Configuration Schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
> 
> 

[<span data-ttu-id="63b39-112">Элемент DNS</span><span class="sxs-lookup"><span data-stu-id="63b39-112">Dns Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> <span data-ttu-id="63b39-113">Hello **имя** атрибута в hello **DnsServer** элемент используется только в качестве ссылки для hello **DnsServerRef** элемента.</span><span class="sxs-lookup"><span data-stu-id="63b39-113">hello **name** attribute in hello **DnsServer** element is used only as a reference for hello **DnsServerRef** element.</span></span> <span data-ttu-id="63b39-114">Он не представляет имя узла hello hello DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="63b39-114">It does not represent hello host name for hello DNS server.</span></span> <span data-ttu-id="63b39-115">Каждый **DnsServer** значение атрибута должно быть уникальным для всей подписки Microsoft Azure hello</span><span class="sxs-lookup"><span data-stu-id="63b39-115">Each **DnsServer** attribute value must be unique across hello entire Microsoft Azure subscription</span></span>
> 
> 

[<span data-ttu-id="63b39-116">Элемент Virtual Network Sites</span><span class="sxs-lookup"><span data-stu-id="63b39-116">Virtual Network Sites Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> <span data-ttu-id="63b39-117">Чтобы toospecify этот параметр для элемента Virtual Network Sites hello, должен быть предварительно определен в элементе DNS hello.</span><span class="sxs-lookup"><span data-stu-id="63b39-117">In order toospecify this setting for hello Virtual Network Sites element, it must be previously defined in hello DNS element.</span></span> <span data-ttu-id="63b39-118">Hello DnsServerRef *имя* в hello сайтов виртуальной сети должен ссылаться tooa имя значение, указанное в элементе hello DNS для DNS-сервер *имя*.</span><span class="sxs-lookup"><span data-stu-id="63b39-118">hello DnsServerRef *name* in hello Virtual Network Sites element must refer tooa name value specified in hello DNS element for DnsServer *name*.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="63b39-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="63b39-119">Next steps</span></span>
* <span data-ttu-id="63b39-120">Понимать hello [схема конфигурации виртуальной сети Azure](http://go.microsoft.com/fwlink/?LinkId=248093).</span><span class="sxs-lookup"><span data-stu-id="63b39-120">Understand hello [Azure Virtual Network Configuration Schema](http://go.microsoft.com/fwlink/?LinkId=248093).</span></span>
* <span data-ttu-id="63b39-121">Понимать hello [схема конфигурации службы Azure](https://msdn.microsoft.com/library/windowsazure/ee758710).</span><span class="sxs-lookup"><span data-stu-id="63b39-121">Understand hello [Azure Service Configuration Schema](https://msdn.microsoft.com/library/windowsazure/ee758710).</span></span>
* <span data-ttu-id="63b39-122">[Настройка виртуальной сети с помощью файлов конфигурации сети](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="63b39-122">[Configure a virtual network using Network configuration files](virtual-networks-using-network-configuration-file.md).</span></span>

