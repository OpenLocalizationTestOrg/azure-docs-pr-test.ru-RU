---
title: "среды службы приложений tooAzure aaaIntroduction"
description: "Краткий обзор среды службы приложений Azure."
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 3c7eaefa-1850-4643-8540-428e8982b7cb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 9261041333cf59374974a039edf89c4983c45cdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapp-service-environments"></a>Введение tooApp службы сред #
 
## <a name="overview"></a>Обзор ##

Среда службы приложений Azure — это компонент службы приложений Azure, предоставляющий полностью изолированную и выделенную среду для безопасного выполнения приложений службы приложений в большом масштабе. В ней можно размещать свои [веб-приложения][webapps], [мобильные приложения][mobileapps], [приложения API][APIapps] и [функции][Functions].

Среды службы приложений (ASE) подходят для рабочих нагрузок приложений, требующих выполнения указанных ниже условий:

- очень большой масштаб;
- изоляция и безопасный доступ к сети;
- высокий уровень использования памяти.

Клиенты могут создавать несколько сред ASE в одном или в нескольких регионах Azure. Благодаря этой гибкости среды ASE идеально подходят для горизонтально масштабируемых уровней приложений без учета состояний, поддерживающих большие рабочие нагрузки RPS.

ASEs — изолированной toorunning только одного клиента приложения и всегда развертываются в виртуальной сети. Клиенты могут детально управлять входящим и исходящим сетевым трафиком приложений, а Приложения могут устанавливать высокоскоростной безопасных соединений через VPN локальной tooon корпоративным ресурсам.

Все статьи и как tooinstructions о ASEs доступны в hello [файл README для среды службы приложений][ASEReadme]:

* Среды ASE обеспечивают размещение крупномасштабных приложений с безопасным доступом к сети. Дополнительные сведения см. в разделе hello [AzureCon глубокое погружение](https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/) на ASEs.
* Несколько ASEs может быть используется tooscale по горизонтали. Дополнительные сведения см. в разделе [как tooset копирования отпечатка географически распределенных приложений](https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/).
* ASEs может быть tooconfigure используется архитектура безопасности, как показано в hello глубокое погружение AzureCon. toosee, как показано в hello AzureCon подробная архитектура безопасности hello был настроен, в разделе hello [статьи о том, как tooimplement архитектура многоуровневый безопасности](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-layered-security) с среды службы приложений.
* Приложения, работающие в средах ASE, могут получать доступ через такие устройства, как брандмауэр веб-приложений (WAF). Дополнительные сведения см. в статье [Настройка брандмауэра веб-приложения (WAF) для среды службы приложений](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-web-application-firewall).

## <a name="dedicated-environment"></a>Выделенная среда ##

ASE будет выделен только одной подписке tooa и может содержать 100 экземпляров. Hello диапазон может занимать 100 экземпляров в одной планы служб приложений too100 план службы приложений одного экземпляра и многого другого.

ASE состоит из внешних интерфейсов и рабочих ролей. Внешние интерфейсы отвечают за завершение HTTP/HTTPS, а также за автоматическую балансировку нагрузки запросов приложения в среде ASE. Интерфейсные автоматически добавляются как масштабировать планы служб приложений в hello ASE hello.

Рабочие роли — это роли, в которых размещаются пользовательские приложения. Они доступны в трех фиксированных размерах:

* одно ядро, 3,5 ГБ ОЗУ;
* два ядра, 7 ГБ ОЗУ;
* четыре ядра, 14 ГБ ОЗУ.

Клиентам не требуется toomanage серверов, обслуживающих и работников. Все инфраструктуры автоматически добавляются во время развертывания планов службы приложений пользователями. Как службы приложений, создать или масштабируется по ASE планы hello требуется инфраструктура добавляется или удаляется соответствующим образом.

Нет плоский Месячная ставка для ASE, оплачивает hello инфраструктуру и не изменяется с размером hello ASE hello. Кроме того, существует плата за ядро плана службы приложений. Все приложения, размещенные в ASE находятся в hello изолированных цены SKU. Сведения о ценах для ASE см. в разделе hello [служб приложений Ценовая] [ Pricing] страницы и просмотрите доступные варианты ASEs hello.

## <a name="virtual-network-support"></a>Поддержка виртуальной сети ##

Создавать среду ASE можно только в виртуальной сети Azure Resource Manager. toolearn Дополнительные сведения о виртуальных сетях Azure, в разделе hello [Azure виртуальные сети часто задаваемые вопросы о](https://azure.microsoft.com/documentation/articles/virtual-networks-faq/). Так как среда ASE всегда существует в виртуальной сети, а точнее в подсети виртуальной сети, Можно использовать средства безопасности hello toocontrol виртуальных сетей входящего и исходящего сетевого подключения для вашего приложения.

Среда ASE может быть доступной из Интернета с использованием общедоступного IP-адреса или из внутренней системы с использованием адреса внутреннего балансировщика нагрузки.

[Сетевых групп безопасности] [ NSGs] ограничить входящего сетевого взаимодействия toohello подсети, где находится ASE. Можно использовать Nsg toorun приложения за вышестоящего устройств и служб, таких как WAFs и поставщики SaaS сети.

Приложения, должны также часто tooaccess корпоративным ресурсам, например внутренними базами данных и веб-службы. При развертывании ASE hello в виртуальной сети с VPN toohello подключения локальной сети в hello ASE приложения hello можно обращаться к ресурсам в локальной hello. Эта возможность имеет значение true, независимо от того, hello VPN [сайт сайт](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/) или [Azure ExpressRoute](http://azure.microsoft.com/services/expressroute/) VPN.

Дополнительные сведения о работе сред ASE с виртуальными сетями и локальными сетями см. в статье [Рекомендации по работе с сетями в среде службы приложений][ASENetwork].

## <a name="app-service-environment-v1"></a>Среда службы приложений версии 1 ##

Среда службы приложений имеет две версии: ASEv1 и ASEv2. предшествующий сведения Hello был основан на ASEv2. В этом разделе представлены hello различия между ASEv1 и ASEv2. 

Нужен toomanage ASEv1, все ресурсы hello вручную. Включающий интерфейсных hello, сотрудников и IP-адреса для SSL на основе IP. Прежде чем можно масштабировать плана служб приложений, необходимо toofirst масштабировать hello рабочего пула место toohost его.

ASEv1 использует модель ценообразования отличную от ASEv2. В ASEv1 вы платите за каждое выделенное ядро. Включая ядра, используемые для внешних интерфейсов и рабочих процессов, которые не содержат рабочие нагрузки. В ASEv1 размер максимальный масштаб по умолчанию hello ASE составляет 55 общее количество узлов. включая рабочие роли и внешние интерфейсы. Одно из преимуществ tooASEv1 — могут быть развернуты в классической виртуальной сети и диспетчер ресурсов виртуальной сети. toolearn Дополнительные сведения о ASEv1, в разделе [введение v1 среды службы приложений][ASEv1Intro].

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
