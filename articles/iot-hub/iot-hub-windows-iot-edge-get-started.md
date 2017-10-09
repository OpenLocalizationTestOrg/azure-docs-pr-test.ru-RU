---
title: "aaaGet работы с Azure IoT Edge (Windows) | Документы Microsoft"
description: "Как toobuild шлюз Azure IoT Edge в Windows компьютер и изучите основные понятия в Azure IoT Edge, например модули и файлы конфигурации JSON."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 9aff3724-5e4e-40ec-b95a-d00df4f590c5
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: andbuc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5dd13cbfc02eeb55d9f2dbffca5021f2624acf14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="explore-azure-iot-edge-architecture-on-windows"></a>Приступая к работе с архитектурой Edge Интернета вещей в Windows

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a>Как toorun hello образца

Hello **build.cmd** сценарий создает выходные данные в hello **построения** папки в локальной копии hello **iot edge** репозитория. Этот выход включает hello используемый в этом примере два модуля IoT Edge.

Здравствуйте местах скрипт построения **logger.dll** в hello **построения\\модули\\средства ведения журнала\\отладки** папки и **hello\_world.dll**  в hello **построения\\модули\\hello_world\\отладки** папки. Эти пути можно использовать для hello **путь к модулю** значения, как показано в следующий файл параметров JSON hello.

Hello hello\_world\_занимает образец файла конфигурации JSON tooa путь hello аргумент командной строки. Hello следующий файл JSON приведены в репозиторий SDK hello в **образцы\\hello\_world\\src\\hello\_world\_win.json**. Это работает файл конфигурации, если только не изменить hello построения hello tooplace сценария IoT Edge модули или образец исполняемые файлы в нестандартные расположения.

> [!NOTE]
> пути поиска модуля Hello, toohello относительный каталог, если hello hello\_world\_sample.exe находится. Образец Hello значения по умолчанию toowriting файл «log.txt» JSON конфигурации в текущий рабочий каталог.

```json
{
  "modules": [
    {
      "name": "logger",
      "loader": {
        "name": "native",
        "entrypoint": {
          "module.path": "..\\..\\..\\modules\\logger\\Debug\\logger.dll"
        }
      },
      "args": { "filename": "log.txt" }
    },
    {
      "name": "hello_world",
      "loader": {
        "name": "native",
        "entrypoint": {
          "module.path": "..\\..\\..\\modules\\hello_world\\Debug\\hello_world.dll"
        }
      },
      "args": null
      }
  ],
  "links": [
    {
      "source": "hello_world",
      "sink": "logger"
    }
  ]
}
```

1. Перейдите toohello **построения** папок в корне hello ваша локальная копия hello **iot edge** репозитория.

1. Выполните следующую команду hello.

    ```cmd
    samples\hello_world\Debug\hello_world_sample.exe ..\samples\hello_world\src\hello_world_win.json
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]
