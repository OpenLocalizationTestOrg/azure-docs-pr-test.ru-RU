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
# <a name="explore-azure-iot-edge-architecture-on-windows"></a><span data-ttu-id="2f29e-103">Приступая к работе с архитектурой Edge Интернета вещей в Windows</span><span class="sxs-lookup"><span data-stu-id="2f29e-103">Explore Azure IoT Edge architecture on Windows</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="2f29e-104">Как toorun hello образца</span><span class="sxs-lookup"><span data-stu-id="2f29e-104">How toorun hello sample</span></span>

<span data-ttu-id="2f29e-105">Hello **build.cmd** сценарий создает выходные данные в hello **построения** папки в локальной копии hello **iot edge** репозитория.</span><span class="sxs-lookup"><span data-stu-id="2f29e-105">hello **build.cmd** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="2f29e-106">Этот выход включает hello используемый в этом примере два модуля IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="2f29e-106">This output includes hello two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="2f29e-107">Здравствуйте местах скрипт построения **logger.dll** в hello **построения\\модули\\средства ведения журнала\\отладки** папки и **hello\_world.dll**  в hello **построения\\модули\\hello_world\\отладки** папки.</span><span class="sxs-lookup"><span data-stu-id="2f29e-107">hello build script places **logger.dll** in hello **build\\modules\\logger\\Debug** folder and **hello\_world.dll** in hello **build\\modules\\hello_world\\Debug** folder.</span></span> <span data-ttu-id="2f29e-108">Эти пути можно использовать для hello **путь к модулю** значения, как показано в следующий файл параметров JSON hello.</span><span class="sxs-lookup"><span data-stu-id="2f29e-108">Use these paths for hello **module path** values as shown in hello following JSON settings file.</span></span>

<span data-ttu-id="2f29e-109">Hello hello\_world\_занимает образец файла конфигурации JSON tooa путь hello аргумент командной строки.</span><span class="sxs-lookup"><span data-stu-id="2f29e-109">hello hello\_world\_sample process takes hello path tooa JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="2f29e-110">Hello следующий файл JSON приведены в репозиторий SDK hello в **образцы\\hello\_world\\src\\hello\_world\_win.json**.</span><span class="sxs-lookup"><span data-stu-id="2f29e-110">hello following example JSON file is provided in hello SDK repository at **samples\\hello\_world\\src\\hello\_world\_win.json**.</span></span> <span data-ttu-id="2f29e-111">Это работает файл конфигурации, если только не изменить hello построения hello tooplace сценария IoT Edge модули или образец исполняемые файлы в нестандартные расположения.</span><span class="sxs-lookup"><span data-stu-id="2f29e-111">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="2f29e-112">пути поиска модуля Hello, toohello относительный каталог, если hello hello\_world\_sample.exe находится.</span><span class="sxs-lookup"><span data-stu-id="2f29e-112">hello module paths are relative toohello directory where hello hello\_world\_sample.exe is located.</span></span> <span data-ttu-id="2f29e-113">Образец Hello значения по умолчанию toowriting файл «log.txt» JSON конфигурации в текущий рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="2f29e-113">hello sample JSON configuration file defaults toowriting 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="2f29e-114">Перейдите toohello **построения** папок в корне hello ваша локальная копия hello **iot edge** репозитория.</span><span class="sxs-lookup"><span data-stu-id="2f29e-114">Navigate toohello **build** folder in hello root of your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="2f29e-115">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="2f29e-115">Run hello following command:</span></span>

    ```cmd
    samples\hello_world\Debug\hello_world_sample.exe ..\samples\hello_world\src\hello_world_win.json
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]
