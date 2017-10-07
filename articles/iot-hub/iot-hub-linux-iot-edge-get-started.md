---
title: "aaaGet работы с Azure IoT Edge (Linux) | Документы Microsoft"
description: "Как toobuild шлюза на Linux машины и изучите основные понятия в Azure IoT Edge, например модули и файлы конфигурации JSON."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: cf537bdd-2352-4bb1-96cd-a283fcd3d6cf
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: andbuc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40aa9c8ddca6a974c361cbb0b453c7d0ddc71b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="explore-azure-iot-edge-architecture-on-linux"></a>Приступая к работе с архитектурой Edge Интернета вещей в Linux

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a>Как toorun hello образца

Hello **build.sh** сценарий создает выходные данные в hello **построения** папки в локальной копии hello **iot edge** репозитория. Этот выход включает hello используемый в этом примере два модуля IoT Edge.

Здравствуйте местах скрипт построения **liblogger.so** в hello **сборки, модули/logger/** папки и **libhello\_world.so** в hello **построения / модули/hello_world/** папки. Эти пути можно использовать для hello **путь к модулю** значения, как показано в следующий пример файла параметров JSON hello.

Hello hello\_world\_образец занимает файл конфигурации JSON tooa путь hello аргумента командной строки. Hello следующий файл JSON приведены в репозиторий SDK hello в **образцы/hello\_мира, src/hello\_world\_lin.json**. Это работает файл конфигурации, если только не изменить hello построения hello tooplace сценария IoT Edge модули или образец исполняемые файлы в нестандартные расположения.

> [!NOTE]
> Hello модуля, пути относительный toohello текущий рабочий каталог откуда hello hello\_world\_запускается исполняемый файл образца, не hello каталог, где находится исполняемый файл hello. Образец Hello значения по умолчанию toowriting файл «log.txt» JSON конфигурации в текущий рабочий каталог.

```json
{
    "modules" :
    [
        {
            "name" : "logger",
            "loader": {
            "name": "native",
            "entrypoint": {
                "module.path": "./modules/logger/liblogger.so"
            }
            },
            "args" : {"filename":"log.txt"}
        },
        {
            "name" : "hello_world",
            "loader": {
            "name": "native",
            "entrypoint": {
                "module.path": "./modules/hello_world/libhello_world.so"
            }
            },
            "args" : null
        }
    ],
    "links":
    [
        {
            "source": "hello_world",
            "sink": "logger"
        }
    ]
}
```

1. Перейдите toohello **построения** папок в корне hello ваша локальная копия hello **iot edge** репозитория.

1. Выполните следующую команду hello.

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

