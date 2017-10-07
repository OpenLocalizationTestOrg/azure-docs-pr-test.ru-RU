---
title: "aaaQuickstart - Azure Kubernetes кластера для Windows | Документы Microsoft"
description: "Быстро Узнайте toocreate Kubernetes кластера для контейнеров Windows в службе контейнера Azure с hello Azure CLI."
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 85fe65a46ae8c78797e8a8a097c2a37f06329335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a>Кластер Azure Kubernetes для Windows | Документация Майкрософт

Hello Azure CLI — используется toocreate и управления ресурсами Azure hello командной строке или в сценариях. В этом руководстве рассматривается использование hello Azure CLI toodeploy [Kubernetes](https://kubernetes.io/docs/home/) кластер в [контейнера службы Azure](../container-service-intro.md). После развертывания кластера hello tooit соединены hello Kubernetes `kubectl` средство командной строки и развертывание первого контейнера Windows.

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, краткого руководства требуется управлением hello Azure CLI версия 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

> [!NOTE]
> Поддержка контейнеров Windows для Kubernetes в Службе контейнеров Azure реализована в режиме предварительной версии. 
>

## <a name="create-a-resource-group"></a>Создание группы ресурсов

Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды. Группа ресурсов Azure — это логическая группа, в которой выполняется развертывание и администрирование ресурсов Azure. 

Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a>Создание кластера Kubernetes
Создание кластера Kubernetes в контейнере службы Azure с hello [создать acs az](/cli/azure/acs#create) команды. 

Hello следующий пример создает кластер с именем *myK8sCluster* с Linux в один главный узел с двумя узлами агент Windows. В этом примере создается SSH master Linux toohello tooconnect необходимые ключи. В этом примере используется *azureuser* имени пользователя с правами администратора и *myPassword12* hello паролем на узлах Windows hello. Обновите эти значения toosomething соответствующие tooyour среду. 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

Через несколько минут завершения команды hello и отображаются сведения о развертывании.

## <a name="install-kubectl"></a>Установка kubectl

tooconnect toohello Kubernetes кластера с клиентского компьютера, используйте [ `kubectl` ](https://kubernetes.io/docs/user-guide/kubectl/), клиент командной строки Kubernetes hello. 

Если вы используете Azure CloudShell, установка `kubectl` уже выполнена. Если требуется, чтобы tooinstall его локально, можно использовать hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) команды.

Здравствуйте, следующий пример устанавливает Azure CLI `kubectl` tooyour системы. В Windows запустите следующую команду от имени администратора:

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a>Подключение с помощью kubectl

tooconfigure `kubectl` tooconnect tooyour Kubernetes кластера, запустите hello [az kubernetes get-учетные данные acs](/cli/azure/acs/kubernetes#get-credentials) команды. Hello следующем примере загружаются hello конфигурации кластера для кластера Kubernetes.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

tooverify hello подключения кластера tooyour с компьютера, попробуйте запустить:

```azurecli-interactive
kubectl get nodes
```

`kubectl`список узлов hello master и агента.

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a>Развертывание контейнера Windows IIS

Можно запустить контейнер Docker внутри группы контейнеров Kubernetes (объект *pod*), которая содержит один или несколько контейнеров. 

Этот простой пример использует toospecify файл JSON контейнер Microsoft Internet Information Server (IIS), а затем создает с помощью hello pod hello `kubctl apply` команды. 

Создание локального файла с именем `iis.json` и копирования hello после текста. Этот файл сообщением о Kubernetes toorun IIS в Windows Server 2016 Nano Server с помощью образа из общего контейнера [Docker Hub](https://hub.docker.com/r/nanoserver/iis/). контейнер Hello использует порт 80, но изначально доступен только в рамках сети кластера hello.

 ```JSON
 {
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "iis",
    "labels": {
      "name": "iis"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "iis",
        "image": "nanoserver/iis",
        "ports": [
          {
          "containerPort": 80
          }
        ]
      }
    ],
    "nodeSelector": {
     "beta.kubernetes.io/os": "windows"
     }
   }
 }
 ```

toostart hello pod, тип:
  
```azurecli-interactive
kubectl apply -f iis.json
```  

Развертывание tootrack hello, тип:
  
```azurecli-interactive
kubectl get pods
```

При развертывании hello pod, находится в состоянии hello `ContainerCreating`. Он может занять несколько минут для hello tooenter контейнера hello `Running` состояния.

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-hello-iis-welcome-page"></a>Представление hello страницу приветствия IIS

tooexpose hello world toohello pod с общедоступный IP-адрес, тип hello следующую команду:

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

С помощью этой команды Kubernetes создает службу и [правило подсистемы балансировки нагрузки Azure](container-service-kubernetes-load-balancing.md) с общедоступный IP-адрес для службы hello. 

Выполните следующие команды toosee hello состояние службы hello hello.

```azurecli-interactive
kubectl get svc
```

Изначально hello IP-адрес выглядит как `pending`. Через несколько минут hello внешний IP-адрес hello `iis` pod имеет значение:
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

Можно использовать веб-браузере choice toosee hello по умолчанию службы IIS страницу приветствия во внешний IP-адрес hello:

![Изображение просмотра tooIIS](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a>Удаление кластера
Когда кластер hello не нужны, можно использовать hello [удаление группы az](/cli/azure/group#delete) команд группы ресурсов tooremove hello, контейнер службы и все связанные ресурсы.

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a>Дальнейшие действия

В этом кратком руководстве описано, как развертывать подключенный к `kubectl` кластер Kubernetes и группу контейнеров с контейнером IIS. toolearn Дополнительные сведения о службе Azure контейнера, продолжить работу с учебником Kubernetes toohello.

> [!div class="nextstepaction"]
> [Create container images to be used with Azure Container Service](container-service-tutorial-kubernetes-prepare-app.md) (Создание образов контейнеров для использования со Службой контейнеров Azure)
