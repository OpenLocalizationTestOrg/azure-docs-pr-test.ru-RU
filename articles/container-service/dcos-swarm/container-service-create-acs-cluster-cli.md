---
title: "aaaDeploy кластер контейнера Docker - Azure CLI | Документы Microsoft"
description: "Развертывание решений Kubernetes, DC/OS или Docker Swarm в службе контейнеров Azure с помощью Azure CLI 2.0"
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: azurecli
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: saudas
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: cdfa4ce69de343dcc7070bc2c58b5132c4062084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-cli-20"></a>Развертывания с помощью Azure CLI 2.0 hello решения по размещению контейнера Docker

Используйте hello `az acs` команды в toocreate hello Azure CLI 2.0 кластеров и управление ими в службе контейнера Azure. Можно также развернуть кластер контейнера службы Azure с помощью hello [портал Azure](container-service-deployment.md) или hello API-интерфейсы службы контейнера Azure.

Для получения справки по `az acs` команд, передайте hello `-h` параметр tooany команды. Например, `az acs create -h`.



## <a name="prerequisites"></a>Предварительные требования
toocreate кластера контейнера службы Azure с помощью hello Azure CLI 2.0, необходимо:
* учетная запись Azure ([получите бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/));
* установки и настройки hello [Azure CLI 2.0](/cli/azure/install-az-cli2)

## <a name="get-started"></a>Начало работы 
### <a name="log-in-tooyour-account"></a>Войдите в учетную запись tooyour
```azurecli
az login 
```

Выполните hello toolog запросы в интерактивном режиме. Другие методы toolog в, в разделе [Приступая к работе с Azure CLI 2.0](/cli/azure/get-started-with-az-cli2).

### <a name="set-your-azure-subscription"></a>Настройка подписки Azure

Если у вас есть несколько подписок Azure, установите подписку по умолчанию hello. Например:

```
az account set --subscription "f66xxxxx-xxxx-xxxx-xxx-zgxxxx33cha5"
```


### <a name="create-a-resource-group"></a>Создание группы ресурсов
Мы рекомендуем создать группу ресурсов для каждого кластера. Укажите регион Azure, в котором [доступна](https://azure.microsoft.com/en-us/regions/services/) Служба контейнеров Azure. Например:

```azurecli
az group create -n acsrg1 -l "westus"
```
Выходные данные выглядят аналогично toohello следующее:

![Создание группы ресурсов](./media/container-service-create-acs-cluster-cli/rg-create.png)


## <a name="create-an-azure-container-service-cluster"></a>Создание кластера Службы контейнеров Azure

toocreate кластер, используйте `az acs create`.
Имя кластера hello и hello hello группы ресурсов, созданных в предыдущем шаге hello — обязательные параметры. 

Другие входные данные, установите toodefault значения (см. следующий экран приветствия) Если не переопределены с помощью их соответствующими параметрами. Например по умолчанию tooDC/OS задается hello orchestrator. И если не указано, создается на имя кластера hello основе префикса имени DNS.

![Использование az acs create](./media/container-service-create-acs-cluster-cli/create-help.png)


### <a name="quick-acs-create-using-defaults"></a>Быстрое выполнение `acs create` с использованием значений по умолчанию
При наличии файла открытого ключа SSH-RSA `id_rsa.pub` в расположении по умолчанию hello (или создана для [OS X и Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) или [Windows](../../virtual-machines/linux/ssh-from-windows.md)), используйте команду hello следующим образом:

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789
```
Если у вас нет открытого ключа SSH, используйте вторую команду. Эта команда с hello `--generate-ssh-keys` коммутатора создаст ее.

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789 --generate-ssh-keys
```

После выполнения команды hello, подождите около 10 минут для создания toobe кластера hello. выходные данные команды Hello включает полные доменные имена (FQDN) главного hello и узлы агентов и SSH команда tooconnect toohello первый образец. Ниже приведены сокращенные выходные данные.

![Изображение создания ACS](./media/container-service-create-acs-cluster-cli/cluster-create.png)

> [!TIP]
> Hello [Пошаговое руководство Kubernetes](../kubernetes/container-service-kubernetes-walkthrough.md) показано, как toouse `az acs create` с toocreate значения по умолчанию Kubernetes кластера.
>

## <a name="manage-acs-clusters"></a>Управление кластерами ACS

Использование дополнительных `az acs` команды toomanage кластера. Ниже приведены некоторые примеры.

### <a name="list-clusters-under-a-subscription"></a>Получение списка кластеров в рамках подписки

```azurecli
az acs list --output table
```

### <a name="list-clusters-in-a-resource-group"></a>Получение списка кластеров в группе ресурсов

```azurecli
az acs list -g acsrg1 --output table
```

![acs list](./media/container-service-create-acs-cluster-cli/acs-list.png)


### <a name="display-details-of-a-container-service-cluster"></a>Отображение сведений о кластере службы контейнеров

```azurecli
az acs show -g acsrg1 -n acs-cluster --output list
```

![acs show](./media/container-service-create-acs-cluster-cli/acs-show.png)


### <a name="scale-hello-cluster"></a>Масштаб hello кластера
Увеличение и уменьшение масштабирования узлов агента разрешено. Здравствуйте, параметр `new-agent-count` hello новое число агентов в кластере hello ACS.

```azurecli
az acs scale -g acsrg1 -n acs-cluster --new-agent-count 4
```

![acs scale](./media/container-service-create-acs-cluster-cli/acs-scale.png)

## <a name="delete-a-container-service-cluster"></a>Удаление кластера службы контейнеров
```azurecli
az acs delete -g acsrg1 -n acs-cluster 
```
Эта команда удаляет все ресурсы (сеть и хранилище), созданные при создании контейнера службы hello. toodelete все ресурсы легко, рекомендуется развертывание каждого кластера в группу различных ресурсов. Затем удалите группу ресурсов hello при hello кластер больше не требуется.

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда у вас есть работающий кластер, выберите ссылки ниже, чтобы узнать о возможностях подключения и управления.

* [Подключите кластер tooan контейнера службы Azure](../container-service-connect.md)
* [Работа со службой контейнеров Azure и DC/OS](container-service-mesos-marathon-rest.md)
* [Работа со службой контейнеров Azure и Docker Swarm](container-service-docker-swarm.md)
* [Работа со службой контейнеров Azure и Kubernetes](../kubernetes/container-service-kubernetes-walkthrough.md)