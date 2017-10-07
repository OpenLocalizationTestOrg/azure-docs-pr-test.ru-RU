---
title: "aaaManage Azure DC/OS кластера с помощью Marathon REST API | Документы Microsoft"
description: "Развертывание кластера контейнера службы Azure DC/OS tooan контейнеры с помощью API-интерфейса REST Marathon hello."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Mesos, Azure"
ms.assetid: c7175446-4507-4a33-a7a2-63583e5996e3
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: d926b9b90f5d4eda85a015d9ea0d96fea2c4b566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-container-management-through-hello-marathon-rest-api"></a>Управление контейнерами DC/OS через API-Интерфейс REST Marathon hello
Контроллер домена/OS предоставляет среду для развертывания и масштабирования кластерных рабочих нагрузок сталкиваясь аппаратным обеспечением hello. На базе DC/OS работает платформа, которая управляет планированием и выполнением вычислительных рабочих нагрузок. Несмотря на то, что платформы доступны для многих распространенных рабочих нагрузок, в этом документе позволяет начать создание и масштабирование развертывания контейнера с помощью API-интерфейса REST Marathon hello. 

## <a name="prerequisites"></a>Предварительные требования

Для выполнения этих примеров вам потребуется кластер DC/OS, настроенный в службе контейнеров Azure. Необходимо также кластера toothis toohave возможности удаленного подключения. Дополнительные сведения об этих элементах см. следующие статьи hello:

* [Развертывание кластера службы контейнеров Azure.](container-service-deployment.md)
* [Подключение кластера tooan контейнера службы Azure](../container-service-connect.md)

## <a name="access-hello-dcos-apis"></a>Доступ к API-интерфейсы DC/OS hello
После toohello подключенных кластера контейнера службы Azure, доступны hello DC/OS и связанные API REST через порт http://localhost:local. Hello примерах в этом документе предполагается, что туннелирование на порт 80. Например, можно получить конечные точки Marathon hello в URI начиная с версии `http://localhost/marathon/v2/`. 

Дополнительные сведения о hello различных API-интерфейсов документации hello Mesosphere hello [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) и [Chronos API](https://mesos.github.io/chronos/docs/api.html)и в документации Apache hello [Mesos API планировщика ](http://mesos.apache.org/documentation/latest/scheduler-http-api/).

## <a name="gather-information-from-dcos-and-marathon"></a>Сбор сведений из DC/OS и Marathon
Перед развертыванием кластера DC/OS toohello контейнеры получить некоторые сведения о кластере DC/OS hello, такие как имена hello и состояние агентов DC/OS hello. toodo таким образом, запрос hello `master/slaves` конечной точке API REST DC/OS hello. Если все пойдет хорошо hello запрос возвращает список агентов DC/OS и несколько свойств для каждого.

```bash
curl http://localhost/mesos/master/slaves
```

Теперь воспользуйтесь hello Marathon `/apps` toocheck конечной точки для текущего кластера DC/OS toohello развертывания приложения. Если это новый кластер, вы увидите пустой массив приложений.

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a>Развертывание контейнера формата Docker
Контейнеры Docker формате через API-Интерфейс REST Marathon hello развертывание с помощью JSON-файл, описывающий hello предназначен развертывания. Hello следующий пример развертывает Nginx контейнера tooa закрытый агент в кластере hello. 

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

toodeploy контейнер Docker в формате хранения hello JSON-файла в доступном расположении. Далее, toodeploy hello контейнер, запустите следующую команду hello. Укажите имя hello hello JSON-файла (`marathon.json` в этом примере).

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

Hello выходные данные выглядят аналогично toohello следующее:

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

Теперь при выполнении запроса Marathon для приложений, это новое приложение появляется в выходных данных hello.

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-hello-container"></a>Достижения контейнера hello

Вы можете проверить, hello Nginx, запущенного на одном из агентов закрытый hello в кластере hello в контейнере. toofind hello узел и порт, где запущен контейнер hello, запросить Marathon hello запуска задач: 

```bash
curl localhost/marathon/v2/tasks
```

Найдите значение hello `host` в выходных данных hello (IP-адресов примерно слишком`10.32.0.x`), а значение hello `ports`.


Теперь можно проверить SSH терминалов (туннельного подключения) toohello Управление соединениями полное доменное имя кластера hello. После подключения сделать hello следующий запрос, заменив hello правильные значения `host` и `ports`:

```bash
curl http://host:ports
```

Hello вывод server Nginx — аналогичные toohello следующее:

![Доступ к Nginx из контейнера](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a>Масштабирование контейнеров
В развертывании приложений можно использовать tooscale Marathon API hello out или масштаб. В предыдущем примере hello развернут один экземпляр приложения. Давайте масштаба toothree экземпляров приложения. Таким образом, toodo создания JSON-файла с помощью hello после текста JSON и сохранить ее в доступном расположении.

```json
{ "instances": 3 }
```

Запустите из туннеля, следующая команда tooscale out приложения hello hello.

> [!NOTE]
> Hello URI является http://localhost/marathon/v2/apps/ следуют идентификатор hello tooscale приложения hello. Если вы используете образец hello Nginx, предоставленная здесь, hello URI будет http://localhost/marathon/v2/apps/nginx.
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

Наконец запроса конечной точки Marathon hello для приложений. вы увидите, что теперь есть три контейнера Nginx.

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a>Аналогичные команды PowerShell
Эти же действия можно выполнить с помощью команд PowerShell в системе Windows.

toogather сведения о кластере DC/OS hello, например имена агентов и состояние агентов, выполните следующую команду hello.

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

Контейнеры Docker формате через Marathon развертывание с помощью JSON-файл, описывающий hello предназначен развертывания. Hello следующий пример развертывает контейнера Nginx hello, привязки контроллера домена/OS hello агента tooport 80 контейнера hello порт 80.

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

toodeploy контейнер Docker в формате хранения hello JSON-файла в доступном расположении. Далее, toodeploy hello контейнер, запустите следующую команду hello. Укажите путь toohello hello JSON-файла (`marathon.json` в этом примере).

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

Также можно использовать tooscale Marathon API hello out или масштаб в развертывании приложений. В предыдущем примере hello развернут один экземпляр приложения. Давайте масштаба toothree экземпляров приложения. Таким образом, toodo создания JSON-файла с помощью hello после текста JSON и сохранить ее в доступном расположении.

```json
{ "instances": 3 }
```

Следующая команда tooscale out приложения hello выполнения hello:

> [!NOTE]
> Hello URI является http://localhost/marathon/v2/apps/ следуют идентификатор hello tooscale приложения hello. Если вы используете пример hello Nginx, описанный здесь, hello URI будет http://localhost/marathon/v2/apps/nginx.
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a>Дальнейшие действия
* [Дополнительные сведения о конечных точек Mesos HTTP hello](http://mesos.apache.org/documentation/latest/endpoints/)
* [Дополнительные сведения об API-интерфейса REST Marathon hello](https://mesosphere.github.io/marathon/docs/rest-api.html)

