---
title: "aaaAuthenticate с реестром контейнер Azure | Документы Microsoft"
description: "Как toolog в реестре tooan контейнер Azure, Azure Active Directory с помощью службы учетную запись администратора или участника"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 128a937a-766a-415b-b9fc-35a6c2f27417
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a0b0462e8432b2567689debca322e2426baa7fa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a><span data-ttu-id="20e43-103">Аутентификация с помощью частного реестра контейнеров Docker</span><span class="sxs-lookup"><span data-stu-id="20e43-103">Authenticate with a private Docker container registry</span></span>
<span data-ttu-id="20e43-104">toowork с образы контейнеров в контейнер Azure реестра вы вошли с использованием hello `docker login` команды.</span><span class="sxs-lookup"><span data-stu-id="20e43-104">toowork with container images in an Azure container registry, you log in using hello `docker login` command.</span></span> <span data-ttu-id="20e43-105">Вы можете войти, используя **[субъект-службу Azure Active Directory](../active-directory/active-directory-application-objects.md)** или специальную **учетную запись администратора**.</span><span class="sxs-lookup"><span data-stu-id="20e43-105">You can log in using either an **[Azure Active Directory service principal](../active-directory/active-directory-application-objects.md)** or a registry-specific **admin account**.</span></span> <span data-ttu-id="20e43-106">В этой статье содержатся подробные сведения об этих удостоверениях.</span><span class="sxs-lookup"><span data-stu-id="20e43-106">This article provides more detail about these identities.</span></span>



## <a name="service-principal"></a><span data-ttu-id="20e43-107">Субъект-служба</span><span class="sxs-lookup"><span data-stu-id="20e43-107">Service principal</span></span>

<span data-ttu-id="20e43-108">Вы можете [назначить участника службы](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour реестра и использовать его для обычной проверки подлинности Docker.</span><span class="sxs-lookup"><span data-stu-id="20e43-108">You can [assign a service principal](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour registry and use it for basic Docker authentication.</span></span> <span data-ttu-id="20e43-109">Мы рекомендуем использовать субъект-службу в большинстве сценариев.</span><span class="sxs-lookup"><span data-stu-id="20e43-109">Using a service principal is recommended for most scenarios.</span></span> <span data-ttu-id="20e43-110">Укажите идентификатор приложения hello и пароль toohello основной службы hello `docker login` команды, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="20e43-110">Provide hello app ID and password of hello service principal toohello `docker login` command, as shown in hello following example:</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="20e43-111">После входа Docker кэширует hello учетные данные, вам требуется идентификатор tooremember hello приложений.</span><span class="sxs-lookup"><span data-stu-id="20e43-111">Once logged in, Docker caches hello credentials, so you don't need tooremember hello app ID.</span></span>

> [!TIP]
> <span data-ttu-id="20e43-112">Если требуется, можно создать повторно hello пароль субъекта-службы, выполнив hello `az ad sp reset-credentials` команды.</span><span class="sxs-lookup"><span data-stu-id="20e43-112">If you want, you can regenerate hello password of a service principal by running hello `az ad sp reset-credentials` command.</span></span>
>


<span data-ttu-id="20e43-113">Разрешить участников службы [доступа на основе ролей](../active-directory/role-based-access-control-configure.md) tooa реестра.</span><span class="sxs-lookup"><span data-stu-id="20e43-113">Service principals allow [role-based access](../active-directory/role-based-access-control-configure.md) tooa registry.</span></span> <span data-ttu-id="20e43-114">Доступные роли:</span><span class="sxs-lookup"><span data-stu-id="20e43-114">Available roles are:</span></span>
  * <span data-ttu-id="20e43-115">Читатель (доступ только для получения).</span><span class="sxs-lookup"><span data-stu-id="20e43-115">Reader (pull only access).</span></span>
  * <span data-ttu-id="20e43-116">Участник (получение и отправка).</span><span class="sxs-lookup"><span data-stu-id="20e43-116">Contributor (pull and push).</span></span>
  * <span data-ttu-id="20e43-117">Владелец (запросу, отправку и назначить роли tooother пользователей).</span><span class="sxs-lookup"><span data-stu-id="20e43-117">Owner (pull, push, and assign roles tooother users).</span></span>

<span data-ttu-id="20e43-118">Анонимный доступ к реестрам контейнеров Azure невозможен.</span><span class="sxs-lookup"><span data-stu-id="20e43-118">Anonymous access is not available on Azure Container Registries.</span></span> <span data-ttu-id="20e43-119">Для общедоступных образов можно использовать [концентратор Docker](https://docs.docker.com/docker-hub/).</span><span class="sxs-lookup"><span data-stu-id="20e43-119">For public images you can use [Docker Hub](https://docs.docker.com/docker-hub/).</span></span>

<span data-ttu-id="20e43-120">Можно назначить несколько участников службы реестра tooa, позволяющий получить доступ toodefine для различных пользователей или приложений.</span><span class="sxs-lookup"><span data-stu-id="20e43-120">You can assign multiple service principals tooa registry, which allows you toodefine access for different users or applications.</span></span> <span data-ttu-id="20e43-121">Также можно включить субъекты-службы реестра tooa «без монитора» подключение в разработчик или DevOps сценариев, таких как hello следующие примеры:</span><span class="sxs-lookup"><span data-stu-id="20e43-121">Service principals also enable "headless" connectivity tooa registry in developer or DevOps scenarios such as hello following examples:</span></span>

  * <span data-ttu-id="20e43-122">Развертывания контейнера из систем tooorchestration реестра, включая DC/OS, помощью Docker Swarm и Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="20e43-122">Container deployments from a registry tooorchestration systems including DC/OS, Docker Swarm and Kubernetes.</span></span> <span data-ttu-id="20e43-123">Можно также извлечь контейнера реестры toorelated служб Azure например [контейнера службы](../container-service/index.yml), [службы приложений](../app-service/index.md), [пакета](../batch/index.md), [Service Fabric](/azure/service-fabric/)и др.</span><span class="sxs-lookup"><span data-stu-id="20e43-123">You can also pull container registries toorelated Azure services such as [Container Service](../container-service/index.yml), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/), and others.</span></span>

  * <span data-ttu-id="20e43-124">Непрерывной интеграции и развертывания решений (например, Visual Studio Team Services или Jenkins), создающие образов контейнеров и отправить их tooa реестра.</span><span class="sxs-lookup"><span data-stu-id="20e43-124">Continuous integration and deployment solutions (such as Visual Studio Team Services or Jenkins) that build container images and push them tooa registry.</span></span>





## <a name="admin-account"></a><span data-ttu-id="20e43-125">Учетная запись администратора</span><span class="sxs-lookup"><span data-stu-id="20e43-125">Admin account</span></span>
<span data-ttu-id="20e43-126">При создании реестра вместе с ним автоматически создается учетная запись администратора.</span><span class="sxs-lookup"><span data-stu-id="20e43-126">With each registry you create, an admin account gets created automatically.</span></span> <span data-ttu-id="20e43-127">По умолчанию hello учетная запись отключена, но вы можете включить его и управлять hello учетные данные, например с помощью hello [портала](container-registry-get-started-portal.md#manage-registry-settings) или с помощью hello [команды Azure CLI 2.0](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span><span class="sxs-lookup"><span data-stu-id="20e43-127">By default hello account is disabled, but you can enable it and manage hello credentials, for example through hello [portal](container-registry-get-started-portal.md#manage-registry-settings) or using hello [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span></span> <span data-ttu-id="20e43-128">Каждой учетной записи администратора предоставляются два пароля, каждый из которых можно создать повторно.</span><span class="sxs-lookup"><span data-stu-id="20e43-128">Each admin account is provided with two passwords, both of which can be regenerated.</span></span> <span data-ttu-id="20e43-129">два пароля Hello разрешить реестра toohello toomaintain подключения с помощью один пароль при повторном создании hello другим паролем.</span><span class="sxs-lookup"><span data-stu-id="20e43-129">hello two passwords allow you toomaintain connections toohello registry by using one password while you regenerate hello other password.</span></span> <span data-ttu-id="20e43-130">Если включена учетная запись hello, можно передать имя пользователя hello и либо пароль toohello `docker login` для обычной проверки подлинности toohello реестра.</span><span class="sxs-lookup"><span data-stu-id="20e43-130">If hello account is enabled, you can pass hello user name and either password toohello `docker login` command for basic authentication toohello registry.</span></span> <span data-ttu-id="20e43-131">Например:</span><span class="sxs-lookup"><span data-stu-id="20e43-131">For example:</span></span>

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> <span data-ttu-id="20e43-132">Учетная запись администратора Hello предназначен для реестра hello tooaccess одного пользователя, главным образом для целей тестирования.</span><span class="sxs-lookup"><span data-stu-id="20e43-132">hello admin account is designed for a single user tooaccess hello registry, mainly for test purposes.</span></span> <span data-ttu-id="20e43-133">Не рекомендуется учетных данных администратора hello tooshare среди других пользователей.</span><span class="sxs-lookup"><span data-stu-id="20e43-133">It is not recommended tooshare hello admin account credentials among other users.</span></span> <span data-ttu-id="20e43-134">Все пользователи отображаются в виде файла реестра toohello одного пользователя.</span><span class="sxs-lookup"><span data-stu-id="20e43-134">All users appear as a single user toohello registry.</span></span> <span data-ttu-id="20e43-135">Отключает доступ к реестру для всех пользователей, которые используют учетные данные hello, изменения или отключения этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="20e43-135">Changing or disabling this account disables registry access for all users who use hello credentials.</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="20e43-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="20e43-136">Next steps</span></span>
* <span data-ttu-id="20e43-137">[Принудительная первый образ с помощью Docker CLI hello](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="20e43-137">[Push your first image using hello Docker CLI](container-registry-get-started-docker-cli.md).</span></span>
* <span data-ttu-id="20e43-138">Дополнительные сведения о проверке подлинности в режиме предварительного просмотра hello реестре контейнеров см. в разделе hello [блога](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span><span class="sxs-lookup"><span data-stu-id="20e43-138">For more information about authentication in hello Container Registry preview, see hello [blog post](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span></span>
