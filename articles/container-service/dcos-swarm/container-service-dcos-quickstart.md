---
title: "aaaAzure быстрого запуска контейнера службы - развертывание кластера DC/OS | Документы Microsoft"
description: "Краткое руководство по службе контейнеров Azure. Развертывание кластера DC/OS"
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
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b961f15bd73deeafda5a3fc25ab53c839195219b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-dcos-cluster"></a>Развертывание кластера DC/OS

DC/OS предоставляет распределенную платформу для запуска современных и контейнерных приложений. Служба контейнеров Azure упрощает и убыстряет подготовку кластера DC/OS для использования в рабочей среде. Это краткое руководство сведения hello основные действия toodeploy кластера DC/OS и выполнения основных рабочей нагрузки.

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.

Упражнений этого учебника требуется hello Azure CLI версия 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Получить tooupgrade [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="log-in-tooazure"></a>Войдите в tooAzure 

Войдите в подписку Azure совместно с hello tooyour [входа az](/cli/azure/#login) команды и выполните hello на экране инструкциям.

```azurecli
az login
```

## <a name="create-a-resource-group"></a>Создание группы ресурсов

Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды. Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими. 

Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение.

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a>Создание кластера DC/OS

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

туннель SSH Hello можно протестировать путем просмотра слишком`http://localhost`. Если порт других что было использовано 80, измените расположение toomatch hello. 

Если туннель SSH hello создана успешно, возвращается hello DC/OS портала.

![Пользовательский интерфейс DCOS](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a>Установка интерфейса командной строки DC/OS

интерфейс командной строки Hello DC/OS — используется toomanage DC/OS кластера из командной строки hello. Для установки контроллера домена/OS cli hello, с помощью hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) команды. При использовании Azure CloudShell hello CLI DC/OS уже установлена. 

Если вы используете hello Azure CLI на macOS или Linux, может потребоваться toorun hello командой sudo.

```azurecli
az acs dcos install-cli
```

Перед hello CLI можно использовать с кластером hello он должен быть туннеля SSH настроенных toouse hello. Таким образом, toodo запустите hello следующую команду, настройки порта hello, при необходимости.

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a>Запуск приложения

по умолчанию Hello, механизм для кластера служб ACS DC/OS планирования — Marathon. Marathon — это приложение используется toostart и управления состоянием приложения hello в кластере DC/OS hello hello. tooschedule приложение через Marathon, создайте файл с именем *marathon app.json*, и hello копировать содержимое в него. 

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
dcos marathon app add marathon-app.json
```

toosee hello состояние развертывания для приложения hello, запустите следующую команду hello.

```azurecli
dcos marathon app list
```

Здравствуйте, когда **ОЖИДАНИЯ** значение столбца переходит от *True* слишком*False*, развертывание приложения завершено.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

Получение hello общедоступный IP-адрес кластера агенты hello DC/OS.

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

Просмотр адреса toothis возвращает узел NGINX по умолчанию hello.

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a>Удаление кластера DC/OS

Если больше не нужны, можно использовать hello [удаление группы az](/cli/azure/group#delete) команд группы ресурсов tooremove hello, кластер DC/OS и все связанные ресурсы.

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a>Дальнейшие действия

В этом кратком руководстве после развертывания кластера DC/OS и запустил простой контейнер Docker на кластере hello. toolearn Дополнительные сведения о службе Azure контейнера, по-прежнему учебники toohello ACS.

> [!div class="nextstepaction"]
> [Управление кластером DC/OS ACS](container-service-dcos-manage-tutorial.md)