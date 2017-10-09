---
title: "кластер aaaMonitor Azure Kubernetes - операции управления | Документы Microsoft"
description: "Мониторинг кластера Kubernetes в Службе контейнеров Azure с помощью Microsoft Operations Management Suite"
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
ms.openlocfilehash: 7474ee1571134ffe43ff8e4041cf5a64f5635bb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a>Мониторинг кластера Службы контейнеров Azure с помощью Microsoft Operations Management Suite (OMS)

## <a name="prerequisites"></a>Предварительные требования
В этом пошаговом руководстве предполагается, что вы [создали кластер Kubernetes с помощью службы контейнеров Azure](container-service-kubernetes-walkthrough.md).

Также предполагается, что имеется hello `az` Azure cli и `kubectl` установлены инструменты.

Можно проверить при наличии hello `az` установить, запустив средство:

```console
$ az --version
```

Если у вас нет hello `az` средство установки приведены инструкции по [здесь](https://github.com/azure/azure-cli#installation).  
Кроме того, можно использовать [оболочки облако Azure](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), имеющий hello `az` Azure cli и `kubectl` средства уже установлен автоматически.  

Можно проверить при наличии hello `kubectl` установить, запустив средство:

```console
$ kubectl version
```

Если средство `kubectl` не установлено, выполните команду:
```console
$ az acs kubernetes install-cli
```

tootest при наличии kubernetes ключи, установленные в средстве kubectl можно запустить:
```console
$ kubectl get nodes
```

Если hello выше команда ошибок, tooinstall kubernetes кластера ключи требуются в средство kubectl. Это можно сделать с помощью hello следующую команду:
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a>Мониторинг контейнеров с помощью Operations Management Suite (OMS)

Microsoft Operations Management (OMS) — это облачное решение Майкрософт для управления ИТ-средой, которое помогает управлять локальной и облачной инфраструктурой и защищать ее. Решение контейнер — это решение в аналитику журнала OMS, служащей для просмотра данных инвентаризации контейнера hello, производительности и журналов в одном месте. Аудит, устранение неполадок контейнеры путем просмотра журналов hello в центральном расположении и найти шумный использование лишние контейнер на узле.

![](media/container-service-monitoring-oms/image1.png)

Дополнительные сведения о решении контейнера можно найти toothe [анализа журналов контейнера решение](../../log-analytics/log-analytics-containers.md).

## <a name="installing-oms-on-kubernetes"></a>Установка OMS в Kubernetes

### <a name="obtain-your-workspace-id-and-key"></a>Получение идентификатора и ключа рабочей области
Hello службы toohello tootalk агента OMS должен toobe настроены идентификатор рабочей области и ключ рабочей области. идентификатор рабочей области tooget hello и toocreate OMS ключа учетной записи в <https://mms.microsoft.com>. Выполните шаги hello toocreate учетную запись. После завершения создания учетной записи hello, вам потребуется tooobtain идентификатор и ключ, щелкнув **параметры**, затем **подключенные источники**, а затем **серверы Linux**, как показано ниже.

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-hello-oms-agent-using-a-daemonset"></a>Установка агента OMS hello, с помощью DaemonSet
DaemonSets используются Kubernetes toorun один экземпляр контейнера на каждом узле в кластере hello.
Они идеально подходят для выполнения агентов мониторинга.

Вот hello [DaemonSet YAML файл](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes). Сохраните файл с именем файла tooa `oms-daemonset.yaml` и замените значения заполнителя hello `WSID` и `KEY` с идентификатор рабочей области и ключ в файле hello.

После добавления идентификатор рабочей области и ключа toohello DaemonSet конфигурации, можно установить агент OMS hello в кластере с hello `kubectl` средство командной строки:

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-hello-oms-agent-using-a-kubernetes-secret"></a>Установка агента OMS hello, с помощью Kubernetes секрета
tooprotect свой идентификатор рабочей области OMS и ключ, можно использовать как часть файла DaemonSet YAML Kubernetes секрет.

 - Скопируйте сценарий hello, файл шаблона секретный и hello DaemonSet YAML файл (из [репозитория](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) и убедитесь, что они находятся на hello один каталог. 
      - Сценарий создания секретов — secret-gen.sh.
      - Шаблон секретов — secret-template.yaml.
   - YAML-файл DaemonSet — omsagent-ds-secrets.yaml.
 - Запустите сценарий hello. Hello скрипт будет запрашивать hello идентификатор рабочей области OMS и первичный ключ. Вставьте, и hello сценарий создаст файл секретный yaml, чтобы можно было запустить.   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - Создайте pod hello секретные данные, выполнив следующие hello:``` kubectl create -f omsagentsecret.yaml ```
 
   - toocheck hello следующей: 

   ``` 
   root@ubuntu16-13db:~# kubectl get secrets
   NAME                  TYPE                                  DATA      AGE
   default-token-gvl91   kubernetes.io/service-account-token   3         50d
   omsagent-secret       Opaque                                2         1d
   root@ubuntu16-13db:~# kubectl describe secrets omsagent-secret
   Name:           omsagent-secret
   Namespace:      default
   Labels:         <none>
   Annotations:    <none>

   Type:   Opaque

   Data
   ====
   WSID:   36 bytes
   KEY:    88 bytes 
   ```
 
  - Создание свой набор daemon-set omsagent, выполнив команду ``` kubectl create -f omsagent-ds-secrets.yaml ```

### <a name="conclusion"></a>Заключение
Вот и все! Через несколько минут должно быть возможности toosee данными, поступающими tooyour мониторинга OMS.
