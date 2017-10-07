---
title: "Учебник контейнера службы aaaAzure - управление DC/OS | Документы Microsoft"
description: "Учебник по службе контейнеров Azure — управление DC/OS"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/17/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b91c433bfd7e48ec405cc62be1486d9d4662839d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-service-tutorial---manage-dcos"></a>Учебник по службе контейнеров Azure — управление DC/OS

DC/OS предоставляет распределенную платформу для запуска современных и контейнерных приложений. Служба контейнеров Azure упрощает и убыстряет подготовку кластера DC/OS для использования в рабочей среде. Основные шаги этого краткого сведения требуется toodeploy кластера DC/OS и выполнения основных рабочей нагрузки.

> [!div class="checklist"]
> * Создание кластера DC/OS ACS
> * Подключите кластер toohello
> * Установка контроллера домена/OS CLI hello
> * Развертывание кластера toohello приложения
> * Масштабирование приложения на кластере hello
> * Масштабирование узлов кластера hello DC/OS
> * Базовое управление DC/OS
> * Удалить кластер DC/OS hello

Упражнений этого учебника требуется hello Azure CLI версия 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Получить tooupgrade [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-dcos-cluster"></a>Создание кластера DC/OS

Во-первых, создайте группу ресурсов с hello [Создание группы az](/cli/azure/group#create) команды. Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими. 

Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *westeurope* расположение.

```azurecli
az group create --name myResourceGroup --location westeurope
```

Создайте кластер DC/OS с hello [создать acs az](/cli/azure/acs#create) команды.

Hello следующий пример создает кластер с именем контроллера домена/OS *myDCOSCluster* и создает ключи SSH, если они еще не существует. toouse конкретный набор ключей, используйте hello `--ssh-key-value` параметр.  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

Через несколько минут hello команда завершается и возвращает сведения о развертывании hello.

## <a name="connect-toodcos-cluster"></a>Подключите кластер tooDC/OS

После создания кластера DC/OS доступ к нему возможен через туннель SSH. Выполните следующие команды tooreturn hello общедоступный IP-адрес основного контроллера домена/OS hello hello. Этот IP-адрес хранится в переменной и используется в следующем шаге hello.

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

toocreate hello туннель SSH, запустите следующую команду hello и выполните hello на экране инструкциям. Если уже используется порт 80, hello команда завершается ошибкой. Обновление hello проводном tooone порта не заняты, такие как `85:localhost:80`. 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a>Установка интерфейса командной строки DC/OS

Для установки контроллера домена/OS cli hello, с помощью hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) команды. При использовании Azure CloudShell hello CLI DC/OS уже установлена. Если вы используете hello Azure CLI на macOS или Linux, может потребоваться toorun hello командой sudo.

```azurecli
az acs dcos install-cli
```

Перед hello CLI можно использовать с кластером hello он должен быть туннеля SSH настроенных toouse hello. Таким образом, toodo запустите hello следующую команду, настройки порта hello, при необходимости.

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a>Запуск приложения

по умолчанию Hello, механизм для кластера служб ACS DC/OS планирования — Marathon. Marathon — это приложение используется toostart и управления состоянием приложения hello в кластере DC/OS hello hello. tooschedule приложение через Marathon, создайте файл с именем **marathon app.json**, и hello копировать содержимое в него. 

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

Запустите следующие toorun приложения hello tooschedule команды на кластере DC/OS hello hello.

```azurecli
dcos marathon app add marathon-app.json
```

toosee hello состояние развертывания для приложения hello, запустите следующую команду hello.

```azurecli
dcos marathon app list
```

Здравствуйте, когда **ЗАДАЧИ** значение столбца переходит от *0 и 1* слишком*1/1*, развертывание приложения завершено.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a>Масштабирование приложения Marathon

Приложение одного экземпляра был создан в предыдущем примере hello. Это развертывание, чтобы были доступны, тремя экземплярами приложения hello открываются hello tooupdate **marathon app.json** файл и обновить свойство too3 hello экземпляра.

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 3,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

Обновление приложения hello, с помощью hello `dcos marathon app update` команды.

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

toosee hello состояние развертывания для приложения hello, запустите следующую команду hello.

```azurecli
dcos marathon app list
```

Здравствуйте, когда **ЗАДАЧИ** значение столбца переходит от *1/3* слишком*3/1*, развертывание приложения завершено.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a>Запуск приложения, доступного через Интернет

Hello ACS DC/OS кластер состоит из двух наборов узлов, один общий доступный на hello Интернета и одно частное, который недоступен на hello Интернета. набор по умолчанию Hello — hello закрытый узлов, который использовался в последний пример hello.

toomake приложения доступны на Здравствуйте Интернета, развертывать их toohello набор общих узлов. toodo таким образом, предоставить hello `acceptedResourceRoles` значение из объекта `slave_public`.

Создайте файл с именем **nginx public.json** и hello копировать содержимое в него.

```json
{
  "id": "demo-app",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  },
  "acceptedResourceRoles": [
    "slave_public"
  ]
}
```

Запустите следующие toorun приложения hello tooschedule команды на кластере DC/OS hello hello.

```azurecli 
dcos marathon app add nginx-public.json
```

Получите общедоступный IP-адрес hello hello DC/OS открытый кластера агентов.

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

Просмотр адреса toothis возвращает узел NGINX по умолчанию hello.

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a>Масштабирование кластера DC/OS

В предыдущих примерах hello приложения было масштабированный toomultiple экземпляра. Инфраструктура DC/OS Hello также может быть масштабированный tooprovide больше или меньше вычислительной мощности. Это делается с hello [масштабировать acs az]() команды. 

использовать toosee hello текущее количество агентов DC/OS hello [Показать acs az](/cli/azure/acs#show) команды.

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

tooincrease hello too5 число, используйте hello [масштабировать acs az](/cli/azure/acs#scale) команды. 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a>Удаление кластера DC/OS

Если больше не нужны, можно использовать hello [удаление группы az](/cli/azure/group#delete) команд группы ресурсов tooremove hello, кластер DC/OS и все связанные ресурсы.

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике вы изучили базовые задачи управления DC/OS, включая следующие hello. 

> [!div class="checklist"]
> * Создание кластера DC/OS ACS
> * Подключите кластер toohello
> * Установка контроллера домена/OS CLI hello
> * Развертывание кластера toohello приложения
> * Масштабирование приложения на кластере hello
> * Масштабирование узлов кластера hello DC/OS
> * Удалить кластер DC/OS hello

Предварительное toohello Далее учебника toolearn о загрузить балансировки приложение в контроллер домена или ОС на платформе Azure. 

> [!div class="nextstepaction"]
> [Приложения балансировки нагрузки](container-service-load-balancing.md)