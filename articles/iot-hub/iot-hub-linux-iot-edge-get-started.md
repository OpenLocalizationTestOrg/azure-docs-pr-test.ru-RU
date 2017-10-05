---
title: "Начало работы с Azure IoT Edge (Linux) | Документация Майкрософт"
description: "Узнайте, как создать шлюз на компьютере Linux, а также ознакомьтесь с основными понятиями Edge Интернета вещей Azure, такими как модули и JSON-файлы конфигурации."
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
ms.openlocfilehash: b02d79fcd9cd2a2ef0041aac4e85528263c8d58a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="explore-azure-iot-edge-architecture-on-linux"></a><span data-ttu-id="5eeba-103">Приступая к работе с архитектурой Edge Интернета вещей в Linux</span><span class="sxs-lookup"><span data-stu-id="5eeba-103">Explore Azure IoT Edge architecture on Linux</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="5eeba-104">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="5eeba-104">How to run the sample</span></span>

<span data-ttu-id="5eeba-105">Скрипт **build.sh** создает выходные данные в папке **build** локальной копии репозитория **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="5eeba-105">The **build.sh** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="5eeba-106">Выходные данные содержат два модуля Edge Интернета вещей, которые используются в данном примере.</span><span class="sxs-lookup"><span data-stu-id="5eeba-106">This output includes the two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="5eeba-107">Скрипт сборки размещает **liblogger.so** в папке **build/modules/logger/**, а **libhello\_world.so** — в папке **build/modules/hello_world/**.</span><span class="sxs-lookup"><span data-stu-id="5eeba-107">The build script places **liblogger.so** in the **build/modules/logger/** folder and **libhello\_world.so** in the **build/modules/hello_world/** folder.</span></span> <span data-ttu-id="5eeba-108">Используйте эти пути для настройки значения **module path**, как указано в приведенном ниже примере файла параметров JSON.</span><span class="sxs-lookup"><span data-stu-id="5eeba-108">Use these paths for the **module path** values as shown in the following example JSON settings file.</span></span>

<span data-ttu-id="5eeba-109">Процесс hello\_world\_sample принимает путь к JSON-файлу конфигурации в качестве аргумента командной строки.</span><span class="sxs-lookup"><span data-stu-id="5eeba-109">The hello\_world\_sample process takes the path to a JSON configuration file a command-line argument.</span></span> <span data-ttu-id="5eeba-110">Приведенный ниже пример JSON-файла размещен в репозитории пакетов SDK по пути **samples/hello\_world/src/hello\_world\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="5eeba-110">The following example JSON file is provided in the SDK repository at **samples/hello\_world/src/hello\_world\_lin.json**.</span></span> <span data-ttu-id="5eeba-111">Этот файл конфигурации работает так, как если бы вы не модифицировали сценарий сборки, чтобы разместить модули IoT Edge или образцы исполняемых файлов в местах, отличных от настроек по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5eeba-111">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="5eeba-112">Пути к модулям зависят от текущего рабочего каталога, в котором запускается исполняемый файл hello\_world\_sample, а не от каталога, где находится исполняемый файл.</span><span class="sxs-lookup"><span data-stu-id="5eeba-112">The module paths are relative to the current working directory from where the hello\_world\_sample executable is launched, not the directory where the executable is located.</span></span> <span data-ttu-id="5eeba-113">По умолчанию пример JSON-файла конфигурации предусматривает запись файла log.txt в текущем рабочем каталоге.</span><span class="sxs-lookup"><span data-stu-id="5eeba-113">The sample JSON configuration file defaults to writing 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="5eeba-114">Перейдите в папку **build** в корневой папке вашей локальной копии репозитория **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="5eeba-114">Navigate to the **build** folder in the root of your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="5eeba-115">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5eeba-115">Run the following command:</span></span>

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

