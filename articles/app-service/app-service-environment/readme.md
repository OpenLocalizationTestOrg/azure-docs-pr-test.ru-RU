---
title: "файл readme aaaAzure среды службы приложений"
description: "Перечисляет hello документация, описывающая среды службы приложений Azure"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 77452413-5193-4762-8b3d-5fa8e4edf1ca
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 6edc74804ded7497e70c31c9e08252257add4415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-documentation"></a>Документация по среде службы приложений
 Среда службы приложений Azure — это компонент службы приложений Azure, предоставляющий полностью изолированную и выделенную среду для безопасного выполнения приложений службы приложений в большом масштабе. В ней можно размещать свои [веб-приложения][webapps], [мобильные приложения][mobileapps], [приложения API][APIApps] и [функции][Functions].

Среды службы приложений (ASE) идеально подходят для рабочих нагрузок приложений, требующих выполнения указанных ниже условий.

* Очень большой масштаб.
* Изоляция и безопасный доступ к сети.

Клиенты могут создавать несколько сред ASE в одном или в нескольких регионах Azure. Благодаря этой гибкости среды ASE идеально подходят для горизонтально масштабируемых уровней приложений без учета состояний, поддерживающих большие рабочие нагрузки RPS.

ASEs — изолированной toorunning только одного клиента приложения и всегда развертываются в виртуальной сети Azure. Клиенты могут детально управлять входящим и исходящим сетевым трафиком приложений, используя [группы безопасности сети][NSGs], а Приложения можно также установить высокоскоростной безопасные соединения по корпоративным ресурсам локальной tooon виртуальных сетей.

Приложения часто требуется tooaccess корпоративным ресурсам, например внутренними базами данных и веб-службы. Приложения, работающие в средах ASE, могут получать доступ к ресурсам через VPN-подключение типа [сеть — сеть][SiteToSite] или через канал [Azure ExpressRoute][ExpressRoute].

* [Введение в среду службы приложений][Intro]
* [Создание среды службы приложений][MakeExternalASE]
* [Создание и использование внутреннего балансировщика нагрузки со средой службы приложений][MakeILBASE]
* [Использование среды службы приложений][UsingASE]
* [Сетевые аспекты и hello среды службы приложений][ASENetwork]
* [Создание среды службы приложений с внутренней подсистемой балансировки нагрузки с помощью шаблонов Azure Resource Manager][MakeASEfromTemplate]


## <a name="videos"></a>Видеоролики
Образец современном PaaS для hello Enterprise службе приложений Azure
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

Развертывание высокомасштабируемых и защищенных приложений
>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

Выполнение корпоративных веб-приложений и мобильных приложений в службе приложений Azure
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]

## <a name="app-service-environment-v1"></a>Среда службы приложений версии 1 ##
Существует две версии среды службы приложений: ASEv1 и ASEv2. Сведения об ASEv1 см. в статье [Документация по среде службы приложений][ASEv1README].


<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[ASEv1README]: ../app-service-app-service-environments-readme.md
[SiteToSite]: ../../vpn-gateway/vpn-gateway-site-to-site-create.md
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
