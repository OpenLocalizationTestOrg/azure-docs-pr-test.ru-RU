---
title: "Подключение aaaSecurely tooBackEnd ресурсов из среды службы приложений"
description: "Дополнительные сведения о подключении ресурсы toobackend toosecurely из среды службы приложений."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: f82eb283-a6e7-4923-a00b-4b4ccf7c4b5b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 6311d3fc301512ea3c4ed8f14f268f75755aa415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="securely-connecting-toobackend-resources-from-an-app-service-environment"></a>Безопасное подключение tooBackend ресурсов из среды службы приложений
## <a name="overview"></a>Обзор
Поскольку всегда создается в среде службы приложений **либо** виртуальной сетью Azure Resource Manager **или** классической модели развертывания [виртуальной сети] [ virtualnetwork], могут передавать исходящие подключения из среды службы приложений tooother внутренних ресурсов исключительно через hello виртуальной сети.  В связи с последним изменением от июня 2016 г. среды ASE можно также развертывать в виртуальных сетях, использующих либо диапазоны общедоступных адресов, либо адресные пространства RFC1918 (т. е. частные адреса).  

Например, SQL Server может работать в кластере виртуальных машин с заблокированным портом 1433.  Hello конечная точка может быть ACLd tooonly разрешения доступа от других ресурсов на hello одной виртуальной сети.  

Еще один пример, конфиденциальные конечные точки могут и локально и быть подключенным tooAzure через либо [сайт-сайт] [ SiteToSite] или [Azure ExpressRoute] [ ExpressRoute] подключений.  В результате только ресурсов в виртуальные сети подключены toohello сайт-сайт или ExpressRoute туннели будут конечными точками в локальной среде может tooaccess.

Для всех этих сценариях приложений, выполняемых в среде службы приложений будет может toosecurely подключения toohello различные серверы и ресурсы.  Исходящий трафик из приложения, выполняющиеся в среде службы приложений tooprivate конечных точек в hello одной виртуальной сети (или подключенных toohello одной виртуальной сети), будут только поток hello виртуальной сети.  Исходящий трафик tooprivate, конечные точки не будет передаваться через hello общедоступный Интернет.

Один нюанс применяется toooutbound трафика от tooendpoints среды службы приложений в виртуальной сети.  Среды службы приложения не могут достичь конечных точек виртуальных машин, размещенных в hello **же** подсети как hello среды службы приложений.  Это обычно не должна быть проблемой при условии, что среды службы приложений, развернутых в подсети, зарезервированные для монопольного использования только hello среды службы приложений.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a>Требования к DNS и исходящим подключениям
Надлежащим образом, для среды службы приложений toofunction требуются конечные точки toovarious исходящий доступ. Полный список hello внешних конечных точек, используемых ASE представлен в hello раздел «Требуется сетевое подключение» hello [конфигурацию сети для ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) статьи.

Среды службы приложений требуется допустимый инфраструктура DNS настроен для hello виртуальной сети.  Если для любого hello причина будет изменена конфигурация DNS после создания среды службы приложений, разработчики можно принудительно toopick среды службы приложения hello новой конфигурации DNS.  Последовательное среды перезагрузку, используя значок «Перезапуск» hello, расположенный вверху hello hello среды службы приложений колонке управления hello портала приведет к toopick среды hello hello новой конфигурации DNS.

Также рекомендуется обеспечить пользовательские DNS-серверы в виртуальной сети hello установки опережает время предыдущего toocreating среды службы приложений.  При создании среды службы приложений при изменении конфигурации DNS виртуальной сети, приведет к сбой процесса создания среды службы приложений hello.  Если существует пользовательского DNS-сервера на приветствия другом конце VPN-шлюза и DNS-сервер hello в аналогичные вена, является hello недоступен или недоступен, произойдет сбой процесса создания среды службы приложений.

## <a name="connecting-tooa-sql-server"></a>Подключение tooa SQL Server
В типичной конфигурации SQL Server конечная точка прослушивает порт 1433:

![Конечная точка сервера SQL Server][SqlServerEndpoint]

Существует два подхода для ограничения трафика toothis endpoint:

* [Сетевые списки управления доступом][NetworkAccessControlLists] (сетевые ACL).
* [Группы безопасности сети][NetworkSecurityGroups].

## <a name="restricting-access-with-a-network-acl"></a>Ограничение доступа с помощью сетевых списков управления доступом
Порт 1433 можно защитить с помощью сетевого списка управления доступом.  пример Hello ниже запрещенного клиента адреса, исходящих от внутри виртуальной сети и блокирует доступ tooall других клиентов.

![Пример сетевого списка управления доступом][NetworkAccessControlListExample]

Hello всем приложениям, выполняющимся в среде службы приложений в одной виртуальной сети, как hello SQL Server будет может tooconnect toohello экземпляром SQL Server hello **внутренней виртуальной сети** IP-адрес для виртуальной машины SQL Server hello.  

Пример строки подключения Hello ниже ссылки hello SQL Server, используя свой закрытый IP-адрес.

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

Несмотря на то, что виртуальная машина hello содержит также общедоступную конечную точку, попытки подключения с помощью hello общедоступный IP-адрес, будут отклонены из-за hello управления сетевым Доступом. 

## <a name="restricting-access-with-a-network-security-group"></a>Ограничение доступа с помощью группы сетевой безопасности
Альтернативный подход для обеспечения безопасного доступа заключается в использовании группы сетевой безопасности.  Сетевые группы безопасности может быть применен tooindividual виртуальных машин или tooa подсети, содержащие виртуальные машины.

Сначала сетевую группу безопасности требуется toobe создан:

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

Ограничение доступа tooonly внутренний трафик виртуальной сети является очень простым с сетевой группой безопасности.  правила по умолчанию Hello в группу безопасности сети только разрешить доступ из других сетевых клиентов в hello одной виртуальной сети.

В результате блокирования доступа tooSQL сервера заключается в применении группы безопасности сети с его по умолчанию правила tooeither hello виртуальные машины под управлением SQL Server или подсети hello, содержащие виртуальные машины hello.

Образец Hello ниже применяется безопасности группы toohello содержащего подсети:

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

Hello конечным результатом является набор правил безопасности, блокирующие внешний доступ, предоставляя внутреннего доступа виртуальной сети:

![Правила сетевой безопасности по умолчанию][DefaultNetworkSecurityRules]

## <a name="getting-started"></a>Приступая к работе
Все статьи и как-для пользователя для среды службы приложений теперь доступны в hello [файл README для среды службы приложения](../app-service/app-service-app-service-environments-readme.md).

tooget к работе с среды службы приложения, в разделе [tooApp введение среды службы][IntroToAppServiceEnvironment]

Вокруг управляющий входящий трафик tooyour среды службы приложений Подробнее [управление tooan входящего трафика среды службы приложений][ControlInboundASE]

Дополнительные сведения о платформе hello службе приложений Azure см. в разделе [службе приложений Azure][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[ControlInboundTraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[NetworkAccessControlLists]: https://azure.microsoft.com/documentation/articles/virtual-networks-acl/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ControlInboundASE]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/ 

<!-- IMAGES -->
[SqlServerEndpoint]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/SqlServerEndpoint01.png
[NetworkAccessControlListExample]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/NetworkAcl01.png
[DefaultNetworkSecurityRules]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/DefaultNetworkSecurityRules01.png 
