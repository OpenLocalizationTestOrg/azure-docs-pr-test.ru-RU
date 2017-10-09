---
title: "aaaList из toowhitelist URL-адреса и порты для Azure RemoteApp развернуты в виртуальной сети клиента | Документы Microsoft"
description: "Узнайте, какие порты и URL-адреса, вам потребуется tooconfigure для связи через Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: 5a001ff7-14c9-47fa-9b39-78fd5a5f0250
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 039866f7b64ac763ca833d66031ade3def1d3543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="list-of-ports-and-urls-toopermit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a>Список URL-адреса и порты доступа toopermit для Azure RemoteApp развернуты в виртуальной сети клиента
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

При развертывании коллекцию Azure RemoteApp облачной или гибридной в виртуальной сети (VNET), просмотрите следующие сведения о порте hello. Дополнительные сведения о виртуальных сетях см. в статье [Обзор виртуальной сети](../virtual-network/virtual-networks-overview.md). При создании ограничения трафика toohello виртуальных сетевых ресурсов в вашей коллекции группы безопасности сети (NSG), убедитесь, что следующие порты hello доступна и разрешенных в соответствии с политиками безопасности hello hello виртуальной сети. Дополнительные сведения о группах безопасности сети см. в разделе [Группа безопасности сети (NSG)](../virtual-network/virtual-networks-nsg.md).

## <a name="azure-remoteapp-subnet-needs-access-toothese-endpoints-and-urls"></a>Azure RemoteApp подсеть должна включать конечные точки доступа toothese и URL-адреса:
* *.servicebus.windows.net
* *.servicebus.net
* https://*.remoteapp.windowsazure.com  
* https://www.remoteapp.windowsazure.com 
* https://*remoteapp.windowsazure.com  
* https://*.core.windows.net  
* Исходящие: TCP: TCP: 443, 9351, 9352, 10101-10175. 
* Необязательно — UDP: 10201-10275  

## <a name="azure-remoteapp-clients-need-access-toothese-endpoints-and-urls"></a>Azure RemoteApp клиенты должны получить доступ к URL-адреса и конечные точки toothese:
Клиентами, которые я имею в виду hello настольных компьютеров, устройств и т.д. людей, используйте tooconnect toohello приложения развернуты в hello коллекции Azure RemoteApp.

* https://telemetry.remoteapp.windowsazure.com  
* https://*.RemoteApp.windowsazure.com (hello дополнительные порты UDP, для этого адреса) 
* https://login.windows.net  
* https://login.microsoftonline.com  
* https://www.remoteapp.windowsazure.com 
* https://*.core.windows.net  
* Исходящие: TCP: 443  
* (Необязательно) UDP: 3391 

