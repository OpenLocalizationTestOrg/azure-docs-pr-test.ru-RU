---
title: "Настройка параметров DNS в файле конфигурации службы | Документация Майкрософт"
description: "Настройка пользовательских параметров DNS с помощью файла конфигурации службы для виртуальной сети"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 467a4b99-8691-40b3-b640-e25e49675c71
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/24/2016
ms.author: jdial
ms.openlocfilehash: 0fba2ea06827aff29a7a092933edb8120d668b29
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a><span data-ttu-id="edf00-103">Настройка параметров DNS в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="edf00-103">Specifying DNS Settings in a Service Configuration File</span></span>
## <a name="dns-elements"></a><span data-ttu-id="edf00-104">Элементы DNS</span><span class="sxs-lookup"><span data-stu-id="edf00-104">DNS elements</span></span>
<span data-ttu-id="edf00-105">Файл конфигурации службы может содержать элемент DnsServers со списком IPv4-адресов для серверов доменных имен (DNS-серверов), которые будет использовать служба.</span><span class="sxs-lookup"><span data-stu-id="edf00-105">A service configuration file may contain a DnsServers element with a list of IPv4 addresses for the Domain Name System (DNS) servers that the service will use.</span></span> <span data-ttu-id="edf00-106">Параметры файла конфигурации службы имеют приоритет над параметрами файла конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="edf00-106">Settings in the service configuration file take precedence over settings in the network configuration file.</span></span> <span data-ttu-id="edf00-107">Дополнительные сведения см. в статье, посвященной [схеме конфигурации службы Azure (файл CSCFG)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="edf00-107">For more information, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span></span>

<span data-ttu-id="edf00-108">**Элемент NetworkConfiguration**</span><span class="sxs-lookup"><span data-stu-id="edf00-108">**NetworkConfiguration element**</span></span>

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> <span data-ttu-id="edf00-109">Атрибут **name** в элементе **DnsServer** используется только в качестве ссылочного имени.</span><span class="sxs-lookup"><span data-stu-id="edf00-109">The **name** attribute in the **DnsServer** element is used only as a reference name.</span></span> <span data-ttu-id="edf00-110">Он не представляет имя узла для DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="edf00-110">It does not represent the host name for the DNS server.</span></span> <span data-ttu-id="edf00-111">Каждое значение атрибута **DnsServer** должно быть уникальным во всей подписке Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="edf00-111">Each **DnsServer** attribute value must be unique across the entire Microsoft Azure subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="edf00-112">См. также</span><span class="sxs-lookup"><span data-stu-id="edf00-112">See Also</span></span>
[<span data-ttu-id="edf00-113">Схема конфигурации службы Azure (CSCFG-файл)</span><span class="sxs-lookup"><span data-stu-id="edf00-113">Azure Service Configuration Schema (.cscfg)</span></span>](https://msdn.microsoft.com/library/windowsazure/ee758710)

[<span data-ttu-id="edf00-114">Схема настройки виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="edf00-114">Azure Virtual Network Configuration Schema</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

[<span data-ttu-id="edf00-115">Настройка виртуальной сети с помощью файлов конфигурации сети</span><span class="sxs-lookup"><span data-stu-id="edf00-115">Configure a Virtual Network Using Network Configuration Files</span></span>](http://go.microsoft.com/fwlink/?LinkId=248094)

[<span data-ttu-id="edf00-116">Параметры виртуальной сети на портале управления</span><span class="sxs-lookup"><span data-stu-id="edf00-116">About Virtual Network settings in the Management Portal</span></span>](http://go.microsoft.com/fwlink/?LinkId=248092)

