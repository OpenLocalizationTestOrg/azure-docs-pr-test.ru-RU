---
title: "tooAzure aaaDeploy экземпляры контейнером из hello реестра контейнера Azure | Azure документы"
description: "Развертывание экземпляров tooAzure контейнера из hello реестра контейнера Azure"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2667f91db8ed92a9ccc9ba722a2b1f5c5ea93886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-container-instances-from-hello-azure-container-registry"></a><span data-ttu-id="61746-103">Развертывание экземпляров tooAzure контейнера из hello реестра контейнера Azure</span><span class="sxs-lookup"><span data-stu-id="61746-103">Deploy tooAzure Container Instances from hello Azure Container Registry</span></span>

<span data-ttu-id="61746-104">Hello реестра контейнера Azure является Azure, частного реестра образов контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="61746-104">hello Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="61746-105">В этой статье рассказывается, как образы контейнеров toodeploy хранить в hello Azure контейнер реестра tooAzure экземпляры контейнером.</span><span class="sxs-lookup"><span data-stu-id="61746-105">This article covers how toodeploy container images stored in hello Azure Container Registry tooAzure Container Instances.</span></span>

## <a name="using-hello-azure-cli"></a><span data-ttu-id="61746-106">С помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="61746-106">Using hello Azure CLI</span></span>

<span data-ttu-id="61746-107">Hello Azure CLI содержит команды для создания и управления контейнерами в экземплярах контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="61746-107">hello Azure CLI includes commands for creating and managing containers in Azure Container Instances.</span></span> <span data-ttu-id="61746-108">Если указать собственный образ в hello `create` команды, можно также указать hello изображения реестра требуется пароль tooauthenticate с контейнер реестра hello.</span><span class="sxs-lookup"><span data-stu-id="61746-108">If you specify a private image in hello `create` command, you can also specify hello image registry password required tooauthenticate with hello container registry.</span></span>

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

<span data-ttu-id="61746-109">Hello `create` команды также поддерживается указание hello `registry-login-server` и `registry-username`.</span><span class="sxs-lookup"><span data-stu-id="61746-109">hello `create` command also supports specifying hello `registry-login-server` and `registry-username`.</span></span> <span data-ttu-id="61746-110">Тем не менее, всегда является hello серверу входа в систему для hello Azure контейнер реестра *registryname*. azurecr.io и hello пользователя по умолчанию — *registryname*, поэтому эти значения выводятся из hello имя изображения, если не заданы явным образом.</span><span class="sxs-lookup"><span data-stu-id="61746-110">However, hello login server for hello Azure Container Registry is always *registryname*.azurecr.io and hello default username is *registryname*, so these values are inferred from hello image name if not explicitly provided.</span></span>

## <a name="using-an-azure-resource-manager-template"></a><span data-ttu-id="61746-111">Использование шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="61746-111">Using an Azure Resource Manager template</span></span>

<span data-ttu-id="61746-112">Можно указать свойства hello реестра контейнера Azure в шаблоне Azure Resource Manager, включая hello `imageRegistryCredentials` свойство в определение группы hello контейнера:</span><span class="sxs-lookup"><span data-stu-id="61746-112">You can specify hello properties of your Azure Container Registry in an Azure Resource Manager template by including hello `imageRegistryCredentials` property in hello container group definition:</span></span>

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

<span data-ttu-id="61746-113">хранение пароля реестра контейнера непосредственно в шаблон hello tooavoid рекомендуется хранить как секрет в [хранилище ключей Azure](../key-vault/key-vault-manage-with-cli2.md) и ссылаться на него в шаблоне hello, с помощью hello [естественная интеграция между Здравствуйте, диспетчер ресурсов Azure и хранилище ключей](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="61746-113">tooavoid storing your container registry password directly in hello template, we recommend that you store it as a secret in [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) and reference it in hello template using hello [native integration between hello Azure Resource Manager and Key Vault](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span>

## <a name="using-hello-azure-portal"></a><span data-ttu-id="61746-114">С помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="61746-114">Using hello Azure portal</span></span>

<span data-ttu-id="61746-115">Если хранятся образы контейнеров в hello реестра контейнера Azure, можно легко создать контейнер в Azure экземпляры контейнером, с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="61746-115">If you maintain container images in hello Azure Container Registry, you can easily create a container in Azure Container Instances using hello Azure portal.</span></span>

1. <span data-ttu-id="61746-116">В hello портал Azure перейдите на контейнер реестра tooyour.</span><span class="sxs-lookup"><span data-stu-id="61746-116">In hello Azure portal, navigate tooyour container registry.</span></span>

2. <span data-ttu-id="61746-117">Выберите "Репозитории".</span><span class="sxs-lookup"><span data-stu-id="61746-117">Choose Repositories.</span></span>

    ![меню реестр контейнера Azure Hello в hello портал Azure][acr-menu]

3. <span data-ttu-id="61746-119">Выберите репозиторий hello нужного toodeploy из.</span><span class="sxs-lookup"><span data-stu-id="61746-119">Choose hello repository that you want toodeploy from.</span></span>

4. <span data-ttu-id="61746-120">Щелкните правой кнопкой мыши hello тег для образа контейнера hello требуется toodeploy.</span><span class="sxs-lookup"><span data-stu-id="61746-120">Right-click hello tag for hello container image you want toodeploy.</span></span>

    ![Контекстное меню запуска контейнера с помощью службы "Экземпляры контейнеров Azure"][acr-runinstance-contextmenu]

5. <span data-ttu-id="61746-122">Введите имя для контейнера hello и имя группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="61746-122">Enter a name for hello container and a name for hello resource group.</span></span> <span data-ttu-id="61746-123">При желании можно также изменить значения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="61746-123">You can also change hello default values if you wish.</span></span>

    ![Меню "Создание" для службы "Экземпляры контейнеров Azure"][acr-create-deeplink]

6. <span data-ttu-id="61746-125">После завершения развертывания hello можно перемещаться toohello контейнер группы из области toofind hello уведомления свой IP-адрес и другие свойства.</span><span class="sxs-lookup"><span data-stu-id="61746-125">Once hello deployment completes, you can navigate toohello container group from hello notifications pane toofind its IP address and other properties.</span></span>

    ![Представление сведений для группы контейнеров службы "Экземпляры контейнеров Azure"][aci-detailsview]

## <a name="next-steps"></a><span data-ttu-id="61746-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="61746-127">Next steps</span></span>

<span data-ttu-id="61746-128">Узнайте, как отправить их tooa закрытый контейнер реестра и развернуть их экземпляры контейнером tooAzure по контейнеры toobuild [завершения учебника hello](container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="61746-128">Learn how toobuild containers, push them tooa private container registry, and deploy them tooAzure Container Instances by [completing hello tutorial](container-instances-tutorial-prepare-app.md).</span></span>

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
