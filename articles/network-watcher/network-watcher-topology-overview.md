---
title: "tootopology aaaIntroduction в Наблюдатель сети Azure | Документы Microsoft"
description: "Эта страница предоставляет обзор возможностей топологии hello Наблюдатель сети"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e753a435-38e0-482b-846b-121cb547555c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7fa1c5518e4a25a5db999d898a9ee19fd0121db7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tootopology-in-azure-network-watcher"></a>Tootopology введение в инспектор сети Azure

Топология возвращает граф сетевых ресурсов в виртуальной сети. Hello диаграмма показывает hello взаимосвязь между hello ресурсы toorepresent hello окончания tooend сетевое подключение.

![Обзор топологии][1]

В портал hello топологии возвращает hello объектов ресурсов для каждой виртуальной сети. связи Hello изображаются линиями между hello ресурсы за пределами области hello Наблюдатель сети, даже если в hello ресурсов группы не отображается. ресурсы Hello, возвращаемые в представлении портала hello представляют собой подмножество hello сетевых компонентов, отображаемых в графике. toosee hello полный список сетевых ресурсов можно использовать [PowerShell](network-watcher-topology-powershell.md) или [REST](network-watcher-topology-rest.md)

> [!NOTE]
> Требуется экземпляр Наблюдатель сети в каждом регионе нужного toorun топологии.

В разделе две связи моделируются как ресурсы возвращаются hello соединения между ними.

- **Вложение.** Например, виртуальная сеть содержит подсеть, которая, в свою очередь, содержит сетевую карту.
- **Связь.** Например, сетевая карта связана с виртуальной машиной.

### <a name="next-steps"></a>Дальнейшие действия

Узнайте, как просмотреть toouse PowerShell tooretrieve hello топологии, посетив [топологией Наблюдатель сети с помощью PowerShell](network-watcher-topology-powershell.md)

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
