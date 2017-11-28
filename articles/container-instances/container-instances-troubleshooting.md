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
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a><span data-ttu-id="29669-103">Устранение неполадок развертывания с помощью службы "Экземпляры контейнеров Azure"</span><span class="sxs-lookup"><span data-stu-id="29669-103">Troubleshoot deployment issues with Azure Container Instances</span></span>

<span data-ttu-id="29669-104">В этой статье показано, как tootroubleshoot проблемы при развертывании контейнеров tooAzure экземпляры контейнером.</span><span class="sxs-lookup"><span data-stu-id="29669-104">This article shows how tootroubleshoot issues when deploying containers tooAzure Container Instances.</span></span> <span data-ttu-id="29669-105">Здесь также описываются некоторые hello распространенных проблем, которые вы можете столкнуться.</span><span class="sxs-lookup"><span data-stu-id="29669-105">It also describes some of hello common issues you may run into.</span></span>

## <a name="getting-diagnostic-events"></a><span data-ttu-id="29669-106">Получение диагностических событий</span><span class="sxs-lookup"><span data-stu-id="29669-106">Getting diagnostic events</span></span>

<span data-ttu-id="29669-107">журналы tooview из кода приложения в контейнере, можно использовать hello [журналы контейнера az](/cli/azure/container#logs) команды.</span><span class="sxs-lookup"><span data-stu-id="29669-107">tooview logs from your application code within a container, you can use hello [az container logs](/cli/azure/container#logs) command.</span></span> <span data-ttu-id="29669-108">Но если не осуществляет развертывание контейнера, необходимо tooreview hello диагностических сведений, предоставляемых поставщика ресурсов Azure экземпляры контейнером hello.</span><span class="sxs-lookup"><span data-stu-id="29669-108">But if your container does not deploy successfully, you need tooreview hello diagnostic information provided by hello Azure Container Instances resource provider.</span></span> <span data-ttu-id="29669-109">tooview hello события для контейнера, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="29669-109">tooview hello events for your container, run hello following command:</span></span>

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

<span data-ttu-id="29669-110">Вывод Hello включает основные свойства hello своего контейнера, вместе с событиями развертывания.</span><span class="sxs-lookup"><span data-stu-id="29669-110">hello output includes hello core properties of your container, along with deployment events:</span></span>

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

## <a name="common-deployment-issues"></a><span data-ttu-id="29669-111">Стандартные проблемы развертывания</span><span class="sxs-lookup"><span data-stu-id="29669-111">Common deployment issues</span></span>

<span data-ttu-id="29669-112">Существует несколько типичных проблем, вызывающих большинство ошибок развертывания.</span><span class="sxs-lookup"><span data-stu-id="29669-112">There are a few common issues that account for most errors in deployment.</span></span>

### <a name="unable-toopull-image"></a><span data-ttu-id="29669-113">Не удается toopull изображения</span><span class="sxs-lookup"><span data-stu-id="29669-113">Unable toopull image</span></span>

<span data-ttu-id="29669-114">Если экземпляры контейнером Azure не удается toopull образ изначально повторяет за определенное перед неудачным со временем.</span><span class="sxs-lookup"><span data-stu-id="29669-114">If Azure Container Instances is unable toopull your image initially, it retries for some period before eventually failing.</span></span> <span data-ttu-id="29669-115">Если недоступный для извлечения изображения hello, отображаются события hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="29669-115">If hello image cannot be pulled, events like hello following are shown:</span></span>

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

<span data-ttu-id="29669-116">tooresolve, удаляйте hello и повторите попытку развертывания, правильно ввели имя образа hello плательщики особое внимание.</span><span class="sxs-lookup"><span data-stu-id="29669-116">tooresolve, delete hello container and retry your deployment, paying close attention that you have typed hello image name correctly.</span></span>

### <a name="container-continually-exits-and-restarts"></a><span data-ttu-id="29669-117">Контейнер постоянно завершает работу и перезагружается</span><span class="sxs-lookup"><span data-stu-id="29669-117">Container continually exits and restarts</span></span>

<span data-ttu-id="29669-118">Сейчас служба "Экземпляры контейнеров Azure" поддерживает только службы, выполняющиеся продолжительное время.</span><span class="sxs-lookup"><span data-stu-id="29669-118">Currently, Azure Container Instances only supports long-running services.</span></span> <span data-ttu-id="29669-119">Если контейнер запускается toocompletion и завершает работу, он автоматически перезагружается и запускается снова.</span><span class="sxs-lookup"><span data-stu-id="29669-119">If your container runs toocompletion and exits, it automatically restarts and runs again.</span></span> <span data-ttu-id="29669-120">В этом случае отображаются следующие события.</span><span class="sxs-lookup"><span data-stu-id="29669-120">If this happens, events like those following are shown.</span></span> <span data-ttu-id="29669-121">Обратите внимание, этот контейнер hello успешно запускается, а затем перезапускает быстро.</span><span class="sxs-lookup"><span data-stu-id="29669-121">Note that hello container successfully starts, then quickly restarts.</span></span> <span data-ttu-id="29669-122">Hello API экземпляры контейнером включает `retryCount` перезапустится, и свойство, которое показывает, сколько раз конкретного контейнера.</span><span class="sxs-lookup"><span data-stu-id="29669-122">hello Container Instances API includes a `retryCount` property that shows how many times a particular container has restarted.</span></span>

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
> <span data-ttu-id="29669-123">Большинство образы контейнеров для ОС Linux оболочки, таких как bash, установите в качестве команды по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="29669-123">Most container images for Linux distributions set a shell, such as bash, as hello default command.</span></span> <span data-ttu-id="29669-124">Так как оболочка сама по себе не является службой, выполняющейся продолжительное время, эти контейнеры немедленно завершают работу и попадают в цикл перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="29669-124">Since a shell on its own is not a long-running service, these containers immediately exit and fall into a restart loop.</span></span>

### <a name="container-takes-a-long-time-toostart"></a><span data-ttu-id="29669-125">Контейнер принимает toostart длительное время</span><span class="sxs-lookup"><span data-stu-id="29669-125">Container takes a long time toostart</span></span>

<span data-ttu-id="29669-126">Если контейнер принимает toostart много времени, но выполнится успешно, сначала рассматривается hello размер образа контейнера.</span><span class="sxs-lookup"><span data-stu-id="29669-126">If your container takes a long time toostart, but eventually succeeds, start by looking at hello size of your container image.</span></span> <span data-ttu-id="29669-127">Так как экземпляры контейнером Azure извлекает образ контейнера по требованию, время запуска hello возникают — непосредственно связанная tooits размер.</span><span class="sxs-lookup"><span data-stu-id="29669-127">Because Azure Container Instances pulls your container image on demand, hello startup time you experience is directly related tooits size.</span></span>

<span data-ttu-id="29669-128">Вы можете просмотреть hello размер образа контейнера с помощью hello Docker CLI:</span><span class="sxs-lookup"><span data-stu-id="29669-128">You can view hello size of your container image using hello Docker CLI:</span></span>

```bash
docker images
```

<span data-ttu-id="29669-129">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="29669-129">Output:</span></span>

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

<span data-ttu-id="29669-130">размер ключа tookeeping изображений Hello небольшой является обеспечение что окончательного образа не содержит все компоненты, не используется во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="29669-130">hello key tookeeping image sizes small is ensuring that your final image does not contain anything that is not required at runtime.</span></span> <span data-ttu-id="29669-131">Одним из способов toodo, это [построений многоэтапным](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span><span class="sxs-lookup"><span data-stu-id="29669-131">One way toodo this is with [multi-stage builds](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span></span> <span data-ttu-id="29669-132">Сборки многоэтапным сделать его легко tooensure hello итоговый образ содержит только hello артефакты, необходимые для вашего приложения, которое не любой из дополнительных hello содержимого, которое требовалось во время построения.</span><span class="sxs-lookup"><span data-stu-id="29669-132">Multi-stage builds make it easy tooensure that hello final image contains only hello artifacts you need for your application, and not any of hello extra content that was required at build time.</span></span>

<span data-ttu-id="29669-133">Hello других способом tooreduce hello воздействии hello запросу изображения на время запуска контейнера, с помощью hello Azure контейнер реестра в hello образ контейнера hello toohost же регионе, где планируется toouse экземпляров контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="29669-133">hello other way tooreduce hello impact of hello image pull on your container's startup time is toohost hello container image using hello Azure Container Registry in hello same region where you intend toouse Azure Container Instances.</span></span> <span data-ttu-id="29669-134">Это позволит сократить hello сетевой путь, hello tootravel потребностей образ контейнера, значительно сократить время загрузки hello.</span><span class="sxs-lookup"><span data-stu-id="29669-134">This shortens hello network path that hello container image needs tootravel, significantly shortening hello download time.</span></span>
