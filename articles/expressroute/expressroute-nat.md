---
title: "требования к aaaNAT для каналов ExpressRoute. | Документы Microsoft"
description: "На этой странице подробно описаны требования по настройке NAT для каналов ExpressRoute и управлению им."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 867bf936-c851-485f-84c8-d8d6e33fee9f
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 09a0e841235de3f6b85e32172d7f99f20b5baf54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-nat-requirements"></a>Требования ExpressRoute к NAT
tooconnect tooMicrosoft облачных служб с помощью ExpressRoute вам требуется tooset вверх и управлять NAT. Некоторые поставщики услуг подключения предлагают настройку NAT как управляемой службы и управление этой службой. Проверьте у вашего подключения к поставщику toosee предлагают такой службы. Если нет, должен соответствовать следующим требованиям toohello. 

Просмотрите hello [ExpressRoute цепи и домены маршрутизации](expressroute-circuit-peerings.md) страница tooget Обзор hello различные домены маршрутизации. toomeet hello открытый IP адрес требования для Azure открытый и пиринг Майкрософт, мы рекомендуем настроить NAT между вашей сетью и Майкрософт. Этот раздел содержит подробное описание инфраструктуры NAT hello необходимые tooset вверх.

## <a name="nat-requirements-for-azure-public-peering"></a>Требования к NAT для общедоступного пиринга Azure
Hello пути открытого пиринга Azure позволяет вам tooconnect tooall служб, размещенных в Azure через их общих IP-адресов. К ним относятся служб, перечисленных в hello [ExpessRoute часто задаваемые вопросы о](expressroute-faqs.md) и ко всем службам, размещенным независимые поставщики программного обеспечения в Microsoft Azure. 

> [!IMPORTANT]
> Подключение tooMicrosoft Azure служб на открытый пиринг всегда инициируется из локальной сети в сеть Microsoft hello. Таким образом сеансы не удается запустить из сети tooyour служб Microsoft Azure по ExpressRoute. Попыток, отправленных пакетов toothese объявляются IP-адреса будет использовать hello Интернет вместо ExpressRoute.
> 

Трафик, проходящий tooMicrosoft Azure на открытый пиринг должно быть toovalid SNATed открытый IPv4-адреса еще до входа hello Microsoft network. на следующем рисунке Hello предоставляет высокоуровневый изображение как hello NAT, может быть установлен hello toomeet выше требования.

![](./media/expressroute-nat/expressroute-nat-azure-public.png) 

### <a name="nat-ip-pool-and-route-advertisements"></a>Пул IP-адресов и объявления маршрутов для NAT
Необходимо убедиться, что трафик вводит hello Azure пути открытого пиринга допустимый общедоступный адрес IPv4. Microsoft должен быть владельцем hello может toovalidate hello пул адресов IPv4 NAT региональный маршрутизации Интернет-регистратор (RIR) или в реестре маршрутизации Интернета (ВСД). Проверка будет выполняться основании hello как номер по рангу со и hello IP-адреса, используемые для hello NAT. См. toohello [требования к маршрутизации ExpressRoute](expressroute-routing.md) страницы сведения о маршрутизации реестров.

Существуют ограничения на длину hello префикс IP-адреса NAT hello, объявленных через этот пиринг. Необходимо отслеживать пул NAT hello и убедитесь, что вы не не испытывает существенной нехватки NAT сеансов.

> [!IMPORTANT]
> Hello пула NAT IP-адресов объявленных tooMicrosoft не должно быть объявленной toohello Интернета. Это приведет к разрыву подключения tooother Майкрософт.
> 
> 

## <a name="nat-requirements-for-microsoft-peering"></a>Требования NAT для пиринга Майкрософт
пути пиринга Microsoft Hello позволяет подключаться через hello Azure пути открытого пиринга tooMicrosoft облачные службы, которые не поддерживаются. Список Hello служб входят такие службы Office 365, Exchange Online, SharePoint Online, Скайп для бизнеса и Dynamics 365. Корпорация Майкрософт рассчитывает toosupport двустороннее соединение на пиринг Майкрософт hello. Трафик, проходящий tooMicrosoft облачные службы должны быть toovalid SNATed открытый IPv4-адреса еще до входа hello Microsoft network. Сетевой трафик, проходящий tooyour из облачных служб Майкрософт должны быть SNATed на ваш tooprevent edge Internet [асимметричного маршрутизации](expressroute-asymmetric-routing.md). на следующем рисунке Hello предоставляет высокоуровневый изображение как hello NAT должны быть установлены для пиринга Майкрософт.

![](./media/expressroute-nat/expressroute-nat-microsoft.png) 

### <a name="traffic-originating-from-your-network-destined-toomicrosoft"></a>Исходящий трафик с вашей сети предназначенные tooMicrosoft
* Необходимо убедиться, что трафик вводит hello пути пиринга Майкрософт с допустимым публичным адресом IPv4. Microsoft должен быть владельцем hello может toovalidate hello пул адресов IPv4 NAT для hello региональный маршрутизации Интернет-регистратор (RIR) или маршрутизации реестра Интернета (ВСД). Проверка будет выполняться основании hello как номер по рангу со и hello IP-адреса, используемые для hello NAT. См. toohello [требования к маршрутизации ExpressRoute](expressroute-routing.md) страницы сведения о маршрутизации реестров.
* IP-адреса используются для hello Настройка открытого пиринга Azure и другие каналы ExpressRoute не должно быть объявленной tooMicrosoft через сеанс BGP hello. Нет никаких ограничений на длину hello префикс IP-адреса NAT hello, объявленных через этот пиринг.
  
  > [!IMPORTANT]
  > Hello пула NAT IP-адресов объявленных tooMicrosoft не должно быть объявленной toohello Интернета. Это приведет к разрыву подключения tooother Майкрософт.
  > 
  > 

### <a name="traffic-originating-from-microsoft-destined-tooyour-network"></a>Исходящий трафик с назначения tooyour сети (Майкрософт)
* Некоторые сценарии требуют Microsoft конечных точек для tooservice tooinitiate подключения к размещенному в сети. Типичный сценарий hello бы подключения tooADFS серверов, размещаемых в сети из Office 365. В таких случаях необходимо утечек соответствующие префиксы сети в пиринг Майкрософт hello. 
* Необходимо SNAT Microsoft трафика в hello Internet edge для конечных точек службы в вашей сети tooprevent [асимметричного маршрутизации](expressroute-asymmetric-routing.md). Запросы **и ответы** с конечным IP-адресом, которые соответствуют маршруту, полученному через ExpressRoute, всегда будут отправляться через ExpressRoute. Асимметричные маршрутизации существует, если запрос hello, полученных через hello Интернета с hello ответа, отправляемые через ExpressRoute. SNATing hello Microsoft трафик на hello Internet edge принудительно ответного трафика задней toohello Internet edge разрешение проблемы hello.

![Асимметричная маршрутизация с помощью ExpressRoute](./media/expressroute-asymmetric-routing/AsymmetricRouting2.png)

## <a name="next-steps"></a>Дальнейшие действия
* См. требования к toohello для [маршрутизации](expressroute-routing.md) и [QoS](expressroute-qos.md).
* Сведения о рабочем процессе см. в статье [Процедуры ExpressRoute для подготовки каналов и состояний каналов](expressroute-workflows.md).
* Настройте подключение ExpressRoute.
  
  * [Создайте канал ExpressRoute.](expressroute-howto-circuit-classic.md)
  * [Настройка маршрутизации](expressroute-howto-routing-classic.md)
  * [Связывание виртуальной сети tooan канал ExpressRoute](expressroute-howto-linkvnet-classic.md)

