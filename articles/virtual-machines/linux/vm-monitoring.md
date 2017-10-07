---
title: "aaaEnable или отключение мониторинга виртуальных Машин Azure"
description: "Описывает способ tooEnable или отключение мониторинга виртуальных Машин Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 6ce366d2-bd4c-4fef-a8f5-a3ae2374abcc
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/08/2016
ms.author: kmouss
ms.openlocfilehash: 39c2211e4e5f3ad364513b52c5acc70c00b432fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a>Включение и отключение мониторинга виртуальной машины Azure

В этом разделе описывается, как tooenable или отключите мониторинг на виртуальные машины в Azure. Можно включить или отключить мониторинг с помощью портала hello или интерфейса командной строки Azure для Mac, Linux и Windows (hello Azure CLI).

> [!IMPORTANT]
> В этом документе описываются версии 2.3 hello диагностического расширения Linux, которое рекомендуется к использованию. Версия 2.3 будет поддерживаться до 30 июня 2018 г.
>
> Вместо этого можно включить версии 3.0 hello диагностического расширения для Linux. Дополнительные сведения см. в разделе [hello документации](./diagnostic-extension.md).

## <a name="enable--disable-monitoring-through-hello-azure-portal"></a>Включить / отключить мониторинг через hello портал Azure

Вы можете включить мониторинг виртуальной машины Azure, который предоставляет данные о вашем экземпляре с интервалом в 1 минуту (применяются изменения хранилища). Подробные диагностические данные затем становится доступным для hello ВМ hello портала диаграммах или с помощью hello API. По умолчанию портал Azure обеспечивает мониторинг ограниченного набора метрик на основе узла. Вы можете включить наблюдение за показателей в виртуальной Машине при приветствия Виртуальная машина запущена или остановлена.

* Откройте hello Azure портала в [https://portal.azure.com](https://portal.azure.com).
* В hello навигации слева выберите виртуальные машины.
* На виртуальных машинах hello список выберите экземпляр запущенной или остановленной. Открывает колонку Hello «Виртуальная машина».
* Щелкните "Все параметры".
* Щелкните "Диагностика".
* Изменить состояние tooOn или Off. Также можно выбрать на этом уровне hello колонке мониторинга сведения tooenable требуется для вашей виртуальной машины.

![Включить / отключить мониторинг через портал Azure hello.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a>Включение и отключение мониторинга с помощью интерфейса командной строки Azure

tooenable мониторинг на Виртуальной машине Azure.

* Создайте файл (например, с именем PrivateConfig.json):

```json
{
        "storageAccountName":"hello storage account tooreceive data",
        "storageAccountKey":"hello key of hello account"
}
```

* Включите расширение hello через Azure CLI.

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

Дополнительные сведения см. в разделе [производительности и диагностических данных с помощью диагностического расширения Linux tooMonitor Linux VM](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
