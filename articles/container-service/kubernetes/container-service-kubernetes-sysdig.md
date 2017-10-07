---
title: "кластер Azure Kubernetes aaaMonitor - Sysdig | Документы Microsoft"
description: "Мониторинг кластера Kubernetes в Службе контейнеров Azure с помощью Sysdig."
services: container-service
documentationcenter: 
author: bburns
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
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: a27813d01ee4624b9e993f6185169ad73aeec3a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a>Мониторинг кластера Kubernetes в Службе контейнеров Azure с помощью Sysdig

## <a name="prerequisites"></a>Предварительные требования
В этом пошаговом руководстве предполагается, что вы [создали кластер Kubernetes с помощью службы контейнеров Azure](container-service-kubernetes-walkthrough.md).

Он также предполагается, что hello azure cli и kubectl установлены инструменты.

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

## <a name="sysdig"></a>Sysdig
Sysdig является компанией, предоставляющей внешний мониторинг как услугу, которая может отслеживать контейнеры в кластере Kubernetes, работающем в Azure. Для использования услуг Sysdig требуется активная учетная запись Sysdig.
Зарегистрироваться для получения учетной записи можно на [сайте компании](https://app.sysdigcloud.com).

После входа в toohello Sysdig облачные и веб-сайт, щелкните имя пользователя, и на странице приветствия вы увидите «Ключа доступа.» 

![Sysdig: ключ API](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-hello-sysdig-agents-tookubernetes"></a>Установка агентов tooKubernetes hello Sysdig
toomonitor вашей контейнеры Sysdig запускается процесс на каждом компьютере, с помощью Kubernetes `DaemonSet`.
Наборы DaemonSet являются объектами API Kubernetes, которые выполняют отдельный экземпляр контейнера на каждом компьютере.
Они идеально подходит для установки средства, такие как hello Sysdig агент мониторинга.

tooinstall hello Sysdig daemonset, следует сначала загрузить [шаблона hello](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) из sysdig. Сохраните этот файл как `sysdig-daemonset.yaml`.

В Linux и OS X можно выполнить команду:

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

В PowerShell:

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

Далее следует Измените свой ключ доступа, который получен из вашей учетной записи Sysdig tooinsert этого файла.

Наконец создайте hello DaemonSet:

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a>Просмотр данных мониторинга
После установки и запуска агентов hello должен выдавать задней tooSysdig данных.  Вернитесь к предыдущему окну toothe [sysdig мониторинга](https://app.sysdigcloud.com) и вы увидите сведения о вашей контейнерах.

Вы можете также установить панели мониторинга для Kubernetes с помощью [мастера создания панелей мониторинга](https://app.sysdigcloud.com/#/dashboards/new).
