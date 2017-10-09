---
title: "toouse aaaHow API управления Azure с внутреннюю виртуальную сеть | Документы Microsoft"
description: "Узнайте, как toosetup и настройка службы управления API Azure в внутреннюю виртуальную сеть."
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: 
ms.assetid: dac28ccf-2550-45a5-89cf-192d87369bc3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 8d25de14e0c0bebe7ba7b47ca432ea4e45dde312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a>Использование службы управления API Azure совместно с внутренней виртуальной сетью
API управления Azure виртуальных сетей (Vnet), позволяет управлять API-интерфейсы не доступен в Интернете hello. Число технологии виртуальных частных СЕТЕЙ, доступных toomake hello подключения и управления API может быть развернуто на два основных режима внутри hello виртуальной сети:
* Внешний
* Внутренний

## <a name="overview"> </a>Содержание раздела
При развертывании управления API в режиме внутренней виртуальной сети все hello конечные точки службы (шлюза, портал разработчиков, портал издателя, прямого управления и Git) отображаются только внутри виртуальной сети, управления доступом к. Ни одна из конечных точек службы hello регистрируются на общедоступном DNS-сервере hello.

С помощью API управления в режиме внутренней можно добиться hello следующие сценарии
* безопасно предоставлять третьим лицам доступ к API, размещенным в частном центре обработки данных, с помощью VPN-подключений типа "сеть —сеть" или ExpressRoute;
* поддерживать сценарии гибридного облака, предоставляя облачные и локально размещенные API-интерфейсы через общий шлюз;
* управлять API-интерфейсами, размещенными в разных географических расположениях, через одну общую конечную точку шлюза. 

## <a name="enable-vpn"> </a>Создание управления API во внутренней виртуальной сети
за внутреннего Balancer(ILB) нагрузки размещается Hello службе управления API в внутренней виртуальной сети. Hello hello ILB IP-адрес находится в hello [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) диапазона.  

### <a name="enable-vnet-connection-using-azure-portal"></a>Активация подключения к виртуальной сети с помощью портала Azure
Сначала создать службу управления API hello, выполните действия hello [службы управления API создания][Create API Management service]. Затем toobe управления API настройки, развернута внутри виртуальной сети.

![Меню настройки APIM во внутренней виртуальной сети][api-management-using-internal-vnet-menu]

После успешного завершения развертывания hello hello внутренний виртуальный IP-адрес службы появится на панели мониторинга hello.

![Панель мониторинга управления API с настроенной внутренней сетью][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a>Активация подключения к виртуальной сети с помощью командлетов PowerShell
Можно также включить подключения к виртуальной сети с помощью командлетов PowerShell hello.

* **Создание службы управления API внутри виртуальной сети**: с помощью командлета hello [New AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate управления API Azure службы внутри виртуальной сети и настроить его тип внутренней виртуальной сети toouse hello.

* **Развернуть существующую службу управления API внутри виртуальной сети**: с помощью командлета hello [AzureRmApiManagementDeployment обновление](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove существующие Azure API Management службы внутри виртуальной сети и настроить его toouse Внутренний тип виртуальной сети.

## <a name="apim-dns-configuration"></a>Настройка DNS
Когда вы используете управление API во внешнем режиме виртуальной сети, службой DNS управляет Azure. Для режима внутренней виртуальной сети у вас toomanage собственные DNS.

> [!NOTE]
> Служба управления API не прослушивает toorequests, поступающий на IP-адреса. Отвечает только toorequests toohello имя узла настроен на его конечные точки службы (которая включает шлюза, портал разработчиков, портал издателя, конечная точка прямого управления и git).

### <a name="access-on-default-host-names"></a>По умолчанию используются такие имена узлов:
При создании API управления службы в общедоступном облаке Azure, например с именем «contoso», hello следующих конечных точек службы настраиваются по умолчанию.

>   шлюз или прокси — contoso.azure api.net;

> портал издателя и портал для разработчиков — contoso.portal.azure api.net;

> конечная точка прямого управления — contoso.management.azure api.net;

>   Git — contoso.scm.azure-api.net.

tooaccess эти конечные точки службы управления API, можно создать виртуальную машину в виртуальной сети toohello подсетью и подключенная, в которой развертывается API управления. При условии hello внутренний виртуальный IP-адрес для службы 10.0.0.5, можно сделать hello сопоставления файлов узлов (% SystemDrive%\drivers\etc\hosts) следующим образом:

> 10.0.0.5    contoso.azure-api.net

> 10.0.0.5    contoso.portal.azure-api.net

> 10.0.0.5    contoso.management.azure-api.net

> 10.0.0.5    contoso.scm.azure-api.net

Можно затем получить все конечные точки службы hello из виртуальной машины, созданную hello. Если вы используете пользовательский DNS-сервер в виртуальной сети, можно создать соответствующие записи DNS типа A. Тогда доступ к конечным точкам будет возможен из любого расположения в пределах виртуальной сети. 

### <a name="access-on-custom-domain-names"></a>Доступ по пользовательским доменным именам
Если вы не хотите tooaccess приветствия имен узлов по умолчанию hello в службе управления API, вы можете настроить пользовательские доменные имена для всех конечных точек службы, такие как ниже

![Настройка пользовательского домена для управления API][api-management-custom-domain-name]

Затем можно создать записи в вашей tooaccess DNS-сервер этих конечных точек, которые доступны только внутри виртуальной сети.

## <a name="related-content"> </a>Связанная информация
* Обзор [распространенных проблем с конфигурацией сети при настройке APIM в виртуальной сети][Common Network Configuration Issues]
* [Часто задаваемые вопросы по виртуальной сети](../virtual-network/virtual-networks-faq.md)
* Инструкции по [созданию записей DNS типа A](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
