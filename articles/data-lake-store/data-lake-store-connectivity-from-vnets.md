---
title: "aaaConnect tooAzure хранилища Озера данных из виртуальных сетей | Документы Microsoft"
description: "Подключение хранилища Озера данных tooAzure из виртуальных сетей Azure"
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 683fcfdc-cf93-46c3-b2d2-5cb79f5e9ea5
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: c695dcf49fe4e1a87a90729cf085a938f3b51fe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-data-lake-store-from-vms-within-an-azure-vnet"></a>Доступ к Azure Data Lake Store из виртуальных машин в виртуальной сети Azure
Azure Data Lake Store — это служба PaaS, которая использует общедоступные IP-адреса в Интернете. Любой сервер, обычно подключения toohello открытый Интернет может подключиться tooAzure конечные точки хранилища Озера данных также. По умолчанию все виртуальные машины, которые находятся в виртуальных сетях Azure можно получить доступ к Интернету hello и таким образом можно получить доступ к хранилищу Озера данных Azure. Однако это возможно tooconfigure ВМ в toonot виртуальной сети имеют toohello доступа к Интернету. Для таких виртуальных машин хранилища Озера данных tooAzure доступ ограничен также. Блокирует общий доступ в Интернет для виртуальных машин в виртуальных сетях Azure можно сделать с помощью любого подходе hello.

* Настройка групп безопасности сети (NSG).
* Настройка определяемых пользователем маршрутов (UDR).
* Путем обмена маршруты через BGP (стандартный динамической маршрутизации протокол) при использовании этого блока ExpressRoute доступ к Интернету toohello

В этой статье вы узнаете, как tooenable доступ к хранилищу Озера данных Azure toohello из виртуальных машин Azure, которой были ограниченными tooaccess ресурсов с помощью одного из трех методов hello, перечисленные выше.

## <a name="enabling-connectivity-tooazure-data-lake-store-from-vms-with-restricted-connectivity"></a>Включение tooAzure подключения к хранилищу Озера данных из виртуальных машин с ограниченным подключением
tooaccess Azure Озера данных хранения из таких виртуальных машин, их необходимо настроить IP-адрес tooaccess hello, где находится hello хранилища Озера данных Azure. Можно определить hello IP-адресов для хранилища Озера данных учетных записей, разрешение имен DNS hello учетных записей (`<account>.azuredatalakestore.net`). Для этого можно использовать такие средства, как **nslookup**. Откройте командную строку на компьютере и запустите следующую команду hello.

    nslookup mydatastore.azuredatalakestore.net

выходные данные Hello напоминает следующее hello. Здравствуйте, значения данных **адрес** свойство — hello IP-адрес, связанный с вашей учетной записи хранилища Озера данных.

    Non-authoritative answer:
    Name:    1434ceb1-3a4b-4bc0-9c69-a0823fd69bba-mydatastore.projectcabostore.net
    Address:  104.44.88.112
    Aliases:  mydatastore.azuredatalakestore.net


### <a name="enabling-connectivity-from-vms-restricted-by-using-nsg"></a>Настройка подключения из виртуальных машин, ограниченных с помощью NSG
При использовании правила NSG tooblock доступ к toohello Интернет, то можно создать другую NSG, которая разрешает доступ toohello адрес хранилища Озера данных. Дополнительные сведения о правилах NSG см. в статье [Группа безопасности сети](../virtual-network/virtual-networks-nsg.md). Инструкции по статье Nsg toocreate [как с помощью Nsg toomanage hello портал Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).

### <a name="enabling-connectivity-from-vms-restricted-by-using-udr-or-expressroute"></a>Настройка подключения из виртуальных машин, ограниченных с помощью UDR или ExpressRoute
Когда маршруты UDRs или обмен BGP маршруты, toohello доступа используется tooblock Интернет, специальные маршрут должен toobe настроен так, что виртуальные машины в таких подсетей можно получить доступ к конечные точки хранилища Озера данных. Дополнительные сведения см. в статье [Что такое определяемые пользователем маршруты и IP-пересылка?](../virtual-network/virtual-networks-udr-overview.md) Инструкции по созданию определяемых пользователем маршрутов см. в статье [Создание определяемых пользователем маршрутов (UDR) в Resource Manager с помощью PowerShell](../virtual-network/virtual-network-create-udr-arm-ps.md).

### <a name="enabling-connectivity-from-vms-restricted-by-using-expressroute"></a>Настройка подключения из виртуальных машин, ограниченных с помощью ExpressRoute
При настройке канала ExpressRoute hello локальных серверов можно обращаться из хранилища Озера данных открытого пиринга. Дополнительные сведения о настройке ExpressRoute для общедоступного пиринга см. в статье [Вопросы и ответы по ExpressRoute](../expressroute/expressroute-faqs.md).

## <a name="see-also"></a>Дополнительные материалы
* [Обзор хранилища озера данных Azure](data-lake-store-overview.md)
* [Обеспечение безопасности в Azure Data Lake Store](data-lake-store-security-overview.md)

