---
title: "подключение aaaCheck с Наблюдатель сети Azure — портал Azure | Документы Microsoft"
description: "На этой странице объясняется, как проверить подключение toouse с Наблюдатель сети с помощью портала Azure hello"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: gwallace
ms.openlocfilehash: ef6ecccd688f06f70003a5b59771c15bcbe8f3e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a>Убедитесь в наличии подключения с Наблюдатель сети Azure с помощью портала Azure hello

> [!div class="op_single_selector"]
> - [Портал](network-watcher-connectivity-portal.md)
> - [PowerShell](network-watcher-connectivity-powershell.md)
> - [CLI 2.0](network-watcher-connectivity-cli.md)
> - [Azure REST API](network-watcher-connectivity-rest.md)

Узнайте, как можно установить toouse tooverify подключения, если прямое подключение TCP от tooa виртуальной машины, заданный конечной точки.

## <a name="before-you-begin"></a>Перед началом работы

В этой статье предполагается, что hello следующие ресурсы:

* Экземпляр Наблюдатель сети в регионе hello нужно toocheck подключения.

* Виртуальные машины toocheck подключение.

> [!IMPORTANT]
> Для проверки возможности подключения требуется расширение виртуальной машины `AzureNetworkWatcherExtension`. Установка расширения hello на виртуальной Машине Windows на сайте [расширение виртуальной машины агента Наблюдатель сети Azure для Windows](../virtual-machines/windows/extensions-nwa.md) и виртуальной Машине Linux см. по адресу [расширение виртуальной машины агента Наблюдатель сети Azure для Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="check-connectivity-tooa-virtual-machine"></a>Проверьте подключение tooa виртуальной машины

В этом примере проверяется подключение tooa целевой виртуальной машине через порт 80.

Найдите tooyour Наблюдатель сети и нажмите кнопку **проверку подключения (Предварительная версия)**. Выберите подключение виртуальной машины toocheck hello. В hello **назначения** выберите **выберите виртуальную машину** и выберите hello соответствующей виртуальной машине и tootest порта.

После нажатия кнопки **проверьте**, проверяются hello подключения между виртуальными машинами hello на указанный порт hello. В примере hello hello назначения виртуальной Машины недоступен, отображаются список переходов.

![Результаты проверки возможности подключения виртуальной машины][1]

## <a name="check-remote-endpoint-connectivity"></a>Проверка возможности подключения к удаленной конечной точке

подключение toocheck hello и задержки tooa удаленную конечную точку, выберите hello **вручную указать** переключатель в hello **назначения** щелкните входных hello URL-адрес и порт hello, щелкните **проверки** .  Это используется для таких удаленных конечных точек, такие как конечные точки веб-сайтов и хранилищ.

![Результаты проверки возможности подключения веб-сайта][2]

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как снимки tooautomate пакетов с оповещениями виртуальной машины, просмотрев [создать получения оповещений триггеру пакетов](network-watcher-alert-triggered-packet-capture.md)

Сведения о состоянии (разрешен или запрещен) входящего и исходящего трафика виртуальной машины см. в статье, посвященной [проверке потока IP-адресов](network-watcher-check-ip-flow-verify-portal.md).

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
