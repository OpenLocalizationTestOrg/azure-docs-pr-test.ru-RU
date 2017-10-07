---
title: "контейнеры aaaDeploy с Helm в Azure Kubernetes | Документы Microsoft"
description: "Используйте hello Helm упаковки средство toodeploy контейнеры в кластере Kubernetes в контейнере службы Azure"
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/10/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: c7bd780afe00084ebe4e3a14873e1e340a29d144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-helm-toodeploy-containers-on-a-kubernetes-cluster"></a>Использование контейнеров toodeploy Helm в кластере Kubernetes 

[Helm](https://github.com/kubernetes/helm/) — это средство упаковки с открытым исходным кодом, которое поможет вам установить и управление жизненным циклом hello Kubernetes приложений. Аналогичные tooLinux пакета диспетчерами, например Apt get и Yum, Helm — используется toomanage Kubernetes диаграммы, которые являются пакетами предварительно настроенных Kubernetes ресурсов. В этой статье показано, как toowork с Helm на кластере Kubernetes развертывание в службе контейнера Azure.

Helm состоит из двух компонентов: 
* Hello **Helm CLI** клиента, который работает на компьютере, локально или в облаке hello  

* **Tiller** — это сервер, работающий на кластере Kubernetes hello и управление жизненным циклом приложений Kubernetes hello 
 
## <a name="prerequisites"></a>Предварительные требования

* [Создание кластера Kubernetes](container-service-kubernetes-walkthrough.md) в Службе контейнеров Azure

* [Установка и настройка`kubectl`](../container-service-connect.md) на локальном компьютере

* [Установка Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) на локальном компьютере

## <a name="helm-basics"></a>Основы использования Helm 

tooview сведения о hello Kubernetes кластера, установке Tiller и развертывания приложений введите hello следующую команду:

```bash
kubectl cluster-info 
```
![kubectl cluster-info](./media/container-service-kubernetes-helm/clusterinfo.png)
 
После установки Helm установки Tiller в кластере Kubernetes введите hello следующую команду:

```bash
helm init --upgrade
```
После успешного завершения, вывод имеет hello следующим образом:

![Установка Tiller](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
tooview все hello Helm диаграммы доступен в репозитории hello, тип hello следующих команд:

```bash 
helm search 
```

Вывод hello следующим образом:

![Поиск Helm](./media/container-service-kubernetes-helm/helm-search.png)
 
tooupdate hello диаграммы tooget hello последние версии, введите следующую команду:

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a>Развертывание чарта входящего контроллера Nginx 
 
toodeploy диаграммы контроллера входящих Nginx, введите одну команду:

```bash
helm install stable/nginx-ingress 
```
![Развертывание входящего контроллера](./media/container-service-kubernetes-helm/nginx-ingress.png)

Если ввести `kubectl get svc` tooview всех служб, выполняющихся на кластере hello, вы видите, что IP-адрес назначается toohello входящих контроллера. (Hello назначения во время выполнения, вы видите `<pending>`. Она принимает ряд toocomplete мин.) 

После назначения IP-адрес hello перейдите toohello значение hello внешнего IP адрес toosee hello Nginx серверной под управлением. 
 
![Входящий IP-адрес](./media/container-service-kubernetes-helm/ingress-ip-address.png)


toosee списка установлены в кластере типа диаграмм:

```bash
helm list 
```

Можно сократить команда hello слишком`helm ls`.
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a>Развертывание клиента и чарта MariaDB

Теперь можно разверните диаграмму MariaDB и tooconnect toohello MariaDB клиентской базе данных.

Диаграмма MariaDB hello toodeploy, тип hello следующую команду:

```bash
helm install --name v1 stable/mariadb
```

здесь `--name` — тег, используемый для выпусков.

> [!TIP]
> Если происходит сбой развертывания hello, запустите `helm repo update` и повторите попытку.
>
 
 
tooview развернуть все hello диаграммы кластера, тип:

```bash 
helm list
```
 
tooview всех развертываний, работающих в кластере, введите следующую команду:

```bash
kubectl get deployments 
``` 
 
 
Наконец toorun клиент hello tooaccess pod, введите следующую команду:

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
Клиент toohello tooconnect, тип hello следующую команду, заменив `v1-mariadb` с именем hello развертывания:

```bash
sudo mysql –h v1-mariadb
```
 
 
Теперь можно использовать обычные БД toocreate команды SQL, таблицы и т. д. Например, `Create DATABASE testdb1;` создает пустую базу данных. 
 
 
 
## <a name="next-steps"></a>Дальнейшие действия

* Дополнительные сведения об управлении Kubernetes диаграммы см. в разделе hello [Helm документации](https://github.com/kubernetes/helm/blob/master/docs/index.md). 

