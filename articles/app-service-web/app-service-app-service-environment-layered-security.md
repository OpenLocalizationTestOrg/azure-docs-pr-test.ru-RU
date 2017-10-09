---
title: "aaaLayered архитектура безопасности с помощью среды службы приложений"
description: "Реализация многоуровневой архитектуры безопасности в средах службы приложений."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 73ce0213-bd3e-4876-b1ed-5ecad4ad5601
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: stefsch
ms.openlocfilehash: 0627ba6fa849908506fe62c451c888c147cabc03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a>Реализация многоуровневой архитектуры безопасности со средами службы приложений
## <a name="overview"></a>Обзор
Среды службы приложений предоставляют изолированную среду выполнения, развернутую в виртуальной сети. Поэтому разработчики могут создавать многоуровневую архитектуру безопасности, предусматривающую разные уровни доступа к сети для каждого физического уровня приложений.

Общие желания toohide API назад интерфейсов из общего доступа к Интернету и только позволяет toobe API-интерфейсы, вызванных вышестоящего веб-приложений.  [Сетевые группы безопасности (Nsg)] [ NetworkSecurityGroups] может использоваться в подсетях, содержащую приложения tooAPI общего доступа toorestrict среды службы приложения.

Hello приведенной ниже схеме показана архитектура примера с управлением WebAPI приложение, развернутое в среде службы приложений.  Три экземпляра приложения Интернета отдельно, развернутый на три отдельные среды службы приложения, сделать вызовы внутренней toohello же WebAPI приложения.

![Концепция архитектуры][ConceptualArchitecture] 

Hello зеленый плюс указывают, hello сетевой группы безопасности в подсети hello, содержащая «apiase» позволяет входящих вызовов из hello вышестоящего веб-приложений, как хорошо вызовы от самого себя.  Однако hello явно отказывает в одной группе безопасности сети, доступ к toogeneral входящего трафика из Интернета hello. 

Hello оставшейся части этой статьи рассматриваются hello действия необходимые tooconfigure hello сетевой группы безопасности в подсети hello, содержащая «apiase».

## <a name="determining-hello-network-behavior"></a>Определение hello неполадки в сети
В порядке tooknow необходимости правила безопасности сети необходимо toodetermine, какие клиенты сети может tooreach среды службы приложений содержащего hello API приложение hello и какие клиенты будут заблокированы.

Так как [сетевых групп безопасности (Nsg)] [ NetworkSecurityGroups] , примененные toosubnets и развертываются среды службы приложения в подсетях, применяются правила hello, содержащихся в NSG слишком**все** приложения, работающие в среде службы приложений.  С помощью hello образец архитектуры для данной статьи после группы безопасности сети применяется toohello подсети, где «apiase», все приложения, работающие на hello «apiase» среды службы приложений будет защищен hello же набор правил безопасности. 

* **Определить hello исходящий IP-адрес вышестоящего вызывающим объектам:** возможности hello IP-адреса вышестоящего hello вызывающих объектов?  Эти адреса должны явно разрешен доступ в hello NSG toobe.  Поскольку вызовы между среды службы приложения считаются вызовы «Internet», это означает hello исходящих IP-адреса, назначенного tooeach из hello три вышестоящего среды службы приложения требованиям toobe доступ разрешен в hello NSG для подсети «apiase» hello.   Дополнительные сведения об определении hello исходящий IP-адрес приложения, выполняющиеся в среде службы приложений см. в разделе hello [архитектура сети] [ NetworkArchitecture] обзорную статью.
* **Потребуется ли API приложение hello серверной части toocall сам?**  Иногда уделяется недостаточно внимания и неявные точки встречается hello целей toocall самого внутреннего приложения hello.  Если в приложении API серверной части в среде службы приложений требуются toocall сам, это также обрабатываются как вызов «Интернет».  В образец hello архитектуры для этого требуются доступ hello исходящий IP-адрес «apiase» среды службы приложений также hello.

## <a name="setting-up-hello-network-security-group"></a>Настройка hello группы безопасности сети
После набора hello известны исходящий IP-адресов, hello следующим шагом является tooconstruct группы безопасности сети.  Группы безопасности сети можно создавать и для виртуальных сетей с Resource Manager, и для классических виртуальных сетей.  Hello ниже примерах Создание и настройка NSG в классической виртуальной сети с помощью Powershell.

Для архитектуры образец hello средах hello находятся в США, так что в этом регионе создается пустой NSG:

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

Сначала явно разрешить добавлено правило для hello инфраструктуры управления Azure, описанных в статье hello на [входящий трафик] [ InboundTraffic] для среды службы приложения.

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

После этого два правила будут добавлены tooallow HTTP и HTTPS вызовы из hello первый вышестоящего среды службы приложений («fe1ase»).

    #Grant access toorequests from hello first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Здравствуйте, снова и повторите эти действия для второго и третьего вышестоящего приложения среды службы («fe2ase» и «fe3ase»).

    #Grant access toorequests from hello second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access toorequests from hello third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Наконец предоставьте доступ toohello исходящих IP-адрес внутреннего интерфейса API hello среды службы приложений, чтобы он может выполнять обратный вызов в саму себя.

    #Allow apps on hello apiase environment toocall back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Нет правил безопасности сети должны toobe настроен по умолчанию, поскольку каждый NSG имеет набор правил по умолчанию, блокирующие доступ входящего трафика из Интернета hello.

Ниже приведены Hello полный список правил в группе безопасности сети hello.  Обратите внимание на то, как hello последнего правило, которое выделяется, блокирует доступ входящего трафика от всех вызывающих объектов, отличных от тех, которые явным образом предоставлен доступ.

![Конфигурация NSG][NSGConfiguration] 

последним шагом Hello является toohello подсети tooapply hello NSG, которая содержит apiase «hello» среды службы приложений.  

     #Apply hello NSG toohello backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

С подсетью toohello hello NSG применяется только hello три вышестоящего среды службы приложения hello содержащего hello среды службы приложений API серверной части, разрешены и toocall в среду «apiase» hello.

## <a name="additional-links-and-information"></a>Дополнительные ссылки и сведения
Все статьи и как-для пользователя для среды службы приложений теперь доступны в hello [файл README для среды службы приложения](../app-service/app-service-app-service-environments-readme.md).

Информация о [группах безопасности сети](../virtual-network/virtual-networks-nsg.md). 

Основные сведения об [исходящих IP-адресах][NetworkArchitecture] и средах службы приложений.

[Сетевые порты][InboundTraffic], используемые в средах службы приложений.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
