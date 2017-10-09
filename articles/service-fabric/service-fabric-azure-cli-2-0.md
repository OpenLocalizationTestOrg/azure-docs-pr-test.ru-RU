---
title: "aaaGet работы с Azure Service Fabric и Azure CLI 2.0"
description: "Узнайте, как toouse hello Azure Service Fabric команды модуля в Azure CLI, версии 2.0. Узнайте, как tooconnect tooa кластера и как toomanage приложений."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ddbd0ef503dd3fff61494cc2cfa7c9a2e8d0a9a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-and-azure-cli-20"></a>Azure Service Fabric и Azure CLI 2.0

Hello средство командной строки Azure (Azure CLI) версии 2.0 включает управление кластерами Azure Service Fabric toohelp команд. Узнайте, как tooget работу с Azure CLI и Service Fabric.

## <a name="install-azure-cli-20"></a>Установка Azure CLI 2.0

Можно использовать toointeract команды Azure CLI 2.0 с и позволяющая управлять кластерами Service Fabric. tooget hello последнюю версию Azure CLI, выполните hello [стандартного процесса Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).

Дополнительные сведения см. в разделе hello [Обзор Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/overview).

## <a name="azure-cli-syntax"></a>Синтаксис Azure CLI

Все команды Service Fabric в Azure CLI начинаются с префикса `az sf`. Общие сведения о командах hello, можно использовать использовать `az sf -h`. Для получения сведений об одной команде используйте `az sf <command> -h`.

Команды Service Fabric в Azure CLI соответствуют такому шаблону именования:

```azurecli
az sf <object> <action>
```

`<object>`является целевым объектом hello `<action>`.

## <a name="select-a-cluster"></a>Выбор кластера

Прежде чем выполнять любые операции, необходимо выбрать tooconnect кластера для. Пример см. в разделе hello, следующий код. Hello подключает tooan незащищенных кластеров.

> [!WARNING]
> Не используйте незащищенные кластеры Service Fabric в рабочей среде.

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

Конечная точка Hello кластера должен стоять `http` или `https`. Она должна включать hello порт для шлюза hello HTTP. Hello порт и адрес hello равна hello Service Fabric Explorer URL-адрес.

Для кластеров, защищенных с помощью сертификата, можно использовать не зашифрованные PEM-файлы или CRT-файлы и KEY-файлы. Например:

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Дополнительные сведения см. в разделе [кластера Azure Service Fabric безопасное подключение tooa](service-fabric-connect-to-secure-cluster.md).

> [!NOTE]
> Hello `select` перед возвратом команда не действовать на все запросы. tooverify, что вы указали кластер правильно, используйте команды, аналогичной `az sf cluster health`. Убедитесь, что команда hello не возвращает все ошибки.

## <a name="basic-operations"></a>Базовые операции

Сведения о подключении кластера сохраняется между различными сеансами Azure CLI. После выбора кластера Service Fabric, можно запустить любую команду Service Fabric на кластере hello.

Например tooget hello состояние работоспособности кластера Service Fabric, используйте hello следующую команду:

```azurecli
az sf cluster health
```

Команда Hello приводит следующие hello, выходные данные (предполагается, что выходные данные JSON указан в конфигурации hello Azure CLI):

```json
{
  "aggregatedHealthState": "Ok",
  "applicationHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "name": "fabric:/System"
    }
  ],
  "healthEvents": [],
  "nodeHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "id": {
        "id": "66aa824a642124089ee474b398d06a57"
      },
      "name": "_Test_0"
    }
  ],
  "unhealthyEvaluations": []
}
```

## <a name="tips-and-troubleshooting"></a>Рекомендации и устранение неполадок

Может оказаться hello следующие сведения, полезные при возникновении проблем при работе с Service Fabric команд в Azure CLI.

### <a name="convert-a-certificate-from-pfx-toopem-format"></a>Преобразование из формата tooPEM PFX сертификата

Azure CLI поддерживает клиентские сертификаты, такие как PEM-файлы. При использовании PFX-файлы из Windows, необходимо преобразовать формат tooPEM этих сертификатов. tooconvert PEM tooa файл PFX-файла, используйте hello следующую команду:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Дополнительные сведения см. в разделе hello [OpenSSL документации](https://www.openssl.org/docs/).

### <a name="connection-issues"></a>Проблемы с подключением

Некоторые операции могут создавать hello следующие сообщения:

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

Убедитесь, что указан hello, что конечные точки кластера доступен и прослушивания. Кроме того убедитесь, что приветствия пользовательский Интерфейс обозревателя Service Fabric доступен на, узла и порта. hello tooupdate конечной точки, используйте `az sf cluster select`.

### <a name="detailed-logs"></a>Подробные журналы

Подробные журналы часто полезны при отладке или при сообщении о проблеме. Предоставляет глобальный Azure CLI `--debug` флаг, который повышает уровень детализации hello файлов журнала.

### <a name="command-help-and-syntax"></a>Справка и синтаксис для команд

Выполните команды Service Fabric hello же соглашениями, что Azure CLI. Для получения справки по определенной команде или группы команд использовать hello `-h` флаг:

```azurecli
az sf application -h
```

Вот еще один пример:

```azurecli
az sf application create -h
```
