---
title: "aaaMonitor Kubernetes Azure кластер с CoScale | Документы Microsoft"
description: "Мониторинг кластера Kubernetes в Службе контейнеров Azure с помощью CoScale"
services: container-service
documentationcenter: 
author: fryckbos
manager: 
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: f835e82d2be3afe1d85070bd0bf69649cc6dd2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a>Мониторинг кластера Kubernetes в Службе контейнеров Azure с помощью CoScale

В этой статье мы покажем, как toodeploy hello [CoScale](https://www.coscale.com/) toomonitor агента, все узлы и контейнеры в вашей Kubernetes кластера в службе контейнера Azure. Для работы с этой конфигурацией вам понадобится учетная запись с CoScale. 


## <a name="about-coscale"></a>Сведения о CoScale 

CoScale представляет собой платформу для мониторинга, собирающую метрики и события из всех контейнеров на нескольких платформах оркестрации. CoScale обеспечивает комплексный мониторинг для сред Kubernetes. Он предоставляет визуализации и анализа для всех слоев в стек hello: hello ОС, Kubernetes, Docker и приложения, работающие на контейнеры. CoScale предоставляет несколько встроенных панелей мониторинга и он имеет операторы tooallow обнаружение аномалий встроенные и проблем инфраструктуры и приложений toofind разработчикам быстро.

![Пользовательский интерфейс CoScale](./media/container-service-kubernetes-coscale/coscale.png)

Как показано в этой статье, можно установить агенты на toorun кластера Kubernetes CoScale как решение SaaS. Если требуется tookeep данных на месте, CoScale также доступна для локальной установки.


## <a name="prerequisites"></a>Предварительные требования

Необходимо сначала слишком[создать учетную запись CoScale](https://www.coscale.com/free-trial).

В этом пошаговом руководстве предполагается, что вы [создали кластер Kubernetes с помощью службы контейнеров Azure](container-service-kubernetes-walkthrough.md).

Также предполагается, что имеется hello `az` Azure CLI и `kubectl` установлены инструменты.

Можно проверить при наличии hello `az` установить, запустив средство:

```azurecli
az --version
```

Если у вас нет hello `az` средство установки приведены инструкции по [здесь](/cli/azure/install-azure-cli).

Можно проверить при наличии hello `kubectl` установить, запустив средство:

```bash
kubectl version
```

Если средство `kubectl` не установлено, выполните команду:

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-hello-coscale-agent-with-a-daemonset"></a>Установка агента CoScale hello с DaemonSet
[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) , используемые Kubernetes toorun один экземпляр контейнера на каждом узле в кластере hello.
Они идеально подходит для выполнения агентов мониторинга, например агент CoScale hello.

После входа в tooCoScale go toohello [агент страница](https://app.coscale.com/) tooinstall CoScale агенты на кластер с помощью DaemonSet. Hello CoScale пользовательского интерфейса предоставляет toocreate действия интерактивная конфигурации агента и начать наблюдение за полный Kubernetes кластера.

![Конфигурация агента CoScale](./media/container-service-kubernetes-coscale/installation.png)

агент hello toostart hello кластере, выполните команду предоставленный hello:

![Запуск агента CoScale hello](./media/container-service-kubernetes-coscale/agent_script.png)

Вот и все! После hello агенты запущены и работают, вы увидите данные в консоли hello через несколько минут. Посетите hello [агент страница](https://app.coscale.com/) toosee сводку по кластеру, выполнять дополнительные действия по настройке и в разделе панелей мониторинга, например hello **Kubernetes кластера Обзор**.

![Основные сведения о кластере Kubernetes](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

агент CoScale Hello автоматически развертываются на новых компьютерах в кластере hello. Hello агента автоматически обновляется при выпуске новой версии.


## <a name="next-steps"></a>Дальнейшие действия

В разделе hello [CoScale документации](http://docs.coscale.com/) и [блог](https://www.coscale.com/blog) для получения дополнительных сведения о CoScale мониторинг решений. 

