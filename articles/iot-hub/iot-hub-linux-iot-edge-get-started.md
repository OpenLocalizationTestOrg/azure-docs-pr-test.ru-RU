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
# <a name="explore-azure-iot-edge-architecture-on-linux"></a><span data-ttu-id="9b1ce-103">Приступая к работе с архитектурой Edge Интернета вещей в Linux</span><span class="sxs-lookup"><span data-stu-id="9b1ce-103">Explore Azure IoT Edge architecture on Linux</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="9b1ce-104">Как toorun hello образца</span><span class="sxs-lookup"><span data-stu-id="9b1ce-104">How toorun hello sample</span></span>

<span data-ttu-id="9b1ce-105">Hello **build.sh** сценарий создает выходные данные в hello **построения** папки в локальной копии hello **iot edge** репозитория.</span><span class="sxs-lookup"><span data-stu-id="9b1ce-105">hello **build.sh** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="9b1ce-106">Этот выход включает hello используемый в этом примере два модуля IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="9b1ce-106">This output includes hello two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="9b1ce-107">Здравствуйте местах скрипт построения **liblogger.so** в hello **сборки, модули/logger/** папки и **libhello\_world.so** в hello **построения / модули/hello_world/** папки.</span><span class="sxs-lookup"><span data-stu-id="9b1ce-107">hello build script places **liblogger.so** in hello **build/modules/logger/** folder and **libhello\_world.so** in hello **build/modules/hello_world/** folder.</span></span> <span data-ttu-id="9b1ce-108">Эти пути можно использовать для hello **путь к модулю** значения, как показано в следующий пример файла параметров JSON hello.</span><span class="sxs-lookup"><span data-stu-id="9b1ce-108">Use these paths for hello **module path** values as shown in hello following example JSON settings file.</span></span>

<span data-ttu-id="9b1ce-109">Hello hello\_world\_образец занимает файл конфигурации JSON tooa путь hello аргумента командной строки.</span><span class="sxs-lookup"><span data-stu-id="9b1ce-109">hello hello\_world\_sample process takes hello path tooa JSON configuration file a command-line argument.</span></span> <span data-ttu-id="9b1ce-110">Hello следующий файл JSON приведены в репозиторий SDK hello в **образцы/hello\_мира, src/hello\_world\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="9b1ce-110">hello following example JSON file is provided in hello SDK repository at **samples/hello\_world/src/hello\_world\_lin.json**.</span></span> <span data-ttu-id="9b1ce-111">Это работает файл конфигурации, если только не изменить hello построения hello tooplace сценария IoT Edge модули или образец исполняемые файлы в нестандартные расположения.</span><span class="sxs-lookup"><span data-stu-id="9b1ce-111">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="9b1ce-112">Hello модуля, пути относительный toohello текущий рабочий каталог откуда hello hello\_world\_запускается исполняемый файл образца, не hello каталог, где находится исполняемый файл hello.</span><span class="sxs-lookup"><span data-stu-id="9b1ce-112">hello module paths are relative toohello current working directory from where hello hello\_world\_sample executable is launched, not hello directory where hello executable is located.</span></span> <span data-ttu-id="9b1ce-113">Образец Hello значения по умолчанию toowriting файл «log.txt» JSON конфигурации в текущий рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="9b1ce-113">hello sample JSON configuration file defaults toowriting 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="9b1ce-114">Перейдите toohello **построения** папок в корне hello ваша локальная копия hello **iot edge** репозитория.</span><span class="sxs-lookup"><span data-stu-id="9b1ce-114">Navigate toohello **build** folder in hello root of your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="9b1ce-115">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="9b1ce-115">Run hello following command:</span></span>

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

