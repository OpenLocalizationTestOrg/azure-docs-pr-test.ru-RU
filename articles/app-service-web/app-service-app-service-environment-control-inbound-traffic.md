---
title: "aaaHow tooControl входящий трафик tooan среды службы приложений"
description: "Узнайте, как toocontrol правила безопасности сети tooconfigure входящего трафика tooan среды службы приложений."
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: 
ms.assetid: 4cc82439-8791-48a4-9485-de6d8e1d1a08
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: stefsch
ms.openlocfilehash: e7c6e6201db6a1ea77f7a2eee29a3b5445175495
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocontrol-inbound-traffic-tooan-app-service-environment"></a>Как tooan tooControl входящий трафик среды службы приложений
## <a name="overview"></a>Обзор
Среду службы приложений можно создать **либо** в виртуальной сети Azure Resource Manager, **либо** в [виртуальной сети][virtualnetwork], использующей классическую модель развертывания.  Во время hello при создании среды службы приложений можно определить новую виртуальную сеть и подсеть.  Кроме того, среду службы приложений можно создать в существующих виртуальной сети и подсети.  В связи с изменением от июня 2016 г. среды ASE можно также развертывать в виртуальных сетях, использующих либо диапазоны общедоступных адресов, либо адресные пространства RFC1918 (т. е. частные адреса).  Дополнительные сведения о создании среды службы приложений см. в разделе [как tooCreate среды службы приложений][HowToCreateAnAppServiceEnvironment].

Среды службы приложений всегда создаются в одной подсети, так как подсеть предоставляет границы сети, который можно использовать toolock вниз входящий трафик за вышестоящего устройств и служб таким образом, что трафик HTTP и HTTPS принимается только от конкретных вышестоящего IP-адреса.

Входящий и исходящий сетевой трафик в подсети контролируется с помощью [группы сетевой безопасности][NetworkSecurityGroups]. Входящий трафик управления требует создания правил безопасности сети в группе безопасности сети, а затем добавляют hello сетевой безопасности группы hello подсети содержащего hello среды службы приложений.

После назначения подсети tooa группы безопасности сети, tooapps входящий трафик в приветствия среды службы приложений, разрешены или заблокированы исходя из hello разрешать и запрещать правила, определенные в группы безопасности сети hello.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="inbound-network-ports-used-in-an-app-service-environment"></a>Входящие сетевые порты, используемые в среде службы приложений
Перед блокировкой вниз входящий сетевой трафик с сетевой группой безопасности, это важные tooknow hello набор обязательных и необязательных сетевые порты, используемые в среде службы приложений.  Случайное закрытие отключение портов toosome трафика может привести к потере функциональности в среде службы приложений.

Hello ниже приведен список портов, используемых в среде службы приложений. Это все **TCP**-порты, если явно не указано иное.

* 454: **обязательный порт**, используемый инфраструктурой Azure для обслуживания сред службы приложений и управления ими через SSL.  Не блокируют трафик toothis порта.  Этот порт всегда является привязанной toohello открытый виртуальный IP-адрес ASE.
* 455: **обязательный порт**, используемый инфраструктурой Azure для обслуживания сред службы приложений и управления ими через SSL.  Не блокируют трафик toothis порта.  Этот порт всегда является привязанной toohello открытый виртуальный IP-адрес ASE.
* 80: порт для входящего трафика HTTP tooapps, работающих в планах обслуживания приложения в среде службы приложений по умолчанию.  ASE ILB включена этот порт является адрес ILB привязанного toohello hello ASE.
* 443: порт для входящего трафика tooapps SSL, работающих в планах обслуживания приложения в среде службы приложений по умолчанию.  ASE ILB включена этот порт является адрес ILB привязанного toohello hello ASE.
* 21: канал управления для FTP.  Этот порт можно безопасно заблокировано, если FTP не используется.  На ASE ILB включена этот порт может быть адрес ILB привязанного toohello ASE.
* 990: канал управления для FTPS.  Этот порт можно благополучно заблокировать, если не используется FTPS.  На ASE ILB включена этот порт может быть адрес ILB привязанного toohello ASE.
* 10001 10020: каналы данных для FTP.  Как канал управления hello, то эти порты безопасно заблокированы, если не используется FTP.  На ASE ILB включена этот порт может быть адрес ILB привязанного toohello ASE элемента.
* 4016: используется для удаленной отладки с помощью Visual Studio 2012.  Этот порт может безопасно заблокировано, если не используется функция hello.  ASE ILB включена этот порт является адрес ILB привязанного toohello hello ASE.
* 4018: используется для удаленной отладки с помощью Visual Studio 2013.  Этот порт может безопасно заблокировано, если не используется функция hello.  ASE ILB включена этот порт является адрес ILB привязанного toohello hello ASE.
* 4020: используется для удаленной отладки с помощью Visual Studio 2015.  Этот порт может безопасно заблокировано, если не используется функция hello.  ASE ILB включена этот порт является адрес ILB привязанного toohello hello ASE.

## <a name="outbound-connectivity-and-dns-requirements"></a>Требования к DNS и исходящим подключениям
Для среды службы приложений toofunction правильно, необходимо также конечные точки toovarious исходящий доступ. Полный список hello внешних конечных точек, используемых ASE представлен в hello раздел «Требуется сетевое подключение» hello [конфигурацию сети для ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) статьи.

Среды службы приложений требуется допустимый инфраструктура DNS настроен для hello виртуальной сети.  Если для любого hello причина будет изменена конфигурация DNS после создания среды службы приложений, разработчики можно принудительно toopick среды службы приложения hello новой конфигурации DNS.  Последовательное среды перезагрузку, используя значок «Перезапуск» hello hello верхней части колонки управления hello среды службы приложений в hello [портал Azure] [ NewPortal] вызовет toopick среды hello копирование hello новую конфигурацию DNS.

Также рекомендуется обеспечить пользовательские DNS-серверы в виртуальной сети hello установки опережает время предыдущего toocreating среды службы приложений.  При создании среды службы приложений при изменении конфигурации DNS виртуальной сети, приведет к сбой процесса создания среды службы приложений hello.  Если существует пользовательского DNS-сервера на приветствия другом конце VPN-шлюза и DNS-сервер hello в аналогичные вена, является hello недоступен или недоступен, произойдет сбой процесса создания среды службы приложений.

## <a name="creating-a-network-security-group"></a>Создание группы сетевой безопасности
Подробные сведения о том, как действия группы безопасности сети см. в разделе ниже hello [сведения][NetworkSecurityGroups].  Пример управления службами Azure Hello ниже штрихи на выделяет групп безопасности сети, имеющий фокус по настройке и применению подсети tooa сетевой безопасности группы, содержащей среды службы приложений.

**Примечание:** сетевых групп безопасности можно настроить графически при помощи hello [портала Azure](https://portal.azure.com) или с помощью Azure PowerShell.

Сначала группы сетевой безопасности создаются как отдельные сущности, связанные с подпиской. Создания групп безопасности сети в регионе Azure убедитесь в эту группу безопасности сети hello создается в hello же региона, как hello среды службы приложений.

Hello следующий код демонстрирует создание группы безопасности сети:

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

После создания группы безопасности сети в одно или несколько правил безопасности сети добавляются tooit.  Поскольку hello набор правил может изменяться со временем, рекомендуется toospace out hello схема нумерации, используемый для toomake правило приоритеты его легко tooinsert Дополнительные правила со временем.

Hello ниже примере правила, которое явным образом предоставляет порты доступа для управления toohello Затребован toomanage hello инфраструктуры Azure и поддерживать среды службы приложений.  Обратите внимание, что весь трафик управления передаются по протоколу SSL и защищен клиентских сертификатов, поэтому несмотря на то, что открыты порты hello они недоступны для любой сущности, отличные от инфраструктуры управления Azure.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP


Если блокировка доступа tooport 80 и 443 слишком «скрыть» среды службы приложений за вышестоящего устройства или службы, вы должны будете tooknow hello вышестоящего IP-адрес.  Например, если вы используете брандмауэр веб-приложения (WAF), hello WAF будет иметь собственный IP-адрес (или адреса) который наблюдают использует перенаправление трафика tooa подчиненных среды службы приложений.  Вам потребуется toouse этот IP-адрес в hello *SourceAddressPrefix* параметр правила безопасности сети.

В следующем примере hello явно разрешенные входящего трафика из конкретного вышестоящего IP-адреса.  Здравствуйте, адрес *1.2.3.4* используется как заполнитель для вышестоящего WAF hello IP-адрес.  Изменить hello toomatch значение hello адрес, используемый вышестоящего устройства или службы.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT HTTP" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT HTTPS" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Если требуется поддержка FTP, hello правил может использоваться как порт управления FTP toohello шаблона toogrant доступа и портов канала данных.  Поскольку FTP — это протокол, с отслеживанием состояния, не могут быть трафик может tooroute FTP через традиционные устройства брандмауэра или прокси-сервера HTTP или HTTPS.  В этом случае вам потребуется tooset hello *SourceAddressPrefix* tooa другое значение — например hello IP адресов машин разработчик или развертывания, на какие FTP клиенты работают под управлением. 

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT FTPCtrl" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '21' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT FTPDataRange" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '10001-10020' -Protocol TCP

(**Примечание:** диапазон портов канала данных hello может измениться в период предварительного просмотра hello.)

При использовании удаленной отладки в Visual Studio hello правилам показывают, как доступ к toogrant.  Существует отдельное правило для каждой поддерживаемой версии Visual Studio, поскольку каждая версия использует другой порт для удаленной отладки.  Как и для FTP-доступа, трафик удаленной отладки не может правильно проходить через традиционный брандмауэр WAF или прокси-устройство.  Hello *SourceAddressPrefix* можно задать диапазон IP-адресов toohello машин разработчика Visual Studio.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2012" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4016' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2013" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4018' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2015" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4020' -Protocol TCP

## <a name="assigning-a-network-security-group-tooa-subnet"></a>Назначение группы безопасности сети tooa подсети
Группа безопасности сети имеет правило безопасности по умолчанию, которое запрещает доступ tooall внешнего трафика.  Здравствуйте, в результате объединения правил безопасности сети hello, описанной выше и Здравствуйте правило безопасности по умолчанию блокирует входящий трафик, что только трафик из диапазонов адресов источника связан с *Разрешить* смогут действия tooapps toosend трафика, работающих в среде службы приложений.

После заполнения группы безопасности сети с правилами безопасности ему назначены toobe toohello подсети, где hello среды службы приложений.  Команда назначения Hello ссылается обоих имя hello hello виртуальной сети, где находится hello среды службы приложений, а также имя hello hello подсети, где был создан hello среды службы приложений.  

Hello ниже примере сетевой группы безопасности, присваиваемого tooa подсети и виртуальной сети:

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-test'

После успешного выполнения Назначение группы безопасности сети hello (hello назначения длительные операции и может занять несколько минут toocomplete), только входящий трафик сопоставления *Разрешить* правила успешно достигнет приложения в приложение hello Среда службы.

Для полноты hello следующем примере показано, как группировать tooremove и, следовательно, несвязанные сопоставление hello сетевой безопасности из подсети hello:

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Remove-AzureNetworkSecurityGroupFromSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-test'

## <a name="special-considerations-for-explicit-ip-ssl"></a>Специальные рекомендации для SSL на основе явного IP
Если приложение настроено с явную SSL на ОСНОВЕ IP-адресом (применимо *только* tooASEs, имеющий открытый виртуальный IP-адрес), вместо того чтобы использовать IP-адрес по умолчанию hello hello среды службы приложений, HTTP и HTTPS-трафик потоков в подсети hello над набором порты, отличные от порты 80 и 443.

Hello отдельные пары порты, используемые каждого SSL на ОСНОВЕ IP-адреса можно найти в hello пользовательского интерфейса портала из колонки UX сведения среды для hello приложения службы.  Выберите "Все параметры" > "IP-адреса".  Колонка Hello «IP-адреса» показана таблица, все явно настроен SSL на ОСНОВЕ IP-адресов для hello среды службы приложений, вместе с парой особого порта hello, которая используется tooroute трафик HTTP и HTTPS, связанный с каждого SSL на ОСНОВЕ IP-адреса.  Это Эта пара порта, который должен использовать hello DestinationPortRange параметров при настройке правила в группе безопасности сети toobe.

Когда приложения на ASE настроенных toouse SSL на ОСНОВЕ IP, внешних клиентов не будут видеть и не обязательно tooworry о сопоставлении пары hello особого порта.  Приложения toohello трафик будет передаваться обычно toohello настроить SSL на ОСНОВЕ IP адрес.  Пара особого порта toohello перевод Hello автоматически происходит внутренним образом во время hello заключительный сегмент маршрутизации трафика в hello ASE содержащего подсеть hello. 

## <a name="getting-started"></a>Приступая к работе
tooget к работе с среды службы приложения, в разделе [tooApp введение среды службы][IntroToAppServiceEnvironment]

Все статьи и как-для пользователя для среды службы приложений теперь доступны в hello [файл README для среды службы приложения](../app-service/app-service-app-service-environments-readme.md).

Дополнительные сведения о приложениях безопасного соединения toobackend ресурсов из среды службы приложений см. в разделе [безопасного соединения tooBackend ресурсов из среды службы приложений][SecurelyConnecttoBackend]

Дополнительные сведения о платформе hello службе приложений Azure см. в разделе [службе приложений Azure][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[SecurelyConnecttoBackend]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NewPortal]:  https://portal.azure.com  

<!-- IMAGES -->

