---
title: "aaaApplication или пользовательские службы Marathon | Документы Microsoft"
description: "Создание службы Marathon с настройками для приложения или пользователя"
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Контейнеры, Marathon, микрослужбы, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 1e6f69ed64e113a3a059788a71ddb57b6d3ad8da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="02b70-104">Создание службы Marathon с настройками для приложения или пользователя</span><span class="sxs-lookup"><span data-stu-id="02b70-104">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="02b70-105">Служба контейнеров Azure предоставляет набор главных серверов с предварительно настроенными решениями Apache Mesos и Marathon.</span><span class="sxs-lookup"><span data-stu-id="02b70-105">Azure Container Service provides a set of master servers on which we preconfigure Apache Mesos and Marathon.</span></span> <span data-ttu-id="02b70-106">Это могут быть используется tooorchestrate приложений на кластере hello, но он является наилучшим образом не toouse hello главных серверов для этой цели.</span><span class="sxs-lookup"><span data-stu-id="02b70-106">These can be used tooorchestrate your applications on hello cluster, but it's best not toouse hello master servers for this purpose.</span></span> <span data-ttu-id="02b70-107">Например, изменение конфигурации hello Marathon требует регистрации в самих серверов master hello и внесения изменений — это поощряет уникальный главных серверов, немного отличаются от стандартных hello и необходимость toobe карточки для и управляемых независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="02b70-107">For example, tweaking hello configuration of Marathon requires logging into hello master servers themselves and making changes--this encourages unique master servers that are a little different from hello standard and need toobe cared for and managed independently.</span></span> <span data-ttu-id="02b70-108">Кроме того hello конфигурацию, необходимую для одной группы может быть hello оптимальной конфигурации для другой команды.</span><span class="sxs-lookup"><span data-stu-id="02b70-108">Additionally, hello configuration required by one team might not be hello optimal configuration for another team.</span></span>

<span data-ttu-id="02b70-109">В этой статье объясняется, как tooadd службу Marathon приложения или конкретного пользователя.</span><span class="sxs-lookup"><span data-stu-id="02b70-109">In this article, we'll explain how tooadd an application or user-specific Marathon service.</span></span>

<span data-ttu-id="02b70-110">Так как эта служба будет принадлежать tooa одного пользователя или группы, они могут бесплатно tooconfigure его каким-либо образом, что пожелает.</span><span class="sxs-lookup"><span data-stu-id="02b70-110">Because this service will belong tooa single user or team, they are free tooconfigure it in any way that they desire.</span></span> <span data-ttu-id="02b70-111">Кроме того служба контейнера Azure будет гарантировать, что служба hello сохраняется toorun.</span><span class="sxs-lookup"><span data-stu-id="02b70-111">Also, Azure Container Service will ensure that hello service continues toorun.</span></span> <span data-ttu-id="02b70-112">Если происходит сбой службы hello, Azure контейнера служба будет перезапущена его автоматически.</span><span class="sxs-lookup"><span data-stu-id="02b70-112">If hello service fails, Azure Container Service will restart it for you.</span></span> <span data-ttu-id="02b70-113">Большую часть времени hello вы не даже Обратите внимание, что за время простоя.</span><span class="sxs-lookup"><span data-stu-id="02b70-113">Most of hello time you won't even notice it had downtime.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02b70-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="02b70-114">Prerequisites</span></span>
<span data-ttu-id="02b70-115">[Разверните экземпляр службы Azure контейнера](container-service-deployment.md) с orchestrator введите DC/OS и [убедитесь, что ваш клиент может подключаться кластера tooyour](../container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="02b70-115">[Deploy an instance of Azure Container Service](container-service-deployment.md) with orchestrator type DC/OS and  [ensure that your client can connect tooyour cluster](../container-service-connect.md).</span></span> <span data-ttu-id="02b70-116">Кроме того hello следующие действия.</span><span class="sxs-lookup"><span data-stu-id="02b70-116">Also, do hello following steps.</span></span>

[!INCLUDE [install hello DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="02b70-117">Создание службы Marathon с настройками для приложения или пользователя</span><span class="sxs-lookup"><span data-stu-id="02b70-117">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="02b70-118">Начните с создания файла конфигурации JSON, который определяет имя службы приложения hello, что требуется toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="02b70-118">Begin by creating a JSON configuration file that defines hello name of hello application service that you want toocreate.</span></span> <span data-ttu-id="02b70-119">Здесь мы используем `marathon-alice` как hello имя платформы.</span><span class="sxs-lookup"><span data-stu-id="02b70-119">Here we use `marathon-alice` as hello framework name.</span></span> <span data-ttu-id="02b70-120">Сохраните файл hello наподобие `marathon-alice.json`:</span><span class="sxs-lookup"><span data-stu-id="02b70-120">Save hello file as something like `marathon-alice.json`:</span></span>

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

<span data-ttu-id="02b70-121">Затем выполните hello CLI DC/OS tooinstall hello Marathon экземпляра с параметрами hello, которые заданы в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="02b70-121">Next, use hello DC/OS CLI tooinstall hello Marathon instance with hello options that are set in your configuration file:</span></span>

```bash
dcos package install --options=marathon-alice.json marathon
```

<span data-ttu-id="02b70-122">Теперь вы увидите вашей `marathon-alice` службе, запущенной на вкладке hello службы контроллера домена/OS пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="02b70-122">You should now see your `marathon-alice` service running in hello Services tab of your DC/OS UI.</span></span> <span data-ttu-id="02b70-123">Hello пользовательского интерфейса будет `http://<hostname>/service/marathon-alice/` Если tooaccess напрямую.</span><span class="sxs-lookup"><span data-stu-id="02b70-123">hello UI will be `http://<hostname>/service/marathon-alice/` if you want tooaccess it directly.</span></span>

## <a name="set-hello-dcos-cli-tooaccess-hello-service"></a><span data-ttu-id="02b70-124">Настройте tooaccess CLI DC/OS hello hello</span><span class="sxs-lookup"><span data-stu-id="02b70-124">Set hello DC/OS CLI tooaccess hello service</span></span>
<span data-ttu-id="02b70-125">Также можно настроить вашей tooaccess CLI DC/OS новой службы, Настройка hello `marathon.url` toohello toopoint свойство `marathon-alice` экземпляра следующим образом:</span><span class="sxs-lookup"><span data-stu-id="02b70-125">You can optionally configure your DC/OS CLI tooaccess this new service by setting hello `marathon.url` property toopoint toohello `marathon-alice` instance as follows:</span></span>

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

<span data-ttu-id="02b70-126">Можно проверить, какой экземпляр Marathon, ваш CLI работает с hello `dcos config show` команды.</span><span class="sxs-lookup"><span data-stu-id="02b70-126">You can verify which instance of Marathon that your CLI is working against with hello `dcos config show` command.</span></span> <span data-ttu-id="02b70-127">Вы можете восстановить toousing master Marathon службы с помощью команды hello `dcos config unset marathon.url`.</span><span class="sxs-lookup"><span data-stu-id="02b70-127">You can revert toousing your master Marathon service with hello command `dcos config unset marathon.url`.</span></span>

