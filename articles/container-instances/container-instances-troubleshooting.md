---
title: "aaaTroubleshooting экземпляров контейнера Azure"
description: "Узнайте, как tootroubleshoot проблемы с экземплярами контейнера Azure"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/03/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: dfec636a0a174c74a6f2e9d9c4da6e871f8d2fda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a>Устранение неполадок развертывания с помощью службы "Экземпляры контейнеров Azure"

В этой статье показано, как tootroubleshoot проблемы при развертывании контейнеров tooAzure экземпляры контейнером. Здесь также описываются некоторые hello распространенных проблем, которые вы можете столкнуться.

## <a name="getting-diagnostic-events"></a>Получение диагностических событий

журналы tooview из кода приложения в контейнере, можно использовать hello [журналы контейнера az](/cli/azure/container#logs) команды. Но если не осуществляет развертывание контейнера, необходимо tooreview hello диагностических сведений, предоставляемых поставщика ресурсов Azure экземпляры контейнером hello. tooview hello события для контейнера, запустите hello следующую команду:

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

Вывод Hello включает основные свойства hello своего контейнера, вместе с событиями развертывания.

```bash
{
  "containers": [
    {
      "command": null,
      "environmentVariables": [],
      "image": "microsoft/aci-helloworld",
      ...

      "events": [
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:52+00:00",
        "lastTimestamp": "2017-08-03T22:12:52+00:00",
        "message": "Pulling: pulling image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Pulled: Successfully pulled image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Created: Created container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Started: Started container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      }
    ],
    "name": "helloworld",
      "ports": [
        {
          "port": 80
        }
      ],
    ...
  ]
}
```

## <a name="common-deployment-issues"></a>Стандартные проблемы развертывания

Существует несколько типичных проблем, вызывающих большинство ошибок развертывания.

### <a name="unable-toopull-image"></a>Не удается toopull изображения

Если экземпляры контейнером Azure не удается toopull образ изначально повторяет за определенное перед неудачным со временем. Если недоступный для извлечения изображения hello, отображаются события hello следующим образом:

```bash
"events": [
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:31+00:00",
    "lastTimestamp": "2017-08-03T22:19:31+00:00",
    "message": "Pulling: pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:32+00:00",
    "lastTimestamp": "2017-08-03T22:19:32+00:00",
    "message": "Failed: Failed toopull image \"microsoft/aci-hellowrld\": rpc error: code 2 desc Error: image microsoft/aci-hellowrld:latest not found",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:33+00:00",
    "lastTimestamp": "2017-08-03T22:19:33+00:00",
    "message": "BackOff: Back-off pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  }
]
```

tooresolve, удаляйте hello и повторите попытку развертывания, правильно ввели имя образа hello плательщики особое внимание.

### <a name="container-continually-exits-and-restarts"></a>Контейнер постоянно завершает работу и перезагружается

Сейчас служба "Экземпляры контейнеров Azure" поддерживает только службы, выполняющиеся продолжительное время. Если контейнер запускается toocompletion и завершает работу, он автоматически перезагружается и запускается снова. В этом случае отображаются следующие события. Обратите внимание, этот контейнер hello успешно запускается, а затем перезапускает быстро. Hello API экземпляры контейнером включает `retryCount` перезапустится, и свойство, которое показывает, сколько раз конкретного контейнера.

```bash
"events": [
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:55+00:00",
    "lastTimestamp": "2017-08-03T22:23:22+00:00",
    "message": "Pulling: pulling image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:23:23+00:00",
    "message": "Pulled: Successfully pulled image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Created: Created container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Started: Started container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Created: Created container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Started: Started container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 13,
    "firstTimestamp": "2017-08-03T22:21:59+00:00",
    "lastTimestamp": "2017-08-03T22:24:36+00:00",
    "message": "BackOff: Back-off restarting failed container",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:22:13+00:00",
    "lastTimestamp": "2017-08-03T22:22:13+00:00",
    "message": "Created: Created container with id 72e347e891290e238135e4a6b3078748ca25a1275dbbff30d8d214f026d89220",
    "type": "Normal"
  },
  ...
```

> [!NOTE]
> Большинство образы контейнеров для ОС Linux оболочки, таких как bash, установите в качестве команды по умолчанию hello. Так как оболочка сама по себе не является службой, выполняющейся продолжительное время, эти контейнеры немедленно завершают работу и попадают в цикл перезагрузки.

### <a name="container-takes-a-long-time-toostart"></a>Контейнер принимает toostart длительное время

Если контейнер принимает toostart много времени, но выполнится успешно, сначала рассматривается hello размер образа контейнера. Так как экземпляры контейнером Azure извлекает образ контейнера по требованию, время запуска hello возникают — непосредственно связанная tooits размер.

Вы можете просмотреть hello размер образа контейнера с помощью hello Docker CLI:

```bash
docker images
```

Выходные данные:

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

размер ключа tookeeping изображений Hello небольшой является обеспечение что окончательного образа не содержит все компоненты, не используется во время выполнения. Одним из способов toodo, это [построений многоэтапным](https://docs.docker.com/engine/userguide/eng-image/multistage-build/). Сборки многоэтапным сделать его легко tooensure hello итоговый образ содержит только hello артефакты, необходимые для вашего приложения, которое не любой из дополнительных hello содержимого, которое требовалось во время построения.

Hello других способом tooreduce hello воздействии hello запросу изображения на время запуска контейнера, с помощью hello Azure контейнер реестра в hello образ контейнера hello toohost же регионе, где планируется toouse экземпляров контейнера Azure. Это позволит сократить hello сетевой путь, hello tootravel потребностей образ контейнера, значительно сократить время загрузки hello.
