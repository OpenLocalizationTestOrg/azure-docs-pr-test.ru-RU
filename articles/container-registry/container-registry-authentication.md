---
title: "Проверка подлинности в реестре контейнеров Azure | Документация Майкрософт"
description: "Сведения о входе в реестр контейнеров Azure с помощью субъекта-службы Azure Active Directory или учетной записи администратора"
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
ms.openlocfilehash: aa2a6bf3d7d9ec22020036851fc0f2bca37e31bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a><span data-ttu-id="01f7a-103">Аутентификация с помощью частного реестра контейнеров Docker</span><span class="sxs-lookup"><span data-stu-id="01f7a-103">Authenticate with a private Docker container registry</span></span>
<span data-ttu-id="01f7a-104">Чтобы приступить к работе с образами контейнеров в реестре контейнеров Azure, нужно войти в систему, выполнив команду `docker login`.</span><span class="sxs-lookup"><span data-stu-id="01f7a-104">To work with container images in an Azure container registry, you log in using the `docker login` command.</span></span> <span data-ttu-id="01f7a-105">Вы можете войти, используя **[субъект-службу Azure Active Directory](../active-directory/active-directory-application-objects.md)** или специальную **учетную запись администратора**.</span><span class="sxs-lookup"><span data-stu-id="01f7a-105">You can log in using either an **[Azure Active Directory service principal](../active-directory/active-directory-application-objects.md)** or a registry-specific **admin account**.</span></span> <span data-ttu-id="01f7a-106">В этой статье содержатся подробные сведения об этих удостоверениях.</span><span class="sxs-lookup"><span data-stu-id="01f7a-106">This article provides more detail about these identities.</span></span>



## <a name="service-principal"></a><span data-ttu-id="01f7a-107">Субъект-служба</span><span class="sxs-lookup"><span data-stu-id="01f7a-107">Service principal</span></span>

<span data-ttu-id="01f7a-108">Вы можете [назначить своему реестру субъект-службу](container-registry-get-started-azure-cli.md#assign-a-service-principal) и использовать ее для базовой проверки подлинности Docker.</span><span class="sxs-lookup"><span data-stu-id="01f7a-108">You can [assign a service principal](container-registry-get-started-azure-cli.md#assign-a-service-principal) to your registry and use it for basic Docker authentication.</span></span> <span data-ttu-id="01f7a-109">Мы рекомендуем использовать субъект-службу в большинстве сценариев.</span><span class="sxs-lookup"><span data-stu-id="01f7a-109">Using a service principal is recommended for most scenarios.</span></span> <span data-ttu-id="01f7a-110">Укажите идентификатор и пароль приложения для субъекта-службы в команде `docker login`, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="01f7a-110">Provide the app ID and password of the service principal to the `docker login` command, as shown in the following example:</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="01f7a-111">После входа в систему Docker кэширует учетные данные, поэтому вам не нужно запоминать идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="01f7a-111">Once logged in, Docker caches the credentials, so you don't need to remember the app ID.</span></span>

> [!TIP]
> <span data-ttu-id="01f7a-112">При необходимости пароль субъекта-службы можно создать повторно, выполнив команду `az ad sp reset-credentials`.</span><span class="sxs-lookup"><span data-stu-id="01f7a-112">If you want, you can regenerate the password of a service principal by running the `az ad sp reset-credentials` command.</span></span>
>


<span data-ttu-id="01f7a-113">Субъекты-службы поддерживают [доступ на основе ролей](../active-directory/role-based-access-control-configure.md) к реестру.</span><span class="sxs-lookup"><span data-stu-id="01f7a-113">Service principals allow [role-based access](../active-directory/role-based-access-control-configure.md) to a registry.</span></span> <span data-ttu-id="01f7a-114">Доступные роли:</span><span class="sxs-lookup"><span data-stu-id="01f7a-114">Available roles are:</span></span>
  * <span data-ttu-id="01f7a-115">Читатель (доступ только для получения).</span><span class="sxs-lookup"><span data-stu-id="01f7a-115">Reader (pull only access).</span></span>
  * <span data-ttu-id="01f7a-116">Участник (получение и отправка).</span><span class="sxs-lookup"><span data-stu-id="01f7a-116">Contributor (pull and push).</span></span>
  * <span data-ttu-id="01f7a-117">Владелец (получение, отправка и назначение ролей другим пользователям).</span><span class="sxs-lookup"><span data-stu-id="01f7a-117">Owner (pull, push, and assign roles to other users).</span></span>

<span data-ttu-id="01f7a-118">Анонимный доступ к реестрам контейнеров Azure невозможен.</span><span class="sxs-lookup"><span data-stu-id="01f7a-118">Anonymous access is not available on Azure Container Registries.</span></span> <span data-ttu-id="01f7a-119">Для общедоступных образов можно использовать [концентратор Docker](https://docs.docker.com/docker-hub/).</span><span class="sxs-lookup"><span data-stu-id="01f7a-119">For public images you can use [Docker Hub](https://docs.docker.com/docker-hub/).</span></span>

<span data-ttu-id="01f7a-120">Для реестра можно назначить несколько субъектов-служб. Это позволяет определять доступ для разных пользователей и приложений.</span><span class="sxs-lookup"><span data-stu-id="01f7a-120">You can assign multiple service principals to a registry, which allows you to define access for different users or applications.</span></span> <span data-ttu-id="01f7a-121">Субъекты-службы также позволяют выполнять автономное подключение к реестру в сценариях DevOps и разработки, как в приведенных ниже примерах.</span><span class="sxs-lookup"><span data-stu-id="01f7a-121">Service principals also enable "headless" connectivity to a registry in developer or DevOps scenarios such as the following examples:</span></span>

  * <span data-ttu-id="01f7a-122">Развертывания контейнеров из реестра в системы управления, в том числе DC/OS, Docker Swarm и Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="01f7a-122">Container deployments from a registry to orchestration systems including DC/OS, Docker Swarm and Kubernetes.</span></span> <span data-ttu-id="01f7a-123">Реестры контейнеров также можно отправлять в связанные службы Azure, например в [службу контейнеров](../container-service/index.yml), [службу приложений](../app-service/index.md), [пакетную службу](../batch/index.md), [Service Fabric](/azure/service-fabric/) и другие.</span><span class="sxs-lookup"><span data-stu-id="01f7a-123">You can also pull container registries to related Azure services such as [Container Service](../container-service/index.yml), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/), and others.</span></span>

  * <span data-ttu-id="01f7a-124">Решения непрерывной интеграции и развертывания (например, Visual Studio Team Services или Jenkins), создающие образы контейнеров и отправляющие их в реестр.</span><span class="sxs-lookup"><span data-stu-id="01f7a-124">Continuous integration and deployment solutions (such as Visual Studio Team Services or Jenkins) that build container images and push them to a registry.</span></span>





## <a name="admin-account"></a><span data-ttu-id="01f7a-125">Учетная запись администратора</span><span class="sxs-lookup"><span data-stu-id="01f7a-125">Admin account</span></span>
<span data-ttu-id="01f7a-126">При создании реестра вместе с ним автоматически создается учетная запись администратора.</span><span class="sxs-lookup"><span data-stu-id="01f7a-126">With each registry you create, an admin account gets created automatically.</span></span> <span data-ttu-id="01f7a-127">По умолчанию эта учетная запись отключена, но ее можно включить, а также можно настроить учетные данные, например на [портале](container-registry-get-started-portal.md#manage-registry-settings) или с помощью [команд Azure CLI 2.0](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span><span class="sxs-lookup"><span data-stu-id="01f7a-127">By default the account is disabled, but you can enable it and manage the credentials, for example through the [portal](container-registry-get-started-portal.md#manage-registry-settings) or using the [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span></span> <span data-ttu-id="01f7a-128">Каждой учетной записи администратора предоставляются два пароля, каждый из которых можно создать повторно.</span><span class="sxs-lookup"><span data-stu-id="01f7a-128">Each admin account is provided with two passwords, both of which can be regenerated.</span></span> <span data-ttu-id="01f7a-129">Благодаря этому вы можете подключаться к реестру, используя один пароль, пока второй создается повторно.</span><span class="sxs-lookup"><span data-stu-id="01f7a-129">The two passwords allow you to maintain connections to the registry by using one password while you regenerate the other password.</span></span> <span data-ttu-id="01f7a-130">Если учетная запись включена, вы можете указать в команде `docker login` имя пользователя и пароль для обычной проверки подлинности в реестре.</span><span class="sxs-lookup"><span data-stu-id="01f7a-130">If the account is enabled, you can pass the user name and either password to the `docker login` command for basic authentication to the registry.</span></span> <span data-ttu-id="01f7a-131">Например:</span><span class="sxs-lookup"><span data-stu-id="01f7a-131">For example:</span></span>

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> <span data-ttu-id="01f7a-132">Учетная запись администратора предоставляет доступ к реестру одному пользователю. Она предназначена, главным образом, для тестирования.</span><span class="sxs-lookup"><span data-stu-id="01f7a-132">The admin account is designed for a single user to access the registry, mainly for test purposes.</span></span> <span data-ttu-id="01f7a-133">Мы не рекомендуем обмениваться учетными данными учетной записи администратора с другими пользователями.</span><span class="sxs-lookup"><span data-stu-id="01f7a-133">It is not recommended to share the admin account credentials among other users.</span></span> <span data-ttu-id="01f7a-134">В реестре все пользователи отображаются как один пользователь.</span><span class="sxs-lookup"><span data-stu-id="01f7a-134">All users appear as a single user to the registry.</span></span> <span data-ttu-id="01f7a-135">Изменив или отключив эту учетную запись, вы ограничите доступ к реестру для пользователей, использующих эти учетные данные.</span><span class="sxs-lookup"><span data-stu-id="01f7a-135">Changing or disabling this account disables registry access for all users who use the credentials.</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="01f7a-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="01f7a-136">Next steps</span></span>
* <span data-ttu-id="01f7a-137">[Отправьте свой первый образ с помощью интерфейса командной строки Docker.](container-registry-get-started-docker-cli.md)</span><span class="sxs-lookup"><span data-stu-id="01f7a-137">[Push your first image using the Docker CLI](container-registry-get-started-docker-cli.md).</span></span>
* <span data-ttu-id="01f7a-138">Дополнительные сведения о проверке подлинности в предварительной версии реестра контейнеров см. в [этой записи блога](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span><span class="sxs-lookup"><span data-stu-id="01f7a-138">For more information about authentication in the Container Registry preview, see the [blog post](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span></span>
