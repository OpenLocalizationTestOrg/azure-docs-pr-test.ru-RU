---
title: "Учебник контейнера службы aaaAzure - Подготовка контроля доступа | Документы Microsoft"
description: "Руководство по службе контейнеров Azure — подготовка ACR"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 3980e5ce4eb9836f83c761a2f76c944bb3f13060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a>Развертывание реестра контейнеров Azure и его использование

Реестр контейнеров Azure (ACR) является частным реестром на базе Azure для образов контейнеров Docker. Этот учебник, часть два из семи, пошаговое руководство по развертыванию экземпляра реестра контейнера Azure и опубликуйте tooit образа контейнера. В частности, рассматриваются такие шаги:

> [!div class="checklist"]
> * развертывание экземпляра реестра контейнеров Azure (ACR);
> * добавление тегов к образу контейнера для ACR;
> * Отправка изображения tooACR hello

В последующих руководствах данный экземпляр ACR интегрируется с кластером Kubernetes службы контейнеров Azure для безопасного выполнения образов контейнеров. 

## <a name="before-you-begin"></a>Перед началом работы

В hello [с предыдущим учебником](./container-service-tutorial-kubernetes-prepare-app.md), образ контейнера был создан для простого приложения Azure с правом голоса. В этом учебнике это изображение помещается tooan реестра контейнера Azure. Если вы не создали образа приложения Azure с правом голоса hello, возвращают слишком[учебник 1 – Создание образов контейнеров](./container-service-tutorial-kubernetes-prepare-app.md). Кроме того действия hello описанный здесь работают с любой образ контейнера.

Что вы используете версию Azure CLI hello 2.0.4 упражнений этого учебника нужен или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="deploy-azure-container-registry"></a>Развертывание реестра контейнеров Azure

При развертывании реестра контейнеров Azure сначала необходимо создать группу ресурсов. Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.

Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды. В этом примере имя группы ресурсов *myResourceGroup* создается в hello *westeurope* области.

```azurecli
az group create --name myResourceGroup --location westeurope
```

Создайте в реестре контейнера Azure с hello [создать az acr](/cli/azure/acr#create) команды. Имя контейнера реестра Hello **должно быть уникальным**.

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

На протяжении hello конца данного учебника «acrname» используется как заполнитель для hello контейнер реестра с выбранным именем.

## <a name="container-registry-login"></a>Вход в реестр контейнеров

Необходимо войти в экземпляре ACR tooyour до отправки tooit изображения. Используйте hello [входа acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) команды toocomplete hello операции. Необходимо tooprovide hello уникальное имя, заданное реестра toohello контейнера, при его создании.

```azurecli
az acr login --name <acrName>
```

Команда Hello возвращает сообщение «Успешно выполнен вход» после завершения.

## <a name="tag-container-images"></a>Присвоение тегов образам контейнеров

Каждый образ контейнера должен toobe тегом hello loginServer имя реестра hello. Данный тег используется для маршрутизации при принудительной установке реестра образов tooan образы контейнера.

список текущего изображения, используйте hello toosee [образов docker](https://docs.docker.com/engine/reference/commandline/images/) команды.

```bash
docker images
```

Выходные данные:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

hello loginServer tooget имя, запустите следующую команду hello.

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

Теперь hello тег *azure голос передней панели* изображение с loginServer hello hello контейнер реестра. Кроме того, добавьте `:redis-v1` toohello конец hello имя образа. Этот тег указывает версию образа hello.

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

После с тегами, выполните операцию hello tooverify (https://docs.docker.com/engine/reference/commandline/images/) [образов docker].

```bash
docker images
```

Выходные данные:

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-tooregistry"></a>Принудительная tooregistry изображений

Принудительная hello *azure голос передней панели* реестра toohello изображения. 

Используя следующий пример hello, замените имя loginServer ACR hello loginServer hello из среды.

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

Это занимает несколько минут toocomplete.

## <a name="list-images-in-registry"></a>Перечисление образов в реестре

tooreturn список образов, которые передаются реестра tooyour контейнера Azure, пользователь hello [списка репозитория acr az](/cli/azure/acr/repository#list) команды. Обновление hello команды с именем экземпляра ACR hello.

```azurecli
az acr repository list --name <acrName> --output table
```

Выходные данные:

```azurecli
Result
----------------
azure-vote-front
```

А затем toosee hello тегов для определенного образа, используйте hello [acr репозитория az show теги](/cli/azure/acr/repository#show-tags) команды.

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

Выходные данные:

```azurecli
Result
--------
redis-v1
```

По завершении учебника образ контейнера hello хранилось в закрытого экземпляра реестра контейнера Azure. Этот образ развертывается из кластера Kubernetes tooa контроля доступа в последующих учебники.

## <a name="next-steps"></a>Дальнейшие действия

В этом руководстве вы подготовили реестр контейнеров Azure для использования в кластере Kubernetes ACS. Привет, следующие шаги были выполнены:

> [!div class="checklist"]
> * развертывание экземпляра реестра контейнеров Azure;
> * добавление тегов к образу контейнера для ACR;
> * Отправленный hello tooACR изображения

Переместить следующий учебник toolearn toohello о развертывании Kubernetes кластера в Azure.

> [!div class="nextstepaction"]
> [Развертывание кластера Kubernetes в службе контейнеров Azure](./container-service-tutorial-kubernetes-deploy-cluster.md)