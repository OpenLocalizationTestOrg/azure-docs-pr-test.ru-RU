---
title: "Приступая к работе с Edge Интернета вещей Azure (Windows) | Документация Майкрософт"
description: "Узнайте, как создать шлюз Edge Интернета вещей Azure на компьютере Windows, а также ознакомьтесь с основными понятиями Edge Интернета вещей Azure, такими как модули и JSON-файлы конфигурации."
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
ms.openlocfilehash: 5db39bab8e31a8e7026b34e72b4614b0f6f57772
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="explore-azure-iot-edge-architecture-on-windows"></a><span data-ttu-id="f29ab-103">Приступая к работе с архитектурой Edge Интернета вещей в Windows</span><span class="sxs-lookup"><span data-stu-id="f29ab-103">Explore Azure IoT Edge architecture on Windows</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="f29ab-104">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="f29ab-104">How to run the sample</span></span>

<span data-ttu-id="f29ab-105">Скрипт **build.cmd** создает выходные данные в папке **build** локальной копии репозитория **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="f29ab-105">The **build.cmd** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="f29ab-106">Выходные данные содержат два модуля Edge Интернета вещей, которые используются в данном примере.</span><span class="sxs-lookup"><span data-stu-id="f29ab-106">This output includes the two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="f29ab-107">Сценарий сборки размещает **logger.dll** в папках **build\\modules\\logger\\Debug** и **hello\_world.dll** in the **build\\modules\\hello_world\\Debug**.</span><span class="sxs-lookup"><span data-stu-id="f29ab-107">The build script places **logger.dll** in the **build\\modules\\logger\\Debug** folder and **hello\_world.dll** in the **build\\modules\\hello_world\\Debug** folder.</span></span> <span data-ttu-id="f29ab-108">Используйте эти пути для настройки значений **module path**, как указано в приведенном ниже файле параметров JSON.</span><span class="sxs-lookup"><span data-stu-id="f29ab-108">Use these paths for the **module path** values as shown in the following JSON settings file.</span></span>

<span data-ttu-id="f29ab-109">Процесс hello\_world\_sample принимает путь к JSON-файлу конфигурации в качестве аргумента командной строки.</span><span class="sxs-lookup"><span data-stu-id="f29ab-109">The hello\_world\_sample process takes the path to a JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="f29ab-110">Приведенный ниже пример JSON-файла размещен в репозитории пакетов SDK по пути **samples\\hello\_world\\src\\hello\_world\_win.json**.</span><span class="sxs-lookup"><span data-stu-id="f29ab-110">The following example JSON file is provided in the SDK repository at **samples\\hello\_world\\src\\hello\_world\_win.json**.</span></span> <span data-ttu-id="f29ab-111">Этот файл конфигурации работает так, как если бы вы не модифицировали сценарий сборки, чтобы разместить модули IoT Edge или образцы исполняемых файлов в местах, отличных от настроек по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f29ab-111">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="f29ab-112">Пути к модулям зависят от каталога, в котором находится файл hello\_world\_sample.exe.</span><span class="sxs-lookup"><span data-stu-id="f29ab-112">The module paths are relative to the directory where the hello\_world\_sample.exe is located.</span></span> <span data-ttu-id="f29ab-113">По умолчанию пример JSON-файла конфигурации предусматривает запись файла log.txt в текущем рабочем каталоге.</span><span class="sxs-lookup"><span data-stu-id="f29ab-113">The sample JSON configuration file defaults to writing 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="f29ab-114">Перейдите в папку **build** в корневой папке вашей локальной копии репозитория **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="f29ab-114">Navigate to the **build** folder in the root of your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="f29ab-115">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f29ab-115">Run the following command:</span></span>

    ```cmd
    samples\hello_world\Debug\hello_world_sample.exe ..\samples\hello_world\src\hello_world_win.json
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]
