---
title: "aaaQuickstart - кластера CE Docker в Azure для Linux | Документы Microsoft"
description: "Быстро Узнайте toocreate кластер Docker CE для Linux с контейнерами в службе контейнера Azure с hello Azure CLI."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, Docker, Swarm
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 6c26c12ed085ec379c3486095a5fa51379afc5a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-ce-cluster"></a>Развертывание кластера Docker CE

В этом кратком руководстве развернут кластер Docker CE с помощью hello Azure CLI. Контейнер несколькими приложение, состоящее из веб-сервер и экземпляр Redis затем развертывается и запускается на кластере hello. После завершения приложения hello доступна через Интернет hello.

Выпуск Docker CE в службе контейнеров Azure находится на стадии предварительной версии и **его не следует использовать для рабочих нагрузок в рабочей среде**.

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.

Если выбрать tooinstall и использовать hello CLI локально, краткого руководства требуется управлением hello Azure CLI версия 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Создание группы ресурсов

Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды. Группа ресурсов Azure — это логическая группа, в которой выполняется развертывание и администрирование ресурсов Azure.

Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *ukwest* расположение.

```azurecli-interactive
az group create --name myResourceGroup --location ukwest
```

Выходные данные:

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westcentralus",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-docker-swarm-cluster"></a>Создание кластера Docker Swarm

Создайте кластер Docker CE в контейнере службы Azure с hello [создать acs az](/cli/azure/acs#create) команды. 

Hello следующий пример создает кластер с именем *mySwarmCluster* с Linux в один главный узел и три узла агента Linux.

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type dockerce --resource-group myResourceGroup --generate-ssh-keys
```

Через несколько минут hello команда завершается и возвращает в формате json сведения о кластере hello.

## <a name="connect-toohello-cluster"></a>Подключите кластер toohello

В этом кратком руководстве необходимо полное доменное имя главного помощью Docker Swarm hello и пул агентов Docker hello hello. Выполните следующую команду, tooreturn оба hello master и агента полных доменных имен hello.


```bash
az acs list --resource-group myResourceGroup --query '[*].{Master:masterProfile.fqdn,Agent:agentPoolProfiles[0].fqdn}' -o table
```

Выходные данные:

```bash
Master                                                               Agent
-------------------------------------------------------------------  --------------------------------------------------------------------
myswarmcluster-myresourcegroup-d5b9d4mgmt.ukwest.cloudapp.azure.com  myswarmcluster-myresourcegroup-d5b9d4agent.ukwest.cloudapp.azure.com
```

Создайте главный группу мелких объектов toohello туннеля SSH. Замените `MasterFQDN` с hello адрес полного доменного ИМЕНИ базы данных master hello группу мелких объектов.

```bash
ssh -p 2200 -fNL localhost:2374:/var/run/docker.sock azureuser@MasterFQDN
```

Набор hello `DOCKER_HOST` переменной среды. Это позволяет toorun команды docker с помощью Docker Swarm hello без имени hello toospecify hello узла.

```bash
export DOCKER_HOST=localhost:2374
```

Теперь вы находитесь службы Docker готов toorun на hello с помощью Docker Swarm.


## <a name="run-hello-application"></a>Запустите приложение hello

Создайте файл с именем `azure-vote.yaml` и hello копировать содержимое в него.


```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

Запустите hello [развертывание стека docker](https://docs.docker.com/engine/reference/commandline/stack_deploy/) команды toocreate hello Azure голос службы.

```bash
docker stack deploy azure-vote --compose-file azure-vote.yaml
```

Выходные данные:

```bash
Creating network azure-vote_default
Creating service azure-vote_azure-vote-back
Creating service azure-vote_azure-vote-front
```

Используйте hello [docker ps стека](https://docs.docker.com/engine/reference/commandline/stack_ps/) команды tooreturn hello состояние развертывания приложения hello.

```bash
docker stack ps azure-vote
```

Здравствуйте, один раз `CURRENT STATE` каждой службы является `Running`, приложение hello готов.

```bash
ID                  NAME                            IMAGE                                 NODE                               DESIRED STATE       CURRENT STATE                ERROR               PORTS
tnklkv3ogu3i        azure-vote_azure-vote-front.1   microsoft/azure-vote-front:redis-v1   swarmm-agentpool0-66066781000004   Running             Running 5 seconds ago                            
lg99i4hy68r9        azure-vote_azure-vote-back.1    redis:latest                          swarmm-agentpool0-66066781000002   Running             Running about a minute ago
```

## <a name="test-hello-application"></a>Тестирование приложения hello

Обзор toohello tootest пула агента hello группу мелких объектов ожидания hello приложения Azure голос полное доменное имя.

![Изображение просмотра tooAzure голоса](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a>Удаление кластера
Когда кластер hello не нужны, можно использовать hello [удаление группы az](/cli/azure/group#delete) команд группы ресурсов tooremove hello, контейнер службы и все связанные ресурсы.

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a>Получение кода hello

В этом кратком руководстве образы контейнеров предварительно созданной были используется toocreate службу Docker. Hello связанные код приложения, Dockerfile, и создать файл доступны на сайте GitHub.

[https://github.com/Azure-Samples/azure-voting-app-redis](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a>Дальнейшие действия

В этом кратком руководстве развертывания кластера с помощью Docker Swarm и развернуты tooit приложение несколькими контейнера.

toolearn об интеграции с Visual Studio Team Services Docker горячего по-прежнему toohello CI или компакт-диска с помощью Docker Swarm и VSTS.

> [!div class="nextstepaction"]
> [Непрерывная интеграция и доставка с помощью Docker Swarm и VSTS](./container-service-docker-swarm-setup-ci-cd.md)