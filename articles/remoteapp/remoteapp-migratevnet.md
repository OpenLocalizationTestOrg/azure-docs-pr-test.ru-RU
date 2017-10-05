---
title: "Переход с платформы RemoteApp VNET на платформу Azure VNET | Документация Майкрософт"
description: "Сведения о переходе с платформы RemoteApp VNET на платформу Azure VNET"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: baea5d29-353b-48f8-b47f-806f2163e067
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 10b5f4844a38fe97852dee8634e8cf54f1a23a1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-migrate-a-hybrid-collection-from-a-remoteapp-vnet-to-an-azure-vnet"></a>Перенос гибридной коллекции с платформы RemoteApp VNET в среду Azure VNET
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Дополнительные сведения см. в [объявлении](https://go.microsoft.com/fwlink/?linkid=821148).
> 
> 

Отличная новость! Теперь вы можете развертывать гибридные коллекции RemoteApp непосредственно в существующих виртуальных сетях Azure (VNET-сетях) вместо создания специальных VNET-сетей для службы RemoteApp. Благодаря этому вам становятся доступны новейшие функции и преимущества VNET (такие как ExpressRoute), а также возможность предоставить своим гибридным коллекциям непосредственный сетевой доступ к другим службам и виртуальным машинам Azure, развернутым для этой VNET-сети.  (Это повышает эффективность и производительность, а также упрощает настройку в сравнении с конфигурациями VNET/VNET.)

Предположим, у вас уже есть гибридная коллекция RemoteApp под названием *OriginalCollection* с VNET-сетью RemoteApp, которая называется *RemoteAppVNET*. Рассмотрим действия, которые необходимо выполнить для ее переноса в новую VNET-сеть Azure под названием *AzureVNET*.

1. На вкладке **Сети** [портала управления](http://manage.windowsazure.com/) создайте VNET-сеть под названием *AzureVNET* с тем же расположением, конфигурацией DNS и адресным пространством (как минимум для одной из подсетей *AzureVNET*), что и у виртуальной сети *RemoteAppVNET*.
2. Настройте сеть *AzureVNET* таким образом, чтобы в ней размещалось развертывание Active Directory, в которое входит домен *OriginalCollection*, или между ними был организован сетевой доступ.
3. На вкладке **RemoteApps** создайте новую коллекцию RemoteApp под названием *NewCollection*. (Используйте вариант **Создать с помощью VNet**, а не **Быстрое создание**.)
4. Разверните коллекцию *NewCollection* в подсети виртуальной сети *AzureVNET*.
5. Задайте для *NewCollection* те же параметры образа и присоединения к домену, что и для коллекции *OriginalCollection*.
6. Через несколько часов коллекция *NewCollection* появится в списке коллекции в активном состоянии.

Теперь, если вам НЕ НУЖНО переносить данные пользователей из исходной коллекции в новую, выполните указанные ниже действия.

1. Удалите исходную коллекцию *OriginalCollection*.
2. Удалите виртуальную сеть *RemoteAppVNET*.

Готово!

Если вам все же НУЖНО перенести данные пользователей из исходной коллекции в новую, выполните указанные ниже действия.

1. Отправьте на адрес [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) электронное сообщение с идентификатором подписки Azure, именами исходной и новой коллекций и просьбой перенести данные пользователей.
2. В течение двух рабочих дней специалисты RemoteApp перенесут список доступа пользователей, а также все их документы и параметры из исходной коллекции в новую.
3. Удалите исходную коллекцию *OriginalCollection*.
4. Удалите виртуальную сеть *RemoteAppVNET*.

Готово!

Если у вас есть какие-либо вопросы или вам необходима дополнительная помощь, напишите по адресу [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).

