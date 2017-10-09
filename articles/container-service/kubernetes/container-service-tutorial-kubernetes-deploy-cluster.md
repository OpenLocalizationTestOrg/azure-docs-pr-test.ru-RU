---
title: "Учебник контейнера службы aaaAzure - развертывание кластера | Документы Microsoft"
description: "Руководство по Службе контейнеров Azure: развертывание кластера"
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
ms.openlocfilehash: c4c8cc95c88d9c2077d0322f57e5d3159e2dd0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a>Развертывание кластера Kubernetes в службе контейнеров Azure

Kubernetes предоставляет распределенную платформу для контейнерных приложений. Служба контейнеров Azure упрощает и убыстряет подготовку кластера Kubernetes для использования в рабочей среде. В этом руководстве (часть 3 из 7) развертывается кластер Kubernetes службы контейнеров Azure. В частности, рассматриваются такие шаги:

> [!div class="checklist"]
> * развертывание кластера ACS Kubernetes;
> * Установка hello Kubernetes CLI (kubectl)
> * настройка kubectl.

В последующих учебники hello Azure голос приложение развертывания кластера toohello, масштабирования, обновления и Operations Management Suite является настроенным toomonitor hello Kubernetes кластера.

## <a name="before-you-begin"></a>Перед началом работы

В предыдущих учебниках образ контейнера был создан и загружен экземпляр tooan реестра контейнера Azure. Если вы не были выполнены следующие действия и хотите toofollow вдоль, возвращают слишком[учебник 1 – Создание образов контейнеров](./container-service-tutorial-kubernetes-prepare-app.md).

## <a name="create-kubernetes-cluster"></a>Создание кластера Kubernetes

В hello [с предыдущим учебником](./container-service-tutorial-kubernetes-prepare-acr.md), группу ресурсов с именем *myResourceGroup* был создан. Если вы этого не сделали, создайте эту группу ресурсов сейчас.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

Создание кластера Kubernetes в контейнере службы Azure с hello [создать acs az](/cli/azure/acs#create) команды. 

Hello следующий пример создает кластер с именем *myK8sCluster* с Linux в один главный узел и три узла агента Linux.

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

Через несколько минут выполнения команды hello и в формате json возвращает сведения о развертывании hello ACS.

## <a name="install-hello-kubectl-cli"></a>Установка hello kubectl CLI

tooconnect toohello Kubernetes кластера с клиентского компьютера, используйте [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), клиент командной строки Kubernetes hello. 

Если вы используете Azure CloudShell, установка `kubectl` уже выполнена. Если требуется, чтобы tooinstall его локально, использовать hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) команды.

Если выполняется macOS или Linux, может потребоваться toorun с sudo. В Windows убедитесь, что оболочка запущена от имени администратора.

```azurecli-interactive 
az acs kubernetes install-cli 
```

В Windows, — установка по умолчанию hello *c:\program files (x86)\kubectl.exe*. Может потребоваться tooadd этот путь к файлу toohello Windows. 

## <a name="connect-with-kubectl"></a>Подключение с помощью kubectl

tooconfigure `kubectl` tooconnect tooyour Kubernetes кластера, запустите hello [az kubernetes get-учетные данные acs](/cli/azure/acs/kubernetes#get-credentials) команды.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

tooverify hello подключения tooyour кластера, запустите hello [kubectl получения узлов](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) команды.

```azurecli-interactive
kubectl get nodes
```

Выходные данные:

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

По завершении руководства вы получите кластер ACS Kubernetes, готовый к обработке рабочих нагрузок. В последующих учебники приложение несколькими контейнера — развернутой toothis кластер, горизонтального масштабирования, обновления и отслеживаться.

## <a name="next-steps"></a>Дальнейшие действия

В этом руководстве был развернут кластер Kubernetes Службы контейнеров Azure. Привет, следующие шаги были выполнены:

> [!div class="checklist"]
> * развертывание кластера ACS Kubernetes;
> * Установленные hello Kubernetes CLI (kubectl)
> * настройка kubectl.

Переместить следующий учебник toolearn toohello о запуске приложения на кластере hello.

> [!div class="nextstepaction"]
> [Запуск приложений в Kubernetes](./container-service-tutorial-kubernetes-deploy-application.md)
