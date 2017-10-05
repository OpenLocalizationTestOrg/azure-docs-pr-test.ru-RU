---
title: "Репозитории реестра контейнеров Azure | Документация Майкрософт"
description: "Использование репозиториев реестра контейнеров Azure для образов Docker"
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
ms.openlocfilehash: 06b809c31cecef1714f60d04657eb74c611be8cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="2ab8d-103">Репозитории реестра контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="2ab8d-103">Azure container registry repositories</span></span>

<span data-ttu-id="2ab8d-104">Реестр контейнеров Azure позволяет хранить образы контейнеров в репозиториях.</span><span class="sxs-lookup"><span data-stu-id="2ab8d-104">Azure container registry allows you to store container images in repositories.</span></span> <span data-ttu-id="2ab8d-105">Это позволяет содержать группы образов (версии образов) в изолированных средах.</span><span class="sxs-lookup"><span data-stu-id="2ab8d-105">By storing images in repositories, you can have groups of images (or version of images) in isolated environments.</span></span> <span data-ttu-id="2ab8d-106">Эти репозитории можно указать при отправке образов в реестр.</span><span class="sxs-lookup"><span data-stu-id="2ab8d-106">You can specify these repositories when you push images to your registry.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="2ab8d-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2ab8d-107">Prerequisites</span></span>
* <span data-ttu-id="2ab8d-108">**Реестр контейнеров Azure.** Создайте реестр контейнеров в своей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="2ab8d-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="2ab8d-109">Это можно сделать на [портале Azure](container-registry-get-started-portal.md) или с помощью [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2ab8d-109">For example, use the [Azure portal](container-registry-get-started-portal.md) or the [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="2ab8d-110">**Интерфейс командной строки Docker.** Установите [подсистему Docker](https://docs.docker.com/engine/installation/), чтобы настроить локальный компьютер в качестве узла Docker и получить доступ к командам интерфейса командной строки Docker.</span><span class="sxs-lookup"><span data-stu-id="2ab8d-110">**Docker CLI** - To set up your local computer as a Docker host and access the Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>
* <span data-ttu-id="2ab8d-111">**Извлечение образа.** Извлеките образ из общедоступного реестра в концентраторе Docker, пометьте его и отправьте в свой реестр.</span><span class="sxs-lookup"><span data-stu-id="2ab8d-111">**Pull an image** - Pull an image from the public Docker Hub registry, tag it, and push it to your registry.</span></span> <span data-ttu-id="2ab8d-112">Сведения об отправке и извлечении изображений см. в разделе [Отправка первого образа в частный реестр контейнеров Docker с помощью интерфейса командной строки Docker](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2ab8d-112">For guidance on how push and pull images, see [Push Docker image to Azure private registry](container-registry-get-started-docker-cli.md).</span></span>


## <a name="viewing-repositories-in-the-portal"></a><span data-ttu-id="2ab8d-113">Просмотр репозиториев на портале</span><span class="sxs-lookup"><span data-stu-id="2ab8d-113">Viewing repositories in the Portal</span></span>

<span data-ttu-id="2ab8d-114">После отправки образов в реестр контейнеров можно просмотреть список репозиториев, в которых размещаются образы, на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="2ab8d-114">Once you have pushed images to your container registry, you can see a list of the repositories hosting the images in the Azure portal.</span></span>

<span data-ttu-id="2ab8d-115">Если вы следовали инструкциям из статьи [Отправка первого образа в частный реестр контейнеров Docker с помощью интерфейса командной строки Docker](container-registry-get-started-docker-cli.md), в вашем реестре контейнеров должен содержаться образ Nginx.</span><span class="sxs-lookup"><span data-stu-id="2ab8d-115">If you followed the steps in the [Push Docker image to Azure private registry](container-registry-get-started-docker-cli.md) article, you should now have a Nginx image in your container registry.</span></span> <span data-ttu-id="2ab8d-116">В ходе выполнения инструкций вы должны были указать пространство имен для образа.</span><span class="sxs-lookup"><span data-stu-id="2ab8d-116">As part of the instructions, you should have specified a namespace for the image.</span></span> <span data-ttu-id="2ab8d-117">В следующем примере команда отправляет образ NGinx в репозиторий samples:</span><span class="sxs-lookup"><span data-stu-id="2ab8d-117">In the example below, the command pushes the NGinx image to the "samples" repository:</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```
 <span data-ttu-id="2ab8d-118">Реестр контейнеров Azure поддерживает многоуровневые пространства имен для репозитория.</span><span class="sxs-lookup"><span data-stu-id="2ab8d-118">Azure Container Registry supports multilevel repository namespaces.</span></span> <span data-ttu-id="2ab8d-119">Благодаря этому можно группировать коллекции образов, связанные с определенным приложением, или коллекции приложений, связанные с определенным развертыванием или рабочими группами.</span><span class="sxs-lookup"><span data-stu-id="2ab8d-119">This feature enables you to group collections of images related to a specific app, or a collection of apps to specific development or operational teams.</span></span> <span data-ttu-id="2ab8d-120">Дополнительные сведения о репозиториях в реестрах контейнеров см. в статье [Общие сведения о частных реестрах контейнеров Docker](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="2ab8d-120">To read more about repositories in container registries, see [Private Docker container registries in Azure](container-registry-intro.md).</span></span>

<span data-ttu-id="2ab8d-121">Чтобы просмотреть репозитории реестра контейнеров, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="2ab8d-121">To view the container registry repositories:</span></span>

1. <span data-ttu-id="2ab8d-122">Войдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2ab8d-122">Log in to the Azure portal</span></span>
2. <span data-ttu-id="2ab8d-123">В колонке **Реестр контейнеров Azure** выберите реестр, который вы хотите проверить.</span><span class="sxs-lookup"><span data-stu-id="2ab8d-123">On the **Azure Container Registry** blade, select the registry you wish to inspect</span></span>
3. <span data-ttu-id="2ab8d-124">В колонке реестра щелкните **Репозитории**, чтобы просмотреть список всех репозиториев и соответствующих образов.</span><span class="sxs-lookup"><span data-stu-id="2ab8d-124">In the registry blade, click **Repositories** to see a list of all the repositories and their images</span></span>
4. <span data-ttu-id="2ab8d-125">(Необязательно.) Выберите определенный образ, чтобы просмотреть теги.</span><span class="sxs-lookup"><span data-stu-id="2ab8d-125">(Optional) Select a specific image to see tags</span></span>

![Репозитории на портале](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a><span data-ttu-id="2ab8d-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2ab8d-127">Next steps</span></span>
<span data-ttu-id="2ab8d-128">Теперь, когда вы знаете основы, можно приступать к использованию реестра.</span><span class="sxs-lookup"><span data-stu-id="2ab8d-128">Now that you know the basics, you are ready to start using your registry!</span></span> <span data-ttu-id="2ab8d-129">Например, разверните образы контейнера в кластер [службы контейнеров Azure](https://azure.microsoft.com/documentation/services/container-service/).</span><span class="sxs-lookup"><span data-stu-id="2ab8d-129">For example, start deploying container images to an [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
