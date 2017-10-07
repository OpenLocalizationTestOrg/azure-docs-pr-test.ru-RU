---
title: "Параметры DNS в файле конфигурации виртуальной сети aaaSpecifying | Документы Microsoft"
description: "Как файл toochange параметры DNS-сервера в виртуальной сети, используя конфигурацию виртуальной сети в hello классической модели развертывания"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a8905927-92ac-42b5-8c33-8e42c000692c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: d53a658773e1c930b5a28a701db0be9edd26565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a>Задание параметров DNS в файле конфигурации виртуальной сети
Файл конфигурации сети состоит из двух элементов, можно использовать параметры системы доменных имен (DNS) toospecify: **DnsServers** и **DnsServerRef**. Можно добавить список DNS-серверов, указав их IP-адреса и ссылаться на имена toohello **DnsServers** элемента. Затем можно использовать **DnsServerRef** toospecify элемент, какие записи DNS-сервера из элемент DnsServers hello используются для различных сетевых сайтов в виртуальной сети.

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

В этой статье рассматриваются hello классической модели развертывания.

файл конфигурации сети Hello может содержать следующие элементы hello. Hello Заголовок каждого элемента является связанного tooa, предоставляющий дополнительные сведения об элементе hello значения параметров.

> [!IMPORTANT]
> Сведения о как tooconfigure hello файла конфигурации сети см. в разделе [настройки виртуальной сети с помощью файла конфигурации сети](virtual-networks-using-network-configuration-file.md). Сведения о каждом элементе, содержащемся в файле конфигурации сети hello см. в разделе [схема конфигурации виртуальной сети Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).
> 
> 

[Элемент DNS](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> Hello **имя** атрибута в hello **DnsServer** элемент используется только в качестве ссылки для hello **DnsServerRef** элемента. Он не представляет имя узла hello hello DNS-сервера. Каждый **DnsServer** значение атрибута должно быть уникальным для всей подписки Microsoft Azure hello
> 
> 

[Элемент Virtual Network Sites](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> Чтобы toospecify этот параметр для элемента Virtual Network Sites hello, должен быть предварительно определен в элементе DNS hello. Hello DnsServerRef *имя* в hello сайтов виртуальной сети должен ссылаться tooa имя значение, указанное в элементе hello DNS для DNS-сервер *имя*.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
* Понимать hello [схема конфигурации виртуальной сети Azure](http://go.microsoft.com/fwlink/?LinkId=248093).
* Понимать hello [схема конфигурации службы Azure](https://msdn.microsoft.com/library/windowsazure/ee758710).
* [Настройка виртуальной сети с помощью файлов конфигурации сети](virtual-networks-using-network-configuration-file.md).

