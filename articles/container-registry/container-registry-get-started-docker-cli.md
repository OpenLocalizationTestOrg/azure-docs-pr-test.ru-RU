---
title: "Отправка образа Docker в частный реестр Azure | Документация Майкрософт"
description: "Отправка образов Docker в частный реестр контейнеров в Azure и их получение с помощью интерфейса командной строки Docker"
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
ms.openlocfilehash: 07d4d72e94eda02e8594dfddb0e911eb0e63012d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="push-your-first-image-to-a-private-docker-container-registry-using-the-docker-cli"></a><span data-ttu-id="7237d-103">Отправка первого образа в частный реестр контейнеров Docker с помощью интерфейса командной строки Docker</span><span class="sxs-lookup"><span data-stu-id="7237d-103">Push your first image to a private Docker container registry using the Docker CLI</span></span>
<span data-ttu-id="7237d-104">В реестре контейнеров Azure хранятся частные образы контейнеров [Docker](http://hub.docker.com), а также осуществляется управление ими (подобно тому, как в [Docker Hub](https://hub.docker.com/) хранятся общедоступные образы Docker).</span><span class="sxs-lookup"><span data-stu-id="7237d-104">An Azure container registry stores and manages private [Docker](http://hub.docker.com) container images, similar to the way [Docker Hub](https://hub.docker.com/) stores public Docker images.</span></span> <span data-ttu-id="7237d-105">[Интерфейс командной строки Docker](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) позволяет [входить](https://docs.docker.com/engine/reference/commandline/login/) в реестр контейнеров, а также выполнять [отправку](https://docs.docker.com/engine/reference/commandline/push/), [получение](https://docs.docker.com/engine/reference/commandline/pull/) и другие операции.</span><span class="sxs-lookup"><span data-stu-id="7237d-105">You use the [Docker Command-Line Interface](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) for [login](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/), and other operations on your container registry.</span></span>

<span data-ttu-id="7237d-106">Общие сведения и основные понятия см. в статье [Общие сведения о службе реестра контейнеров Azure](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="7237d-106">For more background and concepts, see [the overview](container-registry-intro.md)</span></span>



## <a name="prerequisites"></a><span data-ttu-id="7237d-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7237d-107">Prerequisites</span></span>
* <span data-ttu-id="7237d-108">**Реестр контейнеров Azure.** Создайте реестр контейнеров в своей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="7237d-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="7237d-109">Это можно сделать на [портале Azure](container-registry-get-started-portal.md) или с помощью [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7237d-109">For example, use the [Azure portal](container-registry-get-started-portal.md) or the [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="7237d-110">**Интерфейс командной строки Docker.** Установите [подсистему Docker](https://docs.docker.com/engine/installation/), чтобы настроить локальный компьютер в качестве узла Docker и получить доступ к командам интерфейса командной строки Docker.</span><span class="sxs-lookup"><span data-stu-id="7237d-110">**Docker CLI** - To set up your local computer as a Docker host and access the Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>

## <a name="log-in-to-a-registry"></a><span data-ttu-id="7237d-111">Вход в раздел реестра</span><span class="sxs-lookup"><span data-stu-id="7237d-111">Log in to a registry</span></span>
<span data-ttu-id="7237d-112">Выполните команду `docker login`, чтобы войти в реестр контейнеров с помощью [учетных данных реестра](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7237d-112">Run `docker login` to log in to your container registry with your [registry credentials](container-registry-authentication.md).</span></span>

<span data-ttu-id="7237d-113">Следующая команда передает идентификатор и пароль [субъекта-службы](../active-directory/active-directory-application-objects.md) Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7237d-113">The following example passes the ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="7237d-114">Например, назначение субъекта-службы для реестра позволяет автоматизировать некоторые сценарии.</span><span class="sxs-lookup"><span data-stu-id="7237d-114">For example, you might have assigned a service principal to your registry for an automation scenario.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> <span data-ttu-id="7237d-115">Укажите полное доменное имя реестра (все знаки в нижнем регистре).</span><span class="sxs-lookup"><span data-stu-id="7237d-115">Make sure to specify the fully qualified registry name (all lowercase).</span></span> <span data-ttu-id="7237d-116">В нашем примере поисковый запрос будет выглядеть так: `myregistry.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="7237d-116">In this example, it is `myregistry.azurecr.io`.</span></span>

## <a name="steps-to-pull-and-push-an-image"></a><span data-ttu-id="7237d-117">Отправка и получение образов</span><span class="sxs-lookup"><span data-stu-id="7237d-117">Steps to pull and push an image</span></span>
<span data-ttu-id="7237d-118">Следующий пример позволяет скачать образ Nginx из общедоступного реестра Docker Hub, поместить его в частный реестр контейнеров Azure, отправить его в свой реестр, а затем снова извлечь.</span><span class="sxs-lookup"><span data-stu-id="7237d-118">The follow example downloads the Nginx image from the public Docker Hub registry, tags it for your private Azure container registry, pushes it to your registry, then pulls it again.</span></span>

<span data-ttu-id="7237d-119">**1. Получите официальный образ Docker для Nginx.**</span><span class="sxs-lookup"><span data-stu-id="7237d-119">**1. Pull the Docker official image for Nginx**</span></span>

<span data-ttu-id="7237d-120">Сначала общедоступный образ Nginx нужно отправить на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="7237d-120">First pull the public Nginx image to your local computer.</span></span>

```
docker pull nginx
```
<span data-ttu-id="7237d-121">**2. Запустите контейнер Nginx.**</span><span class="sxs-lookup"><span data-stu-id="7237d-121">**2. Start the Nginx container**</span></span>

<span data-ttu-id="7237d-122">Следующая команда запускает локальный контейнер Nginx в интерактивном режиме (для отображения выходных данных) и прослушивает порт 8080.</span><span class="sxs-lookup"><span data-stu-id="7237d-122">The following command starts the local Nginx container interactively on port 8080, allowing you to see output from Nginx.</span></span> <span data-ttu-id="7237d-123">После остановки запущенный контейнер удаляется.</span><span class="sxs-lookup"><span data-stu-id="7237d-123">It removes the running container once stopped.</span></span>

```
docker run -it --rm -p 8080:80 nginx
```

<span data-ttu-id="7237d-124">Перейдите по адресу [http://localhost:8080](http://localhost:8080), чтобы просмотреть запущенный контейнер.</span><span class="sxs-lookup"><span data-stu-id="7237d-124">Browse to [http://localhost:8080](http://localhost:8080) to view the running container.</span></span> <span data-ttu-id="7237d-125">Появится экран, аналогичный показанному ниже.</span><span class="sxs-lookup"><span data-stu-id="7237d-125">You see a screen similar to the following one.</span></span>

![Nginx на локальном компьютере](./media/container-registry-get-started-docker-cli/nginx.png)

<span data-ttu-id="7237d-127">Чтобы остановить запущенный контейнер, нажмите клавиши [CTRL]+[C].</span><span class="sxs-lookup"><span data-stu-id="7237d-127">To stop the running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="7237d-128">**3. Создайте псевдоним образа в реестре.**</span><span class="sxs-lookup"><span data-stu-id="7237d-128">**3. Create an alias of the image in your registry**</span></span>

<span data-ttu-id="7237d-129">Следующая команда создает псевдоним образа с полным путем к вашему реестру.</span><span class="sxs-lookup"><span data-stu-id="7237d-129">The following command creates an alias of the image, with a fully qualified path to your registry.</span></span> <span data-ttu-id="7237d-130">Чтобы избежать беспорядка в корне реестра, эта команда указывает пространство имен `samples`.</span><span class="sxs-lookup"><span data-stu-id="7237d-130">This example specifies the `samples` namespace to avoid clutter in the root of the registry.</span></span>

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

<span data-ttu-id="7237d-131">**4. Отправьте образ в реестр.**</span><span class="sxs-lookup"><span data-stu-id="7237d-131">**4. Push the image to your registry**</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="7237d-132">**5. Получите образ из реестра.**</span><span class="sxs-lookup"><span data-stu-id="7237d-132">**5. Pull the image from your registry**</span></span>

```
docker pull myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="7237d-133">**6. Запустите контейнер Nginx из реестра.**</span><span class="sxs-lookup"><span data-stu-id="7237d-133">**6. Start the Nginx container from your registry**</span></span>

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="7237d-134">Перейдите по адресу [http://localhost:8080](http://localhost:8080), чтобы просмотреть запущенный контейнер.</span><span class="sxs-lookup"><span data-stu-id="7237d-134">Browse to [http://localhost:8080](http://localhost:8080) to view the running container.</span></span>

<span data-ttu-id="7237d-135">Чтобы остановить запущенный контейнер, нажмите клавиши [CTRL]+[C].</span><span class="sxs-lookup"><span data-stu-id="7237d-135">To stop the running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="7237d-136">**7. (Необязательно) Удалите образ**</span><span class="sxs-lookup"><span data-stu-id="7237d-136">**7. (Optional) Remove the image**</span></span>

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a><span data-ttu-id="7237d-137">Ограничения на параллельную обработку</span><span class="sxs-lookup"><span data-stu-id="7237d-137">Concurrent Limits</span></span>
<span data-ttu-id="7237d-138">В некоторых случаях параллельное выполнение вызовов может привести к ошибкам.</span><span class="sxs-lookup"><span data-stu-id="7237d-138">In some scenarios, executing calls concurrently might result in errors.</span></span> <span data-ttu-id="7237d-139">В следующей таблице описаны ограничения на число одновременных вызовов для операций "Принудительная отправка" (PULL) "Извлечение" (PUSH) в реестре контейнера Azure:</span><span class="sxs-lookup"><span data-stu-id="7237d-139">The following table contains the limits of concurrent calls with "Push" and "Pull" operations on Azure container registry:</span></span>

| <span data-ttu-id="7237d-140">Операция</span><span class="sxs-lookup"><span data-stu-id="7237d-140">Operation</span></span>  | <span data-ttu-id="7237d-141">Ограничение</span><span class="sxs-lookup"><span data-stu-id="7237d-141">Limit</span></span>                                  |
| ---------- | -------------------------------------- |
| <span data-ttu-id="7237d-142">PULL</span><span class="sxs-lookup"><span data-stu-id="7237d-142">PULL</span></span>       | <span data-ttu-id="7237d-143">До 10 параллельных операций принудительной отправки на реестр.</span><span class="sxs-lookup"><span data-stu-id="7237d-143">Up to 10 concurrent pulls per registry</span></span> |
| <span data-ttu-id="7237d-144">PUSH</span><span class="sxs-lookup"><span data-stu-id="7237d-144">PUSH</span></span>       | <span data-ttu-id="7237d-145">До 5 параллельных операций извлечения на реестр.</span><span class="sxs-lookup"><span data-stu-id="7237d-145">Up to 5 concurrent pushes per registry</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7237d-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7237d-146">Next steps</span></span>
<span data-ttu-id="7237d-147">Теперь, когда вы знаете основы, можно приступать к использованию реестра.</span><span class="sxs-lookup"><span data-stu-id="7237d-147">Now that you know the basics, you are ready to start using your registry!</span></span> <span data-ttu-id="7237d-148">Например, разверните образы контейнера в кластер [службы контейнеров Azure](https://azure.microsoft.com/documentation/services/container-service/).</span><span class="sxs-lookup"><span data-stu-id="7237d-148">For example, start deploying container images to an [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
