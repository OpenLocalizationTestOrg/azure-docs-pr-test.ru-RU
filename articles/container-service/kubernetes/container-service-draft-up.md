---
title: "aaaUse черновик с контейнера службы Azure и Azure контейнер реестра | Документы Microsoft"
description: "Создание кластера служб ACS Kubernetes и toocreate реестра контейнера Azure первого приложения в Azure с черновик."
services: container-service
documentationcenter: 
author: squillace
manager: gamonroy
editor: 
tags: draft, helm, acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Kubernetes, черновик, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: f5e21cda01e5e8452bf86a5c8fa458904d89f451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-toobuild-and-deploy-an-application-tookubernetes"></a>Использовать черновик с toobuild контейнера службы Azure и Azure контейнер реестра и развертывать приложения tooKubernetes

[Черновик](https://aka.ms/draft) новое средство открытым исходным кодом, которое делает его легко toodevelop контейнера-приложениям и разверните tooKubernetes кластеры без знания многое о Docker и Kubernetes--или даже их установки. С помощью таких средств, как черновик позволяют вам и группам фокус ввода Создание приложения hello с Kubernetes, не обращая tooinfrastructure столько внимания.

Вы можете использовать черновик с любым реестром образов Docker и любым кластером Kubernetes, а также использовать его локально. В этом учебнике показано, как toouse ACS с toocreate Kubernetes, контроля доступа и Azure DNS конвейера с помощью черновик динамической разработчик CI или компакт-диска.


## <a name="create-an-azure-container-registry"></a>Создание реестра контейнеров Azure
Вы можете легко [создать новый контейнер реестра Azure](../../container-registry/container-registry-get-started-azure-cli.md), но действий hello следующим образом:

1. Создайте кластер ACR реестра и hello Kubernetes toomanage группы ресурсов Azure в ACS.
      ```azurecli
      az group create --name draft --location eastus
      ```

2. Создайте реестр образов ACR с помощью команды [az acr create](/cli/azure/acr#create).
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a>Создание службы контейнеров Azure с помощью Kubernetes

Теперь вы готовы toouse [создать acs az](/cli/azure/acs#create) toocreate ACS кластер, использующий Kubernetes как hello `--orchestrator-type` значение.
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> Так как Kubernetes не типом orchestrator по умолчанию hello, убедитесь, что вы используете hello `--orchestrator-type kubernetes` переключения.

Вывод Hello при успешном выполнении выглядит примерно следующие toohello.

```json
waiting for AAD role toopropagate.done
{
  "id": "/subscriptions/<guid>/resourceGroups/draft/providers/Microsoft.Resources/deployments/azurecli14904.93snip09",
  "name": "azurecli1496227204.9323909",
  "properties": {
    "correlationId": "<guid>",
    "debugSetting": null,
    "dependencies": [],
    "mode": "Incremental",
    "outputs": null,
    "parameters": {
      "clientSecret": {
        "type": "SecureString"
      }
    },
    "parametersLink": null,
    "providers": [
      {
        "id": null,
        "namespace": "Microsoft.ContainerService",
        "registrationState": null,
        "resourceTypes": [
          {
            "aliases": null,
            "apiVersions": null,
            "locations": [
              "westus"
            ],
            "properties": null,
            "resourceType": "containerServices"
          }
        ]
      }
    ],
    "provisioningState": "Succeeded",
    "template": null,
    "templateLink": null,
    "timestamp": "2017-05-31T10:46:29.434095+00:00"
  },
  "resourceGroup": "draft"
}
```

Теперь, когда имеется кластер hello учетные данные можно импортировать с помощью hello [az kubernetes get-учетные данные acs](/cli/azure/acs/kubernetes#get-credentials) команды. Теперь имеется файл локальной конфигурации для кластера, являющийся какие Helm и черновик должны tooget поставленных задач.

## <a name="install-and-configure-draft"></a>Установка и настройка черновика
инструкции по установке Hello для черновик находятся в hello [репозитория Черновик](https://github.com/Azure/draft/blob/master/docs/install.md). Они относительно просты, но требуют некоторые конфигурации, так как он зависит от [Helm](https://aka.ms/helm) toocreate и развернуть диаграмму Helm в кластер Kubernetes hello.

1. [Скачайте и установите Helm](https://aka.ms/helm#install).
2. Используйте toosearch Helm для и установите `stable/traefik`и входящих контроллера tooenable входящие запросы для сборок.
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    Теперь задать Контрольное значение для hello `ingress` контроллера toocapture hello внешнего IP значение при его развертывании. Этот IP-адрес будет hello один [сопоставления домена развертывания tooyour](#wire-up-deployment-domain) в следующем разделе hello.

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    В этом случае hello внешний IP-адрес развертывания домен hello `13.64.108.240`. Теперь вы можете сопоставить на IP-адрес домена toothat.

## <a name="wire-up-deployment-domain"></a>Подключение домена развертывания

Черновик создает выпуск для каждого чарта Helm, который он создает, в каждом приложении, над которым вы работаете. Каждый из них возвращает сформированное имя, которое используется черновик как _поддомен_ поверх hello корневой _домена развертывания_ , можно управлять. (В этом примере мы используем `squillace.io` как hello развертывания домен.) tooenable такое поведение дочернего домена, необходимо создать запись A для `'*'` записи DNS для домена развертывания, чтобы автоматически созданный каждого дочернего домена является перенаправленное toohello Kubernetes контроллер входящих кластера.

Поставщиком домена имеет свои собственные способом tooassign DNS-серверы; слишком[tooAzure nameservers вашего домена DNS делегировать](../../dns/dns-delegate-domain-azure-dns.md), принимают hello следующие шаги:

1. Создайте группу ресурсов для зоны.
    ```azurecli
    az group create --name squillace.io --location eastus
    {
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io",
      "location": "eastus",
      "managedBy": null,
      "name": "zones",
      "properties": {
        "provisioningState": "Succeeded"
      },
      "tags": null
    }
    ```

2. Создайте зону DNS для домена.
Используйте hello [создание зоны dns сети az](/cli/azure/network/dns/zone#create) команда tooobtain hello nameservers toodelegate DNS управления tooAzure DNS для домена.
    ```azurecli
    az network dns zone create --resource-group squillace.io --name squillace.io
    {
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/zones/providers/Microsoft.Network/dnszones/squillace.io",
      "location": "global",
      "maxNumberOfRecordSets": 5000,
      "name": "squillace.io",
      "nameServers": [
        "ns1-09.azure-dns.com.",
        "ns2-09.azure-dns.net.",
        "ns3-09.azure-dns.org.",
        "ns4-09.azure-dns.info."
      ],
      "numberOfRecordSets": 2,
      "resourceGroup": "squillace.io",
      "tags": {},
      "type": "Microsoft.Network/dnszones"
    }
    ```
3. Добавьте hello DNS-серверы, которые заданы поставщика toohello домена для домена развертывания, который позволяет вам toouse Azure DNS toorepoint домена необходимо.
4. Создайте запись A набор записей для вашего развертывания домена сопоставление toohello `ingress` IP-адрес из предыдущего раздела hello шаг 2.
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
выходные данные Hello выглядит примерно так:
    ```json
    {
      "arecords": [
        {
          "ipv4Address": "13.64.108.240"
        }
      ],
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io/providers/Microsoft.Network/dnszones/squillace.io/A/*",
      "metadata": null,
      "name": "*",
      "resourceGroup": "squillace.io",
      "ttl": 3600,
      "type": "Microsoft.Network/dnszones/A"
    }
    ```

5. Настройка toouse черновик реестра и создайте дочерние домены для каждой диаграммы Helm созданные им. tooconfigure черновик, необходимо:
  - имя реестра контейнеров Azure (в этом примере — `draft`);
  - раздел реестра или пароль, полученный из `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`;
  - Развертывание Hello корневого домена, что вы настроили toomap toohello Kubernetes входящих внешний IP-адрес (здесь `squillace.io`)

  Вызовите `draft init` и процесса настройки hello запрашивает hello значений, приведенных выше. Hello процесс кажется, что-то hello следующие hello первый раз при запуске.
 ```bash
    $ draft init
    Creating pack ruby...
    Creating pack node...
    Creating pack gradle...
    Creating pack maven...
    Creating pack php...
    Creating pack python...
    Creating pack dotnetcore...
    Creating pack golang...
    $DRAFT_HOME has been configured at /Users/ralphsquillace/.draft.

    In order tooinstall Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io, quay.io, myregistry.azurecr.io): draft.azurecr.io
    2. Enter your username: draft
    3. Enter your password:
    4. Enter your org where Draft will push images [draft]: draft
    5. Enter your top-level domain for ingress (e.g. draft.example.com): squillace.io
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
    ```

Теперь вы готовы toodeploy приложения.


## <a name="build-and-deploy-an-application"></a>Сборка и развертывание приложения

В репозитории черновик hello, [шесть простой пример приложения](https://github.com/Azure/draft/tree/master/examples). Клонировать репозиторий hello и используем hello [примере Python](https://github.com/Azure/draft/tree/master/examples/python). Изменения в каталог hello примеры и Python, а тип `draft create` toobuild приложения hello. Оно должно иметь вид следующий пример hello.
```bash
$ draft create
--> Python app detected
--> Ready toosail
```

Вывод Hello включает файл Dockerfile и Helm диаграммы. toobuild и развертывания, просто введите `draft up`. выходные данные Hello слишком большой, но начинается как следующий пример hello.
```bash
$ draft up
--> Building Dockerfile
Step 1 : FROM python:onbuild
onbuild: Pulling from library/python
10a267c67f42: Pulling fs layer
fb5937da9414: Pulling fs layer
9021b2326a1e: Pulling fs layer
dbed9b09434e: Pulling fs layer
ea8a37f15161: Pulling fs layer
<snip>
```

Когда и успешно заканчивается на что-нибудь подобное toohello следующий пример.
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying tooKubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io tooaccess your application

Watching local files for changes...
```

Все, что указано имя на диаграмме, теперь можно `curl http://gangly-bronco.squillace.io` tooreceive hello ответ, `Hello World!`.

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда кластер ACS Kubernetes можно изучить с помощью [реестра контейнера Azure](../../container-registry/container-registry-intro.md) toocreate дополнительные и различных развертывания этого сценария. Например, вы можете создать набор записей DNS домена draft._basedomain.toplevel_, с помощью которого можно отключать функции важного поддомена для определенных развертываний ACS.






