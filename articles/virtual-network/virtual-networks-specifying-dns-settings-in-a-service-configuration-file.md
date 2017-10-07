---
title: "Параметры DNS в файле конфигурации службы aaaSpecifying | Документы Microsoft"
description: "Настройка пользовательских параметров DNS с помощью файла конфигурации службы для виртуальной сети"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 467a4b99-8691-40b3-b640-e25e49675c71
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/24/2016
ms.author: jdial
ms.openlocfilehash: f192e33566dd8e669da04e6378a0c8e4b0b35ecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a>Настройка параметров DNS в файле конфигурации службы
## <a name="dns-elements"></a>Элементы DNS
Файл конфигурации службы может содержать элемент DnsServers со списком IPv4-адресов для серверов hello доменных имен (DNS), которые будет использовать служба hello. В файле конфигурации службы hello имеют приоритет над параметрами в файле конфигурации сети hello. Дополнительные сведения см. в статье, посвященной [схеме конфигурации службы Azure (файл CSCFG)](https://msdn.microsoft.com/library/azure/ee758710.aspx).

**Элемент NetworkConfiguration**

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> Hello **имя** атрибута в hello **DnsServer** используется только в качестве имени ссылки. Он не представляет имя узла hello hello DNS-сервера. Каждый **DnsServer** значение атрибута должно быть уникальным для всей подписки Microsoft Azure hello.
> 
> 

## <a name="see-also"></a>См. также
[Схема конфигурации службы Azure (CSCFG-файл)](https://msdn.microsoft.com/library/windowsazure/ee758710)

[Схема настройки виртуальной сети Azure](http://go.microsoft.com/fwlink/?LinkId=248093)

[Настройка виртуальной сети с помощью файлов конфигурации сети](http://go.microsoft.com/fwlink/?LinkId=248094)

[Параметры виртуальной сети в hello портала управления](http://go.microsoft.com/fwlink/?LinkId=248092)

