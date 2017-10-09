---
title: "aaaIntroduction tooAzure контейнер службы для Kubernetes | Документы Microsoft"
description: "Служба Azure контейнер для Kubernetes делает простой toodeploy и управлять приложениями на основе контейнера в Azure."
services: container-service
documentationcenter: 
author: gabrtv
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kubernetes, Docker, контейнеры, микрослужбы, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: bfc85a180bdf4a405c9047eb882d3eed01640dd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-container-service-for-kubernetes"></a><span data-ttu-id="d4d85-104">Введение tooAzure контейнер службы для Kubernetes</span><span class="sxs-lookup"><span data-stu-id="d4d85-104">Introduction tooAzure Container Service for Kubernetes</span></span>
<span data-ttu-id="d4d85-105">Служба Azure контейнер для Kubernetes делает простой toocreate, настройки и управления кластера виртуальных машин, которые являются предварительно настроенных toorun контейнерных приложений.</span><span class="sxs-lookup"><span data-stu-id="d4d85-105">Azure Container Service for Kubernetes makes it simple toocreate, configure, and manage a cluster of virtual machines that are preconfigured toorun containerized applications.</span></span> <span data-ttu-id="d4d85-106">Это позволяет вам toouse существующие навыки работы или рисования при растущих части опытом сообщества, toodeploy и управлять приложениями на основе контейнера на Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d4d85-106">This enables you toouse your existing skills, or draw upon a large and growing body of community expertise, toodeploy and manage container-based applications on Microsoft Azure.</span></span>

<span data-ttu-id="d4d85-107">С помощью контейнера службы Azure, можно воспользоваться преимуществами hello функций корпоративного уровня, Azure, одновременно сохраняя переносимость приложения через Kubernetes и hello Docker формат изображения.</span><span class="sxs-lookup"><span data-stu-id="d4d85-107">By using Azure Container Service, you can take advantage of hello enterprise-grade features of Azure, while still maintaining application portability through Kubernetes and hello Docker image format.</span></span>

## <a name="using-azure-container-service-for-kubernetes"></a><span data-ttu-id="d4d85-108">Использование службы контейнеров Azure для Kubernetes</span><span class="sxs-lookup"><span data-stu-id="d4d85-108">Using Azure Container Service for Kubernetes</span></span>
<span data-ttu-id="d4d85-109">Наша цель, с помощью контейнера службы Azure — tooprovide среды размещения контейнера с помощью средств с открытым исходным кодом и технологии, которые часто используются для наших заказчиков сегодня.</span><span class="sxs-lookup"><span data-stu-id="d4d85-109">Our goal with Azure Container Service is tooprovide a container hosting environment by using open-source tools and technologies that are popular among our customers today.</span></span> <span data-ttu-id="d4d85-110">конец toothis мы предоставляем hello стандартные конечные точки Kubernetes API.</span><span class="sxs-lookup"><span data-stu-id="d4d85-110">toothis end, we expose hello standard Kubernetes API endpoints.</span></span> <span data-ttu-id="d4d85-111">Используя эти стандартные конечные точки, может использовать программное обеспечение, которое поддерживает обмен данными tooa Kubernetes кластера.</span><span class="sxs-lookup"><span data-stu-id="d4d85-111">By using these standard endpoints, you can leverage any software that is capable of talking tooa Kubernetes cluster.</span></span> <span data-ttu-id="d4d85-112">Например, можно выбрать [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [Helm](https://helm.sh/) или [Draft](https://github.com/Azure/draft).</span><span class="sxs-lookup"><span data-stu-id="d4d85-112">For example, you might choose [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/), or [draft](https://github.com/Azure/draft).</span></span>

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a><span data-ttu-id="d4d85-113">Создание кластера Kubernetes с помощью службы контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="d4d85-113">Creating a Kubernetes cluster using Azure Container Service</span></span>
<span data-ttu-id="d4d85-114">toobegin с помощью контейнера службы Azure, развернуть кластер контейнера службы Azure с hello [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) или через портал hello (hello поиска Marketplace для **контейнера службы Azure**).</span><span class="sxs-lookup"><span data-stu-id="d4d85-114">toobegin using Azure Container Service, deploy an Azure Container Service cluster with hello [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) or via hello portal (search hello Marketplace for **Azure Container Service**).</span></span> <span data-ttu-id="d4d85-115">Опытных пользователей, которым необходим больший контроль над hello шаблоны диспетчера ресурсов Azure можно использовать Привет открыть источник [acs ядра](https://github.com/Azure/acs-engine) toobuild проект собственных пользовательских Kubernetes кластера и его развертывания через hello `az` CLI.</span><span class="sxs-lookup"><span data-stu-id="d4d85-115">If you are an advanced user who needs more control over hello Azure Resource Manager templates, you can use hello open source [acs-engine](https://github.com/Azure/acs-engine) project toobuild your own custom Kubernetes cluster and deploy it via hello `az` CLI.</span></span>

### <a name="using-kubernetes"></a><span data-ttu-id="d4d85-116">Использование Kubernetes</span><span class="sxs-lookup"><span data-stu-id="d4d85-116">Using Kubernetes</span></span>
<span data-ttu-id="d4d85-117">Kubernetes автоматизирует развертывание, масштабирование приложений-контейнеров и управление ими.</span><span class="sxs-lookup"><span data-stu-id="d4d85-117">Kubernetes automates deployment, scaling, and management of containerized applications.</span></span> <span data-ttu-id="d4d85-118">Это решение предоставляет обширный набор возможностей, в том числе:</span><span class="sxs-lookup"><span data-stu-id="d4d85-118">It has a rich set of features including:</span></span>
* <span data-ttu-id="d4d85-119">автоматическая упаковка в контейнеры;</span><span class="sxs-lookup"><span data-stu-id="d4d85-119">Automatic binpacking</span></span>
* <span data-ttu-id="d4d85-120">самовосстановление;</span><span class="sxs-lookup"><span data-stu-id="d4d85-120">Self-healing</span></span>
* <span data-ttu-id="d4d85-121">горизонтальное масштабирование;</span><span class="sxs-lookup"><span data-stu-id="d4d85-121">Horizontal scaling</span></span>
* <span data-ttu-id="d4d85-122">обнаружение служб и балансировка нагрузки;</span><span class="sxs-lookup"><span data-stu-id="d4d85-122">Service discovery and load balancing</span></span>
* <span data-ttu-id="d4d85-123">автоматические обновления и откаты;</span><span class="sxs-lookup"><span data-stu-id="d4d85-123">Automated rollouts and rollbacks</span></span>
* <span data-ttu-id="d4d85-124">управление секретами и конфигурациями;</span><span class="sxs-lookup"><span data-stu-id="d4d85-124">Secret and configuration management</span></span>
* <span data-ttu-id="d4d85-125">оркестрация хранилища;</span><span class="sxs-lookup"><span data-stu-id="d4d85-125">Storage orchestration</span></span>
* <span data-ttu-id="d4d85-126">пакетное выполнение.</span><span class="sxs-lookup"><span data-stu-id="d4d85-126">Batch execution</span></span>

<span data-ttu-id="d4d85-127">Архитектура службы Kubernetes, развернутой с помощью службы контейнеров Azure:</span><span class="sxs-lookup"><span data-stu-id="d4d85-127">Architectural diagram of Kubernetes deployed via Azure Container Service:</span></span>

![Служба Azure контейнера настроен toouse Kubernetes.](media/acs-intro/kubernetes.png)

## <a name="videos"></a><span data-ttu-id="d4d85-129">Видеоролики</span><span class="sxs-lookup"><span data-stu-id="d4d85-129">Videos</span></span>

<span data-ttu-id="d4d85-130">Поддержка Kubernetes в службе контейнеров ("Пятница с Azure", январь 2017 г.):</span><span class="sxs-lookup"><span data-stu-id="d4d85-130">Kubernetes Support in Azure Container Services (Azure Friday, January 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

<span data-ttu-id="d4d85-131">Средства разработки и развертывания приложений в Kubernetes (Azure OpenDev, июнь 2017 г.):</span><span class="sxs-lookup"><span data-stu-id="d4d85-131">Tools for Developing and Deploying Applications on Kubernetes (Azure OpenDev, June 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a><span data-ttu-id="d4d85-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d4d85-132">Next steps</span></span>

<span data-ttu-id="d4d85-133">Просмотр hello [краткое руководство Kubernetes](container-service-kubernetes-walkthrough.md) toobegin сегодня изучение контейнера службы Azure.</span><span class="sxs-lookup"><span data-stu-id="d4d85-133">Explore hello [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) toobegin exploring Azure Container Service today.</span></span>
