---
title: "aaaUsing Azure DNS с другими службами Azure | Документы Microsoft"
description: "Понимание того, как имя tooresolve toouse Azure DNS для других служб Azure"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure dns
ms.assetid: e9b5eb94-7984-4640-9930-564bb9e82b78
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 09/21/2016
ms.author: gwallace
ms.openlocfilehash: 791f93d6aff2c638c08518e9f1e8ab89ac8de3f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-dns-works-with-other-azure-services"></a>Как Azure DNS работает с другими службами Azure

Azure DNS является размещенной службой управления и разрешения имен (DNS). Это позволяет вам toocreate общих имен DNS для hello других приложений и служб, которые были развернуты в Azure. Создание имени для службы Azure в личный домен простым добавлением запись hello правильного типа службы.

* Для динамически выделенные IP-адреса необходимо создать запись DNS CNAME DNS-имени toohello карты, созданные Azure для службы. Стандартах DNS не позволяют использовать запись CNAME в зоне вершина hello.
* Статически выделенный IP-адресов, можно создать запись DNS типа с помощью любое имя, включая *naked домена* имя в вершине зоны hello.

Hello следующие таблицы контуров hello поддерживается типы записей, которые могут использоваться для различных служб Azure. Как видно из этой таблицы, Azure DNS поддерживает записи DNS только для сетевых ресурсов с выходом в Интернет. Azure DNS невозможно использовать для разрешения имен внутренних, частных адресов.

| Служба Azure | Сетевой интерфейс | Описание |
| --- | --- | --- |
| Шлюз приложений |[Общедоступный IP-адрес внешнего интерфейса](dns-custom-domain.md#public-ip-address) |Можно создать запись A или CNAME в DNS. |
| Балансировщик нагрузки |[Общедоступный IP-адрес внешнего интерфейса](dns-custom-domain.md#public-ip-address)  |Можно создать запись A или CNAME в DNS. Балансировщик нагрузки может иметь общедоступный IP-адрес IPv6, назначаемый динамически. Поэтому необходимо создать запись CNAME для IPv6-адреса. |
| Диспетчер трафика |Общедоступное имя |Можно создать только запись CNAME, которая сопоставляет toohello trafficmanager.net имя, назначенное tooyour профиль диспетчера трафика. Дополнительные сведения см. в статье [Как работает диспетчер трафика](../traffic-manager/traffic-manager-overview.md#traffic-manager-example). |
| Облачная служба |[Общедоступный IP-адрес](dns-custom-domain.md#public-ip-address) |Для статически выделенных IP-адресов можно создать запись A DNS. Для динамически выделенные IP-адреса, необходимо создать запись CNAME, которая сопоставляет toohello *cloudapp.net* имя. Это правило применяется tooVMs создать hello классическом портале, так как они развертываются в облачной службе. Дополнительные сведения см. в статье [Настройка пользовательского доменного имени для облачной службы Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). |
| Служба приложений | [Внешний IP-адрес](dns-custom-domain.md#app-service-web-apps) |Для внешних IP-адресов можно создать запись A DNS. В противном случае необходимо создать запись CNAME, которая сопоставляет имя azurewebsites.net toohello. Дополнительные сведения см. в разделе [сопоставить tooan имя пользовательского домена приложения Azure](../app-service-web/web-sites-custom-domain-name.md) |
| Виртуальные машины Resource Manager |[Общедоступный IP-адрес](dns-custom-domain.md#public-ip-address) |У виртуальных машин Resource Manager могут быть общедоступные IP-адреса. Кроме того, виртуальная машина с общедоступным IP-адресом может обслуживаться балансировщиком нагрузки. Можно создать запись DNS типа или CNAME для hello общедоступный адрес. Это пользовательское имя может быть VIP используется toobypass hello в подсистеме балансировки нагрузки hello. |
| классические виртуальные машины; |[Общедоступный IP-адрес](dns-custom-domain.md#public-ip-address) |Для классических виртуальных машин, созданных с помощью PowerShell или интерфейса командной строки, можно настроить динамический или статический (зарезервированный) виртуальный адрес. Для них можно создать запись CNAME или A в DNS, соответственно. |
