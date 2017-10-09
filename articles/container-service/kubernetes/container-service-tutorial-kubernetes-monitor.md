---
title: "Учебник контейнера службы aaaAzure - монитор Kubernetes | Документы Microsoft"
description: "Руководство по службе контейнеров Azure — мониторинг Kubernetes с помощью Microsoft Operations Management Suite (OMS)"
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
ms.openlocfilehash: 54fa789453768529deaf25d7575e5b21d0e41882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a>Мониторинг кластера Kubernetes с помощью Operations Management Suite

Мониторинг кластера Kubernetes и контейнеров крайне важен, особенно в том случае, если вы управляете масштабируемым рабочим кластером с несколькими приложениями. 

Вы можете воспользоваться преимуществами нескольких решений для мониторинга Kubernetes от корпорации Майкрософт или других поставщиков. В этом учебнике отслеживать Kubernetes кластера с помощью решения контейнеры hello в [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), Облачное решение управления ИТ корпорации Майкрософт. (hello решений OMS контейнеры находится в предварительной версии).

В этом учебнике, часть 7 семь, приведены hello следующие задачи:

> [!div class="checklist"]
> * Получение параметров рабочей области OMS.
> * Настроить агенты OMS на узлах Kubernetes hello
> * Доступ к данным мониторинга на портале OMS hello или портал Azure

## <a name="before-you-begin"></a>Перед началом работы

В предыдущих учебниках приложение было упаковано в образах контейнеров, эти образы, отправленном tooAzure реестра контейнера и создан Kubernetes кластера. Если вы не были выполнены следующие действия и хотите toofollow вдоль, возвращают слишком[учебник 1 – Создание образов контейнеров](./container-service-tutorial-kubernetes-prepare-app.md). 

Для этого руководства требуется по крайней мере кластер Kubernetes с узлами агентов Linux и учетная запись OMS. При необходимости зарегистрируйтесь для получения [бесплатной пробной версии OMS](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).

## <a name="get-workspace-settings"></a>Получение параметров рабочей области

При доступе к hello [портал OMS](https://mms.microsoft.com), перейдите в слишком**параметры** > **подключенные источники** > **серверы Linux**. Здесь можно найти hello *идентификатор рабочей области* и основных или дополнительных *ключ рабочей области*. Запишите эти значения, которые необходимо tooset копирование агенты OMS в кластере hello.

## <a name="set-up-oms-agents"></a>Настройка агентов OMS

Вот tooset файл YAML копирование OMS агенты на узлах кластера hello Linux. Он создает [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) Kubernetes, который запускает идентичный модуль на каждом узле кластера. Hello ресурсов DaemonSet идеально подходит для развертывания агента мониторинга. 

Сохраните следующий текстовый файл tooa с именем hello `oms-daemonset.yaml`и замените значения заполнителей hello для *myWorkspaceID* и *myWorkspaceKey* с идентификатор рабочей области OMS и ключа. (В рабочей среде можно закодировать эти значения в виде секретов.)

```YAML
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
 name: omsagent
spec:
 template:
  metadata:
   labels:
    app: omsagent
    agentVersion: v1.3.4-127
    dockerProviderVersion: 10.0.0-25
  spec:
   containers:
     - name: omsagent 
       image: "microsoft/oms"
       imagePullPolicy: Always
       env:
       - name: WSID
         value: myWorkspaceID
       - name: KEY 
         value: myWorkspaceKey
       - name: DOMAIN
         value: opinsights.azure.com
       securityContext:
         privileged: true
       ports:
       - containerPort: 25225
         protocol: TCP 
       - containerPort: 25224
         protocol: UDP
       volumeMounts:
        - mountPath: /var/run/docker.sock
          name: docker-sock
        - mountPath: /var/log 
          name: host-log
       livenessProbe:
        exec:
         command:
         - /bin/bash
         - -c
         - ps -ef | grep omsagent | grep -v "grep"
        initialDelaySeconds: 60
        periodSeconds: 60
   volumes:
    - name: docker-sock 
      hostPath:
       path: /var/run/docker.sock
    - name: host-log
      hostPath:
       path: /var/log
```

Создайте hello DaemonSet с hello следующую команду:

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

выполните для этого hello создания DaemonSet toosee:

```azurecli-interactive
kubectl get daemonset
```

Выходные данные выглядят аналогично toohello следующее:

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

После запуска агентов hello он занимает несколько минут для OMS tooingest и обрабатывающие данные hello.

## <a name="access-monitoring-data"></a>Доступ к данным мониторинга

Просматривать и анализировать данные мониторинга с hello контейнера OMS hello [решения контейнера](../../log-analytics/log-analytics-containers.md) в портал OMS hello или hello портал Azure. 

tooinstall hello контейнера решения с помощью hello [портал OMS](https://mms.microsoft.com), перейдите в слишком**коллекции решений**. Затем добавьте **решение "Контейнер"**. Кроме того, добавить решение контейнеры hello из hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).

На портале OMS hello, искать **контейнеры** сводки плитки на панели мониторинга OMS hello. Щелкните плитку hello Дополнительные сведения, включая: события контейнера, ошибки, состояние, изображение инвентаризации и использования ЦП и памяти. Более детализированные сведения можно получить, щелкнув строку на одной из плиток или выполнив [поиск по журналам](../../log-analytics/log-analytics-log-searches.md).

![Панель мониторинга "Контейнеры" на портале OMS](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

Аналогичным образом в hello портал Azure, перейдите слишком**анализа журналов** и выберите имя рабочей области. toosee hello **контейнеры** Плитка сводки, щелкните **решения** > **контейнеры**. сведения о toosee, щелкните плитку hello.

В разделе hello [документации Azure Log Analytics](../../log-analytics/index.md) подробное руководство по запросу и анализ данных наблюдения.

## <a name="next-steps"></a>Дальнейшие действия

В этом руководстве вы выполнили мониторинг кластера Kubernetes с помощью OMS, в частности такие задачи:

> [!div class="checklist"]
> * Получение параметров рабочей области OMS.
> * Настроить агенты OMS на узлах Kubernetes hello
> * Доступ к данным мониторинга на портале OMS hello или портал Azure


Выполните этот toosee ссылку готовые примеры скриптов для службы контейнеров.

> [!div class="nextstepaction"]
> [Примеры Azure CLI для службы контейнеров Azure](cli-samples.md)
