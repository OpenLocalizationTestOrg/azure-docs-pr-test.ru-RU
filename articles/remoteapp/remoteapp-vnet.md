---
title: "aaaValidate toouse виртуальной сети Azure hello Azure RemoteApp. | Документы Microsoft"
description: "Узнайте, как toomake убедитесь, что виртуальная сеть Azure готова toouse Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b573ba02-4587-4be5-9821-27bd891a73b2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 5587556c264356e6ab6039b983a38cb2b95ed268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="validate-hello-azure-vnet-toouse-with-azure-remoteapp"></a>Проверка toouse виртуальной сети Azure hello Azure RemoteApp.
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Прежде чем использовать виртуальной сети Azure с Azure RemoteApp, может потребоваться toovalidate hello виртуальной сети. Это помогает избежать проблем с подключением.

toovalidate сети Azure hello следующие:

1. Создание виртуальной машины Azure в подсети hello hello виртуальной сети Azure, требуется toouse с Azure RemoteApp.
2. Подключение toothat виртуальной Машины с помощью hello **Connect** параметр на портале управления hello.
3. Присоединение виртуальной машины toohello hello того же домена, что toouse с Azure RemoteApp. При создании гибридной коллекции, который подключается tooyour локальной сети, присоедините hello виртуальной машины tooyour локального домена.

При успешном выполнении это hello виртуальной сети Azure — Готово toouse с RemoteApp.

Дополнительные сведения о рабочем процессе сбора гибридного конца в конец hello см. следующие статьи hello:

* [Как tooplan виртуальной сети Azure RemoteApp](remoteapp-planvnet.md)
* [Создание гибридной коллекции](remoteapp-create-hybrid-deployment.md)
* [Развертывание Azure RemoteApp коллекции tooyour виртуальной сети Azure (с поддержкой ExpressRoute).](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)

