---
title: "aaaAzure контейнер реестра репозиториев | Документы Microsoft"
description: "Как toouse репозиториями реестра контейнера Azure для Docker images"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: cristyg
ms.openlocfilehash: 108622c565e41777fbb1fc9da9a01168abc7a7fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="73cf4-103">Репозитории реестра контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="73cf4-103">Azure container registry repositories</span></span>

<span data-ttu-id="73cf4-104">Контейнер Azure реестра позволяет toostore образы контейнеров в репозитории.</span><span class="sxs-lookup"><span data-stu-id="73cf4-104">Azure container registry allows you toostore container images in repositories.</span></span> <span data-ttu-id="73cf4-105">Это позволяет содержать группы образов (версии образов) в изолированных средах.</span><span class="sxs-lookup"><span data-stu-id="73cf4-105">By storing images in repositories, you can have groups of images (or version of images) in isolated environments.</span></span> <span data-ttu-id="73cf4-106">При выполнении отправки изображений tooyour реестра можно указать эти репозиториев.</span><span class="sxs-lookup"><span data-stu-id="73cf4-106">You can specify these repositories when you push images tooyour registry.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="73cf4-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="73cf4-107">Prerequisites</span></span>
* <span data-ttu-id="73cf4-108">**Реестр контейнеров Azure.** Создайте реестр контейнеров в своей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="73cf4-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="73cf4-109">Например, использовать hello [портал Azure](container-registry-get-started-portal.md) или hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="73cf4-109">For example, use hello [Azure portal](container-registry-get-started-portal.md) or hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="73cf4-110">**Docker CLI** -tooset ваш локальный компьютер как узла и доступа к hello Docker CLI команды Docker, установите [подсистемы Docker](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="73cf4-110">**Docker CLI** - tooset up your local computer as a Docker host and access hello Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>
* <span data-ttu-id="73cf4-111">**Изображение по запросу** — извлечь изображение из открытого реестра Docker Hub hello пометить ее и принудительно отправить его tooyour реестра.</span><span class="sxs-lookup"><span data-stu-id="73cf4-111">**Pull an image** - Pull an image from hello public Docker Hub registry, tag it, and push it tooyour registry.</span></span> <span data-ttu-id="73cf4-112">Рекомендации о том, как push и pull образов см. в разделе [Push Docker изображения tooAzure частного реестра](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="73cf4-112">For guidance on how push and pull images, see [Push Docker image tooAzure private registry](container-registry-get-started-docker-cli.md).</span></span>


## <a name="viewing-repositories-in-hello-portal"></a><span data-ttu-id="73cf4-113">Просмотр репозитории в hello портала</span><span class="sxs-lookup"><span data-stu-id="73cf4-113">Viewing repositories in hello Portal</span></span>

<span data-ttu-id="73cf4-114">После помещается реестра контейнера tooyour изображения, можно просмотреть список репозиториев hello размещение изображений hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="73cf4-114">Once you have pushed images tooyour container registry, you can see a list of hello repositories hosting hello images in hello Azure portal.</span></span>

<span data-ttu-id="73cf4-115">Если вы следовали инструкциям hello hello [Push Docker изображения tooAzure частного реестра](container-registry-get-started-docker-cli.md) статьи, вы добавили изображения Nginx в реестре контейнера.</span><span class="sxs-lookup"><span data-stu-id="73cf4-115">If you followed hello steps in hello [Push Docker image tooAzure private registry](container-registry-get-started-docker-cli.md) article, you should now have a Nginx image in your container registry.</span></span> <span data-ttu-id="73cf4-116">Как часть инструкции hello следует указано пространство имен для hello изображения.</span><span class="sxs-lookup"><span data-stu-id="73cf4-116">As part of hello instructions, you should have specified a namespace for hello image.</span></span> <span data-ttu-id="73cf4-117">В следующем примере hello команда hello помещает репозитория hello NGinx образов toohello «samples»:</span><span class="sxs-lookup"><span data-stu-id="73cf4-117">In hello example below, hello command pushes hello NGinx image toohello "samples" repository:</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```
 <span data-ttu-id="73cf4-118">Реестр контейнеров Azure поддерживает многоуровневые пространства имен для репозитория.</span><span class="sxs-lookup"><span data-stu-id="73cf4-118">Azure Container Registry supports multilevel repository namespaces.</span></span> <span data-ttu-id="73cf4-119">Эта функция позволяет вам toogroup коллекции изображений связанные tooa определенного приложения или коллекции toospecific разработки приложений или рабочей группы.</span><span class="sxs-lookup"><span data-stu-id="73cf4-119">This feature enables you toogroup collections of images related tooa specific app, or a collection of apps toospecific development or operational teams.</span></span> <span data-ttu-id="73cf4-120">tooread Дополнительные сведения о репозитории в контейнера реестры, в разделе [Docker закрытого контейнера реестры в Azure](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="73cf4-120">tooread more about repositories in container registries, see [Private Docker container registries in Azure](container-registry-intro.md).</span></span>

<span data-ttu-id="73cf4-121">tooview hello контейнер реестра хранилища:</span><span class="sxs-lookup"><span data-stu-id="73cf4-121">tooview hello container registry repositories:</span></span>

1. <span data-ttu-id="73cf4-122">Войдите в toohello портал Azure</span><span class="sxs-lookup"><span data-stu-id="73cf4-122">Log in toohello Azure portal</span></span>
2. <span data-ttu-id="73cf4-123">На hello **реестра контейнера Azure** колонку, вы хотите tooinspect реестра выберите hello</span><span class="sxs-lookup"><span data-stu-id="73cf4-123">On hello **Azure Container Registry** blade, select hello registry you wish tooinspect</span></span>
3. <span data-ttu-id="73cf4-124">В колонке hello реестра щелкните **репозиториев** toosee список всех репозиториев hello и изображений</span><span class="sxs-lookup"><span data-stu-id="73cf4-124">In hello registry blade, click **Repositories** toosee a list of all hello repositories and their images</span></span>
4. <span data-ttu-id="73cf4-125">(Необязательно) Выберите теги toosee определенного образа</span><span class="sxs-lookup"><span data-stu-id="73cf4-125">(Optional) Select a specific image toosee tags</span></span>

![Репозитории в портале hello](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a><span data-ttu-id="73cf4-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="73cf4-127">Next steps</span></span>
<span data-ttu-id="73cf4-128">Теперь, вы знаете основы hello, все готово toostart, с помощью реестра!</span><span class="sxs-lookup"><span data-stu-id="73cf4-128">Now that you know hello basics, you are ready toostart using your registry!</span></span> <span data-ttu-id="73cf4-129">Например, начать развертывание контейнера изображений tooan [контейнера службы Azure](https://azure.microsoft.com/documentation/services/container-service/) кластера.</span><span class="sxs-lookup"><span data-stu-id="73cf4-129">For example, start deploying container images tooan [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
