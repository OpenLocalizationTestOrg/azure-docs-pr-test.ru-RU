---
title: "tooprivate образа Docker aaaPush реестра Azure | Документы Microsoft"
description: "По запросу и принудительные Docker реестра закрытый контейнер tooa образы в Azure с помощью hello Docker CLI"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 64fbe43f-fdde-4c17-a39a-d04f2d6d90a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a81a6f4bfcb23642a89ac7631348d40e2f4911a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="push-your-first-image-tooa-private-docker-container-registry-using-hello-docker-cli"></a><span data-ttu-id="03566-103">Первый изображения tooa закрытый Docker контейнер реестра hello Docker CLI с помощью принудительной отправки</span><span class="sxs-lookup"><span data-stu-id="03566-103">Push your first image tooa private Docker container registry using hello Docker CLI</span></span>
<span data-ttu-id="03566-104">В реестре контейнер Azure хранит данные и управляет закрытый [Docker](http://hub.docker.com) образы контейнеров, аналогичные toohello способом [Docker Hub](https://hub.docker.com/) хранит общедоступные образы Docker.</span><span class="sxs-lookup"><span data-stu-id="03566-104">An Azure container registry stores and manages private [Docker](http://hub.docker.com) container images, similar toohello way [Docker Hub](https://hub.docker.com/) stores public Docker images.</span></span> <span data-ttu-id="03566-105">Использовать hello [интерфейс командной строки Docker](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) для [входа](https://docs.docker.com/engine/reference/commandline/login/), [принудительной](https://docs.docker.com/engine/reference/commandline/push/), [запросу](https://docs.docker.com/engine/reference/commandline/pull/)и других операций в контейнер реестр.</span><span class="sxs-lookup"><span data-stu-id="03566-105">You use hello [Docker Command-Line Interface](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) for [login](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/), and other operations on your container registry.</span></span>

<span data-ttu-id="03566-106">Дополнительные сведения и основные понятия в разделе [Здравствуйте, Обзор](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="03566-106">For more background and concepts, see [hello overview](container-registry-intro.md)</span></span>



## <a name="prerequisites"></a><span data-ttu-id="03566-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="03566-107">Prerequisites</span></span>
* <span data-ttu-id="03566-108">**Реестр контейнеров Azure.** Создайте реестр контейнеров в своей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="03566-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="03566-109">Например, использовать hello [портал Azure](container-registry-get-started-portal.md) или hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="03566-109">For example, use hello [Azure portal](container-registry-get-started-portal.md) or hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="03566-110">**Docker CLI** -tooset ваш локальный компьютер как узла и доступа к hello Docker CLI команды Docker, установите [подсистемы Docker](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="03566-110">**Docker CLI** - tooset up your local computer as a Docker host and access hello Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>

## <a name="log-in-tooa-registry"></a><span data-ttu-id="03566-111">Войдите в реестре tooa</span><span class="sxs-lookup"><span data-stu-id="03566-111">Log in tooa registry</span></span>
<span data-ttu-id="03566-112">Запустите `docker login` toolog в реестре контейнеров tooyour с вашей [учетные данные реестра](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="03566-112">Run `docker login` toolog in tooyour container registry with your [registry credentials](container-registry-authentication.md).</span></span>

<span data-ttu-id="03566-113">Hello следующий пример hello ID и пароль передаются из Azure Active Directory [участника-службы](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="03566-113">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="03566-114">Например которые были назначены реестр службы основной tooyour сценария автоматизации.</span><span class="sxs-lookup"><span data-stu-id="03566-114">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> <span data-ttu-id="03566-115">Создать убедиться, что toospecify hello реестра полное имя (прописными буквами).</span><span class="sxs-lookup"><span data-stu-id="03566-115">Make sure toospecify hello fully qualified registry name (all lowercase).</span></span> <span data-ttu-id="03566-116">В нашем примере поисковый запрос будет выглядеть так: `myregistry.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="03566-116">In this example, it is `myregistry.azurecr.io`.</span></span>

## <a name="steps-toopull-and-push-an-image"></a><span data-ttu-id="03566-117">Toopull действия и отправка изображения</span><span class="sxs-lookup"><span data-stu-id="03566-117">Steps toopull and push an image</span></span>
<span data-ttu-id="03566-118">Hello выполнить пример, что загрузка hello Nginx изображения из реестра Docker Hub, открытого с hello, теги в реестр закрытый контейнер Azure, отправляющий ее tooyour реестра, а затем извлекает его еще раз.</span><span class="sxs-lookup"><span data-stu-id="03566-118">hello follow example downloads hello Nginx image from hello public Docker Hub registry, tags it for your private Azure container registry, pushes it tooyour registry, then pulls it again.</span></span>

<span data-ttu-id="03566-119">**1. Официальный образа Docker hello по запросу для Nginx**</span><span class="sxs-lookup"><span data-stu-id="03566-119">**1. Pull hello Docker official image for Nginx**</span></span>

<span data-ttu-id="03566-120">Сначала по запросу hello открытый Nginx tooyour локального компьютера-образца.</span><span class="sxs-lookup"><span data-stu-id="03566-120">First pull hello public Nginx image tooyour local computer.</span></span>

```
docker pull nginx
```
<span data-ttu-id="03566-121">**2. Запустите контейнер Nginx hello**</span><span class="sxs-lookup"><span data-stu-id="03566-121">**2. Start hello Nginx container**</span></span>

<span data-ttu-id="03566-122">Hello следующая команда запускает hello локального Nginx контейнера интерактивно через порт 8080, позволяя toosee вывод Nginx.</span><span class="sxs-lookup"><span data-stu-id="03566-122">hello following command starts hello local Nginx container interactively on port 8080, allowing you toosee output from Nginx.</span></span> <span data-ttu-id="03566-123">Удаляет контейнер после остановки запускается hello.</span><span class="sxs-lookup"><span data-stu-id="03566-123">It removes hello running container once stopped.</span></span>

```
docker run -it --rm -p 8080:80 nginx
```

<span data-ttu-id="03566-124">Обзор слишком[http://localhost: 8080](http://localhost:8080) tooview hello контейнер запускается.</span><span class="sxs-lookup"><span data-stu-id="03566-124">Browse too[http://localhost:8080](http://localhost:8080) tooview hello running container.</span></span> <span data-ttu-id="03566-125">Вы увидите примерно toohello экрана, выполнив одно.</span><span class="sxs-lookup"><span data-stu-id="03566-125">You see a screen similar toohello following one.</span></span>

![Nginx на локальном компьютере](./media/container-registry-get-started-docker-cli/nginx.png)

<span data-ttu-id="03566-127">toostop Здравствуйте запущенного контейнера, нажмите клавишу [CTRL] + [C].</span><span class="sxs-lookup"><span data-stu-id="03566-127">toostop hello running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="03566-128">**3. Создайте псевдоним hello изображения в реестре**</span><span class="sxs-lookup"><span data-stu-id="03566-128">**3. Create an alias of hello image in your registry**</span></span>

<span data-ttu-id="03566-129">Hello следующая команда создает псевдоним изображения hello с реестра tooyour полный путь.</span><span class="sxs-lookup"><span data-stu-id="03566-129">hello following command creates an alias of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="03566-130">В этом примере указывается hello `samples` перегруженность hello корень реестра hello tooavoid пространства имен.</span><span class="sxs-lookup"><span data-stu-id="03566-130">This example specifies hello `samples` namespace tooavoid clutter in hello root of hello registry.</span></span>

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

<span data-ttu-id="03566-131">**4. Изображение tooyour принудительной hello реестра**</span><span class="sxs-lookup"><span data-stu-id="03566-131">**4. Push hello image tooyour registry**</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="03566-132">**5. Изображение hello запросу из системного реестра**</span><span class="sxs-lookup"><span data-stu-id="03566-132">**5. Pull hello image from your registry**</span></span>

```
docker pull myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="03566-133">**6. Запустите контейнер Nginx hello из системного реестра**</span><span class="sxs-lookup"><span data-stu-id="03566-133">**6. Start hello Nginx container from your registry**</span></span>

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="03566-134">Обзор слишком[http://localhost: 8080](http://localhost:8080) tooview hello контейнер запускается.</span><span class="sxs-lookup"><span data-stu-id="03566-134">Browse too[http://localhost:8080](http://localhost:8080) tooview hello running container.</span></span>

<span data-ttu-id="03566-135">toostop Здравствуйте запущенного контейнера, нажмите клавишу [CTRL] + [C].</span><span class="sxs-lookup"><span data-stu-id="03566-135">toostop hello running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="03566-136">**7. (Необязательно) Удаление образа hello**</span><span class="sxs-lookup"><span data-stu-id="03566-136">**7. (Optional) Remove hello image**</span></span>

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a><span data-ttu-id="03566-137">Ограничения на параллельную обработку</span><span class="sxs-lookup"><span data-stu-id="03566-137">Concurrent Limits</span></span>
<span data-ttu-id="03566-138">В некоторых случаях параллельное выполнение вызовов может привести к ошибкам.</span><span class="sxs-lookup"><span data-stu-id="03566-138">In some scenarios, executing calls concurrently might result in errors.</span></span> <span data-ttu-id="03566-139">в следующей таблице Hello содержит hello ограничения количества одновременных вызовов «Push» и «Pull» операции на контейнер Azure реестра:</span><span class="sxs-lookup"><span data-stu-id="03566-139">hello following table contains hello limits of concurrent calls with "Push" and "Pull" operations on Azure container registry:</span></span>

| <span data-ttu-id="03566-140">Операция</span><span class="sxs-lookup"><span data-stu-id="03566-140">Operation</span></span>  | <span data-ttu-id="03566-141">Ограничение</span><span class="sxs-lookup"><span data-stu-id="03566-141">Limit</span></span>                                  |
| ---------- | -------------------------------------- |
| <span data-ttu-id="03566-142">PULL</span><span class="sxs-lookup"><span data-stu-id="03566-142">PULL</span></span>       | <span data-ttu-id="03566-143">Копирование too10 параллельных запрашивает в реестре</span><span class="sxs-lookup"><span data-stu-id="03566-143">Up too10 concurrent pulls per registry</span></span> |
| <span data-ttu-id="03566-144">PUSH</span><span class="sxs-lookup"><span data-stu-id="03566-144">PUSH</span></span>       | <span data-ttu-id="03566-145">Копирование too5 параллельных помещает в реестре</span><span class="sxs-lookup"><span data-stu-id="03566-145">Up too5 concurrent pushes per registry</span></span> |

## <a name="next-steps"></a><span data-ttu-id="03566-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="03566-146">Next steps</span></span>
<span data-ttu-id="03566-147">Теперь, вы знаете основы hello, все готово toostart, с помощью реестра!</span><span class="sxs-lookup"><span data-stu-id="03566-147">Now that you know hello basics, you are ready toostart using your registry!</span></span> <span data-ttu-id="03566-148">Например, начать развертывание контейнера изображений tooan [контейнера службы Azure](https://azure.microsoft.com/documentation/services/container-service/) кластера.</span><span class="sxs-lookup"><span data-stu-id="03566-148">For example, start deploying container images tooan [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
