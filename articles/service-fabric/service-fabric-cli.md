---
title: "Начало работы с интерфейсом командной строки Azure Service Fabric"
description: "Сведения об использовании интерфейса командной строки Azure Service Fabric. Узнайте, как подключиться к кластеру и как управлять приложениями."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 10/20/2017
ms.author: edwardsa
ms.openlocfilehash: d24c7618c5d53cfe2871d596bfc0fe2cadd5940a
ms.sourcegitcommit: cf4c0ad6a628dfcbf5b841896ab3c78b97d4eafd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/21/2017
---
# <a name="azure-service-fabric-cli"></a>Интерфейс командной строки Azure Service Fabric

Интерфейс командной строки Azure Service Fabric — это служебная программа командной строки для взаимодействия с сущностями Service Fabric и управления ими. Интерфейс командной строки Service Fabric можно использовать с кластерами Windows и Linux. Он выполняется на любой платформе, поддерживающей Python.

[!INCLUDE [links to azure cli and service fabric cli](../../includes/service-fabric-sfctl.md)]

## <a name="prerequisites"></a>Предварительные требования

Прежде чем начать установку, убедитесь, что в вашей среде установлены Python и pip. Дополнительные сведения см. в [кратком руководстве по началу работы с pip](https://pip.pypa.io/en/latest/quickstart/) и официальной [документации по установке Python](https://wiki.python.org/moin/BeginnersGuide/Download).

Интерфейс командной строки поддерживает Python версии 2.7, 3.5 и 3.6. Python 3.6 является рекомендуемой версией, так как поддержка Python 2.7 скоро будет прекращена.

### <a name="service-fabric-target-runtime"></a>Целевая среда выполнения Service Fabric

Интерфейс командной строки Service Fabric используется для поддержки последней версии среды выполнения пакета SDK для Service Fabric. Воспользуйтесь следующей таблицей, чтобы определить, какую версию интерфейса командной строки следует установить.

| Версия интерфейса командной строки   | Поддерживаемая версия среды выполнения |
|---------------|---------------------------|
| Последняя (~=3)  | Последняя (~=6.0)            |
| 1.1.0         | 5.6, 5.7                  |

При необходимости можно указать целевую версию интерфейса командной строки для установки, добавив к команде `pip install` суффикс `==<version>`. Например, для версии 1.1.0 синтаксис будет выглядеть следующим образом:

```
pip install -I sfctl==1.1.0
```

При необходимости замените следующую команду `pip install` ранее упомянутой командой.

Дополнительные сведения о выпусках интерфейса командной строки Service Fabric см. в [документации GitHub](https://github.com/Azure/service-fabric-cli/releases).

## <a name="install-pip-python-and-the-service-fabric-cli"></a>Установка pip, Python и интерфейса командной строки Service Fabric

Существует много способов установки pip и Python на вашей платформе. Ниже приведены действия для быстрой установки Python 3 и pip, которые подходят для большинства операционных систем.

### <a name="windows"></a>Windows

Для Windows 10, Windows Server 2016 и Windows Server 2012 R2 используйте стандартные официальные инструкции по установке. Установщик Python также по умолчанию устанавливает pip.

1. Перейдите на официальную [страницу загрузок Python](https://www.python.org/downloads/) и скачайте последний выпуск Python 3.6.

2. Запустите установщик.

3. В нижней части окна запроса выберите **Add Python 3.6 to PATH** (Добавить Python 3.6 в PATH).

4. Выберите **Install Now** (Установить сейчас) и завершите установку.

Теперь можно открыть новое командное окно, чтобы узнать версию Python и pip.

```bat
python --version
pip --version
```

Затем выполните следующую команду, чтобы установить интерфейс командной строки Service Fabric.

```bat
pip install sfctl
sfctl -h
```

### <a name="ubuntu-and-windows-subsystem-for-linux"></a>Подсистема Ubuntu и Windows для Linux

Чтобы установить интерфейс командной строки Service Fabric, выполните следующие команды.

```bash
sudo apt-get install python3
sudo apt-get install python3-pip
pip3 install sfctl
```

Затем можно проверить установку, выполнив следующую команду.

```bash
sfctl -h
```

Если вы получили ошибку, что команда не найдена, например:

`sfctl: command not found`

Убедитесь, что `~/.local/bin` доступен из `$PATH`.

```bash
export PATH=$PATH:~/.local/bin
echo "export PATH=$PATH:~/.local/bin" >> .bashrc
```

Если установка подсистемы Windows для Linux завершается сбоем из-за неверных разрешений папки, может потребоваться повторить попытку с повышенным уровнем разрешений.

```bash
sudo pip3 install sfctl
```

<a name = "cli-mac"></a>
### <a name="macos"></a>MacOS

Для MacOS мы рекомендуем использовать [диспетчер пакетов HomeBrew](https://brew.sh). Если диспетчер HomeBrew еще не установлен, установите его, выполнив следующую команду:

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Затем с помощью терминала установите Python 3.6, pip и интерфейс командной строки Service Fabric, выполнив следующие команды:

```bash
brew install python3
pip3 install sfctl
sfctl -h
```

## <a name="cli-syntax"></a>Синтаксис CLI

Команды всегда начинаются с префикса `sfctl`. Чтобы получить общие сведения обо всех командах, которые можно применять, используйте `sfctl -h`. Для получения сведений об одной команде используйте `sfctl <command> -h`.

Команды подчиняются повторяющейся структуре, где целевой объект команды указан перед командой (глаголом) или действием.

```azurecli
sfctl <object> <action>
```

В этом примере `<object>` — целевой объект для `<action>`.

## <a name="select-a-cluster"></a>Выбор кластера

Перед выполнением любых операций выберите кластер, к которому нужно подключиться. Например, чтобы выбрать кластер `testcluster.com` и подключиться к нему, выполните следующую команду:

> [!WARNING]
> Не используйте незащищенные кластеры Service Fabric в рабочей среде.

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

Конечная точка кластера должна иметь префикс `http` или `https`. Она должна включать порт для шлюза HTTP. Этот порт и адрес аналогичны URL-адресу Service Fabric Explorer.

Для кластеров, защищенных с помощью сертификата, можно указать сертификат в кодировке PEM. Сертификат можно указать как один файл или как пару "сертификат — ключ". Если это самозаверяющий сертификат, который не подписан центром сертификации (ЦС), вы можете передать параметр `--no-verify` для обхода проверки ЦС.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

Дополнительные сведения см. в статье [Безопасное подключение к кластеру](service-fabric-connect-to-secure-cluster.md).

## <a name="basic-operations"></a>Базовые операции

Сведения о подключении кластера сохраняются между различными сеансами интерфейса командной строки Service Fabric. Выбрав кластер Service Fabric, можно выполнить любую команду Service Fabric в кластере.

Например, чтобы получить сведения о работоспособности кластера Service Fabric, используйте следующую команду:

```azurecli
sfctl cluster health
```

Результаты команды должны быть следующими:

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

В этом разделе приведены рекомендации и советы по устранению распространенных проблем.

### <a name="convert-a-certificate-from-pfx-to-pem-format"></a>Преобразование сертификата PFX в формат PEM

Интерфейс командной строки Service Fabric поддерживает клиентские сертификаты, такие как PEM-файлы. При использовании PFX-файлов из Windows эти сертификаты необходимо преобразовать в формат PEM. Чтобы преобразовать PFX-файл в PEM-файл, используйте следующую команду:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Аналогично, чтобы преобразовать PEM-файл в PFX-файл, можно использовать следующую команду (здесь не нужно вводить пароль):

```bash
openssl  pkcs12 -export -out Certificates.pfx -inkey Certificates.pem -in Certificates.pem -passout pass:'' 
```

Дополнительные сведения см. в [документации по OpenSSL](https://www.openssl.org/docs/).

### <a name="connection-problems"></a>Проблемы с подключением

Некоторые операции могут создавать следующее сообщение:

`Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known`

Убедитесь, что указанная конечная точка кластера доступна и ожидает передачи данных. Также проверьте, доступен ли для этого узла и порта пользовательский интерфейс Service Fabric Explorer. Обновите конечную точку с помощью `sfctl cluster select`.

### <a name="detailed-logs"></a>Подробные журналы

Подробные журналы часто полезны при отладке или при сообщении о проблеме. Глобальный флаг `--debug` повышает уровень детализации файлов журналов.

### <a name="command-help-and-syntax"></a>Справка и синтаксис для команд

Для получения справки по определенной команде или группе команд используйте флаг `-h`.

```azurecli
sfctl application -h
```

Вот еще один пример:

```azurecli
sfctl application create -h
```

## <a name="updating-the-service-fabric-cli"></a>Обновления интерфейса командной строки Service Fabric 

Чтобы обновить интерфейс командной строки Service Fabric, выполните следующие команды (замените параметр `pip` на `pip3` в зависимости от того, какой вы выбрали во время первоначальной установки):

```bash
pip uninstall sfctl
pip install sfctl
```

## <a name="next-steps"></a>Дальнейшие действия

* [Manage an Azure Service Fabric application by using Azure Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) (Управление приложением Azure Service Fabric с помощью интерфейса командной строки Azure Service Fabric)
* [Prepare your development environment on Linux](service-fabric-get-started-linux.md) (Подготовка среды разработки в Linux)
