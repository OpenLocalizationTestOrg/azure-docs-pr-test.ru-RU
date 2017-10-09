---
title: "aaaHow tooplan виртуальной сети коллекцию Azure RemoteApp | Документы Microsoft"
description: "Узнайте, как tooplan виртуальной сети коллекцию Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: ad9aff0e-f374-49c0-951d-4a7be1c36de0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: d7eeefc3c66815b18f9338e2e428585e6f81a12a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooplan-your-virtual-network-for-azure-remoteapp"></a>Как tooplan виртуальной сети Azure RemoteApp
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

В этом документе описывается способ tooset копии виртуальной сети (VNET) Azure и подсеть hello для Azure RemoteApp. Если вы не знакомы с виртуальными сетями Azure, это возможность, которая помогает вам toovirtualize вашей сети инфраструктуры toohello облака и toocreate гибридных решений с помощью Azure и локальным ресурсам. Подробнее об этом можно прочитать [здесь](../virtual-network/virtual-networks-overview.md).

Если требуется toodefine политики безопасности для трафика (входящие и исходящие) в виртуальной сети, в которой выполняется развертывание Azure RemoteApp, настоятельно рекомендуется Создание отдельной подсети для Azure RemoteApp на основе rest hello развертываний в hello Azure Виртуальная сеть. Дополнительные сведения о как toodefine политики безопасности на Azure виртуальные сети подсети, прочитайте [что такое группа безопасности сети (NSG)?](../virtual-network/virtual-networks-nsg.md).

## <a name="types-of-azure-remoteapp-collections-with-azure-virtual-networks"></a>Типы коллекций Azure RemoteApp с виртуальными сетями Azure
Hello следующие графики показывают hello два варианта другую коллекцию при необходимости toouse виртуальной сети.

### <a name="azure-remoteapp-cloud-collection-with-vnet"></a>Облачная коллекция Azure RemoteApp с виртуальной сетью
 ![Azure RemoteApp — облачная коллекция с виртуальной сетью](./media/remoteapp-planvpn/ra-cloudvpn.png)

Представляет коллекцию Azure RemoteApp, задавая расположение всех ресурсов hello необходимость tooaccess узла сеансов удаленных приложений RemoteApp hello в Azure. Они могут находиться в hello одной виртуальной сети как hello виртуальной сети RemoteApp или другую виртуальную сеть в Azure.

### <a name="azure-remoteapp-hybrid-collection-with-vnet"></a>Гибридная коллекция Azure RemoteApp с виртуальной сетью
![Azure RemoteApp — гибридная коллекция с виртуальной сетью](./media/remoteapp-planvpn/ra-hybridvpn.png)

Представляет коллекцию Azure RemoteApp, где приведены некоторые ресурсы hello необходимость tooaccess узла сеансов удаленных приложений RemoteApp hello развернутое локально. Hello виртуальной сети RemoteApp — связанного toohello локальной сети с помощью Azure гибридного технологий, как сайт сайт VPN-подключения или Express Route.

## <a name="how-hello-system-works"></a>Как работает система hello
На деле hello Azure RemoteApp развертывает подсеть виртуальной сети виртуальных машин Azure (с отправленного изображения) toohello, выбранное во время инициализации. Если вы выбрали для гибридной коллекции, мы пытаемся tooresolve hello доменное имя контроллера домена hello, введенное на подготовку рабочего процесса с hello DNS-сервер в виртуальной сети hello hello.  
При подключении tooan существующей виртуальной сети, внести необходимые порты, что tooexpose hello в сетевые группы безопасности в вашей подсети Azure RemoteApp. 

Для Azure RemoteApp рекомендуется использовать [достаточно большую подсеть](remoteapp-vnetsizing.md). / 8 больше — наибольшее Hello поддерживается Azure виртуальной сети (по определениям подсети CIDR). Подсети должен быть достаточно большим, tooaccommodate все виртуальные машины RemoteApp hello Azure во время масштабирования, когда несколько пользователей обращаются к приложения hello. 

Ниже приведены действия hello, вам потребуется tooenable в подсети виртуальной сети: 

1. Исходящий трафик из подсети hello должно быть разрешено на toocommunicate 10101 10175 диапазона портов с помощью одного из внутренних служб Azure RemoteApp hello.
2. Следует разрешить исходящий трафик из вашей подсети tooconnect tooAzure хранилища на порте 443
3. При наличии размещенных в Azure Active Directory, убедитесь, что все виртуальные Машины в подсети виртуальной сети hello для Azure RemoteApp — контроллер домена может tooconnect toothat. Hello DNS в hello виртуальной сети должен быть доступ tooresolve hello полное доменное имя этого контроллера домена.

## <a name="virtual-network-with-forced-tunneling"></a>Виртуальная сеть с принудительным туннелированием
[Принудительное туннелирование](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) теперь поддерживается во всех новых коллекциях Azure RemoteApp. В настоящее время мы не поддерживают hello миграции из существующей коллекции toosupport принудительного туннелирования.  Вы должны будете toodelete все существующие коллекции с помощью hello виртуальной сети выполняется связывание tooAzure удаленных приложений RemoteApp и создать новый один tooget, принудительного туннелирования включен на вашей коллекции. 

