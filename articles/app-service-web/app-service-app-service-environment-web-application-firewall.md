---
title: "aaaConfiguring брандмауэра приложений Web (WAF) для среды службы приложений"
description: "Узнайте, как брандмауэре tooconfigure веб-приложения перед среды службы приложений."
services: app-service\web
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: a2101291-83ba-4169-98a2-2c0ed9a65e8d
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: naziml
ms.openlocfilehash: 0fcf62aea871751c9d4f294d2d24df2186fc0e7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a>Настройка брандмауэра веб-приложения (WAF) для среды службы приложений
## <a name="overview"></a>Обзор
Веб-приложения брандмауэров как hello [WAF Barracuda для Azure](https://www.barracuda.com/programs/azure) , которое доступно на hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) помогает защитить веб-приложений путем проверки tooblock web входящий трафик SQL включению, межсайтовых сценариев, вредоносных программ передач & приложения DDoS и других атак. Он также проверяет hello ответы от hello серверной части веб-серверов для защиты от потери данных (DLP). В сочетании с изоляции hello и дополнительных масштабирования среды службы приложений, предоставляемые, это обеспечивает идеальную среду toohost деловые критических веб-приложения, которым нужны toowithstand вредоносных запросов и большого объема трафика.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a>Настройка
Для этого документа, которые мы настроить нашей среды службы приложений за несколько нагрузки равномерно экземпляров Barracuda WAF, чтобы трафик только с hello WAF может достигать hello среды службы приложений, и он не будет доступен из сети Периметра hello. Мы также получат диспетчера трафика Azure перед нашей Barracuda WAF экземпляров tooload баланс между центрами обработки данных Azure и регионов. Высокоуровневая схема установки hello выглядит следующим образом показанной ниже.

![Архитектура][Architecture] 

> Примечание: С введением hello [ILB поддержка среды службы приложений](app-service-environment-with-internal-load-balancer.md), можно настроить toobe hello ASE недоступны из hello DMZ и быть только доступные toohello частной сети. 
> 
> 

## <a name="configuring-your-app-service-environment"></a>Настройка среды службы приложений
tooconfigure среды службы приложений ссылаться слишком[нашей документации](app-service-web-how-to-create-an-app-service-environment.md) по теме hello. После создания среды службы приложений, можно создать [веб-приложений](app-service-web-overview.md), [приложения API](../app-service-api/app-service-api-apps-why-best-platform.md) и [мобильные приложения](../app-service-mobile/app-service-mobile-value-prop.md) в этой среде, который будет защищать за hello WAF мы Настройте в следующем разделе hello.

## <a name="configuring-your-barracuda-waf-cloud-service"></a>Настройка облачной службы Barracuda WAF
У нас есть [подробная статья](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) о развертывании Barracuda WAF на виртуальной машине в Azure. Но так как мы должны избыточность и вводит единую точку сбоя, необходимо, чтобы экземпляр WAF toodeploy по крайней мере 2 виртуальных машин в hello одной облачной службе, когда выполнение этих инструкций.

### <a name="adding-endpoints-toocloud-service"></a>Добавление tooCloud конечные точки службы
Когда имеется 2 или несколько виртуальных Машин WAF экземпляров в облачной службе можно использовать hello [портал Azure](https://portal.azure.com/) tooadd HTTP и HTTPS конечные точки, используемые вашим приложением, как показано в приведенном ниже рисунке hello.

![Настройка конечной точки][ConfigureEndpoint]

Если приложения используют другие конечные точки, создайте список этих toothis, также убедиться, что tooadd. 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a>Настройка Barracuda WAF через портал управления
Barracuda WAF использует TCP-порт 8000 для настройки с помощью портала управления. Поскольку у нас есть несколько экземпляров виртуальных машин WAF hello toorepeat hello при выполнении шагов потребуется для каждого экземпляра виртуальной Машины. 

> Примечание: После завершения работы с конфигурацией WAF, удалите конечную точку TCP/8000 hello из всех вашей tookeep WAF виртуальных машин вашей WAF безопасного.
> 
> 

Добавьте конечную точку управления hello как показано на рисунке hello ниже tooconfigure вашей WAF Barracuda.

![Добавление конечной точки управления][AddManagementEndpoint]

Используйте браузер конечная точка управления toobrowse toohello на облачной службы. Если облачная служба вызывается test.cloudapp.net, доступ к этой конечной точке путем просмотра toohttp://test.cloudapp.net:8000. Должна появиться страница входа в систему, аналогичные показанным ниже можно выполнить вход с использованием учетных данных, указанный в фазу установки hello WAF виртуальной Машины.

![Страница управления входом][ManagementLoginPage]

После входа вы увидите панель мониторинга как hello один hello рисунке ниже, будет представлять базовую статистику о hello WAF защиты.

![Панель управления][ManagementDashboard]

Нажав на вкладку "службы" hello позволит вам настроить вашей WAF для служб, которые он защищает. Дополнительные сведения о настройке WAF Barracuda можно найти в соответствующей [документации](https://techlib.barracuda.com/waf/getstarted1). В примере hello ниже веб-приложение Azure обслуживающий трафика по протоколам HTTP и HTTPS настроена.

![Управление: добавление служб][ManagementAddServices]

> Примечание: В зависимости от того, как настроена приложения и какие функции используются в среде службы приложений, вам потребуется tooforward трафика для TCP-порты, отличные от 80 и 443, например если вы настроили IP SSL для веб-приложения. Список сетевых портов, используемых в среде службы приложений, можно найти слишком[входящий трафик управления документации](app-service-app-service-environment-control-inbound-traffic.md) раздел сетевые порты.
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a>Настройка диспетчера трафика Microsoft Azure (необязательно)
Если приложение будет доступно в нескольких регионах, то требуется баланс tooload их за [диспетчера трафика Azure](../traffic-manager/traffic-manager-overview.md). toodo, поэтому можно добавить конечную точку в hello [классический портал Azure](https://manage.azure.com) с помощью hello имя облачной службы для вашего WAF в профиле диспетчера трафика hello, как показано в приведенном ниже рисунке hello. 

![Конечная точка диспетчера трафика][TrafficManagerEndpoint]

Если приложение требует проверки подлинности, убедитесь, что у вас есть некоторые ресурсы, не требуется проверка подлинности для tooping диспетчера трафика для доступности приложения hello. Вы можете настроить URL-адресом hello в разделе Настройка hello в hello [классический портал Azure](https://manage.azure.com) как показано ниже.

![Настройка диспетчера трафика][ConfigureTrafficManager]

tooforward hello диспетчера трафика запросы проверки связи от приложения tooyour WAF, Barracuda WAF tooforward трафика tooyour приложения, как показано в следующем примере hello должны переводы toosetup веб-сайта.

![Переводы веб-сайта][WebsiteTranslations]

## <a name="securing-traffic-tooapp-service-environment-using-network-security-groups-nsg"></a>Обеспечение безопасности трафика tooApp службы среды с помощью сетевой безопасности группы (NSG)
Выполните hello [документации входящий трафик управления](app-service-app-service-environment-control-inbound-traffic.md) для сведений об ограничении трафика tooyour среды службы приложений из hello WAF только с помощью адреса hello виртуальный IP-адрес облачной службы. Ниже приведен пример команды Powershell для выполнения этой задачи для TCP-порта 80.

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

Замените hello SourceAddressPrefix hello Virtual IP Address (VIP) для вашей WAF облачной службы.

> Примечание: hello виртуальный IP-адрес облачной службы изменится, если удалить и повторно создать hello облачной службы. Убедитесь, что tooupdate hello IP-адрес в группе ресурсов сети hello после этого. 
> 
> 

<!-- IMAGES -->
[Architecture]: ./media/app-service-app-service-environment-web-application-firewall/Architecture.png
[ConfigureEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureEndpoint.png
[AddManagementEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/AddManagementEndpoint.png
[ManagementAddServices]: ./media/app-service-app-service-environment-web-application-firewall/ManagementAddServices.png
[ManagementDashboard]: ./media/app-service-app-service-environment-web-application-firewall/ManagementDashboard.png
[ManagementLoginPage]: ./media/app-service-app-service-environment-web-application-firewall/ManagementLoginPage.png
[TrafficManagerEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/TrafficManagerEndpoint.png
[ConfigureTrafficManager]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureTrafficManager.png
[WebsiteTranslations]: ./media/app-service-app-service-environment-web-application-firewall/WebsiteTranslations.png
