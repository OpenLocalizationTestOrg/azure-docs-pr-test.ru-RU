---
title: "toomigrate aaaHow из виртуальной сети RemoteApp tooan виртуальной сети Azure | Документы Microsoft"
description: "Узнайте, как toomigrate из виртуальной сети RemoteApp tooan виртуальной сети Azure"
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
ms.openlocfilehash: c0f8617556c6f1e33eca8322febf67ff33937ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-a-hybrid-collection-from-a-remoteapp-vnet-tooan-azure-vnet"></a>Как toomigrate гибридной коллекции из виртуальной сети RemoteApp tooan виртуальной сети Azure
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Отличная новость! Мы включили коллекции RemoteApp гибридного toodeploy непосредственно в вашей существующей Azure виртуальных сетей (Vnet) вместо создания виртуальных сетей RemoteApp определенного. Это позволяет воспользоваться преимуществами hello новейших функций виртуальной сети (например, ExpressRoute) и предоставьте вашей гибридной коллекции прямого сетевого доступа tooother служб Azure и развернуть виртуальные машины toothat виртуальной сети.  (Это повышает эффективность и производительность, а также упрощает настройку в сравнении с конфигурациями VNET/VNET.)

Предположим, у вас уже есть гибридная коллекция RemoteApp под названием *OriginalCollection* с VNET-сетью RemoteApp, которая называется *RemoteAppVNET*. Ниже приведены шаги toomigrate hello его новой виртуальной сети Azure вызывается tooa *AzureVNET*.

1. На hello **сетей** на вкладке hello [портала управления](http://manage.windowsazure.com/), создание виртуальной сети называется *AzureVNET*, с использованием hello местоположения, конфигурацию DNS и адресного пространства (хотя бы для одного из hello *AzureVNET* подсетей) как вы использовали для *RemoteAppVNET*.
2. Настройка *AzureVNET* tooeither размещения или развертывания Active Directory toohello подключения к сети, *OriginalCollection* присоединен к домену.
3. На hello **удаленными приложениями** создайте новую коллекцию RemoteApp с названием *новую коллекцию*. (Используйте hello **Создание виртуальной сети** вариант не **быстрое создание**.)
4. Настройка *NewCollection* toobe развернут в подсети tooa *AzureVNET*.
5. Настройка *NewCollection* toouse hello того же образа и сведений о присоединении домена, как вы использовали для *OriginalCollection*.
6. Через несколько часов коллекция *NewCollection* появится в списке коллекции в активном состоянии.

Теперь если не требуется toomigrate сведений о пользователе из hello исходной коллекции toohello новой коллекции, выполните указанные ниже действия далее:

1. Удалите исходную коллекцию *OriginalCollection*.
2. Удалите виртуальную сеть *RemoteAppVNET*.

Готово!

Кроме того Если требуется toomigrate сведений о пользователе из hello исходной коллекции toohello новой коллекции, выполните указанные ниже действия далее:

1. Отправить сообщение электронной почты слишком[ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) своим Идентификатором подписки Azure hello имя исходной коллекции, а имя новой коллекции hello и попросите его toomigrate свои учетные данные.
2. В течение 2 рабочих дней команды RemoteApp hello будет перемещать hello список доступа пользователей и все документы пользователя и параметров пользователя из hello исходной коллекции toohello новой коллекции.
3. Удалите исходную коллекцию *OriginalCollection*.
4. Удалите виртуальную сеть *RemoteAppVNET*.

Готово!

Если у вас есть какие-либо вопросы или вам необходима дополнительная помощь, напишите по адресу [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).

