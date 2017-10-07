---
title: "Учебник aaaAzure контейнера службы - приложение обновления | Документы Microsoft"
description: "Руководство по Службе контейнеров Azure: обновление приложения"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c467498bab7952926a18e45ffbb21051a98739d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="update-an-application-in-kubernetes"></a>Обновление приложения в Kubernetes

После развертывания приложения в Kubernetes его можно обновить, указав новый образ контейнера или версию образа. При обновлении приложения hello выпуска обновлений на промежуточное хранение, чтобы одновременно обновляется только часть hello развертывания. Это обновление промежуточные включает tookeep приложения hello, во время обновления hello и предоставляет механизм отката, если происходит сбой развертывания. 

В этом учебнике обновляется часть шести семью, приложение Azure голос образец hello. Здесь будут выполнены следующие задачи:

> [!div class="checklist"]
> * Обновление кода клиентского приложения hello
> * Создание обновленного образа контейнера.
> * Образ контейнера проталкивания hello tooAzure реестра контейнера
> * Развертывание образа контейнера обновленные hello

В последующих учебники Operations Management Suite — настроенное toomonitor hello Kubernetes кластер.

## <a name="before-you-begin"></a>Перед началом работы

В предыдущих учебниках приложение было упаковано в образ контейнера, отправить изображение hello, tooAzure реестра контейнера и создания кластера Kubernetes. приложение Hello затем была запущена на кластере Kubernetes hello. 

Если вы еще не выполнит эти действия и toofollow вдоль, возвращают слишком[учебник 1 – Создание образов контейнеров](./container-service-tutorial-kubernetes-prepare-app.md). 

## <a name="update-application"></a>Обновление приложения

toocomplete hello шагах данного учебника, вы должны клонировали копию hello приложения Azure голос. При необходимости создайте это Клонированная копия с hello следующую команду:

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

Откройте hello `config_file.cfg` файла с помощью любого редактора кода или текста. Можно найти этот файл в следующий каталог hello клонирования репозитория hello.

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

Изменить значения hello `VOTE1VALUE` и `VOTE2VALUE`, а затем сохраните файл hello.

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

Используйте [составления docker](https://docs.docker.com/compose/) toore-создать изображение переднего плана hello и выполнения hello обновления приложения.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a>Локальное тестирование приложения

Обзор слишком`http://localhost:8080` toosee hello обновленное приложение.

![Схема кластера Kubernetes в Аzure](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a>Пометка и отправка образов

Тег hello *azure голос передней панели* изображение с loginServer hello hello контейнер реестра.

Если вы используете реестра контейнера Azure, получения имени сервера hello входа с hello [az списка контроля доступа](/cli/azure/acr#list) команды.

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

Используйте [docker тега](https://docs.docker.com/engine/reference/commandline/tag/) tootag hello изображения. Замените `<acrLoginServer>` именем сервера входа реестра контейнеров Azure или именем узла общедоступного реестра.

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

Используйте [docker push](https://docs.docker.com/engine/reference/commandline/push/) tooupload hello изображения tooyour реестра. Замените `<acrLoginServer>` именем сервера входа реестра контейнеров Azure или именем узла общедоступного реестра.

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a>Развертывание обновленного приложения

Максимальное время работоспособности tooensure несколько экземпляров типа pod приложения hello должна быть запущена. Проверьте конфигурацию hello [kubectl получить pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) команды.

```bash
kubectl get pod
```

Выходные данные:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

Если у вас нет несколько модулей под управлением образа azure голос передней панели hello, масштабирование hello *azure голос передней панели* развертывания.


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

приложение hello tooupdate, используйте hello [kubectl набора](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) команды. Обновление `<acrLoginServer>` с hello входа сервера или имя узла в реестре контейнера.

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

Развертывание toomonitor hello, используйте hello [kubectl получить pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) команды. Развернуто приложение hello обновить ваш модулей завершаются и созданы повторно со hello новый образ контейнера.

```azurecli-interactive
kubectl get pod
```

Выходные данные:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a>Тестирование обновленного приложения

Получить hello внешний IP-адрес hello *azure голос передней панели* службы.

```azurecli-interactive
kubectl get service azure-vote-front
```

Обзор toohello IP адрес toosee hello обновленное приложение.

![Схема кластера Kubernetes в Аzure](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике обновить приложение и распространен этого обновления tooa Kubernetes кластера. были выполнены Hello следующие задачи:

> [!div class="checklist"]
> * Обновленные hello код клиентского приложения
> * Создание обновленного образа контейнера.
> * Передано tooAzure образ контейнера hello реестра контейнера
> * Развернутое приложение hello обновление приложения

Далее учебника toolearn toohello о том, как переместить toomonitor Kubernetes с Operations Management Suite.

> [!div class="nextstepaction"]
> [Мониторинг кластера Kubernetes с помощью Operations Management Suite](./container-service-tutorial-kubernetes-monitor.md)