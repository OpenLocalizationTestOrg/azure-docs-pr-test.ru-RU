---
title: "Развертывание модели машинного обучения Azure на устройстве Azure IoT Edge | Документация Майкрософт"
description: "В этом документе объясняется, как развертывать модели машинного обучения Azure на устройствах Azure IoT Edge."
services: machine-learning
author: tedway
ms.author: tedway
manager: mwinkle
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.workload: data-services
ms.topic: article
ms.date: 11/10/2017
ms.openlocfilehash: f83e4b17a3209adeb655723362e6882e38bfaf49
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/18/2017
---
# <a name="deploy-an-azure-machine-learning-model-to-an-azure-iot-edge-device"></a>Развертывание модели машинного обучения Azure для устройства Azure IoT Edge

Все модели машинного обучения Azure, помещенные в контейнеры на основе веб-служб Docker, могут также работать на устройствах Azure IoT Edge. Дополнительные скрипты и инструкции можно найти в [наборе средств для работы с искусственным интеллектом для Azure IoT Edge](http://aka.ms/AI-toolkit).

## <a name="operationalize-the-model"></a>Ввод модели в эксплуатацию
Для ввода модели в эксплуатацию необходимо выполнить инструкции из статьи [Развертывание модели машинного обучения в качестве веб-службы](https://docs.microsoft.com/azure/machine-learning/preview/model-management-service-deploy), чтобы создать образ Docker с вашей моделью.

## <a name="deploy-to-azure-iot-edge"></a>Развертывание в Azure IoT Edge
Azure IoT Edge позволяет перенести аналитику и пользовательскую бизнес-логику из облака на устройства. Все модели машинного обучения могут работать на устройствах Azure IoT Edge. Документацию по настройке устройства IoT Edge и созданию развертывания можно найти на странице [aka.ms/azure-iot-edge-doc](https://aka.ms/azure-iot-edge-doc).

Ниже приведены дополнительные рекомендации.

### <a name="add-registry-credentials-to-the-edge-runtime-on-your-edge-device"></a>Добавление учетных данных реестра в среду выполнения Edge на пограничном устройстве
На компьютере, где выполняется IoT Edge, добавьте учетные данные реестра, чтобы среда выполнения могла иметь доступ для извлечения контейнера.

В ОС Windows выполните следующую команду:
```cmd/sh
iotedgectl login --address <docker-registry-address> --username <docker-username> --password <docker-password>
```
В ОС Linux выполните следующую команду:
```cmd/sh
sudo iotedgectl login --address <docker-registry-address> --username <docker-username> --password <docker-password>
```

### <a name="find-the-machine-learning-container-image-location"></a>Поиск расположения образа контейнера машинного обучения
Вам потребуется расположение образа контейнера машинного обучения. Чтобы найти расположение образа контейнера, выполните следующие действия.

1. Войдите на [портал Azure](http://portal.azure.com/).
2. В области **Реестр контейнеров Azure** выберите реестр, который вы хотите проверить.
3. В этом реестре выберите **Репозитории**, чтобы просмотреть список всех репозиториев и соответствующих образов.













