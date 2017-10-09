---
title: "aaaGet работы с Azure Service Fabric CLI (sfctl)"
description: "Узнайте, как toouse hello Azure Service Fabric CLI. Узнайте, как tooconnect tooa кластера и как toomanage приложений."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: f76e8ff65bb38dfb63791da0a23e19b93b337f6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-command-line"></a>Командная строка Azure Service Fabric

Hello Azure Service Fabric CLI (sfctl) — программа командной строки для взаимодействия и управления сущностями Azure Service Fabric. Sfctl можно использовать с кластерами Windows и Linux. Sfctl выполняется на любой платформе, поддерживающей Python.

## <a name="prerequisites"></a>Предварительные требования

Предыдущий tooinstallation убедитесь, что в вашей среде есть python и pip установлен. Дополнительные сведения, взгляните на hello [pip документации quickstart](https://pip.pypa.io/en/latest/quickstart/)и официальные [python установите документацию](https://wiki.python.org/moin/BeginnersGuide/Download).

Хотя оба python 2.7 и 3.6 поддерживаются, рекомендуется toouse python 3.6.

## <a name="install"></a>Установить

Hello Azure Service Fabric CLI (sfctl), представлена в виде пакета python. tooinstall hello последнюю версию запуска:

```bash
pip install sfctl
```

После установки, выполните `sfctl -h` tooget сведения о доступных команд.

## <a name="cli-syntax"></a>Синтаксис CLI

Команды всегда начинаются с префикса `sfctl`. Чтобы получить общие сведения о всех командах, которые можно применять, используйте `sfctl -h`. Для получения сведений об одной команде используйте `sfctl <command> -h`.

Выполните команды repeatable структуры, с целью hello hello команд выше команда hello или действие:

```azurecli
sfctl <object> <action>
```

В этом примере `<object>` является целевым объектом hello `<action>`.

## <a name="select-a-cluster"></a>Выбор кластера

Прежде чем выполнять любые операции, необходимо выбрать tooconnect кластера для. Выполните следующие tooselect hello и подключите toohello кластер с именем hello `testcluster.com`.

> [!WARNING]
> Не используйте незащищенные кластеры Service Fabric в рабочей среде.

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

Конечная точка Hello кластера должен стоять `http` или `https`. Она должна включать hello порт для шлюза hello HTTP. Hello порт и адрес hello равна hello Service Fabric Explorer URL-адрес.

Для кластеров, защищенных с помощью сертификата, можно указать сертификат в кодировке PEM. Hello сертификата можно указать как один файл или сертификат и пара ключей.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Дополнительные сведения см. в разделе [кластера Azure Service Fabric безопасное подключение tooa](service-fabric-connect-to-secure-cluster.md).

## <a name="basic-operations"></a>Базовые операции

Сведения о подключении кластера сохраняются между разными сеансами sfctl. После выбора кластера Service Fabric, можно запустить любую команду Service Fabric на кластере hello.

Например tooget hello состояние работоспособности кластера Service Fabric, используйте hello следующую команду:

```azurecli
sfctl cluster health
```

результаты выполнения команды Hello в hello следующие выходные данные:

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

Некоторые рекомендации и советы по устранению распространенных проблем.

### <a name="convert-a-certificate-from-pfx-toopem-format"></a>Преобразование из формата tooPEM PFX сертификата

Hello службы структуры CLI поддерживает клиентские сертификаты как PEM-файлы (с расширением .pem). При использовании PFX-файлы из Windows, необходимо преобразовать формат tooPEM этих сертификатов. tooconvert PEM tooa файл PFX-файла, используйте следующую команду:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Дополнительные сведения см. в разделе hello [OpenSSL документации](https://www.openssl.org/docs/).

### <a name="connection-issues"></a>Проблемы с подключением

Некоторые операции могут создавать hello следующие сообщения:

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

Убедитесь, что указан hello, что конечные точки кластера доступен и прослушивания. Кроме того убедитесь, что приветствия пользовательский Интерфейс обозревателя Service Fabric доступен на, узла и порта. hello tooupdate конечной точки, используйте `sfctl cluster select`.

### <a name="detailed-logs"></a>Подробные журналы

Подробные журналы часто полезны при отладке или при сообщении о проблеме. Имеется глобальный `--debug` флаг, который повышает уровень детализации hello файлов журнала.

### <a name="command-help-and-syntax"></a>Справка и синтаксис для команд

Для получения справки по определенной команде или группы команд использовать hello `-h` флаг:

```azurecli
sfctl application -h
```

Другой пример:

```azurecli
sfctl application create -h
```

## <a name="next-steps"></a>Дальнейшие действия

* [Развертывание приложения с hello Azure Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md)
* [Prepare your development environment on Linux](service-fabric-get-started-linux.md) (Подготовка среды разработки в Linux)
