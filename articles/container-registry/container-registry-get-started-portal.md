---
title: "aaaCreate частного реестра Docker - портал Azure | Документы Microsoft"
description: "Начать создание и управление ими частных реестрах контейнера Docker с hello портал Azure"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40f3ce44fea26e5fbeca865c9da6df55c2df9511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-portal"></a><span data-ttu-id="7bd32-103">Создание частного реестра контейнера Docker, с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="7bd32-103">Create a private Docker container registry using hello Azure portal</span></span>
<span data-ttu-id="7bd32-104">Использование hello Azure портала toocreate реестре контейнеров и управления его параметры.</span><span class="sxs-lookup"><span data-stu-id="7bd32-104">Use hello Azure portal toocreate a container registry and manage its settings.</span></span> <span data-ttu-id="7bd32-105">Можно также создать и управлять контейнера реестры с помощью hello [команды Azure CLI 2.0](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) или программным путем с контейнер реестра hello [API-интерфейса REST](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="7bd32-105">You can also create and manage container registries using hello [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>

<span data-ttu-id="7bd32-106">Сведения и основные понятия, в разделе [hello Обзор](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="7bd32-106">For background and concepts, see [hello overview](container-registry-intro.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="7bd32-107">Создание реестра контейнеров</span><span class="sxs-lookup"><span data-stu-id="7bd32-107">Create a container registry</span></span>
1. <span data-ttu-id="7bd32-108">В hello [портал Azure](https://portal.azure.com), нажмите кнопку **+ создать**.</span><span class="sxs-lookup"><span data-stu-id="7bd32-108">In hello [Azure portal](https://portal.azure.com), click **+ New**.</span></span>
2. <span data-ttu-id="7bd32-109">Поиск hello marketplace для **контейнер Azure реестра**.</span><span class="sxs-lookup"><span data-stu-id="7bd32-109">Search hello marketplace for **Azure container registry**.</span></span>
3. <span data-ttu-id="7bd32-110">Выберите **реестр контейнеров Azure** (издатель — корпорация **Майкрософт**).</span><span class="sxs-lookup"><span data-stu-id="7bd32-110">Select **Azure Container Registry**, with publisher **Microsoft**.</span></span>
    <span data-ttu-id="7bd32-111">![Служба реестра контейнеров в Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span><span class="sxs-lookup"><span data-stu-id="7bd32-111">![Container Registry service in Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span></span>
4. <span data-ttu-id="7bd32-112">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7bd32-112">Click **Create**.</span></span> <span data-ttu-id="7bd32-113">Hello **реестра контейнера Azure** колонке отображается.</span><span class="sxs-lookup"><span data-stu-id="7bd32-113">hello **Azure Container Registry** blade appears.</span></span>

    ![Параметры реестра контейнеров](./media/container-registry-get-started-portal/container-registry-settings.png)
5. <span data-ttu-id="7bd32-115">В hello **реестра контейнера Azure** колонки, введите следующую информацию hello.</span><span class="sxs-lookup"><span data-stu-id="7bd32-115">In hello **Azure Container Registry** blade, enter hello following information.</span></span> <span data-ttu-id="7bd32-116">Закончив, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7bd32-116">Click **Create** when you are done.</span></span>

    <span data-ttu-id="7bd32-117">а.</span><span class="sxs-lookup"><span data-stu-id="7bd32-117">a.</span></span> <span data-ttu-id="7bd32-118">**Имя реестра** — глобальное уникальное доменное имя верхнего уровня для определенного реестра.</span><span class="sxs-lookup"><span data-stu-id="7bd32-118">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="7bd32-119">В этом примере — имя реестра hello *myRegistry01*, но заменить собственным уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="7bd32-119">In this example, hello registry name is *myRegistry01*, but substitute a unique name of your own.</span></span> <span data-ttu-id="7bd32-120">Hello имя может содержать только буквы и цифры.</span><span class="sxs-lookup"><span data-stu-id="7bd32-120">hello name can contain only letters and numbers.</span></span>

    <span data-ttu-id="7bd32-121">b.</span><span class="sxs-lookup"><span data-stu-id="7bd32-121">b.</span></span> <span data-ttu-id="7bd32-122">**Группа ресурсов**: выберите существующую [группы ресурсов](../azure-resource-manager/resource-group-overview.md#resource-groups) или имя типа hello новую.</span><span class="sxs-lookup"><span data-stu-id="7bd32-122">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span>

    <span data-ttu-id="7bd32-123">c.</span><span class="sxs-lookup"><span data-stu-id="7bd32-123">c.</span></span> <span data-ttu-id="7bd32-124">**Расположение**: Выбор расположения центра обработки данных Azure, где hello службы [доступных](https://azure.microsoft.com/regions/services/), такие как **центральных штатах юга США**.</span><span class="sxs-lookup"><span data-stu-id="7bd32-124">**Location**: Select an Azure datacenter location where hello service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="7bd32-125">d.</span><span class="sxs-lookup"><span data-stu-id="7bd32-125">d.</span></span> <span data-ttu-id="7bd32-126">**Пользователю с правами администратора**: следует включить в реестре hello tooaccess пользователя администратора.</span><span class="sxs-lookup"><span data-stu-id="7bd32-126">**Admin user**: If you want, enable an admin user tooaccess hello registry.</span></span> <span data-ttu-id="7bd32-127">Можно изменить этот параметр после создания hello реестра.</span><span class="sxs-lookup"><span data-stu-id="7bd32-127">You can change this setting after creating hello registry.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="7bd32-128">В дополнение к этому tooproviding доступ через учетную запись пользователя admin, контейнера реестры поддержки проверки подлинности, поддерживаемый субъекты-службы Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7bd32-128">In addition tooproviding access through an admin user account, container registries support authentication backed by Azure Active Directory service principals.</span></span> <span data-ttu-id="7bd32-129">Дополнительные сведения и рекомендации см. в статье [Authenticate with the container registry](container-registry-authentication.md) (Проверка подлинности с помощью реестра контейнеров).</span><span class="sxs-lookup"><span data-stu-id="7bd32-129">For more information and considerations, see [Authenticate with a container registry](container-registry-authentication.md).</span></span>
      >

    <span data-ttu-id="7bd32-130">д.</span><span class="sxs-lookup"><span data-stu-id="7bd32-130">e.</span></span> <span data-ttu-id="7bd32-131">**Учетная запись хранения**: используйте toocreate параметр по умолчанию hello [учетной записи хранилища](../storage/common/storage-introduction.md), или выберите существующую учетную запись хранения в hello местоположения.</span><span class="sxs-lookup"><span data-stu-id="7bd32-131">**Storage account**: Use hello default setting toocreate a [storage account](../storage/common/storage-introduction.md), or select an existing storage account in hello same location.</span></span> <span data-ttu-id="7bd32-132">Хранилище класса Premium сейчас не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="7bd32-132">Currently Premium Storage is not supported.</span></span>

## <a name="manage-registry-settings"></a><span data-ttu-id="7bd32-133">Управление параметрами реестра</span><span class="sxs-lookup"><span data-stu-id="7bd32-133">Manage registry settings</span></span>
<span data-ttu-id="7bd32-134">После создания реестра hello, найти hello параметры реестра, начиная с hello **контейнера реестры** колонке hello портала.</span><span class="sxs-lookup"><span data-stu-id="7bd32-134">After creating hello registry, find hello registry settings by starting at hello **Container Registries** blade in hello portal.</span></span> <span data-ttu-id="7bd32-135">Например может потребоваться hello toolog параметры в реестре tooyour или может требуется tooenable или отключает hello пользователя с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="7bd32-135">For example, you might need hello settings toolog in tooyour registry, or you might want tooenable or disable hello admin user.</span></span>

1. <span data-ttu-id="7bd32-136">На hello **контейнера реестры** колонка, щелкните имя hello реестра.</span><span class="sxs-lookup"><span data-stu-id="7bd32-136">On hello **Container Registries** blade, click hello name of your registry.</span></span>

    ![Колонка "Container Registry (предварительная версия)"](./media/container-registry-get-started-portal/container-registry-blade.png)
2. <span data-ttu-id="7bd32-138">параметры доступа к toomanage, нажмите кнопку **ключ доступа**.</span><span class="sxs-lookup"><span data-stu-id="7bd32-138">toomanage access settings, click **Access key**.</span></span>

    ![Доступ к реестру контейнеров](./media/container-registry-get-started-portal/container-registry-access.png)
3. <span data-ttu-id="7bd32-140">Обратите внимание, hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="7bd32-140">Note hello following settings:</span></span>

   * <span data-ttu-id="7bd32-141">**Сервер входа в систему** -использовать toolog в реестре toohello полное имя hello.</span><span class="sxs-lookup"><span data-stu-id="7bd32-141">**Login server** - hello fully qualified name you use toolog in toohello registry.</span></span> <span data-ttu-id="7bd32-142">В нашем примере поисковый запрос будет выглядеть так: `myregistry01.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="7bd32-142">In this example, it is `myregistry01.azurecr.io`.</span></span>
   * <span data-ttu-id="7bd32-143">**Пользователю с правами администратора** - переключение tooenable или отключение учетной записи пользователя admin hello реестра.</span><span class="sxs-lookup"><span data-stu-id="7bd32-143">**Admin user** - Toggle tooenable or disable hello registry's admin user account.</span></span>
   * <span data-ttu-id="7bd32-144">**Имя пользователя** и **пароль** -hello учетные данные учетной записи пользователя admin hello (если он включен) можно использовать в реестре toohello toolog.</span><span class="sxs-lookup"><span data-stu-id="7bd32-144">**Username** and **Password** - hello credentials of hello admin user account (if enabled) you can use toolog in toohello registry.</span></span> <span data-ttu-id="7bd32-145">При необходимости можно создать повторно hello пароли.</span><span class="sxs-lookup"><span data-stu-id="7bd32-145">You can optionally regenerate hello passwords.</span></span> <span data-ttu-id="7bd32-146">Двух паролей создаются, чтобы сохранить подключения toohello реестра, используя один пароль, при повторном создании hello другим паролем.</span><span class="sxs-lookup"><span data-stu-id="7bd32-146">Two passwords are created so that you can maintain connections toohello registry by using one password while you regenerate hello other password.</span></span> <span data-ttu-id="7bd32-147">tooauthenticate с субъектом-службой. Вместо этого в разделе [аутентификация с помощью частного реестра контейнера Docker](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7bd32-147">tooauthenticate with a service principal instead, see [Authenticate with a private Docker container registry](container-registry-authentication.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7bd32-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7bd32-148">Next steps</span></span>
* [<span data-ttu-id="7bd32-149">Принудительная первый образ с помощью hello Docker CLI</span><span class="sxs-lookup"><span data-stu-id="7bd32-149">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
