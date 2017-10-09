---
title: "Учебник экземпляры контейнером aaaAzure - Подготовка реестра контейнера Azure | Документы Microsoft"
description: "Руководство по службе \"Экземпляры контейнеров Azure\". Подготовка реестра контейнеров Azure"
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2525626125740c3c861fad36aad207d0b587ff54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a>Развертывание реестра контейнеров Azure и его использование

Это вторая часть руководства, состоящего из трех частей. В hello [ранее](./container-instances-tutorial-prepare-app.md), был создан образ контейнера простого веб-приложения, написанные на [Node.js](http://nodejs.org). В этом учебнике это изображение помещается tooan реестра контейнера Azure. Если вы не создали hello образ контейнера, возвращают слишком[учебник 1 – Создание образа контейнера](./container-instances-tutorial-prepare-app.md). 

Hello реестра контейнера Azure является Azure, частного реестра образов контейнера Docker. Этот учебник Пошаговое руководство по развертыванию экземпляра реестра контейнера Azure и опубликуйте tooit образа контейнера. В частности, рассматриваются такие шаги:

> [!div class="checklist"]
> * Развертывание экземпляра реестра контейнеров Azure.
> * Добавление тегов к образу контейнера для помещения в реестр контейнеров Azure.
> * Отправка изображения tooAzure реестра контейнера

В последующих учебники развертывание hello контейнера из вашего частного реестра tooAzure экземпляры контейнером.

## <a name="before-you-begin"></a>Перед началом работы

Что вы используете версию Azure CLI hello 2.0.4 упражнений этого учебника нужен или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).

## <a name="deploy-azure-container-registry"></a>Развертывание реестра контейнеров Azure

При развертывании реестра контейнеров Azure сначала необходимо создать группу ресурсов. Группа ресурсов Azure — это логическая коллекция, в которой выполняется развертывание и администрирование ресурсов Azure.

Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды. В этом примере имя группы ресурсов *myResourceGroup* создается в hello *eastus* области.

```azurecli
az group create --name myResourceGroup --location eastus
```

Создайте в реестре контейнера Azure с hello [создать az acr](/cli/azure/acr#create) команды. Имя контейнера реестра Hello **должно быть уникальным**. В следующем примере hello, мы используем имя hello *mycontainerregistry082*.

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

На протяжении hello конца данного учебника мы используем `<acrname>` как заполнитель для hello контейнер реестра с выбранным именем.

## <a name="container-registry-login"></a>Вход в реестр контейнеров

Необходимо войти в экземпляре ACR tooyour до отправки tooit изображения. Используйте hello [входа acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) команды toocomplete hello операции. Необходимо tooprovide hello уникальное имя, заданное реестра toohello контейнера, при его создании.

```azurecli
az acr login --name <acrName>
```

Команда Hello возвращает сообщение «Успешно выполнен вход» после завершения.

## <a name="tag-container-image"></a>Добавление тега к образу контейнера

toodeploy образ контейнера из частного реестра hello образ нуждается toobe тегом hello `loginServer` имя реестра hello.

список текущего изображения, используйте hello toosee `docker images` команды.

```bash
docker images
```

Выходные данные:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

hello loginServer tooget имя, запустите следующую команду hello.

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

Тег hello *aci учебника приложений* изображение с loginServer hello hello контейнер реестра. Кроме того, добавьте `:v1` toohello конец hello имя образа. Этот тег указывает номер версии образа hello.

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

После тегов, выполните `docker images` tooverify hello операции.

```bash
docker images
```

Выходные данные:

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-tooazure-container-registry"></a>Принудительная tooAzure образ контейнера реестра

Принудительная hello *aci учебника приложения* toohello реестра образов.

Используя следующий пример hello, замените имя loginServer реестра контейнера hello loginServer hello из среды.

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a>Получение списка образов в реестре контейнеров Azure

tooreturn список образов, которые передаются реестра tooyour контейнера Azure, пользователь hello [списка репозитория acr az](/cli/azure/acr/repository#list) команды. Обновление hello команды с именем реестра hello контейнера.

```azurecli
az acr repository list --name <acrName> --output table
```

Выходные данные:

```azurecli
Result
----------------
aci-tutorial-app
```

А затем toosee hello тегов для определенного образа, используйте hello [acr репозитория az show теги](/cli/azure/acr/repository#show-tags) команды.

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

Выходные данные:

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике в реестре контейнера Azure был подготовлен для использования с экземплярами Azure контейнера и занесен hello образ контейнера. Привет, следующие шаги были выполнены:

> [!div class="checklist"]
> * Развертывание экземпляра реестра контейнеров Azure.
> * Добавление тегов к образу контейнера для помещения в реестр контейнеров Azure.
> * Отправка изображения tooAzure реестра контейнера

Переместить Далее учебника toolearn toohello о развертывании tooAzure hello контейнера, с помощью экземпляров контейнера Azure.

> [!div class="nextstepaction"]
> [Развертывание контейнеров tooAzure экземпляры контейнером](./container-instances-tutorial-deploy-app.md)
