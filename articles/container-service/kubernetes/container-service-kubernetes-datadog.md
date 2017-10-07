---
title: "aaaMonitor Azure Kubernetes кластер с Datadog | Документы Microsoft"
description: "Мониторинг кластера Kubernetes в Службе контейнеров Azure с помощью DataDog."
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: bccd8b59a048e0f791172fcfc4eeba6370dafcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a>Мониторинг кластера службы контейнеров Azure с помощью Datadog

## <a name="prerequisites"></a>Предварительные требования
В этом пошаговом руководстве предполагается, что вы [создали кластер Kubernetes с помощью службы контейнеров Azure](container-service-kubernetes-walkthrough.md).

Также предполагается, что имеется hello `az` Azure cli и `kubectl` установлены инструменты.

Можно проверить при наличии hello `az` установить, запустив средство:

```console
$ az --version
```

Если у вас нет hello `az` средство установки приведены инструкции по [здесь](https://github.com/azure/azure-cli#installation).

Можно проверить при наличии hello `kubectl` установить, запустив средство:

```console
$ kubectl version
```

Если средство `kubectl` не установлено, выполните команду:

```console
$ az acs kubernetes install-cli
```

## <a name="datadog"></a>Datadog
Datadog представляет собой службу мониторинга, которая собирает данные мониторинга из контейнеров в кластере службы контейнеров Azure. Datadog имеет панель мониторинга интеграции с Docker, в которой вы можете увидеть некоторые метрики своих контейнеров. Метрики контейнеров собраны в несколько групп: ЦП, память, сеть и ввод-вывод. Datadog разделяет метрики по контейнерам и образам.

Необходимо сначала слишком[создать учетную запись](https://www.datadoghq.com/lpg/)

## <a name="installing-hello-datadog-agent-with-a-daemonset"></a>Установка агента Datadog hello с DaemonSet
DaemonSets используются Kubernetes toorun один экземпляр контейнера на каждом узле в кластере hello.
Они идеально подходят для выполнения агентов мониторинга.

После входа в Datadog, можно выполнить hello [инструкции Datadog](https://app.datadoghq.com/account/settings#agent/kubernetes) tooinstall Datadog агенты на кластер с помощью DaemonSet.

## <a name="conclusion"></a>Заключение
Вот и все! Когда агенты hello функционируют, и под управлением, вы увидите данные в консоли hello через несколько минут. Посетите hello интеграции [kubernetes мониторинга](https://app.datadoghq.com/screen/integration/kubernetes) toosee Сводка кластера.
