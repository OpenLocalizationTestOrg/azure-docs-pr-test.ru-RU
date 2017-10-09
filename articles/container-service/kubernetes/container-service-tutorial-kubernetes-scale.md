---
title: "Учебник контейнера службы aaaAzure - масштаб приложения | Документы Microsoft"
description: "Руководство по Службе контейнеров Azure: масштабирование приложения"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Kubernetes, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 29571eef0fd91bd6b40f00d8c018539f320179bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a>Масштабирование pod и инфраструктуры Kubernetes

Если вы смотрел hello учебники, имеется действующее Kubernetes кластера в службе контейнера Azure, и вы развернули приложение Azure голосования hello. 

В этом учебнике, часть 5, 7, горизонтальное масштабирование hello модулей в приложение hello и повторите pod автоматического масштабирования. Вы также узнаете, как количество hello tooscale toochange узлы агента ВМ Azure hello кластера емкость для размещения рабочих нагрузок. Вам предстоят следующие задачи:

> [!div class="checklist"]
> * масштабирование pod Kubernetes вручную;
> * Настройка модулей автомасштабирования выполнение внешнего интерфейса приложения hello
> * Масштабирование узлы Azure агентов Kubernetes hello

В последующих учебники hello Azure голос приложение обновляется, и Operations Management Suite настроили кластер Kubernetes toomonitor hello.

## <a name="before-you-begin"></a>Перед началом работы

В предыдущих учебниках приложение было упаковано в образ контейнера, tooAzure реестра контейнера и создания кластера Kubernetes загружены этот образ. приложение Hello затем была запущена на кластере Kubernetes hello. Если вы не были выполнены следующие действия и хотите toofollow вдоль, возвращают toohello [учебник 1 – Создание образов контейнеров](./container-service-tutorial-kubernetes-prepare-app.md). 

Для этого руководства как минимум необходим кластер Kubernetes с выполняющимся приложением.

## <a name="manually-scale-pods"></a>Масштабирование pod вручную

До сих hello Azure голос переднего плана и экземпляр Redis были развернуты, каждый с одной реплики. tooverify, запустите hello [kubectl получить](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) команды.

```azurecli-interactive
kubectl get pods
```

Выходные данные:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

Вручную измените hello количество модулей в hello `azure-vote-front` развертывания с помощью hello [kubectl шкалы](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) команды. В этом примере увеличивается число too5 hello.

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

Запустите [kubectl получить модулей](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify, Kubernetes создает hello модулей. Прошествии минуты под управлением hello дополнительных модулей:

```azurecli-interactive
kubectl get pods
```

Выходные данные:

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a>Автомасштабирование pod

Поддерживает Kubernetes [автоматическое масштабирование горизонтальной pod](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) tooadjust hello число модулей в развертывании в зависимости от загрузки ЦП или другой выбор метрик. 

toouse hello autoscaler, ваш модулей должен иметь ЦП запросы и заданных пределов. В hello `azure-vote-front` развертывания, Процессор запросов 0,25 контейнера переднего плана, ограничение на число 0,5 hello ЦП. Параметры Hello иметь вид:

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

Hello следующий пример использует hello [автомасштабирования kubectl](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) команды tooautoscale hello число модулей в hello `azure-vote-front` развертывания. Здесь Если загрузка ЦП превышает 50%, hello autoscaler увеличивает hello модулей tooa более 10.


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

состояние hello toosee autoscaler hello, запустите hello следующую команду:

```azurecli-interactive
kubectl get hpa
```

Выходные данные:

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

Через несколько минут с минимальной нагрузкой на приложение hello Azure голос число hello pod реплик, которые автоматически уменьшается too3.

## <a name="scale-hello-agents"></a>Агенты hello шкалы

Если вы создали Kubernetes кластер с помощью команды по умолчанию в предыдущем учебнике hello, он имеет три узла агента. При планировании большее или меньшее количество рабочих нагрузок контейнера в кластере hello число агентов можно настроить вручную. Используйте hello [масштабировать acs az](/cli/azure/acs#scale) команду и укажите номер hello агентов hello `--new-agent-count` параметра.

Hello следующем примере увеличивается число hello агента too4 узлов в кластере Kubernetes hello с именем *myK8sCluster*. Команда Hello занимает несколько минут toocomplete.

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

Hello выходные данные команды отображаются номер hello агента узлы в значение hello `agentPoolProfiles:count`:

```azurecli
{
  "agentPoolProfiles": [
    {
      "count": 4,
      "dnsPrefix": "myK8SCluster-myK8SCluster-e44f25-k8s-agents",
      "fqdn": "",
      "name": "agentpools",
      "vmSize": "Standard_D2_v2"
    }
  ],
...

```

## <a name="next-steps"></a>Дальнейшие действия

В этом руководстве вы использовали различные возможности масштабирования кластера Kubernetes. Были рассмотрены такие задачи:

> [!div class="checklist"]
> * масштабирование pod Kubernetes вручную;
> * Настройка модулей автомасштабирования выполнение внешнего интерфейса приложения hello
> * Масштабирование узлы Azure агентов Kubernetes hello

Переместить следующий учебник toolearn toohello об обновлении приложения в Kubernetes.

> [!div class="nextstepaction"]
> [Обновление приложения в Kubernetes](./container-service-tutorial-kubernetes-app-update.md)

