---
title: "веб-перехватчиков реестра контейнера aaaAzure | Документы Microsoft"
description: "Веб-перехватчики реестра контейнеров Azure."
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acr, azure-container-registry
keywords: "Docker, контейнеры, ACR"
ms.assetid: 
ms.service: container-registry
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/06/2017
ms.author: nepeters
ms.openlocfilehash: adc2afec486007e2d54cd689e6f7ef8b1098db06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a><span data-ttu-id="4aecf-104">Использование веб-перехватчиков реестра контейнеров Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="4aecf-104">Using Azure Container Registry webhooks - Azure portal</span></span>

<span data-ttu-id="4aecf-105">В реестре контейнер Azure хранит данные и управляет частных образов контейнеров Docker, так же как toohello Docker Hub содержит общедоступные образы Docker.</span><span class="sxs-lookup"><span data-stu-id="4aecf-105">An Azure container registry stores and manages private Docker container images, similar toohello way Docker Hub stores public Docker images.</span></span> <span data-ttu-id="4aecf-106">Веб-перехватчиков tootrigger события, когда выполнение определенных действий в одном репозитории вашей реестра использовать.</span><span class="sxs-lookup"><span data-stu-id="4aecf-106">You use webhooks tootrigger events when certain actions take place in one of your registry repositories.</span></span> <span data-ttu-id="4aecf-107">Веб-перехватчиков учитывали tooevents на уровне реестра hello или они могут задаваться на работу tooa определенный репозиторий тег.</span><span class="sxs-lookup"><span data-stu-id="4aecf-107">Webhooks can respond tooevents at hello registry level or they can be scoped down tooa specific repository tag.</span></span> 

<span data-ttu-id="4aecf-108">Дополнительные сведения и основные понятия в разделе hello [Обзор](./container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="4aecf-108">For more background and concepts, see hello [overview](./container-registry-intro.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4aecf-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4aecf-109">Prerequisites</span></span> 

- <span data-ttu-id="4aecf-110">Управляемый реестр контейнеров Azure. Создайте управляемый реестр контейнеров в своей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="4aecf-110">Azure container managed registry - Create a managed container registry in your Azure subscription.</span></span> <span data-ttu-id="4aecf-111">Например использовать портал Azure hello или hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="4aecf-111">For example, use hello Azure portal or hello Azure CLI 2.0.</span></span> 
- <span data-ttu-id="4aecf-112">Docker CLI - tooset ваш локальный компьютер как узла и доступа к hello Docker CLI команды Docker, установите подсистему Docker.</span><span class="sxs-lookup"><span data-stu-id="4aecf-112">Docker CLI - tooset up your local computer as a Docker host and access hello Docker CLI commands, install Docker Engine.</span></span> 

## <a name="create-webhook-azure-portal"></a><span data-ttu-id="4aecf-113">Создание веб-перехватчика на портале Azure</span><span class="sxs-lookup"><span data-stu-id="4aecf-113">Create webhook Azure portal</span></span>

1. <span data-ttu-id="4aecf-114">Войдите в портал Azure toohello и перейдите реестра toohello, которой требуется toocreate веб-привязок.</span><span class="sxs-lookup"><span data-stu-id="4aecf-114">Log in toohello Azure portal and navigate toohello registry in which you want toocreate webhooks.</span></span> 

2. <span data-ttu-id="4aecf-115">В колонке контейнера hello перейдите на вкладку «Веб-перехватчиков» hello.</span><span class="sxs-lookup"><span data-stu-id="4aecf-115">In hello container blade, select hello "Webhooks" tab.</span></span> 

3. <span data-ttu-id="4aecf-116">Нажмите «Добавить» в колонке веб-перехватчика hello.</span><span class="sxs-lookup"><span data-stu-id="4aecf-116">Select "Add" from hello webhook blade toolbar.</span></span> 

4. <span data-ttu-id="4aecf-117">Полный hello *создать веб-перехватчика* формы с hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="4aecf-117">Complete hello *Create Webhook* form with hello following information:</span></span>

| <span data-ttu-id="4aecf-118">Значение</span><span class="sxs-lookup"><span data-stu-id="4aecf-118">Value</span></span> | <span data-ttu-id="4aecf-119">Описание</span><span class="sxs-lookup"><span data-stu-id="4aecf-119">Description</span></span> |
|---|---|
| <span data-ttu-id="4aecf-120">Имя</span><span class="sxs-lookup"><span data-stu-id="4aecf-120">Name</span></span> | <span data-ttu-id="4aecf-121">Hello имя, которое будет toogive toohello веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="4aecf-121">hello name you want toogive toohello webhook.</span></span> <span data-ttu-id="4aecf-122">Оно может содержать только 5–50 строчных букв и цифр.</span><span class="sxs-lookup"><span data-stu-id="4aecf-122">It can only contain lowercase letters and numbers and between 5-50 characters.</span></span> |
| <span data-ttu-id="4aecf-123">URI службы</span><span class="sxs-lookup"><span data-stu-id="4aecf-123">Service URI</span></span> | <span data-ttu-id="4aecf-124">Здравствуйте, где веб-перехватчика hello следует отправлять уведомления POST URI.</span><span class="sxs-lookup"><span data-stu-id="4aecf-124">hello URI where hello webhook should send POST notifications.</span></span> |
| <span data-ttu-id="4aecf-125">Настраиваемые заголовки</span><span class="sxs-lookup"><span data-stu-id="4aecf-125">Custom headers</span></span> | <span data-ttu-id="4aecf-126">Заголовки, которые требуется toopass вместе с запросом POST hello.</span><span class="sxs-lookup"><span data-stu-id="4aecf-126">Headers you want toopass along with hello POST request.</span></span> <span data-ttu-id="4aecf-127">Они должны быть в формате "ключ: значение".</span><span class="sxs-lookup"><span data-stu-id="4aecf-127">They should be in "key: value" format.</span></span> |
| <span data-ttu-id="4aecf-128">"Trigger actions" (Активирующие действия)</span><span class="sxs-lookup"><span data-stu-id="4aecf-128">Trigger actions</span></span> | <span data-ttu-id="4aecf-129">Действия, которые вызывают веб-перехватчика hello.</span><span class="sxs-lookup"><span data-stu-id="4aecf-129">Actions that trigger hello webhook.</span></span> <span data-ttu-id="4aecf-130">В настоящее время веб-привязок может быть вызвано push и/или удалить изображение tooan действия.</span><span class="sxs-lookup"><span data-stu-id="4aecf-130">Currently webhooks can be triggered by push and/or delete actions tooan image.</span></span> |
| <span data-ttu-id="4aecf-131">Состояние</span><span class="sxs-lookup"><span data-stu-id="4aecf-131">Status</span></span> | <span data-ttu-id="4aecf-132">состояние Hello веб-перехватчика hello после его создания.</span><span class="sxs-lookup"><span data-stu-id="4aecf-132">hello status for hello webhook after it's created.</span></span> <span data-ttu-id="4aecf-133">По умолчанию он включен.</span><span class="sxs-lookup"><span data-stu-id="4aecf-133">It's enabled by default.</span></span> |
| <span data-ttu-id="4aecf-134">Область</span><span class="sxs-lookup"><span data-stu-id="4aecf-134">Scope</span></span> | <span data-ttu-id="4aecf-135">область Hello, на котором работает веб-перехватчика hello.</span><span class="sxs-lookup"><span data-stu-id="4aecf-135">hello scope at which hello webhook works.</span></span> <span data-ttu-id="4aecf-136">По умолчанию hello область — для всех событий в реестре hello.</span><span class="sxs-lookup"><span data-stu-id="4aecf-136">By default hello scope is for all events in hello registry.</span></span> <span data-ttu-id="4aecf-137">Указанный для репозитория или из тега, используя формат hello» репозитория: тег».</span><span class="sxs-lookup"><span data-stu-id="4aecf-137">It can be specified for a repository or a tag by using hello format "repository: tag".</span></span> |

<span data-ttu-id="4aecf-138">Пример формы для веб-перехватчика приведен ниже.</span><span class="sxs-lookup"><span data-stu-id="4aecf-138">Example webhook form:</span></span>

![Пользовательский интерфейс DCOS](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a><span data-ttu-id="4aecf-140">Создание веб-перехватчика с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4aecf-140">Create webhook Azure CLI</span></span>

<span data-ttu-id="4aecf-141">Здравствуйте, toocreate веб-перехватчик с помощью Azure CLI, используйте hello [создать веб-перехватчика acr az](/cli/azure/acr/webhook#create) команды.</span><span class="sxs-lookup"><span data-stu-id="4aecf-141">toocreate a webhook using hello Azure CLI, use hello [az acr webhook create](/cli/azure/acr/webhook#create) command.</span></span>

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a><span data-ttu-id="4aecf-142">Проверка веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="4aecf-142">Test webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="4aecf-143">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="4aecf-143">Azure portal</span></span>

<span data-ttu-id="4aecf-144">Веб-перехватчика hello предыдущих toousing контейнере образ push и удалить действия, его можно проверить при помощи hello **Ping** кнопки.</span><span class="sxs-lookup"><span data-stu-id="4aecf-144">Prior toousing hello webhook on container image push and delete actions, it can be tested using hello **Ping** button.</span></span> <span data-ttu-id="4aecf-145">При использовании hello Ping отправляет запрос post в универсальный toohello указало конечной точки и журналы hello ответа.</span><span class="sxs-lookup"><span data-stu-id="4aecf-145">When used, hello Ping sends a generic post request toohello specified endpoint and logs hello response.</span></span> <span data-ttu-id="4aecf-146">Это может оказаться полезным, hello веб-перехватчика tooverify настроен правильно.</span><span class="sxs-lookup"><span data-stu-id="4aecf-146">This is helpful tooverify that hello webhook has been set up correctly.</span></span>

1. <span data-ttu-id="4aecf-147">Выберите веб-перехватчика hello требуется tootest.</span><span class="sxs-lookup"><span data-stu-id="4aecf-147">Select hello webhook you want tootest.</span></span> 
2. <span data-ttu-id="4aecf-148">В верхней части панели инструментов hello выберите действие «Проверить связь с» hello.</span><span class="sxs-lookup"><span data-stu-id="4aecf-148">In hello top toolbar, select hello "Ping" action.</span></span> 
3. <span data-ttu-id="4aecf-149">Проверьте hello запроса и ответа.</span><span class="sxs-lookup"><span data-stu-id="4aecf-149">Check hello request and response.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="4aecf-150">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="4aecf-150">Azure CLI</span></span>

<span data-ttu-id="4aecf-151">tootest перехватчик контроля доступа с hello Azure CLI, используйте hello [ping веб-перехватчика acr az](/cli/azure/acr/webhook#ping) команды.</span><span class="sxs-lookup"><span data-stu-id="4aecf-151">tootest an ACR webhook with hello Azure CLI, use hello [az acr webhook ping](/cli/azure/acr/webhook#ping) command.</span></span>

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

<span data-ttu-id="4aecf-152">toosee hello результаты, использование hello [события az acr веб-перехватчика списка](/cli/azure/acr/webhook#list-events) команды.</span><span class="sxs-lookup"><span data-stu-id="4aecf-152">toosee hello results, use hello [az acr webhook list-events](/cli/azure/acr/webhook#list-events) command.</span></span> 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a><span data-ttu-id="4aecf-153">Удаление веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="4aecf-153">Delete webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="4aecf-154">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="4aecf-154">Azure portal</span></span>

<span data-ttu-id="4aecf-155">Каждый веб-перехватчика могут быть удалены с веб-перехватчика hello, а затем кнопку удаления hello на hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4aecf-155">Each webhook can be deleted by selecting hello webhook and then hello delete button on hello Azure portal.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="4aecf-156">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="4aecf-156">Azure CLI</span></span>

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```