---
title: "Знакомство со службой контейнеров Azure для Kubernetes | Документация Майкрософт"
description: "Служба контейнеров Azure для Kubernetes упрощает развертывание и администрирование контейнерных приложений в Azure."
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
ms.openlocfilehash: 92cdbe20e7a2974a734dfed5294c547866050290
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="introduction-to-azure-container-service-for-kubernetes"></a><span data-ttu-id="d16ae-104">Знакомство со службой контейнеров Azure для Kubernetes</span><span class="sxs-lookup"><span data-stu-id="d16ae-104">Introduction to Azure Container Service for Kubernetes</span></span>
<span data-ttu-id="d16ae-105">Служба контейнеров Azure для Kubernetes упрощает создание, настройку и администрирование кластера виртуальных машин, настроенных для запуска контейнерных приложений.</span><span class="sxs-lookup"><span data-stu-id="d16ae-105">Azure Container Service for Kubernetes makes it simple to create, configure, and manage a cluster of virtual machines that are preconfigured to run containerized applications.</span></span> <span data-ttu-id="d16ae-106">Это позволяет использовать имеющиеся навыки либо положиться на опыт обширного и постоянно увеличивающегося сообщества при развертывании приложений на основе контейнера в Microsoft Azure и управлении ими.</span><span class="sxs-lookup"><span data-stu-id="d16ae-106">This enables you to use your existing skills, or draw upon a large and growing body of community expertise, to deploy and manage container-based applications on Microsoft Azure.</span></span>

<span data-ttu-id="d16ae-107">Служба контейнеров Azure позволяет пользоваться преимуществами функций корпоративного уровня в Azure, сохраняя при этом возможность переноса приложений в Kubernetes и поддержку формата образов Docker.</span><span class="sxs-lookup"><span data-stu-id="d16ae-107">By using Azure Container Service, you can take advantage of the enterprise-grade features of Azure, while still maintaining application portability through Kubernetes and the Docker image format.</span></span>

## <a name="using-azure-container-service-for-kubernetes"></a><span data-ttu-id="d16ae-108">Использование службы контейнеров Azure для Kubernetes</span><span class="sxs-lookup"><span data-stu-id="d16ae-108">Using Azure Container Service for Kubernetes</span></span>
<span data-ttu-id="d16ae-109">Цель, которой мы стремимся достичь с помощью службы контейнеров Azure, заключается в том, чтобы предоставить среду для размещения контейнеров, применяя средства и технологии с открытым исходным кодом, которые сейчас пользуются популярностью среди наших клиентов.</span><span class="sxs-lookup"><span data-stu-id="d16ae-109">Our goal with Azure Container Service is to provide a container hosting environment by using open-source tools and technologies that are popular among our customers today.</span></span> <span data-ttu-id="d16ae-110">Для этого мы предоставляем стандартные конечные точки API Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="d16ae-110">To this end, we expose the standard Kubernetes API endpoints.</span></span> <span data-ttu-id="d16ae-111">С помощью этих стандартных конечных точек можно использовать любое программное обеспечение, способное взаимодействовать с кластером Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="d16ae-111">By using these standard endpoints, you can leverage any software that is capable of talking to a Kubernetes cluster.</span></span> <span data-ttu-id="d16ae-112">Например, можно выбрать [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [Helm](https://helm.sh/) или [Draft](https://github.com/Azure/draft).</span><span class="sxs-lookup"><span data-stu-id="d16ae-112">For example, you might choose [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/), or [draft](https://github.com/Azure/draft).</span></span>

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a><span data-ttu-id="d16ae-113">Создание кластера Kubernetes с помощью службы контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="d16ae-113">Creating a Kubernetes cluster using Azure Container Service</span></span>
<span data-ttu-id="d16ae-114">Чтобы приступить к работе со службой контейнеров Azure, разверните кластер службы контейнеров Azure с помощью [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) или портала (выполните в Marketplace поиск по словам **служба контейнеров Azure**).</span><span class="sxs-lookup"><span data-stu-id="d16ae-114">To begin using Azure Container Service, deploy an Azure Container Service cluster with the [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) or via the portal (search the Marketplace for **Azure Container Service**).</span></span> <span data-ttu-id="d16ae-115">Если вы — опытный пользователь, которому требуется дополнительный контроль над шаблонами Azure Resource Manager, вы можете создать пользовательский кластер Kubernetes и развернуть его с помощью интерфейса командной строки `az`, используя проект с открытым кодом [acs-engine](https://github.com/Azure/acs-engine).</span><span class="sxs-lookup"><span data-stu-id="d16ae-115">If you are an advanced user who needs more control over the Azure Resource Manager templates, you can use the open source [acs-engine](https://github.com/Azure/acs-engine) project to build your own custom Kubernetes cluster and deploy it via the `az` CLI.</span></span>

### <a name="using-kubernetes"></a><span data-ttu-id="d16ae-116">Использование Kubernetes</span><span class="sxs-lookup"><span data-stu-id="d16ae-116">Using Kubernetes</span></span>
<span data-ttu-id="d16ae-117">Kubernetes автоматизирует развертывание, масштабирование приложений-контейнеров и управление ими.</span><span class="sxs-lookup"><span data-stu-id="d16ae-117">Kubernetes automates deployment, scaling, and management of containerized applications.</span></span> <span data-ttu-id="d16ae-118">Это решение предоставляет обширный набор возможностей, в том числе:</span><span class="sxs-lookup"><span data-stu-id="d16ae-118">It has a rich set of features including:</span></span>
* <span data-ttu-id="d16ae-119">автоматическая упаковка в контейнеры;</span><span class="sxs-lookup"><span data-stu-id="d16ae-119">Automatic binpacking</span></span>
* <span data-ttu-id="d16ae-120">самовосстановление;</span><span class="sxs-lookup"><span data-stu-id="d16ae-120">Self-healing</span></span>
* <span data-ttu-id="d16ae-121">горизонтальное масштабирование;</span><span class="sxs-lookup"><span data-stu-id="d16ae-121">Horizontal scaling</span></span>
* <span data-ttu-id="d16ae-122">обнаружение служб и балансировка нагрузки;</span><span class="sxs-lookup"><span data-stu-id="d16ae-122">Service discovery and load balancing</span></span>
* <span data-ttu-id="d16ae-123">автоматические обновления и откаты;</span><span class="sxs-lookup"><span data-stu-id="d16ae-123">Automated rollouts and rollbacks</span></span>
* <span data-ttu-id="d16ae-124">управление секретами и конфигурациями;</span><span class="sxs-lookup"><span data-stu-id="d16ae-124">Secret and configuration management</span></span>
* <span data-ttu-id="d16ae-125">оркестрация хранилища;</span><span class="sxs-lookup"><span data-stu-id="d16ae-125">Storage orchestration</span></span>
* <span data-ttu-id="d16ae-126">пакетное выполнение.</span><span class="sxs-lookup"><span data-stu-id="d16ae-126">Batch execution</span></span>

<span data-ttu-id="d16ae-127">Архитектура службы Kubernetes, развернутой с помощью службы контейнеров Azure:</span><span class="sxs-lookup"><span data-stu-id="d16ae-127">Architectural diagram of Kubernetes deployed via Azure Container Service:</span></span>

![Служба контейнеров Azure, настроенная для использования Kubernetes.](media/acs-intro/kubernetes.png)

## <a name="videos"></a><span data-ttu-id="d16ae-129">Видеоролики</span><span class="sxs-lookup"><span data-stu-id="d16ae-129">Videos</span></span>

<span data-ttu-id="d16ae-130">Поддержка Kubernetes в службе контейнеров ("Пятница с Azure", январь 2017 г.):</span><span class="sxs-lookup"><span data-stu-id="d16ae-130">Kubernetes Support in Azure Container Services (Azure Friday, January 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

<span data-ttu-id="d16ae-131">Средства разработки и развертывания приложений в Kubernetes (Azure OpenDev, июнь 2017 г.):</span><span class="sxs-lookup"><span data-stu-id="d16ae-131">Tools for Developing and Deploying Applications on Kubernetes (Azure OpenDev, June 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a><span data-ttu-id="d16ae-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d16ae-132">Next steps</span></span>

<span data-ttu-id="d16ae-133">Изучите [краткое руководство по Kubernetes](container-service-kubernetes-walkthrough.md), чтобы приступить к работе со службой контейнеров Azure прямо сейчас.</span><span class="sxs-lookup"><span data-stu-id="d16ae-133">Explore the [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) to begin exploring Azure Container Service today.</span></span>