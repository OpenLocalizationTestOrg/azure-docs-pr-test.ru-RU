---
title: "aaaUsing контроля доступа с кластера с контроллера домена или ОС Azure | Документы Microsoft"
description: "Использование реестра контейнеров Azure с кластером DC/OS в Службе контейнеров Azure"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service, acr, azure-container-registry
keywords: "Docker, контейнеры, микрослужбы, Mesos, Azure, FileShare, cifs"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 9a2802da788b50147d8b4259436bdcdb0c929db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-acr-with-a-dcos-cluster-toodeploy-your-application"></a>Использовать ACR toodeploy кластера DC/OS приложение

В этой статье мы исследуем как toouse реестра контейнера Azure в кластере DC/OS. С помощью контроля доступа позволяет tooprivately хранилище и управление образами контейнеров. В этом учебнике hello следующие задачи:

> [!div class="checklist"]
> * Развертывание реестра контейнеров Azure (при необходимости).
> * Настройка проверки подлинности ACR в кластере DC/OS.
> * Загрузить образ toohello реестра контейнера Azure
> * Запустите образ контейнера из hello реестра контейнера Azure

Вы должны ACS DC/OS hello toocomplete кластера шаги в этом учебнике. При необходимости его можно создать с помощью следующего [примера сценария](./../kubernetes/scripts/container-service-cli-deploy-dcos.md).

Упражнений этого учебника требуется hello Azure CLI версия 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Получить tooupgrade [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a>Развертывание реестра контейнеров Azure

При необходимости создайте в реестре контейнера Azure с hello [создать az acr](/cli/azure/acr#create) команды. 

Hello следующий пример создает реестр с помощью создания случайного имени. Hello реестра настроен с учетной записью администратора, с использованием hello `--admin-enabled` аргумент.

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

После создания реестра hello hello Azure CLI выводит примерно следующие toohello данных. Запишите hello `name` и `loginServer`, они используются в последующих шагах.

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T03:40:56.511597+00:00",
  "id": "/subscriptions/f2799821-a08a-434e-9128-454ec4348b10/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry23489",
  "location": "eastus",
  "loginServer": "mycontainerregistry23489.azurecr.io",
  "name": "myContainerRegistry23489",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "mycontainerregistr034017"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

Получить учетные данные реестра hello контейнера с помощью hello [Показать учетных данных acr az](/cli/azure/acr/credential) команды. Замена hello `--name` с одного указаны в последнем шаге hello hello. Запишите один пароль, так как он потребуется в дальнейшем.

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

Дополнительные сведения о реестре контейнера Azure см. в разделе [введение tooprivate Docker контейнера реестры](../../container-registry/container-registry-intro.md). 

## <a name="manage-acr-authentication"></a>Управление проверкой подлинности ACR

проверить подлинность Hello традиционным способом toopush и запросу образа из частной реестра — toofirst реестра hello. toodo таким образом, можно использовать hello `docker login` команду на любом клиенте, который должен tooaccess hello частного реестра. Поскольку кластера DC/OS может содержать множество узлов, каждый из которых требуется toobe с hello контроля доступа с проверкой подлинности, это полезно tooautomate этот процесс на каждом узле. 

### <a name="create-shared-storage"></a>Создание общего хранилища

Этот процесс использует Azure файловый ресурс, который был подключен на каждом узле в кластере hello. Если вы еще не настроили общее хранилище, ознакомьтесь со статьей [Создание и подключение файлового ресурса к кластеру DC/OS](container-service-dcos-fileshare.md).

### <a name="configure-acr-authentication"></a>Настройка проверки подлинности ACR

Сначала необходимо получите hello полное доменное имя hello DC/OS-шаблоны и сохранить его в переменной.

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

Создайте SSH-подключения с hello master (или первый образец hello) кластера на базе контроллера домена/ОС. Обновите имя пользователя hello, если значение не по умолчанию использовался при создании кластера hello.

```azurecli-interactive
ssh azureuser@$FQDN
```

Выполнения hello следующая команда toologin toohello реестра контейнера Azure. Замените hello `--username` с именем hello реестра контейнера hello и hello `--password` с одним из предоставленных hello пароли. Замените hello последний аргумент *mycontainerregistry.azurecr.io* в примере hello именем loginServer hello hello контейнер реестра. 

Эта команда сохраняет значения для проверки подлинности hello локально под hello `~/.docker` пути.

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

Создайте сжатый файл, содержащий hello контейнер реестра проверки подлинности.

```azurecli-interactive
tar czf docker.tar.gz .docker
```

Скопируйте этот файл toohello общее хранилище кластера. Этот шаг делает файл hello недоступны на всех узлах кластера DC/OS hello.

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-tooacr"></a>Отправка изображения tooACR

Теперь с компьютера разработки, или любой другой системы с установленным Docker, создать образ и загрузить его toohello реестра контейнера Azure.

Создание контейнера из образа Ubuntu hello.

```azurecli-interactive
docker run ubunut --name base-image
```

Теперь выполните захват hello контейнера в новый образ. Имя образа Hello должно tooinclude hello `loginServer` имя registrywith контейнера hello в формат `loginServer/imageName`.

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

Имя входа в hello реестра контейнера Azure. Замените имя hello имя loginServer hello, hello — имя пользователя с именем hello реестра контейнера hello и hello--пароль с помощью одного из предоставленных hello пароли.

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

Наконец отправьте hello изображения toohello ACR реестра. Этот пример отправляет образ с именем dcos-demo.

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a>Запуск образа из ACR

toouse образа из реестра hello контроля доступа, создайте файл имена *acrDemo.json* и копирования hello после текста в него. Замените имя образа hello hello реестра loginServer имени для контейнера и имя изображения, например `loginServer/imageName`. Запишите hello `uris` свойство. Это свойство содержит hello расположение файла реестра проверки подлинности hello контейнера, который в данном случае является hello Azure файловый ресурс, монтируется на каждом узле в кластере DC/OS hello.

```json
{
  "id": "myapp",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "mycontainerregistry30678.azurecr.io/dcos-demo",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "uris":  [
       "file:///mnt/share/dcosshare/docker.tar.gz"
   ]
}
```

Развертывание приложения hello с hello DC/OC CLI.

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике у настройки toouse DC/OS, которое реестра контейнера Azure, включая hello следующие задачи:

> [!div class="checklist"]
> * Развертывание реестра контейнеров Azure (при необходимости).
> * Настройка проверки подлинности ACR в кластере DC/OS.
> * Загрузить образ toohello реестра контейнера Azure
> * Запустите образ контейнера из hello реестра контейнера Azure
