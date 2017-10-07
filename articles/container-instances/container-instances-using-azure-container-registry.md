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
# <a name="deploy-tooazure-container-instances-from-hello-azure-container-registry"></a>Развертывание экземпляров tooAzure контейнера из hello реестра контейнера Azure

Hello реестра контейнера Azure является Azure, частного реестра образов контейнера Docker. В этой статье рассказывается, как образы контейнеров toodeploy хранить в hello Azure контейнер реестра tooAzure экземпляры контейнером.

## <a name="using-hello-azure-cli"></a>С помощью hello Azure CLI

Hello Azure CLI содержит команды для создания и управления контейнерами в экземплярах контейнера Azure. Если указать собственный образ в hello `create` команды, можно также указать hello изображения реестра требуется пароль tooauthenticate с контейнер реестра hello.

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

Hello `create` команды также поддерживается указание hello `registry-login-server` и `registry-username`. Тем не менее, всегда является hello серверу входа в систему для hello Azure контейнер реестра *registryname*. azurecr.io и hello пользователя по умолчанию — *registryname*, поэтому эти значения выводятся из hello имя изображения, если не заданы явным образом.

## <a name="using-an-azure-resource-manager-template"></a>Использование шаблона Azure Resource Manager

Можно указать свойства hello реестра контейнера Azure в шаблоне Azure Resource Manager, включая hello `imageRegistryCredentials` свойство в определение группы hello контейнера:

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

хранение пароля реестра контейнера непосредственно в шаблон hello tooavoid рекомендуется хранить как секрет в [хранилище ключей Azure](../key-vault/key-vault-manage-with-cli2.md) и ссылаться на него в шаблоне hello, с помощью hello [естественная интеграция между Здравствуйте, диспетчер ресурсов Azure и хранилище ключей](../azure-resource-manager/resource-manager-keyvault-parameter.md).

## <a name="using-hello-azure-portal"></a>С помощью портала Azure hello

Если хранятся образы контейнеров в hello реестра контейнера Azure, можно легко создать контейнер в Azure экземпляры контейнером, с помощью hello портал Azure.

1. В hello портал Azure перейдите на контейнер реестра tooyour.

2. Выберите "Репозитории".

    ![меню реестр контейнера Azure Hello в hello портал Azure][acr-menu]

3. Выберите репозиторий hello нужного toodeploy из.

4. Щелкните правой кнопкой мыши hello тег для образа контейнера hello требуется toodeploy.

    ![Контекстное меню запуска контейнера с помощью службы "Экземпляры контейнеров Azure"][acr-runinstance-contextmenu]

5. Введите имя для контейнера hello и имя группы ресурсов hello. При желании можно также изменить значения по умолчанию hello.

    ![Меню "Создание" для службы "Экземпляры контейнеров Azure"][acr-create-deeplink]

6. После завершения развертывания hello можно перемещаться toohello контейнер группы из области toofind hello уведомления свой IP-адрес и другие свойства.

    ![Представление сведений для группы контейнеров службы "Экземпляры контейнеров Azure"][aci-detailsview]

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как отправить их tooa закрытый контейнер реестра и развернуть их экземпляры контейнером tooAzure по контейнеры toobuild [завершения учебника hello](container-instances-tutorial-prepare-app.md).

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
