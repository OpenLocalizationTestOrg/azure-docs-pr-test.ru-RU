---
title: "контейнеры aaaLoad баланс в кластере Azure DC/OS | Документы Microsoft"
description: "Сведения о балансировке нагрузки нескольких контейнеров в кластере DC/OS в Службе контейнеров Azure."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Контейнеры, микрослужбы, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 2249cb06880cdb7e9a3aa94c0750c6a27316d349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a>Балансировка нагрузки контейнеров в кластере DC/OS в Службе контейнеров Azure
В этой статье мы расскажем, как внутренний балансировщик нагрузки в контроллер домена/OS toocreate управление контейнера службы Azure, с помощью балансировки Нагрузки Marathon. Такая конфигурация позволяет вам tooscale приложений по горизонтали. Оно также позволяет tootake преимуществами кластеров открытых и закрытых агента hello размещая вашей подсистемы балансировки нагрузки на открытый кластера hello и вашего приложения контейнеры закрытый кластере hello. Изучив это руководство, вы:

> [!div class="checklist"]
> * Настройка подсистемы балансировки нагрузки Marathon
> * Развертывание приложения с помощью подсистемы балансировки нагрузки hello
> * Настройка Azure Load Balancer

Вы должны ACS DC/OS hello toocomplete кластера шаги в этом учебнике. При необходимости его можно создать с помощью следующего [примера сценария](./../kubernetes/scripts/container-service-cli-deploy-dcos.md).

Упражнений этого учебника требуется hello Azure CLI версия 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Получить tooupgrade [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a>Общие сведения о балансировке нагрузки

В кластере DC/OS службы контейнеров Azure существует два уровня балансировки нагрузки: 

**Подсистема балансировки нагрузки Azure** предоставляет открытым точкам входа (те, что конечным пользователям доступ к hello). Балансировки Нагрузки Azure автоматически обеспечивается контейнера службы Azure и по умолчанию, настроенные tooexpose порт 80, 443 и 8080.

**Hello Marathon балансировки нагрузки (marathon фунта)** маршруты входящих запросов toocontainer экземпляров, обслуживающих эти запросы. Как мы масштабировать hello контейнеры, предоставляя веб-узле службы, динамически адаптируется hello marathon-балансировки нагрузки. Эта подсистема балансировки нагрузки не предоставляется по умолчанию в службе контейнера, но это просто tooinstall.

## <a name="configure-marathon-load-balancer"></a>Настройка подсистемы балансировки нагрузки Marathon

Подсистема балансировки нагрузки Marathon динамически перенастраивает основании hello контейнеры, которые развернуты. Это также потери устойчивым toohello контейнер или агента -, если это происходит, Apache Mesos перезапускает hello контейнера в другом месте и балансировки нагрузки marathon адаптирует.

Выполнения hello следующая команда балансировки нагрузки marathon tooinstall hello в кластере hello открытый агента.

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a>Развертывание приложения с балансировкой нагрузки

Теперь, когда у нас есть пакет балансировки нагрузки marathon hello, мы разверните контейнер приложения, что мы хочет tooload баланс. 

Сначала необходимо получите полное доменное имя в открытую hello агентов hello.

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

Создайте файл с именем *hello web.json* и копирования в hello после содержимого. Hello `HAPROXY_0_VHOST` метки должен toobe обновляется hello полное доменное имя контроллера домена/OS агентов hello. 

```json
{
  "id": "web",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "yeasy/simple-web",
      "network": "BRIDGE",
      "portMappings": [
        { "hostPort": 0, "containerPort": 80, "servicePort": 10000 }
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
  "labels":{
    "HAPROXY_GROUP":"external",
    "HAPROXY_0_VHOST":"YOUR FQDN",
    "HAPROXY_0_MODE":"http"
  }
}
```

С помощью приложения hello toorun CLI DC/OS hello. По умолчанию Marathon разворачивает закрытый кластера приложение hello toohello hello. Это означает, что hello выше развертывания доступен только через балансировки нагрузки, которое обычно является hello требуемого поведения.

```azurecli-interactive
dcos marathon app add hello-web.json
```

После развертывания приложения hello Обзор toohello полное доменное имя приложения с балансировкой нагрузки tooview кластера hello агента.

![Изображение приложения с балансировкой нагрузки](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a>Настройка Azure Load Balancer

По умолчанию Azure Load Balancer использует порты 80, 8080 и 443. Если вы используете один из этих трех портов (как это было сделано в hello в приведенном выше примере), а затем не требуется toodo. Должен быть доступ toohit полное доменное имя подсистемы балансировки загрузки агента и каждый раз при обновлении будет попадании один из трех веб-серверов в циклического перебора. 

Если используется другой порт, требуется правило tooadd циклический перебор и проверки на hello балансировки нагрузки для hello порт, который использовался. Это можно сделать из hello [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), с помощью команд hello `azure network lb rule create` и `azure network lb probe create`.

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике вы узнали о балансировки нагрузки в ACS с hello Marathon и нагрузки Azure, включая балансировки нагрузки hello следующие действия:

> [!div class="checklist"]
> * Настройка подсистемы балансировки нагрузки Marathon
> * Развертывание приложения с помощью подсистемы балансировки нагрузки hello
> * Настройка Azure Load Balancer

Переместить toohello Далее учебника toolearn об интеграции хранилища Azure с контроллера домена или ОС в Azure.

> [!div class="nextstepaction"]
> [Подключение общей папки Azure в кластере DC/OS](container-service-dcos-fileshare.md)