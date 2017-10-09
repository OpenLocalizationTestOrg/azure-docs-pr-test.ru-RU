---
title: "сведения о aaaSizing для виртуальной сети в Azure RemoteApp | Документы Microsoft"
description: "Дополнительные сведения о hello IP адрес требования для Azure RemoteApp, выполнив виртуальной сети"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b6e1c4ba-0236-42b2-bced-69353bf211be
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: f98b831af32c41740b258d122b3e18765be08d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a>Выбор размера виртуальной сети при работе в среде Azure RemoteApp
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

При использовании Azure RemoteApp с помощью виртуальной сети (VNET) RemoteApp использует IP-адресов в подсети hello. На основе hello масштаба службы RemoteApp, необходимо, чтобы tooensure, что подсеть имеет достаточно IP-адресов, доступных для удаленных приложений RemoteApp виртуальных машин. Это руководство по определению размеров сети не является идеальным с учетом того факта, что среда RemoteApp динамически подключает и отключает виртуальные машины в пределах коллекции, однако оно поможет вам подобрать оптимальный диапазон для своей подсети. Это особенно важно, как после размещения службы RemoteApp в виртуальную сеть невозможно увеличить размер подсети hello без удаления удаленных приложений RemoteApp.

Для каждой коллекции RemoteApp, что требуется toorun с максимальной нагрузкой должны иметь 100 IP-адресов. Например при наличии одной коллекции RemoteApp в плана Standard hello и требуется toohave hello максимум 500 пользователей, должен иметь 100 IP-адресов для этой коллекции. Подобным образом необходимо 100 IP-адресов для коллекции RemoteApp в базовый план hello 800 пользователей. Если планируется toohave меньшее число пользователей (меньше, чем максимальное hello), можно уменьшить hello IP-адреса, необходимые для коллекции. требования к размеру Hello минимальное подсети — 30 IP-адресов (/ 27).

Ознакомьтесь с hello, следуя toomake сведения о том, что виртуальная сеть настроена и работает в реестре должным образом:

* [Перенос из личных tooan виртуальная сеть виртуальной сети Azure](remoteapp-migratevnet.md)
* [Проверка toouse виртуальной сети Azure hello Azure RemoteApp.](remoteapp-vnet.md)

