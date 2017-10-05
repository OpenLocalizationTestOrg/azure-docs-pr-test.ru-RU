---
title: "Создание службы Marathon с настройками для приложения или пользователя | Документация Майкрософт"
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
ms.openlocfilehash: b265763fb5dad240edd710cd8d0fb1079e3a7b51
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="2bcf5-104">Создание службы Marathon с настройками для приложения или пользователя</span><span class="sxs-lookup"><span data-stu-id="2bcf5-104">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="2bcf5-105">Служба контейнеров Azure предоставляет набор главных серверов с предварительно настроенными решениями Apache Mesos и Marathon.</span><span class="sxs-lookup"><span data-stu-id="2bcf5-105">Azure Container Service provides a set of master servers on which we preconfigure Apache Mesos and Marathon.</span></span> <span data-ttu-id="2bcf5-106">Их можно использовать для оркестрации приложений в кластере, но для этого не рекомендуется использовать главные серверы.</span><span class="sxs-lookup"><span data-stu-id="2bcf5-106">These can be used to orchestrate your applications on the cluster, but it's best not to use the master servers for this purpose.</span></span> <span data-ttu-id="2bcf5-107">Например, чтобы изменить конфигурацию Marathon, нужно сначала войти на главный сервер. В таком случае можно использовать специальные главные серверы, которые немного отличаются от стандартных и которыми можно управлять независимо.</span><span class="sxs-lookup"><span data-stu-id="2bcf5-107">For example, tweaking the configuration of Marathon requires logging into the master servers themselves and making changes--this encourages unique master servers that are a little different from the standard and need to be cared for and managed independently.</span></span> <span data-ttu-id="2bcf5-108">Кроме того, конфигурация, которая требуется одной группе пользователей, может оказаться неподходящей для другой.</span><span class="sxs-lookup"><span data-stu-id="2bcf5-108">Additionally, the configuration required by one team might not be the optimal configuration for another team.</span></span>

<span data-ttu-id="2bcf5-109">В этой статье мы объясним, как добавить службу Marathon с настройками для определенного пользователя или приложения.</span><span class="sxs-lookup"><span data-stu-id="2bcf5-109">In this article, we'll explain how to add an application or user-specific Marathon service.</span></span>

<span data-ttu-id="2bcf5-110">Так как эта службу будет использовать один пользователь или группа пользователей, ее можно настроить любым способом.</span><span class="sxs-lookup"><span data-stu-id="2bcf5-110">Because this service will belong to a single user or team, they are free to configure it in any way that they desire.</span></span> <span data-ttu-id="2bcf5-111">Кроме того, служба контейнеров Azure гарантирует бесперебойную работу службы.</span><span class="sxs-lookup"><span data-stu-id="2bcf5-111">Also, Azure Container Service will ensure that the service continues to run.</span></span> <span data-ttu-id="2bcf5-112">В случае сбоя службы служба контейнеров Azure перезапустит ее.</span><span class="sxs-lookup"><span data-stu-id="2bcf5-112">If the service fails, Azure Container Service will restart it for you.</span></span> <span data-ttu-id="2bcf5-113">В большинстве таких случаев вы вообще ничего не заметите.</span><span class="sxs-lookup"><span data-stu-id="2bcf5-113">Most of the time you won't even notice it had downtime.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2bcf5-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2bcf5-114">Prerequisites</span></span>
<span data-ttu-id="2bcf5-115">[Разверните экземпляр службы контейнеров Azure](container-service-deployment.md) с типом оркестратора DC/OS и [подключите клиент к кластеру](../container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="2bcf5-115">[Deploy an instance of Azure Container Service](container-service-deployment.md) with orchestrator type DC/OS and  [ensure that your client can connect to your cluster](../container-service-connect.md).</span></span> <span data-ttu-id="2bcf5-116">Кроме того, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2bcf5-116">Also, do the following steps.</span></span>

[!INCLUDE [install the DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="2bcf5-117">Создание службы Marathon с настройками для приложения или пользователя</span><span class="sxs-lookup"><span data-stu-id="2bcf5-117">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="2bcf5-118">Сначала создайте файл конфигурации JSON, который определяет имя создаваемой службы приложений.</span><span class="sxs-lookup"><span data-stu-id="2bcf5-118">Begin by creating a JSON configuration file that defines the name of the application service that you want to create.</span></span> <span data-ttu-id="2bcf5-119">В нашем примере используется `marathon-alice` в качестве имени платформы.</span><span class="sxs-lookup"><span data-stu-id="2bcf5-119">Here we use `marathon-alice` as the framework name.</span></span> <span data-ttu-id="2bcf5-120">Сохраните файл `marathon-alice.json`:</span><span class="sxs-lookup"><span data-stu-id="2bcf5-120">Save the file as something like `marathon-alice.json`:</span></span>

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

<span data-ttu-id="2bcf5-121">Теперь с помощью интерфейса командной строки DC/OS установите экземпляр Marathon с параметрами, указанными в файле конфигурации:</span><span class="sxs-lookup"><span data-stu-id="2bcf5-121">Next, use the DC/OS CLI to install the Marathon instance with the options that are set in your configuration file:</span></span>

```bash
dcos package install --options=marathon-alice.json marathon
```

<span data-ttu-id="2bcf5-122">На вкладке "Службы" пользовательского интерфейса DC/OS должна отобразиться запущенная служба `marathon-alice` .</span><span class="sxs-lookup"><span data-stu-id="2bcf5-122">You should now see your `marathon-alice` service running in the Services tab of your DC/OS UI.</span></span> <span data-ttu-id="2bcf5-123">Пользовательский интерфейс доступен по адресу `http://<hostname>/service/marathon-alice/` .</span><span class="sxs-lookup"><span data-stu-id="2bcf5-123">The UI will be `http://<hostname>/service/marathon-alice/` if you want to access it directly.</span></span>

## <a name="set-the-dcos-cli-to-access-the-service"></a><span data-ttu-id="2bcf5-124">Настройка интерфейса командной строки DC/OS для доступа к службе</span><span class="sxs-lookup"><span data-stu-id="2bcf5-124">Set the DC/OS CLI to access the service</span></span>
<span data-ttu-id="2bcf5-125">При необходимости можно настроить интерфейс командной строки DC/OS для доступа к этой новой службе. Для этого нужно, чтобы свойство `marathon.url` указывало на экземпляр `marathon-alice`:</span><span class="sxs-lookup"><span data-stu-id="2bcf5-125">You can optionally configure your DC/OS CLI to access this new service by setting the `marathon.url` property to point to the `marathon-alice` instance as follows:</span></span>

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

<span data-ttu-id="2bcf5-126">Вы можете проверить, для какого экземпляра Marathon в интерфейсе командной строки выполняется команда `dcos config show` .</span><span class="sxs-lookup"><span data-stu-id="2bcf5-126">You can verify which instance of Marathon that your CLI is working against with the `dcos config show` command.</span></span> <span data-ttu-id="2bcf5-127">Также вы можете вернуться к использованию службы Marathon на главном сервере с помощью команды `dcos config unset marathon.url`.</span><span class="sxs-lookup"><span data-stu-id="2bcf5-127">You can revert to using your master Marathon service with the command `dcos config unset marathon.url`.</span></span>

